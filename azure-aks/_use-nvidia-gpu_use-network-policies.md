---
merged_at: 2026-01-25T12:25:33.970194
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-nvidia-gpu.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-nvidia-gpu -->

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


---

<!-- DOCUMENTO FUSIONADO: use-network-policies.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-network-policies -->

# Secure traffic between pods with network policies in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Support for Azure Network Policy Manager (NPM) on **Windows** nodes in AKS ends on **September 30, 2026**.

This change applies only to customers already onboarded to NPM. **Subscriptions that aren't registered with this feature will no longer be able to onboard**. Existing onboarded customers can continue using NPM until the end-of-support date.

To ensure your setup continues to receive support, security updates, and deployment compatibility, explore alternative options like [Network Security Groups (NSGs)](concepts-network) on the node level or open-source tools like [Project Calico](https://www.tigera.io/tigera-products/calico/).

Important

Support for Azure Network Policy Manager (NPM) on **Linux** nodes in AKS ends on **September 30, 2026**.

To avoid service disruptions, you need to [migrate AKS clusters running Linux nodes from NPM to Cilium Network Policy](migrate-from-npm-to-cilium-network-policy) by the end-of-support date.

Important

Support for kubenet networking on AKS clusters ends on **March 31, 2028**.

To avoid service disruptions, you need to upgrade to [Azure Container Networking Interface (CNI) Overlay](concepts-network-azure-cni-overlay) by the end-of-support date.

Install a network policy engine and create Kubernetes network policies to control the flow of traffic between pods in AKS clusters.

## Overview of network policy

By default, all pods in an AKS cluster can send and receive traffic without limitations. To improve security, you can define rules that control the flow of traffic.

Network policy is a Kubernetes specification that defines access policies for communication between pods. When you use network policies, you define an ordered set of rules to send and receive traffic. You apply the rules to a collection of pods that match one or more label selectors.

You define the network policy rules as YAML manifests, and you can include them in wider manifests that also create a deployment or service.

## Network policy options in AKS

Azure provides three network policy engines for enforcing network policies:

**Cilium**(for AKS clusters using[Azure CNI Powered by Cilium](azure-cni-powered-by-cilium))**Azure Network Policy Manager (NPM)****Calico**(an open-source network and network security solution founded by[Tigera](https://www.tigera.io/))

We recommend using Cilium. Cilium enforces network policy on the traffic using Linux Berkeley Packet Filter (BPF), which is more efficient than *IPTables*.

To enforce the specified policies, Azure NPM uses *IPTables* for Linux and *Host Network Service (HNS) ACLPolicies* for Windows. Policies are translated into sets of allowed and disallowed IP pairs. These pairs are then programmed as `IPTable`

or `HNS ACLPolicy`

filter rules.

## Differences between network policy engines: Cilium, Azure NPM, and Calico

| Network policy engine | Supported platforms | Supported networking options | Kubernetes specification compliance | Other features | Support |
|---|---|---|---|---|---|
| Cilium | Linux | Azure CNI | Supports all policy types |
|

[Calico Network Policy issue](https://github.com/Azure/AKS/issues/4038).## Azure Network Policy Manager limitations (Linux)

Azure NPM for Linux has the following limitations:

- Scaling beyond
*250 nodes*and*20,000 pods*isn't supported. If you attempt to scale beyond these limits, you might experience*Out of Memory (OOM)*errors. For better scalability and IPv6 support, we recommend using or upgrading to[Azure CNI Powered by Cilium](update-azure-cni)for your network policy engine. - IPv6 isn't supported. Otherwise, it fully supports the network policy specifications in Linux.

## Azure Network Policy Manager limitations (Windows)

Azure NPM for Windows doesn't support the following features of the network policy specifications:

- Named ports.
- Stream Control Transmission Protocol (SCTP).
- Negative match label or namespace selectors. For example, all labels except
`debug=true`

. `except`

classless interdomain routing (CIDR) blocks (CIDR with exceptions).

## Known issues with Azure Network Policy Manager

You might experience temporary connectivity issues for new connections to/from pods on impacted nodes when either editing or deleting a "large enough" network policy. Hitting this race condition never impacts active connections.

If this race condition occurs for a node, the Azure NPM pod on that node enters a state where it can't update security rules, which might lead to unexpected connectivity for new connections to/from pods on the impacted node. To mitigate the issue, the Azure NPM pod automatically restarts ~15 seconds after entering this state. While Azure NPM is rebooting on the impacted node, it deletes all security rules, then reapplies security rules for all network policies. While all the security rules are being reapplied, there's a chance of temporary, unexpected connectivity for new connections to/from pods on the impacted node.

To limit the chance of hitting this race condition, you can reduce the size of the network policy. This issue is most likely to happen for a network policy with several `ipBlock`

sections. A network policy with *four or fewer* `ipBlock`

sections is less likely to hit the issue.

## Load balancer services and network policies

Kubernetes service routing for both inbound and outbound services often involves rewriting the source and destination IPs on traffic that's being processed, including traffic that comes into the cluster from a `LoadBalancer`

service. This rewrite behavior means that the network policies might not properly process traffic being received from or sent to an external service. For more information, see the [Kubernetes Network Policies documentation](https://kubernetes.io/docs/concepts/services-networking/network-policies/).

To restrict what sources can send traffic to a load balancer service, use `spec.loadBalancerSourceRanges`

to configure traffic blocking that applies before any rewrites occur. For more information, see the [AKS Standard load balancer documentation](/en-us/azure/aks/load-balancer-standard#restrict-inbound-traffic-to-specific-ip-ranges).

## Before you begin

You need the Azure CLI version 2.0.61 or later installed and configured. Find the version using the `az --version`

command. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Instead of using a system-assigned identity, you can also use a user-assigned identity. For more information, see [Use managed identities](use-managed-identity).

## Create an AKS cluster with Azure Network Policy Manager (Linux)

Set environment variables for the resource group name, cluster name, and location. Replace the values as needed.

`export RESOURCE_GROUP=myResourceGroup export CLUSTER_NAME=myAKSCluster export LOCATION=eastus`

Create an AKS cluster using the

and specify`az aks create`

`azure`

for the`network-plugin`

and`network-policy`

.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --node-count 1 \ --network-plugin azure \ --network-policy azure \ --generate-ssh-keys`


## Create an AKS cluster with Azure Network Policy Manager (Windows Server 2022 (preview))

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Install the `aks-preview`

Azure CLI extension

Install the

`aks-preview`

extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

`az extension update --name aks-preview`


### Register the `WindowsNetworkPolicyPreview`

feature flag

Register the

`WindowsNetworkPolicyPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "WindowsNetworkPolicyPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "WindowsNetworkPolicyPreview"`

When the status reflects

*Registered*, refresh the registration of the`Microsoft.ContainerService`

resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create administrator credentials for Windows Server containers

Create a username to use as administrator credentials for your Windows Server containers on your cluster. The following command prompts you for a username. Set it to

`WINDOWS_USERNAME`

.`echo "Please enter the username to use as administrator credentials for Windows Server containers on your cluster: " && read WINDOWS_USERNAME`


### Create the AKS cluster

Set environment variables for the resource group name, cluster name, and location. Replace the values as needed.

`export RESOURCE_GROUP=myResourceGroup export CLUSTER_NAME=myAKSCluster export LOCATION=eastus`

Create an AKS cluster using the

and specify`az aks create`

`azure`

for the`network-plugin`

and`network-policy`

.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --node-count 1 \ --windows-admin-username $WINDOWS_USERNAME \ --network-plugin azure \ --network-policy azure \ --generate-ssh-keys`


## Create an AKS cluster with Calico

Create an AKS cluster using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command and specify

`--network-plugin azure`

and `--network-policy calico`

. Specifying `--network-policy calico`

enables Calico on both Linux and Windows node pools.If you plan on adding Windows node pools to your cluster, include the `windows-admin-username`

and `windows-admin-password`

parameters that meet the [Windows Server password requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference). To create administrator credentials for Windows Server containers on your cluster, see [Create administrator credentials for Windows Server containers](#create-administrator-credentials-for-windows-server-containers).

Important

At this time, using Calico network policies with Windows nodes is available on new clusters using Kubernetes version 1.20 or later with Calico 3.17.2 and requires that you use Azure CNI networking. Windows nodes on AKS clusters with Calico enabled also have Floating IP enabled by default.

For clusters with only Linux node pools running Kubernetes 1.20 with earlier versions of Calico, the Calico version automatically upgrades to 3.17.2.

## Install Azure Network Policy Manager or Calico on an existing cluster

Warning

Keep the following information in mind when installing Azure NPM or Calico on an existing cluster:

- The upgrade process triggers each node pool to be reimaged simultaneously. Upgrading each node pool separately isn't supported.
- Within each node pool, nodes follow the same reimaging process as standard Kubernetes version upgrade operations. This behavior means that buffer nodes are temporarily added to minimize disruption to running applications during the node reimaging process. Any disruptions that might occur are similar to what you might encounter during a node image upgrade or
[Kubernetes version upgrade](upgrade-cluster).

The following information applies to upgrades from kubenet with Calico to Azure CNI Overlay with Calico:

- In kubenet clusters with Calico enabled, Calico is used as both a CNI and network policy engine.
- In Azure CNI clusters, Calico is used only for network policy enforcement, not as a CNI. This can cause a short delay between when the pod starts and when Calico allows outbound traffic from the pod.

Update an existing cluster to install Azure NPM or Calico using the

command and specifying`az aks update`

`azure`

or`calico`

for the`--network-policy`

parameter. The following example command shows how to install either Azure NPM:`az aks update --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --network-policy azure`


## Upgrade an existing cluster with Azure NPM or Calico to Cilium

To upgrade an existing cluster to Azure CNI Powered by Cilium, see [Upgrade an existing cluster to Azure CNI Powered by Cilium](upgrade-aks-ipam-and-dataplane)

## Connect to the AKS cluster

Configure

`kubectl`

to connect to your cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Verify network policy setup

To begin verification of network policy, you create a sample application and set traffic rules.

Create a namespace named

`demo`

to run the sample pods using the`kubectl create namespace`

command.`kubectl create namespace demo`

Create a pod named

`server`

to server on TCP port 80 using the`kubectl run`

command.`kubectl run server -n demo --image=k8s.gcr.io/e2e-test-images/agnhost:2.33 --labels="app=server" --port=80 --command -- /agnhost serve-hostname --tcp --http=false --port "80"`

Create a pod named

`client`

to run Bash using the`kubectl run`

command.`kubectl run -it client -n demo --image=k8s.gcr.io/e2e-test-images/agnhost:2.33 --command -- bash`

Note

If you want to schedule the client or server on a particular node, add the following bit before the

`--command`

argument in the pod creationcommand:`kubectl run`

`--overrides='{"spec": { "nodeSelector": {"kubernetes.io/os": "linux|windows"}}}'`

.In a separate window, get the IP address of the

`server`

pod using the`kubectl get pod`

command.`kubectl get pod --output=wide -n demo`

Your output should resemble the following example output:

`NAME READY STATUS RESTARTS AGE IP NODE NOMINATED NODE READINESS GATES server 1/1 Running 0 30s 10.224.0.72 akswin22000001 <none> <none>`


## Test connectivity with network policies

Tip

To test connectivity without network policies, run the following command in the client shell: `/agnhost connect <server-ip>:80 --timeout=3s --protocol=tcp`

. Replace `<server-ip>`

with the IP address of the server pod. If the connection is successful, there's no output.

Create a file named

`demo-policy.yaml`

and paste the following YAML manifest:`apiVersion: networking.k8s.io/v1 kind: NetworkPolicy metadata: name: demo-policy namespace: demo spec: podSelector: matchLabels: app: server ingress: - from: - podSelector: matchLabels: app: client ports: - port: 80 protocol: TCP`

Apply the network policy manifest using the

command.`kubectl apply`

`kubectl apply –f demo-policy.yaml`

In the client shell, verify connectivity with the server using the following

`/agnhost`

command:`/agnhost connect <server-ip>:80 --timeout=3s --protocol=tcp`

Connectivity with traffic is blocked because the server is labeled with

`app=server`

, but the client isn't labeled. Your output should resemble the following example output:`TIMEOUT`

Label the

`client`

and verify connectivity with the server using the`kubectl label`

command.`kubectl label pod client -n demo app=client`

If the connection is successful, there's no output.


## Migrate to self-managed Calico

AKS only supports Calico for standard Kubernetes network policies and doesn't test other features. If you want to move to self-managed Calico, follow the Tigera instructions at [Migrate from Azure-managed Calico to self-managed Calico](https://docs.tigera.io/calico/latest/getting-started/kubernetes/managed-public-cloud/aks-migrate). The Tigera documentation mentions that for self-managed Calico you set `--network-policy none`

like in the [uninstall section](#uninstall-azure-network-policy-manager-or-calico).

## Uninstall Azure Network Policy Manager or Calico

Note

Keep the following information in mind when uninstalling Azure NPM or Calico from a cluster:

- The uninstall process
**doesn't remove**Custom Resource Definitions (CRDs) and Custom Resources (CRs) used by Calico. These CRDs and CRs all have names ending with either*projectcalico.org*or*tigera.io*. You can manually remove these CRDs and associated CRs*after*successfully uninstalling Calico. - The upgrade doesn't remove any network policy resources in the cluster, but the policies are no longer enforced after the uninstall process.

Remove Azure Network Policy Manager or Calico from an existing cluster using the

command and specifying`az aks update`

`none`

for the`--network-policy`

parameter.`az aks update --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --network-policy none`


## Clean up resources

In this article, you created a namespace and two pods and applied a network policy. If you no longer need these resources, you can delete them.

Delete the resources using the

command.`kubectl delete`

`kubectl delete namespace demo`
