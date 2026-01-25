---
merged_at: 2026-01-25T12:25:33.932013
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-labels.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-labels -->

# Use labels in an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If you have multiple node pools, you may want to add a label during node pool creation. [Kubernetes labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) handle the scheduling rules for nodes. You can add labels to a node pool anytime and apply them to all nodes in the node pool.

In this how-to guide, you learn how to use labels in an Azure Kubernetes Service (AKS) cluster.

## Prerequisites

You need the Azure CLI version 2.2.0 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create an AKS cluster with a label

You can create an AKS cluster with node labels to set key/value metadata for workload scheduling.

```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="myResourceGroup$RANDOM_SUFFIX"
export AKS_CLUSTER_NAME="myAKSCluster$RANDOM_SUFFIX"
az group create --name $RESOURCE_GROUP --location $REGION
```


Results:

```
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx",
"location": "eastus2",
"managedBy": null,
"name": "myResourceGroupxxx",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null,
"type": "Microsoft.Resources/resourceGroups"
}
```


Create the AKS cluster specifying node labels (e.g., dept=IT, costcenter=9000):

```
az aks create \
--resource-group $RESOURCE_GROUP \
--name $AKS_CLUSTER_NAME \
--node-count 2 \
--nodepool-labels dept=IT costcenter=9000 \
--generate-ssh-keys --location $REGION
```


Results:

```
{
"aadProfile": null,
"addonProfiles": {},
"agentPoolProfiles": [
{
"count": 2,
"enableAutoScaling": null,
"mode": "System",
"name": "nodepool1",
"nodeLabels": {
"costcenter": "9000",
"dept": "IT"
}
}
],
"dnsPrefix": "myaksclusterxxx-dns",
"fqdn": "myaksclusterxxx-xxxxxxxx.hcp.eastus2.azmk8s.io",
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.ContainerService/managedClusters/myAKSClusterxxx",
"location": "eastus2",
"name": "myAKSClusterxxx",
"resourceGroup": "myResourceGroupxxx"
}
```


Verify the labels were set:

```
az aks get-credentials --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER_NAME --overwrite-existing
kubectl get nodes --show-labels | grep -e "costcenter=9000" -e "dept=IT"
```


## Create a node pool with a label

You can create an additional node pool with labels for specific scheduling needs.

```
export NODEPOOL_NAME="labelnp"
az aks nodepool add \
--resource-group $RESOURCE_GROUP \
--cluster-name $AKS_CLUSTER_NAME \
--name $NODEPOOL_NAME \
--node-count 1 \
--labels dept=HR costcenter=5000
```


The following is example output from the [ az aks nodepool list](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-list) command showing the

*labelnp*node pool is

*Creating*nodes with the specified

*nodeLabels*:

```
az aks nodepool list --resource-group $RESOURCE_GROUP --cluster-name $AKS_CLUSTER_NAME
```


Results:

```
[
{
"count": 2,
"name": "nodepool1",
"nodeLabels": {
"costcenter": "9000",
"dept": "IT"
}
},
{
"count": 1,
"name": "labelnp",
"nodeLabels": {
"costcenter": "5000",
"dept": "HR"
},
"provisioningState": "Creating"
}
]
```


Verify the labels were set:

```
kubectl get nodes --show-labels | grep -e "costcenter=5000" -e "dept=HR"
```


## Updating labels on existing node pools

You can update the labels on an existing node pool. Note that updating labels will overwrite the old labels.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $AKS_CLUSTER_NAME \
--name $NODEPOOL_NAME \
--labels dept=ACCT costcenter=6000
```


Verify the new labels are set:

```
kubectl get nodes --show-labels | grep -e "costcenter=6000" -e "dept=ACCT"
```


## Unavailable labels

### Reserved system labels

Since the [2021-08-19 AKS release](https://github.com/Azure/AKS/releases/tag/2021-08-19), AKS stopped the ability to make changes to AKS reserved labels. Attempting to change these labels results in an error message.

The following labels are AKS reserved labels. *Virtual node usage* specifies if these labels could be a supported system feature on virtual nodes. Some properties that these system features change aren't available on the virtual nodes because they require modifying the host.

| Label | Value | Example/Options | Virtual node usage |
|---|---|---|---|
`kubernetes.azure.com/agentpool` |
<agent pool name> | `nodepool1` |
Same |
`kubernetes.io/arch` |
<runtime.GOARCH> | `amd64 ` |
N/A |
`kubernetes.io/os` |
<OS Type> | `Linux/Windows` |
Same |
`node.kubernetes.io/instance-type` |
<VM size> | `Standard_NC6s_v3` |
Virtual |
`topology.kubernetes.io/region` |
<Azure region> | `westus2` |
Same |
`topology.kubernetes.io/zone` |
<Azure zone> | `0` |
Same |
`kubernetes.azure.com/cluster` |
<MC_RgName> | `MC_aks_myAKSCluster_westus2` |
Same |
`kubernetes.azure.com/managedby` |
`aks` |
`aks` |
N/A |
`kubernetes.azure.com/mode` |
<mode> | `User` or `system` |
User |
`kubernetes.azure.com/role` |
agent | `Agent` |
Same |
`kubernetes.azure.com/scalesetpriority` |
<VMSS priority> | `spot` or `regular` |
N/A |
`kubernetes.io/hostname` |
<hostname> | `aks-nodepool-00000000-vmss000000` |
Same |
`kubernetes.azure.com/storageprofile` |
<OS disk storage profile> | `Managed` |
N/A |
`kubernetes.azure.com/storagetier` |
<OS disk storage tier> | `Premium_LRS` |
N/A |
`kubernetes.azure.com/node-image-version` |
<VHD version> | `AKSUbuntu-1804-2020.03.05` |
Virtual node version |
`kubernetes.azure.com/network-name` |
<nodepool vnet name> | `vnetName` |
Virtual node virtual network |
`kubernetes.azure.com/network-subnet` |
<nodepool subnet name> | `subnetName` |
Virtual node subnet name |
`kubernetes.azure.com/ppg` |
<nodepool ppg name> | `ppgName` |
N/A |
`kubernetes.azure.com/encrypted-set` |
<nodepool encrypted-set name> | `encrypted-set-name` |
N/A |
`kubernetes.azure.com/accelerator` |
<accelerator> | `nvidia` |
N/A |
`kubernetes.azure.com/fips_enabled` |
<is FIPS enabled?> | `true` |
N/A |
`kubernetes.azure.com/os-sku` |
<os/sku> |
|

`kubernetes.azure.com/os-sku-effective`

`Ubuntu2204`

or similar (never Ubuntu, always has the version specified)`kubernetes.azure.com/os-sku-requested`

`Ubuntu`

, `Ubuntu2204`

, or similar (exactly matches requested sku from API)`kubernetes.azure.com/sku-cpu`

`4`

`kubernetes.azure.com/sku-memory`

`16`

`kubernetes.azure.com/nodepool-type`

`VirtualMachineScaleSets`

*Same*is included in places where the expected values for the labels don't differ between a standard node pool and a virtual node pool. As virtual node pods don't expose any underlying virtual machine (VM), the VM SKU values are replaced with the SKU*Virtual*.*Virtual node version*refers to the current version of the[virtual Kubelet-ACI connector release](https://github.com/virtual-kubelet/azure-aci/releases).*Virtual node subnet name*is the name of the subnet where virtual node pods are deployed into Azure Container Instance (ACI).*Virtual node virtual network*is the name of the virtual network, which contains the subnet where virtual node pods are deployed on ACI.*Node Auto Provisioning (Karpenter)*nodes have additional labels corresponding to the supported[selectors](/en-us/azure/aks/node-auto-provisioning-node-pools#well-known-labels-and-sku-selectors).`kubernetes.azure.com/network-name`

and`kubernetes.azure.com/network-subnet`

will be truncated if the underlying resource names are greater than 64 characters long.

### Reserved prefixes

The following prefixes are AKS reserved prefixes and can't be used for any node:

- kubernetes.azure.com/
- kubernetes.io/

For more information on reserved prefixes, see [Kubernetes well-known labels, annotations, and taints](https://kubernetes.io/docs/reference/labels-annotations-taints/).

### Deprecated labels

The following labels are planned for deprecation with the release of [Kubernetes v1.24](supported-kubernetes-versions#aks-kubernetes-release-calendar). You should change any label references to the recommended substitute.

| Label | Recommended substitute | Maintainer |
|---|---|---|
| failure-domain.beta.kubernetes.io/region | topology.kubernetes.io/region |
|

[Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)[Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)[Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)[Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)*Newly deprecated. For more information, see the [Release Notes](https://github.com/Azure/AKS/releases).

## Next steps

Learn more about Kubernetes labels in the [Kubernetes labels documentation](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).


---

<!-- DOCUMENTO FUSIONADO: istio-meshconfig.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-meshconfig -->

# Configure Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Open-source Istio uses [MeshConfig](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/) to define mesh-wide settings for the Istio service mesh. Istio-based service mesh add-on for AKS builds on top of MeshConfig and classifies different properties as supported, allowed, and blocked.

This article walks through how to configure Istio-based service mesh add-on for Azure Kubernetes Service and the support policy applicable for such configuration.

## Prerequisites

This guide assumes you followed the [documentation](istio-deploy-addon) to enable the Istio add-on on an AKS cluster.

## Set up configuration on cluster

Find out which revision of Istio is deployed on the cluster:

`export RANDOM_SUFFIX=$(head -c 3 /dev/urandom | xxd -p) export CLUSTER="my-aks-cluster" export RESOURCE_GROUP="my-aks-rg$RANDOM_SUFFIX" az aks show --name $CLUSTER --resource-group $RESOURCE_GROUP --query 'serviceMeshProfile' --output json`

Results:

`{ "istio": { "certificateAuthority": null, "components": { "egressGateways": null, "ingressGateways": null }, "revisions": [ "asm-1-24" ] }, "mode": "Istio" }`

This command shows the Istio service mesh profile, including the revision(s) currently deployed on your AKS cluster.

Create a ConfigMap with the name

`istio-shared-configmap-<asm-revision>`

in the`aks-istio-system`

namespace. For example, if your cluster is running asm-1-24 revision of mesh, then the ConfigMap needs to be named as`istio-shared-configmap-asm-1-24`

. Mesh configuration has to be provided within the data section under mesh.Example:

`cat <<EOF > istio-shared-configmap-asm-1-24.yaml apiVersion: v1 kind: ConfigMap metadata: name: istio-shared-configmap-asm-1-24 namespace: aks-istio-system data: mesh: |- accessLogFile: /dev/stdout defaultConfig: holdApplicationUntilProxyStarts: true EOF kubectl apply -f istio-shared-configmap-asm-1-24.yaml`

Results:

`configmap/istio-shared-configmap-asm-1-24 created`

The values under

`defaultConfig`

are mesh-wide settings applied for Envoy sidecar proxy.

Caution

A default ConfigMap (for example, `istio-asm-1-24`

for revision asm-1-24) is created in `aks-istio-system`

namespace on the cluster when the Istio add-on is enabled. However, this default ConfigMap gets reconciled by the managed Istio add-on and thus users should NOT directly edit this ConfigMap. Instead users should create a revision specific Istio shared ConfigMap (for example `istio-shared-configmap-asm-1-24`

for revision asm-1-24) in the aks-istio-system namespace, and then the Istio control plane will merge this with the default ConfigMap, with the default settings taking precedence.

### Mesh configuration and upgrades

When you're performing [canary upgrade for Istio](istio-upgrade), you need to create a separate ConfigMap for the new revision in the `aks-istio-system`

namespace **before initiating the canary upgrade**. This way the configuration is available when the new revision's control plane is deployed on cluster. For example, if you're upgrading the mesh from asm-1-24 to asm-1-25, you need to copy changes over from `istio-shared-configmap-asm-1-24`

to create a new ConfigMap called `istio-shared-configmap-asm-1-25`

in the `aks-istio-system`

namespace.

After the upgrade is completed or rolled back, you can delete the ConfigMap of the revision that was removed from the cluster.

## Allowed, supported, and blocked MeshConfig values

Fields in `MeshConfig`

are classified as `allowed`

, `supported`

, or `blocked`

. To learn more about these categories, see the [support policy](istio-support-policy#allowed-supported-and-blocked-customizations) for Istio add-on features and configuration options.

Mesh configuration and the list of allowed/supported fields are revision specific to account for fields being added/removed across revisions. The full list of allowed fields and the supported/unsupported ones within the allowed list is provided in the below table. When new mesh revision is made available, any changes to allowed and supported classification of the fields is noted in this table.

### MeshConfig

Fields present in [open source MeshConfig reference documentation](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/) that are not covered in the following table are blocked. For example, `configSources`

is blocked.

Field |
Supported/Allowed |
Notes |
|---|---|---|
| proxyListenPort | Allowed | - |
| proxyInboundListenPort | Allowed | - |
| proxyHttpPort | Allowed | - |
| connectTimeout | Allowed | Configurable in
|

[DestinationRule](https://istio.io/latest/docs/reference/config/networking/destination-rule/#ConnectionPoolSettings-TCPSettings)[ProxyConfig](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/#ProxyConfig)[Sidecar CR](https://istio.io/latest/docs/reference/config/networking/sidecar/#OutboundTrafficPolicy)[Azure Monitor Container Insights on AKS](/en-us/azure/azure-monitor/containers/container-insights-overview). It is encouraged to configure access logging via the[Telemetry API](istio-telemetry).[Azure Monitor Container Insights on AKS](/en-us/azure/azure-monitor/containers/container-insights-overview)[Azure Monitor Container Insights on AKS](/en-us/azure/azure-monitor/containers/container-insights-overview)[Telemetry API](istio-telemetry).[Azure Monitor Container Insights on AKS](/en-us/azure/azure-monitor/containers/container-insights-overview)[Azure Monitor Container Insights on AKS](/en-us/azure/azure-monitor/containers/container-insights-overview)[DestinationRule](https://istio.io/latest/docs/reference/config/networking/destination-rule/#ClientTLSSettings)[ServiceEntry](https://istio.io/latest/docs/reference/config/networking/service-entry/#ServiceEntry)[VirtualService](https://istio.io/latest/docs/reference/config/networking/virtual-service/#VirtualService)[DestinationRule](https://istio.io/latest/docs/reference/config/networking/destination-rule/#DestinationRule)[DestinationRule](https://istio.io/latest/docs/reference/config/networking/destination-rule/#LoadBalancerSettings)[DestinationRule](https://istio.io/latest/docs/reference/config/networking/destination-rule/#ConnectionPoolSettings-HTTPSettings)[VirtualService](https://istio.io/latest/docs/reference/config/networking/virtual-service/#HTTPRetry)### ProxyConfig (meshConfig.defaultConfig)

Fields present in [open source MeshConfig reference documentation](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/#ProxyConfig) that are not covered in the following table are blocked.

Field |
Supported/Allowed |
Notes |
|---|---|---|
| tracingServiceName | Allowed | It is encouraged to configure tracing via the
|

[Telemetry API](istio-telemetry).[Telemetry API](istio-telemetry).[Telemetry API](istio-telemetry).Caution

**Support scope of configurations:** Mesh configuration allows for extension providers such as self-managed instances of Zipkin or Apache Skywalking to be configured with the Istio add-on. However, these extension providers are outside the support scope of the Istio add-on. Any issues associated with extension tools are outside the support boundary of the Istio add-on.

## Common errors and troubleshooting tips

- Ensure that the MeshConfig is indented with spaces instead of tabs.
- Ensure that you're only editing the revision specific shared ConfigMap (for example
`istio-shared-configmap-asm-1-24`

) and not trying to edit the default ConfigMap (for example`istio-asm-1-24`

). - The ConfigMap must follow the name
`istio-shared-configmap-<asm-revision>`

and be in the`aks-istio-system`

namespace. - Ensure that all MeshConfig fields are spelled correctly. If they're unrecognized or if they aren't part of the allowed list, admission control denies such configurations.
- When performing canary upgrades,
[check your revision specific ConfigMaps](#mesh-configuration-and-upgrades)to ensure configurations exist for the revisions deployed on your cluster. - Certain
`MeshConfig`

options such as accessLogging may increase Envoy's resource consumption, and disabling some of these settings may mitigate Istio data plane resource utilization. It's also advisable to use the`discoverySelectors`

field in the MeshConfig to help alleviate memory consumption for Istiod and Envoy. - If the
`concurrency`

field in the MeshConfig is misconfigured and set to zero, it causes Envoy to use up all CPU cores. Instead if this field is unset, number of worker threads to run is automatically determined based on CPU requests/limits. [Pod and sidecar race conditions](https://istio.io/latest/docs/ops/common-problems/injection/#pod-or-containers-start-with-network-issues-if-istio-proxy-is-not-ready)in which the application starts before Envoy can be mitigated using the`holdApplicationUntilProxyStarts`

field in the MeshConfig.
