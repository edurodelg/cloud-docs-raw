---
merged_at: 2026-01-25T12:25:33.845672
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: deploy-application-template.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/deploy-application-template -->

# Deploy an Azure Kubernetes application by using an ARM template

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To deploy a Kubernetes application programmatically through Azure CLI, you select the Kubernetes application and settings, generate an ARM template, accept legal terms and conditions, and finally deploy the ARM template.

## Select Kubernetes application

First, you need to select the Kubernetes application that you want to deploy in the Azure portal.

In the Azure portal, go to the

[Marketplace page](https://portal.azure.com/#view/Microsoft_Azure_Marketplace/MarketplaceOffersBlade/selectedMenuItemId/home/fromContext/AKS).Select your Kubernetes application.

Select the required plan.

Select the

**Usage Information + Support**tab. Copy the values for`publisherID`

,`productID`

, and`planID`

. You'll need these values later.

## Generate ARM template

Continue on to generate the ARM template for your deployment.

Select the

**Create**button.Fill out all the application (extension) details.

At the bottom of the

**Review + Create**tab, select**Download a template for automation**.If all the validations are passed, you'll see the ARM template in the editor.

Download the ARM template and save it to a file on your computer.


## Accept terms and agreements

Before you can deploy a Kubernetes application, you need to accept its terms and agreements. To do so, use [Azure CLI](/en-us/cli/azure/vm/image/terms) or [Azure PowerShell](/en-us/powershell/module/az.marketplaceordering/). Be sure to use the values you copied for `plan-publisher`

, `plan-offerID`

, and `plan-name`

in your command.

```
az vm image terms accept --offer <Product ID> --plan <Plan ID> --publisher <Publisher ID>
```


Note

Although this Azure CLI command is for VMs, it also works for containers. For more information, see the [ az cm image terms reference](/en-us/cli/azure/vm/image/terms).

```
## Get-AzMarketplaceTerms -Publisher <Publisher ID> -Product <Product ID> -Name <Plan ID>
```


## Deploy ARM template

Once you've accepted the terms, you can deploy your ARM template. For instructions, see [Tutorial: Create and deploy your first ARM template](/en-us/azure/azure-resource-manager/templates/template-tutorial-create-first-template).

## Next steps

- Learn about
[Kubernetes applications available through Marketplace](deploy-marketplace). - Learn about
[cluster extensions](cluster-extensions).


---

<!-- DOCUMENTO FUSIONADO: release-tracker.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/release-tracker -->

# AKS release tracker

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS releases weekly rounds of fixes and feature and component updates that affect all clusters and customers. It's important for you to know when a particular AKS release is hitting your region, and the AKS release tracker provides these details in real time by versions and regions.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Overview

With AKS release tracker, you can follow specific component updates present in an AKS version release, such as fixes shipped to a core add-on, and node image updates for Azure Linux, Ubuntu, and Windows. The tracker provides links to the specific version of the AKS [release notes](https://github.com/Azure/AKS/releases) to help you identify relevant release instances. Real time data updates allow you to track the release order and status of each region.

## Use the release tracker

To view the release tracker, visit the [AKS release status webpage](https://releases.aks.azure.com/webpage/index.html).

### AKS releases

The top half of the tracker shows the current latest version and three previously available release versions for each region and links to the corresponding release notes entries. This view is helpful when you want to track the available versions by region.


The bottom half of the tracker shows the release order. The table has two views: *By Region* and *By Version*.


### AKS node image updates

The top half of the tracker shows the current latest node image version and three previously available node image versions for each region. This view is helpful when you want to track the available node image versions by region.


The bottom half of the tracker shows the node image update order. The table has two views: *By Region* and *By Version*.
