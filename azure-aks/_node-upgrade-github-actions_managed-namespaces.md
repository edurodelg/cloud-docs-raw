---
merged_at: 2026-01-25T12:25:33.931355
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: node-upgrade-github-actions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-upgrade-github-actions -->

# Apply automatic security upgrades to Azure Kubernetes Service (AKS) nodes using GitHub Actions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Security updates are a key part of maintaining your AKS cluster's security and compliance with the latest fixes for the underlying OS. These updates include OS security fixes or kernel updates. Some updates require a node reboot to complete the process.

This article shows you how you can automate the update process of AKS nodes using GitHub Actions and Azure CLI to create an update task based on `cron`

that runs automatically.

Note

You can also perform node image upgrades automatically and schedule these upgrades using planned maintenance. For more information, see [Automatically upgrade node images](auto-upgrade-node-image).

## Before you begin

- This article assumes you have an existing AKS cluster. If you need an AKS cluster, create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[the Azure portal](learn/quick-kubernetes-deploy-portal). - This article also assumes you have a
[GitHub account](https://github.com)and a[profile repository](https://docs.github.com/en/free-pro-team@latest/github/setting-up-and-managing-your-github-profile/about-your-profile)to host your actions. If you don't have a repository, create one with the same name as your GitHub username. - You need the Azure CLI version 2.0.59 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Update nodes with `az aks upgrade`


The `az aks upgrade`

command gives you a zero downtime way to apply updates. The command performs the following actions:

- Applies the latest updates to all your cluster's nodes.
- Cordons (makes the node unavailable for the scheduling of new workloads) and drains (moves the existent workloads to other node) traffic to the nodes.
- Restarts the nodes.
- Enables the updated nodes to receive traffic again.

AKS doesn't automatically restart your nodes if you update them using a different method.

Note

Running `az aks upgrade`

with the `--node-image-only`

flag only upgrades the node images. Running the command without the flag upgrades both the node images and the Kubernetes control plane version. For more information, see the [docs for managed upgrades on nodes](node-image-upgrade) and the [docs for cluster upgrades](upgrade-cluster).

All Kubernetes nodes run in a standard Windows or Linux-based Azure virtual machine (VM). The Linux-based VMs use an Ubuntu image with the OS configured to automatically check for updates every night.

When you use the `az aks upgrade`

command, Azure CLI creates a surge of new nodes with the latest security and kernel updates. These new nodes are initially cordoned to prevent any apps from being scheduled to them until the update completes. After the update completes, Azure cordons and drains the older nodes and uncordons the new ones, transferring all the scheduled applications to the new nodes.

This process is better than updating Linux-based kernels manually because Linux requires a reboot when a new kernel update is installed. If you update the OS manually, you also need to reboot the VM, manually cordoning and draining all the apps.

## Create a timed GitHub Action

`cron`

is a utility that allows you to run a set of commands, or *jobs*, on an automated schedule. To create a job to update your AKS nodes on an automated schedule, you need a repository to host your actions. GitHub Actions are usually configured in the same repository as your application, but you can use any repository.

Navigate to your repository on GitHub.

Select

**Actions**.Select

**New workflow**>**Set up a workflow yourself**.Create a GitHub Action named

*Upgrade cluster node images*with a schedule trigger to run every 15 days at 3am. Copy the following code into the YAML:`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *'`

Create a job named

*upgrade-node*that runs on an Ubuntu agent and connects to your Azure CLI account to execute the node upgrade command. Copy the following code into the YAML under the`on`

key:`jobs: upgrade-node: runs-on: ubuntu-latest`


## Set up the Azure CLI in the workflow

In the

**Search Marketplace for Actions**bar, search for**Azure Login**.Select

**Azure Login**.Under

**Installation**, select a version, such as*v1.4.6*, and copy the installation code snippet.Add the

`steps`

key and the following information from the installation code snippet to the YAML:`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *' jobs: upgrade-node: runs-on: ubuntu-latest steps: - name: Azure Login uses: Azure/login@v1.4.6 with: creds: ${{ secrets.AZURE_CREDENTIALS }}`


## Create credentials for the Azure CLI

In a new browser window, create a new service principal using the

command. Make sure you replace`az ad sp create-for-rbac`

`*{subscriptionID}*`

with your own subscription ID.Note

This example creates the

`Contributor`

role at the*Subscription*scope. You can provide the role and scope that meets your needs. For more information, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles)and[Azure RBAC scope levels](/en-us/azure/role-based-access-control/scope-overview#scope-format).`az ad sp create-for-rbac --role Contributor --scopes /subscriptions/{subscriptionID} -o json`

Your output should be similar to the following example output:

`{ "appId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "displayName": "xxxxx-xxx-xxxx-xx-xx-xx-xx-xx", "password": "xxxxxxxxxxxxxxxxxxxxxxxxxxxx", "tenant": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" }`

Copy the output and navigate to your GitHub repository.

Select

**Settings**>**Secrets and variables**>**Actions**>**New repository secret**.For

**Name**, enter`AZURE_CREDENTIALS`

.For

**Secret**, copy in the contents of the output you received when you created the service principal.Select

**Add Secret**.

## Create the steps to execute the Azure CLI commands

Navigate to your window with the workflow YAML.

In the

**Search Marketplace for Actions**bar, search for**Azure CLI Action**.Select

**Azure CLI Action**.Under

**Installation**, select a version, such as*v1.0.8*, and copy the installation code snippet.Paste the contents of the action into the YAML below the

`*Azure Login*`

step, similar to the following example:`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *' jobs: upgrade-node: runs-on: ubuntu-latest steps: - name: Azure Login uses: Azure/login@v1.4.6 with: creds: ${{ secrets.AZURE_CREDENTIALS }} - name: Upgrade node images uses: Azure/cli@v1.0.8 with: inlineScript: az aks upgrade --resource-group <resourceGroupName> --name <aksClusterName> --node-image-only --yes`

Tip

You can decouple the

`--resource-group`

and`--name`

parameters from the command by creating new repository secrets like you did for`AZURE_CREDENTIALS`

.If you create secrets for these parameters, you need to replace the

`<resourceGroupName>`

and`<aksClusterName>`

placeholders with their secret counterparts. For example,`${{secrets.RESOURCE_GROUP_NAME}}`

and`${{secrets.AKS_CLUSTER_NAME}}`

Rename the YAML to

`upgrade-node-images.yml`

.Select

**Commit changes...**, add a commit message, and then select**Commit changes**.

## Run the GitHub Action manually

You can run the workflow manually in addition to the scheduled run by adding a new `on`

trigger called `workflow_dispatch`

.

Note

If you want to upgrade a single node pool instead of all node pools on the cluster, add the `--name`

parameter to the `az aks nodepool upgrade`

command to specify the node pool name. For example:

```
az aks nodepool upgrade --resource-group <resourceGroupName> --cluster-name <aksClusterName> --name <nodePoolName> --node-image-only
```


Add the

`workflow_dispatch`

trigger under the`on`

key:`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *' workflow_dispatch:`

The YAML should look similar to the following example:

`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *' workflow_dispatch: jobs: upgrade-node: runs-on: ubuntu-latest steps: - name: Azure Login uses: Azure/login@v1.4.6 with: creds: ${{ secrets.AZURE_CREDENTIALS }} - name: Upgrade node images uses: Azure/cli@v1.0.8 with: inlineScript: az aks upgrade -g {resourceGroupName} -n {aksClusterName} --node-image-only --yes # Code for upgrading one or more node pools`


## Next steps

For more information about AKS upgrades, see the following articles and resources:

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).


---

<!-- DOCUMENTO FUSIONADO: managed-namespaces.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/managed-namespaces -->

# Use managed namespaces in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic ✔️ AKS Standard

Managed namespaces in Azure Kubernetes Service (AKS) provide a way to logically isolate workloads and teams within a cluster. This feature enables administrators to enforce resource quotas, apply network policies, and manage access control at the namespace level. For a detailed overview of managed namespaces, see the [managed namespaces overview](concepts-managed-namespaces).

## Before you begin

### Prerequisites

- An Azure account with an active subscription. If you don't have one, you can
[create an account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F). - An
[AKS cluster](automatic/quick-automatic-managed-network)set up in your Azure environment with[Azure role-based access control for Kubernetes authorization](manage-azure-rbac)is required if you intend to utilize Azure RBAC roles. - To use the network policy feature, the AKS cluster needs to be
[configured with a network policy engine](use-network-policies#network-policy-options-in-aks). Cilium is our recommended engine.

| Prerequisite | Notes |
|---|---|
Azure CLI |
`2.80.0` or later installed. To find the CLI version, run `az --version` . If you need to install or upgrade, see
|
AKS API Version |
`2025-09-01` or later. |
Required permission(s) |
`Microsoft.ContainerService/managedClusters/managedNamespaces/*` or `Azure Kubernetes Service Namespace Contributor` built-in role. `Microsoft.Resources/deployments/*` on the resource group containing the cluster. For more information, see
|

### Limitations

- Trying to on-board system namespaces such as
`kube-system`

,`app-routing-system`

,`istio-system`

,`gatekeeper-system`

, etc. to be managed namespaces isn't allowed. - When a namespace is a managed namespace, changes to the namespace via the Kubernetes API are blocked.

- Listing existing namespaces to convert in the portal doesn't work with private clusters. You can add new namespaces.

## Create a managed namespace on a cluster and assign users

Note

When you create a managed namespace, a component is installed on the cluster to reconcile the namespace with the state in Azure Resource Manager. This component blocks changes to the managed fields and resources from the Kubernetes API, ensuring consistency with the desired configuration.

The following Bicep example demonstrates how to create a managed namespace as a subresource of a managed cluster. Make sure to select the appropriate value for `defaultNetworkPolicy`

, `adoptionPolicy`

, and `deletePolicy`

. For more information about what those parameters mean, see the [managed namespaces overview](concepts-managed-namespaces).

```
resource existingCluster 'Microsoft.ContainerService/managedClusters@2024-03-01' existing = {
name: 'contoso-cluster'
}
resource managedNamespace 'Microsoft.ContainerService/managedClusters/managedNamespaces@2025-09-01' = {
parent: existingCluster
name: 'retail-team'
location: location
properties: {
defaultResourceQuota: {
cpuRequest: '1000m'
cpuLimit: '2000m'
memoryRequest: '512Mi'
memoryLimit: '1Gi'
}
defaultNetworkPolicy: {
ingress: 'AllowSameNamespace'
egress: 'AllowAll'
}
adoptionPolicy: 'IfIdentical'
deletePolicy: 'Keep'
labels: {
environment: 'dev'
}
annotations: {
owner: 'retail'
}
}
}
```


Save the Bicep file **managedNamespace.bicep** to your local computer.

Deploy the Bicep file using the Azure CLI.

```
az deployment group create --resource-group <resource-group> --template-file managedNamespace.bicep
```


### Define variables

Define the following variables to be used in the subsequent steps.

```
RG_NAME=cluster-rg
CLUSTER_NAME=contoso-cluster
NAMESPACE_NAME=retail-team
LABELS="environment=dev"
ANNOTATIONS="owner=retail"
```


### Create the managed namespace

To customize its configuration, managed namespaces have various parameter options to choose from during creation. Make sure to select the appropriate value for `ingress-network-policy`

, `egress-network-policy`

, `adoption-policy`

, and `delete-policy`

. For more information about what those parameters mean, see the [managed namespaces overview](concepts-managed-namespaces).

```
az aks namespace add \
--name ${NAMESPACE_NAME} \
--cluster-name ${CLUSTER_NAME} \
--resource-group ${RG_NAME} \
--cpu-request 1000m \
--cpu-limit 2000m \
--memory-request 512Mi \
--memory-limit 1Gi \
--ingress-policy [AllowSameNamespace|AllowAll|DenyAll] \
--egress-policy [AllowSameNamespace|AllowAll|DenyAll] \
--adoption-policy [Never|IfIdentical|Always] \
--delete-policy [Keep|Delete] \
--labels ${LABELS} \
--annotations ${ANNOTATIONS}
```


### Assign role

After the namespace is created, you can assign [one of the built-in roles](concepts-managed-namespaces#managed-namespaces-built-in-roles) for the control plane and data plane.

```
ASSIGNEE="user@contoso.com"
NAMESPACE_ID=$(az aks namespace show --name ${NAMESPACE_NAME} --cluster-name ${CLUSTER_NAME} --resource-group ${RG_NAME} --query id -o tsv)
```


Assign a control plane role to be able to view the managed namespace in the portal, Azure CLI output, and Azure Resource Manager. This role also allows the user to retrieve the credentials to connect to this namespace.

```
az role assignment create \
--assignee ${ASSIGNEE} \
--role "Azure Kubernetes Service Namespace User" \
--scope ${NAMESPACE_ID}
```


Assign data plane role to be able to get access to create resources within the namespace using the Kubernetes API.

```
az role assignment create \
--assignee ${ASSIGNEE} \
--role "Azure Kubernetes Service RBAC Writer" \
--scope ${NAMESPACE_ID}
```


- Sign in to the
[Azure portal](https://portal.azure.com). - On the Azure portal home page, select
**Create a resource**. - In the
**Categories**section, select**Managed Kubernetes Namespaces**. - On the
**Basics**tab, under**Project details**configure the following settings:- Select the target
**cluster**to create the namespace on. - If you're creating a new namespace, leave the default
**create new**, otherwise choose**change existing to managed**to convert an existing namespace.

- Select the target
- Configure the
**networking policy**to be applied on the namespace. - Configure the
**resource requests and limits**for the namespace. - Select the
**members (users or groups)**and their**role**.- Assign the
**Azure Kubernetes Service Namespace User**role to give them access to view the managed namespace in the portal, Azure CLI output, and Azure Resource Manager. This role also allows the user to retrieve the credentials to connect to this namespace. - Assign the
**Azure Kubernetes Service RBAC Writer**role to give them access to create resources within the namespace using the Kubernetes API.

- Assign the
- Select
**Review + create**to run validation on the configuration. After validation completes, select**Create**.

## List managed namespaces

You can list managed namespaces at different scopes using the Azure CLI.

### Subscription level

Run the following command to list all managed namespaces in a subscription.

```
az aks namespace list --subscription <subscription-id>
```


### Resource group level

Run the following command to list all managed namespaces in a specific resource group.

```
az aks namespace list --resource-group <rg-name>
```


### Cluster level

Run the following command to list all managed namespaces in a specific cluster.

```
az aks namespace list --resource-group <rg-name> --cluster-name <cluster-name>
```


## List managed namespaces

You can list managed namespaces at different scopes using the Azure CLI.

### Subscription level

Run the following command to list all managed namespaces in a subscription.

```
az aks namespace list --subscription <subscription-id>
```


### Resource group level

Run the following command to list all managed namespaces in a specific resource group.

```
az aks namespace list --resource-group <rg-name>
```


### Cluster level

Run the following command to list all managed namespaces in a specific cluster.

```
az aks namespace list --resource-group <rg-name> --cluster-name <cluster-name>
```


## Connect to the cluster

You can retrieve the credentials to connect to a namespace via the following command.

```
az aks namespace get-credentials --name <namespace-name> --resource-group <rg-name> --cluster-name <cluster-name>
```


## Connect to the cluster

You can retrieve the credentials to connect to a namespace via the following command.

```
az aks namespace get-credentials --name <namespace-name> --resource-group <rg-name> --cluster-name <cluster-name>
```


## Next steps

This article focused on using the managed namespaces feature to logically isolate teams and applications. You can further explore other guardrails and best practices to apply via [deployment safeguards](deployment-safeguards).
