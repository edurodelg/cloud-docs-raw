---
merged_at: 2026-01-26T20:54:26.182992
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _outbound-rules-control-egress__azure-ad-rbac__container-network-security-l7-pol_5524f9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: outbound-rules-control-egress.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/outbound-rules-control-egress -->

# Outbound network and FQDN rules for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides the necessary details that allow you to secure outbound traffic from your Azure Kubernetes Service (AKS). It contains the cluster requirements for a base AKS deployment and additional requirements for optional addons and features. You can apply this information to any outbound restriction method or appliance.

To see an example configuration using Azure Firewall, visit [Control egress traffic using Azure Firewall in AKS](limit-egress-traffic).

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Background

AKS clusters are deployed on a virtual network. This network can either be customized and preconfigured by you or it can be created and managed by AKS. In either case, the cluster has **outbound**, or egress, dependencies on services outside of the virtual network.

For management and operational purposes, nodes in an AKS cluster need to access certain ports and fully qualified domain names (FQDNs). These endpoints are required for the nodes to communicate with the API server or to download and install core Kubernetes cluster components and node security updates. For example, the cluster needs to pull container images from Microsoft Artifact Registry (MAR).

The AKS outbound dependencies are almost entirely defined with FQDNs, which don't have static addresses behind them. The lack of static addresses means you can't use network security groups (NSGs) to lock down the outbound traffic from an AKS cluster.

By default, AKS clusters have unrestricted outbound internet access. This level of network access allows nodes and services you run to access external resources as needed. If you wish to restrict egress traffic, a limited number of ports and addresses must be accessible to maintain healthy cluster maintenance tasks. For outbound internet traffic, it's not recommended to set all deny rules in an NSG.

A [network isolated AKS cluster](concepts-network-isolated), provides the simplest and most secure solution for setting up outbound restrictions for a cluster out of the box. A network isolated cluster pulls the images for cluster components and add-ons from a private Azure Container Registry (ACR) instance connected to the cluster instead of pulling from MAR. If the images aren't present, the private ACR pulls them from MAR and serves them via its private endpoint, eliminating the need to enable egress from the cluster to the public MAR endpoint. The cluster operator can then incrementally set up allowed outbound traffic securely over a private network for each scenario they want to enable. This way the cluster operators have complete control over designing the allowed outbound traffic from their clusters right from the start, thus allowing them to reduce the risk of data exfiltration.

Another solution to securing outbound addresses is using a firewall device that can control outbound traffic based on domain names. Azure Firewall can restrict outbound HTTP and HTTPS traffic based on the FQDN of the destination. You can also configure your preferred firewall and security rules to allow these required ports and addresses.

Important

This document covers only how to lock down the traffic leaving the AKS subnet. AKS has no ingress requirements by default. Blocking **internal subnet traffic** using network security groups (NSGs) and firewalls isn't supported. To control and block the traffic within the cluster, see [Secure traffic between pods using network policies in AKS](use-network-policies).

## Required outbound network rules and FQDNs for AKS clusters

The following network and FQDN/application rules are required for an AKS cluster. You can use them if you wish to configure a solution other than Azure Firewall.

- IP address dependencies are for non-HTTP/S traffic (both TCP and UDP traffic).
- FQDN HTTP/HTTPS endpoints can be placed in your firewall device.
- Wildcard HTTP/HTTPS endpoints are dependencies that can vary with your AKS cluster based on a number of qualifiers.
- AKS uses an admission controller to inject the FQDN as an environment variable to all deployments under kube-system and gatekeeper-system. This ensures all system communication between nodes and API server uses the API server FQDN and not the API server IP. You can get the same behavior on your own pods, in any namespace, by annotating the pod spec with an annotation named
`kubernetes.azure.com/set-kube-service-host-fqdn`

. If that annotation is present, AKS will set the KUBERNETES_SERVICE_HOST variable to the domain name of the API server instead of the in-cluster service IP. This is useful in cases where the cluster egress is via a layer 7 firewall. - If you have an app or solution that needs to talk to the API server, you must either add an
**additional**network rule to allow**TCP communication to port 443 of your API server's IP****OR**, if you have a layer 7 firewall configured to allow traffic to the API Server's domain name, set`kubernetes.azure.com/set-kube-service-host-fqdn`

in your pod specs. - On rare occasions, if there's a maintenance operation, your API server IP might change. Planned maintenance operations that can change the API server IP are always communicated in advance.
- You might notice traffic towards "md-*.blob.storage.azure.net" endpoint. This endpoint is used for internal components of Azure Managed Disks. Blocking access to this endpoint from your firewall should not cause any issues.
- You might notice traffic towards "umsa*.blob.core.windows.net" endpoint. This endpoint is used to store manifests for Azure Linux VM Agent & Extensions and is regularly checked to download new versions. You can find more details on
[VM Extensions](/en-us/azure/virtual-machines/extensions/features-linux?tabs=azure-cli#network-access).

### Azure Global required network rules

| Destination Endpoint | Protocol | Port | Use |
|---|---|---|---|
`*:1194` Or
`AzureCloud.<Region>:1194` Or
`RegionCIDRs:1194` Or `APIServerPublicIP:1194` `(only known after cluster creation)` |
UDP | 1194 | For tunneled secure communication between the nodes and the control plane. This isn't required for
konnectivity-agent enabled. |

`*:9000`

*Or*[ServiceTag](/en-us/azure/virtual-network/service-tags-overview#available-service-tags)-`AzureCloud.<Region>:9000`

*Or*[Regional CIDRs](/en-us/azure/virtual-network/service-tags-overview#discover-service-tags-by-using-downloadable-json-files)-`RegionCIDRs:9000`

*Or*`APIServerPublicIP:9000`

`(only known after cluster creation)`

[private clusters](private-clusters), or for clusters with the*konnectivity-agent*enabled.**or**`*:123`

**(if using Azure Firewall network rules)**`ntp.ubuntu.com:123`

`CustomDNSIP:53`

`(if using custom DNS servers)`

`APIServerPublicIP:443`

`(if running pods/deployments, like Ingress Controller, that access the API Server)`

[private clusters](private-clusters).### Azure Global required FQDN / application rules

| Destination FQDN | Port | Use |
|---|---|---|
`*.hcp.<location>.azmk8s.io` |
`HTTPS:443` |
Required for Node <-> API server communication. Replace <location> with the region where your AKS cluster is deployed. This is required for clusters with konnectivity-agent enabled. Konnectivity also uses Application-Layer Protocol Negotiation (ALPN) to communicate between agent and server. Blocking or rewriting the ALPN extension will cause a failure. This isn't required for
|
`mcr.microsoft.com` |
`HTTPS:443` |
Required to access images in Microsoft Container Registry (MCR). This registry contains first-party images/charts (for example, coreDNS, etc.). These images are required for the correct creation and functioning of the cluster, including scale and upgrade operations. |
, `*.data.mcr.microsoft.com` `mcr-0001.mcr-msedge.net` |
`HTTPS:443` |
Required for MCR storage backed by the Azure content delivery network (CDN). |
`management.azure.com` |
`HTTPS:443` |
Required for Kubernetes operations against the Azure API. |
`login.microsoftonline.com` |
`HTTPS:443` |
Required for Microsoft Entra authentication. |
`packages.microsoft.com` |
`HTTPS:443` |
This address is the Microsoft packages repository used for cached apt-get operations. Example packages include Moby, PowerShell, and Azure CLI. |
`acs-mirror.azureedge.net` |
`HTTPS:443` |
This address is for the repository required to download and install required binaries like kubenet and Azure CNI. |
`packages.aks.azure.com` |
`HTTPS:443` |
This address will be replacing `acs-mirror.azureedge.net` in the future and will be used to download and install required Kubernetes and Azure CNI binaries. |

### Microsoft Azure operated by 21Vianet required network rules

For information about retired Microsoft Defender for Cloud features, see [Microsoft Defender for Containers](#microsoft-defender-for-containers).

| Destination Endpoint | Protocol | Port | Use |
|---|---|---|---|
`*:1194` Or
`AzureCloud.Region:1194` Or
`RegionCIDRs:1194` Or `APIServerPublicIP:1194` `(only known after cluster creation)` |
UDP | 1194 | For tunneled secure communication between the nodes and the control plane. |
`*:9000` Or
`AzureCloud.<Region>:9000` Or
`RegionCIDRs:9000` Or `APIServerPublicIP:9000` `(only known after cluster creation)` |
TCP | 9000 | For tunneled secure communication between the nodes and the control plane. |
`*:22` Or
`AzureCloud.<Region>:22` Or
`RegionCIDRs:22` Or `APIServerPublicIP:22` `(only known after cluster creation)` |
TCP | 22 | For tunneled secure communication between the nodes and the control plane. |
or `*:123` (if using Azure Firewall network rules)`ntp.ubuntu.com:123` |
UDP | 123 | Required for Network Time Protocol (NTP) time synchronization on Linux nodes. |
`CustomDNSIP:53` `(if using custom DNS servers)` |
UDP | 53 | If you're using custom DNS servers, you must ensure they're accessible by the cluster nodes. |
`APIServerPublicIP:443` `(if running pods/deployments, like Ingress Controller, that access the API Server)` |
TCP | 443 | Required if running pods/deployments that access the API Server (like Ingress Controller), those pod/deployments would use the API IP. |

### Microsoft Azure operated by 21Vianet required FQDN / application rules

For information about retired Microsoft Defender for Cloud features, see [Microsoft Defender for Containers](#microsoft-defender-for-containers).

| Destination FQDN | Port | Use |
|---|---|---|
`*.hcp.<location>.cx.prod.service.azk8s.cn` |
`HTTPS:443` |
Required for Node <-> API server communication. Replace <location> with the region where your AKS cluster is deployed. |
`*.tun.<location>.cx.prod.service.azk8s.cn` |
`HTTPS:443` |
Required for Node <-> API server communication. Replace <location> with the region where your AKS cluster is deployed. |
`mcr.microsoft.com` |
`HTTPS:443` |
Required to access images in Microsoft Container Registry (MCR). This registry contains first-party images/charts (for example, coreDNS, etc.). These images are required for the correct creation and functioning of the cluster, including scale and upgrade operations. |
`*.data.mcr.microsoft.com` |
`HTTPS:443` |
Required for MCR storage backed by the Azure Content Delivery Network (CDN). |
`management.chinacloudapi.cn` |
`HTTPS:443` |
Required for Kubernetes operations against the Azure API. |
`login.chinacloudapi.cn` |
`HTTPS:443` |
Required for Microsoft Entra authentication. |
`packages.microsoft.com` |
`HTTPS:443` |
This address is the Microsoft packages repository used for cached apt-get operations. Example packages include Moby, PowerShell, and Azure CLI. |
`*.azk8s.cn` |
`HTTPS:443` |
This address is for the repository required to download and install required binaries like kubenet and Azure CNI. |
, `mcr.azure.cn` `*.data.mcr.azure.cn` |
`HTTPS:443` |
Required to access images Microsoft Container Registry (MCR) in China Cloud (Mooncake). This registry serves as a cache for mcr.microsoft.com with improved reliability and performance. |

### Azure US Government required network rules

| Destination Endpoint | Protocol | Port | Use |
|---|---|---|---|
`*:1194` Or
`AzureCloud.<Region>:1194` Or
`RegionCIDRs:1194` Or `APIServerPublicIP:1194` `(only known after cluster creation)` |
UDP | 1194 | For tunneled secure communication between the nodes and the control plane. |
`*:9000` Or
`AzureCloud.<Region>:9000` Or
`RegionCIDRs:9000` Or `APIServerPublicIP:9000` `(only known after cluster creation)` |
TCP | 9000 | For tunneled secure communication between the nodes and the control plane. |
or `*:123` (if using Azure Firewall network rules)`ntp.ubuntu.com:123` |
UDP | 123 | Required for Network Time Protocol (NTP) time synchronization on Linux nodes. |
`CustomDNSIP:53` `(if using custom DNS servers)` |
UDP | 53 | If you're using custom DNS servers, you must ensure they're accessible by the cluster nodes. |
`APIServerPublicIP:443` `(if running pods/deployments, like Ingress Controller, that access the API Server)` |
TCP | 443 | Required if running pods/deployments that access the API Server (like Ingress Controller), those pods/deployments would use the API IP. |

### Azure US Government required FQDN / application rules

| Destination FQDN | Port | Use |
|---|---|---|
`*.hcp.<location>.cx.aks.containerservice.azure.us` |
`HTTPS:443` |
Required for Node <-> API server communication. Replace <location> with the region where your AKS cluster is deployed. |
`mcr.microsoft.com` |
`HTTPS:443` |
Required to access images in Microsoft Container Registry (MCR). This registry contains first-party images/charts (for example, coreDNS, etc.). These images are required for the correct creation and functioning of the cluster, including scale and upgrade operations. |
`*.data.mcr.microsoft.com` |
`HTTPS:443` |
Required for MCR storage backed by the Azure content delivery network (CDN). |
`management.usgovcloudapi.net` |
`HTTPS:443` |
Required for Kubernetes operations against the Azure API. |
`login.microsoftonline.us` |
`HTTPS:443` |
Required for Microsoft Entra authentication. |
`packages.microsoft.com` |
`HTTPS:443` |
This address is the Microsoft packages repository used for cached apt-get operations. Example packages include Moby, PowerShell, and Azure CLI. |
`acs-mirror.azureedge.net` |
`HTTPS:443` |
This address is for the repository required to install required binaries like kubenet and Azure CNI. |
`packages.aks.azure.com` |
`HTTPS:443` |
This address will be replacing `acs-mirror.azureedge.net` in the future and will be used to download and install required Kubernetes and Azure CNI binaries. |

## Optional recommended FQDN / application rules for AKS clusters

The following FQDN / application rules aren't required, but are recommended for AKS clusters:

| Destination FQDN | Port | Use |
|---|---|---|
`security.ubuntu.com` , `azure.archive.ubuntu.com` , `changelogs.ubuntu.com` |
`HTTP:80` |
This address lets the Linux cluster nodes download the required security patches and updates. |
`snapshot.ubuntu.com` |
`HTTPS:443` |
This address lets the Linux cluster nodes download the required security patches and updates from ubuntu snapshot service. |

If you choose to block/not allow these FQDNs, the nodes will only receive OS updates when you do a [node image upgrade](node-image-upgrade) or [cluster upgrade](upgrade-cluster). Keep in mind that node image upgrades also come with updated packages including security fixes.

## GPU enabled AKS clusters required FQDN / application rules

| Destination FQDN | Port | Use |
|---|---|---|
`nvidia.github.io` |
`HTTPS:443` |
This address is used for correct driver installation and operation on GPU-based nodes. |
`us.download.nvidia.com` |
`HTTPS:443` |
This address is used for correct driver installation and operation on GPU-based nodes. |
`download.docker.com` |
`HTTPS:443` |
This address is used for correct driver installation and operation on GPU-based nodes. |

## Windows Server based node pools required FQDN / application rules

| Destination FQDN | Port | Use |
|---|---|---|
`onegetcdn.azureedge.net, go.microsoft.com` |
`HTTPS:443` |
To install windows-related binaries |
`*.mp.microsoft.com, www.msftconnecttest.com, ctldl.windowsupdate.com` |
`HTTP:80` |
To install windows-related binaries |

If you choose to block/not allow these FQDNs, the nodes will only receive OS updates when you do a [node image upgrade](node-image-upgrade) or [cluster upgrade](upgrade-cluster). Keep in mind that Node Image Upgrades also come with updated packages including security fixes.

## AKS features, addons, and integrations

### Workload identity

#### Required FQDN / application rules

| Destination FQDN | Port | Use |
|---|---|---|
or `login.microsoftonline.com` or `login.chinacloudapi.cn` `login.microsoftonline.us` |
`HTTPS:443` |
Required for Microsoft Entra authentication. |

### Microsoft Defender for Containers

Important

All Microsoft Defender for Cloud features will be officially retired in the Azure in China region on August 18, 2026. Due to this upcoming retirement, Azure in China customers are no longer able to onboard new subscriptions to the service. A new subscription is any subscription that was not already onboarded to the Microsoft Defender for Cloud service prior to August 18, 2025, the date of the retirement announcement. For more information on the retirement, see [Microsoft Defender for Cloud Deprecation in Microsoft Azure Operated by 21Vianet Announcement](https://aka.ms/mdcretirementinchina).

Customers should work with their account representatives for Microsoft Azure operated by 21Vianet to assess the impact of this retirement on their own operations.

#### Required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`login.microsoftonline.com` (Azure Government) `login.microsoftonline.us` (Azure operated by 21Vianet)`login.microsoftonline.cn` |
`HTTPS:443` |
Required for Microsoft Entra Authentication. |
`*.ods.opinsights.azure.com` (Azure Government) `*.ods.opinsights.azure.us` (Azure operated by 21Vianet)`*.ods.opinsights.azure.cn` |
`HTTPS:443` |
Required for Microsoft Defender to upload security events to the cloud. |
`*.oms.opinsights.azure.com` (Azure Government) `*.oms.opinsights.azure.us` (Azure operated by 21Vianet)`*.oms.opinsights.azure.cn` |
`HTTPS:443` |
Required to authenticate with Log Analytics workspaces. |
`*.cloud.defender.microsoft.com` |
`HTTPS:443` |
NEW: Required for Microsoft Defender to upload security events to the cloud. |

### Azure Key Vault provider for Secrets Store CSI Driver

If using network isolated clusters, it's recommended to set up [private endpoint to access Azure Key Vault](/en-us/azure/key-vault/general/private-link-service?tabs=portal).

If your cluster has outbound type user-defined routing and Azure Firewall, the following network rules and application rules are applicable:

#### Required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`vault.azure.net` |
`HTTPS:443` |
Required for CSI Secret Store addon pods to talk to Azure KeyVault server. |
`*.vault.usgovcloudapi.net` |
`HTTPS:443` |
Required for CSI Secret Store addon pods to talk to Azure KeyVault server in Azure Government. |

### Azure Monitor - Managed Prometheus, Container Insights, and Azure Monitor Application Insights Autoinstrumentation

If using network isolated clusters, it's recommended to set up [private endpoint based ingestion](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-private-link#container-insights-log-analytics-workspace), which is supported for Managed Prometheus (Azure Monitor workspace), Container insights (Log Analytics workspace), and Azure Monitor Application Insights Autoinstrumentation (Application Insights resource).

If your cluster has outbound type user-defined routing and Azure Firewall, the following network rules and application rules are applicable:

#### Required network rules

| Destination Endpoint | Protocol | Port | Use |
|---|---|---|---|
`AzureMonitor:443` |

#### Azure public cloud required FQDN / application rules

| Endpoint | Purpose | Port |
|---|---|---|
`*.ods.opinsights.azure.com` |
443 | |
`*.oms.opinsights.azure.com` |
443 | |
`dc.services.visualstudio.com` |
443 | |
`*.in.applicationinsights.azure.com` |
Application Insights Autoinstrumentation. To limit the scope, can be changed to only allow endpoints in connection strings for the destination resources | 443 |
`*.monitoring.azure.com` |
443 | |
`login.microsoftonline.com` |
443 | |
`global.handler.control.monitor.azure.com` |
Access control service | 443 |
`*.ingest.monitor.azure.com` |
Container Insights - logs ingestion endpoint (DCE) | 443 |
`*.metrics.ingest.monitor.azure.com` |
Azure monitor managed service for Prometheus - metrics ingestion endpoint (DCE) | 443 |
`<cluster-region-name>.handler.control.monitor.azure.com` |
Fetch data collection rules for specific cluster | 443 |

#### Microsoft Azure operated by 21Vianet cloud required FQDN / application rules

For information about retired Microsoft Defender for Cloud features, see [Microsoft Defender for Containers](#microsoft-defender-for-containers).

| Endpoint | Purpose | Port |
|---|---|---|
`*.ods.opinsights.azure.cn` |
Data ingestion | 443 |
`*.oms.opinsights.azure.cn` |
Azure Monitor agent (AMA) onboarding | 443 |
`dc.services.visualstudio.com` |
For agent telemetry that uses Azure Public Cloud Application Insights | 443 |
`*.in.applicationinsights.azure.com` |
Application Insights Autoinstrumentation. To limit the scope, can be changed to only allow endpoints in connection strings for the destination resources | 443 |
`global.handler.control.monitor.azure.cn` |
Access control service | 443 |
`<cluster-region-name>.handler.control.monitor.azure.cn` |
Fetch data collection rules for specific cluster | 443 |
`*.ingest.monitor.azure.cn` |
Container Insights - logs ingestion endpoint (DCE) | 443 |
`*.metrics.ingest.monitor.azure.cn` |
Azure monitor managed service for Prometheus - metrics ingestion endpoint (DCE) | 443 |

#### Azure Government cloud required FQDN / application rules

| Endpoint | Purpose | Port |
|---|---|---|
`*.ods.opinsights.azure.us` |
Data ingestion | 443 |
`*.oms.opinsights.azure.us` |
Azure Monitor agent (AMA) onboarding | 443 |
`dc.services.visualstudio.com` |
For agent telemetry that uses Azure Public Cloud Application Insights | 443 |
`*.in.applicationinsights.azure.com` |
Application Insights Autoinstrumentation. To limit the scope, can be changed to only allow endpoints in connection strings for the destination resources | 443 |
`global.handler.control.monitor.azure.us` |
Access control service | 443 |
`<cluster-region-name>.handler.control.monitor.azure.us` |
Fetch data collection rules for specific cluster | 443 |
`*.ingest.monitor.azure.us` |
Container Insights - logs ingestion endpoint (DCE) | 443 |
`*.metrics.ingest.monitor.azure.us` |
Azure monitor managed service for Prometheus - metrics ingestion endpoint (DCE) | 443 |

### Azure Policy

#### Required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`data.policy.core.windows.net` |
`HTTPS:443` |
This address is used to pull the Kubernetes policies and to report cluster compliance status to policy service. |
`store.policy.core.windows.net` |
`HTTPS:443` |
This address is used to pull the Gatekeeper artifacts of built-in policies. |
`dc.services.visualstudio.com` |
`HTTPS:443` |
Azure Policy add-on that sends telemetry data to applications insights endpoint. |

#### Microsoft Azure operated by 21Vianet required FQDN / application rules

For information about retired Microsoft Defender for Cloud features, see [Microsoft Defender for Containers](#microsoft-defender-for-containers).

| FQDN | Port | Use |
|---|---|---|
`data.policy.azure.cn` |
`HTTPS:443` |
This address is used to pull the Kubernetes policies and to report cluster compliance status to policy service. |
`store.policy.azure.cn` |
`HTTPS:443` |
This address is used to pull the Gatekeeper artifacts of built-in policies. |

#### Azure US Government required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`data.policy.azure.us` |
`HTTPS:443` |
This address is used to pull the Kubernetes policies and to report cluster compliance status to policy service. |
`store.policy.azure.us` |
`HTTPS:443` |
This address is used to pull the Gatekeeper artifacts of built-in policies. |

### AKS cost analysis add-on

#### Required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`management.azure.com` (Azure Government) `management.usgovcloudapi.net` (Azure operated by 21Vianet)`management.chinacloudapi.cn` |
`HTTPS:443` |
Required for Kubernetes operations against the Azure API. |
`login.microsoftonline.com` (Azure Government) `login.microsoftonline.us` (Azure operated by 21Vianet)`login.microsoftonline.cn` |
`HTTPS:443` |
Required for Microsoft Entra ID authentication. |

## Cluster extensions

### Required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`<region>.dp.kubernetesconfiguration.azure.com` |
`HTTPS:443` |
This address is used to fetch configuration information from the Cluster Extensions service and report extension status to the service. |
`mcr.microsoft.com, *.data.mcr.microsoft.com` |
`HTTPS:443` |
This address is required to pull container images for installing cluster extension agents on AKS cluster. |
`arcmktplaceprod.azurecr.io` |
`HTTPS:443` |
This address is required to pull container images for installing marketplace extensions on AKS cluster. |
`arcmktplaceprod.centralindia.data.azurecr.io` |
`HTTPS:443` |
This address is for the Central India regional data endpoint and is required to pull container images for installing marketplace extensions on AKS cluster. |
`arcmktplaceprod.japaneast.data.azurecr.io` |
`HTTPS:443` |
This address is for the East Japan regional data endpoint and is required to pull container images for installing marketplace extensions on AKS cluster. |
`arcmktplaceprod.westus2.data.azurecr.io` |
`HTTPS:443` |
This address is for the West US2 regional data endpoint and is required to pull container images for installing marketplace extensions on AKS cluster. |
`arcmktplaceprod.westeurope.data.azurecr.io` |
`HTTPS:443` |
This address is for the West Europe regional data endpoint and is required to pull container images for installing marketplace extensions on AKS cluster. |
`arcmktplaceprod.eastus.data.azurecr.io` |
`HTTPS:443` |
This address is for the East US regional data endpoint and is required to pull container images for installing marketplace extensions on AKS cluster. |
`*.ingestion.msftcloudes.com, *.microsoftmetrics.com` |
`HTTPS:443` |
This address is used to send agents metrics data to Azure. |
`marketplaceapi.microsoft.com` |
`HTTPS: 443` |
This address is used to send custom meter-based usage to the commerce metering API. |

#### Azure US Government required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`<region>.dp.kubernetesconfiguration.azure.us` |
`HTTPS:443` |
This address is used to fetch configuration information from the Cluster Extensions service and report extension status to the service. |
`mcr.microsoft.com, *.data.mcr.microsoft.com` |
`HTTPS:443` |
This address is required to pull container images for installing cluster extension agents on AKS cluster. |

Note

For any addons that aren't explicitly stated here, the core requirements cover it.

### Istio-based service mesh add-on

In Istio=based service mesh add-on, if you are setting up istiod with a Plugin Certificate Authority (CA) or if you are setting up secure ingress gateway, Azure Key Vault provider for Secrets Store CSI Driver is required for these features. Outbound network requirements for Azure Key Vault provider for Secrets Store CSI Driver can be found [here](#azure-key-vault-provider-for-secrets-store-csi-driver).

### Application routing add-on

Application routing add-on supports SSL termination at the ingress with certificates stored in Azure Key Vault. Outbound network requirements for Azure Key Vault provider for Secrets Store CSI Driver can be found [here](#azure-key-vault-provider-for-secrets-store-csi-driver).

## Next steps

In this article, you learned what ports and addresses to allow if you want to restrict egress traffic for the cluster.

If you want to restrict how pods communicate between themselves and East-West traffic restrictions within cluster see [Secure traffic between pods using network policies in AKS](use-network-policies).


---

<!-- DOCUMENTO FUSIONADO: _azure-ad-rbac__container-network-security-l7-policy-concepts_tutorial-kubernete_b97cff.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: azure-ad-rbac.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-ad-rbac -->

# Use Kubernetes RBAC with Microsoft Entra ID in AKS

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) can be configured to use Microsoft Entra ID for user authentication. In this configuration, you sign in to an AKS cluster using a Microsoft Entra authentication token. Once authenticated, you can use the built-in Kubernetes role-based access control (RBAC) to manage access to namespaces and cluster resources based on a user's identity or group membership.

This article shows you how to:

Control access using Kubernetes RBAC in an AKS cluster based on Microsoft Entra group membership.

Create example groups and users in Microsoft Entra ID.

Create Roles and RoleBindings in an AKS cluster granting the appropriate permissions, such as to create and view resources.


## Prerequisites

You have an existing AKS cluster with Microsoft Entra integration enabled. If you need an AKS cluster with this configuration, see

[Integrate Microsoft Entra ID with AKS](managed-azure-ad).Kubernetes RBAC is enabled by default during AKS cluster creation. To upgrade an existing cluster with Microsoft Entra integration and Kubernetes RBAC, see

[Enable Microsoft Entra integration on your existing AKS cluster](managed-azure-ad#use-an-existing-cluster).Make sure that Azure CLI version 2.0.61 or later is installed and configured. To find the version, run

`az --version`

. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).If using Terraform, install

[Terraform](/en-us/azure/developer/terraform/overview)version 2.99.0 or later.

Use the Azure portal or Azure CLI to verify Microsoft Entra integration with Kubernetes RBAC is enabled.

To verify using the Azure portal:

- Sign-in to the
[Azure portal](https://portal.azure.com)and navigate to your AKS cluster resource. - In the service menu, under
**Settings**, select**Security configuration**. - Under the
**Authentication and Authorization**section, verify the**Microsoft Entra authentication with Kubernetes RBAC**option is selected.

## Create groups in Microsoft Entra ID

This section teaches you how to create two user roles to show how Kubernetes RBAC and Microsoft Entra ID control access cluster resources. The following two example roles are:

**Application developer**- A user named
*aksdev*that's part of the*appdev*group.

- A user named
**Site reliability engineer**(SRE)- A user named
*akssre*that's part of the*opssre*group.

- A user named

In production environments, you can use existing users and groups within a Microsoft Entra tenant.

First, get the resource ID of your AKS cluster using the

command. Then, assign the resource ID to a variable named`az aks show`

*AKS_ID*so it can be referenced in other commands.`AKS_ID=$(az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query id -o tsv)`

Create the first example group in Microsoft Entra ID for the application developers using the

command. The following example creates a group named`az ad group create`

*appdev*:`APPDEV_ID=$(az ad group create --display-name appdev --mail-nickname appdev --query id -o tsv)`

Create an Azure role assignment for the

*appdev*group using thecommand. This assignment lets any member of the group use`az role assignment create`

`kubectl`

to interact with an AKS cluster by granting them the*Azure Kubernetes Service Cluster User*Role.`az role assignment create \ --assignee $APPDEV_ID \ --role "Azure Kubernetes Service Cluster User Role" \ --scope $AKS_ID`

Tip

If you receive an error such as

`Principal 35bfec9328bd4d8d9b54dea6dac57b82 doesn't exist in the directory a5443dcd-cd0e-494d-a387-3039b419f0d5.`

, wait a few seconds for the Microsoft Entra group object ID to propagate through the directory then try the`az role assignment create`

command again.

## Create users in Microsoft Entra ID

After you create the example Microsoft Entra ID groups for application developers and SREs, the next step is to create two corresponding user accounts. These users are used to sign in to the AKS cluster and validate the Kubernetes RBAC integration described later in this article.

Before you begin, you must set the user principal name (UPN) and password for the application developers. The UPN must include the verified domain name of your tenant. For example, an application developer user, `aksdev@contoso.com`

. In order to figure out (or set) the verified domain names in your tenant, see [Managing custom domain names in your Microsoft Entra ID](/en-us/entra/identity/users/domains-manage).

The following command prompts you for the UPN and sets it to *AAD_DEV_UPN* so it can be used in a later command:

```
echo "Please enter the UPN for application developers: " && read AAD_DEV_UPN
```


The following command prompts you for the password and sets it to *AAD_DEV_PW* for use in a later command:

```
echo "Please enter the secure password for application developers: " && read AAD_DEV_PW
```


### Create user accounts

Create the first user account in Microsoft Entra ID using the

command. The following example creates a user with the display name`az ad user create`

*AKS Dev*, the UPN, and secure password using the values in*AAD_DEV_UPN*and*AAD_DEV_PW*:`AKSDEV_ID=$(az ad user create \ --display-name "AKS Dev" \ --user-principal-name $AAD_DEV_UPN \ --password $AAD_DEV_PW \ --query id -o tsv)`

Add the user to the

*appdev*group created in the previous section using thecommand:`az ad group member add`

`az ad group member add --group appdev --member-id $AKSDEV_ID`


## Create AKS cluster resources

We have our Microsoft Entra groups, users, and Azure role assignments created. Now, you configure the AKS cluster to allow these different groups access to specific resources.

Get the cluster admin credentials using the

command. In one of the following sections, you get the regular`az aks get-credentials`

*user*cluster credentials to see the Microsoft Entra authentication flow in action.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --admin`

Create a namespace in the AKS cluster using the

command. The following example creates a namespace name`kubectl create namespace`

*dev*:`kubectl create namespace dev`

Note

In Kubernetes,

*Roles*define the permissions to grant, and*RoleBindings*apply them to desired users or groups. These assignments can be applied to a given namespace, or across the entire cluster. For more information, see[Using Kubernetes RBAC authorization](concepts-identity#kubernetes-rbac).If the user you grant the Kubernetes RBAC binding for is in the same Microsoft Entra tenant, assign permissions based on the

**UPN**. If the user is in a different Microsoft Entra tenant, query for and use the*objectId*property instead.Create a Role for the

*dev*namespace, which grants full permissions to the namespace. In production environments, you can specify more granular permissions for different users or groups. Create a file named`role-dev-namespace.yaml`

and paste the following YAML manifest:`kind: Role apiVersion: rbac.authorization.k8s.io/v1 metadata: name: dev-user-full-access namespace: dev rules: - apiGroups: ["", "extensions", "apps"] resources: ["*"] verbs: ["*"] - apiGroups: ["batch"] resources: - jobs - cronjobs verbs: ["*"]`

Create the Role using the

command and specify the filename of your YAML manifest.`kubectl apply`

`kubectl apply -f role-dev-namespace.yaml`

Get the resource ID for the

*appdev*group using thecommand. This group is set as the subject of a RoleBinding in the next step.`az ad group show`

`az ad group show --group appdev --query id -o tsv`

Create a RoleBinding for the

*appdev*group to use the previously created Role for namespace access. Create a file named`rolebinding-dev-namespace.yaml`

and paste the following YAML manifest. On the last line, replace*groupObjectId*with the group object ID output from the previous command.`kind: RoleBinding apiVersion: rbac.authorization.k8s.io/v1 metadata: name: dev-user-access namespace: dev roleRef: apiGroup: rbac.authorization.k8s.io kind: Role name: dev-user-full-access subjects: - kind: Group namespace: dev name: groupObjectId`

Tip

If you want to create the RoleBinding for a single user, specify

*kind: User*and replace*groupObjectId*with the UPN in the previous sample.Create the RoleBinding using the

command and specify the filename of your YAML manifest:`kubectl apply`

`kubectl apply -f rolebinding-dev-namespace.yaml`


## Access AKS cluster resources with Microsoft Entra identities

Now, test that the expected permissions work when you create and manage resources in an AKS cluster. In these examples, you schedule and view pods in the user's assigned namespace, and try to schedule and view pods outside of the assigned namespace.

Reset the

*kubeconfig*context using thecommand. In a previous section, you set the context using the cluster admin credentials. The admin user bypasses Microsoft Entra sign-in prompts. Without the`az aks get-credentials`

`--admin`

parameter, the user context is applied that requires all requests to be authenticated using Microsoft Entra ID.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --overwrite-existing`

Schedule a basic NGINX pod using the

command in the`kubectl run`

*dev*namespace:`kubectl run nginx-dev --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev`

Enter the credentials for the

*appdev*group account (enter*your*own credentials) at the sign-in prompt. Once you're successfully signed in, the account token is cached for future`kubectl`

commands. The NGINX is successfully scheduled as shown in the following example output:`$ kubectl run nginx-dev --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code B24ZD6FP8 to authenticate. pod/nginx-dev created`

Use the

command to view pods in the`kubectl get pods`

*dev*namespace:`kubectl get pods --namespace dev`

Ensure the status of the NGINX pod is

*Running*. The output looks like the following output:`$ kubectl get pods --namespace dev NAME READY STATUS RESTARTS AGE nginx-dev 1/1 Running 0 4m`


### Test SRE access to AKS cluster resources

To confirm that our Microsoft Entra group membership and Kubernetes RBAC work correctly between different users and groups, try the previous commands when signed in as the *akssre* user.

Reset the

*kubeconfig*context using thecommand that clears the previously cached authentication token for the`az aks get-credentials`

*aksdev*user.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --overwrite-existing`

Schedule and view pods in the assigned

*SRE*namespace. When prompted, sign in with the*opssre*group account credentials (enter*your*own credentials).`kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace sre kubectl get pods --namespace sre`

As shown in the following example output, you can successfully create and view the pods:

`$ kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace sre`

To sign in, use a web browser to open the page

[https://microsoft.com/devicelogin](https://microsoft.com/devicelogin)and enter the code BM4RHP3FD to authenticate.`pod/nginx-sre created $ kubectl get pods --namespace sre NAME READY STATUS RESTARTS AGE nginx-sre 1/1 Running 0`

Try to view or schedule pods outside of assigned SRE namespace.

`kubectl get pods --all-namespaces kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev`

These

`kubectl`

commands fail, as shown in the following example output. The user's group membership and Kubernetes Role and RoleBindings don't grant permissions to create or manager resources in other namespaces.`$ kubectl get pods --all-namespaces Error from server (Forbidden): pods is forbidden: User "akssre@contoso.com" cannot list pods at the cluster scope $ kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev Error from server (Forbidden): pods is forbidden: User "akssre@contoso.com" cannot create pods in the namespace "dev"`


### Create and view cluster resources outside of the assigned namespace

To view pods outside of the *dev* namespace. Use the [ kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command using

`--all-namespaces`

:```
kubectl get pods --all-namespaces
```


The user's group membership doesn't have a Kubernetes Role that allows this action, as shown in the following example output:

```
Error from server (Forbidden): pods is forbidden: User "aksdev@contoso.com" cannot list resource "pods" in API group "" at the cluster scope
```


In the same way, schedule a pod in a different namespace, such as the *SRE* namespace. The user's group membership doesn't align with a Kubernetes Role and RoleBinding to grant these permissions, as shown in the following example output:

```
$ kubectl run nginx-dev --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace sre
Error from server (Forbidden): pods is forbidden: User "akssre@contoso.com" cannot create resource "pods" in API group "" in the namespace "sre"
```


### Clean up cluster resources

To clean up all of the resources, run the following commands:

```
# Get the admin kubeconfig context to delete the necessary cluster resources.
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --admin
# Delete the dev and SRE namespaces. This also deletes the pods, Roles, and RoleBindings.
kubectl delete namespace dev
kubectl delete namespace sre
# Delete the Azure AD user accounts for aksdev and akssre.
az ad user delete --upn-or-object-id $AKSDEV_ID
az ad user delete --upn-or-object-id $AKSSRE_ID
# Delete the Azure AD groups for appdev and opssre. This also deletes the Azure role assignments.
az ad group delete --group appdev
az ad group delete --group opssre
```


## Next steps

For more information about how to secure Kubernetes clusters, see

[Access and identity options for AKS](concepts-identity#kubernetes-rbac).For best practices on identity and resource control, see

[Best practices for authentication and authorization in AKS](operator-best-practices-identity).


---

<!-- DOCUMENTO FUSIONADO: _container-network-security-l7-policy-concepts_tutorial-kubernetes-paas-services.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: container-network-security-l7-policy-concepts.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/container-network-security-l7-policy-concepts -->

# Overview of Layer 7 (L7) policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Network policies are essential for securing Kubernetes clusters by defining and controlling pod communication. They mitigate unauthorized access and potential security breaches by regulating traffic flow. Advanced Container Networking Services strengthens security with [FQDN-based network policies](container-network-security-fqdn-filtering-concepts). Expanding on this foundation, Advanced Container Networking Services now provides L7 policy support, enabling detailed inspection and management of application-level traffic. This advancement enhances both the security and efficiency of network communications within AKS clusters. The offering includes comprehensive support for widely adopted protocols, including HTTP, gRPC, and Kafka.

## Components of L7 policy

**Envoy proxy**: Envoy, part of ACNS security agent acts as the enforcement point for L7 policies. A TPROXY inspects application traffic, comparing it against the defined L7 policies. To enhance scalability and resource management, Envoy is deployed as a separate DaemonSet, decoupled from the Cilium Agent.

## How L7 policy works

When L7 policy enforcement is enabled for an application or pod, outgoing network traffic is first evaluated to determine compliance with the configured application-level rules. The eBPF probe attached to the source pod’s network interface marks the packets, which are then redirected to a node-local Envoy Proxy. This redirection occurs only for pods enforcing L7 policies, ensuring that policy enforcement is applied selectively.

The Envoy proxy, augmented with Cilium network filters, then decides whether to forward the traffic to the destination pod based on policy criteria. If permitted, the traffic proceeds; if not, Envoy returns an appropriate error code to the originating pod. Upon successful authorization, the Envoy proxy facilitates the traffic flow, providing application-level visibility and control. This allows the Cilium agent to enforce detailed network policies within the policy engine. The following diagram illustrates the high-level flow of L7 policy enforcement.

## Monitoring L7 traffic with Hubble and Grafana

To gain insights into L7 traffic flows, specifically HTTP, gRPC, and Kafka, Azure CNI Powered by Cilium leverages Hubble agent, which is enabled by default with Advanced Container Networking Services. Hubble provides detailed flow-level metrics.

To simplify the analysis of these L7 metrics, we provide pre-configured Azure Managed Grafana dashboards. You can find them under the **Dashboards > Azure Managed Prometheus** folder, with filenames like **"Kubernetes/Networking/L7 (Namespace)"** and **"Kubernetes/Networking/L7 (Workload)"**.

These dashboards offer granular visibility into L7 flow data at the cluster, namespace, and workload levels.

Note

These dashboards will only display data if you have this feature enabled on your cluster and have relevant policies applied.
Additionally, the monitoring metrics are **not** required to flow through Envoy, a component of the ACNS security agent. Rather, these metrics are collected by the Hubble agent, which is installed on your cluster as part of the Advanced Container Networking Service's observability feature.

## Key benefits

**Granular Application-Level Control**: L7 policies allow for fine-grained control over network traffic based on application-specific attributes, such as HTTP methods, gRPC paths, and Kafka topics. This extends beyond the basic IP address and port-based control of traditional network policies.

**Enhanced Security**: By inspecting application-level traffic, L7 policies can prevent attacks that exploit vulnerabilities at the application layer. This includes blocking unauthorized access to specific APIs or services. Furthermore, L7 policies are an important component of a Zero Trust security strategy, enabling the enforcement of the principle of least privilege at the application layer.

**Graceful Error Handling**: Unlike L3/L4 policies that typically drop unauthorized traffic silently, L7 policies can return application-level error codes (for example, HTTP 403, Kafka authorization failures), allowing applications to handle errors more gracefully.

**Observability**: With observability enabled for Advanced Container Networking Services and L7 policies applied to your AKS cluster, you can monitor traffic and policy effectiveness using Grafana dashboards.

## Limitations and considerations

- Current feature support relies on Cilium's Layer 7 policy enforcement based on HTTP, HTTPS, gRPC, and Kafka.
- The maximum supported cluster size is up to 1,000 nodes or 40,000 pods, whichever is greater.
- Traffic traversing Envoy proxies do come with latency. Users may experience noticeable latency degradation beyond 3,000 requests per second.
- As part of our observability solution, we provide envoy_http_rq_total metrics. These metrics give the total request count, which could be used to derive requests per seconds (rps).
- During a Cilium upgrade or rollout, existing sessions can be gracefully closed. Applications are expected to handle these interruptions gracefully—typically by implementing retry mechanisms at the connection or request level. New connections initiated during the rollout aren't impacted.
- L7 policy isn't supported by CiliumClusterwideNetworkPolicy(CCNP).
- L7 policy through Advanced Container Networking Services (ACNS) isn't compatible with L7 policies implemented via alternate methods such as Istio. The following table summarizes the supported scenarios.

| Feature/Component | L7 Policies using AKS, Istio - Managed addon |
|---|---|
| K8s network policies by Azure CNI powered by Cilium | Supported |
| L4 (FQDN) Policies by Azure CNI powered by Cilium and ACNS | Supported |
| L7 (HTTP(s)/GRPC/Kafka) Policies by Azure CNI powered by Cilium and ACNS | Not Supported |

## Pricing

Important

Advanced Container Networking Services is a paid offering. For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Next steps

Learn how to apply

[L7 policies](how-to-apply-l7-policies)on AKS.Explore how the open source community builds

[Cilium Network Policies](https://docs.cilium.io/en/latest/security/policy/).For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).Explore Container Network Observability features in Advanced Container Networking Services in

[What is Container Network Observability?](advanced-container-networking-services-overview#container-network-observability)


---

<!-- DOCUMENTO FUSIONADO: tutorial-kubernetes-paas-services.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-paas-services -->

# Tutorial - Use PaaS services with an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

With Kubernetes, you can use PaaS services, such as [Azure Service Bus](/en-us/azure/service-bus-messaging/service-bus-messaging-overview), to develop and run your applications.

In this tutorial, you create an Azure Service Bus namespace and queue to test your application. You learn how to:

- Create an Azure Service Bus namespace and queue.
- Update the Kubernetes manifest file to use the Azure Service Bus queue.
- Test the updated application by placing an order.

## Before you begin

In previous tutorials, you packaged an application into a container image, uploaded the image to Azure Container Registry, created a Kubernetes cluster, and deployed an application. To complete this tutorial, you need the pre-created `aks-store-quickstart.yaml`

Kubernetes manifest file. This file download was included with the application source code in a previous tutorial. Make sure you cloned the repo and changed directories into the cloned repo. If you haven't completed these steps and want to follow along, start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.34.1 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create environment variables

Create the following environment variables to use for the commands in this tutorial:

`LOC_NAME=westus2 RAND=$RANDOM RG_NAME=myResourceGroup AKS_NAME=myAKSCluster SB_NS=sb-store-demo-$RAND`


## Create Azure Service Bus namespace and queue

In previous tutorials, you used a RabbitMQ container to store orders submitted by the `order-service`

. In this tutorial, you use an Azure Service Bus namespace to provide a scoping container for the Service Bus resources within the application. You also use an Azure Service bus queue to send and receive messages between the application components. For more information on Azure Service Bus, see [Create an Azure Service Bus namespace and queue](/en-us/azure/service-bus-messaging/service-bus-quickstart-cli).

Create an Azure Service Bus namespace using the

command.`az servicebus namespace create`

`az servicebus namespace create --name $SB_NS --resource-group $RG_NAME --location $LOC_NAME`

Create an Azure Service Bus queue using the

command.`az servicebus queue create`

`az servicebus queue create --name orders --resource-group $RG_NAME --namespace-name $SB_NS`

Create an Azure Service Bus authorization rule using the

command.`az servicebus queue authorization-rule create`

`az servicebus queue authorization-rule create \ --name sender \ --namespace-name $SB_NS \ --resource-group $RG_NAME \ --queue-name orders \ --rights Send`

Get the Azure Service Bus credentials for later use by using the

and`az servicebus namespace show`

commands.`az servicebus queue authorization-rule keys list`

`az servicebus namespace show --name $SB_NS --resource-group $RG_NAME --query name -o tsv az servicebus queue authorization-rule keys list --namespace-name $SB_NS --resource-group $RG_NAME --queue-name orders --name sender --query primaryKey -o tsv`


## Update Kubernetes manifest file

Configure

`kubectl`

to connect to your cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Open the

`aks-store-quickstart.yaml`

file in a text editor.Remove the existing

`rabbitmq`

StatefulSet, ConfigMap, and Service sections and replace the existing`order-service`

Deployment section with the following content:`apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: <REPLACE_WITH_YOUR_ACR_NAME>.azurecr.io/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "<REPLACE_WITH_YOUR_SB_NS_HOSTNAME>" # Example: sb-store-demo-123456.servicebus.windows.net - name: ORDER_QUEUE_PORT value: "5671" - name: ORDER_QUEUE_TRANSPORT value: "tls" - name: ORDER_QUEUE_USERNAME value: "sender" - name: ORDER_QUEUE_PASSWORD value: "<REPLACE_WITH_YOUR_SB_SENDER_PASSWORD>" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi startupProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 20 periodSeconds: 10 readinessProbe: httpGet: path: /health port: 3000 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3`

Note

Directly adding sensitive information, such as API keys, to your Kubernetes manifest files isn't secure and may accidentally get committed to code repositories. We added it here for simplicity. For production workloads, use

[Managed Identity](use-managed-identity)to authenticate with Azure Service Bus or store your secrets in[Azure Key Vault](csi-secrets-store-driver).Save and close the updated

`aks-store-quickstart.yaml`

file.

## Deploy the updated application

Deploy the updated application using the

`kubectl apply`

command.`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the successfully updated resources:

`deployment.apps/order-service configured service/order-service unchanged deployment.apps/product-service unchanged service/product-service unchanged deployment.apps/store-front configured service/store-front unchanged`


## Test the application

### Place a sample order

Get the external IP address of the

`store-front`

service using the`kubectl get service`

command.`kubectl get service store-front`

Navigate to the external IP address of the

`store-front`

service in your browser using`http://<external-ip>`

.Place an order by choosing a product and selecting

**Add to cart**.Select

**Cart**to view your order, and then select**Checkout**.

### View the order in the Azure Service Bus queue

- Navigate to the Azure portal and open the Azure Service Bus namespace you created earlier.
- Under
**Entities**, select**Queues**, and then select the**orders**queue. - In the
**orders**queue, select**Service Bus Explorer**. - Select
**Peek from start**to view the order you submitted.

## Next steps

In this tutorial, you used Azure Service Bus to update and test the sample application. You learned how to:

- Create an Azure Service Bus namespace and queue.
- Update the Kubernetes manifest file to use the Azure Service Bus queue.
- Test the updated application by placing an order.

In the next tutorial, you learn how to scale an application in AKS.


---

<!-- DOCUMENTO FUSIONADO: __upgrade-os-version__vertical-pod-autoscaler-api-reference_use-node-auto-provis_7395ec.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _upgrade-os-version__vertical-pod-autoscaler-api-reference_use-node-auto-provisi_8f3c42.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: upgrade-os-version.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/upgrade-os-version -->

# Upgrade operating system (OS) versions in AKS

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes OS versions available for Azure Kubernetes Service (AKS) nodes, and best practices for testing and upgrading your OS version.

Caution

In this article, there are references to Ubuntu and Azure Linux OS versions that are being deprecated for AKS:

- Starting on
**March 17, 2027**, AKS will no longer support Ubuntu 20.04. Existing node images will be deleted and AKS will no longer provide security updates. You'll no longer be able to scale your node pools. Migrate to a supported Ubuntu version by[upgrading your node pools](upgrade-aks-cluster)to Kubernetes version 1.34+. For more information on this retirement, see[Retirement: Ubuntu 20.04 node pools on AKS](https://github.com/Azure/AKS/issues/4874). - As of
**November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the[202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning**March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by[upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster)to a supported Kubernetes version or migrating to[osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see[[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Supported OS versions

Each [node image](node-images) corresponds to an OS version, which you can specify using OS SKU. You can specify the following parameters when creating clusters and node pools:

**--os-type**: OS type, including Linux or Windows.*You can't specify the Windows OS type during cluster creation or update.***--os-sku**: Used to specify OS version or OS variant.*You can't specify the Windows OS SKU during cluster creation or update.*For more information for supported OS SKU options, see[Azure AKS CLI](/en-us/cli/azure/aks#az-aks-create)or[API](/en-us/rest/api/aks/agent-pools/create-or-update#ossku).**--kubernetes-version**: Version of Kubernetes to use for creating the node pool or cluster.


Best practice guidanceThe default OS version is the most recent validated version.


- For Ubuntu, we recommend creating clusters and node pools while specifying
`--os-type Linux`

and`--os-sku Ubuntu`

. This will automatically update you to the latest default Ubuntu version based on your Kubernetes version.- For Azure Linux, we recommend creating clusters and node pools while specifying
`--os-type Linux`

and`--os-sku AzureLinux`

. This will automatically update you to the latest default Azure Linux version based on your Kubernetes version.- For Windows, we recommend creating node pools while specifying
`--os-type Windows`

and`--os-sku Windows2022`

. You need to manually update node pools to the next OS version when it's released.

| OS type | OS SKU | Supported Kubernetes versions | Default versioning |
|---|---|---|---|
| Linux | Ubuntu | This OS SKU is supported in all Kubernetes versions. | OS version for this OS SKU changes based on your Kubernetes version. Ubuntu 22.04 is default for Kubernetes versions 1.25 to 1.34. Ubuntu 24.04 is default for Kubernetes versions 1.35+. |
| Linux | Ubuntu2404 | This OS SKU will only be supported in Kubernetes 1.32 to 1.38. | We recommend this versioned OS SKU if you want to migrate to the new OS version without upgrading your Kubernetes version. Ubuntu 24.04 is default when using `--os-sku Ubuntu` in Kubernetes versions 1.35+. |
| Linux | Ubuntu2204 | This OS SKU is supported in Kubernetes versions 1.25 to 1.36. | We recommend this versioned OS SKU if you need to roll back to Ubuntu 22.04. Ubuntu 22.04 is default when using `--os-sku Ubuntu` in Kubernetes versions 1.25 to 1.35. |
| Linux | AzureLinux | This OS SKU is supported in all Kubernetes versions. | OS version for this OS SKU changes based on your Kubernetes version. Azure Linux 2.0 is default for Kubernetes version 1.27 to 1.31. Azure Linux 3.0 is default for Kubernetes version 1.32+. When the `AzureLinuxV3Preview` feature flag is enabled on AKS 1.31, `--os-sku AzureLinux` defaults to 3.0. |
| Linux | AzureLinux3 | This OS SKU is supported in Kubernetes 1.28 to 1.36. | We recommend this OS SKU if you want to test out the new OS version without upgrading your Kubernetes version. You can also use this OS SKU to migrate from Azure Linux 2.0 to Azure Linux 3.0. |
| Linux | AzureLinuxOSGuard | This OS SKU is supported in Kubernetes versions 1.32 and above. | Azure Linux with OS Guard versions are upgraded through node image upgrades. For more information, see
|

[Flatcar Container Linux for AKS](flatcar-container-linux-for-aks).## Migrate to a new OS version

When a new OS version releases on AKS, it's initially supported in preview. After testing in preview for a few months, AKS makes the new OS version generally available (GA) and then updates the default OS SKU (`Ubuntu`

or `AzureLinux`

) to the latest GA OS version. This default update occurs with a new Kubernetes version release.

We recommend testing your nonproduction workloads with the new OS version when it becomes available in preview. In order to access preview functions, make sure you have the preview extension installed. You can install the extension using the `az extension add --name aks-preview`

command.

There are two ways to migrate to a new OS version:

**Default OS SKU**: If you're using a default OS SKU such as`Ubuntu`

or`AzureLinux`

, you automatically get the latest GA version when you[upgrade your Kubernetes version](manage-node-pools). There are no manual changes required to migrate to a new OS version.**Versioned OS SKU**: If you're using a versioned OS SKU such as`Ubuntu2404`

,`AzureLinux3`

, or`Windows2025`

, you need to manually migrate to a new OS version to avoid blocked Kubernetes upgrades. If you're using a Linux OS, you can update the OS SKU on an existing node pool to manually migrate.

### Update OS SKU on an existing node pool

Update the `os-sku`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. In cases where there's a new OS version available in preview, this functionality allows you to migrate your node pool to the new OS version without needing to upgrade your Kubernetes version.

Note

The following values aren't supported for node pool update command:

`--os-sku Windows2019`

`--os-sku Windows2022`

`--os-sku Windows2025`


Instead, you need to add node pools to your cluster with the corresponding `--os-sku`

you intend to use.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku Ubuntu \
--name $NODE_POOL_NAME \
--node-count 1
```


You can use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command to migrate between any supported Linux

`os-sku`

. The command might fail if the target OS doesn't have a supported node image for your Kubernetes version, VM size, or FIPS enablement.#### Migrate to Ubuntu 24.04

Ubuntu 24.04 is the default for `--os-sku Ubuntu`

in Kubernetes versions 1.35+. You can also use Ubuntu 24.04 by specifying `--os-sku Ubuntu2404`

.

Note

Keep the following information in mind when migrating to `--os-sku Ubuntu2404`

:

[FIPS](enable-fips-nodes)is not supported.- Ubuntu 24.04 is supported in Kubernetes versions 1.32 to 1.38.
- You need to update your OS SKU to a supported OS option before upgrading your Kubernetes version to 1.39+.
`--os-sku Ubuntu2404`

is an option and is intended for testing the new OS Linux version without requiring you to upgrade your Kubernetes version. - You need the preview Azure CLI version 18.0.0b5 or later for
*preview*and version 2.82.0 for*GA*installed and configured. To find your CLI version, run`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Update to `--os-sku Ubuntu2404`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku Ubuntu2404 \
--kubernetes-version 1.32.0 \
--name $NODE_POOL_NAME \
--node-count 1
```


#### Migrate to Azure Linux 3.0

Azure Linux 3.0 is the default for `--os-sku AzureLinux`

in Kubernetes versions 1.32 to 1.36. You can also use Azure Linux 3.0 by specifying `--os-sku AzureLinux3`

.

Note

Keep the following information in mind when migrating to `--os-sku AzureLinux3`

:

`--os-sku AzureLinux3`

is supported in Kubernetes versions 1.28 to 1.36.`--os-sku AzureLinux3`

is intended for migrating to Azure Linux 3.0 without upgrading your Kubernetes version. You need to update your OS SKU to a supported OS option before upgrading your Kubernetes version to 1.37+.- You need the Azure CLI version 18.0.0b36 or later for
*preview*and version 2.78.0 or later for*GA*installed and configured. To find your CLI version, run`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Update to `--os-sku AzureLinux3`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku AzureLinux3 \
--kubernetes-version 1.30.0 \
--name $NODE_POOL_NAME \
--node-count 1
```


## Roll back your OS version

In Kubernetes versions where multiple OS versions are supported, you can use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command to roll back to a previous OS version.

You might want to roll back your OS version in the following scenarios:

- If you're testing a new OS version and you run into any issues.
- Once you upgrade to a Kubernetes version that supports the new OS version as default, you might want to roll back to the default
`Ubuntu`

or`AzureLinux`

OS SKU. This allows you to get future OS versions as a part of your Kubernetes upgrades instead of requiring a node pool update.

### Roll back your OS version to the default OS SKU

You can use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command to update the

`os-sku`

on an existing node pool. In cases where there's a previous OS version supported in your Kubernetes version, this functionality can allow you to roll back your OS version.Note

The following values aren't supported for node pool update command:

`--os-sku Windows2019`

`--os-sku Windows2022`

`--os-sku Windows2025`


Instead, you need to add node pools to your cluster with the corresponding `--os-sku`

you intend to use.

| OS SKU | Default OS version |
|---|---|
| Ubuntu | When you have OS SKU `Ubuntu` , Ubuntu 22.04 is the default OS version if your Kubernetes version is 1.25 to 1.34. Ubuntu 24.04 is the default for Ubuntu in Kubernetes 1.35 to 1.37. |
| AzureLinux | When you have OS SKU `AzureLinux` , Azure Linux 2.0 is the default for AzureLinux in Kubernetes 1.26 to 1.31. Azure Linux 3.0 is the default for AzureLinux in Kubernetes 1.32 to 1.36. |

#### Update your OS SKU to Ubuntu on an existing node pool

When updating your node pool to use OS SKU `Ubuntu`

, you'll get the default OS version based on your Kubernetes version. This might trigger an automatic reimage if the OS version changes during the node pool update command.

Update to `--os-sku Ubuntu`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku Ubuntu \
--name $NODE_POOL_NAME \
--node-count 1
```


You can use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command to migrate between any supported Linux

`os-sku`

. The command might fail if the target OS doesn't have a supported node image for your Kubernetes version, VM size, or FIPS enablement.#### Update your OS SKU to Azure Linux on an existing node pool

When updating your node pool to use OS SKU `AzureLinux`

, you'll get the default OS version based on your Kubernetes version. This might trigger an automatic reimage if the OS version changes during the node pool update command.

Update to `--os-sku AzureLinux`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku AzureLinux \
--name $NODE_POOL_NAME \
--node-count 1
```


### Roll back to Ubuntu 22.04

Note

Keep the following information in mind when migrating to `--os-sku Ubuntu2204`

:

[FIPS](enable-fips-nodes)and[CVM](use-cvm)aren't supported.- Ubuntu 22.04 is supported in Kubernetes versions 1.25 to 1.35.
`--os-sku Ubuntu2204`

is intended for roll back to Ubuntu 22.04 on your current Kubernetes version. You need to update your OS SKU to a supported OS option to upgrade your Kubernetes version to 1.36 and above.

Roll back to `--os-sku Ubuntu2204`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku Ubuntu2204 \
--kubernetes-version 1.32.0 \
--name $NODE_POOL_NAME \
--node-count 1
```


## Next steps

To learn more about node images, node pool upgrades, and node configurations on AKS, see the following resources:

- To learn about nodes and node configurations, see
[AKS core concepts](core-aks-concepts). - Configure
[automatic node image upgrades](auto-upgrade-node-os-image)and schedule them using[planned maintenance](planned-maintenance). - Apply
[custom node configurations](custom-node-configuration)to modify OS or kubelet settings. - For information about the latest node images, see the
[AKS release notes](https://github.com/Azure/AKS/releases). [Automatically apply cluster and node pool upgrades with GitHub Actions](node-upgrade-github-actions).- Learn about upgrading best practices with
[AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).


---

<!-- DOCUMENTO FUSIONADO: _vertical-pod-autoscaler-api-reference_use-node-auto-provisioning.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: vertical-pod-autoscaler-api-reference.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/vertical-pod-autoscaler-api-reference -->

# Vertical Pod Autoscaler API reference

This article provides the API reference for the Vertical Pod Autoscaler feature of Azure Kubernetes Service.

This reference is based on version 0.13.0 of the AKS implementation of VPA.

## VerticalPodAutoscaler

| Name |
Object |
Description |
| metadata |
ObjectMeta |
Standard [object metadata](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md#metadata). |
| spec |
VerticalPodAutoscalerSpec |
The desired behavior of the Vertical Pod Autoscaler. |
| status |
VerticalPodAutoscalerStatus |
The most recently observed status of the Vertical Pod Autoscaler. |

## VerticalPodAutoscalerSpec

| Name |
Object |
Description |
| targetRef |
CrossVersionObjectReference |
Reference to the controller managing the set of pods for the autoscaler to control. For example, a Deployment or a StatefulSet. You can point a Vertical Pod Autoscaler at any controller that has a [Scale](https://v1-25.docs.kubernetes.io/docs/reference/generated/kubernetes-api/v1.25/#scalespec-v1-autoscaling) subresource. Typically, the Vertical Pod Autoscaler retrieves the pod set from the controller's ScaleStatus. |
| updatePolicy |
PodUpdatePolicy |
Specifies whether recommended updates are applied when a pod is started and whether recommended updates are applied during the life of a pod. |
| resourcePolicy |
PodResourcePolicy |
Specifies policies for how CPU and memory requests are adjusted for individual containers. The resource policy can be used to set constraints on the recommendations for individual containers. If not specified, the autoscaler computes recommended resources for all containers in the pod, without additional constraints. |
| recommenders |
VerticalPodAutoscalerRecommenderSelector |
Recommender is responsible for generating recommendation for the VPA object. Leave empty to use the default recommender. Otherwise the list can contain exactly one entry for a user-provided alternative recommender. |

## VerticalPodAutoscalerList

| Name |
Object |
Description |
| metadata |
ObjectMeta |
Standard [object metadata](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md#metadata). |
| items |
VerticalPodAutoscaler (array) |
A list of Vertical Pod Autoscaler objects. |

## PodUpdatePolicy

| Name |
Object |
Description |
| updateMode |
string |
A string that specifies whether recommended updates are applied when a pod is started and whether recommended updates are applied during the life of a pod. Possible values are `Off` , `Initial` , `Recreate` , and `Auto` . The default is `Auto` if you don't specify a value. |
| minReplicas |
int32 |
A value representing the minimal number of replicas which need to be alive for Updater to attempt pod eviction (pending other checks like Pod Disruption Budget). Only positive values are allowed. Defaults to global `--min-replicas` flag, which is set to `2` . |

## PodResourcePolicy

| Name |
Object |
Description |
| conainerPolicies |
ContainerResourcePolicy |
An array of resource policies for individual containers. There can be at most one entry for every named container, and optionally a single wildcard entry with `containerName = '*'` , which handles all containers that do not have individual policies. |

## ContainerResourcePolicy

| Name |
Object |
Description |
| containerName |
string |
A string that specifies the name of the container that the policy applies to. If not specified, the policy serves as the default policy. |
| mode |
ContainerScalingMode |
Specifies whether recommended updates are applied to the container when it is started and whether recommended updates are applied during the life of the container. Possible values are `Off` and `Auto` . The default is `Auto` if you don't specify a value. |
| minAllowed |
ResourceList |
Specifies the minimum CPU request and memory request allowed for the container. By default, there is no minimum applied. |
| maxAllowed |
ResourceList |
Specifies the maximum CPU request and memory request allowed for the container. By default, there is no maximum applied. |
| ControlledResources |
[]ResourceName |
Specifies the type of recommendations that are computed (and possibly applied) by the Vertical Pod Autoscaler. If empty, the default of [ResourceCPU, ResourceMemory] is used. |

## VerticalPodAutoscalerRecommenderSelector

| Name |
Object |
Description |
| name |
string |
A string that specifies the name of the recommender responsible for generating recommendation for this object. |

## VerticalPodAutoscalerStatus

| Name |
Object |
Description |
| recommendation |
RecommendedPodResources |
The most recently recommended CPU and memory requests. |
| conditions |
VerticalPodAutoscalerCondition |
An array that describes the current state of the Vertical Pod Autoscaler. |

## RecommendedPodResources

| Name |
Object |
Description |
| containerRecommendation |
RecommendedContainerResources |
An array of resources recommendations for individual containers. |

## RecommendedContainerResources

| Name |
Object |
Description |
| containerName |
string |
A string that specifies the name of the container that the recommendation applies to. |
| target |
ResourceList |
The recommended CPU request and memory request for the container. |
| lowerBound |
ResourceList |
The minimum recommended CPU request and memory request for the container. This amount is not guaranteed to be sufficient for the application to be stable. Running with smaller CPU and memory requests is likely to have a significant impact on performance or availability. |
| upperBound |
ResourceList |
The maximum recommended CPU request and memory request for the container. CPU and memory requests higher than these values are likely to be wasted. |
| uncappedTarget |
ResourceList |
The most recent resource recommendation computed by the autoscaler, based on actual resource usage, not taking into account the **Container Resource Policy**. If actual resource usage causes the target to violate the **Container Resource Policy**, this might be different from the bounded recommendation. This field does not affect actual resource assignment. It is used only as a status indication. |

## VerticalPodAutoscalerCondition

| Name |
Object |
Description |
| type |
VerticalPodAutoscalerConditionType |
The type of condition being described. Possible values are `RecommendationProvided` , `LowConfidence` , `NoPodsMatched` , and `FetchingHistory` . |
| status |
ConditionStatus |
The status of the condition. Possible values are `True` , `False` , and `Unknown` . |
| lastTransitionTime |
Time |
The last time the condition made a transition from one status to another. |
| reason |
string |
The reason for the last transition from one status to another. |
| message |
string |
A human-readable string that gives details about the last transition from one status to another. |

## Next steps

See [Vertical Pod Autoscaler](vertical-pod-autoscaler) to understand how to improve cluster resource utilization and free up CPU and memory for other pods.


---

<!-- DOCUMENTO FUSIONADO: use-node-auto-provisioning.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-node-auto-provisioning -->

# Enable or disable node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to enable or disable node auto-provisioning (NAP) in Azure Kubernetes Service (AKS) using the Azure CLI or Azure Resource Manager (ARM) templates.

If you want to create a NAP-enabled AKS cluster with a custom virtual network (VNet) and subnets, see [Create a node auto-provisioning (NAP) cluster in a custom virtual network](node-auto-provisioning-custom-vnet).

## Before you begin

Before you begin, review the [Overview of node auto-provisioning (NAP) in AKS](node-auto-provisioning) article, which details [how NAP works](node-auto-provisioning#how-does-node-auto-provisioning-work), [prerequisites](node-auto-provisioning#prerequisites) and [limitations](node-auto-provisioning#limitations-and-unsupported-features).

## Enable node auto-provisioning (NAP) on an AKS cluster

The following sections explain how to enable NAP on a new or existing AKS cluster:

Note

You can enable [control plane metrics](monitor-control-plane-metrics) to see the logs and operations from [node auto-provisioning](control-plane-metrics-default-list#minimal-ingestion-for-default-off-targets) with the [Azure Monitor managed service for Prometheus add-on](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview).

### Enable NAP on a new cluster

Enable node auto-provisioning on a new cluster using the

command with the`az aks create`

`--node-provisioning-mode`

flag set to`Auto`

. The following command also sets the`--network-plugin`

to`azure`

,`--network-plugin-mode`

to`overlay`

, and`--network-dataplane`

to`cilium`

.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --node-provisioning-mode Auto \ --network-plugin azure \ --network-plugin-mode overlay \ --network-dataplane cilium \ --generate-ssh-keys`


Create a file named

`nap.json`

and add the following ARM template configuration with the`properties.nodeProvisioningProfile.mode`

field set to`Auto`

, which enables NAP. (The default setting is`Manual`

.)`{ "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#", "contentVersion": "1.0.0.0", "metadata": {}, "parameters": {}, "resources": [ { "type": "Microsoft.ContainerService/managedClusters", "apiVersion": "2025-05-01", "sku": { "name": "Base", "tier": "Standard" }, "name": "napcluster", "location": "uksouth", "identity": { "type": "SystemAssigned" }, "properties": { "networkProfile": { "networkPlugin": "azure", "networkPluginMode": "overlay", "networkPolicy": "cilium", "networkDataplane":"cilium", "loadBalancerSku": "Standard" }, "dnsPrefix": "napcluster", "agentPoolProfiles": [ { "name": "agentpool", "count": 3, "vmSize": "standard_d2s_v3", "osType": "Linux", "mode": "System" } ], "nodeProvisioningProfile": { "mode": "Auto" } } } ] }`

Enable node auto-provisioning on a new cluster using the

command with the`az deployment group create`

`--template-file`

flag set to the path of the ARM template file.`az deployment group create --resource-group $RESOURCE_GROUP --template-file ./nap.json`


### Enable NAP on an existing cluster

Enable node auto-provisioning on an existing cluster using the

command with the`az aks update`

`--node-provisioning-mode`

flag set to`Auto`

.`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --node-provisioning-mode Auto`


## Disable node auto-provisioning (NAP) on an AKS cluster

Important

You can only disable NAP on a cluster if the following conditions are met:

- There are no existing NAP nodes. You can use the
`kubectl get nodes -l karpenter.sh/nodepool`

command to check for existing NAP-managed nodes. - All existing Karpenter
have their`NodePools`

`spec.limits.cpu`

field set to`0`

. This action prevents new nodes from being created, but doesn't disrupt currently running nodes.

Set the

`spec.limits.cpu`

field to`0`

for every existing Karpenter`NodePool`

. For example:`apiVersion: karpenter.sh/v1 kind: NodePool metadata: name: default spec: limits: cpu: 0`

Important

If you don't want to ensure that every pod previously running on a NAP node is safely migrated to a non-NAP node before disabling NAP, you can skip steps 2 and 3 and instead use the

`kubectl delete node`

command for each NAP-managed node. However,**we don't recommend skipping these steps**, as it might leave some pods pending and doesn't honor Pod Disruption Budgets (PDBs).When using the

`kubectl delete node`

command, be careful to only delete NAP-managed nodes. You can identify NAP-managed nodes using the`kubectl get nodes -l karpenter.sh/nodepool`

command.Add the

`karpenter.azure.com/disable:NoSchedule`

taint to every Karpenter`NodePool`

. For example:`apiVersion: karpenter.sh/v1 kind: NodePool metadata: name: default spec: template: spec: ... taints: - key: karpenter.azure.com/disable effect: NoSchedule`

This action starts the process of migrating the workloads on the NAP-managed nodes to non-NAP nodes, honoring PDBs and disruption limits. Pods migrate to non-NAP nodes if they can fit. If there isn't enough fixed-size capacity, some node NAP-managed nodes remain.

Scale up existing fixed-size

`ManagedCluster`

`AgentPools`

or create new fixed-size`AgentPools`

to take the load from the node NAP-managed nodes. As these nodes are added to the cluster, the node NAP-managed nodes are drained, and work is migrated to the fixed-size nodes.Delete all NAP-managed nodes using the

`kubectl get nodes -l karpenter.sh/nodepool`

command. If NAP-managed nodes still exist, the cluster likely lacks fixed-size capacity. In this case, you should add more nodes so the remaining workloads can be migrated.

Update the NAP mode to

`Manual`

using theAzure CLI command with the`az aks update`

`--node-provisioning-mode`

flag set to`Manual`

.`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --node-provisioning-mode Manual`


Update the

`properties.nodeProvisioningProfile.mode`

field to`Manual`

in your ARM template and redeploy it.`{ "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#", "contentVersion": "1.0.0.0", "metadata": {}, "parameters": {}, "resources": [ { "type": "Microsoft.ContainerService/managedClusters", "apiVersion": "2025-05-01", "sku": { "name": "Base", "tier": "Standard" }, "name": "napcluster", "location": "uksouth", "identity": { "type": "SystemAssigned" }, "properties": { "networkProfile": { "networkPlugin": "azure", "networkPluginMode": "overlay", "networkPolicy": "cilium", "networkDataplane":"cilium", "loadBalancerSku": "Standard" }, "dnsPrefix": "napcluster", "agentPoolProfiles": [ { "name": "agentpool", "count": 3, "vmSize": "standard_d2s_v3", "osType": "Linux", "mode": "System" } ], "nodeProvisioningProfile": { "mode": "Manual" } } } ] }`


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: _concepts-security_cluster-autoscaler.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: concepts-security.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-security -->

# Security concepts for applications and clusters in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Container security protects the entire end-to-end pipeline from build to the application workloads running in Azure Kubernetes Service (AKS).

The Secure Supply Chain includes the build environment and registry.

Kubernetes includes security components, such as *pod security standards* and *Secrets*. Azure includes components like Active Directory, Microsoft Defender for Containers, Azure Policy, Azure Key Vault, network security groups, and orchestrated cluster upgrades. AKS combines these security components to:

- Provide a complete authentication and authorization story.
- Apply AKS Built-in Azure Policy to secure your applications.
- End-to-End insight from build through your application with Microsoft Defender for Containers.
- Keep your AKS cluster running the latest OS security updates and Kubernetes releases.
- Provide secure pod traffic and access to sensitive credentials.

This article introduces the core concepts that secure your applications in AKS.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Build Security

As the entry point for the Supply Chain, it's important to conduct static analysis of image builds before they're promoted down the pipeline. This includes vulnerability and compliance assessment. It's not about failing a build because it has a vulnerability, as that breaks development. It's about looking at the **Vendor Status** to segment based on vulnerabilities that are actionable by the development teams. Also use **Grace Periods** to allow developers time to remediate identified issues.

## Registry Security

Assessing the vulnerability state of the image in the Registry detects drift and also catches images that didn't come from your build environment. Use [Notary V2](https://github.com/notaryproject/notaryproject) to attach signatures to your images to ensure deployments are coming from a trusted location.

## Cluster security

In AKS, the Kubernetes master components are part of the managed service provided, managed, and maintained by Microsoft. Each AKS cluster has its own single-tenanted, dedicated Kubernetes master to provide the API Server, Scheduler, etc. For more information, see [Vulnerability management for Azure Kubernetes Service](concepts-vulnerability-management).

By default, the Kubernetes API server uses a public IP address and a fully qualified domain name (FQDN). You can limit access to the API server endpoint using [authorized IP ranges](api-server-authorized-ip-ranges). You can also create a fully [private cluster](private-clusters) to limit API server access to your virtual network.

You can control access to the API server using Kubernetes role-based access control (Kubernetes RBAC) and Azure RBAC. For more information, see [Microsoft Entra integration with AKS](managed-azure-ad).

## Node security

AKS nodes are Azure virtual machines (VMs) that you manage and maintain.

- Linux nodes run optimized versions of Ubuntu or Azure Linux.
- Windows Server nodes run an optimized Windows Server release using the
`containerd`

container runtime.

When an AKS cluster is created or scaled up, the nodes are automatically deployed with the latest OS security updates and configurations.

Note

AKS clusters running:

- Kubernetes version 1.19 and higher - Linux node pools use
`containerd`

as its container runtime. Windows Server 2019 and Windows Server 2022 node pools use`containerd`

as its container runtime. For more information, see[Add a Windows Server node pool with](create-node-pools).`containerd`

- Kubernetes version 1.19 and earlier - Linux node pools use Docker as its container runtime.

For more information about the security upgrade process for Linux and Windows worker nodes, see [Security patching nodes](concepts-vulnerability-management#worker-nodes).

AKS clusters running Azure Generation 2 VMs include support for [Trusted Launch](use-trusted-launch). This feature protects against advanced and persistent attack techniques by combining technologies that you can enable independently, like secure boot and a virtualized version of the trusted platform module (vTPM). Administrators can deploy AKS worker nodes with verified and signed bootloaders, OS kernels, and drivers to ensure integrity of the entire boot chain of the underlying VM.

### Container and security optimized OS options

AKS released support for two new optimized Linux OS options. [Azure Linux OS Guard (preview)](https://aka.ms/aks/azure-linux-os-guard) is Microsoft-created and optimized for Azure. OS Guard is built on top of Azure Linux with specialized configuration to support containerized workloads with security optimizations. [Flatcar Container Linux for AKS (preview)](https://aka.ms/aks/flatcar) is a CNCF-based vendor-neutral container-optimized immutable OS, best suited for running on multicloud and on-premises environments. These OS options provide increased security when compared to other Linux OS options, such as:

- Both Azure Linux OS Guard and Flatcar Container Linux for AKS have an immutable operating system that you can't modify at runtime. All OS binaries, libraries and static configuration are read-only, and the bit-for-bit integrity is often cryptographically protected. These special purpose operating systems ship as self-contained images and come without any kind of package management or other traditional means of altering the OS. User workloads run in isolated environments like containers, sandboxed from the OS.
- Both Azure Linux OS Guard and Flatcar Container Linux for AKS use SELinux for Mandatory Access Control.
- Azure Linux OS Guard enforces
[FIPS](enable-fips-nodes)and[Trusted Launch](use-trusted-launch)enablement, providing improved compliance and protection against advanced and persistent attacks by combining secure boot and virtualized version of trusted platform module (vTPM).

When deciding between which container-optimized OS options to use, AKS recommends the following:

- Use
if you're looking for a vendor neutral immutable OS with cross-cloud support.**Flatcar Container Linux for AKS (preview)** - Use
if you're looking for an enterprise-ready immutable OS, recommended by Microsoft.**Azure Linux OS Guard (preview)** - Use
[Ubuntu](https://aka.ms/aks/supported-ubuntu-versions)if you're looking for a vendor neutral, general purpose OS with cross-cloud support. - Use
[Azure Linux](https://aka.ms/aks/use-azure-linux)if you're looking for an enterprise-ready, general purpose OS, recommended by Microsoft.


### Node authorization

Node authorization is a special-purpose authorization mode that specifically authorizes kubelet API requests to protect against East-West attacks. Node authorization is enabled by default on AKS 1.24 + clusters.

### Node deployment

Nodes are deployed onto a private virtual network subnet, with no public IP addresses assigned. For troubleshooting and management purposes, SSH is enabled by default and only accessible using the internal IP address. Disabling SSH during cluster and node pool creation, or for an existing cluster or node pool, is in preview. See [Manage SSH access](manage-ssh-node-access) for more information.

### Node storage

To provide storage, the nodes use Azure Managed Disks. For most VM node sizes, Azure Managed Disks are Premium disks backed by high-performance SSDs. The data stored on managed disks is automatically encrypted at rest within the Azure platform. To improve redundancy, Azure Managed Disks are securely replicated within the Azure datacenter.

### Hostile multitenant workloads

Currently, Kubernetes environments aren't safe for hostile multitenant usage. Extra security features, like *Pod Security Policies* or Kubernetes RBAC for nodes, efficiently block exploits. For true security when running hostile multitenant workloads, only trust a hypervisor. The security domain for Kubernetes becomes the entire cluster, not an individual node.

For these types of hostile multitenant workloads, you should use physically isolated clusters. For more information on ways to isolate workloads, see [Best practices for cluster isolation in AKS](operator-best-practices-cluster-isolation).

### Compute isolation

Because of compliance or regulatory requirements, certain workloads may require a high degree of isolation from other customer workloads. For these workloads, Azure provides:

[Kernel isolated containers](/en-us/azure/confidential-computing/confidential-containers)to use as the agent nodes in an AKS cluster. These containers are completely isolated to a specific hardware type and isolated from the Azure Host fabric, the host operating system, and the hypervisor. They're dedicated to a single customer. Select[one of the isolated VMs sizes](/en-us/azure/virtual-machines/isolation)as the**node size**when creating an AKS cluster or adding a node pool.[Confidential Containers](confidential-containers-overview)(preview), also based on Kata Confidential Containers, encrypts container memory and prevents data in memory during computation from being in clear text, readable format, and tampering. It helps isolate your containers from other container groups/pods, and VM node OS kernel. Confidential Containers (preview) uses hardware based memory encryption (SEV-SNP).[Pod Sandboxing](use-pod-sandboxing)(preview) provides an isolation boundary between the container application and the shared kernel and compute resources (CPU, memory, and network) of the container host.

## Network security

For connectivity and security with on-premises networks, you can deploy your AKS cluster into existing Azure virtual network subnets. These virtual networks connect back to your on-premises network using Azure Site-to-Site VPN or Express Route. Define Kubernetes ingress controllers with private, internal IP addresses to limit services access to the internal network connection.

### Azure network security groups

To filter virtual network traffic flow, Azure uses network security group rules. These rules define the source and destination IP ranges, ports, and protocols allowed or denied access to resources. Default rules are created to allow TLS traffic to the Kubernetes API server. You create services with load balancers, port mappings, or ingress routes. AKS automatically modifies the network security group for traffic flow.

If you provide your own subnet for your AKS cluster (whether using Azure CNI or Kubenet), **do not** modify the NIC-level network security group managed by AKS. Instead, create more subnet-level network security groups to modify the flow of traffic. Make sure they don't interfere with necessary traffic managing the cluster, such as load balancer access, communication with the control plane, or [egress](limit-egress-traffic).

### Kubernetes network policy

To limit network traffic between pods in your cluster, AKS offers support for [Kubernetes network policies](use-network-policies). With network policies, you can allow or deny specific network paths within the cluster based on namespaces and label selectors.

## Application Security

To protect pods running on AKS, consider [Microsoft Defender for Containers](/en-us/azure/defender-for-cloud/defender-for-containers-introduction) to detect and restrict cyber attacks against your applications running in your pods. Run continual scanning to detect drift in the vulnerability state of your application and implement a "blue/green/canary" process to patch and replace the vulnerable images.

## Secure container access to resources

In the same way that you should grant users or groups the minimum privileges required, you should also limit containers to only necessary actions and processes. To minimize the risk of attack, avoid configuring applications and containers that require escalated privileges or root access. Built-in Linux security features such as *AppArmor* and *seccomp* are recommended as [best practices](/en-us/azure/aks/operator-best-practices-cluster-security) to [secure container access to resources][secure-container-access].

## Kubernetes Secrets

With a Kubernetes *Secret*, you inject sensitive data into pods, such as access credentials or keys.

- Create a Secret using the Kubernetes API.
- Define your pod or deployment and request a specific Secret.
- Secrets are only provided to nodes with a scheduled pod that requires them.
- The Secret is stored in
*tmpfs*, not written to disk.

- When you delete the last pod on a node requiring a Secret, the Secret is deleted from the node's
*tmpfs*.- Secrets are stored within a given namespace and are only accessible from pods within the same namespace.


Using Secrets reduces the sensitive information defined in the pod or service YAML manifest. Instead, you request the Secret stored in Kubernetes API Server as part of your YAML manifest. This approach only provides the specific pod access to the Secret.

Note

The raw secret manifest files contain the secret data in base64 format. For more information, see the [official documentation](https://kubernetes.io/docs/concepts/configuration/secret/#risks). Treat these files as sensitive information, and never commit them to source control.

Kubernetes secrets are stored in *etcd*, a distributed key-value store. AKS allows [encryption at rest of secrets in etcd using customer managed keys](use-kms-etcd-encryption).

## Next steps

To get started with securing your AKS clusters, see [Upgrade an AKS cluster](upgrade-cluster).

For associated best practices, see [Best practices for cluster security and upgrades in AKS](operator-best-practices-cluster-security) and [Best practices for pod security in AKS](developer-best-practices-pod-security).

For more information on core Kubernetes and AKS concepts, see:


---

<!-- DOCUMENTO FUSIONADO: cluster-autoscaler.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/cluster-autoscaler -->

# Use the cluster autoscaler in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To keep up with application demands in AKS, you might need to adjust the number of nodes that run your workloads. The cluster autoscaler component watches for pods in your cluster that can't be scheduled because of resource constraints. When the cluster autoscaler detects issues, it scales up the number of nodes in the node pool to meet the application demands. It also regularly checks nodes for a lack of running pods and scales down the number of nodes as needed.

This article shows you how to enable and manage the cluster autoscaler in AKS, which is based on the [open-source Kubernetes version](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler).

## Before you begin

This article requires Azure CLI version 2.0.76 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Use the cluster autoscaler on an AKS cluster

Important

The cluster autoscaler is a Kubernetes component. Although the AKS cluster uses a virtual machine scale set for the nodes, don't manually enable or edit settings for scale set autoscaling. Let the Kubernetes cluster autoscaler manage the required scale settings. For more information, see [Can I modify the AKS resources in the node resource group?](faq)

### Enable the cluster autoscaler on a new cluster

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

Create an AKS cluster using the

command and enable and configure the cluster autoscaler on the node pool for the cluster using the`az aks create`

`--enable-cluster-autoscaler`

parameter and specifying a node`--min-count`

and`--max-count`

. The following example command creates a cluster with a single node backed by a virtual machine scale set, enables the cluster autoscaler, sets a minimum of one and maximum of three nodes:`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 1 \ --vm-set-type VirtualMachineScaleSets \ --load-balancer-sku standard \ --enable-cluster-autoscaler \ --min-count 1 \ --max-count 3 \ --generate-ssh-keys`

It takes a few minutes to create the cluster and configure the cluster autoscaler settings.


### Enable the cluster autoscaler on an existing cluster

Update an existing cluster using the

command and enable and configure the cluster autoscaler on the node pool using the`az aks update`

`--enable-cluster-autoscaler`

parameter and specifying a node`--min-count`

and`--max-count`

. The following example command updates an existing AKS cluster to enable the cluster autoscaler on the node pool for the cluster and sets a minimum of one and maximum of three nodes:`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --enable-cluster-autoscaler \ --min-count 1 \ --max-count 3`

It takes a few minutes to update the cluster and configure the cluster autoscaler settings.


### Disable the cluster autoscaler on a cluster

Disable the cluster autoscaler using the

command and the`az aks update`

`--disable-cluster-autoscaler`

parameter.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --disable-cluster-autoscaler`

Nodes aren't removed when the cluster autoscaler is disabled.


Note

You can manually scale your cluster after disabling the cluster autoscaler using the [ az aks scale](/en-us/cli/azure/aks#az-aks-scale) command. If you use the horizontal pod autoscaler, it continues to run with the cluster autoscaler disabled, but pods might end up unable to be scheduled if all node resources are in use.

### Re-enable the cluster autoscaler on a cluster

You can re-enable the cluster autoscaler on an existing cluster using the [ az aks update](https://github.com/Azure/azure-cli-extensions/tree/master/src/aks-preview) command and specifying the

`--enable-cluster-autoscaler`

, `--min-count`

, and `--max-count`

parameters.## Use the cluster autoscaler on node pools

### Use the cluster autoscaler on multiple node pools

You can use the cluster autoscaler with [multiple node pools](create-node-pools) and can enable the cluster autoscaler on each individual node pool and pass unique autoscaling rules to them.

Update the settings on an existing node pool using the

command.`az aks nodepool update`

`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name nodepool1 \ --update-cluster-autoscaler \ --min-count 1 \ --max-count 5`


### Disable the cluster autoscaler on a node pool

Disable the cluster autoscaler on a node pool using the

command and the`az aks nodepool update`

`--disable-cluster-autoscaler`

parameter.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name nodepool1 \ --disable-cluster-autoscaler`


### Re-enable the cluster autoscaler on a node pool

You can re-enable the cluster autoscaler on a node pool using the [ az aks nodepool update](https://github.com/Azure/azure-cli-extensions/tree/master/src/aks-preview#enable-cluster-auto-scaler-for-a-node-pool) command and specifying the

`--enable-cluster-autoscaler`

, `--min-count`

, and `--max-count`

parameters.Note

If you plan on using the cluster autoscaler with node pools that span multiple zones and leverage scheduling features related to zones, such as volume topological scheduling, we recommend you have one node pool per zone and enable `--balance-similar-node-groups`

through the autoscaler profile. This ensures the autoscaler can successfully scale up and keep the sizes of the node pools balanced.

## Update the cluster autoscaler settings

As your application demands change, you might need to adjust the cluster autoscaler node count to scale efficiently.

Change the node count using the

command and update the cluster autoscaler using the`az aks update`

`--update-cluster-autoscaler`

parameter and specifying your updated node`--min-count`

and`--max-count`

.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --update-cluster-autoscaler \ --min-count 1 \ --max-count 5`


Note

The cluster autoscaler enforces the minimum count in cases where the actual count drops below the minimum due to external factors, such as during a spot eviction or when changing the minimum count value from the AKS API.

## Use the cluster autoscaler profile

You can configure more granular details of the cluster autoscaler by changing the default values in the cluster-wide autoscaler profile. For example, a scale down event happens after nodes are under-utilized after 10 minutes. If you have workloads that run every 15 minutes, you might want to change the autoscaler profile to scale down under-utilized nodes after 15 or 20 minutes. When you enable the cluster autoscaler, a default profile is used unless you specify different settings.

Important

The cluster autoscaler profile affects **all node pools** that use the cluster autoscaler. You can't set an autoscaler profile per node pool. When you set the profile, any existing node pools with the cluster autoscaler enabled immediately start using the profile.

### Cluster autoscaler profile settings

The following table lists the available settings for the cluster autoscaler profile:

| Setting | Description | Default value |
|---|---|---|
`scan-interval` |
How often the cluster is reevaluated for scale up or down. | 10 seconds |
`scale-down-delay-after-add` |
How long after scale up that scale down evaluation resumes. | 10 minutes |
`scale-down-delay-after-delete` |
How long after node deletion that scale down evaluation resumes. | `scan-interval` |
`scale-down-delay-after-failure` |
How long after scale down failure that scale down evaluation resumes. | Three minutes |
`scale-down-unneeded-time` |
How long a node should be unneeded before it's eligible for scale down. | 10 minutes |
`scale-down-unready-time` |
How long an unready node should be unneeded before it's eligible for scale down. | 20 minutes |
`ignore-daemonsets-utilization` |
Whether DaemonSet pods will be ignored when calculating resource utilization for scale down. | `false` |
`daemonset-eviction-for-empty-nodes` |
Whether DaemonSet pods will be gracefully terminated from empty nodes. | `false` |
`daemonset-eviction-for-occupied-nodes` |
Whether DaemonSet pods will be gracefully terminated from non-empty nodes. | `true` |
`scale-down-utilization-threshold` |
The maximum value between the sum of CPU requests and sum of Memory requests of all pods running on the node divided by node's corresponding allocatable resource, below which a node can be considered for scale down. | 0.5 |
`max-graceful-termination-sec` |
Maximum number of seconds the cluster autoscaler waits for pod termination when trying to scale down a node. | 600 seconds |
`balance-similar-node-groups` |
Detects similar node pools and balances the number of nodes between them. | `false` |
`expander` |
Type of node pool
`most-pods` , `random` , `least-waste` , and `priority` . |

`random`

`skip-nodes-with-local-storage`

`true`

, cluster autoscaler doesn't delete nodes with pods with local storage, for example, EmptyDir or HostPath.`false`

`skip-nodes-with-system-pods`

`true`

, cluster autoscaler doesn't delete nodes with pods from kube-system (except for DaemonSet or mirror pods).`true`

`max-empty-bulk-delete`

`new-pod-scale-up-delay`

`max-total-unready-percentage`

`max-node-provision-time`

`ok-total-unready-count`

Note

The ignore-daemonsets-utilization, daemonset-eviction-for-empty-nodes, and daemonset-eviction-for-occupied-nodes parameters are GA from API version 2024-05-01. If you are using the CLI to update these flags, please ensure you are using version 2.63 or later.

### Set the cluster autoscaler profile on a new cluster

Create an AKS cluster using the

command and set the cluster autoscaler profile using the`az aks create`

`cluster-autoscaler-profile`

parameter.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 1 \ --enable-cluster-autoscaler \ --min-count 1 \ --max-count 3 \ --cluster-autoscaler-profile scan-interval=30s \ --generate-ssh-keys`


### Set the cluster autoscaler profile on an existing cluster

Set the cluster autoscaler on an existing cluster using the

command and the`az aks update`

`cluster-autoscaler-profile`

parameter. The following example configures the scan interval setting as*30s*:`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --cluster-autoscaler-profile scan-interval=30s`


### Configure cluster autoscaler profile for aggressive scale down

Note

Scaling down aggressively is not recommended for clusters experiencing frequent scale-outs and scale-ins within short intervals, as it could potentially result in extended node provisioning times under these circumstances. Increasing `scale-down-delay-after-add`

can help in these circumstances by keeping the node around longer to handle incoming workloads.

```
az aks update \
--resource-group myResourceGroup \
--name myAKSCluster \
--cluster-autoscaler-profile scan-interval=30s,scale-down-delay-after-add=0m,scale-down-delay-after-failure=1m,scale-down-unneeded-time=3m,scale-down-unready-time=3m,max-graceful-termination-sec=30,skip-nodes-with-local-storage=false,max-empty-bulk-delete=1000,max-total-unready-percentage=100,ok-total-unready-count=1000,max-node-provision-time=15m
```


### Configure cluster autoscaler profile for bursty workloads

```
az aks update \
--resource-group "myResourceGroup" \
--name myAKSCluster \
--cluster-autoscaler-profile scan-interval=20s,scale-down-delay-after-add=10m,scale-down-delay-after-failure=1m,scale-down-unneeded-time=5m,scale-down-unready-time=5m,max-graceful-termination-sec=30,skip-nodes-with-local-storage=false,max-empty-bulk-delete=100,max-total-unready-percentage=100,ok-total-unready-count=1000,max-node-provision-time=15m
```


### Reset cluster autoscaler profile to default values

Reset the cluster autoscaler profile using the

command.`az aks update`

`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --cluster-autoscaler-profile ""`


## Retrieve cluster autoscaler logs and status

You can retrieve logs and status updates from the cluster autoscaler to help diagnose and debug autoscaler events. AKS manages the cluster autoscaler on your behalf and runs it in the managed control plane. You can enable control plane node to see the logs and operations from the cluster autoscaler.

Set up a rule for resource logs to push cluster autoscaler logs to Log Analytics using the

[instructions here](monitor-aks#aks-control-plane-resource-logs). Make sure you check the box for`cluster-autoscaler`

when selecting options for**Logs**.Select the

**Log**section on your cluster.Enter the following example query into Log Analytics:

`AzureDiagnostics | where Category == "cluster-autoscaler"`

View cluster autoscaler scale-up not triggered events on CLI.

`kubectl get events --field-selector source=cluster-autoscaler,reason=NotTriggerScaleUp`

View cluster autoscaler warning events on CLI.

`kubectl get events --field-selector source=cluster-autoscaler,type=Warning`

The cluster autoscaler also writes out the health status to a

`configmap`

named`cluster-autoscaler-status`

. You can retrieve these logs using the following`kubectl`

command:`kubectl get configmap -n kube-system cluster-autoscaler-status -o yaml`


For more information, see the [Kubernetes/autoscaler GitHub project FAQ](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#ca-doesnt-work-but-it-used-to-work-yesterday-why).

## Cluster Autoscaler Metrics

You can enable [control plane metrics (Preview)](monitor-control-plane-metrics) to see the logs and operations from the [cluster autoscaler](control-plane-metrics-default-list#minimal-ingestion-for-default-off-targets) with the [Azure Monitor managed service for Prometheus add-on](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)

## Next steps

This article showed you how to automatically scale the number of AKS nodes. You can also use the horizontal pod autoscaler to automatically adjust the number of pods that run your application. For steps on using the horizontal pod autoscaler, see [Scale applications in AKS](tutorial-kubernetes-scale).

To further help improve cluster resource utilization and free up CPU and memory for other pods, see [Vertical Pod Autoscaler](vertical-pod-autoscaler).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/vertical-pod-autoscaler -->

# Vertical pod autoscaling in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of using the Vertical Pod Autoscaler (VPA) in Azure Kubernetes Service (AKS), which is based on the open source [Kubernetes](https://github.com/kubernetes/autoscaler/tree/master/vertical-pod-autoscaler) version.

When configured, the VPA automatically sets resource requests and limits on containers per workload based on past usage. The VPA frees up CPU and Memory for other pods and helps ensure effective utilization of your AKS clusters. The Vertical Pod Autoscaler provides recommendations for resource usage over time. To manage sudden increases in resource usage, use the [Horizontal Pod Autoscaler](concepts-scale#horizontal-pod-autoscaler), which scales the number of pod replicas as needed.

## Benefits

The Vertical Pod Autoscaler offers the following benefits:

- Analyzes and adjusts processor and memory resources to
*right size*your applications. VPA isn't only responsible for scaling up, but also for scaling down based on their resource use over time. - A pod with a scaling mode set to
*auto*or*recreate*is evicted if it needs to change its resource requests. - You can set CPU and memory constraints for individual containers by specifying a resource policy.
- Ensures nodes have correct resources for pod scheduling.
- Offers configurable logging of any adjustments made to processor or memory resources made.
- Improves cluster resource utilization and frees up CPU and memory for other pods.

## Limitations and considerations

Consider the following limitations and considerations when using the Vertical Pod Autoscaler:

- VPA supports a maximum of 1,000 pods associated with
`VerticalPodAutoscaler`

objects per cluster. - VPA might recommend more resources than available in the cluster, which prevents the pod from being assigned to a node and run due to insufficient resources. You can overcome this limitation by setting the
*LimitRange*to the maximum available resources per namespace, which ensures pods don't ask for more resources than specified. You can also set maximum allowed resource recommendations per pod in a`VerticalPodAutoscaler`

object. The VPA can't completely overcome an insufficient node resource issue. The limit range is fixed, but the node resource usage is changed dynamically. - We don't recommend using VPA with the
[Horizontal Pod Autoscaler (HPA)](concepts-scale#horizontal-pod-autoscaler), which scales based on the same CPU and memory usage metrics. - The VPA Recommender only stores up to
*eight days*of historical data. - VPA doesn't support JVM-based workloads due to limited visibility into actual memory usage of the workload.
- VPA doesn't support running your own implementation of VPA alongside it. Having an extra or customized recommender is supported.
- AKS Windows containers aren't supported.

## VPA overview

The VPA object consists of three components:

**Recommender**: The Recommender monitors current and past resource consumption, including metric history, Out of Memory (OOM) events, and VPA deployment specs, and uses the information it gathers to provide recommended values for container CPU and Memory requests/limits.**Updater**: The Updater monitors managed pods to ensure that their resource requests are set correctly. If not, it removes those pods so that their controllers can recreate them with the updated requests.**VPA Admission Controller**: The VPA Admission Controller sets the correct resource requests on new pods either created or recreated by their controller based on the Updater's activity.

### VPA admission controller

The VPA Admission Controller is a binary that registers itself as a *Mutating Admission Webhook*. When a new pod is created, the VPA Admission Controller gets a request from the API server and evaluates if there's a matching VPA configuration or finds a corresponding one and uses the current recommendation to set resource requests in the pod.

A standalone job, `overlay-vpa-cert-webhook-check`

, runs outside of the VPA Admission Controller. The `overlay-vpa-cert-webhook-check`

job creates and renews the certificates and registers the VPA Admission Controller as a `MutatingWebhookConfiguration`

.

### VPA object operation modes

A Vertical Pod Autoscaler resource, most commonly a *deployment*, is inserted for each controller that you want to have automatically computed resource requirements.

There are four modes in which the VPA operates:

`Auto`

: VPA assigns resource requests during pod creation and updates existing pods using the preferred update mechanism.`Auto`

, which is equivalent to`Recreate`

, is the default mode. Once restart-free, or*in-place*, updates of pod requests are available, it can be used as the preferred update mechanism by the`Auto`

mode. With the`Auto`

mode, VPA evicts a pod if it needs to change its resource requests. It might cause the pods to be restarted all at once, which can cause application inconsistencies. You can limit restarts and maintain consistency in this situation using a[PodDisruptionBudget](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/).`Recreate`

: VPA assigns resource requests during pod creation and updates existing pods by evicting them when the requested resources differ significantly from the new recommendations (respecting the PodDisruptionBudget, if defined). You should only use this mode if you need to ensure that the pods are restarted whenever the resource request changes. Otherwise, we recommend using`Auto`

mode, which takes advantage of restart-free updates once available.`Initial`

: VPA only assigns resource requests during pod creation. It doesn't update existing pods. This mode is useful for testing and understanding the VPA behavior without affecting the running pods.`Off`

: VPA doesn't automatically change the resource requirements of the pods. The recommendations are calculated and can be inspected in the VPA object.

## Deployment pattern for application development

If you're unfamiliar with VPA, we recommend the following deployment pattern during application development to identify its unique resource utilization characteristics, test VPA to verify it's functioning properly, and test alongside other Kubernetes components to optimize resource utilization of the cluster:

- Set
`UpdateMode = "Off"`

in your production cluster and run VPA in recommendation mode so you can test and gain familiarity with VPA.`UpdateMode = "Off"`

can avoid introducing a misconfiguration that can cause an outage. - Establish observability first by collecting actual resource utilization telemetry over a given period of time, which helps you understand the behavior and any signs of issues from container and pod resources influenced by the workloads running on them.
- Get familiar with the monitoring data to understand the performance characteristics. Based on this insight, set the desired requests/limits accordingly and then in the next deployment or upgrade.
- Set
`updateMode`

value to`Auto`

,`Recreate`

, or`Initial`

depending on your requirements.

## Next steps

To learn how to set up the Vertical Pod Autoscaler on your AKS cluster, see [Use the Vertical Pod Autoscaler in AKS](use-vertical-pod-autoscaler).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/active-passive-solution -->

# Active-passive disaster recovery solution overview for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create an application in Azure Kubernetes Service (AKS) and choose an Azure region during resource creation, it's a single-region app. When the region becomes unavailable during a disaster, your application also becomes unavailable. If you create an identical deployment in a secondary Azure region, your application becomes less susceptible to a single-region disaster, which guarantees business continuity, and any data replication across the regions lets you recover your last application state.

This guide outlines an active-passive disaster recovery solution for AKS. Within this solution, we deploy two independent and identical AKS clusters into two paired Azure regions with only one cluster actively serving traffic.

Note

The following practice has been reviewed internally and vetted in conjunction with our Microsoft partners.

## Active-passive solution overview

In this disaster recovery approach, we have two independent AKS clusters being deployed in two Azure regions. However, only one of the clusters is actively serving traffic at any one time. The secondary cluster (not actively serving traffic) contains the same configuration and application data as the primary cluster but doesn’t accept any traffic unless directed by Azure Front Door traffic manager.

## Scenarios and configurations

This solution is best implemented when hosting applications reliant on resources, such as databases, that actively serve traffic in one region. In scenarios where you need to host stateless applications deployed across both regions, such as horizontal scaling, we recommend considering an [active-active solution](active-active-solution), as active-passive involves added latency.

## Components

The active-passive disaster recovery solution uses many Azure services. This example architecture involves the following components:

**Multiple clusters and regions**: You deploy multiple AKS clusters, each in a separate Azure region. During normal operations, network traffic is routed to the primary AKS cluster set in the Azure Front Door configuration.

**Configured cluster prioritization**: You set a prioritization level between 1-5 for each cluster (with 1 being the highest priority and 5 being the lowest priority). You can set multiple clusters to the same priority level and specify the weight for each cluster. If the primary cluster becomes unavailable, traffic automatically routes to the next region selected in Azure Front Door. All traffic must go through Azure Front Door for this system to work.

**Azure Front Door**: [Azure Front Door](/en-us/azure/frontdoor/front-door-overview) load balances and routes traffic to the [Azure Application Gateway](/en-us/azure/application-gateway/overview) instance in the primary region (cluster must be marked with priority 1). In the event of a region failure, the service redirects traffic to the next cluster in the priority list.

For more information, see [Priority-based traffic-routing](/en-us/azure/frontdoor/routing-methods#priority-based-traffic-routing).

**Hub-spoke pair**: A hub-spoke pair is deployed for each regional AKS instance. [Azure Firewall Manager](/en-us/azure/firewall-manager/overview) policies manage the firewall rules across each region.

**Key Vault**: You provision an [Azure Key Vault](/en-us/azure/key-vault/general/overview) in each region to store secrets and keys.

**Log Analytics**: Regional [Log Analytics](/en-us/azure/azure-monitor/logs/log-analytics-overview) instances store regional networking metrics and diagnostic logs. A shared instance stores metrics and diagnostic logs for all AKS instances.

**Container Registry**: The container images for the workload are stored in a managed container registry. With this solution, a single [Azure Container Registry](/en-us/azure/container-registry/container-registry-intro) instance is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables you to replicate images to the selected Azure regions and provides continued access to images even if a region experiences an outage.

## Failover process

If a service or service component becomes unavailable in one region, traffic should be routed to a region where that service is available. A multi-region architecture includes many different failure points. In this section, we cover the potential failure points.

### Application Pods (Regional)

A Kubernetes deployment object creates multiple replicas of a pod (*ReplicaSet*). If one is unavailable, traffic is routed between the remaining replicas. The Kubernetes *ReplicaSet* attempts to keep the specified number of replicas up and running. If one instance goes down, a new instance should be recreated. [Liveness probes](/en-us/azure/container-instances/container-instances-liveness-probe) can check the state of the application or process running in the pod. If the pod is unresponsive, the liveness probe removes the pod, which forces the *ReplicaSet* to create a new instance.

For more information, see [Kubernetes ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/).

### Application Pods (Global)

When an entire region becomes unavailable, the pods in the cluster are no longer available to serve requests. In this case, the Azure Front Door instance routes all traffic to the remaining health regions. The Kubernetes clusters and pods in these regions continue to serve requests. To compensate for increased traffic and requests to the remaining cluster, keep in mind the following guidance:

- Make sure network and compute resources are right sized to absorb any sudden increase in traffic due to region failover. For example, when using Azure Container Network Interface (CNI), make sure you have a subnet that can support all pod IPs with a spiked traffic load.
- Use the
[Horizontal Pod Autoscaler](concepts-scale#horizontal-pod-autoscaler)to increase the pod replica count to compensate for the increased regional demand. - Use the AKS
[Cluster Autoscaler](cluster-autoscaler)to increase the Kubernetes instance node counts to compensate for the increased regional demand.

### Kubernetes node pools (Regional)

Occasionally, localized failure can occur to compute resources, such as power becoming unavailable in a single rack of Azure servers. To protect your AKS nodes from becoming a single point regional failure, use [Azure Availability Zones](availability-zones). Availability zones ensure that AKS nodes in each availability zone are physically separated from those defined in another availability zones.

### Kubernetes node pools (Global)

In a complete regional failure, Azure Front Door routes traffic to the remaining healthy regions. Again, make sure to compensate for increased traffic and requests to the remaining cluster.

## Failover testing strategy

While there are no mechanisms currently available within AKS to take down an entire region of deployment for testing purposes, [Azure Chaos Studio](/en-us/azure/chaos-studio/chaos-studio-overview) offers the ability to create a chaos experiment on your cluster.

## Next steps

If you're considering a different solution, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/open-service-mesh-deploy-addon-az-cli -->

# Install the Open Service Mesh (OSM) add-on using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to install the Open Service Mesh (OSM) add-on on an Azure Kubernetes Service (AKS) cluster. The OSM add-on installs the OSM mesh on your cluster. The OSM mesh is a service mesh that provides traffic management, policy enforcement, and telemetry collection for your applications. For more information about the OSM mesh, see [Open Service Mesh](https://openservicemesh.io/).

Warning

Microsoft has announced the retirement of the [Open Service Mesh (OSM) add-on for AKS](https://azure.microsoft.com/updates?id=open-service-mesh-add-on-for-aks-will-be-retired-on-september-30-2027). The upstream OSM project has also been retired by the [Cloud Native Computing Foundation (CNCF)](https://docs.openservicemesh.io/). Identify any existing OSM configurations and migrate them to equivalent Istio configurations. For migration steps, see [Migration guidance for Open Service Mesh (OSM) configurations to Istio](open-service-mesh-istio-migration-guidance).

Important

Based on the version of Kubernetes your cluster is running, the OSM add-on installs a different version of OSM.

| Kubernetes version | OSM version installed |
|---|---|
| 1.24.0 or greater | 1.2.5 |
| Between 1.23.5 and 1.24.0 | 1.1.3 |
| Below 1.23.5 | 1.0.0 |

Older versions of OSM may not be available for install or be actively supported if the corresponding AKS version has reached end of life. You can check the [AKS Kubernetes release calendar](supported-kubernetes-versions#aks-kubernetes-release-calendar) for information on AKS version support windows.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). [Azure CLI installed](/en-us/cli/azure/install-azure-cli).

## Install the OSM add-on on your cluster

If you don't have one already, create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

Create a new AKS cluster with the OSM add-on installed using the

command and specify`az aks create`

`open-service-mesh`

for the`--enable-addons`

parameter.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --enable-addons open-service-mesh \ --generate-ssh-keys`


Important

You can't enable the OSM add-on on an existing cluster if an OSM mesh is already on your cluster. Uninstall any existing OSM meshes on your cluster before enabling the OSM add-on.

When installing on an existing clusters, use the [ az aks enable-addons](/en-us/cli/azure/aks#az-aks-enable-addons) command. The following code shows an example:

```
az aks enable-addons \
--resource-group myResourceGroup \
--name myAKSCluster \
--addons open-service-mesh
```


## Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Verify the OSM add-on is installed on your cluster

Verify the OSM add-on is installed on your cluster using the

command with and specify`az aks show`

`'addonProfiles.openServiceMesh.enabled'`

for the`--query`

parameter. In the output, under`addonProfiles`

, the`enabled`

value should show as`true`

for`openServiceMesh`

.`az aks show --resource-group myResourceGroup --name myAKSCluster --query 'addonProfiles.openServiceMesh.enabled'`


## Verify the OSM mesh is running on your cluster

Verify the version, status, and configuration of the OSM mesh running on your cluster using the

`kubectl get deployment`

command and display the image version of the*osm-controller*deployment.`kubectl get deployment -n kube-system osm-controller -o=jsonpath='{$.spec.template.spec.containers[:1].image}'`

The following example output shows version

*0.11.1*of the OSM mesh:`mcr.microsoft.com/oss/openservicemesh/osm-controller:v0.11.1`

Verify the status of the OSM components running on your cluster using the following

`kubectl`

commands to show the status of the`app.kubernetes.io/name=openservicemesh.io`

deployments, pods, and services.`kubectl get deployments -n kube-system --selector app.kubernetes.io/name=openservicemesh.io kubectl get pods -n kube-system --selector app.kubernetes.io/name=openservicemesh.io kubectl get services -n kube-system --selector app.kubernetes.io/name=openservicemesh.io`

Important

If any pods have a status other than

`Running`

, such as`Pending`

, your cluster might not have enough resources to run OSM. Review the sizing for your cluster, such as the number of nodes and the virtual machine's SKU, before continuing to use OSM on your cluster.Verify the configuration of your OSM mesh using the

`kubectl get meshconfig`

command.`kubectl get meshconfig osm-mesh-config -n kube-system -o yaml`

The following example output shows the configuration of an OSM mesh:

`apiVersion: config.openservicemesh.io/v1alpha1 kind: MeshConfig metadata: creationTimestamp: "0000-00-00A00:00:00A" generation: 1 name: osm-mesh-config namespace: kube-system resourceVersion: "2494" uid: 6c4d67f3-c241-4aeb-bf4f-b029b08faa31 spec: certificate: serviceCertValidityDuration: 24h featureFlags: enableEgressPolicy: true enableMulticlusterMode: false enableWASMStats: true observability: enableDebugServer: true osmLogLevel: info tracing: address: jaeger.osm-system.svc.cluster.local enable: false endpoint: /api/v2/spans port: 9411 sidecar: configResyncInterval: 0s enablePrivilegedInitContainer: false envoyImage: mcr.microsoft.com/oss/envoyproxy/envoy:v1.18.3 initContainerImage: mcr.microsoft.com/oss/openservicemesh/init:v0.9.1 logLevel: error maxDataPlaneConnections: 0 resources: {} traffic: enableEgress: true enablePermissiveTrafficPolicyMode: true inboundExternalAuthorization: enable: false failureModeAllow: false statPrefix: inboundExtAuthz timeout: 1s useHTTPSIngress: false`

The example output shows

`enablePermissiveTrafficPolicyMode: true`

, which means OSM has permissive traffic policy mode enabled. With this mode enabled in your OSM mesh:- The
[SMI](https://smi-spec.io/)traffic policy enforcement is bypassed. - OSM automatically discovers services that are a part of the service mesh.
- OSM creates traffic policy rules on each Envoy proxy sidecar to be able to communicate with these services.

- The

## Delete your cluster

When you no longer need the cluster, you can delete it using the

command, which removes the resource group, the cluster, and all related resources.`az group delete`

`az group delete --name myResourceGroup --yes --no-wait`


Note

Alternatively, you can uninstall the OSM add-on and the related resources from your cluster. For more information, see [Uninstall the Open Service Mesh add-on from your AKS cluster](open-service-mesh-uninstall-add-on).

## Next steps

This article showed you how to install the OSM add-on on an AKS cluster and verify it's installed and running. With the OSM add-on installed on your cluster, you can [deploy a sample application](https://release-v1-0.docs.openservicemesh.io/docs/getting_started/install_apps/) or [onboard an existing application](https://release-v1-0.docs.openservicemesh.io/docs/guides/app_onboarding/) to work with your OSM mesh.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/update-credentials -->

# Update or rotate the credentials for an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS clusters created with a service principal have a one-year expiration time. As you near the expiration date, you can reset the credentials to extend the service principal for an additional period of time. You might also want to update, or rotate, the credentials as part of a defined security policy. AKS clusters [integrated with Microsoft Entra ID](azure-ad-integration-cli) as an authentication provider have two more identities: the Microsoft Entra Server App and the Microsoft Entra Client App. This article details how to update the service principal and Microsoft Entra credentials for an AKS cluster.

Note

Alternatively, you can use a managed identity for permissions instead of a service principal. Managed identities don't require updates or rotations. For more information, see [Use managed identities](use-managed-identity).

## Before you begin

You need the Azure CLI version 2.0.65 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Update or create a new service principal for your AKS cluster

When you want to update the credentials for an AKS cluster, you can choose to either:

- Update the credentials for the existing service principal.
- Create a new service principal and update the cluster to use these new credentials.

Warning

If you choose to create a *new* service principal, wait around 30 minutes for the service principal permission to propagate across all regions. Updating a large AKS cluster to use these credentials can take a long time to complete.

### Check the expiration date of your service principal

To check the expiration date of your service principal, use the [ az ad app credential list](/en-us/cli/azure/ad/app/credential#az-ad-app-credential-list) command. The following example gets the service principal ID for the

`$CLUSTER_NAME`

cluster in the `$RESOURCE_GROUP_NAME`

resource group using the [command. The service principal ID is set as a variable named](/en-us/cli/azure/aks#az-aks-show)

`az aks show`

*SP_ID*.

```
SP_ID=$(az aks show --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME \
--query servicePrincipalProfile.clientId -o tsv)
az ad app credential list --id "$SP_ID" --query "[].endDateTime" -o tsv
```


### Reset the existing service principal credentials

To update the credentials for an existing service principal, get the service principal ID of your cluster using the [ az aks show](/en-us/cli/azure/aks#az-aks-show) command. The following example gets the ID for the

`$CLUSTER_NAME`

cluster in the `$RESOURCE_GROUP_NAME`

resource group. The variable named *SP_ID*stores the service principal ID used in the next step. These commands use the Bash command language.

Warning

When you reset your cluster credentials on an AKS cluster that uses Azure Virtual Machine Scale Sets, a [node image upgrade](node-image-upgrade) is performed to update your nodes with the new credential information.

```
SP_ID=$(az aks show --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME \
--query servicePrincipalProfile.clientId -o tsv)
```


Use the variable *SP_ID* containing the service principal ID to reset the credentials using the [ az ad app credential reset](/en-us/cli/azure/ad/app/credential#az-ad-app-credential-reset) command. The following example enables the Azure platform to generate a new secure secret for the service principal and store it as a variable named

*SP_SECRET*.

```
SP_SECRET=$(az ad app credential reset --id "$SP_ID" --query password -o tsv)
```


Next, you [update AKS cluster with service principal credentials](#update-aks-cluster-with-service-principal-credentials). This step is necessary to update the service principal on your AKS cluster.

### Create a new service principal

Note

If you updated the existing service principal credentials in the previous section, skip this section and instead [update the AKS cluster with service principal credentials](#update-aks-cluster-with-service-principal-credentials).

To create a service principal and update the AKS cluster to use the new credential, use the [ az ad sp create-for-rbac](/en-us/cli/azure/ad/sp#az-ad-sp-create-for-rbac) command.

```
az ad sp create-for-rbac --role Contributor --scopes /subscriptions/$SUBSCRIPTION_ID
```


The output is similar to the following example output. Make a note of your own `appId`

and `password`

to use in the next step.

```
{
"appId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"name": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"password": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"tenant": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
```


Define variables for the service principal ID and client secret using your output from running the [ az ad sp create-for-rbac](/en-us/cli/azure/ad/sp#az-ad-sp-create-for-rbac) command. The

*SP_ID*is the

*appId*, and the

*SP_SECRET*is your

*password*.

```
SP_ID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
SP_SECRET=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```


Next, you [update AKS cluster with the new service principal credential](#update-aks-cluster-with-service-principal-credentials). This step is necessary to update the AKS cluster with the new service principal credential.

## Update AKS cluster with service principal credentials

Important

For large clusters, updating your AKS cluster with a new service principal can take a long time to complete. Consider reviewing and customizing the [node surge upgrade settings](upgrade-aks-cluster#customize-node-surge-upgrade) to minimize disruption during the update. For small and midsize clusters, it takes a several minutes for the new credentials to update in the cluster.

Update the AKS cluster with your new or existing credentials by running the [ az aks update-credentials](/en-us/cli/azure/aks#az-aks-update-credentials) command.

```
az aks update-credentials \
--resource-group $RESOURCE_GROUP_NAME \
--name $CLUSTER_NAME \
--reset-service-principal \
--service-principal "$SP_ID" \
--client-secret "${SP_SECRET}"
```


## Update AKS cluster with new Microsoft Entra application credentials

You can create new Microsoft Entra server and client applications by following the [Microsoft Entra integration steps](azure-ad-integration-cli#create-azure-ad-server-component), or reset your existing Microsoft Entra applications following the [same method as for service principal reset](#reset-the-existing-service-principal-credentials). After that, you need to update your cluster Microsoft Entra application credentials using the [ az aks update-credentials](/en-us/cli/azure/aks#az-aks-update-credentials) command with the

*--reset-aad*variables.

```
az aks update-credentials \
--resource-group $RESOURCE_GROUP_NAME \
--name $CLUSTER_NAME \
--reset-aad \
--aad-server-app-id $SERVER_APPLICATION_ID \
--aad-server-app-secret $SERVER_APPLICATION_SECRET \
--aad-client-app-id $CLIENT_APPLICATION_ID
```


## Next steps

In this article, you learned how to update or rotate service principal and Microsoft Entra application credentials. For more information on how to use a manage identity for workloads within an AKS cluster, see [Best practices for authentication and authorization in AKS](operator-best-practices-identity).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/configure-load-balancer-standard -->

# Configure a public standard load balancer in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can customize different settings for your standard public load balancer at cluster creation time or by updating the cluster. These customization options allow you to create a load balancer that meets your workload needs. With the standard load balancer, you can:

[Change the inbound pool type](#change-the-inbound-pool-type).[Set or scale the number of managed outbound IPs](#scale-the-number-of-managed-outbound-public-ips).[Provide your own custom outbound IPs or outbound IP prefix](#provide-your-own-outbound-public-ips-or-prefixes).[Customize the number of allocated outbound ports to each node on the cluster](#configure-the-allocated-outbound-ports).[Configure the timeout setting for idle connections](#configure-the-load-balancer-idle-timeout).

Important

You can only use one outbound IP option (managed IPs, bring your own IP, or IP prefix) at a given time.

## Before you begin

- Follow the steps in
[Use a public standard load balancer in Azure Kubernetes Service (AKS)](load-balancer-standard)to create and deploy a load balancer service in AKS.

## Change the inbound pool type

You can reference AKS nodes in the load balancer backend pools by their IP configuration (Azure Virtual Machine Scale Sets based membership) or their IP address only. The IP address based backend pool membership provides higher efficiencies when updating services and provisioning load balancers, especially at high node counts. When combined with [NAT Gateway](nat-gateway) or [user-defined routing egress](egress-udr) types, provisioning of new nodes and services are more performant.

Two different pool membership types are available:

`nodeIPConfiguration`

: Legacy Virtual Machine Scale Sets IP configuration based pool membership type.`nodeIP`

: IP-based membership type.

### Requirements for changing the inbound pool type

Make sure you meet the following requirements before changing the inbound pool type:

- The AKS cluster must be version 1.23 or newer.
- The AKS cluster must be using standard load balancers and Virtual Machine Scale Sets.

-
[Create a new AKS cluster with IP-based inbound pool membership](#tabpanel_1_create-cluster-ip-based) -
[Update an existing AKS cluster to use IP-based inbound pool membership](#tabpanel_1_update-cluster-ip-based)

Create an AKS cluster with IP-based inbound pool membership using the

command with the`az aks create`

`--load-balancer-backend-pool-type=nodeIP`

parameter.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-backend-pool-type=nodeIP \ --generate-ssh-keys`


## Scale the number of managed outbound public IPs

Azure Load Balancer provides outbound and inbound connectivity from a VNet. Outbound rules make it simple to configure network address translation for the public standard load balancer.

Outbound rules follow the same syntax as load balancing and inbound NAT rules: *frontend IPs + parameters + backend pool*

An outbound rule configures outbound NAT for all virtual machines (VMs) identified by the backend pool to be translated to the frontend. Parameters provide more control over the outbound NAT algorithm.

While you can use an outbound rule with a single public IP address, outbound rules are great for scaling outbound NAT because they ease the configuration burden. You can use multiple IP addresses to plan for large-scale scenarios and outbound rules to mitigate SNAT exhaustion prone patterns. Each IP address provided by a frontend provides 64k ephemeral ports for the load balancer to use as SNAT ports.

When using a *Standard* SKU load balancer with managed outbound public IPs (which are created by default), you can scale the number of managed outbound public IPs using the `--load-balancer-managed-outbound-ip-count`

parameter.

Important

We don't recommend using the Azure portal to make any outbound rule changes. When making these changes, you should go through the AKS cluster and not directly on the Load Balancer resource.

Outbound rule changes made directly on the Load Balancer resource are removed whenever the cluster is reconciled, such as when it's stopped, started, upgraded, or scaled.

Use the Azure CLI, as shown in the examples. Outbound rule changes made using `az aks`

CLI commands are permanent across cluster downtime.

For more information, see [Azure Load Balancer outbound rules](/en-us/azure/load-balancer/outbound-rules).

### Set the number of managed outbound public IPs

-
[Create a new cluster with a specific number of managed outbound public IPs](#tabpanel_2_create-cluster-managed-outbound-ips) -
[Update an existing cluster to scale the number of managed outbound public IPs](#tabpanel_2_update-cluster-managed-outbound-ips)

Create a new AKS cluster with a specific number of managed outbound public IPs using the

command with the`az aks create`

`--load-balancer-managed-outbound-ip-count`

parameter. The following example sets the number of managed outbound public IPs to*two*.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-managed-outbound-ip-count 2 \ --generate-ssh-keys`


## Provide your own outbound public IPs or prefixes

When you use a *Standard* SKU load balancer, the AKS cluster automatically creates a public IP in the AKS-managed infrastructure resource group and assigns it to the load balancer outbound pool by default.

A public IP created by AKS is an AKS-managed resource, meaning AKS manages the lifecycle of that public IP and doesn't require user action directly on the public IP resource. Alternatively, you can assign your own custom public IP or public IP prefix at cluster creation time. Your custom IPs can also be updated on an existing cluster's load balancer properties.

### Requirements for using your own outbound public IPs or prefixes

Make sure you meet the following requirements before providing your own outbound public IPs or prefixes:

- You must create and own custom public IP addresses. You can't reuse managed public IP addresses created by AKS as a "bring your own custom IP" because it can cause management conflicts.
- You must ensure the AKS cluster identity has permissions to access the outbound IP, as per the
[required public IP permissions list](kubernetes-service-principal#grant-access-to-networking-resources). - Make sure you meet the
[prerequisites and constraints](/en-us/azure/virtual-network/ip-services/public-ip-address-prefix#limitations)necessary to configure outbound IPs or outbound IP prefixes.

### Provide your own outbound public IPs

-
[Provide your own outbound public IPs when creating a new cluster](#tabpanel_3_create-cluster-custom-ips) -
[Update an existing cluster to use your own outbound public IPs](#tabpanel_3_update-cluster-custom-ips)

Create a new AKS cluster with your own outbound public IPs using the

command with the`az aks create`

`--load-balancer-outbound-ips`

parameter. Make sure you replace the placeholder values with your own.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-outbound-ips $PUBLIC_IP_ID1,$PUBLIC_IP_ID2 \ --generate-ssh-keys`


### Provide your own outbound public IP prefixes

-
[Provide your own outbound public IP prefixes when creating a new cluster](#tabpanel_4_create-cluster-custom-ip-prefixes) -
[Update an existing cluster to use your own outbound public IP prefixes](#tabpanel_4_update-cluster-custom-ip-prefixes)

Create a new AKS cluster with your own outbound public IP prefixes using the

command with the`az aks create`

`--load-balancer-outbound-ip-prefixes`

parameter. Make sure you replace the placeholder values with your own.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --load-balancer-outbound-ip-prefixes $PUBLIC_IP_PREFIX_ID1,$PUBLIC_IP_PREFIX_ID2 \ --generate-ssh-keys`


## Configure the allocated outbound ports

Important

If you have applications on your cluster that can establish a large number of connections to small set of destinations on public IP addresses, like many instances of a frontend application connecting to a database, you might have a scenario susceptible to encounter SNAT port exhaustion. SNAT port exhaustion happens when an application runs out of outbound ports to use to establish a connection to another application or host. If you have a scenario susceptible to encounter SNAT port exhaustion, we highly recommend you increase the allocated outbound ports and outbound frontend IPs on the load balancer.

For more information on SNAT, see [Use SNAT for outbound connections](/en-us/azure/load-balancer/load-balancer-outbound-connections).

By default, AKS sets *AllocatedOutboundPorts* on its load balancer to `0`

, which enables [automatic outbound port assignment based on backend pool size](/en-us/azure/load-balancer/load-balancer-outbound-connections#preallocatedports) when creating a cluster. For example, if a cluster has 50 or fewer nodes, 1024 ports are allocated to each node. This value allows for scaling to cluster maximum node counts without requiring networking reconfiguration, but can make SNAT port exhaustion more common as more nodes are added. As the number of nodes in the cluster increases, fewer ports are available per node. Increasing the node counts across the boundaries in the chart (for example, going from 50 to 51 nodes or 100 to 101) might be disruptive to connectivity as the SNAT ports allocated to existing nodes are reduced to allow for more nodes. We recommend using an explicit value for *AllocatedOutboundPorts*.

### View the current allocated outbound ports

Get the

*AllocatedOutboundPorts*value for the AKS cluster load balancer using thecommand.`az network lb outbound-rule list`

`NODE_RG=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query nodeResourceGroup -o tsv) az network lb outbound-rule list --resource-group $NODE_RG --lb-name kubernetes -o table`

The following example output shows that automatic outbound port assignment based on backend pool size is enabled for the cluster:

`AllocatedOutboundPorts EnableTcpReset IdleTimeoutInMinutes Name Protocol ProvisioningState ResourceGroup ------------------------ ---------------- ---------------------- --------------- ---------- ------------------- ------------- 0 True 30 aksOutboundRule All Succeeded MC_myResourceGroup_myAKSCluster_eastus`


### Calculate and verify outbound ports and IPs needed

Before setting a specific value or increasing an existing value for either outbound ports or outbound IP addresses, you must calculate the appropriate number of outbound ports and IP addresses. Use the following equation for this calculation rounded to the nearest integer: `64,000 ports per IP / <outbound ports per node> * <number of outbound IPs> = <maximum number of nodes in the cluster>`

.

#### Considerations for calculating outbound ports and IPs

When calculating the number of outbound ports and IPs and setting the values, keep the following information in mind:

- The number of outbound ports per node is fixed based on the value you set.
- The value for outbound ports must be a multiple of 8.
- Adding more IPs doesn't add more ports to any node, but it provides capacity for more nodes in the cluster.
- You must account for nodes that might be added as part of upgrades, including the count of nodes specified via
and`maxCount`

values.`maxSurge`


#### Examples of calculating outbound ports and IPs

The following examples show how the values you set affect the number of outbound ports and IP addresses:

- If the default values are used and the cluster has 48 nodes, each node has 1024 ports available.
- If the default values are used and the cluster scales from 48 to 52 nodes, each node is updated from 1024 ports available to 512 ports available.
- If the number of outbound ports is set to 1,000 and the outbound IP count is set to 2, then the cluster can support a maximum of 128 nodes:
`64,000 ports per IP / 1,000 ports per node * 2 IPs = 128 nodes`

. - If the number of outbound ports is set to 1,000 and the outbound IP count is set to 7, then the cluster can support a maximum of 448 nodes:
`64,000 ports per IP / 1,000 ports per node * 7 IPs = 448 nodes`

. - If the number of outbound ports is set to 4,000 and the outbound IP count is set to 2, then the cluster can support a maximum of 32 nodes:
`64,000 ports per IP / 4,000 ports per node * 2 IPs = 32 nodes`

. - If the number of outbound ports is set to 4,000 and the outbound IP count is set to 7, then the cluster can support a maximum of 112 nodes:
`64,000 ports per IP / 4,000 ports per node * 7 IPs = 112 nodes`

.

Important

After calculating the number of outbound ports and IPs, verify you have extra outbound port capacity to handle node surge during upgrades. It's critical to allocate sufficient excess ports for extra nodes needed for upgrade and other operations. AKS defaults to *one* buffer node for upgrade operations. If you're using [ maxSurge values](upgrade-aks-cluster#customize-node-surge-upgrade), multiply the outbound ports per node by your

`maxSurge`

value to determine the number of ports required. For example, if you calculate that you need 4000 ports per node with 7 IP addresses on a cluster with a maximum of 100 nodes and a max surge of 2:- 2 surge nodes * 4000 ports per node = 8000 ports needed for node surge during upgrades.
- 100 nodes * 4000 ports per node = 400,000 ports required for your cluster.
- 7 IPs * 64000 ports per IP = 448,000 ports available for your cluster.

This example shows the cluster has an excess capacity of 48,000 ports, which is sufficient to handle the 8000 ports needed for node surge during upgrades.

### Set the allocated outbound ports and outbound IPs

Once the values have been calculated and verified, you can apply those values using `load-balancer-outbound-ports`

and either `load-balancer-managed-outbound-ip-count`

, `load-balancer-outbound-ips`

, or `load-balancer-outbound-ip-prefixes`

when creating or updating a cluster.

-
[Create a new cluster with specific outbound ports and IPs](#tabpanel_5_create-cluster-outbound-ports-ips) -
[Update an existing cluster with specific outbound ports and IPs](#tabpanel_5_update-cluster-outbound-ports-ips)

Create a new AKS cluster with specific outbound ports and IPs using the

command. The following example sets the`az aks create`

`--load-balancer-managed-outbound-ip-count`

parameter to*7*and the`--load-balancer-outbound-ports`

parameter to*4000*:`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-managed-outbound-ip-count 7 \ --load-balancer-outbound-ports 4000 \ --generate-ssh-keys`


## Configure the load balancer idle timeout

When SNAT port resources are exhausted, outbound flows fail until existing flows release SNAT ports. Load balancer reclaims SNAT ports when the flow closes, and the AKS-configured load balancer uses a 30-minute idle timeout for reclaiming SNAT ports from idle flows. You can also use transport (for example, ** TCP keepalives** or

**) to refresh an idle flow and reset this idle timeout if necessary.**

`application-layer keepalives`

If you expect to have numerous short-lived connections and no long-lived connections that might have long times of idle, like using `kubectl proxy`

or `kubectl port-forward`

, consider using a low timeout value such as *4 minutes*. When using TCP keepalives, it's sufficient to enable them on one side of the connection. For example, it's sufficient to enable them on the server side only to reset the idle timer of the flow. It's not necessary for both sides to start TCP keepalives. Similar concepts exist for application layer, including database client-server configurations. Check the server side for what options exist for application-specific keepalives.

Important

AKS enables *TCP Reset* on idle by default. We recommend you keep this configuration and leverage it for more predictable application behavior on your scenarios. For more information, see [Azure load balancer TCP reset](/en-us/azure/load-balancer/load-balancer-tcp-reset).

When setting *IdleTimeoutInMinutes* to a different value than the default of 30 minutes, consider how long your workloads need an outbound connection. Also consider that the default timeout value for a *Standard* SKU load balancer used outside of AKS is *4 minutes*. An *IdleTimeoutInMinutes* value that more accurately reflects your specific AKS workload can help decrease SNAT exhaustion caused by tying up connections no longer being used.

Warning

Altering the values for *AllocatedOutboundPorts* and *IdleTimeoutInMinutes* might significantly change the behavior of the outbound rule for your load balancer and shouldn't be done lightly. See [Troubleshoot SNAT](troubleshoot-source-network-address-translation) and review the [Load balancer outbound rules](/en-us/azure/load-balancer/load-balancer-outbound-connections#outboundrules) and [outbound connections in Azure](/en-us/azure/load-balancer/load-balancer-outbound-connections) before updating these values to fully understand the impact of your changes.

-
[Create a new cluster with a specific idle timeout](#tabpanel_6_create-cluster-idle-timeout) -
[Update an existing cluster with a specific idle timeout](#tabpanel_6_update-cluster-idle-timeout)

Create a new AKS cluster with a specific idle timeout using the

command with the`az aks create`

`--load-balancer-idle-timeout`

parameter. The following example sets the idle timeout to*4 minutes*:`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-idle-timeout 4 \ --generate-ssh-keys`


## Restrict inbound traffic to specific IP ranges

The following manifest uses `loadBalancerSourceRanges`

to specify a new IP range for inbound external traffic:

```
apiVersion: v1
kind: Service
metadata:
name: azure-vote-front
spec:
type: LoadBalancer
ports:
- port: 80
selector:
app: azure-vote-front
loadBalancerSourceRanges:
- MY_EXTERNAL_IP_RANGE
```


This example updates the rule to allow inbound external traffic only from the `MY_EXTERNAL_IP_RANGE`

range. If you replace `MY_EXTERNAL_IP_RANGE`

with the internal subnet IP address, traffic is restricted to only cluster internal IPs. If traffic is restricted to cluster internal IPs, clients outside your Kubernetes cluster are unable to access the load balancer.

Note

Keep the following information in mind when restricting inbound traffic:

- When you need to allow both CIDR blocks and Azure service tags, remove the
`loadBalancerSourceRanges`

property and add the`service.beta.kubernetes.io/azure-allowed-ip-ranges`

and/or`service.beta.kubernetes.io/azure-allowed-service-tags`

Load Balancer annotations. This configuration applies filtering only at the NSG layer and skips host-level kube-proxy rules. If you set the`loadBalancerSourceRanges`

property together with the`azure-allowed-service-tags`

annotation, AKS will report an error when you attempt to apply the specification. - Inbound, external traffic flows from the load balancer to the VNet for your AKS cluster. The VNet has a network security group (NSG) which allows all inbound traffic from the load balancer. This NSG uses a
[service tag](/en-us/azure/virtual-network/network-security-groups-overview#service-tags)of type*LoadBalancer*to allow traffic from the load balancer. - Pod CIDR should be added to
`loadBalancerSourceRanges`

if there are Pods needing to access the service's Load Balancer IP for clusters with Kubernetes version 1.25 or higher.

## Maintain the client's IP on inbound connections

By default, a service of type `LoadBalancer`

[in Kubernetes](https://kubernetes.io/docs/tutorials/services/source-ip/#source-ip-for-services-with-type-loadbalancer) and in AKS doesn't persist the client's IP address on the connection to the pod. The source IP on the packet that's delivered to the pod becomes the private IP of the node. To maintain the client's IP address, you must set `service.spec.externalTrafficPolicy`

to `local`

in the service definition. The following manifest shows an example:

```
apiVersion: v1
kind: Service
metadata:
name: azure-vote-front
spec:
type: LoadBalancer
externalTrafficPolicy: Local
ports:
- port: 80
selector:
app: azure-vote-front
```


## Customizations via Kubernetes Annotations

The following annotations are supported for Kubernetes services with type `LoadBalancer`

, and they only apply to **INBOUND** flows.

| Annotation | Value | Description |
|---|---|---|
`service.beta.kubernetes.io/azure-load-balancer-internal` |
`true` or `false` |
Specify whether the load balancer should be internal. If not set, it defaults to public. |
`service.beta.kubernetes.io/azure-load-balancer-internal-subnet` |
Name of the subnet | Specify which subnet the internal load balancer should be bound to. If not set, it defaults to the subnet configured in cloud config file. |
`service.beta.kubernetes.io/azure-dns-label-name` |
Name of the DNS label on Public IPs | Specify the DNS label name for the public service. If it's set to an empty string, the DNS entry in the Public IP isn't used. |
`service.beta.kubernetes.io/azure-shared-securityrule` |
`true` or `false` |
Specify exposing the service through a potentially shared Azure security rule to increase service exposure, utilizing Azure
|

`service.beta.kubernetes.io/azure-load-balancer-resource-group`

`service.beta.kubernetes.io/azure-allowed-service-tags`

[service tags](/en-us/azure/virtual-network/network-security-groups-overview#service-tags)separated by commas.`service.beta.kubernetes.io/azure-allowed-ip-ranges`

`service.beta.kubernetes.io/azure-load-balancer-tcp-idle-timeout`

`service.beta.kubernetes.io/azure-load-balancer-disable-tcp-reset`

`true`

or `false`

`service.beta.kubernetes.io/azure-load-balancer-ipv4`

`service.beta.kubernetes.io/azure-load-balancer-ipv6`

### Customize allowed IP ranges (preview)

You can use the `azure-allowed-service-tags`

and `azure-allowed-ip-ranges`

annotations to combine CIDR blocks and Azure service tags on the load balancer. Add `service.beta.kubernetes.io/azure-allowed-ip-ranges`

with a comma-separated list of IP prefixes, and add `service.beta.kubernetes.io/azure-allowed-service-tags`

with one or more Azure service tags. The AKS cloud provider merges both values into a single NSG rule, so traffic is filtered centrally at the NSG giving you a single, NSG-centric control plane for both IP addresses and service tags.

You can continue to use the `loadBalancerSourceRanges`

property for cases where you want CIDR-based restrictions enforced both in the NSG and the host. You can't use this property with the `azure-allowed-service-tags`

annotation. If both are specified, AKS reports an error when you try to apply the load balancer service specification.

### Customize the load balancer health probe

The following annotations are supported to customize the load balancer health probe behavior:

| Annotation | Value | Description |
|---|---|---|
`service.beta.kubernetes.io/azure-load-balancer-health-probe-interval` |
Health probe interval | |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-num-of-probe` |
The minimum number of unhealthy responses of health probe | |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path` |
Request path of the health probe | |
`service.beta.kubernetes.io/port_{port}_no_lb_rule` |
true/false | {port} is service port number. When set to `true` , no load balancer or health probe rules for this port are generated. Health check service shouldn't be exposed to the public internet. |
`service.beta.kubernetes.io/port_{port}_no_probe_rule` |
true/false | {port} is service port number. When set to `true` , no health probe rules for this port are generated. |
`service.beta.kubernetes.io/port_{port}_health-probe_protocol` |
Health probe protocol | {port} is service port number. Explicit protocol for the health probe for the service port {port}, overriding port.appProtocol if set. |
`service.beta.kubernetes.io/port_{port}_health-probe_port` |
port number or port name in service manifest | {port} is service port number. Explicit port for the health probe for the service port {port}, overriding the default value. |
`service.beta.kubernetes.io/port_{port}_health-probe_interval` |
Health probe interval | {port} is service port number. |
`service.beta.kubernetes.io/port_{port}_health-probe_num-of-probe` |
The minimum number of unhealthy responses of health probe | {port} is service port number. |
`service.beta.kubernetes.io/port_{port}_health-probe_request-path` |
Request path of the health probe | {port} is service port number. |

Note

AKS now supports shared health probes for `externalTrafficPolicy: Cluster`

Services. To learn more, see [Use shared health probes for externalTrafficPolicy: Cluster Services (preview) in Azure Kubernetes Service (AKS)](shared-health-probes).

#### Default health probe behavior

Currently, the default protocol of the health probe varies among services with different transport protocols, app protocols, annotation, and external traffic policies.

- For local services, HTTP and /healthz would be used. The health probe will query
`NodeHealthPort`

rather than actual backend service. - For cluster TCP services, TCP would be used.
- For cluster UDP services, no health probes.

Note

For local services with PLS integration and PLS proxy protocol enabled, the default HTTP and /healthz health probe doesn't work. Thus health probe can be customized the same way as cluster services to support this scenario.

##### Health probe request path annotation

Starting in Kubernetes version 1.20, the service annotation `service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path`

was introduced to determine the health probe behavior.

- For clusters <=1.23,
`spec.ports.appProtocol`

would only be used as probe protocol when`service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path`

is also set. - For clusters >1.24,
`spec.ports.appProtocol`

would be used as probe protocol and`/`

would be used as default probe request path (`service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path`

could be used to change to a different request path).

Note that the request path would be ignored when using TCP or the `spec.ports.appProtocol`

is empty. The following table summarizes the default health probe behavior:

| loadbalancer sku | `externalTrafficPolicy` |
spec.ports.Protocol | spec.ports.AppProtocol | `service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path` |
LB probe protocol | LB probe request path |
|---|---|---|---|---|---|---|
| standard | local | any | any | any | http | `/healthz` |
| standard | cluster | udp | any | any | null | null |
| standard | cluster | tcp | (ignored) | tcp | null | |
| standard | cluster | tcp | tcp | (ignored) | tcp | null |
| standard | cluster | tcp | http/https | TCP(<=1.23) or http/https(>=1.24) | null(<=1.23) or `/` (>=1.24) |
|
| standard | cluster | tcp | http/https | `/custom-path` |
http/https | `/custom-path` |
| standard | cluster | tcp | unsupported protocol | `/custom-path` |
tcp | null |
| basic | local | any | any | any | http | `/healthz` |
| basic | cluster | tcp | (ignored) | tcp | null | |
| basic | cluster | tcp | tcp | (ignored) | tcp | null |
| basic | cluster | tcp | http | TCP(<=1.23) or http/https(>=1.24) | null(<=1.23) or `/` (>=1.24) |
|
| basic | cluster | tcp | http | `/custom-path` |
http | `/custom-path` |
| basic | cluster | tcp | unsupported protocol | `/custom-path` |
tcp | null |

##### Health probe interval and number of probes annotations

Starting in Kubernetes version 1.21, two service annotations `service.beta.kubernetes.io/azure-load-balancer-health-probe-interval`

and `load-balancer-health-probe-num-of-probe`

were introduced, which customize the configuration of health probe. If `service.beta.kubernetes.io/azure-load-balancer-health-probe-interval`

isn't set, a default value of *5* is applied. If `load-balancer-health-probe-num-of-probe`

isn't set, a default value of *2* is applied.

### Custom Load Balancer health probe for port

Different ports in a service can require different health probe configurations. This could be because of service design (such as a single health endpoint controlling multiple ports), or Kubernetes features like the [MixedProtocolLBService](https://kubernetes.io/docs/concepts/services-networking/service/#load-balancers-with-mixed-protocol-types).

The following table summarizes the port-specific annotations that can be used to override the global health probe annotations for a specific port in the service:

| Port-specific annotation | Global probe annotation | Behavior |
|---|---|---|
`service.beta.kubernetes.io/port_{port}_no_lb_rule` |
N/A (no equivalent globally) | If set to `true` , no load balancer or probe rules are generated. |
`service.beta.kubernetes.io/port_{port}_no_probe_rule` |
N/A (no equivalent globally) | If set to `true` , no probe rules are generated. |
`service.beta.kubernetes.io/port_{port}_health-probe_protocol` |
N/A (no equivalent globally) | Sets the health probe protocol for this service port (for example: Http, Https, Tcp). |
`service.beta.kubernetes.io/port_{port}_health-probe_port` |
N/A (no equivalent globally) | Sets the health probe port for this service port (for example: 15021). |
`service.beta.kubernetes.io/port_{port}_health-probe_request-path` |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path` |
For Http or Https, sets the health probe request path (defaults to /). |
`service.beta.kubernetes.io/port_{port}_health-probe_num-of-probe` |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-num-of-probe` |
Number of consecutive probe failures before the port is considered unhealthy. |
`service.beta.kubernetes.io/port_{port}_health-probe_interval` |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-interval` |
The amount of time between probe attempts. |

## Next steps

To learn more about Kubernetes services, see the [Kubernetes services documentation](https://kubernetes.io/docs/concepts/services-networking/service/).

To learn more about using internal load balancer for inbound traffic, see the [AKS internal load balancer documentation](internal-lb).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr-troubleshooting -->

# Troubleshoot Dapr extension installation errors

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article discusses some common error messages that you may receive when you install or update the [Distributed Application Runtime (Dapr)](https://dapr.io/) extension for Microsoft Azure Kubernetes Service (AKS) or Arc for Kubernetes.

[Learn more about the level of support provided for the Dapr extension.](#next-steps)

## Scenario 1: Installation fails but doesn't show an error message

If the extension generates an error message when you create or update it, you can inspect where the creation failed by running the [az k8s-extension list](/en-us/cli/azure/k8s-extension#az-k8s-extension-list) command:

```
az k8s-extension list --resource-group <my-resource-group-name> \
--cluster-name <my-cluster-name> \
--cluster-type managedClusters
```


If a wrong key is used in the configuration settings, such as `global.ha=false`

instead of `global.ha.enabled=false`

, the following JSON status is returned. The error message is captured in the `message`

property.

```
"statuses": [
{
"code": "InstallationFailed",
"displayStatus": null,
"level": null,
"message": "Error: {failed to install chart from path [] for release [dapr-1]: err [template: dapr/charts/dapr_sidecar_injector/templates/dapr_sidecar_injector_poddisruptionbudget.yaml:1:17: executing \"dapr/charts/dapr_sidecar_injector/templates/dapr_sidecar_injector_poddisruptionbudget.yaml\" at <.Values.global.ha.enabled>: can't evaluate field enabled in type interface {}]} occurred while doing the operation : {Installing the extension} on the config",
"time": null
}
],
```


Here's another example of a JSON error message:

```
"statuses": [
{
"code": "InstallationFailed",
"displayStatus": null,
"level": null,
"message": "The extension operation failed with the following error: unable to add the configuration with configId {extension:microsoft-dapr} due to error: {error while adding the CRD configuration: error {failed to get the immutable configMap from the elevated namespace with err: configmaps 'extension-immutable-values' not found }}. (Code: ExtensionOperationFailed)",
"time": null
}
]
```


### Solution 1: Restart the cluster, register the service provider, or delete and reinstall Dapr

To fix this issue, try the following methods:

Force delete and

[reinstall the Dapr extension](/en-us/azure/aks/dapr).

## Scenario 2: Targeted Dapr version doesn't exist

When you try to install the Dapr extension to [target a specific version](/en-us/azure/aks/dapr#targeting-a-specific-dapr-version), you receive an error message that states that the Dapr version doesn't exist:

(ExtensionOperationFailed) The extension operation failed with the following error: Failed to resolve the extension version from the given values.

Code: ExtensionOperationFailed

Message: The extension operation failed with the following error: Failed to resolve the extension version from the given values.


### Solution 2: Install again for a supported Dapr version

Try again to install the extension. Make sure that you use a [supported version of Dapr](/en-us/azure/aks/dapr#dapr-versions).

## Scenario 3: The targeted Dapr version exists but not in the specified region

Because some versions of Dapr aren't available in all regions, you might receive the following error message:

(ExtensionTypeRegistrationGetFailed) Extension type microsoft.dapr is not registered in region <regionname>.

Code: ExtensionTypeRegistrationGetFailed

Message: Extension type microsoft.dapr is not registered in region <regionname>


### Solution 3: Install in a different region

Install in a [region in which your Dapr version is supported](/en-us/azure/aks/dapr#cloudsregions).

## Scenario 4: Dapr is already installed

You try to install the Dapr extension for AKS or Arc for Kubernetes, but you receive an error message that indicates that the `dapr-system`

namespace already exists. This error message resembles the following text:

(ExtensionOperationFailed) The extension operation failed with the following error: Error: {failed to install chart from path [] for release [dapr-ext]: err [rendered manifests contain a resource that already exists. Unable to continue with install: ServiceAccount "dapr-operator" in namespace "dapr-system" exists and cannot be imported into the current release: invalid ownership metadata; annotation validation error: key "meta.helm.sh/release-name" must equal "dapr-ext": current value is "dapr"]} occurred while doing the operation : {Installing the extension} on the config


### Solution 4: Uninstall Dapr OSS first

Uninstall the Dapr OSS before you install the Dapr extension. For more information, see [Migrate from Dapr OSS to the Dapr extension for AKS](/en-us/azure/aks/dapr-migration).

## Scenario 5: The placement server pod is in a bad state

You encounter the following error:

0/4 nodes are available: 1 node(s) were unschedulable, 3 node(s) had volume node affinity conflict. preemption: 0/4 nodes are available: 4 Preemption is not helpful for scheduling.


This issue might happen when the placement server pod tries to use the persistent volume that's created in a different zone from the placement server pod itself.

### Solution 5: Install Dapr in multiple availability zones or limit the placement service to a particular availability zone

To resolve this issue, use one of the following methods:

Follow the recommended approach in

[Install Dapr in multiple availability zones while in HA mode](/en-us/azure/aks/dapr-settings#install-dapr-in-multiple-availability-zones-while-in-ha-mode).Limit the placement service to a particular availability zone by creating a custom storage class and using it for the placement service, and then run the following command:

`az k8s-extension create --cluster-type managedClusters --cluster-name <clustername> --resource-group <resourcegroup> --name <name> --extension-type Microsoft.Dapr --auto-upgrade-minor-version <minorversion> --version <version> --configuration-settings "dapr_placement.volumeclaims.storageClassName=zone-restricted"`

Here's an example of creating a custom storage class:

`kind: StorageClass apiVersion: storage.k8s.io/v1 metadata: name: zone-restricted provisioner: disk.csi.azure.com reclaimPolicy: Delete allowVolumeExpansion: true volumeBindingMode: WaitForFirstConsumer allowedTopologies: - matchLabelExpressions: - key: topology.kubernetes.io/zone values: - centralus-1 parameters: storageaccounttype: StandardSSD_LRS`


## Next steps

If you're still experiencing installation issues, [create a support request](https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview?DMC=troubleshoot) for Microsoft to investigate and resolve.

If you're experiencing Dapr runtime security risks and regressions while using the extension, open an issue with the [Dapr open source project](https://github.com/dapr/dapr/issues/new/choose).

Note

Learn more about [how Microsoft handles issues raised for the Dapr extension](/en-us/azure/aks/dapr-overview#issue-handling).

You could also start a discussion in the Dapr project Discord:

**Third-party information disclaimer**

The third-party products that this article discusses are manufactured by companies that are independent of Microsoft. Microsoft makes no warranty, implied or otherwise, about the performance or reliability of these products.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-faq -->

# Frequently asked questions about Windows Server on AKS

This article provides answers to some of the most common questions about using Windows Server containers on Azure Kubernetes Service (AKS).

## Why can't I create new Windows Server 2019 node pools?

Windows Server 2019 isn't supported in Kubernetes version 1.33 and above. Use a supported Windows Server version such as Windows Server 2025 (preview) or Windows Server 2022.

## Why can't I upgrade my Windows Server 2019 node pools to Kubernetes version 1.33?

Windows Server 2019 isn't supported in Kubernetes version 1.33 and above. Use a supported Windows Server version such as Windows Server 2025 (preview) or Windows Server 2022.

## What kind of disks are supported for Windows?

Azure Disks and Azure Files are the supported volume types, and are accessed as New Technology File System (NTFS) volumes in the Windows Server container.

## Does Windows support generation 2 virtual machines (VMs)?

Generation 2 VMs are supported on Windows starting with Windows Server 2022. Generation 2 VMs are default in Windows Server 2025.

For more information, see [Support for generation 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2).

## How do I patch my Windows nodes?

To get the latest patches for Windows nodes, you can either [upgrade the node pool](manage-node-pools#upgrade-a-single-node-pool) or [upgrade the node image](node-image-upgrade).

## Is preserving the client source IP supported?

At this time, [client source IP preservation](concepts-network-ingress#ingress-controllers) isn't supported with Windows nodes.

## Can I change the maximum number of pods per node?

Yes. For more information, see [Maximum number of pods](concepts-network-ip-address-planning#maximum-pods-per-node).

## What is the default transmission control protocol (TCP) time-out in Windows OS?

The default TCP time-out in Windows OS is four minutes. This value isn't configurable. When an application uses a longer time-out, the TCP connections between different containers in the same node close after four minutes.

## Why am I seeing an error when I try to create a new Windows agent pool?

If you created your cluster before February 2020 and didn't perform any upgrade operations, the cluster still uses an old Windows image. You might see an error that resembles the following example:

"The following list of images referenced from the deployment template isn't found: Publisher: MicrosoftWindowsServer, Offer: WindowsServer, Sku: 2019-datacenter-core-smalldisk-2004, Version: latest. Refer to [Find and use Azure Marketplace Virtual Machine images with Azure PowerShell](/en-us/azure/virtual-machines/windows/cli-ps-findimage) for instructions on finding available images."

To fix this issue, you need to perform the following steps:

- Upgrade the
[cluster control plane](manage-node-pools#upgrade-a-cluster-control-plane-with-multiple-node-pools), which updates the image offer and publisher. - Create new Windows agent pools.
- Move Windows pods from existing Windows agent pools to new Windows agent pools.
- Delete old Windows agent pools.

## Why am I seeing an error when I try to deploy Windows pods?

If you specify a value in `--max-pods`

less than the number of pods you want to create, you might see the `No available addresses`

error.

To fix this error, use the `az aks nodepool add`

command with a high enough `--max-pods`

value. For example:

```
az aks nodepool add \
--cluster-name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--name $NODEPOOL_NAME \
--max-pods 3
```


For more details, see the [ --max-pods documentation](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add).

## Why is there an unexpected user named "sshd" on my virtual machine node?

AKS adds a user named "sshd" when installing the OpenSSH service. This user isn't malicious. We recommend that customers update their alerts to ignore this unexpected user account.

## How do I rotate the service principal for my Windows node pool?

Windows node pools don't support service principal rotation. To update the service principal, create a new Windows node pool and migrate your pods from the older pool to the new one. After your pods are migrated to the new pool, delete the older node pool.

Instead of service principals, you can use managed identities. For more information, see [Use managed identities in AKS](use-managed-identity).

## How do I change the administrator password for Windows Server nodes on my cluster?

To change the administrator password using the Azure CLI, use the `az aks update`

command with the `--admin-password`

parameter. For example:

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--admin-password <new-password>
```


To change the password using Azure PowerShell, use the `Set-AzAksCluster`

cmdlet with the `-AdminPassword`

parameter. For example:

```
Set-AzAksCluster `
-ResourceGroupName $RESOURCE_GROUP `
-Name $CLUSTER_NAME `
-AdminPassword <new-password>
```


Keep in mind that performing a cluster update causes a restart and only updates the Windows Server node pools. For information about Windows Server password requirements, see [Windows Server password requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference).

## How many node pools can I create?

AKS clusters with Windows node pools have the same resource limits as the default limits specified for the AKS service. For more information, see [Quotas, virtual machine size restrictions, and region availability in Azure Kubernetes Service (AKS)](quotas-skus-regions).

## Can I run ingress controllers on Windows nodes?

Yes, you can run ingress controllers that support Windows Server containers.

## Can my Windows Server containers use gMSA?

Yes. Group-managed service account (gMSA) support is generally available (GA) for Windows on AKS. For more information, see [Enable Group Managed Service Accounts (GMSA) for your Windows Server nodes on your Azure Kubernetes Service (AKS) cluster](use-group-managed-service-accounts)

## Are there any limitations on the number of services on a cluster with Windows nodes?

A cluster with Windows nodes can have approximately 500 services (sometimes less) before it encounters port exhaustion. This limitation applies to a Kubernetes Service with External Traffic Policy set to "Cluster".

When the external traffic policy on a Service is configured as a Cluster, the traffic undergoes an extra Source NAT on the node. This process also results in reservation of a port from the TCPIP dynamic port pool. This port pool is a limited resource (~16K ports by default) and many active connections to a Service can lead to dynamic port pool exhaustion resulting in connection drops.

If the Kubernetes Service is configured with External Traffic Policy set to "Local", port exhaustion problems aren't likely to occur at 500 services.

## How do I change the time zone of a running container?

To change the time zone of a running Windows Server container, connect to the running container with a PowerShell session. For example:

```
kubectl exec -it CONTAINER-NAME -- PowerShell
```


In the running container, use [Set-TimeZone](/en-us/powershell/module/microsoft.powershell.management/set-timezone) to set the time zone of the running container. For example:

```
Set-TimeZone -Id "Russian Standard Time"
```


To see the current time zone of the running container or an available list of time zones, use [Get-TimeZone](/en-us/powershell/module/microsoft.powershell.management/get-timezone).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/control-kubeconfig-access -->

# Use Azure role-based access control to define access to the Kubernetes configuration file in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can interact with Kubernetes clusters using the `kubectl`

tool. The Azure CLI provides an easy way to get the access credentials and *kubeconfig* configuration file to connect to your AKS clusters using `kubectl`

. You can use Azure role-based access control (Azure RBAC) to limit who can get access to the *kubeconfig* file and the permissions they have.

This article shows you how to assign Azure roles that limit who can get the configuration information for an AKS cluster.

## Before you begin

- This article assumes that you have an existing AKS cluster. If you need an AKS cluster, create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[the Azure portal](learn/quick-kubernetes-deploy-portal). - This article also requires that you're running Azure CLI version 2.0.65 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Available permissions for cluster roles

When you interact with an AKS cluster using the `kubectl`

tool, a configuration file, called *kubeconfig*, defines cluster connection information. This configuration file is typically stored in *~/.kube/config*. Multiple clusters can be defined in this *kubeconfig* file. You can switch between clusters using the [ kubectl config use-context](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#config) command.

The [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command lets you get the access credentials for an AKS cluster and merges these credentials into the

*kubeconfig*file. You can use Azure RBAC to control access to these credentials. These Azure roles let you define who can retrieve the

*kubeconfig*file and what permissions they have within the cluster.

There are two Azure roles you can apply to a Microsoft Entra user or group:

**Azure Kubernetes Service Cluster Admin Role**- Allows access to
`Microsoft.ContainerService/managedClusters/listClusterAdminCredential/action`

API call. This API call[lists the cluster admin credentials](/en-us/rest/api/aks/managedclusters/listclusteradmincredentials). - Downloads
*kubeconfig*for the*clusterAdmin*role.

- Allows access to
**Azure Kubernetes Service Cluster User Role**- Allows access to
`Microsoft.ContainerService/managedClusters/listClusterUserCredential/action`

API call. This API call[lists the cluster user credentials](/en-us/rest/api/aks/managedclusters/listclusterusercredentials). - Downloads
*kubeconfig*for*clusterUser*role.

- Allows access to

Note

On clusters that use Microsoft Entra ID, users with the *clusterUser* role have an empty *kubeconfig* file that prompts a login. Once logged in, users have access based on their Microsoft Entra user or group settings. Users with the *clusterAdmin* role have admin access.

On clusters that don't use Microsoft Entra ID, the *clusterUser* role has same effect of *clusterAdmin* role.

## Assign role permissions to a user or group

To assign one of the available roles, you need to get the resource ID of the AKS cluster and the ID of the Microsoft Entra user account or group using the following steps:

- Get the cluster resource ID using the
command for the cluster named`az aks show`

*myAKSCluster*in the*myResourceGroup*resource group. Provide your own cluster and resource group name as needed. - Use the
and`az account show`

commands to get your user ID.`az ad user show`

- Assign a role using the
command.`az role assignment create`


The following example assigns the *Azure Kubernetes Service Cluster Admin Role* to an individual user account:

```
# Get the resource ID of your AKS cluster
AKS_CLUSTER=$(az aks show --resource-group myResourceGroup --name myAKSCluster --query id -o tsv)
# Get the account credentials for the logged in user
ACCOUNT_UPN=$(az account show --query user.name -o tsv)
ACCOUNT_ID=$(az ad user show --id $ACCOUNT_UPN --query objectId -o tsv)
# Assign the 'Cluster Admin' role to the user
az role assignment create \
--assignee $ACCOUNT_ID \
--scope $AKS_CLUSTER \
--role "Azure Kubernetes Service Cluster Admin Role"
```


If you want to assign permissions to a Microsoft Entra group, update the `--assignee`

parameter shown in the previous example with the object ID for the *group* rather than the *user*.

To get the object ID for a group, use the [ az ad group show](/en-us/cli/azure/ad/group#az-ad-group-show) command. The following command gets the object ID for the Microsoft Entra group named

*appdev*:

```
az ad group show --group appdev --query objectId -o tsv
```


Important

In some cases, such as Microsoft Entra guest users, the *user.name* in the account is different than the *userPrincipalName*.

```
$ az account show --query user.name -o tsv
user@contoso.com
$ az ad user list --query "[?contains(otherMails,'user@contoso.com')].{UPN:userPrincipalName}" -o tsv
user_contoso.com#EXT#@contoso.onmicrosoft.com
```


In this case, set the value of *ACCOUNT_UPN* to the *userPrincipalName* from the Microsoft Entra user. For example, if your account *user.name* is *user@contoso.com*, this action would look like the following example:

```
ACCOUNT_UPN=$(az ad user list --query "[?contains(otherMails,'user@contoso.com')].{UPN:userPrincipalName}" -o tsv)
```


## Get and verify the configuration information

Once the roles are assigned, use the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command to get the

*kubeconfig*definition for your AKS cluster. The following example gets the

*--admin*credentials, which works correctly if the user has been granted the

*Cluster Admin Role*:

```
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --admin
```


You can then use the [ kubectl config view](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#config) command to verify that the

*context*for the cluster shows that the admin configuration information has been applied.

```
$ kubectl config view
```


Your output should look similar to the following example output:

```
apiVersion: v1
clusters:
- cluster:
certificate-authority-data: DATA+OMITTED
server: https://myaksclust-myresourcegroup-19da35-4839be06.hcp.eastus.azmk8s.io:443
name: myAKSCluster
contexts:
- context:
cluster: myAKSCluster
user: clusterAdmin_myResourceGroup_myAKSCluster
name: myAKSCluster-admin
current-context: myAKSCluster-admin
kind: Config
preferences: {}
users:
- name: clusterAdmin_myResourceGroup_myAKSCluster
user:
client-certificate-data: REDACTED
client-key-data: REDACTED
token: e9f2f819a4496538b02cefff94e61d35
```


## Remove role permissions

To remove role assignments, use the [ az role assignment delete](/en-us/cli/azure/role/assignment#az-role-assignment-delete) command. Specify the account ID and cluster resource ID that you obtained in the previous steps. If you assigned the role to a group rather than a user, specify the appropriate group object ID rather than account object ID for the

`--assignee`

parameter.```
az role assignment delete --assignee $ACCOUNT_ID --scope $AKS_CLUSTER
```


## Next steps

For enhanced security on access to AKS clusters, [integrate Microsoft Entra authentication](azure-ad-integration-cli).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices-monitoring-proactive -->

# Proactive monitoring best practices for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article covers the best practices for proactive monitoring on Azure Kubernetes Service (AKS) and provides a comprehensive list of the key signals AKS recommends for you to monitor.

Proactively monitoring your AKS clusters is crucial for reducing downtime and saving business interruptions for your applications. This process involves identifying and monitoring key indicators of abnormal behavior in your cluster that might lead to major issues or downtime.

## Monitoring and alerting overview

Monitoring on AKS involves using metrics, logs, and events to ensure the health and performance of your cluster. Common scenarios to monitor include node performance, pod status, and overall resource utilization in your cluster. Logs provide insights into system events and cluster operations and activity. For more information about the methods and signals AKS provides for monitoring, see [Monitor Azure Kubernetes Service (AKS)](monitor-aks).

The best way to proactively monitor your cluster is to configure [Azure Monitor alerts](/en-us/azure/azure-monitor/alerts/alerts-overview). Alerts act as proactive measures to notify you of potential issues or anomalies before they escalate into critical problems. By defining thresholds for key metrics and logs, you receive immediate alerts when these signals exceed predefined limits, indicating potential issues like resource exhaustion or application failures. We highly recommend defining [service-level objectives (SLOs)](/en-us/azure/well-architected/reliability/metrics) for your application to measure the performance and reliability of your service. Configuring alerts on the key signals for your SLOs allows you to quickly detect any degradation of your application's quality of service that your customers receive. Overall, setting timely alerts enables you to quickly investigate and remediate problems, minimizing downtime and ensuring high availability of applications running on your AKS cluster.

## How to configure alerts on specific metric types

| Metric type | Where to find these metrics | How to configure alerts |
|---|---|---|
| AKS Platform Metric | View
|

[Create a metric alert for an Azure resource](/en-us/azure/azure-monitor/alerts/tutorial-metric-alert).[Azure Monitor and Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview).[Azure Monitor managed service for Prometheus rule groups](/en-us/azure/azure-monitor/essentials/prometheus-rule-groups).[Azure activity logs for AKS](monitor-aks#azure-activity-log).[Activity log alerts](/en-us/azure/azure-monitor/alerts/alerts-types#activity-log-alerts).**Settings > Properties**blade for your AKS cluster in the Azure portal.2. Select your

**infrastructure resource group**to view the infrastructure resources associated with your cluster.3. Select the

**Virtual Machine Scale Set instance**that matches the name of your node pool you're creating alerts for.4. Navigate to the

**Alerts**blade to create your metric alert.**Settings > Properties**blade for your AKS cluster in the Azure portal.2. Select your

**infrastructure resource group**to view the infrastructure resources associated with your cluster.3. Select the

**load balancer instance**to bring up the Azure portal page for load balancer.4. Navigate to the

**Alerts**page to create your load balancer metric alert.[Azure Monitor resource logs](monitor-aks#azure-monitor-resource-logs).[Create log search alerts from Container insights](/en-us/azure/azure-monitor/containers/container-insights-log-alerts).## Critical signals for configuring alerts

To get holistic coverage of your AKS environment, you need to configure alerts on the three main components of your cluster:

**Cluster infrastructure**: Alerts targeting the underlying infrastructure of your cluster such as nodes, disks, and networking.**Application health**: Alerts for monitoring the health of your pods and applications. Some common indicators of unhealthy applications include out-of-memory kills (OOMKills) of your pods, pods in not ready state, etc.**Kubernetes control plane**: Alerts on AKS control plane to monitor the health and performance of the API server, etcd, and other components.

The following sections contain the key signals which we recommend all AKS customers monitor closely. The AKS team is working to add all critical signals to the existing [Recommended Alerts](/en-us/azure/azure-monitor/containers/kubernetes-metric-alerts) feature, which allows you to easily enable alerts for all signals with a one-click experience. The Prometheus metrics alerts are available in Public Preview today, and the remaining alerts are estimated to be available in early 2025. For now, you can manually configure alerts on the critical signals.

### Cluster infrastructure alerts

| Alert scenario | Source | Signal | Recommended threshold |
|---|---|---|---|
| Cluster is in a failed state | Azure Activity Logs | Create or update managed cluster | Status of the log is Failed, indicating that the cluster upgrade or creation action failed. |
| Node pool is in a failed state | Azure Activity Logs | Create or update agent pool | Status of the log is Failed, indicating that the node pool is in a Failed state due to a failed Create, Read, Upgrade, or Delete (CRUD) operation. |
| High Node OS Disk Bandwidth Usage | Virtual Machine Scale Set Metric | OS Disk Bandwidth Consumed Percentage | Node OS disk bandwidth utilization is above 95%. |
| High Node OS Disk IOPS Usage | Virtual Machine Scale Set Metric | OS Disk IOPS Consumed Percentage | Node OS disk IOPS utilization is above 95%. |
| High Node OS Disk Space Usage | AKS Platform Metric | Disk Used Percentage | Node OS disk space percentage utilization is above 90%. |
| High Node CPU Usage | AKS Platform Metric | CPU Usage Percentage | Node CPU Usage is greater than 90%. |
| High Node Memory Usage | AKS Platform Metric | Memory Working Set Percentage | Node Memory Usage is greater than 90%. |
| Node is in NotReady state | AKS Platform Metric | Status for various node conditions | Node is in NotReady state for >20 minutes. |
| SNAT port exhaustion | Load Balancer (LB) Metric | SNAT Connection Count | Filter for Connection State = "Failed" |

### Application health alerts

| Alert scenario | Source | Signal | Recommended threshold |
|---|---|---|---|
| High number of unhealthy pods | Azure Managed Prometheus Metric | Alert name: KubePodReadyStateLow | Available as an AKS recommended alert. To enable this alert, see
|

[Recommended alert rules for Kubernetes clusters](/en-us/azure/azure-monitor/containers/kubernetes-metric-alerts?tabs=portal).[Recommended alert rules for Kubernetes clusters](/en-us/azure/azure-monitor/containers/kubernetes-metric-alerts?tabs=portal).### Kubernetes control plane alerts

| Alert scenario | Source | Signal | Recommended threshold |
|---|---|---|---|
| ETCD is Filled Up | Azure Managed Prometheus Metric | etcd_mvcc_db_total_size_in_use_in_bytes | ETCD utilization is greater than 2 GB |
| API Server Too Many Requests Errors | Azure Managed Prometheus Metric | apiserver_request_total | Filter for error code 429 |
| API Server Webhook and Tunnel Errors | Azure Managed Prometheus Metric | apiserver_request_total | Filter for error codes 500 and 503 |

## Next steps

For more information about monitoring on AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-azure-cni-pod-subnet -->

# Azure Container Networking Interface (CNI) Pod Subnet

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure CNI Pod Subnet assigns IP addresses to pods from a separate subnet from your cluster Nodes. This feature is available in two modes: Dynamic IP Allocation and Static Block Allocation.

## Prerequisites

Note

When using Static Block Allocation of CIDRs, exposing an application as a Private Link Service using a Kubernetes Load Balancer Service isn't supported.

- Review the
[prerequisites](configure-azure-cni#prerequisites)for configuring basic Azure CNI networking in AKS, as the same prerequisites apply to this article. - Review the
[deployment parameters](azure-cni-overview#deployment-parameters)for configuring basic Azure CNI networking in AKS, as the same parameters apply. - AKS Engine and DIY clusters aren't supported.
- Azure CLI version
`2.37.0`

or later and the`aks-preview`

extension version`2.0.0b2`

or later. - Register the subscription-level feature flag for your subscription: 'Microsoft.ContainerService/AzureVnetScalePreview'.

## Dynamic IP allocation mode

Dynamic IP allocation helps mitigate pod IP address exhaustion issues by allocating pod IPs from a subnet that's separate from the subnet hosting the AKS cluster.

The Dynamic IP Allocation mode offers the following benefits:

**Better IP utilization**: IPs are dynamically allocated to cluster Pods from the Pod subnet. This leads to better utilization of IPs in the cluster compared to the traditional CNI solution, which does static allocation of IPs for every node.**Scalable and flexible**: Node and pod subnets can be scaled independently. A single pod subnet can be shared across multiple node pools of a cluster or across multiple AKS clusters deployed in the same VNet. You can also configure a separate pod subnet for a node pool.**High performance**: Since pods are assigned VNet IPs, they have direct connectivity to other cluster pods and resources in the VNet. The solution supports very large clusters without any degradation in performance.**Separate VNet policies for pods**: Since pods have a separate subnet, you can configure separate VNet policies for them that are different from node policies. This enables many useful scenarios, such as allowing internet connectivity only for pods and not for nodes, fixing the source IP for pod in a node pool using an Azure NAT Gateway, and using network security groups (NSGs) to filter traffic between node pools.**Kubernetes network policies**: Both the Azure Network Policies and Calico work with this mode.

### Plan IP addressing

With Dynamic IP Allocation, nodes and pods scale independently, so you can plan their address spaces separately. Since pod subnets can be configured to the granularity of a node pool, you can always add a new subnet when you add a node pool. The system pods in a cluster/node pool also receive IPs from the pod subnet, so this behavior needs to be accounted for.

IPs are allocated to nodes in batches of 16. Pod subnet IP allocation should be planned with a minimum of 16 IPs per node in the cluster, as the nodes request 16 IPs on startup and request another batch of 16 anytime there are <8 IPs unallocated in their allotment.

IP address planning for Kubernetes services and Docker Bridge remain unchanged.

## Static block allocation mode

Static block allocation helps mitigate potential pod subnet sizing and Azure address mapping limitations by assigning CIDR blocks to nodes rather than individual IPs.

The Static Block Allocation mode offers the following benefits:

**Better IP scalability**: CIDR blocks are statically allocated to the cluster nodes and are present for the lifetime of the node, as opposed to the traditional dynamic allocation of individual IPs with traditional CNI. This enables routing based on CIDR blocks and helps scale the cluster limit up to 1 million pods from the traditional 65K pods per cluster. Your Azure Virtual Network must be large enough to accommodate the scale of your cluster.**Flexibility**: Node and pod subnets can be scaled independently. A single pod subnet can be shared across multiple node pools of a cluster or across multiple AKS clusters deployed in the same VNet. You can also configure a separate pod subnet for a node pool.**High performance**: Since pods are assigned virtual network IPs, they have direct connectivity to other cluster pods and resources in the VNet.**Separate VNet policies for pods**: Since pods have a separate subnet, you can configure separate VNet policies for them that are different from node policies. This enables many useful scenarios such as allowing internet connectivity only for pods and not for nodes, fixing the source IP for pod in a node pool using an Azure NAT Gateway, and using NSGs to filter traffic between node pools.**Kubernetes network policies**: Cilium, Azure NPM, and Calico work with this solution.

### Limitations

Below are some of the limitations of using Azure CNI Static Block allocation:

- Minimum Kubernetes Version required is 1.28.
- Maximum subnet size supported is x.x.x.x/12 ~ 1 million IPs.
- Only a single mode of operation can be used per subnet. If a subnet uses Static Block allocation mode, it cannot use Dynamic IP allocation mode in a different cluster or node pool with the same subnet and vice versa.
- Only supported in new clusters or when adding node pools with a different subnet to existing clusters. Migrating or updating existing clusters or node pools is not supported.
- Across all the CIDR blocks assigned to a node in the node pool, one IP will be selected as the primary IP of the node. Thus, for network administrators selecting the
`--max-pods`

value try to use the calculation below to best serve your needs and have optimal usage of IPs in the subnet:

`max_pods = (N * 16) - 1`

where `N`

is any positive integer and `N`

> 0

### Plan IP addressing

With Static Block Allocation, nodes and pods scale independently, so you can plan their address spaces separately. Since pod subnets can be configured to the granularity of a node pool, you can always add a new subnet when you add a node pool. The system pods in a cluster/node pool also receive IPs from the pod subnet, so this behavior needs to be accounted for.

CIDR blocks of /28 (16 IPs) are allocated to nodes based on your `--max-pods`

configuration for your node pool, which defines the maximum number of pods per node. 1 IP is reserved on each node from all the available IPs on that node for internal purposes.

While planning your IPs, it's important to define your `--max-pods`

configuration using the following calculation: `max_pods_per_node = (16 * N) - 1`

, where `N`

is any positive integer greater than `0`

.

Ideal values with no IP wastage would require the max pods value to conform to the above expression.

See the following example cases:

Note

The examples assume /28 CIDR blocks (16 IPs each).

| Example case | `max_pods` |
CIDR Blocks allocated per node | Total IP available for pods | IP wastage for node |
|---|---|---|---|---|
| Low wastage (acceptable) | 30 | 2 | (16 * 2) - 1 = 32 - 1 = 31 | 31 - 30 = 1 |
| Ideal case | 31 | 2 | (16 * 2) - 1 = 32 - 1 = 31 | 31 - 31 = 0 |
| High wastage (not recommended) | 32 | 3 | (16 * 3) - 1 = 48 - 1 = 47 | 47 - 32 = 15 |

IP address planning for Kubernetes services remains unchanged.

Note

Ensure your VNet has a sufficiently large and contiguous address space to support your cluster's scale.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/spark-job -->

# Add-ons, extensions, and other integrations with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) provides extra functionality for your clusters using add-ons and extensions. Open-source projects and third parties provide by more integrations that are commonly used with AKS. The [AKS support policy](support-policies) doesn't support the open-source and third-party integrations.

## Add-ons

Add-ons are a fully supported way to provide extra capabilities for your AKS cluster. The installation, configuration, and lifecycle of add-ons are managed on AKS. You can use the [ az aks enable-addons](/en-us/cli/azure/aks#az-aks-enable-addons) command to install an add-on or manage the add-ons for your cluster.

AKS uses the following rules for applying updates to installed add-ons:

- Only an add-on's patch version can be upgraded within a Kubernetes minor version. The add-on's major/minor version isn't upgraded within the same Kubernetes minor version.
- The major/minor version of the add-on is only upgraded when moving to a later Kubernetes minor version.
- Any breaking or behavior changes to the add-on are announced well before, usually 60 days, for a GA minor version of Kubernetes on AKS.
- You can patch add-ons weekly with every new release of AKS, which is announced in the release notes. You can control AKS releases using the
[maintenance windows](planned-maintenance)and[release tracker](release-tracker).

### Exceptions

- Add-ons are upgraded to a new major/minor version (or breaking change) within a Kubernetes minor version if either the cluster's Kubernetes version or the add-on version are in preview.
- There can be unavoidable circumstances, such as CVE security patches or critical bug fixes, when you need to update an add-on within a GA minor version.

### Available add-ons

| Name | Description | Articles | GitHub |
|---|---|---|---|
| ingress-appgw | Use Application Gateway Ingress Controller with your AKS cluster. |
|

[GitHub](https://github.com/Azure/application-gateway-kubernetes-ingress)[Simplified application autoscaling with Kubernetes Event-driven Autoscaling (KEDA) add-on](keda-about)[GitHub](https://github.com/Azure-Samples/aks-keda-addon-workload-identity)[Container insights overview](/en-us/azure/azure-monitor/containers/container-insights-overview)[Managed Prometheus overview](/en-us/azure/azure-monitor/containers/container-insights-overview)[GitHub](https://github.com/Azure/AKS)[GitHub](https://github.com/Azure/prometheus-collector)[Understand Azure Policy for Kubernetes clusters](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks)[GitHub](https://github.com/Azure/azure-policy)[Use the Azure Key Vault Provider for Secrets Store CSI Driver in an AKS cluster](csi-secrets-store-driver)[GitHub](https://github.com/Azure/secrets-store-csi-driver-provider-azure)[Use virtual nodes](virtual-nodes)[GitHub](https://github.com/virtual-kubelet/virtual-kubelet)[Open Service Mesh AKS add-on (retired)](open-service-mesh-about)[GitHub](https://github.com/Azure/osm-azure)## Extensions

Cluster extensions build on top of certain Helm charts and provide an Azure Resource Manager-driven experience for installation and lifecycle management of different Azure capabilities on top of your Kubernetes cluster.

- For more information on the specific cluster extensions for AKS, see
[Deploy and manage cluster extensions for Azure Kubernetes Service (AKS)](cluster-extensions?tabs=azure-cli). - For more information on available cluster extensions, see
[Currently available extensions](cluster-extensions?tabs=azure-cli#currently-available-extensions).

### Difference between extensions and add-ons

Extensions and add-ons are both supported ways to add functionality to your AKS cluster. When you install an add-on, the functionality is added as part of the AKS resource provider in the Azure API. When you install an extension, the functionality is added as part of a separate resource provider in the Azure API.

## GitHub Actions

GitHub Actions help you automate your software development workflows from within GitHub.

- For more information on using GitHub Actions with Azure, see
[GitHub Actions for Azure](/en-us/azure/developer/github/github-actions). - For an example of using GitHub Actions with an AKS cluster, see
[Build, test, and deploy containers to Azure Kubernetes Service using GitHub Actions](kubernetes-action).

## Open-source and third-party integrations

There are many open-source and third-party integrations you can install on your AKS cluster. The [AKS support policy](support-policies) doesn't cover self-managed installations of the following projects. Some of these projects have managed experiences built on top of them (for example in the case of Prometheus, Grafana, and Istio). These managed experiences are noted in the 'More Details' column.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

| Name | Description | More details |
|---|---|---|
|

[Quickstart: Develop on Azure Kubernetes Service (AKS) with Helm](quickstart-helm)[Prometheus](https://prometheus.io/)[Azure Monitor managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview); Self-managed experience -[Prometheus operator](https://github.com/prometheus-operator/kube-prometheus)[Grafana](https://grafana.com/)[Azure Managed Grafana](/en-us/azure/managed-grafana/overview); Self-managed experience -[Deploy Grafana on Kubernetes](https://grafana.com/docs/grafana/latest/installation/kubernetes/).[Couchbase](https://www.couchbase.com/)[Install Couchbase and the Operator on AKS](https://docs.couchbase.com/operator/2.4/tutorial-aks.html)[OpenFaaS](https://www.openfaas.com/)[Use OpenFaaS with AKS](openfaas)[Apache Spark](https://spark.apache.org/)*Standard_D3_v2*. For more information on running Spark jobs on Kubernetes, see the[running Spark on Kubernetes](https://spark.apache.org/docs/latest/running-on-kubernetes.html)guide.[Istio](https://istio.io/)[Istio add-on for AKS](istio-about); Self-managed experience -[Istio open-source installation](https://istio.io/latest/docs/setup/install/)[Linkerd](https://linkerd.io/)[Linkerd Getting Started](https://linkerd.io/2.16/getting-started/)[Consul](https://www.consul.io/)[Getting Started with Consul Service Mesh for Kubernetes](https://learn.hashicorp.com/tutorials/consul/service-mesh-deploy)### Third-party integrations for Windows containers

Microsoft collaborates with partners to ensure the build, test, deployment, configuration, and monitoring of your applications perform optimally with Windows containers on AKS.

For more information, see [Windows AKS partner solutions](windows-aks-partner-solutions).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/integrations -->

# Add-ons, extensions, and other integrations with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) provides extra functionality for your clusters using add-ons and extensions. Open-source projects and third parties provide by more integrations that are commonly used with AKS. The [AKS support policy](support-policies) doesn't support the open-source and third-party integrations.

## Add-ons

Add-ons are a fully supported way to provide extra capabilities for your AKS cluster. The installation, configuration, and lifecycle of add-ons are managed on AKS. You can use the [ az aks enable-addons](/en-us/cli/azure/aks#az-aks-enable-addons) command to install an add-on or manage the add-ons for your cluster.

AKS uses the following rules for applying updates to installed add-ons:

- Only an add-on's patch version can be upgraded within a Kubernetes minor version. The add-on's major/minor version isn't upgraded within the same Kubernetes minor version.
- The major/minor version of the add-on is only upgraded when moving to a later Kubernetes minor version.
- Any breaking or behavior changes to the add-on are announced well before, usually 60 days, for a GA minor version of Kubernetes on AKS.
- You can patch add-ons weekly with every new release of AKS, which is announced in the release notes. You can control AKS releases using the
[maintenance windows](planned-maintenance)and[release tracker](release-tracker).

### Exceptions

- Add-ons are upgraded to a new major/minor version (or breaking change) within a Kubernetes minor version if either the cluster's Kubernetes version or the add-on version are in preview.
- There can be unavoidable circumstances, such as CVE security patches or critical bug fixes, when you need to update an add-on within a GA minor version.

### Available add-ons

| Name | Description | Articles | GitHub |
|---|---|---|---|
| ingress-appgw | Use Application Gateway Ingress Controller with your AKS cluster. |
|

[GitHub](https://github.com/Azure/application-gateway-kubernetes-ingress)[Simplified application autoscaling with Kubernetes Event-driven Autoscaling (KEDA) add-on](keda-about)[GitHub](https://github.com/Azure-Samples/aks-keda-addon-workload-identity)[Container insights overview](/en-us/azure/azure-monitor/containers/container-insights-overview)[Managed Prometheus overview](/en-us/azure/azure-monitor/containers/container-insights-overview)[GitHub](https://github.com/Azure/AKS)[GitHub](https://github.com/Azure/prometheus-collector)[Understand Azure Policy for Kubernetes clusters](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks)[GitHub](https://github.com/Azure/azure-policy)[Use the Azure Key Vault Provider for Secrets Store CSI Driver in an AKS cluster](csi-secrets-store-driver)[GitHub](https://github.com/Azure/secrets-store-csi-driver-provider-azure)[Use virtual nodes](virtual-nodes)[GitHub](https://github.com/virtual-kubelet/virtual-kubelet)[Open Service Mesh AKS add-on (retired)](open-service-mesh-about)[GitHub](https://github.com/Azure/osm-azure)## Extensions

Cluster extensions build on top of certain Helm charts and provide an Azure Resource Manager-driven experience for installation and lifecycle management of different Azure capabilities on top of your Kubernetes cluster.

- For more information on the specific cluster extensions for AKS, see
[Deploy and manage cluster extensions for Azure Kubernetes Service (AKS)](cluster-extensions?tabs=azure-cli). - For more information on available cluster extensions, see
[Currently available extensions](cluster-extensions?tabs=azure-cli#currently-available-extensions).

### Difference between extensions and add-ons

Extensions and add-ons are both supported ways to add functionality to your AKS cluster. When you install an add-on, the functionality is added as part of the AKS resource provider in the Azure API. When you install an extension, the functionality is added as part of a separate resource provider in the Azure API.

## GitHub Actions

GitHub Actions help you automate your software development workflows from within GitHub.

- For more information on using GitHub Actions with Azure, see
[GitHub Actions for Azure](/en-us/azure/developer/github/github-actions). - For an example of using GitHub Actions with an AKS cluster, see
[Build, test, and deploy containers to Azure Kubernetes Service using GitHub Actions](kubernetes-action).

## Open-source and third-party integrations

There are many open-source and third-party integrations you can install on your AKS cluster. The [AKS support policy](support-policies) doesn't cover self-managed installations of the following projects. Some of these projects have managed experiences built on top of them (for example in the case of Prometheus, Grafana, and Istio). These managed experiences are noted in the 'More Details' column.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

| Name | Description | More details |
|---|---|---|
|

[Quickstart: Develop on Azure Kubernetes Service (AKS) with Helm](quickstart-helm)[Prometheus](https://prometheus.io/)[Azure Monitor managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview); Self-managed experience -[Prometheus operator](https://github.com/prometheus-operator/kube-prometheus)[Grafana](https://grafana.com/)[Azure Managed Grafana](/en-us/azure/managed-grafana/overview); Self-managed experience -[Deploy Grafana on Kubernetes](https://grafana.com/docs/grafana/latest/installation/kubernetes/).[Couchbase](https://www.couchbase.com/)[Install Couchbase and the Operator on AKS](https://docs.couchbase.com/operator/2.4/tutorial-aks.html)[OpenFaaS](https://www.openfaas.com/)[Use OpenFaaS with AKS](openfaas)[Apache Spark](https://spark.apache.org/)*Standard_D3_v2*. For more information on running Spark jobs on Kubernetes, see the[running Spark on Kubernetes](https://spark.apache.org/docs/latest/running-on-kubernetes.html)guide.[Istio](https://istio.io/)[Istio add-on for AKS](istio-about); Self-managed experience -[Istio open-source installation](https://istio.io/latest/docs/setup/install/)[Linkerd](https://linkerd.io/)[Linkerd Getting Started](https://linkerd.io/2.16/getting-started/)[Consul](https://www.consul.io/)[Getting Started with Consul Service Mesh for Kubernetes](https://learn.hashicorp.com/tutorials/consul/service-mesh-deploy)### Third-party integrations for Windows containers

Microsoft collaborates with partners to ensure the build, test, deployment, configuration, and monitoring of your applications perform optimally with Windows containers on AKS.

For more information, see [Windows AKS partner solutions](windows-aks-partner-solutions).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/configure-static-egress-gateway -->

# Configure Static Egress Gateway in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Static Egress Gateway in AKS provides a streamlined solution for configuring fixed source IP addresses for outbound traffic from your AKS workloads. This feature allows you to route egress traffic through a dedicated "gateway node pool". By using the Static Egress Gateway, you can efficiently manage and control outbound IP addresses and ensure that your AKS workloads can communicate with external systems securely and consistently, using predefined IPs.

This article provides step-by-step instructions to set up a Static Egress Gateway node pool in your AKS cluster, enabling you to configure fixed source IP addresses for outbound traffic from your Kubernetes workloads.

## Limitations and considerations

Static Egress Gateway isn't supported in clusters with

[Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet).Kubernetes network policies won't apply to traffic leaving the cluster through the gateway node pool.

- This shouldn't affect cluster traffic control as
**only**egress traffic from annotated pods**routed to the gateway node pool**are affected.

- This shouldn't affect cluster traffic control as
The gateway node pool isn't intended for general-purpose workloads and should be used for egress traffic only.

Windows node pools can't be used as gateway node pools.

hostNetwork pods

**cannot**be annotated to use the gateway node pool.Pods can only use a gateway node pool if they are in the same namespace as the

`StaticGatewayConfiguration`

resource.

## Create or update an AKS cluster with Static Egress Gateway

Before you can create and manage gateway node pools, you must enable the Static Egress Gateway feature for your AKS cluster. You can do this when creating a new cluster or by updating an existing cluster using `az aks update`

.

```
az aks create -n <cluster-name> -g <resource-group> --enable-static-egress-gateway
```


## Create a Gateway Node pool

After enabling the feature, create a dedicated gateway node pool. This node pool handles the egress traffic through the specified public IP prefix. The `--gateway-prefix-size`

is the size of the public IP prefix to be applied to the gateway node pool nodes. The allowed range is `28`

-`31`

.

```
az aks nodepool add --cluster-name <cluster-name> \
--name <nodepool-name> \
--resource-group <resource-group> \
--mode gateway \
--node-count <number-of-nodes> \
--gateway-prefix-size <prefix-size>
```


Note

- The number of nodes must fit within the capacity allowed by the selected prefix size. For example, a /30 prefix supports up to 4 nodes, and at least 2 nodes are required for high availability. Since you can’t adjust the node count dynamically, plan your nodes according to the fixed limit set by the prefix size.
- You can define the SKU of the VM to use in your gateway node pool with the
`--vm-size`

parameter. You should understand your specific needs and plan accordingly to ensure the right performance and cost balance.

## Scale the Gateway Node pool (Optional)

If necessary, you can resize the gateway node pool within the limits defined by the prefix size but it doesn't support autoscaling.

```
az aks nodepool scale --cluster-name <cluster-name> -n <nodepool-name> --node-count <desired-node-count>
```


## Create a Static Gateway Configuration

Define the gateway configuration by creating a `StaticGatewayConfiguration`

custom resource. This configuration specifies which node pool and public IP prefix to use.

```
apiVersion: egressgateway.kubernetes.azure.com/v1alpha1
kind: StaticGatewayConfiguration
metadata:
name: <gateway-config-name>
namespace: <namespace>
spec:
gatewayNodepoolName: <nodepool-name>
excludeCidrs: # Optional
- 10.0.0.0/8
- 172.16.0.0/12
- 169.254.169.254/32
publicIpPrefixId: /subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.Network/publicIPPrefixes/<prefix-name> # Optional
```


Tip

If you don't set `publicIpPrefixId`

, a public IP prefix will be created for you automatically. When running `kubectl describe StaticGatewayConfiguration <gateway-config-name> -n <namespace>`

, you can see the "Egress Ip Prefix" in the status. This is the newly created public IP prefix. You can also use an existing public IP prefix by specifying its resource ID in the `publicIpPrefixId`

argument. You need to grant "Network Contributor" role to AKS cluster's identity in this case.

### Static Private IP Support (Preview)

Important

Static private IP support requires clusters running Kubernetes version 1.34 or later and a subscription with the `Microsoft.ContainerService/StaticEgressGatewayPreview`

Azure Feature Exposure Control (AFEC) flag enabled. Follow [Register preview feature](/en-us/azure/azure-resource-manager/management/preview-features#register-preview-feature) to request the feature flag before creating the Gateway VirtualMachines node pool.

If you must keep egress traffic on private addresses, enable private IP support on the gateway node pool. Use the same `az aks nodepool add`

command and set the node pool to use the VirtualMachines VM set type while disabling public IP provisioning:

```
az aks nodepool add --cluster-name <cluster-name> \
--name <nodepool-name> \
--resource-group <resource-group> \
--mode gateway \
--node-count <number-of-nodes> \
--vm-set-type VirtualMachines \
--gateway-prefix-size <prefix-size>
```


In this configuration, the `provisionPublicIps=false`

setting keeps the private IPs allocated to the gateway nodes for the lifetime of the `StaticGatewayConfiguration`

. When you run `kubectl describe StaticGatewayConfiguration <gateway-config-name> -n <namespace>`

, the `egressIpPrefix`

field shows a comma-separated list of those static private IPs. You continue to use the same APIs and manifests for the rest of the workflow, including the `StaticGatewayConfiguration`

resource and the pod annotations.

## Annotate Pods to Use the Gateway Configuration

To route traffic from specific pods through the gateway node pool, annotate the pod template in the deployment configuration.

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: <deployment-name>
namespace: <namespace>
spec:
template:
metadata:
annotations:
kubernetes.azure.com/static-gateway-configuration: <gateway-config-name>
```


Note

The CNI plugin on each node will automatically configure the pod to route its traffic through the selected gateway nodepool.

## Monitor and Manage Gateway Configurations

Once deployed, you can monitor the status of your gateway configurations through the AKS cluster. The status section in the `StaticGatewayConfiguration`

resource is updated with details such as assigned IPs and WireGuard configurations.

## Delete a Gateway Node pool (Optional)

To remove a gateway node pool, ensure all associated configurations are appropriately handled before deletion.

```
az aks nodepool delete --cluster-name <cluster-name> -n <nodepool-name>
```


## Disable the Static Egress Gateway Feature (Optional)

If you no longer need the Static Egress Gateway, you can disable the feature and uninstall the operator. Ensure all gateway node pools are deleted first.

```
az aks update -n <cluster-name> -g <resource-group> --disable-static-egress-gateway
```


By following these steps, you can effectively set up and manage Static Egress Gateway configurations in your AKS cluster, enabling controlled and consistent egress traffic from your workloads.
