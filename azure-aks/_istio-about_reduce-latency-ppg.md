---
merged_at: 2026-01-25T12:25:33.895962
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: istio-about.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-about -->

# Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Istio](https://istio.io/latest/) addresses the challenges developers and operators face with a distributed or microservices architecture. The Istio-based service mesh add-on provides an officially supported and tested integration for Azure Kubernetes Service (AKS).

## What is a Service Mesh?

Modern applications are typically architected as distributed collections of microservices, with each collection of microservices performing some discrete business function. A service mesh is a dedicated infrastructure layer that you can add to your applications. It allows you to transparently add capabilities like observability, traffic management, and security, without adding them to your own code. The term **service mesh** describes both the type of software you use to implement this pattern, and the security or network domain that is created when you use that software.

As the deployment of distributed services, such as in a Kubernetes-based system, grows in size and complexity, it can become harder to understand and manage. You may need to implement capabilities such as discovery, load balancing, failure recovery, metrics, and monitoring. A service mesh can also address more complex operational requirements like A/B testing, canary deployments, rate limiting, access control, encryption, and end-to-end authentication.

Service-to-service communication is what makes a distributed application possible. Routing this communication, both within and across application clusters, becomes increasingly complex as the number of services grow. Istio helps reduce this complexity while easing the strain on development teams.

## What is Istio?

Istio is an open-source service mesh that layers transparently onto existing distributed applications. Istio’s powerful features provide a uniform and more efficient way to secure, connect, and monitor services. Istio enables load balancing, service-to-service authentication, and monitoring – with few or no service code changes. Its powerful control plane brings vital features, including:

- Secure service-to-service communication in a cluster with TLS (Transport Layer Security) encryption, strong identity-based authentication, and authorization.
- Automatic load balancing for HTTP, gRPC, WebSocket, and TCP traffic.
- Fine-grained control of traffic behavior with rich routing rules, retries, failovers, and fault injection.
- A pluggable policy layer and configuration API supporting access controls, rate limits, and quotas.
- Automatic metrics, logs, and traces for all traffic within a cluster, including cluster ingress and egress.

## How is the add-on different from open-source Istio?

This service mesh add-on uses and builds on top of open-source Istio. The add-on flavor provides the following extra benefits:

- Istio versions are tested and verified to be compatible with supported versions of Azure Kubernetes Service.
- Microsoft handles scaling and configuration of Istio control plane
- Microsoft adjusts scaling of AKS components like
`coredns`

when Istio is enabled. - Microsoft provides managed lifecycle (upgrades) for Istio components when triggered by user.
- Verified external and internal ingress set-up.
- Verified to work with
[Azure Monitor managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)and[Azure Managed Grafana](/en-us/azure/managed-grafana/overview). - Official Azure support provided for the add-on.

## Limitations

Istio-based service mesh add-on for AKS has the following limitations:

- The add-on doesn't work on AKS clusters that are using
[Open Service Mesh addon for AKS](open-service-mesh-about). - The add-on doesn't work on AKS clusters with self-managed installations of Istio.
- The add-on doesn't support adding pods associated with virtual nodes to be added under the mesh.
- The add-on doesn't yet support the sidecar-less Ambient mode. Microsoft is currently contributing to Ambient workstream under Istio open source. Product integration for Ambient mode is on the roadmap and is being continuously evaluated as the Ambient workstream evolves.
- The add-on doesn't yet support multi-cluster deployments.
- The add-on doesn't yet support Windows Server containers. Windows Server containers aren't yet supported in open source Istio right now. Issue tracking this feature ask can be found
[here](https://github.com/istio/istio/issues/27893). - Customization of mesh through the following custom resources is currently blocked -
`ProxyConfig, WorkloadEntry, WorkloadGroup, IstioOperator, WasmPlugin`

. - While the add-on allows the use of
`EnvoyFilter`

's, issues arising from them (for example from the Lua script or from the compression library) are outside the support scope of the Istio add-on. See the[support policy document](istio-support-policy#allowed-supported-and-blocked-customizations)for more information about the support categories for Istio add-on features and configuration options. - Gateway API for Istio ingress gateway or managing mesh traffic (GAMMA) is currently not yet supported with Istio add-on. However, Gateway API for Istio ingress traffic management is currently under active development for the add-on. While the add-on supports
[annotation and](istio-deploy-ingress#ingress-gateway-service-customizations), port or protocol configuration is currently not supported.`externalTrafficPolicy`

customization for the Istio ingress gateways - The add-on supports customization of a subset of the fields in
[MeshConfig](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/). Other customizations may be allowed but unsupported or disallowed entirely, as detailed[here](istio-meshconfig#allowed-supported-and-blocked-meshconfig-values).

## Feedback and feature ask

Feedback and feature ask for the Istio add-on can be provided by creating [issues with label 'service-mesh' on AKS GitHub repository](https://github.com/Azure/AKS/issues?q=is%3Aopen+is%3Aissue+label%3Aservice-mesh).


---

<!-- DOCUMENTO FUSIONADO: reduce-latency-ppg.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/reduce-latency-ppg -->

# Use proximity placement groups to reduce latency for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

When using proximity placement groups on AKS, colocation only applies to the agent nodes. Node to node and the corresponding hosted pod to pod latency is improved. The colocation doesn't affect the placement of a cluster's control plane.

When deploying your application in Azure, you can create network latency by spreading virtual machine (VM) instances across regions or availability zones, which may impact the overall performance of your application. A proximity placement group is a logical grouping used to make sure Azure compute resources are physically located close to one another. Some applications, such as gaming, engineering simulations, and high-frequency trading (HFT) require low latency and tasks that can complete quickly. For similar high-performance computing (HPC) scenarios, consider using [proximity placement groups (PPG)](/en-us/azure/virtual-machines/co-location#proximity-placement-groups) for your cluster's node pools.

## Before you begin

This article requires Azure CLI version 2.14 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Limitations

- A proximity placement group can map to only
*one*availability zone. - A node pool must use Virtual Machine Scale Sets to associate a proximity placement group.
- A node pool can associate a proximity placement group at node pool create time only.

## Node pools and proximity placement groups

The first resource you deploy with a proximity placement group attaches to a specific data center. Any extra resources you deploy with the same proximity placement group are colocated in the same data center. Once all resources using the proximity placement group are stopped (deallocated) or deleted, it's no longer attached.

- You can associate multiple node pools with a single proximity placement group.
- You can only associate a node pool with a single proximity placement group.

### Configure proximity placement groups with availability zones

Note

While proximity placement groups require a node pool to use only *one* availability zone, the [baseline Azure VM SLA of 99.9%](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_9/) is still in effect for VMs in a single zone.

Proximity placement groups are a node pool concept and associated with each individual node pool. Using a PPG resource has no impact on AKS control plane availability, which can impact how you should design your cluster with zones. To ensure a cluster is spread across multiple zones, we recommend using the following design:

- Provision a cluster with the first system pool using
*three*zones and no proximity placement group associated to ensure the system pods land in a dedicated node pool, which spreads across multiple zones. - Add extra user node pools with a unique zone and proximity placement group associated to each pool. An example is
*nodepool1*in zone one and PPG1,*nodepool2*in zone two and PPG2, and*nodepool3*in zone 3 with PPG3. This configuration ensures that, at a cluster level, nodes are spread across multiple zones and each individual node pool is colocated in the designated zone with a dedicated PPG resource.

## Create a new AKS cluster with a proximity placement group

Accelerated networking greatly improves networking performance of virtual machines. Ideally, use proximity placement groups with accelerated networking. By default, AKS uses accelerated networking on [supported virtual machine instances](/en-us/azure/virtual-network/accelerated-networking-overview?toc=/azure/virtual-machines/linux/toc.json#limitations-and-constraints), which include most Azure virtual machine with two or more vCPUs.

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location centralus`

Create a proximity placement group using the

command. Make sure to note the ID value in the output.`az ppg create`

`az ppg create --name myPPG --resource-group myResourceGroup --location centralus --type standard`

The command produces an output similar to the following example output, which includes the

*ID*value you need for upcoming CLI commands.`{ "availabilitySets": null, "colocationStatus": null, "id": "/subscriptions/yourSubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.Compute/proximityPlacementGroups/myPPG", "location": "centralus", "name": "myPPG", "proximityPlacementGroupType": "Standard", "resourceGroup": "myResourceGroup", "tags": {}, "type": "Microsoft.Compute/proximityPlacementGroups", "virtualMachineScaleSets": null, "virtualMachines": null }`

Create an AKS cluster using the

command and replace the`az aks create`

*myPPGResourceID*value with your proximity placement group resource ID from the previous step.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --ppg myPPGResourceID --generate-ssh-keys`


## Add a proximity placement group to an existing cluster

You can add a proximity placement group to an existing cluster by creating a new node pool. You can then optionally migrate existing workloads to the new node pool and delete the original node pool.

Use the same proximity placement group that you created earlier to ensure agent nodes in both node pools in your AKS cluster are physically located in the same data center.

Create a new node pool using the

command and replace the`az aks nodepool add`

*myPPGResourceID*value with your proximity placement group resource ID.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name mynodepool \ --node-count 1 \ --ppg myPPGResourceID`


## Clean up

Delete the Azure resource group along with its resources using the

command.`az group delete`

`az group delete --name myResourceGroup --yes --no-wait`


## Next steps

Learn more about [proximity placement groups](/en-us/azure/virtual-machines/co-location#proximity-placement-groups).
