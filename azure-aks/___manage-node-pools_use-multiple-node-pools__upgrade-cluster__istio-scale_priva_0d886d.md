---
merged_at: 2026-01-26T20:54:26.140694
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/manage-node-pools -->

# Create node pools for a cluster in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to create one or more node pools in an AKS cluster.

Note

This feature enables more control over creating and managing multiple node pools and requires separate commands for *create/update/delete* (CRUD) operations. Previously, cluster operations through [ az aks create](/en-us/cli/azure/aks#az-aks-create) or

[used the managedCluster API and were the only options to change your control plane and a single node pool. This feature exposes a separate operation set for agent pools through the agentPool API and requires use of the](/en-us/cli/azure/aks#az-aks-update)

`az aks update`

[command set to execute operations on an individual node pool.](/en-us/cli/azure/aks/nodepool)

`az aks nodepool`

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

- You need Azure CLI version 2.2.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

To deploy an ARM template, you need write access on the resources you're deploying and access to all operations on the

`Microsoft.Resources/deployments`

resource type. For example, to deploy a virtual machine (VM), you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).Review the following requirements for each parameter:

`osTYPE`

: The operating system type. The default is Linux.`osSKU`

: Specifies the OS SKU used by the agent pool.`count`

: Number of agents (VMs) to host docker containers. Allowed values must be in the range of 0 to 1000 (inclusive) for user pools and in the range of 1 to 1000 (inclusive) for system pools. The default value is 1.

After you deploy the cluster using an ARM template, you can use Azure CLI or Azure PowerShell to connect to the cluster and deploy the sample application.


## Limitations

The following limitations apply when you create AKS clusters that support multiple node pools:

You can delete the system node pool if you have another system node pool to take its place in the AKS cluster. Otherwise, you can't delete the system node pool.

System pools must contain at least one node. User node pools can contain zero or more nodes.

**If you create a cluster with a single node pool, the OS type must be**. The OS SKU can be any Linux variation such as`Linux`

`Ubuntu`

or`AzureLinux`

. You can't create a cluster with a single Windows node pool. If you want to run Windows containers, you must[add a Windows node pool](#add-a-windows-server-node-pool)to the cluster after creating it with a Linux system node pool.The AKS cluster must use the Standard SKU load balancer to use multiple node pools. This feature isn't supported with Basic SKU load balancers.

The AKS cluster must use Virtual Machine Scale Sets for the nodes.

The name of a node pool can only contain lowercase alphanumeric characters and must begin with a lowercase letter.

- For Linux node pools, the length must be between 1-12 characters.
- For Windows node pools, the length must be between 1-6 characters.

All node pools must reside in the same virtual network.

You can't change the virtual machine (VM) size of a node pool after you create it.

When you create multiple node pools at cluster creation time, the Kubernetes versions for the node pools must match the version set for the control plane. You can make updates after provisioning the cluster using per node pool operations.


## Create specialized node pools

To learn how to create specialized node pools, see the following articles:

[Add an Azure Spot node pool to an AKS cluster](spot-node-pool)[Add a Virtual Machines node pool to an AKS cluster](virtual-machines-node-pools)[Add a dedicated system node pool to an AKS cluster](use-system-pools#add-a-dedicated-system-node-pool-to-an-existing-aks-cluster)[Enabled Federal Information Processing Standards (FIPS) on an AKS node pool](enable-fips-nodes)[Add a node pool with a Confidential Virtual Machine (CVM) on an AKS cluster](use-cvm)[Create node pools with unique subnets in AKS](node-pool-unique-subnet)[Add a generation 2 VM node pool to an AKS cluster](generation-2-vms)[Add a node pool with Artifact Streaming to an AKS cluster](artifact-streaming)[Add Windows Server node pools with](windows-containerd)`containerd`

to an AKS cluster

## Set environment variables

Set the following environment variables in your shell to simplify the commands in this article. You can change the values to your preferred names.

`export RESOURCE_GROUP_NAME="my-aks-rg" export LOCATION="eastus" export CLUSTER_NAME="my-aks-cluster" export NODE_POOL_NAME="mynodepool"`


## Create a resource group

Create an Azure resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP_NAME --location $LOCATION`


## Create an AKS cluster with a single node pool using the Azure CLI

If you want only one node pool in your AKS cluster, you can schedule application pods on system node pools. If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool. If one node goes down, the redundancy is compromised. You can mitigate this risk by having more system node pool nodes.

-
[Create an AKS cluster with a single Ubuntu node pool](#tabpanel_1_ubuntu) -
[Create an AKS cluster with a single Azure Linux node pool](#tabpanel_1_azure-linux) -
[Create an AKS cluster with a single Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_1_os-guard) -
[Create an AKS cluster with a single Flatcar Container Linux for AKS (preview) node pool](#tabpanel_1_flatcar)

Create a cluster with a single Ubuntu node pool using the

command. This step specifies two nodes in the single node pool.`az aks create`

`az aks create \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --vm-set-type VirtualMachineScaleSets \ --node-count 2 \ --os-sku Ubuntu \ --location $LOCATION \ --load-balancer-sku standard \ --generate-ssh-keys`

It takes a few minutes to create the cluster.

When the cluster is ready, get the cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME`


## Add a second node pool using the Azure CLI

The cluster created in the [previous section](#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli) has a single node pool. In this section, we add a second node pool to the cluster. This second node pool can have an OS type of `Linux`

with an OS SKU of `Ubuntu`

or `AzureLinux`

, or an OS type of `Windows`

.

Note

If you want to add a node pool that uses **Ephemeral OS disks** to your AKS cluster, you can set the `--node-osdisk-type`

flag to `Ephemeral`

when running the `az aks nodepool add`

command.

With Ephemeral OS, you can deploy VMs and instance images up to the size of the VM cache. The default node OS disk configuration in AKS uses 128 GB, which means that you need a VM size that has a cache larger than 128 GB. The default `Standard_DS2_v2`

has a cache size of 86 GB, which isn't large enough. The `Standard_DS3_v2`

VM SKU has a cache size of 172 GB, which is large enough. You can also reduce the default size of the OS disk using `--node-osdisk-size`

, but keep in mind the minimum size for AKS images is 30 GB.

If you want to create node pools with **network-attached OS disks**, you can set the `--node-osdisk-type`

flag to `Managed`

when running the `az aks nodepool add`

command.

### Add a Linux node pool

-
[Add an Ubuntu node pool](#tabpanel_2_ubuntu) -
[Add an Azure Linux node pool](#tabpanel_2_azure-linux) -
[Add an Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_2_os-guard) -
[Add a Flatcar Container Linux for AKS (preview) node pool](#tabpanel_2_flatcar)

Create a new node pool using the

command. The following example creates a`az aks nodepool add`

`Linux`

node pool with the`Ubuntu`

OS SKU that runs*three*nodes. If you don't specify an OS SKU, AKS defaults to`Ubuntu`

.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-vm-size Standard_DS2_v2 \ --os-type Linux \ --os-sku Ubuntu \ --node-count 3`

It takes a few minutes to create the node pool.


### Add a Windows Server node pool

##### Install the `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


##### Register the `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


##### Create the Windows Server 2025 node pool

Create a new node pool using the

command. The following example creates a`az aks nodepool add`

`Windows`

node pool with the`Windows2025`

OS SKU that runs*three*nodes.For more information about Windows OS, see

[Windows best practices](windows-best-practices).`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-vm-size Standard_DS2_v2 \ --os-type Windows \ --os-sku Windows2025 \ --node-count 3`


## Check the status of your node pools

Check the status of your node pools using the

command and specify your resource group and cluster name.`az aks nodepool list`

`az aks nodepool list --resource-group $RESOURCE_GROUP_NAME --cluster-name $CLUSTER_NAME`


## Create an AKS cluster with a single node pool using an ARM template

If you want only one node pool in your AKS cluster, you can schedule application pods on system node pools. If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool. If one node goes down, the redundancy is compromised. You can mitigate this risk by having more system node pool nodes.

### Create a `Microsoft.ContainerService/managedClusters`

resource

- Create a
`Microsoft.ContainerService/managedClusters`

resource by adding[this JSON](/en-us/azure/templates/microsoft.containerservice/managedclusters?pivots=deployment-language-arm-template)to your template.

-
[Modify JSON to create a single Ubuntu node pool](#tabpanel_4_ubuntu-arm) -
[Modify JSON to create a single Azure Linux node pool](#tabpanel_4_azure-linux-arm) -
[Modify JSON to create a single Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_4_os-guard-arm) -
[Modify JSON to create a single Flatcar Container Linux for AKS (preview) node pool](#tabpanel_4_flatcar-arm)

Create a single Ubuntu node pool in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "1", "osSKU": "ubuntu", "osType": "linux" } ], }`


## Add a second node pool using an ARM template

The cluster created in the [previous section](#create-an-aks-cluster-with-a-single-node-pool-using-an-arm-template) has a single node pool. In this section, we add a second node pool to the cluster. This second node pool can have an OS type of `Linux`

with an OS SKU of `Ubuntu`

or `AzureLinux`

, or an OS type of `Windows`

.

### Add Linux node pools

-
[Modify JSON to create multiple Ubuntu node pools](#tabpanel_5_ubuntu-arm) -
[Modify JSON to create multiple Azure Linux node pools](#tabpanel_5_azure-linux-arm) -
[Modify JSON to create multiple Azure Linux with OS Guard for AKS (preview) node pools](#tabpanel_5_os-guard-arm) -
[Modify JSON to create multiple Flatcar Container Linux for AKS (preview) node pools](#tabpanel_5_flatcar-arm)

Create multiple Ubuntu node pools in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "3", "osSKU": "ubuntu", "osType": "linux" } ], }`


### Add Windows Server node pools

-
[Modify JSON to create multiple Windows Server 2025 (preview) node pools](#tabpanel_6_ws2025-arm) -
[Modify JSON to create multiple Windows Server 2022 node pools](#tabpanel_6_ws2022-arm)

##### Install the `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


##### Register the `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


##### Create the Windows Server 2025 node pools

Create multiple Windows node pools in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "3", "osSKU": "windows2025", "osType": "windows" } ], }`


## Deploy your ARM template

- Deploy your ARM template by following the guidance in
[Deploy an Azure Kubernetes Service (AKS) cluster using an ARM template](learn/quick-kubernetes-deploy-rm-template).

## Set taints, labels, or tags for a node pool

When creating a node pool, you can add taints, labels, or tags to it. When you add a taint, label, or tag, all nodes within that node pool also get that taint, label, or tag. We recommend applying these properties to an entire node pool instead of individual nodes. This way, you can easily manage the properties of all nodes in the node pool by updating the node pool properties instead of updating each node individually.

For specific instructions on how to set taints, labels, or tags for a node pool, use the following resources:

[Use node taints in an Azure Kubernetes Service (AKS) cluster](use-node-taints)[Use labels in an Azure Kubernetes Service (AKS) cluster](use-labels)[Use Azure tags in Azure Kubernetes Service (AKS)](use-tags)[Provide dedicated nodes using taints and tolerations in Azure Kubernetes Service (AKS)](operator-best-practices-advanced-scheduler#provide-dedicated-nodes-using-taints-and-tolerations)

## Next steps

In this article, you learned how to create an AKS cluster with a single node pool and add additional node pools to your cluster. To learn more about how to manage your node pools, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-multiple-node-pools -->

# Create node pools for a cluster in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to create one or more node pools in an AKS cluster.

Note

This feature enables more control over creating and managing multiple node pools and requires separate commands for *create/update/delete* (CRUD) operations. Previously, cluster operations through [ az aks create](/en-us/cli/azure/aks#az-aks-create) or

[used the managedCluster API and were the only options to change your control plane and a single node pool. This feature exposes a separate operation set for agent pools through the agentPool API and requires use of the](/en-us/cli/azure/aks#az-aks-update)

`az aks update`

[command set to execute operations on an individual node pool.](/en-us/cli/azure/aks/nodepool)

`az aks nodepool`

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

- You need Azure CLI version 2.2.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

To deploy an ARM template, you need write access on the resources you're deploying and access to all operations on the

`Microsoft.Resources/deployments`

resource type. For example, to deploy a virtual machine (VM), you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).Review the following requirements for each parameter:

`osTYPE`

: The operating system type. The default is Linux.`osSKU`

: Specifies the OS SKU used by the agent pool.`count`

: Number of agents (VMs) to host docker containers. Allowed values must be in the range of 0 to 1000 (inclusive) for user pools and in the range of 1 to 1000 (inclusive) for system pools. The default value is 1.

After you deploy the cluster using an ARM template, you can use Azure CLI or Azure PowerShell to connect to the cluster and deploy the sample application.


## Limitations

The following limitations apply when you create AKS clusters that support multiple node pools:

You can delete the system node pool if you have another system node pool to take its place in the AKS cluster. Otherwise, you can't delete the system node pool.

System pools must contain at least one node. User node pools can contain zero or more nodes.

**If you create a cluster with a single node pool, the OS type must be**. The OS SKU can be any Linux variation such as`Linux`

`Ubuntu`

or`AzureLinux`

. You can't create a cluster with a single Windows node pool. If you want to run Windows containers, you must[add a Windows node pool](#add-a-windows-server-node-pool)to the cluster after creating it with a Linux system node pool.The AKS cluster must use the Standard SKU load balancer to use multiple node pools. This feature isn't supported with Basic SKU load balancers.

The AKS cluster must use Virtual Machine Scale Sets for the nodes.

The name of a node pool can only contain lowercase alphanumeric characters and must begin with a lowercase letter.

- For Linux node pools, the length must be between 1-12 characters.
- For Windows node pools, the length must be between 1-6 characters.

All node pools must reside in the same virtual network.

You can't change the virtual machine (VM) size of a node pool after you create it.

When you create multiple node pools at cluster creation time, the Kubernetes versions for the node pools must match the version set for the control plane. You can make updates after provisioning the cluster using per node pool operations.


## Create specialized node pools

To learn how to create specialized node pools, see the following articles:

[Add an Azure Spot node pool to an AKS cluster](spot-node-pool)[Add a Virtual Machines node pool to an AKS cluster](virtual-machines-node-pools)[Add a dedicated system node pool to an AKS cluster](use-system-pools#add-a-dedicated-system-node-pool-to-an-existing-aks-cluster)[Enabled Federal Information Processing Standards (FIPS) on an AKS node pool](enable-fips-nodes)[Add a node pool with a Confidential Virtual Machine (CVM) on an AKS cluster](use-cvm)[Create node pools with unique subnets in AKS](node-pool-unique-subnet)[Add a generation 2 VM node pool to an AKS cluster](generation-2-vms)[Add a node pool with Artifact Streaming to an AKS cluster](artifact-streaming)[Add Windows Server node pools with](windows-containerd)`containerd`

to an AKS cluster

## Set environment variables

Set the following environment variables in your shell to simplify the commands in this article. You can change the values to your preferred names.

`export RESOURCE_GROUP_NAME="my-aks-rg" export LOCATION="eastus" export CLUSTER_NAME="my-aks-cluster" export NODE_POOL_NAME="mynodepool"`


## Create a resource group

Create an Azure resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP_NAME --location $LOCATION`


## Create an AKS cluster with a single node pool using the Azure CLI

If you want only one node pool in your AKS cluster, you can schedule application pods on system node pools. If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool. If one node goes down, the redundancy is compromised. You can mitigate this risk by having more system node pool nodes.

-
[Create an AKS cluster with a single Ubuntu node pool](#tabpanel_1_ubuntu) -
[Create an AKS cluster with a single Azure Linux node pool](#tabpanel_1_azure-linux) -
[Create an AKS cluster with a single Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_1_os-guard) -
[Create an AKS cluster with a single Flatcar Container Linux for AKS (preview) node pool](#tabpanel_1_flatcar)

Create a cluster with a single Ubuntu node pool using the

command. This step specifies two nodes in the single node pool.`az aks create`

`az aks create \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --vm-set-type VirtualMachineScaleSets \ --node-count 2 \ --os-sku Ubuntu \ --location $LOCATION \ --load-balancer-sku standard \ --generate-ssh-keys`

It takes a few minutes to create the cluster.

When the cluster is ready, get the cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME`


## Add a second node pool using the Azure CLI

The cluster created in the [previous section](#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli) has a single node pool. In this section, we add a second node pool to the cluster. This second node pool can have an OS type of `Linux`

with an OS SKU of `Ubuntu`

or `AzureLinux`

, or an OS type of `Windows`

.

Note

If you want to add a node pool that uses **Ephemeral OS disks** to your AKS cluster, you can set the `--node-osdisk-type`

flag to `Ephemeral`

when running the `az aks nodepool add`

command.

With Ephemeral OS, you can deploy VMs and instance images up to the size of the VM cache. The default node OS disk configuration in AKS uses 128 GB, which means that you need a VM size that has a cache larger than 128 GB. The default `Standard_DS2_v2`

has a cache size of 86 GB, which isn't large enough. The `Standard_DS3_v2`

VM SKU has a cache size of 172 GB, which is large enough. You can also reduce the default size of the OS disk using `--node-osdisk-size`

, but keep in mind the minimum size for AKS images is 30 GB.

If you want to create node pools with **network-attached OS disks**, you can set the `--node-osdisk-type`

flag to `Managed`

when running the `az aks nodepool add`

command.

### Add a Linux node pool

-
[Add an Ubuntu node pool](#tabpanel_2_ubuntu) -
[Add an Azure Linux node pool](#tabpanel_2_azure-linux) -
[Add an Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_2_os-guard) -
[Add a Flatcar Container Linux for AKS (preview) node pool](#tabpanel_2_flatcar)

Create a new node pool using the

command. The following example creates a`az aks nodepool add`

`Linux`

node pool with the`Ubuntu`

OS SKU that runs*three*nodes. If you don't specify an OS SKU, AKS defaults to`Ubuntu`

.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-vm-size Standard_DS2_v2 \ --os-type Linux \ --os-sku Ubuntu \ --node-count 3`

It takes a few minutes to create the node pool.


### Add a Windows Server node pool

##### Install the `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


##### Register the `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


##### Create the Windows Server 2025 node pool

Create a new node pool using the

command. The following example creates a`az aks nodepool add`

`Windows`

node pool with the`Windows2025`

OS SKU that runs*three*nodes.For more information about Windows OS, see

[Windows best practices](windows-best-practices).`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-vm-size Standard_DS2_v2 \ --os-type Windows \ --os-sku Windows2025 \ --node-count 3`


## Check the status of your node pools

Check the status of your node pools using the

command and specify your resource group and cluster name.`az aks nodepool list`

`az aks nodepool list --resource-group $RESOURCE_GROUP_NAME --cluster-name $CLUSTER_NAME`


## Create an AKS cluster with a single node pool using an ARM template

If you want only one node pool in your AKS cluster, you can schedule application pods on system node pools. If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool. If one node goes down, the redundancy is compromised. You can mitigate this risk by having more system node pool nodes.

### Create a `Microsoft.ContainerService/managedClusters`

resource

- Create a
`Microsoft.ContainerService/managedClusters`

resource by adding[this JSON](/en-us/azure/templates/microsoft.containerservice/managedclusters?pivots=deployment-language-arm-template)to your template.

-
[Modify JSON to create a single Ubuntu node pool](#tabpanel_4_ubuntu-arm) -
[Modify JSON to create a single Azure Linux node pool](#tabpanel_4_azure-linux-arm) -
[Modify JSON to create a single Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_4_os-guard-arm) -
[Modify JSON to create a single Flatcar Container Linux for AKS (preview) node pool](#tabpanel_4_flatcar-arm)

Create a single Ubuntu node pool in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "1", "osSKU": "ubuntu", "osType": "linux" } ], }`


## Add a second node pool using an ARM template

The cluster created in the [previous section](#create-an-aks-cluster-with-a-single-node-pool-using-an-arm-template) has a single node pool. In this section, we add a second node pool to the cluster. This second node pool can have an OS type of `Linux`

with an OS SKU of `Ubuntu`

or `AzureLinux`

, or an OS type of `Windows`

.

### Add Linux node pools

-
[Modify JSON to create multiple Ubuntu node pools](#tabpanel_5_ubuntu-arm) -
[Modify JSON to create multiple Azure Linux node pools](#tabpanel_5_azure-linux-arm) -
[Modify JSON to create multiple Azure Linux with OS Guard for AKS (preview) node pools](#tabpanel_5_os-guard-arm) -
[Modify JSON to create multiple Flatcar Container Linux for AKS (preview) node pools](#tabpanel_5_flatcar-arm)

Create multiple Ubuntu node pools in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "3", "osSKU": "ubuntu", "osType": "linux" } ], }`


### Add Windows Server node pools

-
[Modify JSON to create multiple Windows Server 2025 (preview) node pools](#tabpanel_6_ws2025-arm) -
[Modify JSON to create multiple Windows Server 2022 node pools](#tabpanel_6_ws2022-arm)

##### Install the `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


##### Register the `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


##### Create the Windows Server 2025 node pools

Create multiple Windows node pools in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "3", "osSKU": "windows2025", "osType": "windows" } ], }`


## Deploy your ARM template

- Deploy your ARM template by following the guidance in
[Deploy an Azure Kubernetes Service (AKS) cluster using an ARM template](learn/quick-kubernetes-deploy-rm-template).

## Set taints, labels, or tags for a node pool

When creating a node pool, you can add taints, labels, or tags to it. When you add a taint, label, or tag, all nodes within that node pool also get that taint, label, or tag. We recommend applying these properties to an entire node pool instead of individual nodes. This way, you can easily manage the properties of all nodes in the node pool by updating the node pool properties instead of updating each node individually.

For specific instructions on how to set taints, labels, or tags for a node pool, use the following resources:

[Use node taints in an Azure Kubernetes Service (AKS) cluster](use-node-taints)[Use labels in an Azure Kubernetes Service (AKS) cluster](use-labels)[Use Azure tags in Azure Kubernetes Service (AKS)](use-tags)[Provide dedicated nodes using taints and tolerations in Azure Kubernetes Service (AKS)](operator-best-practices-advanced-scheduler#provide-dedicated-nodes-using-taints-and-tolerations)

## Next steps

In this article, you learned how to create an AKS cluster with a single node pool and add additional node pools to your cluster. To learn more about how to manage your node pools, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-cluster -->

# Upgrade options and recommendations for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article gives you a technical foundation for Azure Kubernetes Service (AKS) cluster upgrades by covering upgrade options and common scenarios. For in-depth guidance tailored to your needs, use the scenario-based navigation paths at the end of this article.

## What this article covers

This technical reference provides comprehensive AKS upgrade fundamentals on:

- Manual versus automated upgrade options and when to use each.
- Common upgrade scenarios with specific recommendations.
- Optimization techniques for performance and minimal disruption.
- Troubleshooting guidance for capacity, drain failures, and timing issues.
- Validation processes and pre-upgrade checks.

This hub is best for helping you to understand upgrade mechanics, troubleshoot issues, optimize upgrade settings, and learn about technical implementation.

For more information, see these related articles:

- To upgrade your production AKS clusters, see
[AKS production upgrade strategies](aks-production-upgrade-strategies). - To get upgrade patterns for AKS clusters with stateful workloads, see
[Stateful workload upgrade patterns](stateful-workload-upgrades). - To use the scenario hub to help you choose the right AKS upgrade approach, see
[AKS upgrade scenarios: Choose your path](upgrade-scenarios-hub).

If you're new to AKS upgrades, start with the [upgrade scenarios hub](upgrade-scenarios-hub) for guided, scenario-based assistance.

## Quick navigation

| Your situation | Recommended path |
|---|---|
| Production cluster needs an upgrade |
|

[Stateful workload patterns](stateful-workload-upgrades)[Basic AKS cluster upgrade](upgrade-aks-cluster)[Upgrade scenarios hub](upgrade-scenarios-hub)[Node pool upgrades](manage-node-pools#upgrade-a-cluster-control-plane-with-multiple-node-pools)[Single node pool upgrade](node-image-upgrade#upgrade-a-specific-node-pool)## Upgrade options

### Perform manual upgrades

Manual upgrades let you control when your cluster upgrades to a new Kubernetes version. These upgrades are useful for testing or targeting a specific version:

[Upgrade an AKS cluster](upgrade-aks-cluster)[Upgrade multiple AKS clusters via Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/update-orchestration)[Upgrade the node image](node-image-upgrade)[Customize node surge upgrade](upgrade-aks-cluster#customize-node-surge-upgrade)[Process node OS updates](node-updates-kured)

### Configure automatic upgrades

Automatic upgrades keep your cluster on a supported version and up to date. Use these upgrades when you want to automate your settings:

[Automatically upgrade an AKS cluster](auto-upgrade-cluster)[Automatically upgrade multiple AKS clusters via Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/update-automation)[Use planned maintenance to schedule and control upgrades](planned-maintenance)[Stop AKS cluster upgrades automatically on API breaking changes (preview)](stop-cluster-upgrade-api-breaking-changes)[Automatically upgrade AKS cluster node operating system images](auto-upgrade-node-image)[Apply security updates to AKS nodes automatically by using GitHub actions](node-upgrade-github-actions)

### Special considerations for node pools that span multiple availability zones

AKS uses best-effort zone balancing in node groups. During an upgrade surge, the zones for surge nodes in virtual machine scale sets are unknown ahead of time, which can temporarily cause an unbalanced zone configuration. AKS deletes surge nodes after the upgrade and restores the original zone balance.

To keep zones balanced, set surge to a multiple of three nodes. Persistent volume claims that use Azure locally redundant storage disks are zone bound and might cause downtime if surge nodes are in a different zone. Use a [pod disruption budget (PDB)](https://kubernetes.io/docs/tasks/run-application/configure-pdb/) to maintain high availability during drains.

### Optimize upgrades to improve performance and minimize disruptions

Combine [planned maintenance window](planned-maintenance), [max surge](upgrade-aks-cluster#customize-node-surge-upgrade), [PDB](https://kubernetes.io/docs/tasks/run-application/configure-pdb/), [node drain timeout](upgrade-aks-cluster#set-node-drain-timeout-value), and [node soak time](upgrade-aks-cluster#set-node-soak-time-value) to increase the likelihood of successful, low-disruption upgrades:

[Planned maintenance window](planned-maintenance): Schedule auto-upgrade during low-traffic periods. We recommend at least four hours.[Max surge](upgrade-aks-node-pools-rolling#set-max-surge-value): Higher values speed upgrades but might disrupt workloads. We recommend 33% for production.[Max unavailable](upgrade-aks-node-pools-rolling#customize-unavailable-nodes): Use when capacity is limited.[Pod disruption budget](https://kubernetes.io/docs/tasks/run-application/configure-pdb/): Set to limit pods down during upgrades. Validate for your service.[Node drain timeout](upgrade-aks-cluster#set-node-drain-timeout-value): Configure pod eviction wait duration. The default is 30 minutes.[Node soak time](upgrade-aks-cluster#set-node-soak-time-value): Stagger upgrades to minimize downtime. The default is 0 minutes.

| Upgrade settings | How extra nodes are used | Expected behavior |
|---|---|---|
`maxSurge=5` , `maxUnavailable=0` |
5 surge nodes | Five nodes are surged for upgrade. |
`maxSurge=5` , `maxUnavailable=0` |
0-4 surge nodes | Upgrade fails because of insufficient surge nodes. |
`maxSurge=0` , `maxUnavailable=5` |
N/A | Five existing nodes are drained for upgrade. |

Note

Before you upgrade, check for API breaking changes and review the [AKS release notes](https://github.com/Azure/AKS/releases) to avoid disruptions.

## Validations used in the upgrade process

AKS performs pre-upgrade validations to ensure cluster health:

**API breaking changes:**Detects deprecated APIs.**Kubernetes upgrade version:**Ensures a valid upgrade path.**PDB configuration:**Checks for misconfigured PDBs (for example,`maxUnavailable=0`

).**Quota:**Confirms enough quota for surge nodes.**Subnet:**Verifies sufficient IP addresses.**Certificates/service principals:**Detects expired credentials.

These checks help to minimize upgrade failures and provide early visibility into issues.

## Common upgrade scenarios and recommendations

### Scenario 1: Capacity constraints

If your cluster is limited by product tier or regional capacity, upgrades might fail when surge nodes can't be provisioned. This situation is common with specialized product tiers (like GPU nodes) or in regions with limited resources. Errors such as `SKUNotAvailable`

, `AllocationFailed`

, or `OverconstrainedAllocationRequest`

might occur if `maxSurge`

is set too high for available capacity.

#### Recommendations to prevent or resolve

- Use
`maxUnavailable`

to upgrade by using existing nodes instead of surging new ones. For more information, see[Customize unavailable nodes during upgrade](upgrade-aks-cluster#customize-unavailable-nodes-during-upgrade). - Lower
`maxSurge`

to reduce extra capacity needs. For more information, see[Customize node surge upgrade](upgrade-aks-cluster#customize-node-surge-upgrade). - For security-only updates, use security patch reimages that don't require surge nodes. For more information, see
[Apply security and kernel updates to Linux nodes in Azure Kubernetes Service](node-updates-kured).

### Scenario 2: Node drain failures and PDBs

Upgrades require draining nodes (evicting pods). Drains can fail when pods are slow to terminate or strict [Pod Disruption Budgets (PDBs)](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/) block pod evictions.

Example error:

```
Code: UpgradeFailed
Message: Drain node ... failed when evicting pod ... Cannot evict pod as it would violate the pod's disruption budget.
```


#### Option 1: Force upgrade (bypass PDB)

Warning

Force upgrade bypasses Pod Disruption Budget (PDB) constraints and may cause service disruption by draining all pods simultaneously. Before using this option, first try to fix PDB misconfigurations (review the PDB minAvailable/maxUnavailable settings, ensure adequate pod replicas, verify PDBs aren't blocking all evictions).

Use force upgrade only when PDBs prevent critical upgrades and cannot be resolved. This will override PDB protections and potentially cause complete service unavailability during the upgrade.

**Requirements:** Azure CLI 2.79.0+ or AKS API version 2025-09-01+

```
az aks upgrade \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP_NAME \
--kubernetes-version $KUBERNETES_VERSION \
--enable-force-upgrade \
--upgrade-override-until 2023-10-01T13:00:00Z
```


Note

- The
`upgrade-override-until`

parameter defines when validation bypass ends (must be a future date/time) - If not specified, the window defaults to 3 days from current time
- The 'Z' indicates UTC/GMT time zone

Warning

When force upgrade is enabled, it takes precedence over all other drain configurations. The undrainable node behavior settings (Option 2) will not be applied when force upgrade is active.

#### Option 2: Handle undrainable nodes (honor PDB)

Use this conservative approach to honor PDBs while preventing upgrade failures.

**Configure undrainable node behavior:**

```
az aks nodepool update \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--name <node-pool-name> \
--undrainable-node-behavior Cordon \
--max-blocked-nodes 2 \
--drain-timeout 30
```


**Behavior options:**

**Schedule (default):**Deletes blocked node and surges replacement**Cordon (recommended):**Cordons node and labels it as`kubernetes.azure.com/upgrade-status=Quarantined`


**Max blocked nodes (preview):**

- Specifies how many nodes that fail to drain are tolerated
- Requires
`undrainable-node-behavior`

to be set - Defaults to
`maxSurge`

value (typically 10%) if not specified

##### Prerequisites for max blocked nodes

The Azure CLI

`aks-preview`

extension version 18.0.0b9 or later is required to use the max blocked nodes feature.`# Install or update the aks-preview extension az extension add --name aks-preview az extension update --name aks-preview`


##### Example configuration with max blocked nodes

```
az aks nodepool update \
--cluster-name jizenMC1 \
--name nodepool1 \
--resource-group jizenTestMaxBlockedNodesRG \
--max-surge 1 \
--undrainable-node-behavior Cordon \
--max-blocked-nodes 2 \
--drain-timeout 5
```


#### Recommendations to prevent drain failures

- Set
`maxUnavailable`

in PDBs to allow at least one pod eviction - Increase pod replicas to meet disruption budget requirements
- Extend drain timeout if workloads need more time. (The default is
*30 minutes*.) - Test PDBs in staging, monitor upgrade events, and use blue-green deployments for critical workloads. For more information, see
[Blue-green deployment of AKS clusters](/en-us/azure/architecture/guide/aks/blue-green-deployment-for-aks).

##### Verify undrainable nodes

The blocked nodes are unscheduled for pods and marked with the label

`"kubernetes.azure.com/upgrade-status: Quarantined"`

.Verify the label on any blocked nodes when there's a drain node failure on upgrade:

`kubectl get nodes --show-labels=true`


##### Resolve undrainable nodes

Remove the responsible PDB:

`kubectl delete pdb <pdb-name>`

Remove the

`kubernetes.azure.com/upgrade-status: Quarantined`

label:`kubectl label nodes <node-name> <label-name>`

Optionally, delete the blocked node:

`az aks nodepool delete-machines --cluster-name <cluster-name> --machine-names <machine-name> --name <node-pool-name> --resource-group <resource-group-name>`

After you finish this step, you can reconcile the cluster status by performing any update operation without the optional fields as outlined in

[az aks](/en-us/cli/azure/aks#az-aks-update). Alternatively, you can scale the node pool to the same number of nodes as the count of upgraded nodes. This action ensures that the node pool gets to its intended original size. AKS prioritizes the removal of the blocked nodes. This command also restores the cluster provisioning status to`Succeeded`

. In the following example,`2`

is the total number of upgraded nodes.`# Update the cluster to restore the provisioning status az aks update --resource-group <resource-group-name> --name <cluster-name> # Scale the node pool to restore the original size az aks nodepool scale --resource-group <resource-group-name> --cluster-name <cluster-name> --name <node-pool-name> --node-count 2`


### Scenario 3: Slow upgrades

Conservative settings or node-level issues can delay upgrades, which affects your ability to stay current with patches and improvements.

Common causes of slow upgrades include:

- Low
`maxSurge`

or`maxUnavailable`

values (limits parallelism). - High soak times (long waits between node upgrades).
- Drain failures (see
[Node drain failures](#scenario-2-node-drain-failures-and-pdbs)).

#### Recommendations to prevent or resolve

- Use
`maxSurge=33%`

,`maxUnavailable=1`

for production. - Use
`maxSurge=50%`

,`maxUnavailable=2`

for dev/test. - Use OS Security Patch for fast, targeted patching (avoids full node reimaging).
- Enable
`undrainableNodeBehavior`

to avoid upgrade blockers.

### Scenario 4: IP exhaustion

Surge nodes require more IPs. If the subnet is near capacity, node provisioning can fail (for example, `Error: SubnetIsFull`

). This scenario is common with Azure Container Networking Interface, high `maxPods`

, or large node counts.

#### Recommendations to prevent or resolve

Ensure that your subnet has enough IPs for all nodes, surge nodes, and pods. The formula is

`Total IPs = (Number of nodes + maxSurge) * (1 + maxPods)`

.Reclaim unused IPs or expand the subnet (for example, from /24 to /22).

Lower

`maxSurge`

if subnet expansion isn't possible:`az aks nodepool update \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --max-surge 10%`

Monitor IP usage with Azure Monitor or custom alerts.

Reduce

`maxPods`

per node, clean up orphaned load balancer IPs, and plan subnet sizing for high-scale clusters.

## Frequently asked questions

### Can I use open-source tools for validation?

Yes. Many open-source tools integrate well with AKS upgrade processes:

[kube-no-trouble (kubent)](https://github.com/doitintl/kube-no-trouble): Scans for deprecated APIs before upgrades.[Trivy](https://aquasecurity.github.io/trivy/): Security scanning for container images and Kubernetes configurations.[Sonobuoy](https://sonobuoy.io/): Kubernetes conformance testing and cluster validation.[kube-bench](https://github.com/aquasecurity/kube-bench): Security benchmark checks against Center for Internet Security standards.[Polaris](https://github.com/FairwindsOps/polaris): Validation of Kubernetes best practices.[kubectl-neat](https://github.com/itaysk/kubectl-neat): Clean up Kubernetes manifests for validation.

### How do I validate API compatibility before upgrading?

Run deprecation checks by using tools like kubent:

```
# Install and run API deprecation scanner
kubectl apply -f https://github.com/doitintl/kube-no-trouble/releases/latest/download/knt-full.yaml
# Check for deprecated APIs in your cluster
kubectl run knt --image=doitintl/knt:latest --rm -it --restart=Never -- \
-c /kubeconfig -o json > api-deprecation-report.json
# Review findings
cat api-deprecation-report.json | jq '.[] | select(.deprecated==true)'
```


### What makes AKS upgrades different from other Kubernetes platforms?

AKS provides several unique advantages:

- Native Azure integration with Azure Traffic Manager, Azure Load Balancer, and networking.
- Azure Kubernetes Fleet Manager for coordinated multicluster upgrades.
- Automatic node image patching without manual node management.
- Built-in validation for quota, networking, and credentials.
- Azure support for upgrade-related issues.

## Choose your upgrade path

This article provided you with a technical foundation. Now select your scenario-based path.

### Ready to execute?

| If you have... | Then go to... |
|---|---|
| Production environment |
|

[Stateful workload patterns](stateful-workload-upgrades): Safe upgrade patterns for data persistence[Upgrade scenarios hub](upgrade-scenarios-hub): Decision tree for complex setups[Upgrade an AKS cluster](upgrade-aks-cluster): Step-by-step cluster upgrade### Still deciding?

Use the [upgrade scenarios hub](upgrade-scenarios-hub) for a guided decision tree that considers your:

- Downtime tolerance
- Environment complexity
- Risk profile
- Timeline constraints

## Next tasks

- Review
[AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices)for best practices and planning tips before you start any upgrade. - Always check for
[API breaking changes](https://aka.ms/aks/breakingchanges)and validate your workload's compatibility with the target Kubernetes version. - Test upgrade settings (such as
`maxSurge`

,`maxUnavailable`

, and PDBs) in a staging environment to minimize production risk. - Monitor upgrade events and cluster health throughout the process.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-scale -->

# Istio service mesh add-on performance and scaling

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Istio-based service mesh add-on is logically split into a control plane (`istiod`

) and a data plane. The data plane is composed of Envoy sidecar proxies inside workload pods. Istiod manages and configures these Envoy proxies. This article presents the performance of both the control and data plane for revision asm-1-19, including resource consumption, sidecar capacity, and latency overhead. Additionally, it provides suggestions for addressing potential strain on resources during periods of heavy load. This article also covers how to customize scaling for the control plane and gateways.

## Control plane performance

[Istiod’s CPU and memory requirements](https://istio.io/latest/docs/ops/deployment/performance-and-scalability/#control-plane-performance) correlate with the rate of deployment and configuration changes and the number of proxies connected. The scenarios tested were:

- Pod churn: examines the impact of pod churning on
`istiod`

. To reduce variables, only one service is used for all sidecars. - Multiple services: examines the impact of multiple services on the maximum sidecars Istiod can manage (sidecar capacity), where each service has
`N`

sidecars, totaling the overall maximum.

#### Test specifications

- One
`istiod`

instance with default settings - Horizontal pod autoscaling disabled
- Tested with two network plugins: Azure Container Networking Interface (CNI) Overlay and Azure CNI Overlay with Cilium
[(recommended network plugins for large scale clusters)](/en-us/azure/aks/azure-cni-overlay?tabs=kubectl#choosing-a-network-model-to-use) - Node SKU: Standard D16 v3 (16 vCPU, 64-GB memory)
- Kubernetes version: 1.28.5
- Istio revision: asm-1-19

### Pod churn

The [ClusterLoader2 framework](https://github.com/kubernetes/perf-tests/tree/master/clusterloader2#clusterloader) was used to determine the maximum number of sidecars Istiod can manage when there's sidecar churning. The churn percent is defined as the percent of sidecars churned down/up during the test. For example, 50% churn for 10,000 sidecars would mean that 5,000 sidecars were churned down, then 5,000 sidecars were churned up. The churn percents tested were determined from the typical churn percentage during deployment rollouts (`maxUnavailable`

). The churn rate was calculated by determining the total number of sidecars churned (up and down) over the actual time taken to complete the churning process.

#### Sidecar capacity and Istiod CPU and memory

**Azure CNI overlay**

| Churn (%) | Churn Rate (sidecars/sec) | Sidecar Capacity | Istiod Memory (GB) | Istiod CPU |
|---|---|---|---|---|
| 0 | -- | 25000 | 32.1 | 15 |
| 25 | 31.2 | 15000 | 22.2 | 15 |
| 50 | 31.2 | 15000 | 25.4 | 15 |

**Azure CNI overlay with Cilium**

| Churn (%) | Churn Rate (sidecars/sec) | Sidecar Capacity | Istiod Memory (GB) | Istiod CPU |
|---|---|---|---|---|
| 0 | -- | 30000 | 41.2 | 15 |
| 25 | 41.7 | 25000 | 36.1 | 16 |
| 50 | 37.9 | 25000 | 42.7 | 16 |

### Multiple services

The [ClusterLoader2 framework](https://github.com/kubernetes/perf-tests/tree/master/clusterloader2#clusterloader) was used to determine the maximum number of sidecars `istiod`

can manage with 1,000 services. The results can be compared to the 0% churn test (one service) in the pod churn scenario. Each service had `N`

sidecars contributing to the overall maximum sidecar count. The API Server resource usage was observed to determine if there was any significant stress from the add-on.

**Sidecar capacity**

| Azure CNI Overlay | Azure CNI Overlay with Cilium |
|---|---|
| 20000 | 20000 |

**CPU and memory**

| Resource | Azure CNI Overlay | Azure CNI Overlay with Cilium |
|---|---|---|
| API Server Memory (GB) | 38.9 | 9.7 |
| API Server CPU | 6.1 | 4.7 |
| Istiod Memory (GB) | 40.4 | 42.6 |
| Istiod CPU | 15 | 16 |

## Data plane performance

Various factors impact [sidecar performance](https://istio.io/latest/docs/ops/deployment/performance-and-scalability/#data-plane-performance) such as request size, number of proxy worker threads, and number of client connections. Additionally, any request flowing through the mesh traverses the client-side proxy and then the server-side proxy. Therefore, latency and resource consumption are measured to determine the data plane performance.

[ Fortio](https://fortio.org/) was used to create the load. The test was conducted with the

[Istio benchmark repository](https://github.com/istio/tools/tree/master/perf/benchmark#istio-performance-benchmarking)that was modified for use with the add-on.

#### Test specifications

- Tested with two network plugins: Azure CNI Overlay and Azure CNI Overlay with Cilium
[(recommended network plugins for large scale clusters)](/en-us/azure/aks/azure-cni-overlay?tabs=kubectl#choosing-a-network-model-to-use) - Node SKU: Standard D16 v5 (16 vCPU, 64-GB memory)
- Kubernetes version: 1.28.5
- Two proxy workers
- 1-KB payload
- 1,000 Queries per second (QPS) at varying client connections
`http/1.1`

protocol and mutual Transport Layer Security (TLS) enabled- 26 data points collected

#### CPU and memory

The memory and CPU usage for both the client and server proxy for 16 client connections and 1,000 QPS across all network plugin scenarios is roughly 0.4 vCPU and 72 MB.

#### Latency

The sidecar Envoy proxy collects raw telemetry data after responding to a client, which doesn't directly affect the request's total processing time. However, this process delays the start of handling the next request, contributing to queue wait times and influencing average and tail latencies. Depending on the traffic pattern, the actual tail latency varies.

The following results evaluate the impact of adding sidecar proxies to the data path, showcasing the P90 and P99 latency.

- Sidecar traffic path: client --> client-sidecar --> server-sidecar --> server
- Baseline traffic path: client --> server

A comparison of data plane latency performance across Istio add-on and AKS versions can be found [here](istio-latency).

| Azure CNI Overlay | Azure CNI Overlay with Cilium |
|---|---|
|

## Scaling

### Horizontal pod autoscaling customization

[Horizontal pod autoscaling (HPA)](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) is enabled for the `istiod`

and ingress/egress gateway deployments. The default configurations for `istiod`

and the gateways are:

- Min Replicas: 2
- Max Replicas: 5
- CPU Utilization: 80%

Note

To prevent conflicts with the `PodDisruptionBudget`

, the add-on does not allow setting the `minReplicas`

below the initial default of `2`

.

The following are the `istiod`

and ingress gateway HPA resources:

```
NAMESPACE NAME REFERENCE
aks-istio-ingress aks-istio-ingressgateway-external-asm-1-19 Deployment/aks-istio-ingressgateway-external-asm-1-19
aks-istio-ingress aks-istio-ingressgateway-internal-asm-1-19 Deployment/aks-istio-ingressgateway-internal-asm-1-19
aks-istio-system istiod-asm-1-19 Deployment/istiod-asm-1-19
```


The HPA configuration can be modified through patches and direct edits. Example:

```
kubectl patch hpa aks-istio-ingressgateway-external-asm-1-19 -n aks-istio-ingress --type merge --patch '{"spec": {"minReplicas": 3, "maxReplicas": 6}}'
```


Note

See the [Istio add-on upgrade documentation](istio-upgrade#minor-revision-upgrades-with-horizontal-pod-autoscaling-customizations) for details on how HPA settings are applied across both revisions during a canary upgrade.

## Service entry

Istio's ServiceEntry custom resource definition enables adding other services into the Istio’s internal service registry. A [ServiceEntry](https://istio.io/latest/docs/reference/config/networking/service-entry/) allows services already in the mesh to route or access the services specified. However, the configuration of multiple ServiceEntries with the `resolution`

field set to DNS can cause a [heavy load on Domain Name System (DNS) servers](https://preliminary.istio.io/latest/docs/ops/configuration/traffic-management/dns/#proxy-dns-resolution). The following suggestions can help reduce the load:

- Switch to
`resolution: NONE`

to avoid proxy DNS lookups entirely. Suitable for most use cases. However, when using an[Istio add-on egress gateway](istio-deploy-egress), the ServiceEntry resolution must be set to`DNS`

. - Increase TTL (Time To Live) if you control the domains being resolved.
- Limit the ServiceEntry scope with
`exportTo`

.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/private-apiserver-vnet-integration-cluster -->

# Connect to an API Server VNet Integration cluster by using Azure Private Link

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

API Server VNet Integration lets you place the control‑plane IP inside your own VNet. The pattern described here extends that capability to more VNets by chaining Private Link. It's useful for hub‑and‑spoke topologies, dedicated build networks, or jump‑host VNets that must administer production clusters without opening the API server to the public internet.

This article applies **only to clusters that are created with API Server VNet Integration** and shows you how to:

- Deploy a
**private**AKS cluster with API Server VNet Integration. - Expose the API server through a
**Private Link Service (PLS)**inside the cluster virtual network. - Create a
**Private Endpoint (PE)**in a different virtual network. - Configure
**private DNS**so Kubernetes tools resolve the cluster’s private FQDN inside the remote network.

For private clusters that **do not** use API Server VNet Integration, see [Create a private AKS cluster](private-clusters).

## Region availability

API Server VNet Integration is currently available in a subset of Azure regions and is subject to regional capacity limits. Before you begin, confirm that your target region is supported. For more information, see [API Server VNet Integration](api-server-vnet-integration).

## Prerequisites

| Requirement | Minimum |
|---|---|
| Azure CLI | 2.73.0 |
| Permissions | Contributor + Network Contributor on both subscriptions |

If you use custom DNS servers, add Azure’s virtual IP **168.63.129.16** as an upstream forwarder.

## Set environment variables

Set the following environment variables for use throughout this article. Feel free to replace the placeholder values with your own.

```
LOCATION="westus3"
# Resource groups
AKS_RG="aks-demo-rg"
REMOTE_RG="client-demo-rg"
# AKS cluster
AKS_CLUSTER="aks-private"
AKS_SUBNET="aks-subnet"
# Private Link Service
PLS_NAME="apiserver-pls"
PLS_SUBNET="pls-subnet"
PLS_PREFIX="10.225.0.0/24"
# Remote VNet
REMOTE_VNET="client-vnet"
REMOTE_SUBNET="client-subnet"
REMOTE_VNET_PREFIX="192.168.0.0/16"
REMOTE_SUBNET_PREFIX="192.168.1.0/24"
PE_NAME="aks-pe"
PE_CONN_NAME="aks-pe-conn"
# DNS
DNS_ZONE="private.${LOCATION}.azmk8s.io"
DNS_LINK="dns-link"
```


## Create resource groups

```
# Create resource groups for the AKS cluster
az group create --name $AKS_RG --location $LOCATION
# Create a resource group for the remote VNet
az group create --name $REMOTE_RG --location $LOCATION
```


## Deploy a private cluster with API Server VNet Integration

Important

API Server VNet Integration requires its own subnet. If you don't supply one, AKS automatically creates it in the node resource group.

```
az aks create \
--name $AKS_CLUSTER \
--resource-group $AKS_RG \
--location $LOCATION \
--enable-private-cluster \
--enable-apiserver-vnet-integration
```


After the cluster finishes provisioning, capture the autogenerated node resource group, cluster VNet name, and private FQDN label:

```
AKS_NODE_RG=$(az aks show -g $AKS_RG -n $AKS_CLUSTER --query nodeResourceGroup -o tsv)
AKS_VNET=$(az network vnet list --resource-group $AKS_NODE_RG --query '[0].name' -o tsv)
DNS_RECORD=$(az aks show -g $AKS_RG -n $AKS_CLUSTER --query privateFqdn -o tsv | cut -d'.' -f1,2)
FRONTEND_IP_CONFIG_ID=$(az network lb show \
--name kube-apiserver \
--resource-group $AKS_NODE_RG \
--query "frontendIPConfigurations[0].id" \
-o tsv)
```


## Create a Private Link Service (PLS) in the AKS cluster VNet

Add a dedicated subnet for the PLS and disable network policies, which aren't supported on Private Link subnets.

Create the PLS and point it to the kube‑apiserver internal load balancer that AKS created for the control plane.

```
# Subnet for the PLS
az network vnet subnet create \
--name $PLS_SUBNET \
--vnet-name $AKS_VNET \
--resource-group $AKS_NODE_RG \
--address-prefixes $PLS_PREFIX \
--disable-private-link-service-network-policies
# PLS pointing to the API‑server ILB
az network private-link-service create \
--name $PLS_NAME \
--resource-group $AKS_NODE_RG \
--vnet-name $AKS_VNET \
--subnet $PLS_SUBNET \
--lb-frontend-ip-configs $FRONTEND_IP_CONFIG_ID \
--location $LOCATION
```


## Create a PrivateEndpoint (PE) in the remote VNet

```
# Remote VNet and subnet
az network vnet create \
--name $REMOTE_VNET \
--resource-group $REMOTE_RG \
--location $LOCATION \
--address-prefixes $REMOTE_VNET_PREFIX
az network vnet subnet create \
--name $REMOTE_SUBNET \
--vnet-name $REMOTE_VNET \
--resource-group $REMOTE_RG \
--address-prefixes $REMOTE_SUBNET_PREFIX
# Private Endpoint
PLS_ID=$(az network private-link-service show \
--name $PLS_NAME \
--resource-group $AKS_NODE_RG \
--query id -o tsv)
az network private-endpoint create \
--name $PE_NAME \
--resource-group $REMOTE_RG \
--vnet-name $REMOTE_VNET \
--subnet $REMOTE_SUBNET \
--private-connection-resource-id $PLS_ID \
--connection-name $PE_CONN_NAME \
--location $LOCATION
```


When the Private Endpoint finishes provisioning, note its network interface (NIC) ID so you can retrieve the allocated private IP address.

```
PE_NIC_ID=$(az network private-endpoint show \
--name $PE_NAME \
--resource-group $REMOTE_RG \
--query 'networkInterfaces[0].id' \
--output tsv)
# Capture the IP from the NIC
PE_IP=$(az network nic show \
--ids $PE_NIC_ID \
--query 'ipConfigurations[0].privateIPAddress' \
--output tsv)
```


## Configure private DNS

```
# Create or reuse the regional DNS zone
az network private-dns zone create \
--name $DNS_ZONE \
--resource-group $REMOTE_RG
az network private-dns record-set a create \
--name $DNS_RECORD \
--zone-name $DNS_ZONE \
--resource-group $REMOTE_RG
az network private-dns record-set a add-record \
--record-set-name $DNS_RECORD \
--zone-name $DNS_ZONE \
--resource-group $REMOTE_RG \
--ipv4-address $PE_IP
# Link zone to the remote VNet
REMOTE_VNET_ID=$(az network vnet show \
--name $REMOTE_VNET \
--resource-group $REMOTE_RG \
--query id -o tsv)
az network private-dns link vnet create \
--name $DNS_LINK \
--zone-name $DNS_ZONE \
--resource-group $REMOTE_RG \
--virtual-network $REMOTE_VNET_ID \
--registration-enabled false
```


## Test the connection

If you try to test the connection locally, you might get an error because the DNS zone isn't linked to your local network.

```
az aks get-credentials --resource-group $AKS_RG --name $AKS_CLUSTER
kubectl get nodes
```


### Deploy a test VM in the remote VNet

To confirm the Private Endpoint path, deploy a test VM in the remote VNet and use it to connect to the AKS cluster.

```
# Create Network Security Group that allows inbound SSH (TCP 22)
az network nsg create \
--name "${REMOTE_VNET}-nsg" \
--resource-group $REMOTE_RG \
--location $LOCATION
az network nsg rule create \
--nsg-name "${REMOTE_VNET}-nsg" \
--resource-group $REMOTE_RG \
--name allow-ssh \
--priority 100 \
--access Allow \
--protocol Tcp \
--direction Inbound \
--source-address-prefixes '*' \
--destination-port-ranges 22
# Associate the NSG with the remote subnet
az network vnet subnet update \
--name $REMOTE_SUBNET \
--vnet-name $REMOTE_VNET \
--resource-group $REMOTE_RG \
--network-security-group "${REMOTE_VNET}-nsg"
# Create a small Ubuntu VM in that subnet (with a public IP for quick SSH)
az vm create \
--resource-group $REMOTE_RG \
--name test-vm \
--image Ubuntu2204 \
--size Standard_B2s \
--admin-username azureuser \
--generate-ssh-keys \
--vnet-name $REMOTE_VNET \
--subnet $REMOTE_SUBNET \
--public-ip-sku Standard
# Capture the public IP address
VM_PUBLIC_IP=$(az vm show -d -g $REMOTE_RG -n test-vm --query publicIps -o tsv)
```


### Connect to the VM and test the connection

```
ssh -i ~/.ssh/id_rsa azureuser@$VM_PUBLIC_IP
# Inside the VM
# Install Azure CLI
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
# Install kubectl
sudo az aks install-cli
# re-export the aks variables
export AKS_RG="aks-demo-rg"
export AKS_CLUSTER="aks-private"
# login to Azure. Follow the instructions to authenticate
az login
# Get the AKS credentials
az aks get-credentials --resource-group $AKS_RG --name $AKS_CLUSTER
# Test the connection
kubectl get nodes
# You should see the AKS nodes
# Exit the VM
exit
```


## Clean up resources

To avoid ongoing Azure charges, delete the resource groups using the [ az group delete](/en-us/cli/azure/group#az-group-delete) command.

```
az group delete --name $AKS_RG --yes --no-wait
az group delete --name $REMOTE_RG --yes --no-wait
```

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-autoprovision-networking -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-networking -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/csi-secrets-store-driver -->

# Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Key Vault provider for Secrets Store CSI Driver allows for the integration of an Azure Key Vault as a secret store with an Azure Kubernetes Service (AKS) cluster via a [CSI volume](https://kubernetes-csi.github.io/docs/).

## Features

- Mounts secrets, keys, and certificates to a pod using a CSI volume.
- Supports CSI inline volumes.
- Supports mounting multiple secrets store objects as a single volume.
- Supports pod portability with the
`SecretProviderClass`

CRD. - Supports Windows containers.
- Syncs with Kubernetes secrets.
- Supports autorotation of mounted contents and synced Kubernetes secrets.

## Limitations

- A container using a
`ConfigMap`

or`Secret`

as a`subPath`

volume mount does not receive automated updates when the secret is rotated. This is a Kubernetes limitation. To have the changes take effect, the application needs to reload the changed file by either watching for changes in the file system or by restarting the pod. For more information, see[Secrets Store CSI Driver known limitations](https://secrets-store-csi-driver.sigs.k8s.io/known-limitations.html#secrets-not-rotated-when-using-subpath-volume-mount). - The add-on creates a managed identity named
`azurekeyvaultsecretsprovider-xxx`

in the node resource group and assigns it to the Virtual Machine Scale Sets (VMSS) automatically. You can use this managed identity or your own managed identity to access the key vault. It's not supported to prevent creation of the identity.

## Prerequisites

- If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - Check that your version of the Azure CLI is 2.30.0 or later. If it's an earlier version,
[install the latest version](/en-us/cli/azure/install-azure-cli).

### Network

- If using network isolated clusters, it's recommended to
[set up private endpoint to access Azure Key Vault](/en-us/azure/key-vault/general/private-link-service). - If the cluster has outbound type
`userDefinedRouting`

and uses a firewall device that can control outbound traffic based on domain names, such as Azure Firewall, ensure the[required outbound network rules and FQDNs are allowed](outbound-rules-control-egress#azure-key-vault-provider-for-secrets-store-csi-driver). - If you're restricting Ingress to the cluster, make sure ports
**9808**and**8095**are open.

### Roles

- The identity used to with the
`SecretProviderClass`

needs to have`Key Vault Certificate User`

to access`key`

or`certificate`

[object types](/en-us/azure/key-vault/general/about-keys-secrets-certificates#object-types). - The identity used to with the
`SecretProviderClass`

needs to have`Key Vault Secrets User`

to access`secret`

[object type](/en-us/azure/key-vault/general/about-keys-secrets-certificates#object-types).

## Create an AKS cluster with Azure Key Vault provider for Secrets Store CSI Driver support

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus2`

Create an AKS cluster with Azure Key Vault provider for Secrets Store CSI Driver capability using the

command with the`az aks create`

`--enable-addons azure-keyvault-secrets-provider`

parameter. The add-on creates a user-assigned managed identity you can use to authenticate to your key vault. The following example creates an AKS cluster with the Azure Key Vault provider for Secrets Store CSI Driver enabled.Note

If you want to use Microsoft Entra Workload ID, you must also use the

`--enable-oidc-issuer`

and`--enable-workload-identity`

parameters, such as in the following example:`az aks create --name myAKSCluster --resource-group myResourceGroup --enable-addons azure-keyvault-secrets-provider --enable-oidc-issuer --enable-workload-identity --generate-ssh-keys`

`az aks create \ --name myAKSCluster \ --resource-group myResourceGroup \ --enable-addons azure-keyvault-secrets-provider \ --generate-ssh-keys`

The previous command creates a user-assigned managed identity,

`azureKeyvaultSecretsProvider`

, to access Azure resources. The following example uses this identity to connect to the key vault that stores the secrets, but you can also use other[identity access methods](csi-secrets-store-identity-access). Take note of the identity's`clientId`

in the output.`..., "addonProfiles": { "azureKeyvaultSecretsProvider": { ..., "identity": { "clientId": "<client-id>", ... } }`


Note

After you enable this feature, AKS creates a managed identity named `azurekeyvaultsecretsprovider-xxx`

in the node resource group and assigns it to the Virtual Machine Scale Sets (VMSS) automatically. You can use this managed identity or your own managed identity to access the key vault. It's not supported to prevent creation of the identity.

## Upgrade an existing AKS cluster with Azure Key Vault provider for Secrets Store CSI Driver support

Upgrade an existing AKS cluster with Azure Key Vault provider for Secrets Store CSI Driver capability using the

command and enable the`az aks enable-addons`

`azure-keyvault-secrets-provider`

add-on. The add-on creates a user-assigned managed identity you can use to authenticate to your key vault.`az aks enable-addons --addons azure-keyvault-secrets-provider --name myAKSCluster --resource-group myResourceGroup`


Note

After you enable this feature, AKS creates a managed identity named `azurekeyvaultsecretsprovider-xxx`

in the node resource group and assigns it to the Virtual Machine Scale Sets (VMSS) automatically. You can use this managed identity or your own managed identity to access the key vault. It's not supported to prevent creation of the identity.

## Verify the Azure Key Vault provider for Secrets Store CSI Driver installation

Get the AKS cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials --name myAKSCluster --resource-group myResourceGroup`

Verify the installation is finished using the

`kubectl get pods`

command, which lists all pods with the`secrets-store-csi-driver`

and`secrets-store-provider-azure`

labels in the kube-system namespace.`kubectl get pods -n kube-system -l 'app in (secrets-store-csi-driver,secrets-store-provider-azure)'`

Your output should look similar to the following example output:

`NAME READY STATUS RESTARTS AGE aks-secrets-store-csi-driver-4vpkj 3/3 Running 2 4m25s aks-secrets-store-csi-driver-ctjq6 3/3 Running 2 4m21s aks-secrets-store-csi-driver-tlvlq 3/3 Running 2 4m24s aks-secrets-store-provider-azure-5p4nb 1/1 Running 0 4m21s aks-secrets-store-provider-azure-6pqmv 1/1 Running 0 4m24s aks-secrets-store-provider-azure-f5qlm 1/1 Running 0 4m25s`

Verify that each node in your cluster's node pool has a Secrets Store CSI Driver pod and a Secrets Store Provider Azure pod running.


## Create or use an existing Azure Key Vault

Create or update a key vault with Azure role-based access control (Azure RBAC) enabled using the

command or the`az keyvault create`

command with the`az keyvault update`

`--enable-rbac-authorization`

flag. The name of the key vault must be globally unique. For more details on key vault permission models and Azure RBAC, see[Provide access to Key Vault keys, certificates, and secrets with an Azure role-based access control](/en-us/azure/key-vault/general/rbac-guide)`## Create a new Azure key vault az keyvault create --name <keyvault-name> --resource-group myResourceGroup --location eastus2 --enable-rbac-authorization ## Update an existing Azure key vault az keyvault update --name <keyvault-name> --resource-group myResourceGroup --location eastus2 --enable-rbac-authorization`

Your key vault can store keys, secrets, and certificates. In this example, use the

command to set a plain-text secret called`az keyvault secret set`

`ExampleSecret`

.`az keyvault secret set --vault-name <keyvault-name> --name ExampleSecret --value MyAKSExampleSecret`

Take note of the following properties for future use:

- The name of the secret object in the key vault
- The object type (secret, key, or certificate)
- The name of your key vault resource
- The Azure tenant ID of the subscription


## Next steps

In this article, you learned how to use the Azure Key Vault provider for Secrets Store CSI Driver in an AKS cluster. You now need to provide an identity to access the Azure Key Vault. To learn how, continue to the next article.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-aks-partner-solutions -->

# Windows AKS partner solutions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Microsoft collaborates with partners to ensure your build, test, deployment, configuration, and monitoring of your applications perform optimally with Windows containers on AKS.

Our third party partners featured in this article have introduction guides to help you start using their solutions with your applications running on Windows containers on AKS.

| Solutions | Partners |
|---|---|
| DevOps |
|

[NGINX](#f5-nginx)[Calico](#calico)[Datadog](#datadog)[New Relic](#new-relic)[Prisma Cloud](#prisma-cloud)[NetApp](#netapp)[Chef](#chef)## DevOps

DevOps streamlines the delivery process, improves collaboration across teams, and enhances software quality, ensuring swift, reliable, and continuous deployment of your Windows-based applications.

### GitLab

The GitLab DevSecOps Platform supports the Microsoft development ecosystem with performance, accessibility testing, SAST, DAST and Fuzzing security scanning, dependency scanning, SBOM, license management and more.

As an extensible platform, GitLab also allows you to plug in your own tooling for any stage. GitLab's integration with Azure Kubernetes Services (AKS) enables full DevSecOps workflows for Windows and Linux Container workloads using either Push CD or GitOps Pull CD with flux manifests. Using Cloud Native Buildpaks, GitLab Auto DevOps can build, test, and autodeploy OSS .NET projects.

To learn more, please our see our [joint blog](https://techcommunity.microsoft.com/t5/containers/using-gitlab-to-build-and-deploy-windows-containers-on-azure/ba-p/3889929).

### CircleCI

CircleCI’s integration with Azure Kubernetes Services (AKS) allows you to automate, build, validate, and ship containerized Windows applications, ensuring faster and more reliable software deployment. You can easily integrate your pipeline with AKS using CircleCI orbs, which are prepacked snippets of YAML configuration.

Follow this [tutorial](https://techcommunity.microsoft.com/t5/containers/continuous-deployment-of-windows-containers-with-circleci-and/ba-p/3841220) to learn how to set up a CI/CD pipeline to build a Dockerized ASP.NET application and deploy it to an AKS cluster.

## Networking

Ensure efficient traffic management, enhanced security, and optimal network performance with these solutions to achieve smooth application connectivity and communication.

### F5 NGINX

NGINX Ingress Controller deployed in AKS, on-premises, and in the cloud implements unified Kubernetes-native API gateways, load balancers, and Ingress controllers to reduce complexity, increase uptime, and provide in-depth insights into app health and performance for containerized Windows workloads.

Running at the edge of a Kubernetes cluster, NGINX Ingress Controller ensures holistic app security with user and service identities, authorization, access control, encrypted communications, and other NGINX App Protect modules for Layer 7 WAF and DoS app protection.

Learn how to manage connectivity to your Windows applications running on Windows nodes in a mixed-node AKS cluster with NGINX Ingress controller in this [blog](https://techcommunity.microsoft.com/t5/containers/improving-customer-experiences-with-f5-nginx-and-windows-on/ba-p/3820344).

### Calico

Tigera provides an active security platform with full-stack observability for containerized workloads and Microsoft AKS as a fully managed SaaS (Calico Cloud) or a self-managed service (Calico Enterprise). The platform prevents, detects, troubleshoots, and automatically mitigates exposure risks of security breaches for workloads in Microsoft AKS.

Its open-source offering, Calico Open Source, is the most widely adopted container networking and security solution. It specifies security and observability as code to ensure consistent enforcement of security policies, which enables DevOps, platform, and security teams to protect workloads, detect threats, achieve continuous compliance, and troubleshoot service issues in real-time.

For more information, see [Securing Windows workloads on Azure Kubernetes Service with Calico](https://techcommunity.microsoft.com/t5/containers/securing-windows-workloads-on-azure-kubernetes-service-with/ba-p/3815429).

## Observability

Observability provides deep insights into your systems, enabling rapid issue detection and resolution to enhance your application’s reliability and performance.

### Datadog

Datadog is the essential monitoring and security platform for cloud applications. We bring together end-to-end traces, metrics, and logs to make your applications, infrastructure, and third-party services entirely observable. Partner with Datadog for Windows on AKS environments to streamline monitoring, proactively resolve issues, and optimize application performance and availability.

Get started by following the recommendations in our [joint blog](https://techcommunity.microsoft.com/t5/containers/gain-full-observability-into-windows-containers-on-azure/ba-p/3853603).

### New Relic

New Relic's Azure Kubernetes integration is a powerful solution that seamlessly connects New Relic's monitoring and observability capabilities with Azure Kubernetes Service (AKS). By deploying the New Relic Kubernetes integration, users gain deep insights into their AKS clusters' performance, health, and resource utilization. This integration allows users to efficiently manage and troubleshoot containerized applications, optimize resource allocation, and proactively identify and resolve issues in their AKS environments. With New Relic's comprehensive monitoring and analysis tools, businesses can ensure the smooth operation and optimal performance of their Kubernetes workloads on Azure.

Check this [blog](https://techcommunity.microsoft.com/t5/containers/leveraging-new-relic-for-instrumentation-of-windows-container-on/ba-p/3870323) for detailed information.

## Security

Ensure the integrity and confidentiality of applications, thereby fostering trust and compliance across your infrastructure.

### Prisma Cloud

Prisma Cloud is a comprehensive Cloud-Native Application Protection Platform (CNAPP) tailor-made to help secure Windows containers on Azure Kubernetes Service (AKS). Gain continuous real-time visibility and control over Windows container environments, including vulnerability and compliance management, identities and permissions, and AI-assisted runtime defense. Integrated container scanning across the pipeline and in Azure Container Registry ensure security throughout the entire application lifecycle.

See [our guidance](https://techcommunity.microsoft.com/t5/containers/unlocking-new-possibilities-with-prisma-cloud-and-windows/ba-p/3866485) for more details.

## Storage

Storage enables standardized and seamless storage interactions, ensuring high application performance and data consistency.

### NetApp

[Astra](https://www.netapp.com/cloud-services/astra/) provides dynamic storage provisioning for stateful workloads on Azure Kubernetes Service (AKS). It also provides data protection using snapshots and clones. Provision SMB volumes through the Kubernetes control plane, making storage seamless and on-demand for all your Windows AKS workloads.

Follow the steps provided in [this blog](https://techcommunity.microsoft.com/t5/azure-architecture-blog/azure-netapp-files-smb-volumes-for-azure-kubernetes-services/ba-p/3052900) post to dynamically provision SMB volumes for Windows AKS workloads.

## Config management

Automate and standardize the system settings across your environments to enhance efficiency, reduce errors, and ensuring system stability and compliance.

### Chef

Chef provides visibility and threat detection from build to runtime that monitors, audits, and remediates the security of your Azure cloud services and Kubernetes and Windows container assets. Chef provides comprehensive visibility and continuous compliance into your cloud security posture and helps limit the risk of misconfigurations in cloud-native environments by providing best practices based on CIS, STIG, SOC2, PCI-DSS and other benchmarks. This is part of a broader compliance offering that supports on-premises or hybrid cloud environments including applications deployed on the edge.

To learn more about Chef’s capabilities, check out the comprehensive ‘how-to’ blog post here: [Securing Your Windows Environments Running on Azure Kubernetes Service with Chef](https://techcommunity.microsoft.com/t5/containers/securing-your-windows-environments-running-on-azure-kubernetes/ba-p/3821830).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-tags -->

# Use Azure tags in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

With Azure Kubernetes Service (AKS), you can set Azure tags on an AKS cluster and its related resources using Azure Resource Manager and the Azure CLI. You can also use Kubernetes manifests to set Azure tags for certain resources. Azure tags are a useful tracking resource for certain business processes, such as *chargeback*.

This article explains how to set Azure tags for AKS clusters and related resources.

## Before you begin

Review the following information before you begin:

- Tags set on an AKS cluster apply to all resources related to the cluster, but not the node pools. This operation overwrites the values of existing keys.
- Tags set on a node pool apply only to resources related to that node pool. This operation overwrites the values of existing keys. Resources outside that node pool, including resources for the rest of the cluster and other node pools, are unaffected.
- Public IPs, files, and disks can have tags set by Kubernetes through a Kubernetes manifest. Tags set in this way maintain the Kubernetes values, even if you update them later using a different method. When you remove public IPs, files, or disks through Kubernetes, any tags set by Kubernetes are removed. The tags on those resources that Kubernetes doesn't track remain unaffected.

### Prerequisites

- The Azure CLI version 2.0.59 or later. To find your version, run
`az --version`

. If you need to install it or update your version, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - Kubernetes version 1.20 or later.

### Limitations

- Azure tags have keys that are case-insensitive for operations, such as when you're retrieving a tag by searching the key. In this case, a tag with the specified key is updated or retrieved regardless of casing. Tag values are case-sensitive.
- In AKS, if multiple tags are set with identical keys but different casing, the tags are used in alphabetical order. For example,
`{"Key1": "val1", "kEy1": "val2", "key1": "val3"}`

results in`Key1`

and`val1`

being set. - For shared resources, tags can't determine the split in resource usage on their own.

## Azure tags and AKS clusters

When you create or update an AKS cluster with the `--tags`

parameter, the following are assigned the Azure tags that you specified:

- The AKS cluster itself and its related resources:
- Route table
- Public IP
- Load balancer
- Network security group
- Virtual network
- AKS-managed kubelet msi
- AKS-managed add-on msi
- Private DNS zone associated with the
*private cluster* - Private endpoint associated with the
*private cluster*

- The node resource group

Note

Azure Private DNS only supports 15 tags. For more information, see the [tag resources](/en-us/azure/azure-resource-manager/management/tag-resources).

## Create or update tags on an AKS cluster

### Create a new AKS cluster

Important

If you're using existing resources when you create a new cluster, such as an IP address or route table, the `az aks create`

command overwrites the set of tags. If you delete the cluster later, any tags set by the cluster are removed.

Create a cluster and assign Azure tags using the

command with the`az aks create`

`--tags`

parameter.Note

To set tags on the initial node pool, the virtual machine scale set, and each virtual machine scale set instance associated with the initial node pool, you can also set the

`--nodepool-tags`

parameter.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --tags dept=IT costcenter=9999 \ --generate-ssh-keys`

Verify the tags have been applied to the cluster and its related resources using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --query '[tags]'`

The following example output shows the tags applied to the cluster:

`{ "clusterTags": { "dept": "IT", "costcenter": "9999" } }`


### Update an existing AKS cluster

Important

Setting tags on a cluster using the `az aks update`

command overwrites the set of tags. For example, if your cluster has the tags *dept=IT* and *costcenter=9999*, and you use `az aks update`

with the tags *team=alpha* and *costcenter=1234*, the new list of tags would be *team=alpha* and *costcenter=1234*.

Update the tags on an existing cluster using the

command with the`az aks update`

`--tags`

parameter.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --tags team=alpha costcenter=1234`

Verify the tags have been applied to the cluster and its related resources using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --query '[tags]'`

The following example output shows the tags applied to the cluster:

`{ "clusterTags": { "team": "alpha", "costcenter": "1234" } }`


## Add tags to node pools

You can apply an Azure tag to a new or existing node pool in your AKS cluster. Tags applied to a node pool are applied to each node within the node pool and are persisted through upgrades. Tags are also applied to new nodes that are added to a node pool during scale-out operations. Adding a tag can help with tasks such as policy tracking or cost estimation.

When you create or update a node pool with the `--tags`

parameter, the tags you specify are assigned to the following resources:

- The node pool.
- The virtual machine scale set and each virtual machine scale set instance associated with the node pool.

### Create a new node pool

Create a node pool with an Azure tag using the

command with the`az aks nodepool add`

`--tags`

parameter.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name tagnodepool \ --node-count 1 \ --tags abtest=a costcenter=5555 \ --no-wait`

Verify that the tags have been applied to the node pool using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --query 'agentPoolProfiles[].{nodepoolName:name,tags:tags}'`

The following example output shows the tags applied to the node pool:

`[ { "nodepoolName": "nodepool1", "tags": null }, { "nodepoolName": "tagnodepool", "tags": { "abtest": "a", "costcenter": "5555" } } ]`


### Update an existing node pool

Important

Setting tags on a node pool using the `az aks nodepool update`

command overwrites the set of tags. For example, if your node pool has the tags *abtest=a* and *costcenter=5555*, and you use `az aks nodepool update`

with the tags *appversion=0.0.2* and *costcenter=4444*, the new list of tags would be *appversion=0.0.2* and *costcenter=4444*.

Update a node pool with an Azure tag using the

command.`az aks nodepool update`

`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name tagnodepool \ --tags appversion=0.0.2 costcenter=4444 \ --no-wait`

Verify the tags have been applied to the node pool using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --query 'agentPoolProfiles[].{nodepoolName:name,tags:tags}'`

The following example output shows the tags applied to the node pool:

`[ { "nodepoolName": "nodepool1", "tags": null }, { "nodepoolName": "tagnodepool", "tags": { "appversion": "0.0.2", "costcenter": "4444" } } ]`


## Add tags using Kubernetes

Important

Setting tags on files, disks, and public IPs using Kubernetes updates the set of tags. For example, if your disk has the tags *dept=IT* and *costcenter=5555*, and you use Kubernetes to set the tags *team=beta* and *costcenter=3333*, the new list of tags would be *dept=IT*, *team=beta*, and *costcenter=3333*.

Any updates you make to tags through Kubernetes retain the value set through Kubernetes. For example, if your disk has tags *dept=IT* and *costcenter=5555* set by Kubernetes, and you use the portal to set the tags *team=beta* and *costcenter=3333*, the new list of tags would be *dept=IT*, *team=beta*, and *costcenter=5555*. If you then remove the disk through Kubernetes, the disk would have the tag *team=beta*.

You can apply Azure tags to public IPs, disks, and files using a Kubernetes manifest.

For public IPs, use

*service.beta.kubernetes.io/azure-pip-tags*under*annotations*. For example:`apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-pip-tags: costcenter=3333,team=beta spec: ...`

For files and disks, use

*tags*under*parameters*. For example:`--- apiVersion: storage.k8s.io/v1 ... parameters: ... tags: costcenter=3333,team=beta ...`


## Next steps

Learn more about [using labels in an AKS cluster](use-labels).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/cluster-container-registry-integration -->

# Authenticate with Azure Container Registry (ACR) from Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When using [Azure Container Registry (ACR)](/en-us/azure/container-registry/container-registry-intro) with Azure Kubernetes Service (AKS), you need to establish an authentication mechanism. You can configure the required permissions between ACR and AKS using the Azure CLI, Azure PowerShell, or Azure portal. This article provides examples to configure authentication between these Azure services using the Azure CLI or Azure PowerShell.

The AKS to ACR integration assigns the [ AcrPull role](/en-us/azure/role-based-access-control/built-in-roles#acrpull) to the

[Microsoft Entra ID](/en-us/azure/active-directory/managed-identities-azure-resources/overview)associated with the agent pool in your AKS cluster. For more information on AKS managed identities, see

**managed identity**[Summary of managed identities](managed-identity-overview#summary-of-managed-identities-used-by-aks).

Important

There's a latency issue with Microsoft Entra groups when attaching ACR. If the **AcrPull** role is granted to a Microsoft Entra group and the kubelet identity is added to the group to complete the RBAC configuration, there may be a delay before the RBAC group takes effect. If you're running automation that requires the RBAC configuration to be complete, we recommend you use [Bring your own kubelet identity](use-managed-identity#create-a-kubelet-managed-identity) as a workaround. You can pre-create a user-assigned identity, add it to the Microsoft Entra group, then use the identity as the kubelet identity to create an AKS cluster. This ensures the identity is added to the Microsoft Entra group before a token is generated by kubelet, which avoids the latency issue.

Note

This article covers automatic authentication between AKS and ACR. If you need to pull an image from a private external registry, use an [image pull secret](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/).

Caution

The AKS-ACR integration through `az aks --attach-acr`

is not supported for ABAC-enabled ACR registries where the role assignment permissions mode is set to "RBAC Registry + ABAC Repository Permissions." ABAC-enabled ACR registries require the [ Container Registry Repository Reader role](/en-us/azure/role-based-access-control/built-in-roles#container-registry-repository-reader) instead of the

`AcrPull`

role for granting image pull permissions. For ABAC-enabled ACR registries, you should not use `az aks --attach-acr`

but instead manually assign the `Container Registry Repository Reader`

role assignment using either the Azure Portal, `az role assignment`

CLI, or Azure Resource Manager. Please visit [https://aka.ms/acr/auth/abac](https://aka.ms/acr/auth/abac)for more information on ABAC-enabled ACR registries.

## Before you begin

- You need the
,**Owner**, or**Azure account administrator**role on your Azure subscription.**Azure co-administrator**- To avoid needing one of these roles, you can instead use an existing managed identity to authenticate ACR from AKS. For more information, see
[Use an Azure managed identity to authenticate to an ACR](/en-us/azure/container-registry/container-registry-authentication-managed-identity).

- To avoid needing one of these roles, you can instead use an existing managed identity to authenticate ACR from AKS. For more information, see
- If you're using Azure CLI, this article requires that you're running Azure CLI version 2.7.0 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you're using Azure PowerShell, this article requires that you're running Azure PowerShell version 5.9.0 or later. Run
`Get-InstalledModule -Name Az`

to find the version. If you need to install or upgrade, see[Install Azure PowerShell](/en-us/powershell/azure/install-az-ps). - Examples and syntax to use Terraform for configuring ACR can be found in the
[Terraform reference](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/container_registry).

## Create a new ACR

If you don't already have an ACR, create one using the

command. The following example sets the`az acr create`

`MYACR`

variable to the name of the ACR,*mycontainerregistry*, and uses the variable to create the registry. Your ACR name must be globally unique and use only lowercase letters.`MYACR=mycontainerregistry az acr create --name $MYACR --resource-group myContainerRegistryResourceGroup --sku basic`


## Create a new AKS cluster and integrate with an existing ACR

Create a new AKS cluster and integrate with an existing ACR using the

command with the`az aks create`

. This command allows you to authorize an existing ACR in your subscription and configures the appropriate`--attach-acr`

parameter**AcrPull**role for the managed identity.`MYACR=mycontainerregistry az aks create --name myAKSCluster --resource-group myResourceGroup --generate-ssh-keys --attach-acr $MYACR`

This command may take several minutes to complete.

Note

If you're using an ACR located in a different subscription from your AKS cluster or would prefer to use the ACR

*resource ID*instead of the ACR name, you can do so using the following syntax:`az aks create -n myAKSCluster -g myResourceGroup --generate-ssh-keys --attach-acr /subscriptions/<subscription-id>/resourceGroups/myContainerRegistryResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry`


## Configure ACR integration for an existing AKS cluster

### Attach an ACR to an existing AKS cluster

Integrate an existing ACR with an existing AKS cluster using the

command with the`az aks update`

and a valid value for`--attach-acr`

parameter**acr-name**or**acr-resource-id**.`# Attach using acr-name az aks update --name myAKSCluster --resource-group myResourceGroup --attach-acr <acr-name> # Attach using acr-resource-id az aks update --name myAKSCluster --resource-group myResourceGroup --attach-acr <acr-resource-id>`

Note

The

`az aks update --attach-acr`

command uses the permissions of the user running the command to create the ACR role assignment. This role is assigned to the[kubelet](https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/)managed identity. For more information on AKS managed identities, see[Summary of managed identities](managed-identity-overview#summary-of-managed-identities-used-by-aks).

### Detach an ACR from an AKS cluster

Remove the integration between an ACR and an AKS cluster using the

command with the`az aks update`

and a valid value for`--detach-acr`

parameter**acr-name**or**acr-resource-id**.`# Detach using acr-name az aks update --name myAKSCluster --resource-group myResourceGroup --detach-acr <acr-name> # Detach using acr-resource-id az aks update --name myAKSCluster --resource-group myResourceGroup --detach-acr <acr-resource-id>`


## Working with ACR & AKS

### Import an image into your ACR

Import an image from Docker Hub into your ACR using the

command.`az acr import`

`az acr import --name <acr-name> --source docker.io/library/nginx:latest --image nginx:v1`


### Deploy the sample image from ACR to AKS

Ensure you have the proper AKS credentials using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Create a file called

**acr-nginx.yaml**using the following sample YAML and replace**acr-name**with the name of your ACR.`apiVersion: apps/v1 kind: Deployment metadata: name: nginx0-deployment labels: app: nginx0-deployment spec: replicas: 2 selector: matchLabels: app: nginx0 template: metadata: labels: app: nginx0 spec: containers: - name: nginx image: <acr-name>.azurecr.io/nginx:v1 ports: - containerPort: 80`

Run the deployment in your AKS cluster using the

`kubectl apply`

command.`kubectl apply -f acr-nginx.yaml`

Monitor the deployment using the

`kubectl get pods`

command.`kubectl get pods`

The output should show two running pods, as shown in the following example output:

`NAME READY STATUS RESTARTS AGE nginx0-deployment-669dfc4d4b-x74kr 1/1 Running 0 20s nginx0-deployment-669dfc4d4b-xdpd6 1/1 Running 0 20s`


### Troubleshooting

- Validate the registry is accessible from the AKS cluster using the
command.`az aks check-acr`

- Learn more about
[ACR monitoring](/en-us/azure/container-registry/monitor-service). - Learn more about
[ACR health](/en-us/azure/container-registry/container-registry-check-health).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-trusted-launch -->

# Trusted Launch for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Trusted Launch](/en-us/azure/virtual-machines/trusted-launch) improves the security of generation 2 virtual machines (VMs) by protecting against advanced and persistent attack techniques. It enables administrators to deploy AKS nodes, which contain the underlying virtual machines, with verified and signed bootloaders, OS kernels, and drivers. By using secure and measured boot, administrators gain insights and confidence of the entire boot chain's integrity.

This article helps you understand this new feature, and how to implement it.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Overview

Trusted Launch is composed of several, coordinated infrastructure technologies that can be enabled independently. Each technology provides another layer of defense against sophisticated threats.

**vTPM**- Trusted Launch introduces a virtualized version of a hardware[Trusted Platform Module](/en-us/windows/security/information-protection/tpm/trusted-platform-module-overview)(TPM), compliant with the TPM 2.0 specification. It serves as a dedicated secure vault for keys and measurements. Trusted Launch provides your VM with its own dedicated TPM instance, running in a secure environment outside the reach of any VM. The vTPM enables[attestation](/en-us/windows/security/information-protection/tpm/tpm-fundamentals#measured-boot-with-support-for-attestation)by measuring the entire boot chain of your VM (UEFI, OS, system, and drivers). Trusted Launch uses the vTPM to perform remote attestation by the cloud. It's used for platform health checks and for making trust-based decisions. As a health check, Trusted Launch can cryptographically certify that your VM booted correctly. If the process fails, possibly because your VM is running an unauthorized component,[Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/defender-for-cloud-introduction)issues integrity alerts. The alerts include details on which components failed to pass integrity checks.**Secure Boot**- At the root of Trusted Launch is Secure Boot for your VM. This mode, which is implemented in platform firmware, protects against the installation of malware-based rootkits and boot kits. Secure Boot works to ensure that only signed operating systems and drivers can boot. It establishes a "root of trust" for the software stack on your VM. With Secure Boot enabled, all OS boot components (boot loader, kernel, kernel drivers) must be signed by trusted publishers. Both Windows and select Linux distributions support Secure Boot. If Secure Boot fails to authenticate an image signed by a trusted publisher, the VM isn't allowed to boot. For more information, see[Secure Boot](/en-us/windows-hardware/design/device-experiences/oem-secure-boot).

## Before you begin

- The Azure CLI version 2.66.0 or later. Run
`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

- Secure Boot requires signed boot loaders, OS kernels, and drivers.

## Limitations

- AKS supports Trusted Launch on kubernetes version 1.25.2 and higher.
- Trusted Launch only supports
[Azure Generation 2 VMs](/en-us/azure/virtual-machines/generation-2). - Node pools with Windows Server operating system aren't supported.
- Trusted Launch can't be enabled in the same node pool as
[FIPS](enable-fips-nodes),[Arm64](use-arm64-vms),[Pod Sandboxing](use-pod-sandboxing), or[Confidential VM](use-cvm). For more information, see[node images documentation](node-images). - Trusted Launch doesn't support virtual node.
- Availability sets aren't supported, only Virtual Machine Scale Sets.
- To enable Secure Boot on GPU node pools, you need to skip installing the GPU driver. For more information, see
[Skip GPU driver installation](gpu-cluster#skip-gpu-driver-installation). - Ephemeral OS disks can be created with trusted Launch and all regions are supported. However, not all virtual machines sizes are supported. For more information, see
[Trusted Launch ephemeral OS sizes](/en-us/azure/virtual-machines/ephemeral-os-disks#trusted-launch-for-ephemeral-os-disks). [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks)doesn't support Trusted Launch on AKS.

## Create an AKS cluster with Trusted Launch enabled

When creating a cluster, enabling vTPM or Secure Boot automatically sets up your node pools to use the customized Trusted Launch image. This image is specifically configured to support the security features enabled by Trusted Launch.

Create an AKS cluster using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command. Before running the command, review the following parameters:**--name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--resource-group**: Enter the name of an existing resource group to host the AKS cluster resource.**--enable-secure-boot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**--enable-vtpm**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

Note

Secure Boot requires signed boot loaders, OS kernels, and drivers. If after enabling Secure Boot your nodes don't start, you can verify which boot components are responsible for Secure Boot failures within an Azure Linux Virtual Machine. See

[verify Secure Boot failures](/en-us/azure/virtual-machines/trusted-launch-faq#verify-secure-boot-failures).The following example creates a cluster named

*myAKSCluster*with one node in the*myResourceGroup*, and enables Secure Boot and vTPM:`az aks create \ --name myAKSCluster \ --resource-group myResourceGroup \ --node-count 1 \ --enable-secure-boot \ --enable-vtpm \ --generate-ssh-keys`

Run the following command to get access credentials for the Kubernetes cluster. Use the

[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command and replace the values for the cluster name and the resource group name.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


Create a template with Trusted Launch parameters. Before creating the template, review the following parameters:

**enableSecureBoot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**enableVTPM**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

In your template, provide values for

`enableVTPM`

and`enableSecureBoot`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters/agentPools`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "securityProfile": { "enableVTPM": "true", "enableSecureBoot": "true", } }`

Deploy your template with vTPM and secure boot enabled on your cluster. See

[Deploy an AKS cluster using an ARM template](/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template)for detailed instructions.

## Add a node pool with Trusted Launch enabled

When you create a node pool, enabling vTPM or Secure Boot automatically sets up your node pools to use the customized Trusted Launch image. This image is specifically configured to support the security features enabled by Trusted Launch.

Add a node pool with Trusted Launch enabled using the

command. Before running the command, review the following parameters:`az aks nodepool add`

**--cluster-name**: Enter the name of the AKS cluster.**--resource-group**: Enter the name of an existing resource group to host the AKS cluster resource.**--name**: Enter a unique name for the node pool. The name of a node pool can only contain lowercase alphanumeric characters and must begin with a lowercase letter. For Linux node pools, the length must be between 1-11 characters.**--node-count**: The number of nodes in the Kubernetes agent pool. Default is 3.**--enable-secure-boot**: Enables Secure Boot to authenticate image signed by a trusted publisher.**--enable-vtpm**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

Note

Secure Boot requires signed boot loaders, OS kernels, and drivers. If after enabling Secure Boot your nodes don't start, you can verify which boot components are responsible for Secure Boot failures within an Azure Linux Virtual Machine. See

[verify Secure Boot failures](/en-us/azure/virtual-machines/trusted-launch-faq#verify-secure-boot-failures).The following example deploys a node pool with vTPM and Secure Boot enabled on a cluster named

*myAKSCluster*with three nodes:`az aks nodepool add --resource-group myResourceGroup --cluster-name myAKSCluster --name mynodepool --node-count 3 --enable-vtpm --enable-secure-boot`

Check that your node pool is using a Trusted Launch image.

Trusted Launch nodes have the following output:

- Node image version containing
`"TL"`

, such as`"AKSUbuntu-2204-gen2TLcontainerd"`

. `"Security-type"`

should be`"Trusted Launch"`

.

`kubectl get nodes kubectl describe node {node-name} | grep -e node-image-version -e security-type`

- Node image version containing

Create a template with Trusted Launch parameters. Before creating the template, review the following parameters:

**enableSecureBoot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**enableVTPM**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

In your template, provide values for

`enableVTPM`

and`enableSecureBoot`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters/agentPools`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "securityProfile": { "enableVTPM": "true", "enableSecureBoot": "true", } }`

Deploy your template with vTPM and secure boot enabled on your cluster. See

[Deploy an AKS cluster using an ARM template](/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template)for detailed instructions.

## Enable vTPM or secure boot on an existing Trusted Launch node pool

You can update an existing Trusted Launch node pool to enable vTPM or secure boot. The following scenarios are supported:

- When creating a node pool, you only specify
`--enable-secure-boot`

, you can run the update command to`--enable-vtpm`

- When creating a node pool, you only specify
`--enable-vtpm`

, you can run the update command to`--enable-secure-boot`


If your node pool doesn't currently have a Trusted Launch image, you won't be able to update the node pool to enable secure boot or vTPM.

Check that your node pool is using a Trusted Launch image.

Trusted Launch nodes have the following output:

- Node image version containing
`"TL"`

, such as`"AKSUbuntu-2204-gen2TLcontainerd"`

. `"Security-type"`

should be`"Trusted Launch"`

.

`kubectl get nodes kubectl describe node {node-name} | grep -e node-image-version -e security-type`

If your node pool doesn't currently have a Trusted Launch image, you won't be able to update the node pool to enable secure boot or vTPM.

- Node image version containing
Update a node pool with Trusted Launch enabled using the

command. Before running the command, review the following parameters:`az aks nodepool update`

**--resource-group**: Enter the name of an existing resource group hosting your existing AKS cluster.**--cluster-name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--name**: Enter the name of your node pool, such as*mynodepool*.**--enable-secure-boot**: Enables Secure Boot to authenticate that the image was signed by a trusted publisher.**--enable-vtpm**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

Note

Secure Boot requires signed boot loaders, OS kernels, and drivers. If after enabling Secure Boot your nodes don't start, you can verify which boot components are responsible for Secure Boot failures within an Azure Linux Virtual Machine. See

[verify Secure Boot failures](/en-us/azure/virtual-machines/trusted-launch-faq#verify-secure-boot-failures).The following example updates the node pool

*mynodepool*on the*myAKSCluster*in the*myResourceGroup*, and enables vTPM. In this scenario, secure boot was enabled during node pool creation:`az aks nodepool update --cluster-name myCluster --resource-group myResourceGroup --name mynodepool --enable-vtpm`

The following example updates the node pool

*mynodepool*on the*myAKSCluster*in the*myResourceGroup*, and enables secure boot. In this scenario, vTPM was enabled during node pool creation:`az aks nodepool update --cluster-name myCluster --resource-group myResourceGroup --name mynodepool --enable-secure-boot`


Check that your node pool is using a Trusted Launch image.

Trusted Launch nodes have the following output:

- Node image version containing
`"TL"`

, such as`"AKSUbuntu-2204-gen2TLcontainerd"`

. `"Security-type"`

should be`"Trusted Launch"`

.

`kubectl get nodes kubectl describe node {node-name} | grep -e node-image-version -e security-type`

If your node pool doesn't currently have a Trusted Launch image, you won't be able to update the node pool to enable secure boot or vTPM.

- Node image version containing
Create a template with Trusted Launch parameters. Before creating the template, review the following parameters:

**enableSecureBoot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**enableVTPM**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

In your template, provide values for

`enableVTPM`

and`enableSecureBoot`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters/agentPools`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "securityProfile": { "enableVTPM": "true", "enableSecureBoot": "true", } }`

Deploy your template with vTPM and secure boot enabled on your cluster. See

[Deploy an AKS cluster using an ARM template](/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template)for detailed instructions.

## Assign pods to nodes with Trusted Launch enabled

You can constrain a pod and restrict it to run on a specific node or nodes, or preference to nodes with Trusted Launch enabled. You can control this using the following node pool selector in your pod manifest.

```
spec:
nodeSelector:
kubernetes.azure.com/security-type = "TrustedLaunch"
```


## Disable vTPM or secure boot on an existing Trusted Launch node pool

You can update an existing node pool to disable vTPM or secure boot. When this occurs, you'll still remain on the Trusted Launch image. You can re-enable vTPM or secure boot at any time by updating your node pool.

Update a node pool to disable secure boot or vTPM using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. Before running the command, review the following parameters:

**--resource-group**: Enter the name of an existing resource group hosting your existing AKS cluster.**--cluster-name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--name**: Enter the name of your node pool, such as*mynodepool*.**--enable-secure-boot**: Enables Secure Boot to authenticate that the image was signed by a trusted publisher.**--enable-vtpm**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

To disable vTPM on an existing node pool:

```
az aks nodepool update --cluster-name myCluster --resource-group myResourceGroup --name mynodepool --disable-vtpm
```


To disable secure boot on an existing node pool:

```
az aks nodepool update --cluster-name myCluster --resource-group myResourceGroup --name mynodepool --disable-secure-boot
```


Create a template with Trusted Launch parameters. Before creating the template, review the following parameters:

**enableSecureBoot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**enableVTPM**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

In your template, provide values for

`enableVTPM`

and`enableSecureBoot`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters/agentPools`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "securityProfile": { "enableVTPM": "false", "enableSecureBoot": "false", } }`

Deploy your template with vTPM and secure boot disabled on your cluster. See

[Deploy an AKS cluster using an ARM template](/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template)for detailed instructions.

## Next steps

In this article, you learned how to enable Trusted Launch. Learn more about [Trusted Launch](/en-us/azure/virtual-machines/trusted-launch).
