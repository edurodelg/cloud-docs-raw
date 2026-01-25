---
merged_at: 2026-01-25T12:25:33.898776
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: coredns-autoscale.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/coredns-autoscale -->

# Autoscaling CoreDNS in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure and customize CoreDNS autoscaling in Azure Kubernetes Service (AKS) clusters.

## Configure CoreDNS horizontal pod scaling

Due to the elastic nature of AKS, it's common to experience sudden spikes in DNS traffic within your clusters. These spikes can lead to an increase in memory consumption by CoreDNS pods. In some cases, this increased memory consumption can cause `Out of memory`

issues.

To preempt this issue, AKS clusters autoscale CoreDNS pods to reduce memory usage per pod. The default settings for this autoscaling logic are stored in the `coredns-autoscaler`

ConfigMap. However, you might observe that the default autoscaling of CoreDNS pods isn't always aggressive enough to prevent `Out of memory`

issues for your CoreDNS pods. In this case, you can directly modify the `coredns-autoscaler`

ConfigMap. Keep in mind that simply increasing the number of CoreDNS pods without addressing the root cause of the `Out of memory`

issue might only provide a temporary fix. If there's not enough memory available across the nodes where the CoreDNS pods are running, increasing the number of CoreDNS pods won't help. You might need to investigate further and implement appropriate solutions such as optimizing resource usage, adjusting resource requests and limits, or adding more memory to the nodes.

CoreDNS uses the [horizontal cluster proportional autoscaler](https://github.com/kubernetes-sigs/cluster-proportional-autoscaler) for pod autoscaling. You can edit the `coredns-autoscaler`

to configure the scaling logic for the number of CoreDNS pods. The `coredns-autoscaler`

ConfigMap currently supports two different ConfigMap key values: `linear`

and `ladder`

, which correspond to two supported control modes.

- The
`linear`

controller yields a number of replicas in [min,max] range equivalent to`max( ceil( cores * 1/coresPerReplica ) , ceil( nodes * 1/nodesPerReplica ) )`

. - The
`ladder`

controller calculates the number of replicas by consulting two different step functions, one for core scaling and another for node scaling, yielding the max of the two replica values.

For more information on the control modes and ConfigMap format, see the [upstream documentation](https://github.com/kubernetes-sigs/cluster-proportional-autoscaler#control-patterns-and-configmap-formats).

Important

We recommend a minimum of *two* CoreDNS pod replicas per cluster.

### View the current `coredns-autoscaler`

ConfigMap

Get the current

`coredns-autoscaler`

ConfigMap using thecommand.`kubectl get configmaps`

`kubectl get configmap coredns-autoscaler --namespace kube-system --output yaml`

Your output should resemble the following example output:

`apiVersion: v1 data: ladder: '{"coresToReplicas":[[1,2],[512,3],[1024,4],[2048,5]],"nodesToReplicas":[[1,2],[8,3],[16,4],[32,5]]}' kind: ConfigMap metadata: name: coredns-autoscaler namespace: kube-system resourceVersion: "..." creationTimestamp: "..."`


Note

The configuration provided serves as a potential starting point, but you should customize the values based on your specific cluster requirements and DNS traffic patterns. One way to determine the appropriate number of replicas for your environment is to use the linear scaling formula: `replicas = max( ceil( cores * 1/coresPerReplica ) , ceil( nodes * 1/nodesPerReplica ) )`

to determine replica counts based on core / node count in the cluster.

## CoreDNS vertical pod autoscaling behavior

CoreDNS uses the original provided resource requests/limits when enabling the [add-on autoscaling feature](optimized-addon-scaling) to prevent service unavailability during the CoreDNS pod restart process.

The following table outlines the default requests/limits and request-to-limit ratios for the AKS CoreDNS add-on:

| Resource | Requests/limits | Request-to-limit ratio |
|---|---|---|
| CPU | `100 m / 3 cores` |
Approximately 1:30 |
| Memory | `70 Mi / 500 Mi` |
Approximately 1:7 |

If the recommended CPU requests are *500 m*, VPA adjusts the CPU limits to *15* to maintain this ratio. Similarly, if the recommended memory requests are *700 Mi*, VPA adjusts the memory limit to *5000 Mi*.

VPA sets CoreDNS CPU and memory limits to large values based on the VPA recommended CPU/Memory request and AKS defined request-to-limit ratio. These adjustments are beneficial for handling multiple requests during peak service times. The drawback is that CoreDNS might consume all the CPU and memory available resource on the node when the peak service time.

It's difficult to set a single ideal CPU and memory requests/limits value to meet the requirements of both large cluster and small cluster at the same time. By enabling optimized add-on scaling, you have the flexibility to customize the CoreDNS CPU and memory requests/limits or use VPA to autoscale CoreDNS to meet specific cluster requirements. Keep the following scenarios in mind when deciding whether to customize the resource configuration or use VPA:

- You're considering whether VPA is suitable for your CoreDNS service and want to only view the VPA recommendations. You can disable VPA for CoreDNS by enabling the override VPA update mode to
*Off*if you don't want VPA to automatically update the pods.[Customize the resource configuration in Deployment](customize-resource-configuration)to set the CPU/Memory requests/limits to the value you prefer. - You're considering using VPA but want to restrict the ratio of request-to-limit so VPA won't bump the CPU and Memory limit to large values at one time. You can customize resources in the Deployment and update the CPU and Memory requests/limits value to keep the ratio of request-to-limit to
*1:2*or*1:3*. - If a VPA container policy sets maxAllowed CPU and Memory, the recommended resource requests won't exceed those limits. Customizing the resource configuration allows you to increase or decrease the maxAllowed values and control the recommendations of VPA.

For more information, see [Enable add-on autoscaling on your AKS cluster (Preview)](optimized-addon-scaling).

## Next steps

To learn how to troubleshoot CoreDNS issues, see [Troubleshoot issues with CoreDNS on Azure Kubernetes Service (AKS)](coredns-troubleshoot).


---

<!-- DOCUMENTO FUSIONADO: keda-about.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/keda-about -->

# Simplified application autoscaling with Kubernetes Event-driven Autoscaling (KEDA) add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The KEDA add-on for AKS doesn't currently support modifying the CPU requests or limits and other Helm values for the [Metrics Server](https://keda.sh/docs/2.14/operate/metrics-server/) or [Operator](https://keda.sh/docs/2.14/operate/cluster/). Keep this limitation in mind when using the add-on. If you have any questions, feel free to reach out [here](https://github.com/Azure/AKS/issues).

Kubernetes Event-driven Autoscaling (KEDA) is a single-purpose and lightweight component that strives to make application autoscaling simple and is a Cloud Native Computing Federation (CNCF) Graduate project.

It applies event-driven autoscaling to scale your application to meet demand in a sustainable and cost-efficient manner with scale-to-zero.

The KEDA add-on makes it even easier by deploying a managed KEDA installation, providing you with [a rich catalog of Azure KEDA scalers](https://keda.sh/docs/scalers/) that you can scale your applications with on your Azure Kubernetes Services (AKS) cluster.

Note

KEDA version 2.15+ introduces a breaking change that [removes pod identity support](https://github.com/kedacore/keda/issues/5035). We recommend moving over to workload identity for your authentication if you're using pod identity. While the KEDA managed add-on doesn't currently run KEDA version 2.15+, it will begin running it in the AKS preview version 1.32.

For more information on how to securely scale your applications with workload identity, read our [tutorial](keda-workload-identity). To view KEDA's breaking change/deprecation policy, read their [official documentation](https://github.com/kedacore/governance/blob/main/DEPRECATIONS.md).

## Architecture

[KEDA](https://keda.sh/) provides two main components:

**KEDA operator**allows end-users to scale workloads in or out from 0 to N instances with support for Kubernetes Deployments, Jobs,`StatefulSets`

, or any custom resource that defines`/scale`

subresource.**Metrics server**exposes external metrics to Horizontal Pod Autoscaler (HPA) in Kubernetes for autoscaling purposes such as messages in a Kafka topic, or number of events in an Azure event hub. Due to upstream limitations, KEDA must be the only installed external metric adapter.


Learn more about how KEDA works in the [official KEDA documentation](https://keda.sh/docs/latest/concepts/).

## Installation

KEDA can be added to your Azure Kubernetes Service (AKS) cluster by enabling the KEDA add-on using an [ARM template](keda-deploy-add-on-arm) or [Azure CLI](keda-deploy-add-on-cli).

The KEDA add-on provides a fully supported installation of KEDA that is integrated with AKS.

## Capabilities and features

KEDA provides the following capabilities and features:

- Build sustainable and cost-efficient applications with scale-to-zero
- Scale application workloads to meet demand using
[a rich catalog of Azure KEDA scalers](https://keda.sh/docs/scalers/) - Autoscale applications with
`ScaledObjects`

, such as Deployments,`StatefulSets`

, or any custom resource that defines`/scale`

subresource - Autoscale job-like workloads with
`ScaledJobs`

- Use production-grade security by decoupling autoscaling authentication from workloads
- Bring-your-own external scaler to use tailor-made autoscaling decisions
- Integrate with
[Microsoft Entra Workload ID](workload-identity-overview)for authentication

Note

If you plan to use workload identity, [enable the workload identity add-on](workload-identity-deploy-cluster) before enabling the KEDA add-on.

## Add-on limitations

The KEDA AKS add-on has the following limitations:

- KEDA's
[HTTP add-on (preview)](https://github.com/kedacore/http-add-on)to scale HTTP workloads isn't installed with the extension, but can be deployed separately. - KEDA's
[external scaler for Azure Cosmos DB](https://github.com/kedacore/external-scaler-azure-cosmos-db)to scale based on Azure Cosmos DB change feed isn't installed with the extension, but can be deployed separately. - Only one external metric server is allowed in the Kubernetes cluster. Because of that the KEDA add-on should be the only external metrics server inside the cluster.
- Multiple KEDA installations aren't supported

- It's not recommended to combine KEDA's
`ScaledObject`

with a Horizontal Pod Autoscaler (HPA) to scale the same workload. They compete with each other because KEDA uses Horizontal Pod Autoscaler (HPA) in the background and results in odd scaling behavior.- If an HPA is created first, then a KEDA
`ScaledObject`

is created and the KEDA`ScaledObject`

would fail to be created. - If a KEDA
`ScaledObject`

is created first and then an HPA is created, the HPA creation isn't blocked.

- If an HPA is created first, then a KEDA

For general KEDA questions, we recommend [visiting the FAQ overview](https://keda.sh/docs/2.14/reference/faq/).

Note

If you're using [Microsoft Entra Workload ID](/en-us/azure/aks/workload-identity-overview) and you enable KEDA before Workload ID, you need to restart the KEDA operator pods so the proper environment variables can be injected:

Restart the pods by running

`kubectl rollout restart deployment keda-operator -n kube-system`

.Obtain KEDA operator pods using

`kubectl get pod -n kube-system`

and finding pods that begin with`keda-operator`

.Verify successful injection of the environment variables by running

`kubectl describe pod <keda-operator-pod> -n kube-system`

. Under`Environment`

, you should see values for`AZURE_TENANT_ID`

,`AZURE_FEDERATED_TOKEN_FILE`

, and`AZURE_AUTHORITY_HOST`

.

## Supported Kubernetes and KEDA versions

Your cluster Kubernetes version determines which KEDA version is installed on your AKS cluster. To see which KEDA version maps to each AKS version, see the **AKS managed add-ons** column of the [Kubernetes component version table](supported-kubernetes-versions#aks-components-breaking-changes-by-version).

For GA Kubernetes versions, AKS offers full support of the corresponding KEDA minor version in the table. Kubernetes preview versions and the latest KEDA patch are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:
