---
merged_at: 2026-01-25T12:25:33.963737
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: azure-ad-rbac.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-ad-rbac -->

# Use Kubernetes RBAC with Microsoft Entra ID in AKS

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) can be configured to use Microsoft Entra ID for user authentication. In this configuration, you sign in to an AKS cluster using a Microsoft Entra authentication token. Once authenticated, you can use the built-in Kubernetes role-based access control (RBAC) to manage access to namespaces and cluster resources based on a user's identity or group membership.

This article shows you how to:

Control access using Kubernetes RBAC in an AKS cluster based on Microsoft Entra group membership.

Create example groups and users in Microsoft Entra ID.

Create Roles and RoleBindings in an AKS cluster granting the appropriate permissions, such as to create and view resources.


## Prerequisites

You have an existing AKS cluster with Microsoft Entra integration enabled. If you need an AKS cluster with this configuration, see

[Integrate Microsoft Entra ID with AKS](managed-azure-ad).Kubernetes RBAC is enabled by default during AKS cluster creation. To upgrade an existing cluster with Microsoft Entra integration and Kubernetes RBAC, see

[Enable Microsoft Entra integration on your existing AKS cluster](managed-azure-ad#use-an-existing-cluster).Make sure that Azure CLI version 2.0.61 or later is installed and configured. To find the version, run

`az --version`

. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).If using Terraform, install

[Terraform](/en-us/azure/developer/terraform/overview)version 2.99.0 or later.

Use the Azure portal or Azure CLI to verify Microsoft Entra integration with Kubernetes RBAC is enabled.

To verify using the Azure portal:

- Sign-in to the
[Azure portal](https://portal.azure.com)and navigate to your AKS cluster resource. - In the service menu, under
**Settings**, select**Security configuration**. - Under the
**Authentication and Authorization**section, verify the**Microsoft Entra authentication with Kubernetes RBAC**option is selected.

## Create groups in Microsoft Entra ID

This section teaches you how to create two user roles to show how Kubernetes RBAC and Microsoft Entra ID control access cluster resources. The following two example roles are:

**Application developer**- A user named
*aksdev*that's part of the*appdev*group.

- A user named
**Site reliability engineer**(SRE)- A user named
*akssre*that's part of the*opssre*group.

- A user named

In production environments, you can use existing users and groups within a Microsoft Entra tenant.

First, get the resource ID of your AKS cluster using the

command. Then, assign the resource ID to a variable named`az aks show`

*AKS_ID*so it can be referenced in other commands.`AKS_ID=$(az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query id -o tsv)`

Create the first example group in Microsoft Entra ID for the application developers using the

command. The following example creates a group named`az ad group create`

*appdev*:`APPDEV_ID=$(az ad group create --display-name appdev --mail-nickname appdev --query id -o tsv)`

Create an Azure role assignment for the

*appdev*group using thecommand. This assignment lets any member of the group use`az role assignment create`

`kubectl`

to interact with an AKS cluster by granting them the*Azure Kubernetes Service Cluster User*Role.`az role assignment create \ --assignee $APPDEV_ID \ --role "Azure Kubernetes Service Cluster User Role" \ --scope $AKS_ID`

Tip

If you receive an error such as

`Principal 35bfec9328bd4d8d9b54dea6dac57b82 doesn't exist in the directory a5443dcd-cd0e-494d-a387-3039b419f0d5.`

, wait a few seconds for the Microsoft Entra group object ID to propagate through the directory then try the`az role assignment create`

command again.

## Create users in Microsoft Entra ID

After you create the example Microsoft Entra ID groups for application developers and SREs, the next step is to create two corresponding user accounts. These users are used to sign in to the AKS cluster and validate the Kubernetes RBAC integration described later in this article.

Before you begin, you must set the user principal name (UPN) and password for the application developers. The UPN must include the verified domain name of your tenant. For example, an application developer user, `aksdev@contoso.com`

. In order to figure out (or set) the verified domain names in your tenant, see [Managing custom domain names in your Microsoft Entra ID](/en-us/entra/identity/users/domains-manage).

The following command prompts you for the UPN and sets it to *AAD_DEV_UPN* so it can be used in a later command:

```
echo "Please enter the UPN for application developers: " && read AAD_DEV_UPN
```


The following command prompts you for the password and sets it to *AAD_DEV_PW* for use in a later command:

```
echo "Please enter the secure password for application developers: " && read AAD_DEV_PW
```


### Create user accounts

Create the first user account in Microsoft Entra ID using the

command. The following example creates a user with the display name`az ad user create`

*AKS Dev*, the UPN, and secure password using the values in*AAD_DEV_UPN*and*AAD_DEV_PW*:`AKSDEV_ID=$(az ad user create \ --display-name "AKS Dev" \ --user-principal-name $AAD_DEV_UPN \ --password $AAD_DEV_PW \ --query id -o tsv)`

Add the user to the

*appdev*group created in the previous section using thecommand:`az ad group member add`

`az ad group member add --group appdev --member-id $AKSDEV_ID`


## Create AKS cluster resources

We have our Microsoft Entra groups, users, and Azure role assignments created. Now, you configure the AKS cluster to allow these different groups access to specific resources.

Get the cluster admin credentials using the

command. In one of the following sections, you get the regular`az aks get-credentials`

*user*cluster credentials to see the Microsoft Entra authentication flow in action.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --admin`

Create a namespace in the AKS cluster using the

command. The following example creates a namespace name`kubectl create namespace`

*dev*:`kubectl create namespace dev`

Note

In Kubernetes,

*Roles*define the permissions to grant, and*RoleBindings*apply them to desired users or groups. These assignments can be applied to a given namespace, or across the entire cluster. For more information, see[Using Kubernetes RBAC authorization](concepts-identity#kubernetes-rbac).If the user you grant the Kubernetes RBAC binding for is in the same Microsoft Entra tenant, assign permissions based on the

**UPN**. If the user is in a different Microsoft Entra tenant, query for and use the*objectId*property instead.Create a Role for the

*dev*namespace, which grants full permissions to the namespace. In production environments, you can specify more granular permissions for different users or groups. Create a file named`role-dev-namespace.yaml`

and paste the following YAML manifest:`kind: Role apiVersion: rbac.authorization.k8s.io/v1 metadata: name: dev-user-full-access namespace: dev rules: - apiGroups: ["", "extensions", "apps"] resources: ["*"] verbs: ["*"] - apiGroups: ["batch"] resources: - jobs - cronjobs verbs: ["*"]`

Create the Role using the

command and specify the filename of your YAML manifest.`kubectl apply`

`kubectl apply -f role-dev-namespace.yaml`

Get the resource ID for the

*appdev*group using thecommand. This group is set as the subject of a RoleBinding in the next step.`az ad group show`

`az ad group show --group appdev --query id -o tsv`

Create a RoleBinding for the

*appdev*group to use the previously created Role for namespace access. Create a file named`rolebinding-dev-namespace.yaml`

and paste the following YAML manifest. On the last line, replace*groupObjectId*with the group object ID output from the previous command.`kind: RoleBinding apiVersion: rbac.authorization.k8s.io/v1 metadata: name: dev-user-access namespace: dev roleRef: apiGroup: rbac.authorization.k8s.io kind: Role name: dev-user-full-access subjects: - kind: Group namespace: dev name: groupObjectId`

Tip

If you want to create the RoleBinding for a single user, specify

*kind: User*and replace*groupObjectId*with the UPN in the previous sample.Create the RoleBinding using the

command and specify the filename of your YAML manifest:`kubectl apply`

`kubectl apply -f rolebinding-dev-namespace.yaml`


## Access AKS cluster resources with Microsoft Entra identities

Now, test that the expected permissions work when you create and manage resources in an AKS cluster. In these examples, you schedule and view pods in the user's assigned namespace, and try to schedule and view pods outside of the assigned namespace.

Reset the

*kubeconfig*context using thecommand. In a previous section, you set the context using the cluster admin credentials. The admin user bypasses Microsoft Entra sign-in prompts. Without the`az aks get-credentials`

`--admin`

parameter, the user context is applied that requires all requests to be authenticated using Microsoft Entra ID.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --overwrite-existing`

Schedule a basic NGINX pod using the

command in the`kubectl run`

*dev*namespace:`kubectl run nginx-dev --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev`

Enter the credentials for the

*appdev*group account (enter*your*own credentials) at the sign-in prompt. Once you're successfully signed in, the account token is cached for future`kubectl`

commands. The NGINX is successfully scheduled as shown in the following example output:`$ kubectl run nginx-dev --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code B24ZD6FP8 to authenticate. pod/nginx-dev created`

Use the

command to view pods in the`kubectl get pods`

*dev*namespace:`kubectl get pods --namespace dev`

Ensure the status of the NGINX pod is

*Running*. The output looks like the following output:`$ kubectl get pods --namespace dev NAME READY STATUS RESTARTS AGE nginx-dev 1/1 Running 0 4m`


### Test SRE access to AKS cluster resources

To confirm that our Microsoft Entra group membership and Kubernetes RBAC work correctly between different users and groups, try the previous commands when signed in as the *akssre* user.

Reset the

*kubeconfig*context using thecommand that clears the previously cached authentication token for the`az aks get-credentials`

*aksdev*user.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --overwrite-existing`

Schedule and view pods in the assigned

*SRE*namespace. When prompted, sign in with the*opssre*group account credentials (enter*your*own credentials).`kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace sre kubectl get pods --namespace sre`

As shown in the following example output, you can successfully create and view the pods:

`$ kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace sre`

To sign in, use a web browser to open the page

[https://microsoft.com/devicelogin](https://microsoft.com/devicelogin)and enter the code BM4RHP3FD to authenticate.`pod/nginx-sre created $ kubectl get pods --namespace sre NAME READY STATUS RESTARTS AGE nginx-sre 1/1 Running 0`

Try to view or schedule pods outside of assigned SRE namespace.

`kubectl get pods --all-namespaces kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev`

These

`kubectl`

commands fail, as shown in the following example output. The user's group membership and Kubernetes Role and RoleBindings don't grant permissions to create or manager resources in other namespaces.`$ kubectl get pods --all-namespaces Error from server (Forbidden): pods is forbidden: User "akssre@contoso.com" cannot list pods at the cluster scope $ kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev Error from server (Forbidden): pods is forbidden: User "akssre@contoso.com" cannot create pods in the namespace "dev"`


### Create and view cluster resources outside of the assigned namespace

To view pods outside of the *dev* namespace. Use the [ kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command using

`--all-namespaces`

:```
kubectl get pods --all-namespaces
```


The user's group membership doesn't have a Kubernetes Role that allows this action, as shown in the following example output:

```
Error from server (Forbidden): pods is forbidden: User "aksdev@contoso.com" cannot list resource "pods" in API group "" at the cluster scope
```


In the same way, schedule a pod in a different namespace, such as the *SRE* namespace. The user's group membership doesn't align with a Kubernetes Role and RoleBinding to grant these permissions, as shown in the following example output:

```
$ kubectl run nginx-dev --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace sre
Error from server (Forbidden): pods is forbidden: User "akssre@contoso.com" cannot create resource "pods" in API group "" in the namespace "sre"
```


### Clean up cluster resources

To clean up all of the resources, run the following commands:

```
# Get the admin kubeconfig context to delete the necessary cluster resources.
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --admin
# Delete the dev and SRE namespaces. This also deletes the pods, Roles, and RoleBindings.
kubectl delete namespace dev
kubectl delete namespace sre
# Delete the Azure AD user accounts for aksdev and akssre.
az ad user delete --upn-or-object-id $AKSDEV_ID
az ad user delete --upn-or-object-id $AKSSRE_ID
# Delete the Azure AD groups for appdev and opssre. This also deletes the Azure role assignments.
az ad group delete --group appdev
az ad group delete --group opssre
```


## Next steps

For more information about how to secure Kubernetes clusters, see

[Access and identity options for AKS](concepts-identity#kubernetes-rbac).For best practices on identity and resource control, see

[Best practices for authentication and authorization in AKS](operator-best-practices-identity).


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
