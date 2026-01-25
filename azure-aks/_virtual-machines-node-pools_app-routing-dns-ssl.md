---
merged_at: 2026-01-25T12:06:27.821115
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: virtual-machines-node-pools.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/virtual-machines-node-pools -->

# Use Virtual Machines node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you'll learn about the new Virtual Machines node pool type for AKS.

With Virtual Machines node pools, AKS directly manages the provisioning and bootstrapping of every single node. For Virtual Machine Scale Sets node pools, AKS manages the model of the Virtual Machine Scale Sets and uses it to achieve consistency across all nodes in the node pool. Virtual Machines node pools enable you to orchestrate your cluster with virtual machines that best fit your individual workloads.

## Overview

### How it works

A node pool consists of a set of virtual machines, where different virtual machine sizes are designated to support different types of workloads. These virtual machine sizes, referred to as SKUs, are categorized into different families that are optimized for specific purposes. For more information, see [VM SKUs](/en-us/azure/virtual-machines/sizes/overview).

To enable scaling of multiple virtual machine sizes, the Virtual Machines node pool type uses a `ScaleProfile`

that contains configurations indicating how the node pool can scale, specifically the desired list of virtual machine size and the count of each size. A `ManualScaleProfile`

is a scale profile that specifies one desired virtual machine size and the total count of that type in the nodepool. Only one virtual machine size is allowed in a `ManualScaleProfile`

. You need to create a separate `ManualScaleProfile`

for each virtual machine size in your node pool. When creating a new Virtual Machines node pool, you add an initial manual scale profile for a virtual machine size using the `vm-size`

field and including a `node-count`

, per the instructions below. You can also add additional manual scale profiles following the instructions for [adding manual scale profiles](/en-us/azure/aks/virtual-machines-node-pools#add-a-manual-scale-profile-to-a-node-pool).

Note

When creating a new Virtual Machines node pool, you can have multiple scale profiles, and you need at least one manual scale profile in your nodepool.

### Advantages

Advantages of the Virtual Machines node pool type include:

**Flexibility**: Node specifications can be updated to adapt to your current workload and needs.**Fine-tuned control**: Single node-level controls allow specifying and mixing nodes of different specs to lift restrictions from a single model and improve consistency.**Efficiency**: You can reduce the node footprint for your cluster, simplifying your operational requirements.

Virtual Machines node pools provide a better experience for dynamic workloads and high availability requirements. Virtual Machines node pools enable you to set up multiple similar-family virtual machines in one node pool. Your workload will be automatically scheduled on the available resources that you configure.

### Feature comparison

The following table highlights how Virtual Machines node pools compare with standard [Scale Set](/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-orchestration-modes) node pools.

| Node pool type | Capabilities |
|---|---|
| Virtual Machines node pool | You can add, remove, or update nodes in a node pool. Virtual machine types can be any virtual machine of the same family type (for example, D-series, A-Series, etc.). |
| Virtual Machine Scale Set based node pool | You can add or remove nodes of the same size and type in a node pool. If you add a new virtual machine size to the cluster, you need to create a new node pool. |

### Limitations

[Cluster autoscaler](cluster-autoscaler-overview)is currently not supported.[InifiniBand](/en-us/azure/virtual-machines/extensions/enable-infiniband)isn't available.[Node pool snapshot](node-pool-snapshot)isn't supported.- All VM sizes selected in a node pool need to be from a similar virtual machine family. For example, you can't mix an N-Series virtual machine type with a D-Series virtual machine type in the same node pool.
- Virtual Machines node pools allow up to five different virtual machine sizes per node pool.

## Prerequisites

- An Azure subscription. If you don't have one, you can
[create a free account](https://azure.microsoft.com/free). - Azure CLI version 2.73.0 or later installed and configured. To find the version, run
`az --version`

. For more information about installing or upgrading the Azure CLI, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli#install-azure-cli) - This feature requires kubernetes version 1.27 or greater. To upgrade your kubernetes version, see
[Upgrade AKS cluster](upgrade-aks-cluster)

## Create an AKS cluster with Virtual Machines node pools

Note

Only *one* VM size is allowed in a scale profile, and the maximum limit is *five* VM scale profiles overall for a Virtual Machines node pool.

Create an AKS cluster with Virtual Machines node pools using the

command with the`az aks create`

`--vm-set-type`

flag set to`"VirtualMachines"`

.The following example creates a cluster named

*myAKSCluster*with a Virtual Machines node pool containing two nodes, generates SSH keys, sets the load balancer SKU to*standard*, and sets the Kubernetes version to*1.31.0*:`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --vm-set-type "VirtualMachines" \ --vm-sizes "Standard_D4s_v3" --node-count 2 \ --kubernetes-version 1.31.0`


## Create a cluster with Windows enabled and a Windows Virtual Machine node pool

Virtual Machine node pools are available in Windows enabled clusters. The following example creates a cluster named *myAKSCluster* with a Virtual Machines node pool. These steps create a Linux system pool at first.

Create a username to use as administrator credentials for the Windows Server nodes on your cluster. The following commands prompt you for a username and sets it to

*WINDOWS_USERNAME*for use in a later command.`echo "Please enter the username to use as administrator credentials for Windows Server nodes on your cluster: " && read WINDOWS_USERNAME`

Create a password for the administrator username you created in the previous step. The password must be a minimum of 14 characters and meet the

[Windows Server password complexity requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference).`echo "Please enter the password to use as administrator credentials for Windows Server nodes on your cluster: " && read WINDOWS_PASSWORD`

Create an AKS cluster with Windows enabled and Virtual Machines type node pools using the

command with the`az aks create`

`--vm-set-type`

flag set to`"VirtualMachines"`

.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 2 \ --enable-addons monitoring \ --generate-ssh-keys \ --windows-admin-username $WINDOWS_USERNAME \ --windows-admin-password $WINDOWS_PASSWORD \ --vm-set-type "VirtualMachines" \ --network-plugin azure`

Add a Virtual Machines node pool to an existing Windows enabled cluster using the

command with the`az aks nodepool add`

`--vm-set-type`

flag set to`"VirtualMachines"`

. The following example adds a Virtual Machines node pool named*npwin*to the*myAKSCluster*cluster:`az aks nodepool add --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --os-type Windows \ --name npwin \ --vm-sizes "Standard_D2s_V3" \ --node-count 1 --vm-set-type "VirtualMachines"`


## Add a Virtual Machines node pool to an existing cluster

Add a Virtual Machines node pool to an existing cluster using the

command with the`az aks nodepool add`

`--vm-set-type`

flag set to`"VirtualMachines"`

.The following example adds a Virtual Machines node pool named

*myvmpool*to the*myAKSCluster*cluster. The node pool creates a ManualScaleProfile with`--vm-sizes`

set to*Standard_D4s_v3*and a`--node-count`

of 3:`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myvmpool \ --vm-set-type "VirtualMachines" \ --vm-sizes "Standard_D4s_v3" \ --node-count 3`


## Add a manual scale profile to a node pool

Add a manual scale profile to a node pool using the

with the`az aks nodepool manual-scale add`

`--vm-sizes`

flag set to`"Standard_D2s_v3"`

and the`node-count`

set to 2.The following example adds a manual scale profile to node pool

*myvmpool*in cluster*myAKSCluster*. The node pool includes two nodes with a VM SKU of*Standard_D2s_v3*:`az aks nodepool manual-scale add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myvmpool \ --vm-sizes "Standard_D2s_v3" \ --node-count 2`


## Update an existing manual scale profile

Update an existing manual scale profile in a node pool using the

command with the`az aks nodepool manual-scale update`

`--vm-sizes`

flag set to`"Standard_D2s_v3"`

.Note

Use the

`--current-vm-sizes`

parameter to specify the size of the existing node pool that you want to update. You can update`--vm-sizes`

and/or`--node-count`

. When using other tools or REST APIs, you need to pass in a full`agentPoolProfiles.virtualMachinesProfile.scale`

field when updating the node pool scale profile.The following example updates a manual scale profile to the

*myvmpool*node pool in the*myAKSCluster*cluster. The command updates the number of nodes to five and changes the VM SKU from*Standard_D4s_v3*to*Standard_D8s_v3*:`az aks nodepool manual-scale update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myvmpool \ --current-vm-sizes "Standard_D4s_v3" \ --vm-sizes "Standard_D8s_v3" \ --node-count 5`


## Delete a manual scale profile

Delete an existing manual scale profile using the

command.`az aks nodepool manual-scale delete`

Note

The

`--current-vm-sizes`

parameter specifies the size of the existing node pool to be deleted. When using other tools or REST APIs to update the node pool scale profile, pass in a full`agentPoolProfiles.virtualMachinesProfile.scale`

field.The following example deletes the manual scale profile for the

*Standard_D8s_v3*VM SKU in the*myvmpool*node pool.`az aks nodepool manual-scale delete \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myvmpool \ --current-vm-sizes "Standard_D8s_v3"`


## Next steps

In this article, you learned how to use Virtual Machines node pools in AKS. To learn more about node pools in AKS, see [Create node pools](create-node-pools).


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
