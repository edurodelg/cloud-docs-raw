---
merged_at: 2026-01-25T12:06:27.873136
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-trusted-launch.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-trusted-launch -->

# Trusted Launch for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Trusted Launch](/en-us/azure/virtual-machines/trusted-launch) improves the security of generation 2 virtual machines (VMs) by protecting against advanced and persistent attack techniques. It enables administrators to deploy AKS nodes, which contain the underlying virtual machines, with verified and signed bootloaders, OS kernels, and drivers. By using secure and measured boot, administrators gain insights and confidence of the entire boot chain's integrity.

This article helps you understand this new feature, and how to implement it.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Overview

Trusted Launch is composed of several, coordinated infrastructure technologies that can be enabled independently. Each technology provides another layer of defense against sophisticated threats.

**vTPM**- Trusted Launch introduces a virtualized version of a hardware[Trusted Platform Module](/en-us/windows/security/information-protection/tpm/trusted-platform-module-overview)(TPM), compliant with the TPM 2.0 specification. It serves as a dedicated secure vault for keys and measurements. Trusted Launch provides your VM with its own dedicated TPM instance, running in a secure environment outside the reach of any VM. The vTPM enables[attestation](/en-us/windows/security/information-protection/tpm/tpm-fundamentals#measured-boot-with-support-for-attestation)by measuring the entire boot chain of your VM (UEFI, OS, system, and drivers). Trusted Launch uses the vTPM to perform remote attestation by the cloud. It's used for platform health checks and for making trust-based decisions. As a health check, Trusted Launch can cryptographically certify that your VM booted correctly. If the process fails, possibly because your VM is running an unauthorized component,[Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/defender-for-cloud-introduction)issues integrity alerts. The alerts include details on which components failed to pass integrity checks.**Secure Boot**- At the root of Trusted Launch is Secure Boot for your VM. This mode, which is implemented in platform firmware, protects against the installation of malware-based rootkits and boot kits. Secure Boot works to ensure that only signed operating systems and drivers can boot. It establishes a "root of trust" for the software stack on your VM. With Secure Boot enabled, all OS boot components (boot loader, kernel, kernel drivers) must be signed by trusted publishers. Both Windows and select Linux distributions support Secure Boot. If Secure Boot fails to authenticate an image signed by a trusted publisher, the VM isn't allowed to boot. For more information, see[Secure Boot](/en-us/windows-hardware/design/device-experiences/oem-secure-boot).

## Before you begin

- The Azure CLI version 2.66.0 or later. Run
`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

- Secure Boot requires signed boot loaders, OS kernels, and drivers.

## Limitations

- AKS supports Trusted Launch on kubernetes version 1.25.2 and higher.
- Trusted Launch only supports
[Azure Generation 2 VMs](/en-us/azure/virtual-machines/generation-2). - Node pools with Windows Server operating system aren't supported.
- Trusted Launch can't be enabled in the same node pool as
[FIPS](enable-fips-nodes),[Arm64](use-arm64-vms),[Pod Sandboxing](use-pod-sandboxing), or[Confidential VM](use-cvm). For more information, see[node images documentation](node-images). - Trusted Launch doesn't support virtual node.
- Availability sets aren't supported, only Virtual Machine Scale Sets.
- To enable Secure Boot on GPU node pools, you need to skip installing the GPU driver. For more information, see
[Skip GPU driver installation](gpu-cluster#skip-gpu-driver-installation). - Ephemeral OS disks can be created with trusted Launch and all regions are supported. However, not all virtual machines sizes are supported. For more information, see
[Trusted Launch ephemeral OS sizes](/en-us/azure/virtual-machines/ephemeral-os-disks#trusted-launch-for-ephemeral-os-disks). [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks)doesn't support Trusted Launch on AKS.

## Create an AKS cluster with Trusted Launch enabled

When creating a cluster, enabling vTPM or Secure Boot automatically sets up your node pools to use the customized Trusted Launch image. This image is specifically configured to support the security features enabled by Trusted Launch.

Create an AKS cluster using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command. Before running the command, review the following parameters:**--name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--resource-group**: Enter the name of an existing resource group to host the AKS cluster resource.**--enable-secure-boot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**--enable-vtpm**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

Note

Secure Boot requires signed boot loaders, OS kernels, and drivers. If after enabling Secure Boot your nodes don't start, you can verify which boot components are responsible for Secure Boot failures within an Azure Linux Virtual Machine. See

[verify Secure Boot failures](/en-us/azure/virtual-machines/trusted-launch-faq#verify-secure-boot-failures).The following example creates a cluster named

*myAKSCluster*with one node in the*myResourceGroup*, and enables Secure Boot and vTPM:`az aks create \ --name myAKSCluster \ --resource-group myResourceGroup \ --node-count 1 \ --enable-secure-boot \ --enable-vtpm \ --generate-ssh-keys`

Run the following command to get access credentials for the Kubernetes cluster. Use the

[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command and replace the values for the cluster name and the resource group name.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


Create a template with Trusted Launch parameters. Before creating the template, review the following parameters:

**enableSecureBoot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**enableVTPM**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

In your template, provide values for

`enableVTPM`

and`enableSecureBoot`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters/agentPools`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "securityProfile": { "enableVTPM": "true", "enableSecureBoot": "true", } }`

Deploy your template with vTPM and secure boot enabled on your cluster. See

[Deploy an AKS cluster using an ARM template](/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template)for detailed instructions.

## Add a node pool with Trusted Launch enabled

When you create a node pool, enabling vTPM or Secure Boot automatically sets up your node pools to use the customized Trusted Launch image. This image is specifically configured to support the security features enabled by Trusted Launch.

Add a node pool with Trusted Launch enabled using the

command. Before running the command, review the following parameters:`az aks nodepool add`

**--cluster-name**: Enter the name of the AKS cluster.**--resource-group**: Enter the name of an existing resource group to host the AKS cluster resource.**--name**: Enter a unique name for the node pool. The name of a node pool can only contain lowercase alphanumeric characters and must begin with a lowercase letter. For Linux node pools, the length must be between 1-11 characters.**--node-count**: The number of nodes in the Kubernetes agent pool. Default is 3.**--enable-secure-boot**: Enables Secure Boot to authenticate image signed by a trusted publisher.**--enable-vtpm**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

Note

Secure Boot requires signed boot loaders, OS kernels, and drivers. If after enabling Secure Boot your nodes don't start, you can verify which boot components are responsible for Secure Boot failures within an Azure Linux Virtual Machine. See

[verify Secure Boot failures](/en-us/azure/virtual-machines/trusted-launch-faq#verify-secure-boot-failures).The following example deploys a node pool with vTPM and Secure Boot enabled on a cluster named

*myAKSCluster*with three nodes:`az aks nodepool add --resource-group myResourceGroup --cluster-name myAKSCluster --name mynodepool --node-count 3 --enable-vtpm --enable-secure-boot`

Check that your node pool is using a Trusted Launch image.

Trusted Launch nodes have the following output:

- Node image version containing
`"TL"`

, such as`"AKSUbuntu-2204-gen2TLcontainerd"`

. `"Security-type"`

should be`"Trusted Launch"`

.

`kubectl get nodes kubectl describe node {node-name} | grep -e node-image-version -e security-type`

- Node image version containing

Create a template with Trusted Launch parameters. Before creating the template, review the following parameters:

**enableSecureBoot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**enableVTPM**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

In your template, provide values for

`enableVTPM`

and`enableSecureBoot`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters/agentPools`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "securityProfile": { "enableVTPM": "true", "enableSecureBoot": "true", } }`

Deploy your template with vTPM and secure boot enabled on your cluster. See

[Deploy an AKS cluster using an ARM template](/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template)for detailed instructions.

## Enable vTPM or secure boot on an existing Trusted Launch node pool

You can update an existing Trusted Launch node pool to enable vTPM or secure boot. The following scenarios are supported:

- When creating a node pool, you only specify
`--enable-secure-boot`

, you can run the update command to`--enable-vtpm`

- When creating a node pool, you only specify
`--enable-vtpm`

, you can run the update command to`--enable-secure-boot`


If your node pool doesn't currently have a Trusted Launch image, you won't be able to update the node pool to enable secure boot or vTPM.

Check that your node pool is using a Trusted Launch image.

Trusted Launch nodes have the following output:

- Node image version containing
`"TL"`

, such as`"AKSUbuntu-2204-gen2TLcontainerd"`

. `"Security-type"`

should be`"Trusted Launch"`

.

`kubectl get nodes kubectl describe node {node-name} | grep -e node-image-version -e security-type`

If your node pool doesn't currently have a Trusted Launch image, you won't be able to update the node pool to enable secure boot or vTPM.

- Node image version containing
Update a node pool with Trusted Launch enabled using the

command. Before running the command, review the following parameters:`az aks nodepool update`

**--resource-group**: Enter the name of an existing resource group hosting your existing AKS cluster.**--cluster-name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--name**: Enter the name of your node pool, such as*mynodepool*.**--enable-secure-boot**: Enables Secure Boot to authenticate that the image was signed by a trusted publisher.**--enable-vtpm**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

Note

Secure Boot requires signed boot loaders, OS kernels, and drivers. If after enabling Secure Boot your nodes don't start, you can verify which boot components are responsible for Secure Boot failures within an Azure Linux Virtual Machine. See

[verify Secure Boot failures](/en-us/azure/virtual-machines/trusted-launch-faq#verify-secure-boot-failures).The following example updates the node pool

*mynodepool*on the*myAKSCluster*in the*myResourceGroup*, and enables vTPM. In this scenario, secure boot was enabled during node pool creation:`az aks nodepool update --cluster-name myCluster --resource-group myResourceGroup --name mynodepool --enable-vtpm`

The following example updates the node pool

*mynodepool*on the*myAKSCluster*in the*myResourceGroup*, and enables secure boot. In this scenario, vTPM was enabled during node pool creation:`az aks nodepool update --cluster-name myCluster --resource-group myResourceGroup --name mynodepool --enable-secure-boot`


Check that your node pool is using a Trusted Launch image.

Trusted Launch nodes have the following output:

- Node image version containing
`"TL"`

, such as`"AKSUbuntu-2204-gen2TLcontainerd"`

. `"Security-type"`

should be`"Trusted Launch"`

.

`kubectl get nodes kubectl describe node {node-name} | grep -e node-image-version -e security-type`

If your node pool doesn't currently have a Trusted Launch image, you won't be able to update the node pool to enable secure boot or vTPM.

- Node image version containing
Create a template with Trusted Launch parameters. Before creating the template, review the following parameters:

**enableSecureBoot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**enableVTPM**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

In your template, provide values for

`enableVTPM`

and`enableSecureBoot`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters/agentPools`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "securityProfile": { "enableVTPM": "true", "enableSecureBoot": "true", } }`

Deploy your template with vTPM and secure boot enabled on your cluster. See

[Deploy an AKS cluster using an ARM template](/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template)for detailed instructions.

## Assign pods to nodes with Trusted Launch enabled

You can constrain a pod and restrict it to run on a specific node or nodes, or preference to nodes with Trusted Launch enabled. You can control this using the following node pool selector in your pod manifest.

```
spec:
nodeSelector:
kubernetes.azure.com/security-type = "TrustedLaunch"
```


## Disable vTPM or secure boot on an existing Trusted Launch node pool

You can update an existing node pool to disable vTPM or secure boot. When this occurs, you'll still remain on the Trusted Launch image. You can re-enable vTPM or secure boot at any time by updating your node pool.

Update a node pool to disable secure boot or vTPM using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. Before running the command, review the following parameters:

**--resource-group**: Enter the name of an existing resource group hosting your existing AKS cluster.**--cluster-name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--name**: Enter the name of your node pool, such as*mynodepool*.**--enable-secure-boot**: Enables Secure Boot to authenticate that the image was signed by a trusted publisher.**--enable-vtpm**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

To disable vTPM on an existing node pool:

```
az aks nodepool update --cluster-name myCluster --resource-group myResourceGroup --name mynodepool --disable-vtpm
```


To disable secure boot on an existing node pool:

```
az aks nodepool update --cluster-name myCluster --resource-group myResourceGroup --name mynodepool --disable-secure-boot
```


Create a template with Trusted Launch parameters. Before creating the template, review the following parameters:

**enableSecureBoot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**enableVTPM**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

In your template, provide values for

`enableVTPM`

and`enableSecureBoot`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters/agentPools`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "securityProfile": { "enableVTPM": "false", "enableSecureBoot": "false", } }`

Deploy your template with vTPM and secure boot disabled on your cluster. See

[Deploy an AKS cluster using an ARM template](/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template)for detailed instructions.

## Next steps

In this article, you learned how to enable Trusted Launch. Learn more about [Trusted Launch](/en-us/azure/virtual-machines/trusted-launch).


---

<!-- DOCUMENTO FUSIONADO: use-managed-identity.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-managed-identity -->

# Use a managed identity in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides step-by-step instructions on how to enable and use a system-assigned, user-assigned, or pre-created kubelet managed identity in Azure Kubernetes Service (AKS).

## AKS managed identity prerequisites

Read the

[Overview of managed identities in Azure Kubernetes Service (AKS)](managed-identity-overview)to understand the different types of managed identities available in AKS and how you can use them to securely access Azure resources.Before running the examples in this article, set your subscription as the current active subscription using the

command.`az account set`

`az account set --subscription <subscription-id>`

Create an Azure resource group if you don't already have one by calling the

command.`az group create`

`az group create \ --name <resource-group-name> \ --location <location>`


### Azure CLI version minimum requirements

- Make sure you have Azure CLI version 2.23.0 or later installed. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - To
[use a pre-created kubelet managed identity](use-managed-identity#create-a-kubelet-managed-identity), you need Azure CLI version 2.26.0 or later installed. - To update an existing cluster to use a
[system-assigned managed identity](use-managed-identity#update-an-existing-aks-cluster-to-use-a-system-assigned-managed-identity)or[a user-assigned managed identity](use-managed-identity#update-an-existing-cluster-to-use-a-user-assigned-managed-identity), you need Azure CLI version 2.49.0 or later installed.

### Limitations

Moving or migrating a managed identity-enabled cluster to a different tenant isn't supported.

If the cluster has Microsoft Entra pod-managed identity (

`aad-pod-identity`

) enabled, Node-Managed Identity (NMI) pods modify the iptables of the nodes to intercept calls to the Azure Instance Metadata (IMDS) endpoint. This configuration means any request made to the IMDS endpoint is intercepted by NMI, even if a particular pod doesn't use`aad-pod-identity`

.The AzurePodIdentityException custom resource definition (CRD) can be configured to specify that requests to the IMDS endpoint that originate from a pod matching labels defined in the CRD should be proxied without any processing in NMI. Exclude the system pods with the

`kubernetes.azure.com/managedby: aks`

label in*kube-system*namespace in`aad-pod-identity`

by configuring the AzurePodIdentityException CRD. For more information, see[Use Microsoft Entra pod-managed identities in Azure Kubernetes Service](use-azure-ad-pod-identity).To configure an exception, install the

[mic-exception YAML](https://github.com/Azure/aad-pod-identity/blob/master/deploy/infra/mic-exception.yaml).AKS doesn't support the use of a system-assigned managed identity when using a custom private DNS zone.

The USDOD Central, USDOD East, and USGov Iowa regions in Azure US Government cloud don't support creating a cluster with a user-assigned managed identity.


A pre-created kubelet managed identity must be a user-assigned managed identity.

The China East and China North regions in Microsoft Azure operated by 21Vianet aren't supported.

Important

All Microsoft Defender for Cloud features will be officially retired in the Azure in China region on August 18, 2026. Due to this upcoming retirement, Azure in China customers are no longer able to onboard new subscriptions to the service. A new subscription is any subscription that was not already onboarded to the Microsoft Defender for Cloud service prior to August 18, 2025, the date of the retirement announcement. For more information on the retirement, see

[Microsoft Defender for Cloud Deprecation in Microsoft Azure Operated by 21Vianet Announcement](https://aka.ms/mdcretirementinchina).Customers should work with their account representatives for Microsoft Azure operated by 21Vianet to assess the impact of this retirement on their own operations.


### Update cluster considerations

When you update a cluster, consider the following information:

- An update only works if there's a VHD update to consume. If you're running the latest VHD, you need to wait until the next VHD is available in order to perform the update.
- The Azure CLI ensures your addon's permission is correctly set after migrating. If you're not using the Azure CLI to perform the migrating operation, you need to handle the addon identity's permission by yourself. For an example using an Azure Resource Manager (ARM) template, see
[Assign Azure roles using ARM templates](/en-us/azure/role-based-access-control/role-assignments-template). - If your cluster was using
`--attach-acr`

to pull from images from Azure Container Registry (ACR), you need to run the`az aks update --resource-group <resource-group-name> --name <aks-cluster-name> --attach-acr <acr-resource-id>`

command after updating your cluster to let the newly created kubelet used for managed identity get the permission to pull from ACR. Otherwise, you won't be able to pull from ACR after the update.

## Enable a system-assigned managed identity on an AKS cluster

### Enable a system-assigned managed identity on a new AKS cluster

A system-assigned managed identity is enabled by default when you create a new AKS cluster.

Create an AKS cluster using the

command.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --generate-ssh-keys`


### Update an existing AKS cluster to use a system-assigned managed identity

Update an existing AKS cluster from a service principal to a system-assigned managed identity using the

command with the`az aks update`

`--enable-managed-identity`

parameter.`az aks update \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --enable-managed-identity`

After you update the cluster to use a system-assigned managed identity instead of a service principal, the control plane and pods use the system-assigned managed identity for authorization when accessing other services in Azure. Kubelet continues using a service principal until you also upgrade your agent pool. You can use the

`az aks nodepool upgrade --resource-group <resource-group-name> --cluster-name <aks-cluster-name> --name <node-pool-name> --node-image-only`

command on your nodes to update to a managed identity. A node pool upgrade causes downtime for your AKS cluster as the nodes in the node pools are cordoned, drained, and reimaged.

## Get the principal ID of a system-assigned managed identity

Get the principal ID for the cluster's system-assigned managed identity using the

command.`az aks show`

`CLIENT_ID=$(az aks show \ --name <aks-cluster-name> \ --resource-group <resource-group-name> \ --query identity.principalId \ --output tsv)`


## Add a role assignment for a system-assigned managed identity

Assign an Azure RBAC role to the system-assigned managed identity using the

command.`az role assignment create`

For a VNet, attached Azure disk, static IP address, or route table outside the default worker node resource group, you need to assign the

`Network Contributor`

role on the custom resource group.The following example assigns the

**Network Contributor**role to the system-assigned managed identity. The role assignment is scoped to the resource group that contains the VNet.`az role assignment create \ --assignee <client-id> \ --role "Network Contributor" \ --scope <custom-resource-group-id>`

Note

It can take up to 60 minutes for the permissions granted to your cluster's managed identity to propagate.


## Create a user-assigned managed identity

If you don't yet have a user-assigned managed identity resource, create one using the

command.`az identity create`

`az identity create \ --name <identity-name> \ --resource-group <resource-group-name>`

Your output should resemble the following example output:

`{ "clientId": "<client-id>", "clientSecretUrl": "<clientSecretUrl>", "id": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<identity-name>", "location": "<location>", "name": "<identity-name>", "principalId": "<principal-id>", "resourceGroup": "<resource-group-name>", "tags": {}, "tenantId": "<tenant-id>", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


## Get the principal ID of the user-assigned managed identity

Get the principal ID of the user-assigned managed identity using the

command.`az identity show`

`CLIENT_ID=$(az identity show \ --name <identity-name> \ --resource-group <resource-group-name> \ --query principalId \ --output tsv)`


## Get the resource ID of the user-assigned managed identity

Get the resource ID of the user-assigned managed identity using the

command.`az identity show`

`RESOURCE_ID=$(az identity show \ --name <identity-name> \ --resource-group <resource-group-name> \ --query id \ --output tsv)`


## Assign an Azure RBAC role to the user-assigned managed identity

Add a role assignment for the user-assigned managed identity using the

command.`az role assignment create`

The following example assigns the

**Key Vault Secrets User**role to the user-assigned managed identity to grant it permissions to access secrets in a key vault. The role assignment is scoped to the key vault resource:`az role assignment create \ --assignee <client-id> \ --role "Key Vault Secrets User" \ --scope "<keyvault-resource-id>"`

Note

It can take up to 60 minutes for the permissions granted to your cluster's managed identity to propagate.


## Enable a user-assigned managed identity on an AKS cluster

### Enable a user-assigned managed identity on a new AKS cluster

Create an AKS cluster with the user-assigned managed identity using the

command. Include the`az aks create`

`--assign-identity`

parameter and pass in the resource ID for the user-assigned managed identity:`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --network-plugin azure \ --vnet-subnet-id <vnet-subnet-id> \ --dns-service-ip 10.2.0.10 \ --service-cidr 10.2.0.0/24 \ --assign-identity $RESOURCE_ID \ --generate-ssh-keys`


### Update an existing cluster to use a user-assigned managed identity

Update an existing cluster to use a user-assigned managed identity using the

command. Include the`az aks update`

`--assign-identity`

parameter and pass in the resource ID for the user-assigned managed identity:`az aks update \ --resource-group <resource-group-name> \ --name <cluster-name> \ --enable-managed-identity \ --assign-identity $RESOURCE_ID`

The output for a successful cluster update to use a user-assigned managed identity should resemble the following example output:

`"identity": { "principalId": null, "tenantId": null, "type": "UserAssigned", "userAssignedIdentities": { "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<identity-name>": { "clientId": "<client-id>", "principalId": "<principal-id>" } } },`

Note

Migrating a managed identity for the control plane from system-assigned to user-assigned doesn't result in any downtime for control plane and agent pools. Control plane components continue to the old system-assigned identity for up to several hours, until the next token refresh.


## Determine which type of managed identity a cluster is using

Verify which type of managed identity your cluster is using with the

command.`az aks show`

`az aks show \ --name <aks-cluster-name> \ --resource-group <resource-group-name> \ --query identity.type \ --output tsv`

If the cluster is using a managed identity, the value of the

*type*property will be either**SystemAssigned**or**UserAssigned**.If the cluster is using a service principal, the value of the

*type*property will be null. Consider upgrading your cluster to use a managed identity.

## Create a kubelet managed identity

If you don't have a kubelet managed identity, create one using the

command.`az identity create`

`az identity create \ --name <kubelet-identity-name> \ --resource-group <resource-group-name>`

Your output should resemble the following example output:

`{ "clientId": "<client-id>", "clientSecretUrl": "<clientSecretUrl>", "id": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<kubelet-identity-name>", "location": "<location>", "name": "<kubelet-identity-name>", "principalId": "<principal-id>", "resourceGroup": "<resource-group-name>", "tags": {}, "tenantId": "<tenant-id>", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


## Assign an RBAC role to the kubelet managed identity

Assign the

`acrpull`

role on the kubelet managed identity using thecommand.`az role assignment create`

`az role assignment create \ --assignee <kubelet-client-id> \ --role "acrpull" \ --scope "<acr-registry-id>"`


## Enable a kubelet managed identity on an AKS cluster

### Enable a kubelet managed identity on a new AKS cluster

Create an AKS cluster with your existing identities using the

command.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --network-plugin azure \ --vnet-subnet-id <vnet-subnet-id> \ --dns-service-ip 10.2.0.10 \ --service-cidr 10.2.0.0/24 \ --assign-identity <identity-resource-id> \ --assign-kubelet-identity <kubelet-identity-resource-id> \ --generate-ssh-keys`

A successful AKS cluster creation using a kubelet managed identity should result in output similar to the following:

`"identity": { "principalId": null, "tenantId": null, "type": "UserAssigned", "userAssignedIdentities": { "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<identity-name>": { "clientId": "<client-id>", "principalId": "<principal-id>" } } }, "identityProfile": { "kubeletidentity": { "clientId": "<client-id>", "objectId": "<object-id>", "resourceId": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<kubelet-identity-name>" } },`


### Update an existing cluster to use a kubelet managed identity

To update an existing cluster to use the kubelet managed identity, first get the current control plane managed identity for your AKS cluster.

Warning

Updating the kubelet managed identity upgrades your AKS cluster's node pools, make sure you have the right availability configurations, such as Pod Disruption Budgets, configured before executing this to avoid workload disruption or execute this during a maintenance window.

Confirm your AKS cluster is using the user-assigned managed identity using the

command.`az aks show`

`az aks show \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --query "servicePrincipalProfile"`

If your cluster is using a managed identity, the output shows

`clientId`

with a value of**msi**. A cluster using a service principal shows an object ID. For example:`# The cluster is using a managed identity. { "clientId": "msi" }`

After confirming your cluster is using a managed identity, find the managed identity's resource ID using the

command.`az aks show`

`az aks show --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --query "identity"`

For a user-assigned managed identity, your output should look similar to the following example output:

`{ "principalId": null, "tenantId": null, "type": "UserAssigned", "userAssignedIdentities": <identity-resource-id> "clientId": "<client-id>", "principalId": "<principal-id>" },`

Update your cluster with your existing identities using the

command. Provide the resource ID of the user-assigned managed identity for the control plane for the`az aks update`

`assign-identity`

argument. Provide the resource ID of the kubelet managed identity for the`assign-kubelet-identity`

argument.`az aks update \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --enable-managed-identity \ --assign-identity <identity-resource-id> \ --assign-kubelet-identity <kubelet-identity-resource-id>`

Your output for a successful cluster update using your own kubelet managed identity should resemble the following example output:

`"identity": { "principalId": null, "tenantId": null, "type": "UserAssigned", "userAssignedIdentities": { "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<identity-name>": { "clientId": "<client-id>", "principalId": "<principal-id>" } } }, "identityProfile": { "kubeletidentity": { "clientId": "<client-id>", "objectId": "<object-id>", "resourceId": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<kubelet-identity-name>" } },`


## Get the properties of the kubelet managed identity

Get the properties of the kubelet managed identity using the

command and query on the`az aks show`

`identityProfile.kubeletidentity`

property.`az aks show \ --name <aks-cluster-name> \ --resource-group <resource-group-name> \ --query "identityProfile.kubeletidentity"`


## Next steps

- Use
[Azure Resource Manager templates](/en-us/azure/templates/microsoft.containerservice/managedclusters)to create a managed identity-enabled cluster. - Learn how to
[use kubelogin](kubelogin-authentication)for all supported Microsoft Entra authentication methods in AKS.
