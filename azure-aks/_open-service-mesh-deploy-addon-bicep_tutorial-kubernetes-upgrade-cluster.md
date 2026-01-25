---
merged_at: 2026-01-25T12:25:33.937238
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: open-service-mesh-deploy-addon-bicep.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/open-service-mesh-deploy-addon-bicep -->

# Deploy the Open Service Mesh add-on using Bicep in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to deploy the Open Service Mesh (OSM) add-on to Azure Kubernetes Service (AKS) using a [Bicep](/en-us/azure/azure-resource-manager/bicep/) template.

Note

With the retirement of [Open Service Mesh (OSM)](https://docs.openservicemesh.io/) by the Cloud Native Computing Foundation (CNCF), we recommend identifying your OSM configurations and migrating them to an equivalent Istio configuration. For information about migrating from OSM to Istio, see [Migration guidance for Open Service Mesh (OSM) configurations to Istio](open-service-mesh-istio-migration-guidance).

Important

Based on the version of Kubernetes your cluster is running, the OSM add-on installs a different version of OSM.

| Kubernetes version | OSM version installed |
|---|---|
| 1.24.0 or greater | 1.2.5 |
| Between 1.23.5 and 1.24.0 | 1.1.3 |
| Below 1.23.5 | 1.0.0 |

Older versions of OSM may not be available for install or be actively supported if the corresponding AKS version has reached end of life. You can check the [AKS Kubernetes release calendar](supported-kubernetes-versions#aks-kubernetes-release-calendar) for information on AKS version support windows.

[Bicep](/en-us/azure/azure-resource-manager/bicep/overview) is a domain-specific language that uses declarative syntax to deploy Azure resources. You can use Bicep in place of creating [Azure Resource Manager templates](/en-us/azure/azure-resource-manager/templates/overview) to deploy your infrastructure-as-code Azure resources.

## Before you begin

Before you begin, make sure you have the following prerequisites in place:

- The Azure CLI version 2.20.0 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - An SSH public key used for deploying AKS. For more information, see
[Create SSH keys using the Azure CLI](/en-us/azure/virtual-machines/ssh-keys-azure-cli). [Visual Studio Code](https://code.visualstudio.com/)with a Bash terminal.- The Visual Studio Code
[Bicep extension](/en-us/azure/azure-resource-manager/bicep/install).

## Install the OSM add-on for a new AKS cluster by using Bicep

For deployment of a new AKS cluster, you enable the OSM add-on at cluster creation. The following instructions use a generic Bicep template that deploys an AKS cluster by using ephemeral disks and the [ kubenet](configure-kubenet) container network interface, and then enables the OSM add-on. For more advanced deployment scenarios, see

[What is Bicep?](/en-us/azure/azure-resource-manager/bicep/overview)

### Create a resource group

Create a resource group using the

command.`az group create`

`az group create --name <my-osm-bicep-aks-cluster-rg> --location <azure-region>`


### Create the main and parameters Bicep files

Create a directory to store the necessary Bicep deployment files. The following example creates a directory named

*bicep-osm-aks-addon*and changes to the directory:`mkdir bicep-osm-aks-addon cd bicep-osm-aks-addon`

Create the main file and the parameters file.

`touch osm.aks.bicep && touch osm.aks.parameters.json`

Open the

*osm.aks.bicep*file and copy in the following content:`// https://learn.microsoft.com/azure/aks/troubleshooting#what-naming-restrictions-are-enforced-for-aks-resources-and-parameters @minLength(3) @maxLength(63) @description('Provide a name for the AKS cluster. The only allowed characters are letters, numbers, dashes, and underscore. The first and last character must be a letter or a number.') param clusterName string @minLength(3) @maxLength(54) @description('Provide a name for the AKS dnsPrefix. Valid characters include alphanumeric values and hyphens (-). The dnsPrefix can\'t include special characters such as a period (.)') param clusterDNSPrefix string param k8Version string param sshPubKey string param location string param adminUsername string resource aksCluster 'Microsoft.ContainerService/managedClusters@2021-03-01' = { name: clusterName location: location identity: { type: 'SystemAssigned' } properties: { kubernetesVersion: k8Version dnsPrefix: clusterDNSPrefix enableRBAC: true agentPoolProfiles: [ { name: 'agentpool' count: 3 vmSize: 'Standard_DS2_v2' osDiskSizeGB: 30 osDiskType: 'Ephemeral' osType: 'Linux' mode: 'System' } ] linuxProfile: { adminUsername: adminUserName ssh: { publicKeys: [ { keyData: sshPubKey } ] } } addonProfiles: { openServiceMesh: { enabled: true config: {} } } } }`

Open the

*osm.aks.parameters.json*file and copy in the following content. Make sure you replace the deployment parameter values with your own values.Note

The

*osm.aks.parameters.json*file is an example template parameters file needed for the Bicep deployment. Update the parameters specifically for your deployment environment. The parameters you need to add values for include:`clusterName`

,`clusterDNSPrefix`

,`k8Version`

,`sshPubKey`

,`location`

, and`adminUsername`

. To find a list of supported Kubernetes versions in your region, use the`az aks get-versions --location <region>`

command.`{ "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#", "contentVersion": "1.0.0.0", "parameters": { "clusterName": { "value": "<YOUR CLUSTER NAME HERE>" }, "clusterDNSPrefix": { "value": "<YOUR CLUSTER DNS PREFIX HERE>" }, "k8Version": { "value": "<YOUR SUPPORTED KUBERNETES VERSION HERE>" }, "sshPubKey": { "value": "<YOUR SSH KEY HERE>" }, "location": { "value": "<YOUR AZURE REGION HERE>" }, "adminUsername": { "value": "<YOUR ADMIN USERNAME HERE>" } } }`


### Deploy the Bicep files

Open a terminal and authenticate to your Azure account for the Azure CLI using the

`az login`

command.Deploy the Bicep files using the

command.`az deployment group create`

`az deployment group create \ --name OSMBicepDeployment \ --resource-group osm-bicep-test \ --template-file osm.aks.bicep \ --parameters @osm.aks.parameters.json`


## Validate installation of the OSM add-on

Query the add-on profiles of the cluster to check the enabled state of the installed add-ons. The following command should return

`true`

:`az aks list -g <my-osm-aks-cluster-rg> -o json | jq -r '.[].addonProfiles.openServiceMesh.enabled'`

Get the status of the

*osm-controller*using the following`kubectl`

commands.`kubectl get deployments -n kube-system --selector app=osm-controller kubectl get pods -n kube-system --selector app=osm-controller kubectl get services -n kube-system --selector app=osm-controller`


## Access the OSM add-on configuration

You can configure the OSM controller using the OSM MeshConfig resource, and you can view the OSM controller's configuration settings using the Azure CLI.

View the OSM controller's configuration settings using the

`kubectl get`

command.`kubectl get meshconfig osm-mesh-config -n kube-system -o yaml`

Here's an example output of MeshConfig:

`apiVersion: config.openservicemesh.io/v1alpha1 kind: MeshConfig metadata: creationTimestamp: "0000-00-00A00:00:00A" generation: 1 name: osm-mesh-config namespace: kube-system resourceVersion: "2494" uid: 6c4d67f3-c241-4aeb-bf4f-b029b08faa31 spec: certificate: serviceCertValidityDuration: 24h featureFlags: enableEgressPolicy: true enableMulticlusterMode: false enableWASMStats: true observability: enableDebugServer: true osmLogLevel: info tracing: address: jaeger.osm-system.svc.cluster.local enable: false endpoint: /api/v2/spans port: 9411 sidecar: configResyncInterval: 0s enablePrivilegedInitContainer: false envoyImage: mcr.microsoft.com/oss/envoyproxy/envoy:v1.18.3 initContainerImage: mcr.microsoft.com/oss/openservicemesh/init:v0.9.1 logLevel: error maxDataPlaneConnections: 0 resources: {} traffic: enableEgress: true enablePermissiveTrafficPolicyMode: true inboundExternalAuthorization: enable: false failureModeAllow: false statPrefix: inboundExtAuthz timeout: 1s useHTTPSIngress: false`

Notice that

`enablePermissiveTrafficPolicyMode`

is configured to`true`

. In OSM, permissive traffic policy mode bypasses[SMI](https://smi-spec.io/)traffic policy enforcement. In this mode, OSM automatically discovers services that are a part of the service mesh. The discovered services will have traffic policy rules programmed on each Envoy proxy sidecar to allow communications between these services.Warning

Before you proceed, verify that your permissive traffic policy mode is set to

`true`

. If it isn't, change it to`true`

using the following command:`kubectl patch meshconfig osm-mesh-config -n kube-system -p '{"spec":{"traffic":{"enablePermissiveTrafficPolicyMode":true}}}' --type=merge`


## Clean up resources

When you no longer need the Azure resources, delete the deployment's test resource group using the

command.`az group delete`

`az group delete --name osm-bicep-test`

Alternatively, you can uninstall the OSM add-on and the related resources from your cluster. For more information, see

[Uninstall the Open Service Mesh add-on from your AKS cluster](open-service-mesh-uninstall-add-on).

## Next steps

This article showed you how to install the OSM add-on on an AKS cluster and verify that it's installed and running. With the OSM add-on installed on your cluster, you can [deploy a sample application](https://release-v1-0.docs.openservicemesh.io/docs/getting_started/install_apps/) or [onboard an existing application](https://release-v1-0.docs.openservicemesh.io/docs/guides/app_onboarding/) to work with your OSM mesh.


---

<!-- DOCUMENTO FUSIONADO: tutorial-kubernetes-upgrade-cluster.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-upgrade-cluster -->

# Tutorial - Upgrade an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As part of the application and cluster lifecycle, you might want to upgrade to the latest available version of Kubernetes. You can upgrade your Azure Kubernetes Service (AKS) cluster using the Azure CLI, Azure PowerShell, or the Azure portal.

In this tutorial, you upgrade an AKS cluster. You learn how to:

- Identify current and available Kubernetes versions.
- Upgrade your Kubernetes nodes.
- Validate a successful upgrade.

## Before you begin

In previous tutorials, you packaged an application into a container image and uploaded the container image to Azure Container Registry (ACR). You also created an AKS cluster and deployed an application to it. If you haven't completed these steps and want to follow along, start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

If using Azure CLI, this tutorial requires Azure CLI version 2.34.1 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

If using Azure PowerShell, this tutorial requires Azure PowerShell version 5.9.0 or later. Run `Get-InstalledModule -Name Az`

to find the version. If you need to install or upgrade, see [Install Azure PowerShell](/en-us/powershell/azure/install-az-ps).

## Get available cluster versions

Before you upgrade, check which Kubernetes releases are available for your cluster using the

command.`az aks get-upgrades`

`az aks get-upgrades --resource-group myResourceGroup --name myAKSCluster`

The following example output shows the current version as

*1.28.9*and lists the available versions under`upgrades`

:`{ "agentPoolProfiles": null, "controlPlaneProfile": { "kubernetesVersion": "1.28.9", ... "upgrades": [ { "isPreview": null, "kubernetesVersion": "1.29.4" }, { "isPreview": null, "kubernetesVersion": "1.29.2" } ] }, ... }`


## Upgrade an AKS cluster

AKS nodes are carefully cordoned and drained to minimize any potential disruptions to running applications. During this process, AKS performs the following steps:

- Adds a new buffer node (or as many nodes as configured in
[max surge](upgrade-aks-cluster#customize-node-surge-upgrade)) to the cluster that runs the specified Kubernetes version. [Cordons and drains](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)one of the old nodes to minimize disruption to running applications. If you're using max surge, it[cordons and drains](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)as many nodes at the same time as the number of buffer nodes specified.- When the old node is fully drained, it's reimaged to receive the new version and becomes the buffer node for the following node to be upgraded.
- This process repeats until all nodes in the cluster have been upgraded.
- At the end of the process, the last buffer node is deleted, maintaining the existing agent node count and zone balance.

Note

If no patch is specified, the cluster automatically upgrades to the specified minor version's latest GA patch. For example, setting `--kubernetes-version`

to `1.28`

results in the cluster upgrading to `1.28.9`

.

For more information, see [Supported Kubernetes minor version upgrades in AKS](supported-kubernetes-versions#alias-minor-version).

You can either [manually upgrade your cluster](#manually-upgrade-cluster) or [configure automatic cluster upgrades](#configure-automatic-cluster-upgrades). **We recommend you configure automatic cluster upgrades to ensure your cluster is always running the latest version of Kubernetes**.

### Manually upgrade cluster

Upgrade your cluster using the

command.`az aks upgrade`

`az aks upgrade \ --resource-group myResourceGroup \ --name myAKSCluster \ --kubernetes-version KUBERNETES_VERSION`

You will be prompted to confirm the upgrade operation, and to confirm that you want to upgrade the control plane

*and*all the node pools to the selected version of Kubernetes:`Are you sure you want to perform this operation? (y/N): y Since control-plane-only argument is not specified, this will upgrade the control plane AND all nodepools to version 1.29.2. Continue? (y/N): y`

Note

You can only upgrade one minor version at a time. For example, you can upgrade from

*1.14.x*to*1.15.x*, but you can't upgrade from*1.14.x*to*1.16.x*directly. To upgrade from*1.14.x*to*1.16.x*, you must first upgrade from*1.14.x*to*1.15.x*, then perform another upgrade from*1.15.x*to*1.16.x*.The following example output shows the result of upgrading to

*1.29.2*. Notice the`kubernetesVersion`

now shows*1.29.2*:`{ ... "agentPoolProfiles": [ { ... "count": 3, "currentOrchestratorVersion": "1.29.2", "maxPods": 110, "name": "nodepool1", "nodeImageVersion": "AKSUbuntu-2204gen2containerd-202405.27.0", "orchestratorVersion": "1.29.2", "osType": "Linux", "upgradeSettings": { "drainTimeoutInMinutes": null, "maxSurge": "10%", "nodeSoakDurationInMinutes": null, "undrainableNodeBehavior": null }, "vmSize": "Standard_DS2_v2", ... } ], ... "currentKubernetesVersion": "1.29.2", "dnsPrefix": "myAKSClust-myResourceGroup-19da35", "enableRbac": false, "fqdn": "myaksclust-myresourcegroup-19da35-bd54a4be.hcp.westus2.azmk8s.io", "id": "/subscriptions/<Subscription ID>/resourcegroups/myResourceGroup/providers/Microsoft.ContainerService/managedClusters/myAKSCluster", "kubernetesVersion": "1.29.2", "location": "westus2", "name": "myAKSCluster", "type": "Microsoft.ContainerService/ManagedClusters" ... }`


### Configure automatic cluster upgrades

Set an auto-upgrade channel on your cluster using the

command with the`az aks update`

`--auto-upgrade-channel`

parameter set to`patch`

.`az aks update --resource-group myResourceGroup --name myAKSCluster --auto-upgrade-channel patch`


For more information, see [Automatically upgrade an Azure Kubernetes Service (AKS) cluster](auto-upgrade-cluster).

#### Upgrade AKS node images

AKS regularly provides new node images. Linux node images are updated weekly, and Windows node images are updated monthly. We recommend upgrading your node images frequently to use the latest AKS features and security updates. For more information, see [Upgrade node images in Azure Kubernetes Service (AKS)](node-image-upgrade). To configure automatic node image upgrades, see [Automatically upgrade Azure Kubernetes Service (AKS) cluster node operating system images](auto-upgrade-node-image).

## View the upgrade events

Note

When you upgrade your cluster, the following Kubernetes events might occur on the nodes:

**Surge**: Create a surge node.**Drain**: Evict pods from the node. Each pod has a*five minute timeout*to complete the eviction.**Update**: Update of a node has succeeded or failed.**Delete**: Delete a surge node.

View the upgrade events in the default namespaces using the

`kubectl get events`

command.`kubectl get events --field-selector source=upgrader`

The following example output shows some of the above events listed during an upgrade:

`LAST SEEN TYPE REASON OBJECT MESSAGE ... 5m Normal Drain node/aks-nodepool1-96663640-vmss000000 Draining node: aks-nodepool1-96663640-vmss000000 5m Normal Upgrade node/aks-nodepool1-96663640-vmss000000 Deleting node aks-nodepool1-96663640-vmss000000 from API server 4m Normal Upgrade node/aks-nodepool1-96663640-vmss000000 Successfully reimaged node: aks-nodepool1-96663640-vmss000000 4m Normal Upgrade node/aks-nodepool1-96663640-vmss000000 Successfully upgraded node: aks-nodepool1-96663640-vmss000000 4m Normal Drain node/aks-nodepool1-96663640-vmss000000 Draining node: aks-nodepool1-96663640-vmss000000 ...`


## Validate an upgrade

Confirm the upgrade was successful using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --output table`

The following example output shows the AKS cluster runs

*KubernetesVersion 1.27.3*:`Name Location ResourceGroup KubernetesVersion CurrentKubernetesVersion ProvisioningState Fqdn ------------ ---------- --------------- ------------------- ------------------------ ------------------- ---------------------------------------------------------------- myAKSCluster westus2 myResourceGroup 1.29.2 1.29.2 Succeeded myaksclust-myresourcegroup-19da35-bd54a4be.hcp.westus2.azmk8s.io`


## Delete the cluster

As this tutorial is the last part of the series, you might want to delete your AKS cluster to avoid incurring Azure charges.

Remove the resource group, container service, and all related resources using the

command.`az group delete`

`az group delete --name myResourceGroup --yes --no-wait`


Note

When you delete the cluster, the Microsoft Entra service principal used by the AKS cluster isn't removed. For steps on how to remove the service principal, see [AKS service principal considerations and deletion](kubernetes-service-principal#considerations-when-using-a-service-principal). If you used a managed identity, the identity is managed by the platform and doesn't require that you provision or rotate any secrets.

## Next steps

In this tutorial, you upgraded Kubernetes in an AKS cluster. You learned how to:

- Identify current and available Kubernetes versions.
- Upgrade your Kubernetes nodes.
- Validate a successful upgrade.

For more information on AKS, see the [AKS overview](intro-kubernetes). For guidance on how to create full solutions with AKS, see the [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?WT.mc_id=AKSDOCSPAGE).
