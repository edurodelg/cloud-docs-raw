---
merged_at: 2026-01-25T12:25:33.935989
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: tutorial-kubernetes-deploy-azure-container-storage.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-azure-container-storage -->

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

<!-- DOCUMENTO FUSIONADO: static-ip.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/static-ip -->

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
