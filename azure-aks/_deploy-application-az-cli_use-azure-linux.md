---
merged_at: 2026-01-25T12:25:33.854914
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: deploy-application-az-cli.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/deploy-application-az-cli -->

# Deploy an Azure Kubernetes application programmatically by using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To deploy a Kubernetes application programmatically through Azure CLI, you select the Kubernetes application and settings, accept legal terms and conditions, and finally deploy the application through CLI commands.

## Select Kubernetes application

First, you need to select the Kubernetes application that you want to deploy in the Azure portal. You'll also need to copy some of the details for later use.

In the Azure portal, go to the

[Marketplace page](https://portal.azure.com/#view/Microsoft_Azure_Marketplace/MarketplaceOffersBlade/selectedMenuItemId/home/fromContext/AKS).Select your Kubernetes application.

Select the required plan.

Select the

**Create**button.Fill out all the application (extension) details.

In the

**Review + Create**tab, select**Download a template for automation**. If all the validations are passed, you'll see the ARM template in the editor.Examine the ARM template:

In the variables section, copy the

`plan-name,`

`plan-publisher,`

`plan-offerID,`

and`clusterExtensionTypeName`

values for later use.`"variables": { "plan-name": "DONOTMODIFY", "plan-publisher": "DONOTMODIFY", "plan-offerID": "DONOTMODIFY", "releaseTrain": "DONOTMODIFY", "clusterExtensionTypeName": "DONOTMODIFY" },`

In the resource

`Microsoft.KubernetesConfiguration/extensions`

section, copy the`configurationSettings`

section for later use.

`{ "type": "Microsoft.KubernetesConfiguration/extensions", "apiVersion": "2022-11-01", "name": "[parameters('extensionResourceName')]", "properties": { "extensionType": "[variables('clusterExtensionTypeName')]", "autoUpgradeMinorVersion": true, "releaseTrain": "[variables('releaseTrain')]", "configurationSettings": { "title": "[parameters('app-title')]", "value1": "[parameters('app-value1')]", "value2": "[parameters('app-value2')]" },`

Note

If there are no configuration settings in the ARM template, refer to the application-related documentation in Azure Marketplace or on the partner's website.


## Accept terms and agreements

Before you can deploy a Kubernetes application, you need to accept its terms and agreements. To do so, run the following command, using the values you copied for `plan-publisher`

, `plan-offerID`

, and `plan-name`

.

```
az vm image terms accept --offer <plan-offerID> --plan <plan-name> --publisher <plan-publisher>
```


Note

Although this command is for VMs, it also works for containers. For more information, see the [ az cm image terms reference](/en-us/cli/azure/vm/image/terms).

## Deploy the application

To deploy the application (extension) through Azure CLI, follow the steps outlined in [Deploy and manage cluster extensions by using Azure CLI](deploy-extensions-az-cli).

## Next steps

- Learn about
[Kubernetes applications available through Marketplace](deploy-marketplace). - Learn about
[cluster extensions](cluster-extensions).


---

<!-- DOCUMENTO FUSIONADO: use-azure-linux.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-azure-linux -->

# Use the Azure Linux container host for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Linux container host for AKS is an open-source Linux distribution created by Microsoft, and it's generally available as a container host on Azure Kubernetes Service (AKS). The Azure Linux container host provides reliability and consistency from cloud to edge across the AKS, AKS-HCI, and Arc products. You can deploy Azure Linux node pools in a new cluster, add Azure Linux node pools to your existing Ubuntu clusters, or migrate your Ubuntu nodes to Azure Linux nodes. To learn more about Azure Linux, see the [Azure Linux documentation](/en-us/azure/azure-linux/intro-azure-linux).

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Why use Azure Linux

The Azure Linux container host on AKS uses a native AKS image that provides one place to do all Linux development. Every package is built from source and validated, ensuring your services run on proven components. Azure Linux is lightweight, only including the necessary set of packages needed to run container workloads. It provides a reduced attack surface and eliminates patching and maintenance of unnecessary packages. At the base layer, it has a Microsoft hardened kernel tuned for Azure. Learn more about the [key capabilities of Azure Linux](/en-us/azure/azure-linux/intro-azure-linux#azure-linux-container-host-key-benefits).

## How to use Azure Linux on AKS

To get started using the Azure Linux container host for AKS, see:

[Creating a cluster with Azure Linux](/en-us/azure/azure-linux/quickstart-azure-cli)[How to upgrade Azure Linux clusters](/en-us/azure/azure-linux/tutorial-azure-linux-upgrade)[Add an Azure Linux node pool to your existing cluster](create-node-pools#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli)[Ubuntu to Azure Linux migration](/en-us/azure/azure-linux/tutorial-azure-linux-migration)[Azure Linux supported GPU SKUs](/en-us/azure/azure-linux/intro-azure-linux#azure-linux-container-host-supported-gpu-skus)

## Regional availability

The Azure Linux container host is available for use in the same regions as AKS.

## Next steps

To learn more about Azure Linux, see the [Azure Linux documentation](/en-us/azure/azure-linux/intro-azure-linux).
