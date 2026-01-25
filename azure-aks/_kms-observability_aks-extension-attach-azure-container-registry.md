---
merged_at: 2026-01-25T12:25:33.843884
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



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


---

<!-- DOCUMENTO FUSIONADO: aks-extension-attach-azure-container-registry.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/aks-extension-attach-azure-container-registry -->

# Attach to Azure Container Registry (ACR) using the Azure Kubernetes Service (AKS) extension for Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to attach to Azure Container Registry (ACR) using the Azure Kubernetes Service (AKS) extension for Visual Studio Code.

## Prerequisites

Before you begin, make sure you have the following resources:

- An Azure container registry. If you don't have one, create one using the steps in
[Quickstart: Create a private container registry](/en-us/azure/container-registry/container-registry-get-started-azure-cli). - An AKS cluster. If you don't have one, create one using the steps in
[Quickstart: Deploy an AKS cluster](learn/quick-kubernetes-deploy-cli). - The Azure Kubernetes Service (AKS) extension for Visual Studio Code downloaded. For more information, see
[Install the Azure Kubernetes Service (AKS) extension for Visual Studio Code](aks-extension-vs-code#installation).

## Attach your Azure container registry to your AKS cluster

You can access the screen for attaching your container registry to your AKS cluster using the command palette or the Kubernetes view.

On your keyboard, press

`Ctrl+Shift+P`

to open the command palette.Enter the following information:

**Subscription**: Select the Azure subscription that holds your resources.**ACR Resource Group**: Select the resource group for your container registry.**Container Registry**: Select the container registry you want to attach to your cluster.**Cluster Resource Group**: Select the resource group for your cluster.**Cluster**: Select the cluster you want to attach to your container registry.

Select

**Attach**.You should see a green checkmark, which means your container registry is attached to your AKS cluster.


For more information, see [AKS extension for Visual Studio Code features](https://code.visualstudio.com/docs/azure/aksextensions#_features).

## Product support and feedback

If you have a question or want to offer product feedback, please open an issue on the [AKS extension GitHub repository](https://github.com/Azure/vscode-aks-tools/issues/new/choose).

## Next steps

To learn more about other AKS add-ons and extensions, see [Add-ons, extensions, and other integrations for AKS](integrations).
