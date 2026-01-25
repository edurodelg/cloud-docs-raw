---
merged_at: 2026-01-25T12:25:33.967643
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: kms-data-encryption.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/kms-data-encryption -->

# Enable KMS data encryption in Azure Kubernetes Service (AKS) clusters (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to enable Key Management Service (KMS) data encryption for Kubernetes secrets in Azure Kubernetes Service (AKS). KMS encryption encrypts Kubernetes secrets stored in etcd using Azure Key Vault keys.

AKS supports two key management options:

**Platform-managed keys (PMK)**: AKS automatically creates and manages the encryption keys. This option provides the simplest setup with automatic key rotation.**Customer-managed keys (CMK)**: You create and manage your own Azure Key Vault and encryption keys. This option provides full control over key lifecycle and meets compliance requirements that mandate customer-managed keys.

For more information about encryption concepts and key options, see [Data encryption at rest concepts for AKS](kms-data-encryption-concepts).

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- This article requires version 2.73.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.
- You need the
`aks-preview`

Azure CLI extension version*19.0.0b13*or later.- If you don't already have the
`aks-preview`

extension, install it using thecommand.`az extension add`

`az extension add --name aks-preview`

- If you already have the
`aks-preview`

extension, update it to make sure you have the latest version using thecommand.`az extension update`

`az extension update --name aks-preview`


- If you don't already have the
`kubectl`

CLI tool installed.

### Register the feature flag

To use KMS data encryption with platform-managed keys, register the `KMSPMKPreview`

feature flag in your subscription.

Register the feature flag using the

command.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name KMSPMKPreview`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name KMSPMKPreview`

When the status shows

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Set up environment variables

Set up environment variables for your deployment. Replace the placeholder values with your own.

```
# Set environment variables
export SUBSCRIPTION_ID="<your-subscription-id>"
export RESOURCE_GROUP="<your-resource-group>"
export LOCATION="<your-location>"
export CLUSTER_NAME="<your-cluster-name>"
# Set subscription
az account set --subscription $SUBSCRIPTION_ID
# Create resource group if it doesn't exist
az group create --name $RESOURCE_GROUP --location $LOCATION
```


## Enable platform-managed key encryption

With platform-managed keys, AKS automatically creates and manages the Azure Key Vault and encryption keys. Key rotation is handled automatically by the platform.

### Create a new AKS cluster with platform-managed keys

Create a new AKS cluster with KMS encryption using platform-managed keys.

```
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kubernetes-version 1.33.0 \
--kms-infrastructure-encryption Enabled \
--generate-ssh-keys
```


### Enable platform-managed keys on an existing cluster

Enable KMS encryption with platform-managed keys on an existing AKS cluster.

Note

The cluster must be running Kubernetes version 1.33 or later.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kms-infrastructure-encryption Enabled
```


### Verify KMS configuration

After enabling KMS encryption, verify the configuration.

```
az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query 'securityProfile'
```


The output includes the KMS configuration:

```
{
"kubernetesResourceObjectEncryptionProfile": {
"infrastructureEncryption": "Enabled"
}
}
```


## Enable customer-managed key encryption with a private key vault

For enhanced security, you can use a private key vault that has public network access disabled. AKS accesses the private key vault through the [trusted services firewall exception](/en-us/azure/key-vault/general/network-security#key-vault-firewall-enabled-trusted-services-only). This section shows how to configure customer-managed keys with a private key vault.

### Create a key vault and key with trusted services access

Note

This section illustrates creating a key vault with public network access initially, then enabling the firewall with trusted services bypass. This approach is for illustrative purposes only. In production environments, you should create and manage your key vault as private from the start. For guidance on managing private key vaults, see [Azure Key Vault network security](/en-us/azure/key-vault/general/network-security).

Create a key vault with Azure RBAC enabled.

`export KEY_VAULT_NAME="<your-key-vault-name>" az keyvault create \ --name $KEY_VAULT_NAME \ --resource-group $RESOURCE_GROUP \ --enable-rbac-authorization true \ --public-network-access Enabled # Get the key vault resource ID export KEY_VAULT_RESOURCE_ID=$(az keyvault show --name $KEY_VAULT_NAME --resource-group $RESOURCE_GROUP --query id -o tsv)`

Assign yourself the Key Vault Crypto Officer role to create a key.

`az role assignment create \ --role "Key Vault Crypto Officer" \ --assignee-object-id $(az ad signed-in-user show --query id -o tsv) \ --assignee-principal-type "User" \ --scope $KEY_VAULT_RESOURCE_ID`

Create a key in the key vault.

`export KEY_NAME="<your-key-name>" az keyvault key create --name $KEY_NAME --vault-name $KEY_VAULT_NAME # Get the key ID (without version for automatic rotation) export KEY_ID=$(az keyvault key show --name $KEY_NAME --vault-name $KEY_VAULT_NAME --query 'key.kid' -o tsv) export KEY_ID_NO_VERSION=$(echo $KEY_ID | sed 's|/[^/]*$||')`

Enable the key vault firewall with trusted services bypass.

`az keyvault update \ --name $KEY_VAULT_NAME \ --resource-group $RESOURCE_GROUP \ --default-action Deny \ --bypass AzureServices`

The

`--default-action Deny`

parameter blocks public network access, and the`--bypass AzureServices`

parameter allows trusted Azure services (including AKS) to access the key vault.

### Create a user-assigned managed identity

Create a user-assigned managed identity for the cluster.

`export IDENTITY_NAME="<your-identity-name>" az identity create --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP # Get the identity details export IDENTITY_OBJECT_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'principalId' -o tsv) export IDENTITY_RESOURCE_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'id' -o tsv)`

Assign the required roles to the managed identity.

`# Assign Key Vault Crypto User role for encrypt/decrypt operations az role assignment create \ --role "Key Vault Crypto User" \ --assignee-object-id $IDENTITY_OBJECT_ID \ --assignee-principal-type "ServicePrincipal" \ --scope $KEY_VAULT_RESOURCE_ID # Assign Key Vault Contributor role for key management az role assignment create \ --role "Key Vault Contributor" \ --assignee-object-id $IDENTITY_OBJECT_ID \ --assignee-principal-type "ServicePrincipal" \ --scope $KEY_VAULT_RESOURCE_ID`


### Create a new AKS cluster with customer-managed keys (private)

Create a new AKS cluster with KMS encryption using customer-managed keys with a private key vault.

```
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kubernetes-version 1.33.0 \
--kms-infrastructure-encryption Enabled \
--enable-azure-keyvault-kms \
--azure-keyvault-kms-key-id $KEY_ID_NO_VERSION \
--azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID \
--azure-keyvault-kms-key-vault-network-access Private \
--assign-identity $IDENTITY_RESOURCE_ID \
--generate-ssh-keys
```


### Enable customer-managed keys on an existing cluster (private)

Enable KMS encryption with customer-managed keys using a private key vault on an existing AKS cluster.

Note

The cluster must be running Kubernetes version 1.33 or later.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kms-infrastructure-encryption Enabled \
--enable-azure-keyvault-kms \
--azure-keyvault-kms-key-id $KEY_ID_NO_VERSION \
--azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID \
--azure-keyvault-kms-key-vault-network-access Private \
--assign-identity $IDENTITY_RESOURCE_ID
```


### Verify KMS configuration

After enabling KMS encryption, verify the configuration.

```
az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query 'securityProfile'
```


The output includes the KMS configuration:

```
{
"azureKeyVaultKms": {
"enabled": true,
"keyId": "https://<key-vault-name>.vault.azure.net/keys/<key-name>",
"keyVaultNetworkAccess": "Private",
"keyVaultResourceId": "<key-vault-resource-id>"
},
"kubernetesResourceObjectEncryptionProfile": {
"infrastructureEncryption": "Enabled"
}
}
```


## Enable customer-managed key encryption with a public key vault

With customer-managed keys, you create and manage your own Azure Key Vault and encryption keys. This section shows how to configure customer-managed keys with a public key vault.

### Create a key vault and key

Create a key vault with Azure RBAC enabled.

`export KEY_VAULT_NAME="<your-key-vault-name>" az keyvault create \ --name $KEY_VAULT_NAME \ --resource-group $RESOURCE_GROUP \ --enable-rbac-authorization true \ --public-network-access Enabled # Get the key vault resource ID export KEY_VAULT_RESOURCE_ID=$(az keyvault show --name $KEY_VAULT_NAME --resource-group $RESOURCE_GROUP --query id -o tsv)`

Assign yourself the Key Vault Crypto Officer role to create a key.

`az role assignment create \ --role "Key Vault Crypto Officer" \ --assignee-object-id $(az ad signed-in-user show --query id -o tsv) \ --assignee-principal-type "User" \ --scope $KEY_VAULT_RESOURCE_ID`

Create a key in the key vault.

`export KEY_NAME="<your-key-name>" az keyvault key create --name $KEY_NAME --vault-name $KEY_VAULT_NAME # Get the key ID (without version for automatic rotation) export KEY_ID=$(az keyvault key show --name $KEY_NAME --vault-name $KEY_VAULT_NAME --query 'key.kid' -o tsv) export KEY_ID_NO_VERSION=$(echo $KEY_ID | sed 's|/[^/]*$||')`


### Create a user-assigned managed identity

Create a user-assigned managed identity for the cluster.

`export IDENTITY_NAME="<your-identity-name>" az identity create --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP # Get the identity details export IDENTITY_OBJECT_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'principalId' -o tsv) export IDENTITY_RESOURCE_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'id' -o tsv)`

Assign the required roles to the managed identity.

`# Assign Key Vault Crypto User role for encrypt/decrypt operations az role assignment create \ --role "Key Vault Crypto User" \ --assignee-object-id $IDENTITY_OBJECT_ID \ --assignee-principal-type "ServicePrincipal" \ --scope $KEY_VAULT_RESOURCE_ID # Assign Key Vault Contributor role for key management az role assignment create \ --role "Key Vault Contributor" \ --assignee-object-id $IDENTITY_OBJECT_ID \ --assignee-principal-type "ServicePrincipal" \ --scope $KEY_VAULT_RESOURCE_ID`


### Create a new AKS cluster with customer-managed keys

Create a new AKS cluster with KMS encryption using customer-managed keys.

```
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kubernetes-version 1.33.0 \
--kms-infrastructure-encryption Enabled \
--enable-azure-keyvault-kms \
--azure-keyvault-kms-key-id $KEY_ID_NO_VERSION \
--azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID \
--azure-keyvault-kms-key-vault-network-access Public \
--assign-identity $IDENTITY_RESOURCE_ID \
--generate-ssh-keys
```


### Enable customer-managed keys on an existing cluster

Enable KMS encryption with customer-managed keys on an existing AKS cluster.

Note

The cluster must be running Kubernetes version 1.33 or later.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kms-infrastructure-encryption Enabled \
--enable-azure-keyvault-kms \
--azure-keyvault-kms-key-id $KEY_ID_NO_VERSION \
--azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID \
--azure-keyvault-kms-key-vault-network-access Public \
--assign-identity $IDENTITY_RESOURCE_ID
```


### Verify KMS configuration

After enabling KMS encryption, verify the configuration.

```
az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query 'securityProfile'
```


The output includes the KMS configuration:

```
{
"azureKeyVaultKms": {
"enabled": true,
"keyId": "https://<key-vault-name>.vault.azure.net/keys/<key-name>",
"keyVaultNetworkAccess": "Public",
"keyVaultResourceId": "<key-vault-resource-id>"
},
"kubernetesResourceObjectEncryptionProfile": {
"infrastructureEncryption": "Enabled"
}
}
```


## Migrate between key management options

You can migrate between platform-managed keys and customer-managed keys.

### Migrate from platform-managed keys to customer-managed keys

To migrate from platform-managed keys to customer-managed keys, first set up the key vault, key, and managed identity as described in the customer-managed keys section, then run the update command:

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kms-infrastructure-encryption Enabled \
--enable-azure-keyvault-kms \
--azure-keyvault-kms-key-id $KEY_ID_NO_VERSION \
--azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID \
--azure-keyvault-kms-key-vault-network-access Public \
--assign-identity $IDENTITY_RESOURCE_ID
```


### Migrate from customer-managed keys to platform-managed keys

To migrate from customer-managed keys to platform-managed keys:

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kms-infrastructure-encryption Enabled \
--disable-azure-keyvault-kms
```


## Key rotation

With KMS data encryption, key rotation is handled differently depending on your key management option:

**Platform-managed keys**: Key rotation is automatic. No action is required.**Customer-managed keys**: When you rotate the key version in Azure Key Vault, the KMS controller detects the rotation periodically (every 6 hours) and uses the new key version.

Note

Unlike the legacy KMS experience, with this new implementation you don't need to manually re-encrypt secrets after key rotation. The platform handles this automatically.


---

<!-- DOCUMENTO FUSIONADO: use-azure-ad-pod-identity.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-azure-ad-pod-identity -->

# Use Microsoft Entra pod-managed identities in AKS (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Microsoft Entra pod-managed identities use Azure Kubernetes Service (AKS) primitives to associate [managed identities for Azure resources](/en-us/azure/active-directory/managed-identities-azure-resources/overview) and identities in Microsoft Entra ID with pods. Administrators create identities and bindings as Kubernetes primitives that allow pods to access Azure resources that rely on Microsoft Entra ID as an identity provider.

Microsoft Entra pod-managed identities in AKS have the following limitations:

- Each cluster supports up to 200 pod-managed identities.
- Each cluster supports up to 200 pod-managed identity exceptions.
- Pod-managed identities are supported only on Linux node pools.
- This feature is supported only on clusters backed by Virtual Machine Scale Sets.

Important

We recommend you review [Microsoft Entra Workload ID](workload-identity-overview). This authentication method replaces pod-managed identity (preview), which integrates with the Kubernetes native capabilities to federate with any external identity providers on behalf of the application.

The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service was deprecated on October 24, 2022, and the project archived in September 2023. For more information, see the [deprecation notice](https://github.com/Azure/aad-pod-identity#-announcement). The AKS Pod Identity Managed add-on is patched and supported through September 2025 to allow time for customers to move over to [Microsoft Entra Workload ID](workload-identity-overview).

## Operation mode options

Microsoft Entra pod-managed identity supports two modes of operation:

**Standard Mode**: In this mode, the following two components are deployed to the AKS cluster:[Managed Identity Controller (MIC)](https://azure.github.io/aad-pod-identity/docs/concepts/mic/): An MIC is a Kubernetes controller that watches for changes to pods,[AzureIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentity/), and[AzureIdentityBinding](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentitybinding/)through the Kubernetes API Server. When it detects a relevant change, the MIC adds or deletes[AzureAssignedIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureassignedidentity/)as needed. Specifically, when a pod is scheduled, the MIC assigns the managed identity on Azure to the underlying Virtual Machine Scale Set used by the node pool during the creation phase. When all pods using the identity are deleted, it removes the identity from the Virtual Machine Scale Set of the node pool, unless the same managed identity is used by other pods. The MIC takes similar actions when AzureIdentity or AzureIdentityBinding are created or deleted.[Node Managed Identity (NMI)](https://azure.github.io/aad-pod-identity/docs/concepts/nmi/): NMI is a pod that runs as a DaemonSet on each node in the AKS cluster. NMI intercepts security token requests to the[Azure Instance Metadata Service](/en-us/azure/virtual-machines/linux/instance-metadata-service?tabs=linux)on each node. NMI intercepts token requests and redirects them to itself. It then checks if the pod is authorized to access the requested identity and, if so, retrieves the token from the Microsoft Entra tenant on behalf of the application.

**Managed Mode**: This mode offers only NMI. When installed via the AKS cluster add-on, Azure manages creation of Kubernetes primitives (AzureIdentity and AzureIdentityBinding) and identity assignment in response to CLI commands by the user. Otherwise, if installed via Helm chart, the identity needs to be manually assigned and managed per the user. For more information, see[Pod identity in managed mode](https://azure.github.io/aad-pod-identity/docs/configure/pod_identity_in_managed_mode/).

When you install the Microsoft Entra pod-managed identity via Helm chart or YAML manifest as shown in the [Installation Guide](https://azure.github.io/aad-pod-identity/docs/getting-started/installation/), you can choose between the `standard`

and `managed`

mode. If you instead decide to install the
Microsoft Entra pod-managed identity using the AKS cluster add-on as shown in this article, the setup uses the `managed`

mode.

## Prerequisites

Your Microsoft Entra pod-managed identities in AKS must meet the following requirements:

The Azure CLI version 2.20.0 or later is installed.

Your AKS cluster is at version 1.26 or later.

You must have the appropriate permissions such as the

**Owner**or**Contributor**role.

## Install the aks-preview Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

To install the aks-preview extension, run the following command:

```
az extension add --name aks-preview
```


Run the following command to update to the latest version of the extension released:

```
az extension update --name aks-preview
```


## Register the EnablePodIdentityPreview feature flag

Register the `EnablePodIdentityPreview`

feature flag by using the [az feature register](/en-us/cli/azure/feature#az-feature-register) command as shown in the following example:

```
az feature register --namespace "Microsoft.ContainerService" --name "EnablePodIdentityPreview"
```


Tip

To disable the AKS Managed add-on, run the following command:

```
az feature unregister --namespace "Microsoft.ContainerService" --name "EnablePodIdentityPreview"
```


It takes a few minutes for the status to show as *Registered*. Verify the registration status by using the [az feature show](/en-us/cli/azure/feature#az-feature-show) command:

```
az feature show --namespace "Microsoft.ContainerService" --name "EnablePodIdentityPreview"
```


When the status reflects *Registered*, refresh the registration of the *Microsoft.ContainerService* resource provider by using the [az provider register](/en-us/cli/azure/provider#az-provider-register) command:

```
az provider register --namespace Microsoft.ContainerService
```


## Manage an AKS cluster with pod-managed identities

You can manage your AKS cluster with either the Azure Container Networking Interface (CNI) or Kubenet network plugin when enabling Microsoft Entra pod-managed identities.

Create an AKS cluster with Azure CNI and pod-managed identity enabled with the default recommended configuration. The following commands use

[az group create](/en-us/cli/azure/group#az-group-create)to create a resource group named*myResourceGroup*and thecommand to create an AKS cluster named`az aks create`

*myAKSCluster*in the*myResourceGroup*resource group.`az group create --name myResourceGroup --location eastus az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --enable-pod-identity \ --network-plugin azure \ --generate-ssh-keys`

Use

to sign in to your AKS cluster. This command also downloads and configures the`az aks get-credentials`

`kubectl`

client certificate on your development computer.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


When you enable pod-managed identity on your AKS cluster, the system adds an `AzurePodIdentityException`

named *aks-addon-exception* to the *kube-system* namespace. An `AzurePodIdentityException`

lets pods with certain labels access the Azure Instance Metadata Service (IMDS) endpoint without interception by the NMI server. The *aks-addon-exception* allows AKS first-party addons, such as Microsoft Entra pod-managed identity, to operate without requiring you to manually configure an `AzurePodIdentityException`

. Optionally, you can add, remove, and update an `AzurePodIdentityException`

using:

`az aks pod-identity exception add`

`az aks pod-identity exception delete`

`az aks pod-identity exception update`

Or

`kubectl`


## Update an existing AKS cluster with Azure CNI

To update an existing AKS cluster with Azure CNI to include pod-managed identity, run the following command:

```
az aks update --resource-group $MY_RESOURCE_GROUP --name $MY_CLUSTER --enable-pod-identity
```


## Create a managed identity

You must have the relevant permissions (for example, **Owner**) on your subscription to create the identity.

To create an identity to be used by the demo pod with [az identity create](/en-us/cli/azure/identity#az-identity-create), set the *IDENTITY_CLIENT_ID* and *IDENTITY_RESOURCE_ID* variables, run the following command:

```
az group create --name myIdentityResourceGroup --location eastus
export IDENTITY_RESOURCE_GROUP="myIdentityResourceGroup"
export IDENTITY_NAME="application-identity"
az identity create --resource-group ${IDENTITY_RESOURCE_GROUP} --name ${IDENTITY_NAME}
export IDENTITY_CLIENT_ID="$(az identity show --resource-group ${IDENTITY_RESOURCE_GROUP} --name ${IDENTITY_NAME} --query clientId -o tsv)"
export IDENTITY_RESOURCE_ID="$(az identity show --resource-group ${IDENTITY_RESOURCE_GROUP} --name ${IDENTITY_NAME} --query id -o tsv)"
```


## Assign permissions for the managed identity

The managed identity assigned to the pod must be granted appropriate permissions based on the operations the pod performs. Ensure that you assign only the minimum required roles to follow security best practices.

To run the demo, the *IDENTITY_CLIENT_ID* managed identity must have **Virtual Machine Contributor** permissions in the resource group that contains the Virtual Machine Scale Set of your AKS cluster.

```
# Obtain the name of the resource group containing the Virtual Machine Scale set of your AKS cluster, commonly called the node resource group
NODE_GROUP=$(az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv)
# Obtain the id of the node resource group
NODES_RESOURCE_ID=$(az group show --name $NODE_GROUP -o tsv --query "id")
# Create a role assignment granting your managed identity permissions on the node resource group
az role assignment create --role "Virtual Machine Contributor" --assignee "$IDENTITY_CLIENT_ID" --scope $NODES_RESOURCE_ID
```


## Create a pod-managed identity

To create a pod-managed identity for the cluster using `az aks pod-identity add`

, run the following command:

```
export POD_IDENTITY_NAME="my-pod-identity"
export POD_IDENTITY_NAMESPACE="my-app"
az aks pod-identity add --resource-group myResourceGroup --cluster-name myAKSCluster --namespace ${POD_IDENTITY_NAMESPACE} --name ${POD_IDENTITY_NAME} --identity-resource-id ${IDENTITY_RESOURCE_ID}
```


Note

The "POD_IDENTITY_NAME" has to be a valid Domain Name System [(DNS) subdomain name](https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#dns-subdomain-names) as defined in [RFC 1123](https://tools.ietf.org/html/rfc1123).

When you assign the pod-managed identity by using `pod-identity add`

, the Azure CLI attempts to grant the Managed Identity Operator role over the pod-managed identity (*IDENTITY_RESOURCE_ID*) to the cluster identity.

Azure creates an AzureIdentity resource in your cluster representing the identity in Azure, and an AzureIdentityBinding resource that connects the AzureIdentity to a selector. You can view these resources by running the following command:

```
kubectl get azureidentity -n $POD_IDENTITY_NAMESPACE
kubectl get azureidentitybinding -n $POD_IDENTITY_NAMESPACE
```


## Run a sample application

For a pod to use Microsoft Entra pod-managed identity, the pod needs an *aadpodidbinding* label with a value that matches a selector from a *AzureIdentityBinding*. By default, the selector matches the name of the pod-managed identity, but it can also be set using the `--binding-selector`

option when calling `az aks pod-identity add`

.

To run a sample application using Microsoft Entra pod-managed identity, create a `demo.yaml`

file with the following contents. Replace *POD_IDENTITY_NAME*, *IDENTITY_CLIENT_ID*, and *IDENTITY_RESOURCE_GROUP* with the values from the previous steps. Replace *SUBSCRIPTION_ID* with your subscription ID.

Note

In the previous steps, you created the *POD_IDENTITY_NAME*, *IDENTITY_CLIENT_ID*, and *IDENTITY_RESOURCE_GROUP* variables. You can use a command such as `echo`

to display the value you set for variables, for example `echo $POD_IDENTITY_NAME`

.

```
apiVersion: v1
kind: Pod
metadata:
name: demo
labels:
aadpodidbinding: $POD_IDENTITY_NAME
spec:
containers:
- name: demo
image: mcr.microsoft.com/oss/azure/aad-pod-identity/demo:v1.6.3
args:
- --subscriptionid=$SUBSCRIPTION_ID
- --clientid=$IDENTITY_CLIENT_ID
- --resourcegroup=$IDENTITY_RESOURCE_GROUP
env:
- name: MY_POD_NAME
valueFrom:
fieldRef:
fieldPath: metadata.name
- name: MY_POD_NAMESPACE
valueFrom:
fieldRef:
fieldPath: metadata.namespace
- name: MY_POD_IP
valueFrom:
fieldRef:
fieldPath: status.podIP
nodeSelector:
kubernetes.io/os: linux
```


Notice the pod definition has an `aadpodidbinding`

label with a value that matches the name of the pod-managed identity you ran `az aks pod-identity add`

in the previous step.

Deploy the

`demo.yaml`

to the same namespace as your pod-managed identity using`kubectl apply`

:`kubectl apply -f demo.yaml --namespace $POD_IDENTITY_NAMESPACE`

Verify the sample application successfully runs using

`kubectl logs`

:`kubectl logs demo --follow --namespace $POD_IDENTITY_NAMESPACE`

Verify that the logs show a token is successfully acquired and that the HTTP

*GET*request operation is successful.`... successfully doARMOperations vm count 0 successfully acquired a token using the MSI, msiEndpoint(http://169.254.169.254/metadata/identity/oauth2/token) successfully acquired a token, userAssignedID MSI, msiEndpoint(http://169.254.169.254/metadata/identity/oauth2/token) clientID(xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx) successfully made GET on instance metadata ...`


## Run an application with multiple identities

To enable an application to use multiple identities, set the `--binding-selector`

to the same selector when creating pod identities:

```
az aks pod-identity add --resource-group myResourceGroup --cluster-name myAKSCluster --namespace ${POD_IDENTITY_NAMESPACE} --name ${POD_IDENTITY_NAME_1} --identity-resource-id ${IDENTITY_RESOURCE_ID_1} --binding-selector myMultiIdentitySelector
az aks pod-identity add --resource-group myResourceGroup --cluster-name myAKSCluster --namespace ${POD_IDENTITY_NAMESPACE} --name ${POD_IDENTITY_NAME_2} --identity-resource-id ${IDENTITY_RESOURCE_ID_2} --binding-selector myMultiIdentitySelector
```


Then set the `aadpodidbinding`

field in your pod YAML to the binding selector you specified.

```
apiVersion: v1
kind: Pod
metadata:
name: demo
labels:
aadpodidbinding: myMultiIdentitySelector
...
```


## Disable pod-managed identity on an existing cluster

To disable pod-managed identity on an existing cluster, remove the pod-managed identities from the cluster by running the following command:

`az aks pod-identity delete --name ${POD_IDENTITY_NAME} --namespace ${POD_IDENTITY_NAMESPACE} --resource-group myResourceGroup --cluster-name myAKSCluster`

Then disable the feature on the cluster by running the following command:

`az aks update --resource-group myResourceGroup --name myAKSCluster --disable-pod-identity`


## Clean up resources

To remove a Microsoft Entra pod-managed identity from your cluster, remove the sample application and the pod-managed identity from the cluster.

```
kubectl delete pod demo --namespace $POD_IDENTITY_NAMESPACE
```


Then remove the identity and the role assignment of cluster identity.

```
az aks pod-identity delete \
--name ${POD_IDENTITY_NAME} \
--namespace ${POD_IDENTITY_NAMESPACE} \
--resource-group myResourceGroup \
--cluster-name myAKSCluster
az identity delete \
--resource-group ${IDENTITY_RESOURCE_GROUP} \
--name ${IDENTITY_NAME}
az role assignment delete \
--role "Managed Identity Operator" \
--assignee "$IDENTITY_CLIENT_ID" \
--scope "$IDENTITY_RESOURCE_ID"
```


## Next steps

For more information on managed identities, see [Managed identities for Azure resources](/en-us/azure/active-directory/managed-identities-azure-resources/overview).
