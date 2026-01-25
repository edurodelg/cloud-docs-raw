---
merged_at: 2026-01-25T12:25:33.935283
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



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


---

<!-- DOCUMENTO FUSIONADO: node-updates-kured.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-updates-kured -->

# Apply security and kernel updates to Linux nodes in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To protect your clusters, security updates are automatically applied to Linux nodes in AKS. These updates include OS security fixes or kernel updates. Some of these updates require a node reboot to complete the process. AKS doesn't automatically reboot these Linux nodes to complete the update process.

The process to keep Windows Server nodes up to date is a little different. Windows Server nodes don't receive daily updates. Instead, you perform an AKS upgrade that deploys new nodes with the latest base Window Server image and patches. For AKS clusters that use Windows Server nodes, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

This article shows you how to use the open-source [kured (KUbernetes REboot Daemon)](https://github.com/kubereboot/kured) to watch for Linux nodes that require a reboot, then automatically handle the rescheduling of running pods and node reboot process.

Note

`Kured`

is an open-source project in the Cloud Native Computing Foundation. Please direct issues to the [kured GitHub](https://github.com/kubereboot/kured). Additional support can be found in the #kured channel on [CNCF Slack](https://slack.cncf.io).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Before you begin

You need the Azure CLI version 2.0.59 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Understand the AKS node update experience

In an AKS cluster, your Kubernetes nodes run as Azure virtual machines (VMs). These Linux-based VMs use an Ubuntu or Azure Linux image, with the OS configured to automatically check for updates every day. If security or kernel updates are available, they're automatically downloaded and installed.

Some security updates, such as kernel updates, require a node reboot to finalize the process. A Linux node that requires a reboot creates a file named */var/run/reboot-required*. This reboot process doesn't happen automatically.

You can use your own workflows and processes to handle node reboots, or use `kured`

to orchestrate the process. With `kured`

, a [DaemonSet](concepts-clusters-workloads#statefulsets-and-daemonsets) is deployed that runs a pod on each Linux node in the cluster. These pods in the DaemonSet watch for existence of the */var/run/reboot-required* file, and then initiate a process to reboot the nodes.

### Node image upgrades

Unattended upgrades apply updates to the Linux node OS, but the image used to create nodes for your cluster remains unchanged. If a new Linux node is added to your cluster, the original image is used to create the node. This new node receives all the security and kernel updates available during the automatic check every day but remains unpatched until all checks and restarts are complete.

Alternatively, you can use node image upgrade to check for and update node images used by your cluster. For more information on node image upgrade, see [Azure Kubernetes Service (AKS) node image upgrade](node-image-upgrade).

### Node upgrades

There's another process in AKS that lets you *upgrade* a cluster. An upgrade is typically to move to a newer version of Kubernetes, not just apply node security updates. An AKS upgrade performs the following actions:

- A new node is deployed with the latest security updates and Kubernetes version applied.
- An old node is cordoned and drained.
- Pods are scheduled on the new node.
- The old node is deleted.

You can't remain on the same Kubernetes version during an upgrade event. You must specify a newer version of Kubernetes. To upgrade to the latest version of Kubernetes, you can [upgrade your AKS cluster](upgrade-cluster).

## Deploy kured in an AKS cluster

To deploy the `kured`

DaemonSet, install the following official Kured Helm chart. This creates a role and cluster role, bindings, and a service account, then deploys the DaemonSet using `kured`

.

```
# Add the Kured Helm repository
helm repo add kubereboot https://kubereboot.github.io/charts/
# Update your local Helm chart repository cache
helm repo update
# Create a dedicated namespace where you would like to deploy kured into
kubectl create namespace kured
# Install kured in that namespace with Helm 3 (only on Linux nodes, kured is not working on Windows nodes)
helm install my-release kubereboot/kured --namespace kured --set controller.nodeSelector."kubernetes\.io/os"=linux
```


You can also configure extra parameters for `kured`

, such as integration with Prometheus or Slack. For more information about configuration parameters, see the [kured Helm chart](https://github.com/kubereboot/charts/tree/main/charts/kured).

## Update cluster nodes

By default, Linux nodes in AKS check for updates every evening. If you don't want to wait, you can manually perform an update to check that `kured`

runs correctly. First, follow the steps to [SSH to one of your AKS nodes](ssh). Once you have an SSH connection to the Linux node, check for updates and apply them as follows:

```
sudo apt-get update && sudo apt-get upgrade -y
```


If updates were applied that require a node reboot, a file is written to */var/run/reboot-required*. `Kured`

checks for nodes that require a reboot every 60 minutes by default.

## Monitor and review reboot process

When one of the replicas in the DaemonSet detects that a node reboot is required, a lock is placed on the node through the Kubernetes API. This lock prevents more pods from being scheduled on the node. The lock also indicates that only one node should be rebooted at a time. With the node cordoned off, running pods are drained from the node, and the node is rebooted.

You can monitor the status of the nodes using the [kubectl get nodes](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. The following example output shows a node with a status of *SchedulingDisabled* as the node prepares for the reboot process:

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-28993262-0 Ready,SchedulingDisabled agent 1h v1.11.7
```


Once the update process is complete, you can view the status of the nodes using the [kubectl get nodes](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command with the `--output wide`

parameter. This output lets you see a difference in *KERNEL-VERSION* of the underlying nodes, as shown in the following example output. The *aks-nodepool1-28993262-0* was updated in a previous step and shows kernel version *4.15.0-1039-azure*. The node *aks-nodepool1-28993262-1* that hasn't been updated shows kernel version *4.15.0-1037-azure*.

```
NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME
aks-nodepool1-28993262-0 Ready agent 1h v1.11.7 10.240.0.4 <none> Ubuntu 16.04.6 LTS 4.15.0-1039-azure docker://3.0.4
aks-nodepool1-28993262-1 Ready agent 1h v1.11.7 10.240.0.5 <none> Ubuntu 16.04.6 LTS 4.15.0-1037-azure docker://3.0.4
```


## Next steps

This article detailed how to use `kured`

to reboot Linux nodes automatically as part of the security update process. To upgrade to the latest version of Kubernetes, you can [upgrade your AKS cluster](upgrade-cluster).

For AKS clusters that use Windows Server nodes, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).
