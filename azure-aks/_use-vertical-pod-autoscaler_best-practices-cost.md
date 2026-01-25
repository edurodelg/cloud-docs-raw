---
merged_at: 2026-01-25T12:06:27.867341
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-vertical-pod-autoscaler.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-vertical-pod-autoscaler -->

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
