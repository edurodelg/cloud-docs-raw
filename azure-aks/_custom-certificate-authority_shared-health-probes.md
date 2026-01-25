---
merged_at: 2026-01-25T12:25:33.871583
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: custom-certificate-authority.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/custom-certificate-authority -->

# Use custom certificate authorities (CAs) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Custom Certificate Authority (CA) allows you to add up to 10 base64-encoded certificates to your node's trust store. This feature is often needed when certificate authorities (CAs) are required to be present on the node, like when connecting to a private registry.

This article shows you how to create custom CAs and apply them to your AKS clusters.

Note

The Custom CA feature adds your custom certificates to the trust store of the AKS node. Certificates added with this feature aren't available to containers running in pods. If you need the certificates inside containers, you need to add them separately by adding them to the image used by your pods or at runtime via scripting and a secret.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/free). - Azure CLI version 2.72.0 or later installed and configured. To find your CLI version, run the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - A base64 encoded certificate string or a text file with certificate.

## Limitations

- Windows node pools aren't supported.
- Installing different CAs in the same cluster isn't supported.

## Create a certificate file

Create a text file containing up to 10 blank line separated certificates. When you pass this file to your cluster, the certificates are installed in the trust stores of the AKS node.

Example text file:

`-----BEGIN CERTIFICATE----- cert1 -----END CERTIFICATE----- -----BEGIN CERTIFICATE----- cert2 -----END CERTIFICATE-----`


**Before proceeding to the next step, make sure that there are no blank spaces in your text file to avoid errors**.

## Pass custom CAs to your AKS cluster

Pass certificates to your cluster using the

or`az aks create`

command with`az aks update`

`--custom-ca-trust-certificates`

set to the name of your certificate file.`# Create a new cluster az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --node-count 2 \ --custom-ca-trust-certificates <path-to-certificate-file> \ --generate-ssh-keys # Update an existing cluster az aks update \ --resource-group <resource-group-name> \ --name <cluster-name> \ --custom-ca-trust-certificates <path-to-certificate-file>`

Note

This operation triggers a model update to ensure all existing nodes have the same CAs installed for correct provisioning. AKS creates new nodes, drains existing nodes, deletes existing nodes, and replaces them with nodes that have the new set of CAs installed.


## Verify CAs are installed

Verify the CAs are installed using the

command.`az aks show`

`az aks show --resource-group <resource-group-name> --name <cluster-name> | grep securityProfile -A 4`

In the output, the

`securityProfile`

section should include your custom CA certificates. For example:`"securityProfile": { "azureKeyVaultKms": null, "customCaTrustCertificates": [ "values"`


## Resolve custom CA formatting errors

Adding certificates to a cluster can result in an error if the file with the certificates isn't formatted properly. You might see an error similar to the following example:

```
failed to decode one of SecurityProfile.CustomCATrustCertificates to PEM after base64 decoding
```


If you encounter this error, you should check that your input file has no extra new lines, white spaces, or data other than correctly formatted certificates as shown in the example file.

## Resolve custom CA X.509 Certificate Signed by Unknown Authority errors

AKS requires certificates passed to be properly formatted and base64 encoded. Make sure the CAs you passed are properly base64 encoded and that files with CAs don't have CRLF line breaks.

## Restart containerd to pick up new certificates

If containerd doesn't pick up new certificates, run the `systemctl restart containerd`

command from the node's shell. Once containerd restarts, the container runtime should pick up the new certificates.

## Related content

For more information on AKS security best practices, see [Best practices for cluster security and upgrades in Azure Kubernetes Service (AKS)](operator-best-practices-cluster-security).


---

<!-- DOCUMENTO FUSIONADO: shared-health-probes.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/shared-health-probes -->

# Use shared health probes for externalTrafficPolicy: Cluster Services (preview) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

# Use shared health probes for

This article describes how to enable **shared health probe mode** (preview) for Services with `externalTrafficPolicy: Cluster`

in Azure Kubernetes Service (AKS). Shared probe mode improves load balancer efficiency, reduces configuration complexity, and provides more accurate node health monitoring.

## About shared health probe mode

In clusters that use `externalTrafficPolicy: Cluster`

, Azure Standard Load Balancer (SLB) currently creates a *separate probe per Service* and targets each Service's `nodePort`

.

This design means SLB infers node health from whichever **application pod** answers the probe. As clusters grow, this approach leads to several issues, including:

**Configuration drift and blind spots**: SLB can't detect a failed or misconfigured`kube‑proxy`

if iptables rules are still present.**Duplicate health logic**: Readiness must be defined twice. Once in each pod's`readinessProbe`

, and again through SLB annotations.**Operational overhead**: Each Service on each node is probed every*five seconds*, consuming connections, SNAT ports, and SLB rule space.**Feature friction**: Customers can't set`allocateLoadBalancerNodePorts=false`

, and workloads like Istio or ingress‑nginx require extra annotations to keep probes working.**Troubleshooting confusion**: An unhealthy app, Network Policy rule, or scale‑to‑zero event can make an*entire node*appear down.

**Shared probe mode** solves these problems by moving to a *single HTTP probe* for all `externalTrafficPolicy: Cluster`

Services. In shared probe mode:

- SLB probes
`http://<node‑ip>:10356/healthz`

, the standard`kube‑proxy`

health endpoint. - A lightweight sidecar runs next to
`kube‑proxy`

to relay the probe and handle PROXY protocol when Private Link Service is enabled.

## Benefits of shared probe mode

The following table outlines **key benefits** of using shared probe mode:

| Benefit | Why it matters |
|---|---|
| Accurate node health | SLB now measures `kube‑proxy` directly, not an arbitrary backend pod. |
| Simpler configuration | No per‑Service probe annotations; readiness lives solely in the pod spec. |
| Lower traffic overhead | One probe per node instead of Services × (nodes – 1) probes. |

Note

Keep the following information in mind when using shared probe mode:

- Services that use
`externalTrafficPolicy: Local`

are**unchanged**. - This feature does
**not**address container‑native load balancing.

## Before you begin

[Install or update the](#install-or-update-the-aks-preview-azure-cli-extension).`aks-preview`

Azure CLI extension[Register the](#register-the-enableslbsharedhealthprobepreview-feature-flag).`EnableSLBSharedHealthProbePreview`

feature flag in your Azure subscription

### Install or update the `aks-preview`

Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the

`aks-preview`

extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the

`aks-preview`

extension using thecommand.`az extension update`

`az extension update --name aks-preview`


### Register the `EnableSLBSharedHealthProbePreview`

feature flag

Register the

`EnableSLBSharedHealthProbePreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "EnableSLBSharedHealthProbePreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command:`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "EnableSLBSharedHealthProbePreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`
