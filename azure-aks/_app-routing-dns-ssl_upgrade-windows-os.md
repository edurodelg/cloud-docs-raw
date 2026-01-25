---
merged_at: 2026-01-25T12:25:33.944589
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: app-routing-dns-ssl.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/app-routing-dns-ssl -->

# Set up a custom domain name and SSL certificate with the application routing add-on for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to configure custom domain names and SSL/TLS certificates for AKS ingress using [Azure Key Vault](/en-us/azure/key-vault/general/overview) and [Azure DNS](/en-us/azure/dns/dns-overview) with the [application routing add-on for AKS](app-routing).

## Prerequisites

An AKS cluster with the

[application routing add-on](app-routing).Azure Key Vault if you want to configure SSL termination and store certificates in the vault hosted in Azure. If you don't have one, see

[Create a key vault using the Azure CLI](/en-us/azure/key-vault/general/quick-create-cli).To enable support for HTTPS traffic, you need an SSL certificate. If you don't have one, see

[create a certificate](#create-and-export-a-self-signed-ssl-certificate).Azure DNS if you want to configure global and private zone management and host them in Azure. If you don't have an Azure DNS zone, you can

[create one](#create-a-global-azure-dns-zone). To enable support for DNS zones:- All global Azure DNS zones need to be in the same resource group, which could be different from the cluster resource group.
- All private Azure DNS zones need to be in the same resource group, which could be different from the cluster resource group.
- The resource group doesn't need to be in the same subscription as the cluster.


### Required Azure permissions

**Your user account needs**: [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner), [Azure account administrator](/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles#classic-subscription-administrator-roles), or [Azure co-administrator](/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles#classic-subscription-administrator-roles) role on your Azure subscription.

**What the commands do**: When you run `az aks approuting update --attach-kv`

or `az aks approuting zone add --attach-zones`

, these commands use your role assignment permissions to automatically grant the application routing add-on's managed identity the following roles:

**Key Vault Certificate User**role on your Azure Key Vault (for certificate access).**DNS Zone Contributor**role on your Azure DNS zones (for DNS record management).

For more information on AKS managed identities, see [Summary of managed identities](managed-identity-overview#summary-of-managed-identities-used-by-aks).

## Connect to your AKS cluster

To connect to the Kubernetes cluster from your local computer, you use `kubectl`

, the Kubernetes command-line client. You can install it locally using the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. If you use the Azure Cloud Shell,

`kubectl`

is already installed.Configure kubectl to connect to your Kubernetes cluster using the

command.`az aks get-credentials`

`# Set environment variables for your resource group and cluster name export RESOURCE_GROUP=<resource-group-name> export CLUSTER_NAME=<cluster-name> # Get the AKS cluster credentials az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Create and export a self-signed SSL certificate

For testing, you can use a self-signed public certificate instead of a Certificate Authority (CA)-signed certificate. If you already have a certificate, you can skip this step.

Caution

Self-signed certificates are digital certificates that aren't signed by a trusted third-party CA. The company or developer responsible for the website or software creates, issues, and signs these certificates. This is why self-signed certificates are considered unsafe for public-facing websites and applications. Azure Key Vault has a [trusted partnership with the some Certificate Authorities](/en-us/azure/key-vault/certificates/how-to-integrate-certificate-authority).

Create a self-signed SSL certificate to use with the ingress using the

`openssl req`

command. Make sure you replacewith the DNS name you're using.`<host-name>`

`openssl req -new -x509 -nodes -out aks-ingress-tls.crt -keyout aks-ingress-tls.key -subj "/CN=<host-name>" -addext "subjectAltName=DNS:<host-name>"`

Export the SSL certificate and skip the password prompt using the

`openssl pkcs12 -export`

command.`openssl pkcs12 -export -in aks-ingress-tls.crt -inkey aks-ingress-tls.key -out aks-ingress-tls.pfx`


## Import a self-signed SSL certificate into Azure Key Vault

Import the SSL certificate into Azure Key Vault using the

command. If your certificate is password protected, you can pass the password through the`az keyvault certificate import`

`--password`

flag.`# Set environment variables for your key vault name and certificate name export KEY_VAULT_NAME=<key-vault-name> export KEY_VAULT_CERT_NAME=<key-vault-certificate-name> # Import the SSL certificate into Azure Key Vault az keyvault certificate import --vault-name $KEY_VAULT_NAME --name $KEY_VAULT_CERT_NAME --file aks-ingress-tls.pfx [--password <certificate password if specified>]`


Note

To enable the application routing add-on to reload certificates from Azure Key Vault when they change, you should enable the [secret autorotation feature](csi-secrets-store-configuration-options#manage-auto-rotation) of the Secrets Store CSI driver. When autorotation is enabled, the driver updates the pod mount and the Kubernetes secret by polling for changes periodically, based on the rotation poll interval you define. The default rotation poll interval is two minutes.

## Enable Azure Key Vault integration

Azure Key Vault offers [two authorization systems](/en-us/azure/key-vault/general/rbac-access-policy): **Azure role-based access control (Azure RBAC)**, which operates on the management plane, and the **access policy model**, which operates on both the management plane and the data plane. The `--attach-kv`

operation selects the appropriate access model to use.

Get the resource ID for the key vault using the

command and set the output to an environment variable.`az keyvault show`

`KEY_VAULT_ID=$(az keyvault show --name <KeyVaultName> --query "id" --output tsv)`

Update the application routing add-on to enable the Azure Key Vault provider for Secrets Store CSI Driver and apply the required role assignments using the

command with the`az aks approuting update`

`--enable-kv`

and`--attach-kv`

arguments.`az aks approuting update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --enable-kv --attach-kv ${KEY_VAULT_ID}`


## Create a global Azure DNS zone

If you already have an Azure DNS zone, you can skip this step.

Create an Azure DNS zone using the

command.`az network dns zone create`

`# Set environment variables for your resource group and DNS zone name export RESOURCE_GROUP=<resource-group-name> export ZONE_NAME=<zone-name> # Create the Azure DNS zone az network dns zone create --resource-group $RESOURCE_GROUP --name $ZONE_NAME`


## Enable Azure DNS integration

Get the resource ID for the DNS zone using the

command and set the output to an environment variable.`az network dns zone show`

`ZONE_ID=$(az network dns zone show --resource-group $RESOURCE_GROUP --name $ZONE_NAME --query "id" --output tsv)`

Update the application routing add-on to enable Azure DNS integration using the

command. You can pass a comma-separated list of DNS zone resource IDs.`az aks approuting zone`

`az aks approuting zone add --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --ids=${ZONE_ID} --attach-zones`


## Create an Ingress class that uses a host name and a certificate from Azure Key Vault

The application routing add-on creates an Ingress class on the cluster named *webapprouting.kubernetes.azure.com*. When you create an Ingress object with this class, it activates the add-on.

Get the certificate URI to use in the ingress from Azure Key Vault using the

command.`az keyvault certificate show`

`az keyvault certificate show --vault-name $KEY_VAULT_NAME --name $KEY_VAULT_CERT_NAME --query "id" --output tsv`

The following example output shows the certificate URI returned from the command:

`https://KeyVaultName.vault.azure.net/certificates/KeyVaultCertificateName/ab12c34567d89e01f2345g6h78ijkl90`

Copy the following YAML manifest into a new file named

**ingress.yaml**and save the file to your local computer.Update

with the name of your DNS host and`<host-name>`

with the URI returned from the previous command. The string value for`<key-vault-certificate-uri>`

should only include`<key-vault-certificate-uri>`

`https://yourkeyvault.vault.azure.net/certificates/certname`

. Remove the*Certificate Version*at the end of the URI string to get the current version.The

key in the`secretName`

`tls`

section defines the name of the secret that contains the certificate for this Ingress resource. This certificate is presented in the browser when a client browses to the URL specified in the`<host-name>`

key. Make sure that the value of`secretName`

is equal to`keyvault-`

followed by the value of the Ingress resource name (from`metadata.name`

). In the example YAML,`secretName`

needs to be equal to`keyvault-<your-ingress-name>`

.`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: annotations: kubernetes.azure.com/tls-cert-keyvault-uri: <key-vault-certificate-uri> name: aks-helloworld namespace: hello-web-app-routing spec: ingressClassName: webapprouting.kubernetes.azure.com rules: - host: <host-name> http: paths: - backend: service: name: aks-helloworld port: number: 80 path: / pathType: Prefix tls: - hosts: - <host-name> secretName: keyvault-<your-ingress-name>`

Create the cluster resources using the

command.`kubectl apply`

`kubectl apply -f ingress.yaml -n hello-web-app-routing`

The following example output shows the created resource:

`Ingress.networking.k8s.io/aks-helloworld created`


## Verify the managed ingress was created

Verify the managed ingress was created using the

command.`kubectl get ingress`

`kubectl get ingress -n hello-web-app-routing`

The following example output shows the created managed ingress:

`NAME CLASS HOSTS ADDRESS PORTS AGE aks-helloworld webapprouting.kubernetes.azure.com myapp.contoso.com 20.51.92.19 80, 443 4m`


## Related content

Learn about monitoring the Ingress NGINX controller metrics included with the application routing add-on with [with Prometheus in Grafana](app-routing-nginx-prometheus) as part of analyzing the performance and usage of your application.


---

<!-- DOCUMENTO FUSIONADO: upgrade-windows-os.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/upgrade-windows-os -->

# Upgrade the operating system (OS) version for your Azure Kubernetes Service (AKS) Windows workloads

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When upgrading the OS version of a running Windows workload on Azure Kubernetes Service (AKS), you need to deploy a new node pool to ensure the Windows versions match on each node pool. This article describes the steps to upgrade the OS version for Windows workloads on AKS.

## Windows Server OS version support

When a new Windows Server OS version is released, AKS is committed to supporting it. We recommend that you upgrade to the latest version to take advantage of the fixes, improvements, and new functionality. AKS provides a five-year support lifecycle for every Windows Server version, starting with Windows Server 2022. During this period, AKS releases a new version that supports a newer version of Windows Server OS for you to upgrade to. After the five-year lifecycle ends, you must migrate workloads to newer supported versions to ensure compatibility, security updates, and continued support from AKS.

Note

[Windows Server 2019 retires on March 1, 2026](https://github.com/Azure/AKS/issues/4091). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2019 on any Kubernetes version. All existing node pools with Windows Server 2019 will be unsupported. Windows Server 2019 is not supported in Kubernetes version 1.33 and above. Starting on April 1, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail.[Windows Server 2022 retires on March 15, 2027](https://github.com/Azure/AKS/issues/4168). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2022 on any Kubernetes version. All existing node pools with Windows Server 2022 will be unsupported. Windows Server 2022 is not supported in Kubernetes version 1.36 and above. Starting on April 1, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail.

For more information, see [AKS release notes](https://github.com/Azure/AKS/releases). To stay up to date on the latest Windows Server OS versions and learn more about our roadmap of what's planned for support on AKS, see our [AKS public roadmap](https://github.com/azure/aks/projects/1).

## Limitations

- Node pool update to migrate from one Windows Server version to another isn't supported.
- Different Windows Server versions can't coexist on the same node pool on AKS. You need to create a new node pool to host the new OS version. It's important that you match the permissions and access of the previous node pool to the new one.
- Windows Server 2025 (preview) is supported starting in Kubernetes version 1.32.

## Before you begin

- Update the
`FROM`

statement in your Dockerfile to the new OS version. - Check your application and verify the container app works on the new OS version.
- Deploy the verified container app on AKS to a development or testing environment.
- Take note of the new image name or tag for use in this article.

Note

To learn how to build a Dockerfile for Windows workloads, see [Dockerfile on Windows](/en-us/virtualization/windowscontainers/manage-docker/manage-windows-dockerfile) and [Optimize Windows Dockerfiles](/en-us/virtualization/windowscontainers/manage-docker/optimize-windows-dockerfile).

### Install `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


### Register `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using the [`az feature register`

][az-feature-register] command.`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the [

`az feature show`

][az-feature-show] command. It takes a few minutes for the status to show*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using the [`az provider register`

][az-provider-register] command.`az provider register --namespace Microsoft.ContainerService`


## Add a new node pool to an existing cluster

Add a node pool with your desired OS version to your existing cluster:

[Use CLI to add a Windows node pool](learn/quick-windows-container-deploy-cli)to an existing cluster.[Use Portal to add a Windows node pool](learn/quick-windows-container-deploy-portal)to an existing cluster.[Use PowerShell to add a Windows node pool](learn/quick-windows-container-deploy-powershell)to an existing cluster.[Use Terraform to add a Windows node pool](learn/quick-windows-container-deploy-terraform)to an existing cluster.

## Update the YAML file

Node Selector is the most common and recommended option for placement of Windows pods on Windows nodes.

Add Node Selector to your YAML file by adding the following annotation:

`nodeSelector: "kubernetes.io/os": windows`

The annotation finds any available Windows node and places the pod on that node (following all other scheduling rules). When upgrading your OS version, you need to enforce the placement on a Windows node and a node running the latest OS version. To accomplish this, one option is to use a different annotation. Update

`<OSSKU>`

to match the ossku your desired Windows OS version, for example`Windows2025`

.`nodeSelector: "kubernetes.azure.com/os-sku": <OSSKU>`

Once you update the

`nodeSelector`

in the YAML file, you also need to update the container image you want to use. You can get this information from the previous step in which you created a new version of the containerized application by changing the`FROM`

statement on your Dockerfile.Note

You should use the same YAML file you used to initially deploy the application. This ensures that no other configuration changes besides the

`nodeSelector`

and container image.

## Apply the updated YAML file to the existing workload

View the nodes on your cluster using the

`kubectl get nodes`

command.`kubectl get nodes -o wide`

The following example output shows all nodes on the cluster, including the new node pool you created and the existing node pools:

`NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME aks-agentpool-18877473-vmss000000 Ready agent 5h40m v1.23.8 10.240.0.4 <none> Ubuntu 18.04.6 LTS 5.4.0-1085-azure containerd://1.5.11+azure-2 akspoolws000000 Ready agent 3h15m v1.23.8 10.240.0.208 <none> Windows Server 2022 Datacenter 10.0.20348.825 containerd://1.6.6+azure akspoolws000001 Ready agent 3h17m v1.23.8 10.240.0.239 <none> Windows Server 2022 Datacenter 10.0.20348.825 containerd://1.6.6+azure akspoolws000002 Ready agent 3h17m v1.23.8 10.240.1.14 <none> Windows Server 2022 Datacenter 10.0.20348.825 containerd://1.6.6+azure akswspool000000 Ready agent 5h37m v1.23.8 10.240.0.115 <none> Windows Server 2019 Datacenter 10.0.17763.3165 containerd://1.6.6+azure akswspool000001 Ready agent 5h37m v1.23.8 10.240.0.146 <none> Windows Server 2019 Datacenter 10.0.17763.3165 containerd://1.6.6+azure akswspool000002 Ready agent 5h37m v1.23.8 10.240.0.177 <none> Windows Server 2019 Datacenter 10.0.17763.3165 containerd://1.6.6+azure`

Apply the updated YAML file to the existing workload using the

`kubectl apply`

command and specify the name of the YAML file.`kubectl apply -f <filename>`

The following example output shows a

*configured*status for the deployment:`deployment.apps/sample configured service/sample unchanged`

At this point, AKS starts the process of terminating the existing pods and deploying new pods to the nodes with the

`nodeSelector`

annotation.Check the status of the deployment using the

`kubectl get pods`

command.`kubectl get pods -o wide`

The following example output shows the pods in the

`default`

namespace:`NAME READY STATUS RESTARTS AGE IP NODE NOMINATED NODE READINESS GATES sample-7794bfcc4c-k62cq 1/1 Running 0 2m49s 10.240.0.238 akspoolws000000 <none> <none> sample-7794bfcc4c-rswq9 1/1 Running 0 2m49s 10.240.1.10 akspoolws000001 <none> <none> sample-7794bfcc4c-sh78c 1/1 Running 0 2m49s 10.240.0.228 akspoolws000000 <none> <none>`


## Security and authentication considerations

If you're using Group Managed Service Accounts (gMSA), you need to update the Managed Identity configuration for the new node pool. gMSA uses a secret (user account and password) so the node that runs the Windows pod can authenticate the container against Microsoft Entra ID. To access that secret on Azure Key Vault, the node uses a Managed Identity that allows the node to access the resource. Since Managed Identities are configured per node pool, and the pod now resides on a new node pool, you need to update that configuration. For more information, see [Enable Group Managed Service Accounts (GMSA) for your Windows Server nodes on your Azure Kubernetes Service (AKS) cluster](use-group-managed-service-accounts).

The same principle applies to Managed Identities for any other pod or node pool when accessing other Azure resources. You need to update any access that Managed Identity provides to reflect the new node pool. To view update and sign-in activities, see [How to view Managed Identity activity](/en-us/azure/active-directory/managed-identities-azure-resources/how-to-view-managed-identity-activity).

## Next steps

In this article, you learned how to upgrade the OS version for Windows workloads on AKS. To learn more about Windows workloads on AKS, see [Deploy a Windows container application on Azure Kubernetes Service (AKS)](learn/quick-windows-container-deploy-cli).
