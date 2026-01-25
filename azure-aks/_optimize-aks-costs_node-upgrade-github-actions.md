---
merged_at: 2026-01-25T12:06:27.793191
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: optimize-aks-costs.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/optimize-aks-costs -->

# Optimize Azure Kubernetes Service (AKS) usage and costs

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides guidance on how to optimize your Azure Kubernetes Service (AKS) usage and costs. It covers guidance on the following topics:

## Automatic scaling

### Horizontal pod autoscaling

The * Horizontal Pod Autoscaler (HPA)* monitors resource demand and automatically updates a workload resource to automatically scale the number of pods to match demand. The response to increased load is to deploy more pods. If the load decreases and the number of pods is above the configured minimum, the autoscaler tells the workload resource to scale down.

The Metrics API gets data from the kubelet every 60 seconds, and the HPA checks the Metrics API every 15 seconds for any needed changes by default. This means that the HPA updates every 60 seconds. When you configure the HPA for a deployment, you define the minimum and maximum number of replicas that can run and the metrics that the HPA uses to determine when to scale.

For more information, see [Horizontal Pod Autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) and [Autoscale pods in AKS](tutorial-kubernetes-scale#autoscale-pods).

### Kubernetes event-driven autoscaling

The [Kubernetes Event-driven Autoscaler (KEDA)](https://keda.sh/) applies event-driven autoscaling to your workloads. KEDA works with the HPA and can extend functionality without overwriting or duplication.

You can use the KEDA add-on for AKS to scale your applications and leverage a [rich catalog of Azure KEDA scalers](https://keda.sh/docs/2.16/scalers/). For more information, see [Application autoscaling with the KEDA add-on](keda-about) and [Install the KEDA add-on for AKS](keda-deploy-add-on-cli).

### Vertical pod autoscaling

The * Vertical Pod Autoscaler (VPA)* automatically sets resource requests and limits on containers per workload based on past usage. The VPA frees up CPU and Memory for pods to ensure effective utilization of your AKS clusters. Over time, the VPA provides recommendations for resource usage.

For more information, see [Vertical pod autoscaling in Azure Kubernetes Service (AKS)](vertical-pod-autoscaler) and [Use the Vertical Pod Autoscaler (VPA) in Azure Kubernetes Service (AKS)](use-vertical-pod-autoscaler).

## Cluster right-sizing

### Right-size your cluster

It's important to * right-size your clusters* to optimize costs and performance. You can manually resize a cluster by adding or removing the nodes to meet the needs of your applications. You can also autoscale your cluster to automatically adjust the number of nodes in response to changing demands.

For more information, see [Resize Azure Kubernetes Service (AKS) clusters](resize-cluster).

### Cluster autoscaling

With the * cluster autoscaler*, you can automatically scale node pools based on resource usage and constraints, such as scaling up to schedule pending pods or scaling down to reduce costs for unused nodes. The

[cluster autoscaler profile](cluster-autoscaler-overview#cluster-autoscaler-profile)is a set of parameters that you can fine-tune to control the behavior of the cluster autoscaler.

For more information, see [Cluster autoscaling in Azure Kubernetes Service (AKS) overview](cluster-autoscaler-overview) and [Use the cluster autoscaler in Azure Kubernetes Service (AKS)](cluster-autoscaler).

### Node autoprovisioning (preview)

* Node autoprovisioning (NAP)* (preview), based on the open-source

[Karpenter](https://karpenter.sh/)project, helps you provision the right infrastructure based on the pending pod resource requirements of your workloads. With efficient bin-packing, you can consolidate your workloads onto the right-sized infrastructure to reduce operating costs.

For more information, see [Node autoprovisioning (preview) in Azure Kubernetes Service (AKS)](node-autoprovision).

## GPU optimizations

### GPU partitioning and sharing

GPU partitioning helps combat underutilization by splitting up or sharing GPUs across multiple workloads. The following sections cover different ways to partition and share GPUs in AKS.

#### Time-slicing

The [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/overview.html) enables the * time-slicing* of GPUs in Kubernetes clusters. With time-slicing, a system administrator can define a set of

*replicas*for a GPU, each of which can be handed out independently to a pod to run workloads on. You can apply cluster-wide default time-slicing configurations and node-specific configurations.


For more information, see [Time-slicing GPUs in Kubernetes](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/gpu-sharing.html).

#### Multi-processing service (MPS)

A single process might not utilize all the memory and compute bandwidth capacity available on a GPU. The * Multi-Process Service (MPS)* enables logical partitioning of memory and compute resources between workloads and allows kernel and memcopy operations from different processes to overlap on the GPU. MPS helps you achieve higher GPU utilization and shorter running times.


For more information, see [Multi-Process Service (MPS)](https://docs.nvidia.com/deploy/mps/index.html#mps).

#### Multi-instance GPUs (MIGs)

* Multi-instance GPUs (MIGs)* enable you to partition GPUs based on the NVIDIA Ampere and later architectures into separate and secure GPU instances for CUDA applications.


For more information, see [GPU Operator with MIG](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/gpu-operator-mig.html) and [Create a multi-instance GPU node pool in Azure Kubernetes Service (AKS)](gpu-multi-instance).

## Multitenancy

Multitenancy refers to the sharing of infrastructure across tenants, teams, and business units. The following table outlines different ways to implement multitenancy in AKS:

| Multitenancy type | Multitenancy level | Cluster pod density | Cost allocation | Ideal use case | Potential risks |
|---|---|---|---|---|---|
Dedicated cluster |

• Lower pod density and more overprovisioned resources

**Dedicated node pool**• Requires extra cluster configurations, like network policies, quota management, role-based access control (RBAC), etc.

**Dedicated namespace**• Requires extra cluster configurations, like network policies, quota management, role-based access control (RBAC), etc.

### Dedicated cluster

With * dedicated cluster multitenancy*, clusters are dedicated to a single workload or team.


The following table outlines pros and cons of using a dedicated cluster:

| Pros | Cons |
|---|---|
| • Easier isolation method • Straightforward cost allocation and chargeback • Great for cases where tenants don't trust each other (often from security and resource sharing perspectives) |
• High management and financial overhead • Generally low pod density and overprovisioned resources |

### Dedicated node pool

With * dedicated node pool multitenancy*, clusters are shared by many tenants.


The following table outlines pros and cons of using a dedicated node pool:

| Pros | Cons |
|---|---|
| • Medium pod density • Some shared infrastructure • Apply Azure tags to node pools dedicated to a single tenant (tags propagate to nodes and persist through upgrades) |
• Requires trust between the tenants • Requires extra cluster configurations, like network policies, quota management, role-based access control (RBAC), etc. |

### Dedicated namespace

With * dedicated namespace multitenancy*, clusters are shared by many tenants, with namespaces serving as the isolation boundary.


The following table outlines pros and cons of using a dedicated namespace:

| Pros | Cons |
|---|---|
| • Higher pod density • Best binpacking • Sharing infrastructure to maximize resource utilization |
• Unsafe for hostile environments by default • Requires extra security measures in place if all tenants can't be trusted |

## Azure discounts

To take savings one step further, take advantage of Azure discounts such as Azure Savings Plans, Reserved Instances, and Azure Hybrid Benefits.

| Azure discount type | Details |
|---|---|
Azure Savings Plans |

• Save up to 65% compared to pay-as-you-go

• Flexible, with no SKU family or region restrictions

• Best for workloads with consistent costs with resources in various SKUs and regions

**Reserved Instances**• Save up to 72% compared to pay-as-you-go

• Restricted to specific SKU families and regions

• Best for stable workloads running continuously (with no unexpected SKU or region changes)

**Azure Hybrid Benefits**• Use any qualifying on-premises licenses that have an active Software Assurance (SA) or qualifying subscription

## Next steps

To learn more about cost in AKS, see the following articles:


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
