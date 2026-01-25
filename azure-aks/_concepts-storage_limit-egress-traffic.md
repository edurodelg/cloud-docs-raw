---
merged_at: 2026-01-25T12:25:33.977190
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: concepts-storage.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-storage -->

# Storage options for applications in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Applications running in Azure Kubernetes Service (AKS) might need to store and retrieve data. While some application workloads can use local, fast storage on unneeded, emptied nodes, others require storage that persists on more regular data volumes within the Azure platform.

Multiple pods might need to:

- Share the same data volumes.
- Reattach data volumes if the pod is rescheduled on a different node.

You also might need to collect and store sensitive data or application configuration information into pods.

This article introduces the core concepts that provide storage to your applications in AKS:

## Default OS disk sizing

### Ephemeral OS disks

If you select a VM SKU that supports Ephemeral OS disks but don't specify an OS disk size, AKS by default provisions an Ephemeral OS disk with a size that scales according to the total temp storage of the VM SKU so long as the temp is *at least 128GiB*. For example, the `Standard_D8ds_v5`

SKU with a temp disk size of 300GiB will receive a 300GiB Ephemeral OS disk by default if the disk parameters are unspecified.

If you want to use the temp storage of the VM SKU, you need to specify the OS disk size during deployment, otherwise it's consumed by default.

Important

Default Ephemeral OS disk sizing is only used on new clusters or node pools where Ephemeral OS disks are supported and a default OS disk size isn't specified. The default OS disk size might impact the performance or cost of your cluster. You can't change the OS disk size after cluster or node pool creation. This default Ephemeral sizing affects clusters or node pools created in March 2025 or later.

### Managed OS disks

When you create a new cluster or add a new node pool to an existing cluster, the number for vCPUs by default determines the OS disk size. The number of vCPUs is based on the VM SKU. The following table lists the default OS disk size for each VM SKU:

| VM SKU Cores (vCPUs) | Default OS Disk Tier | Provisioned IOPS | Provisioned Throughput (Mbps) |
|---|---|---|---|
| 1 - 7 | P10/128G | 500 | 100 |
| 8 - 15 | P15/256G | 1100 | 125 |
| 16 - 63 | P20/512G | 2300 | 150 |
| 64+ | P30/1024G | 5000 | 200 |

Important

Default Managed OS disk sizing is only used on new clusters or node pools when Ephemeral OS disks aren't supported and a default OS disk size isn't specified. The default OS disk size might impact the performance or cost of your cluster. You can't change the OS disk size after cluster or node pool creation. We recommend a minimum disk size of 512G if ephemeral OS disk cannot be used. This default Managed sizing affects clusters or node pools created in July 2022 or later.

## Ephemeral OS disk

By default, Azure automatically replicates the operating system disk for a virtual machine to Azure Storage to avoid data loss when the VM is relocated to another host. However, since containers aren't designed to have local state persisted, this behavior offers limited value while providing some drawbacks. These drawbacks include, but aren't limited to, slower node provisioning and higher read/write latency.

By contrast, Ephemeral OS disks are stored only on the host machine, just like a temporary disk. With this configuration, you get lower read/write latency with faster node scaling and cluster upgrades. Therefore, we strongly **recommend using Ephemeral OS disks whenever possible**.

Note

When you don't explicitly request [Azure managed disks](/en-us/azure/virtual-machines/managed-disks-overview) for the OS, AKS defaults to ephemeral OS if possible for a given node pool configuration.

Size requirements and recommendations for ephemeral OS disks are available in the [Azure VM documentation](/en-us/azure/virtual-machines/ephemeral-os-disks). The following are some general sizing considerations:

If you chose to use the AKS default VM size

[Standard_DS2_v2](/en-us/azure/virtual-machines/dv2-dsv2-series#dsv2-series)SKU with the default OS disk size of 100 GiB, the default VM size supports ephemeral OS, but only has 86 GiB of cache size. This configuration would default to managed disks if you don't explicitly specify it. If you do request an ephemeral OS, you receive a validation error.If you request the same

[Standard_DS2_v2](/en-us/azure/virtual-machines/dv2-dsv2-series#dsv2-series)SKU with a 60-GiB OS disk, this configuration would default to ephemeral OS. The requested size of 60 GiB is smaller than the maximum cache size of 86 GiB.If you select the

[Standard_D8s_v3](/en-us/azure/virtual-machines/dv3-dsv3-series#dsv3-series)SKU with 100-GB OS disk, this VM size supports ephemeral OS and has 200 GiB of cache space. If you don't specify the OS disk type, the node pool would receive ephemeral OS by default.

The latest generation of VM series doesn't have a dedicated cache, but only temporary storage. For example, if you selected the [Standard_E2bds_v5](/en-us/azure/virtual-machines/ebdsv5-ebsv5-series#ebdsv5-series) VM size with the default OS disk size of 100 GiB, it supports ephemeral OS disks, but only has 75 GB of temporary storage. This configuration would default to managed OS disks if you don't explicitly specify it. If you do request an ephemeral OS disk, you receive a validation error.

If you request the same

[Standard_E2bds_v5](/en-us/azure/virtual-machines/ebdsv5-ebsv5-series#ebdsv5-series)VM size with a 60-GiB OS disk, this configuration defaults to ephemeral OS disks. The requested size of 60 GiB is smaller than the maximum temporary storage of 75 GiB.If you select

[Standard_E4bds_v5](/en-us/azure/virtual-machines/ebdsv5-ebsv5-series#ebdsv5-series)SKU with 100-GiB OS disk, this VM size supports ephemeral OS and has 150 GiB of temporary storage. If you don't specify the OS disk type, by default Azure provisions an ephemeral OS disk to the node pool.

### Customer-managed keys

You can manage encryption for your ephemeral OS disk with your own keys on an AKS cluster. For more information, see [Use Customer Managed key with Azure disk on AKS](azure-disk-customer-managed-keys).

## Ephemeral NVMe data disks

Ephemeral NVMe data disks provide high-performance, low-latency storage directly attached to the physical host of your Azure VM. These disks are ideal for workloads that require fast, temporary storage for intermediate data processing, such as caching, scratch space, or high-throughput analytics.

Ephemeral NVMe data disks were initially available only on Azure VM L-series, E-series, and GPU VMs. With the introduction of Azure VM v6 and v7 generations, support for ephemeral NVMe data disks has expanded to a much wider range of VM sizes, including D-series, F-series, H-series, and more. NVMe disks deliver significantly higher IOPS and throughput compared to traditional HDD or SSD options. However, data stored on these disks is temporary and will be lost if the VM is deallocated or redeployed.

To simplify management and provisioning of ephemeral NVMe data disks in AKS, use [Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction). Azure Container Storage can automatically detect and orchestrate NVMe data disks, allowing you to create and manage persistent volumes for your Kubernetes workloads with minimal configuration. This approach is recommended for scenarios where high-performance, temporary storage is required, such as:

- High-speed caching layers, such as datasets and checkpoints for AI training, or model files used for AI inference
- High-performance, self-hosted databases that include built-in replication and backup features
- Data-intensive analytics and processing pipelines that require fast, temporary storage
- Temporary scratch space for batch jobs

Important

Ephemeral NVMe data disks are not suitable for storing critical or persistent data. Ensure your application can tolerate data loss and that important data is stored on persistent volumes backed by Azure Disk, Azure Files, or other durable storage options.

For more information on using Azure Container Storage with ephemeral NVMe data disks, see [Use Azure Container Storage with AKS](/en-us/azure/storage/container-storage/use-container-storage-with-local-disk).

## Volumes

Kubernetes typically treats individual pods as ephemeral, disposable resources. Applications have different approaches available to them for using and persisting data. A *volume* represents a way to store, retrieve, and persist data across pods and through the application lifecycle.

Traditional volumes are created as Kubernetes resources backed by Azure Storage. You can manually create data volumes to be assigned to pods directly or have Kubernetes automatically create them. Data volumes can use: [Azure Disk](/en-us/azure/virtual-machines/disks-types), [Azure Files](/en-us/azure/storage/files/storage-files-planning), [Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-service-levels), or [Azure Blobs](/en-us/azure/storage/common/storage-account-overview).

Note

Depending on the VM SKU you're using, the Azure Disk CSI driver might have a per-node volume limit. For some high performance VMs (for example, 16 cores), the limit is 64 volumes per node. To identify the limit per VM SKU, review the **Max data disks** column for each VM SKU offered. For a list of VM SKUs offered and their corresponding detailed capacity limits, see [General purpose virtual machine sizes](/en-us/azure/virtual-machines/sizes-general).

To help determine best fit for your workload between Azure Files and Azure NetApp Files, review the information provided in the article [Azure Files and Azure NetApp Files comparison](/en-us/azure/storage/files/storage-files-netapp-comparison).

### Azure Disk

Use [Azure Disk](azure-disk-csi) to create a Kubernetes *DataDisk* resource. Disks types include:

- Premium SSDs (recommended for most workloads)
- Ultra disks
- Standard SSDs
- Standard HDDs

Tip

For most production and development workloads, use Premium SSDs.

Because an Azure Disk is mounted as *ReadWriteOnce*, it's only available to a single node. For storage volumes accessible by pods on multiple nodes simultaneously, use Azure Files.

### Azure Files

Use [Azure Files](azure-files-csi) to mount a Server Message Block (SMB) version 3.1.1 share or Network File System (NFS) version 4.1 share. Azure Files let you share data across multiple nodes and pods and can use:

- Azure Premium storage backed by high-performance SSDs
- Azure Standard storage backed by regular HDDs

### Azure NetApp Files

- Ultra Storage
- Premium Storage
- Standard Storage

### Azure Blob Storage

Use [Azure Blob Storage](azure-blob-csi) to create a blob storage container and mount it using the NFS v3.0 protocol or BlobFuse.

- Block blobs

### Volume types

Kubernetes volumes represent more than just a traditional disk for storing and retrieving information. Kubernetes volumes can also be used as a way to inject data into a pod for use by its containers.

Common volume types in Kubernetes include:

#### emptyDir

Commonly used as temporary space for a pod. All containers within a pod can access the data on the volume. Data written to this volume type persists only for the lifespan of the pod. Once you delete the pod, the volume is deleted. This volume typically uses the underlying local node disk storage, though it can also exist only in the node's memory.

#### secret

You can use *secret* volumes to inject sensitive data into pods, such as passwords.

- Create a secret using the Kubernetes API.
- Define your pod or deployment and request a specific secret.
- Secrets are only provided to nodes with a scheduled pod that requires them.
- The secret is stored in
*tmpfs*, not written to disk.

- When you delete the last pod on a node requiring a secret, the secret is deleted from the node's tmpfs.
- Secrets are stored within a given namespace and are only accessed by pods within the same namespace.


#### configMap

You can use *configMap* to inject key-value pair properties into pods, such as application configuration information. Define application configuration information as a Kubernetes resource, easily updated and applied to new instances of pods as they're deployed.

Like using a secret:

- Create a ConfigMap using the Kubernetes API.
- Request the ConfigMap when you define a pod or deployment.
- ConfigMaps are stored within a given namespace and are only accessed by pods within the same namespace.


## Persistent volumes

Volumes defined and created as part of the pod lifecycle only exist until you delete the pod. Pods often expect their storage to remain if a pod is rescheduled on a different host during a maintenance event, especially in StatefulSets. A *persistent volume* (PV) is a storage resource created and managed by the Kubernetes API that can exist beyond the lifetime of an individual pod.

You can use the following Azure Storage services to provide the persistent volume:

As noted in the [Volumes](#volumes) section, the choice of Azure Disks or Azure Files is often determined by the need for concurrent access to the data or the performance tier.

A cluster administrator can *statically* create a persistent volume, or a volume can be created *dynamically* by the Kubernetes API server. If a pod is scheduled and requests storage that is currently unavailable, Kubernetes can create the underlying Azure Disk or File storage and attach it to the pod. Dynamic provisioning uses a *storage class* to identify what type of resource needs to be created.

Important

Persistent volumes can't be shared by Windows and Linux pods due to differences in file system support between the two operating systems.

If you want a fully managed solution for block-level access to data, consider using [Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction) instead of CSI drivers. Azure Container Storage integrates with Kubernetes, allowing dynamic and automatic provisioning of persistent volumes. Azure Container Storage supports Azure Disks, Ephemeral Disks, and Azure Elastic SAN (preview) as backing storage, offering flexibility and scalability for stateful applications running on Kubernetes clusters.

## Storage classes

To specify different tiers of storage, such as premium or standard, you can create a *storage class*.

A storage class also defines a *reclaim policy*. When you delete the persistent volume, the reclaim policy controls the behavior of the underlying Azure Storage resource. The underlying resource can either be deleted or kept for use with a future pod.

For clusters using [Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction), you'll see an additional storage class called `acstor-<storage-pool-name>`

. An internal storage class is also created.

For clusters using [Container Storage Interface (CSI) drivers](csi-storage-drivers), the following extra storage classes are created:

| Storage class | Description |
|---|---|
`managed-csi` |
Uses Azure Standard SSD locally redundant storage (LRS) to create a managed disk. The reclaim policy ensures that the underlying Azure Disk is deleted when the persistent volume that used it is deleted. The storage class also configures the persistent volumes to be expandable. You can edit the persistent volume claim to specify the new size. Effective starting with Kubernetes version 1.29, in Azure Kubernetes Service (AKS) clusters deployed across multiple availability zones, this storage class utilizes Azure Standard SSD zone-redundant storage (ZRS) to create managed disks. |
`managed-csi-premium` |
Uses Azure Premium locally redundant storage (LRS) to create a managed disk. The reclaim policy again ensures that the underlying Azure Disk is deleted when the persistent volume that used it is deleted. Similarly, this storage class allows for persistent volumes to be expanded. Effective starting with Kubernetes version 1.29, in Azure Kubernetes Service (AKS) clusters deployed across multiple availability zones, this storage class utilizes Azure Premium zone-redundant storage (ZRS) to create managed disks. |
`azurefile-csi` |
Uses Azure Standard storage to create an Azure file share. The reclaim policy ensures that the underlying Azure file share is deleted when the persistent volume that used it is deleted. |
`azurefile-csi-premium` |
Uses Azure Premium storage to create an Azure file share. The reclaim policy ensures that the underlying Azure file share is deleted when the persistent volume that used it is deleted. |
`azureblob-nfs-premium` |
Uses Azure Premium storage to create an Azure Blob storage container and connect using the NFS v3 protocol. The reclaim policy ensures that the underlying Azure Blob storage container is deleted when the persistent volume that used it is deleted. |
`azureblob-fuse-premium` |
Uses Azure Premium storage to create an Azure Blob storage container and connect using BlobFuse. The reclaim policy ensures that the underlying Azure Blob storage container is deleted when the persistent volume that used it is deleted. |

Unless you specify a storage class for a persistent volume, the default storage class is used. Ensure volumes use the appropriate storage you need when requesting persistent volumes.

Important

Starting with Kubernetes version 1.21, AKS uses CSI drivers by default, and CSI migration is enabled. While existing in-tree persistent volumes continue to function, starting with version 1.26, AKS will no longer support volumes created using in-tree driver and storage provisioned for files and disk.

The `default`

class will be the same as `managed-csi`

.

Effective starting with Kubernetes version 1.29, when you deploy Azure Kubernetes Service (AKS) clusters across multiple availability zones, AKS now utilizes zone-redundant storage (ZRS) to create managed disks within built-in storage classes. ZRS ensures synchronous replication of your Azure managed disks across multiple Azure availability zones in your chosen region. This redundancy strategy enhances the resilience of your applications and safeguards your data against datacenter failures.

However, it's important to note that zone-redundant storage (ZRS) comes at a higher cost compared to locally redundant storage (LRS). If cost optimization is a priority, you can create a new storage class with the `skuname`

parameter set to LRS. You can then use the new storage class in your Persistent Volume Claim (PVC).

You can create a storage class for other needs using `kubectl`

. The following example uses premium managed disks and specifies that the underlying Azure Disk should be *retained* when you delete the pod:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: managed-premium-retain
provisioner: disk.csi.azure.com
parameters:
skuName: Premium_ZRS
reclaimPolicy: Retain
volumeBindingMode: WaitForFirstConsumer
allowVolumeExpansion: true
```


Note

AKS reconciles the default storage classes and will overwrite any changes you make to those storage classes.

For more information about storage classes, see [StorageClass in Kubernetes](https://kubernetes.io/docs/concepts/storage/storage-classes/).

## Persistent volume claims

A persistent volume claim (PVC) requests storage of a particular storage class, access mode, and size. The Kubernetes API server can dynamically provision the underlying Azure Storage resource if no existing resource can fulfill the claim based on the defined storage class.

The pod definition includes the volume mount once the volume has been connected to the pod.

Once an available storage resource has been assigned to the pod requesting storage, the persistent volume is *bound* to a persistent volume claim. Persistent volumes are mapped to claims in a 1:1 mapping.

The following example YAML manifest shows a persistent volume claim that uses the *managed-premium* storage class and requests an Azure Disk that is *5Gi* in size:

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: azure-managed-disk
spec:
accessModes:
- ReadWriteOnce
storageClassName: managed-premium-retain
resources:
requests:
storage: 5Gi
```


When you create a pod definition, you also specify:

- The persistent volume claim to request the desired storage.
- The
*volume mount*for your applications to read and write data.

The following example YAML manifest shows how the previous persistent volume claim can be used to mount a volume at */mnt/azure*:

```
kind: Pod
apiVersion: v1
metadata:
name: nginx
spec:
containers:
- name: myfrontend
image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
volumeMounts:
- mountPath: "/mnt/azure"
name: volume
volumes:
- name: volume
persistentVolumeClaim:
claimName: azure-managed-disk
```


For mounting a volume in a Windows container, specify the drive letter and path. For example:

```
...
volumeMounts:
- mountPath: "d:"
name: volume
- mountPath: "c:\k"
name: k-dir
...
```


## Next steps

For associated best practices, see [Best practices for storage and backups in AKS](operator-best-practices-storage) and [AKS storage considerations](/en-us/azure/cloud-adoption-framework/scenarios/app-platform/aks/storage).

For more information on Azure Container Storage, see the following articles:

For more information on using CSI drivers, see the following articles:

[Container Storage Interface (CSI) drivers for Azure Disk, Azure Files, and Azure Blob storage on Azure Kubernetes Service](csi-storage-drivers)[Use Azure Disk CSI driver in Azure Kubernetes Service](azure-disk-csi)[Use Azure Files CSI driver in Azure Kubernetes Service](azure-files-csi)[Use Azure Blob storage CSI driver in Azure Kubernetes Service](azure-blob-csi)[Configure Azure NetApp Files with Azure Kubernetes Service](azure-netapp-files)

For more information on core Kubernetes and AKS concepts, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: limit-egress-traffic.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/limit-egress-traffic -->

# Limit network traffic with Azure Firewall in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use the [outbound network and fully qualified domain name (FQDN) rules for AKS clusters](outbound-rules-control-egress) to control egress traffic using Azure Firewall. To simplify this configuration, Azure Firewall provides an Azure Kubernetes Service (`AzureKubernetesService`

) FQDN tag that restricts outbound traffic from the AKS cluster.

## Firewall frontend IP requirements

**Production minimum**: Use at least 20 frontend IPs on Azure Firewall to avoid source network address translation (SNAT) port exhaustion.**High-traffic clusters**: If your cluster creates many outbound connections to the same destinations, you might need more frontend IPs to avoid maxing out ports per IP**API server protection**: Add the firewall's public frontend IP to[API server authorized IP ranges](api-server-authorized-ip-ranges)for enhanced security**Developer access**: When using authorized IP ranges, either use a jumpbox in the firewall's virtual network (VNet) or add developer endpoint IPs to the authorized range

This guidance applies throughout the configuration process described in this article.

Note

The FQDN tag contains all the FQDNs listed in [outbound network and FQDN rules for AKS clusters](outbound-rules-control-egress) and is automatically updated.

## Architecture overview

The following diagram illustrates the architecture of an AKS cluster with restricted egress traffic using Azure Firewall:

Key components of this architecture include:

**Public ingress is forced to flow through firewall filters**:- AKS agent nodes are isolated in a dedicated subnet.
[Azure Firewall](/en-us/azure/firewall/overview)is deployed in its own subnet.- A DNAT rule translates the firewall public IP into the load balancer frontend IP.

**Outbound requests start from agent nodes to the Azure Firewall internal IP using a**:[user-defined route (UDR)](egress-outboundtype)- Requests from AKS agent nodes follow a UDR that has been placed on the subnet the AKS cluster was deployed into.
- Azure Firewall egresses out of the VNet from a public IP frontend.
- Access to the public internet or other Azure services flows to and from the firewall frontend IP address.
- You can protect access to the AKS control plane using
[API server authorized IP ranges](api-server-authorized-ip-ranges), including the firewall public frontend IP address.

**Internal traffic**:- You can use an
[internal load balancer](internal-lb)for internal traffic, which you could isolate on its own subnet, instead of or alongside a[public load balancer](load-balancer-standard).

- You can use an

## Configure environment variables

The following table lists the environment variables used in this article. Set these variables in your shell before proceeding, or modify the commands to use your own values.

| Variable | Description | Example value |
|---|---|---|
`PREFIX` |
Prefix for resource names | `aks-egress` |
`RESOURCE_GROUP` |
Name of the resource group | `aks-egress-rg` |
`LOCATION` |
Azure region for resources | `eastus` |
`PLUGIN` |
Network plugin for AKS | `azure` |
`CLUSTER_NAME` |
Name of the AKS cluster | `aks-egress` |
`VNET_NAME` |
Name of the virtual network | `aks-egress-vnet` |
`AKS_SUBNET_NAME` |
Name of the subnet for AKS | `aks-subnet` |
`FW_SUBNET_NAME` |
Name of the subnet for Azure Firewall | `AzureFirewallSubnet` |
`FW_NAME` |
Name of the Azure Firewall | `aks-egress-fw` |
`FW_PUBLICIP_NAME` |
Name of the public IP for Azure Firewall | `aks-egress-fwpublicip` |
`FW_IPCONFIG_NAME` |
Name of the IP configuration for Azure Firewall | `aks-egress-fwconfig` |
`FW_ROUTE_TABLE_NAME` |
Name of the route table for Azure Firewall | `aks-egress-fwrt` |
`FW_ROUTE_NAME_1` |
Name of the route for Azure Firewall | `aks-egress-fwrn` |
`FW_ROUTE_NAME_2` |
Name of the internet route for Azure Firewall | `aks-egress-fwrn-internet` |

## Create a resource group

Create a resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`


## Create a virtual network with multiple subnets

Provision a VNet with two separate subnets: one for the cluster and one for the firewall. Optionally, you can create one for internal service ingress. The following diagram illustrates the empty network topology before deploying any resources:

Create a VNet using the

command.`az network vnet create`

`az network vnet create \ --resource-group $RESOURCE_GROUP \ --name $VNET_NAME \ --location $LOCATION \ --address-prefixes 10.42.0.0/16 \ --subnet-name $AKS_SUBNET_NAME \ --subnet-prefix 10.42.1.0/24`

Create a subnet for Azure Firewall using the

command.`az network vnet subnet create`

`# Dedicated subnet for Azure Firewall (subnet must be named "AzureFirewallSubnet") az network vnet subnet create \ --resource-group $RESOURCE_GROUP \ --vnet-name $VNET_NAME \ --name $FW_SUBNET_NAME \ --address-prefix 10.42.2.0/24`


## Create a public IP for Azure Firewall

Create a standard SKU public IP resource using the

command. This resource is used as the frontend IP address for the Azure Firewall.`az network public-ip create`

`az network public-ip create --resource-group $RESOURCE_GROUP --name $FW_PUBLICIP_NAME --location $LOCATION --sku "Standard"`


## Install the Azure Firewall CLI extension

Register the

[Azure Firewall CLI extension](https://github.com/Azure/azure-cli-extensions/tree/main/src/azure-firewall)to create an Azure Firewall using thecommand.`az extension add`

`az extension add --name azure-firewall`


## Create an Azure Firewall and enable DNS proxy

Note

For high-traffic scenarios, see the [firewall frontend IP requirements](#firewall-frontend-ip-requirements) section.

For more information on how to create an Azure Firewall with multiple IPs, see [Create an Azure Firewall with multiple public IP addresses using Bicep](/en-us/azure/firewall/quick-create-multiple-ip-bicep).

Create an Azure Firewall and enable DNS proxy using the

command with`az network firewall create`

`--enable-dns-proxy`

set to`true`

.`az network firewall create --resource-group $RESOURCE_GROUP --name $FW_NAME --location $LOCATION --enable-dns-proxy true`

Setting up the public IP address to the Azure Firewall might take a few minutes. Once it's ready, you can assign the IP address to the firewall front end.

Note

To use FQDN on network rules, you need DNS proxy enabled. When DNS proxy is enabled, the firewall listens on port 53 and forwards DNS requests to the DNS server you specify. This setting allows the firewall to automatically translate the FQDN.


## Create an IP configuration for Azure Firewall

Create an Azure Firewall IP configuration using the

command.`az network firewall ip-config create`

`az network firewall ip-config create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --name $FW_IPCONFIG_NAME --public-ip-address $FW_PUBLICIP_NAME --vnet-name $VNET_NAME`


## Get the Azure Firewall IP addresses

Save the public and private firewall frontend IP addresses for configuration later using the following commands:

`export FW_PUBLIC_IP=$(az network public-ip show --resource-group $RESOURCE_GROUP --name $FW_PUBLICIP_NAME --query "ipAddress" -o tsv) export FW_PRIVATE_IP=$(az network firewall show --resource-group $RESOURCE_GROUP --name $FW_NAME --query "ipConfigurations[0].privateIPAddress" -o tsv)`

Note

For API server security, see the

[firewall frontend IP requirements](#firewall-frontend-ip-requirements)section.

## UDR configuration for AKS egress through Azure Firewall

Azure automatically routes traffic between Azure subnets, VNets, and on-premises networks. To modify default routing, create a route table with the following requirements:

**Required route parameters**:

**Route destination**:`0.0.0.0/0`

(all traffic)**Next hop type**: Network virtual appliance (NVA)**Next hop IP**: Azure Firewall private IP address**Association**: One route table per subnet (*zero*or*one*allowed)

**UDR constraints**:

- Default internet route (
`0.0.0.0/0`

) already exists but requires public IP for SNAT. - Route must point to gateway/NVA, not directly to internet.
- AKS validates route configuration and prevents direct internet routes.
- Each subnet supports maximum of
*one*associated route table.

**Outbound type impact**:

**UDR (**: No load balancer public IP created for outbound requests.`userDefinedRouting`

)**Load Balancer public IP**: Only created for inbound requests with`LoadBalancer`

service type.**SNAT configuration**: Requires proper public IP configuration for outbound connectivity.

For more information, see [Outbound rules for Azure Load Balancer](/en-us/azure/load-balancer/outbound-rules#scenario6out).

## Create a route with a hop to Azure Firewall

Create an empty route table using the

command. The route table defines the Azure Firewall as the next hop. Each subnet can have`az network route-table create`

*zero*or*one*route table associated to it.`az network route-table create --resource-group $RESOURCE_GROUP --location $LOCATION --name $FW_ROUTE_TABLE_NAME`

Create routes in the route table for the subnets using the

command.`az network route-table route create`

`az network route-table route create --resource-group $RESOURCE_GROUP --name $FW_ROUTE_NAME_1 --route-table-name $FW_ROUTE_TABLE_NAME --address-prefix 0.0.0.0/0 --next-hop-type VirtualAppliance --next-hop-ip-address $FW_PRIVATE_IP az network route-table route create --resource-group $RESOURCE_GROUP --name $FW_ROUTE_NAME_2 --route-table-name $FW_ROUTE_TABLE_NAME --address-prefix $FW_PUBLIC_IP/32 --next-hop-type Internet`


For information on how to override Azure's default system routes or add more routes to a subnet's route table, see the [Virtual network route table documentation](/en-us/azure/virtual-network/virtual-networks-udr-overview#user-defined).

## Azure Firewall outbound rules for AKS

Note

For applications outside of the `kube-system`

or `gatekeeper-system`

namespaces that need to talk to the API server, an extra network rule to allow TCP communication to port 443 for the API server IP in addition to adding application rule for `fqdn-tag`

of `AzureKubernetesService`

is required.

The following network rules are required for AKS egress traffic control through Azure Firewall:

- The first network rule allows access to port 9000 via TCP.
- The second network rule allows access to port 1194 via UDP. If you're deploying to Microsoft Azure operated by 21Vianet, see the
[Azure operated by 21Vianet required network rules](outbound-rules-control-egress#microsoft-azure-operated-by-21vianet-required-network-rules). In this article, the commands use the`AzureCloud.$LOCATION`

service tag as the destination address. Service tags represent groups of IP address prefixes for Azure services in specific regions. This automatically includes the appropriate CIDR ranges for Azure services without requiring manual IP range specification. - The third network rule opens port 123 to
`ntp.ubuntu.com`

FQDN via UDP. Adding an FQDN as a network rule is one of the specific features of Azure Firewall, so you need to adapt it when using your own options. - The fourth and fifth network rules allow access to pull containers from GitHub Container Registry (
`ghcr.io`

) and Docker Hub (`docker.io`

).

## Create network rules on Azure Firewall

Create the network rules using the following

commands.`az network firewall network-rule create`

`az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'apitcp' --protocols 'TCP' --source-addresses '*' --destination-addresses "AzureCloud.$LOCATION" --destination-ports 9000 az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'apiudp' --protocols 'UDP' --source-addresses '*' --destination-addresses "AzureCloud.$LOCATION" --destination-ports 1194 --action allow --priority 100 az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'time' --protocols 'UDP' --source-addresses '*' --destination-fqdns 'ntp.ubuntu.com' --destination-ports 123 az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'ghcr' --protocols 'TCP' --source-addresses '*' --destination-fqdns ghcr.io pkg-containers.githubusercontent.com --destination-ports '443' az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'docker' --protocols 'TCP' --source-addresses '*' --destination-fqdns docker.io registry-1.docker.io production.cloudflare.docker.com --destination-ports '443'`


## Create application rules on Azure Firewall

Create the application rule using the

command.`az network firewall application-rule create`

`az network firewall application-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwar' --name 'fqdn' --source-addresses '*' --protocols 'http=80' 'https=443' --fqdn-tags "AzureKubernetesService" --action allow --priority 100`


To learn more about Azure Firewall, see the [Azure Firewall documentation](/en-us/azure/firewall/overview).

## Associate the route table to AKS

To associate the cluster with the firewall, the dedicated subnet for the cluster's subnet must reference the route table.

Associate the route table to AKS using the

command.`az network vnet subnet update`

`az network vnet subnet update --resource-group $RESOURCE_GROUP --vnet-name $VNET_NAME --name $AKS_SUBNET_NAME --route-table $FW_ROUTE_TABLE_NAME`


## Deploy an AKS cluster that follows your outbound rules

You can now deploy an AKS cluster into the existing VNet. You use the [ userDefinedRouting outbound type](egress-outboundtype), which ensures that any outbound traffic is forced through the firewall and no other egress paths exist. You can also use the

[.](egress-outboundtype#outbound-type-of-loadbalancer)

`loadBalancer`

outbound typeSet an environment variable for the subnet ID of the target subnet using the following command:

`SUBNET_ID=$(az network vnet subnet show --resource-group $RESOURCE_GROUP --vnet-name $VNET_NAME --name $AKS_SUBNET_NAME --query id -o tsv)`


You define the outbound type to use the UDR that already exists on the subnet. This configuration enables AKS to skip the setup and IP provisioning for the load balancer.

Tip

You can add extra features to the cluster deployment, such as [ private clusters](private-clusters).

For API server authorized IP ranges setup and developer access considerations, see the [firewall frontend IP requirements](#firewall-frontend-ip-requirements) section.

## Create an AKS cluster with system-assigned identities

Note

AKS creates a system-assigned kubelet identity in the node resource group if you don't [specify your own kubelet managed identity](use-managed-identity#create-a-kubelet-managed-identity).

For user-defined routing, system-assigned identity only supports the CNI network plugin.

Create an AKS cluster using a system-assigned managed identity with the CNI network plugin using the

command.`az aks create`

`az aks create --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --location $LOCATION \ --node-count 3 \ --network-plugin azure \ --outbound-type userDefinedRouting \ --vnet-subnet-id $SUBNET_ID \ --api-server-authorized-ip-ranges $FW_PUBLIC_IP \ --generate-ssh-keys`


## Create user-assigned identities

If you don't have user-assigned identities, follow the steps in this section. If you already have user-assigned identities, skip to [Create an AKS cluster with user-assigned identities](#create-an-aks-cluster-with-user-assigned-identities).

Create a managed identity using the

command.`az identity create`

`az identity create --name myIdentity --resource-group $RESOURCE_GROUP`

The output should resemble the following example output:

`{ ... "id": "/subscriptions/<subscriptionid>/resourcegroups/aks-egress-rg/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myIdentity", "location": "eastus", "name": "myIdentity", ... "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`

Create a kubelet managed identity using the

command.`az identity create`

`az identity create --name myKubeletIdentity --resource-group $RESOURCE_GROUP`

The output should resemble the following example output:

`{ ... "id": "/subscriptions/<subscriptionid>/resourcegroups/aks-egress-rg/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myKubeletIdentity", "location": "eastus", "name": "myKubeletIdentity", ... "resourceGroup": "aks-egress-rg", ... "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


Note

If you create your own VNet and route table where the resources are outside of the worker node resource group, the CLI automatically adds the role assignment. If you're using an ARM template or other method, you need to use the principal ID of the cluster managed identity to perform a [role assignment](use-managed-identity#add-a-role-assignment-for-a-system-assigned-managed-identity).

## Create an AKS cluster with user-assigned identities

Create an AKS cluster with your existing user-assigned managed identities in the subnet using the

command. Provide the resource ID of the managed identity for the control plane and the resource ID of the kubelet identity.`az aks create`

`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --location $LOCATION \ --node-count 3 \ --network-plugin kubenet \ --outbound-type userDefinedRouting \ --vnet-subnet-id $SUBNET_ID \ --api-server-authorized-ip-ranges $FW_PUBLIC_IP \ --assign-identity <identity-resource-id> \ --assign-kubelet-identity <kubelet-identity-resource-id> \ --generate-ssh-keys`


## Enable developer access to the API server

If you used authorized IP ranges for your cluster in the previous step, you need to add your developer tooling IP addresses to the AKS cluster list of approved IP ranges so you access the API server from there. You can also configure a jumpbox with the needed tooling inside a separate subnet in the firewall's VNet.

Retrieve your IP address using the following command:

`CURRENT_IP=$(dig @resolver1.opendns.com ANY myip.opendns.com +short)`

Add the IP address to the approved ranges using the

command.`az aks update`

`az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --api-server-authorized-ip-ranges $CURRENT_IP/32`


## Connect to the AKS cluster

Configure

`kubectl`

to connect to your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Deploy a public service on AKS

You can now start exposing services and deploying applications to this cluster. This example exposes a public service, but you also might want to expose an internal service using an [internal load balancer](internal-lb).

Review the

[AKS Store Demo quickstart](https://github.com/Azure-Samples/aks-store-demo/blob/main/aks-store-quickstart.yaml)manifest to understand the deployed components.Deploy the service using the

`kubectl apply`

command.`kubectl apply -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/aks-store-quickstart.yaml`


## Get the load balancer internal IP and service IP

Get the internal IP address assigned to the load balancer using the

`kubectl get services`

command.`kubectl get services`

The IP address should be listed in the

`EXTERNAL-IP`

column, as shown in the following example output:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE kubernetes ClusterIP 10.0.0.1 <none> 443/TCP 9m10s order-service ClusterIP 10.0.104.144 <none> 3000/TCP 11s product-service ClusterIP 10.0.237.60 <none> 3002/TCP 10s rabbitmq ClusterIP 10.0.161.128 <none> 5672/TCP,15672/TCP 11s store-front LoadBalancer 10.0.89.139 20.39.18.6 80:32271/TCP 10s`

Get the service IP using the

`kubectl get svc store-front`

command.`SERVICE_IP=$(kubectl get svc store-front -o jsonpath='{.status.loadBalancer.ingress[*].ip}')`


## Create a DNAT rule on Azure Firewall

Important

When you use Azure Firewall to restrict egress traffic and create a UDR to force all egress traffic, make sure you create an appropriate DNAT rule in Azure Firewall to correctly allow ingress traffic. Using Azure Firewall with a UDR breaks the ingress setup due to asymmetric routing. The issue occurs if the AKS subnet has a default route that goes to the firewall's private IP address, but you're using a public load balancer - ingress or Kubernetes service of type `loadBalancer`

. In this case, the incoming load balancer traffic is received via its public IP address, but the return path goes through the firewall's private IP address. Because the firewall is stateful, it drops the returning packet because the firewall isn't aware of an established session. To learn how to integrate Azure Firewall with your ingress or service load balancer, see [Integrate Azure Firewall with Azure Standard Load Balancer](/en-us/azure/firewall/integrate-lb).

To configure inbound connectivity, you need to write a DNAT rule to the Azure Firewall. To test connectivity to your cluster, a rule is defined for the firewall frontend public IP address to route to the internal IP exposed by the internal service. You can customize the destination address. The translated address must be the IP address of the internal load balancer. The translated port must be the exposed port for your Kubernetes service. You also need to specify the internal IP address assigned to the load balancer created by the Kubernetes service.

Add the NAT rule using the

command.`az network firewall nat-rule create`

`az network firewall nat-rule create --collection-name exampleset --destination-addresses $FW_PUBLIC_IP --destination-ports 80 --firewall-name $FW_NAME --name inboundrule --protocols Any --resource-group $RESOURCE_GROUP --source-addresses '*' --translated-port 80 --action Dnat --priority 100 --translated-address $SERVICE_IP`


## Validate connectivity

Navigate to the Azure Firewall frontend IP address in a browser to validate connectivity. You should see the AKS store app. In this example, the firewall public IP was

`52.253.228.132`

:, you can view products, add them to your cart, and then place an order.


## Clean up resources

If you no longer need the resources created in this article, you can delete them to avoid incurring future costs.

Delete the AKS resource group using the

command.`az group delete`

`az group delete --name $RESOURCE_GROUP`
