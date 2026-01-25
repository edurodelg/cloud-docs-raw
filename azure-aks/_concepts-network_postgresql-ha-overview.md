---
merged_at: 2026-01-25T12:25:33.922683
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: concepts-network.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-network -->

# Networking concepts for applications in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In a container-based, microservices approach to application development, application components work together to process their tasks. Kubernetes provides various resources enabling this cooperation:

- You can connect to and expose applications internally or externally.
- You can build highly available applications by load balancing your applications.
- You can restrict the flow of network traffic into or between pods and nodes to improve security.
- You can configure Ingress traffic for SSL/TLS termination or routing of multiple components for your more complex applications.

This article introduces the core concepts that provide networking to your applications in AKS:

## Kubernetes networking basics

Kubernetes employs a virtual networking layer to manage access within and between your applications or their components:

**Kubernetes nodes and virtual network**: Kubernetes nodes are connected to a virtual network. This setup enables pods (basic units of deployment in Kubernetes) to have both inbound and outbound connectivity.**Kube-proxy component**: kube-proxy runs on each node and is responsible for providing the necessary network features.

Regarding specific Kubernetes functionalities:

**Load balancer**: You can use a load balancer to distribute network traffic evenly across various resources.**Ingress controllers**: These facilitate Layer 7 routing, which is essential for directing application traffic.**Egress traffic control**: Kubernetes allows you to manage and control outbound traffic from cluster nodes.**Network policies**: These policies enable security measures and filtering for network traffic in pods.

In the context of the Azure platform:

- Azure streamlines virtual networking for AKS (Azure Kubernetes Service) clusters.
- Creating a Kubernetes load balancer on Azure simultaneously sets up the corresponding Azure load balancer resource.
- As you open network ports to pods, Azure automatically configures the necessary network security group rules.
- Azure can also manage external DNS configurations for HTTP application routing as new Ingress routes are established.

## Azure virtual networks

In AKS, you can deploy a cluster that uses one of the following network models:

**Overlay network model**: Overlay networking is the most common networking model used in Kubernetes. Pods are given an IP address from a private, logically separate CIDR from the Azure virtual network subnet where AKS nodes are deployed. This model enables simpler, improved scalability when compared to the flat network model.**Flat network model**: A flat network model in AKS assigns IP addresses to pods from a subnet from the same Azure virtual network as the AKS nodes. Any traffic leaving your clusters isn't SNAT'd, and the pod IP address is directly exposed to the destination. This model can be useful for scenarios like exposing pod IP addresses to external services.

For more information on networking models in AKS, see [CNI Networking in AKS](concepts-network-cni-overview).

## Control outbound (egress) traffic

AKS clusters are deployed on a virtual network and have outbound dependencies on services outside of that virtual network, which are almost entirely defined with fully qualified domain names (FQDNs). AKS provides several outbound configuration options which allow you to customize the way in which these external resources are accessed.

Note

After [31 March 2026](https://azure.microsoft.com/updates?id=default-outbound-access-for-vms-in-azure-will-be-retired-transition-to-a-new-method-of-internet-access), new AKS clusters that use the **AKS-managed virtual network** option will place cluster subnets into [private subnets](/en-us/azure/virtual-network/ip-services/default-outbound-access#why-is-disabling-default-outbound-access-recommended) by default (`defaultOutboundAccess = false`

).

This setting **does not impact AKS-managed cluster traffic**, which uses explicitly configured outbound paths. It may affect **unsupported scenarios**, such as deploying other resources (e.g., VMs) into the same subnet.

**Clusters using BYO VNets are unaffected** by this change. In supported configurations, no action is required.

### Outbound configuration options

For more information on the supported AKS cluster outbound configuration types, see [Customize cluster egress with outbound types in Azure Kubernetes Service (AKS)](egress-outboundtype).

By default, AKS clusters have unrestricted outbound (egress) Internet access, which allows the nodes and services you run to access external resources as needed. If desired, you can restrict outbound traffic.

For more information on how to restrict outbound traffic from your cluster see [Control egress traffic for cluster nodes in AKS](limit-egress-traffic).

## Network security groups

A network security group filters traffic for VMs like the AKS nodes. As you create Services, such as a *LoadBalancer*, the Azure platform automatically configures any necessary network security group rules.

You don't need to manually configure network security group rules to filter traffic for pods in an AKS cluster. You can define any required ports and forwarding as part of your Kubernetes Service manifests and let the Azure platform create or update the appropriate rules.

You can also use network policies to automatically apply traffic filter rules to pods.

For more information, see [How network security groups filter network traffic](/en-us/azure/virtual-network/network-security-group-how-it-works).

### Custom virtual network requirements

When using a custom virtual network with AKS clusters, if you have added Network Security Group (NSG) rules to restrict traffic between different subnets, ensure that the NSG security rules permit the following types of communication:

| Destination | Source | Protocol | Port | Use |
|---|---|---|---|---|
| APIServer Subnet CIDR | Cluster Subnet | TCP | 443 and 4443 | Required to enable communication between Nodes and the API server. |
| APIServer Subnet CIDR | Azure Load Balancer | TCP | 9988 | Required to enable communication between Azure Load Balancer and the API server. You can also enable all communication between the Azure Load Balancer and the API Server Subnet CIDR. |
| Node CIDR | Node CIDR | All Protocols | All Ports | Required to enable communication between Nodes. |
| Node CIDR | Pod CIDR | All Protocols | All Ports | Required for Service traffic routing. |
| Pod CIDR | Pod CIDR | All Protocols | All Ports | Required for Pod to Pod and Pod to Service traffic, including DNS. |

These requirements apply to both AKS Standard and AKS Automatic clusters when using custom virtual networks.

## Network policies

By default, all pods in an AKS cluster can send and receive traffic without limitations. For improved security, define rules that control the flow of traffic, like:

- Back-end applications are only exposed to required frontend services.
- Database components are only accessible to the application tiers that connect to them.

Network policy is a Kubernetes feature available in AKS that lets you control the traffic flow between pods. You can allow or deny traffic to the pod based on settings such as assigned labels, namespace, or traffic port. While network security groups are better for AKS nodes, network policies are a more suited, cloud-native way to control the flow of traffic for pods. As pods are dynamically created in an AKS cluster, required network policies can be automatically applied.

For more information, see [Secure traffic between pods using network policies in Azure Kubernetes Service (AKS)](use-network-policies).

## Next steps

To get started with AKS networking, create and configure an AKS cluster with your own IP address ranges using [Azure CNI Overlay](azure-cni-overlay) or [Azure CNI](configure-azure-cni).

For associated best practices, see [Best practices for network connectivity and security in AKS](operator-best-practices-network).

For more information on core Kubernetes and AKS concepts, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: postgresql-ha-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/postgresql-ha-overview -->

# Overview of deploying a highly available PostgreSQL database on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this guide, you deploy a highly available PostgreSQL cluster that spans multiple Azure availability zones on AKS with Azure CLI.

This article walks through the prerequisites for setting up a PostgreSQL cluster on [Azure Kubernetes Service (AKS)](what-is-aks) and provides an overview of the full deployment process and architecture.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Prerequisites

- This guide assumes a basic understanding of
[core Kubernetes concepts](concepts-clusters-workloads)and[PostgreSQL](https://www.postgresql.org/). - You need the
**Owner**or**User Access Administrator**and the**Contributor**[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles)on a subscription in your Azure account.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


You also need the following resources installed:

[Azure CLI](/en-us/cli/azure/install-azure-cli)version 2.56 or later.[jq](https://jqlang.github.io/jq/), version 1.5 or later.[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)version 1.21.0 or later.[Helm](https://helm.sh/docs/intro/install/)version 3.0.0 or later.[openssl](https://www.openssl.org/)version 3.3.0 or later.[Visual Studio Code](https://code.visualstudio.com/Download)or equivalent.[Krew](https://krew.sigs.k8s.io/)version 0.4.4 or later.[kubectl CloudNativePG (CNPG) Plugin](https://cloudnative-pg.io/documentation/current/kubectl-plugin/#using-krew).


## Deployment process

In this guide, you learn how to:

- Use Azure CLI to create a multi-zone AKS cluster.
- Deploy a highly available PostgreSQL cluster and database using the
[CNPG operator](https://cloudnative-pg.io/documentation/current/kubectl-plugin/#using-krew). - Set up monitoring for PostgreSQL using Prometheus and Grafana.
- Deploy a sample dataset to a PostgreSQL database.
- Perform PostgreSQL and AKS cluster upgrades.
- Simulate a cluster interruption and PostgreSQL replica failover.
- Perform backup and restore of a PostgreSQL database.

## Deployment architecture

This diagram illustrates a PostgreSQL cluster setup with one primary replica and two read replicas managed by the [CloudNativePG (CNPG)](https://cloudnative-pg.io/) operator. The architecture provides a highly available PostgreSQL running on an AKS cluster that can withstand a zone outage by failing over across replicas.

Backups are stored on [Azure Blob Storage](/en-us/azure/storage/blobs/), providing another way to restore the database in the event of an issue with streaming replication from the primary replica.

You might choose to host PostgreSQL on AKS when you need full control over database configuration, extensions, and deployment architecture. It’s ideal for integrating tightly with Kubernetes-native tooling, optimizing costs at scale, and fine-tuning performance through custom resource allocation, caching strategies, and storage configurations tailored to your workload.

Note

For applications that require data separation at the database level, you can add more databases with postInitSQL commands and similar. It's currently not possible to add more databases in a declarative way with the CNPG operator. [Learn more](https://github.com/cloudnative-pg/cloudnative-pg) about the CNPG operator.

### Storage considerations

The type of storage you use can have large effects on PostgreSQL performance. Later in this guide, you select the option best suited for your goals and performance needs.

| Storage type | Compatible driver | Description |
|---|---|---|
|

**Maximum data resiliency**. Azure Premium SSD delivers high-performance storage and seamlessly works with Azure Premium zone-redundant storage (ZRS). Premium SSD is provisioned based on specific sizes, which each offer certain IOPS and throughput levels.[Premium SSD v2](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2)**Best price-performance**. Azure Premium SSD v2 offers higher performance than Azure Premium SSDs while also generally being less costly. Unlike Premium SSDs, Premium SSD v2 doesn't have dedicated sizes. You can set a Premium SSD v2 to any supported size you prefer, and make granular adjustments to the performance without downtime. Azure Premium SSD v2 disks have certain limitations that you should be aware of. For a complete list, see[Premium SSD v2 limitations](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2-limitations).[Local NVMe or temp SSD (Ephemeral Disks)](/en-us/azure/storage/container-storage/use-container-storage-with-local-disk#what-is-ephemeral-disk)**Maximum performance**. Ephemeral Disks are local NVMe and temporary SSD storage available on select VM families. They offer the highest possible IOPS, throughput, and submillisecond latency for your AKS cluster. You can also take advantage of Ephemeral Disks' high performance using[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction), a managed Kubernetes storage solution that dynamically provisions persistent volumes for stateful workloads like PostgreSQL. However, because these disks reside on the local VMs hosting the cluster, data isn't persisted to an Azure storage service. As a result, any data stored on these disks will be lost if the cluster is stopped or deallocated. To address this limitation, later sections in this guide show you how to set up periodic backups of your PostgreSQL data to[Azure Blob Storage](/en-us/azure/storage/blobs/).## Next steps

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Ken Kilty | Principal TPM
- Russell de Pina | Principal TPM
- Adrian Joian | Senior Customer Engineer
- Jenny Hayes | Senior Content Developer
- Carol Smith | Senior Content Developer
- Erin Schaffer | Content Developer 2
- Adam Sharif | Customer Engineer 2

## Acknowledgment

This documentation was jointly developed with EnterpriseDB, the maintainers of the CloudNativePG operator. We thank [Gabriele Bartolini](https://cloudnative-pg.io/authors/gbartolini/) for reviewing earlier drafts of this document and offering technical improvements.
