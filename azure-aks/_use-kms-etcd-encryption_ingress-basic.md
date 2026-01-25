---
merged_at: 2026-01-25T12:25:33.975342
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-kms-etcd-encryption.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-kms-etcd-encryption -->

# Add Key Management Service (KMS) etcd encryption to an Azure Kubernetes Service (AKS) cluster (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

This article describes the legacy KMS experience for AKS. For new clusters running Kubernetes version 1.33 or later, we recommend using the new [KMS data encryption](kms-data-encryption) experience, which offers platform-managed keys, customer-managed keys with automatic key rotation, and a simplified configuration experience.

For conceptual information about data encryption options, see [Data encryption at rest concepts for AKS](kms-data-encryption-concepts).

This article shows you how to turn on encryption at rest for a public or private key vault using Azure Key Vault and the Key Management Service (KMS) plugin on AKS. You can use the KMS plugin to:

- Use a key in a key vault for etcd encryption.
- Bring your own keys.
- Provide encryption at rest for secrets stored in etcd.
- Rotate the keys in a key vault.

For more information on using KMS, see [Using a KMS provider for data encryption](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/).

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/free). - Azure CLI version 2.39.0 or later. Find your version using the
`az --version`

command. If you need to install or upgrade, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

Warning

Starting on September 15, 2024, Konnectivity is no longer supported for private key vaults for new subscriptions or subscriptions that didn't previously use this configuration. For subscriptions currently using this configuration or used it in the past 60 days, support continues until AKS version 1.30 reaches end of life for community support.

KMS supports Konnectivity or [API Server VNet Integration](api-server-vnet-integration) for public key vaults.

KMS supports [API Server VNet Integration](api-server-vnet-integration) for both private and public key vaults.

You can use `kubectl get pods -n kube-system`

to verify the results and show that a `konnectivity-agent`

pod is running. If a pod is running, the AKS cluster is using Konnectivity. When you use API Server VNet Integration, you can run the `az aks show --resource-group <resource-group-name> --name <cluster-name>`

command to verify that the `enableVnetIntegration`

setting is set to `true`

.

## Limitations

The following limitations apply when you integrate KMS etcd encryption with AKS:

- Deleting the key, the key vault, or the associated identity isn't supported.
- KMS etcd encryption doesn't work with system-assigned managed identity. The key vault access policy must be set before the feature is turned on. System-assigned managed identity isn't available until after the cluster is created. Consider the cycle dependency.
- Because the firewall blocks traffic from the KMS plugin to Key Vault, two scenarios aren't supported. First, Azure Key Vault can't be configured with the firewall option
*Allow public access from specific virtual networks and IP addresses*. Second, Azure Key Vault can't be configured with*Disable public access*unless[API Server VNet Integration](api-server-vnet-integration)is enabled. - The maximum number of secrets supported by a cluster with KMS turned on is
*2,000*. However, it's important to note that[KMS v2](use-kms-v2)isn't limited by this restriction and can handle a higher number of secrets. - Bring your own (BYO) Azure key vault from another tenant isn't supported.
- With KMS turned on, you can't change the associated key vault mode (public versus private). To
[update a key vault mode](update-kms-key-vault), you must first turn off KMS, and then turn it on again. - If a cluster has KMS turned on and has a private key vault, it must use the
[API Server VNet Integration](api-server-vnet-integration)tunnel. Konnectivity isn't supported. - Using the Virtual Machine Scale Sets API to scale the nodes in the cluster down to zero deallocates the nodes. The cluster then goes down and becomes unrecoverable.
- After you turn off KMS, you can't delete or expire the keys. Such behaviors would cause the API server to stop working.
- For a private cluster with KMS enabled and virtual network integration that uses a private key vault, the network security group (NSG) must allow TCP port 443 from the API server to the private key vault's private endpoint IP address. This limitation needs to be considered when using other rules in the API subnet NSG or cluster subnet NSG.

## Create a key vault and key for a public key vault

The following sections describe how to turn on KMS for a public key vault. You can use a public key vault with or without Azure role-based access control (Azure RBAC).

Warning

Deleting the key or the key vault isn't supported and causes the secrets in the cluster to be unrecoverable.

If you need to recover your key vault or your key, see [Azure Key Vault recovery management with soft delete and purge protection](/en-us/azure/key-vault/general/key-vault-recovery?tabs=azure-cli).

Create a key vault with Azure RBAC using the

command. This example command also exports the key vault resource ID to an environment variable.`az keyvault create`

`export KEY_VAULT_RESOURCE_ID=$(az keyvault create --name $KEY_VAULT --resource-group $RESOURCE_GROUP --enable-rbac-authorization true --query id -o tsv)`

Assign yourself permissions to create a key using the

command. This example assigns the Key Vault Crypto Officer role to the signed-in user.`az role assignment create`

`az role assignment create --role "Key Vault Crypto Officer" --assignee-object-id $(az ad signed-in-user show --query id -o tsv) --assignee-principal-type "User" --scope $KEY_VAULT_RESOURCE_ID`

Create a key using the

command.`az keyvault key create`

`az keyvault key create --name $KEY_NAME --vault-name $KEY_VAULT`

Get the key ID and save it as an environment variable using the

command.`az keyvault key show`

`export KEY_ID=$(az keyvault key show --name $KEY_NAME --vault-name $KEY_VAULT --query 'key.kid' -o tsv) echo $KEY_ID`


## Create a user-assigned managed identity for a public key vault

Create a user-assigned managed identity using the

command.`az identity create`

`az identity create --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP`

Get the identity object ID and save it as an environment variable using the

command.`az identity show`

`export IDENTITY_OBJECT_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'principalId' -o tsv) echo $IDENTITY_OBJECT_ID`

Get the identity resource ID and save it as an environment variable using the

command.`az identity show`

`export IDENTITY_RESOURCE_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'id' -o tsv) echo $IDENTITY_RESOURCE_ID`


## Assign permissions to decrypt and encrypt a public key vault

The following sections describe how to assign decrypt and encrypt permissions for a public key vault with or without Azure RBAC.

-
[Assign permissions for a public key vault with Azure RBAC](#tabpanel_2_rbac-kv) -
[Assign permissions for a public key vault without Azure RBAC](#tabpanel_2_non-rbac-kv)

Assign the Key Vault Crypto User role to give decrypt and encrypt permissions using the

command.`az role assignment create`

`az role assignment create --role "Key Vault Crypto User" --assignee-object-id $IDENTITY_OBJECT_ID --assignee-principal-type "ServicePrincipal" --scope $KEY_VAULT_RESOURCE_ID`


## Enable KMS for a public key vault on an AKS cluster

The following sections describe how to turn on KMS for a public key vault on a new or existing AKS cluster.

### Create an AKS cluster with a public key vault and KMS

Create an AKS cluster with a public key vault and KMS using the

command with the`az aks create`

`--enable-azure-keyvault-kms`

,`--azure-keyvault-kms-key-vault-network-access`

, and`--azure-keyvault-kms-key-id`

parameters.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --assign-identity $IDENTITY_RESOURCE_ID \ --enable-azure-keyvault-kms \ --azure-keyvault-kms-key-vault-network-access "Public" \ --azure-keyvault-kms-key-id $KEY_ID \ --generate-ssh-keys`


### Enable a public key vault and KMS on an existing AKS cluster

Enable KMS on a public key vault on an existing cluster using the

command with the`az aks update`

`--enable-azure-keyvault-kms`

,`--azure-keyvault-kms-key-vault-network-access`

, and`--azure-keyvault-kms-key-id`

parameters.`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --enable-azure-keyvault-kms \ --azure-keyvault-kms-key-vault-network-access "Public" \ --azure-keyvault-kms-key-id $KEY_ID`

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


## Rotate existing keys in a public key vault

After you change the key ID (including changing either the key name or the key version), you can rotate the existing keys in the public key vault.

Warning

Remember to update all secrets after key rotation. If you don't update all secrets, the secrets are inaccessible if the keys that were created earlier don't exist or no longer work.

KMS uses two keys at the same time. After the first key rotation, you need to ensure both the old and new keys are valid (not expired) until the next key rotation. After the second key rotation, the oldest key can be safely removed/expired.

After rotating KMS key version with the new `keyId`

, check `securityProfile.azureKeyVaultKms.keyId`

in AKS resource json. Ensure the new key version is in use.

Rotate existing keys using the

command with the`az aks update`

`--enable-azure-keyvault-kms`

,`--azure-keyvault-kms-key-vault-network-access`

, and`--azure-keyvault-kms-key-id`

parameters.`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --enable-azure-keyvault-kms \ --azure-keyvault-kms-key-vault-network-access "Public" \ --azure-keyvault-kms-key-id $NEW_KEY_ID`

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


## Create a key vault and key for a private key vault

If you turn on KMS for a private key vault, AKS automatically creates a private endpoint and a private link in the node resource group. The key vault has a private endpoint connection with the AKS cluster.

Warning

Keep the following information in mind when using a private key vault:

- KMS only supports
[API Server VNet Integration](api-server-vnet-integration)for private key vault. - Creating or updating keys in a private key vault that doesn't have a private endpoint isn't supported. To learn how to manage private key vaults, see
[Integrate a key vault by using Azure Private Link](/en-us/azure/key-vault/general/private-link-service). - Deleting the key or the key vault isn't supported and causes the secrets in the cluster to be unrecoverable. If you need to recover your key vault or your key, see
[Azure Key Vault recovery management with soft delete and purge protection](/en-us/azure/key-vault/general/key-vault-recovery?tabs=azure-cli).

Create a private key vault using the

command with the`az keyvault create`

`--public-network-access Disabled`

parameter.`az keyvault create --name $KEY_VAULT --resource-group $RESOURCE_GROUP --public-network-access Disabled`

Create a key using the

command.`az keyvault key create`

`az keyvault key create --name $KEY_NAME --vault-name $KEY_VAULT`


## Create a user-assigned managed identity for a private key vault

Create a user-assigned managed identity using the

command.`az identity create`

`az identity create --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP`

Get the identity object ID and save it as an environment variable using the

command.`az identity show`

`export IDENTITY_OBJECT_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'principalId' -o tsv) echo $IDENTITY_OBJECT_ID`

Get the identity resource ID and save it as an environment variable using the

command.`az identity show`

`export IDENTITY_RESOURCE_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'id' -o tsv) echo $IDENTITY_RESOURCE_ID`


## Assign permissions to decrypt and encrypt a private key vault

The following sections describe how to assign decrypt and encrypt permissions for a private key vault with or without Azure RBAC.

-
[Assign permissions for a private key vault with Azure RBAC](#tabpanel_3_rbac-kv) -
[Assign permissions for a private key vault without Azure RBAC](#tabpanel_3_non-rbac-kv)

Assign the Key Vault Crypto User role to give decrypt and encrypt permissions using the

command.`az role assignment create`

`az role assignment create --role "Key Vault Crypto User" --assignee-object-id $IDENTITY_OBJECT_ID --assignee-principal-type "ServicePrincipal" --scope $KEY_VAULT_RESOURCE_ID`


## Assign permissions to create a private link

For private key vaults, the Key Vault Contributor role is required to create a private link between the private key vault and the cluster.

Assign the Key Vault Contributor role using the

command.`az role assignment create`

`az role assignment create --role "Key Vault Contributor" --assignee-object-id $IDENTITY_OBJECT_ID --assignee-principal-type "ServicePrincipal" --scope $KEY_VAULT_RESOURCE_ID`


## Enable KMS for a private key vault on an AKS cluster

The following sections describe how to turn on KMS for a private key vault on a new or existing AKS cluster.

### Create an AKS cluster with a private key vault and KMS

Create an AKS cluster with a private key vault and KMS using the

command with the`az aks create`

`--enable-azure-keyvault-kms`

,`--azure-keyvault-kms-key-id`

,`--azure-keyvault-kms-key-vault-network-access`

, and`--azure-keyvault-kms-key-vault-resource-id`

parameters.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --assign-identity $IDENTITY_RESOURCE_ID \ --enable-azure-keyvault-kms \ --azure-keyvault-kms-key-id $KEY_ID \ --azure-keyvault-kms-key-vault-network-access "Private" \ --azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID \ --generate-ssh-keys`


### Update an existing AKS cluster to turn on KMS etcd encryption for a private key vault

Enable KMS on a private key vault on an existing cluster using the

command with the`az aks update`

`--enable-azure-keyvault-kms`

,`--azure-keyvault-kms-key-id`

,`--azure-keyvault-kms-key-vault-network-access`

, and`--azure-keyvault-kms-key-vault-resource-id`

parameters.`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --enable-azure-keyvault-kms \ --azure-keyvault-kms-key-id $KEY_ID \ --azure-keyvault-kms-key-vault-network-access "Private" \ --azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID`

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


### Rotate existing keys in a private key vault

After you change the key ID (including changing either the key name or the key version), you can rotate the existing keys in the private key vault.

Warning

Remember to update all secrets after key rotation. If you don't update all secrets, the secrets are inaccessible if the keys that were created earlier don't exist or no longer work.

After you rotate the key, the previous key (key1) is still cached and shouldn't be deleted. If you want to delete the previous key (key1) immediately, you need to rotate the key twice. Then key2 and key3 are cached, and key1 can be deleted without affecting the existing cluster.

After rotating KMS key version with the new `keyId`

, check `securityProfile.azureKeyVaultKms.keyId`

in AKS resource json. Ensure the new key version is in use.

Rotate existing keys in a private key vault using the

command with the`az aks update`

`--enable-azure-keyvault-kms`

,`--azure-keyvault-kms-key-id`

,`--azure-keyvault-kms-key-vault-network-access`

, and`--azure-keyvault-kms-key-vault-resource-id`

parameters.`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --enable-azure-keyvault-kms \ --azure-keyvault-kms-key-id $NEW_KEY_ID \ --azure-keyvault-kms-key-vault-network-access "Private" \ --azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID`

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


## Disable KMS on an AKS cluster

Before you turn off KMS, verify that KMS is enabled on the cluster using the

command.`az aks list`

`az aks list --query "[].{Name:name, KmsEnabled:securityProfile.azureKeyVaultKms.enabled, KeyId:securityProfile.azureKeyVaultKms.keyId}" -o table`

Once confirmed, you can disable KMS using the

command with the`az aks update`

`--disable-azure-keyvault-kms`

parameter.`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --disable-azure-keyvault-kms`

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


## Next steps

For more information on using KMS with AKS, see the following articles:

[Enable KMS data encryption in AKS](kms-data-encryption)- The new KMS experience with platform-managed keys and automatic key rotation[Data encryption at rest concepts for AKS](kms-data-encryption-concepts)[Update the key vault mode for an Azure Kubernetes Service (AKS) cluster with KMS etcd encryption](update-kms-key-vault)[Migrate to KMS v2 for etcd encryption in Azure Kubernetes Service (AKS)](use-kms-v2)[Observability for KMS etcd encryption in Azure Kubernetes Service (AKS)](kms-observability)


---

<!-- DOCUMENTO FUSIONADO: ingress-basic.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/ingress-basic -->

# Create an unmanaged ingress controller

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

An ingress controller is a piece of software that provides reverse proxy, configurable traffic routing, and TLS termination for Kubernetes services. Kubernetes ingress resources are used to configure the ingress rules and routes for individual Kubernetes services. When you use an ingress controller and ingress rules, a single IP address can be used to route traffic to multiple services in a Kubernetes cluster.

This article shows you how to deploy the [NGINX ingress controller](https://github.com/kubernetes/ingress-nginx) in an Azure Kubernetes Service (AKS) cluster. Two applications are then run in the AKS cluster, each of which is accessible over the single IP address.

Important

The Application routing add-on is recommended for ingress in AKS. For more information, see [Managed nginx Ingress with the application routing add-on](/en-us/azure/aks/app-routing).

Note

There are two open source ingress controllers for Kubernetes based on Nginx: one is maintained by the Kubernetes community ([kubernetes/ingress-nginx](https://github.com/kubernetes/ingress-nginx)), and one is maintained by NGINX, Inc. ([nginxinc/kubernetes-ingress](https://github.com/nginxinc/kubernetes-ingress)). This article will be using the Kubernetes community ingress controller.

## Before you begin

- This article uses Helm 3 to install the NGINX ingress controller on a
[supported version of Kubernetes](/en-us/azure/aks/supported-kubernetes-versions). Make sure that you're using the latest release of Helm and have access to the*ingress-nginx*Helm repository. The steps outlined in this article may not be compatible with previous versions of the Helm chart, NGINX ingress controller, or Kubernetes. - This article assumes you have an existing AKS cluster with an integrated Azure Container Registry (ACR). For more information on creating an AKS cluster with an integrated ACR, see
[Authenticate with Azure Container Registry from Azure Kubernetes Service](/en-us/azure/aks/cluster-container-registry-integration#create-a-new-acr). - The Kubernetes API health endpoint,
`healthz`

was deprecated in Kubernetes v1.16. You can replace this endpoint with the`livez`

and`readyz`

endpoints instead. See[Kubernetes API endpoints for health](https://kubernetes.io/docs/reference/using-api/health-checks/#api-endpoints-for-health)to determine which endpoint to use for your scenario. - If you're using Azure CLI, this article requires that you're running the Azure CLI version 2.0.64 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI][azure-cli-install]. - If you're using Azure PowerShell, this article requires that you're running Azure PowerShell version 5.9.0 or later. Run
`Get-InstalledModule -Name Az`

to find the version. If you need to install or upgrade, see[Install Azure PowerShell](/en-us/powershell/azure/install-azure-powershell).

## Basic configuration

To create a basic NGINX ingress controller without customizing the defaults, you'll use Helm. The following configuration uses the default configuration for simplicity. You can add parameters for customizing the deployment, like `--set controller.replicaCount=3`

.

Note

If you would like to enable [client source IP preservation](/en-us/azure/aks/concepts-network-ingress#ingress-controllers) for requests to containers in your cluster, add `--set controller.service.externalTrafficPolicy=Local`

to the Helm install command. The client source IP is stored in the request header under *X-Forwarded-For*. When you're using an ingress controller with client source IP preservation enabled, TLS pass-through won't work.

```
NAMESPACE=ingress-basic
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install ingress-nginx ingress-nginx/ingress-nginx \
--create-namespace \
--namespace $NAMESPACE \
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz \
--set controller.service.externalTrafficPolicy=Local
```


Note

In this tutorial, `service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path`

is being set to `/healthz`

. This means if the response code of the requests to `/healthz`

is not `200`

, the entire ingress controller will be down. You can modify the value to other URI in your own scenario. You cannot delete this part or unset the value, or the ingress controller will still be down.
The package `ingress-nginx`

used in this tutorial, which is provided by [Kubernetes official](https://github.com/kubernetes/ingress-nginx), will always return `200`

response code if requesting `/healthz`

, as it is designed as [default backend](https://kubernetes.github.io/ingress-nginx/user-guide/default-backend/) for users to have a quick start, unless it is being overwritten by ingress rules.

## Customized configuration

As an alternative to the basic configuration presented in the above section, the next set of steps will show how to deploy a customized ingress controller. You'll have the option of using an internal static IP address, or using a dynamic public IP address.

### Import the images used by the Helm chart into your ACR

To control image versions, you'll want to import them into your own Azure Container Registry. The [NGINX ingress controller Helm chart](https://github.com/kubernetes/ingress-nginx/tree/main/charts/ingress-nginx) relies on three container images. Use `az acr import`

to import those images into your ACR.

```
REGISTRY_NAME=<REGISTRY_NAME>
SOURCE_REGISTRY=registry.k8s.io
CONTROLLER_IMAGE=ingress-nginx/controller
CONTROLLER_TAG=v1.8.1
PATCH_IMAGE=ingress-nginx/kube-webhook-certgen
PATCH_TAG=v20230407
DEFAULTBACKEND_IMAGE=defaultbackend-amd64
DEFAULTBACKEND_TAG=1.5
az acr import --name $REGISTRY_NAME --source $SOURCE_REGISTRY/$CONTROLLER_IMAGE:$CONTROLLER_TAG --image $CONTROLLER_IMAGE:$CONTROLLER_TAG
az acr import --name $REGISTRY_NAME --source $SOURCE_REGISTRY/$PATCH_IMAGE:$PATCH_TAG --image $PATCH_IMAGE:$PATCH_TAG
az acr import --name $REGISTRY_NAME --source $SOURCE_REGISTRY/$DEFAULTBACKEND_IMAGE:$DEFAULTBACKEND_TAG --image $DEFAULTBACKEND_IMAGE:$DEFAULTBACKEND_TAG
```


Note

In addition to importing container images into your ACR, you can also import Helm charts into your ACR. For more information, see [Push and pull Helm charts to an Azure Container Registry](/en-us/azure/container-registry/container-registry-helm-repos).

### Create an ingress controller

To create the ingress controller, use Helm to install *ingress-nginx*. The ingress controller needs to be scheduled on a Linux node. Windows Server nodes shouldn't run the ingress controller. A node selector is specified using the `--set nodeSelector`

parameter to tell the Kubernetes scheduler to run the NGINX ingress controller on a Linux-based node.

For added redundancy, two replicas of the NGINX ingress controllers are deployed with the `--set controller.replicaCount`

parameter. To fully benefit from running replicas of the ingress controller, make sure there's more than one node in your AKS cluster.

The following example creates a Kubernetes namespace for the ingress resources named *ingress-basic* and is intended to work within that namespace. Specify a namespace for your own environment as needed. If your AKS cluster isn't Kubernetes role-based access control enabled, add `--set rbac.create=false`

to the Helm commands.

Note

If you would like to enable [client source IP preservation](/en-us/azure/aks/concepts-network-ingress#ingress-controllers) for requests to containers in your cluster, add `--set controller.service.externalTrafficPolicy=Local`

to the Helm install command. The client source IP is stored in the request header under *X-Forwarded-For*. When you're using an ingress controller with client source IP preservation enabled, TLS pass-through won't work.

```
# Add the ingress-nginx repository
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
# Set variable for ACR location to use for pulling images
ACR_LOGIN_SERVER=<REGISTRY_LOGIN_SERVER>
# Use Helm to deploy an NGINX ingress controller
helm install ingress-nginx ingress-nginx/ingress-nginx \
--version 4.7.1 \
--namespace ingress-basic \
--create-namespace \
--set controller.replicaCount=2 \
--set controller.nodeSelector."kubernetes\.io/os"=linux \
--set controller.image.registry=$ACR_LOGIN_SERVER \
--set controller.image.image=$CONTROLLER_IMAGE \
--set controller.image.tag=$CONTROLLER_TAG \
--set controller.image.digest="" \
--set controller.admissionWebhooks.patch.nodeSelector."kubernetes\.io/os"=linux \
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz \
--set controller.service.externalTrafficPolicy=Local \
--set controller.admissionWebhooks.patch.image.registry=$ACR_LOGIN_SERVER \
--set controller.admissionWebhooks.patch.image.image=$PATCH_IMAGE \
--set controller.admissionWebhooks.patch.image.tag=$PATCH_TAG \
--set controller.admissionWebhooks.patch.image.digest="" \
--set defaultBackend.nodeSelector."kubernetes\.io/os"=linux \
--set defaultBackend.image.registry=$ACR_LOGIN_SERVER \
--set defaultBackend.image.image=$DEFAULTBACKEND_IMAGE \
--set defaultBackend.image.tag=$DEFAULTBACKEND_TAG \
--set defaultBackend.image.digest=""
```


### Create an ingress controller using an internal IP address

By default, an NGINX ingress controller is created with a dynamic public IP address assignment. A common configuration requirement is to use an internal, private network and IP address. This approach allows you to restrict access to your services to internal users, with no external access.

Use the `--set controller.service.loadBalancerIP`

and `--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-internal"=true`

parameters to assign an internal IP address to your ingress controller. Provide your own internal IP address for use with the ingress controller. Make sure that this IP address isn't already in use within your virtual network. If you're using an existing virtual network and subnet, you must configure your AKS cluster with the correct permissions to manage the virtual network and subnet. For more information, see [Use kubenet networking with your own IP address ranges in Azure Kubernetes Service (AKS)](/en-us/azure/aks/configure-kubenet) or [Configure Azure CNI networking in Azure Kubernetes Service (AKS)](/en-us/azure/aks/configure-azure-cni?tabs=configure-networking-portal).

```
# Add the ingress-nginx repository
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
# Set variable for ACR location to use for pulling images
ACR_LOGIN_SERVER=<REGISTRY_LOGIN_SERVER>
# Use Helm to deploy an NGINX ingress controller
helm install ingress-nginx ingress-nginx/ingress-nginx \
--version 4.7.1 \
--namespace ingress-basic \
--create-namespace \
--set controller.replicaCount=2 \
--set controller.nodeSelector."kubernetes\.io/os"=linux \
--set controller.image.registry=$ACR_LOGIN_SERVER \
--set controller.image.image=$CONTROLLER_IMAGE \
--set controller.image.tag=$CONTROLLER_TAG \
--set controller.image.digest="" \
--set controller.admissionWebhooks.patch.nodeSelector."kubernetes\.io/os"=linux \
--set controller.service.loadBalancerIP=10.224.0.42 \
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-internal"=true \
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz \
--set controller.admissionWebhooks.patch.image.registry=$ACR_LOGIN_SERVER \
--set controller.admissionWebhooks.patch.image.image=$PATCH_IMAGE \
--set controller.admissionWebhooks.patch.image.tag=$PATCH_TAG \
--set controller.admissionWebhooks.patch.image.digest="" \
--set defaultBackend.nodeSelector."kubernetes\.io/os"=linux \
--set defaultBackend.image.registry=$ACR_LOGIN_SERVER \
--set defaultBackend.image.image=$DEFAULTBACKEND_IMAGE \
--set defaultBackend.image.tag=$DEFAULTBACKEND_TAG \
--set defaultBackend.image.digest=""
```


## Check the load balancer service

Check the load balancer service by using `kubectl get services`

.

```
kubectl get services --namespace ingress-basic -o wide -w ingress-nginx-controller
```


When the Kubernetes load balancer service is created for the NGINX ingress controller, an IP address is assigned under *EXTERNAL-IP*, as shown in the following example output:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE SELECTOR
ingress-nginx-controller LoadBalancer 10.0.65.205 EXTERNAL-IP 80:30957/TCP,443:32414/TCP 1m app.kubernetes.io/component=controller,app.kubernetes.io/instance=ingress-nginx,app.kubernetes.io/name=ingress-nginx
```


If you browse to the external IP address at this stage, you see a 404 page displayed. This is because you still need to set up the connection to the external IP, which is done in the next sections.

## Run demo applications

To see the ingress controller in action, run two demo applications in your AKS cluster. In this example, you use `kubectl apply`

to deploy two instances of a simple *Hello world* application.

Create an

`aks-helloworld-one.yaml`

file and copy in the following example YAML:`apiVersion: apps/v1 kind: Deployment metadata: name: aks-helloworld-one spec: replicas: 1 selector: matchLabels: app: aks-helloworld-one template: metadata: labels: app: aks-helloworld-one spec: containers: - name: aks-helloworld-one image: mcr.microsoft.com/azuredocs/aks-helloworld:v1 ports: - containerPort: 80 env: - name: TITLE value: "Welcome to Azure Kubernetes Service (AKS)" --- apiVersion: v1 kind: Service metadata: name: aks-helloworld-one spec: type: ClusterIP ports: - port: 80 selector: app: aks-helloworld-one`

Create an

`aks-helloworld-two.yaml`

file and copy in the following example YAML:`apiVersion: apps/v1 kind: Deployment metadata: name: aks-helloworld-two spec: replicas: 1 selector: matchLabels: app: aks-helloworld-two template: metadata: labels: app: aks-helloworld-two spec: containers: - name: aks-helloworld-two image: mcr.microsoft.com/azuredocs/aks-helloworld:v1 ports: - containerPort: 80 env: - name: TITLE value: "AKS Ingress Demo" --- apiVersion: v1 kind: Service metadata: name: aks-helloworld-two spec: type: ClusterIP ports: - port: 80 selector: app: aks-helloworld-two`

Run the two demo applications using

`kubectl apply`

:`kubectl apply -f aks-helloworld-one.yaml --namespace ingress-basic kubectl apply -f aks-helloworld-two.yaml --namespace ingress-basic`


## Create an ingress route

Both applications are now running on your Kubernetes cluster. To route traffic to each application, create a Kubernetes ingress resource. The ingress resource configures the rules that route traffic to one of the two applications.

In the following example, traffic to *EXTERNAL_IP/hello-world-one* is routed to the service named `aks-helloworld-one`

. Traffic to *EXTERNAL_IP/hello-world-two* is routed to the `aks-helloworld-two`

service. Traffic to *EXTERNAL_IP/static* is routed to the service named `aks-helloworld-one`

for static assets.

Create a file named

`hello-world-ingress.yaml`

and copy in the following example YAML:`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: hello-world-ingress annotations: nginx.ingress.kubernetes.io/ssl-redirect: "false" nginx.ingress.kubernetes.io/use-regex: "true" nginx.ingress.kubernetes.io/rewrite-target: /$2 spec: ingressClassName: nginx rules: - http: paths: - path: /hello-world-one(/|$)(.*) pathType: Prefix backend: service: name: aks-helloworld-one port: number: 80 - path: /hello-world-two(/|$)(.*) pathType: Prefix backend: service: name: aks-helloworld-two port: number: 80 - path: /(.*) pathType: Prefix backend: service: name: aks-helloworld-one port: number: 80 --- apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: hello-world-ingress-static annotations: nginx.ingress.kubernetes.io/ssl-redirect: "false" nginx.ingress.kubernetes.io/rewrite-target: /static/$2 spec: ingressClassName: nginx rules: - http: paths: - path: /static(/|$)(.*) pathType: Prefix backend: service: name: aks-helloworld-one port: number: 80`

Create the ingress resource using the

`kubectl apply`

command.`kubectl apply -f hello-world-ingress.yaml --namespace ingress-basic`


## Test the ingress controller

To test the routes for the ingress controller, browse to the two applications. Open a web browser to the IP address of your NGINX ingress controller, such as *EXTERNAL_IP*. The first demo application is displayed in the web browser, as shown in the following example:

Now add the */hello-world-two* path to the IP address, such as *EXTERNAL_IP/hello-world-two*. The second demo application with the custom title is displayed:

### Test an internal IP address

Create a test pod and attach a terminal session to it.

`kubectl run -it --rm aks-ingress-test --image=mcr.microsoft.com/dotnet/runtime-deps:6.0 --namespace ingress-basic`

Install

`curl`

in the pod using`apt-get`

.`apt-get update && apt-get install -y curl`

Access the address of your Kubernetes ingress controller using

`curl`

, such as. Provide your own internal IP address specified when you deployed the ingress controller.[http://10.224.0.42](http://10.224.0.42)`curl -L http://10.224.0.42`

No path was provided with the address, so the ingress controller defaults to the

*/*route. The first demo application is returned, as shown in the following condensed example output:`<!DOCTYPE html> <html xmlns="http://www.w3.org/1999/xhtml"> <head> <link rel="stylesheet" type="text/css" href="/static/default.css"> <title>Welcome to Azure Kubernetes Service (AKS)</title> [...]`

Add the

*/hello-world-two*path to the address, such as.[http://10.224.0.42/hello-world-two](http://10.224.0.42/hello-world-two)`curl -L -k http://10.224.0.42/hello-world-two`

The second demo application with the custom title is returned, as shown in the following condensed example output:

`<!DOCTYPE html> <html xmlns="http://www.w3.org/1999/xhtml"> <head> <link rel="stylesheet" type="text/css" href="/static/default.css"> <title>AKS Ingress Demo</title> [...]`


## Clean up resources

This article used Helm to install the ingress components and sample apps. When you deploy a Helm chart, many Kubernetes resources are created. These resources include pods, deployments, and services. To clean up these resources, you can either delete the entire sample namespace, or the individual resources.

### Delete the sample namespace and all resources

To delete the entire sample namespace, use the `kubectl delete`

command and specify your namespace name. All the resources in the namespace are deleted.

```
kubectl delete namespace ingress-basic
```


### Delete resources individually

Alternatively, a more granular approach is to delete the individual resources created.

List the Helm releases with the

`helm list`

command.`helm list --namespace ingress-basic`

Look for charts named

*ingress-nginx*and*aks-helloworld*, as shown in the following example output:`NAME NAMESPACE REVISION UPDATED STATUS CHART APP VERSION ingress-nginx ingress-basic 1 2020-01-06 19:55:46.358275 -0600 CST deployed nginx-ingress-1.27.1 0.26.1`

Uninstall the releases with the

`helm uninstall`

command.`helm uninstall ingress-nginx --namespace ingress-basic`

Remove the two sample applications.

`kubectl delete -f aks-helloworld-one.yaml --namespace ingress-basic kubectl delete -f aks-helloworld-two.yaml --namespace ingress-basic`

Remove the ingress route that directed traffic to the sample apps.

`kubectl delete -f hello-world-ingress.yaml`

Delete the namespace using the

`kubectl delete`

command and specifying your namespace name.`kubectl delete namespace ingress-basic`


## Next steps

To configure TLS with your existing ingress components, see [Use TLS with an ingress controller](/en-us/previous-versions/azure/aks/ingress-tls).

To configure your AKS cluster to use application routing, see [Application routing add-on](/en-us/azure/aks/app-routing).

This article included some external components to AKS. To learn more about these components, see the following project pages:
