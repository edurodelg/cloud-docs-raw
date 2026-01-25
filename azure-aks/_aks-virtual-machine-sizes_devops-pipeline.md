---
merged_at: 2026-01-25T12:25:33.934404
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: aks-virtual-machine-sizes.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/aks-virtual-machine-sizes -->

# Virtual machine (VM) sizes, generations, and features for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) supports various virtual machine (VM) sizes, generations, and features to accommodate different workloads and performance requirements. This article provides an overview of available VM sizes and generations for AKS, how to check for available VM sizes in your region, reasons why certain VM sizes might not be available, and what happens when a VM size retires.

## VM support on AKS

Azure supports both Generation 1 (Gen 1) and [Generation 2 (Gen 2) virtual machines (VMs)](/en-us/azure/virtual-machines/generation-2). With some [exceptions](/en-us/windows-server/virtualization/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v), we generally recommend [migrating to Generation 2 VMs](#gen-2-vms-on-aks) to take advantage of the newest features and functionalities in Azure VMs.

The VM size and operating system (OS) you select when creating an AKS node pool determines the VM generation and [node image](node-images) used. Check the [list of supported sizes](/en-us/azure/virtual-machines/generation-2#generation-2-vm-sizes) to see if your SKU supports or requires Gen 2.

### Limitations

There are some limitations to take into account when choosing a VM generation and/or OS:

- Trusted Launch can only be enabled on VM sizes that support Gen 2.
- Confidential VM sizes always use Gen 2 on AKS.
- Arm64 VM sizes always use Gen 2 on AKS.
- Windows Server 2019 node pools don't support Gen 2 VM sizes.
- Windows Server 2022 node pools require use of a custom header to use Gen 2.

To use Gen 2 VMs on AKS, see [Use Gen 2 VMs](#gen-2-vms-on-aks).

## Available VM features

AKS supports various VM features that enhance security, performance, and functionality. Some key features include:

uses pending pod resource requirements to decide the optimal VM configuration to run your workloads efficiently and cost-effectively.**Node autoprovisioning (NAP)**provide a better experience for dynamic workloads and high availability requirements. Virtual Machines node pools enable you to set up multiple similar-family VMs in a single node pool. Your workloads are automatically scheduled on the available resources you configure.**Virtual Machines node pools**

## Supported VM sizes

For in-depth information about VM sizes available in Azure, see [Azure VM sizes](/en-us/azure/virtual-machines/sizes/overview?tabs=breakdownseries%2Cgeneralsizelist%2Ccomputesizelist%2Cmemorysizelist%2Cstoragesizelist%2Cgpusizelist%2Cfpgasizelist%2Chpcsizelist). To view supported Gen 2 VM sizes, see [Generation 2 VM sizes](/en-us/azure/virtual-machines/generation-2).

AKS also supports the following VM types and features:

[Confidential VMs (CVMs)](use-cvm)[Arm-based processor (Arm64) VMs](use-arm64-vms)[GPU-optimized VMs](/en-us/azure/virtual-machines/sizes/overview?tabs=breakdownseries%2Cgeneralsizelist%2Ccomputesizelist%2Cmemorysizelist%2Cstoragesizelist%2Cgpusizelist%2Cfpgasizelist%2Chpcsizelist#gpu-accelerated)[Trusted Launch](use-trusted-launch)[Federal Information Process Standard (FIPS)](enable-fips-nodes)

### Default behavior for supported VM sizes

There are three scenarios when creating a node pool with a supported VM size:

- If the VM size supports only Gen 1, the default behavior for both Linux and Windows node pools is to use the Gen 1 node image.
- If the VM size supports only Gen 2, the default behavior for both Linux and Windows node pools is to use the Gen 2 node image. Windows Server 2022 node pools require a custom header to use a VM size that only supports Gen 2. For more information, see
[Create a Windows node pool with a Gen 2 VM](generation-2-vms#create-a-node-pool-with-a-gen-2-vm). - If the VM size supports both Gen 1 and Gen 2, the default behavior for both Linux and Windows (in Windows Server 2025+) nodes pools is to use the Gen 2 node image. To use the Gen 2 node image for Windows Server 2022, see
[Create a Windows node pool with a Gen 2 VM](generation-2-vms#create-a-node-pool-with-a-gen-2-vm).

## Check available VM sizes

Check available VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm#az-vm-list-skus) command.

```
az vm list-skus --location <your-location> --output table
```


## Why certain VM sizes might not be available

There are several reasons why certain VM sizes might not be available, including:

**Quota limits**: All Azure services set default limits and quotas for resources and features. For more information, see the following resources:[Quotas and regional limits for Azure Kubernetes Service (AKS)](quotas-skus-regions)[Check your quota usage](/en-us/azure/virtual-machines/quotas)[Request a quota increase through an Azure support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest)(for**Issue type**, select**Quota**)

Note

- For
, VM sizes with**user node pools***fewer than two vCPUs and two GBs of memory (RAM)*might not be used by default. - For
, VM sizes with**system node pools***fewer than two vCPUs and four GBs of memory (RAM)*might not be used by default. To ensure that you can reliably schedule the required`kube-system`

pods and your applications, we recommend that you**do not use any**.[B series VMs](/en-us/azure/virtual-machines/sizes/general-purpose/bv1-series)or[Av1 series VMs](/en-us/azure/virtual-machines/sizes/retirement/av1-series-retirement)

**VM sizes in preview**: VM sizes in preview might not be available to you if you haven't registered the preview flag for the VM size.**Blocked by AKS**: Some VM sizes might not be available by default in AKS. These sizes might require extra testing or validation to ensure compatibility with AKS. If you need a specific VM size that isn't available to you, you can[submit a GitHub issue request](https://github.com/Azure/AKS/issues).

Make sure you understand which features your workloads need and choose a VM size that meets those requirements. Later VM versions typically have better performance and improved features. For example, [Gen 2 VMs](#gen-2-vms-on-aks) have increased security and performance benefits over Gen 1 VMs.

## What happens when a VM size retires?

When a VM size or series reaches its retirement date, the VM is deallocated. VM deallocation causes your AKS node pools to break. To check the retirement status of a VM size, see [Retired Azure VM size series](/en-us/azure/virtual-machines/sizes/retirement/retired-sizes-list) or perform a search in [Azure Updates](https://azure.microsoft.com/updates). To check the VM size of your node pools, use the [`az aks nodepool list`

][az-aks-nodepool-list] command and query for the `vmSize`

property:

```
az aks nodepool list --resource-group <your-resource-group> --cluster-name <your-cluster-name> --query "[].{Name:name, VMSize:vmSize}" --output table
```


If you're using a VM size that's retiring/retired, we recommend [migrating your node pools to a supported VM size](#migrate-node-pools-to-a-supported-vm-size) to prevent any potential disruption to your service. Currently, AKS *doesn't support* transitioning to a new VM size within the same node pool.

## Migrate node pools to a supported VM size

Once you determine the appropriate node pools to take action on, you can [resize your node pools](resize-node-pool). During the resizing process, a new node pool is created and workloads are migrated to the new node pool.

For more information on migrating to a new VM size, see the following resources:

[Migrate from Gen 1 to Gen 2 VMs](#gen-2-vms-on-aks)[General-purpose sizes migration guide](/en-us/azure/virtual-machines/migration/sizes/d-ds-dv2-dsv2-ls-series-migration-guide)[Storage-optimized sizes migration guide](/en-us/azure/virtual-machines/migration/sizes/d-ds-dv2-dsv2-ls-series-migration-guide)[GPU-accelerated sizes migration guide](/en-us/azure/virtual-machines/migration/sizes/n-series-migration)[Azure Dedicated Host SKU migration guide](/en-us/azure/virtual-machines/migration/dedicated-host-migration-guide)

## Gen 2 VMs on AKS

Gen 2 VMs are generally Azure's newer offerings and have exclusive features over Gen 1 VMs like increased memory, improved CPU performance, support for NVMe disks, and support for [Trusted Launch](use-trusted-launch).

While we generally recommend running Gen 2 VMs, you should make sure that the generation you choose supports your requirements. To learn more about the differences between generations, and when one might make more sense than the other, see [Should I create a Gen 1 or 2 VM in Hyper-V?](/en-us/windows-server/virtualization/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)

To use Gen 2 VMs on AKS, see [Use generation 2 VMs on AKS](generation-2-vms).

## Next steps

- To learn more about Gen 2 VMs, see
[Support for Generation 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2) - To learn more about supported Gen 2 node images, see
[Node images](node-images)


---

<!-- DOCUMENTO FUSIONADO: devops-pipeline.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/devops-pipeline -->

# Build and deploy to Azure Kubernetes Service with Azure Pipelines

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Azure DevOps Services**

Use [Azure Pipelines](/en-us/azure/devops/pipelines/) to automatically deploy to Azure Kubernetes Service (AKS). Azure Pipelines lets you build, test, and deploy with continuous integration (CI) and continuous delivery (CD) using [Azure DevOps](/en-us/azure/devops/).

In this article, you'll learn how to create a pipeline that continuously builds and deploys your app. Every time you change your code in a repository that contains a Dockerfile, the images are pushed to your Azure Container Registry, and the manifests are then deployed to your AKS cluster.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - An Azure Resource Manager service connection.
[Create an Azure Resource Manager service connection](/en-us/azure/devops/pipelines/library/connect-to-azure#create-an-azure-resource-manager-service-connection-using-automated-security). - A GitHub account. Create a free
[GitHub account](https://github.com/join)if you don't have one already.

## Get the code

Fork the following repository containing a sample application and a Dockerfile:

```
https://github.com/MicrosoftDocs/pipelines-javascript-docker
```


## Create the Azure resources

Sign in to the [Azure portal](https://portal.azure.com/), and then select the [Cloud Shell](/en-us/azure/cloud-shell/overview) button in the upper-right corner. Use Azure CLI or PowerShell to create an AKS cluster.

### Create a container registry

```
# Create a resource group
az group create --name myapp-rg --location eastus
# Create a container registry
az acr create --resource-group myapp-rg --name mycontainerregistry --sku Basic
# Create a Kubernetes cluster
az aks create \
--resource-group myapp-rg \
--name myapp \
--node-count 1 \
--enable-addons monitoring \
--generate-ssh-keys
```


## Sign in to Azure Pipelines

Sign in to [Azure Pipelines](https://azure.microsoft.com/services/devops/pipelines). After you sign in, your browser goes to `https://dev.azure.com/my-organization-name`

and displays your Azure DevOps dashboard.

Within your selected organization, create a *project*. If you don't have any projects in your organization, you see a **Create a project to get started** screen. Otherwise, select the **Create Project** button in the upper-right corner of the dashboard.

## Create the pipeline

### Connect and select your repository

Sign in to your Azure DevOps organization and go to your project.

Go to

**Pipelines**, and then select**New pipeline**.Do the steps of the wizard by first selecting

**GitHub**as the location of your source code.You might be redirected to GitHub to sign in. If so, enter your GitHub credentials.

When you see the list of repositories, select your repository.

You might be redirected to GitHub to install the Azure Pipelines app. If so, select

**Approve & install**.Select

**Deploy to Azure Kubernetes Service**.If you're prompted, select the subscription in which you created your registry and cluster.

Select the

`myapp`

cluster.For

**Namespace**, select**Existing**, and then select**default**.Select the name of your container registry.

You can leave the image name set to the default.

Set the service port to 8080.

Set the

**Enable Review App for Pull Requests**checkbox for[review app](/en-us/azure/devops/pipelines/process/environments-kubernetes)related configuration to be included in the pipeline YAML autogenerated in subsequent steps.Select

**Validate and configure**.As Azure Pipelines creates your pipeline, the process will:

Create a

*Docker registry service connection*to enable your pipeline to push images into your container registry.Create an

*environment*and a Kubernetes resource within the environment. For an RBAC-enabled cluster, the created Kubernetes resource implicitly creates ServiceAccount and RoleBinding objects in the cluster so that the created ServiceAccount can't perform operations outside the chosen namespace.Generate an

*azure-pipelines.yml*file, which defines your pipeline.Generate Kubernetes manifest files. These files are generated by hydrating the

[deployment.yml](https://github.com/Microsoft/azure-pipelines-yaml/blob/master/templates/resources/k8s/deployment.yml)and[service.yml](https://github.com/Microsoft/azure-pipelines-yaml/blob/master/templates/resources/k8s/service.yml)templates based on selections you made. When you're ready, select**Save and run**.

Select

**Save and run**.You can change the

**Commit message**to something like*Add pipeline to our repository*. When you're ready, select**Save and run**to commit the new pipeline into your repo, and then begin the first run of your new pipeline!

## See your app deploy

As your pipeline runs, watch as your build stage, and then your deployment stage, go from blue (running) to green (completed). You can select the stages and jobs to watch your pipeline in action.

Note

If you're using a Microsoft-hosted agent, you must add the IP range of the Microsoft-hosted agent to your firewall. Get the weekly list of IP ranges from the [weekly JSON file](https://www.microsoft.com/download/details.aspx?id=56519), which is published every Wednesday. The new IP ranges become effective the following Monday. For more information, see [Microsoft-hosted agents](/en-us/azure/devops/pipelines/agents/hosted?tabs=yaml&view=azure-devops&preserve-view=true#networking).
To find the IP ranges that are required for your Azure DevOps organization, learn how to [identify the possible IP ranges for Microsoft-hosted agents](/en-us/azure/devops/pipelines/agents/hosted?tabs=yaml&view=azure-devops&preserve-view=true#to-identify-the-possible-ip-ranges-for-microsoft-hosted-agents).

After the pipeline run is finished, explore what happened and then go see your app deployed. From the pipeline summary:

Select the

**Environments**tab.Select

**View environment**.Select the instance of your app for the namespace you deployed to. If you used the defaults, then it is the

**myapp**app in the**default**namespace.Select the

**Services**tab.Select and copy the external IP address to your clipboard.

Open a new browser tab or window and enter <IP address>:8080.


If you're building our sample app, then *Hello world* appears in your browser.

## How the pipeline builds

When you finished selecting options and then proceeded to validate and configure the pipeline Azure Pipelines created a pipeline for you, using the *Deploy to Azure Kubernetes Service* template.

The build stage uses the [Docker task](/en-us/azure/devops/pipelines/tasks/build/docker) to build and push the image to the Azure Container Registry.

```
- stage: Build
displayName: Build stage
jobs:
- job: Build
displayName: Build job
pool:
vmImage: $(vmImageName)
steps:
- task: Docker@2
displayName: Build and push an image to container registry
inputs:
command: buildAndPush
repository: $(imageRepository)
dockerfile: $(dockerfilePath)
containerRegistry: $(dockerRegistryServiceConnection)
tags: |
$(tag)
- task: PublishPipelineArtifact@1
inputs:
artifactName: 'manifests'
path: 'manifests'
```


The deployment job uses the *Kubernetes manifest task* to create the `imagePullSecret`

required by Kubernetes cluster nodes to pull from the Azure Container Registry resource. Manifest files are then used by the Kubernetes manifest task to deploy to the Kubernetes cluster. The manifest files, `service.yml`

and `deployment.yml`

, were generated when you used the **Deploy to Azure Kubernetes Service** template.

```
- stage: Deploy
displayName: Deploy stage
dependsOn: Build
jobs:
- deployment: Deploy
displayName: Deploy job
pool:
vmImage: $(vmImageName)
environment: 'myenv.aksnamespace' #customize with your environment
strategy:
runOnce:
deploy:
steps:
- task: DownloadPipelineArtifact@2
inputs:
artifactName: 'manifests'
downloadPath: '$(System.ArtifactsDirectory)/manifests'
- task: KubernetesManifest@1
displayName: Create imagePullSecret
inputs:
action: 'createSecret'
connectionType: 'kubernetesServiceConnection'
kubernetesServiceConnection: 'myapp-default' #customize for your Kubernetes service connection
secretType: 'dockerRegistry'
secretName: '$(imagePullSecret)'
dockerRegistryEndpoint: '$(dockerRegistryServiceConnection)'
- task: KubernetesManifest@1
displayName: Deploy to Kubernetes cluster
inputs:
action: 'deploy'
connectionType: 'kubernetesServiceConnection'
kubernetesServiceConnection: 'myapp-default' #customize for your Kubernetes service connection
manifests: |
$(Pipeline.Workspace)/manifests/deployment.yml
$(Pipeline.Workspace)/manifests/service.yml
containers: '$(containerRegistry)/$(imageRepository):$(tag)'
imagePullSecrets: '$(imagePullSecret)'
```


## Clean up resources

Whenever you're done with the resources you created, you can use the following command to delete them:

```
az group delete --name myapp-rg
```


Enter `y`

when you're prompted.
