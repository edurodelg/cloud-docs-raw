---
merged_at: 2026-01-25T12:25:33.978174
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: best-practices-performance-scale.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/best-practices-performance-scale -->

# Best practices for performance and scaling for small to medium workloads in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This article focuses on general best practices for **small to medium workloads**. For best practices specific to **large workloads**, see [Performance and scaling best practices for large workloads in Azure Kubernetes Service (AKS)](best-practices-performance-scale-large).

As you deploy and maintain clusters in AKS, you can use the following best practices to help you optimize performance and scaling.

In this article, you learn about:

- Tradeoffs and recommendations for autoscaling your workloads.
- Managing node scaling and efficiency based on your workload demands.
- Networking considerations for ingress and egress traffic.
- Monitoring and troubleshooting control plane and node performance.
- Capacity planning, surge scenarios, and cluster upgrades.
- Storage and networking considerations for data plane performance.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Application autoscaling vs. infrastructure autoscaling

### Application autoscaling

Application autoscaling is useful when dealing with cost optimization or infrastructure limitations. A well-configured autoscaler maintains high availability for your application while also minimizing costs. You only pay for the resources required to maintain availability, regardless of the demand.

For example, if an existing node has space but not enough IPs in the subnet, it might be able to skip the creation of a new node and instead immediately start running the application on a new pod.

#### Horizontal Pod autoscaling

Implementing [horizontal pod autoscaling](concepts-scale#horizontal-pod-autoscaler) is useful for applications with a steady and predictable resource demand. The Horizontal Pod Autoscaler (HPA) dynamically scales the number of pod replicas, which effectively distributes the load across multiple pods and nodes. This scaling mechanism is typically most beneficial for applications that can be decomposed into smaller, independent components capable of running in parallel.

The HPA provides resource utilization metrics by default. You can also integrate custom metrics or leverage tools like the [Kubernetes Event-Driven Autoscaler (KEDA) (Preview)](keda-about). These extensions allow the HPA to make scaling decisions based on multiple perspectives and criteria, providing a more holistic view of your application's performance. This is especially helpful for applications with varying complex scaling requirements.

Note

If maintaining high availability for your application is a top priority, we recommend leaving a slightly higher buffer for the minimum pod number for your HPA to account for scaling time.

#### Vertical Pod autoscaling

Implementing [vertical pod autoscaling](vertical-pod-autoscaler) is useful for applications with fluctuating and unpredictable resource demands. The Vertical Pod Autoscaler (VPA) allows you to fine-tune resource requests, including CPU and memory, for individual pods, enabling precise control over resource allocation. This granularity minimizes resource waste and enhances the overall efficiency of cluster utilization. The VPA also streamlines application management by automating resource allocation, freeing up resources for critical tasks.

Warning

You shouldn't use the VPA in conjunction with the HPA on the same CPU or memory metrics. This combination can lead to conflicts, as both autoscalers attempt to respond to changes in demand using the same metrics. However, you can use the VPA for CPU or memory in conjunction with the HPA for custom metrics to prevent overlap and ensure that each autoscaler focuses on distinct aspects of workload scaling.

Note

The VPA works based on historical data. We recommend waiting at least *24 hours* after deploying the VPA before applying any changes to give it time to collect recommendation data.

### Infrastructure autoscaling

#### Cluster autoscaling

Implementing cluster autoscaling is useful if your existing nodes lack sufficient capacity, as it helps with scaling up and provisioning new nodes.

When considering cluster autoscaling, the decision of when to remove a node involves a tradeoff between optimizing resource utilization and ensuring resource availability. Eliminating underutilized nodes enhances cluster utilization but might result in new workloads having to wait for resources to be provisioned before they can be deployed. It's important to find a balance between these two factors that aligns with your cluster and workload requirements and [configure the cluster autoscaler profile settings accordingly](cluster-autoscaler#update-the-cluster-autoscaler-settings).

The Cluster Autoscaler profile settings apply universally to all autoscaler-enabled node pools in your cluster. This means that any scaling actions occurring in one autoscaler-enabled node pool might impact the autoscaling behavior in another node pool. It's important to apply consistent and synchronized profile settings across all relevant node pools to ensure that the autoscaler behaves as expected.

##### Overprovisioning

Overprovisioning is a strategy that helps mitigate the risk of application pressure by ensuring there's an excess of readily available resources. This approach is especially useful for applications that experience highly variable loads and cluster scaling patterns that show frequent scale ups and scale downs.

To determine the optimal amount of overprovisioning, you can use the following formula:

```
1-buffer/1+traffic
```


For example, let's say you want to avoid hitting 100% CPU utilization in your cluster. You might opt for a 30% buffer to maintain a safety margin. If you anticipate an average traffic growth rate of 40%, you might consider overprovisioning by 50%, as calculated by the formula:

```
1-30%/1+40%=50%
```


An effective overprovisioning method involves the use of *pause pods*. Pause pods are low-priority deployments that can be easily replaced by high-priority deployments. You create low priority pods that serve the sole purpose of reserving buffer space. When a high-priority pod requires space, the pause pods are removed and rescheduled on another node or a new node to accommodate the high priority pod.

The following YAML shows an example pause pod manifest:

```
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
name: overprovisioning
value: -1
globalDefault: false
description: "Priority class used by overprovisioning."
---
apiVersion: apps/v1
kind: Deployment
metadata:
name: overprovisioning
namespace: kube-system
spec:
replicas: 1
selector:
matchLabels:
run: overprovisioning
template:
metadata:
labels:
run: overprovisioning
spec:
priorityClassName: overprovisioning
containers:
- name: reserve-resources
image: your-custome-pause-image
resources:
requests:
cpu: 1
memory: 4Gi
```


## Node scaling and efficiency


Best practice guidance:Carefully monitor resource utilization and scheduling policies to ensure nodes are being used efficiently.


Node scaling allows you to dynamically adjust the number of nodes in your cluster based on workload demands. It's important to understand that adding more nodes to a cluster isn't always the best solution for improving performance. To ensure optimal performance, you should carefully monitor resource utilization and scheduling policies to ensure nodes are being used efficiently.

### Node images


Best practice guidance:Use the latest node image version to ensure that you have the latest security patches and bug fixes.


Using the latest node image version provides the best performance experience. AKS ships performance improvements within the weekly image releases. The latest daemonset images are cached on the latest VHD image, which provide lower latency benefits for node provisioning and bootstrapping. Falling behind on updates might have a negative impact on performance, so it's important to avoid large gaps between versions.

#### Azure Linux

The [Azure Linux Container Host on AKS](/en-us/azure/azure-linux/intro-azure-linux) uses a native AKS image and provides a single place for Linux development. Every package is built from source and validated, ensuring your services run on proven components.

Azure Linux is lightweight, only including the necessary set of packages to run container workloads. It provides a reduced attack surface and eliminates patching and maintenance of unnecessary packages. At its base layer, it has a Microsoft-hardened kernel tuned for Azure. This image is ideal for performance-sensitive workloads and platform engineers or operators that manage fleets of AKS clusters.

#### Ubuntu 2204

The [Ubuntu 2204 image](https://github.com/Azure/AKS/blob/master/CHANGELOG.md) is the default node image for AKS. It's a lightweight and efficient operating system optimized for running containerized workloads. This means that it can help reduce resource usage and improve overall performance. The image includes the latest security patches and updates, which help ensure that your workloads are protected from vulnerabilities.

The Ubuntu 2204 image is fully supported by Microsoft, Canonical, and the Ubuntu community and can help you achieve better performance and security for your containerized workloads.

### Virtual machines (VMs)


Best practice guidance:When selecting a VM, ensure the size and performance of the OS disk and VM SKU don't have a large discrepancy. A discrepancy in size or performance can cause performance issues and resource contention.


Application performance is closely tied to the VM SKUs you use in your workloads. Larger and more powerful VMs, generally provide better performance. For *mission critical or product workloads*, we recommend using VMs with at least an 8-core CPU. VMs with newer hardware generations, like v4 and v5, can also help improve performance. Keep in mind that create and scale latency might vary depending on the VM SKUs you use.

### Use dedicated system node pools

For scaling performance and reliability, we recommend using a dedicated system node pool. With this configuration, the dedicated system node pool reserves space for critical system resources such as system OS daemons. Your application workload can then run in a user node pool to increase the availability of allocatable resources for your application. This configuration also helps mitigate the risk of resource competition between the system and application.

### Create operations

Review the extensions and add-ons you have enabled during create provisioning. Extensions and add-ons can add latency to overall duration of create operations. If you don't need an extension or add-on, we recommend removing it to improve create latency.

You can also use availability zones to provide a higher level of availability to protect against potential hardware failures or planned maintenance events. AKS clusters distribute resources across logical sections of underlying Azure infrastructure. Availability zones physically separate nodes from other nodes to help ensure that a single failure doesn't impact the availability of your application. Availability zones are only available in certain regions. For more information, see [Availability zones in Azure](/en-us/azure/reliability/availability-zones-overview).

## Kubernetes API server

### LIST and WATCH operations

Kubernetes uses the LIST and WATCH operations to interact with the Kubernetes API server and monitor information about cluster resources. These operations are fundamental to how Kubernetes performs resource management.

**The LIST operation retrieves a list of resources that fit within certain criteria**, such as all pods in a specific namespace or all services in the cluster. This operation is useful when you want to get an overview of your cluster resources or you need to operator on multiple resources at once.

The LIST operation can retrieve large amounts of data, especially in large clusters with multiple resources. Be mindful of the fact that making unbounded or frequent LIST calls puts a significant load on the API server and can close down response times.

**The WATCH operation performs real-time resource monitoring**. When you set up a WATCH on a resource, the API server sends you updates whenever there are changes to that resource. This is important for controllers, like the ReplicaSet controller, which rely on WATCH to maintain the desired state of resources.

Be mindful of the fact that watching too many mutable resources or making too many concurrent WATCH requests can overwhelm the API server and cause excessive resource consumption.

To avoid potential issues and ensure the stability of the Kubernetes control plane, you can use the following strategies:

**Resource quotas**

Implement resource quotas to limit the number of resources that can be listed or watched by a particular user or namespace to prevent excessive calls.

**API Priority and Fairness**

Kubernetes introduced the concept of API Priority and Fairness (APF) to prioritize and manage API requests. You can use APF in Kubernetes to protect the cluster's API server and reduce the number of `HTTP 429 Too Many Requests`

responses seen by client applications.

| Custom resource | Key features |
|---|---|
| PriorityLevelConfigurations | * Define different priority levels for API requests. * Specifies a unique name and assigns an integer value representing the priority level. Higher priority levels have lower integer values, indicating they're more critical. * Can use multiple to categorize requests into different priority levels based on their importance. * Allow you to specify whether requests at a particular priority level should be subject to rate limits. |
| FlowSchemas | * Define how API requests should be routed to different priority levels based on request attributes. * Specify rules that match requests based on criteria like API groups, versions, and resources. * When a request matches a given rule, the request is directed to the priority level specified in the associated PriorityLevelConfiguration. * Can use to set the order of evaluation when multiple FlowSchemas match a request to ensure that certain rules take precedence. |

Configuring API with PriorityLevelConfigurations and FlowSchemas enables the prioritization of critical API requests over less important requests. This ensures that essential operations don't starve or experience delays because of lower priority requests.

**Optimize labeling and selectors**

When using LIST operations, optimize label selectors to narrow down the scope of the resources you want to query to reduce the amount of data returned and the load on the API server.

In Kubernetes CREATE and UPDATE operations refer to actions that manage and modify cluster resources.

### CREATE and UPDATE operations

**The CREATE operation creates new resources in the Kubernetes cluster**, such as pods, services, deployments, configmaps, and secrets. During a CREATE operation, a client, such as `kubectl`

or a controller, sends a request to the Kubernetes API server to create the new resource. The API server validates the request, ensures compliance with any admission controller policies, and then creates the resource in the cluster's desired state.

**The UPDATE operation modifies existing resources in the Kubernetes cluster**, including changes to resources specifications, like number of replicas, container images, environment variables, or labels. During an UPDATE operation, a client sends a request to the API server to update an existing resource. The API server validates the request, applies the changes to the resource definition, and updates the cluster resource.

CREATE and UPDATE operations can impact the performance of the Kubernetes API server under the following conditions:

**High concurrency**: When multiple users or applications make concurrent CREATE or UPDATE requests, it can lead to a surge in API requests arriving at the server at the same time. This can stress the API server's processing capacity and cause performance issues.**Complex resource definitions**: Resource definitions that are overly complex or involve multiple nested objects can increase the time it takes for the API server to validate and process CREATE and UPDATE requests, which can lead to performance degradation.**Resource validation and admission control**: Kubernetes enforces various admission control policies and validation checks on incoming CREATE and UPDATE requests. Large resource definitions, like ones with extensive annotations or configurations, might require more processing time.**Custom controllers**: Custom controllers that watch for changes in resources, like Deployments or StatefulSet controllers, can generate a significant number of updates when scaling or rolling out changes. These updates can strain the API server's resources.

For more information, see [Troubleshoot API server and etcd problems in AKS](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-apiserver-etcd).

## Data plane performance

The Kubernetes data plane is responsible for managing network traffic between containers and services. Issues with the data plane can lead to slow response times, degraded performance, and application downtime. It's important to carefully monitor and optimize data plane configurations, such as network latency, resource allocation, container density, and network policies, to ensure your containerized applications run smoothly and efficiently.

### Storage types

AKS recommends and defaults to using ephemeral OS disks. Ephemeral OS disks are created on local VM storage and aren't saved to remote Azure storage like managed OS disks. They have faster reimaging and boot times, enabling faster cluster operations, and they provide lower read/write latency on the OS disk of AKS agent nodes. Ephemeral OS disks work well for stateless workloads, where applications are tolerant of individual VM failures but not of VM deployment time or individual VM reimaging instances. Only certain VM SKUs support ephemeral OS disks, so you need to ensure that your desired SKU generation and size is compatible. For more information, see [Ephemeral OS disks in Azure Kubernetes Service (AKS)](cluster-configuration#use-ephemeral-os-on-new-clusters).

If your workload is unable to use ephemeral OS disks, AKS defaults to using Premium SSD OS disks. If Premium SSD OS disks aren't compatible with your workload, AKS defaults to Standard SSD disks. Currently, the only other available OS disk type is Standard HDD. For more information, see [Storage options in Azure Kubernetes Service (AKS)](concepts-storage).

The following table provides a breakdown of suggested use cases for OS disks supported in AKS:

| OS disk type | Key features | Suggested use cases |
|---|---|---|
| Ephemeral OS disks | * Faster reimaging and boot times. * Lower read/write latency on OS disk of AKS agent nodes. * High performance and availability. |
* Demanding enterprise workloads, such as SQL Server, Oracle, Dynamics, Exchange Server, MySQL, Cassandra, MongoDB, SAP Business Suite, etc. * Stateless production workloads that require high availability and low latency. |
| Premium SSD OS disks | * Consistent performance and low latency. * High availability. |
* Demanding enterprise workloads, such as SQL Server, Oracle, Dynamics, Exchange Server, MySQL, Cassandra, MongoDB, SAP Business Suite, etc. * Input/output (IO) intensive enterprise workloads. |
| Standard SSD OS disks | * Consistent performance. * Better availability and latency compared to Standard HDD disks. |
* Web servers. * Low input/output operations per second (IOPS) application servers. * Lightly used enterprise applications. * Dev/test workloads. |
| Standard HDD disks | * Low cost. * Exhibits variability in performance and latency. |
* Backup storage. * Mass storage with infrequent access. |

#### IOPS and throughput

Input/output operations per second (IOPS) refers to the number of read and write operations that a disk can perform in a second. Throughput refers to the amount of data that can be transferred in a given time period.

OS disks are responsible for storing the operating system and its associated files, and the VMs are responsible for running the applications. When selecting a VM, ensure the size and performance of the OS disk and VM SKU don't have a large discrepancy. A discrepancy in size or performance can cause performance issues and resource contention. For example, if the OS disk is significantly smaller than the VMs, it can limit the amount of space available for application data and cause the system to run out of disk space. If the OS disk has lower performance than the VMs, it can become a bottleneck and limit the overall performance of the system. Make sure the size and performance are balanced to ensure optimal performance in Kubernetes.

You can use the following steps to monitor IOPS and bandwidth meters on OS disks in the Azure portal:

- Navigate to the
[Azure portal](https://portal.azure.com/). - Search for
**Virtual machine scale sets**and select your virtual machine scale set. - Under
**Monitoring**, select**Metrics**.

Ephemeral OS disks can provide dynamic IOPS and throughput for your application, whereas managed disks have capped IOPS and throughput. For more information, see [Ephemeral OS disks for Azure VMs](/en-us/azure/virtual-machines/ephemeral-os-disks).

[Azure Premium SSD v2](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2) is designed for IO-intense enterprise workloads that require sub-millisecond disk latencies and high IOPS and throughput at a low cost. It's suited for a broad range of workloads, such as SQL server, Oracle, MariaDB, SAP, Cassandra, MongoDB, big data/analytics, gaming, and more. This disk type is the highest performing option currently available for persistent volumes.

### Pod scheduling

The memory and CPU resources allocated to a VM have a direct impact on the performance of the pods running on the VM. When a pod is created, it's assigned a certain amount of memory and CPU resources, which are used to run the application. If the VM doesn't have enough memory or CPU resources available, it can cause the pods to slow down or even crash. If the VM has too much memory or CPU resources available, it can cause the pods to run inefficiently, wasting resources and increasing costs. We recommend monitoring the total pod requests across your workloads against the total allocatable resources for best scheduling predictability and performance. You can also set the maximum pods per node based on your capacity planning using `--max-pods`

.


---

<!-- DOCUMENTO FUSIONADO: concepts-identity.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-identity -->

# Access and identity options for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can authenticate, authorize, secure, and control access to Kubernetes clusters in a variety of ways:

- Using Kubernetes role-based access control (Kubernetes RBAC), you can grant users, groups, and service accounts access to only the resources they need.
- With Azure Kubernetes Service (AKS), you can further enhance the security and permissions structure using Microsoft Entra ID and Azure RBAC.

Kubernetes RBAC and AKS help you secure your cluster access and provide only the minimum required permissions to developers and operators.

This article introduces the core concepts that help you authenticate and assign permissions in AKS.

## Kubernetes RBAC

Kubernetes RBAC provides granular filtering of user actions. With this control mechanism:

- You assign users or user groups permission to create and modify resources or view logs from running application workloads.
- You can scope permissions to a single namespace or across the entire AKS cluster.
- You create
*roles*to define permissions, and then assign those roles to users with*role bindings*.

For more information, see [Using Kubernetes RBAC authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/).

### Roles and ClusterRoles

#### Roles

Before assigning permissions to users with Kubernetes RBAC, you'll define user permissions as a *Role*. Grant permissions within a namespace using roles.

Note

Kubernetes roles *grant* permissions; they don't *deny* permissions.

To grant permissions across the entire cluster or to cluster resources outside a given namespace, you can instead use *ClusterRoles*.

#### ClusterRoles

A ClusterRole grants and applies permissions to resources across the entire cluster, not a specific namespace.

### RoleBindings and ClusterRoleBindings

Once you've defined roles to grant permissions to resources, you assign those Kubernetes RBAC permissions with a *RoleBinding*. If your AKS cluster [integrates with Microsoft Entra ID](#azure-ad-integration), RoleBindings grant permissions to Microsoft Entra users to perform actions within the cluster. See how in [Control access to cluster resources using Kubernetes role-based access control and Microsoft Entra identities](azure-ad-rbac).

#### RoleBindings

Assign roles to users for a given namespace using RoleBindings. With RoleBindings, you can logically segregate a single AKS cluster, only enabling users to access the application resources in their assigned namespace.

To bind roles across the entire cluster, or to cluster resources outside a given namespace, you instead use *ClusterRoleBindings*.

#### ClusterRoleBinding

With a ClusterRoleBinding, you bind roles to users and apply to resources across the entire cluster, not a specific namespace. This approach lets you grant administrators or support engineers access to all resources in the AKS cluster.

Note

Microsoft/AKS performs any cluster actions with user consent under a built-in Kubernetes role `aks-service`

and built-in role binding `aks-service-rolebinding`

.

This role enables AKS to troubleshoot and diagnose cluster issues, but can't modify permissions nor create roles or role bindings, or other high privilege actions. Role access is only enabled under active support tickets with just-in-time (JIT) access. Read more about [AKS support policies](support-policies).

### Kubernetes service accounts

*Service accounts* are one of the primary user types in Kubernetes. The Kubernetes API holds and manages service accounts. Service account credentials are stored as Kubernetes secrets, allowing them to be used by authorized pods to communicate with the API Server. Most API requests provide an authentication token for a service account or a normal user account.

Normal user accounts allow more traditional access for human administrators or developers, not just services and processes. While Kubernetes doesn't provide an identity management solution to store regular user accounts and passwords, you can integrate external identity solutions into Kubernetes. For AKS clusters, this integrated identity solution is Microsoft Entra ID.

For more information on the identity options in Kubernetes, see [Kubernetes authentication](https://kubernetes.io/docs/reference/access-authn-authz/authentication).

## Azure role-based access control

Azure role-based access control (RBAC) is an authorization system built on [Azure Resource Manager](/en-us/azure/azure-resource-manager/management/overview) that provides fine-grained access management of Azure resources.

| RBAC system | Description |
|---|---|
| Kubernetes RBAC | Designed to work on Kubernetes resources within your AKS cluster. |
| Azure RBAC | Designed to work on resources within your Azure subscription. |

With Azure RBAC, you create a *role definition* that outlines the permissions to be applied. You then assign a user or group this role definition via a *role assignment* for a particular *scope*. The scope can be an individual resource, a resource group, or across the subscription.

For more information, see [What is Azure role-based access control (Azure RBAC)?](/en-us/azure/role-based-access-control/overview)

There are two levels of access needed to fully operate an AKS cluster:

[Access the AKS resource in your Azure subscription](#azure-rbac-to-authorize-access-to-the-aks-resource).- Control scaling or upgrading your cluster using the AKS APIs.
- Pull your
`kubeconfig`

.

- Access to the Kubernetes API. This access is controlled by either:
[Kubernetes RBAC](#kubernetes-rbac)(traditionally).[Integrating Azure RBAC with AKS for Kubernetes authorization](#azure-rbac-for-kubernetes-authorization).


### Azure RBAC to authorize access to the AKS resource

With Azure RBAC, you can provide your users (or identities) with granular access to AKS resources across one or more subscriptions. For example, you could use the [Azure Kubernetes Service Contributor role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-contributor-role) to scale and upgrade your cluster. Meanwhile, another user with the [Azure Kubernetes Service Cluster Admin role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-cluster-admin-role) only has permission to pull the Admin `kubeconfig`

.

[Use Azure RBAC to define access to the Kubernetes configuration file in AKS](control-kubeconfig-access).

### Azure RBAC for Kubernetes Authorization

With the Azure RBAC integration, AKS will use a Kubernetes Authorization webhook server so you can manage Microsoft Entra integrated Kubernetes cluster resource permissions and assignments using Azure role definition and role assignments.

As shown in the above diagram, when using the Azure RBAC integration, all requests to the Kubernetes API will follow the same authentication flow as explained on the [Microsoft Entra integration section](#azure-ad-integration).

If the identity making the request exists in Microsoft Entra ID, Azure will team with Kubernetes RBAC to authorize the request. If the identity exists outside of Microsoft Entra ID (i.e., a Kubernetes service account), authorization will defer to the normal Kubernetes RBAC.

In this scenario, you use Azure RBAC mechanisms and APIs to assign users built-in roles or create custom roles, just as you would with Kubernetes roles.

With this feature, you not only give users permissions to the AKS resource across subscriptions, but you also configure the role and permissions for inside each of those clusters controlling Kubernetes API access. For example, you can grant the `Azure Kubernetes Service RBAC Reader`

role on the subscription scope. The role recipient will be able to list and get all Kubernetes objects from all clusters without modifying them.

Important

You need to enable Azure RBAC for Kubernetes authorization before using this feature. For more details and step by step guidance, follow our [Use Azure RBAC for Kubernetes Authorization](manage-azure-rbac) how-to guide.

#### Built-in roles

AKS provides the following four built-in roles. They are similar to the [Kubernetes built-in roles](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#user-facing-roles) with a few differences, like supporting CRDs. See the full list of actions allowed by each [Azure built-in role](/en-us/azure/role-based-access-control/built-in-roles).

| Role | Description |
|---|---|
| Azure Kubernetes Service RBAC Reader | Allows read-only access to see most objects in a namespace. Doesn't allow viewing roles or role bindings. Doesn't allow viewing `Secrets` . Reading the `Secrets` contents enables access to `ServiceAccount` credentials in the namespace, which would allow API access as any `ServiceAccount` in the namespace (a form of privilege escalation). |
| Azure Kubernetes Service RBAC Writer | Allows read/write access to most objects in a namespace. Doesn't allow viewing or modifying roles, or role bindings. Allows accessing `Secrets` and running pods as any ServiceAccount in the namespace, so it can be used to gain the API access levels of any ServiceAccount in the namespace. |
| Azure Kubernetes Service RBAC Admin | Allows admin access, intended to be granted within a namespace. Allows read/write access to most resources in a namespace (or cluster scope), including the ability to create roles and role bindings within the namespace. Doesn't allow write access to resource quota or to the namespace itself. |
| Azure Kubernetes Service RBAC Cluster Admin | Allows super-user access to perform any action on any resource. Gives full control over every resource in the cluster and in all namespaces. |

## Microsoft Entra integration

Enhance your AKS cluster security with Microsoft Entra integration. Built on decades of enterprise identity management, Microsoft Entra ID is a multi-tenant, cloud-based directory and identity management service that combines core directory services, application access management, and identity protection. With Microsoft Entra ID, you can integrate on-premises identities into AKS clusters to provide a single source for account management and security.

With Microsoft Entra integrated AKS clusters, you can grant users or groups access to Kubernetes resources within a namespace or across the cluster.

- To obtain a
`kubectl`

configuration context, a user runs the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. - When a user interacts with the AKS cluster with
`kubectl`

, they're prompted to sign in with their Microsoft Entra credentials.

This approach provides a single source for user account management and password credentials. The user can only access the resources as defined by the cluster administrator.

Microsoft Entra authentication is provided to AKS clusters with OpenID Connect. OpenID Connect is an identity layer built on top of the OAuth 2.0 protocol. For more information on OpenID Connect, see the [OpenID Connect documentation](/en-us/azure/active-directory/develop/v2-protocols-oidc). From inside of the Kubernetes cluster, [Webhook Token Authentication](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#webhook-token-authentication) is used to verify authentication tokens. Webhook token authentication is configured and managed as part of the AKS cluster.

### Webhook and API server

As shown in the graphic above, the API server calls the AKS webhook server and performs the following steps:

`kubectl`

uses the Microsoft Entra client application to sign in users with[OAuth 2.0 device authorization grant flow](/en-us/azure/active-directory/develop/v2-oauth2-device-code).- Microsoft Entra ID provides an access_token, id_token, and a refresh_token.
- The user makes a request to
`kubectl`

with an access_token from`kubeconfig`

. `kubectl`

sends the access_token to API Server.- The API Server is configured with the Auth WebHook Server to perform validation.
- The authentication webhook server confirms the JSON Web Token signature is valid by checking the Microsoft Entra public signing key.
- If the user is a member of more than 200 groups, the server application uses user-provided credentials to query group memberships of the logged-in user from the MS Graph API. For users with group memberships of 200 or fewer the groups claim already exists in the client token. No query will be performed.
- A response is sent to the API Server with user information such as the user principal name (UPN) claim of the access token, and the group membership of the user based on the object ID.
- The API performs an authorization decision based on the Kubernetes Role/RoleBinding.
- Once authorized, the API server returns a response to
`kubectl`

. `kubectl`

provides feedback to the user.

Learn how to integrate AKS with Microsoft Entra ID with our [AKS-managed Microsoft Entra integration how-to guide](managed-azure-ad).

## AKS service permissions

When creating a cluster, AKS generates or modifies resources it needs (like VMs and NICs) to create and run the cluster on behalf of the user. This identity is distinct from the cluster's identity permission, which is created during cluster creation.

### Identity creating and operating the cluster permissions

The following permissions are needed by the identity creating and operating the cluster.

| Permission | Reason |
|---|---|
`Microsoft.Compute/diskEncryptionSets/read` |
Required to read disk encryption set ID. |
`Microsoft.Compute/proximityPlacementGroups/write` |
Required for updating proximity placement groups. |
`Microsoft.Network/applicationGateways/read` `Microsoft.Network/applicationGateways/write` `Microsoft.Network/virtualNetworks/subnets/join/action` |
Required to configure application gateways and join the subnet. |
`Microsoft.Network/virtualNetworks/subnets/join/action` |
Required to configure the Network Security Group for the subnet when using a custom VNET. |
`Microsoft.Network/publicIPAddresses/join/action` `Microsoft.Network/publicIPPrefixes/join/action` |
Required to configure the outbound public IPs on the Standard Load Balancer. |
`Microsoft.OperationalInsights/workspaces/sharedkeys/read` `Microsoft.OperationalInsights/workspaces/read` `Microsoft.OperationsManagement/solutions/write` `Microsoft.OperationsManagement/solutions/read` `Microsoft.ManagedIdentity/userAssignedIdentities/assign/action` |
Required to create and update Log Analytics workspaces and Azure monitoring for containers. |
`Microsoft.Network/virtualNetworks/joinLoadBalancer/action` |
Required to configure the IP-based Load Balancer Backend Pools. |

### AKS cluster identity permissions

The following permissions are used by the AKS cluster identity, which is created and associated with the AKS cluster. Each permission is used for the reasons below:

| Permission | Reason |
|---|---|
`Microsoft.ContainerService/managedClusters/*` |
Required for creating users and operating the cluster |
`Microsoft.Network/loadBalancers/delete` `Microsoft.Network/loadBalancers/read` `Microsoft.Network/loadBalancers/write` |
Required to configure the load balancer for a LoadBalancer service. |
`Microsoft.Network/publicIPAddresses/delete` `Microsoft.Network/publicIPAddresses/read` `Microsoft.Network/publicIPAddresses/write` |
Required to find and configure public IPs for a LoadBalancer service. |
`Microsoft.Network/publicIPAddresses/join/action` |
Required for configuring public IPs for a LoadBalancer service. |
`Microsoft.Network/networkSecurityGroups/read` `Microsoft.Network/networkSecurityGroups/write` |
Required to create or delete security rules for a LoadBalancer service. |
`Microsoft.Compute/disks/delete` `Microsoft.Compute/disks/read` `Microsoft.Compute/disks/write` `Microsoft.Compute/locations/DiskOperations/read` |
Required to configure AzureDisks. |
`Microsoft.Storage/storageAccounts/delete` `Microsoft.Storage/storageAccounts/listKeys/action` `Microsoft.Storage/storageAccounts/read` `Microsoft.Storage/storageAccounts/write` `Microsoft.Storage/operations/read` |
Required to configure storage accounts for AzureFile or AzureDisk. |
`Microsoft.Network/routeTables/read` `Microsoft.Network/routeTables/routes/delete` `Microsoft.Network/routeTables/routes/read` `Microsoft.Network/routeTables/routes/write` `Microsoft.Network/routeTables/write` |
Required to configure route tables and routes for nodes. |
`Microsoft.Compute/virtualMachines/read` |
Required to find information for virtual machines in a VMAS, such as zones, fault domain, size, and data disks. |
`Microsoft.Compute/virtualMachines/write` |
Required to attach AzureDisks to a virtual machine in a VMAS. |
`Microsoft.Compute/virtualMachineScaleSets/read` `Microsoft.Compute/virtualMachineScaleSets/virtualMachines/read` `Microsoft.Compute/virtualMachineScaleSets/virtualmachines/instanceView/read` |
Required to find information for virtual machines in a virtual machine scale set, such as zones, fault domain, size, and data disks. |
`Microsoft.Network/networkInterfaces/write` |
Required to add a virtual machine in a VMAS to a load balancer backend address pool. |
`Microsoft.Compute/virtualMachineScaleSets/write` |
Required to add a virtual machine scale set to a load balancer backend address pools and scale out nodes in a virtual machine scale set. |
`Microsoft.Compute/virtualMachineScaleSets/delete` |
Required to delete a virtual machine scale set to a load balancer backend address pools and scale down nodes in a virtual machine scale set. |
`Microsoft.Compute/virtualMachineScaleSets/virtualmachines/write` |
Required to attach AzureDisks and add a virtual machine from a virtual machine scale set to the load balancer. |
`Microsoft.Network/networkInterfaces/read` |
Required to search internal IPs and load balancer backend address pools for virtual machines in a VMAS. |
`Microsoft.Compute/virtualMachineScaleSets/virtualMachines/networkInterfaces/read` |
Required to search internal IPs and load balancer backend address pools for a virtual machine in a virtual machine scale set. |
`Microsoft.Compute/virtualMachineScaleSets/virtualMachines/networkInterfaces/ipconfigurations/publicipaddresses/read` |
Required to find public IPs for a virtual machine in a virtual machine scale set. |
`Microsoft.Network/virtualNetworks/read` `Microsoft.Network/virtualNetworks/subnets/read` |
Required to verify if a subnet exists for the internal load balancer in another resource group. |
`Microsoft.Compute/snapshots/delete` `Microsoft.Compute/snapshots/read` `Microsoft.Compute/snapshots/write` |
Required to configure snapshots for AzureDisk. |
`Microsoft.Compute/locations/vmSizes/read` `Microsoft.Compute/locations/operations/read` |
Required to find virtual machine sizes for finding AzureDisk volume limits. |

### Additional cluster identity permissions

When creating a cluster with specific attributes, you will need the following additional permissions for the cluster identity. Since these permissions are not automatically assigned, you must add them to the cluster identity after it's created.

| Permission | Reason |
|---|---|
`Microsoft.Network/networkSecurityGroups/write` `Microsoft.Network/networkSecurityGroups/read` |
Required if using a network security group in another resource group. Required to configure security rules for a LoadBalancer service. |
`Microsoft.Network/virtualNetworks/subnets/read` `Microsoft.Network/virtualNetworks/subnets/join/action` |
Required if using a subnet in another resource group such as a custom VNET. |
`Microsoft.Network/routeTables/routes/read` `Microsoft.Network/routeTables/routes/write` |
Required if using a subnet associated with a route table in another resource group such as a custom VNET with a custom route table. Required to verify if a subnet already exists for the subnet in the other resource group. |
`Microsoft.Network/virtualNetworks/subnets/read` |
Required if using an internal load balancer in another resource group. Required to verify if a subnet already exists for the internal load balancer in the resource group. |
`Microsoft.Network/privatednszones/*` |
Required if using a private DNS zone in another resource group such as a custom privateDNSZone. |

## AKS Node Access

By default Node Access is not required for AKS. The following access is needed for the node if a specific component is leveraged.

| Access | Reason |
|---|---|
`kubelet` |
Required to grant MSI access to ACR. |
`http app routing` |
Required for write permission to "random name".aksapp.io. |
`container insights` |
Required to grant permission to the Log Analytics workspace. |

## Summary

View the table for a quick summary of how users can authenticate to Kubernetes when Microsoft Entra integration is enabled. In all cases, the user's sequence of commands is:

Run

`az login`

to authenticate to Azure.Run

`az aks get-credentials`

to download credentials for the cluster into`.kube/config`

.Run

`kubectl`

commands.- The first command may trigger browser-based authentication to authenticate to the cluster, as described in the following table.


In the Azure portal, you can find:

- The
*Role Grant*(Azure RBAC role grant) referred to in the second column is shown on the**Access Control**tab. - The Cluster Admin Microsoft Entra group is shown on the
**Configuration**tab.- Also found with parameter name
`--aad-admin-group-object-ids`

in the Azure CLI.

- Also found with parameter name

| Description | Role grant required | Cluster admin Microsoft Entra group(s) | When to use |
|---|---|---|---|
| Legacy admin login using client certificate | Azure Kubernetes Service Cluster Admin Role. This role allows `az aks get-credentials` to be used with the `--admin` flag, which downloads a
`.kube/config` . This is the only purpose of "Azure Kubernetes Service Cluster Admin Role". |
n/a | If you're permanently blocked by not having access to a valid Microsoft Entra group with access to your cluster. |
| Microsoft Entra ID with manual (Cluster)RoleBindings | Azure Kubernetes Service Cluster User Role. The "User" role allows `az aks get-credentials` to be used without the `--admin` flag. (This is the only purpose of "Azure Kubernetes Service Cluster User Role".) The result, on a Microsoft Entra ID-enabled cluster, is the download of
`.kube/config` , which triggers browser-based authentication when it's first used by `kubectl` . |
User is not in any of these groups. Because the user is not in any Cluster Admin groups, their rights will be controlled entirely by any RoleBindings or ClusterRoleBindings that have been set up by cluster admins. The (Cluster)RoleBindings
`subjects` . If no such bindings have been set up, the user will not be able to excute any `kubectl` commands. |

`cluster-admin`

Kubernetes role. So users in these groups can run all `kubectl`

commands as `cluster-admin`

.*not*using Azure RBAC for Kubernetes authorization.First,

**Azure Kubernetes Service Cluster User Role**(as above).Second, one of the "Azure Kubernetes Service

**RBAC**..." roles listed above, or your own custom alternative.## Next steps

- To get started with Microsoft Entra ID and Kubernetes RBAC, see
[Integrate Microsoft Entra ID with AKS](managed-azure-ad). - For associated best practices, see
[Best practices for authentication and authorization in AKS](operator-best-practices-identity). - To get started with Azure RBAC for Kubernetes Authorization, see
[Use Azure RBAC to authorize access within the Azure Kubernetes Service (AKS) Cluster](manage-azure-rbac). - To get started securing your
`kubeconfig`

file, see[Limit access to cluster configuration file](control-kubeconfig-access). - To get started with managed identities in AKS, see
[Use a managed identity in AKS](use-managed-identity).

For more information on core Kubernetes and AKS concepts, see the following articles:
