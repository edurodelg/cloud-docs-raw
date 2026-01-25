---
merged_at: 2026-01-25T12:25:33.870495
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: nvidia-gpu-operator.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/nvidia-gpu-operator -->

# Use NVIDIA GPU Operator on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The NVIDIA GPU Operator automates the management and deployment of all NVIDIA software components needed to provision GPU including driver installation, the [NVIDIA device plugin for Kubernetes](https://github.com/NVIDIA/k8s-device-plugin?tab=readme-ov-file), the NVIDIA container runtime, and more. Since the NVIDIA GPU Operator handles these components, it's not necessary to separately install the NVIDIA device plugin on your AKS cluster. This also means that the automatic GPU driver installation should be skipped in order to use the NVIDIA GPU Operator on AKS.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the Azure CLI version 2.72.2 or later installed to set the
`--gpu-driver`

field. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Note

GPU-enabled VMs contain specialized hardware subject to higher pricing and region availability. For more information, see the [pricing](free-standard-pricing-tiers) tool and [region availability](quotas-skus-regions).

## Limitations

- NVIDIA GPU Operator isn't supported for the following OS options: Windows Server versions,
[Flatcar Container Linux for AKS (preview)](flatcar-container-linux-for-aks), and[Azure Linux with OS Guard for AKS (preview)](use-azure-linux-os-guard).

## Get the credentials for your cluster

Get the credentials for your AKS cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. The following example command gets the credentials for the cluster

`myAKSCluster`

in the `myResourceGroup`

resource group:```
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```


Note

The NVIDIA GPU Operator is not compatible with multiple OS versions on the same AKS cluster.

Skip automatic GPU driver installation by creating an NVIDIA GPU-enabled node pool using the [

`az aks nodepool add`

][az-aks-nodepool-add] command and setting the API field`--gpu-driver`

to the value`none`

. Setting this API field to`none`

during node pool creation skips the default GPU driver installation, see[this example](gpu-cluster#skip-gpu-driver-installation). Any existing nodes aren't changed. You can scale the node pool to zero and then back up to make the change take effect.Follow the NVIDIA documentation to

[Install the GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html).Now that you successfully installed the GPU Operator, you can check that your

[GPUs are schedulable](gpu-cluster#confirm-that-gpus-are-schedulable)and[run a GPU workload](gpu-cluster#run-a-gpu-enabled-workload).

Note

There might be additional considerations to take when using the NVIDIA GPU Operator and deploying on SPOT instances. Please refer to [https://github.com/NVIDIA/gpu-operator/issues/577](https://github.com/NVIDIA/gpu-operator/issues/577)

## Next steps

[Monitor NVIDIA GPU metrics](monitor-gpu-metrics)using Azure Managed Prometheus and Azure Managed Grafana.- Learn more about
[Ray clusters on AKS](ray-overview).


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
