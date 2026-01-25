---
merged_at: 2026-01-25T12:06:27.876708
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: support-policies.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/support-policies -->

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

Base infrastructure as a service (IaaS) cloud components, such as compute or networking components, allow you access to low-level controls and customization options. By contrast, AKS provides a turnkey Kubernetes deployment that gives you a common set of configurations and capabilities you need for your cluster. As an AKS user, you have limited customization and deployment options. In exchange, you don't need to worry about or manage Kubernetes clusters directly.

With AKS, you get a fully managed *control plane*. The control plane contains all of the components and services you need to operate and deliver Kubernetes clusters to end users. Microsoft maintains and operates all Kubernetes components.

Microsoft manages and monitors the following components through the control plane:

- Kubelet or Kubernetes API servers
- Etcd or a compatible key-value store, providing Quality of Service (QoS), scalability, and runtime
- DNS services (for example, kube-dns or CoreDNS)
- Kubernetes proxy or networking, except when
[BYOCNI](use-byo-cni)is used - Any other
[add-ons](integrations#add-ons)or system component running in the kube-system namespace.

AKS isn't a Platform-as-a-Service (PaaS) solution. Some components, such as agent nodes, have *shared responsibility*, where you must help maintain the AKS cluster. User input is required, for example, to apply an agent node operating system (OS) security patch.

The services are *managed* in the sense that Microsoft and the AKS team deploys, operates, and is responsible for service availability and functionality. Customers can't alter these managed components. Microsoft limits customization to ensure a consistent and scalable user experience.

## Shared responsibility

When a cluster is created, you define the Kubernetes agent nodes that AKS creates. Your workloads are executed on these nodes.

Because your agent nodes execute private code and store sensitive data, Microsoft Support can access them only in a limited way. Microsoft Support can't sign in to, execute commands in, or view logs for these nodes without your express permission or assistance.

Any modification made directly to the agent nodes using any one of the IaaS APIs renders the cluster unsupportable. Any modification applied to the agent nodes must be done using kubernetes-native mechanisms such as `Daemon Sets`

.

Similarly, while you might add any metadata to the cluster and nodes, such as tags and labels, changing any of the system created metadata renders the cluster unsupported.

## AKS support coverage

### Supported scenarios

Microsoft provides technical support for the following examples:

- Connectivity to all Kubernetes components that the Kubernetes service provides and supports, such as the API server.
- Management, uptime, QoS, and operations of Kubernetes control plane services (For example, Kubernetes control plane, API server, etcd, and coreDNS).
- Etcd data store. Support includes automated, transparent backups of all etcd data every 30 minutes for disaster planning and cluster state restoration. These backups aren't directly available to you or anyone else. They ensure data reliability and consistency. On-demand rollback or restore isn't supported as a feature.
- Any integration points in the Azure cloud provider driver for Kubernetes. These include integrations into other Azure services such as load balancers, persistent volumes, or networking (Kubernetes and Azure CNI, except when
[BYOCNI](use-byo-cni)is in use). - Questions or issues about customization of control plane components such as the Kubernetes API server, etcd, and coreDNS.
- Issues about networking, such as Azure CNI, kubenet, or other network access and functionality issues, except when
[BYOCNI](use-byo-cni)is in use. Issues could include DNS resolution, packet loss, routing, and so on. Microsoft supports various networking scenarios:- Kubenet and Azure CNI using managed VNETs or with custom (bring your own) subnets.
- Connectivity to other Azure services and applications
- Microsoft-managed ingress controllers or load balancer configurations
- Network performance and latency
- Microsoft-managed
[network policies](use-network-policies#differences-between-network-policy-engines-cilium-azure-npm-and-calico)components and functionalities


Note

Any cluster actions taken by Microsoft/AKS are made with your consent under a built-in Kubernetes role `aks-service`

and built-in role binding `aks-service-rolebinding`

. This role enables AKS to troubleshoot and diagnose cluster issues, but can't modify permissions nor create roles or role bindings, or other high privilege actions. Role access is only enabled under active support tickets with just-in-time (JIT) access.

### Unsupported scenarios

Microsoft doesn't provide technical support for the following scenarios:

Questions about how to use Kubernetes. For example, Microsoft Support doesn't provide advice on how to create custom ingress controllers, use application workloads, or apply third-party or open-source software packages or tools.

Note

Microsoft Support can advise on AKS cluster functionality, customization, and tuning (for example, Kubernetes operations issues and procedures).

Third-party open-source projects that aren't provided as part of the Kubernetes control plane or deployed with AKS clusters. These projects might include Istio, Helm, Envoy, or others.

Note

Microsoft can provide best-effort support for third-party open-source projects such as Helm. Where the third-party open-source tool integrates with the Kubernetes Azure cloud provider or other AKS-specific bugs, Microsoft supports examples and applications from Microsoft documentation.

Third-party closed-source software. This software can include security scanning tools and networking devices or software.

Configuring or troubleshooting application-specific code or behavior of third-party applications or tools running within the AKS cluster. This includes application deployment issues not related to the AKS platform itself.

Issuance, renewal, or management of certificates for applications running on AKS.

Network customizations other than the ones listed in the

[AKS documentation](./). For example, Microsoft Support can't configure devices or virtual appliances meant to provide[outbound traffic](outbound-rules-control-egress)for the AKS cluster, such as VPNs or firewalls.Note

On a best-effort basis, Microsoft Support might advise on the

[configuration needed](outbound-rules-control-egress)for Azure Firewall, but not for other third-party devices.Custom or third-party CNI plugins used in

[BYOCNI](use-byo-cni)mode.Configuring or troubleshooting non-Microsoft-managed network policies. While using network policies is supported, Microsoft Support can't investigate issues stemming from custom network policy configurations.

Configuring or troubleshooting non-Microsoft-managed ingress controllers, such as nginx, kong, traefik, etc. This includes addressing functionality issues that arise after AKS-specific operations, like an ingress controller ceasing to work following a Kubernetes version upgrade. Such issues might stem from incompatibilities between the ingress controller version and the new Kubernetes version. For a fully supported option, consider leveraging a

[Microsoft-managed ingress controller option](concepts-network-ingress#compare-ingress-options).Configuring or troubleshooting DaemonSets (including scripts) used to customize node configurations. Although using DaemonSets is the recommended approach to tune, modify, or install third-party software on cluster agent nodes when

[configuration file parameters](custom-node-configuration)are insufficient, Microsoft Support can't troubleshoot issues arising from the custom scripts used in DaemonSets due to their custom nature.Stand-by and proactive scenarios. Microsoft Support provides reactive support to help solve active issues in a timely and professional manner. However, standby or proactive support to help you eliminate operational risks, increase availability, and optimize performance aren't covered.

[Eligible customers](https://www.microsoft.com/unifiedsupport)can contact their account team to get nominated for[Azure Event Management service](https://devblogs.microsoft.com/premier-developer/proactively-plan-for-your-critical-event-in-azure-with-enhanced-support-and-engineering-services/). It's a paid service delivered by Microsoft support engineers that includes a proactive solution risk assessment and coverage during the event.Vulnerabilities / CVEs with a vendor fix that is less than 30 days old. As long as you're running the updated VHD, you shouldn't be running any container image vulnerabilities / CVEs with a vendor fix that is over 30 days old. It's customer responsibility to update the VHD and provide filtered lists to Microsoft support. Once you updated your VHD, it is customer responsibility to filter the vulnerabilities / CVEs report and provide a list only with vulnerabilities/CVEs with a vendor fix that is over 30 days old. If that will be the case, Microsoft support will make sure to work internally and address components with a vendor fix released more than 30 days ago. Additionally, Microsoft provide vulnerability / CVE-related support only for Microsoft-managed components (i.e., AKS node images, managed container images for applications that get deploy during cluster creation or via the installation of a managed add-on). For more details about vulnerability management for AKS, visit

[this page](concepts-vulnerability-management).Custom code samples or scripts. While Microsoft Support

*can*provide small code samples and reviews of small code samples within a support case to demonstrate how to use features of a Microsoft product, Microsoft Support*can't*provide custom code samples that are specific to your environment or application.

## AKS support coverage for agent nodes

### Microsoft responsibilities for AKS agent nodes

Microsoft and you share responsibility for Kubernetes agent nodes where:

- The base OS image has required additions (such as monitoring and networking agents).
- The agent nodes receive OS patches automatically.
- Issues with the Kubernetes control plane components that run on the agent nodes are automatically remediated. These components include the below:
`Kube-proxy`

- Networking tunnels that provide communication paths to the Kubernetes master components
`Kubelet`

`containerd`


Note

If an agent node isn't operational, AKS might restart individual components or the entire agent node. These restart operations are automated and provide auto-remediation for common issues. If you want to know more about the auto-remediation mechanisms, see [Node Auto-Repair](node-auto-repair)

### Customer responsibilities for AKS agent nodes

Microsoft provides patches and new images for your image nodes weekly. To keep your agent node OS and runtime components up to date, you should apply these patches and updates regularly either manually or automatically. For more information, see:

Similarly, AKS regularly releases new Kubernetes patches and minor versions. These updates can contain security or functionality improvements to Kubernetes. You're responsible to keep your clusters' Kubernetes version updated and according to the [AKS Kubernetes support version policy](supported-kubernetes-versions).

#### User customization of agent nodes

Note

AKS agent nodes appear in the Azure portal as standard Azure IaaS resources. However, these virtual machines are deployed into a custom Azure resource group (prefixed with MC_*). You can't change the base OS image or make any direct customizations to these nodes using the IaaS APIs or resources. Any custom changes that aren't performed from the AKS API won't persist through an upgrade, scale, update or reboot. Also, any change to the nodes' extensions like the **CustomScriptExtension** can lead to unexpected behavior and should be prohibited.
Avoid performing changes to the agent nodes unless Microsoft Support directs you to make changes.

AKS manages the lifecycle and operations of agent nodes on your behalf and modifying the IaaS resources associated with the agent nodes is **not supported**. An example of an unsupported operation is customizing a node pool virtual machine scale set by manually changing configurations in the Azure portal or from the API.

For workload-specific configurations or packages, AKS recommends using [Kubernetes daemon sets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/).

Using Kubernetes privileged `daemon sets`

and init containers enables you to tune/modify or install third party software on cluster agent nodes. Examples of such customizations include adding custom security scanning software or updating sysctl settings.

While this path is recommended if the above requirements apply, AKS engineering and support can't help troubleshoot or diagnose modifications that render the node unavailable due to a custom deployed `daemon set`

.

### Security issues and patching

If a security flaw is found in one or more of the managed components of AKS, the AKS team patches all affected clusters to mitigate the issue. Alternatively, the AKS team provides you with upgrade guidance.

For agent nodes affected by a security flaw, Microsoft notifies you with details on the impact and the steps to fix or mitigate the security issue.

### Node maintenance and access

Although you can sign in to and change agent nodes, doing this operation is discouraged because changes can make a cluster unsupportable.

## Network ports, access, and NSGs

You might only customize the NSGs on custom subnets. You might not customize NSGs on managed subnets or at the NIC level of the agent nodes. AKS has egress requirements to specific endpoints, to control egress and ensure the necessary connectivity, see [limit egress traffic](limit-egress-traffic). For ingress, the requirements are based on the applications you have deployed to cluster.

## Stopped, deallocated, and Not Ready nodes

If you don't need your AKS workloads to run continuously, you can [stop the AKS cluster](start-stop-cluster#stop-an-aks-cluster), which stops all nodepools and the control plane. You can start it again when needed. When you stop a cluster using the `az aks stop`

command, the cluster state is preserved for up to 12 months. After 12 months, the cluster state and all of its resources are deleted.

Manually deallocating all cluster nodes from the IaaS APIs, the Azure CLI, or the Azure portal isn't supported to stop an AKS cluster or nodepool. The cluster will be considered out of support and stopped by AKS after 30 days. The clusters are then subject to the same 12 month preservation policy as a correctly stopped cluster.

Clusters with zero **Ready** nodes (or all **Not Ready**) and zero **Running** VMs will be stopped after 30 days.

AKS reserves the right to archive control planes that have been configured out of support guidelines for extended periods equal to and beyond 30 days. AKS maintains backups of cluster etcd metadata and can readily reallocate the cluster. This reallocation is initiated by any PUT operation bringing the cluster back into support, such as an upgrade or scale to active agent nodes.

All clusters in a suspended subscription will be stopped immediately and deleted after 90 days. All clusters in a deleted subscription will be deleted immediately.

## Unsupported alpha and beta Kubernetes features

AKS only supports stable and beta features within the upstream Kubernetes project. Unless otherwise documented, AKS doesn't support any alpha feature that is available in the upstream Kubernetes project.

## Preview features or feature flags

For features and functionality that requires extended testing and user feedback, Microsoft releases new preview features or features behind a feature flag. Consider these features as prerelease or beta features.

Preview features or feature-flag features aren't meant for production. Ongoing changes in APIs and behavior, bug fixes, and other changes can result in unstable clusters and downtime.

Features in public preview fall under **best effort** support, as these features are in preview and aren't meant for production. The AKS technical support teams provides support during business hours only. For more information, see [Azure Support FAQ](https://azure.microsoft.com/support/faq/).

## Upstream bugs and issues

Given the speed of development in the upstream Kubernetes project, bugs invariably arise. Some of these bugs can't be patched or worked around within the AKS system. Instead, bug fixes require larger patches to upstream projects (such as Kubernetes, node or agent operating systems, and kernel). For components that Microsoft owns (such as the Azure cloud provider), AKS and Azure personnel are committed to fixing issues upstream in the community.

When the root cause of a technical support issue is due to one or more upstream bugs, AKS support and engineering teams will:

Identify and link the upstream bugs with any supporting details to help explain why this issue affects your cluster or workload. Customers receive links to the required repositories so they can watch the issues and see when a new release will provide fixes.

Provide potential workarounds or mitigation. If the issue can be mitigated, a

[known issue](https://github.com/Azure/AKS/issues?q=is%3Aissue+is%3Aopen+label%3Aknown-issue)is filed in the AKS repository. The known-issue filing explains:- The issue, including links to upstream bugs.
- The workaround and details about an upgrade or another persistence of the solution.
- Rough timelines for the issue's inclusion, based on the upstream release cadence.


---

<!-- DOCUMENTO FUSIONADO: private-clusters.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/private-clusters -->

# Create a private Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article helps you deploy a private link-based AKS cluster. If you're interested in creating an AKS cluster without required private link or tunnel, see [Create an Azure Kubernetes Service (AKS) cluster with API Server VNet integration](api-server-vnet-integration).

## Overview of private clusters in AKS

In a private cluster, the control plane or API server has internal IP addresses that are defined in the [RFC1918 - Address Allocation for Private Internet](https://tools.ietf.org/html/rfc1918) document. By using a private cluster, you can ensure network traffic between your API server and your node pools remains only on the private network.

The control plane or API server is in an AKS-managed Azure resource group, and your cluster or node pool is in your resource group. The server and the cluster or node pool can communicate with each other through the [Azure Private Link service](/en-us/azure/private-link/private-link-service-overview#limitations) in the API server virtual network and a private endpoint exposed on the subnet of your AKS cluster.

When you create a private AKS cluster, AKS creates both private and public fully qualified domain names (FQDNs) with corresponding DNS zones by default. For detailed DNS configuration options, see [Configure a private DNS zone, private DNS subzone, or custom subdomain](#configure-a-private-dns-zone-private-dns-subzone-or-custom-subdomain-for-a-private-aks-cluster).

## Region availability

Private clusters are available in public regions, Azure Government, and Microsoft Azure operated by 21Vianet regions where [AKS is supported](https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service).

Important

All Microsoft Defender for Cloud features will be officially retired in the Azure in China region on August 18, 2026. Due to this upcoming retirement, Azure in China customers are no longer able to onboard new subscriptions to the service. A new subscription is any subscription that was not already onboarded to the Microsoft Defender for Cloud service prior to August 18, 2025, the date of the retirement announcement. For more information on the retirement, see [Microsoft Defender for Cloud Deprecation in Microsoft Azure Operated by 21Vianet Announcement](https://aka.ms/mdcretirementinchina).

Customers should work with their account representatives for Microsoft Azure operated by 21Vianet to assess the impact of this retirement on their own operations.

## Prerequisites for private AKS clusters

- The Azure CLI version 2.28.0 or higher. Run
`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If using Azure Resource Manager (ARM) or the Azure REST API, the AKS API version must be
*2021-05-01 or higher*. - To use a custom DNS server, add the Azure public IP address
*168.63.129.16*as the upstream DNS server in the custom DNS server, and make sure to add this public IP address as the*first*DNS server. For more information about the Azure IP address, see[What is IP address 168.63.129.16?](/en-us/azure/virtual-network/what-is-ip-address-168-63-129-16)- The cluster's DNS zone should be what you forward to
*168.63.129.16*. You can find more information on zone names in[Azure services DNS zone configuration](/en-us/azure/private-link/private-endpoint-dns#azure-services-dns-zone-configuration).

- The cluster's DNS zone should be what you forward to
- Existing AKS clusters enabled with API Server VNet integration can have private cluster mode enabled. For more information, see
[Enable or disable private cluster mode on an existing cluster with API Server VNet integration](api-server-vnet-integration#enable-or-disable-private-cluster-mode-on-an-existing-cluster-with-api-server-vnet-integration).

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Limitations and considerations for private AKS clusters

- You can't apply IP authorized ranges to the private API server endpoint - they only apply to the public API server.
[Azure Private Link service limitations](/en-us/azure/private-link/private-link-service-overview#limitations)apply to private clusters.- There's no support for Azure DevOps Microsoft-hosted Agents with private clusters. Consider using
[self-hosted agents](/en-us/azure/devops/pipelines/agents/agents). - If you need to enable Azure Container Registry on a private AKS cluster,
[set up a private link for the container registry in the cluster virtual network (VNet)](/en-us/azure/container-registry/container-registry-private-link)or set up peering between the container registry's virtual network and the private cluster's virtual network. - Deleting or modifying the private endpoint in the customer subnet causes the cluster to stop functioning.
- Azure Private Link service is supported on Standard Azure Load Balancer only. Basic Azure Load Balancer isn't supported.

## Hub and spoke with custom DNS for private AKS clusters

[Hub and spoke architectures](/en-us/azure/architecture/reference-architectures/hybrid-networking/hub-spoke) are commonly used to deploy networks in Azure. In many of these deployments, DNS settings in the spoke VNets are configured to reference a central DNS forwarder to allow for on-premises and Azure-based DNS resolution.

Keep the following considerations in mind when deploying private AKS clusters in hub and spoke architectures with custom DNS:

When a private cluster is created, a private endpoint (1) and a private DNS zone (2) are created in the cluster-managed resource group by default. The cluster uses an

`A`

record in the private zone to resolve the IP of the private endpoint for communication to the API server.The private DNS zone is linked only to the VNet that the cluster nodes are attached to (3), which means that the private endpoint can only be resolved by hosts in that linked VNet. In scenarios where no custom DNS is configured on the VNet (default), it works without issue as hosts point at

*168.63.129.16*for DNS that can resolve records in the private DNS zone because of the link.If you keep the default private DNS zone behavior, AKS tries to link the zone directly to the spoke VNet that hosts the cluster even when the zone is already linked to a hub VNet.

In spoke VNets that use custom DNS servers, this action can fail if the cluster's managed identity lacks

**Network Contributor**on the spoke VNet.To prevent the failure, choose

**one**of the following supported configurations:**Custom private DNS zone**: Provide a precreated private zone and set`privateDNSZone`

/`--private-dns-zone`

to its resource ID. Link that zone to the appropriate VNet (for example, the hub VNet) and set`publicDNS`

to`false`

/ use`--disable-public-fqdn`

.**Public DNS only**: Disable private zone creation by setting`privateDNSZone`

/`--private-dns-zone`

to`none`

**and**leave`publicDNS`

at its default value (`true`

) / don't use`--disable-public-fqdn`

.

If you're using

[bring your own (BYO) route table with kubenet](configure-kubenet#bring-your-own-subnet-and-route-table-with-kubenet)and BYO DNS with private clusters, cluster creation fails. You need to associate thein the node resource group to the subnet after the cluster creation failed to make the creation successful.`RouteTable`


Keep the following limitations in mind when using custom DNS with private AKS clusters:

- Setting
`privateDNSZone`

/`--private-dns-zone`

to`none`

**and**`publicDNS: false`

/`--disable-public-fqdn`

at the same time**isn't supported**. - Conditional forwarding doesn't support subdomains.

## Create a private AKS cluster with default basic networking

Create a resource group using the

command. You can also use an existing resource group for your AKS cluster.`az group create`

`az group create \ --name <private-cluster-resource-group> \ --location <location>`

Create a private cluster with default basic networking using the

command with the`az aks create`

`--enable-private-cluster`

flag.**Key parameters in this command**:`--enable-private-cluster`

: Enables private cluster mode.

`az aks create \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --load-balancer-sku standard \ --enable-private-cluster \ --generate-ssh-keys`


## Create a private AKS cluster with advanced networking

Create a resource group using the

command. You can also use an existing resource group for your AKS cluster.`az group create`

`az group create \ --name <private-cluster-resource-group> \ --location <location>`

Create a private cluster with advanced networking using the

command.`az aks create`

**Key parameters in this command**:`--enable-private-cluster`

: Enables private cluster mode.`--network-plugin azure`

: Specifies the Azure CNI networking plugin.`--vnet-subnet-id`

: The resource ID of an existing subnet in a virtual network.`--dns-service-ip`

: An available IP address within the Kubernetes service address range to use for the cluster DNS service.`--service-cidr`

: A CIDR notation IP range from which to assign service cluster IPs.

`az aks create \ --resource-group <private-cluster-resource-group> \ --name <private-cluster-name> \ --load-balancer-sku standard \ --enable-private-cluster \ --network-plugin azure \ --vnet-subnet-id <subnet-id> \ --dns-service-ip 10.2.0.10 \ --service-cidr 10.2.0.0/24 --generate-ssh-keys`


## Use custom domains with private AKS clusters

If you want to configure custom domains that can only be resolved internally, see [Use custom domains](coredns-custom#use-custom-domains).

## Disable a public FQDN on a private AKS cluster

### Disable a public FQDN on a new cluster

Disable a public FQDN when creating a private AKS cluster using the

command with the`az aks create`

`--disable-public-fqdn`

flag.`az aks create \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --load-balancer-sku standard \ --enable-private-cluster \ --assign-identity <resource-id> \ --private-dns-zone <private-dns-zone-mode> \ --disable-public-fqdn \ --generate-ssh-keys`


### Disable a public FQDN on an existing cluster

Disable a public FQDN on an existing AKS cluster using the

command with the`az aks update`

`--disable-public-fqdn`

flag.`az aks update \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --disable-public-fqdn`


## Configure a private DNS zone, private DNS subzone, or custom subdomain for a private AKS cluster

You can configure private DNS settings for a private AKS cluster using the Azure CLI (with the `--private-dns-zone`

parameter) or an Azure Resource Manager (ARM) template (with the `privateDNSZone`

property). The following table outlines the options available for the `--private-dns-zone`

parameter / `privateDNSZone`

property:

| Setting | Description |
|---|---|
`system` |
The default value when configuring a private DNS zone. If you omit `--private-dns-zone` / `privateDNSZone` , AKS creates a private DNS zone in the node resource group. |
`none` |
If you set `--private-dns-zone` / `privateDNSZone` to `none` , AKS doesn't create a private DNS zone. |
`<custom-private-dns-zone-resource-id>` |
To use this parameter, you need to create a private DNS zone in the following format for Azure global cloud: `privatelink.<region>.azmk8s.io` or `<subzone>.privatelink.<region>.azmk8s.io` . You need the resource ID of the private DNS zone for future use. You also need a user-assigned identity or service principal with the
`private.<region>.azmk8s.io` or `<subzone>.private.<region>.azmk8s.io` . You can't change or delete this resource after creating the cluster, as it can cause performance issues and cluster upgrade failures. You can use `--fqdn-subdomain <subdomain>` with `<custom-private-dns-zone-resource-id>` only to provide subdomain capabilities to `privatelink.<region>.azmk8s.io` . If you're specifying a subzone, there's a 32 character limit for the `<subzone>` name. |

Keep the following considerations in mind when configuring private DNS for a private AKS cluster:

- If the private DNS zone is in a different subscription than the AKS cluster, you need to register the
`Microsoft.ContainerServices`

Azure provider in both subscriptions. - If your AKS cluster is configured with an Active Directory service principal, AKS doesn't support using a system-assigned managed identity with custom private DNS zone. The cluster must use
[user-assigned managed identity authentication](use-managed-identity).

## Create a private AKS cluster with a private DNS zone

Create a private AKS cluster with a private DNS zone using the

command.`az aks create`

**Key parameters in this command**:`--enable-private-cluster`

: Enables private cluster mode.`--private-dns-zone [system|none]`

: Configures the private DNS zone for the cluster. The default value is`system`

.`--assign-identity <resource-id>`

: The resource ID of a user-assigned managed identity with the[Private DNS Zone Contributor](/en-us/azure/role-based-access-control/built-in-roles#dns-zone-contributor)and[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)roles.

`az aks create \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --load-balancer-sku standard \ --enable-private-cluster \ --assign-identity <resource-id> \ --private-dns-zone [system|none] \ --generate-ssh-keys`


## Create a private AKS cluster with a custom private DNS zone or private DNS subzone

Create a private AKS cluster with a custom private DNS zone or subzone using the

command.`az aks create`

**Key parameters in this command**:`--enable-private-cluster`

: Enables private cluster mode.`--private-dns-zone <custom-private-dns-zone-resource-id>|<custom-private-dns-subzone-resource-id>`

: The resource ID of a precreated private DNS zone or subzone in the following format for Azure global cloud:`privatelink.<region>.azmk8s.io`

or`<subzone>.privatelink.<region>.azmk8s.io`

.`--assign-identity <resource-id>`

: The resource ID of a user-assigned managed identity with the[Private DNS Zone Contributor](/en-us/azure/role-based-access-control/built-in-roles#dns-zone-contributor)and[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)roles.

`# The custom private DNS zone name should be in the following format: "<subzone>.privatelink.<region>.azmk8s.io" az aks create \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --load-balancer-sku standard \ --enable-private-cluster \ --assign-identity <resource-id> \ --private-dns-zone [<custom-private-dns-zone-resource-id>|<custom-private-dns-subzone-resource-id>] \ --generate-ssh-keys`


## Create a private AKS cluster with a custom private DNS zone and custom subdomain

Create a private AKS cluster with a custom private DNS zone and subdomain using the

command.`az aks create`

**Key parameters in this command**:`--enable-private-cluster`

: Enables private cluster mode.`--private-dns-zone <custom-private-dns-zone-resource-id>`

: The resource ID of a precreated private DNS zone in the following format for Azure global cloud:`privatelink.<region>.azmk8s.io`

.`--fqdn-subdomain <subdomain>`

: The subdomain to use for the cluster FQDN within the custom private DNS zone.`--assign-identity <resource-id>`

: The resource ID of a user-assigned managed identity with the[Private DNS Zone Contributor](/en-us/azure/role-based-access-control/built-in-roles#dns-zone-contributor)and[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)roles.

`# The custom private DNS zone name should be in one of the following formats: "privatelink.<region>.azmk8s.io" or "<subzone>.privatelink.<region>.azmk8s.io" az aks create \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --load-balancer-sku standard \ --enable-private-cluster \ --assign-identity <resource-id> \ --private-dns-zone <custom-private-dns-zone-resource-id> \ --fqdn-subdomain <subdomain> \ --generate-ssh-keys`


## Update an existing private AKS cluster from a private DNS zone to public

You can only update from `byo`

(bring your own) or `system`

to `none`

. No other combination of update values is supported.

Warning

When you update a private cluster from `byo`

or `system`

to `none`

, the agent nodes change to use a public FQDN. In an AKS cluster that uses Azure Virtual Machine Scale Sets, a [node image upgrade](node-image-upgrade) is performed to update your nodes with the public FQDN.

Update a private cluster from

`byo`

or`system`

to`none`

using thecommand with the`az aks update`

`--private-dns-zone`

parameter set to`none`

.`az aks update \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --private-dns-zone none`


## Configure kubectl to connect to a private AKS cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, use the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials --resource-group <private-cluster-resource-group> --name <private-cluster-name>`

Verify the connection to your cluster using the

command. This command returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`

The command returns output similar to the following example output:

`NAME STATUS ROLES AGE VERSION aks-nodepool1-12345678-vmss000000 Ready agent 3h6m v1.15.11 aks-nodepool1-12345678-vmss000001 Ready agent 3h6m v1.15.11 aks-nodepool1-12345678-vmss000002 Ready agent 3h6m v1.15.11`
