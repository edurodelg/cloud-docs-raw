---
merged_at: 2026-01-25T12:25:33.920230
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: developer-best-practices-pod-security.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/developer-best-practices-pod-security -->

# Best practices for pod security in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you develop and run applications in Azure Kubernetes Service (AKS), the security of your pods is a key consideration. Your applications should be designed for the principle of least number of privileges required. Keeping private data secure is top of mind for customers. You don't want credentials like database connection strings, keys, or secrets and certificates exposed to the outside world where an attacker could take advantage of those secrets for malicious purposes. Don't add them to your code or embed them in your container images. This approach would create a risk for exposure and limit the ability to rotate those credentials as the container images will need to be rebuilt.

This best practices article focuses on how to secure pods in AKS. You learn how to:

- Use pod security context to limit access to processes and services or privilege escalation
- Authenticate with other Azure resources using Microsoft Entra Workload ID
- Request and retrieve credentials from a digital vault such as Azure Key Vault

You can also read the best practices for [cluster security](operator-best-practices-cluster-security) and for [container image management](operator-best-practices-container-image-management).

## Secure pod access to resources

**Best practice guidance** - To run as a different user or group and limit access to the underlying node processes and services, define pod security context settings. Assign the least number of privileges required.

For your applications to run correctly, pods should run as a defined user or group and not as *root*. The `securityContext`

for a pod or container lets you define settings such as *runAsUser* or *fsGroup* to assume the appropriate permissions. Only assign the required user or group permissions, and don't use the security context as a means to assume additional permissions. The *runAsUser*, privilege escalation, and other Linux capabilities settings are only available on Linux nodes and pods.

When you run as a non-root user, containers cannot bind to the privileged ports under 1024. In this scenario, Kubernetes Services can be used to disguise the fact that an app is running on a particular port.

A pod security context can also define additional capabilities or permissions for accessing processes and services. The following common security context definitions can be set:

**allowPrivilegeEscalation**defines if the pod can assume*root*privileges. Design your applications so this setting is always set to*false*.**Linux capabilities**let the pod access underlying node processes. Take care with assigning these capabilities. Assign the least number of privileges needed. For more information, see[Linux capabilities](http://man7.org/linux/man-pages/man7/capabilities.7.html).**SELinux labels**is a Linux kernel security module that lets you define access policies for services, processes, and filesystem access. Again, assign the least number of privileges needed. For more information, see[SELinux options in Kubernetes](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.27/#selinuxoptions-v1-core)**hostUsers: false**the pod runs using a user-namespace, a Linux kernel feature. This significatly improves the host isolation and limits the lateral movement in case of container breakouts. These improvements are significant whether the container is running as root or not. For more information, see[user-namespaces](secure-container-access#user-namespaces).

The following example pod YAML manifest sets security context settings to define:

- Pod runs as user ID
*1000*and part of group ID*2000* - Can't escalate privileges to use
`root`

- Allows Linux capabilities to access network interfaces and the host's real-time (hardware) clock

```
apiVersion: v1
kind: Pod
metadata:
name: security-context-demo
spec:
securityContext:
fsGroup: 2000
containers:
- name: security-context-demo
image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
securityContext:
runAsUser: 1000
allowPrivilegeEscalation: false
capabilities:
add: ["NET_ADMIN", "SYS_TIME"]
```


Work with your cluster operator to determine which security context settings you need. Design your applications to minimize other permissions and access the pod requires. There are other security features to limit access using AppArmor, seccomp (secure computing), and user-namespaces that can be implemented by cluster operators.

For more information, see [Secure container access to resources](operator-best-practices-cluster-security#secure-container-access-to-resources).

## Limit credential exposure

**Best practice guidance** - Don't define credentials in your application code. Use managed identities for Azure resources to let your pod request access to other resources. A digital vault, such as Azure Key Vault, should also be used to store and retrieve digital keys and credentials. Pod-managed identities are intended for use with Linux pods and container images only.

To limit the risk of credentials being exposed in your application code, avoid the use of fixed or shared credentials. Credentials or keys shouldn't be included directly in your code. If these credentials are exposed, the application needs to be updated and redeployed. A better approach is to give pods their own identity and way to authenticate themselves, or automatically retrieve credentials from a digital vault.

#### Use a Microsoft Entra Workload ID

A workload identity is an identity used by an application running on a pod that can authenticate itself against other Azure services that support it, such as Storage or SQL. It integrates with the capabilities native to Kubernetes to federate with external identity providers. In this security model, the AKS cluster acts as token issuer, Microsoft Entra ID uses OpenID Connect to discover public signing keys and verify the authenticity of the service account token before exchanging it for a Microsoft Entra token. Your workload can exchange a service account token projected to its volume for a Microsoft Entra token using the Azure Identity client library using the [Azure SDK](https://azure.microsoft.com/downloads/) or the [Microsoft Authentication Library](/en-us/azure/active-directory/develop/msal-overview) (MSAL).

For more information about workload identities, see [Configure an AKS cluster to use Microsoft Entra Workload ID with your applications](workload-identity-overview)

#### Use Azure Key Vault with Secrets Store CSI Driver

Using the [Microsoft Entra Workload ID](workload-identity-overview) enables authentication against supporting Azure services. For your own services or applications without managed identities for Azure resources, you can still authenticate using credentials or keys. A digital vault can be used to store these secret contents.

When applications need a credential, they communicate with the digital vault, retrieve the latest secret contents, and then connect to the required service. Azure Key Vault can be this digital vault. The simplified workflow for retrieving a credential from Azure Key Vault using pod managed identities is shown in the following diagram:


With Key Vault, you store and regularly rotate secrets such as credentials, storage account keys, or certificates. You can integrate Azure Key Vault with an AKS cluster using the [Azure Key Vault provider for the Secrets Store CSI Driver](csi-secrets-store-driver). The Secrets Store CSI driver enables the AKS cluster to natively retrieve secret contents from Key Vault and securely provide them only to the requesting pod. Work with your cluster operator to deploy the Secrets Store CSI Driver onto AKS worker nodes. You can use a Microsoft Entra Workload ID to request access to Key Vault and retrieve the secret contents needed through the Secrets Store CSI Driver.

## Next steps

This article focused on how to secure your pods. To implement some of these areas, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: azure-cni-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-cni-overview -->

# Azure Kubernetes Service (AKS) CNI networking overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes uses Container Networking Interface (CNI) plugins to manage networking in Kubernetes clusters. CNI plug-ins are responsible for assigning IP addresses to pods, network routing between pods, Kubernetes service routing, and more.

Azure Kubernetes Service (AKS) provides multiple CNI plugins that you can use in your clusters, depending on your networking requirements.

## Networking models in AKS

Choosing a CNI plugin for your AKS cluster largely depends on which networking model fits your needs best. Each model has its own advantages and disadvantages that you should consider when planning your AKS cluster.

AKS uses two main networking models:

**Overlay network**:- Conserves IP address space for virtual networks by using logically separate Classless Inter-Domain Routing (CIDR) ranges for pods.
- Provides maximum cluster scale support.
- Provides simple management of IP addresses.

**Flat network**:- Provides full virtual network connectivity for pods. Pods can be directly reached via their private IP address from connected networks.
- Requires large, non-fragmented IP address space for virtual networks.


Both networking models have multiple supported options for CNI plugins. The main differences between the models are how pod IP addresses are assigned and how traffic leaves the cluster.

### Overlay networks

Overlay networking is the most common networking model used in Kubernetes. In overlay networks, pods receive an IP address from a private, logically separate CIDR from the Azure virtual network subnet where AKS nodes are deployed. This configuration allows for simpler and often better scalability than the flat network model.

In overlay networks, pods can communicate with each other directly. Traffic that leaves the cluster is Source Network Address Translated (SNAT'd) to the node's IP address. Inbound pod IP traffic is routed through a service, such as a load balancer. The pod IP address is then "hidden" behind the node's IP address. This approach reduces the number of IP addresses required for virtual networks in your clusters.


For overlay networking, AKS provides the [Azure CNI Overlay](concepts-network-azure-cni-overlay) plugin. We recommend this CNI plugin for most scenarios.

### Flat networks

Unlike an overlay network, a flat network model in AKS assigns IP addresses to pods from a subnet from the same Azure virtual network as the AKS nodes. Traffic that leaves your clusters is not SNAT'd, and the pod IP address is directly exposed to the destination. This approach can be useful for some scenarios, such as when you need to expose pod IP addresses to external services.


AKS provides two CNI plugins for flat networking:

[Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet), the recommended CNI plugin for flat networking scenarios.[Azure CNI Node Subnet](concepts-network-legacy-cni#azure-cni-node-subnet), a legacy CNI model for flat networks. In general, we recommend that you use it only if you*need*a managed virtual network for your cluster.

## Choosing a CNI plugin

When you're choosing a CNI plugin, there are several factors to consider. Each networking model has its own advantages and disadvantages. The best choice for your cluster depends on your specific requirements.

### Use case comparison

| CNI plugin | Networking model | Use case highlights |
|---|---|---|
| Azure CNI Overlay | Overlay | - Best for conserving IPs for virtual networks - Maximum node count supported by API server plus 250 pods per node - Simpler configuration - No direct external pod IP access |
| Azure CNI Pod Subnet | Flat | - Direct external pod access - Modes for efficient IP usage for virtual networks or large cluster scale support (preview) |
| Kubenet (legacy) | Overlay | - Prioritization of IP conservation - Limited scale - Manual route management |
| Azure CNI Node Subnet (legacy) | Flat | - Direct external pod access - Simpler configuration - Limited scale - Inefficient use of IPs for virtual networks |

### Feature comparison

| Feature | Azure CNI Overlay | Azure CNI Pod Subnet | Azure CNI Node Subnet (legacy) | Kubenet (legacy) |
|---|---|---|---|---|
| Deployment of a cluster in an existing or new virtual network | Supported | Supported | Supported | Supported with manual user-defined routes (UDRs) |
| Connectivity between pod and virtual machine (VM), with the VM in the same virtual network or a peered virtual network | Pod initiated | Both ways | Both ways | Pod initiated |
| On-premises access via virtual private network (VPN) and Azure ExpressRoute | Pod initiated | Both ways | Both ways | Pod initiated |
| Access to service endpoints | Supported | Supported | Supported | Supported |
| Exposure of services via load balancer | Supported | Supported | Supported | Supported |
| Exposure of services via Azure Application Gateway ingress controller | Supported | Supported | Supported | Supported |
| Exposure of services via Application Gateway for Containers | Supported | Supported | Supported | Not Supported |
| Windows node pools | Supported | Supported | Supported | Not supported |
| Default Azure DNS and private zones | Supported | Supported | Supported | Supported |
| Sharing of virtual network subnets across multiple clusters | Supported | Supported | Supported | Not supported |

### Support scope between network models

Depending on the CNI plugin that you use, you can deploy the virtual network resources for your cluster in one of the following ways:

- The Azure platform can automatically create and configure the virtual network resources when you create an AKS cluster, like in Azure CNI Overlay, Azure CNI Node Subnet, and Kubenet.
- You can manually create and configure the virtual network resources and attach to those resources when you create your AKS cluster.

Although capabilities like service endpoints or UDRs are supported, the [support policies for AKS](support-policies) define what changes you can make. For example:

- If you manually create the virtual network resources for an AKS cluster, you're supported when configuring your own UDRs or service endpoints.
- If the Azure platform automatically creates the virtual network resources for your AKS cluster, you can't manually change those AKS-managed resources to configure your own UDRs or service endpoints.

## Prerequisites

When you're planning your network configuration for AKS, keep these requirements and considerations in mind:

- The virtual network for the AKS cluster must allow outbound internet connectivity.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for address ranges for the Kubernetes service, pods, or cluster virtual networks. - In scenarios where you bring your own virtual network, the cluster identity that the AKS cluster uses must have at least
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)permissions on the subnet within your virtual network. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, the following permissions are required:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Authorization/roleAssignments/write`

`Microsoft.Network/virtualNetworks/subnets/read`

(needed only if you're defining your own subnets and CIDRs)

- The subnet assigned to the AKS node pool can't be a
[delegated subnet](/en-us/azure/virtual-network/subnet-delegation-overview). - AKS doesn't apply network security groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure that the security rules in the NSGs allow traffic within the node CIDR range. For more information, see
[Azure network security groups overview](/en-us/azure/virtual-network/network-security-groups-overview).
