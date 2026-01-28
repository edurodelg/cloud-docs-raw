---
merged_at: 2026-01-28T07:16:09.847473
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-best-practices -->

# Best practices for Windows containers on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In AKS, you can create node pools that run Linux or Windows Server as the operating system (OS) on the nodes. Windows Server nodes can run native Windows container applications, such as .NET Framework. The Linux OS and Windows OS have different container support and configuration considerations. For more information, see [Windows container considerations in Kubernetes](windows-vs-linux-containers). To learn more about how various industries are using Windows containers on AKS, see [Windows AKS customer stories](windows-aks-customer-stories).

This article outlines best practices for running Windows containers on AKS.

## Create an AKS cluster with Linux and Windows node pools

When you create a new AKS cluster, the Azure platform creates a Linux node pool by default. This node pool contains system services needed for the cluster to function. Azure also creates and manages a control plane abstracted from the user, which means you aren't exposed to the underlying OS of the nodes hosting the main control plane components. We recommend that you run at least *two nodes* on the default Linux node pool to ensure the reliability and performance of your cluster. You can't delete the default Linux node pool unless you delete the entire cluster.

There are some cases where you should consider deploying a Linux node pool when planning to run Windows-based workloads on your AKS cluster, such as:

- If you want to run Linux and Windows workloads, you can deploy a Linux node pool and a Windows node pool in the same cluster.
- If you want to deploy infrastructure-related components based on Linux, such as NGINX, you need a Linux node pool alongside your Windows node pool. You can use control plane nodes for development and testing scenarios. For production workloads, we recommend that you deploy separate Linux node pools to ensure reliability and performance.

## Modernize existing applications with Windows on AKS

You might want to containerize existing applications and run them using Windows on AKS. Before starting the containerization process, it's important to understand the application architecture and dependencies. For more information, see [Containerize existing applications using Windows containers](/en-us/virtualization/windowscontainers/quick-start/lift-shift-to-containers).

## Windows OS version


Best practice guidanceWindows Server 2022 provides improved security and performance and is the recommended OS for Windows node pools on AKS. AKS uses Windows Server 2022 as the host OS version and only supports process isolation.


AKS supports two options for the Windows Server operating system: Long Term Servicing Channel Releases (LTSC) and Windows Server Annual Channel for Containers.

AKS supports Long Term Servicing Channel Releases (LTSC), including Windows Server 2025 (preview), Windows Server 2022, and Windows Server 2019. This channel is released every three years and is supported for five years. Customers using Long Term Support (LTS) should use Windows Server 2022.

AKS uses Windows Server 2019 and Windows Server 2022 as the host OS versions and only supports process isolation. AKS doesn't support container images built by other versions of Windows Server. For more information, see

[Windows container version compatibility](/en-us/virtualization/windowscontainers/deploy-containers/version-compatibility). Windows Server 2022 is the default OS for Kubernetes version 1.25 and later.Note

[Windows Server 2019 retires on March 1, 2026](https://github.com/Azure/AKS/issues/4091). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2019 on any Kubernetes version. All existing node pools with Windows Server 2019 will be unsupported. Windows Server 2019 is not supported in Kubernetes version 1.33 and above. Starting on April 1, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail.[Windows Server 2022 retires on March 15, 2027](https://github.com/Azure/AKS/issues/4168). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2022 on any Kubernetes version. All existing node pools with Windows Server 2022 will be unsupported. Windows Server 2022 is not supported in Kubernetes version 1.36 and above. Starting on April 1, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail.

For more information, see

[AKS release notes](https://github.com/Azure/AKS/releases). To stay up to date on the latest Windows Server OS versions and learn more about our roadmap of what's planned for support on AKS, see our[AKS public roadmap](https://github.com/azure/aks/projects/1).AKS supports

[Windows Server Annual Channel for Containers](https://techcommunity.microsoft.com/t5/windows-server-news-and-best/windows-server-annual-channel-for-containers/ba-p/3866248)(preview). This channel is released annually and is supported for two years. This channel is beneficial for customers requiring increased innovation cycles and portability. The portability functionality enables the Windows Server 2022-based container image OS to run on newer versions of Windows Server host OS, such as the new annual channel release.Windows Annual Channel versions are based on the Kubernetes version of your node pool. To upgrade from one Annual Channel version to the next,

[upgrade to a Kubernetes version](upgrade-aks-cluster)that supports the next Annual Channel version. For more information, see[Windows Server Annual Channel for Containers on AKS](windows-annual-channel).

## Monitoring


Best practice guidanceWindows Exporter is installed on all Windows nodes in certain regions. To view regional rollout, see

[AKS Github]. With Managed Prometheus and Grafana, you can monitor default collectors included in Windows Exporter on AKS. For more information, see[default Prometheus metrics configured in Azure Monitor].

Windows Exporter allows customers to see their metrics through Managed Prometheus or Prometheus OSS deployments and enjoy enhanced observability around their node and pod performance, health, and resource usage. These metrics are also visible with Managed Grafana.

- When enabling managed prometheus, add this required parameter for correct dashboard data presentation for Windows:
`--enable-windows-recording-rules`

. - Grafana includes dashboards for showing Windows resources, such as:
- Kubernetes / Compute Resources / Cluster (Windows)
- Kubernetes / Compute Resources / Namespace (Windows)
- Kubernetes / Compute Resources / Pod (Windows)
- Kubernetes / USE Method / Cluster (Windows)
- Kubernetes / USE Method / Node (Windows)


The default collectors included in Windows Exporter on AKS are: cpu, cpu_info, cs, container, logical_disk, memory, net, os, process, service, system, textfile. The metrics are exposed on port **19182** on the windows node. For more information on what metrics you can see using these collectors, please see [prometheus-community/windows_exporter](https://github.com/prometheus-community/windows_exporter#collectors).

## Networking

### Networking modes


Best practice guidanceAKS clusters with Windows node pools only support Azure Container Networking Interface (Azure CNI) and use it by default.


Windows doesn't support kubenet networking. AKS clusters with Windows node pools must use Azure CNI. For more information, see [Network concepts for applications in AKS](concepts-network).

Azure CNI offers two networking modes based on your workload requirements:

is an overlay network similar to kubenet. The overlay network allows you to use virtual network (VNet) IPs for nodes and private address spaces for pods within those nodes that you can reuse across the cluster. Azure CNI Overlay is the**Azure CNI Overlay****recommended networking mode**. It provides simplified network configuration and management and the best scalability in AKS networking.requires extra planning and consideration for IP address management. This mode provides VNet IPs for nodes**Azure CNI with Dynamic IP Allocation***and*pods. This configuration allows you direct access to pod IPs. However, it comes with increased complexity and reduced scalability.

To help you decide which networking mode to use, see [Choosing a network model](concepts-network-azure-cni-overlay#choose-a-network-model).

### Network policies


Best practice guidanceUse network policies to secure traffic between pods. Windows supports Azure Network Policy Manager and Calico Network Policy. For more information, see

[Differences between Network Policy engines: Cilium, Azure NPM, and Calico].

When managing traffic between pods, you should apply the principle of least privilege. The Network Policy feature in Kubernetes allows you to define and enforce ingress and egress traffic rules between the pods in your cluster. For more information, see [Secure traffic between pods using network policies in AKS](use-network-policies).

Windows pods on AKS clusters that use the Calico Network Policy enable Floating IP by default.

## Upgrades and updates

It's important to keep your Windows environment up-to-date to ensure your systems have the latest security updates, feature sets, and compliance requirements. In a Kubernetes environment like AKS, you need to maintain the Kubernetes version, Windows nodes, and Windows container images and pods.

### Kubernetes version upgrades

As a managed Kubernetes service, AKS provides the necessary tools to upgrade your cluster to the latest Kubernetes version. For more information, see [Upgrade an AKS cluster](upgrade-cluster).

### Windows node monthly updates

Windows nodes on AKS follow a monthly update schedule. Every month, AKS creates a new VHD with the latest available updates for Windows node pools. The VHD includes the host image, latest Nano Server image, latest Server Core image, and container. We recommend performing monthly updates to your Windows node pools to ensure your nodes have the latest security patches. For more information, see [Upgrade AKS node images](node-image-upgrade).

Note

Upgrades on Windows systems include both OS version upgrades and monthly node OS updates.

You can stay up to date with the availability of new monthly releases using the [AKS release tracker](https://releases.aks.azure.com/) and [AKS release notes](https://github.com/Azure/AKS/releases).

### Windows node OS version upgrades

Windows has a release cadence for new versions of the OS, including Windows Server 2025 (preview), Windows Server 2022, and Windows Server 2019. When upgrading your Windows node OS version, ensure the Windows container image version matches the Windows container host version and the node pools have only one version of Windows Server.

To upgrade the Windows node OS version, you need to complete the following steps:

- Create a new node pool with the new Windows Server version.
- Deploy your workloads with the new Windows container images to the new node pool.
- Decommission the old node pool.

For more information, see [Upgrade Windows Server workloads on AKS](upgrade-windows-2019-2022).

Note

Windows announced a new [Windows Server Annual Channel for Containers](https://techcommunity.microsoft.com/t5/windows-server-news-and-best/windows-server-annual-channel-for-containers/ba-p/3866248) that supports portability and mixed versions of Windows nodes and containers. This feature isn't yet supported in AKS.

To track AKS feature plans, see the [Public AKS roadmap](https://github.com/Azure/AKS/projects/1#card-90806240).

## Next steps

To learn more about Windows containers on AKS, see the following resources:

[Learn how to deploy, manage, and monitor Windows containers on AKS](/en-us/training/paths/deploy-manage-monitor-wincontainers-aks).- Open an issue or provide feedback in the
[Windows containers GitHub repository](https://github.com/microsoft/Windows-Containers/issues). - Review the
[third-party partner solutions for Windows on AKS](windows-aks-partner-solutions).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/start-stop-cluster -->

# Stop and start an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You may not need to continuously run your Azure Kubernetes Service (AKS) workloads. For example, you may have a development cluster that you only use during business hours. This means there are times where your cluster might be idle, running nothing more than the system components. You can reduce the cluster footprint by [scaling all User node pools to 0](scale-cluster#scale-user-node-pools-to-0), but your

[is still required to run the system components while the cluster is running.](use-system-pools)

`System`

poolTo better optimize your costs during these periods, you can turn off, or stop, your cluster. This action stops your control plane and agent nodes, allowing you to save on all the compute costs, while maintaining all objects except standalone pods. The cluster state is stored for when you start it again, allowing you to pick up where you left off.

Caution

Stopping your cluster deallocates the control plane and releases the capacity. In regions experiencing capacity constraints, customers may be unable to start a stopped cluster. We do not recommend stopping mission critical workloads for this reason.

Note

AKS start operations will restore all objects from ETCD with the exception of standalone pods with the same names and ages. meaning that a pod's age will continue to be calculated from its original creation time. This count will keep increasing over time, regardless of whether the cluster is in a stopped state.

## Before you begin

This article assumes you have an existing AKS cluster. If you need an AKS cluster, you can create one using [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

### About the cluster stop/start feature

When using the cluster stop/start feature, the following conditions apply:

- This feature is only supported for Virtual Machine Scale Set backed clusters.
- You can't stop clusters which use the
[Node Autoprovisioning (NAP)](node-autoprovision)feature. - The cluster state of a stopped AKS cluster is preserved for up to 12 months. If your cluster is stopped for more than 12 months, you can't recover the state. For more information, see the
[AKS support policies](support-policies). - You can only perform start or delete operations on a stopped AKS cluster. To perform other operations, like scaling or upgrading, you need to start your cluster first.
- If you provisioned PrivateEndpoints linked to private clusters, they need to be deleted and recreated again when starting a stopped AKS cluster.
- Because the stop process drains all nodes, any standalone pods (i.e. pods not managed by a Deployment, StatefulSet, DaemonSet, Job, etc.) will be deleted.
- When you start your cluster back up, the following behavior is expected:
- The IP address of your API server may change.
- If you're using cluster autoscaler, when you start your cluster, your current node count may not be between the min and max range values you set. The cluster starts with the number of nodes it needs to run its workloads, which isn't impacted by your autoscaler settings. When your cluster performs scaling operations, the min and max values will impact your current node count, and your cluster will eventually enter and remain in that desired range until you stop your cluster.


## Stop an AKS cluster

Use the

command to stop a running AKS cluster, including the nodes and control plane. The following example stops a cluster named`az aks stop`

*myAKSCluster*:`az aks stop --name myAKSCluster --resource-group myResourceGroup`

Verify your cluster has stopped using the

command and confirming the`az aks show`

`powerState`

shows as`Stopped`

.`az aks show --name myAKSCluster --resource-group myResourceGroup`

Your output should look similar to the following condensed example output:

`{ [...] "nodeResourceGroup": "MC_myResourceGroup_myAKSCluster_westus2", "powerState":{ "code":"Stopped" }, "privateFqdn": null, "provisioningState": "Succeeded", "resourceGroup": "myResourceGroup", [...] }`

If the

`provisioningState`

shows`Stopping`

, your cluster hasn't fully stopped yet.

Important

If you're using [pod disruption budgets](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/), the stop operation can take longer, as the drain process will take more time to complete.

## Start an AKS cluster

Caution

After utilizing the start/stop feature on AKS, it is essential to wait 15-30 minutes before restarting your AKS cluster. This waiting period is necessary because it takes several minutes for the relevant services to fully stop. Attempting to restart your cluster during this process can disrupt the shutdown process and potentially cause issues with the cluster or its workloads.

Use the

command to start a stopped AKS cluster. The cluster restarts with the previous control plane state and number of agent nodes. The following example starts a cluster named`az aks start`

*myAKSCluster*:`az aks start --name myAKSCluster --resource-group myResourceGroup`

Verify your cluster has started using the

command and confirming the`az aks show`

`powerState`

shows`Running`

.`az aks show --name myAKSCluster --resource-group myResourceGroup`

Your output should look similar to the following condensed example output:

`{ [...] "nodeResourceGroup": "MC_myResourceGroup_myAKSCluster_westus2", "powerState":{ "code":"Running" }, "privateFqdn": null, "provisioningState": "Succeeded", "resourceGroup": "myResourceGroup", [...] }`

If the

`provisioningState`

shows`Starting`

, your cluster hasn't fully started yet.

## Next steps

- To learn how to scale
`User`

pools to 0, see[Scale](scale-cluster#scale-user-node-pools-to-0).`User`

pools to 0 - To learn how to save costs using Spot instances, see
[Add a spot node pool to AKS](spot-node-pool). - To learn more about the AKS support policies, see
[AKS support policies](support-policies).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-ai-ml-language-models -->

# Concepts - Small and large language models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about small and large language models, including when to use them and how you can use them with your AI and machine learning workflows on Azure Kubernetes Service (AKS).

## What are language models?

Language models are powerful machine learning models used for natural language processing (NLP) tasks, such as text generation and sentiment analysis. These models represent natural language based on the probability of words or sequences of words occurring in a given context.

*Conventional language models* have been used in supervised settings for research purposes where the models are trained on well-labeled text datasets for specific tasks. *Pre-trained language models* offer an accessible way to get started with AI and have become more widely used in recent years. These models are trained on large-scale text corpora from the internet using deep neural networks and can be fine-tuned on smaller datasets for specific tasks.

The size of a language model is determined by its number of parameters, or *weights*, that determine how the model processes input data and generates output. Parameters are learned during the training process by adjusting the weights within layers of the model to minimize the difference between the model's predictions and the actual data. The more parameters a model has, the more complex and expressive it is, but also the more computationally expensive it is to train and use.

In general, **small language models** have *fewer than 10 billion parameters*, and **large language models** have *more than 10 billion parameters*. For example, the new Microsoft Phi-3 model family has three versions with different sizes: mini (3.8 billion parameters), small (7 billion parameters), and medium (14 billion parameters).

## When to use small language models

### Advantages

Small language models are a good choice if you want models that are:

**Faster and more cost-effective to train and run**: They require less data and compute power.**Easy to deploy and maintain**: They have smaller storage and memory footprints.**Less prone to**, which is when a model learns the noise or specific patterns of the training data and fails to generalize new data.*overfitting***Interpretable and explainable**: They have fewer parameters and components to understand and analyze.

### Use cases

Small language models are suitable for use cases that require:

**Limited data or resources**, and you need a quick and simple solution.**Well-defined or narrow tasks**, and you don't need much creativity in the output.**High-precision and low-recall tasks**, and you value accuracy and quality over coverage and quantity.**Sensitive or regulated tasks**, and you need to ensure the transparency and accountability of the model.

The following table lists some popular, high-performance small language models:

| Model family | Model sizes (Number of parameters) | Software license |
|---|---|---|
| Microsoft Phi-3 | Phi-3-mini (3.8 billion), Phi-3-small (7 billion) | MIT license |
| Microsoft Phi-2 | Phi-2 (2.7 billion) | MIT license |
| Falcon | Falcon-7B (7 billion) | Apache 2.0 license |

## When to use large language models

### Advantages

Large language models are a good choice if you want models that are:

**Powerful and expressive**: They can capture more complex patterns and relationships in the data.**General and adaptable**: They can handle a wider range of tasks and transfer knowledge across domains.**Robust and consistent**: They can handle noisy or incomplete inputs and avoid common errors and biases.

### Use cases

Large language models are suitable for use cases that require:

**Abundant data and resources**, and you have the budget to build and maintain a complex solution.**Low-precision and high-recall tasks**, and you value coverage and quantity over accuracy and quality.**Challenging or exploratory tasks**, and you want to leverage the model's capacity to learn and adapt.

The following table lists some popular, high-performance large language models:

| Model family | Model sizes (Number of parameters) | Software license |
|---|---|---|
| Microsoft Phi-3 | Phi-3-medium (14 billion) | MIT license |
| Falcon | Falcon-40B (40 billion) | Apache 2.0 license |

## Experiment with small and large language models on AKS

Kubernetes AI Toolchain Operator (KAITO) is an open-source operator that automates small and large language model deployments in Kubernetes clusters. The KAITO add-on for AKS simplifies onboarding and reduces the time-to-inference for open-source models on your AKS clusters. The add-on automatically provisions right-sized GPU nodes and sets up the associated interference server as an endpoint server to your chosen model.

For more information, see [Deploy an AI model on AKS with the AI toolchain operator](ai-toolchain-operator). To get started with a range of supported small and large language models for your inference workflows, see the [KAITO model GitHub repository](https://github.com/Azure/kaito/tree/main/presets).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Next steps

To learn more about containerized AI and machine learning workloads on AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-advanced-container-networking-services -->

# Use Advanced Container Networking Services on your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to enable and disable Advanced Container Networking Services, including [Container Network Observability](advanced-container-networking-services-overview#container-network-observability) and [Container Network Security](advanced-container-networking-services-overview#container-network-security), on your AKS clusters.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - Azure CLI version 2.71.0 or higher. Find your version using the
`az --version`

command. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). [Install the](#install-the-aks-preview-azure-cli-extension)version`aks-preview`

Azure CLI extension`14.0.0b6`

or higher.[Register the](#register-the-advancednetworkingl7policypreview-feature-flag)in your subscription.`AdvancedNetworkingL7PolicyPreview`

feature flag- Clusters that have the Cilium data plane support
*Container Network Observability*and*Container Network Security*in Kubernetes version 1.29 and later.

## Install the `aks-preview`

Azure CLI extension

Install or update the Azure CLI preview extension using the

or`az extension add`

command.`az extension update`

`# Install the aks-preview extension az extension add --name aks-preview # Update the extension to make sure you have the latest version installed az extension update --name aks-preview`


## Register the `AdvancedNetworkingL7PolicyPreview`

feature flag

Register the

`AdvancedNetworkingL7PolicyPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"`

Registration takes a few minutes to complete.

Verify successful registration using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"`


## Set environment variables

The examples in this article use the following environment variables:

| Variable | Description | Example value |
|---|---|---|
`RESOURCE_GROUP` |
Name of the Azure resource group | `myResourceGroup` |
`LOCATION` |
Azure region for resources | `eastus` |
`CLUSTER_NAME` |
Name of the AKS cluster | `myAKSCluster` |

**All commands in this article assume these environment variables are set**. Make sure to replace the example values with your own values.

## Create a resource group

Create a resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`


## Create a new AKS cluster with Advanced Container Networking Services

Note

When the `--acns-advanced-networkpolicies`

parameter is set to `L7`

, both Layer 7 and fully qualified domain name (FQDN) filtering policies are enabled. If you want to enable only FQDN filtering, set the parameter to `FQDN`

.

Create an AKS cluster with Advanced Container Networking Services and Cilium using the

command with the`az aks create`

`--enable-acns`

and`--network-dataplane cilium`

flags.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --network-plugin azure \ --network-plugin-mode overlay \ --network-dataplane cilium \ --kubernetes-version 1.29 \ --enable-acns \ --acns-advanced-networkpolicies <L7/FQDN>`


Important

The [Container Network Security](advanced-container-networking-services-overview#container-network-security) feature isn't available for non-Cilium clusters.

Create an AKS cluster with Advanced Container Networking Services using the

command with the`az aks create`

`--enable-acns`

flag.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --network-plugin azure \ --network-plugin-mode overlay \ --enable-acns`


## Enable Advanced Container Networking Services on an existing cluster

Enable Advanced Container Networking Services on an existing AKS cluster with Cilium using the

command with the`az aks update`

`--enable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --acns-advanced-networkpolicies <L7/FQDN>`


Enable Advanced Container Networking Services on an existing AKS cluster using the

command with the`az aks update`

`--enable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns`


## Disable Advanced Container Networking Services on an AKS cluster

Disable Advanced Container Networking Services on an existing AKS cluster using the

command with the`az aks update`

`--disable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --disable-acns`


## Disable Container Network Observability on an AKS cluster

Disable the Container Network Observability feature without affecting other Advanced Container Networking Services features using the

command with the`az aks update`

`--disable-acns-observability`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --disable-acns-observability`


Container Network Observability is the only feature available for non-Cilium clusters, so you can disable it only by disabling the entire Advanced Container Networking Services suite.

Disable the Container Network Observability feature on an existing AKS cluster using the

command with the`az aks update`

`--disable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --disable-acns`


## Disable Container Network Security on an AKS cluster

Disable the Container Network Security feature without affecting other Advanced Container Networking Services features using the

command with the`az aks update`

`--disable-acns-security`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --disable-acns-security`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-arm64-vms -->

# Use Arm-based processor (Arm64) Virtual Machines (VMs) in an Azure Kubernetes Service (AKS) cluster for cost effectiveness

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Arm-based processors (Arm64)](/en-us/azure/virtual-machines/sizes/cobalt-overview) are power-efficient and cost-effective, but don't compromise on performance. These Arm64 VMs are engineered to efficiently run dynamic, scalable workloads and can deliver up to 50% better price-performance than comparable x86-based VMs for scale-out workloads.

Because of their ability to scale workloads efficiently, Arm64 VMs are well-suited for web or application servers, open-source databases, cloud-native applications, gaming servers, and other high traffic applications.

Note

While a combination of CPU, memory, and networking capacity configurations heavily influences the cost effectiveness of a SKU, Arm64 VM types are recommended for cost optimization.

In this article, you'll learn how to add a Arm64 VM to an existing node pool.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

Before you begin, make sure you have:

## Limitations

- Arm64 VMs aren't supported for Windows node pools.
- Existing node pools can't be updated to use an Arm64 VM.
- Federal Information Process Standard (FIPS)-enabled node pools are only supported with Arm64 SKUs when using Azure Linux 3.0+.
- Arm64 node pools aren't supported on Defender-enabled clusters with Kubernetes version 1.29.0 or lower.

## Create node pools with Arm64 VMs

The Arm64 processor provides low power compute for your Kubernetes workloads. Arm64 virtual machines can be added to existing clusters even mixing Intel and Arm architecture node pools within a cluster. To create an Arm64 node pool, you need to choose a [Dpsv5](/en-us/azure/virtual-machines/dpsv5-dpdsv5-series), [Dplsv5](/en-us/azure/virtual-machines/dplsv5-dpldsv5-series), or [Epsv5](/en-us/azure/virtual-machines/epsv5-epdsv5-series) series virtual machine.

### Add a node pool with an Arm64 VM

Use [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) to add a node pool with an Arm64 VM to an existing cluster. Alternatively, if you're using

[Azure Linux 3.0+](/en-us/azure/azure-linux/how-to-enable-azure-linux-3), you can add a node pool with an Arm64 VM and

[FIPS](enable-fips-nodes)enabled.

Add a node pool with an Arm64 VM

`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $ARM_NODE_POOL_NAME \ --node-count 3 \ --node-vm-size Standard_D2pds_v5`

Add a FIPS-enabled node pool with an Arm64 VM

Limitations:

- Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)enabled aren't supported with Ubuntu OS. - Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)require kubernetes version 1.31+.

Use the

with`az aks nodepool add`

`--enable-fips-image`

and`--os-sku`

parameters.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $ARM_NODE_POOL_NAME \ --os-sku AzureLinux --enable-fips-image --kubernetes-version 1.31 --node-count 3 \ --node-vm-size Standard_D2pds_v5`

For more information on verifying FIPS enablement and disabling FIPS, see

[Enable FIPS node pools](enable-fips-nodes).- Node pools with Arm64 VMs and
Update a node pool with an Arm64 VM to enable FIPS

Limitations:

- Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)enabled aren't supported with Ubuntu OS. - Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)require kubernetes version 1.31+.

Use

command with the`az aks nodepool update`

`--enable-fips-image`

parameter to enable FIPS on an existing node pool.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name np \ --enable-fips-image`

This command triggers a reimage of the node pool immediately to deploy the FIPS compliant Operating System. This reimage occurs during the node pool update. No extra steps are required.

- Node pools with Arm64 VMs and

For more information on verifying FIPS enablement and disabling FIPS, see [Enable FIPS node pools](enable-fips-nodes).

## Verify the node pool uses Arm64

Verify a node pool uses Arm64 using the [ az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command and verify the

`vmSize`

is a [Dpsv5](/en-us/azure/virtual-machines/dpsv5-dpdsv5-series),

[Dplsv5](/en-us/azure/virtual-machines/dplsv5-dpldsv5-series), or

[Epsv5](/en-us/azure/virtual-machines/epsv5-epdsv5-series)series.

```
az aks nodepool show \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name mynodepool \
--query vmSize
```


The following example output shows the node pool uses Arm64:

```
"Standard_D2pds_v5"
```


## Next steps

In this article, you learned how to add a node pool with an Arm64 VM to an AKS cluster.

- For more recommendations for cost savings, see
[Best practices for cost optimization in Azure Kubernetes Service (AKS)](best-practices-cost). - For more information about Arm64, see
[Cobalt Arm-based processors (Arm64)](/en-us/azure/virtual-machines/sizes/cobalt-overview). - For more information on verifying FIPS enablement and disabling FIPS, see
[Enable FIPS node pools](enable-fips-nodes). - For Azure Linux 3.0 enablement and support details, see
[Enable Azure Linux 3.0](/en-us/azure/azure-linux/how-to-enable-azure-linux-3).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/optimized-addon-scaling -->

# Enable cost optimized add-on scaling on your Azure Kubernetes Service (AKS) cluster (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of cost optimized add-on scaling in Azure Kubernetes Service (AKS). With cost-optimized add-on scaling, you can manage add-ons that require custom CPU and memory by overriding default configurations or enabling autoscaling. This feature ensures that resources aren't overly allocated to add-on pods, improving cost savings and cluster efficiency.

## Overview

Enabling cost optimized add-on scaling installs the [Vertical Pod Autoscaler (VPA)add-on](vertical-pod-autoscaler), allowing supported add-ons to autoscale based on usage.

This feature also allows you to customize the resource's default CPU/ memory requests and limits in Deployments and DaemonSets, the maximum and minimum allowed CPU/ memory, and the VPA update mode within VPA custom resources. For more information, see [customize the resource configuration for AKS add-ons](customize-resource-configuration).

### Supported AKS add-ons

The following AKS managed add-ons support the cost optimized add-on scaling feature:

| Add-on | Enablement behavior | VPA custom resource name | Command to check VPA custom resource |
|---|---|---|---|
|

`coredns`

`kubectl get vpa coredns --namespace kube-system`

[Workload identity](workload-identity-deploy-cluster)`azure-wi-webhook-controller-manager`

`kubectl get vpa azure-wi-webhook-controller-manager --namespace kube-system`

[Image Integrity](image-integrity)`ratify`

`kubectl get vpa ratify --namespace gatekeeper-system`

[Network Observability (Retina)](container-network-observability-how-to)`retina-agent`

and `retina-operator`

`kubectl get vpa retina-agent --namespace kube-system`

and `kubectl get vpa retina-operator --namespace kube-system`

### Supported VPA modes for cost optimized add-on scaling

VPA currently supports the following modes for cost optimized add-on scaling:

*Off*: The VPA provides resource recommendation data but doesn't apply it to the target pod.*Initial*(default mode): The VPA automatically applies CPU and memory recommendations to the target pod when it restarts, but it doesn't initiate the restart itself.*Auto*: The VPA automatically updates CPU and memory requests for pods based on recommendations.

Note

When enabling cost optimized add-on scaling, consider the following information:

- If you delete the Deployment, DaemonSet, or VPA custom resource, the changes revert back to the AKS add-on's initial configuration.
- The cost optimized add-on scaling feature enables the
[VPA add-on](vertical-pod-autoscaler)to autoscale the supported AKS add-ons. It doesn't work with self-hosted VPA. - AKS restarts the add-on pods when enabling cost optimized add-on scaling. CoreDNS is currently the only exception to avoid potential disruptions during the restart. For more information, see
[CoreDNS autoscaling behavior](coredns-autoscale).

Warning

Make sure you have enough compute resources on the system node pool for your addons when you enable cost optimized add-on scaling. AKS recommends turning on the [cluster autoscaler](cluster-autoscaler-overview) or [node autoprovision](node-autoprovision) to ensure right-sizing of your compute resources automatically.
Monitor for pending add-on pods when using the cost-optimized add-on scaling feature. VPA might recommend resource requests that exceed available node capacity, potentially leading to unschedulable pods. You can control this behavior by [customizing min/max values](customize-resource-configuration) for requests and limits of supported addons.

## Prerequisites

- An AKS cluster running Kubernetes version 1.25 or later.
- The Azure CLI version 2.60.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). [Install the](#install-the-aks-preview-azure-cli-extension)and`aks-preview`

Azure CLI extension[register the cost optimized add-on scaling preview feature](#register-the-cost-optimized-add-on-scaling-preview-feature).

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Install the `aks-preview`

Azure CLI extension

Install the

`aks-preview`

extension using the`az extension add`

command.`az extension add --name aks-preview`

Update to the latest version of the extension using the

`az extension update`

command.`az extension update --name aks-preview`


### Register the cost optimized add-on scaling preview feature

Register the cost optimized add-on scaling preview feature using the

`az feature register`

command.`az feature register --namespace "Microsoft.ContainerService" --name "AKS-AddonAutoscalingPreview"`

It takes a few minutes for the status to show as

*Registered*.Verify the registration status using the

`az feature show`

command.`az feature show --namespace "Microsoft.ContainerService" --name "AKS-AddonAutoscalingPreview"`

When the status shows as

*Registered*, refresh the registration of the Microsoft.ContainerService provider using the`az provider register`

command.`az provider register --namespace Microsoft.ContainerService`


## Enable cost optimized add-on scaling on an AKS cluster

When enabling the add-on, the AKS cluster automatically installs the [VPA add-on](vertical-pod-autoscaler). The [AKS add-ons that support the cost optimized add-on scaling feature](#supported-aks-add-ons) have different enablement behavior.

Note

If you're using Bicep, ARM templates, or Terraform, set `VerticalPodAutoscaler`

to `"True"`

and `AddonAutoscaling`

to `"enabled"`

.

### Enable cost optimized add-on scaling on a new cluster

Enable cost optimized add-on scaling on a new AKS cluster using the

command with the`az aks create`

`--enable-optimized-addon-scaling`

flag.`az aks create --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --enable-optimized-addon-scaling`


### Enable cost optimized add-on scaling on an existing cluster

Enable cost optimized add-on scaling on an existing AKS cluster using the

command with the`az aks update`

`--enable-optimized-addon-scaling`

flag.`az aks update --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --enable-optimized-addon-scaling`


## Disable cost optimized add-on scaling on an AKS cluster

Disable cost optimized add-on scaling on an AKS cluster using the

command with the`az aks update`

`--disable-optimized-addon-scaling`

flag.`az aks update --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --disable-optimized-addon-scaling`


Note

Disabling the cost optimized add-on scaling feature doesn't disable the VPA add-on by default. To disable VPA, see [Disable VPA on an AKS cluster](use-vertical-pod-autoscaler#disable-the-vertical-pod-autoscaler-on-an-existing-cluster).

## Customize default resource configuration

With the cost optimized add-on scaling feature enabled on your cluster, you can customize the default CPU/memory settings for the add-on resources as well as the default VPA configuration for supported AKS add-ons. For more information, see [customize the resource configuration for AKS add-ons](customize-resource-configuration).

## Applying the VPA recommended values manually

Note

With *Initial* mode, the VPA applies the recommended CPU and memory requests only when a pod is created or updated. If you want the recommendations to take effect immediately, please update the pods manually. Before manually applying the recommended values, [make sure the VPA update mode is set to Initial or Auto in the VPA custom resource](customize-resource-configuration#customize-resource-update-mode).

Check the pod status and CPU/memory utilization to verify that the pod is running as expected.

The following example uses the

`kubectl get pod`

command to check a CoreDNS pod status:`kubectl get pod <coredns-pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a CoreDNS pod:

`apiVersion: v1 kind: Pod metadata: name: <coredns-pod-name> namespace: kube-system spec: ... containers: - name: coredns resources: limits: cpu: "3" memory: "500Mi" requests: cpu: "100m" memory: "70Mi"`

Get the VPA recommended value using the

`kubectl get vpa`

command.`kubectl get vpa coredns --namespace kube-system`

The following output shows an example of the VPA recommended value for a CoreDNS pod:

`NAME MODE CPU MEM PROVIDED AGE coredns Initial 11m 23574998 True 44m`

If you want to use the values recommended by VPA, manually delete the pod using the

`kubectl delete pod`

command to restart the pod with the VPA recommended values.`kubectl delete pod <coredns-pod-name> --namespace kube-system`

After the pod restarts, verify the pod status and CPU/memory updates using the

`kubectl get pod`

command.`kubectl get pod <coredns-pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a CoreDNS pod after applying the VPA recommended values:

`apiVersion: v1 kind: Pod metadata: name: <coredns-pod-name> namespace: kube-system spec: ... containers: - name: coredns resources: limits: cpu: "330m" memory: "168392842" requests: cpu: "11m" memory: "23574998"`


## Troubleshooting

With the cost optimized add-on scaling feature enabled on your cluster, you can customize the default CPU and memory settings for add-on resources, as well as modify the default VPA configuration for supported AKS managed add-ons

If your autoscaling enabled add-on pods are in a pending state, or you don't see any VPA recommendations for autoscaling enabled add-ons, follow these steps to troubleshoot the issue.

### Check AKS-managed VPA add-on status

Check if all VPA system components are running using the

`kubectl get pods`

command.`kubectl get pods --namespace kube-system | grep vpa`

The output should show three pods (vpa-admission-controller, vpa-recommender, and vpa-updater) running in the

`kube-system`

namespace, similar to the following example:`vpa-admission-controller 2/2 2 2 4m11s vpa-recommender 1/1 1 1 4m11s vpa-updater 1/1 1 1 4m11s`

For each of the three VPA pods, check the logs for any errors using the

`kubectl logs`

command. Make sure to replace`<pod-name>`

with the names of the VPA pods.`kubectl logs <pod-name> --namespace kube-system | grep -e '^E[0-9]\{4\}'`

Confirm the custom resource definition (CRD) was creating using the

`kubectl get`

command.`kubectl get customresourcedefinition | grep verticalpodautoscalers`


### Check pod status and CPU/memory utilization

Check the pod's status using the

`kubectl get pod`

command.`kubectl get pod <pod-name> --namespace=kube-system`

If the pod has a status of

`Pending`

, check the pod's status property to determine the reason the pod isn't running.`kubectl describe pod <pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a pod with a status of

`Pending`

:`apiVersion: v1 kind: Pod ... status: conditions: - lastProbeTime: null lastTransitionTime: "2023-05-03T17:05:26Z" message: '0/1 nodes are available: 1 Insufficient cpu, 1 Insufficient memory. preemption: 0/1 nodes are available: 1 Insufficient cpu, 1 Insufficient memory..' reason: Unschedulable status: "False" type: PodScheduled phase: Pending qosClass: Guaranteed`

If the output shows that the pod is

`Pending`

due to insufficient CPU or memory, consider the following actions:- Add more nodes so that pods can be scheduled in nodes with lower resource usage.
- Disable VPA for the target add-on pod by changing the update mode to
*Off*, and then[manually update the requests/limits](customize-resource-configuration)to the available resource values on the node. Be cautious when setting resource limits to extremely low values, as this may result in the pod encountering OOM kills or CPU throttling if it attempts to use more resources than are available on the node.


## Next steps

- Configure
[Cluster Autoscaler](cluster-autoscaler-overview)or[Node Autoprovisioning](node-autoprovision)in your cluster to automatically scale the cluster.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-about -->

# Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Istio](https://istio.io/latest/) addresses the challenges developers and operators face with a distributed or microservices architecture. The Istio-based service mesh add-on provides an officially supported and tested integration for Azure Kubernetes Service (AKS).

## What is a Service Mesh?

Modern applications are typically architected as distributed collections of microservices, with each collection of microservices performing some discrete business function. A service mesh is a dedicated infrastructure layer that you can add to your applications. It allows you to transparently add capabilities like observability, traffic management, and security, without adding them to your own code. The term **service mesh** describes both the type of software you use to implement this pattern, and the security or network domain that is created when you use that software.

As the deployment of distributed services, such as in a Kubernetes-based system, grows in size and complexity, it can become harder to understand and manage. You may need to implement capabilities such as discovery, load balancing, failure recovery, metrics, and monitoring. A service mesh can also address more complex operational requirements like A/B testing, canary deployments, rate limiting, access control, encryption, and end-to-end authentication.

Service-to-service communication is what makes a distributed application possible. Routing this communication, both within and across application clusters, becomes increasingly complex as the number of services grow. Istio helps reduce this complexity while easing the strain on development teams.

## What is Istio?

Istio is an open-source service mesh that layers transparently onto existing distributed applications. Istio’s powerful features provide a uniform and more efficient way to secure, connect, and monitor services. Istio enables load balancing, service-to-service authentication, and monitoring – with few or no service code changes. Its powerful control plane brings vital features, including:

- Secure service-to-service communication in a cluster with TLS (Transport Layer Security) encryption, strong identity-based authentication, and authorization.
- Automatic load balancing for HTTP, gRPC, WebSocket, and TCP traffic.
- Fine-grained control of traffic behavior with rich routing rules, retries, failovers, and fault injection.
- A pluggable policy layer and configuration API supporting access controls, rate limits, and quotas.
- Automatic metrics, logs, and traces for all traffic within a cluster, including cluster ingress and egress.

## How is the add-on different from open-source Istio?

This service mesh add-on uses and builds on top of open-source Istio. The add-on flavor provides the following extra benefits:

- Istio versions are tested and verified to be compatible with supported versions of Azure Kubernetes Service.
- Microsoft handles scaling and configuration of Istio control plane
- Microsoft adjusts scaling of AKS components like
`coredns`

when Istio is enabled. - Microsoft provides managed lifecycle (upgrades) for Istio components when triggered by user.
- Verified external and internal ingress set-up.
- Verified to work with
[Azure Monitor managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)and[Azure Managed Grafana](/en-us/azure/managed-grafana/overview). - Official Azure support provided for the add-on.

## Limitations

Istio-based service mesh add-on for AKS has the following limitations:

- The add-on doesn't work on AKS clusters that are using
[Open Service Mesh addon for AKS](open-service-mesh-about). - The add-on doesn't work on AKS clusters with self-managed installations of Istio.
- The add-on doesn't support adding pods associated with virtual nodes to be added under the mesh.
- The add-on doesn't yet support the sidecar-less Ambient mode. Microsoft is currently contributing to Ambient workstream under Istio open source. Product integration for Ambient mode is on the roadmap and is being continuously evaluated as the Ambient workstream evolves.
- The add-on doesn't yet support multi-cluster deployments.
- The add-on doesn't yet support Windows Server containers. Windows Server containers aren't yet supported in open source Istio right now. Issue tracking this feature ask can be found
[here](https://github.com/istio/istio/issues/27893). - Customization of mesh through the following custom resources is currently blocked -
`ProxyConfig, WorkloadEntry, WorkloadGroup, IstioOperator, WasmPlugin`

. - While the add-on allows the use of
`EnvoyFilter`

's, issues arising from them (for example from the Lua script or from the compression library) are outside the support scope of the Istio add-on. See the[support policy document](istio-support-policy#allowed-supported-and-blocked-customizations)for more information about the support categories for Istio add-on features and configuration options. - Gateway API for Istio ingress gateway or managing mesh traffic (GAMMA) is currently not yet supported with Istio add-on. However, Gateway API for Istio ingress traffic management is currently under active development for the add-on. While the add-on supports
[annotation and](istio-deploy-ingress#ingress-gateway-service-customizations), port or protocol configuration is currently not supported.`externalTrafficPolicy`

customization for the Istio ingress gateways - The add-on supports customization of a subset of the fields in
[MeshConfig](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/). Other customizations may be allowed but unsupported or disallowed entirely, as detailed[here](istio-meshconfig#allowed-supported-and-blocked-meshconfig-values).

## Feedback and feature ask

Feedback and feature ask for the Istio add-on can be provided by creating [issues with label 'service-mesh' on AKS GitHub repository](https://github.com/Azure/AKS/issues?q=is%3Aopen+is%3Aissue+label%3Aservice-mesh).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/reduce-latency-ppg -->

# Use proximity placement groups to reduce latency for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

When using proximity placement groups on AKS, colocation only applies to the agent nodes. Node to node and the corresponding hosted pod to pod latency is improved. The colocation doesn't affect the placement of a cluster's control plane.

When deploying your application in Azure, you can create network latency by spreading virtual machine (VM) instances across regions or availability zones, which may impact the overall performance of your application. A proximity placement group is a logical grouping used to make sure Azure compute resources are physically located close to one another. Some applications, such as gaming, engineering simulations, and high-frequency trading (HFT) require low latency and tasks that can complete quickly. For similar high-performance computing (HPC) scenarios, consider using [proximity placement groups (PPG)](/en-us/azure/virtual-machines/co-location#proximity-placement-groups) for your cluster's node pools.

## Before you begin

This article requires Azure CLI version 2.14 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Limitations

- A proximity placement group can map to only
*one*availability zone. - A node pool must use Virtual Machine Scale Sets to associate a proximity placement group.
- A node pool can associate a proximity placement group at node pool create time only.

## Node pools and proximity placement groups

The first resource you deploy with a proximity placement group attaches to a specific data center. Any extra resources you deploy with the same proximity placement group are colocated in the same data center. Once all resources using the proximity placement group are stopped (deallocated) or deleted, it's no longer attached.

- You can associate multiple node pools with a single proximity placement group.
- You can only associate a node pool with a single proximity placement group.

### Configure proximity placement groups with availability zones

Note

While proximity placement groups require a node pool to use only *one* availability zone, the [baseline Azure VM SLA of 99.9%](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_9/) is still in effect for VMs in a single zone.

Proximity placement groups are a node pool concept and associated with each individual node pool. Using a PPG resource has no impact on AKS control plane availability, which can impact how you should design your cluster with zones. To ensure a cluster is spread across multiple zones, we recommend using the following design:

- Provision a cluster with the first system pool using
*three*zones and no proximity placement group associated to ensure the system pods land in a dedicated node pool, which spreads across multiple zones. - Add extra user node pools with a unique zone and proximity placement group associated to each pool. An example is
*nodepool1*in zone one and PPG1,*nodepool2*in zone two and PPG2, and*nodepool3*in zone 3 with PPG3. This configuration ensures that, at a cluster level, nodes are spread across multiple zones and each individual node pool is colocated in the designated zone with a dedicated PPG resource.

## Create a new AKS cluster with a proximity placement group

Accelerated networking greatly improves networking performance of virtual machines. Ideally, use proximity placement groups with accelerated networking. By default, AKS uses accelerated networking on [supported virtual machine instances](/en-us/azure/virtual-network/accelerated-networking-overview?toc=/azure/virtual-machines/linux/toc.json#limitations-and-constraints), which include most Azure virtual machine with two or more vCPUs.

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location centralus`

Create a proximity placement group using the

command. Make sure to note the ID value in the output.`az ppg create`

`az ppg create --name myPPG --resource-group myResourceGroup --location centralus --type standard`

The command produces an output similar to the following example output, which includes the

*ID*value you need for upcoming CLI commands.`{ "availabilitySets": null, "colocationStatus": null, "id": "/subscriptions/yourSubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.Compute/proximityPlacementGroups/myPPG", "location": "centralus", "name": "myPPG", "proximityPlacementGroupType": "Standard", "resourceGroup": "myResourceGroup", "tags": {}, "type": "Microsoft.Compute/proximityPlacementGroups", "virtualMachineScaleSets": null, "virtualMachines": null }`

Create an AKS cluster using the

command and replace the`az aks create`

*myPPGResourceID*value with your proximity placement group resource ID from the previous step.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --ppg myPPGResourceID --generate-ssh-keys`


## Add a proximity placement group to an existing cluster

You can add a proximity placement group to an existing cluster by creating a new node pool. You can then optionally migrate existing workloads to the new node pool and delete the original node pool.

Use the same proximity placement group that you created earlier to ensure agent nodes in both node pools in your AKS cluster are physically located in the same data center.

Create a new node pool using the

command and replace the`az aks nodepool add`

*myPPGResourceID*value with your proximity placement group resource ID.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name mynodepool \ --node-count 1 \ --ppg myPPGResourceID`


## Clean up

Delete the Azure resource group along with its resources using the

command.`az group delete`

`az group delete --name myResourceGroup --yes --no-wait`


## Next steps

Learn more about [proximity placement groups](/en-us/azure/virtual-machines/co-location#proximity-placement-groups).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kubelogin-authentication -->

# Use kubelogin to authenticate users in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The kubelogin plugin in Azure is a client-go credential [plugin](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#client-go-credential-plugins) that implements Microsoft Entra authentication. The kubelogin plugin offers features that aren't available in the kubectl command-line tool. For more information, see the [kubelogin introduction](https://azure.github.io/kubelogin/index.html) and the [kubectl introduction](https://kubernetes.io/docs/reference/kubectl/introduction/).

This article provides an overview and examples of how to use kubelogin for all supported Microsoft Entra authentication methods in AKS.

## Kubelogin authentication in AKS limitations

- Groups that are created in Microsoft Entra are included only by their
**ObjectID**value, and not by their display name. The`sAMAccountName`

command is available only for groups that are synchronized from on-premises Windows Server Active Directory.

- The service principal authentication method works only with managed Microsoft Entra, and not with the earlier version Azure Active Directory.
- The service principal can be a member of a maximum of 200
[Microsoft Entra groups](/en-us/entra/identity/hybrid/connect/how-to-connect-fed-group-claims). If you have more than 200 groups, consider using[application roles](/en-us/entra/external-id/customers/how-to-use-app-roles-customers).

- The device code authentication method doesn't work when a Microsoft Entra Conditional Access policy is set on a Microsoft Entra tenant. In that scenario, use web browser interactive authentication instead.

- The Azure CLI authentication method works only with AKS managed Microsoft Entra.

## How authentication works

Note

Keep in mind the following information about kubelogin authentication for AKS clusters integrated with Microsoft Entra:

**Clusters running Kubernetes version 1.24 or later**automatically use the kubelogin format.**Clusters running Kubernetes 1.24 or earlier**require manual conversion. You can use the device code authentication method to convert the kubeconfig file to use the exec plugin format.

For most interactions with kubelogin, you use the `convert-kubeconfig`

subcommand. The subcommand uses the kubeconfig file that's specified in `--kubeconfig`

or in the `KUBECONFIG`

environment variable to convert the final kubeconfig file to exec format based on the specified authentication method.

The authentication methods that kubelogin implements are Microsoft Entra OAuth 2.0 token grant flows. In each authentication method, the token isn't cached on the file system.

## Device code authentication

Device code is the default authentication method for the `convert-kubeconfig`

subcommand. This authentication method prompts the device code for the user to sign in from a browser session.

Note

Before the kubelogin and exec plugins were introduced, the Azure authentication method in kubectl supported only the device code flow. It used an earlier version of a library that produces a token that has the `audience`

claim with an `spn:`

prefix. It isn't compatible with [AKS managed Microsoft Entra](managed-azure-ad), which uses an [on-behalf-of (OBO)](/en-us/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) flow. When you run the `convert-kubeconfig`

subcommand, kubelogin removes the `spn:`

prefix from the audience claim.

### Parameters for device code authentication

The following table outlines parameters that you can use with device code authentication:

| Parameter | Description |
|---|---|
`-l devicecode` (optional) |
Specifies the kubelogin authentication method. This parameter is optional because device code is the default method. |
`--legacy` |
Uses legacy behavior for earlier versions of Azure Active Directory clusters. If you're using the kubeconfig file in an earlier version Azure Active Directory cluster, kubelogin automatically adds the `--legacy` flag. |
`--token-cache-dir` |
Overrides the default path of the token cache directory, which is ${HOME}/.kube/cache/kubelogin. |

## Azure CLI authentication

The Azure CLI (command: `-l azurecli`

) authentication method uses the signed-in context that the Azure CLI establishes to get the access token. The token is issued in the same Microsoft Entra tenant as `az login`

. kubelogin doesn't write tokens to the token cache file because the Azure CLI already manages them.

### Parameters for Azure CLI authentication

The following table outlines parameters that you can use with Azure CLI authentication:

| Parameter | Description |
|---|---|
`-l azurecli` |
Specifies the kubelogin authentication method. |
`--azure-config-dir` |
Specifies the Azure CLI configuration directory. The default directory is ${HOME}/.azure. |

## Sign in to Azure

Sign in to Azure using the [ az login](/en-us/cli/azure/authenticate-azure-cli-interactively#interactive-login) command.

```
az login
```


## Web browser interactive authentication

The web browser interactive (command: `-l interactive`

) method of authentication automatically opens a web browser to sign in the user. After the user is authenticated, the browser redirects to the local web server using the verified credentials. This authentication method complies with Conditional Access policy.

You can use either a bearer token or a Proof-of-Possession (PoP) token with this authentication method.

### Parameters for bearer token authentication

The following table outlines parameters that you can use with bearer token authentication:

| Parameter | Description |
|---|---|
`-l interactive` |
Specifies the kubelogin authentication method. |
`--token-cache-dir` |
Overrides the default path of the token cache directory, which is ${HOME}/.kube/cache/kubelogin. |

### Parameters for PoP token authentication

The following table outlines parameters that you can use with PoP token authentication:

| Parameter | Description |
|---|---|
`-l interactive` |
Specifies the kubelogin authentication method. |
`--pop-enabled` |
Enables PoP token authentication. |
`--pop-claims` |
Specifies the PoP token claims in a key-value pair format. For example, `u=/ARM/ID/OF/CLUSTER` . |

## Service principal authentication

The service principal (command: `-l spn`

) authentication method uses a service principal to sign in the user. You can provide the credential by setting an environment variable or by using the credential in a command-line argument. The supported credentials that you can use are a password or a Personal Information Exchange (PFX) client certificate.

### Parameters for service principal authentication

The following table outlines parameters that you can use with service principal authentication:

| Parameter | Description |
|---|---|
`-l spn` |
Specifies the kubelogin authentication method. |
`--client-id` |
The application ID (client-id) of the service principal. |
`--client-secret` |
The client secret of the service principal. |

## Managed identity authentication

Use the [managed identity](/en-us/entra/identity/managed-identities-azure-resources/overview) (command: `-l msi`

) authentication method for applications that connect to resources that support Microsoft Entra authentication. Examples include accessing Azure resources like an Azure virtual machine (VM), a virtual machine scale set, or Azure Cloud Shell.

You can use the default managed identity that's assigned to the resource or a specific user-assigned managed identity.

### Parameters for managed identity authentication

The following table outlines parameters that you can use with managed identity authentication:

| Parameter | Description |
|---|---|
`-l msi` |
Specifies the kubelogin authentication method. |
`--client-id` |
The application ID (client-id) of the user-assigned managed identity. If you don't specify this parameter, the default managed identity is used. |

## Workload identity authentication

The workload identity (command: `-l workloadidentity`

) authentication method uses identity credentials that are federated with Microsoft Entra to authenticate access to AKS clusters. The method uses Microsoft Entra integrated authentication. It works by setting the following environment variables:

| Variable | Description |
|---|---|
`AZURE_CLIENT_ID` |
The Microsoft Entra application ID that is federated with the workload identity. |
`AZURE_TENANT_ID` |
The Microsoft Entra tenant ID. |
`AZURE_FEDERATED_TOKEN_FILE` |
The file that contains a signed assertion of the workload identity, like a Kubernetes projected service account (JWT) token. |
`AZURE_AUTHORITY_HOST` |
The base URL of a Microsoft Entra authority. For example, `https://login.microsoftonline.com/` . |

You can use a [workload identity](/en-us/entra/workload-id/workload-identities-overview) to access Kubernetes clusters from CI/CD systems like GitHub or ArgoCD without storing service principal credentials in the external systems. To configure OpenID Connect (OIDC) federation from GitHub, see the [OIDC federation example](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-azure).

### Parameters for workload identity authentication

The following table outlines parameters that you can use with workload identity authentication:

| Parameter | Description |
|---|---|
`-l workloadidentity` |
Specifies the kubelogin authentication method. |

## Export the kubeconfig file path

Before you run the `convert-kubeconfig`

subcommand, export the kubeconfig file path to the `KUBECONFIG`

environment variable. For example:

```
export KUBECONFIG=/path/to/kubeconfig
```


## Convert the kubeconfig file

Run the `convert-kubeconfig`

subcommand to convert the kubeconfig file to use the exec plugin for your chosen authentication method.

```
kubelogin convert-kubeconfig
```


```
kubelogin convert-kubeconfig -l azurecli
```


```
# Bearer token authentication
kubelogin convert-kubeconfig -l interactive
# Proof-of-Possession (PoP) token authentication
kubelogin convert-kubeconfig -l interactive --pop-enabled --pop-claims "u=/ARM/ID/OF/CLUSTER"
```


-
[Use environment variables](#tabpanel_1_environment-variables) -
[Use command-line arguments](#tabpanel_1_command-line-arguments) -
[Use a client certificate](#tabpanel_1_client-certificate) -
[Use a PoP token with environment variables](#tabpanel_1_pop-token-environment-variables)

Run the

`convert-kubeconfig`

subcommand to convert the kubeconfig file to use the exec plugin.`kubelogin convert-kubeconfig -l spn`

Set the environment variables for the client ID and client secret or client certificate. For example:

`export AZURE_CLIENT_ID=<service-principal-client-id> export AZURE_CLIENT_SECRET=<service-principal-client-secret>`


```
# Default managed identity authentication
kubelogin convert-kubeconfig -l msi
# Specific managed identity authentication
kubelogin convert-kubeconfig -l msi --client-id <managed-identity-client-id>
```


```
kubelogin convert-kubeconfig -l workloadidentity
```


## Remove cached tokens

Remove cached tokens using the `kubelogin remove-tokens`

command.

```
kubelogin remove-tokens
```


## Get node information

Get node information using the `kubectl get`

command.

```
kubectl get nodes
```


## How to use kubelogin with AKS

AKS uses a pair of first-party Microsoft Entra applications. These application IDs are the same in all environments.

The AKS Microsoft Entra server application ID (server-id) that the server side uses is `6dae42f8-4368-4678-94ff-3960e28e3630`

. The access token that accesses AKS clusters must be issued for this application. In most kubelogin authentication methods, you must use `--server-id`

with `kubelogin get-token`

.

The AKS Microsoft Entra client application ID (client-id) that kubelogin uses to perform public client authentication on behalf of the user is `80faf920-1908-4b52-b5ef-a8e7bedfc67a`

. The client application ID is used in device code and web browser interactive authentication methods.

## Related content

- Learn how to integrate AKS with Microsoft Entra in the
[AKS managed Microsoft Entra integration](managed-azure-ad)how-to article. - To get started with managed identities in AKS, see
[Use a managed identity in AKS](use-managed-identity). - To get started with workload identities in AKS, see
[Use a workload identity in AKS](workload-identity-overview).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/customize-resource-configuration -->

# Customize the resource configuration for managed add-ons

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of how to customize the resource configuration for Azure Kubernetes Service (AKS) managed add-ons with [cost optimized add-on scaling (Preview)](optimized-addon-scaling).

## Overview

Enabling the cost optimized add-on scaling feature in your AKS cluster installs the Vertical Pod Autoscaler (VPA) add-on and VPA custom resources for AKS managed add-ons that support this capability. This feature also allows you to manually customize the resource CPU and memory requests and limits in Deployments and DaemonSets. You can also customize the maximum and minimum allowed CPU and memory and the VPA update mode within VPA custom resources.

## Prerequisites

- Review the
[supported AKS managed add-ons](optimized-addon-scaling#supported-aks-add-ons)and[limitations](optimized-addon-scaling)for this feature. - You need an AKS cluster enabled with the cost optimized add-on scaling feature. If you don't have one, see
[Enable cost optimized add-on scaling on your AKS cluster (Preview)](optimized-addon-scaling).

## Customize resource annotations

| Annotation | Description | Values |
|---|---|---|
`kubernetes.azure.com/override-requests-limits` |
Supports the capability to customize the container resource CPU/memory requests/limits in a Deployment or DaemonSet if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. | "enabled" or "disabled" |
`kubernetes.azure.com/override-min-max` |
Supports the capability to customize the container policy maximum/minimum allowed CPU/memory value in VPA custom resource if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. | "enabled" or "disabled" |
`kubernetes.azure.com/override-update-mode` |
Supports the capability to customize the update policy `updateMode` value in a VPA custom resource if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. |
"enabled" or "disabled" |

## Customize resource CPU/memory requests/limits

After setting the `kubernetes.azure.com/override-requests-limits`

annotation to "enabled" in a Deployment or DaemonSet, you can customize the resource CPU/memory requests and limits. The following example shows how to customize the resource CPU/memory requests and limits in a Deployment:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-requests-limits: "enabled"
spec:
...
containers:
- name: coredns
resources:
limits:
# update cpu limits value won't be reconciled back
cpu: "3"
# update memory limits value won't be reconciled back
memory: "500Mi"
requests:
# update cpu requests value won't be reconciled back
cpu: "100m"
# update memory requests value won't be reconciled back
memory: "70Mi"
```


## Customize resource maximum/minimum allowed CPU/memory

After setting the `kubernetes.azure.com/override-min-max`

annotation to "enabled" in a VPA custom resource, you can customize the maximum and minimum allowed CPU and memory values in a VPA custom resource. The following example shows how to customize the maximum and minimum allowed CPU and memory values in a VPA custom resource:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-min-max: "enabled"
spec:
resourcePolicy:
containerPolicies:
- containerName: coredns
maxAllowed:
# update maxAllowed cpu value won't be reconciled back
cpu: 3
# update maxAllowed memory value won't be reconciled back
memory: 500Mi
minAllowed:
# update minAllowed cpu value won't be reconciled back
cpu: 10m
# update minAllowed memory value won't be reconciled back
memory: 10Mi
...
```


## Customize resource update mode

After setting the `kubernetes.azure.com/override-update-mode`

annotation to "enabled" in a VPA custom resource, you can customize the update policy `updateMode`

value in a VPA custom resource to "Off" or "Initial" (default). The following example shows how to customize the update policy `updateMode`

value to "Initial" in a VPA custom resource:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-update-mode: "enabled"
spec:
...
updatePolicy:
# update updateMode won't be reconciled back
updateMode: "Initial"
```


## Disable VPA on a specific AKS managed add-on

To disable VPA on a specific AKS managed add-on, you need to update the VPA custom resource YAML file to set the `kubernetes.azure.com/override-update-mode`

annotation to `"enabled"`

and the `updateMode`

to `"Off"`

. With *Off* mode, the VPA only provides CPU and memory recommendations and doesn't apply the changes to the pod.

The following example shows how to disable VPA on the CoreDNS add-on:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# Set value to "enabled"
kubernetes.azure.com/override-update-mode: "enabled"
spec:
...
updatePolicy:
# Set value to "Off"
updateMode: "Off"
```


## Troubleshooting

- Make sure the AKS managed add-on supports the cost optimized add-on scaling feature. For more information, see
[Supported AKS managed add-ons](optimized-addon-scaling#supported-aks-add-ons). - Verify that the
`kubernetes.azure.com/override-requests-limits`

annotation in the Deployment or DaemonSet is set to "enabled". - Verify that the
`kubernetes.azure.com/override-min-max`

annotation in the VPA custom resource is set to "enabled". - Verify that the
`kubernetes.azure.com/override-update-mode`

annotation in the VPA custom resource is set to "enabled".

## Next steps

To further configure cluster resource utilization and free up CPU/memory for AKS managed add-on pods, see [Vertical pod autoscaling in AKS](vertical-pod-autoscaler).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/localdns-custom -->

# Configure LocalDNS in Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

LocalDNS is a feature in Azure Kubernetes Service (AKS) designed to enhance the Domain Name System (DNS) resolution performance and resiliency for workloads running in your cluster. When you deploy a DNS proxy on each node, LocalDNS reduces DNS query latency, improves reliability during network disruptions, and provides advanced configuration options for DNS caching and forwarding. This article explains how LocalDNS works, its configuration options, and how to enable, verify, and troubleshoot LocalDNS in your AKS clusters.

To learn about what LocalDNS is, including architecture details, and key capabilities, refer to [DNS Resolution in Azure Kubernetes Service (AKS)](dns-concepts).

## Best practices for LocalDNS configuration

When implementing LocalDNS in your AKS clusters, consider the following best practices:

**Start with a minimal configuration**: Begin with a simple configuration that uses the`Preferred`

mode before moving to`Required`

mode. This setup allows you to validate that LocalDNS works as expected without breaking your cluster.**Implement proper caching strategies**: Configure cache settings based on your workload characteristics:- For frequently changing records, use shorter
`cacheDurationInSeconds`

values. When doing so, it's important to note that cacheDurationInSeconds acts as a cap on the DNS record TTL but doesn't increase it. The resulting TTL is the smaller of what is returned from upstream or what is set in the cache plugin. - For stable records, use longer cache durations to reduce DNS queries.
- Enable
`serveStale`

with appropriate settings to maintain service during DNS outages. - Caching with LocalDNS operates on a best effort basis and doesn't guarantee stale responses. The cache is divided into 256 shards and with a default maximum of 10,000 entries, allowing each shard to hold about 39 entries. When a shard is full and a new entry needs to be added, one of the existing entries is chosen at random to be evicted. There's no preference for older or expires entries. As a result, a stale record might not always be available, especially under high query volume.

- For frequently changing records, use shorter
**Monitor DNS performance**: After enabling LocalDNS, monitor your application's DNS performance using:- Application performance metrics.
- Node metrics to detect reduced network pressure.
- Log entries when
`queryLogging`

is set to`Log`

.

**Follow least privilege principle**: When configuring DNS forwarding rules, only allow access to the required DNS servers and domains.**Test before production deployment**: Always test LocalDNS configuration in a nonproduction environment before rolling it out to production clusters.**Use Infrastructure as Code (IaC)**: Store your*localdnsconfig.json*file in your infrastructure repository and include it in your AKS deployment templates.**Network configuration for TCP forwarding**: When using TCP for DNS forwarding to VNetDNS, ensure that your Network Security Groups (NSGs), firewalls, or Network Virtual Appliances (NVAs) don't block TCP traffic between CoreDNS/LocalDNS and VNetDNS servers.**Avoid enabling both NodeLocal DNSCache and LocalDNS**: It isn't recommended to enable both the upstream Kubernetes NodeLocal DNSCache and LocalDNS in your node pool. While AKS doesn't block this configuration, all DNS traffic is routed through LocalDNS, which might lead to unexpected behavior or reduced benefits from NodeLocal DNSCache.

## Prerequisites

You must have an existing AKS cluster with Kubernetes versions 1.31 and later to use LocalDNS. If you need an AKS cluster, you can create one using

[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal).This article requires Azure CLI version 2.80.0 and later. If you're using Azure Cloud Shell, the latest version is already installed.

LocalDNS is only supported on node pools running Azure Linux or Ubuntu 22.04 and newer.

The Virtual Machine (VM) SKU used for your node pool must have at least 4 vCPUs (cores) to support LocalDNS.

LocalDNS isn't compatible with applied Fully Qualified Domain Names (FQDN) filter policies in

[Advanced Container Networking Services (ACNS)](how-to-apply-fqdn-filtering-policies).

## Manage LocalDNS on an AKS cluster

LocalDNS is configured at the node pool level in AKS, meaning you can enable or disable LocalDNS independently for each node pool in your cluster. This tailors DNS resolution behavior based on the specific requirements of different workloads or environments. To enable LocalDNS on a node pool, you need to provide a configuration file: *localdnsconfig.json* that defines how LocalDNS should operate for that node pool.

If you don't specify a custom configuration file, AKS automatically applies a default LocalDNS configuration.

Note

If you're using Node Auto-Provisioning (NAP), see [LocalDNS configuration](node-auto-provisioning-aksnodeclass#localdns-configuration) for instructions on how to enable LocalDNS with NAP.

To enable LocalDNS during node pool creation, use the following command with your custom configuration file:

```
az aks nodepool add --name mynodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --localdns-config ./localdnsconfig.json
```


To enable LocalDNS on an existing node pool, use the following command with your custom configuration file:

```
az aks nodepool update --name mynodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --localdns-config ./localdnsconfig.json
```


Important

Enabling LocalDNS on a node pool initiates a reimage operation on all nodes within that pool. This process can cause temporary disruption to running workloads and might lead to application downtime if not properly managed. You should plan for potential service interruptions and ensure that the applications are configured for high availability or have appropriate disruption budgets in place before enabling this setting.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-cni-powered-by-cilium -->

# Configure Azure CNI Powered by Cilium in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure CNI Powered by Cilium combines the robust control plane of Azure Container Networking Interface (CNI) with the data plane of [Cilium](https://cilium.io/) to provide high-performance networking and security.

Azure CNI Powered by Cilium provides the following benefits by making use of eBPF programs loaded into the Linux kernel and a more efficient API object structure:

- Functionality equivalent to existing Azure CNI and Azure CNI Overlay plugins
- Improved service routing
- More efficient network policy enforcement
- Better observability of cluster traffic
- Support for larger clusters (more nodes, pods, and services)

## IP Address Management (IPAM) with Azure CNI Powered by Cilium

You can deploy Azure CNI Powered by Cilium with two different methods for assigning pod IPs:

- Assign IP addresses from an overlay network (similar to Azure CNI Overlay mode)
- Assign IP addresses from a virtual network (similar to existing Azure CNI with Dynamic Pod IP Assignment)

If you aren't sure which option to select, read [Choose a network model](concepts-network-azure-cni-overlay#choose-a-network-model)

## Versions

| Kubernetes Version | Minimum Cilium Version |
|---|---|
| 1.29 (LTS) | 1.14.19 |
| 1.30 | 1.14.19 |
| 1.31 | 1.16.6 |
| 1.32 | 1.17.0 |
| 1.33 | 1.17.0 |

For more information on AKS versioning and release timelines, see [Supported Kubernetes Versions](supported-kubernetes-versions).

## Network Policy Enforcement

Cilium enforces [network policies to allow or deny traffic between pods](operator-best-practices-network#control-traffic-flow-with-network-policies). With Cilium, you don't need to install a separate network policy engine such as Azure Network Policy Manager or Calico.

## Local Redirect Policy (LRP)

LRP starts to be supported from Kubernetes v1.29 and up, Cilium v1.14 and up. For LRP to work with Advanced Container Networking Services (ACNS) - FQDN Filtering, the Cilium Network Policy egress labels need to match with node-local DNS cache pod labels.

## Limitations

Azure CNI powered by Cilium currently has the following limitations:

- Available only for Linux and not for Windows.
- Network policies can't use
`ipBlock`

to allow access to node or pod IPs. For details and recommended workarounds, see[frequently asked questions](#frequently-asked-questions). - For Cilium versions 1.16 or earlier, multiple Kubernetes services can't use the same host port with different protocols (for example, TCP or UDP) (
[Cilium issue #14287](https://github.com/cilium/cilium/issues/14287)). - Network policies aren't applied to pods using host networking (
`spec.hostNetwork: true`

) because these pods use the host identity instead of having individual identities. - Cilium Endpoint Slices are supported in Kubernetes version 1.32 and above. Cilium Endpoint Slices don't support configuration of how Cilium Endpoints are grouped. Priority namespace through
`cilium.io/ces-namespace`

isn't supported. - L7 policy isn't supported by
`CiliumClusterwideNetworkPolicy`

(CCNP). - Cilium uses Cilium identities as unique identity for provisioning endpoints, so high-churning workloads such as Spark jobs generate high count of Cilium identities. To avoid workloads hitting Cilium identity limits (65535), excluding Spark job's labels like
`!spark-app-name`

and`!spark-app-selector`

in the Cilium configmap can significantly reduce Cilium identity generation. For more details on Cilium identity exclusion rules, check[the official Cilium label documentation](https://docs.cilium.io/en/stable/operations/performance/scalability/identity-relevant-labels/#excluding-labels). - AKS Local DNS isn't compatible with Advanced Container Networking Services (ACNS) - FQDN Filtering.

## Considerations

To gain capabilities such as observability into your network traffic and security features like Fully Qualified Domain Name (FQDN) based filtering and Layer 7 based network policies on your cluster, consider enabling [Advanced Container Networking services](advanced-container-networking-services-overview) on your clusters.

## Prerequisites

- Azure CLI version 2.48.1 or later. Run
`az --version`

to see the currently installed version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you're using ARM templates or the REST API, the AKS API version must be
`2022-09-02-preview`

or later.

Previous AKS API versions (`2022-09-02preview`

to `2023-01-02preview`

) used the field [ networkProfile.ebpfDataplane=cilium](https://github.com/Azure/azure-rest-api-specs/blob/06dbe269f7d9c709cc225c92358b38c3c2b74d60/specification/containerservice/resource-manager/Microsoft.ContainerService/aks/preview/2022-09-02-preview/managedClusters.json#L6939-L6955). AKS API versions since

`2023-02-02preview`

use the field [to enable Azure CNI Powered by Cilium.](https://github.com/Azure/azure-rest-api-specs/blob/06dbe269f7d9c709cc225c92358b38c3c2b74d60/specification/containerservice/resource-manager/Microsoft.ContainerService/aks/preview/2023-02-02-preview/managedClusters.json#L7152-L7173)

`networkProfile.networkDataplane=cilium`

## Create a new AKS Cluster with Azure CNI Powered by Cilium

The following sections use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command to create a cluster and assign IP addresses.

### Option 1: Assign IP addresses from an overlay network

Use the following commands to create a cluster with an overlay network and Cilium. Replace the values for `<clusterName>`

, `<resourceGroupName>`

, and `<location>`

:

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--network-plugin azure \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16 \
--network-dataplane cilium \
--generate-ssh-keys
```


The `--network-dataplane cilium`

flag replaces the deprecated `--enable-ebpf-dataplane`

flag used in earlier versions of the aks-preview CLI extension.

### Option 2: Assign IP addresses from a virtual network

Run the following commands to create a resource group and virtual network with a subnet for nodes and a subnet for pods.

```
# Create the resource group
az group create --name <resourceGroupName> --location <location>
```


```
# Create a virtual network with a subnet for nodes and a subnet for pods
az network vnet create --resource-group <resourceGroupName> --location <location> --name <vnetName> --address-prefixes <address prefix, example: 10.0.0.0/8> -o none
az network vnet subnet create --resource-group <resourceGroupName> --vnet-name <vnetName> --name nodesubnet --address-prefixes <address prefix, example: 10.240.0.0/16> -o none
az network vnet subnet create --resource-group <resourceGroupName> --vnet-name <vnetName> --name podsubnet --address-prefixes <address prefix, example: 10.241.0.0/16> -o none
```


Create the cluster using `--network-dataplane cilium`

:

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--max-pods 250 \
--network-plugin azure \
--vnet-subnet-id /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.Network/virtualNetworks/<vnetName>/subnets/nodesubnet \
--pod-subnet-id /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.Network/virtualNetworks/<vnetName>/subnets/podsubnet \
--network-dataplane cilium \
--generate-ssh-keys
```


### Option 3: Assign IP addresses from the Node Subnet

Azure CLI version 2.69.0 or later is required. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Create a cluster using [node subnet](concepts-network-legacy-cni#azure-cni-node-subnet) with a Cilium data plane:

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--network-plugin azure \
--network-dataplane cilium \
--generate-ssh-keys
```


## Frequently asked questions

**Can I customize Cilium configuration?**No, AKS manages the Cilium configuration and it can't be modified. We recommend that customers who require more control use

[AKS BYO CNI](use-byo-cni)and install Cilium manually.**Can I use**`CiliumNetworkPolicy`

custom resources instead of Kubernetes`NetworkPolicy`

resources?L3 and L4

`CiliumNetworkPolicy`

are supported and can be used alongside Kubernetes`NetworkPolicy`

resources.Customers might use FQDN filtering and Layer 7 policies as part of the

[Advanced Container Networking Services](advanced-container-networking-services-overview)feature bundle.**Can I use**`CiliumClusterwideNetworkPolicy`

?Yes,

`CiliumClusterwideNetworkPolicy`

is supported. The following sample policy YAML shows configuring an L4 rule:`apiVersion: "cilium.io/v2" kind: CiliumClusterwideNetworkPolicy metadata: name: "l4-rule-ingress-backend-frontend" spec: endpointSelector: matchLabels: role: backend ingress: - fromEndpoints: - matchLabels: role: frontend toPorts: - ports: - port: "80" protocol: TCP`

**Which Cilium features are supported in Azure managed CNI? Which of those require Advanced Container Networking Services?**Supported Feature w/o ACNS w/ ACNS Cilium Endpoint Slices ✔️ ✔️ K8s Network Policies ✔️ ✔️ Cilium L3/L4 Network Policies ✔️ ✔️ Cilium Clusterwide Network Policy ✔️ ✔️ FQDN Filtering ❌ ✔️ L7 Network Policies (HTTP/gRPC/Kafka) ❌ ✔️ Container Network Observability (Metrics and Flow logs) ❌ ✔️ eBPF Host Routing ❌ ✔️ **Why is traffic being blocked when the**`NetworkPolicy`

has an`ipBlock`

that allows the IP address?A limitation of Azure CNI Powered by Cilium is that a

`NetworkPolicy`

`ipBlock`

can't select pod or node IPs.For example, this

`NetworkPolicy`

has an`ipBlock`

that allows all egress to`0.0.0.0/0`

:`apiVersion: networking.k8s.io/v1 kind: NetworkPolicy metadata: name: example-ipblock spec: podSelector: {} policyTypes: - Egress egress: - to: - ipBlock: cidr: 0.0.0.0/0 # This will still block pod and node IPs.`

However, when this

`NetworkPolicy`

is applied, Cilium blocks egress to pod and node IPs even though the IPs are within the`ipBlock`

CIDR.As a workaround, you can add

`namespaceSelector`

and`podSelector`

to select pods. This example selects all pods in all namespaces:`apiVersion: networking.k8s.io/v1 kind: NetworkPolicy metadata: name: example-ipblock spec: podSelector: {} policyTypes: - Egress egress: - to: - ipBlock: cidr: 0.0.0.0/0 - namespaceSelector: {} - podSelector: {}`

It isn't currently possible to specify a

`NetworkPolicy`

with an`ipBlock`

to allow traffic to node IPs.**Does AKS configure CPU or memory limits on the Cilium**`daemonset`

?No, AKS doesn't configure CPU or memory limits on the Cilium

`daemonset`

because Cilium is a critical system component for pod networking and network policy enforcement.**Does Azure CNI powered by Cilium use kube-proxy?**No, AKS clusters created with network data plane as Cilium don't use

`kube-proxy`

. If the AKS clusters are on[Azure CNI Overlay](azure-cni-overlay)or[Azure CNI with dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)and are upgraded to AKS clusters running Azure CNI powered by Cilium, new nodes workloads are created without`kube-proxy`

. Older workloads are also migrated to run without`kube-proxy`

as a part of this upgrade process.

## Dual-stack networking with Azure CNI Powered by Cilium

You can deploy your dual-stack AKS clusters with Azure CNI Powered by Cilium. This feature also allows you to control your IPv6 traffic with the Cilium Network Policy engine.

You must have Kubernetes version 1.29 or greater.

### Set up Overlay clusters with Azure CNI Powered by Cilium

Create a cluster with Azure CNI Overlay using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command. Make sure to use the argument

`--network-dataplane cilium`

to specify the Cilium data plane.```
clusterName="myOverlayCluster"
resourceGroup="myResourceGroup"
location="westcentralus"
az aks create \
--name $clusterName \
--resource-group $resourceGroup \
--location $location \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--ip-families ipv4,ipv6 \
--generate-ssh-keys
```


## Next steps

Learn more about networking in AKS in the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-best-practices -->

# Best practices for Windows containers on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In AKS, you can create node pools that run Linux or Windows Server as the operating system (OS) on the nodes. Windows Server nodes can run native Windows container applications, such as .NET Framework. The Linux OS and Windows OS have different container support and configuration considerations. For more information, see [Windows container considerations in Kubernetes](windows-vs-linux-containers). To learn more about how various industries are using Windows containers on AKS, see [Windows AKS customer stories](windows-aks-customer-stories).

This article outlines best practices for running Windows containers on AKS.

## Create an AKS cluster with Linux and Windows node pools

When you create a new AKS cluster, the Azure platform creates a Linux node pool by default. This node pool contains system services needed for the cluster to function. Azure also creates and manages a control plane abstracted from the user, which means you aren't exposed to the underlying OS of the nodes hosting the main control plane components. We recommend that you run at least *two nodes* on the default Linux node pool to ensure the reliability and performance of your cluster. You can't delete the default Linux node pool unless you delete the entire cluster.

There are some cases where you should consider deploying a Linux node pool when planning to run Windows-based workloads on your AKS cluster, such as:

- If you want to run Linux and Windows workloads, you can deploy a Linux node pool and a Windows node pool in the same cluster.
- If you want to deploy infrastructure-related components based on Linux, such as NGINX, you need a Linux node pool alongside your Windows node pool. You can use control plane nodes for development and testing scenarios. For production workloads, we recommend that you deploy separate Linux node pools to ensure reliability and performance.

## Modernize existing applications with Windows on AKS

You might want to containerize existing applications and run them using Windows on AKS. Before starting the containerization process, it's important to understand the application architecture and dependencies. For more information, see [Containerize existing applications using Windows containers](/en-us/virtualization/windowscontainers/quick-start/lift-shift-to-containers).

## Windows OS version


Best practice guidanceWindows Server 2022 provides improved security and performance and is the recommended OS for Windows node pools on AKS. AKS uses Windows Server 2022 as the host OS version and only supports process isolation.


AKS supports two options for the Windows Server operating system: Long Term Servicing Channel Releases (LTSC) and Windows Server Annual Channel for Containers.

AKS supports Long Term Servicing Channel Releases (LTSC), including Windows Server 2025 (preview), Windows Server 2022, and Windows Server 2019. This channel is released every three years and is supported for five years. Customers using Long Term Support (LTS) should use Windows Server 2022.

AKS uses Windows Server 2019 and Windows Server 2022 as the host OS versions and only supports process isolation. AKS doesn't support container images built by other versions of Windows Server. For more information, see

[Windows container version compatibility](/en-us/virtualization/windowscontainers/deploy-containers/version-compatibility). Windows Server 2022 is the default OS for Kubernetes version 1.25 and later.Note

[Windows Server 2019 retires on March 1, 2026](https://github.com/Azure/AKS/issues/4091). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2019 on any Kubernetes version. All existing node pools with Windows Server 2019 will be unsupported. Windows Server 2019 is not supported in Kubernetes version 1.33 and above. Starting on April 1, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail.[Windows Server 2022 retires on March 15, 2027](https://github.com/Azure/AKS/issues/4168). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2022 on any Kubernetes version. All existing node pools with Windows Server 2022 will be unsupported. Windows Server 2022 is not supported in Kubernetes version 1.36 and above. Starting on April 1, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail.

For more information, see

[AKS release notes](https://github.com/Azure/AKS/releases). To stay up to date on the latest Windows Server OS versions and learn more about our roadmap of what's planned for support on AKS, see our[AKS public roadmap](https://github.com/azure/aks/projects/1).AKS supports

[Windows Server Annual Channel for Containers](https://techcommunity.microsoft.com/t5/windows-server-news-and-best/windows-server-annual-channel-for-containers/ba-p/3866248)(preview). This channel is released annually and is supported for two years. This channel is beneficial for customers requiring increased innovation cycles and portability. The portability functionality enables the Windows Server 2022-based container image OS to run on newer versions of Windows Server host OS, such as the new annual channel release.Windows Annual Channel versions are based on the Kubernetes version of your node pool. To upgrade from one Annual Channel version to the next,

[upgrade to a Kubernetes version](upgrade-aks-cluster)that supports the next Annual Channel version. For more information, see[Windows Server Annual Channel for Containers on AKS](windows-annual-channel).

## Monitoring


Best practice guidanceWindows Exporter is installed on all Windows nodes in certain regions. To view regional rollout, see

[AKS Github]. With Managed Prometheus and Grafana, you can monitor default collectors included in Windows Exporter on AKS. For more information, see[default Prometheus metrics configured in Azure Monitor].

Windows Exporter allows customers to see their metrics through Managed Prometheus or Prometheus OSS deployments and enjoy enhanced observability around their node and pod performance, health, and resource usage. These metrics are also visible with Managed Grafana.

- When enabling managed prometheus, add this required parameter for correct dashboard data presentation for Windows:
`--enable-windows-recording-rules`

. - Grafana includes dashboards for showing Windows resources, such as:
- Kubernetes / Compute Resources / Cluster (Windows)
- Kubernetes / Compute Resources / Namespace (Windows)
- Kubernetes / Compute Resources / Pod (Windows)
- Kubernetes / USE Method / Cluster (Windows)
- Kubernetes / USE Method / Node (Windows)


The default collectors included in Windows Exporter on AKS are: cpu, cpu_info, cs, container, logical_disk, memory, net, os, process, service, system, textfile. The metrics are exposed on port **19182** on the windows node. For more information on what metrics you can see using these collectors, please see [prometheus-community/windows_exporter](https://github.com/prometheus-community/windows_exporter#collectors).

## Networking

### Networking modes


Best practice guidanceAKS clusters with Windows node pools only support Azure Container Networking Interface (Azure CNI) and use it by default.


Windows doesn't support kubenet networking. AKS clusters with Windows node pools must use Azure CNI. For more information, see [Network concepts for applications in AKS](concepts-network).

Azure CNI offers two networking modes based on your workload requirements:

is an overlay network similar to kubenet. The overlay network allows you to use virtual network (VNet) IPs for nodes and private address spaces for pods within those nodes that you can reuse across the cluster. Azure CNI Overlay is the**Azure CNI Overlay****recommended networking mode**. It provides simplified network configuration and management and the best scalability in AKS networking.requires extra planning and consideration for IP address management. This mode provides VNet IPs for nodes**Azure CNI with Dynamic IP Allocation***and*pods. This configuration allows you direct access to pod IPs. However, it comes with increased complexity and reduced scalability.

To help you decide which networking mode to use, see [Choosing a network model](concepts-network-azure-cni-overlay#choose-a-network-model).

### Network policies


Best practice guidanceUse network policies to secure traffic between pods. Windows supports Azure Network Policy Manager and Calico Network Policy. For more information, see

[Differences between Network Policy engines: Cilium, Azure NPM, and Calico].

When managing traffic between pods, you should apply the principle of least privilege. The Network Policy feature in Kubernetes allows you to define and enforce ingress and egress traffic rules between the pods in your cluster. For more information, see [Secure traffic between pods using network policies in AKS](use-network-policies).

Windows pods on AKS clusters that use the Calico Network Policy enable Floating IP by default.

## Upgrades and updates

It's important to keep your Windows environment up-to-date to ensure your systems have the latest security updates, feature sets, and compliance requirements. In a Kubernetes environment like AKS, you need to maintain the Kubernetes version, Windows nodes, and Windows container images and pods.

### Kubernetes version upgrades

As a managed Kubernetes service, AKS provides the necessary tools to upgrade your cluster to the latest Kubernetes version. For more information, see [Upgrade an AKS cluster](upgrade-cluster).

### Windows node monthly updates

Windows nodes on AKS follow a monthly update schedule. Every month, AKS creates a new VHD with the latest available updates for Windows node pools. The VHD includes the host image, latest Nano Server image, latest Server Core image, and container. We recommend performing monthly updates to your Windows node pools to ensure your nodes have the latest security patches. For more information, see [Upgrade AKS node images](node-image-upgrade).

Note

Upgrades on Windows systems include both OS version upgrades and monthly node OS updates.

You can stay up to date with the availability of new monthly releases using the [AKS release tracker](https://releases.aks.azure.com/) and [AKS release notes](https://github.com/Azure/AKS/releases).

### Windows node OS version upgrades

Windows has a release cadence for new versions of the OS, including Windows Server 2025 (preview), Windows Server 2022, and Windows Server 2019. When upgrading your Windows node OS version, ensure the Windows container image version matches the Windows container host version and the node pools have only one version of Windows Server.

To upgrade the Windows node OS version, you need to complete the following steps:

- Create a new node pool with the new Windows Server version.
- Deploy your workloads with the new Windows container images to the new node pool.
- Decommission the old node pool.

For more information, see [Upgrade Windows Server workloads on AKS](upgrade-windows-2019-2022).

Note

Windows announced a new [Windows Server Annual Channel for Containers](https://techcommunity.microsoft.com/t5/windows-server-news-and-best/windows-server-annual-channel-for-containers/ba-p/3866248) that supports portability and mixed versions of Windows nodes and containers. This feature isn't yet supported in AKS.

To track AKS feature plans, see the [Public AKS roadmap](https://github.com/Azure/AKS/projects/1#card-90806240).

## Next steps

To learn more about Windows containers on AKS, see the following resources:

[Learn how to deploy, manage, and monitor Windows containers on AKS](/en-us/training/paths/deploy-manage-monitor-wincontainers-aks).- Open an issue or provide feedback in the
[Windows containers GitHub repository](https://github.com/microsoft/Windows-Containers/issues). - Review the
[third-party partner solutions for Windows on AKS](windows-aks-partner-solutions).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/start-stop-cluster -->

# Stop and start an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You may not need to continuously run your Azure Kubernetes Service (AKS) workloads. For example, you may have a development cluster that you only use during business hours. This means there are times where your cluster might be idle, running nothing more than the system components. You can reduce the cluster footprint by [scaling all User node pools to 0](scale-cluster#scale-user-node-pools-to-0), but your

[is still required to run the system components while the cluster is running.](use-system-pools)

`System`

poolTo better optimize your costs during these periods, you can turn off, or stop, your cluster. This action stops your control plane and agent nodes, allowing you to save on all the compute costs, while maintaining all objects except standalone pods. The cluster state is stored for when you start it again, allowing you to pick up where you left off.

Caution

Stopping your cluster deallocates the control plane and releases the capacity. In regions experiencing capacity constraints, customers may be unable to start a stopped cluster. We do not recommend stopping mission critical workloads for this reason.

Note

AKS start operations will restore all objects from ETCD with the exception of standalone pods with the same names and ages. meaning that a pod's age will continue to be calculated from its original creation time. This count will keep increasing over time, regardless of whether the cluster is in a stopped state.

## Before you begin

This article assumes you have an existing AKS cluster. If you need an AKS cluster, you can create one using [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

### About the cluster stop/start feature

When using the cluster stop/start feature, the following conditions apply:

- This feature is only supported for Virtual Machine Scale Set backed clusters.
- You can't stop clusters which use the
[Node Autoprovisioning (NAP)](node-autoprovision)feature. - The cluster state of a stopped AKS cluster is preserved for up to 12 months. If your cluster is stopped for more than 12 months, you can't recover the state. For more information, see the
[AKS support policies](support-policies). - You can only perform start or delete operations on a stopped AKS cluster. To perform other operations, like scaling or upgrading, you need to start your cluster first.
- If you provisioned PrivateEndpoints linked to private clusters, they need to be deleted and recreated again when starting a stopped AKS cluster.
- Because the stop process drains all nodes, any standalone pods (i.e. pods not managed by a Deployment, StatefulSet, DaemonSet, Job, etc.) will be deleted.
- When you start your cluster back up, the following behavior is expected:
- The IP address of your API server may change.
- If you're using cluster autoscaler, when you start your cluster, your current node count may not be between the min and max range values you set. The cluster starts with the number of nodes it needs to run its workloads, which isn't impacted by your autoscaler settings. When your cluster performs scaling operations, the min and max values will impact your current node count, and your cluster will eventually enter and remain in that desired range until you stop your cluster.


## Stop an AKS cluster

Use the

command to stop a running AKS cluster, including the nodes and control plane. The following example stops a cluster named`az aks stop`

*myAKSCluster*:`az aks stop --name myAKSCluster --resource-group myResourceGroup`

Verify your cluster has stopped using the

command and confirming the`az aks show`

`powerState`

shows as`Stopped`

.`az aks show --name myAKSCluster --resource-group myResourceGroup`

Your output should look similar to the following condensed example output:

`{ [...] "nodeResourceGroup": "MC_myResourceGroup_myAKSCluster_westus2", "powerState":{ "code":"Stopped" }, "privateFqdn": null, "provisioningState": "Succeeded", "resourceGroup": "myResourceGroup", [...] }`

If the

`provisioningState`

shows`Stopping`

, your cluster hasn't fully stopped yet.

Important

If you're using [pod disruption budgets](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/), the stop operation can take longer, as the drain process will take more time to complete.

## Start an AKS cluster

Caution

After utilizing the start/stop feature on AKS, it is essential to wait 15-30 minutes before restarting your AKS cluster. This waiting period is necessary because it takes several minutes for the relevant services to fully stop. Attempting to restart your cluster during this process can disrupt the shutdown process and potentially cause issues with the cluster or its workloads.

Use the

command to start a stopped AKS cluster. The cluster restarts with the previous control plane state and number of agent nodes. The following example starts a cluster named`az aks start`

*myAKSCluster*:`az aks start --name myAKSCluster --resource-group myResourceGroup`

Verify your cluster has started using the

command and confirming the`az aks show`

`powerState`

shows`Running`

.`az aks show --name myAKSCluster --resource-group myResourceGroup`

Your output should look similar to the following condensed example output:

`{ [...] "nodeResourceGroup": "MC_myResourceGroup_myAKSCluster_westus2", "powerState":{ "code":"Running" }, "privateFqdn": null, "provisioningState": "Succeeded", "resourceGroup": "myResourceGroup", [...] }`

If the

`provisioningState`

shows`Starting`

, your cluster hasn't fully started yet.

## Next steps

- To learn how to scale
`User`

pools to 0, see[Scale](scale-cluster#scale-user-node-pools-to-0).`User`

pools to 0 - To learn how to save costs using Spot instances, see
[Add a spot node pool to AKS](spot-node-pool). - To learn more about the AKS support policies, see
[AKS support policies](support-policies).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-ai-ml-language-models -->

# Concepts - Small and large language models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about small and large language models, including when to use them and how you can use them with your AI and machine learning workflows on Azure Kubernetes Service (AKS).

## What are language models?

Language models are powerful machine learning models used for natural language processing (NLP) tasks, such as text generation and sentiment analysis. These models represent natural language based on the probability of words or sequences of words occurring in a given context.

*Conventional language models* have been used in supervised settings for research purposes where the models are trained on well-labeled text datasets for specific tasks. *Pre-trained language models* offer an accessible way to get started with AI and have become more widely used in recent years. These models are trained on large-scale text corpora from the internet using deep neural networks and can be fine-tuned on smaller datasets for specific tasks.

The size of a language model is determined by its number of parameters, or *weights*, that determine how the model processes input data and generates output. Parameters are learned during the training process by adjusting the weights within layers of the model to minimize the difference between the model's predictions and the actual data. The more parameters a model has, the more complex and expressive it is, but also the more computationally expensive it is to train and use.

In general, **small language models** have *fewer than 10 billion parameters*, and **large language models** have *more than 10 billion parameters*. For example, the new Microsoft Phi-3 model family has three versions with different sizes: mini (3.8 billion parameters), small (7 billion parameters), and medium (14 billion parameters).

## When to use small language models

### Advantages

Small language models are a good choice if you want models that are:

**Faster and more cost-effective to train and run**: They require less data and compute power.**Easy to deploy and maintain**: They have smaller storage and memory footprints.**Less prone to**, which is when a model learns the noise or specific patterns of the training data and fails to generalize new data.*overfitting***Interpretable and explainable**: They have fewer parameters and components to understand and analyze.

### Use cases

Small language models are suitable for use cases that require:

**Limited data or resources**, and you need a quick and simple solution.**Well-defined or narrow tasks**, and you don't need much creativity in the output.**High-precision and low-recall tasks**, and you value accuracy and quality over coverage and quantity.**Sensitive or regulated tasks**, and you need to ensure the transparency and accountability of the model.

The following table lists some popular, high-performance small language models:

| Model family | Model sizes (Number of parameters) | Software license |
|---|---|---|
| Microsoft Phi-3 | Phi-3-mini (3.8 billion), Phi-3-small (7 billion) | MIT license |
| Microsoft Phi-2 | Phi-2 (2.7 billion) | MIT license |
| Falcon | Falcon-7B (7 billion) | Apache 2.0 license |

## When to use large language models

### Advantages

Large language models are a good choice if you want models that are:

**Powerful and expressive**: They can capture more complex patterns and relationships in the data.**General and adaptable**: They can handle a wider range of tasks and transfer knowledge across domains.**Robust and consistent**: They can handle noisy or incomplete inputs and avoid common errors and biases.

### Use cases

Large language models are suitable for use cases that require:

**Abundant data and resources**, and you have the budget to build and maintain a complex solution.**Low-precision and high-recall tasks**, and you value coverage and quantity over accuracy and quality.**Challenging or exploratory tasks**, and you want to leverage the model's capacity to learn and adapt.

The following table lists some popular, high-performance large language models:

| Model family | Model sizes (Number of parameters) | Software license |
|---|---|---|
| Microsoft Phi-3 | Phi-3-medium (14 billion) | MIT license |
| Falcon | Falcon-40B (40 billion) | Apache 2.0 license |

## Experiment with small and large language models on AKS

Kubernetes AI Toolchain Operator (KAITO) is an open-source operator that automates small and large language model deployments in Kubernetes clusters. The KAITO add-on for AKS simplifies onboarding and reduces the time-to-inference for open-source models on your AKS clusters. The add-on automatically provisions right-sized GPU nodes and sets up the associated interference server as an endpoint server to your chosen model.

For more information, see [Deploy an AI model on AKS with the AI toolchain operator](ai-toolchain-operator). To get started with a range of supported small and large language models for your inference workflows, see the [KAITO model GitHub repository](https://github.com/Azure/kaito/tree/main/presets).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Next steps

To learn more about containerized AI and machine learning workloads on AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-advanced-container-networking-services -->

# Use Advanced Container Networking Services on your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to enable and disable Advanced Container Networking Services, including [Container Network Observability](advanced-container-networking-services-overview#container-network-observability) and [Container Network Security](advanced-container-networking-services-overview#container-network-security), on your AKS clusters.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - Azure CLI version 2.71.0 or higher. Find your version using the
`az --version`

command. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). [Install the](#install-the-aks-preview-azure-cli-extension)version`aks-preview`

Azure CLI extension`14.0.0b6`

or higher.[Register the](#register-the-advancednetworkingl7policypreview-feature-flag)in your subscription.`AdvancedNetworkingL7PolicyPreview`

feature flag- Clusters that have the Cilium data plane support
*Container Network Observability*and*Container Network Security*in Kubernetes version 1.29 and later.

## Install the `aks-preview`

Azure CLI extension

Install or update the Azure CLI preview extension using the

or`az extension add`

command.`az extension update`

`# Install the aks-preview extension az extension add --name aks-preview # Update the extension to make sure you have the latest version installed az extension update --name aks-preview`


## Register the `AdvancedNetworkingL7PolicyPreview`

feature flag

Register the

`AdvancedNetworkingL7PolicyPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"`

Registration takes a few minutes to complete.

Verify successful registration using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"`


## Set environment variables

The examples in this article use the following environment variables:

| Variable | Description | Example value |
|---|---|---|
`RESOURCE_GROUP` |
Name of the Azure resource group | `myResourceGroup` |
`LOCATION` |
Azure region for resources | `eastus` |
`CLUSTER_NAME` |
Name of the AKS cluster | `myAKSCluster` |

**All commands in this article assume these environment variables are set**. Make sure to replace the example values with your own values.

## Create a resource group

Create a resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`


## Create a new AKS cluster with Advanced Container Networking Services

Note

When the `--acns-advanced-networkpolicies`

parameter is set to `L7`

, both Layer 7 and fully qualified domain name (FQDN) filtering policies are enabled. If you want to enable only FQDN filtering, set the parameter to `FQDN`

.

Create an AKS cluster with Advanced Container Networking Services and Cilium using the

command with the`az aks create`

`--enable-acns`

and`--network-dataplane cilium`

flags.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --network-plugin azure \ --network-plugin-mode overlay \ --network-dataplane cilium \ --kubernetes-version 1.29 \ --enable-acns \ --acns-advanced-networkpolicies <L7/FQDN>`


Important

The [Container Network Security](advanced-container-networking-services-overview#container-network-security) feature isn't available for non-Cilium clusters.

Create an AKS cluster with Advanced Container Networking Services using the

command with the`az aks create`

`--enable-acns`

flag.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --network-plugin azure \ --network-plugin-mode overlay \ --enable-acns`


## Enable Advanced Container Networking Services on an existing cluster

Enable Advanced Container Networking Services on an existing AKS cluster with Cilium using the

command with the`az aks update`

`--enable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --acns-advanced-networkpolicies <L7/FQDN>`


Enable Advanced Container Networking Services on an existing AKS cluster using the

command with the`az aks update`

`--enable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns`


## Disable Advanced Container Networking Services on an AKS cluster

Disable Advanced Container Networking Services on an existing AKS cluster using the

command with the`az aks update`

`--disable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --disable-acns`


## Disable Container Network Observability on an AKS cluster

Disable the Container Network Observability feature without affecting other Advanced Container Networking Services features using the

command with the`az aks update`

`--disable-acns-observability`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --disable-acns-observability`


Container Network Observability is the only feature available for non-Cilium clusters, so you can disable it only by disabling the entire Advanced Container Networking Services suite.

Disable the Container Network Observability feature on an existing AKS cluster using the

command with the`az aks update`

`--disable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --disable-acns`


## Disable Container Network Security on an AKS cluster

Disable the Container Network Security feature without affecting other Advanced Container Networking Services features using the

command with the`az aks update`

`--disable-acns-security`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --disable-acns-security`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-arm64-vms -->

# Use Arm-based processor (Arm64) Virtual Machines (VMs) in an Azure Kubernetes Service (AKS) cluster for cost effectiveness

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Arm-based processors (Arm64)](/en-us/azure/virtual-machines/sizes/cobalt-overview) are power-efficient and cost-effective, but don't compromise on performance. These Arm64 VMs are engineered to efficiently run dynamic, scalable workloads and can deliver up to 50% better price-performance than comparable x86-based VMs for scale-out workloads.

Because of their ability to scale workloads efficiently, Arm64 VMs are well-suited for web or application servers, open-source databases, cloud-native applications, gaming servers, and other high traffic applications.

Note

While a combination of CPU, memory, and networking capacity configurations heavily influences the cost effectiveness of a SKU, Arm64 VM types are recommended for cost optimization.

In this article, you'll learn how to add a Arm64 VM to an existing node pool.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

Before you begin, make sure you have:

## Limitations

- Arm64 VMs aren't supported for Windows node pools.
- Existing node pools can't be updated to use an Arm64 VM.
- Federal Information Process Standard (FIPS)-enabled node pools are only supported with Arm64 SKUs when using Azure Linux 3.0+.
- Arm64 node pools aren't supported on Defender-enabled clusters with Kubernetes version 1.29.0 or lower.

## Create node pools with Arm64 VMs

The Arm64 processor provides low power compute for your Kubernetes workloads. Arm64 virtual machines can be added to existing clusters even mixing Intel and Arm architecture node pools within a cluster. To create an Arm64 node pool, you need to choose a [Dpsv5](/en-us/azure/virtual-machines/dpsv5-dpdsv5-series), [Dplsv5](/en-us/azure/virtual-machines/dplsv5-dpldsv5-series), or [Epsv5](/en-us/azure/virtual-machines/epsv5-epdsv5-series) series virtual machine.

### Add a node pool with an Arm64 VM

Use [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) to add a node pool with an Arm64 VM to an existing cluster. Alternatively, if you're using

[Azure Linux 3.0+](/en-us/azure/azure-linux/how-to-enable-azure-linux-3), you can add a node pool with an Arm64 VM and

[FIPS](enable-fips-nodes)enabled.

Add a node pool with an Arm64 VM

`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $ARM_NODE_POOL_NAME \ --node-count 3 \ --node-vm-size Standard_D2pds_v5`

Add a FIPS-enabled node pool with an Arm64 VM

Limitations:

- Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)enabled aren't supported with Ubuntu OS. - Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)require kubernetes version 1.31+.

Use the

with`az aks nodepool add`

`--enable-fips-image`

and`--os-sku`

parameters.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $ARM_NODE_POOL_NAME \ --os-sku AzureLinux --enable-fips-image --kubernetes-version 1.31 --node-count 3 \ --node-vm-size Standard_D2pds_v5`

For more information on verifying FIPS enablement and disabling FIPS, see

[Enable FIPS node pools](enable-fips-nodes).- Node pools with Arm64 VMs and
Update a node pool with an Arm64 VM to enable FIPS

Limitations:

- Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)enabled aren't supported with Ubuntu OS. - Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)require kubernetes version 1.31+.

Use

command with the`az aks nodepool update`

`--enable-fips-image`

parameter to enable FIPS on an existing node pool.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name np \ --enable-fips-image`

This command triggers a reimage of the node pool immediately to deploy the FIPS compliant Operating System. This reimage occurs during the node pool update. No extra steps are required.

- Node pools with Arm64 VMs and

For more information on verifying FIPS enablement and disabling FIPS, see [Enable FIPS node pools](enable-fips-nodes).

## Verify the node pool uses Arm64

Verify a node pool uses Arm64 using the [ az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command and verify the

`vmSize`

is a [Dpsv5](/en-us/azure/virtual-machines/dpsv5-dpdsv5-series),

[Dplsv5](/en-us/azure/virtual-machines/dplsv5-dpldsv5-series), or

[Epsv5](/en-us/azure/virtual-machines/epsv5-epdsv5-series)series.

```
az aks nodepool show \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name mynodepool \
--query vmSize
```


The following example output shows the node pool uses Arm64:

```
"Standard_D2pds_v5"
```


## Next steps

In this article, you learned how to add a node pool with an Arm64 VM to an AKS cluster.

- For more recommendations for cost savings, see
[Best practices for cost optimization in Azure Kubernetes Service (AKS)](best-practices-cost). - For more information about Arm64, see
[Cobalt Arm-based processors (Arm64)](/en-us/azure/virtual-machines/sizes/cobalt-overview). - For more information on verifying FIPS enablement and disabling FIPS, see
[Enable FIPS node pools](enable-fips-nodes). - For Azure Linux 3.0 enablement and support details, see
[Enable Azure Linux 3.0](/en-us/azure/azure-linux/how-to-enable-azure-linux-3).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/optimized-addon-scaling -->

# Enable cost optimized add-on scaling on your Azure Kubernetes Service (AKS) cluster (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of cost optimized add-on scaling in Azure Kubernetes Service (AKS). With cost-optimized add-on scaling, you can manage add-ons that require custom CPU and memory by overriding default configurations or enabling autoscaling. This feature ensures that resources aren't overly allocated to add-on pods, improving cost savings and cluster efficiency.

## Overview

Enabling cost optimized add-on scaling installs the [Vertical Pod Autoscaler (VPA)add-on](vertical-pod-autoscaler), allowing supported add-ons to autoscale based on usage.

This feature also allows you to customize the resource's default CPU/ memory requests and limits in Deployments and DaemonSets, the maximum and minimum allowed CPU/ memory, and the VPA update mode within VPA custom resources. For more information, see [customize the resource configuration for AKS add-ons](customize-resource-configuration).

### Supported AKS add-ons

The following AKS managed add-ons support the cost optimized add-on scaling feature:

| Add-on | Enablement behavior | VPA custom resource name | Command to check VPA custom resource |
|---|---|---|---|
|

`coredns`

`kubectl get vpa coredns --namespace kube-system`

[Workload identity](workload-identity-deploy-cluster)`azure-wi-webhook-controller-manager`

`kubectl get vpa azure-wi-webhook-controller-manager --namespace kube-system`

[Image Integrity](image-integrity)`ratify`

`kubectl get vpa ratify --namespace gatekeeper-system`

[Network Observability (Retina)](container-network-observability-how-to)`retina-agent`

and `retina-operator`

`kubectl get vpa retina-agent --namespace kube-system`

and `kubectl get vpa retina-operator --namespace kube-system`

### Supported VPA modes for cost optimized add-on scaling

VPA currently supports the following modes for cost optimized add-on scaling:

*Off*: The VPA provides resource recommendation data but doesn't apply it to the target pod.*Initial*(default mode): The VPA automatically applies CPU and memory recommendations to the target pod when it restarts, but it doesn't initiate the restart itself.*Auto*: The VPA automatically updates CPU and memory requests for pods based on recommendations.

Note

When enabling cost optimized add-on scaling, consider the following information:

- If you delete the Deployment, DaemonSet, or VPA custom resource, the changes revert back to the AKS add-on's initial configuration.
- The cost optimized add-on scaling feature enables the
[VPA add-on](vertical-pod-autoscaler)to autoscale the supported AKS add-ons. It doesn't work with self-hosted VPA. - AKS restarts the add-on pods when enabling cost optimized add-on scaling. CoreDNS is currently the only exception to avoid potential disruptions during the restart. For more information, see
[CoreDNS autoscaling behavior](coredns-autoscale).

Warning

Make sure you have enough compute resources on the system node pool for your addons when you enable cost optimized add-on scaling. AKS recommends turning on the [cluster autoscaler](cluster-autoscaler-overview) or [node autoprovision](node-autoprovision) to ensure right-sizing of your compute resources automatically.
Monitor for pending add-on pods when using the cost-optimized add-on scaling feature. VPA might recommend resource requests that exceed available node capacity, potentially leading to unschedulable pods. You can control this behavior by [customizing min/max values](customize-resource-configuration) for requests and limits of supported addons.

## Prerequisites

- An AKS cluster running Kubernetes version 1.25 or later.
- The Azure CLI version 2.60.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). [Install the](#install-the-aks-preview-azure-cli-extension)and`aks-preview`

Azure CLI extension[register the cost optimized add-on scaling preview feature](#register-the-cost-optimized-add-on-scaling-preview-feature).

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Install the `aks-preview`

Azure CLI extension

Install the

`aks-preview`

extension using the`az extension add`

command.`az extension add --name aks-preview`

Update to the latest version of the extension using the

`az extension update`

command.`az extension update --name aks-preview`


### Register the cost optimized add-on scaling preview feature

Register the cost optimized add-on scaling preview feature using the

`az feature register`

command.`az feature register --namespace "Microsoft.ContainerService" --name "AKS-AddonAutoscalingPreview"`

It takes a few minutes for the status to show as

*Registered*.Verify the registration status using the

`az feature show`

command.`az feature show --namespace "Microsoft.ContainerService" --name "AKS-AddonAutoscalingPreview"`

When the status shows as

*Registered*, refresh the registration of the Microsoft.ContainerService provider using the`az provider register`

command.`az provider register --namespace Microsoft.ContainerService`


## Enable cost optimized add-on scaling on an AKS cluster

When enabling the add-on, the AKS cluster automatically installs the [VPA add-on](vertical-pod-autoscaler). The [AKS add-ons that support the cost optimized add-on scaling feature](#supported-aks-add-ons) have different enablement behavior.

Note

If you're using Bicep, ARM templates, or Terraform, set `VerticalPodAutoscaler`

to `"True"`

and `AddonAutoscaling`

to `"enabled"`

.

### Enable cost optimized add-on scaling on a new cluster

Enable cost optimized add-on scaling on a new AKS cluster using the

command with the`az aks create`

`--enable-optimized-addon-scaling`

flag.`az aks create --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --enable-optimized-addon-scaling`


### Enable cost optimized add-on scaling on an existing cluster

Enable cost optimized add-on scaling on an existing AKS cluster using the

command with the`az aks update`

`--enable-optimized-addon-scaling`

flag.`az aks update --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --enable-optimized-addon-scaling`


## Disable cost optimized add-on scaling on an AKS cluster

Disable cost optimized add-on scaling on an AKS cluster using the

command with the`az aks update`

`--disable-optimized-addon-scaling`

flag.`az aks update --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --disable-optimized-addon-scaling`


Note

Disabling the cost optimized add-on scaling feature doesn't disable the VPA add-on by default. To disable VPA, see [Disable VPA on an AKS cluster](use-vertical-pod-autoscaler#disable-the-vertical-pod-autoscaler-on-an-existing-cluster).

## Customize default resource configuration

With the cost optimized add-on scaling feature enabled on your cluster, you can customize the default CPU/memory settings for the add-on resources as well as the default VPA configuration for supported AKS add-ons. For more information, see [customize the resource configuration for AKS add-ons](customize-resource-configuration).

## Applying the VPA recommended values manually

Note

With *Initial* mode, the VPA applies the recommended CPU and memory requests only when a pod is created or updated. If you want the recommendations to take effect immediately, please update the pods manually. Before manually applying the recommended values, [make sure the VPA update mode is set to Initial or Auto in the VPA custom resource](customize-resource-configuration#customize-resource-update-mode).

Check the pod status and CPU/memory utilization to verify that the pod is running as expected.

The following example uses the

`kubectl get pod`

command to check a CoreDNS pod status:`kubectl get pod <coredns-pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a CoreDNS pod:

`apiVersion: v1 kind: Pod metadata: name: <coredns-pod-name> namespace: kube-system spec: ... containers: - name: coredns resources: limits: cpu: "3" memory: "500Mi" requests: cpu: "100m" memory: "70Mi"`

Get the VPA recommended value using the

`kubectl get vpa`

command.`kubectl get vpa coredns --namespace kube-system`

The following output shows an example of the VPA recommended value for a CoreDNS pod:

`NAME MODE CPU MEM PROVIDED AGE coredns Initial 11m 23574998 True 44m`

If you want to use the values recommended by VPA, manually delete the pod using the

`kubectl delete pod`

command to restart the pod with the VPA recommended values.`kubectl delete pod <coredns-pod-name> --namespace kube-system`

After the pod restarts, verify the pod status and CPU/memory updates using the

`kubectl get pod`

command.`kubectl get pod <coredns-pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a CoreDNS pod after applying the VPA recommended values:

`apiVersion: v1 kind: Pod metadata: name: <coredns-pod-name> namespace: kube-system spec: ... containers: - name: coredns resources: limits: cpu: "330m" memory: "168392842" requests: cpu: "11m" memory: "23574998"`


## Troubleshooting

With the cost optimized add-on scaling feature enabled on your cluster, you can customize the default CPU and memory settings for add-on resources, as well as modify the default VPA configuration for supported AKS managed add-ons

If your autoscaling enabled add-on pods are in a pending state, or you don't see any VPA recommendations for autoscaling enabled add-ons, follow these steps to troubleshoot the issue.

### Check AKS-managed VPA add-on status

Check if all VPA system components are running using the

`kubectl get pods`

command.`kubectl get pods --namespace kube-system | grep vpa`

The output should show three pods (vpa-admission-controller, vpa-recommender, and vpa-updater) running in the

`kube-system`

namespace, similar to the following example:`vpa-admission-controller 2/2 2 2 4m11s vpa-recommender 1/1 1 1 4m11s vpa-updater 1/1 1 1 4m11s`

For each of the three VPA pods, check the logs for any errors using the

`kubectl logs`

command. Make sure to replace`<pod-name>`

with the names of the VPA pods.`kubectl logs <pod-name> --namespace kube-system | grep -e '^E[0-9]\{4\}'`

Confirm the custom resource definition (CRD) was creating using the

`kubectl get`

command.`kubectl get customresourcedefinition | grep verticalpodautoscalers`


### Check pod status and CPU/memory utilization

Check the pod's status using the

`kubectl get pod`

command.`kubectl get pod <pod-name> --namespace=kube-system`

If the pod has a status of

`Pending`

, check the pod's status property to determine the reason the pod isn't running.`kubectl describe pod <pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a pod with a status of

`Pending`

:`apiVersion: v1 kind: Pod ... status: conditions: - lastProbeTime: null lastTransitionTime: "2023-05-03T17:05:26Z" message: '0/1 nodes are available: 1 Insufficient cpu, 1 Insufficient memory. preemption: 0/1 nodes are available: 1 Insufficient cpu, 1 Insufficient memory..' reason: Unschedulable status: "False" type: PodScheduled phase: Pending qosClass: Guaranteed`

If the output shows that the pod is

`Pending`

due to insufficient CPU or memory, consider the following actions:- Add more nodes so that pods can be scheduled in nodes with lower resource usage.
- Disable VPA for the target add-on pod by changing the update mode to
*Off*, and then[manually update the requests/limits](customize-resource-configuration)to the available resource values on the node. Be cautious when setting resource limits to extremely low values, as this may result in the pod encountering OOM kills or CPU throttling if it attempts to use more resources than are available on the node.


## Next steps

- Configure
[Cluster Autoscaler](cluster-autoscaler-overview)or[Node Autoprovisioning](node-autoprovision)in your cluster to automatically scale the cluster.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-about -->

# Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Istio](https://istio.io/latest/) addresses the challenges developers and operators face with a distributed or microservices architecture. The Istio-based service mesh add-on provides an officially supported and tested integration for Azure Kubernetes Service (AKS).

## What is a Service Mesh?

Modern applications are typically architected as distributed collections of microservices, with each collection of microservices performing some discrete business function. A service mesh is a dedicated infrastructure layer that you can add to your applications. It allows you to transparently add capabilities like observability, traffic management, and security, without adding them to your own code. The term **service mesh** describes both the type of software you use to implement this pattern, and the security or network domain that is created when you use that software.

As the deployment of distributed services, such as in a Kubernetes-based system, grows in size and complexity, it can become harder to understand and manage. You may need to implement capabilities such as discovery, load balancing, failure recovery, metrics, and monitoring. A service mesh can also address more complex operational requirements like A/B testing, canary deployments, rate limiting, access control, encryption, and end-to-end authentication.

Service-to-service communication is what makes a distributed application possible. Routing this communication, both within and across application clusters, becomes increasingly complex as the number of services grow. Istio helps reduce this complexity while easing the strain on development teams.

## What is Istio?

Istio is an open-source service mesh that layers transparently onto existing distributed applications. Istio’s powerful features provide a uniform and more efficient way to secure, connect, and monitor services. Istio enables load balancing, service-to-service authentication, and monitoring – with few or no service code changes. Its powerful control plane brings vital features, including:

- Secure service-to-service communication in a cluster with TLS (Transport Layer Security) encryption, strong identity-based authentication, and authorization.
- Automatic load balancing for HTTP, gRPC, WebSocket, and TCP traffic.
- Fine-grained control of traffic behavior with rich routing rules, retries, failovers, and fault injection.
- A pluggable policy layer and configuration API supporting access controls, rate limits, and quotas.
- Automatic metrics, logs, and traces for all traffic within a cluster, including cluster ingress and egress.

## How is the add-on different from open-source Istio?

This service mesh add-on uses and builds on top of open-source Istio. The add-on flavor provides the following extra benefits:

- Istio versions are tested and verified to be compatible with supported versions of Azure Kubernetes Service.
- Microsoft handles scaling and configuration of Istio control plane
- Microsoft adjusts scaling of AKS components like
`coredns`

when Istio is enabled. - Microsoft provides managed lifecycle (upgrades) for Istio components when triggered by user.
- Verified external and internal ingress set-up.
- Verified to work with
[Azure Monitor managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)and[Azure Managed Grafana](/en-us/azure/managed-grafana/overview). - Official Azure support provided for the add-on.

## Limitations

Istio-based service mesh add-on for AKS has the following limitations:

- The add-on doesn't work on AKS clusters that are using
[Open Service Mesh addon for AKS](open-service-mesh-about). - The add-on doesn't work on AKS clusters with self-managed installations of Istio.
- The add-on doesn't support adding pods associated with virtual nodes to be added under the mesh.
- The add-on doesn't yet support the sidecar-less Ambient mode. Microsoft is currently contributing to Ambient workstream under Istio open source. Product integration for Ambient mode is on the roadmap and is being continuously evaluated as the Ambient workstream evolves.
- The add-on doesn't yet support multi-cluster deployments.
- The add-on doesn't yet support Windows Server containers. Windows Server containers aren't yet supported in open source Istio right now. Issue tracking this feature ask can be found
[here](https://github.com/istio/istio/issues/27893). - Customization of mesh through the following custom resources is currently blocked -
`ProxyConfig, WorkloadEntry, WorkloadGroup, IstioOperator, WasmPlugin`

. - While the add-on allows the use of
`EnvoyFilter`

's, issues arising from them (for example from the Lua script or from the compression library) are outside the support scope of the Istio add-on. See the[support policy document](istio-support-policy#allowed-supported-and-blocked-customizations)for more information about the support categories for Istio add-on features and configuration options. - Gateway API for Istio ingress gateway or managing mesh traffic (GAMMA) is currently not yet supported with Istio add-on. However, Gateway API for Istio ingress traffic management is currently under active development for the add-on. While the add-on supports
[annotation and](istio-deploy-ingress#ingress-gateway-service-customizations), port or protocol configuration is currently not supported.`externalTrafficPolicy`

customization for the Istio ingress gateways - The add-on supports customization of a subset of the fields in
[MeshConfig](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/). Other customizations may be allowed but unsupported or disallowed entirely, as detailed[here](istio-meshconfig#allowed-supported-and-blocked-meshconfig-values).

## Feedback and feature ask

Feedback and feature ask for the Istio add-on can be provided by creating [issues with label 'service-mesh' on AKS GitHub repository](https://github.com/Azure/AKS/issues?q=is%3Aopen+is%3Aissue+label%3Aservice-mesh).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/reduce-latency-ppg -->

# Use proximity placement groups to reduce latency for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

When using proximity placement groups on AKS, colocation only applies to the agent nodes. Node to node and the corresponding hosted pod to pod latency is improved. The colocation doesn't affect the placement of a cluster's control plane.

When deploying your application in Azure, you can create network latency by spreading virtual machine (VM) instances across regions or availability zones, which may impact the overall performance of your application. A proximity placement group is a logical grouping used to make sure Azure compute resources are physically located close to one another. Some applications, such as gaming, engineering simulations, and high-frequency trading (HFT) require low latency and tasks that can complete quickly. For similar high-performance computing (HPC) scenarios, consider using [proximity placement groups (PPG)](/en-us/azure/virtual-machines/co-location#proximity-placement-groups) for your cluster's node pools.

## Before you begin

This article requires Azure CLI version 2.14 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Limitations

- A proximity placement group can map to only
*one*availability zone. - A node pool must use Virtual Machine Scale Sets to associate a proximity placement group.
- A node pool can associate a proximity placement group at node pool create time only.

## Node pools and proximity placement groups

The first resource you deploy with a proximity placement group attaches to a specific data center. Any extra resources you deploy with the same proximity placement group are colocated in the same data center. Once all resources using the proximity placement group are stopped (deallocated) or deleted, it's no longer attached.

- You can associate multiple node pools with a single proximity placement group.
- You can only associate a node pool with a single proximity placement group.

### Configure proximity placement groups with availability zones

Note

While proximity placement groups require a node pool to use only *one* availability zone, the [baseline Azure VM SLA of 99.9%](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_9/) is still in effect for VMs in a single zone.

Proximity placement groups are a node pool concept and associated with each individual node pool. Using a PPG resource has no impact on AKS control plane availability, which can impact how you should design your cluster with zones. To ensure a cluster is spread across multiple zones, we recommend using the following design:

- Provision a cluster with the first system pool using
*three*zones and no proximity placement group associated to ensure the system pods land in a dedicated node pool, which spreads across multiple zones. - Add extra user node pools with a unique zone and proximity placement group associated to each pool. An example is
*nodepool1*in zone one and PPG1,*nodepool2*in zone two and PPG2, and*nodepool3*in zone 3 with PPG3. This configuration ensures that, at a cluster level, nodes are spread across multiple zones and each individual node pool is colocated in the designated zone with a dedicated PPG resource.

## Create a new AKS cluster with a proximity placement group

Accelerated networking greatly improves networking performance of virtual machines. Ideally, use proximity placement groups with accelerated networking. By default, AKS uses accelerated networking on [supported virtual machine instances](/en-us/azure/virtual-network/accelerated-networking-overview?toc=/azure/virtual-machines/linux/toc.json#limitations-and-constraints), which include most Azure virtual machine with two or more vCPUs.

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location centralus`

Create a proximity placement group using the

command. Make sure to note the ID value in the output.`az ppg create`

`az ppg create --name myPPG --resource-group myResourceGroup --location centralus --type standard`

The command produces an output similar to the following example output, which includes the

*ID*value you need for upcoming CLI commands.`{ "availabilitySets": null, "colocationStatus": null, "id": "/subscriptions/yourSubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.Compute/proximityPlacementGroups/myPPG", "location": "centralus", "name": "myPPG", "proximityPlacementGroupType": "Standard", "resourceGroup": "myResourceGroup", "tags": {}, "type": "Microsoft.Compute/proximityPlacementGroups", "virtualMachineScaleSets": null, "virtualMachines": null }`

Create an AKS cluster using the

command and replace the`az aks create`

*myPPGResourceID*value with your proximity placement group resource ID from the previous step.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --ppg myPPGResourceID --generate-ssh-keys`


## Add a proximity placement group to an existing cluster

You can add a proximity placement group to an existing cluster by creating a new node pool. You can then optionally migrate existing workloads to the new node pool and delete the original node pool.

Use the same proximity placement group that you created earlier to ensure agent nodes in both node pools in your AKS cluster are physically located in the same data center.

Create a new node pool using the

command and replace the`az aks nodepool add`

*myPPGResourceID*value with your proximity placement group resource ID.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name mynodepool \ --node-count 1 \ --ppg myPPGResourceID`


## Clean up

Delete the Azure resource group along with its resources using the

command.`az group delete`

`az group delete --name myResourceGroup --yes --no-wait`


## Next steps

Learn more about [proximity placement groups](/en-us/azure/virtual-machines/co-location#proximity-placement-groups).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kubelogin-authentication -->

# Use kubelogin to authenticate users in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The kubelogin plugin in Azure is a client-go credential [plugin](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#client-go-credential-plugins) that implements Microsoft Entra authentication. The kubelogin plugin offers features that aren't available in the kubectl command-line tool. For more information, see the [kubelogin introduction](https://azure.github.io/kubelogin/index.html) and the [kubectl introduction](https://kubernetes.io/docs/reference/kubectl/introduction/).

This article provides an overview and examples of how to use kubelogin for all supported Microsoft Entra authentication methods in AKS.

## Kubelogin authentication in AKS limitations

- Groups that are created in Microsoft Entra are included only by their
**ObjectID**value, and not by their display name. The`sAMAccountName`

command is available only for groups that are synchronized from on-premises Windows Server Active Directory.

- The service principal authentication method works only with managed Microsoft Entra, and not with the earlier version Azure Active Directory.
- The service principal can be a member of a maximum of 200
[Microsoft Entra groups](/en-us/entra/identity/hybrid/connect/how-to-connect-fed-group-claims). If you have more than 200 groups, consider using[application roles](/en-us/entra/external-id/customers/how-to-use-app-roles-customers).

- The device code authentication method doesn't work when a Microsoft Entra Conditional Access policy is set on a Microsoft Entra tenant. In that scenario, use web browser interactive authentication instead.

- The Azure CLI authentication method works only with AKS managed Microsoft Entra.

## How authentication works

Note

Keep in mind the following information about kubelogin authentication for AKS clusters integrated with Microsoft Entra:

**Clusters running Kubernetes version 1.24 or later**automatically use the kubelogin format.**Clusters running Kubernetes 1.24 or earlier**require manual conversion. You can use the device code authentication method to convert the kubeconfig file to use the exec plugin format.

For most interactions with kubelogin, you use the `convert-kubeconfig`

subcommand. The subcommand uses the kubeconfig file that's specified in `--kubeconfig`

or in the `KUBECONFIG`

environment variable to convert the final kubeconfig file to exec format based on the specified authentication method.

The authentication methods that kubelogin implements are Microsoft Entra OAuth 2.0 token grant flows. In each authentication method, the token isn't cached on the file system.

## Device code authentication

Device code is the default authentication method for the `convert-kubeconfig`

subcommand. This authentication method prompts the device code for the user to sign in from a browser session.

Note

Before the kubelogin and exec plugins were introduced, the Azure authentication method in kubectl supported only the device code flow. It used an earlier version of a library that produces a token that has the `audience`

claim with an `spn:`

prefix. It isn't compatible with [AKS managed Microsoft Entra](managed-azure-ad), which uses an [on-behalf-of (OBO)](/en-us/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) flow. When you run the `convert-kubeconfig`

subcommand, kubelogin removes the `spn:`

prefix from the audience claim.

### Parameters for device code authentication

The following table outlines parameters that you can use with device code authentication:

| Parameter | Description |
|---|---|
`-l devicecode` (optional) |
Specifies the kubelogin authentication method. This parameter is optional because device code is the default method. |
`--legacy` |
Uses legacy behavior for earlier versions of Azure Active Directory clusters. If you're using the kubeconfig file in an earlier version Azure Active Directory cluster, kubelogin automatically adds the `--legacy` flag. |
`--token-cache-dir` |
Overrides the default path of the token cache directory, which is ${HOME}/.kube/cache/kubelogin. |

## Azure CLI authentication

The Azure CLI (command: `-l azurecli`

) authentication method uses the signed-in context that the Azure CLI establishes to get the access token. The token is issued in the same Microsoft Entra tenant as `az login`

. kubelogin doesn't write tokens to the token cache file because the Azure CLI already manages them.

### Parameters for Azure CLI authentication

The following table outlines parameters that you can use with Azure CLI authentication:

| Parameter | Description |
|---|---|
`-l azurecli` |
Specifies the kubelogin authentication method. |
`--azure-config-dir` |
Specifies the Azure CLI configuration directory. The default directory is ${HOME}/.azure. |

## Sign in to Azure

Sign in to Azure using the [ az login](/en-us/cli/azure/authenticate-azure-cli-interactively#interactive-login) command.

```
az login
```


## Web browser interactive authentication

The web browser interactive (command: `-l interactive`

) method of authentication automatically opens a web browser to sign in the user. After the user is authenticated, the browser redirects to the local web server using the verified credentials. This authentication method complies with Conditional Access policy.

You can use either a bearer token or a Proof-of-Possession (PoP) token with this authentication method.

### Parameters for bearer token authentication

The following table outlines parameters that you can use with bearer token authentication:

| Parameter | Description |
|---|---|
`-l interactive` |
Specifies the kubelogin authentication method. |
`--token-cache-dir` |
Overrides the default path of the token cache directory, which is ${HOME}/.kube/cache/kubelogin. |

### Parameters for PoP token authentication

The following table outlines parameters that you can use with PoP token authentication:

| Parameter | Description |
|---|---|
`-l interactive` |
Specifies the kubelogin authentication method. |
`--pop-enabled` |
Enables PoP token authentication. |
`--pop-claims` |
Specifies the PoP token claims in a key-value pair format. For example, `u=/ARM/ID/OF/CLUSTER` . |

## Service principal authentication

The service principal (command: `-l spn`

) authentication method uses a service principal to sign in the user. You can provide the credential by setting an environment variable or by using the credential in a command-line argument. The supported credentials that you can use are a password or a Personal Information Exchange (PFX) client certificate.

### Parameters for service principal authentication

The following table outlines parameters that you can use with service principal authentication:

| Parameter | Description |
|---|---|
`-l spn` |
Specifies the kubelogin authentication method. |
`--client-id` |
The application ID (client-id) of the service principal. |
`--client-secret` |
The client secret of the service principal. |

## Managed identity authentication

Use the [managed identity](/en-us/entra/identity/managed-identities-azure-resources/overview) (command: `-l msi`

) authentication method for applications that connect to resources that support Microsoft Entra authentication. Examples include accessing Azure resources like an Azure virtual machine (VM), a virtual machine scale set, or Azure Cloud Shell.

You can use the default managed identity that's assigned to the resource or a specific user-assigned managed identity.

### Parameters for managed identity authentication

The following table outlines parameters that you can use with managed identity authentication:

| Parameter | Description |
|---|---|
`-l msi` |
Specifies the kubelogin authentication method. |
`--client-id` |
The application ID (client-id) of the user-assigned managed identity. If you don't specify this parameter, the default managed identity is used. |

## Workload identity authentication

The workload identity (command: `-l workloadidentity`

) authentication method uses identity credentials that are federated with Microsoft Entra to authenticate access to AKS clusters. The method uses Microsoft Entra integrated authentication. It works by setting the following environment variables:

| Variable | Description |
|---|---|
`AZURE_CLIENT_ID` |
The Microsoft Entra application ID that is federated with the workload identity. |
`AZURE_TENANT_ID` |
The Microsoft Entra tenant ID. |
`AZURE_FEDERATED_TOKEN_FILE` |
The file that contains a signed assertion of the workload identity, like a Kubernetes projected service account (JWT) token. |
`AZURE_AUTHORITY_HOST` |
The base URL of a Microsoft Entra authority. For example, `https://login.microsoftonline.com/` . |

You can use a [workload identity](/en-us/entra/workload-id/workload-identities-overview) to access Kubernetes clusters from CI/CD systems like GitHub or ArgoCD without storing service principal credentials in the external systems. To configure OpenID Connect (OIDC) federation from GitHub, see the [OIDC federation example](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-azure).

### Parameters for workload identity authentication

The following table outlines parameters that you can use with workload identity authentication:

| Parameter | Description |
|---|---|
`-l workloadidentity` |
Specifies the kubelogin authentication method. |

## Export the kubeconfig file path

Before you run the `convert-kubeconfig`

subcommand, export the kubeconfig file path to the `KUBECONFIG`

environment variable. For example:

```
export KUBECONFIG=/path/to/kubeconfig
```


## Convert the kubeconfig file

Run the `convert-kubeconfig`

subcommand to convert the kubeconfig file to use the exec plugin for your chosen authentication method.

```
kubelogin convert-kubeconfig
```


```
kubelogin convert-kubeconfig -l azurecli
```


```
# Bearer token authentication
kubelogin convert-kubeconfig -l interactive
# Proof-of-Possession (PoP) token authentication
kubelogin convert-kubeconfig -l interactive --pop-enabled --pop-claims "u=/ARM/ID/OF/CLUSTER"
```


-
[Use environment variables](#tabpanel_1_environment-variables) -
[Use command-line arguments](#tabpanel_1_command-line-arguments) -
[Use a client certificate](#tabpanel_1_client-certificate) -
[Use a PoP token with environment variables](#tabpanel_1_pop-token-environment-variables)

Run the

`convert-kubeconfig`

subcommand to convert the kubeconfig file to use the exec plugin.`kubelogin convert-kubeconfig -l spn`

Set the environment variables for the client ID and client secret or client certificate. For example:

`export AZURE_CLIENT_ID=<service-principal-client-id> export AZURE_CLIENT_SECRET=<service-principal-client-secret>`


```
# Default managed identity authentication
kubelogin convert-kubeconfig -l msi
# Specific managed identity authentication
kubelogin convert-kubeconfig -l msi --client-id <managed-identity-client-id>
```


```
kubelogin convert-kubeconfig -l workloadidentity
```


## Remove cached tokens

Remove cached tokens using the `kubelogin remove-tokens`

command.

```
kubelogin remove-tokens
```


## Get node information

Get node information using the `kubectl get`

command.

```
kubectl get nodes
```


## How to use kubelogin with AKS

AKS uses a pair of first-party Microsoft Entra applications. These application IDs are the same in all environments.

The AKS Microsoft Entra server application ID (server-id) that the server side uses is `6dae42f8-4368-4678-94ff-3960e28e3630`

. The access token that accesses AKS clusters must be issued for this application. In most kubelogin authentication methods, you must use `--server-id`

with `kubelogin get-token`

.

The AKS Microsoft Entra client application ID (client-id) that kubelogin uses to perform public client authentication on behalf of the user is `80faf920-1908-4b52-b5ef-a8e7bedfc67a`

. The client application ID is used in device code and web browser interactive authentication methods.

## Related content

- Learn how to integrate AKS with Microsoft Entra in the
[AKS managed Microsoft Entra integration](managed-azure-ad)how-to article. - To get started with managed identities in AKS, see
[Use a managed identity in AKS](use-managed-identity). - To get started with workload identities in AKS, see
[Use a workload identity in AKS](workload-identity-overview).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-cni-powered-by-cilium -->

# Configure Azure CNI Powered by Cilium in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure CNI Powered by Cilium combines the robust control plane of Azure Container Networking Interface (CNI) with the data plane of [Cilium](https://cilium.io/) to provide high-performance networking and security.

Azure CNI Powered by Cilium provides the following benefits by making use of eBPF programs loaded into the Linux kernel and a more efficient API object structure:

- Functionality equivalent to existing Azure CNI and Azure CNI Overlay plugins
- Improved service routing
- More efficient network policy enforcement
- Better observability of cluster traffic
- Support for larger clusters (more nodes, pods, and services)

## IP Address Management (IPAM) with Azure CNI Powered by Cilium

You can deploy Azure CNI Powered by Cilium with two different methods for assigning pod IPs:

- Assign IP addresses from an overlay network (similar to Azure CNI Overlay mode)
- Assign IP addresses from a virtual network (similar to existing Azure CNI with Dynamic Pod IP Assignment)

If you aren't sure which option to select, read [Choose a network model](concepts-network-azure-cni-overlay#choose-a-network-model)

## Versions

| Kubernetes Version | Minimum Cilium Version |
|---|---|
| 1.29 (LTS) | 1.14.19 |
| 1.30 | 1.14.19 |
| 1.31 | 1.16.6 |
| 1.32 | 1.17.0 |
| 1.33 | 1.17.0 |

For more information on AKS versioning and release timelines, see [Supported Kubernetes Versions](supported-kubernetes-versions).

## Network Policy Enforcement

Cilium enforces [network policies to allow or deny traffic between pods](operator-best-practices-network#control-traffic-flow-with-network-policies). With Cilium, you don't need to install a separate network policy engine such as Azure Network Policy Manager or Calico.

## Local Redirect Policy (LRP)

LRP starts to be supported from Kubernetes v1.29 and up, Cilium v1.14 and up. For LRP to work with Advanced Container Networking Services (ACNS) - FQDN Filtering, the Cilium Network Policy egress labels need to match with node-local DNS cache pod labels.

## Limitations

Azure CNI powered by Cilium currently has the following limitations:

- Available only for Linux and not for Windows.
- Network policies can't use
`ipBlock`

to allow access to node or pod IPs. For details and recommended workarounds, see[frequently asked questions](#frequently-asked-questions). - For Cilium versions 1.16 or earlier, multiple Kubernetes services can't use the same host port with different protocols (for example, TCP or UDP) (
[Cilium issue #14287](https://github.com/cilium/cilium/issues/14287)). - Network policies aren't applied to pods using host networking (
`spec.hostNetwork: true`

) because these pods use the host identity instead of having individual identities. - Cilium Endpoint Slices are supported in Kubernetes version 1.32 and above. Cilium Endpoint Slices don't support configuration of how Cilium Endpoints are grouped. Priority namespace through
`cilium.io/ces-namespace`

isn't supported. - L7 policy isn't supported by
`CiliumClusterwideNetworkPolicy`

(CCNP). - Cilium uses Cilium identities as unique identity for provisioning endpoints, so high-churning workloads such as Spark jobs generate high count of Cilium identities. To avoid workloads hitting Cilium identity limits (65535), excluding Spark job's labels like
`!spark-app-name`

and`!spark-app-selector`

in the Cilium configmap can significantly reduce Cilium identity generation. For more details on Cilium identity exclusion rules, check[the official Cilium label documentation](https://docs.cilium.io/en/stable/operations/performance/scalability/identity-relevant-labels/#excluding-labels). - AKS Local DNS isn't compatible with Advanced Container Networking Services (ACNS) - FQDN Filtering.

## Considerations

To gain capabilities such as observability into your network traffic and security features like Fully Qualified Domain Name (FQDN) based filtering and Layer 7 based network policies on your cluster, consider enabling [Advanced Container Networking services](advanced-container-networking-services-overview) on your clusters.

## Prerequisites

- Azure CLI version 2.48.1 or later. Run
`az --version`

to see the currently installed version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you're using ARM templates or the REST API, the AKS API version must be
`2022-09-02-preview`

or later.

Previous AKS API versions (`2022-09-02preview`

to `2023-01-02preview`

) used the field [ networkProfile.ebpfDataplane=cilium](https://github.com/Azure/azure-rest-api-specs/blob/06dbe269f7d9c709cc225c92358b38c3c2b74d60/specification/containerservice/resource-manager/Microsoft.ContainerService/aks/preview/2022-09-02-preview/managedClusters.json#L6939-L6955). AKS API versions since

`2023-02-02preview`

use the field [to enable Azure CNI Powered by Cilium.](https://github.com/Azure/azure-rest-api-specs/blob/06dbe269f7d9c709cc225c92358b38c3c2b74d60/specification/containerservice/resource-manager/Microsoft.ContainerService/aks/preview/2023-02-02-preview/managedClusters.json#L7152-L7173)

`networkProfile.networkDataplane=cilium`

## Create a new AKS Cluster with Azure CNI Powered by Cilium

The following sections use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command to create a cluster and assign IP addresses.

### Option 1: Assign IP addresses from an overlay network

Use the following commands to create a cluster with an overlay network and Cilium. Replace the values for `<clusterName>`

, `<resourceGroupName>`

, and `<location>`

:

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--network-plugin azure \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16 \
--network-dataplane cilium \
--generate-ssh-keys
```


The `--network-dataplane cilium`

flag replaces the deprecated `--enable-ebpf-dataplane`

flag used in earlier versions of the aks-preview CLI extension.

### Option 2: Assign IP addresses from a virtual network

Run the following commands to create a resource group and virtual network with a subnet for nodes and a subnet for pods.

```
# Create the resource group
az group create --name <resourceGroupName> --location <location>
```


```
# Create a virtual network with a subnet for nodes and a subnet for pods
az network vnet create --resource-group <resourceGroupName> --location <location> --name <vnetName> --address-prefixes <address prefix, example: 10.0.0.0/8> -o none
az network vnet subnet create --resource-group <resourceGroupName> --vnet-name <vnetName> --name nodesubnet --address-prefixes <address prefix, example: 10.240.0.0/16> -o none
az network vnet subnet create --resource-group <resourceGroupName> --vnet-name <vnetName> --name podsubnet --address-prefixes <address prefix, example: 10.241.0.0/16> -o none
```


Create the cluster using `--network-dataplane cilium`

:

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--max-pods 250 \
--network-plugin azure \
--vnet-subnet-id /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.Network/virtualNetworks/<vnetName>/subnets/nodesubnet \
--pod-subnet-id /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.Network/virtualNetworks/<vnetName>/subnets/podsubnet \
--network-dataplane cilium \
--generate-ssh-keys
```


### Option 3: Assign IP addresses from the Node Subnet

Azure CLI version 2.69.0 or later is required. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Create a cluster using [node subnet](concepts-network-legacy-cni#azure-cni-node-subnet) with a Cilium data plane:

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--network-plugin azure \
--network-dataplane cilium \
--generate-ssh-keys
```


## Frequently asked questions

**Can I customize Cilium configuration?**No, AKS manages the Cilium configuration and it can't be modified. We recommend that customers who require more control use

[AKS BYO CNI](use-byo-cni)and install Cilium manually.**Can I use**`CiliumNetworkPolicy`

custom resources instead of Kubernetes`NetworkPolicy`

resources?L3 and L4

`CiliumNetworkPolicy`

are supported and can be used alongside Kubernetes`NetworkPolicy`

resources.Customers might use FQDN filtering and Layer 7 policies as part of the

[Advanced Container Networking Services](advanced-container-networking-services-overview)feature bundle.**Can I use**`CiliumClusterwideNetworkPolicy`

?Yes,

`CiliumClusterwideNetworkPolicy`

is supported. The following sample policy YAML shows configuring an L4 rule:`apiVersion: "cilium.io/v2" kind: CiliumClusterwideNetworkPolicy metadata: name: "l4-rule-ingress-backend-frontend" spec: endpointSelector: matchLabels: role: backend ingress: - fromEndpoints: - matchLabels: role: frontend toPorts: - ports: - port: "80" protocol: TCP`

**Which Cilium features are supported in Azure managed CNI? Which of those require Advanced Container Networking Services?**Supported Feature w/o ACNS w/ ACNS Cilium Endpoint Slices ✔️ ✔️ K8s Network Policies ✔️ ✔️ Cilium L3/L4 Network Policies ✔️ ✔️ Cilium Clusterwide Network Policy ✔️ ✔️ FQDN Filtering ❌ ✔️ L7 Network Policies (HTTP/gRPC/Kafka) ❌ ✔️ Container Network Observability (Metrics and Flow logs) ❌ ✔️ eBPF Host Routing ❌ ✔️ **Why is traffic being blocked when the**`NetworkPolicy`

has an`ipBlock`

that allows the IP address?A limitation of Azure CNI Powered by Cilium is that a

`NetworkPolicy`

`ipBlock`

can't select pod or node IPs.For example, this

`NetworkPolicy`

has an`ipBlock`

that allows all egress to`0.0.0.0/0`

:`apiVersion: networking.k8s.io/v1 kind: NetworkPolicy metadata: name: example-ipblock spec: podSelector: {} policyTypes: - Egress egress: - to: - ipBlock: cidr: 0.0.0.0/0 # This will still block pod and node IPs.`

However, when this

`NetworkPolicy`

is applied, Cilium blocks egress to pod and node IPs even though the IPs are within the`ipBlock`

CIDR.As a workaround, you can add

`namespaceSelector`

and`podSelector`

to select pods. This example selects all pods in all namespaces:`apiVersion: networking.k8s.io/v1 kind: NetworkPolicy metadata: name: example-ipblock spec: podSelector: {} policyTypes: - Egress egress: - to: - ipBlock: cidr: 0.0.0.0/0 - namespaceSelector: {} - podSelector: {}`

It isn't currently possible to specify a

`NetworkPolicy`

with an`ipBlock`

to allow traffic to node IPs.**Does AKS configure CPU or memory limits on the Cilium**`daemonset`

?No, AKS doesn't configure CPU or memory limits on the Cilium

`daemonset`

because Cilium is a critical system component for pod networking and network policy enforcement.**Does Azure CNI powered by Cilium use kube-proxy?**No, AKS clusters created with network data plane as Cilium don't use

`kube-proxy`

. If the AKS clusters are on[Azure CNI Overlay](azure-cni-overlay)or[Azure CNI with dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)and are upgraded to AKS clusters running Azure CNI powered by Cilium, new nodes workloads are created without`kube-proxy`

. Older workloads are also migrated to run without`kube-proxy`

as a part of this upgrade process.

## Dual-stack networking with Azure CNI Powered by Cilium

You can deploy your dual-stack AKS clusters with Azure CNI Powered by Cilium. This feature also allows you to control your IPv6 traffic with the Cilium Network Policy engine.

You must have Kubernetes version 1.29 or greater.

### Set up Overlay clusters with Azure CNI Powered by Cilium

Create a cluster with Azure CNI Overlay using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command. Make sure to use the argument

`--network-dataplane cilium`

to specify the Cilium data plane.```
clusterName="myOverlayCluster"
resourceGroup="myResourceGroup"
location="westcentralus"
az aks create \
--name $clusterName \
--resource-group $resourceGroup \
--location $location \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--ip-families ipv4,ipv6 \
--generate-ssh-keys
```


## Next steps

Learn more about networking in AKS in the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/customize-resource-configuration -->

# Customize the resource configuration for managed add-ons

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of how to customize the resource configuration for Azure Kubernetes Service (AKS) managed add-ons with [cost optimized add-on scaling (Preview)](optimized-addon-scaling).

## Overview

Enabling the cost optimized add-on scaling feature in your AKS cluster installs the Vertical Pod Autoscaler (VPA) add-on and VPA custom resources for AKS managed add-ons that support this capability. This feature also allows you to manually customize the resource CPU and memory requests and limits in Deployments and DaemonSets. You can also customize the maximum and minimum allowed CPU and memory and the VPA update mode within VPA custom resources.

## Prerequisites

- Review the
[supported AKS managed add-ons](optimized-addon-scaling#supported-aks-add-ons)and[limitations](optimized-addon-scaling)for this feature. - You need an AKS cluster enabled with the cost optimized add-on scaling feature. If you don't have one, see
[Enable cost optimized add-on scaling on your AKS cluster (Preview)](optimized-addon-scaling).

## Customize resource annotations

| Annotation | Description | Values |
|---|---|---|
`kubernetes.azure.com/override-requests-limits` |
Supports the capability to customize the container resource CPU/memory requests/limits in a Deployment or DaemonSet if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. | "enabled" or "disabled" |
`kubernetes.azure.com/override-min-max` |
Supports the capability to customize the container policy maximum/minimum allowed CPU/memory value in VPA custom resource if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. | "enabled" or "disabled" |
`kubernetes.azure.com/override-update-mode` |
Supports the capability to customize the update policy `updateMode` value in a VPA custom resource if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. |
"enabled" or "disabled" |

## Customize resource CPU/memory requests/limits

After setting the `kubernetes.azure.com/override-requests-limits`

annotation to "enabled" in a Deployment or DaemonSet, you can customize the resource CPU/memory requests and limits. The following example shows how to customize the resource CPU/memory requests and limits in a Deployment:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-requests-limits: "enabled"
spec:
...
containers:
- name: coredns
resources:
limits:
# update cpu limits value won't be reconciled back
cpu: "3"
# update memory limits value won't be reconciled back
memory: "500Mi"
requests:
# update cpu requests value won't be reconciled back
cpu: "100m"
# update memory requests value won't be reconciled back
memory: "70Mi"
```


## Customize resource maximum/minimum allowed CPU/memory

After setting the `kubernetes.azure.com/override-min-max`

annotation to "enabled" in a VPA custom resource, you can customize the maximum and minimum allowed CPU and memory values in a VPA custom resource. The following example shows how to customize the maximum and minimum allowed CPU and memory values in a VPA custom resource:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-min-max: "enabled"
spec:
resourcePolicy:
containerPolicies:
- containerName: coredns
maxAllowed:
# update maxAllowed cpu value won't be reconciled back
cpu: 3
# update maxAllowed memory value won't be reconciled back
memory: 500Mi
minAllowed:
# update minAllowed cpu value won't be reconciled back
cpu: 10m
# update minAllowed memory value won't be reconciled back
memory: 10Mi
...
```


## Customize resource update mode

After setting the `kubernetes.azure.com/override-update-mode`

annotation to "enabled" in a VPA custom resource, you can customize the update policy `updateMode`

value in a VPA custom resource to "Off" or "Initial" (default). The following example shows how to customize the update policy `updateMode`

value to "Initial" in a VPA custom resource:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-update-mode: "enabled"
spec:
...
updatePolicy:
# update updateMode won't be reconciled back
updateMode: "Initial"
```


## Disable VPA on a specific AKS managed add-on

To disable VPA on a specific AKS managed add-on, you need to update the VPA custom resource YAML file to set the `kubernetes.azure.com/override-update-mode`

annotation to `"enabled"`

and the `updateMode`

to `"Off"`

. With *Off* mode, the VPA only provides CPU and memory recommendations and doesn't apply the changes to the pod.

The following example shows how to disable VPA on the CoreDNS add-on:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# Set value to "enabled"
kubernetes.azure.com/override-update-mode: "enabled"
spec:
...
updatePolicy:
# Set value to "Off"
updateMode: "Off"
```


## Troubleshooting

- Make sure the AKS managed add-on supports the cost optimized add-on scaling feature. For more information, see
[Supported AKS managed add-ons](optimized-addon-scaling#supported-aks-add-ons). - Verify that the
`kubernetes.azure.com/override-requests-limits`

annotation in the Deployment or DaemonSet is set to "enabled". - Verify that the
`kubernetes.azure.com/override-min-max`

annotation in the VPA custom resource is set to "enabled". - Verify that the
`kubernetes.azure.com/override-update-mode`

annotation in the VPA custom resource is set to "enabled".

## Next steps

To further configure cluster resource utilization and free up CPU/memory for AKS managed add-on pods, see [Vertical pod autoscaling in AKS](vertical-pod-autoscaler).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-application -->

# Tutorial - Deploy an application to Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes provides a distributed platform for containerized applications. You build and deploy your own applications and services into a Kubernetes cluster and let the cluster manage the availability and connectivity.

In this tutorial, you deploy a sample application into a Kubernetes cluster. You learn how to:

- Update a Kubernetes manifest file.
- Run an application in Kubernetes.
- Test the application.

Tip

With AKS, you can use the following approaches for configuration management:

**GitOps**: Enables declarations of your cluster's state to automatically apply to the cluster. To learn how to use GitOps to deploy an application with an AKS cluster, see the[prerequisites for Azure Kubernetes Service clusters](/en-us/azure/azure-arc/kubernetes/tutorial-use-gitops-flux2?toc=/azure/aks/toc.json#for-azure-kubernetes-service-clusters)in the[GitOps with Flux v2](/en-us/azure/azure-arc/kubernetes/tutorial-use-gitops-flux2?toc=/azure/aks/toc.json)tutorial.**DevOps**: Enables you to build, test, and deploy with continuous integration (CI) and continuous delivery (CD). To see examples of how to use DevOps to deploy an application with an AKS cluster, see[Build and deploy to AKS with Azure Pipelines](devops-pipeline)or[GitHub Actions for deploying to Kubernetes](kubernetes-action).

## Before you begin

In previous tutorials, you packaged an application into a container image, uploaded the image to Azure Container Registry, and created a Kubernetes cluster. To complete this tutorial, you need the precreated `aks-store-quickstart.yaml`

Kubernetes manifest file. This file was downloaded in the application source code from [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.0.53 or later. Check your version with `az --version`

. To install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Update the manifest file

In these tutorials, your Azure Container Registry (ACR) instance stores the container images for the sample application. To deploy the application, you must update the image names in the Kubernetes manifest file to include your ACR login server name.

Get your login server address using the

command and query for your login server.`az acr list`

`az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table`

Make sure you're in the cloned

*aks-store-demo*directory, and then open the`aks-store-quickstart.yaml`

manifest file with a text editor.Update the

`image`

property for the containers by replacing*ghcr.io/azure-samples*with your ACR login server name.`containers: ... - name: order-service image: <acrName>.azurecr.io/aks-store-demo/order-service:latest ... - name: product-service image: <acrName>.azurecr.io/aks-store-demo/product-service:latest ... - name: store-front image: <acrName>.azurecr.io/aks-store-demo/store-front:latest ...`

Save and close the file.


## Run the application

Deploy the application using the

command, which parses the manifest file and creates the defined Kubernetes objects.`kubectl apply`

`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the resources successfully created in the AKS cluster:

`statefulset.apps/rabbitmq created configmap/rabbitmq-enabled-plugins created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`

Check the deployment is successful by viewing the pods with the

`kubectl get pods`

command.`kubectl get pods`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

### Command Line

Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`kubectl get service store-front --watch`

Initially, the

`EXTERNAL-IP`

for the`store-front`

service shows as`<pending>`

:`store-front LoadBalancer 10.0.34.242 <pending> 80:30676/TCP 5s`

When the

`EXTERNAL-IP`

address changes from`<pending>`

to a public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`store-front LoadBalancer 10.0.34.242 52.179.23.131 80:30676/TCP 67s`

View the application in action by opening a web browser and navigating to the external IP address of your service:

`http://<external-ip>`

.

If the application doesn't load, it might be an authorization problem with your image registry. To view the status of your containers, use the `kubectl get pods`

command. If you can't pull the container images, see [Authenticate with Azure Container Registry from Azure Kubernetes Service](cluster-container-registry-integration).

### Azure portal

Navigate to the Azure portal to find your deployment information.

Navigate to your AKS cluster resource.

From the service menu, under

**Kubernetes Resources**, select**Services and ingresses**.Copy the External IP shown in the column for the

`store-front`

service.Paste the IP into your browser to visit your store page.


## Clean up resources

Since you validated the application's functionality, you can now remove the cluster from the application. We will deploy the application again in the next tutorial.

Stop and remove the container instances and resources using the

`kubectl delete`

command.`kubectl delete -f aks-store-quickstart.yaml`

Check that all the application pods have been removed using the

`kubectl get pods`

command.`kubectl get pods`


## Next steps

In this tutorial, you deployed a sample Azure application to a Kubernetes cluster in AKS. You learned how to:

- Update a Kubernetes manifest file.
- Run an application in Kubernetes.
- Test the application.

In the next tutorial, you learn how to use PaaS services for stateful workloads in Kubernetes.
