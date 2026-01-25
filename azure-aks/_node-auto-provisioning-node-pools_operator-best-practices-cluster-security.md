---
merged_at: 2026-01-25T12:06:27.798650
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: node-auto-provisioning-node-pools.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-node-pools -->

# Configure node pools for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure node pools for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS), including SKU selectors, resource limits, and priority weights. It also provides examples to help you get started.

## Overview of node pools in NAP

NAP uses virtual machine (VM) SKU requirements to decide the best VMs for pending workloads. You can configure:

- SKU families and specific instance types.
- Resource limits and priorities.
- Spot or On-demand instances.
- Architecture and capabilities requirements.

The `NodePool`

resource sets constraints on the nodes that NAP creates and the pods that run on those nodes. When you first install NAP, it creates a [default NodePool](#review-default-node-pool-configuration). You can modify this node pool or create extra node pools to suit your workload requirements.

## Key behaviors of `NodePools`

in NAP

When configuring `NodePools`

for NAP, keep the following behaviors in mind:

- NAP requires at least one
`NodePool`

to function. - NAP evaluates each configured
`NodePool`

. - NAP skips
`NodePools`

with taints not tolerated by a pod. - NAP applies startup taints to provisioned nodes but doesn't require pod toleration.
- NAP works best with mutually exclusive
`NodePools`

. When multiple`NodePools`

match, it uses the one with highest weight.

## Review default node pool configuration

The configuration of the default [Karpenter NodePool](https://karpenter.sh/docs/concepts/nodepools/) named

`default`

created by NAP is as follows:```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
disruption:
consolidationPolicy: WhenEmptyOrUnderutilized
template:
spec:
nodeClassRef:
name: default
expireAfter: Never
# Requirements that constrain the parameters of provisioned nodes.
# These requirements are combined with pod.spec.affinity.nodeAffinity rules.
# Operators { In, NotIn, Exists, DoesNotExist, Gt, and Lt } are supported.
# https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#operators
requirements:
- key: kubernetes.io/arch
operator: In
values:
- amd64
- key: kubernetes.io/os
operator: In
values:
- linux
- key: karpenter.sh/capacity-type
operator: In
values:
- on-demand
- key: karpenter.azure.com/sku-family
operator: In
values:
- D
```


It also creates a `system-surge`

node pool, which helps to autoscale system pool nodes.

## Control configuration of default node pool during cluster creation

When you [create a new AKS cluster enabled with NAP using the Azure CLI](use-node-auto-provisioning#enable-nap-on-a-new-cluster), you can include the `--node-provisioning-default-pools`

flag to control the configuration of the default NAP `NodePool`

.

The `--node-provisioning-default-pools`

flag controls the default NAP `NodePool`

configuration and accepts the following values:

(default): Creates two standard`Auto`

`NodePools`

for immediate use.: Doesn't create any`None`

`NodePools`

. You must define your own.

Warning

**Changing from Auto to None**: If you change the setting from


`Auto`

to `None`

on an existing cluster, the default `NodePools`

aren't deleted automatically. You must delete them manually if you no longer need them.## Node pool configuration options

The following sections outline various configuration options for `NodePools`

in NAP, including [well-known labels and SKU selectors](#well-known-labels-and-sku-selectors), [node pool limits](#node-pool-limits), and [node pool weights](#node-pool-weights).

### Well-known labels and SKU selectors

Kubernetes defines [well-known labels](https://kubernetes.io/docs/reference/labels-annotations-taints/) that Azure implements. You can define these labels in the `spec.requirements`

section of the `NodePool`

API. NAP also supports Azure-specific labels for more advanced scheduling.

`karpenter.azure.com`

SKU selectors

The following table lists the `karpenter.azure.com`

SKU selectors you can use in the `spec.requirements`

section of your `NodePool`

API to define VM characteristics for your nodes:

| Selector | Description | Example |
|---|---|---|
`karpenter.azure.com/sku-family` |
VM SKU family | D, F, L, etc. |
`karpenter.azure.com/sku-name` |
Explicit SKU name | Standard_A1_v2 |
`karpenter.azure.com/sku-version` |
SKU version (without "v", can use 1) | 1, 2 |
`karpenter.sh/capacity-type` |
VM allocation type (Spot / On-demand) | Spot |
`karpenter.azure.com/sku-cpu` |
Number of CPUs in VM | 16 |
`karpenter.azure.com/sku-memory` |
Memory in VM in MiB | 131072 |
`kubernetes.azure.com/sku-cpu` |
Number of CPUs in VM | 16 |
`kubernetes.azure.com/sku-memory` |
Memory in VM in MiB | 131072 |
`karpenter.azure.com/sku-gpu-name` |
GPU name | A100 |
`karpenter.azure.com/sku-gpu-manufacturer` |
GPU manufacturer | nvidia |
`karpenter.azure.com/sku-gpu-count` |
GPU count per VM | 2 |
`karpenter.azure.com/sku-networking-accelerated` |
Whether the VM has accelerated networking | [true, false] |
`karpenter.azure.com/sku-storage-premium-capable` |
Whether the VM supports Premium IO storage | [true, false] |
`karpenter.azure.com/sku-storage-ephemeralos-maxsize` |
Size limit for the Ephemeral operating system (OS) disk in Gb | 92 |

`kubernetes.io`

well-known labels

The following table lists the `kubernetes.io`

well-known labels you can use in the `spec.requirements`

section of your `NodePool`

API to define node characteristics for your nodes:

| Label | Description | Example |
|---|---|---|
`topology.kubernetes.io/zone` |
Availability zone(s) | [uksouth-1,uksouth-2,uksouth-3] |
`kubernetes.io/os` |
Operating system | linux |
`kubernetes.io/arch` |
CPU architecture (AMD64 or ARM64) | [amd64, arm64] |

#### SKU family examples

The `karpenter.azure.com/sku-family`

selector allows you to target specific VM families.

| Family | Description |
|---|---|
| D-series | General-purpose VMs with balanced CPU-to-memory ratio |
| F-series | Compute-optimized VMs with high CPU-to-memory ratio |
| E-series | Memory-optimized VMs for memory-intensive applications |
| L-series | Storage-optimized VMs with high disk throughput |
| N-series | GPU-enabled VMs for compute-intensive workloads |

Example configuration using SKU family:

```
requirements:
- key: karpenter.azure.com/sku-family
operator: In
values:
- D
- F
```


#### SKU name examples

The `karpenter.azure.com/sku-name`

selector allows you to specify the exact VM instance type.

```
requirements:
- key: karpenter.azure.com/sku-name
operator: In
values:
- Standard_D4s_v3
- Standard_F8s_v2
```


#### SKU version examples

The `karpenter.azure.com/sku-version`

selector targets specific generations of VM SKUs.

```
requirements:
- key: karpenter.azure.com/sku-version
operator: In
values:
- "3" # v3 generation
- "5" # v5 generation
```


#### Availability zone example

The `topology.kubernetes.io/zone`

selector allows you to specify the availability zones for your nodes.

```
requirements:
- key: topology.kubernetes.io/zone
operator: In
values:
- eastus-1
- eastus-2
```


Note

You can find available zones for your region using the `az account list-locations --output table`

Azure CLI command.

#### Architecture example

The `kubernetes.io/arch`

selector allows you to specify the CPU architecture for your nodes. NAP supports both `amd64`

and `arm64`

nodes.

```
requirements:
- key: kubernetes.io/arch
operator: In
values:
- amd64
- arm64
```


#### OS example

The `kubernetes.io/os`

selector allows you to specify the operating system for your nodes.

```
requirements:
- key: kubernetes.io/os
operator: In
values:
- linux
```


#### Capacity type example

The `karpenter.sh/capacity-type`

selector allows you to specify whether to use Spot or On-demand instances.

Note

NAP prioritizes Spot instances when both Spot and On-demand are specified.

```
requirements:
- key: karpenter.sh/capacity-type
operator: In
values:
- spot
- on-demand
```


### Node pool limits

By default, NAP attempts to schedule your workloads within the Azure quota you have available. You can also specify the upper limit of resources that a node pool uses by specifying limits within the node pool spec. For example:

```
spec:
# Resource limits constrain the total size of the cluster.
# Limits prevent Node Auto Provisioning from creating new instances once the limit is exceeded.
limits:
cpu: "1000"
memory: 1000Gi
```


### Node pool weights

When you have multiple node pools defined, you can set a preference of where a workload should be scheduled by defining the relative weight in your node pool definitions. For example:

```
spec:
# Priority given to the node pool when the scheduler considers which to select.
# Higher weights indicate higher priority when comparing node pools.
# Specifying no weight is equivalent to specifying a weight of 0.
weight: 10
```


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: operator-best-practices-cluster-security.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-cluster-security -->

# Best practices for cluster security and upgrades in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you manage clusters in Azure Kubernetes Service (AKS), workload and data security is a key consideration. When you run multi-tenant clusters using logical isolation, you especially need to secure resource and workload access. Minimize the risk of attack by applying the latest Kubernetes and node OS security updates.

This article focuses on how to secure your AKS cluster. You learn how to:

- Use Microsoft Entra ID and Kubernetes role-based access control (Kubernetes RBAC) to secure API server access.
- Secure container access to node resources.
- Upgrade an AKS cluster to the latest Kubernetes version.
- Keep nodes up to date and automatically apply security patches.

You can also read the best practices for [container image management](operator-best-practices-container-image-management) and for [pod security](developer-best-practices-pod-security).

## Enable threat protection


Best practice guidanceYou can enable

[Defender for Containers]to help secure your containers. Defender for Containers can assess cluster configurations and provide security recommendations, run vulnerability scans, and provide real-time protection and alerting for Kubernetes nodes and clusters.

## Secure access to the API server and cluster nodes


Best practice guidanceOne of the most important ways to secure your cluster is to secure access to the Kubernetes API server. To control access to the API server, integrate Kubernetes RBAC with Microsoft Entra ID. With these controls,you secure AKS the same way that you secure access to your Azure subscriptions.


The Kubernetes API server provides a single connection point for requests to perform actions within a cluster. To secure and audit access to the API server, limit access and provide the lowest possible permission levels. while this approach isn't unique to Kubernetes, it's especially important when you've logically isolated your AKS cluster for multi-tenant use.

Microsoft Entra ID provides an enterprise-ready identity management solution that integrates with AKS clusters. Since Kubernetes doesn't provide an identity management solution, you may be hard-pressed to granularly restrict access to the API server. With Microsoft Entra integrated clusters in AKS, you use your existing user and group accounts to authenticate users to the API server.

Using Kubernetes RBAC and Microsoft Entra ID-integration, you can secure the API server and provide the minimum permissions required to a scoped resource set, like a single namespace. You can grant different Microsoft Entra users or groups different Kubernetes roles. With granular permissions, you can restrict access to the API server and provide a clear audit trail of actions performed.

The recommended best practice is to use *groups* to provide access to files and folders instead of individual identities. For example, use a Microsoft Entra ID *group* membership to bind users to Kubernetes roles rather than individual *users*. As a user's group membership changes, their access permissions on the AKS cluster change accordingly.

Meanwhile, let's say you bind the individual user directly to a role and their job function changes. While the Microsoft Entra group memberships update, their permissions on the AKS cluster would not. In this scenario, the user ends up with more permissions than they require.

For more information about Microsoft Entra integration, Kubernetes RBAC, and Azure RBAC, see [Best practices for authentication and authorization in AKS](concepts-identity).

## Restrict access to Instance Metadata API


Best practice guidanceAdd a network policy in all user namespaces to block pod egress to the metadata endpoint.


Note

To implement Network Policy, include the attribute `--network-policy azure`

when creating the AKS cluster. Use the following command to create the cluster:
`az aks create -g myResourceGroup -n myManagedCluster --network-plugin azure --network-policy azure --generate-ssh-keys`


```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: restrict-instance-metadata
spec:
podSelector:
matchLabels: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 10.10.0.0/0#example
except:
- 169.254.169.254/32
```


## Secure container access to resources


Best practice guidanceLimit access to actions that containers can perform. Provide the least number of permissions, and avoid the use of root access or privileged escalation.


In the same way that you should grant users or groups the minimum privileges required, you should also limit containers to only necessary actions and processes. To minimize the risk of attack, avoid configuring applications and containers that require escalated privileges or root access.

Using user-namespaces, you improve the host isolation and limit the lateral movement in case of container breakouts. These improvements are significant whether the pod is running as root or not.

For even more granular control of container actions, you can also use built-in Linux security features such as *AppArmor* and *seccomp*.

For more information, see [Secure container access to resources](secure-container-access).

## Regularly update to the latest version of Kubernetes


Best practice guidanceTo stay current on new features and bug fixes, regularly upgrade the Kubernetes version in your AKS cluster.


Kubernetes releases new features at a quicker pace than more traditional infrastructure platforms. Kubernetes updates include:

- New features
- Bug or security fixes

New features typically move through *alpha* and *beta* status before they become *stable*. Once stable, are generally available and recommended for production use. Kubernetes new feature release cycle allows you to update Kubernetes without regularly encountering breaking changes or adjusting your deployments and templates.

AKS supports three minor versions of Kubernetes. Once a new minor patch version is introduced, the oldest minor version and patch releases supported are retired. Minor Kubernetes updates happen on a periodic basis. To stay within support, ensure you have a governance process to check for necessary upgrades. For more information, see [Supported Kubernetes versions AKS](supported-kubernetes-versions).

To check the versions that are available for your cluster, use the [az aks get-upgrades](/en-us/cli/azure/aks#az-aks-get-upgrades) command as shown in the following example:

```
az aks get-upgrades --resource-group myResourceGroup --name myAKSCluster --output table
```


You can then upgrade your AKS cluster using the [az aks upgrade](/en-us/cli/azure/aks#az-aks-upgrade) command. The upgrade process safely:

- Cordons and drains one node at a time.
- Schedules pods on remaining nodes.
- Deploys a new node running the latest OS and Kubernetes versions.

Important

Test new minor versions in a dev test environment and validate that your workload remains healthy with the new Kubernetes version.

Kubernetes may deprecate APIs (like in version 1.16) that your workloads rely on. When bringing new versions into production, consider using [multiple node pools on separate versions](create-node-pools) and upgrade individual pools one at a time to progressively roll the update across a cluster. If running multiple clusters, upgrade one cluster at a time to progressively monitor for impact or changes.

```
az aks upgrade --resource-group myResourceGroup --name myAKSCluster --kubernetes-version KUBERNETES_VERSION
```


For more information about upgrades in AKS, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions) and [Upgrade an AKS cluster](upgrade-cluster).

## Process Linux node updates

Each evening, Linux nodes in AKS get security patches through their distro update channel. This behavior is automatically configured as the nodes are deployed in an AKS cluster. To minimize disruption and potential impact to running workloads, nodes are not automatically rebooted if a security patch or kernel update requires it. For more information about how to handle node reboots, see [Apply security and kernel updates to nodes in AKS](node-updates-kured).

### Node image upgrades

Unattended upgrades apply updates to the Linux node OS, but the image used to create nodes for your cluster remains unchanged. If a new Linux node is added to your cluster, the original image is used to create the node. This new node will receive all the security and kernel updates available during the automatic check every night but will remain unpatched until all checks and restarts are complete. You can use node image upgrade to check for and update node images used by your cluster. For more information on node image upgrade, see [Azure Kubernetes Service (AKS) node image upgrade](node-image-upgrade).

## Process Windows Server node updates

For Windows Server nodes, regularly perform a node image upgrade operation to safely cordon and drain pods and deploy updated nodes.
