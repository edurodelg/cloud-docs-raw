---
merged_at: 2026-01-25T15:16:21.129973
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___azure-app-configuration-settings_custom-certificate-authority__shared-health-_1cb524.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __azure-app-configuration-settings_custom-certificate-authority__shared-health-p_356344.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _azure-app-configuration-settings_custom-certificate-authority.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: azure-app-configuration-settings.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-app-configuration-settings -->

# Configure the Azure App Configuration extension for your Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Once you [created the Azure App Configuration extension](azure-app-configuration), you can configure the extension to work best for you and your project using various configuration options, like:

- Configuring the replica count.
- Configuring the log verbosity.
- Configuring the installation namespace.

The extension enables you to configure Azure App Configuration extension settings by using the `--configuration-settings`

parameter in the Azure CLI.

Tip

For a list of available options, see [Azure App Configuration Kubernetes Provider helm values](https://raw.githubusercontent.com/Azure/AppConfiguration-KubernetesProvider/main/deploy/parameter/helm-values.yaml).

## Configure the replica count

The default replica count is `1`

. Create Azure App Configuration extension with customized replica count:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--configuration-settings "replicaCount=3"
```


Note

If configuration settings are sensitive and need to be protected (for example, cert-related information), pass the `--configuration-protected-settings`

parameter and the value will be protected from being read.

## Configure the log verbosity

The default log verbosity is `1`

. Create Azure App Configuration extension with customized log verbosity:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--configuration-settings "logVerbosity=3"
```


Log verbosity levels follow the [klog](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-instrumentation/logging.md#what-method-to-use) convention:

`0`

: Warning and error only.`1`

: Informational, this level is default.`2`

: Detailed steady state information.`3`

: Extended information about changes.`4`

: Debug level verbosity.`5`

: Trace level verbosity.

## Configure the Azure App Configuration extension namespace

The Azure App Configuration extension gets installed in the `azappconfig-system`

namespace by default. To override it, use `--release-namespace`

. Include the cluster `--scope`

to redefine the namespace.

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--scope cluster \
--release-namespace custom-namespace
```


## Show current configuration settings

Use the `az k8s-extension show`

command to show the current Azure App Configuration extension settings:

```
az k8s-extension show --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider
```


## Update configuration settings

To update your Azure App Configuration extension settings, recreate the extension with the desired state. For example, assume we installed the extension using the following configuration:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--configuration-settings "replicaCount=2"
```


To update the `replicaCount`

from two to three, use the following command:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--configuration-settings "replicaCount=3"
```


## Next Steps

Once you successfully install Azure App Configuration extension in your AKS cluster, try [quickstart](/en-us/azure/azure-app-configuration/quickstart-azure-kubernetes-service) to learn how to use it.


---

<!-- DOCUMENTO FUSIONADO: custom-certificate-authority.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/custom-certificate-authority -->

# Use custom certificate authorities (CAs) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Custom Certificate Authority (CA) allows you to add up to 10 base64-encoded certificates to your node's trust store. This feature is often needed when certificate authorities (CAs) are required to be present on the node, like when connecting to a private registry.

This article shows you how to create custom CAs and apply them to your AKS clusters.

Note

The Custom CA feature adds your custom certificates to the trust store of the AKS node. Certificates added with this feature aren't available to containers running in pods. If you need the certificates inside containers, you need to add them separately by adding them to the image used by your pods or at runtime via scripting and a secret.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/free). - Azure CLI version 2.72.0 or later installed and configured. To find your CLI version, run the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - A base64 encoded certificate string or a text file with certificate.

## Limitations

- Windows node pools aren't supported.
- Installing different CAs in the same cluster isn't supported.

## Create a certificate file

Create a text file containing up to 10 blank line separated certificates. When you pass this file to your cluster, the certificates are installed in the trust stores of the AKS node.

Example text file:

`-----BEGIN CERTIFICATE----- cert1 -----END CERTIFICATE----- -----BEGIN CERTIFICATE----- cert2 -----END CERTIFICATE-----`


**Before proceeding to the next step, make sure that there are no blank spaces in your text file to avoid errors**.

## Pass custom CAs to your AKS cluster

Pass certificates to your cluster using the

or`az aks create`

command with`az aks update`

`--custom-ca-trust-certificates`

set to the name of your certificate file.`# Create a new cluster az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --node-count 2 \ --custom-ca-trust-certificates <path-to-certificate-file> \ --generate-ssh-keys # Update an existing cluster az aks update \ --resource-group <resource-group-name> \ --name <cluster-name> \ --custom-ca-trust-certificates <path-to-certificate-file>`

Note

This operation triggers a model update to ensure all existing nodes have the same CAs installed for correct provisioning. AKS creates new nodes, drains existing nodes, deletes existing nodes, and replaces them with nodes that have the new set of CAs installed.


## Verify CAs are installed

Verify the CAs are installed using the

command.`az aks show`

`az aks show --resource-group <resource-group-name> --name <cluster-name> | grep securityProfile -A 4`

In the output, the

`securityProfile`

section should include your custom CA certificates. For example:`"securityProfile": { "azureKeyVaultKms": null, "customCaTrustCertificates": [ "values"`


## Resolve custom CA formatting errors

Adding certificates to a cluster can result in an error if the file with the certificates isn't formatted properly. You might see an error similar to the following example:

```
failed to decode one of SecurityProfile.CustomCATrustCertificates to PEM after base64 decoding
```


If you encounter this error, you should check that your input file has no extra new lines, white spaces, or data other than correctly formatted certificates as shown in the example file.

## Resolve custom CA X.509 Certificate Signed by Unknown Authority errors

AKS requires certificates passed to be properly formatted and base64 encoded. Make sure the CAs you passed are properly base64 encoded and that files with CAs don't have CRLF line breaks.

## Restart containerd to pick up new certificates

If containerd doesn't pick up new certificates, run the `systemctl restart containerd`

command from the node's shell. Once containerd restarts, the container runtime should pick up the new certificates.

## Related content

For more information on AKS security best practices, see [Best practices for cluster security and upgrades in Azure Kubernetes Service (AKS)](operator-best-practices-cluster-security).


---

<!-- DOCUMENTO FUSIONADO: _shared-health-probes_windows-vs-linux-containers.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: shared-health-probes.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/shared-health-probes -->

# Use shared health probes for externalTrafficPolicy: Cluster Services (preview) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

# Use shared health probes for

This article describes how to enable **shared health probe mode** (preview) for Services with `externalTrafficPolicy: Cluster`

in Azure Kubernetes Service (AKS). Shared probe mode improves load balancer efficiency, reduces configuration complexity, and provides more accurate node health monitoring.

## About shared health probe mode

In clusters that use `externalTrafficPolicy: Cluster`

, Azure Standard Load Balancer (SLB) currently creates a *separate probe per Service* and targets each Service's `nodePort`

.

This design means SLB infers node health from whichever **application pod** answers the probe. As clusters grow, this approach leads to several issues, including:

**Configuration drift and blind spots**: SLB can't detect a failed or misconfigured`kube‑proxy`

if iptables rules are still present.**Duplicate health logic**: Readiness must be defined twice. Once in each pod's`readinessProbe`

, and again through SLB annotations.**Operational overhead**: Each Service on each node is probed every*five seconds*, consuming connections, SNAT ports, and SLB rule space.**Feature friction**: Customers can't set`allocateLoadBalancerNodePorts=false`

, and workloads like Istio or ingress‑nginx require extra annotations to keep probes working.**Troubleshooting confusion**: An unhealthy app, Network Policy rule, or scale‑to‑zero event can make an*entire node*appear down.

**Shared probe mode** solves these problems by moving to a *single HTTP probe* for all `externalTrafficPolicy: Cluster`

Services. In shared probe mode:

- SLB probes
`http://<node‑ip>:10356/healthz`

, the standard`kube‑proxy`

health endpoint. - A lightweight sidecar runs next to
`kube‑proxy`

to relay the probe and handle PROXY protocol when Private Link Service is enabled.

## Benefits of shared probe mode

The following table outlines **key benefits** of using shared probe mode:

| Benefit | Why it matters |
|---|---|
| Accurate node health | SLB now measures `kube‑proxy` directly, not an arbitrary backend pod. |
| Simpler configuration | No per‑Service probe annotations; readiness lives solely in the pod spec. |
| Lower traffic overhead | One probe per node instead of Services × (nodes – 1) probes. |

Note

Keep the following information in mind when using shared probe mode:

- Services that use
`externalTrafficPolicy: Local`

are**unchanged**. - This feature does
**not**address container‑native load balancing.

## Before you begin

[Install or update the](#install-or-update-the-aks-preview-azure-cli-extension).`aks-preview`

Azure CLI extension[Register the](#register-the-enableslbsharedhealthprobepreview-feature-flag).`EnableSLBSharedHealthProbePreview`

feature flag in your Azure subscription

### Install or update the `aks-preview`

Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the

`aks-preview`

extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the

`aks-preview`

extension using thecommand.`az extension update`

`az extension update --name aks-preview`


### Register the `EnableSLBSharedHealthProbePreview`

feature flag

Register the

`EnableSLBSharedHealthProbePreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "EnableSLBSharedHealthProbePreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command:`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "EnableSLBSharedHealthProbePreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


---

<!-- DOCUMENTO FUSIONADO: windows-vs-linux-containers.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/windows-vs-linux-containers -->

# Windows container considerations with Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create deployments that use Windows Server containers on Azure Kubernetes Service (AKS), there are a few differences relative to Linux deployments you should keep in mind. For a detailed comparison of the differences between Windows and Linux in upstream Kubernetes, see [Windows containers in Kubernetes](https://kubernetes.io/docs/concepts/windows/intro/).

Some of the major differences include:

**Identity**: Windows Server uses a larger binary security identifier (SID) that's stored in the Windows Security Access Manager (SAM) database. This database isn't shared between the host and containers or between containers.**File permissions**: Windows Server uses an access control list based on SIDs rather than a bitmask of permissions and UID+GID.**File paths**: The convention on Windows Server is to use \ instead of /. In pod specs that mount volumes, specify the path correctly for Windows Server containers. For example, rather than a mount point of*/mnt/volume*in a Linux container, specify a drive letter and location such as*/K/Volume*to mount as the*K:*drive.

Note

[Windows Server 2019 retires on March 1, 2026](https://github.com/Azure/AKS/issues/4091). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2019 on any Kubernetes version. All existing node pools with Windows Server 2019 will be unsupported. Windows Server 2019 is not supported in Kubernetes version 1.33 and above. Starting on April 1, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail.[Windows Server 2022 retires on March 15, 2027](https://github.com/Azure/AKS/issues/4168). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2022 on any Kubernetes version. All existing node pools with Windows Server 2022 will be unsupported. Windows Server 2022 is not supported in Kubernetes version 1.36 and above. Starting on April 1, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail.

For more information, see [AKS release notes](https://github.com/Azure/AKS/releases). To stay up to date on the latest Windows Server OS versions and learn more about our roadmap of what's planned for support on AKS, see our [AKS public roadmap](https://github.com/azure/aks/projects/1).

This article covers important considerations to keep in mind when using Windows containers instead of Linux containers in Kubernetes. For an in-depth comparison of Windows and Linux containers, see [Comparison with Linux](https://kubernetes.io/docs/concepts/windows/intro/#compatibility-linux-similarities).

## Considerations

| Feature | Windows considerations |
|---|---|
|

*must*be Linux.• The maximum number of nodes per cluster is 5000.

• The Windows Server node pool name has a limit of six characters.

[Privileged containers](use-windows-hpc#limitations)**HostProcess Containers (HPC) containers**.[HPC containers](use-windows-hpc#limitations)[Create a Windows HostProcess pod](https://kubernetes.io/docs/tasks/configure-pod-container/create-hostprocess-pod/).[Azure Network Policy Manager (Azure)](use-network-policies#overview-of-network-policy)• Named ports

• SCTP protocol

• Negative match labels or namespace selectors (all labels except "debug=true")

• "except" CIDR blocks (a CIDR with exceptions)

• Windows Server 2019

[Node upgrade](manage-node-pools#upgrade-a-single-node-pool)[node image upgrade](node-image-upgrade). These upgrades deploy new nodes with the latest Window Server 2019 and Windows Server 2022 base node image and security patches.[AKS Image Cleaner](image-cleaner#limitations)[BYOCNI](use-byo-cni)[Open Service Mesh](open-service-mesh-about)[GPU](use-windows-gpu)[Multi-instance GPU](gpu-multi-instance)[Generation 2 VMs](generation-2-vms)[Custom node config](custom-node-configuration)•

[kubelet](custom-node-configuration#kubelet-configuration): Supported.• OS config: Not supported.

## Next steps

For more information on Windows containers, see the [Windows Server containers FAQ](windows-faq).


---

<!-- DOCUMENTO FUSIONADO: deploy-ray.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/deploy-ray -->

# Configure and deploy a Ray cluster on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you configure and deploy a Ray cluster on Azure Kubernetes Service (AKS) using KubeRay. You also learn how to use the Ray cluster to train a simple machine learning model and display the results on the Ray Dashboard.

This article provides two methods to deploy the Ray cluster on AKS:

: Use the[Non-interactive deployment](#deploy-the-ray-sample-non-interactively)`deploy.sh`

script in the GitHub repository to deploy the complete Ray sample non-interactively.: Follow the manual deployment steps to deploy the Ray sample to AKS.[Manual deployment](#manually-deploy-the-ray-sample)

## Prerequisites

- Review the
[Ray cluster on AKS overview](ray-overview)to understand the components and deployment process. - An Azure subscription. If you don't have an Azure subscription, you can create a free account
[here](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - The Azure CLI installed on your local machine. You can install it using the instructions in
[How to install the Azure CLI](/en-us/cli/azure/install-azure-cli). - The
[Azure Kubernetes Service Preview extension](/en-us/azure/aks/draft#install-the-aks-preview-azure-cli-extension)installed. [Helm](https://helm.sh/docs/intro/install/)installed.[Terraform client tools](https://developer.hashicorp.com/terraform/install)or[OpenTofu](https://opentofu.org/)installed. This article uses Terraform, but the modules used should be compatible with OpenTofu.

## Deploy the Ray sample non-interactively

If you want to deploy the complete Ray sample non-interactively, you can use the `deploy.sh`

script in the GitHub repository ([https://github.com/Azure-Samples/aks-ray-sample](https://github.com/Azure-Samples/aks-ray-sample)). This script completes the steps outlined in the [Ray deployment process section](ray-overview#ray-deployment-process).

Clone the GitHub repo locally and change to the root of the repo using the following commands:

`git clone https://github.com/Azure-Samples/aks-ray-sample cd aks-ray-sample`

Deploy the complete sample using the following commands:

`chmod +x deploy.sh ./deploy.sh`

Once the deployment completes, review the output of the logs and the resource group in the Azure portal to see the infrastructure that was created.


## Manually deploy the Ray sample

Fashion MNIST is a dataset of Zalando's article images consisting of a training set of 60,000 examples and a test set of 10,000 examples. Each example is a 28x28 grayscale image associated with a label from ten classes. In this guide, you train a simple PyTorch model on this dataset using the Ray cluster.

### Deploy the RayJob specification

To train the model, you need to submit a Ray Job specification to the KubeRay operator running on a private AKS cluster. The Ray Job specification is a YAML file that describes the resources required to run the job, including the Docker image, the command to run, and the number of workers to use.

Looking at the Ray Job description, you might need to modify some fields to match your environment:

- The
`replicas`

field under the`workerGroupSpecs`

section in`rayClusterSpec`

specifies the number of worker pods that KubeRay schedules to the Kubernetes cluster. Each worker pod requires*3 CPUs*and*4 GB of memory*. The head pod requires*1 CPU*and*4 GB of memory*. Setting the`replicas`

field to*2*requires*8 vCPUs*in the node pool used to implement the RayCluster for the job. - The
`NUM_WORKERS`

field under`runtimeEnvYAML`

in`spec`

specifies the number of Ray actors to launch. Each Ray actor must be serviced by a worker pod in the Kubernetes cluster, so this field must be less than or equal to the`replicas`

field. In this example, we set`NUM_WORKERS`

to*2*, which matches the`replicas`

field. - The
`CPUS_PER_WORKER`

field must be set to*less than or equal the number of CPUs allocated to each worker pod minus 1*. In this example, the CPU resource request per worker pod is*3*, so`CPUS_PER_WORKER`

is set to*2*.

To summarize, you need a total of *8 vCPUs* in the node pool to run the PyTorch model training job. Since we added a taint on the system node pool so that no user pods can be scheduled on it, we must create a new node pool with at least *8 vCPUs* to host the Ray cluster.

Download the Ray Job specification file using the following command:

`curl -LO https://raw.githubusercontent.com/ray-project/kuberay/master/ray-operator/config/samples/pytorch-mnist/ray-job.pytorch-mnist.yaml`

Make any necessary modifications to the Ray Job specification file.

Launch the PyTorch model training job using the

`kubectl apply`

command.`kubectl apply -n kuberay -f ray-job.pytorch-mnist.yaml`


### Verify the RayJob deployment

Verify that you have two worker pods and one head pod running in the namespace using the

`kubectl get pods`

command.`kubectl get pods -n kuberay`

Your output should look similar to the following example output:

`NAME READY STATUS RESTARTS AGE kuberay-operator-7d7998bcdb-9h8hx 1/1 Running 0 3d2h pytorch-mnist-raycluster-s7xd9-worker-small-group-knpgl 1/1 Running 0 6m15s pytorch-mnist-raycluster-s7xd9-worker-small-group-p74cm 1/1 Running 0 6m15s rayjob-pytorch-mnist-fc959 1/1 Running 0 5m35s rayjob-pytorch-mnist-raycluster-s7xd9-head-l24hn 1/1 Running 0 6m15s`

Check the status of the RayJob using the

`kubectl get`

command.`kubectl get rayjob -n kuberay`

Your output should look similar to the following example output:

`NAME JOB STATUS DEPLOYMENT STATUS START TIME END TIME AGE rayjob-pytorch-mnist RUNNING Running 2024-11-22T03:08:22Z 9m36s`

Wait until the RayJob completes. This might take a few minutes. Once the

`JOB STATUS`

is`SUCCEEDED`

, you can check the training logs. You can do this by first getting the name of the pod running the RayJob using the`kubectl get pods`

command.`kubectl get pods -n kuberay`

In the output, you should see a pod with a name that starts with

`rayjob-pytorch-mnist`

, similar to the following example output:`NAME READY STATUS RESTARTS AGE kuberay-operator-7d7998bcdb-9h8hx 1/1 Running 0 3d2h pytorch-mnist-raycluster-s7xd9-worker-small-group-knpgl 1/1 Running 0 14m pytorch-mnist-raycluster-s7xd9-worker-small-group-p74cm 1/1 Running 0 14m rayjob-pytorch-mnist-fc959 0/1 Completed 0 13m rayjob-pytorch-mnist-raycluster-s7xd9-head-l24hn 1/1 Running 0 14m`

View the logs of the RayJob using the

`kubectl logs`

command. Make sure to replace`rayjob-pytorch-mnist-fc959`

with the name of the pod running your RayJob.`kubectl logs -n kuberay rayjob-pytorch-mnist-fc959`

In the output, you should see the training logs for the PyTorch model, similar to the following example output:

`2024-11-21 19:09:04,986 INFO cli.py:39 -- Job submission server address: http://rayjob-pytorch-mnist-raycluster-s7xd9-head-svc.kuberay.svc.cluster.local:8265 2024-11-21 19:09:05,712 SUCC cli.py:63 -- ------------------------------------------------------- 2024-11-21 19:09:05,713 SUCC cli.py:64 -- Job 'rayjob-pytorch-mnist-hndpx' submitted successfully 2024-11-21 19:09:05,713 SUCC cli.py:65 -- ------------------------------------------------------- 2024-11-21 19:09:05,713 INFO cli.py:289 -- Next steps 2024-11-21 19:09:05,713 INFO cli.py:290 -- Query the logs of the job: 2024-11-21 19:09:05,713 INFO cli.py:292 -- ray job logs rayjob-pytorch-mnist-hndpx 2024-11-21 19:09:05,713 INFO cli.py:294 -- Query the status of the job: ... View detailed results here: /home/ray/ray_results/TorchTrainer_2024-11-21_19-11-23 To visualize your results with TensorBoard, run: `tensorboard --logdir /tmp/ray/session_2024-11-21_19-08-24_556164_1/artifacts/2024-11-21_19-11-24/TorchTrainer_2024-11-21_19-11-23/driver_artifacts` Training started with configuration: ╭─────────────────────────────────────────────────╮ │ Training config │ ├─────────────────────────────────────────────────┤ │ train_loop_config/batch_size_per_worker 16 │ │ train_loop_config/epochs 10 │ │ train_loop_config/lr 0.001 │ ╰─────────────────────────────────────────────────╯ (RayTrainWorker pid=1193, ip=10.244.4.193) Setting up process group for: env:// [rank=0, world_size=2] (TorchTrainer pid=1138, ip=10.244.4.193) Started distributed worker processes: (TorchTrainer pid=1138, ip=10.244.4.193) - (node_id=3ea81f12c0f73ebfbd5b46664e29ced00266e69355c699970e1d824b, ip=10.244.4.193, pid=1193) world_rank=0, local_rank=0, node_rank=0 (TorchTrainer pid=1138, ip=10.244.4.193) - (node_id=2b00ea2b369c9d27de9596ce329daad1d24626b149975cf23cd10ea3, ip=10.244.1.42, pid=1341) world_rank=1, local_rank=0, node_rank=1 (RayTrainWorker pid=1341, ip=10.244.1.42) Downloading http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/train-images-idx3-ubyte.gz (RayTrainWorker pid=1193, ip=10.244.4.193) Downloading http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/train-images-idx3-ubyte.gz to /home/ray/data/FashionMNIST/raw/train-images-idx3-ubyte.gz (RayTrainWorker pid=1193, ip=10.244.4.193) 0%| | 0.00/26.4M [00:00<?, ?B/s] (RayTrainWorker pid=1193, ip=10.244.4.193) 0%| | 65.5k/26.4M [00:00<01:13, 356kB/s] (RayTrainWorker pid=1193, ip=10.244.4.193) 100%|██████████| 26.4M/26.4M [00:01<00:00, 18.9MB/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Extracting /home/ray/data/FashionMNIST/raw/train-images-idx3-ubyte.gz to /home/ray/data/FashionMNIST/raw (RayTrainWorker pid=1341, ip=10.244.1.42) 100%|██████████| 26.4M/26.4M [00:01<00:00, 18.7MB/s] ... Training finished iteration 1 at 2024-11-21 19:15:46. Total running time: 4min 22s ╭───────────────────────────────╮ │ Training result │ ├───────────────────────────────┤ │ checkpoint_dir_name │ │ time_this_iter_s 144.9 │ │ time_total_s 144.9 │ │ training_iteration 1 │ │ accuracy 0.805 │ │ loss 0.52336 │ ╰───────────────────────────────╯ (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 0: 97%|█████████▋| 303/313 [00:01<00:00, 269.60it/s] Test Epoch 0: 100%|██████████| 313/313 [00:01<00:00, 267.14it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 1: 0%| | 0/1875 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 0: 100%|██████████| 313/313 [00:01<00:00, 270.44it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 0: 100%|█████████▉| 1866/1875 [00:24<00:00, 82.49it/s] [repeated 35x across cluster] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 0: 100%|██████████| 1875/1875 [00:24<00:00, 77.99it/s] Train Epoch 0: 100%|██████████| 1875/1875 [00:24<00:00, 76.19it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 0: 0%| | 0/313 [00:00<?, ?it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 0: 88%|████████▊ | 275/313 [00:01<00:00, 265.39it/s] [repeated 19x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 19%|█▉ | 354/1875 [00:04<00:18, 82.66it/s] [repeated 80x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 0%| | 0/1875 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 40%|████ | 757/1875 [00:09<00:13, 83.01it/s] [repeated 90x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 62%|██████▏ | 1164/1875 [00:14<00:08, 83.39it/s] [repeated 92x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 82%|████████▏ | 1533/1875 [00:19<00:05, 68.09it/s] [repeated 91x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 91%|█████████▏| 1713/1875 [00:22<00:02, 70.20it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 1: 91%|█████████ | 1707/1875 [00:22<00:02, 70.04it/s] [repeated 47x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 0%| | 0/313 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 8%|▊ | 24/313 [00:00<00:01, 237.98it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 1: 96%|█████████▋| 302/313 [00:01<00:00, 250.76it/s] Test Epoch 1: 100%|██████████| 313/313 [00:01<00:00, 262.94it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 2: 0%| | 0/1875 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 92%|█████████▏| 289/313 [00:01<00:00, 222.57it/s] Training finished iteration 2 at 2024-11-21 19:16:12. Total running time: 4min 48s ╭───────────────────────────────╮ │ Training result │ ├───────────────────────────────┤ │ checkpoint_dir_name │ │ time_this_iter_s 25.975 │ │ time_total_s 170.875 │ │ training_iteration 2 │ │ accuracy 0.828 │ │ loss 0.45946 │ ╰───────────────────────────────╯ (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 100%|██████████| 313/313 [00:01<00:00, 226.04it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 1: 100%|██████████| 1875/1875 [00:24<00:00, 76.24it/s] [repeated 45x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 2: 13%|█▎ | 239/1875 [00:03<00:24, 67.30it/s] [repeated 64x across cluster] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 1: 0%| | 0/313 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 85%|████████▍ | 266/313 [00:01<00:00, 222.54it/s] [repeated 20x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) .. Training completed after 10 iterations at 2024-11-21 19:19:47. Total running time: 8min 23s 2024-11-21 19:19:47,596 INFO tune.py:1009 -- Wrote the latest version of all result files and experiment state to '/home/ray/ray_results/TorchTrainer_2024-11-21_19-11-23' in 0.0029s. Training result: Result( metrics={'loss': 0.35892221605786073, 'accuracy': 0.872}, path='/home/ray/ray_results/TorchTrainer_2024-11-21_19-11-23/TorchTrainer_74867_00000_0_2024-11-21_19-11-24', filesystem='local', checkpoint=None ) (RayTrainWorker pid=1341, ip=10.244.1.42) Downloading http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/t10k-labels-idx1-ubyte.gz [repeated 7x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Downloading http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/t10k-labels-idx1-ubyte.gz to /home/ray/data/FashionMNIST/raw/t10k-labels-idx1-ubyte.gz [repeated 7x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Extracting /home/ray/data/FashionMNIST/raw/t10k-labels-idx1-ubyte.gz to /home/ray/data/FashionMNIST/raw [repeated 7x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 9: 91%|█████████ | 1708/1875 [00:21<00:01, 83.84it/s] [repeated 23x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 9: 100%|██████████| 1875/1875 [00:23<00:00, 78.52it/s] [repeated 37x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 9: 0%| | 0/313 [00:00<?, ?it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 9: 89%|████████▉ | 278/313 [00:01<00:00, 266.46it/s] [repeated 19x across cluster] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 9: 97%|█████████▋| 305/313 [00:01<00:00, 256.69it/s] Test Epoch 9: 100%|██████████| 313/313 [00:01<00:00, 267.35it/s] 2024-11-21 19:19:51,728 SUCC cli.py:63 -- ------------------------------------------ 2024-11-21 19:19:51,728 SUCC cli.py:64 -- Job 'rayjob-pytorch-mnist-hndpx' succeeded 2024-11-21 19:19:51,728 SUCC cli.py:65 -- ------------------------------------------`


## View training results on the Ray Dashboard

When the RayJob successfully completes, you can view the training results on the Ray Dashboard. The Ray Dashboard provides real-time monitoring and visualizations of Ray clusters. You can use the Ray Dashboard to monitor the status of Ray clusters, view logs, and visualize the results of machine learning jobs.

To access the Ray Dashboard, you need to expose the Ray head service to the public internet by creating a *service shim* to expose the Ray head service on port 80 instead of port 8265.

Note

The `deploy.sh`

described in the previous section automatically exposes the Ray head service to the public internet. The following steps are included in the `deploy.sh`

script.

Get the name of the Ray head service and save it in a shell variable using the following command:

`rayclusterhead=$(kubectl get service -n $kuberay_namespace | grep 'rayjob-pytorch-mnist-raycluster' | grep 'ClusterIP' | awk '{print $1}')`

Create the service shim to expose the Ray head service on port 80 using the

`kubectl expose service`

command.`kubectl expose service $rayclusterhead \ -n $kuberay_namespace \ --port=80 \ --target-port=8265 \ --type=NodePort \ --name=ray-dash`

Create the ingress to expose the service shim using the ingress controller using the following command:

`cat <<EOF | kubectl apply -f - apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: ray-dash namespace: kuberay annotations: nginx.ingress.kubernetes.io/rewrite-target: / spec: ingressClassName: webapprouting.kubernetes.azure.com rules: - http: paths: - backend: service: name: ray-dash port: number: 80 path: / pathType: Prefix EOF`

Get the public IP address of the ingress controller using the

`kubectl get service`

command.`kubectl get service -n app-routing-system`

In the output, you should see the public IP address of the load balancer attached to the ingress controller. Copy the public IP address and paste it into a web browser. You should see the Ray Dashboard.


## Clean up resources

To clean up the resources created in this guide, you can delete the Azure resource group that contains the AKS cluster.

## Next steps

To learn more about AI and machine learning workloads on AKS, see the following articles:

[Deploy an application that uses OpenAI on Azure Kubernetes Service (AKS)](open-ai-quickstart)[Build and deploy data and machine learning pipelines with Flyte on Azure Kubernetes Service (AKS)](use-flyte)[Deploy an AI model on Azure Kubernetes Service (AKS) with the AI toolchain operator](ai-toolchain-operator)

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Russell de Pina | Principal TPM
- Ken Kilty | Principal TPM
- Erin Schaffer | Content Developer 2
- Adrian Joian | Principal Customer Engineer
- Ryan Graham | Principal Technical Specialist


---

<!-- DOCUMENTO FUSIONADO: __tutorial-kubernetes-deploy-azure-container-storage_static-ip__istio-deploy-add_c939ee.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _tutorial-kubernetes-deploy-azure-container-storage_static-ip.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: tutorial-kubernetes-deploy-azure-container-storage.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-azure-container-storage -->

# Tutorial - Deploy Azure Container Storage (version 1.x.x) on an AKS cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This tutorial introduces Azure Container Storage and demonstrates how to deploy and manage container-native storage for applications running on Azure Kubernetes Service (AKS). If you don't want to deploy Azure Container Storage now, you can skip this tutorial and proceed directly to [Deploy an application in AKS](tutorial-kubernetes-deploy-application). You won't need Azure Container Storage for the basic storefront application in this tutorial series.

Important

This article explains how to install Azure Container Storage (version 1.x.x), which now explicitly requires a version pinning parameter `--container-storage-version 1`

for installation. [Azure Container Storage (version 2.x.x)](/en-us/azure/storage/container-storage/container-storage-introduction) is now available.

Azure Container Storage simplifies the management of stateful applications in Kubernetes by offering container-native storage tailored to a variety of workloads, including databases, analytics platforms, and high-performance applications.

By the end of this tutorial, you will:

- Understand how Azure Container Storage supports diverse workloads in Kubernetes.
- Explore multiple storage backend options to tailor storage to your application's needs.
- Deploy Azure Container Storage (version 1.x.x) on your AKS cluster and create a generic ephemeral volume.

## Before you begin

In previous tutorials, you created a container image, uploaded it to an ACR instance, and created an AKS cluster. Start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app) to follow along.

- This tutorial requires using the Azure CLI version 2.35.0 or later. Portal and PowerShell aren't currently supported for Azure Container Storage. Check your version with
`az --version`

. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). If you're using the Bash environment in Azure Cloud Shell, the latest version is already installed. - You must have an existing Linux-based AKS cluster with at least 3 nodes with
[Storage optimized VM SKUs](/en-us/azure/virtual-machines/sizes/overview#storage-optimized)or[GPU accelerated VM SKUs](/en-us/azure/virtual-machines/sizes/overview#gpu-accelerated). See[Tutorial 3 - Create an AKS cluster](tutorial-kubernetes-deploy-cluster). - You'll need the Kubernetes command-line client,
`kubectl`

. It's already installed if you're using Azure Cloud Shell, or you can install it locally by running the`az aks install-cli`

command.

## Install the Kubernetes extension

Add or upgrade to the latest version of `k8s-extension`

by running the following command.

```
az extension add --upgrade --name k8s-extension
```


## Connect to the cluster and check node status

If you're not already connected to your cluster from the previous tutorial, run the following commands. If you're already connected, you can skip this section.

Run the following command to connect to the cluster.

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using the

`kubectl get`

command. This command returns a list of the cluster nodes.`kubectl get nodes`

The following output example shows the nodes in your cluster. Make sure the status for all nodes shows

*Ready*:`NAME STATUS ROLES AGE VERSION aks-nodepool1-34832848-vmss000000 Ready agent 80m v1.30.9 aks-nodepool1-34832848-vmss000001 Ready agent 80m v1.30.9 aks-nodepool1-34832848-vmss000002 Ready agent 80m v1.30.9`


## Choose a backing storage option

Azure Container Storage (version 1.x.x) uses storage pools to provision and manage persistent and generic volumes. It offers a variety of back-end storage options for your storage pools, each suited for specific workloads. Selecting the right storage type is critical for optimizing workload performance, durability, and cost efficiency. For this tutorial, we'll use Ephemeral Disk with local NVMe as backing storage to create a generic ephemeral volume. However, we'll also explore the other backing storage options that allow you to create persistent volumes.

### Ephemeral Disk

Ephemeral Disk utilizes local storage resources on the AKS nodes (either local NVMe or temp SSD). It offers low sub-ms latency and high IOPS, but no data persistence if the VM restarts. Ephemeral Disk is best suited for applications such as Cassandra that prioritize speed over persistence, and is ideal for workloads with their own application-level replication.

You can use Ephemeral Disk to create either generic ephemeral volumes or persistent volumes, even though the data will be lost if the VM restarts.

### Azure Disks

Ideal for databases like PostgreSQL and MongoDB, Azure Disks offer durability, scalability, and multi-tiered performance options, including Premium SSD and Ultra SSD.

Azure Disks allow for automatic provisioning of storage volumes and include built-in redundancy and high availability.

### Azure Elastic SAN (preview)

Designed for shared storage needs and general-purpose databases requiring scalability and high availability, Azure Elastic SAN is a good fit for workloads such as CI/CD pipelines or large-scale data processing.

## Enable Azure Container Storage (version 1.x.x) and create a storage pool

Run the following command to install Azure Container Storage on the cluster and create a Local NVMe storage pool.

```
az aks update -n myAKSCluster -g myResourceGroup --enable-azure-container-storage ephemeralDisk --container-storage-version 1 --storage-pool-option NVMe
```


The deployment should take less than 15 minutes.

### Verify the storage pool status

When deployment completes, the components for your chosen storage pool type will be enabled, and you'll have a default storage pool.

To get the list of available storage pools, run the following command:

```
kubectl get sp -n acstor
```


To check the status of a storage pool, run the following command:

```
kubectl describe sp <storage-pool-name> -n acstor
```


If the `Message`

doesn't say `StoragePool is ready`

, then your storage pool is still creating or ran into a problem.

## Display the available storage classes

When the storage pool is ready to use, you must select a storage class to define how storage is dynamically created when creating and deploying volumes.

Run `kubectl get sc`

to display the available storage classes. You should see a storage class called `acstor-<storage-pool-name>`

. Use this storage class in the next section to deploy a pod.

## Deploy a pod with a generic ephemeral volume

Create a pod using [Fio](https://github.com/axboe/fio) (Flexible I/O Tester) for benchmarking and workload simulation, that uses a generic ephemeral volume.

Use your favorite text editor to create a YAML manifest file such as

`code acstor-pod.yaml`

.Paste in the following code and save the file.

`kind: Pod apiVersion: v1 metadata: name: fiopod spec: nodeSelector: acstor.azure.com/io-engine: acstor containers: - name: fio image: nixery.dev/shell/fio args: - sleep - "1000000" volumeMounts: - mountPath: "/volume" name: ephemeralvolume volumes: - name: ephemeralvolume ephemeral: volumeClaimTemplate: metadata: labels: type: my-ephemeral-volume spec: accessModes: [ "ReadWriteOnce" ] storageClassName: acstor-ephemeraldisk-nvme # replace with the name of your storage class if different resources: requests: storage: 1Gi`

If you change the storage size of the volume, make sure the size is less than the available capacity of a single node's ephemeral disk. Run

`kubectl get diskpool -n acstor`

to check the available capacity.Apply the YAML manifest file to deploy the pod.

`kubectl apply -f acstor-pod.yaml`

You should see output similar to the following:

`pod/fiopod created`

Check that the pod is running and that the ephemeral volume claim has been bound successfully to the pod:

`kubectl describe pod fiopod kubectl describe pvc fiopod-ephemeralvolume`


You've now deployed a pod that's using local NVMe as its storage, and you can use it for your Kubernetes workloads.

Verify the available capacity of ephemeral disks before provisioning additional volumes:

```
kubectl describe node <node-name>
```


To learn more about Azure Container Storage (version 1.x.x), including how to create persistent volumes, see [What is Azure Container Storage?](/en-us/azure/storage/container-storage/container-storage-introduction-version-1)

## Clean up resources

You won't need Azure Container Storage for the rest of this tutorial series, so we recommend deleting it now to avoid incurring unnecessary Azure charges.

Delete the pod.

`kubectl delete pod fiopod`

Delete the storage pool.

`kubectl delete sp -n acstor <storage-pool-name>`

Delete the extension instance.

`az aks update -n myAKSCluster -g myResourceGroup --disable-azure-container-storage all`


## Next step

In this tutorial, you deployed Azure Container Storage (version 1.x.x) on your AKS cluster. You learned how to:

- Enable Azure Container Storage (version 1.x.x) on your AKS cluster.
- Choose a backing storage type and create a storage pool.
- Deploy a pod with a generic ephemeral volume.

In the next tutorial, you learn how to deploy an application to your cluster.


---

<!-- DOCUMENTO FUSIONADO: static-ip.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/static-ip -->

# Use a static public IP address and DNS label with the Azure Kubernetes Service (AKS) load balancer

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create a load balancer resource in an Azure Kubernetes Service (AKS) cluster, the public IP address assigned to it is only valid for the lifespan of that resource. If you delete the Kubernetes service, the associated load balancer and IP address are also deleted. If you want to assign a specific IP address or retain an IP address for redeployed Kubernetes services, you can create and use a static public IP address.

This article shows you how to create a static public IP address and assign it to your Kubernetes service.

## Before you begin

- You need the Azure CLI version 2.0.59 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - This article covers using a
*Standard*SKU IP with a*Standard*SKU load balancer. For more information, see[IP address types and allocation methods in Azure](/en-us/azure/virtual-network/ip-services/public-ip-addresses#sku).

## Create an AKS cluster

Create an Azure resource group using the

command.`az group create`

`az group create --name myNetworkResourceGroup --location eastus`

Create an AKS cluster using the

command.`az aks create`

`az aks create --name myAKSCluster --resource-group myNetworkResourceGroup --generate-ssh-keys`


## Create a static IP address

Get the name of the node resource group using the

command and query for the`az aks show`

`nodeResourceGroup`

property.`az aks show --name myAKSCluster --resource-group myNetworkResourceGroup --query nodeResourceGroup -o tsv`

Create a static public IP address in the node resource group using the

command.`az network public ip create`

`az network public-ip create \ --resource-group <node resource group name> \ --name myAKSPublicIP \ --sku Standard \ --allocation-method static`

Note

If you're using a

*Basic*SKU load balancer in your AKS cluster, use*Basic*for the`--sku`

parameter when defining a public IP. Only*Basic*SKU IPs work with the*Basic*SKU load balancer and only*Standard*SKU IPs work with*Standard*SKU load balancers.Get the static public IP address using the

command. Specify the name of the node resource group and public IP address you created, and query for the`az network public-ip list`

`ipAddress`

.`az network public-ip show --resource-group <node resource group name> --name myAKSPublicIP --query ipAddress --output tsv`


## Create a service using the static IP address

First, determine which type of managed identity your AKS cluster is using, system-assigned or user-assigned. If you're not certain, call the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the identity's*type*property.`az aks show \ --name myAKSCluster \ --resource-group myResourceGroup \ --query identity.type \ --output tsv`

If the cluster is using a managed identity, the value of the

*type*property will be either**SystemAssigned**or**UserAssigned**.If the cluster is using a service principal, the value of the

*type*property will be null. Consider upgrading your cluster to use a managed identity.If your AKS cluster uses a system-assigned managed identity, then query for the managed identity's principal ID as follows:

`# Get the principal ID for a system-assigned managed identity. CLIENT_ID=$(az aks show \ --name myAKSCluster \ --resource-group myNetworkResourceGroup \ --query identity.principalId \ --output tsv)`

If your AKS cluster uses a user-assigned managed identity, then the principal ID will be null. Query for the user-assigned managed identity's client ID instead:

`# Get the client ID for a user-assigned managed identity. CLIENT_ID=$(az aks show \ --name myAKSCluster \ --resource-group myNetworkResourceGroup \ --query identity.userAssignedIdentities.*.clientId \ --output tsv`

Assign delegated permissions for the managed identity used by the AKS cluster for the public IP's resource group by calling the

command.`az role assignment create`

`# Get the resource ID for the node resource group. RG_SCOPE=$(az group show \ --name <node resource group> \ --query id \ --output tsv) # Assign the Network Contributor role to the managed identity, # scoped to the node resource group. az role assignment create \ --assignee ${CLIENT_ID} \ --role "Network Contributor" \ --scope ${RG_SCOPE}`

Important

If you customized your outbound IP, make sure your cluster identity has permissions to both the outbound public IP and the inbound public IP.

Create a file named

`load-balancer-service.yaml`

and copy in the contents of the following YAML file, providing your own public IP address created in the previous step and the node resource group name.Important

Adding the

`loadBalancerIP`

property to the load balancer YAML manifest is deprecating following[upstream Kubernetes](https://github.com/kubernetes/kubernetes/pull/107235). While current usage remains the same and existing services are expected to work without modification, we**highly recommend setting service annotations**instead. To set service annotations, you can either use`service.beta.kubernetes.io/azure-pip-name`

for public IP name, or use`service.beta.kubernetes.io/azure-load-balancer-ipv4`

for an IPv4 address and`service.beta.kubernetes.io/azure-load-balancer-ipv6`

for an IPv6 address, as shown in the example YAML.`apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-load-balancer-resource-group: <node resource group name> service.beta.kubernetes.io/azure-pip-name: myAKSPublicIP name: azure-load-balancer spec: type: LoadBalancer ports: - port: 80 selector: app: azure-load-balancer`

Note

Adding the

`service.beta.kubernetes.io/azure-pip-name`

annotation ensures the most efficient LoadBalancer creation and is highly recommended to avoid potential throttling.Set a public-facing DNS label to the service using the

`service.beta.kubernetes.io/azure-dns-label-name`

service annotation. This publishes a fully qualified domain name (FQDN) for your service using Azure's public DNS servers and top-level domain. The annotation value must be unique within the Azure location, so we recommend you use a sufficiently qualified label. Azure automatically appends a default suffix in the location you selected, such as`<location>.cloudapp.azure.com`

, to the name you provide, creating the FQDN.Note

If you want to publish the service on your own domain, see

[Azure DNS](https://azure.microsoft.com/services/dns/)and the[external-dns](https://github.com/kubernetes-sigs/external-dns)project.`apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-load-balancer-resource-group: <node resource group name> service.beta.kubernetes.io/azure-pip-name: myAKSPublicIP service.beta.kubernetes.io/azure-dns-label-name: <unique-service-label> name: azure-load-balancer spec: type: LoadBalancer ports: - port: 80 selector: app: azure-load-balancer`

Create the service and deployment using the

`kubectl apply`

command.`kubectl apply -f load-balancer-service.yaml`

To see the DNS label for your load balancer, use the

`kubectl describe service`

command.`kubectl describe service azure-load-balancer`

The DNS label will be listed under the

`Annotations`

, as shown in the following condensed example output:`Name: azure-load-balancer Namespace: default Labels: <none> Annotations: service.beta.kuberenetes.io/azure-dns-label-name: <unique-service-label>`


## Troubleshoot

If the static IP address defined in the `loadBalancerIP`

property of the Kubernetes service manifest doesn't exist or hasn't been created in the node resource group and there are no other delegations configured, the load balancer service creation fails. To troubleshoot, review the service creation events using the [ kubectl describe](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#describe) command. Provide the name of the service specified in the YAML manifest, as shown in the following example:

```
kubectl describe service azure-load-balancer
```


The output shows you information about the Kubernetes service resource. The following example output shows a `Warning`

in the `Events`

: "`user supplied IP address was not found`

." In this scenario, make sure you created the static public IP address in the node resource group and that the IP address specified in the Kubernetes service manifest is correct.

```
Name: azure-load-balancer
Namespace: default
Labels: <none>
Annotations: <none>
Selector: app=azure-load-balancer
Type: LoadBalancer
IP: 10.0.18.125
IP: 40.121.183.52
Port: <unset> 80/TCP
TargetPort: 80/TCP
NodePort: <unset> 32582/TCP
Endpoints: <none>
Session Affinity: None
External Traffic Policy: Cluster
Events:
Type Reason Age From Message
---- ------ ---- ---- -------
Normal CreatingLoadBalancer 7s (x2 over 22s) service-controller Creating load balancer
Warning CreatingLoadBalancerFailed 6s (x2 over 12s) service-controller Error creating load balancer (will retry): Failed to create load balancer for service default/azure-load-balancer: user supplied IP Address 40.121.183.52 was not found
```


## Next steps

For more control over the network traffic to your applications, use the application routing addon for AKS. For more information about the app routing addon, see [Managed NGINX ingress with the application routing add-on](app-routing).


---

<!-- DOCUMENTO FUSIONADO: _istio-deploy-addon__azure-cni-overlay-pod-expand__aks-extension-vs-code_kms-obs_b58605.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: istio-deploy-addon.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-deploy-addon -->

# Deploy Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to install the Istio-based service mesh add-on for Azure Kubernetes Service (AKS) cluster.

For more information on Istio and the service mesh add-on, see [Istio-based service mesh add-on for Azure Kubernetes Service](istio-about).

Tip

You can use Azure Copilot to help deploy Istio to your AKS clusters in the Azure portal. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#install-and-work-with-istio).

## Before you begin

The add-on requires Azure CLI version 2.57.0 or later installed. You can run

`az --version`

to verify version. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).To find information about which Istio add-on revisions are available in a region and their compatibility with AKS standard and LTS cluster versions, use the command

:`az aks mesh get-revisions`

`az aks mesh get-revisions --location <location> -o table`

For more information on the Istio add-on's compatibility with AKS, refer to the

[compatibility support policy](istio-support-policy#aks-compatibility).In some cases, Istio CRDs from previous installations may not be automatically cleaned up on uninstall. Ensure existing Istio CRDs are deleted:

`kubectl delete crd $(kubectl get crd -A | grep "istio.io" | awk '{print $1}')`

It is recommended to also clean up other resources from self-managed installations of Istio such as ClusterRoles, MutatingWebhookConfigurations and ValidatingWebhookConfigurations.

Note that if you choose to use any

`istioctl`

CLI commands, you will need to include a flag to point to the add-on installation of Istio:`--istioNamespace aks-istio-system`


### Set environment variables

```
export CLUSTER=<cluster-name>
export RESOURCE_GROUP=<resource-group-name>
export LOCATION=<location>
```


## Install Istio add-on

This section includes steps to install the Istio add-on during cluster creation or enable for an existing cluster using the Azure CLI. If you want to install the add-on using Bicep, see the guide for [installing an AKS cluster with the Istio service mesh add-on using Bicep](https://github.com/Azure-Samples/aks-istio-addon-bicep). To learn more about the Bicep resource definition for an AKS cluster, see [Bicep managedCluster reference](/en-us/azure/templates/microsoft.containerservice/managedclusters).

Note

If you need the `istiod`

and ingress/egress gateway pods scheduled onto particular nodes, you can use [AKS system nodes](/en-us/azure/aks/use-system-pools) or the `azureservicemesh/istio.replica.preferred`

node label. The pods have node affinities with a weighted preference of `100`

for AKS system nodes (labeled `kubernetes.azure.com/mode: system`

), and a weighted preference of `50`

for nodes labeled `azureservicemesh/istio.replica.preferred: true`

.

### Revision selection

If you enable the add-on without specifying a revision, a default supported revision is installed for you.

To specify a revision, perform the following steps.

- Use the
command to check which revisions are available for different AKS cluster versions in a region.`az aks mesh get-revisions`

- Based on the available revisions, you can include the
`--revision asm-X-Y`

(ex:`--revision asm-1-24`

) flag in the enable command you use for mesh installation.

### Install mesh during cluster creation

To install the Istio add-on when creating the cluster, use the `--enable-azure-service-mesh`

or`--enable-asm`

parameter.

```
az group create --name ${RESOURCE_GROUP} --location ${LOCATION}
az aks create \
--resource-group ${RESOURCE_GROUP} \
--name ${CLUSTER} \
--enable-asm \
--generate-ssh-keys
```


### Install mesh for existing cluster

The following example enables Istio add-on for an existing AKS cluster:

Important

You can't enable the Istio add-on on an existing cluster if an OSM add-on is already on your cluster. Uninstall the OSM add-on before installing the Istio add-on.
For more information, see [uninstall the OSM add-on from your AKS cluster](open-service-mesh-uninstall-add-on).
Istio add-on can only be enabled on AKS clusters of version >= 1.23.

```
az aks mesh enable --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


## Verify successful installation

To verify the Istio add-on is installed on your cluster, run the following command:

```
az aks show --resource-group ${RESOURCE_GROUP} --name ${CLUSTER} --query 'serviceMeshProfile.mode'
```


Confirm the output shows `Istio`

.

Use `az aks get-credentials`

to get the credentials for your AKS cluster:

```
az aks get-credentials --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


Use `kubectl`

to verify that `istiod`

(Istio control plane) pods are running successfully:

```
kubectl get pods -n aks-istio-system
```


Confirm the `istiod`

pod has a status of `Running`

. For example:

```
NAME READY STATUS RESTARTS AGE
istiod-asm-1-24-74f7f7c46c-xfdtl 1/1 Running 0 2m
istiod-asm-1-24-74f7f7c46c-4nt2v 1/1 Running 0 2m
```


## Enable sidecar injection

To automatically install sidecar to any new pods, you need to annotate your namespaces with the revision label corresponding to the control plane revision currently installed.

If you're unsure which revision is installed, use:

```
az aks show --resource-group ${RESOURCE_GROUP} --name ${CLUSTER} --query 'serviceMeshProfile.istio.revisions'
```


Apply the revision label:

```
kubectl label namespace default istio.io/rev=asm-X-Y
```


Important

Explicit versioning matching the control plane revision (ex: `istio.io/rev=asm-1-24`

) is required.

The default `istio-injection=enabled`

label will not work and will **cause the sidecar injection to skip the namespace** for the add-on.

For manual injection of sidecar using `istioctl kube-inject`

, you need to specify extra parameters for `istioNamespace`

(`-i`

) and `revision`

(`-r`

). For example:

```
kubectl apply -f <(istioctl kube-inject -f sample.yaml -i aks-istio-system -r asm-X-Y) -n foo
```


## Trigger sidecar injection

You can either deploy the sample application provided for testing, or trigger sidecar injection for existing workloads.

### Existing applications

If you have existing applications to be added to the mesh, ensure their namespaces are labeled as in the previous step, and then restart their deployments to trigger sidecar injection:

```
kubectl rollout restart -n <namespace> <deployment name>
```


Verify that sidecar injection succeeded by ensuring all containers are ready and looking for the `istio-proxy`

container in the `kubectl describe`

output, for example:

```
kubectl describe pod -n namespace <pod name>
```


The `istio-proxy`

container is the Envoy sidecar. Your application is now part of the data plane.

### Deploy sample application

Use `kubectl apply`

to deploy the sample application on the cluster:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.24/samples/bookinfo/platform/kube/bookinfo.yaml
```


Note

Clusters using an HTTP proxy for outbound internet access will need to set up a Service Entry. For setup instructions see [HTTP proxy support in Azure Kubernetes Service](http-proxy)

Confirm several deployments and services are created on your cluster. For example:

```
service/details created
serviceaccount/bookinfo-details created
deployment.apps/details-v1 created
service/ratings created
serviceaccount/bookinfo-ratings created
deployment.apps/ratings-v1 created
service/reviews created
serviceaccount/bookinfo-reviews created
deployment.apps/reviews-v1 created
deployment.apps/reviews-v2 created
deployment.apps/reviews-v3 created
service/productpage created
serviceaccount/bookinfo-productpage created
deployment.apps/productpage-v1 created
```


Use `kubectl get services`

to verify that the services were created successfully:

```
kubectl get services
```


Confirm the following services were deployed:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
details ClusterIP 10.0.180.193 <none> 9080/TCP 87s
kubernetes ClusterIP 10.0.0.1 <none> 443/TCP 15m
productpage ClusterIP 10.0.112.238 <none> 9080/TCP 86s
ratings ClusterIP 10.0.15.201 <none> 9080/TCP 86s
reviews ClusterIP 10.0.73.95 <none> 9080/TCP 86s
```


```
kubectl get pods
```


```
NAME READY STATUS RESTARTS AGE
details-v1-558b8b4b76-2llld 2/2 Running 0 2m41s
productpage-v1-6987489c74-lpkgl 2/2 Running 0 2m40s
ratings-v1-7dc98c7588-vzftc 2/2 Running 0 2m41s
reviews-v1-7f99cc4496-gdxfn 2/2 Running 0 2m41s
reviews-v2-7d79d5bd5d-8zzqd 2/2 Running 0 2m41s
reviews-v3-7dbcdcbc56-m8dph 2/2 Running 0 2m41s
```


Confirm that all the pods have status of `Running`

with two containers in the `READY`

column. The second container (`istio-proxy`

) added to each pod is the Envoy sidecar injected by Istio, and the other is the application container.

To test this sample application against ingress, check out [next-steps](#next-steps).

## Next steps

[Deploy external or internal ingresses for Istio service mesh add-on](istio-deploy-ingress)[Scale istiod and ingress gateway HPA](istio-scale#scaling)[Collect metrics for Istio service mesh add-on workloads in Azure Managed Prometheus](istio-metrics-managed-prometheus)[Deploy egress gateways for the Istio service mesh add-on](istio-deploy-egress)[Enable Istio CNI for Istio service mesh add-on (Preview)](istio-cni)


---

<!-- DOCUMENTO FUSIONADO: _azure-cni-overlay-pod-expand__aks-extension-vs-code_kms-observability.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: azure-cni-overlay-pod-expand.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-cni-overlay-pod-expand -->

# Expand pod CIDR space in Azure CNI Overlay Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can expand your pod Classless Inter-Domain Routing (CIDR) space on Azure CNI Overlay clusters in Azure Kubernetes Service with Linux nodes only. The operation uses the [ az aks update](/en-us/cli/azure/aks#az_aks_update) command and allows expansions without the need to re-create your AKS cluster.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Requirements and parameters

| Requirement or parameter | Supported versions or values | Description |
|---|---|---|
| Feature flag | `EnableAzureCNIOverlayPodCIDRExpansion` |
This feature flag must be registered in your subscription to enable pod CIDR expansion in Azure CNI Overlay AKS clusters. |
| Azure CLI version | 2.48.0 or later | The Azure CLI version must be 2.48.0 or later to support the pod CIDR expansion feature. |
| Kubernetes version | 1.33 | Pod CIDR expansion is supported only on AKS clusters running Kubernetes version 1.33. |
| Node operating system | Linux | Pod CIDR expansion is supported only on Azure CNI Overlay AKS clusters with Linux nodes. |
| Networking mode | Azure CNI Overlay | Pod CIDR expansion is supported only on AKS clusters that use Azure CNI Overlay networking. |
| Example original pod CIDR | `10.244.0.0/18` |
This is an example of a starting pod CIDR block. |
| Example expanded pod CIDR | `10.244.0.0/16` |
This is an example of a target expanded pod CIDR block. |

## Limitations

- Windows nodes and hybrid node scenarios aren't supported.
- Shrinking or changing the pod CIDR isn't supported.
- Adding a discontinuous pod CIDR isn't supported. The new pod CIDR must be a larger superset that contains the complete original range.
- IPv6 pod CIDR expansion isn't supported.
- Changing multiple pod CIDR blocks via
`--pod-cidrs`

isn't supported. - If an
[Azure availability zone](availability-zones)is down during the expansion operation, new nodes might appear as`unready`

. You can expect these nodes to reconcile after the availability zone is up.

## Prerequisites

- You need an Azure subscription. If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/free/)before you begin. - Ensure that you meet the requirements listed in the
[Requirements and parameters](#requirements-and-parameters)section.

## Register the `EnableAzureCNIOverlayPodCIDRExpansion`

feature flag

Register the

`EnableAzureCNIOverlayPodCIDRExpansion`

feature flag by using thecommand:`az feature register`

`az feature register --namespace Microsoft.ContainerService --name EnableAzureCNIOverlayPodCIDRExpansion`

Verify successful registration by using the

command. It takes a few minutes for the registration to finish.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "EnableAzureCNIOverlayPodCIDRExpansion"`

After the feature shows

`Registered`

, refresh the registration of the`Microsoft.ContainerService`

resource provider by using thecommand:`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Update an Azure CNI Overlay AKS cluster to expand the pod CIDR space

Starting from a pod CIDR block of

`10.244.0.0/18`

, you can expand the pod CIDR space by using thecommand. For example:`az aks update`

`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --pod-cidr 10.244.0.0/16`

Note

Although the update operation might successfully finish and show the new pod CIDR in the network profile, be sure to validate the new cluster state through

`NodeNetworkConfig`

(`nnc`

).Verify the state of the upgrade operation by checking

`NodeNetworkConfig`

(`nnc`

) via the`kubectl get nnc`

command. In the output, all node pools should match your new pod CIDR block (for example,`10.244.0.0/16`

).`kubectl get nnc -A -o jsonpath='{range .items[*]}{.metadata.name}{" "}{.status.networkContainers[0].subnetAddressSpace}{"\n"}{end}'`


## Related content

To learn more about Azure CNI Overlay networking on AKS, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: _aks-extension-vs-code_kms-observability.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: aks-extension-vs-code.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/aks-extension-vs-code -->

# Use the Azure Kubernetes Service (AKS) extension for Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Kubernetes Service (AKS) extension for Visual Studio Code allows you to easily view and manage your AKS clusters from your development environment.

## Features

The Azure Kubernetes Service (AKS) extension for Visual Studio Code provides a rich set of features to help you manage your AKS clusters, including:

**Merge into Kubeconfig**: Merge your AKS cluster into your`kubeconfig`

file to manage your cluster from the command line.**Save Kubeconfig**: Save your AKS cluster configuration to a file.**AKS Diagnostics**: View diagnostics information based on your cluster's backend telemetry for identity, security, networking, node health, and create, upgrade, delete, and scale issues.**AKS Periscope**: Extract detailed diagnostic information and export it to an Azure storage account for further analysis.**Install Azure Service Operator (ASO)**: Deploy the latest version of ASO and provision Azure resources within Kubernetes.**Start or stop a cluster**: Start or stop your AKS cluster to save costs when you're not using it.

For more information, see [AKS extension for Visual Studio Code features](https://code.visualstudio.com/docs/azure/aksextensions#_features).

## Installation

- Open Visual Studio Code.
- In the
**Extensions**view, search for**Azure Kubernetes Service**. - Select the
**Azure Kubernetes Service**extension and then select**Install**.

For more information, see [Install the AKS extension for Visual Studio Code](https://code.visualstudio.com/docs/azure/aksextensions#_install-the-azure-kubernetes-services-extension).

## Next steps

To learn more about other AKS add-ons and extensions, see [Add-ons, extensions, and other integrations with AKS](integrations).


---

<!-- DOCUMENTO FUSIONADO: kms-observability.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/kms-observability -->

# Observability for Azure Kubernetes Service (AKS) clusters with Key Management Service (KMS) etcd encryption (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to view observability metrics and improve observability for AKS clusters with KMS etcd encryption.

## Prerequisites

- An AKS cluster with KMS etcd encryption enabled. For more information, see
[Add Key Management Service (KMS) etcd encryption to an Azure Kubernetes Service (AKS) cluster](use-kms-etcd-encryption). - You must enable
[diagnostic settings for the key vault to check the encryption logs](/en-us/azure/key-vault/general/howto-logging).

## Check the KMS config

Get the KMS config using the

command.`az aks show`

`az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query "securityProfile.azureKeyVaultKms"`

The output looks similar to the following example output:

`... "securityProfile": { "azureKeyVaultKms": { "enabled": true, "keyId": "https://<key-vault-name>.vault.azure.net/keys/<key-name>/<key-id>", "keyVaultNetworkAccess": "Public", "keyVaultResourceId": <key-vault-resource-id> ...`


## Diagnose and solve problems

Because the KMS plugin is a sidecar of `kube-apiserver`

pod, you can't access it directly. To improve the observability of KMS, you can check the KMS status using the Azure portal.

- In the Azure portal, navigate to your AKS cluster.
- From the service menu, select
**Diagnose and solve problems**. - In the search bar, search for
**KMS**and select**Azure KeyVault KMS Integration Issues**.

### Example problem

Let's say you see the following issue: `KeyExpired: Operation encrypt isn't allowed on an expired key`

.

Because the AKS KMS plugin currently only allows bring your own (BYO) key vault and key, it's your responsibility to manage the key lifecycle. If the key is expired, the KMS plugin fails to decrypt the existing secrets. To resolve this issue, you need to *extend the key expiration date* to make KMS work and *rotate the key version*.

## Next steps

For more information on using KMS with AKS, see the following articles:
