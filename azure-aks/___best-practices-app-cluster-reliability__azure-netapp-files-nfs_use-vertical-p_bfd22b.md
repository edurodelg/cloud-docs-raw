---
merged_at: 2026-01-29T15:23:36.562542
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices-app-cluster-reliability -->

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

Starting on **September 30, 2025**, Azure Kubernetes Service (AKS) no longer supports Basic Load Balancer. To avoid any potential service disruptions, we recommend using Standard Load Balancer for new deployments and [upgrading any existing deployments to the Standard Load Balancer](/en-us/azure/load-balancer/load-balancer-basic-upgrade-guidance). For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/5020) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates/azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer/). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-netapp-files-nfs -->

# Provision Azure NetApp Files NFS volumes for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

After you [configure Azure NetApp Files for Azure Kubernetes Service](azure-netapp-files), you can provision Azure NetApp Files volumes for Azure Kubernetes Service.

Azure NetApp Files supports volumes using NFS (NFSv3 or NFSv4.1), [SMB](azure-netapp-files-smb), or [dual-protocol](azure-netapp-files-dual-protocol) (NFSv3 and SMB, or NFSv4.1 and SMB).

- This article describes details for provisioning NFS volumes statically or dynamically.
- For information about provisioning SMB volumes statically or dynamically, see
[Provision Azure NetApp Files SMB volumes for Azure Kubernetes Service](azure-netapp-files-smb). - For information about provisioning dual-protocol volumes statically, see
[Provision Azure NetApp Files dual-protocol volumes for Azure Kubernetes Service](azure-netapp-files-dual-protocol)

## Statically configure for applications that use NFS volumes

This section describes how to create an NFS volume on Azure NetApp Files and expose the volume statically to Kubernetes. It also describes how to use the volume with a containerized application.

### Create an NFS volume

Define variables for later usage. Replace

*myresourcegroup*,*mylocation*,*myaccountname*,*mypool1*,*premium*,*myfilepath*,*myvolsize*,*myvolname*,*vnetid*, and*anfSubnetID*with an appropriate value from your account and environment. The*filepath*must be unique within all ANF accounts.`RESOURCE_GROUP="myresourcegroup" LOCATION="mylocation" ANF_ACCOUNT_NAME="myaccountname" POOL_NAME="mypool1" SERVICE_LEVEL="premium" # Valid values are Standard, Premium, and Ultra UNIQUE_FILE_PATH="myfilepath" VOLUME_SIZE_GIB="myvolsize" VOLUME_NAME="myvolname" VNET_ID="vnetId" SUBNET_ID="anfSubnetId"`

Create a volume using the

command. For more information, see`az netappfiles volume create`

[Create an NFS volume for Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-create-volumes).`az netappfiles volume create \ --resource-group $RESOURCE_GROUP \ --location $LOCATION \ --account-name $ANF_ACCOUNT_NAME \ --pool-name $POOL_NAME \ --name "$VOLUME_NAME" \ --service-level $SERVICE_LEVEL \ --vnet $VNET_ID \ --subnet $SUBNET_ID \ --usage-threshold $VOLUME_SIZE_GIB \ --file-path $UNIQUE_FILE_PATH \ --protocol-types NFSv3`


### Create the persistent volume

List the details of your volume using

command. Replace the variables with appropriate values from your Azure NetApp Files account and environment if not defined in a previous step.`az netappfiles volume show`

`az netappfiles volume show \ --resource-group $RESOURCE_GROUP \ --account-name $ANF_ACCOUNT_NAME \ --pool-name $POOL_NAME \ --volume-name "$VOLUME_NAME -o JSON`

The following output is an example of the above command executed with real values.

`{ ... "creationToken": "myfilepath2", ... "mountTargets": [ { ... "ipAddress": "10.0.0.4", ... } ], ... }`

Create a file named

`pv-nfs.yaml`

and copy in the following YAML. Make sure the server matches the output IP address from Step 1, and the path matches the output from`creationToken`

above. The capacity must also match the volume size from the step above.`apiVersion: v1 kind: PersistentVolume metadata: name: pv-nfs spec: capacity: storage: 100Gi accessModes: - ReadWriteMany mountOptions: - vers=3 nfs: server: 10.0.0.4 path: /myfilepath2`

Create the persistent volume using the

command:`kubectl apply`

`kubectl apply -f pv-nfs.yaml`

Verify the status of the persistent volume is

*Available*by using thecommand:`kubectl describe`

`kubectl describe pv pv-nfs`


### Create a persistent volume claim

Create a file named

`pvc-nfs.yaml`

and copy in the following YAML. This manifest creates a PVC named`pvc-nfs`

for 100Gi storage and`ReadWriteMany`

access mode, matching the PV you created.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: pvc-nfs spec: accessModes: - ReadWriteMany storageClassName: "" resources: requests: storage: 100Gi`

Create the persistent volume claim using the

command:`kubectl apply`

`kubectl apply -f pvc-nfs.yaml`

Verify the

*Status*of the persistent volume claim is*Bound*by using thecommand:`kubectl describe`

`kubectl describe pvc pvc-nfs`


### Mount with a pod

Create a file named

`nginx-nfs.yaml`

and copy in the following YAML. This manifest defines a`nginx`

pod that uses the persistent volume claim.`kind: Pod apiVersion: v1 metadata: name: nginx-nfs spec: containers: - image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine name: nginx-nfs command: - "/bin/sh" - "-c" - while true; do echo $(date) >> /mnt/azure/outfile; sleep 1; done volumeMounts: - name: disk01 mountPath: /mnt/azure volumes: - name: disk01 persistentVolumeClaim: claimName: pvc-nfs`

Create the pod using the

command:`kubectl apply`

`kubectl apply -f nginx-nfs.yaml`

Verify the pod is

*Running*by using thecommand:`kubectl describe`

`kubectl describe pod nginx-nfs`

Verify your volume has been mounted on the pod by using

to connect to the pod, and then use`kubectl exec`

`df -h`

to check if the volume is mounted.`kubectl exec -it nginx-nfs -- sh`

`/ # df -h Filesystem Size Used Avail Use% Mounted on ... 10.0.0.4:/myfilepath2 100T 384K 100T 1% /mnt/azure ...`


## Dynamically configure for applications that use NFS volumes

Trident may be used to dynamically provision NFS or SMB files on Azure NetApp Files. Dynamically provisioned SMB volumes are only supported with windows worker nodes.

This section describes how to use Trident to dynamically create an NFS volume on Azure NetApp Files and automatically mount it to a containerized application.

### Install Trident

To dynamically provision NFS volumes, you need to install Trident. Trident is NetApp's dynamic storage provisioner that is purpose-built for Kubernetes. Simplify the consumption of storage for Kubernetes applications using Trident's industry-standard [Container Storage Interface (CSI)](https://kubernetes-csi.github.io/docs/) driver. Trident deploys on Kubernetes clusters as pods and provides dynamic storage orchestration services for your Kubernetes workloads.

Trident can be installed using the Trident operator (manually or using [Helm](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy-operator.html)) or [ tridentctl](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy-tridentctl.html). To learn more about these installation methods and how they work, see the

[Trident Install Guide](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy.html).

#### Install Trident using Helm

[Helm](https://helm.sh/) must be installed on your workstation to install Trident using this method. For other methods of installing Trident, see the [Trident Install Guide](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy.html).

To install Trident using Helm for a cluster with only Linux worker nodes, run the following commands:

`helm repo add netapp-trident https://netapp.github.io/trident-helm-chart helm install trident netapp-trident/trident-operator --version 23.04.0 --create-namespace --namespace trident`

The output of the command resembles the following example:

`NAME: trident LAST DEPLOYED: Fri May 5 13:55:36 2023 NAMESPACE: trident STATUS: deployed REVISION: 1 TEST SUITE: None NOTES: Thank you for installing trident-operator, which will deploy and manage NetApp's Trident CSI storage provisioner for Kubernetes. Your release is named 'trident' and is installed into the 'trident' namespace. Please note that there must be only one instance of Trident (and trident-operator) in a Kubernetes cluster. To configure Trident to manage storage resources, you will need a copy of tridentctl, which is available in pre-packaged Trident releases. You may find all Trident releases and source code online at https://github.com/NetApp/trident. To learn more about the release, try: $ helm status trident $ helm get all trident`

To confirm Trident was installed successfully, run the following

command:`kubectl describe`

`kubectl describe torc trident`

The output of the command resembles the following example:

`Name: trident Namespace: Labels: app.kubernetes.io/managed-by=Helm Annotations: meta.helm.sh/release-name: trident meta.helm.sh/release-namespace: trident API Version: trident.netapp.io/v1 Kind: TridentOrchestrator Metadata: ... Spec: IPv6: false Autosupport Image: docker.io/netapp/trident-autosupport:23.04 Autosupport Proxy: <nil> Disable Audit Log: true Enable Force Detach: false Http Request Timeout: 90s Image Pull Policy: IfNotPresent k8sTimeout: 0 Kubelet Dir: <nil> Log Format: text Log Layers: <nil> Log Workflows: <nil> Namespace: trident Probe Port: 17546 Silence Autosupport: false Trident Image: docker.io/netapp/trident:23.04.0 Windows: false Status: Current Installation Params: IPv6: false Autosupport Hostname: Autosupport Image: docker.io/netapp/trident-autosupport:23.04 Autosupport Proxy: Autosupport Serial Number: Debug: false Disable Audit Log: true Enable Force Detach: false Http Request Timeout: 90s Image Pull Policy: IfNotPresent Image Pull Secrets: Image Registry: k8sTimeout: 30 Kubelet Dir: /var/lib/kubelet Log Format: text Log Layers: Log Level: info Log Workflows: Probe Port: 17546 Silence Autosupport: false Trident Image: docker.io/netapp/trident:23.04.0 Message: Trident installed Namespace: trident Status: Installed Version: v23.04.0 Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal Installing 2m59s trident-operator.netapp.io Installing Trident Normal Installed 2m31s trident-operator.netapp.io Trident installed`


### Create a backend

To instruct Trident about the Azure NetApp Files subscription and where it needs to create volumes, a backend is created. This step requires details about the account that was created in a previous step.

Create a file named

`backend-secret.yaml`

and copy in the following YAML. Change the`Client ID`

and`clientSecret`

to the correct values for your environment.`apiVersion: v1 kind: Secret metadata: name: backend-tbc-anf-secret type: Opaque stringData: clientID: 00001111-aaaa-2222-bbbb-3333cccc4444 clientSecret: rR0rUmWXfNioN1KhtHisiSAnoTherboGuskey6pU`

Create a file named

`backend-anf.yaml`

and copy in the following YAML. Change the`subscriptionID`

,`tenantID`

,`location`

, and`serviceLevel`

to the correct values for your environment. Use the`subscriptionID`

for the Azure subscription where Azure NetApp Files is enabled. Obtain the`tenantID`

,`clientID`

, and`clientSecret`

from an[application registration](/en-us/azure/active-directory/develop/howto-create-service-principal-portal)in Microsoft Entra ID with sufficient permissions for the Azure NetApp Files service. The application registration includes the Owner or Contributor role predefined by Azure. The location must be an Azure location that contains at least one delegated subnet created in a previous step. The`serviceLevel`

must match the`serviceLevel`

configured for the capacity pool in[Configure Azure NetApp Files for AKS workloads](azure-netapp-files#configure-azure-netapp-files-for-aks-workloads).`apiVersion: trident.netapp.io/v1 kind: TridentBackendConfig metadata: name: backend-tbc-anf spec: version: 1 storageDriverName: azure-netapp-files subscriptionID: aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e tenantID: aaaabbbb-0000-cccc-1111-dddd2222eeee location: eastus serviceLevel: Premium credentials: name: backend-tbc-anf-secret`

For more information about backends, see

[Azure NetApp Files backend configuration options and examples](https://docs.netapp.com/us-en/trident/trident-use/anf-examples.html).Apply the secret and backend using the

command. First apply the secret:`kubectl apply`

`kubectl apply -f backend-secret.yaml -n trident`

The output of the command resembles the following example:

`secret/backend-tbc-anf-secret created`

Apply the backend:

`kubectl apply -f backend-anf.yaml -n trident`

The output of the command resembles the following example:

`tridentbackendconfig.trident.netapp.io/backend-tbc-anf created`

Confirm the backend was created by using the

command:`kubectl get`

`kubectl get tridentbackends -n trident`

The output of the command resembles the following example:

`NAME BACKEND BACKEND UUID tbe-kfrdh backend-tbc-anf 8da4e926-9dd4-4a40-8d6a-375aab28c566`


### Create a storage class

A storage class is used to define how a unit of storage is dynamically created with a persistent volume. To consume Azure NetApp Files volumes, a storage class must be created.

Create a file named

`anf-storageclass.yaml`

and copy in the following YAML:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: azure-netapp-files provisioner: csi.trident.netapp.io parameters: backendType: "azure-netapp-files" fsType: "nfs"`

Create the storage class using the

command:`kubectl apply`

`kubectl apply -f anf-storageclass.yaml`

The output of the command resembles the following example:

`storageclass/azure-netapp-files created`

Run the

command to view the status of the storage class:`kubectl get`

`kubectl get sc NAME PROVISIONER RECLAIMPOLICY VOLUMEBINDINGMODE ALLOWVOLUMEEXPANSION AGE azure-netapp-files csi.trident.netapp.io Delete Immediate false`


### Create a PVC

A persistent volume claim (PVC) is a request for storage by a user. Upon the creation of a persistent volume claim, Trident automatically creates an Azure NetApp Files volume and makes it available for Kubernetes workloads to consume.

Create a file named

`anf-pvc.yaml`

and copy in the following YAML. In this example, a 1-TiB volume is needed with ReadWriteMany access.`kind: PersistentVolumeClaim apiVersion: v1 metadata: name: anf-pvc spec: accessModes: - ReadWriteMany resources: requests: storage: 1Ti storageClassName: azure-netapp-files`

Create the persistent volume claim with the

command:`kubectl apply`

`kubectl apply -f anf-pvc.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/anf-pvc created`

To view information about the persistent volume claim, run the

command:`kubectl get`

`kubectl get pvc`

The output of the command resembles the following example:

`kubectl get pvc -n trident NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE anf-pvc Bound pvc-bffa315d-3f44-4770-86eb-c922f567a075 1Ti RWO azure-netapp-files 62s`


### Use the persistent volume

After the PVC is created, Trident creates the persistent volume. A pod can be spun up to mount and access the Azure NetApp Files volume.

The following manifest can be used to define an NGINX pod that mounts the Azure NetApp Files volume created in the previous step. In this example, the volume is mounted at `/mnt/data`

.

Create a file named

`anf-nginx-pod.yaml`

and copy in the following YAML:`kind: Pod apiVersion: v1 metadata: name: nginx-pod spec: containers: - name: nginx image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: "/mnt/data" name: volume volumes: - name: volume persistentVolumeClaim: claimName: anf-pvc`

Create the pod using the

command:`kubectl apply`

`kubectl apply -f anf-nginx-pod.yaml`

The output of the command resembles the following example:

`pod/nginx-pod created`

Kubernetes has created a pod with the volume mounted and accessible within the

`nginx`

container at`/mnt/data`

. You can confirm by checking the event logs for the pod usingcommand:`kubectl describe`

`kubectl describe pod nginx-pod`

The output of the command resembles the following example:

`[...] Volumes: volume: Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace) ClaimName: anf-pvc ReadOnly: false default-token-k7952: Type: Secret (a volume populated by a Secret) SecretName: default-token-k7952 Optional: false [...] Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal Scheduled 15s default-scheduler Successfully assigned trident/nginx-pod to brameshb-non-root-test Normal SuccessfulAttachVolume 15s attachdetach-controller AttachVolume.Attach succeeded for volume "pvc-bffa315d-3f44-4770-86eb-c922f567a075" Normal Pulled 12s kubelet Container image "mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine" already present on machine Normal Created 11s kubelet Created container nginx Normal Started 10s kubelet Started container nginx`


## Next steps

Trident supports many features with Azure NetApp Files. For more information, see:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-vertical-pod-autoscaler -->

# Use the Vertical Pod Autoscaler in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use the Vertical Pod Autoscaler (VPA) on your Azure Kubernetes Service (AKS) cluster. The VPA automatically adjusts the CPU and memory requests for your pods to match the usage patterns of your workloads. This feature helps to optimize the performance of your applications and reduce the cost of running your workloads in AKS.

For more information, see the [Vertical Pod Autoscaler overview](vertical-pod-autoscaler).

## Before you begin

If you have an existing AKS cluster, make sure it's running Kubernetes version 1.24 or higher.

You need the Azure CLI version 2.52.0 or later installed and configured. Run

`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).If enabling VPA on an existing cluster, make sure

`kubectl`

is installed and configured to connect to your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --name <cluster-name> --resource-group <resource-group-name>`


## Deploy the Vertical Pod Autoscaler on a new cluster

Create a new AKS cluster with the VPA enabled using the

command with the`az aks create`

`--enable-vpa`

flag.`az aks create --name <cluster-name> --resource-group <resource-group-name> --enable-vpa --generate-ssh-keys`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.


## Update an existing cluster to use the Vertical Pod Autoscaler

Update an existing cluster to use the VPA using the

command with the`az aks update`

`--enable-vpa`

flag.`az aks update --name <cluster-name> --resource-group <resource-group-name> --enable-vpa`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.


## Disable the Vertical Pod Autoscaler on an existing cluster

Disable the VPA on an existing cluster using the

command with the`az aks update`

`--disable-vpa`

flag.`az aks update --name <cluster-name> --resource-group <resource-group-name> --disable-vpa`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.


## Test Vertical Pod Autoscaler installation

In the following example, we create a deployment with two pods, each running a single container that requests 100 millicore and tries to utilize slightly above 500 millicores. We also create a VPA config pointing at the deployment. The VPA observes the behavior of the pods, and after about five minutes, updates the pods to request 500 millicores.

Create a file named

`hamster.yaml`

and copy in the following manifest of the Vertical Pod Autoscaler example from the[kubernetes/autoscaler](https://github.com/kubernetes/autoscaler/blob/master/vertical-pod-autoscaler/examples/hamster.yaml)GitHub repository:`apiVersion: "autoscaling.k8s.io/v1" kind: VerticalPodAutoscaler metadata: name: hamster-vpa spec: targetRef: apiVersion: "apps/v1" kind: Deployment name: hamster resourcePolicy: containerPolicies: - containerName: '*' minAllowed: cpu: 100m memory: 50Mi maxAllowed: cpu: 1 memory: 500Mi controlledResources: ["cpu", "memory"] --- apiVersion: apps/v1 kind: Deployment metadata: name: hamster spec: selector: matchLabels: app: hamster replicas: 2 template: metadata: labels: app: hamster spec: securityContext: runAsNonRoot: true runAsUser: 65534 containers: - name: hamster image: registry.k8s.io/ubuntu-slim:0.1 resources: requests: cpu: 100m memory: 50Mi command: ["/bin/sh"] args: - "-c" - "while true; do timeout 0.5s yes >/dev/null; sleep 0.5s; done"`

Deploy the

`hamster.yaml`

Vertical Pod Autoscaler example using thecommand.`kubectl apply`

`kubectl apply -f hamster.yaml`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

View the running pods using the

command.`kubectl get`

`kubectl get pods -l app=hamster`

Your output should look similar to the following example output:

`hamster-78f9dcdd4c-hf7gk 1/1 Running 0 24s hamster-78f9dcdd4c-j9mc7 1/1 Running 0 24s`

View the CPU and Memory reservations on one of the pods using the

command. Make sure you replace`kubectl describe`

`<example-pod>`

with one of the pod IDs returned in your output from the previous step.`kubectl describe pod hamster-<example-pod>`

Your output should look similar to the following example output:

`hamster: Container ID: containerd:// Image: k8s.gcr.io/ubuntu-slim:0.1 Image ID: sha256: Port: <none> Host Port: <none> Command: /bin/sh Args: -c while true; do timeout 0.5s yes >/dev/null; sleep 0.5s; done State: Running Started: Wed, 28 Sep 2022 15:06:14 -0400 Ready: True Restart Count: 0 Requests: cpu: 100m memory: 50Mi Environment: <none>`

The pod has 100 millicpu and 50 Mibibytes of Memory reserved in this example. For this sample application, the pod needs less than 100 millicpu to run, so there's no CPU capacity available. The pods also reserves less memory than needed. The Vertical Pod Autoscaler

*vpa-recommender*deployment analyzes the pods hosting the hamster application to see if the CPU and Memory requirements are appropriate. If adjustments are needed, the vpa-updater relaunches the pods with updated values.Monitor the pods using the

command.`kubectl get`

`kubectl get --watch pods -l app=hamster`

When the new hamster pod starts, you can view the updated CPU and Memory reservations using the

command. Make sure you replace`kubectl describe`

`<example-pod>`

with one of the pod IDs returned in your output from the previous step.`kubectl describe pod hamster-<example-pod>`

Your output should look similar to the following example output:

`State: Running Started: Wed, 28 Sep 2022 15:09:51 -0400 Ready: True Restart Count: 0 Requests: cpu: 587m memory: 262144k Environment: <none>`

In the previous output, you can see that the CPU reservation increased to 587 millicpu, which is over five times the original value. The Memory increased to 262,144 Kilobytes, which is around 250 Mibibytes, or five times the original value. This pod was under-resourced, and the Vertical Pod Autoscaler corrected the estimate with a much more appropriate value.

View updated recommendations from VPA using the

command to describe the hamster-vpa resource information.`kubectl describe`

`kubectl describe vpa/hamster-vpa`

Your output should look similar to the following example output:

`State: Running Started: Wed, 28 Sep 2022 15:09:51 -0400 Ready: True Restart Count: 0 Requests: cpu: 587m memory: 262144k Environment: <none>`


## Set Vertical Pod Autoscaler requests

The `VerticalPodAutoscaler`

object automatically sets resource requests on pods with an `updateMode`

of `Auto`

. You can set a different value depending on your requirements and testing. In this example, we create and test a deployment manifest with two pods, each running a container that requests 100 milliCPU and 50 MiB of Memory, and sets the `updateMode`

to `Recreate`

.

Create a file named

`azure-autodeploy.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: vpa-auto-deployment spec: replicas: 2 selector: matchLabels: app: vpa-auto-deployment template: metadata: labels: app: vpa-auto-deployment spec: containers: - name: mycontainer image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine resources: requests: cpu: 100m memory: 50Mi command: ["/bin/sh"] args: ["-c", "while true; do timeout 0.5s yes >/dev/null; sleep 0.5s; done"]`

Create the pod using the

command.`kubectl create`

`kubectl create -f azure-autodeploy.yaml`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

View the running pods using the

command.`kubectl get`

`kubectl get pods`

Your output should look similar to the following example output:

`NAME READY STATUS RESTARTS AGE vpa-auto-deployment-54465fb978-kchc5 1/1 Running 0 52s vpa-auto-deployment-54465fb978-nhtmj 1/1 Running 0 52s`

Create a file named

`azure-vpa-auto.yaml`

and copy in the following manifest:`apiVersion: autoscaling.k8s.io/v1 kind: VerticalPodAutoscaler metadata: name: vpa-auto spec: targetRef: apiVersion: "apps/v1" kind: Deployment name: vpa-auto-deployment updatePolicy: updateMode: "Recreate"`

The

`targetRef.name`

value specifies that any pod controlled by a deployment named`vpa-auto-deployment`

belongs to`VerticalPodAutoscaler`

. The`updateMode`

value of`Recreate`

means that the Vertical Pod Autoscaler controller can delete a pod, adjust the CPU and Memory requests, and then create a new pod.Apply the manifest to the cluster using the

command.`kubectl apply`

`kubectl create -f azure-vpa-auto.yaml`

Wait a few minutes and then view the running pods using the

command.`kubectl get`

`kubectl get pods`

Your output should look similar to the following example output:

`NAME READY STATUS RESTARTS AGE vpa-auto-deployment-54465fb978-qbhc4 1/1 Running 0 2m49s vpa-auto-deployment-54465fb978-vbj68 1/1 Running 0 109s`

Get detailed information about one of your running pods using the

command. Make sure you replace`kubectl get`

`<pod-name>`

with the name of one of your pods from your previous output.`kubectl get pod <pod-name> --output yaml`

Your output should look similar to the following example output, which shows that VPA controller increased the Memory request to 262144k and the CPU request to 25 milliCPU:

`apiVersion: v1 kind: Pod metadata: annotations: vpaObservedContainers: mycontainer vpaUpdates: 'Pod resources updated by vpa-auto: container 0: cpu request, memory request' creationTimestamp: "2022-09-29T16:44:37Z" generateName: vpa-auto-deployment-54465fb978- labels: app: vpa-auto-deployment spec: containers: - args: - -c - while true; do timeout 0.5s yes >/dev/null; sleep 0.5s; done command: - /bin/sh image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine imagePullPolicy: IfNotPresent name: mycontainer resources: requests: cpu: 25m memory: 262144k`

Get detailed information about the Vertical Pod Autoscaler and its recommendations for CPU and Memory using the

command.`kubectl get`

`kubectl get vpa vpa-auto --output yaml`

Your output should look similar to the following example output:

`recommendation: containerRecommendations: - containerName: mycontainer lowerBound: cpu: 25m memory: 262144k target: cpu: 25m memory: 262144k uncappedTarget: cpu: 25m memory: 262144k upperBound: cpu: 230m memory: 262144k`

In this example, the results in the

`target`

attribute specify that it doesn't need to change the CPU or the Memory target for the container to run optimally. However, results can vary depending on the application and its resource utilization.The Vertical Pod Autoscaler uses the

`lowerBound`

and`upperBound`

attributes to decide whether to delete a pod and replace it with a new pod. If a pod has requests less than the lower bound or greater than the upper bound, the Vertical Pod Autoscaler deletes the pod and replaces it with a pod that meets the target attribute.

## Extra Recommender for Vertical Pod Autoscaler

The Recommender provides recommendations for resource usage based on real-time resource consumption. AKS deploys a Recommender when a cluster enables VPA. You can deploy a customized Recommender or an extra Recommender with the same image as the default one. The benefit of having a customized Recommender is that you can customize your recommendation logic. With an extra Recommender, you can partition VPAs to use different Recommenders.

In the following example, we create an extra Recommender, apply to an existing AKS cluster, and configure the VPA object to use the extra Recommender.

Create a file named

`extra_recommender.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: extra-recommender namespace: kube-system spec: replicas: 1 selector: matchLabels: app: extra-recommender template: metadata: labels: app: extra-recommender spec: serviceAccountName: vpa-recommender securityContext: runAsNonRoot: true runAsUser: 65534 containers: - name: recommender image: registry.k8s.io/autoscaling/vpa-recommender:0.13.0 imagePullPolicy: Always args: - --recommender-name=extra-recommender resources: limits: cpu: 200m memory: 1000Mi requests: cpu: 50m memory: 500Mi ports: - name: prometheus containerPort: 8942`

Deploy the

`extra-recomender.yaml`

Vertical Pod Autoscaler example using thecommand.`kubectl apply`

`kubectl apply -f extra-recommender.yaml`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

Create a file named

`hamster-extra-recommender.yaml`

and copy in the following manifest:`apiVersion: "autoscaling.k8s.io/v1" kind: VerticalPodAutoscaler metadata: name: hamster-vpa spec: recommenders: - name: 'extra-recommender' targetRef: apiVersion: "apps/v1" kind: Deployment name: hamster updatePolicy: updateMode: "Auto" resourcePolicy: containerPolicies: - containerName: '*' minAllowed: cpu: 100m memory: 50Mi maxAllowed: cpu: 1 memory: 500Mi controlledResources: ["cpu", "memory"] --- apiVersion: apps/v1 kind: Deployment metadata: name: hamster spec: selector: matchLabels: app: hamster replicas: 2 template: metadata: labels: app: hamster spec: securityContext: runAsNonRoot: true runAsUser: 65534 # nobody containers: - name: hamster image: k8s.gcr.io/ubuntu-slim:0.1 resources: requests: cpu: 100m memory: 50Mi command: ["/bin/sh"] args: - "-c" - "while true; do timeout 0.5s yes >/dev/null; sleep 0.5s; done"`

If

`memory`

isn't specified in`controlledResources`

, the Recommender doesn't respond to OOM events. In this example, we only set CPU in`controlledValues`

.`controlledValues`

allows you to choose whether to update the container's resource requests using the`RequestsOnly`

option, or by both resource requests and limits using the`RequestsAndLimits`

option. The default value is`RequestsAndLimits`

. If you use the`RequestsAndLimits`

option, requests are computed based on actual usage, and limits are calculated based on the current pod's request and limit ratio.For example, if you start with a pod that requests 2 CPUs and limits to 4 CPUs, VPA always sets the limit to be twice as much as requests. The same principle applies to Memory. When you use the

`RequestsAndLimits`

mode, it can serve as a blueprint for your initial application resource requests and limits.You can simplify the VPA object using

`Auto`

mode and computing recommendations for both CPU and Memory.Deploy the

`hamster-extra-recomender.yaml`

example using thecommand.`kubectl apply`

`kubectl apply -f hamster-extra-recommender.yaml`

Monitor your pods using the

`[kubectl get`

][kubectl-get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command.`kubectl get --watch pods -l app=hamster`

When the new hamster pod starts, view the updated CPU and Memory reservations using the

command. Make sure you replace`kubectl describe`

`<example-pod>`

with one of your pod IDs.`kubectl describe pod hamster-<example-pod>`

Your output should look similar to the following example output:

`State: Running Started: Wed, 28 Sep 2022 15:09:51 -0400 Ready: True Restart Count: 0 Requests: cpu: 587m memory: 262144k Environment: <none>`

View updated recommendations from VPA using the

command.`kubectl describe`

`kubectl describe vpa/hamster-vpa`

Your output should look similar to the following example output:

`State: Running Started: Wed, 28 Sep 2022 15:09:51 -0400 Ready: True Restart Count: 0 Requests: cpu: 587m memory: 262144k Environment: <none> Spec: recommenders: Name: customized-recommender`


## Troubleshoot the Vertical Pod Autoscaler

If you encounter issues with the Vertical Pod Autoscaler, you can troubleshoot the system components and custom resource definition to identify the problem.

Verify that all system components are running using the following command:

`kubectl get pods|grep vpa`

Your output should list

*three pods*: recommender, updater, and admission-controller, all with a status of`Running`

.For each of the pods returned in your previous output, verify that the system components are logging any errors using the following command:

`kubectl logs [pod name] | grep -e '^E[0-9]\{4\}'`

Verify that the custom resource definition was created using the following command:

`kubectl get customresourcedefinition | grep verticalpodautoscalers`


## Next steps

To learn more about the VPA object, see the [Vertical Pod Autoscaler API reference](vertical-pod-autoscaler-api-reference).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices-cost -->

# Best practices for cost optimization in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Cost optimization is about maximizing the value of resources while minimizing unnecessary expenses within your cloud environment. This process involves identifying cost effective configuration options and implementing best practices to improve operational efficiency. An AKS environment can be optimized to minimize cost while taking into account performance and reliability requirements.

In this article, you learn about:

- Holistic monitoring and FinOps practices.
- Strategic infrastructure selection.
- Dynamic rightsizing and autoscaling.
- Leveraging Azure discounts for substantial savings.

## Embrace FinOps to build a cost saving culture

[Financial operations (FinOps)](https://www.finops.org/introduction/what-is-finops/) is a discipline that combines financial accountability with cloud management and optimization. It focuses on driving alignment between finance, operations, and engineering teams to understand and control cloud costs. The FinOps foundation has several notable projects, such as the [ FinOps Framework](https://finops.org/framework) and the

[.](https://focus.finops.org/)

**FOCUS Specification**For more information, see [What is FinOps?](/en-us/azure/cost-management-billing/finops/)

## Prepare the application environment

### Evaluate SKU family

It's important to evaluate the resource requirements of your application before deployment. Small development workloads have different infrastructure needs than large production ready workloads. While a combination of CPU, memory, and networking capacity configurations heavily influences the cost effectiveness of a SKU, consider the following virtual machine (VM) types:

| SKU family | Description | Use case |
|---|---|---|
Azure Spot Virtual Machines |

[Spot node pools](spot-node-pool)and deployed to a single fault domain with no high availability or service-level agreement (SLA) guarantees. Spot VMs allow you to take advantage of unutilized Azure capacity with significant discounts (up to 90%, as compared to pay-as-you-go prices). If Azure needs capacity back, the Azure infrastructure evicts the Spot nodes.**Arm-based processors (Arm64)**[Arm64 node pool support in AKS](use-arm64-vms), you can create Arm64 Ubuntu agent nodes and even mix Intel and ARM architecture nodes within a cluster. These ARM VMs are engineered to efficiently run dynamic, scalable workloads and can deliver up to 50% better price-performance than comparable x86-based VMs for scale-out workloads.**GPU optimized SKUs**[GPU-enabled Linux node pools on AKS](gpu-cluster)are best for compute-intensive workloads like graphics rendering, large model training, and inferencing.Note

The cost of compute varies across regions. When picking a less expensive region to run workloads, be conscious of the potential impact of latency as well as data transfer costs. To learn more about VM SKUs and their characteristics, see [Sizes for virtual machines in Azure](/en-us/azure/virtual-machines/sizes).

### Review storage options

For more information on storage options and related cost considerations, see the following articles:

[Best practices for storage and backups in Azure Kubernetes Service (AKS)](operator-best-practices-storage)[Storage options for applications in Azure Kubernetes Service (AKS)](concepts-storage)

### Use cluster preset configurations

It can be difficult to pick the right VM SKU, regions, number of nodes, and other configuration options. [Cluster preset configurations](quotas-skus-regions#cluster-configuration-presets-in-the-azure-portal) in the Azure portal offloads this initial challenge by providing recommended configurations for different application environments that are cost-conscious and performant. The **Dev/Test** preset is best for developing new workloads or testing existing workloads. The **Production Economy** preset is best for serving production traffic in a cost-conscious way if your workloads can tolerate interruptions. Noncritical features are off by default, and the preset values can be modified at any time.

### Consider multitenancy

AKS offer flexibility in how you run multitenant clusters and isolate resources. For friendly multitenancy, you can share clusters and infrastructure across teams and business units through [ logical isolation](operator-best-practices-cluster-isolation#logically-isolated-clusters). Kubernetes

[Namespaces](concepts-clusters-workloads#namespaces)form the logical isolation boundary for workloads and resources. Sharing infrastructure reduces cluster management overhead while also improving resource utilization and pod density within the cluster. To learn more about multitenancy on AKS and to determine if it's right for your organizational needs, see

[AKS considerations for multitenancy](/en-us/azure/architecture/guide/multitenant/service/aks)and

[Design clusters for multitenancy](operator-best-practices-cluster-isolation#design-clusters-for-multi-tenancy).

Warning

Kubernetes environments aren't entirely safe for hostile multitenancy. If any tenant on the shared infrastructure can't be trusted, more planning is needed to prevent tenants from impacting the security of other services.

Consider [ physical isolation](operator-best-practices-cluster-isolation#physically-isolated-clusters) boundaries. In this model, teams or workloads are assigned to their own cluster. Added management and financial overhead will be a tradeoff.

## Build cloud native applications

### Make your container as lean as possible

A lean container refers to optimizing the size and resource footprint of the containerized application. Check that your base image is minimal and only contains the necessary dependencies. Remove any unnecessary libraries and packages. A smaller container image accelerates deployment times and increases the efficiency of scaling operations. [Artifact Streaming on AKS](artifact-streaming) allows you to stream container images from Azure Container Registry (ACR). It pulls only the necessary layer for initial pod startup, reducing the pull time for larger images from minutes to seconds.

### Enforce resource quotas

[Resource quotas](operator-best-practices-scheduler#enforce-resource-quotas) provide a way to reserve and limit resources across a development team or project. Quotas are defined on a namespace and can set on compute resources, storage resources, and object counts. When you define resource quotas, it prevents individual namespaces from consuming more resources than allocated. Resource quotas are useful for multitenant clusters where teams are sharing infrastructure.

### Use cluster start/stop

When left unattended, small development/test clusters can accrue unnecessary costs. You can turn off clusters that don't need to run at all times using the [cluster start and stop](start-stop-cluster?tabs=azure-cli) feature. This feature shuts down all system and user node pools so you don't pay for extra compute. The state of your cluster and objects is maintained when you start the cluster again.

### Use capacity reservations

Capacity reservations allow you to reserve compute capacity in an Azure region or availability zone for any duration of time. Reserved capacity is available for immediate use until the reservation is deleted. [Associating an existing capacity reservation group to a node pool](manage-node-pools#associate-capacity-reservation-groups-to-node-pools) guarantees allocated capacity for your node pool and helps you avoid potential on-demand pricing spikes during periods of high compute demand.

## Monitor your environment and spend

### Increase visibility with Microsoft Cost Management

[Microsoft Cost Management](/en-us/azure/cost-management-billing/cost-management-billing-overview) offers a broad set of capabilities to help with cloud budgeting, forecasting, and visibility for costs both inside and outside of the cluster. Proper visibility is essential for deciphering spending trends, identifying optimization opportunities, and increasing accountability among application developers and platform teams. Enable the [AKS Cost Analysis add-on](cost-analysis) for granular cluster cost breakdown by Kubernetes constructs along with Azure Compute, Network, and Storage categories.

### Azure Monitor

If you're ingesting metric data via Container insights, we recommend migrating to managed Prometheus, which offers a significant cost reduction. You can [disable Container insights metrics using the data collection rule (DCR)](/en-us/azure/azure-monitor/containers/container-insights-data-collection-dcr?tabs=portal) and deploy the [managed Prometheus add-on](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable#enable-prometheus-and-grafana), which supports configuration via Azure Resource Manager, Azure CLI, Azure portal, and Terraform.

For more information, see [Azure Monitor best practices](/en-us/azure/azure-monitor/best-practices-containers#cost-optimization) and [managing costs for Container insights](/en-us/azure/azure-monitor/containers/container-insights-cost).

### Log Analytics

For control plane logs, consider disabling the categories you don't need and/or using the Basic Logs API when applicable to reduce Log Analytics costs. For more information, see [Azure Kubernetes Service (AKS) control plane/resource logs](monitor-aks#aks-control-plane-resource-logs). For data plane logs, or *application logs*, consider adjusting the [cost optimization settings](monitor-aks#aks-data-plane-container-insights-logs).

You can also use [Transformations in Azure Monitor](/en-us/azure/azure-monitor/data-collection/data-collection-transformations) to filter or modify control plane and data plane logs before they are sent to a Log Analytics workspace. For more information on how to create a transformation see [Create a transformation in Azure Monitor](/en-us/azure/azure-monitor/data-collection/data-collection-transformations-create?tabs=portal).

### Azure Advisor cost recommendations

AKS cost recommendations in Azure Advisor provide recommendations to help you achieve cost-efficiency without sacrificing reliability. Advisor analyzes your resource configurations and recommends optimization solutions. For more information, see [Get Azure Kubernetes Service (AKS) cost recommendations in Azure Advisor](cost-advisors).

## Optimize workloads through autoscaling

### Establish a baseline

Before configuring your autoscaling settings, you can use [Azure Load Testing](/en-us/azure/load-testing/overview-what-is-azure-load-testing) to establish a baseline for your application. Load testing helps you understand how your application behaves under different traffic conditions and identify performance bottlenecks. Once you have a baseline, you can configure autoscaling settings to ensure your application can handle the expected load.

### Enable application autoscaling

#### Vertical pod autoscaling

Requests and limits that are higher than actual usage can result in overprovisioned workloads and wasted resources. In contrast, requests and limits that are too low can result in throttling and workload issues due to lack of memory. The [Vertical Pod Autoscaler (VPA)](vertical-pod-autoscaler) allows you to fine-tune CPU and memory resources required by your pods. VPA provides recommended values for CPU and memory requests and limits based on historical container usage, which you can set manually or update automatically. * Best for applications with fluctuating resource demands*. VPA’s recommendation-only

*off mode*allows teams to review resource suggestions without enforcing them automatically. This mode can be enabled during testing, and VPA recommendations can be used to set the CPU and memory request and limits for production environments.

#### Horizontal pod autoscaling

The [Horizontal Pod Autoscaler (HPA)](concepts-scale#horizontal-pod-autoscaler) dynamically scales the number of pod replicas based on observed metrics, such as CPU or memory utilization. During periods of high demand, HPA scales out, adding more pod replicas to distribute the workload. During periods of low demand, HPA scales in, reducing the number of replicas to conserve resources. * Best for applications with predictable resource demands*.

Warning

You shouldn't use the VPA with the HPA on the same CPU or memory metrics. This combination can lead to conflicts, as both autoscalers attempt to respond to changes in demand using the same metrics. However, you can use the VPA for CPU or memory with the HPA for custom metrics to prevent overlap and ensure that each autoscaler focuses on distinct aspects of workload scaling.

#### Kubernetes event-driven autoscaling

The [Kubernetes Event-driven Autoscaler (KEDA) add-on](keda-about) provides extra flexibility to scale based on various event-driven metrics that align with your application behavior. For example, for a web application, KEDA can monitor incoming HTTP request traffic and adjust the number of pod replicas to ensure the application remains responsive. For processing jobs, KEDA can scale the application based on message queue length. Managed support is provided for all [Azure Scalers](https://keda.sh/docs/2.13/scalers/). KEDA also allows you to scale down to 0 replicas, especially helpful for sporadic event-driven workloads, periodic machine learning (ML) or GPU workloads, and dev/test or low traffic environments.

### Enable infrastructure autoscaling

#### Cluster autoscaling

To keep up with application demand, the [Cluster Autoscaler](cluster-autoscaler-overview) watches for pods that can't be scheduled due to resource constraints and scales the number of nodes in the node pool accordingly. When nodes don't have running pods, the Cluster Autoscaler scales down the number of nodes. The Cluster Autoscaler profile settings apply to all autoscaler-enabled node pools in a cluster. For more information, see [Cluster Autoscaler best practices and considerations](cluster-autoscaler-overview#best-practices-and-considerations).

#### Node autoprovisioning

Complicated workloads might require several node pools with different VM size configurations to accommodate CPU and memory requirements. Accurately selecting and managing several node pool configurations adds complexity and operational overhead. [Node Autoprovision (NAP)](node-autoprovision?tabs=azure-cli) simplifies the SKU selection process and decides the optimal VM configuration based on pending pod resource requirements to run workloads in the most efficient and cost effective manner.

Note

For more information on scaling best practices, see [Performance and scaling for small to medium workloads in Azure Kubernetes Service (AKS)](best-practices-performance-scale) and [Performance and scaling best practices for large workloads in Azure Kubernetes Service (AKS)](best-practices-performance-scale-large).

## Save with Azure discounts

### Azure Reservations

If your workload is predictable and exists for an extended period of time, consider purchasing an [Azure Reservation](/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations) to further reduce your resource costs. Azure Reservations operate on a one-year or three-year term, offering up to 72% discount as compared to pay-as-you-go prices for compute. Reservations automatically apply to matching resources. * Best for workloads that are committed to running in the same SKUs and regions over an extended period of time*.

### Azure Savings Plan

If you have consistent spend, but your use of disparate resources across SKUs and regions makes Azure Reservations infeasible, consider purchasing an [Azure Savings Plan](/en-us/azure/cost-management-billing/savings-plan/savings-plan-compute-overview). Like Azure Reservations, Azure Savings Plans operate on a one-year or three-year term and automatically apply to any resources within benefit scope. You commit to spend a fixed hourly amount on compute resources irrespective of SKU or region. * Best for workloads that utilize different resources and/or different data center regions*.

### Azure Hybrid Benefit

[Azure Hybrid Benefit for Azure Kubernetes Service (AKS)](azure-hybrid-benefit) allows you to maximize your on-premises licenses at no extra cost. Use any qualifying on-premises licenses that also have an active Software Assurance (SA) or a qualifying subscription to get Windows VMs on Azure at a reduced cost.

## Next steps

Cost optimization is an ongoing and iterative effort. Learn more by reviewing the following recommendations and architecture guidance:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/postgresql-ha-overview -->

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

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/csi-secrets-store-configuration-options -->

# Azure Key Vault provider for Secrets Store CSI Driver for AKS configuration and troubleshooting options

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Key Vault provider for Secrets Store Container Storage Interface (CSI) Driver enables secure and automated management of secrets in Azure Kubernetes Service (AKS). This article provides guidance on configuring the provider, troubleshooting common issues, and optimizing secret handling in your AKS environment.

## Prerequisites

Follow the steps in the following articles before proceeding with this guide. Once you complete these steps, you can apply extra configurations or perform troubleshooting on your AKS cluster.

[Use the Azure Key Vault provider for Secrets Store CSI Driver in an AKS cluster](csi-secrets-store-driver)[Provide an identity to access the Azure Key Vault provider for Secrets Store CSI Driver in AKS](csi-secrets-store-identity-access)

## Configuration options

### Manage auto rotation

Once you enable auto rotation for Azure Key Vault Secrets Provider, it updates the pod mount and the Kubernetes secret defined in the `secretObjects`

field of `SecretProviderClass`

. It does so by polling for changes periodically, based on the rotation poll interval you defined. The default rotation poll interval is *two minutes*. When a secret is updated in the external secrets store after the initial pod deployment, both the Kubernetes Secret and the pod mount are periodically refreshed. The update frequency and method depend on how your application accesses the secret data.

**Mount the Kubernetes Secret as a volume**: Use the auto rotation and sync K8s secrets features of Secrets Store CSI Driver. The application needs to watch for changes from the mounted Kubernetes Secret volume. When the CSI Driver updates the Kubernetes Secret, the corresponding volume contents automatically update as well.**Application reads the data from the container filesystem**: Use the rotation feature of Secrets Store CSI Driver. The application needs to watch for the file change from the volume mounted by the CSI driver.**Use the Kubernetes Secret for an environment variable**: Restart the pod to get the latest secret as an environment variable. Use a tool such as[Reloader](https://github.com/stakater/Reloader)to watch for changes on the synced Kubernetes Secret and perform rolling upgrades on pods.

To enable auto rotation of secrets on a new AKS cluster using the

command and enable the`az aks create`

`enable-secret-rotation`

add-on, run the following command:`az aks create \ --name myAKSCluster2 \ --resource-group myResourceGroup \ --enable-addons azure-keyvault-secrets-provider \ --enable-secret-rotation \ --generate-ssh-keys`

To update an existing AKS cluster to enable auto rotation of secrets using the

command and the`az aks addon update`

`enable-secret-rotation`

parameter, run the following command:`az aks addon update --resource-group myResourceGroup --name myAKSCluster2 --addon azure-keyvault-secrets-provider --enable-secret-rotation`


### Sync mounted content with a Kubernetes secret

Note

The YAML examples in this section are incomplete. You need to modify them to support your chosen method of access to your key vault identity. For details, see [Provide an identity to access the Azure Key Vault provider for Secrets Store CSI Driver](csi-secrets-store-identity-access).

You might want to create a Kubernetes secret to mirror your mounted secrets content. Your secrets sync after you start a pod to mount them. When you delete the pods that consume the secrets, your Kubernetes secret is also deleted.

Sync mounted content with a Kubernetes secret using the `secretObjects`

field when creating a `SecretProviderClass`

to define the desired state of the Kubernetes secret, as shown in the
following example YAML. Make sure the `objectName`

in the `secretObjects`

field matches the file name of the mounted content. If you use `objectAlias`

instead, it should match the object alias.

```
apiVersion: secrets-store.csi.x-k8s.io/v1
kind: SecretProviderClass
metadata:
name: azure-sync
spec:
provider: azure
secretObjects: # [OPTIONAL] SecretObjects defines the desired state of synced Kubernetes secret objects
- data:
- key: username # data field to populate
objectName: foo1 # name of the mounted content to sync; this could be the object name or the object alias
secretName: foosecret # name of the Kubernetes secret object
type: Opaque # type of Kubernetes secret object (for example, Opaque, kubernetes.io/tls)
```


### Set an environment variable to reference Kubernetes secrets

Note

The example YAML demonstrates how to access a secret using either environment variables or `volume/volumeMount`

. Typically, an application uses one method or the other. However, to make a secret available through environment variables, at least one pod must mount the secret.

Reference your newly created Kubernetes secret by setting an environment variable in your pod, as shown in the following example YAML.

```
kind: Pod
apiVersion: v1
metadata:
name: busybox-secrets-store-inline
spec:
containers:
- name: busybox
image: registry.k8s.io/e2e-test-images/busybox:1.29-1
command:
- "/bin/sleep"
- "10000"
volumeMounts:
- name: secrets-store01-inline
mountPath: "/mnt/secrets-store"
readOnly: true
env:
- name: SECRET_USERNAME
valueFrom:
secretKeyRef:
name: foosecret
key: username
volumes:
- name: secrets-store01-inline
csi:
driver: secrets-store.csi.k8s.io
readOnly: true
volumeAttributes:
secretProviderClass: "azure-sync"
```


### Migrate from open-source to AKS-managed Secrets Store CSI Driver

Uninstall the open-source Secrets Store CSI Driver using the following

`helm delete`

command:`helm delete <release name>`

Tip

If you installed the driver and provider using deployment YAMLs, you can delete the components using the following

`kubectl delete`

command:`# Delete AKV provider pods from Linux nodes kubectl delete -f https://raw.githubusercontent.com/Azure/secrets-store-csi-driver-provider-azure/master/deployment/provider-azure-installer.yaml # Delete AKV provider pods from Windows nodes kubectl delete -f https://raw.githubusercontent.com/Azure/secrets-store-csi-driver-provider-azure/master/deployment/provider-azure-installer-windows.yaml`

Upgrade your existing AKS cluster with the feature using the

command:`az aks enable-addons`

`az aks enable-addons --addons azure-keyvault-secrets-provider --name myAKSCluster --resource-group myResourceGroup`


## Access metrics

You can monitor the health and performance of the Azure Key Vault provider for Secrets Store CSI Driver by collecting metrics it exposes. These metrics provide insights into request durations, error rates, and the overall operation of the provider and driver components, helping you troubleshoot issues and optimize your AKS cluster's secret management.

Metrics are served via Prometheus from port 8898, but this port isn't exposed outside the pod by default. Access the metrics over localhost using the `kubectl port-forward`

command:

```
kubectl port-forward -n kube-system ds/aks-secrets-store-provider-azure 8898:8898 & curl localhost:8898/metrics
```


These metrics help you monitor the performance and reliability of the Azure Key Vault provider including request latency and error tracking for both Key Vault and gRPC operations.

| Metric | Description | Tags |
|---|---|---|
| keyvault_request | The distribution of how long it took to get from the key vault. | `os_type=<runtime os>` , `provider=azure` , `object_name=<keyvault object name>` , `object_type=<keyvault object type>` , `error=<error if failed>` |
| grpc_request | The distribution of how long it took for the gRPC requests. | `os_type=<runtime os>` , `provider=azure` , `grpc_method=<rpc full method>` , `grpc_code=<grpc status code>` , `grpc_message=<grpc status message>` |

## Troubleshooting

For troubleshooting steps, see [Troubleshoot Azure Key Vault Provider for Secrets Store CSI Driver](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-key-vault-csi-secrets-store-csi-driver).

## Next steps

To learn more about the Azure Key Vault provider for Secrets Store CSI Driver, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/gpu-cluster -->

# Use GPUs for compute-intensive workloads on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Graphical processing units (GPUs) are often used for compute-intensive workloads, such as graphics and visualization workloads. AKS supports GPU-enabled Linux node pools to run compute-intensive Kubernetes workloads.

This article helps you provision nodes with schedulable GPUs on new and existing AKS clusters.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Supported GPU-enabled VMs

To view the available GPU-enabled VMs, see [GPU-optimized VM sizes in Azure](/en-us/azure/virtual-machines/sizes-gpu). If a GPU VM size is not in our list of supported VM sizes, AKS does not install the necessary GPU software components or provide support. AKS allows the use of unsupported GPU VM sizes after [skipping the automatic GPU driver installation](#skip-gpu-driver-installation).

Check available and supported VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm) command.

```
az vm list-skus --location <your-location> --output table
```


For AKS node pools, we recommend a minimum size of *Standard_NC6s_v3*. The NVv4 series (based on AMD GPUs) aren't supported on AKS.

Note

GPU-enabled VMs contain specialized hardware subject to higher pricing and region availability. For more information, see the [pricing](https://azure.microsoft.com/pricing/) tool and [region availability](https://azure.microsoft.com/global-infrastructure/services/).

## Limitations

- If you're using an Azure Linux GPU-enabled node pool, automatic security patches aren't applied. Refer to your current AKS API version for the default behavior of node OS upgrade channel.
[Flatcar Container Linux for AKS](flatcar-container-linux-for-aks)isn't supported with NVIDIA GPU on AKS.[Azure Linux with OS Guard for AKS](use-azure-linux-os-guard)isn't supported with NVIDIA GPU on AKS.

Note

For AKS API version 2023-06-01 or later, the default channel for node OS upgrade is *NodeImage*. For previous versions, the default channel is *None*. To learn more, see [auto-upgrade](auto-upgrade-node-image).

- Updating an existing node pool to add GPU VM size is not supported on AKS.

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the Azure CLI version 2.72.2 or later installed to set the
`--gpu-driver`

field. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you have the
`aks-preview`

Azure CLI extension installed, please update the version to 18.0.0b2 or later.

## Get the credentials for your cluster

Get the credentials for your AKS cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. The following example command gets the credentials for the

*myAKSCluster*in the

*myResourceGroup*resource group:

```
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```


## Options for using NVIDIA GPUs

Using NVIDIA GPUs involves the installation of various NVIDIA software components such as the [NVIDIA device plugin for Kubernetes](https://github.com/NVIDIA/k8s-device-plugin?tab=readme-ov-file), GPU driver installation, and more.

Note

By default, Microsoft automatically maintains the version of the NVIDIA drivers as part of the node image deployment, and AKS * supports and manages* it. While the NVIDIA drivers are installed by default on GPU capable nodes, you need to install the device plugin.

### NVIDIA device plugin installation

NVIDIA device plugin installation is required when using GPUs on AKS. In some cases, the installation is handled automatically, such as when using the [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html). Alternatively, you can manually install the NVIDIA device plugin.

#### Manually install the NVIDIA device plugin

You can deploy a DaemonSet for the NVIDIA device plugin, which runs a pod on each node to provide the required drivers for the GPUs. This is the recommended approach when using GPU-enabled node pools for Azure Linux.

To use the default OS SKU, you create the node pool without specifying an OS SKU. The node pool is configured for the default operating system based on the Kubernetes version of the cluster.

Add a node pool to your cluster using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name gpunp \
--node-count 1 \
--node-vm-size Standard_NC6s_v3 \
--node-taints sku=gpu:NoSchedule \
--enable-cluster-autoscaler \
--min-count 1 \
--max-count 3
```


This command adds a node pool named *gpunp* to *myAKSCluster* in *myResourceGroup* and uses parameters to configure the following node pool settings:

`--node-vm-size`

: Sets the VM size for the node in the node pool to*Standard_NC6s_v3*.`--node-taints`

: Specifies a*sku=gpu:NoSchedule*taint on the node pool.`--enable-cluster-autoscaler`

: Enables the cluster autoscaler.`--min-count`

: Configures the cluster autoscaler to maintain a minimum of one node in the node pool.`--max-count`

: Configures the cluster autoscaler to maintain a maximum of three nodes in the node pool.

Note

Taints and VM sizes can only be set for node pools during node pool creation, but you can update autoscaler settings at any time.

Create a namespace using the

command.`kubectl create namespace`

`kubectl create namespace gpu-resources`

Create a file named

*nvidia-device-plugin-ds.yaml*and paste the following YAML manifest provided as part of the[NVIDIA device plugin for Kubernetes project](https://github.com/NVIDIA/k8s-device-plugin/blob/4b3d6b0a6613a3672f71ea4719fd8633eaafb4f3/deployments/static/nvidia-device-plugin.yml):`apiVersion: apps/v1 kind: DaemonSet metadata: name: nvidia-device-plugin-daemonset namespace: gpu-resources spec: selector: matchLabels: name: nvidia-device-plugin-ds updateStrategy: type: RollingUpdate template: metadata: labels: name: nvidia-device-plugin-ds spec: tolerations: - key: "sku" operator: "Equal" value: "gpu" effect: "NoSchedule" # Mark this pod as a critical add-on; when enabled, the critical add-on # scheduler reserves resources for critical add-on pods so that they can # be rescheduled after a failure. # See https://kubernetes.io/docs/tasks/administer-cluster/guaranteed-scheduling-critical-addon-pods/ priorityClassName: "system-node-critical" containers: - image: nvcr.io/nvidia/k8s-device-plugin:v0.18.0 name: nvidia-device-plugin-ctr env: - name: FAIL_ON_INIT_ERROR value: "false" securityContext: allowPrivilegeEscalation: false capabilities: drop: ["ALL"] volumeMounts: - name: device-plugin mountPath: /var/lib/kubelet/device-plugins volumes: - name: device-plugin hostPath: path: /var/lib/kubelet/device-plugins`

Create the DaemonSet and confirm the NVIDIA device plugin is created successfully using the

command.`kubectl apply`

`kubectl apply -f nvidia-device-plugin-ds.yaml`

Now that you successfully installed the NVIDIA device plugin, you can check that your

[GPUs are schedulable](#confirm-that-gpus-are-schedulable)and[run a GPU workload](#run-a-gpu-enabled-workload).

### Skip GPU driver installation

If you want to control the installation of the NVIDIA drivers or use the [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html), you can skip the default GPU driver installation. Microsoft **doesn't support or manage** the maintenance and compatibility of the NVIDIA drivers as part of the node image deployment.

Important

Starting on **August 14, 2025**, Azure Kubernetes Service (AKS) no longer supports the `--skip-gpu-driver-install`

node pool tag. After this date, you'll be unable to provision GPU-enabled node pools using this tag to bypass automatic GPU driver installation. You can achieve the same behavior by setting the `--gpu-driver`

field to `none`

. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4925) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=496440). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Create a node pool using the

command and set`az aks nodepool add`

`--gpu-driver`

field to`none`

to skip default GPU driver installation.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --gpu-driver none \ --node-vm-size Standard_NC6s_v3 \ --enable-cluster-autoscaler \ --min-count 1 \ --max-count 3`

Setting the

`--gpu-driver`

API field to`none`

during node pool creation skips the automatic GPU driver installation. Any existing nodes aren't changed. You can scale the node pool to zero and then back up to make the change take effect.If you get the error

`unrecognized arguments: --gpu-driver none`

then[update the Azure CLI version](/en-us/cli/azure/update-azure-cli). For more information, see[Before you begin](#before-you-begin).You can optionally install the NVIDIA GPU Operator following

[these steps](nvidia-gpu-operator).

## Confirm that GPUs are schedulable

After creating your cluster, confirm that GPUs are schedulable in Kubernetes.

List the nodes in your cluster using the

command.`kubectl get nodes`

`kubectl get nodes`

Your output should look similar to the following example output:

`NAME STATUS ROLES AGE VERSION aks-gpunp-28993262-0 Ready agent 13m v1.20.7`

Confirm the GPUs are schedulable using the

command.`kubectl describe node`

`kubectl describe node aks-gpunp-28993262-0`

Under the

*Capacity*section, the GPU should list as`nvidia.com/gpu: 1`

. Your output should look similar to the following condensed example output:`Name: aks-gpunp-28993262-0 Roles: agent Labels: accelerator=nvidia [...] Capacity: [...] nvidia.com/gpu: 1 [...]`


## Run a GPU-enabled workload

To see the GPU in action, you can schedule a GPU-enabled workload with the appropriate resource request. In this example, we'll run a [Tensorflow](https://www.tensorflow.org/) job against the [MNIST dataset](http://yann.lecun.com/exdb/mnist/).

Create a file named

*samples-tf-mnist-demo.yaml*and paste the following YAML manifest, which includes a resource limit of`nvidia.com/gpu: 1`

:Note

If you receive a version mismatch error when calling into drivers, such as "CUDA driver version is insufficient for CUDA runtime version", review the

[NVIDIA driver matrix compatibility chart](https://docs.nvidia.com/deploy/cuda-compatibility/index.html).`apiVersion: batch/v1 kind: Job metadata: labels: app: samples-tf-mnist-demo name: samples-tf-mnist-demo spec: template: metadata: labels: app: samples-tf-mnist-demo spec: containers: - name: samples-tf-mnist-demo image: mcr.microsoft.com/azuredocs/samples-tf-mnist-demo:gpu args: ["--max_steps", "500"] imagePullPolicy: IfNotPresent resources: limits: nvidia.com/gpu: 1 restartPolicy: OnFailure tolerations: - key: "sku" operator: "Equal" value: "gpu" effect: "NoSchedule"`

Run the job using the

command, which parses the manifest file and creates the defined Kubernetes objects.`kubectl apply`

`kubectl apply -f samples-tf-mnist-demo.yaml`


## View the status of the GPU-enabled workload

Monitor the progress of the job using the

command with the`kubectl get jobs`

`--watch`

flag. It may take a few minutes to first pull the image and process the dataset.`kubectl get jobs samples-tf-mnist-demo --watch`

When the

*COMPLETIONS*column shows*1/1*, the job has successfully finished, as shown in the following example output:`NAME COMPLETIONS DURATION AGE samples-tf-mnist-demo 0/1 3m29s 3m29s samples-tf-mnist-demo 1/1 3m10s 3m36s`

Exit the

`kubectl --watch`

process with*Ctrl-C*.Get the name of the pod using the

command.`kubectl get pods`

`kubectl get pods --selector app=samples-tf-mnist-demo`

View the output of the GPU-enabled workload using the

command.`kubectl logs`

`kubectl logs samples-tf-mnist-demo-smnr6`

The following condensed example output of the pod logs confirms that the appropriate GPU device,

`Tesla K80`

, has been discovered:`2019-05-16 16:08:31.258328: I tensorflow/core/platform/cpu_feature_guard.cc:137] Your CPU supports instructions that this TensorFlow binary was not compiled to use: SSE4.1 SSE4.2 AVX AVX2 FMA 2019-05-16 16:08:31.396846: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1030] Found device 0 with properties: name: Tesla K80 major: 3 minor: 7 memoryClockRate(GHz): 0.8235 pciBusID: 2fd7:00:00.0 totalMemory: 11.17GiB freeMemory: 11.10GiB 2019-05-16 16:08:31.396886: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1120] Creating TensorFlow device (/device:GPU:0) -> (device: 0, name: Tesla K80, pci bus id: 2fd7:00:00.0, compute capability: 3.7) 2019-05-16 16:08:36.076962: I tensorflow/stream_executor/dso_loader.cc:139] successfully opened CUDA library libcupti.so.8.0 locally Successfully downloaded train-images-idx3-ubyte.gz 9912422 bytes. Extracting /tmp/tensorflow/input_data/train-images-idx3-ubyte.gz Successfully downloaded train-labels-idx1-ubyte.gz 28881 bytes. Extracting /tmp/tensorflow/input_data/train-labels-idx1-ubyte.gz Successfully downloaded t10k-images-idx3-ubyte.gz 1648877 bytes. Extracting /tmp/tensorflow/input_data/t10k-images-idx3-ubyte.gz Successfully downloaded t10k-labels-idx1-ubyte.gz 4542 bytes. Extracting /tmp/tensorflow/input_data/t10k-labels-idx1-ubyte.gz Accuracy at step 0: 0.1081 Accuracy at step 10: 0.7457 Accuracy at step 20: 0.8233 Accuracy at step 30: 0.8644 Accuracy at step 40: 0.8848 Accuracy at step 50: 0.8889 Accuracy at step 60: 0.8898 Accuracy at step 70: 0.8979 Accuracy at step 80: 0.9087 Accuracy at step 90: 0.9099 Adding run metadata for 99 Accuracy at step 100: 0.9125 Accuracy at step 110: 0.9184 Accuracy at step 120: 0.922 Accuracy at step 130: 0.9161 Accuracy at step 140: 0.9219 Accuracy at step 150: 0.9151 Accuracy at step 160: 0.9199 Accuracy at step 170: 0.9305 Accuracy at step 180: 0.9251 Accuracy at step 190: 0.9258 Adding run metadata for 199 [...] Adding run metadata for 499`


## Upgrading a node pool

Whether you want to [update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) or [upgrade](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade) your node pools, you might notice that there is no `--gpu-driver`

parameter for either operation. You might run into an error like `unrecognized arguments: --gpu-driver none`

if you attempt to pass the parameter. There is no need to call on the parameter, as the value is not affected by any such operations.

When you first create your node pool, whatever parameter you declare for `--gpu-driver`

will not be impacted by upgrade/update operations. If you don't want any drivers to be installed, and selected `--gpu-driver None`

when creating your node pool, drivers will not be installed in any subsequent updates/upgrades.

## Clean up resources

Remove the associated Kubernetes objects you created in this article using the [ kubectl delete job](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#delete) command.

```
kubectl delete jobs samples-tf-mnist-demo
```


## Next steps

- To run Apache Spark jobs, see
[Run Apache Spark jobs on AKS](spark-job). - For more information on features of the Kubernetes scheduler, see
[Best practices for advanced scheduler features in AKS](operator-best-practices-advanced-scheduler). - For more information on Azure Kubernetes Service and Azure Machine Learning, see:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-nvidia-gpu -->

# Use GPUs for compute-intensive workloads on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Graphical processing units (GPUs) are often used for compute-intensive workloads, such as graphics and visualization workloads. AKS supports GPU-enabled Linux node pools to run compute-intensive Kubernetes workloads.

This article helps you provision nodes with schedulable GPUs on new and existing AKS clusters.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Supported GPU-enabled VMs

To view the available GPU-enabled VMs, see [GPU-optimized VM sizes in Azure](/en-us/azure/virtual-machines/sizes-gpu). If a GPU VM size is not in our list of supported VM sizes, AKS does not install the necessary GPU software components or provide support. AKS allows the use of unsupported GPU VM sizes after [skipping the automatic GPU driver installation](#skip-gpu-driver-installation).

Check available and supported VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm) command.

```
az vm list-skus --location <your-location> --output table
```


For AKS node pools, we recommend a minimum size of *Standard_NC6s_v3*. The NVv4 series (based on AMD GPUs) aren't supported on AKS.

Note

GPU-enabled VMs contain specialized hardware subject to higher pricing and region availability. For more information, see the [pricing](https://azure.microsoft.com/pricing/) tool and [region availability](https://azure.microsoft.com/global-infrastructure/services/).

## Limitations

- If you're using an Azure Linux GPU-enabled node pool, automatic security patches aren't applied. Refer to your current AKS API version for the default behavior of node OS upgrade channel.
[Flatcar Container Linux for AKS](flatcar-container-linux-for-aks)isn't supported with NVIDIA GPU on AKS.[Azure Linux with OS Guard for AKS](use-azure-linux-os-guard)isn't supported with NVIDIA GPU on AKS.

Note

For AKS API version 2023-06-01 or later, the default channel for node OS upgrade is *NodeImage*. For previous versions, the default channel is *None*. To learn more, see [auto-upgrade](auto-upgrade-node-image).

- Updating an existing node pool to add GPU VM size is not supported on AKS.

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the Azure CLI version 2.72.2 or later installed to set the
`--gpu-driver`

field. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you have the
`aks-preview`

Azure CLI extension installed, please update the version to 18.0.0b2 or later.

## Get the credentials for your cluster

Get the credentials for your AKS cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. The following example command gets the credentials for the

*myAKSCluster*in the

*myResourceGroup*resource group:

```
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```


## Options for using NVIDIA GPUs

Using NVIDIA GPUs involves the installation of various NVIDIA software components such as the [NVIDIA device plugin for Kubernetes](https://github.com/NVIDIA/k8s-device-plugin?tab=readme-ov-file), GPU driver installation, and more.

Note

By default, Microsoft automatically maintains the version of the NVIDIA drivers as part of the node image deployment, and AKS * supports and manages* it. While the NVIDIA drivers are installed by default on GPU capable nodes, you need to install the device plugin.

### NVIDIA device plugin installation

NVIDIA device plugin installation is required when using GPUs on AKS. In some cases, the installation is handled automatically, such as when using the [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html). Alternatively, you can manually install the NVIDIA device plugin.

#### Manually install the NVIDIA device plugin

You can deploy a DaemonSet for the NVIDIA device plugin, which runs a pod on each node to provide the required drivers for the GPUs. This is the recommended approach when using GPU-enabled node pools for Azure Linux.

To use the default OS SKU, you create the node pool without specifying an OS SKU. The node pool is configured for the default operating system based on the Kubernetes version of the cluster.

Add a node pool to your cluster using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name gpunp \
--node-count 1 \
--node-vm-size Standard_NC6s_v3 \
--node-taints sku=gpu:NoSchedule \
--enable-cluster-autoscaler \
--min-count 1 \
--max-count 3
```


This command adds a node pool named *gpunp* to *myAKSCluster* in *myResourceGroup* and uses parameters to configure the following node pool settings:

`--node-vm-size`

: Sets the VM size for the node in the node pool to*Standard_NC6s_v3*.`--node-taints`

: Specifies a*sku=gpu:NoSchedule*taint on the node pool.`--enable-cluster-autoscaler`

: Enables the cluster autoscaler.`--min-count`

: Configures the cluster autoscaler to maintain a minimum of one node in the node pool.`--max-count`

: Configures the cluster autoscaler to maintain a maximum of three nodes in the node pool.

Note

Taints and VM sizes can only be set for node pools during node pool creation, but you can update autoscaler settings at any time.

Create a namespace using the

command.`kubectl create namespace`

`kubectl create namespace gpu-resources`

Create a file named

*nvidia-device-plugin-ds.yaml*and paste the following YAML manifest provided as part of the[NVIDIA device plugin for Kubernetes project](https://github.com/NVIDIA/k8s-device-plugin/blob/4b3d6b0a6613a3672f71ea4719fd8633eaafb4f3/deployments/static/nvidia-device-plugin.yml):`apiVersion: apps/v1 kind: DaemonSet metadata: name: nvidia-device-plugin-daemonset namespace: gpu-resources spec: selector: matchLabels: name: nvidia-device-plugin-ds updateStrategy: type: RollingUpdate template: metadata: labels: name: nvidia-device-plugin-ds spec: tolerations: - key: "sku" operator: "Equal" value: "gpu" effect: "NoSchedule" # Mark this pod as a critical add-on; when enabled, the critical add-on # scheduler reserves resources for critical add-on pods so that they can # be rescheduled after a failure. # See https://kubernetes.io/docs/tasks/administer-cluster/guaranteed-scheduling-critical-addon-pods/ priorityClassName: "system-node-critical" containers: - image: nvcr.io/nvidia/k8s-device-plugin:v0.18.0 name: nvidia-device-plugin-ctr env: - name: FAIL_ON_INIT_ERROR value: "false" securityContext: allowPrivilegeEscalation: false capabilities: drop: ["ALL"] volumeMounts: - name: device-plugin mountPath: /var/lib/kubelet/device-plugins volumes: - name: device-plugin hostPath: path: /var/lib/kubelet/device-plugins`

Create the DaemonSet and confirm the NVIDIA device plugin is created successfully using the

command.`kubectl apply`

`kubectl apply -f nvidia-device-plugin-ds.yaml`

Now that you successfully installed the NVIDIA device plugin, you can check that your

[GPUs are schedulable](#confirm-that-gpus-are-schedulable)and[run a GPU workload](#run-a-gpu-enabled-workload).

### Skip GPU driver installation

If you want to control the installation of the NVIDIA drivers or use the [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html), you can skip the default GPU driver installation. Microsoft **doesn't support or manage** the maintenance and compatibility of the NVIDIA drivers as part of the node image deployment.

Important

Starting on **August 14, 2025**, Azure Kubernetes Service (AKS) no longer supports the `--skip-gpu-driver-install`

node pool tag. After this date, you'll be unable to provision GPU-enabled node pools using this tag to bypass automatic GPU driver installation. You can achieve the same behavior by setting the `--gpu-driver`

field to `none`

. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4925) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=496440). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Create a node pool using the

command and set`az aks nodepool add`

`--gpu-driver`

field to`none`

to skip default GPU driver installation.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --gpu-driver none \ --node-vm-size Standard_NC6s_v3 \ --enable-cluster-autoscaler \ --min-count 1 \ --max-count 3`

Setting the

`--gpu-driver`

API field to`none`

during node pool creation skips the automatic GPU driver installation. Any existing nodes aren't changed. You can scale the node pool to zero and then back up to make the change take effect.If you get the error

`unrecognized arguments: --gpu-driver none`

then[update the Azure CLI version](/en-us/cli/azure/update-azure-cli). For more information, see[Before you begin](#before-you-begin).You can optionally install the NVIDIA GPU Operator following

[these steps](nvidia-gpu-operator).

## Confirm that GPUs are schedulable

After creating your cluster, confirm that GPUs are schedulable in Kubernetes.

List the nodes in your cluster using the

command.`kubectl get nodes`

`kubectl get nodes`

Your output should look similar to the following example output:

`NAME STATUS ROLES AGE VERSION aks-gpunp-28993262-0 Ready agent 13m v1.20.7`

Confirm the GPUs are schedulable using the

command.`kubectl describe node`

`kubectl describe node aks-gpunp-28993262-0`

Under the

*Capacity*section, the GPU should list as`nvidia.com/gpu: 1`

. Your output should look similar to the following condensed example output:`Name: aks-gpunp-28993262-0 Roles: agent Labels: accelerator=nvidia [...] Capacity: [...] nvidia.com/gpu: 1 [...]`


## Run a GPU-enabled workload

To see the GPU in action, you can schedule a GPU-enabled workload with the appropriate resource request. In this example, we'll run a [Tensorflow](https://www.tensorflow.org/) job against the [MNIST dataset](http://yann.lecun.com/exdb/mnist/).

Create a file named

*samples-tf-mnist-demo.yaml*and paste the following YAML manifest, which includes a resource limit of`nvidia.com/gpu: 1`

:Note

If you receive a version mismatch error when calling into drivers, such as "CUDA driver version is insufficient for CUDA runtime version", review the

[NVIDIA driver matrix compatibility chart](https://docs.nvidia.com/deploy/cuda-compatibility/index.html).`apiVersion: batch/v1 kind: Job metadata: labels: app: samples-tf-mnist-demo name: samples-tf-mnist-demo spec: template: metadata: labels: app: samples-tf-mnist-demo spec: containers: - name: samples-tf-mnist-demo image: mcr.microsoft.com/azuredocs/samples-tf-mnist-demo:gpu args: ["--max_steps", "500"] imagePullPolicy: IfNotPresent resources: limits: nvidia.com/gpu: 1 restartPolicy: OnFailure tolerations: - key: "sku" operator: "Equal" value: "gpu" effect: "NoSchedule"`

Run the job using the

command, which parses the manifest file and creates the defined Kubernetes objects.`kubectl apply`

`kubectl apply -f samples-tf-mnist-demo.yaml`


## View the status of the GPU-enabled workload

Monitor the progress of the job using the

command with the`kubectl get jobs`

`--watch`

flag. It may take a few minutes to first pull the image and process the dataset.`kubectl get jobs samples-tf-mnist-demo --watch`

When the

*COMPLETIONS*column shows*1/1*, the job has successfully finished, as shown in the following example output:`NAME COMPLETIONS DURATION AGE samples-tf-mnist-demo 0/1 3m29s 3m29s samples-tf-mnist-demo 1/1 3m10s 3m36s`

Exit the

`kubectl --watch`

process with*Ctrl-C*.Get the name of the pod using the

command.`kubectl get pods`

`kubectl get pods --selector app=samples-tf-mnist-demo`

View the output of the GPU-enabled workload using the

command.`kubectl logs`

`kubectl logs samples-tf-mnist-demo-smnr6`

The following condensed example output of the pod logs confirms that the appropriate GPU device,

`Tesla K80`

, has been discovered:`2019-05-16 16:08:31.258328: I tensorflow/core/platform/cpu_feature_guard.cc:137] Your CPU supports instructions that this TensorFlow binary was not compiled to use: SSE4.1 SSE4.2 AVX AVX2 FMA 2019-05-16 16:08:31.396846: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1030] Found device 0 with properties: name: Tesla K80 major: 3 minor: 7 memoryClockRate(GHz): 0.8235 pciBusID: 2fd7:00:00.0 totalMemory: 11.17GiB freeMemory: 11.10GiB 2019-05-16 16:08:31.396886: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1120] Creating TensorFlow device (/device:GPU:0) -> (device: 0, name: Tesla K80, pci bus id: 2fd7:00:00.0, compute capability: 3.7) 2019-05-16 16:08:36.076962: I tensorflow/stream_executor/dso_loader.cc:139] successfully opened CUDA library libcupti.so.8.0 locally Successfully downloaded train-images-idx3-ubyte.gz 9912422 bytes. Extracting /tmp/tensorflow/input_data/train-images-idx3-ubyte.gz Successfully downloaded train-labels-idx1-ubyte.gz 28881 bytes. Extracting /tmp/tensorflow/input_data/train-labels-idx1-ubyte.gz Successfully downloaded t10k-images-idx3-ubyte.gz 1648877 bytes. Extracting /tmp/tensorflow/input_data/t10k-images-idx3-ubyte.gz Successfully downloaded t10k-labels-idx1-ubyte.gz 4542 bytes. Extracting /tmp/tensorflow/input_data/t10k-labels-idx1-ubyte.gz Accuracy at step 0: 0.1081 Accuracy at step 10: 0.7457 Accuracy at step 20: 0.8233 Accuracy at step 30: 0.8644 Accuracy at step 40: 0.8848 Accuracy at step 50: 0.8889 Accuracy at step 60: 0.8898 Accuracy at step 70: 0.8979 Accuracy at step 80: 0.9087 Accuracy at step 90: 0.9099 Adding run metadata for 99 Accuracy at step 100: 0.9125 Accuracy at step 110: 0.9184 Accuracy at step 120: 0.922 Accuracy at step 130: 0.9161 Accuracy at step 140: 0.9219 Accuracy at step 150: 0.9151 Accuracy at step 160: 0.9199 Accuracy at step 170: 0.9305 Accuracy at step 180: 0.9251 Accuracy at step 190: 0.9258 Adding run metadata for 199 [...] Adding run metadata for 499`


## Upgrading a node pool

Whether you want to [update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) or [upgrade](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade) your node pools, you might notice that there is no `--gpu-driver`

parameter for either operation. You might run into an error like `unrecognized arguments: --gpu-driver none`

if you attempt to pass the parameter. There is no need to call on the parameter, as the value is not affected by any such operations.

When you first create your node pool, whatever parameter you declare for `--gpu-driver`

will not be impacted by upgrade/update operations. If you don't want any drivers to be installed, and selected `--gpu-driver None`

when creating your node pool, drivers will not be installed in any subsequent updates/upgrades.

## Clean up resources

Remove the associated Kubernetes objects you created in this article using the [ kubectl delete job](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#delete) command.

```
kubectl delete jobs samples-tf-mnist-demo
```


## Next steps

- To run Apache Spark jobs, see
[Run Apache Spark jobs on AKS](spark-job). - For more information on features of the Kubernetes scheduler, see
[Best practices for advanced scheduler features in AKS](operator-best-practices-advanced-scheduler). - For more information on Azure Kubernetes Service and Azure Machine Learning, see:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-acr -->

# Tutorial - Create an Azure Container Registry (ACR) and build images

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Container Registry (ACR) is a private registry for container images. A private container registry allows you to securely build and deploy your applications and custom code.

In this tutorial, you deploy an ACR instance and push a container image to it. You learn how to:

- Create an ACR instance.
- Use
[ACR Tasks](/en-us/azure/container-registry/container-registry-tasks-overview)to build and push container images to ACR. - View images in your registry.

## Before you begin

In the [previous tutorial](tutorial-kubernetes-prepare-app), you used Docker to create a container image for a simple Azure Store Front application. If you haven't created the Azure Store Front app image, return to [Tutorial 1 - Prepare an application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.0.53 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create an Azure Container Registry

Before creating an ACR instance, you need a resource group. An Azure resource group is a logical container into which you deploy and manage Azure resources.

Important

This tutorial uses *myResourceGroup* as a placeholder for the resource group name. If you want to use a different name, replace *myResourceGroup* with your own resource group name.

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location westus2`

Create an ACR instance using the

command and provide your own unique registry name. The registry name must be unique within Azure and contain 5-50 lowercase alphanumeric characters. This tutorial series uses an environment variable,`az acr create`

`$ACRNAME`

, as a placeholder for the container registry name. You can set this environment variable to your unique ACR name to use in future commands. The*Basic*SKU is a cost-optimized entry point for development purposes that provides a balance of storage and throughput.`az acr create --resource-group myResourceGroup --name $ACRNAME --sku Basic`


## Build and push container images to registry

Build and push the images to your ACR using the Azure CLI

command.`az acr build`

Note

For this step, there isn't an equivalent Azure PowerShell cmdlet that performs this task.

In the following example, we don't build the

`product-service`

image. This image can take a long time to build, and there's a container image already available in the GitHub Container Registry (GHCR). You can use thecommand to import the image from the GHCR to your ACR instance. We also don't build the`az acr import`

`rabbitmq`

image. This image is available from the Docker Hub public repository and doesn't need to be built or pushed to your ACR instance.`az acr import --name $ACRNAME --source ghcr.io/azure-samples/aks-store-demo/product-service:latest --image aks-store-demo/product-service:latest az acr build --registry $ACRNAME --image aks-store-demo/order-service:latest ./src/order-service/ az acr build --registry $ACRNAME --image aks-store-demo/store-front:latest ./src/store-front/`


## List images in registry

View the images in your ACR instance using the

command.`az acr repository list`

`az acr repository list --name $ACRNAME --output table`

The following example output lists the available images in your registry:

`Result ---------------- aks-store-demo/product-service aks-store-demo/order-service aks-store-demo/store-front`


## Next steps

In this tutorial, you created an ACR and pushed images to it to use in an AKS cluster. You learned how to:

- Create an ACR instance.
- Use
[ACR Tasks](/en-us/azure/container-registry/container-registry-tasks-overview)to build and push container images to ACR. - View images in your registry.

In the next tutorial, you learn how to deploy a Kubernetes cluster in Azure.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-metrics-managed-prometheus -->

# Collect metrics for Istio service mesh add-on workloads for Azure Kubernetes Service in Azure Managed Prometheus

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This guide explains how to set up and use Azure Managed Prometheus to collect metrics from Istio service mesh add-on workloads on your Azure Kubernetes cluster.

## Prerequisites

Complete steps to enable the Istio add-on on the cluster as per

[documentation](istio-deploy-addon)

## Enable Azure Monitor managed service for Prometheus

Azure Monitor managed service for Prometheus collects data from Azure Kubernetes cluster.
To enable Azure Monitor managed service for Prometheus, you must create an [Azure Monitor workspace](/en-us/azure/azure-monitor/essentials/azure-monitor-workspace-manage?tabs=cli#create-an-azure-monitor-workspace) to store the metrics:

```
export AZURE_MONITOR_WORKSPACE=<azure-monitor-workspace-name>
export AZURE_MONITOR_WORKSPACE_ID=$(az monitor account create \
--name $AZURE_MONITOR_WORKSPACE \
--resource-group $RESOURCE_GROUP \
--location $LOCATION \
--query id -o tsv)
```


### Enable Prometheus addon

To collect Prometheus metrics from your Kubernetes cluster, [enable Prometheus addon](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable?tabs=cli#enable-with-cli):

```
az aks update --enable-azure-monitor-metrics --name $CLUSTER --resource-group $RESOURCE_GROUP --azure-monitor-workspace-resource-id $AZURE_MONITOR_WORKSPACE_ID
```


### Customize scraping of Prometheus metrics in Azure Monitor managed service

Create a scrape config in a file named `prometheus-config`

, similar to the sample provided below. This configuration enables pod annotation-based scraping, which allows Prometheus to automatically discover and scrape metrics from pods with specific annotations.

Important

The scrape config below is just an example. We **highly** recommend customizing it based on your needs. If not adjusted, it could lead to unexpected costs from frequent metric collection and increased data storage.

```
global:
scrape_interval: 30s
scrape_configs:
- job_name: workload
scheme: http
kubernetes_sd_configs:
- role: endpoints
relabel_configs:
- source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_scrape]
action: keep
regex: true
- source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_path]
action: replace
target_label: __metrics_path__
regex: (.+)
- source_labels: [__address__, __meta_kubernetes_pod_annotation_prometheus_io_port]
action: replace
regex: ([^:]+)(?::\d+)?;(\d+)
replacement: $1:$2
target_label: __address__
```


To [enable pod annotation-based scraping](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-configuration), create configmap `ama-metrics-prometheus-config`

that references `prometheus-config`

file in `kube-system`

namespace.

```
kubectl create configmap ama-metrics-prometheus-config --from-file=prometheus-config -n kube-system
```


### Verify Metric Collection

Configure access permissions: navigate to your Azure Monitor workspace in Azure portal and create role assignment for yourself to grant 'Monitoring Data Reader' role on the workspace resource.

Generate sample traffic: send a few requests to the product page created earlier, for example:

`curl -s "http://${GATEWAY_URL_EXTERNAL}/productpage" | grep -o "<title>.*</title>"`

View/Query metrics in Azure portal: navigate to Prometheus explorer under your Azure Monitor workspace and

[query metrics](/en-us/azure/azure-monitor/essentials/prometheus-workbooks). The example below shows results for query`istio_requests_total`

.

## Delete resources

If you want to clean up the Istio service mesh and the ingresses (leaving behind the cluster), run the following command:

```
az aks mesh disable --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up all the resources created from the Istio how-to guidance documents, run the following command:

```
az group delete --name ${RESOURCE_GROUP} --yes --no-wait
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-security-wireguard-encryption-concepts -->

# In transit encryption with WireGuard (public preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As organizations increasingly rely on Azure Kubernetes Service (AKS) to run containerized workloads, ensuring the security of network traffic between applications and services becomes essential especially in regulated or security-sensitive environments. In-transit encryption with WireGuard protects data as it moves between pods and nodes, mitigating risks of interception or tampering. WireGuard is known for its simplicity, and robust cryptography, offers a powerful solution for securing communication within AKS clusters.

WireGuard encryption for AKS is part of the [Advanced Container Networking Services (ACNS)](advanced-container-networking-services-overview) feature set, and its implementation is based on [Cilium](https://docs.cilium.io/en/stable/security/network/encryption-wireguard/).

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## WireGuard encryption scope

WireGuard in-transit encryption in AKS is designed to secure specific traffic flows within your Kubernetes cluster. This section outlines which traffic types are encrypted and which aren't currently supported via Advanced Container Networking Services(ACNS).

Supported/Encrypted traffic flows:

- Inter-node pod traffic: Traffic leaving a pod from one node destined to a pod on another node.

Unsupported/Unencrypted traffic flows

- Same-node pod traffic: Traffic between pods on the same node
- Node-network traffic: traffic generated by the node itself destined to another node

## Architecture overview

WireGuard encryption relies on [Azure CNI powered by cilium](azure-cni-powered-by-cilium) to secure inter-node communications within a distributed system. The architecture uses a dedicated WireGuard agent that orchestrates key management, interface configuration, and dynamic peer updates. This section attempts to provide a detailed explanation

### WireGuard agent

Upon startup, the Cilium agent evaluates its configuration to determine if encryption is enabled. When WireGuard is selected as the encryption mode, the agent initializes a dedicated WireGuard subsystem. The wireguard agent is responsible for configuring and initializing components required for enforcing WireGuard encryption.

### Key generation

A fundamental requirement to secure communication is the generation of cryptographic key pairs. Each node in the Kubernetes cluster will automatically generate a unique WireGuard key pair during the initialization phase and distributes its public key via the “network.cilium.io/wg-pub-key” annotation in the Kubernetes CiliumNode custom resource object. The key pairs are stored in memory and rotated every 120 seconds. The private key serves as the node’s confidential identity. The public key is shared with the peer nodes in the cluster to decrypt and encrypt traffic from and to Cilium-managed endpoints running on that node. These keys are managed entirely by Azure, not by the customer, ensuring secure and automated handling without requiring manual intervention. This mechanism ensures that only nodes with validated credentials can participate in the encrypted network.

### Interface creation

Once the key generation process concludes, the WireGuard agent configures a dedicated network interface (cilium_wg0). This process involves interface creation and configuration with the previously generated private key.

## Comparison with virtual network encryption

Azure offers multiple options for securing in-transit traffic in AKS, including [virtual network level encryption](/en-us/azure/virtual-network/virtual-network-encryption-overview) and WireGuard-based encryption. While both approaches enhance the confidentiality and integrity of network traffic, they differ in scope, flexibility, and deployment requirements. This section helps you understand when to use each solution.

**Use virtual network encryption when**

**You require full network-layer encryption for all traffic within the virtual network:**Virtual network encryption ensures that all traffic regardless of workload or orchestration layer is automatically encrypted as it traverses the Azure Virtual Network.**You need minimal performance overhead:**Virtual network encryption uses hardware acceleration in supported VM SKUs, offloading encryption from the OS to the underlying hardware. This design delivers high throughput with low CPU usage.**All your virtual machines support virtual network encryption:**Virtual network encryption depends on VM SKUs that support the necessary hardware acceleration. If your infrastructure consists entirely of supported SKUs, virtual network encryption can be seamlessly enabled.**Your AKS Network configurations supports virtual network encryption:**Virtual network encryption has some limitations when it comes to aks pod networking. For more information, see[Virtual network encryption supported scenarios](/en-us/azure/virtual-network/virtual-network-encryption-overview#supported-scenarios)

**Use WireGuard encryption When**

**You want to make sure that your application traffic is encrypted across all node**virtual network encryption does not encrypt traffic between nodes on the same physical host.**You want to unify encryption across multi-cloud or hybrid environments:**WireGuard offers a cloud-agnostic solution, enabling consistent encryption across clusters running in different cloud providers or on-premises.**You don’t need or want to encrypt all traffic within the virtual network:**WireGuard enables a more targeted encryption strategy ideal for securing sensitive workloads without incurring the overhead of encrypting all traffic.**Some of your VM SKUs don’t support virtual network encryption:**WireGuard is implemented in software and works regardless of VM hardware support, making it a practical option for heterogeneous environments.

## Considerations & limitations

• WireGuard isn't [FIPS](https://csrc.nist.gov/pubs/fips/140-2/upd2/final) compliant.
• WireGuard encryption doesn't apply to pods uses host networking (spec.hostNetwork: true) because these pods use the host identity instead of having individual identities.

Important

WireGuard encryption operates at the software level, which can introduce latency and impact throughput performance. The extent of this impact depends on various factors, including VM size (node SKU), network configuration, and application traffic patterns. Our benchmarking indicates that throughput is limited to 1.5 Gbps with an MTU of 1500; however, results may vary depending on workload characteristics and cluster configuration. Using a SKU that supports MTU 3900 resulted in approximately 2.5x higher throughput. While WireGuard encryption can be used alongside network policies, doing so may lead to further performance degradation, with reduced throughput and increased latency. For applications sensitive to latency or throughput, we strongly recommend evaluating WireGuard in a non-production environment first. As always, results may vary based on workload characteristics and cluster configuration.

## Pricing

Important

Advanced Container Networking Services is a paid offering. For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Next steps

Learn how to apply

[WireGuard encryption](how-to-apply-wireguard)on AKS.For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).Explore Container Network Observability features in Advanced Container Networking Services in

[What is Container Network Observability?](container-network-observability-metrics).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-resource-reservations -->

# Node resource reservations in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about node resource reservations in Azure Kubernetes Service (AKS).

## Resource reservations

AKS uses node resources to help the nodes function as part of the cluster. This usage can cause a discrepancy between the node's total resources and the allocatable resources in AKS.

AKS reserves two types of resources, **CPU** and **memory**, on each node to maintain node performance and functionality. As a node grows larger in resources, the resource reservations also grow due to a higher need for management of user-deployed pods. Keep in mind that you can't change resource reservations on a node.

### CPU reservations

Reserved CPU is dependent on node type and cluster configuration, which might result in less allocatable CPU due to running extra features. The following table shows CPU reservations in millicores:

| CPU cores on host | 1 core | 2 cores | 4 cores | 8 cores | 16 cores | 32 cores | 64 cores |
|---|---|---|---|---|---|---|---|
| Kube-reserved CPU (millicores) | 60 | 100 | 140 | 180 | 260 | 420 | 740 |

### Memory reservations

In AKS, reserved memory consists of the sum of two values:

**AKS 1.29 and later**

has the`kubelet`

daemon*memory.available < 100 Mi*eviction rule by default. This rule ensures that a node has at least 100 Mi allocatable at all times. When a host is below that available memory threshold, the`kubelet`

triggers the termination of one of the running pods and frees up memory on the host machine.**A rate of memory reservations**set according to the lesser value of:*20 MB * Max Pods supported on the Node + 50 MB*or*25% of the total system memory resources*.**Examples**:- If the virtual machine (VM) provides 8 GB of memory and the node supports up to 30 pods, AKS reserves
*20 MB * 30 Max Pods + 50 MB = 650 MB*for kube-reserved.`Allocatable space = 8 GB - 0.65 GB (kube-reserved) - 0.1 GB (eviction threshold) = 7.25 GB or 90.625% allocatable.`

- If the VM provides 4 GB of memory and the node supports up to 70 pods, AKS reserves
*25% * 4 GB = 1000 MB*for kube-reserved, as this is less than*20 MB * 70 Max Pods + 50 MB = 1450 MB*.

For more information, see

[Configure maximum pods per node in an AKS cluster](concepts-network-ip-address-planning#maximum-pods-per-node).- If the virtual machine (VM) provides 8 GB of memory and the node supports up to 30 pods, AKS reserves

**AKS versions prior to 1.29**

has the`kubelet`

daemon*memory.available < 750 Mi*eviction rule by default. This rule ensures that a node has at least 750 Mi allocatable at all times. When a host is below that available memory threshold, the`kubelet`

triggers the termination of one of the running pods and free up memory on the host machine.**A regressive rate of memory reservations**for the kubelet daemon to properly function (*kube-reserved*).- 25% of the first 4 GB of memory
- 20% of the next 4 GB of memory (up to 8 GB)
- 10% of the next 8 GB of memory (up to 16 GB)
- 6% of the next 112 GB of memory (up to 128 GB)
- 2% of any memory more than 128 GB


Note

AKS reserves an extra 2 GB for system processes in Windows nodes that isn't part of the calculated memory.

Memory and CPU allocation rules are designed to:

- Keep agent nodes healthy, including some hosting system pods critical to cluster health.
- Cause the node to report less allocatable memory and CPU than it would report if it weren't part of a Kubernetes cluster.

For example, if a node offers 7 GB, it reports 34% of memory not allocatable including the 750 Mi hard eviction threshold.

`0.75 + (0.25*4) + (0.20*3) = 0.75 GB + 1 GB + 0.6 GB = 2.35 GB / 7 GB = 33.57% reserved`


In addition to reservations for Kubernetes itself, the underlying node OS also reserves an amount of CPU and memory resources to maintain OS functions.

For associated best practices, see [Best practices for basic scheduler features in AKS](operator-best-practices-scheduler).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-diagnostics -->

# Azure Kubernetes Service Diagnose and Solve Problems overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Troubleshooting Azure Kubernetes Service (AKS) cluster issues plays an important role in maintaining your cluster, especially if your cluster is running mission-critical workloads. AKS Diagnose and Solve Problems is an intelligent, self-diagnostic experience that:

- Helps you identify and resolve problems in your cluster.
- Requires no extra configuration or billing cost.

## Open AKS Diagnose and Solve Problems

You can access AKS Diagnose and Solve Problems using the following steps:

In the

[Azure portal](https://portal.azure.com), navigate to your AKS cluster resource.From the service menu, select

**Diagnose and solve problems**.Select a troubleshooting category tile that best describes the issue of your cluster by referring the keywords in each tile description on the homepage or typing a keyword that best describes your issue in the search bar.


## View a diagnostic report

After selecting a category, you can view various diagnostic reports that provide detailed information about the issue. The *Overview* option from the navigation menu runs all the diagnostics in that particular category and displays any issues that are found with the cluster. Select **View details** under each tile to view a detailed description of the issue, including:

- An issue summary
- Error details
- Recommended actions
- Links to helpful docs
- Related-metrics
- Logging data

### Example scenario: Diagnose connectivity issues

I observed that my application is getting disconnected or experiencing intermittent connection issues. In response, I navigate to the AKS Diagnose and Solve Problems home page and select the **Connectivity Issues** tile to investigate the potential causes.

I received a diagnostic alert indicating that the disconnection might be related to my *Cluster DNS*. To gather more information, I select **View details**.

Based on the diagnostic result, it appears that the issue might be related to known DNS issues or the VNet configuration. I can use the documentation links provided to address the issue and resolve the problem.

If the recommended documentation based on the diagnostic results doesn't resolve the issue, I can return to the previous step in Diagnostics and refer to additional documentation.

## Use AKS Diagnose and Solve Problems for best practices

Deploying applications on AKS requires adherence to best practices to guarantee optimal performance, availability, and security. The AKS Diagnose and Solve Problems **Best Practices** tile provides an array of best practices that can assist in managing various aspects, such as VM resource provisioning, cluster upgrades, scaling operations, subnet configuration, and other essential aspects of a cluster's configuration.

Leveraging the AKS Diagnose and Solve Problems can be vital in ensuring that your cluster adheres to best practices and that any potential issues are identified and resolved in a timely and effective manner. By incorporating AKS Diagnose and Solve Problems into your operational practices, you can be confident in the reliability and security of your application in production.

### Example scenario: View best practices

I'm curious about the best practices I can follow to prevent potential problems. In response, I navigate to the AKS Diagnose and Solve Problems home page and select the **Best Practices** tile.

From here, I can view the best practices that are recommended for my cluster and select **View details** to see the results.

## Next steps

- Collect logs to help you further troubleshoot your cluster issues using
[AKS Periscope](https://aka.ms/aksperiscope). - Read the
[triage practices section](/en-us/azure/architecture/operator-guides/aks/aks-triage-practices)of the AKS day-2 operations guide. - Post your questions or feedback at
[UserVoice](https://feedback.azure.com/d365community/forum/aabe212a-f724-ec11-b6e6-000d3a4f0da0). Make sure to add "[Diag]" in the title.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-problem-detector -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-cni -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kubernetes-action -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-extension-vs-code -->

# Use the Azure Kubernetes Service (AKS) extension for Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Kubernetes Service (AKS) extension for Visual Studio Code allows you to easily view and manage your AKS clusters from your development environment.

## Features

The Azure Kubernetes Service (AKS) extension for Visual Studio Code provides a rich set of features to help you manage your AKS clusters, including:

**Merge into Kubeconfig**: Merge your AKS cluster into your`kubeconfig`

file to manage your cluster from the command line.**Save Kubeconfig**: Save your AKS cluster configuration to a file.**AKS Diagnostics**: View diagnostics information based on your cluster's backend telemetry for identity, security, networking, node health, and create, upgrade, delete, and scale issues.**AKS Periscope**: Extract detailed diagnostic information and export it to an Azure storage account for further analysis.**Install Azure Service Operator (ASO)**: Deploy the latest version of ASO and provision Azure resources within Kubernetes.**Start or stop a cluster**: Start or stop your AKS cluster to save costs when you're not using it.

For more information, see [AKS extension for Visual Studio Code features](https://code.visualstudio.com/docs/azure/aksextensions#_features).

## Installation

- Open Visual Studio Code.
- In the
**Extensions**view, search for**Azure Kubernetes Service**. - Select the
**Azure Kubernetes Service**extension and then select**Install**.

For more information, see [Install the AKS extension for Visual Studio Code](https://code.visualstudio.com/docs/azure/aksextensions#_install-the-azure-kubernetes-services-extension).

## Next steps

To learn more about other AKS add-ons and extensions, see [Add-ons, extensions, and other integrations with AKS](integrations).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/troubleshooting -->

# Azure Kubernetes Service (AKS) troubleshooting documentation

Welcome to Azure Kubernetes Service troubleshooting. These articles explain how to determine, diagnose, and fix issues that you might encounter when you use Azure Kubernetes Service (AKS). In the navigation pane on the left, browse through the article list or use the search box to find issues and solutions.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks -->

# Azure Kubernetes Service (AKS)

AKS allows you to quickly deploy a production ready Kubernetes cluster in Azure. Learn how to use AKS with these quickstarts, tutorials, and samples.

This browser is no longer supported.

Upgrade to Microsoft Edge to take advantage of the latest features, security updates, and technical support.

AKS allows you to quickly deploy a production ready Kubernetes cluster in Azure. Learn how to use AKS with these quickstarts, tutorials, and samples.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-latency -->

# Latency comparison across versions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This document elaborates on the [data plane latency performance](istio-scale#data-plane-performance) across Istio add-on versions and Kubernetes version. The results evaluate the impact of adding sidecar proxies to the data path, showcasing the P90 and P99 latency difference. The comparison measures the difference between traffic routed through the sidecar and traffic sent directly to the pod.

- Traffic going through the sidecar: client --> client-sidecar --> server-sidecar --> server
- Traffic directly going to the pod: client --> server

## Test specifications

- Node SKU: Standard D16 v5 (16 vCPU, 64-GB memory)
- Two proxy workers
- 1-KB payload
- 1,000 Queries per second (QPS) at varying client connections
`http/1.1`

protocol and mutual Transport Layer Security (TLS) enabled

| P99 Latency Difference | P90 Latency Difference |
|---|---|
|

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/troubleshoot-source-network-address-translation -->

# Troubleshoot SNAT port exhaustion for a Standard Load Balancer in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If you know that you're starting many outbound TCP or UDP connections to the same destination IP address and port, and you observe failing outbound connections or support notifies you that you're exhausting SNAT ports, you have several general mitigation options. Review these options and decide what's best for your scenario. It's possible that one or more can help manage your scenario. For detailed information, review the [outbound connections troubleshooting guide](/en-us/azure/load-balancer/troubleshoot-outbound-connection).

The root cause of SNAT exhaustion is frequently an anti-pattern for how outbound connectivity is established, managed, or configurable timers changed from their default values.

This article helps you troubleshoot SNAT port exhaustion issues when using a Standard Load Balancer in Azure Kubernetes Service (AKS).

## Steps to troubleshoot SNAT port exhaustion

Use the following steps to troubleshoot SNAT port exhaustion:

- Check if your connections remain idle for a long time and rely on the default idle timeout for releasing that port. If so, the default timeout of 30 minutes might need to be reduced for your scenario.
- Investigate how your application creates outbound connectivity (for example: code review or packet capture).
- Determine if this activity is expected behavior or whether the application is misbehaving. Use
[metrics](/en-us/azure/load-balancer/load-balancer-standard-diagnostics)and[logs](/en-us/azure/load-balancer/monitor-load-balancer)in Azure Monitor to substantiate your findings. For example, use the "Failed" category for SNAT connections metric. - Evaluate if appropriate
[design patterns](#snat-port-exhaustion-design-patterns)are followed. - Evaluate if SNAT port exhaustion should be mitigated with
[more outbound IP addresses and allocated outbound ports](configure-load-balancer-standard#configure-the-allocated-outbound-ports).

## SNAT port exhaustion design patterns

Take advantage of connection reuse and connection pooling whenever possible. These patterns help you avoid resource exhaustion problems and result in predictable behavior.

- Atomic requests (one request per connection) generally aren't a good design choice. Such anti-patterns limit scale, reduce performance, and decrease reliability. Instead, reuse HTTP/S connections to reduce the numbers of connections and associated SNAT ports. The application scale increases and performance improves because of reduced handshakes, overhead, and cryptographic operation cost when using TLS.
- If you're using out of cluster/custom DNS, or custom upstream servers on coreDNS, keep in mind that DNS can introduce many individual flows at volume when the client isn't caching the DNS resolvers result. Make sure to customize coreDNS first instead of using custom DNS servers and to define a good caching value.
- UDP flows (for example, DNS lookups) allocate SNAT ports during the idle timeout. The longer the idle timeout, the higher the pressure on SNAT ports. Use short idle timeout (for example, 4 minutes).
- Use connection pools to shape your connection volume.
- Never silently abandon a TCP flow and rely on TCP timers to clean up flow. If you don't let TCP explicitly close the connection, state remains allocated at intermediate systems and endpoints, and it makes SNAT ports unavailable for other connections. This pattern can trigger application failures and SNAT exhaustion.
- Don't change OS-level TCP close related timer values without expert knowledge of impact. While the TCP stack recovers, your application performance can be negatively affected when the endpoints of a connection have mismatched expectations. Wishing to change timers is usually a sign of an underlying design problem. Review following recommendations.

## Next steps

To learn more about AKS Standard Load Balancer configuration options, see [Configure your public standard load balancer in AKS](configure-load-balancer-standard).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-enable-ebpf-host-routing -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/gpu-multi-instance -->

# Create a multi-instance GPU node pool in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Certain NVIDIA GPUs can be divided in up to seven independent instances. Each instance has its own Stream Multiprocessor (SM), which is responsible for executing instructions in parallel, and GPU memory. For more information on GPU partitioning, see [NVIDIA MIG](https://www.nvidia.com/en-us/technologies/multi-instance-gpu/).

This article walks you through how to create a multi-instance GPU node pool using a MIG-compatible VM size in an Azure Kubernetes Service (AKS) cluster.

## Prerequisites and limitations

- An Azure account with an active subscription. If you don't have one, you can
[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - Azure CLI version 2.2.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - The Kubernetes command-line client,
[kubectl](https://kubernetes.io/docs/reference/kubectl/), installed and configured. If you use Azure Cloud Shell,`kubectl`

is already installed. If you want to install it locally, you can use thecommand.`az aks install-cli`

- Helm v3 installed and configured. For more information, see
[Installing Helm](https://helm.sh/docs/intro/install/). - Multi-instance GPU is currently supported on the
`Standard_NC40ads_H100_v5`

,`Standard_ND96isr_H100_v5`

, and A100 GPU VM sizes on AKS.

## GPU instance profiles

GPU instance profiles define how GPUs are partitioned. The following table shows the available GPU instance profile for the `Standard_ND96asr_v4`

:

| Profile name | Fraction of SM | Fraction of memory | Number of instances created |
|---|---|---|---|
| MIG 1g.5gb | 1/7 | 1/8 | 7 |
| MIG 2g.10gb | 2/7 | 2/8 | 3 |
| MIG 3g.20gb | 3/7 | 4/8 | 2 |
| MIG 4g.20gb | 4/7 | 4/8 | 1 |
| MIG 7g.40gb | 7/7 | 8/8 | 1 |

As an example, the GPU instance profile of `MIG 1g.5gb`

indicates that each GPU instance has 1g SM (streaming multiprocessors) and 5gb memory. In this case, the GPU is partitioned into seven instances.

The available GPU instance profiles available for this VM size include `MIG1g`

, `MIG2g`

, `MIG3g`

, `MIG4g`

, and `MIG7g`

.

Important

You can't change the applied GPU instance profile after node pool creation.

## Create an AKS cluster

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location southcentralus`

Create an AKS cluster using the

command.`az aks create`

`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --generate-ssh-keys`

Configure

`kubectl`

to connect to your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Create a multi-instance GPU node pool

You can use either the Azure CLI or an HTTP request to the ARM API to create the node pool.

Create a multi-instance GPU node pool using the

command and specify the GPU instance profile. The example below creates a node pool with the`az aks nodepool add`

`Standard_ND96asr_v4`

MIG-compatible GPU VM size.`az aks nodepool add \ --name aksMigNode \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --node-vm-size Standard_ND96asr_v4 \ --node-count 1 \ --gpu-instance-profile MIG1g`


## Determine multi-instance GPU (MIG) strategy

Before you install the NVIDIA plugins, you need to specify which multi-instance GPU (MIG) strategy to use for GPU partitioning: *Single strategy* or *Mixed strategy*. The two strategies don't affect how you execute CPU workloads, but how GPU resources are displayed.

**Single strategy**: The single strategy treats every GPU instance as a GPU. If you use this strategy, the GPU resources are displayed as`nvidia.com/gpu: 1`

.**Mixed strategy**: The mixed strategy exposes the GPU instances and the GPU instance profile. If you use this strategy, the GPU resource are displayed as`nvidia.com/mig1g.5gb: 1`

.

## Install the NVIDIA device plugin and GPU feature discovery (GFD) components

Set your MIG strategy as an environment variable. You can use either single or mixed strategy.

`# Single strategy export MIG_STRATEGY=single # Mixed strategy export MIG_STRATEGY=mixed`

Add the NVIDIA device plugin helm repository using the

`helm repo add`

and`helm repo update`

commands.`helm repo add nvdp https://nvidia.github.io/k8s-device-plugin helm repo update`

Install the NVIDIA device plugin using the

`helm install`

command.`helm install nvdp nvdp/nvidia-device-plugin \ --version=0.17.0 \ --set migStrategy=${MIG_STRATEGY} \ --set gfd.enabled=true \ --namespace nvidia-device-plugin \ --create-namespace`


Note

Helm installation of the NVIDIA device plugin consolidates the Kubernetes device plugin and GFD repositories. Separate helm installation of the GFD software component is not recommended when using AKS-managed multi-instance GPU.

## Confirm multi-instance GPU capability

Verify the

`kubectl`

connection to your cluster using the`kubectl get`

command to return a list of cluster nodes.`kubectl get nodes -o wide`

Confirm the node has multi-instance GPU capability using the

`kubectl describe node`

command. The following example command describes the node named*aksMigNode*, which uses MIG1g as the GPU instance profile.`kubectl describe node aksMigNode`

Your output should resemble the following example output:

`# Single strategy output Allocatable: nvidia.com/gpu: 56 # Mixed strategy output Allocatable: nvidia.com/mig-1g.5gb: 56`


## Schedule work

The following examples are based on CUDA base image **version 12.1.1** for Ubuntu **22.04**, tagged as `12.1.1-base-ubuntu22.04`

.

### Single strategy

Create a file named

`single-strategy-example.yaml`

and copy in the following manifest.`apiVersion: v1 kind: Pod metadata: name: nvidia-single spec: containers: - name: nvidia-single image: nvidia/cuda:12.1.1-base-ubuntu22.04 command: ["/bin/sh"] args: ["-c","sleep 1000"] resources: limits: "nvidia.com/gpu": 1`

Deploy the application using the

`kubectl apply`

command and specify the name of your YAML manifest.`kubectl apply -f single-strategy-example.yaml`

Verify the allocated GPU devices using the

`kubectl exec`

command. This command returns a list of the cluster nodes.`kubectl exec nvidia-single -- nvidia-smi -L`

The following example resembles output showing successfully created deployments and services:

`GPU 0: NVIDIA A100 40GB PCIe (UUID: GPU-48aeb943-9458-4282-da24-e5f49e0db44b) MIG 1g.5gb Device 0: (UUID: MIG-fb42055e-9e53-5764-9278-438605a3014c) MIG 1g.5gb Device 1: (UUID: MIG-3d4db13e-c42d-5555-98f4-8b50389791bc) MIG 1g.5gb Device 2: (UUID: MIG-de819d17-9382-56a2-b9ca-aec36c88014f) MIG 1g.5gb Device 3: (UUID: MIG-50ab4b32-92db-5567-bf6d-fac646fe29f2) MIG 1g.5gb Device 4: (UUID: MIG-7b6b1b6e-5101-58a4-b5f5-21563789e62e) MIG 1g.5gb Device 5: (UUID: MIG-14549027-dd49-5cc0-bca4-55e67011bd85) MIG 1g.5gb Device 6: (UUID: MIG-37e055e8-8890-567f-a646-ebf9fde3ce7a)`


### Mixed strategy

Create a file named

`mixed-strategy-example.yaml`

and copy in the following manifest.`apiVersion: v1 kind: Pod metadata: name: nvidia-mixed spec: containers: - name: nvidia-mixed image: nvidia/cuda:12.1.1-base-ubuntu22.04 command: ["/bin/sh"] args: ["-c","sleep 100"] resources: limits: "nvidia.com/mig-1g.5gb": 1`

Deploy the application using the

`kubectl apply`

command and specify the name of your YAML manifest.`kubectl apply -f mixed-strategy-example.yaml`

Verify the allocated GPU devices using the

`kubectl exec`

command. This command returns a list of the cluster nodes.`kubectl exec nvidia-mixed -- nvidia-smi -L`

The following example resembles output showing successfully created deployments and services:

`GPU 0: NVIDIA A100 40GB PCIe (UUID: GPU-48aeb943-9458-4282-da24-e5f49e0db44b) MIG 1g.5gb Device 0: (UUID: MIG-fb42055e-9e53-5764-9278-438605a3014c)`


Important

The `latest`

tag for CUDA images has been deprecated on Docker Hub. Please refer to [NVIDIA's repository](https://hub.docker.com/r/nvidia/cuda/tags) for the latest images and corresponding tags.

## Troubleshooting

If you don't see multi-instance GPU capability after creating the node pool, confirm the API version isn't older than *2021-08-01*.

## Next steps

To learn more about GPUs on Azure Kubernetes Service, see:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/active-active-solution -->

# Recommended active-active high availability solution overview for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create an application in Azure Kubernetes Service (AKS) and choose an Azure region during resource creation, it's a single-region app. In the event of a disaster that causes the region to become unavailable, your application also becomes unavailable. If you create an identical deployment in a secondary Azure region, your application becomes less susceptible to a single-region disaster, which guarantees business continuity, and any data replication across the regions lets you recover your last application state.

While there are multiple patterns that can provide recoverability for an AKS solution, this guide outlines the recommended active-active high availability solution for AKS. Within this solution, we deploy two independent and identical AKS clusters into two paired Azure regions with both clusters actively serving traffic.

Note

The following use case can be considered standard practice within AKS. It has been reviewed internally and vetted in conjunction with our Microsoft partners.

## Active-active high availability solution overview

This solution relies on two identical AKS clusters configured to actively serve traffic. You place a global traffic manager, such as [Azure Front Door](/en-us/azure/frontdoor/front-door-overview), in front of the two clusters to distribute traffic across them. You must consistently configure the clusters to host an instance of all applications required for the solution to function.

Availability zones are another way to ensure high availability and fault tolerance for your AKS cluster within the same region. Availability zones allow you to distribute your cluster nodes across multiple isolated locations within an Azure region. This way, if one zone goes down due to a power outage, hardware failure, or network issue, your cluster can continue to run and serve your applications. Availability zones also improve the performance and scalability of your cluster by reducing the latency and contention among nodes. To set up availability zones for your AKS cluster, you need to specify the zone numbers when creating or updating your node pools. For more information, see [What are Azure availability zones?](/en-us/azure/reliability/availability-zones-overview)

Note

Many regions support availability zones. Consider using regions with availability zones to provide more resiliency and availability for your workloads. For more information, see [Recover from a region-wide service disruption](/en-us/azure/architecture/resiliency/recovery-loss-azure-region).

## Scenarios and configurations

This solution is best implemented when hosting stateless applications and/or with other technologies also deployed across both regions, such as horizontal scaling. In scenarios where the hosted application is reliant on resources, such as databases, that are actively in only one region, we recommend instead implementing an [active-passive solution](active-passive-solution) for potential cost savings, as active-passive has more downtime than active-active.

## Components

The active-active high availability solution uses many Azure services. This section covers only the components unique to this multi-cluster architecture. For more information on the remaining components, see the [AKS baseline architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=%2Fazure%2Faks%2Ftoc.json&bc=%2Fazure%2Faks%2Fbreadcrumb%2Ftoc.json).

**Multiple clusters and regions**: You deploy multiple AKS clusters, each in a separate Azure region. During normal operations, your Azure Front Door configuration routes network traffic between all regions. If one region becomes unavailable, traffic routes to a region with the fastest load time for the user.

**Hub-spoke network per region**: A regional hub-spoke network pair is deployed for each regional AKS instance. [Azure Firewall Manager](/en-us/azure/firewall-manager/overview) policies manage the firewall policies across all regions.

**Regional key store**: You provision [Azure Key Vault](/en-us/azure/key-vault/general/overview) in each region to store sensitive values and keys specific to the AKS instance and to support services found in that region.

**Azure Front Door**: [Azure Front Door](/en-us/azure/frontdoor/front-door-overview) load balances and routes traffic to a regional [Azure Application Gateway](/en-us/azure/application-gateway/overview) instance, which sits in front of each AKS cluster. Azure Front Door allows for *layer seven* global routing.

**Log Analytics**: Regional [Log Analytics](/en-us/azure/azure-monitor/logs/log-analytics-overview) instances store regional networking metrics and diagnostic logs. A shared instance stores metrics and diagnostic logs for all AKS instances.

**Container Registry**: The container images for the workload are stored in a managed container registry. With this solution, a single [Azure Container Registry](/en-us/azure/container-registry/container-registry-intro) instance is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables you to replicate images to the selected Azure regions and provides continued access to images even if a region experiences an outage.

## Failover process

If a service or service component becomes unavailable in one region, traffic should be routed to a region where that service is available. A multi-region architecture includes many different failure points. In this section, we cover the potential failure points.

### Application Pods (Regional)

A Kubernetes deployment object creates multiple replicas of a pod (*ReplicaSet*). If one is unavailable, traffic is routed between the remaining replicas. The Kubernetes *ReplicaSet* attempts to keep the specified number of replicas up and running. If one instance goes down, a new instance should be recreated. [Liveness probes](/en-us/azure/container-instances/container-instances-liveness-probe) can check the state of the application or process running in the pod. If the pod is unresponsive, the liveness probe removes the pod, which forces the *ReplicaSet* to create a new instance.

For more information, see [Kubernetes ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/).

### Application Pods (Global)

When an entire region becomes unavailable, the pods in the cluster are no longer available to serve requests. In this case, the Azure Front Door instance routes all traffic to the remaining health regions. The Kubernetes clusters and pods in these regions continue to serve requests. To compensate for increased traffic and requests to the remaining cluster, keep in mind the following guidance:

- Make sure network and compute resources are right sized to absorb any sudden increase in traffic due to region failover. For example, when using Azure Container Network Interface (CNI), make sure you have a subnet that can support all pod IPs with a spiked traffic load.
- Use the
[Horizontal Pod Autoscaler](concepts-scale#horizontal-pod-autoscaler)to increase the pod replica count to compensate for the increased regional demand. - Use the AKS
[Cluster Autoscaler](cluster-autoscaler)to increase the Kubernetes instance node counts to compensate for the increased regional demand.

### Kubernetes node pools (Regional)

Occasionally, localized failure can occur to compute resources, such as power becoming unavailable in a single rack of Azure servers. To protect your AKS nodes from becoming a single point regional failure, use [Azure Availability Zones](availability-zones). Availability zones ensure that AKS nodes in each availability zone are physically separated from those defined in another availability zones.

### Kubernetes node pools (Global)

In a complete regional failure, Azure Front Door routes traffic to the remaining healthy regions. Again, make sure to compensate for increased traffic and requests to the remaining cluster.

## Failover testing strategy

While there are no mechanisms currently available within AKS to take down an entire region of deployment for testing purposes, [Azure Chaos Studio](/en-us/azure/chaos-studio/chaos-studio-overview) offers the ability to create a chaos experiment on your cluster.

## Next steps

If you're considering a different solution, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network -->

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

Important

Starting on **March 31, 2026**, Azure Kubernetes Service (AKS) no longer supports default outbound access for virtual machines (VMs). New AKS clusters that use the **AKS-managed virtual network** option will place cluster subnets into [private subnets](/en-us/azure/virtual-network/ip-services/default-outbound-access#why-is-disabling-default-outbound-access-recommended) by default (`defaultOutboundAccess = false`

). This setting **doesn't impact AKS-managed cluster traffic**, which uses explicitly configured outbound paths. It might affect **unsupported scenarios**, such as deploying other resources into the same subnet. Clusters using **BYO VNets are unaffected** by this change. In supported configurations, no action is required. For more information on this retirement, see the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=default-outbound-access-for-vms-in-azure-will-be-retired-transition-to-a-new-method-of-internet-access). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/access-private-cluster -->

# Access a private Azure Kubernetes Service (AKS) cluster using the command invoke or Run command feature

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you access a private Azure Kubernetes Service (AKS) cluster, you need to connect to the cluster from the cluster virtual network (VNet), a peered network, or a configured private endpoint. These approaches require extra configuration, such as setting up a VPN or Express Route.

With the Azure CLI, you can use `command invoke`

to access private clusters without the need to configure a VPN or Express Route. `command invoke`

allows you to remotely invoke commands, like `kubectl`

and `helm`

, on your private cluster through the Azure API without directly connecting to the cluster. The RBAC actions `Microsoft.ContainerService/managedClusters/runcommand/action`

and `Microsoft.ContainerService/managedClusters/commandResults/read`

control the permissions for using `command invoke`

.

With the Azure portal, you can use the `Run command`

feature to run commands on your private cluster. The `Run command`

feature uses the same `command invoke`

functionality to run commands on your cluster. The pod created by `Run command`

provides `kubectl`

and `helm`

for operating your cluster. `jq`

, `xargs`

, `grep`

, and `awk`

are available for Bash support.

Tip

You can use Azure Copilot to run `kubectl`

commands in the Azure portal. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#run-cluster-commands).

## Prerequisites

**System and permission requirements**

| Requirement type | Specification | How to verify |
|---|---|---|
Azure CLI version |
2.24.0 or later | Use the
`az --version` |

**Private AKS cluster**[Create a private AKS cluster](private-clusters).**RBAC actions**`Microsoft.ContainerService/managedClusters/runcommand/action`

and `Microsoft.ContainerService/managedClusters/commandResults/read`

[Azure CLI command.](/en-us/cli/azure/role/assignment#az-role-assignment-list)`az role assignment list`

**Run command pod resource specifications**

| Resource type | Value | Impact |
|---|---|---|
CPU requests |
200m | Minimum CPU reserved for command pod |
Memory requests |
500Mi | Minimum memory reserved for command pod |
CPU limits |
500m | Maximum CPU available to command pod |
Memory limits |
1Gi | Maximum memory available to command pod |
Azure Resource Manager (ARM) API timeout |
60 seconds | Maximum time for pod scheduling |
Output size limit |
512kB | Maximum command output size |

## Limitations and considerations

**Design scope**

**Not for programmatic access**: Use Bastion, VPN, or ExpressRoute for automated API calls.**Pod scheduling dependency**: Requires sufficient cluster resources (see the[resource specifications](#prerequisites)).**Output limitations**:*exitCode*and*text*only, no API-level details.**Network constraints apply**: Subject to cluster networking and security restrictions.

**Potential failure points**

- Pod scheduling failure if nodes are resource-constrained.
- ARM API timeout (60 seconds) if pod can't be scheduled quickly.
- Output truncation if response exceeds 512kB limit.

## Use `command invoke`

on a private AKS cluster with the Azure CLI

Set environment variables for your resource group and cluster name to use in subsequent commands.

`export AKS_RESOURCE_GROUP="<resource-group-name>" export AKS_CLUSTER_NAME="<cluster-name>"`

These environment variables allow you to run AKS commands without having to rewrite their names.


### Use `command invoke`

to run a single command

Run a single command on your cluster using the

command and the`az aks command invoke`

`--command`

parameter to specify the command to run. The following example gets the pods in the`kube-system`

namespace.`az aks command invoke \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER_NAME \ --command "kubectl get pods -n kube-system"`


### Use `command invoke`

to run multiple commands

Run multiple commands on your cluster using the

command and the`az aks command invoke`

`--command`

parameter to specify the commands to run. The following example adds the Bitnami Helm chart repository, updates the repository, and installs the`nginx`

chart.`az aks command invoke \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER_NAME \ --command "helm repo add bitnami https://charts.bitnami.com/bitnami && helm repo update && helm install my-release bitnami/nginx"`


### Use `command invoke`

to run commands with an attached file

If you want to run a command with an attached file, the file must exist and be accessible in your current working directory. In the following example, we create a minimal deployment file for demonstration.

Create a Kubernetes manifest file named

`deployment.yaml`

. The following example deployment file deploys an`nginx`

pod.`cat <<EOF > deployment.yaml apiVersion: apps/v1 kind: Deployment metadata: name: nginx-demo spec: replicas: 1 selector: matchLabels: app: nginx-demo template: metadata: labels: app: nginx-demo spec: containers: - name: nginx image: nginx:1.21.6 ports: - containerPort: 80 EOF`

Apply the deployment file to your cluster using the

command with the`az aks command invoke`

`--file`

parameter to attach the file. The following example applies the`deployment.yaml`

file to the`default`

namespace.`az aks command invoke \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER_NAME \ --command "kubectl apply -f deployment.yaml -n default" \ --file deployment.yaml`


### Use `command invoke`

to run commands with all files in the current directory

Note

Use only small, necessary files to avoid exceeding system size limits.

In the following example, we create two minimal deployment files for demonstration.

Create two Kubernetes manifest files named

`deployment.yaml`

and`configmap.yaml`

. The following example deployment files deploy an`nginx`

pod and create a ConfigMap with a welcome message.`cat <<EOF > deployment.yaml apiVersion: apps/v1 kind: Deployment metadata: name: nginx-demo spec: replicas: 1 selector: matchLabels: app: nginx-demo template: metadata: labels: app: nginx-demo spec: containers: - name: nginx image: nginx:1.21.6 ports: - containerPort: 80 EOF cat <<EOF > configmap.yaml apiVersion: v1 kind: ConfigMap metadata: name: nginx-config data: welcome-message: "Hello from configmap" EOF`

Apply the deployment files to your cluster using the

command with the`az aks command invoke`

`--file`

parameter to attach the file. The following example applies the`deployment.yaml`

and`configmap.yaml`

files to the`default`

namespace.`az aks command invoke \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER_NAME \ --command "kubectl apply -f deployment.yaml -f configmap.yaml -n default" \ --file deployment.yaml \ --file configmap.yaml`


## Use `Run command`

on a private AKS cluster in the Azure portal

You can use the following `kubectl`

commands with the `Run command`

feature:

`kubectl get nodes`

`kubectl get deployments`

`kubectl get pods`

`kubectl describe nodes`

`kubectl describe pod <pod-name>`

`kubectl describe deployment <deployment-name>`

`kubectl apply -f <file-name>`


### Use `Run command`

to run a single command

- In the Azure portal, navigate to your private cluster.
- From the service menu, under
**Kubernetes resources**, select**Run command**. - Enter the command you want to run and select
**Run**.

### Use `Run command`

to run commands with attached files

In the Azure portal, navigate to your private cluster.

From the service menu, under

**Kubernetes resources**, select**Run command**.Select

**Attach files**>**Browse for files**.Select the file or files you want to attach, and then select

**Attach**.Enter the command you want to run and select

**Run**.

## Disable `Run command`


You can disable the `Run command`

feature by setting [ .properties.apiServerAccessProfile.disableRunCommand to true](/en-us/rest/api/aks/managed-clusters/create-or-update).


## Troubleshoot `command invoke`

issues

For information on the most common issues with `az aks command invoke`

and how to fix them, see [Resolve az aks command invoke failures](/en-us/troubleshoot/azure/azure-kubernetes/resolve-az-aks-command-invoke-failures).

## Related content

In this article, you learned how to access a private cluster and run commands on that cluster. For more information on AKS clusters, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/intro-aks-automatic -->

# What is Azure Kubernetes Service (AKS) Automatic?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic

Azure Kubernetes Service (AKS) Automatic offers an experience that makes the most common tasks on Kubernetes fast and frictionless, while preserving the flexibility, extensibility, and consistency of Kubernetes. Azure takes care of your cluster setup, including node management, scaling, security, and preconfigured settings that follow AKS well-architected recommendations. Automatic clusters dynamically allocate compute resources based on your specific workload requirements and are tuned for running production applications.

**Production ready by default**: Clusters are preconfigured for optimal production use, suitable for most applications. They offer fully managed node pools that automatically allocate and scale resources based on your workload needs. Pods are bin packed efficiently, to maximize resource utilization.**Built-in best practices and safeguards**: AKS Automatic clusters have a hardened default configuration, with many cluster, application, and networking security settings enabled by default. AKS automatically patches your nodes and cluster components while adhering to any planned maintenance schedules.**Code to Kubernetes in minutes**: Go from a container image to a deployed application that adheres to best practices patterns within minutes, with access to the comprehensive capabilities of the Kubernetes API and its rich ecosystem.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-scale -->

# Istio service mesh add-on performance and scaling

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Istio-based service mesh add-on is logically split into a control plane (`istiod`

) and a data plane. The data plane is composed of Envoy sidecar proxies inside workload pods. Istiod manages and configures these Envoy proxies. This article presents the performance of both the control and data plane for revision asm-1-19, including resource consumption, sidecar capacity, and latency overhead. Additionally, it provides suggestions for addressing potential strain on resources during periods of heavy load. This article also covers how to customize scaling for the control plane and gateways.

## Control plane performance

[Istiod’s CPU and memory requirements](https://istio.io/latest/docs/ops/deployment/performance-and-scalability/#control-plane-performance) correlate with the rate of deployment and configuration changes and the number of proxies connected. The scenarios tested were:

- Pod churn: examines the impact of pod churning on
`istiod`

. To reduce variables, only one service is used for all sidecars. - Multiple services: examines the impact of multiple services on the maximum sidecars Istiod can manage (sidecar capacity), where each service has
`N`

sidecars, totaling the overall maximum.

#### Test specifications

- One
`istiod`

instance with default settings - Horizontal pod autoscaling disabled
- Tested with two network plugins: Azure Container Networking Interface (CNI) Overlay and Azure CNI Overlay with Cilium
[(recommended network plugins for large scale clusters)](/en-us/azure/aks/azure-cni-overlay?tabs=kubectl#choosing-a-network-model-to-use) - Node SKU: Standard D16 v3 (16 vCPU, 64-GB memory)
- Kubernetes version: 1.28.5
- Istio revision: asm-1-19

### Pod churn

The [ClusterLoader2 framework](https://github.com/kubernetes/perf-tests/tree/master/clusterloader2#clusterloader) was used to determine the maximum number of sidecars Istiod can manage when there's sidecar churning. The churn percent is defined as the percent of sidecars churned down/up during the test. For example, 50% churn for 10,000 sidecars would mean that 5,000 sidecars were churned down, then 5,000 sidecars were churned up. The churn percents tested were determined from the typical churn percentage during deployment rollouts (`maxUnavailable`

). The churn rate was calculated by determining the total number of sidecars churned (up and down) over the actual time taken to complete the churning process.

#### Sidecar capacity and Istiod CPU and memory

**Azure CNI overlay**

| Churn (%) | Churn Rate (sidecars/sec) | Sidecar Capacity | Istiod Memory (GB) | Istiod CPU |
|---|---|---|---|---|
| 0 | -- | 25000 | 32.1 | 15 |
| 25 | 31.2 | 15000 | 22.2 | 15 |
| 50 | 31.2 | 15000 | 25.4 | 15 |

**Azure CNI overlay with Cilium**

| Churn (%) | Churn Rate (sidecars/sec) | Sidecar Capacity | Istiod Memory (GB) | Istiod CPU |
|---|---|---|---|---|
| 0 | -- | 30000 | 41.2 | 15 |
| 25 | 41.7 | 25000 | 36.1 | 16 |
| 50 | 37.9 | 25000 | 42.7 | 16 |

### Multiple services

The [ClusterLoader2 framework](https://github.com/kubernetes/perf-tests/tree/master/clusterloader2#clusterloader) was used to determine the maximum number of sidecars `istiod`

can manage with 1,000 services. The results can be compared to the 0% churn test (one service) in the pod churn scenario. Each service had `N`

sidecars contributing to the overall maximum sidecar count. The API Server resource usage was observed to determine if there was any significant stress from the add-on.

**Sidecar capacity**

| Azure CNI Overlay | Azure CNI Overlay with Cilium |
|---|---|
| 20000 | 20000 |

**CPU and memory**

| Resource | Azure CNI Overlay | Azure CNI Overlay with Cilium |
|---|---|---|
| API Server Memory (GB) | 38.9 | 9.7 |
| API Server CPU | 6.1 | 4.7 |
| Istiod Memory (GB) | 40.4 | 42.6 |
| Istiod CPU | 15 | 16 |

## Data plane performance

Various factors impact [sidecar performance](https://istio.io/latest/docs/ops/deployment/performance-and-scalability/#data-plane-performance) such as request size, number of proxy worker threads, and number of client connections. Additionally, any request flowing through the mesh traverses the client-side proxy and then the server-side proxy. Therefore, latency and resource consumption are measured to determine the data plane performance.

[ Fortio](https://fortio.org/) was used to create the load. The test was conducted with the

[Istio benchmark repository](https://github.com/istio/tools/tree/master/perf/benchmark#istio-performance-benchmarking)that was modified for use with the add-on.

#### Test specifications

- Tested with two network plugins: Azure CNI Overlay and Azure CNI Overlay with Cilium
[(recommended network plugins for large scale clusters)](/en-us/azure/aks/azure-cni-overlay?tabs=kubectl#choosing-a-network-model-to-use) - Node SKU: Standard D16 v5 (16 vCPU, 64-GB memory)
- Kubernetes version: 1.28.5
- Two proxy workers
- 1-KB payload
- 1,000 Queries per second (QPS) at varying client connections
`http/1.1`

protocol and mutual Transport Layer Security (TLS) enabled- 26 data points collected

#### CPU and memory

The memory and CPU usage for both the client and server proxy for 16 client connections and 1,000 QPS across all network plugin scenarios is roughly 0.4 vCPU and 72 MB.

#### Latency

The sidecar Envoy proxy collects raw telemetry data after responding to a client, which doesn't directly affect the request's total processing time. However, this process delays the start of handling the next request, contributing to queue wait times and influencing average and tail latencies. Depending on the traffic pattern, the actual tail latency varies.

The following results evaluate the impact of adding sidecar proxies to the data path, showcasing the P90 and P99 latency.

- Sidecar traffic path: client --> client-sidecar --> server-sidecar --> server
- Baseline traffic path: client --> server

A comparison of data plane latency performance across Istio add-on and AKS versions can be found [here](istio-latency).

| Azure CNI Overlay | Azure CNI Overlay with Cilium |
|---|---|
|

## Scaling

### Horizontal pod autoscaling customization

[Horizontal pod autoscaling (HPA)](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) is enabled for the `istiod`

and ingress/egress gateway deployments. The default configurations for `istiod`

and the gateways are:

- Min Replicas: 2
- Max Replicas: 5
- CPU Utilization: 80%

Note

To prevent conflicts with the `PodDisruptionBudget`

, the add-on does not allow setting the `minReplicas`

below the initial default of `2`

.

The following are the `istiod`

and ingress gateway HPA resources:

```
NAMESPACE NAME REFERENCE
aks-istio-ingress aks-istio-ingressgateway-external-asm-1-19 Deployment/aks-istio-ingressgateway-external-asm-1-19
aks-istio-ingress aks-istio-ingressgateway-internal-asm-1-19 Deployment/aks-istio-ingressgateway-internal-asm-1-19
aks-istio-system istiod-asm-1-19 Deployment/istiod-asm-1-19
```


The HPA configuration can be modified through patches and direct edits. Example:

```
kubectl patch hpa aks-istio-ingressgateway-external-asm-1-19 -n aks-istio-ingress --type merge --patch '{"spec": {"minReplicas": 3, "maxReplicas": 6}}'
```


Note

See the [Istio add-on upgrade documentation](istio-upgrade#minor-revision-upgrades-with-horizontal-pod-autoscaling-customizations) for details on how HPA settings are applied across both revisions during a canary upgrade.

## Service entry

Istio's ServiceEntry custom resource definition enables adding other services into the Istio’s internal service registry. A [ServiceEntry](https://istio.io/latest/docs/reference/config/networking/service-entry/) allows services already in the mesh to route or access the services specified. However, the configuration of multiple ServiceEntries with the `resolution`

field set to DNS can cause a [heavy load on Domain Name System (DNS) servers](https://preliminary.istio.io/latest/docs/ops/configuration/traffic-management/dns/#proxy-dns-resolution). The following suggestions can help reduce the load:

- Switch to
`resolution: NONE`

to avoid proxy DNS lookups entirely. Suitable for most use cases. However, when using an[Istio add-on egress gateway](istio-deploy-egress), the ServiceEntry resolution must be set to`DNS`

. - Increase TTL (Time To Live) if you control the domains being resolved.
- Limit the ServiceEntry scope with
`exportTo`

.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-cluster -->

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
