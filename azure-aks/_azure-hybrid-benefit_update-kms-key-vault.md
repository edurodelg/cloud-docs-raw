---
merged_at: 2026-01-25T12:25:33.850677
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: azure-hybrid-benefit.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-hybrid-benefit -->

# What is Azure Hybrid Benefit for Azure Kubernetes Service?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Hybrid Benefit is a program that enables you to significantly reduce the costs of running workloads in the cloud. With Azure Hybrid Benefit for Azure Kubernetes Service (AKS), you can maximize the value of your on-premises licenses and modernize your applications at no extra cost. Azure Hybrid Benefit enables you to use your on-premises licenses that also have either active Software Assurance (SA) or a qualifying subscription to get Windows virtual machines (VMs) on Azure at a reduced cost.

For more information on qualifications for Azure Hybrid Benefit, what is included with it, how to stay compliant, and more, check out [Azure Hybrid Benefit for Windows Server](/en-us/azure/virtual-machines/windows/hybrid-use-benefit-licensing).

Note

Azure Hybrid Benefit for Azure Kubernetes Service follows the same licensing guidance as Azure Hybrid Benefit for Windows Server VMs on Azure.

## Enable Azure Hybrid Benefit for Azure Kubernetes Service

Azure Hybrid Benefit for Azure Kubernetes Service can be enabled at cluster creation or on an existing AKS cluster. You can enable and disable Azure Hybrid Benefit using either the Azure CLI or Azure PowerShell. In the following examples, be sure to replace the variable definitions with values matching your own cluster.

To create a new AKS cluster with Azure Hybrid Benefit enabled:

```
PASSWORD='' # replace with your own password value
RG_NAME='myResourceGroup'
CLUSTER='myAKSCluster'
az aks create \
--resource-group $RG_NAME \
--name $CLUSTER \
--load-balancer-sku Standard \
--network-plugin azure \
--windows-admin-username azure \
--windows-admin-password $PASSWORD \
--enable-ahub \
--generate-ssh-keys
```


To enable Azure Hybrid Benefit on an existing AKS cluster:

```
RG_NAME='myResourceGroup'
CLUSTER='myAKSCluster'
az aks update --resource-group $RG_NAME --name $CLUSTER--enable-ahub
```


## Disable Azure Hybrid Benefit for Azure Kubernetes Service

To disable Azure Hybrid Benefit for an AKS cluster:

```
RG_NAME='myResourceGroup'
CLUSTER='myAKSCluster'
az aks update --resource-group $RG_NAME --name $CLUSTER --disable-ahub
```


## Next steps

To learn more about Windows containers on AKS, see the following resources:

[Learn how to deploy, manage, and monitor Windows containers on AKS](/en-us/training/paths/deploy-manage-monitor-wincontainers-aks).- Open an issue or provide feedback in the
[Windows containers GitHub repository](https://github.com/microsoft/Windows-Containers/issues). - Review the
[third-party partner solutions for Windows on AKS](windows-aks-partner-solutions).


---

<!-- DOCUMENTO FUSIONADO: update-kms-key-vault.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/update-kms-key-vault -->

# Update the key vault mode for an Azure Kubernetes Service (AKS) cluster with Key Management Service (KMS) etcd encryption (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to update the key vault mode from public to private or private to public for an Azure Kubernetes Service (AKS) cluster with Key Management Service (KMS) etcd encryption.

## Prerequisites

- An AKS cluster with KMS etcd encryption enabled. For more information, see
[Add Key Management Service (KMS) etcd encryption to an Azure Kubernetes Service (AKS) cluster](use-kms-etcd-encryption). - Azure CLI version 2.39.0 or later. Find your version using the
`az --version`

command. If you need to install or upgrade, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

## Update a key vault mode

Note

To change a different key vault with a different mode (whether public or private), you can run [ az aks update](/en-us/cli/azure/aks#az-aks-update) directly. To change the mode of an attached key vault, you must first turn off KMS, then turn it on again using the new key vault IDs.

Turn off KMS on the existing cluster and release the key vault using the

command with the`az aks update`

`--disable-azure-keyvault-kms`

parameter.`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --disable-azure-keyvault-kms`

Warning

After you turn off KMS, the encryption key vault key is still needed. You can't delete or expire it.

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`

Update the key vault from public to private using the

command with the`az keyvault update`

`--public-network-access`

parameter set to`Disabled`

.`az keyvault update --name $KEY_VAULT --resource-group $RESOURCE_GROUP --public-network-access Disabled`

Turn on KMS with the updated private key vault using the

command with the`az aks update`

`--azure-keyvault-kms-key-vault-network-access`

parameter set to`Private`

.`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --enable-azure-keyvault-kms \ --azure-keyvault-kms-key-id $KEY_ID \ --azure-keyvault-kms-key-vault-network-access "Private" \ --azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID`
