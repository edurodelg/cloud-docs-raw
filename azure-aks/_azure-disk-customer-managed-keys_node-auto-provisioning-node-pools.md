---
merged_at: 2026-01-25T12:25:33.933532
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: azure-disk-customer-managed-keys.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-disk-customer-managed-keys -->

# Bring your own keys (BYOK) with Azure managed disks in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure encrypts all data in a managed disk at rest. By default, data is encrypted with Microsoft-managed keys. For more control over encryption keys, you can supply customer-managed keys to use for encryption at rest for both the OS and data disks for your AKS clusters.

Learn more about customer-managed keys on [Linux](/en-us/azure/virtual-machines/disk-encryption#customer-managed-keys) and [Windows](/en-us/azure/virtual-machines/disk-encryption#customer-managed-keys).

## Prerequisites

- You must enable soft delete and purge protection for
*Azure Key Vault*when using Key Vault to encrypt managed disks. - You need the Azure CLI version 2.11.1 or later.
- Data disk encryption and customer-managed keys are supported on Kubernetes versions 1.24 and higher.
- If you choose to rotate (change) your keys periodically, see
[Customer-managed keys and encryption of Azure managed disk](/en-us/azure/virtual-machines/disk-encryption)for more information.

## Limitations

Encryption of an OS disk with customer-managed keys can only be enabled when creating an AKS cluster.

Virtual nodes are not supported.

When encrypting an ephemeral OS disk-enabled node pool with customer-managed keys, if you want to rotate the key in Azure Key Vault, there are two options to consider:

Immediate usage of new CMK

- Scale down the node pool count to 0.
- Rotate the key.
- Scale up the node pool to the original count.

Gradual usage of new CMK

- Allow AKS node image upgrades or version upgrades to naturally adopt the new CMK over time.
- Until all nodes in the pool are upgraded, the existing CMK will continue to function without disruption.
- Once the upgrade process is complete across all nodes, the new CMK takes effect seamlessly.


## Create an Azure Key Vault instance

Use an Azure Key Vault instance to store your keys. You can optionally use the Azure portal to [Configure customer-managed keys with Azure Key Vault](/en-us/azure/storage/common/customer-managed-keys-configure-key-vault)

Create a new *resource group*, then create a new *Key Vault* instance and enable soft delete and purge protection. Ensure you use the same region and resource group names for each command.

```
# Optionally retrieve Azure region short names for use on upcoming commands
az account list-locations
```


```
# Create new resource group in a supported Azure region
az group create --location myAzureRegionName --name myResourceGroup
# Create an Azure Key Vault resource in a supported Azure region
az keyvault create --name myKeyVaultName --resource-group myResourceGroup --location myAzureRegionName --enable-purge-protection true
```


## Create an instance of a DiskEncryptionSet

Replace *myKeyVaultName* with the name of your key vault. You also need a *key* stored in Azure Key Vault to complete the following steps. Either store your existing Key in the Key Vault you created on the previous steps, or [generate a new key](/en-us/azure/key-vault/general/manage-with-cli2) and replace *myKeyName* with the name of your key.

Note

For cross-account access support for customer-managed encryption keys, you need to create the DiskEncryptionSet for cross-tenant customer-managed keys as detailed in [this guide](/en-us/azure/virtual-machines/disks-cross-tenant-customer-managed-keys?tabs=azure-cli#create-a-disk-encryption-set). The remaining storage class configuration is the same as normal customer managed keys.

```
# Retrieve the Key Vault Id and store it in a variable
keyVaultId=$(az keyvault show --name myKeyVaultName --query "[id]" -o tsv)
# Retrieve the Key Vault key URL and store it in a variable
keyVaultKeyUrl=$(az keyvault key show --vault-name myKeyVaultName --name myKeyName --query "[key.kid]" -o tsv)
# Create a DiskEncryptionSet
az disk-encryption-set create --name myDiskEncryptionSetName --location myAzureRegionName --resource-group myResourceGroup --source-vault $keyVaultId --key-url $keyVaultKeyUrl
```


Important

Make sure that the DiskEncryptionSet is located in the same region as your AKS cluster and that the AKS cluster identity has **read** access to the DiskEncryptionSet.

## Grant the DiskEncryptionSet access to key vault

Use the DiskEncryptionSet and resource groups you created on the prior steps, and grant the DiskEncryptionSet resource access to the Azure Key Vault.

```
# Retrieve the DiskEncryptionSet value and set a variable
desIdentity=$(az disk-encryption-set show --name myDiskEncryptionSetName --resource-group myResourceGroup --query "[identity.principalId]" -o tsv)
# Update security policy settings
az keyvault set-policy --name myKeyVaultName --resource-group myResourceGroup --object-id $desIdentity --key-permissions wrapkey unwrapkey get
```


## Create a new AKS cluster and encrypt the OS disk

Either create a new resource group, or select an existing resource group hosting other AKS clusters, then use your key to encrypt either using network-attached OS disks or ephemeral OS disk. By default, a cluster uses ephemeral OS disk when possible in conjunction with VM size and OS disk size.

Run the following command to retrieve the DiskEncryptionSet value and set a variable:

```
diskEncryptionSetId=$(az disk-encryption-set show --name mydiskEncryptionSetName --resource-group myResourceGroup --query "[id]" -o tsv)
```


If you want to create a new resource group for the cluster, run the following command:

```
az group create --name myResourceGroup --location myAzureRegionName
```


To create a regular cluster using network-attached OS disks encrypted with your key, you can do so by specifying the `--node-osdisk-type=Managed`

argument.

```
az aks create --name myAKSCluster --resource-group myResourceGroup --node-osdisk-diskencryptionset-id $diskEncryptionSetId --generate-ssh-keys --node-osdisk-type Managed
```


To create a cluster with ephemeral OS disk encrypted with your key, you can do so by specifying the `--node-osdisk-type=Ephemeral`

argument. You also need to specify the argument `--node-vm-size`

because the default vm size is too small and doesn't support ephemeral OS disk.

```
az aks create --name myAKSCluster --resource-group myResourceGroup --node-osdisk-diskencryptionset-id $diskEncryptionSetId --generate-ssh-keys --node-osdisk-type Ephemeral --node-vm-size Standard_DS3_v2
```


When new node pools are added to the cluster, the customer-managed key provided during the create process is used to encrypt the OS disk. The following example shows how to deploy a new node pool with an ephemeral OS disk.

```
az aks nodepool add --cluster-name $CLUSTER_NAME --resource-group $RG_NAME --name $NODEPOOL_NAME --node-osdisk-type Ephemeral
```


Important

The DiskEncryptionSet we previously applied to the storage class only encrypts new PVCs. Encrypting existing PVCs requires detaching first before using the Azure Disks API/CLI to update the underlying disks, as shown in [this related guide](/en-us/azure/virtual-machines/linux/disks-enable-customer-managed-keys-cli#encrypt-existing-managed-disks).

## Encrypt your AKS cluster data disk

If you have already provided a disk encryption set during cluster creation, encrypting data disks with the same disk encryption set is the default option. Therefore, this step is optional. However, if you want to encrypt data disks with a different disk encryption set, you can follow these steps.

Important

Ensure you have the proper AKS credentials. The managed identity needs to have contributor access to the resource group where the diskencryptionset is deployed. Otherwise, you'll get an error suggesting that the managed identity does not have permissions.

To assign the AKS cluster identity the Contributor role for the diskencryptionset, execute the following commands:

```
aksIdentity=$(az aks show --resource-group $RG_NAME --name $CLUSTER_NAME --query "identity.principalId")
az role assignment create --role "Contributor" --assignee $aksIdentity --scope $diskEncryptionSetId
```


Create a file called **byok-azure-disk.yaml** that contains the following information. Replace *myAzureSubscriptionId*, *myResourceGroup*, and *myDiskEncrptionSetName* with your values, and apply the yaml. Make sure to use the resource group where your DiskEncryptionSet is deployed.

```
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
name: byok
provisioner: disk.csi.azure.com # replace with "kubernetes.io/azure-disk" if aks version is less than 1.21
parameters:
skuname: StandardSSD_LRS
kind: managed
diskEncryptionSetID: "/subscriptions/{myAzureSubscriptionId}/resourceGroups/{myResourceGroup}/providers/Microsoft.Compute/diskEncryptionSets/{myDiskEncryptionSetName}"
```


Next, run the following commands to update your AKS cluster:

```
# Get credentials
az aks get-credentials --name myAksCluster --resource-group myResourceGroup --output table
# Update cluster
kubectl apply -f byok-azure-disk.yaml
```


---

<!-- DOCUMENTO FUSIONADO: node-auto-provisioning-node-pools.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-node-pools -->

# Configure node pools for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure node pools for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS), including SKU selectors, resource limits, and priority weights. It also provides examples to help you get started.

## Overview of node pools in NAP

NAP uses virtual machine (VM) SKU requirements to decide the best VMs for pending workloads. You can configure:

- SKU families and specific instance types.
- Resource limits and priorities.
- Spot or On-demand instances.
- Architecture and capabilities requirements.

The `NodePool`

resource sets constraints on the nodes that NAP creates and the pods that run on those nodes. When you first install NAP, it creates a [default NodePool](#review-default-node-pool-configuration). You can modify this node pool or create extra node pools to suit your workload requirements.

## Key behaviors of `NodePools`

in NAP

When configuring `NodePools`

for NAP, keep the following behaviors in mind:

- NAP requires at least one
`NodePool`

to function. - NAP evaluates each configured
`NodePool`

. - NAP skips
`NodePools`

with taints not tolerated by a pod. - NAP applies startup taints to provisioned nodes but doesn't require pod toleration.
- NAP works best with mutually exclusive
`NodePools`

. When multiple`NodePools`

match, it uses the one with highest weight.

## Review default node pool configuration

The configuration of the default [Karpenter NodePool](https://karpenter.sh/docs/concepts/nodepools/) named

`default`

created by NAP is as follows:```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
disruption:
consolidationPolicy: WhenEmptyOrUnderutilized
template:
spec:
nodeClassRef:
name: default
expireAfter: Never
# Requirements that constrain the parameters of provisioned nodes.
# These requirements are combined with pod.spec.affinity.nodeAffinity rules.
# Operators { In, NotIn, Exists, DoesNotExist, Gt, and Lt } are supported.
# https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#operators
requirements:
- key: kubernetes.io/arch
operator: In
values:
- amd64
- key: kubernetes.io/os
operator: In
values:
- linux
- key: karpenter.sh/capacity-type
operator: In
values:
- on-demand
- key: karpenter.azure.com/sku-family
operator: In
values:
- D
```


It also creates a `system-surge`

node pool, which helps to autoscale system pool nodes.

## Control configuration of default node pool during cluster creation

When you [create a new AKS cluster enabled with NAP using the Azure CLI](use-node-auto-provisioning#enable-nap-on-a-new-cluster), you can include the `--node-provisioning-default-pools`

flag to control the configuration of the default NAP `NodePool`

.

The `--node-provisioning-default-pools`

flag controls the default NAP `NodePool`

configuration and accepts the following values:

(default): Creates two standard`Auto`

`NodePools`

for immediate use.: Doesn't create any`None`

`NodePools`

. You must define your own.

Warning

**Changing from Auto to None**: If you change the setting from


`Auto`

to `None`

on an existing cluster, the default `NodePools`

aren't deleted automatically. You must delete them manually if you no longer need them.## Node pool configuration options

The following sections outline various configuration options for `NodePools`

in NAP, including [well-known labels and SKU selectors](#well-known-labels-and-sku-selectors), [node pool limits](#node-pool-limits), and [node pool weights](#node-pool-weights).

### Well-known labels and SKU selectors

Kubernetes defines [well-known labels](https://kubernetes.io/docs/reference/labels-annotations-taints/) that Azure implements. You can define these labels in the `spec.requirements`

section of the `NodePool`

API. NAP also supports Azure-specific labels for more advanced scheduling.

`karpenter.azure.com`

SKU selectors

The following table lists the `karpenter.azure.com`

SKU selectors you can use in the `spec.requirements`

section of your `NodePool`

API to define VM characteristics for your nodes:

| Selector | Description | Example |
|---|---|---|
`karpenter.azure.com/sku-family` |
VM SKU family | D, F, L, etc. |
`karpenter.azure.com/sku-name` |
Explicit SKU name | Standard_A1_v2 |
`karpenter.azure.com/sku-version` |
SKU version (without "v", can use 1) | 1, 2 |
`karpenter.sh/capacity-type` |
VM allocation type (Spot / On-demand) | Spot |
`karpenter.azure.com/sku-cpu` |
Number of CPUs in VM | 16 |
`karpenter.azure.com/sku-memory` |
Memory in VM in MiB | 131072 |
`kubernetes.azure.com/sku-cpu` |
Number of CPUs in VM | 16 |
`kubernetes.azure.com/sku-memory` |
Memory in VM in MiB | 131072 |
`karpenter.azure.com/sku-gpu-name` |
GPU name | A100 |
`karpenter.azure.com/sku-gpu-manufacturer` |
GPU manufacturer | nvidia |
`karpenter.azure.com/sku-gpu-count` |
GPU count per VM | 2 |
`karpenter.azure.com/sku-networking-accelerated` |
Whether the VM has accelerated networking | [true, false] |
`karpenter.azure.com/sku-storage-premium-capable` |
Whether the VM supports Premium IO storage | [true, false] |
`karpenter.azure.com/sku-storage-ephemeralos-maxsize` |
Size limit for the Ephemeral operating system (OS) disk in Gb | 92 |

`kubernetes.io`

well-known labels

The following table lists the `kubernetes.io`

well-known labels you can use in the `spec.requirements`

section of your `NodePool`

API to define node characteristics for your nodes:

| Label | Description | Example |
|---|---|---|
`topology.kubernetes.io/zone` |
Availability zone(s) | [uksouth-1,uksouth-2,uksouth-3] |
`kubernetes.io/os` |
Operating system | linux |
`kubernetes.io/arch` |
CPU architecture (AMD64 or ARM64) | [amd64, arm64] |

#### SKU family examples

The `karpenter.azure.com/sku-family`

selector allows you to target specific VM families.

| Family | Description |
|---|---|
| D-series | General-purpose VMs with balanced CPU-to-memory ratio |
| F-series | Compute-optimized VMs with high CPU-to-memory ratio |
| E-series | Memory-optimized VMs for memory-intensive applications |
| L-series | Storage-optimized VMs with high disk throughput |
| N-series | GPU-enabled VMs for compute-intensive workloads |

Example configuration using SKU family:

```
requirements:
- key: karpenter.azure.com/sku-family
operator: In
values:
- D
- F
```


#### SKU name examples

The `karpenter.azure.com/sku-name`

selector allows you to specify the exact VM instance type.

```
requirements:
- key: karpenter.azure.com/sku-name
operator: In
values:
- Standard_D4s_v3
- Standard_F8s_v2
```


#### SKU version examples

The `karpenter.azure.com/sku-version`

selector targets specific generations of VM SKUs.

```
requirements:
- key: karpenter.azure.com/sku-version
operator: In
values:
- "3" # v3 generation
- "5" # v5 generation
```


#### Availability zone example

The `topology.kubernetes.io/zone`

selector allows you to specify the availability zones for your nodes.

```
requirements:
- key: topology.kubernetes.io/zone
operator: In
values:
- eastus-1
- eastus-2
```


Note

You can find available zones for your region using the `az account list-locations --output table`

Azure CLI command.

#### Architecture example

The `kubernetes.io/arch`

selector allows you to specify the CPU architecture for your nodes. NAP supports both `amd64`

and `arm64`

nodes.

```
requirements:
- key: kubernetes.io/arch
operator: In
values:
- amd64
- arm64
```


#### OS example

The `kubernetes.io/os`

selector allows you to specify the operating system for your nodes.

```
requirements:
- key: kubernetes.io/os
operator: In
values:
- linux
```


#### Capacity type example

The `karpenter.sh/capacity-type`

selector allows you to specify whether to use Spot or On-demand instances.

Note

NAP prioritizes Spot instances when both Spot and On-demand are specified.

```
requirements:
- key: karpenter.sh/capacity-type
operator: In
values:
- spot
- on-demand
```


### Node pool limits

By default, NAP attempts to schedule your workloads within the Azure quota you have available. You can also specify the upper limit of resources that a node pool uses by specifying limits within the node pool spec. For example:

```
spec:
# Resource limits constrain the total size of the cluster.
# Limits prevent Node Auto Provisioning from creating new instances once the limit is exceeded.
limits:
cpu: "1000"
memory: 1000Gi
```


### Node pool weights

When you have multiple node pools defined, you can set a preference of where a workload should be scheduled by defining the relative weight in your node pool definitions. For example:

```
spec:
# Priority given to the node pool when the scheduler considers which to select.
# Higher weights indicate higher priority when comparing node pools.
# Specifying no weight is equivalent to specifying a weight of 0.
weight: 10
```


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:
