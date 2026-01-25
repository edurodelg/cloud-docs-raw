---
merged_at: 2026-01-25T12:06:27.886806
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: faq.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/faq -->

# AKS frequently asked questions

This article provides answers to some of the most common questions about Azure Kubernetes Service (AKS).

## Support

### Does AKS offer a service-level agreement?

AKS provides service-level agreement (SLA) guarantees in the [Standard pricing tier with the Uptime SLA feature](free-standard-pricing-tiers).

### What is platform support, and what does it include?

Platform support is a reduced support plan for unsupported n-3 version clusters. Platform support includes only Azure infrastructure support.

For more information, see the [platform support policy](supported-kubernetes-versions).

### Does AKS automatically upgrade my unsupported clusters?

Yes, AKS initiates auto-upgrades for unsupported clusters. When a cluster in an n-3 version (where *n* is the latest supported AKS minor version that's generally available) is about to drop to n-4, AKS automatically upgrades the cluster to n-2 to remain in an AKS support policy.

For more information, see [Supported Kubernetes versions](supported-kubernetes-versions), [Planned maintenance windows](planned-maintenance), and [Automatic upgrades](auto-upgrade-cluster).

### Can I apply Azure reservation discounts to my AKS agent nodes?

AKS agent nodes are billed as standard Azure virtual machines (VMs). If you purchased [Azure reservations](/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations) for the VM size that you're using in AKS, those discounts are automatically applied.

## Operations

### Can I run Windows Server containers on AKS?

Yes, AKS supports Windows Server containers. For more information, see the [Windows Server on AKS FAQ](windows-faq).

### What Linux operating systems (OS) are supported on AKS?

AKS supports four main Linux operating systems, including Ubuntu Linux, [Azure Linux](use-azure-linux), [Azure Linux OS Guard](use-azure-linux-os-guard), and [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks). When specifying `--os-type Linux`

during node pool creation or cluster creation, the default OS is Ubuntu Linux.

### What operating systems (OS) versions are supported on AKS?

When using `--os-sku Ubuntu`

, AKS defaults to Ubuntu 22.04 in Kubernetes versions 1.25-1.34. AKS defaults to Ubuntu 24.04 in Kubernetes versions 1.35+.
When using `--os-sku AzureLinux`

, AKS defaults to Azure Linux 3.0 in Kubernetes versions 1.32+.
In some scenarios, like FIPS-enabled node pools, the default OS version might differ. See [node images](node-images) for more information.

### Can I move or migrate my cluster between Azure tenants?

No. Moving your AKS cluster between tenants is currently unsupported.

### Can I move or migrate my cluster between subscriptions?

No. Moving your AKS cluster between subscriptions is currently unsupported.

### Can I move my AKS cluster or AKS infrastructure resources to other resource groups or rename them?

No. Moving or renaming your AKS cluster and its associated resources isn't supported.

### Can I restore my cluster after I delete it?

No. You can't restore your cluster after you delete it. When you delete your cluster, the node resource group and all its resources are also deleted.

If you want to keep any of your resources, move them to another resource group before you delete your cluster. If you want to protect against accidental deletes, you can lock the AKS managed resource group that's hosting your cluster resources by using [Node resource group lockdown](node-resource-group-lockdown).

### Can I scale my AKS cluster to zero?

You can completely [stop a running AKS cluster](start-stop-cluster) or [scale or autoscale all or specific User node pools](scale-cluster#scale-user-node-pools-to-0) to zero.

You can't directly scale [system node pools](use-system-pools) to zero.

### Can I use the virtual machine scale set APIs to scale manually?

No. Scale operations that use the virtual machine scale set APIs aren't supported. You can use the AKS APIs (`az aks scale`

).

### Can I use virtual machine scale sets to manually scale to zero nodes?

No. Scale operations that use the virtual machine scale set APIs aren't supported. You can use the AKS API to scale nonsystem node pools to zero or [stop your cluster](start-stop-cluster) instead.

### Can I stop or deallocate all my VMs?

No. This configuration isn't supported. [Stop your cluster](start-stop-cluster) instead.

### Why are two resource groups created with AKS?

AKS builds upon many Azure infrastructure resources, including virtual machine scale sets, virtual networks, and managed disks. These integrations enable you to apply many of the core capabilities of the Azure platform within the managed Kubernetes environment provided by AKS. For example, you can use most Azure VM types directly with AKS, and you can use Azure Reservations to receive discounts on those resources automatically.

To enable this architecture, each AKS deployment spans two resource groups:

- You create the first resource group. This group contains only the Kubernetes service resource. The AKS resource provider automatically creates the second resource group during deployment. An example of the second resource group is
*MC_myResourceGroup_myAKSCluster_eastus*. For information on how to specify the name of this second resource group, see the next section. - The second resource group, known as the
*node resource group*, contains all of the infrastructure resources associated with the cluster. These resources include the Kubernetes node VMs, virtual networking, and storage. By default, the node resource group has a name like*MC_myResourceGroup_myAKSCluster_eastus*. AKS automatically deletes the node resource group whenever you delete the cluster. Use this resource group only for resources that share the cluster's lifecycle.

Note

Modifying any resource under the node resource group in the AKS cluster is an unsupported action and will cause cluster operation failures. You can prevent changes from being made to the node resource group. [Block users from modifying resources](node-resource-group-lockdown) that the AKS cluster manages.

### Can I provide my own name for the AKS node resource group?

By default, AKS names the node resource group *MC_resourcegroupname_clustername_location*, but you can provide your own name.

To specify your own resource group name, install the [aks-preview](/en-us/cli/azure/aks) Azure CLI extension version *0.3.2* or later. When you create an AKS cluster by using the `az aks create`

command, use the `--node-resource-group`

parameter and specify a name for the resource group. If you use an [Azure Resource Manager template](/en-us/azure/templates/microsoft.containerservice/2022-09-01/managedclusters) to deploy an AKS cluster, you can define the resource group name by using the `nodeResourceGroup`

property.

- The Azure resource provider automatically creates the secondary resource group.
- You can specify a custom resource group name only when you create the cluster.

As you work with the node resource group, you can't:

- Specify an existing resource group for the node resource group.
- Specify a different subscription for the node resource group.
- Change the node resource group name after you create the cluster.
- Specify names for the managed resources within the node resource group.
- Modify or delete Azure-created tags of managed resources within the node resource group.

### Can I modify tags and other properties of the AKS resources in the node resource group?

You might get unexpected scaling and upgrading errors if you modify or delete Azure-created tags and other resource properties in the node resource group. AKS allows you to create and modify custom tags created by end users, and you can add those tags when you [create a node pool](manage-node-pools#specify-a-taint-label-or-tag-for-a-node-pool). You might want to create or modify custom tags, for example, to assign a business unit or cost center. Another option is to apply policies and modify tags through the AKS resource itself—specifically via the cluster and node pools..

Azure-created tags are created for their respective Azure services, and you should always allow them. For AKS, there are the `aks-managed`

and `k8s-azure`

tags. Modifying any *Azure-created tags* on resources under the node resource group in the AKS cluster is an unsupported action, which breaks the service-level objective (SLO).

Note

In the past, the tag name `Owner`

was reserved for AKS to manage the public IP that's assigned on the front-end IP of the load balancer. Now, services use the `aks-managed`

prefix. For legacy resources, don't use Azure policies to apply the `Owner`

tag name. Otherwise, all resources on your AKS cluster deployment and update operations will break. This restriction doesn't apply to newly created resources.

### Why do I see aks-managed prefixed Helm releases on my cluster, and why does their revision count keep increasing?

AKS uses Helm to deliver components to your cluster. You can safely ignore `aks-managed`

prefixed Helm releases. Continuously increasing revisions on these Helm releases are expected and safe.

## Quotas, limits, and region availability

### Which Azure regions currently provide AKS?

For a complete list of available regions, see [AKS regions and availability](https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service).

### Can I spread an AKS cluster across regions?

No. AKS clusters are regional resources and can't span regions. For guidance on how to create an architecture that includes multiple regions, see [best practices for business continuity and disaster recovery](operator-best-practices-multi-region#plan-for-multiregion-deployment).

### Can I spread an AKS cluster across availability zones?

Yes, you can deploy an AKS cluster across one or more [availability zones](availability-zones) in [regions that support them](/en-us/azure/reliability/availability-zones-region-support).

### Can I have different VM sizes in a single cluster?

Yes, you can use different VM sizes in your AKS cluster by creating [multiple node pools](create-node-pools).

### What's the size limit on a container image in AKS?

AKS doesn't set a limit on the container image size. But the larger the image, the higher the memory demand. A larger size could potentially exceed resource limits or the overall available memory of worker nodes. By default, memory for VM size Standard_DS2_v2 for an AKS cluster is set to 7 GiB.

When a container image is excessively large, as in the terabyte (TB) range, the kubelet might not be able to pull it from your container registry to a node because of the lack of disk space.

For Windows Server nodes, Windows Update doesn't automatically run and apply the latest updates. You should perform an upgrade on the cluster and the Windows Server node pools in your AKS cluster. Follow a regular schedule based on the Windows Update release cycle and your own validation process. This upgrade process creates nodes that run the latest Windows Server image and patches, and then removes the older nodes. For more information on this process, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

### Are AKS images required to run as root?

The following images have functional requirements to run as root, and exceptions must be filed for any policies:

*mcr.microsoft.com/oss/kubernetes/coredns**mcr.microsoft.com/azuremonitor/containerinsights/ciprod**mcr.microsoft.com/oss/calico/node**mcr.microsoft.com/oss/kubernetes-csi/azuredisk-csi*

## Security, access, and identity

### Can I limit who has access to the Kubernetes API server?

Yes, there are two options for limiting access to the API server:

- Use
[API server authorized IP ranges](api-server-authorized-ip-ranges)if you want to maintain a public endpoint for the API server but restrict access to a set of trusted IP ranges. - Use a
[private cluster](private-clusters)if you want to limit the API server to be accessible*only*from within your virtual network.

### Are security updates applied to AKS agent nodes?

AKS patches CVEs that have a *vendor fix* every week. CVEs without a fix are waiting on a vendor fix before they can be remediated. The AKS images are automatically updated within 30 days. We recommend that you apply an updated node image on a regular cadence to ensure that the latest patched images and OS patches are all applied and current. You can do this task:

- Manually, through the Azure portal or the Azure CLI.
- By upgrading your AKS cluster. The cluster upgrades
[cordon and drain nodes](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)automatically. Then it brings a new node online with the latest Ubuntu image and a new patch version or a minor Kubernetes version. For more information, see[Upgrade an AKS cluster](upgrade-cluster). - By using a
[node image upgrade](node-image-upgrade).

### Are there security threats that target AKS that I should be aware of?

Microsoft provides guidance for other actions that you can take to secure your workloads through services like [Microsoft Defender for Containers](/en-us/azure/defender-for-cloud/defender-for-containers-introduction?tabs=defender-for-container-arch-aks). For information on a security threat related to AKS and Kubernetes, see [New large-scale campaign targets Kubeflow](https://techcommunity.microsoft.com/t5/azure-security-center/new-large-scale-campaign-targets-kubeflow/ba-p/2425750) (June 8, 2021).

### Does AKS store any customer data outside the cluster's region?

No. All data is stored in the cluster's region.

### How can I avoid permission ownership setting slow issues when the volume has numerous files?

Traditionally, if your pod is running as a nonroot user (which it should), you must specify an `fsGroup`

parameter inside the pod's security context so that the volume is readable and writable by the pod. For more information on this requirement, see [Configure a security context for a pod or container](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/).

A side effect of setting `fsGroup`

is that each time a volume is mounted, Kubernetes must use the `chown()`

and `chmod()`

commands recursively for all the files and directories inside the volume (with a few exceptions). This scenario happens even if group ownership of the volume already matches the requested `fsGroup`

parameter. This configuration might be expensive for larger volumes with lots of small files, which can cause pod startup to take a long time. This scenario was a known problem before v1.20. The workaround is to set the pod to run as root:

```
apiVersion: v1
kind: Pod
metadata:
name: security-context-demo
spec:
securityContext:
runAsUser: 0
fsGroup: 0
```


The issue was resolved with Kubernetes version 1.20. For more information, see [Kubernetes 1.20: Granular control of volume permission changes](https://kubernetes.io/blog/2020/12/14/kubernetes-release-1.20-fsgroupchangepolicy-fsgrouppolicy/).

## Networking

### How does the managed control plane communicate with my nodes?

AKS uses a secure tunnel communication to allow the `api-server`

and individual node kubelets to communicate, even on separate virtual networks. The tunnel is secured through mutual Transport Layer Security encryption. The current main tunnel that AKS uses is [Konnectivity, previously known as apiserver-network-proxy](https://kubernetes.io/docs/tasks/extend-kubernetes/setup-konnectivity/). Verify that all network rules follow the [Azure required network rules and fully qualified domain names (FQDNs)](limit-egress-traffic).

### Can my pods use the API server FQDN instead of the cluster IP?

Yes, you can add the annotation `kubernetes.azure.com/set-kube-service-host-fqdn`

to pods to set the `KUBERNETES_SERVICE_HOST`

variable to the domain name of the API server instead of the in-cluster service IP. This modification is useful in cases where your cluster egress is done via a layer 7 firewall. An example is when you use Azure Firewall with application rules.

### Can I configure NSGs with AKS?

AKS doesn't apply network security groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. AKS modifies only the network interface NSG settings. If you're using Container Network Interface (CNI), you also must ensure that the security rules in the NSGs allow traffic between the node and pod classless interdomain routing (CIDR) ranges. If you're using kubenet, you must also ensure that the security rules in the NSGs allow traffic between the node and pod CIDR. For more information, see [Network security groups](concepts-network#network-security-groups).

### How does time synchronization work in AKS?

AKS nodes run the chrony service, which pulls time from the local host. Containers that run on pods get the time from the AKS nodes. Applications that open inside a container use time from the container of the pod.

## Add-ons, extensions, and integrations

### Can I use custom VM extensions?

No. AKS is a managed service. Manipulation of the infrastructure as a service (IaaS) resources isn't supported. To install custom components, use the Kubernetes APIs and mechanisms. For example, use DaemonSets to install any required components.

### What Kubernetes admission controllers does AKS support? Can admission controllers be added or removed?

AKS supports the following [admission controllers](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/):

`NamespaceLifecycle`

`LimitRanger`

`ServiceAccount`

`DefaultIngressClass`

`DefaultStorageClass`

`DefaultTolerationSeconds`

`MutatingAdmissionWebhook`

`ValidatingAdmissionWebhook`

`ResourceQuota`

`PodNodeSelector`

`PodTolerationRestriction`

`ExtendedResourceToleration`


Currently, you can't modify the list of admission controllers in AKS.

### Can I use admission controller webhooks on AKS?

Yes, you can use admission controller webhooks on AKS. We recommend that you exclude internal AKS namespaces, which are marked with the `control-plane`

label. For example:

```
namespaceSelector:
matchExpressions:
- key: control-plane
operator: DoesNotExist
```


AKS firewalls the API server egress so that your admission controller webhooks need to be accessible from within the cluster.

### Can admission controller webhooks affect kube-system and internal AKS namespaces?

To protect the stability of the system and prevent custom admission controllers from affecting internal services in the `kube-system`

namespace, AKS has an admissions enforcer, which automatically excludes `kube-system`

and AKS internal namespaces. This service ensures that the custom admission controllers don't affect the services that run in `kube-system`

.

If you have a critical use case for deploying something on `kube-system`

(not recommended) in support of your custom admission webhook, you can add the following label or annotation so that the admissions enforcer ignores it:

- Label:
`"admissions.enforcer/disabled": "true"`

- Annotation:
`"admissions.enforcer/disabled": true`


### Is Azure Key Vault integrated with AKS?

[Azure Key Vault provider for Secrets Store CSI Driver](csi-secrets-store-driver) provides native integration of Azure Key Vault into AKS.

### Can I use FIPS cryptographic libraries with deployments on AKS?

Nodes that are enabled with Federal Information Processing Standards (FIPS) are now supported on Linux-based node pools. For more information, see [Add a FIPS-enabled node pool](enable-fips-nodes).

### How are AKS add-ons updated?

Any patch, including a security patch, is automatically applied to the AKS cluster. Anything bigger than a patch, like major or minor version changes (which can have breaking changes to your deployed objects), are updated when you update your cluster if a new release is available. For information on when a new release is available, see [AKS release notes](https://github.com/Azure/AKS/releases).

### What is the purpose of the AKS Linux extension that I see installed on my Linux virtual machine scale sets instances?

The AKS Linux extension is an Azure VM extension that installs and configures monitoring tools on Kubernetes worker nodes. The extension is installed on all new and existing Linux nodes. It configures the following monitoring tools:

[Node-exporter](https://github.com/prometheus/node_exporter): Collects hardware telemetry from the VM and makes it available by using a metrics endpoint. Then, a monitoring tool, such as Prometheus, can scrap these metrics.[Node-problem-detector](https://github.com/kubernetes/node-problem-detector): Aims to make various node problems visible to upstream layers in the cluster management stack. It's a systemd unit that runs on each node, detects node problems, and reports them to the cluster's API server by using`Events`

and`NodeConditions`

.[ig](https://go.microsoft.com/fwlink/p/?linkid=2260320): Is an eBPF-powered open-source framework for debugging and observing Linux and Kubernetes systems. It provides a set of tools (or gadgets) that gather relevant information that users can use to identify the cause of performance issues, crashes, or other anomalies. Notably, its independence from Kubernetes enables users to employ it also for debugging control plane issues.

These tools help provide observability around many node health-related problems, such as:

**Infrastructure daemon issues:**NTP service down**Hardware issues:**Bad CPU, memory, or disk**Kernel issues:**Kernel deadlock, corrupted file system**Container runtime issues:**Unresponsive runtime daemon

The extension *doesn't require extra outbound access* to any URLs, IP addresses, or ports beyond the [documented AKS egress requirements](limit-egress-traffic). It doesn't require any special permissions granted in Azure. It uses `kubeconfig`

to connect to the API server to send the monitoring data that's collected.

## Troubleshoot cluster issues

### Why is it taking so long to delete my cluster?

Most clusters are deleted upon user request. In some cases, especially cases where you bring your own resource group or perform cross-resource group tasks, deletion can take more time or even fail. If you have an issue with deletions, double-check that you don't have locks on the resource group. Also make sure that any resources outside the resource group are disassociated from the resource group.

### Why is it taking so long to create or update my cluster?

If you have issues with creating and updating clusters, make sure that you don't have any assigned policies or service constraints that might block your AKS cluster from managing resources like VMs, load balancers, or tags.

### If I have pods or deployments in NodeLost or Unknown states, can I still upgrade my cluster?

You can, but we don't recommend it. Perform updates when the state of the cluster is known and healthy.

### If I have a cluster with one or more nodes in an Unhealthy state, or if it's shut down, can I perform an upgrade?

No. Delete or remove any nodes that are in a failed state or otherwise from the cluster before you upgrade.

### I tried to delete my cluster, but I see the error "[Errno 11001] getaddrinfo failed."

Most commonly, this error arises if you have one or more NSGs in use that are still associated with the cluster. Remove them and attempt to delete the cluster again.

### I ran an upgrade, but now my pods are in crash loops and readiness probes fail.

Confirm that your service principal isn't expired. For more information, see [AKS service principal](kubernetes-service-principal) and [AKS update credentials](update-credentials).

### My cluster was working, but suddenly I can't provision load balancers or mount persistent volume claims.

Confirm that your service principal isn't expired. For more information, see [AKS service principal](kubernetes-service-principal) and [AKS update credentials](update-credentials).

## Retirements and deprecations

### Which Linux OS versions are deprecated on AKS?

Ubuntu 16.04 and Ubuntu 18.04 are no longer supported on AKS.
Starting on 17 March 2027, AKS will no longer support Ubuntu 20.04. For more information on this retirement, see [Retirement: Ubuntu 20.04 node pools on AKS](https://github.com/Azure/AKS/issues/4874).

### Which Windows OS versions are deprecated on AKS?

Starting on 1 March 2026, AKS will no longer support Windows Server 2019 node pools. Kubernetes versions 1.33+ can't use Windows Server 2019. For more information on this retirement, see [Retirement: Windows Server 2019 node pools on AKS](https://github.com/Azure/AKS/issues/4091).
Starting on 15 March 2027, AKS will no longer support Windows Server 2022 node pools. Kubernetes versions 1.36+ can't use Windows Server 2022. For more information on this retirement, see [Retirement: Windows Server 2022 node pools on AKS](https://github.com/Azure/AKS/issues/4168).


---

<!-- DOCUMENTO FUSIONADO: manage-ssh-node-access.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/manage-ssh-node-access -->

# Manage SSH for secure access to Azure Kubernetes Service (AKS) nodes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to configure SSH access (preview) on your AKS clusters or node pools, during initial deployment or at a later time.

AKS supports the following configuration options to manage SSH access on cluster nodes:

**Disabled SSH**: Completely disable SSH access to cluster nodes for enhanced security**Entra ID based SSH**: Use Microsoft Entra ID credentials for SSH authentication. Benefits of using Entra ID based SSH:**Centralized identity management**: Use your existing Entra ID identities to access cluster nodes**No SSH key management**: Eliminates the need to generate, distribute, and rotate SSH keys**Enhanced security**: Leverage Entra ID security features like Conditional Access and MFA**Audit and compliance**: Centralized logging of access events through Entra ID logs**Just-in-time access**: Combine with Azure RBAC for granular access control

**Local User SSH**: Traditional SSH key-based authentication for node access

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


This article requires version 2.61.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.

You need

`aks-preview`

version 9.0.0b1 or later.- If you don't already have the
`aks-preview`

extension, install it using thecommand:`az extension add`

`az extension add --name aks-preview`

- If you already have the
`aks-preview`

extension, update it to make sure you have the latest version using thecommand:`az extension update`

`az extension update --name aks-preview`


- If you don't already have the
Register the

`DisableSSHPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "DisableSSHPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "DisableSSHPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


This article requires version 2.73.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.

You need

`aks-preview`

version 19.0.0b7 or later for Entra ID SSH.- If you don't already have the
`aks-preview`

extension, install it using thecommand:`az extension add`

`az extension add --name aks-preview`

- If you already have the
`aks-preview`

extension, update it to make sure you have the latest version using thecommand:`az extension update`

`az extension update --name aks-preview`


- If you don't already have the
Appropriate Azure RBAC permissions to access nodes:

**Required action**:`Microsoft.Compute/virtualMachineScaleSets/*/read`

- to read Virtual Machine Scale Sets information**Required data action**:`Microsoft.Compute/virtualMachineScaleSets/virtualMachines/login/action`

- to authenticate and log in to VMs as regular user.`Microsoft.Compute/virtualMachines/loginAsAdmin/action`

- to login with root user privileges.

**Built-in role**:or**Virtual Machine Administrator Login**(for non-admin access)**Virtual Machine User Login**


Register the

`EntraIdSSHPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "EntraIdSSHPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "EntraIdSSHPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- This article requires version 2.61.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.
- You need
`aks-preview`

version 9.0.0b1 or later to update SSH access method on nodepools.- If you don't already have the
`aks-preview`

extension, install it using thecommand:`az extension add`

`az extension add --name aks-preview`

- If you already have the
`aks-preview`

extension, update it to make sure you have the latest version using thecommand:`az extension update`

`az extension update --name aks-preview`


- If you don't already have the

### Set environment variables

Set the following environment variables for your resource group, cluster name, and location:

```
export RESOURCE_GROUP="<your-resource-group-name>"
export CLUSTER_NAME="<your-cluster-name>"
export LOCATION="<your-azure-region>"
```


## Limitations

- Entra ID SSH to nodes is not yet available for Windows node pool.
- Entra ID SSH to nodes is not supported for AKS automatic because of
[node resource group lockdown](node-resource-group-lockdown)preventing role assignments.

## Configure SSH access

To improve security and support your corporate security requirements or strategy, AKS supports disabling SSH both on the cluster and at the node pool level. Disable SSH introduces a simplified approach compared to configuring [network security group rules](concepts-security#azure-network-security-groups) on the AKS subnet/node network interface card (NIC). Disable SSH only supports Virtual Machine Scale Sets node pools.

When you disable SSH at cluster creation time, it takes effect after the cluster is created. However, when you disable SSH on an existing cluster or node pool, AKS doesn't automatically disable SSH. At any time, you can choose to perform a nodepool upgrade operation. The disable/enable SSH operation takes effect after the node image update is complete.

Note

When you disable SSH at the cluster level, it applies to all existing node pools. Any node pools created after this operation will have SSH enabled by default, and you'll need to run these commands again in order to disable it.

Note

[kubectl debug node](node-access) continues to work after you disable SSH because it doesn't depend on the SSH service.

### Create a resource group

Create a resource group using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create --name $RESOURCE_GROUP --location $LOCATION
```


### Disable SSH on a new cluster deployment

By default, the SSH service on AKS cluster nodes is open to all users and pods running on the cluster. You can prevent direct SSH access from any network to cluster nodes to help limit the attack vector if a container in a pod becomes compromised.

Use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command to create a new cluster, and include the

`--ssh-access disabled`

argument to disable SSH (preview) on all the node pools during cluster creation.Important

After you disable the SSH service, you can't SSH into the cluster to perform administrative tasks or to troubleshoot.

Note

On a newly created cluster, disable SSH will only configure the first system node pool. All other node pools need to be configured at the node pool level.

```
az aks create --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --ssh-access disabled
```


After a few minutes, the command completes and returns JSON-formatted information about the cluster. The following example resembles the output and the results related to disabling SSH:

```
"securityProfile": {
"sshAccess": "Disabled"
},
```


### Disable SSH for a new node pool

Use the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command to add a node pool, and include the

`--ssh-access disabled`

argument to disable SSH during node pool creation.```
az aks nodepool add \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--ssh-access disabled
```


After a few minutes, the command completes and returns JSON-formatted information about the cluster indicating *mynodepool* was successfully created. The following example resembles the output and the results related to disabling SSH:

```
"securityProfile": {
"sshAccess": "Disabled"
},
```


### Disable SSH for an existing node pool

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command with the

`--ssh-access disabled`

argument to disable SSH (preview) on an existing node pool.```
az aks nodepool update \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--ssh-access disabled
```


After a few minutes, the command completes and returns JSON-formatted information about the cluster indicating *mynodepool* was successfully updated. The following example resembles the output and the results related to disabling SSH:

```
"securityProfile": {
"sshAccess": "Disabled"
},
```


For the change to take effect, you need to reimage the node pool by using the [ az aks nodepool upgrade](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade) command.

```
az aks nodepool upgrade \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--node-image-only
```


Important

To disable SSH on an existing cluster, you need to disable SSH for each node pool on this cluster.

### Re-enable SSH access

To re-enable SSH access on a node pool, update the node pool with either `--ssh-access localuser`

(for traditional SSH key-based access) or `--ssh-access entraid`

(for Entra ID based access). See the respective sections for detailed instructions.

You can configure your AKS cluster to use Microsoft Entra ID (formerly Azure AD) for SSH authentication to cluster nodes. This eliminates the need to manage SSH keys and allows you to use your Entra ID credentials to access nodes securely.

### Create a resource group

Create a resource group using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create --name $RESOURCE_GROUP --location $LOCATION
```


### Enable Entra ID based SSH on a new cluster

Use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command with the

`--ssh-access entraid`

argument to enable Entra ID based SSH authentication during cluster creation.```
az aks create \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--ssh-access entraid
```


After a few minutes, the command completes and returns JSON-formatted information about the cluster. The following example resembles the output:

```
"securityProfile": {
"sshAccess": "EntraID"
},
```


### Enable Entra ID based SSH for a new node pool

Use the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command with the

`--ssh-access entraid`

argument to enable Entra ID based SSH during node pool creation.```
az aks nodepool add \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--ssh-access entraid
```


After a few minutes, the command completes and returns JSON-formatted information indicating *mynodepool* was successfully created with Entra ID based SSH. The following example resembles the output:

```
"securityProfile": {
"sshAccess": "EntraID"
},
```


### Enable Entra ID based SSH for an existing node pool

Use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command with the

`--ssh-access entraid`

argument to enable Entra ID based SSH on an existing node pool.```
az aks nodepool update \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--ssh-access entraid
```


After a few minutes, the command completes and returns JSON-formatted information indicating *mynodepool* was successfully updated with Entra ID based SSH. The following example resembles the output:

```
"securityProfile": {
"sshAccess": "EntraID"
},
```


For the change to take effect, you need to reimage the node pool by using the [ az aks nodepool upgrade](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade) command.

```
az aks nodepool upgrade \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--node-image-only
```


Important

To enable Entra ID based SSH on an existing cluster, you need to enable it for each node pool individually.

Local user SSH access uses traditional SSH key-based authentication. This is the default SSH access method for AKS clusters.

### Create a resource group

Create a resource group using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create --name $RESOURCE_GROUP --location $LOCATION
```


### Create an AKS cluster with SSH keys

Use the [az aks create](/en-us/cli/azure/aks#az-aks-create) command to deploy an AKS cluster with an SSH public key. You can either specify the key or a key file using the `--ssh-key-value`

argument, or use `--ssh-access localuser`

to explicitly set local user SSH access.

| SSH parameter | Description | Default value |
|---|---|---|
`--generate-ssh-key` |
If you don't have your own SSH keys, specify `--generate-ssh-key` . The Azure CLI automatically generates a set of SSH keys and saves them in the default directory `~/.ssh/` . |
|
`--ssh-key-value` |
Public key path or key contents to install on node VMs for SSH access. For example, `ssh-rsa AAAAB...snip...UcyupgH azureuser@linuxvm` . |
`~/.ssh/id_rsa.pub` |
`--ssh-access localuser` |
Explicitly enable local user SSH access with key-based authentication. | |
`--no-ssh-key` |
If you don't require SSH keys, specify this argument. However, AKS automatically generates a set of SSH keys because the Azure Virtual Machine resource dependency doesn't support an empty SSH keys file. As a result, the keys aren't returned and can't be used to SSH into the node VMs. The private key is discarded and not saved. |

Note

If no parameters are specified, the Azure CLI defaults to referencing the SSH keys stored in the `~/.ssh/id_rsa.pub`

file. If the keys aren't found, the command returns the message `An RSA key file or key value must be supplied to SSH Key Value`

.

**Examples:**

To create a cluster and use the default generated SSH keys:

`az aks create --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --generate-ssh-key`

To specify an SSH public key file:

`az aks create --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --ssh-key-value ~/.ssh/id_rsa.pub`

To explicitly enable local user SSH access:

`az aks create --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --ssh-access localuser --generate-ssh-key`


### Enable local user SSH for a new node pool

Use the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command with the

`--ssh-access localuser`

argument to enable local user SSH during node pool creation.```
az aks nodepool add \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--ssh-access localuser
```


### Enable local user SSH for an existing node pool

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command with the

`--ssh-access localuser`

argument to enable local user SSH on an existing node pool.```
az aks nodepool update \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--ssh-access localuser
```


Important

For the change to take effect, you need to reimage the node pool by using the [ az aks nodepool upgrade](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade) command.

```
az aks nodepool upgrade \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--node-image-only
```


### Update SSH public key on an existing AKS cluster

Use the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command to update the SSH public key (preview) on your cluster. This operation updates the key on all node pools. You can either specify a key or a key file using the

`--ssh-key-value`

argument.Note

Updating the SSH keys is supported on Azure virtual machine scale sets with AKS clusters.

**Examples:**

To specify a new SSH public key value:

`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --ssh-key-value 'ssh-rsa AAAAB3Nza-xxx'`

To specify an SSH public key file:

`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --ssh-key-value ~/.ssh/id_rsa.pub`


Important

After you update the SSH key, AKS doesn't automatically update your node pool. At any time, you can choose to perform a [nodepool upgrade operation](node-image-upgrade). The update SSH keys operation takes effect after a node image update is complete. For clusters with [Node Auto-provisioning](node-autoprovision) enabled, a node image update can be performed by applying a new label to the Kubernetes NodePool custom resource.

## Verify SSH service status

After disabling SSH, you can verify that the SSH service is inactive on your cluster nodes.

Use the Virtual Machine Scale Set [ az vmss run-command invoke](/en-us/cli/azure/vmss/run-command#az-vmss-run-command-invoke) command to check SSH service status.

```
az vmss run-command invoke --resource-group <node-resource-group> --name <vmss-name> --command-id RunShellScript --instance-id 0 --scripts "systemctl status ssh"
```


The following sample output shows the expected result when SSH is disabled:

```
{
"value": [
{
"code": "ProvisioningState/succeeded",
"displayStatus": "Provisioning succeeded",
"level": "Info",
"message": "Enable succeeded: \n[stdout]\n○ ssh.service - OpenBSD Secure Shell server\n Loaded: loaded (/lib/systemd/system/ssh.service; disabled; vendor preset: enabled)\n Active: inactive (dead) since Wed 2024-01-03 15:36:53 UTC; 25min ago\n..."
}
]
}
```


Search for the word **Active** and verify that its value is `Active: inactive (dead)`

, which confirms SSH is disabled on the node.

After enabling Entra ID based SSH, you can verify that the SSH service is active and configured for Entra ID authentication on your cluster nodes.

Use the Virtual Machine Scale Set [ az vmss run-command invoke](/en-us/cli/azure/vmss/run-command#az-vmss-run-command-invoke) command to check SSH service status.

```
az vmss run-command invoke --resource-group <node-resource-group> --name <vmss-name> --command-id RunShellScript --instance-id 0 --scripts "systemctl status ssh"
```


The following sample output shows the expected result when SSH is enabled:

```
{
"value": [
{
"code": "ProvisioningState/succeeded",
"displayStatus": "Provisioning succeeded",
"level": "Info",
"message": "Enable succeeded: \n[stdout]\n● ssh.service - OpenBSD Secure Shell server\n Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)\n Active: active (running) since Wed 2024-01-03 15:40:20 UTC; 19min ago\n..."
}
]
}
```


Search for the word **Active** and verify that its value is `Active: active (running)`

, which confirms SSH is enabled on the node.

After configuring local user SSH, you can verify that the SSH service is active on your cluster nodes.

Use the Virtual Machine Scale Set [ az vmss run-command invoke](/en-us/cli/azure/vmss/run-command#az-vmss-run-command-invoke) command to check SSH service status.

```
az vmss run-command invoke --resource-group <node-resource-group> --name <vmss-name> --command-id RunShellScript --instance-id 0 --scripts "systemctl status ssh"
```


The following sample output shows the expected result when SSH is enabled:

```
{
"value": [
{
"code": "ProvisioningState/succeeded",
"displayStatus": "Provisioning succeeded",
"level": "Info",
"message": "Enable succeeded: \n[stdout]\n● ssh.service - OpenBSD Secure Shell server\n Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)\n Active: active (running) since Wed 2024-01-03 15:40:20 UTC; 19min ago\n..."
}
]
}
```


Search for the word **Active** and verify that its value is `Active: active (running)`

, which confirms SSH is enabled on the node.

## Next steps

To help troubleshoot any issues with SSH connectivity to your clusters nodes, you can [view the kubelet logs](kubelet-logs) or [view the Kubernetes master node logs](monitor-aks-reference#resource-logs).
