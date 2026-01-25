---
merged_at: 2026-01-25T12:25:33.911924
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: dapr-troubleshooting.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/dapr-troubleshooting -->

# Troubleshoot Dapr extension installation errors

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article discusses some common error messages that you may receive when you install or update the [Distributed Application Runtime (Dapr)](https://dapr.io/) extension for Microsoft Azure Kubernetes Service (AKS) or Arc for Kubernetes.

[Learn more about the level of support provided for the Dapr extension.](#next-steps)

## Scenario 1: Installation fails but doesn't show an error message

If the extension generates an error message when you create or update it, you can inspect where the creation failed by running the [az k8s-extension list](/en-us/cli/azure/k8s-extension#az-k8s-extension-list) command:

```
az k8s-extension list --resource-group <my-resource-group-name> \
--cluster-name <my-cluster-name> \
--cluster-type managedClusters
```


If a wrong key is used in the configuration settings, such as `global.ha=false`

instead of `global.ha.enabled=false`

, the following JSON status is returned. The error message is captured in the `message`

property.

```
"statuses": [
{
"code": "InstallationFailed",
"displayStatus": null,
"level": null,
"message": "Error: {failed to install chart from path [] for release [dapr-1]: err [template: dapr/charts/dapr_sidecar_injector/templates/dapr_sidecar_injector_poddisruptionbudget.yaml:1:17: executing \"dapr/charts/dapr_sidecar_injector/templates/dapr_sidecar_injector_poddisruptionbudget.yaml\" at <.Values.global.ha.enabled>: can't evaluate field enabled in type interface {}]} occurred while doing the operation : {Installing the extension} on the config",
"time": null
}
],
```


Here's another example of a JSON error message:

```
"statuses": [
{
"code": "InstallationFailed",
"displayStatus": null,
"level": null,
"message": "The extension operation failed with the following error: unable to add the configuration with configId {extension:microsoft-dapr} due to error: {error while adding the CRD configuration: error {failed to get the immutable configMap from the elevated namespace with err: configmaps 'extension-immutable-values' not found }}. (Code: ExtensionOperationFailed)",
"time": null
}
]
```


### Solution 1: Restart the cluster, register the service provider, or delete and reinstall Dapr

To fix this issue, try the following methods:

Force delete and

[reinstall the Dapr extension](/en-us/azure/aks/dapr).

## Scenario 2: Targeted Dapr version doesn't exist

When you try to install the Dapr extension to [target a specific version](/en-us/azure/aks/dapr#targeting-a-specific-dapr-version), you receive an error message that states that the Dapr version doesn't exist:

(ExtensionOperationFailed) The extension operation failed with the following error: Failed to resolve the extension version from the given values.

Code: ExtensionOperationFailed

Message: The extension operation failed with the following error: Failed to resolve the extension version from the given values.


### Solution 2: Install again for a supported Dapr version

Try again to install the extension. Make sure that you use a [supported version of Dapr](/en-us/azure/aks/dapr#dapr-versions).

## Scenario 3: The targeted Dapr version exists but not in the specified region

Because some versions of Dapr aren't available in all regions, you might receive the following error message:

(ExtensionTypeRegistrationGetFailed) Extension type microsoft.dapr is not registered in region <regionname>.

Code: ExtensionTypeRegistrationGetFailed

Message: Extension type microsoft.dapr is not registered in region <regionname>


### Solution 3: Install in a different region

Install in a [region in which your Dapr version is supported](/en-us/azure/aks/dapr#cloudsregions).

## Scenario 4: Dapr is already installed

You try to install the Dapr extension for AKS or Arc for Kubernetes, but you receive an error message that indicates that the `dapr-system`

namespace already exists. This error message resembles the following text:

(ExtensionOperationFailed) The extension operation failed with the following error: Error: {failed to install chart from path [] for release [dapr-ext]: err [rendered manifests contain a resource that already exists. Unable to continue with install: ServiceAccount "dapr-operator" in namespace "dapr-system" exists and cannot be imported into the current release: invalid ownership metadata; annotation validation error: key "meta.helm.sh/release-name" must equal "dapr-ext": current value is "dapr"]} occurred while doing the operation : {Installing the extension} on the config


### Solution 4: Uninstall Dapr OSS first

Uninstall the Dapr OSS before you install the Dapr extension. For more information, see [Migrate from Dapr OSS to the Dapr extension for AKS](/en-us/azure/aks/dapr-migration).

## Scenario 5: The placement server pod is in a bad state

You encounter the following error:

0/4 nodes are available: 1 node(s) were unschedulable, 3 node(s) had volume node affinity conflict. preemption: 0/4 nodes are available: 4 Preemption is not helpful for scheduling.


This issue might happen when the placement server pod tries to use the persistent volume that's created in a different zone from the placement server pod itself.

### Solution 5: Install Dapr in multiple availability zones or limit the placement service to a particular availability zone

To resolve this issue, use one of the following methods:

Follow the recommended approach in

[Install Dapr in multiple availability zones while in HA mode](/en-us/azure/aks/dapr-settings#install-dapr-in-multiple-availability-zones-while-in-ha-mode).Limit the placement service to a particular availability zone by creating a custom storage class and using it for the placement service, and then run the following command:

`az k8s-extension create --cluster-type managedClusters --cluster-name <clustername> --resource-group <resourcegroup> --name <name> --extension-type Microsoft.Dapr --auto-upgrade-minor-version <minorversion> --version <version> --configuration-settings "dapr_placement.volumeclaims.storageClassName=zone-restricted"`

Here's an example of creating a custom storage class:

`kind: StorageClass apiVersion: storage.k8s.io/v1 metadata: name: zone-restricted provisioner: disk.csi.azure.com reclaimPolicy: Delete allowVolumeExpansion: true volumeBindingMode: WaitForFirstConsumer allowedTopologies: - matchLabelExpressions: - key: topology.kubernetes.io/zone values: - centralus-1 parameters: storageaccounttype: StandardSSD_LRS`


## Next steps

If you're still experiencing installation issues, [create a support request](https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview?DMC=troubleshoot) for Microsoft to investigate and resolve.

If you're experiencing Dapr runtime security risks and regressions while using the extension, open an issue with the [Dapr open source project](https://github.com/dapr/dapr/issues/new/choose).

Note

Learn more about [how Microsoft handles issues raised for the Dapr extension](/en-us/azure/aks/dapr-overview#issue-handling).

You could also start a discussion in the Dapr project Discord:

**Third-party information disclaimer**

The third-party products that this article discusses are manufactured by companies that are independent of Microsoft. Microsoft makes no warranty, implied or otherwise, about the performance or reliability of these products.


---

<!-- DOCUMENTO FUSIONADO: control-kubeconfig-access.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/control-kubeconfig-access -->

# Use Azure role-based access control to define access to the Kubernetes configuration file in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can interact with Kubernetes clusters using the `kubectl`

tool. The Azure CLI provides an easy way to get the access credentials and *kubeconfig* configuration file to connect to your AKS clusters using `kubectl`

. You can use Azure role-based access control (Azure RBAC) to limit who can get access to the *kubeconfig* file and the permissions they have.

This article shows you how to assign Azure roles that limit who can get the configuration information for an AKS cluster.

## Before you begin

- This article assumes that you have an existing AKS cluster. If you need an AKS cluster, create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[the Azure portal](learn/quick-kubernetes-deploy-portal). - This article also requires that you're running Azure CLI version 2.0.65 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Available permissions for cluster roles

When you interact with an AKS cluster using the `kubectl`

tool, a configuration file, called *kubeconfig*, defines cluster connection information. This configuration file is typically stored in *~/.kube/config*. Multiple clusters can be defined in this *kubeconfig* file. You can switch between clusters using the [ kubectl config use-context](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#config) command.

The [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command lets you get the access credentials for an AKS cluster and merges these credentials into the

*kubeconfig*file. You can use Azure RBAC to control access to these credentials. These Azure roles let you define who can retrieve the

*kubeconfig*file and what permissions they have within the cluster.

There are two Azure roles you can apply to a Microsoft Entra user or group:

**Azure Kubernetes Service Cluster Admin Role**- Allows access to
`Microsoft.ContainerService/managedClusters/listClusterAdminCredential/action`

API call. This API call[lists the cluster admin credentials](/en-us/rest/api/aks/managedclusters/listclusteradmincredentials). - Downloads
*kubeconfig*for the*clusterAdmin*role.

- Allows access to
**Azure Kubernetes Service Cluster User Role**- Allows access to
`Microsoft.ContainerService/managedClusters/listClusterUserCredential/action`

API call. This API call[lists the cluster user credentials](/en-us/rest/api/aks/managedclusters/listclusterusercredentials). - Downloads
*kubeconfig*for*clusterUser*role.

- Allows access to

Note

On clusters that use Microsoft Entra ID, users with the *clusterUser* role have an empty *kubeconfig* file that prompts a login. Once logged in, users have access based on their Microsoft Entra user or group settings. Users with the *clusterAdmin* role have admin access.

On clusters that don't use Microsoft Entra ID, the *clusterUser* role has same effect of *clusterAdmin* role.

## Assign role permissions to a user or group

To assign one of the available roles, you need to get the resource ID of the AKS cluster and the ID of the Microsoft Entra user account or group using the following steps:

- Get the cluster resource ID using the
command for the cluster named`az aks show`

*myAKSCluster*in the*myResourceGroup*resource group. Provide your own cluster and resource group name as needed. - Use the
and`az account show`

commands to get your user ID.`az ad user show`

- Assign a role using the
command.`az role assignment create`


The following example assigns the *Azure Kubernetes Service Cluster Admin Role* to an individual user account:

```
# Get the resource ID of your AKS cluster
AKS_CLUSTER=$(az aks show --resource-group myResourceGroup --name myAKSCluster --query id -o tsv)
# Get the account credentials for the logged in user
ACCOUNT_UPN=$(az account show --query user.name -o tsv)
ACCOUNT_ID=$(az ad user show --id $ACCOUNT_UPN --query objectId -o tsv)
# Assign the 'Cluster Admin' role to the user
az role assignment create \
--assignee $ACCOUNT_ID \
--scope $AKS_CLUSTER \
--role "Azure Kubernetes Service Cluster Admin Role"
```


If you want to assign permissions to a Microsoft Entra group, update the `--assignee`

parameter shown in the previous example with the object ID for the *group* rather than the *user*.

To get the object ID for a group, use the [ az ad group show](/en-us/cli/azure/ad/group#az-ad-group-show) command. The following command gets the object ID for the Microsoft Entra group named

*appdev*:

```
az ad group show --group appdev --query objectId -o tsv
```


Important

In some cases, such as Microsoft Entra guest users, the *user.name* in the account is different than the *userPrincipalName*.

```
$ az account show --query user.name -o tsv
user@contoso.com
$ az ad user list --query "[?contains(otherMails,'user@contoso.com')].{UPN:userPrincipalName}" -o tsv
user_contoso.com#EXT#@contoso.onmicrosoft.com
```


In this case, set the value of *ACCOUNT_UPN* to the *userPrincipalName* from the Microsoft Entra user. For example, if your account *user.name* is *user@contoso.com*, this action would look like the following example:

```
ACCOUNT_UPN=$(az ad user list --query "[?contains(otherMails,'user@contoso.com')].{UPN:userPrincipalName}" -o tsv)
```


## Get and verify the configuration information

Once the roles are assigned, use the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command to get the

*kubeconfig*definition for your AKS cluster. The following example gets the

*--admin*credentials, which works correctly if the user has been granted the

*Cluster Admin Role*:

```
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --admin
```


You can then use the [ kubectl config view](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#config) command to verify that the

*context*for the cluster shows that the admin configuration information has been applied.

```
$ kubectl config view
```


Your output should look similar to the following example output:

```
apiVersion: v1
clusters:
- cluster:
certificate-authority-data: DATA+OMITTED
server: https://myaksclust-myresourcegroup-19da35-4839be06.hcp.eastus.azmk8s.io:443
name: myAKSCluster
contexts:
- context:
cluster: myAKSCluster
user: clusterAdmin_myResourceGroup_myAKSCluster
name: myAKSCluster-admin
current-context: myAKSCluster-admin
kind: Config
preferences: {}
users:
- name: clusterAdmin_myResourceGroup_myAKSCluster
user:
client-certificate-data: REDACTED
client-key-data: REDACTED
token: e9f2f819a4496538b02cefff94e61d35
```


## Remove role permissions

To remove role assignments, use the [ az role assignment delete](/en-us/cli/azure/role/assignment#az-role-assignment-delete) command. Specify the account ID and cluster resource ID that you obtained in the previous steps. If you assigned the role to a group rather than a user, specify the appropriate group object ID rather than account object ID for the

`--assignee`

parameter.```
az role assignment delete --assignee $ACCOUNT_ID --scope $AKS_CLUSTER
```


## Next steps

For enhanced security on access to AKS clusters, [integrate Microsoft Entra authentication](azure-ad-integration-cli).
