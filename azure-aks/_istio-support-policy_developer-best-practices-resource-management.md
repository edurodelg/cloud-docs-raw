---
merged_at: 2026-01-25T12:25:33.902284
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: istio-support-policy.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-support-policy -->

# Support policy for Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article outlines the support policy for the Istio-based service mesh add-on for Azure Kubernetes Service (AKS).

## Versioning and support policy

### Service mesh add-on release calendar

The Istio-based service mesh add-on release calendar indicates each revision's AKS compatibility and estimated release and deprecation dates.

New minor revisions and patches are rolled out as part of AKS releases. Announcements about the releases of new minor revisions or patches to the Istio-based service mesh add-on are published in the [AKS release notes](https://github.com/Azure/AKS/releases). To see real-time updates of regional release status and AKS release notes containing updates about Istio revision support, visit the [AKS release status webpage](https://releases.aks.azure.com/).

| Service mesh revision | Upstream release | AKS release | End of life | Compatible AKS versions | Compatible AKS LTS versions |
|---|---|---|---|---|---|
| asm-1-17 | Feb 2023 | Apr 2023 | Jan 2024 | 1.23, 1.24, 1.25, 1.26, 1.27, 1.28 | |
| asm-1-18 | Jun 2023 | Nov 2023 | Feb 2024 | 1.24, 1.25, 1.26, 1.27, 1.28 | |
| asm-1-19 | Sept 2023 | Jan 2024 | Jun 2024 | 1.25, 1.26, 1.27, 1.28 | |
| asm-1-20 | Nov 2023 | Feb 2024 | Sept 2024 | 1.25, 1.26, 1.27, 1.28, 1.29 | |
| asm-1-21 | Mar 2024 | Apr 2024 | Oct 2024 | 1.26, 1.27, 1.28, 1.29, 1.30 | |
| asm-1-22 | May 2024 | Jul 2024 | March 2025 | 1.27, 1.28, 1.29, 1.30 | |
| asm-1-23 | Aug 2024 | Sept 2024 | June 2025 | 1.27, 1.28, 1.29, 1.30, 1.31, 1.32 | |
| asm-1-24 | Nov 2024 | Feb 2025 | Sept 2025 | 1.28, 1.29, 1.30, 1.31, 1.32, 1.33 | |
| asm-1-25 | Mar 2025 | May 2025 | Jan 2026 | 1.29, 1.30, 1.31, 1.32, 1.33 | 1.28, 1.29, 1.30, 1.31, 1.32, 1.33 |
| asm-1-26 | May 2025 | July 2025 | ~Feb 2026 (expected) | 1.29, 1.30, 1.31, 1.32, 1.33, 1.34 | 1.28, 1.29, 1.30, 1.31, 1.32, 1.33, 1.34 |
| asm-1-27 | Aug 2025 | Sept 2025 | ~May 2026 (expected) | 1.29, 1.30, 1.31, 1.32, 1.33, 1.34, 1.35 | 1.29, 1.30, 1.31, 1.32, 1.33, 1.34, 1.35 |
| asm-1-28 | Nov 2025 | Jan 2026 | ~Aug 2026 (expected) | 1.30, 1.31, 1.32, 1.33, 1.34, 1.35 | 1.30, 1.31, 1.32, 1.33, 1.34, 1.35 |

If using an AKS [long term-support (LTS) cluster](long-term-support), a newer revision may be declared as compatible when a previous compatible Istio revision reaches end of life before the AKS LTS version's end of life. For more details, read Istio's [AKS compatibility policy](#aks-compatibility).

### Supported revisions

**Minor revision**:- At any given time, at least two revisions of the Istio-based service mesh add-on are supported.
- An older revision
`n-2`

will continue to be supported until six weeks after the newest revision`n`

starts rolling out to all regions. For example, if`asm-1-22`

just started rolling out to all regions,`asm-1-20`

will be deprecated after six weeks. - Deprecation means no new mesh installations can be done with this revision. While clusters already having this revision continue to work, for support issues and security patches, it's recommended to
[upgrade to a newer supported mesh revision](istio-upgrade#minor-revision-upgrade).

**Patch version**:- Patches to Istio control plane (istiod) and Istio ingresses are rolled out as part of AKS releases. User is expected to follow AKS release notes on availability of newer patch versions and to then
[upgrade istio-proxy sidecars by restarting their workloads](istio-upgrade#patch-version-upgrade). - AKS reserves the right to deprecate patches if a critical Common Vulnerability and Exposure (CVE) or security vulnerability is detected. For awareness on patch availability and any ad-hoc deprecation, refer to
[AKS release notes](https://github.com/Azure/AKS/releases)and visit the[AKS release status webpage](https://releases.aks.azure.com/).

- Patches to Istio control plane (istiod) and Istio ingresses are rolled out as part of AKS releases. User is expected to follow AKS release notes on availability of newer patch versions and to then

### Default revision

If a revision isn't explicitly provided by user during installation, the `n-1`

revision is installed by default. For example, if `asm-1-22`

is the latest revision, the default is `asm-1-21`

.

### AKS compatibility

Each revision of the add-on is compatible with a set of AKS minor versions established by the [upstream Istio support and release calendar](https://istio.io/latest/docs/releases/supported-releases/#support-status-of-istio-releases).

**AKS LTS clusters may be compatible with additional revisions beyond upstream Istio's support table.** For Istio revisions `asm-1-25`

+ and AKS LTS versions 1.28+, every supported AKS LTS version will have *at least one* compatible Istio revision.

To check the compatible AKS versions for an Istio revision, use the command [ az aks mesh get-revisions](/en-us/cli/azure/aks/mesh#az-aks-mesh-get-revisions):

```
az aks mesh get-revisions --location <location> -o table
```


This command has been updated to include separate `CompatibleWith`

outputs for `KubernetesOfficial`

(standard tier) and `AKSLongTermSupport`

, replacing the earlier response that only included `kubernetes`

(standard tier).

If using the Azure portal to enable the Istio add-on for an existing cluster, the available Istio revisions will be filtered based on the cluster's tier.

Each Istio add-on revision follows upstream lifecycle for end of life and patch availability. This means:

Every Istio revision will not be compatible with every AKS LTS version, but every AKS LTS version will be compatible with at least one Istio add-on revision.

If an Istio revision reaches end of life before the AKS LTS version it is compatible with, a newer revision will be declared compatible with that LTS version. The add-on will need to be upgraded to stay in support.

For example, if

`asm-1-26`

is compatible with AKS LTS 1.28, and`asm-1-26`

reaches end of life,`asm-1-27`

may become compatible with 1.28 LTS instead.

## Allowed, supported, and blocked customizations

The Istio-based service mesh add-on for AKS designates features and [configuration options](istio-meshconfig#allowed-supported-and-blocked-meshconfig-values) as `allowed`

, `supported`

, or `blocked`

.

**Blocked**: Disallowed features and configuration options are blocked via add-on managed admission webhooks. The API server immediately publishes the error message to the user that the feature is disallowed.**Supported**: Supported features receive support from Azure support.**Allowed**: Allowed features are open and available to Istio add-on users but aren't covered by Azure support.


---

<!-- DOCUMENTO FUSIONADO: developer-best-practices-resource-management.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/developer-best-practices-resource-management -->

# Best practices for application developers to manage resources in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you develop and run applications in Azure Kubernetes Service (AKS), there are a few key areas to consider. The way you manage your application deployments can negatively impact the end-user experience of services you provide.

This article focuses on running your clusters and workloads from an application developer perspective. For information about administrative best practices, see [Cluster operator best practices for isolation and resource management in Azure Kubernetes Service (AKS)](operator-best-practices-cluster-isolation).

This article covers the following topics:

- Pod resource requests and limits.
- Ways to develop, debug, and deploy applications with Bridge to Kubernetes and Visual Studio Code.

## Define pod resource requests and limits


Best practice guidanceSet pod requests and limits on all pods in your YAML manifests. If the AKS cluster uses

resource quotasand you don't define these values, your deployment may be rejected.

Use pod requests and limits to manage compute resources within an AKS cluster. Pod requests and limits inform the Kubernetes scheduler of the compute resources to assign to a pod.

### Pod CPU/Memory requests

*Pod requests* define a set amount of CPU and memory the pod needs regularly.

In your pod specifications, it's important you define these requests and limits based on the above information. If you don't include these values, the Kubernetes scheduler can't consider the resources your applications require to help with scheduling decisions.

Monitor the performance of your application to adjust pod requests. If you underestimate pod requests, your application may receive degraded performance due to over-scheduling a node. If requests are overestimated, your application may have increased scheduling difficulty.

### Pod CPU/Memory limits

*Pod limits* set the maximum amount of CPU and memory a pod can use. *Memory limits* define which pods should be removed when nodes are unstable due to insufficient resources. Without proper limits set, pods are removed until resource pressure is lifted. While a pod may exceed the *CPU limit* periodically, the pod isn't removed for exceeding the CPU limit.

Pod limits define when a pod loses control of resource consumption. When it exceeds the limit, the pod is marked for removal. This behavior maintains node health and minimizes impact to pods sharing the node. If you don't set a pod limit, it defaults to the highest available value on a given node.

Avoid setting a pod limit higher than your nodes can support. Each AKS node reserves a set amount of CPU and memory for the core Kubernetes components. Your application may try to consume too many resources on the node for other pods to successfully run.

Monitor the performance of your application at different times during the day or week. Determine peak demand times and align the pod limits to the resources required to meet maximum needs.

Important

In your pod specifications, define these requests and limits based on the above information. Failing to include these values prevents the Kubernetes scheduler from accounting for resources your applications require to help with scheduling decisions.

If the scheduler places a pod on a node with insufficient resources, application performance is degraded. Cluster administrators **must set resource quotas** on a namespace that requires you to set resource requests and limits. For more information, see

[resource quotas on AKS clusters](operator-best-practices-scheduler#enforce-resource-quotas).

When you define a CPU request or limit, the value is measured in CPU units.

*1.0*CPU equates to one underlying virtual CPU core on the node.- The same measurement is used for GPUs.

- You can define fractions measured in millicores. For example,
*100 m*is*0.1*of an underlying vCPU core.

In the following basic example for a single NGINX pod, the pod requests *100 m* of CPU time and *128Mi* of memory. The resource limits for the pod are set to *250 m* CPU and *256Mi* memory.

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


For more information about resource measurements and assignments, see [Managing compute resources for containers](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/).

## Develop and debug applications against an AKS cluster


Best practice guidanceDevelopment teams should deploy and debug against an AKS cluster using Bridge to Kubernetes.


With Bridge to Kubernetes, you can develop, debug, and test applications directly against an AKS cluster. Developers within a team collaborate to build and test throughout the application lifecycle. You can continue to use existing tools such as Visual Studio or Visual Studio Code with the Bridge to Kubernetes extension.

Using integrated development and test process with Bridge to Kubernetes reduces the need for local test environments like [minikube](https://kubernetes.io/docs/setup/minikube/). Instead, you develop and test against an AKS cluster, even in secured and isolated clusters.

Note

Bridge to Kubernetes is intended for use with applications running on Linux pods and nodes.

## Use the Visual Studio Code (VS Code) extension for Kubernetes


Best practice guidanceInstall and use the VS Code extension for Kubernetes when you write YAML manifests. You can also use the extension for integrated deployment solution, which may help application owners that infrequently interact with the AKS cluster.


The [Visual Studio Code extension for Kubernetes](https://github.com/Azure/vscode-kubernetes-tools) helps you develop and deploy applications to AKS. The extension provides the following features:

Intellisense for Kubernetes resources, Helm charts, and templates.

The ability to browse, deploy, and edit capabilities for Kubernetes resources from within VS Code.

Intellisense checks for resource requests or limits being set in the pod specifications:


## Next steps

This article focused on how to run your cluster and workloads from a cluster operator perspective. For information about administrative best practices, see [Cluster operator best practices for isolation and resource management in Azure Kubernetes Service (AKS)](operator-best-practices-cluster-isolation).

To implement some of these best practices, see [Develop with Bridge to Kubernetes](/en-us/visualstudio/containers/overview-bridge-to-kubernetes).
