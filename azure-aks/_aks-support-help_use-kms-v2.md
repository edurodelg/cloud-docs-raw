---
merged_at: 2026-01-25T12:25:33.853592
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: aks-support-help.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/aks-support-help -->

# Support and troubleshooting for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

## Self help troubleshooting


The [AKS troubleshooting documentation](/en-us/troubleshoot/azure/azure-kubernetes/welcome-azure-kubernetes) provides guidance for how to diagnose and resolve issues that you might encounter when using AKS. These articles cover how to troubleshoot deployment failures, security-related problems, connection issues, and more.

## Post a question on Microsoft Q&A


Azure's preferred destination for community support, [Microsoft Q&A](/en-us/answers/products/azure), allows you to ask technical questions and engage with Azure engineers, Most Valuable Professionals (MVPs), partners, and customers. When you ask a question, make sure you use the `azure-kubernetes-service`

tag. You can also submit your own answers and help other community members with their questions.

If you can't find an answer to your problem using search, you can submit a new question to Microsoft Q&A and tag it with the appropriate Azure service and area.

The following table lists the tags for AKS and related services:

## Create an Azure support request


Explore the range of [Azure support options](https://azure.microsoft.com/support/plans) and choose a plan that best fits your needs. Azure customers can create and manage support requests in the Azure portal.

If you already have an Azure Support Plan, you can [open a support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest).

## Create a GitHub issue


If you need help with the languages and tools for developing and managing AKS, you can open an issue in its GitHub repository.

The following table lists the GitHub repositories for AKS and related services:

| Library | GitHub issues URL |
|---|---|
| Azure PowerShell |
|

[https://github.com/Azure/azure-cli/issues](https://github.com/Azure/azure-cli/issues)[https://github.com/Azure/azure-rest-api-specs/issues](https://github.com/Azure/azure-rest-api-specs/issues)[https://github.com/Azure/azure-sdk-for-java/issues](https://github.com/Azure/azure-sdk-for-java/issues)[https://github.com/Azure/azure-sdk-for-python/issues](https://github.com/Azure/azure-sdk-for-python/issues)[https://github.com/Azure/azure-sdk-for-net/issues](https://github.com/Azure/azure-sdk-for-net/issues)[https://github.com/Azure/azure-sdk-for-js/issues](https://github.com/Azure/azure-sdk-for-js/issues)[https://github.com/Azure/terraform/issues](https://github.com/Azure/terraform/issues)## Stay informed of updates and new releases


Learn about important product updates, roadmap, and announcements in [Azure Updates](https://azure.microsoft.com/updates/?searchterms=compute). For information about Azure Virtual Machines, see the [Azure blog](https://azure.microsoft.com/blog/product/virtual-machines/).

## Next steps

Visit the [Azure Kubernetes Service (AKS) documentation](./).


---

<!-- DOCUMENTO FUSIONADO: use-kms-v2.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-kms-v2 -->

# Migrate to Key Management Service (KMS) v2 in Azure Kubernetes Service (AKS) (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

This article applies to clusters using the legacy KMS experience that need to migrate from KMS v1 to KMS v2. For clusters running Kubernetes version 1.33 or later, we recommend using the new [KMS data encryption](kms-data-encryption) experience, which offers platform-managed keys, customer-managed keys with automatic key rotation, and a simplified configuration experience.

In this article, you learn how to migrate to KMS v2 for clusters with versions older than 1.27. Beginning in AKS version 1.27, turning on the KMS feature configures KMS v2. With KMS v2, you aren't limited to the 2,000 secrets that earlier versions support. For more information, see [KMS v2 improvements](https://kubernetes.io/blog/2023/05/16/kms-v2-moves-to-beta/).

Important

If your cluster version is older than 1.27 and you already turned on KMS, the upgrade to cluster version 1.27 or later is blocked.

## Turn off KMS

Disable KMS on an existing cluster using the

command with the`az aks update`

`--disable-azure-keyvault-kms`

parameter.`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --disable-azure-keyvault-kms`

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


## Upgrade your AKS cluster and turn on KMS

Upgrade your AKS cluster to version 1.27 or later using the

command with the`az aks upgrade`

`--kubernetes-version`

parameter set to your desired version. The following example upgrades to version`1.27.1`

:`az aks upgrade --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --kubernetes-version 1.27.1`

Once the upgrade completes, you can turn on KMS for a public or private key vault using one of the following resources:

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


## Next steps

For more information on using KMS with AKS, see the following articles:
