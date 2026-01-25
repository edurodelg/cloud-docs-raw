---
merged_at: 2026-01-25T12:25:33.849132
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: node-pool-unique-subnet.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-pool-unique-subnet -->

# Create node pools with unique subnets in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Certain workloads might require splitting cluster nodes into separate pools for logical isolation. Separate subnets dedicated to each node pool in the cluster can help support this isolation, which can address requirements such as having noncontiguous virtual network address space to split across node pools.

In this article, you learn how to create node pools with unique subnets in Azure Kubernetes Service (AKS).

## Prerequisites

[Azure CLI](/en-us/cli/azure/install-azure-cli)version 2.35.0 or later. Run`az version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).- An existing AKS cluster with a system node pool. If you need to create one, see
[Create an AKS cluster with a single node pool](create-node-pools#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli).

## Limitations

- All subnets assigned to node pools must belong to the same virtual network (VNet).
- System pods must have access to all nodes and pods in the cluster to provide critical functionality, such as DNS resolution and tunneling kubectl logs/exec/port-forward proxy.
- If you expand your VNet after creating the cluster, you must update your cluster before adding a subnet outside the original CIDR block. While AKS errors out on the agent pool add, the
`aks-preview`

Azure CLI extension (version 0.5.66 and higher) now supports running`az aks update`

command with only the required`--resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`

arguments. This command performs an update operation without making any changes, which can recover a cluster stuck in a failed state. - In clusters with Kubernetes version less than 1.23.3, kube-proxy SNATs traffic from new subnets, which can cause Azure Network Policy to drop the packets.
- Windows nodes SNAT traffic to the new subnets until the node pool is reimaged.
- Internal load balancers default to one of the node pool subnets.

## Add a node pool with a unique subnet

Add a node pool with a unique subnet into your existing AKS cluster using the

command and the`az aks nodepool add`

`--vnet-subnet-id`

parameter specified.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-count 3 \ --vnet-subnet-id $SUBNET_RESOURCE_ID`


## Next steps

For more information about node pools in AKS, see [Manage node pools for a cluster in Azure Kubernetes Service (AKS)](manage-node-pools).


---

<!-- DOCUMENTO FUSIONADO: concepts-network-services.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-network-services -->

# Kubernetes Services in AKS

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can use Kubernetes Services to logically group pods and provide network connectivity by allowing direct access to them through a specific IP address or DNS name on a designated port. This allows you to expose your application workloads to other services within the cluster or to external clients without having to manually manage the network configuration for each pod hosting a workload.

You can specify what kind of service you want using Kubernetes *Service type values*. For more information, see the

[Kubernetes Service documentation](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types).

The following Service types are available in AKS: [ ClusterIP](#clusterip),

[,](#nodeport)

`NodePort`

[, and](#loadbalancer)

`LoadBalancer`

[.](#externalname)

`ExternalName`

## ClusterIP

`ClusterIP`

creates an internal IP address for use within the AKS cluster. The `ClusterIP`

Service is good for *internal-only applications* that support other workloads within the cluster. ClusterIP is used by default if you don't explicitly specify a type for a Service.


## NodePort

`NodePort`

creates a port mapping on the underlying node that allows the application to be accessed directly with the node IP address and port.


## LoadBalancer

`LoadBalancer`

creates an Azure load balancer resource, configures an external IP address, and connects the requested pods to the load balancer backend pool. To allow customer traffic to reach the application, load balancing rules are created on the desired ports.


For HTTP load balancing of inbound traffic, you can also use an [Ingress controller](concepts-network-ingress#ingress-controllers).

You can also use the `LoadBalancer`

type to create multiple public load balancers in a single AKS cluster. This is useful for large clusters or port-heavy workloads that can quickly exhaust the limits of a single load balancer. For more information, see [Use multiple public load balancers in Azure Kubernetes Service (preview)](use-multiple-standard-load-balancer).

## ExternalName

`ExternalName`

creates a specific DNS entry for easier application access. You can dynamically assign the load balancers and service IP address, or you can specify an existing static IP address. You can assign both internal and external static IP addresses. Existing static IP addresses are often tied to a DNS entry.

You can create both *internal* and *external* load balancers. Internal load balancers are only assigned a private IP address, so they can't be accessed from the Internet.
