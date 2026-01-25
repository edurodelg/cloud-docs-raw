---
merged_at: 2026-01-25T12:06:27.669917
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



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


---

<!-- DOCUMENTO FUSIONADO: understand-aks-costs.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/understand-aks-costs -->

# Understand Azure Kubernetes Service (AKS) usage and costs

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides resources you can use to better understand your Azure Kubernetes Service (AKS) usage and costs and identify cost optimization opportunities.

## About cost analysis

[Microsoft Cost Management](/en-us/azure/cost-management-billing/costs/reporting-get-started) is a suite of FinOps tools that help you analyze, monitor, and optimize your cloud costs. It's available for Azure customers with access to a billing account, subscription, resource group, or management group. For more information, see [What is Microsoft Cost Management?](/en-us/azure/cost-management-billing/costs/overview-cost-management)

[Cost analysis](/en-us/azure/cost-management-billing/costs/reporting-get-started#cost-analysis) is a feature of Cost Management that helps you understand your costs and usage. It provides insights into how your resources are being used and helps you identify opportunities to reduce costs. For more information, see [Start analyzing costs in Azure](/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis).

## Cost analysis resources

### Cost analysis add-on for AKS

The cost analysis add-on for AKS allows you to view comprehensive cost data scoped to Kubernetes constructs, such as clusters and namespaces, and Azure Compute, Network, and Storage resources. Enable it on your AKS cluster by following the steps in [Enable the Azure Kubernetes Service (AKS) cost analysis add-on](cost-analysis). To learn more about viewing the cost data, see [View Kubernetes costs](/en-us/azure/cost-management-billing/costs/view-kubernetes-costs).

### Azure Cost Optimization workbook

The [Azure Cost Optimization workbook](/en-us/azure/advisor/advisor-workbook-cost-optimization) provides a comprehensive view of your Azure costs and recommendations for optimizing them. For more information, see [Cost Optimization workbook](/en-us/azure/advisor/advisor-workbook-cost-optimization).

### Azure Orphaned Resources workbook

The [Azure Orphaned Resources workbook](https://github.com/dolevshor/azure-orphan-resources) helps you identify and manage unused resources in your Azure environment. For more information, see [Orphaned Resources workbook](https://techcommunity.microsoft.com/blog/fasttrackforazureblog/azure-orphan-resources/3492198).

## Next steps

For more information about managing your AKS costs, see [Best practices for cost optimization in Azure Kubernetes Service (AKS)](best-practices-cost).
