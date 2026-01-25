---
merged_at: 2026-01-25T12:25:33.928199
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: csi-secrets-store-driver.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/csi-secrets-store-driver -->

# Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Key Vault provider for Secrets Store CSI Driver allows for the integration of an Azure Key Vault as a secret store with an Azure Kubernetes Service (AKS) cluster via a [CSI volume](https://kubernetes-csi.github.io/docs/).

## Features

- Mounts secrets, keys, and certificates to a pod using a CSI volume.
- Supports CSI inline volumes.
- Supports mounting multiple secrets store objects as a single volume.
- Supports pod portability with the
`SecretProviderClass`

CRD. - Supports Windows containers.
- Syncs with Kubernetes secrets.
- Supports autorotation of mounted contents and synced Kubernetes secrets.

## Limitations

- A container using a
`ConfigMap`

or`Secret`

as a`subPath`

volume mount does not receive automated updates when the secret is rotated. This is a Kubernetes limitation. To have the changes take effect, the application needs to reload the changed file by either watching for changes in the file system or by restarting the pod. For more information, see[Secrets Store CSI Driver known limitations](https://secrets-store-csi-driver.sigs.k8s.io/known-limitations.html#secrets-not-rotated-when-using-subpath-volume-mount). - The add-on creates a managed identity named
`azurekeyvaultsecretsprovider-xxx`

in the node resource group and assigns it to the Virtual Machine Scale Sets (VMSS) automatically. You can use this managed identity or your own managed identity to access the key vault. It's not supported to prevent creation of the identity.

## Prerequisites

- If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - Check that your version of the Azure CLI is 2.30.0 or later. If it's an earlier version,
[install the latest version](/en-us/cli/azure/install-azure-cli).

### Network

- If using network isolated clusters, it's recommended to
[set up private endpoint to access Azure Key Vault](/en-us/azure/key-vault/general/private-link-service). - If the cluster has outbound type
`userDefinedRouting`

and uses a firewall device that can control outbound traffic based on domain names, such as Azure Firewall, ensure the[required outbound network rules and FQDNs are allowed](outbound-rules-control-egress#azure-key-vault-provider-for-secrets-store-csi-driver). - If you're restricting Ingress to the cluster, make sure ports
**9808**and**8095**are open.

### Roles

- The identity used to with the
`SecretProviderClass`

needs to have`Key Vault Certificate User`

to access`key`

or`certificate`

[object types](/en-us/azure/key-vault/general/about-keys-secrets-certificates#object-types). - The identity used to with the
`SecretProviderClass`

needs to have`Key Vault Secrets User`

to access`secret`

[object type](/en-us/azure/key-vault/general/about-keys-secrets-certificates#object-types).

## Create an AKS cluster with Azure Key Vault provider for Secrets Store CSI Driver support

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus2`

Create an AKS cluster with Azure Key Vault provider for Secrets Store CSI Driver capability using the

command with the`az aks create`

`--enable-addons azure-keyvault-secrets-provider`

parameter. The add-on creates a user-assigned managed identity you can use to authenticate to your key vault. The following example creates an AKS cluster with the Azure Key Vault provider for Secrets Store CSI Driver enabled.Note

If you want to use Microsoft Entra Workload ID, you must also use the

`--enable-oidc-issuer`

and`--enable-workload-identity`

parameters, such as in the following example:`az aks create --name myAKSCluster --resource-group myResourceGroup --enable-addons azure-keyvault-secrets-provider --enable-oidc-issuer --enable-workload-identity --generate-ssh-keys`

`az aks create \ --name myAKSCluster \ --resource-group myResourceGroup \ --enable-addons azure-keyvault-secrets-provider \ --generate-ssh-keys`

The previous command creates a user-assigned managed identity,

`azureKeyvaultSecretsProvider`

, to access Azure resources. The following example uses this identity to connect to the key vault that stores the secrets, but you can also use other[identity access methods](csi-secrets-store-identity-access). Take note of the identity's`clientId`

in the output.`..., "addonProfiles": { "azureKeyvaultSecretsProvider": { ..., "identity": { "clientId": "<client-id>", ... } }`


Note

After you enable this feature, AKS creates a managed identity named `azurekeyvaultsecretsprovider-xxx`

in the node resource group and assigns it to the Virtual Machine Scale Sets (VMSS) automatically. You can use this managed identity or your own managed identity to access the key vault. It's not supported to prevent creation of the identity.

## Upgrade an existing AKS cluster with Azure Key Vault provider for Secrets Store CSI Driver support

Upgrade an existing AKS cluster with Azure Key Vault provider for Secrets Store CSI Driver capability using the

command and enable the`az aks enable-addons`

`azure-keyvault-secrets-provider`

add-on. The add-on creates a user-assigned managed identity you can use to authenticate to your key vault.`az aks enable-addons --addons azure-keyvault-secrets-provider --name myAKSCluster --resource-group myResourceGroup`


Note

After you enable this feature, AKS creates a managed identity named `azurekeyvaultsecretsprovider-xxx`

in the node resource group and assigns it to the Virtual Machine Scale Sets (VMSS) automatically. You can use this managed identity or your own managed identity to access the key vault. It's not supported to prevent creation of the identity.

## Verify the Azure Key Vault provider for Secrets Store CSI Driver installation

Get the AKS cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials --name myAKSCluster --resource-group myResourceGroup`

Verify the installation is finished using the

`kubectl get pods`

command, which lists all pods with the`secrets-store-csi-driver`

and`secrets-store-provider-azure`

labels in the kube-system namespace.`kubectl get pods -n kube-system -l 'app in (secrets-store-csi-driver,secrets-store-provider-azure)'`

Your output should look similar to the following example output:

`NAME READY STATUS RESTARTS AGE aks-secrets-store-csi-driver-4vpkj 3/3 Running 2 4m25s aks-secrets-store-csi-driver-ctjq6 3/3 Running 2 4m21s aks-secrets-store-csi-driver-tlvlq 3/3 Running 2 4m24s aks-secrets-store-provider-azure-5p4nb 1/1 Running 0 4m21s aks-secrets-store-provider-azure-6pqmv 1/1 Running 0 4m24s aks-secrets-store-provider-azure-f5qlm 1/1 Running 0 4m25s`

Verify that each node in your cluster's node pool has a Secrets Store CSI Driver pod and a Secrets Store Provider Azure pod running.


## Create or use an existing Azure Key Vault

Create or update a key vault with Azure role-based access control (Azure RBAC) enabled using the

command or the`az keyvault create`

command with the`az keyvault update`

`--enable-rbac-authorization`

flag. The name of the key vault must be globally unique. For more details on key vault permission models and Azure RBAC, see[Provide access to Key Vault keys, certificates, and secrets with an Azure role-based access control](/en-us/azure/key-vault/general/rbac-guide)`## Create a new Azure key vault az keyvault create --name <keyvault-name> --resource-group myResourceGroup --location eastus2 --enable-rbac-authorization ## Update an existing Azure key vault az keyvault update --name <keyvault-name> --resource-group myResourceGroup --location eastus2 --enable-rbac-authorization`

Your key vault can store keys, secrets, and certificates. In this example, use the

command to set a plain-text secret called`az keyvault secret set`

`ExampleSecret`

.`az keyvault secret set --vault-name <keyvault-name> --name ExampleSecret --value MyAKSExampleSecret`

Take note of the following properties for future use:

- The name of the secret object in the key vault
- The object type (secret, key, or certificate)
- The name of your key vault resource
- The Azure tenant ID of the subscription


## Next steps

In this article, you learned how to use the Azure Key Vault provider for Secrets Store CSI Driver in an AKS cluster. You now need to provide an identity to access the Azure Key Vault. To learn how, continue to the next article.


---

<!-- DOCUMENTO FUSIONADO: windows-aks-partner-solutions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/windows-aks-partner-solutions -->

# Windows AKS partner solutions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Microsoft collaborates with partners to ensure your build, test, deployment, configuration, and monitoring of your applications perform optimally with Windows containers on AKS.

Our third party partners featured in this article have introduction guides to help you start using their solutions with your applications running on Windows containers on AKS.

| Solutions | Partners |
|---|---|
| DevOps |
|

[NGINX](#f5-nginx)[Calico](#calico)[Datadog](#datadog)[New Relic](#new-relic)[Prisma Cloud](#prisma-cloud)[NetApp](#netapp)[Chef](#chef)## DevOps

DevOps streamlines the delivery process, improves collaboration across teams, and enhances software quality, ensuring swift, reliable, and continuous deployment of your Windows-based applications.

### GitLab

The GitLab DevSecOps Platform supports the Microsoft development ecosystem with performance, accessibility testing, SAST, DAST and Fuzzing security scanning, dependency scanning, SBOM, license management and more.

As an extensible platform, GitLab also allows you to plug in your own tooling for any stage. GitLab's integration with Azure Kubernetes Services (AKS) enables full DevSecOps workflows for Windows and Linux Container workloads using either Push CD or GitOps Pull CD with flux manifests. Using Cloud Native Buildpaks, GitLab Auto DevOps can build, test, and autodeploy OSS .NET projects.

To learn more, please our see our [joint blog](https://techcommunity.microsoft.com/t5/containers/using-gitlab-to-build-and-deploy-windows-containers-on-azure/ba-p/3889929).

### CircleCI

CircleCI’s integration with Azure Kubernetes Services (AKS) allows you to automate, build, validate, and ship containerized Windows applications, ensuring faster and more reliable software deployment. You can easily integrate your pipeline with AKS using CircleCI orbs, which are prepacked snippets of YAML configuration.

Follow this [tutorial](https://techcommunity.microsoft.com/t5/containers/continuous-deployment-of-windows-containers-with-circleci-and/ba-p/3841220) to learn how to set up a CI/CD pipeline to build a Dockerized ASP.NET application and deploy it to an AKS cluster.

## Networking

Ensure efficient traffic management, enhanced security, and optimal network performance with these solutions to achieve smooth application connectivity and communication.

### F5 NGINX

NGINX Ingress Controller deployed in AKS, on-premises, and in the cloud implements unified Kubernetes-native API gateways, load balancers, and Ingress controllers to reduce complexity, increase uptime, and provide in-depth insights into app health and performance for containerized Windows workloads.

Running at the edge of a Kubernetes cluster, NGINX Ingress Controller ensures holistic app security with user and service identities, authorization, access control, encrypted communications, and other NGINX App Protect modules for Layer 7 WAF and DoS app protection.

Learn how to manage connectivity to your Windows applications running on Windows nodes in a mixed-node AKS cluster with NGINX Ingress controller in this [blog](https://techcommunity.microsoft.com/t5/containers/improving-customer-experiences-with-f5-nginx-and-windows-on/ba-p/3820344).

### Calico

Tigera provides an active security platform with full-stack observability for containerized workloads and Microsoft AKS as a fully managed SaaS (Calico Cloud) or a self-managed service (Calico Enterprise). The platform prevents, detects, troubleshoots, and automatically mitigates exposure risks of security breaches for workloads in Microsoft AKS.

Its open-source offering, Calico Open Source, is the most widely adopted container networking and security solution. It specifies security and observability as code to ensure consistent enforcement of security policies, which enables DevOps, platform, and security teams to protect workloads, detect threats, achieve continuous compliance, and troubleshoot service issues in real-time.

For more information, see [Securing Windows workloads on Azure Kubernetes Service with Calico](https://techcommunity.microsoft.com/t5/containers/securing-windows-workloads-on-azure-kubernetes-service-with/ba-p/3815429).

## Observability

Observability provides deep insights into your systems, enabling rapid issue detection and resolution to enhance your application’s reliability and performance.

### Datadog

Datadog is the essential monitoring and security platform for cloud applications. We bring together end-to-end traces, metrics, and logs to make your applications, infrastructure, and third-party services entirely observable. Partner with Datadog for Windows on AKS environments to streamline monitoring, proactively resolve issues, and optimize application performance and availability.

Get started by following the recommendations in our [joint blog](https://techcommunity.microsoft.com/t5/containers/gain-full-observability-into-windows-containers-on-azure/ba-p/3853603).

### New Relic

New Relic's Azure Kubernetes integration is a powerful solution that seamlessly connects New Relic's monitoring and observability capabilities with Azure Kubernetes Service (AKS). By deploying the New Relic Kubernetes integration, users gain deep insights into their AKS clusters' performance, health, and resource utilization. This integration allows users to efficiently manage and troubleshoot containerized applications, optimize resource allocation, and proactively identify and resolve issues in their AKS environments. With New Relic's comprehensive monitoring and analysis tools, businesses can ensure the smooth operation and optimal performance of their Kubernetes workloads on Azure.

Check this [blog](https://techcommunity.microsoft.com/t5/containers/leveraging-new-relic-for-instrumentation-of-windows-container-on/ba-p/3870323) for detailed information.

## Security

Ensure the integrity and confidentiality of applications, thereby fostering trust and compliance across your infrastructure.

### Prisma Cloud

Prisma Cloud is a comprehensive Cloud-Native Application Protection Platform (CNAPP) tailor-made to help secure Windows containers on Azure Kubernetes Service (AKS). Gain continuous real-time visibility and control over Windows container environments, including vulnerability and compliance management, identities and permissions, and AI-assisted runtime defense. Integrated container scanning across the pipeline and in Azure Container Registry ensure security throughout the entire application lifecycle.

See [our guidance](https://techcommunity.microsoft.com/t5/containers/unlocking-new-possibilities-with-prisma-cloud-and-windows/ba-p/3866485) for more details.

## Storage

Storage enables standardized and seamless storage interactions, ensuring high application performance and data consistency.

### NetApp

[Astra](https://www.netapp.com/cloud-services/astra/) provides dynamic storage provisioning for stateful workloads on Azure Kubernetes Service (AKS). It also provides data protection using snapshots and clones. Provision SMB volumes through the Kubernetes control plane, making storage seamless and on-demand for all your Windows AKS workloads.

Follow the steps provided in [this blog](https://techcommunity.microsoft.com/t5/azure-architecture-blog/azure-netapp-files-smb-volumes-for-azure-kubernetes-services/ba-p/3052900) post to dynamically provision SMB volumes for Windows AKS workloads.

## Config management

Automate and standardize the system settings across your environments to enhance efficiency, reduce errors, and ensuring system stability and compliance.

### Chef

Chef provides visibility and threat detection from build to runtime that monitors, audits, and remediates the security of your Azure cloud services and Kubernetes and Windows container assets. Chef provides comprehensive visibility and continuous compliance into your cloud security posture and helps limit the risk of misconfigurations in cloud-native environments by providing best practices based on CIS, STIG, SOC2, PCI-DSS and other benchmarks. This is part of a broader compliance offering that supports on-premises or hybrid cloud environments including applications deployed on the edge.

To learn more about Chef’s capabilities, check out the comprehensive ‘how-to’ blog post here: [Securing Your Windows Environments Running on Azure Kubernetes Service with Chef](https://techcommunity.microsoft.com/t5/containers/securing-your-windows-environments-running-on-azure-kubernetes/ba-p/3821830).
