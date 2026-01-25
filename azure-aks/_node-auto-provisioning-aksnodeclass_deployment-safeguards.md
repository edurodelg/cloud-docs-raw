---
merged_at: 2026-01-25T12:25:33.964770
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: node-auto-provisioning-aksnodeclass.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-aksnodeclass -->

# Configure AKSNodeClass resources for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure `AKSNodeClass`

resources to define Azure-specific settings for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS) using Karpenter. `AKSNodeClass`

allows you to customize various aspects of the nodes that Karpenter provisions, such as the virtual machine (VM) image, operating system (OS) disk size, maximum pods per node, and kubelet configurations.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Overview of AKSNodeClass resources

`AKSNodeClass`

resources enable you to configure Azure-specific settings for NAP. Each [ NodePool resource](node-auto-provisioning-node-pools) must reference an

`AKSNodeClass`

using `spec.template.spec.nodeClassRef`

. You can have multiple `NodePools`

that point to the same `AKSNodeClass`

, allowing you to share common Azure configurations across different node pools.## Image family configuration

The `imageFamily`

field dictates the default VM image and bootstrapping logic for nodes provisioned through the `AKSNodeClass`

. If you don't specify an image family, the default is `Ubuntu2204`

. GPUs are supported with both image families on compatible VM sizes.

### Supported image families

: Ubuntu 22.04 Long Term Support (LTS) is the default Linux distribution for AKS nodes.`Ubuntu`

: Azure Linux is Microsoft's alternative Linux distribution for AKS workloads. For more information, see the`AzureLinux`

[Azure Linux documentation](/en-us/azure/aks/use-azure-linux)

#### Example image family configuration

The following example configures the `AKSNodeClass`

to use the `AzureLinux`

image family:

```
spec:
imageFamily: AzureLinux
```


#### FIPS compliant node image configuration

You can enable Federal Information Process Standard (FIPS) compliant node images also. For more in FIPS in AKS, visit our [FIPS documentation](enable-fips-nodes)

The `fipsMode`

field is set by default to Disabled, and can be set to the following options:

- FIPS - select FIPS-compliant node images
- Disabled - do not use FIPS-compliant node images

The following example configures the 'AKSNodeClass' to select FIPS-compliant node images by setting `fipsMode`

to `FIPS`

:

```
spec:
fipsMode: FIPS
```


## Virtual network (VNet) subnet configuration

The `vnetSubnetID`

field specifies which Azure VNet subnet should be used for provisioning node network interfaces. This field is optional. If you don't specify a subnet, NAP uses the default subnet configured during Karpenter installation. For more information, see [Subnet configurations for NAP](node-auto-provisioning-networking#subnet-configurations-for-nap).

### Example subnet configuration

The subnet ID must be in the full Azure Resource Manager (ARM) format, as shown in the following example:

```
spec:
vnetSubnetID: "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Network/virtualNetworks/{vnet-name}/subnets/{subnet-name}"
```


## OS disk size configuration

The `osDiskSizeGB`

field specifies the size of the OS disk in gigabytes. The default value is 128 GB, and the minimum value is 30 GB.

Consider larger OS disk sizes for workloads that:

- Store significant data locally.
- Require extra space for container images.
- Have high disk I/O requirements.

### Example OS disk size configuration

```
spec:
osDiskSizeGB: 256 # 256 GB OS disk
```


## Ephemeral OS disk configuration

NAP automatically uses [Ephemeral OS disks](/en-us/azure/virtual-machines/ephemeral-os-disks) when available and suitable for the requested disk size. Ephemeral OS disks provide better performance and lower cost compared to managed disks.

### Ephemeral disk selection criteria

The system automatically chooses Ephemeral disks in the following scenarios:

- The VM instance type supports Ephemeral OS disks.
- The Ephemeral disk capacity is greater than or equal to the requested
`osDiskSizeGB`

. - The VM has sufficient ephemeral storage capacity.

If these conditions aren't met, the system falls back to using managed disks.

### Ephemeral disk types and prioritization

Azure VMs can have different types of ephemeral storage. The system uses the following priority order:

**NVMe disks**(highest performance)**Cache disks**(balanced performance)**Resource disks**(basic performance)

### Example ephemeral disk configuration

You can use node pool requirements to ensure nodes have sufficient ephemeral disk capacity, as shown in the following example:

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: ephemeral-disk-pool
spec:
template:
spec:
requirements:
- key: karpenter.azure.com/sku-storage-ephemeralos-maxsize
operator: Gt
values: ["128"] # Require ephemeral disk larger than 128 GB
nodeClassRef:
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
name: my-node-class
---
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: my-node-class
spec:
osDiskSizeGB: 128 # This will use ephemeral disk if available and large enough
```


This configuration ensures that only VM instance types with ephemeral disks larger than 128 GB are selected, guaranteeing ephemeral disk usage for the specified OS disk size.

## Maximum pods configuration

The `maxPods`

field specifies the maximum number of pods that can be scheduled on a node. This setting affects both cluster density and network configuration.

The minimum value for `maxPods`

is 10, and the maximum value is 250.

### Default behavior for `maxPods`


The default behavior for `maxPods`

depends on the network plugin configuration. The following table summarizes the defaults:

| Network plugin configuration | Default `maxPods` per node |
|---|---|
| Azure CNI with standard networking (v1 or NodeSubnet) | 30 |
| Azure CNI with overlay networking | 250 |
| None (no network plugin) | 250 |
| Other configurations | 110 (standard Kubernetes default) |

### Example maximum pods configuration

```
spec:
maxPods: 50 # Allow up to 50 pods per node
```


## LocalDNS configuration

LocalDNS deploys a node level DNS proxy that resolves DNS queries closer to workloads, reducing query latency and improving resiliency during transient DNS disruptions. For more information, see the [LocalDNS documentation](localdns-custom). By default, LocalDNS is set to Disabled and can be configured to the following options:

`Disabled`

(default) - Disables the LocalDNS feature. DNS queries aren't resolved locally on the node.`Preferred`

- AKS manages LocalDNS enablement based on the Kubernetes version of the node pool. The configuration is always validated and included, but LocalDNS isn't enabled unless the correct Kubernetes version is used.`Required`

- LocalDNS is enforced on the node pool if all prerequisites are satisfied. If the requirements aren't met, the deployment fails.

### Example LocalDNS configuration

You can customize LocalDNS configurations such as `vnetDNSOverrides`

and `kubeDNSOverrides`

. For more details on the supported plugins, see [Customize LocalDNS](localdns-custom).

```
spec:
LocalDNS:
mode: Required
vnetDNSOverrides:
- zone: "."
cacheDuration: "30s"
forwardDestination: VnetDNS
forwardPolicy: Random
maxConcurrent: 80
protocol: ForceTCP
queryLogging: Log
serveStale: Immediate
serveStaleDuration: "100s"
- zone: "cluster.local"
cacheDuration: "40s"
forwardDestination: VnetDNS
forwardPolicy: Sequential
maxConcurrent: 70
protocol: PreferUDP
queryLogging: Error
serveStale: Disable
serveStaleDuration: "30s"
kubeDNSOverrides:
- zone: "."
cacheDuration: "30s"
forwardDestination: ClusterCoreDNS
forwardPolicy: RoundRobin
maxConcurrent: 100
protocol: PreferUDP
queryLogging: Log
serveStale: Immediate
serveStaleDuration: "60s"
- zone: "cluster.local"
cacheDuration: "10s"
forwardDestination: ClusterCoreDNS
forwardPolicy: Sequential
maxConcurrent: 50
protocol: PreferUDP
queryLogging: Error
serveStale: Disable
serveStaleDuration: "30s"
```


## Kubelet configuration

The `kubelet`

section allows you to configure various kubelet parameters that affect node behavior. These parameters are typical kubelet arguments, so the Azure provider simply passes them through to the kubelet on the node.

Important

**Configure kubelet settings carefully**, and test any changes in nonproduction environments first.

### CPU management

The following settings control CPU management behavior for the kubelet:

```
spec:
kubelet:
cpuManagerPolicy: "static" # or "none"
cpuCFSQuota: true
cpuCFSQuotaPeriod: "100ms"
```


`cpuManagerPolicy`

: Controls how the kubelet allocates CPU resources. Set to`"static"`

for CPU pinning in latency-sensitive workloads.`cpuCFSQuota`

: Enables CPU Completely Fair Scheduler (CFS) quota enforcement for containers that specify CPU limits.`cpuCFSQuotaPeriod`

: Sets the CPU CFS quota period.

### Image garbage collection

The following settings control image garbage collection behavior for the kubelet:

```
spec:
kubelet:
imageGCHighThresholdPercent: 85
imageGCLowThresholdPercent: 80
```


These settings control when the kubelet performs garbage collection of container images:

`imageGCHighThresholdPercent`

: Disk usage percentage that triggers image garbage collection.`imageGCLowThresholdPercent`

: Target disk usage percentage after garbage collection.

### Topology management

The following setting controls the topology manager policy for the kubelet:

```
spec:
kubelet:
topologyManagerPolicy: "best-effort" # none, restricted, best-effort, single-numa-node
```


The topology manager helps coordinate resource allocation for latency-sensitive workloads across CPU and device (like GPU) resources.

### System configuration

The following settings allow you to configure extra system parameters for the kubelet:

```
spec:
kubelet:
allowedUnsafeSysctls:
- "kernel.msg*"
- "net.ipv4.route.min_pmtu"
containerLogMaxSize: "50Mi"
containerLogMaxFiles: 5
podPidsLimit: 4096
```


`allowedUnsafeSysctls`

: List of permitted unsafe sysctls that pods can use.`containerLogMaxSize`

: Maximum size of container log files before rotation.`containerLogMaxFiles`

: Maximum number of container log files to retain.`podPidsLimit`

: Maximum number of processes allowed in any pod.

## Azure resource tags configuration

You can specify Azure resource tags that apply to all VM instances created using a particular `AKSNodeClass`

resource. Tags are useful for cost tracking, resource organization, and compliance requirements.

### Tag limitations

- Azure resource tags have a limit of 50 tags per resource.
- Tag names are case-insensitive but tag values are case-sensitive.
- Azure reserves some tag names that can't be used. For more information, see
[Tag guidance and limits](/en-us/azure/azure-resource-manager/management/tag-resources#tag-restrictions).

### Example tags configuration

```
spec:
tags:
Environment: "production"
Team: "platform"
Application: "web-service"
CostCenter: "engineering"
```


## Comprehensive `AKSNodeClass`

configuration example

The following example demonstrates a comprehensive `AKSNodeClass`

configuration that includes all the settings discussed in this article:

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
template:
spec:
nodeClassRef:
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
name: comprehensive-example
---
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: comprehensive-example
spec:
# Image family configuration
# Default: Ubuntu
# Valid values: Ubuntu, AzureLinux
imageFamily: Ubuntu
# FIPS compliant mode - allows support for FIPS-compliant node images
# Default: Disabled
# Valid values: FIPS, Disabled
fipsMode: Disabled
# LocalDNS mode - allows use of LocalDNS feature
# Default: Disabled
# Valid values: Preferred, Required, Disabled
LocalDNS:
mode: Disabled
# additional details on vnetDNSOverrides and kubeDNSOverrides can be added here
# Virtual network subnet configuration (optional)
# If not specified, uses the default --vnet-subnet-id from Karpenter installation
vnetSubnetID: "/subscriptions/12345678-1234-1234-1234-123456789012/resourceGroups/my-rg/providers/Microsoft.Network/virtualNetworks/my-vnet/subnets/my-subnet"
# OS disk size configuration
# Default: 128 GB
# Minimum: 30 GB
osDiskSizeGB: 128
# Maximum pods per node configuration
# Default behavior depends on network plugin:
# - Azure CNI with standard networking: 30 pods
# - Azure CNI with overlay networking: 250 pods
# - Other configurations: 110 pods
# Range: 10-250
maxPods: 30
# Azure resource tags (optional)
# Applied to all VM instances created with this AKSNodeClass
tags:
Environment: "production"
Team: "platform-team"
Application: "web-service"
CostCenter: "engineering"
# Kubelet configuration (optional)
# All fields are optional with sensible defaults
kubelet:
# CPU management policy
# Default: "none"
# Valid values: none, static
cpuManagerPolicy: "static"
# CPU CFS quota enforcement
# Default: true
cpuCFSQuota: true
# CPU CFS quota period
# Default: "100ms"
cpuCFSQuotaPeriod: "100ms"
# Image garbage collection thresholds
# imageGCHighThresholdPercent must be greater than imageGCLowThresholdPercent
# Range: 0-100
imageGCHighThresholdPercent: 85
imageGCLowThresholdPercent: 80
# Topology manager policy
# Default: "none"
# Valid values: none, restricted, best-effort, single-numa-node
topologyManagerPolicy: "best-effort"
# Allowed unsafe sysctls (optional)
# Comma-separated list of unsafe sysctls or patterns
allowedUnsafeSysctls:
- "kernel.msg*"
- "net.ipv4.route.min_pmtu"
# Container log configuration
# containerLogMaxSize default: "50Mi"
containerLogMaxSize: "50Mi"
# containerLogMaxFiles default: 5, minimum: 2
containerLogMaxFiles: 5
# Pod process limits
# Default: -1 (unlimited)
podPidsLimit: 4096
```


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: deployment-safeguards.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/deployment-safeguards -->

# Use Deployment Safeguards to enforce best practices in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Deployment Safeguards to enforce best practices on an Azure Kubernetes Service (AKS) cluster.

## Overview

Note

Deployment Safeguards is turned on by default in AKS Automatic.

Throughout the development lifecycle, it is common for bugs, issues, and other problems to arise if the initial deployment of your Kubernetes resources includes misconfigurations. To ease the burden of Kubernetes development, Azure Kubernetes Service (AKS) offers Deployment Safeguards. Deployment Safeguards enforce Kubernetes best practices in your AKS cluster through Azure Policy controls.

Deployment Safeguards offer two levels of configuration:

`Warn`

: Displays warning messages in the code terminal to alert you of any noncompliant cluster configurations but still allows the request to go through.`Enforce`

: Enforces compliant configurations by denying and mutating deployments if they don't follow best practices.

After you configure Deployment Safeguards for 'Warn' or 'Enforce', Deployment Safeguards programmatically assess your Kubernetes resources at creation or update time for compliance. Deployment Safeguards also display aggregated compliance information across your workloads at a per resource level via Azure Policy's compliance dashboard in the [Azure portal](https://portal.azure.com/#view/Microsoft_Azure_Policy/PolicyMenuBlade/%7E/Compliance) or in your CLI or terminal. Running a noncompliant workload indicates that your cluster is not following best practices and that workloads on your cluster are at risk of experiencing issues caused by your cluster configuration.

## Prerequisites

Note

Cluster admins don't need Azure Policy permissions to enable or disable Deployment Safeguards. However, it's required to have the Azure Policy add-on installed.

- You need to enable the Azure Policy add-on for AKS. For more information, see
[Enable Azure Policy on your AKS cluster](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks). This includes registering the`Microsoft.PolicyInsights`

resource provider in your subscription.

## Deployment Safeguards policies

The following table lists the policies that become active and the Kubernetes resources they target when you enable Deployment Safeguards. You can view the [currently available Deployment Safeguards](https://portal.azure.com/#view/Microsoft_Azure_Policy/InitiativeDetail.ReactView/id/%2Fproviders%2FMicrosoft.Authorization%2FpolicySetDefinitions%2Fc047ea8e-9c78-49b2-958b-37e56d291a44/scopes/) in the Azure portal as an Azure Policy definition or at [Azure Policy built-in definitions for Azure Kubernetes Service](/en-us/azure/aks/policy-reference#policy-definitions). The intention behind this collection is to create a common and generic list of best practices applicable to most users and use cases.

| Deployment safeguard policy | Mutation outcome if available |
|---|---|
| Cannot Edit Individual Nodes | N/A |
| Kubernetes cluster containers CPU and memory resource limits shouldn't exceed the specified limits | Sets CPU resource limits to 500m if not set and sets memory limits to 500Mi if no path is present |
| Must Have Anti Affinity Rules or topologySpreadConstraintsSet | N/A |
| No AKS Specific Labels | N/A |
| Kubernetes cluster containers should only use allowed images | N/A |
| Reserved System Pool Taints | Removes the `CriticalAddonsOnly` taint from a user node pool if not set. AKS uses the `CriticalAddonsOnly` taint to keep customer pods away from the system pool. This configuration ensures a clear separation between AKS components and customer pods and prevents eviction of customer pods that don't tolerate the `CriticalAddonsOnly` taint. |
| Ensure cluster containers have readiness or liveness probes configured | N/A |
| Kubernetes clusters should use Container Storage Interface (CSI) driver StorageClass | N/A |
| Kubernetes cluster services should use unique selectors | N/A |
| Kubernetes cluster container images should not include latest image tag | N/A |

If you want to submit an idea or request for Deployment Safeguards, open an issue in the [AKS GitHub repository](https://github.com/Azure/AKS) and add `[Deployment Safeguards request]`

to the beginning of the title.

## Pod Security Standards in Deployment Safeguards

Note

Baseline Pod Security Standards are now turned on by default in AKS Automatic. The baseline Pod Security Standards in AKS Automatic can't be turned off.

Deployment Safeguards also supports the ability to turn on [Baseline, Restricted and Privileged Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/). To ensure your workloads deploy successfully, make sure each manifest complies with the Baseline or Restricted Pod Security requirements. By default, Azure Kubernetes Service uses Privileged Pod Security Standards.

| Policy | Error Message | Fix |
|---|---|---|
| AppArmor | `AppArmor annotation values must be undefined/nil, runtime/default, or localhost/*` or `AppArmor profile type must be one of: undefined/nil, RuntimeDefault, or Localhost` |
Remove any specification of AppArmor. Kubernetes by default applies apparmor settings. "On supported hosts, the RuntimeDefault AppArmor profile is applied by default". |
| Host Namespaces | `Host network namespaces are disallowed: spec.hostNetwork is set to true'` or `'Host PID namespaces are disallowed: spec.hostPID is set to true'` or `'Host IPC namespaces are disallowed: spec.hostIPC is set to true'` |
Set those values to false, or remove specifying the fields. |
| Privileged Containers | `'Privileged [ephemeral\|init\|N/A] containers are disallowed: spec.containers[*].securityContext.privileged is set to true'` |
Set the appropriate securityContext.privileged field to false, or remove the field. |
| Capabilities | Message will start with `'Disallowed capabilities detected` |
Remove the capability shown from the container's manifest. |
| HostPath volumes | `HostPath volumes are forbidden under restricted security policy unless containers mounting them are from allowed images` |
Remove the HostPath volume and volume mount. |
| Host Ports | HostPorts are forbidden under baseline security policy | Remove the host port specification from the offending container. |
| SELinux | `SELinux type must be one of: undefined/empty, container_t, container_init_t, container_kvm_t, or container_engine_t` |
Set the container's securityContext.seLinuxOptions.type field to one of the allowed values. |
| /proc Mount Type | ProcMount must be undefined/nil or 'Default' in spec.containers[*].securityContext.procMount | Set "* `spec.containers[*].securityContext.procMount` " to 'Default' or have it be undefined. |
| Seccomp | `Seccomp profile must not be explicitly set to Unconfined. Allowed values are: undefined/nil, RuntimeDefault, or Localhost` |
Set `securityContext.seccompProfile.type` on the pod or containers to one of the allowed values. |
| Sysctls | `Disallowed sysctl detected. Only baseline Kubernetes pod security standard sysctls are permitted` |
Remove the disallowed systctls( see the
|

`Only the following volume types are allowed under restricted policy: configMap, csi, downwardAPI, emptyDir, ephemeral, persistentVolumeClaim, projected, secret`

`Privilege escalation must be set to false under restricted policy`

`* `

spec.containers[*].securityContext.allowPrivilegeEscalation`` must explicitly be set to false for each container, initContainer, and ephemeralContainer.`Containers must not run as root user in spec.containers[*].securityContext.runAsNonRoot`

`'Containers must not run as root user: spec.securityContext.runAsUser is set to 0'`

`Seccomp profile must be "RuntimeDefault" or "Localhost" under restricted policy`

`securityContext.seccompProfile.type`

on the pod or containers to one of the allowed values. This differs from the baseline in the fact that the restricted policy doesn't allow an undefined value.`All containers must drop ALL capabilities under restricted policy`

or `Only NET_BIND_SERVICE may be added to capabilities under restricted policy`

## Enable Deployment Safeguards

Note

Using the Deployment Safeguards `Enforce`

level means you're opting in to deployments being blocked and mutated. Consider how these policies might work with your AKS cluster before enabling `Enforce`

.

### Enable Deployment Safeguards on an existing cluster

Enable Deployment Safeguards on an existing cluster that has the Azure Policy add-on enabled using the `az aks safeguard create`

command with the `--level`

flag. If you want to receive noncompliance warnings, set the `--level`

to `Warn`

. If you want to deny or mutate all noncompliant deployments, set it to `Enforce`

.

```
az aks safeguards create --resource-group <resource-group-name> --name <cluster-name> --level Enforce
```


You can also enable Deployment Safeguards by using the `--cluster`

flag and specifying the cluster resource ID.

```
az aks safeguards create --cluster <ID> --level Enforce
```


If you want to update the Deployment Safeguards level of an existing cluster, run the following command with the new value for `--level`

.

```
az aks safeguards update --resource-group <resource-group-name> --name <cluster-name> --level Warn
```


### Excluding namespaces

You can also exclude certain namespaces from Deployment Safeguards. When you exclude a namespace, activity in that namespace is unaffected by Deployment Safeguards warnings or enforcement.

For example, to exclude the namespaces `ns1`

and `ns2`

, use a space separated list of namespaces with the `--excluded-ns`

flag, as shown in the following example:

```
az aks safeguards update --resource-group <resource-group-name> --name <cluster-name> --level Warn --excluded-ns ns1 ns2
```


### Turn on Pod Security Standards

Note

Azure Kubernetes Service (AKS) uses `Privileged`

Pod Security Standards by default. If you want to revert to the default configuration, set the `--pss-level`

flag to `Privileged`

.

To enable Pod Security Standards in Deployment Safeguards, use the `--pss-level`

flag to select one of the following levels: `Baseline`

, `Restricted`

, or `Privileged`

.

```
az aks safeguards update --resource-group <resource-group-name> --name <cluster-name> --level Warn --pss-level <Baseline|Restricted|Privileged>
```


### Update your Deployment Safeguard version

Deployment Safeguards adhere to the [AKS addon versioning scheme](supported-kubernetes-versions). Each new version of a Deployment Safeguard will be released as a new minor version in AKS. These updates will be communicated through the [AKS GitHub release notes](https://github.com/Azure/AKS/releases) and reflected in the "Deployment Safeguards Policies" table in our documentation.

To learn more about AKS versioning and addons, refer to the following documentation: [aks-component-versions](supported-kubernetes-versions) and [aks-versioning-for-addons](integrations#add-ons).

## Verify compliance across clusters

After deploying your Kubernetes manifest, you see warnings or a potential denial message in your CLI or terminal if the cluster isn't compliant with Deployment Safeguards, as shown in the following examples:

**Warn**

```
$ kubectl apply -f deployment.yaml
Warning: [azurepolicy-k8sazurev1antiaffinityrules-ceffa082711831ebffd1] Deployment with 2 replicas should have either podAntiAffinity or topologySpreadConstraints set to avoid disruptions due to nodes crashing
deployment.apps/simple-web created
```


**Enforce**

With Deployment Safeguard mutations, the `Enforce`

level mutates your Kubernetes resources when applicable. However, your Kubernetes resources still need to pass all safeguards to deploy successfully. If any safeguard policies fail, your resource is denied and won't be deployed.

```
$ kubectl apply -f deployment.yaml
Error from server (Forbidden): error when creating "deployment.yaml": admission webhook "validation.gatekeeper.sh" denied the request: [azurepolicy-k8sazurev1antiaffinityrules-ceffa082711831ebffd1] Deployment with 2 replicas should have either podAntiAffinity or topologySpreadConstraints set to avoid disruptions due to nodes crashing
```


If your Kubernetes resources comply with the applicable mutation safeguards and meet all other safeguard requirements, they'll be successfully deployed, as shown in the following example:

```
$ kubectl apply -f deployment.yaml
deployment.apps/simple-web created
```


## Verify compliance across clusters using the Azure Policy dashboard

To verify Deployment Safeguards have been applied and to check on your cluster's compliance, navigate to the Azure portal page for your cluster and select **Policies**, then select **go to Azure Policy**.

From the list of policies and initiatives, select the initiative associated with Deployment Safeguards. You see a dashboard showing compliance state across your AKS cluster.

Note

To properly assess compliance across your AKS cluster, the Azure Policy initiative must be scoped to your cluster's resource group.

## Disable Deployment Safeguards

To disable Deployment Safeguards on your cluster, use the `delete`

command.

```
az aks safeguards delete --resource-group <resource-group-name> --name <cluster-name>
```


## FAQ

#### Can I create my own mutations?

No. If you have an idea for a safeguard, open an issue in the [AKS GitHub repository](https://github.com/Azure/AKS) and add `[Deployment Safeguards request]`

to the beginning of the title.

#### Can I pick and choose which mutations I want in Enforcement?

No. Deployment Safeguards is all or nothing. Once you turn on Warn or Enforce, all safeguards are active.

#### Why did my deployment resource get admitted even though it wasn't following best practices?

Deployment Safeguards enforce best practice standards through Azure Policy controls and has policies that validate against Kubernetes resources. To evaluate and enforce cluster components, Azure Policy extends [Gatekeeper](https://open-policy-agent.github.io/gatekeeper/website/). Gatekeeper enforcement also currently operates in a [ fail-open model](https://open-policy-agent.github.io/gatekeeper/website/docs/failing-closed/#considerations). As there's no guarantee that Gatekeeper responds to our networking call, we make sure that in that case, the validation is skipped so that the deny doesn't block your deployments.

To learn more, see [workload validation in Gatekeeper](https://open-policy-agent.github.io/gatekeeper/website/docs/workload-resources/).

## Next steps

- Learn more about
[best practices](best-practices)for operating an AKS cluster.
