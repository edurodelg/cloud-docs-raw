---
merged_at: 2026-01-25T12:25:33.841829
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: open-service-mesh-uninstall-add-on.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/open-service-mesh-uninstall-add-on -->

# Uninstall the Open Service Mesh (OSM) add-on from your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to uninstall the OMS add-on and related resources from your AKS cluster.

Warning

Microsoft has announced the retirement of the [Open Service Mesh (OSM) add-on for AKS](https://azure.microsoft.com/updates?id=open-service-mesh-add-on-for-aks-will-be-retired-on-september-30-2027). The upstream OSM project has also been retired by the [Cloud Native Computing Foundation (CNCF)](https://docs.openservicemesh.io/). Identify any existing OSM configurations and migrate them to equivalent Istio configurations. For migration steps, see [Migration guidance for Open Service Mesh (OSM) configurations to Istio](open-service-mesh-istio-migration-guidance).

## Disable the OSM add-on from your cluster

Disable the OSM add-on from your cluster using the

command and the`az aks disable-addon`

`--addons`

parameter.`az aks disable-addons \ --resource-group myResourceGroup \ --name myAKSCluster \ --addons open-service-mesh`


## Remove OSM resources

Uninstall the remaining resources on the cluster using the

`osm uninstall cluster-wide-resources`

command.`osm uninstall cluster-wide-resources`

Note

For version 1.1, the command is

`osm uninstall mesh --delete-cluster-wide-resources`

Important

You must remove these additional resources after you disable the OSM add-on. Leaving these resources on your cluster may cause issues if you enable the OSM add-on again in the future.


## Next steps

Learn more about [Open Service Mesh](open-service-mesh-about).


---

<!-- DOCUMENTO FUSIONADO: aks-extension-vs-code.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/aks-extension-vs-code -->

# Use the Azure Kubernetes Service (AKS) extension for Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Kubernetes Service (AKS) extension for Visual Studio Code allows you to easily view and manage your AKS clusters from your development environment.

## Features

The Azure Kubernetes Service (AKS) extension for Visual Studio Code provides a rich set of features to help you manage your AKS clusters, including:

**Merge into Kubeconfig**: Merge your AKS cluster into your`kubeconfig`

file to manage your cluster from the command line.**Save Kubeconfig**: Save your AKS cluster configuration to a file.**AKS Diagnostics**: View diagnostics information based on your cluster's backend telemetry for identity, security, networking, node health, and create, upgrade, delete, and scale issues.**AKS Periscope**: Extract detailed diagnostic information and export it to an Azure storage account for further analysis.**Install Azure Service Operator (ASO)**: Deploy the latest version of ASO and provision Azure resources within Kubernetes.**Start or stop a cluster**: Start or stop your AKS cluster to save costs when you're not using it.

For more information, see [AKS extension for Visual Studio Code features](https://code.visualstudio.com/docs/azure/aksextensions#_features).

## Installation

- Open Visual Studio Code.
- In the
**Extensions**view, search for**Azure Kubernetes Service**. - Select the
**Azure Kubernetes Service**extension and then select**Install**.

For more information, see [Install the AKS extension for Visual Studio Code](https://code.visualstudio.com/docs/azure/aksextensions#_install-the-azure-kubernetes-services-extension).

## Next steps

To learn more about other AKS add-ons and extensions, see [Add-ons, extensions, and other integrations with AKS](integrations).
