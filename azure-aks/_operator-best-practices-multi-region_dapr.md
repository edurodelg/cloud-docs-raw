---
merged_at: 2026-01-25T12:25:33.951179
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: operator-best-practices-multi-region.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-multi-region -->

# Multi-region deployment models for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) provides a managed Kubernetes environment for deploying, managing, and scaling containerized applications. To provide resiliency to regional outages for your applications running on AKS, you can implement various multi-region deployment models. This article provides an overview of these models, their pros and cons, and best practices for maintaining application uptime.

AKS provides a range of capabilities that support both high availability (HA) and disaster recovery (DR) for your cluster and the applications running on AKS. For more information on how AKS supports reliability requirements, see [Reliability in AKS](/en-us/azure/reliability/reliability-aks#multi-region-support).

## Considerations

Below are some important considerations when implementing multi-region deployment models in AKS:

### Regional and global resources

**Regional resources** are provisioned as part of a *deployment stamp* to a single Azure region. These resources share nothing with resources in other regions, and they can be independently removed or replicated to other regions. For more information, see [Regional resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#regional-resources).

**Global resources** share the lifetime of the system, and they can be globally available within the context of a multi-region deployment. For more information, see [Global resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#global-resources).

### Global load balancing

Global load balancing services distribute traffic across regional backends, clouds, or hybrid on-premises services. These services route end-user traffic to the closest available backend. They also react to changes in service reliability or performance to maximize availability and performance. The following Azure services provide global load balancing:

[Azure Front Door](/en-us/azure/frontdoor/front-door-overview)[Azure Traffic Manager](/en-us/azure/traffic-manager/traffic-manager-overview)[Cross-region Azure Load Balancer](/en-us/azure/load-balancer/cross-region-overview)[Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/overview)

### Scope definition

Application uptime becomes important as you manage AKS clusters. By default, AKS provides high availability by using multiple nodes in a [Virtual Machine Scale Set](/en-us/azure/virtual-machine-scale-sets/overview), but these nodes don’t protect your system from a region failure. To maximize your uptime, plan ahead to maintain business continuity and prepare for disaster recovery using the following best practices:

- Plan for AKS clusters in multiple regions.
- Route traffic across multiple clusters using Azure Traffic Manager.
- Use geo-replication for your container image registries.
- Plan for application state across multiple clusters.
- Replicate storage across multiple regions.

## Multi-region deployment model implementations

The following table summarizes the three main multi-region deployment models in AKS, along with their pros and cons:

| Deployment model | Pros | Cons |
|---|---|---|
|

• High resiliency

• Better utilization of resources with higher performance

• Higher cost

• Requires a load balancer and form of traffic routing

[Active-passive](#active-passive-disaster-recovery-deployment-model)• Lower cost

• Doesn't require a load balancer or traffic manager

• Longer recovery time and downtime

• Underutilization of resources

[Passive-cold](#passive-cold-failover-deployment-model)• Doesn't require synchronization, replication, load balancer, or traffic manager

• Suitable for low-priority, non-critical workloads

• Longest recovery time and downtime

• Requires manual intervention to activate cluster and trigger backup

### Active-active high availability deployment model

In the active-active high availability (HA) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes between both regions. If one region becomes unavailable, traffic automatically routes to a region closest to the user who issued the request.
- There's a deployed hub-spoke pair for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Azure Front Door load balances and routes traffic to a regional Azure Application Gateway instance, which sits in front of each AKS cluster.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-active deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Create two instances of your web app.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- Two origin groups, each with a priority of
*one*. - A route.

Limit network traffic to the web apps only from the Azure Front Door instance. 5. Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both web apps with continuous deployment.


For more information, see the [ Recommended active-active high availability solution overview for AKS](active-active-solution).

### Active-passive disaster recovery deployment model

In the active-passive disaster recovery (DR) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic. Only one of the clusters actively serves traffic at any given time. The other cluster contains the same configuration and application data as the active cluster, but doesn't accept traffic unless directed by a traffic manager.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes to the primary AKS cluster, which you set in the Azure Front Door configuration.
- Priority needs to be set between
*1-5*with 1 being the highest and 5 being the lowest. - You can set multiple clusters to the same priority level and can specify the weight of each.

- Priority needs to be set between
- If the primary cluster becomes unavailable (disaster occurs), traffic automatically routes to the next region selected in the Azure Front Door.
- All traffic must go through the Azure Front Door traffic manager for this system to work.

- Azure Front Door routes traffic to the Azure App Gateway in the primary region (cluster must be marked with priority 1). If this region fails, the service redirects traffic to the next cluster in the priority list.
- Rules come from Azure Front Door.

- A hub-spoke pair is deployed for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-passive deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up. This helps reduce costs.

Create two instances of your web application, with one on each cluster.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- An origin group with a priority of
*one*for the primary region. - A second origin group with a priority of
*two*for the secondary region. - A route.

Limit network traffic to the web applications from only the Azure Front Door instance.

Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both the web applications with continuous deployment.


For more information, see the [ Recommended active-passive disaster recovery solution overview for AKS](active-passive-solution).

### Passive-cold failover deployment model

The passive-cold failover deployment model is configured in the same way as the [active-passive disaster recovery deployment model](#active-passive-disaster-recovery-deployment-model), except the clusters remain inactive until a user activates them in the event of a disaster. We consider this approach *out-of-scope* because it involves a similar configuration to active-passive, but with the added complexity of manual intervention to activate the cluster and trigger a backup.

With this example architecture:

- You create two AKS clusters, preferably in different regions or zones for better resiliency.
- When you need to fail over, you activate the deployment to take over the traffic flow.
- In the case the primary passive cluster goes down, you need to manually activate the cold cluster to take over the traffic flow.
- This condition needs to be set either by a manual input every time or a certain event as specified by you.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs for each cluster.

To create a passive-cold failover deployment model in AKS, you perform the following steps:

- Create two identical deployments in different zones/regions.
- Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up, which helps reduce costs.
- Create two instances of your web application, with one on each cluster.
- Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.
- Set a condition when the cold cluster should be triggered. You can use a load balancer if you need.

For more information, see the [ Recommended passive-cold failover solution overview for AKS](passive-cold-solution).

For more information, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: dapr.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/dapr -->

# Install the Dapr extension for Azure Kubernetes Service (AKS) and Arc-enabled Kubernetes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Dapr](dapr-overview) simplifies building resilient, stateless, and stateful applications that run on the cloud and edge and embrace the diversity of languages and developer frameworks. With Dapr's sidecar architecture, you can keep your code platform agnostic while tackling challenges around building microservices, like:

- Calling other services reliably and securely
- Building event-driven apps with pub/sub
- Building applications that are portable across multiple cloud services and hosts (for example, Kubernetes vs. a virtual machine)

Note

If you plan on installing Dapr in a Kubernetes production environment, see the [Dapr guidelines for production usage](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-production) documentation page.

## How it works

The Dapr extension uses the Azure CLI or a Bicep template to provision the Dapr control plane on your AKS or Arc-enabled Kubernetes cluster, creating the following Dapr services:

| Dapr service | Description |
|---|---|
`dapr-operator` |
Manages component updates and Kubernetes services endpoints for Dapr (state stores, pub/subs, etc.) |
`dapr-sidecar-injector` |
Injects Dapr into annotated deployment pods and adds the environment variables `DAPR_HTTP_PORT` and `DAPR_GRPC_PORT` to enable user-defined applications to easily communicate with Dapr without hard-coding Dapr port values. |
`dapr-placement` |
Used for actors only. Creates mapping tables that map actor instances to pods. |
`dapr-sentry` |
Manages mTLS between services and acts as a certificate authority. For more information, read the
|

Once Dapr is installed on your cluster, you can begin to develop using the Dapr building block APIs by [adding a few annotations](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-overview/#adding-dapr-to-a-kubernetes-deployment) to your deployments. For a more in-depth overview of the building block APIs and how to best use them, see the [Dapr building blocks overview](https://docs.dapr.io/developing-applications/building-blocks/).

Warning

If you install Dapr through the AKS or Arc-enabled Kubernetes extension, our recommendation is to continue using the extension for future management of Dapr instead of the Dapr CLI. Combining the two tools can cause conflicts and result in undesired behavior.

## Prerequisites

- An Azure subscription.
[Don't have one? Create a free account.](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) - The latest version of the
[Azure CLI](/en-us/cli/azure/install-azure-cli). - An existing
[AKS cluster](tutorial-kubernetes-deploy-cluster)or connected[Arc-enabled Kubernetes cluster](/en-us/azure/azure-arc/kubernetes/quickstart-connect-cluster). [An Azure Kubernetes Service Role-Based Access Control Admin role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-rbac-admin)

Select how you'd like to install, deploy, and configure the Dapr extension.

## Before you begin

### Add the Azure CLI extension for cluster extensions

Install the `k8s-extension`

Azure CLI extension by running the following commands:

```
az extension add --name k8s-extension
```


If the `k8s-extension`

extension is already installed, you can update it to the latest version using the following command:

```
az extension update --name k8s-extension
```


### Register the `KubernetesConfiguration`

resource provider

If you aren't already using cluster extensions, you may need to register the resource provider with your subscription. You can check the status of the provider registration using the [az provider list](/en-us/cli/azure/provider#az-provider-list) command, as shown in the following example:

```
az provider list --query "[?contains(namespace,'Microsoft.KubernetesConfiguration')]" -o table
```


The *Microsoft.KubernetesConfiguration* provider should report as *Registered*, as shown in the following example output:

```
Namespace RegistrationState RegistrationPolicy
--------------------------------- ------------------- --------------------
Microsoft.KubernetesConfiguration Registered RegistrationRequired
```


If the provider shows as *NotRegistered*, register the provider using the [az provider register](/en-us/cli/azure/provider#az-provider-register) as shown in the following example:

```
az provider register --namespace Microsoft.KubernetesConfiguration
```


### Register the `ExtensionTypes`

feature to your Azure subscription

The `ExtensionTypes`

feature needs to be registered to your Azure subscription. In the terminal, verify you're in the correct subscription:

```
az account set --subscription <YOUR-AZURE-SUBSCRIPTION-ID>
```


Register the `ExtensionTypes`

feature.

```
az feature registration create --namespace Microsoft.KubernetesConfiguration --name ExtensionTypes
```


Feature registration may take some time. After a few minutes, check the registration status using the following command:

```
az feature show --namespace Microsoft.KubernetesConfiguration --name ExtensionTypes
```


## Create the extension and install Dapr on your AKS or Arc-enabled Kubernetes cluster

When installing the Dapr extension, use the flag value that corresponds to your cluster type:

**AKS cluster**:`--cluster-type managedClusters`

.**Arc-enabled Kubernetes cluster**:`--cluster-type connectedClusters`

.

Note

If you're using Dapr OSS on your AKS cluster and would like to install the Dapr extension for AKS, read more about [how to successfully migrate to the Dapr extension](dapr-migration).

Create the Dapr extension, which installs Dapr on your AKS or Arc-enabled Kubernetes cluster.

For example, install the latest version of Dapr via the Dapr extension on your AKS cluster:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name <myAKSCluster> \
--resource-group <myResourceGroup> \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version false
```


### Keep your managed AKS cluster updated to the latest version

Based on your environment (dev, test, or production), you can keep up-to-date with the latest stable Dapr versions.

#### Choosing a release train

When configuring the extension, you can choose to install Dapr from a particular release train. Specify one of the two release train values:

| Value | Description |
|---|---|
`stable` |
Default. |
`dev` |
Early releases that can contain experimental features. Not suitable for production. |

For example:

```
--release-train stable
```


#### Configuring automatic updates to Dapr control plane

Warning

Auto-upgrade is not suitable for production environments. Only enable automatic updates to the Dapr control plane in dev or test environments. [Learn how to manually upgrade to the latest Dapr version for production environments.](#viewing-the-latest-stable-dapr-versions-available)

If you install Dapr without specifying a version, `--auto-upgrade-minor-version`

*is automatically enabled*, configuring the Dapr control plane to automatically update its minor version on new releases.

You can disable auto-update by specifying the `--auto-upgrade-minor-version`

parameter and setting the value to `false`

.

[Dapr versioning is in MAJOR.MINOR.PATCH format](https://docs.dapr.io/operations/support/support-versioning/#versioning), which means

`1.11.0`

to `1.12.0`

is a *minor*version upgrade.

```
--auto-upgrade-minor-version true
```


#### Viewing the latest stable Dapr versions available

To upgrade to the latest Dapr version in a production environment, you need to manually upgrade. Start by viewing a list of the stable Dapr versions available to your managed AKS cluster. Run the following command:

```
az k8s-extension extension-types list-versions-by-cluster --resource-group <myResourceGroup> --cluster-name <myCluster> --cluster-type managedClusters --extension-type microsoft.dapr --release-train stable
```


To see the latest stable Dapr version available to your managed AKS cluster, run the following command:

```
az k8s-extension extension-types list-versions-by-cluster --resource-group <myResourceGroup> --cluster-name <myCluster> --cluster-type managedClusters --extension-type microsoft.dapr --release-train stable --show-latest
```


To view a list of the stable Dapr versions available *by location*:

[Make sure you've registered the](dapr#register-the-extensiontypes-feature-to-your-azure-subscription)`ExtensionTypes`

feature to your Azure subscription.- Run the following command.

```
az k8s-extension extension-types list-versions-by-location --location westus --extension-type microsoft.dapr
```


[Next, manually update Dapr to the latest stable version.](#targeting-a-specific-dapr-version)

#### Targeting a specific Dapr version

Note

Dapr is supported with a rolling window, including only the current and previous versions. It is your operational responsibility to remain up to date with these supported versions. If you have an older version of Dapr, you may have to do intermediate upgrades to get to a supported version.

The same command-line argument is used for installing a specific version of Dapr or rolling back to a previous version. Set `--auto-upgrade-minor-version`

to `false`

and `--version`

to the version of Dapr you wish to install. If the `version`

parameter is omitted, the extension installs the latest version of Dapr. The following example command installs Dapr version `1.14.4-msft.10`

on your AKS cluster:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name <myAKSCluster> \
--resource-group <myResourceGroup> \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version false \
--version 1.14.4-msft.10
```


## Troubleshooting

### Troubleshooting extension management errors

If the extension fails to create or update, try suggestions and solutions in the [Dapr extension troubleshooting guide](dapr-troubleshooting).

### Troubleshooting Dapr functional errors

Troubleshoot Dapr open source errors unrelated to the extension via the [common Dapr issues and solutions guide](https://docs.dapr.io/operations/troubleshooting/common_issues/).

## Support

Note

Learn more about [how Microsoft handles issues raised for the Dapr extension](dapr-overview#issue-handling).

If you're experiencing Dapr runtime security risks and regressions while using the extension, open an issue with the [Dapr open source project](https://github.com/dapr/dapr/issues/new/choose).

You could also start a discussion in the Dapr project Discord:

## Delete the Dapr extension from your cluster

The process of uninstalling the Dapr extension from AKS does not delete the CRDs created during installation. These CRDs remain in the cluster as residual components, essential for the reconciler during the installation and uninstallation of the extension.

To clean the cluster of these CRDs, you can manually delete them **after** the Dapr extension has been completely uninstalled from AKS.

### Uninstalling the extension

Delete the extension from your AKS cluster using the following command:

```
az k8s-extension delete --resource-group <myResourceGroup> --cluster-name <myAKSCluster> --cluster-type managedClusters --name dapr
```


Or, if using a Bicep template, you can delete the template.

### Listing the CRDs in your cluster

To find the CRDs you'd like to remove, run the following command:

```
kubectl get crds | findstr dapr.io
```
