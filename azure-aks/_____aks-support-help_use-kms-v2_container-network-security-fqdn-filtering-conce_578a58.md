---
merged_at: 2026-01-25T15:16:21.147593
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____aks-support-help_use-kms-v2_container-network-security-fqdn-filtering-concep_c0216b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___aks-support-help_use-kms-v2_container-network-security-fqdn-filtering-concept_b82ea5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __aks-support-help_use-kms-v2_container-network-security-fqdn-filtering-concepts.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _aks-support-help_use-kms-v2.md -->
<!-- URL ORIGINAL: N/A -->

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


---

<!-- DOCUMENTO FUSIONADO: container-network-security-fqdn-filtering-concepts.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/container-network-security-fqdn-filtering-concepts -->

# Overview of FQDN filtering

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Containerized environments present unique security challenges. Traditional network security methods, often reliant on IP-based filtering, can become cumbersome and less effective as IP addresses frequently change. Additionally, understanding network traffic patterns and identifying potential threats can be complex.

FQDN filtering offers an efficient and user-friendly approach for managing network policies. By defining these policies based on domain names rather than IP addresses, organizations can significantly simplify the process of policy management. This approach eliminates the need for frequent updates that are typically required when IP addresses change, as a result reducing the administrative burden and minimizing the risk of configuration errors.

In a Kubernetes cluster, pod IP addresses can change often, which makes it challenging to secure the pods with security policies using IP addresses. FQDN filtering allows you to create pod level policies using domain names rather than IP addresses, which eliminates the need to update policies when an IP address changes.

Note

Azure CNI Powered by Cilium and Kubernetes version 1.29 or greater is required in order to use Container Network security features of Advanced Container Networking Services.

## Components of FQDN filtering

**Cilium Agent**: The Cilium Agent is a critical networking component that runs as a DaemonSet within Azure CNI clusters powered by Cilium. It handles networking, load balancing, and network policies for pods in the cluster. For pods with enforced FQDN policies, the Cilium Agent redirects packets to the ACNS Security Agent for DNS resolution and updates the network policy using the FQDN-IP mappings obtained from the ACNS Security Agent.

**ACNS Security Agent**: ACNS Security Agent runs as DaemonSet in Azure CNI powered by Cilium cluster with Advanced Container Networking services enabled. It handles DNS resolution for pods and on successful DNS resolution, it updates Cilium Agent with FQDN to IP mappings.

## How FQDN filtering works

When FQDN Filtering is enabled, DNS requests are first evaluated to determine if they should be allowed after which pods can only access specified domain names based on the network policy. The Cilium Agent marks DNS request packets originating from the pods, redirecting them to the ACNS Security Agent. This redirection occurs only for pods that are enforcing FQDN policies.

The ACNS Security Agent then decides whether to forward a DNS request to the DNS server based on the policy criteria. If permitted, the request is sent to the DNS server, and upon receiving the response, the ACNS Security Agent updates the Cilium Agent with FQDN mappings. This allows the Cilium Agent to update the network policy within the policy engine. The following image illustrates the high-level flow of FQDN Filtering.

## Key benefits

**Scalable security policy management**: Cluster and security admins don't have to update security policies each time an IP address changes making operations more efficient.

**Enhanced security compliance**: FQDN filtering supports a Zero Trust security model. Network traffic is restricted to trusted domains only mitigating risks from unauthorized access.

**Resilient Policy enforcement**: The ACNS Security Agent that is implemented with FQDN filtering ensures that DNS resolution continues seamlessly even if the Cilium agent goes down and policies continue to remain enforced. This implementation critically ensures that security and stability are maintained in dynamic and distributed environments.

## Considerations:

Container Network Security features require Azure CNI Powered by Cilium and Kubernetes version 1.29 and above.

Supported by

`CiliumClusterwideNetworkPolicy`

(CCNP): FQDN filtering can be applied cluster wide via`CiliumClusterwideNetworkPolicy`

.

## Limitations:

- Wildcard FQDN policies are partially supported. This means you can create policies that match specific patterns with a leading wildcard (for example,
*.example.com), but you cannot use a universal wildcard (*) to match all domains on the field`spec.egress.toPorts.rules.dns.matchPattern`


Supported Pattern:

`*.example.com`

- This allows traffic to all subdomains under example.com.`app*.example.com`

- This rule is more specific and only allows traffic to subdomains that start with "app" under example.comUnsupported Pattern

`*`

This attempts to match any domain name, which isn't supported.

- FQDN filtering is currently not supported with node-local DNS.
- Kubernetes service names aren't supported.
- Other L7 policies aren't supported.
- FQDN pods may exhibit performance degradation when handling more than 1,000 requests per second.
- If Advanced Container Networking Services(ACNS) security is disabled, FQDN and L7 policies (HTTP(s), Kafka and gRPC) will be blocked.
- Alpine-based container images may encounter DNS resolution issues when used with Cilium Network Policies. This is due to musl libc's limited search domain iteration. To work around this, explicitly define all search domains in the Network Policy's DNS rules using wildcard patterns, like the below example

```
rules:
dns:
- matchPattern: "*.example.com"
- matchPattern: "*.example.com.*.*"
- matchPattern: "*.example.com.*.*.*"
- matchPattern: "*.example.com.*.*.*.*"
- matchPattern: "*.example.com.*.*.*.*.*"
- toFQDNs:
- matchPattern: "*.example.com"
```


## Pricing

Important

Advanced Container Networking Services is a paid offering. For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Next steps

Learn how to apply

[fqdn filtering policies](how-to-apply-fqdn-filtering-policies)on AKS.Explore how the open source community builds

[Cilium Network Policies](https://docs.cilium.io/en/latest/security/policy/).For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).Explore Container Network Observability features in Advanced Container Networking Services in

[What is Container Network Observability?](advanced-container-networking-services-overview#container-network-observability).


---

<!-- DOCUMENTO FUSIONADO: dapr-settings.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/dapr-settings -->

# Configure the Dapr extension for your Azure Kubernetes Service (AKS) and Arc-enabled Kubernetes project

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

After [completing the prerequisites for installing the Dapr extension](dapr), you can configure the [Dapr](https://dapr.io/) extension to work best for you and your project using various configuration options, like:

- Rotating expiring certificates
- Provisioning Dapr with high availability (HA) enabled
- Limiting which of your nodes use the Dapr extension
- Setting automatic custom resource definition (CRD) updates
- Configuring the Dapr release namespace

The extension enables you to set Dapr configuration options by using the `--configuration-settings`

parameter in the Azure CLI or `configurationSettings`

property in a Bicep template.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Update configuration settings

Important

Some configuration options cannot be modified post-creation. Adjustments to these options require deletion and recreation of the extension, applicable to the following settings:

`global.ha.*`

`dapr_placement.*`


HA is enabled by default. Disabling it requires deletion and recreation of the extension.

To update your Dapr configuration settings, recreate the extension with the desired state. For example, let's say you previously created and installed the extension using the following configuration:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2"
```


To update the `dapr_operator.replicaCount`

from two to three, use the following command:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=3"
```


## Manage mTLS certificates

The Dapr extension supports in-transit encryption of communication between Dapr instances using the Dapr Sentry service control plane, which is a central Certificate Authority (CA). With the Sentry service, you can encrypt communication using self-signed or user-supplied x.509 certificates. [Learn more about setting up mTLS certificates in the open-source Dapr documentation.](https://docs.dapr.io/operations/security/mtls/#dapr-generated-self-signed-certificates)

You can [bring in your own certificates](https://docs.dapr.io/operations/security/mtls/#bringing-your-own-certificates), or let [Dapr automatically create and persist self-signed root and issuer certificates](https://docs.dapr.io/operations/security/mtls/#dapr-generated-self-signed-certificates).

Important

If you don't explicitly configure certificates, [Dapr defaults to generating self-signed certificates](#manage-dapr-generated-self-signed-certificates), which are generally valid for 1 year. **Currently, using self-signed certificates generated by Dapr is not recommended.** Best practice is to generate custom certificates and update them manually.

### Manage Dapr-generated self-signed certificates

If you haven't provided any custom certificates, Dapr automatically creates and persists self-signed certificates, valid for 1 year. The Dapr extension installs the `dapr-trust-bundle`

secret, which contains certificate information under the default `dapr-system`

namespace.

#### Check expiry of current Dapr-generated self-signed certificates

You can check when the Dapr root certificate of your Kubernetes cluster expires by using [the Dapr CLI](https://docs.dapr.io/getting-started/install-dapr-cli/).

```
dapr mtls expiry
```


**Expected output:**

```
Root certificate expires in 8759 hours. Expiry date: 2025-12-06 18:14:20 +0000 UTC
```


You can also find the expiration date for your current certificate in the Kubernetes `dapr-trust-bundle`

secret data.

```
kubectl get secret dapr-trust-bundle -n dapr-system -o jsonpath='{.data.issuer\.crt}' | base64 -d | openssl x509 -noout -dates
```


**Expected output:**

```
notBefore=Dec 6 17:59:20 2024 GMT
notAfter=Dec 6 18:14:20 2025 GMT
```


#### Generate a new Dapr-generated self-signed certificate

**Via the Dapr CLI (recommended)**

Refer to Dapr's[Root and issuer certificate upgrade using CLI](https://docs.dapr.io/operations/security/mtls/#root-and-issuer-certificate-upgrade-using-cli-recommended)guide.**Via**Refer to Dapr's`kubectl`

commands[Updating root or issuer certs using Kubectl](https://docs.dapr.io/operations/security/mtls/#updating-root-or-issuer-certs-using-kubectl)guide.

### Manage your own user-supplied x.509 certificates

You can also bring your own custom certificates.

**Generate custom certificates**

Create your own custom certificate; for example,[an Azure Key Vault certificate](/en-us/azure/key-vault/certificates/certificate-scenarios).**Update your custom certficate manually**

Follow[the instructions provided in the Dapr open source documentation to update your custom certificates manually](https://docs.dapr.io/operations/security/mtls/#custom-certificates-bring-your-own)using.`kubectl`


## Provision Dapr with high availability (HA) enabled

Provision Dapr with high availability (HA) enabled by setting the `global.ha.enabled`

parameter to `true`

.

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2"
```


Note

If configuration settings are sensitive and need to be protected (for example, cert-related information), pass the `--configuration-protected-settings`

parameter and the value will be protected from being read.

If no configuration-settings are passed, the Dapr configuration defaults to:

```
ha:
enabled: true
replicaCount: 3
disruption:
minimumAvailable: ""
maximumUnavailable: "25%"
prometheus:
enabled: true
port: 9090
mtls:
enabled: true
workloadCertTTL: 24h
allowedClockSkew: 15m
```


For a list of available options, see [Dapr configuration](https://github.com/dapr/dapr/blob/master/charts/dapr/README.md#configuration).

## Limit the extension to certain nodes

In some configurations, you may only want to run Dapr on certain nodes. You can limit the extension by passing a `nodeSelector`

in the extension configuration. If the desired `nodeSelector`

contains `.`

, you must escape them from the shell and the extension. For example, the following configuration installs Dapr only to nodes with `topology.kubernetes.io/zone: "us-east-1c"`

:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2" \
--configuration-settings "global.nodeSelector.kubernetes\.io/zone=us-east-1c"
```


For managing OS and architecture, use the [supported versions](https://github.com/dapr/dapr/blob/b8ae13bf3f0a84c25051fcdacbfd8ac8e32695df/docker/docker.mk#L50) of the `global.daprControlPlaneOs`

and `global.daprControlPlaneArch`

configuration:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2" \
--configuration-settings "global.daprControlPlaneOs=linux" \
--configuration-settings "global.daprControlPlaneArch=amd64"
```


## Install Dapr in multiple availability zones while in HA mode

By default, the placement service uses a storage class of type `standard_LRS`

. It's recommended to create a **zone redundant storage class** while installing Dapr in HA mode across multiple availability zones. For example, to create a `zrs`

type storage class, add the `storageaccounttype`

parameter:

```
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
name: custom-zone-redundant-storage
provisioner: disk.csi.azure.com
reclaimPolicy: Delete
allowVolumeExpansion: true
volumeBindingMode: WaitForFirstConsumer
parameters:
storageaccounttype: Premium_ZRS
```


When installing Dapr, use the storage class you used in the YAML file:

```
az k8s-extension create --cluster-type managedClusters
--cluster-name XXX
--resource-group XXX
--name XXX
--extension-type Microsoft.Dapr
--auto-upgrade-minor-version XXX
--version XXX
--configuration-settings "dapr_placement.volumeclaims.storageClassName=custom-zone-redundant-storage"
```


## Configure the Dapr release namespace

You can configure the release namespace.

The Dapr extension gets installed in the `dapr-system`

namespace by default. To override it, use `--release-namespace`

. To redefine the namespace, include the cluster `--scope`

.

```
az k8s-extension create \
--cluster-type managedClusters \
--cluster-name dapr-aks \
--resource-group dapr-rg \
--name my-dapr-ext \
--extension-type microsoft.dapr \
--release-train stable \
--auto-upgrade false \
--version 1.9.2 \
--scope cluster \
--release-namespace dapr-custom
```


## Show current configuration settings

Use the `az k8s-extension show`

command to show the current Dapr configuration settings:

```
az k8s-extension show --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr
```


## Set Dapr monitoring log levels

You can configure settings for the Dapr monitoring component with your AKS cluster extension. For exmaple, to update `dapr_monitoring`

log levels to "warn" (only notified when receiving a warning or error), set the following `configuration-settings`

:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_monitoring.logLevel=warn"
```


## Set the outbound proxy for Dapr extension for Azure Arc on-premises

If you want to use an outbound proxy with the Dapr extension for AKS, you can do so by:

- Setting the proxy environment variables using the
:`dapr.io/env`

annotations`HTTP_PROXY`

`HTTPS_PROXY`

`NO_PROXY`


[Installing the proxy certificate in the sidecar](https://docs.dapr.io/operations/configuration/install-certificates/).

## Updating your Dapr installation version

If you are on a specific Dapr version and you don't have `--auto-upgrade-minor-version`

available, you can use the following command to upgrade or downgrade Dapr:

```
az k8s-extension update --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--version 1.12.0 # Version to upgrade or downgrade to
```


The preceding command updates the Dapr control plane *only.* To update the Dapr sidecars, restart your application deployments:

```
kubectl rollout restart deploy/<DEPLOYMENT-NAME>
```


## Using Azure Linux-based images

From Dapr version 1.8.0, you can use Azure Linux images with the Dapr extension. To use them, set the `global.tag`

flag:

```
az k8s-extension update --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--set global.tag=1.10.0-mariner
```


[Learn more about using Mariner-based images with Dapr](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-deploy/#using-mariner-based-images).[Learn more about deploying Azure Linux on AKS](cluster-configuration#azure-linux-container-host-for-aks).

## Disable automatic CRD updates

From Dapr version 1.9.2, CRDs are automatically upgraded when the extension upgrades. To disable this setting, you can set `hooks.applyCrds`

to `false`

.

```
az k8s-extension update --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--configuration-settings "hooks.applyCrds=false"
```


Note

CRDs are only applied in case of upgrades and are skipped during downgrades.

## Meet network requirements

The Dapr extension requires the following outbound URLs on `https://:443`

to function on AKS and Arc for Kubernetes:

`https://mcr.microsoft.com/daprio`

URL for pulling Dapr artifacts.- The
[outbound URLs required for AKS or Arc for Kubernetes](/en-us/azure/azure-arc/kubernetes/network-requirements).


---

<!-- DOCUMENTO FUSIONADO: __azure-app-configuration_upgrade-aks-cluster_use-node-taints.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _azure-app-configuration_upgrade-aks-cluster.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: azure-app-configuration.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-app-configuration -->

# Install Azure App Configuration AKS extension

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Azure App Configuration](/en-us/azure/azure-app-configuration/overview) provides a service to centrally manage application settings and feature flags. [Azure App Configuration Kubernetes Provider](https://mcr.microsoft.com/en-us/product/azure-app-configuration/kubernetes-provider/about) is a Kubernetes operator that gets key-values, Key Vault references and feature flags from Azure App Configuration and builds them into Kubernetes ConfigMaps and Secrets. Azure App Configuration extension for Azure Kubernetes Service (AKS) allows you to install and manage Azure App Configuration Kubernetes Provider on your AKS cluster via Azure Resource Manager (ARM).

## Prerequisites

- An Azure subscription.
[Create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - The latest version of the
[Azure CLI](/en-us/cli/azure/install-azure-cli). - An Azure Kubernetes Service (AKS) cluster.
[Create an AKS cluster](/en-us/azure/aks/tutorial-kubernetes-deploy-cluster#create-a-kubernetes-cluster). - Permission with the
[Azure Kubernetes Service RBAC Admin](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-rbac-admin)role.

### Set up the Azure CLI extension for cluster extensions

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

If you haven't previously used cluster extensions, you may need to register the resource provider with your subscription. You can check the status of the provider registration using the [az provider list](/en-us/cli/azure/provider#az-provider-list) command, as shown in the following example:

```
az provider list --query "[?namespace=='Microsoft.KubernetesConfiguration']" -o table
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


## Install the extension on your AKS cluster

Create the Azure App Configuration extension, which installs Azure App Configuration Kubernetes Provider on your AKS.

For example, install the latest version of Azure App Configuration Kubernetes Provider via the Azure App Configuration extension on your AKS cluster:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration
```


Important

The Azure App Configuration AKS extension is installed into the `azappconfig-system`

namespace by default. If you have Azure Policy assignments that validate or mutate pod specifications (for example, the built-in policy "Kubernetes clusters should disable automounting API credentials" which enforces `automountServiceAccountToken: false`

), exclude the `azappconfig-system`

namespace from those policies by adding it to the policy's namespace exclusion list so the extension can function correctly. Not excluding it may cause the extension pods to fail validation or appear non-compliant.

### Configure automatic updates

If you create Azure App Configuration extension without specifying a version, `--auto-upgrade-minor-version`

*is automatically enabled*, configuring the Azure App Configuration extension to automatically update its minor version on new releases.

You can disable auto update by specifying the `--auto-upgrade-minor-version`

parameter and setting the value to `false`

.

### Targeting a specific version

The same command-line argument is used for installing a specific version of Azure App Configuration Kubernetes Provider or rolling back to a previous version. Set `--auto-upgrade-minor-version`

to `false`

and `--version`

to the version of Azure App Configuration Kubernetes Provider you wish to install. If the `version`

parameter is omitted, the extension installs the latest version.

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version false
--version 2.1.0
```


## Extension versions

The Azure App Configuration extension supports the following version of Azure App Configuration Kubernetes Provider:

`2.1.0`

`2.0.0`


## Troubleshoot extension installation errors

If the extension fails to create or update, try suggestions and solutions in the [Azure App Configuration extension troubleshooting guide](/en-us/troubleshoot/azure/azure-kubernetes/extensions/troubleshoot-app-configuration-extension-installation-errors).

## Troubleshoot Azure App Configuration Kubernetes Provider

Troubleshoot Azure App Configuration Kubernetes Provider errors via the [troubleshooting guide](/en-us/azure/azure-app-configuration/quickstart-azure-kubernetes-service#troubleshooting).

## Delete the extension

If you need to delete the extension and remove Azure App Configuration Kubernetes Provider from your AKS cluster, you can use the following command:

```
az k8s-extension delete --resource-group myResourceGroup --cluster-name myAKSCluster --cluster-type managedClusters --name appconfigurationkubernetesprovider
```


## Next Steps

- Learn more about
[extra settings and preferences you can set on the Azure App Configuration extension](azure-app-configuration-settings). - Once you successfully install Azure App Configuration extension in your AKS cluster, try
[quickstart](/en-us/azure/azure-app-configuration/quickstart-azure-kubernetes-service)to learn how to use it. - See all the supported features of
[Azure App Configuration Kubernetes Provider](/en-us/azure/azure-app-configuration/reference-kubernetes-provider).


---

<!-- DOCUMENTO FUSIONADO: upgrade-aks-cluster.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/upgrade-aks-cluster -->

# Upgrade the Azure Kubernetes Service (AKS) cluster control plane

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) clusters consist of two main components: the **control plane managed by Azure** and the **node pools where your workloads run**. This article focuses on upgrading the control plane independently, which allows you to adopt new Kubernetes versions for API server features while separately managing node pool upgrades.

## Before you begin

- If you're using the Azure CLI, this article requires Azure CLI version 2.34.1 or later. Use the
`az --version`

command to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you're using Azure PowerShell, this article requires Azure PowerShell version 5.9.0 or later. Use the
`Get-InstalledModule -Name Az`

cmdlet to find the version. If you need to install or upgrade, see[Install Azure PowerShell](/en-us/powershell/azure/install-az-ps). - Performing upgrade operations requires the
`Microsoft.ContainerService/managedClusters/agentPools/write`

RBAC role. For more on Azure RBAC roles, see the[Azure resource provider operations](/en-us/azure/role-based-access-control/built-in-roles#containers). - Starting with Kubernetes version 1.30 and 1.27 LTS versions, beta APIs are disabled by default when you upgrade to them.

Warning

Ensure you have sufficient compute quota before upgrading. If quota is low, the upgrade might fail. For more information, see [increase quotas](/en-us/azure/azure-portal/supportability/regional-quota-requests).

## Overview of AKS upgrade types

The following table outlines three types of AKS upgrades, highlighting their scope and use cases:

| Upgrade type | Scope | Use case |
|---|---|---|
|

[Full cluster](#upgrade-the-full-aks-cluster)[Node pool only](upgrade-aks-node-pools-rolling)Tip

Upgrading the control plane first allows you to validate Kubernetes API compatibility before affecting running workloads. For node pool upgrade strategies, see [Configure rolling upgrades](upgrade-aks-node-pools-rolling).

## Kubernetes version upgrade rules

When you upgrade a supported AKS cluster, you can't skip Kubernetes minor versions. You must perform all upgrades sequentially by minor version number. For example, upgrades between *1.28.x* -> *1.29.x* or *1.29.x* -> *1.30.x* are allowed. *1.28.x* -> *1.30.x* isn't allowed.

The control plane can be up to two minor versions ahead of node pools. For example, if your control plane is at *1.30.x*, your node pools can be at *1.28.x*, *1.29.x*, or *1.30.x*.

## Check for available AKS upgrades

Tip

To stay up to date with the latest AKS releases and updates, see the [AKS release tracker](release-tracker).

Check for available Kubernetes releases for your AKS cluster using the [ az aks get-upgrades](/en-us/cli/azure/aks#az-aks-get-upgrades) command.

```
az aks get-upgrades --resource-group <resource-group-name> --name <cluster-name> --output table
```


The following example output shows the current version as *1.28.9* and lists the available versions under `upgrades`

:

```
Name ResourceGroup MasterVersion Upgrades
------- --------------- --------------- --------------
default <resource-group-name> 1.28.9 1.29.2, 1.29.4
```


## Upgrade the AKS control plane only

Upgrade the control plane using the

command with the`az aks upgrade`

`--control-plane-only`

flag. The following example upgrades the control plane to Kubernetes version*1.29.4*:`az aks upgrade \ --resource-group <resource-group-name> \ --name <cluster-name> \ --kubernetes-version 1.29.4 \ --control-plane-only`

Confirm the control plane upgrade was successful using the

command.`az aks show`

`az aks show --resource-group <resource-group-name> --name <cluster-name> --output table`

The following example output shows the control plane now runs

*1.29.4*:`Name Location ResourceGroup KubernetesVersion ProvisioningState Fqdn ------------ ---------- --------------- ------------------- ------------------- ------------------------------------------------ <cluster-name> eastus <resource-group-name> 1.29.4 Succeeded <cluster-name>-dns-123abcd4.hcp.eastus.azmk8s.io`

Verify the node pool versions remain unchanged using the [

`az aks nodepool list`

][az-aks-nodepool-list] command.`az aks nodepool list --resource-group <resource-group-name> --cluster-name <cluster-name> --query "[].{Name:name,Version:orchestratorVersion}" --output table`

In the output, the node pools should still show the previous Kubernetes version.


## Upgrade the full AKS cluster

Note

During a full cluster upgrade, AKS upgrades the control plane first, then upgrades each node pool sequentially. For more control over node pool upgrades, see [Configure rolling upgrades](upgrade-aks-node-pools-rolling).

Upgrade the full cluster (control plane and all node pools) using the [ az aks upgrade](/en-us/cli/azure/aks#az-aks-upgrade) command. The following example upgrades the cluster to Kubernetes version

*1.29.4*:

```
az aks upgrade \
--resource-group <resource-group-name> \
--name <cluster-name> \
--kubernetes-version 1.29.4
```


## Frequently asked questions (FAQs)

### Why were my node pools upgraded when I only upgraded the control plane?

AKS might trigger a rolling node pool upgrade alongside a control plane upgrade to keep the cluster compliant and healthy. This upgrade typically occurs when a previous node upgrade failed or left nodes on mixed versions.

### Can I upgrade node pools before the control plane?

No. The control plane version must always be equal to or greater than any node pool version. You must upgrade the control plane first.

### How long does a control plane upgrade take?

Control plane upgrades typically complete within 5-15 minutes, depending on cluster configuration and Azure region load. Node pool upgrades take longer as they involve draining and reimaging nodes.

## Resolve control plane upgrade issues

### No upgrades available

If `az aks get-upgrades`

shows no available upgrades, your cluster might be:

- Already on the latest supported version.
- On an unsupported version that requires migration.

For unsupported versions, create a new cluster with a supported version and migrate your workloads.

### Upgrade failed due to deprecated APIs

Before upgrading, check for deprecated APIs using tools like [kube-no-trouble (kubent)](https://github.com/doitintl/kube-no-trouble):

```
kubent
```


Update your manifests to use supported API versions before upgrading.


---

<!-- DOCUMENTO FUSIONADO: use-node-taints.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-node-taints -->

# Use node taints in an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to use node taints in an Azure Kubernetes Service (AKS) cluster.

## Overview

The AKS scheduling mechanism is responsible for placing pods onto nodes and is based upon the upstream Kubernetes scheduler, [kube-scheduler](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/). You can constrain a pod to run on particular nodes by attaching the pods to a set of nodes using [node affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity) or by instructing the node to repel a set of pods using [node taints](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/), which interact with the AKS scheduler.

Node taints work by marking a node so that the scheduler avoids placing certain pods on the marked nodes. You can place [tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) on a pod to allow the scheduler to schedule that pod on a node with a matching taint. Taints and tolerations work together to help you control how the scheduler places pods onto nodes. For more information, see [example use cases of taints and tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/#example-use-cases:%7E:text=not%20be%20evicted.-,Example%20Use%20Cases,-Taints%20and%20tolerations).

Taints are key-value pairs with an [effect](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/). There are three values for the effect field when using node taints: `NoExecute`

, `NoSchedule`

, and `PreferNoSchedule`

.

`NoExecute`

: Pods already running on the node are immediately evicted if they don't have a matching toleration. If a pod has a matching toleration, it might be evicted if`tolerationSeconds`

are specified.`NoSchedule`

: Only pods with a matching toleration are placed on this node. Existing pods aren't evicted.`PreferNoSchedule`

: The scheduler avoids placing any pods that don't have a matching toleration.

### Node taint options

There are two types of node taints that can be applied to your AKS nodes: **node taints** and **node initialization taints**.

**Node taints**are meant to remain permanently on the node for scheduling pods with node affinity. Node taints can only be added, updated, or removed completely using the AKS API.**Node initialization taints**are placed on the node at boot time and are meant to be used temporarily, such as in scenarios where you might need extra time to set up your nodes. You can remove node initialization taint using the Kubernetes API and they aren't guaranteed during the node lifecycle. They will appear on new replicas of the node when it is scaled up or on all replicas when a node is upgraded. If you want to remove the initialization taints completely, you can remove them using the AKS API after untainting the nodes using the Kubernetes API. Once you remove the initialization taints from the cluster spec using the AKS API, newly created nodes don't come up with those initialization taints. If the initialization taint is still present on existing nodes, you can permanently remove it by performing a node image upgrade operation.

Note

Node taints and labels applied using the AKS node pool API aren't modifiable from the Kubernetes API and vice versa. Modifications to system taints aren't allowed.

This doesn't apply to node initialization taints.

## Use node taints

### Prerequisites

This article assumes you have an existing AKS cluster. If you need an AKS cluster, you can create one using [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

### Create a node pool with a node taint

Create a node pool with a taint using the

command and use the`az aks nodepool add`

`--node-taints`

parameter to specify`sku=gpu:NoSchedule`

for the taint.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-count 1 \ --node-taints "sku=gpu:NoSchedule" \ --no-wait`


### Update a node pool to add a node taint

Update a node pool to add a node taint using the

command and use the`az aks nodepool update`

`--node-taints`

parameter to specify`sku=gpu:NoSchedule`

for the taint.`az aks nodepool update \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-taints "sku=gpu:NoSchedule" \ --no-wait`


## Use node initialization taints (preview)

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Prerequisites and limitations

- You need the Azure CLI version
`3.0.0b3`

or later installed and configured. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You can only apply initialization taints via cluster create or upgrade when using the AKS API. If using ARM template that will result in a Managed Cluster level operation, you can specify node initialization taints during node pool creation and update. Agentpool level operations are blocked when
`NodeInitializationTaints`

are present in the request body. - You can't apply initialization taints to Windows node pools using the Azure CLI.

### Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME`


### Install the `aks-preview`

Azure CLI extension

Register or update the aks-preview extension using the

or`az extension add`

command.`az extension update`

`# Register the aks-preview extension az extension add --name aks-preview # Update the aks-preview extension az extension update --name aks-preview`


### Register the `NodeInitializationTaintsPreview`

feature flag

Register the

`NodeInitializationTaintsPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "NodeInitializationTaintsPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "NodeInitializationTaintsPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create a cluster with a node initialization taint

Create a cluster with a node initialization taint using the

command and the`az aks create`

`--node-initialization-taints`

parameter to specify`sku=gpu:NoSchedule`

for the taint.Important

The node initialization taints you specify apply to all of the node pools in the cluster. To apply the initialization taint to a specific node, you can use an ARM template instead of the CLI.

`az aks create \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --node-count 1 \ --node-init-taints "sku=gpu:NoSchedule" \ --generate-ssh-keys`


### Update a cluster to add a node initialization taint

Update a cluster to add a node initialization taint using the

command and the`az aks update`

`--node-initialization-taints`

parameter to specify`sku=gpu:NoSchedule`

for the taint.Important

When updating a cluster with a node initialization taint, the taints apply to all node pools in the cluster. If your nodes are using VMSS, you can view updates to node initialization taints on the node after the node's VMSS model is updated (for example, after a node image version upgrade operation). Initialization taints will not appear on your nodes until an operation that triggers a VMSS model update occurs.

`az aks update \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --node-init-taints "sku=gpu:NoSchedule"`


## Check the status of the node pool

After applying the node taint or initialization taint, check the status of the node pool using the

command.`az aks nodepool list`

`az aks nodepool list --resource-group $RESOURCE_GROUP_NAME --cluster-name $CLUSTER_NAME`

If you applied node taints, the following example output shows that the

`<node-pool-name>`

node pool is`Creating`

nodes with the specified`nodeTaints`

:`[ { ... "count": 1, ... "name": "<node-pool-name>", "orchestratorVersion": "1.15.7", ... "provisioningState": "Creating", ... "nodeTaints": [ "sku=gpu:NoSchedule" ], ... }, ... ]`

If you applied node initialization taints, the following example output shows that the

`<node-pool-name>`

node pool is`Creating`

nodes with the specified`nodeInitializationTaints`

:`[ { ... "count": 1, ... "name": "<node-pool-name>", "orchestratorVersion": "1.15.7", ... "provisioningState": "Creating", ... "nodeInitializationTaints": [ "sku=gpu:NoSchedule" ], ... }, ... ]`


## Check that the taint is set on the node

Check the node taints and node initialization taints in the node configuration using the

`kubectl describe node`

command.`kubectl describe node $NODE_NAME`

If you applied node taints, the following example output shows that the

`<node-pool-name>`

node pool has the specified`Taints`

:`[ ... Name: <node-pool-name> ... Taints: sku=gpu:NoSchedule ... ], ... ... ]`


Important

If your nodes are using VMSS, node initialization taints will not be visible on actual nodes in your cluster until an operation that triggers VMSS model update occurs (for example, Kubernetes version upgrade or node image version upgrade).

## Remove node taints

### Remove a specific node taint

Remove node taints using the

command. The following example command removes the`az aks nodepool update`

`"sku=gpu:NoSchedule"`

node taint from the node pool.`az aks nodepool update \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --node-taints ""`


### Remove all node taints

Remove all node taints from a node pool using the

command. The following example command removes all node taints from the node pool.`az aks nodepool update`

`az aks nodepool update \ --cluster-name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --name $NODE_POOL_NAME \ --node-taints ""`


## Remove node initialization taints

You have the following options to remove node initialization taints from the node:

**Remove node initialization taints temporarily**using the Kubernetes API. If you remove them this way, the taints reappear after node scaling or upgrade occurs. New nodes still have the node initialization taint after scaling. Node initialization taints appear on all nodes after upgrading.**Remove node initialization taints permanently**by untainting the node using the Kubernetes API, and then removing the taint using the AKS API. Once the initialization taints are removed from cluster spec using AKS API, newly created nodes after reimage operations no longer have initialization taints.

When you remove all initialization taint occurrences from node pool replicas, the existing initialization taint might reappear after an upgrade with any new initialization taints.

### Remove node initialization taints temporarily

Remove node initialization taints temporarily using the

`kubectl taint nodes`

command.This command removes the taint from only the specified node. If you want to remove the taint from every node in the node pool, you need to run the command for every node that you want the taint removed from.

`kubectl taint nodes $NODE_POOL_NAME sku=gpu:NoSchedule-`

Once removed, node initialization taints reappear after node scaling or upgrading occurs.


### Remove node initialization taints permanently

Follow steps in

[Remove node initialization taints temporarily](#remove-node-initialization-taints-temporarily)to remove the node initialization taint using the Kubernetes API.Remove the taint from the node using the AKS API using the

command. This command removes the node initialization taint from every node in the cluster.`az aks update`

`az aks update \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --node-init-taints ""`


## Check that the taint has been removed from the node

Check the node taints and node initialization taints in the node configuration using the

`kubectl describe node`

command.`kubectl describe node $NODE_NAME`

If you removed a node taint, the following example output shows that the

`<node-pool-name>`

node pool doesn't have the removed taint under`Taints`

:`[ ... Name: <node-pool-name> ... Taints: ... ], ... ... ]`


## Next steps

- Learn more about example use cases for
[taints and tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/#example-use-cases:%7E:text=not%20be%20evicted.-,Example%20Use%20Cases,-Taints%20and%20tolerations). - Learn more about
[best practices for advanced AKS scheduler features](operator-best-practices-advanced-scheduler). - Learn more about Kubernetes labels in the
[Kubernetes labels documentation](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).


---

<!-- DOCUMENTO FUSIONADO: __enable-fips-nodes__upgrade-aks-control-plane__deploy-application-az-cli_use-az_bde122.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _enable-fips-nodes__upgrade-aks-control-plane__deploy-application-az-cli_use-azu_04b1b8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: enable-fips-nodes.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/enable-fips-nodes -->

# Enable Federal Information Process Standard (FIPS) for Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Federal Information Processing Standard (FIPS) 140-2 is a US government standard that defines minimum security requirements for cryptographic modules in information technology products and systems. Azure Kubernetes Service (AKS) allows you to create Linux and Windows node pools with FIPS 140-2 enabled. Deployments running on FIPS-enabled node pools can use those cryptographic modules to provide increased security and help meet security controls as part of FedRAMP compliance. For more information on FIPS 140-2, see [Federal Information Processing Standard (FIPS) 140](/en-us/azure/compliance/offerings/offering-fips-140-2).

Caution

In this article, there are references to a feature that may be using Ubuntu OS versions that are being deprecated for AKS.

- Starting on March 17, 2027, AKS will no longer support Ubuntu 20.04. Existing node images will be deleted and AKS will no longer provide security updates. You'll no longer be able to scale your node pools.
[Upgrade your node pools](upgrade-aks-cluster)to kubernetes version 1.35+ to migrate to a supported Ubuntu version. For more information on this retirement, see[AKS GitHub Issues](https://github.com/Azure/AKS/issues)

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

Azure CLI version 2.32.0 or later installed and configured. To find the version, run `az --version`

. For more information about installing or upgrading the Azure CLI, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Note

AKS Monitoring Addon supports FIPS enabled node pools with Ubuntu, Azure Linux, and Windows starting with Agent version 3.1.17 (Linux) and Win-3.1.17 (Windows).

## Limitations

- FIPS-enabled node pools have the following limitations:
- FIPS-enabled node pools require Kubernetes version 1.19 and greater.
- To update the underlying packages or modules used for FIPS, you must use
[Node Image Upgrade](node-image-upgrade). - Container images on the FIPS nodes aren't assessed for FIPS compliance.
- Mounting of a CIFS share fails because FIPS disables some authentication modules. To work around this issue, see
[Errors when mounting a file share on a FIPS-enabled node pool](/en-us/troubleshoot/azure/azure-kubernetes/fail-to-mount-azure-file-share#fipsnodepool). - FIPS-enabled node pools with
[Arm64 VMs](use-arm64-vms)are only supported with Azure Linux 3.0+. - FIPS isn't supported with
[Flatcar Container Linux for AKS (preview)](flatcar-container-linux-for-aks).


Important

The FIPS-enabled Linux image is a different image than the default Linux image used for Linux-based node pools.

FIPS-enabled node images can have different version numbers, such as kernel version, than images that aren't FIPS-enabled. The update cycle for FIPS-enabled node pools and node images can differ from node pools and images that aren't FIPS-enabled.

## Supported OS Versions

You can create FIPS-enabled node pools on all supported OS types (Linux and Windows). However, not all OS versions support FIPS-enabled node pools. After a new OS version is released, there's typically a waiting period before it's FIPS compliant.

This table includes the supported OS versions:

| OS Type | OS SKU | FIPS Compliance |
|---|---|---|
| Linux | Ubuntu | Supported |
| Linux | Azure Linux | Supported |
| Windows | Windows Server 2019 | Supported |
| Windows | Windows Server 2022 | Supported |

When requesting FIPS enabled Ubuntu, if the default Ubuntu version doesn't support FIPS, AKS defaults to the most recent FIPS-supported version of Ubuntu. For example, Ubuntu 22.04 is default for Linux node pools. Since 22.04 doesn't currently support FIPS, AKS defaults to Ubuntu 20.04 for Linux FIPS-enabled node pools.

Note

Previously, you could use the GetOSOptions API to determine whether a given OS supported FIPS. The GetOSOptions API is now deprecated and it will no longer be included in new AKS API versions starting with 2024-05-01.

## Create a FIPS-enabled Linux node pool

Create a FIPS-enabled Linux node pool using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command with the`--enable-fips-image`

parameter.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name fipsnp \ --enable-fips-image`

Note

You can also use the

`--enable-fips-image`

parameter with the[az aks create](/en-us/cli/azure/aks#az-aks-create)command when creating a cluster to enable FIPS on the default node pool. When adding node pools to a cluster created in this way, you still must use the`--enable-fips-image`

parameter when adding node pools to create a FIPS-enabled node pool.Verify your node pool is FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

The following example output shows the

*fipsnp*node pool is FIPS-enabled:`Name enableFips --------- ------------ fipsnp True nodepool1 False`

List the nodes using the

`kubectl get nodes`

command.`kubectl get nodes`

The following example output shows a list of the nodes in the cluster. The nodes starting with

`aks-fipsnp`

are part of the FIPS-enabled node pool.`NAME STATUS ROLES AGE VERSION aks-fipsnp-12345678-vmss000000 Ready agent 6m4s v1.19.9 aks-fipsnp-12345678-vmss000001 Ready agent 5m21s v1.19.9 aks-fipsnp-12345678-vmss000002 Ready agent 6m8s v1.19.9 aks-nodepool1-12345678-vmss000000 Ready agent 34m v1.19.9`

Run a deployment with an interactive session on one of the nodes in the FIPS-enabled node pool using the

`kubectl debug`

command.`kubectl debug node/aks-fipsnp-12345678-vmss000000 -it --image=mcr.microsoft.com/dotnet/runtime-deps:6.0`

From the interactive session output, verify the FIPS cryptographic libraries are enabled. Your output should look similar to the following example output:

`root@aks-fipsnp-12345678-vmss000000:/# cat /proc/sys/crypto/fips_enabled 1`

FIPS-enabled node pools also have a

*kubernetes.azure.com/fips_enabled=true*label, which deployments can use to target those node pools.

## Create a FIPS-enabled Windows node pool

Create a FIPS-enabled Windows node pool using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command with the`--enable-fips-image`

parameter. Unlike Linux-based node pools, Windows node pools share the same image set.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name fipsnp \ --enable-fips-image \ --os-type Windows`

Verify your node pool is FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

Verify Windows node pools have access to the FIPS cryptographic libraries by

[creating an RDP connection to a Windows node](rdp)in a FIPS-enabled node pool and check the registry. From the**Run**application, enter`regedit`

.Look for

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\FIPSAlgorithmPolicy`

in the registry.If

`Enabled`

is set to*1*, then FIPS is enabled.FIPS-enabled node pools also have a

*kubernetes.azure.com/fips_enabled=true*label, which deployments can use to target those node pools.

## Update an existing node pool to enable or disable FIPS

Existing Linux node pools can be updated to enable or disable FIPS. If you're planning to migrate your node pools from non-FIPS to FIPS, first validate that your application is working properly in a test environment before migrating it to a production environment. Validating your application in a test environment should prevent issues caused by the FIPS kernel blocking some weak cipher or encryption algorithm, such as an MD4 algorithm that isn't FIPS compliant.

Note

When updating an existing Linux node pool to enable or disable FIPS, the node pool update moves between the fips and non-fips image. This node pool update triggers a reimage to complete the update. This can cause the node pool update to take a few minutes to complete.

### Prerequisites

Azure CLI version 2.64.0 or later. To find the version, run `az --version`

. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Enable FIPS on an existing node pool

Existing Linux node pools can be updated to enable FIPS. When you update an existing node pool, the node image changes from the current image to the recommended FIPS image of the same OS SKU.

Update a node pool using the

[az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)command with the`--enable-fips-image`

parameter.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name np \ --enable-fips-image`

This command triggers a reimage of the node pool immediately to deploy the FIPS compliant Operating System. This reimage occurs during the node pool update. No extra steps are required.

Verify that your node pool is FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

The following example output shows that the

*np*node pool is FIPS-enabled:`Name enableFips --------- ------------ np True nodepool1 False`

List the nodes using the

`kubectl get nodes`

command.`kubectl get nodes`

The following example output shows a list of the nodes in the cluster. The nodes starting with

`aks-np`

are part of the FIPS-enabled node pool.`NAME STATUS ROLES AGE VERSION aks-np-12345678-vmss000000 Ready agent 6m4s v1.19.9 aks-np-12345678-vmss000001 Ready agent 5m21s v1.19.9 aks-np-12345678-vmss000002 Ready agent 6m8s v1.19.9 aks-nodepool1-12345678-vmss000000 Ready agent 34m v1.19.9`

Run a deployment with an interactive session on one of the nodes in the FIPS-enabled node pool using the

`kubectl debug`

command.`kubectl debug node/aks-np-12345678-vmss000000 -it --image=mcr.microsoft.com/dotnet/runtime-deps:6.0`

From the interactive session output, verify the FIPS cryptographic libraries are enabled. Your output should look similar to the following example output:

`root@aks-np-12345678-vmss000000:/# cat /proc/sys/crypto/fips_enabled 1`

FIPS-enabled node pools also have a

*kubernetes.azure.com/fips_enabled=true*label, which deployments can use to target those node pools.

## Disable FIPS on an existing node pool

Existing Linux node pools can be updated to disable FIPS. When updating an existing node pool, the node image changes from the current FIPS image to the recommended non-FIPS image of the same OS SKU. The node image change will occur after a reimage.

Update a Linux node pool using the

[az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)command with the`--disable-fips-image`

parameter.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name np \ --disable-fips-image`

This command triggers a reimage of the node pool immediately to deploy the FIPS compliant Operating System. This reimage occurs during the node pool update. No extra steps are required.

Verify that your node pool isn't FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

The following example output shows that the

*np*node pool isn't FIPS-enabled:`Name enableFips --------- ------------ np False nodepool1 False`


## Message of the Day

Pass the `--message-of-the-day`

flag with the location of the file to replace the Message of the Day on Linux nodes at cluster creation or node pool creation.

Create a cluster with message of the day using the [az aks create](/en-us/cli/azure/aks#az-aks-create) command.

```
az aks create --cluster-name myAKSCluster --resource-group myResourceGroup --message-of-the-day ./newMOTD.txt
```


Add a node pool with message of the day using the [az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command.

```
az aks nodepool add --name mynodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --message-of-the-day ./newMOTD.txt
```


## Next steps

To learn more about AKS security, see [Best practices for cluster security and upgrades in Azure Kubernetes Service (AKS)](operator-best-practices-cluster-security).


---

<!-- DOCUMENTO FUSIONADO: _upgrade-aks-control-plane__deploy-application-az-cli_use-azure-linux.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: upgrade-aks-control-plane.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/upgrade-aks-control-plane -->

# Upgrade the Azure Kubernetes Service (AKS) cluster control plane

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) clusters consist of two main components: the **control plane managed by Azure** and the **node pools where your workloads run**. This article focuses on upgrading the control plane independently, which allows you to adopt new Kubernetes versions for API server features while separately managing node pool upgrades.

## Before you begin

- If you're using the Azure CLI, this article requires Azure CLI version 2.34.1 or later. Use the
`az --version`

command to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you're using Azure PowerShell, this article requires Azure PowerShell version 5.9.0 or later. Use the
`Get-InstalledModule -Name Az`

cmdlet to find the version. If you need to install or upgrade, see[Install Azure PowerShell](/en-us/powershell/azure/install-az-ps). - Performing upgrade operations requires the
`Microsoft.ContainerService/managedClusters/agentPools/write`

RBAC role. For more on Azure RBAC roles, see the[Azure resource provider operations](/en-us/azure/role-based-access-control/built-in-roles#containers). - Starting with Kubernetes version 1.30 and 1.27 LTS versions, beta APIs are disabled by default when you upgrade to them.

Warning

Ensure you have sufficient compute quota before upgrading. If quota is low, the upgrade might fail. For more information, see [increase quotas](/en-us/azure/azure-portal/supportability/regional-quota-requests).

## Overview of AKS upgrade types

The following table outlines three types of AKS upgrades, highlighting their scope and use cases:

| Upgrade type | Scope | Use case |
|---|---|---|
|

[Full cluster](#upgrade-the-full-aks-cluster)[Node pool only](upgrade-aks-node-pools-rolling)Tip

Upgrading the control plane first allows you to validate Kubernetes API compatibility before affecting running workloads. For node pool upgrade strategies, see [Configure rolling upgrades](upgrade-aks-node-pools-rolling).

## Kubernetes version upgrade rules

When you upgrade a supported AKS cluster, you can't skip Kubernetes minor versions. You must perform all upgrades sequentially by minor version number. For example, upgrades between *1.28.x* -> *1.29.x* or *1.29.x* -> *1.30.x* are allowed. *1.28.x* -> *1.30.x* isn't allowed.

The control plane can be up to two minor versions ahead of node pools. For example, if your control plane is at *1.30.x*, your node pools can be at *1.28.x*, *1.29.x*, or *1.30.x*.

## Check for available AKS upgrades

Tip

To stay up to date with the latest AKS releases and updates, see the [AKS release tracker](release-tracker).

Check for available Kubernetes releases for your AKS cluster using the [ az aks get-upgrades](/en-us/cli/azure/aks#az-aks-get-upgrades) command.

```
az aks get-upgrades --resource-group <resource-group-name> --name <cluster-name> --output table
```


The following example output shows the current version as *1.28.9* and lists the available versions under `upgrades`

:

```
Name ResourceGroup MasterVersion Upgrades
------- --------------- --------------- --------------
default <resource-group-name> 1.28.9 1.29.2, 1.29.4
```


## Upgrade the AKS control plane only

Upgrade the control plane using the

command with the`az aks upgrade`

`--control-plane-only`

flag. The following example upgrades the control plane to Kubernetes version*1.29.4*:`az aks upgrade \ --resource-group <resource-group-name> \ --name <cluster-name> \ --kubernetes-version 1.29.4 \ --control-plane-only`

Confirm the control plane upgrade was successful using the

command.`az aks show`

`az aks show --resource-group <resource-group-name> --name <cluster-name> --output table`

The following example output shows the control plane now runs

*1.29.4*:`Name Location ResourceGroup KubernetesVersion ProvisioningState Fqdn ------------ ---------- --------------- ------------------- ------------------- ------------------------------------------------ <cluster-name> eastus <resource-group-name> 1.29.4 Succeeded <cluster-name>-dns-123abcd4.hcp.eastus.azmk8s.io`

Verify the node pool versions remain unchanged using the [

`az aks nodepool list`

][az-aks-nodepool-list] command.`az aks nodepool list --resource-group <resource-group-name> --cluster-name <cluster-name> --query "[].{Name:name,Version:orchestratorVersion}" --output table`

In the output, the node pools should still show the previous Kubernetes version.


## Upgrade the full AKS cluster

Note

During a full cluster upgrade, AKS upgrades the control plane first, then upgrades each node pool sequentially. For more control over node pool upgrades, see [Configure rolling upgrades](upgrade-aks-node-pools-rolling).

Upgrade the full cluster (control plane and all node pools) using the [ az aks upgrade](/en-us/cli/azure/aks#az-aks-upgrade) command. The following example upgrades the cluster to Kubernetes version

*1.29.4*:

```
az aks upgrade \
--resource-group <resource-group-name> \
--name <cluster-name> \
--kubernetes-version 1.29.4
```


## Frequently asked questions (FAQs)

### Why were my node pools upgraded when I only upgraded the control plane?

AKS might trigger a rolling node pool upgrade alongside a control plane upgrade to keep the cluster compliant and healthy. This upgrade typically occurs when a previous node upgrade failed or left nodes on mixed versions.

### Can I upgrade node pools before the control plane?

No. The control plane version must always be equal to or greater than any node pool version. You must upgrade the control plane first.

### How long does a control plane upgrade take?

Control plane upgrades typically complete within 5-15 minutes, depending on cluster configuration and Azure region load. Node pool upgrades take longer as they involve draining and reimaging nodes.

## Resolve control plane upgrade issues

### No upgrades available

If `az aks get-upgrades`

shows no available upgrades, your cluster might be:

- Already on the latest supported version.
- On an unsupported version that requires migration.

For unsupported versions, create a new cluster with a supported version and migrate your workloads.

### Upgrade failed due to deprecated APIs

Before upgrading, check for deprecated APIs using tools like [kube-no-trouble (kubent)](https://github.com/doitintl/kube-no-trouble):

```
kubent
```


Update your manifests to use supported API versions before upgrading.


---

<!-- DOCUMENTO FUSIONADO: _deploy-application-az-cli_use-azure-linux.md -->
<!-- URL ORIGINAL: N/A -->

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


---

<!-- DOCUMENTO FUSIONADO: __kaito-custom-inference-model_resize-cluster_open-ai-quickstart.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _kaito-custom-inference-model_resize-cluster.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: kaito-custom-inference-model.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/kaito-custom-inference-model -->

# Onboard custom models for inferencing with the AI toolchain operator (KAITO) on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As an AI engineer or developer, you might have to prototype and deploy AI workloads with a range of different model weights. AKS provides the option to deploy inferencing workloads using open-source presets supported out-of-box and managed in the KAITO [model registry](https://github.com/kaito-project/kaito/tree/main/presets) or to dynamically download from the [HuggingFace registry](https://huggingface.co/models) at runtime onto your AKS cluster.

In this article, you learn how to onboard a sample HuggingFace model for inferencing with the AI toolchain operator add-on without having to manage custom images on Azure Kubernetes Service (AKS).

## Prerequisites

An Azure account with an active subscription. If you don't have an account, you can

[create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An AKS cluster with the AI toolchain operator add-on enabled. For more information, see

[Enable KAITO on an AKS cluster](ai-toolchain-operator#enable-the-ai-toolchain-operator-add-on-on-an-aks-cluster).This example deployment requires quota for the

`Standard_NCads_A100_v4`

virtual machine (VM) family in your Azure subscription. If you don't have quota for this VM family, please[request a quota increase](/en-us/azure/quotas/quickstart-increase-quota-portal).Note

Currently, only the HuggingFace runtime supports inference with the KAITO custom model deployment template.


## Choose an open-source language model from HuggingFace

In this example, we use the [BigScience Bloom-1B7](https://huggingface.co/bigscience/bloom-1b7) small language model. Alternatively, you can choose from thousands of text-generation models supported on [HuggingFace](https://huggingface.co/models?pipeline_tag=text-generation).

Connect to your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group <resource-group-name> --name <aks-cluster-name>`

Clone the KAITO project GitHub repository using the

`git clone`

command.`git clone https://github.com/kaito-project/kaito.git`


## Deploy your model inferencing workload using the KAITO workspace template

Navigate to the

`kaito`

directory and copy the[sample deployment YAML](https://github.com/kaito-project/kaito/tree/main/examples/custom-model-integration/custom-model-deployment.yaml)manifest. Replace the default values in the following fields with your model's requirements. For this example, we specify the**bloom-1b7**HuggingFace model ID for[BigScience Bloom-1B7](https://huggingface.co/bigscience/bloom-1b7)model:`instanceType`

: The minimum VM size for this inference service deployment is`Standard_NC24ads_A100_v4`

. For larger model sizes you can choose a VM in thefamily with higher memory capacity.`Standard_NCads_A100_v4`

`MODEL_ID`

: Replace with your model's specific HuggingFace identifier, which can be found after`https://huggingface.co/`

in the model card URL.`"--torch_dtype"`

: Set to`"float16"`

for compatibility with V100 GPUs. For A100, H100 or newer GPUs, use`"bfloat16"`

.- (Optional)
`HF_TOKEN`

: Specify the values in this section only if you are deploying a private or gated Hugging Face model for inference.

`apiVersion: kaito.sh/v1beta1 kind: Workspace metadata: name: workspace-custom-llm resource: instanceType: "Standard_NC24ads_A100_v4" # Replace with the required VM SKU based on model requirements labelSelector: matchLabels: apps: custom-llm inference: template: spec: containers: - name: custom-llm-container image: mcr.microsoft.com/aks/kaito/kaito-base:0.0.8 # KAITO base image which includes hf runtime livenessProbe: failureThreshold: 3 httpGet: path: /health port: 5000 scheme: HTTP initialDelaySeconds: 600 periodSeconds: 10 successThreshold: 1 timeoutSeconds: 1 readinessProbe: failureThreshold: 3 httpGet: path: /health port: 5000 scheme: HTTP initialDelaySeconds: 30 periodSeconds: 10 successThreshold: 1 timeoutSeconds: 1 resources: requests: nvidia.com/gpu: 1 # Request 1 GPU; adjust as needed limits: nvidia.com/gpu: 1 # Optional: Limit to 1 GPU command: - "accelerate" args: - "launch" - "--num_processes" - "1" - "--num_machines" - "1" - "--gpu_ids" - "all" - "tfs/inference_api.py" - "--pipeline" - "text-generation" - "--trust_remote_code" - "--allow_remote_files" - "--pretrained_model_name_or_path" - "bloom-1b7" - "--torch_dtype" - "bfloat16" # env: # HF_TOKEN is required only for private or gated Hugging Face models # Uncomment and configure this block if needed # - name: HF_TOKEN # valueFrom: # secretKeyRef: # name: hf-token-secret # Replace with your Kubernetes Secret name # key: HF_TOKEN # Replace with the specific key holding the token volumeMounts: - name: dshm mountPath: /dev/shm volumes: - name: dshm emptyDir: medium: Memory`

Save these changes to your

`custom-model-deployment.yaml`

file.Run the deployment in your AKS cluster using the

`kubectl apply`

command.`kubectl apply -f custom-model-deployment.yaml`


## Test your custom model inferencing service

Track the live resource changes in your KAITO workspace using the

`kubectl get workspace`

command.`kubectl get workspace workspace-custom-llm -w`

Note

Note that machine readiness can take

*up to 10 minutes*, and workspace readiness*up to 20 minutes*.Check your language model inference service and get the service IP address using the

`kubectl get svc`

command.`export SERVICE_IP=$(kubectl get svc workspace-custom-llm -o jsonpath='{.spec.clusterIP}')`

Test your custom model inference service with a sample input of your choice using the

[OpenAI API format](https://platform.openai.com/docs/api-reference/chat):`kubectl run -it --rm --restart=Never curl --image=curlimages/curl -- curl -X POST http://$SERVICE_IP/v1/completions \ -H "Content-Type: application/json" \ -d '{ "model": "bloom-1b7", "prompt": "What sport should I play in rainy weather?", "max_tokens": 20 }'`


## Clean up resources

If you no longer need these resources, you can delete them to avoid incurring extra Azure compute charges.

Delete the KAITO inference workspace using the `kubectl delete workspace`

command.

```
kubectl delete workspace workspace-custom-llm
```


## Next steps

In this article, you learned how to onboard a HuggingFace model for inferencing with the AI toolchain operator add-on directly to your AKS cluster. To learn more about AI and machine learning on AKS, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: resize-cluster.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/resize-cluster -->

# Resize Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to resize an Azure Kubernetes Service (AKS) cluster. It's important to right-size your clusters to optimize costs and performance. You can manually resize a cluster by adding or removing the nodes to meet the needs of your applications. You can also autoscale your cluster to automatically adjust the number of nodes in response to changing demands.

## Cluster right-sizing

When you create an AKS cluster, you specify the number of nodes and the size of the nodes, which determines the compute capacity of the cluster. Oversized clusters can lead to unnecessary costs, while undersized clusters can lead to performance issues. You can adjust the number and size of the nodes in the cluster to right-size the cluster to meet the needs of your applications.

Consider the following factors when right-sizing your cluster:

**Resource requirements**: Understand the resource requirements of your applications to determine the number of nodes and the size of the nodes needed to run your workloads.**Performance requirements**: Determine the performance requirements of your applications to ensure that the cluster can meet the demands of your workloads.**Cost considerations**: Optimize costs by right-sizing your cluster to avoid unnecessary costs associated with oversized clusters.**Application demands**: Monitor the demands of your applications to adjust the size of the cluster in response to changing demands.**Infrastructure constraints**: Consider the infrastructure constraints of your environment, such as capacity or reserved instance limiting to specific SKUs, to ensure that the cluster can be right-sized within the limits of your environment.

## Monitor cluster performance and cost

Closely monitor the performance and cost of your clusters to ensure they're right-sized to meet the needs of your application and make adjustments as needed. You can use the following resources for monitoring:

[Identify high CPU usage in Azure Kubernetes Service (AKS) clusters](/en-us/troubleshoot/azure/azure-kubernetes/availability-performance/identify-high-cpu-consuming-containers-aks)[Troubleshoot memory saturation in Azure Kubernetes Service (AKS) clusters](/en-us/troubleshoot/azure/azure-kubernetes/availability-performance/identify-memory-saturation-aks)[Cost analysis add-on for Azure Kubernetes Service (AKS)](cost-analysis)[Configure the Metrics Server Vertical Pod Autoscaler (VPA) in Azure Kubernetes Service (AKS)](use-metrics-server-vertical-pod-autoscaler)

## When to resize a cluster

You might want to resize a cluster in scenarios such as the following:

- If you see that CPU and memory usage is consistently low, consider
*downsizing*the cluster. If usage is consistently high, make sure you have[autoscaling enabled](#automatically-resize-an-aks-cluster)and increase the maximum node count if necessary. - The
[cost analysis add-on for AKS](cost-analysis)shows you details about node usage and cost that indicate you might benefit from cluster resizing. For example, if you see that your nodes have a*high idle cost*with a*low usage cost*, you might consider resizing your cluster to reduce costs. - The
[Metrics Server VPA](use-metrics-server-vertical-pod-autoscaler)shows you that your requests and/or limits are too high or low based on historical usage. You can use this information to adjust your cluster size to better match your workload. - You experience performance issues such as resource starvation. This might be a result of the cluster being undersized for the demands of your applications.

## What happens when I resize a cluster?

### Increasing cluster size

You can increase the size of an AKS cluster by adding nodes to the cluster. You can [add nodes to the cluster manually](scale-cluster) or [configure autoscaling to automatically adjust the number of nodes](#automatically-resize-an-aks-cluster) in response to changing demands.

When you increase the size of a cluster, the following changes occur:

- New node instances are created using the same configuration as the existing nodes in the cluster.
- New pods might be scheduled on the new nodes to distribute the workload across the cluster.
- Existing pods don't move to the new nodes unless they are rescheduled due to node failures or other reasons.

### Decreasing cluster size

You can decrease the size of an AKS cluster by removing nodes from the cluster. When you remove nodes from the cluster, the nodes are automatically drained and removed from the cluster. You can remove nodes from the cluster manually or configure autoscaling to automatically adjust the number of nodes in response to changing demands.

When you decrease the size of a cluster, the following changes occur:

- AKS gracefully terminates the nodes and drains the pods running on the nodes before removing the nodes from the cluster.
- Any pods managed by a replication controller are rescheduled on other node instances in the cluster.
- Any pods that aren't managed by a replication controller aren't restarted.

## Manually resize an AKS cluster

- Resize an AKS cluster using the
command with the`az aks scale`

`--node-count`

and`--nodepool-name`

parameters.

Before running the resize command, set the required environment variables with your own values. The example values should be substituted with your actual resource group, cluster, desired node count, and node pool name.

```
az aks scale --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --node-count $NUM_NODES --nodepool-name $NODE_POOL_NAME
```


Results:

```
{
"agentPoolProfiles": [
{
"count": 4,
"maxCount": null,
"minCount": null,
"name": "nodepool1",
...
}
],
"dnsPrefix": "xxxxx",
"fqdn": "xxxxx.xxxxx.xxxxxx.cloudapp.azure.com",
...
}
```


Repeat this command for each node pool in the cluster that you want to resize. If your cluster has only one node pool, you can omit the `--nodepool-name`

parameter.

## Automatically resize an AKS cluster

Use the [cluster autoscaler](cluster-autoscaler-overview) to automatically resize your node pools in response to changing demands.

For more information, see the [Cluster autoscaling in Azure Kubernetes Service (AKS) overview](cluster-autoscaler-overview). To configure cluster autoscaling in AKS, see [Use the cluster autoscaler in Azure Kubernetes Service (AKS)](cluster-autoscaler).

## Next steps

In this article, you learned how to right-size an AKS cluster. To learn more about managing AKS clusters, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: open-ai-quickstart.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/open-ai-quickstart -->

# Deploy an application that uses OpenAI on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy an application that uses Azure OpenAI or OpenAI on AKS. With OpenAI, you can easily adapt different AI models, such as content generation, summarization, semantic search, and natural language to code generation, for your specific tasks. You start by deploying an AKS cluster in your Azure subscription. Then, you deploy your OpenAI service and the sample application.

The sample cloud native application is representative of real-world implementations. The multi-container application is comprised of applications written in multiple languages and frameworks, including:

- Golang with Gin
- Rust with Actix-Web
- JavaScript with Vue.js and Fastify
- Python with FastAPI

These applications provide front ends for customers and store admins, REST APIs for sending data to RabbitMQ message queue and MongoDB database, and console apps to simulate traffic.

Note

We don't recommend running stateful containers, such as MongoDB and Rabbit MQ, without persistent storage for production. We use them here for simplicity, but we recommend using managed services, such as Azure CosmosDB or Azure Service Bus.

To access the GitHub codebase for the sample application, see [AKS Store Demo](https://github.com/Azure-Samples/aks-store-demo).

## Before you begin

- You need an Azure account with an active subscription. If you don't have one,
[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - For this demo, you can either use Azure OpenAI service or OpenAI service.
- If you plan on using Azure OpenAI service, you need to request access to enable it on your Azure subscription using the
[Request access to Azure OpenAI Service form](https://aka.ms/oai/access). - If you plan on using OpenAI, sign up on the
[OpenAI website](https://openai.com/).

- If you plan on using Azure OpenAI service, you need to request access to enable it on your Azure subscription using the

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which you deploy and manage Azure resources. When you create a resource group, you're prompted to specify a location. This location is the storage location of your resource group metadata and where your resources run in Azure if you don't specify another region during resource creation.

The following example creates a resource group named *myResourceGroup* in the *eastus* location.

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

The following example output shows successful creation of the resource group:

`{ "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup", "location": "eastus", "managedBy": null, "name": "myResourceGroup", "properties": { "provisioningState": "Succeeded" }, "tags": null, "type": "Microsoft.Resources/resourceGroups" }`


## Create an AKS cluster

The following example creates a cluster named *myAKSCluster* in *myResourceGroup*.

Create an AKS cluster using the

command.`az aks create`

`az aks create --resource-group myResourceGroup --name myAKSCluster --generate-ssh-keys`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.


## Connect to the cluster

To manage a Kubernetes cluster, you use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell.

Install

`kubectl`

locally using thecommand.`az aks install-cli`

`az aks install-cli`

Note

If your Linux-based system requires elevated permissions, you can use the

`sudo az aks install-cli`

command.Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand.`az aks get-credentials`

This command executes the following operations:

- Downloads credentials and configures the Kubernetes CLI to use them.
- Uses
`~/.kube/config`

, the default location for the[Kubernetes configuration file](https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/). Specify a different location for your Kubernetes configuration file using*--file*argument.

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using the

command. This command returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`

The following example output shows the nodes created in the previous steps. Make sure the node status is

*Ready*.`NAME STATUS ROLES AGE VERSION aks-nodepool1-31469198-vmss000000 Ready agent 3h29m v1.25.6 aks-nodepool1-31469198-vmss000001 Ready agent 3h29m v1.25.6 aks-nodepool1-31469198-vmss000002 Ready agent 3h29m v1.25.6`


Note

For private clusters, the nodes might be unreachable if you try to connect to them through the public IP address. In order to fix this, you need to create an endpoint within the same VNET as the cluster to connect from. Follow the instructions to [Create a private AKS cluster](private-clusters) and then connect to it.

## Deploy the application

The [AKS Store application](https://github.com/Azure-Samples/aks-store-demo) manifest includes the following Kubernetes deployments and services:

**Product service**: Shows product information.**Order service**: Places orders.**Makeline service**: Processes orders from the queue and completes the orders.**Store front**: Web application for customers to view products and place orders.**Store admin**: Web application for store employees to view orders in the queue and manage product information.**Virtual customer**: Simulates order creation on a scheduled basis.**Virtual worker**: Simulates order completion on a scheduled basis.**Mongo DB**: NoSQL instance for persisted data.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as MongoDB and Rabbit MQ, without persistent storage for production. We use them here for simplicity, but we recommend using managed services, such as Azure CosmosDB or Azure Service Bus.

Review the

[YAML manifest](https://github.com/Azure-Samples/aks-store-demo/blob/main/aks-store-all-in-one.yaml)for the application.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/aks-store-all-in-one.yaml`

The following example output shows the successfully created deployments and services:

`deployment.apps/mongodb created service/mongodb created deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/makeline-service created service/makeline-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created deployment.apps/store-admin created service/store-admin created deployment.apps/virtual-customer created deployment.apps/virtual-worker created`


## Deploy OpenAI

You can either use Azure OpenAI or OpenAI and run your application on AKS.

- In the Azure portal, create an Azure OpenAI instance.
- Navigate to the Azure OpenAI instance you created.
- From the
**Overview**blade, navigate to the[Azure AI Foundry portal](https://oai.azure.com/portal/). - Create a new
**Chat**deployment using the**gpt-4o-mini**base model.

For more information on how to create a deployment in Azure OpenAI, see [Get started generating text using Azure OpenAI Service](/en-us/azure/ai-services/openai/quickstart).

## Deploy the AI service

Now that the application is deployed, you can deploy the Python-based microservice that uses OpenAI to automatically generate descriptions for new products being added to the store's catalog.

Create a file named

`ai-service.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: ai-service spec: replicas: 1 selector: matchLabels: app: ai-service template: metadata: labels: app: ai-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: ai-service image: ghcr.io/azure-samples/aks-store-demo/ai-service:latest ports: - containerPort: 5001 env: - name: USE_AZURE_OPENAI value: "True" - name: AZURE_OPENAI_DEPLOYMENT_NAME value: "" - name: AZURE_OPENAI_ENDPOINT value: "" - name: OPENAI_API_KEY value: "" resources: requests: cpu: 20m memory: 50Mi limits: cpu: 50m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: ai-service spec: type: ClusterIP ports: - name: http port: 5001 targetPort: 5001 selector: app: ai-service`

Set the environment variable

`USE_AZURE_OPENAI`

to`"True"`

.Get your Azure OpenAI deployment name from

[Azure AI Foundry](https://oai.azure.com/portal/)and fill in the`AZURE_OPENAI_DEPLOYMENT_NAME`

value.Get your Azure OpenAI endpoint and Azure OpenAI API key from the Azure portal by selecting

**Keys and Endpoint**in the left blade of the resource. Update the`AZURE_OPENAI_ENDPOINT`

and`OPENAI_API_KEY`

in the YAML accordingly.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f ai-service.yaml`

The following example output shows the successfully created deployments and services:

`deployment.apps/ai-service created service/ai-service created`


Note

Directly adding sensitive information, such as API keys, to your Kubernetes manifest files isn't secure and may accidentally get committed to code repositories. We added it here for simplicity. For production workloads, use [Managed Identity](/en-us/azure/ai-services/openai/how-to/managed-identity#authorize-access-to-managed-identities) to authenticate to Azure OpenAI service instead or store your secrets in [Azure Key Vault](csi-secrets-store-driver).

## Test the application

Check the status of the deployed pods using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command.`kubectl get pods`

Make sure all the pods are

*Running*before continuing to the next step.`NAME READY STATUS RESTARTS AGE makeline-service-7db94dc7d4-8g28l 1/1 Running 0 99s mongodb-78f6d95f8-nptbz 1/1 Running 0 99s order-service-55cbd784bb-6bmfb 1/1 Running 0 99s product-service-6bf4d65f74-7cbvk 1/1 Running 0 99s rabbitmq-9855984f9-94nlm 1/1 Running 0 99s store-admin-7f7d768c48-9hn8l 1/1 Running 0 99s store-front-6786c64d97-xq5s9 1/1 Running 0 99s virtual-customer-79498f8667-xzsb7 1/1 Running 0 99s virtual-worker-6d77fff4b5-7g7rj 1/1 Running 0 99s`

Get the IP of the store admin web application and store front web application using the

`kubectl get service`

command.`kubectl get service store-admin`

The application exposes the Store Admin site to the internet via a public load balancer provisioned by the Kubernetes service. This process can take a few minutes to complete.

**EXTERNAL IP**initially shows*pending*until the service comes up and shows the IP address.`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-admin LoadBalancer 10.0.142.228 40.64.86.161 80:32494/TCP 50m`

Repeat the same step for the service named `store-front``.

Open a web browser and browse to the external IP address of your service. In the example shown here, open

*40.64.86.161*to see Store Admin in the browser. Repeat the same step for Store Front.In store admin, select the products tab, then select

**Add Products**.When the `ai-service`` is running successfully, you should see the Ask OpenAI button next to the description field. Fill in the name, price, and keywords, then generate a product description by selecting

**Ask OpenAI**>**Save product**.You can now see the new product you created on Store Admin used by sellers. In the picture, you can see Dog Smart Collar is added.

You can also see the new product you created on Store Front used by buyers. In the picture, you can see Dog Smart Collar is added. Remember to get the IP address of store front using the

command.`kubectl get service`


## Next steps

Now that you added OpenAI functionality to an AKS application, you can [Secure access to Azure OpenAI from Azure Kubernetes Service (AKS)](open-ai-secure-access-quickstart).

To learn more about generative AI use cases, see the following resources:
