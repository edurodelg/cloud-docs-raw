---
merged_at: 2026-01-25T12:25:33.961082
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: considerations-pod-sandboxing.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/considerations-pod-sandboxing -->

# Pod Sandboxing considerations

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

For Pod Sandboxing deployments on Azure Kubernetes Service (AKS) there are several items to consider in regard to resource management, memory management, CPU management, and security.

## Resource management

Memory and CPU management behavior with Pod Sandboxing might be unfamiliar to some users. These considerations are relevant when specifying resources in a deployment, especially for larger and resource sensitive workloads.

### Kata components

In a Kata deployment, there are generally two families of components that get deployed. You have **host components** and **guest components**.

- The main
**host components**comprise of the*Kata shim*,*Cloud Hypervisor*, and*virtiofsd*.- The
*Kata shim*manages a pod VM lifecycle. *Cloud Hypervisor*is the Virtual Machine Monitor (VMM) used by the Kata shim.*virtiofsd*is a daemon used to share files between each Pod VM and its container host.

- The
- The main
**guest components**include the*user's workloads*,*pod VM kernel*, and the*Kata agent*.- The
*Kata agent*manages containers inside of the Pod VMs

- The

### Memory management

With Kata pods, you have the ability to specify the amount of memory of the Pod VM that hosts your workloads. It's crucial that you configure the values accordingly so that a pod has sufficient resources, but doesn't result in unused memory being allocated to the pod.

### Pod VM memory size

There's an amount of memory allocated to each pod VM that runs a container. This VM memory size is inclusive of all the memory necessary to run Kata guest components. Users should take care to ensure that they buffer some extra memory beyond the expected consumption of their workloads to account for the consumption of other guest components, such as the kata agent or VM kernel. Examples are given on typical memory values later on in this article.

The pod VM memory size is equivalent to the [Kubernetes pod memory limit](https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/#specify-a-memory-request-and-a-memory-limit) the user specifies. A user can change the value by changing their pod memory limit; if no values are specified, a default size of 512Mi is applied. Once the pod starts, this size becomes fixed.

As the pod VM memory size increases, the runtime class memory overhead should be expected to increase alongside it.

### Runtime class memory overhead

Pod Sandboxing workloads come with a default kata runtime class (`kata-vm-isolation`

) which comes with default overheads for resources. Users that want finer grain control of their resource quotas can [set up a custom runtime class](https://kubernetes.io/docs/concepts/containers/runtime-class/#setup) with specific resource overheads. When doing so, users should ensure that the memory overhead value of the runtime class is enough that covers all expected usage for the **host components** of a kata deployment. The runtime class memory overhead does *not* need to account for the expected memory consumption of the **guest components**.

You can create a specialized runtime and specify the memory overhead in your runtime class through the `overhead`

field in your `RuntimeClass`

manifest. [As an example](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-overhead/#usage-example), let's assume I want to create a runtime for workloads I expect to be smaller in consumption:

```
apiVersion: node.k8s.io/v1
kind: RuntimeClass
metadata:
name: small-kata-pods
handler: kata
overhead:
podFixed:
memory: "120Mi"
```


Specifying overheads isn't required, and suggested if you want finer control over the resources being set aside for your workloads. If you use the default `kata-vm-isolation`

runtime class and don't specify any overheads in your YAML, the overhead of the Pod VM size defaults to 512Mi and the runtime class overhead defaults to 600Mi. This default runtime overhead is calculated with the default pod VM size (512Mi) plus to approximate memory needed by host components for such a VM size (~88Mi).

### User workloads

When a user deploys a Kata workload, they're able to use memory up to the configured *pod VM memory size* minus the other guest components, such as the Kata agent or the guest VM kernel.

If you would like to get an approximation of the memory used by these components:

- Connect to the pod VM (either via
`kubectl exec`

or`kubectl debug`

to open a shell inside your pod). - Run the
`free`

command. - Inspect the "used" column in the output to get an idea of the memory consumed by the guest kernel/kata agent.

### Memory cgroups

When a Kata pod is scheduled to run, kubelet assigns the pod to a memory `cgroup`

. This `cgroup`

enforces the pod's memory limits/requests, allowing a user to define the resource quotas available to a pod.

Within the memory `cgroup`

, there are two important fields to consider:

`memory.current`

defines how many bytes of memory the host components and the pod VM memory size allocates.`memory.max`

optional, user defined upper limit of memory.current for pods where users want to impose a memory limit.- The kubelet computes this value as the sum of a pod's memory limit and its runtime class memory overhead.


At any point, if the `memory.current`

value exceeds that of `memory.max`

, [the kernel might trigger an OOMKill on the pod if memory pressure is detected](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#requests-and-limits).

### Reference usage values

Users can utilize these values to serve as a reference for the typical memory usage and values across the different variables covered. Pod VM memory sizes under 128Mi aren't supported.

| Pod VM Memory Size | Runtime class overhead | memory.current | memory.max | Free memory available to Host components |
|---|---|---|---|---|
| 128Mi | 16Mi | 133Mi | 144Mi | 11Mi |
| 256Mi | 32Mi | 263Mi | 288Mi | 25Mi |
| 1Gi | 128Mi | 1034Mi | 1152Mi | 118Mi |
| 2Gi | 256Mi | 2063Mi | 2304Mi | 241Mi |
| 4Gi | 374Mi | 4122Mi | 4470Mi | 348Mi |
| 8Gi | 512Mi | 8232Mi | 8704Mi | 472Mi |
| 32Gi | 640Mi | 32918Mi | 33408Mi | 490Mi |
| 64Gi | 768Mi | 65825Mi | 66304Mi | 479Mi |
| 96Gi | 896Mi | 98738Mi | 99200Mi | 462Mi |
| 128Gi | 1Gi | 131646Mi | 132096Mi | 450Mi |

## CPU management

In a similar vein to memory, you can also allocate CPU resources to your Kata workloads. Doing so is recommended; without declaring a CPU limit for your Kata pod, Kata host components are able to use any CPU capacity available on the node.

### Reserving CPU

When reserving CPUs for your Kata workloads, you have two fields you can choose to set.

- The
*runtime class CPU overhead* - The
*pod CPU limit*

When at least one of the two values is specified, the control plane reserves the specified number of CPUs on the node for your workload. Other pods on the same node can't access this reserved capacity.

### Pod CPU limit

You can declare your [pod CPU limit](https://kubernetes.io/docs/tasks/configure-pod-container/assign-cpu-resource/) in your application's manifest. A specified pod CPU limit defines the limit of the CPUs that containers in the associated pod VM can use.

If you specify fractions of CPUs for the pod CPU limit, those fractions will get rounded up to the next integer. The rounded up number becomes the number of vCPUs allocated to the Pod VM, but a `cgroup`

will limit the workload to only consume the fraction specified in the pod CPU limit.

If no number is declared, one vCPU will be allocated to the pod VM if the capacity is available on the node. There's no limit on the CPU consumption of the Kata host components.

### Runtime class CPU overhead

The runtime class overhead should be specified if you'd like to preemptively reserve some node capacity for the Kata host components.

You can specify the memory overhead in your runtime class through the `overhead`

field in your `RunTimeClass`

manifest. [As an example](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-overhead/#usage-example):

```
apiVersion: node.k8s.io/v1
kind: RuntimeClass
metadata:
name: custom-kata-runtime
handler: kata
overhead:
podFixed:
cpu: "250m"
```


### Best practices

#### Memory management

- Ensure you specify pod VM memory sizes (defined by the
`limits.memory`

in your manifest) and suitable resource quotas for all your deployments.- Ensure you use a nonzero
*pod request*if you want to ensure that some node capacity is reserved for the pod VM before that VM starts up. The request should account for the pod VM and containers that are expected to run on it. - Ensure you use a nonzero
*runtime class overhead*if you want to reserve some node capacity for the Kata host components before those components start up.

- Ensure you use a nonzero
- If you expect your pod workloads to be especially resource hungry, you can specify limits accordingly for the pod VM to ensure that there are ample resources available for your workloads.
- Declare a suitable runtime class memory overhead such that it gives enough memory for your host components but doesn't take too much to avoid allocating unused memory.

#### CPU management

If your node typically has plenty of free CPU capacity, these reservations might be unnecessary.

If your nodes typically run to the limit with CPU consumption, then a nonzero reservation ensures your pods can be executed more reliably.

- You can utilize pod CPU requests to ensure that some CPU node capacity is reserved for the Kata host components. Reserved capacity for a specific workload is
*not*available to other workloads on the node.

- You can utilize pod CPU requests to ensure that some CPU node capacity is reserved for the Kata host components. Reserved capacity for a specific workload is
Make sure you specify CPU requests that your infrastructure can accommodate. If your available capacity runs near 0, or your request is too large, your workloads might

[fail to start](https://kubernetes.io/docs/tasks/configure-pod-container/assign-cpu-resource/#specify-a-cpu-request-that-is-too-big-for-your-nodes)Align your CPU requests with your CPU limits. The Kata shim doesn't have visibility into requests. Therefore, if no CPU limit is declared, the pod VM is limited to one vCPU. The Kata host components, which do have visibility into request values, consumes the rest of the requested CPU count and have no limit to CPU consumption.

Reserved capacity for a specific workload is

*not*available to other workloads on the node.

### Example declarations

| Runtime class CPU overhead | Pod CPU Request/Limit | Expected behavior |
|---|---|---|
| 1 | 1 | The control plane reserves two CPUs on the node. The pod VM gets one CPU, and containers on the pod can use up to the one vCPU capacity. The Kata host components and pod VM together can use up to two CPUs from the reserved capacity on the node. |
| 1 | 2.5 | The control plane reserves 3.5 CPUs on the node. The pod VM gets three vCPUs, but containers on the pod VM can use up to 2.5 vCPU capacity. The Kata host components and pod VM together can use up to 3.5 CPUs from the reserved capacity on the node. |
| None | 1 | The control plane reserves one CPU on the node. The pod VM gets one vCPU, and containers on the pod VM can use up to one vCPU capacity. The Kata host components and the pod VM together are allowed to use up to one CPU from the reserved capacity on the node. One CPU is always available to the pod VM due to the CPU request. |
| 1 | None | The control plane reserves one CPU on the node. The pod VM gets one vCPU, and containers on the pod VM can use up to one vCPU capacity. The kata host components and the pod VM can use any CPU capacity available on the node. At least one CPU is always available due to the overhead reservation. |

## Security

Pod Sandboxing offers users a compelling option to isolate their workloads from other workloads and the host. There are, nonetheless, important security concerns that should be taken into account.

### Privileged pods

There are scenarios in which privileged pods might be required. Users are able to spin up privileged pods, but no [host devices are attached to the pod](https://github.com/kata-containers/kata-containers/blob/main/docs/how-to/privileged.md#containerd).

Using privileged containers lead to root access in the guest VM, but remain isolated from the host.

Privileged pods, even on Pod Sandboxing, should only be used when necessary. Privileged pods should continue to be [managed by trusted users](https://kubernetes.io/docs/concepts/security/pod-security-standards/#privileged).

### Host path storage volumes

`hostPath`

volumes can be mounted into Kata pods. In Pod Sandboxing, using `hostPath`

volumes can potentially undermine the isolation that Kata provides; since part of the host filesystem is exposed directly to the container, a potential attack vector is opened. The warnings posed by [upstream](https://kubernetes.io/docs/concepts/storage/volumes/#hostpath) should be considered as relevant for Pod Sandboxing as well.

There are some exceptions; files under `/dev`

are mounted into the container from the guest system instead of the host system. This helps maintain pod isolation for situations where this path must be mounted to function.

Warning

Unless necessary, the recommendation is to *avoid* using hostPath storage volumes.

#### Blocking hostPath via Azure Policy

[Azure Policy](/en-us/azure/governance/policy/concepts/policy-for-kubernetes) allows users to apply at-scale enforcements and safeguards on their cluster components in a centralized, consistent manner.

There is a set of [built-in policy sets](policy-reference) for AKS that enforce best practices. Users can take advantage of one of these policies to block deployments that attempt to mount hostPaths.

## Next steps

Once you're ready, learn how to [deploy pod sandboxing on AKS](use-pod-sandboxing).


---

<!-- DOCUMENTO FUSIONADO: control-plane-metrics-monitor.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/control-plane-metrics-monitor -->

# Monitor Azure Kubernetes Service control plane metrics (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to monitor the Azure Kubernetes Service (AKS) control plane by using control plane metrics in Azure Monitor.

AKS supports a subset of control plane metrics free through [Azure Monitor platform metrics](monitor-aks#aks-monitoring-data-metrics-logs-integrations). The control plane metrics feature gives you visibility into the availability and performance of critical control plane components like the API server, etcd, the scheduler, the autoscaler, and the controller manager in AKS. The feature is also fully compatible with the managed service for Prometheus and Azure Managed Grafana. You can use these metrics to maximize overall observability and to maintain operational excellence for your AKS cluster.

## Control plane platform metrics

AKS offers some free control plane metrics for monitoring the API server and etcd. These metrics are automatically collected for all AKS clusters at no cost. You can analyze the metrics by using the [metrics explorer](/en-us/azure/azure-monitor/essentials/analyze-metrics) in the Azure portal. You can also create metrics-based alerts by using the metrics data.

To see the full list of supported control plane platform metrics, see the [AKS monitoring reference](monitor-aks-reference#metrics).

## Prerequisites and limitations

- The control plane metrics (preview) feature supports only the
[managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)in Azure Monitor. [Azure Private Link](/en-us/azure/azure-monitor/logs/private-link-security)isn't supported.- You can customize only the default
configmap file. No other customization is supported.`ama-metrics-settings-configmap.yaml`

- Your AKS cluster must use
[managed identity authentication](use-managed-identity).

### Install the aks-preview extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install or update the

`aks-preview`

Azure CLI extension by using theor`az extension add`

command:`az extension update`

`# Install the aks-preview extension az extension add --name aks-preview # Update the aks-preview extension az extension update --name aks-preview`


### Register the AzureMonitorMetricsControlPlanePreview feature flag

Register the

`AzureMonitorMetricsControlPlanePreview`

feature flag by using thecommand:`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AzureMonitorMetricsControlPlanePreview"`

It takes a few minutes for the status to show as

**Registered**.Verify the registration status by using the

command:`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "AzureMonitorMetricsControlPlanePreview"`

When the status is

**Registered**, refresh the registration of the Microsoft.ContainerService resource provider by using thecommand:`az provider register`

`az provider register --namespace "Microsoft.ContainerService"`


## Enable control plane metrics on an AKS cluster

Enable control plane metrics by using the managed service for Prometheus add-on when you create a new cluster or update an existing cluster.

Note

Unlike the metrics that are collected from cluster nodes, control plane metrics are collected by a component that isn't part of the `ama-metrics`

add-on. Enabling the `AzureMonitorMetricsControlPlanePreview`

feature flag and the managed service for Prometheus add-on ensures that control plane metrics are collected. After you enable metrics collection, it can take several minutes for the data to appear in the workspace.

### New AKS cluster

To learn how to collect managed service for Prometheus metrics from your AKS cluster, see [Enable Prometheus and Grafana for AKS clusters](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable#enable-prometheus-and-grafana). For an AKS cluster, complete the steps described on the **CLI** tab.

### Existing AKS cluster

If your cluster already has the managed service for Prometheus add-on, update the cluster to ensure that it collects control plane metrics by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command:

```
az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Query control plane metrics

Control plane metrics are stored in an Azure Monitor workspace in the cluster's region. You can query the metrics directly in the workspace or by using the Azure Managed Grafana instance that's connected to the workspace.

In the

[Azure portal](https://portal.azure.com), go to your AKS cluster resource.On the left menu, select

**Monitor**>**Monitor Settings**.Go to the Azure Monitor workspace that is linked to the cluster.

In the Azure Monitor workspace, under

**Managed Prometheus**, query the metrics by using the Prometheus explorer.

Note

AKS provides dashboard templates to help you view and analyze your control plane telemetry data in real time. If you use Azure Managed Grafana to visualize the data, you can import the following dashboards:

## Customize control plane metrics

AKS includes a preconfigured set of metrics to collect and store for each component. Metrics for the API server and etcd are collected by default. You can customize the list of metrics that are collected by modifying the [ ama-metrics-settings-configmap.yaml](https://github.com/Azure/prometheus-collector/blob/main/otelcollector/configmaps/ama-metrics-settings-configmap.yaml) configmap file.

Default targets include the following values:

```
controlplane-apiserver = true
controlplane-cluster-autoscaler = false
controlplace-node-auto-provisioning = false
controlplane-kube-scheduler = false
controlplane-kube-controller-manager = false
controlplane-etcd = true
```


All configmap files should be applied to the `kube-system`

namespace for any cluster.

### Customize an ingestion profile

You can customize an ingestion file for collected metrics. For more information, see [Minimal ingestion profile for control plane metrics in managed service for Prometheus](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-configuration-minimal#minimal-ingestion-for-default-on-targets).

#### Ingest only minimal metrics from default targets

- Set
`default-targets-metrics-keep-list.minimalIngestionProfile`

to`true`

, so it ingests only the minimal set of metrics for each of the default targets:`controlplane-apiserver`

and`controlplane-etcd`

.

#### Ingest all metrics from all targets

Download the

configmap file.`ama-metrics-settings-configmap.yaml`

Rename the configmap file

`configmap-controlplane.yaml`

.Set

`minimalingestionprofile`

to`false`

.Under

`default-scrape-settings-enabled`

, verify that the targets you want to scrape are set to`true`

.The targets you can set are:

`controlplane-apiserver`

`controlplane-cluster-autoscaler`

`controlplace-node-auto-provisioning`

`controlplane-kube-scheduler`

`controlplane-kube-controller-manager`

`controlplane-etcd`


Apply the configmap file by using the

command:`kubectl apply`

`kubectl apply -f configmap-controlplane.yaml`


After you apply the configuration, it takes several minutes for the metrics from the specified targets that are scraped from the control plane to appear in the Azure Monitor workspace.

#### Ingest more than minimal metrics

Using the `minimalingestionprofile`

setting helps reduce the ingestion volume of metrics. If set to `true`

, only default recording rules, default alerts, and metrics that appear in the default dashboards are collected.

Download the

configmap file.`ama-metrics-settings-configmap.yaml`

Rename the configmap file

`configmap-controlplane.yaml`

.Set

`minimalingestionprofile`

to`true`

.Under

`default-scrape-settings-enabled`

, verify that the targets you want to scrape are set to`true`

.The targets you can set are:

`controlplane-apiserver`

`controlplane-cluster-autoscaler`

`controlplane-node-auto-provisioning`

`controlplane-kube-scheduler`

`controlplane-kube-controller-manager`

`controlplane-etcd`


Under

`default-targets-metrics-keep-list`

, specify the list of metrics for the`true`

targets.For example:

`controlplane-apiserver= "apiserver_admission_webhook_admission_duration_seconds|apiserver_longrunning_requests"`

Apply the configmap file by using the

command:`kubectl apply`

`kubectl apply -f configmap-controlplane.yaml`


After you apply the configuration, it takes several minutes for the metrics from the specified targets that are scraped from the control plane to appear in the Azure Monitor workspace.

#### Ingest specific metrics from specific targets

Download the

configmap file.`ama-metrics-settings-configmap.yaml`

Rename the configmap file

`configmap-controlplane.yaml`

.Set

`minimalingestionprofile`

to`false`

.Under

`default-scrape-settings-enabled`

, verify that the targets that you want to scrape are set to`true`

.The targets you can set are:

`controlplane-apiserver`

`controlplane-cluster-autoscaler`

`controlplane-node-auto-provisioning`

`controlplane-kube-scheduler`

`controlplane-kube-controller-manager`

`controlplane-etcd`


Under

`default-targets-metrics-keep-list`

, specify the list of metrics for the`true`

targets.For example:

`controlplane-apiserver= "apiserver_admission_webhook_admission_duration_seconds|apiserver_longrunning_requests"`

Apply the configmap file:

`kubectl apply -f configmap-controlplane.yaml`


After you apply the configuration, it takes several minutes for the metrics from the specified targets that are scraped from the control plane to appear in the Azure Monitor workspace.

## Troubleshoot control plane metrics issues

Make sure that the `AzureMonitorMetricsControlPlanePreview`

feature flag is enabled and that the `ama-metrics`

pods are running.

Note

The [troubleshooting methods](/en-us/azure/azure-monitor/containers/prometheus-metrics-troubleshoot) for the managed service for Prometheus don't apply directly in this scenario. The components that scrape the control plane aren't included in the managed service for Prometheus add-on.

**Configmap file formatting**: Make sure that you use the correct formatting in the configmap file. Verify that the fields`default-targets-metrics-keep-list`

,`minimal-ingestion-profile`

, and`default-scrape-settings-enabled`

and other fields are correctly populated with their intended values.**Isolate the control plane from the data plane**: Start by setting some of the[node-related metrics](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-default)to`true`

, and then verify that the metrics are forwarded to the workspace. Completing these steps helps you determine whether an issue is specific to scraping control plane metrics.**A change in the number of events ingested**: After you apply the changes, you can open the metrics explorer in the Azure portal. Go to the Azure Monitor overview pane for the cluster or go to the**Monitoring**section of the selected cluster. Check for an increase or a decrease in the number of events ingested per minute. This information can help you determine whether a specific metric is missing or if all metrics are missing.**A specific metric isn't exposed**: In some scenarios, a metric is documented, but it isn't exposed from the target and isn't forwarded to the Azure Monitor workspace. In this case, it's necessary to verify that other metrics are forwarded to the workspace.Note

If you want to collect the

`apiserver_request_duration_seconds`

metric or another bucket metric, you must set the entire series in the histogram family:`controlplane-apiserver = "apiserver_request_duration_seconds_bucket|apiserver_request_duration_seconds_sum|apiserver_request_duration_seconds_count"`

**No access to the Azure Monitor workspace**: When you enable the add-on, you might specify an existing workspace that you can't access. In that scenario, it appears that metrics aren't collected and forwarded. Make sure that you create a new workspace to use to collect metrics when you enable the add-on or when you create the cluster.

## Disable control plane metrics on your AKS cluster

You can disable control plane metrics at any time by disabling the managed service for Prometheus add-on and unregistering the `AzureMonitorMetricsControlPlanePreview`

feature flag.

Remove the metrics add-on that scrapes Prometheus metrics by using the

command:`az aks update`

`az aks update --disable-azure-monitor-metrics --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP`

To disable scraping control plane metrics on the AKS cluster, unregister the

`AzureMonitorMetricsControlPlanePreview`

feature flag via thecommand:`az feature unregister`

`az feature unregister "Microsoft.ContainerService" --name "AzureMonitorMetricsControlPlanePreview"`


## Frequently asked questions

### Can I scrape control plane metrics by using self-hosted Prometheus?

No. Currently, you can't scrape control plane metrics by using self-hosted Prometheus. Self-hosted Prometheus can scrape only a single instance, depending on the load balancer, so the metrics aren't reliable. Often, multiple replicas of the control plane metrics are visible only through the managed service for Prometheus.

### Why isn't the user agent available in the control plane metrics?

In AKS, [control plane metrics](https://kubernetes.io/docs/reference/instrumentation/metrics/) don't have the user agent. The user agent is available only through the control plane logs that you access in [diagnostic settings](/en-us/azure/azure-monitor/essentials/diagnostic-settings).
