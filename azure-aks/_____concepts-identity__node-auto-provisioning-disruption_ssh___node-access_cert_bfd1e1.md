---
merged_at: 2026-02-05T08:27:02.815725
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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/certificate-rotation -->

# Certificate rotation in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) uses certificates for authentication with many of its components. You need to periodically rotate those certificates for security or policy reasons. This article shows you how certificate rotation works in your AKS cluster.

Important

Starting on **March 30, 2026** Azure Kubernetes Service (AKS) no longer supports the `aks-disable-kubelet-serving-certificate-rotation=true`

node pool tag to disable Kubelet Serving Certificate Rotation (KSCR). You can create new node pools using this tag, but AKS won't respect it. This behavior means that the node pools will be created with KSCR enabled. For existing node pools, KSCR will be automatically enabled on their next reimage operation. Before this date you can update your node pools using the [`az aks nodepool update`

][az-aks-nodepool-update] command with the `aks-disable-kubelet-serving-certificate-rotation=true`

tag. To prepare for the removal, you should update your workloads with the correct cert path. For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/5539). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Prerequisites

This article requires the Azure CLI version 2.0.77 or later. Check your version using the

`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).Configure

`kubectl`

to connect to your AKS cluster using thecommand:`az aks get-credentials`

`az aks get-credentials --resource-group <resource-group> --name <cluster-name>`


## AKS certificates, Certificate Authorities, and Service Accounts

AKS generates and uses the following certificates, Certificate Authorities (CA), and Service Accounts (SA):

- The AKS API server creates a CA called the
*Cluster CA*, which signs certificates for one-way communication from the API server to kubelet. - Each kubelet creates a Certificate Signing Request (CSR), which the Cluster CA signs, for communication from the kubelet to the API server.
- The API aggregator uses the Cluster CA to issue certificates for communication with other APIs. The API aggregator can also have its own CA for issuing those certificates, but it currently uses the Cluster CA.
- Each agent node uses an SA token, which the Cluster CA signs.
- The
`kubectl`

client has a certificate for communicating with the AKS cluster.

Microsoft maintains all certificates mentioned in this section, except for the cluster certificate.

## Certificate expiration dates

Important

The expiration date for your certificates depends on when your AKS cluster was created:

**AKS clusters created**have certificates that expire after two years.*before*May 2019**AKS clusters created**have Cluster CA certificates that expire after 30 years.*after*May 2019

You can verify when your cluster was created using the `kubectl get nodes`

command, which shows you the `Age`

of your agent nodes.

## Check cluster certificate expiration date

Check the expiration date of the cluster certificate using the

`kubectl config view`

command.`kubectl config view --raw -o jsonpath="{.clusters[?(@.name == '')].cluster.certificate-authority-data}" | base64 -d | openssl x509 -text | grep -A2 Validity`


## Check API server certificate expiration date

Check the expiration date of the API server certificate using the following

`curl`

command:`curl https://{apiserver-fqdn} -k -v 2>&1 | grep expire`


## Check virtual machine (VM) agent node certificate expiration date

Check the expiration date of the VM agent node certificate using the

command.`az vm run-command invoke`

**Key parameters in this command**: -`--resource-group <node-resource-group>`

: The resource group that contains the VM agent node. -`--name <vm-name>`

: The name of the VM agent node. -`--scripts "openssl x509 -in /etc/kubernetes/certs/apiserver.crt -noout -enddate"`

: The script that retrieves the expiration date of the API server certificate located at`/etc/kubernetes/certs/apiserver.crt`

.`az vm run-command invoke --resource-group <node-resource-group> --name <vm-name> --command-id RunShellScript --query 'value[0].message' -otsv --scripts "openssl x509 -in /etc/kubernetes/certs/apiserver.crt -noout -enddate"`


## Check certificate expiration for the Azure Virtual Machine Scale Set agent node

Check the expiration date of the Azure Virtual Machine Scale Set agent node certificate using the

command.`az vmss run-command invoke`

**Key parameters in this command**: -`--resource-group <node-resource-group>`

: The resource group that contains the Azure Virtual Machine Scale Set agent node. -`--name <vmss-name>`

: The name of the Azure Virtual Machine Scale Set. -`--instance-id 1`

: The instance ID of the Azure Virtual Machine Scale Set agent node. -`--scripts "openssl x509 -in /var/lib/kubelet/pki/kubelet-client-current.pem -noout -enddate"`

: The script that retrieves the expiration date of the kubelet client certificate located at`/var/lib/kubelet/pki/kubelet-client-current.pem`

.`az vmss run-command invoke --resource-group <node-resource-group> --name <vmss-name> --command-id RunShellScript --instance-id 1 --scripts "openssl x509 -in /var/lib/kubelet/pki/kubelet-client-current.pem -noout -enddate" --query "value[0].message"`


## Manually rotate your cluster certificates

Rotate all certificates, CAs, and SAs on your cluster using the

command.`az aks rotate-certs`

`az aks rotate-certs --resource-group <resource-group> --name <cluster-name>`

Important

The

command recreates all of your agent nodes, Azure Virtual Machine Scale Sets, and disks. This command can also cause up to`az aks rotate-certs`

*30 minutes of downtime*for your AKS cluster. If the command fails before completing, use the [`az aks show`

][az-aks-show] command to verify the status of the cluster is`Certificate Rotating`

. If the cluster is in a failed state, rerun thecommand to rotate your certificates again.`az aks rotate-certs`

Verify the old certificates are no longer valid using any

`kubectl`

command. The following example uses the`kubectl get nodes`

command:`kubectl get nodes`

If you didn't update the certificates used by

`kubectl`

, you see an error similar to the following example output:`Unable to connect to the server: x509: certificate signed by unknown authority (possibly because of "crypto/rsa: verification error" while trying to verify candidate authority certificate "ca")`

Update the certificate used by

`kubectl`

using thecommand with the`az aks get-credentials`

`--overwrite-existing`

flag.`az aks get-credentials --resource-group <resource-group> --name <cluster-name> --overwrite-existing`

Verify the certificates are updated using the

command.`kubectl get`

`kubectl get nodes`


If you have any services that run on top of AKS, you might need to update their certificates as well.

## Rotate the kubelet serving certificate

When you rotate the kubelet serving certificate, AKS allows kubelet server Transport Layer Security (TLS) Bootstrapping for both bootstrapping and rotating serving certificates signed by the Cluster CA.

### Limitations for kubelet serving certificate rotation

- Supported on Kubernetes version 1.27 and above.
- Not supported when the node pool is using a node pool snapshot based on any node image older than
`202501.12.0`

. - You can't manually enable this feature. Kubelet serving certificate rotation is enabled by default on existing node pools when they perform their first upgrade to any Kubernetes version 1.27 or higher. Kubelet serving certificate rotation is enabled by default on new node pools using Kubernetes version 1.27 or higher. To see if kubelet serving certificate rotation is enabled in your region, check the
[AKS releases](https://github.com/Azure/AKS/releases).

## Verify kubelet serving certificate rotation is enabled

Each node with the feature enabled is automatically given the label `kubernetes.azure.com/kubelet-serving-ca=cluster`

.

Verify the labels are set using the

`kubectl get nodes -L kubernetes.azure.com/kubelet-serving-ca`

command.`kubectl get nodes -L kubernetes.azure.com/kubelet-serving-ca`

The output should show the label

`kubernetes.azure.com/kubelet-serving-ca`

with the value`cluster`

for each agent node.

## Verify kubelet TLS Bootstrapping is working

Verify the bootstrapping process is taking place using the

command.`kubectl get`

`kubectl get csr --field-selector=spec.signerName=kubernetes.io/kubelet-serving`

In the output, all serving CSRs should be in the

`Approved,Issued`

state, which indicates the CSR was approved and issued a signed certificate. Serving CSRs have a signer name of`kubernetes.io/kubelet-serving`

. For example:`NAME AGE SIGNERNAME REQUESTOR REQUESTEDDURATION CONDITION csr-1ab2c 113s kubernetes.io/kube-apiserver-client-kubelet system:bootstrap:uoxr9r none Approved,Issued csr-defgh 111s kubernetes.io/kubelet-serving system:node:akswinp7000000 none Approved,Issued csr-ij3kl 46m kubernetes.io/kubelet-serving system:node:akswinp6000000 none Approved,Issued csr-mn4op 46m kubernetes.io/kube-apiserver-client-kubelet system:bootstrap:ho7zyu none Approved,Issued`


## Verify kubelet is using a certificate obtained from server TLS Bootstrapping

Confirm the kubelet is using a serving certificate signed by the Cluster CA using the

command.`kubectl debug`

`kubectl debug node/<node> -ti --image=mcr.microsoft.com/azurelinux/base/core:3.0 -- ls -l /host/var/lib/kubelet/kubelet-server-current.pem`

If a

`kubelet-server-current.pem`

symlink exists, then the kubelet bootstrapped/rotated its own serving certificate, and the Cluster CA signed it.

## Disable kubelet serving certificate rotation

Disable kubelet serving certificate rotation by updating the node pool using the

command with the`az aks nodepool update`

`aks-disable-kubelet-serving-certificate-rotation=true`

tag.`az aks nodepool update --cluster-name <cluster-name> --resource-group <resource-group> --name <node-pool-name> --tags aks-disable-kubelet-serving-certificate-rotation=true`


- Reimage your nodes using a
[node image upgrade](node-image-upgrade)or by scaling the pool to*zero*instances and then back up to the desired value.

## Certificate autorotation

Keep the following considerations in mind when using certificate autorotation:

- If you have an existing cluster, you have to upgrade that cluster to enable certificate autorotation.
- Don't disable TLS Bootstrap to keep certificate autorotation enabled.
- If the cluster is in a stopped state during certificate autorotation, only the control plane certificates are rotated. In this case, you should recreate the node pool after certificate rotation to initiate the node pool certificate rotation.
- For any AKS clusters created or upgraded after March 2022, AKS automatically rotates non-CA certificates on both the control plane and agent nodes within 80% of the client certificate valid time before they expire with no downtime for the cluster.

## Verify TLS Bootstrapping is enabled on current agent node pool

Verify your cluster has TLS Bootstrapping enabled by browsing to one to the following paths:

**On a Linux node**:`/var/lib/kubelet/bootstrap-kubeconfig`

or`/host/var/lib/kubelet/bootstrap-kubeconfig`

**On a Windows node**:`C:\k\bootstrap-config`


For more information, see

[Connect to Azure Kubernetes Service (AKS) cluster nodes for maintenance or troubleshooting](node-access).Note

The file path might change as Kubernetes versions evolve.

Once a region is configured, create a new cluster or upgrade an existing cluster to set certificate autorotation for the cluster certificate. You need to upgrade the control plane and node pool to enable this feature.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-production-upgrade-strategies -->

# AKS production upgrade strategies

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Upgrade your production Azure Kubernetes Service (AKS) clusters safely by using these proven patterns. Each strategy is optimized for specific business constraints and risk tolerance.

## What this article covers

This article provides tested upgrade patterns for production AKS clusters and focuses on:

- Blue-green deployments for zero-downtime upgrades.
- Staged fleet upgrades across multiple environments.
- Safe Kubernetes version adoption with validation gates.
- Emergency security patching for rapid common vulnerabilities and exposures (CVE) response.
- Application resilience patterns for seamless upgrades.

These patterns are best for production environments, site reliability engineers, and platform teams that require minimal downtime and maximum safety.

For more information, see these related articles:

- To get upgrade patterns for AKS clusters with stateful workloads, see
[Stateful workload upgrade patterns](stateful-workload-upgrades). - To check for and apply basic upgrades to your AKS cluster, see
[Upgrade an Azure Kubernetes Service cluster](upgrade-aks-cluster). - To use the scenario hub to help you choose the right AKS upgrade approach, see
[AKS upgrade scenarios: Choose your path](upgrade-scenarios-hub).

For a quick start, select a link for instructions:

## Choose your strategy

| Your priority | Best pattern | Downtime | Time to complete |
|---|---|---|---|
| Zero downtime |
|

[Staged fleet upgrades](#scenario-2-stage-upgrades-across-environments)[Canary with validation](#scenario-3-safe-kubernetes-version-intake)[Automated patching](#scenario-4-fastest-security-patch-deployment)[Resilient architecture](#scenario-5-application-architecture-for-seamless-upgrades)#### Role-based quick start

| Role | Start here |
|---|---|
| Site reliability engineer/Platform |
|

[Stateful workload patterns](stateful-workload-upgrades)[Scenario 5](#scenario-5-application-architecture-for-seamless-upgrades)[Scenario 4](#scenario-4-fastest-security-patch-deployment)## Scenario 1: Minimal downtime production upgrades

**Challenge:** "I need to upgrade my production cluster with less than 2 minutes of downtime during business hours."

**Strategy:** Use blue-green deployment with intelligent traffic shifting.

To learn more, see [Blue-green deployment patterns](/en-us/azure/architecture/guide/aks/blue-green-deployment-for-aks) and [Azure Traffic Manager configuration](/en-us/azure/traffic-manager/traffic-manager-configure-weighted-routing-method).

### Quick implementation (15 minutes)

```
# 1. Create green cluster (parallel to blue)
az aks create --name myaks-green --resource-group myRG \
--kubernetes-version 1.29.0 --enable-cluster-autoscaler \
--min-count 3 --max-count 10
# 2. Deploy application to green cluster
kubectl config use-context myaks-green
kubectl apply -f ./production-manifests/
# 3. Validate green cluster
# Run your application-specific health checks here
# Examples: API endpoint tests, database connectivity, dependency checks
# 4. Switch traffic (<30-second downtime)
az network traffic-manager endpoint update \
--profile-name prod-tm --name green-endpoint --weight 100
az network traffic-manager endpoint update \
--profile-name prod-tm --name blue-endpoint --weight 0
```


** Detailed step-by-step guide**

#### Prerequisites

- Secondary cluster capacity planned.
- Application supports horizontal scaling.
- Database connections use connection pooling.
- Health checks configured (
`/health`

,`/ready`

). - Rollback procedure tested in staging.

#### Step 1: Prepare the blue-green infrastructure

```
# Create resource group for green cluster
az group create --name myRG-green --location eastus2
# Create green cluster with same configuration as blue
az aks create \
--resource-group myRG-green \
--name myaks-green \
--kubernetes-version 1.29.0 \
--node-count 3 \
--enable-cluster-autoscaler \
--min-count 3 \
--max-count 10 \
--enable-addons monitoring \
--generate-ssh-keys
```


#### Step 2: Deploy and validate the green environment

```
# Get green cluster credentials
az aks get-credentials --resource-group myRG-green --name myaks-green
# Deploy application stack
# Apply your Kubernetes manifests in order:
kubectl apply -f ./your-manifests/namespace.yaml # Create namespace
kubectl apply -f ./your-manifests/secrets/ # Deploy secrets
kubectl apply -f ./your-manifests/configmaps/ # Deploy config maps
kubectl apply -f ./your-manifests/deployments/ # Deploy applications
kubectl apply -f ./your-manifests/services/ # Deploy services
# Wait for all pods to be ready
kubectl wait --for=condition=ready pod --all --timeout=300s
# Validate application health
kubectl get pods -A
kubectl logs -l app=my-app --tail=50
```


#### Step 3: Traffic switching (critical 30-second window)

```
# Pre-switch validation
curl -f https://myapp-green.eastus2.cloudapp.azure.com/health
if [ $? -ne 0 ]; then echo "Green health check failed!"; exit 1; fi
# Execute traffic switch
az network dns record-set cname set-record \
--resource-group myRG-dns \
--zone-name mycompany.com \
--record-set-name api \
--cname myapp-green.eastus2.cloudapp.azure.com
# Immediate validation
sleep 30
curl -f https://api.mycompany.com/health
```


#### Step 4: Monitor and validate

```
# Monitor traffic and errors for 15 minutes
kubectl top nodes
kubectl top pods
kubectl logs -l app=my-app --since=15m | grep ERROR
# Check application metrics
curl https://api.mycompany.com/metrics | grep http_requests_total
```


### Common pitfalls and FAQs

**Expand for quick troubleshooting and tips**

**Domain Name System (DNS) propagation is slow:**Use low time-to-live values before upgrade, and validate the DNS cache flush.**Pods stuck terminating:**Check for finalizers, long shutdown hooks, or pod disruption budgets (PDBs) with`maxUnavailable: 0`

.**Traffic not shifting:**Validate Azure Load Balancer/Azure Traffic Manager configuration and health probes.**Rollback fails:**Always keep the blue cluster ready until the green cluster is fully validated.**Q: Can I use open-source software tools for validation?****A:**Yes. Use[kube-no-trouble](https://github.com/doitintl/kube-no-trouble)for API checks and[Trivy](https://aquasecurity.github.io/trivy/)for image scanning.

**Q: What's unique to AKS?****A:**Native integration with Traffic Manager, Azure Kubernetes Fleet Manager, and node image patching for zero-downtime upgrades.


### Advanced configuration

For applications that require <30-second downtime:

```
# Use session affinity during transition
apiVersion: v1
kind: Service
metadata:
name: my-app
spec:
sessionAffinity: ClientIP
sessionAffinityConfig:
clientIP:
timeoutSeconds: 300
```


### Success validation

To validate your progress, use the following checklist:

- Application responds within two seconds.
- No 5xx errors are in logs.
- Database connections are stable.
- User sessions are preserved.

### Emergency rollback (if needed)

```
# Immediate rollback to blue cluster
az network dns record-set cname set-record \
--resource-group myRG-dns \
--zone-name mycompany.com \
--record-set-name api \
--cname myapp-blue.eastus2.cloudapp.azure.com
```


**Expected outcome:** Less than 2-minute total downtime, zero data loss, and full rollback capability.

```
az aks create \
--resource-group production-rg \
--name aks-green-cluster \
--kubernetes-version 1.29.0 \
--node-count 3 \
--tier premium \
--auto-upgrade-channel patch \
--planned-maintenance-config ./maintenance-window.json
```


## Verify cluster readiness

```
az aks get-credentials --resource-group production-rg --name aks-green-cluster
kubectl get nodes
```


### Implementation steps

#### Step 1: Deploy the application to a green cluster

```
# Deploy application stack
kubectl apply -f ./k8s-manifests/
kubectl apply -f ./monitoring/
# Wait for all pods to be ready
kubectl wait --for=condition=ready pod --all --timeout=300s
# Validate application health
curl -f http://green-cluster-ingress/health
```


#### Step 2: Run traffic shift

```
# Update DNS or load balancer to point to green cluster
az network dns record-set a update \
--resource-group dns-rg \
--zone-name contoso.com \
--name api \
--set aRecords[0].ipv4Address="<green-cluster-ip>"
# Monitor traffic shift (should complete in 60-120 seconds)
watch kubectl top pods -n production
```


#### Step 3: Validate and clean up

```
# Verify zero errors in application logs
kubectl logs -l app=api --tail=100 | grep -i error
# Monitor key metrics for 15 minutes
kubectl get events --sort-by='.lastTimestamp' | head -20
# After validation, decommission blue cluster
az aks delete --resource-group production-rg --name aks-blue-cluster --yes
```


### Success metrics

**Downtime:**<2 minutes (DNS propagation time)**Error rate:**0% during transition**Recovery time:**<5 minutes if rollback needed

## Scenario 2: Stage upgrades across environments

**Challenge:** "I need to safely test upgrades through dev/test/production with proper validation gates."

**Strategy:** Use Azure Kubernetes Fleet Manager with staged rollouts.

To learn more, see the [Azure Kubernetes Fleet Manager overview](/en-us/azure/kubernetes-fleet/overview) and [Update orchestration](/en-us/azure/kubernetes-fleet/update-orchestration).

### Prerequisites

```
# Install Fleet extension
az extension add --name fleet
az extension update --name fleet
# Create Fleet resource
az fleet create \
--resource-group fleet-rg \
--name production-fleet \
--location eastus
```


### Implementation steps

#### Step 1: Define stage configuration

Create `upgrade-stages.json`

:

```
{
"stages": [
{
"name": "development",
"groups": [{ "name": "dev-clusters" }],
"afterStageWaitInSeconds": 1800
},
{
"name": "testing",
"groups": [{ "name": "test-clusters" }],
"afterStageWaitInSeconds": 3600
},
{
"name": "production",
"groups": [{ "name": "prod-clusters" }],
"afterStageWaitInSeconds": 0
}
]
}
```


#### Step 2: Add clusters to a fleet

```
# Add development clusters
az fleet member create \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name dev-east \
--member-cluster-id "/subscriptions/.../clusters/aks-dev-east" \
--group dev-clusters
# Add test clusters
az fleet member create \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name test-east \
--member-cluster-id "/subscriptions/.../clusters/aks-test-east" \
--group test-clusters
# Add production clusters
az fleet member create \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name prod-east \
--member-cluster-id "/subscriptions/.../clusters/aks-prod-east" \
--group prod-clusters
```


#### Step 3: Create and run a staged update

```
# Create staged update run
az fleet updaterun create \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name k8s-1-29-upgrade \
--upgrade-type Full \
--kubernetes-version 1.29.0 \
--node-image-selection Latest \
--stages upgrade-stages.json
# Start the staged rollout
az fleet updaterun start \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name k8s-1-29-upgrade
```


#### Step 4: Validation gates between stages

After dev stage (30-minute soak):

```
# Run automated test suite
./scripts/run-e2e-tests.sh dev-cluster
./scripts/performance-baseline.sh dev-cluster
# Check for any regressions
kubectl get events --sort-by='.lastTimestamp' | grep -i warn
```


After test stage (60-minute soak):

```
# Extended testing with production-like load
./scripts/load-test.sh test-cluster 1000-users 15-minutes
./scripts/chaos-engineering.sh test-cluster
# Manual approval gate
echo "Approve production deployment? (y/n)"
read approval
```


### Common pitfalls and FAQs

**Expand for quick troubleshooting and tips**

**Stage fails because of quota:**Precheck regional quotas for all clusters in the fleet.**Validation scripts fail:**Ensure that test scripts are idempotent and have clear pass/fail output.**Manual approval delays:**Use automation for nonproduction. Require manual only for production.**Q: Can I use open-source software tools for validation?****A:**Yes. Integrate[Sonobuoy](https://sonobuoy.io/)for conformance and[kube-bench](https://github.com/aquasecurity/kube-bench)for security.

**Q: What's unique to AKS?****A:**Azure Kubernetes Fleet Manager enables true staged rollouts and validation gates natively.


## Scenario 3: Safe Kubernetes version intake

**Challenge:** "I need to adopt Kubernetes 1.30 without breaking existing workloads or APIs."

**Strategy:** Use multiphase validation with canary deployment.

To learn more, see [Canary deployments](/en-us/azure/architecture/reference-architectures/containers/aks-microservices/aks-microservices-advanced#deployment-strategies) and [API deprecation policies](https://kubernetes.io/docs/reference/using-api/deprecation-policy/).

### Implementation steps

#### Step 1: API deprecation analysis

```
# Install and run API deprecation scanner
kubectl apply -f https://github.com/doitintl/kube-no-trouble/releases/latest/download/knt-full.yaml
# Scan for deprecated APIs
kubectl run knt --image=doitintl/knt:latest --rm -it --restart=Never -- \
-c /kubeconfig -o json > api-deprecation-report.json
# Review and remediate findings
cat api-deprecation-report.json | jq '.[] | select(.deprecated==true)'
```


To learn more, see the [Kubernetes API deprecation guide](https://kubernetes.io/docs/reference/using-api/deprecation-guide/) and [kube-no-trouble documentation](https://github.com/doitintl/kube-no-trouble).

#### Step 2: Create a canary environment

```
# Create canary cluster with target version
az aks create \
--resource-group canary-rg \
--name aks-canary-k8s130 \
--kubernetes-version 1.30.0 \
--node-count 2 \
--tier premium \
--enable-addons monitoring
# Deploy subset of workloads
kubectl apply -f ./canary-manifests/
```


#### Step 3: Progressive workload migration

```
# Phase 1: Stateless services (20% traffic)
kubectl patch service api-service -p '{"spec":{"selector":{"version":"canary"}}}'
./scripts/monitor-error-rate.sh 15-minutes
# Phase 2: Background jobs (50% traffic)
kubectl scale deployment batch-processor --replicas=3
./scripts/validate-job-completion.sh
# Phase 3: Critical services (100% traffic)
kubectl patch deployment critical-api -p '{"spec":{"template":{"metadata":{"labels":{"cluster":"canary"}}}}}'
```


#### Step 4: Feature gate validation

```
# Test new Kubernetes 1.30 features
apiVersion: v1
kind: ConfigMap
metadata:
name: feature-validation
data:
test-script: |
# Test new security features
kubectl auth can-i create pods --as=service-account:default:test-sa
# Validate performance improvements
kubectl top nodes --use-protocol-buffers=true
# Check new API versions
kubectl api-versions | grep "v1.30"
```


### Success metrics

**API compatibility:**100% (zero breaking changes)**Performance:**≤5% regression in key metrics**Feature adoption:**New features validated in canary

## Scenario 4: Fastest security patch deployment

**Challenge:** "A critical CVE was announced. I need patches deployed across all clusters within 4 hours."

**Strategy:** Use automated node image patching with minimal disruption.

To learn more, see [Node image upgrade strategies](node-image-upgrade), [Auto-upgrade channels](auto-upgrade-cluster), and [Security patching best practices](/en-us/azure/aks/operator-best-practices-cluster-security).

### Implementation steps

#### Step 1: Emergency response preparation

```
# Set up automated monitoring for security updates
az aks nodepool update \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--auto-upgrade-channel SecurityPatch
# Configure maintenance window for emergency patches
az aks maintenance-configuration create \
--resource-group production-rg \
--cluster-name aks-prod \
--config-name emergency-security \
--week-index First,Second,Third,Fourth \
--day-of-week Monday,Tuesday,Wednesday,Thursday,Friday \
--start-hour 0 \
--duration 4
```


To learn more, see [Planned maintenance configuration](planned-maintenance) and [Autoupgrade channels](auto-upgrade-cluster#cluster-autoupgrade-channels).

#### Step 2: Automated security scanning

```
# security-scan-cronjob.yaml
apiVersion: batch/v1
kind: CronJob
metadata:
name: security-scanner
spec:
schedule: "0 */6 * * *" # Every 6 hours
jobTemplate:
spec:
template:
spec:
containers:
- name: scanner
image: aquasec/trivy:latest
command:
- trivy
- k8s
- --report
- summary
- cluster
```


#### Step 3: Rapid patch deployment

```
# Trigger immediate node image upgrade for security patches
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--node-image-only \
--max-surge 50% \
--drain-timeout 5
# Monitor patch deployment
watch az aks nodepool show \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--query "upgradeSettings"
```


#### Step 4: Compliance validation

```
# Verify patch installation
kubectl get nodes -o wide
kubectl describe node | grep "Kernel Version"
# Generate compliance report
./scripts/generate-security-report.sh > security-compliance-$(date +%Y%m%d).json
# Notify security team
curl -X POST "$SLACK_WEBHOOK" -d "{\"text\":\"Security patches deployed to production cluster. Compliance report attached.\"}"
```


### Success metrics

**Deployment time:**<4 hours from common vulnerabilities and exposures announcement**Coverage:**100% of nodes patched**Downtime:**<5 minutes per node pool

## Scenario 5: Application architecture for seamless upgrades

**Challenge:** "I want my applications to handle cluster upgrades gracefully without affecting users."

**Strategy:** Use resilient application patterns with graceful degradation.

To learn more, see [Application reliability patterns](/en-us/azure/architecture/framework/resiliency/reliability-patterns), [Pod disruption budgets](https://kubernetes.io/docs/tasks/run-application/configure-pdb/), and [Health check best practices](/en-us/azure/architecture/patterns/health-endpoint-monitoring).

### Implementation steps

#### Step 1: Implement robust health checks

```
# robust-health-checks.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
name: resilient-api
spec:
replicas: 3
template:
spec:
containers:
- name: api
image: myapp:latest
readinessProbe:
httpGet:
path: /health/ready
port: 8080
initialDelaySeconds: 10
periodSeconds: 5
timeoutSeconds: 3
successThreshold: 1
failureThreshold: 3
livenessProbe:
httpGet:
path: /health/live
port: 8080
initialDelaySeconds: 30
periodSeconds: 10
timeoutSeconds: 5
failureThreshold: 3
lifecycle:
preStop:
exec:
command: ["/bin/sh", "-c", "sleep 15"]
```


#### Step 2: Configure pod disruption budgets

```
# optimal-pdb.yaml
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: api-pdb
spec:
selector:
matchLabels:
app: api
maxUnavailable: 1
# Ensures at least 2 pods remain available during upgrades
---
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: database-pdb
spec:
selector:
matchLabels:
app: database
minAvailable: 2
# Critical: Always keep majority of database pods running
```


#### Step 3: Implement a circuit breaker pattern

```
// circuit-breaker.js
const CircuitBreaker = require('opossum');
const options = {
timeout: 3000,
errorThresholdPercentage: 50,
resetTimeout: 30000,
fallback: () => 'Service temporarily unavailable'
};
const breaker = new CircuitBreaker(callExternalService, options);
// Monitor circuit breaker state during upgrades
breaker.on('open', () => console.log('Circuit breaker opened'));
breaker.on('halfOpen', () => console.log('Circuit breaker half-open'));
```


To learn more, see [Circuit breaker pattern](/en-us/azure/architecture/patterns/circuit-breaker), [Retry pattern](/en-us/azure/architecture/patterns/retry), and [Application resilience](/en-us/azure/well-architected/reliability/).

#### Step 4: Database connection resilience

```
# connection-pool-config.yaml
apiVersion: v1
kind: ConfigMap
metadata:
name: db-config
data:
database.yml: |
production:
adapter: postgresql
pool: 25
timeout: 5000
retry_attempts: 3
retry_delay: 1000
connection_validation: true
validation_query: "SELECT 1"
test_on_borrow: true
```


### Success metrics

**Error rate:**<0.01% during upgrades**Response time:**<10% degradation**Recovery time:**<30 seconds after node replacement

## Monitoring and alerting setup

To learn more, see the [AKS monitoring overview](monitor-aks), [Container Insights](/en-us/azure/azure-monitor/containers/container-insights-overview), and [Prometheus metrics](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview).

### Essential metrics to monitor

```
# upgrade-monitoring.yaml
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
name: upgrade-monitoring
spec:
groups:
- name: upgrade.rules
rules:
- alert: UpgradeInProgress
expr: kube_node_spec_unschedulable > 0
for: 1m
annotations:
summary: "Node upgrade in progress"
- alert: HighErrorRate
expr: rate(http_requests_total{status=~"5.."}[5m]) > 0.01
for: 2m
annotations:
summary: "High error rate during upgrade"
- alert: PodEvictionFailed
expr: increase(kube_pod_container_status_restarts_total[5m]) > 5
for: 1m
annotations:
summary: "Multiple pod restarts detected"
```


### Dashboard configuration

```
{
"dashboard": {
"title": "AKS Upgrade Dashboard",
"panels": [
{
"title": "Upgrade Progress",
"targets":
[
"kube_node_info",
"kube_node_status_condition"
]
},
{
"title": "Application Health",
"targets":
[
"up{job='kubernetes-pods'}",
"http_request_duration_seconds"
]
}
]
}
}
```


## Troubleshooting guide

To learn more, see the [AKS troubleshooting guide](/en-us/azure/aks/troubleshooting), [Node and pod troubleshooting](node-access), and [Upgrade error messages](upgrade-aks-cluster#troubleshoot-aks-cluster-upgrade-error-messages).

### Common issues and solutions

| Issue | Symptoms | Solution |
|---|---|---|
| Stuck node drain | Pods won't evict. | Check PDB configuration, increase drain timeout. |
| High error rates | 5xx responses are increasing. | Verify health checks, check resource limits. |
| Slow upgrades | Takes >2 hours. | Increase `maxSurge` , optimize container startup. |
| DNS resolution | Service discovery is failing. | Verify `CoreDNS` pods, check service endpoints. |

### Emergency rollback procedures

```
# Quick rollback script
#!/bin/bash
echo "Initiating emergency rollback..."
# Switch traffic back to previous cluster
az network traffic-manager endpoint update \
--resource-group traffic-rg \
--profile-name production-tm \
--name current-endpoint \
--target-resource-id "/subscriptions/.../clusters/aks-previous"
# Verify rollback success
curl -f https://api.production.com/health
echo "Rollback completed in $(date)"
```


## Related resources

### Specialized scenarios

[Stateful workloads](stateful-workload-upgrades): Use PostgreSQL, Redis, and MongoDB upgrade patterns.[Upgrade scenarios hub](upgrade-scenarios-hub): Choose your upgrade path.[Basic AKS upgrades](upgrade-aks-cluster): Find simple cluster version upgrades.

### Supporting tools

[Auto-upgrade configuration](auto-upgrade-cluster): Use automated upgrade channels.[Maintenance windows](planned-maintenance): Schedule upgrade windows.[Upgrade monitoring](aks-communication-manager): Use real-time upgrade alerts.

### Best practices

[Cluster reliability](best-practices-app-cluster-reliability): Design for upgrades.[Security guidelines](operator-best-practices-cluster-security): Use secure upgrade practices.[Support policies](support-policies): Understand upgrade support windows.

## Next tasks

**Set up monitoring:**Configure[upgrade notifications](aks-communication-manager)before your first upgrade.**Practice safely:**Test scenarios in staging by using[cluster snapshots](node-pool-snapshot).**Automate gradually:**Start with[auto-upgrade channels](auto-upgrade-cluster)for nonproduction.**Handle stateful data:**Review[stateful workload patterns](stateful-workload-upgrades)if you run databases.

## Related content

- For more help, see
[AKS support options](aks-support-help)or review[common upgrade scenarios](upgrade-cluster#common-upgrade-scenarios-and-recommendations).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-gateway-api -->

# Configure Istio ingress with the Kubernetes Gateway API for Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

The Istio service mesh add-on supports both [Istio's own ingress traffic management API](istio-deploy-ingress) and the Kubernetes Gateway API for ingress traffic management. You can use the Istio Gateway API [automated deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#automated-deployment) or the [manual deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#manual-deployment). This article describes how to configure ingress traffic management for the Istio service mesh add-on using the Kubernetes Gateway API with the [automated deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#automated-deployment).

## Limitations and considerations

- Using the Kubernetes Gateway API for
[egress traffic management](istio-deploy-egress)with the Istio service mesh add-on is only supported for the[manual deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#manual-deployment). - ConfigMap customizations for
`Gateway`

resources must fall within the Resource customization allow list. Fields not on the allow list are disallowed and blocked via add-on managed webhooks. For more information, see the[Istio service mesh add-on support policy](istio-support-policy#allowed-supported-and-blocked-customizations).

## Prerequisites

- Enable the
[Managed Gateway API](managed-gateway-api)on your AKS cluster. - Install the Istio service mesh add-on revision
`asm-1-26`

or higher. Follow the[installation guide](istio-deploy-addon)if you don't have the Istio service mesh add-on installed yet, or the[upgrade guide](istio-upgrade)if you're on a lower minor revision.

## Set environment variables

Set the following environment variables to use throughout this article:

| Variable | Description |
|---|---|
`RESOURCE_GROUP` |
The name of the resource group containing your AKS cluster. |
`CLUSTER_NAME` |
The name of your AKS cluster. |
`LOCATION` |
The Azure region where your AKS cluster is deployed. |
`KEY_VAULT_NAME` |
The name of the Azure Key Vault resource to be created for storing TLS secrets. If you have an existing resource, use that name. |

## Deploy sample application

Deploy the sample

`httpbin`

application in the`default`

namespace using thecommand.`kubectl apply`

`kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.26/samples/httpbin/httpbin.yaml`


## Create Kubernetes Gateway and HTTPRoute

The example manifest creates an external ingress load balancer service that's accessible from outside the cluster. You can add [annotations](#annotation-customizations) to create an internal load balancer and customize other load balancer settings.

Deploy a Gateway API configuration in the

`default`

namespace with the`gatewayClassName`

set to`istio`

and an`HTTPRoute`

that routes traffic to the`httpbin`

service using the following manifest:`kubectl apply -f - <<EOF apiVersion: gateway.networking.k8s.io/v1 kind: Gateway metadata: name: httpbin-gateway spec: gatewayClassName: istio listeners: - name: http port: 80 protocol: HTTP allowedRoutes: namespaces: from: Same --- apiVersion: gateway.networking.k8s.io/v1 kind: HTTPRoute metadata: name: http namespace: default spec: parentRefs: - name: httpbin-gateway hostnames: ["httpbin.example.com"] rules: - matches: - path: type: PathPrefix value: /get backendRefs: - name: httpbin port: 8000 EOF`

Note

If you're performing a

[minor revision upgrade](istio-upgrade)and have two Istio service mesh add-on revisions installed on your cluster simultaneously, the control plane for the higher minor revision takes ownership of the`Gateways`

by default. You can add the`istio.io/rev`

label to the`Gateway`

to control which control plane revision owns it. If you add the revision label, make sure that you update it accordingly to the appropriate control plane revision before rolling back or completing the upgrade operation.

## Verify resource creation

Verify the

`Deployment`

,`Service`

,`HorizontalPodAutoscaler`

, and`PodDisruptionBudget`

resources were created using the following`kubectl get`

commands:`kubectl get deployment httpbin-gateway-istio kubectl get service httpbin-gateway-istio kubectl get hpa httpbin-gateway-istio kubectl get pdb httpbin-gateway-istio`

Example output:

`# Deployment resource NAME READY UP-TO-DATE AVAILABLE AGE httpbin-gateway-istio 2/2 2 2 31m # Service resource NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE httpbin-gateway-istio LoadBalancer 10.0.65.45 <external-ip> 15021:32053/TCP,80:31587/TCP 33m # HPA resource NAME REFERENCE TARGETS MINPODS MAXPODS REPLICAS AGE httpbin-gateway-istio Deployment/httpbin-gateway-istio cpu: 3%/80% 2 5 3 34m # PDB resource NAME MIN AVAILABLE MAX UNAVAILABLE ALLOWED DISRUPTIONS AGE httpbin-gateway-istio 1 N/A 2 36m`


## Send request to sample application

Try sending a

`curl`

request to the`httpbin`

application. First, set the`INGRESS_HOST`

environment variable:`kubectl wait --for=condition=programmed gateways.gateway.networking.k8s.io httpbin-gateway export INGRESS_HOST=$(kubectl get gateways.gateway.networking.k8s.io httpbin-gateway -ojsonpath='{.status.addresses[0].value}')`

Try sending an HTTP request to

`httpbin`

.`curl -s -I -HHost:httpbin.example.com "http://$INGRESS_HOST/get"`

In the output, you should see an

`HTTP 200`

response.

## Secure Istio ingress traffic with the Kubernetes Gateway API

The Istio service mesh add-on supports syncing secrets from Azure Key Vault for securing Gateway API-based ingress traffic with [Transport Layer Security (TLS) termination](https://istio.io/latest/docs/tasks/traffic-management/ingress/secure-ingress/) or [Server Name Indication (SNI) passthrough](https://istio.io/latest/docs/tasks/traffic-management/ingress/ingress-sni-passthrough/). In the following sections, you sync secrets from Azure Key Vault onto your AKS cluster using the [Azure Key Vault provider for Secrets Store Container Storage Interface (CSI) Driver add-on](csi-secrets-store-driver) and terminate TLS at the ingress gateway.

## Create client/server certificates and keys

Create a root certificate and private key for signing the certificates for sample services:

`mkdir httpbin_certs openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -subj '/O=example Inc./CN=example.com' -keyout httpbin_certs/example.com.key -out httpbin_certs/example.com.crt`

Generate a certificate and a private key for

`httpbin.example.com`

:`openssl req -out httpbin_certs/httpbin.example.com.csr -newkey rsa:2048 -nodes -keyout httpbin_certs/httpbin.example.com.key -subj "/CN=httpbin.example.com/O=httpbin organization" openssl x509 -req -sha256 -days 365 -CA httpbin_certs/example.com.crt -CAkey httpbin_certs/example.com.key -set_serial 0 -in httpbin_certs/httpbin.example.com.csr -out httpbin_certs/httpbin.example.com.crt`


## Set up Azure Key Vault and create secrets

Create an Azure Key Vault instance to supply the certificate and key inputs to the Istio service mesh add-on using the

command. If you already have an Azure Key Vault instance, you can skip this step.`az keyvault create`

`az keyvault create --name $KEY_VAULT_NAME --resource-group $RESOURCE_GROUP --location $LOCATION`

Enable the

[Azure Key Vault provider for Secrets Store (CSI) Driver add-on](csi-secrets-store-driver)on your cluster using thecommand.`az aks enable-addons`

`az aks enable-addons --addons azure-keyvault-secrets-provider --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`

If your key vault uses Azure role-based access control (RBAC) for the permissions model, follow the instructions in

[Provide access to Azure Key Vault keys, certificates, and secrets with Azure role-based access control](/en-us/azure/key-vault/general/rbac-guide)to assign an Azure role of*Key Vault Secrets User*for the add-on's user-assigned managed identity. Alternatively, if your key vault uses the vault access policy permissions model, authorize the user-assigned managed identity of the add-on to access Azure Key Vault resource using access policy using thecommand.`az keyvault set-policy`

`OBJECT_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query 'addonProfiles.azureKeyvaultSecretsProvider.identity.objectId' -o tsv | tr -d '\r') CLIENT_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query 'addonProfiles.azureKeyvaultSecretsProvider.identity.clientId') TENANT_ID=$(az keyvault show --resource-group $RESOURCE_GROUP --name $KEY_VAULT_NAME --query 'properties.tenantId') az keyvault set-policy --name $KEY_VAULT_NAME --object-id $OBJECT_ID --secret-permissions get list`

Create secrets in Azure Key Vault using the certificates and keys using the following

commands:`az keyvault secret set`

`az keyvault secret set --vault-name $KEY_VAULT_NAME --name test-httpbin-key --file httpbin_certs/httpbin.example.com.key az keyvault secret set --vault-name $KEY_VAULT_NAME --name test-httpbin-crt --file httpbin_certs/httpbin.example.com.crt`


## Deploy SecretProviderClass and sample pod

Deploy the SecretProviderClass to provide Azure Key Vault specific parameters to the CSI driver using the following manifest. In this example,

`test-httpbin-key`

and`test-httpbin-crt`

are the names of the secret objects in Azure Key Vault.`cat <<EOF | kubectl apply -f - apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: httpbin-credential-spc spec: provider: azure secretObjects: - secretName: httpbin-credential type: kubernetes.io/tls data: - objectName: test-httpbin-key key: tls.key - objectName: test-httpbin-crt key: tls.crt parameters: useVMManagedIdentity: "true" userAssignedIdentityID: $CLIENT_ID keyvaultName: $KEY_VAULT_NAME cloudName: "" objects: | array: - | objectName: test-httpbin-key objectType: secret objectAlias: "test-httpbin-key" - | objectName: test-httpbin-crt objectType: secret objectAlias: "test-httpbin-crt" tenantId: $TENANT_ID EOF`

Note

Alternatively, to reference a certificate object type directly from Azure Key Vault, use the following manifest to deploy SecretProviderClass. In this example,

`test-httpbin-cert-pxf`

is the name of the certificate object in Azure Key Vault.`cat <<EOF | kubectl apply -f - apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: httpbin-credential-spc spec: provider: azure secretObjects: - secretName: httpbin-credential type: kubernetes.io/tls data: - objectName: test-httpbin-key key: tls.key - objectName: test-httpbin-crt key: tls.crt parameters: useVMManagedIdentity: "true" userAssignedIdentityID: $CLIENT_ID keyvaultName: $KEY_VAULT_NAME cloudName: "" objects: | array: - | objectName: test-httpbin-cert-pfx #certificate object name from keyvault objectType: secret objectAlias: "test-httpbin-key" - | objectName: test-httpbin-cert-pfx #certificate object name from keyvault objectType: cert objectAlias: "test-httpbin-crt" tenantId: $TENANT_ID EOF`

Deploy a sample pod using the following manifest. The Azure Key Vault provider for Secrets Store (CSI) Driver add-on requires a pod to reference the SecretProviderClass resource to ensure secrets sync from Azure Key Vault to the cluster.

`cat <<EOF | kubectl apply -f - apiVersion: v1 kind: Pod metadata: name: secrets-store-sync-httpbin spec: containers: - name: busybox image: mcr.microsoft.com/oss/busybox/busybox:1.33.1 command: - "/bin/sleep" - "10" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "httpbin-credential-spc" EOF`


## Verify TLS secret creation

Verify the

`httpbin-credential`

secret was created in the`default`

namespace as defined in the SecretProviderClass resource using the`kubectl describe secret`

command.`kubectl describe secret/httpbin-credential`

Example output:

`Name: httpbin-credential Namespace: default Labels: secrets-store.csi.k8s.io/managed=true Annotations: <none> Type: kubernetes.io/tls Data ==== tls.crt: 1180 bytes tls.key: 1675 bytes`


## Deploy TLS Gateway

Create a Kubernetes Gateway that references the

`httpbin-credential`

secret under the TLS configuration using the following manifest:`cat <<EOF | kubectl apply -f - apiVersion: gateway.networking.k8s.io/v1 kind: Gateway metadata: name: httpbin-gateway spec: gatewayClassName: istio listeners: - name: https hostname: "httpbin.example.com" port: 443 protocol: HTTPS tls: mode: Terminate certificateRefs: - name: httpbin-credential allowedRoutes: namespaces: from: Selector selector: matchLabels: kubernetes.io/metadata.name: default EOF`

Note

In the gateway definition,

`tls.certificateRefs.name`

must match the`secretName`

in SecretProviderClass resource.Create a corresponding

`HTTPRoute`

to configure ingress traffic routing to the`httpbin`

service over HTTPS using the following manifest:`cat <<EOF | kubectl apply -f - apiVersion: gateway.networking.k8s.io/v1 kind: HTTPRoute metadata: name: httpbin spec: parentRefs: - name: httpbin-gateway hostnames: ["httpbin.example.com"] rules: - matches: - path: type: PathPrefix value: /status - path: type: PathPrefix value: /delay backendRefs: - name: httpbin port: 8000 EOF`

Get the ingress gateway's external IP address and secure port using the following commands:

`kubectl wait --for=condition=programmed gateways.gateway.networking.k8s.io httpbin-gateway export INGRESS_HOST=$(kubectl get gateways.gateway.networking.k8s.io httpbin-gateway -o jsonpath='{.status.addresses[0].value}') export SECURE_INGRESS_PORT=$(kubectl get gateways.gateway.networking.k8s.io httpbin-gateway -o jsonpath='{.spec.listeners[?(@.name=="https")].port}')`

Send an HTTPS request to access the

`httpbin`

service:`curl -v -HHost:httpbin.example.com --resolve "httpbin.example.com:$SECURE_INGRESS_PORT:$INGRESS_HOST" \ --cacert httpbin_certs/example.com.crt "https://httpbin.example.com:$SECURE_INGRESS_PORT/status/418"`

The output should show the

`httpbin`

service return the*418 I’m a Teapot*code.Note

To configure HTTPS ingress access to an HTTPS service, update the TLS mode in the gateway definition to

`Passthrough`

. This configuration instructs the gateway to pass the ingress traffic*as is*, without terminating TLS.

## Annotation customizations

You can add annotations under `spec.infrastructure.annotations`

to [configure load balancer settings](configure-load-balancer-standard#customizations-via-kubernetes-annotations) for the `Gateway`

. For instance, to create an internal load balancer attached to a specific subnet, you can create a `Gateway`

with the following annotations:

```
spec:
# ... existing spec content ...
infrastructure:
annotations:
service.beta.kubernetes.io/azure-load-balancer-internal: "true"
service.beta.kubernetes.io/azure-load-balancer-internal-subnet: "my-subnet"
```


## ConfigMap customizations

The Istio service mesh add-on supports [customizations of the resources](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#automated-deployment) generated for the `Gateways`

, including:

- Service
- Deployment
- Horizontal Pod Autoscaler (HPA)
- Pod Disruption Budget (PDB)

The [default settings for these resources](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#gatewayclass-defaults) are set in the `istio-gateway-class-defaults`

ConfigMap in the `aks-istio-system`

namespace. This ConfigMap must have the `gateway.istio.io/defaults-for-class`

label set to `istio`

for the customizations to take effect for all `Gateways`

with `spec.gatewayClassName: istio`

. The `GatewayClass`

-level ConfigMap is installed by default in the `aks-istio-system`

namespace when the [Managed Gateway API installation](managed-gateway-api) is enabled. It could take up to five minutes for the `istio-gateway-class-defaults`

ConfigMap to get deployed after installing the Managed Gateway API CRDs.

```
kubectl get configmap istio-gateway-class-defaults -n aks-istio-system -o yaml
```


```
...
data:
horizontalPodAutoscaler: |
spec:
minReplicas: 2
maxReplicas: 5
podDisruptionBudget: |
spec:
minAvailable: 1
...
```


You can modify these settings for all Istio `Gateways`

at a `GatewayClass`

level by updating the `istio-gateway-class-defaults`

ConfigMap, or you can set them for individual `Gateway`

resources. For both the `GatewayClass`

-level and `Gateway`

-level `ConfigMaps`

, you must add fields to the allow list for the given resource. If there are customizations both for the `GatewayClass`

and an individual `Gateway`

, the `Gateway`

-level configuration takes precedence.

## Deployment customization allow list fields

| Field path | Description |
|---|---|
`metadata.labels` |
Deployment labels |
`metadata.annotations` |
Deployment annotations |
`spec.replicas` |
Deployment replica count |
`spec.template.metadata.labels` |
Pod labels |
`spec.template.metadata.annotations` |
Pod annotations |
`spec.template.spec.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms` |
Node affinity |
`spec.template.spec.affinity.nodeAffinity.preferredDuringSchedulingIgnoredDuringExecution` |
Node affinity |
`spec.template.spec.affinity.podAffinity.requiredDuringSchedulingIgnoredDuringExecution` |
Pod affinity |
`spec.template.spec.affinity.podAffinity.preferredDuringSchedulingIgnoredDuringExecution` |
Pod affinity |
`spec.template.spec.affinity.podAntiAffinity.requiredDuringSchedulingIgnoredDuringExecution` |
Pod anti-affinity |
`spec.template.spec.affinity.podAntiAffinity.preferredDuringSchedulingIgnoredDuringExecution` |
Pod anti-affinity |
`spec.template.spec.containers.resizePolicy` |
Container resource utilization |
`spec.template.spec.containers.resources.limits` |
Container resource utilization |
`spec.template.spec.containers.resources.requests` |
Container resource utilization |
`spec.template.spec.containers.stdin` |
Container debugging |
`spec.template.spec.containers.stdinOnce` |
Container debugging |
`spec.template.spec.nodeSelector` |
Pod scheduling |
`spec.template.spec.nodeName` |
Pod scheduling |
`spec.template.spec.tolerations` |
Pod scheduling |
`spec.template.spec.topologySpreadConstraints` |
Pod scheduling |

## Service customization allow list fields

| Field path | Description |
|---|---|
`metadata.labels` |
Service labels |
`metadata.annotations` |
Service annotations |
`spec.type` |
Service type |
`spec.loadBalancerSourceRanges` |
Service load balancer settings |
`spec.loadBalancerClass` |
Service load balancer settings |
`spec.externalTrafficPolicy` |
Service traffic policy |
`spec.internalTrafficPolicy` |
Service traffic policy |

## HorizontalPodAutoscaler (HPA) customization allow list fields

| Field path | Description |
|---|---|
`metadata.labels` |
HPA labels |
`metadata.annotations` |
HPA annotations |
`spec.behavior.scaleUp.stabilizationWindowSeconds` |
HPA scale-up behavior |
`spec.behavior.scaleUp.selectPolicy` |
HPA scale-up behavior |
`spec.behavior.scaleUp.policies` |
HPA scale-up behavior |
`spec.behavior.scaleDown.stabilizationWindowSeconds` |
HPA scale-down behavior |
`spec.behavior.scaleDown.selectPolicy` |
HPA scale-down behavior |
`spec.behavior.scaleDown.policies` |
HPA scale-down behavior |
`spec.metrics` |
HPA scaling resource metrics |
`spec.minReplicas` |
HPA minimum replica count. Must not be below 2. |
`spec.maxReplicas` |
HPA maximum replica count |

## PodDisruptionBudget (PDB) customization allow list fields

| Field path | Description |
|---|---|
`metadata.labels` |
PDB labels |
`metadata.annotations` |
PDB annotations |
`spec.minAvailable` |
PDB minimum availability |
`spec.unhealthyPodEvictionPolicy` |
PDB eviction policy |

Note

Modifying the `PDB`

minimum availability and eviction policy can lead to potential errors during cluster/node upgrade and deletion operations. Follow the [PDB troubleshooting guide](/en-us/troubleshoot/azure/azure-kubernetes/create-upgrade-delete/error-code-poddrainfailure) to address *UpgradeFailed* errors due to `PDB`

eviction failures.

## Configure GatewayClass-level settings

Update the

`GatewayClass`

-level ConfigMap in the`aks-istio-system`

namespace using the`kubectl edit configmap`

command:`kubectl edit cm istio-gateway-class-defaults -n aks-istio-system`

Edit the resource settings in the

`data`

section as needed. For example, to update the HPA min/max replicas and add a label to the`Deployment`

, modify the ConfigMap as follows:`... data: deployment: | metadata: labels: test.azureservicemesh.io/deployment-config: "updated" horizontalPodAutoscaler: | spec: minReplicas: 3 maxReplicas: 6 podDisruptionBudget: | spec: minAvailable: 1 ...`

Note

Only one ConfigMap per

`GatewayClass`

is allowed.Now, you should see the

`HPA`

for`httpbin-gateway`

that you created earlier get updated with the new min/max values. Verify the`HPA`

settings using the`kubectl get hpa`

command.`kubectl get hpa httpbin-gateway-istio`

Example output:

`NAME REFERENCE TARGETS MINPODS MAXPODS REPLICAS AGE httpbin-gateway-istio Deployment/httpbin-gateway-istio cpu: 3%/80% 3 6 3 36m`

Verify the

`Deployment`

is updated with the new label using the`kubectl get deployment`

command.`kubectl get deployment httpbin-gateway-istio -ojsonpath='{.metadata.labels.test\.azureservicemesh\.io\/deployment-config}'`

Example output:

`updated`


## Configure settings for a specific gateway

Create a ConfigMap with resource customizations for the

`httpbin`

Gateway using the following manifest:`kubectl apply -f - <<EOF apiVersion: v1 kind: ConfigMap metadata: name: gw-options data: horizontalPodAutoscaler: | spec: minReplicas: 2 maxReplicas: 4 deployment: | metadata: labels: test.azureservicemesh.io/deployment-config: "updated-per-gateway" EOF`

Update the

`httpbin`

`Gateway`

to reference the ConfigMap:`spec: # ... existing spec content ... infrastructure: parametersRef: group: "" kind: ConfigMap name: gw-options`

Apply the update using the

`kubectl apply`

command.`kubectl apply -f httpbin-gateway-updated.yaml`

Verify the

`HPA`

is updated with the new min/max values using the`kubectl get hpa`

command. If you also configured the`GatewayClass`

-level ConfigMap, the`Gateway`

-level settings should take precedence.`kubectl get hpa httpbin-gateway-istio`

Example output:

`NAME REFERENCE TARGETS MINPODS MAXPODS REPLICAS AGE httpbin-gateway-istio Deployment/httpbin-gateway-istio cpu: 3%/80% 2 4 2 4h14m`

Inspect the

`Deployment`

labels to ensure that the`test.azureservicemesh.io/deployment-config`

is updated to the new value using the`kubectl get deployment`

command.`kubectl get deployment httpbin-gateway-istio -ojsonpath='{.metadata.labels.test\.azureservicemesh\.io\/deployment-config}'`

Example output:

`updated-per-gateway`


## Clean up resources

If you no longer need the resources created in this article, you can delete them to avoid incurring any charges.

Delete the Gateway and HTTPRoute resources using the following

`kubectl delete`

commands:`kubectl delete gateways.gateway.networking.k8s.io httpbin-gateway kubectl delete httproute httpbin`

If you created a ConfigMap to customize your Gateway resources, delete it using the

`kubectl delete configmap`

command.`kubectl delete configmap gw-options`

If you created a SecretProviderClass and secret to use for TLS termination delete the resources using the following

`kubectl delete`

commands:`kubectl delete secret httpbin-credential kubectl delete pod secrets-store-sync-httpbin kubectl delete secretproviderclass httpbin-credential-spc`

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-windows-gpu -->

# Use Windows GPUs for compute-intensive workloads on Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Graphical processing units (GPUs) are often used for compute-intensive workloads, such as graphics and visualization workloads. AKS supports GPU-enabled Windows and [Linux](gpu-cluster) node pools to run compute-intensive Kubernetes workloads.

This article helps you provision Windows nodes with schedulable GPUs on new and existing AKS clusters (preview).

## Supported GPU-enabled virtual machines (VMs)

To view supported GPU-enabled VMs, see [GPU-optimized VM sizes in Azure](/en-us/azure/virtual-machines/sizes-gpu). For AKS node pools, we recommend a minimum size of *Standard_NC6s_v3*. The NVv4 series (based on AMD GPUs) aren't supported on AKS.

Note

GPU-enabled VMs contain specialized hardware subject to higher pricing and region availability. For more information, see the [pricing](https://azure.microsoft.com/pricing/) tool and [region availability](https://azure.microsoft.com/global-infrastructure/services/).

## Limitations

- Updating an existing Windows node pool to add GPU isn't supported.
- Not supported on Kubernetes version 1.28 and below.

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-windows-container-deploy-cli),[Azure PowerShell](learn/quick-windows-container-deploy-powershell), or the[Azure portal](learn/quick-windows-container-deploy-portal). - You need the Azure CLI version 2.72.2 or later installed and configured to use the
`--gpu-driver`

field with the`az aks nodepool add`

command. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you have the
`aks-preview`

Azure CLI extension installed, please update the version to 18.0.0b2 or later.

## Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command. The following example command gets the credentials for the`az aks get-credentials`

*myAKSCluster*in the*myResourceGroup*resource group:`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Using Windows GPU with automatic driver installation

Using NVIDIA GPUs involves the installation of various NVIDIA software components such as the [DirectX device plugin for Kubernetes](https://github.com/aarnaud/k8s-directx-device-plugin), GPU driver installation, and more. When you create a Windows node pool with a supported GPU-enabled VM, these components and the appropriate NVIDIA CUDA or GRID drivers are installed. For NC and ND series VM sizes, the CUDA driver is installed. For NV series VM sizes, the GRID driver is installed.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Install the `aks-preview`

Azure CLI extension

Register or update the aks-preview extension using the

or`az extension add`

command.`az extension update`

`# Register the aks-preview extension az extension add --name aks-preview # Update the aks-preview extension az extension update --name aks-preview`


### Register the `WindowsGPUPreview`

feature flag

Register the

`WindowsGPUPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "WindowsGPUPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "WindowsGPUPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create a Windows GPU-enabled node pool (preview)

To create a Windows GPU-enabled node pool, you need to use a supported GPU-enabled VM size and specify the `os-type`

as `Windows`

. The default Windows `os-sku`

is `Windows2022`

, but all Windows `os-sku`

options are supported.

Create a Windows GPU-enabled node pool using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --os-type Windows \ --kubernetes-version 1.29.0 \ --node-vm-size Standard_NC6s_v3`

Check that your

[GPUs are schedulable](#confirm-that-gpus-are-schedulable).Once you confirm that your GPUs are schedulable, you can run your GPU workload.


#### Specify GPU Driver Type (preview)

By default, AKS specifies a default GPU driver type for each supported GPU-enabled VM. Because workload and driver compatibility are important for functioning GPU workloads, you can specify the driver type for your Windows GPU node. This feature is not supported for Linux GPU node pools.

When creating a Windows agent pool with GPU support, you have the option to specify the type of GPU driver using the `--driver-type`

flag.

The available options are:

- GRID: For applications requiring virtualization support.
- CUDA: Optimized for computational tasks in scientific computing and data-intensive applications.

Note

When you set the `--driver-type`

flag, you assume responsibility for ensuring that the selected driver type is compatible with the specific VM size and configuration of your node pool. While AKS attempts to validate compatibility, there are scenarios where the node pool creation might fail due to incompatibilities between the specified driver type and the underlying VM or hardware.

To create a Windows GPU-enabled node pool with a specific GPU Driver type, use the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name gpunp \
--node-count 1 \
--os-type Windows \
--kubernetes-version 1.29.0 \
--node-vm-size Standard_NC6s_v3 \
--driver-type GRID
```


For example, the above command creates a GPU-enabled node pool using the `GRID`

GPU driver type. Selecting this driver type overrides the default of `CUDA`

driver type for NC series VM skus.

## Using Windows GPU with manual driver installation

When creating a Windows node pool with N-series (NVIDIA GPU) VM sizes in AKS, the GPU driver and Kubernetes DirectX device plugin are installed automatically. To bypass this automatic installation, use the following steps:

[Skip GPU driver installation](#skip-gpu-driver-installation)by setting the configuration`--gpu-driver none`

at node pool create time.[Manual installation of the Kubernetes DirectX device plugin](#manually-install-the-kubernetes-directx-device-plugin).

### Skip GPU driver installation

AKS has automatic GPU driver installation enabled by default. In some cases, such as installing your own drivers, you may want to skip GPU driver installation.

Important

Starting on **August 14, 2025**, Azure Kubernetes Service (AKS) no longer supports the `--skip-gpu-driver-install`

node pool tag. After this date, you'll be unable to provision GPU-enabled node pools using this tag to bypass automatic GPU driver installation. You can achieve the same behavior by setting the `--gpu-driver`

field to `none`

. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4925) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=496440). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Create a node pool using the

command and setting the API field`az aks nodepool add`

`--gpu-driver`

to`none`

to skip automatic GPU driver installation.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --os-type windows \ --os-sku windows2022 \ --gpu-driver none`


Note

If the `--node-vm-size`

that you're using isn't yet onboarded on AKS, you can't use GPUs and the `--gpu-driver`

field doesn't work.

### Manually install the Kubernetes DirectX device plugin

You can deploy a DaemonSet for the Kubernetes DirectX device plugin, which runs a pod on each node to provide the required drivers for the GPUs.

Add a node pool to your cluster using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --os-type windows \ --os-sku windows2022`


## Create a namespace and deploy the Kubernetes DirectX device plugin

Create a namespace using the

command.`kubectl create namespace`

`kubectl create namespace gpu-resources`

Create a file named

*k8s-directx-device-plugin.yaml*and paste the following YAML manifest provided as part of the[NVIDIA device plugin for Kubernetes project](https://github.com/NVIDIA/k8s-device-plugin):`apiVersion: apps/v1 kind: DaemonSet metadata: name: nvidia-device-plugin-daemonset namespace: gpu-resources spec: selector: matchLabels: name: nvidia-device-plugin-ds updateStrategy: type: RollingUpdate template: metadata: # Mark this pod as a critical add-on; when enabled, the critical add-on scheduler # reserves resources for critical add-on pods so that they can be rescheduled after # a failure. This annotation works in tandem with the toleration below. annotations: scheduler.alpha.kubernetes.io/critical-pod: "" labels: name: nvidia-device-plugin-ds spec: tolerations: # Allow this pod to be rescheduled while the node is in "critical add-ons only" mode. # This, along with the annotation above marks this pod as a critical add-on. - key: CriticalAddonsOnly operator: Exists - key: nvidia.com/gpu operator: Exists effect: NoSchedule - key: "sku" operator: "Equal" value: "gpu" effect: "NoSchedule" containers: - image: mcr.microsoft.com/aks/aks-windows-gpu-device-plugin:0.0.17 name: nvidia-device-plugin-ctr securityContext: allowPrivilegeEscalation: false capabilities: drop: ["ALL"] volumeMounts: - name: device-plugin mountPath: /var/lib/kubelet/device-plugins volumes: - name: device-plugin hostPath: path: /var/lib/kubelet/device-plugins`

Create the DaemonSet and confirm the NVIDIA device plugin is created successfully using the

command.`kubectl apply`

`kubectl apply -f nvidia-device-plugin-ds.yaml`

Now that you successfully installed the NVIDIA device plugin, you can check that your

[GPUs are schedulable](#confirm-that-gpus-are-schedulable).

## Confirm that GPUs are schedulable

After creating your cluster, confirm that GPUs are schedulable in Kubernetes.

List the nodes in your cluster using the

command.`kubectl get nodes`

`kubectl get nodes`

Your output should look similar to the following example output:

`NAME STATUS ROLES AGE VERSION aks-gpunp-28993262-0 Ready agent 13m v1.20.7`

Confirm the GPUs are schedulable using the

command.`kubectl describe node`

`kubectl describe node aks-gpunp-28993262-0`

Under the

*Capacity*section, the GPU should list as`microsoft.com/directx: 1`

. Your output should look similar to the following condensed example output:`Capacity: [...] microsoft.com.directx/gpu: 1 [...]`


## Clean up resources

Remove the associated Kubernetes objects you created in this article using the

command.`kubectl delete job`

`kubectl delete jobs windows-gpu-workload`


## Next steps

- To run Apache Spark jobs, see
[Run Apache Spark jobs on AKS](spark-job). - For more information on features of the Kubernetes scheduler, see
[Best practices for advanced scheduler features in AKS](operator-best-practices-advanced-scheduler). - For more information on Azure Kubernetes Service and Azure Machine Learning, see:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-aks-node-pools-rolling -->

# Configure rolling upgrades for Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A rolling upgrade strategy upgrades nodes one at a time (or a few at a time), minimizing workload disruption while ensuring the node pool remains available throughout the upgrade process. This article explains how to configure rolling upgrades for AKS node pools, including surge settings, drain timeout, and soak time.

## Before you begin

- Ensure your control plane is already upgraded to the target Kubernetes version. You can't upgrade node pools to a version higher than the control plane. For more information, see
[Upgrade the AKS cluster control plane](upgrade-aks-control-plane). - If you're using the Azure CLI, this article requires Azure CLI version 2.34.1 or later. Use the
`az --version`

command to find the version. If you need to install or upgrade, see [Install Azure CLI][azure-cli-install]. - You need the
`Microsoft.ContainerService/managedClusters/agentPools/write`

RBAC role permission to configure rolling upgrades for AKS node pools.

## Overview of rolling upgrade behavior

During a rolling upgrade, AKS performs the following operations for each node in the node pool:

**Add surge nodes**: Add new buffer nodes based on max surge (`--max-surge`

) settings to maintain capacity during the upgrade.**Cordon and drain nodes**:[Cordon and drain](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)the old nodes one at a time to minimize disruption to running applications. If you're using max surge, it cordons and drains as many nodes at the same time as the number of buffer nodes specified.**Wait for soak time**(optional): Wait for a configured[soak duration](#set-node-soak-time-value)before proceeding to allow workloads to stabilize on the new nodes before continuing the upgrade.**Reimage old nodes**: When the old nodes are drained, they're reimaged to receive the new version. The reimaged nodes become the buffer nodes for the next set of nodes to be upgraded.**Repeat**: The process repeats until all nodes in the node pool are upgraded.**Remove surge nodes**: After all nodes are upgraded, any remaining buffer nodes are removed, maintaining the original node pool size and balance.

## Configure rolling upgrade settings

### Customize node surge

Important

- Node surges require subscription quota for the requested max surge count for each upgrade operation. For example, a cluster that has five node pools, each with a count of four nodes, has a total of 20 nodes. If each node pool has a max surge value of 50%, extra compute and IP quota of 10 nodes (
*two*nodes ×*five*pools) is required to complete the upgrade. - The max surge setting on a node pool is persistent. Subsequent Kubernetes upgrades or node version upgrades use this setting. You can change the max surge value for your node pools at any time. For production node pools, we recommend a max surge setting of 33%.
- If you're using Azure CNI, validate there are available IPs in the subnet to
[satisfy IP requirements of Azure CNI](configure-azure-cni).

AKS configures upgrades to surge with one extra node by default. A default value of *one* for the max surge setting enables AKS to minimize workload disruption by creating an extra node before the cordon/drain of existing applications to replace an older versioned node. You can customize the max surge value per node pool. When you increase the max surge value, the upgrade process completes faster, but you might experience more disruptions during the upgrade process.

For example, a max surge value of `100%`

provides the fastest possible upgrade process but also causes all nodes in the node pool to be drained simultaneously. You might want to use a higher value like this for testing environments. For production node pools, we recommend a max surge setting of `33%`

.

AKS accepts both integer values and a percentage value for max surge. For example:

| Value type | Example | Description |
|---|---|---|
| Integer | `5` |
Five extra nodes to surge |
| Percentage | `50%` |
Surge value of half the current node count in the pool |

Max surge percent values can be a minimum of `1%`

and a maximum of `100%`

. A percent value is rounded up to the nearest node count. If the max surge value is higher than the required number of nodes to be upgraded, the number of nodes to be upgraded is used for the max surge value.

#### Set max surge value

Set max surge values for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) or

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

`--max-surge`

parameter. For example:```
# Set max surge for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 33%
# Update max surge for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 5
```


### Customize unavailable nodes

Important

- You must set max surge to
`0`

in order to set a max unavailable value. The two values can't both be active at the same time. - Max unavailable doesn't create surge nodes during the upgrade process. Instead, AKS cordons
*n*nodes (the max unavailable value) at a time and evicts the pods to other nodes in the agent pool. This might cause workload disruptions if the pods can't be scheduled. - Max unavailable might cause more failures due to unsatisfied Pod Disruption Budgets (PDBs) since there are fewer resources for pods to be scheduled on. For more information, see
[Troubleshooting for Pod Disruption Budgets](/en-us/troubleshoot/azure/azure-kubernetes/create-upgrade-delete/error-code-poddrainfailure). - You can't set max unavailable on system node pools.

AKS can also configure upgrades to not use a surge node and upgrade the nodes in place. The max unavailable value determines how many nodes can be simultaneously cordoned and drained from the existing node pool nodes.

AKS accepts both integer values and a percentage value for max unavailable. For example:

| Value type | Example | Description |
|---|---|---|
| Integer | `5` |
Five nodes are cordoned from the existing nodes |
| Percentage | `50%` |
Half the current node count in the pool will be unavailable |

Max unavailable percent values can be a minimum of `1%`

and a maximum of `100%`

. A percent value is rounded up to the nearest node count.

#### Set max unavailable value

Set max unavailable values for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add),

[, or the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade)

`az aks nodepool upgrade`

`--max-unavailable`

parameter. For example:```
# Set max unavailable for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 0 \
--max-unavailable 5
# Update max unavailable for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 0 \
--max-unavailable 5
# Set max unavailable at upgrade time
az aks nodepool upgrade \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 0 \
--max-unavailable 5
```


### Customize node drain timeout

You might have long-running workloads on certain pods that you can't reschedule to another node during runtime. For example, a memory-intensive stateful workload that must finish running. In these cases, you can configure a node drain timeout that AKS respects in the upgrade workflow.

The default node drain timeout value is 30 minutes. Node drain timeout values can be a minimum of 5 minutes and a maximum of 24 hours.

If the drain timeout value elapses and pods are still running, the upgrade operation stops. Any subsequent `PUT`

operation resumes the stopped upgrade.

Tip

For long-running pods, you should also configure the [ terminationGracePeriodSeconds](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) in your pod spec.

#### Set node drain timeout value

Set node drain timeout (in minutes) for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) or

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

`--drain-time-out`

parameter.```
# Set drain timeout for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--drain-time-out 100
# Update drain timeout for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--drain-time-out 45
```


### Customize node soak time

To enable a waiting period for a specified duration of time between draining a node and proceeding to reimage it and move on to the next node, you can set the soak time. This soak time gives you the opportunity to perform other tasks during the upgrade process, such as checking application health from a monitoring dashboard.

The default node soak time is 0 minutes. Node soak time values can be a minimum of 0 minutes and a maximum of 30 minutes. We recommend keeping soak time as short as reasonably possible. A higher node soak time increases the total upgrade duration and delays discovery of issues.

#### Set node soak time value

Set node soak time (in minutes) for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add),

[, or](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade)

`az aks nodepool upgrade`

`--node-soak-duration`

flag.```
# Set node soak time for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--node-soak-duration 10
# Update node soak time for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 33% \
--node-soak-duration 5
# Set node soak time when upgrading an existing node pool
az aks nodepool upgrade \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 33% \
--node-soak-duration 20
```


## View AKS node upgrade events

View upgrade events using the `kubectl get events`

command to monitor the rolling upgrade progress.

```
kubectl get events --field-selector reason=Drain,reason=Surge,reason=Upgrade
```


Example output during an upgrade event:

```
default 2m1s Normal Drain node/aks-nodepool1-12345678-vmss000001 Draining node: [aks-nodepool1-12345678-vmss000001]
default 9m22s Normal Surge node/aks-nodepool1-12345678-vmss000002 Created a surge node [aks-nodepool1-12345678-vmss000002 nodepool1] for agentpool nodepool1
default 1m45s Normal Upgrade node/aks-nodepool1-12345678-vmss000001 Soak duration 5m0s after draining node: aks-nodepool1-12345678-vmss000001
```


## Recommended AKS node pool upgrade settings for production workloads

The following table outlines recommended node pool upgrade settings for production workloads:

| Setting | Recommendation |
|---|---|
Max surge |
Set to 33% for production node pools |
Drain timeout |
Configure based on your longest-running pod's requirements |
Soak time |
Use a short duration (0-5 minutes) unless you need manual verification |
Pod Disruption Budgets |
Configure PDBs for critical workloads to control pod eviction |
Upgrade order |
Upgrade non-production node pools first to validate the new version |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-upgrade-image -->

# Node image updates for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of node image updates for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS), including how it works, recommended maintenance windows, and examples to get started.

## How do node image updates work for node auto-provisioning nodes?

By default, NAP node pool virtual machines (VMs) are automatically updated when a new image version is available. You can configure an [AKS-managed node operating system (OS) upgrade schedule maintenance window](#node-os-upgrade-maintenance-windows-for-nap) to control when new images are picked up and applied to your NAP nodes, or [use Karpenter Node Disruption Budgets and Pod Disruption Budgets](#karpenter-node-disruption-budgets-and-pod-disruption-budgets-for-nap) to control how and when disruption occurs during upgrades.

Note

NAP forces the latest image version to be picked up if the existing node image version is older than 90 days. This bypasses any existing maintenance window.

## Node OS upgrade maintenance windows for NAP

You can use the [AKS planned maintenance feature](planned-maintenance) with a [node OS auto-upgrade channel](auto-upgrade-node-os-image) to configure a `aksManagedNodeOSUpgradeSchedule`

maintenance window that controls when to perform node OS security patching scheduled by your designated node OS auto-upgrade channel.

### Node OS upgrade maintenance window behavior and considerations

Keep the following information in mind when configuring a node OS upgrade maintenance window for NAP:

- The
`aksManagedNodeOSUpgradeSchedule`

maintenance configuration determines the window during which NAP picks up a new image. This configuration doesn't necessarily determine when existing nodes are disrupted. - The upgrade mechanism and decision criteria are specific to NAP/Karpenter and are evaluated by NAP's drift logic. NAP respects Karpenter Node Disruption Budgets and Pod Disruption Budgets. For more information about drift, see the
[Karpenter drift documentation](https://karpenter.sh/docs/concepts/disruption/#drift). - These NAP upgrade decisions are separate from the cluster
`NodeImage`

and`SecurityPatch`

channels. However, the`aksManagedNodeOSUpgradeSchedule`

maintenance configuration applies them as well. - We recommend using a maintenance window of four hours or more for reliable operation.
- If no maintenance configuration exists, AKS might use a fallback schedule to pick up new images, which can cause images to be picked up at unexpected times. You can avoid unexpected timing of new images and upgrades by defining an explicit
`aksManagedNodeOSUpgradeSchedule`

. - Allow at least 30 minutes between creating or updating a maintenance configuration and the scheduled start time to ensure AKS has time to reconcile the new configuration.

### Recommended schedule pattern for NAP-managed nodes

We recommend the following schedule pattern for NAP-managed nodes:

**Weekly cadence**: Recommended for routine node image roll outs (for example:*Every week on Sunday*).

## Create a node OS maintenance schedule example

The following sections show you how to create a weekly maintenance window for NAP-managed nodes using the Azure CLI and a JSON configuration file and how to update, view, list, and delete the maintenance configuration.

### Create a maintenance configuration

Create a JSON file named

`nodeosMaintenance.json`

with a weekly maintenance window (for example:*Sunday at 01:00 UTC for 4 hours*).`{ "properties": { "maintenanceWindow": { "durationHours": 4, "schedule": { "weekly": { "intervalWeeks": 1, "dayOfWeek": "Sunday" } }, "startDate": "2025-01-01", "startTime": "01:00", "utcOffset": "+00:00" } } }`

Add the maintenance configuration to your cluster using the

command.`az aks maintenanceconfiguration add`

`az aks maintenanceconfiguration add \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule \ --config-file ./nodeosMaintenance.json`


### Update, view, list, or delete a maintenance configuration

You can use the following commands to update, view, list, or delete a maintenance configuration for NAP-managed nodes:

Update a maintenance configuration by modifying the JSON file and then running the

command.`az aks maintenanceconfiguration update`

`az aks maintenanceconfiguration update \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule \ --config-file ./nodeosMaintenance.json`

View the details of a maintenance configuration using the

command.`az aks maintenanceconfiguration show`

`az aks maintenanceconfiguration show \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule`

List all maintenance configurations for your cluster using the

command.`az aks maintenanceconfiguration list`

`az aks maintenanceconfiguration list \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME`

Delete a maintenance configuration using the

command.`az aks maintenanceconfiguration delete`

`az aks maintenanceconfiguration delete \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule`


For complete details, examples, and advanced scenarios, see [Use Planned Maintenance to schedule maintenance windows for your AKS cluster](planned-maintenance).

## Karpenter Node Disruption Budgets and Pod Disruption Budgets for NAP

For more information on configuring Karpenter Node Disruption Budgets and Pod Disruption Budgets for NAP, see the following resources from the official Karpenter documentation:

## Next steps

For more information on node auto-provisioning in AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/generation-2-vm -->

# Use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS), including how to check available Gen 2 VM sizes, create AKS node pools with Gen 2 VMs, migrate from Gen 1 to Gen 2 VMs on AKS, and verify the VM generation of your AKS nodes.

## Before you begin

- Review the
[Virtual machine (VM) sizes, generations, and features for Azure Kubernetes Service (AKS)](aks-virtual-machine-sizes)article to understand VM generations and features supported on AKS.

## Check available Gen 2 VM sizes

Check available Gen 2 VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm#az-vm-list-skus) command.

```
# Set environment variables
export LOCATION=<your-region>
export VM_SIZE=<vm-size-to-check>
# Check if the VM size is available in the specified location
az vm list-skus --location $LOCATION --size $VM_SIZE --output table
```


For a breakdown of what VM sizes support Gen 2, see [Support for Gen 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2).

## Create a node pool with a Gen 2 VM

By default, Linux uses the Gen 2 node image unless the VM size doesn't support Gen 2.

Create a Linux node pool with a Gen 2 VM using the default [node pool creation](create-node-pools) process.

## Migrate an existing node pool to Gen 2

If you're using a VM size that only supports Gen 1, you can update your node pool to a VM size that supports Gen 2 using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. This update changes your node image from Gen 1 to Gen 2.

```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
export VM_SIZE=<supported-generation-2-vm-size>
# Update a Linux node pool to use a Gen 2 VM
az aks nodepool update --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --node-vm-size $VM_SIZE --os-type Linux
```


## Check if you're using a Gen 2 node image

Verify a successful node pool creation using the [ az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command and check that the

`nodeImageVersion`

contains `gen2`

in the output.```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
# Show node pool details
az aks nodepool show --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --output table
```


## Next steps

- To learn more about Gen 2 VMs, see
[Support for Generation 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2) - To learn more about supported Gen 2 node images, see
[Node images](node-images)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/generation-2-vms -->

# Use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS), including how to check available Gen 2 VM sizes, create AKS node pools with Gen 2 VMs, migrate from Gen 1 to Gen 2 VMs on AKS, and verify the VM generation of your AKS nodes.

## Before you begin

- Review the
[Virtual machine (VM) sizes, generations, and features for Azure Kubernetes Service (AKS)](aks-virtual-machine-sizes)article to understand VM generations and features supported on AKS.

## Check available Gen 2 VM sizes

Check available Gen 2 VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm#az-vm-list-skus) command.

```
# Set environment variables
export LOCATION=<your-region>
export VM_SIZE=<vm-size-to-check>
# Check if the VM size is available in the specified location
az vm list-skus --location $LOCATION --size $VM_SIZE --output table
```


For a breakdown of what VM sizes support Gen 2, see [Support for Gen 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2).

## Create a node pool with a Gen 2 VM

By default, Linux uses the Gen 2 node image unless the VM size doesn't support Gen 2.

Create a Linux node pool with a Gen 2 VM using the default [node pool creation](create-node-pools) process.

## Migrate an existing node pool to Gen 2

If you're using a VM size that only supports Gen 1, you can update your node pool to a VM size that supports Gen 2 using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. This update changes your node image from Gen 1 to Gen 2.

```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
export VM_SIZE=<supported-generation-2-vm-size>
# Update a Linux node pool to use a Gen 2 VM
az aks nodepool update --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --node-vm-size $VM_SIZE --os-type Linux
```


## Check if you're using a Gen 2 node image

Verify a successful node pool creation using the [ az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command and check that the

`nodeImageVersion`

contains `gen2`

in the output.```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
# Show node pool details
az aks nodepool show --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --output table
```


## Next steps

- To learn more about Gen 2 VMs, see
[Support for Generation 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2) - To learn more about supported Gen 2 node images, see
[Node images](node-images)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-vulnerability-management -->

# Vulnerability management for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Vulnerability management involves detecting, assessing, mitigating, and reporting on any security vulnerabilities that exist in an organization's systems and software. Vulnerability management is a shared responsibility between you and Microsoft.

This article describes how Microsoft manages security vulnerabilities and security updates (also referred to as patches), for Azure Kubernetes Service (AKS) clusters.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-best-practices -->

# Best practices for Windows containers on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In AKS, you can create node pools that run Linux or Windows Server as the operating system (OS) on the nodes. Windows Server nodes can run native Windows container applications, such as .NET Framework. The Linux OS and Windows OS have different container support and configuration considerations. For more information, see [Windows container considerations in Kubernetes](windows-vs-linux-containers). To learn more about how various industries are using Windows containers on AKS, see [Windows AKS customer stories](windows-aks-customer-stories).

This article outlines best practices for running Windows containers on AKS.

## Create an AKS cluster with Linux and Windows node pools

When you create a new AKS cluster, the Azure platform creates a Linux node pool by default. This node pool contains system services needed for the cluster to function. Azure also creates and manages a control plane abstracted from the user, which means you aren't exposed to the underlying OS of the nodes hosting the main control plane components. We recommend that you run at least *two nodes* on the default Linux node pool to ensure the reliability and performance of your cluster. You can't delete the default Linux node pool unless you delete the entire cluster.

There are some cases where you should consider deploying a Linux node pool when planning to run Windows-based workloads on your AKS cluster, such as:

- If you want to run Linux and Windows workloads, you can deploy a Linux node pool and a Windows node pool in the same cluster.
- If you want to deploy infrastructure-related components based on Linux, such as NGINX, you need a Linux node pool alongside your Windows node pool. You can use control plane nodes for development and testing scenarios. For production workloads, we recommend that you deploy separate Linux node pools to ensure reliability and performance.

## Modernize existing applications with Windows on AKS

You might want to containerize existing applications and run them using Windows on AKS. Before starting the containerization process, it's important to understand the application architecture and dependencies. For more information, see [Containerize existing applications using Windows containers](/en-us/virtualization/windowscontainers/quick-start/lift-shift-to-containers).

## Windows OS version


Best practice guidanceWindows Server 2022 provides improved security and performance and is the recommended OS for Windows node pools on AKS. AKS uses Windows Server 2022 as the host OS version and only supports process isolation.


AKS supports two options for the Windows Server operating system: Long Term Servicing Channel Releases (LTSC) and Windows Server Annual Channel for Containers.

AKS supports Long Term Servicing Channel Releases (LTSC), including Windows Server 2025 (preview), Windows Server 2022, and Windows Server 2019. This channel is released every three years and is supported for five years. Customers using Long Term Support (LTS) should use Windows Server 2022.

AKS uses Windows Server 2019 and Windows Server 2022 as the host OS versions and only supports process isolation. AKS doesn't support container images built by other versions of Windows Server. For more information, see

[Windows container version compatibility](/en-us/virtualization/windowscontainers/deploy-containers/version-compatibility). Windows Server 2022 is the default OS for Kubernetes version 1.25 and later.Important

Starting on March 01, 2026, Azure Kubernetes Service (AKS) no longer supports Windows Server 2019 node pools. Node pools running Kubernetes version 1.33+ can't use Windows Server 2019. Starting on April 01, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail. For more information on this retirement, see the

[Retirement GitHub issue](https://github.com/Azure/AKS/issues/4091)and the[Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=aks-will-stop-support-for-windows-server-2019-on-march-1-2026). To stay informed on announcements and updates, follow the[AKS release notes](https://github.com/Azure/AKS/releases).Important

Starting on March 15, 2027, Azure Kubernetes Service (AKS) no longer supports Windows Server 2022 node pools. Node pools running Kubernetes version 1.36+ can't use Windows Server 2022. Starting on April 01, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail. For more information on this retirement, see the

[Retirement GitHub issue](https://github.com/Azure/AKS/issues/4168)and the[Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=ws2022-retirement-aks). To stay informed on announcements and updates, follow the[AKS release notes](https://github.com/Azure/AKS/releases).AKS supports

[Windows Server Annual Channel for Containers](https://techcommunity.microsoft.com/t5/windows-server-news-and-best/windows-server-annual-channel-for-containers/ba-p/3866248)(preview). This channel is released annually and is supported for two years. This channel is beneficial for customers requiring increased innovation cycles and portability. The portability functionality enables the Windows Server 2022-based container image OS to run on newer versions of Windows Server host OS, such as the new annual channel release.Windows Annual Channel versions are based on the Kubernetes version of your node pool. To upgrade from one Annual Channel version to the next,

[upgrade to a Kubernetes version](upgrade-aks-cluster)that supports the next Annual Channel version. For more information, see[Windows Server Annual Channel for Containers on AKS](windows-annual-channel).

## Monitoring


Best practice guidanceWindows Exporter is installed on all Windows nodes in certain regions. To view regional rollout, see

[AKS Github]. With Managed Prometheus and Grafana, you can monitor default collectors included in Windows Exporter on AKS. For more information, see[default Prometheus metrics configured in Azure Monitor].

Windows Exporter allows customers to see their metrics through Managed Prometheus or Prometheus OSS deployments and enjoy enhanced observability around their node and pod performance, health, and resource usage. These metrics are also visible with Managed Grafana.

- When enabling managed prometheus, add this required parameter for correct dashboard data presentation for Windows:
`--enable-windows-recording-rules`

. - Grafana includes dashboards for showing Windows resources, such as:
- Kubernetes / Compute Resources / Cluster (Windows)
- Kubernetes / Compute Resources / Namespace (Windows)
- Kubernetes / Compute Resources / Pod (Windows)
- Kubernetes / USE Method / Cluster (Windows)
- Kubernetes / USE Method / Node (Windows)


The default collectors included in Windows Exporter on AKS are: cpu, cpu_info, cs, container, logical_disk, memory, net, os, process, service, system, textfile. The metrics are exposed on port **19182** on the windows node. For more information on what metrics you can see using these collectors, please see [prometheus-community/windows_exporter](https://github.com/prometheus-community/windows_exporter#collectors).

## Networking

### Networking modes


Best practice guidanceAKS clusters with Windows node pools only support Azure Container Networking Interface (Azure CNI) and use it by default.


Windows doesn't support kubenet networking. AKS clusters with Windows node pools must use Azure CNI. For more information, see [Network concepts for applications in AKS](concepts-network).

Azure CNI offers two networking modes based on your workload requirements:

is an overlay network similar to kubenet. The overlay network allows you to use virtual network (VNet) IPs for nodes and private address spaces for pods within those nodes that you can reuse across the cluster. Azure CNI Overlay is the**Azure CNI Overlay****recommended networking mode**. It provides simplified network configuration and management and the best scalability in AKS networking.requires extra planning and consideration for IP address management. This mode provides VNet IPs for nodes**Azure CNI with Dynamic IP Allocation***and*pods. This configuration allows you direct access to pod IPs. However, it comes with increased complexity and reduced scalability.

To help you decide which networking mode to use, see [Choosing a network model](concepts-network-azure-cni-overlay#choose-a-network-model).

### Network policies


Best practice guidanceUse network policies to secure traffic between pods. Windows supports Azure Network Policy Manager and Calico Network Policy. For more information, see

[Differences between Network Policy engines: Cilium, Azure NPM, and Calico].

When managing traffic between pods, you should apply the principle of least privilege. The Network Policy feature in Kubernetes allows you to define and enforce ingress and egress traffic rules between the pods in your cluster. For more information, see [Secure traffic between pods using network policies in AKS](use-network-policies).

Windows pods on AKS clusters that use the Calico Network Policy enable Floating IP by default.

## Upgrades and updates

It's important to keep your Windows environment up-to-date to ensure your systems have the latest security updates, feature sets, and compliance requirements. In a Kubernetes environment like AKS, you need to maintain the Kubernetes version, Windows nodes, and Windows container images and pods.

### Kubernetes version upgrades

As a managed Kubernetes service, AKS provides the necessary tools to upgrade your cluster to the latest Kubernetes version. For more information, see [Upgrade an AKS cluster](upgrade-cluster).

### Windows node monthly updates

Windows nodes on AKS follow a monthly update schedule. Every month, AKS creates a new VHD with the latest available updates for Windows node pools. The VHD includes the host image, latest Nano Server image, latest Server Core image, and container. We recommend performing monthly updates to your Windows node pools to ensure your nodes have the latest security patches. For more information, see [Upgrade AKS node images](node-image-upgrade).

Note

Upgrades on Windows systems include both OS version upgrades and monthly node OS updates.

You can stay up to date with the availability of new monthly releases using the [AKS release tracker](https://releases.aks.azure.com/) and [AKS release notes](https://github.com/Azure/AKS/releases).

### Windows node OS version upgrades

Windows has a release cadence for new versions of the OS, including Windows Server 2025 (preview), Windows Server 2022, and Windows Server 2019. When upgrading your Windows node OS version, ensure the Windows container image version matches the Windows container host version and the node pools have only one version of Windows Server.

To upgrade the Windows node OS version, you need to complete the following steps:

- Create a new node pool with the new Windows Server version.
- Deploy your workloads with the new Windows container images to the new node pool.
- Decommission the old node pool.

For more information, see [Upgrade Windows Server workloads on AKS](upgrade-windows-2019-2022).

Note

Windows announced a new [Windows Server Annual Channel for Containers](https://techcommunity.microsoft.com/t5/windows-server-news-and-best/windows-server-annual-channel-for-containers/ba-p/3866248) that supports portability and mixed versions of Windows nodes and containers. This feature isn't yet supported in AKS.

To track AKS feature plans, see the [Public AKS roadmap](https://github.com/Azure/AKS/projects/1#card-90806240).

## Next steps

To learn more about Windows containers on AKS, see the following resources:

[Learn how to deploy, manage, and monitor Windows containers on AKS](/en-us/training/paths/deploy-manage-monitor-wincontainers-aks).- Open an issue or provide feedback in the
[Windows containers GitHub repository](https://github.com/microsoft/Windows-Containers/issues). - Review the
[third-party partner solutions for Windows on AKS](windows-aks-partner-solutions).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-repair -->

# Azure Kubernetes Service (AKS) node auto-repair

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) continuously monitors the health state of worker nodes and performs automatic node repair if they become unhealthy. The Azure virtual machine (VM) platform [performs maintenance on VMs](/en-us/azure/virtual-machines/maintenance-and-updates) experiencing issues. AKS and Azure VMs work together to minimize service disruptions for clusters.

In this article, you learn how the automatic node repair functionality behaves for Windows and Linux nodes.

## How AKS checks for NotReady nodes

AKS uses the following rules to determine if a node is unhealthy and needs repair:

- The node reports the
status on consecutive checks within a 10-minute time frame.**NotReady** - The node doesn't report any status within 10 minutes.

You can manually check the health state of your nodes with the `kubectl get nodes`

command.

## How automatic repair works

Note

AKS initiates repair operations with the user account **aks-remediator**.

If AKS identifies an unhealthy node that remains unhealthy for at least *five* minutes, AKS performs the following actions:

- AKS reboots the node.
- If the node remains unhealthy after reboot, AKS reimages the node.
- If the node remains unhealthy after reimage and it's a Linux node, AKS redeploys the node.

AKS retries the restart, reimage, and redeploy sequence up to three times if the node remains unhealthy. The overall auto repair process can take up to an hour to complete.

## Limitations

AKS node auto-repair is a best effort service and we don't guarantee that the node is restored back to healthy status. If your node persists in an unhealthy state, we highly encourage that you perform manual investigation of the node. Learn more about [troubleshooting node NotReady status](/en-us/troubleshoot/azure/azure-kubernetes/availability-performance/node-not-ready-basic-troubleshooting).

There are cases where AKS doesn't perform automatic repair. Failure to automatically repair the node can occur either by design or if Azure can't detect that an issue exists. Examples of when auto-repair isn't performed include:

- A node status isn't being reported due to error in network configuration.
- A node failed to initially register as a healthy node.
- If either of the following taints are present on the node:
`node.cloudprovider.kubernetes.io/shutdown`

,`ToBeDeletedByClusterAutoscaler`

. - A node is in the process of being upgraded, resulting in the following annotation on the node
`"cluster-autoscaler.kubernetes.io/scale-down-disabled": "true"`

and`"kubernetes.azure.com/azure-cluster-autoscaler-scale-down-disabled-reason": "upgrade"`


## Monitor node auto-repair using Kubernetes events

When AKS performs node auto-repair on your cluster, AKS emits Kubernetes events from the aks-auto-repair source for visibility. The following events appear on a node object when auto-repair happens.

To learn more about accessing, storing, and configuring alerts on Kubernetes events, see [Use Kubernetes events for troubleshooting in Azure Kubernetes Service](events).

| Reason | Event Message | Description |
|---|---|---|
| NodeRebootStart | Node auto-repair is initiating a reboot action due to NotReady status persisting for more than 5 minutes. | This event is emitted to notify you when reboot is about to be performed on your node. This action is the first in the overall node auto-repair sequence. |
| NodeRebootEnd | Reboot action from node auto-repair is completed. | Emitted once reboot is complete on the node. This event doesn't indicate the health status (healthy or unhealthy) of the node after the reboot is performed. |
| NodeReimageStart | Node auto-repair is initiating a reimage action due to NotReady status persisting for more than 5 minutes. | This event is emitted to notify you when reimage is about to be performed on your node. |
| NodeReimageEnd | Reimage action from node auto-repair is completed. | Emitted once reimage is complete on the node. This event doesn't indicate the health status (healthy or unhealthy) of the node after the reimage is performed. |
| NodeRedeployStart | Node auto-repair is initiating a redeploy action due to NotReady status persisting more than 5 minutes. | This event is emitted to notify you when redeploy is about to be performed on your node. Redeploy is the last action in the node auto-repair sequence. |
| NodeRedeployEnd | Redeploy action from node auto-repair is completed. | Emitted once redeploy is complete on the node. This event doesn't indicate the health status (healthy or unhealthy) of the node after redeploy is performed. |

If any errors occur during the node auto-repair process, the following events are emitted with the verbatim error message. Learn more about [troubleshooting common node auto-repair errors](/en-us/troubleshoot/azure/azure-kubernetes/availability-performance/node-auto-repair-errors).

Note

*Error code* in the following event messages varies depending on the error reported.

| Reason | Event Message | Description |
|---|---|---|
| NodeRebootError | Node auto-repair reboot action failed due to an operation failure. See error details here: Error code |
Emitted when there's an error with the reboot action. |
| NodeReimageError | Node auto-repair reimage action failed due to an operation failure. See error details here: Error code |
Emitted when there's an error with the reimage action. |
| NodeRedeployError | Node auto-repair redeploy action failed due to an operation failure. See error details here: Error code |
Emitted when there's an error with the redeploy action. |

## Next steps

By default, you can access Kubernetes events and logs on your AKS cluster from the past 1 hour. To store and query events and logs from the past 90 days, enable [Container Insights](/en-us/azure/azure-monitor/containers/container-insights-overview#access-container-insights) for deeper troubleshooting on your AKS cluster.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-image-upgrade -->

# Upgrade Azure Kubernetes Service (AKS) node images

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) regularly provides new node images, so it's beneficial to upgrade your node images frequently to use the latest AKS features. Linux node images are updated weekly, and Windows node images are updated monthly. Image upgrade announcements are included in the [AKS release notes](https://github.com/Azure/AKS/releases), and it can take up to a week for these updates to be rolled out across all regions. You can also perform node image upgrades automatically and schedule them using planned maintenance. For more information, see [Automatically upgrade node images](auto-upgrade-node-image).

This article shows you how to upgrade AKS cluster node images and how to update node pool images without upgrading the Kubernetes version. For information on upgrading the Kubernetes version for your cluster, see [Upgrade an AKS cluster](upgrade-aks-cluster).

Note

The AKS cluster must use virtual machine scale sets for the nodes.

It's not possible to downgrade a node image version (for example *AKSUbuntu-2204 to AKSUbuntu-1804*, or *AKSUbuntu-2204-202308.01.0 to AKSUbuntu-2204-202307.27.0*).

## Connect to your AKS cluster

Connect to your AKS cluster using the [

`az aks get-credentials`

][az-aks-get-credentials] command.`az aks get-credentials \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER`


## Check for available node image upgrades

Check for available node image upgrades using the

command.`az aks nodepool get-upgrades`

`az aks nodepool get-upgrades \ --nodepool-name $AKS_NODEPOOL \ --cluster-name $AKS_CLUSTER \ --resource-group $AKS_RESOURCE_GROUP`

In the output, find and make note of the

`latestNodeImageVersion`

value. This value is the latest node image version available for your node pool.Check your current node image version to compare with the latest version using the

command.`az aks nodepool show`

`az aks nodepool show \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL \ --query nodeImageVersion`

If the

`nodeImageVersion`

value is different from the`latestNodeImageVersion`

, you can upgrade your node image.

## Upgrade all node images in all node pools

Upgrade all node images in all node pools in your cluster using the

command with the`az aks upgrade`

`--node-image-only`

flag.`az aks upgrade \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER \ --node-image-only \ --yes`

You can check the status of the node images using the

`kubectl get nodes`

command.Note

This command might differ slightly depending on the shell you use. For more information on Windows and PowerShell environments, see the

[Kubernetes JSONPath documentation](https://kubernetes.io/docs/reference/kubectl/jsonpath/).`kubectl get nodes -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.metadata.labels.kubernetes\.azure\.com\/node-image-version}{"\n"}{end}'`

When the upgrade completes, use the

command to get the updated node pool details. The current node image is shown in the`az aks show`

`nodeImageVersion`

property.`az aks show \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER`


## Upgrade a specific node pool

Update the OS image of a node pool without doing a Kubernetes cluster upgrade using the

command with the`az aks nodepool upgrade`

`--node-image-only`

flag.`az aks nodepool upgrade \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL \ --node-image-only`

You can check the status of the node images with the

`kubectl get nodes`

command.Note

This command may differ slightly depending on the shell you use. For more information on Windows and PowerShell environments, see the

[Kubernetes JSONPath documentation](https://kubernetes.io/docs/reference/kubectl/jsonpath/).`kubectl get nodes -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.metadata.labels.kubernetes\.azure\.com\/node-image-version}{"\n"}{end}'`

When the upgrade completes, use the

command to get the updated node pool details. The current node image is shown in the`az aks nodepool show`

`nodeImageVersion`

property.`az aks nodepool show \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL`


## Upgrade node images with node surge

To speed up the node image upgrade process, you can upgrade your node images using a customizable node surge value. By default, AKS uses one extra node to configure upgrades.

Upgrade node images with node surge using the

command with the`az aks nodepool update`

`--max-surge`

flag to configure the number of nodes used for upgrades.Note

To learn more about the trade-offs of various

`--max-surge`

settings, see[Customize node surge upgrade](upgrade-aks-cluster#customize-node-surge-upgrade).`az aks nodepool update \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL \ --max-surge 33% \ --no-wait`

You can check the status of the node images with the

`kubectl get nodes`

command.`kubectl get nodes -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.metadata.labels.kubernetes\.azure\.com\/node-image-version}{"\n"}{end}'`

Get the updated node pool details using the

command. The current node image is shown in the`az aks nodepool show`

`nodeImageVersion`

property.`az aks nodepool show \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL`


## Next steps

- For information about the latest node images, see the
[AKS release notes](https://github.com/Azure/AKS/releases). - Learn how to upgrade the Kubernetes version with
[Upgrade an AKS cluster](upgrade-aks-cluster). [Automatically apply cluster and node pool upgrades with GitHub Actions](node-upgrade-github-actions).- Learn more about multiple node pools with
[Create multiple node pools](create-node-pools). - Learn about upgrading best practices with
[AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-production-upgrade-strategies -->

# AKS production upgrade strategies

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Upgrade your production Azure Kubernetes Service (AKS) clusters safely by using these proven patterns. Each strategy is optimized for specific business constraints and risk tolerance.

## What this article covers

This article provides tested upgrade patterns for production AKS clusters and focuses on:

- Blue-green deployments for zero-downtime upgrades.
- Staged fleet upgrades across multiple environments.
- Safe Kubernetes version adoption with validation gates.
- Emergency security patching for rapid common vulnerabilities and exposures (CVE) response.
- Application resilience patterns for seamless upgrades.

These patterns are best for production environments, site reliability engineers, and platform teams that require minimal downtime and maximum safety.

For more information, see these related articles:

- To get upgrade patterns for AKS clusters with stateful workloads, see
[Stateful workload upgrade patterns](stateful-workload-upgrades). - To check for and apply basic upgrades to your AKS cluster, see
[Upgrade an Azure Kubernetes Service cluster](upgrade-aks-cluster). - To use the scenario hub to help you choose the right AKS upgrade approach, see
[AKS upgrade scenarios: Choose your path](upgrade-scenarios-hub).

For a quick start, select a link for instructions:

## Choose your strategy

| Your priority | Best pattern | Downtime | Time to complete |
|---|---|---|---|
| Zero downtime |
|

[Staged fleet upgrades](#scenario-2-stage-upgrades-across-environments)[Canary with validation](#scenario-3-safe-kubernetes-version-intake)[Automated patching](#scenario-4-fastest-security-patch-deployment)[Resilient architecture](#scenario-5-application-architecture-for-seamless-upgrades)#### Role-based quick start

| Role | Start here |
|---|---|
| Site reliability engineer/Platform |
|

[Stateful workload patterns](stateful-workload-upgrades)[Scenario 5](#scenario-5-application-architecture-for-seamless-upgrades)[Scenario 4](#scenario-4-fastest-security-patch-deployment)## Scenario 1: Minimal downtime production upgrades

**Challenge:** "I need to upgrade my production cluster with less than 2 minutes of downtime during business hours."

**Strategy:** Use blue-green deployment with intelligent traffic shifting.

To learn more, see [Blue-green deployment patterns](/en-us/azure/architecture/guide/aks/blue-green-deployment-for-aks) and [Azure Traffic Manager configuration](/en-us/azure/traffic-manager/traffic-manager-configure-weighted-routing-method).

### Quick implementation (15 minutes)

```
# 1. Create green cluster (parallel to blue)
az aks create --name myaks-green --resource-group myRG \
--kubernetes-version 1.29.0 --enable-cluster-autoscaler \
--min-count 3 --max-count 10
# 2. Deploy application to green cluster
kubectl config use-context myaks-green
kubectl apply -f ./production-manifests/
# 3. Validate green cluster
# Run your application-specific health checks here
# Examples: API endpoint tests, database connectivity, dependency checks
# 4. Switch traffic (<30-second downtime)
az network traffic-manager endpoint update \
--profile-name prod-tm --name green-endpoint --weight 100
az network traffic-manager endpoint update \
--profile-name prod-tm --name blue-endpoint --weight 0
```


** Detailed step-by-step guide**

#### Prerequisites

- Secondary cluster capacity planned.
- Application supports horizontal scaling.
- Database connections use connection pooling.
- Health checks configured (
`/health`

,`/ready`

). - Rollback procedure tested in staging.

#### Step 1: Prepare the blue-green infrastructure

```
# Create resource group for green cluster
az group create --name myRG-green --location eastus2
# Create green cluster with same configuration as blue
az aks create \
--resource-group myRG-green \
--name myaks-green \
--kubernetes-version 1.29.0 \
--node-count 3 \
--enable-cluster-autoscaler \
--min-count 3 \
--max-count 10 \
--enable-addons monitoring \
--generate-ssh-keys
```


#### Step 2: Deploy and validate the green environment

```
# Get green cluster credentials
az aks get-credentials --resource-group myRG-green --name myaks-green
# Deploy application stack
# Apply your Kubernetes manifests in order:
kubectl apply -f ./your-manifests/namespace.yaml # Create namespace
kubectl apply -f ./your-manifests/secrets/ # Deploy secrets
kubectl apply -f ./your-manifests/configmaps/ # Deploy config maps
kubectl apply -f ./your-manifests/deployments/ # Deploy applications
kubectl apply -f ./your-manifests/services/ # Deploy services
# Wait for all pods to be ready
kubectl wait --for=condition=ready pod --all --timeout=300s
# Validate application health
kubectl get pods -A
kubectl logs -l app=my-app --tail=50
```


#### Step 3: Traffic switching (critical 30-second window)

```
# Pre-switch validation
curl -f https://myapp-green.eastus2.cloudapp.azure.com/health
if [ $? -ne 0 ]; then echo "Green health check failed!"; exit 1; fi
# Execute traffic switch
az network dns record-set cname set-record \
--resource-group myRG-dns \
--zone-name mycompany.com \
--record-set-name api \
--cname myapp-green.eastus2.cloudapp.azure.com
# Immediate validation
sleep 30
curl -f https://api.mycompany.com/health
```


#### Step 4: Monitor and validate

```
# Monitor traffic and errors for 15 minutes
kubectl top nodes
kubectl top pods
kubectl logs -l app=my-app --since=15m | grep ERROR
# Check application metrics
curl https://api.mycompany.com/metrics | grep http_requests_total
```


### Common pitfalls and FAQs

**Expand for quick troubleshooting and tips**

**Domain Name System (DNS) propagation is slow:**Use low time-to-live values before upgrade, and validate the DNS cache flush.**Pods stuck terminating:**Check for finalizers, long shutdown hooks, or pod disruption budgets (PDBs) with`maxUnavailable: 0`

.**Traffic not shifting:**Validate Azure Load Balancer/Azure Traffic Manager configuration and health probes.**Rollback fails:**Always keep the blue cluster ready until the green cluster is fully validated.**Q: Can I use open-source software tools for validation?****A:**Yes. Use[kube-no-trouble](https://github.com/doitintl/kube-no-trouble)for API checks and[Trivy](https://aquasecurity.github.io/trivy/)for image scanning.

**Q: What's unique to AKS?****A:**Native integration with Traffic Manager, Azure Kubernetes Fleet Manager, and node image patching for zero-downtime upgrades.


### Advanced configuration

For applications that require <30-second downtime:

```
# Use session affinity during transition
apiVersion: v1
kind: Service
metadata:
name: my-app
spec:
sessionAffinity: ClientIP
sessionAffinityConfig:
clientIP:
timeoutSeconds: 300
```


### Success validation

To validate your progress, use the following checklist:

- Application responds within two seconds.
- No 5xx errors are in logs.
- Database connections are stable.
- User sessions are preserved.

### Emergency rollback (if needed)

```
# Immediate rollback to blue cluster
az network dns record-set cname set-record \
--resource-group myRG-dns \
--zone-name mycompany.com \
--record-set-name api \
--cname myapp-blue.eastus2.cloudapp.azure.com
```


**Expected outcome:** Less than 2-minute total downtime, zero data loss, and full rollback capability.

```
az aks create \
--resource-group production-rg \
--name aks-green-cluster \
--kubernetes-version 1.29.0 \
--node-count 3 \
--tier premium \
--auto-upgrade-channel patch \
--planned-maintenance-config ./maintenance-window.json
```


## Verify cluster readiness

```
az aks get-credentials --resource-group production-rg --name aks-green-cluster
kubectl get nodes
```


### Implementation steps

#### Step 1: Deploy the application to a green cluster

```
# Deploy application stack
kubectl apply -f ./k8s-manifests/
kubectl apply -f ./monitoring/
# Wait for all pods to be ready
kubectl wait --for=condition=ready pod --all --timeout=300s
# Validate application health
curl -f http://green-cluster-ingress/health
```


#### Step 2: Run traffic shift

```
# Update DNS or load balancer to point to green cluster
az network dns record-set a update \
--resource-group dns-rg \
--zone-name contoso.com \
--name api \
--set aRecords[0].ipv4Address="<green-cluster-ip>"
# Monitor traffic shift (should complete in 60-120 seconds)
watch kubectl top pods -n production
```


#### Step 3: Validate and clean up

```
# Verify zero errors in application logs
kubectl logs -l app=api --tail=100 | grep -i error
# Monitor key metrics for 15 minutes
kubectl get events --sort-by='.lastTimestamp' | head -20
# After validation, decommission blue cluster
az aks delete --resource-group production-rg --name aks-blue-cluster --yes
```


### Success metrics

**Downtime:**<2 minutes (DNS propagation time)**Error rate:**0% during transition**Recovery time:**<5 minutes if rollback needed

## Scenario 2: Stage upgrades across environments

**Challenge:** "I need to safely test upgrades through dev/test/production with proper validation gates."

**Strategy:** Use Azure Kubernetes Fleet Manager with staged rollouts.

To learn more, see the [Azure Kubernetes Fleet Manager overview](/en-us/azure/kubernetes-fleet/overview) and [Update orchestration](/en-us/azure/kubernetes-fleet/update-orchestration).

### Prerequisites

```
# Install Fleet extension
az extension add --name fleet
az extension update --name fleet
# Create Fleet resource
az fleet create \
--resource-group fleet-rg \
--name production-fleet \
--location eastus
```


### Implementation steps

#### Step 1: Define stage configuration

Create `upgrade-stages.json`

:

```
{
"stages": [
{
"name": "development",
"groups": [{ "name": "dev-clusters" }],
"afterStageWaitInSeconds": 1800
},
{
"name": "testing",
"groups": [{ "name": "test-clusters" }],
"afterStageWaitInSeconds": 3600
},
{
"name": "production",
"groups": [{ "name": "prod-clusters" }],
"afterStageWaitInSeconds": 0
}
]
}
```


#### Step 2: Add clusters to a fleet

```
# Add development clusters
az fleet member create \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name dev-east \
--member-cluster-id "/subscriptions/.../clusters/aks-dev-east" \
--group dev-clusters
# Add test clusters
az fleet member create \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name test-east \
--member-cluster-id "/subscriptions/.../clusters/aks-test-east" \
--group test-clusters
# Add production clusters
az fleet member create \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name prod-east \
--member-cluster-id "/subscriptions/.../clusters/aks-prod-east" \
--group prod-clusters
```


#### Step 3: Create and run a staged update

```
# Create staged update run
az fleet updaterun create \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name k8s-1-29-upgrade \
--upgrade-type Full \
--kubernetes-version 1.29.0 \
--node-image-selection Latest \
--stages upgrade-stages.json
# Start the staged rollout
az fleet updaterun start \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name k8s-1-29-upgrade
```


#### Step 4: Validation gates between stages

After dev stage (30-minute soak):

```
# Run automated test suite
./scripts/run-e2e-tests.sh dev-cluster
./scripts/performance-baseline.sh dev-cluster
# Check for any regressions
kubectl get events --sort-by='.lastTimestamp' | grep -i warn
```


After test stage (60-minute soak):

```
# Extended testing with production-like load
./scripts/load-test.sh test-cluster 1000-users 15-minutes
./scripts/chaos-engineering.sh test-cluster
# Manual approval gate
echo "Approve production deployment? (y/n)"
read approval
```


### Common pitfalls and FAQs

**Expand for quick troubleshooting and tips**

**Stage fails because of quota:**Precheck regional quotas for all clusters in the fleet.**Validation scripts fail:**Ensure that test scripts are idempotent and have clear pass/fail output.**Manual approval delays:**Use automation for nonproduction. Require manual only for production.**Q: Can I use open-source software tools for validation?****A:**Yes. Integrate[Sonobuoy](https://sonobuoy.io/)for conformance and[kube-bench](https://github.com/aquasecurity/kube-bench)for security.

**Q: What's unique to AKS?****A:**Azure Kubernetes Fleet Manager enables true staged rollouts and validation gates natively.


## Scenario 3: Safe Kubernetes version intake

**Challenge:** "I need to adopt Kubernetes 1.30 without breaking existing workloads or APIs."

**Strategy:** Use multiphase validation with canary deployment.

To learn more, see [Canary deployments](/en-us/azure/architecture/reference-architectures/containers/aks-microservices/aks-microservices-advanced#deployment-strategies) and [API deprecation policies](https://kubernetes.io/docs/reference/using-api/deprecation-policy/).

### Implementation steps

#### Step 1: API deprecation analysis

```
# Install and run API deprecation scanner
kubectl apply -f https://github.com/doitintl/kube-no-trouble/releases/latest/download/knt-full.yaml
# Scan for deprecated APIs
kubectl run knt --image=doitintl/knt:latest --rm -it --restart=Never -- \
-c /kubeconfig -o json > api-deprecation-report.json
# Review and remediate findings
cat api-deprecation-report.json | jq '.[] | select(.deprecated==true)'
```


To learn more, see the [Kubernetes API deprecation guide](https://kubernetes.io/docs/reference/using-api/deprecation-guide/) and [kube-no-trouble documentation](https://github.com/doitintl/kube-no-trouble).

#### Step 2: Create a canary environment

```
# Create canary cluster with target version
az aks create \
--resource-group canary-rg \
--name aks-canary-k8s130 \
--kubernetes-version 1.30.0 \
--node-count 2 \
--tier premium \
--enable-addons monitoring
# Deploy subset of workloads
kubectl apply -f ./canary-manifests/
```


#### Step 3: Progressive workload migration

```
# Phase 1: Stateless services (20% traffic)
kubectl patch service api-service -p '{"spec":{"selector":{"version":"canary"}}}'
./scripts/monitor-error-rate.sh 15-minutes
# Phase 2: Background jobs (50% traffic)
kubectl scale deployment batch-processor --replicas=3
./scripts/validate-job-completion.sh
# Phase 3: Critical services (100% traffic)
kubectl patch deployment critical-api -p '{"spec":{"template":{"metadata":{"labels":{"cluster":"canary"}}}}}'
```


#### Step 4: Feature gate validation

```
# Test new Kubernetes 1.30 features
apiVersion: v1
kind: ConfigMap
metadata:
name: feature-validation
data:
test-script: |
# Test new security features
kubectl auth can-i create pods --as=service-account:default:test-sa
# Validate performance improvements
kubectl top nodes --use-protocol-buffers=true
# Check new API versions
kubectl api-versions | grep "v1.30"
```


### Success metrics

**API compatibility:**100% (zero breaking changes)**Performance:**≤5% regression in key metrics**Feature adoption:**New features validated in canary

## Scenario 4: Fastest security patch deployment

**Challenge:** "A critical CVE was announced. I need patches deployed across all clusters within 4 hours."

**Strategy:** Use automated node image patching with minimal disruption.

To learn more, see [Node image upgrade strategies](node-image-upgrade), [Auto-upgrade channels](auto-upgrade-cluster), and [Security patching best practices](/en-us/azure/aks/operator-best-practices-cluster-security).

### Implementation steps

#### Step 1: Emergency response preparation

```
# Set up automated monitoring for security updates
az aks nodepool update \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--auto-upgrade-channel SecurityPatch
# Configure maintenance window for emergency patches
az aks maintenance-configuration create \
--resource-group production-rg \
--cluster-name aks-prod \
--config-name emergency-security \
--week-index First,Second,Third,Fourth \
--day-of-week Monday,Tuesday,Wednesday,Thursday,Friday \
--start-hour 0 \
--duration 4
```


To learn more, see [Planned maintenance configuration](planned-maintenance) and [Autoupgrade channels](auto-upgrade-cluster#cluster-autoupgrade-channels).

#### Step 2: Automated security scanning

```
# security-scan-cronjob.yaml
apiVersion: batch/v1
kind: CronJob
metadata:
name: security-scanner
spec:
schedule: "0 */6 * * *" # Every 6 hours
jobTemplate:
spec:
template:
spec:
containers:
- name: scanner
image: aquasec/trivy:latest
command:
- trivy
- k8s
- --report
- summary
- cluster
```


#### Step 3: Rapid patch deployment

```
# Trigger immediate node image upgrade for security patches
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--node-image-only \
--max-surge 50% \
--drain-timeout 5
# Monitor patch deployment
watch az aks nodepool show \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--query "upgradeSettings"
```


#### Step 4: Compliance validation

```
# Verify patch installation
kubectl get nodes -o wide
kubectl describe node | grep "Kernel Version"
# Generate compliance report
./scripts/generate-security-report.sh > security-compliance-$(date +%Y%m%d).json
# Notify security team
curl -X POST "$SLACK_WEBHOOK" -d "{\"text\":\"Security patches deployed to production cluster. Compliance report attached.\"}"
```


### Success metrics

**Deployment time:**<4 hours from common vulnerabilities and exposures announcement**Coverage:**100% of nodes patched**Downtime:**<5 minutes per node pool

## Scenario 5: Application architecture for seamless upgrades

**Challenge:** "I want my applications to handle cluster upgrades gracefully without affecting users."

**Strategy:** Use resilient application patterns with graceful degradation.

To learn more, see [Application reliability patterns](/en-us/azure/architecture/framework/resiliency/reliability-patterns), [Pod disruption budgets](https://kubernetes.io/docs/tasks/run-application/configure-pdb/), and [Health check best practices](/en-us/azure/architecture/patterns/health-endpoint-monitoring).

### Implementation steps

#### Step 1: Implement robust health checks

```
# robust-health-checks.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
name: resilient-api
spec:
replicas: 3
template:
spec:
containers:
- name: api
image: myapp:latest
readinessProbe:
httpGet:
path: /health/ready
port: 8080
initialDelaySeconds: 10
periodSeconds: 5
timeoutSeconds: 3
successThreshold: 1
failureThreshold: 3
livenessProbe:
httpGet:
path: /health/live
port: 8080
initialDelaySeconds: 30
periodSeconds: 10
timeoutSeconds: 5
failureThreshold: 3
lifecycle:
preStop:
exec:
command: ["/bin/sh", "-c", "sleep 15"]
```


#### Step 2: Configure pod disruption budgets

```
# optimal-pdb.yaml
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: api-pdb
spec:
selector:
matchLabels:
app: api
maxUnavailable: 1
# Ensures at least 2 pods remain available during upgrades
---
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: database-pdb
spec:
selector:
matchLabels:
app: database
minAvailable: 2
# Critical: Always keep majority of database pods running
```


#### Step 3: Implement a circuit breaker pattern

```
// circuit-breaker.js
const CircuitBreaker = require('opossum');
const options = {
timeout: 3000,
errorThresholdPercentage: 50,
resetTimeout: 30000,
fallback: () => 'Service temporarily unavailable'
};
const breaker = new CircuitBreaker(callExternalService, options);
// Monitor circuit breaker state during upgrades
breaker.on('open', () => console.log('Circuit breaker opened'));
breaker.on('halfOpen', () => console.log('Circuit breaker half-open'));
```


To learn more, see [Circuit breaker pattern](/en-us/azure/architecture/patterns/circuit-breaker), [Retry pattern](/en-us/azure/architecture/patterns/retry), and [Application resilience](/en-us/azure/well-architected/reliability/).

#### Step 4: Database connection resilience

```
# connection-pool-config.yaml
apiVersion: v1
kind: ConfigMap
metadata:
name: db-config
data:
database.yml: |
production:
adapter: postgresql
pool: 25
timeout: 5000
retry_attempts: 3
retry_delay: 1000
connection_validation: true
validation_query: "SELECT 1"
test_on_borrow: true
```


### Success metrics

**Error rate:**<0.01% during upgrades**Response time:**<10% degradation**Recovery time:**<30 seconds after node replacement

## Monitoring and alerting setup

To learn more, see the [AKS monitoring overview](monitor-aks), [Container Insights](/en-us/azure/azure-monitor/containers/container-insights-overview), and [Prometheus metrics](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview).

### Essential metrics to monitor

```
# upgrade-monitoring.yaml
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
name: upgrade-monitoring
spec:
groups:
- name: upgrade.rules
rules:
- alert: UpgradeInProgress
expr: kube_node_spec_unschedulable > 0
for: 1m
annotations:
summary: "Node upgrade in progress"
- alert: HighErrorRate
expr: rate(http_requests_total{status=~"5.."}[5m]) > 0.01
for: 2m
annotations:
summary: "High error rate during upgrade"
- alert: PodEvictionFailed
expr: increase(kube_pod_container_status_restarts_total[5m]) > 5
for: 1m
annotations:
summary: "Multiple pod restarts detected"
```


### Dashboard configuration

```
{
"dashboard": {
"title": "AKS Upgrade Dashboard",
"panels": [
{
"title": "Upgrade Progress",
"targets":
[
"kube_node_info",
"kube_node_status_condition"
]
},
{
"title": "Application Health",
"targets":
[
"up{job='kubernetes-pods'}",
"http_request_duration_seconds"
]
}
]
}
}
```


## Troubleshooting guide

To learn more, see the [AKS troubleshooting guide](/en-us/azure/aks/troubleshooting), [Node and pod troubleshooting](node-access), and [Upgrade error messages](upgrade-aks-cluster#troubleshoot-aks-cluster-upgrade-error-messages).

### Common issues and solutions

| Issue | Symptoms | Solution |
|---|---|---|
| Stuck node drain | Pods won't evict. | Check PDB configuration, increase drain timeout. |
| High error rates | 5xx responses are increasing. | Verify health checks, check resource limits. |
| Slow upgrades | Takes >2 hours. | Increase `maxSurge` , optimize container startup. |
| DNS resolution | Service discovery is failing. | Verify `CoreDNS` pods, check service endpoints. |

### Emergency rollback procedures

```
# Quick rollback script
#!/bin/bash
echo "Initiating emergency rollback..."
# Switch traffic back to previous cluster
az network traffic-manager endpoint update \
--resource-group traffic-rg \
--profile-name production-tm \
--name current-endpoint \
--target-resource-id "/subscriptions/.../clusters/aks-previous"
# Verify rollback success
curl -f https://api.production.com/health
echo "Rollback completed in $(date)"
```


## Related resources

### Specialized scenarios

[Stateful workloads](stateful-workload-upgrades): Use PostgreSQL, Redis, and MongoDB upgrade patterns.[Upgrade scenarios hub](upgrade-scenarios-hub): Choose your upgrade path.[Basic AKS upgrades](upgrade-aks-cluster): Find simple cluster version upgrades.

### Supporting tools

[Auto-upgrade configuration](auto-upgrade-cluster): Use automated upgrade channels.[Maintenance windows](planned-maintenance): Schedule upgrade windows.[Upgrade monitoring](aks-communication-manager): Use real-time upgrade alerts.

### Best practices

[Cluster reliability](best-practices-app-cluster-reliability): Design for upgrades.[Security guidelines](operator-best-practices-cluster-security): Use secure upgrade practices.[Support policies](support-policies): Understand upgrade support windows.

## Next tasks

**Set up monitoring:**Configure[upgrade notifications](aks-communication-manager)before your first upgrade.**Practice safely:**Test scenarios in staging by using[cluster snapshots](node-pool-snapshot).**Automate gradually:**Start with[auto-upgrade channels](auto-upgrade-cluster)for nonproduction.**Handle stateful data:**Review[stateful workload patterns](stateful-workload-upgrades)if you run databases.

## Related content

- For more help, see
[AKS support options](aks-support-help)or review[common upgrade scenarios](upgrade-cluster#common-upgrade-scenarios-and-recommendations).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-gateway-api -->

# Configure Istio ingress with the Kubernetes Gateway API for Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

The Istio service mesh add-on supports both [Istio's own ingress traffic management API](istio-deploy-ingress) and the Kubernetes Gateway API for ingress traffic management. You can use the Istio Gateway API [automated deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#automated-deployment) or the [manual deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#manual-deployment). This article describes how to configure ingress traffic management for the Istio service mesh add-on using the Kubernetes Gateway API with the [automated deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#automated-deployment).

## Limitations and considerations

- Using the Kubernetes Gateway API for
[egress traffic management](istio-deploy-egress)with the Istio service mesh add-on is only supported for the[manual deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#manual-deployment). - ConfigMap customizations for
`Gateway`

resources must fall within the Resource customization allow list. Fields not on the allow list are disallowed and blocked via add-on managed webhooks. For more information, see the[Istio service mesh add-on support policy](istio-support-policy#allowed-supported-and-blocked-customizations).

## Prerequisites

- Enable the
[Managed Gateway API](managed-gateway-api)on your AKS cluster. - Install the Istio service mesh add-on revision
`asm-1-26`

or higher. Follow the[installation guide](istio-deploy-addon)if you don't have the Istio service mesh add-on installed yet, or the[upgrade guide](istio-upgrade)if you're on a lower minor revision.

## Set environment variables

Set the following environment variables to use throughout this article:

| Variable | Description |
|---|---|
`RESOURCE_GROUP` |
The name of the resource group containing your AKS cluster. |
`CLUSTER_NAME` |
The name of your AKS cluster. |
`LOCATION` |
The Azure region where your AKS cluster is deployed. |
`KEY_VAULT_NAME` |
The name of the Azure Key Vault resource to be created for storing TLS secrets. If you have an existing resource, use that name. |

## Deploy sample application

Deploy the sample

`httpbin`

application in the`default`

namespace using thecommand.`kubectl apply`

`kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.26/samples/httpbin/httpbin.yaml`


## Create Kubernetes Gateway and HTTPRoute

The example manifest creates an external ingress load balancer service that's accessible from outside the cluster. You can add [annotations](#annotation-customizations) to create an internal load balancer and customize other load balancer settings.

Deploy a Gateway API configuration in the

`default`

namespace with the`gatewayClassName`

set to`istio`

and an`HTTPRoute`

that routes traffic to the`httpbin`

service using the following manifest:`kubectl apply -f - <<EOF apiVersion: gateway.networking.k8s.io/v1 kind: Gateway metadata: name: httpbin-gateway spec: gatewayClassName: istio listeners: - name: http port: 80 protocol: HTTP allowedRoutes: namespaces: from: Same --- apiVersion: gateway.networking.k8s.io/v1 kind: HTTPRoute metadata: name: http namespace: default spec: parentRefs: - name: httpbin-gateway hostnames: ["httpbin.example.com"] rules: - matches: - path: type: PathPrefix value: /get backendRefs: - name: httpbin port: 8000 EOF`

Note

If you're performing a

[minor revision upgrade](istio-upgrade)and have two Istio service mesh add-on revisions installed on your cluster simultaneously, the control plane for the higher minor revision takes ownership of the`Gateways`

by default. You can add the`istio.io/rev`

label to the`Gateway`

to control which control plane revision owns it. If you add the revision label, make sure that you update it accordingly to the appropriate control plane revision before rolling back or completing the upgrade operation.

## Verify resource creation

Verify the

`Deployment`

,`Service`

,`HorizontalPodAutoscaler`

, and`PodDisruptionBudget`

resources were created using the following`kubectl get`

commands:`kubectl get deployment httpbin-gateway-istio kubectl get service httpbin-gateway-istio kubectl get hpa httpbin-gateway-istio kubectl get pdb httpbin-gateway-istio`

Example output:

`# Deployment resource NAME READY UP-TO-DATE AVAILABLE AGE httpbin-gateway-istio 2/2 2 2 31m # Service resource NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE httpbin-gateway-istio LoadBalancer 10.0.65.45 <external-ip> 15021:32053/TCP,80:31587/TCP 33m # HPA resource NAME REFERENCE TARGETS MINPODS MAXPODS REPLICAS AGE httpbin-gateway-istio Deployment/httpbin-gateway-istio cpu: 3%/80% 2 5 3 34m # PDB resource NAME MIN AVAILABLE MAX UNAVAILABLE ALLOWED DISRUPTIONS AGE httpbin-gateway-istio 1 N/A 2 36m`


## Send request to sample application

Try sending a

`curl`

request to the`httpbin`

application. First, set the`INGRESS_HOST`

environment variable:`kubectl wait --for=condition=programmed gateways.gateway.networking.k8s.io httpbin-gateway export INGRESS_HOST=$(kubectl get gateways.gateway.networking.k8s.io httpbin-gateway -ojsonpath='{.status.addresses[0].value}')`

Try sending an HTTP request to

`httpbin`

.`curl -s -I -HHost:httpbin.example.com "http://$INGRESS_HOST/get"`

In the output, you should see an

`HTTP 200`

response.

## Secure Istio ingress traffic with the Kubernetes Gateway API

The Istio service mesh add-on supports syncing secrets from Azure Key Vault for securing Gateway API-based ingress traffic with [Transport Layer Security (TLS) termination](https://istio.io/latest/docs/tasks/traffic-management/ingress/secure-ingress/) or [Server Name Indication (SNI) passthrough](https://istio.io/latest/docs/tasks/traffic-management/ingress/ingress-sni-passthrough/). In the following sections, you sync secrets from Azure Key Vault onto your AKS cluster using the [Azure Key Vault provider for Secrets Store Container Storage Interface (CSI) Driver add-on](csi-secrets-store-driver) and terminate TLS at the ingress gateway.

## Create client/server certificates and keys

Create a root certificate and private key for signing the certificates for sample services:

`mkdir httpbin_certs openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -subj '/O=example Inc./CN=example.com' -keyout httpbin_certs/example.com.key -out httpbin_certs/example.com.crt`

Generate a certificate and a private key for

`httpbin.example.com`

:`openssl req -out httpbin_certs/httpbin.example.com.csr -newkey rsa:2048 -nodes -keyout httpbin_certs/httpbin.example.com.key -subj "/CN=httpbin.example.com/O=httpbin organization" openssl x509 -req -sha256 -days 365 -CA httpbin_certs/example.com.crt -CAkey httpbin_certs/example.com.key -set_serial 0 -in httpbin_certs/httpbin.example.com.csr -out httpbin_certs/httpbin.example.com.crt`


## Set up Azure Key Vault and create secrets

Create an Azure Key Vault instance to supply the certificate and key inputs to the Istio service mesh add-on using the

command. If you already have an Azure Key Vault instance, you can skip this step.`az keyvault create`

`az keyvault create --name $KEY_VAULT_NAME --resource-group $RESOURCE_GROUP --location $LOCATION`

Enable the

[Azure Key Vault provider for Secrets Store (CSI) Driver add-on](csi-secrets-store-driver)on your cluster using thecommand.`az aks enable-addons`

`az aks enable-addons --addons azure-keyvault-secrets-provider --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`

If your key vault uses Azure role-based access control (RBAC) for the permissions model, follow the instructions in

[Provide access to Azure Key Vault keys, certificates, and secrets with Azure role-based access control](/en-us/azure/key-vault/general/rbac-guide)to assign an Azure role of*Key Vault Secrets User*for the add-on's user-assigned managed identity. Alternatively, if your key vault uses the vault access policy permissions model, authorize the user-assigned managed identity of the add-on to access Azure Key Vault resource using access policy using thecommand.`az keyvault set-policy`

`OBJECT_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query 'addonProfiles.azureKeyvaultSecretsProvider.identity.objectId' -o tsv | tr -d '\r') CLIENT_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query 'addonProfiles.azureKeyvaultSecretsProvider.identity.clientId') TENANT_ID=$(az keyvault show --resource-group $RESOURCE_GROUP --name $KEY_VAULT_NAME --query 'properties.tenantId') az keyvault set-policy --name $KEY_VAULT_NAME --object-id $OBJECT_ID --secret-permissions get list`

Create secrets in Azure Key Vault using the certificates and keys using the following

commands:`az keyvault secret set`

`az keyvault secret set --vault-name $KEY_VAULT_NAME --name test-httpbin-key --file httpbin_certs/httpbin.example.com.key az keyvault secret set --vault-name $KEY_VAULT_NAME --name test-httpbin-crt --file httpbin_certs/httpbin.example.com.crt`


## Deploy SecretProviderClass and sample pod

Deploy the SecretProviderClass to provide Azure Key Vault specific parameters to the CSI driver using the following manifest. In this example,

`test-httpbin-key`

and`test-httpbin-crt`

are the names of the secret objects in Azure Key Vault.`cat <<EOF | kubectl apply -f - apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: httpbin-credential-spc spec: provider: azure secretObjects: - secretName: httpbin-credential type: kubernetes.io/tls data: - objectName: test-httpbin-key key: tls.key - objectName: test-httpbin-crt key: tls.crt parameters: useVMManagedIdentity: "true" userAssignedIdentityID: $CLIENT_ID keyvaultName: $KEY_VAULT_NAME cloudName: "" objects: | array: - | objectName: test-httpbin-key objectType: secret objectAlias: "test-httpbin-key" - | objectName: test-httpbin-crt objectType: secret objectAlias: "test-httpbin-crt" tenantId: $TENANT_ID EOF`

Note

Alternatively, to reference a certificate object type directly from Azure Key Vault, use the following manifest to deploy SecretProviderClass. In this example,

`test-httpbin-cert-pxf`

is the name of the certificate object in Azure Key Vault.`cat <<EOF | kubectl apply -f - apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: httpbin-credential-spc spec: provider: azure secretObjects: - secretName: httpbin-credential type: kubernetes.io/tls data: - objectName: test-httpbin-key key: tls.key - objectName: test-httpbin-crt key: tls.crt parameters: useVMManagedIdentity: "true" userAssignedIdentityID: $CLIENT_ID keyvaultName: $KEY_VAULT_NAME cloudName: "" objects: | array: - | objectName: test-httpbin-cert-pfx #certificate object name from keyvault objectType: secret objectAlias: "test-httpbin-key" - | objectName: test-httpbin-cert-pfx #certificate object name from keyvault objectType: cert objectAlias: "test-httpbin-crt" tenantId: $TENANT_ID EOF`

Deploy a sample pod using the following manifest. The Azure Key Vault provider for Secrets Store (CSI) Driver add-on requires a pod to reference the SecretProviderClass resource to ensure secrets sync from Azure Key Vault to the cluster.

`cat <<EOF | kubectl apply -f - apiVersion: v1 kind: Pod metadata: name: secrets-store-sync-httpbin spec: containers: - name: busybox image: mcr.microsoft.com/oss/busybox/busybox:1.33.1 command: - "/bin/sleep" - "10" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "httpbin-credential-spc" EOF`


## Verify TLS secret creation

Verify the

`httpbin-credential`

secret was created in the`default`

namespace as defined in the SecretProviderClass resource using the`kubectl describe secret`

command.`kubectl describe secret/httpbin-credential`

Example output:

`Name: httpbin-credential Namespace: default Labels: secrets-store.csi.k8s.io/managed=true Annotations: <none> Type: kubernetes.io/tls Data ==== tls.crt: 1180 bytes tls.key: 1675 bytes`


## Deploy TLS Gateway

Create a Kubernetes Gateway that references the

`httpbin-credential`

secret under the TLS configuration using the following manifest:`cat <<EOF | kubectl apply -f - apiVersion: gateway.networking.k8s.io/v1 kind: Gateway metadata: name: httpbin-gateway spec: gatewayClassName: istio listeners: - name: https hostname: "httpbin.example.com" port: 443 protocol: HTTPS tls: mode: Terminate certificateRefs: - name: httpbin-credential allowedRoutes: namespaces: from: Selector selector: matchLabels: kubernetes.io/metadata.name: default EOF`

Note

In the gateway definition,

`tls.certificateRefs.name`

must match the`secretName`

in SecretProviderClass resource.Create a corresponding

`HTTPRoute`

to configure ingress traffic routing to the`httpbin`

service over HTTPS using the following manifest:`cat <<EOF | kubectl apply -f - apiVersion: gateway.networking.k8s.io/v1 kind: HTTPRoute metadata: name: httpbin spec: parentRefs: - name: httpbin-gateway hostnames: ["httpbin.example.com"] rules: - matches: - path: type: PathPrefix value: /status - path: type: PathPrefix value: /delay backendRefs: - name: httpbin port: 8000 EOF`

Get the ingress gateway's external IP address and secure port using the following commands:

`kubectl wait --for=condition=programmed gateways.gateway.networking.k8s.io httpbin-gateway export INGRESS_HOST=$(kubectl get gateways.gateway.networking.k8s.io httpbin-gateway -o jsonpath='{.status.addresses[0].value}') export SECURE_INGRESS_PORT=$(kubectl get gateways.gateway.networking.k8s.io httpbin-gateway -o jsonpath='{.spec.listeners[?(@.name=="https")].port}')`

Send an HTTPS request to access the

`httpbin`

service:`curl -v -HHost:httpbin.example.com --resolve "httpbin.example.com:$SECURE_INGRESS_PORT:$INGRESS_HOST" \ --cacert httpbin_certs/example.com.crt "https://httpbin.example.com:$SECURE_INGRESS_PORT/status/418"`

The output should show the

`httpbin`

service return the*418 I’m a Teapot*code.Note

To configure HTTPS ingress access to an HTTPS service, update the TLS mode in the gateway definition to

`Passthrough`

. This configuration instructs the gateway to pass the ingress traffic*as is*, without terminating TLS.

## Annotation customizations

You can add annotations under `spec.infrastructure.annotations`

to [configure load balancer settings](configure-load-balancer-standard#customizations-via-kubernetes-annotations) for the `Gateway`

. For instance, to create an internal load balancer attached to a specific subnet, you can create a `Gateway`

with the following annotations:

```
spec:
# ... existing spec content ...
infrastructure:
annotations:
service.beta.kubernetes.io/azure-load-balancer-internal: "true"
service.beta.kubernetes.io/azure-load-balancer-internal-subnet: "my-subnet"
```


## ConfigMap customizations

The Istio service mesh add-on supports [customizations of the resources](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#automated-deployment) generated for the `Gateways`

, including:

- Service
- Deployment
- Horizontal Pod Autoscaler (HPA)
- Pod Disruption Budget (PDB)

The [default settings for these resources](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#gatewayclass-defaults) are set in the `istio-gateway-class-defaults`

ConfigMap in the `aks-istio-system`

namespace. This ConfigMap must have the `gateway.istio.io/defaults-for-class`

label set to `istio`

for the customizations to take effect for all `Gateways`

with `spec.gatewayClassName: istio`

. The `GatewayClass`

-level ConfigMap is installed by default in the `aks-istio-system`

namespace when the [Managed Gateway API installation](managed-gateway-api) is enabled. It could take up to five minutes for the `istio-gateway-class-defaults`

ConfigMap to get deployed after installing the Managed Gateway API CRDs.

```
kubectl get configmap istio-gateway-class-defaults -n aks-istio-system -o yaml
```


```
...
data:
horizontalPodAutoscaler: |
spec:
minReplicas: 2
maxReplicas: 5
podDisruptionBudget: |
spec:
minAvailable: 1
...
```


You can modify these settings for all Istio `Gateways`

at a `GatewayClass`

level by updating the `istio-gateway-class-defaults`

ConfigMap, or you can set them for individual `Gateway`

resources. For both the `GatewayClass`

-level and `Gateway`

-level `ConfigMaps`

, you must add fields to the allow list for the given resource. If there are customizations both for the `GatewayClass`

and an individual `Gateway`

, the `Gateway`

-level configuration takes precedence.

## Deployment customization allow list fields

| Field path | Description |
|---|---|
`metadata.labels` |
Deployment labels |
`metadata.annotations` |
Deployment annotations |
`spec.replicas` |
Deployment replica count |
`spec.template.metadata.labels` |
Pod labels |
`spec.template.metadata.annotations` |
Pod annotations |
`spec.template.spec.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms` |
Node affinity |
`spec.template.spec.affinity.nodeAffinity.preferredDuringSchedulingIgnoredDuringExecution` |
Node affinity |
`spec.template.spec.affinity.podAffinity.requiredDuringSchedulingIgnoredDuringExecution` |
Pod affinity |
`spec.template.spec.affinity.podAffinity.preferredDuringSchedulingIgnoredDuringExecution` |
Pod affinity |
`spec.template.spec.affinity.podAntiAffinity.requiredDuringSchedulingIgnoredDuringExecution` |
Pod anti-affinity |
`spec.template.spec.affinity.podAntiAffinity.preferredDuringSchedulingIgnoredDuringExecution` |
Pod anti-affinity |
`spec.template.spec.containers.resizePolicy` |
Container resource utilization |
`spec.template.spec.containers.resources.limits` |
Container resource utilization |
`spec.template.spec.containers.resources.requests` |
Container resource utilization |
`spec.template.spec.containers.stdin` |
Container debugging |
`spec.template.spec.containers.stdinOnce` |
Container debugging |
`spec.template.spec.nodeSelector` |
Pod scheduling |
`spec.template.spec.nodeName` |
Pod scheduling |
`spec.template.spec.tolerations` |
Pod scheduling |
`spec.template.spec.topologySpreadConstraints` |
Pod scheduling |

## Service customization allow list fields

| Field path | Description |
|---|---|
`metadata.labels` |
Service labels |
`metadata.annotations` |
Service annotations |
`spec.type` |
Service type |
`spec.loadBalancerSourceRanges` |
Service load balancer settings |
`spec.loadBalancerClass` |
Service load balancer settings |
`spec.externalTrafficPolicy` |
Service traffic policy |
`spec.internalTrafficPolicy` |
Service traffic policy |

## HorizontalPodAutoscaler (HPA) customization allow list fields

| Field path | Description |
|---|---|
`metadata.labels` |
HPA labels |
`metadata.annotations` |
HPA annotations |
`spec.behavior.scaleUp.stabilizationWindowSeconds` |
HPA scale-up behavior |
`spec.behavior.scaleUp.selectPolicy` |
HPA scale-up behavior |
`spec.behavior.scaleUp.policies` |
HPA scale-up behavior |
`spec.behavior.scaleDown.stabilizationWindowSeconds` |
HPA scale-down behavior |
`spec.behavior.scaleDown.selectPolicy` |
HPA scale-down behavior |
`spec.behavior.scaleDown.policies` |
HPA scale-down behavior |
`spec.metrics` |
HPA scaling resource metrics |
`spec.minReplicas` |
HPA minimum replica count. Must not be below 2. |
`spec.maxReplicas` |
HPA maximum replica count |

## PodDisruptionBudget (PDB) customization allow list fields

| Field path | Description |
|---|---|
`metadata.labels` |
PDB labels |
`metadata.annotations` |
PDB annotations |
`spec.minAvailable` |
PDB minimum availability |
`spec.unhealthyPodEvictionPolicy` |
PDB eviction policy |

Note

Modifying the `PDB`

minimum availability and eviction policy can lead to potential errors during cluster/node upgrade and deletion operations. Follow the [PDB troubleshooting guide](/en-us/troubleshoot/azure/azure-kubernetes/create-upgrade-delete/error-code-poddrainfailure) to address *UpgradeFailed* errors due to `PDB`

eviction failures.

## Configure GatewayClass-level settings

Update the

`GatewayClass`

-level ConfigMap in the`aks-istio-system`

namespace using the`kubectl edit configmap`

command:`kubectl edit cm istio-gateway-class-defaults -n aks-istio-system`

Edit the resource settings in the

`data`

section as needed. For example, to update the HPA min/max replicas and add a label to the`Deployment`

, modify the ConfigMap as follows:`... data: deployment: | metadata: labels: test.azureservicemesh.io/deployment-config: "updated" horizontalPodAutoscaler: | spec: minReplicas: 3 maxReplicas: 6 podDisruptionBudget: | spec: minAvailable: 1 ...`

Note

Only one ConfigMap per

`GatewayClass`

is allowed.Now, you should see the

`HPA`

for`httpbin-gateway`

that you created earlier get updated with the new min/max values. Verify the`HPA`

settings using the`kubectl get hpa`

command.`kubectl get hpa httpbin-gateway-istio`

Example output:

`NAME REFERENCE TARGETS MINPODS MAXPODS REPLICAS AGE httpbin-gateway-istio Deployment/httpbin-gateway-istio cpu: 3%/80% 3 6 3 36m`

Verify the

`Deployment`

is updated with the new label using the`kubectl get deployment`

command.`kubectl get deployment httpbin-gateway-istio -ojsonpath='{.metadata.labels.test\.azureservicemesh\.io\/deployment-config}'`

Example output:

`updated`


## Configure settings for a specific gateway

Create a ConfigMap with resource customizations for the

`httpbin`

Gateway using the following manifest:`kubectl apply -f - <<EOF apiVersion: v1 kind: ConfigMap metadata: name: gw-options data: horizontalPodAutoscaler: | spec: minReplicas: 2 maxReplicas: 4 deployment: | metadata: labels: test.azureservicemesh.io/deployment-config: "updated-per-gateway" EOF`

Update the

`httpbin`

`Gateway`

to reference the ConfigMap:`spec: # ... existing spec content ... infrastructure: parametersRef: group: "" kind: ConfigMap name: gw-options`

Apply the update using the

`kubectl apply`

command.`kubectl apply -f httpbin-gateway-updated.yaml`

Verify the

`HPA`

is updated with the new min/max values using the`kubectl get hpa`

command. If you also configured the`GatewayClass`

-level ConfigMap, the`Gateway`

-level settings should take precedence.`kubectl get hpa httpbin-gateway-istio`

Example output:

`NAME REFERENCE TARGETS MINPODS MAXPODS REPLICAS AGE httpbin-gateway-istio Deployment/httpbin-gateway-istio cpu: 3%/80% 2 4 2 4h14m`

Inspect the

`Deployment`

labels to ensure that the`test.azureservicemesh.io/deployment-config`

is updated to the new value using the`kubectl get deployment`

command.`kubectl get deployment httpbin-gateway-istio -ojsonpath='{.metadata.labels.test\.azureservicemesh\.io\/deployment-config}'`

Example output:

`updated-per-gateway`


## Clean up resources

If you no longer need the resources created in this article, you can delete them to avoid incurring any charges.

Delete the Gateway and HTTPRoute resources using the following

`kubectl delete`

commands:`kubectl delete gateways.gateway.networking.k8s.io httpbin-gateway kubectl delete httproute httpbin`

If you created a ConfigMap to customize your Gateway resources, delete it using the

`kubectl delete configmap`

command.`kubectl delete configmap gw-options`

If you created a SecretProviderClass and secret to use for TLS termination delete the resources using the following

`kubectl delete`

commands:`kubectl delete secret httpbin-credential kubectl delete pod secrets-store-sync-httpbin kubectl delete secretproviderclass httpbin-credential-spc`

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-windows-gpu -->

# Use Windows GPUs for compute-intensive workloads on Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Graphical processing units (GPUs) are often used for compute-intensive workloads, such as graphics and visualization workloads. AKS supports GPU-enabled Windows and [Linux](gpu-cluster) node pools to run compute-intensive Kubernetes workloads.

This article helps you provision Windows nodes with schedulable GPUs on new and existing AKS clusters (preview).

## Supported GPU-enabled virtual machines (VMs)

To view supported GPU-enabled VMs, see [GPU-optimized VM sizes in Azure](/en-us/azure/virtual-machines/sizes-gpu). For AKS node pools, we recommend a minimum size of *Standard_NC6s_v3*. The NVv4 series (based on AMD GPUs) aren't supported on AKS.

Note

GPU-enabled VMs contain specialized hardware subject to higher pricing and region availability. For more information, see the [pricing](https://azure.microsoft.com/pricing/) tool and [region availability](https://azure.microsoft.com/global-infrastructure/services/).

## Limitations

- Updating an existing Windows node pool to add GPU isn't supported.
- Not supported on Kubernetes version 1.28 and below.

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-windows-container-deploy-cli),[Azure PowerShell](learn/quick-windows-container-deploy-powershell), or the[Azure portal](learn/quick-windows-container-deploy-portal). - You need the Azure CLI version 2.72.2 or later installed and configured to use the
`--gpu-driver`

field with the`az aks nodepool add`

command. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you have the
`aks-preview`

Azure CLI extension installed, please update the version to 18.0.0b2 or later.

## Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command. The following example command gets the credentials for the`az aks get-credentials`

*myAKSCluster*in the*myResourceGroup*resource group:`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Using Windows GPU with automatic driver installation

Using NVIDIA GPUs involves the installation of various NVIDIA software components such as the [DirectX device plugin for Kubernetes](https://github.com/aarnaud/k8s-directx-device-plugin), GPU driver installation, and more. When you create a Windows node pool with a supported GPU-enabled VM, these components and the appropriate NVIDIA CUDA or GRID drivers are installed. For NC and ND series VM sizes, the CUDA driver is installed. For NV series VM sizes, the GRID driver is installed.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Install the `aks-preview`

Azure CLI extension

Register or update the aks-preview extension using the

or`az extension add`

command.`az extension update`

`# Register the aks-preview extension az extension add --name aks-preview # Update the aks-preview extension az extension update --name aks-preview`


### Register the `WindowsGPUPreview`

feature flag

Register the

`WindowsGPUPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "WindowsGPUPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "WindowsGPUPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create a Windows GPU-enabled node pool (preview)

To create a Windows GPU-enabled node pool, you need to use a supported GPU-enabled VM size and specify the `os-type`

as `Windows`

. The default Windows `os-sku`

is `Windows2022`

, but all Windows `os-sku`

options are supported.

Create a Windows GPU-enabled node pool using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --os-type Windows \ --kubernetes-version 1.29.0 \ --node-vm-size Standard_NC6s_v3`

Check that your

[GPUs are schedulable](#confirm-that-gpus-are-schedulable).Once you confirm that your GPUs are schedulable, you can run your GPU workload.


#### Specify GPU Driver Type (preview)

By default, AKS specifies a default GPU driver type for each supported GPU-enabled VM. Because workload and driver compatibility are important for functioning GPU workloads, you can specify the driver type for your Windows GPU node. This feature is not supported for Linux GPU node pools.

When creating a Windows agent pool with GPU support, you have the option to specify the type of GPU driver using the `--driver-type`

flag.

The available options are:

- GRID: For applications requiring virtualization support.
- CUDA: Optimized for computational tasks in scientific computing and data-intensive applications.

Note

When you set the `--driver-type`

flag, you assume responsibility for ensuring that the selected driver type is compatible with the specific VM size and configuration of your node pool. While AKS attempts to validate compatibility, there are scenarios where the node pool creation might fail due to incompatibilities between the specified driver type and the underlying VM or hardware.

To create a Windows GPU-enabled node pool with a specific GPU Driver type, use the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name gpunp \
--node-count 1 \
--os-type Windows \
--kubernetes-version 1.29.0 \
--node-vm-size Standard_NC6s_v3 \
--driver-type GRID
```


For example, the above command creates a GPU-enabled node pool using the `GRID`

GPU driver type. Selecting this driver type overrides the default of `CUDA`

driver type for NC series VM skus.

## Using Windows GPU with manual driver installation

When creating a Windows node pool with N-series (NVIDIA GPU) VM sizes in AKS, the GPU driver and Kubernetes DirectX device plugin are installed automatically. To bypass this automatic installation, use the following steps:

[Skip GPU driver installation](#skip-gpu-driver-installation)by setting the configuration`--gpu-driver none`

at node pool create time.[Manual installation of the Kubernetes DirectX device plugin](#manually-install-the-kubernetes-directx-device-plugin).

### Skip GPU driver installation

AKS has automatic GPU driver installation enabled by default. In some cases, such as installing your own drivers, you may want to skip GPU driver installation.

Note

The `gpu-driver`

API field is a suggested alternative for customers previously using the `--skip-gpu-driver-install`

node pool tag.

- The
`--skip-gpu-driver-install`

node pool tag on AKS will be retired on 14 August 2025. To retain the existing behavior of skipping automatic GPU driver installation, upgrade your node pools to the latest node image version and set the`--gpu-driver`

field to`none`

. After 14 August 2025, you won't be able to provision AKS GPU-enabled node pools with the`--skip-gpu-driver-install`

node pool tag to bypass this default behavior. For more information, see.`skip-gpu-driver`

tag retirement

Create a node pool using the

command and setting the API field`az aks nodepool add`

`--gpu-driver`

to`none`

to skip automatic GPU driver installation.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --os-type windows \ --os-sku windows2022 \ --gpu-driver none`


Note

If the `--node-vm-size`

that you're using isn't yet onboarded on AKS, you can't use GPUs and the `--gpu-driver`

field doesn't work.

### Manually install the Kubernetes DirectX device plugin

You can deploy a DaemonSet for the Kubernetes DirectX device plugin, which runs a pod on each node to provide the required drivers for the GPUs.

Add a node pool to your cluster using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --os-type windows \ --os-sku windows2022`


## Create a namespace and deploy the Kubernetes DirectX device plugin

Create a namespace using the

command.`kubectl create namespace`

`kubectl create namespace gpu-resources`

Create a file named

*k8s-directx-device-plugin.yaml*and paste the following YAML manifest provided as part of the[NVIDIA device plugin for Kubernetes project](https://github.com/NVIDIA/k8s-device-plugin):`apiVersion: apps/v1 kind: DaemonSet metadata: name: nvidia-device-plugin-daemonset namespace: gpu-resources spec: selector: matchLabels: name: nvidia-device-plugin-ds updateStrategy: type: RollingUpdate template: metadata: # Mark this pod as a critical add-on; when enabled, the critical add-on scheduler # reserves resources for critical add-on pods so that they can be rescheduled after # a failure. This annotation works in tandem with the toleration below. annotations: scheduler.alpha.kubernetes.io/critical-pod: "" labels: name: nvidia-device-plugin-ds spec: tolerations: # Allow this pod to be rescheduled while the node is in "critical add-ons only" mode. # This, along with the annotation above marks this pod as a critical add-on. - key: CriticalAddonsOnly operator: Exists - key: nvidia.com/gpu operator: Exists effect: NoSchedule - key: "sku" operator: "Equal" value: "gpu" effect: "NoSchedule" containers: - image: mcr.microsoft.com/aks/aks-windows-gpu-device-plugin:0.0.17 name: nvidia-device-plugin-ctr securityContext: allowPrivilegeEscalation: false capabilities: drop: ["ALL"] volumeMounts: - name: device-plugin mountPath: /var/lib/kubelet/device-plugins volumes: - name: device-plugin hostPath: path: /var/lib/kubelet/device-plugins`

Create the DaemonSet and confirm the NVIDIA device plugin is created successfully using the

command.`kubectl apply`

`kubectl apply -f nvidia-device-plugin-ds.yaml`

Now that you successfully installed the NVIDIA device plugin, you can check that your

[GPUs are schedulable](#confirm-that-gpus-are-schedulable).

## Confirm that GPUs are schedulable

After creating your cluster, confirm that GPUs are schedulable in Kubernetes.

List the nodes in your cluster using the

command.`kubectl get nodes`

`kubectl get nodes`

Your output should look similar to the following example output:

`NAME STATUS ROLES AGE VERSION aks-gpunp-28993262-0 Ready agent 13m v1.20.7`

Confirm the GPUs are schedulable using the

command.`kubectl describe node`

`kubectl describe node aks-gpunp-28993262-0`

Under the

*Capacity*section, the GPU should list as`microsoft.com/directx: 1`

. Your output should look similar to the following condensed example output:`Capacity: [...] microsoft.com.directx/gpu: 1 [...]`


## Clean up resources

Remove the associated Kubernetes objects you created in this article using the

command.`kubectl delete job`

`kubectl delete jobs windows-gpu-workload`


## Next steps

- To run Apache Spark jobs, see
[Run Apache Spark jobs on AKS](spark-job). - For more information on features of the Kubernetes scheduler, see
[Best practices for advanced scheduler features in AKS](operator-best-practices-advanced-scheduler). - For more information on Azure Kubernetes Service and Azure Machine Learning, see:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-aks-node-pools-rolling -->

# Configure rolling upgrades for Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A rolling upgrade strategy upgrades nodes one at a time (or a few at a time), minimizing workload disruption while ensuring the node pool remains available throughout the upgrade process. This article explains how to configure rolling upgrades for AKS node pools, including surge settings, drain timeout, and soak time.

## Before you begin

- Ensure your control plane is already upgraded to the target Kubernetes version. You can't upgrade node pools to a version higher than the control plane. For more information, see
[Upgrade the AKS cluster control plane](upgrade-aks-control-plane). - If you're using the Azure CLI, this article requires Azure CLI version 2.34.1 or later. Use the
`az --version`

command to find the version. If you need to install or upgrade, see [Install Azure CLI][azure-cli-install]. - You need the
`Microsoft.ContainerService/managedClusters/agentPools/write`

RBAC role permission to configure rolling upgrades for AKS node pools.

## Overview of rolling upgrade behavior

During a rolling upgrade, AKS performs the following operations for each node in the node pool:

**Add surge nodes**: Add new buffer nodes based on max surge (`--max-surge`

) settings to maintain capacity during the upgrade.**Cordon and drain nodes**:[Cordon and drain](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)the old nodes one at a time to minimize disruption to running applications. If you're using max surge, it cordons and drains as many nodes at the same time as the number of buffer nodes specified.**Wait for soak time**(optional): Wait for a configured[soak duration](#set-node-soak-time-value)before proceeding to allow workloads to stabilize on the new nodes before continuing the upgrade.**Reimage old nodes**: When the old nodes are drained, they're reimaged to receive the new version. The reimaged nodes become the buffer nodes for the next set of nodes to be upgraded.**Repeat**: The process repeats until all nodes in the node pool are upgraded.**Remove surge nodes**: After all nodes are upgraded, any remaining buffer nodes are removed, maintaining the original node pool size and balance.

## Configure rolling upgrade settings

### Customize node surge

Important

- Node surges require subscription quota for the requested max surge count for each upgrade operation. For example, a cluster that has five node pools, each with a count of four nodes, has a total of 20 nodes. If each node pool has a max surge value of 50%, extra compute and IP quota of 10 nodes (
*two*nodes ×*five*pools) is required to complete the upgrade. - The max surge setting on a node pool is persistent. Subsequent Kubernetes upgrades or node version upgrades use this setting. You can change the max surge value for your node pools at any time. For production node pools, we recommend a max surge setting of 33%.
- If you're using Azure CNI, validate there are available IPs in the subnet to
[satisfy IP requirements of Azure CNI](configure-azure-cni).

AKS configures upgrades to surge with one extra node by default. A default value of *one* for the max surge setting enables AKS to minimize workload disruption by creating an extra node before the cordon/drain of existing applications to replace an older versioned node. You can customize the max surge value per node pool. When you increase the max surge value, the upgrade process completes faster, but you might experience more disruptions during the upgrade process.

For example, a max surge value of `100%`

provides the fastest possible upgrade process but also causes all nodes in the node pool to be drained simultaneously. You might want to use a higher value like this for testing environments. For production node pools, we recommend a max surge setting of `33%`

.

AKS accepts both integer values and a percentage value for max surge. For example:

| Value type | Example | Description |
|---|---|---|
| Integer | `5` |
Five extra nodes to surge |
| Percentage | `50%` |
Surge value of half the current node count in the pool |

Max surge percent values can be a minimum of `1%`

and a maximum of `100%`

. A percent value is rounded up to the nearest node count. If the max surge value is higher than the required number of nodes to be upgraded, the number of nodes to be upgraded is used for the max surge value.

#### Set max surge value

Set max surge values for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) or

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

`--max-surge`

parameter. For example:```
# Set max surge for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 33%
# Update max surge for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 5
```


### Customize unavailable nodes

Important

- You must set max surge to
`0`

in order to set a max unavailable value. The two values can't both be active at the same time. - Max unavailable doesn't create surge nodes during the upgrade process. Instead, AKS cordons
*n*nodes (the max unavailable value) at a time and evicts the pods to other nodes in the agent pool. This might cause workload disruptions if the pods can't be scheduled. - Max unavailable might cause more failures due to unsatisfied Pod Disruption Budgets (PDBs) since there are fewer resources for pods to be scheduled on. For more information, see
[Troubleshooting for Pod Disruption Budgets](/en-us/troubleshoot/azure/azure-kubernetes/create-upgrade-delete/error-code-poddrainfailure). - You can't set max unavailable on system node pools.

AKS can also configure upgrades to not use a surge node and upgrade the nodes in place. The max unavailable value determines how many nodes can be simultaneously cordoned and drained from the existing node pool nodes.

AKS accepts both integer values and a percentage value for max unavailable. For example:

| Value type | Example | Description |
|---|---|---|
| Integer | `5` |
Five nodes are cordoned from the existing nodes |
| Percentage | `50%` |
Half the current node count in the pool will be unavailable |

Max unavailable percent values can be a minimum of `1%`

and a maximum of `100%`

. A percent value is rounded up to the nearest node count.

#### Set max unavailable value

Set max unavailable values for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add),

[, or the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade)

`az aks nodepool upgrade`

`--max-unavailable`

parameter. For example:```
# Set max unavailable for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 0 \
--max-unavailable 5
# Update max unavailable for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 0 \
--max-unavailable 5
# Set max unavailable at upgrade time
az aks nodepool upgrade \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 0 \
--max-unavailable 5
```


### Customize node drain timeout

You might have long-running workloads on certain pods that you can't reschedule to another node during runtime. For example, a memory-intensive stateful workload that must finish running. In these cases, you can configure a node drain timeout that AKS respects in the upgrade workflow.

The default node drain timeout value is 30 minutes. Node drain timeout values can be a minimum of 5 minutes and a maximum of 24 hours.

If the drain timeout value elapses and pods are still running, the upgrade operation stops. Any subsequent `PUT`

operation resumes the stopped upgrade.

Tip

For long-running pods, you should also configure the [ terminationGracePeriodSeconds](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) in your pod spec.

#### Set node drain timeout value

Set node drain timeout (in minutes) for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) or

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

`--drain-time-out`

parameter.```
# Set drain timeout for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--drain-time-out 100
# Update drain timeout for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--drain-time-out 45
```


### Customize node soak time

To enable a waiting period for a specified duration of time between draining a node and proceeding to reimage it and move on to the next node, you can set the soak time. This soak time gives you the opportunity to perform other tasks during the upgrade process, such as checking application health from a monitoring dashboard.

The default node soak time is 0 minutes. Node soak time values can be a minimum of 0 minutes and a maximum of 30 minutes. We recommend keeping soak time as short as reasonably possible. A higher node soak time increases the total upgrade duration and delays discovery of issues.

#### Set node soak time value

Set node soak time (in minutes) for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add),

[, or](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade)

`az aks nodepool upgrade`

`--node-soak-duration`

flag.```
# Set node soak time for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--node-soak-duration 10
# Update node soak time for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 33% \
--node-soak-duration 5
# Set node soak time when upgrading an existing node pool
az aks nodepool upgrade \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 33% \
--node-soak-duration 20
```


## View AKS node upgrade events

View upgrade events using the `kubectl get events`

command to monitor the rolling upgrade progress.

```
kubectl get events --field-selector reason=Drain,reason=Surge,reason=Upgrade
```


Example output during an upgrade event:

```
default 2m1s Normal Drain node/aks-nodepool1-12345678-vmss000001 Draining node: [aks-nodepool1-12345678-vmss000001]
default 9m22s Normal Surge node/aks-nodepool1-12345678-vmss000002 Created a surge node [aks-nodepool1-12345678-vmss000002 nodepool1] for agentpool nodepool1
default 1m45s Normal Upgrade node/aks-nodepool1-12345678-vmss000001 Soak duration 5m0s after draining node: aks-nodepool1-12345678-vmss000001
```


## Recommended AKS node pool upgrade settings for production workloads

The following table outlines recommended node pool upgrade settings for production workloads:

| Setting | Recommendation |
|---|---|
Max surge |
Set to 33% for production node pools |
Drain timeout |
Configure based on your longest-running pod's requirements |
Soak time |
Use a short duration (0-5 minutes) unless you need manual verification |
Pod Disruption Budgets |
Configure PDBs for critical workloads to control pod eviction |
Upgrade order |
Upgrade non-production node pools first to validate the new version |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-upgrade-image -->

# Node image updates for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of node image updates for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS), including how it works, recommended maintenance windows, and examples to get started.

## How do node image updates work for node auto-provisioning nodes?

By default, NAP node pool virtual machines (VMs) are automatically updated when a new image version is available. You can configure an [AKS-managed node operating system (OS) upgrade schedule maintenance window](#node-os-upgrade-maintenance-windows-for-nap) to control when new images are picked up and applied to your NAP nodes, or [use Karpenter Node Disruption Budgets and Pod Disruption Budgets](#karpenter-node-disruption-budgets-and-pod-disruption-budgets-for-nap) to control how and when disruption occurs during upgrades.

Note

NAP forces the latest image version to be picked up if the existing node image version is older than 90 days. This bypasses any existing maintenance window.

## Node OS upgrade maintenance windows for NAP

You can use the [AKS planned maintenance feature](planned-maintenance) with a [node OS auto-upgrade channel](auto-upgrade-node-os-image) to configure a `aksManagedNodeOSUpgradeSchedule`

maintenance window that controls when to perform node OS security patching scheduled by your designated node OS auto-upgrade channel.

### Node OS upgrade maintenance window behavior and considerations

Keep the following information in mind when configuring a node OS upgrade maintenance window for NAP:

- The
`aksManagedNodeOSUpgradeSchedule`

maintenance configuration determines the window during which NAP picks up a new image. This configuration doesn't necessarily determine when existing nodes are disrupted. - The upgrade mechanism and decision criteria are specific to NAP/Karpenter and are evaluated by NAP's drift logic. NAP respects Karpenter Node Disruption Budgets and Pod Disruption Budgets. For more information about drift, see the
[Karpenter drift documentation](https://karpenter.sh/docs/concepts/disruption/#drift). - These NAP upgrade decisions are separate from the cluster
`NodeImage`

and`SecurityPatch`

channels. However, the`aksManagedNodeOSUpgradeSchedule`

maintenance configuration applies them as well. - We recommend using a maintenance window of four hours or more for reliable operation.
- If no maintenance configuration exists, AKS might use a fallback schedule to pick up new images, which can cause images to be picked up at unexpected times. You can avoid unexpected timing of new images and upgrades by defining an explicit
`aksManagedNodeOSUpgradeSchedule`

. - Allow at least 30 minutes between creating or updating a maintenance configuration and the scheduled start time to ensure AKS has time to reconcile the new configuration.

### Recommended schedule pattern for NAP-managed nodes

We recommend the following schedule pattern for NAP-managed nodes:

**Weekly cadence**: Recommended for routine node image roll outs (for example:*Every week on Sunday*).

## Create a node OS maintenance schedule example

The following sections show you how to create a weekly maintenance window for NAP-managed nodes using the Azure CLI and a JSON configuration file and how to update, view, list, and delete the maintenance configuration.

### Create a maintenance configuration

Create a JSON file named

`nodeosMaintenance.json`

with a weekly maintenance window (for example:*Sunday at 01:00 UTC for 4 hours*).`{ "properties": { "maintenanceWindow": { "durationHours": 4, "schedule": { "weekly": { "intervalWeeks": 1, "dayOfWeek": "Sunday" } }, "startDate": "2025-01-01", "startTime": "01:00", "utcOffset": "+00:00" } } }`

Add the maintenance configuration to your cluster using the

command.`az aks maintenanceconfiguration add`

`az aks maintenanceconfiguration add \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule \ --config-file ./nodeosMaintenance.json`


### Update, view, list, or delete a maintenance configuration

You can use the following commands to update, view, list, or delete a maintenance configuration for NAP-managed nodes:

Update a maintenance configuration by modifying the JSON file and then running the

command.`az aks maintenanceconfiguration update`

`az aks maintenanceconfiguration update \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule \ --config-file ./nodeosMaintenance.json`

View the details of a maintenance configuration using the

command.`az aks maintenanceconfiguration show`

`az aks maintenanceconfiguration show \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule`

List all maintenance configurations for your cluster using the

command.`az aks maintenanceconfiguration list`

`az aks maintenanceconfiguration list \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME`

Delete a maintenance configuration using the

command.`az aks maintenanceconfiguration delete`

`az aks maintenanceconfiguration delete \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule`


For complete details, examples, and advanced scenarios, see [Use Planned Maintenance to schedule maintenance windows for your AKS cluster](planned-maintenance).

## Karpenter Node Disruption Budgets and Pod Disruption Budgets for NAP

For more information on configuring Karpenter Node Disruption Budgets and Pod Disruption Budgets for NAP, see the following resources from the official Karpenter documentation:

## Next steps

For more information on node auto-provisioning in AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/generation-2-vm -->

# Use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS), including how to check available Gen 2 VM sizes, create AKS node pools with Gen 2 VMs, migrate from Gen 1 to Gen 2 VMs on AKS, and verify the VM generation of your AKS nodes.

## Before you begin

- Review the
[Virtual machine (VM) sizes, generations, and features for Azure Kubernetes Service (AKS)](aks-virtual-machine-sizes)article to understand VM generations and features supported on AKS.

## Check available Gen 2 VM sizes

Check available Gen 2 VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm#az-vm-list-skus) command.

```
# Set environment variables
export LOCATION=<your-region>
export VM_SIZE=<vm-size-to-check>
# Check if the VM size is available in the specified location
az vm list-skus --location $LOCATION --size $VM_SIZE --output table
```


For a breakdown of what VM sizes support Gen 2, see [Support for Gen 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2).

## Create a node pool with a Gen 2 VM

By default, Linux uses the Gen 2 node image unless the VM size doesn't support Gen 2.

Create a Linux node pool with a Gen 2 VM using the default [node pool creation](create-node-pools) process.

## Migrate an existing node pool to Gen 2

If you're using a VM size that only supports Gen 1, you can update your node pool to a VM size that supports Gen 2 using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. This update changes your node image from Gen 1 to Gen 2.

```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
export VM_SIZE=<supported-generation-2-vm-size>
# Update a Linux node pool to use a Gen 2 VM
az aks nodepool update --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --node-vm-size $VM_SIZE --os-type Linux
```


## Check if you're using a Gen 2 node image

Verify a successful node pool creation using the [ az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command and check that the

`nodeImageVersion`

contains `gen2`

in the output.```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
# Show node pool details
az aks nodepool show --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --output table
```


## Next steps

- To learn more about Gen 2 VMs, see
[Support for Generation 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2) - To learn more about supported Gen 2 node images, see
[Node images](node-images)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/generation-2-vms -->

# Use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS), including how to check available Gen 2 VM sizes, create AKS node pools with Gen 2 VMs, migrate from Gen 1 to Gen 2 VMs on AKS, and verify the VM generation of your AKS nodes.

## Before you begin

- Review the
[Virtual machine (VM) sizes, generations, and features for Azure Kubernetes Service (AKS)](aks-virtual-machine-sizes)article to understand VM generations and features supported on AKS.

## Check available Gen 2 VM sizes

Check available Gen 2 VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm#az-vm-list-skus) command.

```
# Set environment variables
export LOCATION=<your-region>
export VM_SIZE=<vm-size-to-check>
# Check if the VM size is available in the specified location
az vm list-skus --location $LOCATION --size $VM_SIZE --output table
```


For a breakdown of what VM sizes support Gen 2, see [Support for Gen 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2).

## Create a node pool with a Gen 2 VM

By default, Linux uses the Gen 2 node image unless the VM size doesn't support Gen 2.

Create a Linux node pool with a Gen 2 VM using the default [node pool creation](create-node-pools) process.

## Migrate an existing node pool to Gen 2

If you're using a VM size that only supports Gen 1, you can update your node pool to a VM size that supports Gen 2 using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. This update changes your node image from Gen 1 to Gen 2.

```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
export VM_SIZE=<supported-generation-2-vm-size>
# Update a Linux node pool to use a Gen 2 VM
az aks nodepool update --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --node-vm-size $VM_SIZE --os-type Linux
```


## Check if you're using a Gen 2 node image

Verify a successful node pool creation using the [ az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command and check that the

`nodeImageVersion`

contains `gen2`

in the output.```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
# Show node pool details
az aks nodepool show --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --output table
```


## Next steps

- To learn more about Gen 2 VMs, see
[Support for Generation 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2) - To learn more about supported Gen 2 node images, see
[Node images](node-images)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-node-image -->

# Autoupgrade node OS images

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS provides multiple autoupgrade channels dedicated to timely node-level OS security updates. This channel is different from cluster-level Kubernetes version upgrades and supersedes it.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Interactions between node OS autoupgrade and cluster autoupgrade

Node-level OS security updates are released at a faster rate than Kubernetes patch or minor version updates. The node OS autoupgrade channel grants you flexibility and enables a customized strategy for node-level OS security updates. Then, you can choose a separate plan for cluster-level Kubernetes version [autoupgrades](auto-upgrade-cluster).
It's best to use both cluster-level [autoupgrades](auto-upgrade-cluster) and the node OS autoupgrade channel together. Scheduling can be fine-tuned by applying two separate sets of [maintenance windows](planned-maintenance) - `aksManagedAutoUpgradeSchedule`

for the cluster [autoupgrade](auto-upgrade-cluster) channel and `aksManagedNodeOSUpgradeSchedule`

for the node OS autoupgrade channel.

## Channels for node OS image upgrades

The selected channel determines the timing of upgrades. When making changes to node OS auto-upgrade channels, allow up to 24 hours for the changes to take effect.

Note

- Node OS image auto-upgrade don't affect the cluster's Kubernetes version.
- Starting with API version 2023-06-01, the default for any new AKS cluster is
`NodeImage`

.

### Node OS channel changes that cause a reimage

The following node os channel transitions will trigger reimage on the nodes:

| From | To |
|---|---|
| Unmanaged | None |
| Unspecified | Unmanaged |
| SecurityPatch | Unmanaged |
| NodeImage | Unmanaged |
| None | Unmanaged |

### Available node OS upgrade channels

The following upgrade channels are available. You're allowed to choose one of these options:

| Channel | Description | OS-specific behavior |
|---|---|---|
`None` |
Your nodes don't have security updates applied automatically. This means you're solely responsible for your security updates. | N/A |
`Unmanaged` |
The OS built-in patching infrastructure automatically applies OS updates. Newly allocated machines are initially unpatched. The OS's infrastructure patches them at some point. | Ubuntu and Azure Linux (CPU node pools) apply security patches through unattended upgrade/dnf-automatic roughly once per day around 06:00 UTC. Windows doesn't automatically apply security patches, so this option behaves equivalently to `None` . You need to manage the reboot process using a tool like
`Unmanaged` . |
`SecurityPatch` |
OS security patches, which are AKS-tested, fully managed, and applied with safe deployment practices. AKS regularly updates the node's virtual hard disk (VHD) with patches from the image maintainer labeled "security only." There might be disruptions when the security patches are applied to the nodes. However AKS is limiting disruptions by only reimaging your nodes only when necessary, such as for certain kernel security packages. When the patches are applied, the VHD is updated and existing machines are upgraded to that VHD, honoring maintenance windows and surge settings. If AKS decides that reimaging nodes isn't necessary, it patches nodes live without draining pods and performs no VHD update. This option incurs the extra cost of hosting the VHDs in your node resource group. If you use this channel, Linux
|

`SecurityPatch`

works on kubernetes patch versions that are deprecated, so long as the minor Kubernetes version is still supported. [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks)and[Azure Linux with OS Guard on AKS](use-azure-linux-os-guard)do not support`SecurityPatch`

.`NodeImage`

[unattended upgrades](https://help.ubuntu.com/community/AutomaticSecurityUpdates)are disabled by default. Node image upgrades are supported as long as cluster Kubernetes minor version is still in support. Node images are AKS-tested, fully managed, and applied with safe deployment practices.## What to choose - SecurityPatch Channel or NodeImage Channel?

There are two important considerations for you to choose between `SecurityPatch`

or `NodeImage`

channels.

| Property | NodeImage Channel | SecurityPatch Channel | Recommended Channel |
|---|---|---|---|
`Speed of shipping` |
The typical build, test, release, and rollout timelines for a new VHD can take approximately two weeks following safe deployment practices. Although in the event of CVEs, accelerated rollouts can occur on a case by case basis. The exact timing when a new VHD hits a region can be monitored via
|

`NodeImage`

, even with safe deployment practices. SecurityPatch has the advantage of 'Live-patching' in Linux environments, where patching leads to selective 'reimaging' and doesn't reimage every time a patch gets applied. Re-image if it happens is controlled by maintenance windows.`SecurityPatch`

`Bugfixes`

`NodeImage`

## Set the node OS autoupgrade channel on a new cluster

- Set the node OS autoupgrade channel on a new cluster using the
command with the`az aks create`

`--node-os-upgrade-channel`

parameter. The following example sets the node OS autoupgrade channel to`SecurityPatch`

.

```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="myResourceGroup$RANDOM_SUFFIX"
export AKS_CLUSTER="myAKSCluster$RANDOM_SUFFIX"
az aks create \
--resource-group $RESOURCE_GROUP \
--name $AKS_CLUSTER \
--node-os-upgrade-channel SecurityPatch \
--generate-ssh-keys
```


## Set the node OS autoupgrade channel on an existing cluster

- Set the node os autoupgrade channel on an existing cluster using the
command with the`az aks update`

`--node-os-upgrade-channel`

parameter. The following example sets the node OS autoupgrade channel to`SecurityPatch`

.

```
az aks update --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER --node-os-upgrade-channel SecurityPatch
```


Results:

```
{
"autoUpgradeProfile": {
"nodeOsUpgradeChannel": "SecurityPatch"
}
}
```


## Update ownership and schedule

The default cadence means there's no planned maintenance window applied.

| Channel | Updates Ownership | Default cadence |
|---|---|---|
`Unmanaged` |
OS driven security updates. AKS has no control over these updates. | Nightly around 6AM UTC for Ubuntu and Azure Linux. Monthly for Windows. |
`SecurityPatch` |
AKS-tested, fully managed, and applied with safe deployment practices. For more information, see
|

`NodeImage`

[AKS Node Images in Release tracker](release-tracker)Note

While Windows security updates are released on a monthly basis, using the `Unmanaged`

channel won't automatically apply these updates to Windows nodes. If you choose the `Unmanaged`

channel, you need to manage the reboot process for Windows nodes.

## Node channel known limitations

Currently, when you set the

[cluster autoupgrade channel](auto-upgrade-cluster)to`node-image`

, it also automatically sets the node OS autoupgrade channel to`NodeImage`

. You can't change node OS autoupgrade channel value if your cluster autoupgrade channel is`node-image`

. In order to set the node OS autoupgrade channel value, check the[cluster autoupgrade channel](auto-upgrade-cluster)value isn't`node-image`

.The

`SecurityPatch`

channel isn't supported on Windows OS node pools.

Note

Use CLI version 2.61.0 or above for the `SecurityPatch`

channel.

## Node OS planned maintenance windows

Planned maintenance for the node OS autoupgrade starts at your specified maintenance window.

Note

To ensure proper functionality, use a maintenance window of four hours or more.

For more information on Planned Maintenance, see [Use Planned Maintenance to schedule maintenance windows for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Node OS autoupgrades FAQ

### How can I check the current nodeOsUpgradeChannel value on a cluster?

Run the `az aks show`

command and check the "autoUpgradeProfile" to determine what value the `nodeOsUpgradeChannel`

is set to:

```
az aks show --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER --query "autoUpgradeProfile"
```


Results:

```
{
"nodeOsUpgradeChannel": "SecurityPatch"
}
```


### How can I monitor the status of node OS autoupgrades?

To view the status of your node OS auto upgrades, look up [activity logs](monitor-aks-reference) on your cluster. You can also look up specific upgrade-related events as mentioned in [Upgrade an AKS cluster](upgrade-cluster). AKS also emits upgrade-related Event Grid events. To learn more, see [AKS as an Event Grid source](quickstart-event-grid).

### Can I change the node OS autoupgrade channel value if my cluster autoupgrade channel is set to `node-image`

?

No. Currently, when you set the [cluster autoupgrade channel](auto-upgrade-cluster) to `node-image`

, it also automatically sets the node OS autoupgrade channel to `NodeImage`

. You can't change the node OS autoupgrade channel value if your cluster autoupgrade channel is `node-image`

. In order to be able to change the node OS autoupgrade channel values, make sure the [cluster autoupgrade channel](auto-upgrade-cluster) isn't `node-image`

.

### Why is `SecurityPatch`

recommended over `Unmanaged`

channel?

On the `Unmanaged`

channel, AKS has no control over how and when the security updates are delivered. With `SecurityPatch`

, the security updates are fully tested and follow safe deployment practices. `SecurityPatch`

also honors maintenance windows. For more information, see [Increased security and resiliency of Canonical workloads on Azure](https://techcommunity.microsoft.com/t5/linux-and-open-source-blog/increased-security-and-resiliency-of-canonical-workloads-on/ba-p/3970623).

### Does `SecurityPatch`

always lead to a reimage of my nodes?

AKS limits reimages to only when necessary, such as certain kernel packages that may require a reimage to get fully applied. `SecurityPatch`

is designed to minimize disruptions as much as possible. If AKS decides reimaging nodes isn't necessary, it patches nodes live without draining pods and no VHD update is performed in such cases.

### Why does `SecurityPatch`

channel requires to reach `snapshot.ubuntu.com`

endpoint?

With the `SecurityPatch`

channel, the Linux cluster nodes have to download the required security patches and updates from ubuntu snapshot service described in [ubuntu-snapshots-on-azure-ensuring-predictability-and-consistency-in-cloud-deployments](https://ubuntu.com/blog/ubuntu-snapshots-on-azure-ensuring-predictability-and-consistency-in-cloud-deployments).

### How do I know if a `SecurityPatch`

or `NodeImage`

upgrade is applied on my node?

Run the `kubectl get nodes --show-labels`

command to list the nodes in your cluster and their labels.

Among the returned labels, you should see a line similar to the following output:

```
kubernetes.azure.com/node-image-version=AKSUbuntu-2204gen2containerd-202410.27.0-2024.12.01
```


Here, the base node image version is `AKSUbuntu-2204gen2containerd-202410.27.0`

. If applicable, the security patch version typically follows. In the above example, it's `2024.12.01`

.

The same details also be looked up in the Azure portal under the node label view:

## Next steps

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-node-os-image -->

# Autoupgrade node OS images

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS provides multiple autoupgrade channels dedicated to timely node-level OS security updates. This channel is different from cluster-level Kubernetes version upgrades and supersedes it.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Interactions between node OS autoupgrade and cluster autoupgrade

Node-level OS security updates are released at a faster rate than Kubernetes patch or minor version updates. The node OS autoupgrade channel grants you flexibility and enables a customized strategy for node-level OS security updates. Then, you can choose a separate plan for cluster-level Kubernetes version [autoupgrades](auto-upgrade-cluster).
It's best to use both cluster-level [autoupgrades](auto-upgrade-cluster) and the node OS autoupgrade channel together. Scheduling can be fine-tuned by applying two separate sets of [maintenance windows](planned-maintenance) - `aksManagedAutoUpgradeSchedule`

for the cluster [autoupgrade](auto-upgrade-cluster) channel and `aksManagedNodeOSUpgradeSchedule`

for the node OS autoupgrade channel.

## Channels for node OS image upgrades

The selected channel determines the timing of upgrades. When making changes to node OS auto-upgrade channels, allow up to 24 hours for the changes to take effect.

Note

- Node OS image auto-upgrade don't affect the cluster's Kubernetes version.
- Starting with API version 2023-06-01, the default for any new AKS cluster is
`NodeImage`

.

### Node OS channel changes that cause a reimage

The following node os channel transitions will trigger reimage on the nodes:

| From | To |
|---|---|
| Unmanaged | None |
| Unspecified | Unmanaged |
| SecurityPatch | Unmanaged |
| NodeImage | Unmanaged |
| None | Unmanaged |

### Available node OS upgrade channels

The following upgrade channels are available. You're allowed to choose one of these options:

| Channel | Description | OS-specific behavior |
|---|---|---|
`None` |
Your nodes don't have security updates applied automatically. This means you're solely responsible for your security updates. | N/A |
`Unmanaged` |
The OS built-in patching infrastructure automatically applies OS updates. Newly allocated machines are initially unpatched. The OS's infrastructure patches them at some point. | Ubuntu and Azure Linux (CPU node pools) apply security patches through unattended upgrade/dnf-automatic roughly once per day around 06:00 UTC. Windows doesn't automatically apply security patches, so this option behaves equivalently to `None` . You need to manage the reboot process using a tool like
`Unmanaged` . |
`SecurityPatch` |
OS security patches, which are AKS-tested, fully managed, and applied with safe deployment practices. AKS regularly updates the node's virtual hard disk (VHD) with patches from the image maintainer labeled "security only." There might be disruptions when the security patches are applied to the nodes. However AKS is limiting disruptions by only reimaging your nodes only when necessary, such as for certain kernel security packages. When the patches are applied, the VHD is updated and existing machines are upgraded to that VHD, honoring maintenance windows and surge settings. If AKS decides that reimaging nodes isn't necessary, it patches nodes live without draining pods and performs no VHD update. This option incurs the extra cost of hosting the VHDs in your node resource group. If you use this channel, Linux
|

`SecurityPatch`

works on kubernetes patch versions that are deprecated, so long as the minor Kubernetes version is still supported. [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks)and[Azure Linux with OS Guard on AKS](use-azure-linux-os-guard)do not support`SecurityPatch`

.`NodeImage`

[unattended upgrades](https://help.ubuntu.com/community/AutomaticSecurityUpdates)are disabled by default. Node image upgrades are supported as long as cluster Kubernetes minor version is still in support. Node images are AKS-tested, fully managed, and applied with safe deployment practices.## What to choose - SecurityPatch Channel or NodeImage Channel?

There are two important considerations for you to choose between `SecurityPatch`

or `NodeImage`

channels.

| Property | NodeImage Channel | SecurityPatch Channel | Recommended Channel |
|---|---|---|---|
`Speed of shipping` |
The typical build, test, release, and rollout timelines for a new VHD can take approximately two weeks following safe deployment practices. Although in the event of CVEs, accelerated rollouts can occur on a case by case basis. The exact timing when a new VHD hits a region can be monitored via
|

`NodeImage`

, even with safe deployment practices. SecurityPatch has the advantage of 'Live-patching' in Linux environments, where patching leads to selective 'reimaging' and doesn't reimage every time a patch gets applied. Re-image if it happens is controlled by maintenance windows.`SecurityPatch`

`Bugfixes`

`NodeImage`

## Set the node OS autoupgrade channel on a new cluster

- Set the node OS autoupgrade channel on a new cluster using the
command with the`az aks create`

`--node-os-upgrade-channel`

parameter. The following example sets the node OS autoupgrade channel to`SecurityPatch`

.

```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="myResourceGroup$RANDOM_SUFFIX"
export AKS_CLUSTER="myAKSCluster$RANDOM_SUFFIX"
az aks create \
--resource-group $RESOURCE_GROUP \
--name $AKS_CLUSTER \
--node-os-upgrade-channel SecurityPatch \
--generate-ssh-keys
```


## Set the node OS autoupgrade channel on an existing cluster

- Set the node os autoupgrade channel on an existing cluster using the
command with the`az aks update`

`--node-os-upgrade-channel`

parameter. The following example sets the node OS autoupgrade channel to`SecurityPatch`

.

```
az aks update --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER --node-os-upgrade-channel SecurityPatch
```


Results:

```
{
"autoUpgradeProfile": {
"nodeOsUpgradeChannel": "SecurityPatch"
}
}
```


## Update ownership and schedule

The default cadence means there's no planned maintenance window applied.

| Channel | Updates Ownership | Default cadence |
|---|---|---|
`Unmanaged` |
OS driven security updates. AKS has no control over these updates. | Nightly around 6AM UTC for Ubuntu and Azure Linux. Monthly for Windows. |
`SecurityPatch` |
AKS-tested, fully managed, and applied with safe deployment practices. For more information, see
|

`NodeImage`

[AKS Node Images in Release tracker](release-tracker)Note

While Windows security updates are released on a monthly basis, using the `Unmanaged`

channel won't automatically apply these updates to Windows nodes. If you choose the `Unmanaged`

channel, you need to manage the reboot process for Windows nodes.

## Node channel known limitations

Currently, when you set the

[cluster autoupgrade channel](auto-upgrade-cluster)to`node-image`

, it also automatically sets the node OS autoupgrade channel to`NodeImage`

. You can't change node OS autoupgrade channel value if your cluster autoupgrade channel is`node-image`

. In order to set the node OS autoupgrade channel value, check the[cluster autoupgrade channel](auto-upgrade-cluster)value isn't`node-image`

.The

`SecurityPatch`

channel isn't supported on Windows OS node pools.

Note

Use CLI version 2.61.0 or above for the `SecurityPatch`

channel.

## Node OS planned maintenance windows

Planned maintenance for the node OS autoupgrade starts at your specified maintenance window.

Note

To ensure proper functionality, use a maintenance window of four hours or more.

For more information on Planned Maintenance, see [Use Planned Maintenance to schedule maintenance windows for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Node OS autoupgrades FAQ

### How can I check the current nodeOsUpgradeChannel value on a cluster?

Run the `az aks show`

command and check the "autoUpgradeProfile" to determine what value the `nodeOsUpgradeChannel`

is set to:

```
az aks show --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER --query "autoUpgradeProfile"
```


Results:

```
{
"nodeOsUpgradeChannel": "SecurityPatch"
}
```


### How can I monitor the status of node OS autoupgrades?

To view the status of your node OS auto upgrades, look up [activity logs](monitor-aks-reference) on your cluster. You can also look up specific upgrade-related events as mentioned in [Upgrade an AKS cluster](upgrade-cluster). AKS also emits upgrade-related Event Grid events. To learn more, see [AKS as an Event Grid source](quickstart-event-grid).

### Can I change the node OS autoupgrade channel value if my cluster autoupgrade channel is set to `node-image`

?

No. Currently, when you set the [cluster autoupgrade channel](auto-upgrade-cluster) to `node-image`

, it also automatically sets the node OS autoupgrade channel to `NodeImage`

. You can't change the node OS autoupgrade channel value if your cluster autoupgrade channel is `node-image`

. In order to be able to change the node OS autoupgrade channel values, make sure the [cluster autoupgrade channel](auto-upgrade-cluster) isn't `node-image`

.

### Why is `SecurityPatch`

recommended over `Unmanaged`

channel?

On the `Unmanaged`

channel, AKS has no control over how and when the security updates are delivered. With `SecurityPatch`

, the security updates are fully tested and follow safe deployment practices. `SecurityPatch`

also honors maintenance windows. For more information, see [Increased security and resiliency of Canonical workloads on Azure](https://techcommunity.microsoft.com/t5/linux-and-open-source-blog/increased-security-and-resiliency-of-canonical-workloads-on/ba-p/3970623).

### Does `SecurityPatch`

always lead to a reimage of my nodes?

AKS limits reimages to only when necessary, such as certain kernel packages that may require a reimage to get fully applied. `SecurityPatch`

is designed to minimize disruptions as much as possible. If AKS decides reimaging nodes isn't necessary, it patches nodes live without draining pods and no VHD update is performed in such cases.

### Why does `SecurityPatch`

channel requires to reach `snapshot.ubuntu.com`

endpoint?

With the `SecurityPatch`

channel, the Linux cluster nodes have to download the required security patches and updates from ubuntu snapshot service described in [ubuntu-snapshots-on-azure-ensuring-predictability-and-consistency-in-cloud-deployments](https://ubuntu.com/blog/ubuntu-snapshots-on-azure-ensuring-predictability-and-consistency-in-cloud-deployments).

### How do I know if a `SecurityPatch`

or `NodeImage`

upgrade is applied on my node?

Run the `kubectl get nodes --show-labels`

command to list the nodes in your cluster and their labels.

Among the returned labels, you should see a line similar to the following output:

```
kubernetes.azure.com/node-image-version=AKSUbuntu-2204gen2containerd-202410.27.0-2024.12.01
```


Here, the base node image version is `AKSUbuntu-2204gen2containerd-202410.27.0`

. If applicable, the security patch version typically follows. In the above example, it's `2024.12.01`

.

The same details also be looked up in the Azure portal under the node label view:

## Next steps

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-repair -->

# Azure Kubernetes Service (AKS) node auto-repair

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) continuously monitors the health state of worker nodes and performs automatic node repair if they become unhealthy. The Azure virtual machine (VM) platform [performs maintenance on VMs](/en-us/azure/virtual-machines/maintenance-and-updates) experiencing issues. AKS and Azure VMs work together to minimize service disruptions for clusters.

In this article, you learn how the automatic node repair functionality behaves for Windows and Linux nodes.

## How AKS checks for NotReady nodes

AKS uses the following rules to determine if a node is unhealthy and needs repair:

- The node reports the
status on consecutive checks within a 10-minute time frame.**NotReady** - The node doesn't report any status within 10 minutes.

You can manually check the health state of your nodes with the `kubectl get nodes`

command.

## How automatic repair works

Note

AKS initiates repair operations with the user account **aks-remediator**.

If AKS identifies an unhealthy node that remains unhealthy for at least *five* minutes, AKS performs the following actions:

- AKS reboots the node.
- If the node remains unhealthy after reboot, AKS reimages the node.
- If the node remains unhealthy after reimage and it's a Linux node, AKS redeploys the node.

AKS retries the restart, reimage, and redeploy sequence up to three times if the node remains unhealthy. The overall auto repair process can take up to an hour to complete.

## Limitations

AKS node auto-repair is a best effort service and we don't guarantee that the node is restored back to healthy status. If your node persists in an unhealthy state, we highly encourage that you perform manual investigation of the node. Learn more about [troubleshooting node NotReady status](/en-us/troubleshoot/azure/azure-kubernetes/availability-performance/node-not-ready-basic-troubleshooting).

There are cases where AKS doesn't perform automatic repair. Failure to automatically repair the node can occur either by design or if Azure can't detect that an issue exists. Examples of when auto-repair isn't performed include:

- A node status isn't being reported due to error in network configuration.
- A node failed to initially register as a healthy node.
- If either of the following taints are present on the node:
`node.cloudprovider.kubernetes.io/shutdown`

,`ToBeDeletedByClusterAutoscaler`

. - A node is in the process of being upgraded, resulting in the following annotation on the node
`"cluster-autoscaler.kubernetes.io/scale-down-disabled": "true"`

and`"kubernetes.azure.com/azure-cluster-autoscaler-scale-down-disabled-reason": "upgrade"`


## Monitor node auto-repair using Kubernetes events

When AKS performs node auto-repair on your cluster, AKS emits Kubernetes events from the aks-auto-repair source for visibility. The following events appear on a node object when auto-repair happens.

To learn more about accessing, storing, and configuring alerts on Kubernetes events, see [Use Kubernetes events for troubleshooting in Azure Kubernetes Service](events).

| Reason | Event Message | Description |
|---|---|---|
| NodeRebootStart | Node auto-repair is initiating a reboot action due to NotReady status persisting for more than 5 minutes. | This event is emitted to notify you when reboot is about to be performed on your node. This action is the first in the overall node auto-repair sequence. |
| NodeRebootEnd | Reboot action from node auto-repair is completed. | Emitted once reboot is complete on the node. This event doesn't indicate the health status (healthy or unhealthy) of the node after the reboot is performed. |
| NodeReimageStart | Node auto-repair is initiating a reimage action due to NotReady status persisting for more than 5 minutes. | This event is emitted to notify you when reimage is about to be performed on your node. |
| NodeReimageEnd | Reimage action from node auto-repair is completed. | Emitted once reimage is complete on the node. This event doesn't indicate the health status (healthy or unhealthy) of the node after the reimage is performed. |
| NodeRedeployStart | Node auto-repair is initiating a redeploy action due to NotReady status persisting more than 5 minutes. | This event is emitted to notify you when redeploy is about to be performed on your node. Redeploy is the last action in the node auto-repair sequence. |
| NodeRedeployEnd | Redeploy action from node auto-repair is completed. | Emitted once redeploy is complete on the node. This event doesn't indicate the health status (healthy or unhealthy) of the node after redeploy is performed. |

If any errors occur during the node auto-repair process, the following events are emitted with the verbatim error message. Learn more about [troubleshooting common node auto-repair errors](/en-us/troubleshoot/azure/azure-kubernetes/availability-performance/node-auto-repair-errors).

Note

*Error code* in the following event messages varies depending on the error reported.

| Reason | Event Message | Description |
|---|---|---|
| NodeRebootError | Node auto-repair reboot action failed due to an operation failure. See error details here: Error code |
Emitted when there's an error with the reboot action. |
| NodeReimageError | Node auto-repair reimage action failed due to an operation failure. See error details here: Error code |
Emitted when there's an error with the reimage action. |
| NodeRedeployError | Node auto-repair redeploy action failed due to an operation failure. See error details here: Error code |
Emitted when there's an error with the redeploy action. |

## Next steps

By default, you can access Kubernetes events and logs on your AKS cluster from the past 1 hour. To store and query events and logs from the past 90 days, enable [Container Insights](/en-us/azure/azure-monitor/containers/container-insights-overview#access-container-insights) for deeper troubleshooting on your AKS cluster.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-image-upgrade -->

# Upgrade Azure Kubernetes Service (AKS) node images

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) regularly provides new node images, so it's beneficial to upgrade your node images frequently to use the latest AKS features. Linux node images are updated weekly, and Windows node images are updated monthly. Image upgrade announcements are included in the [AKS release notes](https://github.com/Azure/AKS/releases), and it can take up to a week for these updates to be rolled out across all regions. You can also perform node image upgrades automatically and schedule them using planned maintenance. For more information, see [Automatically upgrade node images](auto-upgrade-node-image).

This article shows you how to upgrade AKS cluster node images and how to update node pool images without upgrading the Kubernetes version. For information on upgrading the Kubernetes version for your cluster, see [Upgrade an AKS cluster](upgrade-aks-cluster).

Note

The AKS cluster must use virtual machine scale sets for the nodes.

It's not possible to downgrade a node image version (for example *AKSUbuntu-2204 to AKSUbuntu-1804*, or *AKSUbuntu-2204-202308.01.0 to AKSUbuntu-2204-202307.27.0*).

## Connect to your AKS cluster

Connect to your AKS cluster using the [

`az aks get-credentials`

][az-aks-get-credentials] command.`az aks get-credentials \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER`


## Check for available node image upgrades

Check for available node image upgrades using the

command.`az aks nodepool get-upgrades`

`az aks nodepool get-upgrades \ --nodepool-name $AKS_NODEPOOL \ --cluster-name $AKS_CLUSTER \ --resource-group $AKS_RESOURCE_GROUP`

In the output, find and make note of the

`latestNodeImageVersion`

value. This value is the latest node image version available for your node pool.Check your current node image version to compare with the latest version using the

command.`az aks nodepool show`

`az aks nodepool show \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL \ --query nodeImageVersion`

If the

`nodeImageVersion`

value is different from the`latestNodeImageVersion`

, you can upgrade your node image.

## Upgrade all node images in all node pools

Upgrade all node images in all node pools in your cluster using the

command with the`az aks upgrade`

`--node-image-only`

flag.`az aks upgrade \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER \ --node-image-only \ --yes`

You can check the status of the node images using the

`kubectl get nodes`

command.Note

This command might differ slightly depending on the shell you use. For more information on Windows and PowerShell environments, see the

[Kubernetes JSONPath documentation](https://kubernetes.io/docs/reference/kubectl/jsonpath/).`kubectl get nodes -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.metadata.labels.kubernetes\.azure\.com\/node-image-version}{"\n"}{end}'`

When the upgrade completes, use the

command to get the updated node pool details. The current node image is shown in the`az aks show`

`nodeImageVersion`

property.`az aks show \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER`


## Upgrade a specific node pool

Update the OS image of a node pool without doing a Kubernetes cluster upgrade using the

command with the`az aks nodepool upgrade`

`--node-image-only`

flag.`az aks nodepool upgrade \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL \ --node-image-only`

You can check the status of the node images with the

`kubectl get nodes`

command.Note

This command may differ slightly depending on the shell you use. For more information on Windows and PowerShell environments, see the

[Kubernetes JSONPath documentation](https://kubernetes.io/docs/reference/kubectl/jsonpath/).`kubectl get nodes -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.metadata.labels.kubernetes\.azure\.com\/node-image-version}{"\n"}{end}'`

When the upgrade completes, use the

command to get the updated node pool details. The current node image is shown in the`az aks nodepool show`

`nodeImageVersion`

property.`az aks nodepool show \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL`


## Upgrade node images with node surge

To speed up the node image upgrade process, you can upgrade your node images using a customizable node surge value. By default, AKS uses one extra node to configure upgrades.

Upgrade node images with node surge using the

command with the`az aks nodepool update`

`--max-surge`

flag to configure the number of nodes used for upgrades.Note

To learn more about the trade-offs of various

`--max-surge`

settings, see[Customize node surge upgrade](upgrade-aks-cluster#customize-node-surge-upgrade).`az aks nodepool update \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL \ --max-surge 33% \ --no-wait`

You can check the status of the node images with the

`kubectl get nodes`

command.`kubectl get nodes -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.metadata.labels.kubernetes\.azure\.com\/node-image-version}{"\n"}{end}'`

Get the updated node pool details using the

command. The current node image is shown in the`az aks nodepool show`

`nodeImageVersion`

property.`az aks nodepool show \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL`


## Next steps

- For information about the latest node images, see the
[AKS release notes](https://github.com/Azure/AKS/releases). - Learn how to upgrade the Kubernetes version with
[Upgrade an AKS cluster](upgrade-aks-cluster). [Automatically apply cluster and node pool upgrades with GitHub Actions](node-upgrade-github-actions).- Learn more about multiple node pools with
[Create multiple node pools](create-node-pools). - Learn about upgrading best practices with
[AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/secure-container-access -->

# Security container access to resources using built-in Linux security features

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to secure container access to resources for your Azure Kubernetes Service (AKS) workloads.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Overview

In the same way that you should grant users or groups the minimum privileges required, you should also limit containers to only necessary actions and processes. To minimize the risk of attack, avoid configuring applications and containers that require escalated privileges or root access.

You can use built-in Kubernetes *pod security contexts* to define more permissions, such as the user or group to run as, the Linux capabilities to expose, or setting `allowPrivilegeEscalation: false`

in the pod manifest. For more best practices, see [Secure pod access to resources](https://kubernetes.io/docs/concepts/security/pod-security-standards/).

To improve the host isolation and decrease lateral movement on Linux, you can use *user-namespaces*.

For even more granular control of container actions, you can use built-in Linux security features such as *AppArmor* and *seccomp*.

- Define Linux security features at the node level.
- Implement features through a pod manifest.

Built-in Linux security features are only available on Linux nodes and pods.

Note

Currently, Kubernetes environments aren't completely safe for hostile multitenant usage. Additional security features, like *Microsoft Defender for Containers*, *AppArmor*, *seccomp*, *user-namespaces*, *Pod Security Admission*, or *Kubernetes RBAC for nodes*, efficiently block exploits.

For true security when running hostile multitenant workloads, only trust a hypervisor. The security domain for Kubernetes becomes the entire cluster, not an individual node.

For these types of hostile multitenant workloads, you should use physically isolated clusters.

## User-namespaces

Linux pods run using several namespaces by default: a network namespaces to isolate the network identity and a PID namespace to isolate the processes. A [user-namespace](https://man7.org/linux/man-pages/man7/user_namespaces.7.html) isolates the users inside the container from the users on the host. It also limits the scope of capabilities and the pod's interactions with the rest of the system.

The UIDs and GIDs inside the container are mapped to unprivileged users on the host, so all interaction with the rest of the host happen as those unprivileged UID and GID. For example, root inside the container (UID 0) can be mapped to user 65536 on the host. Kubernetes creates the mapping to guarantee it doesn't overlap with other pods using user-namespaces on the system.

The Kubernetes implementation has some key benefits:

**Increased host isolation**: If a container escapes the pod boundaries, even if it runs as root inside the container, it has no privileges on the host. The reason is because the UIDs and GIDs of the container are mapped to unprivileged users on the host. If there's a container escape, user-namespaces greatly protects what files on the host a container can read/write, which process it can send signals to. Capabilities granted are only valid inside the user namespace and not on the host.**Prevention of lateral movement**: As the UIDs and GIDs for different containers are mapped to different, nonoverlapping UIDs and GIDs on the host, containers have a harder time attacking each other. For example, suppose container A runs with different UIDs and GIDs on the host than container B. In case of a container breakout, the operations it can do on container B's files and processes are limited: only read/write what a file allows to others. But not even that ends up being possible, as there's an extra prevention on the parent directory of the pod root volume to make sure only the pod GID can access it.**Honor Least-privilege principle**: As the UIDs and GIDs are mapped to unprivileged users on the host, only users that need the privilege on the host (and disable user namespaces) get it. Without user namespaces, there's no separation between container's users and host's users. We can't avoid giving privileges on the host to processes that don't need it, when they need privilege just inside the container.**Enablement of new use cases**: User namespaces allow containers to gain certain capabilities inside their own user namespace without affecting the host. The capabilities granted restricted to the pod unlocks new possibilities, such as running applications that require privileged operations without granting full root access on the host. Common new use-cases that can be implemented securely are: running nested containers and unprivileged container builds.**Unprivileged container setup**: Most of the container creation and setup doesn't run as root on the host, which significantly limits the impact of many CVEs.

None of these things are true when user-namespaces aren't used. If the container runs as root, when user-namespaces aren't used, the process is running as root on the host, the capabilities are valid on the host and the container setup is done as root on the host.

### Before you begin

Before you begin, make sure you have the following:

- An existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Minimum kubernetes version 1.33 for the control plane and worker nodes. If you're not using kubernetes version 1.33 or higher, you'll need to
[upgrade your kubernetes version](upgrade-aks-cluster). - Worker nodes running Azure Linux 3.0 or Ubuntu 24.04. If you're not using these OS versions, you will not have the minimum
[stack requirements](https://kubernetes.io/docs/concepts/workloads/pods/user-namespaces/#before-you-begin)to enable user-namespaces. You'll need to[upgrade your OS version](upgrade-os-version).

### Limitations

- User-namespaces is a linux kernel feature and is not supported for Windows node pools.
- Don't hesitate to check the
[Kubernetes documentation for user namespaces](https://kubernetes.io/docs/concepts/workloads/pods/user-namespaces/), in particular the limitations section.

### Enable user-namespaces

There are no configurations needed to use this feature. If using the required AKS version, everything works out of the box.

Create a file named

`mypod.yaml`

and copy in the following manifest:To use user-namespaces, the yaml needs to have the field

`hostUsers: false`

.`apiVersion: v1 kind: Pod metadata: name: userns spec: hostUsers: false containers: - name: shell command: ["sleep", "infinity"] image: debian`

Deploy the application using the

`kubectl apply`

command and specify the name of your YAML manifest.`kubectl apply -f mypod.yaml`

Check the status of the deployed pods using the

`kubectl get pods`

command.`kubectl get pods`

Exec into the pod to check

`/proc/self/uid_map`

by using the`kubectl exec`

command:`kubectl exec -ti userns -- bash # Now inside the pod run cat /proc/self/uid_map`


The output should have 65536 in the last column. For example:

```
0 833617920 65536
```


### CVEs mitigated

Here are some CVEs that are completely/partially mitigated with user-namespaces.

Bear in mind the list isn't exhaustive, it's just a selection of CVEs with high score that are mitigated:

[CVE-2019-5736](https://nvd.nist.gov/vuln/detail/CVE-2019-5736)- Score 8.6 (HIGH)[CVE 2024-21262](https://github.com/opencontainers/runc/security/advisories/GHSA-xr7r-f8xq-vfvv): Score 8.6 (HIGH)[CVE 2022-0492](https://unit42.paloaltonetworks.com/cve-2022-0492-cgroups/): Score 7.8 (HIGH)[CVE-2021-25741](https://nvd.nist.gov/vuln/detail/CVE-2021-25741): Score: 8.1 (HIGH) / 8.8 (HIGH)[CVE-2017-1002101](https://nvd.nist.gov/vuln/detail/CVE-2017-1002101): Score: 9.6 (CRITICAL) / 8.8(HIGH)

To learn more, read this [blog post](https://kubernetes.io/blog/2025/04/25/userns-enabled-by-default/) with additional information around user-namespaces.

## App Armor

To limit container actions, you can use the [AppArmor](https://kubernetes.io/docs/tutorials/clusters/apparmor/) Linux kernel security module. AppArmor is available as part of the underlying AKS node OS and is enabled by default. You create AppArmor profiles that restrict read, write, or execute actions, or system functions like mounting filesystems. Default AppArmor profiles restrict access to various `/proc`

and `/sys`

locations and provide a means to logically isolate containers from the underlying node. AppArmor works for any application that runs on Linux, not just Kubernetes pods.

Note

Azure Linux 3.0 does not offer AppArmor support. For Azure Linux 3.0 nodes, the recommendation is to leverage SELinux instead of AppArmor for mandatory access control.

To see AppArmor in action, the following example creates a profile that prevents writing to files.

[SSH](manage-ssh-node-access)to an AKS node.Create a file named

*deny-write.profile*.Copy and paste the following content:

`#include <tunables/global> profile k8s-apparmor-example-deny-write flags=(attach_disconnected) { #include <abstractions/base> file, # Deny all file writes. deny /** w, }`


AppArmor profiles are added using the `apparmor_parser`

command.

Add the profile to AppArmor.

Specify the name of the profile created in the previous step:

`sudo apparmor_parser deny-write.profile`

If the profile is correctly parsed and applied to AppArmor, you won't see any output and you'll return to the command prompt.

From your local machine, create a pod manifest named

*aks-apparmor.yaml*. This manifest:- Defines an annotation for
`container.apparmor.security.beta.kubernetes`

. - References the
*deny-write*profile created in the previous steps.

`apiVersion: v1 kind: Pod metadata: name: hello-apparmor annotations: container.apparmor.security.beta.kubernetes.io/hello: localhost/k8s-apparmor-example-deny-write spec: containers: - name: hello image: mcr.microsoft.com/dotnet/runtime-deps:6.0 command: [ "sh", "-c", "echo 'Hello AppArmor!' && sleep 1h" ]`

- Defines an annotation for
With the pod deployed, run the following command and verify the

*hello-apparmor*pod shows a*Running*status:`kubectl get pods NAME READY STATUS RESTARTS AGE aks-ssh 1/1 Running 0 4m2s hello-apparmor 0/1 Running 0 50s`


For more information about AppArmor, see [AppArmor profiles in Kubernetes](https://kubernetes.io/docs/tutorials/clusters/apparmor/).

## Secure computing (seccomp)

While AppArmor works for any Linux application, [seccomp ( secure computing)](https://kubernetes.io/docs/reference/node/seccomp/) works at the process level. Seccomp is also a Linux kernel security module and is natively supported by the

`containerd`

runtime used by AKS nodes. With seccomp, you can limit a container's system calls. Seccomp establishes an extra layer of protection against common system call vulnerabilities exploited by malicious actors and allows you to specify a default profile for all workloads in the node.### Configure a default seccomp profile (preview)

You can apply default seccomp profiles using [custom node configurations](/en-us/azure/aks/custom-node-configuration) when creating a new Linux node pool. There are two values supported on AKS: `RuntimeDefault`

and `Unconfined`

. Some workloads might require a lower number of syscall restrictions than others. This means that they can fail during runtime with the 'RuntimeDefault' profile. To mitigate such a failure, you can specify the `Unconfined`

profile. If your workload requires a custom profile, see [Configure a custom seccomp profile](#configure-a-custom-seccomp-profile).

#### Limitations

- SeccompDefault is not a supported parameter for windows node pools.
- SeccompDefault is available starting in 2024-09-02-preview API.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

#### Register the `KubeletDefaultSeccompProfilePreview`

feature flag

Register the

`KubeletDefaultSeccompProfilePreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "KubeletDefaultSeccompProfilePreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "KubeletDefaultSeccompProfilePreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


#### Restrict your container's system calls with seccomp

**1. Follow steps to apply a seccomp profile in your kubelet configuration by specifying "seccompDefault": "RuntimeDefault"**.


`RuntimeDefault`

uses containerd's default seccomp profile, restricting certain system calls to enhance security. Restricted syscalls will fail. For more information, see the [containerD default seccomp profile](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51).

**2. Check that the configuration was applied**.

You can confirm the settings are applied to the nodes by [connecting to the host](node-access) and verifying configuration changes have been made on the filesystem.

**3. Troubleshoot workload failures**.

When SeccompDefault is enabled, the container runtime default seccomp profile is used by default for all workloads scheduled on the node. This might cause workloads to fail due to blocked syscalls. If a workload failure has occurred, you might see errors such as:

- Workload is existing unexpectedly after the feature is enabled, with "permission denied" error.
- Seccomp error messages can also be seen in auditd or syslog by replacing SCMP_ACT_ERRNO with SCMP_ACT_LOG in the default profile.

If you experience the above errors, we recommend that you change your seccomp profile to `Unconfined`

. `Unconfined`

places no restrictions on syscalls, allowing all system calls, which reduces security.

### Configure a custom seccomp profile

With a custom seccomp profile, you can have more granular control over restricted syscalls. Align to the best practice of granting the container minimal permission only to run by:

- Defining with filters what actions to allow or deny.
- Annotating within a pod YAML manifest to associate with the seccomp filter.

To see seccomp in action, create a filter that prevents changing permissions on a file.

[SSH](manage-ssh-node-access)to an AKS node.Create a seccomp filter named

*/var/lib/kubelet/seccomp/prevent-chmod*.Copy and paste the following content:

`{ "defaultAction": "SCMP_ACT_ALLOW", "syscalls": [ { "name": "chmod", "action": "SCMP_ACT_ERRNO" }, { "name": "fchmodat", "action": "SCMP_ACT_ERRNO" }, { "name": "chmodat", "action": "SCMP_ACT_ERRNO" } ] }`

In version 1.19 and later, you need to configure:

`{ "defaultAction": "SCMP_ACT_ALLOW", "syscalls": [ { "names": ["chmod","fchmodat","chmodat"], "action": "SCMP_ACT_ERRNO" } ] }`

From your local machine, create a pod manifest named

*aks-seccomp.yaml*and paste the following content. This manifest:- Defines an annotation for
`seccomp.security.alpha.kubernetes.io`

. - References the
*prevent-chmod*filter created in the previous step.

`apiVersion: v1 kind: Pod metadata: name: chmod-prevented annotations: seccomp.security.alpha.kubernetes.io/pod: localhost/prevent-chmod spec: containers: - name: chmod image: mcr.microsoft.com/dotnet/runtime-deps:6.0 command: - "chmod" args: - "777" - /etc/hostname restartPolicy: Never`

In version 1.19 and later, you need to configure:

`apiVersion: v1 kind: Pod metadata: name: chmod-prevented spec: securityContext: seccompProfile: type: Localhost localhostProfile: prevent-chmod containers: - name: chmod image: mcr.microsoft.com/dotnet/runtime-deps:6.0 command: - "chmod" args: - "777" - /etc/hostname restartPolicy: Never`

- Defines an annotation for
Deploy the sample pod using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f ./aks-seccomp.yaml`

View pod status using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command.- The pod reports an error.
- The
`chmod`

command is prevented from running by the seccomp filter, as shown in the example output:

`kubectl get pods NAME READY STATUS RESTARTS AGE chmod-prevented 0/1 Error 0 7s`


For help troubleshooting your seccomp profile see the article [Troubleshoot seccomp profile configuration in Azure Kubernetes Service](/en-us/troubleshoot/azure/azure-kubernetes/security/troubleshoot-seccomp-profiles).

## Seccomp security profile options

Seccomp security profiles are a set of defined syscalls that are allowed or restricted. Most container runtimes have a default seccomp profile that is similar if not the same as the one Docker uses. For more information about available profiles, see [Docker](https://kubernetes.io/docs/reference/node/seccomp/) or [containerD](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51) default seccomp profiles.

AKS uses the [containerD](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51) default seccomp profile for our RuntimeDefault when you configure seccomp using [custom node configuration](/en-us/azure/aks/custom-node-configuration).

### Significant syscalls blocked by default profile

Both [Docker](https://kubernetes.io/docs/reference/node/seccomp/) and [containerD](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51) maintain allowlists of safe syscalls. This table lists the significant (but not all) syscalls that are effectively blocked because they aren't on the allowlist. If any of the blocked syscalls are required by your workload, don't use the `RuntimeDefault`

seccomp profile.

When changes are made to [Docker](https://kubernetes.io/docs/reference/node/seccomp/) and [containerD](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51), AKS updates their default configuration to match. Updates to this list may cause workload failure. For release updates, see [AKS release notes](https://github.com/Azure/AKS/releases).

| Blocked syscall | Description |
|---|---|
`acct` |
Accounting syscall which could let containers disable their own resource limits or process accounting. Also gated by `CAP_SYS_PACCT` . |
`add_key` |
Prevent containers from using the kernel keyring, which isn't namespaced. |
`bpf` |
Deny loading potentially persistent bpf programs into kernel, already gated by `CAP_SYS_ADMIN` . |
`clock_adjtime` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`clock_settime` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`clone` |
Deny cloning new namespaces. Also gated by `CAP_SYS_ADMIN for CLONE_*` flags, except `CLONE_NEWUSER` . |
`create_module` |
Deny manipulation and functions on kernel modules. Obsolete. Also gated by `CAP_SYS_MODULE` . |
`delete_module` |
Deny manipulation and functions on kernel modules. Also gated by `CAP_SYS_MODULE` . |
`finit_module` |
Deny manipulation and functions on kernel modules. Also gated by `CAP_SYS_MODULE` . |
`get_kernel_syms` |
Deny retrieval of exported kernel and module symbols. Obsolete. |
`get_mempolicy` |
Syscall that modifies kernel memory and NUMA settings. Already gated by `CAP_SYS_NICE` . |
`init_module` |
Deny manipulation and functions on kernel modules. Also gated by `CAP_SYS_MODULE` . |
`ioperm` |
Prevent containers from modifying kernel I/O privilege levels. Already gated by `CAP_SYS_RAWIO` . |
`iopl` |
Prevent containers from modifying kernel I/O privilege levels. Already gated by `CAP_SYS_RAWIO` . |
`kcmp` |
Restrict process inspection capabilities, already blocked by dropping `CAP_SYS_PTRACE` . |
`kexec_file_load` |
Sister syscall of kexec_load that does the same thing, slightly different arguments. Also gated by `CAP_SYS_BOOT` . |
`kexec_load` |
Deny loading a new kernel for later execution. Also gated by `CAP_SYS_BOOT` . |
`keyctl` |
Prevent containers from using the kernel keyring, which isn't namespaced. |
`lookup_dcookie` |
Tracing/profiling syscall, which could leak information on the host. Also gated by `CAP_SYS_ADMIN` . |
`mbind` |
Syscall that modifies kernel memory and NUMA settings. Already gated by `CAP_SYS_NICE` . |
`mount` |
Deny mounting, already gated by `CAP_SYS_ADMIN` . |
`move_pages` |
Syscall that modifies kernel memory and NUMA settings. |
`nfsservctl` |
Deny interaction with the kernel nfs daemon. Obsolete since Linux 3.1. |
`open_by_handle_at` |
Cause of an old container breakout. Also gated by `CAP_DAC_READ_SEARCH` . |
`perf_event_open` |
Tracing/profiling syscall, which could leak information on the host. |
`personality` |
Prevent container from enabling BSD emulation. Not inherently dangerous, but poorly tested, potential for kernel vulns. |
`pivot_root` |
Deny pivot_root, should be privileged operation. |
`process_vm_readv` |
Restrict process inspection capabilities, already blocked by dropping `CAP_SYS_PTRACE` . |
`process_vm_writev` |
Restrict process inspection capabilities, already blocked by dropping `CAP_SYS_PTRACE` . |
`ptrace` |
Tracing/profiling syscall. Blocked in Linux kernel versions before 4.8 to avoid seccomp bypass. Tracing/profiling arbitrary processes is already blocked by dropping CAP_SYS_PTRACE, because it could leak information on the host. |
`query_module` |
Deny manipulation and functions on kernel modules. Obsolete. |
`quotactl` |
Quota syscall which could let containers disable their own resource limits or process accounting. Also gated by `CAP_SYS_ADMIN` . |
`reboot` |
Don't let containers reboot the host. Also gated by `CAP_SYS_BOOT` . |
`request_key` |
Prevent containers from using the kernel keyring, which isn't namespaced. |
`set_mempolicy` |
Syscall that modifies kernel memory and NUMA settings. Already gated by `CAP_SYS_NICE` . |
`setns` |
Deny associating a thread with a namespace. Also gated by `CAP_SYS_ADMIN` . |
`settimeofday` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`stime` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`swapon` |
Deny start/stop swapping to file/device. Also gated by `CAP_SYS_ADMIN` . |
`swapoff` |
Deny start/stop swapping to file/device. Also gated by `CAP_SYS_ADMIN` . |
`sysfs` |
Obsolete syscall. |
`_sysctl` |
Obsolete, replaced by /proc/sys. |
`umount` |
Should be a privileged operation. Also gated by `CAP_SYS_ADMIN` . |
`umount2` |
Should be a privileged operation. Also gated by `CAP_SYS_ADMIN` . |
`unshare` |
Deny cloning new namespaces for processes. Also gated by `CAP_SYS_ADMIN` , with the exception of unshare --user. |
`uselib` |
Older syscall related to shared libraries, unused for a long time. |
`userfaultfd` |
Userspace page fault handling, largely needed for process migration. |
`ustat` |
Obsolete syscall. |
`vm86` |
In kernel x86 real mode virtual machine. Also gated by `CAP_SYS_ADMIN` . |
`vm86old` |
In kernel x86 real mode virtual machine. Also gated by `CAP_SYS_ADMIN` . |

## Next steps

For associated best practices, see [Best practices for cluster security and upgrades in AKS](operator-best-practices-cluster-security) and [Best practices for pod security in AKS](developer-best-practices-pod-security).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/faq -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/quotas-skus-regions -->

# Quotas, virtual machine size restrictions, and region availability in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure services set default limits and quotas for resources and features, including usage restrictions for certain virtual machine (VM) SKUs.

This article details the default resource limits for Azure Kubernetes Service (AKS) resources and the availability of AKS in Azure regions.

## Service quotas and limits

| Resource | Limit |
|---|---|
| Maximum number of clusters per subscription globally | 5,000 |
| Maximum nodes per cluster with Virtual Machine Scale Sets and
|

[node pools](/en-us/azure/aks/create-node-pools)Note: If you're unable to scale up to 5,000 nodes per cluster, see

[Best Practices for Large Clusters](/en-us/azure/aks/best-practices-performance-scale-large).[Kubenet](/en-us/azure/aks/concepts-network-legacy-cni#kubenet)networking plug-inAzure CLI default: 110

Azure Resource Manager template default: 110

Azure portal deployment default: 30

[Azure Container Networking Interface (Azure CNI)](/en-us/azure/aks/concepts-network-cni-overview)1Maximum recommended for Windows Server containers: 110

Default: 30

OSM controllers per cluster: 1

Pods per OSM controller: 1600

Kubernetes service accounts managed by OSM: 160

[Standard Load Balancer SKU](/en-us/azure/load-balancer/load-balancer-overview)1 Windows Server containers must use Azure CNI networking plug-in. Kubenet isn't supported for Windows Server containers.

| Kubernetes Control Plane tier | Limit |
|---|---|
| Standard tier | Automatically scales Kubernetes API server based on load. Larger control plane component limits and API server/etcd instances. |
| Free tier | Limited resources with
Not advised for production/critical workloads. |

### Quota limits on AKS Managed Clusters

Starting in September 2025, Azure Kubernetes Service will begin rolling out a change to enable quota for all current and new AKS customers. This rollout is expected to take place between September 1-30, 2025.

AKS quota will represent a limit of the maximum number of managed clusters (AKS clusters) that an Azure subscription can create per region. Once managed cluster quota is released, customers will need both quota for managed clusters and quota for their nodes (VM skus) in order to create an AKS cluster.

**Existing AKS customer subscriptions** will be given a default limit at or above their current usage depending on the available regional capacity. **Existing subscriptions using AKS for the first time and new subscriptions** will be given a default limit.

Customers can [view quota limits and usage](/en-us/azure/quotas/view-quotas) and [request additional quota](/en-us/azure/quotas/quickstart-increase-quota-portal) via the Azure portal Quotas page or via the [Quotas REST API](/en-us/rest/api/reserved-vm-instances/quotaapi). Prior to rollout completion, quota limits and usage *may* be visible in the Portal Quotas blade and customers will be able to request quota —however, the limits will not be enforced until rollout is complete.


lightbox="./media/quotas-skus-regions/portal-quotas-page-expanded.png"

When Managed Clusters Quota is rolled out, customers will receive the following error if they attempt to create a new cluster and are out of quota:

```
ManagedClusterCountExceedsQuotaLimit: Operation results in exceeding quota limits for managed clusters. Maximum allowed: %d, Current usage: %d, Additional requested: %d. Consider deleting unused clusters or requesting a quota increase. To request a quota increase, follow the instructions here: https://learn.microsoft.com/azure/quotas/quickstart-increase-quota-portal.
```


To remedy this, customers can [request additional quota in the Azure portal Quotas page](/en-us/azure/quotas/view-quotas) or via the [Quotas REST API](/en-us/rest/api/reserved-vm-instances/quotaapi).

#### AKS Managed Clusters Quota Limits

| Subscription Type | Default number of AKS clusters per subscription per region for new subscriptions1 |
Maximum number of AKS clusters per subscription per region via self service using
2 |
|---|

1 The default number of AKS clusters per subscription per region for new subscriptions may vary in regions with capacity constraints.

2 To request an increase of the quota limit, [use the Azure portal Quotas request process](/en-us/azure/quotas/quickstart-increase-quota-portal). Quota increase requests above the maximum self service amount will require a support ticket. Free Trial and Azure for Students subscriptions aren't eligible for limit or quota increases. If you have a Free Trial or Azure for Students subscription, you can upgrade to a pay-as-you-go subscription to get higher quota limits.

### Throttling limits on AKS resource provider APIs

AKS uses the [token bucket](https://en.wikipedia.org/wiki/Token_bucket) throttling algorithm to limit certain AKS [resource provider](/en-us/azure/azure-resource-manager/management/resource-providers-and-types) APIs. Throttling limits ensures the performance of the service and promotes fair usage of the service for all customers.

The buckets have a fixed size (also known as a burst rate) and refill over time at a fixed rate (also known as a sustained rate). Each throttling limit is in effect at the regional level for the specified resource in that region. For example, in the following table, a Subscription can call ListManagedClusters a maximum of 60 times (burst rate) at once for each ResourceGroup, but can continue to make 1 call every second thereafter (sustained rate).

| API request | Bucket size | Refill rate | Scope |
|---|---|---|---|
| LIST ManagedClusters | 500 requests | 1 requests / 1 second | Subscription |
| LIST ManagedClusters | 60 requests | 1 request / 1 second | ResourceGroup |
| PUT AgentPool | 20 requests | 1 request / 1 minute | AgentPool |
| PUT ManagedCluster | 20 requests | 1 request / 1 minute | ManagedCluster |
| GET ManagedCluster | 60 requests | 1 request / 1 second | Managed Cluster |
| GET Operation Status | 200 requests | 2 requests / 1 second | Subscription |
| All Other APIs | 60 requests | 1 request / 1 second | Subscription |

Note

The ManagedClusters and AgentPools buckets are counted separately for the same AKS cluster.

If a request is throttled, the request returns HTTP response code `429`

(Too Many Requests) and the error code shows as `Throttled`

in the response. Each throttled request includes a `Retry-After`

in the HTTP response header with the interval to wait before retrying, in seconds. Clients that use a bursty API call pattern should ensure that the Retry-After can be handled appropriately. To learn more about Retry-After, see the [following article](https://developer.mozilla.org/docs/Web/HTTP/Headers/Retry-After). Specifically, AKS uses `delay-seconds`

to specify the retry.

## Provisioned infrastructure

All other network, compute, and storage limitations apply to the provisioned infrastructure. For the relevant limits, see [Azure subscription and service limits](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits).

Important

When you upgrade an AKS cluster, extra resources are temporarily consumed. These resources include available IP addresses in a virtual network subnet or virtual machine vCPU quota.

For Windows Server containers, you can perform an upgrade operation to apply the latest node updates. If you don't have the available IP address space or vCPU quota to handle these temporary resources, the cluster upgrade process fails. For more information on the Windows Server node upgrade process, see [Upgrade a node pool in AKS](use-multiple-node-pools#upgrade-a-node-pool).

## Supported VM sizes

The list of supported VM sizes in AKS is evolving with the release of new VM SKUs in Azure. Follow the [AKS release notes](https://github.com/Azure/AKS/releases) to stay informed of new supported SKUs.

## Restricted VM sizes

Each node in an AKS cluster contains a fixed amount of compute resources such as vCPU and memory. Due to the required compute resources needed to run Kubernetes correctly, certain VM SKU sizes are restricted by default in AKS. These restrictions are to ensure that pods can be scheduled and function correctly on these nodes.

### User node pools

For user node pools, VM sizes with fewer than two vCPUs and two GBs of RAM (memory) might not be used.

### System node pools

For system node pools, VM sizes with fewer than two vCPUs and four GBs of RAM (memory) might not be used. To ensure that the required *kube-system* pods and your applications can reliably be scheduled, [B series VMs](/en-us/azure/virtual-machines/sizes-b-series-burstable) aren't supported for system node pools and [Av1 series VMs](/en-us/azure/virtual-machines/sizes/retirement/av1-series-retirement) aren't recommended.

For more information on VM types and their compute resources, see [Sizes for virtual machines in Azure](/en-us/azure/virtual-machines/sizes).

## Supported container image sizes

AKS doesn't set a limit on the container image size. However, it's important to understand that the larger the container image, the higher the memory demand. This demand could potentially exceed resource limits or the overall available memory of worker nodes. By default, memory for VM size Standard_DS2_v2 for an AKS cluster is set to 7 GiB.

When a container image is large (1 TiB or more), kubelet might not be able to pull it from your container registry to a node due to lack of disk space.

## Region availability

For the latest list of where you can deploy and run clusters, see [AKS region availability](https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service).

## Smart VM Defaults

As of May 2025, AKS automatically selects the optimal default VM SKU based on available capacity and quota if the parameter is unspecified during deployment. This default ensures that deployments are matched with the best possible SKU, enhancing performance and reliability while optimizing resource utilization. Previously, the default AKS VM SKU was Standard_DS2_V2, but there are now dynamic outcomes in default provisioning based on SKU availability that affects all new VM create operations.

## Cluster configuration presets in the Azure portal

When you create a cluster using the Azure portal, you can choose a preset configuration to quickly customize based on your scenario. You can modify any of the preset values at any time.

| Preset | Description |
|---|---|
| Production Standard | Best for most applications serving production traffic with AKS recommended best practices. |
| Dev/Test | Best for developing new workloads or testing existing workloads. |
| Production Economy | Best for serving production traffic in a cost conscious way if your workloads can tolerate interruptions. |
| Production Enterprise | Best for serving production traffic with rigorous permissions and hardened security. |

| Production Standard | Dev/Test | Production Economy | Production Enterprise | |
|---|---|---|---|---|
System node pool node size |
Standard_D8ds_v5 | Standard_D4ds_v5 | Standard_D8ds_v5 | Standard_D16ds_v5 |
System node pool autoscaling range |
2-5 nodes | 2-5 nodes | 2-5 nodes | 2-5 nodes |
User node pool node size |
Standard_D8ds_v5 | - | Standard_D8as_v4 | Standard_D8ds_v5 |
User node pool autoscaling range |
2-100 nodes | - | 0-25 nodes | 2-100 nodes |
Private cluster |
- | - | - | |
Availability zones |
- | - | ||
Azure Policy |
- | - | ||
Azure Monitor |
- | - | ||
Secrets store CSI driver |
- | - | ||
Network configuration |
Azure CNI Overlay | Azure CNI Overlay | Azure CNI Overlay | Azure CNI Overlay |
Network policy |
None | None | None | None |
Authentication and Authorization |
Local accounts with Kubernetes role-based access control (RBAC) | Local accounts with Kubernetes RBAC | Microsoft Entra ID Authentication with Azure role-based access control (Azure RBAC) | Microsoft Entra ID authentication with Azure RBAC |

## Next steps

You can increase certain default limits and quotas. If your resource supports an increase, request the increase through an [Azure support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest) (for **Issue type**, select **Quota**).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-scale -->

# Scaling options for applications in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When running applications in Azure Kubernetes Service (AKS), you might need to actively increase or decrease the amount of compute resources in your cluster. As you change the number of application instances you have, you might need to change the number of underlying Kubernetes nodes. You might also need to provision a large number of other application instances.

This article introduces core AKS application scaling concepts, including [manually scaling pods or nodes](#manually-scale-pods-or-nodes), using the [Horizontal pod autoscaler](#horizontal-pod-autoscaler), using the [Cluster autoscaler](#cluster-autoscaler), and integrating with [Azure Container Instances (ACI)](#burst-to-azure-container-instances-aci).

## Manually scale pods or nodes

You can manually scale replicas, or pods, and nodes to test how your application responds to a change in available resources and state. Manually scaling resources lets you define a set amount of resources to use, such as the number of nodes, to maintain a fixed cost. To manually scale, you define a replica or node count. The Kubernetes API then schedules the creation of more pods or the draining of nodes based on that replica or node count.

When you scale down nodes, the Kubernetes API calls the relevant Azure Compute API tied to the compute type used by your cluster. For example, for clusters built on Virtual Machine Scale Sets, the Virtual Machine Scale Sets API determines which nodes to remove. To learn more about how nodes are selected for removal on scale down, see the [Virtual Machine Scale Sets FAQ](/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-faq#if-i-reduce-my-scale-set-capacity-from-20-to-15--which-vms-are-removed-).

To get started with manually scaling nodes, see [manually scale nodes in an AKS cluster](scale-cluster). To manually scale the number of pods, see [kubectl scale command](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_scale/).

## Horizontal pod autoscaler

Kubernetes uses the horizontal pod autoscaler (HPA) to monitor the resource demand and automatically scale the number of pods. By default, the HPA checks the Metrics API every 15 seconds for any required changes in replica count, while the Metrics API retrieves data from the Kubelet every 60 seconds. As a result, HPA is updated every 60 seconds. When changes are required, the number of replicas is scaled accordingly. HPA works with AKS clusters that have deployed Metrics Server for Kubernetes version 1.8 and higher.

When you configure the HPA for a given deployment, you define the minimum and maximum number of replicas that can run. You also define the metric to monitor and base scaling decisions on, such as CPU usage.

To get started with the horizontal pod autoscaler in AKS, see [Autoscale pods in AKS](tutorial-kubernetes-scale#autoscale-pods).

### Cooldown of scaling events

As the HPA is effectively updated every 60 seconds, previous scale events might not have successfully completed before another check is made. This behavior could cause the HPA to change the number of replicas before the previous scale event could receive application workload and the resource demands to adjust accordingly.

To minimize race events, a delay value is set. This value defines how long the HPA must wait after a scale event before another scale event can be triggered. This behavior allows the new replica count to take effect and the Metrics API to reflect the distributed workload. There's [no delay for scale-up events as of Kubernetes 1.12](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/#support-for-cooldown-delay). However, the default delay on scale down events is *5 minutes*.

## Cluster autoscaler

To respond to changing pod demands, the Kubernetes cluster autoscaler adjusts the number of nodes based on the requested compute resources in the node pool. By default, the cluster autoscaler checks the Metrics API server every 10 seconds for any required changes in node count. If the cluster autoscaler determines that a change is required, the number of nodes in your AKS cluster is increased or decreased accordingly. The cluster autoscaler works with Kubernetes RBAC-enabled AKS clusters that run Kubernetes 1.10.x or higher.

The cluster autoscaler is typically used alongside the [horizontal pod autoscaler](#horizontal-pod-autoscaler). When combined, the horizontal pod autoscaler increases or decreases the number of pods based on application demand, and the cluster autoscaler adjusts the number of nodes to run more pods.

To get started with the cluster autoscaler in AKS, see [Cluster autoscaler on AKS](cluster-autoscaler).

### Scale out events

If a node doesn't have sufficient compute resources to run a requested pod, that pod can't progress through the scheduling process. The pod can't start unless more compute resources are made available within the node pool.

When the cluster autoscaler notices pods that can't be scheduled because of node pool resource constraints, the number of nodes within the node pool is increased to provide extra compute resources. When the nodes are successfully deployed and available for use within the node pool, the pods are then scheduled to run on them.

If your application needs to scale rapidly, some pods might remain in a state of waiting to be scheduled until more nodes deployed by the cluster autoscaler can accept the scheduled pods. For applications that have high burst demands, you can scale with virtual nodes and [Azure Container Instances](#burst-to-azure-container-instances-aci).

### Scale in events

The cluster autoscaler also monitors the pod scheduling status for nodes that haven't recently received new scheduling requests. This scenario indicates the node pool has more compute resources than required, and the number of nodes can be decreased. By default, nodes that pass a threshold of no longer being needed for 10 minutes are scheduled for deletion. When this situation occurs, pods are scheduled to run on other nodes within the node pool, and the cluster autoscaler decreases the number of nodes.

Your applications might experience some disruption as pods are scheduled on different nodes when the cluster autoscaler decreases the number of nodes. To minimize disruption, avoid applications that use a single pod instance.

## Kubernetes Event-driven Autoscaling (KEDA)

[Kubernetes Event-driven Autoscaling](https://keda.sh/docs/2.13/concepts/) (KEDA) is an open source component for event-driven autoscaling of workloads. It scales workloads dynamically based on the number of events received. KEDA extends Kubernetes with a custom resource definition (CRD), referred to as a *ScaledObject*, to describe how applications should be scaled in response to specific traffic.

KEDA scaling is useful in scenarios where workloads receive bursts of traffic or handle high volumes of data. KEDA differs from the Horizontal Pod Autoscaler as KEDA is event-driven and scales based on the number of events, while HPA is metrics-driven based on the resource utilization (for example, CPU and memory).

To get started with the KEDA add-on in AKS, see [KEDA overview](keda-about).

## Node Autoprovisioning

[Node autoprovisioning (preview)](node-autoprovision) (NAP), uses the open source Karpenter project that automatically deploys, configures, and manages [Karpenter](https://karpenter.sh/) on your AKS cluster. NAP dynamically provisions nodes based on pending pod resource requirements; it'll automatically select the optimal virtual machine (VM) SKU and quantity to meet real-time demand.

NAP takes a predefined list of VM SKUs as the starting point to decide which SKU is best suited for pending workloads. For more precise control, users can define the upper limits of resources used by a node pool and preferences of where workloads should be scheduled if there are multiple node pools.

## Control Plane Scaling and Safeguards

Kubernetes has a multi-dimensional scale envelope with each resource type representing a dimension. Not all resources are alike. For example, watches are commonly set on secrets, which result in list calls to the kube-apiserver that add cost and a disproportionately higher load on the control plane compared to resources without watches.

The control plane manages all the resource scaling in the cluster, so the more you scale the cluster within a given dimension, the less you can scale within other dimensions. For example, running hundreds of thousands of pods in an AKS cluster impacts how much pod churn rate (pod mutations per second) the control plane can support. Refer to ** best practices**.

AKS automatically scales control plane components based on key signals such as the total number of cores in the cluster and CPU or memory pressure on the control plane components.

To verify whether the control plane has scaled up, check the ConfigMap named 'large-cluster-control-plane-scaling-status'

```
kubectl describe configmap large-cluster-control-plane-scaling-status -n kube-system
```


### Control Plane Safeguards

If scaling the API server automatically does not stabilize it under high load scenarios, AKS deploys a managed API server guard. This guard acts as a last-resort mechanism to protect the API server by throttling non-system client requests and preventing the control plane from becoming completely unresponsive. System-critical calls to API server from components such as kubelet will continue to function normally.

To verify whether the managed API server guard has been applied, check for the presence of **"aks-managed-apiserver-guard"** FlowSchema and PriorityLevelConfiguration.

```
kubectl get flowschemas
kubectl get prioritylevelconfigurations
```


Refer to [API server and Etcd Troubleshooting guide](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-apiserver-etcd#cause-4-aks-managed-api-server-guard-was-applied) if the **"aks-managed-apiserver-guard"** FlowSchema and PriorityLevelConfiguration have been applied on the cluster for quick mitigation.

## Burst to Azure Container Instances (ACI)

To rapidly scale your AKS cluster, you can integrate with Azure Container Instances (ACI). Kubernetes has built-in components to scale the replica and node count. However, if your application needs to rapidly scale, the [horizontal pod autoscaler](#horizontal-pod-autoscaler) might schedule more pods than what the existing compute resources in the node pool can support. If configured, this scenario would then trigger the [cluster autoscaler](#cluster-autoscaler) to deploy more nodes in the node pool, but it might take a few minutes for those nodes to successfully provision and allow the Kubernetes scheduler to run pods on them.

ACI lets you quickly deploy container instances without extra infrastructure overhead. When you connect with AKS, ACI becomes a secured, logical extension of your AKS cluster. The [virtual nodes](virtual-nodes-cli) component, which is based on [virtual Kubelet](https://virtual-kubelet.io/), is installed in your AKS cluster that presents ACI as a virtual Kubernetes node. Kubernetes can then schedule pods that run as ACI instances through virtual nodes, not as pods on VM nodes directly in your AKS cluster.

Your application requires no modifications to use virtual nodes. Your deployments can scale across AKS and ACI and with no delay as the cluster autoscaler deploys new nodes in your AKS cluster.

Virtual nodes are deployed to another subnet in the same virtual network as your AKS cluster. This virtual network configuration secures the traffic between ACI and AKS. Like an AKS cluster, an ACI instance is a secure, logical compute resource isolated from other users.

## Next steps

To get started with scaling applications, see the following resources:

- Manually scale
[pods](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_scale/)or[nodes](scale-cluster) - Use the
[horizontal pod autoscaler](tutorial-kubernetes-scale#autoscale-pods) - Use the
[cluster autoscaler](cluster-autoscaler) - Use the
[Kubernetes Event-driven Autoscaling (KEDA) add-on](keda-about)

For more information on core Kubernetes and AKS concepts, see the following articles:

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-best-practices -->

# Best practices for Windows containers on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In AKS, you can create node pools that run Linux or Windows Server as the operating system (OS) on the nodes. Windows Server nodes can run native Windows container applications, such as .NET Framework. The Linux OS and Windows OS have different container support and configuration considerations. For more information, see [Windows container considerations in Kubernetes](windows-vs-linux-containers). To learn more about how various industries are using Windows containers on AKS, see [Windows AKS customer stories](windows-aks-customer-stories).

This article outlines best practices for running Windows containers on AKS.

## Create an AKS cluster with Linux and Windows node pools

When you create a new AKS cluster, the Azure platform creates a Linux node pool by default. This node pool contains system services needed for the cluster to function. Azure also creates and manages a control plane abstracted from the user, which means you aren't exposed to the underlying OS of the nodes hosting the main control plane components. We recommend that you run at least *two nodes* on the default Linux node pool to ensure the reliability and performance of your cluster. You can't delete the default Linux node pool unless you delete the entire cluster.

There are some cases where you should consider deploying a Linux node pool when planning to run Windows-based workloads on your AKS cluster, such as:

- If you want to run Linux and Windows workloads, you can deploy a Linux node pool and a Windows node pool in the same cluster.
- If you want to deploy infrastructure-related components based on Linux, such as NGINX, you need a Linux node pool alongside your Windows node pool. You can use control plane nodes for development and testing scenarios. For production workloads, we recommend that you deploy separate Linux node pools to ensure reliability and performance.

## Modernize existing applications with Windows on AKS

You might want to containerize existing applications and run them using Windows on AKS. Before starting the containerization process, it's important to understand the application architecture and dependencies. For more information, see [Containerize existing applications using Windows containers](/en-us/virtualization/windowscontainers/quick-start/lift-shift-to-containers).

## Windows OS version


Best practice guidanceWindows Server 2022 provides improved security and performance and is the recommended OS for Windows node pools on AKS. AKS uses Windows Server 2022 as the host OS version and only supports process isolation.


AKS supports two options for the Windows Server operating system: Long Term Servicing Channel Releases (LTSC) and Windows Server Annual Channel for Containers.

AKS supports Long Term Servicing Channel Releases (LTSC), including Windows Server 2025 (preview), Windows Server 2022, and Windows Server 2019. This channel is released every three years and is supported for five years. Customers using Long Term Support (LTS) should use Windows Server 2022.

AKS uses Windows Server 2019 and Windows Server 2022 as the host OS versions and only supports process isolation. AKS doesn't support container images built by other versions of Windows Server. For more information, see

[Windows container version compatibility](/en-us/virtualization/windowscontainers/deploy-containers/version-compatibility). Windows Server 2022 is the default OS for Kubernetes version 1.25 and later.Note

[Windows Server 2019 retires on March 1, 2026](https://github.com/Azure/AKS/issues/4091). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2019 on any Kubernetes version. All existing node pools with Windows Server 2019 will be unsupported. Windows Server 2019 is not supported in Kubernetes version 1.33 and above. Starting on April 1, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail.[Windows Server 2022 retires on March 15, 2027](https://github.com/Azure/AKS/issues/4168). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2022 on any Kubernetes version. All existing node pools with Windows Server 2022 will be unsupported. Windows Server 2022 is not supported in Kubernetes version 1.36 and above. Starting on April 1, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail.

For more information, see

[AKS release notes](https://github.com/Azure/AKS/releases). To stay up to date on the latest Windows Server OS versions and learn more about our roadmap of what's planned for support on AKS, see our[AKS public roadmap](https://github.com/azure/aks/projects/1).AKS supports

[Windows Server Annual Channel for Containers](https://techcommunity.microsoft.com/t5/windows-server-news-and-best/windows-server-annual-channel-for-containers/ba-p/3866248)(preview). This channel is released annually and is supported for two years. This channel is beneficial for customers requiring increased innovation cycles and portability. The portability functionality enables the Windows Server 2022-based container image OS to run on newer versions of Windows Server host OS, such as the new annual channel release.Windows Annual Channel versions are based on the Kubernetes version of your node pool. To upgrade from one Annual Channel version to the next,

[upgrade to a Kubernetes version](upgrade-aks-cluster)that supports the next Annual Channel version. For more information, see[Windows Server Annual Channel for Containers on AKS](windows-annual-channel).

## Monitoring


Best practice guidanceWindows Exporter is installed on all Windows nodes in certain regions. To view regional rollout, see

[AKS Github]. With Managed Prometheus and Grafana, you can monitor default collectors included in Windows Exporter on AKS. For more information, see[default Prometheus metrics configured in Azure Monitor].

Windows Exporter allows customers to see their metrics through Managed Prometheus or Prometheus OSS deployments and enjoy enhanced observability around their node and pod performance, health, and resource usage. These metrics are also visible with Managed Grafana.

- When enabling managed prometheus, add this required parameter for correct dashboard data presentation for Windows:
`--enable-windows-recording-rules`

. - Grafana includes dashboards for showing Windows resources, such as:
- Kubernetes / Compute Resources / Cluster (Windows)
- Kubernetes / Compute Resources / Namespace (Windows)
- Kubernetes / Compute Resources / Pod (Windows)
- Kubernetes / USE Method / Cluster (Windows)
- Kubernetes / USE Method / Node (Windows)


The default collectors included in Windows Exporter on AKS are: cpu, cpu_info, cs, container, logical_disk, memory, net, os, process, service, system, textfile. The metrics are exposed on port **19182** on the windows node. For more information on what metrics you can see using these collectors, please see [prometheus-community/windows_exporter](https://github.com/prometheus-community/windows_exporter#collectors).

## Networking

### Networking modes


Best practice guidanceAKS clusters with Windows node pools only support Azure Container Networking Interface (Azure CNI) and use it by default.


Windows doesn't support kubenet networking. AKS clusters with Windows node pools must use Azure CNI. For more information, see [Network concepts for applications in AKS](concepts-network).

Azure CNI offers two networking modes based on your workload requirements:

is an overlay network similar to kubenet. The overlay network allows you to use virtual network (VNet) IPs for nodes and private address spaces for pods within those nodes that you can reuse across the cluster. Azure CNI Overlay is the**Azure CNI Overlay****recommended networking mode**. It provides simplified network configuration and management and the best scalability in AKS networking.requires extra planning and consideration for IP address management. This mode provides VNet IPs for nodes**Azure CNI with Dynamic IP Allocation***and*pods. This configuration allows you direct access to pod IPs. However, it comes with increased complexity and reduced scalability.

To help you decide which networking mode to use, see [Choosing a network model](concepts-network-azure-cni-overlay#choose-a-network-model).

### Network policies


Best practice guidanceUse network policies to secure traffic between pods. Windows supports Azure Network Policy Manager and Calico Network Policy. For more information, see

[Differences between Network Policy engines: Cilium, Azure NPM, and Calico].

When managing traffic between pods, you should apply the principle of least privilege. The Network Policy feature in Kubernetes allows you to define and enforce ingress and egress traffic rules between the pods in your cluster. For more information, see [Secure traffic between pods using network policies in AKS](use-network-policies).

Windows pods on AKS clusters that use the Calico Network Policy enable Floating IP by default.

## Upgrades and updates

It's important to keep your Windows environment up-to-date to ensure your systems have the latest security updates, feature sets, and compliance requirements. In a Kubernetes environment like AKS, you need to maintain the Kubernetes version, Windows nodes, and Windows container images and pods.

### Kubernetes version upgrades

As a managed Kubernetes service, AKS provides the necessary tools to upgrade your cluster to the latest Kubernetes version. For more information, see [Upgrade an AKS cluster](upgrade-cluster).

### Windows node monthly updates

Windows nodes on AKS follow a monthly update schedule. Every month, AKS creates a new VHD with the latest available updates for Windows node pools. The VHD includes the host image, latest Nano Server image, latest Server Core image, and container. We recommend performing monthly updates to your Windows node pools to ensure your nodes have the latest security patches. For more information, see [Upgrade AKS node images](node-image-upgrade).

Note

Upgrades on Windows systems include both OS version upgrades and monthly node OS updates.

You can stay up to date with the availability of new monthly releases using the [AKS release tracker](https://releases.aks.azure.com/) and [AKS release notes](https://github.com/Azure/AKS/releases).

### Windows node OS version upgrades

Windows has a release cadence for new versions of the OS, including Windows Server 2025 (preview), Windows Server 2022, and Windows Server 2019. When upgrading your Windows node OS version, ensure the Windows container image version matches the Windows container host version and the node pools have only one version of Windows Server.

To upgrade the Windows node OS version, you need to complete the following steps:

- Create a new node pool with the new Windows Server version.
- Deploy your workloads with the new Windows container images to the new node pool.
- Decommission the old node pool.

For more information, see [Upgrade Windows Server workloads on AKS](upgrade-windows-2019-2022).

Note

Windows announced a new [Windows Server Annual Channel for Containers](https://techcommunity.microsoft.com/t5/windows-server-news-and-best/windows-server-annual-channel-for-containers/ba-p/3866248) that supports portability and mixed versions of Windows nodes and containers. This feature isn't yet supported in AKS.

To track AKS feature plans, see the [Public AKS roadmap](https://github.com/Azure/AKS/projects/1#card-90806240).

## Next steps

To learn more about Windows containers on AKS, see the following resources:

[Learn how to deploy, manage, and monitor Windows containers on AKS](/en-us/training/paths/deploy-manage-monitor-wincontainers-aks).- Open an issue or provide feedback in the
[Windows containers GitHub repository](https://github.com/microsoft/Windows-Containers/issues). - Review the
[third-party partner solutions for Windows on AKS](windows-aks-partner-solutions).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/start-stop-cluster -->

# Stop and start an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You may not need to continuously run your Azure Kubernetes Service (AKS) workloads. For example, you may have a development cluster that you only use during business hours. This means there are times where your cluster might be idle, running nothing more than the system components. You can reduce the cluster footprint by [scaling all User node pools to 0](scale-cluster#scale-user-node-pools-to-0), but your

[is still required to run the system components while the cluster is running.](use-system-pools)

`System`

poolTo better optimize your costs during these periods, you can turn off, or stop, your cluster. This action stops your control plane and agent nodes, allowing you to save on all the compute costs, while maintaining all objects except standalone pods. The cluster state is stored for when you start it again, allowing you to pick up where you left off.

Caution

Stopping your cluster deallocates the control plane and releases the capacity. In regions experiencing capacity constraints, customers may be unable to start a stopped cluster. We do not recommend stopping mission critical workloads for this reason.

Note

AKS start operations will restore all objects from ETCD with the exception of standalone pods with the same names and ages. meaning that a pod's age will continue to be calculated from its original creation time. This count will keep increasing over time, regardless of whether the cluster is in a stopped state.

## Before you begin

This article assumes you have an existing AKS cluster. If you need an AKS cluster, you can create one using [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

### About the cluster stop/start feature

When using the cluster stop/start feature, the following conditions apply:

- This feature is only supported for Virtual Machine Scale Set backed clusters.
- You can't stop clusters which use the
[Node Autoprovisioning (NAP)](node-autoprovision)feature. - The cluster state of a stopped AKS cluster is preserved for up to 12 months. If your cluster is stopped for more than 12 months, you can't recover the state. For more information, see the
[AKS support policies](support-policies). - You can only perform start or delete operations on a stopped AKS cluster. To perform other operations, like scaling or upgrading, you need to start your cluster first.
- If you provisioned PrivateEndpoints linked to private clusters, they need to be deleted and recreated again when starting a stopped AKS cluster.
- Because the stop process drains all nodes, any standalone pods (i.e. pods not managed by a Deployment, StatefulSet, DaemonSet, Job, etc.) will be deleted.
- When you start your cluster back up, the following behavior is expected:
- The IP address of your API server may change.
- If you're using cluster autoscaler, when you start your cluster, your current node count may not be between the min and max range values you set. The cluster starts with the number of nodes it needs to run its workloads, which isn't impacted by your autoscaler settings. When your cluster performs scaling operations, the min and max values will impact your current node count, and your cluster will eventually enter and remain in that desired range until you stop your cluster.


## Stop an AKS cluster

Use the

command to stop a running AKS cluster, including the nodes and control plane. The following example stops a cluster named`az aks stop`

*myAKSCluster*:`az aks stop --name myAKSCluster --resource-group myResourceGroup`

Verify your cluster has stopped using the

command and confirming the`az aks show`

`powerState`

shows as`Stopped`

.`az aks show --name myAKSCluster --resource-group myResourceGroup`

Your output should look similar to the following condensed example output:

`{ [...] "nodeResourceGroup": "MC_myResourceGroup_myAKSCluster_westus2", "powerState":{ "code":"Stopped" }, "privateFqdn": null, "provisioningState": "Succeeded", "resourceGroup": "myResourceGroup", [...] }`

If the

`provisioningState`

shows`Stopping`

, your cluster hasn't fully stopped yet.

Important

If you're using [pod disruption budgets](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/), the stop operation can take longer, as the drain process will take more time to complete.

## Start an AKS cluster

Caution

After utilizing the start/stop feature on AKS, it is essential to wait 15-30 minutes before restarting your AKS cluster. This waiting period is necessary because it takes several minutes for the relevant services to fully stop. Attempting to restart your cluster during this process can disrupt the shutdown process and potentially cause issues with the cluster or its workloads.

Use the

command to start a stopped AKS cluster. The cluster restarts with the previous control plane state and number of agent nodes. The following example starts a cluster named`az aks start`

*myAKSCluster*:`az aks start --name myAKSCluster --resource-group myResourceGroup`

Verify your cluster has started using the

command and confirming the`az aks show`

`powerState`

shows`Running`

.`az aks show --name myAKSCluster --resource-group myResourceGroup`

Your output should look similar to the following condensed example output:

`{ [...] "nodeResourceGroup": "MC_myResourceGroup_myAKSCluster_westus2", "powerState":{ "code":"Running" }, "privateFqdn": null, "provisioningState": "Succeeded", "resourceGroup": "myResourceGroup", [...] }`

If the

`provisioningState`

shows`Starting`

, your cluster hasn't fully started yet.

## Next steps

- To learn how to scale
`User`

pools to 0, see[Scale](scale-cluster#scale-user-node-pools-to-0).`User`

pools to 0 - To learn how to save costs using Spot instances, see
[Add a spot node pool to AKS](spot-node-pool). - To learn more about the AKS support policies, see
[AKS support policies](support-policies).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-ai-ml-language-models -->

# Concepts - Small and large language models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about small and large language models, including when to use them and how you can use them with your AI and machine learning workflows on Azure Kubernetes Service (AKS).

## What are language models?

Language models are powerful machine learning models used for natural language processing (NLP) tasks, such as text generation and sentiment analysis. These models represent natural language based on the probability of words or sequences of words occurring in a given context.

*Conventional language models* have been used in supervised settings for research purposes where the models are trained on well-labeled text datasets for specific tasks. *Pre-trained language models* offer an accessible way to get started with AI and have become more widely used in recent years. These models are trained on large-scale text corpora from the internet using deep neural networks and can be fine-tuned on smaller datasets for specific tasks.

The size of a language model is determined by its number of parameters, or *weights*, that determine how the model processes input data and generates output. Parameters are learned during the training process by adjusting the weights within layers of the model to minimize the difference between the model's predictions and the actual data. The more parameters a model has, the more complex and expressive it is, but also the more computationally expensive it is to train and use.

In general, **small language models** have *fewer than 10 billion parameters*, and **large language models** have *more than 10 billion parameters*. For example, the new Microsoft Phi-3 model family has three versions with different sizes: mini (3.8 billion parameters), small (7 billion parameters), and medium (14 billion parameters).

## When to use small language models

### Advantages

Small language models are a good choice if you want models that are:

**Faster and more cost-effective to train and run**: They require less data and compute power.**Easy to deploy and maintain**: They have smaller storage and memory footprints.**Less prone to**, which is when a model learns the noise or specific patterns of the training data and fails to generalize new data.*overfitting***Interpretable and explainable**: They have fewer parameters and components to understand and analyze.

### Use cases

Small language models are suitable for use cases that require:

**Limited data or resources**, and you need a quick and simple solution.**Well-defined or narrow tasks**, and you don't need much creativity in the output.**High-precision and low-recall tasks**, and you value accuracy and quality over coverage and quantity.**Sensitive or regulated tasks**, and you need to ensure the transparency and accountability of the model.

The following table lists some popular, high-performance small language models:

| Model family | Model sizes (Number of parameters) | Software license |
|---|---|---|
| Microsoft Phi-3 | Phi-3-mini (3.8 billion), Phi-3-small (7 billion) | MIT license |
| Microsoft Phi-2 | Phi-2 (2.7 billion) | MIT license |
| Falcon | Falcon-7B (7 billion) | Apache 2.0 license |

## When to use large language models

### Advantages

Large language models are a good choice if you want models that are:

**Powerful and expressive**: They can capture more complex patterns and relationships in the data.**General and adaptable**: They can handle a wider range of tasks and transfer knowledge across domains.**Robust and consistent**: They can handle noisy or incomplete inputs and avoid common errors and biases.

### Use cases

Large language models are suitable for use cases that require:

**Abundant data and resources**, and you have the budget to build and maintain a complex solution.**Low-precision and high-recall tasks**, and you value coverage and quantity over accuracy and quality.**Challenging or exploratory tasks**, and you want to leverage the model's capacity to learn and adapt.

The following table lists some popular, high-performance large language models:

| Model family | Model sizes (Number of parameters) | Software license |
|---|---|---|
| Microsoft Phi-3 | Phi-3-medium (14 billion) | MIT license |
| Falcon | Falcon-40B (40 billion) | Apache 2.0 license |

## Experiment with small and large language models on AKS

Kubernetes AI Toolchain Operator (KAITO) is an open-source operator that automates small and large language model deployments in Kubernetes clusters. The KAITO add-on for AKS simplifies onboarding and reduces the time-to-inference for open-source models on your AKS clusters. The add-on automatically provisions right-sized GPU nodes and sets up the associated interference server as an endpoint server to your chosen model.

For more information, see [Deploy an AI model on AKS with the AI toolchain operator](ai-toolchain-operator). To get started with a range of supported small and large language models for your inference workflows, see the [KAITO model GitHub repository](https://github.com/Azure/kaito/tree/main/presets).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Next steps

To learn more about containerized AI and machine learning workloads on AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-advanced-container-networking-services -->

# Use Advanced Container Networking Services on your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to enable and disable Advanced Container Networking Services, including [Container Network Observability](advanced-container-networking-services-overview#container-network-observability) and [Container Network Security](advanced-container-networking-services-overview#container-network-security), on your AKS clusters.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - Azure CLI version 2.71.0 or higher. Find your version using the
`az --version`

command. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). [Install the](#install-the-aks-preview-azure-cli-extension)version`aks-preview`

Azure CLI extension`14.0.0b6`

or higher.[Register the](#register-the-advancednetworkingl7policypreview-feature-flag)in your subscription.`AdvancedNetworkingL7PolicyPreview`

feature flag- Clusters that have the Cilium data plane support
*Container Network Observability*and*Container Network Security*in Kubernetes version 1.29 and later.

## Install the `aks-preview`

Azure CLI extension

Install or update the Azure CLI preview extension using the

or`az extension add`

command.`az extension update`

`# Install the aks-preview extension az extension add --name aks-preview # Update the extension to make sure you have the latest version installed az extension update --name aks-preview`


## Register the `AdvancedNetworkingL7PolicyPreview`

feature flag

Register the

`AdvancedNetworkingL7PolicyPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"`

Registration takes a few minutes to complete.

Verify successful registration using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"`


## Set environment variables

The examples in this article use the following environment variables:

| Variable | Description | Example value |
|---|---|---|
`RESOURCE_GROUP` |
Name of the Azure resource group | `myResourceGroup` |
`LOCATION` |
Azure region for resources | `eastus` |
`CLUSTER_NAME` |
Name of the AKS cluster | `myAKSCluster` |

**All commands in this article assume these environment variables are set**. Make sure to replace the example values with your own values.

## Create a resource group

Create a resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`


## Create a new AKS cluster with Advanced Container Networking Services

Note

When the `--acns-advanced-networkpolicies`

parameter is set to `L7`

, both Layer 7 and fully qualified domain name (FQDN) filtering policies are enabled. If you want to enable only FQDN filtering, set the parameter to `FQDN`

.

Create an AKS cluster with Advanced Container Networking Services and Cilium using the

command with the`az aks create`

`--enable-acns`

and`--network-dataplane cilium`

flags.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --network-plugin azure \ --network-plugin-mode overlay \ --network-dataplane cilium \ --kubernetes-version 1.29 \ --enable-acns \ --acns-advanced-networkpolicies <L7/FQDN>`


Important

The [Container Network Security](advanced-container-networking-services-overview#container-network-security) feature isn't available for non-Cilium clusters.

Create an AKS cluster with Advanced Container Networking Services using the

command with the`az aks create`

`--enable-acns`

flag.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --network-plugin azure \ --network-plugin-mode overlay \ --enable-acns`


## Enable Advanced Container Networking Services on an existing cluster

Enable Advanced Container Networking Services on an existing AKS cluster with Cilium using the

command with the`az aks update`

`--enable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --acns-advanced-networkpolicies <L7/FQDN>`


Enable Advanced Container Networking Services on an existing AKS cluster using the

command with the`az aks update`

`--enable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns`


## Disable Advanced Container Networking Services on an AKS cluster

Disable Advanced Container Networking Services on an existing AKS cluster using the

command with the`az aks update`

`--disable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --disable-acns`


## Disable Container Network Observability on an AKS cluster

Disable the Container Network Observability feature without affecting other Advanced Container Networking Services features using the

command with the`az aks update`

`--disable-acns-observability`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --disable-acns-observability`


Container Network Observability is the only feature available for non-Cilium clusters, so you can disable it only by disabling the entire Advanced Container Networking Services suite.

Disable the Container Network Observability feature on an existing AKS cluster using the

command with the`az aks update`

`--disable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --disable-acns`


## Disable Container Network Security on an AKS cluster

Disable the Container Network Security feature without affecting other Advanced Container Networking Services features using the

command with the`az aks update`

`--disable-acns-security`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --disable-acns-security`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-arm64-vms -->

# Use Arm-based processor (Arm64) Virtual Machines (VMs) in an Azure Kubernetes Service (AKS) cluster for cost effectiveness

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Arm-based processors (Arm64)](/en-us/azure/virtual-machines/sizes/cobalt-overview) are power-efficient and cost-effective, but don't compromise on performance. These Arm64 VMs are engineered to efficiently run dynamic, scalable workloads and can deliver up to 50% better price-performance than comparable x86-based VMs for scale-out workloads.

Because of their ability to scale workloads efficiently, Arm64 VMs are well-suited for web or application servers, open-source databases, cloud-native applications, gaming servers, and other high traffic applications.

Note

While a combination of CPU, memory, and networking capacity configurations heavily influences the cost effectiveness of a SKU, Arm64 VM types are recommended for cost optimization.

In this article, you'll learn how to add a Arm64 VM to an existing node pool.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

Before you begin, make sure you have:

## Limitations

- Arm64 VMs aren't supported for Windows node pools.
- Existing node pools can't be updated to use an Arm64 VM.
- Federal Information Process Standard (FIPS)-enabled node pools are only supported with Arm64 SKUs when using Azure Linux 3.0+.
- Arm64 node pools aren't supported on Defender-enabled clusters with Kubernetes version 1.29.0 or lower.

## Create node pools with Arm64 VMs

The Arm64 processor provides low power compute for your Kubernetes workloads. Arm64 virtual machines can be added to existing clusters even mixing Intel and Arm architecture node pools within a cluster. To create an Arm64 node pool, you need to choose a [Dpsv5](/en-us/azure/virtual-machines/dpsv5-dpdsv5-series), [Dplsv5](/en-us/azure/virtual-machines/dplsv5-dpldsv5-series), or [Epsv5](/en-us/azure/virtual-machines/epsv5-epdsv5-series) series virtual machine.

### Add a node pool with an Arm64 VM

Use [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) to add a node pool with an Arm64 VM to an existing cluster. Alternatively, if you're using

[Azure Linux 3.0+](/en-us/azure/azure-linux/how-to-enable-azure-linux-3), you can add a node pool with an Arm64 VM and

[FIPS](enable-fips-nodes)enabled.

Add a node pool with an Arm64 VM

`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $ARM_NODE_POOL_NAME \ --node-count 3 \ --node-vm-size Standard_D2pds_v5`

Add a FIPS-enabled node pool with an Arm64 VM

Limitations:

- Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)enabled aren't supported with Ubuntu OS. - Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)require kubernetes version 1.31+.

Use the

with`az aks nodepool add`

`--enable-fips-image`

and`--os-sku`

parameters.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $ARM_NODE_POOL_NAME \ --os-sku AzureLinux --enable-fips-image --kubernetes-version 1.31 --node-count 3 \ --node-vm-size Standard_D2pds_v5`

For more information on verifying FIPS enablement and disabling FIPS, see

[Enable FIPS node pools](enable-fips-nodes).- Node pools with Arm64 VMs and
Update a node pool with an Arm64 VM to enable FIPS

Limitations:

- Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)enabled aren't supported with Ubuntu OS. - Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)require kubernetes version 1.31+.

Use

command with the`az aks nodepool update`

`--enable-fips-image`

parameter to enable FIPS on an existing node pool.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name np \ --enable-fips-image`

This command triggers a reimage of the node pool immediately to deploy the FIPS compliant Operating System. This reimage occurs during the node pool update. No extra steps are required.

- Node pools with Arm64 VMs and

For more information on verifying FIPS enablement and disabling FIPS, see [Enable FIPS node pools](enable-fips-nodes).

## Verify the node pool uses Arm64

Verify a node pool uses Arm64 using the [ az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command and verify the

`vmSize`

is a [Dpsv5](/en-us/azure/virtual-machines/dpsv5-dpdsv5-series),

[Dplsv5](/en-us/azure/virtual-machines/dplsv5-dpldsv5-series), or

[Epsv5](/en-us/azure/virtual-machines/epsv5-epdsv5-series)series.

```
az aks nodepool show \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name mynodepool \
--query vmSize
```


The following example output shows the node pool uses Arm64:

```
"Standard_D2pds_v5"
```


## Next steps

In this article, you learned how to add a node pool with an Arm64 VM to an AKS cluster.

- For more recommendations for cost savings, see
[Best practices for cost optimization in Azure Kubernetes Service (AKS)](best-practices-cost). - For more information about Arm64, see
[Cobalt Arm-based processors (Arm64)](/en-us/azure/virtual-machines/sizes/cobalt-overview). - For more information on verifying FIPS enablement and disabling FIPS, see
[Enable FIPS node pools](enable-fips-nodes). - For Azure Linux 3.0 enablement and support details, see
[Enable Azure Linux 3.0](/en-us/azure/azure-linux/how-to-enable-azure-linux-3).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/optimized-addon-scaling -->

# Enable cost optimized add-on scaling on your Azure Kubernetes Service (AKS) cluster (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of cost optimized add-on scaling in Azure Kubernetes Service (AKS). With cost-optimized add-on scaling, you can manage add-ons that require custom CPU and memory by overriding default configurations or enabling autoscaling. This feature ensures that resources aren't overly allocated to add-on pods, improving cost savings and cluster efficiency.

## Overview

Enabling cost optimized add-on scaling installs the [Vertical Pod Autoscaler (VPA)add-on](vertical-pod-autoscaler), allowing supported add-ons to autoscale based on usage.

This feature also allows you to customize the resource's default CPU/ memory requests and limits in Deployments and DaemonSets, the maximum and minimum allowed CPU/ memory, and the VPA update mode within VPA custom resources. For more information, see [customize the resource configuration for AKS add-ons](customize-resource-configuration).

### Supported AKS add-ons

The following AKS managed add-ons support the cost optimized add-on scaling feature:

| Add-on | Enablement behavior | VPA custom resource name | Command to check VPA custom resource |
|---|---|---|---|
|

`coredns`

`kubectl get vpa coredns --namespace kube-system`

[Workload identity](workload-identity-deploy-cluster)`azure-wi-webhook-controller-manager`

`kubectl get vpa azure-wi-webhook-controller-manager --namespace kube-system`

[Image Integrity](image-integrity)`ratify`

`kubectl get vpa ratify --namespace gatekeeper-system`

[Network Observability (Retina)](container-network-observability-how-to)`retina-agent`

and `retina-operator`

`kubectl get vpa retina-agent --namespace kube-system`

and `kubectl get vpa retina-operator --namespace kube-system`

### Supported VPA modes for cost optimized add-on scaling

VPA currently supports the following modes for cost optimized add-on scaling:

*Off*: The VPA provides resource recommendation data but doesn't apply it to the target pod.*Initial*(default mode): The VPA automatically applies CPU and memory recommendations to the target pod when it restarts, but it doesn't initiate the restart itself.*Auto*: The VPA automatically updates CPU and memory requests for pods based on recommendations.

Note

When enabling cost optimized add-on scaling, consider the following information:

- If you delete the Deployment, DaemonSet, or VPA custom resource, the changes revert back to the AKS add-on's initial configuration.
- The cost optimized add-on scaling feature enables the
[VPA add-on](vertical-pod-autoscaler)to autoscale the supported AKS add-ons. It doesn't work with self-hosted VPA. - AKS restarts the add-on pods when enabling cost optimized add-on scaling. CoreDNS is currently the only exception to avoid potential disruptions during the restart. For more information, see
[CoreDNS autoscaling behavior](coredns-autoscale).

Warning

Make sure you have enough compute resources on the system node pool for your addons when you enable cost optimized add-on scaling. AKS recommends turning on the [cluster autoscaler](cluster-autoscaler-overview) or [node autoprovision](node-autoprovision) to ensure right-sizing of your compute resources automatically.
Monitor for pending add-on pods when using the cost-optimized add-on scaling feature. VPA might recommend resource requests that exceed available node capacity, potentially leading to unschedulable pods. You can control this behavior by [customizing min/max values](customize-resource-configuration) for requests and limits of supported addons.

## Prerequisites

- An AKS cluster running Kubernetes version 1.25 or later.
- The Azure CLI version 2.60.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). [Install the](#install-the-aks-preview-azure-cli-extension)and`aks-preview`

Azure CLI extension[register the cost optimized add-on scaling preview feature](#register-the-cost-optimized-add-on-scaling-preview-feature).

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Install the `aks-preview`

Azure CLI extension

Install the

`aks-preview`

extension using the`az extension add`

command.`az extension add --name aks-preview`

Update to the latest version of the extension using the

`az extension update`

command.`az extension update --name aks-preview`


### Register the cost optimized add-on scaling preview feature

Register the cost optimized add-on scaling preview feature using the

`az feature register`

command.`az feature register --namespace "Microsoft.ContainerService" --name "AKS-AddonAutoscalingPreview"`

It takes a few minutes for the status to show as

*Registered*.Verify the registration status using the

`az feature show`

command.`az feature show --namespace "Microsoft.ContainerService" --name "AKS-AddonAutoscalingPreview"`

When the status shows as

*Registered*, refresh the registration of the Microsoft.ContainerService provider using the`az provider register`

command.`az provider register --namespace Microsoft.ContainerService`


## Enable cost optimized add-on scaling on an AKS cluster

When enabling the add-on, the AKS cluster automatically installs the [VPA add-on](vertical-pod-autoscaler). The [AKS add-ons that support the cost optimized add-on scaling feature](#supported-aks-add-ons) have different enablement behavior.

Note

If you're using Bicep, ARM templates, or Terraform, set `VerticalPodAutoscaler`

to `"True"`

and `AddonAutoscaling`

to `"enabled"`

.

### Enable cost optimized add-on scaling on a new cluster

Enable cost optimized add-on scaling on a new AKS cluster using the

command with the`az aks create`

`--enable-optimized-addon-scaling`

flag.`az aks create --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --enable-optimized-addon-scaling`


### Enable cost optimized add-on scaling on an existing cluster

Enable cost optimized add-on scaling on an existing AKS cluster using the

command with the`az aks update`

`--enable-optimized-addon-scaling`

flag.`az aks update --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --enable-optimized-addon-scaling`


## Disable cost optimized add-on scaling on an AKS cluster

Disable cost optimized add-on scaling on an AKS cluster using the

command with the`az aks update`

`--disable-optimized-addon-scaling`

flag.`az aks update --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --disable-optimized-addon-scaling`


Note

Disabling the cost optimized add-on scaling feature doesn't disable the VPA add-on by default. To disable VPA, see [Disable VPA on an AKS cluster](use-vertical-pod-autoscaler#disable-the-vertical-pod-autoscaler-on-an-existing-cluster).

## Customize default resource configuration

With the cost optimized add-on scaling feature enabled on your cluster, you can customize the default CPU/memory settings for the add-on resources as well as the default VPA configuration for supported AKS add-ons. For more information, see [customize the resource configuration for AKS add-ons](customize-resource-configuration).

## Applying the VPA recommended values manually

Note

With *Initial* mode, the VPA applies the recommended CPU and memory requests only when a pod is created or updated. If you want the recommendations to take effect immediately, please update the pods manually. Before manually applying the recommended values, [make sure the VPA update mode is set to Initial or Auto in the VPA custom resource](customize-resource-configuration#customize-resource-update-mode).

Check the pod status and CPU/memory utilization to verify that the pod is running as expected.

The following example uses the

`kubectl get pod`

command to check a CoreDNS pod status:`kubectl get pod <coredns-pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a CoreDNS pod:

`apiVersion: v1 kind: Pod metadata: name: <coredns-pod-name> namespace: kube-system spec: ... containers: - name: coredns resources: limits: cpu: "3" memory: "500Mi" requests: cpu: "100m" memory: "70Mi"`

Get the VPA recommended value using the

`kubectl get vpa`

command.`kubectl get vpa coredns --namespace kube-system`

The following output shows an example of the VPA recommended value for a CoreDNS pod:

`NAME MODE CPU MEM PROVIDED AGE coredns Initial 11m 23574998 True 44m`

If you want to use the values recommended by VPA, manually delete the pod using the

`kubectl delete pod`

command to restart the pod with the VPA recommended values.`kubectl delete pod <coredns-pod-name> --namespace kube-system`

After the pod restarts, verify the pod status and CPU/memory updates using the

`kubectl get pod`

command.`kubectl get pod <coredns-pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a CoreDNS pod after applying the VPA recommended values:

`apiVersion: v1 kind: Pod metadata: name: <coredns-pod-name> namespace: kube-system spec: ... containers: - name: coredns resources: limits: cpu: "330m" memory: "168392842" requests: cpu: "11m" memory: "23574998"`


## Troubleshooting

With the cost optimized add-on scaling feature enabled on your cluster, you can customize the default CPU and memory settings for add-on resources, as well as modify the default VPA configuration for supported AKS managed add-ons

If your autoscaling enabled add-on pods are in a pending state, or you don't see any VPA recommendations for autoscaling enabled add-ons, follow these steps to troubleshoot the issue.

### Check AKS-managed VPA add-on status

Check if all VPA system components are running using the

`kubectl get pods`

command.`kubectl get pods --namespace kube-system | grep vpa`

The output should show three pods (vpa-admission-controller, vpa-recommender, and vpa-updater) running in the

`kube-system`

namespace, similar to the following example:`vpa-admission-controller 2/2 2 2 4m11s vpa-recommender 1/1 1 1 4m11s vpa-updater 1/1 1 1 4m11s`

For each of the three VPA pods, check the logs for any errors using the

`kubectl logs`

command. Make sure to replace`<pod-name>`

with the names of the VPA pods.`kubectl logs <pod-name> --namespace kube-system | grep -e '^E[0-9]\{4\}'`

Confirm the custom resource definition (CRD) was creating using the

`kubectl get`

command.`kubectl get customresourcedefinition | grep verticalpodautoscalers`


### Check pod status and CPU/memory utilization

Check the pod's status using the

`kubectl get pod`

command.`kubectl get pod <pod-name> --namespace=kube-system`

If the pod has a status of

`Pending`

, check the pod's status property to determine the reason the pod isn't running.`kubectl describe pod <pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a pod with a status of

`Pending`

:`apiVersion: v1 kind: Pod ... status: conditions: - lastProbeTime: null lastTransitionTime: "2023-05-03T17:05:26Z" message: '0/1 nodes are available: 1 Insufficient cpu, 1 Insufficient memory. preemption: 0/1 nodes are available: 1 Insufficient cpu, 1 Insufficient memory..' reason: Unschedulable status: "False" type: PodScheduled phase: Pending qosClass: Guaranteed`

If the output shows that the pod is

`Pending`

due to insufficient CPU or memory, consider the following actions:- Add more nodes so that pods can be scheduled in nodes with lower resource usage.
- Disable VPA for the target add-on pod by changing the update mode to
*Off*, and then[manually update the requests/limits](customize-resource-configuration)to the available resource values on the node. Be cautious when setting resource limits to extremely low values, as this may result in the pod encountering OOM kills or CPU throttling if it attempts to use more resources than are available on the node.


## Next steps

- Configure
[Cluster Autoscaler](cluster-autoscaler-overview)or[Node Autoprovisioning](node-autoprovision)in your cluster to automatically scale the cluster.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-about -->

# Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Istio](https://istio.io/latest/) addresses the challenges developers and operators face with a distributed or microservices architecture. The Istio-based service mesh add-on provides an officially supported and tested integration for Azure Kubernetes Service (AKS).

## What is a Service Mesh?

Modern applications are typically architected as distributed collections of microservices, with each collection of microservices performing some discrete business function. A service mesh is a dedicated infrastructure layer that you can add to your applications. It allows you to transparently add capabilities like observability, traffic management, and security, without adding them to your own code. The term **service mesh** describes both the type of software you use to implement this pattern, and the security or network domain that is created when you use that software.

As the deployment of distributed services, such as in a Kubernetes-based system, grows in size and complexity, it can become harder to understand and manage. You may need to implement capabilities such as discovery, load balancing, failure recovery, metrics, and monitoring. A service mesh can also address more complex operational requirements like A/B testing, canary deployments, rate limiting, access control, encryption, and end-to-end authentication.

Service-to-service communication is what makes a distributed application possible. Routing this communication, both within and across application clusters, becomes increasingly complex as the number of services grow. Istio helps reduce this complexity while easing the strain on development teams.

## What is Istio?

Istio is an open-source service mesh that layers transparently onto existing distributed applications. Istio’s powerful features provide a uniform and more efficient way to secure, connect, and monitor services. Istio enables load balancing, service-to-service authentication, and monitoring – with few or no service code changes. Its powerful control plane brings vital features, including:

- Secure service-to-service communication in a cluster with TLS (Transport Layer Security) encryption, strong identity-based authentication, and authorization.
- Automatic load balancing for HTTP, gRPC, WebSocket, and TCP traffic.
- Fine-grained control of traffic behavior with rich routing rules, retries, failovers, and fault injection.
- A pluggable policy layer and configuration API supporting access controls, rate limits, and quotas.
- Automatic metrics, logs, and traces for all traffic within a cluster, including cluster ingress and egress.

## How is the add-on different from open-source Istio?

This service mesh add-on uses and builds on top of open-source Istio. The add-on flavor provides the following extra benefits:

- Istio versions are tested and verified to be compatible with supported versions of Azure Kubernetes Service.
- Microsoft handles scaling and configuration of Istio control plane
- Microsoft adjusts scaling of AKS components like
`coredns`

when Istio is enabled. - Microsoft provides managed lifecycle (upgrades) for Istio components when triggered by user.
- Verified external and internal ingress set-up.
- Verified to work with
[Azure Monitor managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)and[Azure Managed Grafana](/en-us/azure/managed-grafana/overview). - Official Azure support provided for the add-on.

## Limitations

Istio-based service mesh add-on for AKS has the following limitations:

- The add-on doesn't work on AKS clusters that are using
[Open Service Mesh addon for AKS](open-service-mesh-about). - The add-on doesn't work on AKS clusters with self-managed installations of Istio.
- The add-on doesn't support adding pods associated with virtual nodes to be added under the mesh.
- The add-on doesn't yet support the sidecar-less Ambient mode. Microsoft is currently contributing to Ambient workstream under Istio open source. Product integration for Ambient mode is on the roadmap and is being continuously evaluated as the Ambient workstream evolves.
- The add-on doesn't yet support multi-cluster deployments.
- The add-on doesn't yet support Windows Server containers. Windows Server containers aren't yet supported in open source Istio right now. Issue tracking this feature ask can be found
[here](https://github.com/istio/istio/issues/27893). - Customization of mesh through the following custom resources is currently blocked -
`ProxyConfig, WorkloadEntry, WorkloadGroup, IstioOperator, WasmPlugin`

. - While the add-on allows the use of
`EnvoyFilter`

's, issues arising from them (for example from the Lua script or from the compression library) are outside the support scope of the Istio add-on. See the[support policy document](istio-support-policy#allowed-supported-and-blocked-customizations)for more information about the support categories for Istio add-on features and configuration options. - Gateway API for Istio ingress gateway or managing mesh traffic (GAMMA) is currently not yet supported with Istio add-on. However, Gateway API for Istio ingress traffic management is currently under active development for the add-on. While the add-on supports
[annotation and](istio-deploy-ingress#ingress-gateway-service-customizations), port or protocol configuration is currently not supported.`externalTrafficPolicy`

customization for the Istio ingress gateways - The add-on supports customization of a subset of the fields in
[MeshConfig](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/). Other customizations may be allowed but unsupported or disallowed entirely, as detailed[here](istio-meshconfig#allowed-supported-and-blocked-meshconfig-values).

## Feedback and feature ask

Feedback and feature ask for the Istio add-on can be provided by creating [issues with label 'service-mesh' on AKS GitHub repository](https://github.com/Azure/AKS/issues?q=is%3Aopen+is%3Aissue+label%3Aservice-mesh).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/reduce-latency-ppg -->

# Use proximity placement groups to reduce latency for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

When using proximity placement groups on AKS, colocation only applies to the agent nodes. Node to node and the corresponding hosted pod to pod latency is improved. The colocation doesn't affect the placement of a cluster's control plane.

When deploying your application in Azure, you can create network latency by spreading virtual machine (VM) instances across regions or availability zones, which may impact the overall performance of your application. A proximity placement group is a logical grouping used to make sure Azure compute resources are physically located close to one another. Some applications, such as gaming, engineering simulations, and high-frequency trading (HFT) require low latency and tasks that can complete quickly. For similar high-performance computing (HPC) scenarios, consider using [proximity placement groups (PPG)](/en-us/azure/virtual-machines/co-location#proximity-placement-groups) for your cluster's node pools.

## Before you begin

This article requires Azure CLI version 2.14 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Limitations

- A proximity placement group can map to only
*one*availability zone. - A node pool must use Virtual Machine Scale Sets to associate a proximity placement group.
- A node pool can associate a proximity placement group at node pool create time only.

## Node pools and proximity placement groups

The first resource you deploy with a proximity placement group attaches to a specific data center. Any extra resources you deploy with the same proximity placement group are colocated in the same data center. Once all resources using the proximity placement group are stopped (deallocated) or deleted, it's no longer attached.

- You can associate multiple node pools with a single proximity placement group.
- You can only associate a node pool with a single proximity placement group.

### Configure proximity placement groups with availability zones

Note

While proximity placement groups require a node pool to use only *one* availability zone, the [baseline Azure VM SLA of 99.9%](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_9/) is still in effect for VMs in a single zone.

Proximity placement groups are a node pool concept and associated with each individual node pool. Using a PPG resource has no impact on AKS control plane availability, which can impact how you should design your cluster with zones. To ensure a cluster is spread across multiple zones, we recommend using the following design:

- Provision a cluster with the first system pool using
*three*zones and no proximity placement group associated to ensure the system pods land in a dedicated node pool, which spreads across multiple zones. - Add extra user node pools with a unique zone and proximity placement group associated to each pool. An example is
*nodepool1*in zone one and PPG1,*nodepool2*in zone two and PPG2, and*nodepool3*in zone 3 with PPG3. This configuration ensures that, at a cluster level, nodes are spread across multiple zones and each individual node pool is colocated in the designated zone with a dedicated PPG resource.

## Create a new AKS cluster with a proximity placement group

Accelerated networking greatly improves networking performance of virtual machines. Ideally, use proximity placement groups with accelerated networking. By default, AKS uses accelerated networking on [supported virtual machine instances](/en-us/azure/virtual-network/accelerated-networking-overview?toc=/azure/virtual-machines/linux/toc.json#limitations-and-constraints), which include most Azure virtual machine with two or more vCPUs.

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location centralus`

Create a proximity placement group using the

command. Make sure to note the ID value in the output.`az ppg create`

`az ppg create --name myPPG --resource-group myResourceGroup --location centralus --type standard`

The command produces an output similar to the following example output, which includes the

*ID*value you need for upcoming CLI commands.`{ "availabilitySets": null, "colocationStatus": null, "id": "/subscriptions/yourSubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.Compute/proximityPlacementGroups/myPPG", "location": "centralus", "name": "myPPG", "proximityPlacementGroupType": "Standard", "resourceGroup": "myResourceGroup", "tags": {}, "type": "Microsoft.Compute/proximityPlacementGroups", "virtualMachineScaleSets": null, "virtualMachines": null }`

Create an AKS cluster using the

command and replace the`az aks create`

*myPPGResourceID*value with your proximity placement group resource ID from the previous step.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --ppg myPPGResourceID --generate-ssh-keys`


## Add a proximity placement group to an existing cluster

You can add a proximity placement group to an existing cluster by creating a new node pool. You can then optionally migrate existing workloads to the new node pool and delete the original node pool.

Use the same proximity placement group that you created earlier to ensure agent nodes in both node pools in your AKS cluster are physically located in the same data center.

Create a new node pool using the

command and replace the`az aks nodepool add`

*myPPGResourceID*value with your proximity placement group resource ID.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name mynodepool \ --node-count 1 \ --ppg myPPGResourceID`


## Clean up

Delete the Azure resource group along with its resources using the

command.`az group delete`

`az group delete --name myResourceGroup --yes --no-wait`


## Next steps

Learn more about [proximity placement groups](/en-us/azure/virtual-machines/co-location#proximity-placement-groups).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kubelogin-authentication -->

# Use kubelogin to authenticate users in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The kubelogin plugin in Azure is a client-go credential [plugin](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#client-go-credential-plugins) that implements Microsoft Entra authentication. The kubelogin plugin offers features that aren't available in the kubectl command-line tool. For more information, see the [kubelogin introduction](https://azure.github.io/kubelogin/index.html) and the [kubectl introduction](https://kubernetes.io/docs/reference/kubectl/introduction/).

This article provides an overview and examples of how to use kubelogin for all supported Microsoft Entra authentication methods in AKS.

## Kubelogin authentication in AKS limitations

- Groups that are created in Microsoft Entra are included only by their
**ObjectID**value, and not by their display name. The`sAMAccountName`

command is available only for groups that are synchronized from on-premises Windows Server Active Directory.

- The service principal authentication method works only with managed Microsoft Entra, and not with the earlier version Azure Active Directory.
- The service principal can be a member of a maximum of 200
[Microsoft Entra groups](/en-us/entra/identity/hybrid/connect/how-to-connect-fed-group-claims). If you have more than 200 groups, consider using[application roles](/en-us/entra/external-id/customers/how-to-use-app-roles-customers).

- The device code authentication method doesn't work when a Microsoft Entra Conditional Access policy is set on a Microsoft Entra tenant. In that scenario, use web browser interactive authentication instead.

- The Azure CLI authentication method works only with AKS managed Microsoft Entra.

## How authentication works

Note

Keep in mind the following information about kubelogin authentication for AKS clusters integrated with Microsoft Entra:

**Clusters running Kubernetes version 1.24 or later**automatically use the kubelogin format.**Clusters running Kubernetes 1.24 or earlier**require manual conversion. You can use the device code authentication method to convert the kubeconfig file to use the exec plugin format.

For most interactions with kubelogin, you use the `convert-kubeconfig`

subcommand. The subcommand uses the kubeconfig file that's specified in `--kubeconfig`

or in the `KUBECONFIG`

environment variable to convert the final kubeconfig file to exec format based on the specified authentication method.

The authentication methods that kubelogin implements are Microsoft Entra OAuth 2.0 token grant flows. In each authentication method, the token isn't cached on the file system.

## Device code authentication

Device code is the default authentication method for the `convert-kubeconfig`

subcommand. This authentication method prompts the device code for the user to sign in from a browser session.

Note

Before the kubelogin and exec plugins were introduced, the Azure authentication method in kubectl supported only the device code flow. It used an earlier version of a library that produces a token that has the `audience`

claim with an `spn:`

prefix. It isn't compatible with [AKS managed Microsoft Entra](managed-azure-ad), which uses an [on-behalf-of (OBO)](/en-us/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) flow. When you run the `convert-kubeconfig`

subcommand, kubelogin removes the `spn:`

prefix from the audience claim.

### Parameters for device code authentication

The following table outlines parameters that you can use with device code authentication:

| Parameter | Description |
|---|---|
`-l devicecode` (optional) |
Specifies the kubelogin authentication method. This parameter is optional because device code is the default method. |
`--legacy` |
Uses legacy behavior for earlier versions of Azure Active Directory clusters. If you're using the kubeconfig file in an earlier version Azure Active Directory cluster, kubelogin automatically adds the `--legacy` flag. |
`--token-cache-dir` |
Overrides the default path of the token cache directory, which is ${HOME}/.kube/cache/kubelogin. |

## Azure CLI authentication

The Azure CLI (command: `-l azurecli`

) authentication method uses the signed-in context that the Azure CLI establishes to get the access token. The token is issued in the same Microsoft Entra tenant as `az login`

. kubelogin doesn't write tokens to the token cache file because the Azure CLI already manages them.

### Parameters for Azure CLI authentication

The following table outlines parameters that you can use with Azure CLI authentication:

| Parameter | Description |
|---|---|
`-l azurecli` |
Specifies the kubelogin authentication method. |
`--azure-config-dir` |
Specifies the Azure CLI configuration directory. The default directory is ${HOME}/.azure. |

## Sign in to Azure

Sign in to Azure using the [ az login](/en-us/cli/azure/authenticate-azure-cli-interactively#interactive-login) command.

```
az login
```


## Web browser interactive authentication

The web browser interactive (command: `-l interactive`

) method of authentication automatically opens a web browser to sign in the user. After the user is authenticated, the browser redirects to the local web server using the verified credentials. This authentication method complies with Conditional Access policy.

You can use either a bearer token or a Proof-of-Possession (PoP) token with this authentication method.

### Parameters for bearer token authentication

The following table outlines parameters that you can use with bearer token authentication:

| Parameter | Description |
|---|---|
`-l interactive` |
Specifies the kubelogin authentication method. |
`--token-cache-dir` |
Overrides the default path of the token cache directory, which is ${HOME}/.kube/cache/kubelogin. |

### Parameters for PoP token authentication

The following table outlines parameters that you can use with PoP token authentication:

| Parameter | Description |
|---|---|
`-l interactive` |
Specifies the kubelogin authentication method. |
`--pop-enabled` |
Enables PoP token authentication. |
`--pop-claims` |
Specifies the PoP token claims in a key-value pair format. For example, `u=/ARM/ID/OF/CLUSTER` . |

## Service principal authentication

The service principal (command: `-l spn`

) authentication method uses a service principal to sign in the user. You can provide the credential by setting an environment variable or by using the credential in a command-line argument. The supported credentials that you can use are a password or a Personal Information Exchange (PFX) client certificate.

### Parameters for service principal authentication

The following table outlines parameters that you can use with service principal authentication:

| Parameter | Description |
|---|---|
`-l spn` |
Specifies the kubelogin authentication method. |
`--client-id` |
The application ID (client-id) of the service principal. |
`--client-secret` |
The client secret of the service principal. |

## Managed identity authentication

Use the [managed identity](/en-us/entra/identity/managed-identities-azure-resources/overview) (command: `-l msi`

) authentication method for applications that connect to resources that support Microsoft Entra authentication. Examples include accessing Azure resources like an Azure virtual machine (VM), a virtual machine scale set, or Azure Cloud Shell.

You can use the default managed identity that's assigned to the resource or a specific user-assigned managed identity.

### Parameters for managed identity authentication

The following table outlines parameters that you can use with managed identity authentication:

| Parameter | Description |
|---|---|
`-l msi` |
Specifies the kubelogin authentication method. |
`--client-id` |
The application ID (client-id) of the user-assigned managed identity. If you don't specify this parameter, the default managed identity is used. |

## Workload identity authentication

The workload identity (command: `-l workloadidentity`

) authentication method uses identity credentials that are federated with Microsoft Entra to authenticate access to AKS clusters. The method uses Microsoft Entra integrated authentication. It works by setting the following environment variables:

| Variable | Description |
|---|---|
`AZURE_CLIENT_ID` |
The Microsoft Entra application ID that is federated with the workload identity. |
`AZURE_TENANT_ID` |
The Microsoft Entra tenant ID. |
`AZURE_FEDERATED_TOKEN_FILE` |
The file that contains a signed assertion of the workload identity, like a Kubernetes projected service account (JWT) token. |
`AZURE_AUTHORITY_HOST` |
The base URL of a Microsoft Entra authority. For example, `https://login.microsoftonline.com/` . |

You can use a [workload identity](/en-us/entra/workload-id/workload-identities-overview) to access Kubernetes clusters from CI/CD systems like GitHub or ArgoCD without storing service principal credentials in the external systems. To configure OpenID Connect (OIDC) federation from GitHub, see the [OIDC federation example](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-azure).

### Parameters for workload identity authentication

The following table outlines parameters that you can use with workload identity authentication:

| Parameter | Description |
|---|---|
`-l workloadidentity` |
Specifies the kubelogin authentication method. |

## Export the kubeconfig file path

Before you run the `convert-kubeconfig`

subcommand, export the kubeconfig file path to the `KUBECONFIG`

environment variable. For example:

```
export KUBECONFIG=/path/to/kubeconfig
```


## Convert the kubeconfig file

Run the `convert-kubeconfig`

subcommand to convert the kubeconfig file to use the exec plugin for your chosen authentication method.

```
kubelogin convert-kubeconfig
```


```
kubelogin convert-kubeconfig -l azurecli
```


```
# Bearer token authentication
kubelogin convert-kubeconfig -l interactive
# Proof-of-Possession (PoP) token authentication
kubelogin convert-kubeconfig -l interactive --pop-enabled --pop-claims "u=/ARM/ID/OF/CLUSTER"
```


-
[Use environment variables](#tabpanel_1_environment-variables) -
[Use command-line arguments](#tabpanel_1_command-line-arguments) -
[Use a client certificate](#tabpanel_1_client-certificate) -
[Use a PoP token with environment variables](#tabpanel_1_pop-token-environment-variables)

Run the

`convert-kubeconfig`

subcommand to convert the kubeconfig file to use the exec plugin.`kubelogin convert-kubeconfig -l spn`

Set the environment variables for the client ID and client secret or client certificate. For example:

`export AZURE_CLIENT_ID=<service-principal-client-id> export AZURE_CLIENT_SECRET=<service-principal-client-secret>`


```
# Default managed identity authentication
kubelogin convert-kubeconfig -l msi
# Specific managed identity authentication
kubelogin convert-kubeconfig -l msi --client-id <managed-identity-client-id>
```


```
kubelogin convert-kubeconfig -l workloadidentity
```


## Remove cached tokens

Remove cached tokens using the `kubelogin remove-tokens`

command.

```
kubelogin remove-tokens
```


## Get node information

Get node information using the `kubectl get`

command.

```
kubectl get nodes
```


## How to use kubelogin with AKS

AKS uses a pair of first-party Microsoft Entra applications. These application IDs are the same in all environments.

The AKS Microsoft Entra server application ID (server-id) that the server side uses is `6dae42f8-4368-4678-94ff-3960e28e3630`

. The access token that accesses AKS clusters must be issued for this application. In most kubelogin authentication methods, you must use `--server-id`

with `kubelogin get-token`

.

The AKS Microsoft Entra client application ID (client-id) that kubelogin uses to perform public client authentication on behalf of the user is `80faf920-1908-4b52-b5ef-a8e7bedfc67a`

. The client application ID is used in device code and web browser interactive authentication methods.

## Related content

- Learn how to integrate AKS with Microsoft Entra in the
[AKS managed Microsoft Entra integration](managed-azure-ad)how-to article. - To get started with managed identities in AKS, see
[Use a managed identity in AKS](use-managed-identity). - To get started with workload identities in AKS, see
[Use a workload identity in AKS](workload-identity-overview).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/customize-resource-configuration -->

# Customize the resource configuration for managed add-ons

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of how to customize the resource configuration for Azure Kubernetes Service (AKS) managed add-ons with [cost optimized add-on scaling (Preview)](optimized-addon-scaling).

## Overview

Enabling the cost optimized add-on scaling feature in your AKS cluster installs the Vertical Pod Autoscaler (VPA) add-on and VPA custom resources for AKS managed add-ons that support this capability. This feature also allows you to manually customize the resource CPU and memory requests and limits in Deployments and DaemonSets. You can also customize the maximum and minimum allowed CPU and memory and the VPA update mode within VPA custom resources.

## Prerequisites

- Review the
[supported AKS managed add-ons](optimized-addon-scaling#supported-aks-add-ons)and[limitations](optimized-addon-scaling)for this feature. - You need an AKS cluster enabled with the cost optimized add-on scaling feature. If you don't have one, see
[Enable cost optimized add-on scaling on your AKS cluster (Preview)](optimized-addon-scaling).

## Customize resource annotations

| Annotation | Description | Values |
|---|---|---|
`kubernetes.azure.com/override-requests-limits` |
Supports the capability to customize the container resource CPU/memory requests/limits in a Deployment or DaemonSet if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. | "enabled" or "disabled" |
`kubernetes.azure.com/override-min-max` |
Supports the capability to customize the container policy maximum/minimum allowed CPU/memory value in VPA custom resource if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. | "enabled" or "disabled" |
`kubernetes.azure.com/override-update-mode` |
Supports the capability to customize the update policy `updateMode` value in a VPA custom resource if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. |
"enabled" or "disabled" |

## Customize resource CPU/memory requests/limits

After setting the `kubernetes.azure.com/override-requests-limits`

annotation to "enabled" in a Deployment or DaemonSet, you can customize the resource CPU/memory requests and limits. The following example shows how to customize the resource CPU/memory requests and limits in a Deployment:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-requests-limits: "enabled"
spec:
...
containers:
- name: coredns
resources:
limits:
# update cpu limits value won't be reconciled back
cpu: "3"
# update memory limits value won't be reconciled back
memory: "500Mi"
requests:
# update cpu requests value won't be reconciled back
cpu: "100m"
# update memory requests value won't be reconciled back
memory: "70Mi"
```


## Customize resource maximum/minimum allowed CPU/memory

After setting the `kubernetes.azure.com/override-min-max`

annotation to "enabled" in a VPA custom resource, you can customize the maximum and minimum allowed CPU and memory values in a VPA custom resource. The following example shows how to customize the maximum and minimum allowed CPU and memory values in a VPA custom resource:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-min-max: "enabled"
spec:
resourcePolicy:
containerPolicies:
- containerName: coredns
maxAllowed:
# update maxAllowed cpu value won't be reconciled back
cpu: 3
# update maxAllowed memory value won't be reconciled back
memory: 500Mi
minAllowed:
# update minAllowed cpu value won't be reconciled back
cpu: 10m
# update minAllowed memory value won't be reconciled back
memory: 10Mi
...
```


## Customize resource update mode

After setting the `kubernetes.azure.com/override-update-mode`

annotation to "enabled" in a VPA custom resource, you can customize the update policy `updateMode`

value in a VPA custom resource to "Off" or "Initial" (default). The following example shows how to customize the update policy `updateMode`

value to "Initial" in a VPA custom resource:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-update-mode: "enabled"
spec:
...
updatePolicy:
# update updateMode won't be reconciled back
updateMode: "Initial"
```


## Disable VPA on a specific AKS managed add-on

To disable VPA on a specific AKS managed add-on, you need to update the VPA custom resource YAML file to set the `kubernetes.azure.com/override-update-mode`

annotation to `"enabled"`

and the `updateMode`

to `"Off"`

. With *Off* mode, the VPA only provides CPU and memory recommendations and doesn't apply the changes to the pod.

The following example shows how to disable VPA on the CoreDNS add-on:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# Set value to "enabled"
kubernetes.azure.com/override-update-mode: "enabled"
spec:
...
updatePolicy:
# Set value to "Off"
updateMode: "Off"
```


## Troubleshooting

- Make sure the AKS managed add-on supports the cost optimized add-on scaling feature. For more information, see
[Supported AKS managed add-ons](optimized-addon-scaling#supported-aks-add-ons). - Verify that the
`kubernetes.azure.com/override-requests-limits`

annotation in the Deployment or DaemonSet is set to "enabled". - Verify that the
`kubernetes.azure.com/override-min-max`

annotation in the VPA custom resource is set to "enabled". - Verify that the
`kubernetes.azure.com/override-update-mode`

annotation in the VPA custom resource is set to "enabled".

## Next steps

To further configure cluster resource utilization and free up CPU/memory for AKS managed add-on pods, see [Vertical pod autoscaling in AKS](vertical-pod-autoscaler).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/localdns-custom -->

# Configure LocalDNS in Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

LocalDNS is a feature in Azure Kubernetes Service (AKS) designed to enhance the Domain Name System (DNS) resolution performance and resiliency for workloads running in your cluster. When you deploy a DNS proxy on each node, LocalDNS reduces DNS query latency, improves reliability during network disruptions, and provides advanced configuration options for DNS caching and forwarding. This article explains how LocalDNS works, its configuration options, and how to enable, verify, and troubleshoot LocalDNS in your AKS clusters.

To learn about what LocalDNS is, including architecture details, and key capabilities, refer to [DNS Resolution in Azure Kubernetes Service (AKS)](dns-concepts).

## Best practices for LocalDNS configuration

When implementing LocalDNS in your AKS clusters, consider the following best practices:

**Start with a minimal configuration**: Begin with a simple configuration that uses the`Preferred`

mode before moving to`Required`

mode. This setup allows you to validate that LocalDNS works as expected without breaking your cluster.**Implement proper caching strategies**: Configure cache settings based on your workload characteristics:- For frequently changing records, use shorter
`cacheDurationInSeconds`

values. When doing so, it's important to note that cacheDurationInSeconds acts as a cap on the DNS record TTL but doesn't increase it. The resulting TTL is the smaller of what is returned from upstream or what is set in the cache plugin. - For stable records, use longer cache durations to reduce DNS queries.
- Enable
`serveStale`

with appropriate settings to maintain service during DNS outages. - Caching with LocalDNS operates on a best effort basis and doesn't guarantee stale responses. The cache is divided into 256 shards and with a default maximum of 10,000 entries, allowing each shard to hold about 39 entries. When a shard is full and a new entry needs to be added, one of the existing entries is chosen at random to be evicted. There's no preference for older or expires entries. As a result, a stale record might not always be available, especially under high query volume.

- For frequently changing records, use shorter
**Monitor DNS performance**: After enabling LocalDNS, monitor your application's DNS performance using:- Application performance metrics.
- Node metrics to detect reduced network pressure.
- Log entries when
`queryLogging`

is set to`Log`

.

**Follow least privilege principle**: When configuring DNS forwarding rules, only allow access to the required DNS servers and domains.**Test before production deployment**: Always test LocalDNS configuration in a nonproduction environment before rolling it out to production clusters.**Use Infrastructure as Code (IaC)**: Store your*localdnsconfig.json*file in your infrastructure repository and include it in your AKS deployment templates.**Network configuration for TCP forwarding**: When using TCP for DNS forwarding to VNetDNS, ensure that your Network Security Groups (NSGs), firewalls, or Network Virtual Appliances (NVAs) don't block TCP traffic between CoreDNS/LocalDNS and VNetDNS servers.**Avoid enabling both NodeLocal DNSCache and LocalDNS**: It isn't recommended to enable both the upstream Kubernetes NodeLocal DNSCache and LocalDNS in your node pool. While AKS doesn't block this configuration, all DNS traffic is routed through LocalDNS, which might lead to unexpected behavior or reduced benefits from NodeLocal DNSCache.

## Prerequisites

You must have an existing AKS cluster with Kubernetes versions 1.31 and later to use LocalDNS. If you need an AKS cluster, you can create one using

[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal).This article requires Azure CLI version 2.80.0 and later. If you're using Azure Cloud Shell, the latest version is already installed.

LocalDNS is only supported on node pools running Azure Linux or Ubuntu 22.04 and newer.

The Virtual Machine (VM) SKU used for your node pool must have at least 4 vCPUs (cores) to support LocalDNS.

LocalDNS isn't compatible with applied Fully Qualified Domain Names (FQDN) filter policies in

[Advanced Container Networking Services (ACNS)](how-to-apply-fqdn-filtering-policies).

## Manage LocalDNS on an AKS cluster

LocalDNS is configured at the node pool level in AKS, meaning you can enable or disable LocalDNS independently for each node pool in your cluster. This tailors DNS resolution behavior based on the specific requirements of different workloads or environments. To enable LocalDNS on a node pool, you need to provide a configuration file: *localdnsconfig.json* that defines how LocalDNS should operate for that node pool.

If you don't specify a custom configuration file, AKS automatically applies a default LocalDNS configuration.

Note

If you're using Node Auto-Provisioning (NAP), see [LocalDNS configuration](node-auto-provisioning-aksnodeclass#localdns-configuration) for instructions on how to enable LocalDNS with NAP.

To enable LocalDNS during node pool creation, use the following command with your custom configuration file:

```
az aks nodepool add --name mynodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --localdns-config ./localdnsconfig.json
```


To enable LocalDNS on an existing node pool, use the following command with your custom configuration file:

```
az aks nodepool update --name mynodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --localdns-config ./localdnsconfig.json
```


Important

Enabling LocalDNS on a node pool initiates a reimage operation on all nodes within that pool. This process can cause temporary disruption to running workloads and might lead to application downtime if not properly managed. You should plan for potential service interruptions and ensure that the applications are configured for high availability or have appropriate disruption budgets in place before enabling this setting.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-cni-powered-by-cilium -->

# Configure Azure CNI Powered by Cilium in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure CNI Powered by Cilium combines the robust control plane of Azure Container Networking Interface (CNI) with the data plane of [Cilium](https://cilium.io/) to provide high-performance networking and security.

Azure CNI Powered by Cilium provides the following benefits by making use of eBPF programs loaded into the Linux kernel and a more efficient API object structure:

- Functionality equivalent to existing Azure CNI and Azure CNI Overlay plugins
- Improved service routing
- More efficient network policy enforcement
- Better observability of cluster traffic
- Support for larger clusters (more nodes, pods, and services)

## IP Address Management (IPAM) with Azure CNI Powered by Cilium

You can deploy Azure CNI Powered by Cilium with two different methods for assigning pod IPs:

- Assign IP addresses from an overlay network (similar to Azure CNI Overlay mode)
- Assign IP addresses from a virtual network (similar to existing Azure CNI with Dynamic Pod IP Assignment)

If you aren't sure which option to select, read [Choose a network model](concepts-network-azure-cni-overlay#choose-a-network-model)

## Versions

| Kubernetes Version | Minimum Cilium Version |
|---|---|
| 1.29 (LTS) | 1.14.19 |
| 1.30 | 1.14.19 |
| 1.31 | 1.16.6 |
| 1.32 | 1.17.0 |
| 1.33 | 1.17.0 |

For more information on AKS versioning and release timelines, see [Supported Kubernetes Versions](supported-kubernetes-versions).

## Network Policy Enforcement

Cilium enforces [network policies to allow or deny traffic between pods](operator-best-practices-network#control-traffic-flow-with-network-policies). With Cilium, you don't need to install a separate network policy engine such as Azure Network Policy Manager or Calico.

## Local Redirect Policy (LRP)

LRP starts to be supported from Kubernetes v1.29 and up, Cilium v1.14 and up. For LRP to work with Advanced Container Networking Services (ACNS) - FQDN Filtering, the Cilium Network Policy egress labels need to match with node-local DNS cache pod labels.

## Limitations

Azure CNI powered by Cilium currently has the following limitations:

- Available only for Linux and not for Windows.
- Network policies can't use
`ipBlock`

to allow access to node or pod IPs. For details and recommended workarounds, see[frequently asked questions](#frequently-asked-questions). - For Cilium versions 1.16 or earlier, multiple Kubernetes services can't use the same host port with different protocols (for example, TCP or UDP) (
[Cilium issue #14287](https://github.com/cilium/cilium/issues/14287)). - Network policies aren't applied to pods using host networking (
`spec.hostNetwork: true`

) because these pods use the host identity instead of having individual identities. - Cilium Endpoint Slices are supported in Kubernetes version 1.32 and above. Cilium Endpoint Slices don't support configuration of how Cilium Endpoints are grouped. Priority namespace through
`cilium.io/ces-namespace`

isn't supported. - L7 policy isn't supported by
`CiliumClusterwideNetworkPolicy`

(CCNP). - Cilium uses Cilium identities as unique identity for provisioning endpoints, so high-churning workloads such as Spark jobs generate high count of Cilium identities. To avoid workloads hitting Cilium identity limits (65535), excluding Spark job's labels like
`!spark-app-name`

and`!spark-app-selector`

in the Cilium configmap can significantly reduce Cilium identity generation. For more details on Cilium identity exclusion rules, check[the official Cilium label documentation](https://docs.cilium.io/en/stable/operations/performance/scalability/identity-relevant-labels/#excluding-labels). - AKS Local DNS isn't compatible with Advanced Container Networking Services (ACNS) - FQDN Filtering.

## Considerations

To gain capabilities such as observability into your network traffic and security features like Fully Qualified Domain Name (FQDN) based filtering and Layer 7 based network policies on your cluster, consider enabling [Advanced Container Networking services](advanced-container-networking-services-overview) on your clusters.

## Prerequisites

- Azure CLI version 2.48.1 or later. Run
`az --version`

to see the currently installed version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you're using ARM templates or the REST API, the AKS API version must be
`2022-09-02-preview`

or later.

Previous AKS API versions (`2022-09-02preview`

to `2023-01-02preview`

) used the field [ networkProfile.ebpfDataplane=cilium](https://github.com/Azure/azure-rest-api-specs/blob/06dbe269f7d9c709cc225c92358b38c3c2b74d60/specification/containerservice/resource-manager/Microsoft.ContainerService/aks/preview/2022-09-02-preview/managedClusters.json#L6939-L6955). AKS API versions since

`2023-02-02preview`

use the field [to enable Azure CNI Powered by Cilium.](https://github.com/Azure/azure-rest-api-specs/blob/06dbe269f7d9c709cc225c92358b38c3c2b74d60/specification/containerservice/resource-manager/Microsoft.ContainerService/aks/preview/2023-02-02-preview/managedClusters.json#L7152-L7173)

`networkProfile.networkDataplane=cilium`

## Create a new AKS Cluster with Azure CNI Powered by Cilium

The following sections use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command to create a cluster and assign IP addresses.

### Option 1: Assign IP addresses from an overlay network

Use the following commands to create a cluster with an overlay network and Cilium. Replace the values for `<clusterName>`

, `<resourceGroupName>`

, and `<location>`

:

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--network-plugin azure \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16 \
--network-dataplane cilium \
--generate-ssh-keys
```


The `--network-dataplane cilium`

flag replaces the deprecated `--enable-ebpf-dataplane`

flag used in earlier versions of the aks-preview CLI extension.

### Option 2: Assign IP addresses from a virtual network

Run the following commands to create a resource group and virtual network with a subnet for nodes and a subnet for pods.

```
# Create the resource group
az group create --name <resourceGroupName> --location <location>
```


```
# Create a virtual network with a subnet for nodes and a subnet for pods
az network vnet create --resource-group <resourceGroupName> --location <location> --name <vnetName> --address-prefixes <address prefix, example: 10.0.0.0/8> -o none
az network vnet subnet create --resource-group <resourceGroupName> --vnet-name <vnetName> --name nodesubnet --address-prefixes <address prefix, example: 10.240.0.0/16> -o none
az network vnet subnet create --resource-group <resourceGroupName> --vnet-name <vnetName> --name podsubnet --address-prefixes <address prefix, example: 10.241.0.0/16> -o none
```


Create the cluster using `--network-dataplane cilium`

:

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--max-pods 250 \
--network-plugin azure \
--vnet-subnet-id /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.Network/virtualNetworks/<vnetName>/subnets/nodesubnet \
--pod-subnet-id /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.Network/virtualNetworks/<vnetName>/subnets/podsubnet \
--network-dataplane cilium \
--generate-ssh-keys
```


### Option 3: Assign IP addresses from the Node Subnet

Azure CLI version 2.69.0 or later is required. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Create a cluster using [node subnet](concepts-network-legacy-cni#azure-cni-node-subnet) with a Cilium data plane:

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--network-plugin azure \
--network-dataplane cilium \
--generate-ssh-keys
```


## Frequently asked questions

**Can I customize Cilium configuration?**No, AKS manages the Cilium configuration and it can't be modified. We recommend that customers who require more control use

[AKS BYO CNI](use-byo-cni)and install Cilium manually.**Can I use**`CiliumNetworkPolicy`

custom resources instead of Kubernetes`NetworkPolicy`

resources?L3 and L4

`CiliumNetworkPolicy`

are supported and can be used alongside Kubernetes`NetworkPolicy`

resources.Customers might use FQDN filtering and Layer 7 policies as part of the

[Advanced Container Networking Services](advanced-container-networking-services-overview)feature bundle.**Can I use**`CiliumClusterwideNetworkPolicy`

?Yes,

`CiliumClusterwideNetworkPolicy`

is supported. The following sample policy YAML shows configuring an L4 rule:`apiVersion: "cilium.io/v2" kind: CiliumClusterwideNetworkPolicy metadata: name: "l4-rule-ingress-backend-frontend" spec: endpointSelector: matchLabels: role: backend ingress: - fromEndpoints: - matchLabels: role: frontend toPorts: - ports: - port: "80" protocol: TCP`

**Which Cilium features are supported in Azure managed CNI? Which of those require Advanced Container Networking Services?**Supported Feature w/o ACNS w/ ACNS Cilium Endpoint Slices ✔️ ✔️ K8s Network Policies ✔️ ✔️ Cilium L3/L4 Network Policies ✔️ ✔️ Cilium Clusterwide Network Policy ✔️ ✔️ FQDN Filtering ❌ ✔️ L7 Network Policies (HTTP/gRPC/Kafka) ❌ ✔️ Container Network Observability (Metrics and Flow logs) ❌ ✔️ eBPF Host Routing ❌ ✔️ **Why is traffic being blocked when the**`NetworkPolicy`

has an`ipBlock`

that allows the IP address?A limitation of Azure CNI Powered by Cilium is that a

`NetworkPolicy`

`ipBlock`

can't select pod or node IPs.For example, this

`NetworkPolicy`

has an`ipBlock`

that allows all egress to`0.0.0.0/0`

:`apiVersion: networking.k8s.io/v1 kind: NetworkPolicy metadata: name: example-ipblock spec: podSelector: {} policyTypes: - Egress egress: - to: - ipBlock: cidr: 0.0.0.0/0 # This will still block pod and node IPs.`

However, when this

`NetworkPolicy`

is applied, Cilium blocks egress to pod and node IPs even though the IPs are within the`ipBlock`

CIDR.As a workaround, you can add

`namespaceSelector`

and`podSelector`

to select pods. This example selects all pods in all namespaces:`apiVersion: networking.k8s.io/v1 kind: NetworkPolicy metadata: name: example-ipblock spec: podSelector: {} policyTypes: - Egress egress: - to: - ipBlock: cidr: 0.0.0.0/0 - namespaceSelector: {} - podSelector: {}`

It isn't currently possible to specify a

`NetworkPolicy`

with an`ipBlock`

to allow traffic to node IPs.**Does AKS configure CPU or memory limits on the Cilium**`daemonset`

?No, AKS doesn't configure CPU or memory limits on the Cilium

`daemonset`

because Cilium is a critical system component for pod networking and network policy enforcement.**Does Azure CNI powered by Cilium use kube-proxy?**No, AKS clusters created with network data plane as Cilium don't use

`kube-proxy`

. If the AKS clusters are on[Azure CNI Overlay](azure-cni-overlay)or[Azure CNI with dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)and are upgraded to AKS clusters running Azure CNI powered by Cilium, new nodes workloads are created without`kube-proxy`

. Older workloads are also migrated to run without`kube-proxy`

as a part of this upgrade process.

## Dual-stack networking with Azure CNI Powered by Cilium

You can deploy your dual-stack AKS clusters with Azure CNI Powered by Cilium. This feature also allows you to control your IPv6 traffic with the Cilium Network Policy engine.

You must have Kubernetes version 1.29 or greater.

### Set up Overlay clusters with Azure CNI Powered by Cilium

Create a cluster with Azure CNI Overlay using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command. Make sure to use the argument

`--network-dataplane cilium`

to specify the Cilium data plane.```
clusterName="myOverlayCluster"
resourceGroup="myResourceGroup"
location="westcentralus"
az aks create \
--name $clusterName \
--resource-group $resourceGroup \
--location $location \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--ip-families ipv4,ipv6 \
--generate-ssh-keys
```


## Next steps

Learn more about networking in AKS in the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-best-practices -->

# Best practices for Windows containers on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In AKS, you can create node pools that run Linux or Windows Server as the operating system (OS) on the nodes. Windows Server nodes can run native Windows container applications, such as .NET Framework. The Linux OS and Windows OS have different container support and configuration considerations. For more information, see [Windows container considerations in Kubernetes](windows-vs-linux-containers). To learn more about how various industries are using Windows containers on AKS, see [Windows AKS customer stories](windows-aks-customer-stories).

This article outlines best practices for running Windows containers on AKS.

## Create an AKS cluster with Linux and Windows node pools

When you create a new AKS cluster, the Azure platform creates a Linux node pool by default. This node pool contains system services needed for the cluster to function. Azure also creates and manages a control plane abstracted from the user, which means you aren't exposed to the underlying OS of the nodes hosting the main control plane components. We recommend that you run at least *two nodes* on the default Linux node pool to ensure the reliability and performance of your cluster. You can't delete the default Linux node pool unless you delete the entire cluster.

There are some cases where you should consider deploying a Linux node pool when planning to run Windows-based workloads on your AKS cluster, such as:

- If you want to run Linux and Windows workloads, you can deploy a Linux node pool and a Windows node pool in the same cluster.
- If you want to deploy infrastructure-related components based on Linux, such as NGINX, you need a Linux node pool alongside your Windows node pool. You can use control plane nodes for development and testing scenarios. For production workloads, we recommend that you deploy separate Linux node pools to ensure reliability and performance.

## Modernize existing applications with Windows on AKS

You might want to containerize existing applications and run them using Windows on AKS. Before starting the containerization process, it's important to understand the application architecture and dependencies. For more information, see [Containerize existing applications using Windows containers](/en-us/virtualization/windowscontainers/quick-start/lift-shift-to-containers).

## Windows OS version


Best practice guidanceWindows Server 2022 provides improved security and performance and is the recommended OS for Windows node pools on AKS. AKS uses Windows Server 2022 as the host OS version and only supports process isolation.


AKS supports two options for the Windows Server operating system: Long Term Servicing Channel Releases (LTSC) and Windows Server Annual Channel for Containers.

AKS supports Long Term Servicing Channel Releases (LTSC), including Windows Server 2025 (preview), Windows Server 2022, and Windows Server 2019. This channel is released every three years and is supported for five years. Customers using Long Term Support (LTS) should use Windows Server 2022.

AKS uses Windows Server 2019 and Windows Server 2022 as the host OS versions and only supports process isolation. AKS doesn't support container images built by other versions of Windows Server. For more information, see

[Windows container version compatibility](/en-us/virtualization/windowscontainers/deploy-containers/version-compatibility). Windows Server 2022 is the default OS for Kubernetes version 1.25 and later.Note

[Windows Server 2019 retires on March 1, 2026](https://github.com/Azure/AKS/issues/4091). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2019 on any Kubernetes version. All existing node pools with Windows Server 2019 will be unsupported. Windows Server 2019 is not supported in Kubernetes version 1.33 and above. Starting on April 1, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail.[Windows Server 2022 retires on March 15, 2027](https://github.com/Azure/AKS/issues/4168). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2022 on any Kubernetes version. All existing node pools with Windows Server 2022 will be unsupported. Windows Server 2022 is not supported in Kubernetes version 1.36 and above. Starting on April 1, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail.

For more information, see

[AKS release notes](https://github.com/Azure/AKS/releases). To stay up to date on the latest Windows Server OS versions and learn more about our roadmap of what's planned for support on AKS, see our[AKS public roadmap](https://github.com/azure/aks/projects/1).AKS supports

[Windows Server Annual Channel for Containers](https://techcommunity.microsoft.com/t5/windows-server-news-and-best/windows-server-annual-channel-for-containers/ba-p/3866248)(preview). This channel is released annually and is supported for two years. This channel is beneficial for customers requiring increased innovation cycles and portability. The portability functionality enables the Windows Server 2022-based container image OS to run on newer versions of Windows Server host OS, such as the new annual channel release.Windows Annual Channel versions are based on the Kubernetes version of your node pool. To upgrade from one Annual Channel version to the next,

[upgrade to a Kubernetes version](upgrade-aks-cluster)that supports the next Annual Channel version. For more information, see[Windows Server Annual Channel for Containers on AKS](windows-annual-channel).

## Monitoring


Best practice guidanceWindows Exporter is installed on all Windows nodes in certain regions. To view regional rollout, see

[AKS Github]. With Managed Prometheus and Grafana, you can monitor default collectors included in Windows Exporter on AKS. For more information, see[default Prometheus metrics configured in Azure Monitor].

Windows Exporter allows customers to see their metrics through Managed Prometheus or Prometheus OSS deployments and enjoy enhanced observability around their node and pod performance, health, and resource usage. These metrics are also visible with Managed Grafana.

- When enabling managed prometheus, add this required parameter for correct dashboard data presentation for Windows:
`--enable-windows-recording-rules`

. - Grafana includes dashboards for showing Windows resources, such as:
- Kubernetes / Compute Resources / Cluster (Windows)
- Kubernetes / Compute Resources / Namespace (Windows)
- Kubernetes / Compute Resources / Pod (Windows)
- Kubernetes / USE Method / Cluster (Windows)
- Kubernetes / USE Method / Node (Windows)


The default collectors included in Windows Exporter on AKS are: cpu, cpu_info, cs, container, logical_disk, memory, net, os, process, service, system, textfile. The metrics are exposed on port **19182** on the windows node. For more information on what metrics you can see using these collectors, please see [prometheus-community/windows_exporter](https://github.com/prometheus-community/windows_exporter#collectors).

## Networking

### Networking modes


Best practice guidanceAKS clusters with Windows node pools only support Azure Container Networking Interface (Azure CNI) and use it by default.


Windows doesn't support kubenet networking. AKS clusters with Windows node pools must use Azure CNI. For more information, see [Network concepts for applications in AKS](concepts-network).

Azure CNI offers two networking modes based on your workload requirements:

is an overlay network similar to kubenet. The overlay network allows you to use virtual network (VNet) IPs for nodes and private address spaces for pods within those nodes that you can reuse across the cluster. Azure CNI Overlay is the**Azure CNI Overlay****recommended networking mode**. It provides simplified network configuration and management and the best scalability in AKS networking.requires extra planning and consideration for IP address management. This mode provides VNet IPs for nodes**Azure CNI with Dynamic IP Allocation***and*pods. This configuration allows you direct access to pod IPs. However, it comes with increased complexity and reduced scalability.

To help you decide which networking mode to use, see [Choosing a network model](concepts-network-azure-cni-overlay#choose-a-network-model).

### Network policies


Best practice guidanceUse network policies to secure traffic between pods. Windows supports Azure Network Policy Manager and Calico Network Policy. For more information, see

[Differences between Network Policy engines: Cilium, Azure NPM, and Calico].

When managing traffic between pods, you should apply the principle of least privilege. The Network Policy feature in Kubernetes allows you to define and enforce ingress and egress traffic rules between the pods in your cluster. For more information, see [Secure traffic between pods using network policies in AKS](use-network-policies).

Windows pods on AKS clusters that use the Calico Network Policy enable Floating IP by default.

## Upgrades and updates

It's important to keep your Windows environment up-to-date to ensure your systems have the latest security updates, feature sets, and compliance requirements. In a Kubernetes environment like AKS, you need to maintain the Kubernetes version, Windows nodes, and Windows container images and pods.

### Kubernetes version upgrades

As a managed Kubernetes service, AKS provides the necessary tools to upgrade your cluster to the latest Kubernetes version. For more information, see [Upgrade an AKS cluster](upgrade-cluster).

### Windows node monthly updates

Windows nodes on AKS follow a monthly update schedule. Every month, AKS creates a new VHD with the latest available updates for Windows node pools. The VHD includes the host image, latest Nano Server image, latest Server Core image, and container. We recommend performing monthly updates to your Windows node pools to ensure your nodes have the latest security patches. For more information, see [Upgrade AKS node images](node-image-upgrade).

Note

Upgrades on Windows systems include both OS version upgrades and monthly node OS updates.

You can stay up to date with the availability of new monthly releases using the [AKS release tracker](https://releases.aks.azure.com/) and [AKS release notes](https://github.com/Azure/AKS/releases).

### Windows node OS version upgrades

Windows has a release cadence for new versions of the OS, including Windows Server 2025 (preview), Windows Server 2022, and Windows Server 2019. When upgrading your Windows node OS version, ensure the Windows container image version matches the Windows container host version and the node pools have only one version of Windows Server.

To upgrade the Windows node OS version, you need to complete the following steps:

- Create a new node pool with the new Windows Server version.
- Deploy your workloads with the new Windows container images to the new node pool.
- Decommission the old node pool.

For more information, see [Upgrade Windows Server workloads on AKS](upgrade-windows-2019-2022).

Note

Windows announced a new [Windows Server Annual Channel for Containers](https://techcommunity.microsoft.com/t5/windows-server-news-and-best/windows-server-annual-channel-for-containers/ba-p/3866248) that supports portability and mixed versions of Windows nodes and containers. This feature isn't yet supported in AKS.

To track AKS feature plans, see the [Public AKS roadmap](https://github.com/Azure/AKS/projects/1#card-90806240).

## Next steps

To learn more about Windows containers on AKS, see the following resources:

[Learn how to deploy, manage, and monitor Windows containers on AKS](/en-us/training/paths/deploy-manage-monitor-wincontainers-aks).- Open an issue or provide feedback in the
[Windows containers GitHub repository](https://github.com/microsoft/Windows-Containers/issues). - Review the
[third-party partner solutions for Windows on AKS](windows-aks-partner-solutions).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/start-stop-cluster -->

# Stop and start an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You may not need to continuously run your Azure Kubernetes Service (AKS) workloads. For example, you may have a development cluster that you only use during business hours. This means there are times where your cluster might be idle, running nothing more than the system components. You can reduce the cluster footprint by [scaling all User node pools to 0](scale-cluster#scale-user-node-pools-to-0), but your

[is still required to run the system components while the cluster is running.](use-system-pools)

`System`

poolTo better optimize your costs during these periods, you can turn off, or stop, your cluster. This action stops your control plane and agent nodes, allowing you to save on all the compute costs, while maintaining all objects except standalone pods. The cluster state is stored for when you start it again, allowing you to pick up where you left off.

Caution

Stopping your cluster deallocates the control plane and releases the capacity. In regions experiencing capacity constraints, customers may be unable to start a stopped cluster. We do not recommend stopping mission critical workloads for this reason.

Note

AKS start operations will restore all objects from ETCD with the exception of standalone pods with the same names and ages. meaning that a pod's age will continue to be calculated from its original creation time. This count will keep increasing over time, regardless of whether the cluster is in a stopped state.

## Before you begin

This article assumes you have an existing AKS cluster. If you need an AKS cluster, you can create one using [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

### About the cluster stop/start feature

When using the cluster stop/start feature, the following conditions apply:

- This feature is only supported for Virtual Machine Scale Set backed clusters.
- You can't stop clusters which use the
[Node Autoprovisioning (NAP)](node-autoprovision)feature. - The cluster state of a stopped AKS cluster is preserved for up to 12 months. If your cluster is stopped for more than 12 months, you can't recover the state. For more information, see the
[AKS support policies](support-policies). - You can only perform start or delete operations on a stopped AKS cluster. To perform other operations, like scaling or upgrading, you need to start your cluster first.
- If you provisioned PrivateEndpoints linked to private clusters, they need to be deleted and recreated again when starting a stopped AKS cluster.
- Because the stop process drains all nodes, any standalone pods (i.e. pods not managed by a Deployment, StatefulSet, DaemonSet, Job, etc.) will be deleted.
- When you start your cluster back up, the following behavior is expected:
- The IP address of your API server may change.
- If you're using cluster autoscaler, when you start your cluster, your current node count may not be between the min and max range values you set. The cluster starts with the number of nodes it needs to run its workloads, which isn't impacted by your autoscaler settings. When your cluster performs scaling operations, the min and max values will impact your current node count, and your cluster will eventually enter and remain in that desired range until you stop your cluster.


## Stop an AKS cluster

Use the

command to stop a running AKS cluster, including the nodes and control plane. The following example stops a cluster named`az aks stop`

*myAKSCluster*:`az aks stop --name myAKSCluster --resource-group myResourceGroup`

Verify your cluster has stopped using the

command and confirming the`az aks show`

`powerState`

shows as`Stopped`

.`az aks show --name myAKSCluster --resource-group myResourceGroup`

Your output should look similar to the following condensed example output:

`{ [...] "nodeResourceGroup": "MC_myResourceGroup_myAKSCluster_westus2", "powerState":{ "code":"Stopped" }, "privateFqdn": null, "provisioningState": "Succeeded", "resourceGroup": "myResourceGroup", [...] }`

If the

`provisioningState`

shows`Stopping`

, your cluster hasn't fully stopped yet.

Important

If you're using [pod disruption budgets](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/), the stop operation can take longer, as the drain process will take more time to complete.

## Start an AKS cluster

Caution

After utilizing the start/stop feature on AKS, it is essential to wait 15-30 minutes before restarting your AKS cluster. This waiting period is necessary because it takes several minutes for the relevant services to fully stop. Attempting to restart your cluster during this process can disrupt the shutdown process and potentially cause issues with the cluster or its workloads.

Use the

command to start a stopped AKS cluster. The cluster restarts with the previous control plane state and number of agent nodes. The following example starts a cluster named`az aks start`

*myAKSCluster*:`az aks start --name myAKSCluster --resource-group myResourceGroup`

Verify your cluster has started using the

command and confirming the`az aks show`

`powerState`

shows`Running`

.`az aks show --name myAKSCluster --resource-group myResourceGroup`

Your output should look similar to the following condensed example output:

`{ [...] "nodeResourceGroup": "MC_myResourceGroup_myAKSCluster_westus2", "powerState":{ "code":"Running" }, "privateFqdn": null, "provisioningState": "Succeeded", "resourceGroup": "myResourceGroup", [...] }`

If the

`provisioningState`

shows`Starting`

, your cluster hasn't fully started yet.

## Next steps

- To learn how to scale
`User`

pools to 0, see[Scale](scale-cluster#scale-user-node-pools-to-0).`User`

pools to 0 - To learn how to save costs using Spot instances, see
[Add a spot node pool to AKS](spot-node-pool). - To learn more about the AKS support policies, see
[AKS support policies](support-policies).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-ai-ml-language-models -->

# Concepts - Small and large language models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about small and large language models, including when to use them and how you can use them with your AI and machine learning workflows on Azure Kubernetes Service (AKS).

## What are language models?

Language models are powerful machine learning models used for natural language processing (NLP) tasks, such as text generation and sentiment analysis. These models represent natural language based on the probability of words or sequences of words occurring in a given context.

*Conventional language models* have been used in supervised settings for research purposes where the models are trained on well-labeled text datasets for specific tasks. *Pre-trained language models* offer an accessible way to get started with AI and have become more widely used in recent years. These models are trained on large-scale text corpora from the internet using deep neural networks and can be fine-tuned on smaller datasets for specific tasks.

The size of a language model is determined by its number of parameters, or *weights*, that determine how the model processes input data and generates output. Parameters are learned during the training process by adjusting the weights within layers of the model to minimize the difference between the model's predictions and the actual data. The more parameters a model has, the more complex and expressive it is, but also the more computationally expensive it is to train and use.

In general, **small language models** have *fewer than 10 billion parameters*, and **large language models** have *more than 10 billion parameters*. For example, the new Microsoft Phi-3 model family has three versions with different sizes: mini (3.8 billion parameters), small (7 billion parameters), and medium (14 billion parameters).

## When to use small language models

### Advantages

Small language models are a good choice if you want models that are:

**Faster and more cost-effective to train and run**: They require less data and compute power.**Easy to deploy and maintain**: They have smaller storage and memory footprints.**Less prone to**, which is when a model learns the noise or specific patterns of the training data and fails to generalize new data.*overfitting***Interpretable and explainable**: They have fewer parameters and components to understand and analyze.

### Use cases

Small language models are suitable for use cases that require:

**Limited data or resources**, and you need a quick and simple solution.**Well-defined or narrow tasks**, and you don't need much creativity in the output.**High-precision and low-recall tasks**, and you value accuracy and quality over coverage and quantity.**Sensitive or regulated tasks**, and you need to ensure the transparency and accountability of the model.

The following table lists some popular, high-performance small language models:

| Model family | Model sizes (Number of parameters) | Software license |
|---|---|---|
| Microsoft Phi-3 | Phi-3-mini (3.8 billion), Phi-3-small (7 billion) | MIT license |
| Microsoft Phi-2 | Phi-2 (2.7 billion) | MIT license |
| Falcon | Falcon-7B (7 billion) | Apache 2.0 license |

## When to use large language models

### Advantages

Large language models are a good choice if you want models that are:

**Powerful and expressive**: They can capture more complex patterns and relationships in the data.**General and adaptable**: They can handle a wider range of tasks and transfer knowledge across domains.**Robust and consistent**: They can handle noisy or incomplete inputs and avoid common errors and biases.

### Use cases

Large language models are suitable for use cases that require:

**Abundant data and resources**, and you have the budget to build and maintain a complex solution.**Low-precision and high-recall tasks**, and you value coverage and quantity over accuracy and quality.**Challenging or exploratory tasks**, and you want to leverage the model's capacity to learn and adapt.

The following table lists some popular, high-performance large language models:

| Model family | Model sizes (Number of parameters) | Software license |
|---|---|---|
| Microsoft Phi-3 | Phi-3-medium (14 billion) | MIT license |
| Falcon | Falcon-40B (40 billion) | Apache 2.0 license |

## Experiment with small and large language models on AKS

Kubernetes AI Toolchain Operator (KAITO) is an open-source operator that automates small and large language model deployments in Kubernetes clusters. The KAITO add-on for AKS simplifies onboarding and reduces the time-to-inference for open-source models on your AKS clusters. The add-on automatically provisions right-sized GPU nodes and sets up the associated interference server as an endpoint server to your chosen model.

For more information, see [Deploy an AI model on AKS with the AI toolchain operator](ai-toolchain-operator). To get started with a range of supported small and large language models for your inference workflows, see the [KAITO model GitHub repository](https://github.com/Azure/kaito/tree/main/presets).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Next steps

To learn more about containerized AI and machine learning workloads on AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-advanced-container-networking-services -->

# Use Advanced Container Networking Services on your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to enable and disable Advanced Container Networking Services, including [Container Network Observability](advanced-container-networking-services-overview#container-network-observability) and [Container Network Security](advanced-container-networking-services-overview#container-network-security), on your AKS clusters.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - Azure CLI version 2.71.0 or higher. Find your version using the
`az --version`

command. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). [Install the](#install-the-aks-preview-azure-cli-extension)version`aks-preview`

Azure CLI extension`14.0.0b6`

or higher.[Register the](#register-the-advancednetworkingl7policypreview-feature-flag)in your subscription.`AdvancedNetworkingL7PolicyPreview`

feature flag- Clusters that have the Cilium data plane support
*Container Network Observability*and*Container Network Security*in Kubernetes version 1.29 and later.

## Install the `aks-preview`

Azure CLI extension

Install or update the Azure CLI preview extension using the

or`az extension add`

command.`az extension update`

`# Install the aks-preview extension az extension add --name aks-preview # Update the extension to make sure you have the latest version installed az extension update --name aks-preview`


## Register the `AdvancedNetworkingL7PolicyPreview`

feature flag

Register the

`AdvancedNetworkingL7PolicyPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"`

Registration takes a few minutes to complete.

Verify successful registration using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"`


## Set environment variables

The examples in this article use the following environment variables:

| Variable | Description | Example value |
|---|---|---|
`RESOURCE_GROUP` |
Name of the Azure resource group | `myResourceGroup` |
`LOCATION` |
Azure region for resources | `eastus` |
`CLUSTER_NAME` |
Name of the AKS cluster | `myAKSCluster` |

**All commands in this article assume these environment variables are set**. Make sure to replace the example values with your own values.

## Create a resource group

Create a resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`


## Create a new AKS cluster with Advanced Container Networking Services

Note

When the `--acns-advanced-networkpolicies`

parameter is set to `L7`

, both Layer 7 and fully qualified domain name (FQDN) filtering policies are enabled. If you want to enable only FQDN filtering, set the parameter to `FQDN`

.

Create an AKS cluster with Advanced Container Networking Services and Cilium using the

command with the`az aks create`

`--enable-acns`

and`--network-dataplane cilium`

flags.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --network-plugin azure \ --network-plugin-mode overlay \ --network-dataplane cilium \ --kubernetes-version 1.29 \ --enable-acns \ --acns-advanced-networkpolicies <L7/FQDN>`


Important

The [Container Network Security](advanced-container-networking-services-overview#container-network-security) feature isn't available for non-Cilium clusters.

Create an AKS cluster with Advanced Container Networking Services using the

command with the`az aks create`

`--enable-acns`

flag.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --network-plugin azure \ --network-plugin-mode overlay \ --enable-acns`


## Enable Advanced Container Networking Services on an existing cluster

Enable Advanced Container Networking Services on an existing AKS cluster with Cilium using the

command with the`az aks update`

`--enable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --acns-advanced-networkpolicies <L7/FQDN>`


Enable Advanced Container Networking Services on an existing AKS cluster using the

command with the`az aks update`

`--enable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns`


## Disable Advanced Container Networking Services on an AKS cluster

Disable Advanced Container Networking Services on an existing AKS cluster using the

command with the`az aks update`

`--disable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --disable-acns`


## Disable Container Network Observability on an AKS cluster

Disable the Container Network Observability feature without affecting other Advanced Container Networking Services features using the

command with the`az aks update`

`--disable-acns-observability`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --disable-acns-observability`


Container Network Observability is the only feature available for non-Cilium clusters, so you can disable it only by disabling the entire Advanced Container Networking Services suite.

Disable the Container Network Observability feature on an existing AKS cluster using the

command with the`az aks update`

`--disable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --disable-acns`


## Disable Container Network Security on an AKS cluster

Disable the Container Network Security feature without affecting other Advanced Container Networking Services features using the

command with the`az aks update`

`--disable-acns-security`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --disable-acns-security`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-arm64-vms -->

# Use Arm-based processor (Arm64) Virtual Machines (VMs) in an Azure Kubernetes Service (AKS) cluster for cost effectiveness

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Arm-based processors (Arm64)](/en-us/azure/virtual-machines/sizes/cobalt-overview) are power-efficient and cost-effective, but don't compromise on performance. These Arm64 VMs are engineered to efficiently run dynamic, scalable workloads and can deliver up to 50% better price-performance than comparable x86-based VMs for scale-out workloads.

Because of their ability to scale workloads efficiently, Arm64 VMs are well-suited for web or application servers, open-source databases, cloud-native applications, gaming servers, and other high traffic applications.

Note

While a combination of CPU, memory, and networking capacity configurations heavily influences the cost effectiveness of a SKU, Arm64 VM types are recommended for cost optimization.

In this article, you'll learn how to add a Arm64 VM to an existing node pool.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

Before you begin, make sure you have:

## Limitations

- Arm64 VMs aren't supported for Windows node pools.
- Existing node pools can't be updated to use an Arm64 VM.
- Federal Information Process Standard (FIPS)-enabled node pools are only supported with Arm64 SKUs when using Azure Linux 3.0+.
- Arm64 node pools aren't supported on Defender-enabled clusters with Kubernetes version 1.29.0 or lower.

## Create node pools with Arm64 VMs

The Arm64 processor provides low power compute for your Kubernetes workloads. Arm64 virtual machines can be added to existing clusters even mixing Intel and Arm architecture node pools within a cluster. To create an Arm64 node pool, you need to choose a [Dpsv5](/en-us/azure/virtual-machines/dpsv5-dpdsv5-series), [Dplsv5](/en-us/azure/virtual-machines/dplsv5-dpldsv5-series), or [Epsv5](/en-us/azure/virtual-machines/epsv5-epdsv5-series) series virtual machine.

### Add a node pool with an Arm64 VM

Use [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) to add a node pool with an Arm64 VM to an existing cluster. Alternatively, if you're using

[Azure Linux 3.0+](/en-us/azure/azure-linux/how-to-enable-azure-linux-3), you can add a node pool with an Arm64 VM and

[FIPS](enable-fips-nodes)enabled.

Add a node pool with an Arm64 VM

`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $ARM_NODE_POOL_NAME \ --node-count 3 \ --node-vm-size Standard_D2pds_v5`

Add a FIPS-enabled node pool with an Arm64 VM

Limitations:

- Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)enabled aren't supported with Ubuntu OS. - Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)require kubernetes version 1.31+.

Use the

with`az aks nodepool add`

`--enable-fips-image`

and`--os-sku`

parameters.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $ARM_NODE_POOL_NAME \ --os-sku AzureLinux --enable-fips-image --kubernetes-version 1.31 --node-count 3 \ --node-vm-size Standard_D2pds_v5`

For more information on verifying FIPS enablement and disabling FIPS, see

[Enable FIPS node pools](enable-fips-nodes).- Node pools with Arm64 VMs and
Update a node pool with an Arm64 VM to enable FIPS

Limitations:

- Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)enabled aren't supported with Ubuntu OS. - Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)require kubernetes version 1.31+.

Use

command with the`az aks nodepool update`

`--enable-fips-image`

parameter to enable FIPS on an existing node pool.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name np \ --enable-fips-image`

This command triggers a reimage of the node pool immediately to deploy the FIPS compliant Operating System. This reimage occurs during the node pool update. No extra steps are required.

- Node pools with Arm64 VMs and

For more information on verifying FIPS enablement and disabling FIPS, see [Enable FIPS node pools](enable-fips-nodes).

## Verify the node pool uses Arm64

Verify a node pool uses Arm64 using the [ az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command and verify the

`vmSize`

is a [Dpsv5](/en-us/azure/virtual-machines/dpsv5-dpdsv5-series),

[Dplsv5](/en-us/azure/virtual-machines/dplsv5-dpldsv5-series), or

[Epsv5](/en-us/azure/virtual-machines/epsv5-epdsv5-series)series.

```
az aks nodepool show \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name mynodepool \
--query vmSize
```


The following example output shows the node pool uses Arm64:

```
"Standard_D2pds_v5"
```


## Next steps

In this article, you learned how to add a node pool with an Arm64 VM to an AKS cluster.

- For more recommendations for cost savings, see
[Best practices for cost optimization in Azure Kubernetes Service (AKS)](best-practices-cost). - For more information about Arm64, see
[Cobalt Arm-based processors (Arm64)](/en-us/azure/virtual-machines/sizes/cobalt-overview). - For more information on verifying FIPS enablement and disabling FIPS, see
[Enable FIPS node pools](enable-fips-nodes). - For Azure Linux 3.0 enablement and support details, see
[Enable Azure Linux 3.0](/en-us/azure/azure-linux/how-to-enable-azure-linux-3).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/optimized-addon-scaling -->

# Enable cost optimized add-on scaling on your Azure Kubernetes Service (AKS) cluster (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of cost optimized add-on scaling in Azure Kubernetes Service (AKS). With cost-optimized add-on scaling, you can manage add-ons that require custom CPU and memory by overriding default configurations or enabling autoscaling. This feature ensures that resources aren't overly allocated to add-on pods, improving cost savings and cluster efficiency.

## Overview

Enabling cost optimized add-on scaling installs the [Vertical Pod Autoscaler (VPA)add-on](vertical-pod-autoscaler), allowing supported add-ons to autoscale based on usage.

This feature also allows you to customize the resource's default CPU/ memory requests and limits in Deployments and DaemonSets, the maximum and minimum allowed CPU/ memory, and the VPA update mode within VPA custom resources. For more information, see [customize the resource configuration for AKS add-ons](customize-resource-configuration).

### Supported AKS add-ons

The following AKS managed add-ons support the cost optimized add-on scaling feature:

| Add-on | Enablement behavior | VPA custom resource name | Command to check VPA custom resource |
|---|---|---|---|
|

`coredns`

`kubectl get vpa coredns --namespace kube-system`

[Workload identity](workload-identity-deploy-cluster)`azure-wi-webhook-controller-manager`

`kubectl get vpa azure-wi-webhook-controller-manager --namespace kube-system`

[Image Integrity](image-integrity)`ratify`

`kubectl get vpa ratify --namespace gatekeeper-system`

[Network Observability (Retina)](container-network-observability-how-to)`retina-agent`

and `retina-operator`

`kubectl get vpa retina-agent --namespace kube-system`

and `kubectl get vpa retina-operator --namespace kube-system`

### Supported VPA modes for cost optimized add-on scaling

VPA currently supports the following modes for cost optimized add-on scaling:

*Off*: The VPA provides resource recommendation data but doesn't apply it to the target pod.*Initial*(default mode): The VPA automatically applies CPU and memory recommendations to the target pod when it restarts, but it doesn't initiate the restart itself.*Auto*: The VPA automatically updates CPU and memory requests for pods based on recommendations.

Note

When enabling cost optimized add-on scaling, consider the following information:

- If you delete the Deployment, DaemonSet, or VPA custom resource, the changes revert back to the AKS add-on's initial configuration.
- The cost optimized add-on scaling feature enables the
[VPA add-on](vertical-pod-autoscaler)to autoscale the supported AKS add-ons. It doesn't work with self-hosted VPA. - AKS restarts the add-on pods when enabling cost optimized add-on scaling. CoreDNS is currently the only exception to avoid potential disruptions during the restart. For more information, see
[CoreDNS autoscaling behavior](coredns-autoscale).

Warning

Make sure you have enough compute resources on the system node pool for your addons when you enable cost optimized add-on scaling. AKS recommends turning on the [cluster autoscaler](cluster-autoscaler-overview) or [node autoprovision](node-autoprovision) to ensure right-sizing of your compute resources automatically.
Monitor for pending add-on pods when using the cost-optimized add-on scaling feature. VPA might recommend resource requests that exceed available node capacity, potentially leading to unschedulable pods. You can control this behavior by [customizing min/max values](customize-resource-configuration) for requests and limits of supported addons.

## Prerequisites

- An AKS cluster running Kubernetes version 1.25 or later.
- The Azure CLI version 2.60.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). [Install the](#install-the-aks-preview-azure-cli-extension)and`aks-preview`

Azure CLI extension[register the cost optimized add-on scaling preview feature](#register-the-cost-optimized-add-on-scaling-preview-feature).

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Install the `aks-preview`

Azure CLI extension

Install the

`aks-preview`

extension using the`az extension add`

command.`az extension add --name aks-preview`

Update to the latest version of the extension using the

`az extension update`

command.`az extension update --name aks-preview`


### Register the cost optimized add-on scaling preview feature

Register the cost optimized add-on scaling preview feature using the

`az feature register`

command.`az feature register --namespace "Microsoft.ContainerService" --name "AKS-AddonAutoscalingPreview"`

It takes a few minutes for the status to show as

*Registered*.Verify the registration status using the

`az feature show`

command.`az feature show --namespace "Microsoft.ContainerService" --name "AKS-AddonAutoscalingPreview"`

When the status shows as

*Registered*, refresh the registration of the Microsoft.ContainerService provider using the`az provider register`

command.`az provider register --namespace Microsoft.ContainerService`


## Enable cost optimized add-on scaling on an AKS cluster

When enabling the add-on, the AKS cluster automatically installs the [VPA add-on](vertical-pod-autoscaler). The [AKS add-ons that support the cost optimized add-on scaling feature](#supported-aks-add-ons) have different enablement behavior.

Note

If you're using Bicep, ARM templates, or Terraform, set `VerticalPodAutoscaler`

to `"True"`

and `AddonAutoscaling`

to `"enabled"`

.

### Enable cost optimized add-on scaling on a new cluster

Enable cost optimized add-on scaling on a new AKS cluster using the

command with the`az aks create`

`--enable-optimized-addon-scaling`

flag.`az aks create --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --enable-optimized-addon-scaling`


### Enable cost optimized add-on scaling on an existing cluster

Enable cost optimized add-on scaling on an existing AKS cluster using the

command with the`az aks update`

`--enable-optimized-addon-scaling`

flag.`az aks update --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --enable-optimized-addon-scaling`


## Disable cost optimized add-on scaling on an AKS cluster

Disable cost optimized add-on scaling on an AKS cluster using the

command with the`az aks update`

`--disable-optimized-addon-scaling`

flag.`az aks update --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --disable-optimized-addon-scaling`


Note

Disabling the cost optimized add-on scaling feature doesn't disable the VPA add-on by default. To disable VPA, see [Disable VPA on an AKS cluster](use-vertical-pod-autoscaler#disable-the-vertical-pod-autoscaler-on-an-existing-cluster).

## Customize default resource configuration

With the cost optimized add-on scaling feature enabled on your cluster, you can customize the default CPU/memory settings for the add-on resources as well as the default VPA configuration for supported AKS add-ons. For more information, see [customize the resource configuration for AKS add-ons](customize-resource-configuration).

## Applying the VPA recommended values manually

Note

With *Initial* mode, the VPA applies the recommended CPU and memory requests only when a pod is created or updated. If you want the recommendations to take effect immediately, please update the pods manually. Before manually applying the recommended values, [make sure the VPA update mode is set to Initial or Auto in the VPA custom resource](customize-resource-configuration#customize-resource-update-mode).

Check the pod status and CPU/memory utilization to verify that the pod is running as expected.

The following example uses the

`kubectl get pod`

command to check a CoreDNS pod status:`kubectl get pod <coredns-pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a CoreDNS pod:

`apiVersion: v1 kind: Pod metadata: name: <coredns-pod-name> namespace: kube-system spec: ... containers: - name: coredns resources: limits: cpu: "3" memory: "500Mi" requests: cpu: "100m" memory: "70Mi"`

Get the VPA recommended value using the

`kubectl get vpa`

command.`kubectl get vpa coredns --namespace kube-system`

The following output shows an example of the VPA recommended value for a CoreDNS pod:

`NAME MODE CPU MEM PROVIDED AGE coredns Initial 11m 23574998 True 44m`

If you want to use the values recommended by VPA, manually delete the pod using the

`kubectl delete pod`

command to restart the pod with the VPA recommended values.`kubectl delete pod <coredns-pod-name> --namespace kube-system`

After the pod restarts, verify the pod status and CPU/memory updates using the

`kubectl get pod`

command.`kubectl get pod <coredns-pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a CoreDNS pod after applying the VPA recommended values:

`apiVersion: v1 kind: Pod metadata: name: <coredns-pod-name> namespace: kube-system spec: ... containers: - name: coredns resources: limits: cpu: "330m" memory: "168392842" requests: cpu: "11m" memory: "23574998"`


## Troubleshooting

With the cost optimized add-on scaling feature enabled on your cluster, you can customize the default CPU and memory settings for add-on resources, as well as modify the default VPA configuration for supported AKS managed add-ons

If your autoscaling enabled add-on pods are in a pending state, or you don't see any VPA recommendations for autoscaling enabled add-ons, follow these steps to troubleshoot the issue.

### Check AKS-managed VPA add-on status

Check if all VPA system components are running using the

`kubectl get pods`

command.`kubectl get pods --namespace kube-system | grep vpa`

The output should show three pods (vpa-admission-controller, vpa-recommender, and vpa-updater) running in the

`kube-system`

namespace, similar to the following example:`vpa-admission-controller 2/2 2 2 4m11s vpa-recommender 1/1 1 1 4m11s vpa-updater 1/1 1 1 4m11s`

For each of the three VPA pods, check the logs for any errors using the

`kubectl logs`

command. Make sure to replace`<pod-name>`

with the names of the VPA pods.`kubectl logs <pod-name> --namespace kube-system | grep -e '^E[0-9]\{4\}'`

Confirm the custom resource definition (CRD) was creating using the

`kubectl get`

command.`kubectl get customresourcedefinition | grep verticalpodautoscalers`


### Check pod status and CPU/memory utilization

Check the pod's status using the

`kubectl get pod`

command.`kubectl get pod <pod-name> --namespace=kube-system`

If the pod has a status of

`Pending`

, check the pod's status property to determine the reason the pod isn't running.`kubectl describe pod <pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a pod with a status of

`Pending`

:`apiVersion: v1 kind: Pod ... status: conditions: - lastProbeTime: null lastTransitionTime: "2023-05-03T17:05:26Z" message: '0/1 nodes are available: 1 Insufficient cpu, 1 Insufficient memory. preemption: 0/1 nodes are available: 1 Insufficient cpu, 1 Insufficient memory..' reason: Unschedulable status: "False" type: PodScheduled phase: Pending qosClass: Guaranteed`

If the output shows that the pod is

`Pending`

due to insufficient CPU or memory, consider the following actions:- Add more nodes so that pods can be scheduled in nodes with lower resource usage.
- Disable VPA for the target add-on pod by changing the update mode to
*Off*, and then[manually update the requests/limits](customize-resource-configuration)to the available resource values on the node. Be cautious when setting resource limits to extremely low values, as this may result in the pod encountering OOM kills or CPU throttling if it attempts to use more resources than are available on the node.


## Next steps

- Configure
[Cluster Autoscaler](cluster-autoscaler-overview)or[Node Autoprovisioning](node-autoprovision)in your cluster to automatically scale the cluster.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-about -->

# Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Istio](https://istio.io/latest/) addresses the challenges developers and operators face with a distributed or microservices architecture. The Istio-based service mesh add-on provides an officially supported and tested integration for Azure Kubernetes Service (AKS).

## What is a Service Mesh?

Modern applications are typically architected as distributed collections of microservices, with each collection of microservices performing some discrete business function. A service mesh is a dedicated infrastructure layer that you can add to your applications. It allows you to transparently add capabilities like observability, traffic management, and security, without adding them to your own code. The term **service mesh** describes both the type of software you use to implement this pattern, and the security or network domain that is created when you use that software.

As the deployment of distributed services, such as in a Kubernetes-based system, grows in size and complexity, it can become harder to understand and manage. You may need to implement capabilities such as discovery, load balancing, failure recovery, metrics, and monitoring. A service mesh can also address more complex operational requirements like A/B testing, canary deployments, rate limiting, access control, encryption, and end-to-end authentication.

Service-to-service communication is what makes a distributed application possible. Routing this communication, both within and across application clusters, becomes increasingly complex as the number of services grow. Istio helps reduce this complexity while easing the strain on development teams.

## What is Istio?

Istio is an open-source service mesh that layers transparently onto existing distributed applications. Istio’s powerful features provide a uniform and more efficient way to secure, connect, and monitor services. Istio enables load balancing, service-to-service authentication, and monitoring – with few or no service code changes. Its powerful control plane brings vital features, including:

- Secure service-to-service communication in a cluster with TLS (Transport Layer Security) encryption, strong identity-based authentication, and authorization.
- Automatic load balancing for HTTP, gRPC, WebSocket, and TCP traffic.
- Fine-grained control of traffic behavior with rich routing rules, retries, failovers, and fault injection.
- A pluggable policy layer and configuration API supporting access controls, rate limits, and quotas.
- Automatic metrics, logs, and traces for all traffic within a cluster, including cluster ingress and egress.

## How is the add-on different from open-source Istio?

This service mesh add-on uses and builds on top of open-source Istio. The add-on flavor provides the following extra benefits:

- Istio versions are tested and verified to be compatible with supported versions of Azure Kubernetes Service.
- Microsoft handles scaling and configuration of Istio control plane
- Microsoft adjusts scaling of AKS components like
`coredns`

when Istio is enabled. - Microsoft provides managed lifecycle (upgrades) for Istio components when triggered by user.
- Verified external and internal ingress set-up.
- Verified to work with
[Azure Monitor managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)and[Azure Managed Grafana](/en-us/azure/managed-grafana/overview). - Official Azure support provided for the add-on.

## Limitations

Istio-based service mesh add-on for AKS has the following limitations:

- The add-on doesn't work on AKS clusters that are using
[Open Service Mesh addon for AKS](open-service-mesh-about). - The add-on doesn't work on AKS clusters with self-managed installations of Istio.
- The add-on doesn't support adding pods associated with virtual nodes to be added under the mesh.
- The add-on doesn't yet support the sidecar-less Ambient mode. Microsoft is currently contributing to Ambient workstream under Istio open source. Product integration for Ambient mode is on the roadmap and is being continuously evaluated as the Ambient workstream evolves.
- The add-on doesn't yet support multi-cluster deployments.
- The add-on doesn't yet support Windows Server containers. Windows Server containers aren't yet supported in open source Istio right now. Issue tracking this feature ask can be found
[here](https://github.com/istio/istio/issues/27893). - Customization of mesh through the following custom resources is currently blocked -
`ProxyConfig, WorkloadEntry, WorkloadGroup, IstioOperator, WasmPlugin`

. - While the add-on allows the use of
`EnvoyFilter`

's, issues arising from them (for example from the Lua script or from the compression library) are outside the support scope of the Istio add-on. See the[support policy document](istio-support-policy#allowed-supported-and-blocked-customizations)for more information about the support categories for Istio add-on features and configuration options. - Gateway API for Istio ingress gateway or managing mesh traffic (GAMMA) is currently not yet supported with Istio add-on. However, Gateway API for Istio ingress traffic management is currently under active development for the add-on. While the add-on supports
[annotation and](istio-deploy-ingress#ingress-gateway-service-customizations), port or protocol configuration is currently not supported.`externalTrafficPolicy`

customization for the Istio ingress gateways - The add-on supports customization of a subset of the fields in
[MeshConfig](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/). Other customizations may be allowed but unsupported or disallowed entirely, as detailed[here](istio-meshconfig#allowed-supported-and-blocked-meshconfig-values).

## Feedback and feature ask

Feedback and feature ask for the Istio add-on can be provided by creating [issues with label 'service-mesh' on AKS GitHub repository](https://github.com/Azure/AKS/issues?q=is%3Aopen+is%3Aissue+label%3Aservice-mesh).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/reduce-latency-ppg -->

# Use proximity placement groups to reduce latency for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

When using proximity placement groups on AKS, colocation only applies to the agent nodes. Node to node and the corresponding hosted pod to pod latency is improved. The colocation doesn't affect the placement of a cluster's control plane.

When deploying your application in Azure, you can create network latency by spreading virtual machine (VM) instances across regions or availability zones, which may impact the overall performance of your application. A proximity placement group is a logical grouping used to make sure Azure compute resources are physically located close to one another. Some applications, such as gaming, engineering simulations, and high-frequency trading (HFT) require low latency and tasks that can complete quickly. For similar high-performance computing (HPC) scenarios, consider using [proximity placement groups (PPG)](/en-us/azure/virtual-machines/co-location#proximity-placement-groups) for your cluster's node pools.

## Before you begin

This article requires Azure CLI version 2.14 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Limitations

- A proximity placement group can map to only
*one*availability zone. - A node pool must use Virtual Machine Scale Sets to associate a proximity placement group.
- A node pool can associate a proximity placement group at node pool create time only.

## Node pools and proximity placement groups

The first resource you deploy with a proximity placement group attaches to a specific data center. Any extra resources you deploy with the same proximity placement group are colocated in the same data center. Once all resources using the proximity placement group are stopped (deallocated) or deleted, it's no longer attached.

- You can associate multiple node pools with a single proximity placement group.
- You can only associate a node pool with a single proximity placement group.

### Configure proximity placement groups with availability zones

Note

While proximity placement groups require a node pool to use only *one* availability zone, the [baseline Azure VM SLA of 99.9%](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_9/) is still in effect for VMs in a single zone.

Proximity placement groups are a node pool concept and associated with each individual node pool. Using a PPG resource has no impact on AKS control plane availability, which can impact how you should design your cluster with zones. To ensure a cluster is spread across multiple zones, we recommend using the following design:

- Provision a cluster with the first system pool using
*three*zones and no proximity placement group associated to ensure the system pods land in a dedicated node pool, which spreads across multiple zones. - Add extra user node pools with a unique zone and proximity placement group associated to each pool. An example is
*nodepool1*in zone one and PPG1,*nodepool2*in zone two and PPG2, and*nodepool3*in zone 3 with PPG3. This configuration ensures that, at a cluster level, nodes are spread across multiple zones and each individual node pool is colocated in the designated zone with a dedicated PPG resource.

## Create a new AKS cluster with a proximity placement group

Accelerated networking greatly improves networking performance of virtual machines. Ideally, use proximity placement groups with accelerated networking. By default, AKS uses accelerated networking on [supported virtual machine instances](/en-us/azure/virtual-network/accelerated-networking-overview?toc=/azure/virtual-machines/linux/toc.json#limitations-and-constraints), which include most Azure virtual machine with two or more vCPUs.

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location centralus`

Create a proximity placement group using the

command. Make sure to note the ID value in the output.`az ppg create`

`az ppg create --name myPPG --resource-group myResourceGroup --location centralus --type standard`

The command produces an output similar to the following example output, which includes the

*ID*value you need for upcoming CLI commands.`{ "availabilitySets": null, "colocationStatus": null, "id": "/subscriptions/yourSubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.Compute/proximityPlacementGroups/myPPG", "location": "centralus", "name": "myPPG", "proximityPlacementGroupType": "Standard", "resourceGroup": "myResourceGroup", "tags": {}, "type": "Microsoft.Compute/proximityPlacementGroups", "virtualMachineScaleSets": null, "virtualMachines": null }`

Create an AKS cluster using the

command and replace the`az aks create`

*myPPGResourceID*value with your proximity placement group resource ID from the previous step.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --ppg myPPGResourceID --generate-ssh-keys`


## Add a proximity placement group to an existing cluster

You can add a proximity placement group to an existing cluster by creating a new node pool. You can then optionally migrate existing workloads to the new node pool and delete the original node pool.

Use the same proximity placement group that you created earlier to ensure agent nodes in both node pools in your AKS cluster are physically located in the same data center.

Create a new node pool using the

command and replace the`az aks nodepool add`

*myPPGResourceID*value with your proximity placement group resource ID.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name mynodepool \ --node-count 1 \ --ppg myPPGResourceID`


## Clean up

Delete the Azure resource group along with its resources using the

command.`az group delete`

`az group delete --name myResourceGroup --yes --no-wait`


## Next steps

Learn more about [proximity placement groups](/en-us/azure/virtual-machines/co-location#proximity-placement-groups).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kubelogin-authentication -->

# Use kubelogin to authenticate users in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The kubelogin plugin in Azure is a client-go credential [plugin](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#client-go-credential-plugins) that implements Microsoft Entra authentication. The kubelogin plugin offers features that aren't available in the kubectl command-line tool. For more information, see the [kubelogin introduction](https://azure.github.io/kubelogin/index.html) and the [kubectl introduction](https://kubernetes.io/docs/reference/kubectl/introduction/).

This article provides an overview and examples of how to use kubelogin for all supported Microsoft Entra authentication methods in AKS.

## Kubelogin authentication in AKS limitations

- Groups that are created in Microsoft Entra are included only by their
**ObjectID**value, and not by their display name. The`sAMAccountName`

command is available only for groups that are synchronized from on-premises Windows Server Active Directory.

- The service principal authentication method works only with managed Microsoft Entra, and not with the earlier version Azure Active Directory.
- The service principal can be a member of a maximum of 200
[Microsoft Entra groups](/en-us/entra/identity/hybrid/connect/how-to-connect-fed-group-claims). If you have more than 200 groups, consider using[application roles](/en-us/entra/external-id/customers/how-to-use-app-roles-customers).

- The device code authentication method doesn't work when a Microsoft Entra Conditional Access policy is set on a Microsoft Entra tenant. In that scenario, use web browser interactive authentication instead.

- The Azure CLI authentication method works only with AKS managed Microsoft Entra.

## How authentication works

Note

Keep in mind the following information about kubelogin authentication for AKS clusters integrated with Microsoft Entra:

**Clusters running Kubernetes version 1.24 or later**automatically use the kubelogin format.**Clusters running Kubernetes 1.24 or earlier**require manual conversion. You can use the device code authentication method to convert the kubeconfig file to use the exec plugin format.

For most interactions with kubelogin, you use the `convert-kubeconfig`

subcommand. The subcommand uses the kubeconfig file that's specified in `--kubeconfig`

or in the `KUBECONFIG`

environment variable to convert the final kubeconfig file to exec format based on the specified authentication method.

The authentication methods that kubelogin implements are Microsoft Entra OAuth 2.0 token grant flows. In each authentication method, the token isn't cached on the file system.

## Device code authentication

Device code is the default authentication method for the `convert-kubeconfig`

subcommand. This authentication method prompts the device code for the user to sign in from a browser session.

Note

Before the kubelogin and exec plugins were introduced, the Azure authentication method in kubectl supported only the device code flow. It used an earlier version of a library that produces a token that has the `audience`

claim with an `spn:`

prefix. It isn't compatible with [AKS managed Microsoft Entra](managed-azure-ad), which uses an [on-behalf-of (OBO)](/en-us/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) flow. When you run the `convert-kubeconfig`

subcommand, kubelogin removes the `spn:`

prefix from the audience claim.

### Parameters for device code authentication

The following table outlines parameters that you can use with device code authentication:

| Parameter | Description |
|---|---|
`-l devicecode` (optional) |
Specifies the kubelogin authentication method. This parameter is optional because device code is the default method. |
`--legacy` |
Uses legacy behavior for earlier versions of Azure Active Directory clusters. If you're using the kubeconfig file in an earlier version Azure Active Directory cluster, kubelogin automatically adds the `--legacy` flag. |
`--token-cache-dir` |
Overrides the default path of the token cache directory, which is ${HOME}/.kube/cache/kubelogin. |

## Azure CLI authentication

The Azure CLI (command: `-l azurecli`

) authentication method uses the signed-in context that the Azure CLI establishes to get the access token. The token is issued in the same Microsoft Entra tenant as `az login`

. kubelogin doesn't write tokens to the token cache file because the Azure CLI already manages them.

### Parameters for Azure CLI authentication

The following table outlines parameters that you can use with Azure CLI authentication:

| Parameter | Description |
|---|---|
`-l azurecli` |
Specifies the kubelogin authentication method. |
`--azure-config-dir` |
Specifies the Azure CLI configuration directory. The default directory is ${HOME}/.azure. |

## Sign in to Azure

Sign in to Azure using the [ az login](/en-us/cli/azure/authenticate-azure-cli-interactively#interactive-login) command.

```
az login
```


## Web browser interactive authentication

The web browser interactive (command: `-l interactive`

) method of authentication automatically opens a web browser to sign in the user. After the user is authenticated, the browser redirects to the local web server using the verified credentials. This authentication method complies with Conditional Access policy.

You can use either a bearer token or a Proof-of-Possession (PoP) token with this authentication method.

### Parameters for bearer token authentication

The following table outlines parameters that you can use with bearer token authentication:

| Parameter | Description |
|---|---|
`-l interactive` |
Specifies the kubelogin authentication method. |
`--token-cache-dir` |
Overrides the default path of the token cache directory, which is ${HOME}/.kube/cache/kubelogin. |

### Parameters for PoP token authentication

The following table outlines parameters that you can use with PoP token authentication:

| Parameter | Description |
|---|---|
`-l interactive` |
Specifies the kubelogin authentication method. |
`--pop-enabled` |
Enables PoP token authentication. |
`--pop-claims` |
Specifies the PoP token claims in a key-value pair format. For example, `u=/ARM/ID/OF/CLUSTER` . |

## Service principal authentication

The service principal (command: `-l spn`

) authentication method uses a service principal to sign in the user. You can provide the credential by setting an environment variable or by using the credential in a command-line argument. The supported credentials that you can use are a password or a Personal Information Exchange (PFX) client certificate.

### Parameters for service principal authentication

The following table outlines parameters that you can use with service principal authentication:

| Parameter | Description |
|---|---|
`-l spn` |
Specifies the kubelogin authentication method. |
`--client-id` |
The application ID (client-id) of the service principal. |
`--client-secret` |
The client secret of the service principal. |

## Managed identity authentication

Use the [managed identity](/en-us/entra/identity/managed-identities-azure-resources/overview) (command: `-l msi`

) authentication method for applications that connect to resources that support Microsoft Entra authentication. Examples include accessing Azure resources like an Azure virtual machine (VM), a virtual machine scale set, or Azure Cloud Shell.

You can use the default managed identity that's assigned to the resource or a specific user-assigned managed identity.

### Parameters for managed identity authentication

The following table outlines parameters that you can use with managed identity authentication:

| Parameter | Description |
|---|---|
`-l msi` |
Specifies the kubelogin authentication method. |
`--client-id` |
The application ID (client-id) of the user-assigned managed identity. If you don't specify this parameter, the default managed identity is used. |

## Workload identity authentication

The workload identity (command: `-l workloadidentity`

) authentication method uses identity credentials that are federated with Microsoft Entra to authenticate access to AKS clusters. The method uses Microsoft Entra integrated authentication. It works by setting the following environment variables:

| Variable | Description |
|---|---|
`AZURE_CLIENT_ID` |
The Microsoft Entra application ID that is federated with the workload identity. |
`AZURE_TENANT_ID` |
The Microsoft Entra tenant ID. |
`AZURE_FEDERATED_TOKEN_FILE` |
The file that contains a signed assertion of the workload identity, like a Kubernetes projected service account (JWT) token. |
`AZURE_AUTHORITY_HOST` |
The base URL of a Microsoft Entra authority. For example, `https://login.microsoftonline.com/` . |

You can use a [workload identity](/en-us/entra/workload-id/workload-identities-overview) to access Kubernetes clusters from CI/CD systems like GitHub or ArgoCD without storing service principal credentials in the external systems. To configure OpenID Connect (OIDC) federation from GitHub, see the [OIDC federation example](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-azure).

### Parameters for workload identity authentication

The following table outlines parameters that you can use with workload identity authentication:

| Parameter | Description |
|---|---|
`-l workloadidentity` |
Specifies the kubelogin authentication method. |

## Export the kubeconfig file path

Before you run the `convert-kubeconfig`

subcommand, export the kubeconfig file path to the `KUBECONFIG`

environment variable. For example:

```
export KUBECONFIG=/path/to/kubeconfig
```


## Convert the kubeconfig file

Run the `convert-kubeconfig`

subcommand to convert the kubeconfig file to use the exec plugin for your chosen authentication method.

```
kubelogin convert-kubeconfig
```


```
kubelogin convert-kubeconfig -l azurecli
```


```
# Bearer token authentication
kubelogin convert-kubeconfig -l interactive
# Proof-of-Possession (PoP) token authentication
kubelogin convert-kubeconfig -l interactive --pop-enabled --pop-claims "u=/ARM/ID/OF/CLUSTER"
```


-
[Use environment variables](#tabpanel_1_environment-variables) -
[Use command-line arguments](#tabpanel_1_command-line-arguments) -
[Use a client certificate](#tabpanel_1_client-certificate) -
[Use a PoP token with environment variables](#tabpanel_1_pop-token-environment-variables)

Run the

`convert-kubeconfig`

subcommand to convert the kubeconfig file to use the exec plugin.`kubelogin convert-kubeconfig -l spn`

Set the environment variables for the client ID and client secret or client certificate. For example:

`export AZURE_CLIENT_ID=<service-principal-client-id> export AZURE_CLIENT_SECRET=<service-principal-client-secret>`


```
# Default managed identity authentication
kubelogin convert-kubeconfig -l msi
# Specific managed identity authentication
kubelogin convert-kubeconfig -l msi --client-id <managed-identity-client-id>
```


```
kubelogin convert-kubeconfig -l workloadidentity
```


## Remove cached tokens

Remove cached tokens using the `kubelogin remove-tokens`

command.

```
kubelogin remove-tokens
```


## Get node information

Get node information using the `kubectl get`

command.

```
kubectl get nodes
```


## How to use kubelogin with AKS

AKS uses a pair of first-party Microsoft Entra applications. These application IDs are the same in all environments.

The AKS Microsoft Entra server application ID (server-id) that the server side uses is `6dae42f8-4368-4678-94ff-3960e28e3630`

. The access token that accesses AKS clusters must be issued for this application. In most kubelogin authentication methods, you must use `--server-id`

with `kubelogin get-token`

.

The AKS Microsoft Entra client application ID (client-id) that kubelogin uses to perform public client authentication on behalf of the user is `80faf920-1908-4b52-b5ef-a8e7bedfc67a`

. The client application ID is used in device code and web browser interactive authentication methods.

## Related content

- Learn how to integrate AKS with Microsoft Entra in the
[AKS managed Microsoft Entra integration](managed-azure-ad)how-to article. - To get started with managed identities in AKS, see
[Use a managed identity in AKS](use-managed-identity). - To get started with workload identities in AKS, see
[Use a workload identity in AKS](workload-identity-overview).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-cni-powered-by-cilium -->

# Configure Azure CNI Powered by Cilium in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure CNI Powered by Cilium combines the robust control plane of Azure Container Networking Interface (CNI) with the data plane of [Cilium](https://cilium.io/) to provide high-performance networking and security.

Azure CNI Powered by Cilium provides the following benefits by making use of eBPF programs loaded into the Linux kernel and a more efficient API object structure:

- Functionality equivalent to existing Azure CNI and Azure CNI Overlay plugins
- Improved service routing
- More efficient network policy enforcement
- Better observability of cluster traffic
- Support for larger clusters (more nodes, pods, and services)

## IP Address Management (IPAM) with Azure CNI Powered by Cilium

You can deploy Azure CNI Powered by Cilium with two different methods for assigning pod IPs:

- Assign IP addresses from an overlay network (similar to Azure CNI Overlay mode)
- Assign IP addresses from a virtual network (similar to existing Azure CNI with Dynamic Pod IP Assignment)

If you aren't sure which option to select, read [Choose a network model](concepts-network-azure-cni-overlay#choose-a-network-model)

## Versions

| Kubernetes Version | Minimum Cilium Version |
|---|---|
| 1.29 (LTS) | 1.14.19 |
| 1.30 | 1.14.19 |
| 1.31 | 1.16.6 |
| 1.32 | 1.17.0 |
| 1.33 | 1.17.0 |

For more information on AKS versioning and release timelines, see [Supported Kubernetes Versions](supported-kubernetes-versions).

## Network Policy Enforcement

Cilium enforces [network policies to allow or deny traffic between pods](operator-best-practices-network#control-traffic-flow-with-network-policies). With Cilium, you don't need to install a separate network policy engine such as Azure Network Policy Manager or Calico.

## Local Redirect Policy (LRP)

LRP starts to be supported from Kubernetes v1.29 and up, Cilium v1.14 and up. For LRP to work with Advanced Container Networking Services (ACNS) - FQDN Filtering, the Cilium Network Policy egress labels need to match with node-local DNS cache pod labels.

## Limitations

Azure CNI powered by Cilium currently has the following limitations:

- Available only for Linux and not for Windows.
- Network policies can't use
`ipBlock`

to allow access to node or pod IPs. For details and recommended workarounds, see[frequently asked questions](#frequently-asked-questions). - For Cilium versions 1.16 or earlier, multiple Kubernetes services can't use the same host port with different protocols (for example, TCP or UDP) (
[Cilium issue #14287](https://github.com/cilium/cilium/issues/14287)). - Network policies aren't applied to pods using host networking (
`spec.hostNetwork: true`

) because these pods use the host identity instead of having individual identities. - Cilium Endpoint Slices are supported in Kubernetes version 1.32 and above. Cilium Endpoint Slices don't support configuration of how Cilium Endpoints are grouped. Priority namespace through
`cilium.io/ces-namespace`

isn't supported. - L7 policy isn't supported by
`CiliumClusterwideNetworkPolicy`

(CCNP). - Cilium uses Cilium identities as unique identity for provisioning endpoints, so high-churning workloads such as Spark jobs generate high count of Cilium identities. To avoid workloads hitting Cilium identity limits (65535), excluding Spark job's labels like
`!spark-app-name`

and`!spark-app-selector`

in the Cilium configmap can significantly reduce Cilium identity generation. For more details on Cilium identity exclusion rules, check[the official Cilium label documentation](https://docs.cilium.io/en/stable/operations/performance/scalability/identity-relevant-labels/#excluding-labels). - AKS Local DNS isn't compatible with Advanced Container Networking Services (ACNS) - FQDN Filtering.

## Considerations

To gain capabilities such as observability into your network traffic and security features like Fully Qualified Domain Name (FQDN) based filtering and Layer 7 based network policies on your cluster, consider enabling [Advanced Container Networking services](advanced-container-networking-services-overview) on your clusters.

## Prerequisites

- Azure CLI version 2.48.1 or later. Run
`az --version`

to see the currently installed version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you're using ARM templates or the REST API, the AKS API version must be
`2022-09-02-preview`

or later.

Previous AKS API versions (`2022-09-02preview`

to `2023-01-02preview`

) used the field [ networkProfile.ebpfDataplane=cilium](https://github.com/Azure/azure-rest-api-specs/blob/06dbe269f7d9c709cc225c92358b38c3c2b74d60/specification/containerservice/resource-manager/Microsoft.ContainerService/aks/preview/2022-09-02-preview/managedClusters.json#L6939-L6955). AKS API versions since

`2023-02-02preview`

use the field [to enable Azure CNI Powered by Cilium.](https://github.com/Azure/azure-rest-api-specs/blob/06dbe269f7d9c709cc225c92358b38c3c2b74d60/specification/containerservice/resource-manager/Microsoft.ContainerService/aks/preview/2023-02-02-preview/managedClusters.json#L7152-L7173)

`networkProfile.networkDataplane=cilium`

## Create a new AKS Cluster with Azure CNI Powered by Cilium

The following sections use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command to create a cluster and assign IP addresses.

### Option 1: Assign IP addresses from an overlay network

Use the following commands to create a cluster with an overlay network and Cilium. Replace the values for `<clusterName>`

, `<resourceGroupName>`

, and `<location>`

:

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--network-plugin azure \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16 \
--network-dataplane cilium \
--generate-ssh-keys
```


The `--network-dataplane cilium`

flag replaces the deprecated `--enable-ebpf-dataplane`

flag used in earlier versions of the aks-preview CLI extension.

### Option 2: Assign IP addresses from a virtual network

Run the following commands to create a resource group and virtual network with a subnet for nodes and a subnet for pods.

```
# Create the resource group
az group create --name <resourceGroupName> --location <location>
```


```
# Create a virtual network with a subnet for nodes and a subnet for pods
az network vnet create --resource-group <resourceGroupName> --location <location> --name <vnetName> --address-prefixes <address prefix, example: 10.0.0.0/8> -o none
az network vnet subnet create --resource-group <resourceGroupName> --vnet-name <vnetName> --name nodesubnet --address-prefixes <address prefix, example: 10.240.0.0/16> -o none
az network vnet subnet create --resource-group <resourceGroupName> --vnet-name <vnetName> --name podsubnet --address-prefixes <address prefix, example: 10.241.0.0/16> -o none
```


Create the cluster using `--network-dataplane cilium`

:

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--max-pods 250 \
--network-plugin azure \
--vnet-subnet-id /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.Network/virtualNetworks/<vnetName>/subnets/nodesubnet \
--pod-subnet-id /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.Network/virtualNetworks/<vnetName>/subnets/podsubnet \
--network-dataplane cilium \
--generate-ssh-keys
```


### Option 3: Assign IP addresses from the Node Subnet

Azure CLI version 2.69.0 or later is required. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Create a cluster using [node subnet](concepts-network-legacy-cni#azure-cni-node-subnet) with a Cilium data plane:

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--network-plugin azure \
--network-dataplane cilium \
--generate-ssh-keys
```


## Frequently asked questions

**Can I customize Cilium configuration?**No, AKS manages the Cilium configuration and it can't be modified. We recommend that customers who require more control use

[AKS BYO CNI](use-byo-cni)and install Cilium manually.**Can I use**`CiliumNetworkPolicy`

custom resources instead of Kubernetes`NetworkPolicy`

resources?L3 and L4

`CiliumNetworkPolicy`

are supported and can be used alongside Kubernetes`NetworkPolicy`

resources.Customers might use FQDN filtering and Layer 7 policies as part of the

[Advanced Container Networking Services](advanced-container-networking-services-overview)feature bundle.**Can I use**`CiliumClusterwideNetworkPolicy`

?Yes,

`CiliumClusterwideNetworkPolicy`

is supported. The following sample policy YAML shows configuring an L4 rule:`apiVersion: "cilium.io/v2" kind: CiliumClusterwideNetworkPolicy metadata: name: "l4-rule-ingress-backend-frontend" spec: endpointSelector: matchLabels: role: backend ingress: - fromEndpoints: - matchLabels: role: frontend toPorts: - ports: - port: "80" protocol: TCP`

**Which Cilium features are supported in Azure managed CNI? Which of those require Advanced Container Networking Services?**Supported Feature w/o ACNS w/ ACNS Cilium Endpoint Slices ✔️ ✔️ K8s Network Policies ✔️ ✔️ Cilium L3/L4 Network Policies ✔️ ✔️ Cilium Clusterwide Network Policy ✔️ ✔️ FQDN Filtering ❌ ✔️ L7 Network Policies (HTTP/gRPC/Kafka) ❌ ✔️ Container Network Observability (Metrics and Flow logs) ❌ ✔️ eBPF Host Routing ❌ ✔️ **Why is traffic being blocked when the**`NetworkPolicy`

has an`ipBlock`

that allows the IP address?A limitation of Azure CNI Powered by Cilium is that a

`NetworkPolicy`

`ipBlock`

can't select pod or node IPs.For example, this

`NetworkPolicy`

has an`ipBlock`

that allows all egress to`0.0.0.0/0`

:`apiVersion: networking.k8s.io/v1 kind: NetworkPolicy metadata: name: example-ipblock spec: podSelector: {} policyTypes: - Egress egress: - to: - ipBlock: cidr: 0.0.0.0/0 # This will still block pod and node IPs.`

However, when this

`NetworkPolicy`

is applied, Cilium blocks egress to pod and node IPs even though the IPs are within the`ipBlock`

CIDR.As a workaround, you can add

`namespaceSelector`

and`podSelector`

to select pods. This example selects all pods in all namespaces:`apiVersion: networking.k8s.io/v1 kind: NetworkPolicy metadata: name: example-ipblock spec: podSelector: {} policyTypes: - Egress egress: - to: - ipBlock: cidr: 0.0.0.0/0 - namespaceSelector: {} - podSelector: {}`

It isn't currently possible to specify a

`NetworkPolicy`

with an`ipBlock`

to allow traffic to node IPs.**Does AKS configure CPU or memory limits on the Cilium**`daemonset`

?No, AKS doesn't configure CPU or memory limits on the Cilium

`daemonset`

because Cilium is a critical system component for pod networking and network policy enforcement.**Does Azure CNI powered by Cilium use kube-proxy?**No, AKS clusters created with network data plane as Cilium don't use

`kube-proxy`

. If the AKS clusters are on[Azure CNI Overlay](azure-cni-overlay)or[Azure CNI with dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)and are upgraded to AKS clusters running Azure CNI powered by Cilium, new nodes workloads are created without`kube-proxy`

. Older workloads are also migrated to run without`kube-proxy`

as a part of this upgrade process.

## Dual-stack networking with Azure CNI Powered by Cilium

You can deploy your dual-stack AKS clusters with Azure CNI Powered by Cilium. This feature also allows you to control your IPv6 traffic with the Cilium Network Policy engine.

You must have Kubernetes version 1.29 or greater.

### Set up Overlay clusters with Azure CNI Powered by Cilium

Create a cluster with Azure CNI Overlay using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command. Make sure to use the argument

`--network-dataplane cilium`

to specify the Cilium data plane.```
clusterName="myOverlayCluster"
resourceGroup="myResourceGroup"
location="westcentralus"
az aks create \
--name $clusterName \
--resource-group $resourceGroup \
--location $location \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--ip-families ipv4,ipv6 \
--generate-ssh-keys
```


## Next steps

Learn more about networking in AKS in the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/customize-resource-configuration -->

# Customize the resource configuration for managed add-ons

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of how to customize the resource configuration for Azure Kubernetes Service (AKS) managed add-ons with [cost optimized add-on scaling (Preview)](optimized-addon-scaling).

## Overview

Enabling the cost optimized add-on scaling feature in your AKS cluster installs the Vertical Pod Autoscaler (VPA) add-on and VPA custom resources for AKS managed add-ons that support this capability. This feature also allows you to manually customize the resource CPU and memory requests and limits in Deployments and DaemonSets. You can also customize the maximum and minimum allowed CPU and memory and the VPA update mode within VPA custom resources.

## Prerequisites

- Review the
[supported AKS managed add-ons](optimized-addon-scaling#supported-aks-add-ons)and[limitations](optimized-addon-scaling)for this feature. - You need an AKS cluster enabled with the cost optimized add-on scaling feature. If you don't have one, see
[Enable cost optimized add-on scaling on your AKS cluster (Preview)](optimized-addon-scaling).

## Customize resource annotations

| Annotation | Description | Values |
|---|---|---|
`kubernetes.azure.com/override-requests-limits` |
Supports the capability to customize the container resource CPU/memory requests/limits in a Deployment or DaemonSet if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. | "enabled" or "disabled" |
`kubernetes.azure.com/override-min-max` |
Supports the capability to customize the container policy maximum/minimum allowed CPU/memory value in VPA custom resource if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. | "enabled" or "disabled" |
`kubernetes.azure.com/override-update-mode` |
Supports the capability to customize the update policy `updateMode` value in a VPA custom resource if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. |
"enabled" or "disabled" |

## Customize resource CPU/memory requests/limits

After setting the `kubernetes.azure.com/override-requests-limits`

annotation to "enabled" in a Deployment or DaemonSet, you can customize the resource CPU/memory requests and limits. The following example shows how to customize the resource CPU/memory requests and limits in a Deployment:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-requests-limits: "enabled"
spec:
...
containers:
- name: coredns
resources:
limits:
# update cpu limits value won't be reconciled back
cpu: "3"
# update memory limits value won't be reconciled back
memory: "500Mi"
requests:
# update cpu requests value won't be reconciled back
cpu: "100m"
# update memory requests value won't be reconciled back
memory: "70Mi"
```


## Customize resource maximum/minimum allowed CPU/memory

After setting the `kubernetes.azure.com/override-min-max`

annotation to "enabled" in a VPA custom resource, you can customize the maximum and minimum allowed CPU and memory values in a VPA custom resource. The following example shows how to customize the maximum and minimum allowed CPU and memory values in a VPA custom resource:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-min-max: "enabled"
spec:
resourcePolicy:
containerPolicies:
- containerName: coredns
maxAllowed:
# update maxAllowed cpu value won't be reconciled back
cpu: 3
# update maxAllowed memory value won't be reconciled back
memory: 500Mi
minAllowed:
# update minAllowed cpu value won't be reconciled back
cpu: 10m
# update minAllowed memory value won't be reconciled back
memory: 10Mi
...
```


## Customize resource update mode

After setting the `kubernetes.azure.com/override-update-mode`

annotation to "enabled" in a VPA custom resource, you can customize the update policy `updateMode`

value in a VPA custom resource to "Off" or "Initial" (default). The following example shows how to customize the update policy `updateMode`

value to "Initial" in a VPA custom resource:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-update-mode: "enabled"
spec:
...
updatePolicy:
# update updateMode won't be reconciled back
updateMode: "Initial"
```


## Disable VPA on a specific AKS managed add-on

To disable VPA on a specific AKS managed add-on, you need to update the VPA custom resource YAML file to set the `kubernetes.azure.com/override-update-mode`

annotation to `"enabled"`

and the `updateMode`

to `"Off"`

. With *Off* mode, the VPA only provides CPU and memory recommendations and doesn't apply the changes to the pod.

The following example shows how to disable VPA on the CoreDNS add-on:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# Set value to "enabled"
kubernetes.azure.com/override-update-mode: "enabled"
spec:
...
updatePolicy:
# Set value to "Off"
updateMode: "Off"
```


## Troubleshooting

- Make sure the AKS managed add-on supports the cost optimized add-on scaling feature. For more information, see
[Supported AKS managed add-ons](optimized-addon-scaling#supported-aks-add-ons). - Verify that the
`kubernetes.azure.com/override-requests-limits`

annotation in the Deployment or DaemonSet is set to "enabled". - Verify that the
`kubernetes.azure.com/override-min-max`

annotation in the VPA custom resource is set to "enabled". - Verify that the
`kubernetes.azure.com/override-update-mode`

annotation in the VPA custom resource is set to "enabled".

## Next steps

To further configure cluster resource utilization and free up CPU/memory for AKS managed add-on pods, see [Vertical pod autoscaling in AKS](vertical-pod-autoscaler).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-application -->

# Tutorial - Deploy an application to Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes provides a distributed platform for containerized applications. You build and deploy your own applications and services into a Kubernetes cluster and let the cluster manage the availability and connectivity.

In this tutorial, you deploy a sample application into a Kubernetes cluster. You learn how to:

- Update a Kubernetes manifest file.
- Run an application in Kubernetes.
- Test the application.

Tip

With AKS, you can use the following approaches for configuration management:

**GitOps**: Enables declarations of your cluster's state to automatically apply to the cluster. To learn how to use GitOps to deploy an application with an AKS cluster, see the[prerequisites for Azure Kubernetes Service clusters](/en-us/azure/azure-arc/kubernetes/tutorial-use-gitops-flux2?toc=/azure/aks/toc.json#for-azure-kubernetes-service-clusters)in the[GitOps with Flux v2](/en-us/azure/azure-arc/kubernetes/tutorial-use-gitops-flux2?toc=/azure/aks/toc.json)tutorial.**DevOps**: Enables you to build, test, and deploy with continuous integration (CI) and continuous delivery (CD). To see examples of how to use DevOps to deploy an application with an AKS cluster, see[Build and deploy to AKS with Azure Pipelines](devops-pipeline)or[GitHub Actions for deploying to Kubernetes](kubernetes-action).

## Before you begin

In previous tutorials, you packaged an application into a container image, uploaded the image to Azure Container Registry, and created a Kubernetes cluster. To complete this tutorial, you need the precreated `aks-store-quickstart.yaml`

Kubernetes manifest file. This file was downloaded in the application source code from [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.0.53 or later. Check your version with `az --version`

. To install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Update the manifest file

In these tutorials, your Azure Container Registry (ACR) instance stores the container images for the sample application. To deploy the application, you must update the image names in the Kubernetes manifest file to include your ACR login server name.

Get your login server address using the

command and query for your login server.`az acr list`

`az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table`

Make sure you're in the cloned

*aks-store-demo*directory, and then open the`aks-store-quickstart.yaml`

manifest file with a text editor.Update the

`image`

property for the containers by replacing*ghcr.io/azure-samples*with your ACR login server name.`containers: ... - name: order-service image: <acrName>.azurecr.io/aks-store-demo/order-service:latest ... - name: product-service image: <acrName>.azurecr.io/aks-store-demo/product-service:latest ... - name: store-front image: <acrName>.azurecr.io/aks-store-demo/store-front:latest ...`

Save and close the file.


## Run the application

Deploy the application using the

command, which parses the manifest file and creates the defined Kubernetes objects.`kubectl apply`

`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the resources successfully created in the AKS cluster:

`statefulset.apps/rabbitmq created configmap/rabbitmq-enabled-plugins created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`

Check the deployment is successful by viewing the pods with the

`kubectl get pods`

command.`kubectl get pods`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

### Command Line

Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`kubectl get service store-front --watch`

Initially, the

`EXTERNAL-IP`

for the`store-front`

service shows as`<pending>`

:`store-front LoadBalancer 10.0.34.242 <pending> 80:30676/TCP 5s`

When the

`EXTERNAL-IP`

address changes from`<pending>`

to a public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`store-front LoadBalancer 10.0.34.242 52.179.23.131 80:30676/TCP 67s`

View the application in action by opening a web browser and navigating to the external IP address of your service:

`http://<external-ip>`

.

If the application doesn't load, it might be an authorization problem with your image registry. To view the status of your containers, use the `kubectl get pods`

command. If you can't pull the container images, see [Authenticate with Azure Container Registry from Azure Kubernetes Service](cluster-container-registry-integration).

### Azure portal

Navigate to the Azure portal to find your deployment information.

Navigate to your AKS cluster resource.

From the service menu, under

**Kubernetes Resources**, select**Services and ingresses**.Copy the External IP shown in the column for the

`store-front`

service.Paste the IP into your browser to visit your store page.


## Clean up resources

Since you validated the application's functionality, you can now remove the cluster from the application. We will deploy the application again in the next tutorial.

Stop and remove the container instances and resources using the

`kubectl delete`

command.`kubectl delete -f aks-store-quickstart.yaml`

Check that all the application pods have been removed using the

`kubectl get pods`

command.`kubectl get pods`


## Next steps

In this tutorial, you deployed a sample Azure application to a Kubernetes cluster in AKS. You learned how to:

- Update a Kubernetes manifest file.
- Run an application in Kubernetes.
- Test the application.

In the next tutorial, you learn how to use PaaS services for stateful workloads in Kubernetes.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-best-practices -->

# Best practices for Windows containers on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In AKS, you can create node pools that run Linux or Windows Server as the operating system (OS) on the nodes. Windows Server nodes can run native Windows container applications, such as .NET Framework. The Linux OS and Windows OS have different container support and configuration considerations. For more information, see [Windows container considerations in Kubernetes](windows-vs-linux-containers). To learn more about how various industries are using Windows containers on AKS, see [Windows AKS customer stories](windows-aks-customer-stories).

This article outlines best practices for running Windows containers on AKS.

## Create an AKS cluster with Linux and Windows node pools

When you create a new AKS cluster, the Azure platform creates a Linux node pool by default. This node pool contains system services needed for the cluster to function. Azure also creates and manages a control plane abstracted from the user, which means you aren't exposed to the underlying OS of the nodes hosting the main control plane components. We recommend that you run at least *two nodes* on the default Linux node pool to ensure the reliability and performance of your cluster. You can't delete the default Linux node pool unless you delete the entire cluster.

There are some cases where you should consider deploying a Linux node pool when planning to run Windows-based workloads on your AKS cluster, such as:

- If you want to run Linux and Windows workloads, you can deploy a Linux node pool and a Windows node pool in the same cluster.
- If you want to deploy infrastructure-related components based on Linux, such as NGINX, you need a Linux node pool alongside your Windows node pool. You can use control plane nodes for development and testing scenarios. For production workloads, we recommend that you deploy separate Linux node pools to ensure reliability and performance.

## Modernize existing applications with Windows on AKS

You might want to containerize existing applications and run them using Windows on AKS. Before starting the containerization process, it's important to understand the application architecture and dependencies. For more information, see [Containerize existing applications using Windows containers](/en-us/virtualization/windowscontainers/quick-start/lift-shift-to-containers).

## Windows OS version


Best practice guidanceWindows Server 2022 provides improved security and performance and is the recommended OS for Windows node pools on AKS. AKS uses Windows Server 2022 as the host OS version and only supports process isolation.


AKS supports two options for the Windows Server operating system: Long Term Servicing Channel Releases (LTSC) and Windows Server Annual Channel for Containers.

AKS supports Long Term Servicing Channel Releases (LTSC), including Windows Server 2025 (preview), Windows Server 2022, and Windows Server 2019. This channel is released every three years and is supported for five years. Customers using Long Term Support (LTS) should use Windows Server 2022.

AKS uses Windows Server 2019 and Windows Server 2022 as the host OS versions and only supports process isolation. AKS doesn't support container images built by other versions of Windows Server. For more information, see

[Windows container version compatibility](/en-us/virtualization/windowscontainers/deploy-containers/version-compatibility). Windows Server 2022 is the default OS for Kubernetes version 1.25 and later.Important

Starting on March 01, 2026, Azure Kubernetes Service (AKS) no longer supports Windows Server 2019 node pools. Node pools running Kubernetes version 1.33+ can't use Windows Server 2019. Starting on April 01, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail. For more information on this retirement, see the

[Retirement GitHub issue](https://github.com/Azure/AKS/issues/4091)and the[Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=aks-will-stop-support-for-windows-server-2019-on-march-1-2026). To stay informed on announcements and updates, follow the[AKS release notes](https://github.com/Azure/AKS/releases).Important

Starting on March 15, 2027, Azure Kubernetes Service (AKS) no longer supports Windows Server 2022 node pools. Node pools running Kubernetes version 1.36+ can't use Windows Server 2022. Starting on April 01, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail. For more information on this retirement, see the

[Retirement GitHub issue](https://github.com/Azure/AKS/issues/4168)and the[Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=ws2022-retirement-aks). To stay informed on announcements and updates, follow the[AKS release notes](https://github.com/Azure/AKS/releases).AKS supports

[Windows Server Annual Channel for Containers](https://techcommunity.microsoft.com/t5/windows-server-news-and-best/windows-server-annual-channel-for-containers/ba-p/3866248)(preview). This channel is released annually and is supported for two years. This channel is beneficial for customers requiring increased innovation cycles and portability. The portability functionality enables the Windows Server 2022-based container image OS to run on newer versions of Windows Server host OS, such as the new annual channel release.Windows Annual Channel versions are based on the Kubernetes version of your node pool. To upgrade from one Annual Channel version to the next,

[upgrade to a Kubernetes version](upgrade-aks-cluster)that supports the next Annual Channel version. For more information, see[Windows Server Annual Channel for Containers on AKS](windows-annual-channel).

## Monitoring


Best practice guidanceWindows Exporter is installed on all Windows nodes in certain regions. To view regional rollout, see

[AKS Github]. With Managed Prometheus and Grafana, you can monitor default collectors included in Windows Exporter on AKS. For more information, see[default Prometheus metrics configured in Azure Monitor].

Windows Exporter allows customers to see their metrics through Managed Prometheus or Prometheus OSS deployments and enjoy enhanced observability around their node and pod performance, health, and resource usage. These metrics are also visible with Managed Grafana.

- When enabling managed prometheus, add this required parameter for correct dashboard data presentation for Windows:
`--enable-windows-recording-rules`

. - Grafana includes dashboards for showing Windows resources, such as:
- Kubernetes / Compute Resources / Cluster (Windows)
- Kubernetes / Compute Resources / Namespace (Windows)
- Kubernetes / Compute Resources / Pod (Windows)
- Kubernetes / USE Method / Cluster (Windows)
- Kubernetes / USE Method / Node (Windows)


The default collectors included in Windows Exporter on AKS are: cpu, cpu_info, cs, container, logical_disk, memory, net, os, process, service, system, textfile. The metrics are exposed on port **19182** on the windows node. For more information on what metrics you can see using these collectors, please see [prometheus-community/windows_exporter](https://github.com/prometheus-community/windows_exporter#collectors).

## Networking

### Networking modes


Best practice guidanceAKS clusters with Windows node pools only support Azure Container Networking Interface (Azure CNI) and use it by default.


Windows doesn't support kubenet networking. AKS clusters with Windows node pools must use Azure CNI. For more information, see [Network concepts for applications in AKS](concepts-network).

Azure CNI offers two networking modes based on your workload requirements:

is an overlay network similar to kubenet. The overlay network allows you to use virtual network (VNet) IPs for nodes and private address spaces for pods within those nodes that you can reuse across the cluster. Azure CNI Overlay is the**Azure CNI Overlay****recommended networking mode**. It provides simplified network configuration and management and the best scalability in AKS networking.requires extra planning and consideration for IP address management. This mode provides VNet IPs for nodes**Azure CNI with Dynamic IP Allocation***and*pods. This configuration allows you direct access to pod IPs. However, it comes with increased complexity and reduced scalability.

To help you decide which networking mode to use, see [Choosing a network model](concepts-network-azure-cni-overlay#choose-a-network-model).

### Network policies


Best practice guidanceUse network policies to secure traffic between pods. Windows supports Azure Network Policy Manager and Calico Network Policy. For more information, see

[Differences between Network Policy engines: Cilium, Azure NPM, and Calico].

When managing traffic between pods, you should apply the principle of least privilege. The Network Policy feature in Kubernetes allows you to define and enforce ingress and egress traffic rules between the pods in your cluster. For more information, see [Secure traffic between pods using network policies in AKS](use-network-policies).

Windows pods on AKS clusters that use the Calico Network Policy enable Floating IP by default.

## Upgrades and updates

It's important to keep your Windows environment up-to-date to ensure your systems have the latest security updates, feature sets, and compliance requirements. In a Kubernetes environment like AKS, you need to maintain the Kubernetes version, Windows nodes, and Windows container images and pods.

### Kubernetes version upgrades

As a managed Kubernetes service, AKS provides the necessary tools to upgrade your cluster to the latest Kubernetes version. For more information, see [Upgrade an AKS cluster](upgrade-cluster).

### Windows node monthly updates

Windows nodes on AKS follow a monthly update schedule. Every month, AKS creates a new VHD with the latest available updates for Windows node pools. The VHD includes the host image, latest Nano Server image, latest Server Core image, and container. We recommend performing monthly updates to your Windows node pools to ensure your nodes have the latest security patches. For more information, see [Upgrade AKS node images](node-image-upgrade).

Note

Upgrades on Windows systems include both OS version upgrades and monthly node OS updates.

You can stay up to date with the availability of new monthly releases using the [AKS release tracker](https://releases.aks.azure.com/) and [AKS release notes](https://github.com/Azure/AKS/releases).

### Windows node OS version upgrades

Windows has a release cadence for new versions of the OS, including Windows Server 2025 (preview), Windows Server 2022, and Windows Server 2019. When upgrading your Windows node OS version, ensure the Windows container image version matches the Windows container host version and the node pools have only one version of Windows Server.

To upgrade the Windows node OS version, you need to complete the following steps:

- Create a new node pool with the new Windows Server version.
- Deploy your workloads with the new Windows container images to the new node pool.
- Decommission the old node pool.

For more information, see [Upgrade Windows Server workloads on AKS](upgrade-windows-2019-2022).

Note

Windows announced a new [Windows Server Annual Channel for Containers](https://techcommunity.microsoft.com/t5/windows-server-news-and-best/windows-server-annual-channel-for-containers/ba-p/3866248) that supports portability and mixed versions of Windows nodes and containers. This feature isn't yet supported in AKS.

To track AKS feature plans, see the [Public AKS roadmap](https://github.com/Azure/AKS/projects/1#card-90806240).

## Next steps

To learn more about Windows containers on AKS, see the following resources:

[Learn how to deploy, manage, and monitor Windows containers on AKS](/en-us/training/paths/deploy-manage-monitor-wincontainers-aks).- Open an issue or provide feedback in the
[Windows containers GitHub repository](https://github.com/microsoft/Windows-Containers/issues). - Review the
[third-party partner solutions for Windows on AKS](windows-aks-partner-solutions).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-repair -->

# Azure Kubernetes Service (AKS) node auto-repair

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) continuously monitors the health state of worker nodes and performs automatic node repair if they become unhealthy. The Azure virtual machine (VM) platform [performs maintenance on VMs](/en-us/azure/virtual-machines/maintenance-and-updates) experiencing issues. AKS and Azure VMs work together to minimize service disruptions for clusters.

In this article, you learn how the automatic node repair functionality behaves for Windows and Linux nodes.

## How AKS checks for NotReady nodes

AKS uses the following rules to determine if a node is unhealthy and needs repair:

- The node reports the
status on consecutive checks within a 10-minute time frame.**NotReady** - The node doesn't report any status within 10 minutes.

You can manually check the health state of your nodes with the `kubectl get nodes`

command.

## How automatic repair works

Note

AKS initiates repair operations with the user account **aks-remediator**.

If AKS identifies an unhealthy node that remains unhealthy for at least *five* minutes, AKS performs the following actions:

- AKS reboots the node.
- If the node remains unhealthy after reboot, AKS reimages the node.
- If the node remains unhealthy after reimage and it's a Linux node, AKS redeploys the node.

AKS retries the restart, reimage, and redeploy sequence up to three times if the node remains unhealthy. The overall auto repair process can take up to an hour to complete.

## Limitations

AKS node auto-repair is a best effort service and we don't guarantee that the node is restored back to healthy status. If your node persists in an unhealthy state, we highly encourage that you perform manual investigation of the node. Learn more about [troubleshooting node NotReady status](/en-us/troubleshoot/azure/azure-kubernetes/availability-performance/node-not-ready-basic-troubleshooting).

There are cases where AKS doesn't perform automatic repair. Failure to automatically repair the node can occur either by design or if Azure can't detect that an issue exists. Examples of when auto-repair isn't performed include:

- A node status isn't being reported due to error in network configuration.
- A node failed to initially register as a healthy node.
- If either of the following taints are present on the node:
`node.cloudprovider.kubernetes.io/shutdown`

,`ToBeDeletedByClusterAutoscaler`

. - A node is in the process of being upgraded, resulting in the following annotation on the node
`"cluster-autoscaler.kubernetes.io/scale-down-disabled": "true"`

and`"kubernetes.azure.com/azure-cluster-autoscaler-scale-down-disabled-reason": "upgrade"`


## Monitor node auto-repair using Kubernetes events

When AKS performs node auto-repair on your cluster, AKS emits Kubernetes events from the aks-auto-repair source for visibility. The following events appear on a node object when auto-repair happens.

To learn more about accessing, storing, and configuring alerts on Kubernetes events, see [Use Kubernetes events for troubleshooting in Azure Kubernetes Service](events).

| Reason | Event Message | Description |
|---|---|---|
| NodeRebootStart | Node auto-repair is initiating a reboot action due to NotReady status persisting for more than 5 minutes. | This event is emitted to notify you when reboot is about to be performed on your node. This action is the first in the overall node auto-repair sequence. |
| NodeRebootEnd | Reboot action from node auto-repair is completed. | Emitted once reboot is complete on the node. This event doesn't indicate the health status (healthy or unhealthy) of the node after the reboot is performed. |
| NodeReimageStart | Node auto-repair is initiating a reimage action due to NotReady status persisting for more than 5 minutes. | This event is emitted to notify you when reimage is about to be performed on your node. |
| NodeReimageEnd | Reimage action from node auto-repair is completed. | Emitted once reimage is complete on the node. This event doesn't indicate the health status (healthy or unhealthy) of the node after the reimage is performed. |
| NodeRedeployStart | Node auto-repair is initiating a redeploy action due to NotReady status persisting more than 5 minutes. | This event is emitted to notify you when redeploy is about to be performed on your node. Redeploy is the last action in the node auto-repair sequence. |
| NodeRedeployEnd | Redeploy action from node auto-repair is completed. | Emitted once redeploy is complete on the node. This event doesn't indicate the health status (healthy or unhealthy) of the node after redeploy is performed. |

If any errors occur during the node auto-repair process, the following events are emitted with the verbatim error message. Learn more about [troubleshooting common node auto-repair errors](/en-us/troubleshoot/azure/azure-kubernetes/availability-performance/node-auto-repair-errors).

Note

*Error code* in the following event messages varies depending on the error reported.

| Reason | Event Message | Description |
|---|---|---|
| NodeRebootError | Node auto-repair reboot action failed due to an operation failure. See error details here: Error code |
Emitted when there's an error with the reboot action. |
| NodeReimageError | Node auto-repair reimage action failed due to an operation failure. See error details here: Error code |
Emitted when there's an error with the reimage action. |
| NodeRedeployError | Node auto-repair redeploy action failed due to an operation failure. See error details here: Error code |
Emitted when there's an error with the redeploy action. |

## Next steps

By default, you can access Kubernetes events and logs on your AKS cluster from the past 1 hour. To store and query events and logs from the past 90 days, enable [Container Insights](/en-us/azure/azure-monitor/containers/container-insights-overview#access-container-insights) for deeper troubleshooting on your AKS cluster.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-image-upgrade -->

# Upgrade Azure Kubernetes Service (AKS) node images

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) regularly provides new node images, so it's beneficial to upgrade your node images frequently to use the latest AKS features. Linux node images are updated weekly, and Windows node images are updated monthly. Image upgrade announcements are included in the [AKS release notes](https://github.com/Azure/AKS/releases), and it can take up to a week for these updates to be rolled out across all regions. You can also perform node image upgrades automatically and schedule them using planned maintenance. For more information, see [Automatically upgrade node images](auto-upgrade-node-image).

This article shows you how to upgrade AKS cluster node images and how to update node pool images without upgrading the Kubernetes version. For information on upgrading the Kubernetes version for your cluster, see [Upgrade an AKS cluster](upgrade-aks-cluster).

Note

The AKS cluster must use virtual machine scale sets for the nodes.

It's not possible to downgrade a node image version (for example *AKSUbuntu-2204 to AKSUbuntu-1804*, or *AKSUbuntu-2204-202308.01.0 to AKSUbuntu-2204-202307.27.0*).

## Connect to your AKS cluster

Connect to your AKS cluster using the [

`az aks get-credentials`

][az-aks-get-credentials] command.`az aks get-credentials \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER`


## Check for available node image upgrades

Check for available node image upgrades using the

command.`az aks nodepool get-upgrades`

`az aks nodepool get-upgrades \ --nodepool-name $AKS_NODEPOOL \ --cluster-name $AKS_CLUSTER \ --resource-group $AKS_RESOURCE_GROUP`

In the output, find and make note of the

`latestNodeImageVersion`

value. This value is the latest node image version available for your node pool.Check your current node image version to compare with the latest version using the

command.`az aks nodepool show`

`az aks nodepool show \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL \ --query nodeImageVersion`

If the

`nodeImageVersion`

value is different from the`latestNodeImageVersion`

, you can upgrade your node image.

## Upgrade all node images in all node pools

Upgrade all node images in all node pools in your cluster using the

command with the`az aks upgrade`

`--node-image-only`

flag.`az aks upgrade \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER \ --node-image-only \ --yes`

You can check the status of the node images using the

`kubectl get nodes`

command.Note

This command might differ slightly depending on the shell you use. For more information on Windows and PowerShell environments, see the

[Kubernetes JSONPath documentation](https://kubernetes.io/docs/reference/kubectl/jsonpath/).`kubectl get nodes -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.metadata.labels.kubernetes\.azure\.com\/node-image-version}{"\n"}{end}'`

When the upgrade completes, use the

command to get the updated node pool details. The current node image is shown in the`az aks show`

`nodeImageVersion`

property.`az aks show \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER`


## Upgrade a specific node pool

Update the OS image of a node pool without doing a Kubernetes cluster upgrade using the

command with the`az aks nodepool upgrade`

`--node-image-only`

flag.`az aks nodepool upgrade \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL \ --node-image-only`

You can check the status of the node images with the

`kubectl get nodes`

command.Note

This command may differ slightly depending on the shell you use. For more information on Windows and PowerShell environments, see the

[Kubernetes JSONPath documentation](https://kubernetes.io/docs/reference/kubectl/jsonpath/).`kubectl get nodes -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.metadata.labels.kubernetes\.azure\.com\/node-image-version}{"\n"}{end}'`

When the upgrade completes, use the

command to get the updated node pool details. The current node image is shown in the`az aks nodepool show`

`nodeImageVersion`

property.`az aks nodepool show \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL`


## Upgrade node images with node surge

To speed up the node image upgrade process, you can upgrade your node images using a customizable node surge value. By default, AKS uses one extra node to configure upgrades.

Upgrade node images with node surge using the

command with the`az aks nodepool update`

`--max-surge`

flag to configure the number of nodes used for upgrades.Note

To learn more about the trade-offs of various

`--max-surge`

settings, see[Customize node surge upgrade](upgrade-aks-cluster#customize-node-surge-upgrade).`az aks nodepool update \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL \ --max-surge 33% \ --no-wait`

You can check the status of the node images with the

`kubectl get nodes`

command.`kubectl get nodes -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.metadata.labels.kubernetes\.azure\.com\/node-image-version}{"\n"}{end}'`

Get the updated node pool details using the

command. The current node image is shown in the`az aks nodepool show`

`nodeImageVersion`

property.`az aks nodepool show \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL`


## Next steps

- For information about the latest node images, see the
[AKS release notes](https://github.com/Azure/AKS/releases). - Learn how to upgrade the Kubernetes version with
[Upgrade an AKS cluster](upgrade-aks-cluster). [Automatically apply cluster and node pool upgrades with GitHub Actions](node-upgrade-github-actions).- Learn more about multiple node pools with
[Create multiple node pools](create-node-pools). - Learn about upgrading best practices with
[AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/quotas-skus-regions -->

# Quotas, virtual machine size restrictions, and region availability in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure services set default limits and quotas for resources and features, including usage restrictions for certain virtual machine (VM) SKUs.

This article details the default resource limits for Azure Kubernetes Service (AKS) resources and the availability of AKS in Azure regions.

## Service quotas and limits

| Resource | Limit |
|---|---|
| Maximum number of clusters per subscription globally | 5,000 |
| Maximum nodes per cluster with Virtual Machine Scale Sets and
|

[node pools](/en-us/azure/aks/create-node-pools)Note: If you're unable to scale up to 5,000 nodes per cluster, see

[Best Practices for Large Clusters](/en-us/azure/aks/best-practices-performance-scale-large).[Kubenet](/en-us/azure/aks/concepts-network-legacy-cni#kubenet)networking plug-inAzure CLI default: 110

Azure Resource Manager template default: 110

Azure portal deployment default: 30

[Azure Container Networking Interface (Azure CNI)](/en-us/azure/aks/concepts-network-cni-overview)1Maximum recommended for Windows Server containers: 110

Default: 30

OSM controllers per cluster: 1

Pods per OSM controller: 1600

Kubernetes service accounts managed by OSM: 160

[Standard Load Balancer SKU](/en-us/azure/load-balancer/load-balancer-overview)1 Windows Server containers must use Azure CNI networking plug-in. Kubenet isn't supported for Windows Server containers.

| Kubernetes Control Plane tier | Limit |
|---|---|
| Standard tier | Automatically scales Kubernetes API server based on load. Larger control plane component limits and API server/etcd instances. |
| Free tier | Limited resources with
Not advised for production/critical workloads. |

### Quota limits on AKS Managed Clusters

Starting in September 2025, Azure Kubernetes Service will begin rolling out a change to enable quota for all current and new AKS customers. This rollout is expected to take place between September 1-30, 2025.

AKS quota will represent a limit of the maximum number of managed clusters (AKS clusters) that an Azure subscription can create per region. Once managed cluster quota is released, customers will need both quota for managed clusters and quota for their nodes (VM skus) in order to create an AKS cluster.

**Existing AKS customer subscriptions** will be given a default limit at or above their current usage depending on the available regional capacity. **Existing subscriptions using AKS for the first time and new subscriptions** will be given a default limit.

Customers can [view quota limits and usage](/en-us/azure/quotas/view-quotas) and [request additional quota](/en-us/azure/quotas/quickstart-increase-quota-portal) via the Azure portal Quotas page or via the [Quotas REST API](/en-us/rest/api/reserved-vm-instances/quotaapi). Prior to rollout completion, quota limits and usage *may* be visible in the Portal Quotas blade and customers will be able to request quota —however, the limits will not be enforced until rollout is complete.


lightbox="./media/quotas-skus-regions/portal-quotas-page-expanded.png"

When Managed Clusters Quota is rolled out, customers will receive the following error if they attempt to create a new cluster and are out of quota:

```
ManagedClusterCountExceedsQuotaLimit: Operation results in exceeding quota limits for managed clusters. Maximum allowed: %d, Current usage: %d, Additional requested: %d. Consider deleting unused clusters or requesting a quota increase. To request a quota increase, follow the instructions here: https://learn.microsoft.com/azure/quotas/quickstart-increase-quota-portal.
```


To remedy this, customers can [request additional quota in the Azure portal Quotas page](/en-us/azure/quotas/view-quotas) or via the [Quotas REST API](/en-us/rest/api/reserved-vm-instances/quotaapi).

#### AKS Managed Clusters Quota Limits

| Subscription Type | Default number of AKS clusters per subscription per region for new subscriptions1 |
Maximum number of AKS clusters per subscription per region via self service using
2 |
|---|

1 The default number of AKS clusters per subscription per region for new subscriptions may vary in regions with capacity constraints.

2 To request an increase of the quota limit, [use the Azure portal Quotas request process](/en-us/azure/quotas/quickstart-increase-quota-portal). Quota increase requests above the maximum self service amount will require a support ticket. Free Trial and Azure for Students subscriptions aren't eligible for limit or quota increases. If you have a Free Trial or Azure for Students subscription, you can upgrade to a pay-as-you-go subscription to get higher quota limits.

### Throttling limits on AKS resource provider APIs

AKS uses the [token bucket](https://en.wikipedia.org/wiki/Token_bucket) throttling algorithm to limit certain AKS [resource provider](/en-us/azure/azure-resource-manager/management/resource-providers-and-types) APIs. Throttling limits ensures the performance of the service and promotes fair usage of the service for all customers.

The buckets have a fixed size (also known as a burst rate) and refill over time at a fixed rate (also known as a sustained rate). Each throttling limit is in effect at the regional level for the specified resource in that region. For example, in the following table, a Subscription can call ListManagedClusters a maximum of 60 times (burst rate) at once for each ResourceGroup, but can continue to make 1 call every second thereafter (sustained rate).

| API request | Bucket size | Refill rate | Scope |
|---|---|---|---|
| LIST ManagedClusters | 500 requests | 1 requests / 1 second | Subscription |
| LIST ManagedClusters | 60 requests | 1 request / 1 second | ResourceGroup |
| PUT AgentPool | 20 requests | 1 request / 1 minute | AgentPool |
| PUT ManagedCluster | 20 requests | 1 request / 1 minute | ManagedCluster |
| GET ManagedCluster | 60 requests | 1 request / 1 second | Managed Cluster |
| GET Operation Status | 200 requests | 2 requests / 1 second | Subscription |
| All Other APIs | 60 requests | 1 request / 1 second | Subscription |

Note

The ManagedClusters and AgentPools buckets are counted separately for the same AKS cluster.

If a request is throttled, the request returns HTTP response code `429`

(Too Many Requests) and the error code shows as `Throttled`

in the response. Each throttled request includes a `Retry-After`

in the HTTP response header with the interval to wait before retrying, in seconds. Clients that use a bursty API call pattern should ensure that the Retry-After can be handled appropriately. To learn more about Retry-After, see the [following article](https://developer.mozilla.org/docs/Web/HTTP/Headers/Retry-After). Specifically, AKS uses `delay-seconds`

to specify the retry.

## Provisioned infrastructure

All other network, compute, and storage limitations apply to the provisioned infrastructure. For the relevant limits, see [Azure subscription and service limits](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits).

Important

When you upgrade an AKS cluster, extra resources are temporarily consumed. These resources include available IP addresses in a virtual network subnet or virtual machine vCPU quota.

For Windows Server containers, you can perform an upgrade operation to apply the latest node updates. If you don't have the available IP address space or vCPU quota to handle these temporary resources, the cluster upgrade process fails. For more information on the Windows Server node upgrade process, see [Upgrade a node pool in AKS](use-multiple-node-pools#upgrade-a-node-pool).

## Supported VM sizes

The list of supported VM sizes in AKS is evolving with the release of new VM SKUs in Azure. Follow the [AKS release notes](https://github.com/Azure/AKS/releases) to stay informed of new supported SKUs.

## Restricted VM sizes

Each node in an AKS cluster contains a fixed amount of compute resources such as vCPU and memory. Due to the required compute resources needed to run Kubernetes correctly, certain VM SKU sizes are restricted by default in AKS. These restrictions are to ensure that pods can be scheduled and function correctly on these nodes.

### User node pools

For user node pools, VM sizes with fewer than two vCPUs and two GBs of RAM (memory) might not be used.

### System node pools

For system node pools, VM sizes with fewer than two vCPUs and four GBs of RAM (memory) might not be used. To ensure that the required *kube-system* pods and your applications can reliably be scheduled, [B series VMs](/en-us/azure/virtual-machines/sizes-b-series-burstable) aren't supported for system node pools and [Av1 series VMs](/en-us/azure/virtual-machines/sizes/retirement/av1-series-retirement) aren't recommended.

For more information on VM types and their compute resources, see [Sizes for virtual machines in Azure](/en-us/azure/virtual-machines/sizes).

## Supported container image sizes

AKS doesn't set a limit on the container image size. However, it's important to understand that the larger the container image, the higher the memory demand. This demand could potentially exceed resource limits or the overall available memory of worker nodes. By default, memory for VM size Standard_DS2_v2 for an AKS cluster is set to 7 GiB.

When a container image is large (1 TiB or more), kubelet might not be able to pull it from your container registry to a node due to lack of disk space.

## Region availability

For the latest list of where you can deploy and run clusters, see [AKS region availability](https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service).

## Smart VM Defaults

As of May 2025, AKS automatically selects the optimal default VM SKU based on available capacity and quota if the parameter is unspecified during deployment. This default ensures that deployments are matched with the best possible SKU, enhancing performance and reliability while optimizing resource utilization. Previously, the default AKS VM SKU was Standard_DS2_V2, but there are now dynamic outcomes in default provisioning based on SKU availability that affects all new VM create operations.

## Cluster configuration presets in the Azure portal

When you create a cluster using the Azure portal, you can choose a preset configuration to quickly customize based on your scenario. You can modify any of the preset values at any time.

| Preset | Description |
|---|---|
| Production Standard | Best for most applications serving production traffic with AKS recommended best practices. |
| Dev/Test | Best for developing new workloads or testing existing workloads. |
| Production Economy | Best for serving production traffic in a cost conscious way if your workloads can tolerate interruptions. |
| Production Enterprise | Best for serving production traffic with rigorous permissions and hardened security. |

| Production Standard | Dev/Test | Production Economy | Production Enterprise | |
|---|---|---|---|---|
System node pool node size |
Standard_D8ds_v5 | Standard_D4ds_v5 | Standard_D8ds_v5 | Standard_D16ds_v5 |
System node pool autoscaling range |
2-5 nodes | 2-5 nodes | 2-5 nodes | 2-5 nodes |
User node pool node size |
Standard_D8ds_v5 | - | Standard_D8as_v4 | Standard_D8ds_v5 |
User node pool autoscaling range |
2-100 nodes | - | 0-25 nodes | 2-100 nodes |
Private cluster |
- | - | - | |
Availability zones |
- | - | ||
Azure Policy |
- | - | ||
Azure Monitor |
- | - | ||
Secrets store CSI driver |
- | - | ||
Network configuration |
Azure CNI Overlay | Azure CNI Overlay | Azure CNI Overlay | Azure CNI Overlay |
Network policy |
None | None | None | None |
Authentication and Authorization |
Local accounts with Kubernetes role-based access control (RBAC) | Local accounts with Kubernetes RBAC | Microsoft Entra ID Authentication with Azure role-based access control (Azure RBAC) | Microsoft Entra ID authentication with Azure RBAC |

## Next steps

You can increase certain default limits and quotas. If your resource supports an increase, request the increase through an [Azure support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest) (for **Issue type**, select **Quota**).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-scale -->

# Scaling options for applications in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When running applications in Azure Kubernetes Service (AKS), you might need to actively increase or decrease the amount of compute resources in your cluster. As you change the number of application instances you have, you might need to change the number of underlying Kubernetes nodes. You might also need to provision a large number of other application instances.

This article introduces core AKS application scaling concepts, including [manually scaling pods or nodes](#manually-scale-pods-or-nodes), using the [Horizontal pod autoscaler](#horizontal-pod-autoscaler), using the [Cluster autoscaler](#cluster-autoscaler), and integrating with [Azure Container Instances (ACI)](#burst-to-azure-container-instances-aci).

## Manually scale pods or nodes

You can manually scale replicas, or pods, and nodes to test how your application responds to a change in available resources and state. Manually scaling resources lets you define a set amount of resources to use, such as the number of nodes, to maintain a fixed cost. To manually scale, you define a replica or node count. The Kubernetes API then schedules the creation of more pods or the draining of nodes based on that replica or node count.

When you scale down nodes, the Kubernetes API calls the relevant Azure Compute API tied to the compute type used by your cluster. For example, for clusters built on Virtual Machine Scale Sets, the Virtual Machine Scale Sets API determines which nodes to remove. To learn more about how nodes are selected for removal on scale down, see the [Virtual Machine Scale Sets FAQ](/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-faq#if-i-reduce-my-scale-set-capacity-from-20-to-15--which-vms-are-removed-).

To get started with manually scaling nodes, see [manually scale nodes in an AKS cluster](scale-cluster). To manually scale the number of pods, see [kubectl scale command](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_scale/).

## Horizontal pod autoscaler

Kubernetes uses the horizontal pod autoscaler (HPA) to monitor the resource demand and automatically scale the number of pods. By default, the HPA checks the Metrics API every 15 seconds for any required changes in replica count, while the Metrics API retrieves data from the Kubelet every 60 seconds. As a result, HPA is updated every 60 seconds. When changes are required, the number of replicas is scaled accordingly. HPA works with AKS clusters that have deployed Metrics Server for Kubernetes version 1.8 and higher.

When you configure the HPA for a given deployment, you define the minimum and maximum number of replicas that can run. You also define the metric to monitor and base scaling decisions on, such as CPU usage.

To get started with the horizontal pod autoscaler in AKS, see [Autoscale pods in AKS](tutorial-kubernetes-scale#autoscale-pods).

### Cooldown of scaling events

As the HPA is effectively updated every 60 seconds, previous scale events might not have successfully completed before another check is made. This behavior could cause the HPA to change the number of replicas before the previous scale event could receive application workload and the resource demands to adjust accordingly.

To minimize race events, a delay value is set. This value defines how long the HPA must wait after a scale event before another scale event can be triggered. This behavior allows the new replica count to take effect and the Metrics API to reflect the distributed workload. There's [no delay for scale-up events as of Kubernetes 1.12](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/#support-for-cooldown-delay). However, the default delay on scale down events is *5 minutes*.

## Cluster autoscaler

To respond to changing pod demands, the Kubernetes cluster autoscaler adjusts the number of nodes based on the requested compute resources in the node pool. By default, the cluster autoscaler checks the Metrics API server every 10 seconds for any required changes in node count. If the cluster autoscaler determines that a change is required, the number of nodes in your AKS cluster is increased or decreased accordingly. The cluster autoscaler works with Kubernetes RBAC-enabled AKS clusters that run Kubernetes 1.10.x or higher.

The cluster autoscaler is typically used alongside the [horizontal pod autoscaler](#horizontal-pod-autoscaler). When combined, the horizontal pod autoscaler increases or decreases the number of pods based on application demand, and the cluster autoscaler adjusts the number of nodes to run more pods.

To get started with the cluster autoscaler in AKS, see [Cluster autoscaler on AKS](cluster-autoscaler).

### Scale out events

If a node doesn't have sufficient compute resources to run a requested pod, that pod can't progress through the scheduling process. The pod can't start unless more compute resources are made available within the node pool.

When the cluster autoscaler notices pods that can't be scheduled because of node pool resource constraints, the number of nodes within the node pool is increased to provide extra compute resources. When the nodes are successfully deployed and available for use within the node pool, the pods are then scheduled to run on them.

If your application needs to scale rapidly, some pods might remain in a state of waiting to be scheduled until more nodes deployed by the cluster autoscaler can accept the scheduled pods. For applications that have high burst demands, you can scale with virtual nodes and [Azure Container Instances](#burst-to-azure-container-instances-aci).

### Scale in events

The cluster autoscaler also monitors the pod scheduling status for nodes that haven't recently received new scheduling requests. This scenario indicates the node pool has more compute resources than required, and the number of nodes can be decreased. By default, nodes that pass a threshold of no longer being needed for 10 minutes are scheduled for deletion. When this situation occurs, pods are scheduled to run on other nodes within the node pool, and the cluster autoscaler decreases the number of nodes.

Your applications might experience some disruption as pods are scheduled on different nodes when the cluster autoscaler decreases the number of nodes. To minimize disruption, avoid applications that use a single pod instance.

## Kubernetes Event-driven Autoscaling (KEDA)

[Kubernetes Event-driven Autoscaling](https://keda.sh/docs/2.13/concepts/) (KEDA) is an open source component for event-driven autoscaling of workloads. It scales workloads dynamically based on the number of events received. KEDA extends Kubernetes with a custom resource definition (CRD), referred to as a *ScaledObject*, to describe how applications should be scaled in response to specific traffic.

KEDA scaling is useful in scenarios where workloads receive bursts of traffic or handle high volumes of data. KEDA differs from the Horizontal Pod Autoscaler as KEDA is event-driven and scales based on the number of events, while HPA is metrics-driven based on the resource utilization (for example, CPU and memory).

To get started with the KEDA add-on in AKS, see [KEDA overview](keda-about).

## Node Autoprovisioning

[Node autoprovisioning (preview)](node-autoprovision) (NAP), uses the open source Karpenter project that automatically deploys, configures, and manages [Karpenter](https://karpenter.sh/) on your AKS cluster. NAP dynamically provisions nodes based on pending pod resource requirements; it'll automatically select the optimal virtual machine (VM) SKU and quantity to meet real-time demand.

NAP takes a predefined list of VM SKUs as the starting point to decide which SKU is best suited for pending workloads. For more precise control, users can define the upper limits of resources used by a node pool and preferences of where workloads should be scheduled if there are multiple node pools.

## Control Plane Scaling and Safeguards

Kubernetes has a multi-dimensional scale envelope with each resource type representing a dimension. Not all resources are alike. For example, watches are commonly set on secrets, which result in list calls to the kube-apiserver that add cost and a disproportionately higher load on the control plane compared to resources without watches.

The control plane manages all the resource scaling in the cluster, so the more you scale the cluster within a given dimension, the less you can scale within other dimensions. For example, running hundreds of thousands of pods in an AKS cluster impacts how much pod churn rate (pod mutations per second) the control plane can support. Refer to ** best practices**.

AKS automatically scales control plane components based on key signals such as the total number of cores in the cluster and CPU or memory pressure on the control plane components.

To verify whether the control plane has scaled up, check the ConfigMap named 'large-cluster-control-plane-scaling-status'

```
kubectl describe configmap large-cluster-control-plane-scaling-status -n kube-system
```


### Control Plane Safeguards

If scaling the API server automatically does not stabilize it under high load scenarios, AKS deploys a managed API server guard. This guard acts as a last-resort mechanism to protect the API server by throttling non-system client requests and preventing the control plane from becoming completely unresponsive. System-critical calls to API server from components such as kubelet will continue to function normally.

To verify whether the managed API server guard has been applied, check for the presence of **"aks-managed-apiserver-guard"** FlowSchema and PriorityLevelConfiguration.

```
kubectl get flowschemas
kubectl get prioritylevelconfigurations
```


Refer to [API server and Etcd Troubleshooting guide](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-apiserver-etcd#cause-4-aks-managed-api-server-guard-was-applied) if the **"aks-managed-apiserver-guard"** FlowSchema and PriorityLevelConfiguration have been applied on the cluster for quick mitigation.

## Burst to Azure Container Instances (ACI)

To rapidly scale your AKS cluster, you can integrate with Azure Container Instances (ACI). Kubernetes has built-in components to scale the replica and node count. However, if your application needs to rapidly scale, the [horizontal pod autoscaler](#horizontal-pod-autoscaler) might schedule more pods than what the existing compute resources in the node pool can support. If configured, this scenario would then trigger the [cluster autoscaler](#cluster-autoscaler) to deploy more nodes in the node pool, but it might take a few minutes for those nodes to successfully provision and allow the Kubernetes scheduler to run pods on them.

ACI lets you quickly deploy container instances without extra infrastructure overhead. When you connect with AKS, ACI becomes a secured, logical extension of your AKS cluster. The [virtual nodes](virtual-nodes-cli) component, which is based on [virtual Kubelet](https://virtual-kubelet.io/), is installed in your AKS cluster that presents ACI as a virtual Kubernetes node. Kubernetes can then schedule pods that run as ACI instances through virtual nodes, not as pods on VM nodes directly in your AKS cluster.

Your application requires no modifications to use virtual nodes. Your deployments can scale across AKS and ACI and with no delay as the cluster autoscaler deploys new nodes in your AKS cluster.

Virtual nodes are deployed to another subnet in the same virtual network as your AKS cluster. This virtual network configuration secures the traffic between ACI and AKS. Like an AKS cluster, an ACI instance is a secure, logical compute resource isolated from other users.

## Next steps

To get started with scaling applications, see the following resources:

- Manually scale
[pods](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_scale/)or[nodes](scale-cluster) - Use the
[horizontal pod autoscaler](tutorial-kubernetes-scale#autoscale-pods) - Use the
[cluster autoscaler](cluster-autoscaler) - Use the
[Kubernetes Event-driven Autoscaling (KEDA) add-on](keda-about)

For more information on core Kubernetes and AKS concepts, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/start-stop-cluster -->

# Stop and start an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You may not need to continuously run your Azure Kubernetes Service (AKS) workloads. For example, you may have a development cluster that you only use during business hours. This means there are times where your cluster might be idle, running nothing more than the system components. You can reduce the cluster footprint by [scaling all User node pools to 0](scale-cluster#scale-user-node-pools-to-0), but your

[is still required to run the system components while the cluster is running.](use-system-pools)

`System`

poolTo better optimize your costs during these periods, you can turn off, or stop, your cluster. This action stops your control plane and agent nodes, allowing you to save on all the compute costs, while maintaining all objects except standalone pods. The cluster state is stored for when you start it again, allowing you to pick up where you left off.

Caution

Stopping your cluster deallocates the control plane and releases the capacity. In regions experiencing capacity constraints, customers may be unable to start a stopped cluster. We do not recommend stopping mission critical workloads for this reason.

Note

AKS start operations will restore all objects from ETCD with the exception of standalone pods with the same names and ages. meaning that a pod's age will continue to be calculated from its original creation time. This count will keep increasing over time, regardless of whether the cluster is in a stopped state.

## Before you begin

This article assumes you have an existing AKS cluster. If you need an AKS cluster, you can create one using [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

### About the cluster stop/start feature

When using the cluster stop/start feature, the following conditions apply:

- This feature is only supported for Virtual Machine Scale Set backed clusters.
- You can't stop clusters which use the
[Node Autoprovisioning (NAP)](node-autoprovision)feature. - The cluster state of a stopped AKS cluster is preserved for up to 12 months. If your cluster is stopped for more than 12 months, you can't recover the state. For more information, see the
[AKS support policies](support-policies). - You can only perform start or delete operations on a stopped AKS cluster. To perform other operations, like scaling or upgrading, you need to start your cluster first.
- If you provisioned PrivateEndpoints linked to private clusters, they need to be deleted and recreated again when starting a stopped AKS cluster.
- Because the stop process drains all nodes, any standalone pods (i.e. pods not managed by a Deployment, StatefulSet, DaemonSet, Job, etc.) will be deleted.
- When you start your cluster back up, the following behavior is expected:
- The IP address of your API server may change.
- If you're using cluster autoscaler, when you start your cluster, your current node count may not be between the min and max range values you set. The cluster starts with the number of nodes it needs to run its workloads, which isn't impacted by your autoscaler settings. When your cluster performs scaling operations, the min and max values will impact your current node count, and your cluster will eventually enter and remain in that desired range until you stop your cluster.


## Stop an AKS cluster

Use the

command to stop a running AKS cluster, including the nodes and control plane. The following example stops a cluster named`az aks stop`

*myAKSCluster*:`az aks stop --name myAKSCluster --resource-group myResourceGroup`

Verify your cluster has stopped using the

command and confirming the`az aks show`

`powerState`

shows as`Stopped`

.`az aks show --name myAKSCluster --resource-group myResourceGroup`

Your output should look similar to the following condensed example output:

`{ [...] "nodeResourceGroup": "MC_myResourceGroup_myAKSCluster_westus2", "powerState":{ "code":"Stopped" }, "privateFqdn": null, "provisioningState": "Succeeded", "resourceGroup": "myResourceGroup", [...] }`

If the

`provisioningState`

shows`Stopping`

, your cluster hasn't fully stopped yet.

Important

If you're using [pod disruption budgets](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/), the stop operation can take longer, as the drain process will take more time to complete.

## Start an AKS cluster

Caution

After utilizing the start/stop feature on AKS, it is essential to wait 15-30 minutes before restarting your AKS cluster. This waiting period is necessary because it takes several minutes for the relevant services to fully stop. Attempting to restart your cluster during this process can disrupt the shutdown process and potentially cause issues with the cluster or its workloads.

Use the

command to start a stopped AKS cluster. The cluster restarts with the previous control plane state and number of agent nodes. The following example starts a cluster named`az aks start`

*myAKSCluster*:`az aks start --name myAKSCluster --resource-group myResourceGroup`

Verify your cluster has started using the

command and confirming the`az aks show`

`powerState`

shows`Running`

.`az aks show --name myAKSCluster --resource-group myResourceGroup`

Your output should look similar to the following condensed example output:

`{ [...] "nodeResourceGroup": "MC_myResourceGroup_myAKSCluster_westus2", "powerState":{ "code":"Running" }, "privateFqdn": null, "provisioningState": "Succeeded", "resourceGroup": "myResourceGroup", [...] }`

If the

`provisioningState`

shows`Starting`

, your cluster hasn't fully started yet.

## Next steps

- To learn how to scale
`User`

pools to 0, see[Scale](scale-cluster#scale-user-node-pools-to-0).`User`

pools to 0 - To learn how to save costs using Spot instances, see
[Add a spot node pool to AKS](spot-node-pool). - To learn more about the AKS support policies, see
[AKS support policies](support-policies).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-ai-ml-language-models -->

# Concepts - Small and large language models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about small and large language models, including when to use them and how you can use them with your AI and machine learning workflows on Azure Kubernetes Service (AKS).

## What are language models?

Language models are powerful machine learning models used for natural language processing (NLP) tasks, such as text generation and sentiment analysis. These models represent natural language based on the probability of words or sequences of words occurring in a given context.

*Conventional language models* have been used in supervised settings for research purposes where the models are trained on well-labeled text datasets for specific tasks. *Pre-trained language models* offer an accessible way to get started with AI and have become more widely used in recent years. These models are trained on large-scale text corpora from the internet using deep neural networks and can be fine-tuned on smaller datasets for specific tasks.

The size of a language model is determined by its number of parameters, or *weights*, that determine how the model processes input data and generates output. Parameters are learned during the training process by adjusting the weights within layers of the model to minimize the difference between the model's predictions and the actual data. The more parameters a model has, the more complex and expressive it is, but also the more computationally expensive it is to train and use.

In general, **small language models** have *fewer than 10 billion parameters*, and **large language models** have *more than 10 billion parameters*. For example, the new Microsoft Phi-3 model family has three versions with different sizes: mini (3.8 billion parameters), small (7 billion parameters), and medium (14 billion parameters).

## When to use small language models

### Advantages

Small language models are a good choice if you want models that are:

**Faster and more cost-effective to train and run**: They require less data and compute power.**Easy to deploy and maintain**: They have smaller storage and memory footprints.**Less prone to**, which is when a model learns the noise or specific patterns of the training data and fails to generalize new data.*overfitting***Interpretable and explainable**: They have fewer parameters and components to understand and analyze.

### Use cases

Small language models are suitable for use cases that require:

**Limited data or resources**, and you need a quick and simple solution.**Well-defined or narrow tasks**, and you don't need much creativity in the output.**High-precision and low-recall tasks**, and you value accuracy and quality over coverage and quantity.**Sensitive or regulated tasks**, and you need to ensure the transparency and accountability of the model.

The following table lists some popular, high-performance small language models:

| Model family | Model sizes (Number of parameters) | Software license |
|---|---|---|
| Microsoft Phi-3 | Phi-3-mini (3.8 billion), Phi-3-small (7 billion) | MIT license |
| Microsoft Phi-2 | Phi-2 (2.7 billion) | MIT license |
| Falcon | Falcon-7B (7 billion) | Apache 2.0 license |

## When to use large language models

### Advantages

Large language models are a good choice if you want models that are:

**Powerful and expressive**: They can capture more complex patterns and relationships in the data.**General and adaptable**: They can handle a wider range of tasks and transfer knowledge across domains.**Robust and consistent**: They can handle noisy or incomplete inputs and avoid common errors and biases.

### Use cases

Large language models are suitable for use cases that require:

**Abundant data and resources**, and you have the budget to build and maintain a complex solution.**Low-precision and high-recall tasks**, and you value coverage and quantity over accuracy and quality.**Challenging or exploratory tasks**, and you want to leverage the model's capacity to learn and adapt.

The following table lists some popular, high-performance large language models:

| Model family | Model sizes (Number of parameters) | Software license |
|---|---|---|
| Microsoft Phi-3 | Phi-3-medium (14 billion) | MIT license |
| Falcon | Falcon-40B (40 billion) | Apache 2.0 license |

## Experiment with small and large language models on AKS

Kubernetes AI Toolchain Operator (KAITO) is an open-source operator that automates small and large language model deployments in Kubernetes clusters. The KAITO add-on for AKS simplifies onboarding and reduces the time-to-inference for open-source models on your AKS clusters. The add-on automatically provisions right-sized GPU nodes and sets up the associated interference server as an endpoint server to your chosen model.

For more information, see [Deploy an AI model on AKS with the AI toolchain operator](ai-toolchain-operator). To get started with a range of supported small and large language models for your inference workflows, see the [KAITO model GitHub repository](https://github.com/Azure/kaito/tree/main/presets).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Next steps

To learn more about containerized AI and machine learning workloads on AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-node-image -->

# Autoupgrade node OS images

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS provides multiple autoupgrade channels dedicated to timely node-level OS security updates. This channel is different from cluster-level Kubernetes version upgrades and supersedes it.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Interactions between node OS autoupgrade and cluster autoupgrade

Node-level OS security updates are released at a faster rate than Kubernetes patch or minor version updates. The node OS autoupgrade channel grants you flexibility and enables a customized strategy for node-level OS security updates. Then, you can choose a separate plan for cluster-level Kubernetes version [autoupgrades](auto-upgrade-cluster).
It's best to use both cluster-level [autoupgrades](auto-upgrade-cluster) and the node OS autoupgrade channel together. Scheduling can be fine-tuned by applying two separate sets of [maintenance windows](planned-maintenance) - `aksManagedAutoUpgradeSchedule`

for the cluster [autoupgrade](auto-upgrade-cluster) channel and `aksManagedNodeOSUpgradeSchedule`

for the node OS autoupgrade channel.

## Channels for node OS image upgrades

The selected channel determines the timing of upgrades. When making changes to node OS auto-upgrade channels, allow up to 24 hours for the changes to take effect.

Note

- Node OS image auto-upgrade don't affect the cluster's Kubernetes version.
- Starting with API version 2023-06-01, the default for any new AKS cluster is
`NodeImage`

.

### Node OS channel changes that cause a reimage

The following node os channel transitions will trigger reimage on the nodes:

| From | To |
|---|---|
| Unmanaged | None |
| Unspecified | Unmanaged |
| SecurityPatch | Unmanaged |
| NodeImage | Unmanaged |
| None | Unmanaged |

### Available node OS upgrade channels

The following upgrade channels are available. You're allowed to choose one of these options:

| Channel | Description | OS-specific behavior |
|---|---|---|
`None` |
Your nodes don't have security updates applied automatically. This means you're solely responsible for your security updates. | N/A |
`Unmanaged` |
The OS built-in patching infrastructure automatically applies OS updates. Newly allocated machines are initially unpatched. The OS's infrastructure patches them at some point. | Ubuntu and Azure Linux (CPU node pools) apply security patches through unattended upgrade/dnf-automatic roughly once per day around 06:00 UTC. Windows doesn't automatically apply security patches, so this option behaves equivalently to `None` . You need to manage the reboot process using a tool like
`Unmanaged` . |
`SecurityPatch` |
OS security patches, which are AKS-tested, fully managed, and applied with safe deployment practices. AKS regularly updates the node's virtual hard disk (VHD) with patches from the image maintainer labeled "security only." There might be disruptions when the security patches are applied to the nodes. However AKS is limiting disruptions by only reimaging your nodes only when necessary, such as for certain kernel security packages. When the patches are applied, the VHD is updated and existing machines are upgraded to that VHD, honoring maintenance windows and surge settings. If AKS decides that reimaging nodes isn't necessary, it patches nodes live without draining pods and performs no VHD update. This option incurs the extra cost of hosting the VHDs in your node resource group. If you use this channel, Linux
|

`SecurityPatch`

works on kubernetes patch versions that are deprecated, so long as the minor Kubernetes version is still supported. [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks)and[Azure Linux with OS Guard on AKS](use-azure-linux-os-guard)do not support`SecurityPatch`

.`NodeImage`

[unattended upgrades](https://help.ubuntu.com/community/AutomaticSecurityUpdates)are disabled by default. Node image upgrades are supported as long as cluster Kubernetes minor version is still in support. Node images are AKS-tested, fully managed, and applied with safe deployment practices.## What to choose - SecurityPatch Channel or NodeImage Channel?

There are two important considerations for you to choose between `SecurityPatch`

or `NodeImage`

channels.

| Property | NodeImage Channel | SecurityPatch Channel | Recommended Channel |
|---|---|---|---|
`Speed of shipping` |
The typical build, test, release, and rollout timelines for a new VHD can take approximately two weeks following safe deployment practices. Although in the event of CVEs, accelerated rollouts can occur on a case by case basis. The exact timing when a new VHD hits a region can be monitored via
|

`NodeImage`

, even with safe deployment practices. SecurityPatch has the advantage of 'Live-patching' in Linux environments, where patching leads to selective 'reimaging' and doesn't reimage every time a patch gets applied. Re-image if it happens is controlled by maintenance windows.`SecurityPatch`

`Bugfixes`

`NodeImage`

## Set the node OS autoupgrade channel on a new cluster

- Set the node OS autoupgrade channel on a new cluster using the
command with the`az aks create`

`--node-os-upgrade-channel`

parameter. The following example sets the node OS autoupgrade channel to`SecurityPatch`

.

```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="myResourceGroup$RANDOM_SUFFIX"
export AKS_CLUSTER="myAKSCluster$RANDOM_SUFFIX"
az aks create \
--resource-group $RESOURCE_GROUP \
--name $AKS_CLUSTER \
--node-os-upgrade-channel SecurityPatch \
--generate-ssh-keys
```


## Set the node OS autoupgrade channel on an existing cluster

- Set the node os autoupgrade channel on an existing cluster using the
command with the`az aks update`

`--node-os-upgrade-channel`

parameter. The following example sets the node OS autoupgrade channel to`SecurityPatch`

.

```
az aks update --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER --node-os-upgrade-channel SecurityPatch
```


Results:

```
{
"autoUpgradeProfile": {
"nodeOsUpgradeChannel": "SecurityPatch"
}
}
```


## Update ownership and schedule

The default cadence means there's no planned maintenance window applied.

| Channel | Updates Ownership | Default cadence |
|---|---|---|
`Unmanaged` |
OS driven security updates. AKS has no control over these updates. | Nightly around 6AM UTC for Ubuntu and Azure Linux. Monthly for Windows. |
`SecurityPatch` |
AKS-tested, fully managed, and applied with safe deployment practices. For more information, see
|

`NodeImage`

[AKS Node Images in Release tracker](release-tracker)Note

While Windows security updates are released on a monthly basis, using the `Unmanaged`

channel won't automatically apply these updates to Windows nodes. If you choose the `Unmanaged`

channel, you need to manage the reboot process for Windows nodes.

## Node channel known limitations

Currently, when you set the

[cluster autoupgrade channel](auto-upgrade-cluster)to`node-image`

, it also automatically sets the node OS autoupgrade channel to`NodeImage`

. You can't change node OS autoupgrade channel value if your cluster autoupgrade channel is`node-image`

. In order to set the node OS autoupgrade channel value, check the[cluster autoupgrade channel](auto-upgrade-cluster)value isn't`node-image`

.The

`SecurityPatch`

channel isn't supported on Windows OS node pools.

Note

Use CLI version 2.61.0 or above for the `SecurityPatch`

channel.

## Node OS planned maintenance windows

Planned maintenance for the node OS autoupgrade starts at your specified maintenance window.

Note

To ensure proper functionality, use a maintenance window of four hours or more.

For more information on Planned Maintenance, see [Use Planned Maintenance to schedule maintenance windows for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Node OS autoupgrades FAQ

### How can I check the current nodeOsUpgradeChannel value on a cluster?

Run the `az aks show`

command and check the "autoUpgradeProfile" to determine what value the `nodeOsUpgradeChannel`

is set to:

```
az aks show --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER --query "autoUpgradeProfile"
```


Results:

```
{
"nodeOsUpgradeChannel": "SecurityPatch"
}
```


### How can I monitor the status of node OS autoupgrades?

To view the status of your node OS auto upgrades, look up [activity logs](monitor-aks-reference) on your cluster. You can also look up specific upgrade-related events as mentioned in [Upgrade an AKS cluster](upgrade-cluster). AKS also emits upgrade-related Event Grid events. To learn more, see [AKS as an Event Grid source](quickstart-event-grid).

### Can I change the node OS autoupgrade channel value if my cluster autoupgrade channel is set to `node-image`

?

No. Currently, when you set the [cluster autoupgrade channel](auto-upgrade-cluster) to `node-image`

, it also automatically sets the node OS autoupgrade channel to `NodeImage`

. You can't change the node OS autoupgrade channel value if your cluster autoupgrade channel is `node-image`

. In order to be able to change the node OS autoupgrade channel values, make sure the [cluster autoupgrade channel](auto-upgrade-cluster) isn't `node-image`

.

### Why is `SecurityPatch`

recommended over `Unmanaged`

channel?

On the `Unmanaged`

channel, AKS has no control over how and when the security updates are delivered. With `SecurityPatch`

, the security updates are fully tested and follow safe deployment practices. `SecurityPatch`

also honors maintenance windows. For more information, see [Increased security and resiliency of Canonical workloads on Azure](https://techcommunity.microsoft.com/t5/linux-and-open-source-blog/increased-security-and-resiliency-of-canonical-workloads-on/ba-p/3970623).

### Does `SecurityPatch`

always lead to a reimage of my nodes?

AKS limits reimages to only when necessary, such as certain kernel packages that may require a reimage to get fully applied. `SecurityPatch`

is designed to minimize disruptions as much as possible. If AKS decides reimaging nodes isn't necessary, it patches nodes live without draining pods and no VHD update is performed in such cases.

### Why does `SecurityPatch`

channel requires to reach `snapshot.ubuntu.com`

endpoint?

With the `SecurityPatch`

channel, the Linux cluster nodes have to download the required security patches and updates from ubuntu snapshot service described in [ubuntu-snapshots-on-azure-ensuring-predictability-and-consistency-in-cloud-deployments](https://ubuntu.com/blog/ubuntu-snapshots-on-azure-ensuring-predictability-and-consistency-in-cloud-deployments).

### How do I know if a `SecurityPatch`

or `NodeImage`

upgrade is applied on my node?

Run the `kubectl get nodes --show-labels`

command to list the nodes in your cluster and their labels.

Among the returned labels, you should see a line similar to the following output:

```
kubernetes.azure.com/node-image-version=AKSUbuntu-2204gen2containerd-202410.27.0-2024.12.01
```


Here, the base node image version is `AKSUbuntu-2204gen2containerd-202410.27.0`

. If applicable, the security patch version typically follows. In the above example, it's `2024.12.01`

.

The same details also be looked up in the Azure portal under the node label view:

## Next steps

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-node-os-image -->

# Autoupgrade node OS images

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS provides multiple autoupgrade channels dedicated to timely node-level OS security updates. This channel is different from cluster-level Kubernetes version upgrades and supersedes it.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Interactions between node OS autoupgrade and cluster autoupgrade

Node-level OS security updates are released at a faster rate than Kubernetes patch or minor version updates. The node OS autoupgrade channel grants you flexibility and enables a customized strategy for node-level OS security updates. Then, you can choose a separate plan for cluster-level Kubernetes version [autoupgrades](auto-upgrade-cluster).
It's best to use both cluster-level [autoupgrades](auto-upgrade-cluster) and the node OS autoupgrade channel together. Scheduling can be fine-tuned by applying two separate sets of [maintenance windows](planned-maintenance) - `aksManagedAutoUpgradeSchedule`

for the cluster [autoupgrade](auto-upgrade-cluster) channel and `aksManagedNodeOSUpgradeSchedule`

for the node OS autoupgrade channel.

## Channels for node OS image upgrades

The selected channel determines the timing of upgrades. When making changes to node OS auto-upgrade channels, allow up to 24 hours for the changes to take effect.

Note

- Node OS image auto-upgrade don't affect the cluster's Kubernetes version.
- Starting with API version 2023-06-01, the default for any new AKS cluster is
`NodeImage`

.

### Node OS channel changes that cause a reimage

The following node os channel transitions will trigger reimage on the nodes:

| From | To |
|---|---|
| Unmanaged | None |
| Unspecified | Unmanaged |
| SecurityPatch | Unmanaged |
| NodeImage | Unmanaged |
| None | Unmanaged |

### Available node OS upgrade channels

The following upgrade channels are available. You're allowed to choose one of these options:

| Channel | Description | OS-specific behavior |
|---|---|---|
`None` |
Your nodes don't have security updates applied automatically. This means you're solely responsible for your security updates. | N/A |
`Unmanaged` |
The OS built-in patching infrastructure automatically applies OS updates. Newly allocated machines are initially unpatched. The OS's infrastructure patches them at some point. | Ubuntu and Azure Linux (CPU node pools) apply security patches through unattended upgrade/dnf-automatic roughly once per day around 06:00 UTC. Windows doesn't automatically apply security patches, so this option behaves equivalently to `None` . You need to manage the reboot process using a tool like
`Unmanaged` . |
`SecurityPatch` |
OS security patches, which are AKS-tested, fully managed, and applied with safe deployment practices. AKS regularly updates the node's virtual hard disk (VHD) with patches from the image maintainer labeled "security only." There might be disruptions when the security patches are applied to the nodes. However AKS is limiting disruptions by only reimaging your nodes only when necessary, such as for certain kernel security packages. When the patches are applied, the VHD is updated and existing machines are upgraded to that VHD, honoring maintenance windows and surge settings. If AKS decides that reimaging nodes isn't necessary, it patches nodes live without draining pods and performs no VHD update. This option incurs the extra cost of hosting the VHDs in your node resource group. If you use this channel, Linux
|

`SecurityPatch`

works on kubernetes patch versions that are deprecated, so long as the minor Kubernetes version is still supported. [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks)and[Azure Linux with OS Guard on AKS](use-azure-linux-os-guard)do not support`SecurityPatch`

.`NodeImage`

[unattended upgrades](https://help.ubuntu.com/community/AutomaticSecurityUpdates)are disabled by default. Node image upgrades are supported as long as cluster Kubernetes minor version is still in support. Node images are AKS-tested, fully managed, and applied with safe deployment practices.## What to choose - SecurityPatch Channel or NodeImage Channel?

There are two important considerations for you to choose between `SecurityPatch`

or `NodeImage`

channels.

| Property | NodeImage Channel | SecurityPatch Channel | Recommended Channel |
|---|---|---|---|
`Speed of shipping` |
The typical build, test, release, and rollout timelines for a new VHD can take approximately two weeks following safe deployment practices. Although in the event of CVEs, accelerated rollouts can occur on a case by case basis. The exact timing when a new VHD hits a region can be monitored via
|

`NodeImage`

, even with safe deployment practices. SecurityPatch has the advantage of 'Live-patching' in Linux environments, where patching leads to selective 'reimaging' and doesn't reimage every time a patch gets applied. Re-image if it happens is controlled by maintenance windows.`SecurityPatch`

`Bugfixes`

`NodeImage`

## Set the node OS autoupgrade channel on a new cluster

- Set the node OS autoupgrade channel on a new cluster using the
command with the`az aks create`

`--node-os-upgrade-channel`

parameter. The following example sets the node OS autoupgrade channel to`SecurityPatch`

.

```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="myResourceGroup$RANDOM_SUFFIX"
export AKS_CLUSTER="myAKSCluster$RANDOM_SUFFIX"
az aks create \
--resource-group $RESOURCE_GROUP \
--name $AKS_CLUSTER \
--node-os-upgrade-channel SecurityPatch \
--generate-ssh-keys
```


## Set the node OS autoupgrade channel on an existing cluster

- Set the node os autoupgrade channel on an existing cluster using the
command with the`az aks update`

`--node-os-upgrade-channel`

parameter. The following example sets the node OS autoupgrade channel to`SecurityPatch`

.

```
az aks update --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER --node-os-upgrade-channel SecurityPatch
```


Results:

```
{
"autoUpgradeProfile": {
"nodeOsUpgradeChannel": "SecurityPatch"
}
}
```


## Update ownership and schedule

The default cadence means there's no planned maintenance window applied.

| Channel | Updates Ownership | Default cadence |
|---|---|---|
`Unmanaged` |
OS driven security updates. AKS has no control over these updates. | Nightly around 6AM UTC for Ubuntu and Azure Linux. Monthly for Windows. |
`SecurityPatch` |
AKS-tested, fully managed, and applied with safe deployment practices. For more information, see
|

`NodeImage`

[AKS Node Images in Release tracker](release-tracker)Note

While Windows security updates are released on a monthly basis, using the `Unmanaged`

channel won't automatically apply these updates to Windows nodes. If you choose the `Unmanaged`

channel, you need to manage the reboot process for Windows nodes.

## Node channel known limitations

Currently, when you set the

[cluster autoupgrade channel](auto-upgrade-cluster)to`node-image`

, it also automatically sets the node OS autoupgrade channel to`NodeImage`

. You can't change node OS autoupgrade channel value if your cluster autoupgrade channel is`node-image`

. In order to set the node OS autoupgrade channel value, check the[cluster autoupgrade channel](auto-upgrade-cluster)value isn't`node-image`

.The

`SecurityPatch`

channel isn't supported on Windows OS node pools.

Note

Use CLI version 2.61.0 or above for the `SecurityPatch`

channel.

## Node OS planned maintenance windows

Planned maintenance for the node OS autoupgrade starts at your specified maintenance window.

Note

To ensure proper functionality, use a maintenance window of four hours or more.

For more information on Planned Maintenance, see [Use Planned Maintenance to schedule maintenance windows for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Node OS autoupgrades FAQ

### How can I check the current nodeOsUpgradeChannel value on a cluster?

Run the `az aks show`

command and check the "autoUpgradeProfile" to determine what value the `nodeOsUpgradeChannel`

is set to:

```
az aks show --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER --query "autoUpgradeProfile"
```


Results:

```
{
"nodeOsUpgradeChannel": "SecurityPatch"
}
```


### How can I monitor the status of node OS autoupgrades?

To view the status of your node OS auto upgrades, look up [activity logs](monitor-aks-reference) on your cluster. You can also look up specific upgrade-related events as mentioned in [Upgrade an AKS cluster](upgrade-cluster). AKS also emits upgrade-related Event Grid events. To learn more, see [AKS as an Event Grid source](quickstart-event-grid).

### Can I change the node OS autoupgrade channel value if my cluster autoupgrade channel is set to `node-image`

?

No. Currently, when you set the [cluster autoupgrade channel](auto-upgrade-cluster) to `node-image`

, it also automatically sets the node OS autoupgrade channel to `NodeImage`

. You can't change the node OS autoupgrade channel value if your cluster autoupgrade channel is `node-image`

. In order to be able to change the node OS autoupgrade channel values, make sure the [cluster autoupgrade channel](auto-upgrade-cluster) isn't `node-image`

.

### Why is `SecurityPatch`

recommended over `Unmanaged`

channel?

On the `Unmanaged`

channel, AKS has no control over how and when the security updates are delivered. With `SecurityPatch`

, the security updates are fully tested and follow safe deployment practices. `SecurityPatch`

also honors maintenance windows. For more information, see [Increased security and resiliency of Canonical workloads on Azure](https://techcommunity.microsoft.com/t5/linux-and-open-source-blog/increased-security-and-resiliency-of-canonical-workloads-on/ba-p/3970623).

### Does `SecurityPatch`

always lead to a reimage of my nodes?

AKS limits reimages to only when necessary, such as certain kernel packages that may require a reimage to get fully applied. `SecurityPatch`

is designed to minimize disruptions as much as possible. If AKS decides reimaging nodes isn't necessary, it patches nodes live without draining pods and no VHD update is performed in such cases.

### Why does `SecurityPatch`

channel requires to reach `snapshot.ubuntu.com`

endpoint?

With the `SecurityPatch`

channel, the Linux cluster nodes have to download the required security patches and updates from ubuntu snapshot service described in [ubuntu-snapshots-on-azure-ensuring-predictability-and-consistency-in-cloud-deployments](https://ubuntu.com/blog/ubuntu-snapshots-on-azure-ensuring-predictability-and-consistency-in-cloud-deployments).

### How do I know if a `SecurityPatch`

or `NodeImage`

upgrade is applied on my node?

Run the `kubectl get nodes --show-labels`

command to list the nodes in your cluster and their labels.

Among the returned labels, you should see a line similar to the following output:

```
kubernetes.azure.com/node-image-version=AKSUbuntu-2204gen2containerd-202410.27.0-2024.12.01
```


Here, the base node image version is `AKSUbuntu-2204gen2containerd-202410.27.0`

. If applicable, the security patch version typically follows. In the above example, it's `2024.12.01`

.

The same details also be looked up in the Azure portal under the node label view:

## Next steps

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-advanced-container-networking-services -->

# Use Advanced Container Networking Services on your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to enable and disable Advanced Container Networking Services, including [Container Network Observability](advanced-container-networking-services-overview#container-network-observability) and [Container Network Security](advanced-container-networking-services-overview#container-network-security), on your AKS clusters.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - Azure CLI version 2.71.0 or higher. Find your version using the
`az --version`

command. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). [Install the](#install-the-aks-preview-azure-cli-extension)version`aks-preview`

Azure CLI extension`14.0.0b6`

or higher.[Register the](#register-the-advancednetworkingl7policypreview-feature-flag)in your subscription.`AdvancedNetworkingL7PolicyPreview`

feature flag- Clusters that have the Cilium data plane support
*Container Network Observability*and*Container Network Security*in Kubernetes version 1.29 and later.

## Install the `aks-preview`

Azure CLI extension

Install or update the Azure CLI preview extension using the

or`az extension add`

command.`az extension update`

`# Install the aks-preview extension az extension add --name aks-preview # Update the extension to make sure you have the latest version installed az extension update --name aks-preview`


## Register the `AdvancedNetworkingL7PolicyPreview`

feature flag

Register the

`AdvancedNetworkingL7PolicyPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"`

Registration takes a few minutes to complete.

Verify successful registration using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"`


## Set environment variables

The examples in this article use the following environment variables:

| Variable | Description | Example value |
|---|---|---|
`RESOURCE_GROUP` |
Name of the Azure resource group | `myResourceGroup` |
`LOCATION` |
Azure region for resources | `eastus` |
`CLUSTER_NAME` |
Name of the AKS cluster | `myAKSCluster` |

**All commands in this article assume these environment variables are set**. Make sure to replace the example values with your own values.

## Create a resource group

Create a resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`


## Create a new AKS cluster with Advanced Container Networking Services

Note

When the `--acns-advanced-networkpolicies`

parameter is set to `L7`

, both Layer 7 and fully qualified domain name (FQDN) filtering policies are enabled. If you want to enable only FQDN filtering, set the parameter to `FQDN`

.

Create an AKS cluster with Advanced Container Networking Services and Cilium using the

command with the`az aks create`

`--enable-acns`

and`--network-dataplane cilium`

flags.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --network-plugin azure \ --network-plugin-mode overlay \ --network-dataplane cilium \ --kubernetes-version 1.29 \ --enable-acns \ --acns-advanced-networkpolicies <L7/FQDN>`


Important

The [Container Network Security](advanced-container-networking-services-overview#container-network-security) feature isn't available for non-Cilium clusters.

Create an AKS cluster with Advanced Container Networking Services using the

command with the`az aks create`

`--enable-acns`

flag.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --network-plugin azure \ --network-plugin-mode overlay \ --enable-acns`


## Enable Advanced Container Networking Services on an existing cluster

Enable Advanced Container Networking Services on an existing AKS cluster with Cilium using the

command with the`az aks update`

`--enable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --acns-advanced-networkpolicies <L7/FQDN>`


Enable Advanced Container Networking Services on an existing AKS cluster using the

command with the`az aks update`

`--enable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns`


## Disable Advanced Container Networking Services on an AKS cluster

Disable Advanced Container Networking Services on an existing AKS cluster using the

command with the`az aks update`

`--disable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --disable-acns`


## Disable Container Network Observability on an AKS cluster

Disable the Container Network Observability feature without affecting other Advanced Container Networking Services features using the

command with the`az aks update`

`--disable-acns-observability`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --disable-acns-observability`


Container Network Observability is the only feature available for non-Cilium clusters, so you can disable it only by disabling the entire Advanced Container Networking Services suite.

Disable the Container Network Observability feature on an existing AKS cluster using the

command with the`az aks update`

`--disable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --disable-acns`


## Disable Container Network Security on an AKS cluster

Disable the Container Network Security feature without affecting other Advanced Container Networking Services features using the

command with the`az aks update`

`--disable-acns-security`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --disable-acns-security`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-about -->

# Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Istio](https://istio.io/latest/) addresses the challenges developers and operators face with a distributed or microservices architecture. The Istio-based service mesh add-on provides an officially supported and tested integration for Azure Kubernetes Service (AKS).

## What is a Service Mesh?

Modern applications are typically architected as distributed collections of microservices, with each collection of microservices performing some discrete business function. A service mesh is a dedicated infrastructure layer that you can add to your applications. It allows you to transparently add capabilities like observability, traffic management, and security, without adding them to your own code. The term **service mesh** describes both the type of software you use to implement this pattern, and the security or network domain that is created when you use that software.

As the deployment of distributed services, such as in a Kubernetes-based system, grows in size and complexity, it can become harder to understand and manage. You may need to implement capabilities such as discovery, load balancing, failure recovery, metrics, and monitoring. A service mesh can also address more complex operational requirements like A/B testing, canary deployments, rate limiting, access control, encryption, and end-to-end authentication.

Service-to-service communication is what makes a distributed application possible. Routing this communication, both within and across application clusters, becomes increasingly complex as the number of services grow. Istio helps reduce this complexity while easing the strain on development teams.

## What is Istio?

Istio is an open-source service mesh that layers transparently onto existing distributed applications. Istio’s powerful features provide a uniform and more efficient way to secure, connect, and monitor services. Istio enables load balancing, service-to-service authentication, and monitoring – with few or no service code changes. Its powerful control plane brings vital features, including:

- Secure service-to-service communication in a cluster with TLS (Transport Layer Security) encryption, strong identity-based authentication, and authorization.
- Automatic load balancing for HTTP, gRPC, WebSocket, and TCP traffic.
- Fine-grained control of traffic behavior with rich routing rules, retries, failovers, and fault injection.
- A pluggable policy layer and configuration API supporting access controls, rate limits, and quotas.
- Automatic metrics, logs, and traces for all traffic within a cluster, including cluster ingress and egress.

## How is the add-on different from open-source Istio?

This service mesh add-on uses and builds on top of open-source Istio. The add-on flavor provides the following extra benefits:

- Istio versions are tested and verified to be compatible with supported versions of Azure Kubernetes Service.
- Microsoft handles scaling and configuration of Istio control plane
- Microsoft adjusts scaling of AKS components like
`coredns`

when Istio is enabled. - Microsoft provides managed lifecycle (upgrades) for Istio components when triggered by user.
- Verified external and internal ingress set-up.
- Verified to work with
[Azure Monitor managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)and[Azure Managed Grafana](/en-us/azure/managed-grafana/overview). - Official Azure support provided for the add-on.

## Limitations

Istio-based service mesh add-on for AKS has the following limitations:

- The add-on doesn't work on AKS clusters that are using
[Open Service Mesh addon for AKS](open-service-mesh-about). - The add-on doesn't work on AKS clusters with self-managed installations of Istio.
- The add-on doesn't support adding pods associated with virtual nodes to be added under the mesh.
- The add-on doesn't yet support the sidecar-less Ambient mode. Microsoft is currently contributing to Ambient workstream under Istio open source. Product integration for Ambient mode is on the roadmap and is being continuously evaluated as the Ambient workstream evolves.
- The add-on doesn't yet support multi-cluster deployments.
- The add-on doesn't yet support Windows Server containers. Windows Server containers aren't yet supported in open source Istio right now. Issue tracking this feature ask can be found
[here](https://github.com/istio/istio/issues/27893). - Customization of mesh through the following custom resources is currently blocked -
`ProxyConfig, WorkloadEntry, WorkloadGroup, IstioOperator, WasmPlugin`

. - While the add-on allows the use of
`EnvoyFilter`

's, issues arising from them (for example from the Lua script or from the compression library) are outside the support scope of the Istio add-on. See the[support policy document](istio-support-policy#allowed-supported-and-blocked-customizations)for more information about the support categories for Istio add-on features and configuration options. - Gateway API for Istio ingress gateway or managing mesh traffic (GAMMA) is currently not yet supported with Istio add-on. However, Gateway API for Istio ingress traffic management is currently under active development for the add-on. While the add-on supports
[annotation and](istio-deploy-ingress#ingress-gateway-service-customizations), port or protocol configuration is currently not supported.`externalTrafficPolicy`

customization for the Istio ingress gateways - The add-on supports customization of a subset of the fields in
[MeshConfig](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/). Other customizations may be allowed but unsupported or disallowed entirely, as detailed[here](istio-meshconfig#allowed-supported-and-blocked-meshconfig-values).

## Feedback and feature ask

Feedback and feature ask for the Istio add-on can be provided by creating [issues with label 'service-mesh' on AKS GitHub repository](https://github.com/Azure/AKS/issues?q=is%3Aopen+is%3Aissue+label%3Aservice-mesh).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/optimized-addon-scaling -->

# Enable cost optimized add-on scaling on your Azure Kubernetes Service (AKS) cluster (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of cost optimized add-on scaling in Azure Kubernetes Service (AKS). With cost-optimized add-on scaling, you can manage add-ons that require custom CPU and memory by overriding default configurations or enabling autoscaling. This feature ensures that resources aren't overly allocated to add-on pods, improving cost savings and cluster efficiency.

## Overview

Enabling cost optimized add-on scaling installs the [Vertical Pod Autoscaler (VPA)add-on](vertical-pod-autoscaler), allowing supported add-ons to autoscale based on usage.

This feature also allows you to customize the resource's default CPU/ memory requests and limits in Deployments and DaemonSets, the maximum and minimum allowed CPU/ memory, and the VPA update mode within VPA custom resources. For more information, see [customize the resource configuration for AKS add-ons](customize-resource-configuration).

### Supported AKS add-ons

The following AKS managed add-ons support the cost optimized add-on scaling feature:

| Add-on | Enablement behavior | VPA custom resource name | Command to check VPA custom resource |
|---|---|---|---|
|

`coredns`

`kubectl get vpa coredns --namespace kube-system`

[Workload identity](workload-identity-deploy-cluster)`azure-wi-webhook-controller-manager`

`kubectl get vpa azure-wi-webhook-controller-manager --namespace kube-system`

[Image Integrity](image-integrity)`ratify`

`kubectl get vpa ratify --namespace gatekeeper-system`

[Network Observability (Retina)](container-network-observability-how-to)`retina-agent`

and `retina-operator`

`kubectl get vpa retina-agent --namespace kube-system`

and `kubectl get vpa retina-operator --namespace kube-system`

### Supported VPA modes for cost optimized add-on scaling

VPA currently supports the following modes for cost optimized add-on scaling:

*Off*: The VPA provides resource recommendation data but doesn't apply it to the target pod.*Initial*(default mode): The VPA automatically applies CPU and memory recommendations to the target pod when it restarts, but it doesn't initiate the restart itself.*Auto*: The VPA automatically updates CPU and memory requests for pods based on recommendations.

Note

When enabling cost optimized add-on scaling, consider the following information:

- If you delete the Deployment, DaemonSet, or VPA custom resource, the changes revert back to the AKS add-on's initial configuration.
- The cost optimized add-on scaling feature enables the
[VPA add-on](vertical-pod-autoscaler)to autoscale the supported AKS add-ons. It doesn't work with self-hosted VPA. - AKS restarts the add-on pods when enabling cost optimized add-on scaling. CoreDNS is currently the only exception to avoid potential disruptions during the restart. For more information, see
[CoreDNS autoscaling behavior](coredns-autoscale).

Warning

Make sure you have enough compute resources on the system node pool for your addons when you enable cost optimized add-on scaling. AKS recommends turning on the [cluster autoscaler](cluster-autoscaler-overview) or [node autoprovision](node-autoprovision) to ensure right-sizing of your compute resources automatically.
Monitor for pending add-on pods when using the cost-optimized add-on scaling feature. VPA might recommend resource requests that exceed available node capacity, potentially leading to unschedulable pods. You can control this behavior by [customizing min/max values](customize-resource-configuration) for requests and limits of supported addons.

## Prerequisites

- An AKS cluster running Kubernetes version 1.25 or later.
- The Azure CLI version 2.60.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). [Install the](#install-the-aks-preview-azure-cli-extension)and`aks-preview`

Azure CLI extension[register the cost optimized add-on scaling preview feature](#register-the-cost-optimized-add-on-scaling-preview-feature).

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Install the `aks-preview`

Azure CLI extension

Install the

`aks-preview`

extension using the`az extension add`

command.`az extension add --name aks-preview`

Update to the latest version of the extension using the

`az extension update`

command.`az extension update --name aks-preview`


### Register the cost optimized add-on scaling preview feature

Register the cost optimized add-on scaling preview feature using the

`az feature register`

command.`az feature register --namespace "Microsoft.ContainerService" --name "AKS-AddonAutoscalingPreview"`

It takes a few minutes for the status to show as

*Registered*.Verify the registration status using the

`az feature show`

command.`az feature show --namespace "Microsoft.ContainerService" --name "AKS-AddonAutoscalingPreview"`

When the status shows as

*Registered*, refresh the registration of the Microsoft.ContainerService provider using the`az provider register`

command.`az provider register --namespace Microsoft.ContainerService`


## Enable cost optimized add-on scaling on an AKS cluster

When enabling the add-on, the AKS cluster automatically installs the [VPA add-on](vertical-pod-autoscaler). The [AKS add-ons that support the cost optimized add-on scaling feature](#supported-aks-add-ons) have different enablement behavior.

Note

If you're using Bicep, ARM templates, or Terraform, set `VerticalPodAutoscaler`

to `"True"`

and `AddonAutoscaling`

to `"enabled"`

.

### Enable cost optimized add-on scaling on a new cluster

Enable cost optimized add-on scaling on a new AKS cluster using the

command with the`az aks create`

`--enable-optimized-addon-scaling`

flag.`az aks create --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --enable-optimized-addon-scaling`


### Enable cost optimized add-on scaling on an existing cluster

Enable cost optimized add-on scaling on an existing AKS cluster using the

command with the`az aks update`

`--enable-optimized-addon-scaling`

flag.`az aks update --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --enable-optimized-addon-scaling`


## Disable cost optimized add-on scaling on an AKS cluster

Disable cost optimized add-on scaling on an AKS cluster using the

command with the`az aks update`

`--disable-optimized-addon-scaling`

flag.`az aks update --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --disable-optimized-addon-scaling`


Note

Disabling the cost optimized add-on scaling feature doesn't disable the VPA add-on by default. To disable VPA, see [Disable VPA on an AKS cluster](use-vertical-pod-autoscaler#disable-the-vertical-pod-autoscaler-on-an-existing-cluster).

## Customize default resource configuration

With the cost optimized add-on scaling feature enabled on your cluster, you can customize the default CPU/memory settings for the add-on resources as well as the default VPA configuration for supported AKS add-ons. For more information, see [customize the resource configuration for AKS add-ons](customize-resource-configuration).

## Applying the VPA recommended values manually

Note

With *Initial* mode, the VPA applies the recommended CPU and memory requests only when a pod is created or updated. If you want the recommendations to take effect immediately, please update the pods manually. Before manually applying the recommended values, [make sure the VPA update mode is set to Initial or Auto in the VPA custom resource](customize-resource-configuration#customize-resource-update-mode).

Check the pod status and CPU/memory utilization to verify that the pod is running as expected.

The following example uses the

`kubectl get pod`

command to check a CoreDNS pod status:`kubectl get pod <coredns-pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a CoreDNS pod:

`apiVersion: v1 kind: Pod metadata: name: <coredns-pod-name> namespace: kube-system spec: ... containers: - name: coredns resources: limits: cpu: "3" memory: "500Mi" requests: cpu: "100m" memory: "70Mi"`

Get the VPA recommended value using the

`kubectl get vpa`

command.`kubectl get vpa coredns --namespace kube-system`

The following output shows an example of the VPA recommended value for a CoreDNS pod:

`NAME MODE CPU MEM PROVIDED AGE coredns Initial 11m 23574998 True 44m`

If you want to use the values recommended by VPA, manually delete the pod using the

`kubectl delete pod`

command to restart the pod with the VPA recommended values.`kubectl delete pod <coredns-pod-name> --namespace kube-system`

After the pod restarts, verify the pod status and CPU/memory updates using the

`kubectl get pod`

command.`kubectl get pod <coredns-pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a CoreDNS pod after applying the VPA recommended values:

`apiVersion: v1 kind: Pod metadata: name: <coredns-pod-name> namespace: kube-system spec: ... containers: - name: coredns resources: limits: cpu: "330m" memory: "168392842" requests: cpu: "11m" memory: "23574998"`


## Troubleshooting

With the cost optimized add-on scaling feature enabled on your cluster, you can customize the default CPU and memory settings for add-on resources, as well as modify the default VPA configuration for supported AKS managed add-ons

If your autoscaling enabled add-on pods are in a pending state, or you don't see any VPA recommendations for autoscaling enabled add-ons, follow these steps to troubleshoot the issue.

### Check AKS-managed VPA add-on status

Check if all VPA system components are running using the

`kubectl get pods`

command.`kubectl get pods --namespace kube-system | grep vpa`

The output should show three pods (vpa-admission-controller, vpa-recommender, and vpa-updater) running in the

`kube-system`

namespace, similar to the following example:`vpa-admission-controller 2/2 2 2 4m11s vpa-recommender 1/1 1 1 4m11s vpa-updater 1/1 1 1 4m11s`

For each of the three VPA pods, check the logs for any errors using the

`kubectl logs`

command. Make sure to replace`<pod-name>`

with the names of the VPA pods.`kubectl logs <pod-name> --namespace kube-system | grep -e '^E[0-9]\{4\}'`

Confirm the custom resource definition (CRD) was creating using the

`kubectl get`

command.`kubectl get customresourcedefinition | grep verticalpodautoscalers`


### Check pod status and CPU/memory utilization

Check the pod's status using the

`kubectl get pod`

command.`kubectl get pod <pod-name> --namespace=kube-system`

If the pod has a status of

`Pending`

, check the pod's status property to determine the reason the pod isn't running.`kubectl describe pod <pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a pod with a status of

`Pending`

:`apiVersion: v1 kind: Pod ... status: conditions: - lastProbeTime: null lastTransitionTime: "2023-05-03T17:05:26Z" message: '0/1 nodes are available: 1 Insufficient cpu, 1 Insufficient memory. preemption: 0/1 nodes are available: 1 Insufficient cpu, 1 Insufficient memory..' reason: Unschedulable status: "False" type: PodScheduled phase: Pending qosClass: Guaranteed`

If the output shows that the pod is

`Pending`

due to insufficient CPU or memory, consider the following actions:- Add more nodes so that pods can be scheduled in nodes with lower resource usage.
- Disable VPA for the target add-on pod by changing the update mode to
*Off*, and then[manually update the requests/limits](customize-resource-configuration)to the available resource values on the node. Be cautious when setting resource limits to extremely low values, as this may result in the pod encountering OOM kills or CPU throttling if it attempts to use more resources than are available on the node.


## Next steps

- Configure
[Cluster Autoscaler](cluster-autoscaler-overview)or[Node Autoprovisioning](node-autoprovision)in your cluster to automatically scale the cluster.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/reduce-latency-ppg -->

# Use proximity placement groups to reduce latency for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

When using proximity placement groups on AKS, colocation only applies to the agent nodes. Node to node and the corresponding hosted pod to pod latency is improved. The colocation doesn't affect the placement of a cluster's control plane.

When deploying your application in Azure, you can create network latency by spreading virtual machine (VM) instances across regions or availability zones, which may impact the overall performance of your application. A proximity placement group is a logical grouping used to make sure Azure compute resources are physically located close to one another. Some applications, such as gaming, engineering simulations, and high-frequency trading (HFT) require low latency and tasks that can complete quickly. For similar high-performance computing (HPC) scenarios, consider using [proximity placement groups (PPG)](/en-us/azure/virtual-machines/co-location#proximity-placement-groups) for your cluster's node pools.

## Before you begin

This article requires Azure CLI version 2.14 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Limitations

- A proximity placement group can map to only
*one*availability zone. - A node pool must use Virtual Machine Scale Sets to associate a proximity placement group.
- A node pool can associate a proximity placement group at node pool create time only.

## Node pools and proximity placement groups

The first resource you deploy with a proximity placement group attaches to a specific data center. Any extra resources you deploy with the same proximity placement group are colocated in the same data center. Once all resources using the proximity placement group are stopped (deallocated) or deleted, it's no longer attached.

- You can associate multiple node pools with a single proximity placement group.
- You can only associate a node pool with a single proximity placement group.

### Configure proximity placement groups with availability zones

Note

While proximity placement groups require a node pool to use only *one* availability zone, the [baseline Azure VM SLA of 99.9%](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_9/) is still in effect for VMs in a single zone.

Proximity placement groups are a node pool concept and associated with each individual node pool. Using a PPG resource has no impact on AKS control plane availability, which can impact how you should design your cluster with zones. To ensure a cluster is spread across multiple zones, we recommend using the following design:

- Provision a cluster with the first system pool using
*three*zones and no proximity placement group associated to ensure the system pods land in a dedicated node pool, which spreads across multiple zones. - Add extra user node pools with a unique zone and proximity placement group associated to each pool. An example is
*nodepool1*in zone one and PPG1,*nodepool2*in zone two and PPG2, and*nodepool3*in zone 3 with PPG3. This configuration ensures that, at a cluster level, nodes are spread across multiple zones and each individual node pool is colocated in the designated zone with a dedicated PPG resource.

## Create a new AKS cluster with a proximity placement group

Accelerated networking greatly improves networking performance of virtual machines. Ideally, use proximity placement groups with accelerated networking. By default, AKS uses accelerated networking on [supported virtual machine instances](/en-us/azure/virtual-network/accelerated-networking-overview?toc=/azure/virtual-machines/linux/toc.json#limitations-and-constraints), which include most Azure virtual machine with two or more vCPUs.

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location centralus`

Create a proximity placement group using the

command. Make sure to note the ID value in the output.`az ppg create`

`az ppg create --name myPPG --resource-group myResourceGroup --location centralus --type standard`

The command produces an output similar to the following example output, which includes the

*ID*value you need for upcoming CLI commands.`{ "availabilitySets": null, "colocationStatus": null, "id": "/subscriptions/yourSubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.Compute/proximityPlacementGroups/myPPG", "location": "centralus", "name": "myPPG", "proximityPlacementGroupType": "Standard", "resourceGroup": "myResourceGroup", "tags": {}, "type": "Microsoft.Compute/proximityPlacementGroups", "virtualMachineScaleSets": null, "virtualMachines": null }`

Create an AKS cluster using the

command and replace the`az aks create`

*myPPGResourceID*value with your proximity placement group resource ID from the previous step.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --ppg myPPGResourceID --generate-ssh-keys`


## Add a proximity placement group to an existing cluster

You can add a proximity placement group to an existing cluster by creating a new node pool. You can then optionally migrate existing workloads to the new node pool and delete the original node pool.

Use the same proximity placement group that you created earlier to ensure agent nodes in both node pools in your AKS cluster are physically located in the same data center.

Create a new node pool using the

command and replace the`az aks nodepool add`

*myPPGResourceID*value with your proximity placement group resource ID.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name mynodepool \ --node-count 1 \ --ppg myPPGResourceID`


## Clean up

Delete the Azure resource group along with its resources using the

command.`az group delete`

`az group delete --name myResourceGroup --yes --no-wait`


## Next steps

Learn more about [proximity placement groups](/en-us/azure/virtual-machines/co-location#proximity-placement-groups).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/customize-resource-configuration -->

# Customize the resource configuration for managed add-ons

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of how to customize the resource configuration for Azure Kubernetes Service (AKS) managed add-ons with [cost optimized add-on scaling (Preview)](optimized-addon-scaling).

## Overview

Enabling the cost optimized add-on scaling feature in your AKS cluster installs the Vertical Pod Autoscaler (VPA) add-on and VPA custom resources for AKS managed add-ons that support this capability. This feature also allows you to manually customize the resource CPU and memory requests and limits in Deployments and DaemonSets. You can also customize the maximum and minimum allowed CPU and memory and the VPA update mode within VPA custom resources.

## Prerequisites

- Review the
[supported AKS managed add-ons](optimized-addon-scaling#supported-aks-add-ons)and[limitations](optimized-addon-scaling)for this feature. - You need an AKS cluster enabled with the cost optimized add-on scaling feature. If you don't have one, see
[Enable cost optimized add-on scaling on your AKS cluster (Preview)](optimized-addon-scaling).

## Customize resource annotations

| Annotation | Description | Values |
|---|---|---|
`kubernetes.azure.com/override-requests-limits` |
Supports the capability to customize the container resource CPU/memory requests/limits in a Deployment or DaemonSet if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. | "enabled" or "disabled" |
`kubernetes.azure.com/override-min-max` |
Supports the capability to customize the container policy maximum/minimum allowed CPU/memory value in VPA custom resource if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. | "enabled" or "disabled" |
`kubernetes.azure.com/override-update-mode` |
Supports the capability to customize the update policy `updateMode` value in a VPA custom resource if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. |
"enabled" or "disabled" |

## Customize resource CPU/memory requests/limits

After setting the `kubernetes.azure.com/override-requests-limits`

annotation to "enabled" in a Deployment or DaemonSet, you can customize the resource CPU/memory requests and limits. The following example shows how to customize the resource CPU/memory requests and limits in a Deployment:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-requests-limits: "enabled"
spec:
...
containers:
- name: coredns
resources:
limits:
# update cpu limits value won't be reconciled back
cpu: "3"
# update memory limits value won't be reconciled back
memory: "500Mi"
requests:
# update cpu requests value won't be reconciled back
cpu: "100m"
# update memory requests value won't be reconciled back
memory: "70Mi"
```


## Customize resource maximum/minimum allowed CPU/memory

After setting the `kubernetes.azure.com/override-min-max`

annotation to "enabled" in a VPA custom resource, you can customize the maximum and minimum allowed CPU and memory values in a VPA custom resource. The following example shows how to customize the maximum and minimum allowed CPU and memory values in a VPA custom resource:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-min-max: "enabled"
spec:
resourcePolicy:
containerPolicies:
- containerName: coredns
maxAllowed:
# update maxAllowed cpu value won't be reconciled back
cpu: 3
# update maxAllowed memory value won't be reconciled back
memory: 500Mi
minAllowed:
# update minAllowed cpu value won't be reconciled back
cpu: 10m
# update minAllowed memory value won't be reconciled back
memory: 10Mi
...
```


## Customize resource update mode

After setting the `kubernetes.azure.com/override-update-mode`

annotation to "enabled" in a VPA custom resource, you can customize the update policy `updateMode`

value in a VPA custom resource to "Off" or "Initial" (default). The following example shows how to customize the update policy `updateMode`

value to "Initial" in a VPA custom resource:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-update-mode: "enabled"
spec:
...
updatePolicy:
# update updateMode won't be reconciled back
updateMode: "Initial"
```


## Disable VPA on a specific AKS managed add-on

To disable VPA on a specific AKS managed add-on, you need to update the VPA custom resource YAML file to set the `kubernetes.azure.com/override-update-mode`

annotation to `"enabled"`

and the `updateMode`

to `"Off"`

. With *Off* mode, the VPA only provides CPU and memory recommendations and doesn't apply the changes to the pod.

The following example shows how to disable VPA on the CoreDNS add-on:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# Set value to "enabled"
kubernetes.azure.com/override-update-mode: "enabled"
spec:
...
updatePolicy:
# Set value to "Off"
updateMode: "Off"
```


## Troubleshooting

- Make sure the AKS managed add-on supports the cost optimized add-on scaling feature. For more information, see
[Supported AKS managed add-ons](optimized-addon-scaling#supported-aks-add-ons). - Verify that the
`kubernetes.azure.com/override-requests-limits`

annotation in the Deployment or DaemonSet is set to "enabled". - Verify that the
`kubernetes.azure.com/override-min-max`

annotation in the VPA custom resource is set to "enabled". - Verify that the
`kubernetes.azure.com/override-update-mode`

annotation in the VPA custom resource is set to "enabled".

## Next steps

To further configure cluster resource utilization and free up CPU/memory for AKS managed add-on pods, see [Vertical pod autoscaling in AKS](vertical-pod-autoscaler).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kubelogin-authentication -->

# Use kubelogin to authenticate users in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The kubelogin plugin in Azure is a client-go credential [plugin](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#client-go-credential-plugins) that implements Microsoft Entra authentication. The kubelogin plugin offers features that aren't available in the kubectl command-line tool. For more information, see the [kubelogin introduction](https://azure.github.io/kubelogin/index.html) and the [kubectl introduction](https://kubernetes.io/docs/reference/kubectl/introduction/).

This article provides an overview and examples of how to use kubelogin for all supported Microsoft Entra authentication methods in AKS.

## Kubelogin authentication in AKS limitations

- Groups that are created in Microsoft Entra are included only by their
**ObjectID**value, and not by their display name. The`sAMAccountName`

command is available only for groups that are synchronized from on-premises Windows Server Active Directory.

- The service principal authentication method works only with managed Microsoft Entra, and not with the earlier version Azure Active Directory.
- The service principal can be a member of a maximum of 200
[Microsoft Entra groups](/en-us/entra/identity/hybrid/connect/how-to-connect-fed-group-claims). If you have more than 200 groups, consider using[application roles](/en-us/entra/external-id/customers/how-to-use-app-roles-customers).

- The device code authentication method doesn't work when a Microsoft Entra Conditional Access policy is set on a Microsoft Entra tenant. In that scenario, use web browser interactive authentication instead.

- The Azure CLI authentication method works only with AKS managed Microsoft Entra.

## How authentication works

Note

Keep in mind the following information about kubelogin authentication for AKS clusters integrated with Microsoft Entra:

**Clusters running Kubernetes version 1.24 or later**automatically use the kubelogin format.**Clusters running Kubernetes 1.24 or earlier**require manual conversion. You can use the device code authentication method to convert the kubeconfig file to use the exec plugin format.

For most interactions with kubelogin, you use the `convert-kubeconfig`

subcommand. The subcommand uses the kubeconfig file that's specified in `--kubeconfig`

or in the `KUBECONFIG`

environment variable to convert the final kubeconfig file to exec format based on the specified authentication method.

The authentication methods that kubelogin implements are Microsoft Entra OAuth 2.0 token grant flows. In each authentication method, the token isn't cached on the file system.

## Device code authentication

Device code is the default authentication method for the `convert-kubeconfig`

subcommand. This authentication method prompts the device code for the user to sign in from a browser session.

Note

Before the kubelogin and exec plugins were introduced, the Azure authentication method in kubectl supported only the device code flow. It used an earlier version of a library that produces a token that has the `audience`

claim with an `spn:`

prefix. It isn't compatible with [AKS managed Microsoft Entra](managed-azure-ad), which uses an [on-behalf-of (OBO)](/en-us/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) flow. When you run the `convert-kubeconfig`

subcommand, kubelogin removes the `spn:`

prefix from the audience claim.

### Parameters for device code authentication

The following table outlines parameters that you can use with device code authentication:

| Parameter | Description |
|---|---|
`-l devicecode` (optional) |
Specifies the kubelogin authentication method. This parameter is optional because device code is the default method. |
`--legacy` |
Uses legacy behavior for earlier versions of Azure Active Directory clusters. If you're using the kubeconfig file in an earlier version Azure Active Directory cluster, kubelogin automatically adds the `--legacy` flag. |
`--token-cache-dir` |
Overrides the default path of the token cache directory, which is ${HOME}/.kube/cache/kubelogin. |

## Azure CLI authentication

The Azure CLI (command: `-l azurecli`

) authentication method uses the signed-in context that the Azure CLI establishes to get the access token. The token is issued in the same Microsoft Entra tenant as `az login`

. kubelogin doesn't write tokens to the token cache file because the Azure CLI already manages them.

### Parameters for Azure CLI authentication

The following table outlines parameters that you can use with Azure CLI authentication:

| Parameter | Description |
|---|---|
`-l azurecli` |
Specifies the kubelogin authentication method. |
`--azure-config-dir` |
Specifies the Azure CLI configuration directory. The default directory is ${HOME}/.azure. |

## Sign in to Azure

Sign in to Azure using the [ az login](/en-us/cli/azure/authenticate-azure-cli-interactively#interactive-login) command.

```
az login
```


## Web browser interactive authentication

The web browser interactive (command: `-l interactive`

) method of authentication automatically opens a web browser to sign in the user. After the user is authenticated, the browser redirects to the local web server using the verified credentials. This authentication method complies with Conditional Access policy.

You can use either a bearer token or a Proof-of-Possession (PoP) token with this authentication method.

### Parameters for bearer token authentication

The following table outlines parameters that you can use with bearer token authentication:

| Parameter | Description |
|---|---|
`-l interactive` |
Specifies the kubelogin authentication method. |
`--token-cache-dir` |
Overrides the default path of the token cache directory, which is ${HOME}/.kube/cache/kubelogin. |

### Parameters for PoP token authentication

The following table outlines parameters that you can use with PoP token authentication:

| Parameter | Description |
|---|---|
`-l interactive` |
Specifies the kubelogin authentication method. |
`--pop-enabled` |
Enables PoP token authentication. |
`--pop-claims` |
Specifies the PoP token claims in a key-value pair format. For example, `u=/ARM/ID/OF/CLUSTER` . |

## Service principal authentication

The service principal (command: `-l spn`

) authentication method uses a service principal to sign in the user. You can provide the credential by setting an environment variable or by using the credential in a command-line argument. The supported credentials that you can use are a password or a Personal Information Exchange (PFX) client certificate.

### Parameters for service principal authentication

The following table outlines parameters that you can use with service principal authentication:

| Parameter | Description |
|---|---|
`-l spn` |
Specifies the kubelogin authentication method. |
`--client-id` |
The application ID (client-id) of the service principal. |
`--client-secret` |
The client secret of the service principal. |

## Managed identity authentication

Use the [managed identity](/en-us/entra/identity/managed-identities-azure-resources/overview) (command: `-l msi`

) authentication method for applications that connect to resources that support Microsoft Entra authentication. Examples include accessing Azure resources like an Azure virtual machine (VM), a virtual machine scale set, or Azure Cloud Shell.

You can use the default managed identity that's assigned to the resource or a specific user-assigned managed identity.

### Parameters for managed identity authentication

The following table outlines parameters that you can use with managed identity authentication:

| Parameter | Description |
|---|---|
`-l msi` |
Specifies the kubelogin authentication method. |
`--client-id` |
The application ID (client-id) of the user-assigned managed identity. If you don't specify this parameter, the default managed identity is used. |

## Workload identity authentication

The workload identity (command: `-l workloadidentity`

) authentication method uses identity credentials that are federated with Microsoft Entra to authenticate access to AKS clusters. The method uses Microsoft Entra integrated authentication. It works by setting the following environment variables:

| Variable | Description |
|---|---|
`AZURE_CLIENT_ID` |
The Microsoft Entra application ID that is federated with the workload identity. |
`AZURE_TENANT_ID` |
The Microsoft Entra tenant ID. |
`AZURE_FEDERATED_TOKEN_FILE` |
The file that contains a signed assertion of the workload identity, like a Kubernetes projected service account (JWT) token. |
`AZURE_AUTHORITY_HOST` |
The base URL of a Microsoft Entra authority. For example, `https://login.microsoftonline.com/` . |

You can use a [workload identity](/en-us/entra/workload-id/workload-identities-overview) to access Kubernetes clusters from CI/CD systems like GitHub or ArgoCD without storing service principal credentials in the external systems. To configure OpenID Connect (OIDC) federation from GitHub, see the [OIDC federation example](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-azure).

### Parameters for workload identity authentication

The following table outlines parameters that you can use with workload identity authentication:

| Parameter | Description |
|---|---|
`-l workloadidentity` |
Specifies the kubelogin authentication method. |

## Export the kubeconfig file path

Before you run the `convert-kubeconfig`

subcommand, export the kubeconfig file path to the `KUBECONFIG`

environment variable. For example:

```
export KUBECONFIG=/path/to/kubeconfig
```


## Convert the kubeconfig file

Run the `convert-kubeconfig`

subcommand to convert the kubeconfig file to use the exec plugin for your chosen authentication method.

```
kubelogin convert-kubeconfig
```


```
kubelogin convert-kubeconfig -l azurecli
```


```
# Bearer token authentication
kubelogin convert-kubeconfig -l interactive
# Proof-of-Possession (PoP) token authentication
kubelogin convert-kubeconfig -l interactive --pop-enabled --pop-claims "u=/ARM/ID/OF/CLUSTER"
```


-
[Use environment variables](#tabpanel_1_environment-variables) -
[Use command-line arguments](#tabpanel_1_command-line-arguments) -
[Use a client certificate](#tabpanel_1_client-certificate) -
[Use a PoP token with environment variables](#tabpanel_1_pop-token-environment-variables)

Run the

`convert-kubeconfig`

subcommand to convert the kubeconfig file to use the exec plugin.`kubelogin convert-kubeconfig -l spn`

Set the environment variables for the client ID and client secret or client certificate. For example:

`export AZURE_CLIENT_ID=<service-principal-client-id> export AZURE_CLIENT_SECRET=<service-principal-client-secret>`


```
# Default managed identity authentication
kubelogin convert-kubeconfig -l msi
# Specific managed identity authentication
kubelogin convert-kubeconfig -l msi --client-id <managed-identity-client-id>
```


```
kubelogin convert-kubeconfig -l workloadidentity
```


## Remove cached tokens

Remove cached tokens using the `kubelogin remove-tokens`

command.

```
kubelogin remove-tokens
```


## Get node information

Get node information using the `kubectl get`

command.

```
kubectl get nodes
```


## How to use kubelogin with AKS

AKS uses a pair of first-party Microsoft Entra applications. These application IDs are the same in all environments.

The AKS Microsoft Entra server application ID (server-id) that the server side uses is `6dae42f8-4368-4678-94ff-3960e28e3630`

. The access token that accesses AKS clusters must be issued for this application. In most kubelogin authentication methods, you must use `--server-id`

with `kubelogin get-token`

.

The AKS Microsoft Entra client application ID (client-id) that kubelogin uses to perform public client authentication on behalf of the user is `80faf920-1908-4b52-b5ef-a8e7bedfc67a`

. The client application ID is used in device code and web browser interactive authentication methods.

## Related content

- Learn how to integrate AKS with Microsoft Entra in the
[AKS managed Microsoft Entra integration](managed-azure-ad)how-to article. - To get started with managed identities in AKS, see
[Use a managed identity in AKS](use-managed-identity). - To get started with workload identities in AKS, see
[Use a workload identity in AKS](workload-identity-overview).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-cni-powered-by-cilium -->

# Configure Azure CNI Powered by Cilium in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure CNI Powered by Cilium combines the robust control plane of Azure Container Networking Interface (CNI) with the data plane of [Cilium](https://cilium.io/) to provide high-performance networking and security.

Azure CNI Powered by Cilium provides the following benefits by making use of eBPF programs loaded into the Linux kernel and a more efficient API object structure:

- Functionality equivalent to existing Azure CNI and Azure CNI Overlay plugins
- Improved service routing
- More efficient network policy enforcement
- Better observability of cluster traffic
- Support for larger clusters (more nodes, pods, and services)

## IP Address Management (IPAM) with Azure CNI Powered by Cilium

You can deploy Azure CNI Powered by Cilium with two different methods for assigning pod IPs:

- Assign IP addresses from an overlay network (similar to Azure CNI Overlay mode)
- Assign IP addresses from a virtual network (similar to existing Azure CNI with Dynamic Pod IP Assignment)

If you aren't sure which option to select, read [Choose a network model](concepts-network-azure-cni-overlay#choose-a-network-model)

## Versions

| Kubernetes Version | Minimum Cilium Version |
|---|---|
| 1.29 (LTS) | 1.14.19 |
| 1.30 | 1.14.19 |
| 1.31 | 1.16.6 |
| 1.32 | 1.17.0 |
| 1.33 | 1.17.0 |

For more information on AKS versioning and release timelines, see [Supported Kubernetes Versions](supported-kubernetes-versions).

## Network Policy Enforcement

Cilium enforces [network policies to allow or deny traffic between pods](operator-best-practices-network#control-traffic-flow-with-network-policies). With Cilium, you don't need to install a separate network policy engine such as Azure Network Policy Manager or Calico.

## Local Redirect Policy (LRP)

LRP starts to be supported from Kubernetes v1.29 and up, Cilium v1.14 and up. For LRP to work with Advanced Container Networking Services (ACNS) - FQDN Filtering, the Cilium Network Policy egress labels need to match with node-local DNS cache pod labels.

## Limitations

Azure CNI powered by Cilium currently has the following limitations:

- Available only for Linux and not for Windows.
- Network policies can't use
`ipBlock`

to allow access to node or pod IPs. For details and recommended workarounds, see[frequently asked questions](#frequently-asked-questions). - For Cilium versions 1.16 or earlier, multiple Kubernetes services can't use the same host port with different protocols (for example, TCP or UDP) (
[Cilium issue #14287](https://github.com/cilium/cilium/issues/14287)). - Network policies aren't applied to pods using host networking (
`spec.hostNetwork: true`

) because these pods use the host identity instead of having individual identities. - Cilium Endpoint Slices are supported in Kubernetes version 1.32 and above. Cilium Endpoint Slices don't support configuration of how Cilium Endpoints are grouped. Priority namespace through
`cilium.io/ces-namespace`

isn't supported. - L7 policy isn't supported by
`CiliumClusterwideNetworkPolicy`

(CCNP). - Cilium uses Cilium identities as unique identity for provisioning endpoints, so high-churning workloads such as Spark jobs generate high count of Cilium identities. To avoid workloads hitting Cilium identity limits (65535), excluding Spark job's labels like
`!spark-app-name`

and`!spark-app-selector`

in the Cilium configmap can significantly reduce Cilium identity generation. For more details on Cilium identity exclusion rules, check[the official Cilium label documentation](https://docs.cilium.io/en/stable/operations/performance/scalability/identity-relevant-labels/#excluding-labels). - AKS Local DNS isn't compatible with Advanced Container Networking Services (ACNS) - FQDN Filtering.

## Considerations

To gain capabilities such as observability into your network traffic and security features like Fully Qualified Domain Name (FQDN) based filtering and Layer 7 based network policies on your cluster, consider enabling [Advanced Container Networking services](advanced-container-networking-services-overview) on your clusters.

## Prerequisites

- Azure CLI version 2.48.1 or later. Run
`az --version`

to see the currently installed version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you're using ARM templates or the REST API, the AKS API version must be
`2022-09-02-preview`

or later.

Previous AKS API versions (`2022-09-02preview`

to `2023-01-02preview`

) used the field [ networkProfile.ebpfDataplane=cilium](https://github.com/Azure/azure-rest-api-specs/blob/06dbe269f7d9c709cc225c92358b38c3c2b74d60/specification/containerservice/resource-manager/Microsoft.ContainerService/aks/preview/2022-09-02-preview/managedClusters.json#L6939-L6955). AKS API versions since

`2023-02-02preview`

use the field [to enable Azure CNI Powered by Cilium.](https://github.com/Azure/azure-rest-api-specs/blob/06dbe269f7d9c709cc225c92358b38c3c2b74d60/specification/containerservice/resource-manager/Microsoft.ContainerService/aks/preview/2023-02-02-preview/managedClusters.json#L7152-L7173)

`networkProfile.networkDataplane=cilium`

## Create a new AKS Cluster with Azure CNI Powered by Cilium

The following sections use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command to create a cluster and assign IP addresses.

### Option 1: Assign IP addresses from an overlay network

Use the following commands to create a cluster with an overlay network and Cilium. Replace the values for `<clusterName>`

, `<resourceGroupName>`

, and `<location>`

:

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--network-plugin azure \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16 \
--network-dataplane cilium \
--generate-ssh-keys
```


The `--network-dataplane cilium`

flag replaces the deprecated `--enable-ebpf-dataplane`

flag used in earlier versions of the aks-preview CLI extension.

### Option 2: Assign IP addresses from a virtual network

Run the following commands to create a resource group and virtual network with a subnet for nodes and a subnet for pods.

```
# Create the resource group
az group create --name <resourceGroupName> --location <location>
```


```
# Create a virtual network with a subnet for nodes and a subnet for pods
az network vnet create --resource-group <resourceGroupName> --location <location> --name <vnetName> --address-prefixes <address prefix, example: 10.0.0.0/8> -o none
az network vnet subnet create --resource-group <resourceGroupName> --vnet-name <vnetName> --name nodesubnet --address-prefixes <address prefix, example: 10.240.0.0/16> -o none
az network vnet subnet create --resource-group <resourceGroupName> --vnet-name <vnetName> --name podsubnet --address-prefixes <address prefix, example: 10.241.0.0/16> -o none
```


Create the cluster using `--network-dataplane cilium`

:

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--max-pods 250 \
--network-plugin azure \
--vnet-subnet-id /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.Network/virtualNetworks/<vnetName>/subnets/nodesubnet \
--pod-subnet-id /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.Network/virtualNetworks/<vnetName>/subnets/podsubnet \
--network-dataplane cilium \
--generate-ssh-keys
```


### Option 3: Assign IP addresses from the Node Subnet

Azure CLI version 2.69.0 or later is required. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Create a cluster using [node subnet](concepts-network-legacy-cni#azure-cni-node-subnet) with a Cilium data plane:

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--network-plugin azure \
--network-dataplane cilium \
--generate-ssh-keys
```


## Frequently asked questions

**Can I customize Cilium configuration?**No, AKS manages the Cilium configuration and it can't be modified. We recommend that customers who require more control use

[AKS BYO CNI](use-byo-cni)and install Cilium manually.**Can I use**`CiliumNetworkPolicy`

custom resources instead of Kubernetes`NetworkPolicy`

resources?L3 and L4

`CiliumNetworkPolicy`

are supported and can be used alongside Kubernetes`NetworkPolicy`

resources.Customers might use FQDN filtering and Layer 7 policies as part of the

[Advanced Container Networking Services](advanced-container-networking-services-overview)feature bundle.**Can I use**`CiliumClusterwideNetworkPolicy`

?Yes,

`CiliumClusterwideNetworkPolicy`

is supported. The following sample policy YAML shows configuring an L4 rule:`apiVersion: "cilium.io/v2" kind: CiliumClusterwideNetworkPolicy metadata: name: "l4-rule-ingress-backend-frontend" spec: endpointSelector: matchLabels: role: backend ingress: - fromEndpoints: - matchLabels: role: frontend toPorts: - ports: - port: "80" protocol: TCP`

**Which Cilium features are supported in Azure managed CNI? Which of those require Advanced Container Networking Services?**Supported Feature w/o ACNS w/ ACNS Cilium Endpoint Slices ✔️ ✔️ K8s Network Policies ✔️ ✔️ Cilium L3/L4 Network Policies ✔️ ✔️ Cilium Clusterwide Network Policy ✔️ ✔️ FQDN Filtering ❌ ✔️ L7 Network Policies (HTTP/gRPC/Kafka) ❌ ✔️ Container Network Observability (Metrics and Flow logs) ❌ ✔️ eBPF Host Routing ❌ ✔️ **Why is traffic being blocked when the**`NetworkPolicy`

has an`ipBlock`

that allows the IP address?A limitation of Azure CNI Powered by Cilium is that a

`NetworkPolicy`

`ipBlock`

can't select pod or node IPs.For example, this

`NetworkPolicy`

has an`ipBlock`

that allows all egress to`0.0.0.0/0`

:`apiVersion: networking.k8s.io/v1 kind: NetworkPolicy metadata: name: example-ipblock spec: podSelector: {} policyTypes: - Egress egress: - to: - ipBlock: cidr: 0.0.0.0/0 # This will still block pod and node IPs.`

However, when this

`NetworkPolicy`

is applied, Cilium blocks egress to pod and node IPs even though the IPs are within the`ipBlock`

CIDR.As a workaround, you can add

`namespaceSelector`

and`podSelector`

to select pods. This example selects all pods in all namespaces:`apiVersion: networking.k8s.io/v1 kind: NetworkPolicy metadata: name: example-ipblock spec: podSelector: {} policyTypes: - Egress egress: - to: - ipBlock: cidr: 0.0.0.0/0 - namespaceSelector: {} - podSelector: {}`

It isn't currently possible to specify a

`NetworkPolicy`

with an`ipBlock`

to allow traffic to node IPs.**Does AKS configure CPU or memory limits on the Cilium**`daemonset`

?No, AKS doesn't configure CPU or memory limits on the Cilium

`daemonset`

because Cilium is a critical system component for pod networking and network policy enforcement.**Does Azure CNI powered by Cilium use kube-proxy?**No, AKS clusters created with network data plane as Cilium don't use

`kube-proxy`

. If the AKS clusters are on[Azure CNI Overlay](azure-cni-overlay)or[Azure CNI with dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)and are upgraded to AKS clusters running Azure CNI powered by Cilium, new nodes workloads are created without`kube-proxy`

. Older workloads are also migrated to run without`kube-proxy`

as a part of this upgrade process.

## Dual-stack networking with Azure CNI Powered by Cilium

You can deploy your dual-stack AKS clusters with Azure CNI Powered by Cilium. This feature also allows you to control your IPv6 traffic with the Cilium Network Policy engine.

You must have Kubernetes version 1.29 or greater.

### Set up Overlay clusters with Azure CNI Powered by Cilium

Create a cluster with Azure CNI Overlay using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command. Make sure to use the argument

`--network-dataplane cilium`

to specify the Cilium data plane.```
clusterName="myOverlayCluster"
resourceGroup="myResourceGroup"
location="westcentralus"
az aks create \
--name $clusterName \
--resource-group $resourceGroup \
--location $location \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--ip-families ipv4,ipv6 \
--generate-ssh-keys
```


## Next steps

Learn more about networking in AKS in the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-application -->

# Tutorial - Deploy an application to Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes provides a distributed platform for containerized applications. You build and deploy your own applications and services into a Kubernetes cluster and let the cluster manage the availability and connectivity.

In this tutorial, you deploy a sample application into a Kubernetes cluster. You learn how to:

- Update a Kubernetes manifest file.
- Run an application in Kubernetes.
- Test the application.

Tip

With AKS, you can use the following approaches for configuration management:

**GitOps**: Enables declarations of your cluster's state to automatically apply to the cluster. To learn how to use GitOps to deploy an application with an AKS cluster, see the[prerequisites for Azure Kubernetes Service clusters](/en-us/azure/azure-arc/kubernetes/tutorial-use-gitops-flux2?toc=/azure/aks/toc.json#for-azure-kubernetes-service-clusters)in the[GitOps with Flux v2](/en-us/azure/azure-arc/kubernetes/tutorial-use-gitops-flux2?toc=/azure/aks/toc.json)tutorial.**DevOps**: Enables you to build, test, and deploy with continuous integration (CI) and continuous delivery (CD). To see examples of how to use DevOps to deploy an application with an AKS cluster, see[Build and deploy to AKS with Azure Pipelines](devops-pipeline)or[GitHub Actions for deploying to Kubernetes](kubernetes-action).

## Before you begin

In previous tutorials, you packaged an application into a container image, uploaded the image to Azure Container Registry, and created a Kubernetes cluster. To complete this tutorial, you need the precreated `aks-store-quickstart.yaml`

Kubernetes manifest file. This file was downloaded in the application source code from [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.0.53 or later. Check your version with `az --version`

. To install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Update the manifest file

In these tutorials, your Azure Container Registry (ACR) instance stores the container images for the sample application. To deploy the application, you must update the image names in the Kubernetes manifest file to include your ACR login server name.

Get your login server address using the

command and query for your login server.`az acr list`

`az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table`

Make sure you're in the cloned

*aks-store-demo*directory, and then open the`aks-store-quickstart.yaml`

manifest file with a text editor.Update the

`image`

property for the containers by replacing*ghcr.io/azure-samples*with your ACR login server name.`containers: ... - name: order-service image: <acrName>.azurecr.io/aks-store-demo/order-service:latest ... - name: product-service image: <acrName>.azurecr.io/aks-store-demo/product-service:latest ... - name: store-front image: <acrName>.azurecr.io/aks-store-demo/store-front:latest ...`

Save and close the file.


## Run the application

Deploy the application using the

command, which parses the manifest file and creates the defined Kubernetes objects.`kubectl apply`

`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the resources successfully created in the AKS cluster:

`statefulset.apps/rabbitmq created configmap/rabbitmq-enabled-plugins created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`

Check the deployment is successful by viewing the pods with the

`kubectl get pods`

command.`kubectl get pods`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

### Command Line

Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`kubectl get service store-front --watch`

Initially, the

`EXTERNAL-IP`

for the`store-front`

service shows as`<pending>`

:`store-front LoadBalancer 10.0.34.242 <pending> 80:30676/TCP 5s`

When the

`EXTERNAL-IP`

address changes from`<pending>`

to a public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`store-front LoadBalancer 10.0.34.242 52.179.23.131 80:30676/TCP 67s`

View the application in action by opening a web browser and navigating to the external IP address of your service:

`http://<external-ip>`

.

If the application doesn't load, it might be an authorization problem with your image registry. To view the status of your containers, use the `kubectl get pods`

command. If you can't pull the container images, see [Authenticate with Azure Container Registry from Azure Kubernetes Service](cluster-container-registry-integration).

### Azure portal

Navigate to the Azure portal to find your deployment information.

Navigate to your AKS cluster resource.

From the service menu, under

**Kubernetes Resources**, select**Services and ingresses**.Copy the External IP shown in the column for the

`store-front`

service.Paste the IP into your browser to visit your store page.


## Clean up resources

Since you validated the application's functionality, you can now remove the cluster from the application. We will deploy the application again in the next tutorial.

Stop and remove the container instances and resources using the

`kubectl delete`

command.`kubectl delete -f aks-store-quickstart.yaml`

Check that all the application pods have been removed using the

`kubectl get pods`

command.`kubectl get pods`


## Next steps

In this tutorial, you deployed a sample Azure application to a Kubernetes cluster in AKS. You learned how to:

- Update a Kubernetes manifest file.
- Run an application in Kubernetes.
- Test the application.

In the next tutorial, you learn how to use PaaS services for stateful workloads in Kubernetes.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-support-help -->

# Support and troubleshooting for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

## Self help troubleshooting


The [AKS troubleshooting documentation](/en-us/troubleshoot/azure/azure-kubernetes/welcome-azure-kubernetes) provides guidance for how to diagnose and resolve issues that you might encounter when using AKS. These articles cover how to troubleshoot deployment failures, security-related problems, connection issues, and more.

## Post a question on Microsoft Q&A


Azure's preferred destination for community support, [Microsoft Q&A](/en-us/answers/products/azure), allows you to ask technical questions and engage with Azure engineers, Most Valuable Professionals (MVPs), partners, and customers. When you ask a question, make sure you use the `azure-kubernetes-service`

tag. You can also submit your own answers and help other community members with their questions.

If you can't find an answer to your problem using search, you can submit a new question to Microsoft Q&A and tag it with the appropriate Azure service and area.

The following table lists the tags for AKS and related services:

## Create an Azure support request


Explore the range of [Azure support options](https://azure.microsoft.com/support/plans) and choose a plan that best fits your needs. Azure customers can create and manage support requests in the Azure portal.

If you already have an Azure Support Plan, you can [open a support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest).

## Create a GitHub issue


If you need help with the languages and tools for developing and managing AKS, you can open an issue in its GitHub repository.

The following table lists the GitHub repositories for AKS and related services:

| Library | GitHub issues URL |
|---|---|
| Azure PowerShell |
|

[https://github.com/Azure/azure-cli/issues](https://github.com/Azure/azure-cli/issues)[https://github.com/Azure/azure-rest-api-specs/issues](https://github.com/Azure/azure-rest-api-specs/issues)[https://github.com/Azure/azure-sdk-for-java/issues](https://github.com/Azure/azure-sdk-for-java/issues)[https://github.com/Azure/azure-sdk-for-python/issues](https://github.com/Azure/azure-sdk-for-python/issues)[https://github.com/Azure/azure-sdk-for-net/issues](https://github.com/Azure/azure-sdk-for-net/issues)[https://github.com/Azure/azure-sdk-for-js/issues](https://github.com/Azure/azure-sdk-for-js/issues)[https://github.com/Azure/terraform/issues](https://github.com/Azure/terraform/issues)## Stay informed of updates and new releases


Learn about important product updates, roadmap, and announcements in [Azure Updates](https://azure.microsoft.com/updates/?searchterms=compute). For information about Azure Virtual Machines, see the [Azure blog](https://azure.microsoft.com/blog/product/virtual-machines/).

## Next steps

Visit the [Azure Kubernetes Service (AKS) documentation](./).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-kms-v2 -->

# Migrate to Key Management Service (KMS) v2 in Azure Kubernetes Service (AKS) (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

This article applies to clusters using the legacy KMS experience that need to migrate from KMS v1 to KMS v2. For clusters running Kubernetes version 1.33 or later, we recommend using the new [KMS data encryption](kms-data-encryption) experience, which offers platform-managed keys, customer-managed keys with automatic key rotation, and a simplified configuration experience.

In this article, you learn how to migrate to KMS v2 for clusters with versions older than 1.27. Beginning in AKS version 1.27, turning on the KMS feature configures KMS v2. With KMS v2, you aren't limited to the 2,000 secrets that earlier versions support. For more information, see [KMS v2 improvements](https://kubernetes.io/blog/2023/05/16/kms-v2-moves-to-beta/).

Important

If your cluster version is older than 1.27 and you already turned on KMS, the upgrade to cluster version 1.27 or later is blocked.

## Turn off KMS

Disable KMS on an existing cluster using the

command with the`az aks update`

`--disable-azure-keyvault-kms`

parameter.`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --disable-azure-keyvault-kms`

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


## Upgrade your AKS cluster and turn on KMS

Upgrade your AKS cluster to version 1.27 or later using the

command with the`az aks upgrade`

`--kubernetes-version`

parameter set to your desired version. The following example upgrades to version`1.27.1`

:`az aks upgrade --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --kubernetes-version 1.27.1`

Once the upgrade completes, you can turn on KMS for a public or private key vault using one of the following resources:

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


## Next steps

For more information on using KMS with AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-managed-namespaces -->

# Overview of managed namespaces in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic ✔️ AKS Standard

As you manage clusters in Azure Kubernetes Service (AKS), you often need to isolate teams and workloads. With logical isolation, you can use a single AKS cluster for multiple workloads, teams, or environments. Kubernetes namespaces form the logical isolation boundary for workloads and resources. Performing logical isolation involves implementing scripts and processes to create namespaces, set resource limits, apply network policies, and grant team access via role-based access control. Learn how to use managed namespaces in Azure Kubernetes Service (AKS) to simplify namespace management, cluster multi-tenancy, and resource isolation.

Logical separation of clusters usually provides a higher pod density than physically isolated clusters, with less excess compute capacity sitting idle in the cluster. When combined with [cluster autoscaler](cluster-autoscaler) or [Node Auto Provisioning](node-autoprovision), you can scale the number of nodes up or down to meet demands. This best practice approach minimizes costs by running only the required number of nodes.

## Network policies

[Network Policies](use-network-policies) are Kubernetes resources you can use to control the flow of traffic between pods, namespaces, and external endpoints. Network policies allow you to define rules for ingress (incoming) and egress (outgoing) traffic, ensuring that only authorized communication is permitted. By applying network policies, you can enhance the security and isolation of workloads within your cluster.

Note

The default ingress network policy rule of **Allow same namespace** opts for a secure by default stance. If you need your Kubernetes Services, ingresses, or gateways to be accessible from outside of the namespace where they're deployed, for example from an ingress controller deployed in a separate namespace, you need to select **Allow all**. You might then apply your own network policy to restrict ingress to be from that namespace only.

Managed namespaces come with a set of built-in policies.

**Allow all**: Allows all network traffic.**Allow same namespace**: Allows all network traffic within the same namespace.**Deny all**: Denies all network traffic.

You can apply any of the built-in policies on both **ingress** and **egress** rules and they have the following default values.

| Policy | Default value |
|---|---|
| Ingress | Allow same namespace |
| Egress | Allow all |

Note

Users with a `Microsoft.ContainerService/managedClusters/networking.k8s.io/networkpolicies/write`

action, such as `Azure Kubernetes Service RBAC Writer`

, on the Microsoft Entra ID role they're assigned can add more network policies through the Kubernetes API.

For example, if an admin applies a `Deny All`

policy for ingress/egress, and a user applies an `Allow`

policy for a namespace via the Kubernetes API, the `Allow`

policy takes priority over the `Deny All`

policy, and traffic is allowed to flow for the namespace.

## Resource quotas

[Resource Quotas](operator-best-practices-scheduler#enforce-resource-quotas) are Kubernetes resources that are used to manage and limit the resource consumption of namespaces within a cluster. They allow administrators to define constraints on the amount of CPU, memory, storage, or other resources that are used by workloads in a namespace. By applying resource quotas, you can ensure fair resource distribution, prevent resource overuse, and maintain cluster stability.

Managed namespaces can be created with the following resource quotas:

**CPU requests and limits**: Define the minimum and maximum amount of CPU resources that workloads in the namespace can request or consume. The quota ensures that workloads have sufficient CPU resources to operate while preventing overuse that could affect other namespaces. The quota is defined in the[milliCPU form](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-cpu).**Memory requests and limits**: Specify the minimum and maximum amount of memory resources that workloads in the namespace can request or consume. The quota helps maintain stability by avoiding memory overcommitment and ensuring fair resource allocation across namespaces. The quota is defined in[power-of-two equivalents form](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-memory)such as`Ei`

,`Pi`

,`Ti`

,`Gi`

,`Mi`

,`Ki`

.

## Labels and annotations

Kubernetes [Labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) and [Annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) are metadata attached to Kubernetes objects, such as namespaces, to provide additional information. Labels are key-value pairs used to organize and select resources, enabling efficient grouping and querying. Annotations store nonidentifying metadata, such as configuration details or operational instructions, that are consumed by tools or systems.

You can optionally set Kubernetes Labels and Annotations to be applied on the namespace.

## Adoption policy

The adoption policy determines how an existing namespace in Kubernetes is handled when creating a managed namespace.

Warning

Onboarding an existing namespace to be managed can cause disruption. If the **resource quota** applied is less than what is already being requested by pods, new deployments and pods that exceed the quota is denied. Existing deployments aren't affected, but scaling is denied. Applying **network policies** to an existing namespace can affect existing traffic. Ensure that the policies are tested and validated to avoid unintended disruptions to communication between pods or external endpoints.

The following options are available:

**Never**: If the namespace already exists in the cluster, attempts to create that namespace as a managed namespace fails.**IfIdentical**: Take over the existing namespace to be managed, provided there are no differences between the existing namespace and the desired configuration.**Always**: Always take over the existing namespace to be managed, even if some fields in the namespace might be overwritten.

## Delete policy

The delete policy specifies how the Kubernetes namespace is handled when the managed namespace resource is deleted.

Warning

Deleting a managed namespace with the **Delete** policy causes all resources within that namespace, such as Deployments, Services, Ingresses, and other Kubernetes objects, to be deleted. Ensure that you back up or migrate any critical resources before proceeding.

The following options are available:

**Keep**: Only delete the managed namespace resource while keeping the Kubernetes namespace intact. Additionally, the`ManagedByARM`

label is removed from the namespace.**Delete**: Delete both the managed namespace resource and the Kubernetes namespace together.

## Managed namespaces built-in roles

Managed namespaces uses the following built-in roles for the control plane.

| Role | Description |
|---|---|
|

[Azure Kubernetes Service Namespace User](/en-us/azure/role-based-access-control/built-in-roles/containers#azure-kubernetes-service-namespace-user)Managed namespaces uses the following built-in roles for the data plane.

| Role | Description |
|---|---|
|

[Azure Kubernetes Service RBAC Writer](/en-us/azure/role-based-access-control/built-in-roles/containers#azure-kubernetes-service-rbac-writer)[Azure Kubernetes Service RBAC Admin](/en-us/azure/role-based-access-control/built-in-roles/containers#azure-kubernetes-service-rbac-admin)## Managed namespaces use cases

Properly setting up [namespaces](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/) with associated [quotas](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/quota-memory-cpu-namespace/) or [network policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/#networkpolicy-resource) can be complex and time-consuming. Managed namespaces allow you to set up preconfigured namespaces in your AKS clusters that you can interact with using the Azure CLI.

The following sections outline some common use cases for managed namespaces.

### Manage teams and resources on AKS

Let's say you're an admin at a small startup. You have an AKS cluster provisioned and want to set up namespaces for developers from your *finance*, *legal*, and *design* teams. As you're setting up your company's environment, you want to make sure that access is tightly controlled, resources are rightly scoped, and environments are organized properly.

The

*finance*team intakes forms and files from teams all across the company, but they hold sensitive information that ideally shouldn't leave their environment. Their applications and workflows are lighter on the computing side but consume a lot of memory. As a result, you decide to set up a namespace that allows for all network ingress, network egress only within their namespace, and scope their resources accordingly. A label to the namespace helps easily identify which team is using it.`az aks namespace add \ --name $FINANCE_NAMESPACE \ --cluster-name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --cpu-request 250m \ --cpu-limit 500m \ --memory-request 512Mi \ --memory-limit 2Gi \ --ingress-policy AllowAll \ --egress-policy AllowSameNamespace \ --labels team=finance`

The

*legal*team deals primarily with sensitive data. Their applications use a fair amount of memory but require little compute resources. You decide to set up a namespace that's extremely restrictive for both the ingress/egress policies, and scope their resource quotas accordingly.`az aks namespace add \ --name $LEGAL_NAMESPACE \ --cluster-name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --cpu-request 250m \ --cpu-limit 500m \ --memory-request 2Gi \ --memory-limit 5Gi \ --ingress-policy DenyAll \ --egress-policy DenyAll \ --labels team=legal`

The

*design*team needs the ability to freely flow data to showcase their work across the company. They also encourage teams to send them content for reference. Their applications are intensive and require a large chunk of memory and CPU. You decide to set them up with a minimally restrictive namespace and allocate a sizeable amount of resources for them.`az aks namespace add \ --name $DESIGN_NAMESPACE \ --cluster-name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --cpu-request 2000m \ --cpu-limit 2500m \ --memory-request 5Gi \ --memory-limit 8Gi \ --ingress-policy AllowAll \ --egress-policy AllowAll \ --labels team=design`


With these namespaces set up, you now have environments for the three teams in your organization that should allow each team to get up and running in an environment that best suits their needs. Admins can use [Azure CLI calls](/en-us/cli/azure/aks/namespace) to update the namespaces as needs shift.

### View managed namespaces

As the number of teams you deal with expands, or as your organization grows, you might find yourself needing to review the namespaces you set up.

Let's say you want to review the namespaces in your cluster from the [previous section](#manage-teams-and-resources-on-aks) to ensure there are three namespaces.

Use the [ az aks namespace list](/en-us/cli/azure/aks/namespace#az-aks-namespace-list) command to review your namespaces.

```
az aks namespace list \
--cluster-name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--output table
```


Your output should look similar to the following example output:

```
Name ResourceGroup Location
------------------ --------------- ----------
$CLUSTER_NAME/$DESIGN_NAMESPACE $RESOURCE_GROUP <LOCATION>
$CLUSTER_NAME/$LEGAL_NAMESPACE $RESOURCE_GROUP <LOCATION>
$CLUSTER_NAME/$FINANCE_NAMESPACE $RESOURCE_GROUP <LOCATION>
```


### Control access to managed namespaces

You can further use [Azure RBAC roles](#managed-namespaces-built-in-roles), scoped to each namespace, to determine which users have access to certain actions within the namespace. With the proper configuration, you can ensure users have all the access they need within the namespace, while limiting their access to other namespaces or cluster-wide resources.

## Next steps

- Learn how to
[create and use managed namespaces on Azure Kubernetes Service (AKS)](managed-namespaces). - Learn about
[multi-cluster managed namespaces](../kubernetes-fleet/concepts-fleet-managed-namespace)with Azure Kubernetes Fleet Manager.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/workload-identity-overview -->

# Use Microsoft Entra Workload ID with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Workloads deployed on an AKS cluster require Microsoft Entra application credentials or managed identities to access Microsoft Entra protected resources, such as Azure Key Vault and Microsoft Graph. Microsoft Entra Workload ID integrates with the capabilities native to Kubernetes to federate with external identity providers, allowing you to assign workload identities to your workloads to authenticate and access other services and resources.

[Microsoft Entra Workload ID](/en-us/azure/active-directory/develop/workload-identities-overview) uses [Service Account Token Volume Projection](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#serviceaccount-token-volume-projection) (or a *service account*), to enable pods to use a Kubernetes identity. A Kubernetes token is issued and [OpenID Connect (OIDC) federation](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#openid-connect-tokens) enables Kubernetes applications to access Azure resources securely with Microsoft Entra ID, based on annotated service accounts.

You can use Microsoft Entra Workload ID with [Azure Identity client libraries](#azure-identity-client-libraries) or the [Microsoft Authentication Library](/en-us/azure/active-directory/develop/msal-overview) (MSAL) collection, together with [application registration](/en-us/azure/active-directory/develop/application-model#register-an-application), to seamlessly authenticate and access Azure cloud resources.

Note

You can use *Service Connector* to help you configure some steps automatically. For more information, see [What is Service Connector?](/en-us/azure/service-connector/overview)

## Prerequisites

- AKS supports Microsoft Entra Workload ID on version 1.22 and higher.
- The Azure CLI version 2.47.0 or later. Run
`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Limitations

- You can have a maximum of
[20 federated identity credentials](/en-us/azure/active-directory/workload-identities/workload-identity-federation-considerations#general-federated-identity-credential-considerations)per managed identity. - It takes a few seconds for the federated identity credential to propagate after being initially added.
- The
[virtual nodes](virtual-nodes)add-on, based on the open source project[Virtual Kubelet](https://virtual-kubelet.io/docs/), isn't supported. - Creation of federated identity credentials isn't supported on user-assigned managed identities in
[these regions](/en-us/azure/active-directory/workload-identities/workload-identity-federation-considerations#unsupported-regions-user-assigned-managed-identities).

## Azure Identity client libraries

In the Azure Identity client libraries, choose one of the following approaches:

- Use
`DefaultAzureCredential`

, which attempts to use the`WorkloadIdentityCredential`

. - Create a
`ChainedTokenCredential`

instance that includes`WorkloadIdentityCredential`

. - Use
`WorkloadIdentityCredential`

directly.

The following table provides the **minimum** package version required for each language ecosystem's client library:

| Ecosystem | Library | Minimum version |
|---|---|---|
| .NET |
|

[azure-identity-cpp](https://github.com/Azure/azure-sdk-for-cpp/blob/main/sdk/identity/azure-identity/README.md)[azidentity](https://pkg.go.dev/github.com/Azure/azure-sdk-for-go/sdk/azidentity)[azure-identity](/en-us/java/api/overview/azure/identity-readme)[@azure/identity](/en-us/javascript/api/overview/azure/identity-readme)[azure-identity](/en-us/python/api/overview/azure/identity-readme)## Azure Identity client library code samples

The following code samples use the `DefaultAzureCredential`

. This credential type uses the environment variables injected by the workload identity mutating [webhook](#webhook-certificate-auto-rotation) to authenticate with Azure Key Vault. To see samples using one of the other approaches, refer to the [ecosystem-specific client libraries](#azure-identity-client-libraries).

```
using Azure.Identity;
using Azure.Security.KeyVault.Secrets;
string keyVaultUrl = Environment.GetEnvironmentVariable("<key-vault-url>");
string secretName = Environment.GetEnvironmentVariable("<secret-name>");
var client = new SecretClient(
new Uri(keyVaultUrl),
new DefaultAzureCredential());
KeyVaultSecret secret = await client.GetSecretAsync(secretName);
```


## Microsoft Authentication Library (MSAL)

The following client libraries are the **minimum** version required:

| Ecosystem | Library | Image | Example | Has Windows |
|---|---|---|---|---|
| .NET |
|

`ghcr.io/azure/azure-workload-identity/msal-net:latest`

[Link](https://github.com/Azure/azure-workload-identity/tree/main/examples/msal-net/akvdotnet)[Microsoft Authentication Library-for-go](https://github.com/AzureAD/microsoft-authentication-library-for-go)`ghcr.io/azure/azure-workload-identity/msal-go:latest`

[Link](https://github.com/Azure/azure-workload-identity/tree/main/examples/msal-go)[Microsoft Authentication Library-for-java](https://github.com/AzureAD/microsoft-authentication-library-for-java)`ghcr.io/azure/azure-workload-identity/msal-java:latest`

[Link](https://github.com/Azure/azure-workload-identity/tree/main/examples/msal-java)[Microsoft Authentication Library-for-js](https://github.com/AzureAD/microsoft-authentication-library-for-js)`ghcr.io/azure/azure-workload-identity/msal-node:latest`

[Link](https://github.com/Azure/azure-workload-identity/tree/main/examples/msal-node)[Microsoft Authentication Library-for-python](https://github.com/AzureAD/microsoft-authentication-library-for-python)`ghcr.io/azure/azure-workload-identity/msal-python:latest`

[Link](https://github.com/Azure/azure-workload-identity/tree/main/examples/msal-python)## How it works

In this security model, the AKS cluster acts as the token issuer. Microsoft Entra ID uses OIDC to discover public signing keys and verify the authenticity of the service account token before exchanging it for a Microsoft Entra token. Your workload can exchange a service account token projected to its volume for a Microsoft Entra token using the Azure Identity client library or the MSAL.

The following table describes the required OIDC issuer endpoints for Microsoft Entra Workload ID:

| Endpoint | Description |
|---|---|
`{IssuerURL}/.well-known/openid-configuration` |
Also known as the OIDC discovery document. This contains the metadata about the issuer's configurations. |
`{IssuerURL}/openid/v1/jwks` |
This contains the public signing key(s) that Microsoft Entra ID uses to verify the authenticity of the service account token. |

The following diagram summarizes the authentication sequence using OIDC:

### Webhook certificate auto-rotation

Similar to other webhook add-ons, the [cluster certificate auto-rotation](certificate-rotation#certificate-autorotation) operation rotates the certificate.

## Service account labels and annotations

Microsoft Entra Workload ID supports the following mappings related to a service account:

**One-to-one**, where a service account references a Microsoft Entra object.**Many-to-one**, where multiple service accounts reference the same Microsoft Entra object.**One-to-many**, where a service account references multiple Microsoft Entra objects by changing the client ID annotation. For more information, see[How to federate multiple identities with a Kubernetes service account](https://azure.github.io/azure-workload-identity/docs/faq.html#how-to-federate-multiple-identities-with-a-kubernetes-service-account).

Note

If you update the service account annotations, you must restart the pod for the changes to take effect.

If you've used [Microsoft Entra pod-managed identity](use-azure-ad-pod-identity), think of a service account as an Azure security principal, except that a service account is part of the core Kubernetes API, rather than a [Custom Resource Definition](https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/) (CRD). The following sections describe a list of available labels and annotations that you can use to configure the behavior when exchanging the service account token for a Microsoft Entra access token.

### Service account annotations

All annotations are optional. If the annotation isn't specified, the default value is used.

| Annotation | Description | Default |
|---|---|---|
`azure.workload.identity/client-id` |
Represents the Microsoft Entra application client ID to be used with the pod. |
|
`azure.workload.identity/tenant-id` |
Represents the Azure tenant ID where the Microsoft Entra application is registered. |
AZURE_TENANT_ID environment variable extracted from `azure-wi-webhook-config` ConfigMap. |
`azure.workload.identity/service-account-token-expiration` |
Represents the `expirationSeconds` field for the projected service account token. It's an optional field that you configure to prevent any downtime caused by errors during service account token refresh. Kubernetes service account token expiry isn't correlated with Microsoft Entra tokens. Microsoft Entra tokens expire in 24 hours after they're issued. |
3600 Supported range is 3600-86400. |

### Pod labels

Note

For applications using Microsoft Entra Workload ID, it's required to add the label `azure.workload.identity/use: "true"`

to the pod spec for AKS to move the workload identity to a *Fail Close* scenario to provide a consistent and reliable behavior for pods that need to use workload identity. Otherwise, the pods fail after they're restarted.

| Label | Description | Recommended value | Required |
|---|---|---|---|
`azure.workload.identity/use` |
This label is required in the pod template spec. Only pods with this label are mutated by the azure-workload-identity mutating admission webhook to inject the Azure specific environment variables and the projected service account token volume. | true | Yes |

### Pod annotations

All annotations are optional. If the annotation isn't specified, the default value is used.

| Annotation | Description | Default |
|---|---|---|
`azure.workload.identity/service-account-token-expiration` |
See
Pod annotations take precedence over service account annotations. |

Supported range is 3600-86400.

`azure.workload.identity/skip-containers`

`container1;container2`

.`azure.workload.identity/use: true`

.`azure.workload.identity/inject-proxy-sidecar`

`azure.workload.identity/proxy-sidecar-port`

## Migrate to Microsoft Entra Workload ID

You can configure clusters already running a pod-managed identity to use Microsoft Entra Workload ID using one of two ways:

- Use the same configuration you implemented for pod-managed identity. You can annotate the service account within the namespace with the identity to enable Microsoft Entra Workload ID and inject the annotations into the pods.
- Rewrite your application to use the latest version of the Azure Identity client library.

To help streamline and ease the migration process, we developed a migration sidecar that converts the Instance Metadata Service (IMDS) transactions your application makes over to [OIDC](/en-us/azure/active-directory/develop/v2-protocols-oidc). The migration sidecar isn't intended to be a long-term solution, but a way to get up and running quickly on Microsoft Entra Workload ID. Running the migration sidecar within your application proxies the application IMDS transactions over to OIDC. The alternative approach is to upgrade to a supported version of the [Azure Identity](/en-us/azure/active-directory/develop/reference-v2-libraries) client library, which supports OIDC authentication.

The following table summarizes our migration or deployment recommendations for your AKS cluster:

| Scenario | Description |
|---|---|
| New or existing cluster deployment
|

Sample deployment resources:

[Deploy and configure Microsoft Entra Workload ID on a new cluster](workload-identity-deploy-cluster)[migration sidecar](workload-identity-migrate-from-pod-identity).## Next steps

- To learn how to set up your pod to authenticate using a workload identity as a migration option, see
[Modernize application authentication with Microsoft Entra Workload ID](workload-identity-migrate-from-pod-identity). - See
[Deploy and configure an AKS cluster with Microsoft Entra Workload ID](workload-identity-deploy-cluster), which helps you deploy a cluster and configure a sample application to use a workload identity.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-scheduler -->

# Best practices for basic scheduler features in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you manage clusters in Azure Kubernetes Service (AKS), you often need to isolate teams and workloads. The Kubernetes scheduler lets you control the distribution of compute resources, or limit the impact of maintenance events.

This best practices article focuses on basic Kubernetes scheduling features for cluster operators. In this article, you learn how to:

- Use resource quotas to provide a fixed amount of resources to teams or workloads
- Limit the impact of scheduled maintenance using pod disruption budgets

## Enforce resource quotas


Best practice guidancePlan and apply resource quotas at the namespace level. If pods don't define resource requests and limits, reject the deployment. Monitor resource usage and adjust quotas as needed.


Resource requests and limits are placed in the pod specification. Requests are used by the Kubernetes scheduler at deployment time to find an available node in the cluster. Limits and requests work at the individual pod level. For more information about how to define these values, see [Define pod resource requests and limits](developer-best-practices-resource-management#define-pod-resource-requests-and-limits).

To provide a way to reserve and limit resources across a development team or project, you should use *resource quotas*. These quotas are defined on a namespace, and can be used to set quotas on the following basis:

**Compute resources**, such as CPU and memory, or GPUs.**Storage resources**, including the total number of volumes or amount of disk space for a given storage class.**Object count**, such as maximum number of secrets, services, or jobs can be created.

Kubernetes doesn't overcommit resources. Once your cumulative resource request total passes the assigned quota, all further deployments will be unsuccessful.

When you define resource quotas, all pods created in the namespace must provide limits or requests in their pod specifications. If they don't provide these values, you can reject the deployment. Instead, you can [configure default requests and limits for a namespace](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/memory-default-namespace/).

The following example YAML manifest named *dev-app-team-quotas.yaml* sets a hard limit of a total of *10* CPUs, *20Gi* of memory, and *10* pods:

```
apiVersion: v1
kind: ResourceQuota
metadata:
name: dev-app-team
spec:
hard:
cpu: "10"
memory: 20Gi
pods: "10"
```


This resource quota can be applied by specifying the namespace, such as *dev-apps*:

```
kubectl apply -f dev-app-team-quotas.yaml --namespace dev-apps
```


Work with your application developers and owners to understand their needs and apply the appropriate resource quotas.

For more information about available resource objects, scopes, and priorities, see [Resource quotas in Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/).

## Plan for availability using pod disruption budgets


Best practice guidanceTo maintain the availability of applications, define Pod Disruption Budgets (PDBs) to make sure that a minimum number of pods are available in the cluster.


There are two disruptive events that cause pods to be removed:

### Involuntary disruptions

*Involuntary disruptions* are events beyond the typical control of the cluster operator or application owner. Include:

- Hardware failure on the physical machine
- Kernel panic
- Deletion of a node VM

Involuntary disruptions can be mitigated by:

- Using multiple replicas of your pods in a deployment.
- Running multiple nodes in the AKS cluster.

### Voluntary disruptions

*Voluntary disruptions* are events requested by the cluster operator or application owner. Include:

- Cluster upgrades
- Updated deployment template
- Accidentally deleting a pod

Kubernetes provides *pod disruption budgets* for voluntary disruptions, letting you plan for how deployments or replica sets respond when a voluntary disruption event occurs. Using pod disruption budgets, cluster operators can define a minimum available or maximum unavailable resource count.

If you upgrade a cluster or update a deployment template, the Kubernetes scheduler will schedule extra pods on other nodes before allowing voluntary disruption events to continue. The scheduler waits to reboot a node until the defined number of pods are successfully scheduled on other nodes in the cluster.

Let's look at an example of a replica set with five pods that run NGINX. The pods in the replica set are assigned the label `app: nginx-frontend`

. During a voluntary disruption event, such as a cluster upgrade, you want to make sure at least three pods continue to run. The following YAML manifest for a *PodDisruptionBudget* object defines these requirements:

```
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: nginx-pdb
spec:
minAvailable: 3
selector:
matchLabels:
app: nginx-frontend
```


You can also define a percentage, such as *60%*, which allows you to automatically compensate for the replica set scaling up the number of pods.

You can define a maximum number of unavailable instances in a replica set. Again, a percentage for the maximum unavailable pods can also be defined. The following pod disruption budget YAML manifest defines that no more than two pods in the replica set be unavailable:

```
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: nginx-pdb
spec:
maxUnavailable: 2
selector:
matchLabels:
app: nginx-frontend
```


Once your pod disruption budget is defined, you create it in your AKS cluster as with any other Kubernetes object:

```
kubectl apply -f nginx-pdb.yaml
```


Work with your application developers and owners to understand their needs and apply the appropriate pod disruption budgets.

For more information about using pod disruption budgets, see [Specify a disruption budget for your application](https://kubernetes.io/docs/tasks/run-application/configure-pdb/).

## Next steps

This article focused on basic Kubernetes scheduler features. For more information about cluster operations in AKS, see the following best practices:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/localdns-custom -->

# Configure LocalDNS in Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

LocalDNS is a feature in Azure Kubernetes Service (AKS) designed to enhance the Domain Name System (DNS) resolution performance and resiliency for workloads running in your cluster. When you deploy a DNS proxy on each node, LocalDNS reduces DNS query latency, improves reliability during network disruptions, and provides advanced configuration options for DNS caching and forwarding. This article explains how LocalDNS works, its configuration options, and how to enable, verify, and troubleshoot LocalDNS in your AKS clusters.

To learn about what LocalDNS is, including architecture details, and key capabilities, refer to [DNS Resolution in Azure Kubernetes Service (AKS)](dns-concepts).

## Best practices for LocalDNS configuration

When implementing LocalDNS in your AKS clusters, consider the following best practices:

**Start with a minimal configuration**: Begin with a simple configuration that uses the`Preferred`

mode to validate your LocalDNS configuration syntax before moving to`Required`

mode. The`Preferred`

mode validates your configuration without enabling LocalDNS, allowing you to catch configuration errors early without impacting your cluster.**Implement proper caching strategies**: Configure cache settings based on your workload characteristics:- For frequently changing records, use shorter
`cacheDurationInSeconds`

values. When doing so, it's important to note that cacheDurationInSeconds acts as a cap on the DNS record TTL but doesn't increase it. The resulting TTL is the smaller of what is returned from upstream or what is set in the cache plugin. - For stable records, use longer cache durations to reduce DNS queries.
- Enable
`serveStale`

with appropriate settings to maintain service during DNS outages. - Caching with LocalDNS operates on a best effort basis and doesn't guarantee stale responses. The cache is divided into 256 shards and with a default maximum of 10,000 entries, allowing each shard to hold about 39 entries. When a shard is full and a new entry needs to be added, one of the existing entries is chosen at random to be evicted. There's no preference for older or expires entries. As a result, a stale record might not always be available, especially under high query volume.

- For frequently changing records, use shorter
**Monitor DNS performance**: After enabling LocalDNS, monitor your application's DNS performance using:- Application performance metrics.
- Node metrics to detect reduced network pressure.
- Log entries when
`queryLogging`

is set to`Log`

.

**Follow least privilege principle**: When configuring DNS forwarding rules, only allow access to the required DNS servers and domains.**Test before production deployment**: Always test LocalDNS configuration in a nonproduction environment before rolling it out to production clusters.**Use Infrastructure as Code (IaC)**: Store your*localdnsconfig.json*file in your infrastructure repository and include it in your AKS deployment templates.**Network configuration for TCP forwarding**: When using TCP for DNS forwarding to VnetDNS, ensure that your Network Security Groups (NSGs), firewalls, or Network Virtual Appliances (NVAs) don't block TCP traffic between CoreDNS/LocalDNS and VnetDNS servers.**Avoid enabling both NodeLocal DNSCache and LocalDNS**: It isn't recommended to enable both the upstream Kubernetes NodeLocal DNSCache and LocalDNS in your node pool. While AKS doesn't block this configuration, all DNS traffic is routed through LocalDNS, which might lead to unexpected behavior or reduced benefits from NodeLocal DNSCache.

## Prerequisites

You must have an existing AKS cluster with Kubernetes versions 1.31 and later to use LocalDNS. If you need an AKS cluster, you can create one using

[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal).This article requires Azure CLI version 2.80.0 and later. If you're using Azure Cloud Shell, the latest version is already installed.

LocalDNS is only supported on node pools running Azure Linux or Ubuntu 22.04 and newer.

The Virtual Machine (VM) SKU used for your node pool must have at least 4 vCPUs (cores) to support LocalDNS.

LocalDNS isn't compatible with applied Fully Qualified Domain Names (FQDN) filter policies in

[Advanced Container Networking Services (ACNS)](how-to-apply-fqdn-filtering-policies).

## Manage LocalDNS on an AKS cluster

LocalDNS is configured at the node pool level in AKS, meaning you can enable or disable LocalDNS independently for each node pool in your cluster. This tailors DNS resolution behavior based on the specific requirements of different workloads or environments. To enable LocalDNS on a node pool, you need to provide a configuration file: *localdnsconfig.json* that defines how LocalDNS should operate for that node pool.

If you don't specify a custom configuration file, AKS automatically applies a default LocalDNS configuration.

Note

If you're using Node Auto-Provisioning (NAP), see [LocalDNS configuration](node-auto-provisioning-aksnodeclass#localdns-configuration) for instructions on how to enable LocalDNS with NAP.

To enable LocalDNS during node pool creation, use the following command with your custom configuration file:

```
az aks nodepool add --name mynodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --localdns-config ./localdnsconfig.json
```


To enable LocalDNS on an existing node pool, use the following command with your custom configuration file:

```
az aks nodepool update --name mynodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --localdns-config ./localdnsconfig.json
```


Important

Enabling LocalDNS on a node pool initiates a reimage operation on all nodes within that pool. This process can cause temporary disruption to running workloads and might lead to application downtime if not properly managed. You should plan for potential service interruptions and ensure that the applications are configured for high availability or have appropriate disruption budgets in place before enabling this setting.
