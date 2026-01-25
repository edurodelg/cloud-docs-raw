---
merged_at: 2026-01-25T12:25:33.969508
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: best-practices-cost.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/best-practices-cost -->

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

<!-- DOCUMENTO FUSIONADO: gpu-cluster.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/gpu-cluster -->

# Use GPUs for compute-intensive workloads on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Graphical processing units (GPUs) are often used for compute-intensive workloads, such as graphics and visualization workloads. AKS supports GPU-enabled Linux node pools to run compute-intensive Kubernetes workloads.

This article helps you provision nodes with schedulable GPUs on new and existing AKS clusters.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

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

Note

The AKS GPU image (preview) is retired starting on January 10, 2025. The custom header is no longer available, meaning that you can't create new GPU-enabled node pools using the AKS GPU image. We recommend migrating to or using the default GPU configuration rather than the GPU image, as the GPU image is no longer supported. For more information, see [AKS release notes](https://github.com/Azure/AKS/releases), or view this retirement announcement in our [AKS public roadmap](https://github.com/Azure/AKS/issues/4472).

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

Note

The `gpu-driver`

API field is a suggested alternative for customers previously using the `--skip-gpu-driver-install`

node pool tag.

- The
`--skip-gpu-driver-install`

node pool tag on AKS will be retired on 14 August 2025. When spinning up a new node pool, the existing behavior of skipping automatic GPU driver installation can be replicated by setting the`--gpu-driver`

field to`none`

. - After 14 August 2025, you will not be able to provision AKS GPU-enabled node pools with the
`--skip-gpu-driver-install`

node pool tag to bypass this default behavior. For more information, see.`skip-gpu-driver`

tag retirement

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
