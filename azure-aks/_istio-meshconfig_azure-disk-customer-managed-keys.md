---
merged_at: 2026-01-25T12:06:27.796856
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



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


---

<!-- DOCUMENTO FUSIONADO: azure-disk-customer-managed-keys.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-disk-customer-managed-keys -->

# Bring your own keys (BYOK) with Azure managed disks in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure encrypts all data in a managed disk at rest. By default, data is encrypted with Microsoft-managed keys. For more control over encryption keys, you can supply customer-managed keys to use for encryption at rest for both the OS and data disks for your AKS clusters.

Learn more about customer-managed keys on [Linux](/en-us/azure/virtual-machines/disk-encryption#customer-managed-keys) and [Windows](/en-us/azure/virtual-machines/disk-encryption#customer-managed-keys).

## Prerequisites

- You must enable soft delete and purge protection for
*Azure Key Vault*when using Key Vault to encrypt managed disks. - You need the Azure CLI version 2.11.1 or later.
- Data disk encryption and customer-managed keys are supported on Kubernetes versions 1.24 and higher.
- If you choose to rotate (change) your keys periodically, see
[Customer-managed keys and encryption of Azure managed disk](/en-us/azure/virtual-machines/disk-encryption)for more information.

## Limitations

Encryption of an OS disk with customer-managed keys can only be enabled when creating an AKS cluster.

Virtual nodes are not supported.

When encrypting an ephemeral OS disk-enabled node pool with customer-managed keys, if you want to rotate the key in Azure Key Vault, there are two options to consider:

Immediate usage of new CMK

- Scale down the node pool count to 0.
- Rotate the key.
- Scale up the node pool to the original count.

Gradual usage of new CMK

- Allow AKS node image upgrades or version upgrades to naturally adopt the new CMK over time.
- Until all nodes in the pool are upgraded, the existing CMK will continue to function without disruption.
- Once the upgrade process is complete across all nodes, the new CMK takes effect seamlessly.


## Create an Azure Key Vault instance

Use an Azure Key Vault instance to store your keys. You can optionally use the Azure portal to [Configure customer-managed keys with Azure Key Vault](/en-us/azure/storage/common/customer-managed-keys-configure-key-vault)

Create a new *resource group*, then create a new *Key Vault* instance and enable soft delete and purge protection. Ensure you use the same region and resource group names for each command.

```
# Optionally retrieve Azure region short names for use on upcoming commands
az account list-locations
```


```
# Create new resource group in a supported Azure region
az group create --location myAzureRegionName --name myResourceGroup
# Create an Azure Key Vault resource in a supported Azure region
az keyvault create --name myKeyVaultName --resource-group myResourceGroup --location myAzureRegionName --enable-purge-protection true
```


## Create an instance of a DiskEncryptionSet

Replace *myKeyVaultName* with the name of your key vault. You also need a *key* stored in Azure Key Vault to complete the following steps. Either store your existing Key in the Key Vault you created on the previous steps, or [generate a new key](/en-us/azure/key-vault/general/manage-with-cli2) and replace *myKeyName* with the name of your key.

Note

For cross-account access support for customer-managed encryption keys, you need to create the DiskEncryptionSet for cross-tenant customer-managed keys as detailed in [this guide](/en-us/azure/virtual-machines/disks-cross-tenant-customer-managed-keys?tabs=azure-cli#create-a-disk-encryption-set). The remaining storage class configuration is the same as normal customer managed keys.

```
# Retrieve the Key Vault Id and store it in a variable
keyVaultId=$(az keyvault show --name myKeyVaultName --query "[id]" -o tsv)
# Retrieve the Key Vault key URL and store it in a variable
keyVaultKeyUrl=$(az keyvault key show --vault-name myKeyVaultName --name myKeyName --query "[key.kid]" -o tsv)
# Create a DiskEncryptionSet
az disk-encryption-set create --name myDiskEncryptionSetName --location myAzureRegionName --resource-group myResourceGroup --source-vault $keyVaultId --key-url $keyVaultKeyUrl
```


Important

Make sure that the DiskEncryptionSet is located in the same region as your AKS cluster and that the AKS cluster identity has **read** access to the DiskEncryptionSet.

## Grant the DiskEncryptionSet access to key vault

Use the DiskEncryptionSet and resource groups you created on the prior steps, and grant the DiskEncryptionSet resource access to the Azure Key Vault.

```
# Retrieve the DiskEncryptionSet value and set a variable
desIdentity=$(az disk-encryption-set show --name myDiskEncryptionSetName --resource-group myResourceGroup --query "[identity.principalId]" -o tsv)
# Update security policy settings
az keyvault set-policy --name myKeyVaultName --resource-group myResourceGroup --object-id $desIdentity --key-permissions wrapkey unwrapkey get
```


## Create a new AKS cluster and encrypt the OS disk

Either create a new resource group, or select an existing resource group hosting other AKS clusters, then use your key to encrypt either using network-attached OS disks or ephemeral OS disk. By default, a cluster uses ephemeral OS disk when possible in conjunction with VM size and OS disk size.

Run the following command to retrieve the DiskEncryptionSet value and set a variable:

```
diskEncryptionSetId=$(az disk-encryption-set show --name mydiskEncryptionSetName --resource-group myResourceGroup --query "[id]" -o tsv)
```


If you want to create a new resource group for the cluster, run the following command:

```
az group create --name myResourceGroup --location myAzureRegionName
```


To create a regular cluster using network-attached OS disks encrypted with your key, you can do so by specifying the `--node-osdisk-type=Managed`

argument.

```
az aks create --name myAKSCluster --resource-group myResourceGroup --node-osdisk-diskencryptionset-id $diskEncryptionSetId --generate-ssh-keys --node-osdisk-type Managed
```


To create a cluster with ephemeral OS disk encrypted with your key, you can do so by specifying the `--node-osdisk-type=Ephemeral`

argument. You also need to specify the argument `--node-vm-size`

because the default vm size is too small and doesn't support ephemeral OS disk.

```
az aks create --name myAKSCluster --resource-group myResourceGroup --node-osdisk-diskencryptionset-id $diskEncryptionSetId --generate-ssh-keys --node-osdisk-type Ephemeral --node-vm-size Standard_DS3_v2
```


When new node pools are added to the cluster, the customer-managed key provided during the create process is used to encrypt the OS disk. The following example shows how to deploy a new node pool with an ephemeral OS disk.

```
az aks nodepool add --cluster-name $CLUSTER_NAME --resource-group $RG_NAME --name $NODEPOOL_NAME --node-osdisk-type Ephemeral
```


Important

The DiskEncryptionSet we previously applied to the storage class only encrypts new PVCs. Encrypting existing PVCs requires detaching first before using the Azure Disks API/CLI to update the underlying disks, as shown in [this related guide](/en-us/azure/virtual-machines/linux/disks-enable-customer-managed-keys-cli#encrypt-existing-managed-disks).

## Encrypt your AKS cluster data disk

If you have already provided a disk encryption set during cluster creation, encrypting data disks with the same disk encryption set is the default option. Therefore, this step is optional. However, if you want to encrypt data disks with a different disk encryption set, you can follow these steps.

Important

Ensure you have the proper AKS credentials. The managed identity needs to have contributor access to the resource group where the diskencryptionset is deployed. Otherwise, you'll get an error suggesting that the managed identity does not have permissions.

To assign the AKS cluster identity the Contributor role for the diskencryptionset, execute the following commands:

```
aksIdentity=$(az aks show --resource-group $RG_NAME --name $CLUSTER_NAME --query "identity.principalId")
az role assignment create --role "Contributor" --assignee $aksIdentity --scope $diskEncryptionSetId
```


Create a file called **byok-azure-disk.yaml** that contains the following information. Replace *myAzureSubscriptionId*, *myResourceGroup*, and *myDiskEncrptionSetName* with your values, and apply the yaml. Make sure to use the resource group where your DiskEncryptionSet is deployed.

```
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
name: byok
provisioner: disk.csi.azure.com # replace with "kubernetes.io/azure-disk" if aks version is less than 1.21
parameters:
skuname: StandardSSD_LRS
kind: managed
diskEncryptionSetID: "/subscriptions/{myAzureSubscriptionId}/resourceGroups/{myResourceGroup}/providers/Microsoft.Compute/diskEncryptionSets/{myDiskEncryptionSetName}"
```


Next, run the following commands to update your AKS cluster:

```
# Get credentials
az aks get-credentials --name myAksCluster --resource-group myResourceGroup --output table
# Update cluster
kubectl apply -f byok-azure-disk.yaml
```
