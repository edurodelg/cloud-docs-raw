---
merged_at: 2026-01-25T12:25:33.927555
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: node-autoprovision-networking.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-autoprovision-networking -->

# Overview of networking configurations for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of networking configuration requirements and recommendations for Azure Kubernetes Service (AKS) clusters using node auto-provisioning (NAP). It covers supported configurations, default subnet behavior, role-based access control (RBAC) setup, and classless inter-domain routing (CIDR) considerations.

For an overview of node auto-provisioning in AKS, see [Overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)](node-auto-provisioning).

## Supported networking configurations for NAP

NAP supports the following networking configurations:

We recommend using Azure CNI with [Cilium](azure-cni-powered-by-cilium). Cilium provides advanced networking capabilities and is optimized for performance with NAP.

### Unsupported networking configurations for NAP

NAP doesn't support the following networking configurations:

- Calico network policy
- Dynamic IP allocation

## Subnet configurations for NAP

NAP automatically deploys, configures, and manages Karpenter on your AKS clusters and is based on the open-source [Karpenter](https://karpenter.sh) and [AKS Karpenter provider](https://github.com/Azure/karpenter-provider-azure) projects. You can use [ AKSNodeClass](node-auto-provisioning-aksnodeclass) resources to specify custom subnet configurations for NAP nodes in your node pools by setting the optional

`vnetSubnetID`

field, and Karpenter uses the subnet you specify for node provisioning. If you don't specify a subnet, Karpenter uses the default subnet configured during Karpenter installation. This default subnet is typically the same subnet specified during AKS cluster creation with the `--vnet-subnet-id`

parameter in the `az aks create`

command.This approach allows you to have a mix of node classes, with some using custom subnets for specific workloads, and others using the cluster's default subnet configuration.

## Subnet drift behavior

Karpenter monitors subnet configuration changes and detects drift when the `vnetSubnetID`

in an `AKSNodeClass`

is modified. Understanding this behavior is critical when managing custom networking configurations.

**Modifying vnetSubnetID from one valid subnet to another valid subnet isn't a supported operation**. If you change the

`vnetSubnetID`

to point to a different valid subnet, Karpenter detects this as subnet drift and prevents node provisioning until the issue is resolved by reverting the `vnetSubnetID`

to the original subnet. This behavior ensures that nodes are only provisioned in the intended subnets, maintaining network integrity and security. However, there are exceptions to this rule. You can only modify the `vnetSubnetID`

in the following scenarios:- Correcting a malformed subnet ID that prevents node provisioning.
- Fixing an invalid subnet reference that causes configuration errors.
- Updating a subnet identifier that points to a nonexistent or inaccessible subnet.

## Understand AKS cluster Classless Inter-Domain Routing (CIDR) ranges

When configuring custom networking with `vnetSubnetID`

, you're responsible for understanding and managing your cluster's CIDR ranges to avoid network conflicts. Unlike traditional AKS node pools created through ARM templates, Karpenter applies custom resource definitions (CRDs) that provision nodes instantly without the extended validation that ARM provides.

### CIDR considerations for custom subnet configurations

When configuring `vnetSubnetID`

, you must:

**Verify CIDR compatibility**: Ensure custom subnets don't conflict with existing CIDR ranges.**Plan IP capacity**: Calculate required IP addresses for expected scaling.**Validate connectivity**: Test network routes and security group rules.**Monitor usage**: Track subnet utilization and plan for growth.**Document configuration**: Maintain records of network design decisions.

### Common CIDR conflicts

Be aware of the following common CIDR conflict scenarios when using custom subnets with NAP:

```
# Example conflict scenarios:
# Cluster Pod CIDR: 10.244.0.0/16
# Custom Subnet: 10.244.1.0/24 ❌ CONFLICT
# Service CIDR: 10.0.0.0/16
# Custom Subnet: 10.0.10.0/24 ❌ CONFLICT
# Safe configuration:
# Cluster Pod CIDR: 10.244.0.0/16
# Service CIDR: 10.0.0.0/16
# Custom Subnet: 10.1.0.0/24 ✅ NO CONFLICT
```


## RBAC setup for custom subnet configurations

When using custom subnet configurations with NAP, you need to ensure that Karpenter has the necessary permissions to read subnet information and join nodes to the specified subnets. This requires setting up appropriate RBAC permissions for the cluster's managed identity.

There are two main approaches to setting up these permissions: **Assign broad virtual network (VNet) permissions** or **Assign scoped subnet permissions**.

This approach is the most permissive and grants the cluster identity permissions to read and join any subnet within the main VNet and provides network contributor access.

Important

Investigate the "Network Contributor" role before applying this approach to your production cluster.

#### Benefits and considerations

The following table outlines the benefits and considerations of assigning broad VNet permissions:

| Benefits | Considerations |
|---|---|
| • Simplifies permission management. • Eliminates the need to update permissions when adding new subnets. • Works well for single-tenant environments. • Functions when a subscription reaches the maximum number of custom roles. |
• Provides broader permissions than strictly necessary. • Might not meet strict security requirements. |

#### Required permissions

To assign broad VNet permissions, grant the cluster's managed identity the following permissions on the VNet:

```
# Get your cluster's managed identity
CLUSTER_IDENTITY=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query identity.principalId -o tsv)
# Get your VNet resource ID
VNET_ID="/subscriptions/$SUBSCRIPTION_ID/resourceGroups/$VNET_RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME"
# Assign Network Contributor role for subnet read/join operations
az role assignment create \
--assignee $CLUSTER_IDENTITY \
--role "Network Contributor" \
--scope $VNET_ID
```


For a complete example of setting up custom networking and assigning broad VNet permissions, see the [Custom VNET setup - Most permissive RBAC sample script](https://gist.github.com/Bryce-Soghigian/a4259d6224db0c55081718caa7b37268).

## Example custom subnet configurations

The following example shows how to configure a custom subnet for NAP nodes using the `vnetSubnetID`

field in an `AKSNodeClass`

resource:

```
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: custom-networking
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME"
```


The following example shows how to use multiple node classes with different subnet configurations:

```
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: frontend-nodes
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$FRONTEND_SUBNET_NAME"
---
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: backend-nodes
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$BACKEND_SUBNET_NAME"
```


## Bring your own CNI (BYO CNI) support policy

Karpenter for Azure allows bring your own Container Network Interface (BYO CNI) configurations, following the same support policy as AKS. This means that when using a custom CNI, troubleshooting support related to networking is out of scope of any service-level agreements or warranties.

### Support scope details

The following outlines what is and isn't supported when using BYO CNI with Karpenter:

**Supported**: Karpenter-specific functionality and integration issues when using bring-your-own (BYO) CNI configurations.**Not supported**: CNI-specific networking issues, configuration problems, or troubleshooting when using third-party CNI plugins.

## Next steps

For more information on node auto-provisioning in AKS, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: node-auto-provisioning-networking.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-networking -->

# Overview of networking configurations for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of networking configuration requirements and recommendations for Azure Kubernetes Service (AKS) clusters using node auto-provisioning (NAP). It covers supported configurations, default subnet behavior, role-based access control (RBAC) setup, and classless inter-domain routing (CIDR) considerations.

For an overview of node auto-provisioning in AKS, see [Overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)](node-auto-provisioning).

## Supported networking configurations for NAP

NAP supports the following networking configurations:

We recommend using Azure CNI with [Cilium](azure-cni-powered-by-cilium). Cilium provides advanced networking capabilities and is optimized for performance with NAP.

### Unsupported networking configurations for NAP

NAP doesn't support the following networking configurations:

- Calico network policy
- Dynamic IP allocation

## Subnet configurations for NAP

NAP automatically deploys, configures, and manages Karpenter on your AKS clusters and is based on the open-source [Karpenter](https://karpenter.sh) and [AKS Karpenter provider](https://github.com/Azure/karpenter-provider-azure) projects. You can use [ AKSNodeClass](node-auto-provisioning-aksnodeclass) resources to specify custom subnet configurations for NAP nodes in your node pools by setting the optional

`vnetSubnetID`

field, and Karpenter uses the subnet you specify for node provisioning. If you don't specify a subnet, Karpenter uses the default subnet configured during Karpenter installation. This default subnet is typically the same subnet specified during AKS cluster creation with the `--vnet-subnet-id`

parameter in the `az aks create`

command.This approach allows you to have a mix of node classes, with some using custom subnets for specific workloads, and others using the cluster's default subnet configuration.

## Subnet drift behavior

Karpenter monitors subnet configuration changes and detects drift when the `vnetSubnetID`

in an `AKSNodeClass`

is modified. Understanding this behavior is critical when managing custom networking configurations.

**Modifying vnetSubnetID from one valid subnet to another valid subnet isn't a supported operation**. If you change the

`vnetSubnetID`

to point to a different valid subnet, Karpenter detects this as subnet drift and prevents node provisioning until the issue is resolved by reverting the `vnetSubnetID`

to the original subnet. This behavior ensures that nodes are only provisioned in the intended subnets, maintaining network integrity and security. However, there are exceptions to this rule. You can only modify the `vnetSubnetID`

in the following scenarios:- Correcting a malformed subnet ID that prevents node provisioning.
- Fixing an invalid subnet reference that causes configuration errors.
- Updating a subnet identifier that points to a nonexistent or inaccessible subnet.

## Understand AKS cluster Classless Inter-Domain Routing (CIDR) ranges

When configuring custom networking with `vnetSubnetID`

, you're responsible for understanding and managing your cluster's CIDR ranges to avoid network conflicts. Unlike traditional AKS node pools created through ARM templates, Karpenter applies custom resource definitions (CRDs) that provision nodes instantly without the extended validation that ARM provides.

### CIDR considerations for custom subnet configurations

When configuring `vnetSubnetID`

, you must:

**Verify CIDR compatibility**: Ensure custom subnets don't conflict with existing CIDR ranges.**Plan IP capacity**: Calculate required IP addresses for expected scaling.**Validate connectivity**: Test network routes and security group rules.**Monitor usage**: Track subnet utilization and plan for growth.**Document configuration**: Maintain records of network design decisions.

### Common CIDR conflicts

Be aware of the following common CIDR conflict scenarios when using custom subnets with NAP:

```
# Example conflict scenarios:
# Cluster Pod CIDR: 10.244.0.0/16
# Custom Subnet: 10.244.1.0/24 ❌ CONFLICT
# Service CIDR: 10.0.0.0/16
# Custom Subnet: 10.0.10.0/24 ❌ CONFLICT
# Safe configuration:
# Cluster Pod CIDR: 10.244.0.0/16
# Service CIDR: 10.0.0.0/16
# Custom Subnet: 10.1.0.0/24 ✅ NO CONFLICT
```


## RBAC setup for custom subnet configurations

When using custom subnet configurations with NAP, you need to ensure that Karpenter has the necessary permissions to read subnet information and join nodes to the specified subnets. This requires setting up appropriate RBAC permissions for the cluster's managed identity.

There are two main approaches to setting up these permissions: **Assign broad virtual network (VNet) permissions** or **Assign scoped subnet permissions**.

This approach is the most permissive and grants the cluster identity permissions to read and join any subnet within the main VNet and provides network contributor access.

Important

Investigate the "Network Contributor" role before applying this approach to your production cluster.

#### Benefits and considerations

The following table outlines the benefits and considerations of assigning broad VNet permissions:

| Benefits | Considerations |
|---|---|
| • Simplifies permission management. • Eliminates the need to update permissions when adding new subnets. • Works well for single-tenant environments. • Functions when a subscription reaches the maximum number of custom roles. |
• Provides broader permissions than strictly necessary. • Might not meet strict security requirements. |

#### Required permissions

To assign broad VNet permissions, grant the cluster's managed identity the following permissions on the VNet:

```
# Get your cluster's managed identity
CLUSTER_IDENTITY=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query identity.principalId -o tsv)
# Get your VNet resource ID
VNET_ID="/subscriptions/$SUBSCRIPTION_ID/resourceGroups/$VNET_RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME"
# Assign Network Contributor role for subnet read/join operations
az role assignment create \
--assignee $CLUSTER_IDENTITY \
--role "Network Contributor" \
--scope $VNET_ID
```


For a complete example of setting up custom networking and assigning broad VNet permissions, see the [Custom VNET setup - Most permissive RBAC sample script](https://gist.github.com/Bryce-Soghigian/a4259d6224db0c55081718caa7b37268).

## Example custom subnet configurations

The following example shows how to configure a custom subnet for NAP nodes using the `vnetSubnetID`

field in an `AKSNodeClass`

resource:

```
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: custom-networking
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME"
```


The following example shows how to use multiple node classes with different subnet configurations:

```
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: frontend-nodes
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$FRONTEND_SUBNET_NAME"
---
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: backend-nodes
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$BACKEND_SUBNET_NAME"
```


## Bring your own CNI (BYO CNI) support policy

Karpenter for Azure allows bring your own Container Network Interface (BYO CNI) configurations, following the same support policy as AKS. This means that when using a custom CNI, troubleshooting support related to networking is out of scope of any service-level agreements or warranties.

### Support scope details

The following outlines what is and isn't supported when using BYO CNI with Karpenter:

**Supported**: Karpenter-specific functionality and integration issues when using bring-your-own (BYO) CNI configurations.**Not supported**: CNI-specific networking issues, configuration problems, or troubleshooting when using third-party CNI plugins.

## Next steps

For more information on node auto-provisioning in AKS, see the following articles:
