---
merged_at: 2026-01-25T12:06:27.729904
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: advanced-container-networking-services-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/advanced-container-networking-services-overview -->

# Advanced Container Networking Services for Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Advanced Container Networking Services is a suite of services designed to enhance the networking capabilities of Azure Kubernetes Service (AKS) clusters. Advanced Container Networking Services offers the following key feature sets: [ Container Network Observability](#container-network-observability),

[, and](#container-network-security)

**Container Network Security**[. These features provide deep insights into network traffic, strengthen security measures, and optimize network performance for containerized applications running in AKS.](#container-network-performance)

**Container Network Performance**## Container Network Observability

Container Network Observability provides deep insights into network traffic and performance across containerized environments. This feature set **works across both Cilium and non-Cilium data planes**, offering flexibility for diverse networking needs. The feature uses eBPF to enhance scalability and performance by identifying potential bottlenecks and network congestion before applications are affected.

Key benefits of Container Network Observability include:

- Compatibility with all Container Networking Interface (CNI) variants in Azure.
, including node-level metrics and Hubble metrics for detailed network insights.*Container network metrics*- Hubble metrics for Domain Name System (DNS) resolution, pod-to-pod communication, and service interactions.
that capture essential metadata such as IPs, ports, and traffic flow for troubleshooting, monitoring, and security enforcement.*Container network logs*- Integration with the managed service for Prometheus in Azure Monitor and Azure Managed Grafana for simplified metrics storage and visualization.

### Container network metrics

This feature collects node-level metrics, including CPU, memory, and network performance, to monitor the health of cluster nodes. For deeper insights, Hubble metrics provide data on DNS resolution times, service-to-service communication, and pod-level network behavior. These metrics help you analyze application performance, detect anomalies, and optimize workloads.

For more information, see the [metrics overview](container-network-observability-metrics).

### Container network logs

Container network logs give you detailed insight into traffic within and across clusters by capturing metadata like source and destination IP addresses, ports, protocols, and flow direction. These logs enable monitoring network behavior, troubleshooting connectivity issues, and enforcing security policies. Persistent and real-time logging options ensure comprehensive, actionable network observability.

For more information, see the [container network logs overview](container-network-observability-logs).

## Container Network Security

Container Network Security enhances the security posture of AKS clusters by providing advanced network security features. It leverages eBPF technology to enforce network policies at the kernel level, ensuring efficient and effective security controls for containerized applications. **Container Network Security is available only on clusters with Azure CNI Powered by Cilium**.

### FQDN-based filtering

FQDN-based filtering allows you to create network policies based on fully qualified domain names (FQDNs) rather than IP addresses. This capability simplifies policy management, especially in dynamic environments where IP addresses frequently change. By using FQDNs, you can ensure that your applications communicate only with trusted external services, enhancing security and compliance.

For more information, see the [FQDN-based filtering overview](container-network-security-fqdn-filtering-concepts).

### Layer 7 policy

Layer 7 policy enables application-layer traffic control, allowing you to define policies based on specific application protocols. This feature provides granular control over network traffic, enabling you to enforce security policies that align with application behavior. With Layer 7 policy, you can monitor and restrict traffic based on HTTP methods, URLs, headers, and other application-level attributes.

For more information, see the [Layer 7 policy overview](container-network-security-l7-policy-concepts).

### WireGuard Encryption (preview)

WireGuard Encryption leverages the WireGuard protocol to provide secure, encrypted communication between Cilium-managed endpoints within your AKS cluster. This feature ensures that data transmitted over the network is protected from eavesdropping and tampering, enhancing the overall security of your containerized applications.

For more information, see the [WireGuard encryption overview](container-network-security-wireguard-encryption-concepts).

## Container Network Performance

Container Network Performance optimizes network performance for containerized applications running in AKS clusters. It leverages eBPF technology to enhance network routing and reduce latency, ensuring that applications can communicate efficiently and effectively. **Container Network Performance is available only on clusters with Azure CNI Powered by Cilium**.

### eBPF Host Routing

eBPF Host Routing uses extended Berkeley Packet Filter (eBPF) technology to optimize traffic flow in AKS clusters.

For more information, see the [eBPF Host Routing overview](container-network-performance-ebpf-host-routing).


---

<!-- DOCUMENTO FUSIONADO: use-oidc-issuer.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-oidc-issuer -->

# Create an OpenID Connect provider on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to create and manage an OpenID Connect (OIDC) provider for your Azure Kubernetes Service (AKS) cluster. The OIDC issuer allows your AKS cluster to integrate with identity providers like Microsoft Entra ID, enabling secure authentication and single sign-on (SSO) capabilities for applications running within the cluster.

## About OpenID Connect (OIDC) on AKS

[OpenID Connect](/en-us/azure/active-directory/fundamentals/auth-oidc) (OIDC) extends the OAuth 2.0 authorization protocol for use as another authentication protocol issued by Microsoft Entra ID. You can use OIDC to enable single sign-on (SSO) between OAuth-enabled applications on your Azure Kubernetes Service (AKS) cluster using a security token called an ID token. You can enable the OIDC issuer on your AKS clusters, which allows Microsoft Entra ID (or another cloud provider's identity and access management platform) to discover the API server's public signing keys.

## Prerequisites

**Platform requirements**:

- Azure CLI version 2.42.0+ (
`az --version`

to check version,[install or upgrade Azure CLI](/en-us/cli/azure/install-azure-cli)if needed) - Minimum Kubernetes version is 1.22+

**Version-specific behavior**:

- OIDC issuer enabled by default (no
`--enable-oidc-issuer`

flag needed) for Kubernetes version 1.34+ - Token auto-extension disabled (
`--service-account-extend-token-expiration=false`

) for Kubernetes version 1.30.0+ - Manual enablement required if not previously configured for Kubernetes version earlier than 1.34

**Important considerations**:

- You can't disable OIDC issuer once enabled
- Enabling OIDC issuer on existing clusters requires API server restart (brief downtime)
- Maximum token lifetime is 24 hours (one day)
- Projected service account tokens required for Kubernetes 1.30+ clusters

## Create an AKS cluster with the OIDC issuer

Create an AKS cluster using the

command with the`az aks create`

`--enable-oidc-issuer`

parameter.`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Create the AKS cluster with OIDC issuer enabled (OIDC issuer enabled by default for Kubernetes 1.34+) az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --node-count 1 \ --enable-oidc-issuer \ --generate-ssh-keys`


## Enable the OIDC issuer on an existing AKS cluster

Enable the OIDC issuer on an existing AKS cluster using the

command with the`az aks update`

`--enable-oidc-issuer`

parameter.`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Enable the OIDC issuer on the existing AKS cluster az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-oidc-issuer`


## Get the OIDC issuer URL

Get the OIDC issuer URL using the

command.`az aks show`

`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Get the OIDC issuer URL az aks show \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --query "oidcIssuerProfile.issuerUrl" \ -o tsv`

By default, the issuer is set to use the base URL

`https://{region}.oic.prod-aks.azure.com`

, where the value for`{region}`

matches the location the AKS cluster is deployed in.

## Rotate the OIDC key

Important

Keep the following considerations in mind when rotating the OIDC key:

- If you want to invalidate the old key immediately after key rotation, you must rotate the OIDC key twice and restart the pods using projected service account tokens.
- Both old and new keys remain valid for 24 hours after rotation.
- Manual token refresh required every 24 hours (unless using
[Azure Identity SDK](workload-identity-overview#azure-identity-client-libraries), which rotates automatically).

Rotate the OIDC key using the

command.`az aks oidc-issuer`

`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Rotate the OIDC signing keys az aks oidc-issuer rotate-signing-keys \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP`


## Get the discovery document

Navigate to your

[OIDC issuer URL](#get-the-oidc-issuer-url)in your browser and append`/.well-known/openid-configuration`

to the URL. For example:`https://eastus.oic.prod-aks.azure.com/.well-known/openid-configuration`

.Your output should resemble the following example output:

`{ "issuer": "https://eastus.oic.prod-aks.azure.com/ffffffff-eeee-dddd-cccc-bbbbbbbbbbb0/00000000-0000-0000-0000-000000000000/", "jwks_uri": "https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/00000000-0000-0000-0000-000000000000/openid/v1/jwks", "response_types_supported": [ "id_token" ], "subject_types_supported": [ "public" ], "id_token_signing_alg_values_supported": [ "RS256" ] }`


## Get the JWK Set document

Navigate to the

in your browser. For example:**jwks_uri**from the discovery document`https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/00000000-0000-0000-0000-000000000000/openid/v1/jwks`

.Your output should resemble the following example output:

`{ "keys": [ { "use": "sig", "kty": "RSA", "kid": "xxx", "alg": "RS256", "n": "xxxx", "e": "AQAB" }, { "use": "sig", "kty": "RSA", "kid": "xxx", "alg": "RS256", "n": "xxxx", "e": "AQAB" } ] }`

Note

During key rotation, there's one other key present in the discovery document.
