---
merged_at: 2026-01-25T12:25:33.938469
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: enable-authentication-microsoft-entra-id.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/enable-authentication-microsoft-entra-id -->

# Enable AKS-managed Microsoft Entra integration for Kubernetes clusters with kubelogin

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The AKS-managed Microsoft Entra integration simplifies the Microsoft Entra integration process. Previously, you were required to create a client and server app, and the Microsoft Entra tenant had to assign [Directory Readers](/en-us/entra/identity/role-based-access-control/permissions-reference#directory-readers) role permissions. Now, the Azure Kubernetes Service (AKS) resource provider manages the client and server apps for you.

Cluster administrators can configure Kubernetes role-based access control (Kubernetes RBAC) based on a user's identity or directory group membership. Microsoft Entra authentication is provided to AKS clusters with OpenID Connect. OpenID Connect is an identity layer built on top of the OAuth 2.0 protocol. For more information on OpenID Connect, see the [OpenID Connect documentation](/en-us/entra/identity-platform/v2-protocols-oidc).

Learn more about the Microsoft Entra integration flow in the [Microsoft Entra documentation](concepts-identity#azure-ad-integration).

## Limitations

The following are constraints to integrate authentication on AKS:

- Integration can't be disabled after being added.
- Downgrades from an integrated cluster to the legacy Microsoft Entra ID clusters aren't supported.
- Clusters without Kubernetes RBAC support are unable to add the integration.

## Before you begin

To install the AKS addon, verify you have the following items:

- You have Azure CLI version 2.29.0 or later installed and configured. To find the version, run the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need
`kubectl`

with a minimum version of[1.18.1](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.18.md#v1181)or. With the Azure CLI and the Azure PowerShell module, these two commands are included and automatically managed. Meaning, they're upgraded by default and running`kubelogin`

`az aks install-cli`

isn't required or recommended. If you're using an automated pipeline, you need to manage upgrades for the correct or latest version. The difference between the minor versions of Kubernetes and`kubectl`

shouldn't be more than*one*version. Otherwise, authentication issues occur on the wrong version. - If you're using
[helm](https://github.com/helm/helm), you need a minimum version of helm 3.3. - This configuration requires you have a Microsoft Entra group for your cluster. This group is registered as an admin group on the cluster to grant admin permissions. If you don't have an existing Microsoft Entra group, you can create one using the
command.`az ad group create`


Note

Microsoft Entra integrated clusters using a Kubernetes version newer than version 1.24 automatically use the `kubelogin`

format. Beginning with Kubernetes version 1.24, the default format of the `clusterUser`

credential for Microsoft Entra ID clusters is `exec`

, which requires [ kubelogin](https://github.com/Azure/kubelogin) binary in the execution

`PATH`

. There's no behavior change for non-Microsoft Entra clusters, or Microsoft Entra ID clusters running a version older than 1.24.
Existing downloaded `kubeconfig`

continues to work. An optional query parameter `format`

is included when getting `clusterUser`

credential to overwrite the default behavior change. You can explicitly specify format to `azure`

if you need to maintain the old `kubeconfig`

format.## Enable the integration on your AKS cluster

### Create a new cluster

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location centralus`

Create an AKS cluster and enable administration access for your Microsoft Entra group using the

command.`az aks create`

`az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-aad \ --aad-admin-group-object-ids <id> \ --aad-tenant-id <id> \ --generate-ssh-keys`

A successful creation of an AKS-managed Microsoft Entra ID cluster has the following section in the response body.

`"AADProfile": { "adminGroupObjectIds": [ "aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb" ], "clientAppId": null, "managed": true, "serverAppId": null, "serverAppSecret": null, "tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee" }`


### Use an existing cluster

Enable AKS-managed Microsoft Entra integration on your existing Kubernetes RBAC enabled cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. Make sure to set your admin group to keep access on your cluster.

```
az aks update \
--resource-group MyResourceGroup \
--name myManagedCluster \
--enable-aad \
--aad-admin-group-object-ids <id-1>,<id-2> \
--aad-tenant-id <id>
```


A successful activation of an AKS-managed Microsoft Entra ID cluster has the following section in the response body:

```
"AADProfile": {
"adminGroupObjectIds": [
"aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
],
"clientAppId": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee"
}
```


### Migrate legacy cluster to integration

If your cluster uses legacy Microsoft Entra integration, you can upgrade to AKS-managed Microsoft Entra integration through the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

Warning

Free tier clusters might experience API server downtime during the upgrade. We recommend upgrading during your nonbusiness hours.
After the upgrade, the `kubeconfig`

content changes. You need to run `az aks get-credentials --resource-group <AKS resource group name> --name <AKS cluster name>`

to merge the new credentials into the `kubeconfig`

file.

```
az aks update \
--resource-group myResourceGroup \
--name myManagedCluster \
--enable-aad \
--aad-admin-group-object-ids <id> \
--aad-tenant-id <id>
```


A successful migration of an AKS-managed Microsoft Entra ID cluster has the following section in the response body:

```
"AADProfile": {
"adminGroupObjectIds": [
"aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
],
"clientAppId": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee"
}
```


## Access your enabled cluster

Get the user credentials to access your cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myManagedCluster`

Follow your sign in instructions.

Set

`kubelogin`

to use the Azure CLI.`kubelogin convert-kubeconfig -l azurecli`

View the nodes in the cluster with the

`kubectl get nodes`

command.`kubectl get nodes`


## Non-interactive sign-in with kubelogin

There are some non-interactive scenarios that don't support `kubectl`

. In these cases, use [ kubelogin](https://github.com/Azure/kubelogin) to connect to the cluster with a non-interactive service principal credential to perform continuous integration pipelines.

Note

Microsoft Entra integrated clusters using a Kubernetes version newer than version 1.24 automatically use the `kubelogin`

format. Beginning with Kubernetes version 1.24, the default format of the `clusterUser`

credential for Microsoft Entra ID clusters is `exec`

, which requires [ kubelogin](https://github.com/Azure/kubelogin) binary in the execution PATH. There's no behavior change for non-Microsoft Entra clusters, or Microsoft Entra ID clusters running a version older than 1.24.
Existing downloaded

`kubeconfig`

continues to work. An optional query parameter `format`

is included when getting `clusterUser`

credential to overwrite the default behavior change. You can explicitly specify format to `azure`

if you need to maintain the old `kubeconfig`

format.When getting the `clusterUser`

credential, you can use the `format`

query parameter to overwrite the default behavior. You can set the value to `azure`

to use the original `kubeconfig`

format:

```
az aks get-credentials --format azure
```


If your Microsoft Entra integrated cluster uses Kubernetes version 1.24 or lower, you need to manually convert the `kubeconfig`

format.

```
export KUBECONFIG=/path/to/kubeconfig
kubelogin convert-kubeconfig
```


If you receive the message **error: The Azure auth plugin has been removed.**, you need to run the command `kubelogin convert-kubeconfig`

to convert the `kubeconfig`

format manually. For more information, see [Azure Kubelogin Known Issues](https://azure.github.io/kubelogin/known-issues.html).

## Troubleshoot access issues

Important

The step described in this section suggests an alternative authentication method compared to the normal Microsoft Entra group authentication. Use this option only in an emergency.

If you lack administrative access to a valid Microsoft Entra group, you can follow this workaround. Sign in with an account that is a member of the [Azure Kubernetes Service Cluster Admin](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-cluster-admin-role) role and grant your group or tenant admin credentials to access your cluster.

## Next steps

- Learn about
[Microsoft Entra integration with Kubernetes RBAC](azure-ad-rbac). - Learn more about
[AKS and Kubernetes identity concepts](concepts-identity). - Learn how to
[use kubelogin](kubelogin-authentication)for all supported Microsoft Entra authentication methods in AKS. - Use
[Azure Resource Manager templates](/en-us/azure/templates/microsoft.containerservice/managedclusters)to create AKS-managed Microsoft Entra ID enabled clusters.


---

<!-- DOCUMENTO FUSIONADO: auto-upgrade-cluster.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-cluster -->

# Automatically upgrade an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Part of the AKS cluster lifecycle involves performing periodic upgrades to the latest Kubernetes version. It's important you apply the latest security releases or upgrade to get the latest features. Before you learn about automatic upgrades, make sure you understand the [AKS cluster upgrade fundamentals](upgrade-cluster).

Note

Any upgrade operation, whether performed manually or automatically, upgrades the node image version if it's not already on the latest version. The latest version is contingent on a full AKS release and can be determined by visiting the [AKS release tracker](release-tracker).

Autoupgrade first upgrades the control plane, and then upgrades agent pools one by one.

## Why use cluster autoupgrade

Cluster autoupgrade provides a *set once and forget* mechanism that yields tangible time and operational cost benefits. You don't need to stop your workloads, redeploy your workloads, or create a new AKS cluster. By enabling autoupgrade, you can ensure your clusters are up to date and don't miss the latest features or patches from AKS and upstream Kubernetes.

AKS follows a strict supportability versioning window. With properly selected autoupgrade channels, you can avoid clusters falling into an unsupported version. For more on the AKS support window, see [Alias minor versions](supported-kubernetes-versions).

## Customer versus AKS-initiated autoupgrades

You can specify cluster autoupgrade specifics using the following guidance. The upgrades occur based on your specified cadence and are recommended to remain on supported Kubernetes versions.

AKS also initiates autoupgrades for unsupported clusters. When a cluster in an n-3 version (where n is the latest supported AKS GA minor version) is about to drop to n-4, AKS automatically upgrades the cluster to n-2 to remain in an AKS support [policy](supported-kubernetes-versions). Automatically upgrading a platform supported cluster to a supported version is enabled by default. Stopped node pools are upgraded during an autoupgrade operation. The upgrade applies to nodes when the node pool is started. To minimize disruptions, set up [maintenance windows](planned-maintenance).

## Cluster autoupgrade limitations

If you're using cluster autoupgrade, you can no longer upgrade the control plane first, and then upgrade the individual node pools. Cluster autoupgrade always upgrades the control plane and the node pools together. You can't upgrade the control plane only. Running the `az aks upgrade --control-plane-only`

command raises the following error:

```
NotAllAgentPoolOrchestratorVersionSpecifiedAndUnchanged: Using managed cluster api, all Agent pools' OrchestratorVersion must be all specified or all unspecified. If all specified, they must be stay unchanged or the same with control plane.
```


If using the `node-image`

(legacy and not to be used) cluster autoupgrade channel or the `NodeImage`

node image autoupgrade channel, Linux [unattended upgrades](https://help.ubuntu.com/community/AutomaticSecurityUpdates) are disabled by default.

## Cluster autoupgrade channels

Automatically completed upgrades are functionally the same as manual upgrades. The [selected autoupgrade channel](planned-maintenance) determines the timing of upgrades. When making changes to autoupgrade, allow 24 hours for the changes to take effect. Automatically upgrading a cluster follows the same process as manually upgrading a cluster. For more information, see [Upgrade an AKS cluster](upgrade-cluster).

The following upgrade channels are available:

| Channel | Action | Example |
|---|---|---|
`none` |
disables autoupgrades and keeps the cluster at its current version of Kubernetes. | Default setting if left unchanged. |
`patch` |
automatically upgrades the cluster to the latest supported patch version when it becomes available while keeping the minor version the same. | For example, if a cluster runs version 1.17.7, and versions 1.17.9, 1.18.4, 1.18.6, and 1.19.1 are available, the cluster upgrades to 1.17.9. |
`stable` |
automatically upgrades the cluster to the latest supported patch release on minor version N-1, where N is the latest supported minor version. |
For example, if a cluster runs version 1.17.7 and versions 1.17.9, 1.18.4, 1.18.6, and 1.19.1 are available, the cluster upgrades to 1.18.6. |
`rapid` |
automatically upgrades the cluster to the latest supported patch release on the latest supported minor version. | In cases where the cluster's Kubernetes version is an N-2 minor version, where N is the latest supported minor version, the cluster first upgrades to the latest supported patch version on N-1 minor version. For example, if a cluster runs version 1.17.7 and versions 1.17.9, 1.18.4, 1.18.6, and 1.19.1 are available, the cluster first upgrades to 1.18.6, then upgrades to 1.19.1. |
`node-image` (legacy) |
automatically upgrades the node image to the latest version available. | Microsoft provides patches and new images for image nodes frequently (weekly), but your running nodes don't get the new images unless you do a node image upgrade. Turning on the node-image channel automatically updates your node images whenever a new version is available. If you use this channel, Linux [unattended upgrades] are disabled by default. Node image upgrades work on patch versions that are deprecated, so long as the minor Kubernetes version is still supported. This channel is no longer recommended and is planned for deprecation in future. For an option that can automatically upgrade node images, see the `NodeImage` channel in
|

Note

Keep the following information in mind when using cluster autoupgrade:

Cluster autoupgrade only updates to GA versions of Kubernetes and doesn't update to preview versions.

With AKS, you can create a cluster without specifying the exact patch version. When you create a cluster without designating a patch, the cluster runs the minor version's latest GA patch. To learn more, see

[AKS support window](supported-kubernetes-versions).Autoupgrade requires the cluster's Kubernetes version to be within the

[AKS support window](supported-kubernetes-versions), even if using the`node-image`

channel.If you're using the preview API

`11-02-preview`

or later, and you select the`node-image`

cluster autoupgrade channel, the[node image autoupgrade channel](auto-upgrade-node-image)automatically sets to`NodeImage`

.Each cluster can only be associated with a single autoupgrade channel. The reason is because your specified channel determines the Kubernetes version that runs on the cluster.

If your cluster has no autoupgrade channel and you enable it for Long-Term Support (LTS), the cluster defaults to a

`patch`

autoupgrade channel.

## Use cluster autoupgrade with a new AKS cluster

Set the autoupgrade channel when creating a new cluster using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command and the

`auto-upgrade-channel`

parameter.```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="myResourceGroup$RANDOM_SUFFIX"
export AKS_CLUSTER_NAME="myAKSCluster"
az aks create --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER_NAME --auto-upgrade-channel stable --generate-ssh-keys
```


## Use cluster autoupgrade with an existing AKS cluster

Set the autoupgrade channel on an existing cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`auto-upgrade-channel`

parameter.```
az aks update --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER_NAME --auto-upgrade-channel stable
```


Results:

```
{
"id": "/subscriptions/aaaa6a6a-bb7b-cc8c-dd9d-eeeeee0e0e0e/resourceGroups/myResourceGroupabc123/providers/Microsoft.ContainerService/managedClusters/myAKSCluster",
"properties": {
"autoUpgradeChannel": "stable",
"provisioningState": "Succeeded"
}
}
```


## Use autoupgrade with Planned Maintenance

If using Planned Maintenance and cluster autoupgrade, your upgrade starts during your specified maintenance window.

Note

To ensure proper functionality, use a maintenance window of *four hours or more*.

For more information on how to set a maintenance window with Planned Maintenance, see [Use Planned Maintenance to schedule maintenance windows for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Best practices for cluster autoupgrade

Use the following best practices to help maximize your success when using autoupgrade:

- To ensure your cluster is always in a supported version, for example within the N-2 rule, choose either
`stable`

or`rapid`

channels. - If you're interested in getting the latest patches as soon as possible, use the
`patch`

channel. The`node-image`

channel is a good fit if you want your agent pools to always run the most recent node images. - To automatically upgrade node images while using a different cluster upgrade channel, consider using the
[node image autoupgrade](auto-upgrade-node-image)`NodeImage`

channel. - Follow
[Operator best practices](operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets). - Follow
[PodDisruptionBudget (PDB) best practices](https://kubernetes.io/docs/tasks/run-application/configure-pdb/). - For upgrade troubleshooting information, see the
[AKS troubleshooting documentation](/en-us/support/azure/azure-kubernetes/welcome-azure-kubernetes).

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).
