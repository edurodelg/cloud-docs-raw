---
merged_at: 2026-01-28T07:16:09.845033
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-isolated -->

# Network isolated Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Organizations typically have strict security and compliance requirements to regulate egress (outbound) network traffic from a cluster to eliminate risks of data exfiltration. By default, standard SKU Azure Kubernetes Service (AKS) clusters have unrestricted outbound internet access. This level of network access allows nodes and services you run to access external resources as needed. If you wish to restrict egress traffic, a limited number of ports and addresses must be accessible to maintain healthy cluster maintenance tasks. The conceptual document on [outbound network and fully qualified domain name (FQDN) rules for AKS clusters](outbound-rules-control-egress) provides a list of required endpoints for the AKS cluster and its optional add-ons and features.

One common solution to restricting outbound traffic from the cluster is to use a [firewall device](limit-egress-traffic) to restrict traffic based on firewall rules. Firewall is applicable when your application requires outbound access, but when outbound requests have to be inspected and secured. Configuring a firewall manually with required egress rules and *FQDNs* is a cumbersome process especially if your only requirement is to create an isolated AKS cluster with no outbound dependencies for the cluster bootstrapping.

To reduce risk of data exfiltration, network isolated cluster allows for bootstrapping the AKS cluster without any outbound network dependencies, even for fetching cluster components/images from Microsoft Artifact Registry (MAR). The cluster operator could incrementally set up allowed outbound traffic for each scenario they want to enable.

## How a network isolated cluster works

The following diagram shows the network communication between dependencies for a network isolated cluster.


AKS clusters fetch artifacts required for the cluster and its features or add-ons from the Microsoft Artifact Registry (MAR). This image pull allows AKS to provide newer versions of the cluster components and to also address critical security vulnerabilities. A network isolated cluster attempts to pull those images and binaries from a private Azure Container Registry (ACR) instance connected to the cluster instead of pulling from MAR. If the images aren't present, the private ACR pulls them from MAR and serves them via its private endpoint, eliminating the need to enable egress from the cluster to the public MAR endpoint.

The following two options are supported for a private ACR associated with network isolated clusters:

**AKS-managed ACR**- AKS creates, manages, and reconciles an ACR resource in this option. There's nothing you need to do.Note

The AKS-managed ACR resource is created in your subscription. If you delete the cluster with AKS-managed ACR for bootstrap artifact source. Related resources such as the AKS-managed ACR, private link, and private endpoint are also automatically deleted. If you change outbound type on a cluster to any type other than

`none`

or`block`

with`--bootstrap-artifact-source`

retained as`Cache`

. Then the related resources are not deleted.**Bring your own (BYO) ACR**- The BYO ACR option requires creating an ACR with a private link between the ACR resource and the AKS cluster. See[Connect privately to an Azure container registry using Azure Private Link](/en-us/azure/container-registry/container-registry-private-link)to understand how to configure a private endpoint for your registry. You also need to assign permissions and manage the cache rules, private link, and private endpoint used in the cluster.Note

When you delete the AKS cluster or after you disable the feature. The BYO ACR, private link, and private endpoint aren't deleted automatically. If you add customized images and cache rules to the BYO ACR, they persist after cluster reconciliation.


To create a network isolated cluster, you need to first ensure network traffic between your API server and your node pools remains only on the private network, you can choose one of the following private cluster modes:

[Private link-based cluster](private-clusters)- The control plane or API server is in an AKS-managed Azure resource group, and your node pool is in your resource group. The server and the node pool can communicate with each other through the Azure Private Link service in the API server virtual network and a private endpoint which is exposed on the subnet of your AKS cluster.[API Server VNet Integration configured cluster](api-server-vnet-integration)- A cluster configured with API Server VNet Integration projects the API server endpoint directly into a delegated subnet in the virtual network where AKS is deployed. API Server VNet Integration enables network communication between the API server and the cluster nodes without requiring a private link or tunnel.

You also need to ensure the egress path for your AKS cluster are controlled and limited, you can choose one of the following network outbound types:

[Outbound type of](/en-us/azure/aks/egress-outboundtype#outbound-type-of-none)- If`none`

`none`

is set. AKS doesn't automatically configure egress paths and a default route is not required. It is supported in both bring-your-own (BYO) virtual network scenarios and managed virtual network scenarios. For bring your own virtual network scenario, you must establish explicit egress paths if needed.[Outbound type of](/en-us/azure/aks/egress-outboundtype#outbound-type-of-block-preview)-If`block`

(preview)`block`

is set. AKS configures network rules to actively block all egress traffic from the cluster. This option is useful for highly secure environments where outbound connectivity must be restricted. It is supported in managed virtual network scenario. You can also achieve similar effect by blocking all egress traffic by adding[network security group (NSG)](/en-us/azure/virtual-network/network-security-groups-overview)rules with`none`

in bring-your-own virtual network scenario.

Note

Outbound type of `none`

is generally available.
Outbound type `block`

is in preview.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Limitations

`Unmanaged`

channel is not supported.- Windows node pools are not yet supported.
- kubenet networking is not supported.

Caution

If you are using [Node Public IP](use-node-public-ips) in network isolated AKS clusters, it will allow outbound traffic with outbound type `none`

.

## Using features, add-ons, and extensions requiring egress

For network isolated clusters with BYO ACR:

- If you want to use any AKS feature or add-on that requires outbound network access in network isolated clusters with outbound type
`none`

,[this document](outbound-rules-control-egress)contains the outbound network requirements for each feature. Also, this doc enumerates the features or add-ons that support private link integration for secure connection from within the cluster's virtual network. It is recommended to set up private endpoints to access these features. For example, you can set up[private endpoint based ingestion](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-private-link)to use Managed Prometheus (Azure Monitor workspace) and Container insights (Log Analytics workspace) in network isolated clusters. If a private link integration is not available for any of these features. Then you can set up the cluster with a[user-defined routing table and an Azure Firewall](limit-egress-traffic)based on the network rules and application rules that required for that feature. - If you are using
[Azure Container Storage Interface (CSI) driver](azure-files-csi)for Azure Files and Blob storage, you must create a custom storage class with "networkEndpointType: privateEndpoint", see examples in[Azure Files storage classes](/en-us/azure/aks/azure-csi-files-storage-provision#dynamically-provision-a-volume)and[Azure Blob storage classes](/en-us/azure/aks/azure-csi-blob-storage-provision?tabs=mount-nfs%2Csecret#storage-class-parameters-for-dynamic-persistent-volumes). - The following AKS cluster extensions aren't supported yet on network isolated clusters:

## Frequently asked questions

### What's the difference between network isolated cluster and Azure Firewall?

A network isolated cluster doesn't require any egress traffic beyond the VNet throughout the cluster bootstrapping process. A network isolated cluster has outbound type as either `none`

or `block`

. If the outbound type is set to `none`

, then AKS doesn't set up any outbound connections for the cluster, allowing the user to configure them on their own. If the outbound type is set to `block`

, then all outbound connections are blocked.

A firewall typically establishes a barrier between a trusted network and an untrusted network, such as the Internet. Azure Firewall, for example, can restrict outbound HTTP and HTTPS traffic that's based on the destination. It gives you fine-grained control of egress traffic, but at the same time allows you to provide access to the FQDNs encompassing an AKS cluster’s outbound dependencies. This is something that NSGs can't do. For example, you can set outbound type of the cluster to `userDefinedRouting`

to force outbound traffic through the firewall and then configure FQDN restrictions on outbound traffic. There are many cases where you still want a firewall. Such as you have outbound traffic anyway from your application or you want to control, inspect, and secure the cluster traffic both egress and ingress.

In summary, while Azure Firewall can be used to define egress restrictions on clusters with outbound requests, network isolated clusters go further on secure-by-default posture by eliminating or blocking the outbound requests altogether.

### Do I need to set up any allowlist endpoints for the network isolated cluster to work?

The cluster creation and bootstrapping stages don't require any outbound traffic from the network isolated cluster. Images required for AKS components and addons are pulled from the private ACR connected to the cluster instead of pulling from Microsoft Artifact Registry (MAR) over public endpoints.

After setting up a network isolated cluster. If you want to enable features or add-ons that need to make outbound requests to their service endpoints, you can set up private endpoints to the services powered by Azure Private Link.

### Can I manually upgrade packages to upgrade node pool image?

Manually upgrading packages based on egress to package repositories is not recommended. Instead, you can [manually upgrade](node-image-upgrade) or [autoupgrade your node OS images](auto-upgrade-node-os-image). Only `NodeImage`

and `None`

upgrade channels are currently supported for network isolated clusters.

### What if I change the outbound type other than `none`

or `block`

, does that still make a network isolated cluster?

The only supported outbound types for a network isolated cluster are outbound type `none`

and `block`

. If you use any other outbound type, the cluster may still pull artifacts from the private ACR associated, however that may generate egress traffic.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kms-data-encryption-concepts -->

# Data encryption at rest concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) stores sensitive data such as Kubernetes secrets in etcd, the distributed key-value store used by Kubernetes. For enhanced security and compliance requirements, AKS supports encryption of Kubernetes secrets at rest using the Kubernetes Key Management Service (KMS) provider integrated with Azure Key Vault.

This article explains the key concepts, encryption models, and key management options available for protecting Kubernetes secrets at rest in AKS.

## Understanding data encryption at rest

Data encryption at rest protects your data when it's stored on disk. Without encryption at rest, an attacker who gains access to the underlying storage could potentially read sensitive data like Kubernetes secrets.

AKS provides encryption for Kubernetes secrets stored in etcd:

| Layer | Description |
|---|---|
Azure platform encryption |
Azure Storage automatically encrypts all data at rest using 256-bit AES encryption. This encryption is always enabled and transparent to users. |
KMS provider encryption |
An optional layer that encrypts Kubernetes secrets before they're written to etcd using keys stored in Azure Key Vault. |

For more information about Azure's encryption at rest capabilities, see [Azure data encryption at rest](/en-us/azure/security/fundamentals/encryption-atrest) and [Azure encryption models](/en-us/azure/security/fundamentals/encryption-models).

## KMS provider for data encryption

The [Kubernetes KMS provider](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/) is a mechanism that enables encryption of Kubernetes secrets at rest using an external key management system. AKS integrates with Azure Key Vault to provide this capability, giving you control over encryption keys while maintaining the security benefits of a managed Kubernetes service.

### How KMS encryption works

When you enable KMS for an AKS cluster:

**Secret creation**: When a secret is created, the Kubernetes API server sends the secret data to the KMS provider plugin.**Encryption**: The KMS plugin encrypts the secret data using a Data Encryption Key (DEK), which is itself encrypted using a Key Encryption Key (KEK) stored in Azure Key Vault.**Storage**: The encrypted secret is stored in etcd.**Secret retrieval**: When a secret is read, the KMS plugin decrypts the DEK using the KEK from Azure Key Vault, then uses the DEK to decrypt the secret data.

This envelope encryption approach provides both security and performance benefits. The DEK handles frequent encryption operations locally while the KEK in Azure Key Vault provides the security of a hardware-backed key management system.

## Key management options

AKS offers two key management options for KMS encryption:

### Platform-managed keys (PMK)

With platform-managed keys, AKS automatically manages the encryption keys for you:

- AKS creates and manages the encryption keys.
- Key rotation is handled automatically by the platform.
- No additional configuration or key vault setup is required.

**When to use platform-managed keys:**

- You want the simplest setup with minimal configuration.
- You don't have specific regulatory requirements that mandate customer-managed keys.
- You want automatic key rotation without manual intervention.

### Customer-managed keys (CMK)

With customer-managed keys, you have full control over the encryption keys:

- You create and manage your own Azure Key Vault and encryption keys.
- You control key rotation schedules and policies.

**When to use customer-managed keys:**

- You have regulatory or compliance requirements that mandate customer-managed keys.
- You need to control the key lifecycle, including rotation schedules and key versions.
- You require audit logs for all key operations.

### Key vault network access options

When using customer-managed keys, you can configure the network access for your Azure Key Vault:

| Network access | Description | Use case |
|---|---|---|
Public |
Key vault is accessible over the public internet with authentication. | Development environments, simpler setup |
Private |
Key vault has public network access disabled. AKS accesses the key vault through the
|

## Comparing encryption key options

| Feature | Platform-managed keys | Customer-managed keys (Public) | Customer-managed keys (Private) |
|---|---|---|---|
Key ownership |
Microsoft manages | Customer manages | Customer manages |
Key rotation |
Automatic |
|

[User configurable](/en-us/azure/key-vault/keys/how-to-configure-key-rotation)**Key vault creation****Network isolation**## Requirements

- The new
[KMS encryption with platform-managed keys or customer-managed keys with automatic key rotation](kms-data-encryption)experience requires**Kubernetes version 1.33 or later**. - The new
[KMS encryption with platform-managed keys or customer-managed keys with automatic key rotation](kms-data-encryption)experience is only supported on AKS clusters where[managed identity is used for the cluster's identity](use-managed-identity).

## Limitations

**No downgrade**: After enabling the new KMS encryption experience, you can't disable the feature.**Key deletion**: Deleting the encryption key or key vault makes your secrets unrecoverable.**Private endpoint access**: Key vault access using[private link/endpoint](/en-us/azure/key-vault/general/private-link-service)isn't yet supported. For private key vaults, use the[trusted services firewall exception](/en-us/azure/key-vault/general/network-security#key-vault-firewall-enabled-trusted-services-only).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-hybrid-benefit -->

# What is Azure Hybrid Benefit for Azure Kubernetes Service?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Hybrid Benefit is a program that enables you to significantly reduce the costs of running workloads in the cloud. With Azure Hybrid Benefit for Azure Kubernetes Service (AKS), you can maximize the value of your on-premises licenses and modernize your applications at no extra cost. Azure Hybrid Benefit enables you to use your on-premises licenses that also have either active Software Assurance (SA) or a qualifying subscription to get Windows virtual machines (VMs) on Azure at a reduced cost.

For more information on qualifications for Azure Hybrid Benefit, what is included with it, how to stay compliant, and more, check out [Azure Hybrid Benefit for Windows Server](/en-us/azure/virtual-machines/windows/hybrid-use-benefit-licensing).

Note

Azure Hybrid Benefit for Azure Kubernetes Service follows the same licensing guidance as Azure Hybrid Benefit for Windows Server VMs on Azure.

## Enable Azure Hybrid Benefit for Azure Kubernetes Service

Azure Hybrid Benefit for Azure Kubernetes Service can be enabled at cluster creation or on an existing AKS cluster. You can enable and disable Azure Hybrid Benefit using either the Azure CLI or Azure PowerShell. In the following examples, be sure to replace the variable definitions with values matching your own cluster.

To create a new AKS cluster with Azure Hybrid Benefit enabled:

```
PASSWORD='' # replace with your own password value
RG_NAME='myResourceGroup'
CLUSTER='myAKSCluster'
az aks create \
--resource-group $RG_NAME \
--name $CLUSTER \
--load-balancer-sku Standard \
--network-plugin azure \
--windows-admin-username azure \
--windows-admin-password $PASSWORD \
--enable-ahub \
--generate-ssh-keys
```


To enable Azure Hybrid Benefit on an existing AKS cluster:

```
RG_NAME='myResourceGroup'
CLUSTER='myAKSCluster'
az aks update --resource-group $RG_NAME --name $CLUSTER--enable-ahub
```


## Disable Azure Hybrid Benefit for Azure Kubernetes Service

To disable Azure Hybrid Benefit for an AKS cluster:

```
RG_NAME='myResourceGroup'
CLUSTER='myAKSCluster'
az aks update --resource-group $RG_NAME --name $CLUSTER --disable-ahub
```


## Next steps

To learn more about Windows containers on AKS, see the following resources:

[Learn how to deploy, manage, and monitor Windows containers on AKS](/en-us/training/paths/deploy-manage-monitor-wincontainers-aks).- Open an issue or provide feedback in the
[Windows containers GitHub repository](https://github.com/microsoft/Windows-Containers/issues). - Review the
[third-party partner solutions for Windows on AKS](windows-aks-partner-solutions).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/update-kms-key-vault -->

# Update the key vault mode for an Azure Kubernetes Service (AKS) cluster with Key Management Service (KMS) etcd encryption (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to update the key vault mode from public to private or private to public for an Azure Kubernetes Service (AKS) cluster with Key Management Service (KMS) etcd encryption.

## Prerequisites

- An AKS cluster with KMS etcd encryption enabled. For more information, see
[Add Key Management Service (KMS) etcd encryption to an Azure Kubernetes Service (AKS) cluster](use-kms-etcd-encryption). - Azure CLI version 2.39.0 or later. Find your version using the
`az --version`

command. If you need to install or upgrade, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

## Update a key vault mode

Note

To change a different key vault with a different mode (whether public or private), you can run [ az aks update](/en-us/cli/azure/aks#az-aks-update) directly. To change the mode of an attached key vault, you must first turn off KMS, then turn it on again using the new key vault IDs.

Turn off KMS on the existing cluster and release the key vault using the

command with the`az aks update`

`--disable-azure-keyvault-kms`

parameter.`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --disable-azure-keyvault-kms`

Warning

After you turn off KMS, the encryption key vault key is still needed. You can't delete or expire it.

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`

Update the key vault from public to private using the

command with the`az keyvault update`

`--public-network-access`

parameter set to`Disabled`

.`az keyvault update --name $KEY_VAULT --resource-group $RESOURCE_GROUP --public-network-access Disabled`

Turn on KMS with the updated private key vault using the

command with the`az aks update`

`--azure-keyvault-kms-key-vault-network-access`

parameter set to`Private`

.`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --enable-azure-keyvault-kms \ --azure-keyvault-kms-key-id $KEY_ID \ --azure-keyvault-kms-key-vault-network-access "Private" \ --azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices-performance-scale -->

# Best practices for performance and scaling for small to medium workloads in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This article focuses on general best practices for **small to medium workloads**. For best practices specific to **large workloads**, see [Performance and scaling best practices for large workloads in Azure Kubernetes Service (AKS)](best-practices-performance-scale-large).

As you deploy and maintain clusters in AKS, you can use the following best practices to help you optimize performance and scaling.

In this article, you learn about:

- Tradeoffs and recommendations for autoscaling your workloads.
- Managing node scaling and efficiency based on your workload demands.
- Networking considerations for ingress and egress traffic.
- Monitoring and troubleshooting control plane and node performance.
- Capacity planning, surge scenarios, and cluster upgrades.
- Storage and networking considerations for data plane performance.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Application autoscaling vs. infrastructure autoscaling

### Application autoscaling

Application autoscaling is useful when dealing with cost optimization or infrastructure limitations. A well-configured autoscaler maintains high availability for your application while also minimizing costs. You only pay for the resources required to maintain availability, regardless of the demand.

For example, if an existing node has space but not enough IPs in the subnet, it might be able to skip the creation of a new node and instead immediately start running the application on a new pod.

#### Horizontal Pod autoscaling

Implementing [horizontal pod autoscaling](concepts-scale#horizontal-pod-autoscaler) is useful for applications with a steady and predictable resource demand. The Horizontal Pod Autoscaler (HPA) dynamically scales the number of pod replicas, which effectively distributes the load across multiple pods and nodes. This scaling mechanism is typically most beneficial for applications that can be decomposed into smaller, independent components capable of running in parallel.

The HPA provides resource utilization metrics by default. You can also integrate custom metrics or leverage tools like the [Kubernetes Event-Driven Autoscaler (KEDA) (Preview)](keda-about). These extensions allow the HPA to make scaling decisions based on multiple perspectives and criteria, providing a more holistic view of your application's performance. This is especially helpful for applications with varying complex scaling requirements.

Note

If maintaining high availability for your application is a top priority, we recommend leaving a slightly higher buffer for the minimum pod number for your HPA to account for scaling time.

#### Vertical Pod autoscaling

Implementing [vertical pod autoscaling](vertical-pod-autoscaler) is useful for applications with fluctuating and unpredictable resource demands. The Vertical Pod Autoscaler (VPA) allows you to fine-tune resource requests, including CPU and memory, for individual pods, enabling precise control over resource allocation. This granularity minimizes resource waste and enhances the overall efficiency of cluster utilization. The VPA also streamlines application management by automating resource allocation, freeing up resources for critical tasks.

Warning

You shouldn't use the VPA in conjunction with the HPA on the same CPU or memory metrics. This combination can lead to conflicts, as both autoscalers attempt to respond to changes in demand using the same metrics. However, you can use the VPA for CPU or memory in conjunction with the HPA for custom metrics to prevent overlap and ensure that each autoscaler focuses on distinct aspects of workload scaling.

Note

The VPA works based on historical data. We recommend waiting at least *24 hours* after deploying the VPA before applying any changes to give it time to collect recommendation data.

### Infrastructure autoscaling

#### Cluster autoscaling

Implementing cluster autoscaling is useful if your existing nodes lack sufficient capacity, as it helps with scaling up and provisioning new nodes.

When considering cluster autoscaling, the decision of when to remove a node involves a tradeoff between optimizing resource utilization and ensuring resource availability. Eliminating underutilized nodes enhances cluster utilization but might result in new workloads having to wait for resources to be provisioned before they can be deployed. It's important to find a balance between these two factors that aligns with your cluster and workload requirements and [configure the cluster autoscaler profile settings accordingly](cluster-autoscaler#update-the-cluster-autoscaler-settings).

The Cluster Autoscaler profile settings apply universally to all autoscaler-enabled node pools in your cluster. This means that any scaling actions occurring in one autoscaler-enabled node pool might impact the autoscaling behavior in another node pool. It's important to apply consistent and synchronized profile settings across all relevant node pools to ensure that the autoscaler behaves as expected.

##### Overprovisioning

Overprovisioning is a strategy that helps mitigate the risk of application pressure by ensuring there's an excess of readily available resources. This approach is especially useful for applications that experience highly variable loads and cluster scaling patterns that show frequent scale ups and scale downs.

To determine the optimal amount of overprovisioning, you can use the following formula:

```
1-buffer/1+traffic
```


For example, let's say you want to avoid hitting 100% CPU utilization in your cluster. You might opt for a 30% buffer to maintain a safety margin. If you anticipate an average traffic growth rate of 40%, you might consider overprovisioning by 50%, as calculated by the formula:

```
1-30%/1+40%=50%
```


An effective overprovisioning method involves the use of *pause pods*. Pause pods are low-priority deployments that can be easily replaced by high-priority deployments. You create low priority pods that serve the sole purpose of reserving buffer space. When a high-priority pod requires space, the pause pods are removed and rescheduled on another node or a new node to accommodate the high priority pod.

The following YAML shows an example pause pod manifest:

```
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
name: overprovisioning
value: -1
globalDefault: false
description: "Priority class used by overprovisioning."
---
apiVersion: apps/v1
kind: Deployment
metadata:
name: overprovisioning
namespace: kube-system
spec:
replicas: 1
selector:
matchLabels:
run: overprovisioning
template:
metadata:
labels:
run: overprovisioning
spec:
priorityClassName: overprovisioning
containers:
- name: reserve-resources
image: your-custome-pause-image
resources:
requests:
cpu: 1
memory: 4Gi
```


## Node scaling and efficiency


Best practice guidance:Carefully monitor resource utilization and scheduling policies to ensure nodes are being used efficiently.


Node scaling allows you to dynamically adjust the number of nodes in your cluster based on workload demands. It's important to understand that adding more nodes to a cluster isn't always the best solution for improving performance. To ensure optimal performance, you should carefully monitor resource utilization and scheduling policies to ensure nodes are being used efficiently.

### Node images


Best practice guidance:Use the latest node image version to ensure that you have the latest security patches and bug fixes.


Using the latest node image version provides the best performance experience. AKS ships performance improvements within the weekly image releases. The latest daemonset images are cached on the latest VHD image, which provide lower latency benefits for node provisioning and bootstrapping. Falling behind on updates might have a negative impact on performance, so it's important to avoid large gaps between versions.

#### Azure Linux

The [Azure Linux Container Host on AKS](/en-us/azure/azure-linux/intro-azure-linux) uses a native AKS image and provides a single place for Linux development. Every package is built from source and validated, ensuring your services run on proven components.

Azure Linux is lightweight, only including the necessary set of packages to run container workloads. It provides a reduced attack surface and eliminates patching and maintenance of unnecessary packages. At its base layer, it has a Microsoft-hardened kernel tuned for Azure. This image is ideal for performance-sensitive workloads and platform engineers or operators that manage fleets of AKS clusters.

#### Ubuntu 2204

The [Ubuntu 2204 image](https://github.com/Azure/AKS/blob/master/CHANGELOG.md) is the default node image for AKS. It's a lightweight and efficient operating system optimized for running containerized workloads. This means that it can help reduce resource usage and improve overall performance. The image includes the latest security patches and updates, which help ensure that your workloads are protected from vulnerabilities.

The Ubuntu 2204 image is fully supported by Microsoft, Canonical, and the Ubuntu community and can help you achieve better performance and security for your containerized workloads.

### Virtual machines (VMs)


Best practice guidance:When selecting a VM, ensure the size and performance of the OS disk and VM SKU don't have a large discrepancy. A discrepancy in size or performance can cause performance issues and resource contention.


Application performance is closely tied to the VM SKUs you use in your workloads. Larger and more powerful VMs, generally provide better performance. For *mission critical or product workloads*, we recommend using VMs with at least an 8-core CPU. VMs with newer hardware generations, like v4 and v5, can also help improve performance. Keep in mind that create and scale latency might vary depending on the VM SKUs you use.

### Use dedicated system node pools

For scaling performance and reliability, we recommend using a dedicated system node pool. With this configuration, the dedicated system node pool reserves space for critical system resources such as system OS daemons. Your application workload can then run in a user node pool to increase the availability of allocatable resources for your application. This configuration also helps mitigate the risk of resource competition between the system and application.

### Create operations

Review the extensions and add-ons you have enabled during create provisioning. Extensions and add-ons can add latency to overall duration of create operations. If you don't need an extension or add-on, we recommend removing it to improve create latency.

You can also use availability zones to provide a higher level of availability to protect against potential hardware failures or planned maintenance events. AKS clusters distribute resources across logical sections of underlying Azure infrastructure. Availability zones physically separate nodes from other nodes to help ensure that a single failure doesn't impact the availability of your application. Availability zones are only available in certain regions. For more information, see [Availability zones in Azure](/en-us/azure/reliability/availability-zones-overview).

## Kubernetes API server

### LIST and WATCH operations

Kubernetes uses the LIST and WATCH operations to interact with the Kubernetes API server and monitor information about cluster resources. These operations are fundamental to how Kubernetes performs resource management.

**The LIST operation retrieves a list of resources that fit within certain criteria**, such as all pods in a specific namespace or all services in the cluster. This operation is useful when you want to get an overview of your cluster resources or you need to operator on multiple resources at once.

The LIST operation can retrieve large amounts of data, especially in large clusters with multiple resources. Be mindful of the fact that making unbounded or frequent LIST calls puts a significant load on the API server and can close down response times.

**The WATCH operation performs real-time resource monitoring**. When you set up a WATCH on a resource, the API server sends you updates whenever there are changes to that resource. This is important for controllers, like the ReplicaSet controller, which rely on WATCH to maintain the desired state of resources.

Be mindful of the fact that watching too many mutable resources or making too many concurrent WATCH requests can overwhelm the API server and cause excessive resource consumption.

To avoid potential issues and ensure the stability of the Kubernetes control plane, you can use the following strategies:

**Resource quotas**

Implement resource quotas to limit the number of resources that can be listed or watched by a particular user or namespace to prevent excessive calls.

**API Priority and Fairness**

Kubernetes introduced the concept of API Priority and Fairness (APF) to prioritize and manage API requests. You can use APF in Kubernetes to protect the cluster's API server and reduce the number of `HTTP 429 Too Many Requests`

responses seen by client applications.

| Custom resource | Key features |
|---|---|
| PriorityLevelConfigurations | * Define different priority levels for API requests. * Specifies a unique name and assigns an integer value representing the priority level. Higher priority levels have lower integer values, indicating they're more critical. * Can use multiple to categorize requests into different priority levels based on their importance. * Allow you to specify whether requests at a particular priority level should be subject to rate limits. |
| FlowSchemas | * Define how API requests should be routed to different priority levels based on request attributes. * Specify rules that match requests based on criteria like API groups, versions, and resources. * When a request matches a given rule, the request is directed to the priority level specified in the associated PriorityLevelConfiguration. * Can use to set the order of evaluation when multiple FlowSchemas match a request to ensure that certain rules take precedence. |

Configuring API with PriorityLevelConfigurations and FlowSchemas enables the prioritization of critical API requests over less important requests. This ensures that essential operations don't starve or experience delays because of lower priority requests.

**Optimize labeling and selectors**

When using LIST operations, optimize label selectors to narrow down the scope of the resources you want to query to reduce the amount of data returned and the load on the API server.

In Kubernetes CREATE and UPDATE operations refer to actions that manage and modify cluster resources.

### CREATE and UPDATE operations

**The CREATE operation creates new resources in the Kubernetes cluster**, such as pods, services, deployments, configmaps, and secrets. During a CREATE operation, a client, such as `kubectl`

or a controller, sends a request to the Kubernetes API server to create the new resource. The API server validates the request, ensures compliance with any admission controller policies, and then creates the resource in the cluster's desired state.

**The UPDATE operation modifies existing resources in the Kubernetes cluster**, including changes to resources specifications, like number of replicas, container images, environment variables, or labels. During an UPDATE operation, a client sends a request to the API server to update an existing resource. The API server validates the request, applies the changes to the resource definition, and updates the cluster resource.

CREATE and UPDATE operations can impact the performance of the Kubernetes API server under the following conditions:

**High concurrency**: When multiple users or applications make concurrent CREATE or UPDATE requests, it can lead to a surge in API requests arriving at the server at the same time. This can stress the API server's processing capacity and cause performance issues.**Complex resource definitions**: Resource definitions that are overly complex or involve multiple nested objects can increase the time it takes for the API server to validate and process CREATE and UPDATE requests, which can lead to performance degradation.**Resource validation and admission control**: Kubernetes enforces various admission control policies and validation checks on incoming CREATE and UPDATE requests. Large resource definitions, like ones with extensive annotations or configurations, might require more processing time.**Custom controllers**: Custom controllers that watch for changes in resources, like Deployments or StatefulSet controllers, can generate a significant number of updates when scaling or rolling out changes. These updates can strain the API server's resources.

For more information, see [Troubleshoot API server and etcd problems in AKS](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-apiserver-etcd).

## Data plane performance

The Kubernetes data plane is responsible for managing network traffic between containers and services. Issues with the data plane can lead to slow response times, degraded performance, and application downtime. It's important to carefully monitor and optimize data plane configurations, such as network latency, resource allocation, container density, and network policies, to ensure your containerized applications run smoothly and efficiently.

### Storage types

AKS recommends and defaults to using ephemeral OS disks. Ephemeral OS disks are created on local VM storage and aren't saved to remote Azure storage like managed OS disks. They have faster reimaging and boot times, enabling faster cluster operations, and they provide lower read/write latency on the OS disk of AKS agent nodes. Ephemeral OS disks work well for stateless workloads, where applications are tolerant of individual VM failures but not of VM deployment time or individual VM reimaging instances. Only certain VM SKUs support ephemeral OS disks, so you need to ensure that your desired SKU generation and size is compatible. For more information, see [Ephemeral OS disks in Azure Kubernetes Service (AKS)](cluster-configuration#use-ephemeral-os-on-new-clusters).

If your workload is unable to use ephemeral OS disks, AKS defaults to using Premium SSD OS disks. If Premium SSD OS disks aren't compatible with your workload, AKS defaults to Standard SSD disks. Currently, the only other available OS disk type is Standard HDD. For more information, see [Storage options in Azure Kubernetes Service (AKS)](concepts-storage).

The following table provides a breakdown of suggested use cases for OS disks supported in AKS:

| OS disk type | Key features | Suggested use cases |
|---|---|---|
| Ephemeral OS disks | * Faster reimaging and boot times. * Lower read/write latency on OS disk of AKS agent nodes. * High performance and availability. |
* Demanding enterprise workloads, such as SQL Server, Oracle, Dynamics, Exchange Server, MySQL, Cassandra, MongoDB, SAP Business Suite, etc. * Stateless production workloads that require high availability and low latency. |
| Premium SSD OS disks | * Consistent performance and low latency. * High availability. |
* Demanding enterprise workloads, such as SQL Server, Oracle, Dynamics, Exchange Server, MySQL, Cassandra, MongoDB, SAP Business Suite, etc. * Input/output (IO) intensive enterprise workloads. |
| Standard SSD OS disks | * Consistent performance. * Better availability and latency compared to Standard HDD disks. |
* Web servers. * Low input/output operations per second (IOPS) application servers. * Lightly used enterprise applications. * Dev/test workloads. |
| Standard HDD disks | * Low cost. * Exhibits variability in performance and latency. |
* Backup storage. * Mass storage with infrequent access. |

#### IOPS and throughput

Input/output operations per second (IOPS) refers to the number of read and write operations that a disk can perform in a second. Throughput refers to the amount of data that can be transferred in a given time period.

OS disks are responsible for storing the operating system and its associated files, and the VMs are responsible for running the applications. When selecting a VM, ensure the size and performance of the OS disk and VM SKU don't have a large discrepancy. A discrepancy in size or performance can cause performance issues and resource contention. For example, if the OS disk is significantly smaller than the VMs, it can limit the amount of space available for application data and cause the system to run out of disk space. If the OS disk has lower performance than the VMs, it can become a bottleneck and limit the overall performance of the system. Make sure the size and performance are balanced to ensure optimal performance in Kubernetes.

You can use the following steps to monitor IOPS and bandwidth meters on OS disks in the Azure portal:

- Navigate to the
[Azure portal](https://portal.azure.com/). - Search for
**Virtual machine scale sets**and select your virtual machine scale set. - Under
**Monitoring**, select**Metrics**.

Ephemeral OS disks can provide dynamic IOPS and throughput for your application, whereas managed disks have capped IOPS and throughput. For more information, see [Ephemeral OS disks for Azure VMs](/en-us/azure/virtual-machines/ephemeral-os-disks).

[Azure Premium SSD v2](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2) is designed for IO-intense enterprise workloads that require sub-millisecond disk latencies and high IOPS and throughput at a low cost. It's suited for a broad range of workloads, such as SQL server, Oracle, MariaDB, SAP, Cassandra, MongoDB, big data/analytics, gaming, and more. This disk type is the highest performing option currently available for persistent volumes.

### Pod scheduling

The memory and CPU resources allocated to a VM have a direct impact on the performance of the pods running on the VM. When a pod is created, it's assigned a certain amount of memory and CPU resources, which are used to run the application. If the VM doesn't have enough memory or CPU resources available, it can cause the pods to slow down or even crash. If the VM has too much memory or CPU resources available, it can cause the pods to run inefficiently, wasting resources and increasing costs. We recommend monitoring the total pod requests across your workloads against the total allocatable resources for best scheduling predictability and performance. You can also set the maximum pods per node based on your capacity planning using `--max-pods`

.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-metrics-server-vertical-pod-autoscaler -->

# Configure Metrics Server VPA in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Metrics Server](https://kubernetes-sigs.github.io/metrics-server/) is a scalable, efficient source of container resource metrics for Kubernetes built-in autoscaling pipelines. With Azure Kubernetes Service (AKS), vertical pod autoscaling is enabled for the Metrics Server. The Metrics Server is commonly used by other Kubernetes add-ons, like the [Horizontal Pod Autoscaler](concepts-scale#horizontal-pod-autoscaler).

Vertical Pod Autoscaler (VPA) enables you to adjust the resource limit when the Metrics Server is experiencing consistent CPU and memory resource constraints.

## Prerequisites

- An AKS cluster with Kubernetes version 1.24 or higher.
- The Kubernetes command-line tool
`kubectl`

installed on your computer or use Azure Cloud Shell to run`kubectl`

commands.

## Get credentials

To run the `kubectl`

commands, you need your AKS credentials merged into your profile's `.kube/config`

file. Replace `<resourceGroupName>`

and `<clusterName>`

with your cluster's values.

```
az aks get-credentials --resource-group <resourceGroupName> --name <clusterName>
```


## Metrics server throttling

If the Metrics Server throttling rate is high, and the memory usage of its two pods is unbalanced, it's an indication that the Metrics Server needs more resources than the default values.

To update the coefficient values, create a `ConfigMap`

in the overlay `kube-system`

namespace to override the values in the Metrics Server specification. Perform the following steps to update the metrics server.

Create a

`ConfigMap`

file named*metrics-server-config.yaml*and copy the manifest code into the file.`apiVersion: v1 kind: ConfigMap metadata: name: metrics-server-config namespace: kube-system labels: kubernetes.io/cluster-service: "true" addonmanager.kubernetes.io/mode: EnsureExists data: NannyConfiguration: |- apiVersion: nannyconfig/v1alpha1 kind: NannyConfiguration baseCPU: 100m cpuPerNode: 1m baseMemory: 100Mi memoryPerNode: 8Mi`

In the

`ConfigMap`

example, the resource limit and request are changed to the following values where`n`

is the number of nodes:- cpu: (100+1n) millicores
- memory: (100+8n) mebibytes

If you're using Cloud Shell, use

**Manage files**and select**Upload**so the file is available in your Bash session.Create the

`ConfigMap`

using the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest:`kubectl apply -f metrics-server-config.yaml`

Restart the two Metrics Server pods using

[kubectl rollout restart](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#rollout). The following command deletes both pods and new pods are created.`kubectl rollout restart -n kube-system deployment metrics-server`

The new Metrics Server pods are created before the old pods are terminated so there isn't downtime.

List the pods using

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)to get the new Metrics Server pod names that are used in the next command.`kubectl get pods --namespace kube-system`

`NAME READY STATUS RESTARTS AGE metrics-server-1a2b333c44-wxyz5 2/2 Running 0 15s metrics-server-1a2b333c44-abcd6 2/2 Running 0 15s`

If you notice a third Metrics Server pod with a longer age value, it's because the termination occurs after the new pods are available.

To verify the updated resources took effect for each pod, run the following command to review the Metrics Server VPA log. Replace

`<metrics-server-pod-name>`

with the name of each of your metrics server pods.`kubectl -n kube-system logs <metrics-server-pod-name> -c metrics-server-vpa`

The following example output resembles the results showing the updated throttling settings were applied.

`I0811 19:08:34.930865 1 pod_nanny.go:86] Invoked by [/pod_nanny --config-dir=/etc/config --cpu=150m --extra-cpu=0.5m --memory=100Mi --extra-memory=4Mi --poll-period=180000 --threshold=5 --deployment=metrics-server --container=metrics-server] I0811 19:08:34.931128 1 pod_nanny.go:87] Version: 1.8.23 I0811 19:08:34.931200 1 pod_nanny.go:109] Watching namespace: kube-system, pod: <metrics-server-pod-name>, container: metrics-server. I0811 19:08:34.931249 1 pod_nanny.go:110] storage: MISSING, extra_storage: 0Gi I0811 19:08:34.932085 1 pod_nanny.go:144] cpu: 100m, extra_cpu: 1m, memory: 100Mi, extra_memory: 8Mi I0811 19:08:34.932177 1 pod_nanny.go:278] Resources: [{Base:{i:{value:100 scale:-3} d:{Dec:<nil>} s:100m Format:DecimalSI} ExtraPerResource:{i:{value:1 scale:-3} d:{Dec:<nil>} s:1m Format:DecimalSI} Name:cpu} {Base:{i:{value:104857600 scale:0} d:{Dec:<nil>} s:100Mi Format:BinarySI} ExtraPerResource:{i:{value:8388608 scale:0} d:{Dec:<nil>} s: Format:BinarySI} Name:memory}]`


Be cautious of the `baseCPU`

, `cpuPerNode`

, `baseMemory`

, and the `memoryPerNode`

, because AKS doesn't validate the `ConfigMap`

. As a recommended practice, increase the value gradually to avoid unnecessary resource consumption. Proactively monitor resource usage when updating or creating the `ConfigMap`

. A large number of resource requests could negatively affect the node.

## Manually configure Metrics Server resource usage

The Metrics Server VPA adjusts resource usage by the number of nodes. If the cluster scales up or down often, the Metrics Server might restart frequently. In this case, you can bypass VPA and manually control its resource usage. This method to configure VPA isn't to be performed in addition to the steps described in the previous section.

If you would like to bypass VPA for Metrics Server and manually control its resource usage, perform the following steps.

Create a

`ConfigMap`

file named*metrics-server-config.yaml*and copy in the following manifest.`apiVersion: v1 kind: ConfigMap metadata: name: metrics-server-config namespace: kube-system labels: kubernetes.io/cluster-service: "true" addonmanager.kubernetes.io/mode: EnsureExists data: NannyConfiguration: |- apiVersion: nannyconfig/v1alpha1 kind: NannyConfiguration baseCPU: 100m cpuPerNode: 0m baseMemory: 100Mi memoryPerNode: 0Mi`

In this

`ConfigMap`

example, the resource limit and request are changed to the following values that don't trigger autoscaling:- cpu: 100 millicores
- memory: 100 mebibytes

If you're using Cloud Shell, use

**Manage files**and select**Upload**so the file is available in your Bash session.Create the

`ConfigMap`

using the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest:`kubectl apply -f metrics-server-config.yaml`

Restart the two Metrics Server pods using

[kubectl rollout restart](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#rollout). The following command deletes both pods and new pods are created.`kubectl rollout restart -n kube-system deployment metrics-server`

The new Metrics Server pods are created before the old pods are terminated so there isn't downtime.

List the pods using

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)to get the new Metrics Server pod names that are used in the next command.`kubectl get pods --namespace kube-system`

`NAME READY STATUS RESTARTS AGE metrics-server-1a2b333c44-wxyz5 2/2 Running 0 15s metrics-server-1a2b333c44-abcd6 2/2 Running 0 15s`

If you notice a third Metrics Server pod with a longer age value, it's because the termination occurs after the new pods are available.

To verify the updated resources took effect for each pod, run the following command to review the Metrics Server VPA log. Replace

`<metrics-server-pod-name>`

with the name of each of your metrics server pods.`kubectl -n kube-system logs <metrics-server-pod-name> -c metrics-server-vpa`

The following example output resembles the results showing the updated throttling settings were applied.

`I0811 19:19:06.235018 1 pod_nanny.go:86] Invoked by [/pod_nanny --config-dir=/etc/config --cpu=150m --extra-cpu=0.5m --memory=100Mi --extra-memory=4Mi --poll-period=180000 --threshold=5 --deployment=metrics-server --container=metrics-server] I0811 19:19:06.235105 1 pod_nanny.go:87] Version: 1.8.23 I0811 19:19:06.235136 1 pod_nanny.go:109] Watching namespace: kube-system, pod: <metrics-server-pod-name>, container: metrics-server. I0811 19:19:06.235171 1 pod_nanny.go:110] storage: MISSING, extra_storage: 0Gi I0811 19:19:06.235899 1 pod_nanny.go:144] cpu: 100m, extra_cpu: 0m, memory: 100Mi, extra_memory: 0Mi I0811 19:19:06.235917 1 pod_nanny.go:278] Resources: [{Base:{i:{value:100 scale:-3} d:{Dec:<nil>} s:100m Format:DecimalSI} ExtraPerResource:{i:{value:0 scale:-3} d:{Dec:<nil>} s: Format:DecimalSI} Name:cpu} {Base:{i:{value:104857600 scale:0} d:{Dec:<nil>} s:100Mi Format:BinarySI} ExtraPerResource:{i:{value:0 scale:0} d:{Dec:<nil>} s: Format:BinarySI} Name:memory}]`


## Troubleshooting

### ConfigMap error

If you apply the following `ConfigMap`

, the Metrics Server VPA customizations aren't applied. You need add a unit for `baseCPU`

like `baseCPU: 100m`

that includes the `m`

unit.

```
apiVersion: v1
kind: ConfigMap
metadata:
name: metrics-server-config
namespace: kube-system
labels:
kubernetes.io/cluster-service: "true"
addonmanager.kubernetes.io/mode: EnsureExists
data:
NannyConfiguration: |-
apiVersion: nannyconfig/v1alpha1
kind: NannyConfiguration
baseCPU: 100
cpuPerNode: 1m
baseMemory: 100Mi
memoryPerNode: 8Mi
```


The following example output resembles the results showing the updated throttling settings aren't applied.

```
I0811 19:25:33.992691 1 pod_nanny.go:86] Invoked by [/pod_nanny --config-dir=/etc/config --cpu=150m --extra-cpu=0.5m --memory=100Mi --extra-memory=4Mi --poll-period=180000 --threshold=5 --deployment=metrics-server --container=metrics-server]
I0811 19:25:33.992890 1 pod_nanny.go:87] Version: 1.8.23
I0811 19:25:33.992918 1 pod_nanny.go:109] Watching namespace: kube-system, pod: <metrics-server-pod-name>, container: metrics-server.
I0811 19:25:33.992937 1 pod_nanny.go:110] storage: MISSING, extra_storage: 0Gi
I0811 19:25:33.993586 1 pod_nanny.go:217] Unable to decode Nanny Configuration from config map, using default parameters
I0811 19:25:33.993602 1 pod_nanny.go:144] cpu: 150m, extra_cpu: 0.5m, memory: 100Mi, extra_memory: 4Mi
I0811 19:25:33.993610 1 pod_nanny.go:278] Resources: [{Base:{i:{value:150 scale:-3} d:{Dec:<nil>} s:150m Format:DecimalSI} ExtraPerResource:{i:{value:5 scale:-4} d:{Dec:<nil>} s: Format:DecimalSI} Name:cpu} {Base:{i:{value:104857600 scale:0} d:{Dec:<nil>} s:100Mi Format:BinarySI} ExtraPerResource:{i:{value:4194304 scale:0} d:{Dec:<nil>} s:4Mi Format:BinarySI} Name:memory}]
```


### PodDisruptionBudget

For Kubernetes version 1.23 and higher clusters, Metrics Server has a `PodDisruptionBudget`

. It ensures the number of available Metrics Server pods is at least one. If you get something like this after running `kubectl get pods --namespace kube-system`

, it's possible that the customized resource usage is small. Increase the coefficient values to resolve it.

```
metrics-server-1a2b333c44-wxyz5 1/2 CrashLoopBackOff 6 (36s ago) 6m33s
metrics-server-1a2b333c44-abcd6 1/2 CrashLoopBackOff 6 (54s ago) 6m33s
metrics-server-5d69966543-hcrff 2/2 Running 0 37m
```


## Next steps

Metrics Server is a component in the core metrics pipeline. For more information, see [Metrics Server API design](https://kubernetes.io/docs/tasks/debug/debug-cluster/resource-metrics-pipeline/).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr-workflow -->

# Deploy and run workflows with the Dapr extension for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

With Dapr Workflow, you can easily orchestrate messaging, state management, and failure-handling logic across various microservices. Dapr Workflow can help you create long-running, fault-tolerant, and stateful applications.

In this guide, you use the [provided order processing workflow example](https://github.com/Azure-Samples/dapr-workflows-aks-sample) to:

- Create an Azure Container Registry and an AKS cluster for this sample.
- Install the Dapr extension on your AKS cluster.
- Deploy the sample application to AKS.
- Start and query workflow instances using HTTP API calls.

The workflow example is an ASP.NET Core project with:

- A
that contains the setup of the app, including the registration of the workflow and workflow activities.`Program.cs`

file - Workflow definitions found in the
.`Workflows`

directory - Workflow activity definitions found in the
.`Activities`

directory

## Prerequisites

- An
[Azure subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)with Owner or Admin role. [An Azure Kubernetes Service Role-Based Access Control Admin role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-rbac-admin)- The latest version of the
[Azure CLI](/en-us/cli/azure/install-azure-cli) - The latest version of
[Dapr](https://docs.dapr.io/getting-started/install-dapr-cli/) - Latest
[Docker](https://docs.docker.com/get-docker/) - Latest
[Helm](https://helm.sh/docs/intro/install/)

## Set up the environment

### Clone the sample project

Clone the example workflow application.

```
git clone https://github.com/Azure-Samples/dapr-workflows-aks-sample.git
```


Navigate to the sample's root directory.

```
cd dapr-workflows-aks-sample
```


### Create a Kubernetes cluster

Create a resource group to hold the AKS cluster.

```
az group create --name myResourceGroup --location eastus
```


Create an AKS cluster.

```
az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 2 --generate-ssh-keys
```


[Make sure kubectl is installed and pointed to your AKS cluster.](tutorial-kubernetes-deploy-cluster#connect-to-cluster-using-kubectl) If you use the Azure Cloud Shell,

`kubectl`

is already installed.For more information, see the [Deploy an AKS cluster](tutorial-kubernetes-deploy-cluster) tutorial.

## Deploy the application to AKS

### Install Dapr on your AKS cluster

Install the Dapr extension on your AKS cluster. Before you start, make sure you have:

[Installed or updated the](dapr#add-the-azure-cli-extension-for-cluster-extensions).`k8s-extension`

[Registered the](dapr#register-the-kubernetesconfiguration-resource-provider)`Microsoft.KubernetesConfiguration`

service provider

```
az k8s-extension create --cluster-type managedClusters --cluster-name myAKSCluster --resource-group myResourceGroup --name dapr --extension-type Microsoft.Dapr
```


After a few minutes, you'll see output showing the Dapr connection to your AKS cluster. Next, initialize Dapr on your cluster.

```
dapr init -k
```


Verify Dapr is installed:

```
kubectl get pods -A
```


### Deploy the Redis Actor state store component

Navigate to the `Deploy`

directory in your forked version of the sample:

```
cd Deploy
```


Deploy the Redis component:

```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install redis bitnami/redis
kubectl apply -f redis.yaml
```


### Run the application

Once Redis is deployed, deploy the application to AKS:

```
kubectl apply -f deployment.yaml
```


Expose the Dapr sidecar and the sample app:

```
kubectl apply -f service.yaml
export APP_URL=$(kubectl get svc/workflows-sample -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export DAPR_URL=$(kubectl get svc/workflows-sample-dapr -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
```


Verify that the above commands were exported:

```
echo $APP_URL
echo $DAPR_URL
```


## Start the workflow

Now that the application and Dapr are deployed to the AKS cluster, you can now start and query workflow instances. Restock items in the inventory using the following API call to the sample app:

```
curl -X GET $APP_URL/stock/restock
```


Start the workflow:

```
curl -i -X POST $DAPR_URL/v1.0/workflows/dapr/OrderProcessingWorkflow/start \
-H "Content-Type: application/json" \
-H "dapr-app-id: dwf-app" \
-d '{"Name": "Paperclips", "TotalCost": 99.95, "Quantity": 1}'
```


Expected output includes an auto-generated instance ID:

```
HTTP/1.1 202 Accepted
Content-Type: application/json
Traceparent: 00-00000000000000000000000000000000-0000000000000000-00
Date: Tue, 23 Apr 2024 15:35:00 GMT
Content-Length: 21
{"instanceID":"<generated-id>"}
```


Check the workflow status:

```
curl -i -X GET $DAPR_URL/v1.0/workflows/dapr/OrderProcessingWorkflow/<instance-id> \
-H "dapr-app-id: dwf-app"
```


Expected output:

```
HTTP/1.1 200 OK
Content-Type: application/json
Traceparent: 00-00000000000000000000000000000000-0000000000000000-00
Date: Tue, 23 Apr 2024 15:51:02 GMT
Content-Length: 580
```


Monitor the application logs:

```
kubectl logs -l run=workflows-sample -c workflows-sample --tail=20
```


Expected output:

```
{
"instanceID":"1234",
"workflowName":"OrderProcessingWorkflow",
"createdAt":"2024-04-23T15:35:00.156714334Z",
"lastUpdatedAt":"2024-04-23T15:35:00.176459055Z",
"runtimeStatus":"COMPLETED",
"dapr.workflow.input":"{ \"input\" : {\"Name\": \"Paperclips\", \"TotalCost\": 99.95, \"Quantity\": 1}}",
"dapr.workflow.output":"{\"Processed\":true}"
}
```


Notice that the workflow status is marked as completed.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-capacity-reservation-groups -->

# Assign capacity reservation groups to Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As your workload demands change, you can associate existing [capacity reservation groups (CRGs)](/en-us/azure/virtual-machines/capacity-reservation-associate-virtual-machine-scale-set) to your Azure Kubernetes Service (AKS) node pools to guarantee allocated capacity for them. Capacity reservation groups allow you to reserve compute capacity in an Azure region or availability zone for any duration of time. This feature is useful for workloads that require guaranteed capacity, such as those with predictable traffic patterns or those that need to meet specific performance requirements.

In this article, you learn how to use capacity reservation groups with node pools in AKS.

Note

Deleting a node pool implicitly dissociates that node pool from any associated capacity reservation group before the node pool is deleted. Deleting a cluster implicitly dissociates all node pools in that cluster from their associated capacity reservation groups.

## Prerequisites for using capacity reservation groups with AKS node pools

- You need the Azure CLI version 2.56 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need an existing
[capacity reservation group](/en-us/azure/virtual-machines/capacity-reservation-associate-virtual-machine-scale-set)with at least one capacity reservation. If not, the node pool is added to the cluster with a warning and no capacity reservation group gets associated. - You need to
[create a user-assigned managed identity with the](#create-a-user-assigned-managed-identity-and-assign-it-to-an-aks-cluster)for the resource group that contains the capacity reservation group and assign the identity to your AKS cluster. System-assigned managed identities don't work for this feature.`Contributor`

role

### Create a user-assigned managed identity and assign it to an AKS cluster

Create a user-assigned managed identity using the

command.`az identity create`

`az identity create --name <identity-name> --resource-group <resource-group-name> --location <location>`

Get the ID of the user-assigned managed identity using the

command and set it to an environment variable.`az identity show`

`IDENTITY_ID=$(az identity show --name <identity-name> --resource-group <resource-group-name> --query identity.id -o tsv)`

Assign the

`Contributor`

role to the user-assigned identity using thecommand.`az role assignment create`

`az role assignment create --assignee $IDENTITY_ID --role "Contributor" --scope /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>`

It can take up to

*60 minutes*for the role assignment to propagate.Assign the user-assigned managed identity to a new or existing AKS cluster using the

`--assign-identity`

flag with theor`az aks create`

command.`az aks update`

`# Create a new AKS cluster with the user-assigned managed identity az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> --node-count <node-count> \ --assign-identity $IDENTITY_ID \ --generate-ssh-keys # Update an existing AKS cluster to use the user-assigned managed identity az aks update \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> \ --node-count <node-count> \ --enable-managed-identity \ --assign-identity $IDENTITY_ID`


## Limitations for using capacity reservation groups with AKS node pools

You can't update an existing node pool with a capacity reservation group. Instead, you need to create a new node pool with the `--crg-id`

flag to associate it with the capacity reservation group. You can also associate an existing capacity reservation group with a system node pool during cluster creation.

## Get the ID of an existing capacity reservation group

Get the ID of an existing capacity reservation group using the

command and set it to an environment variable.`az capacity reservation group show`

`CRG_ID=$(az capacity reservation group show --capacity-reservation-group <crg-name> --resource-group <resource-group-name> --query id -o tsv)`


## Associate an existing capacity reservation group with a node pool

Associate an existing capacity reservation group with a node pool using the

command with the`az aks nodepool add`

`--crg-id`

flag. The following example assumes you have a CRG named "myCRG".`az aks nodepool add --resource-group <resource-group-name> --cluster-name <cluster-name> --name <node-pool-name> --crg-id $CRG_ID`


## Associate an existing capacity reservation group with a system node pool

To associate an existing capacity reservation group with a system node pool, you need to assign the user-assigned managed identity with the `Contributor`

role to the cluster during cluster creation. You can then use the `--crg-id`

flag to associate the capacity reservation group with the system node pool.

Create a new AKS cluster with the user-assigned managed identity and associate it with the capacity reservation group using the

`--assign-identity`

and`--crg-id`

flags with thecommand.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> --node-count <node-count> \ --assign-identity $IDENTITY_ID \ --crg-id $CRG_ID \ --generate-ssh-keys`


## Next steps: Manage node pools in AKS

To learn more about managing node pools in AKS, see [Manage node pools in Azure Kubernetes Service (AKS)](manage-node-pools).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-cni-overlay -->

# Configure Azure CNI Overlay networking in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains the setup process, dual-stack networking configuration, and an example workload deployment for Azure CNI Overlay in Azure Kubernetes Service (AKS) clusters. For an overview of Azure CNI Overlay networking, see [Overview of Azure CNI Overlay networking in Azure Kubernetes Service (AKS)](concepts-network-azure-cni-overlay).

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/free/)before you begin. - Azure CLI version 2.48.0 or later. To install or upgrade the Azure CLI, see
[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). - An existing Azure resource group. If you need to create one, see
[Create resource groups](/en-us/azure/azure-resource-manager/management/manage-resource-groups-cli#create-resource-groups).

For dual-stack networking, you need Kubernetes version 1.26.3 or later.

## Key parameters for Azure CNI Overlay AKS clusters

The following table describes the key parameters for configuring Azure CNI Overlay networking in AKS clusters:

| Parameter | Description |
|---|---|
`--network-plugin` |
Set to `azure` to use Azure Container Networking Interface (CNI) networking. |
`--network-plugin-mode` |
Set to `overlay` to enable Azure CNI Overlay networking. This setting applies only when `--network-plugin=azure` . |
`--pod-cidr` |
Specify a custom pod Classless Inter-Domain Routing (CIDR) block for the cluster. The default is `10.244.0.0/16` . |

The default behavior for network plugins depends on whether you explicitly set `--network-plugin`

:

- If you don't specify
`--network-plugin`

, AKS defaults to Azure CNI Overlay. - If you specify
`--network-plugin=azure`

and omit`--network-plugin-mode`

, AKS intentionally uses virtual network (node subnet) mode for backward compatibility.

## Create an Azure CNI Overlay AKS cluster

Create an Azure CNI Overlay AKS cluster by using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command with

`--network-plugin=azure`

and `--network-plugin-mode=overlay`

. If you don't specify a value for `--pod-cidr`

, AKS assigns the default value of `10.244.0.0/16`

.```
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--location $REGION \
--network-plugin azure \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16 \
--generate-ssh-keys
```


## Add a new node pool to a dedicated subnet

Add a node pool to a different subnet within the same virtual network to control virtual machine (VM) node IP addresses for network traffic to virtual network or peered virtual network resources.

Add a new node pool to the cluster by using the [ az aks nodepool add](/en-us/cli/azure/aks#az_aks_nodepool_add) command and specify the subnet resource ID with the

`--vnet-subnet-id`

parameter. For example:```
az aks nodepool add \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--name $NODE_POOL_NAME \
--node-count 1 \
--mode system \
--vnet-subnet-id $SUBNET_RESOURCE_ID
```


## About Azure CNI Overlay AKS clusters with dual-stack networking

You can deploy your Azure CNI Overlay AKS clusters in a dual-stack mode with an Azure virtual network. In this configuration, nodes receive both an IPv4 and IPv6 address from the Azure virtual network subnet. Pods receive an IPv4 and IPv6 address from a different address space to the Azure virtual network subnet of the nodes. Network address translation (NAT) is then configured so that the pods can reach resources on the Azure virtual network. The source IP address of the traffic is NAT'd to the node's primary IP address of the same family (*IPv4 to IPv4* and *IPv6 to IPv6*).

Note

You can also deploy dual-stack networking clusters by using Azure CNI Powered by Cilium. For more information, see [Dual-stack networking with Azure CNI Powered by Cilium](azure-cni-powered-by-cilium#dual-stack-networking-with-azure-cni-powered-by-cilium).

## Dual-stack networking limitations

The following features aren't supported with dual-stack networking:

## Key parameters for dual-stack networking

The following table describes the key parameters for configuring dual-stack networking in Azure CNI Overlay AKS clusters:

| Parameter | Description |
|---|---|
`--ip-families` |
Takes a comma-separated list of IP families to enable on the cluster. Only `ipv4` and `ipv4,ipv6` are supported. |
`--pod-cidrs` |
Takes a comma-separated list of Classless Inter-Domain Routing (CIDR) notation IP ranges to assign pod IPs from. The count and order of ranges in this list must match the value provided to `--ip-families` . If you don't supply any values, the parameter uses the default value of `10.244.0.0/16,fd12:3456:789a::/64` . |
`--service-cidrs` |
Takes a comma-separated list of CIDR notation IP ranges to assign service IPs from. The count and order of ranges in this list must match the value provided to `--ip-families` . If you don't supply any values, the parameter uses the default value of `10.0.0.0/16,fd12:3456:789a:1::/108` . The IPv6 subnet assigned to `--service-cidrs` can be no larger than `/108` . |

## Create an Azure CNI Overlay AKS cluster with dual-stack networking (Linux)

Create an Azure resource group for the cluster by using the

command:`az group create`

`az group create --location $REGION --name $RESOURCE_GROUP`

Create a dual-stack AKS cluster by using the

command with the`az aks create`

`--ip-families`

parameter set to`ipv4,ipv6`

:`az aks create \ --location $REGION \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --network-plugin azure \ --network-plugin-mode overlay \ --ip-families ipv4,ipv6 \ --generate-ssh-keys`


## Create an Azure CNI Overlay AKS cluster with dual-stack networking (Windows)

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Before you create an Azure CNI Overlay AKS cluster with dual-stack networking with Windows node pools, you need to install the `aks-preview`

Azure CLI extension and register the `AzureOverlayDualStackPreview`

feature flag in your subscription.

### Install the `aks-preview`

Azure CLI extension

Install the

`aks-preview`

extension by using thecommand:`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the extension by using the

command:`az extension update`

`az extension update --name aks-preview`


### Register the `AzureOverlayDualStackPreview`

feature flag

Register the

`AzureOverlayDualStackPreview`

feature flag by using thecommand:`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AzureOverlayDualStackPreview"`

It takes a few minutes for the status to show

`Registered`

.Verify the registration status by using the

command:`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "AzureOverlayDualStackPreview"`

When the status reflects

`Registered`

, refresh the registration of the`Microsoft.ContainerService`

resource provider by using thecommand:`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create a dual-stack Azure CNI Overlay AKS cluster and add a Windows node pool

Create a cluster with Azure CNI Overlay by using the

command:`az aks create`

`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --location $REGION \ --network-plugin azure \ --network-plugin-mode overlay \ --ip-families ipv4,ipv6 \ --generate-ssh-keys`

Add a Windows node pool to the cluster by using the

command:`az aks nodepool add`

`az aks nodepool add \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --os-type Windows \ --name $WINDOWS_NODE_POOL_NAME \ --node-count 2`


## Deploy an example workload to the Azure CNI Overlay AKS cluster

Deploy dual-stack AKS CNI Overlay clusters with IPv4/IPv6 addresses on virtual machine nodes. This example deploys an NGINX web server and exposes it by using a `LoadBalancer`

service with both IPv4 and IPv6 addresses.

Note

We recommend using the application routing add-on for ingress in AKS clusters. However, for demonstration purposes, this example deploys an NGINX web server without the application routing add-on. For more information about the add-on, see [Managed NGINX ingress with the application routing add-on](app-routing).

### Expose the workload by using a `LoadBalancer`

service

Expose the NGINX deployment by using either `kubectl`

commands or YAML manifests.

Important

There are currently *two limitations* that pertain to IPv6 services in AKS:

- Azure Load Balancer sends health probes to IPv6 destinations from a link-local address. In
*Azure Linux node pools*, you can't route this traffic to a pod, so traffic flowing to IPv6 services deployed with`externalTrafficPolicy: Cluster`

fails. - You must deploy IPv6 services with
`externalTrafficPolicy: Local`

, which causes`kube-proxy`

to respond to the probe on the node.

Expose the NGINX deployment by using the

`kubectl expose deployment nginx`

command:`kubectl expose deployment nginx --name=nginx-ipv4 --port=80 --type=LoadBalancer kubectl expose deployment nginx --name=nginx-ipv6 --port=80 --type=LoadBalancer --overrides='{"spec":{"ipFamilies": ["IPv6"]}}'`

Your output should show the exposed services. For example:

`service/nginx-ipv4 exposed service/nginx-ipv6 exposed`

After the deployment is exposed and the

`LoadBalancer`

services are fully provisioned, get the IP addresses of the services by using the`kubectl get services`

command:`kubectl get services`

Your output should show the services with their assigned IP addresses. For example:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE nginx-ipv4 LoadBalancer 10.0.88.78 20.46.24.24 80:30652/TCP 97s nginx-ipv6 LoadBalancer fd12:3456:789a:1::981a 2603:1030:8:5::2d 80:32002/TCP 63s`

Get the service IP by using the

`kubectl get services`

command and set it to an environment variable:`SERVICE_IP=$(kubectl get services nginx-ipv6 -o jsonpath='{.status.loadBalancer.ingress[0].ip}')`

Verify functionality by using a

`curl`

request from an IPv6-capable host. (*Azure Cloud Shell isn't IPv6 capable*.)`curl -s "http://[${SERVICE_IP}]" | head -n5`

Your output should show the HTML for the NGINX welcome page. For example:

`<!DOCTYPE html> <html> <head> <title>Welcome to nginx!</title> <style>`


## Related content

To learn more about Azure CNI Overlay networking on AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-marketplace -->

# Deploy and manage a Kubernetes application from Azure Marketplace

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy and manage a Kubernetes application from Azure Marketplace.

[Azure Marketplace](/en-us/marketplace/azure-marketplace-overview) is an online store that contains thousands of IT software applications and services built by industry-leading technology companies. In Azure Marketplace, you can find, try, buy, and deploy the software and services that you need to build new solutions and manage your cloud infrastructure. The catalog includes solutions for different industries and technical areas, free trials, and consulting services from Microsoft partners.

## Limitations

- This feature is currently supported only in the following regions:
- Australia East, Australia Southeast, Brazil South, Canada Central, Canada East, Central India, Central US, East Asia, East US, East US 2, East US 2 EAUP, France Central, France South, Germany North, Germany West Central, Japan East, Japan West, Jio India West, Korea Central, Korea South, North Central Us, North Europe, Norway East, Norway West, South Africa North, South Central US, South India, Southeast Asia, Sweden Central, Switzerland North, UAE North, UK South, UK West, West Central US, West Europe, West US, West US 2, West US 3

- You can't deploy Kubernetes application-based container offers on AKS for Azure Stack HCI or AKS Edge Essentials.

## Select and deploy a Kubernetes application

### From an AKS cluster

In the Azure portal, navigate to your AKS cluster resource.

From the service menu, under

**Settings**, select**Extensions + applications**>**Add**.You can search for an offer or publisher directly by name, or you can browse all offers. To view Kubernetes application offers, select

**Containers**under**Categories**.After you decide on an application, select the offer. The following example uses the

**TrilioVault for Kubernetes - BYOL**offer.Select

**Plans + Pricing**to ensure the terms are acceptable, and then select**Create**.Follow each page in the application creation process, filling in information for your resource group, your cluster, and any configuration options that the application requires. You can decide to deploy on a new AKS cluster or use an existing cluster.

Once you've filled in all the required information, select

**Review + create**>**Create**.It might take a few minutes for the application to deploy. You can monitor the deployment status from the

**Extensions + applications**page.

### Search in the Azure portal

From the Azure portal home page, search for and select

**Marketplace**.You can search for an offer or publisher directly by name, or you can browse all offers. To find Kubernetes application offers, on the left side under

**Categories**select**Containers**.After you decide on an application, select the offer. The following example uses the

**TrilioVault for Kubernetes - BYOL**offer.Select

**Plans + Pricing**to ensure the terms are acceptable, and then select**Create**.Follow each page in the application creation process, filling in information for your resource group, your cluster, and any configuration options that the application requires. You can decide to deploy on a new AKS cluster or use an existing cluster.

Once you've filled in all the required information, select

**Review + create**>**Create**.It might take a few minutes for the application to deploy. You can monitor the deployment status from the

**Extensions + applications**page.

## Verify the deployment

- Navigate to the cluster where you recently installed the application.
- From the service menu, under
**Settings**, select**Extensions + applications**. - Verify that the extension is listed and the
*Provisioning State*shows**Succeeded**.

## Manage the offer lifecycle

For lifecycle management, a Kubernetes offer is represented as a cluster extension for AKS. For more information, see [Cluster extensions for AKS](cluster-extensions). Purchasing an offer from Azure Marketplace creates a new instance of the extension on your AKS cluster.

- In the Azure portal, navigate to the cluster where you recently installed the application.
- From the service menu, under
**Settings**, select**Extensions + applications**. - Select an extension name to navigate to a properties view where you're able to disable autoupgrades, check the provisioning state, delete the extension instance, or modify configuration settings as needed.

## Monitor billing and usage information

- In the Azure portal, navigate to your cluster's resource group.
- From the service menu, under
**Cost Management**, select**Cost analysis**. Under**Product**, you can see a cost breakdown for the plan that you selected.

## Remove an offer

You can delete a purchased plan for an Azure container offer by deleting the extension instance on the cluster.

- Navigate to the cluster where you recently installed the application.
- From the service menu, under
**Settings**, select**Extensions + applications**. - Select an application, then select
**Uninstall**.

## Troubleshooting

If you experience issues, see the [troubleshooting checklist for failed deployments of a Kubernetes offer](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-failed-kubernetes-deployment-offer).

## Next steps

- Learn more about
[exploring and analyzing costs](/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis). - Learn more about
[deploying a Kubernetes application programmatically using Azure CLI](/en-us/azure/aks/deploy-application-az-cli). - Learn more about
[deploying a Kubernetes application using an ARM template](/en-us/azure/aks/deploy-application-template).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/quickstart-event-grid -->

# Quickstart: Subscribe to Azure Kubernetes Service (AKS) events with Azure Event Grid

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Event Grid is a fully managed event routing service that provides uniform event consumption using a publish-subscribe model.

In this quickstart, you create an AKS cluster and subscribe to AKS events.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). [Azure CLI](/en-us/cli/azure/install-azure-cli)or[Azure PowerShell](/en-us/powershell/azure/install-az-ps)installed.

Note

AKS operations are independent of Azure Event Grid availability and aren't impacted during Event Grid [Service Outages](https://azure.status.microsoft/status).

## Create an AKS cluster

Create an AKS cluster using the [az aks create](/en-us/cli/azure/aks#az-aks-create) command. The following example creates a resource group *MyResourceGroup* and a cluster named *MyAKS* with one node in the *MyResourceGroup* resource group:

```
az group create --name MyResourceGroup --location eastus
az aks create --resource-group yResourceGroup --name MyAKS --location eastus --node-count 1 --generate-ssh-keys
```


## Subscribe to AKS events

Create a namespace and event hub using [az eventhubs namespace create](/en-us/cli/azure/eventhubs/namespace#az-eventhubs-namespace-create) and [az eventhubs eventhub create](/en-us/cli/azure/eventhubs/eventhub#az-eventhubs-eventhub-create). The following example creates a namespace *MyNamespace* and an event hub *MyEventGridHub* in *MyNamespace*, both in the *MyResourceGroup* resource group.

```
az eventhubs namespace create --location eastus --name MyNamespace --resource-group MyResourceGroup
az eventhubs eventhub create --name MyEventGridHub --namespace-name MyNamespace --resource-group MyResourceGroup
```


Note

The *name* of your namespace must be unique.

Subscribe to the AKS events using [az eventgrid event-subscription create](/en-us/cli/azure/eventgrid/event-subscription#az-eventgrid-event-subscription-create):

```
SOURCE_RESOURCE_ID=$(az aks show --resource-group MyResourceGroup --name MyAKS --query id --output tsv)
ENDPOINT=$(az eventhubs eventhub show --resource-group MyResourceGroup --name MyEventGridHub --namespace-name MyNamespace --query id --output tsv)
az eventgrid event-subscription create --name MyEventGridSubscription \
--source-resource-id $SOURCE_RESOURCE_ID \
--endpoint-type eventhub \
--endpoint $ENDPOINT
```


Verify your subscription to AKS events using `az eventgrid event-subscription list`

:

```
az eventgrid event-subscription list --source-resource-id $SOURCE_RESOURCE_ID
```


The following example output shows you're subscribed to events from the *MyAKS* cluster and those events are delivered to the *MyEventGridHub* event hub:

```
[
{
"deadLetterDestination": null,
"deadLetterWithResourceIdentity": null,
"deliveryWithResourceIdentity": null,
"destination": {
"deliveryAttributeMappings": null,
"endpointType": "EventHub",
"resourceId": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/MyResourceGroup/providers/Microsoft.EventHub/namespaces/MyNamespace/eventhubs/MyEventGridHub"
},
"eventDeliverySchema": "EventGridSchema",
"expirationTimeUtc": null,
"filter": {
"advancedFilters": null,
"enableAdvancedFilteringOnArrays": null,
"includedEventTypes": [
"Microsoft.ContainerService.NewKubernetesVersionAvailable","Microsoft.ContainerService.ClusterSupportEnded","Microsoft.ContainerService.ClusterSupportEnding","Microsoft.ContainerService.NodePoolRollingFailed","Microsoft.ContainerService.NodePoolRollingStarted","Microsoft.ContainerService.NodePoolRollingSucceeded"
],
"isSubjectCaseSensitive": null,
"subjectBeginsWith": "",
"subjectEndsWith": ""
},
"id": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/MyResourceGroup/providers/Microsoft.ContainerService/managedClusters/MyAKS/providers/Microsoft.EventGrid/eventSubscriptions/MyEventGridSubscription",
"labels": null,
"name": "MyEventGridSubscription",
"provisioningState": "Succeeded",
"resourceGroup": "MyResourceGroup",
"retryPolicy": {
"eventTimeToLiveInMinutes": 1440,
"maxDeliveryAttempts": 30
},
"systemData": null,
"topic": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/MyResourceGroup/providers/microsoft.containerservice/managedclusters/MyAKS",
"type": "Microsoft.EventGrid/eventSubscriptions"
}
]
```


When AKS events occur, you see those events appear in your event hub. For example, when the list of available Kubernetes versions for your clusters changes, you see a `Microsoft.ContainerService.NewKubernetesVersionAvailable`

event. There are also new events available now for upgrades and cluster within support. For more information on the events AKS emits, see [Azure Kubernetes Service (AKS) as an Event Grid source](/en-us/azure/event-grid/event-schema-aks).

## Delete the cluster and subscriptions

Use the [az group delete](/en-us/cli/azure/group#az-group-delete) command to remove the resource group, the AKS cluster, namespace, and event hub, and all related resources.

```
az group delete --name MyResourceGroup --yes --no-wait
```


Note

When you delete the cluster, the Microsoft Entra service principal used by the AKS cluster isn't removed. For steps on how to remove the service principal, see [AKS service principal considerations and deletion](kubernetes-service-principal#considerations-when-using-a-service-principal).

If you used a managed identity, the identity is managed by the platform and doesn't require removal.

## Next steps

In this quickstart, you deployed a Kubernetes cluster and then subscribed to AKS events in Azure Event Hubs.

To learn more about AKS, and walk through a complete code to deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/spot-node-pool -->

# Add an Azure Spot node pool to an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you add a secondary Spot node pool to an existing Azure Kubernetes Service (AKS) cluster.

A Spot node pool is a node pool backed by an [Azure Spot Virtual Machine scale set](/en-us/azure/virtual-machine-scale-sets/use-spot). With Spot VMs in your AKS cluster, you can take advantage of unutilized Azure capacity with significant cost savings. The amount of available unutilized capacity varies based on many factors, such as node size, region, and time of day.

When you deploy a Spot node pool, Azure allocates the Spot nodes if there's capacity available and deploys a Spot scale set that backs the Spot node pool in a single default domain. There's no SLA for the Spot nodes. There are no high availability guarantees. If Azure needs capacity back, the Azure infrastructure evicts the Spot nodes.

Spot nodes are great for workloads that can handle interruptions, early terminations, or evictions. For example, workloads such as batch processing jobs, development and testing environments, and large compute workloads might be good candidates to schedule on a Spot node pool.

## Before you begin

- This article assumes a basic understanding of Kubernetes and Azure Load Balancer concepts. For more information, see
[Kubernetes core concepts for Azure Kubernetes Service (AKS)](concepts-clusters-workloads). - If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - When you create a cluster to use a Spot node pool, the cluster must use Virtual Machine Scale Sets for node pools and the
*Standard*SKU load balancer. You must also add another node pool after you create your cluster, which is covered in this tutorial. - This article requires that you're running the Azure CLI version 2.14 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Limitations

The following limitations apply when you create and manage AKS clusters with a Spot node pool:

- A Spot node pool can't be a default node pool, it can only be used as a secondary pool.
- You can't upgrade the control plane and node pools at the same time. You must upgrade them separately or remove the Spot node pool to upgrade the control plane and remaining node pools at the same time.
- A Spot node pool must use Virtual Machine Scale Sets.
- You can't change
`ScaleSetPriority`

or`SpotMaxPrice`

after creation. - When setting
`SpotMaxPrice`

, the value must be*-1*or a*positive value with up to five decimal places*. - A Spot node pool has the
`kubernetes.azure.com/scalesetpriority:spot`

label, the`kubernetes.azure.com/scalesetpriority=spot:NoSchedule`

taint, and the system pods have anti-affinity. - You must add a
[corresponding toleration](#verify-the-spot-node-pool)and affinity to schedule workloads on a Spot node pool.

## Add a Spot node pool to an AKS cluster

When adding a Spot node pool to an existing cluster, it must be a cluster with multiple node pools enabled. When you create an AKS cluster with multiple node pools enabled, you create a node pool with a `priority`

of `Regular`

by default. To add a Spot node pool, you must specify `Spot`

as the value for `priority`

. For more details on creating an AKS cluster with multiple node pools, see [use multiple node pools](create-node-pools).

- Create a node pool with a
`priority`

of`Spot`

using thecommand.`az aks nodepool add`


```
export SPOT_NODEPOOL="spotnodepool"
az aks nodepool add \
--resource-group $RESOURCE_GROUP \
--cluster-name $AKS_CLUSTER \
--name $SPOT_NODEPOOL \
--priority Spot \
--eviction-policy Delete \
--spot-max-price -1 \
--enable-cluster-autoscaler \
--min-count 1 \
--max-count 3 \
--no-wait
```


In the previous command, the `priority`

of `Spot`

makes the node pool a Spot node pool. The `eviction-policy`

parameter is set to `Delete`

, which is the default value. When you set the [eviction policy](/en-us/azure/virtual-machine-scale-sets/use-spot#eviction-policy) to `Delete`

, nodes in the underlying scale set of the node pool are deleted when they're evicted.

You can also set the eviction policy to `Deallocate`

, which means that the nodes in the underlying scale set are set to the *stopped-deallocated* state upon eviction. Nodes in the *stopped-deallocated* state count against your compute quota and can cause issues with cluster scaling or upgrading. The `priority`

and `eviction-policy`

values can only be set during node pool creation. Those values can't be updated later.

The previous command also enables the [cluster autoscaler](cluster-autoscaler), which we recommend using with Spot node pools. Based on the workloads running in your cluster, the cluster autoscaler scales the number of nodes up and down. For Spot node pools, the cluster autoscaler will scale up the number of nodes after an eviction if more nodes are still needed. If you change the maximum number of nodes a node pool can have, you also need to adjust the `maxCount`

value associated with the cluster autoscaler. If you don't use a cluster autoscaler, upon eviction, the Spot pool will eventually decrease to *0* and require manual operation to receive any additional Spot nodes.

Important

Only schedule workloads on Spot node pools that can handle interruptions, such as batch processing jobs and testing environments. We recommend you set up [taints and tolerations](operator-best-practices-advanced-scheduler#provide-dedicated-nodes-using-taints-and-tolerations) on your Spot node pool to ensure that only workloads that can handle node evictions are scheduled on a Spot node pool. For example, the above command adds a taint of `kubernetes.azure.com/scalesetpriority=spot:NoSchedule`

, so only pods with a corresponding toleration are scheduled on this node.

## Verify the Spot node pool

- Verify your node pool was added using the
command and confirming the`az aks nodepool show`

`scaleSetPriority`

is`Spot`

.

```
az aks nodepool show --resource-group $RESOURCE_GROUP --cluster-name $AKS_CLUSTER --name $SPOT_NODEPOOL
```


Results:

```
{
"artifactStreamingProfile": null,
"availabilityZones": null,
"capacityReservationGroupId": null,
"count": 3,
"creationData": null,
"currentOrchestratorVersion": "1.30.10",
"eTag": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"enableAutoScaling": true,
"enableCustomCaTrust": false,
"enableEncryptionAtHost": false,
"enableFips": false,
"enableNodePublicIp": false,
"enableUltraSsd": false,
"gatewayProfile": null,
"gpuInstanceProfile": null,
"gpuProfile": null,
"hostGroupId": null,
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/xxxxxxxxxxxxxxxx/providers/Microsoft.ContainerService/managedClusters/xxxxxxxxxxxxxxxx/agentPools/xxxxxxxxxxxx",
"kubeletConfig": null,
"kubeletDiskType": "OS",
"linuxOsConfig": null,
"maxCount": 3,
"maxPods": 30,
"messageOfTheDay": null,
"minCount": 1,
"mode": "User",
"name": "xxxxxxxxxxxx",
"networkProfile": {
"allowedHostPorts": null,
"applicationSecurityGroups": null,
"nodePublicIpTags": null
},
"nodeImageVersion": "AKSUbuntu-2204gen2containerd-xxxxxxxx.xx.x",
"nodeInitializationTaints": null,
"nodeLabels": {
"kubernetes.azure.com/scalesetpriority": "spot"
},
"nodePublicIpPrefixId": null,
"nodeTaints": [
"kubernetes.azure.com/scalesetpriority=spot:NoSchedule"
],
"orchestratorVersion": "x.xx.xx",
"osDiskSizeGb": 128,
"osDiskType": "Managed",
"osSku": "Ubuntu",
"osType": "Linux",
"podIpAllocationMode": null,
"podSubnetId": null,
"powerState": {
"code": "Running"
},
"provisioningState": "Creating",
"proximityPlacementGroupId": null,
"resourceGroup": "xxxxxxxxxxxxxxxx",
"scaleDownMode": "Delete",
"scaleSetEvictionPolicy": "Delete",
"scaleSetPriority": "Spot",
"securityProfile": {
"enableSecureBoot": false,
"enableVtpm": false,
"sshAccess": "LocalUser"
},
"spotMaxPrice": -1.0,
"status": null,
"tags": null,
"type": "Microsoft.ContainerService/managedClusters/agentPools",
"typePropertiesType": "VirtualMachineScaleSets",
"upgradeSettings": {
"drainTimeoutInMinutes": null,
"maxSurge": null,
"maxUnavailable": null,
"nodeSoakDurationInMinutes": null,
"undrainableNodeBehavior": null
},
"virtualMachineNodesStatus": null,
"virtualMachinesProfile": null,
"vmSize": "Standard_DS2_v2",
"vnetSubnetId": null,
"windowsProfile": null,
"workloadRuntime": "OCIContainer"
}
```


## Schedule a pod to run on the Spot node

To schedule a pod to run on a Spot node, you can add a toleration and node affinity that corresponds to the taint applied to your Spot node.

The following example shows a portion of a YAML file that defines a toleration corresponding to the `kubernetes.azure.com/scalesetpriority=spot:NoSchedule`

taint and a node affinity corresponding to the `kubernetes.azure.com/scalesetpriority=spot`

label used in the previous step with `requiredDuringSchedulingIgnoredDuringExecution`

and `preferredDuringSchedulingIgnoredDuringExecution`

node affinity rules:

```
spec:
containers:
- name: spot-example
tolerations:
- key: "kubernetes.azure.com/scalesetpriority"
operator: "Equal"
value: "spot"
effect: "NoSchedule"
affinity:
nodeAffinity:
requiredDuringSchedulingIgnoredDuringExecution:
nodeSelectorTerms:
- matchExpressions:
- key: "kubernetes.azure.com/scalesetpriority"
operator: In
values:
- "spot"
preferredDuringSchedulingIgnoredDuringExecution:
- weight: 1
preference:
matchExpressions:
- key: another-node-label-key
operator: In
values:
- another-node-label-value
```


When you deploy a pod with this toleration and node affinity, Kubernetes successfully schedules the pod on the nodes with the taint and label applied. In this example, the following rules apply:

- The node
*must*have a label with the key`kubernetes.azure.com/scalesetpriority`

, and the value of that label*must*be`spot`

. - The node
*preferably*has a label with the key`another-node-label-key`

, and the value of that label*must*be`another-node-label-value`

.

For more information, see [Assigning pods to nodes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity).

## Upgrade a Spot node pool

When you upgrade a Spot node pool, AKS internally issues a cordon and an eviction notice, but no drain is applied. There are no surge nodes available for Spot node pool upgrades. Outside of these changes, the behavior when upgrading Spot node pools is consistent with that of other node pool types.

For more information on upgrading, see [Upgrade an AKS cluster](upgrade-cluster).

## Max price for a Spot pool

[Pricing for Spot instances is variable](/en-us/azure/virtual-machine-scale-sets/use-spot#pricing), based on region and SKU. For more information, see pricing information for [Linux](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/) and [Windows](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/windows/).

With variable pricing, you have the option to set a max price, in US dollars (USD) using up to five decimal places. For example, the value *0.98765* would be a max price of *$0.98765 USD per hour*. If you set the max price to *-1*, the instance won't be evicted based on price. As long as there's capacity and quota available, the price for the instance will be the lower price of either the current price for a Spot instance or for a standard instance.

## Next steps

In this article, you learned how to add a Spot node pool to an AKS cluster. For more information about how to control pods across node pools, see [Best practices for advanced scheduler features in AKS](operator-best-practices-advanced-scheduler).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-images -->

# Node images in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes the node images available for Azure Kubernetes Service (AKS) nodes.

Caution

In this article, there are references to Ubuntu OS versions that are being deprecated for AKS.

- Starting on March 17, 2027, AKS no longer supports Ubuntu 20.04. Existing node images will be deleted and AKS will no longer provide security updates. You'll no longer be able to scale your node pools. Migrate to a supported Ubuntu version by
[upgrading your node pools](upgrade-aks-cluster)to kubernetes version 1.34+. For more information on this retirement, see[AKS GitHub Issues](https://github.com/Azure/AKS/issues/4874). - As of
**November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the[202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning**March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by[upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster)to a supported Kubernetes version or migrating to[osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see[[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

Important

Older node images can contain unpatched security vulnerabilities and might not work properly with recently released features. Using older images might lead to issues with scaling, node readiness, and security. Depending on the age of the image version, it could also place the cluster outside of the support scope until you perform a node image upgrade. **We recommend that you keep node images current and enable automatic upgrades**.

## Node image releases

Azure Kubernetes Service (AKS) regularly provides new node images, so it's beneficial to upgrade your node images frequently to access the latest AKS features, component updates, and security fixes. You can find detailed summaries of each node image version in the [AKS VHD notes](https://github.com/Azure/AKS/tree/master/vhd-notes).

Linux node images are released weekly, and Windows node images are released monthly. New node images are included in the [AKS release notes](https://github.com/Azure/AKS/releases).


Best practice guidanceConfigure

[automatic node image upgrades]and schedule them using[planned maintenance]. This will ensure that your node images are always up to date without requiring manual upgrades.

When new node images are released, it can take up to two weeks for the updates to be rolled out across all regions. The [AKS Release Tracker](release-tracker) shows the current latest node image version, three previously available node image versions for each region, and the node image update order by region. Once the node image is available in your region, you can perform a [manual node image upgrade](node-image-upgrade) or configure [automatic node image upgrades](auto-upgrade-node-os-image) and schedule them using [planned maintenance](planned-maintenance).

## Default node images

AKS sets a default operating system (OS) and node image during cluster and node pool creation. OS Type can be used to filter between Linux or Windows.

| OS Type | Default OS | Default node image |
|---|---|---|
| Not Specified | Ubuntu Linux | Ubuntu with containerd and gen 2 |
| Linux | Ubuntu Linux | Ubuntu with containerd and gen 2 |
| Windows | Windows Server | Windows Server Long Term Servicing Channel (LTSC) with containerd and gen 1 |

Note

You can't specify the Windows OS Type during cluster creation since the system node pool in every cluster must be Linux.

### Factors that influence the default node image

The following factors influence the default image AKS chooses for your node pool:

**OS SKU**: If`--os-sku`

is specified, then your default OS changes. For example, if you specify Azure Linux as the OS SKU, then your node image is Azure Linux with containerd.**Virtual machine (VM) size**:**Hypervisor generation**: Each VM size supports Generation 1,[Generation 2](generation-2-vm), or both.- If Generation 2 is supported, AKS defaults to using the Generation 2 node image in all OS versions except for Windows Server 2019 and Windows Server 2022.
- If only Generation 1 is supported, AKS defaults to using the Generation 1 node image. Generation 1 isn't supported for Azure Linux OS Guard (preview) or Flatcar Container Linux for AKS (preview).

**Feature enablement**: There are some features embedded into the node image. If you choose to use any of these features, your default node image changes.[Federal Information Processing Standards (FIPS)](enable-fips-nodes)changes the default node image for all Linux node pools.[Pod Sandboxing](use-pod-sandboxing)changes the default node image for Azure Linux node pools.[Trusted Launch](use-trusted-launch)changes the default node image for all Linux node pools.


Note

Certain features can't be combined in a single node pool. Follow links to the feature documentation to review the limitations.

## Available Linux node images

### Ubuntu node images

The Ubuntu node images are fully validated by AKS and supported by Microsoft, Canonical, and the Ubuntu community. AKS won't retire an Ubuntu version before the end of Canonical's support lifecycle.

| Node image | Use case | Limitations |
|---|---|---|
Ubuntu with containerd and Gen 1 |
This is the standard node image for Ubuntu node pools using a VM size that only supports Generation 1. | N/A |
Ubuntu with containerd and Gen 2 |
This is the standard node image for Ubuntu node pools using a VM size that supports Generation 2. If a VM size supports both Generation 1 and Generation 2, this node image is selected. | N/A |
Ubuntu with containerd and FIPS |
This is a variant of the default node image for customers that enable
|

**Ubuntu with containerd and Arm64**[Arm64](use-arm64-vms). These images support Generation 2 only.**Ubuntu with containerd and CVM**[Confidential VM](use-cvm)size. These images support Generation 2 only.**Ubuntu with containerd and Trusted Launch**[Trusted Launch](use-trusted-launch). These images support Generation 2 only.### Azure Linux node images

The Azure Linux node images are fully validated by AKS and built from source, using a native AKS image.

| Node image | Use case | Limitations |
|---|---|---|
Azure Linux with containerd and Gen 1 |
This is the standard node image for Azure Linux node pools using a VM size that only supports Generation 1. | N/A |
Azure Linux with containerd and Gen 2 |
This is the standard node image for Azure Linux node pools using a VM size that supports Generation 2. If a VM size supports both Generation 1 and Generation 2, node image is selected. | N/A |
Azure Linux with containerd and FIPS |
This is a variant of the default node image for customers that enable
|

**Azure Linux with containerd and Arm64**[Arm64](use-arm64-vms). These images support Generation 2 only.**Azure Linux with containerd, FIPS, and Arm64**[Federal Information Processing Standards (FIPS)](enable-fips-nodes)and use a VM size that supports[Arm64](use-arm64-vms). These images support Generation 2 only.**Azure Linux with containerd and Trusted Launch**[Trusted Launch](use-trusted-launch). These images support Generation 2 only.**Azure Linux with containerd and Pod Sandboxing**[Pod Sandboxing](use-pod-sandboxing). These images support Generation 2 only.### Azure Linux with OS Guard for AKS (preview) node images

The Azure Linux with OS Guard for AKS node images are fully validated by AKS and built from source, using a native AKS image. Versioning for Azure Linux with OS Guard node images follow the AKS date-based format (for example: 202509.23.0). You can check the node images in the release notes and by running the [ az aks nodepool list](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-list) command to view the

`nodeImageVersion`

. For more information, see [Azure Linux with OS Guard for AKS](use-azure-linux-os-guard).

| Node image | Use case | Limitations |
|---|---|---|
Azure Linux with OS Guard with containerd, Gen 2, FIPS, and Trusted Launch |
This is the standard node image for Azure Linux with OS Guard for AKS node pools using a VM size. If you use a VM size that supports Gen 1 only, you won't be able to use Azure Linux with OS Guard. | N/A |

### Flatcar Container Linux for AKS (preview) node images

The Flatcar Container Linux for AKS node images are fully validated by AKS and supported by Microsoft and the Flatcar community. Versioning for Flatcar Container Linux node images follow the AKS date-based format (for example: 202506.13.0). You can check the node images in the release notes and by using the [ az aks nodepool list](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-list) command to view the

`nodeImageVersion`

. You can check the Flatcar version number (for example: Flatcar 4344.0.0) in the release notes and by running the `kubectl get nodes`

command. For more information, see [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks).

| Node image | Use case | Limitations |
|---|---|---|
Flatcar Container Linux with containerd and Gen 2 |
This is the standard node image for Flatcar Container Linux for AKS node pools using a VM size. If you use a VM size that supports Gen 1 only, you won't be able to use Flatcar OS. | N/A |
Flatcar Container Linux with containerd and Arm64 |
This is a variant of the default node image for customers that use a VM size that supports
|

## Available Windows Server node images

The Windows Server node images are fully validated by AKS and supported by Microsoft.

### Windows Server Long Term Servicing Channel (LTSC) node images

| Node image | Use case | Limitations |
|---|---|---|
Windows Server with containerd and Gen 1 |
This is the standard node image for Windows node pools using a VM size that supports Generation 1. If a VM size supports both Generation 1 and Generation 2, this node image is selected if using Windows Server 2019 or Windows Server 2022. | N/A |
Windows Server with containerd and Gen 2 |
This is the standard node image for Windows node pools using a VM size that supports Generation 2. If a VM size supports both Generation 1 and Generation 2, this node image is selected if using Windows Server 2025. | N/A |

### Windows Server Annual Channel for Containers (preview) node images

| Node image | Use case | Limitations |
|---|---|---|
Windows Server with containerd and Gen 1 |
This is the standard node image for Windows node pools using a VM size that only supports Generation 1. If a VM size supports both Generation 1 and Generation 2, this node image is selected. | N/A |
Windows Server with containerd and Gen 2 |
This is the standard node image for Windows node pools using a VM size that supports Generation 2. | N/A |

## Next steps

To learn more about node images, node pool upgrades, and node configurations on AKS, see the following resources:

- To learn about nodes and node configurations, see
[AKS core concepts](core-aks-concepts). - Configure
[automatic node image upgrades](auto-upgrade-node-os-image)and schedule them using[planned maintenance](planned-maintenance). - Apply
[custom node configurations](custom-node-configuration)to modify OS or kubelet settings. - For information about the latest node images, see the
[AKS release notes](https://github.com/Azure/AKS/releases). [Automatically apply cluster and node pool upgrades with GitHub Actions](node-upgrade-github-actions).- Learn about upgrading best practices with
[AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-identity -->

# Access and identity options for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can authenticate, authorize, secure, and control access to Kubernetes clusters in a variety of ways:

- Using Kubernetes role-based access control (Kubernetes RBAC), you can grant users, groups, and service accounts access to only the resources they need.
- With Azure Kubernetes Service (AKS), you can further enhance the security and permissions structure using Microsoft Entra ID and Azure RBAC.

Kubernetes RBAC and AKS help you secure your cluster access and provide only the minimum required permissions to developers and operators.

This article introduces the core concepts that help you authenticate and assign permissions in AKS.

## Kubernetes RBAC

Kubernetes RBAC provides granular filtering of user actions. With this control mechanism:

- You assign users or user groups permission to create and modify resources or view logs from running application workloads.
- You can scope permissions to a single namespace or across the entire AKS cluster.
- You create
*roles*to define permissions, and then assign those roles to users with*role bindings*.

For more information, see [Using Kubernetes RBAC authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/).

### Roles and ClusterRoles

#### Roles

Before assigning permissions to users with Kubernetes RBAC, you'll define user permissions as a *Role*. Grant permissions within a namespace using roles.

Note

Kubernetes roles *grant* permissions; they don't *deny* permissions.

To grant permissions across the entire cluster or to cluster resources outside a given namespace, you can instead use *ClusterRoles*.

#### ClusterRoles

A ClusterRole grants and applies permissions to resources across the entire cluster, not a specific namespace.

### RoleBindings and ClusterRoleBindings

Once you've defined roles to grant permissions to resources, you assign those Kubernetes RBAC permissions with a *RoleBinding*. If your AKS cluster [integrates with Microsoft Entra ID](#azure-ad-integration), RoleBindings grant permissions to Microsoft Entra users to perform actions within the cluster. See how in [Control access to cluster resources using Kubernetes role-based access control and Microsoft Entra identities](azure-ad-rbac).

#### RoleBindings

Assign roles to users for a given namespace using RoleBindings. With RoleBindings, you can logically segregate a single AKS cluster, only enabling users to access the application resources in their assigned namespace.

To bind roles across the entire cluster, or to cluster resources outside a given namespace, you instead use *ClusterRoleBindings*.

#### ClusterRoleBinding

With a ClusterRoleBinding, you bind roles to users and apply to resources across the entire cluster, not a specific namespace. This approach lets you grant administrators or support engineers access to all resources in the AKS cluster.

Note

Microsoft/AKS performs any cluster actions with user consent under a built-in Kubernetes role `aks-service`

and built-in role binding `aks-service-rolebinding`

.

This role enables AKS to troubleshoot and diagnose cluster issues, but can't modify permissions nor create roles or role bindings, or other high privilege actions. Role access is only enabled under active support tickets with just-in-time (JIT) access. Read more about [AKS support policies](support-policies).

### Kubernetes service accounts

*Service accounts* are one of the primary user types in Kubernetes. The Kubernetes API holds and manages service accounts. Service account credentials are stored as Kubernetes secrets, allowing them to be used by authorized pods to communicate with the API Server. Most API requests provide an authentication token for a service account or a normal user account.

Normal user accounts allow more traditional access for human administrators or developers, not just services and processes. While Kubernetes doesn't provide an identity management solution to store regular user accounts and passwords, you can integrate external identity solutions into Kubernetes. For AKS clusters, this integrated identity solution is Microsoft Entra ID.

For more information on the identity options in Kubernetes, see [Kubernetes authentication](https://kubernetes.io/docs/reference/access-authn-authz/authentication).

## Azure role-based access control

Azure role-based access control (RBAC) is an authorization system built on [Azure Resource Manager](/en-us/azure/azure-resource-manager/management/overview) that provides fine-grained access management of Azure resources.

| RBAC system | Description |
|---|---|
| Kubernetes RBAC | Designed to work on Kubernetes resources within your AKS cluster. |
| Azure RBAC | Designed to work on resources within your Azure subscription. |

With Azure RBAC, you create a *role definition* that outlines the permissions to be applied. You then assign a user or group this role definition via a *role assignment* for a particular *scope*. The scope can be an individual resource, a resource group, or across the subscription.

For more information, see [What is Azure role-based access control (Azure RBAC)?](/en-us/azure/role-based-access-control/overview)

There are two levels of access needed to fully operate an AKS cluster:

[Access the AKS resource in your Azure subscription](#azure-rbac-to-authorize-access-to-the-aks-resource).- Control scaling or upgrading your cluster using the AKS APIs.
- Pull your
`kubeconfig`

.

- Access to the Kubernetes API. This access is controlled by either:
[Kubernetes RBAC](#kubernetes-rbac)(traditionally).[Integrating Azure RBAC with AKS for Kubernetes authorization](#azure-rbac-for-kubernetes-authorization).


### Azure RBAC to authorize access to the AKS resource

With Azure RBAC, you can provide your users (or identities) with granular access to AKS resources across one or more subscriptions. For example, you could use the [Azure Kubernetes Service Contributor role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-contributor-role) to scale and upgrade your cluster. Meanwhile, another user with the [Azure Kubernetes Service Cluster Admin role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-cluster-admin-role) only has permission to pull the Admin `kubeconfig`

.

[Use Azure RBAC to define access to the Kubernetes configuration file in AKS](control-kubeconfig-access).

### Azure RBAC for Kubernetes Authorization

With the Azure RBAC integration, AKS will use a Kubernetes Authorization webhook server so you can manage Microsoft Entra integrated Kubernetes cluster resource permissions and assignments using Azure role definition and role assignments.

As shown in the above diagram, when using the Azure RBAC integration, all requests to the Kubernetes API will follow the same authentication flow as explained on the [Microsoft Entra integration section](#azure-ad-integration).

If the identity making the request exists in Microsoft Entra ID, Azure will team with Kubernetes RBAC to authorize the request. If the identity exists outside of Microsoft Entra ID (i.e., a Kubernetes service account), authorization will defer to the normal Kubernetes RBAC.

In this scenario, you use Azure RBAC mechanisms and APIs to assign users built-in roles or create custom roles, just as you would with Kubernetes roles.

With this feature, you not only give users permissions to the AKS resource across subscriptions, but you also configure the role and permissions for inside each of those clusters controlling Kubernetes API access. For example, you can grant the `Azure Kubernetes Service RBAC Reader`

role on the subscription scope. The role recipient will be able to list and get all Kubernetes objects from all clusters without modifying them.

Important

You need to enable Azure RBAC for Kubernetes authorization before using this feature. For more details and step by step guidance, follow our [Use Azure RBAC for Kubernetes Authorization](manage-azure-rbac) how-to guide.

#### Built-in roles

AKS provides the following four built-in roles. They are similar to the [Kubernetes built-in roles](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#user-facing-roles) with a few differences, like supporting CRDs. See the full list of actions allowed by each [Azure built-in role](/en-us/azure/role-based-access-control/built-in-roles).

| Role | Description |
|---|---|
| Azure Kubernetes Service RBAC Reader | Allows read-only access to see most objects in a namespace. Doesn't allow viewing roles or role bindings. Doesn't allow viewing `Secrets` . Reading the `Secrets` contents enables access to `ServiceAccount` credentials in the namespace, which would allow API access as any `ServiceAccount` in the namespace (a form of privilege escalation). |
| Azure Kubernetes Service RBAC Writer | Allows read/write access to most objects in a namespace. Doesn't allow viewing or modifying roles, or role bindings. Allows accessing `Secrets` and running pods as any ServiceAccount in the namespace, so it can be used to gain the API access levels of any ServiceAccount in the namespace. |
| Azure Kubernetes Service RBAC Admin | Allows admin access, intended to be granted within a namespace. Allows read/write access to most resources in a namespace (or cluster scope), including the ability to create roles and role bindings within the namespace. Doesn't allow write access to resource quota or to the namespace itself. |
| Azure Kubernetes Service RBAC Cluster Admin | Allows super-user access to perform any action on any resource. Gives full control over every resource in the cluster and in all namespaces. |

## Microsoft Entra integration

Enhance your AKS cluster security with Microsoft Entra integration. Built on decades of enterprise identity management, Microsoft Entra ID is a multi-tenant, cloud-based directory and identity management service that combines core directory services, application access management, and identity protection. With Microsoft Entra ID, you can integrate on-premises identities into AKS clusters to provide a single source for account management and security.

With Microsoft Entra integrated AKS clusters, you can grant users or groups access to Kubernetes resources within a namespace or across the cluster.

- To obtain a
`kubectl`

configuration context, a user runs the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. - When a user interacts with the AKS cluster with
`kubectl`

, they're prompted to sign in with their Microsoft Entra credentials.

This approach provides a single source for user account management and password credentials. The user can only access the resources as defined by the cluster administrator.

Microsoft Entra authentication is provided to AKS clusters with OpenID Connect. OpenID Connect is an identity layer built on top of the OAuth 2.0 protocol. For more information on OpenID Connect, see the [OpenID Connect documentation](/en-us/azure/active-directory/develop/v2-protocols-oidc). From inside of the Kubernetes cluster, [Webhook Token Authentication](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#webhook-token-authentication) is used to verify authentication tokens. Webhook token authentication is configured and managed as part of the AKS cluster.

### Webhook and API server

As shown in the graphic above, the API server calls the AKS webhook server and performs the following steps:

`kubectl`

uses the Microsoft Entra client application to sign in users with[OAuth 2.0 device authorization grant flow](/en-us/azure/active-directory/develop/v2-oauth2-device-code).- Microsoft Entra ID provides an access_token, id_token, and a refresh_token.
- The user makes a request to
`kubectl`

with an access_token from`kubeconfig`

. `kubectl`

sends the access_token to API Server.- The API Server is configured with the Auth WebHook Server to perform validation.
- The authentication webhook server confirms the JSON Web Token signature is valid by checking the Microsoft Entra public signing key.
- If the user is a member of more than 200 groups, the server application uses user-provided credentials to query group memberships of the logged-in user from the MS Graph API. For users with group memberships of 200 or fewer the groups claim already exists in the client token. No query will be performed.
- A response is sent to the API Server with user information such as the user principal name (UPN) claim of the access token, and the group membership of the user based on the object ID.
- The API performs an authorization decision based on the Kubernetes Role/RoleBinding.
- Once authorized, the API server returns a response to
`kubectl`

. `kubectl`

provides feedback to the user.

Learn how to integrate AKS with Microsoft Entra ID with our [AKS-managed Microsoft Entra integration how-to guide](managed-azure-ad).

## AKS service permissions

When creating a cluster, AKS generates or modifies resources it needs (like VMs and NICs) to create and run the cluster on behalf of the user. This identity is distinct from the cluster's identity permission, which is created during cluster creation.

### Identity creating and operating the cluster permissions

The following permissions are needed by the identity creating and operating the cluster.

| Permission | Reason |
|---|---|
`Microsoft.Compute/diskEncryptionSets/read` |
Required to read disk encryption set ID. |
`Microsoft.Compute/proximityPlacementGroups/write` |
Required for updating proximity placement groups. |
`Microsoft.Network/applicationGateways/read` `Microsoft.Network/applicationGateways/write` `Microsoft.Network/virtualNetworks/subnets/join/action` |
Required to configure application gateways and join the subnet. |
`Microsoft.Network/virtualNetworks/subnets/join/action` |
Required to configure the Network Security Group for the subnet when using a custom VNET. |
`Microsoft.Network/publicIPAddresses/join/action` `Microsoft.Network/publicIPPrefixes/join/action` |
Required to configure the outbound public IPs on the Standard Load Balancer. |
`Microsoft.OperationalInsights/workspaces/sharedkeys/read` `Microsoft.OperationalInsights/workspaces/read` `Microsoft.OperationsManagement/solutions/write` `Microsoft.OperationsManagement/solutions/read` `Microsoft.ManagedIdentity/userAssignedIdentities/assign/action` |
Required to create and update Log Analytics workspaces and Azure monitoring for containers. |
`Microsoft.Network/virtualNetworks/joinLoadBalancer/action` |
Required to configure the IP-based Load Balancer Backend Pools. |

### AKS cluster identity permissions

The following permissions are used by the AKS cluster identity, which is created and associated with the AKS cluster. Each permission is used for the reasons below:

| Permission | Reason |
|---|---|
`Microsoft.ContainerService/managedClusters/*` |
Required for creating users and operating the cluster |
`Microsoft.Network/loadBalancers/delete` `Microsoft.Network/loadBalancers/read` `Microsoft.Network/loadBalancers/write` |
Required to configure the load balancer for a LoadBalancer service. |
`Microsoft.Network/publicIPAddresses/delete` `Microsoft.Network/publicIPAddresses/read` `Microsoft.Network/publicIPAddresses/write` |
Required to find and configure public IPs for a LoadBalancer service. |
`Microsoft.Network/publicIPAddresses/join/action` |
Required for configuring public IPs for a LoadBalancer service. |
`Microsoft.Network/networkSecurityGroups/read` `Microsoft.Network/networkSecurityGroups/write` |
Required to create or delete security rules for a LoadBalancer service. |
`Microsoft.Compute/disks/delete` `Microsoft.Compute/disks/read` `Microsoft.Compute/disks/write` `Microsoft.Compute/locations/DiskOperations/read` |
Required to configure AzureDisks. |
`Microsoft.Storage/storageAccounts/delete` `Microsoft.Storage/storageAccounts/listKeys/action` `Microsoft.Storage/storageAccounts/read` `Microsoft.Storage/storageAccounts/write` `Microsoft.Storage/operations/read` |
Required to configure storage accounts for AzureFile or AzureDisk. |
`Microsoft.Network/routeTables/read` `Microsoft.Network/routeTables/routes/delete` `Microsoft.Network/routeTables/routes/read` `Microsoft.Network/routeTables/routes/write` `Microsoft.Network/routeTables/write` |
Required to configure route tables and routes for nodes. |
`Microsoft.Compute/virtualMachines/read` |
Required to find information for virtual machines in a VMAS, such as zones, fault domain, size, and data disks. |
`Microsoft.Compute/virtualMachines/write` |
Required to attach AzureDisks to a virtual machine in a VMAS. |
`Microsoft.Compute/virtualMachineScaleSets/read` `Microsoft.Compute/virtualMachineScaleSets/virtualMachines/read` `Microsoft.Compute/virtualMachineScaleSets/virtualmachines/instanceView/read` |
Required to find information for virtual machines in a virtual machine scale set, such as zones, fault domain, size, and data disks. |
`Microsoft.Network/networkInterfaces/write` |
Required to add a virtual machine in a VMAS to a load balancer backend address pool. |
`Microsoft.Compute/virtualMachineScaleSets/write` |
Required to add a virtual machine scale set to a load balancer backend address pools and scale out nodes in a virtual machine scale set. |
`Microsoft.Compute/virtualMachineScaleSets/delete` |
Required to delete a virtual machine scale set to a load balancer backend address pools and scale down nodes in a virtual machine scale set. |
`Microsoft.Compute/virtualMachineScaleSets/virtualmachines/write` |
Required to attach AzureDisks and add a virtual machine from a virtual machine scale set to the load balancer. |
`Microsoft.Network/networkInterfaces/read` |
Required to search internal IPs and load balancer backend address pools for virtual machines in a VMAS. |
`Microsoft.Compute/virtualMachineScaleSets/virtualMachines/networkInterfaces/read` |
Required to search internal IPs and load balancer backend address pools for a virtual machine in a virtual machine scale set. |
`Microsoft.Compute/virtualMachineScaleSets/virtualMachines/networkInterfaces/ipconfigurations/publicipaddresses/read` |
Required to find public IPs for a virtual machine in a virtual machine scale set. |
`Microsoft.Network/virtualNetworks/read` `Microsoft.Network/virtualNetworks/subnets/read` |
Required to verify if a subnet exists for the internal load balancer in another resource group. |
`Microsoft.Compute/snapshots/delete` `Microsoft.Compute/snapshots/read` `Microsoft.Compute/snapshots/write` |
Required to configure snapshots for AzureDisk. |
`Microsoft.Compute/locations/vmSizes/read` `Microsoft.Compute/locations/operations/read` |
Required to find virtual machine sizes for finding AzureDisk volume limits. |

### Additional cluster identity permissions

When creating a cluster with specific attributes, you will need the following additional permissions for the cluster identity. Since these permissions are not automatically assigned, you must add them to the cluster identity after it's created.

| Permission | Reason |
|---|---|
`Microsoft.Network/networkSecurityGroups/write` `Microsoft.Network/networkSecurityGroups/read` |
Required if using a network security group in another resource group. Required to configure security rules for a LoadBalancer service. |
`Microsoft.Network/virtualNetworks/subnets/read` `Microsoft.Network/virtualNetworks/subnets/join/action` |
Required if using a subnet in another resource group such as a custom VNET. |
`Microsoft.Network/routeTables/routes/read` `Microsoft.Network/routeTables/routes/write` |
Required if using a subnet associated with a route table in another resource group such as a custom VNET with a custom route table. Required to verify if a subnet already exists for the subnet in the other resource group. |
`Microsoft.Network/virtualNetworks/subnets/read` |
Required if using an internal load balancer in another resource group. Required to verify if a subnet already exists for the internal load balancer in the resource group. |
`Microsoft.Network/privatednszones/*` |
Required if using a private DNS zone in another resource group such as a custom privateDNSZone. |

## AKS Node Access

By default Node Access is not required for AKS. The following access is needed for the node if a specific component is leveraged.

| Access | Reason |
|---|---|
`kubelet` |
Required to grant MSI access to ACR. |
`http app routing` |
Required for write permission to "random name".aksapp.io. |
`container insights` |
Required to grant permission to the Log Analytics workspace. |

## Summary

View the table for a quick summary of how users can authenticate to Kubernetes when Microsoft Entra integration is enabled. In all cases, the user's sequence of commands is:

Run

`az login`

to authenticate to Azure.Run

`az aks get-credentials`

to download credentials for the cluster into`.kube/config`

.Run

`kubectl`

commands.- The first command may trigger browser-based authentication to authenticate to the cluster, as described in the following table.


In the Azure portal, you can find:

- The
*Role Grant*(Azure RBAC role grant) referred to in the second column is shown on the**Access Control**tab. - The Cluster Admin Microsoft Entra group is shown on the
**Configuration**tab.- Also found with parameter name
`--aad-admin-group-object-ids`

in the Azure CLI.

- Also found with parameter name

| Description | Role grant required | Cluster admin Microsoft Entra group(s) | When to use |
|---|---|---|---|
| Legacy admin login using client certificate | Azure Kubernetes Service Cluster Admin Role. This role allows `az aks get-credentials` to be used with the `--admin` flag, which downloads a
`.kube/config` . This is the only purpose of "Azure Kubernetes Service Cluster Admin Role". |
n/a | If you're permanently blocked by not having access to a valid Microsoft Entra group with access to your cluster. |
| Microsoft Entra ID with manual (Cluster)RoleBindings | Azure Kubernetes Service Cluster User Role. The "User" role allows `az aks get-credentials` to be used without the `--admin` flag. (This is the only purpose of "Azure Kubernetes Service Cluster User Role".) The result, on a Microsoft Entra ID-enabled cluster, is the download of
`.kube/config` , which triggers browser-based authentication when it's first used by `kubectl` . |
User is not in any of these groups. Because the user is not in any Cluster Admin groups, their rights will be controlled entirely by any RoleBindings or ClusterRoleBindings that have been set up by cluster admins. The (Cluster)RoleBindings
`subjects` . If no such bindings have been set up, the user will not be able to excute any `kubectl` commands. |

`cluster-admin`

Kubernetes role. So users in these groups can run all `kubectl`

commands as `cluster-admin`

.*not*using Azure RBAC for Kubernetes authorization.First,

**Azure Kubernetes Service Cluster User Role**(as above).Second, one of the "Azure Kubernetes Service

**RBAC**..." roles listed above, or your own custom alternative.## Next steps

- To get started with Microsoft Entra ID and Kubernetes RBAC, see
[Integrate Microsoft Entra ID with AKS](managed-azure-ad). - For associated best practices, see
[Best practices for authentication and authorization in AKS](operator-best-practices-identity). - To get started with Azure RBAC for Kubernetes Authorization, see
[Use Azure RBAC to authorize access within the Azure Kubernetes Service (AKS) Cluster](manage-azure-rbac). - To get started securing your
`kubeconfig`

file, see[Limit access to cluster configuration file](control-kubeconfig-access). - To get started with managed identities in AKS, see
[Use a managed identity in AKS](use-managed-identity).

For more information on core Kubernetes and AKS concepts, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-disruption -->

# Configure node disruption policies for node auto-provisioning (NAP) nodes in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure node disruption policies for Azure Kubernetes Service (AKS) node auto-provisioning (NAP) nodes and details how disruption works to optimize resource utilization and cost efficiency.

NAP optimizes your cluster by:

- Removing or replacing underutilized nodes.
- Consolidating workloads to reduce costs.
- Respecting disruption budgets and maintenance windows.
- Providing manual control when needed.

## Before you begin

- Read the
[Overview of node auto-provisioning (NAP) in AKS](node-auto-provisioning)article, which details[how NAP works](node-auto-provisioning#how-does-node-auto-provisioning-work). - Read the
[Overview of networking configurations for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)](node-auto-provisioning-networking).

## How does node disruption work for NAP nodes?

Karpenter sets a Kubernetes [finalizer](https://kubernetes.io/docs/concepts/overview/working-with-objects/finalizers/) on each node and node claim it provisions. The finalizer blocks the deletion of the node object, while the Termination Controller taints and drains the node before removing the underlying node claim.

When the workloads on your nodes scale down, NAP uses disruption rules on the node pool specification to decide when and how to remove those nodes and potentially reschedule your workloads for efficiency.

## Node disruption methods

NAP automatically discovers nodes eligible for disruption and spins up replacements when needed. You can trigger disruption through automated methods like *Expiration*, *Consolidation*, and *Drift*, manual methods, or external systems.

## Expiration

Expiration allows you to set a maximum age for your NAP nodes. Nodes are marked as expired and disrupted after reaching the age you specify for the node pool's `spec.disruption.expireAfter`

value.

### Example expiration configuration

The following example shows how to set the expiration time for NAP nodes to 24 hours:

```
spec:
disruption:
expireAfter: 24h # Expire nodes after 24 hours
```


## Consolidation

NAP works to actively reduce cluster cost by identifying when nodes can be removed because they're empty or underutilized, or when nodes can be replaced with lower priced variants. This process is called *Consolidation*. NAP primarily uses Consolidation to delete or replace nodes for optimal pod placement.

NAP performs the following types of consolidation in order to optimize resource utilization:

**Empty node consolidation**: Deletes any empty nodes in parallel.**Multi-node consolidation**: Deletes multiple nodes, possibly launching a single replacement.**Single-node consolidation**: Deletes any single node, possibly launching a replacement.

You can trigger consolidation through the `spec.disruption.consolidationPolicy`

field in the node pool specification using the `WhenEmpty`

, or `WhenEmptyOrUnderUtilized`

settings. You can also set the `consolidateAfter`

field, which is a time-based condition that determines how long NAP waits after discovering a consolidation opportunity before disrupting the node.

### Example consolidation configuration

The following example shows how to configure NAP to consolidate nodes when they're empty, and to wait 30 seconds after discovering a consolidation opportunity before disrupting the node:

```
disruption:
# Describes which types of nodes NAP should consider for consolidation
# `WhenEmptyOrUnderUtilized`: NAP considers all nodes for consolidation and attempts to remove or replace nodes when it discovers that the node is empty or underutilized and could be changed to reduce cost
# `WhenEmpty`: NAP only considers nodes for consolidation that don't contain any workload pods
consolidationPolicy: WhenEmpty
# The amount of time NAP should wait after discovering a consolidation decision
# Currently, you can only set this value when the consolidation policy is `WhenEmpty`
# You can choose to disable consolidation entirely by setting the string value `Never`
consolidateAfter: 30s
```


## Drift

Drift handles changes to the `NodePool`

/`AKSNodeClass`

resources. Values in the `NodeClaimTemplateSpec`

/`AKSNodeClassSpec`

are reflected in the same way that they're set. A `NodeClaim`

is detected as *drifted* if the values in the associated `NodePool`

/`AKSNodeClass`

don't match the values in the `NodeClaim`

. Similar to the upstream `deployment.spec.template`

relationship to pods, Karpenter annotates the associated `NodePool`

/`AKSNodeClass`

with a hash of the `NodeClaimTemplateSpec`

to check for drift. Karpenter removes the `Drifted`

status condition in the following scenarios:

- The
`Drift`

feature gate isn't enabled but the`NodeClaim`

is drifted. - The
`NodeClaim`

isn't drifted, but has the status condition.

Karpenter or the cloud provider interface might discover [special cases](#special-cases-on-drift) triggered by `NodeClaim`

/`Instance`

/`NodePool`

/`AKSNodeClass`

changes.

### Special cases on drift

In special cases, drift can correspond to multiple values and must be handled differently. Drift on resolved fields can create cases where drift occurs without changes to Custom Resource Definitions (CRDs), or where CRD changes don't result in drift.

For example, if a `NodeClaim`

has `node.kubernetes.io/instance-type: Standard_D2s_v3`

, and requirements change from `node.kubernetes.io/instance-type In [Standard_D2s_v3]`

to `node.kubernetes.io/instance-type In [Standard_D2s_v3, Standard_D4s_v3]`

, the `NodeClaim`

isn't drifted because its value is still compatible with the new requirements. Conversely, if a `NodeClaim`

uses a `NodeClaim`

`imageFamily`

, but the `spec.imageFamily`

field changes, Karpenter detects the `NodeClaim`

as *drifted* and rotates the node to meet that specification.

Important

Karpenter monitors subnet configuration changes and detects drift when the `vnetSubnetID`

in an `AKSNodeClass`

is modified. Understanding this behavior is critical when managing custom networking configurations. For more information, see [Subnet drift behavior](node-auto-provisioning-networking#subnet-drift-behavior).

For more information, see [Drift Design](https://github.com/aws/karpenter-core/blob/main/designs/drift.md).

## Termination grace period

You can set a termination grace period for NAP nodes using the `spec.template.spec.terminationGracePeriod`

field in the node pool specification. This setting allows you to configure how long Karpenter waits for pods to terminate gracefully. This setting takes precedence over a pod's `terminationGracePeriodSeconds`

and bypasses `PodDisruptionBudgets`

and the `karpenter.sh/do-not-disrupt`

annotation.

### Example termination grace period configuration

The following example shows how to set a termination grace period of 30 seconds for NAP nodes:

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
template:
spec:
terminationGracePeriod: 30s
```


## Disruption budgets

You can rate limit Karpenter's disruption by modifying the `spec.disruption.budgets`

field in the node pool specification. If you leave this setting undefined, Karpenter defaults to one budget with `nodes: 10%`

. Budgets consider nodes that are being deleted for any reason, and they only block Karpenter from voluntary disruptions through expiration, drift, emptiness, and consolidation.

When calculating if a budget blocks nodes from disruption, Karpenter counts the total nodes owned by a node pool and then subtracts nodes that are being deleted and nodes that are `NotReady`

. If the budget is configured with a percentage value, such as `20%`

, Karpenter calculates the number of allowed disruptions as `allowed_disruptions = roundup(total * percentage) - total_deleting - total_notready`

. For multiple budgets in a node pool, Karpenter takes the minimum (most restrictive) value of each of the budgets.

### Schedule and duration fields

When using budgets, you can optionally set the `schedule`

and `duration`

fields to create time-based budgets. These fields allow you to define maintenance windows or specific timeframes when disruption limits are stricter.

**Schedule**uses cron job syntax with special macros like`@yearly`

,`@monthly`

,`@weekly`

,`@daily`

,`@hourly`

.**Duration**allows compound durations like`10h5m`

,`30m`

, or`160h`

. Duration and Schedule must be defined together.

#### Schedule and duration examples

##### Maintenance window budget

Prevent disruptions during business hours:

```
budgets:
- nodes: "0"
schedule: "0 9 * * 1-5" # 9 AM Monday-Friday
duration: 8h # For 8 hours
```


##### Weekend-only disruptions

Only allow disruptions on weekends:

```
budgets:
- nodes: "50%"
schedule: "0 0 * * 6" # Saturday midnight
duration: 48h # All weekend
- nodes: "0" # Block all other times
```


##### Gradual rollout budget

Allow increasing disruption rates:

```
budgets:
- nodes: "1"
schedule: "0 2 * * *" # 2 AM daily
duration: 2h
- nodes: "3"
schedule: "0 4 * * *" # 4 AM daily
duration: 4h
```


### Budget configuration examples

The following `NodePool`

specification has three budgets configured:

- The first budget allows 20% of nodes owned by the node pool to be disrupted at once.
- The second budget acts as a ceiling, only allowing five disruptions when there are more than 25 nodes.
- The last budget blocks disruptions during the first 10 minutes of each day.

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
disruption:
consolidationPolicy: WhenEmptyOrUnderutilized
expireAfter: 720h # 30 * 24h = 720h
budgets:
- nodes: "20%" # Allow 20% of nodes to be disrupted
- nodes: "5" # Cap at maximum 5 nodes
- nodes: "0" # Block all disruptions during maintenance window
schedule: "@daily" # Scheduled daily
duration: 10m # Duration of 10 minutes
```


## Manual node disruption

You can manually disrupt NAP nodes using `kubectl`

or by deleting `NodePool`

resources.

### Remove nodes with kubectl

You can manually remove nodes using the `kubectl delete node`

command. You can delete specific nodes, all NAP-managed nodes, or nodes from a specific node pool by using labels, for example:

```
# Delete a specific node
kubectl delete node $NODE_NAME
# Delete all NAP-managed nodes
kubectl delete nodes -l karpenter.sh/nodepool
# Delete nodes from a specific nodepool
kubectl delete nodes -l karpenter.sh/nodepool=$NODEPOOL_NAME
```


### Delete `NodePool`

resources

The `NodePool`

owns `NodeClaims`

through an owner reference. NAP gracefully terminates nodes through cascading deletion when you delete the associated `NodePool`

.

## Control disruption using annotations

You can block or disable disruption for specific pods, nodes, or entire node pools using annotations.

### Pod controls

Block NAP from disrupting certain pods by setting the `karpenter.sh/do-not-disrupt: "true"`

annotation:

```
apiVersion: apps/v1
kind: Deployment
spec:
template:
metadata:
annotations:
karpenter.sh/do-not-disrupt: "true"
```


This annotation prevents voluntary disruption for Expiration, Consolidation, and Drift. However, it doesn't prevent disruption from external systems or manual disruption through `kubectl`

or `NodePool`

deletion.

### Node controls

Block NAP from disrupting specific nodes:

```
apiVersion: v1
kind: Node
metadata:
annotations:
karpenter.sh/do-not-disrupt: "true"
```


### Node pool controls

Disable disruption for all nodes in a `NodePool`

:

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
template:
metadata:
annotations:
karpenter.sh/do-not-disrupt: "true"
```


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ssh -->

# Connect to Azure Kubernetes Service (AKS) cluster nodes for maintenance or troubleshooting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Throughout the lifecycle of your Azure Kubernetes Service (AKS) cluster, you eventually need to directly access an AKS node. This access could be for maintenance, log collection, or troubleshooting operations.

You access a node through authentication, which methods vary depending on your Node OS and method of connection. You securely authenticate against AKS Linux and Windows nodes through two options discussed in this article. One requires that you have Kubernetes API access, and the other is through the AKS ARM API, which provides direct private IP information. For security reasons, AKS nodes aren't exposed to the internet. Instead, to connect directly to any AKS nodes, you need to use either `kubectl debug`

or the host's private IP address.

## Access nodes using the Kubernetes API

This method requires usage of `kubectl debug`

command.

### Before you begin

This guide shows you how to create a connection to an AKS node and update the SSH key of your AKS cluster. To follow along the steps, you need to use Azure CLI that supports version 2.0.64 or later. Run `az --version`

to check the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Complete these steps if you don't have an SSH key. Create an SSH key depending on your Node OS Image, for [macOS and Linux](/en-us/azure/virtual-machines/linux/mac-create-ssh-keys), or [Windows](/en-us/azure/virtual-machines/linux/ssh-from-windows). Make sure you save the key pair in the OpenSSH format, avoid unsupported formats such as `.ppk`

. Next, refer to [Manage SSH configuration](manage-ssh-node-access) to add the key to your cluster.

### Linux and macOS

Linux and macOS users can access their node using `kubectl debug`

or their private IP Address. Windows users should skip to the Windows Server Proxy section for a workaround to SSH via proxy.

#### Connect using kubectl debug

To create an interactive shell connection, use the `kubectl debug`

command to run a privileged container on your node.

To list your nodes, use the

`kubectl get nodes`

command:`kubectl get nodes -o wide`

Sample output:

`NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE aks-nodepool1-37663765-vmss000000 Ready agent 166m v1.25.6 10.224.0.33 <none> Ubuntu 22.04.2 LTS aks-nodepool1-37663765-vmss000001 Ready agent 166m v1.25.6 10.224.0.4 <none> Ubuntu 22.04.2 LTS aksnpwin000000 Ready agent 160m v1.25.6 10.224.0.62 <none> Windows Server 2022 Datacenter`

Use the

`kubectl debug`

command to start a privileged container on your node and connect to it.`kubectl debug node/aks-nodepool1-37663765-vmss000000 -it --image=mcr.microsoft.com/cbl-mariner/busybox:2.0`

Sample output:

`Creating debugging pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx with container debugger on node aks-nodepool1-37663765-vmss000000. If you don't see a command prompt, try pressing enter. root@aks-nodepool1-37663765-vmss000000:/#`

You now have access to the node through a privileged container as a debugging pod.

Note

You can interact with the node session by running

`chroot /host`

from the privileged container.

#### Exit kubectl debug mode

When you're done with your node, enter the `exit`

command to end the interactive shell session. After the interactive container session closes, delete the debugging pod used with `kubectl delete pod`

.

```
kubectl delete pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx
```


### Windows Server proxy connection for SSH

Follow these steps as a workaround to connect with SSH on a Windows Server node.

#### Create a proxy server

At this time, you can't connect to a Windows Server node directly by using `kubectl debug`

. Instead, you need to first connect to another node in the cluster with `kubectl`

, then connect to the Windows Server node from that node using SSH.

To connect to another node in the cluster, use the `kubectl debug`

command. For more information, follow the above steps in the kubectl section. Create an SSH connection to the Windows Server node from another node using the SSH keys provided when you created the AKS cluster and the internal IP address of the Windows Server node.

Important

The following steps for creating the SSH connection to the Windows Server node from another node can only be used if you created your AKS cluster using the Azure CLI with the `--generate-ssh-keys`

parameter. If you want to use your own SSH keys instead, you can use the `az aks update`

to manage SSH keys on an existing AKS cluster. For more information, see [manage SSH node access](manage-ssh-node-access).

Note

If your Linux proxy node is down or unresponsive, use the [Azure Bastion](/en-us/azure/bastion/bastion-overview) method to connect instead.

Use the

`kubectl debug`

command to start a privileged container on your proxy (Linux) node and connect to it.`kubectl debug node/aks-nodepool1-37663765-vmss000000 -it --image=mcr.microsoft.com/cbl-mariner/busybox:2.0`

Sample output:

`Creating debugging pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx with container debugger on node aks-nodepool1-37663765-vmss000000. If you don't see a command prompt, try pressing enter. root@aks-nodepool1-37663765-vmss000000:/#`

Open a new terminal window and use the

`kubectl get pods`

command to get the name of the pod started by`kubectl debug`

.`kubectl get pods`

Sample output:

`NAME READY STATUS RESTARTS AGE node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx 1/1 Running 0 21s`

In the sample output,

*node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx*is the name of the pod started by`kubectl debug`

.Use the

`kubectl port-forward`

command to open a connection to the deployed pod:`kubectl port-forward node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx 2022:22`

Sample output:

`Forwarding from 127.0.0.1:2022 -> 22 Forwarding from [::1]:2022 -> 22`

The previous example begins forwarding network traffic from port

`2022`

on your development computer to port`22`

on the deployed pod. When using`kubectl port-forward`

to open a connection and forward network traffic, the connection remains open until you stop the`kubectl port-forward`

command.Open a new terminal and run the command

`kubectl get nodes`

to show the internal IP address of the Windows Server node:`kubectl get no -o custom-columns=NAME:metadata.name,'INTERNAL_IP:status.addresses[?(@.type == \"InternalIP\")].address'`

Sample output:

`NAME INTERNAL_IP aks-nodepool1-19409214-vmss000003 10.224.0.8`

In the previous example,

*10.224.0.62*is the internal IP address of the Windows Server node.Create an SSH connection to the Windows Server node using the internal IP address, and connect to port

`22`

through port`2022`

on your development computer. The default username for AKS nodes is*azureuser*. Accept the prompt to continue with the connection. You're then provided with the bash prompt of your Windows Server node:`ssh -o 'ProxyCommand ssh -p 2022 -W %h:%p azureuser@127.0.0.1' azureuser@10.224.0.62`

Sample output:

`The authenticity of host '10.224.0.62 (10.224.0.62)' can't be established. ECDSA key fingerprint is SHA256:1234567890abcdefghijklmnopqrstuvwxyzABCDEFG. Are you sure you want to continue connecting (yes/no)? yes`

Note

If you prefer to use password authentication, include the parameter

`-o PreferredAuthentications=password`

. For example:`ssh -o 'ProxyCommand ssh -p 2022 -W %h:%p azureuser@127.0.0.1' -o PreferredAuthentications=password azureuser@10.224.0.62`


## Use a host process container to access Windows node

Run the following script to create

`hostprocess.yaml`

. In the script, replace`AKSWINDOWSNODENAME`

with the AKS Windows node name.This specification uses the nanoserver base image. The base image doesn't have PowerShell, but because it runs as a host process container (HPC), PowerShell is available in the underlying VM.

`apiVersion: v1 kind: Pod metadata: labels: pod: hpc name: hpc spec: securityContext: windowsOptions: hostProcess: true runAsUserName: "NT AUTHORITY\\SYSTEM" hostNetwork: true containers: - name: hpc image: mcr.microsoft.com/windows/nanoserver:ltsc2022 # Use nanoserver:1809 for WS2019 command: - powershell.exe - -Command - "Start-Sleep 2147483" imagePullPolicy: IfNotPresent nodeSelector: kubernetes.io/os: windows kubernetes.io/hostname: AKSWINDOWSNODENAME tolerations: - effect: NoSchedule key: node.kubernetes.io/unschedulable operator: Exists - effect: NoSchedule key: node.kubernetes.io/network-unavailable operator: Exists - effect: NoExecute key: node.kubernetes.io/unreachable operator: Exists`

Run

`kubectl apply -f hostprocess.yaml`

to deploy the Windows HPC in the specified Windows node.Use

`kubectl exec -it [HPC-POD-NAME] -- powershell`

.You can run any PowerShell commands inside the HPC container to access the Windows node.


Note

You need to switch the root folder to `C:\`

inside the HPC container to access the files in the Windows node.

## SSH using Azure Bastion for Windows

If your Linux proxy node isn't reachable, using Azure Bastion as a proxy is an alternative. This method requires that you set up an Azure Bastion host for the virtual network in which the cluster resides. See [Connect with Azure Bastion](/en-us/azure/bastion/bastion-overview) for more details.

## SSH using private IPs from the AKS API

If you don't have access to the Kubernetes API, you can get access to properties such as `Node IP`

and `Node Name`

through the [AKS agent pool API ](/en-us/rest/api/aks/agent-pools/get#agentpool), (available on stable versions `07-01-2024`

or above) to connect to AKS nodes.

### Create an interactive shell connection to a node using the IP address

For convenience, AKS nodes are exposed on the cluster's virtual network through private IP addresses. However, you need to be in the cluster's virtual network to SSH into the node. If you don't already have an environment configured, you can use [Azure Bastion](/en-us/azure/bastion/bastion-connect-vm-ssh-linux) to establish a proxy from which you can SSH to cluster nodes. Make sure the Azure Bastion is deployed in the same virtual network as the cluster.

Obtain private IPs using the

`az aks machine list`

command, targeting all the VMs in a specific node pool with the`--nodepool-name`

flag.`az aks machine list --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name nodepool1 -o table`

The following example output shows the internal IP addresses of all the nodes in the node pool:

`Name Ip Family --------------------------------- ----------- ----------- aks-nodepool1-33555069-vmss000000 10.224.0.5 IPv4 aks-nodepool1-33555069-vmss000001 10.224.0.6 IPv4 aks-nodepool1-33555069-vmss000002 10.224.0.4 IPv4`

To target a specific node inside the node pool, use the

`--machine-name`

flag:`az aks machine show --cluster-name myAKScluster --nodepool-name nodepool1 -g myResourceGroup --machine-name aks-nodepool1-33555069-vmss000000 -o table`

The following example output shows the internal IP address of all the specified node:

`Name Ip Family --------------------------------- ----------- ----------- aks-nodepool1-33555069-vmss000000 10.224.0.5 IPv4`

SSH to the node using the private IP address you obtained in the previous step. This step is applicable for Linux machines only. For Windows machines, see

[Connect with Azure Bastion](/en-us/azure/bastion/bastion-overview).`ssh -i /path/to/private_key.pem azureuser@10.224.0.33`


## Next steps

If you need more troubleshooting data, you can [view the kubelet logs](kubelet-logs) or [view the Kubernetes control plane logs](monitor-aks-reference#resource-logs).

To learn about managing your SSH keys, see [Manage SSH configuration](manage-ssh-node-access).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-access -->

# Connect to Azure Kubernetes Service (AKS) cluster nodes for maintenance or troubleshooting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Throughout the lifecycle of your Azure Kubernetes Service (AKS) cluster, you eventually need to directly access an AKS node. This access could be for maintenance, log collection, or troubleshooting operations.

You access a node through authentication, which methods vary depending on your Node OS and method of connection. You securely authenticate against AKS Linux and Windows nodes through two options discussed in this article. One requires that you have Kubernetes API access, and the other is through the AKS ARM API, which provides direct private IP information. For security reasons, AKS nodes aren't exposed to the internet. Instead, to connect directly to any AKS nodes, you need to use either `kubectl debug`

or the host's private IP address.

## Access nodes using the Kubernetes API

This method requires usage of `kubectl debug`

command.

### Before you begin

This guide shows you how to create a connection to an AKS node and update the SSH key of your AKS cluster. To follow along the steps, you need to use Azure CLI that supports version 2.0.64 or later. Run `az --version`

to check the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Complete these steps if you don't have an SSH key. Create an SSH key depending on your Node OS Image, for [macOS and Linux](/en-us/azure/virtual-machines/linux/mac-create-ssh-keys), or [Windows](/en-us/azure/virtual-machines/linux/ssh-from-windows). Make sure you save the key pair in the OpenSSH format, avoid unsupported formats such as `.ppk`

. Next, refer to [Manage SSH configuration](manage-ssh-node-access) to add the key to your cluster.

### Linux and macOS

Linux and macOS users can access their node using `kubectl debug`

or their private IP Address. Windows users should skip to the Windows Server Proxy section for a workaround to SSH via proxy.

#### Connect using kubectl debug

To create an interactive shell connection, use the `kubectl debug`

command to run a privileged container on your node.

To list your nodes, use the

`kubectl get nodes`

command:`kubectl get nodes -o wide`

Sample output:

`NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE aks-nodepool1-37663765-vmss000000 Ready agent 166m v1.25.6 10.224.0.33 <none> Ubuntu 22.04.2 LTS aks-nodepool1-37663765-vmss000001 Ready agent 166m v1.25.6 10.224.0.4 <none> Ubuntu 22.04.2 LTS aksnpwin000000 Ready agent 160m v1.25.6 10.224.0.62 <none> Windows Server 2022 Datacenter`

Use the

`kubectl debug`

command to start a privileged container on your node and connect to it.`kubectl debug node/aks-nodepool1-37663765-vmss000000 -it --image=mcr.microsoft.com/cbl-mariner/busybox:2.0`

Sample output:

`Creating debugging pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx with container debugger on node aks-nodepool1-37663765-vmss000000. If you don't see a command prompt, try pressing enter. root@aks-nodepool1-37663765-vmss000000:/#`

You now have access to the node through a privileged container as a debugging pod.

Note

You can interact with the node session by running

`chroot /host`

from the privileged container.

#### Exit kubectl debug mode

When you're done with your node, enter the `exit`

command to end the interactive shell session. After the interactive container session closes, delete the debugging pod used with `kubectl delete pod`

.

```
kubectl delete pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx
```


### Windows Server proxy connection for SSH

Follow these steps as a workaround to connect with SSH on a Windows Server node.

#### Create a proxy server

At this time, you can't connect to a Windows Server node directly by using `kubectl debug`

. Instead, you need to first connect to another node in the cluster with `kubectl`

, then connect to the Windows Server node from that node using SSH.

To connect to another node in the cluster, use the `kubectl debug`

command. For more information, follow the above steps in the kubectl section. Create an SSH connection to the Windows Server node from another node using the SSH keys provided when you created the AKS cluster and the internal IP address of the Windows Server node.

Important

The following steps for creating the SSH connection to the Windows Server node from another node can only be used if you created your AKS cluster using the Azure CLI with the `--generate-ssh-keys`

parameter. If you want to use your own SSH keys instead, you can use the `az aks update`

to manage SSH keys on an existing AKS cluster. For more information, see [manage SSH node access](manage-ssh-node-access).

Note

If your Linux proxy node is down or unresponsive, use the [Azure Bastion](/en-us/azure/bastion/bastion-overview) method to connect instead.

Use the

`kubectl debug`

command to start a privileged container on your proxy (Linux) node and connect to it.`kubectl debug node/aks-nodepool1-37663765-vmss000000 -it --image=mcr.microsoft.com/cbl-mariner/busybox:2.0`

Sample output:

`Creating debugging pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx with container debugger on node aks-nodepool1-37663765-vmss000000. If you don't see a command prompt, try pressing enter. root@aks-nodepool1-37663765-vmss000000:/#`

Open a new terminal window and use the

`kubectl get pods`

command to get the name of the pod started by`kubectl debug`

.`kubectl get pods`

Sample output:

`NAME READY STATUS RESTARTS AGE node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx 1/1 Running 0 21s`

In the sample output,

*node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx*is the name of the pod started by`kubectl debug`

.Use the

`kubectl port-forward`

command to open a connection to the deployed pod:`kubectl port-forward node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx 2022:22`

Sample output:

`Forwarding from 127.0.0.1:2022 -> 22 Forwarding from [::1]:2022 -> 22`

The previous example begins forwarding network traffic from port

`2022`

on your development computer to port`22`

on the deployed pod. When using`kubectl port-forward`

to open a connection and forward network traffic, the connection remains open until you stop the`kubectl port-forward`

command.Open a new terminal and run the command

`kubectl get nodes`

to show the internal IP address of the Windows Server node:`kubectl get no -o custom-columns=NAME:metadata.name,'INTERNAL_IP:status.addresses[?(@.type == \"InternalIP\")].address'`

Sample output:

`NAME INTERNAL_IP aks-nodepool1-19409214-vmss000003 10.224.0.8`

In the previous example,

*10.224.0.62*is the internal IP address of the Windows Server node.Create an SSH connection to the Windows Server node using the internal IP address, and connect to port

`22`

through port`2022`

on your development computer. The default username for AKS nodes is*azureuser*. Accept the prompt to continue with the connection. You're then provided with the bash prompt of your Windows Server node:`ssh -o 'ProxyCommand ssh -p 2022 -W %h:%p azureuser@127.0.0.1' azureuser@10.224.0.62`

Sample output:

`The authenticity of host '10.224.0.62 (10.224.0.62)' can't be established. ECDSA key fingerprint is SHA256:1234567890abcdefghijklmnopqrstuvwxyzABCDEFG. Are you sure you want to continue connecting (yes/no)? yes`

Note

If you prefer to use password authentication, include the parameter

`-o PreferredAuthentications=password`

. For example:`ssh -o 'ProxyCommand ssh -p 2022 -W %h:%p azureuser@127.0.0.1' -o PreferredAuthentications=password azureuser@10.224.0.62`


## Use a host process container to access Windows node

Run the following script to create

`hostprocess.yaml`

. In the script, replace`AKSWINDOWSNODENAME`

with the AKS Windows node name.This specification uses the nanoserver base image. The base image doesn't have PowerShell, but because it runs as a host process container (HPC), PowerShell is available in the underlying VM.

`apiVersion: v1 kind: Pod metadata: labels: pod: hpc name: hpc spec: securityContext: windowsOptions: hostProcess: true runAsUserName: "NT AUTHORITY\\SYSTEM" hostNetwork: true containers: - name: hpc image: mcr.microsoft.com/windows/nanoserver:ltsc2022 # Use nanoserver:1809 for WS2019 command: - powershell.exe - -Command - "Start-Sleep 2147483" imagePullPolicy: IfNotPresent nodeSelector: kubernetes.io/os: windows kubernetes.io/hostname: AKSWINDOWSNODENAME tolerations: - effect: NoSchedule key: node.kubernetes.io/unschedulable operator: Exists - effect: NoSchedule key: node.kubernetes.io/network-unavailable operator: Exists - effect: NoExecute key: node.kubernetes.io/unreachable operator: Exists`

Run

`kubectl apply -f hostprocess.yaml`

to deploy the Windows HPC in the specified Windows node.Use

`kubectl exec -it [HPC-POD-NAME] -- powershell`

.You can run any PowerShell commands inside the HPC container to access the Windows node.


Note

You need to switch the root folder to `C:\`

inside the HPC container to access the files in the Windows node.

## SSH using Azure Bastion for Windows

If your Linux proxy node isn't reachable, using Azure Bastion as a proxy is an alternative. This method requires that you set up an Azure Bastion host for the virtual network in which the cluster resides. See [Connect with Azure Bastion](/en-us/azure/bastion/bastion-overview) for more details.

## SSH using private IPs from the AKS API

If you don't have access to the Kubernetes API, you can get access to properties such as `Node IP`

and `Node Name`

through the [AKS agent pool API ](/en-us/rest/api/aks/agent-pools/get#agentpool), (available on stable versions `07-01-2024`

or above) to connect to AKS nodes.

### Create an interactive shell connection to a node using the IP address

For convenience, AKS nodes are exposed on the cluster's virtual network through private IP addresses. However, you need to be in the cluster's virtual network to SSH into the node. If you don't already have an environment configured, you can use [Azure Bastion](/en-us/azure/bastion/bastion-connect-vm-ssh-linux) to establish a proxy from which you can SSH to cluster nodes. Make sure the Azure Bastion is deployed in the same virtual network as the cluster.

Obtain private IPs using the

`az aks machine list`

command, targeting all the VMs in a specific node pool with the`--nodepool-name`

flag.`az aks machine list --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name nodepool1 -o table`

The following example output shows the internal IP addresses of all the nodes in the node pool:

`Name Ip Family --------------------------------- ----------- ----------- aks-nodepool1-33555069-vmss000000 10.224.0.5 IPv4 aks-nodepool1-33555069-vmss000001 10.224.0.6 IPv4 aks-nodepool1-33555069-vmss000002 10.224.0.4 IPv4`

To target a specific node inside the node pool, use the

`--machine-name`

flag:`az aks machine show --cluster-name myAKScluster --nodepool-name nodepool1 -g myResourceGroup --machine-name aks-nodepool1-33555069-vmss000000 -o table`

The following example output shows the internal IP address of all the specified node:

`Name Ip Family --------------------------------- ----------- ----------- aks-nodepool1-33555069-vmss000000 10.224.0.5 IPv4`

SSH to the node using the private IP address you obtained in the previous step. This step is applicable for Linux machines only. For Windows machines, see

[Connect with Azure Bastion](/en-us/azure/bastion/bastion-overview).`ssh -i /path/to/private_key.pem azureuser@10.224.0.33`


## Next steps

If you need more troubleshooting data, you can [view the kubelet logs](kubelet-logs) or [view the Kubernetes control plane logs](monitor-aks-reference#resource-logs).

To learn about managing your SSH keys, see [Manage SSH configuration](manage-ssh-node-access).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-vulnerability-management -->

# Vulnerability management for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Vulnerability management involves detecting, assessing, mitigating, and reporting on any security vulnerabilities that exist in an organization's systems and software. Vulnerability management is a shared responsibility between you and Microsoft.

This article describes how Microsoft manages security vulnerabilities and security updates (also referred to as patches), for Azure Kubernetes Service (AKS) clusters.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## How vulnerabilities are discovered

Microsoft identifies and patches vulnerabilities and missing security updates for the following components:

AKS Container Images

Ubuntu operating system 18.04 and 22.04 worker nodes: Canonical provides Microsoft with OS builds that have all available security updates applied.

Windows Server 2022 OS worker nodes: The Windows Server operating system is patched on the second Tuesday of every month. SLAs should be the same as per their support contract and severity.

Azure Linux OS Nodes: Azure Linux provides AKS with OS builds that have all available security updates applied.


## AKS Container Images

While the [Cloud Native Computing Foundation](https://www.cncf.io/) (CNCF) owns and maintains most of the code AKS runs, Microsoft takes responsibility for building the open-source packages we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, as well as control over the binaries in container images. Having responsibility for building the open-source packages deployed on AKS enables us to establish a software supply chain over the binary, and to patch the software as needed.

Microsoft is active in the broader Kubernetes ecosystem to help build the future of cloud-native compute in the wider CNCF community. This work not only ensures the quality of every Kubernetes release for the world, but also enables AKS quickly get new Kubernetes releases out into production for several years. In some cases, ahead of other cloud providers by several months. Microsoft collaborates with other industry partners in the Kubernetes security organization. For example, the Security Response Committee (SRC) receives, prioritizes, and patches embargoed security vulnerabilities before they're announced to the public. This commitment ensures Kubernetes is secure for everyone, and enables AKS to patch and respond to vulnerabilities faster to keep our customers safe. In addition to Kubernetes, Microsoft has signed up to receive pre-release notifications for software vulnerabilities for products such as Envoy, container runtimes, and many other open-source projects.

Microsoft scans container images using static analysis to discover vulnerabilities and missing updates in Kubernetes and Microsoft-managed containers. If fixes are available, the scanner automatically begins the update and release process.

In addition to automated scanning, Microsoft discovers and updates vulnerabilities unknown to scanners in the following ways:

Microsoft performs its own audits, penetration testing, and vulnerability discovery across all AKS platforms. Specialized teams inside Microsoft and trusted third-party security vendors conduct their own attack research.

Microsoft actively engages with the security research community through multiple vulnerability reward programs. A dedicated

[Microsoft Azure Bounty program](https://www.microsoft.com/msrc/bounty-microsoft-azure)provides significant bounties for the best cloud vulnerability found each year.Microsoft collaborates with other industry and open source software partners who share vulnerabilities, security research, and updates before the public release of the vulnerability. The goal of this collaboration is to update large pieces of Internet infrastructure before the vulnerability is announced to the public. In some cases, Microsoft contributes vulnerabilities found to this community.

Microsoft's security collaboration happens on many levels. Sometimes it occurs formally through programs where organizations sign up to receive pre-release notifications about software vulnerabilities for products such as Kubernetes and Docker. Collaboration also happens informally due to our engagement with many open source projects such as the Linux kernel, container runtimes, virtualization technology, and others.


## Worker Nodes

### Linux nodes

The nightly canonical OS security updates are turned off by default in AKS. In order to enable them explicitly, use the `unmanaged`

[channel](node-image-upgrade).

If you are using the `unmanaged`

[channel](node-image-upgrade), then nightly canonical security updates are applied to the OS on the node. The node image used to create nodes for your cluster remains unchanged. If a new Linux node is added to your cluster, the original image is used to create the node. This new node receives all the security and kernel updates available during the automatic assessment performed every night, but remains unpatched until all checks and restarts are complete. You can use node image upgrade to check for and update node images used by your cluster. For more information on node image upgrade, see [Azure Kubernetes Service (AKS) node image upgrade](node-image-upgrade).

For AKS clusters using a [channel](node-image-upgrade) other than `unmanaged`

, the unattended upgrade process is disabled.

### Windows Server nodes

For Windows Server nodes, Windows Update doesn't automatically run and apply the latest updates. Schedule Windows Server node pool upgrades in your AKS cluster around the regular Windows Update release cycle and your own update management process. This upgrade process creates nodes that run the latest Windows Server image and patches, then removes the older nodes. For more information on this process, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

## How vulnerabilities are classified

Microsoft makes large investments in security hardening the entire stack, including the OS, container, Kubernetes, and network layers, in addition to setting good defaults and providing security-hardened configurations and managed components. Combined, these efforts help to reduce the impact and likelihood of vulnerabilities.

The AKS team classifies vulnerabilities according to the Kubernetes vulnerability scoring system. Classifications consider many factors including AKS configuration and security hardening. As a result of this approach, and the investments AKS make in security, AKS vulnerability classifications might differ from other classification sources.

The following table describes vulnerability severity categories:

| Severity | Description |
|---|---|
| Critical | A vulnerability easily exploitable in all clusters by an unauthenticated remote attacker that leads to full system compromise. |
| High | A vulnerability easily exploitable for many clusters that leads to loss of confidentiality, integrity, or availability. |
| Medium | A vulnerability exploitable for some clusters where loss of confidentiality, integrity, or availability is limited by common configurations, difficulty of the exploit itself, required access, or user interaction. |
| Low | All other vulnerabilities. Exploitation is unlikely or consequences of exploitation are limited. |

## How vulnerabilities are updated

AKS patches Common Vulnerabilities and Exposures (CVEs) that have a *vendor fix* every week. Any CVEs without a fix are waiting on a vendor fix before they can be remediated. The fixed container images are cached in the next corresponding virtual hard disk (VHD) build, which also contains the updated Ubuntu/Azure Linux/Windows patched CVEs. As long as you're running the updated VHD, you shouldn't be running any container image CVEs with a vendor fix that is over 30 days old.

For the OS-based vulnerabilities in the VHD, AKS also relies on node image vhd updates by default, so any security updates will come with weekly node image releases. Unattended upgrades is disabled unless you switch to unmanaged which is not recommended as its release is global.

## Update release timelines

Microsoft's goal is to mitigate detected vulnerabilities within a time period appropriate for the risks they represent. The [Microsoft Azure FedRAMP High](/en-us/azure/azure-government/compliance/azure-services-in-fedramp-auditscope#azure-government-services-by-audit-scope) Provisional Authorization to Operate (P-ATO) includes AKS in audit scope and has been authorized. FedRAMP Continuous Monitoring Strategy Guide and the FedRAMP Low, Moderate, and High Security Control baselines requires remediation of known vulnerabilities within a specific time period according to their severity level. As specified in FedRAMP RA-5d.

## How vulnerabilities and updates are communicated

In general, Microsoft doesn't broadly communicate the release of new patch versions for AKS. However, Microsoft constantly monitors and validates available CVE patches to support them in AKS in a timely manner. If a critical patch is found or user action is required, Microsoft [posts and updates CVE issue details on GitHub](https://github.com/Azure/AKS/issues?q=is%3Aissue+is%3Aopen+cve).

## Security Reporting

You can report a security issue to the Microsoft Security Response Center (MSRC), by [creating a vulnerability report](https://aka.ms/opensource/security/create-report).

If you prefer to submit a report without logging in to the tool, send email to [secure@microsoft.com](mailto:secure@microsoft.com). If possible, encrypt your message with our PGP key by downloading it from the [Microsoft Security Response Center PGP Key page](https://aka.ms/opensource/security/pgpkey).

You should receive a response within 24 hours. If for some reason you don't, follow up with an email to ensure we received your original message. For more information, go to the [Microsoft Security Response Center](https://aka.ms/opensource/security/msrc).

Include the following requested information (as much as you can provide) to help us better understand the nature and scope of the possible issue:

- Type of issue (for example, buffer overflow, SQL injection, cross-site scripting, etc.)
- Full paths of source file(s) related to the manifestation of the issue
- The location of the affected source code (tag/branch/commit or direct URL)
- Any special configuration required to reproduce the issue
- Step-by-step instructions to reproduce the issue
- Proof-of-concept or exploit code (if possible)
- Impact of the issue, including how an attacker might exploit the issue

This information helps us triage your reported security issue quicker.

If you're reporting for a bug bounty, more complete reports can contribute to a higher bounty award. For more information about our active programs, see [Microsoft Bug Bounty Program](https://aka.ms/opensource/security/bounty).

### Policy

Microsoft follows the principle of [Coordinated Vulnerability Disclosure](https://aka.ms/opensource/security/cvd).

## Next steps

See the overview about [Upgrading Azure Kubernetes Service clusters and node pools](upgrade).
