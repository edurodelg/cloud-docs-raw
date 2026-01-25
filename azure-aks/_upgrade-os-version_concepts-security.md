---
merged_at: 2026-01-25T12:06:27.859406
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: upgrade-os-version.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/upgrade-os-version -->

# Upgrade operating system (OS) versions in AKS

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes OS versions available for Azure Kubernetes Service (AKS) nodes, and best practices for testing and upgrading your OS version.

Caution

In this article, there are references to Ubuntu and Azure Linux OS versions that are being deprecated for AKS:

- Starting on
**March 17, 2027**, AKS will no longer support Ubuntu 20.04. Existing node images will be deleted and AKS will no longer provide security updates. You'll no longer be able to scale your node pools. Migrate to a supported Ubuntu version by[upgrading your node pools](upgrade-aks-cluster)to Kubernetes version 1.34+. For more information on this retirement, see[Retirement: Ubuntu 20.04 node pools on AKS](https://github.com/Azure/AKS/issues/4874). - As of
**November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the[202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning**March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by[upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster)to a supported Kubernetes version or migrating to[osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see[[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Supported OS versions

Each [node image](node-images) corresponds to an OS version, which you can specify using OS SKU. You can specify the following parameters when creating clusters and node pools:

**--os-type**: OS type, including Linux or Windows.*You can't specify the Windows OS type during cluster creation or update.***--os-sku**: Used to specify OS version or OS variant.*You can't specify the Windows OS SKU during cluster creation or update.*For more information for supported OS SKU options, see[Azure AKS CLI](/en-us/cli/azure/aks#az-aks-create)or[API](/en-us/rest/api/aks/agent-pools/create-or-update#ossku).**--kubernetes-version**: Version of Kubernetes to use for creating the node pool or cluster.


Best practice guidanceThe default OS version is the most recent validated version.


- For Ubuntu, we recommend creating clusters and node pools while specifying
`--os-type Linux`

and`--os-sku Ubuntu`

. This will automatically update you to the latest default Ubuntu version based on your Kubernetes version.- For Azure Linux, we recommend creating clusters and node pools while specifying
`--os-type Linux`

and`--os-sku AzureLinux`

. This will automatically update you to the latest default Azure Linux version based on your Kubernetes version.- For Windows, we recommend creating node pools while specifying
`--os-type Windows`

and`--os-sku Windows2022`

. You need to manually update node pools to the next OS version when it's released.

| OS type | OS SKU | Supported Kubernetes versions | Default versioning |
|---|---|---|---|
| Linux | Ubuntu | This OS SKU is supported in all Kubernetes versions. | OS version for this OS SKU changes based on your Kubernetes version. Ubuntu 22.04 is default for Kubernetes versions 1.25 to 1.34. Ubuntu 24.04 is default for Kubernetes versions 1.35+. |
| Linux | Ubuntu2404 | This OS SKU will only be supported in Kubernetes 1.32 to 1.38. | We recommend this versioned OS SKU if you want to migrate to the new OS version without upgrading your Kubernetes version. Ubuntu 24.04 is default when using `--os-sku Ubuntu` in Kubernetes versions 1.35+. |
| Linux | Ubuntu2204 | This OS SKU is supported in Kubernetes versions 1.25 to 1.36. | We recommend this versioned OS SKU if you need to roll back to Ubuntu 22.04. Ubuntu 22.04 is default when using `--os-sku Ubuntu` in Kubernetes versions 1.25 to 1.35. |
| Linux | AzureLinux | This OS SKU is supported in all Kubernetes versions. | OS version for this OS SKU changes based on your Kubernetes version. Azure Linux 2.0 is default for Kubernetes version 1.27 to 1.31. Azure Linux 3.0 is default for Kubernetes version 1.32+. When the `AzureLinuxV3Preview` feature flag is enabled on AKS 1.31, `--os-sku AzureLinux` defaults to 3.0. |
| Linux | AzureLinux3 | This OS SKU is supported in Kubernetes 1.28 to 1.36. | We recommend this OS SKU if you want to test out the new OS version without upgrading your Kubernetes version. You can also use this OS SKU to migrate from Azure Linux 2.0 to Azure Linux 3.0. |
| Linux | AzureLinuxOSGuard | This OS SKU is supported in Kubernetes versions 1.32 and above. | Azure Linux with OS Guard versions are upgraded through node image upgrades. For more information, see
|

[Flatcar Container Linux for AKS](flatcar-container-linux-for-aks).## Migrate to a new OS version

When a new OS version releases on AKS, it's initially supported in preview. After testing in preview for a few months, AKS makes the new OS version generally available (GA) and then updates the default OS SKU (`Ubuntu`

or `AzureLinux`

) to the latest GA OS version. This default update occurs with a new Kubernetes version release.

We recommend testing your nonproduction workloads with the new OS version when it becomes available in preview. In order to access preview functions, make sure you have the preview extension installed. You can install the extension using the `az extension add --name aks-preview`

command.

There are two ways to migrate to a new OS version:

**Default OS SKU**: If you're using a default OS SKU such as`Ubuntu`

or`AzureLinux`

, you automatically get the latest GA version when you[upgrade your Kubernetes version](manage-node-pools). There are no manual changes required to migrate to a new OS version.**Versioned OS SKU**: If you're using a versioned OS SKU such as`Ubuntu2404`

,`AzureLinux3`

, or`Windows2025`

, you need to manually migrate to a new OS version to avoid blocked Kubernetes upgrades. If you're using a Linux OS, you can update the OS SKU on an existing node pool to manually migrate.

### Update OS SKU on an existing node pool

Update the `os-sku`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. In cases where there's a new OS version available in preview, this functionality allows you to migrate your node pool to the new OS version without needing to upgrade your Kubernetes version.

Note

The following values aren't supported for node pool update command:

`--os-sku Windows2019`

`--os-sku Windows2022`

`--os-sku Windows2025`


Instead, you need to add node pools to your cluster with the corresponding `--os-sku`

you intend to use.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku Ubuntu \
--name $NODE_POOL_NAME \
--node-count 1
```


You can use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command to migrate between any supported Linux

`os-sku`

. The command might fail if the target OS doesn't have a supported node image for your Kubernetes version, VM size, or FIPS enablement.#### Migrate to Ubuntu 24.04

Ubuntu 24.04 is the default for `--os-sku Ubuntu`

in Kubernetes versions 1.35+. You can also use Ubuntu 24.04 by specifying `--os-sku Ubuntu2404`

.

Note

Keep the following information in mind when migrating to `--os-sku Ubuntu2404`

:

[FIPS](enable-fips-nodes)is not supported.- Ubuntu 24.04 is supported in Kubernetes versions 1.32 to 1.38.
- You need to update your OS SKU to a supported OS option before upgrading your Kubernetes version to 1.39+.
`--os-sku Ubuntu2404`

is an option and is intended for testing the new OS Linux version without requiring you to upgrade your Kubernetes version. - You need the preview Azure CLI version 18.0.0b5 or later for
*preview*and version 2.82.0 for*GA*installed and configured. To find your CLI version, run`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Update to `--os-sku Ubuntu2404`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku Ubuntu2404 \
--kubernetes-version 1.32.0 \
--name $NODE_POOL_NAME \
--node-count 1
```


#### Migrate to Azure Linux 3.0

Azure Linux 3.0 is the default for `--os-sku AzureLinux`

in Kubernetes versions 1.32 to 1.36. You can also use Azure Linux 3.0 by specifying `--os-sku AzureLinux3`

.

Note

Keep the following information in mind when migrating to `--os-sku AzureLinux3`

:

`--os-sku AzureLinux3`

is supported in Kubernetes versions 1.28 to 1.36.`--os-sku AzureLinux3`

is intended for migrating to Azure Linux 3.0 without upgrading your Kubernetes version. You need to update your OS SKU to a supported OS option before upgrading your Kubernetes version to 1.37+.- You need the Azure CLI version 18.0.0b36 or later for
*preview*and version 2.78.0 or later for*GA*installed and configured. To find your CLI version, run`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Update to `--os-sku AzureLinux3`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku AzureLinux3 \
--kubernetes-version 1.30.0 \
--name $NODE_POOL_NAME \
--node-count 1
```


## Roll back your OS version

In Kubernetes versions where multiple OS versions are supported, you can use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command to roll back to a previous OS version.

You might want to roll back your OS version in the following scenarios:

- If you're testing a new OS version and you run into any issues.
- Once you upgrade to a Kubernetes version that supports the new OS version as default, you might want to roll back to the default
`Ubuntu`

or`AzureLinux`

OS SKU. This allows you to get future OS versions as a part of your Kubernetes upgrades instead of requiring a node pool update.

### Roll back your OS version to the default OS SKU

You can use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command to update the

`os-sku`

on an existing node pool. In cases where there's a previous OS version supported in your Kubernetes version, this functionality can allow you to roll back your OS version.Note

The following values aren't supported for node pool update command:

`--os-sku Windows2019`

`--os-sku Windows2022`

`--os-sku Windows2025`


Instead, you need to add node pools to your cluster with the corresponding `--os-sku`

you intend to use.

| OS SKU | Default OS version |
|---|---|
| Ubuntu | When you have OS SKU `Ubuntu` , Ubuntu 22.04 is the default OS version if your Kubernetes version is 1.25 to 1.34. Ubuntu 24.04 is the default for Ubuntu in Kubernetes 1.35 to 1.37. |
| AzureLinux | When you have OS SKU `AzureLinux` , Azure Linux 2.0 is the default for AzureLinux in Kubernetes 1.26 to 1.31. Azure Linux 3.0 is the default for AzureLinux in Kubernetes 1.32 to 1.36. |

#### Update your OS SKU to Ubuntu on an existing node pool

When updating your node pool to use OS SKU `Ubuntu`

, you'll get the default OS version based on your Kubernetes version. This might trigger an automatic reimage if the OS version changes during the node pool update command.

Update to `--os-sku Ubuntu`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku Ubuntu \
--name $NODE_POOL_NAME \
--node-count 1
```


You can use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command to migrate between any supported Linux

`os-sku`

. The command might fail if the target OS doesn't have a supported node image for your Kubernetes version, VM size, or FIPS enablement.#### Update your OS SKU to Azure Linux on an existing node pool

When updating your node pool to use OS SKU `AzureLinux`

, you'll get the default OS version based on your Kubernetes version. This might trigger an automatic reimage if the OS version changes during the node pool update command.

Update to `--os-sku AzureLinux`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku AzureLinux \
--name $NODE_POOL_NAME \
--node-count 1
```


### Roll back to Ubuntu 22.04

Note

Keep the following information in mind when migrating to `--os-sku Ubuntu2204`

:

[FIPS](enable-fips-nodes)and[CVM](use-cvm)aren't supported.- Ubuntu 22.04 is supported in Kubernetes versions 1.25 to 1.35.
`--os-sku Ubuntu2204`

is intended for roll back to Ubuntu 22.04 on your current Kubernetes version. You need to update your OS SKU to a supported OS option to upgrade your Kubernetes version to 1.36 and above.

Roll back to `--os-sku Ubuntu2204`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku Ubuntu2204 \
--kubernetes-version 1.32.0 \
--name $NODE_POOL_NAME \
--node-count 1
```


## Next steps

To learn more about node images, node pool upgrades, and node configurations on AKS, see the following resources:

- To learn about nodes and node configurations, see
[AKS core concepts](core-aks-concepts). - Configure
[automatic node image upgrades](auto-upgrade-node-os-image)and schedule them using[planned maintenance](planned-maintenance). - Apply
[custom node configurations](custom-node-configuration)to modify OS or kubelet settings. - For information about the latest node images, see the
[AKS release notes](https://github.com/Azure/AKS/releases). [Automatically apply cluster and node pool upgrades with GitHub Actions](node-upgrade-github-actions).- Learn about upgrading best practices with
[AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).


---

<!-- DOCUMENTO FUSIONADO: concepts-security.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-security -->

# Security concepts for applications and clusters in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Container security protects the entire end-to-end pipeline from build to the application workloads running in Azure Kubernetes Service (AKS).

The Secure Supply Chain includes the build environment and registry.

Kubernetes includes security components, such as *pod security standards* and *Secrets*. Azure includes components like Active Directory, Microsoft Defender for Containers, Azure Policy, Azure Key Vault, network security groups, and orchestrated cluster upgrades. AKS combines these security components to:

- Provide a complete authentication and authorization story.
- Apply AKS Built-in Azure Policy to secure your applications.
- End-to-End insight from build through your application with Microsoft Defender for Containers.
- Keep your AKS cluster running the latest OS security updates and Kubernetes releases.
- Provide secure pod traffic and access to sensitive credentials.

This article introduces the core concepts that secure your applications in AKS.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Build Security

As the entry point for the Supply Chain, it's important to conduct static analysis of image builds before they're promoted down the pipeline. This includes vulnerability and compliance assessment. It's not about failing a build because it has a vulnerability, as that breaks development. It's about looking at the **Vendor Status** to segment based on vulnerabilities that are actionable by the development teams. Also use **Grace Periods** to allow developers time to remediate identified issues.

## Registry Security

Assessing the vulnerability state of the image in the Registry detects drift and also catches images that didn't come from your build environment. Use [Notary V2](https://github.com/notaryproject/notaryproject) to attach signatures to your images to ensure deployments are coming from a trusted location.

## Cluster security

In AKS, the Kubernetes master components are part of the managed service provided, managed, and maintained by Microsoft. Each AKS cluster has its own single-tenanted, dedicated Kubernetes master to provide the API Server, Scheduler, etc. For more information, see [Vulnerability management for Azure Kubernetes Service](concepts-vulnerability-management).

By default, the Kubernetes API server uses a public IP address and a fully qualified domain name (FQDN). You can limit access to the API server endpoint using [authorized IP ranges](api-server-authorized-ip-ranges). You can also create a fully [private cluster](private-clusters) to limit API server access to your virtual network.

You can control access to the API server using Kubernetes role-based access control (Kubernetes RBAC) and Azure RBAC. For more information, see [Microsoft Entra integration with AKS](managed-azure-ad).

## Node security

AKS nodes are Azure virtual machines (VMs) that you manage and maintain.

- Linux nodes run optimized versions of Ubuntu or Azure Linux.
- Windows Server nodes run an optimized Windows Server release using the
`containerd`

container runtime.

When an AKS cluster is created or scaled up, the nodes are automatically deployed with the latest OS security updates and configurations.

Note

AKS clusters running:

- Kubernetes version 1.19 and higher - Linux node pools use
`containerd`

as its container runtime. Windows Server 2019 and Windows Server 2022 node pools use`containerd`

as its container runtime. For more information, see[Add a Windows Server node pool with](create-node-pools).`containerd`

- Kubernetes version 1.19 and earlier - Linux node pools use Docker as its container runtime.

For more information about the security upgrade process for Linux and Windows worker nodes, see [Security patching nodes](concepts-vulnerability-management#worker-nodes).

AKS clusters running Azure Generation 2 VMs include support for [Trusted Launch](use-trusted-launch). This feature protects against advanced and persistent attack techniques by combining technologies that you can enable independently, like secure boot and a virtualized version of the trusted platform module (vTPM). Administrators can deploy AKS worker nodes with verified and signed bootloaders, OS kernels, and drivers to ensure integrity of the entire boot chain of the underlying VM.

### Container and security optimized OS options

AKS released support for two new optimized Linux OS options. [Azure Linux OS Guard (preview)](https://aka.ms/aks/azure-linux-os-guard) is Microsoft-created and optimized for Azure. OS Guard is built on top of Azure Linux with specialized configuration to support containerized workloads with security optimizations. [Flatcar Container Linux for AKS (preview)](https://aka.ms/aks/flatcar) is a CNCF-based vendor-neutral container-optimized immutable OS, best suited for running on multicloud and on-premises environments. These OS options provide increased security when compared to other Linux OS options, such as:

- Both Azure Linux OS Guard and Flatcar Container Linux for AKS have an immutable operating system that you can't modify at runtime. All OS binaries, libraries and static configuration are read-only, and the bit-for-bit integrity is often cryptographically protected. These special purpose operating systems ship as self-contained images and come without any kind of package management or other traditional means of altering the OS. User workloads run in isolated environments like containers, sandboxed from the OS.
- Both Azure Linux OS Guard and Flatcar Container Linux for AKS use SELinux for Mandatory Access Control.
- Azure Linux OS Guard enforces
[FIPS](enable-fips-nodes)and[Trusted Launch](use-trusted-launch)enablement, providing improved compliance and protection against advanced and persistent attacks by combining secure boot and virtualized version of trusted platform module (vTPM).

When deciding between which container-optimized OS options to use, AKS recommends the following:

- Use
if you're looking for a vendor neutral immutable OS with cross-cloud support.**Flatcar Container Linux for AKS (preview)** - Use
if you're looking for an enterprise-ready immutable OS, recommended by Microsoft.**Azure Linux OS Guard (preview)** - Use
[Ubuntu](https://aka.ms/aks/supported-ubuntu-versions)if you're looking for a vendor neutral, general purpose OS with cross-cloud support. - Use
[Azure Linux](https://aka.ms/aks/use-azure-linux)if you're looking for an enterprise-ready, general purpose OS, recommended by Microsoft.


### Node authorization

Node authorization is a special-purpose authorization mode that specifically authorizes kubelet API requests to protect against East-West attacks. Node authorization is enabled by default on AKS 1.24 + clusters.

### Node deployment

Nodes are deployed onto a private virtual network subnet, with no public IP addresses assigned. For troubleshooting and management purposes, SSH is enabled by default and only accessible using the internal IP address. Disabling SSH during cluster and node pool creation, or for an existing cluster or node pool, is in preview. See [Manage SSH access](manage-ssh-node-access) for more information.

### Node storage

To provide storage, the nodes use Azure Managed Disks. For most VM node sizes, Azure Managed Disks are Premium disks backed by high-performance SSDs. The data stored on managed disks is automatically encrypted at rest within the Azure platform. To improve redundancy, Azure Managed Disks are securely replicated within the Azure datacenter.

### Hostile multitenant workloads

Currently, Kubernetes environments aren't safe for hostile multitenant usage. Extra security features, like *Pod Security Policies* or Kubernetes RBAC for nodes, efficiently block exploits. For true security when running hostile multitenant workloads, only trust a hypervisor. The security domain for Kubernetes becomes the entire cluster, not an individual node.

For these types of hostile multitenant workloads, you should use physically isolated clusters. For more information on ways to isolate workloads, see [Best practices for cluster isolation in AKS](operator-best-practices-cluster-isolation).

### Compute isolation

Because of compliance or regulatory requirements, certain workloads may require a high degree of isolation from other customer workloads. For these workloads, Azure provides:

[Kernel isolated containers](/en-us/azure/confidential-computing/confidential-containers)to use as the agent nodes in an AKS cluster. These containers are completely isolated to a specific hardware type and isolated from the Azure Host fabric, the host operating system, and the hypervisor. They're dedicated to a single customer. Select[one of the isolated VMs sizes](/en-us/azure/virtual-machines/isolation)as the**node size**when creating an AKS cluster or adding a node pool.[Confidential Containers](confidential-containers-overview)(preview), also based on Kata Confidential Containers, encrypts container memory and prevents data in memory during computation from being in clear text, readable format, and tampering. It helps isolate your containers from other container groups/pods, and VM node OS kernel. Confidential Containers (preview) uses hardware based memory encryption (SEV-SNP).[Pod Sandboxing](use-pod-sandboxing)(preview) provides an isolation boundary between the container application and the shared kernel and compute resources (CPU, memory, and network) of the container host.

## Network security

For connectivity and security with on-premises networks, you can deploy your AKS cluster into existing Azure virtual network subnets. These virtual networks connect back to your on-premises network using Azure Site-to-Site VPN or Express Route. Define Kubernetes ingress controllers with private, internal IP addresses to limit services access to the internal network connection.

### Azure network security groups

To filter virtual network traffic flow, Azure uses network security group rules. These rules define the source and destination IP ranges, ports, and protocols allowed or denied access to resources. Default rules are created to allow TLS traffic to the Kubernetes API server. You create services with load balancers, port mappings, or ingress routes. AKS automatically modifies the network security group for traffic flow.

If you provide your own subnet for your AKS cluster (whether using Azure CNI or Kubenet), **do not** modify the NIC-level network security group managed by AKS. Instead, create more subnet-level network security groups to modify the flow of traffic. Make sure they don't interfere with necessary traffic managing the cluster, such as load balancer access, communication with the control plane, or [egress](limit-egress-traffic).

### Kubernetes network policy

To limit network traffic between pods in your cluster, AKS offers support for [Kubernetes network policies](use-network-policies). With network policies, you can allow or deny specific network paths within the cluster based on namespaces and label selectors.

## Application Security

To protect pods running on AKS, consider [Microsoft Defender for Containers](/en-us/azure/defender-for-cloud/defender-for-containers-introduction) to detect and restrict cyber attacks against your applications running in your pods. Run continual scanning to detect drift in the vulnerability state of your application and implement a "blue/green/canary" process to patch and replace the vulnerable images.

## Secure container access to resources

In the same way that you should grant users or groups the minimum privileges required, you should also limit containers to only necessary actions and processes. To minimize the risk of attack, avoid configuring applications and containers that require escalated privileges or root access. Built-in Linux security features such as *AppArmor* and *seccomp* are recommended as [best practices](/en-us/azure/aks/operator-best-practices-cluster-security) to [secure container access to resources][secure-container-access].

## Kubernetes Secrets

With a Kubernetes *Secret*, you inject sensitive data into pods, such as access credentials or keys.

- Create a Secret using the Kubernetes API.
- Define your pod or deployment and request a specific Secret.
- Secrets are only provided to nodes with a scheduled pod that requires them.
- The Secret is stored in
*tmpfs*, not written to disk.

- When you delete the last pod on a node requiring a Secret, the Secret is deleted from the node's
*tmpfs*.- Secrets are stored within a given namespace and are only accessible from pods within the same namespace.


Using Secrets reduces the sensitive information defined in the pod or service YAML manifest. Instead, you request the Secret stored in Kubernetes API Server as part of your YAML manifest. This approach only provides the specific pod access to the Secret.

Note

The raw secret manifest files contain the secret data in base64 format. For more information, see the [official documentation](https://kubernetes.io/docs/concepts/configuration/secret/#risks). Treat these files as sensitive information, and never commit them to source control.

Kubernetes secrets are stored in *etcd*, a distributed key-value store. AKS allows [encryption at rest of secrets in etcd using customer managed keys](use-kms-etcd-encryption).

## Next steps

To get started with securing your AKS clusters, see [Upgrade an AKS cluster](upgrade-cluster).

For associated best practices, see [Best practices for cluster security and upgrades in AKS](operator-best-practices-cluster-security) and [Best practices for pod security in AKS](developer-best-practices-pod-security).

For more information on core Kubernetes and AKS concepts, see:
