---
merged_at: 2026-01-25T12:25:33.981672
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: best-practices-app-cluster-reliability.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/best-practices-app-cluster-reliability -->

# Deployment and cluster reliability best practices for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides best practices for cluster reliability implemented both at a deployment and cluster level for your Azure Kubernetes Service (AKS) workloads. The article is intended for cluster operators and developers who are responsible for deploying and managing applications in AKS.

The best practices in this article are organized into the following categories:

## Deployment level best practices

The following deployment level best practices help ensure high availability and reliability for your AKS workloads. These best practices are local configurations that you can implement in the YAML files for your pods and deployments.

Note

Make sure you implement these best practices every time you deploy an update to your application. If not, you might experience issues with your application's availability and reliability, such as unintentional application downtime.

### Pod CPU and memory limits


Best practice guidanceSet pod CPU and memory limits for all pods to ensure that pods don't consume all resources on a node and to provide protection during service threats, such as DDoS attacks.


Pod CPU and memory limits define the maximum amount of CPU and memory a pod can use. When a pod exceeds its defined limits, it gets marked for removal. For more information, see [CPU resource units in Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-cpu) and [Memory resource units in Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-memory).

Setting CPU and memory limits helps you maintain node health and minimizes impact to other pods on the node. Avoid setting a pod limit higher than your nodes can support. Each AKS node reserves a set amount of CPU and memory for the core Kubernetes components. If you set a pod limit higher than the node can support, your application might try to consume too many resources and negatively impact other pods on the node. Cluster administrators need to set resource quotas on a namespace that requires setting resource requests and limits. For more information, see [Enforce resource quotas in AKS](operator-best-practices-scheduler#enforce-resource-quotas).

In the following example pod definition file, the `resources`

section sets the CPU and memory limits for the pod:

```
kind: Pod
apiVersion: v1
metadata:
name: mypod
spec:
containers:
- name: mypod
image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
resources:
requests:
cpu: 100m
memory: 128Mi
limits:
cpu: 250m
memory: 256Mi
```


Tip

You can use the `kubectl describe node`

command to view the CPU and memory capacity of your nodes, as shown in the following example:

```
kubectl describe node <node-name>
# Example output
Capacity:
cpu: 8
ephemeral-storage: 129886128Ki
hugepages-1Gi: 0
hugepages-2Mi: 0
memory: 32863116Ki
pods: 110
Allocatable:
cpu: 7820m
ephemeral-storage: 119703055367
hugepages-1Gi: 0
hugepages-2Mi: 0
memory: 28362636Ki
pods: 110
```


For more information, see [Assign CPU Resources to Containers and Pods](https://kubernetes.io/docs/tasks/configure-pod-container/assign-cpu-resource/) and [Assign Memory Resources to Containers and Pods](https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/).

### Vertical Pod Autoscaler (VPA)


Best practice guidanceUse Vertical Pod Autoscaler (VPA) to automatically adjust CPU and memory requests for your pods based on their actual usage.


While not directly implemented through the pod YAML, the Vertical Pod Autoscaler (VPA) helps optimize resource allocation by automatically adjusting the CPU and memory requests for your pods. This ensures that your applications have the resources they need to run efficiently without overprovisioning or underprovisioning.

VPA operates in three modes:

**Off**: Only provides recommendations without applying changes.**Auto**: Automatically updates pod resource requests during pod restarts.**Initial**: Sets resource requests only during pod creation.

The following example shows how to configure a VPA resource in Kubernetes:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: my-vpa
spec:
targetRef:
apiVersion: "apps/v1"
kind: Deployment
name: my-deployment
updatePolicy:
updateMode: "Auto" # Options: Off, Auto, Initial
```


For more information, see [Vertical Pod Autoscaler documentation](https://github.com/kubernetes/autoscaler/tree/master/vertical-pod-autoscaler).

### Pod Disruption Budgets (PDBs)


Best practice guidanceUse Pod Disruption Budgets (PDBs) to ensure that a minimum number of pods remain available during

voluntary disruptions, such as upgrade operations or accidental pod deletions.

[Pod Disruption Budgets (PDBs)](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/#pod-disruption-budgets) allow you to define how deployments or replica sets respond during voluntary disruptions, such as upgrade operations or accidental pod deletions. Using PDBs, you can define a minimum or maximum unavailable resource count. PDBs only affect the Eviction API for voluntary disruptions.

For example, let's say you need to perform a cluster upgrade and already have a PDB defined. Before performing the cluster upgrade, the Kubernetes scheduler ensures that the minimum number of pods defined in the PDB are available. If the upgrade would cause the number of available pods to fall below the minimum defined in the PDBs, the scheduler schedules extra pods on other nodes before allowing the upgrade to proceed. If you don't set a PDB, the scheduler doesn't have any constraints on the number of pods that can be unavailable during the upgrade, which can lead to a lack of resources and potential cluster outages.

In the following example PDB definition file, the `minAvailable`

field sets the minimum number of pods that must remain available during voluntary disruptions. The value can be an absolute number (for example, *3*) or a percentage of the desired number of pods (for example, *10%*).

```
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: mypdb
spec:
minAvailable: 3 # Minimum number of pods that must remain available during voluntary disruptions
selector:
matchLabels:
app: myapp
```


For more information, see [Plan for availability using PDBs](operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets) and [Specifying a Disruption Budget for your Application](https://kubernetes.io/docs/tasks/run-application/configure-pdb/).

### Graceful termination for pods


Best practice guidanceUtilize

`PreStop`

hooks and configure an appropriate`terminationGracePeriodSeconds`

value to ensure pods are terminated gracefully.

Graceful termination ensures that pods are given enough time to clean up resources, complete ongoing tasks, or notify dependent services before being terminated. This is particularly important for stateful applications or services that require proper shutdown procedures.

#### Using `PreStop`

hooks

A `PreStop`

hook is called immediately before a container is terminated due to an API request or management event, such as preemption, resource contention, or a liveness/startup probe failure. The `PreStop`

hook allows you to define custom commands or scripts to execute before the container is stopped. For example, you can use it to flush logs, close database connections, or notify other services of the shutdown.

The following example pod definition file shows how to use a `PreStop`

hook to ensure graceful termination of a container:

```
apiVersion: v1
kind: Pod
metadata:
name: lifecycle-demo
spec:
containers:
- name: lifecycle-demo-container
image: nginx
lifecycle:
preStop:
exec:
command: ["/bin/sh", "-c", "nginx -s quit; while killall -0 nginx; do sleep 1; done"]
```


#### Configuring `terminationGracePeriodSeconds`


The `terminationGracePeriodSeconds`

field specifies the amount of time Kubernetes waits before forcefully terminating a pod. This period includes the time taken to execute the `PreStop`

hook. If the `PreStop`

hook doesn't complete within the grace period, the pod is forcefully terminated.

For example, the following pod definition sets a termination grace period of 30 seconds:

```
apiVersion: v1
kind: Pod
metadata:
name: example-pod
spec:
terminationGracePeriodSeconds: 30
containers:
- name: example-container
image: nginx
```


For more information, see [Container lifecycle hooks](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/#container-hooks) and [Termination of Pods](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-termination).

### High availability during upgrades

#### Using `maxSurge`

for faster updates


Best practice guidanceConfigure the

`maxSurge`

field to allow additional pods to be created during rolling updates, enabling faster updates with minimal downtime.

The `maxSurge`

field specifies the maximum number of additional pods that can be created beyond the desired number of pods during a rolling update. This allows new pods to be created and become ready before old pods are terminated, ensuring faster updates and reducing the risk of downtime.

The following example deployment manifest demonstrates how to configure `maxSurge`

:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: nginx-deployment
labels:
app: nginx
spec:
replicas: 3
selector:
matchLabels:
app: nginx
template:
metadata:
labels:
app: nginx
spec:
containers:
- name: nginx
image: nginx:1.14.2
ports:
- containerPort: 80
strategy:
type: RollingUpdate
rollingUpdate:
maxSurge: 33% # Maximum number of additional pods created during the update
```


By setting `maxSurge`

to 3, this configuration ensures that up to three additional pods can be created during the rolling update, speeding up the deployment process while maintaining availability of your application.
For more information, see [Rolling Updates in Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-update-deployment).

#### Using `maxUnavailable`

for controlled updates


Best practice guidanceConfigure the

`maxUnavailable`

field to limit the number of pods that can be unavailable during rolling updates, ensuring your application remains operational with minimal disruption.

The `maxUnavailable`

field is particularly useful for applications that require are compute intensive or have specific infrastructure needs. It specifies the maximum number of pods that can be unavailable at any given time during a rolling update. This ensures that a portion of your application remains functional while new pods are being deployed and old ones are terminated.

You can set `maxUnavailable`

as an absolute number (e.g., `1`

) or a percentage of the desired number of pods (e.g., `25%`

). For example, if your application has four replicas and you set `maxUnavailable`

to `1`

, Kubernetes ensures that at least three pods remain available during the update process.

The following example deployment manifest demonstrates how to configure `maxUnavailable`

:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: nginx-deployment
labels:
app: nginx
spec:
replicas: 4
selector:
matchLabels:
app: nginx
template:
metadata:
labels:
app: nginx
spec:
containers:
- name: nginx
image: nginx:1.14.2
ports:
- containerPort: 80
strategy:
type: RollingUpdate
rollingUpdate:
maxUnavailable: 1 # Maximum number of pods that can be unavailable during the update
```


In this example, setting `maxUnavailable`

to `1`

ensures that no more than one pod is unavailable at any given time during the rolling update. This configuration is ideal for applications which require specialized compute, where maintaining a minimum level of service availability is critical.

For more information, see [Rolling Updates in Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-update-deployment).

### Pod topology spread constraints


Best practice guidanceUse pod topology spread constraints to ensure that pods are spread across different nodes or zones to improve availability and reliability.


You can use pod topology spread constraints to control how pods are spread across your cluster based on the topology of the nodes and spread pods across different nodes or zones to improve availability and reliability.

The following example pod definition file shows how to use the `topologySpreadConstraints`

field to spread pods across different nodes:

```
apiVersion: v1
kind: Pod
metadata:
name: example-pod
spec:
# Configure a topology spread constraint
topologySpreadConstraints:
- maxSkew: <integer>
minDomains: <integer> # optional
topologyKey: <string>
whenUnsatisfiable: <string>
labelSelector: <object>
matchLabelKeys: <list> # optional
nodeAffinityPolicy: [Honor|Ignore] # optional
nodeTaintsPolicy: [Honor|Ignore] # optional
```


For more information, see [Pod Topology Spread Constraints](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/).

### Readiness, liveness, and startup probes


Best practice guidanceConfigure readiness, liveness, and startup probes when applicable to improve resiliency for high loads and lower container restarts.


#### Readiness probes

In Kubernetes, the kubelet uses readiness probes to know when a container is ready to start accepting traffic. A pod is considered *ready* when all of its containers are ready. When a pod is *not ready*, it's removed from service load balancers. For more information, see [Readiness Probes in Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-readiness-probes).

The following example pod definition file shows a readiness probe configuration:

```
readinessProbe:
exec:
command:
- cat
- /tmp/healthy
initialDelaySeconds: 5
periodSeconds: 5
```


For more information, see [Configure readiness probes](/en-us/azure/container-instances/container-instances-readiness-probe).

#### Liveness probes

In Kubernetes, the kubelet uses liveness probes to know when to restart a container. If a container fails its liveness probe, the container is restarted. For more information, see [Liveness Probes in Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/).

The following example pod definition file shows a liveness probe configuration:

```
livenessProbe:
exec:
command:
- cat
- /tmp/healthy
```


Another kind of liveness probe uses an HTTP GET request. The following example pod definition file shows an HTTP GET request liveness probe configuration:

```
apiVersion: v1
kind: Pod
metadata:
labels:
test: liveness
name: liveness-http
spec:
containers:
- name: liveness
image: registry.k8s.io/liveness
args:
- /server
livenessProbe:
httpGet:
path: /healthz
port: 8080
httpHeaders:
- name: Custom-Header
value: Awesome
initialDelaySeconds: 3
periodSeconds: 3
```


For more information, see [Configure liveness probes](/en-us/azure/container-instances/container-instances-liveness-probe) and [Define a liveness HTTP request](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-a-liveness-http-request).

#### Startup probes

In Kubernetes, the kubelet uses startup probes to know when a container application has started. When you configure a startup probe, readiness and liveness probes don't start until the startup probe succeeds, ensuring the readiness and liveness probes don't interfere with application startup. For more information, see [Startup Probes in Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-startup-probes).

The following example pod definition file shows a startup probe configuration:

```
startupProbe:
httpGet:
path: /healthz
port: 8080
failureThreshold: 30
periodSeconds: 10
```


### Multi-replica applications


Best practice guidanceDeploy at least two replicas of your application to ensure high availability and resiliency in node-down scenarios.


In Kubernetes, you can use the `replicas`

field in your deployment to specify the number of pods you want to run. Running multiple instances of your application helps ensure high availability and resiliency in node-down scenarios. If you have [availability zones](#availability-zones) enabled, you can use the `replicas`

field to specify the number of pods you want to run across multiple availability zones.

The following example pod definition file shows how to use the `replicas`

field to specify the number of pods you want to run:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: nginx-deployment
labels:
app: nginx
spec:
replicas: 3
selector:
matchLabels:
app: nginx
template:
metadata:
labels:
app: nginx
spec:
containers:
- name: nginx
image: nginx:1.14.2
ports:
- containerPort: 80
```


For more information, see [Recommended active-active high availability solution overview for AKS](active-active-solution) and [Replicas in Deployment Specs](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#replicas).

## Cluster and node pool level best practices

The following cluster and node pool level best practices help ensure high availability and reliability for your AKS clusters. You can implement these best practices when creating or updating your AKS clusters.

### Availability zones


Best practice guidanceUse multiple availability zones when creating an AKS cluster to ensure high availability in zone-down scenarios. Keep in mind that you can't change the availability zone configuration after creating the cluster.


[Availability zones](/en-us/azure/reliability/availability-zones-overview) are separated groups of datacenters within a region. These zones are close enough to have low-latency connections to each other, but far enough apart to reduce the likelihood that more than one zone is affected by local outages or weather. Using availability zones helps your data stay synchronized and accessible in zone-down scenarios. For more information, see [Running in multiple zones](https://kubernetes.io/docs/setup/best-practices/multiple-zones/).

### Cluster autoscaling


Best practice guidanceUse cluster autoscaling to ensure that your cluster can handle increased load and to reduce costs during low load.


To keep up with application demands in AKS, you might need to adjust the number of nodes that run your workloads. The cluster autoscaler component watches for pods in your cluster that can't be scheduled because of resource constraints. When the cluster autoscaler detects issues, it scales up the number of nodes in the node pool to meet the application demand. It also regularly checks nodes for a lack of running pods and scales down the number of nodes as needed. For more information, see [Cluster autoscaling in AKS](cluster-autoscaler-overview).

You can use the `--enable-cluster-autoscaler`

parameter when creating an AKS cluster to enable the cluster autoscaler, as shown in the following example:

```
az aks create \
--resource-group myResourceGroup \
--name myAKSCluster \
--node-count 2 \
--vm-set-type VirtualMachineScaleSets \
--load-balancer-sku standard \
--enable-cluster-autoscaler \
--min-count 1 \
--max-count 3 \
--generate-ssh-keys
```


You can also enable the cluster autoscaler on an existing node pool and configure more granular details of the cluster autoscaler by changing the default values in the cluster-wide autoscaler profile.

For more information, see [Use the cluster autoscaler in AKS](cluster-autoscaler).

### Standard Load Balancer


Best practice guidanceUse the Standard Load Balancer to provide greater reliability and resources, support for multiple availability zones, HTTP probes, and functionality across multiple data centers.


In Azure, the [Standard Load Balancer](/en-us/azure/load-balancer/skus) SKU is designed to be equipped for load balancing network layer traffic when high performance and low latency are needed. The Standard Load Balancer routes traffic within and across regions and to availability zones for high resiliency. The Standard SKU is the recommended and default SKU to use when creating an AKS cluster.

Important

On September 30, 2025, Basic Load Balancer will be retired. For more information, see the [official announcement](https://azure.microsoft.com/updates/azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer/). We recommend that you use the Standard Load Balancer for new deployments and upgrade existing deployments to the Standard Load Balancer. For more information, see [Upgrading from Basic Load Balancer](/en-us/azure/load-balancer/load-balancer-basic-upgrade-guidance).

The following example shows a `LoadBalancer`

service manifest that uses the Standard Load Balancer:

```
apiVersion: v1
kind: Service
metadata:
annotations:
service.beta.kubernetes.io/azure-load-balancer-ipv4 # Service annotation for an IPv4 address
name: azure-load-balancer
spec:
type: LoadBalancer
ports:
- port: 80
selector:
app: azure-load-balancer
```


For more information, see [Use a standard load balancer in AKS](load-balancer-standard).

Tip

You can also use an [ingress controller](app-routing) or a [service mesh](istio-deploy-ingress) to manage network traffic, with each option providing different features and capabilities.

### System node pools

#### Use dedicated system node pools


Best practice guidanceUse system node pools to ensure no other user applications run on the same nodes, which can cause resource scarcity and impact system pods.


Use dedicated system node pools to ensure no other user application runs on the same nodes, which can cause scarcity of resources and potential cluster outages because of race conditions. To use a dedicated system node pool, you can use the `CriticalAddonsOnly`

taint on the system node pool. For more information, see [Use system node pools in AKS](use-system-pools#system-and-user-node-pools).

#### Autoscaling for system node pools


Best practice guidanceConfigure the autoscaler for system node pools to set minimum and maximum scale limits for the node pool.


Use the autoscaler on node pools to configure the minimum and maximum scale limits for the node pool. The system node pool should always be able to scale to meet the demands of system pods. If the system node pool is unable to scale, the cluster runs out of resources to help manage scheduling, scaling, and load balancing, which can lead to an unresponsive cluster.

For more information, see [Use the cluster autoscaler on node pools](cluster-autoscaler#use-the-cluster-autoscaler-on-node-pools).

#### At least two nodes per system node pool


Best practice guidanceEnsure that system node pools have at least two nodes to ensure resiliency against freeze/upgrade scenarios, which can lead to nodes being restarted or shut down.


System node pools are used to run system pods, such as the kube-proxy, coredns, and the Azure CNI plugin. We recommend that you * ensure that system node pools have at least two nodes* to ensure resiliency against freeze/upgrade scenarios, which can lead to nodes being restarted or shut down. For more information, see

[Manage system node pools in AKS](use-system-pools).

### Upgrade configurations for node pools

#### Using `maxSurge`

for node pool upgrades


Best practice guidanceConfigure the

`maxSurge`

setting for node pool upgrades to improve reliability and minimize downtime during upgrade operations.

The `maxSurge`

setting specifies the maximum number of additional nodes that can be created during an upgrade. This ensures that new nodes are provisioned and ready before old nodes are drained and removed, reducing the risk of application downtime.

For example, the following Azure CLI command sets `maxSurge`

to 1 for a node pool:

```
az aks nodepool update \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name myNodePool \
--max-surge 1
```


By configuring `maxSurge`

, you can ensure that upgrades are performed faster while maintaining application availability.

For more information, see [Upgrade node pools in AKS](upgrade-cluster).

#### Using `maxUnavailable`

for node pool upgrades


Best practice guidanceConfigure the

`maxUnavailable`

setting for node pool upgrades to ensure application availability during upgrade operations.

The `maxUnavailable`

setting specifies the maximum number of nodes that can be unavailable during an upgrade. This ensures that a portion of your node pool remains operational while nodes are being upgraded.

For example, the following Azure CLI command sets `maxUnavailable`

to 1 for a node pool:

```
az aks nodepool update \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name myNodePool \
--max-unavailable 1
```


By configuring `maxUnavailable`

, you can control the impact of upgrades on your workloads, ensuring that sufficient resources remain available during the process.

For more information, see [Upgrade node pools in AKS](upgrade-cluster).


Best practice guidanceUse Accelerated Networking to provide lower latency, reduced jitter, and decreased CPU utilization on your VMs.


Accelerated Networking enables [single root I/O virtualization (SR-IOV)](/en-us/windows-hardware/drivers/network/overview-of-single-root-i-o-virtualization--sr-iov-) on [supported VM types](/en-us/azure/virtual-network/accelerated-networking-overview#supported-vm-instances), greatly improving networking performance.

The following diagram illustrates how two VMs communicate with and without Accelerated Networking:


For more information, see [Accelerated Networking overview](/en-us/azure/virtual-network/accelerated-networking-overview).

### Image versions


Best practice guidanceImages shouldn't use the

`latest`

tag.

#### Container image tags

Using the `latest`

tag for [container images](https://kubernetes.io/docs/concepts/containers/images/) can lead to unpredictable behavior and makes it difficult to track which version of the image is running in your cluster. You can minimize these risks by integrating and running scan and remediation tools in your containers at build and runtime. For more information, see [Best practices for container image management in AKS](operator-best-practices-container-image-management).

#### Node image upgrades

AKS provides multiple auto-upgrade channels for node OS image upgrades. You can use these channels to control the timing of upgrades. We recommend joining these auto-upgrade channels to ensure that your nodes are running the latest security patches and updates. For more information, see [Auto-upgrade node OS images in AKS](auto-upgrade-node-os-image).

### Standard tier for production workloads


Best practice guidanceUse the Standard tier for product workloads for greater cluster reliability and resources, support for up to 5,000 nodes in a cluster, and Uptime SLA enabled by default. If you need LTS, consider using the Premium tier.


The Standard tier for Azure Kubernetes Service (AKS) provides a financially backed 99.9% uptime [service-level agreement (SLA)](https://www.azure.cn/en-us/support/sla/kubernetes-service/) for your production workloads. The standard tier also provides greater cluster reliability and resources, support for up to 5,000 nodes in a cluster, and Uptime SLA enabled by default. For more information, see [Pricing tiers for AKS cluster management](free-standard-pricing-tiers).

### Azure CNI for dynamic IP allocation


Best practice guidanceConfigure Azure CNI for dynamic IP allocation for better IP utilization and to prevent IP exhaustion for AKS clusters.


The dynamic IP allocation capability in Azure CNI allocates pod IPs from a subnet separate from the subnet hosting the AKS cluster and offers the following benefits:

**Better IP utilization**: IPs are dynamically allocated to cluster Pods from the Pod subnet. This leads to better utilization of IPs in the cluster compared to the traditional CNI solution, which does static allocation of IPs for every node.**Scalable and flexible**: Node and pod subnets can be scaled independently. A single pod subnet can be shared across multiple node pools of a cluster or across multiple AKS clusters deployed in the same VNet. You can also configure a separate pod subnet for a node pool.**High performance**: Since pod are assigned virtual network IPs, they have direct connectivity to other cluster pod and resources in the VNet. The solution supports very large clusters without any degradation in performance.**Separate VNet policies for pods**: Since pods have a separate subnet, you can configure separate VNet policies for them that are different from node policies. This enables many useful scenarios such as allowing internet connectivity only for pods and not for nodes, fixing the source IP for pod in a node pool using an Azure NAT Gateway, and using NSGs to filter traffic between node pools.**Kubernetes network policies**: Both the Azure Network Policies and Calico work with this solution.

For more information, see [Configure Azure CNI networking for dynamic allocation of IPs and enhanced subnet support](configure-azure-cni-dynamic-ip-allocation).

### v5 SKU VMs


Best practice guidanceUse v5 VM SKUs for improved performance during and after updates, less overall impact, and a more reliable connection for your applications.


For node pools in AKS, use v5 SKU VMs with ephemeral OS disks to provide sufficient compute resources for kube-system pods. For more information, see [Best practices for performance and scaling large workloads in AKS](best-practices-performance-scale-large).

### Do *not* use B series VMs


Best practice guidanceDon't use B series VMs for AKS clusters because they're low performance and don't work well with AKS.


B series VMs are low performance and don't work well with AKS. Instead, we recommend using [v5 SKU VMs](#v5-sku-vms).

### Premium Disks


Best practice guidanceUse Premium Disks to achieve 99.9% availability in one virtual machine (VM).


[Azure Premium Disks](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2) offer a consistent submillisecond disk latency and high IOPS and throughout. Premium Disks are designed to provide low-latency, high-performance, and consistent disk performance for VMs.

The following example YAML manifest shows a [storage class definition](https://kubernetes.io/docs/concepts/storage/storage-classes/) for a premium disk:

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


For more information, see [Use Azure Premium SSD v2 disks on AKS](use-premium-v2-disks).

### Container Insights


Best practice guidanceEnable Container Insights to monitor and diagnose the performance of your containerized applications.


[Container Insights](/en-us/azure/azure-monitor/containers/container-insights-overview) is a feature of Azure Monitor that collects and analyzes container logs from AKS. You can analyze the collected data with a collection of [views](/en-us/azure/azure-monitor/containers/container-insights-analyze) and prebuilt [workbooks](/en-us/azure/azure-monitor/containers/container-insights-reports).

You can enable Container Insights monitoring on your AKS cluster using various methods. The following example shows how to enable Container Insights monitoring on an existing cluster using the Azure CLI:

```
az aks enable-addons -a monitoring --name myAKSCluster --resource-group myResourceGroup
```


For more information, see [Enable monitoring for Kubernetes clusters](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable).

### Azure Policy


Best practice guidanceApply and enforce security and compliance requirements for your AKS clusters using Azure Policy.


You can apply and enforce built-in security policies on your AKS clusters using [Azure Policy](/en-us/azure/governance/policy/overview). Azure Policy helps enforce organizational standards and assess compliance at-scale. After you install the [Azure Policy add-on for AKS](/en-us/azure/governance/policy/concepts/policy-for-kubernetes), you can apply individual policy definitions or groups of policy definitions called initiatives to your clusters.

For more information, see [Secure your AKS clusters with Azure Policy](use-azure-policy).

## Next steps

This article focused on best practices for deployment and cluster reliability for Azure Kubernetes Service (AKS) clusters. For more best practices, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: how-to-configure-container-network-logs.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/how-to-configure-container-network-logs -->

# Set up container network logs with Advanced Container Networking Services (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Component renaming (starting November 11, 2025)

We are renaming components in the Container Network Logs feature to improve clarity and consistency:

What's changing

**CRD**:`RetinaNetworkFlowLogs`

→`ContainerNetworkLog`

**CLI flag**:`--enable-retinanetworkflowlog`

→`--enable-container-network-logs`

**Log Analytics table**:`RetinaNetworkFlowLogs`

→`ContainerNetworkLog`


Action items for existing users to enable new naming

**Update Azure CLI**(MUST - First step!):`az upgrade`

**Update Preview CLI Extension**(MUST):`az extension update --name aks-preview`

**Disable Monitoring**:`az aks disable-addons -a monitoring -n <cluster-name> -g <resource-group>`

**Re-enable Monitoring**:`az aks enable-addons -a monitoring --enable-high-log-scale-mode -g <resource-group> -n <cluster-name>`

**Re-enable ACNS Container Network Logs**:`az aks update --enable-acns --enable-container-network-logs -g <resource-group> -n <cluster-name>`

**Apply new ContainerNetworkLog CRD**: Apply your updated CRD configuration with the new naming.**Reimport Grafana Dashboards**: Import the updated dashboards to reflect the new table names.

Note

- Previously collected data stays in your workspace in old table RetinaNetworkFlowLogs.
- After re-enabling, allow a short delay before new data appears in new table ContainerNetworkLog.

In this article, you complete the steps to configure and use the container network logs feature in Advanced Container Networking Services for Azure Kubernetes Service (AKS). These logs offer persistent network flow monitoring tailored to enhance visibility in containerized environments.

By capturing container network logs, you can effectively track network traffic, detect anomalies, optimize performance, and ensure compliance with established policies. Follow the detailed instructions provided to set up and integrate container network logs for your system. For more information about the container network logs feature, see [Overview of container network logs](container-network-observability-logs).

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of the Azure CLI required to complete the steps in this article is 2.75.0. To find your version, run

`az --version`

in the Azure CLI. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).Container network logs in stored logs mode work only for Cilium data planes.

Container network logs in on-demand mode work for both Cilium and non-Cilium data planes.

If your existing cluster is version 1.33 or earlier, upgrade the cluster to the latest available Kubernetes version.

The minimum version of the

`aks-preview`

Azure CLI extension to complete the steps in this article is`19.0.07`

.

### Install the aks-preview Azure CLI extension

Install or update the Azure CLI preview extension by using the [ az extension add](/en-us/cli/azure/extension#az-extension-add) or

[command.](/en-us/cli/azure/extension#az-extension-update)

`az extension update`

```
# Install the aks-preview extension
az extension add --name aks-preview
# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```


### Register the AdvancedNetworkingFlowLogsPreview feature flag

First, register the AdvancedNetworkingFlowLogsPreview feature flag by using the [ az feature register](/en-us/cli/azure/feature#az-feature-register) command:

```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingFlowLogsPreview"
```


Verify successful registration by using the [ az feature show](/en-us/cli/azure/feature#az-feature-show) command. It takes a few minutes for registration to complete.

```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingFlowLogsPreview"
```


When the feature shows **Registered**, refresh the registration of the `Microsoft.ContainerService`

resource provider by using the [ az provider register](/en-us/cli/azure/provider#az-provider-register) command.

## Limitations

- Layer 7 flow data is captured only when Layer 7 policy support is enabled. For more information, see
[Configure a Layer 7 policy](how-to-apply-l7-policies). - Domain Name System (DNS) flows and related metrics are captured only when a Cilium Fully Qualified Domain (FQDN) network policy is applied. For more information, see
[Configure an FQDN policy](how-to-apply-fqdn-filtering-policies). - Onboarding by using Terraform isn't supported at this time.
- When Log Analytics isn't configured for log storage, container network logs are limited to a maximum of 50 MB of storage. When this limit is reached, new entries overwrite older logs.
- If the log table plan is set to Basic logs, the prebuilt Grafana dashboards don't function as expected.
- The Auxiliary logs table plan isn't supported.

## Configure stored logs mode for container network logs

### Deployment methods

You can onboard to container network logs using different deployment methods:

This section provides two paths for setting up container network logs based on your current situation:

: Complete setup for new AKS clusters[New clusters](#new-clusters): Enable container network logs on existing AKS clusters[Existing clusters](#existing-clusters)

## New clusters

This section guides you through setting up container network logs on a new AKS cluster from start to finish.

### Create a new AKS cluster with Advanced Container Networking Services

Use the `az aks create`

command with the `--enable-acns`

flag to create a new AKS cluster that has all Advanced Container Networking Services features. These features include:

**Container Network Observability:**Provides insight into your network traffic. To learn more, see[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more, see[Container Network Security](advanced-container-networking-services-overview#container-network-security).

```
# Set an environment variable for the AKS cluster name. Make sure you replace the placeholder with your own value.
export CLUSTER_NAME="<aks-cluster-name>"
export RESOURCE_GROUP="<aks-resource-group>"
export LOCATION="<location>"
# Create the resource group if it doesn't already exist
az group create --name $RESOURCE_GROUP --location $LOCATION
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--location $LOCATION \
--max-pods 250 \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--node-count 2 \
--pod-cidr 192.168.0.0/16 \
--kubernetes-version 1.33 or later \
--enable-acns
```


### Configure custom resources for log filtering

To configure container network logs in stored logs mode, you must define specific custom resources to set filters for log collection. When at least one custom resource is defined, logs are collected and stored on the host node at `/var/log/acns/hubble/events.log`

.

To configure logging, you must define and apply the `ContainerNetworkLog`

type of custom resource. You set filters like namespace, pod, service, port, protocol, and verdict. Multiple custom resources can exist in a cluster simultaneously. If no custom resource is defined with nonempty filters, no logs are saved in the designated location.

The following sample definition demonstrates how to configure the `ContainerNetworkLog`

type of custom resource.

### ContainerNetworkLog CRD template

```
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkLog
metadata:
name: sample-containernetworklog # Cluster scoped
spec:
includefilters: # List of filters
- name: sample-filter # Filter name
from:
namespacedPod: # List of source namespace/pods. Prepend namespace with /
- sample-namespace/sample-pod
labelSelector: # Standard k8s label selector
matchLabels:
app: frontend
k8s.io/namespace: sample-namespace
matchExpressions:
- key: environment
operator: In
values:
- production
- staging
ip: # List of source IPs; can be CIDR
- "192.168.1.10"
- "10.0.0.1"
to:
namespacedPod:
- sample-namespace2/sample-pod2
labelSelector:
matchLabels:
app: backend
k8s.io/namespace: sample-namespace2
matchExpressions:
- key: tier
operator: NotIn
values:
- dev
ip:
- "192.168.1.20"
- "10.0.1.1"
protocol: # List of protocols; can be tcp, udp, dns
- tcp
- udp
- dns
verdict: # List of verdicts; can be forwarded, dropped
- forwarded
- dropped
```


The following table describes the fields in the custom resource definition:

| Field | Type | Description | Required |
|---|---|---|---|
`includefilters` |
[]filter | A list of filters that define network flows to include. Each filter specifies the source, destination, protocol, and other matching criteria. Include filters can't be empty and must have at least one filter. | Mandatory |
`filters.name` |
String | The name of the filter. | Optional |
`filters.protocol` |
[]string | The protocols to match for this filter. Valid values are `tcp` , `udp` , and `dns` . This parameter is optional. If not specified, logs with all protocols are included. |
Optional |
`filters.verdict` |
[]string | The verdict of the flow to match. Valid values are `forwarded` and `dropped` . This parameter is optional. If not specified, logs with all verdicts are included. |
Optional |
`filters.from` |
Endpoint | Specifies the source of the network flow. Can include IP addresses, label selectors, and namespace/pod pairs. | Optional |
`Endpoint.ip` |
[]string | It can be a single IP or a CIDR. | Optional |
`Endpoint.labelSelector` |
Object | A label selector is a mechanism to filter and query resources based on labels, so you can identify specific subsets of resources. A label selector can include two components: `matchLabels` and `matchExpressions` . Use `matchLabels` for straightforward matching by specifying a key/value pair (for example, `{"app": "frontend"}` ). For more advanced criteria, use `matchExpressions` , where you define a label key, an operator (such as `In` , `NotIn` , `Exists` , or `DoesNotExist` ), and an optional list of values. Ensure that the conditions in both `matchLabels` and `matchExpressions` are met, because they're logically combined by `AND` . If no conditions are specified, the selector matches all resources. To match none, leave the selector null. Carefully define your label selector to target the correct set of resources. |
Optional |
`Endpoint.namespacedPod` |
[]string | A list of namespace and pod pairs (formatted as `namespace/pod` ) for matching the source. `name` should match the RegEx pattern `^.+$` . |
Optional |
`filters.to` |
Endpoint | Specifies the destination of the network flow. Can include IP addresses, label selectors, or namespace/pod pairs. | Optional |
`Endpoint.ip` |
[]string | It can be a single IP or a CIDR. | Optional |
`Endpoint.labelSelector` |
Object | A label selector to match resources based on their labels. | Optional |
`Endpoint.namespacedPod` |
[]string | A list of namespace and pod pairs (formatted as `namespace/pod` ) to match the destination. |
Optional |

Apply the

`ContainerNetworkLog`

custom resource to enable log collection at the cluster:`kubectl apply -f <crd.yaml>`

Tip

For a practical example of a ContainerNetworkLog custom resource configuration, see the

[sample CRD in the AKS Labs documentation](https://azure-samples.github.io/aks-labs/docs/networking/acns-lab/#enable-flow-logs-for-the-pets-namespace).

Logs stored locally on host nodes are temporary because the host or node itself isn't a persistent storage solution. Logs on host nodes are also rotated when their size reaches 50 MB. For longer-term storage and analysis, we recommend that you configure the Azure Monitor Agent on the cluster to collect and retain logs in the Log Analytics workspace.

Alternatively, you can integrate a partner logging service like an OpenTelemetry collector for more log management options.

### Configure Azure Monitor for managed storage (recommended)

For persistent storage and advanced analytics, configure the Azure Monitor Agent to collect and store logs in a Log Analytics workspace:

```
# Set an environment variable for the AKS cluster name. Make sure you replace the placeholder with your own value.
export CLUSTER_NAME="<aks-cluster-name>"
export RESOURCE_GROUP="<aks-resource-group>"
# Enable azure monitor with high log scale mode
### To use the default Log Analytics workspace
az aks enable-addons -a monitoring --enable-high-log-scale-mode -g $RESOURCE_GROUP -n $CLUSTER_NAME
### To use an existing Log Analytics workspace
az aks enable-addons -a monitoring --enable-high-log-scale-mode -g $RESOURCE_GROUP -n $CLUSTER_NAME --workspace-resource-id <workspace-resource-id>
# Update the AKS cluster with the enable-container-network-logs flag
az aks update --enable-acns \
--enable-container-network-logs \
-g $RESOURCE_GROUP \
-n $CLUSTER_NAME
```


Note

When enabled, container network flow logs are written to `/var/log/acns/hubble/events.log`

when the `ContainerNetworkLog`

custom resource is applied. If Log Analytics integration is enabled later, the Azure Monitor Agent begins collecting logs at that point. Logs older than two minutes aren't ingested. Only new entries that are appended after monitoring begins are collected in a Log Analytics workspace.

## Existing clusters

Note

If your cluster already has Advanced Container Networking Services (ACNS) enabled, you can start collecting flow logs on the host node by simply applying a ContainerNetworkLog CRD. However, if you want to enable flow logs with Log Analytics workspace integration for persistent storage and advanced analytics, follow the steps in the [Configure integration with log analytics on existing cluster](#configure-integration-with-log-analytics-on-existing-cluster) section.

```
# Set environment variables for your existing cluster. Make sure you replace the placeholders with your own values.
export CLUSTER_NAME="<aks-cluster-name>"
export RESOURCE_GROUP="<aks-resource-group>"
```


### Configure integration with log analytics on existing cluster

To enable container network logs on an existing cluster:

Check whether monitoring add-ons are already enabled on that cluster:

`az aks addon list -g $RESOURCE_GROUP -n $CLUSTER_NAME`

If monitoring add-ons are enabled, disable monitoring add-ons:

`az aks disable-addons -a monitoring -g $RESOURCE_GROUP -n $CLUSTER_NAME`

Complete this step because monitoring add-ons might already be enabled, but not for high scale. For more information, see

[High-scale mode](/en-us/azure/azure-monitor/containers/container-insights-high-scale).Set Azure Monitor to

`enable-high-log-scale-mode`

:`### Use default Log Analytics workspace az aks enable-addons -a monitoring --enable-high-log-scale-mode -g $RESOURCE_GROUP -n $CLUSTER_NAME ### Use existing Log Analytics workspace az aks enable-addons -a monitoring --enable-high-log-scale-mode -g $RESOURCE_GROUP -n $CLUSTER_NAME --workspace-resource-id <workspace-resource-id>`

Update the AKS cluster with the

`enable-container-network-logs`

flag:`az aks update --enable-acns \ --enable-container-network-logs \ -g $RESOURCE_GROUP \ -n $CLUSTER_NAME`

Create the CRD as per the

[ContainerNetworkLog template](#containernetworklog-crd-template)mentioned above and apply it to start log collection in log analytics workspace.Tip

For a practical example of a ContainerNetworkLog custom resource configuration, see the

[sample CRD in the AKS Labs documentation](https://azure-samples.github.io/aks-labs/docs/networking/acns-lab/#enable-flow-logs-for-the-pets-namespace).

**Viewing L7 flows and DNS errors**

To capture Layer 7 (L7) flow data and DNS errors/flows in your container network logs, you must apply Cilium network policies with FQDN filtering and L7 policy support enabled. Without these policies, L7 and DNS-related flow information won't be captured.

Example of a Cilium network policy with FQDN filtering and L7 support:

```
apiVersion: cilium.io/v2
kind: CiliumNetworkPolicy
metadata:
name: l7-dns-policy
namespace: default
spec:
endpointSelector:
matchLabels:
app: myapp
egress:
- toEndpoints:
- matchLabels:
"k8s:io.kubernetes.pod.namespace": kube-system
"k8s:k8s-app": kube-dns
toPorts:
- ports:
- port: "53"
protocol: UDP
rules:
dns:
- matchPattern: "*.example.com"
- toFQDNs:
- matchPattern: "*.example.com"
toPorts:
- ports:
- port: "443"
protocol: TCP
rules:
http:
- method: "GET"
path: "/1"
```


Apply the policy using:

```
kubectl apply -f l7-dns-policy.yaml
```


For more information, see [Configure a Layer 7 policy](how-to-apply-l7-policies) and [Configure an FQDN policy](how-to-apply-fqdn-filtering-policies)

## Common post-setup steps to verify configuration

The following steps apply to both new and existing cluster setups.

### Get cluster credentials

Get your cluster credentials by using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command:

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


### Validate the setup

Validate that the retina network flow log capability is enabled:

```
az aks show -g $RESOURCE_GROUP -n $CLUSTER_NAME
```


Expected output:

```
"networkProfile":{
"advancedNetworking": {
"enabled": true,
"observability":{
"enabled": true
}
}
}
----------------------------
"osmagent":{
"config":{
"enableContainerNetworkLogs": "True"
}
}
```


Check which custom resource definitions are installed for flow logs:

```
kubectl get containernetworklog
```


This command lists all the `ContainerNetworkLog`

custom resources created in the cluster.

Validate that the `ContainerNetworkLog`

custom resource is applied:

```
k describe containernetworklog <cr-name>
```


Expect to see a `Spec`

node that contains `Include filters`

and a `Status`

node. The value for `Status`

> `State`

should be `CONFIGURED`

(not `FAILED`

).

```
Spec:
Includefilters:
From:
Namespaced Pod:
namespace/pod-
Name: sample-filter
Protocol:
tcp
To:
Namespaced Pod:
namespace/pod-
Verdict:
dropped
Status:
State: CONFIGURED
Timestamp: 2025-05-01T11:24:48Z
```


Users can apply multiple `ContainerNetworkLog`

custom resources in the cluster. Each custom resource has its own status.

### Querying Container Network Flow Logs in Log Analytics dashboard

When Container Network Flow Logs are enabled with a Log Analytics workspace, you have access to historical logs that allow you to analyze network traffic patterns over time. You can query these logs using the `ContainerNetworkLog`

table to perform detailed forensic analysis and troubleshooting.

Customers can use Kusto Query Language (KQL) to analyze network data in Log Analytics. This historical data is invaluable for understanding network behavior patterns, identifying security incidents, troubleshooting connectivity issues, and performing root cause analysis over extended periods. The ability to correlate network events across time helps detect intermittent issues and understand traffic flows that may not be apparent in real-time monitoring.

To see sample queries that can be applied for troubleshooting connectivity issues, refer to the [progressive diagnosis using flow logs](https://azure-samples.github.io/aks-labs/docs/networking/acns-lab/#progressive-diagnosis-using-flow-logs) in the AKS Labs documentation.

### Azure Managed Grafana

You can access prebuilt Grafana dashboards through the Azure portal. Navigate to either the Azure Monitor resource or your Azure Kubernetes Service (AKS) cluster to view and interact with these dashboards. But before that:

Make sure that the Azure logs pods are running:

`kubectl get pods -o wide -n kube-system | grep ama-logs`

Your output should look similar to the following example:

`ama-logs-9bxc6 3/3 Running 1 (39m ago) 44m ama-logs-fd568 3/3 Running 1 (40m ago) 44m ama-logs-rs-65bdd98f75-hqnd2 2/2 Running 1 (43m ago) 22h`

Ensure that your Managed Grafana workspace can access and search all monitoring data in the relevant subscription. This step is required to access prebuilt dashboards for network flow logs.

**Use case 1**: If you're a subscription Owner or a User Access Administrator, when a Managed Grafana workspace is created, it comes with the Monitoring Reader role granted on all Azure Monitor data and Log Analytics resources in the subscription. The new Managed Grafana workspace can access and search all monitoring data in the subscription. It can view the Azure Monitor metrics and logs from all resources and view any logs stored in Log Analytics workspaces in the subscription.**Use case 2**: If you're not a subscription Owner or User Access Administrator, or if your Log Analytics and Managed Grafana workspaces are in different subscriptions, Grafana can't access Log Analytics and the subscription. The Grafana workspace must have the Monitoring Reader role in the relevant subscription to access prebuilt Grafana dashboards. In this scenario, complete these steps to provide access:In your Managed Grafana workspace, go to

**Settings**>**Identity**.Select

**Azure role assignments**>**Add role assignments**.For

**Scope**, enter**Subscription**. Select your subscription. Set**Role**to**Monitoring Reader**, and then select**Save**.Verify the data source for the Managed Grafana instance. To verify the subscription for the data source for the Grafana dashboards, check the

**Data source**tab in the Managed Grafana instance:


#### Visualization in Grafana dashboards

Azure Monitor dashboards with Grafana enable you to use Grafana's query, transformation, and visualization capabilities on metrics and logs collected in Azure Monitor. You can use this option as an alternative to visualize container network flow logs.

- Navigate to the left pane of the Kubernetes cluster in the Azure portal.
- Select
**Dashboards with Grafana (Preview)**. - Browse the list of available dashboards in the Azure Monitor or Azure Managed Prometheus listings.
- Select a dashboard, for example
**Azure | Insights | Containers | Networking | Flow Logs**.

You can visualize container network flow logs for analysis by using two prebuilt Grafana dashboards. You can access the dashboards either through Azure Managed Grafana or in the Azure portal.

To simplify log analysis, we provide two preconfigured Azure Managed Grafana dashboards:

Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs**. This dashboard provides visualizations in which AKS workloads communicate with each other, including network requests, responses, drops, and errors. Currently, you must use[ID 23155](https://grafana.com/grafana/dashboards/23155-azure-insights-containers-networking-flow-logs//)to import these dashboards.Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs (External Traffic)**. This dashboard provides visualizations in which AKS workloads send and receive communications from outside an AKS cluster, including network requests, responses, drops, and errors. Use[ID 23156](https://grafana.com/grafana/dashboards/23156-azure-insights-containers-networking-flow-logs-external-traffic//).

For more information about how to use this dashboard, see the [overview of container network logs](container-network-observability-logs).

## Configure on-demand logs mode

On-demand logs mode for network flows works with both Cilium and non-Cilium data planes.

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. The features include:

**Container Network Observability:**Provides insights into your network traffic. To learn more, visit[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more, visit[Container Network Security](advanced-container-networking-services-overview#container-network-security).

Note

Clusters that have the Cilium data plane support the Container Network Observability and Container Network Security features in Kubernetes version 1.29 and later.

```
# Set an environment variable for the AKS cluster name. Make sure you replace the placeholder with your own value.
export CLUSTER_NAME="<aks-cluster-name>"
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--location eastus \
--max-pods 250 \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--node-count 2 \
--pod-cidr 192.168.0.0/16 \
--kubernetes-version 1.33 \
--enable-acns
```


### Enable Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--enable-acns`

flag updates an existing AKS cluster with all Advanced Container Networking Services features. The features include [Container Network Observability](advanced-container-networking-services-overview#container-network-observability)and

[Container Network Security](advanced-container-networking-services-overview#container-network-security).

Note

Only clusters that have the Cilium data plane support the Container Network Security features of Advanced Container Networking Services.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns
```


Next, get your cluster credentials by using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command:

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


### Install the Hubble CLI

Install the Hubble CLI to access the data it collects. Run the following commands:

```
# Set environment variables
export HUBBLE_VERSION=v1.16.3
export HUBBLE_ARCH=amd64
#Install the Hubble CLI
if [ "$(uname -m)" = "aarch64" ]; then HUBBLE_ARCH=arm64; fi
curl -L --fail --remote-name-all https://github.com/cilium/hubble/releases/download/$HUBBLE_VERSION/hubble-linux-${HUBBLE_ARCH}.tar.gz{,.sha256sum}
sha256sum --check hubble-linux-${HUBBLE_ARCH}.tar.gz.sha256sum
sudo tar xzvfC hubble-linux-${HUBBLE_ARCH}.tar.gz /usr/local/bin
rm hubble-linux-${HUBBLE_ARCH}.tar.gz{,.sha256sum}
```


### Visualize the Hubble flows

Make sure that the Hubble pods are running:

`kubectl get pods -o wide -n kube-system -l k8s-app=hubble-relay`

Your output should look similar to the following example:

`hubble-relay-7ddd887cdb-h6khj 1/1 Running 0 23h`

Port-forward the Hubble Relay server:

`kubectl port-forward -n kube-system svc/hubble-relay --address 127.0.0.1 4245:443`

Mutual TLS (mTLS) ensures the security of the Hubble Relay server. To enable the Hubble client to retrieve flows, you must get the appropriate certificates and configure the client with them. Apply the certificates by using the following commands:

`#!/usr/bin/env bash set -euo pipefail set -x # Directory where certificates will be stored CERT_DIR="$(pwd)/.certs" mkdir -p "$CERT_DIR" declare -A CERT_FILES=( ["tls.crt"]="tls-client-cert-file" ["tls.key"]="tls-client-key-file" ["ca.crt"]="tls-ca-cert-files" ) for FILE in "${!CERT_FILES[@]}"; do KEY="${CERT_FILES[$FILE]}" JSONPATH="{.data['${FILE//./\\.}']}" # Retrieve the secret and decode it kubectl get secret hubble-relay-client-certs -n kube-system \ -o jsonpath="${JSONPATH}" | \ base64 -d > "$CERT_DIR/$FILE" # Set the appropriate hubble CLI config hubble config set "$KEY" "$CERT_DIR/$FILE" done hubble config set tls true hubble config set tls-server-name instance.hubble-relay.cilium.io`

Confirm that the secrets were generated:

`kubectl get secrets -n kube-system | grep hubble-`

Your output should look similar to the following example:

`kube-system hubble-relay-client-certs kubernetes.io/tls 3 9d kube-system hubble-relay-server-certs kubernetes.io/tls 3 9d kube-system hubble-server-certs kubernetes.io/tls 3 9d`

Verify that the Hubble Relay pod is running:

`hubble observe --pod hubble-relay-7ddd887cdb-h6khj`


### Visualize by using the Hubble UI

To use the Hubble UI, save the following script in the

`hubble-ui.yaml`

file:`apiVersion: v1 kind: ServiceAccount metadata: name: hubble-ui namespace: kube-system --- kind: ClusterRole apiVersion: rbac.authorization.k8s.io/v1 metadata: name: hubble-ui labels: app.kubernetes.io/part-of: retina rules: - apiGroups: - networking.k8s.io resources: - networkpolicies verbs: - get - list - watch - apiGroups: - "" resources: - componentstatuses - endpoints - namespaces - nodes - pods - services verbs: - get - list - watch - apiGroups: - apiextensions.k8s.io resources: - customresourcedefinitions verbs: - get - list - watch - apiGroups: - cilium.io resources: - "*" verbs: - get - list - watch --- apiVersion: rbac.authorization.k8s.io/v1 kind: ClusterRoleBinding metadata: name: hubble-ui labels: app.kubernetes.io/part-of: retina roleRef: apiGroup: rbac.authorization.k8s.io kind: ClusterRole name: hubble-ui subjects: - kind: ServiceAccount name: hubble-ui namespace: kube-system --- apiVersion: v1 kind: ConfigMap metadata: name: hubble-ui-nginx namespace: kube-system data: nginx.conf: | server { listen 8081; server_name localhost; root /app; index index.html; client_max_body_size 1G; location / { proxy_set_header Host $host; proxy_set_header X-Real-IP $remote_addr; # CORS add_header Access-Control-Allow-Methods "GET, POST, PUT, HEAD, DELETE, OPTIONS"; add_header Access-Control-Allow-Origin *; add_header Access-Control-Max-Age 1728000; add_header Access-Control-Expose-Headers content-length,grpc-status,grpc-message; add_header Access-Control-Allow-Headers range,keep-alive,user-agent,cache-control,content-type,content-transfer-encoding,x-accept-content-transfer-encoding,x-accept-response-streaming,x-user-agent,x-grpc-web,grpc-timeout; if ($request_method = OPTIONS) { return 204; } # /CORS location /api { proxy_http_version 1.1; proxy_pass_request_headers on; proxy_hide_header Access-Control-Allow-Origin; proxy_pass http://127.0.0.1:8090; } location / { try_files $uri $uri/ /index.html /index.html; } # Liveness probe location /healthz { access_log off; add_header Content-Type text/plain; return 200 'ok'; } } } --- kind: Deployment apiVersion: apps/v1 metadata: name: hubble-ui namespace: kube-system labels: k8s-app: hubble-ui app.kubernetes.io/name: hubble-ui app.kubernetes.io/part-of: retina spec: replicas: 1 selector: matchLabels: k8s-app: hubble-ui template: metadata: labels: k8s-app: hubble-ui app.kubernetes.io/name: hubble-ui app.kubernetes.io/part-of: retina spec: serviceAccountName: hubble-ui automountServiceAccountToken: true containers: - name: frontend image: mcr.microsoft.com/oss/cilium/hubble-ui:v0.12.2 imagePullPolicy: Always ports: - name: http containerPort: 8081 livenessProbe: httpGet: path: /healthz port: 8081 readinessProbe: httpGet: path: / port: 8081 resources: {} volumeMounts: - name: hubble-ui-nginx-conf mountPath: /etc/nginx/conf.d/default.conf subPath: nginx.conf - name: tmp-dir mountPath: /tmp terminationMessagePolicy: FallbackToLogsOnError securityContext: {} - name: backend image: mcr.microsoft.com/oss/cilium/hubble-ui-backend:v0.12.2 imagePullPolicy: Always env: - name: EVENTS_SERVER_PORT value: "8090" - name: FLOWS_API_ADDR value: "hubble-relay:443" - name: TLS_TO_RELAY_ENABLED value: "true" - name: TLS_RELAY_SERVER_NAME value: ui.hubble-relay.cilium.io - name: TLS_RELAY_CA_CERT_FILES value: /var/lib/hubble-ui/certs/hubble-relay-ca.crt - name: TLS_RELAY_CLIENT_CERT_FILE value: /var/lib/hubble-ui/certs/client.crt - name: TLS_RELAY_CLIENT_KEY_FILE value: /var/lib/hubble-ui/certs/client.key livenessProbe: httpGet: path: /healthz port: 8090 readinessProbe: httpGet: path: /healthz port: 8090 ports: - name: grpc containerPort: 8090 resources: {} volumeMounts: - name: hubble-ui-client-certs mountPath: /var/lib/hubble-ui/certs readOnly: true terminationMessagePolicy: FallbackToLogsOnError securityContext: {} nodeSelector: kubernetes.io/os: linux volumes: - configMap: defaultMode: 420 name: hubble-ui-nginx name: hubble-ui-nginx-conf - emptyDir: {} name: tmp-dir - name: hubble-ui-client-certs projected: defaultMode: 0400 sources: - secret: name: hubble-relay-client-certs items: - key: tls.crt path: client.crt - key: tls.key path: client.key - key: ca.crt path: hubble-relay-ca.crt --- kind: Service apiVersion: v1 metadata: name: hubble-ui namespace: kube-system labels: k8s-app: hubble-ui app.kubernetes.io/name: hubble-ui app.kubernetes.io/part-of: retina spec: type: ClusterIP selector: k8s-app: hubble-ui ports: - name: http port: 80 targetPort: 8081`

Apply the

`hubble-ui.yaml`

manifest to your cluster:`kubectl apply -f hubble-ui.yaml`

Set up port forwarding for the Hubble UI:

`kubectl -n kube-system port-forward svc/hubble-ui 12000:80`

In your web browser, enter

`http://localhost:12000/`

to access the Hubble UI.

### Basic troubleshooting

Advanced Container Networking Services is a prerequisite to turn on the Azure Monitor Agent log collection feature.

Trying to enable the container network flow logs capability on a cluster without enabling Advanced Container Networking Services, for example:

`az aks update -g test-rg -n test-cluster --enable-container-network-logs`

Results in an error message:

`Flow logs requires '--enable-acns', advanced networking to be enabled, and the monitoring addon to be enabled.`

If the cluster Kubernetes version is earlier than version 1.33.0, trying to run

`--enable-container-network-logs`

results in an error message:`The specified orchestrator version %s is not valid. Advanced Networking Flow Logs is only supported on Kubernetes version 1.33.0 or later.`

where

`%s`

is your Kubernetes version.If you try to run

`--enable-container-network-logs`

on a subscription where the Azure Feature Exposure Control (AFEC) flag isn't enabled, an error message appears:`Feature Microsoft.ContainerService/AdvancedNetworkingFlowLogsPreview is not enabled. Please see https://aka.ms/aks/previews for how to enable features.`

If you try to apply a

`ContainerNetworkLog`

custom resource on a cluster where Advanced Container Networking Services isn't enabled, an error message appears:`error: resource mapping not found for <....>": no matches for kind "ContainerNetworkLog" in version "acn.azure.com/v1alpha1"`

Ensure that you install custom resources first.


### Disable container network logs: Stored logs mode on existing cluster

If all custom resources are deleted, flow log collection stops because no filters are defined for collection.

To disable container network log collection by the Azure Monitor Agent, run:

```
az aks update -n $CLUSTER_NAME -g $RESOURCE_GROUP --disable-container-network-logs
```


## Clean up resources

If you don't plan to use this example application, delete the resources you created in this article by using the [ az group delete](/en-us/cli/azure/#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP
```


## Related content

- Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services.
