---
merged_at: 2026-01-25T12:25:33.895085
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-advanced-container-networking-services.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-advanced-container-networking-services -->

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

<!-- DOCUMENTO FUSIONADO: use-arm64-vms.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-arm64-vms -->

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
