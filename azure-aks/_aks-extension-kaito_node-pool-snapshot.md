---
merged_at: 2026-01-25T12:25:33.886650
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: aks-extension-kaito.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/aks-extension-kaito -->

# Deploy and test inference models with the AI toolchain operator (KAITO) in Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use the AI toolchain operator (KAITO) add-on in the Azure Kubernetes Service (AKS) extension for Visual Studio Code. KAITO automatically provisions the right-sized GPU nodes and sets up the inference server as an endpoint server to your AI model(s), allowing you to test and experiment with AI on AKS with ease.

## Prerequisites

- The Azure Kubernetes Service (AKS) extension for Visual Studio Code needs to be installed to use the KAITO experience. For more information, see
[Install the Azure Kubernetes Service (AKS) extension for Visual Studio Code](aks-extension-vs-code#installation). - The cluster that you are deploying to is a Standard Cluster
*(Kaito cannot currently be installed on Automatic clusters)*. - Verify that your Azure subscription has GPU quota for your chosen model by checking the
[KAITO model workspaces](https://github.com/kaito-project/kaito/tree/main/presets).

## Install KAITO on your cluster

- In the Kubernetes tab, under
**Clouds**>**Azure**>**your subscription**>**Deploy a LLM with KAITO**, right click on your cluster and select**Install KAITO**. - Once on the page, select
**Install KAITO**to start the KAITO installation process. - When the installation completes, you will see a
**Generate Workspace**button that redirects you to the model deployment page.

## Create a KAITO workspace

When creating a KAITO workspace, you can either deploy the default workspace CRD directly into your AKS cluster or save the CRD and customize it for your needs.

- In the Kubernetes tab, under
**Clouds**>**Azure**>**your subscription**>**Deploy a LLM with KAITO**, right click on your cluster and select**Create KAITO workspace**. - Find and select the model you want to deploy.
- Select
**Deploy default workspace CRD**or**Customize workspace CRD**. - Select
**Deploy default workspace CRD**to deploy the model. It tracks the progress of the model and notifies you once the model successfully deploys. It also notifies you if the model was already deployed unsuccessfully onto your cluster. - When the deployment completes, you see a
**View Deployed Models**button that redirects you to the deployment management page.

## Manage KAITO models

The **Manage KAITO models** page allows you to see all models deployed in your AKS cluster along with their status (*ongoing*, *successful*, or *failed*).

In the Kubernetes tab, under

**Clouds**>**Azure**>**your subscription**>**Deploy a LLM with KAITO**, right click on your cluster and select**Manage KAITO models**.From this page, you can choose to perform one of the following actions:

**Get logs**: Select**Get Logs**to access the latest logs from the KAITO workspace pods for your deployment. This action generates a new text file containing the most recent 500 lines of logs.**Delete a model**: Select**Delete Workspace**(or**Cancel**for ongoing deployments). For failed deployments, select**Redeploy Default CRD**to remove the current deployment and restart the model deployment process from scratch.**Test a model**: Select**Test**. This action brings you to a new page where you can interact with the deployed model through a chat interface.


## Test your model

In the Kubernetes tab, under

**Clouds**>**Azure**>**your subscription**>**Deploy a LLM with KAITO**, right click on your cluster and select**Manage KAITO models**.Select

**Test**. This action brings you to a new page where you can interact with the deployed model through the**Prompt**box chat interface.You can optionally adjust the parameters:

**Temperature**: Controls the randomness of the model's output. A low temperature is good for tasks needing precision, like math problems, while a high temperature is better for tasks like creative writing.**Top P**: Limits the next-word choices to a dynamic subset of the vocabulary, determined by a cumulative probability threshold.**Top K**: Limits the next-word selection to the top`K`

most probable words. Smaller`K`

values lead to more predictable outputs, while larger values increase variability.**Repetition Penalty**: Penalizes the model for repeating the same phrases, words, or sequences. This is useful for avoiding repetitive or looping outputs, especially in longer generations.**Max Length**: Defines the maximum number of tokens (words or subwords) in the generated output.


For more information, see [AKS extension for Visual Studio Code features](https://code.visualstudio.com/docs/azure/aksextensions#_features).

## Delete your model inference deployment

- Once you've finished testing the model(s) and you want to free up the allocated GPU resources on your cluster, go to the Kubernetes tab, and under
**Clouds**>**Azure**>**your subscription**>**Deploy a LLM with KAITO**, right click on your cluster and select**Manage KAITO models**. - For each deployed model, select
**Delete Workspace**to clear all allocated resources created by the inference deployment.

## Product support and feedback

If you have a question or want to offer product feedback, please open an issue on the [AKS extension GitHub repository](https://github.com/Azure/vscode-aks-tools/issues/new/choose).

## Next steps

To learn more about other AKS add-ons and extensions, see [Add-ons, extensions, and other integrations for AKS](integrations).


---

<!-- DOCUMENTO FUSIONADO: node-pool-snapshot.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-pool-snapshot -->

# Azure Kubernetes Service (AKS) node pool snapshot

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS releases a new node image weekly. Every new cluster, new node pool, or upgrade cluster always receives the latest image, which can make it hard to maintain consistency and have repeatable environments.

Node pool snapshots allow you to take a configuration snapshot of your node pool and then create new node pools or new clusters based of that snapshot for as long as that configuration and kubernetes version is supported. For more information on the supportability windows, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions).

The snapshot is an Azure resource that contains the configuration information from the source node pool, such as the node image version, kubernetes version, OS type, and OS SKU. You can then reference this snapshot resource and the respective values of its configuration to create any new node pool or cluster based off of it.

## Before you begin

This article assumes that you have an existing AKS cluster. If you don't have an AKS cluster, for guidance on a designing an enterprise-scale implementation of AKS, see [Plan your AKS design](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

### Limitations

- Any node pool or cluster created from a snapshot must use a VM from the same virtual machine family as the snapshot, for example, you can't create a new N-Series node pool based of a snapshot captured from a D-Series node pool because the node images in those cases are structurally different.
- Snapshots must be created same region as the source node pool, those snapshots can be used to create or update clusters and node pools in other regions.

## Take a node pool snapshot

In order to take a snapshot from a node pool, you need the node pool resource ID, which you can get from the following command:

```
NODEPOOL_ID=$(az aks nodepool show --name nodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --query id -o tsv)
```


Important

Your AKS node pool must be created or upgraded after Nov 10th, 2021 in order for a snapshot to be taken from it.
If you are using the `aks-preview`

Azure CLI extension version `0.5.59`

or newer, the commands for node pool snapshot have changed. For updated commands, see the [Node Pool Snapshot CLI reference](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add).

Now, to take a snapshot from the previous node pool, you use the `az aks snapshot`

CLI command.

```
az aks nodepool snapshot create --name MySnapshot --resource-group MyResourceGroup --nodepool-id $NODEPOOL_ID --location eastus
```


## Create a node pool from a snapshot

First, you need the resource ID from the snapshot that was previously created, which you can get from the following command:

```
SNAPSHOT_ID=$(az aks nodepool snapshot show --name MySnapshot --resource-group myResourceGroup --query id -o tsv)
```


Now, we can use the following command to add a new node pool based off of this snapshot.

```
az aks nodepool add --name np2 --cluster-name myAKSCluster --resource-group myResourceGroup --snapshot-id $SNAPSHOT_ID
```


## Upgrading a node pool to a snapshot

You can upgrade a node pool to a snapshot configuration so long as the snapshot kubernetes version and node image version are more recent than the versions in the current node pool.

First, you need the resource ID from the snapshot that was previously created, which you can get from the following command:

```
SNAPSHOT_ID=$(az aks nodepool snapshot show --name MySnapshot --resource-group myResourceGroup --query id -o tsv)
```


Now, we can use this command to upgrade this node pool to this snapshot configuration.

```
az aks nodepool upgrade --name nodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --snapshot-id $SNAPSHOT_ID
```


Note

Your node pool image version is the same contained in the snapshot and remains the same throughout every scale operation. However, if this node pool is upgraded or a node image upgrade is performed without providing a snapshot-id the node image is upgraded to the latest version.

Note

To upgrade only the node version for your node pool, use the `--node-image-only`

flag. This is required when upgrading the node image version for a node pool based on a snapshot with an identical Kubernetes version.

## Create a cluster from a snapshot

When you create a cluster from a snapshot, the snapshot configuration creates the cluster original system pool.

First, you need the resource ID from the snapshot that was previously created, which you can get from the following command:

```
SNAPSHOT_ID=$(az aks nodepool snapshot show --name MySnapshot --resource-group myResourceGroup --query id -o tsv)
```


Now, we can use this command to create this cluster off of the snapshot configuration.

```
az aks create \
--name myAKSCluster2 \
--resource-group myResourceGroup \
--snapshot-id $SNAPSHOT_ID \
--generate-ssh-keys
```


## Next steps

- See the
[AKS release notes](https://github.com/Azure/AKS/releases)for information about the latest node images. - Learn how to upgrade the Kubernetes version with
[Upgrade an AKS cluster](upgrade-cluster). - Learn how to upgrade your node image version with
[Node Image Upgrade](node-image-upgrade) - Learn more about multiple node pools with
[Create multiple node pools](create-node-pools).
