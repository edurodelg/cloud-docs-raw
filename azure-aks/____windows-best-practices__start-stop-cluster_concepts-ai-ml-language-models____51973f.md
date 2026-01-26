---
merged_at: 2026-01-26T20:54:26.172818
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

---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _faq__auto-upgrade-node-os-image___node-pool-unique-subnet_concepts-network-serv_0c9dce.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: faq.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/faq -->

# AKS frequently asked questions

This article provides answers to some of the most common questions about Azure Kubernetes Service (AKS).

## Support

### Does AKS offer a service-level agreement?

AKS provides service-level agreement (SLA) guarantees in the [Standard pricing tier with the Uptime SLA feature](free-standard-pricing-tiers).

### What is platform support, and what does it include?

Platform support is a reduced support plan for unsupported n-3 version clusters. Platform support includes only Azure infrastructure support.

For more information, see the [platform support policy](supported-kubernetes-versions).

### Does AKS automatically upgrade my unsupported clusters?

Yes, AKS initiates auto-upgrades for unsupported clusters. When a cluster in an n-3 version (where *n* is the latest supported AKS minor version that's generally available) is about to drop to n-4, AKS automatically upgrades the cluster to n-2 to remain in an AKS support policy.

For more information, see [Supported Kubernetes versions](supported-kubernetes-versions), [Planned maintenance windows](planned-maintenance), and [Automatic upgrades](auto-upgrade-cluster).

### Can I apply Azure reservation discounts to my AKS agent nodes?

AKS agent nodes are billed as standard Azure virtual machines (VMs). If you purchased [Azure reservations](/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations) for the VM size that you're using in AKS, those discounts are automatically applied.

## Operations

### Can I run Windows Server containers on AKS?

Yes, AKS supports Windows Server containers. For more information, see the [Windows Server on AKS FAQ](windows-faq).

### What Linux operating systems (OS) are supported on AKS?

AKS supports four main Linux operating systems, including Ubuntu Linux, [Azure Linux](use-azure-linux), [Azure Linux OS Guard](use-azure-linux-os-guard), and [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks). When specifying `--os-type Linux`

during node pool creation or cluster creation, the default OS is Ubuntu Linux.

### What operating systems (OS) versions are supported on AKS?

When using `--os-sku Ubuntu`

, AKS defaults to Ubuntu 22.04 in Kubernetes versions 1.25-1.34. AKS defaults to Ubuntu 24.04 in Kubernetes versions 1.35+.
When using `--os-sku AzureLinux`

, AKS defaults to Azure Linux 3.0 in Kubernetes versions 1.32+.
In some scenarios, like FIPS-enabled node pools, the default OS version might differ. See [node images](node-images) for more information.

### Can I move or migrate my cluster between Azure tenants?

No. Moving your AKS cluster between tenants is currently unsupported.

### Can I move or migrate my cluster between subscriptions?

No. Moving your AKS cluster between subscriptions is currently unsupported.

### Can I move my AKS cluster or AKS infrastructure resources to other resource groups or rename them?

No. Moving or renaming your AKS cluster and its associated resources isn't supported.

### Can I restore my cluster after I delete it?

No. You can't restore your cluster after you delete it. When you delete your cluster, the node resource group and all its resources are also deleted.

If you want to keep any of your resources, move them to another resource group before you delete your cluster. If you want to protect against accidental deletes, you can lock the AKS managed resource group that's hosting your cluster resources by using [Node resource group lockdown](node-resource-group-lockdown).

### Can I scale my AKS cluster to zero?

You can completely [stop a running AKS cluster](start-stop-cluster) or [scale or autoscale all or specific User node pools](scale-cluster#scale-user-node-pools-to-0) to zero.

You can't directly scale [system node pools](use-system-pools) to zero.

### Can I use the virtual machine scale set APIs to scale manually?

No. Scale operations that use the virtual machine scale set APIs aren't supported. You can use the AKS APIs (`az aks scale`

).

### Can I use virtual machine scale sets to manually scale to zero nodes?

No. Scale operations that use the virtual machine scale set APIs aren't supported. You can use the AKS API to scale nonsystem node pools to zero or [stop your cluster](start-stop-cluster) instead.

### Can I stop or deallocate all my VMs?

No. This configuration isn't supported. [Stop your cluster](start-stop-cluster) instead.

### Why are two resource groups created with AKS?

AKS builds upon many Azure infrastructure resources, including virtual machine scale sets, virtual networks, and managed disks. These integrations enable you to apply many of the core capabilities of the Azure platform within the managed Kubernetes environment provided by AKS. For example, you can use most Azure VM types directly with AKS, and you can use Azure Reservations to receive discounts on those resources automatically.

To enable this architecture, each AKS deployment spans two resource groups:

- You create the first resource group. This group contains only the Kubernetes service resource. The AKS resource provider automatically creates the second resource group during deployment. An example of the second resource group is
*MC_myResourceGroup_myAKSCluster_eastus*. For information on how to specify the name of this second resource group, see the next section. - The second resource group, known as the
*node resource group*, contains all of the infrastructure resources associated with the cluster. These resources include the Kubernetes node VMs, virtual networking, and storage. By default, the node resource group has a name like*MC_myResourceGroup_myAKSCluster_eastus*. AKS automatically deletes the node resource group whenever you delete the cluster. Use this resource group only for resources that share the cluster's lifecycle.

Note

Modifying any resource under the node resource group in the AKS cluster is an unsupported action and will cause cluster operation failures. You can prevent changes from being made to the node resource group. [Block users from modifying resources](node-resource-group-lockdown) that the AKS cluster manages.

### Can I provide my own name for the AKS node resource group?

By default, AKS names the node resource group *MC_resourcegroupname_clustername_location*, but you can provide your own name.

To specify your own resource group name, install the [aks-preview](/en-us/cli/azure/aks) Azure CLI extension version *0.3.2* or later. When you create an AKS cluster by using the `az aks create`

command, use the `--node-resource-group`

parameter and specify a name for the resource group. If you use an [Azure Resource Manager template](/en-us/azure/templates/microsoft.containerservice/2022-09-01/managedclusters) to deploy an AKS cluster, you can define the resource group name by using the `nodeResourceGroup`

property.

- The Azure resource provider automatically creates the secondary resource group.
- You can specify a custom resource group name only when you create the cluster.

As you work with the node resource group, you can't:

- Specify an existing resource group for the node resource group.
- Specify a different subscription for the node resource group.
- Change the node resource group name after you create the cluster.
- Specify names for the managed resources within the node resource group.
- Modify or delete Azure-created tags of managed resources within the node resource group.

### Can I modify tags and other properties of the AKS resources in the node resource group?

You might get unexpected scaling and upgrading errors if you modify or delete Azure-created tags and other resource properties in the node resource group. AKS allows you to create and modify custom tags created by end users, and you can add those tags when you [create a node pool](manage-node-pools#specify-a-taint-label-or-tag-for-a-node-pool). You might want to create or modify custom tags, for example, to assign a business unit or cost center. Another option is to apply policies and modify tags through the AKS resource itself—specifically via the cluster and node pools..

Azure-created tags are created for their respective Azure services, and you should always allow them. For AKS, there are the `aks-managed`

and `k8s-azure`

tags. Modifying any *Azure-created tags* on resources under the node resource group in the AKS cluster is an unsupported action, which breaks the service-level objective (SLO).

Note

In the past, the tag name `Owner`

was reserved for AKS to manage the public IP that's assigned on the front-end IP of the load balancer. Now, services use the `aks-managed`

prefix. For legacy resources, don't use Azure policies to apply the `Owner`

tag name. Otherwise, all resources on your AKS cluster deployment and update operations will break. This restriction doesn't apply to newly created resources.

### Why do I see aks-managed prefixed Helm releases on my cluster, and why does their revision count keep increasing?

AKS uses Helm to deliver components to your cluster. You can safely ignore `aks-managed`

prefixed Helm releases. Continuously increasing revisions on these Helm releases are expected and safe.

## Quotas, limits, and region availability

### Which Azure regions currently provide AKS?

For a complete list of available regions, see [AKS regions and availability](https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service).

### Can I spread an AKS cluster across regions?

No. AKS clusters are regional resources and can't span regions. For guidance on how to create an architecture that includes multiple regions, see [best practices for business continuity and disaster recovery](operator-best-practices-multi-region#plan-for-multiregion-deployment).

### Can I spread an AKS cluster across availability zones?

Yes, you can deploy an AKS cluster across one or more [availability zones](availability-zones) in [regions that support them](/en-us/azure/reliability/availability-zones-region-support).

### Can I have different VM sizes in a single cluster?

Yes, you can use different VM sizes in your AKS cluster by creating [multiple node pools](create-node-pools).

### What's the size limit on a container image in AKS?

AKS doesn't set a limit on the container image size. But the larger the image, the higher the memory demand. A larger size could potentially exceed resource limits or the overall available memory of worker nodes. By default, memory for VM size Standard_DS2_v2 for an AKS cluster is set to 7 GiB.

When a container image is excessively large, as in the terabyte (TB) range, the kubelet might not be able to pull it from your container registry to a node because of the lack of disk space.

For Windows Server nodes, Windows Update doesn't automatically run and apply the latest updates. You should perform an upgrade on the cluster and the Windows Server node pools in your AKS cluster. Follow a regular schedule based on the Windows Update release cycle and your own validation process. This upgrade process creates nodes that run the latest Windows Server image and patches, and then removes the older nodes. For more information on this process, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

### Are AKS images required to run as root?

The following images have functional requirements to run as root, and exceptions must be filed for any policies:

*mcr.microsoft.com/oss/kubernetes/coredns**mcr.microsoft.com/azuremonitor/containerinsights/ciprod**mcr.microsoft.com/oss/calico/node**mcr.microsoft.com/oss/kubernetes-csi/azuredisk-csi*

## Security, access, and identity

### Can I limit who has access to the Kubernetes API server?

Yes, there are two options for limiting access to the API server:

- Use
[API server authorized IP ranges](api-server-authorized-ip-ranges)if you want to maintain a public endpoint for the API server but restrict access to a set of trusted IP ranges. - Use a
[private cluster](private-clusters)if you want to limit the API server to be accessible*only*from within your virtual network.

### Are security updates applied to AKS agent nodes?

AKS patches CVEs that have a *vendor fix* every week. CVEs without a fix are waiting on a vendor fix before they can be remediated. The AKS images are automatically updated within 30 days. We recommend that you apply an updated node image on a regular cadence to ensure that the latest patched images and OS patches are all applied and current. You can do this task:

- Manually, through the Azure portal or the Azure CLI.
- By upgrading your AKS cluster. The cluster upgrades
[cordon and drain nodes](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)automatically. Then it brings a new node online with the latest Ubuntu image and a new patch version or a minor Kubernetes version. For more information, see[Upgrade an AKS cluster](upgrade-cluster). - By using a
[node image upgrade](node-image-upgrade).

### Are there security threats that target AKS that I should be aware of?

Microsoft provides guidance for other actions that you can take to secure your workloads through services like [Microsoft Defender for Containers](/en-us/azure/defender-for-cloud/defender-for-containers-introduction?tabs=defender-for-container-arch-aks). For information on a security threat related to AKS and Kubernetes, see [New large-scale campaign targets Kubeflow](https://techcommunity.microsoft.com/t5/azure-security-center/new-large-scale-campaign-targets-kubeflow/ba-p/2425750) (June 8, 2021).

### Does AKS store any customer data outside the cluster's region?

No. All data is stored in the cluster's region.

### How can I avoid permission ownership setting slow issues when the volume has numerous files?

Traditionally, if your pod is running as a nonroot user (which it should), you must specify an `fsGroup`

parameter inside the pod's security context so that the volume is readable and writable by the pod. For more information on this requirement, see [Configure a security context for a pod or container](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/).

A side effect of setting `fsGroup`

is that each time a volume is mounted, Kubernetes must use the `chown()`

and `chmod()`

commands recursively for all the files and directories inside the volume (with a few exceptions). This scenario happens even if group ownership of the volume already matches the requested `fsGroup`

parameter. This configuration might be expensive for larger volumes with lots of small files, which can cause pod startup to take a long time. This scenario was a known problem before v1.20. The workaround is to set the pod to run as root:

```
apiVersion: v1
kind: Pod
metadata:
name: security-context-demo
spec:
securityContext:
runAsUser: 0
fsGroup: 0
```


The issue was resolved with Kubernetes version 1.20. For more information, see [Kubernetes 1.20: Granular control of volume permission changes](https://kubernetes.io/blog/2020/12/14/kubernetes-release-1.20-fsgroupchangepolicy-fsgrouppolicy/).

## Networking

### How does the managed control plane communicate with my nodes?

AKS uses a secure tunnel communication to allow the `api-server`

and individual node kubelets to communicate, even on separate virtual networks. The tunnel is secured through mutual Transport Layer Security encryption. The current main tunnel that AKS uses is [Konnectivity, previously known as apiserver-network-proxy](https://kubernetes.io/docs/tasks/extend-kubernetes/setup-konnectivity/). Verify that all network rules follow the [Azure required network rules and fully qualified domain names (FQDNs)](limit-egress-traffic).

### Can my pods use the API server FQDN instead of the cluster IP?

Yes, you can add the annotation `kubernetes.azure.com/set-kube-service-host-fqdn`

to pods to set the `KUBERNETES_SERVICE_HOST`

variable to the domain name of the API server instead of the in-cluster service IP. This modification is useful in cases where your cluster egress is done via a layer 7 firewall. An example is when you use Azure Firewall with application rules.

### Can I configure NSGs with AKS?

AKS doesn't apply network security groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. AKS modifies only the network interface NSG settings. If you're using Container Network Interface (CNI), you also must ensure that the security rules in the NSGs allow traffic between the node and pod classless interdomain routing (CIDR) ranges. If you're using kubenet, you must also ensure that the security rules in the NSGs allow traffic between the node and pod CIDR. For more information, see [Network security groups](concepts-network#network-security-groups).

### How does time synchronization work in AKS?

AKS nodes run the chrony service, which pulls time from the local host. Containers that run on pods get the time from the AKS nodes. Applications that open inside a container use time from the container of the pod.

## Add-ons, extensions, and integrations

### Can I use custom VM extensions?

No. AKS is a managed service. Manipulation of the infrastructure as a service (IaaS) resources isn't supported. To install custom components, use the Kubernetes APIs and mechanisms. For example, use DaemonSets to install any required components.

### What Kubernetes admission controllers does AKS support? Can admission controllers be added or removed?

AKS supports the following [admission controllers](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/):

`NamespaceLifecycle`

`LimitRanger`

`ServiceAccount`

`DefaultIngressClass`

`DefaultStorageClass`

`DefaultTolerationSeconds`

`MutatingAdmissionWebhook`

`ValidatingAdmissionWebhook`

`ResourceQuota`

`PodNodeSelector`

`PodTolerationRestriction`

`ExtendedResourceToleration`


Currently, you can't modify the list of admission controllers in AKS.

### Can I use admission controller webhooks on AKS?

Yes, you can use admission controller webhooks on AKS. We recommend that you exclude internal AKS namespaces, which are marked with the `control-plane`

label. For example:

```
namespaceSelector:
matchExpressions:
- key: control-plane
operator: DoesNotExist
```


AKS firewalls the API server egress so that your admission controller webhooks need to be accessible from within the cluster.

### Can admission controller webhooks affect kube-system and internal AKS namespaces?

To protect the stability of the system and prevent custom admission controllers from affecting internal services in the `kube-system`

namespace, AKS has an admissions enforcer, which automatically excludes `kube-system`

and AKS internal namespaces. This service ensures that the custom admission controllers don't affect the services that run in `kube-system`

.

If you have a critical use case for deploying something on `kube-system`

(not recommended) in support of your custom admission webhook, you can add the following label or annotation so that the admissions enforcer ignores it:

- Label:
`"admissions.enforcer/disabled": "true"`

- Annotation:
`"admissions.enforcer/disabled": true`


### Is Azure Key Vault integrated with AKS?

[Azure Key Vault provider for Secrets Store CSI Driver](csi-secrets-store-driver) provides native integration of Azure Key Vault into AKS.

### Can I use FIPS cryptographic libraries with deployments on AKS?

Nodes that are enabled with Federal Information Processing Standards (FIPS) are now supported on Linux-based node pools. For more information, see [Add a FIPS-enabled node pool](enable-fips-nodes).

### How are AKS add-ons updated?

Any patch, including a security patch, is automatically applied to the AKS cluster. Anything bigger than a patch, like major or minor version changes (which can have breaking changes to your deployed objects), are updated when you update your cluster if a new release is available. For information on when a new release is available, see [AKS release notes](https://github.com/Azure/AKS/releases).

### What is the purpose of the AKS Linux extension that I see installed on my Linux virtual machine scale sets instances?

The AKS Linux extension is an Azure VM extension that installs and configures monitoring tools on Kubernetes worker nodes. The extension is installed on all new and existing Linux nodes. It configures the following monitoring tools:

[Node-exporter](https://github.com/prometheus/node_exporter): Collects hardware telemetry from the VM and makes it available by using a metrics endpoint. Then, a monitoring tool, such as Prometheus, can scrap these metrics.[Node-problem-detector](https://github.com/kubernetes/node-problem-detector): Aims to make various node problems visible to upstream layers in the cluster management stack. It's a systemd unit that runs on each node, detects node problems, and reports them to the cluster's API server by using`Events`

and`NodeConditions`

.[ig](https://go.microsoft.com/fwlink/p/?linkid=2260320): Is an eBPF-powered open-source framework for debugging and observing Linux and Kubernetes systems. It provides a set of tools (or gadgets) that gather relevant information that users can use to identify the cause of performance issues, crashes, or other anomalies. Notably, its independence from Kubernetes enables users to employ it also for debugging control plane issues.

These tools help provide observability around many node health-related problems, such as:

**Infrastructure daemon issues:**NTP service down**Hardware issues:**Bad CPU, memory, or disk**Kernel issues:**Kernel deadlock, corrupted file system**Container runtime issues:**Unresponsive runtime daemon

The extension *doesn't require extra outbound access* to any URLs, IP addresses, or ports beyond the [documented AKS egress requirements](limit-egress-traffic). It doesn't require any special permissions granted in Azure. It uses `kubeconfig`

to connect to the API server to send the monitoring data that's collected.

## Troubleshoot cluster issues

### Why is it taking so long to delete my cluster?

Most clusters are deleted upon user request. In some cases, especially cases where you bring your own resource group or perform cross-resource group tasks, deletion can take more time or even fail. If you have an issue with deletions, double-check that you don't have locks on the resource group. Also make sure that any resources outside the resource group are disassociated from the resource group.

### Why is it taking so long to create or update my cluster?

If you have issues with creating and updating clusters, make sure that you don't have any assigned policies or service constraints that might block your AKS cluster from managing resources like VMs, load balancers, or tags.

### If I have pods or deployments in NodeLost or Unknown states, can I still upgrade my cluster?

You can, but we don't recommend it. Perform updates when the state of the cluster is known and healthy.

### If I have a cluster with one or more nodes in an Unhealthy state, or if it's shut down, can I perform an upgrade?

No. Delete or remove any nodes that are in a failed state or otherwise from the cluster before you upgrade.

### I tried to delete my cluster, but I see the error "[Errno 11001] getaddrinfo failed."

Most commonly, this error arises if you have one or more NSGs in use that are still associated with the cluster. Remove them and attempt to delete the cluster again.

### I ran an upgrade, but now my pods are in crash loops and readiness probes fail.

Confirm that your service principal isn't expired. For more information, see [AKS service principal](kubernetes-service-principal) and [AKS update credentials](update-credentials).

### My cluster was working, but suddenly I can't provision load balancers or mount persistent volume claims.

Confirm that your service principal isn't expired. For more information, see [AKS service principal](kubernetes-service-principal) and [AKS update credentials](update-credentials).

## Retirements and deprecations

### Which Linux OS versions are deprecated on AKS?

Ubuntu 16.04 and Ubuntu 18.04 are no longer supported on AKS.
Starting on 17 March 2027, AKS will no longer support Ubuntu 20.04. For more information on this retirement, see [Retirement: Ubuntu 20.04 node pools on AKS](https://github.com/Azure/AKS/issues/4874).

### Which Windows OS versions are deprecated on AKS?

Starting on 1 March 2026, AKS will no longer support Windows Server 2019 node pools. Kubernetes versions 1.33+ can't use Windows Server 2019. For more information on this retirement, see [Retirement: Windows Server 2019 node pools on AKS](https://github.com/Azure/AKS/issues/4091).
Starting on 15 March 2027, AKS will no longer support Windows Server 2022 node pools. Kubernetes versions 1.36+ can't use Windows Server 2022. For more information on this retirement, see [Retirement: Windows Server 2022 node pools on AKS](https://github.com/Azure/AKS/issues/4168).


---

<!-- DOCUMENTO FUSIONADO: _auto-upgrade-node-os-image___node-pool-unique-subnet_concepts-network-services__15a883.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: auto-upgrade-node-os-image.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-node-os-image -->

# Autoupgrade node OS images

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS provides multiple autoupgrade channels dedicated to timely node-level OS security updates. This channel is different from cluster-level Kubernetes version upgrades and supersedes it.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Interactions between node OS autoupgrade and cluster autoupgrade

Node-level OS security updates are released at a faster rate than Kubernetes patch or minor version updates. The node OS autoupgrade channel grants you flexibility and enables a customized strategy for node-level OS security updates. Then, you can choose a separate plan for cluster-level Kubernetes version [autoupgrades](auto-upgrade-cluster).
It's best to use both cluster-level [autoupgrades](auto-upgrade-cluster) and the node OS autoupgrade channel together. Scheduling can be fine-tuned by applying two separate sets of [maintenance windows](planned-maintenance) - `aksManagedAutoUpgradeSchedule`

for the cluster [autoupgrade](auto-upgrade-cluster) channel and `aksManagedNodeOSUpgradeSchedule`

for the node OS autoupgrade channel.

## Channels for node OS image upgrades

The selected channel determines the timing of upgrades. When making changes to node OS auto-upgrade channels, allow up to 24 hours for the changes to take effect.

Note

- Node OS image auto-upgrade don't affect the cluster's Kubernetes version.
- Starting with API version 2023-06-01, the default for any new AKS cluster is
`NodeImage`

.

### Node OS channel changes that cause a reimage

The following node os channel transitions will trigger reimage on the nodes:

| From | To |
|---|---|
| Unmanaged | None |
| Unspecified | Unmanaged |
| SecurityPatch | Unmanaged |
| NodeImage | Unmanaged |
| None | Unmanaged |

### Available node OS upgrade channels

The following upgrade channels are available. You're allowed to choose one of these options:

| Channel | Description | OS-specific behavior |
|---|---|---|
`None` |
Your nodes don't have security updates applied automatically. This means you're solely responsible for your security updates. | N/A |
`Unmanaged` |
The OS built-in patching infrastructure automatically applies OS updates. Newly allocated machines are initially unpatched. The OS's infrastructure patches them at some point. | Ubuntu and Azure Linux (CPU node pools) apply security patches through unattended upgrade/dnf-automatic roughly once per day around 06:00 UTC. Windows doesn't automatically apply security patches, so this option behaves equivalently to `None` . You need to manage the reboot process using a tool like
`Unmanaged` . |
`SecurityPatch` |
OS security patches, which are AKS-tested, fully managed, and applied with safe deployment practices. AKS regularly updates the node's virtual hard disk (VHD) with patches from the image maintainer labeled "security only." There might be disruptions when the security patches are applied to the nodes. However AKS is limiting disruptions by only reimaging your nodes only when necessary, such as for certain kernel security packages. When the patches are applied, the VHD is updated and existing machines are upgraded to that VHD, honoring maintenance windows and surge settings. If AKS decides that reimaging nodes isn't necessary, it patches nodes live without draining pods and performs no VHD update. This option incurs the extra cost of hosting the VHDs in your node resource group. If you use this channel, Linux
|

`SecurityPatch`

works on kubernetes patch versions that are deprecated, so long as the minor Kubernetes version is still supported. [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks)and[Azure Linux with OS Guard on AKS](use-azure-linux-os-guard)do not support`SecurityPatch`

.`NodeImage`

[unattended upgrades](https://help.ubuntu.com/community/AutomaticSecurityUpdates)are disabled by default. Node image upgrades are supported as long as cluster Kubernetes minor version is still in support. Node images are AKS-tested, fully managed, and applied with safe deployment practices.## What to choose - SecurityPatch Channel or NodeImage Channel?

There are two important considerations for you to choose between `SecurityPatch`

or `NodeImage`

channels.

| Property | NodeImage Channel | SecurityPatch Channel | Recommended Channel |
|---|---|---|---|
`Speed of shipping` |
The typical build, test, release, and rollout timelines for a new VHD can take approximately two weeks following safe deployment practices. Although in the event of CVEs, accelerated rollouts can occur on a case by case basis. The exact timing when a new VHD hits a region can be monitored via
|

`NodeImage`

, even with safe deployment practices. SecurityPatch has the advantage of 'Live-patching' in Linux environments, where patching leads to selective 'reimaging' and doesn't reimage every time a patch gets applied. Re-image if it happens is controlled by maintenance windows.`SecurityPatch`

`Bugfixes`

`NodeImage`

## Set the node OS autoupgrade channel on a new cluster

- Set the node OS autoupgrade channel on a new cluster using the
command with the`az aks create`

`--node-os-upgrade-channel`

parameter. The following example sets the node OS autoupgrade channel to`SecurityPatch`

.

```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="myResourceGroup$RANDOM_SUFFIX"
export AKS_CLUSTER="myAKSCluster$RANDOM_SUFFIX"
az aks create \
--resource-group $RESOURCE_GROUP \
--name $AKS_CLUSTER \
--node-os-upgrade-channel SecurityPatch \
--generate-ssh-keys
```


## Set the node OS autoupgrade channel on an existing cluster

- Set the node os autoupgrade channel on an existing cluster using the
command with the`az aks update`

`--node-os-upgrade-channel`

parameter. The following example sets the node OS autoupgrade channel to`SecurityPatch`

.

```
az aks update --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER --node-os-upgrade-channel SecurityPatch
```


Results:

```
{
"autoUpgradeProfile": {
"nodeOsUpgradeChannel": "SecurityPatch"
}
}
```


## Update ownership and schedule

The default cadence means there's no planned maintenance window applied.

| Channel | Updates Ownership | Default cadence |
|---|---|---|
`Unmanaged` |
OS driven security updates. AKS has no control over these updates. | Nightly around 6AM UTC for Ubuntu and Azure Linux. Monthly for Windows. |
`SecurityPatch` |
AKS-tested, fully managed, and applied with safe deployment practices. For more information, see
|

`NodeImage`

[AKS Node Images in Release tracker](release-tracker)Note

While Windows security updates are released on a monthly basis, using the `Unmanaged`

channel won't automatically apply these updates to Windows nodes. If you choose the `Unmanaged`

channel, you need to manage the reboot process for Windows nodes.

## Node channel known limitations

Currently, when you set the

[cluster autoupgrade channel](auto-upgrade-cluster)to`node-image`

, it also automatically sets the node OS autoupgrade channel to`NodeImage`

. You can't change node OS autoupgrade channel value if your cluster autoupgrade channel is`node-image`

. In order to set the node OS autoupgrade channel value, check the[cluster autoupgrade channel](auto-upgrade-cluster)value isn't`node-image`

.The

`SecurityPatch`

channel isn't supported on Windows OS node pools.

Note

Use CLI version 2.61.0 or above for the `SecurityPatch`

channel.

## Node OS planned maintenance windows

Planned maintenance for the node OS autoupgrade starts at your specified maintenance window.

Note

To ensure proper functionality, use a maintenance window of four hours or more.

For more information on Planned Maintenance, see [Use Planned Maintenance to schedule maintenance windows for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Node OS autoupgrades FAQ

### How can I check the current nodeOsUpgradeChannel value on a cluster?

Run the `az aks show`

command and check the "autoUpgradeProfile" to determine what value the `nodeOsUpgradeChannel`

is set to:

```
az aks show --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER --query "autoUpgradeProfile"
```


Results:

```
{
"nodeOsUpgradeChannel": "SecurityPatch"
}
```


### How can I monitor the status of node OS autoupgrades?

To view the status of your node OS auto upgrades, look up [activity logs](monitor-aks-reference) on your cluster. You can also look up specific upgrade-related events as mentioned in [Upgrade an AKS cluster](upgrade-cluster). AKS also emits upgrade-related Event Grid events. To learn more, see [AKS as an Event Grid source](quickstart-event-grid).

### Can I change the node OS autoupgrade channel value if my cluster autoupgrade channel is set to `node-image`

?

No. Currently, when you set the [cluster autoupgrade channel](auto-upgrade-cluster) to `node-image`

, it also automatically sets the node OS autoupgrade channel to `NodeImage`

. You can't change the node OS autoupgrade channel value if your cluster autoupgrade channel is `node-image`

. In order to be able to change the node OS autoupgrade channel values, make sure the [cluster autoupgrade channel](auto-upgrade-cluster) isn't `node-image`

.

### Why is `SecurityPatch`

recommended over `Unmanaged`

channel?

On the `Unmanaged`

channel, AKS has no control over how and when the security updates are delivered. With `SecurityPatch`

, the security updates are fully tested and follow safe deployment practices. `SecurityPatch`

also honors maintenance windows. For more information, see [Increased security and resiliency of Canonical workloads on Azure](https://techcommunity.microsoft.com/t5/linux-and-open-source-blog/increased-security-and-resiliency-of-canonical-workloads-on/ba-p/3970623).

### Does `SecurityPatch`

always lead to a reimage of my nodes?

AKS limits reimages to only when necessary, such as certain kernel packages that may require a reimage to get fully applied. `SecurityPatch`

is designed to minimize disruptions as much as possible. If AKS decides reimaging nodes isn't necessary, it patches nodes live without draining pods and no VHD update is performed in such cases.

### Why does `SecurityPatch`

channel requires to reach `snapshot.ubuntu.com`

endpoint?

With the `SecurityPatch`

channel, the Linux cluster nodes have to download the required security patches and updates from ubuntu snapshot service described in [ubuntu-snapshots-on-azure-ensuring-predictability-and-consistency-in-cloud-deployments](https://ubuntu.com/blog/ubuntu-snapshots-on-azure-ensuring-predictability-and-consistency-in-cloud-deployments).

### How do I know if a `SecurityPatch`

or `NodeImage`

upgrade is applied on my node?

Run the `kubectl get nodes --show-labels`

command to list the nodes in your cluster and their labels.

Among the returned labels, you should see a line similar to the following output:

```
kubernetes.azure.com/node-image-version=AKSUbuntu-2204gen2containerd-202410.27.0-2024.12.01
```


Here, the base node image version is `AKSUbuntu-2204gen2containerd-202410.27.0`

. If applicable, the security patch version typically follows. In the above example, it's `2024.12.01`

.

The same details also be looked up in the Azure portal under the node label view:

## Next steps

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).


---

<!-- DOCUMENTO FUSIONADO: __node-pool-unique-subnet_concepts-network-services_node-auto-provisioning-upgra_5ff2d9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _node-pool-unique-subnet_concepts-network-services.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: node-pool-unique-subnet.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-pool-unique-subnet -->

# Create node pools with unique subnets in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Certain workloads might require splitting cluster nodes into separate pools for logical isolation. Separate subnets dedicated to each node pool in the cluster can help support this isolation, which can address requirements such as having noncontiguous virtual network address space to split across node pools.

In this article, you learn how to create node pools with unique subnets in Azure Kubernetes Service (AKS).

## Prerequisites

[Azure CLI](/en-us/cli/azure/install-azure-cli)version 2.35.0 or later. Run`az version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).- An existing AKS cluster with a system node pool. If you need to create one, see
[Create an AKS cluster with a single node pool](create-node-pools#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli).

## Limitations

- All subnets assigned to node pools must belong to the same virtual network (VNet).
- System pods must have access to all nodes and pods in the cluster to provide critical functionality, such as DNS resolution and tunneling kubectl logs/exec/port-forward proxy.
- If you expand your VNet after creating the cluster, you must update your cluster before adding a subnet outside the original CIDR block. While AKS errors out on the agent pool add, the
`aks-preview`

Azure CLI extension (version 0.5.66 and higher) now supports running`az aks update`

command with only the required`--resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`

arguments. This command performs an update operation without making any changes, which can recover a cluster stuck in a failed state. - In clusters with Kubernetes version less than 1.23.3, kube-proxy SNATs traffic from new subnets, which can cause Azure Network Policy to drop the packets.
- Windows nodes SNAT traffic to the new subnets until the node pool is reimaged.
- Internal load balancers default to one of the node pool subnets.

## Add a node pool with a unique subnet

Add a node pool with a unique subnet into your existing AKS cluster using the

command and the`az aks nodepool add`

`--vnet-subnet-id`

parameter specified.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-count 3 \ --vnet-subnet-id $SUBNET_RESOURCE_ID`


## Next steps

For more information about node pools in AKS, see [Manage node pools for a cluster in Azure Kubernetes Service (AKS)](manage-node-pools).


---

<!-- DOCUMENTO FUSIONADO: concepts-network-services.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-network-services -->

# Kubernetes Services in AKS

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can use Kubernetes Services to logically group pods and provide network connectivity by allowing direct access to them through a specific IP address or DNS name on a designated port. This allows you to expose your application workloads to other services within the cluster or to external clients without having to manually manage the network configuration for each pod hosting a workload.

You can specify what kind of service you want using Kubernetes *Service type values*. For more information, see the

[Kubernetes Service documentation](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types).

The following Service types are available in AKS: [ ClusterIP](#clusterip),

[,](#nodeport)

`NodePort`

[, and](#loadbalancer)

`LoadBalancer`

[.](#externalname)

`ExternalName`

## ClusterIP

`ClusterIP`

creates an internal IP address for use within the AKS cluster. The `ClusterIP`

Service is good for *internal-only applications* that support other workloads within the cluster. ClusterIP is used by default if you don't explicitly specify a type for a Service.


## NodePort

`NodePort`

creates a port mapping on the underlying node that allows the application to be accessed directly with the node IP address and port.


## LoadBalancer

`LoadBalancer`

creates an Azure load balancer resource, configures an external IP address, and connects the requested pods to the load balancer backend pool. To allow customer traffic to reach the application, load balancing rules are created on the desired ports.


For HTTP load balancing of inbound traffic, you can also use an [Ingress controller](concepts-network-ingress#ingress-controllers).

You can also use the `LoadBalancer`

type to create multiple public load balancers in a single AKS cluster. This is useful for large clusters or port-heavy workloads that can quickly exhaust the limits of a single load balancer. For more information, see [Use multiple public load balancers in Azure Kubernetes Service (preview)](use-multiple-standard-load-balancer).

## ExternalName

`ExternalName`

creates a specific DNS entry for easier application access. You can dynamically assign the load balancers and service IP address, or you can specify an existing static IP address. You can assign both internal and external static IP addresses. Existing static IP addresses are often tied to a DNS entry.

You can create both *internal* and *external* load balancers. Internal load balancers are only assigned a private IP address, so they can't be accessed from the Internet.


---

<!-- DOCUMENTO FUSIONADO: node-auto-provisioning-upgrade-image.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-upgrade-image -->

# Node image updates for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of node image updates for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS), including how it works, recommended maintenance windows, and examples to get started.

## How do node image updates work for node auto-provisioning nodes?

By default, NAP node pool virtual machines (VMs) are automatically updated when a new image version is available. You can configure an [AKS-managed node operating system (OS) upgrade schedule maintenance window](#node-os-upgrade-maintenance-windows-for-nap) to control when new images are picked up and applied to your NAP nodes, or [use Karpenter Node Disruption Budgets and Pod Disruption Budgets](#karpenter-node-disruption-budgets-and-pod-disruption-budgets-for-nap) to control how and when disruption occurs during upgrades.

Note

NAP forces the latest image version to be picked up if the existing node image version is older than 90 days. This bypasses any existing maintenance window.

## Node OS upgrade maintenance windows for NAP

You can use the [AKS planned maintenance feature](planned-maintenance) with a [node OS auto-upgrade channel](auto-upgrade-node-os-image) to configure a `aksManagedNodeOSUpgradeSchedule`

maintenance window that controls when to perform node OS security patching scheduled by your designated node OS auto-upgrade channel.

### Node OS upgrade maintenance window behavior and considerations

Keep the following information in mind when configuring a node OS upgrade maintenance window for NAP:

- The
`aksManagedNodeOSUpgradeSchedule`

maintenance configuration determines the window during which NAP picks up a new image. This configuration doesn't necessarily determine when existing nodes are disrupted. - The upgrade mechanism and decision criteria are specific to NAP/Karpenter and are evaluated by NAP's drift logic. NAP respects Karpenter Node Disruption Budgets and Pod Disruption Budgets. For more information about drift, see the
[Karpenter drift documentation](https://karpenter.sh/docs/concepts/disruption/#drift). - These NAP upgrade decisions are separate from the cluster
`NodeImage`

and`SecurityPatch`

channels. However, the`aksManagedNodeOSUpgradeSchedule`

maintenance configuration applies them as well. - We recommend using a maintenance window of four hours or more for reliable operation.
- If no maintenance configuration exists, AKS might use a fallback schedule to pick up new images, which can cause images to be picked up at unexpected times. You can avoid unexpected timing of new images and upgrades by defining an explicit
`aksManagedNodeOSUpgradeSchedule`

. - Allow at least 30 minutes between creating or updating a maintenance configuration and the scheduled start time to ensure AKS has time to reconcile the new configuration.

### Recommended schedule pattern for NAP-managed nodes

We recommend the following schedule pattern for NAP-managed nodes:

**Weekly cadence**: Recommended for routine node image roll outs (for example:*Every week on Sunday*).

## Create a node OS maintenance schedule example

The following sections show you how to create a weekly maintenance window for NAP-managed nodes using the Azure CLI and a JSON configuration file and how to update, view, list, and delete the maintenance configuration.

### Create a maintenance configuration

Create a JSON file named

`nodeosMaintenance.json`

with a weekly maintenance window (for example:*Sunday at 01:00 UTC for 4 hours*).`{ "properties": { "maintenanceWindow": { "durationHours": 4, "schedule": { "weekly": { "intervalWeeks": 1, "dayOfWeek": "Sunday" } }, "startDate": "2025-01-01", "startTime": "01:00", "utcOffset": "+00:00" } } }`

Add the maintenance configuration to your cluster using the

command.`az aks maintenanceconfiguration add`

`az aks maintenanceconfiguration add \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule \ --config-file ./nodeosMaintenance.json`


### Update, view, list, or delete a maintenance configuration

You can use the following commands to update, view, list, or delete a maintenance configuration for NAP-managed nodes:

Update a maintenance configuration by modifying the JSON file and then running the

command.`az aks maintenanceconfiguration update`

`az aks maintenanceconfiguration update \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule \ --config-file ./nodeosMaintenance.json`

View the details of a maintenance configuration using the

command.`az aks maintenanceconfiguration show`

`az aks maintenanceconfiguration show \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule`

List all maintenance configurations for your cluster using the

command.`az aks maintenanceconfiguration list`

`az aks maintenanceconfiguration list \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME`

Delete a maintenance configuration using the

command.`az aks maintenanceconfiguration delete`

`az aks maintenanceconfiguration delete \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule`


For complete details, examples, and advanced scenarios, see [Use Planned Maintenance to schedule maintenance windows for your AKS cluster](planned-maintenance).

## Karpenter Node Disruption Budgets and Pod Disruption Budgets for NAP

For more information on configuring Karpenter Node Disruption Budgets and Pod Disruption Budgets for NAP, see the following resources from the official Karpenter documentation:

## Next steps

For more information on node auto-provisioning in AKS, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: __quotas-skus-regions_concepts-scale__windows-best-practices_optimized-addon-sca_62cda1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _quotas-skus-regions_concepts-scale.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: quotas-skus-regions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/quotas-skus-regions -->

# Quotas, virtual machine size restrictions, and region availability in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure services set default limits and quotas for resources and features, including usage restrictions for certain virtual machine (VM) SKUs.

This article details the default resource limits for Azure Kubernetes Service (AKS) resources and the availability of AKS in Azure regions.

## Service quotas and limits

| Resource | Limit |
|---|---|
| Maximum number of clusters per subscription globally | 5,000 |
| Maximum nodes per cluster with Virtual Machine Scale Sets and
|

[node pools](/en-us/azure/aks/create-node-pools)Note: If you're unable to scale up to 5,000 nodes per cluster, see

[Best Practices for Large Clusters](/en-us/azure/aks/best-practices-performance-scale-large).[Kubenet](/en-us/azure/aks/concepts-network-legacy-cni#kubenet)networking plug-inAzure CLI default: 110

Azure Resource Manager template default: 110

Azure portal deployment default: 30

[Azure Container Networking Interface (Azure CNI)](/en-us/azure/aks/concepts-network-cni-overview)1Maximum recommended for Windows Server containers: 110

Default: 30

OSM controllers per cluster: 1

Pods per OSM controller: 1600

Kubernetes service accounts managed by OSM: 160

[Standard Load Balancer SKU](/en-us/azure/load-balancer/load-balancer-overview)1 Windows Server containers must use Azure CNI networking plug-in. Kubenet isn't supported for Windows Server containers.

| Kubernetes Control Plane tier | Limit |
|---|---|
| Standard tier | Automatically scales Kubernetes API server based on load. Larger control plane component limits and API server/etcd instances. |
| Free tier | Limited resources with
Not advised for production/critical workloads. |

### Quota limits on AKS Managed Clusters

Starting in September 2025, Azure Kubernetes Service will begin rolling out a change to enable quota for all current and new AKS customers. This rollout is expected to take place between September 1-30, 2025.

AKS quota will represent a limit of the maximum number of managed clusters (AKS clusters) that an Azure subscription can create per region. Once managed cluster quota is released, customers will need both quota for managed clusters and quota for their nodes (VM skus) in order to create an AKS cluster.

**Existing AKS customer subscriptions** will be given a default limit at or above their current usage depending on the available regional capacity. **Existing subscriptions using AKS for the first time and new subscriptions** will be given a default limit.

Customers can [view quota limits and usage](/en-us/azure/quotas/view-quotas) and [request additional quota](/en-us/azure/quotas/quickstart-increase-quota-portal) via the Azure portal Quotas page or via the [Quotas REST API](/en-us/rest/api/reserved-vm-instances/quotaapi). Prior to rollout completion, quota limits and usage *may* be visible in the Portal Quotas blade and customers will be able to request quota —however, the limits will not be enforced until rollout is complete.


lightbox="./media/quotas-skus-regions/portal-quotas-page-expanded.png"

When Managed Clusters Quota is rolled out, customers will receive the following error if they attempt to create a new cluster and are out of quota:

```
ManagedClusterCountExceedsQuotaLimit: Operation results in exceeding quota limits for managed clusters. Maximum allowed: %d, Current usage: %d, Additional requested: %d. Consider deleting unused clusters or requesting a quota increase. To request a quota increase, follow the instructions here: https://learn.microsoft.com/azure/quotas/quickstart-increase-quota-portal.
```


To remedy this, customers can [request additional quota in the Azure portal Quotas page](/en-us/azure/quotas/view-quotas) or via the [Quotas REST API](/en-us/rest/api/reserved-vm-instances/quotaapi).

#### AKS Managed Clusters Quota Limits

| Subscription Type | Default number of AKS clusters per subscription per region for new subscriptions1 |
Maximum number of AKS clusters per subscription per region via self service using
2 |
|---|

1 The default number of AKS clusters per subscription per region for new subscriptions may vary in regions with capacity constraints.

2 To request an increase of the quota limit, [use the Azure portal Quotas request process](/en-us/azure/quotas/quickstart-increase-quota-portal). Quota increase requests above the maximum self service amount will require a support ticket. Free Trial and Azure for Students subscriptions aren't eligible for limit or quota increases. If you have a Free Trial or Azure for Students subscription, you can upgrade to a pay-as-you-go subscription to get higher quota limits.

### Throttling limits on AKS resource provider APIs

AKS uses the [token bucket](https://en.wikipedia.org/wiki/Token_bucket) throttling algorithm to limit certain AKS [resource provider](/en-us/azure/azure-resource-manager/management/resource-providers-and-types) APIs. Throttling limits ensures the performance of the service and promotes fair usage of the service for all customers.

The buckets have a fixed size (also known as a burst rate) and refill over time at a fixed rate (also known as a sustained rate). Each throttling limit is in effect at the regional level for the specified resource in that region. For example, in the following table, a Subscription can call ListManagedClusters a maximum of 60 times (burst rate) at once for each ResourceGroup, but can continue to make 1 call every second thereafter (sustained rate).

| API request | Bucket size | Refill rate | Scope |
|---|---|---|---|
| LIST ManagedClusters | 500 requests | 1 requests / 1 second | Subscription |
| LIST ManagedClusters | 60 requests | 1 request / 1 second | ResourceGroup |
| PUT AgentPool | 20 requests | 1 request / 1 minute | AgentPool |
| PUT ManagedCluster | 20 requests | 1 request / 1 minute | ManagedCluster |
| GET ManagedCluster | 60 requests | 1 request / 1 second | Managed Cluster |
| GET Operation Status | 200 requests | 2 requests / 1 second | Subscription |
| All Other APIs | 60 requests | 1 request / 1 second | Subscription |

Note

The ManagedClusters and AgentPools buckets are counted separately for the same AKS cluster.

If a request is throttled, the request returns HTTP response code `429`

(Too Many Requests) and the error code shows as `Throttled`

in the response. Each throttled request includes a `Retry-After`

in the HTTP response header with the interval to wait before retrying, in seconds. Clients that use a bursty API call pattern should ensure that the Retry-After can be handled appropriately. To learn more about Retry-After, see the [following article](https://developer.mozilla.org/docs/Web/HTTP/Headers/Retry-After). Specifically, AKS uses `delay-seconds`

to specify the retry.

## Provisioned infrastructure

All other network, compute, and storage limitations apply to the provisioned infrastructure. For the relevant limits, see [Azure subscription and service limits](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits).

Important

When you upgrade an AKS cluster, extra resources are temporarily consumed. These resources include available IP addresses in a virtual network subnet or virtual machine vCPU quota.

For Windows Server containers, you can perform an upgrade operation to apply the latest node updates. If you don't have the available IP address space or vCPU quota to handle these temporary resources, the cluster upgrade process fails. For more information on the Windows Server node upgrade process, see [Upgrade a node pool in AKS](use-multiple-node-pools#upgrade-a-node-pool).

## Supported VM sizes

The list of supported VM sizes in AKS is evolving with the release of new VM SKUs in Azure. Follow the [AKS release notes](https://github.com/Azure/AKS/releases) to stay informed of new supported SKUs.

## Restricted VM sizes

Each node in an AKS cluster contains a fixed amount of compute resources such as vCPU and memory. Due to the required compute resources needed to run Kubernetes correctly, certain VM SKU sizes are restricted by default in AKS. These restrictions are to ensure that pods can be scheduled and function correctly on these nodes.

### User node pools

For user node pools, VM sizes with fewer than two vCPUs and two GBs of RAM (memory) might not be used.

### System node pools

For system node pools, VM sizes with fewer than two vCPUs and four GBs of RAM (memory) might not be used. To ensure that the required *kube-system* pods and your applications can reliably be scheduled, [B series VMs](/en-us/azure/virtual-machines/sizes-b-series-burstable) aren't supported for system node pools and [Av1 series VMs](/en-us/azure/virtual-machines/sizes/retirement/av1-series-retirement) aren't recommended.

For more information on VM types and their compute resources, see [Sizes for virtual machines in Azure](/en-us/azure/virtual-machines/sizes).

## Supported container image sizes

AKS doesn't set a limit on the container image size. However, it's important to understand that the larger the container image, the higher the memory demand. This demand could potentially exceed resource limits or the overall available memory of worker nodes. By default, memory for VM size Standard_DS2_v2 for an AKS cluster is set to 7 GiB.

When a container image is large (1 TiB or more), kubelet might not be able to pull it from your container registry to a node due to lack of disk space.

## Region availability

For the latest list of where you can deploy and run clusters, see [AKS region availability](https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service).

## Smart VM Defaults

As of May 2025, AKS automatically selects the optimal default VM SKU based on available capacity and quota if the parameter is unspecified during deployment. This default ensures that deployments are matched with the best possible SKU, enhancing performance and reliability while optimizing resource utilization. Previously, the default AKS VM SKU was Standard_DS2_V2, but there are now dynamic outcomes in default provisioning based on SKU availability that affects all new VM create operations.

## Cluster configuration presets in the Azure portal

When you create a cluster using the Azure portal, you can choose a preset configuration to quickly customize based on your scenario. You can modify any of the preset values at any time.

| Preset | Description |
|---|---|
| Production Standard | Best for most applications serving production traffic with AKS recommended best practices. |
| Dev/Test | Best for developing new workloads or testing existing workloads. |
| Production Economy | Best for serving production traffic in a cost conscious way if your workloads can tolerate interruptions. |
| Production Enterprise | Best for serving production traffic with rigorous permissions and hardened security. |

| Production Standard | Dev/Test | Production Economy | Production Enterprise | |
|---|---|---|---|---|
System node pool node size |
Standard_D8ds_v5 | Standard_D4ds_v5 | Standard_D8ds_v5 | Standard_D16ds_v5 |
System node pool autoscaling range |
2-5 nodes | 2-5 nodes | 2-5 nodes | 2-5 nodes |
User node pool node size |
Standard_D8ds_v5 | - | Standard_D8as_v4 | Standard_D8ds_v5 |
User node pool autoscaling range |
2-100 nodes | - | 0-25 nodes | 2-100 nodes |
Private cluster |
- | - | - | |
Availability zones |
- | - | ||
Azure Policy |
- | - | ||
Azure Monitor |
- | - | ||
Secrets store CSI driver |
- | - | ||
Network configuration |
Azure CNI Overlay | Azure CNI Overlay | Azure CNI Overlay | Azure CNI Overlay |
Network policy |
None | None | None | None |
Authentication and Authorization |
Local accounts with Kubernetes role-based access control (RBAC) | Local accounts with Kubernetes RBAC | Microsoft Entra ID Authentication with Azure role-based access control (Azure RBAC) | Microsoft Entra ID authentication with Azure RBAC |

## Next steps

You can increase certain default limits and quotas. If your resource supports an increase, request the increase through an [Azure support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest) (for **Issue type**, select **Quota**).


---

<!-- DOCUMENTO FUSIONADO: concepts-scale.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-scale -->

# Scaling options for applications in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When running applications in Azure Kubernetes Service (AKS), you might need to actively increase or decrease the amount of compute resources in your cluster. As you change the number of application instances you have, you might need to change the number of underlying Kubernetes nodes. You might also need to provision a large number of other application instances.

This article introduces core AKS application scaling concepts, including [manually scaling pods or nodes](#manually-scale-pods-or-nodes), using the [Horizontal pod autoscaler](#horizontal-pod-autoscaler), using the [Cluster autoscaler](#cluster-autoscaler), and integrating with [Azure Container Instances (ACI)](#burst-to-azure-container-instances-aci).

## Manually scale pods or nodes

You can manually scale replicas, or pods, and nodes to test how your application responds to a change in available resources and state. Manually scaling resources lets you define a set amount of resources to use, such as the number of nodes, to maintain a fixed cost. To manually scale, you define a replica or node count. The Kubernetes API then schedules the creation of more pods or the draining of nodes based on that replica or node count.

When you scale down nodes, the Kubernetes API calls the relevant Azure Compute API tied to the compute type used by your cluster. For example, for clusters built on Virtual Machine Scale Sets, the Virtual Machine Scale Sets API determines which nodes to remove. To learn more about how nodes are selected for removal on scale down, see the [Virtual Machine Scale Sets FAQ](/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-faq#if-i-reduce-my-scale-set-capacity-from-20-to-15--which-vms-are-removed-).

To get started with manually scaling nodes, see [manually scale nodes in an AKS cluster](scale-cluster). To manually scale the number of pods, see [kubectl scale command](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_scale/).

## Horizontal pod autoscaler

Kubernetes uses the horizontal pod autoscaler (HPA) to monitor the resource demand and automatically scale the number of pods. By default, the HPA checks the Metrics API every 15 seconds for any required changes in replica count, while the Metrics API retrieves data from the Kubelet every 60 seconds. As a result, HPA is updated every 60 seconds. When changes are required, the number of replicas is scaled accordingly. HPA works with AKS clusters that have deployed Metrics Server for Kubernetes version 1.8 and higher.

When you configure the HPA for a given deployment, you define the minimum and maximum number of replicas that can run. You also define the metric to monitor and base scaling decisions on, such as CPU usage.

To get started with the horizontal pod autoscaler in AKS, see [Autoscale pods in AKS](tutorial-kubernetes-scale#autoscale-pods).

### Cooldown of scaling events

As the HPA is effectively updated every 60 seconds, previous scale events might not have successfully completed before another check is made. This behavior could cause the HPA to change the number of replicas before the previous scale event could receive application workload and the resource demands to adjust accordingly.

To minimize race events, a delay value is set. This value defines how long the HPA must wait after a scale event before another scale event can be triggered. This behavior allows the new replica count to take effect and the Metrics API to reflect the distributed workload. There's [no delay for scale-up events as of Kubernetes 1.12](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/#support-for-cooldown-delay). However, the default delay on scale down events is *5 minutes*.

## Cluster autoscaler

To respond to changing pod demands, the Kubernetes cluster autoscaler adjusts the number of nodes based on the requested compute resources in the node pool. By default, the cluster autoscaler checks the Metrics API server every 10 seconds for any required changes in node count. If the cluster autoscaler determines that a change is required, the number of nodes in your AKS cluster is increased or decreased accordingly. The cluster autoscaler works with Kubernetes RBAC-enabled AKS clusters that run Kubernetes 1.10.x or higher.

The cluster autoscaler is typically used alongside the [horizontal pod autoscaler](#horizontal-pod-autoscaler). When combined, the horizontal pod autoscaler increases or decreases the number of pods based on application demand, and the cluster autoscaler adjusts the number of nodes to run more pods.

To get started with the cluster autoscaler in AKS, see [Cluster autoscaler on AKS](cluster-autoscaler).

### Scale out events

If a node doesn't have sufficient compute resources to run a requested pod, that pod can't progress through the scheduling process. The pod can't start unless more compute resources are made available within the node pool.

When the cluster autoscaler notices pods that can't be scheduled because of node pool resource constraints, the number of nodes within the node pool is increased to provide extra compute resources. When the nodes are successfully deployed and available for use within the node pool, the pods are then scheduled to run on them.

If your application needs to scale rapidly, some pods might remain in a state of waiting to be scheduled until more nodes deployed by the cluster autoscaler can accept the scheduled pods. For applications that have high burst demands, you can scale with virtual nodes and [Azure Container Instances](#burst-to-azure-container-instances-aci).

### Scale in events

The cluster autoscaler also monitors the pod scheduling status for nodes that haven't recently received new scheduling requests. This scenario indicates the node pool has more compute resources than required, and the number of nodes can be decreased. By default, nodes that pass a threshold of no longer being needed for 10 minutes are scheduled for deletion. When this situation occurs, pods are scheduled to run on other nodes within the node pool, and the cluster autoscaler decreases the number of nodes.

Your applications might experience some disruption as pods are scheduled on different nodes when the cluster autoscaler decreases the number of nodes. To minimize disruption, avoid applications that use a single pod instance.

## Kubernetes Event-driven Autoscaling (KEDA)

[Kubernetes Event-driven Autoscaling](https://keda.sh/docs/2.13/concepts/) (KEDA) is an open source component for event-driven autoscaling of workloads. It scales workloads dynamically based on the number of events received. KEDA extends Kubernetes with a custom resource definition (CRD), referred to as a *ScaledObject*, to describe how applications should be scaled in response to specific traffic.

KEDA scaling is useful in scenarios where workloads receive bursts of traffic or handle high volumes of data. KEDA differs from the Horizontal Pod Autoscaler as KEDA is event-driven and scales based on the number of events, while HPA is metrics-driven based on the resource utilization (for example, CPU and memory).

To get started with the KEDA add-on in AKS, see [KEDA overview](keda-about).

## Node Autoprovisioning

[Node autoprovisioning (preview)](node-autoprovision) (NAP), uses the open source Karpenter project that automatically deploys, configures, and manages [Karpenter](https://karpenter.sh/) on your AKS cluster. NAP dynamically provisions nodes based on pending pod resource requirements; it'll automatically select the optimal virtual machine (VM) SKU and quantity to meet real-time demand.

NAP takes a predefined list of VM SKUs as the starting point to decide which SKU is best suited for pending workloads. For more precise control, users can define the upper limits of resources used by a node pool and preferences of where workloads should be scheduled if there are multiple node pools.

## Control Plane Scaling and Safeguards

Kubernetes has a multi-dimensional scale envelope with each resource type representing a dimension. Not all resources are alike. For example, watches are commonly set on secrets, which result in list calls to the kube-apiserver that add cost and a disproportionately higher load on the control plane compared to resources without watches.

The control plane manages all the resource scaling in the cluster, so the more you scale the cluster within a given dimension, the less you can scale within other dimensions. For example, running hundreds of thousands of pods in an AKS cluster impacts how much pod churn rate (pod mutations per second) the control plane can support. Refer to ** best practices**.

AKS automatically scales control plane components based on key signals such as the total number of cores in the cluster and CPU or memory pressure on the control plane components.

To verify whether the control plane has scaled up, check the ConfigMap named 'large-cluster-control-plane-scaling-status'

```
kubectl describe configmap large-cluster-control-plane-scaling-status -n kube-system
```


### Control Plane Safeguards

If scaling the API server automatically does not stabilize it under high load scenarios, AKS deploys a managed API server guard. This guard acts as a last-resort mechanism to protect the API server by throttling non-system client requests and preventing the control plane from becoming completely unresponsive. System-critical calls to API server from components such as kubelet will continue to function normally.

To verify whether the managed API server guard has been applied, check for the presence of **"aks-managed-apiserver-guard"** FlowSchema and PriorityLevelConfiguration.

```
kubectl get flowschemas
kubectl get prioritylevelconfigurations
```


Refer to [API server and Etcd Troubleshooting guide](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-apiserver-etcd#cause-4-aks-managed-api-server-guard-was-applied) if the **"aks-managed-apiserver-guard"** FlowSchema and PriorityLevelConfiguration have been applied on the cluster for quick mitigation.

## Burst to Azure Container Instances (ACI)

To rapidly scale your AKS cluster, you can integrate with Azure Container Instances (ACI). Kubernetes has built-in components to scale the replica and node count. However, if your application needs to rapidly scale, the [horizontal pod autoscaler](#horizontal-pod-autoscaler) might schedule more pods than what the existing compute resources in the node pool can support. If configured, this scenario would then trigger the [cluster autoscaler](#cluster-autoscaler) to deploy more nodes in the node pool, but it might take a few minutes for those nodes to successfully provision and allow the Kubernetes scheduler to run pods on them.

ACI lets you quickly deploy container instances without extra infrastructure overhead. When you connect with AKS, ACI becomes a secured, logical extension of your AKS cluster. The [virtual nodes](virtual-nodes-cli) component, which is based on [virtual Kubelet](https://virtual-kubelet.io/), is installed in your AKS cluster that presents ACI as a virtual Kubernetes node. Kubernetes can then schedule pods that run as ACI instances through virtual nodes, not as pods on VM nodes directly in your AKS cluster.

Your application requires no modifications to use virtual nodes. Your deployments can scale across AKS and ACI and with no delay as the cluster autoscaler deploys new nodes in your AKS cluster.

Virtual nodes are deployed to another subnet in the same virtual network as your AKS cluster. This virtual network configuration secures the traffic between ACI and AKS. Like an AKS cluster, an ACI instance is a secure, logical compute resource isolated from other users.

## Next steps

To get started with scaling applications, see the following resources:

- Manually scale
[pods](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_scale/)or[nodes](scale-cluster) - Use the
[horizontal pod autoscaler](tutorial-kubernetes-scale#autoscale-pods) - Use the
[cluster autoscaler](cluster-autoscaler) - Use the
[Kubernetes Event-driven Autoscaling (KEDA) add-on](keda-about)

For more information on core Kubernetes and AKS concepts, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: _windows-best-practices_optimized-addon-scaling.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: windows-best-practices.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/windows-best-practices -->

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

<!-- DOCUMENTO FUSIONADO: optimized-addon-scaling.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/optimized-addon-scaling -->

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
