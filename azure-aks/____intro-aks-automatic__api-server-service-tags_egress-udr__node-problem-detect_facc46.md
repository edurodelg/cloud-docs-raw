---
merged_at: 2026-01-25T15:16:21.156743
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___intro-aks-automatic__api-server-service-tags_egress-udr__node-problem-detecto_af7dcb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __intro-aks-automatic__api-server-service-tags_egress-udr__node-problem-detector_b8ec1d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _intro-aks-automatic__api-server-service-tags_egress-udr.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: intro-aks-automatic.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/intro-aks-automatic -->

# What is Azure Kubernetes Service (AKS) Automatic?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic

Azure Kubernetes Service (AKS) Automatic offers an experience that makes the most common tasks on Kubernetes fast and frictionless, while preserving the flexibility, extensibility, and consistency of Kubernetes. Azure takes care of your cluster setup, including node management, scaling, security, and preconfigured settings that follow AKS well-architected recommendations. Automatic clusters dynamically allocate compute resources based on your specific workload requirements and are tuned for running production applications.

**Production ready by default**: Clusters are preconfigured for optimal production use, suitable for most applications. They offer fully managed node pools that automatically allocate and scale resources based on your workload needs. Pods are bin packed efficiently, to maximize resource utilization.**Built-in best practices and safeguards**: AKS Automatic clusters have a hardened default configuration, with many cluster, application, and networking security settings enabled by default. AKS automatically patches your nodes and cluster components while adhering to any planned maintenance schedules.**Code to Kubernetes in minutes**: Go from a container image to a deployed application that adheres to best practices patterns within minutes, with access to the comprehensive capabilities of the Kubernetes API and its rich ecosystem.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## AKS Automatic and Standard feature comparison

The following table provides a comparison of options that are available, preconfigured, and default in both AKS Automatic and AKS Standard. For more information on whether specific features are available in Automatic, you can check the documentation for that feature.

**Preconfigured** features are always enabled and you can't disable or change their settings. **Default** features are configured for you but can be changed. **Optional** features are available for you to configure and aren't enabled by default.

When enabling optional features, you can follow the linked feature documentation. When you reach a step for cluster creation, follow steps to create an [AKS Automatic cluster](learn/quick-kubernetes-automatic-deploy) instead of creating an AKS Standard cluster.

### Application deployment, monitoring, and observability

Application deployment can be streamlined using [automated deployments](automated-deployments) from source control, which creates Kubernetes manifest and generates CI/CD workflows. Additionally, the cluster is configured with monitoring tools such as Managed Prometheus for metrics, Managed Grafana for visualization, and Container Insights for log collection.

| Option | AKS Automatic | AKS Standard |
|---|---|---|
| Application deployment | Optional: * Use
* Create deployment pipelines using
* Bring your own CI/CD pipeline. |
Optional: * Use
* Create deployment pipelines using
* Bring your own CI/CD pipeline. |
| Monitoring, logging, and visualization | Default: *
*
*
*
Optional: *
|
Default:
Optional: *
*
*
*
|

### Node management, scaling, and cluster operations

Node management is automatically handled without the need for manual node pool creation. Scaling is seamless, with nodes created based on workload requests. Additionally, features for workload scaling like Horizontal Pod Autoscaler (HPA), [Kubernetes Event Driven Autoscaling (KEDA)](keda-about), and [Vertical Pod Autoscaler (VPA)](vertical-pod-autoscaler) are enabled. Clusters are configured for automatic node repair, automatic cluster upgrades, and detection of deprecated Kubernetes standard API usage. You can also set a planned maintenance schedule for upgrades if needed.

| Option | AKS Automatic | AKS Standard |
|---|---|---|
| Node management | Preconfigured: AKS Automatic manages the node pools using
|
Default: You create and manage system and user node pools Optional: AKS Standard manages user node pools using
|
| Scaling | Preconfigured: AKS Automatic creates nodes based on workload requests using
|
Default: Manual scaling of node pools. Optional: *
*
*
*
|
| Cluster tier and Service Level Agreement (SLA) | Preconfigured: Standard tier cluster with up to 5,000 nodes, a
|
Default: Free tier cluster with 10 nodes but can support up to 1,000 nodes. Optional: * Standard tier cluster with up to 5,000 nodes and a
* Premium tier cluster with up to 5,000 nodes,
|
| Node operating system | Preconfigured:
|
Default: Ubuntu Optional: *
*
|
| Node resource group | Preconfigured: Fully managed node resource group to prevent accidental or intentional changes to cluster resources. |
Default: Unrestricted Optional:
|
| Node auto-repair | Preconfigured: Continuously monitors the health state of worker nodes and performs
|
Preconfigured: Continuously monitors the health state of worker nodes and performs
|
| Cluster upgrades | Preconfigured: Clusters are
|
Default: Manual upgrade. Optional: Automatic upgrade using a selectable
|
| Kubernetes API breaking change detection | Preconfigured: Cluster upgrades are stopped on detection of
|
Preconfigured: Cluster upgrades are stopped on detection of
|
| Planned maintenance windows | Default: Set
|
Optional: Set
|

### Security and policies

Cluster authentication and authorization use [Azure Role-based Access Control (RBAC) for Kubernetes authorization](manage-azure-rbac) and applications can use features like [workload identity with Microsoft Entra Workload ID](workload-identity-overview) and [OpenID Connect (OIDC) cluster issuer](use-oidc-issuer) to have secure communication with Azure services. [Deployment safeguards](deployment-safeguards) enforce Kubernetes best practices through Azure Policy controls and the built-in [image cleaner](image-cleaner) removes unused images with vulnerabilities, enhancing image security.

| Option | AKS Automatic | AKS Standard |
|---|---|---|
| Cluster authentication and authorization | Preconfigured:
|
Default: Local accounts. Optional: *
*
|
| Cluster security | Preconfigured:
|
Optional:
|
| Application security | Preconfigured: *
*
Optional:*
|
Optional: *
*
Optional:*
|
| Image security | Preconfigured:
|
Optional:
|
| Policy enforcement | Preconfigured:
Optional:*
|
Optional:
Optional:*
|
| Managed namespaces | Optional: Use
|
Optional: Use
|

### Networking

AKS Automatic clusters use [managed Virtual Network powered by Azure CNI Overlay with Cilium](azure-cni-powered-by-cilium) for high-performance networking and robust security. Ingress is handled by [managed NGINX using the application routing add-on](app-routing), integrating seamlessly with Azure DNS and Azure Key Vault. Egress uses a [managed NAT gateway](nat-gateway#create-an-aks-cluster-with-a-managed-nat-gateway) for scalable outbound connections. Additionally, you have the flexibility to enable [Istio-based service mesh add-on for AKS](istio-about) or bring your own service mesh.

| Option | AKS Automatic | AKS Standard |
|---|---|---|
| Virtual network | Default:
Optional: *
*
|
Default:
Optional: *
*
*
*
|
| Ingress | Preconfigured:
Optional: *
* Bring your own ingress or gateway. |
Optional: *
*
* Bring your own ingress or gateway. |
| Egress | Preconfigured:
Optional (with custom virtual network): *
*
*
|
Default:
Optional: *
*
*
|
| Service mesh | Optional: *
* Bring your own service mesh. |
Optional: *
* Bring your own service mesh. |

## Next steps

To learn more about AKS Automatic, follow the quickstart to create a cluster.


---

<!-- DOCUMENTO FUSIONADO: _api-server-service-tags_egress-udr.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: api-server-service-tags.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/api-server-service-tags -->

# Use service tags for API server authorized IP ranges in Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Service tags for API server authorized IP ranges is a preview feature that allows you to use service tags to specify authorized IP ranges for the API server in Azure Kubernetes Service (AKS). This feature simplifies the management of authorized IP ranges by allowing you to use predefined service tags instead of manually specifying individual IP addresses or CIDR ranges.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Prerequisites

- The Azure CLI version 2.0.76 or later installed and configured. Check your version using the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - The
installed.`aks-preview`

Azure CLI extension - The
registered in your Azure subscription.`EnableServiceTagAuthorizedIPPreview`

feature flag

## Limitations

- This feature isn't compatible with
[API Server VNet Integration](api-server-vnet-integration). - Only one service tag is allowed in the
`--api-server-authorized-ip-ranges`

parameter. You can't specify multiple service tags.

## Install the `aks-preview`

Azure CLI extension

Install the Azure CLI preview extension using the

command.`az extension add`

`az extension add --name aks-preview`

Update the extension to make sure you have the latest version using the

command.`az extension update`

`az extension update --name aks-preview`


## Register the service tag authorized IP feature flag

Register the

`EnableServiceTagAuthorizedIPPreview`

feature flag using thecommand. It takes a few minutes for the registration to complete.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "EnableServiceTagAuthorizedIPPreview"`

Example output:

`{ "id": "/subscriptions/<subscription-id>/providers/Microsoft.ContainerService/features/EnableServiceTagAuthorizedIPPreview", "name": "EnableServiceTagAuthorizedIPPreview", "properties": { "state": "Registering" }, "type": "Microsoft.ContainerService/features" }`

Once the feature flag state changes from

`Registering`

to`Registered`

, refresh the registration of the`Microsoft.ContainerService`

resource provider using thecommand.`az provider register`

`az provider register --namespace "Microsoft.ContainerService"`

Verify the registration using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "EnableServiceTagAuthorizedIPPreview"`

Example output:

`{ "id": "/subscriptions/<subscription-id>/providers/Microsoft.ContainerService/features/EnableServiceTagAuthorizedIPPreview", "name": "EnableServiceTagAuthorizedIPPreview", "properties": { "state": "Registered" }, "type": "Microsoft.ContainerService/features" }`


## Create an AKS cluster with service tag authorized IP ranges

Create a cluster with service tag authorized IP ranges using the

command with the`az aks create`

`--api-server-authorized-ip-ranges`

parameter. The following example creates a cluster named*myAKSCluster*in the*myResourceGroup*resource group and authorizes the`AzureCloud`

service tag to allow all Azure services to access the API server and specify an extra IP address:`az aks create --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges AzureCloud,20.20.20.20`

Note

You should be able to curl the API server from an Azure virtual machine (VM) or Azure service that's part of the

`AzureCloud`

service tag.


---

<!-- DOCUMENTO FUSIONADO: egress-udr.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/egress-udr -->

# Customize cluster egress with a user-defined routing table in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can customize the egress for your Azure Kubernetes Service (AKS) clusters to fit specific scenarios. AKS provisions a `Standard`

SKU load balancer for egress by default. However, the default setup may not meet the requirements of all scenarios if public IPs are disallowed or the scenario requires extra hops for egress.

This article walks through how to customize a cluster's egress route to support custom network scenarios. These scenarios include ones which disallow public IPs and require the cluster to sit behind a network virtual appliance (NVA).

## Prerequisites

- Azure CLI version 2.0.81 or greater. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - API version
`2020-01-01`

or greater.

## Requirements and limitations

Using outbound type is an advanced networking scenario and requires proper network configuration. The following requirements and limitations apply to using outbound type:

- Setting
`outboundType`

requires AKS clusters with a`vm-set-type`

of`VirtualMachineScaleSets`

and a`load-balancer-sku`

of`Standard`

. - Setting
`outboundType`

to a value of`UDR`

requires a user-defined route with valid outbound connectivity for the cluster. - Setting
`outboundType`

to a value of`UDR`

implies the ingress source IP routed to the load-balancer may**not match**the cluster's outgoing egress destination address.

## Overview of customizing egress with a user-defined routing table

AKS doesn't automatically configure egress paths if `userDefinedRouting`

is set, which means you must configure the egress.

When you don't use standard load balancer (SLB) architecture, you must establish explicit egress. You must deploy your AKS cluster into an existing virtual network with a subnet that has been previously configured. This architecture requires explicitly sending egress traffic to an appliance like a firewall, gateway, or proxy, so a public IP assigned to the standard load balancer or appliance can handle the Network Address Translation (NAT).

### Load balancer creation with `userDefinedRouting`


AKS clusters with an outbound type of UDR get a standard load balancer only when the first Kubernetes service of type `loadBalancer`

is deployed. The load balancer is configured with a public IP address for *inbound* requests and a backend pool for *inbound* requests. The Azure cloud provider configures inbound rules, but it **doesn't configure outbound public IP address or outbound rules**. Your UDR is the only source for egress traffic.

Note

Azure load balancers [don't incur a charge until a rule is placed](https://azure.microsoft.com/pricing/details/load-balancer/).

## Deploy a cluster with outbound type of UDR and Azure Firewall

To see an application of a cluster with outbound type using a user-defined route, see this [restrict egress traffic with Azure firewall example](limit-egress-traffic).

Important

Outbound type of UDR requires a route for 0.0.0.0/0 and a next hop destination of NVA in the route table.
The route table already has a default 0.0.0.0/0 to the Internet. Without a public IP address for Azure to use for Source Network Address Translation (SNAT), simply adding this route won't provide you outbound Internet connectivity. AKS validates that you don't create a 0.0.0.0/0 route pointing to the Internet but instead to a gateway, NVA, etc.
When using an outbound type of UDR, a load balancer public IP address for **inbound requests** isn't created unless you configure a service of type *loadbalancer*. AKS never creates a public IP address for **outbound requests** if you set an outbound type of UDR.

## Next steps

For more information on user-defined routes and Azure networking, see:


---

<!-- DOCUMENTO FUSIONADO: _node-problem-detector_istio-cni.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: node-problem-detector.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-problem-detector -->

# Node Problem Detector (NPD) in Azure Kubernetes Service (AKS) nodes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Node Problem Detector (NPD)](https://github.com/kubernetes/node-problem-detector) is an open source Kubernetes component that detects node-related problems and reports on them. It runs as a systemd serviced on each node in the cluster and collects various metrics and system information, such as CPU usage, disk usage, and network connectivity. When it detects a problem, it generates *events and/or node conditions*. Azure Kubernetes Service (AKS) uses NPD to monitor and manage nodes in a Kubernetes cluster running on the Azure cloud platform. The AKS Linux extension enables NPD by default.

Note

Upgrades to NPD are independent of the node image and Kubernetes version upgrade processes. If a node pool is unhealthy (that is, in a failed state), new NPD versions aren't installed.

## Node conditions

Node conditions indicate a permanent problem that makes the node unavailable. AKS uses the following node conditions from NPD to expose permanent problems on the node. NPD also emits corresponding Kubernetes events.

| Problem Daemon type | NodeCondition | Reason | Compute type |
|---|---|---|---|
| CustomPluginMonitor | FilesystemCorruptionProblem | FilesystemCorruptionDetected | General purpose |
| CustomPluginMonitor | KubeletProblem | KubeletIsDown | General purpose |
| CustomPluginMonitor | ContainerRuntimeProblem | ContainerRuntimeIsDown | General purpose |
| CustomPluginMonitor | VMEventScheduled | VMEventScheduled | General purpose |
| CustomPluginMonitor | FrequentUnregisterNetDevice | UnregisterNetDevice | General purpose |
| CustomPluginMonitor | FrequentKubeletRestart | FrequentKubeletRestart | General purpose |
| CustomPluginMonitor | FrequentContainerdRestart | FrequentContainerdRestart | General purpose |
| CustomPluginMonitor | FrequentDockerRestart | FrequentDockerRestart | General purpose |
| CustomPluginMonitor | GPUMissing | Observed GPU count does not match expected GPU count | GPU only |
| CustomPluginMonitor | NVLinkStatusInactive | NVLinkStatusInactive | GPU only |
| CustomPluginMonitor | XIDErrors | XID errors present in kernel log | GPU only |
| CustomPluginMonitor | IBLinkFlapping | Intermittent InfiniBand device connectivity | GPU only |
| SystemLogMonitor | KernelDeadlock | DockerHung | General purpose |
| SystemLogMonitor | ReadonlyFilesystem | FilesystemIsReadOnly | General purpose |

Note

The `GPU only`

node conditions currently apply to AKS node pools with `Standard_ND96asr_v4`

or `Standard_ND96isr_H100_v5`

VM size, and are supported on standard GPU and [MIG-enabled GPU node pools](gpu-multi-instance).

## Events

NPD emits events with relevant information to help you diagnose underlying issues.

| Problem Daemon type | Reason | Frequency | Description | Action |
|---|---|---|---|---|
| CustomPluginMonitor | EgressBlocked | 30 min | This event checks for connectivity to external
|

[https://aka.ms/aks/scheduledevents](https://aka.ms/aks/scheduledevents)for more information[https://aka.ms/aks/scheduledevents](https://aka.ms/aks/scheduledevents)for more information[https://aka.ms/aks/scheduledevents](https://aka.ms/aks/scheduledevents)for more information[https://aka.ms/aks/scheduledevents](https://aka.ms/aks/scheduledevents)for more information[https://aka.ms/aks/scheduledevents](https://aka.ms/aks/scheduledevents)for more informationIn certain instances, AKS automatically cordons and drains the node to minimize disruption to workloads. For more information about the events and actions, see [Node autodrain](/en-us/azure/aks/node-auto-repair#node-auto-drain).

### EgressBlocked

The list of endpoints checked by the EgressBlocked are listed below

Note

The actual endpoints will depend on the type of the cluster and the location where it's hosted (Public cloud vs Airgapped clouds). Review the documentation for outbound access [here](/en-us/azure/aks/outbound-rules-control-egress). The documentation is for public clouds

| Type | Example | Note |
|---|---|---|
| MCR |
|

## Check the node conditions and events

Check the node conditions and events using the

`kubectl describe node`

command.`kubectl describe node my-aks-node`

Your output should look similar to the following example condensed output:

`... ... Conditions: Type Status LastHeartbeatTime LastTransitionTime Reason Message ---- ------ ----------------- ------------------ ------ ------- VMEventScheduled False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 NoVMEventScheduled VM has no scheduled event FrequentContainerdRestart False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 NoFrequentContainerdRestart containerd is functioning properly FrequentDockerRestart False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 NoFrequentDockerRestart docker is functioning properly FilesystemCorruptionProblem False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 FilesystemIsOK Filesystem is healthy FrequentUnregisterNetDevice False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 NoFrequentUnregisterNetDevice node is functioning properly ContainerRuntimeProblem False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:40 +0000 ContainerRuntimeIsUp container runtime service is up KernelDeadlock False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 KernelHasNoDeadlock kernel has no deadlock FrequentKubeletRestart False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 NoFrequentKubeletRestart kubelet is functioning properly KubeletProblem False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 KubeletIsUp kubelet service is up ReadonlyFilesystem False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 FilesystemIsNotReadOnly Filesystem is not read-only NetworkUnavailable False Thu, 01 Jun 2023 03:58:39 +0000 Thu, 01 Jun 2023 03:58:39 +0000 RouteCreated RouteController created a route MemoryPressure True Thu, 01 Jun 2023 19:16:50 +0000 Thu, 01 Jun 2023 19:16:50 +0000 KubeletHasInsufficientMemory kubelet has insufficient memory available DiskPressure False Thu, 01 Jun 2023 19:16:50 +0000 Thu, 01 Jun 2023 03:57:22 +0000 KubeletHasNoDiskPressure kubelet has no disk pressure PIDPressure False Thu, 01 Jun 2023 19:16:50 +0000 Thu, 01 Jun 2023 03:57:22 +0000 KubeletHasSufficientPID kubelet has sufficient PID available Ready True Thu, 01 Jun 2023 19:16:50 +0000 Thu, 01 Jun 2023 03:57:23 +0000 KubeletReady kubelet is posting ready status. AppArmor enabled ... ... ... Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal NodeHasSufficientMemory 94s (x176 over 15h) kubelet Node aks-agentpool-40622340-vmss000009 status is now: NodeHasSufficientMemory`


These events are also available in [Container Insights](/en-us/azure/azure-monitor/containers/container-insights-overview) through [KubeEvents](/en-us/azure/azure-monitor/reference/tables/kubeevents).

## Metrics

NPD also exposes Prometheus metrics based on the node problems, which you can use for monitoring and alerting. These metrics are exposed on port 20257 of the Node IP and Prometheus can scrape them.

The following example YAML shows a scrape config you can use with the [Azure Managed Prometheus add on as a DaemonSet](/en-us/azure/azure-monitor/essentials/prometheus-metrics-scrape-configuration#advanced-setup-configure-custom-prometheus-scrape-jobs-for-the-daemonset):

```
kind: ConfigMap
apiVersion: v1
metadata:
name: ama-metrics-prometheus-config-node
namespace: kube-system
data:
prometheus-config: |-
global:
scrape_interval: 1m
scrape_configs:
- job_name: node-problem-detector
scrape_interval: 1m
scheme: http
metrics_path: /metrics
relabel_configs:
- source_labels: [__metrics_path__]
regex: (.*)
target_label: metrics_path
- source_labels: [__address__]
replacement: '$NODE_NAME'
target_label: instance
static_configs:
- targets: ['$NODE_IP:20257']
```


The following example shows the scraped metrics:

```
problem_gauge{reason="UnregisterNetDevice",type="FrequentUnregisterNetDevice"} 0
problem_gauge{reason="VMEventScheduled",type="VMEventScheduled"} 0
```


## Next steps

For more information on NPD, see [kubernetes/node-problem-detector](https://github.com/kubernetes/node-problem-detector).


---

<!-- DOCUMENTO FUSIONADO: istio-cni.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-cni -->

# Enable Istio CNI for Istio-based service mesh add-on for Azure Kubernetes Service (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to enable Istio CNI for the Istio-based service mesh add-on on Azure Kubernetes Service (AKS). Istio CNI improves security by eliminating the need for privileged network capabilities in application workloads within the service mesh.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Overview

By default, Istio service mesh uses privileged init containers (`istio-init`

) in each application pod to configure network traffic redirection to the Envoy sidecar proxy. These init containers require `NET_ADMIN`

and `NET_RAW`

capabilities, which are often flagged as security concerns in enterprise environments.

Istio CNI addresses this security concern by moving the network configuration responsibilities from individual pod init containers to a cluster-level CNI plugin. This approach:

**Improves security**: Removes the need for privileged network capabilities (`NET_ADMIN`

,`NET_RAW`

) from application workloads**Simplifies pod security policies**: Application pods only require minimal capabilities**Maintains functionality**: Provides the same traffic management capabilities as the traditional init container approach

When Istio CNI is enabled, application pods use a minimal `istio-validation`

init container that drops all capabilities instead of the privileged `istio-init`

container.

Note

Istio CNI is **not** a replacement for [Azure CNI](concepts-network-cni-overview) and will not interfere with your normal AKS networking. It is a separate plugin designed to handle Istio’s traffic redirection setup at the node level, improving security by removing the need for privileged init containers in application pods.

## Before you begin

Install the Azure CLI version 2.77.0 or later. You can run

`az --version`

to verify the version. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).Install the

`aks-preview`

Azure CLI extension version 19.0.0b5 or later:`az extension add --name aks-preview`

If you already have the

`aks-preview`

extension, update it to the latest version:`az extension update --name aks-preview`

Register the

`IstioCNIPreview`

feature flag on your Azure subscription:`az feature register --namespace "Microsoft.ContainerService" --name "IstioCNIPreview"`

Use the following command to check the registration status:

`az feature show --namespace "Microsoft.ContainerService" --name "IstioCNIPreview"`

It takes a few minutes for the feature to register. Verify the registration state shows

`Registered`

:`{ "id": "/subscriptions/xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/providers/Microsoft.Features/providers/Microsoft.ContainerService/features/IstioCNIPreview", "name": "Microsoft.ContainerService/IstioCNIPreview", "properties": { "state": "Registered" }, "type": "Microsoft.Features/providers/features" }`

You need an AKS cluster with the Istio-based service mesh add-on enabled. If you don't have this setup, see

[Deploy Istio-based service mesh add-on for Azure Kubernetes Service](istio-deploy-addon).Ensure your Istio service mesh is using revision

`asm-1-25`

or later. You can check the current revision with:`az aks show --resource-group <resource-group-name> --name <cluster-name> --query 'serviceMeshProfile.istio.revisions'`


Note

Istio CNI is not compatible with Ubuntu 20.04 node pools. Ensure your cluster uses Ubuntu 22.04 or Azure Linux node pools.

### Set environment variables

```
export CLUSTER=<cluster-name>
export RESOURCE_GROUP=<resource-group-name>
```


## Enable Istio CNI

Use the following command to enable Istio CNI on your AKS cluster:

```
az aks mesh enable-istio-cni --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


## Verify Istio CNI is enabled

Use `az aks get-credentials`

to get the credentials for your AKS cluster:

```
az aks get-credentials --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


After enabling Istio CNI, verify the installation by checking that the CNI DaemonSet is running:

```
kubectl get daemonset -n aks-istio-system
```


You should see the Istio CNI DaemonSet running:

```
NAME DESIRED CURRENT READY UP-TO-DATE AVAILABLE NODE SELECTOR AGE
azure-service-mesh-istio-cni-addon-node 3 3 3 3 3 kubernetes.io/os=linux 94s
```


## Deploy workloads and verify behavior

To verify the security improvement, you can deploy the bookinfo sample application and check that workloads use the secure `istio-validation`

init container instead of the privileged `istio-init`

container.

### Deploy sample application

First, enable sidecar injection for the default namespace:

```
# Get the current Istio revision
REVISION=$(az aks show --resource-group ${RESOURCE_GROUP} --name ${CLUSTER} --query 'serviceMeshProfile.istio.revisions[0]' -o tsv)
# Label the namespace for sidecar injection
kubectl label namespace default istio.io/rev=${REVISION}
```


Deploy the bookinfo sample application:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.25/samples/bookinfo/platform/kube/bookinfo.yaml
```


### Verify secure init container usage

Check that the deployed pods use the secure `istio-validation`

init container instead of `istio-init`

:

```
kubectl get pods -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.spec.initContainers[0].name}{"\t"}{.spec.initContainers[0].securityContext.capabilities}{"\n"}{end}'
```


Expected output should show `istio-validation`

as the init container with dropped capabilities:

```
details-v1-799dc5d847-7x9gl istio-validation {"drop":["ALL"]}
productpage-v1-99d6d698f-89gpj istio-validation {"drop":["ALL"]}
ratings-v1-7545c4bb6c-m7t42 istio-validation {"drop":["ALL"]}
reviews-v1-8679d76d6c-jz4vg istio-validation {"drop":["ALL"]}
reviews-v2-5b9c77895c-b2b7m istio-validation {"drop":["ALL"]}
reviews-v3-5b57874f5f-kk9rt istio-validation {"drop":["ALL"]}
```


You can also describe a specific pod to verify the security context:

```
kubectl describe pod <pod-name> | grep -A 10 -B 5 "istio-validation"
```


The output should show that the `istio-validation`

init container has no privileged capabilities:

```
Init Containers:
istio-validation:
Container ID: containerd://...
Image: mcr.microsoft.com/oss/istio/proxyv2:...
...
Security Context:
capabilities:
drop:
- ALL
runAsGroup: 1337
runAsNonRoot: true
runAsUser: 1337
```


## Disable Istio CNI

To disable Istio CNI and return to using traditional init containers, use the following command:

```
az aks mesh disable-istio-cni --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


After disabling Istio CNI:

The CNI DaemonSet will be removed:

`kubectl get daemonset azure-service-mesh-istio-cni-addon-node -n aks-istio-system`

Expected output (no CNI DaemonSet):

`Error from server (NotFound): daemonsets.apps "azure-service-mesh-istio-cni-addon-node" not found`

New workloads will use the traditional

`istio-init`

init container with network capabilities. Restart all existing deployments to pick up the change:`kubectl rollout restart deployment/details-v1 kubectl rollout restart deployment/productpage-v1 kubectl rollout restart deployment/ratings-v1 kubectl rollout restart deployment/reviews-v1 kubectl rollout restart deployment/reviews-v2 kubectl rollout restart deployment/reviews-v3`

Verify init container name and capabilities:

`kubectl get pods -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.spec.initContainers[0].name}{"\t"}{.spec.initContainers[0].securityContext.capabilities}{"\n"}{end}'`

Expected output should show

`istio-init`

with network capabilities:`details-v1-57bc58c559-722v8 istio-init {"drop":["ALL"]} productpage-v1-7bb64f657c-jw6gs istio-init {"drop":["ALL"]} ratings-v1-57d5594c75-4zd49 istio-init {"drop":["ALL"]} reviews-v1-7fd8f9cd59-mdcf9 istio-init {"drop":["ALL"]} reviews-v2-7b8bdc9cdf-k9qgb istio-init {"drop":["ALL"]} reviews-v3-588854d9d7-s2f7j istio-init {"drop":["ALL"]}`


---

<!-- DOCUMENTO FUSIONADO: _use-network-policies_create-node-pools.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-network-policies.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-network-policies -->

# Secure traffic between pods with network policies in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Support for Azure Network Policy Manager (NPM) on **Windows** nodes in AKS ends on **September 30, 2026**.

This change applies only to customers already onboarded to NPM. **Subscriptions that aren't registered with this feature will no longer be able to onboard**. Existing onboarded customers can continue using NPM until the end-of-support date.

To ensure your setup continues to receive support, security updates, and deployment compatibility, explore alternative options like [Network Security Groups (NSGs)](concepts-network) on the node level or open-source tools like [Project Calico](https://www.tigera.io/tigera-products/calico/).

Important

Support for Azure Network Policy Manager (NPM) on **Linux** nodes in AKS ends on **September 30, 2026**.

To avoid service disruptions, you need to [migrate AKS clusters running Linux nodes from NPM to Cilium Network Policy](migrate-from-npm-to-cilium-network-policy) by the end-of-support date.

Important

Support for kubenet networking on AKS clusters ends on **March 31, 2028**.

To avoid service disruptions, you need to upgrade to [Azure Container Networking Interface (CNI) Overlay](concepts-network-azure-cni-overlay) by the end-of-support date.

Install a network policy engine and create Kubernetes network policies to control the flow of traffic between pods in AKS clusters.

## Overview of network policy

By default, all pods in an AKS cluster can send and receive traffic without limitations. To improve security, you can define rules that control the flow of traffic.

Network policy is a Kubernetes specification that defines access policies for communication between pods. When you use network policies, you define an ordered set of rules to send and receive traffic. You apply the rules to a collection of pods that match one or more label selectors.

You define the network policy rules as YAML manifests, and you can include them in wider manifests that also create a deployment or service.

## Network policy options in AKS

Azure provides three network policy engines for enforcing network policies:

**Cilium**(for AKS clusters using[Azure CNI Powered by Cilium](azure-cni-powered-by-cilium))**Azure Network Policy Manager (NPM)****Calico**(an open-source network and network security solution founded by[Tigera](https://www.tigera.io/))

We recommend using Cilium. Cilium enforces network policy on the traffic using Linux Berkeley Packet Filter (BPF), which is more efficient than *IPTables*.

To enforce the specified policies, Azure NPM uses *IPTables* for Linux and *Host Network Service (HNS) ACLPolicies* for Windows. Policies are translated into sets of allowed and disallowed IP pairs. These pairs are then programmed as `IPTable`

or `HNS ACLPolicy`

filter rules.

## Differences between network policy engines: Cilium, Azure NPM, and Calico

| Network policy engine | Supported platforms | Supported networking options | Kubernetes specification compliance | Other features | Support |
|---|---|---|---|---|---|
| Cilium | Linux | Azure CNI | Supports all policy types |
|

[Calico Network Policy issue](https://github.com/Azure/AKS/issues/4038).## Azure Network Policy Manager limitations (Linux)

Azure NPM for Linux has the following limitations:

- Scaling beyond
*250 nodes*and*20,000 pods*isn't supported. If you attempt to scale beyond these limits, you might experience*Out of Memory (OOM)*errors. For better scalability and IPv6 support, we recommend using or upgrading to[Azure CNI Powered by Cilium](update-azure-cni)for your network policy engine. - IPv6 isn't supported. Otherwise, it fully supports the network policy specifications in Linux.

## Azure Network Policy Manager limitations (Windows)

Azure NPM for Windows doesn't support the following features of the network policy specifications:

- Named ports.
- Stream Control Transmission Protocol (SCTP).
- Negative match label or namespace selectors. For example, all labels except
`debug=true`

. `except`

classless interdomain routing (CIDR) blocks (CIDR with exceptions).

## Known issues with Azure Network Policy Manager

You might experience temporary connectivity issues for new connections to/from pods on impacted nodes when either editing or deleting a "large enough" network policy. Hitting this race condition never impacts active connections.

If this race condition occurs for a node, the Azure NPM pod on that node enters a state where it can't update security rules, which might lead to unexpected connectivity for new connections to/from pods on the impacted node. To mitigate the issue, the Azure NPM pod automatically restarts ~15 seconds after entering this state. While Azure NPM is rebooting on the impacted node, it deletes all security rules, then reapplies security rules for all network policies. While all the security rules are being reapplied, there's a chance of temporary, unexpected connectivity for new connections to/from pods on the impacted node.

To limit the chance of hitting this race condition, you can reduce the size of the network policy. This issue is most likely to happen for a network policy with several `ipBlock`

sections. A network policy with *four or fewer* `ipBlock`

sections is less likely to hit the issue.

## Load balancer services and network policies

Kubernetes service routing for both inbound and outbound services often involves rewriting the source and destination IPs on traffic that's being processed, including traffic that comes into the cluster from a `LoadBalancer`

service. This rewrite behavior means that the network policies might not properly process traffic being received from or sent to an external service. For more information, see the [Kubernetes Network Policies documentation](https://kubernetes.io/docs/concepts/services-networking/network-policies/).

To restrict what sources can send traffic to a load balancer service, use `spec.loadBalancerSourceRanges`

to configure traffic blocking that applies before any rewrites occur. For more information, see the [AKS Standard load balancer documentation](/en-us/azure/aks/load-balancer-standard#restrict-inbound-traffic-to-specific-ip-ranges).

## Before you begin

You need the Azure CLI version 2.0.61 or later installed and configured. Find the version using the `az --version`

command. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Instead of using a system-assigned identity, you can also use a user-assigned identity. For more information, see [Use managed identities](use-managed-identity).

## Create an AKS cluster with Azure Network Policy Manager (Linux)

Set environment variables for the resource group name, cluster name, and location. Replace the values as needed.

`export RESOURCE_GROUP=myResourceGroup export CLUSTER_NAME=myAKSCluster export LOCATION=eastus`

Create an AKS cluster using the

and specify`az aks create`

`azure`

for the`network-plugin`

and`network-policy`

.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --node-count 1 \ --network-plugin azure \ --network-policy azure \ --generate-ssh-keys`


## Create an AKS cluster with Azure Network Policy Manager (Windows Server 2022 (preview))

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Install the `aks-preview`

Azure CLI extension

Install the

`aks-preview`

extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

`az extension update --name aks-preview`


### Register the `WindowsNetworkPolicyPreview`

feature flag

Register the

`WindowsNetworkPolicyPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "WindowsNetworkPolicyPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "WindowsNetworkPolicyPreview"`

When the status reflects

*Registered*, refresh the registration of the`Microsoft.ContainerService`

resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create administrator credentials for Windows Server containers

Create a username to use as administrator credentials for your Windows Server containers on your cluster. The following command prompts you for a username. Set it to

`WINDOWS_USERNAME`

.`echo "Please enter the username to use as administrator credentials for Windows Server containers on your cluster: " && read WINDOWS_USERNAME`


### Create the AKS cluster

Set environment variables for the resource group name, cluster name, and location. Replace the values as needed.

`export RESOURCE_GROUP=myResourceGroup export CLUSTER_NAME=myAKSCluster export LOCATION=eastus`

Create an AKS cluster using the

and specify`az aks create`

`azure`

for the`network-plugin`

and`network-policy`

.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --node-count 1 \ --windows-admin-username $WINDOWS_USERNAME \ --network-plugin azure \ --network-policy azure \ --generate-ssh-keys`


## Create an AKS cluster with Calico

Create an AKS cluster using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command and specify

`--network-plugin azure`

and `--network-policy calico`

. Specifying `--network-policy calico`

enables Calico on both Linux and Windows node pools.If you plan on adding Windows node pools to your cluster, include the `windows-admin-username`

and `windows-admin-password`

parameters that meet the [Windows Server password requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference). To create administrator credentials for Windows Server containers on your cluster, see [Create administrator credentials for Windows Server containers](#create-administrator-credentials-for-windows-server-containers).

Important

At this time, using Calico network policies with Windows nodes is available on new clusters using Kubernetes version 1.20 or later with Calico 3.17.2 and requires that you use Azure CNI networking. Windows nodes on AKS clusters with Calico enabled also have Floating IP enabled by default.

For clusters with only Linux node pools running Kubernetes 1.20 with earlier versions of Calico, the Calico version automatically upgrades to 3.17.2.

## Install Azure Network Policy Manager or Calico on an existing cluster

Warning

Keep the following information in mind when installing Azure NPM or Calico on an existing cluster:

- The upgrade process triggers each node pool to be reimaged simultaneously. Upgrading each node pool separately isn't supported.
- Within each node pool, nodes follow the same reimaging process as standard Kubernetes version upgrade operations. This behavior means that buffer nodes are temporarily added to minimize disruption to running applications during the node reimaging process. Any disruptions that might occur are similar to what you might encounter during a node image upgrade or
[Kubernetes version upgrade](upgrade-cluster).

The following information applies to upgrades from kubenet with Calico to Azure CNI Overlay with Calico:

- In kubenet clusters with Calico enabled, Calico is used as both a CNI and network policy engine.
- In Azure CNI clusters, Calico is used only for network policy enforcement, not as a CNI. This can cause a short delay between when the pod starts and when Calico allows outbound traffic from the pod.

Update an existing cluster to install Azure NPM or Calico using the

command and specifying`az aks update`

`azure`

or`calico`

for the`--network-policy`

parameter. The following example command shows how to install either Azure NPM:`az aks update --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --network-policy azure`


## Upgrade an existing cluster with Azure NPM or Calico to Cilium

To upgrade an existing cluster to Azure CNI Powered by Cilium, see [Upgrade an existing cluster to Azure CNI Powered by Cilium](upgrade-aks-ipam-and-dataplane)

## Connect to the AKS cluster

Configure

`kubectl`

to connect to your cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Verify network policy setup

To begin verification of network policy, you create a sample application and set traffic rules.

Create a namespace named

`demo`

to run the sample pods using the`kubectl create namespace`

command.`kubectl create namespace demo`

Create a pod named

`server`

to server on TCP port 80 using the`kubectl run`

command.`kubectl run server -n demo --image=k8s.gcr.io/e2e-test-images/agnhost:2.33 --labels="app=server" --port=80 --command -- /agnhost serve-hostname --tcp --http=false --port "80"`

Create a pod named

`client`

to run Bash using the`kubectl run`

command.`kubectl run -it client -n demo --image=k8s.gcr.io/e2e-test-images/agnhost:2.33 --command -- bash`

Note

If you want to schedule the client or server on a particular node, add the following bit before the

`--command`

argument in the pod creationcommand:`kubectl run`

`--overrides='{"spec": { "nodeSelector": {"kubernetes.io/os": "linux|windows"}}}'`

.In a separate window, get the IP address of the

`server`

pod using the`kubectl get pod`

command.`kubectl get pod --output=wide -n demo`

Your output should resemble the following example output:

`NAME READY STATUS RESTARTS AGE IP NODE NOMINATED NODE READINESS GATES server 1/1 Running 0 30s 10.224.0.72 akswin22000001 <none> <none>`


## Test connectivity with network policies

Tip

To test connectivity without network policies, run the following command in the client shell: `/agnhost connect <server-ip>:80 --timeout=3s --protocol=tcp`

. Replace `<server-ip>`

with the IP address of the server pod. If the connection is successful, there's no output.

Create a file named

`demo-policy.yaml`

and paste the following YAML manifest:`apiVersion: networking.k8s.io/v1 kind: NetworkPolicy metadata: name: demo-policy namespace: demo spec: podSelector: matchLabels: app: server ingress: - from: - podSelector: matchLabels: app: client ports: - port: 80 protocol: TCP`

Apply the network policy manifest using the

command.`kubectl apply`

`kubectl apply –f demo-policy.yaml`

In the client shell, verify connectivity with the server using the following

`/agnhost`

command:`/agnhost connect <server-ip>:80 --timeout=3s --protocol=tcp`

Connectivity with traffic is blocked because the server is labeled with

`app=server`

, but the client isn't labeled. Your output should resemble the following example output:`TIMEOUT`

Label the

`client`

and verify connectivity with the server using the`kubectl label`

command.`kubectl label pod client -n demo app=client`

If the connection is successful, there's no output.


## Migrate to self-managed Calico

AKS only supports Calico for standard Kubernetes network policies and doesn't test other features. If you want to move to self-managed Calico, follow the Tigera instructions at [Migrate from Azure-managed Calico to self-managed Calico](https://docs.tigera.io/calico/latest/getting-started/kubernetes/managed-public-cloud/aks-migrate). The Tigera documentation mentions that for self-managed Calico you set `--network-policy none`

like in the [uninstall section](#uninstall-azure-network-policy-manager-or-calico).

## Uninstall Azure Network Policy Manager or Calico

Note

Keep the following information in mind when uninstalling Azure NPM or Calico from a cluster:

- The uninstall process
**doesn't remove**Custom Resource Definitions (CRDs) and Custom Resources (CRs) used by Calico. These CRDs and CRs all have names ending with either*projectcalico.org*or*tigera.io*. You can manually remove these CRDs and associated CRs*after*successfully uninstalling Calico. - The upgrade doesn't remove any network policy resources in the cluster, but the policies are no longer enforced after the uninstall process.

Remove Azure Network Policy Manager or Calico from an existing cluster using the

command and specifying`az aks update`

`none`

for the`--network-policy`

parameter.`az aks update --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --network-policy none`


## Clean up resources

In this article, you created a namespace and two pods and applied a network policy. If you no longer need these resources, you can delete them.

Delete the resources using the

command.`kubectl delete`

`kubectl delete namespace demo`


---

<!-- DOCUMENTO FUSIONADO: create-node-pools.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/create-node-pools -->

# Create node pools for a cluster in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to create one or more node pools in an AKS cluster.

Note

This feature enables more control over creating and managing multiple node pools and requires separate commands for *create/update/delete* (CRUD) operations. Previously, cluster operations through [ az aks create](/en-us/cli/azure/aks#az-aks-create) or

[used the managedCluster API and were the only options to change your control plane and a single node pool. This feature exposes a separate operation set for agent pools through the agentPool API and requires use of the](/en-us/cli/azure/aks#az-aks-update)

`az aks update`

[command set to execute operations on an individual node pool.](/en-us/cli/azure/aks/nodepool)

`az aks nodepool`

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

- You need Azure CLI version 2.2.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

To deploy an ARM template, you need write access on the resources you're deploying and access to all operations on the

`Microsoft.Resources/deployments`

resource type. For example, to deploy a virtual machine (VM), you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).Review the following requirements for each parameter:

`osTYPE`

: The operating system type. The default is Linux.`osSKU`

: Specifies the OS SKU used by the agent pool.`count`

: Number of agents (VMs) to host docker containers. Allowed values must be in the range of 0 to 1000 (inclusive) for user pools and in the range of 1 to 1000 (inclusive) for system pools. The default value is 1.

After you deploy the cluster using an ARM template, you can use Azure CLI or Azure PowerShell to connect to the cluster and deploy the sample application.


## Limitations

The following limitations apply when you create AKS clusters that support multiple node pools:

You can delete the system node pool if you have another system node pool to take its place in the AKS cluster. Otherwise, you can't delete the system node pool.

System pools must contain at least one node. User node pools can contain zero or more nodes.

**If you create a cluster with a single node pool, the OS type must be**. The OS SKU can be any Linux variation such as`Linux`

`Ubuntu`

or`AzureLinux`

. You can't create a cluster with a single Windows node pool. If you want to run Windows containers, you must[add a Windows node pool](#add-a-windows-server-node-pool)to the cluster after creating it with a Linux system node pool.The AKS cluster must use the Standard SKU load balancer to use multiple node pools. This feature isn't supported with Basic SKU load balancers.

The AKS cluster must use Virtual Machine Scale Sets for the nodes.

The name of a node pool can only contain lowercase alphanumeric characters and must begin with a lowercase letter.

- For Linux node pools, the length must be between 1-12 characters.
- For Windows node pools, the length must be between 1-6 characters.

All node pools must reside in the same virtual network.

You can't change the virtual machine (VM) size of a node pool after you create it.

When you create multiple node pools at cluster creation time, the Kubernetes versions for the node pools must match the version set for the control plane. You can make updates after provisioning the cluster using per node pool operations.


## Create specialized node pools

To learn how to create specialized node pools, see the following articles:

[Add an Azure Spot node pool to an AKS cluster](spot-node-pool)[Add a Virtual Machines node pool to an AKS cluster](virtual-machines-node-pools)[Add a dedicated system node pool to an AKS cluster](use-system-pools#add-a-dedicated-system-node-pool-to-an-existing-aks-cluster)[Enabled Federal Information Processing Standards (FIPS) on an AKS node pool](enable-fips-nodes)[Add a node pool with a Confidential Virtual Machine (CVM) on an AKS cluster](use-cvm)[Create node pools with unique subnets in AKS](node-pool-unique-subnet)[Add a generation 2 VM node pool to an AKS cluster](generation-2-vms)[Add a node pool with Artifact Streaming to an AKS cluster](artifact-streaming)[Add Windows Server node pools with](windows-containerd)`containerd`

to an AKS cluster

## Set environment variables

Set the following environment variables in your shell to simplify the commands in this article. You can change the values to your preferred names.

`export RESOURCE_GROUP_NAME="my-aks-rg" export LOCATION="eastus" export CLUSTER_NAME="my-aks-cluster" export NODE_POOL_NAME="mynodepool"`


## Create a resource group

Create an Azure resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP_NAME --location $LOCATION`


## Create an AKS cluster with a single node pool using the Azure CLI

If you want only one node pool in your AKS cluster, you can schedule application pods on system node pools. If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool. If one node goes down, the redundancy is compromised. You can mitigate this risk by having more system node pool nodes.

-
[Create an AKS cluster with a single Ubuntu node pool](#tabpanel_1_ubuntu) -
[Create an AKS cluster with a single Azure Linux node pool](#tabpanel_1_azure-linux) -
[Create an AKS cluster with a single Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_1_os-guard) -
[Create an AKS cluster with a single Flatcar Container Linux for AKS (preview) node pool](#tabpanel_1_flatcar)

Create a cluster with a single Ubuntu node pool using the

command. This step specifies two nodes in the single node pool.`az aks create`

`az aks create \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --vm-set-type VirtualMachineScaleSets \ --node-count 2 \ --os-sku Ubuntu \ --location $LOCATION \ --load-balancer-sku standard \ --generate-ssh-keys`

It takes a few minutes to create the cluster.

When the cluster is ready, get the cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME`


## Add a second node pool using the Azure CLI

The cluster created in the [previous section](#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli) has a single node pool. In this section, we add a second node pool to the cluster. This second node pool can have an OS type of `Linux`

with an OS SKU of `Ubuntu`

or `AzureLinux`

, or an OS type of `Windows`

.

Note

If you want to add a node pool that uses **Ephemeral OS disks** to your AKS cluster, you can set the `--node-osdisk-type`

flag to `Ephemeral`

when running the `az aks nodepool add`

command.

With Ephemeral OS, you can deploy VMs and instance images up to the size of the VM cache. The default node OS disk configuration in AKS uses 128 GB, which means that you need a VM size that has a cache larger than 128 GB. The default `Standard_DS2_v2`

has a cache size of 86 GB, which isn't large enough. The `Standard_DS3_v2`

VM SKU has a cache size of 172 GB, which is large enough. You can also reduce the default size of the OS disk using `--node-osdisk-size`

, but keep in mind the minimum size for AKS images is 30 GB.

If you want to create node pools with **network-attached OS disks**, you can set the `--node-osdisk-type`

flag to `Managed`

when running the `az aks nodepool add`

command.

### Add a Linux node pool

-
[Add an Ubuntu node pool](#tabpanel_2_ubuntu) -
[Add an Azure Linux node pool](#tabpanel_2_azure-linux) -
[Add an Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_2_os-guard) -
[Add a Flatcar Container Linux for AKS (preview) node pool](#tabpanel_2_flatcar)

Create a new node pool using the

command. The following example creates a`az aks nodepool add`

`Linux`

node pool with the`Ubuntu`

OS SKU that runs*three*nodes. If you don't specify an OS SKU, AKS defaults to`Ubuntu`

.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-vm-size Standard_DS2_v2 \ --os-type Linux \ --os-sku Ubuntu \ --node-count 3`

It takes a few minutes to create the node pool.


### Add a Windows Server node pool

##### Install the `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


##### Register the `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


##### Create the Windows Server 2025 node pool

Create a new node pool using the

command. The following example creates a`az aks nodepool add`

`Windows`

node pool with the`Windows2025`

OS SKU that runs*three*nodes.For more information about Windows OS, see

[Windows best practices](windows-best-practices).`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-vm-size Standard_DS2_v2 \ --os-type Windows \ --os-sku Windows2025 \ --node-count 3`


## Check the status of your node pools

Check the status of your node pools using the

command and specify your resource group and cluster name.`az aks nodepool list`

`az aks nodepool list --resource-group $RESOURCE_GROUP_NAME --cluster-name $CLUSTER_NAME`


## Create an AKS cluster with a single node pool using an ARM template

If you want only one node pool in your AKS cluster, you can schedule application pods on system node pools. If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool. If one node goes down, the redundancy is compromised. You can mitigate this risk by having more system node pool nodes.

### Create a `Microsoft.ContainerService/managedClusters`

resource

- Create a
`Microsoft.ContainerService/managedClusters`

resource by adding[this JSON](/en-us/azure/templates/microsoft.containerservice/managedclusters?pivots=deployment-language-arm-template)to your template.

-
[Modify JSON to create a single Ubuntu node pool](#tabpanel_4_ubuntu-arm) -
[Modify JSON to create a single Azure Linux node pool](#tabpanel_4_azure-linux-arm) -
[Modify JSON to create a single Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_4_os-guard-arm) -
[Modify JSON to create a single Flatcar Container Linux for AKS (preview) node pool](#tabpanel_4_flatcar-arm)

Create a single Ubuntu node pool in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "1", "osSKU": "ubuntu", "osType": "linux" } ], }`


## Add a second node pool using an ARM template

The cluster created in the [previous section](#create-an-aks-cluster-with-a-single-node-pool-using-an-arm-template) has a single node pool. In this section, we add a second node pool to the cluster. This second node pool can have an OS type of `Linux`

with an OS SKU of `Ubuntu`

or `AzureLinux`

, or an OS type of `Windows`

.

### Add Linux node pools

-
[Modify JSON to create multiple Ubuntu node pools](#tabpanel_5_ubuntu-arm) -
[Modify JSON to create multiple Azure Linux node pools](#tabpanel_5_azure-linux-arm) -
[Modify JSON to create multiple Azure Linux with OS Guard for AKS (preview) node pools](#tabpanel_5_os-guard-arm) -
[Modify JSON to create multiple Flatcar Container Linux for AKS (preview) node pools](#tabpanel_5_flatcar-arm)

Create multiple Ubuntu node pools in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "3", "osSKU": "ubuntu", "osType": "linux" } ], }`


### Add Windows Server node pools

-
[Modify JSON to create multiple Windows Server 2025 (preview) node pools](#tabpanel_6_ws2025-arm) -
[Modify JSON to create multiple Windows Server 2022 node pools](#tabpanel_6_ws2022-arm)

##### Install the `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


##### Register the `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


##### Create the Windows Server 2025 node pools

Create multiple Windows node pools in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "3", "osSKU": "windows2025", "osType": "windows" } ], }`


## Deploy your ARM template

- Deploy your ARM template by following the guidance in
[Deploy an Azure Kubernetes Service (AKS) cluster using an ARM template](learn/quick-kubernetes-deploy-rm-template).

## Set taints, labels, or tags for a node pool

When creating a node pool, you can add taints, labels, or tags to it. When you add a taint, label, or tag, all nodes within that node pool also get that taint, label, or tag. We recommend applying these properties to an entire node pool instead of individual nodes. This way, you can easily manage the properties of all nodes in the node pool by updating the node pool properties instead of updating each node individually.

For specific instructions on how to set taints, labels, or tags for a node pool, use the following resources:

[Use node taints in an Azure Kubernetes Service (AKS) cluster](use-node-taints)[Use labels in an Azure Kubernetes Service (AKS) cluster](use-labels)[Use Azure tags in Azure Kubernetes Service (AKS)](use-tags)[Provide dedicated nodes using taints and tolerations in Azure Kubernetes Service (AKS)](operator-best-practices-advanced-scheduler#provide-dedicated-nodes-using-taints-and-tolerations)

## Next steps

In this article, you learned how to create an AKS cluster with a single node pool and add additional node pools to your cluster. To learn more about how to manage your node pools, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: __manage-node-pools_use-multiple-node-pools__upgrade-cluster__kubernetes-action__e0f440.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _manage-node-pools_use-multiple-node-pools.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: manage-node-pools.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/manage-node-pools -->

# Create node pools for a cluster in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to create one or more node pools in an AKS cluster.

Note

This feature enables more control over creating and managing multiple node pools and requires separate commands for *create/update/delete* (CRUD) operations. Previously, cluster operations through [ az aks create](/en-us/cli/azure/aks#az-aks-create) or

[used the managedCluster API and were the only options to change your control plane and a single node pool. This feature exposes a separate operation set for agent pools through the agentPool API and requires use of the](/en-us/cli/azure/aks#az-aks-update)

`az aks update`

[command set to execute operations on an individual node pool.](/en-us/cli/azure/aks/nodepool)

`az aks nodepool`

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

- You need Azure CLI version 2.2.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

To deploy an ARM template, you need write access on the resources you're deploying and access to all operations on the

`Microsoft.Resources/deployments`

resource type. For example, to deploy a virtual machine (VM), you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).Review the following requirements for each parameter:

`osTYPE`

: The operating system type. The default is Linux.`osSKU`

: Specifies the OS SKU used by the agent pool.`count`

: Number of agents (VMs) to host docker containers. Allowed values must be in the range of 0 to 1000 (inclusive) for user pools and in the range of 1 to 1000 (inclusive) for system pools. The default value is 1.

After you deploy the cluster using an ARM template, you can use Azure CLI or Azure PowerShell to connect to the cluster and deploy the sample application.


## Limitations

The following limitations apply when you create AKS clusters that support multiple node pools:

You can delete the system node pool if you have another system node pool to take its place in the AKS cluster. Otherwise, you can't delete the system node pool.

System pools must contain at least one node. User node pools can contain zero or more nodes.

**If you create a cluster with a single node pool, the OS type must be**. The OS SKU can be any Linux variation such as`Linux`

`Ubuntu`

or`AzureLinux`

. You can't create a cluster with a single Windows node pool. If you want to run Windows containers, you must[add a Windows node pool](#add-a-windows-server-node-pool)to the cluster after creating it with a Linux system node pool.The AKS cluster must use the Standard SKU load balancer to use multiple node pools. This feature isn't supported with Basic SKU load balancers.

The AKS cluster must use Virtual Machine Scale Sets for the nodes.

The name of a node pool can only contain lowercase alphanumeric characters and must begin with a lowercase letter.

- For Linux node pools, the length must be between 1-12 characters.
- For Windows node pools, the length must be between 1-6 characters.

All node pools must reside in the same virtual network.

You can't change the virtual machine (VM) size of a node pool after you create it.

When you create multiple node pools at cluster creation time, the Kubernetes versions for the node pools must match the version set for the control plane. You can make updates after provisioning the cluster using per node pool operations.


## Create specialized node pools

To learn how to create specialized node pools, see the following articles:

[Add an Azure Spot node pool to an AKS cluster](spot-node-pool)[Add a Virtual Machines node pool to an AKS cluster](virtual-machines-node-pools)[Add a dedicated system node pool to an AKS cluster](use-system-pools#add-a-dedicated-system-node-pool-to-an-existing-aks-cluster)[Enabled Federal Information Processing Standards (FIPS) on an AKS node pool](enable-fips-nodes)[Add a node pool with a Confidential Virtual Machine (CVM) on an AKS cluster](use-cvm)[Create node pools with unique subnets in AKS](node-pool-unique-subnet)[Add a generation 2 VM node pool to an AKS cluster](generation-2-vms)[Add a node pool with Artifact Streaming to an AKS cluster](artifact-streaming)[Add Windows Server node pools with](windows-containerd)`containerd`

to an AKS cluster

## Set environment variables

Set the following environment variables in your shell to simplify the commands in this article. You can change the values to your preferred names.

`export RESOURCE_GROUP_NAME="my-aks-rg" export LOCATION="eastus" export CLUSTER_NAME="my-aks-cluster" export NODE_POOL_NAME="mynodepool"`


## Create a resource group

Create an Azure resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP_NAME --location $LOCATION`


## Create an AKS cluster with a single node pool using the Azure CLI

If you want only one node pool in your AKS cluster, you can schedule application pods on system node pools. If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool. If one node goes down, the redundancy is compromised. You can mitigate this risk by having more system node pool nodes.

-
[Create an AKS cluster with a single Ubuntu node pool](#tabpanel_1_ubuntu) -
[Create an AKS cluster with a single Azure Linux node pool](#tabpanel_1_azure-linux) -
[Create an AKS cluster with a single Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_1_os-guard) -
[Create an AKS cluster with a single Flatcar Container Linux for AKS (preview) node pool](#tabpanel_1_flatcar)

Create a cluster with a single Ubuntu node pool using the

command. This step specifies two nodes in the single node pool.`az aks create`

`az aks create \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --vm-set-type VirtualMachineScaleSets \ --node-count 2 \ --os-sku Ubuntu \ --location $LOCATION \ --load-balancer-sku standard \ --generate-ssh-keys`

It takes a few minutes to create the cluster.

When the cluster is ready, get the cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME`


## Add a second node pool using the Azure CLI

The cluster created in the [previous section](#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli) has a single node pool. In this section, we add a second node pool to the cluster. This second node pool can have an OS type of `Linux`

with an OS SKU of `Ubuntu`

or `AzureLinux`

, or an OS type of `Windows`

.

Note

If you want to add a node pool that uses **Ephemeral OS disks** to your AKS cluster, you can set the `--node-osdisk-type`

flag to `Ephemeral`

when running the `az aks nodepool add`

command.

With Ephemeral OS, you can deploy VMs and instance images up to the size of the VM cache. The default node OS disk configuration in AKS uses 128 GB, which means that you need a VM size that has a cache larger than 128 GB. The default `Standard_DS2_v2`

has a cache size of 86 GB, which isn't large enough. The `Standard_DS3_v2`

VM SKU has a cache size of 172 GB, which is large enough. You can also reduce the default size of the OS disk using `--node-osdisk-size`

, but keep in mind the minimum size for AKS images is 30 GB.

If you want to create node pools with **network-attached OS disks**, you can set the `--node-osdisk-type`

flag to `Managed`

when running the `az aks nodepool add`

command.

### Add a Linux node pool

-
[Add an Ubuntu node pool](#tabpanel_2_ubuntu) -
[Add an Azure Linux node pool](#tabpanel_2_azure-linux) -
[Add an Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_2_os-guard) -
[Add a Flatcar Container Linux for AKS (preview) node pool](#tabpanel_2_flatcar)

Create a new node pool using the

command. The following example creates a`az aks nodepool add`

`Linux`

node pool with the`Ubuntu`

OS SKU that runs*three*nodes. If you don't specify an OS SKU, AKS defaults to`Ubuntu`

.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-vm-size Standard_DS2_v2 \ --os-type Linux \ --os-sku Ubuntu \ --node-count 3`

It takes a few minutes to create the node pool.


### Add a Windows Server node pool

##### Install the `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


##### Register the `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


##### Create the Windows Server 2025 node pool

Create a new node pool using the

command. The following example creates a`az aks nodepool add`

`Windows`

node pool with the`Windows2025`

OS SKU that runs*three*nodes.For more information about Windows OS, see

[Windows best practices](windows-best-practices).`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-vm-size Standard_DS2_v2 \ --os-type Windows \ --os-sku Windows2025 \ --node-count 3`


## Check the status of your node pools

Check the status of your node pools using the

command and specify your resource group and cluster name.`az aks nodepool list`

`az aks nodepool list --resource-group $RESOURCE_GROUP_NAME --cluster-name $CLUSTER_NAME`


## Create an AKS cluster with a single node pool using an ARM template

If you want only one node pool in your AKS cluster, you can schedule application pods on system node pools. If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool. If one node goes down, the redundancy is compromised. You can mitigate this risk by having more system node pool nodes.

### Create a `Microsoft.ContainerService/managedClusters`

resource

- Create a
`Microsoft.ContainerService/managedClusters`

resource by adding[this JSON](/en-us/azure/templates/microsoft.containerservice/managedclusters?pivots=deployment-language-arm-template)to your template.

-
[Modify JSON to create a single Ubuntu node pool](#tabpanel_4_ubuntu-arm) -
[Modify JSON to create a single Azure Linux node pool](#tabpanel_4_azure-linux-arm) -
[Modify JSON to create a single Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_4_os-guard-arm) -
[Modify JSON to create a single Flatcar Container Linux for AKS (preview) node pool](#tabpanel_4_flatcar-arm)

Create a single Ubuntu node pool in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "1", "osSKU": "ubuntu", "osType": "linux" } ], }`


## Add a second node pool using an ARM template

The cluster created in the [previous section](#create-an-aks-cluster-with-a-single-node-pool-using-an-arm-template) has a single node pool. In this section, we add a second node pool to the cluster. This second node pool can have an OS type of `Linux`

with an OS SKU of `Ubuntu`

or `AzureLinux`

, or an OS type of `Windows`

.

### Add Linux node pools

-
[Modify JSON to create multiple Ubuntu node pools](#tabpanel_5_ubuntu-arm) -
[Modify JSON to create multiple Azure Linux node pools](#tabpanel_5_azure-linux-arm) -
[Modify JSON to create multiple Azure Linux with OS Guard for AKS (preview) node pools](#tabpanel_5_os-guard-arm) -
[Modify JSON to create multiple Flatcar Container Linux for AKS (preview) node pools](#tabpanel_5_flatcar-arm)

Create multiple Ubuntu node pools in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "3", "osSKU": "ubuntu", "osType": "linux" } ], }`


### Add Windows Server node pools

-
[Modify JSON to create multiple Windows Server 2025 (preview) node pools](#tabpanel_6_ws2025-arm) -
[Modify JSON to create multiple Windows Server 2022 node pools](#tabpanel_6_ws2022-arm)

##### Install the `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


##### Register the `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


##### Create the Windows Server 2025 node pools

Create multiple Windows node pools in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "3", "osSKU": "windows2025", "osType": "windows" } ], }`


## Deploy your ARM template

- Deploy your ARM template by following the guidance in
[Deploy an Azure Kubernetes Service (AKS) cluster using an ARM template](learn/quick-kubernetes-deploy-rm-template).

## Set taints, labels, or tags for a node pool

When creating a node pool, you can add taints, labels, or tags to it. When you add a taint, label, or tag, all nodes within that node pool also get that taint, label, or tag. We recommend applying these properties to an entire node pool instead of individual nodes. This way, you can easily manage the properties of all nodes in the node pool by updating the node pool properties instead of updating each node individually.

For specific instructions on how to set taints, labels, or tags for a node pool, use the following resources:

[Use node taints in an Azure Kubernetes Service (AKS) cluster](use-node-taints)[Use labels in an Azure Kubernetes Service (AKS) cluster](use-labels)[Use Azure tags in Azure Kubernetes Service (AKS)](use-tags)[Provide dedicated nodes using taints and tolerations in Azure Kubernetes Service (AKS)](operator-best-practices-advanced-scheduler#provide-dedicated-nodes-using-taints-and-tolerations)

## Next steps

In this article, you learned how to create an AKS cluster with a single node pool and add additional node pools to your cluster. To learn more about how to manage your node pools, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: use-multiple-node-pools.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-multiple-node-pools -->

# Create node pools for a cluster in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to create one or more node pools in an AKS cluster.

Note

This feature enables more control over creating and managing multiple node pools and requires separate commands for *create/update/delete* (CRUD) operations. Previously, cluster operations through [ az aks create](/en-us/cli/azure/aks#az-aks-create) or

[used the managedCluster API and were the only options to change your control plane and a single node pool. This feature exposes a separate operation set for agent pools through the agentPool API and requires use of the](/en-us/cli/azure/aks#az-aks-update)

`az aks update`

[command set to execute operations on an individual node pool.](/en-us/cli/azure/aks/nodepool)

`az aks nodepool`

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

- You need Azure CLI version 2.2.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

To deploy an ARM template, you need write access on the resources you're deploying and access to all operations on the

`Microsoft.Resources/deployments`

resource type. For example, to deploy a virtual machine (VM), you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).Review the following requirements for each parameter:

`osTYPE`

: The operating system type. The default is Linux.`osSKU`

: Specifies the OS SKU used by the agent pool.`count`

: Number of agents (VMs) to host docker containers. Allowed values must be in the range of 0 to 1000 (inclusive) for user pools and in the range of 1 to 1000 (inclusive) for system pools. The default value is 1.

After you deploy the cluster using an ARM template, you can use Azure CLI or Azure PowerShell to connect to the cluster and deploy the sample application.


## Limitations

The following limitations apply when you create AKS clusters that support multiple node pools:

You can delete the system node pool if you have another system node pool to take its place in the AKS cluster. Otherwise, you can't delete the system node pool.

System pools must contain at least one node. User node pools can contain zero or more nodes.

**If you create a cluster with a single node pool, the OS type must be**. The OS SKU can be any Linux variation such as`Linux`

`Ubuntu`

or`AzureLinux`

. You can't create a cluster with a single Windows node pool. If you want to run Windows containers, you must[add a Windows node pool](#add-a-windows-server-node-pool)to the cluster after creating it with a Linux system node pool.The AKS cluster must use the Standard SKU load balancer to use multiple node pools. This feature isn't supported with Basic SKU load balancers.

The AKS cluster must use Virtual Machine Scale Sets for the nodes.

The name of a node pool can only contain lowercase alphanumeric characters and must begin with a lowercase letter.

- For Linux node pools, the length must be between 1-12 characters.
- For Windows node pools, the length must be between 1-6 characters.

All node pools must reside in the same virtual network.

You can't change the virtual machine (VM) size of a node pool after you create it.

When you create multiple node pools at cluster creation time, the Kubernetes versions for the node pools must match the version set for the control plane. You can make updates after provisioning the cluster using per node pool operations.


## Create specialized node pools

To learn how to create specialized node pools, see the following articles:

[Add an Azure Spot node pool to an AKS cluster](spot-node-pool)[Add a Virtual Machines node pool to an AKS cluster](virtual-machines-node-pools)[Add a dedicated system node pool to an AKS cluster](use-system-pools#add-a-dedicated-system-node-pool-to-an-existing-aks-cluster)[Enabled Federal Information Processing Standards (FIPS) on an AKS node pool](enable-fips-nodes)[Add a node pool with a Confidential Virtual Machine (CVM) on an AKS cluster](use-cvm)[Create node pools with unique subnets in AKS](node-pool-unique-subnet)[Add a generation 2 VM node pool to an AKS cluster](generation-2-vms)[Add a node pool with Artifact Streaming to an AKS cluster](artifact-streaming)[Add Windows Server node pools with](windows-containerd)`containerd`

to an AKS cluster

## Set environment variables

Set the following environment variables in your shell to simplify the commands in this article. You can change the values to your preferred names.

`export RESOURCE_GROUP_NAME="my-aks-rg" export LOCATION="eastus" export CLUSTER_NAME="my-aks-cluster" export NODE_POOL_NAME="mynodepool"`


## Create a resource group

Create an Azure resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP_NAME --location $LOCATION`


## Create an AKS cluster with a single node pool using the Azure CLI

If you want only one node pool in your AKS cluster, you can schedule application pods on system node pools. If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool. If one node goes down, the redundancy is compromised. You can mitigate this risk by having more system node pool nodes.

-
[Create an AKS cluster with a single Ubuntu node pool](#tabpanel_1_ubuntu) -
[Create an AKS cluster with a single Azure Linux node pool](#tabpanel_1_azure-linux) -
[Create an AKS cluster with a single Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_1_os-guard) -
[Create an AKS cluster with a single Flatcar Container Linux for AKS (preview) node pool](#tabpanel_1_flatcar)

Create a cluster with a single Ubuntu node pool using the

command. This step specifies two nodes in the single node pool.`az aks create`

`az aks create \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --vm-set-type VirtualMachineScaleSets \ --node-count 2 \ --os-sku Ubuntu \ --location $LOCATION \ --load-balancer-sku standard \ --generate-ssh-keys`

It takes a few minutes to create the cluster.

When the cluster is ready, get the cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME`


## Add a second node pool using the Azure CLI

The cluster created in the [previous section](#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli) has a single node pool. In this section, we add a second node pool to the cluster. This second node pool can have an OS type of `Linux`

with an OS SKU of `Ubuntu`

or `AzureLinux`

, or an OS type of `Windows`

.

Note

If you want to add a node pool that uses **Ephemeral OS disks** to your AKS cluster, you can set the `--node-osdisk-type`

flag to `Ephemeral`

when running the `az aks nodepool add`

command.

With Ephemeral OS, you can deploy VMs and instance images up to the size of the VM cache. The default node OS disk configuration in AKS uses 128 GB, which means that you need a VM size that has a cache larger than 128 GB. The default `Standard_DS2_v2`

has a cache size of 86 GB, which isn't large enough. The `Standard_DS3_v2`

VM SKU has a cache size of 172 GB, which is large enough. You can also reduce the default size of the OS disk using `--node-osdisk-size`

, but keep in mind the minimum size for AKS images is 30 GB.

If you want to create node pools with **network-attached OS disks**, you can set the `--node-osdisk-type`

flag to `Managed`

when running the `az aks nodepool add`

command.

### Add a Linux node pool

-
[Add an Ubuntu node pool](#tabpanel_2_ubuntu) -
[Add an Azure Linux node pool](#tabpanel_2_azure-linux) -
[Add an Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_2_os-guard) -
[Add a Flatcar Container Linux for AKS (preview) node pool](#tabpanel_2_flatcar)

Create a new node pool using the

command. The following example creates a`az aks nodepool add`

`Linux`

node pool with the`Ubuntu`

OS SKU that runs*three*nodes. If you don't specify an OS SKU, AKS defaults to`Ubuntu`

.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-vm-size Standard_DS2_v2 \ --os-type Linux \ --os-sku Ubuntu \ --node-count 3`

It takes a few minutes to create the node pool.


### Add a Windows Server node pool

##### Install the `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


##### Register the `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


##### Create the Windows Server 2025 node pool

Create a new node pool using the

command. The following example creates a`az aks nodepool add`

`Windows`

node pool with the`Windows2025`

OS SKU that runs*three*nodes.For more information about Windows OS, see

[Windows best practices](windows-best-practices).`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-vm-size Standard_DS2_v2 \ --os-type Windows \ --os-sku Windows2025 \ --node-count 3`


## Check the status of your node pools

Check the status of your node pools using the

command and specify your resource group and cluster name.`az aks nodepool list`

`az aks nodepool list --resource-group $RESOURCE_GROUP_NAME --cluster-name $CLUSTER_NAME`


## Create an AKS cluster with a single node pool using an ARM template

If you want only one node pool in your AKS cluster, you can schedule application pods on system node pools. If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool. If one node goes down, the redundancy is compromised. You can mitigate this risk by having more system node pool nodes.

### Create a `Microsoft.ContainerService/managedClusters`

resource

- Create a
`Microsoft.ContainerService/managedClusters`

resource by adding[this JSON](/en-us/azure/templates/microsoft.containerservice/managedclusters?pivots=deployment-language-arm-template)to your template.

-
[Modify JSON to create a single Ubuntu node pool](#tabpanel_4_ubuntu-arm) -
[Modify JSON to create a single Azure Linux node pool](#tabpanel_4_azure-linux-arm) -
[Modify JSON to create a single Azure Linux with OS Guard for AKS (preview) node pool](#tabpanel_4_os-guard-arm) -
[Modify JSON to create a single Flatcar Container Linux for AKS (preview) node pool](#tabpanel_4_flatcar-arm)

Create a single Ubuntu node pool in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "1", "osSKU": "ubuntu", "osType": "linux" } ], }`


## Add a second node pool using an ARM template

The cluster created in the [previous section](#create-an-aks-cluster-with-a-single-node-pool-using-an-arm-template) has a single node pool. In this section, we add a second node pool to the cluster. This second node pool can have an OS type of `Linux`

with an OS SKU of `Ubuntu`

or `AzureLinux`

, or an OS type of `Windows`

.

### Add Linux node pools

-
[Modify JSON to create multiple Ubuntu node pools](#tabpanel_5_ubuntu-arm) -
[Modify JSON to create multiple Azure Linux node pools](#tabpanel_5_azure-linux-arm) -
[Modify JSON to create multiple Azure Linux with OS Guard for AKS (preview) node pools](#tabpanel_5_os-guard-arm) -
[Modify JSON to create multiple Flatcar Container Linux for AKS (preview) node pools](#tabpanel_5_flatcar-arm)

Create multiple Ubuntu node pools in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "3", "osSKU": "ubuntu", "osType": "linux" } ], }`


### Add Windows Server node pools

-
[Modify JSON to create multiple Windows Server 2025 (preview) node pools](#tabpanel_6_ws2025-arm) -
[Modify JSON to create multiple Windows Server 2022 node pools](#tabpanel_6_ws2022-arm)

##### Install the `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


##### Register the `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


##### Create the Windows Server 2025 node pools

Create multiple Windows node pools in your AKS cluster by making the following modifications to your ARM template:

`"properties": { "agentPoolProfiles": [ { "count": "3", "osSKU": "windows2025", "osType": "windows" } ], }`


## Deploy your ARM template

- Deploy your ARM template by following the guidance in
[Deploy an Azure Kubernetes Service (AKS) cluster using an ARM template](learn/quick-kubernetes-deploy-rm-template).

## Set taints, labels, or tags for a node pool

When creating a node pool, you can add taints, labels, or tags to it. When you add a taint, label, or tag, all nodes within that node pool also get that taint, label, or tag. We recommend applying these properties to an entire node pool instead of individual nodes. This way, you can easily manage the properties of all nodes in the node pool by updating the node pool properties instead of updating each node individually.

For specific instructions on how to set taints, labels, or tags for a node pool, use the following resources:

[Use node taints in an Azure Kubernetes Service (AKS) cluster](use-node-taints)[Use labels in an Azure Kubernetes Service (AKS) cluster](use-labels)[Use Azure tags in Azure Kubernetes Service (AKS)](use-tags)[Provide dedicated nodes using taints and tolerations in Azure Kubernetes Service (AKS)](operator-best-practices-advanced-scheduler#provide-dedicated-nodes-using-taints-and-tolerations)

## Next steps

In this article, you learned how to create an AKS cluster with a single node pool and add additional node pools to your cluster. To learn more about how to manage your node pools, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: _upgrade-cluster__kubernetes-action_how-to-enable-ebpf-host-routing.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: upgrade-cluster.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/upgrade-cluster -->

# Upgrade options and recommendations for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article gives you a technical foundation for Azure Kubernetes Service (AKS) cluster upgrades by covering upgrade options and common scenarios. For in-depth guidance tailored to your needs, use the scenario-based navigation paths at the end of this article.

## What this article covers

This technical reference provides comprehensive AKS upgrade fundamentals on:

- Manual versus automated upgrade options and when to use each.
- Common upgrade scenarios with specific recommendations.
- Optimization techniques for performance and minimal disruption.
- Troubleshooting guidance for capacity, drain failures, and timing issues.
- Validation processes and pre-upgrade checks.

This hub is best for helping you to understand upgrade mechanics, troubleshoot issues, optimize upgrade settings, and learn about technical implementation.

For more information, see these related articles:

- To upgrade your production AKS clusters, see
[AKS production upgrade strategies](aks-production-upgrade-strategies). - To get upgrade patterns for AKS clusters with stateful workloads, see
[Stateful workload upgrade patterns](stateful-workload-upgrades). - To use the scenario hub to help you choose the right AKS upgrade approach, see
[AKS upgrade scenarios: Choose your path](upgrade-scenarios-hub).

If you're new to AKS upgrades, start with the [upgrade scenarios hub](upgrade-scenarios-hub) for guided, scenario-based assistance.

## Quick navigation

| Your situation | Recommended path |
|---|---|
| Production cluster needs an upgrade |
|

[Stateful workload patterns](stateful-workload-upgrades)[Basic AKS cluster upgrade](upgrade-aks-cluster)[Upgrade scenarios hub](upgrade-scenarios-hub)[Node pool upgrades](manage-node-pools#upgrade-a-cluster-control-plane-with-multiple-node-pools)[Single node pool upgrade](node-image-upgrade#upgrade-a-specific-node-pool)## Upgrade options

### Perform manual upgrades

Manual upgrades let you control when your cluster upgrades to a new Kubernetes version. These upgrades are useful for testing or targeting a specific version:

[Upgrade an AKS cluster](upgrade-aks-cluster)[Upgrade multiple AKS clusters via Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/update-orchestration)[Upgrade the node image](node-image-upgrade)[Customize node surge upgrade](upgrade-aks-cluster#customize-node-surge-upgrade)[Process node OS updates](node-updates-kured)

### Configure automatic upgrades

Automatic upgrades keep your cluster on a supported version and up to date. Use these upgrades when you want to automate your settings:

[Automatically upgrade an AKS cluster](auto-upgrade-cluster)[Automatically upgrade multiple AKS clusters via Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/update-automation)[Use planned maintenance to schedule and control upgrades](planned-maintenance)[Stop AKS cluster upgrades automatically on API breaking changes (preview)](stop-cluster-upgrade-api-breaking-changes)[Automatically upgrade AKS cluster node operating system images](auto-upgrade-node-image)[Apply security updates to AKS nodes automatically by using GitHub actions](node-upgrade-github-actions)

### Special considerations for node pools that span multiple availability zones

AKS uses best-effort zone balancing in node groups. During an upgrade surge, the zones for surge nodes in virtual machine scale sets are unknown ahead of time, which can temporarily cause an unbalanced zone configuration. AKS deletes surge nodes after the upgrade and restores the original zone balance.

To keep zones balanced, set surge to a multiple of three nodes. Persistent volume claims that use Azure locally redundant storage disks are zone bound and might cause downtime if surge nodes are in a different zone. Use a [pod disruption budget (PDB)](https://kubernetes.io/docs/tasks/run-application/configure-pdb/) to maintain high availability during drains.

### Optimize upgrades to improve performance and minimize disruptions

Combine [planned maintenance window](planned-maintenance), [max surge](upgrade-aks-cluster#customize-node-surge-upgrade), [PDB](https://kubernetes.io/docs/tasks/run-application/configure-pdb/), [node drain timeout](upgrade-aks-cluster#set-node-drain-timeout-value), and [node soak time](upgrade-aks-cluster#set-node-soak-time-value) to increase the likelihood of successful, low-disruption upgrades:

[Planned maintenance window](planned-maintenance): Schedule auto-upgrade during low-traffic periods. We recommend at least four hours.[Max surge](upgrade-aks-node-pools-rolling#set-max-surge-value): Higher values speed upgrades but might disrupt workloads. We recommend 33% for production.[Max unavailable](upgrade-aks-node-pools-rolling#customize-unavailable-nodes): Use when capacity is limited.[Pod disruption budget](https://kubernetes.io/docs/tasks/run-application/configure-pdb/): Set to limit pods down during upgrades. Validate for your service.[Node drain timeout](upgrade-aks-cluster#set-node-drain-timeout-value): Configure pod eviction wait duration. The default is 30 minutes.[Node soak time](upgrade-aks-cluster#set-node-soak-time-value): Stagger upgrades to minimize downtime. The default is 0 minutes.

| Upgrade settings | How extra nodes are used | Expected behavior |
|---|---|---|
`maxSurge=5` , `maxUnavailable=0` |
5 surge nodes | Five nodes are surged for upgrade. |
`maxSurge=5` , `maxUnavailable=0` |
0-4 surge nodes | Upgrade fails because of insufficient surge nodes. |
`maxSurge=0` , `maxUnavailable=5` |
N/A | Five existing nodes are drained for upgrade. |

Note

Before you upgrade, check for API breaking changes and review the [AKS release notes](https://github.com/Azure/AKS/releases) to avoid disruptions.

## Validations used in the upgrade process

AKS performs pre-upgrade validations to ensure cluster health:

**API breaking changes:**Detects deprecated APIs.**Kubernetes upgrade version:**Ensures a valid upgrade path.**PDB configuration:**Checks for misconfigured PDBs (for example,`maxUnavailable=0`

).**Quota:**Confirms enough quota for surge nodes.**Subnet:**Verifies sufficient IP addresses.**Certificates/service principals:**Detects expired credentials.

These checks help to minimize upgrade failures and provide early visibility into issues.

## Common upgrade scenarios and recommendations

### Scenario 1: Capacity constraints

If your cluster is limited by product tier or regional capacity, upgrades might fail when surge nodes can't be provisioned. This situation is common with specialized product tiers (like GPU nodes) or in regions with limited resources. Errors such as `SKUNotAvailable`

, `AllocationFailed`

, or `OverconstrainedAllocationRequest`

might occur if `maxSurge`

is set too high for available capacity.

#### Recommendations to prevent or resolve

- Use
`maxUnavailable`

to upgrade by using existing nodes instead of surging new ones. For more information, see[Customize unavailable nodes during upgrade](upgrade-aks-cluster#customize-unavailable-nodes-during-upgrade). - Lower
`maxSurge`

to reduce extra capacity needs. For more information, see[Customize node surge upgrade](upgrade-aks-cluster#customize-node-surge-upgrade). - For security-only updates, use security patch reimages that don't require surge nodes. For more information, see
[Apply security and kernel updates to Linux nodes in Azure Kubernetes Service](node-updates-kured).

### Scenario 2: Node drain failures and PDBs

Upgrades require draining nodes (evicting pods). Drains can fail when pods are slow to terminate or strict [Pod Disruption Budgets (PDBs)](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/) block pod evictions.

Example error:

```
Code: UpgradeFailed
Message: Drain node ... failed when evicting pod ... Cannot evict pod as it would violate the pod's disruption budget.
```


#### Option 1: Force upgrade (bypass PDB)

Warning

Force upgrade bypasses Pod Disruption Budget (PDB) constraints and may cause service disruption by draining all pods simultaneously. Before using this option, first try to fix PDB misconfigurations (review the PDB minAvailable/maxUnavailable settings, ensure adequate pod replicas, verify PDBs aren't blocking all evictions).

Use force upgrade only when PDBs prevent critical upgrades and cannot be resolved. This will override PDB protections and potentially cause complete service unavailability during the upgrade.

**Requirements:** Azure CLI 2.79.0+ or AKS API version 2025-09-01+

```
az aks upgrade \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP_NAME \
--kubernetes-version $KUBERNETES_VERSION \
--enable-force-upgrade \
--upgrade-override-until 2023-10-01T13:00:00Z
```


Note

- The
`upgrade-override-until`

parameter defines when validation bypass ends (must be a future date/time) - If not specified, the window defaults to 3 days from current time
- The 'Z' indicates UTC/GMT time zone

Warning

When force upgrade is enabled, it takes precedence over all other drain configurations. The undrainable node behavior settings (Option 2) will not be applied when force upgrade is active.

#### Option 2: Handle undrainable nodes (honor PDB)

Use this conservative approach to honor PDBs while preventing upgrade failures.

**Configure undrainable node behavior:**

```
az aks nodepool update \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--name <node-pool-name> \
--undrainable-node-behavior Cordon \
--max-blocked-nodes 2 \
--drain-timeout 30
```


**Behavior options:**

**Schedule (default):**Deletes blocked node and surges replacement**Cordon (recommended):**Cordons node and labels it as`kubernetes.azure.com/upgrade-status=Quarantined`


**Max blocked nodes (preview):**

- Specifies how many nodes that fail to drain are tolerated
- Requires
`undrainable-node-behavior`

to be set - Defaults to
`maxSurge`

value (typically 10%) if not specified

##### Prerequisites for max blocked nodes

The Azure CLI

`aks-preview`

extension version 18.0.0b9 or later is required to use the max blocked nodes feature.`# Install or update the aks-preview extension az extension add --name aks-preview az extension update --name aks-preview`


##### Example configuration with max blocked nodes

```
az aks nodepool update \
--cluster-name jizenMC1 \
--name nodepool1 \
--resource-group jizenTestMaxBlockedNodesRG \
--max-surge 1 \
--undrainable-node-behavior Cordon \
--max-blocked-nodes 2 \
--drain-timeout 5
```


#### Recommendations to prevent drain failures

- Set
`maxUnavailable`

in PDBs to allow at least one pod eviction - Increase pod replicas to meet disruption budget requirements
- Extend drain timeout if workloads need more time. (The default is
*30 minutes*.) - Test PDBs in staging, monitor upgrade events, and use blue-green deployments for critical workloads. For more information, see
[Blue-green deployment of AKS clusters](/en-us/azure/architecture/guide/aks/blue-green-deployment-for-aks).

##### Verify undrainable nodes

The blocked nodes are unscheduled for pods and marked with the label

`"kubernetes.azure.com/upgrade-status: Quarantined"`

.Verify the label on any blocked nodes when there's a drain node failure on upgrade:

`kubectl get nodes --show-labels=true`


##### Resolve undrainable nodes

Remove the responsible PDB:

`kubectl delete pdb <pdb-name>`

Remove the

`kubernetes.azure.com/upgrade-status: Quarantined`

label:`kubectl label nodes <node-name> <label-name>`

Optionally, delete the blocked node:

`az aks nodepool delete-machines --cluster-name <cluster-name> --machine-names <machine-name> --name <node-pool-name> --resource-group <resource-group-name>`

After you finish this step, you can reconcile the cluster status by performing any update operation without the optional fields as outlined in

[az aks](/en-us/cli/azure/aks#az-aks-update). Alternatively, you can scale the node pool to the same number of nodes as the count of upgraded nodes. This action ensures that the node pool gets to its intended original size. AKS prioritizes the removal of the blocked nodes. This command also restores the cluster provisioning status to`Succeeded`

. In the following example,`2`

is the total number of upgraded nodes.`# Update the cluster to restore the provisioning status az aks update --resource-group <resource-group-name> --name <cluster-name> # Scale the node pool to restore the original size az aks nodepool scale --resource-group <resource-group-name> --cluster-name <cluster-name> --name <node-pool-name> --node-count 2`


### Scenario 3: Slow upgrades

Conservative settings or node-level issues can delay upgrades, which affects your ability to stay current with patches and improvements.

Common causes of slow upgrades include:

- Low
`maxSurge`

or`maxUnavailable`

values (limits parallelism). - High soak times (long waits between node upgrades).
- Drain failures (see
[Node drain failures](#scenario-2-node-drain-failures-and-pdbs)).

#### Recommendations to prevent or resolve

- Use
`maxSurge=33%`

,`maxUnavailable=1`

for production. - Use
`maxSurge=50%`

,`maxUnavailable=2`

for dev/test. - Use OS Security Patch for fast, targeted patching (avoids full node reimaging).
- Enable
`undrainableNodeBehavior`

to avoid upgrade blockers.

### Scenario 4: IP exhaustion

Surge nodes require more IPs. If the subnet is near capacity, node provisioning can fail (for example, `Error: SubnetIsFull`

). This scenario is common with Azure Container Networking Interface, high `maxPods`

, or large node counts.

#### Recommendations to prevent or resolve

Ensure that your subnet has enough IPs for all nodes, surge nodes, and pods. The formula is

`Total IPs = (Number of nodes + maxSurge) * (1 + maxPods)`

.Reclaim unused IPs or expand the subnet (for example, from /24 to /22).

Lower

`maxSurge`

if subnet expansion isn't possible:`az aks nodepool update \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --max-surge 10%`

Monitor IP usage with Azure Monitor or custom alerts.

Reduce

`maxPods`

per node, clean up orphaned load balancer IPs, and plan subnet sizing for high-scale clusters.

## Frequently asked questions

### Can I use open-source tools for validation?

Yes. Many open-source tools integrate well with AKS upgrade processes:

[kube-no-trouble (kubent)](https://github.com/doitintl/kube-no-trouble): Scans for deprecated APIs before upgrades.[Trivy](https://aquasecurity.github.io/trivy/): Security scanning for container images and Kubernetes configurations.[Sonobuoy](https://sonobuoy.io/): Kubernetes conformance testing and cluster validation.[kube-bench](https://github.com/aquasecurity/kube-bench): Security benchmark checks against Center for Internet Security standards.[Polaris](https://github.com/FairwindsOps/polaris): Validation of Kubernetes best practices.[kubectl-neat](https://github.com/itaysk/kubectl-neat): Clean up Kubernetes manifests for validation.

### How do I validate API compatibility before upgrading?

Run deprecation checks by using tools like kubent:

```
# Install and run API deprecation scanner
kubectl apply -f https://github.com/doitintl/kube-no-trouble/releases/latest/download/knt-full.yaml
# Check for deprecated APIs in your cluster
kubectl run knt --image=doitintl/knt:latest --rm -it --restart=Never -- \
-c /kubeconfig -o json > api-deprecation-report.json
# Review findings
cat api-deprecation-report.json | jq '.[] | select(.deprecated==true)'
```


### What makes AKS upgrades different from other Kubernetes platforms?

AKS provides several unique advantages:

- Native Azure integration with Azure Traffic Manager, Azure Load Balancer, and networking.
- Azure Kubernetes Fleet Manager for coordinated multicluster upgrades.
- Automatic node image patching without manual node management.
- Built-in validation for quota, networking, and credentials.
- Azure support for upgrade-related issues.

## Choose your upgrade path

This article provided you with a technical foundation. Now select your scenario-based path.

### Ready to execute?

| If you have... | Then go to... |
|---|---|
| Production environment |
|

[Stateful workload patterns](stateful-workload-upgrades): Safe upgrade patterns for data persistence[Upgrade scenarios hub](upgrade-scenarios-hub): Decision tree for complex setups[Upgrade an AKS cluster](upgrade-aks-cluster): Step-by-step cluster upgrade### Still deciding?

Use the [upgrade scenarios hub](upgrade-scenarios-hub) for a guided decision tree that considers your:

- Downtime tolerance
- Environment complexity
- Risk profile
- Timeline constraints

## Next tasks

- Review
[AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices)for best practices and planning tips before you start any upgrade. - Always check for
[API breaking changes](https://aka.ms/aks/breakingchanges)and validate your workload's compatibility with the target Kubernetes version. - Test upgrade settings (such as
`maxSurge`

,`maxUnavailable`

, and PDBs) in a staging environment to minimize production risk. - Monitor upgrade events and cluster health throughout the process.


---

<!-- DOCUMENTO FUSIONADO: _kubernetes-action_how-to-enable-ebpf-host-routing.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: kubernetes-action.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/kubernetes-action -->

# Build, test, and deploy containers to Azure Kubernetes Service (AKS) using GitHub Actions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[GitHub Actions](https://docs.github.com/en/actions) gives you the flexibility to build an automated software development lifecycle workflow. You can use multiple Kubernetes actions to deploy to containers from Azure Container Registry (ACR) to Azure Kubernetes Service (AKS) with GitHub Actions.

## Prerequisites

- An Azure account with an active subscription. If you don't have one,
[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - A GitHub account. If you don't have one,
[sign up for free](https://github.com/join).- When using GitHub Actions, you need to configure the integration between Azure and your GitHub repository. To configure the integration, see
[Use GitHub Actions to connect to Azure](/en-us/azure/developer/github/connect-from-azure?tabs=azure-cli%2Clinux).

- When using GitHub Actions, you need to configure the integration between Azure and your GitHub repository. To configure the integration, see
- An existing AKS cluster with an attached ACR. If you don't have one, see
[Authenticate with ACR from AKS](cluster-container-registry-integration).

## GitHub Actions for AKS

With GiHub Actions, you can automate your software development workflows from within GitHub. For more information, see [GitHub Actions for Azure](/en-us/azure/developer/github/github-actions).

The following table lists the available actions for AKS:

| Name | Description | More details |
|---|---|---|
`azure/aks-set-context` |
Set the target AKS cluster context for other actions to use or run any kubectl commands. |
|

`azure/k8s-set-context`

[azure/k8s-set-context](https://github.com/Azure/k8s-set-context)`azure/k8s-bake`

[azure/k8s-bake](https://github.com/Azure/k8s-bake)`azure/k8s-create-secret`

[azure/k8s-create-secret](https://github.com/Azure/k8s-create-secret)`azure/k8s-deploy`

[azure/k8s-deploy](https://github.com/Azure/k8s-deploy)`azure/k8s-lint`

[azure/k8s-lint](https://github.com/Azure/k8s-lint)`azure/setup-helm`

[azure/setup-helm](https://github.com/Azure/setup-helm)`azure/setup-kubectl`

[azure/setup-kubectl](https://github.com/Azure/setup-kubectl)`azure/k8s-artifact-substitute`

[azure/k8s-artifact-substitute](https://github.com/Azure/k8s-artifact-substitute)`azure/aks-create-action`

[azure/aks-create-action](https://github.com/Azure/aks-create-action)`azure/aks-github-runner`

[azure/aks-github-runner](https://github.com/Azure/aks-github-runner)`azure/acr-build`

[azure/acr-build](https://github.com/Azure/acr-build)## Use GitHub Actions with AKS

As an example, you can use GitHub Actions to deploy an application to your AKS cluster every time a change is pushed to your GitHub repository. This example uses the [Azure Vote](https://github.com/Azure-Samples/azure-voting-app-redis) application.

Note

This example uses a service principal for authentication with your ACR and AKS cluster. Alternatively, you can configure Open ID Connect (OIDC) and update the `azure/login`

action to use OIDC. For more information, see [Set up Azure Login with OpenID Connect authentication](/en-us/azure/developer/github/connect-from-azure?tabs=azure-cli%2Clinux#use-the-azure-login-action-with-openid-connect).

### Fork and update the repository

Navigate to the

[Azure Vote](https://github.com/Azure-Samples/azure-voting-app-redis)repository and select**Fork**.Update the

`azure-vote-all-in-one-redis.yaml`

to use your ACR for the`azure-vote-front`

image. Replace`<registryName>`

with the name of your registry.`... containers: - name: azure-vote-front image: <registryName>.azurecr.io/azuredocs/azure-vote-front:v1 ...`

Commit the updated

`azure-vote-all-in-one-redis.yaml`

to your repository.

### Create secrets

Create a service principal to access your resource group with the

`Contributor`

role using thecommand. Replace`az ad sp create-for-rbac`

`<SUBSCRIPTION_ID>`

with the subscription ID of your Azure account and`<RESOURCE_GROUP>`

with the name of the resource group containing your ACR.`az ad sp create-for-rbac \ --name "ghActionAzureVote" \ --scope /subscriptions/<SUBSCRIPTION_ID>/resourceGroups/<RESOURCE_GROUP> \ --role Contributor \ --json-auth`

Your output should look similar to the following example output:

`{ "clientId": <clientId>, "clientSecret": <clientSecret>, "subscriptionId": <subscriptionId>, "tenantId": <tenantId>, ... }`

Navigate to your GitHub repository settings and select

**Security**>**Secrets and variables**>**Actions**.For each secret, select

**New Repository Secret**and enter the name and value of the secret.Secret name Secret value AZURE_CREDENTIALS The entire JSON output from the `az ad sp create-for-rbac`

command.service_principal The value of `<clientId>`

.service_principal_password The value of `<clientSecret>`

.subscription The value of `<subscriptionId>`

.tenant The value of `<tenantId>`

.registry The name of your registry. repository azuredocs resource_group The name of your resource group. cluster_name The name of your cluster.

For more information about creating secrets, see [Encrypted Secrets](https://docs.github.com/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository).

### Create actions file

In your repository, create a

`.github/workflows/main.yml`

and paste in the following contents:`name: build_deploy_aks on: push: paths: - "azure-vote/**" jobs: build: runs-on: ubuntu-latest steps: - name: Checkout source code uses: actions/checkout@v3 - name: ACR build id: build-push-acr uses: azure/acr-build@v1 with: service_principal: ${{ secrets.service_principal }} service_principal_password: ${{ secrets.service_principal_password }} tenant: ${{ secrets.tenant }} registry: ${{ secrets.registry }} repository: ${{ secrets.repository }} image: azure-vote-front folder: azure-vote branch: master tag: ${{ github.sha }} - name: Azure login id: login uses: azure/login@v1.4.3 with: creds: ${{ secrets.AZURE_CREDENTIALS }} - name: Set AKS context id: set-context uses: azure/aks-set-context@v3 with: resource-group: '${{ secrets.resource_group }}' cluster-name: '${{ secrets.cluster_name }}' - name: Setup kubectl id: install-kubectl uses: azure/setup-kubectl@v3 - name: Deploy to AKS id: deploy-aks uses: Azure/k8s-deploy@v4 with: namespace: 'default' manifests: | azure-vote-all-in-one-redis.yaml images: '${{ secrets.registry }}.azurecr.io/${{ secrets.repository }}/azure-vote-front:${{ github.sha }}' pull-images: false`

The

`on`

section contains the event that triggers the action. In the example file, the action triggers when a change is pushed to the`azure-vote`

directory.The

`steps`

section contains each distinct action:*Checkout source code*uses the[GitHub Actions Checkout Action](https://github.com/actions/checkout)to clone the repository.*ACR build*uses the[Azure Container Registry Build Action](https://github.com/Azure/acr-build)to build the image and upload it to your registry.*Azure login*uses the[Azure Login Action](https://github.com/Azure/login)to sign in to your Azure account.*Set AKS context*uses the[Azure AKS Set Context Action](https://github.com/Azure/aks-set-context)to set the context for your AKS cluster.*Setup kubectl*uses the[Azure AKS Setup Kubectl Action](https://github.com/Azure/setup-kubectl)to install kubectl on your runner.*Deploy to AKS*uses the[Azure Kubernetes Deploy Action](https://github.com/Azure/k8s-deploy)to deploy the application to your Kubernetes cluster.

Commit the

`.github/workflows/main.yml`

file to your repository.To confirm the action is working, update the

`azure-vote/azure-vote/config_file.cfg`

with the following contents:`# UI Configurations TITLE = 'Azure Voting App' VOTE1VALUE = 'Fish' VOTE2VALUE = 'Dogs' SHOWHOST = 'false'`

Commit the updated

`azure-vote/azure-vote/config_file.cfg`

to your repository.In your repository, select

**Actions**and confirm a workflow is running. Then, confirm the workflow has a green checkmark and the updated application is deployed to your cluster.

## Next steps

Review the following starter workflows for AKS. For more information, see [Using starter workflows](https://docs.github.com/actions/using-workflows/using-starter-workflows#using-starter-workflows).


---

<!-- DOCUMENTO FUSIONADO: how-to-enable-ebpf-host-routing.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/how-to-enable-ebpf-host-routing -->

# Enable eBPF Host Routing with Advanced Container Networking Services (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

eBPF Host Routing with Advanced Container Networking Services is currently in PREVIEW.

See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

This article shows you how to enable eBPF Host Routing with Advanced Container Networking Services (ACNS) on Azure Kubernetes Service (AKS) clusters.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of Azure CLI required for the steps in this article is 2.71.0. To find the version, run

`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).eBPF Host Routing is only supported with Azure CNI powered by Cilium. See

[Configure Azure CNI Powered by Cilium](/en-us/azure/aks/azure-cni-powered-by-cilium)for more information on managed Cilium clusters.Review the

[Limitations](container-network-performance-ebpf-host-routing#limitations)section for node requirements and compatibility with existing iptable rules.

### Install the `aks-preview`

Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install or update the Azure CLI preview extension using the [ az extension add](/en-us/cli/azure/extension#az-extension-add) or

[command.](/en-us/cli/azure/extension#az-extension-update)

`az extension update`

The minimum version of the aks-preview Azure CLI extension is `14.0.0b6`


```
# Install the aks-preview extension
az extension add --name aks-preview
# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```


### Register the `AdvancedNetworkingPerformancePreview`

feature flag

Register the `AdvancedNetworkingPerformancePreview`

feature flag using the [ az feature register](/en-us/cli/azure/feature#az-feature-register) command.

```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingPerformancePreview"
```


Verify successful registration using the [ az feature show](/en-us/cli/azure/feature#az-feature-show) command. It takes a few minutes for the registration to complete.

```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingPerformancePreview"
```


Once the feature shows `Registered`

, refresh the registration of the `Microsoft.ContainerService`

resource provider using the [ az provider register](/en-us/cli/azure/provider#az-provider-register) command.

### Enable Advanced Container Networking Services and eBPF Host Routing

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. These features encompass:

**Container Network Observability:**Provides insights into your network traffic. To learn more visit[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more visit[Container Network Security](advanced-container-networking-services-overview#container-network-security).**Container Network Performance:**Improves latency and throughput for pod network traffic. To learn more visit[Container Network Performance](advanced-container-networking-services-overview#container-network-performance)

Note

Clusters with the Cilium data plane support Container Network Performance with eBPF Host Routing starting with Kubernetes version 1.33.

Warning

The only compatible OS versions are Ubuntu 24.04 or Azure Linux 3.0.

Create an Azure resource group for the cluster using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
export LOCATION="<location>"
az group create --location $LOCATION --name <resourcegroup-name>
```


Create a new AKS cluster with eBPF Host Routing by enabling ACNS through `--enable-acns`

and setting the acceleration mode with `--acns-datapath-acceleration-mode BpfVeth`

.

```
# Set environment variables for the AKS cluster name and resource group. Make sure to replace the placeholders with your own values.
export CLUSTER_NAME="<aks-cluster-name>"
export RESOURCE_GROUP="<resourcegroup-name>"
export LOCATION="<location>"
export OS_SKU="<os-sku>" # Use AzureLinux or Ubuntu2404
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--location $LOCATION \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--kubernetes-version 1.33 \
--os-sku $OS_SKU \
--enable-acns \
--acns-datapath-acceleration-mode BpfVeth \
--generate-ssh-keys
```


### Enable eBPF Host Routing with Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the Advanced Container Networking Services flag,

`--enable-acns`

, updates an existing AKS cluster with `--acns-datapath-acceleration-mode BpfVeth`

to enable Advanced Container Networking Services features that includes [Container Network Observability](advanced-container-networking-services-overview#container-network-observability),

[Container Network Security](advanced-container-networking-services-overview#container-network-security), and

[Container Network Performance](advanced-container-networking-services-overview#container-network-performance).

Note

Enabling eBPF Host Routing on an existing cluster may disrupt existing connections.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns \
--acns-datapath-acceleration-mode BpfVeth
```


## Disabling eBPF Host Routing on an existing cluster

eBPF Host Routing can be disabled independently without affecting other ACNS features. To disable it, set the flag `--acns-datapath-acceleration-mode=None`

.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns \
--acns-datapath-acceleration-mode None
```


## Related content

- Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services.
