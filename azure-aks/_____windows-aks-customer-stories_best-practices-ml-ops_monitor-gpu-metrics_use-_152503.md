---
merged_at: 2026-01-26T20:54:26.141828
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-aks-customer-stories -->

# Windows AKS customer stories

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Explore how various industries are using Windows Containers on Azure Kubernetes Service (AKS) for seamless Kubernetes integration with minimal code modifications.

Learn directly from the customer stories listed here.

## Customer stories

### Finastra

LaserPro document management software is key to the Finastra vision of delivering the future of banking. Migrating from an on-premises management system to a cloud-based infrastructure using Windows containers on Azure Kubernetes Service has significantly increased agility through biweekly updates and reduced support costs for both customers and developers.

For more information visit [Finastra's Windows AKS customer story](https://customers.microsoft.com/en-us/story/1759082810297807726-finastra-azure-kubernetes-service-professional-services-en-united-kingdom).

### Relativity

Relativity, transitioned from virtual machines to Windows containers on Azure Kubernetes Service (AKS) to modernize its Windows code base, streamline development, and improve scalability.

This shift enabled faster, more cost-effective deployment of their products and services without rewriting millions of lines of code. The transition to a containerized architecture significantly reduced deployment cycles from six months to a single day, enhancing the speed and flexibility of Relativity’s engineering teams and leading to better performance and security in their application delivery.

For more information visit [Relativity’s Windows AKS customer story](https://customers.microsoft.com/story/1516554049543037694-windows-containers-helps-relativity-boost-reliability-security).

### Duck Creek

Duck Creek Technologies modernized its insurance software solutions by adopting Windows containers on Azure Kubernetes Service (AKS), significantly enhancing operational efficiency and reducing time to market for new features. This transition to AKS enabled Duck Creek to offer scalable, reliable, and up-to-date SaaS solutions to its insurance clients, supporting rapid deployment and active delivery of updates.

By containerizing their applications to Windows Containers, Duck Creek could maintain the flexibility and robustness of their products without extensive code rewriting, thereby ensuring high availability and scalability, especially critical during peak demand periods like natural disasters. This move represents Duck Creek's commitment to leveraging cutting-edge technology for Insurtech innovation.

### Forza

Forza Horizon 5, developed by Turn 10 Studios, achieved remarkable performance and scalability by transitioning to Azure Kubernetes Service (AKS) with Windows-based containers. This shift allowed the team to adapt swiftly to demand spikes, handling over 10 million concurrent players at launch, the biggest first week in Xbox Game Studios history.

By utilizing Windows AKS, they were able to significantly reduce infrastructure management tasks, enhancing both the development process and the gaming experience. The move to containerized architecture enabled rapid scaling from 600,000 to 3 million concurrent users and reduced infrastructure costs, demonstrating the effectiveness of AKS in high-demand, low-latency environments like gaming.

For more information visit [Forza Horizon 5 runs on Windows containers on Azure Kubernetes Services](https://techcommunity.microsoft.com/blog/itopstalkblog/forza-horizon-5-runs-on-windows-containers-on-azure-kubernetes-services/3570404).

### Microsoft Experience + Devices

Microsoft's E+D group, responsible for supporting products such as Teams and Office modernized the Microsoft 365 infrastructure by transitioning to Windows containers on Azure Kubernetes Service (AKS), aiming for more consistent, efficient DevOps within strict security and compliance frameworks.

The transition enabled Microsoft 365 developers to focus more on innovation and iterating quickly, leveraging the benefits of AKS like security-optimized hosting, automated compliance checks, and centralized capacity management, thereby accelerating development while optimizing resource utilization and costs.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices-ml-ops -->

# Machine learning operations (MLOps) best practices in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes best practices and considerations to keep in mind when using MLOps in AKS. For more information on MLOps, see [Machine learning operations (MLOps) for AI and machine learning workflows](concepts-machine-learning-ops).

## Infrastructure as code (IaC)

[IaC](/en-us/devops/deliver/what-is-infrastructure-as-code) enables consistent and reproducible infrastructure provisioning and management for a range of application types. With intelligent application deployments, your IaC implementation might change throughout the AI pipeline, as the compute power and resources needed for inferencing, serving, training, and fine-tuning models can vary. Defining and versioning IaC templates for your AI developer teams can help ensure consistency and cost-effectiveness across job types while demystifying their individual hardware requirements and accelerating the deployment process.

## Containerization

Managing your model weights, metadata, and configurations in container images allows for portability, simplified versioning, and reduced storage costs over time. With containerization, you can:

- Leverage existing container images, especially for large language models (LLMs) ranging in millions to billions of parameters in size and stable diffusion models, stored in secure container registries.
- Avoid single point of failure (SPOF) in your pipeline with the use of multiple lightweight containers containing the unique dependencies for each task instead of maintaining one large image.
- Store large text/image datasets outside of your base container image and reference them when needed at runtime.

[Get started with the Kubernetes AI Toolchain Operator](ai-toolchain-operator) to deploy a high performance LLM on AKS in a matter of minutes.

## Model management and versioning

Model management and versioning are essential for tracking changes to your models over time. By versioning your models, you can:

- Maintain consistency across your model containers for ease of deployment in different environments.
- Employ parameter-efficient fine-tuning (PEFT) methods to iterate faster on a subset of model weights and maintain new versions in lightweight containers.

## Automation

Automation is key to reducing manual errors, increasing efficiency, and ensuring consistency across the ML lifecycle. By automating tasks, you can:

- Integrate alerting tools to automatically trigger a vector ingestion flow as new data flows into your application.
- Set model performance thresholds to track degradations and trigger retraining pipelines.

## Scalability and resource management

Scalability and resource management are critical for ensuring that your AI pipeline can handle the demands of your application. By optimizing your resource usage, you can:

- Integrate tools that efficiently use your allocated CPU, GPU, and memory resources through distributed computing and multiple levels of parallelism (for example: data, model, and pipeline parallelism).
- Enable autoscaling on your compute resources to support high model request volumes at peak times and scale down in off-peak hours.
- Similar to your traditional applications, plan for disaster recovery by following
[AKS resiliency and reliability best practices](ha-dr-overview).

## Security and compliance

Security and compliance are critical for protecting your data and ensuring that your AI pipeline meets regulatory requirements. By implementing security and compliance best practices, you can:

- Integrate common vulnerability and exposure (CVE) scanning to detect common vulnerabilities on open-source model container images.
- Use
[Microsoft Defender for Containers](/en-us/azure/defender-for-cloud/defender-for-containers-introduction)for model container images stored in your Azure Container Registry.

- Use
- Maintain an audit trail of the ingested data, model changes, and metrics to remain compliant with your organizational policies.

## Next steps

Learn about best practices across other areas of your application deployment and operations on AKS:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/monitor-gpu-metrics -->

# Learn about NVIDIA GPU metrics to optimize GPU performance and utilization on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Efficient placement and optimization of GPU workloads often requires visibility into resource utilization and performance. Managed GPU metrics on AKS (preview) provide automated collection and exposure of GPU utilization, memory, and performance data across NVIDIA GPU-enabled node pools. This enables platform administrators to optimize cluster resources and developers to tune and debug workloads with limited manual instrumentation.

In this article, you learn about GPU metrics collected by the NVIDIA Data Center GPU Manager [(DCGM) exporter](https://github.com/NVIDIA/dcgm-exporter/tree/main) with [a fully managed GPU-enabled node pool (preview)](aks-managed-gpu-nodes) in Azure Kubernetes Service (AKS).

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Prerequisites

- An AKS cluster with
[a fully managed GPU-enabled node pool (preview)](aks-managed-gpu-nodes)and ensure that the[GPUs are schedulable](use-nvidia-gpu#confirm-that-gpus-are-schedulable). - A
[sample GPU workload](use-nvidia-gpu#run-a-gpu-enabled-workload)deployed to your node pool.

## Limitations

- Managed GPU metrics is not currently supported with
[Azure Managed Prometheus or Azure Managed Grafana](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable).

## Verify that managed GPU components are installed

After creating your managed NVIDIA GPU node pool (preview) following [these instructions](aks-managed-gpu-nodes), confirm that the GPU software components were installed with the [az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command:

```
az aks nodepool show \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--name <node-pool-name> \
```


Your output should include the following values:

```
...
...
"gpuInstanceProfile": …
"gpuProfile": {
"driver": "Install"
},
...
...
```


## Understanding GPU metrics

### GPU Utilization Metrics

GPU Utilization metrics show the percentage of time the GPU’s cores are actively processing work. High values indicate that the GPU is heavily used, which is generally desirable for workloads like training or data processing. Interpretation of this metric should consider the type of workload: AI training typically keeps utilization high, while inference may have intermittent utilization due to bursty traffic.

Memory Utilization: Shows the percentage of GPU memory in use. High memory usage without high GPU utilization can indicate memory-bound workloads where the GPU waits on memory transfers. Low memory usage with low utilization may suggest the workload is too small to fully leverage the GPU.

SM (Streaming Multiprocessor) Efficiency: Measures the efficiency with which the GPU’s cores are used. A low SM efficiency indicates that cores are idle or underutilized due to workload imbalance or suboptimal kernel design. High efficiency is ideal for compute-heavy applications.

### Memory Metrics

Memory Bandwidth Utilization: Reflects how much of the theoretical memory bandwidth is being consumed. High bandwidth utilization with low compute utilization can indicate a memory-bound workload. Conversely, high utilization in both compute and memory bandwidth suggests a well-balanced workload.

Memory Errors: Tracks ECC (Error-Correcting Code) errors if enabled. A high number of errors may indicate hardware degradation or thermal issues and should be monitored for reliability.

### Temperature and Power Metrics

GPU Temperature: Indicates the operating temperature of the GPU. Sustained high temperatures can trigger thermal throttling, reducing performance. Ideal interpretation of this metric involves observing temperature relative to the GPU’s thermal limits and cooling capacity.

Power Usage: Shows instantaneous power draw. Comparing power usage to TDP (Thermal Design Power) helps understand whether the GPU is being pushed to its limits. Sudden drops in power may indicate throttling or underutilization.

### Clocks and Frequency Metrics

GPU Clock: The actual operating frequency of the GPU. Combined with utilization, this helps determine if the GPU is throttling or underperforming relative to its potential.

Memory Clock: Operating frequency of GPU memory. Memory-bound workloads may benefit from higher memory clocks; a mismatch between memory and compute utilization can highlight bottlenecks.

### PCIe and NVLink Metrics

PCIe Bandwidth: Measures the throughput over the PCIe bus. Low utilization with heavy workloads may suggest CPU-GPU communication is not a bottleneck. High utilization could point to data transfer limitations impacting performance.

NVLink Bandwidth: This metric is similar to PCIe bandwidth but specific to NVLink interconnects, and relevant in multi-GPU systems for cross-GPU communication. High NVLink usage with low SM utilization may indicate synchronization or data transfer delays.

### Error and Reliability Metrics

Retired Pages and XID Errors: Track GPU memory errors and critical failures. Frequent occurrences signal potential hardware faults and require attention for long-running workloads.

### Interpretation Guidance

DCGM metrics should always be interpreted contextually with the type of your workload on AKS. A high compute-intensive workload should ideally show high GPU and SM utilization, high memory bandwidth usage, stable temperatures below throttling thresholds, and power draw near but below TDP.

Memory-bound workloads might show high memory utilization and bandwidth but lower compute utilization. Anomalies such as low utilization with high temperature or power consumption often indicate throttling, inefficient scheduling, or system-level bottlenecks.

Monitoring trends over time rather than single snapshots is critical. Sudden drops in utilization or spikes in errors often reveal underlying issues before they impact production workloads. Comparing metrics across multiple GPUs can also help identify outliers or misbehaving devices in a cluster. Understanding these metrics in combination, rather than isolation, provides the clearest insight into GPU efficiency and workload performance.

## Common GPU metrics

The following NVIDIA DCGM metrics are commonly evaluated for performance of GPU node pools on Kubernetes:

| GPU Metric Name | Meaning | Typical Range / Indicator | Usage Tip |
|---|---|---|---|
`DCGM_FI_DEV_GPU_UTIL` |
GPU utilization (% time GPU cores are active) | 0–100% (higher is better) | Monitor per-node and per-pod; low values may indicate CPU or I/O bottlenecks |
`DCGM_FI_DEV_SM_UTIL` |
Streaming Multiprocessor efficiency (% active cores) | 0–100% | Low values with high memory usage indicate a memory-bound workload |
`DCGM_FI_DEV_FB_USED` |
Framebuffer memory used (bytes) | 0 to total memory | Use pod GPU memory limits and track per-pod memory usage |
`DCGM_FI_DEV_FB_FREE` |
Free GPU memory (bytes) | 0 to total memory | Useful for scheduling and to avoid OOM errors |
`DCGM_FI_DEV_MEMORY_UTIL` |
Memory utilization (%) | 0–100% | Combine with GPU/SM utilization to determine memory-bound workloads |
`DCGM_FI_DEV_MEMORY_CLOCK` |
Current memory clock frequency (MHz) | 0 to max memory clock | Low values under high memory utilization may indicate throttling |
`DCGM_FI_DEV_POWER_USAGE` |
Instantaneous power usage (Watts) | 0 to TDP | Drops during high utilization may indicate throttling |
`DCGM_FI_DEV_TEMPERATURE` |
GPU temperature (°C) | ~30–85°C normal | Alert on sustained high temperatures |
`DCGM_FI_DEV_NVLINK_RX` |
NVLink receive bandwidth utilization (%) | 0–100% | Multi-GPU synchronization bottleneck if high with low SM utilization |
`DCGM_FI_DEV_XID_ERRORS` |
GPU critical errors reported by driver | Typically 0 | Immediate investigation required; can taint node in Kubernetes |

To learn about the full suite of GPU metrics, visit [NVIDIA DCGM](https://docs.nvidia.com/datacenter/dcgm/latest/user-guide/index.html) Upstream documentation.

## Next steps

- Track your
[GPU node health](gpu-health-monitoring)with Node Problem Detector (NPD) - Create
[multi-instance GPU](gpu-multi-instance)node pools on AKS - Explore the
[AI toolchain operator add-on](ai-toolchain-operator)for AI inferencing and fine-tuning

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-managed-identity -->

# Use a managed identity in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides step-by-step instructions on how to enable and use a system-assigned, user-assigned, or pre-created kubelet managed identity in Azure Kubernetes Service (AKS).

## AKS managed identity prerequisites

Read the

[Overview of managed identities in Azure Kubernetes Service (AKS)](managed-identity-overview)to understand the different types of managed identities available in AKS and how you can use them to securely access Azure resources.Before running the examples in this article, set your subscription as the current active subscription using the

command.`az account set`

`az account set --subscription <subscription-id>`

Create an Azure resource group if you don't already have one by calling the

command.`az group create`

`az group create \ --name <resource-group-name> \ --location <location>`


### Azure CLI version minimum requirements

- Make sure you have Azure CLI version 2.23.0 or later installed. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - To
[use a pre-created kubelet managed identity](use-managed-identity#create-a-kubelet-managed-identity), you need Azure CLI version 2.26.0 or later installed. - To update an existing cluster to use a
[system-assigned managed identity](use-managed-identity#update-an-existing-aks-cluster-to-use-a-system-assigned-managed-identity)or[a user-assigned managed identity](use-managed-identity#update-an-existing-cluster-to-use-a-user-assigned-managed-identity), you need Azure CLI version 2.49.0 or later installed.

### Limitations

Moving or migrating a managed identity-enabled cluster to a different tenant isn't supported.

If the cluster has Microsoft Entra pod-managed identity (

`aad-pod-identity`

) enabled, Node-Managed Identity (NMI) pods modify the iptables of the nodes to intercept calls to the Azure Instance Metadata (IMDS) endpoint. This configuration means any request made to the IMDS endpoint is intercepted by NMI, even if a particular pod doesn't use`aad-pod-identity`

.The AzurePodIdentityException custom resource definition (CRD) can be configured to specify that requests to the IMDS endpoint that originate from a pod matching labels defined in the CRD should be proxied without any processing in NMI. Exclude the system pods with the

`kubernetes.azure.com/managedby: aks`

label in*kube-system*namespace in`aad-pod-identity`

by configuring the AzurePodIdentityException CRD. For more information, see[Use Microsoft Entra pod-managed identities in Azure Kubernetes Service](use-azure-ad-pod-identity).To configure an exception, install the

[mic-exception YAML](https://github.com/Azure/aad-pod-identity/blob/master/deploy/infra/mic-exception.yaml).AKS doesn't support the use of a system-assigned managed identity when using a custom private DNS zone.

The USDOD Central, USDOD East, and USGov Iowa regions in Azure US Government cloud don't support creating a cluster with a user-assigned managed identity.


A pre-created kubelet managed identity must be a user-assigned managed identity.

The China East and China North regions in Microsoft Azure operated by 21Vianet aren't supported.

Important

All Microsoft Defender for Cloud features will be officially retired in the Azure in China region on August 18, 2026. Due to this upcoming retirement, Azure in China customers are no longer able to onboard new subscriptions to the service. A new subscription is any subscription that was not already onboarded to the Microsoft Defender for Cloud service prior to August 18, 2025, the date of the retirement announcement. For more information on the retirement, see

[Microsoft Defender for Cloud Deprecation in Microsoft Azure Operated by 21Vianet Announcement](https://aka.ms/mdcretirementinchina).Customers should work with their account representatives for Microsoft Azure operated by 21Vianet to assess the impact of this retirement on their own operations.


### Update cluster considerations

When you update a cluster, consider the following information:

- An update only works if there's a VHD update to consume. If you're running the latest VHD, you need to wait until the next VHD is available in order to perform the update.
- The Azure CLI ensures your addon's permission is correctly set after migrating. If you're not using the Azure CLI to perform the migrating operation, you need to handle the addon identity's permission by yourself. For an example using an Azure Resource Manager (ARM) template, see
[Assign Azure roles using ARM templates](/en-us/azure/role-based-access-control/role-assignments-template). - If your cluster was using
`--attach-acr`

to pull from images from Azure Container Registry (ACR), you need to run the`az aks update --resource-group <resource-group-name> --name <aks-cluster-name> --attach-acr <acr-resource-id>`

command after updating your cluster to let the newly created kubelet used for managed identity get the permission to pull from ACR. Otherwise, you won't be able to pull from ACR after the update.

## Enable a system-assigned managed identity on an AKS cluster

### Enable a system-assigned managed identity on a new AKS cluster

A system-assigned managed identity is enabled by default when you create a new AKS cluster.

Create an AKS cluster using the

command.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --generate-ssh-keys`


### Update an existing AKS cluster to use a system-assigned managed identity

Update an existing AKS cluster from a service principal to a system-assigned managed identity using the

command with the`az aks update`

`--enable-managed-identity`

parameter.`az aks update \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --enable-managed-identity`

After you update the cluster to use a system-assigned managed identity instead of a service principal, the control plane and pods use the system-assigned managed identity for authorization when accessing other services in Azure. Kubelet continues using a service principal until you also upgrade your agent pool. You can use the

`az aks nodepool upgrade --resource-group <resource-group-name> --cluster-name <aks-cluster-name> --name <node-pool-name> --node-image-only`

command on your nodes to update to a managed identity. A node pool upgrade causes downtime for your AKS cluster as the nodes in the node pools are cordoned, drained, and reimaged.

## Get the principal ID of a system-assigned managed identity

Get the principal ID for the cluster's system-assigned managed identity using the

command.`az aks show`

`CLIENT_ID=$(az aks show \ --name <aks-cluster-name> \ --resource-group <resource-group-name> \ --query identity.principalId \ --output tsv)`


## Add a role assignment for a system-assigned managed identity

Assign an Azure RBAC role to the system-assigned managed identity using the

command.`az role assignment create`

For a VNet, attached Azure disk, static IP address, or route table outside the default worker node resource group, you need to assign the

`Network Contributor`

role on the custom resource group.The following example assigns the

**Network Contributor**role to the system-assigned managed identity. The role assignment is scoped to the resource group that contains the VNet.`az role assignment create \ --assignee <client-id> \ --role "Network Contributor" \ --scope <custom-resource-group-id>`

Note

It can take up to 60 minutes for the permissions granted to your cluster's managed identity to propagate.


## Create a user-assigned managed identity

If you don't yet have a user-assigned managed identity resource, create one using the

command.`az identity create`

`az identity create \ --name <identity-name> \ --resource-group <resource-group-name>`

Your output should resemble the following example output:

`{ "clientId": "<client-id>", "clientSecretUrl": "<clientSecretUrl>", "id": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<identity-name>", "location": "<location>", "name": "<identity-name>", "principalId": "<principal-id>", "resourceGroup": "<resource-group-name>", "tags": {}, "tenantId": "<tenant-id>", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


## Get the principal ID of the user-assigned managed identity

Get the principal ID of the user-assigned managed identity using the

command.`az identity show`

`CLIENT_ID=$(az identity show \ --name <identity-name> \ --resource-group <resource-group-name> \ --query principalId \ --output tsv)`


## Get the resource ID of the user-assigned managed identity

Get the resource ID of the user-assigned managed identity using the

command.`az identity show`

`RESOURCE_ID=$(az identity show \ --name <identity-name> \ --resource-group <resource-group-name> \ --query id \ --output tsv)`


## Assign an Azure RBAC role to the user-assigned managed identity

Add a role assignment for the user-assigned managed identity using the

command.`az role assignment create`

The following example assigns the

**Key Vault Secrets User**role to the user-assigned managed identity to grant it permissions to access secrets in a key vault. The role assignment is scoped to the key vault resource:`az role assignment create \ --assignee <client-id> \ --role "Key Vault Secrets User" \ --scope "<keyvault-resource-id>"`

Note

It can take up to 60 minutes for the permissions granted to your cluster's managed identity to propagate.


## Enable a user-assigned managed identity on an AKS cluster

### Enable a user-assigned managed identity on a new AKS cluster

Create an AKS cluster with the user-assigned managed identity using the

command. Include the`az aks create`

`--assign-identity`

parameter and pass in the resource ID for the user-assigned managed identity:`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --network-plugin azure \ --vnet-subnet-id <vnet-subnet-id> \ --dns-service-ip 10.2.0.10 \ --service-cidr 10.2.0.0/24 \ --assign-identity $RESOURCE_ID \ --generate-ssh-keys`


### Update an existing cluster to use a user-assigned managed identity

Update an existing cluster to use a user-assigned managed identity using the

command. Include the`az aks update`

`--assign-identity`

parameter and pass in the resource ID for the user-assigned managed identity:`az aks update \ --resource-group <resource-group-name> \ --name <cluster-name> \ --enable-managed-identity \ --assign-identity $RESOURCE_ID`

The output for a successful cluster update to use a user-assigned managed identity should resemble the following example output:

`"identity": { "principalId": null, "tenantId": null, "type": "UserAssigned", "userAssignedIdentities": { "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<identity-name>": { "clientId": "<client-id>", "principalId": "<principal-id>" } } },`

Note

Migrating a managed identity for the control plane from system-assigned to user-assigned doesn't result in any downtime for control plane and agent pools. Control plane components continue to the old system-assigned identity for up to several hours, until the next token refresh.


## Determine which type of managed identity a cluster is using

Verify which type of managed identity your cluster is using with the

command.`az aks show`

`az aks show \ --name <aks-cluster-name> \ --resource-group <resource-group-name> \ --query identity.type \ --output tsv`

If the cluster is using a managed identity, the value of the

*type*property will be either**SystemAssigned**or**UserAssigned**.If the cluster is using a service principal, the value of the

*type*property will be null. Consider upgrading your cluster to use a managed identity.

## Create a kubelet managed identity

If you don't have a kubelet managed identity, create one using the

command.`az identity create`

`az identity create \ --name <kubelet-identity-name> \ --resource-group <resource-group-name>`

Your output should resemble the following example output:

`{ "clientId": "<client-id>", "clientSecretUrl": "<clientSecretUrl>", "id": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<kubelet-identity-name>", "location": "<location>", "name": "<kubelet-identity-name>", "principalId": "<principal-id>", "resourceGroup": "<resource-group-name>", "tags": {}, "tenantId": "<tenant-id>", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


## Assign an RBAC role to the kubelet managed identity

Assign the

`acrpull`

role on the kubelet managed identity using thecommand.`az role assignment create`

`az role assignment create \ --assignee <kubelet-client-id> \ --role "acrpull" \ --scope "<acr-registry-id>"`


## Enable a kubelet managed identity on an AKS cluster

### Enable a kubelet managed identity on a new AKS cluster

Create an AKS cluster with your existing identities using the

command.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --network-plugin azure \ --vnet-subnet-id <vnet-subnet-id> \ --dns-service-ip 10.2.0.10 \ --service-cidr 10.2.0.0/24 \ --assign-identity <identity-resource-id> \ --assign-kubelet-identity <kubelet-identity-resource-id> \ --generate-ssh-keys`

A successful AKS cluster creation using a kubelet managed identity should result in output similar to the following:

`"identity": { "principalId": null, "tenantId": null, "type": "UserAssigned", "userAssignedIdentities": { "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<identity-name>": { "clientId": "<client-id>", "principalId": "<principal-id>" } } }, "identityProfile": { "kubeletidentity": { "clientId": "<client-id>", "objectId": "<object-id>", "resourceId": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<kubelet-identity-name>" } },`


### Update an existing cluster to use a kubelet managed identity

To update an existing cluster to use the kubelet managed identity, first get the current control plane managed identity for your AKS cluster.

Warning

Updating the kubelet managed identity upgrades your AKS cluster's node pools, make sure you have the right availability configurations, such as Pod Disruption Budgets, configured before executing this to avoid workload disruption or execute this during a maintenance window.

Confirm your AKS cluster is using the user-assigned managed identity using the

command.`az aks show`

`az aks show \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --query "servicePrincipalProfile"`

If your cluster is using a managed identity, the output shows

`clientId`

with a value of**msi**. A cluster using a service principal shows an object ID. For example:`# The cluster is using a managed identity. { "clientId": "msi" }`

After confirming your cluster is using a managed identity, find the managed identity's resource ID using the

command.`az aks show`

`az aks show --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --query "identity"`

For a user-assigned managed identity, your output should look similar to the following example output:

`{ "principalId": null, "tenantId": null, "type": "UserAssigned", "userAssignedIdentities": <identity-resource-id> "clientId": "<client-id>", "principalId": "<principal-id>" },`

Update your cluster with your existing identities using the

command. Provide the resource ID of the user-assigned managed identity for the control plane for the`az aks update`

`assign-identity`

argument. Provide the resource ID of the kubelet managed identity for the`assign-kubelet-identity`

argument.`az aks update \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --enable-managed-identity \ --assign-identity <identity-resource-id> \ --assign-kubelet-identity <kubelet-identity-resource-id>`

Your output for a successful cluster update using your own kubelet managed identity should resemble the following example output:

`"identity": { "principalId": null, "tenantId": null, "type": "UserAssigned", "userAssignedIdentities": { "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<identity-name>": { "clientId": "<client-id>", "principalId": "<principal-id>" } } }, "identityProfile": { "kubeletidentity": { "clientId": "<client-id>", "objectId": "<object-id>", "resourceId": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<kubelet-identity-name>" } },`


## Get the properties of the kubelet managed identity

Get the properties of the kubelet managed identity using the

command and query on the`az aks show`

`identityProfile.kubeletidentity`

property.`az aks show \ --name <aks-cluster-name> \ --resource-group <resource-group-name> \ --query "identityProfile.kubeletidentity"`


## Next steps

- Use
[Azure Resource Manager templates](/en-us/azure/templates/microsoft.containerservice/managedclusters)to create a managed identity-enabled cluster. - Learn how to
[use kubelogin](kubelogin-authentication)for all supported Microsoft Entra authentication methods in AKS.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kubernetes-helm -->

# Install existing applications with Helm in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage the lifecycle of Kubernetes applications. Similar to Linux package managers, such as *APT* and *Yum*, you can use Helm to manage Kubernetes charts, which are packages of preconfigured Kubernetes resources.

This article shows you how to configure and use Helm in a Kubernetes cluster on Azure Kubernetes Service (AKS).

## Before you begin

- This article assumes you have an existing AKS cluster. If you need an AKS cluster, create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[Azure portal](learn/quick-kubernetes-deploy-portal). - Your AKS cluster needs to have
**an integrated ACR**. For details on creating an AKS cluster with an integrated ACR, see[Authenticate with Azure Container Registry from Azure Kubernetes Service](cluster-container-registry-integration#create-a-new-acr). - You also need the Helm CLI installed, which is the client that runs on your development system. It allows you to start, stop, and manage applications with Helm. If you use the Azure Cloud Shell, the Helm CLI is already installed. For installation instructions on your local platform, see
[Installing Helm](https://helm.sh/docs/intro/install/).

Important

Helm is intended to run on Linux nodes. If you have Windows Server nodes in your cluster, you must ensure that Helm pods are only scheduled to run on Linux nodes. You also need to ensure that any Helm charts you install are also scheduled to run on the correct nodes. The commands in this article use [node-selectors](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector) to make sure pods are scheduled to the correct nodes, but not all Helm charts may expose a node selector. You can also consider using other options on your cluster, such as [taints](operator-best-practices-advanced-scheduler).

## Verify your version of Helm

Use the

`helm version`

command to verify you have Helm 3 installed.`helm version`

The following example output shows Helm version 3.0.0 installed:

`version.BuildInfo{Version:"v3.0.0", GitCommit:"e29ce2a54e96cd02ccfce88bee4f58bb6e2a28b6", GitTreeState:"clean", GoVersion:"go1.13.4"}`


## Install an application with Helm v3

### Add Helm repositories

Add the

*ingress-nginx*repository using the[helm repo](https://helm.sh/docs/intro/quickstart/#initialize-a-helm-chart-repository)command.`helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx`


### Find Helm charts

Search for precreated Helm charts using the

[helm search](https://helm.sh/docs/intro/using_helm/#helm-search-finding-charts)command.`helm search repo ingress-nginx`

The following condensed example output shows some of the Helm charts available for use:

`NAME CHART VERSION APP VERSION DESCRIPTION ingress-nginx/ingress-nginx 4.7.0 1.8.0 Ingress controller for Kubernetes using NGINX a...`

Update the list of charts using the

[helm repo update](https://helm.sh/docs/intro/using_helm/#helm-repo-working-with-repositories)command.`helm repo update`

The following example output shows a successful repo update:

`Hang tight while we grab the latest from your chart repositories... ...Successfully got an update from the "ingress-nginx" chart repository Update Complete. ⎈ Happy Helming!⎈`


## Import the Helm chart images into your ACR

This article uses the [NGINX ingress controller Helm chart](https://github.com/kubernetes/ingress-nginx/tree/main/charts/ingress-nginx), which relies on three container images.

Use

`az acr import`

to import the NGINX ingress controller images into your ACR.`REGISTRY_NAME=<REGISTRY_NAME> CONTROLLER_REGISTRY=registry.k8s.io CONTROLLER_IMAGE=ingress-nginx/controller CONTROLLER_TAG=v1.8.0 PATCH_REGISTRY=registry.k8s.io PATCH_IMAGE=ingress-nginx/kube-webhook-certgen PATCH_TAG=v20230407 DEFAULTBACKEND_REGISTRY=registry.k8s.io DEFAULTBACKEND_IMAGE=defaultbackend-amd64 DEFAULTBACKEND_TAG=1.5 az acr import --name $REGISTRY_NAME --source $CONTROLLER_REGISTRY/$CONTROLLER_IMAGE:$CONTROLLER_TAG --image $CONTROLLER_IMAGE:$CONTROLLER_TAG az acr import --name $REGISTRY_NAME --source $PATCH_REGISTRY/$PATCH_IMAGE:$PATCH_TAG --image $PATCH_IMAGE:$PATCH_TAG az acr import --name $REGISTRY_NAME --source $DEFAULTBACKEND_REGISTRY/$DEFAULTBACKEND_IMAGE:$DEFAULTBACKEND_TAG --image $DEFAULTBACKEND_IMAGE:$DEFAULTBACKEND_TAG`

Note

In addition to importing container images into your ACR, you can also import Helm charts into your ACR. For more information, see

[Push and pull Helm charts to an Azure container registry](/en-us/azure/container-registry/container-registry-helm-repos).

### Run Helm charts

Install Helm charts using the

[helm install](https://helm.sh/docs/intro/using_helm/#helm-install-installing-a-package)command and specify a release name and the name of the chart to install.Tip

The following example creates a Kubernetes namespace for the ingress resources named

*ingress-basic*and is intended to work within that namespace. Specify a namespace for your own environment as needed.`ACR_URL=<REGISTRY_URL> # Create a namespace for your ingress resources kubectl create namespace ingress-basic # Use Helm to deploy an NGINX ingress controller helm install ingress-nginx ingress-nginx/ingress-nginx \ --version 4.0.13 \ --namespace ingress-basic \ --set controller.replicaCount=2 \ --set controller.nodeSelector."kubernetes\.io/os"=linux \ --set controller.image.registry=$ACR_URL \ --set controller.image.image=$CONTROLLER_IMAGE \ --set controller.image.tag=$CONTROLLER_TAG \ --set controller.image.digest="" \ --set controller.admissionWebhooks.patch.nodeSelector."kubernetes\.io/os"=linux \ --set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz \ --set controller.admissionWebhooks.patch.image.registry=$ACR_URL \ --set controller.admissionWebhooks.patch.image.image=$PATCH_IMAGE \ --set controller.admissionWebhooks.patch.image.tag=$PATCH_TAG \ --set defaultBackend.nodeSelector."kubernetes\.io/os"=linux \ --set defaultBackend.image.registry=$ACR_URL \ --set defaultBackend.image.image=$DEFAULTBACKEND_IMAGE \ --set defaultBackend.image.tag=$DEFAULTBACKEND_TAG \ --set defaultBackend.image.digest=""`

The following condensed example output shows the deployment status of the Kubernetes resources created by the Helm chart:

`NAME: nginx-ingress LAST DEPLOYED: Wed Jul 28 11:35:29 2021 NAMESPACE: ingress-basic STATUS: deployed REVISION: 1 TEST SUITE: None NOTES: The ingress-nginx controller has been installed. It may take a few minutes for the LoadBalancer IP to be available. You can watch the status by running 'kubectl --namespace ingress-basic get services -o wide -w nginx-ingress-ingress-nginx-controller' ...`

Get the

*EXTERNAL-IP*of your service using the`kubectl get services`

command.`kubectl --namespace ingress-basic get services -o wide -w ingress-nginx-ingress-nginx-controller`

The following example output shows the

*EXTERNAL-IP*for the*ingress-nginx-ingress-nginx-controller*service:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE SELECTOR nginx-ingress-ingress-nginx-controller LoadBalancer 10.0.254.93 <EXTERNAL_IP> 80:30004/TCP,443:30348/TCP 61s app.kubernetes.io/component=controller,app.kubernetes.io/instance=nginx-ingress,app.kubernetes.io/name=ingress-nginx`


### List releases

Get a list of releases installed on your cluster using the

`helm list`

command.`helm list --namespace ingress-basic`

The following example output shows the

*ingress-nginx*release deployed in the previous step:`NAME NAMESPACE REVISION UPDATED STATUS CHART APP VERSION ingress-nginx ingress-basic 1 2021-07-28 11:35:29.9623734 -0500 CDT deployed ingress-nginx-3.34.0 0.47.0`


### Clean up resources

Deploying a Helm chart creates Kubernetes resources like pods, deployments, and services.

Clean up resources using the

[helm uninstall](https://helm.sh/docs/intro/using_helm/#helm-uninstall-uninstalling-a-release)command and specify your release name.`helm uninstall --namespace ingress-basic ingress-nginx`

The following example output shows the release named

*ingress-nginx*has been uninstalled:`release "nginx-ingress" uninstalled`

Delete the entire sample namespace along with the resources using the

`kubectl delete`

command and specify your namespace name.`kubectl delete namespace ingress-basic`


## Next steps

For more information about managing Kubernetes application deployments with Helm, see the Helm documentation.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-performance-ebpf-host-routing -->

# Overview of eBPF Host Routing (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

As containerized workloads scale across distributed environments, the need for high-performance, low-latency networking becomes critical. eBPF Host Routing is a performance-focused feature within [Advanced Container Networking Services (ACNS)](advanced-container-networking-services-overview) that uses extended Berkeley Packet Filter (eBPF) technology to optimize traffic flow in Kubernetes clusters. Legacy routing on Kubernetes hosts introduces overhead in the form of iptables and netfilter rule processing in the host network namespace. eBPF Host Routing has benefits over legacy host routing by:

- Implementing the routing logic in eBPF programs.
- Allowing Cilium eBPF to bypass iptables in the host namespace.

This direct path reduces the number of hops and processing layers, resulting in faster packet delivery.

## Key benefits

Reduced latency - Bypassing iptables in host results in lower pod-to-pod latency

Increased throughput - Compared to legacy routing, significant improvements can be observed for pod-to-pod traffic between nodes

Reduced CPU usage - Due to removing iptables-based SNAT and routing logic, a modest reduction of CPU usage

Use cases for eBPF Host Routing are performance-critical workloads such as high-throughput microservices, real-time services, or AI/ML workloads. Ensure deployment environment meets the requirements before enabling.

## Components of eBPF Host Routing

** iptables blocker** - An init container that prevents any future installation of iptables rules in the host network namespace (such rules will be bypassed when eBPF host routing is enabled).

** IP Masquerade Agent** - When eBPF Host Routing is active, Cilium takes over SNAT responsibilities using BPF-based masquerading.

`ip-masq-agent`

remains running to maintain consistent behavior if eBPF Host Routing is later disabled; however, its iptables rules are ignored while eBPF Host Routing is active.## Considerations

Enabling eBPF Host Routing causes iptables rules in the host network namespace to be bypassed. Hence, AKS attempts to detect and block enablement of eBPF Host Routing on clusters where iptables rules are in use in the host network namespace.

On clusters with eBPF host routing enabled, AKS blocks attempts to install iptables rules in the host network namespace. Trying to bypass this block may cause the cluster to be inoperational.


## Limitations

eBPF host routing is currently incompatible with nodes running OSes other than Ubuntu 24.04, or Azure Linux 3.0. eBPF host routing is currently also not supported with Confidential VMs and Pod Sandboxing.

eBPF Host Routing can only be enabled for all nodes in a cluster. Hybrid node scenarios aren't supported.

Windows nodes aren't supported by Azure CNI Powered by Cilium, and by extension, eBPF Host Routing.

Istio add-on can't be used along with eBPF Host Routing enabled clusters.

Dual stack networking isn't supported.


## Pricing

Important

Advanced Container Networking Services is a paid offering. For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Next steps

Learn how to enable

[eBPF Host Routing](how-to-enable-ebpf-host-routing)on AKS.For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).Explore Container Network Observability features in Advanced Container Networking Services in

[What is Container Network Observability?](container-network-observability-metrics).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade -->

# Upgrading Azure Kubernetes Service clusters and node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

An Azure Kubernetes Service (AKS) cluster needs to be periodically updated to ensure security and compatibility with the latest features. There are two components of an AKS cluster that are necessary to maintain:

*Cluster Kubernetes version*: Part of the AKS cluster lifecycle involves performing upgrades to the latest Kubernetes version. It’s important that you upgrade to apply the latest security releases and to get access to the latest Kubernetes features, as well as to stay within the[AKS support window](supported-kubernetes-versions#kubernetes-version-support-policy).*Node image version*: AKS regularly provides new node images with the latest OS and runtime updates. It's beneficial to upgrade your nodes' images regularly to ensure support for the latest AKS features and to apply essential security patches and hot fixes.

For Linux nodes, node image security patches and hotfixes may be performed without your initiation as *unattended updates*. These updates are automatically applied, but AKS doesn't automatically reboot your Linux nodes to complete the update process. You're required to use a tool like [kured](node-updates-kured) or [node image upgrade](node-image-upgrade) to reboot the nodes and complete the cycle.

The following table summarizes the details of updating each component:

| Component name | Frequency of upgrade | Planned Maintenance supported | Supported operation methods | Supported operation methods (Multi-Cluster) | Documentation link |
|---|---|---|---|---|---|
| Cluster Kubernetes version upgrade (minor) | Roughly every three months | Yes | Automatic, Manual | Automatic, Manual |
|

[AKS release tracker](release-tracker)[Upgrade an AKS cluster](upgrade-cluster),[Multi-cluster upgrade](/en-us/azure/kubernetes-fleet/concepts-update-orchestration)**Linux**: weekly**Windows**: monthly[AKS node image upgrade](node-image-upgrade),[Multi-cluster upgrade](/en-us/azure/kubernetes-fleet/concepts-update-orchestration)[AKS node security patches](concepts-vulnerability-management#worker-nodes)## Multi-cluster upgrade

When you have multiple clusters, an important practice that you should include as part of your upgrade process is remembering to follow commonly used deployment and testing patterns. Testing an upgrade in a development or test environment before deployment in production is an important step to ensure application functionality and compatibility with the target environment. It can help you identify and fix any errors, bugs, or issues that might affect the performance, security, or usability of the application or underlying infrastructure.

[Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/overview) has built-in support for [multi-cluster upgrades](/en-us/azure/kubernetes-fleet/concepts-update-orchestration) which implements the best practice above to minimize application disruptions caused by cluster upgrades. Besides allowing you to customize the order of upgrades of multiple clusters, it also allows you to use consistent node OS image versions across clusters in different regions.

## Automatic upgrades

Automatic upgrades can be performed through [auto upgrade channels](auto-upgrade-cluster) or via [GitHub Actions](node-upgrade-github-actions).

[Automatic multi-cluster upgrades](/en-us/azure/kubernetes-fleet/update-automation) can be performed through [Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/overview) to adopt the best practice of testing and verifying an upgrade in a development or test environment before production.

## Planned maintenance

[Planned maintenance](planned-maintenance) allows you to schedule weekly maintenance windows that will update your control plane and your kube-system pods, helping to minimize workload impact.

## Troubleshooting

To find details and solutions to specific issues, view the following troubleshooting guides:

## Next steps

For more information what cluster operations may trigger specific upgrade events, upgrade best practices, and other considerations, see the [AKS operator's guide on patching](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/quickstart-helm -->

# Quickstart: Develop on Azure Kubernetes Service (AKS) with Helm

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Helm](https://helm.sh/) is an open-source packaging tool that helps you install and manage the lifecycle of Kubernetes applications. Similar to Linux package managers like *APT* and *Yum*, Helm manages Kubernetes charts, which are packages of pre-configured Kubernetes resources.

In this quickstart, you use Helm to package and run an application on AKS. For information on installing an existing application using Helm, see [Install existing applications with Helm in AKS](kubernetes-helm).

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). [Azure CLI](/en-us/cli/azure/install-azure-cli)or[Azure PowerShell](/en-us/powershell/azure/install-az-ps)installed.[Helm v3 installed](https://helm.sh/docs/intro/install/).

## Create an Azure Container Registry

You need to store your container images in an Azure Container Registry (ACR) to run your application in your AKS cluster using Helm. Your registry name must be unique within Azure and contain 5-50 alphanumeric characters. Only lowercase characters are allowed. The *Basic* SKU is a cost-optimized entry point for development purposes that provides a balance of storage and throughput.

Create an Azure resource group using the

[az group create](/en-us/cli/azure/group#az-group-create)command. The following example creates a resource group named*myResourceGroup*in the*eastus*location.`az group create --name myResourceGroup --location eastus`

Create an Azure Container Registry with a unique name by calling the

[az acr create](/en-us/cli/azure/acr#az-acr-create)command. The following example creates an ACR named*myhelmacr*with the*Basic*SKU.`az acr create --resource-group myResourceGroup --name myhelmacr --sku Basic`

Your output should look similar to the following condensed example output. Take note of your

*loginServer*value for your ACR to use in a later step.`{ "adminUserEnabled": false, "creationDate": "2023-12-26T22:36:23.998425+00:00", "id": "/subscriptions/<ID>/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myhelmacr", "location": "eastus", "loginServer": "myhelmacr.azurecr.io", "name": "myhelmacr", "networkRuleSet": null, "provisioningState": "Succeeded", "resourceGroup": "myResourceGroup", "sku": { "name": "Basic", "tier": "Basic" }, "status": null, "storageAccount": null, "tags": {}, "type": "Microsoft.ContainerRegistry/registries" }`


## Create an AKS cluster

Your new AKS cluster needs access to your ACR to pull the container images and run them.

Create an AKS cluster using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command with the`--attach-acr`

parameter to grant the cluster access to your ACR. The following example creates an AKS cluster named*myAKSCluster*and grants it access to the*myhelmacr*ACR. Make sure you replace`myhelmacr`

with the name of your ACR.`az aks create --resource-group myResourceGroup --name myAKSCluster --location eastus --attach-acr myhelmacr --generate-ssh-keys`


## Connect to your AKS cluster

To connect a Kubernetes cluster locally, you use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell.

Install

`kubectl`

locally using the[az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli)command.`az aks install-cli`

Configure

`kubectl`

to connect to your Kubernetes cluster using the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. The following command gets credentials for the AKS cluster named*myAKSCluster*in*myResourceGroup*.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Download the sample application

This quickstart uses the [Azure Vote application](https://github.com/Azure-Samples/azure-voting-app-redis.git).

Clone the application from GitHub using the

`git clone`

command.`git clone https://github.com/Azure-Samples/azure-voting-app-redis.git`

Navigate to the

`azure-vote`

directory using the`cd`

command.`cd azure-voting-app-redis/azure-vote/`


## Build and push the sample application to ACR

Build and push the image to your ACR using the

[az acr build](/en-us/cli/azure/acr#az-acr-build)command. The following example builds an image named*azure-vote-front:v1*and pushes it to the*myhelmacr*ACR. Make sure you replace`myhelmacr`

with the name of your ACR.`az acr build --image azure-vote-front:v1 --registry myhelmacr --file Dockerfile .`


Note

You can also import Helm charts into your ACR. For more information, see [Push and pull Helm charts to an Azure container registry](/en-us/azure/container-registry/container-registry-helm-repos).

## Create your Helm chart

Generate your Helm chart using the

`helm create`

command.`helm create azure-vote-front`

Update

*azure-vote-front/Chart.yaml*to add a dependency for the*redis*chart from the`https://charts.bitnami.com/bitnami`

chart repository and update`appVersion`

to`v1`

, as shown in the following example:Note

The container image versions shown in this guide have been tested to work with this example but may not be the latest version available.

`apiVersion: v2 name: azure-vote-front description: A Helm chart for Kubernetes dependencies: - name: redis version: 17.3.17 repository: https://charts.bitnami.com/bitnami ... # This is the version number of the application being deployed. This version number should be # incremented each time you make changes to the application. appVersion: v1`

Update your Helm chart dependencies using the

`helm dependency update`

command.`helm dependency update azure-vote-front`

Update

*azure-vote-front/values.yaml*with the following changes.- Add a
*redis*section to set the image details, container port, and deployment name. - Add a
*backendName*for connecting the frontend portion to the*redis*deployment. - Change
*image.repository*to`<loginServer>/azure-vote-front`

. - Change
*image.tag*to`v1`

. - Change
*service.type*to*LoadBalancer*.

For example:

`replicaCount: 1 backendName: azure-vote-backend-master redis: image: registry: mcr.microsoft.com repository: oss/bitnami/redis tag: 6.0.8 fullnameOverride: azure-vote-backend auth: enabled: false image: repository: myhelmacr.azurecr.io/azure-vote-front pullPolicy: IfNotPresent tag: "v1" ... service: type: LoadBalancer port: 80 ...`

- Add a
Add an

`env`

section to*azure-vote-front/templates/deployment.yaml*to pass the name of the*redis*deployment.`... containers: - name: {{ .Chart.Name }} securityContext: {{- toYaml .Values.securityContext | nindent 12 }} image: "{{ .Values.image.repository }}:{{ .Values.image.tag | default .Chart.AppVersion }}" imagePullPolicy: {{ .Values.image.pullPolicy }} env: - name: REDIS value: {{ .Values.backendName }} ...`


## Run your Helm chart

Install your application using your Helm chart using the

`helm install`

command.`helm install azure-vote-front azure-vote-front/`

It takes a few minutes for the service to return a public IP address. Monitor progress using the

`kubectl get service`

command with the`--watch`

argument.`kubectl get service azure-vote-front --watch`

When the service is ready, the

`EXTERNAL-IP`

value changes from`<pending>`

to an IP address. Press`CTRL+C`

to stop the`kubectl`

watch process.`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE azure-vote-front LoadBalancer 10.0.18.228 <pending> 80:32021/TCP 6s ... azure-vote-front LoadBalancer 10.0.18.228 52.188.140.81 80:32021/TCP 2m6s`

Navigate to your application's load balancer in a browser using the

`<EXTERNAL-IP>`

to see the sample application.

## Delete the cluster

Remove your resource group, AKS cluster, Azure container registry, container images stored in the ACR, and all related resources using the

[az group delete](/en-us/cli/azure/group#az-group-delete)command with the`--yes`

parameter to confirm deletion and the`--no-wait`

parameter to return to the command prompt without waiting for the operation to complete.`az group delete --name myResourceGroup --yes --no-wait`


Note

If you created your AKS cluster with a system-assigned managed identity (the default identity option in this quickstart), the identity is managed by the platform and doesn't require removal.

If you created your AKS cluster with a service principal, the service principal isn't removed when you delete the cluster. To remove the service principal, see [AKS service principal considerations and deletion](kubernetes-service-principal#considerations-when-using-a-service-principal).

## Next steps

For more information about using Helm, see the [Helm documentation](https://helm.sh/docs/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/open-ai-secure-access-quickstart -->

# Secure access to Azure OpenAI from Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to secure access to Azure OpenAI from Azure Kubernetes Service (AKS) using Microsoft Entra Workload ID. You learn how to:

- Enable workload identities on an AKS cluster.
- Create an Azure user-assigned managed identity.
- Create a Microsoft Entra ID federated credential.
- Enable workload identity on a Kubernetes Pod.

Note

We recommend using Microsoft Entra Workload ID and managed identities on AKS for Azure OpenAI access because it enables a secure, passwordless authentication process for accessing Azure resources.

## Before you begin

- You need an Azure account with an active subscription. If you don't have one,
[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - This article builds on
[Deploy an application that uses OpenAI on AKS](open-ai-quickstart). You should complete that article before you begin this one. - You need a custom domain name enabled on your Azure OpenAI account to use for Microsoft Entra authorization. For more information, see
[Custom subdomain names for Azure AI services](/en-us/azure/ai-services/cognitive-services-custom-subdomains).

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Enable Microsoft Entra Workload ID on an AKS cluster

The Microsoft Entra Workload ID and OIDC Issuer Endpoint features aren't enabled on AKS by default. You must enable them on your AKS cluster before you can use them.

Set the resource group name and AKS cluster resource group name variables.

`# Set the resource group variable RG_NAME=myResourceGroup # Set the AKS cluster name based on the resource group variable AKS_NAME=$(az resource list --resource-group $RG_NAME --resource-type Microsoft.ContainerService/managedClusters --query "[0].name" -o tsv)`

Enable the Microsoft Entra Workload ID and OIDC Issuer Endpoint features on your existing AKS cluster using the

command.`az aks update`

`az aks update \ --resource-group $RG_NAME \ --name $AKS_NAME \ --enable-workload-identity \ --enable-oidc-issuer`

Get the AKS OIDC Issuer Endpoint URL using the

command.`az aks show`

`AKS_OIDC_ISSUER=$(az aks show --resource-group $RG_NAME --name $AKS_NAME --query "oidcIssuerProfile.issuerUrl" -o tsv)`


## Create an Azure user-assigned managed identity

Create an Azure user-assigned managed identity using the

command.`az identity create`

`# Set the managed identity name variable MANAGED_IDENTITY_NAME=myIdentity # Create the managed identity az identity create \ --resource-group $RG_NAME \ --name $MANAGED_IDENTITY_NAME`

Get the managed identity client ID and object ID using the

command.`az identity show`

`# Get the managed identity client ID MANAGED_IDENTITY_CLIENT_ID=$(az identity show --resource-group $RG_NAME --name $MANAGED_IDENTITY_NAME --query clientId -o tsv) # Get the managed identity object ID MANAGED_IDENTITY_OBJECT_ID=$(az identity show --resource-group $RG_NAME --name $MANAGED_IDENTITY_NAME --query principalId -o tsv)`

Get the Azure OpenAI resource ID using the

command.`az resource list`

`AOAI_RESOURCE_ID=$(az resource list --resource-group $RG_NAME --resource-type Microsoft.CognitiveServices/accounts --query "[0].id" -o tsv)`

Grant the managed identity access to the Azure OpenAI resource using the

command.`az role assignment create`

`az role assignment create \ --role "Cognitive Services OpenAI User" \ --assignee-object-id $MANAGED_IDENTITY_OBJECT_ID \ --assignee-principal-type ServicePrincipal \ --scope $AOAI_RESOURCE_ID`


## Create a Microsoft Entra ID federated credential

Set the federated credential, namespace, and service account variables.

`# Set the federated credential name variable FEDERATED_CREDENTIAL_NAME=myFederatedCredential # Set the namespace variable SERVICE_ACCOUNT_NAMESPACE=default # Set the service account variable SERVICE_ACCOUNT_NAME=ai-service-account`

Create the federated credential using the

command.`az identity federated-credential create`

`az identity federated-credential create \ --name ${FEDERATED_CREDENTIAL_NAME} \ --resource-group ${RG_NAME} \ --identity-name ${MANAGED_IDENTITY_NAME} \ --issuer ${AKS_OIDC_ISSUER} \ --subject system:serviceaccount:${SERVICE_ACCOUNT_NAMESPACE}:${SERVICE_ACCOUNT_NAME}`


## Use Microsoft Entra Workload ID on AKS

To use Microsoft Entra Workload ID on AKS, you need to make a few changes to the `ai-service`

deployment manifest.

### Create a ServiceAccount

Get the kubeconfig for your cluster using the

command.`az aks get-credentials`

`az aks get-credentials \ --resource-group $RG_NAME \ --name $AKS_NAME`

Create a Kubernetes ServiceAccount using the

command.`kubectl apply`

`kubectl apply -f - <<EOF apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: ${MANAGED_IDENTITY_CLIENT_ID} name: ${SERVICE_ACCOUNT_NAME} namespace: ${SERVICE_ACCOUNT_NAMESPACE} EOF`


### Enable Microsoft Entra Workload ID on the Pod

Set the Azure OpenAI resource name, endpoint, and deployment name variables.

`# Get the Azure OpenAI resource name AOAI_NAME=$(az resource list \ --resource-group $RG_NAME \ --resource-type Microsoft.CognitiveServices/accounts \ --query "[0].name" -o tsv) # Get the Azure OpenAI endpoint AOAI_ENDPOINT=$(az cognitiveservices account show \ --resource-group $RG_NAME \ --name $AOAI_NAME \ --query properties.endpoint -o tsv) # Get the Azure OpenAI deployment name AOAI_DEPLOYMENT_NAME=$(az cognitiveservices account deployment list \ --resource-group $RG_NAME \ --name $AOAI_NAME \ --query "[0].name" -o tsv)`

Redeploy the

`ai-service`

with the ServiceAccount and the`azure.workload.identity/use`

annotation set to`true`

using thecommand.`kubectl apply`

`kubectl apply -f - <<EOF apiVersion: apps/v1 kind: Deployment metadata: name: ai-service spec: replicas: 1 selector: matchLabels: app: ai-service template: metadata: labels: app: ai-service azure.workload.identity/use: "true" spec: serviceAccountName: $SERVICE_ACCOUNT_NAME nodeSelector: "kubernetes.io/os": linux containers: - name: ai-service image: ghcr.io/azure-samples/aks-store-demo/ai-service:latest ports: - containerPort: 5001 env: - name: USE_AZURE_OPENAI value: "True" - name: USE_AZURE_AD value: "True" - name: AZURE_OPENAI_DEPLOYMENT_NAME value: "${AOAI_DEPLOYMENT_NAME}" - name: AZURE_OPENAI_ENDPOINT value: "${AOAI_ENDPOINT}" resources: requests: cpu: 20m memory: 50Mi limits: cpu: 50m memory: 128Mi EOF`


### Test the application

Verify the new pod is running using the

command.`kubectl get pods`

`kubectl get pods --selector app=ai-service`

Get the pod environment variables using the

command. The output demonstrates that the Azure OpenAI API key no longer exists in the Pod's environment variables.`kubectl describe pod`

`kubectl describe pod --selector app=ai-service`

Open a new terminal and get the IP of the store admin service using the following

`echo`

command.`echo "http://$(kubectl get svc/store-admin -o jsonpath='{.status.loadBalancer.ingress[0].ip}')"`

Open a web browser and navigate to the IP address from the previous step.

Select

**Products**. You should be able to add a new product and get a description for it using Azure OpenAI.

## Next steps

In this article, you learned how to secure access to Azure OpenAI from Azure Kubernetes Service (AKS) using Microsoft Entra Workload ID.

For more information on Microsoft Entra Workload ID, see [Microsoft Entra Workload ID](workload-identity-overview).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-group-managed-service-accounts -->

# Enable Group Managed Service Accounts (GMSA) for your Windows Server nodes on your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Group Managed Service Accounts (GMSA)](/en-us/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview) is a managed domain account for multiple servers that provides automatic password management, simplified service principal name (SPN) management, and the ability to delegate management to other administrators. With Azure Kubernetes Service (AKS), you can enable GMSA on your Windows Server nodes, which allows containers running on Windows Server nodes to integrate with and be managed by GMSA.

## Prerequisites

- Kubernetes 1.19 or greater. To check your version, see
[Check for available upgrades](upgrade-aks-cluster#check-for-available-aks-cluster-upgrades). To upgrade your version, see[Upgrade AKS cluster](upgrade-aks-cluster). - Azure CLI version 2.35.0 or greater. To find the version, run
`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). [Managed identities](use-managed-identity)enabled on your AKS cluster.- Permissions to create or update an Azure Key Vault.
- Permissions to configure GMSA on Active Directory Domain Service or on-premises Active Directory.
- The domain controller must have Active Directory Web Services enabled and must be reachable on port 9389 by the AKS cluster.

Note

Microsoft also provides a purpose-built PowerShell module to configure gMSA on AKS. For more information, see [gMSA on Azure Kubernetes Service](/en-us/virtualization/windowscontainers/manage-containers/gmsa-aks-ps-module).

## Configure GMSA on Active Directory domain controller

To use GMSA with AKS, you need a standard domain user credential to access the GMSA credential configured on your domain controller. To configure GMSA on your domain controller, see [Get started with Group Managed Service Accounts](/en-us/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts). For the standard domain user credential, you can use an existing user or create a new one, as long as it has access to the GMSA credential.

Important

You must use either Active Directory Domain Service or on-premises Active Directory. At this time, you can't use Microsoft Entra ID to configure GMSA with an AKS cluster.

## Store the standard domain user credentials in Azure Key Vault

Your AKS cluster uses the standard domain user credentials to access the GMSA credentials from the domain controller. To provide secure access to those credentials for the AKS cluster, you should store them in Azure Key Vault.

If you don't already have an Azure key vault, create one using the

command.`az keyvault create`

`az keyvault create --resource-group myResourceGroup --name myGMSAVault`

Store the standard domain user credential as a secret in your key vault using the

command. The following example stores the domain user credential with the key`az keyvault secret set`

*GMSADomainUserCred*in the*myGMSAVault*key vault.`az keyvault secret set --vault-name myGMSAVault --name "GMSADomainUserCred" --value "$Domain\\$DomainUsername:$DomainUserPassword"`

Note

Make sure to use the fully qualified domain name for the domain.


### Optional: Use a custom virtual network with custom DNS

You need to configure your domain controller through DNS so it's reachable by the AKS cluster. You can configure your network and DNS outside of your AKS cluster to allow your cluster to access the domain controller. Alternatively, you can use Azure CNI to configure a custom virtual network with a custom DNS on your AKS cluster to provide access to your domain controller. For more information, see [Configure Azure CNI networking in Azure Kubernetes Service (AKS)](configure-azure-cni).

### Optional: Configure more than one DNS server

If you want to configure more than one DNS server for Windows GMSA in your AKS cluster, don't specify `--gmsa-dns-server`

or `v--gmsa-root-domain-name`

. Instead, you can add multiple DNS servers in the virtual network by selecting *Custom DNS* and adding the DNS servers.

### Optional: Use your own kubelet identity for your cluster

To provide the AKS cluster access to your key vault, the cluster kubelet identity needs access to your key vault. When you create a cluster with managed identity enabled, a kubelet identity is automatically created by default.

You can either [grant access to your key vault for the identity after cluster creation](#enable-gmsa-on-existing-cluster) or create your own identity before cluster creation using the following steps:

Create a kubelet identity using the

command.`az identity create`

`az identity create --name myIdentity --resource-group myResourceGroup`

Get the ID of the identity using the

command and set it to a variable named`az identity list`

`MANAGED_ID`

.`MANAGED_ID=$(az identity list --query "[].id" -o tsv)`

Grant the identity access to your key vault using the

command.`az keyvault set-policy`

`az keyvault set-policy --name "myGMSAVault" --object-id $MANAGED_ID --secret-permissions get`


## Enable GMSA on a new AKS cluster

Create administrator credentials to use during cluster creation. The following commands prompt you for a username and set it to

`WINDOWS_USERNAME`

for use in a later command.`echo "Please enter the username to use as administrator credentials for Windows Server nodes on your cluster: " && read WINDOWS_USERNAME`

Create an AKS cluster using the

command with the following parameters:`az aks create`

`--enable-windows-gmsa`

: Enables GMSA for the cluster.`--gmsa-dns-server`

: The IP address of the DNS server.`--gmsa-root-domain-name`

: The root domain name of the DNS server.

`DNS_SERVER=<IP address of DNS server> ROOT_DOMAIN_NAME="contoso.com" az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --vm-set-type VirtualMachineScaleSets \ --network-plugin azure \ --load-balancer-sku standard \ --windows-admin-username $WINDOWS_USERNAME \ --enable-windows-gmsa \ --gmsa-dns-server $DNS_SERVER \ --gmsa-root-domain-name $ROOT_DOMAIN_NAME \ --generate-ssh-keys`

Note

If you're using a custom virtual network, you need to specify the virtual network ID using the

`vnet-subnet-id`

parameter, and you might need to also add the`docker-bridge-address`

,`dns-service-ip`

, and`service-cidr`

parameters depending on your configuration.If you created your own identity for the kubelet identity, use the

`assign-kubelet-identity`

parameter to specify your identity.When you specify the

`--gmsa-dns-server`

and`--gmsa-root-domain-name`

parameters, a DNS forward rule is added to the`kube-system/coredns`

ConfigMap. This rule forwards the DNS requests for`$ROOT_DOMAIN_NAME`

from the pods to the`$DNS_SERVER`

.`$ROOT_DOMAIN_NAME:53 { errors cache 30 log forward . $DNS_SERVER }`


Add a Windows Server node pool using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --os-type Windows \ --name npwin \ --node-count 1`


### Enable GMSA on existing cluster

Enable GMSA on an existing cluster with Windows Server nodes and managed identities enabled using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--resource-group myResourceGroup \
--name myAKSCluster \
--enable-windows-gmsa \
--gmsa-dns-server $DNS_SERVER \
--gmsa-root-domain-name $ROOT_DOMAIN_NAME
```


## Grant access to your key vault for the kubelet identity

Note

Skip this step if you provided your own identity for the kubelet identity.

Grant access to your key vault for the kubelet identity using the [ az keyvault set-policy](/en-us/cli/azure/keyvault#az-keyvault-set-policy) command.

```
MANAGED_ID=$(az aks show -g myResourceGroup -n myAKSCluster --query "identityProfile.kubeletidentity.objectId" -o tsv)
az keyvault set-policy --name "myGMSAVault" --object-id $MANAGED_ID --secret-permissions get
```


## Install GMSA cred spec

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Create a new YAML named

*gmsa-spec.yaml*and paste in the following YAML. Make sure you replace the placeholders with your own values. Placeholders are indicated with angle brackets (`<>`

), for example replace`<GMSA_ACCOUNT_USERNAME>`

with an account name like`gmsa-account`

.`apiVersion: windows.k8s.io/v1 kind: GMSACredentialSpec metadata: name: aks-gmsa-spec # This name can be changed, but it will be used as a reference in the pod spec credspec: ActiveDirectoryConfig: GroupManagedServiceAccounts: - Name: <GMSA_ACCOUNT_USERNAME> # GMSA account username like gmsa-account Scope: <NETBIOS_DOMAIN_NAME> # NetBIOS domain name like contoso - Name: <GMSA_ACCOUNT_USERNAME> # GMSA account username like gmsa-account Scope: <DNS_DOMAIN_NAME> # Fully qualified domain name like contoso.com HostAccountConfig: PluginGUID: '{CCC2A336-D7F3-4818-A213-272B7924213E}' PortableCcgVersion: "1" PluginInput: "ObjectId=<MANAGED_IDENTITY_OBJECT_ID>;SecretUri=https://<KEY_VAULT_NAME>.vault.azure.net/secrets/<KEY_VAULT_SECRET_NAME>" # MANAGED_IDENTITY_OBJECT_ID is managed identity object ID GUID # KEY_VAULT_NAME is the name of your key vault, like myGMSAVault # KEY_VAULT_SECRET_NAME is the name of the key vault secret you created, like GMSADomainUserCred CmsPlugins: - ActiveDirectory DomainJoinConfig: DnsName: <DNS_DOMAIN_NAME> # Fully qualified domain name like contoso.com DnsTreeName: <DNS_ROOT_DOMAIN_NAME> # Root domain name like contoso.com Guid: <AD_DOMAIN_OBJECT_GUID> # Domain object GUID like 66aa66aa-bb77-cc88-dd99-00ee00ee00ee MachineAccountName: <GMSA_ACCOUNT_USERNAME> # GMSA account username like gmsa-account NetBiosName: <NETBIOS_DOMAIN_NAME> # NetBIOS domain name like contoso Sid: <AD_DOMAIN_OBJECT_SID> # Domain object SID like S-1-5-21-1111111111-2222222222-3333333333`


Note

AKS upgraded the `apiVersion`

of `GMSACredentialSpec`

from `windows.k8s.io/v1alpha1`

to `windows.k8s.io/v1`

in release v20230903.

Create a new YAML named

*gmsa-role.yaml*and paste in the following YAML.`apiVersion: rbac.authorization.k8s.io/v1 kind: ClusterRole metadata: name: aks-gmsa-role rules: - apiGroups: ["windows.k8s.io"] resources: ["gmsacredentialspecs"] verbs: ["use"] resourceNames: ["aks-gmsa-spec"]`

Create a new YAML file named

*gmsa-role-binding.yaml*and paste in the following YAML.`apiVersion: rbac.authorization.k8s.io/v1 kind: RoleBinding metadata: name: allow-default-svc-account-read-on-aks-gmsa-spec namespace: default subjects: - kind: ServiceAccount name: default namespace: default roleRef: kind: ClusterRole name: aks-gmsa-role apiGroup: rbac.authorization.k8s.io`

Apply the changes from

*gmsa-spec.yaml*,*gmsa-role.yaml*, and*gmsa-role-binding.yaml*using the`kubectl apply`

command.`kubectl apply -f gmsa-spec.yaml kubectl apply -f gmsa-role.yaml kubectl apply -f gmsa-role-binding.yaml`


## Verify GMSA installation

Create a new YAML named

*gmsa-demo.yaml*and paste in the following YAML.`--- kind: ConfigMap apiVersion: v1 metadata: labels: app: gmsa-demo name: gmsa-demo namespace: default data: run.ps1: | $ErrorActionPreference = "Stop" Write-Output "Configuring IIS with authentication." # Add required Windows features, since they are not installed by default. Install-WindowsFeature "Web-Windows-Auth", "Web-Asp-Net45" # Create simple ASP.NET page. New-Item -Force -ItemType Directory -Path 'C:\inetpub\wwwroot\app' Set-Content -Path 'C:\inetpub\wwwroot\app\default.aspx' -Value 'Authenticated as <B><%=User.Identity.Name%></B>, Type of Authentication: <B><%=User.Identity.AuthenticationType%></B>' # Configure IIS with authentication. Import-Module IISAdministration Start-IISCommitDelay (Get-IISConfigSection -SectionPath 'system.webServer/security/authentication/windowsAuthentication').Attributes['enabled'].value = $true (Get-IISConfigSection -SectionPath 'system.webServer/security/authentication/anonymousAuthentication').Attributes['enabled'].value = $false (Get-IISServerManager).Sites[0].Applications[0].VirtualDirectories[0].PhysicalPath = 'C:\inetpub\wwwroot\app' Stop-IISCommitDelay Write-Output "IIS with authentication is ready." C:\ServiceMonitor.exe w3svc --- apiVersion: apps/v1 kind: Deployment metadata: labels: app: gmsa-demo name: gmsa-demo namespace: default spec: replicas: 1 selector: matchLabels: app: gmsa-demo template: metadata: labels: app: gmsa-demo spec: securityContext: windowsOptions: gmsaCredentialSpecName: aks-gmsa-spec containers: - name: iis image: mcr.microsoft.com/windows/servercore/iis:windowsservercore-ltsc2019 imagePullPolicy: IfNotPresent command: - powershell args: - -File - /gmsa-demo/run.ps1 volumeMounts: - name: gmsa-demo mountPath: /gmsa-demo volumes: - configMap: defaultMode: 420 name: gmsa-demo name: gmsa-demo nodeSelector: kubernetes.io/os: windows --- apiVersion: v1 kind: Service metadata: labels: app: gmsa-demo name: gmsa-demo namespace: default spec: ports: - port: 80 targetPort: 80 selector: app: gmsa-demo type: LoadBalancer`

Apply the changes from

*gmsa-demo.yaml*using the`kubectl apply`

command.`kubectl apply -f gmsa-demo.yaml`

Get the IP address of the sample application using the

`kubectl get service`

command.`kubectl get service gmsa-demo --watch`

Initially, the

`EXTERNAL-IP`

for the`gmsa-demo`

service shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE gmsa-demo LoadBalancer 10.0.37.27 <pending> 80:30572/TCP 6s`

When the

`EXTERNAL-IP`

address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`gmsa-demo LoadBalancer 10.0.37.27 EXTERNAL-IP 80:30572/TCP 2m`

Open a web browser to the external IP address of the

`gmsa-demo`

service.Authenticate with the

`$NETBIOS_DOMAIN_NAME\$AD_USERNAME`

and password and confirm you see`Authenticated as $NETBIOS_DOMAIN_NAME\$AD_USERNAME, Type of Authentication: Negotiate`

.

### Disable GMSA on an existing cluster

Disable GMSA on an existing cluster with Windows Server nodes using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--resource-group myResourceGroup \
--name myAKSCluster \
--disable-windows-gmsa
```


You can reenable GMSA on an existing cluster by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

## Troubleshooting

### No authentication is prompted when loading the page

If the page loads, but you aren't prompted to authenticate, use the `kubectl logs POD_NAME`

command to display the logs of your pod and verify you see *IIS with authentication is ready*.

Windows containers don't show logs on kubectl by default. To enable Windows containers to show logs, you need to embed the Log Monitor tool on your Windows image. For more information, see [Windows Container Tools](https://github.com/microsoft/windows-container-tools).

### Connection timeout when trying to load the page

If you receive a connection timeout when trying to load the page, verify the sample app is running using the `kubectl get pods --watch`

command. Sometimes the external IP address for the sample app service is available before the sample app pod is running.

### Pod fails to start and a winapi error shows in the pod events

If your pod doesn't start after running the `kubectl get pods --watch`

command and waiting several minutes, use the `kubectl describe pod POD_NAME`

command. If you see a *winapi error* in the pod events, it's likely an error in your GMSA cred spec configuration. Verify all the replacement values in *gmsa-spec.yaml* are correct, rerun `kubectl apply -f gmsa-spec.yaml`

, and redeploy the sample application.

### Container Credential Guard event logs show the directory service isn't available errors

If you see this error message, it might indicate that DNS queries are failing due to blocked TCP fallback.

When gMSA is enabled, the system performs DNS lookups to locate domain controllers, for example `_ldap._tcp.dc._msdcs.<domain>`

. In large Active Directory environments, these responses can exceed the 512-byte UDP limit. When the UDP limit is reached, the DNS server sets the truncated (TC) flag, prompting CoreDNS to retry the query over TCP, as required by [RFC5966](https://datatracker.ietf.org/doc/html/rfc5966). This fallback to TCP is essential for completing the authentication flow. If network security group (NSG) or firewall rules block TCP traffic on port 53, the DNS resolution, and therefore gMSA sign in fails.

To verify if this error is occurring in your environment, enable [CoreDNS query logging](coredns-custom) and use the `kubectl logs --namespace kube-system -l k8s-app=kube-dns`

command to view CoreDNS logs.

Look for patterns like this, where UDP responses are truncated and TCP retries fail:

```
[INFO] 10.123.123.200:62380 - 2 "ANY IN _ldap._tcp.dc._msdcs.contoso.com. udp 49 false 512" NOERROR qr,aa,tc,rd,ra 1357 0.003399698s
[INFO] 10.123.123.200:64233 - 2 "ANY IN _ldap._tcp.dc._msdcs.contoso.com. tcp 49 false 65535" - - 0 6.009670817s
[ERROR] plugin/errors: 2 _ldap._tcp.dc._msdcs.contoso.com. ANY: read tcp 10.123.123.11:55216-><DNS server IP>:53: i/o timeout
```


To resolve this error, we recommend updating your NSG or firewall rules to explicitly allow DNS traffic over TCP on port 53. This update will ensure that large DNS responses can be successfully retried over TCP, enabling the authentication flow to complete as expected.

## Next steps

For more information, see [Windows containers considerations with Azure Kubernetes Service (AKS)](windows-vs-linux-containers).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/managed-identity-overview -->

# Overview of managed identities in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of system-assigned and user-assigned managed identities in AKS, including how they work, role assignments, and AKS-specific managed identity features.

To enable a managed identity on a new or existing AKS cluster, see [Use a managed identity in Azure Kubernetes Service (AKS)](use-managed-identity). For more information about managed identities in Azure, see the [Managed identities for Azure resources documentation](/en-us/entra/identity/managed-identities-azure-resources/).

Note

The system-assigned and user-assigned identity types differ from a [workload identity](workload-identity-overview), which is intended for use by an application running on a pod.

## AKS managed identity authorization flow

AKS clusters use system-assigned or user-assigned [managed identities](/en-us/entra/identity/managed-identities-azure-resources/overview) to request tokens from Microsoft Entra. These tokens help authorize access to other resources running in Azure. You assign an [Azure role-based access control (Azure RBAC)](/en-us/azure/role-based-access-control/overview) role to the managed identity to grant it permissions to a particular Azure resource. For example, you can grant permissions to a managed identity to access secrets in an Azure key vault for use by the cluster.

### Managed identity behavior in AKS

When you deploy an AKS cluster, a system-assigned managed identity is created for you by default. You can also create the cluster with a user-assigned managed identity, or update an existing cluster to a different type of managed identity.

If your cluster already uses a managed identity and you change the identity type (for example, from system-assigned to user-assigned), there's a delay while control plane components switch to the new identity. Control plane components continue to use the old identity until its token expires. After the token refreshes, they switch to the new identity. This process can take several hours.

Note

It's also possible to create a cluster with an application [service principal](kubernetes-service-principal) rather that a managed identity. However, we recommend using a managed identity over an application service principal for security and ease of use. If you have an existing cluster that uses an application service principal, you can update it to use a managed identity.

### AKS identity and credential management

The Azure platform manages both system-assigned and user-assigned managed identities and their credentials, so you can authorize access from your applications without needing to provision or rotate any secrets.

## System-assigned managed identity

The following table summarizes the key characteristics of a system-assigned managed identity in AKS:

| Creation | Lifecycle | Sharing across resources | Common use cases |
|---|---|---|---|
| Created as part of an Azure resource, such as an AKS cluster | Tied to the lifecycle of the parent resource, so it gets deleted when the parent resource is deleted | Can only be associated with a single resource | • Workloads contained within a single Azure resource • Workloads that require independent identities |

### User-assigned managed identity

The following table summarizes the key characteristics of a user-assigned managed identity in AKS:

| Creation | Lifecycle | Sharing across resources | Common use cases |
|---|---|---|---|
| Created as a standalone Azure resource, and must exist prior to cluster creation | Independent of the lifecycle of any specific resource, so it requires manual deletion if no longer needed | Can be shared across multiple resources | • Workloads that run on multiple resources and can share a single identity • Workloads that require preauthorization to a secure resource as part of a provisioning process • Workloads where resources are recycled frequently but need consistent permissions |

### Pre-created kubelet managed identity

A pre-created kubelet managed identity is an optional user-assigned identity that kubelet can use to access other resources in Azure. This feature enables scenarios such as connection to Azure Container Registry (ACR) during cluster creation. If you don't specify a user-assigned managed identity for kubelet, AKS creates a user-assigned kubelet identity in the node resource group. For a user-assigned kubelet identity outside the default worker node resource group, you need to assign the [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) role on the kubelet identity for control plane managed identity.

## Role assignments for managed identities in AKS

You can assign an Azure RBAC role to a managed identity to grant the cluster permissions on another Azure resource. Azure RBAC supports both built-in and custom role definitions that specify levels of permissions. To assign a role, see [Steps to assign an Azure role](/en-us/azure/role-based-access-control/role-assignments-steps).

When you assign an Azure RBAC role to a managed identity, you must define the scope for the role. In general, it's a best practice to limit the scope of a role to the minimum privileges required by the managed identity. For more information on scoping Azure RBAC roles, see [Understand scope for Azure RBAC](/en-us/azure/role-based-access-control/scope-overview).

### Control plane managed identity role assignments

When you create and use your own VNet, attached Azure disks, static IP address, route table, or user-assigned kubelet identity where the resources are outside of the worker node resource group, the Azure CLI adds the role assignment automatically. If you're using an ARM template or another method, use the principal ID of the managed identity to perform a role assignment.

If you're not using the Azure CLI, but you're using your own VNet, attached Azure disks, static IP address, route table, or user-assigned kubelet identity that's outside of the worker node resource group, we recommend using a [user-assigned managed identity for the control plane](use-managed-identity#create-a-user-assigned-managed-identity).

When the control plane uses a system-assigned managed identity, the identity is created at the same time as the cluster, so the role assignment can't be performed until after cluster creation.

## Summary of managed identities used by AKS

AKS uses several managed identities for built-in services and add-ons. The following table summarizes the managed identities used by AKS, their use cases, default permissions, and whether you can bring your own identity:

| Identity | Name | Use case | Default permissions | Bring your own identity |
|---|---|---|---|---|
| Control plane | AKS cluster name | Used by AKS control plane components to manage cluster resources including ingress load balancers and AKS-managed public IPs, Cluster Autoscaler, Azure Disk, File, Blob CSI drivers | Contributor role for Node resource group | Supported |
| Kubelet | AKS cluster name-agentpool | Authentication with Azure Container Registry (ACR) | N/A for Kubernetes version 1.15 and later | Supported |
| Add-on | AzureNPM | No identity required | N/A | Unsupported |
| Add-on | AzureCNI network monitoring | No identity required | N/A | Unsupported |
| Add-on | azure-policy (gatekeeper) | No identity required | N/A | Unsupported |
| Add-on | Calico | No identity required | N/A | Unsupported |
| Add-on | application-routing | Manages Azure DNS and Azure Key Vault certificates | Key Vault Secrets User role for Key Vault, DNS Zone Contributor role for DNS zones, Private DNS Zone Contributor role for private DNS zones | Unsupported |
| Add-on | HTTPApplicationRouting | Manages required network resources | Reader role for node resource group, contributor role for DNS zone | Unsupported |
| Add-on | Ingress application gateway | Manages required network resources | Contributor role for node resource group | Unsupported |
| Add-on | omsagent | Used to send AKS metrics to Azure Monitor | Monitoring Metrics Publisher role | Unsupported |
| Add-on | Virtual-Node (ACIConnector) | Manages required network resources for Azure Container Instances (ACI) | Contributor role for node resource group | Unsupported |
| Add-on | Cost analysis | Used to gather cost allocation data | N/A | Supported |
| Workload identity | Microsoft Entra Workload ID | Enables applications to access cloud resources securely with Microsoft Entra Workload ID | N/A | Unsupported |

## Next step: Enable managed identities in AKS

To learn how to enable managed identities on a new or existing AKS cluster, see [Use a managed identity in Azure Kubernetes Service (AKS)](use-managed-identity).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/nvidia-gpu-operator -->

# Use NVIDIA GPU Operator on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The NVIDIA GPU Operator automates the management and deployment of all NVIDIA software components needed to provision GPU including driver installation, the [NVIDIA device plugin for Kubernetes](https://github.com/NVIDIA/k8s-device-plugin?tab=readme-ov-file), the NVIDIA container runtime, and more. Since the NVIDIA GPU Operator handles these components, it's not necessary to separately install the NVIDIA device plugin on your AKS cluster. This also means that the automatic GPU driver installation should be skipped in order to use the NVIDIA GPU Operator on AKS.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the Azure CLI version 2.72.2 or later installed to set the
`--gpu-driver`

field. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Note

GPU-enabled VMs contain specialized hardware subject to higher pricing and region availability. For more information, see the [pricing](free-standard-pricing-tiers) tool and [region availability](quotas-skus-regions).

## Limitations

- NVIDIA GPU Operator isn't supported for the following OS options: Windows Server versions,
[Flatcar Container Linux for AKS (preview)](flatcar-container-linux-for-aks), and[Azure Linux with OS Guard for AKS (preview)](use-azure-linux-os-guard).

## Get the credentials for your cluster

Get the credentials for your AKS cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. The following example command gets the credentials for the cluster

`myAKSCluster`

in the `myResourceGroup`

resource group:```
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```


Note

The NVIDIA GPU Operator is not compatible with multiple OS versions on the same AKS cluster.

Skip automatic GPU driver installation by creating an NVIDIA GPU-enabled node pool using the [

`az aks nodepool add`

][az-aks-nodepool-add] command and setting the API field`--gpu-driver`

to the value`none`

. Setting this API field to`none`

during node pool creation skips the default GPU driver installation, see[this example](gpu-cluster#skip-gpu-driver-installation). Any existing nodes aren't changed. You can scale the node pool to zero and then back up to make the change take effect.Follow the NVIDIA documentation to

[Install the GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html).Now that you successfully installed the GPU Operator, you can check that your

[GPUs are schedulable](gpu-cluster#confirm-that-gpus-are-schedulable)and[run a GPU workload](gpu-cluster#run-a-gpu-enabled-workload).

Note

There might be additional considerations to take when using the NVIDIA GPU Operator and deploying on SPOT instances. Please refer to [https://github.com/NVIDIA/gpu-operator/issues/577](https://github.com/NVIDIA/gpu-operator/issues/577)

## Next steps

[Monitor NVIDIA GPU metrics](monitor-gpu-metrics)using Azure Managed Prometheus and Azure Managed Grafana.- Learn more about
[Ray clusters on AKS](ray-overview).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-app-configuration-settings -->

# Configure the Azure App Configuration extension for your Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Once you [created the Azure App Configuration extension](azure-app-configuration), you can configure the extension to work best for you and your project using various configuration options, like:

- Configuring the replica count.
- Configuring the log verbosity.
- Configuring the installation namespace.

The extension enables you to configure Azure App Configuration extension settings by using the `--configuration-settings`

parameter in the Azure CLI.

Tip

For a list of available options, see [Azure App Configuration Kubernetes Provider helm values](https://raw.githubusercontent.com/Azure/AppConfiguration-KubernetesProvider/main/deploy/parameter/helm-values.yaml).

## Configure the replica count

The default replica count is `1`

. Create Azure App Configuration extension with customized replica count:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--configuration-settings "replicaCount=3"
```


Note

If configuration settings are sensitive and need to be protected (for example, cert-related information), pass the `--configuration-protected-settings`

parameter and the value will be protected from being read.

## Configure the log verbosity

The default log verbosity is `1`

. Create Azure App Configuration extension with customized log verbosity:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--configuration-settings "logVerbosity=3"
```


Log verbosity levels follow the [klog](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-instrumentation/logging.md#what-method-to-use) convention:

`0`

: Warning and error only.`1`

: Informational, this level is default.`2`

: Detailed steady state information.`3`

: Extended information about changes.`4`

: Debug level verbosity.`5`

: Trace level verbosity.

## Configure the Azure App Configuration extension namespace

The Azure App Configuration extension gets installed in the `azappconfig-system`

namespace by default. To override it, use `--release-namespace`

. Include the cluster `--scope`

to redefine the namespace.

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--scope cluster \
--release-namespace custom-namespace
```


## Show current configuration settings

Use the `az k8s-extension show`

command to show the current Azure App Configuration extension settings:

```
az k8s-extension show --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider
```


## Update configuration settings

To update your Azure App Configuration extension settings, recreate the extension with the desired state. For example, assume we installed the extension using the following configuration:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--configuration-settings "replicaCount=2"
```


To update the `replicaCount`

from two to three, use the following command:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--configuration-settings "replicaCount=3"
```


## Next Steps

Once you successfully install Azure App Configuration extension in your AKS cluster, try [quickstart](/en-us/azure/azure-app-configuration/quickstart-azure-kubernetes-service) to learn how to use it.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/optimize-aks-costs -->

# Optimize Azure Kubernetes Service (AKS) usage and costs

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides guidance on how to optimize your Azure Kubernetes Service (AKS) usage and costs. It covers guidance on the following topics:

## Automatic scaling

### Horizontal pod autoscaling

The * Horizontal Pod Autoscaler (HPA)* monitors resource demand and automatically updates a workload resource to automatically scale the number of pods to match demand. The response to increased load is to deploy more pods. If the load decreases and the number of pods is above the configured minimum, the autoscaler tells the workload resource to scale down.

The Metrics API gets data from the kubelet every 60 seconds, and the HPA checks the Metrics API every 15 seconds for any needed changes by default. This means that the HPA updates every 60 seconds. When you configure the HPA for a deployment, you define the minimum and maximum number of replicas that can run and the metrics that the HPA uses to determine when to scale.

For more information, see [Horizontal Pod Autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) and [Autoscale pods in AKS](tutorial-kubernetes-scale#autoscale-pods).

### Kubernetes event-driven autoscaling

The [Kubernetes Event-driven Autoscaler (KEDA)](https://keda.sh/) applies event-driven autoscaling to your workloads. KEDA works with the HPA and can extend functionality without overwriting or duplication.

You can use the KEDA add-on for AKS to scale your applications and leverage a [rich catalog of Azure KEDA scalers](https://keda.sh/docs/2.16/scalers/). For more information, see [Application autoscaling with the KEDA add-on](keda-about) and [Install the KEDA add-on for AKS](keda-deploy-add-on-cli).

### Vertical pod autoscaling

The * Vertical Pod Autoscaler (VPA)* automatically sets resource requests and limits on containers per workload based on past usage. The VPA frees up CPU and Memory for pods to ensure effective utilization of your AKS clusters. Over time, the VPA provides recommendations for resource usage.

For more information, see [Vertical pod autoscaling in Azure Kubernetes Service (AKS)](vertical-pod-autoscaler) and [Use the Vertical Pod Autoscaler (VPA) in Azure Kubernetes Service (AKS)](use-vertical-pod-autoscaler).

## Cluster right-sizing

### Right-size your cluster

It's important to * right-size your clusters* to optimize costs and performance. You can manually resize a cluster by adding or removing the nodes to meet the needs of your applications. You can also autoscale your cluster to automatically adjust the number of nodes in response to changing demands.

For more information, see [Resize Azure Kubernetes Service (AKS) clusters](resize-cluster).

### Cluster autoscaling

With the * cluster autoscaler*, you can automatically scale node pools based on resource usage and constraints, such as scaling up to schedule pending pods or scaling down to reduce costs for unused nodes. The

[cluster autoscaler profile](cluster-autoscaler-overview#cluster-autoscaler-profile)is a set of parameters that you can fine-tune to control the behavior of the cluster autoscaler.

For more information, see [Cluster autoscaling in Azure Kubernetes Service (AKS) overview](cluster-autoscaler-overview) and [Use the cluster autoscaler in Azure Kubernetes Service (AKS)](cluster-autoscaler).

### Node autoprovisioning (preview)

* Node autoprovisioning (NAP)* (preview), based on the open-source

[Karpenter](https://karpenter.sh/)project, helps you provision the right infrastructure based on the pending pod resource requirements of your workloads. With efficient bin-packing, you can consolidate your workloads onto the right-sized infrastructure to reduce operating costs.

For more information, see [Node autoprovisioning (preview) in Azure Kubernetes Service (AKS)](node-autoprovision).

## GPU optimizations

### GPU partitioning and sharing

GPU partitioning helps combat underutilization by splitting up or sharing GPUs across multiple workloads. The following sections cover different ways to partition and share GPUs in AKS.

#### Time-slicing

The [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/overview.html) enables the * time-slicing* of GPUs in Kubernetes clusters. With time-slicing, a system administrator can define a set of

*replicas*for a GPU, each of which can be handed out independently to a pod to run workloads on. You can apply cluster-wide default time-slicing configurations and node-specific configurations.


For more information, see [Time-slicing GPUs in Kubernetes](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/gpu-sharing.html).

#### Multi-processing service (MPS)

A single process might not utilize all the memory and compute bandwidth capacity available on a GPU. The * Multi-Process Service (MPS)* enables logical partitioning of memory and compute resources between workloads and allows kernel and memcopy operations from different processes to overlap on the GPU. MPS helps you achieve higher GPU utilization and shorter running times.


For more information, see [Multi-Process Service (MPS)](https://docs.nvidia.com/deploy/mps/index.html#mps).

#### Multi-instance GPUs (MIGs)

* Multi-instance GPUs (MIGs)* enable you to partition GPUs based on the NVIDIA Ampere and later architectures into separate and secure GPU instances for CUDA applications.


For more information, see [GPU Operator with MIG](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/gpu-operator-mig.html) and [Create a multi-instance GPU node pool in Azure Kubernetes Service (AKS)](gpu-multi-instance).

## Multitenancy

Multitenancy refers to the sharing of infrastructure across tenants, teams, and business units. The following table outlines different ways to implement multitenancy in AKS:

| Multitenancy type | Multitenancy level | Cluster pod density | Cost allocation | Ideal use case | Potential risks |
|---|---|---|---|---|---|
Dedicated cluster |

• Lower pod density and more overprovisioned resources

**Dedicated node pool**• Requires extra cluster configurations, like network policies, quota management, role-based access control (RBAC), etc.

**Dedicated namespace**• Requires extra cluster configurations, like network policies, quota management, role-based access control (RBAC), etc.

### Dedicated cluster

With * dedicated cluster multitenancy*, clusters are dedicated to a single workload or team.


The following table outlines pros and cons of using a dedicated cluster:

| Pros | Cons |
|---|---|
| • Easier isolation method • Straightforward cost allocation and chargeback • Great for cases where tenants don't trust each other (often from security and resource sharing perspectives) |
• High management and financial overhead • Generally low pod density and overprovisioned resources |

### Dedicated node pool

With * dedicated node pool multitenancy*, clusters are shared by many tenants.


The following table outlines pros and cons of using a dedicated node pool:

| Pros | Cons |
|---|---|
| • Medium pod density • Some shared infrastructure • Apply Azure tags to node pools dedicated to a single tenant (tags propagate to nodes and persist through upgrades) |
• Requires trust between the tenants • Requires extra cluster configurations, like network policies, quota management, role-based access control (RBAC), etc. |

### Dedicated namespace

With * dedicated namespace multitenancy*, clusters are shared by many tenants, with namespaces serving as the isolation boundary.


The following table outlines pros and cons of using a dedicated namespace:

| Pros | Cons |
|---|---|
| • Higher pod density • Best binpacking • Sharing infrastructure to maximize resource utilization |
• Unsafe for hostile environments by default • Requires extra security measures in place if all tenants can't be trusted |

## Azure discounts

To take savings one step further, take advantage of Azure discounts such as Azure Savings Plans, Reserved Instances, and Azure Hybrid Benefits.

| Azure discount type | Details |
|---|---|
Azure Savings Plans |

• Save up to 65% compared to pay-as-you-go

• Flexible, with no SKU family or region restrictions

• Best for workloads with consistent costs with resources in various SKUs and regions

**Reserved Instances**• Save up to 72% compared to pay-as-you-go

• Restricted to specific SKU families and regions

• Best for stable workloads running continuously (with no unexpected SKU or region changes)

**Azure Hybrid Benefits**• Use any qualifying on-premises licenses that have an active Software Assurance (SA) or qualifying subscription

## Next steps

To learn more about cost in AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-upgrade-github-actions -->

# Apply automatic security upgrades to Azure Kubernetes Service (AKS) nodes using GitHub Actions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Security updates are a key part of maintaining your AKS cluster's security and compliance with the latest fixes for the underlying OS. These updates include OS security fixes or kernel updates. Some updates require a node reboot to complete the process.

This article shows you how you can automate the update process of AKS nodes using GitHub Actions and Azure CLI to create an update task based on `cron`

that runs automatically.

Note

You can also perform node image upgrades automatically and schedule these upgrades using planned maintenance. For more information, see [Automatically upgrade node images](auto-upgrade-node-image).

## Before you begin

- This article assumes you have an existing AKS cluster. If you need an AKS cluster, create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[the Azure portal](learn/quick-kubernetes-deploy-portal). - This article also assumes you have a
[GitHub account](https://github.com)and a[profile repository](https://docs.github.com/en/free-pro-team@latest/github/setting-up-and-managing-your-github-profile/about-your-profile)to host your actions. If you don't have a repository, create one with the same name as your GitHub username. - You need the Azure CLI version 2.0.59 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Update nodes with `az aks upgrade`


The `az aks upgrade`

command gives you a zero downtime way to apply updates. The command performs the following actions:

- Applies the latest updates to all your cluster's nodes.
- Cordons (makes the node unavailable for the scheduling of new workloads) and drains (moves the existent workloads to other node) traffic to the nodes.
- Restarts the nodes.
- Enables the updated nodes to receive traffic again.

AKS doesn't automatically restart your nodes if you update them using a different method.

Note

Running `az aks upgrade`

with the `--node-image-only`

flag only upgrades the node images. Running the command without the flag upgrades both the node images and the Kubernetes control plane version. For more information, see the [docs for managed upgrades on nodes](node-image-upgrade) and the [docs for cluster upgrades](upgrade-cluster).

All Kubernetes nodes run in a standard Windows or Linux-based Azure virtual machine (VM). The Linux-based VMs use an Ubuntu image with the OS configured to automatically check for updates every night.

When you use the `az aks upgrade`

command, Azure CLI creates a surge of new nodes with the latest security and kernel updates. These new nodes are initially cordoned to prevent any apps from being scheduled to them until the update completes. After the update completes, Azure cordons and drains the older nodes and uncordons the new ones, transferring all the scheduled applications to the new nodes.

This process is better than updating Linux-based kernels manually because Linux requires a reboot when a new kernel update is installed. If you update the OS manually, you also need to reboot the VM, manually cordoning and draining all the apps.

## Create a timed GitHub Action

`cron`

is a utility that allows you to run a set of commands, or *jobs*, on an automated schedule. To create a job to update your AKS nodes on an automated schedule, you need a repository to host your actions. GitHub Actions are usually configured in the same repository as your application, but you can use any repository.

Navigate to your repository on GitHub.

Select

**Actions**.Select

**New workflow**>**Set up a workflow yourself**.Create a GitHub Action named

*Upgrade cluster node images*with a schedule trigger to run every 15 days at 3am. Copy the following code into the YAML:`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *'`

Create a job named

*upgrade-node*that runs on an Ubuntu agent and connects to your Azure CLI account to execute the node upgrade command. Copy the following code into the YAML under the`on`

key:`jobs: upgrade-node: runs-on: ubuntu-latest`


## Set up the Azure CLI in the workflow

In the

**Search Marketplace for Actions**bar, search for**Azure Login**.Select

**Azure Login**.Under

**Installation**, select a version, such as*v1.4.6*, and copy the installation code snippet.Add the

`steps`

key and the following information from the installation code snippet to the YAML:`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *' jobs: upgrade-node: runs-on: ubuntu-latest steps: - name: Azure Login uses: Azure/login@v1.4.6 with: creds: ${{ secrets.AZURE_CREDENTIALS }}`


## Create credentials for the Azure CLI

In a new browser window, create a new service principal using the

command. Make sure you replace`az ad sp create-for-rbac`

`*{subscriptionID}*`

with your own subscription ID.Note

This example creates the

`Contributor`

role at the*Subscription*scope. You can provide the role and scope that meets your needs. For more information, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles)and[Azure RBAC scope levels](/en-us/azure/role-based-access-control/scope-overview#scope-format).`az ad sp create-for-rbac --role Contributor --scopes /subscriptions/{subscriptionID} -o json`

Your output should be similar to the following example output:

`{ "appId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "displayName": "xxxxx-xxx-xxxx-xx-xx-xx-xx-xx", "password": "xxxxxxxxxxxxxxxxxxxxxxxxxxxx", "tenant": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" }`

Copy the output and navigate to your GitHub repository.

Select

**Settings**>**Secrets and variables**>**Actions**>**New repository secret**.For

**Name**, enter`AZURE_CREDENTIALS`

.For

**Secret**, copy in the contents of the output you received when you created the service principal.Select

**Add Secret**.

## Create the steps to execute the Azure CLI commands

Navigate to your window with the workflow YAML.

In the

**Search Marketplace for Actions**bar, search for**Azure CLI Action**.Select

**Azure CLI Action**.Under

**Installation**, select a version, such as*v1.0.8*, and copy the installation code snippet.Paste the contents of the action into the YAML below the

`*Azure Login*`

step, similar to the following example:`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *' jobs: upgrade-node: runs-on: ubuntu-latest steps: - name: Azure Login uses: Azure/login@v1.4.6 with: creds: ${{ secrets.AZURE_CREDENTIALS }} - name: Upgrade node images uses: Azure/cli@v1.0.8 with: inlineScript: az aks upgrade --resource-group <resourceGroupName> --name <aksClusterName> --node-image-only --yes`

Tip

You can decouple the

`--resource-group`

and`--name`

parameters from the command by creating new repository secrets like you did for`AZURE_CREDENTIALS`

.If you create secrets for these parameters, you need to replace the

`<resourceGroupName>`

and`<aksClusterName>`

placeholders with their secret counterparts. For example,`${{secrets.RESOURCE_GROUP_NAME}}`

and`${{secrets.AKS_CLUSTER_NAME}}`

Rename the YAML to

`upgrade-node-images.yml`

.Select

**Commit changes...**, add a commit message, and then select**Commit changes**.

## Run the GitHub Action manually

You can run the workflow manually in addition to the scheduled run by adding a new `on`

trigger called `workflow_dispatch`

.

Note

If you want to upgrade a single node pool instead of all node pools on the cluster, add the `--name`

parameter to the `az aks nodepool upgrade`

command to specify the node pool name. For example:

```
az aks nodepool upgrade --resource-group <resourceGroupName> --cluster-name <aksClusterName> --name <nodePoolName> --node-image-only
```


Add the

`workflow_dispatch`

trigger under the`on`

key:`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *' workflow_dispatch:`

The YAML should look similar to the following example:

`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *' workflow_dispatch: jobs: upgrade-node: runs-on: ubuntu-latest steps: - name: Azure Login uses: Azure/login@v1.4.6 with: creds: ${{ secrets.AZURE_CREDENTIALS }} - name: Upgrade node images uses: Azure/cli@v1.0.8 with: inlineScript: az aks upgrade -g {resourceGroupName} -n {aksClusterName} --node-image-only --yes # Code for upgrading one or more node pools`


## Next steps

For more information about AKS upgrades, see the following articles and resources:

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/managed-namespaces -->

# Use managed namespaces in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic ✔️ AKS Standard

Managed namespaces in Azure Kubernetes Service (AKS) provide a way to logically isolate workloads and teams within a cluster. This feature enables administrators to enforce resource quotas, apply network policies, and manage access control at the namespace level. For a detailed overview of managed namespaces, see the [managed namespaces overview](concepts-managed-namespaces).

## Before you begin

### Prerequisites

- An Azure account with an active subscription. If you don't have one, you can
[create an account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F). - An
[AKS cluster](automatic/quick-automatic-managed-network)set up in your Azure environment with[Azure role-based access control for Kubernetes authorization](manage-azure-rbac)is required if you intend to utilize Azure RBAC roles. - To use the network policy feature, the AKS cluster needs to be
[configured with a network policy engine](use-network-policies#network-policy-options-in-aks). Cilium is our recommended engine.

| Prerequisite | Notes |
|---|---|
Azure CLI |
`2.80.0` or later installed. To find the CLI version, run `az --version` . If you need to install or upgrade, see
|
AKS API Version |
`2025-09-01` or later. |
Required permission(s) |
`Microsoft.ContainerService/managedClusters/managedNamespaces/*` or `Azure Kubernetes Service Namespace Contributor` built-in role. `Microsoft.Resources/deployments/*` on the resource group containing the cluster. For more information, see
|

### Limitations

- Trying to on-board system namespaces such as
`kube-system`

,`app-routing-system`

,`istio-system`

,`gatekeeper-system`

, etc. to be managed namespaces isn't allowed. - When a namespace is a managed namespace, changes to the namespace via the Kubernetes API are blocked.

- Listing existing namespaces to convert in the portal doesn't work with private clusters. You can add new namespaces.

## Create a managed namespace on a cluster and assign users

Note

When you create a managed namespace, a component is installed on the cluster to reconcile the namespace with the state in Azure Resource Manager. This component blocks changes to the managed fields and resources from the Kubernetes API, ensuring consistency with the desired configuration.

The following Bicep example demonstrates how to create a managed namespace as a subresource of a managed cluster. Make sure to select the appropriate value for `defaultNetworkPolicy`

, `adoptionPolicy`

, and `deletePolicy`

. For more information about what those parameters mean, see the [managed namespaces overview](concepts-managed-namespaces).

```
resource existingCluster 'Microsoft.ContainerService/managedClusters@2024-03-01' existing = {
name: 'contoso-cluster'
}
resource managedNamespace 'Microsoft.ContainerService/managedClusters/managedNamespaces@2025-09-01' = {
parent: existingCluster
name: 'retail-team'
location: location
properties: {
defaultResourceQuota: {
cpuRequest: '1000m'
cpuLimit: '2000m'
memoryRequest: '512Mi'
memoryLimit: '1Gi'
}
defaultNetworkPolicy: {
ingress: 'AllowSameNamespace'
egress: 'AllowAll'
}
adoptionPolicy: 'IfIdentical'
deletePolicy: 'Keep'
labels: {
environment: 'dev'
}
annotations: {
owner: 'retail'
}
}
}
```


Save the Bicep file **managedNamespace.bicep** to your local computer.

Deploy the Bicep file using the Azure CLI.

```
az deployment group create --resource-group <resource-group> --template-file managedNamespace.bicep
```


### Define variables

Define the following variables to be used in the subsequent steps.

```
RG_NAME=cluster-rg
CLUSTER_NAME=contoso-cluster
NAMESPACE_NAME=retail-team
LABELS="environment=dev"
ANNOTATIONS="owner=retail"
```


### Create the managed namespace

To customize its configuration, managed namespaces have various parameter options to choose from during creation. Make sure to select the appropriate value for `ingress-network-policy`

, `egress-network-policy`

, `adoption-policy`

, and `delete-policy`

. For more information about what those parameters mean, see the [managed namespaces overview](concepts-managed-namespaces).

```
az aks namespace add \
--name ${NAMESPACE_NAME} \
--cluster-name ${CLUSTER_NAME} \
--resource-group ${RG_NAME} \
--cpu-request 1000m \
--cpu-limit 2000m \
--memory-request 512Mi \
--memory-limit 1Gi \
--ingress-policy [AllowSameNamespace|AllowAll|DenyAll] \
--egress-policy [AllowSameNamespace|AllowAll|DenyAll] \
--adoption-policy [Never|IfIdentical|Always] \
--delete-policy [Keep|Delete] \
--labels ${LABELS} \
--annotations ${ANNOTATIONS}
```


### Assign role

After the namespace is created, you can assign [one of the built-in roles](concepts-managed-namespaces#managed-namespaces-built-in-roles) for the control plane and data plane.

```
ASSIGNEE="user@contoso.com"
NAMESPACE_ID=$(az aks namespace show --name ${NAMESPACE_NAME} --cluster-name ${CLUSTER_NAME} --resource-group ${RG_NAME} --query id -o tsv)
```


Assign a control plane role to be able to view the managed namespace in the portal, Azure CLI output, and Azure Resource Manager. This role also allows the user to retrieve the credentials to connect to this namespace.

```
az role assignment create \
--assignee ${ASSIGNEE} \
--role "Azure Kubernetes Service Namespace User" \
--scope ${NAMESPACE_ID}
```


Assign data plane role to be able to get access to create resources within the namespace using the Kubernetes API.

```
az role assignment create \
--assignee ${ASSIGNEE} \
--role "Azure Kubernetes Service RBAC Writer" \
--scope ${NAMESPACE_ID}
```


- Sign in to the
[Azure portal](https://portal.azure.com). - On the Azure portal home page, select
**Create a resource**. - In the
**Categories**section, select**Managed Kubernetes Namespaces**. - On the
**Basics**tab, under**Project details**configure the following settings:- Select the target
**cluster**to create the namespace on. - If you're creating a new namespace, leave the default
**create new**, otherwise choose**change existing to managed**to convert an existing namespace.

- Select the target
- Configure the
**networking policy**to be applied on the namespace. - Configure the
**resource requests and limits**for the namespace. - Select the
**members (users or groups)**and their**role**.- Assign the
**Azure Kubernetes Service Namespace User**role to give them access to view the managed namespace in the portal, Azure CLI output, and Azure Resource Manager. This role also allows the user to retrieve the credentials to connect to this namespace. - Assign the
**Azure Kubernetes Service RBAC Writer**role to give them access to create resources within the namespace using the Kubernetes API.

- Assign the
- Select
**Review + create**to run validation on the configuration. After validation completes, select**Create**.

## List managed namespaces

You can list managed namespaces at different scopes using the Azure CLI.

### Subscription level

Run the following command to list all managed namespaces in a subscription.

```
az aks namespace list --subscription <subscription-id>
```


### Resource group level

Run the following command to list all managed namespaces in a specific resource group.

```
az aks namespace list --resource-group <rg-name>
```


### Cluster level

Run the following command to list all managed namespaces in a specific cluster.

```
az aks namespace list --resource-group <rg-name> --cluster-name <cluster-name>
```


## List managed namespaces

You can list managed namespaces at different scopes using the Azure CLI.

### Subscription level

Run the following command to list all managed namespaces in a subscription.

```
az aks namespace list --subscription <subscription-id>
```


### Resource group level

Run the following command to list all managed namespaces in a specific resource group.

```
az aks namespace list --resource-group <rg-name>
```


### Cluster level

Run the following command to list all managed namespaces in a specific cluster.

```
az aks namespace list --resource-group <rg-name> --cluster-name <cluster-name>
```


## Connect to the cluster

You can retrieve the credentials to connect to a namespace via the following command.

```
az aks namespace get-credentials --name <namespace-name> --resource-group <rg-name> --cluster-name <cluster-name>
```


## Connect to the cluster

You can retrieve the credentials to connect to a namespace via the following command.

```
az aks namespace get-credentials --name <namespace-name> --resource-group <rg-name> --cluster-name <cluster-name>
```


## Next steps

This article focused on using the managed namespaces feature to logically isolate teams and applications. You can further explore other guardrails and best practices to apply via [deployment safeguards](deployment-safeguards).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-labels -->

# Use labels in an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If you have multiple node pools, you may want to add a label during node pool creation. [Kubernetes labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) handle the scheduling rules for nodes. You can add labels to a node pool anytime and apply them to all nodes in the node pool.

In this how-to guide, you learn how to use labels in an Azure Kubernetes Service (AKS) cluster.

## Prerequisites

You need the Azure CLI version 2.2.0 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create an AKS cluster with a label

You can create an AKS cluster with node labels to set key/value metadata for workload scheduling.

```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="myResourceGroup$RANDOM_SUFFIX"
export AKS_CLUSTER_NAME="myAKSCluster$RANDOM_SUFFIX"
az group create --name $RESOURCE_GROUP --location $REGION
```


Results:

```
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx",
"location": "eastus2",
"managedBy": null,
"name": "myResourceGroupxxx",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null,
"type": "Microsoft.Resources/resourceGroups"
}
```


Create the AKS cluster specifying node labels (e.g., dept=IT, costcenter=9000):

```
az aks create \
--resource-group $RESOURCE_GROUP \
--name $AKS_CLUSTER_NAME \
--node-count 2 \
--nodepool-labels dept=IT costcenter=9000 \
--generate-ssh-keys --location $REGION
```


Results:

```
{
"aadProfile": null,
"addonProfiles": {},
"agentPoolProfiles": [
{
"count": 2,
"enableAutoScaling": null,
"mode": "System",
"name": "nodepool1",
"nodeLabels": {
"costcenter": "9000",
"dept": "IT"
}
}
],
"dnsPrefix": "myaksclusterxxx-dns",
"fqdn": "myaksclusterxxx-xxxxxxxx.hcp.eastus2.azmk8s.io",
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.ContainerService/managedClusters/myAKSClusterxxx",
"location": "eastus2",
"name": "myAKSClusterxxx",
"resourceGroup": "myResourceGroupxxx"
}
```


Verify the labels were set:

```
az aks get-credentials --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER_NAME --overwrite-existing
kubectl get nodes --show-labels | grep -e "costcenter=9000" -e "dept=IT"
```


## Create a node pool with a label

You can create an additional node pool with labels for specific scheduling needs.

```
export NODEPOOL_NAME="labelnp"
az aks nodepool add \
--resource-group $RESOURCE_GROUP \
--cluster-name $AKS_CLUSTER_NAME \
--name $NODEPOOL_NAME \
--node-count 1 \
--labels dept=HR costcenter=5000
```


The following is example output from the [ az aks nodepool list](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-list) command showing the

*labelnp*node pool is

*Creating*nodes with the specified

*nodeLabels*:

```
az aks nodepool list --resource-group $RESOURCE_GROUP --cluster-name $AKS_CLUSTER_NAME
```


Results:

```
[
{
"count": 2,
"name": "nodepool1",
"nodeLabels": {
"costcenter": "9000",
"dept": "IT"
}
},
{
"count": 1,
"name": "labelnp",
"nodeLabels": {
"costcenter": "5000",
"dept": "HR"
},
"provisioningState": "Creating"
}
]
```


Verify the labels were set:

```
kubectl get nodes --show-labels | grep -e "costcenter=5000" -e "dept=HR"
```


## Updating labels on existing node pools

You can update the labels on an existing node pool. Note that updating labels will overwrite the old labels.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $AKS_CLUSTER_NAME \
--name $NODEPOOL_NAME \
--labels dept=ACCT costcenter=6000
```


Verify the new labels are set:

```
kubectl get nodes --show-labels | grep -e "costcenter=6000" -e "dept=ACCT"
```


## Unavailable labels

### Reserved system labels

Since the [2021-08-19 AKS release](https://github.com/Azure/AKS/releases/tag/2021-08-19), AKS stopped the ability to make changes to AKS reserved labels. Attempting to change these labels results in an error message.

The following labels are AKS reserved labels. *Virtual node usage* specifies if these labels could be a supported system feature on virtual nodes. Some properties that these system features change aren't available on the virtual nodes because they require modifying the host.

| Label | Value | Example/Options | Virtual node usage |
|---|---|---|---|
`kubernetes.azure.com/agentpool` |
<agent pool name> | `nodepool1` |
Same |
`kubernetes.io/arch` |
<runtime.GOARCH> | `amd64 ` |
N/A |
`kubernetes.io/os` |
<OS Type> | `Linux/Windows` |
Same |
`node.kubernetes.io/instance-type` |
<VM size> | `Standard_NC6s_v3` |
Virtual |
`topology.kubernetes.io/region` |
<Azure region> | `westus2` |
Same |
`topology.kubernetes.io/zone` |
<Azure zone> | `0` |
Same |
`kubernetes.azure.com/cluster` |
<MC_RgName> | `MC_aks_myAKSCluster_westus2` |
Same |
`kubernetes.azure.com/managedby` |
`aks` |
`aks` |
N/A |
`kubernetes.azure.com/mode` |
<mode> | `User` or `system` |
User |
`kubernetes.azure.com/role` |
agent | `Agent` |
Same |
`kubernetes.azure.com/scalesetpriority` |
<VMSS priority> | `spot` or `regular` |
N/A |
`kubernetes.io/hostname` |
<hostname> | `aks-nodepool-00000000-vmss000000` |
Same |
`kubernetes.azure.com/storageprofile` |
<OS disk storage profile> | `Managed` |
N/A |
`kubernetes.azure.com/storagetier` |
<OS disk storage tier> | `Premium_LRS` |
N/A |
`kubernetes.azure.com/node-image-version` |
<VHD version> | `AKSUbuntu-1804-2020.03.05` |
Virtual node version |
`kubernetes.azure.com/network-name` |
<nodepool vnet name> | `vnetName` |
Virtual node virtual network |
`kubernetes.azure.com/network-subnet` |
<nodepool subnet name> | `subnetName` |
Virtual node subnet name |
`kubernetes.azure.com/ppg` |
<nodepool ppg name> | `ppgName` |
N/A |
`kubernetes.azure.com/encrypted-set` |
<nodepool encrypted-set name> | `encrypted-set-name` |
N/A |
`kubernetes.azure.com/accelerator` |
<accelerator> | `nvidia` |
N/A |
`kubernetes.azure.com/fips_enabled` |
<is FIPS enabled?> | `true` |
N/A |
`kubernetes.azure.com/os-sku` |
<os/sku> |
|

`kubernetes.azure.com/os-sku-effective`

`Ubuntu2204`

or similar (never Ubuntu, always has the version specified)`kubernetes.azure.com/os-sku-requested`

`Ubuntu`

, `Ubuntu2204`

, or similar (exactly matches requested sku from API)`kubernetes.azure.com/sku-cpu`

`4`

`kubernetes.azure.com/sku-memory`

`16`

`kubernetes.azure.com/nodepool-type`

`VirtualMachineScaleSets`

*Same*is included in places where the expected values for the labels don't differ between a standard node pool and a virtual node pool. As virtual node pods don't expose any underlying virtual machine (VM), the VM SKU values are replaced with the SKU*Virtual*.*Virtual node version*refers to the current version of the[virtual Kubelet-ACI connector release](https://github.com/virtual-kubelet/azure-aci/releases).*Virtual node subnet name*is the name of the subnet where virtual node pods are deployed into Azure Container Instance (ACI).*Virtual node virtual network*is the name of the virtual network, which contains the subnet where virtual node pods are deployed on ACI.*Node Auto Provisioning (Karpenter)*nodes have additional labels corresponding to the supported[selectors](/en-us/azure/aks/node-auto-provisioning-node-pools#well-known-labels-and-sku-selectors).`kubernetes.azure.com/network-name`

and`kubernetes.azure.com/network-subnet`

will be truncated if the underlying resource names are greater than 64 characters long.

### Reserved prefixes

The following prefixes are AKS reserved prefixes and can't be used for any node:

- kubernetes.azure.com/
- kubernetes.io/

For more information on reserved prefixes, see [Kubernetes well-known labels, annotations, and taints](https://kubernetes.io/docs/reference/labels-annotations-taints/).

### Deprecated labels

The following labels are planned for deprecation with the release of [Kubernetes v1.24](supported-kubernetes-versions#aks-kubernetes-release-calendar). You should change any label references to the recommended substitute.

| Label | Recommended substitute | Maintainer |
|---|---|---|
| failure-domain.beta.kubernetes.io/region | topology.kubernetes.io/region |
|

[Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)[Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)[Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)[Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)*Newly deprecated. For more information, see the [Release Notes](https://github.com/Azure/AKS/releases).

## Next steps

Learn more about Kubernetes labels in the [Kubernetes labels documentation](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).
