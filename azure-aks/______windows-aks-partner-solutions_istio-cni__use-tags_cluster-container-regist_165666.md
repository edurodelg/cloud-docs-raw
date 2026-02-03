---
merged_at: 2026-02-04T00:17:48.879679
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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-aks-partner-solutions -->

# Windows AKS partner solutions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Microsoft collaborates with partners to ensure your build, test, deployment, configuration, and monitoring of your applications perform optimally with Windows containers on AKS.

Our third party partners featured in this article have introduction guides to help you start using their solutions with your applications running on Windows containers on AKS.

| Solutions | Partners |
|---|---|
| DevOps |
|

[NGINX](#f5-nginx)[Calico](#calico)[Datadog](#datadog)[New Relic](#new-relic)[Prisma Cloud](#prisma-cloud)[NetApp](#netapp)[Chef](#chef)## DevOps

DevOps streamlines the delivery process, improves collaboration across teams, and enhances software quality, ensuring swift, reliable, and continuous deployment of your Windows-based applications.

### GitLab

The GitLab DevSecOps Platform supports the Microsoft development ecosystem with performance, accessibility testing, SAST, DAST and Fuzzing security scanning, dependency scanning, SBOM, license management and more.

As an extensible platform, GitLab also allows you to plug in your own tooling for any stage. GitLab's integration with Azure Kubernetes Services (AKS) enables full DevSecOps workflows for Windows and Linux Container workloads using either Push CD or GitOps Pull CD with flux manifests. Using Cloud Native Buildpaks, GitLab Auto DevOps can build, test, and autodeploy OSS .NET projects.

To learn more, please our see our [joint blog](https://techcommunity.microsoft.com/t5/containers/using-gitlab-to-build-and-deploy-windows-containers-on-azure/ba-p/3889929).

### CircleCI

CircleCI’s integration with Azure Kubernetes Services (AKS) allows you to automate, build, validate, and ship containerized Windows applications, ensuring faster and more reliable software deployment. You can easily integrate your pipeline with AKS using CircleCI orbs, which are prepacked snippets of YAML configuration.

Follow this [tutorial](https://techcommunity.microsoft.com/t5/containers/continuous-deployment-of-windows-containers-with-circleci-and/ba-p/3841220) to learn how to set up a CI/CD pipeline to build a Dockerized ASP.NET application and deploy it to an AKS cluster.

## Networking

Ensure efficient traffic management, enhanced security, and optimal network performance with these solutions to achieve smooth application connectivity and communication.

### F5 NGINX

NGINX Ingress Controller deployed in AKS, on-premises, and in the cloud implements unified Kubernetes-native API gateways, load balancers, and Ingress controllers to reduce complexity, increase uptime, and provide in-depth insights into app health and performance for containerized Windows workloads.

Running at the edge of a Kubernetes cluster, NGINX Ingress Controller ensures holistic app security with user and service identities, authorization, access control, encrypted communications, and other NGINX App Protect modules for Layer 7 WAF and DoS app protection.

Learn how to manage connectivity to your Windows applications running on Windows nodes in a mixed-node AKS cluster with NGINX Ingress controller in this [blog](https://techcommunity.microsoft.com/t5/containers/improving-customer-experiences-with-f5-nginx-and-windows-on/ba-p/3820344).

### Calico

Tigera provides an active security platform with full-stack observability for containerized workloads and Microsoft AKS as a fully managed SaaS (Calico Cloud) or a self-managed service (Calico Enterprise). The platform prevents, detects, troubleshoots, and automatically mitigates exposure risks of security breaches for workloads in Microsoft AKS.

Its open-source offering, Calico Open Source, is the most widely adopted container networking and security solution. It specifies security and observability as code to ensure consistent enforcement of security policies, which enables DevOps, platform, and security teams to protect workloads, detect threats, achieve continuous compliance, and troubleshoot service issues in real-time.

For more information, see [Securing Windows workloads on Azure Kubernetes Service with Calico](https://techcommunity.microsoft.com/t5/containers/securing-windows-workloads-on-azure-kubernetes-service-with/ba-p/3815429).

## Observability

Observability provides deep insights into your systems, enabling rapid issue detection and resolution to enhance your application’s reliability and performance.

### Datadog

Datadog is the essential monitoring and security platform for cloud applications. We bring together end-to-end traces, metrics, and logs to make your applications, infrastructure, and third-party services entirely observable. Partner with Datadog for Windows on AKS environments to streamline monitoring, proactively resolve issues, and optimize application performance and availability.

Get started by following the recommendations in our [joint blog](https://techcommunity.microsoft.com/t5/containers/gain-full-observability-into-windows-containers-on-azure/ba-p/3853603).

### New Relic

New Relic's Azure Kubernetes integration is a powerful solution that seamlessly connects New Relic's monitoring and observability capabilities with Azure Kubernetes Service (AKS). By deploying the New Relic Kubernetes integration, users gain deep insights into their AKS clusters' performance, health, and resource utilization. This integration allows users to efficiently manage and troubleshoot containerized applications, optimize resource allocation, and proactively identify and resolve issues in their AKS environments. With New Relic's comprehensive monitoring and analysis tools, businesses can ensure the smooth operation and optimal performance of their Kubernetes workloads on Azure.

Check this [blog](https://techcommunity.microsoft.com/t5/containers/leveraging-new-relic-for-instrumentation-of-windows-container-on/ba-p/3870323) for detailed information.

## Security

Ensure the integrity and confidentiality of applications, thereby fostering trust and compliance across your infrastructure.

### Prisma Cloud

Prisma Cloud is a comprehensive Cloud-Native Application Protection Platform (CNAPP) tailor-made to help secure Windows containers on Azure Kubernetes Service (AKS). Gain continuous real-time visibility and control over Windows container environments, including vulnerability and compliance management, identities and permissions, and AI-assisted runtime defense. Integrated container scanning across the pipeline and in Azure Container Registry ensure security throughout the entire application lifecycle.

See [our guidance](https://techcommunity.microsoft.com/t5/containers/unlocking-new-possibilities-with-prisma-cloud-and-windows/ba-p/3866485) for more details.

## Storage

Storage enables standardized and seamless storage interactions, ensuring high application performance and data consistency.

### NetApp

[Astra](https://www.netapp.com/cloud-services/astra/) provides dynamic storage provisioning for stateful workloads on Azure Kubernetes Service (AKS). It also provides data protection using snapshots and clones. Provision SMB volumes through the Kubernetes control plane, making storage seamless and on-demand for all your Windows AKS workloads.

Follow the steps provided in [this blog](https://techcommunity.microsoft.com/t5/azure-architecture-blog/azure-netapp-files-smb-volumes-for-azure-kubernetes-services/ba-p/3052900) post to dynamically provision SMB volumes for Windows AKS workloads.

## Config management

Automate and standardize the system settings across your environments to enhance efficiency, reduce errors, and ensuring system stability and compliance.

### Chef

Chef provides visibility and threat detection from build to runtime that monitors, audits, and remediates the security of your Azure cloud services and Kubernetes and Windows container assets. Chef provides comprehensive visibility and continuous compliance into your cloud security posture and helps limit the risk of misconfigurations in cloud-native environments by providing best practices based on CIS, STIG, SOC2, PCI-DSS and other benchmarks. This is part of a broader compliance offering that supports on-premises or hybrid cloud environments including applications deployed on the edge.

To learn more about Chef’s capabilities, check out the comprehensive ‘how-to’ blog post here: [Securing Your Windows Environments Running on Azure Kubernetes Service with Chef](https://techcommunity.microsoft.com/t5/containers/securing-your-windows-environments-running-on-azure-kubernetes/ba-p/3821830).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-cni -->

# Enable Istio CNI for Istio-based service mesh add-on for Azure Kubernetes Service (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to enable Istio CNI for the Istio-based service mesh add-on on Azure Kubernetes Service (AKS). Istio CNI improves security by eliminating the need for privileged network capabilities in application workloads within the service mesh.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Overview

By default, Istio service mesh uses privileged init containers (`istio-init`

) in each application pod to configure network traffic redirection to the Envoy sidecar proxy. These init containers require `NET_ADMIN`

and `NET_RAW`

capabilities, which are often flagged as security concerns in enterprise environments.

Istio CNI addresses this security concern by moving the network configuration responsibilities from individual pod init containers to a cluster-level CNI plugin. This approach:

**Improves security**: Removes the need for privileged network capabilities (`NET_ADMIN`

,`NET_RAW`

) from application workloads**Simplifies pod security policies**: Application pods only require minimal capabilities**Maintains functionality**: Provides the same traffic management capabilities as the traditional init container approach

When Istio CNI is enabled, application pods use a minimal `istio-validation`

init container that drops all capabilities instead of the privileged `istio-init`

container.

Note

Istio CNI is **not** a replacement for [Azure CNI](concepts-network-cni-overview) and will not interfere with your normal AKS networking. It is a separate plugin designed to handle Istio’s traffic redirection setup at the node level, improving security by removing the need for privileged init containers in application pods.

## Before you begin

Install the Azure CLI version 2.77.0 or later. You can run

`az --version`

to verify the version. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).Install the

`aks-preview`

Azure CLI extension version 19.0.0b5 or later:`az extension add --name aks-preview`

If you already have the

`aks-preview`

extension, update it to the latest version:`az extension update --name aks-preview`

Register the

`IstioCNIPreview`

feature flag on your Azure subscription:`az feature register --namespace "Microsoft.ContainerService" --name "IstioCNIPreview"`

Use the following command to check the registration status:

`az feature show --namespace "Microsoft.ContainerService" --name "IstioCNIPreview"`

It takes a few minutes for the feature to register. Verify the registration state shows

`Registered`

:`{ "id": "/subscriptions/xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/providers/Microsoft.Features/providers/Microsoft.ContainerService/features/IstioCNIPreview", "name": "Microsoft.ContainerService/IstioCNIPreview", "properties": { "state": "Registered" }, "type": "Microsoft.Features/providers/features" }`

You need an AKS cluster with the Istio-based service mesh add-on enabled. If you don't have this setup, see

[Deploy Istio-based service mesh add-on for Azure Kubernetes Service](istio-deploy-addon).Ensure your Istio service mesh is using revision

`asm-1-25`

or later. You can check the current revision with:`az aks show --resource-group <resource-group-name> --name <cluster-name> --query 'serviceMeshProfile.istio.revisions'`


Note

Istio CNI is not compatible with Ubuntu 20.04 node pools. Ensure your cluster uses Ubuntu 22.04 or Azure Linux node pools.

### Set environment variables

```
export CLUSTER=<cluster-name>
export RESOURCE_GROUP=<resource-group-name>
```


## Enable Istio CNI

Use the following command to enable Istio CNI on your AKS cluster:

```
az aks mesh enable-istio-cni --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


## Verify Istio CNI is enabled

Use `az aks get-credentials`

to get the credentials for your AKS cluster:

```
az aks get-credentials --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


After enabling Istio CNI, verify the installation by checking that the CNI DaemonSet is running:

```
kubectl get daemonset -n aks-istio-system
```


You should see the Istio CNI DaemonSet running:

```
NAME DESIRED CURRENT READY UP-TO-DATE AVAILABLE NODE SELECTOR AGE
azure-service-mesh-istio-cni-addon-node 3 3 3 3 3 kubernetes.io/os=linux 94s
```


## Deploy workloads and verify behavior

To verify the security improvement, you can deploy the bookinfo sample application and check that workloads use the secure `istio-validation`

init container instead of the privileged `istio-init`

container.

### Deploy sample application

First, enable sidecar injection for the default namespace:

```
# Get the current Istio revision
REVISION=$(az aks show --resource-group ${RESOURCE_GROUP} --name ${CLUSTER} --query 'serviceMeshProfile.istio.revisions[0]' -o tsv)
# Label the namespace for sidecar injection
kubectl label namespace default istio.io/rev=${REVISION}
```


Deploy the bookinfo sample application:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.25/samples/bookinfo/platform/kube/bookinfo.yaml
```


### Verify secure init container usage

Check that the deployed pods use the secure `istio-validation`

init container instead of `istio-init`

:

```
kubectl get pods -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.spec.initContainers[0].name}{"\t"}{.spec.initContainers[0].securityContext.capabilities}{"\n"}{end}'
```


Expected output should show `istio-validation`

as the init container with dropped capabilities:

```
details-v1-799dc5d847-7x9gl istio-validation {"drop":["ALL"]}
productpage-v1-99d6d698f-89gpj istio-validation {"drop":["ALL"]}
ratings-v1-7545c4bb6c-m7t42 istio-validation {"drop":["ALL"]}
reviews-v1-8679d76d6c-jz4vg istio-validation {"drop":["ALL"]}
reviews-v2-5b9c77895c-b2b7m istio-validation {"drop":["ALL"]}
reviews-v3-5b57874f5f-kk9rt istio-validation {"drop":["ALL"]}
```


You can also check the YAML for a specific pod to verify the security context:

```
kubectl get pod <pod-name> -n <namespace> -o yaml | grep -A 20 -B 25 "name: istio-validation"
```


The output should show that the `istio-validation`

init container has no privileged capabilities:

```
initContainers:
- args:
…
name: istio-validation
…
securityContext:
allowPrivilegeEscalation: false
capabilities:
drop:
- ALL
privileged: false
readOnlyRootFilesystem: true
runAsGroup: 1337
runAsNonRoot: true
runAsUser: 1337
```


## Disable Istio CNI

To disable Istio CNI and return to using traditional init containers, use the following command:

```
az aks mesh disable-istio-cni --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


After disabling Istio CNI:

The CNI DaemonSet will be removed:

`kubectl get daemonset azure-service-mesh-istio-cni-addon-node -n aks-istio-system`

Expected output (no CNI DaemonSet):

`Error from server (NotFound): daemonsets.apps "azure-service-mesh-istio-cni-addon-node" not found`

New workloads will use the traditional

`istio-init`

init container with network capabilities. Restart all existing deployments to pick up the change:`kubectl rollout restart deployment/details-v1 kubectl rollout restart deployment/productpage-v1 kubectl rollout restart deployment/ratings-v1 kubectl rollout restart deployment/reviews-v1 kubectl rollout restart deployment/reviews-v2 kubectl rollout restart deployment/reviews-v3`

Verify init container name and capabilities:

`kubectl get pods -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.spec.initContainers[0].name}{"\t"}{.spec.initContainers[0].securityContext.capabilities}{"\n"}{end}'`

Expected output should show

`istio-init`

with network capabilities:`details-v1-57bc58c559-722v8 istio-init {"add":["NET_ADMIN","NET_RAW"],"drop":["ALL"]} productpage-v1-7bb64f657c-jw6gs istio-init {"add":["NET_ADMIN","NET_RAW"],"drop":["ALL"]} ratings-v1-57d5594c75-4zd49 istio-init {"add":["NET_ADMIN","NET_RAW"],"drop":["ALL"]} reviews-v1-7fd8f9cd59-mdcf9 istio-init {"add":["NET_ADMIN","NET_RAW"],"drop":["ALL"]} reviews-v2-7b8bdc9cdf-k9qgb istio-init {"add":["NET_ADMIN","NET_RAW"],"drop":["ALL"]} reviews-v3-588854d9d7-s2f7j istio-init {"add":["NET_ADMIN","NET_RAW"],"drop":["ALL"]}`

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-tags -->

# Use Azure tags in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

With Azure Kubernetes Service (AKS), you can set Azure tags on an AKS cluster and its related resources using Azure Resource Manager and the Azure CLI. You can also use Kubernetes manifests to set Azure tags for certain resources. Azure tags are a useful tracking resource for certain business processes, such as *chargeback*.

This article explains how to set Azure tags for AKS clusters and related resources.

## Before you begin

Review the following information before you begin:

- Tags set on an AKS cluster apply to all resources related to the cluster, but not the node pools. This operation overwrites the values of existing keys.
- Tags set on a node pool apply only to resources related to that node pool. This operation overwrites the values of existing keys. Resources outside that node pool, including resources for the rest of the cluster and other node pools, are unaffected.
- Public IPs, files, and disks can have tags set by Kubernetes through a Kubernetes manifest. Tags set in this way maintain the Kubernetes values, even if you update them later using a different method. When you remove public IPs, files, or disks through Kubernetes, any tags set by Kubernetes are removed. The tags on those resources that Kubernetes doesn't track remain unaffected.

### Prerequisites

- The Azure CLI version 2.0.59 or later. To find your version, run
`az --version`

. If you need to install it or update your version, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - Kubernetes version 1.20 or later.

### Limitations

- Azure tags have keys that are case-insensitive for operations, such as when you're retrieving a tag by searching the key. In this case, a tag with the specified key is updated or retrieved regardless of casing. Tag values are case-sensitive.
- In AKS, if multiple tags are set with identical keys but different casing, the tags are used in alphabetical order. For example,
`{"Key1": "val1", "kEy1": "val2", "key1": "val3"}`

results in`Key1`

and`val1`

being set. - For shared resources, tags can't determine the split in resource usage on their own.

## Azure tags and AKS clusters

When you create or update an AKS cluster with the `--tags`

parameter, the following are assigned the Azure tags that you specified:

- The AKS cluster itself and its related resources:
- Route table
- Public IP
- Load balancer
- Network security group
- Virtual network
- AKS-managed kubelet msi
- AKS-managed add-on msi
- Private DNS zone associated with the
*private cluster* - Private endpoint associated with the
*private cluster*

- The node resource group

Note

Azure Private DNS only supports 15 tags. For more information, see the [tag resources](/en-us/azure/azure-resource-manager/management/tag-resources).

## Create or update tags on an AKS cluster

### Create a new AKS cluster

Important

If you're using existing resources when you create a new cluster, such as an IP address or route table, the `az aks create`

command overwrites the set of tags. If you delete the cluster later, any tags set by the cluster are removed.

Create a cluster and assign Azure tags using the

command with the`az aks create`

`--tags`

parameter.Note

To set tags on the initial node pool, the virtual machine scale set, and each virtual machine scale set instance associated with the initial node pool, you can also set the

`--nodepool-tags`

parameter.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --tags dept=IT costcenter=9999 \ --generate-ssh-keys`

Verify the tags have been applied to the cluster and its related resources using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --query '[tags]'`

The following example output shows the tags applied to the cluster:

`{ "clusterTags": { "dept": "IT", "costcenter": "9999" } }`


### Update an existing AKS cluster

Important

Setting tags on a cluster using the `az aks update`

command overwrites the set of tags. For example, if your cluster has the tags *dept=IT* and *costcenter=9999*, and you use `az aks update`

with the tags *team=alpha* and *costcenter=1234*, the new list of tags would be *team=alpha* and *costcenter=1234*.

Update the tags on an existing cluster using the

command with the`az aks update`

`--tags`

parameter.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --tags team=alpha costcenter=1234`

Verify the tags have been applied to the cluster and its related resources using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --query '[tags]'`

The following example output shows the tags applied to the cluster:

`{ "clusterTags": { "team": "alpha", "costcenter": "1234" } }`


## Add tags to node pools

You can apply an Azure tag to a new or existing node pool in your AKS cluster. Tags applied to a node pool are applied to each node within the node pool and are persisted through upgrades. Tags are also applied to new nodes that are added to a node pool during scale-out operations. Adding a tag can help with tasks such as policy tracking or cost estimation.

When you create or update a node pool with the `--tags`

parameter, the tags you specify are assigned to the following resources:

- The node pool.
- The virtual machine scale set and each virtual machine scale set instance associated with the node pool.

### Create a new node pool

Create a node pool with an Azure tag using the

command with the`az aks nodepool add`

`--tags`

parameter.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name tagnodepool \ --node-count 1 \ --tags abtest=a costcenter=5555 \ --no-wait`

Verify that the tags have been applied to the node pool using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --query 'agentPoolProfiles[].{nodepoolName:name,tags:tags}'`

The following example output shows the tags applied to the node pool:

`[ { "nodepoolName": "nodepool1", "tags": null }, { "nodepoolName": "tagnodepool", "tags": { "abtest": "a", "costcenter": "5555" } } ]`


### Update an existing node pool

Important

Setting tags on a node pool using the `az aks nodepool update`

command overwrites the set of tags. For example, if your node pool has the tags *abtest=a* and *costcenter=5555*, and you use `az aks nodepool update`

with the tags *appversion=0.0.2* and *costcenter=4444*, the new list of tags would be *appversion=0.0.2* and *costcenter=4444*.

Update a node pool with an Azure tag using the

command.`az aks nodepool update`

`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name tagnodepool \ --tags appversion=0.0.2 costcenter=4444 \ --no-wait`

Verify the tags have been applied to the node pool using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --query 'agentPoolProfiles[].{nodepoolName:name,tags:tags}'`

The following example output shows the tags applied to the node pool:

`[ { "nodepoolName": "nodepool1", "tags": null }, { "nodepoolName": "tagnodepool", "tags": { "appversion": "0.0.2", "costcenter": "4444" } } ]`


## Add tags using Kubernetes

Important

Setting tags on files, disks, and public IPs using Kubernetes updates the set of tags. For example, if your disk has the tags *dept=IT* and *costcenter=5555*, and you use Kubernetes to set the tags *team=beta* and *costcenter=3333*, the new list of tags would be *dept=IT*, *team=beta*, and *costcenter=3333*.

Any updates you make to tags through Kubernetes retain the value set through Kubernetes. For example, if your disk has tags *dept=IT* and *costcenter=5555* set by Kubernetes, and you use the portal to set the tags *team=beta* and *costcenter=3333*, the new list of tags would be *dept=IT*, *team=beta*, and *costcenter=5555*. If you then remove the disk through Kubernetes, the disk would have the tag *team=beta*.

You can apply Azure tags to public IPs, disks, and files using a Kubernetes manifest.

For public IPs, use

*service.beta.kubernetes.io/azure-pip-tags*under*annotations*. For example:`apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-pip-tags: costcenter=3333,team=beta spec: ...`

For files and disks, use

*tags*under*parameters*. For example:`--- apiVersion: storage.k8s.io/v1 ... parameters: ... tags: costcenter=3333,team=beta ...`


## Next steps

Learn more about [using labels in an AKS cluster](use-labels).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/cluster-container-registry-integration -->

# Authenticate with Azure Container Registry (ACR) from Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When using [Azure Container Registry (ACR)](/en-us/azure/container-registry/container-registry-intro) with Azure Kubernetes Service (AKS), you need to establish an authentication mechanism. You can configure the required permissions between ACR and AKS using the Azure CLI, Azure PowerShell, or Azure portal. This article provides examples to configure authentication between these Azure services using the Azure CLI or Azure PowerShell.

The AKS to ACR integration assigns the [ AcrPull role](/en-us/azure/role-based-access-control/built-in-roles#acrpull) to the

[Microsoft Entra ID](/en-us/azure/active-directory/managed-identities-azure-resources/overview)associated with the agent pool in your AKS cluster. For more information on AKS managed identities, see

**managed identity**[Summary of managed identities](managed-identity-overview#summary-of-managed-identities-used-by-aks).

Important

There's a latency issue with Microsoft Entra groups when attaching ACR. If the **AcrPull** role is granted to a Microsoft Entra group and the kubelet identity is added to the group to complete the RBAC configuration, there may be a delay before the RBAC group takes effect. If you're running automation that requires the RBAC configuration to be complete, we recommend you use [Bring your own kubelet identity](use-managed-identity#create-a-kubelet-managed-identity) as a workaround. You can pre-create a user-assigned identity, add it to the Microsoft Entra group, then use the identity as the kubelet identity to create an AKS cluster. This ensures the identity is added to the Microsoft Entra group before a token is generated by kubelet, which avoids the latency issue.

Note

This article covers automatic authentication between AKS and ACR. If you need to pull an image from a private external registry, use an [image pull secret](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/).

Caution

The AKS-ACR integration through `az aks --attach-acr`

is not supported for ABAC-enabled ACR registries where the role assignment permissions mode is set to "RBAC Registry + ABAC Repository Permissions." ABAC-enabled ACR registries require the [ Container Registry Repository Reader role](/en-us/azure/role-based-access-control/built-in-roles#container-registry-repository-reader) instead of the

`AcrPull`

role for granting image pull permissions. For ABAC-enabled ACR registries, you should not use `az aks --attach-acr`

but instead manually assign the `Container Registry Repository Reader`

role assignment using either the Azure Portal, `az role assignment`

CLI, or Azure Resource Manager. Please visit [https://aka.ms/acr/auth/abac](https://aka.ms/acr/auth/abac)for more information on ABAC-enabled ACR registries.

## Before you begin

- You need the
,**Owner**, or**Azure account administrator**role on your Azure subscription.**Azure co-administrator**- To avoid needing one of these roles, you can instead use an existing managed identity to authenticate ACR from AKS. For more information, see
[Use an Azure managed identity to authenticate to an ACR](/en-us/azure/container-registry/container-registry-authentication-managed-identity).

- To avoid needing one of these roles, you can instead use an existing managed identity to authenticate ACR from AKS. For more information, see
- If you're using Azure CLI, this article requires that you're running Azure CLI version 2.7.0 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you're using Azure PowerShell, this article requires that you're running Azure PowerShell version 5.9.0 or later. Run
`Get-InstalledModule -Name Az`

to find the version. If you need to install or upgrade, see[Install Azure PowerShell](/en-us/powershell/azure/install-az-ps). - Examples and syntax to use Terraform for configuring ACR can be found in the
[Terraform reference](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/container_registry).

## Create a new ACR

If you don't already have an ACR, create one using the

command. The following example sets the`az acr create`

`MYACR`

variable to the name of the ACR,*mycontainerregistry*, and uses the variable to create the registry. Your ACR name must be globally unique and use only lowercase letters.`MYACR=mycontainerregistry az acr create --name $MYACR --resource-group myContainerRegistryResourceGroup --sku basic`


## Create a new AKS cluster and integrate with an existing ACR

Create a new AKS cluster and integrate with an existing ACR using the

command with the`az aks create`

. This command allows you to authorize an existing ACR in your subscription and configures the appropriate`--attach-acr`

parameter**AcrPull**role for the managed identity.`MYACR=mycontainerregistry az aks create --name myAKSCluster --resource-group myResourceGroup --generate-ssh-keys --attach-acr $MYACR`

This command may take several minutes to complete.

Note

If you're using an ACR located in a different subscription from your AKS cluster or would prefer to use the ACR

*resource ID*instead of the ACR name, you can do so using the following syntax:`az aks create -n myAKSCluster -g myResourceGroup --generate-ssh-keys --attach-acr /subscriptions/<subscription-id>/resourceGroups/myContainerRegistryResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry`


## Configure ACR integration for an existing AKS cluster

### Attach an ACR to an existing AKS cluster

Integrate an existing ACR with an existing AKS cluster using the

command with the`az aks update`

and a valid value for`--attach-acr`

parameter**acr-name**or**acr-resource-id**.`# Attach using acr-name az aks update --name myAKSCluster --resource-group myResourceGroup --attach-acr <acr-name> # Attach using acr-resource-id az aks update --name myAKSCluster --resource-group myResourceGroup --attach-acr <acr-resource-id>`

Note

The

`az aks update --attach-acr`

command uses the permissions of the user running the command to create the ACR role assignment. This role is assigned to the[kubelet](https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/)managed identity. For more information on AKS managed identities, see[Summary of managed identities](managed-identity-overview#summary-of-managed-identities-used-by-aks).

### Detach an ACR from an AKS cluster

Remove the integration between an ACR and an AKS cluster using the

command with the`az aks update`

and a valid value for`--detach-acr`

parameter**acr-name**or**acr-resource-id**.`# Detach using acr-name az aks update --name myAKSCluster --resource-group myResourceGroup --detach-acr <acr-name> # Detach using acr-resource-id az aks update --name myAKSCluster --resource-group myResourceGroup --detach-acr <acr-resource-id>`


## Working with ACR & AKS

### Import an image into your ACR

Import an image from Docker Hub into your ACR using the

command.`az acr import`

`az acr import --name <acr-name> --source docker.io/library/nginx:latest --image nginx:v1`


### Deploy the sample image from ACR to AKS

Ensure you have the proper AKS credentials using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Create a file called

**acr-nginx.yaml**using the following sample YAML and replace**acr-name**with the name of your ACR.`apiVersion: apps/v1 kind: Deployment metadata: name: nginx0-deployment labels: app: nginx0-deployment spec: replicas: 2 selector: matchLabels: app: nginx0 template: metadata: labels: app: nginx0 spec: containers: - name: nginx image: <acr-name>.azurecr.io/nginx:v1 ports: - containerPort: 80`

Run the deployment in your AKS cluster using the

`kubectl apply`

command.`kubectl apply -f acr-nginx.yaml`

Monitor the deployment using the

`kubectl get pods`

command.`kubectl get pods`

The output should show two running pods, as shown in the following example output:

`NAME READY STATUS RESTARTS AGE nginx0-deployment-669dfc4d4b-x74kr 1/1 Running 0 20s nginx0-deployment-669dfc4d4b-xdpd6 1/1 Running 0 20s`


### Troubleshooting

- Validate the registry is accessible from the AKS cluster using the
command.`az aks check-acr`

- Learn more about
[ACR monitoring](/en-us/azure/container-registry/monitor-service). - Learn more about
[ACR health](/en-us/azure/container-registry/container-registry-check-health).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/create-node-pools -->

# Create node pools for a cluster in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to create one or more node pools in an AKS cluster.

Note

This feature enables more control over creating and managing multiple node pools and requires separate commands for *create/update/delete* (CRUD) operations. Previously, cluster operations through [ az aks create](/en-us/cli/azure/aks#az-aks-create) or

[used the managedCluster API and were the only options to change your control plane and a single node pool. This feature exposes a separate operation set for agent pools through the agentPool API and requires use of the](/en-us/cli/azure/aks#az-aks-update)

`az aks update`

[command set to execute operations on an individual node pool.](/en-us/cli/azure/aks/nodepool)

`az aks nodepool`

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Prerequisites

- You need Azure CLI version 2.2.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

To deploy an ARM template, you need write access on the resources you're deploying and access to all operations on the

`Microsoft.Resources/deployments`

resource type. For example, to deploy a virtual machine (VM), you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).Review the following requirements for each parameter:

`osTYPE`

: The operating system type. The default is Linux.`osSKU`

: Specifies the OS SKU used by the agent pool.`count`

: Number of agents (VMs) to host docker containers. Allowed values must be in the range of 0 to 1000 (inclusive) for user pools and in the range of 1 to 1000 (inclusive) for system pools. The default value is 1.

After you deploy the cluster using an ARM template, you can use Azure CLI or Azure PowerShell to connect to the cluster and deploy the sample application.


## Limitations

The following limitations apply when you create AKS clusters that support multiple node pools:

You can delete the system node pool if you have another system node pool to take its place in the AKS cluster. Otherwise, you can't delete the system node pool.

System pools must contain at least one node. User node pools can contain zero or more nodes.

**If you create a cluster with a single node pool, the OS type must be**. The OS SKU can be any Linux variation such as`Linux`

`Ubuntu`

or`AzureLinux`

. You can't create a cluster with a single Windows node pool. If you want to run Windows containers, you must[add a Windows node pool](#add-a-windows-server-node-pool)to the cluster after creating it with a Linux system node pool.The AKS cluster must use the Standard SKU load balancer to use multiple node pools. This feature isn't supported with Basic SKU load balancers.

The AKS cluster must use Virtual Machine Scale Sets for the nodes.

The name of a node pool can only contain lowercase alphanumeric characters and must begin with a lowercase letter.

- For Linux node pools, the length must be between 1-12 characters.
- For Windows node pools, the length must be between 1-6 characters.

All node pools must reside in the same virtual network.

You can't change the virtual machine (VM) size of a node pool after you create it.

When you create multiple node pools at cluster creation time, the Kubernetes versions for the node pools must match the version set for the control plane. You can make updates after provisioning the cluster using per node pool operations.


## Create specialized node pools

To learn how to create specialized node pools, see the following articles:

[Add an Azure Spot node pool to an AKS cluster](spot-node-pool)[Add a Virtual Machines node pool to an AKS cluster](virtual-machines-node-pools)[Add a dedicated system node pool to an AKS cluster](use-system-pools#add-a-dedicated-system-node-pool-to-an-existing-aks-cluster)[Enabled Federal Information Processing Standards (FIPS) on an AKS node pool](enable-fips-nodes)[Add a node pool with a Confidential Virtual Machine (CVM) on an AKS cluster](use-cvm)[Create node pools with unique subnets in AKS](node-pool-unique-subnet)[Add a generation 2 VM node pool to an AKS cluster](generation-2-vms)[Add a node pool with Artifact Streaming to an AKS cluster](artifact-streaming)[Add Windows Server node pools with](windows-containerd)`containerd`

to an AKS cluster

## Set environment variables

Set the following environment variables in your shell to simplify the commands in this article. You can change the values to your preferred names.

`export RESOURCE_GROUP_NAME="my-aks-rg" export LOCATION="eastus" export CLUSTER_NAME="my-aks-cluster" export NODE_POOL_NAME="mynodepool"`


## Create a resource group

Create an Azure resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP_NAME --location $LOCATION`


## Create an AKS cluster with a single node pool using the Azure CLI

If you want only one node pool in your AKS cluster, you can schedule application pods on system node pools. If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool. If one node goes down, the redundancy is compromised. You can mitigate this risk by having more system node pool nodes.

-
[Create an AKS cluster with a single Ubuntu node pool](#tabpanel_1_ubuntu) -
[Create an AKS cluster with a single Azure Linux node pool](#tabpanel_1_azure-linux) -
[Create an AKS cluster with a single Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_1_os-guard) -
[Create an AKS cluster with a single Flatcar Container Linux for AKS (preview) node pool](#tabpanel_1_flatcar)

Create a cluster with a single Ubuntu node pool using the

command. This step specifies two nodes in the single node pool.`az aks create`

`az aks create \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --vm-set-type VirtualMachineScaleSets \ --node-count 2 \ --os-sku Ubuntu \ --location $LOCATION \ --load-balancer-sku standard \ --generate-ssh-keys`

It takes a few minutes to create the cluster.

When the cluster is ready, get the cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME`


## Add a second node pool using the Azure CLI

The cluster created in the [previous section](#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli) has a single node pool. In this section, we add a second node pool to the cluster. This second node pool can have an OS type of `Linux`

with an OS SKU of `Ubuntu`

or `AzureLinux`

, or an OS type of `Windows`

.

Note

If you want to add a node pool that uses **Ephemeral OS disks** to your AKS cluster, you can set the `--node-osdisk-type`

flag to `Ephemeral`

when running the `az aks nodepool add`

command.

With Ephemeral OS, you can deploy VMs and instance images up to the size of the VM cache. The default node OS disk configuration in AKS uses 128 GB, which means that you need a VM size that has a cache larger than 128 GB. The default `Standard_DS2_v2`

has a cache size of 86 GB, which isn't large enough. The `Standard_DS3_v2`

VM SKU has a cache size of 172 GB, which is large enough. You can also reduce the default size of the OS disk using `--node-osdisk-size`

, but keep in mind the minimum size for AKS images is 30 GB.

If you want to create node pools with **network-attached OS disks**, you can set the `--node-osdisk-type`

flag to `Managed`

when running the `az aks nodepool add`

command.

### Add a Linux node pool

-
[Add an Ubuntu node pool](#tabpanel_2_ubuntu) -
[Add an Azure Linux node pool](#tabpanel_2_azure-linux) -
[Add an Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_2_os-guard) -
[Add a Flatcar Container Linux for AKS (preview) node pool](#tabpanel_2_flatcar)

Create a new node pool using the

command. The following example creates a`az aks nodepool add`

`Linux`

node pool with the`Ubuntu`

OS SKU that runs*three*nodes. If you don't specify an OS SKU, AKS defaults to`Ubuntu`

.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-vm-size Standard_DS2_v2 \ --os-type Linux \ --os-sku Ubuntu \ --node-count 3`

It takes a few minutes to create the node pool.


### Add a Windows Server node pool

##### Install the `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


##### Register the `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


##### Create the Windows Server 2025 node pool

Create a new node pool using the

command. The following example creates a`az aks nodepool add`

`Windows`

node pool with the`Windows2025`

OS SKU that runs*three*nodes.For more information about Windows OS, see

[Windows best practices](windows-best-practices).`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-vm-size Standard_DS2_v2 \ --os-type Windows \ --os-sku Windows2025 \ --node-count 3`


## Check the status of your node pools

Check the status of your node pools using the

command and specify your resource group and cluster name.`az aks nodepool list`

`az aks nodepool list --resource-group $RESOURCE_GROUP_NAME --cluster-name $CLUSTER_NAME`


## Create an AKS cluster with a single node pool using an ARM template

If you want only one node pool in your AKS cluster, you can schedule application pods on system node pools. If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool. If one node goes down, the redundancy is compromised. You can mitigate this risk by having more system node pool nodes.

### Create a `Microsoft.ContainerService/managedClusters`

resource

- Create a
`Microsoft.ContainerService/managedClusters`

resource by adding[this JSON](/en-us/azure/templates/microsoft.containerservice/managedclusters?pivots=deployment-language-arm-template)to your template.

-
[Modify JSON to create a single Ubuntu node pool](#tabpanel_4_ubuntu-arm) -
[Modify JSON to create a single Azure Linux node pool](#tabpanel_4_azure-linux-arm) -
[Modify JSON to create a single Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_4_os-guard-arm) -
[Modify JSON to create a single Flatcar Container Linux for AKS (preview) node pool](#tabpanel_4_flatcar-arm)

Create a single Ubuntu node pool in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "1", "osSKU": "ubuntu", "osType": "linux" } ], }`


## Add a second node pool using an ARM template

The cluster created in the [previous section](#create-an-aks-cluster-with-a-single-node-pool-using-an-arm-template) has a single node pool. In this section, we add a second node pool to the cluster. This second node pool can have an OS type of `Linux`

with an OS SKU of `Ubuntu`

or `AzureLinux`

, or an OS type of `Windows`

.

### Add Linux node pools

-
[Modify JSON to create multiple Ubuntu node pools](#tabpanel_5_ubuntu-arm) -
[Modify JSON to create multiple Azure Linux node pools](#tabpanel_5_azure-linux-arm) -
[Modify JSON to create multiple Azure Linux with OS Guard for AKS (preview) node pools](#tabpanel_5_os-guard-arm) -
[Modify JSON to create multiple Flatcar Container Linux for AKS (preview) node pools](#tabpanel_5_flatcar-arm)

Create multiple Ubuntu node pools in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "3", "osSKU": "ubuntu", "osType": "linux" } ], }`


### Add Windows Server node pools

-
[Modify JSON to create multiple Windows Server 2025 (preview) node pools](#tabpanel_6_ws2025-arm) -
[Modify JSON to create multiple Windows Server 2022 node pools](#tabpanel_6_ws2022-arm)

##### Install the `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


##### Register the `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


##### Create the Windows Server 2025 node pools

Create multiple Windows node pools in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "3", "osSKU": "windows2025", "osType": "windows" } ], }`


## Deploy your ARM template

- Deploy your ARM template by following the guidance in
[Deploy an Azure Kubernetes Service (AKS) cluster using an ARM template](learn/quick-kubernetes-deploy-rm-template).

## Set taints, labels, or tags for a node pool

When creating a node pool, you can add taints, labels, or tags to it. When you add a taint, label, or tag, all nodes within that node pool also get that taint, label, or tag. We recommend applying these properties to an entire node pool instead of individual nodes. This way, you can easily manage the properties of all nodes in the node pool by updating the node pool properties instead of updating each node individually.

For specific instructions on how to set taints, labels, or tags for a node pool, use the following resources:

[Use node taints in an Azure Kubernetes Service (AKS) cluster](use-node-taints)[Use labels in an Azure Kubernetes Service (AKS) cluster](use-labels)[Use Azure tags in Azure Kubernetes Service (AKS)](use-tags)[Provide dedicated nodes using taints and tolerations in Azure Kubernetes Service (AKS)](operator-best-practices-advanced-scheduler#provide-dedicated-nodes-using-taints-and-tolerations)

## Next steps

In this article, you learned how to create an AKS cluster with a single node pool and add additional node pools to your cluster. To learn more about how to manage your node pools, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/manage-node-pools -->

# Create node pools for a cluster in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to create one or more node pools in an AKS cluster.

Note

This feature enables more control over creating and managing multiple node pools and requires separate commands for *create/update/delete* (CRUD) operations. Previously, cluster operations through [ az aks create](/en-us/cli/azure/aks#az-aks-create) or

[used the managedCluster API and were the only options to change your control plane and a single node pool. This feature exposes a separate operation set for agent pools through the agentPool API and requires use of the](/en-us/cli/azure/aks#az-aks-update)

`az aks update`

[command set to execute operations on an individual node pool.](/en-us/cli/azure/aks/nodepool)

`az aks nodepool`

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Prerequisites

- You need Azure CLI version 2.2.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

To deploy an ARM template, you need write access on the resources you're deploying and access to all operations on the

`Microsoft.Resources/deployments`

resource type. For example, to deploy a virtual machine (VM), you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).Review the following requirements for each parameter:

`osTYPE`

: The operating system type. The default is Linux.`osSKU`

: Specifies the OS SKU used by the agent pool.`count`

: Number of agents (VMs) to host docker containers. Allowed values must be in the range of 0 to 1000 (inclusive) for user pools and in the range of 1 to 1000 (inclusive) for system pools. The default value is 1.

After you deploy the cluster using an ARM template, you can use Azure CLI or Azure PowerShell to connect to the cluster and deploy the sample application.


## Limitations

The following limitations apply when you create AKS clusters that support multiple node pools:

You can delete the system node pool if you have another system node pool to take its place in the AKS cluster. Otherwise, you can't delete the system node pool.

System pools must contain at least one node. User node pools can contain zero or more nodes.

**If you create a cluster with a single node pool, the OS type must be**. The OS SKU can be any Linux variation such as`Linux`

`Ubuntu`

or`AzureLinux`

. You can't create a cluster with a single Windows node pool. If you want to run Windows containers, you must[add a Windows node pool](#add-a-windows-server-node-pool)to the cluster after creating it with a Linux system node pool.The AKS cluster must use the Standard SKU load balancer to use multiple node pools. This feature isn't supported with Basic SKU load balancers.

The AKS cluster must use Virtual Machine Scale Sets for the nodes.

The name of a node pool can only contain lowercase alphanumeric characters and must begin with a lowercase letter.

- For Linux node pools, the length must be between 1-12 characters.
- For Windows node pools, the length must be between 1-6 characters.

All node pools must reside in the same virtual network.

You can't change the virtual machine (VM) size of a node pool after you create it.

When you create multiple node pools at cluster creation time, the Kubernetes versions for the node pools must match the version set for the control plane. You can make updates after provisioning the cluster using per node pool operations.


## Create specialized node pools

To learn how to create specialized node pools, see the following articles:

[Add an Azure Spot node pool to an AKS cluster](spot-node-pool)[Add a Virtual Machines node pool to an AKS cluster](virtual-machines-node-pools)[Add a dedicated system node pool to an AKS cluster](use-system-pools#add-a-dedicated-system-node-pool-to-an-existing-aks-cluster)[Enabled Federal Information Processing Standards (FIPS) on an AKS node pool](enable-fips-nodes)[Add a node pool with a Confidential Virtual Machine (CVM) on an AKS cluster](use-cvm)[Create node pools with unique subnets in AKS](node-pool-unique-subnet)[Add a generation 2 VM node pool to an AKS cluster](generation-2-vms)[Add a node pool with Artifact Streaming to an AKS cluster](artifact-streaming)[Add Windows Server node pools with](windows-containerd)`containerd`

to an AKS cluster

## Set environment variables

Set the following environment variables in your shell to simplify the commands in this article. You can change the values to your preferred names.

`export RESOURCE_GROUP_NAME="my-aks-rg" export LOCATION="eastus" export CLUSTER_NAME="my-aks-cluster" export NODE_POOL_NAME="mynodepool"`


## Create a resource group

Create an Azure resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP_NAME --location $LOCATION`


## Create an AKS cluster with a single node pool using the Azure CLI

If you want only one node pool in your AKS cluster, you can schedule application pods on system node pools. If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool. If one node goes down, the redundancy is compromised. You can mitigate this risk by having more system node pool nodes.

-
[Create an AKS cluster with a single Ubuntu node pool](#tabpanel_1_ubuntu) -
[Create an AKS cluster with a single Azure Linux node pool](#tabpanel_1_azure-linux) -
[Create an AKS cluster with a single Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_1_os-guard) -
[Create an AKS cluster with a single Flatcar Container Linux for AKS (preview) node pool](#tabpanel_1_flatcar)

Create a cluster with a single Ubuntu node pool using the

command. This step specifies two nodes in the single node pool.`az aks create`

`az aks create \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --vm-set-type VirtualMachineScaleSets \ --node-count 2 \ --os-sku Ubuntu \ --location $LOCATION \ --load-balancer-sku standard \ --generate-ssh-keys`

It takes a few minutes to create the cluster.

When the cluster is ready, get the cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME`


## Add a second node pool using the Azure CLI

The cluster created in the [previous section](#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli) has a single node pool. In this section, we add a second node pool to the cluster. This second node pool can have an OS type of `Linux`

with an OS SKU of `Ubuntu`

or `AzureLinux`

, or an OS type of `Windows`

.

Note

If you want to add a node pool that uses **Ephemeral OS disks** to your AKS cluster, you can set the `--node-osdisk-type`

flag to `Ephemeral`

when running the `az aks nodepool add`

command.

With Ephemeral OS, you can deploy VMs and instance images up to the size of the VM cache. The default node OS disk configuration in AKS uses 128 GB, which means that you need a VM size that has a cache larger than 128 GB. The default `Standard_DS2_v2`

has a cache size of 86 GB, which isn't large enough. The `Standard_DS3_v2`

VM SKU has a cache size of 172 GB, which is large enough. You can also reduce the default size of the OS disk using `--node-osdisk-size`

, but keep in mind the minimum size for AKS images is 30 GB.

If you want to create node pools with **network-attached OS disks**, you can set the `--node-osdisk-type`

flag to `Managed`

when running the `az aks nodepool add`

command.

### Add a Linux node pool

-
[Add an Ubuntu node pool](#tabpanel_2_ubuntu) -
[Add an Azure Linux node pool](#tabpanel_2_azure-linux) -
[Add an Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_2_os-guard) -
[Add a Flatcar Container Linux for AKS (preview) node pool](#tabpanel_2_flatcar)

Create a new node pool using the

command. The following example creates a`az aks nodepool add`

`Linux`

node pool with the`Ubuntu`

OS SKU that runs*three*nodes. If you don't specify an OS SKU, AKS defaults to`Ubuntu`

.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-vm-size Standard_DS2_v2 \ --os-type Linux \ --os-sku Ubuntu \ --node-count 3`

It takes a few minutes to create the node pool.


### Add a Windows Server node pool

##### Install the `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


##### Register the `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


##### Create the Windows Server 2025 node pool

Create a new node pool using the

command. The following example creates a`az aks nodepool add`

`Windows`

node pool with the`Windows2025`

OS SKU that runs*three*nodes.For more information about Windows OS, see

[Windows best practices](windows-best-practices).`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-vm-size Standard_DS2_v2 \ --os-type Windows \ --os-sku Windows2025 \ --node-count 3`


## Check the status of your node pools

Check the status of your node pools using the

command and specify your resource group and cluster name.`az aks nodepool list`

`az aks nodepool list --resource-group $RESOURCE_GROUP_NAME --cluster-name $CLUSTER_NAME`


## Create an AKS cluster with a single node pool using an ARM template

If you want only one node pool in your AKS cluster, you can schedule application pods on system node pools. If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool. If one node goes down, the redundancy is compromised. You can mitigate this risk by having more system node pool nodes.

### Create a `Microsoft.ContainerService/managedClusters`

resource

- Create a
`Microsoft.ContainerService/managedClusters`

resource by adding[this JSON](/en-us/azure/templates/microsoft.containerservice/managedclusters?pivots=deployment-language-arm-template)to your template.

-
[Modify JSON to create a single Ubuntu node pool](#tabpanel_4_ubuntu-arm) -
[Modify JSON to create a single Azure Linux node pool](#tabpanel_4_azure-linux-arm) -
[Modify JSON to create a single Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_4_os-guard-arm) -
[Modify JSON to create a single Flatcar Container Linux for AKS (preview) node pool](#tabpanel_4_flatcar-arm)

Create a single Ubuntu node pool in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "1", "osSKU": "ubuntu", "osType": "linux" } ], }`


## Add a second node pool using an ARM template

The cluster created in the [previous section](#create-an-aks-cluster-with-a-single-node-pool-using-an-arm-template) has a single node pool. In this section, we add a second node pool to the cluster. This second node pool can have an OS type of `Linux`

with an OS SKU of `Ubuntu`

or `AzureLinux`

, or an OS type of `Windows`

.

### Add Linux node pools

-
[Modify JSON to create multiple Ubuntu node pools](#tabpanel_5_ubuntu-arm) -
[Modify JSON to create multiple Azure Linux node pools](#tabpanel_5_azure-linux-arm) -
[Modify JSON to create multiple Azure Linux with OS Guard for AKS (preview) node pools](#tabpanel_5_os-guard-arm) -
[Modify JSON to create multiple Flatcar Container Linux for AKS (preview) node pools](#tabpanel_5_flatcar-arm)

Create multiple Ubuntu node pools in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "3", "osSKU": "ubuntu", "osType": "linux" } ], }`


### Add Windows Server node pools

-
[Modify JSON to create multiple Windows Server 2025 (preview) node pools](#tabpanel_6_ws2025-arm) -
[Modify JSON to create multiple Windows Server 2022 node pools](#tabpanel_6_ws2022-arm)

##### Install the `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


##### Register the `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


##### Create the Windows Server 2025 node pools

Create multiple Windows node pools in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "3", "osSKU": "windows2025", "osType": "windows" } ], }`


## Deploy your ARM template

- Deploy your ARM template by following the guidance in
[Deploy an Azure Kubernetes Service (AKS) cluster using an ARM template](learn/quick-kubernetes-deploy-rm-template).

## Set taints, labels, or tags for a node pool

When creating a node pool, you can add taints, labels, or tags to it. When you add a taint, label, or tag, all nodes within that node pool also get that taint, label, or tag. We recommend applying these properties to an entire node pool instead of individual nodes. This way, you can easily manage the properties of all nodes in the node pool by updating the node pool properties instead of updating each node individually.

For specific instructions on how to set taints, labels, or tags for a node pool, use the following resources:

[Use node taints in an Azure Kubernetes Service (AKS) cluster](use-node-taints)[Use labels in an Azure Kubernetes Service (AKS) cluster](use-labels)[Use Azure tags in Azure Kubernetes Service (AKS)](use-tags)[Provide dedicated nodes using taints and tolerations in Azure Kubernetes Service (AKS)](operator-best-practices-advanced-scheduler#provide-dedicated-nodes-using-taints-and-tolerations)

## Next steps

In this article, you learned how to create an AKS cluster with a single node pool and add additional node pools to your cluster. To learn more about how to manage your node pools, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-multiple-node-pools -->

# Create node pools for a cluster in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to create one or more node pools in an AKS cluster.

Note

This feature enables more control over creating and managing multiple node pools and requires separate commands for *create/update/delete* (CRUD) operations. Previously, cluster operations through [ az aks create](/en-us/cli/azure/aks#az-aks-create) or

[used the managedCluster API and were the only options to change your control plane and a single node pool. This feature exposes a separate operation set for agent pools through the agentPool API and requires use of the](/en-us/cli/azure/aks#az-aks-update)

`az aks update`

[command set to execute operations on an individual node pool.](/en-us/cli/azure/aks/nodepool)

`az aks nodepool`

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Prerequisites

- You need Azure CLI version 2.2.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

To deploy an ARM template, you need write access on the resources you're deploying and access to all operations on the

`Microsoft.Resources/deployments`

resource type. For example, to deploy a virtual machine (VM), you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).Review the following requirements for each parameter:

`osTYPE`

: The operating system type. The default is Linux.`osSKU`

: Specifies the OS SKU used by the agent pool.`count`

: Number of agents (VMs) to host docker containers. Allowed values must be in the range of 0 to 1000 (inclusive) for user pools and in the range of 1 to 1000 (inclusive) for system pools. The default value is 1.

After you deploy the cluster using an ARM template, you can use Azure CLI or Azure PowerShell to connect to the cluster and deploy the sample application.


## Limitations

The following limitations apply when you create AKS clusters that support multiple node pools:

You can delete the system node pool if you have another system node pool to take its place in the AKS cluster. Otherwise, you can't delete the system node pool.

System pools must contain at least one node. User node pools can contain zero or more nodes.

**If you create a cluster with a single node pool, the OS type must be**. The OS SKU can be any Linux variation such as`Linux`

`Ubuntu`

or`AzureLinux`

. You can't create a cluster with a single Windows node pool. If you want to run Windows containers, you must[add a Windows node pool](#add-a-windows-server-node-pool)to the cluster after creating it with a Linux system node pool.The AKS cluster must use the Standard SKU load balancer to use multiple node pools. This feature isn't supported with Basic SKU load balancers.

The AKS cluster must use Virtual Machine Scale Sets for the nodes.

The name of a node pool can only contain lowercase alphanumeric characters and must begin with a lowercase letter.

- For Linux node pools, the length must be between 1-12 characters.
- For Windows node pools, the length must be between 1-6 characters.

All node pools must reside in the same virtual network.

You can't change the virtual machine (VM) size of a node pool after you create it.

When you create multiple node pools at cluster creation time, the Kubernetes versions for the node pools must match the version set for the control plane. You can make updates after provisioning the cluster using per node pool operations.


## Create specialized node pools

To learn how to create specialized node pools, see the following articles:

[Add an Azure Spot node pool to an AKS cluster](spot-node-pool)[Add a Virtual Machines node pool to an AKS cluster](virtual-machines-node-pools)[Add a dedicated system node pool to an AKS cluster](use-system-pools#add-a-dedicated-system-node-pool-to-an-existing-aks-cluster)[Enabled Federal Information Processing Standards (FIPS) on an AKS node pool](enable-fips-nodes)[Add a node pool with a Confidential Virtual Machine (CVM) on an AKS cluster](use-cvm)[Create node pools with unique subnets in AKS](node-pool-unique-subnet)[Add a generation 2 VM node pool to an AKS cluster](generation-2-vms)[Add a node pool with Artifact Streaming to an AKS cluster](artifact-streaming)[Add Windows Server node pools with](windows-containerd)`containerd`

to an AKS cluster

## Set environment variables

Set the following environment variables in your shell to simplify the commands in this article. You can change the values to your preferred names.

`export RESOURCE_GROUP_NAME="my-aks-rg" export LOCATION="eastus" export CLUSTER_NAME="my-aks-cluster" export NODE_POOL_NAME="mynodepool"`


## Create a resource group

Create an Azure resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP_NAME --location $LOCATION`


## Create an AKS cluster with a single node pool using the Azure CLI

If you want only one node pool in your AKS cluster, you can schedule application pods on system node pools. If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool. If one node goes down, the redundancy is compromised. You can mitigate this risk by having more system node pool nodes.

-
[Create an AKS cluster with a single Ubuntu node pool](#tabpanel_1_ubuntu) -
[Create an AKS cluster with a single Azure Linux node pool](#tabpanel_1_azure-linux) -
[Create an AKS cluster with a single Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_1_os-guard) -
[Create an AKS cluster with a single Flatcar Container Linux for AKS (preview) node pool](#tabpanel_1_flatcar)

Create a cluster with a single Ubuntu node pool using the

command. This step specifies two nodes in the single node pool.`az aks create`

`az aks create \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --vm-set-type VirtualMachineScaleSets \ --node-count 2 \ --os-sku Ubuntu \ --location $LOCATION \ --load-balancer-sku standard \ --generate-ssh-keys`

It takes a few minutes to create the cluster.

When the cluster is ready, get the cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME`


## Add a second node pool using the Azure CLI

The cluster created in the [previous section](#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli) has a single node pool. In this section, we add a second node pool to the cluster. This second node pool can have an OS type of `Linux`

with an OS SKU of `Ubuntu`

or `AzureLinux`

, or an OS type of `Windows`

.

Note

If you want to add a node pool that uses **Ephemeral OS disks** to your AKS cluster, you can set the `--node-osdisk-type`

flag to `Ephemeral`

when running the `az aks nodepool add`

command.

With Ephemeral OS, you can deploy VMs and instance images up to the size of the VM cache. The default node OS disk configuration in AKS uses 128 GB, which means that you need a VM size that has a cache larger than 128 GB. The default `Standard_DS2_v2`

has a cache size of 86 GB, which isn't large enough. The `Standard_DS3_v2`

VM SKU has a cache size of 172 GB, which is large enough. You can also reduce the default size of the OS disk using `--node-osdisk-size`

, but keep in mind the minimum size for AKS images is 30 GB.

If you want to create node pools with **network-attached OS disks**, you can set the `--node-osdisk-type`

flag to `Managed`

when running the `az aks nodepool add`

command.

### Add a Linux node pool

-
[Add an Ubuntu node pool](#tabpanel_2_ubuntu) -
[Add an Azure Linux node pool](#tabpanel_2_azure-linux) -
[Add an Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_2_os-guard) -
[Add a Flatcar Container Linux for AKS (preview) node pool](#tabpanel_2_flatcar)

Create a new node pool using the

command. The following example creates a`az aks nodepool add`

`Linux`

node pool with the`Ubuntu`

OS SKU that runs*three*nodes. If you don't specify an OS SKU, AKS defaults to`Ubuntu`

.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-vm-size Standard_DS2_v2 \ --os-type Linux \ --os-sku Ubuntu \ --node-count 3`

It takes a few minutes to create the node pool.


### Add a Windows Server node pool

##### Install the `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


##### Register the `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


##### Create the Windows Server 2025 node pool

Create a new node pool using the

command. The following example creates a`az aks nodepool add`

`Windows`

node pool with the`Windows2025`

OS SKU that runs*three*nodes.For more information about Windows OS, see

[Windows best practices](windows-best-practices).`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-vm-size Standard_DS2_v2 \ --os-type Windows \ --os-sku Windows2025 \ --node-count 3`


## Check the status of your node pools

Check the status of your node pools using the

command and specify your resource group and cluster name.`az aks nodepool list`

`az aks nodepool list --resource-group $RESOURCE_GROUP_NAME --cluster-name $CLUSTER_NAME`


## Create an AKS cluster with a single node pool using an ARM template

If you want only one node pool in your AKS cluster, you can schedule application pods on system node pools. If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool. If one node goes down, the redundancy is compromised. You can mitigate this risk by having more system node pool nodes.

### Create a `Microsoft.ContainerService/managedClusters`

resource

- Create a
`Microsoft.ContainerService/managedClusters`

resource by adding[this JSON](/en-us/azure/templates/microsoft.containerservice/managedclusters?pivots=deployment-language-arm-template)to your template.

-
[Modify JSON to create a single Ubuntu node pool](#tabpanel_4_ubuntu-arm) -
[Modify JSON to create a single Azure Linux node pool](#tabpanel_4_azure-linux-arm) -
[Modify JSON to create a single Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_4_os-guard-arm) -
[Modify JSON to create a single Flatcar Container Linux for AKS (preview) node pool](#tabpanel_4_flatcar-arm)

Create a single Ubuntu node pool in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "1", "osSKU": "ubuntu", "osType": "linux" } ], }`


## Add a second node pool using an ARM template

The cluster created in the [previous section](#create-an-aks-cluster-with-a-single-node-pool-using-an-arm-template) has a single node pool. In this section, we add a second node pool to the cluster. This second node pool can have an OS type of `Linux`

with an OS SKU of `Ubuntu`

or `AzureLinux`

, or an OS type of `Windows`

.

### Add Linux node pools

-
[Modify JSON to create multiple Ubuntu node pools](#tabpanel_5_ubuntu-arm) -
[Modify JSON to create multiple Azure Linux node pools](#tabpanel_5_azure-linux-arm) -
[Modify JSON to create multiple Azure Linux with OS Guard for AKS (preview) node pools](#tabpanel_5_os-guard-arm) -
[Modify JSON to create multiple Flatcar Container Linux for AKS (preview) node pools](#tabpanel_5_flatcar-arm)

Create multiple Ubuntu node pools in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "3", "osSKU": "ubuntu", "osType": "linux" } ], }`


### Add Windows Server node pools

-
[Modify JSON to create multiple Windows Server 2025 (preview) node pools](#tabpanel_6_ws2025-arm) -
[Modify JSON to create multiple Windows Server 2022 node pools](#tabpanel_6_ws2022-arm)

##### Install the `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


##### Register the `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


##### Create the Windows Server 2025 node pools

Create multiple Windows node pools in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "3", "osSKU": "windows2025", "osType": "windows" } ], }`


## Deploy your ARM template

- Deploy your ARM template by following the guidance in
[Deploy an Azure Kubernetes Service (AKS) cluster using an ARM template](learn/quick-kubernetes-deploy-rm-template).

## Set taints, labels, or tags for a node pool

When creating a node pool, you can add taints, labels, or tags to it. When you add a taint, label, or tag, all nodes within that node pool also get that taint, label, or tag. We recommend applying these properties to an entire node pool instead of individual nodes. This way, you can easily manage the properties of all nodes in the node pool by updating the node pool properties instead of updating each node individually.

For specific instructions on how to set taints, labels, or tags for a node pool, use the following resources:

[Use node taints in an Azure Kubernetes Service (AKS) cluster](use-node-taints)[Use labels in an Azure Kubernetes Service (AKS) cluster](use-labels)[Use Azure tags in Azure Kubernetes Service (AKS)](use-tags)[Provide dedicated nodes using taints and tolerations in Azure Kubernetes Service (AKS)](operator-best-practices-advanced-scheduler#provide-dedicated-nodes-using-taints-and-tolerations)

## Next steps

In this article, you learned how to create an AKS cluster with a single node pool and add additional node pools to your cluster. To learn more about how to manage your node pools, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-aks-customer-stories -->

# Windows AKS customer stories

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Explore how various industries are using Windows Containers on Azure Kubernetes Service (AKS) for seamless Kubernetes integration with minimal code modifications.

Learn directly from the customer stories listed here.

## Customer stories

### Finastra

LaserPro document management software is key to the Finastra vision of delivering the future of banking. Migrating from an on-premises management system to a cloud-based infrastructure using Windows containers on Azure Kubernetes Service has significantly increased agility through biweekly updates and reduced support costs for both customers and developers.

For more information visit [Finastra's Windows AKS customer story](https://customers.microsoft.com/en-us/story/1759082810297807726-finastra-azure-kubernetes-service-professional-services-en-united-kingdom).

### Relativity

Relativity, transitioned from virtual machines to Windows containers on Azure Kubernetes Service (AKS) to modernize its Windows code base, streamline development, and improve scalability.

This shift enabled faster, more cost-effective deployment of their products and services without rewriting millions of lines of code. The transition to a containerized architecture significantly reduced deployment cycles from six months to a single day, enhancing the speed and flexibility of Relativity’s engineering teams and leading to better performance and security in their application delivery.

For more information visit [Relativity’s Windows AKS customer story](https://customers.microsoft.com/story/1516554049543037694-windows-containers-helps-relativity-boost-reliability-security).

### Duck Creek

Duck Creek Technologies modernized its insurance software solutions by adopting Windows containers on Azure Kubernetes Service (AKS), significantly enhancing operational efficiency and reducing time to market for new features. This transition to AKS enabled Duck Creek to offer scalable, reliable, and up-to-date SaaS solutions to its insurance clients, supporting rapid deployment and active delivery of updates.

By containerizing their applications to Windows Containers, Duck Creek could maintain the flexibility and robustness of their products without extensive code rewriting, thereby ensuring high availability and scalability, especially critical during peak demand periods like natural disasters. This move represents Duck Creek's commitment to leveraging cutting-edge technology for Insurtech innovation.

### Forza

Forza Horizon 5, developed by Turn 10 Studios, achieved remarkable performance and scalability by transitioning to Azure Kubernetes Service (AKS) with Windows-based containers. This shift allowed the team to adapt swiftly to demand spikes, handling over 10 million concurrent players at launch, the biggest first week in Xbox Game Studios history.

By utilizing Windows AKS, they were able to significantly reduce infrastructure management tasks, enhancing both the development process and the gaming experience. The move to containerized architecture enabled rapid scaling from 600,000 to 3 million concurrent users and reduced infrastructure costs, demonstrating the effectiveness of AKS in high-demand, low-latency environments like gaming.

For more information visit [Forza Horizon 5 runs on Windows containers on Azure Kubernetes Services](https://techcommunity.microsoft.com/blog/itopstalkblog/forza-horizon-5-runs-on-windows-containers-on-azure-kubernetes-services/3570404).

### Microsoft Experience + Devices

Microsoft's E+D group, responsible for supporting products such as Teams and Office modernized the Microsoft 365 infrastructure by transitioning to Windows containers on Azure Kubernetes Service (AKS), aiming for more consistent, efficient DevOps within strict security and compliance frameworks.

The transition enabled Microsoft 365 developers to focus more on innovation and iterating quickly, leveraging the benefits of AKS like security-optimized hosting, automated compliance checks, and centralized capacity management, thereby accelerating development while optimizing resource utilization and costs.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices-ml-ops -->

# Machine learning operations (MLOps) best practices in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes best practices and considerations to keep in mind when using MLOps in AKS. For more information on MLOps, see [Machine learning operations (MLOps) for AI and machine learning workflows](concepts-machine-learning-ops).

## Infrastructure as code (IaC)

[IaC](/en-us/devops/deliver/what-is-infrastructure-as-code) enables consistent and reproducible infrastructure provisioning and management for a range of application types. With intelligent application deployments, your IaC implementation might change throughout the AI pipeline, as the compute power and resources needed for inferencing, serving, training, and fine-tuning models can vary. Defining and versioning IaC templates for your AI developer teams can help ensure consistency and cost-effectiveness across job types while demystifying their individual hardware requirements and accelerating the deployment process.

## Containerization

Managing your model weights, metadata, and configurations in container images allows for portability, simplified versioning, and reduced storage costs over time. With containerization, you can:

- Leverage existing container images, especially for large language models (LLMs) ranging in millions to billions of parameters in size and stable diffusion models, stored in secure container registries.
- Avoid single point of failure (SPOF) in your pipeline with the use of multiple lightweight containers containing the unique dependencies for each task instead of maintaining one large image.
- Store large text/image datasets outside of your base container image and reference them when needed at runtime.

[Get started with the Kubernetes AI Toolchain Operator](ai-toolchain-operator) to deploy a high performance LLM on AKS in a matter of minutes.

## Model management and versioning

Model management and versioning are essential for tracking changes to your models over time. By versioning your models, you can:

- Maintain consistency across your model containers for ease of deployment in different environments.
- Employ parameter-efficient fine-tuning (PEFT) methods to iterate faster on a subset of model weights and maintain new versions in lightweight containers.

## Automation

Automation is key to reducing manual errors, increasing efficiency, and ensuring consistency across the ML lifecycle. By automating tasks, you can:

- Integrate alerting tools to automatically trigger a vector ingestion flow as new data flows into your application.
- Set model performance thresholds to track degradations and trigger retraining pipelines.

## Scalability and resource management

Scalability and resource management are critical for ensuring that your AI pipeline can handle the demands of your application. By optimizing your resource usage, you can:

- Integrate tools that efficiently use your allocated CPU, GPU, and memory resources through distributed computing and multiple levels of parallelism (for example: data, model, and pipeline parallelism).
- Enable autoscaling on your compute resources to support high model request volumes at peak times and scale down in off-peak hours.
- Similar to your traditional applications, plan for disaster recovery by following
[AKS resiliency and reliability best practices](ha-dr-overview).

## Security and compliance

Security and compliance are critical for protecting your data and ensuring that your AI pipeline meets regulatory requirements. By implementing security and compliance best practices, you can:

- Integrate common vulnerability and exposure (CVE) scanning to detect common vulnerabilities on open-source model container images.
- Use
[Microsoft Defender for Containers](/en-us/azure/defender-for-cloud/defender-for-containers-introduction)for model container images stored in your Azure Container Registry.

- Use
- Maintain an audit trail of the ingested data, model changes, and metrics to remain compliant with your organizational policies.

## Next steps

Learn about best practices across other areas of your application deployment and operations on AKS:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/monitor-gpu-metrics -->

# Learn about NVIDIA GPU metrics to optimize GPU performance and utilization on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Efficient placement and optimization of GPU workloads often requires visibility into resource utilization and performance. Managed GPU metrics on AKS (preview) provide automated collection and exposure of GPU utilization, memory, and performance data across NVIDIA GPU-enabled node pools. This enables platform administrators to optimize cluster resources and developers to tune and debug workloads with limited manual instrumentation.

In this article, you learn about GPU metrics collected by the NVIDIA Data Center GPU Manager [(DCGM) exporter](https://github.com/NVIDIA/dcgm-exporter/tree/main) with [a fully managed GPU-enabled node pool (preview)](aks-managed-gpu-nodes) in Azure Kubernetes Service (AKS).

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Prerequisites

- An AKS cluster with
[a fully managed GPU-enabled node pool (preview)](aks-managed-gpu-nodes)and ensure that the[GPUs are schedulable](use-nvidia-gpu#confirm-that-gpus-are-schedulable). - A
[sample GPU workload](use-nvidia-gpu#run-a-gpu-enabled-workload)deployed to your node pool.

## Limitations

- Managed GPU metrics is not currently supported with
[Azure Managed Prometheus or Azure Managed Grafana](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable).

## Verify that managed GPU components are installed

After creating your managed NVIDIA GPU node pool (preview) following [these instructions](aks-managed-gpu-nodes), confirm that the GPU software components were installed with the [az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command:

```
az aks nodepool show \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--name <node-pool-name> \
```


Your output should include the following values:

```
...
...
"gpuInstanceProfile": …
"gpuProfile": {
"driver": "Install"
},
...
...
```


## Understanding GPU metrics

### GPU Utilization Metrics

GPU Utilization metrics show the percentage of time the GPU’s cores are actively processing work. High values indicate that the GPU is heavily used, which is generally desirable for workloads like training or data processing. Interpretation of this metric should consider the type of workload: AI training typically keeps utilization high, while inference may have intermittent utilization due to bursty traffic.

Memory Utilization: Shows the percentage of GPU memory in use. High memory usage without high GPU utilization can indicate memory-bound workloads where the GPU waits on memory transfers. Low memory usage with low utilization may suggest the workload is too small to fully leverage the GPU.

SM (Streaming Multiprocessor) Efficiency: Measures the efficiency with which the GPU’s cores are used. A low SM efficiency indicates that cores are idle or underutilized due to workload imbalance or suboptimal kernel design. High efficiency is ideal for compute-heavy applications.

### Memory Metrics

Memory Bandwidth Utilization: Reflects how much of the theoretical memory bandwidth is being consumed. High bandwidth utilization with low compute utilization can indicate a memory-bound workload. Conversely, high utilization in both compute and memory bandwidth suggests a well-balanced workload.

Memory Errors: Tracks ECC (Error-Correcting Code) errors if enabled. A high number of errors may indicate hardware degradation or thermal issues and should be monitored for reliability.

### Temperature and Power Metrics

GPU Temperature: Indicates the operating temperature of the GPU. Sustained high temperatures can trigger thermal throttling, reducing performance. Ideal interpretation of this metric involves observing temperature relative to the GPU’s thermal limits and cooling capacity.

Power Usage: Shows instantaneous power draw. Comparing power usage to TDP (Thermal Design Power) helps understand whether the GPU is being pushed to its limits. Sudden drops in power may indicate throttling or underutilization.

### Clocks and Frequency Metrics

GPU Clock: The actual operating frequency of the GPU. Combined with utilization, this helps determine if the GPU is throttling or underperforming relative to its potential.

Memory Clock: Operating frequency of GPU memory. Memory-bound workloads may benefit from higher memory clocks; a mismatch between memory and compute utilization can highlight bottlenecks.

### PCIe and NVLink Metrics

PCIe Bandwidth: Measures the throughput over the PCIe bus. Low utilization with heavy workloads may suggest CPU-GPU communication is not a bottleneck. High utilization could point to data transfer limitations impacting performance.

NVLink Bandwidth: This metric is similar to PCIe bandwidth but specific to NVLink interconnects, and relevant in multi-GPU systems for cross-GPU communication. High NVLink usage with low SM utilization may indicate synchronization or data transfer delays.

### Error and Reliability Metrics

Retired Pages and XID Errors: Track GPU memory errors and critical failures. Frequent occurrences signal potential hardware faults and require attention for long-running workloads.

### Interpretation Guidance

DCGM metrics should always be interpreted contextually with the type of your workload on AKS. A high compute-intensive workload should ideally show high GPU and SM utilization, high memory bandwidth usage, stable temperatures below throttling thresholds, and power draw near but below TDP.

Memory-bound workloads might show high memory utilization and bandwidth but lower compute utilization. Anomalies such as low utilization with high temperature or power consumption often indicate throttling, inefficient scheduling, or system-level bottlenecks.

Monitoring trends over time rather than single snapshots is critical. Sudden drops in utilization or spikes in errors often reveal underlying issues before they impact production workloads. Comparing metrics across multiple GPUs can also help identify outliers or misbehaving devices in a cluster. Understanding these metrics in combination, rather than isolation, provides the clearest insight into GPU efficiency and workload performance.

## Common GPU metrics

The following NVIDIA DCGM metrics are commonly evaluated for performance of GPU node pools on Kubernetes:

| GPU Metric Name | Meaning | Typical Range / Indicator | Usage Tip |
|---|---|---|---|
`DCGM_FI_DEV_GPU_UTIL` |
GPU utilization (% time GPU cores are active) | 0–100% (higher is better) | Monitor per-node and per-pod; low values may indicate CPU or I/O bottlenecks |
`DCGM_FI_DEV_SM_UTIL` |
Streaming Multiprocessor efficiency (% active cores) | 0–100% | Low values with high memory usage indicate a memory-bound workload |
`DCGM_FI_DEV_FB_USED` |
Framebuffer memory used (bytes) | 0 to total memory | Use pod GPU memory limits and track per-pod memory usage |
`DCGM_FI_DEV_FB_FREE` |
Free GPU memory (bytes) | 0 to total memory | Useful for scheduling and to avoid OOM errors |
`DCGM_FI_DEV_MEMORY_UTIL` |
Memory utilization (%) | 0–100% | Combine with GPU/SM utilization to determine memory-bound workloads |
`DCGM_FI_DEV_MEMORY_CLOCK` |
Current memory clock frequency (MHz) | 0 to max memory clock | Low values under high memory utilization may indicate throttling |
`DCGM_FI_DEV_POWER_USAGE` |
Instantaneous power usage (Watts) | 0 to TDP | Drops during high utilization may indicate throttling |
`DCGM_FI_DEV_TEMPERATURE` |
GPU temperature (°C) | ~30–85°C normal | Alert on sustained high temperatures |
`DCGM_FI_DEV_NVLINK_RX` |
NVLink receive bandwidth utilization (%) | 0–100% | Multi-GPU synchronization bottleneck if high with low SM utilization |
`DCGM_FI_DEV_XID_ERRORS` |
GPU critical errors reported by driver | Typically 0 | Immediate investigation required; can taint node in Kubernetes |

To learn about the full suite of GPU metrics, visit [NVIDIA DCGM](https://docs.nvidia.com/datacenter/dcgm/latest/user-guide/index.html) Upstream documentation.

## Next steps

- Track your
[GPU node health](gpu-health-monitoring)with Node Problem Detector (NPD) - Create
[multi-instance GPU](gpu-multi-instance)node pools on AKS - Explore the
[AI toolchain operator add-on](ai-toolchain-operator)for AI inferencing and fine-tuning

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-managed-identity -->

# Use a managed identity in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides step-by-step instructions on how to enable and use a system-assigned, user-assigned, or pre-created kubelet managed identity in Azure Kubernetes Service (AKS).

## AKS managed identity prerequisites

Read the

[Overview of managed identities in Azure Kubernetes Service (AKS)](managed-identity-overview)to understand the different types of managed identities available in AKS and how you can use them to securely access Azure resources.Before running the examples in this article, set your subscription as the current active subscription using the

command.`az account set`

`az account set --subscription <subscription-id>`

Create an Azure resource group if you don't already have one by calling the

command.`az group create`

`az group create \ --name <resource-group-name> \ --location <location>`


### Azure CLI version minimum requirements

- Make sure you have Azure CLI version 2.23.0 or later installed. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - To
[use a pre-created kubelet managed identity](use-managed-identity#create-a-kubelet-managed-identity), you need Azure CLI version 2.26.0 or later installed. - To update an existing cluster to use a
[system-assigned managed identity](use-managed-identity#update-an-existing-aks-cluster-to-use-a-system-assigned-managed-identity)or[a user-assigned managed identity](use-managed-identity#update-an-existing-cluster-to-use-a-user-assigned-managed-identity), you need Azure CLI version 2.49.0 or later installed.

### Limitations

Moving or migrating a managed identity-enabled cluster to a different tenant isn't supported.

If the cluster has Microsoft Entra pod-managed identity (

`aad-pod-identity`

) enabled, Node-Managed Identity (NMI) pods modify the iptables of the nodes to intercept calls to the Azure Instance Metadata (IMDS) endpoint. This configuration means any request made to the IMDS endpoint is intercepted by NMI, even if a particular pod doesn't use`aad-pod-identity`

.The AzurePodIdentityException custom resource definition (CRD) can be configured to specify that requests to the IMDS endpoint that originate from a pod matching labels defined in the CRD should be proxied without any processing in NMI. Exclude the system pods with the

`kubernetes.azure.com/managedby: aks`

label in*kube-system*namespace in`aad-pod-identity`

by configuring the AzurePodIdentityException CRD. For more information, see[Use Microsoft Entra pod-managed identities in Azure Kubernetes Service](use-azure-ad-pod-identity).To configure an exception, install the

[mic-exception YAML](https://github.com/Azure/aad-pod-identity/blob/master/deploy/infra/mic-exception.yaml).AKS doesn't support the use of a system-assigned managed identity when using a custom private DNS zone.

The USDOD Central, USDOD East, and USGov Iowa regions in Azure US Government cloud don't support creating a cluster with a user-assigned managed identity.


A pre-created kubelet managed identity must be a user-assigned managed identity.

The China East and China North regions in Microsoft Azure operated by 21Vianet aren't supported.

Important

All Microsoft Defender for Cloud features will be officially retired in the Azure in China region on August 18, 2026. Due to this upcoming retirement, Azure in China customers are no longer able to onboard new subscriptions to the service. A new subscription is any subscription that was not already onboarded to the Microsoft Defender for Cloud service prior to August 18, 2025, the date of the retirement announcement. For more information on the retirement, see

[Microsoft Defender for Cloud Deprecation in Microsoft Azure Operated by 21Vianet Announcement](https://aka.ms/mdcretirementinchina).Customers should work with their account representatives for Microsoft Azure operated by 21Vianet to assess the impact of this retirement on their own operations.


### Update cluster considerations

When you update a cluster, consider the following information:

- An update only works if there's a VHD update to consume. If you're running the latest VHD, you need to wait until the next VHD is available in order to perform the update.
- The Azure CLI ensures your addon's permission is correctly set after migrating. If you're not using the Azure CLI to perform the migrating operation, you need to handle the addon identity's permission by yourself. For an example using an Azure Resource Manager (ARM) template, see
[Assign Azure roles using ARM templates](/en-us/azure/role-based-access-control/role-assignments-template). - If your cluster was using
`--attach-acr`

to pull from images from Azure Container Registry (ACR), you need to run the`az aks update --resource-group <resource-group-name> --name <aks-cluster-name> --attach-acr <acr-resource-id>`

command after updating your cluster to let the newly created kubelet used for managed identity get the permission to pull from ACR. Otherwise, you won't be able to pull from ACR after the update.

## Enable a system-assigned managed identity on an AKS cluster

### Enable a system-assigned managed identity on a new AKS cluster

A system-assigned managed identity is enabled by default when you create a new AKS cluster.

Create an AKS cluster using the

command.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --generate-ssh-keys`


### Update an existing AKS cluster to use a system-assigned managed identity

Update an existing AKS cluster from a service principal to a system-assigned managed identity using the

command with the`az aks update`

`--enable-managed-identity`

parameter.`az aks update \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --enable-managed-identity`

After you update the cluster to use a system-assigned managed identity instead of a service principal, the control plane and pods use the system-assigned managed identity for authorization when accessing other services in Azure. Kubelet continues using a service principal until you also upgrade your agent pool. You can use the

`az aks nodepool upgrade --resource-group <resource-group-name> --cluster-name <aks-cluster-name> --name <node-pool-name> --node-image-only`

command on your nodes to update to a managed identity. A node pool upgrade causes downtime for your AKS cluster as the nodes in the node pools are cordoned, drained, and reimaged.

## Get the principal ID of a system-assigned managed identity

Get the principal ID for the cluster's system-assigned managed identity using the

command.`az aks show`

`CLIENT_ID=$(az aks show \ --name <aks-cluster-name> \ --resource-group <resource-group-name> \ --query identity.principalId \ --output tsv)`


## Add a role assignment for a system-assigned managed identity

Assign an Azure RBAC role to the system-assigned managed identity using the

command.`az role assignment create`

For a VNet, attached Azure disk, static IP address, or route table outside the default worker node resource group, you need to assign the

`Network Contributor`

role on the custom resource group.The following example assigns the

**Network Contributor**role to the system-assigned managed identity. The role assignment is scoped to the resource group that contains the VNet.`az role assignment create \ --assignee <client-id> \ --role "Network Contributor" \ --scope <custom-resource-group-id>`

Note

It can take up to 60 minutes for the permissions granted to your cluster's managed identity to propagate.


## Create a user-assigned managed identity

If you don't yet have a user-assigned managed identity resource, create one using the

command.`az identity create`

`az identity create \ --name <identity-name> \ --resource-group <resource-group-name>`

Your output should resemble the following example output:

`{ "clientId": "<client-id>", "clientSecretUrl": "<clientSecretUrl>", "id": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<identity-name>", "location": "<location>", "name": "<identity-name>", "principalId": "<principal-id>", "resourceGroup": "<resource-group-name>", "tags": {}, "tenantId": "<tenant-id>", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


## Get the principal ID of the user-assigned managed identity

Get the principal ID of the user-assigned managed identity using the

command.`az identity show`

`CLIENT_ID=$(az identity show \ --name <identity-name> \ --resource-group <resource-group-name> \ --query principalId \ --output tsv)`


## Get the resource ID of the user-assigned managed identity

Get the resource ID of the user-assigned managed identity using the

command.`az identity show`

`RESOURCE_ID=$(az identity show \ --name <identity-name> \ --resource-group <resource-group-name> \ --query id \ --output tsv)`


## Assign an Azure RBAC role to the user-assigned managed identity

Add a role assignment for the user-assigned managed identity using the

command.`az role assignment create`

The following example assigns the

**Key Vault Secrets User**role to the user-assigned managed identity to grant it permissions to access secrets in a key vault. The role assignment is scoped to the key vault resource:`az role assignment create \ --assignee <client-id> \ --role "Key Vault Secrets User" \ --scope "<keyvault-resource-id>"`

Note

It can take up to 60 minutes for the permissions granted to your cluster's managed identity to propagate.


## Enable a user-assigned managed identity on an AKS cluster

### Enable a user-assigned managed identity on a new AKS cluster

Create an AKS cluster with the user-assigned managed identity using the

command. Include the`az aks create`

`--assign-identity`

parameter and pass in the resource ID for the user-assigned managed identity:`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --network-plugin azure \ --vnet-subnet-id <vnet-subnet-id> \ --dns-service-ip 10.2.0.10 \ --service-cidr 10.2.0.0/24 \ --assign-identity $RESOURCE_ID \ --generate-ssh-keys`


### Update an existing cluster to use a user-assigned managed identity

Update an existing cluster to use a user-assigned managed identity using the

command. Include the`az aks update`

`--assign-identity`

parameter and pass in the resource ID for the user-assigned managed identity:`az aks update \ --resource-group <resource-group-name> \ --name <cluster-name> \ --enable-managed-identity \ --assign-identity $RESOURCE_ID`

The output for a successful cluster update to use a user-assigned managed identity should resemble the following example output:

`"identity": { "principalId": null, "tenantId": null, "type": "UserAssigned", "userAssignedIdentities": { "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<identity-name>": { "clientId": "<client-id>", "principalId": "<principal-id>" } } },`

Note

Migrating a managed identity for the control plane from system-assigned to user-assigned doesn't result in any downtime for control plane and agent pools. Control plane components continue to the old system-assigned identity for up to several hours, until the next token refresh.


## Determine which type of managed identity a cluster is using

Verify which type of managed identity your cluster is using with the

command.`az aks show`

`az aks show \ --name <aks-cluster-name> \ --resource-group <resource-group-name> \ --query identity.type \ --output tsv`

If the cluster is using a managed identity, the value of the

*type*property will be either**SystemAssigned**or**UserAssigned**.If the cluster is using a service principal, the value of the

*type*property will be null. Consider upgrading your cluster to use a managed identity.

## Create a kubelet managed identity

If you don't have a kubelet managed identity, create one using the

command.`az identity create`

`az identity create \ --name <kubelet-identity-name> \ --resource-group <resource-group-name>`

Your output should resemble the following example output:

`{ "clientId": "<client-id>", "clientSecretUrl": "<clientSecretUrl>", "id": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<kubelet-identity-name>", "location": "<location>", "name": "<kubelet-identity-name>", "principalId": "<principal-id>", "resourceGroup": "<resource-group-name>", "tags": {}, "tenantId": "<tenant-id>", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


## Assign an RBAC role to the kubelet managed identity

Assign the

`acrpull`

role on the kubelet managed identity using thecommand.`az role assignment create`

`az role assignment create \ --assignee <kubelet-client-id> \ --role "acrpull" \ --scope "<acr-registry-id>"`


## Enable a kubelet managed identity on an AKS cluster

### Enable a kubelet managed identity on a new AKS cluster

Create an AKS cluster with your existing identities using the

command.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --network-plugin azure \ --vnet-subnet-id <vnet-subnet-id> \ --dns-service-ip 10.2.0.10 \ --service-cidr 10.2.0.0/24 \ --assign-identity <identity-resource-id> \ --assign-kubelet-identity <kubelet-identity-resource-id> \ --generate-ssh-keys`

A successful AKS cluster creation using a kubelet managed identity should result in output similar to the following:

`"identity": { "principalId": null, "tenantId": null, "type": "UserAssigned", "userAssignedIdentities": { "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<identity-name>": { "clientId": "<client-id>", "principalId": "<principal-id>" } } }, "identityProfile": { "kubeletidentity": { "clientId": "<client-id>", "objectId": "<object-id>", "resourceId": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<kubelet-identity-name>" } },`


### Update an existing cluster to use a kubelet managed identity

To update an existing cluster to use the kubelet managed identity, first get the current control plane managed identity for your AKS cluster.

Warning

Updating the kubelet managed identity upgrades your AKS cluster's node pools, make sure you have the right availability configurations, such as Pod Disruption Budgets, configured before executing this to avoid workload disruption or execute this during a maintenance window.

Confirm your AKS cluster is using the user-assigned managed identity using the

command.`az aks show`

`az aks show \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --query "servicePrincipalProfile"`

If your cluster is using a managed identity, the output shows

`clientId`

with a value of**msi**. A cluster using a service principal shows an object ID. For example:`# The cluster is using a managed identity. { "clientId": "msi" }`

After confirming your cluster is using a managed identity, find the managed identity's resource ID using the

command.`az aks show`

`az aks show --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --query "identity"`

For a user-assigned managed identity, your output should look similar to the following example output:

`{ "principalId": null, "tenantId": null, "type": "UserAssigned", "userAssignedIdentities": <identity-resource-id> "clientId": "<client-id>", "principalId": "<principal-id>" },`

Update your cluster with your existing identities using the

command. Provide the resource ID of the user-assigned managed identity for the control plane for the`az aks update`

`assign-identity`

argument. Provide the resource ID of the kubelet managed identity for the`assign-kubelet-identity`

argument.`az aks update \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --enable-managed-identity \ --assign-identity <identity-resource-id> \ --assign-kubelet-identity <kubelet-identity-resource-id>`

Your output for a successful cluster update using your own kubelet managed identity should resemble the following example output:

`"identity": { "principalId": null, "tenantId": null, "type": "UserAssigned", "userAssignedIdentities": { "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<identity-name>": { "clientId": "<client-id>", "principalId": "<principal-id>" } } }, "identityProfile": { "kubeletidentity": { "clientId": "<client-id>", "objectId": "<object-id>", "resourceId": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<kubelet-identity-name>" } },`


## Get the properties of the kubelet managed identity

Get the properties of the kubelet managed identity using the

command and query on the`az aks show`

`identityProfile.kubeletidentity`

property.`az aks show \ --name <aks-cluster-name> \ --resource-group <resource-group-name> \ --query "identityProfile.kubeletidentity"`


## Next steps

- Use
[Azure Resource Manager templates](/en-us/azure/templates/microsoft.containerservice/managedclusters)to create a managed identity-enabled cluster. - Learn how to
[use kubelogin](kubelogin-authentication)for all supported Microsoft Entra authentication methods in AKS.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kubernetes-helm -->

# Install existing applications with Helm in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage the lifecycle of Kubernetes applications. Similar to Linux package managers, such as *APT* and *Yum*, you can use Helm to manage Kubernetes charts, which are packages of preconfigured Kubernetes resources.

This article shows you how to configure and use Helm in a Kubernetes cluster on Azure Kubernetes Service (AKS).

## Before you begin

- This article assumes you have an existing AKS cluster. If you need an AKS cluster, create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[Azure portal](learn/quick-kubernetes-deploy-portal). - Your AKS cluster needs to have
**an integrated ACR**. For details on creating an AKS cluster with an integrated ACR, see[Authenticate with Azure Container Registry from Azure Kubernetes Service](cluster-container-registry-integration#create-a-new-acr). - You also need the Helm CLI installed, which is the client that runs on your development system. It allows you to start, stop, and manage applications with Helm. If you use the Azure Cloud Shell, the Helm CLI is already installed. For installation instructions on your local platform, see
[Installing Helm](https://helm.sh/docs/intro/install/).

Important

Helm is intended to run on Linux nodes. If you have Windows Server nodes in your cluster, you must ensure that Helm pods are only scheduled to run on Linux nodes. You also need to ensure that any Helm charts you install are also scheduled to run on the correct nodes. The commands in this article use [node-selectors](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector) to make sure pods are scheduled to the correct nodes, but not all Helm charts may expose a node selector. You can also consider using other options on your cluster, such as [taints](operator-best-practices-advanced-scheduler).

## Verify your version of Helm

Use the

`helm version`

command to verify you have Helm 3 installed.`helm version`

The following example output shows Helm version 3.0.0 installed:

`version.BuildInfo{Version:"v3.0.0", GitCommit:"e29ce2a54e96cd02ccfce88bee4f58bb6e2a28b6", GitTreeState:"clean", GoVersion:"go1.13.4"}`


## Install an application with Helm v3

### Add Helm repositories

Add the

*ingress-nginx*repository using the[helm repo](https://helm.sh/docs/intro/quickstart/#initialize-a-helm-chart-repository)command.`helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx`


### Find Helm charts

Search for precreated Helm charts using the

[helm search](https://helm.sh/docs/intro/using_helm/#helm-search-finding-charts)command.`helm search repo ingress-nginx`

The following condensed example output shows some of the Helm charts available for use:

`NAME CHART VERSION APP VERSION DESCRIPTION ingress-nginx/ingress-nginx 4.7.0 1.8.0 Ingress controller for Kubernetes using NGINX a...`

Update the list of charts using the

[helm repo update](https://helm.sh/docs/intro/using_helm/#helm-repo-working-with-repositories)command.`helm repo update`

The following example output shows a successful repo update:

`Hang tight while we grab the latest from your chart repositories... ...Successfully got an update from the "ingress-nginx" chart repository Update Complete. ⎈ Happy Helming!⎈`


## Import the Helm chart images into your ACR

This article uses the [NGINX ingress controller Helm chart](https://github.com/kubernetes/ingress-nginx/tree/main/charts/ingress-nginx), which relies on three container images.

Use

`az acr import`

to import the NGINX ingress controller images into your ACR.`REGISTRY_NAME=<REGISTRY_NAME> CONTROLLER_REGISTRY=registry.k8s.io CONTROLLER_IMAGE=ingress-nginx/controller CONTROLLER_TAG=v1.8.0 PATCH_REGISTRY=registry.k8s.io PATCH_IMAGE=ingress-nginx/kube-webhook-certgen PATCH_TAG=v20230407 DEFAULTBACKEND_REGISTRY=registry.k8s.io DEFAULTBACKEND_IMAGE=defaultbackend-amd64 DEFAULTBACKEND_TAG=1.5 az acr import --name $REGISTRY_NAME --source $CONTROLLER_REGISTRY/$CONTROLLER_IMAGE:$CONTROLLER_TAG --image $CONTROLLER_IMAGE:$CONTROLLER_TAG az acr import --name $REGISTRY_NAME --source $PATCH_REGISTRY/$PATCH_IMAGE:$PATCH_TAG --image $PATCH_IMAGE:$PATCH_TAG az acr import --name $REGISTRY_NAME --source $DEFAULTBACKEND_REGISTRY/$DEFAULTBACKEND_IMAGE:$DEFAULTBACKEND_TAG --image $DEFAULTBACKEND_IMAGE:$DEFAULTBACKEND_TAG`

Note

In addition to importing container images into your ACR, you can also import Helm charts into your ACR. For more information, see

[Push and pull Helm charts to an Azure container registry](/en-us/azure/container-registry/container-registry-helm-repos).

### Run Helm charts

Install Helm charts using the

[helm install](https://helm.sh/docs/intro/using_helm/#helm-install-installing-a-package)command and specify a release name and the name of the chart to install.Tip

The following example creates a Kubernetes namespace for the ingress resources named

*ingress-basic*and is intended to work within that namespace. Specify a namespace for your own environment as needed.`ACR_URL=<REGISTRY_URL> # Create a namespace for your ingress resources kubectl create namespace ingress-basic # Use Helm to deploy an NGINX ingress controller helm install ingress-nginx ingress-nginx/ingress-nginx \ --version 4.0.13 \ --namespace ingress-basic \ --set controller.replicaCount=2 \ --set controller.nodeSelector."kubernetes\.io/os"=linux \ --set controller.image.registry=$ACR_URL \ --set controller.image.image=$CONTROLLER_IMAGE \ --set controller.image.tag=$CONTROLLER_TAG \ --set controller.image.digest="" \ --set controller.admissionWebhooks.patch.nodeSelector."kubernetes\.io/os"=linux \ --set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz \ --set controller.admissionWebhooks.patch.image.registry=$ACR_URL \ --set controller.admissionWebhooks.patch.image.image=$PATCH_IMAGE \ --set controller.admissionWebhooks.patch.image.tag=$PATCH_TAG \ --set defaultBackend.nodeSelector."kubernetes\.io/os"=linux \ --set defaultBackend.image.registry=$ACR_URL \ --set defaultBackend.image.image=$DEFAULTBACKEND_IMAGE \ --set defaultBackend.image.tag=$DEFAULTBACKEND_TAG \ --set defaultBackend.image.digest=""`

The following condensed example output shows the deployment status of the Kubernetes resources created by the Helm chart:

`NAME: nginx-ingress LAST DEPLOYED: Wed Jul 28 11:35:29 2021 NAMESPACE: ingress-basic STATUS: deployed REVISION: 1 TEST SUITE: None NOTES: The ingress-nginx controller has been installed. It may take a few minutes for the LoadBalancer IP to be available. You can watch the status by running 'kubectl --namespace ingress-basic get services -o wide -w nginx-ingress-ingress-nginx-controller' ...`

Get the

*EXTERNAL-IP*of your service using the`kubectl get services`

command.`kubectl --namespace ingress-basic get services -o wide -w ingress-nginx-ingress-nginx-controller`

The following example output shows the

*EXTERNAL-IP*for the*ingress-nginx-ingress-nginx-controller*service:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE SELECTOR nginx-ingress-ingress-nginx-controller LoadBalancer 10.0.254.93 <EXTERNAL_IP> 80:30004/TCP,443:30348/TCP 61s app.kubernetes.io/component=controller,app.kubernetes.io/instance=nginx-ingress,app.kubernetes.io/name=ingress-nginx`


### List releases

Get a list of releases installed on your cluster using the

`helm list`

command.`helm list --namespace ingress-basic`

The following example output shows the

*ingress-nginx*release deployed in the previous step:`NAME NAMESPACE REVISION UPDATED STATUS CHART APP VERSION ingress-nginx ingress-basic 1 2021-07-28 11:35:29.9623734 -0500 CDT deployed ingress-nginx-3.34.0 0.47.0`


### Clean up resources

Deploying a Helm chart creates Kubernetes resources like pods, deployments, and services.

Clean up resources using the

[helm uninstall](https://helm.sh/docs/intro/using_helm/#helm-uninstall-uninstalling-a-release)command and specify your release name.`helm uninstall --namespace ingress-basic ingress-nginx`

The following example output shows the release named

*ingress-nginx*has been uninstalled:`release "nginx-ingress" uninstalled`

Delete the entire sample namespace along with the resources using the

`kubectl delete`

command and specify your namespace name.`kubectl delete namespace ingress-basic`


## Next steps

For more information about managing Kubernetes application deployments with Helm, see the Helm documentation.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-performance-ebpf-host-routing -->

# Overview of eBPF Host Routing (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

As containerized workloads scale across distributed environments, the need for high-performance, low-latency networking becomes critical. eBPF Host Routing is a performance-focused feature within [Advanced Container Networking Services (ACNS)](advanced-container-networking-services-overview) that uses extended Berkeley Packet Filter (eBPF) technology to optimize traffic flow in Kubernetes clusters. Legacy routing on Kubernetes hosts introduces overhead in the form of iptables and netfilter rule processing in the host network namespace. eBPF Host Routing has benefits over legacy host routing by:

- Implementing the routing logic in eBPF programs.
- Allowing Cilium eBPF to bypass iptables in the host namespace.

This direct path reduces the number of hops and processing layers, resulting in faster packet delivery.

## Key benefits

Reduced latency - Bypassing iptables in host results in lower pod-to-pod latency

Increased throughput - Compared to legacy routing, significant improvements can be observed for pod-to-pod traffic between nodes

Reduced CPU usage - Due to removing iptables-based SNAT and routing logic, a modest reduction of CPU usage

Use cases for eBPF Host Routing are performance-critical workloads such as high-throughput microservices, real-time services, or AI/ML workloads. Ensure deployment environment meets the requirements before enabling.

## Components of eBPF Host Routing

** iptables blocker** - An init container that prevents any future installation of iptables rules in the host network namespace (such rules will be bypassed when eBPF host routing is enabled).

** IP Masquerade Agent** - When eBPF Host Routing is active, Cilium takes over SNAT responsibilities using BPF-based masquerading.

`ip-masq-agent`

remains running to maintain consistent behavior if eBPF Host Routing is later disabled; however, its iptables rules are ignored while eBPF Host Routing is active.## Considerations

Enabling eBPF Host Routing causes iptables rules in the host network namespace to be bypassed. Hence, AKS attempts to detect and block enablement of eBPF Host Routing on clusters where iptables rules are in use in the host network namespace.

On clusters with eBPF host routing enabled, AKS blocks attempts to install iptables rules in the host network namespace. Trying to bypass this block may cause the cluster to be inoperational.


## Limitations

eBPF host routing is currently incompatible with nodes running OSes other than Ubuntu 24.04, or Azure Linux 3.0. eBPF host routing is currently also not supported with Confidential VMs and Pod Sandboxing.

eBPF Host Routing can only be enabled for all nodes in a cluster. Hybrid node scenarios aren't supported.

Windows nodes aren't supported by Azure CNI Powered by Cilium, and by extension, eBPF Host Routing.

Istio add-on can't be used along with eBPF Host Routing enabled clusters.

Dual stack networking isn't supported.


## Pricing

Important

Advanced Container Networking Services is a paid offering. For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Next steps

Learn how to enable

[eBPF Host Routing](how-to-enable-ebpf-host-routing)on AKS.For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).Explore Container Network Observability features in Advanced Container Networking Services in

[What is Container Network Observability?](container-network-observability-metrics).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade -->

# Upgrading Azure Kubernetes Service clusters and node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

An Azure Kubernetes Service (AKS) cluster needs to be periodically updated to ensure security and compatibility with the latest features. There are two components of an AKS cluster that are necessary to maintain:

*Cluster Kubernetes version*: Part of the AKS cluster lifecycle involves performing upgrades to the latest Kubernetes version. It’s important that you upgrade to apply the latest security releases and to get access to the latest Kubernetes features, as well as to stay within the[AKS support window](supported-kubernetes-versions#kubernetes-version-support-policy).*Node image version*: AKS regularly provides new node images with the latest OS and runtime updates. It's beneficial to upgrade your nodes' images regularly to ensure support for the latest AKS features and to apply essential security patches and hot fixes.

For Linux nodes, node image security patches and hotfixes may be performed without your initiation as *unattended updates*. These updates are automatically applied, but AKS doesn't automatically reboot your Linux nodes to complete the update process. You're required to use a tool like [kured](node-updates-kured) or [node image upgrade](node-image-upgrade) to reboot the nodes and complete the cycle.

The following table summarizes the details of updating each component:

| Component name | Frequency of upgrade | Planned Maintenance supported | Supported operation methods | Supported operation methods (Multi-Cluster) | Documentation link |
|---|---|---|---|---|---|
| Cluster Kubernetes version upgrade (minor) | Roughly every three months | Yes | Automatic, Manual | Automatic, Manual |
|

[AKS release tracker](release-tracker)[Upgrade an AKS cluster](upgrade-cluster),[Multi-cluster upgrade](/en-us/azure/kubernetes-fleet/concepts-update-orchestration)**Linux**: weekly**Windows**: monthly[AKS node image upgrade](node-image-upgrade),[Multi-cluster upgrade](/en-us/azure/kubernetes-fleet/concepts-update-orchestration)[AKS node security patches](concepts-vulnerability-management#worker-nodes)## Multi-cluster upgrade

When you have multiple clusters, an important practice that you should include as part of your upgrade process is remembering to follow commonly used deployment and testing patterns. Testing an upgrade in a development or test environment before deployment in production is an important step to ensure application functionality and compatibility with the target environment. It can help you identify and fix any errors, bugs, or issues that might affect the performance, security, or usability of the application or underlying infrastructure.

[Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/overview) has built-in support for [multi-cluster upgrades](/en-us/azure/kubernetes-fleet/concepts-update-orchestration) which implements the best practice above to minimize application disruptions caused by cluster upgrades. Besides allowing you to customize the order of upgrades of multiple clusters, it also allows you to use consistent node OS image versions across clusters in different regions.

## Automatic upgrades

Automatic upgrades can be performed through [auto upgrade channels](auto-upgrade-cluster) or via [GitHub Actions](node-upgrade-github-actions).

[Automatic multi-cluster upgrades](/en-us/azure/kubernetes-fleet/update-automation) can be performed through [Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/overview) to adopt the best practice of testing and verifying an upgrade in a development or test environment before production.

## Planned maintenance

[Planned maintenance](planned-maintenance) allows you to schedule weekly maintenance windows that will update your control plane and your kube-system pods, helping to minimize workload impact.

## Troubleshooting

To find details and solutions to specific issues, view the following troubleshooting guides:

## Next steps

For more information what cluster operations may trigger specific upgrade events, upgrade best practices, and other considerations, see the [AKS operator's guide on patching](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-trusted-launch -->

# Trusted Launch for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Trusted Launch](/en-us/azure/virtual-machines/trusted-launch) improves the security of generation 2 virtual machines (VMs) by protecting against advanced and persistent attack techniques. It enables administrators to deploy AKS nodes, which contain the underlying virtual machines, with verified and signed bootloaders, OS kernels, and drivers. By using secure and measured boot, administrators gain insights and confidence of the entire boot chain's integrity.

This article helps you understand this new feature, and how to implement it.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Overview

Trusted Launch is composed of several, coordinated infrastructure technologies that can be enabled independently. Each technology provides another layer of defense against sophisticated threats.

**vTPM**- Trusted Launch introduces a virtualized version of a hardware[Trusted Platform Module](/en-us/windows/security/information-protection/tpm/trusted-platform-module-overview)(TPM), compliant with the TPM 2.0 specification. It serves as a dedicated secure vault for keys and measurements. Trusted Launch provides your VM with its own dedicated TPM instance, running in a secure environment outside the reach of any VM. The vTPM enables[attestation](/en-us/windows/security/information-protection/tpm/tpm-fundamentals#measured-boot-with-support-for-attestation)by measuring the entire boot chain of your VM (UEFI, OS, system, and drivers). Trusted Launch uses the vTPM to perform remote attestation by the cloud. It's used for platform health checks and for making trust-based decisions. As a health check, Trusted Launch can cryptographically certify that your VM booted correctly. If the process fails, possibly because your VM is running an unauthorized component,[Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/defender-for-cloud-introduction)issues integrity alerts. The alerts include details on which components failed to pass integrity checks.**Secure Boot**- At the root of Trusted Launch is Secure Boot for your VM. This mode, which is implemented in platform firmware, protects against the installation of malware-based rootkits and boot kits. Secure Boot works to ensure that only signed operating systems and drivers can boot. It establishes a "root of trust" for the software stack on your VM. With Secure Boot enabled, all OS boot components (boot loader, kernel, kernel drivers) must be signed by trusted publishers. Both Windows and select Linux distributions support Secure Boot. If Secure Boot fails to authenticate an image signed by a trusted publisher, the VM isn't allowed to boot. For more information, see[Secure Boot](/en-us/windows-hardware/design/device-experiences/oem-secure-boot).

## Before you begin

- The Azure CLI version 2.66.0 or later. Run
`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

- Secure Boot requires signed boot loaders, OS kernels, and drivers.

## Limitations

- AKS supports Trusted Launch on kubernetes version 1.25.2 and higher.
- Trusted Launch only supports
[Azure Generation 2 VMs](/en-us/azure/virtual-machines/generation-2). - Node pools with Windows Server operating system aren't supported.
- Trusted Launch can't be enabled in the same node pool as
[FIPS](enable-fips-nodes),[Arm64](use-arm64-vms),[Pod Sandboxing](use-pod-sandboxing), or[Confidential VM](use-cvm). For more information, see[node images documentation](node-images). - Trusted Launch doesn't support virtual node.
- Availability sets aren't supported, only Virtual Machine Scale Sets.
- To enable Secure Boot on GPU node pools, you need to skip installing the GPU driver. For more information, see
[Skip GPU driver installation](gpu-cluster#skip-gpu-driver-installation). - Ephemeral OS disks can be created with trusted Launch and all regions are supported. However, not all virtual machines sizes are supported. For more information, see
[Trusted Launch ephemeral OS sizes](/en-us/azure/virtual-machines/ephemeral-os-disks#trusted-launch-for-ephemeral-os-disks). [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks)doesn't support Trusted Launch on AKS.

## Create an AKS cluster with Trusted Launch enabled

When creating a cluster, enabling vTPM or Secure Boot automatically sets up your node pools to use the customized Trusted Launch image. This image is specifically configured to support the security features enabled by Trusted Launch.

Create an AKS cluster using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command. Before running the command, review the following parameters:**--name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--resource-group**: Enter the name of an existing resource group to host the AKS cluster resource.**--enable-secure-boot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**--enable-vtpm**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

Note

Secure Boot requires signed boot loaders, OS kernels, and drivers. If after enabling Secure Boot your nodes don't start, you can verify which boot components are responsible for Secure Boot failures within an Azure Linux Virtual Machine. See

[verify Secure Boot failures](/en-us/azure/virtual-machines/trusted-launch-faq#verify-secure-boot-failures).The following example creates a cluster named

*myAKSCluster*with one node in the*myResourceGroup*, and enables Secure Boot and vTPM:`az aks create \ --name myAKSCluster \ --resource-group myResourceGroup \ --node-count 1 \ --enable-secure-boot \ --enable-vtpm \ --generate-ssh-keys`

Run the following command to get access credentials for the Kubernetes cluster. Use the

[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command and replace the values for the cluster name and the resource group name.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


Create a template with Trusted Launch parameters. Before creating the template, review the following parameters:

**enableSecureBoot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**enableVTPM**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

In your template, provide values for

`enableVTPM`

and`enableSecureBoot`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters/agentPools`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "securityProfile": { "enableVTPM": "true", "enableSecureBoot": "true", } }`

Deploy your template with vTPM and secure boot enabled on your cluster. See

[Deploy an AKS cluster using an ARM template](/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template)for detailed instructions.

## Add a node pool with Trusted Launch enabled

When you create a node pool, enabling vTPM or Secure Boot automatically sets up your node pools to use the customized Trusted Launch image. This image is specifically configured to support the security features enabled by Trusted Launch.

Add a node pool with Trusted Launch enabled using the

command. Before running the command, review the following parameters:`az aks nodepool add`

**--cluster-name**: Enter the name of the AKS cluster.**--resource-group**: Enter the name of an existing resource group to host the AKS cluster resource.**--name**: Enter a unique name for the node pool. The name of a node pool can only contain lowercase alphanumeric characters and must begin with a lowercase letter. For Linux node pools, the length must be between 1-11 characters.**--node-count**: The number of nodes in the Kubernetes agent pool. Default is 3.**--enable-secure-boot**: Enables Secure Boot to authenticate image signed by a trusted publisher.**--enable-vtpm**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

Note

Secure Boot requires signed boot loaders, OS kernels, and drivers. If after enabling Secure Boot your nodes don't start, you can verify which boot components are responsible for Secure Boot failures within an Azure Linux Virtual Machine. See

[verify Secure Boot failures](/en-us/azure/virtual-machines/trusted-launch-faq#verify-secure-boot-failures).The following example deploys a node pool with vTPM and Secure Boot enabled on a cluster named

*myAKSCluster*with three nodes:`az aks nodepool add --resource-group myResourceGroup --cluster-name myAKSCluster --name mynodepool --node-count 3 --enable-vtpm --enable-secure-boot`

Check that your node pool is using a Trusted Launch image.

Trusted Launch nodes have the following output:

- Node image version containing
`"TL"`

, such as`"AKSUbuntu-2204-gen2TLcontainerd"`

. `"Security-type"`

should be`"Trusted Launch"`

.

`kubectl get nodes kubectl describe node {node-name} | grep -e node-image-version -e security-type`

- Node image version containing

Create a template with Trusted Launch parameters. Before creating the template, review the following parameters:

**enableSecureBoot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**enableVTPM**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

In your template, provide values for

`enableVTPM`

and`enableSecureBoot`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters/agentPools`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "securityProfile": { "enableVTPM": "true", "enableSecureBoot": "true", } }`

Deploy your template with vTPM and secure boot enabled on your cluster. See

[Deploy an AKS cluster using an ARM template](/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template)for detailed instructions.

## Enable vTPM or secure boot on an existing Trusted Launch node pool

You can update an existing Trusted Launch node pool to enable vTPM or secure boot. The following scenarios are supported:

- When creating a node pool, you only specify
`--enable-secure-boot`

, you can run the update command to`--enable-vtpm`

- When creating a node pool, you only specify
`--enable-vtpm`

, you can run the update command to`--enable-secure-boot`


If your node pool doesn't currently have a Trusted Launch image, you won't be able to update the node pool to enable secure boot or vTPM.

Check that your node pool is using a Trusted Launch image.

Trusted Launch nodes have the following output:

- Node image version containing
`"TL"`

, such as`"AKSUbuntu-2204-gen2TLcontainerd"`

. `"Security-type"`

should be`"Trusted Launch"`

.

`kubectl get nodes kubectl describe node {node-name} | grep -e node-image-version -e security-type`

If your node pool doesn't currently have a Trusted Launch image, you won't be able to update the node pool to enable secure boot or vTPM.

- Node image version containing
Update a node pool with Trusted Launch enabled using the

command. Before running the command, review the following parameters:`az aks nodepool update`

**--resource-group**: Enter the name of an existing resource group hosting your existing AKS cluster.**--cluster-name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--name**: Enter the name of your node pool, such as*mynodepool*.**--enable-secure-boot**: Enables Secure Boot to authenticate that the image was signed by a trusted publisher.**--enable-vtpm**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

Note

Secure Boot requires signed boot loaders, OS kernels, and drivers. If after enabling Secure Boot your nodes don't start, you can verify which boot components are responsible for Secure Boot failures within an Azure Linux Virtual Machine. See

[verify Secure Boot failures](/en-us/azure/virtual-machines/trusted-launch-faq#verify-secure-boot-failures).The following example updates the node pool

*mynodepool*on the*myAKSCluster*in the*myResourceGroup*, and enables vTPM. In this scenario, secure boot was enabled during node pool creation:`az aks nodepool update --cluster-name myCluster --resource-group myResourceGroup --name mynodepool --enable-vtpm`

The following example updates the node pool

*mynodepool*on the*myAKSCluster*in the*myResourceGroup*, and enables secure boot. In this scenario, vTPM was enabled during node pool creation:`az aks nodepool update --cluster-name myCluster --resource-group myResourceGroup --name mynodepool --enable-secure-boot`


Check that your node pool is using a Trusted Launch image.

Trusted Launch nodes have the following output:

- Node image version containing
`"TL"`

, such as`"AKSUbuntu-2204-gen2TLcontainerd"`

. `"Security-type"`

should be`"Trusted Launch"`

.

`kubectl get nodes kubectl describe node {node-name} | grep -e node-image-version -e security-type`

If your node pool doesn't currently have a Trusted Launch image, you won't be able to update the node pool to enable secure boot or vTPM.

- Node image version containing
Create a template with Trusted Launch parameters. Before creating the template, review the following parameters:

**enableSecureBoot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**enableVTPM**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

In your template, provide values for

`enableVTPM`

and`enableSecureBoot`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters/agentPools`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "securityProfile": { "enableVTPM": "true", "enableSecureBoot": "true", } }`

Deploy your template with vTPM and secure boot enabled on your cluster. See

[Deploy an AKS cluster using an ARM template](/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template)for detailed instructions.

## Assign pods to nodes with Trusted Launch enabled

You can constrain a pod and restrict it to run on a specific node or nodes, or preference to nodes with Trusted Launch enabled. You can control this using the following node pool selector in your pod manifest.

```
spec:
nodeSelector:
kubernetes.azure.com/security-type = "TrustedLaunch"
```


## Disable vTPM or secure boot on an existing Trusted Launch node pool

You can update an existing node pool to disable vTPM or secure boot. When this occurs, you'll still remain on the Trusted Launch image. You can re-enable vTPM or secure boot at any time by updating your node pool.

Update a node pool to disable secure boot or vTPM using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. Before running the command, review the following parameters:

**--resource-group**: Enter the name of an existing resource group hosting your existing AKS cluster.**--cluster-name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--name**: Enter the name of your node pool, such as*mynodepool*.**--enable-secure-boot**: Enables Secure Boot to authenticate that the image was signed by a trusted publisher.**--enable-vtpm**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

To disable vTPM on an existing node pool:

```
az aks nodepool update --cluster-name myCluster --resource-group myResourceGroup --name mynodepool --disable-vtpm
```


To disable secure boot on an existing node pool:

```
az aks nodepool update --cluster-name myCluster --resource-group myResourceGroup --name mynodepool --disable-secure-boot
```


Create a template with Trusted Launch parameters. Before creating the template, review the following parameters:

**enableSecureBoot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**enableVTPM**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

In your template, provide values for

`enableVTPM`

and`enableSecureBoot`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters/agentPools`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "securityProfile": { "enableVTPM": "false", "enableSecureBoot": "false", } }`

Deploy your template with vTPM and secure boot disabled on your cluster. See

[Deploy an AKS cluster using an ARM template](/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template)for detailed instructions.

## Next steps

In this article, you learned how to enable Trusted Launch. Learn more about [Trusted Launch](/en-us/azure/virtual-machines/trusted-launch).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/quickstart-helm -->

# Quickstart: Develop on Azure Kubernetes Service (AKS) with Helm

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Helm](https://helm.sh/) is an open-source packaging tool that helps you install and manage the lifecycle of Kubernetes applications. Similar to Linux package managers like *APT* and *Yum*, Helm manages Kubernetes charts, which are packages of pre-configured Kubernetes resources.

In this quickstart, you use Helm to package and run an application on AKS. For information on installing an existing application using Helm, see [Install existing applications with Helm in AKS](kubernetes-helm).

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). [Azure CLI](/en-us/cli/azure/install-azure-cli)or[Azure PowerShell](/en-us/powershell/azure/install-az-ps)installed.[Helm v3 installed](https://helm.sh/docs/intro/install/).

## Create an Azure Container Registry

You need to store your container images in an Azure Container Registry (ACR) to run your application in your AKS cluster using Helm. Your registry name must be unique within Azure and contain 5-50 alphanumeric characters. Only lowercase characters are allowed. The *Basic* SKU is a cost-optimized entry point for development purposes that provides a balance of storage and throughput.

Create an Azure resource group using the

[az group create](/en-us/cli/azure/group#az-group-create)command. The following example creates a resource group named*myResourceGroup*in the*eastus*location.`az group create --name myResourceGroup --location eastus`

Create an Azure Container Registry with a unique name by calling the

[az acr create](/en-us/cli/azure/acr#az-acr-create)command. The following example creates an ACR named*myhelmacr*with the*Basic*SKU.`az acr create --resource-group myResourceGroup --name myhelmacr --sku Basic`

Your output should look similar to the following condensed example output. Take note of your

*loginServer*value for your ACR to use in a later step.`{ "adminUserEnabled": false, "creationDate": "2023-12-26T22:36:23.998425+00:00", "id": "/subscriptions/<ID>/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myhelmacr", "location": "eastus", "loginServer": "myhelmacr.azurecr.io", "name": "myhelmacr", "networkRuleSet": null, "provisioningState": "Succeeded", "resourceGroup": "myResourceGroup", "sku": { "name": "Basic", "tier": "Basic" }, "status": null, "storageAccount": null, "tags": {}, "type": "Microsoft.ContainerRegistry/registries" }`


## Create an AKS cluster

Your new AKS cluster needs access to your ACR to pull the container images and run them.

Create an AKS cluster using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command with the`--attach-acr`

parameter to grant the cluster access to your ACR. The following example creates an AKS cluster named*myAKSCluster*and grants it access to the*myhelmacr*ACR. Make sure you replace`myhelmacr`

with the name of your ACR.`az aks create --resource-group myResourceGroup --name myAKSCluster --location eastus --attach-acr myhelmacr --generate-ssh-keys`


## Connect to your AKS cluster

To connect a Kubernetes cluster locally, you use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell.

Install

`kubectl`

locally using the[az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli)command.`az aks install-cli`

Configure

`kubectl`

to connect to your Kubernetes cluster using the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. The following command gets credentials for the AKS cluster named*myAKSCluster*in*myResourceGroup*.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Download the sample application

This quickstart uses the [Azure Vote application](https://github.com/Azure-Samples/azure-voting-app-redis.git).

Clone the application from GitHub using the

`git clone`

command.`git clone https://github.com/Azure-Samples/azure-voting-app-redis.git`

Navigate to the

`azure-vote`

directory using the`cd`

command.`cd azure-voting-app-redis/azure-vote/`


## Build and push the sample application to ACR

Build and push the image to your ACR using the

[az acr build](/en-us/cli/azure/acr#az-acr-build)command. The following example builds an image named*azure-vote-front:v1*and pushes it to the*myhelmacr*ACR. Make sure you replace`myhelmacr`

with the name of your ACR.`az acr build --image azure-vote-front:v1 --registry myhelmacr --file Dockerfile .`


Note

You can also import Helm charts into your ACR. For more information, see [Push and pull Helm charts to an Azure container registry](/en-us/azure/container-registry/container-registry-helm-repos).

## Create your Helm chart

Generate your Helm chart using the

`helm create`

command.`helm create azure-vote-front`

Update

*azure-vote-front/Chart.yaml*to add a dependency for the*redis*chart from the`https://charts.bitnami.com/bitnami`

chart repository and update`appVersion`

to`v1`

, as shown in the following example:Note

The container image versions shown in this guide have been tested to work with this example but may not be the latest version available.

`apiVersion: v2 name: azure-vote-front description: A Helm chart for Kubernetes dependencies: - name: redis version: 17.3.17 repository: https://charts.bitnami.com/bitnami ... # This is the version number of the application being deployed. This version number should be # incremented each time you make changes to the application. appVersion: v1`

Update your Helm chart dependencies using the

`helm dependency update`

command.`helm dependency update azure-vote-front`

Update

*azure-vote-front/values.yaml*with the following changes.- Add a
*redis*section to set the image details, container port, and deployment name. - Add a
*backendName*for connecting the frontend portion to the*redis*deployment. - Change
*image.repository*to`<loginServer>/azure-vote-front`

. - Change
*image.tag*to`v1`

. - Change
*service.type*to*LoadBalancer*.

For example:

`replicaCount: 1 backendName: azure-vote-backend-master redis: image: registry: mcr.microsoft.com repository: oss/bitnami/redis tag: 6.0.8 fullnameOverride: azure-vote-backend auth: enabled: false image: repository: myhelmacr.azurecr.io/azure-vote-front pullPolicy: IfNotPresent tag: "v1" ... service: type: LoadBalancer port: 80 ...`

- Add a
Add an

`env`

section to*azure-vote-front/templates/deployment.yaml*to pass the name of the*redis*deployment.`... containers: - name: {{ .Chart.Name }} securityContext: {{- toYaml .Values.securityContext | nindent 12 }} image: "{{ .Values.image.repository }}:{{ .Values.image.tag | default .Chart.AppVersion }}" imagePullPolicy: {{ .Values.image.pullPolicy }} env: - name: REDIS value: {{ .Values.backendName }} ...`


## Run your Helm chart

Install your application using your Helm chart using the

`helm install`

command.`helm install azure-vote-front azure-vote-front/`

It takes a few minutes for the service to return a public IP address. Monitor progress using the

`kubectl get service`

command with the`--watch`

argument.`kubectl get service azure-vote-front --watch`

When the service is ready, the

`EXTERNAL-IP`

value changes from`<pending>`

to an IP address. Press`CTRL+C`

to stop the`kubectl`

watch process.`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE azure-vote-front LoadBalancer 10.0.18.228 <pending> 80:32021/TCP 6s ... azure-vote-front LoadBalancer 10.0.18.228 52.188.140.81 80:32021/TCP 2m6s`

Navigate to your application's load balancer in a browser using the

`<EXTERNAL-IP>`

to see the sample application.

## Delete the cluster

Remove your resource group, AKS cluster, Azure container registry, container images stored in the ACR, and all related resources using the

[az group delete](/en-us/cli/azure/group#az-group-delete)command with the`--yes`

parameter to confirm deletion and the`--no-wait`

parameter to return to the command prompt without waiting for the operation to complete.`az group delete --name myResourceGroup --yes --no-wait`


Note

If you created your AKS cluster with a system-assigned managed identity (the default identity option in this quickstart), the identity is managed by the platform and doesn't require removal.

If you created your AKS cluster with a service principal, the service principal isn't removed when you delete the cluster. To remove the service principal, see [AKS service principal considerations and deletion](kubernetes-service-principal#considerations-when-using-a-service-principal).

## Next steps

For more information about using Helm, see the [Helm documentation](https://helm.sh/docs/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/open-ai-secure-access-quickstart -->

# Secure access to Azure OpenAI from Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to secure access to Azure OpenAI from Azure Kubernetes Service (AKS) using Microsoft Entra Workload ID. You learn how to:

- Enable workload identities on an AKS cluster.
- Create an Azure user-assigned managed identity.
- Create a Microsoft Entra ID federated credential.
- Enable workload identity on a Kubernetes Pod.

Note

We recommend using Microsoft Entra Workload ID and managed identities on AKS for Azure OpenAI access because it enables a secure, passwordless authentication process for accessing Azure resources.

## Before you begin

- You need an Azure account with an active subscription. If you don't have one,
[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - This article builds on
[Deploy an application that uses OpenAI on AKS](open-ai-quickstart). You should complete that article before you begin this one. - You need a custom domain name enabled on your Azure OpenAI account to use for Microsoft Entra authorization. For more information, see
[Custom subdomain names for Azure AI services](/en-us/azure/ai-services/cognitive-services-custom-subdomains).

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Enable Microsoft Entra Workload ID on an AKS cluster

The Microsoft Entra Workload ID and OIDC Issuer Endpoint features aren't enabled on AKS by default. You must enable them on your AKS cluster before you can use them.

Set the resource group name and AKS cluster resource group name variables.

`# Set the resource group variable RG_NAME=myResourceGroup # Set the AKS cluster name based on the resource group variable AKS_NAME=$(az resource list --resource-group $RG_NAME --resource-type Microsoft.ContainerService/managedClusters --query "[0].name" -o tsv)`

Enable the Microsoft Entra Workload ID and OIDC Issuer Endpoint features on your existing AKS cluster using the

command.`az aks update`

`az aks update \ --resource-group $RG_NAME \ --name $AKS_NAME \ --enable-workload-identity \ --enable-oidc-issuer`

Get the AKS OIDC Issuer Endpoint URL using the

command.`az aks show`

`AKS_OIDC_ISSUER=$(az aks show --resource-group $RG_NAME --name $AKS_NAME --query "oidcIssuerProfile.issuerUrl" -o tsv)`


## Create an Azure user-assigned managed identity

Create an Azure user-assigned managed identity using the

command.`az identity create`

`# Set the managed identity name variable MANAGED_IDENTITY_NAME=myIdentity # Create the managed identity az identity create \ --resource-group $RG_NAME \ --name $MANAGED_IDENTITY_NAME`

Get the managed identity client ID and object ID using the

command.`az identity show`

`# Get the managed identity client ID MANAGED_IDENTITY_CLIENT_ID=$(az identity show --resource-group $RG_NAME --name $MANAGED_IDENTITY_NAME --query clientId -o tsv) # Get the managed identity object ID MANAGED_IDENTITY_OBJECT_ID=$(az identity show --resource-group $RG_NAME --name $MANAGED_IDENTITY_NAME --query principalId -o tsv)`

Get the Azure OpenAI resource ID using the

command.`az resource list`

`AOAI_RESOURCE_ID=$(az resource list --resource-group $RG_NAME --resource-type Microsoft.CognitiveServices/accounts --query "[0].id" -o tsv)`

Grant the managed identity access to the Azure OpenAI resource using the

command.`az role assignment create`

`az role assignment create \ --role "Cognitive Services OpenAI User" \ --assignee-object-id $MANAGED_IDENTITY_OBJECT_ID \ --assignee-principal-type ServicePrincipal \ --scope $AOAI_RESOURCE_ID`


## Create a Microsoft Entra ID federated credential

Set the federated credential, namespace, and service account variables.

`# Set the federated credential name variable FEDERATED_CREDENTIAL_NAME=myFederatedCredential # Set the namespace variable SERVICE_ACCOUNT_NAMESPACE=default # Set the service account variable SERVICE_ACCOUNT_NAME=ai-service-account`

Create the federated credential using the

command.`az identity federated-credential create`

`az identity federated-credential create \ --name ${FEDERATED_CREDENTIAL_NAME} \ --resource-group ${RG_NAME} \ --identity-name ${MANAGED_IDENTITY_NAME} \ --issuer ${AKS_OIDC_ISSUER} \ --subject system:serviceaccount:${SERVICE_ACCOUNT_NAMESPACE}:${SERVICE_ACCOUNT_NAME}`


## Use Microsoft Entra Workload ID on AKS

To use Microsoft Entra Workload ID on AKS, you need to make a few changes to the `ai-service`

deployment manifest.

### Create a ServiceAccount

Get the kubeconfig for your cluster using the

command.`az aks get-credentials`

`az aks get-credentials \ --resource-group $RG_NAME \ --name $AKS_NAME`

Create a Kubernetes ServiceAccount using the

command.`kubectl apply`

`kubectl apply -f - <<EOF apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: ${MANAGED_IDENTITY_CLIENT_ID} name: ${SERVICE_ACCOUNT_NAME} namespace: ${SERVICE_ACCOUNT_NAMESPACE} EOF`


### Enable Microsoft Entra Workload ID on the Pod

Set the Azure OpenAI resource name, endpoint, and deployment name variables.

`# Get the Azure OpenAI resource name AOAI_NAME=$(az resource list \ --resource-group $RG_NAME \ --resource-type Microsoft.CognitiveServices/accounts \ --query "[0].name" -o tsv) # Get the Azure OpenAI endpoint AOAI_ENDPOINT=$(az cognitiveservices account show \ --resource-group $RG_NAME \ --name $AOAI_NAME \ --query properties.endpoint -o tsv) # Get the Azure OpenAI deployment name AOAI_DEPLOYMENT_NAME=$(az cognitiveservices account deployment list \ --resource-group $RG_NAME \ --name $AOAI_NAME \ --query "[0].name" -o tsv)`

Redeploy the

`ai-service`

with the ServiceAccount and the`azure.workload.identity/use`

annotation set to`true`

using thecommand.`kubectl apply`

`kubectl apply -f - <<EOF apiVersion: apps/v1 kind: Deployment metadata: name: ai-service spec: replicas: 1 selector: matchLabels: app: ai-service template: metadata: labels: app: ai-service azure.workload.identity/use: "true" spec: serviceAccountName: $SERVICE_ACCOUNT_NAME nodeSelector: "kubernetes.io/os": linux containers: - name: ai-service image: ghcr.io/azure-samples/aks-store-demo/ai-service:latest ports: - containerPort: 5001 env: - name: USE_AZURE_OPENAI value: "True" - name: USE_AZURE_AD value: "True" - name: AZURE_OPENAI_DEPLOYMENT_NAME value: "${AOAI_DEPLOYMENT_NAME}" - name: AZURE_OPENAI_ENDPOINT value: "${AOAI_ENDPOINT}" resources: requests: cpu: 20m memory: 50Mi limits: cpu: 50m memory: 128Mi EOF`


### Test the application

Verify the new pod is running using the

command.`kubectl get pods`

`kubectl get pods --selector app=ai-service`

Get the pod environment variables using the

command. The output demonstrates that the Azure OpenAI API key no longer exists in the Pod's environment variables.`kubectl describe pod`

`kubectl describe pod --selector app=ai-service`

Open a new terminal and get the IP of the store admin service using the following

`echo`

command.`echo "http://$(kubectl get svc/store-admin -o jsonpath='{.status.loadBalancer.ingress[0].ip}')"`

Open a web browser and navigate to the IP address from the previous step.

Select

**Products**. You should be able to add a new product and get a description for it using Azure OpenAI.

## Next steps

In this article, you learned how to secure access to Azure OpenAI from Azure Kubernetes Service (AKS) using Microsoft Entra Workload ID.

For more information on Microsoft Entra Workload ID, see [Microsoft Entra Workload ID](workload-identity-overview).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-group-managed-service-accounts -->

# Enable Group Managed Service Accounts (GMSA) for your Windows Server nodes on your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Group Managed Service Accounts (GMSA)](/en-us/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview) is a managed domain account for multiple servers that provides automatic password management, simplified service principal name (SPN) management, and the ability to delegate management to other administrators. With Azure Kubernetes Service (AKS), you can enable GMSA on your Windows Server nodes, which allows containers running on Windows Server nodes to integrate with and be managed by GMSA.

## Prerequisites

- Kubernetes 1.19 or greater. To check your version, see
[Check for available upgrades](upgrade-aks-cluster#check-for-available-aks-cluster-upgrades). To upgrade your version, see[Upgrade AKS cluster](upgrade-aks-cluster). - Azure CLI version 2.35.0 or greater. To find the version, run
`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). [Managed identities](use-managed-identity)enabled on your AKS cluster.- Permissions to create or update an Azure Key Vault.
- Permissions to configure GMSA on Active Directory Domain Service or on-premises Active Directory.
- The domain controller must have Active Directory Web Services enabled and must be reachable on port 9389 by the AKS cluster.

Note

Microsoft also provides a purpose-built PowerShell module to configure gMSA on AKS. For more information, see [gMSA on Azure Kubernetes Service](/en-us/virtualization/windowscontainers/manage-containers/gmsa-aks-ps-module).

## Configure GMSA on Active Directory domain controller

To use GMSA with AKS, you need a standard domain user credential to access the GMSA credential configured on your domain controller. To configure GMSA on your domain controller, see [Get started with Group Managed Service Accounts](/en-us/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts). For the standard domain user credential, you can use an existing user or create a new one, as long as it has access to the GMSA credential.

Important

You must use either Active Directory Domain Service or on-premises Active Directory. At this time, you can't use Microsoft Entra ID to configure GMSA with an AKS cluster.

## Store the standard domain user credentials in Azure Key Vault

Your AKS cluster uses the standard domain user credentials to access the GMSA credentials from the domain controller. To provide secure access to those credentials for the AKS cluster, you should store them in Azure Key Vault.

If you don't already have an Azure key vault, create one using the

command.`az keyvault create`

`az keyvault create --resource-group myResourceGroup --name myGMSAVault`

Store the standard domain user credential as a secret in your key vault using the

command. The following example stores the domain user credential with the key`az keyvault secret set`

*GMSADomainUserCred*in the*myGMSAVault*key vault.`az keyvault secret set --vault-name myGMSAVault --name "GMSADomainUserCred" --value "$Domain\\$DomainUsername:$DomainUserPassword"`

Note

Make sure to use the fully qualified domain name for the domain.


### Optional: Use a custom virtual network with custom DNS

You need to configure your domain controller through DNS so it's reachable by the AKS cluster. You can configure your network and DNS outside of your AKS cluster to allow your cluster to access the domain controller. Alternatively, you can use Azure CNI to configure a custom virtual network with a custom DNS on your AKS cluster to provide access to your domain controller. For more information, see [Configure Azure CNI networking in Azure Kubernetes Service (AKS)](configure-azure-cni).

### Optional: Configure more than one DNS server

If you want to configure more than one DNS server for Windows GMSA in your AKS cluster, don't specify `--gmsa-dns-server`

or `v--gmsa-root-domain-name`

. Instead, you can add multiple DNS servers in the virtual network by selecting *Custom DNS* and adding the DNS servers.

### Optional: Use your own kubelet identity for your cluster

To provide the AKS cluster access to your key vault, the cluster kubelet identity needs access to your key vault. When you create a cluster with managed identity enabled, a kubelet identity is automatically created by default.

You can either [grant access to your key vault for the identity after cluster creation](#enable-gmsa-on-existing-cluster) or create your own identity before cluster creation using the following steps:

Create a kubelet identity using the

command.`az identity create`

`az identity create --name myIdentity --resource-group myResourceGroup`

Get the ID of the identity using the

command and set it to a variable named`az identity list`

`MANAGED_ID`

.`MANAGED_ID=$(az identity list --query "[].id" -o tsv)`

Grant the identity access to your key vault using the

command.`az keyvault set-policy`

`az keyvault set-policy --name "myGMSAVault" --object-id $MANAGED_ID --secret-permissions get`


## Enable GMSA on a new AKS cluster

Create administrator credentials to use during cluster creation. The following commands prompt you for a username and set it to

`WINDOWS_USERNAME`

for use in a later command.`echo "Please enter the username to use as administrator credentials for Windows Server nodes on your cluster: " && read WINDOWS_USERNAME`

Create an AKS cluster using the

command with the following parameters:`az aks create`

`--enable-windows-gmsa`

: Enables GMSA for the cluster.`--gmsa-dns-server`

: The IP address of the DNS server.`--gmsa-root-domain-name`

: The root domain name of the DNS server.

`DNS_SERVER=<IP address of DNS server> ROOT_DOMAIN_NAME="contoso.com" az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --vm-set-type VirtualMachineScaleSets \ --network-plugin azure \ --load-balancer-sku standard \ --windows-admin-username $WINDOWS_USERNAME \ --enable-windows-gmsa \ --gmsa-dns-server $DNS_SERVER \ --gmsa-root-domain-name $ROOT_DOMAIN_NAME \ --generate-ssh-keys`

Note

If you're using a custom virtual network, you need to specify the virtual network ID using the

`vnet-subnet-id`

parameter, and you might need to also add the`docker-bridge-address`

,`dns-service-ip`

, and`service-cidr`

parameters depending on your configuration.If you created your own identity for the kubelet identity, use the

`assign-kubelet-identity`

parameter to specify your identity.When you specify the

`--gmsa-dns-server`

and`--gmsa-root-domain-name`

parameters, a DNS forward rule is added to the`kube-system/coredns`

ConfigMap. This rule forwards the DNS requests for`$ROOT_DOMAIN_NAME`

from the pods to the`$DNS_SERVER`

.`$ROOT_DOMAIN_NAME:53 { errors cache 30 log forward . $DNS_SERVER }`


Add a Windows Server node pool using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --os-type Windows \ --name npwin \ --node-count 1`


### Enable GMSA on existing cluster

Enable GMSA on an existing cluster with Windows Server nodes and managed identities enabled using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--resource-group myResourceGroup \
--name myAKSCluster \
--enable-windows-gmsa \
--gmsa-dns-server $DNS_SERVER \
--gmsa-root-domain-name $ROOT_DOMAIN_NAME
```


## Grant access to your key vault for the kubelet identity

Note

Skip this step if you provided your own identity for the kubelet identity.

Grant access to your key vault for the kubelet identity using the [ az keyvault set-policy](/en-us/cli/azure/keyvault#az-keyvault-set-policy) command.

```
MANAGED_ID=$(az aks show -g myResourceGroup -n myAKSCluster --query "identityProfile.kubeletidentity.objectId" -o tsv)
az keyvault set-policy --name "myGMSAVault" --object-id $MANAGED_ID --secret-permissions get
```


## Install GMSA cred spec

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Create a new YAML named

*gmsa-spec.yaml*and paste in the following YAML. Make sure you replace the placeholders with your own values. Placeholders are indicated with angle brackets (`<>`

), for example replace`<GMSA_ACCOUNT_USERNAME>`

with an account name like`gmsa-account`

.`apiVersion: windows.k8s.io/v1 kind: GMSACredentialSpec metadata: name: aks-gmsa-spec # This name can be changed, but it will be used as a reference in the pod spec credspec: ActiveDirectoryConfig: GroupManagedServiceAccounts: - Name: <GMSA_ACCOUNT_USERNAME> # GMSA account username like gmsa-account Scope: <NETBIOS_DOMAIN_NAME> # NetBIOS domain name like contoso - Name: <GMSA_ACCOUNT_USERNAME> # GMSA account username like gmsa-account Scope: <DNS_DOMAIN_NAME> # Fully qualified domain name like contoso.com HostAccountConfig: PluginGUID: '{CCC2A336-D7F3-4818-A213-272B7924213E}' PortableCcgVersion: "1" PluginInput: "ObjectId=<MANAGED_IDENTITY_OBJECT_ID>;SecretUri=https://<KEY_VAULT_NAME>.vault.azure.net/secrets/<KEY_VAULT_SECRET_NAME>" # MANAGED_IDENTITY_OBJECT_ID is managed identity object ID GUID # KEY_VAULT_NAME is the name of your key vault, like myGMSAVault # KEY_VAULT_SECRET_NAME is the name of the key vault secret you created, like GMSADomainUserCred CmsPlugins: - ActiveDirectory DomainJoinConfig: DnsName: <DNS_DOMAIN_NAME> # Fully qualified domain name like contoso.com DnsTreeName: <DNS_ROOT_DOMAIN_NAME> # Root domain name like contoso.com Guid: <AD_DOMAIN_OBJECT_GUID> # Domain object GUID like 66aa66aa-bb77-cc88-dd99-00ee00ee00ee MachineAccountName: <GMSA_ACCOUNT_USERNAME> # GMSA account username like gmsa-account NetBiosName: <NETBIOS_DOMAIN_NAME> # NetBIOS domain name like contoso Sid: <AD_DOMAIN_OBJECT_SID> # Domain object SID like S-1-5-21-1111111111-2222222222-3333333333`


Note

AKS upgraded the `apiVersion`

of `GMSACredentialSpec`

from `windows.k8s.io/v1alpha1`

to `windows.k8s.io/v1`

in release v20230903.

Create a new YAML named

*gmsa-role.yaml*and paste in the following YAML.`apiVersion: rbac.authorization.k8s.io/v1 kind: ClusterRole metadata: name: aks-gmsa-role rules: - apiGroups: ["windows.k8s.io"] resources: ["gmsacredentialspecs"] verbs: ["use"] resourceNames: ["aks-gmsa-spec"]`

Create a new YAML file named

*gmsa-role-binding.yaml*and paste in the following YAML.`apiVersion: rbac.authorization.k8s.io/v1 kind: RoleBinding metadata: name: allow-default-svc-account-read-on-aks-gmsa-spec namespace: default subjects: - kind: ServiceAccount name: default namespace: default roleRef: kind: ClusterRole name: aks-gmsa-role apiGroup: rbac.authorization.k8s.io`

Apply the changes from

*gmsa-spec.yaml*,*gmsa-role.yaml*, and*gmsa-role-binding.yaml*using the`kubectl apply`

command.`kubectl apply -f gmsa-spec.yaml kubectl apply -f gmsa-role.yaml kubectl apply -f gmsa-role-binding.yaml`


## Verify GMSA installation

Create a new YAML named

*gmsa-demo.yaml*and paste in the following YAML.`--- kind: ConfigMap apiVersion: v1 metadata: labels: app: gmsa-demo name: gmsa-demo namespace: default data: run.ps1: | $ErrorActionPreference = "Stop" Write-Output "Configuring IIS with authentication." # Add required Windows features, since they are not installed by default. Install-WindowsFeature "Web-Windows-Auth", "Web-Asp-Net45" # Create simple ASP.NET page. New-Item -Force -ItemType Directory -Path 'C:\inetpub\wwwroot\app' Set-Content -Path 'C:\inetpub\wwwroot\app\default.aspx' -Value 'Authenticated as <B><%=User.Identity.Name%></B>, Type of Authentication: <B><%=User.Identity.AuthenticationType%></B>' # Configure IIS with authentication. Import-Module IISAdministration Start-IISCommitDelay (Get-IISConfigSection -SectionPath 'system.webServer/security/authentication/windowsAuthentication').Attributes['enabled'].value = $true (Get-IISConfigSection -SectionPath 'system.webServer/security/authentication/anonymousAuthentication').Attributes['enabled'].value = $false (Get-IISServerManager).Sites[0].Applications[0].VirtualDirectories[0].PhysicalPath = 'C:\inetpub\wwwroot\app' Stop-IISCommitDelay Write-Output "IIS with authentication is ready." C:\ServiceMonitor.exe w3svc --- apiVersion: apps/v1 kind: Deployment metadata: labels: app: gmsa-demo name: gmsa-demo namespace: default spec: replicas: 1 selector: matchLabels: app: gmsa-demo template: metadata: labels: app: gmsa-demo spec: securityContext: windowsOptions: gmsaCredentialSpecName: aks-gmsa-spec containers: - name: iis image: mcr.microsoft.com/windows/servercore/iis:windowsservercore-ltsc2019 imagePullPolicy: IfNotPresent command: - powershell args: - -File - /gmsa-demo/run.ps1 volumeMounts: - name: gmsa-demo mountPath: /gmsa-demo volumes: - configMap: defaultMode: 420 name: gmsa-demo name: gmsa-demo nodeSelector: kubernetes.io/os: windows --- apiVersion: v1 kind: Service metadata: labels: app: gmsa-demo name: gmsa-demo namespace: default spec: ports: - port: 80 targetPort: 80 selector: app: gmsa-demo type: LoadBalancer`

Apply the changes from

*gmsa-demo.yaml*using the`kubectl apply`

command.`kubectl apply -f gmsa-demo.yaml`

Get the IP address of the sample application using the

`kubectl get service`

command.`kubectl get service gmsa-demo --watch`

Initially, the

`EXTERNAL-IP`

for the`gmsa-demo`

service shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE gmsa-demo LoadBalancer 10.0.37.27 <pending> 80:30572/TCP 6s`

When the

`EXTERNAL-IP`

address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`gmsa-demo LoadBalancer 10.0.37.27 EXTERNAL-IP 80:30572/TCP 2m`

Open a web browser to the external IP address of the

`gmsa-demo`

service.Authenticate with the

`$NETBIOS_DOMAIN_NAME\$AD_USERNAME`

and password and confirm you see`Authenticated as $NETBIOS_DOMAIN_NAME\$AD_USERNAME, Type of Authentication: Negotiate`

.

### Disable GMSA on an existing cluster

Disable GMSA on an existing cluster with Windows Server nodes using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--resource-group myResourceGroup \
--name myAKSCluster \
--disable-windows-gmsa
```


You can reenable GMSA on an existing cluster by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

## Troubleshooting

### No authentication is prompted when loading the page

If the page loads, but you aren't prompted to authenticate, use the `kubectl logs POD_NAME`

command to display the logs of your pod and verify you see *IIS with authentication is ready*.

Windows containers don't show logs on kubectl by default. To enable Windows containers to show logs, you need to embed the Log Monitor tool on your Windows image. For more information, see [Windows Container Tools](https://github.com/microsoft/windows-container-tools).

### Connection timeout when trying to load the page

If you receive a connection timeout when trying to load the page, verify the sample app is running using the `kubectl get pods --watch`

command. Sometimes the external IP address for the sample app service is available before the sample app pod is running.

### Pod fails to start and a winapi error shows in the pod events

If your pod doesn't start after running the `kubectl get pods --watch`

command and waiting several minutes, use the `kubectl describe pod POD_NAME`

command. If you see a *winapi error* in the pod events, it's likely an error in your GMSA cred spec configuration. Verify all the replacement values in *gmsa-spec.yaml* are correct, rerun `kubectl apply -f gmsa-spec.yaml`

, and redeploy the sample application.

### Container Credential Guard event logs show the directory service isn't available errors

If you see this error message, it might indicate that DNS queries are failing due to blocked TCP fallback.

When gMSA is enabled, the system performs DNS lookups to locate domain controllers, for example `_ldap._tcp.dc._msdcs.<domain>`

. In large Active Directory environments, these responses can exceed the 512-byte UDP limit. When the UDP limit is reached, the DNS server sets the truncated (TC) flag, prompting CoreDNS to retry the query over TCP, as required by [RFC5966](https://datatracker.ietf.org/doc/html/rfc5966). This fallback to TCP is essential for completing the authentication flow. If network security group (NSG) or firewall rules block TCP traffic on port 53, the DNS resolution, and therefore gMSA sign in fails.

To verify if this error is occurring in your environment, enable [CoreDNS query logging](coredns-custom) and use the `kubectl logs --namespace kube-system -l k8s-app=kube-dns`

command to view CoreDNS logs.

Look for patterns like this, where UDP responses are truncated and TCP retries fail:

```
[INFO] 10.123.123.200:62380 - 2 "ANY IN _ldap._tcp.dc._msdcs.contoso.com. udp 49 false 512" NOERROR qr,aa,tc,rd,ra 1357 0.003399698s
[INFO] 10.123.123.200:64233 - 2 "ANY IN _ldap._tcp.dc._msdcs.contoso.com. tcp 49 false 65535" - - 0 6.009670817s
[ERROR] plugin/errors: 2 _ldap._tcp.dc._msdcs.contoso.com. ANY: read tcp 10.123.123.11:55216-><DNS server IP>:53: i/o timeout
```


To resolve this error, we recommend updating your NSG or firewall rules to explicitly allow DNS traffic over TCP on port 53. This update will ensure that large DNS responses can be successfully retried over TCP, enabling the authentication flow to complete as expected.

## Next steps

For more information, see [Windows containers considerations with Azure Kubernetes Service (AKS)](windows-vs-linux-containers).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/managed-identity-overview -->

# Overview of managed identities in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of system-assigned and user-assigned managed identities in AKS, including how they work, role assignments, and AKS-specific managed identity features.

To enable a managed identity on a new or existing AKS cluster, see [Use a managed identity in Azure Kubernetes Service (AKS)](use-managed-identity). For more information about managed identities in Azure, see the [Managed identities for Azure resources documentation](/en-us/entra/identity/managed-identities-azure-resources/).

Note

The system-assigned and user-assigned identity types differ from a [workload identity](workload-identity-overview), which is intended for use by an application running on a pod.

## AKS managed identity authorization flow

AKS clusters use system-assigned or user-assigned [managed identities](/en-us/entra/identity/managed-identities-azure-resources/overview) to request tokens from Microsoft Entra. These tokens help authorize access to other resources running in Azure. You assign an [Azure role-based access control (Azure RBAC)](/en-us/azure/role-based-access-control/overview) role to the managed identity to grant it permissions to a particular Azure resource. For example, you can grant permissions to a managed identity to access secrets in an Azure key vault for use by the cluster.

### Managed identity behavior in AKS

When you deploy an AKS cluster, a system-assigned managed identity is created for you by default. You can also create the cluster with a user-assigned managed identity, or update an existing cluster to a different type of managed identity.

If your cluster already uses a managed identity and you change the identity type (for example, from system-assigned to user-assigned), there's a delay while control plane components switch to the new identity. Control plane components continue to use the old identity until its token expires. After the token refreshes, they switch to the new identity. This process can take several hours.

Note

It's also possible to create a cluster with an application [service principal](kubernetes-service-principal) rather that a managed identity. However, we recommend using a managed identity over an application service principal for security and ease of use. If you have an existing cluster that uses an application service principal, you can update it to use a managed identity.

### AKS identity and credential management

The Azure platform manages both system-assigned and user-assigned managed identities and their credentials, so you can authorize access from your applications without needing to provision or rotate any secrets.

## System-assigned managed identity

The following table summarizes the key characteristics of a system-assigned managed identity in AKS:

| Creation | Lifecycle | Sharing across resources | Common use cases |
|---|---|---|---|
| Created as part of an Azure resource, such as an AKS cluster | Tied to the lifecycle of the parent resource, so it gets deleted when the parent resource is deleted | Can only be associated with a single resource | • Workloads contained within a single Azure resource • Workloads that require independent identities |

### User-assigned managed identity

The following table summarizes the key characteristics of a user-assigned managed identity in AKS:

| Creation | Lifecycle | Sharing across resources | Common use cases |
|---|---|---|---|
| Created as a standalone Azure resource, and must exist prior to cluster creation | Independent of the lifecycle of any specific resource, so it requires manual deletion if no longer needed | Can be shared across multiple resources | • Workloads that run on multiple resources and can share a single identity • Workloads that require preauthorization to a secure resource as part of a provisioning process • Workloads where resources are recycled frequently but need consistent permissions |

### Pre-created kubelet managed identity

A pre-created kubelet managed identity is an optional user-assigned identity that kubelet can use to access other resources in Azure. This feature enables scenarios such as connection to Azure Container Registry (ACR) during cluster creation. If you don't specify a user-assigned managed identity for kubelet, AKS creates a user-assigned kubelet identity in the node resource group. For a user-assigned kubelet identity outside the default worker node resource group, you need to assign the [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) role on the kubelet identity for control plane managed identity.

## Role assignments for managed identities in AKS

You can assign an Azure RBAC role to a managed identity to grant the cluster permissions on another Azure resource. Azure RBAC supports both built-in and custom role definitions that specify levels of permissions. To assign a role, see [Steps to assign an Azure role](/en-us/azure/role-based-access-control/role-assignments-steps).

When you assign an Azure RBAC role to a managed identity, you must define the scope for the role. In general, it's a best practice to limit the scope of a role to the minimum privileges required by the managed identity. For more information on scoping Azure RBAC roles, see [Understand scope for Azure RBAC](/en-us/azure/role-based-access-control/scope-overview).

### Control plane managed identity role assignments

When you create and use your own VNet, attached Azure disks, static IP address, route table, or user-assigned kubelet identity where the resources are outside of the worker node resource group, the Azure CLI adds the role assignment automatically. If you're using an ARM template or another method, use the principal ID of the managed identity to perform a role assignment.

If you're not using the Azure CLI, but you're using your own VNet, attached Azure disks, static IP address, route table, or user-assigned kubelet identity that's outside of the worker node resource group, we recommend using a [user-assigned managed identity for the control plane](use-managed-identity#create-a-user-assigned-managed-identity).

When the control plane uses a system-assigned managed identity, the identity is created at the same time as the cluster, so the role assignment can't be performed until after cluster creation.

## Summary of managed identities used by AKS

AKS uses several managed identities for built-in services and add-ons. The following table summarizes the managed identities used by AKS, their use cases, default permissions, and whether you can bring your own identity:

| Identity | Name | Use case | Default permissions | Bring your own identity |
|---|---|---|---|---|
| Control plane | AKS cluster name | Used by AKS control plane components to manage cluster resources including ingress load balancers and AKS-managed public IPs, Cluster Autoscaler, Azure Disk, File, Blob CSI drivers | Contributor role for Node resource group | Supported |
| Kubelet | AKS cluster name-agentpool | Authentication with Azure Container Registry (ACR) | N/A for Kubernetes version 1.15 and later | Supported |
| Add-on | AzureNPM | No identity required | N/A | Unsupported |
| Add-on | AzureCNI network monitoring | No identity required | N/A | Unsupported |
| Add-on | azure-policy (gatekeeper) | No identity required | N/A | Unsupported |
| Add-on | Calico | No identity required | N/A | Unsupported |
| Add-on | application-routing | Manages Azure DNS and Azure Key Vault certificates | Key Vault Secrets User role for Key Vault, DNS Zone Contributor role for DNS zones, Private DNS Zone Contributor role for private DNS zones | Unsupported |
| Add-on | HTTPApplicationRouting | Manages required network resources | Reader role for node resource group, contributor role for DNS zone | Unsupported |
| Add-on | Ingress application gateway | Manages required network resources | Contributor role for node resource group | Unsupported |
| Add-on | omsagent | Used to send AKS metrics to Azure Monitor | Monitoring Metrics Publisher role | Unsupported |
| Add-on | Virtual-Node (ACIConnector) | Manages required network resources for Azure Container Instances (ACI) | Contributor role for node resource group | Unsupported |
| Add-on | Cost analysis | Used to gather cost allocation data | N/A | Supported |
| Workload identity | Microsoft Entra Workload ID | Enables applications to access cloud resources securely with Microsoft Entra Workload ID | N/A | Unsupported |

## Next step: Enable managed identities in AKS

To learn how to enable managed identities on a new or existing AKS cluster, see [Use a managed identity in Azure Kubernetes Service (AKS)](use-managed-identity).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/nvidia-gpu-operator -->

# Use NVIDIA GPU Operator on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The NVIDIA GPU Operator automates the management and deployment of all NVIDIA software components needed to provision GPU including driver installation, the [NVIDIA device plugin for Kubernetes](https://github.com/NVIDIA/k8s-device-plugin?tab=readme-ov-file), the NVIDIA container runtime, and more. Since the NVIDIA GPU Operator handles these components, it's not necessary to separately install the NVIDIA device plugin on your AKS cluster. This also means that the automatic GPU driver installation should be skipped in order to use the NVIDIA GPU Operator on AKS.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the Azure CLI version 2.72.2 or later installed to set the
`--gpu-driver`

field. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Note

GPU-enabled VMs contain specialized hardware subject to higher pricing and region availability. For more information, see the [pricing](free-standard-pricing-tiers) tool and [region availability](quotas-skus-regions).

## Limitations

- NVIDIA GPU Operator isn't supported for the following OS options: Windows Server versions,
[Flatcar Container Linux for AKS (preview)](flatcar-container-linux-for-aks), and[Azure Linux with OS Guard for AKS (preview)](use-azure-linux-os-guard).

## Get the credentials for your cluster

Get the credentials for your AKS cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. The following example command gets the credentials for the cluster

`myAKSCluster`

in the `myResourceGroup`

resource group:```
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```


Note

The NVIDIA GPU Operator is not compatible with multiple OS versions on the same AKS cluster.

Skip automatic GPU driver installation by creating an NVIDIA GPU-enabled node pool using the [

`az aks nodepool add`

][az-aks-nodepool-add] command and setting the API field`--gpu-driver`

to the value`none`

. Setting this API field to`none`

during node pool creation skips the default GPU driver installation, see[this example](gpu-cluster#skip-gpu-driver-installation). Any existing nodes aren't changed. You can scale the node pool to zero and then back up to make the change take effect.Follow the NVIDIA documentation to

[Install the GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html).Now that you successfully installed the GPU Operator, you can check that your

[GPUs are schedulable](gpu-cluster#confirm-that-gpus-are-schedulable)and[run a GPU workload](gpu-cluster#run-a-gpu-enabled-workload).

Note

There might be additional considerations to take when using the NVIDIA GPU Operator and deploying on SPOT instances. Please refer to [https://github.com/NVIDIA/gpu-operator/issues/577](https://github.com/NVIDIA/gpu-operator/issues/577)

## Next steps

[Monitor NVIDIA GPU metrics](monitor-gpu-metrics)using Azure Managed Prometheus and Azure Managed Grafana.- Learn more about
[Ray clusters on AKS](ray-overview).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-app-configuration-settings -->

# Configure the Azure App Configuration extension for your Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Once you [created the Azure App Configuration extension](azure-app-configuration), you can configure the extension to work best for you and your project using various configuration options, like:

- Configuring the replica count.
- Configuring the log verbosity.
- Configuring the installation namespace.

The extension enables you to configure Azure App Configuration extension settings by using the `--configuration-settings`

parameter in the Azure CLI.

Tip

For a list of available options, see [Azure App Configuration Kubernetes Provider helm values](https://raw.githubusercontent.com/Azure/AppConfiguration-KubernetesProvider/main/deploy/parameter/helm-values.yaml).

## Configure the replica count

The default replica count is `1`

. Create Azure App Configuration extension with customized replica count:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--configuration-settings "replicaCount=3"
```


Note

If configuration settings are sensitive and need to be protected (for example, cert-related information), pass the `--configuration-protected-settings`

parameter and the value will be protected from being read.

## Configure the log verbosity

The default log verbosity is `1`

. Create Azure App Configuration extension with customized log verbosity:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--configuration-settings "logVerbosity=3"
```


Log verbosity levels follow the [klog](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-instrumentation/logging.md#what-method-to-use) convention:

`0`

: Warning and error only.`1`

: Informational, this level is default.`2`

: Detailed steady state information.`3`

: Extended information about changes.`4`

: Debug level verbosity.`5`

: Trace level verbosity.

## Configure the Azure App Configuration extension namespace

The Azure App Configuration extension gets installed in the `azappconfig-system`

namespace by default. To override it, use `--release-namespace`

. Include the cluster `--scope`

to redefine the namespace.

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--scope cluster \
--release-namespace custom-namespace
```


## Show current configuration settings

Use the `az k8s-extension show`

command to show the current Azure App Configuration extension settings:

```
az k8s-extension show --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider
```


## Update configuration settings

To update your Azure App Configuration extension settings, recreate the extension with the desired state. For example, assume we installed the extension using the following configuration:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--configuration-settings "replicaCount=2"
```


To update the `replicaCount`

from two to three, use the following command:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--configuration-settings "replicaCount=3"
```


## Next Steps

Once you successfully install Azure App Configuration extension in your AKS cluster, try [quickstart](/en-us/azure/azure-app-configuration/quickstart-azure-kubernetes-service) to learn how to use it.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/optimize-aks-costs -->

# Optimize Azure Kubernetes Service (AKS) usage and costs

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides guidance on how to optimize your Azure Kubernetes Service (AKS) usage and costs. It covers guidance on the following topics:

## Automatic scaling

### Horizontal pod autoscaling

The * Horizontal Pod Autoscaler (HPA)* monitors resource demand and automatically updates a workload resource to automatically scale the number of pods to match demand. The response to increased load is to deploy more pods. If the load decreases and the number of pods is above the configured minimum, the autoscaler tells the workload resource to scale down.

The Metrics API gets data from the kubelet every 60 seconds, and the HPA checks the Metrics API every 15 seconds for any needed changes by default. This means that the HPA updates every 60 seconds. When you configure the HPA for a deployment, you define the minimum and maximum number of replicas that can run and the metrics that the HPA uses to determine when to scale.

For more information, see [Horizontal Pod Autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) and [Autoscale pods in AKS](tutorial-kubernetes-scale#autoscale-pods).

### Kubernetes event-driven autoscaling

The [Kubernetes Event-driven Autoscaler (KEDA)](https://keda.sh/) applies event-driven autoscaling to your workloads. KEDA works with the HPA and can extend functionality without overwriting or duplication.

You can use the KEDA add-on for AKS to scale your applications and leverage a [rich catalog of Azure KEDA scalers](https://keda.sh/docs/2.16/scalers/). For more information, see [Application autoscaling with the KEDA add-on](keda-about) and [Install the KEDA add-on for AKS](keda-deploy-add-on-cli).

### Vertical pod autoscaling

The * Vertical Pod Autoscaler (VPA)* automatically sets resource requests and limits on containers per workload based on past usage. The VPA frees up CPU and Memory for pods to ensure effective utilization of your AKS clusters. Over time, the VPA provides recommendations for resource usage.

For more information, see [Vertical pod autoscaling in Azure Kubernetes Service (AKS)](vertical-pod-autoscaler) and [Use the Vertical Pod Autoscaler (VPA) in Azure Kubernetes Service (AKS)](use-vertical-pod-autoscaler).

## Cluster right-sizing

### Right-size your cluster

It's important to * right-size your clusters* to optimize costs and performance. You can manually resize a cluster by adding or removing the nodes to meet the needs of your applications. You can also autoscale your cluster to automatically adjust the number of nodes in response to changing demands.

For more information, see [Resize Azure Kubernetes Service (AKS) clusters](resize-cluster).

### Cluster autoscaling

With the * cluster autoscaler*, you can automatically scale node pools based on resource usage and constraints, such as scaling up to schedule pending pods or scaling down to reduce costs for unused nodes. The

[cluster autoscaler profile](cluster-autoscaler-overview#cluster-autoscaler-profile)is a set of parameters that you can fine-tune to control the behavior of the cluster autoscaler.

For more information, see [Cluster autoscaling in Azure Kubernetes Service (AKS) overview](cluster-autoscaler-overview) and [Use the cluster autoscaler in Azure Kubernetes Service (AKS)](cluster-autoscaler).

### Node autoprovisioning (preview)

* Node autoprovisioning (NAP)* (preview), based on the open-source

[Karpenter](https://karpenter.sh/)project, helps you provision the right infrastructure based on the pending pod resource requirements of your workloads. With efficient bin-packing, you can consolidate your workloads onto the right-sized infrastructure to reduce operating costs.

For more information, see [Node autoprovisioning (preview) in Azure Kubernetes Service (AKS)](node-autoprovision).

## GPU optimizations

### GPU partitioning and sharing

GPU partitioning helps combat underutilization by splitting up or sharing GPUs across multiple workloads. The following sections cover different ways to partition and share GPUs in AKS.

#### Time-slicing

The [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/overview.html) enables the * time-slicing* of GPUs in Kubernetes clusters. With time-slicing, a system administrator can define a set of

*replicas*for a GPU, each of which can be handed out independently to a pod to run workloads on. You can apply cluster-wide default time-slicing configurations and node-specific configurations.


For more information, see [Time-slicing GPUs in Kubernetes](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/gpu-sharing.html).

#### Multi-processing service (MPS)

A single process might not utilize all the memory and compute bandwidth capacity available on a GPU. The * Multi-Process Service (MPS)* enables logical partitioning of memory and compute resources between workloads and allows kernel and memcopy operations from different processes to overlap on the GPU. MPS helps you achieve higher GPU utilization and shorter running times.


For more information, see [Multi-Process Service (MPS)](https://docs.nvidia.com/deploy/mps/index.html#mps).

#### Multi-instance GPUs (MIGs)

* Multi-instance GPUs (MIGs)* enable you to partition GPUs based on the NVIDIA Ampere and later architectures into separate and secure GPU instances for CUDA applications.


For more information, see [GPU Operator with MIG](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/gpu-operator-mig.html) and [Create a multi-instance GPU node pool in Azure Kubernetes Service (AKS)](gpu-multi-instance).

## Multitenancy

Multitenancy refers to the sharing of infrastructure across tenants, teams, and business units. The following table outlines different ways to implement multitenancy in AKS:

| Multitenancy type | Multitenancy level | Cluster pod density | Cost allocation | Ideal use case | Potential risks |
|---|---|---|---|---|---|
Dedicated cluster |

• Lower pod density and more overprovisioned resources

**Dedicated node pool**• Requires extra cluster configurations, like network policies, quota management, role-based access control (RBAC), etc.

**Dedicated namespace**• Requires extra cluster configurations, like network policies, quota management, role-based access control (RBAC), etc.

### Dedicated cluster

With * dedicated cluster multitenancy*, clusters are dedicated to a single workload or team.


The following table outlines pros and cons of using a dedicated cluster:

| Pros | Cons |
|---|---|
| • Easier isolation method • Straightforward cost allocation and chargeback • Great for cases where tenants don't trust each other (often from security and resource sharing perspectives) |
• High management and financial overhead • Generally low pod density and overprovisioned resources |

### Dedicated node pool

With * dedicated node pool multitenancy*, clusters are shared by many tenants.


The following table outlines pros and cons of using a dedicated node pool:

| Pros | Cons |
|---|---|
| • Medium pod density • Some shared infrastructure • Apply Azure tags to node pools dedicated to a single tenant (tags propagate to nodes and persist through upgrades) |
• Requires trust between the tenants • Requires extra cluster configurations, like network policies, quota management, role-based access control (RBAC), etc. |

### Dedicated namespace

With * dedicated namespace multitenancy*, clusters are shared by many tenants, with namespaces serving as the isolation boundary.


The following table outlines pros and cons of using a dedicated namespace:

| Pros | Cons |
|---|---|
| • Higher pod density • Best binpacking • Sharing infrastructure to maximize resource utilization |
• Unsafe for hostile environments by default • Requires extra security measures in place if all tenants can't be trusted |

## Azure discounts

To take savings one step further, take advantage of Azure discounts such as Azure Savings Plans, Reserved Instances, and Azure Hybrid Benefits.

| Azure discount type | Details |
|---|---|
Azure Savings Plans |

• Save up to 65% compared to pay-as-you-go

• Flexible, with no SKU family or region restrictions

• Best for workloads with consistent costs with resources in various SKUs and regions

**Reserved Instances**• Save up to 72% compared to pay-as-you-go

• Restricted to specific SKU families and regions

• Best for stable workloads running continuously (with no unexpected SKU or region changes)

**Azure Hybrid Benefits**• Use any qualifying on-premises licenses that have an active Software Assurance (SA) or qualifying subscription

## Next steps

To learn more about cost in AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-upgrade-github-actions -->

# Apply automatic security upgrades to Azure Kubernetes Service (AKS) nodes using GitHub Actions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Security updates are a key part of maintaining your AKS cluster's security and compliance with the latest fixes for the underlying OS. These updates include OS security fixes or kernel updates. Some updates require a node reboot to complete the process.

This article shows you how you can automate the update process of AKS nodes using GitHub Actions and Azure CLI to create an update task based on `cron`

that runs automatically.

Note

You can also perform node image upgrades automatically and schedule these upgrades using planned maintenance. For more information, see [Automatically upgrade node images](auto-upgrade-node-image).

## Before you begin

- This article assumes you have an existing AKS cluster. If you need an AKS cluster, create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[the Azure portal](learn/quick-kubernetes-deploy-portal). - This article also assumes you have a
[GitHub account](https://github.com)and a[profile repository](https://docs.github.com/en/free-pro-team@latest/github/setting-up-and-managing-your-github-profile/about-your-profile)to host your actions. If you don't have a repository, create one with the same name as your GitHub username. - You need the Azure CLI version 2.0.59 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Update nodes with `az aks upgrade`


The `az aks upgrade`

command gives you a zero downtime way to apply updates. The command performs the following actions:

- Applies the latest updates to all your cluster's nodes.
- Cordons (makes the node unavailable for the scheduling of new workloads) and drains (moves the existent workloads to other node) traffic to the nodes.
- Restarts the nodes.
- Enables the updated nodes to receive traffic again.

AKS doesn't automatically restart your nodes if you update them using a different method.

Note

Running `az aks upgrade`

with the `--node-image-only`

flag only upgrades the node images. Running the command without the flag upgrades both the node images and the Kubernetes control plane version. For more information, see the [docs for managed upgrades on nodes](node-image-upgrade) and the [docs for cluster upgrades](upgrade-cluster).

All Kubernetes nodes run in a standard Windows or Linux-based Azure virtual machine (VM). The Linux-based VMs use an Ubuntu image with the OS configured to automatically check for updates every night.

When you use the `az aks upgrade`

command, Azure CLI creates a surge of new nodes with the latest security and kernel updates. These new nodes are initially cordoned to prevent any apps from being scheduled to them until the update completes. After the update completes, Azure cordons and drains the older nodes and uncordons the new ones, transferring all the scheduled applications to the new nodes.

This process is better than updating Linux-based kernels manually because Linux requires a reboot when a new kernel update is installed. If you update the OS manually, you also need to reboot the VM, manually cordoning and draining all the apps.

## Create a timed GitHub Action

`cron`

is a utility that allows you to run a set of commands, or *jobs*, on an automated schedule. To create a job to update your AKS nodes on an automated schedule, you need a repository to host your actions. GitHub Actions are usually configured in the same repository as your application, but you can use any repository.

Navigate to your repository on GitHub.

Select

**Actions**.Select

**New workflow**>**Set up a workflow yourself**.Create a GitHub Action named

*Upgrade cluster node images*with a schedule trigger to run every 15 days at 3am. Copy the following code into the YAML:`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *'`

Create a job named

*upgrade-node*that runs on an Ubuntu agent and connects to your Azure CLI account to execute the node upgrade command. Copy the following code into the YAML under the`on`

key:`jobs: upgrade-node: runs-on: ubuntu-latest`


## Set up the Azure CLI in the workflow

In the

**Search Marketplace for Actions**bar, search for**Azure Login**.Select

**Azure Login**.Under

**Installation**, select a version, such as*v1.4.6*, and copy the installation code snippet.Add the

`steps`

key and the following information from the installation code snippet to the YAML:`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *' jobs: upgrade-node: runs-on: ubuntu-latest steps: - name: Azure Login uses: Azure/login@v1.4.6 with: creds: ${{ secrets.AZURE_CREDENTIALS }}`


## Create credentials for the Azure CLI

In a new browser window, create a new service principal using the

command. Make sure you replace`az ad sp create-for-rbac`

`*{subscriptionID}*`

with your own subscription ID.Note

This example creates the

`Contributor`

role at the*Subscription*scope. You can provide the role and scope that meets your needs. For more information, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles)and[Azure RBAC scope levels](/en-us/azure/role-based-access-control/scope-overview#scope-format).`az ad sp create-for-rbac --role Contributor --scopes /subscriptions/{subscriptionID} -o json`

Your output should be similar to the following example output:

`{ "appId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "displayName": "xxxxx-xxx-xxxx-xx-xx-xx-xx-xx", "password": "xxxxxxxxxxxxxxxxxxxxxxxxxxxx", "tenant": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" }`

Copy the output and navigate to your GitHub repository.

Select

**Settings**>**Secrets and variables**>**Actions**>**New repository secret**.For

**Name**, enter`AZURE_CREDENTIALS`

.For

**Secret**, copy in the contents of the output you received when you created the service principal.Select

**Add Secret**.

## Create the steps to execute the Azure CLI commands

Navigate to your window with the workflow YAML.

In the

**Search Marketplace for Actions**bar, search for**Azure CLI Action**.Select

**Azure CLI Action**.Under

**Installation**, select a version, such as*v1.0.8*, and copy the installation code snippet.Paste the contents of the action into the YAML below the

`*Azure Login*`

step, similar to the following example:`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *' jobs: upgrade-node: runs-on: ubuntu-latest steps: - name: Azure Login uses: Azure/login@v1.4.6 with: creds: ${{ secrets.AZURE_CREDENTIALS }} - name: Upgrade node images uses: Azure/cli@v1.0.8 with: inlineScript: az aks upgrade --resource-group <resourceGroupName> --name <aksClusterName> --node-image-only --yes`

Tip

You can decouple the

`--resource-group`

and`--name`

parameters from the command by creating new repository secrets like you did for`AZURE_CREDENTIALS`

.If you create secrets for these parameters, you need to replace the

`<resourceGroupName>`

and`<aksClusterName>`

placeholders with their secret counterparts. For example,`${{secrets.RESOURCE_GROUP_NAME}}`

and`${{secrets.AKS_CLUSTER_NAME}}`

Rename the YAML to

`upgrade-node-images.yml`

.Select

**Commit changes...**, add a commit message, and then select**Commit changes**.

## Run the GitHub Action manually

You can run the workflow manually in addition to the scheduled run by adding a new `on`

trigger called `workflow_dispatch`

.

Note

If you want to upgrade a single node pool instead of all node pools on the cluster, add the `--name`

parameter to the `az aks nodepool upgrade`

command to specify the node pool name. For example:

```
az aks nodepool upgrade --resource-group <resourceGroupName> --cluster-name <aksClusterName> --name <nodePoolName> --node-image-only
```


Add the

`workflow_dispatch`

trigger under the`on`

key:`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *' workflow_dispatch:`

The YAML should look similar to the following example:

`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *' workflow_dispatch: jobs: upgrade-node: runs-on: ubuntu-latest steps: - name: Azure Login uses: Azure/login@v1.4.6 with: creds: ${{ secrets.AZURE_CREDENTIALS }} - name: Upgrade node images uses: Azure/cli@v1.0.8 with: inlineScript: az aks upgrade -g {resourceGroupName} -n {aksClusterName} --node-image-only --yes # Code for upgrading one or more node pools`


## Next steps

For more information about AKS upgrades, see the following articles and resources:

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/managed-namespaces -->

# Use managed namespaces in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic ✔️ AKS Standard

Managed namespaces in Azure Kubernetes Service (AKS) provide a way to logically isolate workloads and teams within a cluster. This feature enables administrators to enforce resource quotas, apply network policies, and manage access control at the namespace level. For a detailed overview of managed namespaces, see the [managed namespaces overview](concepts-managed-namespaces).

## Before you begin

### Prerequisites

- An Azure account with an active subscription. If you don't have one, you can
[create an account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F). - An
[AKS cluster](automatic/quick-automatic-managed-network)set up in your Azure environment with[Azure role-based access control for Kubernetes authorization](manage-azure-rbac)is required if you intend to utilize Azure RBAC roles. - To use the network policy feature, the AKS cluster needs to be
[configured with a network policy engine](use-network-policies#network-policy-options-in-aks). Cilium is our recommended engine.

| Prerequisite | Notes |
|---|---|
Azure CLI |
`2.80.0` or later installed. To find the CLI version, run `az --version` . If you need to install or upgrade, see
|
AKS API Version |
`2025-09-01` or later. |
Required permission(s) |
`Microsoft.ContainerService/managedClusters/managedNamespaces/*` or `Azure Kubernetes Service Namespace Contributor` built-in role. `Microsoft.Resources/deployments/*` on the resource group containing the cluster. For more information, see
|

### Limitations

- Trying to on-board system namespaces such as
`kube-system`

,`app-routing-system`

,`istio-system`

,`gatekeeper-system`

, etc. to be managed namespaces isn't allowed. - When a namespace is a managed namespace, changes to the namespace via the Kubernetes API are blocked.

- Listing existing namespaces to convert in the portal doesn't work with private clusters. You can add new namespaces.

## Create a managed namespace on a cluster and assign users

Note

When you create a managed namespace, a component is installed on the cluster to reconcile the namespace with the state in Azure Resource Manager. This component blocks changes to the managed fields and resources from the Kubernetes API, ensuring consistency with the desired configuration.

The following Bicep example demonstrates how to create a managed namespace as a subresource of a managed cluster. Make sure to select the appropriate value for `defaultNetworkPolicy`

, `adoptionPolicy`

, and `deletePolicy`

. For more information about what those parameters mean, see the [managed namespaces overview](concepts-managed-namespaces).

```
resource existingCluster 'Microsoft.ContainerService/managedClusters@2024-03-01' existing = {
name: 'contoso-cluster'
}
resource managedNamespace 'Microsoft.ContainerService/managedClusters/managedNamespaces@2025-09-01' = {
parent: existingCluster
name: 'retail-team'
location: location
properties: {
defaultResourceQuota: {
cpuRequest: '1000m'
cpuLimit: '2000m'
memoryRequest: '512Mi'
memoryLimit: '1Gi'
}
defaultNetworkPolicy: {
ingress: 'AllowSameNamespace'
egress: 'AllowAll'
}
adoptionPolicy: 'IfIdentical'
deletePolicy: 'Keep'
labels: {
environment: 'dev'
}
annotations: {
owner: 'retail'
}
}
}
```


Save the Bicep file **managedNamespace.bicep** to your local computer.

Deploy the Bicep file using the Azure CLI.

```
az deployment group create --resource-group <resource-group> --template-file managedNamespace.bicep
```


### Define variables

Define the following variables to be used in the subsequent steps.

```
RG_NAME=cluster-rg
CLUSTER_NAME=contoso-cluster
NAMESPACE_NAME=retail-team
LABELS="environment=dev"
ANNOTATIONS="owner=retail"
```


### Create the managed namespace

To customize its configuration, managed namespaces have various parameter options to choose from during creation. Make sure to select the appropriate value for `ingress-network-policy`

, `egress-network-policy`

, `adoption-policy`

, and `delete-policy`

. For more information about what those parameters mean, see the [managed namespaces overview](concepts-managed-namespaces).

```
az aks namespace add \
--name ${NAMESPACE_NAME} \
--cluster-name ${CLUSTER_NAME} \
--resource-group ${RG_NAME} \
--cpu-request 1000m \
--cpu-limit 2000m \
--memory-request 512Mi \
--memory-limit 1Gi \
--ingress-policy [AllowSameNamespace|AllowAll|DenyAll] \
--egress-policy [AllowSameNamespace|AllowAll|DenyAll] \
--adoption-policy [Never|IfIdentical|Always] \
--delete-policy [Keep|Delete] \
--labels ${LABELS} \
--annotations ${ANNOTATIONS}
```


### Assign role

After the namespace is created, you can assign [one of the built-in roles](concepts-managed-namespaces#managed-namespaces-built-in-roles) for the control plane and data plane.

```
ASSIGNEE="user@contoso.com"
NAMESPACE_ID=$(az aks namespace show --name ${NAMESPACE_NAME} --cluster-name ${CLUSTER_NAME} --resource-group ${RG_NAME} --query id -o tsv)
```


Assign a control plane role to be able to view the managed namespace in the portal, Azure CLI output, and Azure Resource Manager. This role also allows the user to retrieve the credentials to connect to this namespace.

```
az role assignment create \
--assignee ${ASSIGNEE} \
--role "Azure Kubernetes Service Namespace User" \
--scope ${NAMESPACE_ID}
```


Assign data plane role to be able to get access to create resources within the namespace using the Kubernetes API.

```
az role assignment create \
--assignee ${ASSIGNEE} \
--role "Azure Kubernetes Service RBAC Writer" \
--scope ${NAMESPACE_ID}
```


- Sign in to the
[Azure portal](https://portal.azure.com). - On the Azure portal home page, select
**Create a resource**. - In the
**Categories**section, select**Managed Kubernetes Namespaces**. - On the
**Basics**tab, under**Project details**configure the following settings:- Select the target
**cluster**to create the namespace on. - If you're creating a new namespace, leave the default
**create new**, otherwise choose**change existing to managed**to convert an existing namespace.

- Select the target
- Configure the
**networking policy**to be applied on the namespace. - Configure the
**resource requests and limits**for the namespace. - Select the
**members (users or groups)**and their**role**.- Assign the
**Azure Kubernetes Service Namespace User**role to give them access to view the managed namespace in the portal, Azure CLI output, and Azure Resource Manager. This role also allows the user to retrieve the credentials to connect to this namespace. - Assign the
**Azure Kubernetes Service RBAC Writer**role to give them access to create resources within the namespace using the Kubernetes API.

- Assign the
- Select
**Review + create**to run validation on the configuration. After validation completes, select**Create**.

## List managed namespaces

You can list managed namespaces at different scopes using the Azure CLI.

### Subscription level

Run the following command to list all managed namespaces in a subscription.

```
az aks namespace list --subscription <subscription-id>
```


### Resource group level

Run the following command to list all managed namespaces in a specific resource group.

```
az aks namespace list --resource-group <rg-name>
```


### Cluster level

Run the following command to list all managed namespaces in a specific cluster.

```
az aks namespace list --resource-group <rg-name> --cluster-name <cluster-name>
```


## List managed namespaces

You can list managed namespaces at different scopes using the Azure CLI.

### Subscription level

Run the following command to list all managed namespaces in a subscription.

```
az aks namespace list --subscription <subscription-id>
```


### Resource group level

Run the following command to list all managed namespaces in a specific resource group.

```
az aks namespace list --resource-group <rg-name>
```


### Cluster level

Run the following command to list all managed namespaces in a specific cluster.

```
az aks namespace list --resource-group <rg-name> --cluster-name <cluster-name>
```


## Connect to the cluster

You can retrieve the credentials to connect to a namespace via the following command.

```
az aks namespace get-credentials --name <namespace-name> --resource-group <rg-name> --cluster-name <cluster-name>
```


## Connect to the cluster

You can retrieve the credentials to connect to a namespace via the following command.

```
az aks namespace get-credentials --name <namespace-name> --resource-group <rg-name> --cluster-name <cluster-name>
```


## Next steps

This article focused on using the managed namespaces feature to logically isolate teams and applications. You can further explore other guardrails and best practices to apply via [deployment safeguards](deployment-safeguards).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-labels -->

# Use labels in an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If you have multiple node pools, you may want to add a label during node pool creation. [Kubernetes labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) handle the scheduling rules for nodes. You can add labels to a node pool anytime and apply them to all nodes in the node pool.

In this how-to guide, you learn how to use labels in an Azure Kubernetes Service (AKS) cluster.

## Prerequisites

You need the Azure CLI version 2.2.0 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create an AKS cluster with a label

You can create an AKS cluster with node labels to set key/value metadata for workload scheduling.

```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="myResourceGroup$RANDOM_SUFFIX"
export AKS_CLUSTER_NAME="myAKSCluster$RANDOM_SUFFIX"
az group create --name $RESOURCE_GROUP --location $REGION
```


Results:

```
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx",
"location": "eastus2",
"managedBy": null,
"name": "myResourceGroupxxx",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null,
"type": "Microsoft.Resources/resourceGroups"
}
```


Create the AKS cluster specifying node labels (e.g., dept=IT, costcenter=9000):

```
az aks create \
--resource-group $RESOURCE_GROUP \
--name $AKS_CLUSTER_NAME \
--node-count 2 \
--nodepool-labels dept=IT costcenter=9000 \
--generate-ssh-keys --location $REGION
```


Results:

```
{
"aadProfile": null,
"addonProfiles": {},
"agentPoolProfiles": [
{
"count": 2,
"enableAutoScaling": null,
"mode": "System",
"name": "nodepool1",
"nodeLabels": {
"costcenter": "9000",
"dept": "IT"
}
}
],
"dnsPrefix": "myaksclusterxxx-dns",
"fqdn": "myaksclusterxxx-xxxxxxxx.hcp.eastus2.azmk8s.io",
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.ContainerService/managedClusters/myAKSClusterxxx",
"location": "eastus2",
"name": "myAKSClusterxxx",
"resourceGroup": "myResourceGroupxxx"
}
```


Verify the labels were set:

```
az aks get-credentials --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER_NAME --overwrite-existing
kubectl get nodes --show-labels | grep -e "costcenter=9000" -e "dept=IT"
```


## Create a node pool with a label

You can create an additional node pool with labels for specific scheduling needs.

```
export NODEPOOL_NAME="labelnp"
az aks nodepool add \
--resource-group $RESOURCE_GROUP \
--cluster-name $AKS_CLUSTER_NAME \
--name $NODEPOOL_NAME \
--node-count 1 \
--labels dept=HR costcenter=5000
```


The following is example output from the [ az aks nodepool list](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-list) command showing the

*labelnp*node pool is

*Creating*nodes with the specified

*nodeLabels*:

```
az aks nodepool list --resource-group $RESOURCE_GROUP --cluster-name $AKS_CLUSTER_NAME
```


Results:

```
[
{
"count": 2,
"name": "nodepool1",
"nodeLabels": {
"costcenter": "9000",
"dept": "IT"
}
},
{
"count": 1,
"name": "labelnp",
"nodeLabels": {
"costcenter": "5000",
"dept": "HR"
},
"provisioningState": "Creating"
}
]
```


Verify the labels were set:

```
kubectl get nodes --show-labels | grep -e "costcenter=5000" -e "dept=HR"
```


## Updating labels on existing node pools

You can update the labels on an existing node pool. Note that updating labels will overwrite the old labels.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $AKS_CLUSTER_NAME \
--name $NODEPOOL_NAME \
--labels dept=ACCT costcenter=6000
```


Verify the new labels are set:

```
kubectl get nodes --show-labels | grep -e "costcenter=6000" -e "dept=ACCT"
```


## Unavailable labels

### Reserved system labels

Since the [2021-08-19 AKS release](https://github.com/Azure/AKS/releases/tag/2021-08-19), AKS stopped the ability to make changes to AKS reserved labels. Attempting to change these labels results in an error message.

The following labels are AKS reserved labels. *Virtual node usage* specifies if these labels could be a supported system feature on virtual nodes. Some properties that these system features change aren't available on the virtual nodes because they require modifying the host.

| Label | Value | Example/Options | Virtual node usage |
|---|---|---|---|
`kubernetes.azure.com/agentpool` |
<agent pool name> | `nodepool1` |
Same |
`kubernetes.io/arch` |
<runtime.GOARCH> | `amd64 ` |
N/A |
`kubernetes.io/os` |
<OS Type> | `Linux/Windows` |
Same |
`node.kubernetes.io/instance-type` |
<VM size> | `Standard_NC6s_v3` |
Virtual |
`topology.kubernetes.io/region` |
<Azure region> | `westus2` |
Same |
`topology.kubernetes.io/zone` |
<Azure zone> | `0` |
Same |
`kubernetes.azure.com/cluster` |
<MC_RgName> | `MC_aks_myAKSCluster_westus2` |
Same |
`kubernetes.azure.com/managedby` |
`aks` |
`aks` |
N/A |
`kubernetes.azure.com/mode` |
<mode> | `User` or `system` |
User |
`kubernetes.azure.com/role` |
agent | `Agent` |
Same |
`kubernetes.azure.com/scalesetpriority` |
<VMSS priority> | `spot` or `regular` |
N/A |
`kubernetes.io/hostname` |
<hostname> | `aks-nodepool-00000000-vmss000000` |
Same |
`kubernetes.azure.com/storageprofile` |
<OS disk storage profile> | `Managed` |
N/A |
`kubernetes.azure.com/storagetier` |
<OS disk storage tier> | `Premium_LRS` |
N/A |
`kubernetes.azure.com/node-image-version` |
<VHD version> | `AKSUbuntu-1804-2020.03.05` |
Virtual node version |
`kubernetes.azure.com/network-name` |
<nodepool vnet name> | `vnetName` |
Virtual node virtual network |
`kubernetes.azure.com/network-subnet` |
<nodepool subnet name> | `subnetName` |
Virtual node subnet name |
`kubernetes.azure.com/ppg` |
<nodepool ppg name> | `ppgName` |
N/A |
`kubernetes.azure.com/encrypted-set` |
<nodepool encrypted-set name> | `encrypted-set-name` |
N/A |
`kubernetes.azure.com/accelerator` |
<accelerator> | `nvidia` |
N/A |
`kubernetes.azure.com/fips_enabled` |
<is FIPS enabled?> | `true` |
N/A |
`kubernetes.azure.com/os-sku` |
<os/sku> |
|

`kubernetes.azure.com/os-sku-effective`

`Ubuntu2204`

or similar (never Ubuntu, always has the version specified)`kubernetes.azure.com/os-sku-requested`

`Ubuntu`

, `Ubuntu2204`

, or similar (exactly matches requested sku from API)`kubernetes.azure.com/sku-cpu`

`4`

`kubernetes.azure.com/sku-memory`

`16`

`kubernetes.azure.com/nodepool-type`

`VirtualMachineScaleSets`

*Same*is included in places where the expected values for the labels don't differ between a standard node pool and a virtual node pool. As virtual node pods don't expose any underlying virtual machine (VM), the VM SKU values are replaced with the SKU*Virtual*.*Virtual node version*refers to the current version of the[virtual Kubelet-ACI connector release](https://github.com/virtual-kubelet/azure-aci/releases).*Virtual node subnet name*is the name of the subnet where virtual node pods are deployed into Azure Container Instance (ACI).*Virtual node virtual network*is the name of the virtual network, which contains the subnet where virtual node pods are deployed on ACI.*Node Auto Provisioning (Karpenter)*nodes have additional labels corresponding to the supported[selectors](/en-us/azure/aks/node-auto-provisioning-node-pools#well-known-labels-and-sku-selectors).`kubernetes.azure.com/network-name`

and`kubernetes.azure.com/network-subnet`

will be truncated if the underlying resource names are greater than 64 characters long.

### Reserved prefixes

The following prefixes are AKS reserved prefixes and can't be used for any node:

- kubernetes.azure.com/
- kubernetes.io/

For more information on reserved prefixes, see [Kubernetes well-known labels, annotations, and taints](https://kubernetes.io/docs/reference/labels-annotations-taints/).

### Deprecated labels

The following labels are planned for deprecation with the release of [Kubernetes v1.24](supported-kubernetes-versions#aks-kubernetes-release-calendar). You should change any label references to the recommended substitute.

| Label | Recommended substitute | Maintainer |
|---|---|---|
| failure-domain.beta.kubernetes.io/region | topology.kubernetes.io/region |
|

[Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)[Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)[Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)[Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)*Newly deprecated. For more information, see the [Release Notes](https://github.com/Azure/AKS/releases).

## Next steps

Learn more about Kubernetes labels in the [Kubernetes labels documentation](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-deploy-egress -->

# Deploy egress gateways for Istio service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to deploy egress gateways for the Istio service mesh add-on for Azure Kubernetes Service (AKS) cluster.

## Overview

The Istio egress gateway can serve as a centralized point to monitor and restrict outbound traffic from applications in the mesh. With the Istio add-on, you can deploy multiple egress gateways across different namespaces, allowing you to set up an egress gateway topology of your choice: egress gateways per-cluster, per-namespace, per-workload, etc. While AKS manages the provisioning and lifecycle of the Istio add-on egress gateways, you must create Istio custom resources to route traffic from applications in the mesh through the egress gateway and apply policies and telemetry collection.

The Istio add-on egress gateway also builds on top of and requires the [Static Egress Gateway](configure-static-egress-gateway) feature, which assigns a fixed source IP address prefix to the Istio egress Pods. You can use this predicable egress IP range for firewall rules and other outbound traffic filtering mechanisms. By using Istio egress gateway on top of Static Egress Gateway, you can apply Istio L7, identity-based policies, and IP-based restrictions for defense-in-depth egress traffic control. Additionally, directing outbound traffic through the Istio egress gateway allows multiple workloads to route traffic via the Static Egress Gateway node pools without modifying those application pods/deployments directly.

## Limitations and requirements

- You can enable a maximum of
`500`

Istio add-on egress gateways per cluster. - Istio add-on egress gateway names must be unique per namespace.
- Istio add-on egress gateway names must be between
`1-53`

characters, must only consist of lowercase alphanumerical characters, '-' and '.,' and must start and end with an alphanumerical character. Names should also be a valid Domain Name System (DNS) name. The regex used for name validation is`^[a-z0-9]([-a-z0-9]*[a-z0-9])?(\.[a-z0-9]([-a-z0-9]*[a-z0-9])?)*$`

. - Using the
[Kubernetes Gateway API](istio-gateway-api)for egress traffic management with the Istio add-on is only supported for the[manual deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#manual-deployment). - Because Static Egress Gateway is currently not supported on
[Azure CNI Pod Subnet clusters](concepts-network-azure-cni-pod-subnet), the Istio add-on egress gateway isn't supported on Pod Subnet clusters either.

## Prerequisites

### Enable Istio add-on

This guide assumes you followed the [documentation](istio-deploy-addon) to enable the Istio add-on on an AKS cluster.

### Update Azure CLI version

You must use `azure-cli`

version `2.80.0`

or higher. Run `az --version`

to find your `azure-cli`

version, and run `az upgrade`

to upgrade.

### Enable and configure Static Egress Gateway

Follow the instructions in the [Static Egress Gateway documentation](configure-static-egress-gateway) to enable Static Egress Gateway on your cluster, create a node pool of mode `gateway`

, and create a `StaticGatewayConfiguration`

resource.

## Enable an Istio egress gateway

Note

The Istio add-on egress gateway pods don't get scheduled onto the `gateway`

node pool. The `gateway`

node pool is only used to route egress traffic and doesn't serve general-purpose workloads. If you need the egress gateway pods scheduled onto particular nodes, you can use [AKS system nodes](/en-us/azure/aks/use-system-pools) or the `azureservicemesh/istio.replica.preferred`

node label. The pods have node affinities with a weighted preference of `100`

for AKS system nodes (labeled `kubernetes.azure.com/mode: system`

), and a weighted preference of `50`

for nodes labeled `azureservicemesh/istio.replica.preferred: true`

.

Use `az aks mesh enable-egress-gateway`

to enable an Istio egress gateway on your AKS cluster. You must specify a name for the Istio egress gateway and the name of the `StaticGatewayConfiguration`

that you created in the [prerequisites](#prerequisites) step. You can also specify a namespace to deploy the Istio egress gateway in, which must be the same namespace that the `StaticGatewayConfiguration`

was created in. If you don't specify a namespace, the egress gateway gets provisioned in the `aks-istio-egress`

namespace.

As a best-practice, you should wait until the `StaticGatewayConfiguration`

is assigned an `egressIpPrefix`

before enabling the Istio egress gateway using that gateway configuration.

```
az aks mesh enable-egress-gateway --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --istio-egressgateway-name $ISTIO_EGRESS_NAME --istio-egressgateway-namespace $ISTIO_EGRESS_NAMESPACE --gateway-configuration-name $ISTIO_SGC_NAME
```


Verify that the service gets created for the egress gateway.

```
kubectl get svc $ISTIO_EGRESS_NAME -n $ISTIO_EGRESS_NAMESPACE
```


You should see a `ClusterIP`

service for the egress gateway:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
asm-egress-test ClusterIP 10.0.128.17 <none> 15021/TCP,80/TCP,443/TCP 6d4h
```


You can also verify that a deployment gets created for the Istio egress gateway and that the egress gateway pods have the `kubernetes.azure.com/static-gateway-configuration`

annotation set to the `gatewayConfigurationName`

.

```
ASM_REVISION=$(az aks show -g $RESOURCE_GROUP -n $CLUSTER_NAME | jq '.serviceMeshProfile.istio.revisions[0]' | sed 's/"//g')
kubectl get deployment $ISTIO_EGRESS_NAME-$ASM_REVISION -n $ISTIO_EGRESS_NAMESPACE -o jsonpath={.spec.template.metadata.annotations."kubernetes\.azure\.com\/static-gateway-configuration"}
```


You can run the `az aks mesh enable-egress-gateway`

command again to create another Istio egress gateway.

Note

When you perform a [minor revision upgrade](istio-upgrade#minor-revision-upgrades-with-ingress-and-egress-gateways) of the Istio add-on, another deployment for each egress gateway gets created for the new control plane revision.

## Route traffic through the Istio egress gateway

### Set `outboundTrafficPolicy.mode`


By default, the Istio `outboundTrafficPolicy.mode`

is set to `ALLOW_ANY`

, meaning that Envoy passes through requests for unknown services. As a security best-practice, you should set the Istio `outboundTrafficPolicy.mode`

to `REGISTRY_ONLY`

so that the Istio proxy blocks requests to services that weren't added to Istio's Service Registry. You can add hosts outside of the cluster to Istio's service registry with a `ServiceEntry`

.

You can configure the `outboundTrafficPolicy.mode`

on a mesh-wide level using the Istio add-on [shared MeshConfig](istio-meshconfig), or use the [Sidecar Custom Resource](https://istio.io/latest/docs/reference/config/networking/sidecar/#OutboundTrafficPolicy) to target specific namespaces or workloads.

```
apiVersion: v1
kind: ConfigMap
metadata:
name: istio-shared-configmap-asm-1-27
namespace: aks-istio-system
data:
mesh: |-
outboundTrafficPolicy:
mode: REGISTRY_ONLY
```


### Deploy sample application

In this example, we deploy the `curl`

application in the same namespace as the Istio add-on egress gateway. Remember to label the `ISTIO_EGRESS_NAMESPACE`

with the `istio.io/rev`

label so that the deployed application pod gets injected with a sidecar:

```
kubectl label namespace $ISTIO_EGRESS_NAMESPACE istio.io/rev=$ASM_REVISION
```


Then, deploy the sample application:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.27/samples/curl/curl.yaml -n $ISTIO_EGRESS_NAMESPACE
```


You should see the `curl`

pod running with an injected sidecar container:

```
NAME READY STATUS RESTARTS AGE
curl-5b549b49b8-bcgts 2/2 Running 0 13s
```


Try sending a request from `curl`

directly to `edition.cnn.com`

:

```
SOURCE_POD=$(kubectl get pod -n $ISTIO_EGRESS_NAMESPACE -l app=curl -o jsonpath={.items..metadata.name})
kubectl exec -n $ISTIO_EGRESS_NAMESPACE "$SOURCE_POD" -c curl -- curl -sSL -o /dev/null -D - http://edition.cnn.com/politics
```


If you set `outboundTrafficPolicy.mode`

to `REGISTRY_ONLY`

, then the `curl`

request should fail because you didn't create a `ServiceEntry`

for `edition.cnn.com`

. If `outboundTrafficPolicy.mode`

is `ALLOW_ANY`

, then the request should succeed.

To actually route requests to `edition.cnn.com`

from the `curl`

pod to the Istio add-on egress gateway, you need to create a `ServiceEntry`

and configure other Istio custom resources. Follow instructions one of the subsequent sections to configure an [HTTP Egress Gateway](#configure-an-http-istio-egress-gateway), [HTTPS Egress Gateway](#configure-an-https-istio-egress-gateway), or an [Egress Gateway that originates a Transport Layer Security (TLS) connection](#configure-an-istio-egress-gateway-to-perform-tls-origination).

Before starting any of the following scenarios, set these environment variables:

```
ISTIO_EGRESS_DEPLOYMENT=$ISTIO_EGRESS_NAME-$ASM_REVISION
EGRESS_GTW_SELECTOR=$(kubectl get deployment $ISTIO_EGRESS_DEPLOYMENT -n $ISTIO_EGRESS_NAMESPACE -o jsonpath={.metadata.labels.istio})
```


You can also [enable Envoy access logging](https://istio.io/latest/docs/tasks/observability/logs/access-log/) either through the [MeshConfig](istio-meshconfig) or [Telemetry API](istio-telemetry). Once you have access logging enabled, you can verify that traffic is flowing through the egress gateway by inspecting the `istio-proxy`

container logs:

```
kubectl logs -l istio=$EGRESS_GTW_SELECTOR -n $ISTIO_EGRESS_NAMESPACE
```


### Configure an HTTP Istio egress gateway

- Create a
`ServiceEntry`

for`edition.cnn.com`

:

```
kubectl apply -n $ISTIO_EGRESS_NAMESPACE -f - <<EOF
apiVersion: networking.istio.io/v1
kind: ServiceEntry
metadata:
name: cnn
spec:
hosts:
- edition.cnn.com
ports:
- number: 80
name: http-port
protocol: HTTP
- number: 443
name: https
protocol: HTTPS
resolution: DNS
EOF
```


- Create the
`Gateway`

,`VirtualService`

, and`DestinationRule`

to route HTTP traffic from the`curl`

application to`edition.cnn.com`

through the egress gateway. Be sure to set the gateway selector and service Fully Qualified Domain Name (FQDN) accordingly based on the`istio`

label selector in the egress gateway deployment.

```
kubectl apply -n $ISTIO_EGRESS_NAMESPACE -f - <<EOF
apiVersion: networking.istio.io/v1
kind: Gateway
metadata:
name: istio-egressgateway
spec:
selector:
istio: $EGRESS_GTW_SELECTOR
servers:
- port:
number: 80
name: http
protocol: HTTP
hosts:
- edition.cnn.com
---
apiVersion: networking.istio.io/v1
kind: DestinationRule
metadata:
name: egressgateway-for-cnn
spec:
host: $ISTIO_EGRESS_NAME.$ISTIO_EGRESS_NAMESPACE.svc.cluster.local
subsets:
- name: cnn
---
apiVersion: networking.istio.io/v1
kind: VirtualService
metadata:
name: direct-cnn-through-egress-gateway
spec:
hosts:
- edition.cnn.com
gateways:
- istio-egressgateway
- mesh
http:
- match:
- gateways:
- mesh
port: 80
route:
- destination:
host: $ISTIO_EGRESS_NAME.$ISTIO_EGRESS_NAMESPACE.svc.cluster.local
subset: cnn
port:
number: 80
weight: 100
- match:
- gateways:
- istio-egressgateway
port: 80
route:
- destination:
host: edition.cnn.com
port:
number: 80
weight: 100
EOF
```


- Try sending an HTTP request from the
`curl`

pod to`edition.cnn.com`

:

```
kubectl exec -n $ISTIO_EGRESS_NAMESPACE "$SOURCE_POD" -c curl -- curl -sSL -o /dev/null -D - http://edition.cnn.com/politics
```


You should see an `HTTP/2 200`

response.

- Clean up resources

```
kubectl delete serviceentry cnn -n $ISTIO_EGRESS_NAMESPACE
kubectl delete gateway istio-egressgateway -n $ISTIO_EGRESS_NAMESPACE
kubectl delete virtualservice direct-cnn-through-egress-gateway -n $ISTIO_EGRESS_NAMESPACE
kubectl delete destinationrule egressgateway-for-cnn -n $ISTIO_EGRESS_NAMESPACE
```


### Configure an HTTPS Istio egress gateway

- Create an HTTPS
`ServiceEntry`

for`edition.cnn.com`

:

```
kubectl apply -n $ISTIO_EGRESS_NAMESPACE -f - <<EOF
apiVersion: networking.istio.io/v1
kind: ServiceEntry
metadata:
name: cnn
spec:
hosts:
- edition.cnn.com
ports:
- number: 443
name: tls
protocol: TLS
resolution: DNS
EOF
```


- Create the
`Gateway`

,`VirtualService`

, and`DestinationRule`

to route HTTP traffic from the`curl`

application to`edition.cnn.com`

through the egress gateway. Be sure to set the gateway selector and service FQDN accordingly based on the`istio`

label selector in the egress gateway deployment.

```
kubectl apply -n $ISTIO_EGRESS_NAMESPACE -f - <<EOF
apiVersion: networking.istio.io/v1
kind: Gateway
metadata:
name: istio-egressgateway
spec:
selector:
istio: $EGRESS_GTW_SELECTOR
servers:
- port:
number: 443
name: tls
protocol: TLS
hosts:
- edition.cnn.com
tls:
mode: PASSTHROUGH
---
apiVersion: networking.istio.io/v1
kind: DestinationRule
metadata:
name: egressgateway-for-cnn
spec:
host: $ISTIO_EGRESS_NAME.$ISTIO_EGRESS_NAMESPACE.svc.cluster.local
subsets:
- name: cnn
---
apiVersion: networking.istio.io/v1
kind: VirtualService
metadata:
name: direct-cnn-through-egress-gateway
spec:
hosts:
- edition.cnn.com
gateways:
- mesh
- istio-egressgateway
tls:
- match:
- gateways:
- mesh
port: 443
sniHosts:
- edition.cnn.com
route:
- destination:
host: $ISTIO_EGRESS_NAME.$ISTIO_EGRESS_NAMESPACE.svc.cluster.local
subset: cnn
port:
number: 443
- match:
- gateways:
- istio-egressgateway
port: 443
sniHosts:
- edition.cnn.com
route:
- destination:
host: edition.cnn.com
port:
number: 443
weight: 100
EOF
```


- Try sending an HTTPS request from
`curl`

to`edition.cnn.com`

:

```
kubectl exec "$SOURCE_POD" -n $ISTIO_EGRESS_NAMESPACE -c curl -- curl -sSL -o /dev/null -D - https://edition.cnn.com/politics
```


You should see an `HTTP/2 200`

response.

- Clean up resources

```
kubectl delete serviceentry cnn -n $ISTIO_EGRESS_NAMESPACE
kubectl delete gateway istio-egressgateway -n $ISTIO_EGRESS_NAMESPACE
kubectl delete virtualservice direct-cnn-through-egress-gateway -n $ISTIO_EGRESS_NAMESPACE
kubectl delete destinationrule egressgateway-for-cnn -n $ISTIO_EGRESS_NAMESPACE
```


### Configure an Istio egress gateway to perform TLS Origination

- Create a
`ServiceEntry`

for`edition.cnn.com`

:

```
kubectl apply -n $ISTIO_EGRESS_NAMESPACE -f - <<EOF
apiVersion: networking.istio.io/v1
kind: ServiceEntry
metadata:
name: cnn
spec:
hosts:
- edition.cnn.com
ports:
- number: 80
name: http
protocol: HTTP
- number: 443
name: https
protocol: HTTPS
resolution: DNS
EOF
```


- Create the
`Gateway`

,`VirtualService`

, and`DestinationRule`

to route HTTP traffic from the`curl`

application to`edition.cnn.com`

through the egress gateway, and to perform TLS origination at the egress gateway. Be sure to set the gateway selector and service FQDN accordingly based on the`istio`

label selector in the egress gateway deployment.

```
kubectl apply -n $ISTIO_EGRESS_NAMESPACE -f - <<EOF
apiVersion: networking.istio.io/v1
kind: Gateway
metadata:
name: istio-egressgateway
spec:
selector:
istio: $EGRESS_GTW_SELECTOR
servers:
- port:
number: 80
name: https-port-for-tls-origination
protocol: HTTPS
hosts:
- edition.cnn.com
tls:
mode: ISTIO_MUTUAL
---
apiVersion: networking.istio.io/v1
kind: DestinationRule
metadata:
name: egressgateway-for-cnn
spec:
host: $ISTIO_EGRESS_NAME.$ISTIO_EGRESS_NAMESPACE.svc.cluster.local
subsets:
- name: cnn
trafficPolicy:
loadBalancer:
simple: ROUND_ROBIN
portLevelSettings:
- port:
number: 80
tls:
mode: ISTIO_MUTUAL
sni: edition.cnn.com
---
apiVersion: networking.istio.io/v1
kind: VirtualService
metadata:
name: direct-cnn-through-egress-gateway
spec:
hosts:
- edition.cnn.com
gateways:
- istio-egressgateway
- mesh
http:
- match:
- gateways:
- mesh
port: 80
route:
- destination:
host: $ISTIO_EGRESS_NAME.$ISTIO_EGRESS_NAMESPACE.svc.cluster.local
subset: cnn
port:
number: 80
weight: 100
- match:
- gateways:
- istio-egressgateway
port: 80
route:
- destination:
host: edition.cnn.com
port:
number: 443
weight: 100
---
apiVersion: networking.istio.io/v1
kind: DestinationRule
metadata:
name: originate-tls-for-edition-cnn-com
spec:
host: edition.cnn.com
trafficPolicy:
loadBalancer:
simple: ROUND_ROBIN
portLevelSettings:
- port:
number: 443
tls:
mode: SIMPLE # initiates HTTPS for connections to edition.cnn.com
EOF
```


- Try sending a request form
`curl`

to`edition.cnn.com`

with the egress gateway performing TLS origination;

```
kubectl exec "${SOURCE_POD}" -n $ISTIO_EGRESS_NAMESPACE -c curl -- curl -sSL -o /dev/null -D - http://edition.cnn.com/politics
```


You should see a `200`

status response.

- Clean up resources

```
kubectl delete serviceentry cnn -n $ISTIO_EGRESS_NAMESPACE
kubectl delete gateway istio-egressgateway -n $ISTIO_EGRESS_NAMESPACE
kubectl delete virtualservice direct-cnn-through-egress-gateway -n $ISTIO_EGRESS_NAMESPACE
kubectl delete destinationrule originate-tls-for-edition-cnn-com -n $ISTIO_EGRESS_NAMESPACE
kubectl delete destinationrule egressgateway-for-cnn -n $ISTIO_EGRESS_NAMESPACE
```


## Disable the Istio egress gateway

Run the `az aks mesh disable-egress-gateway`

command to disable the Istio add-on egress gateway that you created:

```
az aks mesh disable-egress-gateway --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --istio-egressgateway-name $ISTIO_EGRESS_NAME --istio-egressgateway-namespace $ISTIO_EGRESS_NAMESPACE
```


Once you disable the Istio egress gateway, you should be able to delete the `StaticGatewayConfiguration`

, namespace, and `gateway`

node pool that the egress gateway was using if no other Istio egress gateway is using them.

## Next steps

[Configure ingress for Istio service mesh add-on with the Kubernetes Gateway API](istio-gateway-api)[Deploy external or internal ingresses for Istio service mesh add-on](istio-deploy-ingress)[Configure egress gateway Horizontal Pod Autoscaler (HPA)](istio-scale#scaling)

Note

If there are any issues encountered with deploying the Istio egress gateway or configuring egress traffic routing, refer to [article on troubleshooting Istio add-on egress gateways](/en-us/troubleshoot/azure/azure-kubernetes/extensions/istio-add-on-egress-gateway)

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-meshconfig -->

# Configure Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Open-source Istio uses [MeshConfig](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/) to define mesh-wide settings for the Istio service mesh. Istio-based service mesh add-on for AKS builds on top of MeshConfig and classifies different properties as supported, allowed, and blocked.

This article walks through how to configure Istio-based service mesh add-on for Azure Kubernetes Service and the support policy applicable for such configuration.

## Prerequisites

This guide assumes you followed the [documentation](istio-deploy-addon) to enable the Istio add-on on an AKS cluster.

## Set up configuration on cluster

Find out which revision of Istio is deployed on the cluster:

`export RANDOM_SUFFIX=$(head -c 3 /dev/urandom | xxd -p) export CLUSTER="my-aks-cluster" export RESOURCE_GROUP="my-aks-rg$RANDOM_SUFFIX" az aks show --name $CLUSTER --resource-group $RESOURCE_GROUP --query 'serviceMeshProfile' --output json`

Results:

`{ "istio": { "certificateAuthority": null, "components": { "egressGateways": null, "ingressGateways": null }, "revisions": [ "asm-1-24" ] }, "mode": "Istio" }`

This command shows the Istio service mesh profile, including the revision(s) currently deployed on your AKS cluster.

Create a ConfigMap with the name

`istio-shared-configmap-<asm-revision>`

in the`aks-istio-system`

namespace. For example, if your cluster is running asm-1-24 revision of mesh, then the ConfigMap needs to be named as`istio-shared-configmap-asm-1-24`

. Mesh configuration has to be provided within the data section under mesh.Example:

`cat <<EOF > istio-shared-configmap-asm-1-24.yaml apiVersion: v1 kind: ConfigMap metadata: name: istio-shared-configmap-asm-1-24 namespace: aks-istio-system data: mesh: |- accessLogFile: /dev/stdout defaultConfig: holdApplicationUntilProxyStarts: true EOF kubectl apply -f istio-shared-configmap-asm-1-24.yaml`

Results:

`configmap/istio-shared-configmap-asm-1-24 created`

The values under

`defaultConfig`

are mesh-wide settings applied for Envoy sidecar proxy.

Caution

A default ConfigMap (for example, `istio-asm-1-24`

for revision asm-1-24) is created in `aks-istio-system`

namespace on the cluster when the Istio add-on is enabled. However, this default ConfigMap gets reconciled by the managed Istio add-on and thus users should NOT directly edit this ConfigMap. Instead users should create a revision specific Istio shared ConfigMap (for example `istio-shared-configmap-asm-1-24`

for revision asm-1-24) in the aks-istio-system namespace, and then the Istio control plane will merge this with the default ConfigMap, with the default settings taking precedence.

### Mesh configuration and upgrades

When you're performing [canary upgrade for Istio](istio-upgrade), you need to create a separate ConfigMap for the new revision in the `aks-istio-system`

namespace **before initiating the canary upgrade**. This way the configuration is available when the new revision's control plane is deployed on cluster. For example, if you're upgrading the mesh from asm-1-24 to asm-1-25, you need to copy changes over from `istio-shared-configmap-asm-1-24`

to create a new ConfigMap called `istio-shared-configmap-asm-1-25`

in the `aks-istio-system`

namespace.

After the upgrade is completed or rolled back, you can delete the ConfigMap of the revision that was removed from the cluster.

## Allowed, supported, and blocked MeshConfig values

Fields in `MeshConfig`

are classified as `allowed`

, `supported`

, or `blocked`

. To learn more about these categories, see the [support policy](istio-support-policy#allowed-supported-and-blocked-customizations) for Istio add-on features and configuration options.

Mesh configuration and the list of allowed/supported fields are revision specific to account for fields being added/removed across revisions. The full list of allowed fields and the supported/unsupported ones within the allowed list is provided in the below table. When new mesh revision is made available, any changes to allowed and supported classification of the fields is noted in this table.

### MeshConfig

Fields present in [open source MeshConfig reference documentation](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/) that are not covered in the following table are blocked. For example, `configSources`

is blocked.

Field |
Supported/Allowed |
Notes |
|---|---|---|
| proxyListenPort | Allowed | - |
| proxyInboundListenPort | Allowed | - |
| proxyHttpPort | Allowed | - |
| connectTimeout | Allowed | Configurable in
|

[DestinationRule](https://istio.io/latest/docs/reference/config/networking/destination-rule/#ConnectionPoolSettings-TCPSettings)[ProxyConfig](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/#ProxyConfig)[Sidecar CR](https://istio.io/latest/docs/reference/config/networking/sidecar/#OutboundTrafficPolicy)[Azure Monitor Container Insights on AKS](/en-us/azure/azure-monitor/containers/container-insights-overview). It is encouraged to configure access logging via the[Telemetry API](istio-telemetry).[Azure Monitor Container Insights on AKS](/en-us/azure/azure-monitor/containers/container-insights-overview)[Azure Monitor Container Insights on AKS](/en-us/azure/azure-monitor/containers/container-insights-overview)[Telemetry API](istio-telemetry).[Azure Monitor Container Insights on AKS](/en-us/azure/azure-monitor/containers/container-insights-overview)[Azure Monitor Container Insights on AKS](/en-us/azure/azure-monitor/containers/container-insights-overview)[DestinationRule](https://istio.io/latest/docs/reference/config/networking/destination-rule/#ClientTLSSettings)[ServiceEntry](https://istio.io/latest/docs/reference/config/networking/service-entry/#ServiceEntry)[VirtualService](https://istio.io/latest/docs/reference/config/networking/virtual-service/#VirtualService)[DestinationRule](https://istio.io/latest/docs/reference/config/networking/destination-rule/#DestinationRule)[DestinationRule](https://istio.io/latest/docs/reference/config/networking/destination-rule/#LoadBalancerSettings)[DestinationRule](https://istio.io/latest/docs/reference/config/networking/destination-rule/#ConnectionPoolSettings-HTTPSettings)[VirtualService](https://istio.io/latest/docs/reference/config/networking/virtual-service/#HTTPRetry)### ProxyConfig (meshConfig.defaultConfig)

Fields present in [open source MeshConfig reference documentation](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/#ProxyConfig) that are not covered in the following table are blocked.

Field |
Supported/Allowed |
Notes |
|---|---|---|
| tracingServiceName | Allowed | It is encouraged to configure tracing via the
|

[Telemetry API](istio-telemetry).[Telemetry API](istio-telemetry).[Telemetry API](istio-telemetry).Caution

**Support scope of configurations:** Mesh configuration allows for extension providers such as self-managed instances of Zipkin or Apache Skywalking to be configured with the Istio add-on. However, these extension providers are outside the support scope of the Istio add-on. Any issues associated with extension tools are outside the support boundary of the Istio add-on.

## Common errors and troubleshooting tips

- Ensure that the MeshConfig is indented with spaces instead of tabs.
- Ensure that you're only editing the revision specific shared ConfigMap (for example
`istio-shared-configmap-asm-1-24`

) and not trying to edit the default ConfigMap (for example`istio-asm-1-24`

). - The ConfigMap must follow the name
`istio-shared-configmap-<asm-revision>`

and be in the`aks-istio-system`

namespace. - Ensure that all MeshConfig fields are spelled correctly. If they're unrecognized or if they aren't part of the allowed list, admission control denies such configurations.
- When performing canary upgrades,
[check your revision specific ConfigMaps](#mesh-configuration-and-upgrades)to ensure configurations exist for the revisions deployed on your cluster. - Certain
`MeshConfig`

options such as accessLogging may increase Envoy's resource consumption, and disabling some of these settings may mitigate Istio data plane resource utilization. It's also advisable to use the`discoverySelectors`

field in the MeshConfig to help alleviate memory consumption for Istiod and Envoy. - If the
`concurrency`

field in the MeshConfig is misconfigured and set to zero, it causes Envoy to use up all CPU cores. Instead if this field is unset, number of worker threads to run is automatically determined based on CPU requests/limits. [Pod and sidecar race conditions](https://istio.io/latest/docs/ops/common-problems/injection/#pod-or-containers-start-with-network-issues-if-istio-proxy-is-not-ready)in which the application starts before Envoy can be mitigated using the`holdApplicationUntilProxyStarts`

field in the MeshConfig.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/custom-certificate-authority -->

# Use custom certificate authorities (CAs) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Custom Certificate Authority (CA) allows you to add up to 10 base64-encoded certificates to your node's trust store. This feature is often needed when certificate authorities (CAs) are required to be present on the node, like when connecting to a private registry.

This article shows you how to create custom CAs and apply them to your AKS clusters.

Note

The Custom CA feature adds your custom certificates to the trust store of the AKS node. Certificates added with this feature aren't available to containers running in pods. If you need the certificates inside containers, you need to add them separately by adding them to the image used by your pods or at runtime via scripting and a secret.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/free). - Azure CLI version 2.72.0 or later installed and configured. To find your CLI version, run the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - A base64 encoded certificate string or a text file with certificate.

## Limitations

- Windows node pools aren't supported.
- Installing different CAs in the same cluster isn't supported.

## Create a certificate file

Create a text file containing up to 10 blank line separated certificates. When you pass this file to your cluster, the certificates are installed in the trust stores of the AKS node.

Example text file:

`-----BEGIN CERTIFICATE----- cert1 -----END CERTIFICATE----- -----BEGIN CERTIFICATE----- cert2 -----END CERTIFICATE-----`


**Before proceeding to the next step, make sure that there are no blank spaces in your text file to avoid errors**.

## Pass custom CAs to your AKS cluster

Pass certificates to your cluster using the

or`az aks create`

command with`az aks update`

`--custom-ca-trust-certificates`

set to the name of your certificate file.`# Create a new cluster az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --node-count 2 \ --custom-ca-trust-certificates <path-to-certificate-file> \ --generate-ssh-keys # Update an existing cluster az aks update \ --resource-group <resource-group-name> \ --name <cluster-name> \ --custom-ca-trust-certificates <path-to-certificate-file>`

Note

This operation triggers a model update to ensure all existing nodes have the same CAs installed for correct provisioning. AKS creates new nodes, drains existing nodes, deletes existing nodes, and replaces them with nodes that have the new set of CAs installed.


## Verify CAs are installed

Verify the CAs are installed using the

command.`az aks show`

`az aks show --resource-group <resource-group-name> --name <cluster-name> | grep securityProfile -A 4`

In the output, the

`securityProfile`

section should include your custom CA certificates. For example:`"securityProfile": { "azureKeyVaultKms": null, "customCaTrustCertificates": [ "values"`


## Resolve custom CA formatting errors

Adding certificates to a cluster can result in an error if the file with the certificates isn't formatted properly. You might see an error similar to the following example:

```
failed to decode one of SecurityProfile.CustomCATrustCertificates to PEM after base64 decoding
```


If you encounter this error, you should check that your input file has no extra new lines, white spaces, or data other than correctly formatted certificates as shown in the example file.

## Resolve custom CA X.509 Certificate Signed by Unknown Authority errors

AKS requires certificates passed to be properly formatted and base64 encoded. Make sure the CAs you passed are properly base64 encoded and that files with CAs don't have CRLF line breaks.

## Restart containerd to pick up new certificates

If containerd doesn't pick up new certificates, run the `systemctl restart containerd`

command from the node's shell. Once containerd restarts, the container runtime should pick up the new certificates.

## Related content

For more information on AKS security best practices, see [Best practices for cluster security and upgrades in Azure Kubernetes Service (AKS)](operator-best-practices-cluster-security).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-vs-linux-containers -->

# Windows container considerations with Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create deployments that use Windows Server containers on Azure Kubernetes Service (AKS), there are a few differences relative to Linux deployments you should keep in mind. For a detailed comparison of the differences between Windows and Linux in upstream Kubernetes, see [Windows containers in Kubernetes](https://kubernetes.io/docs/concepts/windows/intro/).

Some of the major differences include:

**Identity**: Windows Server uses a larger binary security identifier (SID) that's stored in the Windows Security Access Manager (SAM) database. This database isn't shared between the host and containers or between containers.**File permissions**: Windows Server uses an access control list based on SIDs rather than a bitmask of permissions and UID+GID.**File paths**: The convention on Windows Server is to use \ instead of /. In pod specs that mount volumes, specify the path correctly for Windows Server containers. For example, rather than a mount point of*/mnt/volume*in a Linux container, specify a drive letter and location such as*/K/Volume*to mount as the*K:*drive.

Important

Starting on March 01, 2026, Azure Kubernetes Service (AKS) no longer supports Windows Server 2019 node pools. Node pools running Kubernetes version 1.33+ can't use Windows Server 2019. Starting on April 01, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4091) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=aks-will-stop-support-for-windows-server-2019-on-march-1-2026). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on March 15, 2027, Azure Kubernetes Service (AKS) no longer supports Windows Server 2022 node pools. Node pools running Kubernetes version 1.36+ can't use Windows Server 2022. Starting on April 01, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4168) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=ws2022-retirement-aks). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

This article covers important considerations to keep in mind when using Windows containers instead of Linux containers in Kubernetes. For an in-depth comparison of Windows and Linux containers, see [Comparison with Linux](https://kubernetes.io/docs/concepts/windows/intro/#compatibility-linux-similarities).

## Considerations

| Feature | Windows considerations |
|---|---|
|

*must*be Linux.• The maximum number of nodes per cluster is 5000.

• The Windows Server node pool name has a limit of six characters.

[Privileged containers](use-windows-hpc#limitations)**HostProcess Containers (HPC) containers**.[HPC containers](use-windows-hpc#limitations)[Create a Windows HostProcess pod](https://kubernetes.io/docs/tasks/configure-pod-container/create-hostprocess-pod/).[Azure Network Policy Manager (Azure)](use-network-policies#overview-of-network-policy)• Named ports

• SCTP protocol

• Negative match labels or namespace selectors (all labels except "debug=true")

• "except" CIDR blocks (a CIDR with exceptions)

• Windows Server 2019

[Node upgrade](manage-node-pools#upgrade-a-single-node-pool)[node image upgrade](node-image-upgrade). These upgrades deploy new nodes with the latest Window Server 2019 and Windows Server 2022 base node image and security patches.[AKS Image Cleaner](image-cleaner#limitations)[BYOCNI](use-byo-cni)[Open Service Mesh](open-service-mesh-about)[GPU](use-windows-gpu)[Multi-instance GPU](gpu-multi-instance)[Generation 2 VMs](generation-2-vms)[Custom node config](custom-node-configuration)•

[kubelet](custom-node-configuration#kubelet-configuration): Supported.• OS config: Not supported.

## Next steps

For more information on Windows containers, see the [Windows Server containers FAQ](windows-faq).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices-performance-scale-large -->

# Best practices for performance and scaling for large workloads in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This article focuses on general best practices for **large workloads**. For best practices specific to **small to medium workloads**, see [Performance and scaling best practices for small to medium workloads in Azure Kubernetes Service (AKS)](best-practices-performance-scale).

As you deploy and maintain clusters in AKS, you can use the following best practices to help you optimize performance and scaling.

Keep in mind that *large* is a relative term. Kubernetes has a multi-dimensional scale envelope, and the scale envelope for your workload depends on the resources you use. For example, a cluster with 100 nodes and thousands of pods or CRDs might be considered large. A 1,000 node cluster with 1,000 pods and various other resources might be considered small from the control plane perspective. The best signal for scale of a Kubernetes control plane is API server HTTP request success rate and latency, as that's a proxy for the amount of load on the control plane.

In this article, you learn about:

- AKS and Kubernetes control plane scalability.
- Kubernetes Client best practices, including backoff, watches, and pagination.
- Azure API and platform throttling limits.
- Feature limitations.
- Networking and node pool scaling best practices.

## AKS and Kubernetes control plane scalability

In AKS, a *cluster* consists of a set of nodes (physical or virtual machines (VMs)) that run Kubernetes agents and are managed by the Kubernetes control plane hosted by AKS. While AKS optimizes the Kubernetes control plane and its components for scalability and performance, it's still bound by the upstream project limits.

Kubernetes has a multi-dimensional scale envelope with each resource type representing a dimension. Not all resources are alike. For example, *watches* are commonly set on secrets, which result in list calls to the kube-apiserver that add cost and a disproportionately higher load on the control plane compared to resources without watches.

The control plane manages all the resource scaling in the cluster, so the more you scale the cluster within a given dimension, the less you can scale within other dimensions. For example, running hundreds of thousands of pods in an AKS cluster impacts how much pod churn rate (pod mutations per second) the control plane can support.

The size of the envelope is proportional to the size of the Kubernetes control plane. AKS supports three control plane tiers as part of the Base SKU: Free, Standard, and Premium tier. For more information, see [Free, Standard, and Premium pricing tiers for AKS cluster management](free-standard-pricing-tiers).

Important

We highly recommend using the Standard or Premium tier for production or at-scale workloads. AKS automatically scales up the Kubernetes control plane to support the following scale limits:

- Up to 5,000 nodes per AKS cluster
- 200,000 pods per AKS cluster (with Azure CNI Overlay)

In most cases, crossing the scale limit threshold results in degraded performance, but doesn't cause the cluster to immediately fail over. To manage load on the Kubernetes control plane, consider scaling in batches of up to 10-20% of the current scale. For example, for a 5,000 node cluster, scale in increments of 500-1,000 nodes. While AKS does autoscale your control plane, it doesn't happen instantaneously.

You can leverage API Priority and Fairness (APF) to throttle specific clients and request types to protect the control plane during high churn and load.

## Kubernetes clients

Kubernetes clients are the applications clients, such as operators or monitoring agents, deployed in the Kubernetes cluster that need to communicate with the kube-api server to perform read or mutate operations. It's important to optimize the behavior of these clients to minimize the load they add to the kube-api server and Kubernetes control plane.

You can analyze API server traffic and client behavior through Kube Audit logs. For more information, see [Troubleshoot the Kubernetes control plane](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-apiserver-etcd).

LIST requests can be expensive. When working with lists that might have more than a few thousand small objects or more than a few hundred large objects, you should consider the following guidelines:

**Consider the number of objects (CRs) you expect to eventually exist**when defining a new resource type (CRD).**The load on etcd and API server primarily relies on the size of the response**. Even if you use a field selector to filter the list and retrieve only a small number of results, these guidelines still apply. The only exception is retrieval of a single object by`metadata.name`

.**Avoid repeated LIST calls if possible**if your code needs to maintain an updated list of objects in memory. Instead, consider using the Informer classes provided in most Kubernetes libraries. Informers automatically combine LIST and WATCH functionalities to efficiently maintain an in-memory collection.**Consider whether you need strong consistency**if Informers don't meet your needs. Do you need to see the most recent data, up to the exact moment in time you issued the query? If not, set`ResourceVersion=0`

. This causes the API server cache to serve your request instead of etcd.**If you can't use Informers or the API server cache, read large lists in chunks**.**Avoid listing more often than needed**. If you can't use Informers, consider how often your application lists the resources. After you read the last object in a large list, don't immediately re-query the same list. You should wait a while instead.**Add approporiate exponential backoffs and retry policies**to prevent clients from overwhelming the API server.**Consider the number of running instances of your client application**. There's a big difference between having a single controller listing objects vs. having pods on each node doing the same thing. If you plan to have multiple instances of your client application periodically listing large numbers of objects, your solution won't scale to large clusters.**Keep the overall Etcd size small**and do not use Etcd as a regular database. Some object size reduction techniques are listed below- To reduce pod specification sizes, move environment variables from pod specifications to ConfigMaps
- Split large secrets or ConfigMaps into smaller, more manageable pieces
- Review and optimize resource specifications in your applications
- Reduce revision count


## Azure API and Platform throttling

The load on a cloud application can vary over time based on factors such as the number of active users or the types of actions that users perform. If the processing requirements of the system exceed the capacity of the available resources, the system can become overloaded and suffer from poor performance and failures.

To handle varying load sizes in a cloud application, you can allow the application to use resources up to a specified limit and then throttle them when the limit is reached. On Azure, throttling happens at two levels. Azure Resource Manager (ARM) throttles requests for the subscription and tenant. If the request is under the throttling limits for the subscription and tenant, ARM routes the request to the resource provider. The resource provider then applies throttling limits tailored to its operations. For more information, see [ARM throttling requests](/en-us/azure/azure-resource-manager/management/request-limits-and-throttling).

### Manage throttling in AKS

Azure API limits are usually defined at a subscription-region combination level. For example, all clients within a subscription in a given region share API limits for a given Azure API, such as Virtual Machine Scale Sets PUT APIs. Every AKS cluster has several AKS-owned clients, such as cloud provider or cluster autoscaler, or customer-owned clients, such as Datadog or self-hosted Prometheus, that call Azure APIs. When running multiple AKS clusters in a subscription within a given region, all the AKS-owned and customer-owned clients within the clusters share a common set of API limits. Therefore, the number of clusters you can deploy in a subscription region is a function of the number of clients deployed, their call patterns, and the overall scale and elasticity of the clusters.

Keeping the above considerations in mind, customers are typically able to deploy between 20-40 small to medium scale clusters per subscription-region. You can maximize your subscription scale using the following best practices:

Always upgrade your Kubernetes clusters to the latest version. Newer versions contain many improvements that address performance and throttling issues. If you're using an upgraded version of Kubernetes and still see throttling due to the actual load or the number of clients in the subscription, you can try the following options:

**Analyze errors using AKS Diagnose and Solve Problems**: You can use[AKS Diagnose and Solve Problems](aks-diagnostics)to analyze errors, identity the root cause, and get resolution recommendations.**Increase the Cluster Autoscaler scan interval**: If the diagnostic reports show that[Cluster Autoscaler throttling has been detected](/en-us/troubleshoot/azure/azure-kubernetes/429-too-many-requests-errors#analyze-and-identify-errors-by-using-aks-diagnose-and-solve-problems), you can[increase the scan interval](cluster-autoscaler#update-the-cluster-autoscaler-settings)to reduce the number of calls to Virtual Machine Scale Sets from the Cluster Autoscaler.**Reconfigure third-party applications to make fewer calls**: If you filter by*user agents*in thediagnostic and see that**View request rate and throttle details**[a third-party application, such as a monitoring application, makes a large number of GET requests](/en-us/troubleshoot/azure/azure-kubernetes/429-too-many-requests-errors#analyze-and-identify-errors-by-using-aks-diagnose-and-solve-problems), you can change the settings of these applications to reduce the frequency of the GET calls. Make sure the application clients use exponential backoff when calling Azure APIs.

**Split your clusters into different subscriptions or regions**: If you have a large number of clusters and node pools that use Virtual Machine Scale Sets, you can split them into different subscriptions or regions within the same subscription. Most Azure API limits are shared at the subscription-region level, so you can move or scale your clusters to different subscriptions or regions to get unblocked on Azure API throttling. This option is especially helpful if you expect your clusters to have high activity. There are no generic guidelines for these limits. If you want specific guidance, you can create a support ticket.

## Monitor AKS Control Plane metrics and logs

Monitoring control plane metrics in large AKS clusters is crucial for ensuring the stability and performance of Kubernetes workloads. These metrics provide visibility into the health and behavior of critical components like the API server, etcd, controller manager, and scheduler. In large-scale environments, where resource contention and high API call volumes are common, monitoring control plane metrics helps identify bottlenecks, detect anomalies, and optimize resource usage. By analyzing these metrics, operators can proactively address issues such as API server latency, high etcd objects, or excessive control plane resource consumption, ensuring efficient cluster operation and minimizing downtime.

Azure Monitor offers comprehensive metrics and logs on the health of the control plane through [Azure Managed Prometheus](monitor-control-plane-metrics#monitor-aks-control-plane-metrics-preview) and [Diagnostic settings](monitor-control-plane-metrics#azure-monitor-resource-logs)

- For list of alerts to configure for health of the control plane, please checkout
[Best practices for AKS control plane monitoring](best-practices-monitoring-proactive#kubernetes-control-plane-alerts) - To get the list of user agents having the highest latency, you can use the Control Plane logs/Diagnostic Settings

## Feature limitations

As you scale your AKS clusters to larger scale points, keep the following feature limitations in mind:

- AKS supports scaling up to 5,000 nodes by default for all Standard Tier / LTS clusters. AKS scales your cluster's control plane at runtime based on cluster size and API server resource utilization. If you can't scale up to the supported limit, enable
[control plane metrics (Preview)](monitor-control-plane-metrics)with the[Azure Monitor managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)to monitor the control plane. To help troubleshoot scaling performance or reliability issues, see the following resources:

Note

During the operation to scale the control plane, you might encounter elevated API server latency or timeouts for up to 15 minutes. If you continue to have problems scaling to the supported limit, open a [support ticket](https://portal.azure.com/#create/Microsoft.Support/Parameters/%7B%0D%0A%09%22subId%22%3A+%22%22%2C%0D%0A%09%22pesId%22%3A+%225a3a423f-8667-9095-1770-0a554a934512%22%2C%0D%0A%09%22supportTopicId%22%3A+%2280ea0df7-5108-8e37-2b0e-9737517f0b96%22%2C%0D%0A%09%22contextInfo%22%3A+%22AksLabelDeprecationMarch22%22%2C%0D%0A%09%22caller%22%3A+%22Microsoft_Azure_ContainerService+%2B+AksLabelDeprecationMarch22%22%2C%0D%0A%09%22severity%22%3A+%223%22%0D%0A%7D).

[Azure Network Policy Manager (Azure npm)](/en-us/azure/virtual-network/kubernetes-network-policies)only supports up to 250 nodes.- Some AKS node metrics, including node disk usage, node CPU/memory usage, and network in/out, won't be accessible in
[azure monitor platform metrics](/en-us/azure/azure-monitor/reference/supported-metrics/microsoft-containerservice-managedclusters-metrics)after the control plane is scaled up. To confirm if your control plane has been scaled up, look for the configmap 'large-cluster-control-plane-scaling-status'

```
kubectl describe configmap large-cluster-control-plane-scaling-status -n kube-system
```


- You can't use the Stop and Start feature with clusters that have more than 100 nodes. For more information, see
[Stop and start an AKS cluster](start-stop-cluster).

## Networking

As you scale your AKS clusters to larger scale points, keep the following networking best practices in mind:

- Use Managed NAT for cluster egress with at least two public IPs on the NAT gateway. For more information, see
[Create a managed NAT gateway for your AKS cluster](nat-gateway). - Use Azure CNI Overlay to scale up to 200,000 pods and 5,000 nodes per cluster. For more information, see
[Configure Azure CNI Overlay networking in AKS](azure-cni-overlay). - If your application needs direct pod-to-pod communication across clusters, use Azure CNI with dynamic IP allocation and scale up to 50,000 application pods per cluster with one routable IP per pod. For more information, see
[Configure Azure CNI networking for dynamic IP allocation in AKS](configure-azure-cni-dynamic-ip-allocation). - When using internal Kubernetes services behind an internal load balancer, we recommend creating an internal load balancer or service below a 750 node scale for optimal scaling performance and load balancer elasticity.
- Azure npm only supports up to 250 nodes. If you want to enforce network policies for larger clusters, consider using
[Azure CNI powered by Cilium](azure-cni-powered-by-cilium), which combines the robust control plane of Azure CNI with the Cilium data plane to provide high performance networking and security.

## Node pool scaling

As you scale your AKS clusters to larger scale points, keep the following node pool scaling best practices in mind:

- For system node pools, use the
*Standard_D16ds_v5*SKU or an equivalent core/memory VM SKU with ephemeral OS disks to provide sufficient compute resources for kube-system pods. - Since AKS has a limit of 1,000 nodes per node pool, we recommend creating at least five user node pools to scale up to 5,000 nodes.
- When running at-scale AKS clusters, use the cluster autoscaler whenever possible to ensure dynamic scaling of node pools based on the demand for compute resources. For more information, see
[Automatically scale an AKS cluster to meet application demands](cluster-autoscaler). - If you're scaling beyond 1,000 nodes and are
*not*using the cluster autoscaler, we recommend scaling in batches of 500-700 nodes at a time. The scaling operations should have a two-minute to five-minute wait time between scale up operations to prevent Azure API throttling. For more information, see[API management: Caching and throttling policies](https://azure.microsoft.com/blog/api-management-advanced-caching-and-throttling-policies/).

## Cluster upgrade considerations and best practices

- When a cluster reaches the 5,000 node limit, cluster upgrades are blocked. This limits prevents an upgrade because there isn't available node capacity to perform rolling updates within the max surge property limit. If you have a cluster at this limit, we recommend
[scaling down the cluster](concepts-scale)under 3,000 nodes before attempting a cluster upgrade. This will provide extra capacity for node churn and minimize load on the control plane. - When upgrading clusters with more than 500 nodes, it is recommended to use a
[max surge configuration](upgrade-aks-cluster#set-max-surge-value)of 10-20% of the node pool's capacity. AKS configures upgrades with a default value of 10% for max surge. You can customize the max surge settings per node pool to enable a trade-off between upgrade speed and workload disruption. When you increase the max surge settings, the upgrade process completes faster, but you might experience disruptions during the upgrade process. For more information, see[Customize node surge upgrade](upgrade-aks-cluster#customize-node-surge-upgrade). - For more cluster upgrade information, see
[Upgrade an AKS cluster](upgrade-cluster).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-network-policies -->

# Secure traffic between pods with network policies in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Starting on **September 30, 2026**, Azure Kubernetes Service (AKS) no longer supports Azure Network Policy Manager (NPM) on **Windows** nodes. This change applies only to customers already onboarded to NPM. **Subscriptions that aren't registered with this feature will no longer be able to onboard**. Existing onboarded customers can continue using NPM until the end-of-support date. To ensure your setup continues to receive support, security updates, and deployment compatibility, explore alternative options like [Network Security Groups (NSGs)](concepts-network) on the node level or open-source tools like [Project Calico](https://www.tigera.io/tigera-products/calico/). For more information on this retirement, see the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500273). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on **September 30, 2028**, Azure Kubernetes Service (AKS) no longer supports Azure Network Policy Manager (NPM) on **Linux** nodes. To avoid service disruptions, you need to [migrate AKS clusters running Linux nodes from NPM to Cilium Network Policy](migrate-from-npm-to-cilium-network-policy) by the end-of-support date. For more information on this retirement, see the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500268). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on **March 31, 2028**, Azure Kubernetes Service (AKS) no longer supports kubenet networking. To avoid service disruptions, [upgrade to Azure Container Networking Interface (CNI) Overlay networking](/en-us/azure/aks/update-azure-cni) before the end-of-support date. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4859) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=485172). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Install a network policy engine and create Kubernetes network policies to control the flow of traffic between pods in AKS clusters.

## Overview of network policy

By default, all pods in an AKS cluster can send and receive traffic without limitations. To improve security, you can define rules that control the flow of traffic.

Network policy is a Kubernetes specification that defines access policies for communication between pods. When you use network policies, you define an ordered set of rules to send and receive traffic. You apply the rules to a collection of pods that match one or more label selectors.

You define the network policy rules as YAML manifests, and you can include them in wider manifests that also create a deployment or service.

## Network policy options in AKS

Azure provides three network policy engines for enforcing network policies:

**Cilium**(for AKS clusters using[Azure CNI Powered by Cilium](azure-cni-powered-by-cilium))**Azure Network Policy Manager (NPM)****Calico**(an open-source network and network security solution founded by[Tigera](https://www.tigera.io/))

We recommend using Cilium. Cilium enforces network policy on the traffic using Linux Berkeley Packet Filter (BPF), which is more efficient than *IPTables*.

To enforce the specified policies, Azure NPM uses *IPTables* for Linux and *Host Network Service (HNS) ACLPolicies* for Windows. Policies are translated into sets of allowed and disallowed IP pairs. These pairs are then programmed as `IPTable`

or `HNS ACLPolicy`

filter rules.

## Differences between network policy engines: Cilium, Azure NPM, and Calico

| Network policy engine | Supported platforms | Supported networking options | Kubernetes specification compliance | Other features | Support |
|---|---|---|---|---|---|
| Cilium | Linux | Azure CNI | Supports all policy types |
|

[Calico Network Policy issue](https://github.com/Azure/AKS/issues/4038).## Azure Network Policy Manager limitations (Linux)

Azure NPM for Linux has the following limitations:

- Scaling beyond
*250 nodes*and*20,000 pods*isn't supported. If you attempt to scale beyond these limits, you might experience*Out of Memory (OOM)*errors. For better scalability and IPv6 support, we recommend using or upgrading to[Azure CNI Powered by Cilium](update-azure-cni)for your network policy engine. - IPv6 isn't supported. Otherwise, it fully supports the network policy specifications in Linux.

## Azure Network Policy Manager limitations (Windows)

Azure NPM for Windows doesn't support the following features of the network policy specifications:

- Named ports.
- Stream Control Transmission Protocol (SCTP).
- Negative match label or namespace selectors. For example, all labels except
`debug=true`

. `except`

classless interdomain routing (CIDR) blocks (CIDR with exceptions).

## Known issues with Azure Network Policy Manager

You might experience temporary connectivity issues for new connections to/from pods on impacted nodes when either editing or deleting a "large enough" network policy. Hitting this race condition never impacts active connections.

If this race condition occurs for a node, the Azure NPM pod on that node enters a state where it can't update security rules, which might lead to unexpected connectivity for new connections to/from pods on the impacted node. To mitigate the issue, the Azure NPM pod automatically restarts ~15 seconds after entering this state. While Azure NPM is rebooting on the impacted node, it deletes all security rules, then reapplies security rules for all network policies. While all the security rules are being reapplied, there's a chance of temporary, unexpected connectivity for new connections to/from pods on the impacted node.

To limit the chance of hitting this race condition, you can reduce the size of the network policy. This issue is most likely to happen for a network policy with several `ipBlock`

sections. A network policy with *four or fewer* `ipBlock`

sections is less likely to hit the issue.

## Load balancer services and network policies

Kubernetes service routing for both inbound and outbound services often involves rewriting the source and destination IPs on traffic that's being processed, including traffic that comes into the cluster from a `LoadBalancer`

service. This rewrite behavior means that the network policies might not properly process traffic being received from or sent to an external service. For more information, see the [Kubernetes Network Policies documentation](https://kubernetes.io/docs/concepts/services-networking/network-policies/).

To restrict what sources can send traffic to a load balancer service, use `spec.loadBalancerSourceRanges`

to configure traffic blocking that applies before any rewrites occur. For more information, see the [AKS Standard load balancer documentation](/en-us/azure/aks/load-balancer-standard#restrict-inbound-traffic-to-specific-ip-ranges).

## Before you begin

You need the Azure CLI version 2.0.61 or later installed and configured. Find the version using the `az --version`

command. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Instead of using a system-assigned identity, you can also use a user-assigned identity. For more information, see [Use managed identities](use-managed-identity).

## Create an AKS cluster with Azure Network Policy Manager (Linux)

Set environment variables for the resource group name, cluster name, and location. Replace the values as needed.

`export RESOURCE_GROUP=myResourceGroup export CLUSTER_NAME=myAKSCluster export LOCATION=eastus`

Create an AKS cluster using the

and specify`az aks create`

`azure`

for the`network-plugin`

and`network-policy`

.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --node-count 1 \ --network-plugin azure \ --network-policy azure \ --generate-ssh-keys`


## Create an AKS cluster with Azure Network Policy Manager (Windows Server 2022 (preview))

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Install the `aks-preview`

Azure CLI extension

Install the

`aks-preview`

extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

`az extension update --name aks-preview`


### Register the `WindowsNetworkPolicyPreview`

feature flag

Register the

`WindowsNetworkPolicyPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "WindowsNetworkPolicyPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "WindowsNetworkPolicyPreview"`

When the status reflects

*Registered*, refresh the registration of the`Microsoft.ContainerService`

resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create administrator credentials for Windows Server containers

Create a username to use as administrator credentials for your Windows Server containers on your cluster. The following command prompts you for a username. Set it to

`WINDOWS_USERNAME`

.`echo "Please enter the username to use as administrator credentials for Windows Server containers on your cluster: " && read WINDOWS_USERNAME`


### Create the AKS cluster

Set environment variables for the resource group name, cluster name, and location. Replace the values as needed.

`export RESOURCE_GROUP=myResourceGroup export CLUSTER_NAME=myAKSCluster export LOCATION=eastus`

Create an AKS cluster using the

and specify`az aks create`

`azure`

for the`network-plugin`

and`network-policy`

.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --node-count 1 \ --windows-admin-username $WINDOWS_USERNAME \ --network-plugin azure \ --network-policy azure \ --generate-ssh-keys`


## Create an AKS cluster with Calico

Create an AKS cluster using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command and specify

`--network-plugin azure`

and `--network-policy calico`

. Specifying `--network-policy calico`

enables Calico on both Linux and Windows node pools.If you plan on adding Windows node pools to your cluster, include the `windows-admin-username`

and `windows-admin-password`

parameters that meet the [Windows Server password requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference). To create administrator credentials for Windows Server containers on your cluster, see [Create administrator credentials for Windows Server containers](#create-administrator-credentials-for-windows-server-containers).

Important

At this time, using Calico network policies with Windows nodes is available on new clusters using Kubernetes version 1.20 or later with Calico 3.17.2 and requires that you use Azure CNI networking. Windows nodes on AKS clusters with Calico enabled also have Floating IP enabled by default.

For clusters with only Linux node pools running Kubernetes 1.20 with earlier versions of Calico, the Calico version automatically upgrades to 3.17.2.

## Install Azure Network Policy Manager or Calico on an existing cluster

Warning

Keep the following information in mind when installing Azure NPM or Calico on an existing cluster:

- The upgrade process triggers each node pool to be reimaged simultaneously. Upgrading each node pool separately isn't supported.
- Within each node pool, nodes follow the same reimaging process as standard Kubernetes version upgrade operations. This behavior means that buffer nodes are temporarily added to minimize disruption to running applications during the node reimaging process. Any disruptions that might occur are similar to what you might encounter during a node image upgrade or
[Kubernetes version upgrade](upgrade-cluster).

The following information applies to upgrades from kubenet with Calico to Azure CNI Overlay with Calico:

- In kubenet clusters with Calico enabled, Calico is used as both a CNI and network policy engine.
- In Azure CNI clusters, Calico is used only for network policy enforcement, not as a CNI. This can cause a short delay between when the pod starts and when Calico allows outbound traffic from the pod.

Update an existing cluster to install Azure NPM or Calico using the

command and specifying`az aks update`

`azure`

or`calico`

for the`--network-policy`

parameter. The following example command shows how to install either Azure NPM:`az aks update --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --network-policy azure`


## Upgrade an existing cluster with Azure NPM or Calico to Cilium

To upgrade an existing cluster to Azure CNI Powered by Cilium, see [Upgrade an existing cluster to Azure CNI Powered by Cilium](upgrade-aks-ipam-and-dataplane)

## Connect to the AKS cluster

Configure

`kubectl`

to connect to your cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Verify network policy setup

To begin verification of network policy, you create a sample application and set traffic rules.

Create a namespace named

`demo`

to run the sample pods using the`kubectl create namespace`

command.`kubectl create namespace demo`

Create a pod named

`server`

to server on TCP port 80 using the`kubectl run`

command.`kubectl run server -n demo --image=k8s.gcr.io/e2e-test-images/agnhost:2.33 --labels="app=server" --port=80 --command -- /agnhost serve-hostname --tcp --http=false --port "80"`

Create a pod named

`client`

to run Bash using the`kubectl run`

command.`kubectl run -it client -n demo --image=k8s.gcr.io/e2e-test-images/agnhost:2.33 --command -- bash`

Note

If you want to schedule the client or server on a particular node, add the following bit before the

`--command`

argument in the pod creationcommand:`kubectl run`

`--overrides='{"spec": { "nodeSelector": {"kubernetes.io/os": "linux|windows"}}}'`

.In a separate window, get the IP address of the

`server`

pod using the`kubectl get pod`

command.`kubectl get pod --output=wide -n demo`

Your output should resemble the following example output:

`NAME READY STATUS RESTARTS AGE IP NODE NOMINATED NODE READINESS GATES server 1/1 Running 0 30s 10.224.0.72 akswin22000001 <none> <none>`


## Test connectivity with network policies

Tip

To test connectivity without network policies, run the following command in the client shell: `/agnhost connect <server-ip>:80 --timeout=3s --protocol=tcp`

. Replace `<server-ip>`

with the IP address of the server pod. If the connection is successful, there's no output.

Create a file named

`demo-policy.yaml`

and paste the following YAML manifest:`apiVersion: networking.k8s.io/v1 kind: NetworkPolicy metadata: name: demo-policy namespace: demo spec: podSelector: matchLabels: app: server ingress: - from: - podSelector: matchLabels: app: client ports: - port: 80 protocol: TCP`

Apply the network policy manifest using the

command.`kubectl apply`

`kubectl apply –f demo-policy.yaml`

In the client shell, verify connectivity with the server using the following

`/agnhost`

command:`/agnhost connect <server-ip>:80 --timeout=3s --protocol=tcp`

Connectivity with traffic is blocked because the server is labeled with

`app=server`

, but the client isn't labeled. Your output should resemble the following example output:`TIMEOUT`

Label the

`client`

and verify connectivity with the server using the`kubectl label`

command.`kubectl label pod client -n demo app=client`

If the connection is successful, there's no output.


## Migrate to self-managed Calico

AKS only supports Calico for standard Kubernetes network policies and doesn't test other features. If you want to move to self-managed Calico, follow the Tigera instructions at [Migrate from Azure-managed Calico to self-managed Calico](https://docs.tigera.io/calico/latest/getting-started/kubernetes/managed-public-cloud/aks-migrate). The Tigera documentation mentions that for self-managed Calico you set `--network-policy none`

like in the [uninstall section](#uninstall-azure-network-policy-manager-or-calico).

## Uninstall Azure Network Policy Manager or Calico

Note

Keep the following information in mind when uninstalling Azure NPM or Calico from a cluster:

- The uninstall process
**doesn't remove**Custom Resource Definitions (CRDs) and Custom Resources (CRs) used by Calico. These CRDs and CRs all have names ending with either*projectcalico.org*or*tigera.io*. You can manually remove these CRDs and associated CRs*after*successfully uninstalling Calico. - The upgrade doesn't remove any network policy resources in the cluster, but the policies are no longer enforced after the uninstall process.

Remove Azure Network Policy Manager or Calico from an existing cluster using the

command and specifying`az aks update`

`none`

for the`--network-policy`

parameter.`az aks update --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --network-policy none`


## Clean up resources

In this article, you created a namespace and two pods and applied a network policy. If you no longer need these resources, you can delete them.

Delete the resources using the

command.`kubectl delete`

`kubectl delete namespace demo`

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices-storage-nvme -->

# Best practices for ephemeral NVMe data disks in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Ephemeral NVMe data disks provide high-performance, low-latency storage that's ideal for demanding workloads running on Azure Kubernetes Service (AKS). Many modern applications, such as AI/ML training, data analytics, and high-throughput databases, require fast temporary storage to process large volumes of intermediate data efficiently. By using ephemeral NVMe disks, you can significantly improve application responsiveness and throughput, while optimizing for cost and scalability in your AKS clusters.

In contrast to remote disks, whose performance scales with the size of the virtual machine (VM), Ephemeral NVMe disks maintain full performance regardless of vCPU count. This is because they are physically attached to the VM and operate without relying on a remote disk controller. The difference is notable:

**Ultra Disk:**Achieving 400,000 IOPS requires a 112-vCPU VM (for example,[Standard_E112ibds_v5](/en-us/azure/virtual-machines/ebdsv5-ebsv5-series#ebdsv5-series-nvme)).**Local NVMe:**An 8-vCPU VM (for example,[Standard_L8s_v3](/en-us/azure/virtual-machines/sizes/storage-optimized/lsv3-series?tabs=sizestoragelocal#sizes-in-series)) can deliver 400,000 IOPS.

This results in approximately 14 times fewer vCPUs for equivalent IOPS performance, offering a substantial reduction in compute resource requirements.

This best practices article focuses on storage considerations for cluster operators. In this article, you learn:

- Common scenarios where ephemeral NVMe data disks provide performance benefits.
- How to identify which VM sizes support ephemeral NVMe data disks.
- How to use ephemeral NVMe data disks for your Kubernetes workloads.
- How ephemeral NVMe data disks work when your AKS nodes use ephemeral OS disks.
- How to measure the performance of your workloads using ephemeral NVMe data disks.

## Common scenarios of high-performance workloads

Ephemeral NVMe data disks are ideal for workloads that demand high throughput, low latency, and fast access to temporary or intermediate data. The following scenarios highlight where local NVMe disks provide the most significant benefits:

### High-performance databases (for example, PostgreSQL)

For databases such as PostgreSQL, especially in high-availability (HA) or read-intensive deployments, local NVMe disks can dramatically improve transaction throughput and reduce query latency. When used for temporary tablespaces, write-ahead logs (WAL), or as a cache layer, NVMe disks help offload I/O from persistent storage, accelerating analytics and transactional workloads.

Best practices:

- Use NVMe-backed volumes for PostgreSQL temp directories and WAL logs to maximize IOPS and minimize latency.
- For HA scenarios, ensure that persistent data directories remain on durable storage, while using NVMe for non-persistent, high-churn data.
- See
[PostgreSQL HA on AKS](/en-us/azure/aks/postgresql-ha-overview)for architecture guidance.

### AI model hosting and inference (for example, KAITO)

AI model serving platforms like [KAITO](https://github.com/kaito-project/kaito) benefit from NVMe disks for rapid model loading, artifact caching, and high-throughput inference. When models are stored as Open Container Initiative (OCI) artifacts and loaded on demand, local NVMe storage ensures minimal cold start times and efficient batch processing.

Best practices:

- Use NVMe-backed volumes for model cache directories to accelerate model pulls and reduce inference latency.
- For distributed inference, ensure each node has sufficient NVMe capacity to cache frequently used models.
- Integrate with Kubernetes-native storage solutions (for example, Azure Container Storage) for automated management and monitoring.
- See
[KAITO model as OCI artifacts](https://kaito-project.github.io/kaito/docs/next/model-as-oci-artifacts)for architecture guidance.

### Data analytics and ETL pipelines

Workloads that process large volumes of intermediate data, such as [Spark](https://spark.apache.org/), [Dask](https://www.dask.org/), or custom ETL jobs, can apply NVMe disks for shuffle storage, temporary files, and scratch space. This approach reduces bottlenecks during data transformation and aggregation.

Best practices:

- Configure shuffle and temp directories to use NVMe-backed storage.
- Clean up temporary data promptly to maximize available space.

### Caching layers and key-value stores

In-memory databases and caching solutions (for example, Redis, Memcached, RocksDB) can use NVMe disks as a fast persistence layer or for overflow storage, providing a balance between speed and durability.

Best practices:

- Use NVMe for write-heavy cache workloads where persistence isn't critical.
- Monitor disk usage to avoid eviction or data loss due to node restarts.

### High-performance computing (HPC) and simulation

HPC workloads, including genomics, financial modeling, and scientific simulations, often require rapid access to large datasets and scratch space for intermediate results. NVMe disks provide the necessary bandwidth and low latency for these scenarios.

## Check VM sizes with ephemeral NVMe data disks

Ephemeral NVMe data disks are available on select Azure VM sizes that offer local, high-performance storage directly attached to the physical host. These disks are ideal for temporary data, such as caches, scratch files, or intermediate processing, and aren't persisted after a VM is deallocated or stopped. The number and capacity of NVMe disks vary by VM size and family.

To determine which VM sizes support ephemeral NVMe data disks and their configurations, refer to the [Azure VM documentation](/en-us/azure/virtual-machines/sizes) and the [AKS supported VM sizes](/en-us/azure/aks/quotas-skus-regions). Look for VM series such as [Lsv4](/en-us/azure/virtual-machines/sizes/storage-optimized/lsv4-series) and [Ddsv6](/en-us/azure/virtual-machines/sizes/general-purpose/ddsv6-series), which are designed for high-throughput, low-latency workloads.

The following table lists example VM sizes and their NVMe disk configurations:

| VM Size | Number of NVMe Disks | Total NVMe Capacity (GiB) |
|---|---|---|
| Standard_L4s_v4 | 2 | 894 |
| Standard_L8s_v4 | 4 | 1,788 |
| Standard_L96s_v4 | 12 | 21,456 |
| Standard_D16ds_v6 | 2 | 880 |
| Standard_D32ds_v6 | 4 | 1,760 |
| Standard_D96ds_v6 | 6 | 5,280 |

For AI workloads that require GPU acceleration, consider VM sizes in the NC, ND, and NV series. Some GPU-enabled VM sizes, such as `Standard_NC48ads_A100_v4`

and `Standard_ND96isr_H100_v5`

, offer local NVMe storage in addition to powerful GPUs. These VMs are suitable for AI training, inference, and other compute-intensive scenarios where both GPU and fast local storage are needed.

Example GPU VM sizes with NVMe disks:

| VM Size | GPU Type | Number of NVMe Disks | Total NVMe Capacity (GiB) |
|---|---|---|---|
| Standard_NC48ads_A100_v4 | 2 x A100 | 2 | 1,788 |
| Standard_NC96ads_A100_v4 | 4 x A100 | 4 | 3,576 |
| Standard_ND96isr_H100_v5 | 8 x H100 | 8 | 28,610 |
| Standard_ND96isr_H200_v5 | 8 x H200 | 8 | 28,610 |

Note

Actual NVMe disk capacity and number might vary by region and VM generation. Not all GPU VM sizes include local NVMe storage. Always verify the latest VM specifications and NVMe disk availability in the Azure documentation, as configurations might change.

## Validate ephemeral NVMe data disks configuration

To ensure your AKS node is provisioned with ephemeral NVMe data disks, you can validate the configuration using the Azure CLI and by inspecting the node directly.

### Option 1: Use Azure CLI to check NVMe disk configuration

You can use the Azure CLI to inspect the VM size and attached NVMe disks with the following sample commands.

```
# Modify location and VM size if needed
locationName="eastus"
vmSize="Standard_L8s_v4"
az vm list-skus --resource-type virtualMachines --location $locationName \
--query "[?name=='$vmSize'].{
SkuName: name,
NvmeDiskSizeInMiB: capabilities[?name=='NvmeDiskSizeInMiB'] | [0].value,
NvmeSizePerDiskInMiB: capabilities[?name=='NvmeSizePerDiskInMiB'] | [0].value
}" -o table
SkuName NvmeDiskSizeInMiB NvmeSizePerDiskInMiB
--------------- ------------------- ----------------------
Standard_L8s_v4 1830912 457728
```


### Option 2: Use `lsblk`

to check disk and mount layout on the node

Login into an AKS node:

```
kubectl get nodes
# Modify the node name from above list as needed
nodeName="aks-myworkload-22647054-vmss000000"
# Use your approach to login into the node.
kubectl debug "node/$nodeName" \
--image=ubuntu \
--profile=sysadmin -it \
-- chroot /host /bin/bash
```


Once connected, use `lsblk`

to list block devices and identify NVMe disks:

```
lsblk -o NAME,HCTL,SIZE,MOUNTPOINT,MODEL
NAME HCTL SIZE MOUNTPOINT MODEL
sr0 0:0:0:2 750K Virtual DVD-ROM
nvme0n1 110G Microsoft NVMe Direct Disk v2
```


NVMe disks typically appear as `nvme*n1`

and are configured with `Microsoft NVMe Direct Disk*`

on model. This result confirms the presence and configuration of ephemeral NVMe data disks on your AKS node.

## Use ephemeral NVMe data disks in workloads

There are several ways to use ephemeral NVMe data disks in your AKS workloads. The most common approaches are:

### Azure Container Storage (recommended)

[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction) is a Kubernetes-native storage solution that abstracts and manages local NVMe disks as persistent volumes, with advanced orchestration and data services.

You can deploy Azure Container Storage in your AKS cluster and provision volumes using standard Kubernetes PVCs.

Azure Container Storage offers the following advantages:

- Kubernetes-native experience with PersistentVolumeClaims.
- Automated discovery and management of NVMe disks for any VM sizes.
- Supports advanced features: dynamic provisioning, data security, and native integration with AKS.
- Improved reliability and operational simplicity.
- Enables high-performance workloads with default volume striping cross all available disks.

Azure Container Storage is the best option for Kubernetes workloads to orchestrate ephemeral NVMe data disks. It combines the raw performance of NVMe disks with Kubernetes-native management, security, and built-in integration with Azure’s monitoring features and Prometheus. This approach reduces operational complexity, improves reliability, and enables advanced scenarios (such as scaling and failover) that are difficult to achieve with `emptyDir`

or `hostPath`

.

For more information, see [Azure Container Storage documentation](/en-us/azure/storage/container-storage/container-storage-introduction).

`emptyDir`

Volumes

`emptyDir`

is a Kubernetes volume type that uses the node's local storage. When backed by NVMe disks, `emptyDir`

provides high throughput and low latency for temporary data.

To use this method, define an `emptyDir`

volume in your Pod spec. By default, it uses the fastest available storage (NVMe if present).

#### Advantages

- Simple to use and configure.
- No external dependencies.
- High performance when backed by NVMe.

#### Disadvantages

- Data is lost if the Pod is rescheduled to another node.
- No data persistence or replication.
- Limited to single NVMe disk.

`hostPath`

Volumes

`hostPath`

mounts a specific directory or disk from the node’s filesystem into the Pod. You can target NVMe mount points directly.

To use this method, specify the NVMe disk path (for example, `/mnt`

or `/mnt/nvme0n1`

) in the Pod spec.

#### Advantages

- Direct access to NVMe disk.
- Useful for advanced scenarios (for example, custom formatting, partitioning).

#### Disadvantages

- Tightly coupled to node layout; not portable.
- Security risks if not properly restricted.
- Limited to single NVMe disk.

## Ephemeral NVMe data disks with ephemeral OS disks

When deploying AKS nodes with local NVMe data disks, such as the `Standard_D2ads_v6`

VM size (single 100 GiB NVMe disk) with ephemeral OS disks setting opt-in, you might observe that the ephemeral OS disk (for example, 60 GiB) is provisioned from the NVMe capacity. However, the unused NVMe space (in this example, the extra 40 GiB) isn’t available to use, and there’s no supported way to access or recover it after the node is created.

This behavior is by design, as the ephemeral OS disk requirements dictate how the NVMe device is partitioned at provisioning time. It can be confusing since you don’t get access to all of its storage, especially with many VM sizes that come with only one NVMe disk.

Use the following example to validate this behavior:

```
# Create Standard_D2ads_v6 (Single 100 GiB NVMe disk) node pool using ephemeral OS disk with 60 GiB capacity
az aks nodepool add \
--resource-group $resourceGroup \
--cluster-name $clusterName \
--name $nodePoolName \
--node-count 1 \
--node-vm-size Standard_D2ads_v6 \
--node-osdisk-type Ephemeral \
--node-osdisk-size 60
kubectl debug "node/$nodeName" \
--image=ubuntu \
--profile=sysadmin -it \
-- chroot /host /bin/bash
lsblk -o NAME,FSTYPE,LABEL,MOUNTPOINT,SIZE,VENDOR,MODEL
NAME FSTYPE LABEL MOUNTPOINT SIZE VENDOR MODEL
sr0 750K Msft Virtual DVD-ROM
nvme0n1 60G MSFT NVMe Accelerator v1.0
|-nvme0n1p1 ext4 cloudimg-rootfs / 59.9G
|-nvme0n1p14 4M
`-nvme0n1p15 vfat UEFI /boot/efi 106M
```


When you use VM sizes with a single local NVMe data disk and enable ephemeral OS disk, the OS consumes the entire NVMe disk, leaving no space available for Kubernetes workloads to provision persistent volumes. For VM sizes with two or more local NVMe data disks, one disk is used for the ephemeral OS, and the others can be used to provision persistent volumes for your workloads.

### Current limitations

- The ephemeral OS disk consumes a portion of one local NVMe drive, with the remainder left inaccessible.
- There's no supported way to access or mount the unused NVMe space after node creation.
- You can't update or repartition the NVMe disk post-deployment.

### Customer impact

- Reduced usable NVMe capacity compared to what is advertised for the VM size.
- Inability to fully use high-performance local storage for workloads.
- Potential confusion and inconvenience during upgrades or node replacement.

### Recommendation

Decide the intended use of local NVMe disks, either for the OS disk or for Kubernetes workload storage—before provisioning AKS nodes. Ephemeral OS disk configuration is immutable after node creation, so planning ahead avoids the need to recreate nodes if requirements change.

Omit the OS disk size input when creating AKS nodes with ephemeral OS disks on NVMe-backed VMs. This prevents misconfiguration and aligns with product documentation, reducing the risk of inaccessible capacity and upgrade issues.


Note

These improvements are important for user experience and operational efficiency, especially as more VM SKUs with single NVMe disks become available. Follow the latest AKS documentation and monitor Azure updates for enhancements in ephemeral disk management.

## Measure workload performance with ephemeral NVMe data disks

Ephemeral NVMe data disks deliver high throughput and low latency for AKS workloads, but it's important to validate performance against your application's requirements. Benchmark your workloads on different VM sizes to identify the optimal configuration, and adjust VM sizes or disk configurations as needed.

Set up your application using local NVMe volumes, then use workload-specific benchmarking tools to measure IOPS, throughput, and latency. For example, with PostgreSQL, follow [Create infrastructure for PostgreSQL](/en-us/azure/aks/create-postgresql-ha) to deploy your environment, and use [pgbench](https://cloudnative-pg.io/documentation/1.26/benchmarking/#pgbench) to evaluate database performance.

The following steps introduce generic benchmarking with fio and local NVMe volumes managed by Azure Container Storage.

Enable Azure Container Storage on your AKS cluster. See

[Azure Container Storage Quickstart](/en-us/azure/storage/container-storage/container-storage-aks-quickstart)Deploy storage class, generic volume, fio pod with local NVMe volumes. See

[Use local NVMe with Azure Container Storage](/en-us/azure/storage/container-storage/use-container-storage-with-local-disk).Run the following fio command and modify as needed.

`# Run fio benchmark kubectl exec -it fiopod -- fio --directory=/mnt/cns --size=4000MB --filename_format='testfile.$jobnum' --wait_for_previous \ --thread --group_reporting --direct=1 --randrepeat=0 --norandommap=1 \ --ioengine=io_uring --numjobs=8 --disable_clat=1 --disable_slat=1 \ --name=precondition --bs=1M --iodepth=64 --rw=write \ --name=randwritebench --rw=randwrite --bs=4k --iodepth=16 --time_based --runtime=60 \ --name=randreadbench --rw=randread --bs=4k --iodepth=16 --time_based --runtime=60 \ --name=seqwritebench --rw=write --bs=128k --iodepth=16 --time_based --runtime=60 \ --name=seqreadbench --rw=read --bs=128k --iodepth=16 --time_based --runtime=60 > ./fio.log result=$(cat ./fio.log | \ awk ' BEGIN { print "Scenario,Type,IOPS,BW(MiB/s)" } /^[a-z]+bench:/ { split($1, a, ":") scenario = a[1] } /read: IOPS=/ && scenario ~ /(randreadbench|seqreadbench)/ { type = "read" match($0, /IOPS=([0-9.]+)([kM]?)/, iops_arr) match($0, /BW=([0-9.]+)MiB\/s/, bw_arr) iops = iops_arr[1] unit = iops_arr[2] if (unit == "k") iops *= 1000 else if (unit == "M") iops *= 1000000 bw = bw_arr[1] printf "%s,%s,%.0f,%.2f\n", scenario, type, iops, bw } /write: IOPS=/ && scenario ~ /(randwritebench|seqwritebench)/ { type = "write" match($0, /IOPS=([0-9.]+)([kM]?)/, iops_arr) match($0, /BW=([0-9.]+)MiB\/s/, bw_arr) iops = iops_arr[1] unit = iops_arr[2] if (unit == "k") iops *= 1000 else if (unit == "M") iops *= 1000000 bw = bw_arr[1] printf "%s,%s,%.0f,%.2f\n", scenario, type, iops, bw } ' | column -t -s,)`

Run fio on the VM with single NVMe disk (for example, standard_l8s_v3) and the VM with two NVMe disks (for example, Standard_L16s_v3). Evaluate the performance improvements from the NVMe volume striping cross multiple NVMe disks. See the following charts as examples:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr-overview -->

# Dapr extension for Azure Kubernetes Service (AKS) and Arc-enabled Kubernetes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Distributed Application Runtime (Dapr)](https://docs.dapr.io/) offers APIs that help you write and implement simple, portable, resilient, and secured microservices. Dapr APIs run as a sidecar process in tandem with your applications and abstract away common complexities you may encounter when building distributed applications, such as:

- Service discovery
- Message broker integration
- Encryption
- Observability
- Secret management

Dapr is incrementally adoptable. You can use any of the API building blocks as needed. [Learn the support level Microsoft offers for the Dapr extension.](#issue-handling)

## Capabilities and features

[Using the Dapr extension to provision Dapr on your AKS or Arc-enabled Kubernetes cluster](dapr) eliminates the overhead of:

- Downloading Dapr tooling
- Manually installing and managing the Dapr runtime on your AKS cluster

Additionally, the extension offers support for all [native Dapr configuration capabilities](dapr-settings) through simple command-line arguments.

Dapr provides the following set of capabilities to help with your microservice development on AKS:

- Easy provisioning of Dapr on AKS through
[cluster extensions](cluster-extensions) - Portability enabled through HTTP and gRPC APIs which abstract underlying technologies choices
- Reliable, secure, and resilient service-to-service calls through HTTP and gRPC APIs
- Publish and subscribe messaging made easy with support for CloudEvent filtering and "at-least-once" semantics for message delivery
- Pluggable observability and monitoring through Open Telemetry API collector
- Independent of language, while also offering language specific software development kits (SDKs)
- Integration with Visual Studio Code through the Dapr extension
[More APIs for solving distributed application challenges](https://docs.dapr.io/concepts/building-blocks-concept/)

## Issue handling

Microsoft categorizes issues raised against the Dapr extension into two parts:

- Extension operations
- Dapr runtime (including APIs and components)

The following table breaks down support priority levels for each of these categories.

| Description | Security risks/Regressions | Functional issues | |
|---|---|---|---|
Extension operations |
Issues encountered during extension operations, such as installing/uninstalling or upgrading the Dapr extension. | Microsoft prioritizes for immediate resolution. | Microsoft investigates and addresses as needed. |
Dapr runtime |
Issues encountered when using the Dapr runtime, APIs, and components via the extension, like cert expiration and unexpected component behavior. |
|

[Discuss issues with the Dapr open source project](https://github.com/dapr/dapr/issues/new/choose)to resolve in a hotfix or future Dapr open source release. Known open source functional issues won't be investigated by Microsoft at this time.### Clouds/regions

Global Azure cloud is supported with AKS and Arc support on the following regions:

| Region | AKS support | Arc for Kubernetes support |
|---|---|---|
`australiaeast` |
✔️ | ✔️ |
`australiasoutheast` |
✔️ | ❌ |
`brazilsouth` |
✔️ | ❌ |
`canadacentral` |
✔️ | ✔️ |
`canadaeast` |
✔️ | ✔️ |
`centralindia` |
✔️ | ✔️ |
`centralus` |
✔️ | ✔️ |
`eastasia` |
✔️ | ✔️ |
`eastus` |
✔️ | ✔️ |
`eastus2` |
✔️ | ✔️ |
`eastus2euap` |
❌ | ✔️ |
`francecentral` |
✔️ | ✔️ |
`francesouth` |
✔️ | ❌ |
`germanywestcentral` |
✔️ | ✔️ |
`japaneast` |
✔️ | ✔️ |
`japanwest` |
✔️ | ❌ |
`koreacentral` |
✔️ | ✔️ |
`koreasouth` |
✔️ | ❌ |
`northcentralus` |
✔️ | ✔️ |
`northeurope` |
✔️ | ✔️ |
`norwayeast` |
✔️ | ❌ |
`southafricanorth` |
✔️ | ❌ |
`southcentralus` |
✔️ | ✔️ |
`southeastasia` |
✔️ | ✔️ |
`southindia` |
✔️ | ❌ |
`swedencentral` |
✔️ | ✔️ |
`switzerlandnorth` |
✔️ | ✔️ |
`uaenorth` |
✔️ | ❌ |
`uksouth` |
✔️ | ✔️ |
`ukwest` |
✔️ | ❌ |
`westcentralus` |
✔️ | ✔️ |
`westeurope` |
✔️ | ✔️ |
`westus` |
✔️ | ✔️ |
`westus2` |
✔️ | ✔️ |
`westus3` |
✔️ | ✔️ |

## Frequently asked questions

### How do Dapr and Service meshes compare?

While Dapr and service meshes do offer some overlapping capabilities, a service mesh is focused on networking concerns, whereas Dapr is focused on providing building blocks that make building applications as microservices easier. Dapr is developer-centric, while service meshes are infrastructure-centric.

Some common capabilities that Dapr shares with service meshes include:

- Secure service-to-service communication with mTLS encryption
- Service-to-service metric collection
- Service-to-service distributed tracing
- Resiliency through retries

Dapr provides other application-level building blocks for state management, pub/sub messaging, actors, and more. However, Dapr doesn't provide capabilities for traffic behavior, such as routing or traffic splitting. If your solution would benefit from the traffic splitting a service mesh provides, consider using [Open Service Mesh](open-service-mesh-about).

For more information on Dapr and service meshes, and how they can be used together, visit the [Dapr documentation](https://docs.dapr.io/).

### How does the Dapr secrets API compare to the Secrets Store CSI driver?

Both the Dapr secrets API and the managed Secrets Store CSI driver allow for the integration of secrets held in an external store, abstracting secret store technology from application code.

The Secrets Store CSI driver mounts secrets held in Azure Key Vault as a CSI volume for consumption by an application.

Dapr exposes secrets via a RESTful API that can be:

- Called by application code
- Configured with assorted secret stores

The following table lists the capabilities of each offering:

| Dapr secrets API | Secrets Store CSI driver | |
|---|---|---|
Supported secrets stores |
Local environment variables (for Development); Local file (for Development); Kubernetes Secrets; AWS Secrets Manager; Azure Key Vault secret store; Azure Key Vault with Managed Identities on Kubernetes; GCP Secret Manager; HashiCorp Vault | Azure Key Vault secret store |
Accessing secrets in application code |
Call the Dapr secrets API | Access the mounted volume or sync mounted content as a Kubernetes secret and set an environment variable |
Secret rotation |
New API calls obtain the updated secrets | Polls for secrets and updates the mount at a configurable interval |
Logging and metrics |
The Dapr sidecar generates logs, which can be configured with collectors such as Azure Monitor, emits metrics via Prometheus, and exposes an HTTP endpoint for health checks | Emits driver and Azure Key Vault provider metrics via Prometheus |

For more information on the secret management in Dapr, see the [secrets management overview](https://docs.dapr.io/developing-applications/building-blocks/secrets/secrets-overview/).

For more information on the Secrets Store CSI driver and Azure Key Vault provider, see the [Secrets Store CSI driver overview](csi-secrets-store-driver).

### How does the managed Dapr cluster extension compare to the open source Dapr offering?

The managed Dapr cluster extension is the easiest method to provision Dapr on an AKS cluster. With the extension, you're able to offload management of the Dapr runtime version by opting into automatic upgrades. Additionally, the extension installs Dapr with smart defaults (for example, provisioning the Dapr control plane in high availability mode).

When installing Dapr open source via helm or the Dapr CLI, developers and cluster maintainers are also responsible for runtime versions and configuration options.

Lastly, the Dapr extension is an extension of AKS, therefore you can expect the same support policy as other AKS features.

[Learn more about migrating from Dapr open source to the Dapr extension for AKS](dapr-migration).

### How can I authenticate Dapr components with Microsoft Entra ID using managed identities?

- Learn how
[Dapr components authenticate with Microsoft Entra ID](https://docs.dapr.io/developing-applications/integrations/azure/azure-authentication). - Learn about
[using managed identities with AKS](use-managed-identity).

### How can I switch to using the Dapr extension if I've already installed Dapr via a method, such as Helm?

Recommended guidance is to completely uninstall Dapr from the AKS cluster and reinstall it via the cluster extension. [You can also check for the existing Dapr installation and migrate it to AKS.](dapr-migration)

If you install Dapr through the AKS extension, our recommendation is to continue using the extension for future management of Dapr instead of the Dapr CLI. Combining the two tools can cause conflicts and result in undesired behavior.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator-fine-tune -->

# Fine-tune and deploy an AI model for inferencing on Azure Kubernetes Service (AKS) with the AI toolchain operator add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to fine-tune and deploy a language model inferencing workload on AKS with the AI toolchain operator add-on. You learn how to accomplish the following tasks:

[Set environment variables](#export-environmental-variables)to reference your Azure Container Registry (ACR) and repository details.[Create your container registry image push/pull secret](#create-a-new-secret-for-your-private-registry)to store and retrieve private fine-tuning adapter images.[Select a supported model and fine-tune it to your data](#fine-tune-an-ai-model).[Test the inference service endpoint](#test-the-model-inference-service-endpoint).[Clean up resources](#clean-up-resources).

The AI toolchain operator (KAITO) is a managed add-on for AKS that simplifies the deployment and operations for AI models on your AKS clusters. Starting with [KAITO version 0.3.1](https://github.com/kaito-project/kaito/releases/tag/v0.3.1) and above, you can use the AKS managed add-on to fine-tune supported foundation models with new data and enhance the accuracy of your AI models. To learn more about parameter efficient fine-tuning methods and their use cases, see [Concepts - Fine-tuning language models for AI and machine learning workflows on AKS](concepts-fine-tune-language-models).

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Azure CLI version 2.47.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Prerequisites

- The Kubernetes command-line client, kubectl, installed and configured. For more information, see
[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/). - Configure
[Azure Container Registry (ACR) integration](aks-extension-attach-azure-container-registry)of a new or existing ACR with your AKS cluster. - Install the
[AI toolchain operator add-on](ai-toolchain-operator)on your AKS cluster. - If you already have the AI toolchain operator add-on installed, update your AKS cluster to the latest version to run KAITO v0.3.1+ and ensure that the AI toolchain operator add-on feature flag is enabled.

## Export environmental variables

To simplify the configuration steps in this article, you can define environment variables using the following commands. Make sure to replace the placeholder values with your own.

```
ACR_NAME="myACRname"
ACR_USERNAME="myACRusername"
REPOSITORY="myRepository"
VERSION="repositoryVersion'
ACR_PASSWORD=$(az acr token create --name $ACR_USERNAME --registry $ACR_NAME --expiration-in-days 10 --repository $REPOSITORY content/write content/read --query "credentials.passwords[0].value" --output tsv)
```


## Create a new secret for your private registry

In this example, your KAITO fine-tuning deployment produces a containerized adapter output, and the KAITO workspace requires a new push secret as authorization to push the adapter image to your ACR.

Generate a new secret to provide the KAITO fine-tuning workspace access to push the model fine-tuning output image to your ACR using the `kubectl create secret docker-registry`

command.

```
kubectl create secret docker-registry myregistrysecret --docker-server=$ACR_NAME.azurecr.io --docker-username=$ACR_USERNAME --docker-password=$ACR_PASSWORD
```


## Fine-tune an AI model

In this example, you fine-tune the [Phi-3-mini small language model](https://huggingface.co/docs/transformers/main/en/model_doc/phi3) using the qLoRA tuning method by applying the following Phi-3-mini KAITO fine-tuning workspace CRD:

```
apiVersion: kaito.sh/v1alpha1
kind: Workspace
metadata:
name: workspace-tuning-phi-3-mini
resource:
instanceType: "Standard_NC24ads_A100_v4"
labelSelector:
matchLabels:
apps: tuning-phi-3-mini-pycoder
tuning:
preset:
name: phi3mini128kinst
method: qlora
input:
urls:
- “myDatasetURL”
output:
image: “$ACR_NAME.azurecr.io/$REPOSITORY:$VERSION”
imagePushSecret: myregistrysecret
```


This example uses a public dataset specified by a URL in the input. If choosing an image as the source of your fine-tuning data, please refer to the [KAITO fine-tuning API](https://github.com/kaito-project/kaito/tree/main) specification to adjust the input to pull an image from your ACR.

Note

The choice of GPU SKU is critical since model fine-tuning normally requires more GPU memory compared to model inference. To avoid GPU Out-Of-Memory errors, we recommend using NVIDIA A100 or higher tier GPUs.

Apply the KAITO fine-tuning workspace CRD using the

`kubectl apply`

command.`kubectl apply workspace-tuning-phi-3-mini.yaml`

Track the readiness of your GPU resources, fine-tuning job, and workspace using the

`kubectl get workspace`

command.`kubectl get workspace -w`

Your output should look similar to the following example output:

`NAME INSTANCE RESOURCE READY INFERENCE READY JOB STARTED WORKSPACE SUCCEEDED AGE workspace-tuning-phi-3-mini Standard_NC24ads_A100_v4 True True 3m 45s`

Check the status of your fine-tuning job pods using the

`kubectl get pods`

command.`kubectl get pods`


Note

You can store the adapter to your specific output location as a container image or any storage type supported by Kubernetes.

## Deploy the fine-tuned model for inferencing

Now, you use the Phi-3-mini adapter image created in the previous section for a new inferencing deployment with this model.

The KAITO inference workspace CRD below consists of the following resources and adapter(s) to deploy on your AKS cluster:

```
apiVersion: kaito.sh/v1alpha1
kind: Workspace
metadata:
name: workspace-phi-3-mini-adapter
resource:
instanceType: "Standard_NC6s_v3"
labelSelector:
matchLabels:
apps: phi-3-adapter
inference:
preset:
name: “phi-3-mini-128k-instruct“
adapters:
-source:
name: kubernetes-adapter
image: $ACR_NAME.azurecr.io/$REPOSITORY:$VERSION
imagePullSecrets:
- myregistrysecret
strength: “1.0”
```


Note

Optionally, you can pull in several adapters created from fine-tuning deployments with the same model on different data sets by defining additional "source" fields. Inference with different adapters to compare the performance of your fine-tuned model in varying contexts.

Apply the KAITO inference workspace CRD using the

`kubectl apply`

command.`kubectl apply -f workspace-phi-3-mini-adapter.yaml`

Track the readiness of your GPU resources, inference server, and workspace using the

`kubectl get workspace`

command.`kubectl get workspace -w`

Your output should look similar to the following example output:

`NAME INSTANCE RESOURCE READY INFERENCE READY JOB STARTED WORKSPACE SUCCEEDED AGE workspace-phi-3-mini-adapter Standard_NC6s_v3 True True True 5m 47s`

Check the status of your inferencing workload pods using the

`kubectl get pods`

command.`kubectl get pods`

It might take several minutes for your pods to show the

`Running`

status.

## Test the model inference service endpoint

Check your model inferencing service and retrieve the service IP address using the

`kubectl get svc`

command.`export SERVICE_IP=$(kubectl get svc workspace-phi-3-mini-adapter -o jsonpath=’{.spec.clusterIP}’)`

Run your fine-tuned Phi-3-mini model with a sample input of your choice using the

`kubectl run`

command. The following example asks the generative AI model,*"What is AKS?"*:`kubectl run -it --rm --restart=Never curl --image=curlimages/curl -- curl -X POST http://$SERVICE_IP/chat -H "accept: application/json" -H "Content-Type: application/json" -d "{\"prompt\":\"What is AKS?\"}"`

Your output might look similar to the following example output:

`"Kubernetes on Azure" is the official name. https://learn.microsoft.com/en-us/azure/aks/ ...`


## Clean up resources

If you no longer need these resources, you can delete them to avoid incurring extra Azure charges. To calculate the estimated cost of your resources, you can use the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?service=kubernetes-service).

Delete the KAITO workspaces and their allocated resources on your AKS cluster using the `kubectl delete workspace`

command.

```
kubectl delete workspace workspace-tuning-phi-3-mini
kubectl delete workspace workspace-phi-3-mini-adapter
```


## Next steps

- Learn more about fine-tuning language models with KAITO in this
[AKS Engineering Blog](https://blog.aks.azure.com/2024/08/23/fine-tuning-language-models-with-kaito)! - Explore
[MLOps for AI and machine learning workflows](concepts-machine-learning-ops)and best practices on AKS - Learn about supported families of
[GPUs on Azure Kubernetes Service](gpu-cluster)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-disk-customer-managed-keys -->

# Bring your own keys (BYOK) with Azure managed disks in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure encrypts all data in a managed disk at rest. By default, data is encrypted with Microsoft-managed keys. For more control over encryption keys, you can supply customer-managed keys to use for encryption at rest for both the OS and data disks for your AKS clusters.

Learn more about customer-managed keys on [Linux](/en-us/azure/virtual-machines/disk-encryption#customer-managed-keys) and [Windows](/en-us/azure/virtual-machines/disk-encryption#customer-managed-keys).

## Prerequisites

- You must enable soft delete and purge protection for
*Azure Key Vault*when using Key Vault to encrypt managed disks. - You need the Azure CLI version 2.11.1 or later.
- Data disk encryption and customer-managed keys are supported on Kubernetes versions 1.24 and higher.
- If you choose to rotate (change) your keys periodically, see
[Customer-managed keys and encryption of Azure managed disk](/en-us/azure/virtual-machines/disk-encryption)for more information.

## Limitations

Encryption of an OS disk with customer-managed keys can only be enabled when creating an AKS cluster.

Virtual nodes are not supported.

When encrypting an ephemeral OS disk-enabled node pool with customer-managed keys, if you want to rotate the key in Azure Key Vault, there are two options to consider:

Immediate usage of new CMK

- Scale down the node pool count to 0.
- Rotate the key.
- Scale up the node pool to the original count.

Gradual usage of new CMK

- Allow AKS node image upgrades or version upgrades to naturally adopt the new CMK over time.
- Until all nodes in the pool are upgraded, the existing CMK will continue to function without disruption.
- Once the upgrade process is complete across all nodes, the new CMK takes effect seamlessly.


## Create an Azure Key Vault instance

Use an Azure Key Vault instance to store your keys. You can optionally use the Azure portal to [Configure customer-managed keys with Azure Key Vault](/en-us/azure/storage/common/customer-managed-keys-configure-key-vault)

Create a new *resource group*, then create a new *Key Vault* instance and enable soft delete and purge protection. Ensure you use the same region and resource group names for each command.

```
# Optionally retrieve Azure region short names for use on upcoming commands
az account list-locations
```


```
# Create new resource group in a supported Azure region
az group create --location myAzureRegionName --name myResourceGroup
# Create an Azure Key Vault resource in a supported Azure region
az keyvault create --name myKeyVaultName --resource-group myResourceGroup --location myAzureRegionName --enable-purge-protection true
```


## Create an instance of a DiskEncryptionSet

Replace *myKeyVaultName* with the name of your key vault. You also need a *key* stored in Azure Key Vault to complete the following steps. Either store your existing Key in the Key Vault you created on the previous steps, or [generate a new key](/en-us/azure/key-vault/general/manage-with-cli2) and replace *myKeyName* with the name of your key.

Note

For cross-account access support for customer-managed encryption keys, you need to create the DiskEncryptionSet for cross-tenant customer-managed keys as detailed in [this guide](/en-us/azure/virtual-machines/disks-cross-tenant-customer-managed-keys?tabs=azure-cli#create-a-disk-encryption-set). The remaining storage class configuration is the same as normal customer managed keys.

```
# Retrieve the Key Vault Id and store it in a variable
keyVaultId=$(az keyvault show --name myKeyVaultName --query "[id]" -o tsv)
# Retrieve the Key Vault key URL and store it in a variable
keyVaultKeyUrl=$(az keyvault key show --vault-name myKeyVaultName --name myKeyName --query "[key.kid]" -o tsv)
# Create a DiskEncryptionSet
az disk-encryption-set create --name myDiskEncryptionSetName --location myAzureRegionName --resource-group myResourceGroup --source-vault $keyVaultId --key-url $keyVaultKeyUrl
```


Important

Make sure that the DiskEncryptionSet is located in the same region as your AKS cluster and that the AKS cluster identity has **read** access to the DiskEncryptionSet.

## Grant the DiskEncryptionSet access to key vault

Use the DiskEncryptionSet and resource groups you created on the prior steps, and grant the DiskEncryptionSet resource access to the Azure Key Vault.

```
# Retrieve the DiskEncryptionSet value and set a variable
desIdentity=$(az disk-encryption-set show --name myDiskEncryptionSetName --resource-group myResourceGroup --query "[identity.principalId]" -o tsv)
# Update security policy settings
az keyvault set-policy --name myKeyVaultName --resource-group myResourceGroup --object-id $desIdentity --key-permissions wrapkey unwrapkey get
```


## Create a new AKS cluster and encrypt the OS disk

Either create a new resource group, or select an existing resource group hosting other AKS clusters, then use your key to encrypt either using network-attached OS disks or ephemeral OS disk. By default, a cluster uses ephemeral OS disk when possible in conjunction with VM size and OS disk size.

Run the following command to retrieve the DiskEncryptionSet value and set a variable:

```
diskEncryptionSetId=$(az disk-encryption-set show --name mydiskEncryptionSetName --resource-group myResourceGroup --query "[id]" -o tsv)
```


If you want to create a new resource group for the cluster, run the following command:

```
az group create --name myResourceGroup --location myAzureRegionName
```


To create a regular cluster using network-attached OS disks encrypted with your key, you can do so by specifying the `--node-osdisk-type=Managed`

argument.

```
az aks create --name myAKSCluster --resource-group myResourceGroup --node-osdisk-diskencryptionset-id $diskEncryptionSetId --generate-ssh-keys --node-osdisk-type Managed
```


To create a cluster with ephemeral OS disk encrypted with your key, you can do so by specifying the `--node-osdisk-type=Ephemeral`

argument. You also need to specify the argument `--node-vm-size`

because the default vm size is too small and doesn't support ephemeral OS disk.

```
az aks create --name myAKSCluster --resource-group myResourceGroup --node-osdisk-diskencryptionset-id $diskEncryptionSetId --generate-ssh-keys --node-osdisk-type Ephemeral --node-vm-size Standard_DS3_v2
```


When new node pools are added to the cluster, the customer-managed key provided during the create process is used to encrypt the OS disk. The following example shows how to deploy a new node pool with an ephemeral OS disk.

```
az aks nodepool add --cluster-name $CLUSTER_NAME --resource-group $RG_NAME --name $NODEPOOL_NAME --node-osdisk-type Ephemeral
```


Important

The DiskEncryptionSet we previously applied to the storage class only encrypts new PVCs. Encrypting existing PVCs requires detaching first before using the Azure Disks API/CLI to update the underlying disks, as shown in [this related guide](/en-us/azure/virtual-machines/linux/disks-enable-customer-managed-keys-cli#encrypt-existing-managed-disks).

## Encrypt your AKS cluster data disk

If you have already provided a disk encryption set during cluster creation, encrypting data disks with the same disk encryption set is the default option. Therefore, this step is optional. However, if you want to encrypt data disks with a different disk encryption set, you can follow these steps.

Important

Ensure you have the proper AKS credentials. The managed identity needs to have contributor access to the resource group where the diskencryptionset is deployed. Otherwise, you'll get an error suggesting that the managed identity does not have permissions.

To assign the AKS cluster identity the Contributor role for the diskencryptionset, execute the following commands:

```
aksIdentity=$(az aks show --resource-group $RG_NAME --name $CLUSTER_NAME --query "identity.principalId")
az role assignment create --role "Contributor" --assignee $aksIdentity --scope $diskEncryptionSetId
```


Create a file called **byok-azure-disk.yaml** that contains the following information. Replace *myAzureSubscriptionId*, *myResourceGroup*, and *myDiskEncrptionSetName* with your values, and apply the yaml. Make sure to use the resource group where your DiskEncryptionSet is deployed.

```
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
name: byok
provisioner: disk.csi.azure.com # replace with "kubernetes.io/azure-disk" if aks version is less than 1.21
parameters:
skuname: StandardSSD_LRS
kind: managed
diskEncryptionSetID: "/subscriptions/{myAzureSubscriptionId}/resourceGroups/{myResourceGroup}/providers/Microsoft.Compute/diskEncryptionSets/{myDiskEncryptionSetName}"
```


Next, run the following commands to update your AKS cluster:

```
# Get credentials
az aks get-credentials --name myAksCluster --resource-group myResourceGroup --output table
# Update cluster
kubectl apply -f byok-azure-disk.yaml
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-node-pools -->

# Configure node pools for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure node pools for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS), including SKU selectors, resource limits, and priority weights. It also provides examples to help you get started.

## Overview of node pools in NAP

NAP uses virtual machine (VM) SKU requirements to decide the best VMs for pending workloads. You can configure:

- SKU families and specific instance types.
- Resource limits and priorities.
- Spot or On-demand instances.
- Architecture and capabilities requirements.

The `NodePool`

resource sets constraints on the nodes that NAP creates and the pods that run on those nodes. When you first install NAP, it creates a [default NodePool](#review-default-node-pool-configuration). You can modify this node pool or create extra node pools to suit your workload requirements.

## Key behaviors of `NodePools`

in NAP

When configuring `NodePools`

for NAP, keep the following behaviors in mind:

- NAP requires at least one
`NodePool`

to function. - NAP evaluates each configured
`NodePool`

. - NAP skips
`NodePools`

with taints not tolerated by a pod. - NAP applies startup taints to provisioned nodes but doesn't require pod toleration.
- NAP works best with mutually exclusive
`NodePools`

. When multiple`NodePools`

match, it uses the one with highest weight.

## Review default node pool configuration

The configuration of the default [Karpenter NodePool](https://karpenter.sh/docs/concepts/nodepools/) named

`default`

created by NAP is as follows:```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
disruption:
consolidationPolicy: WhenEmptyOrUnderutilized
template:
spec:
nodeClassRef:
name: default
expireAfter: Never
# Requirements that constrain the parameters of provisioned nodes.
# These requirements are combined with pod.spec.affinity.nodeAffinity rules.
# Operators { In, NotIn, Exists, DoesNotExist, Gt, and Lt } are supported.
# https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#operators
requirements:
- key: kubernetes.io/arch
operator: In
values:
- amd64
- key: kubernetes.io/os
operator: In
values:
- linux
- key: karpenter.sh/capacity-type
operator: In
values:
- on-demand
- key: karpenter.azure.com/sku-family
operator: In
values:
- D
```


It also creates a `system-surge`

node pool, which helps to autoscale system pool nodes.

## Control configuration of default node pool during cluster creation

When you [create a new AKS cluster enabled with NAP using the Azure CLI](use-node-auto-provisioning#enable-nap-on-a-new-cluster), you can include the `--node-provisioning-default-pools`

flag to control the configuration of the default NAP `NodePool`

.

The `--node-provisioning-default-pools`

flag controls the default NAP `NodePool`

configuration and accepts the following values:

(default): Creates two standard`Auto`

`NodePools`

for immediate use.: Doesn't create any`None`

`NodePools`

. You must define your own.

Warning

**Changing from Auto to None**: If you change the setting from


`Auto`

to `None`

on an existing cluster, the default `NodePools`

aren't deleted automatically. You must delete them manually if you no longer need them.## Node pool configuration options

The following sections outline various configuration options for `NodePools`

in NAP, including [well-known labels and SKU selectors](#well-known-labels-and-sku-selectors), [node pool limits](#node-pool-limits), and [node pool weights](#node-pool-weights).

### Well-known labels and SKU selectors

Kubernetes defines [well-known labels](https://kubernetes.io/docs/reference/labels-annotations-taints/) that Azure implements. You can define these labels in the `spec.requirements`

section of the `NodePool`

API. NAP also supports Azure-specific labels for more advanced scheduling.

`karpenter.azure.com`

SKU selectors

The following table lists the `karpenter.azure.com`

SKU selectors you can use in the `spec.requirements`

section of your `NodePool`

API to define VM characteristics for your nodes:

| Selector | Description | Example |
|---|---|---|
`karpenter.azure.com/sku-family` |
VM SKU family | D, F, L, etc. |
`karpenter.azure.com/sku-name` |
Explicit SKU name | Standard_A1_v2 |
`karpenter.azure.com/sku-version` |
SKU version (without "v", can use 1) | 1, 2 |
`karpenter.sh/capacity-type` |
VM allocation type (Spot / On-demand) | Spot |
`karpenter.azure.com/sku-cpu` |
Number of CPUs in VM | 16 |
`karpenter.azure.com/sku-memory` |
Memory in VM in MiB | 131072 |
`kubernetes.azure.com/sku-cpu` |
Number of CPUs in VM | 16 |
`kubernetes.azure.com/sku-memory` |
Memory in VM in MiB | 131072 |
`karpenter.azure.com/sku-gpu-name` |
GPU name | A100 |
`karpenter.azure.com/sku-gpu-manufacturer` |
GPU manufacturer | nvidia |
`karpenter.azure.com/sku-gpu-count` |
GPU count per VM | 2 |
`karpenter.azure.com/sku-networking-accelerated` |
Whether the VM has accelerated networking | [true, false] |
`karpenter.azure.com/sku-storage-premium-capable` |
Whether the VM supports Premium IO storage | [true, false] |
`karpenter.azure.com/sku-storage-ephemeralos-maxsize` |
Size limit for the Ephemeral operating system (OS) disk in Gb | 92 |

`kubernetes.io`

well-known labels

The following table lists the `kubernetes.io`

well-known labels you can use in the `spec.requirements`

section of your `NodePool`

API to define node characteristics for your nodes:

| Label | Description | Example |
|---|---|---|
`topology.kubernetes.io/zone` |
Availability zone(s) | [uksouth-1,uksouth-2,uksouth-3] |
`kubernetes.io/os` |
Operating system | linux |
`kubernetes.io/arch` |
CPU architecture (AMD64 or ARM64) | [amd64, arm64] |

#### SKU family examples

The `karpenter.azure.com/sku-family`

selector allows you to target specific VM families.

| Family | Description |
|---|---|
| D-series | General-purpose VMs with balanced CPU-to-memory ratio |
| F-series | Compute-optimized VMs with high CPU-to-memory ratio |
| E-series | Memory-optimized VMs for memory-intensive applications |
| L-series | Storage-optimized VMs with high disk throughput |
| N-series | GPU-enabled VMs for compute-intensive workloads |

Example configuration using SKU family:

```
requirements:
- key: karpenter.azure.com/sku-family
operator: In
values:
- D
- F
```


#### SKU name examples

The `karpenter.azure.com/sku-name`

selector allows you to specify the exact VM instance type.

```
requirements:
- key: karpenter.azure.com/sku-name
operator: In
values:
- Standard_D4s_v3
- Standard_F8s_v2
```


#### SKU version examples

The `karpenter.azure.com/sku-version`

selector targets specific generations of VM SKUs.

```
requirements:
- key: karpenter.azure.com/sku-version
operator: In
values:
- "3" # v3 generation
- "5" # v5 generation
```


#### Availability zone example

The `topology.kubernetes.io/zone`

selector allows you to specify the availability zones for your nodes.

```
requirements:
- key: topology.kubernetes.io/zone
operator: In
values:
- eastus-1
- eastus-2
```


Note

You can find available zones for your region using the `az account list-locations --output table`

Azure CLI command.

#### Architecture example

The `kubernetes.io/arch`

selector allows you to specify the CPU architecture for your nodes. NAP supports both `amd64`

and `arm64`

nodes.

```
requirements:
- key: kubernetes.io/arch
operator: In
values:
- amd64
- arm64
```


#### OS example

The `kubernetes.io/os`

selector allows you to specify the operating system for your nodes.

```
requirements:
- key: kubernetes.io/os
operator: In
values:
- linux
```


#### Capacity type example

The `karpenter.sh/capacity-type`

selector allows you to specify whether to use Spot or On-demand instances.

Note

NAP prioritizes Spot instances when both Spot and On-demand are specified.

```
requirements:
- key: karpenter.sh/capacity-type
operator: In
values:
- spot
- on-demand
```


### Node pool limits

By default, NAP attempts to schedule your workloads within the Azure quota you have available. You can also specify the upper limit of resources that a node pool uses by specifying limits within the node pool spec. For example:

```
spec:
# Resource limits constrain the total size of the cluster.
# Limits prevent Node Auto Provisioning from creating new instances once the limit is exceeded.
limits:
cpu: "1000"
memory: 1000Gi
```


### Node pool weights

When you have multiple node pools defined, you can set a preference of where a workload should be scheduled by defining the relative weight in your node pool definitions. For example:

```
spec:
# Priority given to the node pool when the scheduler considers which to select.
# Higher weights indicate higher priority when comparing node pools.
# Specifying no weight is equivalent to specifying a weight of 0.
weight: 10
```


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-virtual-machine-sizes -->

# Virtual machine (VM) sizes, generations, and features for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) supports various virtual machine (VM) sizes, generations, and features to accommodate different workloads and performance requirements. This article provides an overview of available VM sizes and generations for AKS, how to check for available VM sizes in your region, reasons why certain VM sizes might not be available, and what happens when a VM size retires.

## VM support on AKS

Azure supports both Generation 1 (Gen 1) and [Generation 2 (Gen 2) virtual machines (VMs)](/en-us/azure/virtual-machines/generation-2). With some [exceptions](/en-us/windows-server/virtualization/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v), we generally recommend [migrating to Generation 2 VMs](#gen-2-vms-on-aks) to take advantage of the newest features and functionalities in Azure VMs.

The VM size and operating system (OS) you select when creating an AKS node pool determines the VM generation and [node image](node-images) used. Check the [list of supported sizes](/en-us/azure/virtual-machines/generation-2#generation-2-vm-sizes) to see if your SKU supports or requires Gen 2.

### Limitations

There are some limitations to take into account when choosing a VM generation and/or OS:

- Trusted Launch can only be enabled on VM sizes that support Gen 2.
- Confidential VM sizes always use Gen 2 on AKS.
- Arm64 VM sizes always use Gen 2 on AKS.
- Windows Server 2019 node pools don't support Gen 2 VM sizes.
- Windows Server 2022 node pools require use of a custom header to use Gen 2.

To use Gen 2 VMs on AKS, see [Use Gen 2 VMs](#gen-2-vms-on-aks).

## Available VM features

AKS supports various VM features that enhance security, performance, and functionality. Some key features include:

uses pending pod resource requirements to decide the optimal VM configuration to run your workloads efficiently and cost-effectively.**Node autoprovisioning (NAP)**provide a better experience for dynamic workloads and high availability requirements. Virtual Machines node pools enable you to set up multiple similar-family VMs in a single node pool. Your workloads are automatically scheduled on the available resources you configure.**Virtual Machines node pools**

## Supported VM sizes

For in-depth information about VM sizes available in Azure, see [Azure VM sizes](/en-us/azure/virtual-machines/sizes/overview?tabs=breakdownseries%2Cgeneralsizelist%2Ccomputesizelist%2Cmemorysizelist%2Cstoragesizelist%2Cgpusizelist%2Cfpgasizelist%2Chpcsizelist). To view supported Gen 2 VM sizes, see [Generation 2 VM sizes](/en-us/azure/virtual-machines/generation-2).

AKS also supports the following VM types and features:

[Confidential VMs (CVMs)](use-cvm)[Arm-based processor (Arm64) VMs](use-arm64-vms)[GPU-optimized VMs](/en-us/azure/virtual-machines/sizes/overview?tabs=breakdownseries%2Cgeneralsizelist%2Ccomputesizelist%2Cmemorysizelist%2Cstoragesizelist%2Cgpusizelist%2Cfpgasizelist%2Chpcsizelist#gpu-accelerated)[Trusted Launch](use-trusted-launch)[Federal Information Process Standard (FIPS)](enable-fips-nodes)

### Default behavior for supported VM sizes

There are three scenarios when creating a node pool with a supported VM size:

- If the VM size supports only Gen 1, the default behavior for both Linux and Windows node pools is to use the Gen 1 node image.
- If the VM size supports only Gen 2, the default behavior for both Linux and Windows node pools is to use the Gen 2 node image. Windows Server 2022 node pools require a custom header to use a VM size that only supports Gen 2. For more information, see
[Create a Windows node pool with a Gen 2 VM](generation-2-vms#create-a-node-pool-with-a-gen-2-vm). - If the VM size supports both Gen 1 and Gen 2, the default behavior for both Linux and Windows (in Windows Server 2025+) nodes pools is to use the Gen 2 node image. To use the Gen 2 node image for Windows Server 2022, see
[Create a Windows node pool with a Gen 2 VM](generation-2-vms#create-a-node-pool-with-a-gen-2-vm).

## Check available VM sizes

Check available VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm#az-vm-list-skus) command.

```
az vm list-skus --location <your-location> --output table
```


## Why certain VM sizes might not be available

There are several reasons why certain VM sizes might not be available, including:

**Quota limits**: All Azure services set default limits and quotas for resources and features. For more information, see the following resources:[Quotas and regional limits for Azure Kubernetes Service (AKS)](quotas-skus-regions)[Check your quota usage](/en-us/azure/virtual-machines/quotas)[Request a quota increase through an Azure support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest)(for**Issue type**, select**Quota**)

Note

- For
, VM sizes with**user node pools***fewer than two vCPUs and two GBs of memory (RAM)*might not be used by default. - For
, VM sizes with**system node pools***fewer than two vCPUs and four GBs of memory (RAM)*might not be used by default. To ensure that you can reliably schedule the required`kube-system`

pods and your applications, we recommend that you**do not use any**.[B series VMs](/en-us/azure/virtual-machines/sizes/general-purpose/bv1-series)or[Av1 series VMs](/en-us/azure/virtual-machines/sizes/retirement/av1-series-retirement)

**VM sizes in preview**: VM sizes in preview might not be available to you if you haven't registered the preview flag for the VM size.**Blocked by AKS**: Some VM sizes might not be available by default in AKS. These sizes might require extra testing or validation to ensure compatibility with AKS. If you need a specific VM size that isn't available to you, you can[submit a GitHub issue request](https://github.com/Azure/AKS/issues).

Make sure you understand which features your workloads need and choose a VM size that meets those requirements. Later VM versions typically have better performance and improved features. For example, [Gen 2 VMs](#gen-2-vms-on-aks) have increased security and performance benefits over Gen 1 VMs.

## What happens when a VM size retires?

When a VM size or series reaches its retirement date, the VM is deallocated. VM deallocation causes your AKS node pools to break. To check the retirement status of a VM size, see [Retired Azure VM size series](/en-us/azure/virtual-machines/sizes/retirement/retired-sizes-list) or perform a search in [Azure Updates](https://azure.microsoft.com/updates). To check the VM size of your node pools, use the [`az aks nodepool list`

][az-aks-nodepool-list] command and query for the `vmSize`

property:

```
az aks nodepool list --resource-group <your-resource-group> --cluster-name <your-cluster-name> --query "[].{Name:name, VMSize:vmSize}" --output table
```


If you're using a VM size that's retiring/retired, we recommend [migrating your node pools to a supported VM size](#migrate-node-pools-to-a-supported-vm-size) to prevent any potential disruption to your service. Currently, AKS *doesn't support* transitioning to a new VM size within the same node pool.

## Migrate node pools to a supported VM size

Once you determine the appropriate node pools to take action on, you can [resize your node pools](resize-node-pool). During the resizing process, a new node pool is created and workloads are migrated to the new node pool.

For more information on migrating to a new VM size, see the following resources:

[Migrate from Gen 1 to Gen 2 VMs](#gen-2-vms-on-aks)[General-purpose sizes migration guide](/en-us/azure/virtual-machines/migration/sizes/d-ds-dv2-dsv2-ls-series-migration-guide)[Storage-optimized sizes migration guide](/en-us/azure/virtual-machines/migration/sizes/d-ds-dv2-dsv2-ls-series-migration-guide)[GPU-accelerated sizes migration guide](/en-us/azure/virtual-machines/migration/sizes/n-series-migration)[Azure Dedicated Host SKU migration guide](/en-us/azure/virtual-machines/migration/dedicated-host-migration-guide)

## Gen 2 VMs on AKS

Gen 2 VMs are generally Azure's newer offerings and have exclusive features over Gen 1 VMs like increased memory, improved CPU performance, support for NVMe disks, and support for [Trusted Launch](use-trusted-launch).

While we generally recommend running Gen 2 VMs, you should make sure that the generation you choose supports your requirements. To learn more about the differences between generations, and when one might make more sense than the other, see [Should I create a Gen 1 or 2 VM in Hyper-V?](/en-us/windows-server/virtualization/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)

To use Gen 2 VMs on AKS, see [Use generation 2 VMs on AKS](generation-2-vms).

## Next steps

- To learn more about Gen 2 VMs, see
[Support for Generation 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2) - To learn more about supported Gen 2 node images, see
[Node images](node-images)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/devops-pipeline -->

# Build and deploy to Azure Kubernetes Service with Azure Pipelines

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Azure DevOps Services**

Use [Azure Pipelines](/en-us/azure/devops/pipelines/) to automatically deploy to Azure Kubernetes Service (AKS). Azure Pipelines lets you build, test, and deploy with continuous integration (CI) and continuous delivery (CD) using [Azure DevOps](/en-us/azure/devops/).

In this article, you'll learn how to create a pipeline that continuously builds and deploys your app. Every time you change your code in a repository that contains a Dockerfile, the images are pushed to your Azure Container Registry, and the manifests are then deployed to your AKS cluster.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - An Azure Resource Manager service connection.
[Create an Azure Resource Manager service connection](/en-us/azure/devops/pipelines/library/connect-to-azure#create-an-azure-resource-manager-service-connection-using-automated-security). - A GitHub account. Create a free
[GitHub account](https://github.com/join)if you don't have one already.

## Get the code

Fork the following repository containing a sample application and a Dockerfile:

```
https://github.com/MicrosoftDocs/pipelines-javascript-docker
```


## Create the Azure resources

Sign in to the [Azure portal](https://portal.azure.com/), and then select the [Cloud Shell](/en-us/azure/cloud-shell/overview) button in the upper-right corner. Use Azure CLI or PowerShell to create an AKS cluster.

### Create a container registry

```
# Create a resource group
az group create --name myapp-rg --location eastus
# Create a container registry
az acr create --resource-group myapp-rg --name mycontainerregistry --sku Basic
# Create a Kubernetes cluster
az aks create \
--resource-group myapp-rg \
--name myapp \
--node-count 1 \
--enable-addons monitoring \
--generate-ssh-keys
```


## Sign in to Azure Pipelines

Sign in to [Azure Pipelines](https://azure.microsoft.com/services/devops/pipelines). After you sign in, your browser goes to `https://dev.azure.com/my-organization-name`

and displays your Azure DevOps dashboard.

Within your selected organization, create a *project*. If you don't have any projects in your organization, you see a **Create a project to get started** screen. Otherwise, select the **Create Project** button in the upper-right corner of the dashboard.

## Create the pipeline

### Connect and select your repository

Sign in to your Azure DevOps organization and go to your project.

Go to

**Pipelines**, and then select**New pipeline**.Do the steps of the wizard by first selecting

**GitHub**as the location of your source code.You might be redirected to GitHub to sign in. If so, enter your GitHub credentials.

When you see the list of repositories, select your repository.

You might be redirected to GitHub to install the Azure Pipelines app. If so, select

**Approve & install**.Select

**Deploy to Azure Kubernetes Service**.If you're prompted, select the subscription in which you created your registry and cluster.

Select the

`myapp`

cluster.For

**Namespace**, select**Existing**, and then select**default**.Select the name of your container registry.

You can leave the image name set to the default.

Set the service port to 8080.

Set the

**Enable Review App for Pull Requests**checkbox for[review app](/en-us/azure/devops/pipelines/process/environments-kubernetes)related configuration to be included in the pipeline YAML autogenerated in subsequent steps.Select

**Validate and configure**.As Azure Pipelines creates your pipeline, the process will:

Create a

*Docker registry service connection*to enable your pipeline to push images into your container registry.Create an

*environment*and a Kubernetes resource within the environment. For an RBAC-enabled cluster, the created Kubernetes resource implicitly creates ServiceAccount and RoleBinding objects in the cluster so that the created ServiceAccount can't perform operations outside the chosen namespace.Generate an

*azure-pipelines.yml*file, which defines your pipeline.Generate Kubernetes manifest files. These files are generated by hydrating the

[deployment.yml](https://github.com/Microsoft/azure-pipelines-yaml/blob/master/templates/resources/k8s/deployment.yml)and[service.yml](https://github.com/Microsoft/azure-pipelines-yaml/blob/master/templates/resources/k8s/service.yml)templates based on selections you made. When you're ready, select**Save and run**.

Select

**Save and run**.You can change the

**Commit message**to something like*Add pipeline to our repository*. When you're ready, select**Save and run**to commit the new pipeline into your repo, and then begin the first run of your new pipeline!

## See your app deploy

As your pipeline runs, watch as your build stage, and then your deployment stage, go from blue (running) to green (completed). You can select the stages and jobs to watch your pipeline in action.

Note

If you're using a Microsoft-hosted agent, you must add the IP range of the Microsoft-hosted agent to your firewall. Get the weekly list of IP ranges from the [weekly JSON file](https://www.microsoft.com/download/details.aspx?id=56519), which is published every Wednesday. The new IP ranges become effective the following Monday. For more information, see [Microsoft-hosted agents](/en-us/azure/devops/pipelines/agents/hosted?tabs=yaml&view=azure-devops&preserve-view=true#networking).
To find the IP ranges that are required for your Azure DevOps organization, learn how to [identify the possible IP ranges for Microsoft-hosted agents](/en-us/azure/devops/pipelines/agents/hosted?tabs=yaml&view=azure-devops&preserve-view=true#to-identify-the-possible-ip-ranges-for-microsoft-hosted-agents).

After the pipeline run is finished, explore what happened and then go see your app deployed. From the pipeline summary:

Select the

**Environments**tab.Select

**View environment**.Select the instance of your app for the namespace you deployed to. If you used the defaults, then it is the

**myapp**app in the**default**namespace.Select the

**Services**tab.Select and copy the external IP address to your clipboard.

Open a new browser tab or window and enter <IP address>:8080.


If you're building our sample app, then *Hello world* appears in your browser.

## How the pipeline builds

When you finished selecting options and then proceeded to validate and configure the pipeline Azure Pipelines created a pipeline for you, using the *Deploy to Azure Kubernetes Service* template.

The build stage uses the [Docker task](/en-us/azure/devops/pipelines/tasks/build/docker) to build and push the image to the Azure Container Registry.

```
- stage: Build
displayName: Build stage
jobs:
- job: Build
displayName: Build job
pool:
vmImage: $(vmImageName)
steps:
- task: Docker@2
displayName: Build and push an image to container registry
inputs:
command: buildAndPush
repository: $(imageRepository)
dockerfile: $(dockerfilePath)
containerRegistry: $(dockerRegistryServiceConnection)
tags: |
$(tag)
- task: PublishPipelineArtifact@1
inputs:
artifactName: 'manifests'
path: 'manifests'
```


The deployment job uses the *Kubernetes manifest task* to create the `imagePullSecret`

required by Kubernetes cluster nodes to pull from the Azure Container Registry resource. Manifest files are then used by the Kubernetes manifest task to deploy to the Kubernetes cluster. The manifest files, `service.yml`

and `deployment.yml`

, were generated when you used the **Deploy to Azure Kubernetes Service** template.

```
- stage: Deploy
displayName: Deploy stage
dependsOn: Build
jobs:
- deployment: Deploy
displayName: Deploy job
pool:
vmImage: $(vmImageName)
environment: 'myenv.aksnamespace' #customize with your environment
strategy:
runOnce:
deploy:
steps:
- task: DownloadPipelineArtifact@2
inputs:
artifactName: 'manifests'
downloadPath: '$(System.ArtifactsDirectory)/manifests'
- task: KubernetesManifest@1
displayName: Create imagePullSecret
inputs:
action: 'createSecret'
connectionType: 'kubernetesServiceConnection'
kubernetesServiceConnection: 'myapp-default' #customize for your Kubernetes service connection
secretType: 'dockerRegistry'
secretName: '$(imagePullSecret)'
dockerRegistryEndpoint: '$(dockerRegistryServiceConnection)'
- task: KubernetesManifest@1
displayName: Deploy to Kubernetes cluster
inputs:
action: 'deploy'
connectionType: 'kubernetesServiceConnection'
kubernetesServiceConnection: 'myapp-default' #customize for your Kubernetes service connection
manifests: |
$(Pipeline.Workspace)/manifests/deployment.yml
$(Pipeline.Workspace)/manifests/service.yml
containers: '$(containerRegistry)/$(imageRepository):$(tag)'
imagePullSecrets: '$(imagePullSecret)'
```


## Clean up resources

Whenever you're done with the resources you created, you can use the following command to delete them:

```
az group delete --name myapp-rg
```


Enter `y`

when you're prompted.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-postgresql-ha -->

# Deploy a highly available PostgreSQL database on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you deploy a highly available PostgreSQL database on AKS.

- If you still need to create the required infrastructure for this deployment, follow the steps in
[Create infrastructure for deploying a highly available PostgreSQL database on AKS](create-postgresql-ha)to get set up, and then return to this article.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Create secret for bootstrap app user

- Generate a secret to validate the PostgreSQL deployment by interactive login for a bootstrap app user using the
command.`kubectl create secret`


Important

Microsoft recommends that you use the most secure authentication flow available. The authentication flow described in this procedure requires a high degree of trust in the application and carries risks that are not present in other flows. You should only use this flow when other more secure flows, such as managed identities, aren't viable.

```
PG_DATABASE_APPUSER_SECRET=$(echo -n | openssl rand -base64 16)
kubectl create secret generic db-user-pass \
--from-literal=username=app \
--from-literal=password="${PG_DATABASE_APPUSER_SECRET}" \
--namespace $PG_NAMESPACE \
--context $AKS_PRIMARY_CLUSTER_NAME
```


Validate that the secret was successfully created using the

command.`kubectl get`

`kubectl get secret db-user-pass --namespace $PG_NAMESPACE --context $AKS_PRIMARY_CLUSTER_NAME`


## Set environment variables for the PostgreSQL cluster

Deploy a ConfigMap to configure the CNPG operator using the following

command. These values replace the legacy`kubectl apply`

`ENABLE_AZURE_PVC_UPDATES`

toggle, which is no longer required, and help stagger upgrades and speed up replica reconnections. Before rolling this configuration into production, validate that any existing`DRAIN_TAINTS`

settings you rely on remain compatible with your Azure environment.`cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME -n $PG_NAMESPACE -f - apiVersion: v1 kind: ConfigMap metadata: name: cnpg-controller-manager-config data: CLUSTERS_ROLLOUT_DELAY: '120' STANDBY_TCP_USER_TIMEOUT: '10' EOF`


## Install the Prometheus PodMonitors

Prometheus scrapes CNPG using the recording rules stored in the CNPG GitHub samples repo. Because the operator-managed PodMonitor is being deprecated, create and manage the PodMonitor resource yourself so you can tailor it to your monitoring stack.

Add the Prometheus Community Helm repo using the

command.`helm repo add`

`helm repo add prometheus-community \ https://prometheus-community.github.io/helm-charts`

Upgrade the Prometheus Community Helm repo and install it on the primary cluster using the

command with the`helm upgrade`

`--install`

flag.`helm upgrade --install \ --namespace $PG_NAMESPACE \ -f https://raw.githubusercontent.com/cloudnative-pg/cloudnative-pg/main/docs/src/samples/monitoring/kube-stack-config.yaml \ prometheus-community \ prometheus-community/kube-prometheus-stack \ --kube-context=$AKS_PRIMARY_CLUSTER_NAME`

Create a PodMonitor for the cluster. The CNPG team is deprecating the operator-managed PodMonitor, so you now manage it directly:

`cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -f - apiVersion: monitoring.coreos.com/v1 kind: PodMonitor metadata: name: $PG_PRIMARY_CLUSTER_NAME namespace: ${PG_NAMESPACE} labels: cnpg.io/cluster: ${PG_PRIMARY_CLUSTER_NAME} spec: selector: matchLabels: cnpg.io/cluster: ${PG_PRIMARY_CLUSTER_NAME} podMetricsEndpoints: - port: metrics EOF`


## Create a federated credential

In this section, you create a federated identity credential for PostgreSQL backup to allow CNPG to use AKS workload identity to authenticate to the storage account destination for backups. The CNPG operator creates a Kubernetes service account with the same name as the cluster named used in the CNPG Cluster deployment manifest.

Get the OIDC issuer URL of the cluster using the

command.`az aks show`

`export AKS_PRIMARY_CLUSTER_OIDC_ISSUER="$(az aks show \ --name $AKS_PRIMARY_CLUSTER_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query "oidcIssuerProfile.issuerUrl" \ --output tsv)"`

Create a federated identity credential using the

command.`az identity federated-credential create`

`az identity federated-credential create \ --name $AKS_PRIMARY_CLUSTER_FED_CREDENTIAL_NAME \ --identity-name $AKS_UAMI_CLUSTER_IDENTITY_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --issuer "${AKS_PRIMARY_CLUSTER_OIDC_ISSUER}" \ --subject system:serviceaccount:"${PG_NAMESPACE}":"${PG_PRIMARY_CLUSTER_NAME}" \ --audience api://AzureADTokenExchange`


## Deploy a highly available PostgreSQL cluster

In this section, you deploy a highly available PostgreSQL cluster using the [CNPG Cluster custom resource definition (CRD)](https://cloudnative-pg.io/documentation/1.23/cloudnative-pg.v1/#postgresql-cnpg-io-v1-ClusterSpec).

### Cluster CRD parameters

The following table outlines the key properties set in the YAML deployment manifest for the Cluster CRD:

| Property | Definition |
|---|---|
`imageName` |
Points to the CloudNativePG operand container image. Use `ghcr.io/cloudnative-pg/postgresql:18-system-trixie` with the in-core backup integration shown in this guide, or switch to `18-standard-trixie` when you adopt the Barman Cloud plugin. |
`inheritedMetadata` |
Specific to the CNPG operator. The CNPG operator applies the metadata to every object related to the cluster. |
`annotations` |
Includes the DNS label required when exposing the cluster endpoints and enables
`alpha.cnpg.io/failoverQuorum` |

`labels: azure.workload.identity/use: "true"`

`topologySpreadConstraints`

`"workload=postgres"`

.`resources`

*Guaranteed*. In a production environment, these values are key for maximizing usage of the underlying node VM and vary based on the Azure VM SKU used.`probes`

`startDelay`

configuration. Streaming startup and readiness probes help ensure replicas are healthy before serving traffic.`smartShutdownTimeout`

`bootstrap`

`storage`

`postgresql.synchronous`

`minSyncReplicas`

/`maxSyncReplicas`

and lets you specify synchronous replication behavior using the newer schema.`postgresql.parameters`

`postgresql.conf`

, `pg_hba.conf`

, and `pg_ident.conf`

. The sample emphasizes observability and WAL retention defaults that suit the AKS workload identity scenario but should be tuned per workload.`serviceAccountTemplate`

`barmanObjectStore`

To further isolate PostgreSQL workloads, you can add a taint (for example, `node-role.kubernetes.io/postgres=:NoSchedule`

) to your data plane nodes and replace the sample `nodeSelector`

/`tolerations`

with the values recommended by CloudNativePG. If you take this approach, label the nodes accordingly and confirm the AKS autoscaler policies align with your topology.

### PostgreSQL performance parameters

PostgreSQL performance heavily depends on your cluster's underlying resources and workload. The following table provides baseline guidance for a three-node cluster running on Standard D4s v3 nodes (16-GiB memory). Treat these values as a starting point and adjust them once you understand your workload profile:

| Property | Recommended value | Definition |
|---|---|---|
`wal_compression` |
lz4 | Compresses full-page writes written in WAL file with specified method |
`max_wal_size` |
6 GB | Sets the WAL size that triggers a checkpoint |
`checkpoint_timeout` |
15 min | Sets the maximum time between automatic WAL checkpoints |
`checkpoint_completion_target` |
0.9 | Balances checkpoint work across the checkpoint window |
`checkpoint_flush_after` |
2 MB | Number of pages after which previously performed writes are flushed to disk |
`wal_writer_flush_after` |
2 MB | Amount of WAL written out by WAL writer that triggers a flush |
`min_wal_size` |
2 GB | Sets the minimum size to shrink the WAL to |
`max_slot_wal_keep_size` |
10 GB | Upper bound for WAL left to service replication slots |
`shared_buffers` |
4 GB | Sets the number of shared memory buffers used by the server (25% of node memory in this example) |
`effective_cache_size` |
12 GB | Sets the planner's assumption about the total size of the data caches |
`work_mem` |
1/256th of node memory | Sets the maximum memory to be used for query workspaces |
`maintenance_work_mem` |
6.25% of node memory | Sets the maximum memory to be used for maintenance operations |
`autovacuum_vacuum_cost_limit` |
2400 | Vacuum cost amount available before napping, for autovacuum |
`random_page_cost` |
1.1 | Sets the planner's estimate of the cost of a nonsequentially fetched disk page |
`effective_io_concurrency` |
64 | Sets how many simultaneous requests the disk subsystem can handle efficiently |
`maintenance_io_concurrency` |
64 | A variant of "effective_io_concurrency" that is used for maintenance work |

### Deploying PostgreSQL

Deploy the PostgreSQL cluster with the Cluster CRD using the

command.`kubectl apply`

`cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME -n $PG_NAMESPACE -v 9 -f - apiVersion: postgresql.cnpg.io/v1 kind: Cluster metadata: name: $PG_PRIMARY_CLUSTER_NAME annotations: alpha.cnpg.io/failoverQuorum: "true" spec: imageName: ghcr.io/cloudnative-pg/postgresql:18-system-trixie inheritedMetadata: annotations: service.beta.kubernetes.io/azure-dns-label-name: $AKS_PRIMARY_CLUSTER_PG_DNSPREFIX labels: azure.workload.identity/use: "true" instances: 3 smartShutdownTimeout: 30 probes: startup: type: streaming maximumLag: 32Mi periodSeconds: 5 timeoutSeconds: 3 failureThreshold: 120 readiness: type: streaming maximumLag: 0 periodSeconds: 10 failureThreshold: 6 topologySpreadConstraints: - maxSkew: 1 topologyKey: topology.kubernetes.io/zone whenUnsatisfiable: DoNotSchedule labelSelector: matchLabels: cnpg.io/cluster: $PG_PRIMARY_CLUSTER_NAME affinity: nodeSelector: workload: postgres resources: requests: memory: '8Gi' cpu: 2 limits: memory: '8Gi' cpu: 2 bootstrap: initdb: database: appdb owner: app secret: name: db-user-pass dataChecksums: true storage: storageClass: $POSTGRES_STORAGE_CLASS size: 64Gi postgresql: synchronous: method: any number: 1 parameters: wal_compression: lz4 max_wal_size: 6GB max_slot_wal_keep_size: 10GB checkpoint_timeout: 15min checkpoint_completion_target: '0.9' checkpoint_flush_after: 2MB wal_writer_flush_after: 2MB min_wal_size: 2GB shared_buffers: 4GB effective_cache_size: 12GB work_mem: 62MB maintenance_work_mem: 1GB autovacuum_vacuum_cost_limit: "2400" random_page_cost: "1.1" effective_io_concurrency: "64" maintenance_io_concurrency: "64" log_checkpoints: 'on' log_lock_waits: 'on' log_min_duration_statement: '1000' log_statement: 'ddl' log_temp_files: '1024' log_autovacuum_min_duration: '1s' pg_stat_statements.max: '10000' pg_stat_statements.track: 'all' hot_standby_feedback: 'on' pg_hba: - host all all all scram-sha-256 serviceAccountTemplate: metadata: annotations: azure.workload.identity/client-id: "$AKS_UAMI_WORKLOAD_CLIENTID" labels: azure.workload.identity/use: "true" backup: barmanObjectStore: destinationPath: "https://${PG_PRIMARY_STORAGE_ACCOUNT_NAME}.blob.core.windows.net/backups" azureCredentials: inheritFromAzureAD: true retentionPolicy: '7d' EOF`


Note

The sample manifest uses the `ghcr.io/cloudnative-pg/postgresql:18-system-trixie`

image because it works with the in-core Barman Cloud integration shown later. When you're ready to switch to the Barman Cloud plugin, update `spec.imageName`

to `ghcr.io/cloudnative-pg/postgresql:18-standard-trixie`

and follow the [plugin configuration guidance](https://cloudnative-pg.io/plugin-barman-cloud/docs/intro/) before redeploying the cluster.

Important

The example `pg_hba`

entry allows non-TLS access. If you keep this configuration, document the security implications for your team and prefer encrypted connections wherever possible.

Validate that the primary PostgreSQL cluster was successfully created using the

command. The CNPG Cluster CRD specified three instances, which can be validated by viewing running pods once each instance is brought up and joined for replication. Be patient as it can take some time for all three instances to come online and join the cluster.`kubectl get`

`kubectl get pods --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -l cnpg.io/cluster=$PG_PRIMARY_CLUSTER_NAME`

Example output

`NAME READY STATUS RESTARTS AGE pg-primary-cnpg-r8c7unrw-1 1/1 Running 0 4m25s pg-primary-cnpg-r8c7unrw-2 1/1 Running 0 3m33s pg-primary-cnpg-r8c7unrw-3 1/1 Running 0 2m49s`


Important

If you use local NVMe with Azure Container Storage and a pod remains in the init state with a multi-attach error, the pod is still searching for the volume on a lost node. After the pod starts running, it enters a `CrashLoopBackOff`

state because CNPG creates a new replica on a new node without data and can't find the `pgdata`

directory. To resolve this issue, destroy the affected instance and bring up a new one. Run the following command:

```
kubectl cnpg destroy [cnpg-cluster-name] [instance-number]
```


## Validate the Prometheus PodMonitor is running

The manually created PodMonitor ties the kube-prometheus-stack scrape configuration to the CNPG pods you deployed earlier.

Validate the PodMonitor is running using the [ kubectl get](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_get/) command.

```
kubectl --namespace $PG_NAMESPACE \
--context $AKS_PRIMARY_CLUSTER_NAME \
get podmonitors.monitoring.coreos.com \
$PG_PRIMARY_CLUSTER_NAME \
--output yaml
```


Example output

```
kind: PodMonitor
metadata:
labels:
cnpg.io/cluster: pg-primary-cnpg-r8c7unrw
name: pg-primary-cnpg-r8c7unrw
namespace: cnpg-database
spec:
podMetricsEndpoints:
- port: metrics
selector:
matchLabels:
cnpg.io/cluster: pg-primary-cnpg-r8c7unrw
```


If you're using Azure Monitor for Managed Prometheus, you need to add another pod monitor using the custom group name. Managed Prometheus doesn't pick up the custom resource definitions (CRDs) from the Prometheus community. Aside from the group name, the CRDs are the same. That design lets pod monitors for Managed Prometheus run alongside pod monitors that use the community CRD. If you're not using Managed Prometheus, you can skip this section. Create a new pod monitor:

```
cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -f -
apiVersion: azmonitoring.coreos.com/v1
kind: PodMonitor
metadata:
name: cnpg-cluster-metrics-managed-prometheus
namespace: ${PG_NAMESPACE}
labels:
azure.workload.identity/use: "true"
cnpg.io/cluster: ${PG_PRIMARY_CLUSTER_NAME}
spec:
selector:
matchLabels:
azure.workload.identity/use: "true"
cnpg.io/cluster: ${PG_PRIMARY_CLUSTER_NAME}
podMetricsEndpoints:
- port: metrics
EOF
```


Verify that the pod monitor is created (note the difference in the group name).

```
kubectl --namespace $PG_NAMESPACE \
--context $AKS_PRIMARY_CLUSTER_NAME \
get podmonitors.azmonitoring.coreos.com \
-l cnpg.io/cluster=$PG_PRIMARY_CLUSTER_NAME \
-o yaml
```


### Option A - Azure Monitor workspace

After you deploy the Postgres cluster and the pod monitor, you can view the metrics using the Azure portal in an Azure Monitor workspace.

### Option B - Managed Grafana

Alternatively, after you deploy the Postgres cluster and pod monitors, you can create a metrics dashboard on the Managed Grafana instance created by the deployment script to visualize the metrics exported to the Azure Monitor workspace. You can access the Managed Grafana via the Azure portal. Navigate to the Managed Grafana instance created by the deployment script and select the Endpoint link as shown here:

Selecting the Endpoint link opens a new browser window where you can create dashboards on the Managed Grafana instance. Following the instructions to [configure an Azure Monitor data source](/en-us/azure/azure-monitor/visualize/grafana-plugin#configure-an-azure-monitor-data-source-plug-in), you can then add visualizations to create a dashboard of metrics from the Postgres cluster. After setting up the data source connection, from the main menu, select the Data sources option. You should see a set of data source options for the data source connection as shown here:

On the Managed Prometheus option, select the option to build a dashboard to open the dashboard editor. After the editor window opens, select the Add visualization option then select the Managed Prometheus option to browse the metrics from the Postgres cluster. After you select the metric you want to visualize, select the Run queries button to fetch the data for the visualization as shown here:

Select the Save icon to add the panel to your dashboard. You can add other panels by selecting the Add button in the dashboard editor and repeating this process to visualize other metrics. Adding the metrics visualizations, you should have something that looks like this:

Select the Save icon to save your dashboard.

## Next steps

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Ken Kilty | Principal TPM
- Russell de Pina | Principal TPM
- Adrian Joian | Senior Customer Engineer
- Jenny Hayes | Senior Content Developer
- Carol Smith | Senior Content Developer
- Erin Schaffer | Content Developer 2
- Adam Sharif | Customer Engineer 2

## Acknowledgment

This documentation was jointly developed with EnterpriseDB, the maintainers of the CloudNativePG operator. We thank [Gabriele Bartolini](https://cloudnative-pg.io/authors/gbartolini/) for reviewing earlier drafts of this document and offering technical improvements.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-cluster-security -->

# Best practices for cluster security and upgrades in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you manage clusters in Azure Kubernetes Service (AKS), workload and data security is a key consideration. When you run multi-tenant clusters using logical isolation, you especially need to secure resource and workload access. Minimize the risk of attack by applying the latest Kubernetes and node OS security updates.

This article focuses on how to secure your AKS cluster. You learn how to:

- Use Microsoft Entra ID and Kubernetes role-based access control (Kubernetes RBAC) to secure API server access.
- Secure container access to node resources.
- Upgrade an AKS cluster to the latest Kubernetes version.
- Keep nodes up to date and automatically apply security patches.

You can also read the best practices for [container image management](operator-best-practices-container-image-management) and for [pod security](developer-best-practices-pod-security).

## Enable threat protection


Best practice guidanceYou can enable

[Defender for Containers]to help secure your containers. Defender for Containers can assess cluster configurations and provide security recommendations, run vulnerability scans, and provide real-time protection and alerting for Kubernetes nodes and clusters.

## Secure access to the API server and cluster nodes


Best practice guidanceOne of the most important ways to secure your cluster is to secure access to the Kubernetes API server. To control access to the API server, integrate Kubernetes RBAC with Microsoft Entra ID. With these controls,you secure AKS the same way that you secure access to your Azure subscriptions.


The Kubernetes API server provides a single connection point for requests to perform actions within a cluster. To secure and audit access to the API server, limit access and provide the lowest possible permission levels. while this approach isn't unique to Kubernetes, it's especially important when you've logically isolated your AKS cluster for multi-tenant use.

Microsoft Entra ID provides an enterprise-ready identity management solution that integrates with AKS clusters. Since Kubernetes doesn't provide an identity management solution, you may be hard-pressed to granularly restrict access to the API server. With Microsoft Entra integrated clusters in AKS, you use your existing user and group accounts to authenticate users to the API server.

Using Kubernetes RBAC and Microsoft Entra ID-integration, you can secure the API server and provide the minimum permissions required to a scoped resource set, like a single namespace. You can grant different Microsoft Entra users or groups different Kubernetes roles. With granular permissions, you can restrict access to the API server and provide a clear audit trail of actions performed.

The recommended best practice is to use *groups* to provide access to files and folders instead of individual identities. For example, use a Microsoft Entra ID *group* membership to bind users to Kubernetes roles rather than individual *users*. As a user's group membership changes, their access permissions on the AKS cluster change accordingly.

Meanwhile, let's say you bind the individual user directly to a role and their job function changes. While the Microsoft Entra group memberships update, their permissions on the AKS cluster would not. In this scenario, the user ends up with more permissions than they require.

For more information about Microsoft Entra integration, Kubernetes RBAC, and Azure RBAC, see [Best practices for authentication and authorization in AKS](concepts-identity).

## Restrict access to Instance Metadata API


Best practice guidanceAdd a network policy in all user namespaces to block pod egress to the metadata endpoint.


Note

To implement Network Policy, include the attribute `--network-policy azure`

when creating the AKS cluster. Use the following command to create the cluster:
`az aks create -g myResourceGroup -n myManagedCluster --network-plugin azure --network-policy azure --generate-ssh-keys`


```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: restrict-instance-metadata
spec:
podSelector:
matchLabels: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 10.10.0.0/0#example
except:
- 169.254.169.254/32
```


## Secure container access to resources


Best practice guidanceLimit access to actions that containers can perform. Provide the least number of permissions, and avoid the use of root access or privileged escalation.


In the same way that you should grant users or groups the minimum privileges required, you should also limit containers to only necessary actions and processes. To minimize the risk of attack, avoid configuring applications and containers that require escalated privileges or root access.

Using user-namespaces, you improve the host isolation and limit the lateral movement in case of container breakouts. These improvements are significant whether the pod is running as root or not.

For even more granular control of container actions, you can also use built-in Linux security features such as *AppArmor* and *seccomp*.

For more information, see [Secure container access to resources](secure-container-access).

## Regularly update to the latest version of Kubernetes


Best practice guidanceTo stay current on new features and bug fixes, regularly upgrade the Kubernetes version in your AKS cluster.


Kubernetes releases new features at a quicker pace than more traditional infrastructure platforms. Kubernetes updates include:

- New features
- Bug or security fixes

New features typically move through *alpha* and *beta* status before they become *stable*. Once stable, are generally available and recommended for production use. Kubernetes new feature release cycle allows you to update Kubernetes without regularly encountering breaking changes or adjusting your deployments and templates.

AKS supports three minor versions of Kubernetes. Once a new minor patch version is introduced, the oldest minor version and patch releases supported are retired. Minor Kubernetes updates happen on a periodic basis. To stay within support, ensure you have a governance process to check for necessary upgrades. For more information, see [Supported Kubernetes versions AKS](supported-kubernetes-versions).

To check the versions that are available for your cluster, use the [az aks get-upgrades](/en-us/cli/azure/aks#az-aks-get-upgrades) command as shown in the following example:

```
az aks get-upgrades --resource-group myResourceGroup --name myAKSCluster --output table
```


You can then upgrade your AKS cluster using the [az aks upgrade](/en-us/cli/azure/aks#az-aks-upgrade) command. The upgrade process safely:

- Cordons and drains one node at a time.
- Schedules pods on remaining nodes.
- Deploys a new node running the latest OS and Kubernetes versions.

Important

Test new minor versions in a dev test environment and validate that your workload remains healthy with the new Kubernetes version.

Kubernetes may deprecate APIs (like in version 1.16) that your workloads rely on. When bringing new versions into production, consider using [multiple node pools on separate versions](create-node-pools) and upgrade individual pools one at a time to progressively roll the update across a cluster. If running multiple clusters, upgrade one cluster at a time to progressively monitor for impact or changes.

```
az aks upgrade --resource-group myResourceGroup --name myAKSCluster --kubernetes-version KUBERNETES_VERSION
```


For more information about upgrades in AKS, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions) and [Upgrade an AKS cluster](upgrade-cluster).

## Process Linux node updates

Each evening, Linux nodes in AKS get security patches through their distro update channel. This behavior is automatically configured as the nodes are deployed in an AKS cluster. To minimize disruption and potential impact to running workloads, nodes are not automatically rebooted if a security patch or kernel update requires it. For more information about how to handle node reboots, see [Apply security and kernel updates to nodes in AKS](node-updates-kured).

### Node image upgrades

Unattended upgrades apply updates to the Linux node OS, but the image used to create nodes for your cluster remains unchanged. If a new Linux node is added to your cluster, the original image is used to create the node. This new node will receive all the security and kernel updates available during the automatic check every night but will remain unpatched until all checks and restarts are complete. You can use node image upgrade to check for and update node images used by your cluster. For more information on node image upgrade, see [Azure Kubernetes Service (AKS) node image upgrade](node-image-upgrade).

## Process Windows Server node updates

For Windows Server nodes, regularly perform a node image upgrade operation to safely cordon and drain pods and deploy updated nodes.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/shared-health-probes -->

# Use shared health probes for externalTrafficPolicy: Cluster Services (preview) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

# Use shared health probes for

This article describes how to enable **shared health probe mode** (preview) for Services with `externalTrafficPolicy: Cluster`

in Azure Kubernetes Service (AKS). Shared probe mode improves load balancer efficiency, reduces configuration complexity, and provides more accurate node health monitoring.

## About shared health probe mode

In clusters that use `externalTrafficPolicy: Cluster`

, Azure Standard Load Balancer (SLB) currently creates a *separate probe per Service* and targets each Service's `nodePort`

.

This design means SLB infers node health from whichever **application pod** answers the probe. As clusters grow, this approach leads to several issues, including:

**Configuration drift and blind spots**: SLB can't detect a failed or misconfigured`kube‑proxy`

if iptables rules are still present.**Duplicate health logic**: Readiness must be defined twice. Once in each pod's`readinessProbe`

, and again through SLB annotations.**Operational overhead**: Each Service on each node is probed every*five seconds*, consuming connections, SNAT ports, and SLB rule space.**Feature friction**: Customers can't set`allocateLoadBalancerNodePorts=false`

, and workloads like Istio or ingress‑nginx require extra annotations to keep probes working.**Troubleshooting confusion**: An unhealthy app, Network Policy rule, or scale‑to‑zero event can make an*entire node*appear down.

**Shared probe mode** solves these problems by moving to a *single HTTP probe* for all `externalTrafficPolicy: Cluster`

Services. In shared probe mode:

- SLB probes
`http://<node‑ip>:10356/healthz`

, the standard`kube‑proxy`

health endpoint. - A lightweight sidecar runs next to
`kube‑proxy`

to relay the probe and handle PROXY protocol when Private Link Service is enabled.

## Benefits of shared probe mode

The following table outlines **key benefits** of using shared probe mode:

| Benefit | Why it matters |
|---|---|
| Accurate node health | SLB now measures `kube‑proxy` directly, not an arbitrary backend pod. |
| Simpler configuration | No per‑Service probe annotations; readiness lives solely in the pod spec. |
| Lower traffic overhead | One probe per node instead of Services × (nodes – 1) probes. |

Note

Keep the following information in mind when using shared probe mode:

- Services that use
`externalTrafficPolicy: Local`

are**unchanged**. - This feature does
**not**address container‑native load balancing.

## Before you begin

[Install or update the](#install-or-update-the-aks-preview-azure-cli-extension).`aks-preview`

Azure CLI extension[Register the](#register-the-enableslbsharedhealthprobepreview-feature-flag).`EnableSLBSharedHealthProbePreview`

feature flag in your Azure subscription

### Install or update the `aks-preview`

Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the

`aks-preview`

extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the

`aks-preview`

extension using thecommand.`az extension update`

`az extension update --name aks-preview`


### Register the `EnableSLBSharedHealthProbePreview`

feature flag

Register the

`EnableSLBSharedHealthProbePreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "EnableSLBSharedHealthProbePreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command:`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "EnableSLBSharedHealthProbePreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-cni-overlay-pod-expand -->

# Expand pod CIDR space in Azure CNI Overlay Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can expand your pod Classless Inter-Domain Routing (CIDR) space on Azure CNI Overlay clusters in Azure Kubernetes Service with Linux nodes only. The operation uses the [ az aks update](/en-us/cli/azure/aks#az_aks_update) command and allows expansions without the need to re-create your AKS cluster.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Requirements and parameters

| Requirement or parameter | Supported versions or values | Description |
|---|---|---|
| Feature flag | `EnableAzureCNIOverlayPodCIDRExpansion` |
This feature flag must be registered in your subscription to enable pod CIDR expansion in Azure CNI Overlay AKS clusters. |
| Azure CLI version | 2.48.0 or later | The Azure CLI version must be 2.48.0 or later to support the pod CIDR expansion feature. |
| Kubernetes version | 1.33 | Pod CIDR expansion is supported only on AKS clusters running Kubernetes version 1.33. |
| Node operating system | Linux | Pod CIDR expansion is supported only on Azure CNI Overlay AKS clusters with Linux nodes. |
| Networking mode | Azure CNI Overlay | Pod CIDR expansion is supported only on AKS clusters that use Azure CNI Overlay networking. |
| Example original pod CIDR | `10.244.0.0/18` |
This is an example of a starting pod CIDR block. |
| Example expanded pod CIDR | `10.244.0.0/16` |
This is an example of a target expanded pod CIDR block. |

## Limitations

- Windows nodes and hybrid node scenarios aren't supported.
- Shrinking or changing the pod CIDR isn't supported.
- Adding a discontinuous pod CIDR isn't supported. The new pod CIDR must be a larger superset that contains the complete original range.
- IPv6 pod CIDR expansion isn't supported.
- Changing multiple pod CIDR blocks via
`--pod-cidrs`

isn't supported. - If an
[Azure availability zone](availability-zones)is down during the expansion operation, new nodes might appear as`unready`

. You can expect these nodes to reconcile after the availability zone is up.

## Prerequisites

- You need an Azure subscription. If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/free/)before you begin. - Ensure that you meet the requirements listed in the
[Requirements and parameters](#requirements-and-parameters)section.

## Register the `EnableAzureCNIOverlayPodCIDRExpansion`

feature flag

Register the

`EnableAzureCNIOverlayPodCIDRExpansion`

feature flag by using thecommand:`az feature register`

`az feature register --namespace Microsoft.ContainerService --name EnableAzureCNIOverlayPodCIDRExpansion`

Verify successful registration by using the

command. It takes a few minutes for the registration to finish.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "EnableAzureCNIOverlayPodCIDRExpansion"`

After the feature shows

`Registered`

, refresh the registration of the`Microsoft.ContainerService`

resource provider by using thecommand:`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Update an Azure CNI Overlay AKS cluster to expand the pod CIDR space

Starting from a pod CIDR block of

`10.244.0.0/18`

, you can expand the pod CIDR space by using thecommand. For example:`az aks update`

`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --pod-cidr 10.244.0.0/16`

Note

Although the update operation might successfully finish and show the new pod CIDR in the network profile, be sure to validate the new cluster state through

`NodeNetworkConfig`

(`nnc`

).Verify the state of the upgrade operation by checking

`NodeNetworkConfig`

(`nnc`

) via the`kubectl get nnc`

command. In the output, all node pools should match your new pod CIDR block (for example,`10.244.0.0/16`

).`kubectl get nnc -A -o jsonpath='{range .items[*]}{.metadata.name}{" "}{.status.networkContainers[0].subnetAddressSpace}{"\n"}{end}'`


## Related content

To learn more about Azure CNI Overlay networking on AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/security-controls-policy -->

# Azure Policy Regulatory Compliance controls for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Regulatory Compliance in Azure Policy](/en-us/azure/governance/policy/concepts/regulatory-compliance)
provides initiative definitions (*built-ins*) created and managed by Microsoft, for the compliance domains and security controls related to different compliance standards. This page lists the Azure Kubernetes Service (AKS) compliance domains and security controls.

You can assign the built-ins for a **security control** individually to help make your Azure resources compliant with the specific standard.

The title of each built-in policy definition links to the policy definition in the Azure portal. Use the link in the **Policy Version** column to view the source on the
[Azure Policy GitHub repo](https://github.com/Azure/azure-policy).

Important

Each control is associated with one or more [Azure Policy](/en-us/azure/governance/policy/overview) definitions. These policies might help you [assess compliance](/en-us/azure/governance/policy/how-to/get-compliance-data) with the control.
However, there often isn't a one-to-one or complete match between a control and one or more policies. As such, **Compliant** in Azure Policy refers only to the policies themselves. This doesn't ensure that you're fully compliant with all requirements of a control. In addition, the compliance standard includes controls that aren't addressed by any Azure Policy definitions at this time.
Therefore, compliance in Azure Policy is only a partial view of your overall compliance status. The associations between controls and Azure Policy Regulatory Compliance definitions for these compliance standards can change over time.

## CIS Microsoft Azure Foundations Benchmark 1.1.0

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - CIS Microsoft Azure Foundations Benchmark 1.1.0](/en-us/azure/governance/policy/samples/cis-azure-1-1-0).
For more information about this compliance standard, see
[CIS Microsoft Azure Foundations Benchmark](https://www.cisecurity.org/benchmark/azure/).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| 8 Other Security Considerations | 8.5 | Enable role-based access control (RBAC) within Azure Kubernetes Services |
|

[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)## CIS Microsoft Azure Foundations Benchmark 1.3.0

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - CIS Microsoft Azure Foundations Benchmark 1.3.0](/en-us/azure/governance/policy/samples/cis-azure-1-3-0).
For more information about this compliance standard, see
[CIS Microsoft Azure Foundations Benchmark](https://www.cisecurity.org/benchmark/azure/).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| 8 Other Security Considerations | 8.5 | Enable role-based access control (RBAC) within Azure Kubernetes Services |
|

[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)## CIS Microsoft Azure Foundations Benchmark 1.4.0

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance details for CIS v1.4.0](/en-us/azure/governance/policy/samples/cis-azure-1-4-0).
For more information about this compliance standard, see
[CIS Microsoft Azure Foundations Benchmark](https://www.cisecurity.org/benchmark/azure/).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| 8 Other Security Considerations | 8.7 | Enable role-based access control (RBAC) within Azure Kubernetes Services |
|

[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)## CMMC Level 3

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - CMMC Level 3](/en-us/azure/governance/policy/samples/cmmc-l3).
For more information about this compliance standard, see
[Cybersecurity Maturity Model Certification (CMMC)](https://dodcio.defense.gov/CMMC/).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| Access Control | AC.1.001 | Limit information system access to authorized users, processes acting on behalf of authorized users, and devices (including other information systems). |
|

[7.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/HostNetworkPorts.json)[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)[Kubernetes cluster pods should only use approved host network and port list](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F82985f06-dc18-4a48-bc1c-b9f4f0098cfe)[7.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/HostNetworkPorts.json)[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)[Kubernetes cluster pods should only use approved host network and port list](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F82985f06-dc18-4a48-bc1c-b9f4f0098cfe)[7.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/HostNetworkPorts.json)[Kubernetes Services should be upgraded to a non-vulnerable Kubernetes version](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffb893a29-21bb-418c-a157-e99480ec364c)[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_UpgradeVersion_KubernetesService_Audit.json)[Kubernetes cluster pods should only use approved host network and port list](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F82985f06-dc18-4a48-bc1c-b9f4f0098cfe)[7.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/HostNetworkPorts.json)[Both operating systems and data disks in Azure Kubernetes Service clusters should be encrypted by customer-managed keys](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F7d7be79c-23ba-4033-84dd-45e2a5ccdd67)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_CMK_Deny.json)[Kubernetes cluster pods should only use approved host network and port list](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F82985f06-dc18-4a48-bc1c-b9f4f0098cfe)[7.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/HostNetworkPorts.json)[Kubernetes Services should be upgraded to a non-vulnerable Kubernetes version](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffb893a29-21bb-418c-a157-e99480ec364c)[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_UpgradeVersion_KubernetesService_Audit.json)## FedRAMP High

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - FedRAMP High](/en-us/azure/governance/policy/samples/fedramp-high).
For more information about this compliance standard, see
[FedRAMP High](https://www.fedramp.gov/).

## FedRAMP Moderate

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - FedRAMP Moderate](/en-us/azure/governance/policy/samples/fedramp-moderate).
For more information about this compliance standard, see
[FedRAMP Moderate](https://www.fedramp.gov/).

## HIPAA HITRUST

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - HIPAA HITRUST](/en-us/azure/governance/policy/samples/hipaa-hitrust).
For more information about this compliance standard, see
[HIPAA HITRUST](https://www.hhs.gov/hipaa/for-professionals/security/laws-regulations/index.html).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| Privilege Management | 1149.01c2System.9 - 01.c | The organization facilitates information sharing by enabling authorized users to determine a business partner's access when discretion is allowed as defined by the organization and by employing manual processes or automated mechanisms to assist users in making information sharing/collaboration decisions. |
|

[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)## Microsoft Cloud for Sovereignty Baseline Confidential Policies

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance details for MCfS Sovereignty Baseline Confidential Policies](/en-us/azure/governance/policy/samples/mcfs-baseline-confidential).
For more information about this compliance standard, see
[Microsoft Cloud for Sovereignty Policy portfolio](/en-us/industry/sovereignty/policy-portfolio-baseline).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| SO.3 - Customer-Managed Keys | SO.3 | Azure products must be configured to use Customer-Managed Keys when possible. |
|

[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_CMK_Deny.json)## Microsoft cloud security benchmark

The [Microsoft cloud security benchmark](/en-us/security/benchmark/azure/introduction) provides recommendations on
how you can secure your cloud solutions on Azure. To see how this service completely maps to the
Microsoft cloud security benchmark, see the
[Azure Security Benchmark mapping files](https://github.com/MicrosoftDocs/SecurityBenchmarks/tree/master/Azure%20Offer%20Security%20Baselines).

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - Microsoft cloud security benchmark](/en-us/azure/governance/policy/samples/azure-security-benchmark).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| Network Security | NS-2 | NS-2 Secure cloud services with network controls |
|

[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableIpRanges_KubernetesService_Audit.json)[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)[Kubernetes clusters should be accessible only over HTTPS](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1a5b4dca-0b6f-4cf5-907c-56316bc1bf3d)[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/IngressHttpsOnly.json)[Azure Kubernetes Service clusters should have Defender profile enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa1840de2-8088-4ea8-b153-b4c723e9cb01)[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ASC_Azure_Defender_AKS_SecurityProfile_Audit.json)[Azure Kubernetes Service clusters should have Defender profile enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa1840de2-8088-4ea8-b153-b4c723e9cb01)[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ASC_Azure_Defender_AKS_SecurityProfile_Audit.json)[Resource logs in Azure Kubernetes Service should be enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F245fc9df-fa96-4414-9a0b-3738c2f7341c)[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AuditDiagnosticLog_Audit.json)[Azure Policy Add-on for Kubernetes service (AKS) should be installed and enabled on your clusters](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0a15ec92-a229-4763-bb14-0ea34a568f8d)[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_AzurePolicyAddOn_Audit.json)[Kubernetes cluster containers CPU and memory resource limits should not exceed the specified limits](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe345eecc-fa47-480f-9e88-67dcc122b164)[9.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerResourceLimits.json)[Kubernetes cluster containers should not share host namespaces](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F47a1ee2f-2a2a-4576-bf2a-e0e36709c2b8)[6.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockHostNamespace.json)[Kubernetes cluster containers should only use allowed AppArmor profiles](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F511f5417-5d12-434d-ab2e-816901e72a5e)[6.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/EnforceAppArmorProfile.json)[Kubernetes cluster containers should only use allowed capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc26596ff-4d70-4e6a-9a30-c2506bd2f80c)[6.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedCapabilities.json)[Kubernetes cluster containers should only use allowed images](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffebd0533-8e55-448f-b837-bd0e06f16469)[9.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedImages.json)[Kubernetes cluster containers should run with a read only root file system](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fdf49d893-a74c-421d-bc95-c663042e5b80)[6.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ReadOnlyRootFileSystem.json)[Kubernetes cluster pod hostPath volumes should only use allowed host paths](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F098fc59e-46c7-4d99-9b16-64990e543d75)[6.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedHostPaths.json)[Kubernetes cluster pods and containers should only run with approved user and group IDs](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff06ddb64-5fa3-4b77-b166-acb36f7f6042)[6.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedUsersGroups.json)[Kubernetes cluster pods should only use approved host network and port list](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F82985f06-dc18-4a48-bc1c-b9f4f0098cfe)[7.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/HostNetworkPorts.json)[Kubernetes cluster services should listen only on allowed ports](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F233a2a17-77ca-4fb1-9b6b-69223d272a44)[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ServiceAllowedPorts.json)[Kubernetes cluster should not allow privileged containers](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F95edb821-ddaf-4404-9732-666045e056b4)[9.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerNoPrivilege.json)[Kubernetes clusters should disable automounting API credentials](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F423dd1ba-798e-40e4-9c4d-b6902674b423)[4.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockAutomountToken.json)[Kubernetes clusters should not allow container privilege escalation](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1c6e92c9-99f0-4e55-9cf2-0c234dc48f99)[8.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerNoPrivilegeEscalation.json)[Kubernetes clusters should not grant CAP_SYS_ADMIN security capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd2e7ea85-6b44-4317-a0be-1b951587f626)[5.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerDisallowedSysAdminCapability.json)[Kubernetes clusters should not use the default namespace](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F9f061a12-e40d-4183-a00e-171812443373)[4.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockDefaultNamespace.json)[Azure running container images should have vulnerabilities resolved (powered by Microsoft Defender Vulnerability Management)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F17f4b1cc-c55c-4d94-b1f9-2978f6ac2957)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/MDC_K8sRuningImagesVulnerabilityAssessmentBasedOnMDVM_Audit.json)[Azure running container images should have vulnerabilities resolved (powered by Microsoft Defender Vulnerability Management)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F17f4b1cc-c55c-4d94-b1f9-2978f6ac2957)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/MDC_K8sRuningImagesVulnerabilityAssessmentBasedOnMDVM_Audit.json)## NIST SP 800-171 R2

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - NIST SP 800-171 R2](/en-us/azure/governance/policy/samples/nist-sp-800-171-r2).
For more information about this compliance standard, see
[NIST SP 800-171 R2](https://csrc.nist.gov/publications/detail/sp/800-171/rev-2/final).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| Access Control | 3.1.3 | Control the flow of CUI in accordance with approved authorizations. |
|

[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableIpRanges_KubernetesService_Audit.json)[Authorized IP ranges should be defined on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0e246bcf-5f6f-4f87-bc6f-775d4712c7ea)[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableIpRanges_KubernetesService_Audit.json)[Both operating systems and data disks in Azure Kubernetes Service clusters should be encrypted by customer-managed keys](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F7d7be79c-23ba-4033-84dd-45e2a5ccdd67)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_CMK_Deny.json)[Temp disks and cache for agent node pools in Azure Kubernetes Service clusters should be encrypted at host](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F41425d9f-d1a5-499a-9932-f8ed8453932c)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_EncryptionAtHost_Deny.json)[Authorized IP ranges should be defined on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0e246bcf-5f6f-4f87-bc6f-775d4712c7ea)[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableIpRanges_KubernetesService_Audit.json)[Authorized IP ranges should be defined on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0e246bcf-5f6f-4f87-bc6f-775d4712c7ea)[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableIpRanges_KubernetesService_Audit.json)[Authorized IP ranges should be defined on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0e246bcf-5f6f-4f87-bc6f-775d4712c7ea)[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableIpRanges_KubernetesService_Audit.json)[Kubernetes clusters should be accessible only over HTTPS](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1a5b4dca-0b6f-4cf5-907c-56316bc1bf3d)[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/IngressHttpsOnly.json)[Kubernetes Services should be upgraded to a non-vulnerable Kubernetes version](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffb893a29-21bb-418c-a157-e99480ec364c)[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_UpgradeVersion_KubernetesService_Audit.json)[Azure Policy Add-on for Kubernetes service (AKS) should be installed and enabled on your clusters](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0a15ec92-a229-4763-bb14-0ea34a568f8d)[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_AzurePolicyAddOn_Audit.json)[Kubernetes cluster containers CPU and memory resource limits should not exceed the specified limits](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe345eecc-fa47-480f-9e88-67dcc122b164)[9.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerResourceLimits.json)[Kubernetes cluster containers should not share host namespaces](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F47a1ee2f-2a2a-4576-bf2a-e0e36709c2b8)[6.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockHostNamespace.json)[Kubernetes cluster containers should only use allowed AppArmor profiles](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F511f5417-5d12-434d-ab2e-816901e72a5e)[6.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/EnforceAppArmorProfile.json)[Kubernetes cluster containers should only use allowed capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc26596ff-4d70-4e6a-9a30-c2506bd2f80c)[6.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedCapabilities.json)[Kubernetes cluster containers should only use allowed images](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffebd0533-8e55-448f-b837-bd0e06f16469)[9.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedImages.json)[Kubernetes cluster containers should run with a read only root file system](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fdf49d893-a74c-421d-bc95-c663042e5b80)[6.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ReadOnlyRootFileSystem.json)[Kubernetes cluster pod hostPath volumes should only use allowed host paths](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F098fc59e-46c7-4d99-9b16-64990e543d75)[6.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedHostPaths.json)[Kubernetes cluster pods and containers should only run with approved user and group IDs](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff06ddb64-5fa3-4b77-b166-acb36f7f6042)[6.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedUsersGroups.json)[Kubernetes cluster pods should only use approved host network and port list](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F82985f06-dc18-4a48-bc1c-b9f4f0098cfe)[7.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/HostNetworkPorts.json)[Kubernetes cluster services should listen only on allowed ports](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F233a2a17-77ca-4fb1-9b6b-69223d272a44)[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ServiceAllowedPorts.json)[Kubernetes cluster should not allow privileged containers](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F95edb821-ddaf-4404-9732-666045e056b4)[9.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerNoPrivilege.json)[Kubernetes clusters should not allow container privilege escalation](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1c6e92c9-99f0-4e55-9cf2-0c234dc48f99)[8.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerNoPrivilegeEscalation.json)[Azure Policy Add-on for Kubernetes service (AKS) should be installed and enabled on your clusters](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0a15ec92-a229-4763-bb14-0ea34a568f8d)[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_AzurePolicyAddOn_Audit.json)[Kubernetes cluster containers CPU and memory resource limits should not exceed the specified limits](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe345eecc-fa47-480f-9e88-67dcc122b164)[9.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerResourceLimits.json)[Kubernetes cluster containers should not share host namespaces](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F47a1ee2f-2a2a-4576-bf2a-e0e36709c2b8)[6.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockHostNamespace.json)[Kubernetes cluster containers should only use allowed AppArmor profiles](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F511f5417-5d12-434d-ab2e-816901e72a5e)[6.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/EnforceAppArmorProfile.json)[Kubernetes cluster containers should only use allowed capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc26596ff-4d70-4e6a-9a30-c2506bd2f80c)[6.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedCapabilities.json)[Kubernetes cluster containers should only use allowed images](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffebd0533-8e55-448f-b837-bd0e06f16469)[9.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedImages.json)[Kubernetes cluster containers should run with a read only root file system](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fdf49d893-a74c-421d-bc95-c663042e5b80)[6.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ReadOnlyRootFileSystem.json)[Kubernetes cluster pod hostPath volumes should only use allowed host paths](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F098fc59e-46c7-4d99-9b16-64990e543d75)[6.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedHostPaths.json)[Kubernetes cluster pods and containers should only run with approved user and group IDs](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff06ddb64-5fa3-4b77-b166-acb36f7f6042)[6.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedUsersGroups.json)[Kubernetes cluster pods should only use approved host network and port list](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F82985f06-dc18-4a48-bc1c-b9f4f0098cfe)[7.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/HostNetworkPorts.json)[Kubernetes cluster services should listen only on allowed ports](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F233a2a17-77ca-4fb1-9b6b-69223d272a44)[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ServiceAllowedPorts.json)[Kubernetes cluster should not allow privileged containers](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F95edb821-ddaf-4404-9732-666045e056b4)[9.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerNoPrivilege.json)[Kubernetes clusters should not allow container privilege escalation](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1c6e92c9-99f0-4e55-9cf2-0c234dc48f99)[8.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerNoPrivilegeEscalation.json)## NIST SP 800-53 Rev. 4

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - NIST SP 800-53 Rev. 4](/en-us/azure/governance/policy/samples/nist-sp-800-53-r4).
For more information about this compliance standard, see
[NIST SP 800-53 Rev. 4](https://nvd.nist.gov/800-53).

## NIST SP 800-53 Rev. 5

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - NIST SP 800-53 Rev. 5](/en-us/azure/governance/policy/samples/nist-sp-800-53-r5).
For more information about this compliance standard, see
[NIST SP 800-53 Rev. 5](https://nvd.nist.gov/800-53).

## NL BIO Cloud Theme

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance details for NL BIO Cloud Theme](/en-us/azure/governance/policy/samples/nl-bio-cloud-theme).
For more information about this compliance standard, see
[Baseline Information Security Government Cybersecurity - Digital Government (digitaleoverheid.nl)](https://www.digitaleoverheid.nl/overzicht-van-alle-onderwerpen/cybersecurity/kaders-voor-cybersecurity/baseline-informatiebeveiliging-overheid/).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| C.04.3 Technical vulnerability management - Timelines | C.04.3 | If the probability of abuse and the expected damage are both high, patches are installed no later than within a week. |
|

[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_UpgradeVersion_KubernetesService_Audit.json)[Kubernetes Services should be upgraded to a non-vulnerable Kubernetes version](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffb893a29-21bb-418c-a157-e99480ec364c)[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_UpgradeVersion_KubernetesService_Audit.json)[Azure Policy Add-on for Kubernetes service (AKS) should be installed and enabled on your clusters](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0a15ec92-a229-4763-bb14-0ea34a568f8d)[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_AzurePolicyAddOn_Audit.json)[Kubernetes cluster containers CPU and memory resource limits should not exceed the specified limits](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe345eecc-fa47-480f-9e88-67dcc122b164)[9.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerResourceLimits.json)[Kubernetes cluster containers should not share host namespaces](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F47a1ee2f-2a2a-4576-bf2a-e0e36709c2b8)[6.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockHostNamespace.json)[Kubernetes cluster containers should only use allowed AppArmor profiles](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F511f5417-5d12-434d-ab2e-816901e72a5e)[6.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/EnforceAppArmorProfile.json)[Kubernetes cluster containers should only use allowed capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc26596ff-4d70-4e6a-9a30-c2506bd2f80c)[6.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedCapabilities.json)[Kubernetes cluster containers should only use allowed images](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffebd0533-8e55-448f-b837-bd0e06f16469)[9.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedImages.json)[Kubernetes cluster containers should run with a read only root file system](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fdf49d893-a74c-421d-bc95-c663042e5b80)[6.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ReadOnlyRootFileSystem.json)[Kubernetes cluster pod hostPath volumes should only use allowed host paths](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F098fc59e-46c7-4d99-9b16-64990e543d75)[6.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedHostPaths.json)[Kubernetes cluster pods and containers should only run with approved user and group IDs](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff06ddb64-5fa3-4b77-b166-acb36f7f6042)[6.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedUsersGroups.json)[Kubernetes cluster pods should only use approved host network and port list](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F82985f06-dc18-4a48-bc1c-b9f4f0098cfe)[7.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/HostNetworkPorts.json)[Kubernetes cluster services should listen only on allowed ports](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F233a2a17-77ca-4fb1-9b6b-69223d272a44)[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ServiceAllowedPorts.json)[Kubernetes cluster should not allow privileged containers](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F95edb821-ddaf-4404-9732-666045e056b4)[9.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerNoPrivilege.json)[Kubernetes clusters should disable automounting API credentials](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F423dd1ba-798e-40e4-9c4d-b6902674b423)[4.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockAutomountToken.json)[Kubernetes clusters should not allow container privilege escalation](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1c6e92c9-99f0-4e55-9cf2-0c234dc48f99)[8.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerNoPrivilegeEscalation.json)[Kubernetes clusters should not grant CAP_SYS_ADMIN security capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd2e7ea85-6b44-4317-a0be-1b951587f626)[5.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerDisallowedSysAdminCapability.json)[Kubernetes clusters should not use the default namespace](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F9f061a12-e40d-4183-a00e-171812443373)[4.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockDefaultNamespace.json)[Kubernetes Services should be upgraded to a non-vulnerable Kubernetes version](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffb893a29-21bb-418c-a157-e99480ec364c)[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_UpgradeVersion_KubernetesService_Audit.json)[Kubernetes clusters should be accessible only over HTTPS](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1a5b4dca-0b6f-4cf5-907c-56316bc1bf3d)[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/IngressHttpsOnly.json)[Both operating systems and data disks in Azure Kubernetes Service clusters should be encrypted by customer-managed keys](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F7d7be79c-23ba-4033-84dd-45e2a5ccdd67)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_CMK_Deny.json)[Temp disks and cache for agent node pools in Azure Kubernetes Service clusters should be encrypted at host](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F41425d9f-d1a5-499a-9932-f8ed8453932c)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_EncryptionAtHost_Deny.json)[Authorized IP ranges should be defined on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0e246bcf-5f6f-4f87-bc6f-775d4712c7ea)[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableIpRanges_KubernetesService_Audit.json)[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)[Kubernetes Services should be upgraded to a non-vulnerable Kubernetes version](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffb893a29-21bb-418c-a157-e99480ec364c)[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_UpgradeVersion_KubernetesService_Audit.json)[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)[Kubernetes clusters should be accessible only over HTTPS](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1a5b4dca-0b6f-4cf5-907c-56316bc1bf3d)[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/IngressHttpsOnly.json)[Kubernetes clusters should be accessible only over HTTPS](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1a5b4dca-0b6f-4cf5-907c-56316bc1bf3d)[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/IngressHttpsOnly.json)[Both operating systems and data disks in Azure Kubernetes Service clusters should be encrypted by customer-managed keys](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F7d7be79c-23ba-4033-84dd-45e2a5ccdd67)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_CMK_Deny.json)[Temp disks and cache for agent node pools in Azure Kubernetes Service clusters should be encrypted at host](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F41425d9f-d1a5-499a-9932-f8ed8453932c)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_EncryptionAtHost_Deny.json)[Resource logs in Azure Kubernetes Service should be enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F245fc9df-fa96-4414-9a0b-3738c2f7341c)[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AuditDiagnosticLog_Audit.json)## Reserve Bank of India - IT Framework for NBFC

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - Reserve Bank of India - IT Framework for NBFC](/en-us/azure/governance/policy/samples/rbi-itf-nbfc-2017).
For more information about this compliance standard, see
[Reserve Bank of India - IT Framework for NBFC](https://www.rbi.org.in/Scripts/NotificationUser.aspx?Id=10999&Mode=0#C1).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| IT Governance | 1 | IT Governance-1 |
|

[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_UpgradeVersion_KubernetesService_Audit.json)[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)[Azure Kubernetes Service clusters should have Defender profile enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa1840de2-8088-4ea8-b153-b4c723e9cb01)[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ASC_Azure_Defender_AKS_SecurityProfile_Audit.json)[Kubernetes Services should be upgraded to a non-vulnerable Kubernetes version](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffb893a29-21bb-418c-a157-e99480ec364c)[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_UpgradeVersion_KubernetesService_Audit.json)## Reserve Bank of India IT Framework for Banks v2016

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - RBI ITF Banks v2016](/en-us/azure/governance/policy/samples/rbi-itf-banks-2016).
For more information about this compliance standard, see
[RBI ITF Banks v2016 (PDF)](https://rbidocs.rbi.org.in/rdocs/notification/PDFs/NT41893F697BC1D57443BB76AFC7AB56272EB.PDF).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| Patch/Vulnerability & Change Management | Patch/Vulnerability & Change Management-7.7 |
|

[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableIpRanges_KubernetesService_Audit.json)[Azure Kubernetes Service clusters should have Defender profile enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa1840de2-8088-4ea8-b153-b4c723e9cb01)[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ASC_Azure_Defender_AKS_SecurityProfile_Audit.json)[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)## RMIT Malaysia

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - RMIT Malaysia](/en-us/azure/governance/policy/samples/rmit-malaysia).
For more information about this compliance standard, see
[RMIT Malaysia](https://www.bnm.gov.my/documents/20124/963937/Risk+Management+in+Technology+(RMiT).pdf/810b088e-6f4f-aa35-b603-1208ace33619?t=1592866162078).

## Spain ENS

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance details for Spain ENS](/en-us/azure/governance/policy/samples/spain-ens).
For more information about this compliance standard, see
[CCN-STIC 884](https://www.ccn-cert.cni.es/es/comunicacion-eventos/comunicados-ccn-cert/9519-disponible-la-guia-ccn-stic-884-perfil-de-cumplimiento-especifico-para-azure-servicio-de-cloud-corporativo).

## SWIFT CSP-CSCF v2021

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance details for SWIFT CSP-CSCF v2021](/en-us/azure/governance/policy/samples/swift-csp-cscf-2021).
For more information about this compliance standard, see
[SWIFT CSP CSCF v2021](https://www.swift.com/myswift/customer-security-programme-csp).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| SWIFT Environment Protection | 1.1 | SWIFT Environment Protection |
|

[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableIpRanges_KubernetesService_Audit.json)[Authorized IP ranges should be defined on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0e246bcf-5f6f-4f87-bc6f-775d4712c7ea)[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableIpRanges_KubernetesService_Audit.json)[Kubernetes clusters should be accessible only over HTTPS](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1a5b4dca-0b6f-4cf5-907c-56316bc1bf3d)[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/IngressHttpsOnly.json)[Both operating systems and data disks in Azure Kubernetes Service clusters should be encrypted by customer-managed keys](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F7d7be79c-23ba-4033-84dd-45e2a5ccdd67)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_CMK_Deny.json)[Both operating systems and data disks in Azure Kubernetes Service clusters should be encrypted by customer-managed keys](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F7d7be79c-23ba-4033-84dd-45e2a5ccdd67)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_CMK_Deny.json)## System and Organization Controls (SOC) 2

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance details for System and Organization Controls (SOC) 2](/en-us/azure/governance/policy/samples/soc-2).
For more information about this compliance standard, see
[System and Organization Controls (SOC) 2](/en-us/azure/compliance/offerings/offering-soc-2).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| Logical and Physical Access Controls | CC6.1 | Logical access security software, infrastructure, and architectures |
|

[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/IngressHttpsOnly.json)[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json)[Kubernetes clusters should be accessible only over HTTPS](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1a5b4dca-0b6f-4cf5-907c-56316bc1bf3d)[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/IngressHttpsOnly.json)[Kubernetes clusters should be accessible only over HTTPS](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1a5b4dca-0b6f-4cf5-907c-56316bc1bf3d)[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/IngressHttpsOnly.json)[Azure Policy Add-on for Kubernetes service (AKS) should be installed and enabled on your clusters](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0a15ec92-a229-4763-bb14-0ea34a568f8d)[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_AzurePolicyAddOn_Audit.json)[Kubernetes cluster containers CPU and memory resource limits should not exceed the specified limits](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe345eecc-fa47-480f-9e88-67dcc122b164)[9.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerResourceLimits.json)[Kubernetes cluster containers should not share host namespaces](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F47a1ee2f-2a2a-4576-bf2a-e0e36709c2b8)[6.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockHostNamespace.json)[Kubernetes cluster containers should only use allowed AppArmor profiles](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F511f5417-5d12-434d-ab2e-816901e72a5e)[6.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/EnforceAppArmorProfile.json)[Kubernetes cluster containers should only use allowed capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc26596ff-4d70-4e6a-9a30-c2506bd2f80c)[6.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedCapabilities.json)[Kubernetes cluster containers should only use allowed images](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffebd0533-8e55-448f-b837-bd0e06f16469)[9.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedImages.json)[Kubernetes cluster containers should run with a read only root file system](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fdf49d893-a74c-421d-bc95-c663042e5b80)[6.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ReadOnlyRootFileSystem.json)[Kubernetes cluster pod hostPath volumes should only use allowed host paths](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F098fc59e-46c7-4d99-9b16-64990e543d75)[6.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedHostPaths.json)[Kubernetes cluster pods and containers should only run with approved user and group IDs](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff06ddb64-5fa3-4b77-b166-acb36f7f6042)[6.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedUsersGroups.json)[Kubernetes cluster pods should only use approved host network and port list](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F82985f06-dc18-4a48-bc1c-b9f4f0098cfe)[7.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/HostNetworkPorts.json)[Kubernetes cluster services should listen only on allowed ports](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F233a2a17-77ca-4fb1-9b6b-69223d272a44)[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ServiceAllowedPorts.json)[Kubernetes cluster should not allow privileged containers](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F95edb821-ddaf-4404-9732-666045e056b4)[9.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerNoPrivilege.json)[Kubernetes clusters should disable automounting API credentials](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F423dd1ba-798e-40e4-9c4d-b6902674b423)[4.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockAutomountToken.json)[Kubernetes clusters should not allow container privilege escalation](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1c6e92c9-99f0-4e55-9cf2-0c234dc48f99)[8.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerNoPrivilegeEscalation.json)[Kubernetes clusters should not grant CAP_SYS_ADMIN security capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd2e7ea85-6b44-4317-a0be-1b951587f626)[5.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerDisallowedSysAdminCapability.json)[Kubernetes clusters should not use the default namespace](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F9f061a12-e40d-4183-a00e-171812443373)[4.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockDefaultNamespace.json)[Azure Kubernetes Service clusters should have Defender profile enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa1840de2-8088-4ea8-b153-b4c723e9cb01)[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ASC_Azure_Defender_AKS_SecurityProfile_Audit.json)[Azure Policy Add-on for Kubernetes service (AKS) should be installed and enabled on your clusters](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0a15ec92-a229-4763-bb14-0ea34a568f8d)[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_AzurePolicyAddOn_Audit.json)[Kubernetes cluster containers CPU and memory resource limits should not exceed the specified limits](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe345eecc-fa47-480f-9e88-67dcc122b164)[9.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerResourceLimits.json)[Kubernetes cluster containers should not share host namespaces](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F47a1ee2f-2a2a-4576-bf2a-e0e36709c2b8)[6.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockHostNamespace.json)[Kubernetes cluster containers should only use allowed AppArmor profiles](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F511f5417-5d12-434d-ab2e-816901e72a5e)[6.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/EnforceAppArmorProfile.json)[Kubernetes cluster containers should only use allowed capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc26596ff-4d70-4e6a-9a30-c2506bd2f80c)[6.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedCapabilities.json)[Kubernetes cluster containers should only use allowed images](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffebd0533-8e55-448f-b837-bd0e06f16469)[9.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedImages.json)[Kubernetes cluster containers should run with a read only root file system](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fdf49d893-a74c-421d-bc95-c663042e5b80)[6.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ReadOnlyRootFileSystem.json)[Kubernetes cluster pod hostPath volumes should only use allowed host paths](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F098fc59e-46c7-4d99-9b16-64990e543d75)[6.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedHostPaths.json)[Kubernetes cluster pods and containers should only run with approved user and group IDs](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff06ddb64-5fa3-4b77-b166-acb36f7f6042)[6.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedUsersGroups.json)[Kubernetes cluster pods should only use approved host network and port list](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F82985f06-dc18-4a48-bc1c-b9f4f0098cfe)[7.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/HostNetworkPorts.json)[Kubernetes cluster services should listen only on allowed ports](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F233a2a17-77ca-4fb1-9b6b-69223d272a44)[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ServiceAllowedPorts.json)[Kubernetes cluster should not allow privileged containers](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F95edb821-ddaf-4404-9732-666045e056b4)[9.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerNoPrivilege.json)[Kubernetes clusters should disable automounting API credentials](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F423dd1ba-798e-40e4-9c4d-b6902674b423)[4.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockAutomountToken.json)[Kubernetes clusters should not allow container privilege escalation](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1c6e92c9-99f0-4e55-9cf2-0c234dc48f99)[8.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerNoPrivilegeEscalation.json)[Kubernetes clusters should not grant CAP_SYS_ADMIN security capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd2e7ea85-6b44-4317-a0be-1b951587f626)[5.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerDisallowedSysAdminCapability.json)[Kubernetes clusters should not use the default namespace](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F9f061a12-e40d-4183-a00e-171812443373)[4.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockDefaultNamespace.json)## Next steps

- Learn more about
[Azure Policy Regulatory Compliance](/en-us/azure/governance/policy/concepts/regulatory-compliance). - See the built-ins on the
[Azure Policy GitHub repo](https://github.com/Azure/azure-policy).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-configure-container-network-logs -->

# Set up container network logs with Advanced Container Networking Services (preview)

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

In this article, you complete the steps to configure and use the container network logs feature in Advanced Container Networking Services for Azure Kubernetes Service (AKS). These logs offer persistent network flow monitoring tailored to enhance visibility in containerized environments.

By capturing container network logs, you can effectively track network traffic, detect anomalies, optimize performance, and ensure compliance with established policies. Follow the detailed instructions provided to set up and integrate container network logs for your system. For more information about the container network logs feature, see [Overview of container network logs](container-network-observability-logs).

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of the Azure CLI required to complete the steps in this article is 2.75.0. To find your version, run

`az --version`

in the Azure CLI. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).Container network logs in stored logs mode work only for Cilium data planes.

Container network logs in on-demand mode work for both Cilium and non-Cilium data planes.

If your existing cluster is version 1.33 or earlier, upgrade the cluster to the latest available Kubernetes version.

The minimum version of the

`aks-preview`

Azure CLI extension to complete the steps in this article is`19.0.07`

.

### Install the aks-preview Azure CLI extension

Install or update the Azure CLI preview extension by using the [ az extension add](/en-us/cli/azure/extension#az-extension-add) or

[command.](/en-us/cli/azure/extension#az-extension-update)

`az extension update`

```
# Install the aks-preview extension
az extension add --name aks-preview
# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```


### Register the AdvancedNetworkingFlowLogsPreview feature flag

First, register the AdvancedNetworkingFlowLogsPreview feature flag by using the [ az feature register](/en-us/cli/azure/feature#az-feature-register) command:

```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingFlowLogsPreview"
```


Verify successful registration by using the [ az feature show](/en-us/cli/azure/feature#az-feature-show) command. It takes a few minutes for registration to complete.

```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingFlowLogsPreview"
```


When the feature shows **Registered**, refresh the registration of the `Microsoft.ContainerService`

resource provider by using the [ az provider register](/en-us/cli/azure/provider#az-provider-register) command.

## Limitations

- Layer 7 flow data is captured only when Layer 7 policy support is enabled. For more information, see
[Configure a Layer 7 policy](how-to-apply-l7-policies). - Domain Name System (DNS) flows and related metrics are captured only when a Cilium Fully Qualified Domain (FQDN) network policy is applied. For more information, see
[Configure an FQDN policy](how-to-apply-fqdn-filtering-policies). - Onboarding by using Terraform isn't supported at this time.
- When Log Analytics isn't configured for log storage, container network logs are limited to a maximum of 50 MB of storage. When this limit is reached, new entries overwrite older logs.
- If the log table plan is set to Basic logs, the prebuilt Grafana dashboards don't function as expected.
- The Auxiliary logs table plan isn't supported.

## Configure stored logs mode for container network logs

### Deployment methods

You can onboard to container network logs using different deployment methods:

This section provides two paths for setting up container network logs based on your current situation:

: Complete setup for new AKS clusters[New clusters](#new-clusters): Enable container network logs on existing AKS clusters[Existing clusters](#existing-clusters)

## New clusters

This section guides you through setting up container network logs on a new AKS cluster from start to finish.

### Create a new AKS cluster with Advanced Container Networking Services

Use the `az aks create`

command with the `--enable-acns`

flag to create a new AKS cluster that has all Advanced Container Networking Services features. These features include:

**Container Network Observability:**Provides insight into your network traffic. To learn more, see[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more, see[Container Network Security](advanced-container-networking-services-overview#container-network-security).

```
# Set an environment variable for the AKS cluster name. Make sure you replace the placeholder with your own value.
export CLUSTER_NAME="<aks-cluster-name>"
export RESOURCE_GROUP="<aks-resource-group>"
export LOCATION="<location>"
# Create the resource group if it doesn't already exist
az group create --name $RESOURCE_GROUP --location $LOCATION
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--location $LOCATION \
--max-pods 250 \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--node-count 2 \
--pod-cidr 192.168.0.0/16 \
--kubernetes-version 1.33 or later \
--enable-acns
```


### Configure custom resources for log filtering

To configure container network logs in stored logs mode, you must define specific custom resources to set filters for log collection. When at least one custom resource is defined, logs are collected and stored on the host node at `/var/log/acns/hubble/events.log`

.

To configure logging, you must define and apply the `ContainerNetworkLog`

type of custom resource. You set filters like namespace, pod, service, port, protocol, and verdict. Multiple custom resources can exist in a cluster simultaneously. If no custom resource is defined with nonempty filters, no logs are saved in the designated location.

The following sample definition demonstrates how to configure the `ContainerNetworkLog`

type of custom resource.

### ContainerNetworkLog CRD template

```
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkLog
metadata:
name: sample-containernetworklog # Cluster scoped
spec:
includefilters: # List of filters
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
```


The following table describes the fields in the custom resource definition:

| Field | Type | Description | Required |
|---|---|---|---|
`includefilters` |
[]filter | A list of filters that define network flows to include. Each filter specifies the source, destination, protocol, and other matching criteria. Include filters can't be empty and must have at least one filter. | Mandatory |
`filters.name` |
String | The name of the filter. | Optional |
`filters.protocol` |
[]string | The protocols to match for this filter. Valid values are `tcp` , `udp` , and `dns` . This parameter is optional. If not specified, logs with all protocols are included. |
Optional |
`filters.verdict` |
[]string | The verdict of the flow to match. Valid values are `forwarded` and `dropped` . This parameter is optional. If not specified, logs with all verdicts are included. |
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

Apply the

`ContainerNetworkLog`

custom resource to enable log collection at the cluster:`kubectl apply -f <crd.yaml>`

Tip

For a practical example of a ContainerNetworkLog custom resource configuration, see the

[sample CRD in the AKS Labs documentation](https://azure-samples.github.io/aks-labs/docs/networking/acns-lab/#enable-flow-logs-for-the-pets-namespace).

Logs stored locally on host nodes are temporary because the host or node itself isn't a persistent storage solution. Logs on host nodes are also rotated when their size reaches 50 MB. For longer-term storage and analysis, we recommend that you configure the Azure Monitor Agent on the cluster to collect and retain logs in the Log Analytics workspace.

Alternatively, you can integrate a partner logging service like an OpenTelemetry collector for more log management options.

### Configure Azure Monitor for managed storage (recommended)

For persistent storage and advanced analytics, configure the Azure Monitor Agent to collect and store logs in a Log Analytics workspace:

```
# Set an environment variable for the AKS cluster name. Make sure you replace the placeholder with your own value.
export CLUSTER_NAME="<aks-cluster-name>"
export RESOURCE_GROUP="<aks-resource-group>"
# Enable azure monitor with high log scale mode
### To use the default Log Analytics workspace
az aks enable-addons -a monitoring --enable-high-log-scale-mode -g $RESOURCE_GROUP -n $CLUSTER_NAME
### To use an existing Log Analytics workspace
az aks enable-addons -a monitoring --enable-high-log-scale-mode -g $RESOURCE_GROUP -n $CLUSTER_NAME --workspace-resource-id <workspace-resource-id>
# Update the AKS cluster with the enable-container-network-logs flag
az aks update --enable-acns \
--enable-container-network-logs \
-g $RESOURCE_GROUP \
-n $CLUSTER_NAME
```


Note

When enabled, container network flow logs are written to `/var/log/acns/hubble/events.log`

when the `ContainerNetworkLog`

custom resource is applied. If Log Analytics integration is enabled later, the Azure Monitor Agent begins collecting logs at that point. Logs older than two minutes aren't ingested. Only new entries that are appended after monitoring begins are collected in a Log Analytics workspace.

## Existing clusters

Note

If your cluster already has Advanced Container Networking Services (ACNS) enabled, you can start collecting flow logs on the host node by simply applying a ContainerNetworkLog CRD. However, if you want to enable flow logs with Log Analytics workspace integration for persistent storage and advanced analytics, follow the steps in the [Configure integration with log analytics on existing cluster](#configure-integration-with-log-analytics-on-existing-cluster) section.

```
# Set environment variables for your existing cluster. Make sure you replace the placeholders with your own values.
export CLUSTER_NAME="<aks-cluster-name>"
export RESOURCE_GROUP="<aks-resource-group>"
```


### Configure integration with log analytics on existing cluster

To enable container network logs on an existing cluster:

Check whether monitoring add-ons are already enabled on that cluster:

`az aks addon list -g $RESOURCE_GROUP -n $CLUSTER_NAME`

If monitoring add-ons are enabled, disable monitoring add-ons:

`az aks disable-addons -a monitoring -g $RESOURCE_GROUP -n $CLUSTER_NAME`

Complete this step because monitoring add-ons might already be enabled, but not for high scale. For more information, see

[High-scale mode](/en-us/azure/azure-monitor/containers/container-insights-high-scale).Set Azure Monitor to

`enable-high-log-scale-mode`

:`### Use default Log Analytics workspace az aks enable-addons -a monitoring --enable-high-log-scale-mode -g $RESOURCE_GROUP -n $CLUSTER_NAME ### Use existing Log Analytics workspace az aks enable-addons -a monitoring --enable-high-log-scale-mode -g $RESOURCE_GROUP -n $CLUSTER_NAME --workspace-resource-id <workspace-resource-id>`

Update the AKS cluster with the

`enable-container-network-logs`

flag:`az aks update --enable-acns \ --enable-container-network-logs \ -g $RESOURCE_GROUP \ -n $CLUSTER_NAME`

Create the CRD as per the

[ContainerNetworkLog template](#containernetworklog-crd-template)mentioned above and apply it to start log collection in log analytics workspace.Tip

For a practical example of a ContainerNetworkLog custom resource configuration, see the

[sample CRD in the AKS Labs documentation](https://azure-samples.github.io/aks-labs/docs/networking/acns-lab/#enable-flow-logs-for-the-pets-namespace).

**Viewing L7 flows and DNS errors**

To capture Layer 7 (L7) flow data and DNS errors/flows in your container network logs, you must apply Cilium network policies with FQDN filtering and L7 policy support enabled. Without these policies, L7 and DNS-related flow information won't be captured.

Example of a Cilium network policy with FQDN filtering and L7 support:

```
apiVersion: cilium.io/v2
kind: CiliumNetworkPolicy
metadata:
name: l7-dns-policy
namespace: default
spec:
endpointSelector:
matchLabels:
app: myapp
egress:
- toEndpoints:
- matchLabels:
"k8s:io.kubernetes.pod.namespace": kube-system
"k8s:k8s-app": kube-dns
toPorts:
- ports:
- port: "53"
protocol: UDP
rules:
dns:
- matchPattern: "*.example.com"
- toFQDNs:
- matchPattern: "*.example.com"
toPorts:
- ports:
- port: "443"
protocol: TCP
rules:
http:
- method: "GET"
path: "/1"
```


Apply the policy using:

```
kubectl apply -f l7-dns-policy.yaml
```


For more information, see [Configure a Layer 7 policy](how-to-apply-l7-policies) and [Configure an FQDN policy](how-to-apply-fqdn-filtering-policies)

## Common post-setup steps to verify configuration

The following steps apply to both new and existing cluster setups.

### Get cluster credentials

Get your cluster credentials by using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command:

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


### Validate the setup

Validate that the retina network flow log capability is enabled:

```
az aks show -g $RESOURCE_GROUP -n $CLUSTER_NAME
```


Expected output:

```
"networkProfile":{
"advancedNetworking": {
"enabled": true,
"observability":{
"enabled": true
}
}
}
----------------------------
"osmagent":{
"config":{
"enableContainerNetworkLogs": "True"
}
}
```


Check which custom resource definitions are installed for flow logs:

```
kubectl get containernetworklog
```


This command lists all the `ContainerNetworkLog`

custom resources created in the cluster.

Validate that the `ContainerNetworkLog`

custom resource is applied:

```
k describe containernetworklog <cr-name>
```


Expect to see a `Spec`

node that contains `Include filters`

and a `Status`

node. The value for `Status`

> `State`

should be `CONFIGURED`

(not `FAILED`

).

```
Spec:
Includefilters:
From:
Namespaced Pod:
namespace/pod-
Name: sample-filter
Protocol:
tcp
To:
Namespaced Pod:
namespace/pod-
Verdict:
dropped
Status:
State: CONFIGURED
Timestamp: 2025-05-01T11:24:48Z
```


Users can apply multiple `ContainerNetworkLog`

custom resources in the cluster. Each custom resource has its own status.

### Querying Container Network Flow Logs in Log Analytics dashboard

When Container Network Flow Logs are enabled with a Log Analytics workspace, you have access to historical logs that allow you to analyze network traffic patterns over time. You can query these logs using the `ContainerNetworkLog`

table to perform detailed forensic analysis and troubleshooting.

Customers can use Kusto Query Language (KQL) to analyze network data in Log Analytics. This historical data is invaluable for understanding network behavior patterns, identifying security incidents, troubleshooting connectivity issues, and performing root cause analysis over extended periods. The ability to correlate network events across time helps detect intermittent issues and understand traffic flows that may not be apparent in real-time monitoring.

To see sample queries that can be applied for troubleshooting connectivity issues, refer to the [progressive diagnosis using flow logs](https://azure-samples.github.io/aks-labs/docs/networking/acns-lab/#progressive-diagnosis-using-flow-logs) in the AKS Labs documentation.

### Azure Managed Grafana

You can access prebuilt Grafana dashboards through the Azure portal. Navigate to either the Azure Monitor resource or your Azure Kubernetes Service (AKS) cluster to view and interact with these dashboards. But before that:

Make sure that the Azure logs pods are running:

`kubectl get pods -o wide -n kube-system | grep ama-logs`

Your output should look similar to the following example:

`ama-logs-9bxc6 3/3 Running 1 (39m ago) 44m ama-logs-fd568 3/3 Running 1 (40m ago) 44m ama-logs-rs-65bdd98f75-hqnd2 2/2 Running 1 (43m ago) 22h`

Ensure that your Managed Grafana workspace can access and search all monitoring data in the relevant subscription. This step is required to access prebuilt dashboards for network flow logs.

**Use case 1**: If you're a subscription Owner or a User Access Administrator, when a Managed Grafana workspace is created, it comes with the Monitoring Reader role granted on all Azure Monitor data and Log Analytics resources in the subscription. The new Managed Grafana workspace can access and search all monitoring data in the subscription. It can view the Azure Monitor metrics and logs from all resources and view any logs stored in Log Analytics workspaces in the subscription.**Use case 2**: If you're not a subscription Owner or User Access Administrator, or if your Log Analytics and Managed Grafana workspaces are in different subscriptions, Grafana can't access Log Analytics and the subscription. The Grafana workspace must have the Monitoring Reader role in the relevant subscription to access prebuilt Grafana dashboards. In this scenario, complete these steps to provide access:In your Managed Grafana workspace, go to

**Settings**>**Identity**.Select

**Azure role assignments**>**Add role assignments**.For

**Scope**, enter**Subscription**. Select your subscription. Set**Role**to**Monitoring Reader**, and then select**Save**.Verify the data source for the Managed Grafana instance. To verify the subscription for the data source for the Grafana dashboards, check the

**Data source**tab in the Managed Grafana instance:


#### Visualization in Grafana dashboards

Azure Monitor dashboards with Grafana enable you to use Grafana's query, transformation, and visualization capabilities on metrics and logs collected in Azure Monitor. You can use this option as an alternative to visualize container network flow logs.

- Navigate to the left pane of the Kubernetes cluster in the Azure portal.
- Select
**Dashboards with Grafana (Preview)**. - Browse the list of available dashboards in the Azure Monitor or Azure Managed Prometheus listings.
- Select a dashboard, for example
**Azure | Insights | Containers | Networking | Flow Logs**.

You can visualize container network flow logs for analysis by using two prebuilt Grafana dashboards. You can access the dashboards either through Azure Managed Grafana or in the Azure portal.

To simplify log analysis, we provide two preconfigured Azure Managed Grafana dashboards:

Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs**. This dashboard provides visualizations in which AKS workloads communicate with each other, including network requests, responses, drops, and errors. Currently, you must use[ID 23155](https://grafana.com/grafana/dashboards/23155-azure-insights-containers-networking-flow-logs//)to import these dashboards.Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs (External Traffic)**. This dashboard provides visualizations in which AKS workloads send and receive communications from outside an AKS cluster, including network requests, responses, drops, and errors. Use[ID 23156](https://grafana.com/grafana/dashboards/23156-azure-insights-containers-networking-flow-logs-external-traffic//).

For more information about how to use this dashboard, see the [overview of container network logs](container-network-observability-logs).

## Configure on-demand logs mode

On-demand logs mode for network flows works with both Cilium and non-Cilium data planes.

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. The features include:

**Container Network Observability:**Provides insights into your network traffic. To learn more, visit[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more, visit[Container Network Security](advanced-container-networking-services-overview#container-network-security).

Note

Clusters that have the Cilium data plane support the Container Network Observability and Container Network Security features in Kubernetes version 1.29 and later.

```
# Set an environment variable for the AKS cluster name. Make sure you replace the placeholder with your own value.
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
--kubernetes-version 1.33 \
--enable-acns
```


### Enable Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--enable-acns`

flag updates an existing AKS cluster with all Advanced Container Networking Services features. The features include [Container Network Observability](advanced-container-networking-services-overview#container-network-observability)and

[Container Network Security](advanced-container-networking-services-overview#container-network-security).

Note

Only clusters that have the Cilium data plane support the Container Network Security features of Advanced Container Networking Services.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns
```


Next, get your cluster credentials by using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command:

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


### Install the Hubble CLI

Install the Hubble CLI to access the data it collects. Run the following commands:

```
# Set environment variables
export HUBBLE_VERSION=v1.16.3
export HUBBLE_ARCH=amd64
#Install the Hubble CLI
if [ "$(uname -m)" = "aarch64" ]; then HUBBLE_ARCH=arm64; fi
curl -L --fail --remote-name-all https://github.com/cilium/hubble/releases/download/$HUBBLE_VERSION/hubble-linux-${HUBBLE_ARCH}.tar.gz{,.sha256sum}
sha256sum --check hubble-linux-${HUBBLE_ARCH}.tar.gz.sha256sum
sudo tar xzvfC hubble-linux-${HUBBLE_ARCH}.tar.gz /usr/local/bin
rm hubble-linux-${HUBBLE_ARCH}.tar.gz{,.sha256sum}
```


### Visualize the Hubble flows

Make sure that the Hubble pods are running:

`kubectl get pods -o wide -n kube-system -l k8s-app=hubble-relay`

Your output should look similar to the following example:

`hubble-relay-7ddd887cdb-h6khj 1/1 Running 0 23h`

Port-forward the Hubble Relay server:

`kubectl port-forward -n kube-system svc/hubble-relay --address 127.0.0.1 4245:443`

Mutual TLS (mTLS) ensures the security of the Hubble Relay server. To enable the Hubble client to retrieve flows, you must get the appropriate certificates and configure the client with them. Apply the certificates by using the following commands:

`#!/usr/bin/env bash set -euo pipefail set -x # Directory where certificates will be stored CERT_DIR="$(pwd)/.certs" mkdir -p "$CERT_DIR" declare -A CERT_FILES=( ["tls.crt"]="tls-client-cert-file" ["tls.key"]="tls-client-key-file" ["ca.crt"]="tls-ca-cert-files" ) for FILE in "${!CERT_FILES[@]}"; do KEY="${CERT_FILES[$FILE]}" JSONPATH="{.data['${FILE//./\\.}']}" # Retrieve the secret and decode it kubectl get secret hubble-relay-client-certs -n kube-system \ -o jsonpath="${JSONPATH}" | \ base64 -d > "$CERT_DIR/$FILE" # Set the appropriate hubble CLI config hubble config set "$KEY" "$CERT_DIR/$FILE" done hubble config set tls true hubble config set tls-server-name instance.hubble-relay.cilium.io`

Confirm that the secrets were generated:

`kubectl get secrets -n kube-system | grep hubble-`

Your output should look similar to the following example:

`kube-system hubble-relay-client-certs kubernetes.io/tls 3 9d kube-system hubble-relay-server-certs kubernetes.io/tls 3 9d kube-system hubble-server-certs kubernetes.io/tls 3 9d`

Verify that the Hubble Relay pod is running:

`hubble observe --pod hubble-relay-7ddd887cdb-h6khj`


### Visualize by using the Hubble UI

To use the Hubble UI, save the following script in the

`hubble-ui.yaml`

file:`apiVersion: v1 kind: ServiceAccount metadata: name: hubble-ui namespace: kube-system --- kind: ClusterRole apiVersion: rbac.authorization.k8s.io/v1 metadata: name: hubble-ui labels: app.kubernetes.io/part-of: retina rules: - apiGroups: - networking.k8s.io resources: - networkpolicies verbs: - get - list - watch - apiGroups: - "" resources: - componentstatuses - endpoints - namespaces - nodes - pods - services verbs: - get - list - watch - apiGroups: - apiextensions.k8s.io resources: - customresourcedefinitions verbs: - get - list - watch - apiGroups: - cilium.io resources: - "*" verbs: - get - list - watch --- apiVersion: rbac.authorization.k8s.io/v1 kind: ClusterRoleBinding metadata: name: hubble-ui labels: app.kubernetes.io/part-of: retina roleRef: apiGroup: rbac.authorization.k8s.io kind: ClusterRole name: hubble-ui subjects: - kind: ServiceAccount name: hubble-ui namespace: kube-system --- apiVersion: v1 kind: ConfigMap metadata: name: hubble-ui-nginx namespace: kube-system data: nginx.conf: | server { listen 8081; server_name localhost; root /app; index index.html; client_max_body_size 1G; location / { proxy_set_header Host $host; proxy_set_header X-Real-IP $remote_addr; # CORS add_header Access-Control-Allow-Methods "GET, POST, PUT, HEAD, DELETE, OPTIONS"; add_header Access-Control-Allow-Origin *; add_header Access-Control-Max-Age 1728000; add_header Access-Control-Expose-Headers content-length,grpc-status,grpc-message; add_header Access-Control-Allow-Headers range,keep-alive,user-agent,cache-control,content-type,content-transfer-encoding,x-accept-content-transfer-encoding,x-accept-response-streaming,x-user-agent,x-grpc-web,grpc-timeout; if ($request_method = OPTIONS) { return 204; } # /CORS location /api { proxy_http_version 1.1; proxy_pass_request_headers on; proxy_hide_header Access-Control-Allow-Origin; proxy_pass http://127.0.0.1:8090; } location / { try_files $uri $uri/ /index.html /index.html; } # Liveness probe location /healthz { access_log off; add_header Content-Type text/plain; return 200 'ok'; } } } --- kind: Deployment apiVersion: apps/v1 metadata: name: hubble-ui namespace: kube-system labels: k8s-app: hubble-ui app.kubernetes.io/name: hubble-ui app.kubernetes.io/part-of: retina spec: replicas: 1 selector: matchLabels: k8s-app: hubble-ui template: metadata: labels: k8s-app: hubble-ui app.kubernetes.io/name: hubble-ui app.kubernetes.io/part-of: retina spec: serviceAccountName: hubble-ui automountServiceAccountToken: true containers: - name: frontend image: mcr.microsoft.com/oss/cilium/hubble-ui:v0.12.2 imagePullPolicy: Always ports: - name: http containerPort: 8081 livenessProbe: httpGet: path: /healthz port: 8081 readinessProbe: httpGet: path: / port: 8081 resources: {} volumeMounts: - name: hubble-ui-nginx-conf mountPath: /etc/nginx/conf.d/default.conf subPath: nginx.conf - name: tmp-dir mountPath: /tmp terminationMessagePolicy: FallbackToLogsOnError securityContext: {} - name: backend image: mcr.microsoft.com/oss/cilium/hubble-ui-backend:v0.12.2 imagePullPolicy: Always env: - name: EVENTS_SERVER_PORT value: "8090" - name: FLOWS_API_ADDR value: "hubble-relay:443" - name: TLS_TO_RELAY_ENABLED value: "true" - name: TLS_RELAY_SERVER_NAME value: ui.hubble-relay.cilium.io - name: TLS_RELAY_CA_CERT_FILES value: /var/lib/hubble-ui/certs/hubble-relay-ca.crt - name: TLS_RELAY_CLIENT_CERT_FILE value: /var/lib/hubble-ui/certs/client.crt - name: TLS_RELAY_CLIENT_KEY_FILE value: /var/lib/hubble-ui/certs/client.key livenessProbe: httpGet: path: /healthz port: 8090 readinessProbe: httpGet: path: /healthz port: 8090 ports: - name: grpc containerPort: 8090 resources: {} volumeMounts: - name: hubble-ui-client-certs mountPath: /var/lib/hubble-ui/certs readOnly: true terminationMessagePolicy: FallbackToLogsOnError securityContext: {} nodeSelector: kubernetes.io/os: linux volumes: - configMap: defaultMode: 420 name: hubble-ui-nginx name: hubble-ui-nginx-conf - emptyDir: {} name: tmp-dir - name: hubble-ui-client-certs projected: defaultMode: 0400 sources: - secret: name: hubble-relay-client-certs items: - key: tls.crt path: client.crt - key: tls.key path: client.key - key: ca.crt path: hubble-relay-ca.crt --- kind: Service apiVersion: v1 metadata: name: hubble-ui namespace: kube-system labels: k8s-app: hubble-ui app.kubernetes.io/name: hubble-ui app.kubernetes.io/part-of: retina spec: type: ClusterIP selector: k8s-app: hubble-ui ports: - name: http port: 80 targetPort: 8081`

Apply the

`hubble-ui.yaml`

manifest to your cluster:`kubectl apply -f hubble-ui.yaml`

Set up port forwarding for the Hubble UI:

`kubectl -n kube-system port-forward svc/hubble-ui 12000:80`

In your web browser, enter

`http://localhost:12000/`

to access the Hubble UI.

### Basic troubleshooting

Advanced Container Networking Services is a prerequisite to turn on the Azure Monitor Agent log collection feature.

Trying to enable the container network flow logs capability on a cluster without enabling Advanced Container Networking Services, for example:

`az aks update -g test-rg -n test-cluster --enable-container-network-logs`

Results in an error message:

`Flow logs requires '--enable-acns', advanced networking to be enabled, and the monitoring addon to be enabled.`

If the cluster Kubernetes version is earlier than version 1.33.0, trying to run

`--enable-container-network-logs`

results in an error message:`The specified orchestrator version %s is not valid. Advanced Networking Flow Logs is only supported on Kubernetes version 1.33.0 or later.`

where

`%s`

is your Kubernetes version.If you try to run

`--enable-container-network-logs`

on a subscription where the Azure Feature Exposure Control (AFEC) flag isn't enabled, an error message appears:`Feature Microsoft.ContainerService/AdvancedNetworkingFlowLogsPreview is not enabled. Please see https://aka.ms/aks/previews for how to enable features.`

If you try to apply a

`ContainerNetworkLog`

custom resource on a cluster where Advanced Container Networking Services isn't enabled, an error message appears:`error: resource mapping not found for <....>": no matches for kind "ContainerNetworkLog" in version "acn.azure.com/v1alpha1"`

Ensure that you install custom resources first.


### Disable container network logs: Stored logs mode on existing cluster

If all custom resources are deleted, flow log collection stops because no filters are defined for collection.

To disable container network log collection by the Azure Monitor Agent, run:

```
az aks update -n $CLUSTER_NAME -g $RESOURCE_GROUP --disable-container-network-logs
```


## Clean up resources

If you don't plan to use this example application, delete the resources you created in this article by using the [ az group delete](/en-us/cli/azure/#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP
```


## Related content

- Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/support-policies -->

# Support policies for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes technical support policies and limitations for Azure Kubernetes Service (AKS). It also details agent node management, managed control plane components, third-party open-source components, and security or patch management.

## Service updates and releases

- For release information, see
[AKS release notes](https://github.com/Azure/AKS/releases). - For information on preview features, see the
[AKS roadmap](https://github.com/Azure/AKS/projects/1).

## Managed features in AKS

Base infrastructure as a service (IaaS) cloud components, like compute or networking components, allow you access to low-level controls and customization options. By contrast, AKS provides a turnkey Kubernetes deployment that gives you a common set of configurations and capabilities you need for your cluster. As an AKS user, you have limited customization and deployment options. In exchange, you don't need to worry about or manage Kubernetes clusters directly.

With AKS, you get a fully managed *control plane*. The control plane contains all of the components and services you need to operate and deliver Kubernetes clusters to end users. Microsoft maintains and operates all Kubernetes components.

Microsoft manages and monitors the following components through the control plane:

- Kubelet or Kubernetes API servers.
`etcd`

or a compatible key-value store, providing Quality of Service (QoS), scalability, and runtime.- DNS services like kube-dns or CoreDNS.
- Kubernetes proxy or networking, except when
[BYOCNI](use-byo-cni)is used. - Any other
[add-ons](integrations#add-ons)or system component running in the kube-system namespace.

AKS isn't a Platform-as-a-Service (PaaS) solution. Some components, like agent nodes, have *shared responsibility*, where you must help maintain the AKS cluster. User input is required, for example, to apply an agent node operating system (OS) security patch.

The services are *managed* in the sense that Microsoft and the AKS team deploys, operates, and is responsible for service availability and functionality. Customers can't alter these managed components. Microsoft limits customization to ensure a consistent and scalable user experience.

## Shared responsibility

When a cluster is created, you define the Kubernetes agent nodes that AKS creates. Your workloads are executed on these nodes.

Because your agent nodes execute private code and store sensitive data, Microsoft Support can access them only in a limited way. Microsoft Support can't sign in to, execute commands in, or view logs for these nodes without your express permission or assistance.

Any modification made directly to the agent nodes using any one of the IaaS APIs renders the cluster unsupportable. Any modification applied to the agent nodes must be done using kubernetes-native mechanisms like a `DaemonSet`

.

Similarly, while you might add any metadata to the cluster and nodes, like tags and labels, changing any of the system created metadata renders the cluster unsupported.

## AKS support coverage

The following sections describe the supported and unsupported scenarios for AKS technical support.

### Supported scenarios

Microsoft provides technical support for the following examples:

- Connectivity to all Kubernetes components that the Kubernetes service provides and supports, like the API server.
- Management, uptime, QoS, and operations of Kubernetes control plane services like Kubernetes control plane, API server,
`etcd`

, and coreDNS. `etcd`

data store. Support includes automated, transparent backups of all`etcd`

data every 30 minutes for disaster planning and cluster state restoration. These backups aren't directly available to you or anyone else. They ensure data reliability and consistency. On-demand rollback or restore isn't supported as a feature.- Any integration points in the Azure cloud provider driver for Kubernetes. These include integrations into other Azure services like load balancers, persistent volumes, or networking (Kubernetes and Azure CNI, except when
[BYOCNI](use-byo-cni)is in use). - Questions or issues about customization of control plane components like the Kubernetes API server,
`etcd`

, and coreDNS. - Issues about networking, like Azure CNI, kubenet, or other network access and functionality issues, except when
[BYOCNI](use-byo-cni)is in use. Issues could include DNS resolution, packet loss, routing, and so on. Microsoft supports various networking scenarios:- Kubenet and Azure CNI using managed VNETs or with custom (bring your own) subnets.
- Connectivity to other Azure services and applications.
- Microsoft-managed ingress controllers or load balancer configurations.
- Network performance and latency.
- Microsoft-managed
[network policies](use-network-policies#differences-between-network-policy-engines-cilium-azure-npm-and-calico)components and functionalities.


Any cluster actions taken by Microsoft/AKS are made with your consent under a built-in Kubernetes role `aks-service`

and built-in role binding `aks-service-rolebinding`

. This role enables AKS to troubleshoot and diagnose cluster issues, but can't modify permissions nor create roles or role bindings, or other high privilege actions. Role access is only enabled under active support tickets with just-in-time (JIT) access.

### Unsupported scenarios

Microsoft doesn't provide technical support for the following scenarios:

Questions about how to use Kubernetes. For example, Microsoft Support doesn't provide advice on how to create custom ingress controllers, use application workloads, or apply third-party or open-source software packages or tools.

Microsoft Support can advise on AKS cluster functionality, customization, and tuning (for example, Kubernetes operations issues and procedures).

Third-party open-source projects that aren't provided as part of the Kubernetes control plane or deployed with AKS clusters. These projects might include Istio, Helm, Envoy, or others.

Microsoft can provide best-effort support for third-party open-source projects like Helm. Where the third-party open-source tool integrates with the Kubernetes Azure cloud provider or other AKS-specific bugs, Microsoft supports examples and applications from Microsoft documentation.

Third-party closed-source software. This software can include security scanning tools and networking devices or software.

Configuring or troubleshooting application-specific code or behavior of third-party applications or tools running within the AKS cluster. This includes application deployment issues not related to the AKS platform itself.

Issuance, renewal, or management of certificates for applications running on AKS.

Network customizations other than the ones listed in the

[AKS documentation](./). For example, Microsoft Support can't configure devices or virtual appliances meant to provide[outbound traffic](outbound-rules-control-egress)for the AKS cluster, like VPNs or firewalls.On a best-effort basis, Microsoft Support might advise on the

[configuration needed](outbound-rules-control-egress)for Azure Firewall, but not for other third-party devices.Custom or third-party CNI plugins used in

[BYOCNI](use-byo-cni)mode.Configuring or troubleshooting non-Microsoft-managed network policies. While using network policies is supported, Microsoft Support can't investigate issues stemming from custom network policy configurations.

Configuring or troubleshooting non-Microsoft-managed ingress controllers, like

`nginx`

,`kong`

,`traefik`

, etc. This includes addressing functionality issues that arise after AKS-specific operations, like an ingress controller ceasing to work following a Kubernetes version upgrade. Such issues might stem from incompatibilities between the ingress controller version and the new Kubernetes version. For a fully supported option, consider using a[Microsoft-managed ingress controller option](concepts-network-ingress#compare-ingress-options).Configuring or troubleshooting

`DaemonSet`

(including scripts) used to customize node configurations. Although using`DaemonSet`

is the recommended approach to tune, modify, or install third-party software on cluster agent nodes when[configuration file parameters](custom-node-configuration)are insufficient, Microsoft Support can't troubleshoot issues arising from the custom scripts used in`DaemonSet`

due to their custom nature.Stand-by and proactive scenarios. Microsoft Support provides reactive support to help solve active issues in a timely and professional manner. However, standby or proactive support to help you eliminate operational risks, increase availability, and optimize performance aren't covered.

[Eligible customers](https://www.microsoft.com/unifiedsupport)can contact their account team to get nominated for[Azure Event Management service](https://devblogs.microsoft.com/premier-developer/proactively-plan-for-your-critical-event-in-azure-with-enhanced-support-and-engineering-services/). It's a paid service delivered by Microsoft support engineers that includes a proactive solution risk assessment and coverage during the event.Vulnerabilities/CVEs with a vendor fix that's less than 30 days old. As long as you're running the updated VHD, you shouldn't be running any container image vulnerabilities/CVEs with a vendor fix that is over 30 days old. It's customer responsibility to update the VHD and provide filtered lists to Microsoft support. After you update your VHD, it's customer responsibility to filter the vulnerabilities/CVEs report and provide a list only with vulnerabilities/CVEs with a vendor fix that is over 30 days old. If that's the case, Microsoft support will make sure to work internally and address components with a vendor fix released more than 30 days ago. Additionally, Microsoft provides vulnerability/CVE-related support only for Microsoft-managed components. For example, AKS node images, managed container images for applications that are deployed during cluster creation or via the installation of a managed add-on. For more details about vulnerability management for AKS, visit

[Vulnerability management for Azure Kubernetes Service (AKS)](concepts-vulnerability-management).Custom code samples or scripts. While Microsoft Support

*can*provide small code samples and reviews of small code samples within a support case to demonstrate how to use features of a Microsoft product, Microsoft Support*can't*provide custom code samples that are specific to your environment or application.

## AKS support coverage for agent nodes

The following sections describe the Microsoft and customer responsibilities for AKS agent nodes.

### Microsoft responsibilities for AKS agent nodes

Microsoft and you share responsibility for Kubernetes agent nodes where:

- The base OS image has required additions like monitoring and networking agents.
- The agent nodes receive OS patches automatically.
- Issues with the Kubernetes control plane components that run on the agent nodes are automatically remediated. These components include the following items:
`Kube-proxy`

- Networking tunnels that provide communication paths to the Kubernetes master components
`Kubelet`

`containerd`


If an agent node isn't operational, AKS might restart individual components or the entire agent node. These restart operations are automated and provide autoremediation for common issues. If you want to know more about the autoremediation mechanisms, see [Node Auto-Repair](node-auto-repair).

### Customer responsibilities for AKS agent nodes

Microsoft provides patches and new images for your image nodes weekly. To keep your agent node OS and runtime components up to date, you should apply these patches and updates regularly either manually or automatically. For more information, see:

Similarly, AKS regularly releases new Kubernetes patches and minor versions. These updates can contain security or functionality improvements to Kubernetes. You're responsible to keep your clusters' Kubernetes version updated and according to the [AKS Kubernetes support version policy](supported-kubernetes-versions).

#### User customization of agent nodes

Note

AKS agent nodes appear in the Azure portal as standard Azure IaaS resources. However, these virtual machines are deployed into a custom Azure resource group (prefixed with `MC_\*`

). You can't change the base OS image or make any direct customizations to these nodes using the IaaS APIs or resources. Any custom changes that aren't performed from the AKS API don't persist through an upgrade, scale, update, or reboot. Also, any change to the nodes' extensions like the `CustomScriptExtension`

can lead to unexpected behavior and should be prohibited.
Avoid performing changes to the agent nodes unless Microsoft Support directs you to make changes.

AKS manages the lifecycle and operations of agent nodes on your behalf and modifying the IaaS resources associated with the agent nodes is **not supported**. An example of an unsupported operation is customizing a node pool virtual machine scale set by manually changing configurations in the Azure portal or from the API.

For workload-specific configurations or packages, AKS recommends using a [Kubernetes DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/).

Using Kubernetes privileged `DaemonSet`

and `init`

containers enables you to tune/modify or install third party software on cluster agent nodes. Examples of such customizations include adding custom security scanning software or updating sysctl settings.

While this path is recommended if the above requirements apply, AKS engineering and support can't help troubleshoot or diagnose modifications that render the node unavailable due to a custom deployed `DaemonSet`

.

### Security issues and patching

If a security flaw is found in one or more of the managed components of AKS, the AKS team patches all affected clusters to mitigate the issue. Alternatively, the AKS team provides you with upgrade guidance.

For agent nodes affected by a security flaw, Microsoft notifies you with details on the impact and the steps to fix or mitigate the security issue.

### Node maintenance and access

Although you can sign in to and change agent nodes, doing this operation is discouraged because changes can make a cluster unsupportable.

## Network ports, access, and NSGs

You might only customize the NSGs on custom subnets. You might not customize NSGs on managed subnets or at the NIC level of the agent nodes. AKS has egress requirements to specific endpoints, to control egress and ensure the necessary connectivity, see [limit egress traffic](limit-egress-traffic). For ingress, the requirements are based on the applications you deployed to the cluster.

## Stopped, deallocated, and Not Ready nodes

If you don't need your AKS workloads to run continuously, you can [stop the AKS cluster](start-stop-cluster#stop-an-aks-cluster), which stops all node pools and the control plane. You can start it again when needed. When you stop a cluster using the `az aks stop`

command, the cluster state is preserved for up to 12 months. After 12 months, the cluster state and all of its resources are deleted.

Manually deallocating all cluster nodes from the IaaS APIs, the Azure CLI, or the Azure portal isn't supported to stop an AKS cluster or node pool. The cluster will be considered out of support and stopped by AKS after 30 days. The clusters are then subject to the same 12 month preservation policy as a correctly stopped cluster.

Clusters with zero **Ready** nodes (or all **Not Ready**) and zero **Running** VMs will be stopped after 30 days.

AKS reserves the right to archive control planes that have been configured out of support guidelines for extended periods equal to and beyond 30 days. AKS maintains backups of cluster `etcd`

metadata and can readily reallocate the cluster. This reallocation is initiated by any PUT operation bringing the cluster back into support, like an upgrade or scale to active agent nodes.

All clusters in a suspended subscription will be stopped immediately and deleted after 90 days. All clusters in a deleted subscription will be deleted immediately.

## Unsupported alpha and beta Kubernetes features

AKS only supports stable and beta features within the upstream Kubernetes project. Unless otherwise documented, AKS doesn't support any alpha feature that's available in the upstream Kubernetes project.

## Preview features or feature flags

For features and functionality that requires extended testing and user feedback, Microsoft releases new preview features or features behind a feature flag. Consider these features as prerelease or beta features.

Preview features or feature-flag features aren't meant for production. Ongoing changes in APIs and behavior, bug fixes, and other changes can result in unstable clusters and downtime.

Features in public preview fall under **best effort** support, as these features are in preview and aren't meant for production. The AKS technical support teams provide support during business hours only. For more information, see [Azure Support FAQ](https://azure.microsoft.com/support/faq/).

## Upstream bugs and issues

Given the speed of development in the upstream Kubernetes project, bugs invariably arise. Some of these bugs can't be patched or worked around within the AKS system. Instead, bug fixes require larger patches to upstream projects (like Kubernetes, node or agent operating systems, and kernel). For components that Microsoft owns (like the Azure cloud provider), AKS and Azure personnel are committed to fixing issues upstream in the community.

When the root cause of a technical support issue is due to one or more upstream bugs, AKS support and engineering teams will:

- Identify and link the upstream bugs with any supporting details to help explain why this issue affects your cluster or workload. Customers receive links to the required repositories so they can watch the issues and see when a new release provides fixes.
- Provide potential workarounds or mitigation. If the issue can be mitigated, a
[known issue](https://github.com/Azure/AKS/issues?q=is%3Aissue+is%3Aopen+label%3Aknown-issue)is filed in the AKS repository. The known-issue filing explains:- The issue, including links to upstream bugs.
- The workaround and details about an upgrade or another persistence of the solution.
- Rough timelines for the issue's inclusion, based on the upstream release cadence.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-azure-container-storage -->

# Tutorial - Deploy Azure Container Storage (version 1.x.x) on an AKS cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This tutorial introduces Azure Container Storage and demonstrates how to deploy and manage container-native storage for applications running on Azure Kubernetes Service (AKS). If you don't want to deploy Azure Container Storage now, you can skip this tutorial and proceed directly to [Deploy an application in AKS](tutorial-kubernetes-deploy-application). You won't need Azure Container Storage for the basic storefront application in this tutorial series.

Important

This article explains how to install Azure Container Storage (version 1.x.x), which now explicitly requires a version pinning parameter `--container-storage-version 1`

for installation. [Azure Container Storage (version 2.x.x)](/en-us/azure/storage/container-storage/container-storage-introduction) is now available.

Azure Container Storage simplifies the management of stateful applications in Kubernetes by offering container-native storage tailored to a variety of workloads, including databases, analytics platforms, and high-performance applications.

By the end of this tutorial, you will:

- Understand how Azure Container Storage supports diverse workloads in Kubernetes.
- Explore multiple storage backend options to tailor storage to your application's needs.
- Deploy Azure Container Storage (version 1.x.x) on your AKS cluster and create a generic ephemeral volume.

## Before you begin

In previous tutorials, you created a container image, uploaded it to an ACR instance, and created an AKS cluster. Start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app) to follow along.

- This tutorial requires using the Azure CLI version 2.35.0 or later. Portal and PowerShell aren't currently supported for Azure Container Storage. Check your version with
`az --version`

. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). If you're using the Bash environment in Azure Cloud Shell, the latest version is already installed. - You must have an existing Linux-based AKS cluster with at least 3 nodes with
[Storage optimized VM SKUs](/en-us/azure/virtual-machines/sizes/overview#storage-optimized)or[GPU accelerated VM SKUs](/en-us/azure/virtual-machines/sizes/overview#gpu-accelerated). See[Tutorial 3 - Create an AKS cluster](tutorial-kubernetes-deploy-cluster). - You'll need the Kubernetes command-line client,
`kubectl`

. It's already installed if you're using Azure Cloud Shell, or you can install it locally by running the`az aks install-cli`

command.

## Install the Kubernetes extension

Add or upgrade to the latest version of `k8s-extension`

by running the following command.

```
az extension add --upgrade --name k8s-extension
```


## Connect to the cluster and check node status

If you're not already connected to your cluster from the previous tutorial, run the following commands. If you're already connected, you can skip this section.

Run the following command to connect to the cluster.

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using the

`kubectl get`

command. This command returns a list of the cluster nodes.`kubectl get nodes`

The following output example shows the nodes in your cluster. Make sure the status for all nodes shows

*Ready*:`NAME STATUS ROLES AGE VERSION aks-nodepool1-34832848-vmss000000 Ready agent 80m v1.30.9 aks-nodepool1-34832848-vmss000001 Ready agent 80m v1.30.9 aks-nodepool1-34832848-vmss000002 Ready agent 80m v1.30.9`


## Choose a backing storage option

Azure Container Storage (version 1.x.x) uses storage pools to provision and manage persistent and generic volumes. It offers a variety of back-end storage options for your storage pools, each suited for specific workloads. Selecting the right storage type is critical for optimizing workload performance, durability, and cost efficiency. For this tutorial, we'll use Ephemeral Disk with local NVMe as backing storage to create a generic ephemeral volume. However, we'll also explore the other backing storage options that allow you to create persistent volumes.

### Ephemeral Disk

Ephemeral Disk utilizes local storage resources on the AKS nodes (either local NVMe or temp SSD). It offers low sub-ms latency and high IOPS, but no data persistence if the VM restarts. Ephemeral Disk is best suited for applications such as Cassandra that prioritize speed over persistence, and is ideal for workloads with their own application-level replication.

You can use Ephemeral Disk to create either generic ephemeral volumes or persistent volumes, even though the data will be lost if the VM restarts.

### Azure Disks

Ideal for databases like PostgreSQL and MongoDB, Azure Disks offer durability, scalability, and multi-tiered performance options, including Premium SSD and Ultra SSD.

Azure Disks allow for automatic provisioning of storage volumes and include built-in redundancy and high availability.

### Azure Elastic SAN (preview)

Designed for shared storage needs and general-purpose databases requiring scalability and high availability, Azure Elastic SAN is a good fit for workloads such as CI/CD pipelines or large-scale data processing.

## Enable Azure Container Storage (version 1.x.x) and create a storage pool

Run the following command to install Azure Container Storage on the cluster and create a Local NVMe storage pool.

```
az aks update -n myAKSCluster -g myResourceGroup --enable-azure-container-storage ephemeralDisk --container-storage-version 1 --storage-pool-option NVMe
```


The deployment should take less than 15 minutes.

### Verify the storage pool status

When deployment completes, the components for your chosen storage pool type will be enabled, and you'll have a default storage pool.

To get the list of available storage pools, run the following command:

```
kubectl get sp -n acstor
```


To check the status of a storage pool, run the following command:

```
kubectl describe sp <storage-pool-name> -n acstor
```


If the `Message`

doesn't say `StoragePool is ready`

, then your storage pool is still creating or ran into a problem.

## Display the available storage classes

When the storage pool is ready to use, you must select a storage class to define how storage is dynamically created when creating and deploying volumes.

Run `kubectl get sc`

to display the available storage classes. You should see a storage class called `acstor-<storage-pool-name>`

. Use this storage class in the next section to deploy a pod.

## Deploy a pod with a generic ephemeral volume

Create a pod using [Fio](https://github.com/axboe/fio) (Flexible I/O Tester) for benchmarking and workload simulation, that uses a generic ephemeral volume.

Use your favorite text editor to create a YAML manifest file such as

`code acstor-pod.yaml`

.Paste in the following code and save the file.

`kind: Pod apiVersion: v1 metadata: name: fiopod spec: nodeSelector: acstor.azure.com/io-engine: acstor containers: - name: fio image: nixery.dev/shell/fio args: - sleep - "1000000" volumeMounts: - mountPath: "/volume" name: ephemeralvolume volumes: - name: ephemeralvolume ephemeral: volumeClaimTemplate: metadata: labels: type: my-ephemeral-volume spec: accessModes: [ "ReadWriteOnce" ] storageClassName: acstor-ephemeraldisk-nvme # replace with the name of your storage class if different resources: requests: storage: 1Gi`

If you change the storage size of the volume, make sure the size is less than the available capacity of a single node's ephemeral disk. Run

`kubectl get diskpool -n acstor`

to check the available capacity.Apply the YAML manifest file to deploy the pod.

`kubectl apply -f acstor-pod.yaml`

You should see output similar to the following:

`pod/fiopod created`

Check that the pod is running and that the ephemeral volume claim has been bound successfully to the pod:

`kubectl describe pod fiopod kubectl describe pvc fiopod-ephemeralvolume`


You've now deployed a pod that's using local NVMe as its storage, and you can use it for your Kubernetes workloads.

Verify the available capacity of ephemeral disks before provisioning additional volumes:

```
kubectl describe node <node-name>
```


To learn more about Azure Container Storage (version 1.x.x), including how to create persistent volumes, see [What is Azure Container Storage?](/en-us/azure/storage/container-storage/container-storage-introduction-version-1)

## Clean up resources

You won't need Azure Container Storage for the rest of this tutorial series, so we recommend deleting it now to avoid incurring unnecessary Azure charges.

Delete the pod.

`kubectl delete pod fiopod`

Delete the storage pool.

`kubectl delete sp -n acstor <storage-pool-name>`

Delete the extension instance.

`az aks update -n myAKSCluster -g myResourceGroup --disable-azure-container-storage all`


## Next step

In this tutorial, you deployed Azure Container Storage (version 1.x.x) on your AKS cluster. You learned how to:

- Enable Azure Container Storage (version 1.x.x) on your AKS cluster.
- Choose a backing storage type and create a storage pool.
- Deploy a pod with a generic ephemeral volume.

In the next tutorial, you learn how to deploy an application to your cluster.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-updates-kured -->

# Apply security and kernel updates to Linux nodes in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To protect your clusters, security updates are automatically applied to Linux nodes in AKS. These updates include OS security fixes or kernel updates. Some of these updates require a node reboot to complete the process. AKS doesn't automatically reboot these Linux nodes to complete the update process.

The process to keep Windows Server nodes up to date is a little different. Windows Server nodes don't receive daily updates. Instead, you perform an AKS upgrade that deploys new nodes with the latest base Window Server image and patches. For AKS clusters that use Windows Server nodes, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

This article shows you how to use the open-source [kured (KUbernetes REboot Daemon)](https://github.com/kubereboot/kured) to watch for Linux nodes that require a reboot, then automatically handle the rescheduling of running pods and node reboot process.

Note

`Kured`

is an open-source project in the Cloud Native Computing Foundation. Please direct issues to the [kured GitHub](https://github.com/kubereboot/kured). Additional support can be found in the #kured channel on [CNCF Slack](https://slack.cncf.io).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Before you begin

You need the Azure CLI version 2.0.59 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Understand the AKS node update experience

In an AKS cluster, your Kubernetes nodes run as Azure virtual machines (VMs). These Linux-based VMs use an Ubuntu or Azure Linux image, with the OS configured to automatically check for updates every day. If security or kernel updates are available, they're automatically downloaded and installed.

Some security updates, such as kernel updates, require a node reboot to finalize the process. A Linux node that requires a reboot creates a file named */var/run/reboot-required*. This reboot process doesn't happen automatically.

You can use your own workflows and processes to handle node reboots, or use `kured`

to orchestrate the process. With `kured`

, a [DaemonSet](concepts-clusters-workloads#statefulsets-and-daemonsets) is deployed that runs a pod on each Linux node in the cluster. These pods in the DaemonSet watch for existence of the */var/run/reboot-required* file, and then initiate a process to reboot the nodes.

### Node image upgrades

Unattended upgrades apply updates to the Linux node OS, but the image used to create nodes for your cluster remains unchanged. If a new Linux node is added to your cluster, the original image is used to create the node. This new node receives all the security and kernel updates available during the automatic check every day but remains unpatched until all checks and restarts are complete.

Alternatively, you can use node image upgrade to check for and update node images used by your cluster. For more information on node image upgrade, see [Azure Kubernetes Service (AKS) node image upgrade](node-image-upgrade).

### Node upgrades

There's another process in AKS that lets you *upgrade* a cluster. An upgrade is typically to move to a newer version of Kubernetes, not just apply node security updates. An AKS upgrade performs the following actions:

- A new node is deployed with the latest security updates and Kubernetes version applied.
- An old node is cordoned and drained.
- Pods are scheduled on the new node.
- The old node is deleted.

You can't remain on the same Kubernetes version during an upgrade event. You must specify a newer version of Kubernetes. To upgrade to the latest version of Kubernetes, you can [upgrade your AKS cluster](upgrade-cluster).

## Deploy kured in an AKS cluster

To deploy the `kured`

DaemonSet, install the following official Kured Helm chart. This creates a role and cluster role, bindings, and a service account, then deploys the DaemonSet using `kured`

.

```
# Add the Kured Helm repository
helm repo add kubereboot https://kubereboot.github.io/charts/
# Update your local Helm chart repository cache
helm repo update
# Create a dedicated namespace where you would like to deploy kured into
kubectl create namespace kured
# Install kured in that namespace with Helm 3 (only on Linux nodes, kured is not working on Windows nodes)
helm install my-release kubereboot/kured --namespace kured --set controller.nodeSelector."kubernetes\.io/os"=linux
```


You can also configure extra parameters for `kured`

, such as integration with Prometheus or Slack. For more information about configuration parameters, see the [kured Helm chart](https://github.com/kubereboot/charts/tree/main/charts/kured).

## Update cluster nodes

By default, Linux nodes in AKS check for updates every evening. If you don't want to wait, you can manually perform an update to check that `kured`

runs correctly. First, follow the steps to [SSH to one of your AKS nodes](ssh). Once you have an SSH connection to the Linux node, check for updates and apply them as follows:

```
sudo apt-get update && sudo apt-get upgrade -y
```


If updates were applied that require a node reboot, a file is written to */var/run/reboot-required*. `Kured`

checks for nodes that require a reboot every 60 minutes by default.

## Monitor and review reboot process

When one of the replicas in the DaemonSet detects that a node reboot is required, a lock is placed on the node through the Kubernetes API. This lock prevents more pods from being scheduled on the node. The lock also indicates that only one node should be rebooted at a time. With the node cordoned off, running pods are drained from the node, and the node is rebooted.

You can monitor the status of the nodes using the [kubectl get nodes](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. The following example output shows a node with a status of *SchedulingDisabled* as the node prepares for the reboot process:

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-28993262-0 Ready,SchedulingDisabled agent 1h v1.11.7
```


Once the update process is complete, you can view the status of the nodes using the [kubectl get nodes](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command with the `--output wide`

parameter. This output lets you see a difference in *KERNEL-VERSION* of the underlying nodes, as shown in the following example output. The *aks-nodepool1-28993262-0* was updated in a previous step and shows kernel version *4.15.0-1039-azure*. The node *aks-nodepool1-28993262-1* that hasn't been updated shows kernel version *4.15.0-1037-azure*.

```
NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME
aks-nodepool1-28993262-0 Ready agent 1h v1.11.7 10.240.0.4 <none> Ubuntu 16.04.6 LTS 4.15.0-1039-azure docker://3.0.4
aks-nodepool1-28993262-1 Ready agent 1h v1.11.7 10.240.0.5 <none> Ubuntu 16.04.6 LTS 4.15.0-1037-azure docker://3.0.4
```


## Next steps

This article detailed how to use `kured`

to reboot Linux nodes automatically as part of the security update process. To upgrade to the latest version of Kubernetes, you can [upgrade your AKS cluster](upgrade-cluster).

For AKS clusters that use Windows Server nodes, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).
