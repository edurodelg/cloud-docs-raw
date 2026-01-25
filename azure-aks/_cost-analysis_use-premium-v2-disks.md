---
merged_at: 2026-01-25T12:25:33.921850
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cost-analysis.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/cost-analysis -->

# Azure Kubernetes Service (AKS) cost analysis

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to enable cost analysis on Azure Kubernetes Service (AKS) to view detailed cost data for cluster resources.

## About cost analysis

AKS clusters rely on Azure resources, such as virtual machines (VMs), virtual disks, load balancers, and public IP addresses. Multiple applications can use these resources. The resource consumption patterns often differ for each application, so their contribution toward the total cluster resource cost might also vary. Some applications might have footprints across multiple clusters, which can pose a challenge when performing cost attribution and cost management.

When you enable cost analysis on your AKS cluster, you can view detailed cost allocation scoped to Kubernetes constructs, such as clusters and namespaces, and Azure Compute, Network, and Storage resources. The add-on is built on top of [OpenCost](https://www.opencost.io/), an open-source Cloud Native Computing Foundation Incubating project for usage data collection. Usage data is reconciled with your Azure invoice data to provide a comprehensive view of your AKS cluster costs directly in the Azure portal Cost Management views.

For more information on Microsoft Cost Management, see [Start analyzing costs in Azure](/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis).

After enabling the cost analysis add-on and allowing time for data to be collected, you can use the information in [Understand AKS usage and costs](understand-aks-costs) to help you understand your data.

## Prerequisites

- Your cluster must use the
`Standard`

or`Premium`

tier, not the`Free`

tier. - To view cost analysis information, you must have one of the following roles on the subscription hosting the cluster:
`Owner`

,`Contributor`

,`Reader`

,`Cost Management Contributor`

, or`Cost Management Reader`

. [Managed identity](use-managed-identity)configured on your cluster.- If using the Azure CLI, you need version
`2.61.0`

or later installed. - Once you have enabled cost analysis, you can't downgrade your cluster to the
`Free`

tier without first disabling cost analysis. - Access to the Azure API including Azure Resource Manager (ARM) API. For a list of fully qualified domain names (FQDNs) required, see
[AKS Cost Analysis required FQDN](outbound-rules-control-egress#aks-cost-analysis-add-on).

## Limitations

- Kubernetes cost views are only available for the
*Enterprise Agreement*and*Microsoft Customer Agreement*Microsoft Azure offer types. For more information, see[Supported Microsoft Azure offers](/en-us/azure/cost-management-billing/costs/understand-cost-mgt-data#supported-microsoft-azure-offers). - Currently, virtual nodes aren't supported.

## Enable cost analysis on your AKS cluster

You can enable the cost analysis with the `--enable-cost-analysis`

flag during one of the following operations:

- Creating a
`Standard`

or`Premium`

tier AKS cluster. - Updating an existing
`Standard`

or`Premium`

tier AKS cluster. - Upgrading a
`Free`

cluster to`Standard`

or`Premium`

. - Upgrading a
`Standard`

cluster to`Premium`

. - Downgrading a
`Premium`

cluster to`Standard`

tier.

### Enable cost analysis on a new cluster

Enable cost analysis on a new cluster using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command with the

`--enable-cost-analysis`

flag. The following example creates a new AKS cluster in the `Standard`

tier with cost analysis enabled:```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="AKSCostRG$RANDOM_SUFFIX"
export CLUSTER_NAME="AKSCostCluster$RANDOM_SUFFIX"
export LOCATION="WestUS2"
az group create --resource-group $RESOURCE_GROUP --location $LOCATION
az aks create --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --location $LOCATION --enable-managed-identity --generate-ssh-keys --tier standard --enable-cost-analysis
```


Results:

```
{
"id": "/subscriptions/xxxxx/resourceGroups/AKSCostRGxxxx",
"location": "WestUS2",
"name": "AKSCostClusterxxxx",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null,
"type": "Microsoft.ContainerService/managedClusters"
}
```


### Enable cost analysis on an existing cluster

Enable cost analysis on an existing cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--enable-cost-analysis`

flag. The following example updates an existing AKS cluster in the `Standard`

tier to enable cost analysis:```
az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --enable-cost-analysis
```


Results:

```
{
"id": "/subscriptions/xxxxx/resourceGroups/AKSCostRGxxxx",
"name": "AKSCostClusterxxxx",
"properties": {
"provisioningState": "Succeeded"
}
}
```


Note

An agent is deployed to the cluster when you enable the add-on. The agent consumes a small amount of CPU and Memory resources.

Warning

The AKS cost analysis add-on Memory usage is dependent on the number of containers deployed. You can roughly approximate Memory consumption using *200 MB + 0.5 MB per container*. The current Memory limit is set to *4 GB*, which supports approximately *7000 containers per cluster*. These estimates are subject to change.

Note

Enabling the cost analysis also creates a [managed identity](/en-us/entra/identity/managed-identities-azure-resources/overview) named `cost-analysis-identity`

with read access to the cluster's node resource group, and assigns it to the node pools in the cluster.
This is used to collect the ARM identifiers of cluster assets for reporting.

Since there is already a managed identity for the node pool itself, any commands on the node that use managed identities will need to [specify the identity to use](/en-us/entra/identity/managed-identities-azure-resources/managed-identities-faq#what-identity-will-imds-default-to-if-i-dont-specify-the-identity-in-the-request) rather than relying on the default.

For example, `az login --identity --resource-id <resource ID of identity>`

.

## Disable cost analysis on your AKS cluster

Disable cost analysis using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--disable-cost-analysis`

flag.```
az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --disable-cost-analysis
```


Results:

```
{
"id": "/subscriptions/xxxxx/resourceGroups/AKSCostRGxxxx",
"name": "AKSCostClusterxxxx",
"properties": {
"provisioningState": "Succeeded"
}
}
```


Note

If you want to downgrade your cluster from the `Standard`

or `Premium`

tier to the `Free`

tier while cost analysis is enabled, you must first disable cost analysis.

## View the cost data

You can view cost allocation data in the Azure portal. For more information, see [View AKS costs in Microsoft Cost Management](/en-us/azure/cost-management-billing/costs/view-kubernetes-costs).

### Cost definitions

In the Kubernetes namespaces and assets views, you might see any of the following charges:

**Idle charges**represent the cost of available resource capacity that isn't used by any workloads.**Service charges**represent the charges associated with the service, like Uptime SLA, Microsoft Defender for Containers, etc.**System charges**represent the cost of capacity reserved by AKS on each node to run system processes required by the cluster, including the kubelet and container runtime.[Learn more](concepts-clusters-workloads#resource-reservations).**Unallocated charges**represent the cost of resources that couldn't be allocated to namespaces.

Note

It might take *up to one day* for data to finalize. After 24 hours, any fluctuations in costs for the previous day will have stabilized.

## Troubleshooting

If you're experiencing issues, such as the `cost-agent`

pod getting `OOMKilled`

or stuck in a `Pending`

state, see [Troubleshoot AKS cost analysis add-on issues](/en-us/troubleshoot/azure/azure-kubernetes/aks-cost-analysis-add-on-issues).

## Next steps

For more information on cost in AKS, see [Understand Azure Kubernetes Service (AKS) usage and costs](understand-aks-costs).


---

<!-- DOCUMENTO FUSIONADO: use-premium-v2-disks.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-premium-v2-disks -->

# Use Azure Premium SSD v2 disks on Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Azure Premium SSD v2 disks](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2) offer IO-intense enterprise workloads, a consistent submillisecond disk latency, and high IOPS and throughput. The performance (capacity, throughput, and IOPS) of Premium SSD v2 disks can be independently configured at any time, making it easier for more scenarios to be cost efficient while meeting performance needs.

This article describes how to configure a new or existing AKS cluster to use Azure Premium SSD v2 disks.

## Before you begin

Before creating or upgrading an AKS cluster that is able to use Azure Premium SSD v2 disks, you need to create an AKS cluster in the same region and availability zone that supports Premium Storage and attach the disks following the steps below.

For an existing AKS cluster, you can enable Premium SSD v2 disks by adding a new node pool to your cluster, and then attach the disks following the steps below.

Important

Azure Premium SSD v2 disks require node pools deployed in regions that support these disks. For a list of supported regions, see [Premium SSD v2 disk supported regions](/en-us/azure/virtual-machines/disks-types#regional-availability).

### Limitations

- Azure Premium SSD v2 disks have certain limitations that you need to be aware of. For a complete list, see
[Premium SSD v2 limitations](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2-limitations).

## Use Premium SSD v2 disks dynamically with a storage class

To use Premium SSD v2 disks in a deployment or stateful set, you can use a [storage class for dynamic provisioning](azure-disk-csi).

### Create the storage class

A storage class is used to define how a unit of storage is dynamically created with a persistent volume. For more information on Kubernetes storage classes, see [Kubernetes Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/).

In this example, you create a storage class that references Premium SSD v2 disks. Create a file named `azure-pv2-disk-sc.yaml`

, and copy in the following manifest.

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: premium2-disk-sc
parameters:
cachingMode: None
skuName: PremiumV2_LRS
DiskIOPSReadWrite: "4000"
DiskMBpsReadWrite: "1000"
provisioner: disk.csi.azure.com
reclaimPolicy: Delete
volumeBindingMode: Immediate
allowVolumeExpansion: true
```


Create the storage class with the [kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply) command and specify your *azure-pv2-disk-sc.yaml* file:

```
kubectl apply -f azure-pv2-disk-sc.yaml
```


The output from the command resembles the following example:

```
storageclass.storage.k8s.io/premium2-disk-sc created
```


## Create a persistent volume claim

A persistent volume claim (PVC) is used to automatically provision storage based on a storage class. In this case, a PVC can use the previously created storage class to create an ultra disk.

Create a file named `azure-pv2-disk-pvc.yaml`

, and copy in the following manifest. The claim requests a disk named `premium2-disk`

that is *1000 GB* in size with *ReadWriteOnce* access. The *premium2-disk-sc* storage class is specified as the storage class.

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: premium2-disk
spec:
accessModes:
- ReadWriteOnce
storageClassName: premium2-disk-sc
resources:
requests:
storage: 1000Gi
```


Create the persistent volume claim with the [kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply) command and specify your *azure-pv2-disk-pvc.yaml* file:

```
kubectl apply -f azure-pv2-disk-pvc.yaml
```


The output from the command resembles the following example:

```
persistentvolumeclaim/premium2-disk created
```


## Use the persistent volume

Once the persistent volume claim has been created and the disk successfully provisioned, a pod can be created with access to the disk. The following manifest creates a basic NGINX pod that uses the persistent volume claim named *premium2-disk* to mount the Azure disk at the path `/mnt/azure`

.

Create a file named `nginx-premium2.yaml`

, and copy in the following manifest.

```
kind: Pod
apiVersion: v1
metadata:
name: nginx-premium2
spec:
containers:
- name: nginx-premium2
image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
resources:
requests:
cpu: 100m
memory: 128Mi
limits:
cpu: 250m
memory: 256Mi
volumeMounts:
- mountPath: "/mnt/azure"
name: volume
volumes:
- name: volume
persistentVolumeClaim:
claimName: premium2-disk
```


Create the pod with the [kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply) command, as shown in the following example:

```
kubectl apply -f nginx-premium2.yaml
```


The output from the command resembles the following example:

```
pod/nginx-premium2 created
```


You now have a running pod with your Azure disk mounted in the `/mnt/azure`

directory. This configuration can be seen when inspecting your pod via `kubectl describe pod nginx-premium2`

, as shown in the following condensed example:

```
kubectl describe pod nginx-premium2
[...]
Volumes:
volume:
Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
ClaimName: premium2-disk
ReadOnly: false
kube-api-access-sh59b:
Type: Projected (a volume that contains injected data from multiple sources)
TokenExpirationSeconds: 3607
ConfigMapName: kube-root-ca.crt
ConfigMapOptional: <nil>
DownwardAPI: true
QoS Class: Burstable
Node-Selectors: <none>
Tolerations: node.kubernetes.io/memory-pressure:NoSchedule op=Exists
node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
Type Reason Age From Message
---- ------ ---- ---- -------
Normal Scheduled 7m58s default-scheduler Successfully assigned default/nginx-premium2 to aks-agentpool-12254644-vmss000006
Normal SuccessfulAttachVolume 7m46s attachdetach-controller AttachVolume.Attach succeeded for volume "pvc-ff39fb64-1189-4c52-9a24-e065b855b886"
Normal Pulling 7m39s kubelet Pulling image "mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine"
Normal Pulled 7m38s kubelet Successfully pulled image "mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine" in 1.192915667s
Normal Created 7m38s kubelet Created container nginx-premium2
Normal Started 7m38s kubelet Started container nginx-premium2
[...]
```


## Set IOPS and throughput limits

Input/Output Operations Per Second (IOPS) and throughput limits for Azure Premium v2 SSD disk is currently not supported through AKS. To adjust performance, you can use the Azure CLI command [az disk update](/en-us/cli/azure/disk#az-disk-update) and including the `--disk-iops-read-write`

and `--disk-mbps-read-write`

parameters.

The following example updates the disk IOPS read/write to **5000** and Mbps to **200**. For `--resource-group`

, the value must be the second resource group automatically created to store the AKS worker nodes with the naming convention *MC_resourcegroupname_clustername_location*. For more information, see [Why are two resource groups created with AKS?](faq).

The value for the `--name`

parameter is the name of the volume created using the StorageClass, and it starts with `pvc-`

. To identify the disk name, you can run `kubectl get pvc`

or navigate to the secondary resource group in the portal to find it. See [manage resources from the Azure portal](/en-us/azure/azure-resource-manager/management/manage-resources-portal#open-resources) to learn more.

```
az disk update --subscription subscriptionName --resource-group myResourceGroup --name diskName --disk-iops-read-write=5000 --disk-mbps-read-write=200
```


## Next steps

- For more about Premium SSD v2 disks, see
[Using Azure Premium SSD v2 disks](/en-us/azure/virtual-machines/disks-deploy-premium-v2). - For more about storage best practices, see
[Best practices for storage and backups in Azure Kubernetes Service (AKS)](operator-best-practices-storage).
