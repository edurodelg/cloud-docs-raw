---
merged_at: 2026-01-26T23:04:05.990066
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-updates-kured -->

# Apply security and kernel updates to Linux nodes in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To protect your clusters, security updates are automatically applied to Linux nodes in AKS. These updates include OS security fixes or kernel updates. Some of these updates require a node reboot to complete the process. AKS doesn't automatically reboot these Linux nodes to complete the update process.

The process to keep Windows Server nodes up to date is a little different. Windows Server nodes don't receive daily updates. Instead, you perform an AKS upgrade that deploys new nodes with the latest base Window Server image and patches. For AKS clusters that use Windows Server nodes, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

This article shows you how to use the open-source [kured (KUbernetes REboot Daemon)](https://github.com/kubereboot/kured) to watch for Linux nodes that require a reboot, then automatically handle the rescheduling of running pods and node reboot process.

Note

`Kured`

is an open-source project in the Cloud Native Computing Foundation. Please direct issues to the [kured GitHub](https://github.com/kubereboot/kured). Additional support can be found in the #kured channel on [CNCF Slack](https://slack.cncf.io).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Before you begin

You need the Azure CLI version 2.0.59 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Understand the AKS node update experience

In an AKS cluster, your Kubernetes nodes run as Azure virtual machines (VMs). These Linux-based VMs use an Ubuntu or Azure Linux image, with the OS configured to automatically check for updates every day. If security or kernel updates are available, they're automatically downloaded and installed.

Some security updates, such as kernel updates, require a node reboot to finalize the process. A Linux node that requires a reboot creates a file named */var/run/reboot-required*. This reboot process doesn't happen automatically.

You can use your own workflows and processes to handle node reboots, or use `kured`

to orchestrate the process. With `kured`

, a [DaemonSet](concepts-clusters-workloads#statefulsets-and-daemonsets) is deployed that runs a pod on each Linux node in the cluster. These pods in the DaemonSet watch for existence of the */var/run/reboot-required* file, and then initiate a process to reboot the nodes.

### Node image upgrades

Unattended upgrades apply updates to the Linux node OS, but the image used to create nodes for your cluster remains unchanged. If a new Linux node is added to your cluster, the original image is used to create the node. This new node receives all the security and kernel updates available during the automatic check every day but remains unpatched until all checks and restarts are complete.

Alternatively, you can use node image upgrade to check for and update node images used by your cluster. For more information on node image upgrade, see [Azure Kubernetes Service (AKS) node image upgrade](node-image-upgrade).

### Node upgrades

There's another process in AKS that lets you *upgrade* a cluster. An upgrade is typically to move to a newer version of Kubernetes, not just apply node security updates. An AKS upgrade performs the following actions:

- A new node is deployed with the latest security updates and Kubernetes version applied.
- An old node is cordoned and drained.
- Pods are scheduled on the new node.
- The old node is deleted.

You can't remain on the same Kubernetes version during an upgrade event. You must specify a newer version of Kubernetes. To upgrade to the latest version of Kubernetes, you can [upgrade your AKS cluster](upgrade-cluster).

## Deploy kured in an AKS cluster

To deploy the `kured`

DaemonSet, install the following official Kured Helm chart. This creates a role and cluster role, bindings, and a service account, then deploys the DaemonSet using `kured`

.

```
# Add the Kured Helm repository
helm repo add kubereboot https://kubereboot.github.io/charts/
# Update your local Helm chart repository cache
helm repo update
# Create a dedicated namespace where you would like to deploy kured into
kubectl create namespace kured
# Install kured in that namespace with Helm 3 (only on Linux nodes, kured is not working on Windows nodes)
helm install my-release kubereboot/kured --namespace kured --set controller.nodeSelector."kubernetes\.io/os"=linux
```


You can also configure extra parameters for `kured`

, such as integration with Prometheus or Slack. For more information about configuration parameters, see the [kured Helm chart](https://github.com/kubereboot/charts/tree/main/charts/kured).

## Update cluster nodes

By default, Linux nodes in AKS check for updates every evening. If you don't want to wait, you can manually perform an update to check that `kured`

runs correctly. First, follow the steps to [SSH to one of your AKS nodes](ssh). Once you have an SSH connection to the Linux node, check for updates and apply them as follows:

```
sudo apt-get update && sudo apt-get upgrade -y
```


If updates were applied that require a node reboot, a file is written to */var/run/reboot-required*. `Kured`

checks for nodes that require a reboot every 60 minutes by default.

## Monitor and review reboot process

When one of the replicas in the DaemonSet detects that a node reboot is required, a lock is placed on the node through the Kubernetes API. This lock prevents more pods from being scheduled on the node. The lock also indicates that only one node should be rebooted at a time. With the node cordoned off, running pods are drained from the node, and the node is rebooted.

You can monitor the status of the nodes using the [kubectl get nodes](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. The following example output shows a node with a status of *SchedulingDisabled* as the node prepares for the reboot process:

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-28993262-0 Ready,SchedulingDisabled agent 1h v1.11.7
```


Once the update process is complete, you can view the status of the nodes using the [kubectl get nodes](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command with the `--output wide`

parameter. This output lets you see a difference in *KERNEL-VERSION* of the underlying nodes, as shown in the following example output. The *aks-nodepool1-28993262-0* was updated in a previous step and shows kernel version *4.15.0-1039-azure*. The node *aks-nodepool1-28993262-1* that hasn't been updated shows kernel version *4.15.0-1037-azure*.

```
NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME
aks-nodepool1-28993262-0 Ready agent 1h v1.11.7 10.240.0.4 <none> Ubuntu 16.04.6 LTS 4.15.0-1039-azure docker://3.0.4
aks-nodepool1-28993262-1 Ready agent 1h v1.11.7 10.240.0.5 <none> Ubuntu 16.04.6 LTS 4.15.0-1037-azure docker://3.0.4
```


## Next steps

This article detailed how to use `kured`

to reboot Linux nodes automatically as part of the security update process. To upgrade to the latest version of Kubernetes, you can [upgrade your AKS cluster](upgrade-cluster).

For AKS clusters that use Windows Server nodes, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-azure-container-storage -->

# Tutorial - Deploy Azure Container Storage (version 1.x.x) on an AKS cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This tutorial introduces Azure Container Storage and demonstrates how to deploy and manage container-native storage for applications running on Azure Kubernetes Service (AKS). If you don't want to deploy Azure Container Storage now, you can skip this tutorial and proceed directly to [Deploy an application in AKS](tutorial-kubernetes-deploy-application). You won't need Azure Container Storage for the basic storefront application in this tutorial series.

Important

This article explains how to install Azure Container Storage (version 1.x.x), which now explicitly requires a version pinning parameter `--container-storage-version 1`

for installation. [Azure Container Storage (version 2.x.x)](/en-us/azure/storage/container-storage/container-storage-introduction) is now available.

Azure Container Storage simplifies the management of stateful applications in Kubernetes by offering container-native storage tailored to a variety of workloads, including databases, analytics platforms, and high-performance applications.

By the end of this tutorial, you will:

- Understand how Azure Container Storage supports diverse workloads in Kubernetes.
- Explore multiple storage backend options to tailor storage to your application's needs.
- Deploy Azure Container Storage (version 1.x.x) on your AKS cluster and create a generic ephemeral volume.

## Before you begin

In previous tutorials, you created a container image, uploaded it to an ACR instance, and created an AKS cluster. Start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app) to follow along.

- This tutorial requires using the Azure CLI version 2.35.0 or later. Portal and PowerShell aren't currently supported for Azure Container Storage. Check your version with
`az --version`

. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). If you're using the Bash environment in Azure Cloud Shell, the latest version is already installed. - You must have an existing Linux-based AKS cluster with at least 3 nodes with
[Storage optimized VM SKUs](/en-us/azure/virtual-machines/sizes/overview#storage-optimized)or[GPU accelerated VM SKUs](/en-us/azure/virtual-machines/sizes/overview#gpu-accelerated). See[Tutorial 3 - Create an AKS cluster](tutorial-kubernetes-deploy-cluster). - You'll need the Kubernetes command-line client,
`kubectl`

. It's already installed if you're using Azure Cloud Shell, or you can install it locally by running the`az aks install-cli`

command.

## Install the Kubernetes extension

Add or upgrade to the latest version of `k8s-extension`

by running the following command.

```
az extension add --upgrade --name k8s-extension
```


## Connect to the cluster and check node status

If you're not already connected to your cluster from the previous tutorial, run the following commands. If you're already connected, you can skip this section.

Run the following command to connect to the cluster.

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using the

`kubectl get`

command. This command returns a list of the cluster nodes.`kubectl get nodes`

The following output example shows the nodes in your cluster. Make sure the status for all nodes shows

*Ready*:`NAME STATUS ROLES AGE VERSION aks-nodepool1-34832848-vmss000000 Ready agent 80m v1.30.9 aks-nodepool1-34832848-vmss000001 Ready agent 80m v1.30.9 aks-nodepool1-34832848-vmss000002 Ready agent 80m v1.30.9`


## Choose a backing storage option

Azure Container Storage (version 1.x.x) uses storage pools to provision and manage persistent and generic volumes. It offers a variety of back-end storage options for your storage pools, each suited for specific workloads. Selecting the right storage type is critical for optimizing workload performance, durability, and cost efficiency. For this tutorial, we'll use Ephemeral Disk with local NVMe as backing storage to create a generic ephemeral volume. However, we'll also explore the other backing storage options that allow you to create persistent volumes.

### Ephemeral Disk

Ephemeral Disk utilizes local storage resources on the AKS nodes (either local NVMe or temp SSD). It offers low sub-ms latency and high IOPS, but no data persistence if the VM restarts. Ephemeral Disk is best suited for applications such as Cassandra that prioritize speed over persistence, and is ideal for workloads with their own application-level replication.

You can use Ephemeral Disk to create either generic ephemeral volumes or persistent volumes, even though the data will be lost if the VM restarts.

### Azure Disks

Ideal for databases like PostgreSQL and MongoDB, Azure Disks offer durability, scalability, and multi-tiered performance options, including Premium SSD and Ultra SSD.

Azure Disks allow for automatic provisioning of storage volumes and include built-in redundancy and high availability.

### Azure Elastic SAN (preview)

Designed for shared storage needs and general-purpose databases requiring scalability and high availability, Azure Elastic SAN is a good fit for workloads such as CI/CD pipelines or large-scale data processing.

## Enable Azure Container Storage (version 1.x.x) and create a storage pool

Run the following command to install Azure Container Storage on the cluster and create a Local NVMe storage pool.

```
az aks update -n myAKSCluster -g myResourceGroup --enable-azure-container-storage ephemeralDisk --container-storage-version 1 --storage-pool-option NVMe
```


The deployment should take less than 15 minutes.

### Verify the storage pool status

When deployment completes, the components for your chosen storage pool type will be enabled, and you'll have a default storage pool.

To get the list of available storage pools, run the following command:

```
kubectl get sp -n acstor
```


To check the status of a storage pool, run the following command:

```
kubectl describe sp <storage-pool-name> -n acstor
```


If the `Message`

doesn't say `StoragePool is ready`

, then your storage pool is still creating or ran into a problem.

## Display the available storage classes

When the storage pool is ready to use, you must select a storage class to define how storage is dynamically created when creating and deploying volumes.

Run `kubectl get sc`

to display the available storage classes. You should see a storage class called `acstor-<storage-pool-name>`

. Use this storage class in the next section to deploy a pod.

## Deploy a pod with a generic ephemeral volume

Create a pod using [Fio](https://github.com/axboe/fio) (Flexible I/O Tester) for benchmarking and workload simulation, that uses a generic ephemeral volume.

Use your favorite text editor to create a YAML manifest file such as

`code acstor-pod.yaml`

.Paste in the following code and save the file.

`kind: Pod apiVersion: v1 metadata: name: fiopod spec: nodeSelector: acstor.azure.com/io-engine: acstor containers: - name: fio image: nixery.dev/shell/fio args: - sleep - "1000000" volumeMounts: - mountPath: "/volume" name: ephemeralvolume volumes: - name: ephemeralvolume ephemeral: volumeClaimTemplate: metadata: labels: type: my-ephemeral-volume spec: accessModes: [ "ReadWriteOnce" ] storageClassName: acstor-ephemeraldisk-nvme # replace with the name of your storage class if different resources: requests: storage: 1Gi`

If you change the storage size of the volume, make sure the size is less than the available capacity of a single node's ephemeral disk. Run

`kubectl get diskpool -n acstor`

to check the available capacity.Apply the YAML manifest file to deploy the pod.

`kubectl apply -f acstor-pod.yaml`

You should see output similar to the following:

`pod/fiopod created`

Check that the pod is running and that the ephemeral volume claim has been bound successfully to the pod:

`kubectl describe pod fiopod kubectl describe pvc fiopod-ephemeralvolume`


You've now deployed a pod that's using local NVMe as its storage, and you can use it for your Kubernetes workloads.

Verify the available capacity of ephemeral disks before provisioning additional volumes:

```
kubectl describe node <node-name>
```


To learn more about Azure Container Storage (version 1.x.x), including how to create persistent volumes, see [What is Azure Container Storage?](/en-us/azure/storage/container-storage/container-storage-introduction-version-1)

## Clean up resources

You won't need Azure Container Storage for the rest of this tutorial series, so we recommend deleting it now to avoid incurring unnecessary Azure charges.

Delete the pod.

`kubectl delete pod fiopod`

Delete the storage pool.

`kubectl delete sp -n acstor <storage-pool-name>`

Delete the extension instance.

`az aks update -n myAKSCluster -g myResourceGroup --disable-azure-container-storage all`


## Next step

In this tutorial, you deployed Azure Container Storage (version 1.x.x) on your AKS cluster. You learned how to:

- Enable Azure Container Storage (version 1.x.x) on your AKS cluster.
- Choose a backing storage type and create a storage pool.
- Deploy a pod with a generic ephemeral volume.

In the next tutorial, you learn how to deploy an application to your cluster.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/private-clusters -->

# Create a private Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article helps you deploy a private link-based AKS cluster. If you're interested in creating an AKS cluster without required private link or tunnel, see [Create an Azure Kubernetes Service (AKS) cluster with API Server VNet integration](api-server-vnet-integration).

## Overview of private clusters in AKS

In a private cluster, the control plane or API server has internal IP addresses that are defined in the [RFC1918 - Address Allocation for Private Internet](https://tools.ietf.org/html/rfc1918) document. By using a private cluster, you can ensure network traffic between your API server and your node pools remains only on the private network.

The control plane or API server is in an AKS-managed Azure resource group, and your cluster or node pool is in your resource group. The server and the cluster or node pool can communicate with each other through the [Azure Private Link service](/en-us/azure/private-link/private-link-service-overview#limitations) in the API server virtual network and a private endpoint exposed on the subnet of your AKS cluster.

When you create a private AKS cluster, AKS creates both private and public fully qualified domain names (FQDNs) with corresponding DNS zones by default. For detailed DNS configuration options, see [Configure a private DNS zone, private DNS subzone, or custom subdomain](#configure-a-private-dns-zone-private-dns-subzone-or-custom-subdomain-for-a-private-aks-cluster).

## Region availability

Private clusters are available in public regions, Azure Government, and Microsoft Azure operated by 21Vianet regions where [AKS is supported](https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service).

Important

All Microsoft Defender for Cloud features will be officially retired in the Azure in China region on August 18, 2026. Due to this upcoming retirement, Azure in China customers are no longer able to onboard new subscriptions to the service. A new subscription is any subscription that was not already onboarded to the Microsoft Defender for Cloud service prior to August 18, 2025, the date of the retirement announcement. For more information on the retirement, see [Microsoft Defender for Cloud Deprecation in Microsoft Azure Operated by 21Vianet Announcement](https://aka.ms/mdcretirementinchina).

Customers should work with their account representatives for Microsoft Azure operated by 21Vianet to assess the impact of this retirement on their own operations.

## Prerequisites for private AKS clusters

- The Azure CLI version 2.28.0 or higher. Run
`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If using Azure Resource Manager (ARM) or the Azure REST API, the AKS API version must be
*2021-05-01 or higher*. - To use a custom DNS server, add the Azure public IP address
*168.63.129.16*as the upstream DNS server in the custom DNS server, and make sure to add this public IP address as the*first*DNS server. For more information about the Azure IP address, see[What is IP address 168.63.129.16?](/en-us/azure/virtual-network/what-is-ip-address-168-63-129-16)- The cluster's DNS zone should be what you forward to
*168.63.129.16*. You can find more information on zone names in[Azure services DNS zone configuration](/en-us/azure/private-link/private-endpoint-dns#azure-services-dns-zone-configuration).

- The cluster's DNS zone should be what you forward to
- Existing AKS clusters enabled with API Server VNet integration can have private cluster mode enabled. For more information, see
[Enable or disable private cluster mode on an existing cluster with API Server VNet integration](api-server-vnet-integration#enable-or-disable-private-cluster-mode-on-an-existing-cluster-with-api-server-vnet-integration).

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Limitations and considerations for private AKS clusters

- You can't apply IP authorized ranges to the private API server endpoint - they only apply to the public API server.
[Azure Private Link service limitations](/en-us/azure/private-link/private-link-service-overview#limitations)apply to private clusters.- There's no support for Azure DevOps Microsoft-hosted Agents with private clusters. Consider using
[self-hosted agents](/en-us/azure/devops/pipelines/agents/agents). - If you need to enable Azure Container Registry on a private AKS cluster,
[set up a private link for the container registry in the cluster virtual network (VNet)](/en-us/azure/container-registry/container-registry-private-link)or set up peering between the container registry's virtual network and the private cluster's virtual network. - Deleting or modifying the private endpoint in the customer subnet causes the cluster to stop functioning.
- Azure Private Link service is supported on Standard Azure Load Balancer only. Basic Azure Load Balancer isn't supported.

## Hub and spoke with custom DNS for private AKS clusters

[Hub and spoke architectures](/en-us/azure/architecture/reference-architectures/hybrid-networking/hub-spoke) are commonly used to deploy networks in Azure. In many of these deployments, DNS settings in the spoke VNets are configured to reference a central DNS forwarder to allow for on-premises and Azure-based DNS resolution.

Keep the following considerations in mind when deploying private AKS clusters in hub and spoke architectures with custom DNS:

When a private cluster is created, a private endpoint (1) and a private DNS zone (2) are created in the cluster-managed resource group by default. The cluster uses an

`A`

record in the private zone to resolve the IP of the private endpoint for communication to the API server.The private DNS zone is linked only to the VNet that the cluster nodes are attached to (3), which means that the private endpoint can only be resolved by hosts in that linked VNet. In scenarios where no custom DNS is configured on the VNet (default), it works without issue as hosts point at

*168.63.129.16*for DNS that can resolve records in the private DNS zone because of the link.If you keep the default private DNS zone behavior, AKS tries to link the zone directly to the spoke VNet that hosts the cluster even when the zone is already linked to a hub VNet.

In spoke VNets that use custom DNS servers, this action can fail if the cluster's managed identity lacks

**Network Contributor**on the spoke VNet.To prevent the failure, choose

**one**of the following supported configurations:**Custom private DNS zone**: Provide a precreated private zone and set`privateDNSZone`

/`--private-dns-zone`

to its resource ID. Link that zone to the appropriate VNet (for example, the hub VNet) and set`publicDNS`

to`false`

/ use`--disable-public-fqdn`

.**Public DNS only**: Disable private zone creation by setting`privateDNSZone`

/`--private-dns-zone`

to`none`

**and**leave`publicDNS`

at its default value (`true`

) / don't use`--disable-public-fqdn`

.

If you're using

[bring your own (BYO) route table with kubenet](configure-kubenet#bring-your-own-subnet-and-route-table-with-kubenet)and BYO DNS with private clusters, cluster creation fails. You need to associate thein the node resource group to the subnet after the cluster creation failed to make the creation successful.`RouteTable`


Keep the following limitations in mind when using custom DNS with private AKS clusters:

- Setting
`privateDNSZone`

/`--private-dns-zone`

to`none`

**and**`publicDNS: false`

/`--disable-public-fqdn`

at the same time**isn't supported**. - Conditional forwarding doesn't support subdomains.

## Create a private AKS cluster with default basic networking

Create a resource group using the

command. You can also use an existing resource group for your AKS cluster.`az group create`

`az group create \ --name <private-cluster-resource-group> \ --location <location>`

Create a private cluster with default basic networking using the

command with the`az aks create`

`--enable-private-cluster`

flag.**Key parameters in this command**:`--enable-private-cluster`

: Enables private cluster mode.

`az aks create \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --load-balancer-sku standard \ --enable-private-cluster \ --generate-ssh-keys`


## Create a private AKS cluster with advanced networking

Create a resource group using the

command. You can also use an existing resource group for your AKS cluster.`az group create`

`az group create \ --name <private-cluster-resource-group> \ --location <location>`

Create a private cluster with advanced networking using the

command.`az aks create`

**Key parameters in this command**:`--enable-private-cluster`

: Enables private cluster mode.`--network-plugin azure`

: Specifies the Azure CNI networking plugin.`--vnet-subnet-id`

: The resource ID of an existing subnet in a virtual network.`--dns-service-ip`

: An available IP address within the Kubernetes service address range to use for the cluster DNS service.`--service-cidr`

: A CIDR notation IP range from which to assign service cluster IPs.

`az aks create \ --resource-group <private-cluster-resource-group> \ --name <private-cluster-name> \ --load-balancer-sku standard \ --enable-private-cluster \ --network-plugin azure \ --vnet-subnet-id <subnet-id> \ --dns-service-ip 10.2.0.10 \ --service-cidr 10.2.0.0/24 --generate-ssh-keys`


## Use custom domains with private AKS clusters

If you want to configure custom domains that can only be resolved internally, see [Use custom domains](coredns-custom#use-custom-domains).

## Disable a public FQDN on a private AKS cluster

### Disable a public FQDN on a new cluster

Disable a public FQDN when creating a private AKS cluster using the

command with the`az aks create`

`--disable-public-fqdn`

flag.`az aks create \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --load-balancer-sku standard \ --enable-private-cluster \ --assign-identity <resource-id> \ --private-dns-zone <private-dns-zone-mode> \ --disable-public-fqdn \ --generate-ssh-keys`


### Disable a public FQDN on an existing cluster

Disable a public FQDN on an existing AKS cluster using the

command with the`az aks update`

`--disable-public-fqdn`

flag.`az aks update \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --disable-public-fqdn`


## Configure a private DNS zone, private DNS subzone, or custom subdomain for a private AKS cluster

You can configure private DNS settings for a private AKS cluster using the Azure CLI (with the `--private-dns-zone`

parameter) or an Azure Resource Manager (ARM) template (with the `privateDNSZone`

property). The following table outlines the options available for the `--private-dns-zone`

parameter / `privateDNSZone`

property:

| Setting | Description |
|---|---|
`system` |
The default value when configuring a private DNS zone. If you omit `--private-dns-zone` / `privateDNSZone` , AKS creates a private DNS zone in the node resource group. |
`none` |
If you set `--private-dns-zone` / `privateDNSZone` to `none` , AKS doesn't create a private DNS zone. |
`<custom-private-dns-zone-resource-id>` |
To use this parameter, you need to create a private DNS zone in the following format for Azure global cloud: `privatelink.<region>.azmk8s.io` or `<subzone>.privatelink.<region>.azmk8s.io` . You need the resource ID of the private DNS zone for future use. You also need a user-assigned identity or service principal with the
`private.<region>.azmk8s.io` or `<subzone>.private.<region>.azmk8s.io` . You can't change or delete this resource after creating the cluster, as it can cause performance issues and cluster upgrade failures. You can use `--fqdn-subdomain <subdomain>` with `<custom-private-dns-zone-resource-id>` only to provide subdomain capabilities to `privatelink.<region>.azmk8s.io` . If you're specifying a subzone, there's a 32 character limit for the `<subzone>` name. |

Keep the following considerations in mind when configuring private DNS for a private AKS cluster:

- If the private DNS zone is in a different subscription than the AKS cluster, you need to register the
`Microsoft.ContainerServices`

Azure provider in both subscriptions. - If your AKS cluster is configured with an Active Directory service principal, AKS doesn't support using a system-assigned managed identity with custom private DNS zone. The cluster must use
[user-assigned managed identity authentication](use-managed-identity).

## Create a private AKS cluster with a private DNS zone

Create a private AKS cluster with a private DNS zone using the

command.`az aks create`

**Key parameters in this command**:`--enable-private-cluster`

: Enables private cluster mode.`--private-dns-zone [system|none]`

: Configures the private DNS zone for the cluster. The default value is`system`

.`--assign-identity <resource-id>`

: The resource ID of a user-assigned managed identity with the[Private DNS Zone Contributor](/en-us/azure/role-based-access-control/built-in-roles#dns-zone-contributor)and[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)roles.

`az aks create \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --load-balancer-sku standard \ --enable-private-cluster \ --assign-identity <resource-id> \ --private-dns-zone [system|none] \ --generate-ssh-keys`


## Create a private AKS cluster with a custom private DNS zone or private DNS subzone

Create a private AKS cluster with a custom private DNS zone or subzone using the

command.`az aks create`

**Key parameters in this command**:`--enable-private-cluster`

: Enables private cluster mode.`--private-dns-zone <custom-private-dns-zone-resource-id>|<custom-private-dns-subzone-resource-id>`

: The resource ID of a precreated private DNS zone or subzone in the following format for Azure global cloud:`privatelink.<region>.azmk8s.io`

or`<subzone>.privatelink.<region>.azmk8s.io`

.`--assign-identity <resource-id>`

: The resource ID of a user-assigned managed identity with the[Private DNS Zone Contributor](/en-us/azure/role-based-access-control/built-in-roles#dns-zone-contributor)and[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)roles.

`# The custom private DNS zone name should be in the following format: "<subzone>.privatelink.<region>.azmk8s.io" az aks create \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --load-balancer-sku standard \ --enable-private-cluster \ --assign-identity <resource-id> \ --private-dns-zone [<custom-private-dns-zone-resource-id>|<custom-private-dns-subzone-resource-id>] \ --generate-ssh-keys`


## Create a private AKS cluster with a custom private DNS zone and custom subdomain

Create a private AKS cluster with a custom private DNS zone and subdomain using the

command.`az aks create`

**Key parameters in this command**:`--enable-private-cluster`

: Enables private cluster mode.`--private-dns-zone <custom-private-dns-zone-resource-id>`

: The resource ID of a precreated private DNS zone in the following format for Azure global cloud:`privatelink.<region>.azmk8s.io`

.`--fqdn-subdomain <subdomain>`

: The subdomain to use for the cluster FQDN within the custom private DNS zone.`--assign-identity <resource-id>`

: The resource ID of a user-assigned managed identity with the[Private DNS Zone Contributor](/en-us/azure/role-based-access-control/built-in-roles#dns-zone-contributor)and[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)roles.

`# The custom private DNS zone name should be in one of the following formats: "privatelink.<region>.azmk8s.io" or "<subzone>.privatelink.<region>.azmk8s.io" az aks create \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --load-balancer-sku standard \ --enable-private-cluster \ --assign-identity <resource-id> \ --private-dns-zone <custom-private-dns-zone-resource-id> \ --fqdn-subdomain <subdomain> \ --generate-ssh-keys`


## Update an existing private AKS cluster from a private DNS zone to public

You can only update from `byo`

(bring your own) or `system`

to `none`

. No other combination of update values is supported.

Warning

When you update a private cluster from `byo`

or `system`

to `none`

, the agent nodes change to use a public FQDN. In an AKS cluster that uses Azure Virtual Machine Scale Sets, a [node image upgrade](node-image-upgrade) is performed to update your nodes with the public FQDN.

Update a private cluster from

`byo`

or`system`

to`none`

using thecommand with the`az aks update`

`--private-dns-zone`

parameter set to`none`

.`az aks update \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --private-dns-zone none`


## Configure kubectl to connect to a private AKS cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, use the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials --resource-group <private-cluster-resource-group> --name <private-cluster-name>`

Verify the connection to your cluster using the

command. This command returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`

The command returns output similar to the following example output:

`NAME STATUS ROLES AGE VERSION aks-nodepool1-12345678-vmss000000 Ready agent 3h6m v1.15.11 aks-nodepool1-12345678-vmss000001 Ready agent 3h6m v1.15.11 aks-nodepool1-12345678-vmss000002 Ready agent 3h6m v1.15.11`

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/cost-advisors -->

# Get Azure Kubernetes Service (AKS) cost recommendations in Azure Advisor

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS cost recommendations in Azure Advisor follow AKS cost best practices and help you optimize your deployments to achieve cost-efficiency without compromising on reliability. Advisor analyzes your resource configuration and recommends solutions to optimize your AKS cluster.

With Advisor, you can:

- Get proactive, actionable, and personalized best practices recommendations.
- Identify opportunities to reduce your overall Azure spend.
- Get recommendations with proposed actions inline.

Cost is one of five categories that Advisor recommendations can fall into. Other categories include reliability, security, performance, and operational excellence. For more information, see the
[Introduction to Azure Advisor](/en-us/azure/advisor/advisor-overview).

## Prerequisites

- To access Advisor recommendations you must have one of the following roles: Owner, Contributor, or Reader of a subscription, resource group, or resource.

## AKS cost recommendations

Recommendations are available for all clusters, but only the ones relevant to the cluster configuration and historical usage will be surfaced. There is no action required by the customer to enable Azure Advisor, as it is a provided by default for all Azure services out of box.

AKS cost recommendations include the following:

- Enable Vertical Pod Autoscaler recommendation mode to rightsize resource requests and limits.
- Use Azure Kubernetes Service Cost Analysis.
- Fine-tune the cluster autoscaler profile for rapid scale down and cost savings.

For more information, see [Cost recommendations](/en-us/azure/advisor/advisor-reference-cost-recommendations#azure-kubernetes-service).

### Enable Vertical Pod Autoscaler recommendation mode to rightsize resource requests and limits

Setting the correct request and limit values is difficult given the required amount of resources can vary greatly across workloads. Managing this at scale across hundreds or thousands of pods is an even greater challenge. Vertical Pod Autoscaler (VPA) automatically adjusts CPU and memory requests and limits for your pods based on historical workload usage patterns to improve resource utilization.

If you don't want VPA to automatically adjust the values and want additional control, VPA recommendation only mode provides suggested values without making automatic changes. This enables you to review and implement suggested values manually, which can prevent potential disruptions and ensure better control over resource allocation. VPA recommendation mode is a great option to help prevent over-provisioning, a major driver of unnecessary spend.

For more information, see [Vertical pod autoscaling in Azure Kubernetes Service (AKS)](vertical-pod-autoscaler#vpa-overview).

### Use Azure Kubernetes Service cost analysis

AKS cost analysis add-on provides detailed insights into the cost of resources used by your AKS cluster. View costs broken down by Kubernetes constructs like clusters and namespaces. This feature helps you identify cost drivers, track historical trends, identify anomalies and clusters or workloads with optimization opportunities. Having cost monitoring in place is an easy way to get visibility into cluster spend and take action to achieve significant cost savings.

Note

This recommendation is only available for public cloud clusters running in Enterprise or MCA type subscriptions.

For more information, see [Azure Kubernetes Service (AKS) cost analysis](cost-analysis).

### Fine-tune the cluster autoscaler profile for rapid scale down and cost savings

The cluster autoscaler profile is a set of parameters that control the behavior of the cluster autoscaler, which automatically adjusts the number of nodes in a cluster based on workload demand. Tuning these settings allows greater control over autoscaler behavior to optimize resource allocation for specific scenarios. A rapid scale down configuration means more aggressive node scale, which means less idle node costs.

For more information, see [Use the cluster autoscaler in Azure Kubernetes Service (AKS)](cluster-autoscaler#configure-cluster-autoscaler-profile-for-aggressive-scale-down).

## View the Advisor dashboard

You can view recommendations on the Advisor dashboard in Azure portal. For more information, see [Azure Advisor portal basics](/en-us/azure/advisor/advisor-get-started).

## Next steps

To learn more about cost optimization in Azure Kubernetes Service (AKS), see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/virtual-nodes -->

# Create and configure an Azure Kubernetes Services (AKS) cluster to use virtual nodes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To rapidly scale application workloads in an AKS cluster, you can use virtual nodes. With virtual nodes, you have quick provisioning of pods, and only pay per second for their execution time. You don't need to wait for Kubernetes cluster autoscaler to deploy VM compute nodes to run more pods. Virtual nodes are only supported with Linux pods and nodes.

The virtual nodes add on for AKS is based on the open source project [Virtual Kubelet](https://github.com/virtual-kubelet/virtual-kubelet).

This article gives you an overview of the region availability and networking requirements for using virtual nodes, and the known limitations.

## Regional availability

All regions, where ACI supports VNET SKUs, are supported for virtual nodes deployments. For more information, see [Resource availability for Azure Container Instances in Azure regions](/en-us/azure/container-instances/container-instances-region-availability).

For available CPU and memory SKUs in each region, review [Azure Container Instances Resource availability for Azure Container Instances in Azure regions - Linux container groups](/en-us/azure/container-instances/container-instances-region-availability#linux-container-groups)

## Network requirements

Virtual nodes enable network communication between pods that run in Azure Container Instances (ACI) and the AKS cluster. To support this communication, a virtual network subnet is created and delegated permissions are assigned. Virtual nodes only work with AKS clusters created using *advanced* networking (Azure CNI). By default, AKS clusters are created with *basic* networking (kubenet).

Pods running in Azure Container Instances (ACI) need access to the AKS API server endpoint, in order to configure networking.

## Limitations

Virtual nodes functionality is heavily dependent on ACI's feature set. In addition to the [quotas and limits for Azure Container Instances](/en-us/azure/container-instances/container-instances-quotas), the following are scenarios not supported with virtual nodes or are deployment considerations:

Using service principal to pull ACR images.

[Workaround](https://github.com/virtual-kubelet/azure-aci/blob/master/README.md#private-registry)is to use[Kubernetes secrets](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/#create-a-secret-by-providing-credentials-on-the-command-line).Important

Secrets built according to the Kubernetes documentation (for standard nodes) will not work with virtual nodes. A specific server format is required, as detailed in

.`ImageRegistryCredential`

- Azure Container Instances[Virtual Network Limitations](/en-us/azure/container-instances/container-instances-vnet)including VNet peering, Kubernetes network policies, and outbound traffic to the internet with network security groups.Init containers.

[Arguments](/en-us/azure/container-instances/container-instances-exec#restrictions)for exec in ACI.[DaemonSets](concepts-clusters-workloads#statefulsets-and-daemonsets)won't deploy pods to the virtual nodes.To schedule Windows Server containers to ACI, you need to manually install the open source

[Virtual Kubelet ACI](https://github.com/virtual-kubelet/azure-aci)provider.Virtual nodes require AKS clusters with Azure CNI networking.

Using API server authorized ip ranges for AKS.

Volume mounting Azure Files share support

[General-purpose V2](/en-us/azure/storage/common/storage-account-overview#types-of-storage-accounts)and[General-purpose V1](/en-us/azure/storage/common/storage-account-overview#types-of-storage-accounts). However, virtual nodes currently don't support[Persistent Volumes](concepts-storage#persistent-volumes)and[Persistent Volume Claims](concepts-storage#persistent-volume-claims). Follow the instructions for mounting[a volume with Azure Files share as an inline volume](azure-csi-files-storage-provision#mount-file-share-as-an-inline-volume).Using IPv6 isn't supported.

Attaching managed identities to virtual node is not supported.

Virtual nodes don't support the

[Container hooks](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/)feature.

## Next steps

Configure virtual nodes for your clusters:

[Create virtual nodes using Azure CLI](virtual-nodes-cli)[Create virtual nodes using the portal in Azure Kubernetes Services (AKS)](virtual-nodes-portal)

Virtual nodes are often one component of a scaling solution in AKS. For more information on scaling solutions, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/static-ip -->

# Use a static public IP address and DNS label with the Azure Kubernetes Service (AKS) load balancer

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create a load balancer resource in an Azure Kubernetes Service (AKS) cluster, the public IP address assigned to it is only valid for the lifespan of that resource. If you delete the Kubernetes service, the associated load balancer and IP address are also deleted. If you want to assign a specific IP address or retain an IP address for redeployed Kubernetes services, you can create and use a static public IP address.

This article shows you how to create a static public IP address and assign it to your Kubernetes service.

## Before you begin

- You need the Azure CLI version 2.0.59 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - This article covers using a
*Standard*SKU IP with a*Standard*SKU load balancer. For more information, see[IP address types and allocation methods in Azure](/en-us/azure/virtual-network/ip-services/public-ip-addresses#sku).

## Create an AKS cluster

Create an Azure resource group using the

command.`az group create`

`az group create --name myNetworkResourceGroup --location eastus`

Create an AKS cluster using the

command.`az aks create`

`az aks create --name myAKSCluster --resource-group myNetworkResourceGroup --generate-ssh-keys`


## Create a static IP address

Get the name of the node resource group using the

command and query for the`az aks show`

`nodeResourceGroup`

property.`az aks show --name myAKSCluster --resource-group myNetworkResourceGroup --query nodeResourceGroup -o tsv`

Create a static public IP address in the node resource group using the

command.`az network public ip create`

`az network public-ip create \ --resource-group <node resource group name> \ --name myAKSPublicIP \ --sku Standard \ --allocation-method static`

Note

If you're using a

*Basic*SKU load balancer in your AKS cluster, use*Basic*for the`--sku`

parameter when defining a public IP. Only*Basic*SKU IPs work with the*Basic*SKU load balancer and only*Standard*SKU IPs work with*Standard*SKU load balancers.Get the static public IP address using the

command. Specify the name of the node resource group and public IP address you created, and query for the`az network public-ip list`

`ipAddress`

.`az network public-ip show --resource-group <node resource group name> --name myAKSPublicIP --query ipAddress --output tsv`


## Create a service using the static IP address

First, determine which type of managed identity your AKS cluster is using, system-assigned or user-assigned. If you're not certain, call the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the identity's*type*property.`az aks show \ --name myAKSCluster \ --resource-group myResourceGroup \ --query identity.type \ --output tsv`

If the cluster is using a managed identity, the value of the

*type*property will be either**SystemAssigned**or**UserAssigned**.If the cluster is using a service principal, the value of the

*type*property will be null. Consider upgrading your cluster to use a managed identity.If your AKS cluster uses a system-assigned managed identity, then query for the managed identity's principal ID as follows:

`# Get the principal ID for a system-assigned managed identity. CLIENT_ID=$(az aks show \ --name myAKSCluster \ --resource-group myNetworkResourceGroup \ --query identity.principalId \ --output tsv)`

If your AKS cluster uses a user-assigned managed identity, then the principal ID will be null. Query for the user-assigned managed identity's client ID instead:

`# Get the client ID for a user-assigned managed identity. CLIENT_ID=$(az aks show \ --name myAKSCluster \ --resource-group myNetworkResourceGroup \ --query identity.userAssignedIdentities.*.clientId \ --output tsv`

Assign delegated permissions for the managed identity used by the AKS cluster for the public IP's resource group by calling the

command.`az role assignment create`

`# Get the resource ID for the node resource group. RG_SCOPE=$(az group show \ --name <node resource group> \ --query id \ --output tsv) # Assign the Network Contributor role to the managed identity, # scoped to the node resource group. az role assignment create \ --assignee ${CLIENT_ID} \ --role "Network Contributor" \ --scope ${RG_SCOPE}`

Important

If you customized your outbound IP, make sure your cluster identity has permissions to both the outbound public IP and the inbound public IP.

Create a file named

`load-balancer-service.yaml`

and copy in the contents of the following YAML file, providing your own public IP address created in the previous step and the node resource group name.Important

Adding the

`loadBalancerIP`

property to the load balancer YAML manifest is deprecating following[upstream Kubernetes](https://github.com/kubernetes/kubernetes/pull/107235). While current usage remains the same and existing services are expected to work without modification, we**highly recommend setting service annotations**instead. To set service annotations, you can either use`service.beta.kubernetes.io/azure-pip-name`

for public IP name, or use`service.beta.kubernetes.io/azure-load-balancer-ipv4`

for an IPv4 address and`service.beta.kubernetes.io/azure-load-balancer-ipv6`

for an IPv6 address, as shown in the example YAML.`apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-load-balancer-resource-group: <node resource group name> service.beta.kubernetes.io/azure-pip-name: myAKSPublicIP name: azure-load-balancer spec: type: LoadBalancer ports: - port: 80 selector: app: azure-load-balancer`

Note

Adding the

`service.beta.kubernetes.io/azure-pip-name`

annotation ensures the most efficient LoadBalancer creation and is highly recommended to avoid potential throttling.Set a public-facing DNS label to the service using the

`service.beta.kubernetes.io/azure-dns-label-name`

service annotation. This publishes a fully qualified domain name (FQDN) for your service using Azure's public DNS servers and top-level domain. The annotation value must be unique within the Azure location, so we recommend you use a sufficiently qualified label. Azure automatically appends a default suffix in the location you selected, such as`<location>.cloudapp.azure.com`

, to the name you provide, creating the FQDN.Note

If you want to publish the service on your own domain, see

[Azure DNS](https://azure.microsoft.com/services/dns/)and the[external-dns](https://github.com/kubernetes-sigs/external-dns)project.`apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-load-balancer-resource-group: <node resource group name> service.beta.kubernetes.io/azure-pip-name: myAKSPublicIP service.beta.kubernetes.io/azure-dns-label-name: <unique-service-label> name: azure-load-balancer spec: type: LoadBalancer ports: - port: 80 selector: app: azure-load-balancer`

Create the service and deployment using the

`kubectl apply`

command.`kubectl apply -f load-balancer-service.yaml`

To see the DNS label for your load balancer, use the

`kubectl describe service`

command.`kubectl describe service azure-load-balancer`

The DNS label will be listed under the

`Annotations`

, as shown in the following condensed example output:`Name: azure-load-balancer Namespace: default Labels: <none> Annotations: service.beta.kuberenetes.io/azure-dns-label-name: <unique-service-label>`


## Troubleshoot

If the static IP address defined in the `loadBalancerIP`

property of the Kubernetes service manifest doesn't exist or hasn't been created in the node resource group and there are no other delegations configured, the load balancer service creation fails. To troubleshoot, review the service creation events using the [ kubectl describe](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#describe) command. Provide the name of the service specified in the YAML manifest, as shown in the following example:

```
kubectl describe service azure-load-balancer
```


The output shows you information about the Kubernetes service resource. The following example output shows a `Warning`

in the `Events`

: "`user supplied IP address was not found`

." In this scenario, make sure you created the static public IP address in the node resource group and that the IP address specified in the Kubernetes service manifest is correct.

```
Name: azure-load-balancer
Namespace: default
Labels: <none>
Annotations: <none>
Selector: app=azure-load-balancer
Type: LoadBalancer
IP: 10.0.18.125
IP: 40.121.183.52
Port: <unset> 80/TCP
TargetPort: 80/TCP
NodePort: <unset> 32582/TCP
Endpoints: <none>
Session Affinity: None
External Traffic Policy: Cluster
Events:
Type Reason Age From Message
---- ------ ---- ---- -------
Normal CreatingLoadBalancer 7s (x2 over 22s) service-controller Creating load balancer
Warning CreatingLoadBalancerFailed 6s (x2 over 12s) service-controller Error creating load balancer (will retry): Failed to create load balancer for service default/azure-load-balancer: user supplied IP Address 40.121.183.52 was not found
```


## Next steps

For more control over the network traffic to your applications, use the application routing addon for AKS. For more information about the app routing addon, see [Managed NGINX ingress with the application routing add-on](app-routing).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-ray -->

# Configure and deploy a Ray cluster on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you configure and deploy a Ray cluster on Azure Kubernetes Service (AKS) using KubeRay. You also learn how to use the Ray cluster to train a simple machine learning model and display the results on the Ray Dashboard.

This article provides two methods to deploy the Ray cluster on AKS:

: Use the[Non-interactive deployment](#deploy-the-ray-sample-non-interactively)`deploy.sh`

script in the GitHub repository to deploy the complete Ray sample non-interactively.: Follow the manual deployment steps to deploy the Ray sample to AKS.[Manual deployment](#manually-deploy-the-ray-sample)

## Prerequisites

- Review the
[Ray cluster on AKS overview](ray-overview)to understand the components and deployment process. - An Azure subscription. If you don't have an Azure subscription, you can create a free account
[here](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - The Azure CLI installed on your local machine. You can install it using the instructions in
[How to install the Azure CLI](/en-us/cli/azure/install-azure-cli). - The
[Azure Kubernetes Service Preview extension](/en-us/azure/aks/draft#install-the-aks-preview-azure-cli-extension)installed. [Helm](https://helm.sh/docs/intro/install/)installed.[Terraform client tools](https://developer.hashicorp.com/terraform/install)or[OpenTofu](https://opentofu.org/)installed. This article uses Terraform, but the modules used should be compatible with OpenTofu.

## Deploy the Ray sample non-interactively

If you want to deploy the complete Ray sample non-interactively, you can use the `deploy.sh`

script in the GitHub repository ([https://github.com/Azure-Samples/aks-ray-sample](https://github.com/Azure-Samples/aks-ray-sample)). This script completes the steps outlined in the [Ray deployment process section](ray-overview#ray-deployment-process).

Clone the GitHub repo locally and change to the root of the repo using the following commands:

`git clone https://github.com/Azure-Samples/aks-ray-sample cd aks-ray-sample`

Deploy the complete sample using the following commands:

`chmod +x deploy.sh ./deploy.sh`

Once the deployment completes, review the output of the logs and the resource group in the Azure portal to see the infrastructure that was created.


## Manually deploy the Ray sample

Fashion MNIST is a dataset of Zalando's article images consisting of a training set of 60,000 examples and a test set of 10,000 examples. Each example is a 28x28 grayscale image associated with a label from ten classes. In this guide, you train a simple PyTorch model on this dataset using the Ray cluster.

### Deploy the RayJob specification

To train the model, you need to submit a Ray Job specification to the KubeRay operator running on a private AKS cluster. The Ray Job specification is a YAML file that describes the resources required to run the job, including the Docker image, the command to run, and the number of workers to use.

Looking at the Ray Job description, you might need to modify some fields to match your environment:

- The
`replicas`

field under the`workerGroupSpecs`

section in`rayClusterSpec`

specifies the number of worker pods that KubeRay schedules to the Kubernetes cluster. Each worker pod requires*3 CPUs*and*4 GB of memory*. The head pod requires*1 CPU*and*4 GB of memory*. Setting the`replicas`

field to*2*requires*8 vCPUs*in the node pool used to implement the RayCluster for the job. - The
`NUM_WORKERS`

field under`runtimeEnvYAML`

in`spec`

specifies the number of Ray actors to launch. Each Ray actor must be serviced by a worker pod in the Kubernetes cluster, so this field must be less than or equal to the`replicas`

field. In this example, we set`NUM_WORKERS`

to*2*, which matches the`replicas`

field. - The
`CPUS_PER_WORKER`

field must be set to*less than or equal the number of CPUs allocated to each worker pod minus 1*. In this example, the CPU resource request per worker pod is*3*, so`CPUS_PER_WORKER`

is set to*2*.

To summarize, you need a total of *8 vCPUs* in the node pool to run the PyTorch model training job. Since we added a taint on the system node pool so that no user pods can be scheduled on it, we must create a new node pool with at least *8 vCPUs* to host the Ray cluster.

Download the Ray Job specification file using the following command:

`curl -LO https://raw.githubusercontent.com/ray-project/kuberay/master/ray-operator/config/samples/pytorch-mnist/ray-job.pytorch-mnist.yaml`

Make any necessary modifications to the Ray Job specification file.

Launch the PyTorch model training job using the

`kubectl apply`

command.`kubectl apply -n kuberay -f ray-job.pytorch-mnist.yaml`


### Verify the RayJob deployment

Verify that you have two worker pods and one head pod running in the namespace using the

`kubectl get pods`

command.`kubectl get pods -n kuberay`

Your output should look similar to the following example output:

`NAME READY STATUS RESTARTS AGE kuberay-operator-7d7998bcdb-9h8hx 1/1 Running 0 3d2h pytorch-mnist-raycluster-s7xd9-worker-small-group-knpgl 1/1 Running 0 6m15s pytorch-mnist-raycluster-s7xd9-worker-small-group-p74cm 1/1 Running 0 6m15s rayjob-pytorch-mnist-fc959 1/1 Running 0 5m35s rayjob-pytorch-mnist-raycluster-s7xd9-head-l24hn 1/1 Running 0 6m15s`

Check the status of the RayJob using the

`kubectl get`

command.`kubectl get rayjob -n kuberay`

Your output should look similar to the following example output:

`NAME JOB STATUS DEPLOYMENT STATUS START TIME END TIME AGE rayjob-pytorch-mnist RUNNING Running 2024-11-22T03:08:22Z 9m36s`

Wait until the RayJob completes. This might take a few minutes. Once the

`JOB STATUS`

is`SUCCEEDED`

, you can check the training logs. You can do this by first getting the name of the pod running the RayJob using the`kubectl get pods`

command.`kubectl get pods -n kuberay`

In the output, you should see a pod with a name that starts with

`rayjob-pytorch-mnist`

, similar to the following example output:`NAME READY STATUS RESTARTS AGE kuberay-operator-7d7998bcdb-9h8hx 1/1 Running 0 3d2h pytorch-mnist-raycluster-s7xd9-worker-small-group-knpgl 1/1 Running 0 14m pytorch-mnist-raycluster-s7xd9-worker-small-group-p74cm 1/1 Running 0 14m rayjob-pytorch-mnist-fc959 0/1 Completed 0 13m rayjob-pytorch-mnist-raycluster-s7xd9-head-l24hn 1/1 Running 0 14m`

View the logs of the RayJob using the

`kubectl logs`

command. Make sure to replace`rayjob-pytorch-mnist-fc959`

with the name of the pod running your RayJob.`kubectl logs -n kuberay rayjob-pytorch-mnist-fc959`

In the output, you should see the training logs for the PyTorch model, similar to the following example output:

`2024-11-21 19:09:04,986 INFO cli.py:39 -- Job submission server address: http://rayjob-pytorch-mnist-raycluster-s7xd9-head-svc.kuberay.svc.cluster.local:8265 2024-11-21 19:09:05,712 SUCC cli.py:63 -- ------------------------------------------------------- 2024-11-21 19:09:05,713 SUCC cli.py:64 -- Job 'rayjob-pytorch-mnist-hndpx' submitted successfully 2024-11-21 19:09:05,713 SUCC cli.py:65 -- ------------------------------------------------------- 2024-11-21 19:09:05,713 INFO cli.py:289 -- Next steps 2024-11-21 19:09:05,713 INFO cli.py:290 -- Query the logs of the job: 2024-11-21 19:09:05,713 INFO cli.py:292 -- ray job logs rayjob-pytorch-mnist-hndpx 2024-11-21 19:09:05,713 INFO cli.py:294 -- Query the status of the job: ... View detailed results here: /home/ray/ray_results/TorchTrainer_2024-11-21_19-11-23 To visualize your results with TensorBoard, run: `tensorboard --logdir /tmp/ray/session_2024-11-21_19-08-24_556164_1/artifacts/2024-11-21_19-11-24/TorchTrainer_2024-11-21_19-11-23/driver_artifacts` Training started with configuration: ╭─────────────────────────────────────────────────╮ │ Training config │ ├─────────────────────────────────────────────────┤ │ train_loop_config/batch_size_per_worker 16 │ │ train_loop_config/epochs 10 │ │ train_loop_config/lr 0.001 │ ╰─────────────────────────────────────────────────╯ (RayTrainWorker pid=1193, ip=10.244.4.193) Setting up process group for: env:// [rank=0, world_size=2] (TorchTrainer pid=1138, ip=10.244.4.193) Started distributed worker processes: (TorchTrainer pid=1138, ip=10.244.4.193) - (node_id=3ea81f12c0f73ebfbd5b46664e29ced00266e69355c699970e1d824b, ip=10.244.4.193, pid=1193) world_rank=0, local_rank=0, node_rank=0 (TorchTrainer pid=1138, ip=10.244.4.193) - (node_id=2b00ea2b369c9d27de9596ce329daad1d24626b149975cf23cd10ea3, ip=10.244.1.42, pid=1341) world_rank=1, local_rank=0, node_rank=1 (RayTrainWorker pid=1341, ip=10.244.1.42) Downloading http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/train-images-idx3-ubyte.gz (RayTrainWorker pid=1193, ip=10.244.4.193) Downloading http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/train-images-idx3-ubyte.gz to /home/ray/data/FashionMNIST/raw/train-images-idx3-ubyte.gz (RayTrainWorker pid=1193, ip=10.244.4.193) 0%| | 0.00/26.4M [00:00<?, ?B/s] (RayTrainWorker pid=1193, ip=10.244.4.193) 0%| | 65.5k/26.4M [00:00<01:13, 356kB/s] (RayTrainWorker pid=1193, ip=10.244.4.193) 100%|██████████| 26.4M/26.4M [00:01<00:00, 18.9MB/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Extracting /home/ray/data/FashionMNIST/raw/train-images-idx3-ubyte.gz to /home/ray/data/FashionMNIST/raw (RayTrainWorker pid=1341, ip=10.244.1.42) 100%|██████████| 26.4M/26.4M [00:01<00:00, 18.7MB/s] ... Training finished iteration 1 at 2024-11-21 19:15:46. Total running time: 4min 22s ╭───────────────────────────────╮ │ Training result │ ├───────────────────────────────┤ │ checkpoint_dir_name │ │ time_this_iter_s 144.9 │ │ time_total_s 144.9 │ │ training_iteration 1 │ │ accuracy 0.805 │ │ loss 0.52336 │ ╰───────────────────────────────╯ (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 0: 97%|█████████▋| 303/313 [00:01<00:00, 269.60it/s] Test Epoch 0: 100%|██████████| 313/313 [00:01<00:00, 267.14it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 1: 0%| | 0/1875 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 0: 100%|██████████| 313/313 [00:01<00:00, 270.44it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 0: 100%|█████████▉| 1866/1875 [00:24<00:00, 82.49it/s] [repeated 35x across cluster] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 0: 100%|██████████| 1875/1875 [00:24<00:00, 77.99it/s] Train Epoch 0: 100%|██████████| 1875/1875 [00:24<00:00, 76.19it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 0: 0%| | 0/313 [00:00<?, ?it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 0: 88%|████████▊ | 275/313 [00:01<00:00, 265.39it/s] [repeated 19x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 19%|█▉ | 354/1875 [00:04<00:18, 82.66it/s] [repeated 80x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 0%| | 0/1875 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 40%|████ | 757/1875 [00:09<00:13, 83.01it/s] [repeated 90x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 62%|██████▏ | 1164/1875 [00:14<00:08, 83.39it/s] [repeated 92x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 82%|████████▏ | 1533/1875 [00:19<00:05, 68.09it/s] [repeated 91x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 91%|█████████▏| 1713/1875 [00:22<00:02, 70.20it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 1: 91%|█████████ | 1707/1875 [00:22<00:02, 70.04it/s] [repeated 47x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 0%| | 0/313 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 8%|▊ | 24/313 [00:00<00:01, 237.98it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 1: 96%|█████████▋| 302/313 [00:01<00:00, 250.76it/s] Test Epoch 1: 100%|██████████| 313/313 [00:01<00:00, 262.94it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 2: 0%| | 0/1875 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 92%|█████████▏| 289/313 [00:01<00:00, 222.57it/s] Training finished iteration 2 at 2024-11-21 19:16:12. Total running time: 4min 48s ╭───────────────────────────────╮ │ Training result │ ├───────────────────────────────┤ │ checkpoint_dir_name │ │ time_this_iter_s 25.975 │ │ time_total_s 170.875 │ │ training_iteration 2 │ │ accuracy 0.828 │ │ loss 0.45946 │ ╰───────────────────────────────╯ (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 100%|██████████| 313/313 [00:01<00:00, 226.04it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 1: 100%|██████████| 1875/1875 [00:24<00:00, 76.24it/s] [repeated 45x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 2: 13%|█▎ | 239/1875 [00:03<00:24, 67.30it/s] [repeated 64x across cluster] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 1: 0%| | 0/313 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 85%|████████▍ | 266/313 [00:01<00:00, 222.54it/s] [repeated 20x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) .. Training completed after 10 iterations at 2024-11-21 19:19:47. Total running time: 8min 23s 2024-11-21 19:19:47,596 INFO tune.py:1009 -- Wrote the latest version of all result files and experiment state to '/home/ray/ray_results/TorchTrainer_2024-11-21_19-11-23' in 0.0029s. Training result: Result( metrics={'loss': 0.35892221605786073, 'accuracy': 0.872}, path='/home/ray/ray_results/TorchTrainer_2024-11-21_19-11-23/TorchTrainer_74867_00000_0_2024-11-21_19-11-24', filesystem='local', checkpoint=None ) (RayTrainWorker pid=1341, ip=10.244.1.42) Downloading http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/t10k-labels-idx1-ubyte.gz [repeated 7x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Downloading http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/t10k-labels-idx1-ubyte.gz to /home/ray/data/FashionMNIST/raw/t10k-labels-idx1-ubyte.gz [repeated 7x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Extracting /home/ray/data/FashionMNIST/raw/t10k-labels-idx1-ubyte.gz to /home/ray/data/FashionMNIST/raw [repeated 7x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 9: 91%|█████████ | 1708/1875 [00:21<00:01, 83.84it/s] [repeated 23x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 9: 100%|██████████| 1875/1875 [00:23<00:00, 78.52it/s] [repeated 37x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 9: 0%| | 0/313 [00:00<?, ?it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 9: 89%|████████▉ | 278/313 [00:01<00:00, 266.46it/s] [repeated 19x across cluster] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 9: 97%|█████████▋| 305/313 [00:01<00:00, 256.69it/s] Test Epoch 9: 100%|██████████| 313/313 [00:01<00:00, 267.35it/s] 2024-11-21 19:19:51,728 SUCC cli.py:63 -- ------------------------------------------ 2024-11-21 19:19:51,728 SUCC cli.py:64 -- Job 'rayjob-pytorch-mnist-hndpx' succeeded 2024-11-21 19:19:51,728 SUCC cli.py:65 -- ------------------------------------------`


## View training results on the Ray Dashboard

When the RayJob successfully completes, you can view the training results on the Ray Dashboard. The Ray Dashboard provides real-time monitoring and visualizations of Ray clusters. You can use the Ray Dashboard to monitor the status of Ray clusters, view logs, and visualize the results of machine learning jobs.

To access the Ray Dashboard, you need to expose the Ray head service to the public internet by creating a *service shim* to expose the Ray head service on port 80 instead of port 8265.

Note

The `deploy.sh`

described in the previous section automatically exposes the Ray head service to the public internet. The following steps are included in the `deploy.sh`

script.

Get the name of the Ray head service and save it in a shell variable using the following command:

`rayclusterhead=$(kubectl get service -n $kuberay_namespace | grep 'rayjob-pytorch-mnist-raycluster' | grep 'ClusterIP' | awk '{print $1}')`

Create the service shim to expose the Ray head service on port 80 using the

`kubectl expose service`

command.`kubectl expose service $rayclusterhead \ -n $kuberay_namespace \ --port=80 \ --target-port=8265 \ --type=NodePort \ --name=ray-dash`

Create the ingress to expose the service shim using the ingress controller using the following command:

`cat <<EOF | kubectl apply -f - apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: ray-dash namespace: kuberay annotations: nginx.ingress.kubernetes.io/rewrite-target: / spec: ingressClassName: webapprouting.kubernetes.azure.com rules: - http: paths: - backend: service: name: ray-dash port: number: 80 path: / pathType: Prefix EOF`

Get the public IP address of the ingress controller using the

`kubectl get service`

command.`kubectl get service -n app-routing-system`

In the output, you should see the public IP address of the load balancer attached to the ingress controller. Copy the public IP address and paste it into a web browser. You should see the Ray Dashboard.


## Clean up resources

To clean up the resources created in this guide, you can delete the Azure resource group that contains the AKS cluster.

## Next steps

To learn more about AI and machine learning workloads on AKS, see the following articles:

[Deploy an application that uses OpenAI on Azure Kubernetes Service (AKS)](open-ai-quickstart)[Build and deploy data and machine learning pipelines with Flyte on Azure Kubernetes Service (AKS)](use-flyte)[Deploy an AI model on Azure Kubernetes Service (AKS) with the AI toolchain operator](ai-toolchain-operator)

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Russell de Pina | Principal TPM
- Ken Kilty | Principal TPM
- Erin Schaffer | Content Developer 2
- Adrian Joian | Principal Customer Engineer
- Ryan Graham | Principal Technical Specialist
