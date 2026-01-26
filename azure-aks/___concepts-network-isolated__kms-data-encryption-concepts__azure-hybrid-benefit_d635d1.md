---
merged_at: 2026-01-26T23:04:06.000540
merged_files: 2
---


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
