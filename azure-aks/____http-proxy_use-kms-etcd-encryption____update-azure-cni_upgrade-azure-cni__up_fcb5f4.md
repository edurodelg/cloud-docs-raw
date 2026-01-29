---
merged_at: 2026-01-29T15:23:36.571447
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/http-proxy -->

# HTTP proxy support in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to configure Azure Kubernetes Service (AKS) clusters to use an HTTP proxy for outbound internet access.

AKS clusters deployed into managed or custom virtual networks have certain outbound dependencies that are necessary to function properly, which created problems in environments requiring internet access to be routed through HTTP proxies. Nodes had no way of bootstrapping the configuration, environment variables, and certificates necessary to access internet services.

The HTTP proxy feature adds HTTP proxy support to AKS clusters, exposing a straightforward interface that you can use to secure AKS-required network traffic in proxy-dependent environments. With this feature, both AKS nodes and pods are configured to use the HTTP proxy. The feature also enables installation of a trusted certificate authority onto the nodes as part of bootstrapping a cluster. More complex solutions might require creating a chain of trust to establish secure communications across the network.

## Limitations and considerations

The following scenarios are **not** supported:

- Different proxy configurations per node pool
- User/Password authentication
- Custom certificate authorities (CAs) for API server communication
- AKS clusters with Windows node pools
- Node pools using Virtual Machine Availability Sets (VMAS)
- Using * as wildcard attached to a domain suffix for noProxy

`httpProxy`

, `httpsProxy`

, and `trustedCa`

have no value by default. Pods are injected with the following environment variables:

`HTTP_PROXY`

`http_proxy`

`HTTPS_PROXY`

`https_proxy`

`NO_PROXY`

`no_proxy`


To disable the injection of the proxy environment variables, you need to annotate the Pod with `"kubernetes.azure.com/no-http-proxy-vars":"true"`

.

## Before you begin

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Create a configuration file with HTTP proxy values

Create a file and provide values for `httpProxy`

, `httpsProxy`

, and `noProxy`

. If your environment requires it, provide a value for `trustedCa`

.

The schema for the config file looks like this:

```
{
"httpProxy": "string",
"httpsProxy": "string",
"noProxy": [
"string"
],
"trustedCa": "string"
}
```


Review requirements for each parameter:

`httpProxy`

: A proxy URL to use for creating HTTP connections outside the cluster. The URL scheme must be`http`

.`httpsProxy`

: A proxy URL to use for creating HTTPS connections outside the cluster. If not specified, then`httpProxy`

is used for both HTTP and HTTPS connections.`noProxy`

: A list of destination domain names, domains, IP addresses, or other network CIDRs to exclude proxying.`trustedCa`

: A string containing the`base64 encoded`

alternative CA certificate content. Currently only the`PEM`

format is supported.

Important

For compatibility with Go-based components that are part of the Kubernetes system, the certificate **must** support `Subject Alternative Names(SANs)`

instead of the deprecated Common Name certs.

There are differences in applications on how to comply with the environment variable `http_proxy`

, `https_proxy`

, and `no_proxy`

. Curl and Python don't support CIDR in `no_proxy`

, but Ruby does.

Example input:

```
{
"httpProxy": "http://myproxy.server.com:8080",
"httpsProxy": "https://myproxy.server.com:8080",
"noProxy": [
"localhost",
"127.0.0.1"
],
"trustedCA": "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUgvVENDQmVXZ0F3SUJB...S0tLS0="
}
```


## Create a cluster with an HTTP proxy configuration using the Azure CLI

You can configure an AKS cluster with an HTTP proxy configuration during cluster creation.

Use the

command and pass in your configuration as a JSON file.`az aks create`

`az aks create \ --name $clusterName \ --resource-group $resourceGroup \ --http-proxy-config aks-proxy-config.json \ --generate-ssh-keys`

Your cluster should initialize with the HTTP proxy configured on the nodes.

Verify the HTTP proxy configuration is on the pods and nodes by checking that the environment variables contain the appropriate values for

`http_proxy`

,`https_proxy`

, and`no_proxy`

using the`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables are set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


## Update an HTTP proxy configuration

You can update HTTP proxy configurations on existing clusters, including:

- Updating an existing cluster to enable HTTP proxy and adding a new HTTP proxy configuration.
- Updating an existing cluster to change an HTTP proxy configuration.

### HTTP proxy update considerations

The `--http-proxy-config`

parameter should be set to a new JSON file with updated values for `httpProxy`

, `httpsProxy`

, `noProxy`

, and `trustedCa`

if necessary. The update injects new environment variables into pods with the new `httpProxy`

, `httpsProxy`

, or `noProxy`

values. Pods must be rotated for the apps to pick it up, because the environment variable values are injected by a mutating admission webhook.

Note

If switching to a new proxy, the new proxy must already exist for the update to be successful. After the upgrade is completed, you can delete the old proxy.

### Update a cluster to update or enable HTTP proxy

Enable or update HTTP proxy configurations on an existing cluster using the

command.`az aks update`

For example, let's say you created a new file with the base64 encoded string of the new CA cert called

*aks-proxy-config-2.json*. You can update the proxy configuration on your cluster with the following command:`az aks update --name $clusterName --resource-group $resourceGroup --http-proxy-config aks-proxy-config-2.json`


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Verify the HTTP proxy configuration is on the pods and nodes by checking that the environment variables contain the appropriate values for

`http_proxy`

,`https_proxy`

, and`no_proxy`

using the`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables are set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


## Disable HTTP proxy on an existing cluster (Preview)

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

**Disable HTTP Proxy requires a minimum of 18.0.0b13**.`az extension update --name aks-preview`


### Register `DisableHTTPProxyPreview`

feature flag

Register the

`DisableHTTPProxyPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name DisableHTTPProxyPreview`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name DisableHTTPProxyPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Update cluster to disable HTTP proxy (preview)

Update your cluster to disable HTTP proxy using the

command with`az aks update`

`--disable-http-proxy`

flag.`az aks update --name $clusterName --resource-group $resourceGroup --disable-http-proxy`


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Verify HTTP proxy is disabled by validating the HTTP proxy configuration isn't set on the pods and nodes using the

`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables aren't set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


### Re-enable HTTP proxy on an existing cluster

When you create a cluster, HTTP proxy is enabled by default. Once you disable HTTP proxy on a cluster, the proxy configuration is saved in the database but the proxy variables are removed from the pods and nodes.

To re-enable HTTP proxy on an existing cluster, use the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--enable-http-proxy`

flag.```
az aks update --name $clusterName --resource-group $resourceGroup --enable-http-proxy
```


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Important

If you had an HTTP proxy configuration on your cluster before disabling, the existing HTTP proxy configuration automatically applies when you re-enable HTTP proxy on that cluster. We recommend verifying the configuration to ensure it meets your current requirements before proceeding. If you want to change your HTTP proxy configuration after re-enabling HTTP proxy, follow the steps to [Update the HTTP proxy configuration on an existing cluster](#update-a-cluster-to-update-or-enable-http-proxy).

## Configure an HTTP proxy configuration using an Azure Resource Manager (ARM) template

You can deploy an AKS cluster with an HTTP proxy using an ARM template.

Review requirements for each parameter:

`httpProxy`

: A proxy URL to use for creating HTTP connections outside the cluster. The URL scheme must be`http`

.`httpsProxy`

: A proxy URL to use for creating HTTPS connections outside the cluster. If not specified, then`httpProxy`

is used for both HTTP and HTTPS connections.`noProxy`

: A list of destination domain names, domains, IP addresses, or other network CIDRs to exclude proxying.`trustedCa`

: A string containing the`base64 encoded`

alternative CA certificate content. Currently only the`PEM`

format is supported.

Important

For compatibility with Go-based components that are part of the Kubernetes system, the certificate

**must**support`Subject Alternative Names (SANs)`

instead of the deprecated Common Name certs.There are differences in applications on how to comply with the environment variable

`http_proxy`

,`https_proxy`

, and`no_proxy`

. Curl and Python don't support CIDR in`no_proxy`

, but Ruby does.Create a template with HTTP proxy parameters. In your template, provide values for

`httpProxy`

,`httpsProxy`

, and`noProxy`

. If necessary, provide a value for`trustedCa`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "httpProxyConfig": { "enabled": "true", "httpProxy": "string", "httpsProxy": "string", "noProxy": [ "string" ], "trustedCa": "string" } }`

Deploy your ARM template with the HTTP Proxy configuration. Your cluster should initialize with your HTTP proxy configured on the nodes.


## Update an HTTP proxy configuration

You can update HTTP proxy configurations on existing clusters, including:

- Updating an existing cluster to enable HTTP proxy and adding a new HTTP proxy configuration.
- Updating an existing cluster to change an HTTP proxy configuration.

### HTTP proxy update considerations

The `--http-proxy-config`

parameter should be set to a new JSON file with updated values for `httpProxy`

, `httpsProxy`

, `noProxy`

, and `trustedCa`

if necessary. The update injects new environment variables into pods with the new `httpProxy`

, `httpsProxy`

, or `noProxy`

values. Pods must be rotated for the apps to pick it up, because the environment variable values are injected by a mutating admission webhook.

Note

If switching to a new proxy, the new proxy must already exist for the update to be successful. After the upgrade is completed, you can delete the old proxy.

### Update an ARM template to configure HTTP proxy

In your template, provide new values for

`httpProxy`

,`httpsProxy`

, and`noProxy`

. If necessary, provide a value for`trustedCa`

.The same schema used for CLI deployment exists in the

`Microsoft.ContainerService/managedClusters`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "httpProxyConfig": { "enabled": "true", "httpProxy": "string", "httpsProxy": "string", "noProxy": [ "string" ], "trustedCa": "string" } }`

Deploy your ARM template with the updated HTTP Proxy configuration.


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Verify the HTTP proxy configuration is on the pods and nodes by checking that the environment variables contain the appropriate values for

`http_proxy`

,`https_proxy`

, and`no_proxy`

using the`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables are set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


## Disable HTTP proxy on an existing cluster using an ARM template (Preview)

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

**Disable HTTP Proxy requires a minimum of 18.0.0b13**.`az extension update --name aks-preview`


### Register `DisableHTTPProxyPreview`

feature flag

Register the

`DisableHTTPProxyPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name DisableHTTPProxyPreview`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name DisableHTTPProxyPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Update cluster to disable HTTP proxy

Update your cluster ARM template to disable HTTP proxy by setting

`enabled`

to`false`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "httpProxyConfig": { "enabled": "false", } }`

Deploy your ARM template with HTTP Proxy disabled.


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Verify HTTP proxy is disabled by validating that the HTTP Proxy configuration isn't set on the pods and nodes using the

`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables aren't set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


### Re-enable HTTP proxy on an existing cluster

When you create a cluster, HTTP proxy is enabled by default. Once you disable HTTP proxy on a cluster, you can no longer add HTTP proxy configurations to that cluster.

If you want to re-enable HTTP proxy, follow the steps to [Update an HTTP proxy configuration using an ARM template](#update-an-arm-template-to-configure-http-proxy).

## Istio add-on HTTP proxy for External Services

If you're using the [Istio-based service mesh add-on for AKS](istio-about), you must create a Service Entry to enable your applications in the mesh to access noncluster or external resources via the HTTP proxy.

For example:

```
apiVersion: networking.istio.io/v1
kind: ServiceEntry
metadata:
name: proxy
spec:
hosts:
- my-company-proxy.com # ignored
addresses:
- $PROXY_IP/32
ports:
- number: $PROXY_PORT
name: tcp
protocol: TCP
location: MESH_EXTERNAL
```


Create a file and provide values for

`PROXY_IP`

and`PROXY_PORT`

.You can deploy the Service Entry using:

`kubectl apply -f service_proxy.yaml`


## Monitoring add-on configuration

HTTP proxy with the monitoring add-on supports the following configurations:

- Outbound proxy without authentication
- Outbound proxy with trusted cert for Log Analytics endpoint

The following configuration isn't supported:

- Custom Metrics and Recommended Alerts features when using a proxy with trusted certificates

## Next steps

For more information regarding the network requirements of AKS clusters, see [Control egress traffic for cluster nodes in AKS](limit-egress-traffic).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-kms-etcd-encryption -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/update-azure-cni -->

# Update Azure CNI IPAM mode and data plane technology for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Existing Azure Kubernetes Service (AKS) clusters inevitably need an update to newer IP assignment management (IPAM) modes and data plane technologies to access the latest features and supportability. This article provides guidance on updating an existing AKS cluster to use Azure CNI Overlay for the IPAM mode and Azure CNI Powered by Cilium as the data plane.

## Update the IPAM mode to Azure CNI Overlay

Updating an existing cluster to Azure CNI Overlay is an irreversible process.

You can update an existing AKS cluster to Azure CNI Overlay if the cluster:

- Is on Kubernetes version 1.27 or later.
- Doesn't use the
[dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)feature. - Doesn't have network policies enabled. If you need to uninstall the network policy engine before updating your cluster, follow the steps in
[Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico). - Doesn't use any Windows node pools with Docker as the container runtime.

Before Windows OS build 20348.1668, there was a limitation around Windows overlay pods incorrectly routing packets from host network pods via Source Network Address Translation (SNAT). This limitation had a detrimental effect for clusters that were updating to Azure CNI Overlay. To avoid this issue, use Windows OS build 20348.1668 or later.

Warning

If you're using a custom

`azure-ip-masq-agent`

configuration to include additional IP ranges that shouldn't send SNAT packets from pods, updating to Azure CNI Overlay can break connectivity to these ranges. Pod IPs from the overlay space are unreachable by anything outside the cluster nodes.For old clusters, a ConfigMap might be left over from a previous version of

`azure-ip-masq-agent`

. If this ConfigMap (named`azure-ip-masq-agent-config`

) exists and isn't intentionally in place, you should delete it before updating.If you're not using a custom

`ip-masq-agent`

configuration, only the`azure-ip-masq-agent-config-reconciled`

ConfigMap should exist with respect to Azure`ip-masq-agent`

ConfigMap. It's updated automatically during the update process.

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately to Azure CNI Overlay isn't supported. Any disruptions to cluster networking are similar to a node image update or Kubernetes version upgrade where each node in a node pool is reimaged.

Update an existing Azure Container Networking Interface (CNI) cluster to use Azure CNI Overlay by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16
```


The `--pod-cidr`

parameter is required when you update from legacy CNI plugins because the pods need to get IPs from a new overlay space. The new overlay space doesn't overlap with the existing Azure CNI Node Subnet plugin.

Classless Inter-Domain Routing (CIDR) for the pod also can't overlap with any virtual network address of the node pools. For example, if your virtual network address is 10.0.0.0/8, and your nodes are in the subnet 10.240.0.0/16, the `--pod-cidr`

parameter can't overlap with 10.0.0.0/8 or the existing service CIDR on the cluster.

## Update the data plane to Azure CNI Powered by Cilium

When you enable Cilium in a cluster that uses a different network policy engine (Azure Network Policy Manager or Calico), the network policy engine is uninstalled and replaced with Cilium. For more information, see [Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico).

You can update an existing cluster to Azure CNI Powered by Cilium if the cluster doesn't have any Windows node pools.

Warning

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image update or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium begins enforcing network policies only after all nodes are reimaged.

To perform the update, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

Update an existing cluster to Azure CNI Powered by Cilium by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-dataplane cilium
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-azure-cni -->

# Update Azure CNI IPAM mode and data plane technology for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Existing Azure Kubernetes Service (AKS) clusters inevitably need an update to newer IP assignment management (IPAM) modes and data plane technologies to access the latest features and supportability. This article provides guidance on updating an existing AKS cluster to use Azure CNI Overlay for the IPAM mode and Azure CNI Powered by Cilium as the data plane.

## Update the IPAM mode to Azure CNI Overlay

Updating an existing cluster to Azure CNI Overlay is an irreversible process.

You can update an existing AKS cluster to Azure CNI Overlay if the cluster:

- Is on Kubernetes version 1.27 or later.
- Doesn't use the
[dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)feature. - Doesn't have network policies enabled. If you need to uninstall the network policy engine before updating your cluster, follow the steps in
[Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico). - Doesn't use any Windows node pools with Docker as the container runtime.

Before Windows OS build 20348.1668, there was a limitation around Windows overlay pods incorrectly routing packets from host network pods via Source Network Address Translation (SNAT). This limitation had a detrimental effect for clusters that were updating to Azure CNI Overlay. To avoid this issue, use Windows OS build 20348.1668 or later.

Warning

If you're using a custom

`azure-ip-masq-agent`

configuration to include additional IP ranges that shouldn't send SNAT packets from pods, updating to Azure CNI Overlay can break connectivity to these ranges. Pod IPs from the overlay space are unreachable by anything outside the cluster nodes.For old clusters, a ConfigMap might be left over from a previous version of

`azure-ip-masq-agent`

. If this ConfigMap (named`azure-ip-masq-agent-config`

) exists and isn't intentionally in place, you should delete it before updating.If you're not using a custom

`ip-masq-agent`

configuration, only the`azure-ip-masq-agent-config-reconciled`

ConfigMap should exist with respect to Azure`ip-masq-agent`

ConfigMap. It's updated automatically during the update process.

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately to Azure CNI Overlay isn't supported. Any disruptions to cluster networking are similar to a node image update or Kubernetes version upgrade where each node in a node pool is reimaged.

Update an existing Azure Container Networking Interface (CNI) cluster to use Azure CNI Overlay by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16
```


The `--pod-cidr`

parameter is required when you update from legacy CNI plugins because the pods need to get IPs from a new overlay space. The new overlay space doesn't overlap with the existing Azure CNI Node Subnet plugin.

Classless Inter-Domain Routing (CIDR) for the pod also can't overlap with any virtual network address of the node pools. For example, if your virtual network address is 10.0.0.0/8, and your nodes are in the subnet 10.240.0.0/16, the `--pod-cidr`

parameter can't overlap with 10.0.0.0/8 or the existing service CIDR on the cluster.

## Update the data plane to Azure CNI Powered by Cilium

When you enable Cilium in a cluster that uses a different network policy engine (Azure Network Policy Manager or Calico), the network policy engine is uninstalled and replaced with Cilium. For more information, see [Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico).

You can update an existing cluster to Azure CNI Powered by Cilium if the cluster doesn't have any Windows node pools.

Warning

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image update or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium begins enforcing network policies only after all nodes are reimaged.

To perform the update, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

Update an existing cluster to Azure CNI Powered by Cilium by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-dataplane cilium
```

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-node-pools -->

# Upgrade node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to upgrade a single node pool and how to upgrade the cluster control plane for multiple node pools in Azure Kubernetes Service (AKS).

Note

As a best practice, you should upgrade all node pools in an AKS cluster to the same Kubernetes version. The default behavior of [`az aks upgrade`

][az-aks-upgrade] is to upgrade all node pools together with the control plane to achieve this alignment. The ability to upgrade individual node pools lets you perform a rolling upgrade and schedule pods between node pools to maintain application uptime.

## Upgrade a single node pool

Note

The node pool operating system (OS) image version is tied to the Kubernetes version of the cluster. You only get OS image upgrades following a cluster upgrade.

Check for any available upgrades using the [

`az aks get-upgrades`

][az-aks-get-upgrades] command.`az aks get-upgrades --resource-group <resource-group-name> --name <cluster-name>`

Upgrade a specific node pool using the [

`az aks nodepool upgrade`

][az-aks-nodepool-upgrade] command.`az aks nodepool upgrade \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --kubernetes-version <kubernetes-version> \ --no-wait`

Check the status of your node pool using the [

`az aks nodepool list`

][az-aks-nodepool-list] command.`az aks nodepool list --resource-group <resource-group-name> --cluster-name <cluster-name>`

The following example output shows the node pool is in the

*Upgrading*state:`[ { ... "count": 3, ... "name": "<node-pool-name>", "orchestratorVersion": "<kubernetes-version>", ... "provisioningState": "Upgrading", ... "vmSize": "Standard_DS2_v2", ... }, { ... "count": 2, ... "name": "<node-pool-name-2>", "orchestratorVersion": "<kubernetes-version-2>", ... "provisioningState": "Succeeded", ... "vmSize": "Standard_DS2_v2", ... } ]`

It takes a few minutes to upgrade the nodes to the specified version. After the upgrade is complete, the node pool's

`provisioningState`

changes to*Succeeded*.

## Upgrade a cluster control plane with multiple node pools

An AKS cluster has two cluster resource objects with Kubernetes versions associated to them: the cluster control plane Kubernetes version and a node pool with a Kubernetes version.

### Upgrade behavior for the control plane and node pools

The control plane maps to one or many node pools. The behavior of an upgrade operation depends on which Azure CLI command you use and the flags you specify:

upgrades the control plane and all node pools in the cluster to the same Kubernetes version.`az aks upgrade`

with the`az aks upgrade`

`--control-plane-only`

flag upgrades only the cluster control plane and leaves all node pools unchanged.upgrades only the target node pool with the specified Kubernetes version.`az aks nodepool upgrade`


### Validation rules for upgrades

Note

Kubernetes uses the standard [Semantic Versioning](https://semver.org/) versioning scheme. The version number is expressed as *x.y.z*, where *x* is the major version, *y* is the minor version, and *z* is the patch version. For example, in version *1.12.6*, *1* is the major version, *12* is the minor version, and *6* is the patch version. The Kubernetes version of the control plane and the initial node pool are set during cluster creation. Other node pools have their Kubernetes version set when they are added to the cluster. The Kubernetes versions may differ between node pools and between a node pool and the control plane.

Kubernetes upgrades for a cluster control plane and node pools are validated using the following sets of rules:

**Rules for valid versions to upgrade node pools**:- The node pool version must have the same
*major*version as the control plane. - The node pool
*minor*version must be within two*minor*versions of the control plane version. - The node pool version can't be greater than the control
`major.minor.patch`

version.

- The node pool version must have the same
**Rules for submitting an upgrade operation**:- You can't downgrade the control plane or a node pool Kubernetes version.
- If a node pool Kubernetes version isn't specified, the behavior depends on the client. In Azure Resource Manager (ARM) templates, declaration falls back to the existing version defined for the node pool. If nothing is set, it falls back to the control plane version.
- You can't simultaneously submit multiple operations on a single control plane or node pool resource. You can either upgrade or scale a control plane or a node pool at a given time.


## Next steps: Manage node pools in AKS

To learn more about managing node pools in AKS, see [Manage node pools in Azure Kubernetes Service (AKS)](manage-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/stop-cluster-upgrade-api-breaking-changes -->

# Stop Azure Kubernetes Service (AKS) cluster upgrades automatically on API breaking changes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to stop Azure Kubernetes Service (AKS) cluster upgrades automatically on API breaking changes.

## Overview

To stay within a supported Kubernetes version, you have to upgrade your cluster at least once per year and prepare for all possible disruptions. These disruptions include ones caused by API breaking changes, deprecations, and dependencies such as Helm and Container Storage Interface (CSI). It can be difficult to anticipate these disruptions and migrate critical workloads without experiencing any downtime.

You can configure your AKS cluster to automatically stop upgrade operations consisting of a minor version change with deprecated APIs and alert you to the issue. This feature helps you avoid unexpected disruptions and gives you time to address the deprecated APIs before proceeding with the upgrade.

## Before you begin

Before you begin, make sure you meet the following prerequisites:

- The upgrade operation is a Kubernetes minor version change for the cluster control plane.
- The Kubernetes version you're upgrading to is 1.26 or later.
- The last seen usage of deprecated APIs for the targeted version you're upgrading to must occur within 12 hours before the upgrade operation. AKS records usage hourly, so any usage of deprecated APIs within one hour isn't guaranteed to appear in the detection.

## Mitigate stopped upgrade operations

If you meet the [prerequisites](#before-you-begin), attempt an upgrade, and receive an error message similar to the following example error message:

```
Bad Request({
"code": "ValidationError",
"message": "Control Plane upgrade is blocked due to recent usage of a Kubernetes API deprecated in the specified version. Please refer to https://kubernetes.io/docs/reference/using-api/deprecation-guide to migrate the usage. To bypass this error, set enable-force-upgrade in upgradeSettings.overrideSettings. Bypassing this error without migrating usage will result in the deprecated Kubernetes API calls failing. Usage details: 1 error occurred:\n\t* usage has been detected on API flowcontrol.apiserver.k8s.io.prioritylevelconfigurations.v1beta1, and was recently seen at: 2023-03-23 20:57:18 +0000 UTC, which will be removed in 1.26\n\n",
"subcode": "UpgradeBlockedOnDeprecatedAPIUsage"
})
```


You have two options to mitigate the issue: you can [remove usage of deprecated APIs (recommended)](#remove-usage-of-deprecated-apis-recommended) or [bypass validation to ignore API changes](#bypass-validation-to-ignore-api-changes).

### Remove usage of deprecated APIs (recommended)

In the Azure portal, navigate to your cluster resource and select

**Diagnose and solve problems**Select

**Create, Upgrade, Delete, and Scale**>**Kubernetes API deprecations**.Wait 12 hours from the time the last deprecated API usage was seen. Read-Only verbs are excluded from the deprecated api usage namely

[Get/List/Watch](https://kubernetes.io/docs/reference/using-api/api-concepts/).(You can also check past API usage by enabling[Container insights](/en-us/azure/azure-monitor/containers/container-insights-log-query#resource-logs)and exploring kube audit logs.)Retry your cluster upgrade.


### Bypass validation to ignore API changes

Note

This method requires you to use the Azure CLI version 2.57 or later. If you have the preview CLI extension installed, you need to update to version `3.0.0b10`

or later. This method isn't recommended, as deprecated APIs in the targeted Kubernetes version might not work long term. We recommend removing them as soon as possible after the upgrade completes.

Bypass validation to ignore API breaking changes and invoke an upgrade. Specify the

`enable-force-upgrade`

flag and set the`upgrade-override-until`

property to define the end of the window during which validation is bypassed. If no value is set, it defaults the window to three days from the current time. The date and time you specify must be in the future.`az aks upgrade --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME --kubernetes-version $KUBERNETES_VERSION --enable-force-upgrade --upgrade-override-until 2023-10-01T13:00:00Z`

Note

`Z`

is the zone designator for the zero UTC/GMT offset, also known as 'Zulu' time. This example sets the end of the window to`13:00:00`

GMT. For more information, see[Combined date and time representations](https://wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).

## Next steps

This article showed you how to stop AKS cluster upgrades automatically on API breaking changes. To learn more about more upgrade options for AKS clusters, see [Upgrade options for Azure Kubernetes Service (AKS) clusters](upgrade-cluster).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-metrics -->

# What is container network metrics?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Advanced Container Networking Services in Azure Kubernetes Service (AKS) facilitates the collection of comprehensive container network metrics to give you valuable insights into the performance of your containerized environment. The capability continuously captures essential metrics at the node level and pod level, including traffic volume, dropped packets, connection states, and Domain Name System (DNS) resolution times for effective monitoring and optimizing network performance.

Capturing these metrics is essential for understanding how containers communicate, how traffic flows between services, and where bottlenecks or disruptions might occur. Advanced Container Networking Services integrates seamlessly with monitoring tools like Prometheus and Grafana to give you a complete view of networking metrics. Use the metrics for in-depth troubleshooting, network optimization, and performance tuning.

In a cloud-native world, maintaining a healthy and efficient network in a dynamic containerized environment is vital to ensuring that applications perform as expected. Without proper visibility into network traffic and its patterns, identifying potential issues or inefficiencies becomes challenging.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Key benefits

Deep visibility into network performance

Enhanced troubleshooting and optimization

Proactive anomaly detection

Better resource management and scaling

Capacity planning and compliance

Source-level metrics filtering for cost optimization and noise reduction with

[container network metrics filtering](#container-network-metrics-filtering-preview)Simplified metrics storage and visualization options. Choose between:

**Azure managed service for Prometheus and Azure Managed Grafana**: Azure manages the infrastructure and maintenance, so you can focus on configuring metrics and visualizing metrics.**Bring your own (BYO) Prometheus and Grafana**: You deploy and configure your own instances of Prometheus and Grafana, and you manage the underlying infrastructure.


## Metrics captured

### Node-level metrics

Understanding the health of your container network at the node-level is crucial for maintaining optimal application performance. These metrics provide insights into traffic volume, dropped packets, number of connections, and other data by node. The metrics are stored in Prometheus format, so, you can view them in Grafana.

The following metrics are aggregated per node. All metrics include one of these labels:

`cluster`

`instance`

(node name)

For Cilium data plane scenarios, Container Network Observability provides metrics only for Linux. Windows is currently not supported. Cilium exposes several metrics including the following used by Container Network Observability.

| Metric name | Description | Extra labels | Linux | Windows |
|---|---|---|---|---|
cilium_forward_count_total |
Total forwarded packet count | `direction` |
✅ | ❌ |
cilium_forward_bytes_total |
Total forwarded byte count | `direction` |
✅ | ❌ |
cilium_drop_count_total |
Total dropped packet count | `direction` , `reason` |
✅ | ❌ |
cilium_drop_bytes_total |
Total dropped byte count | `direction` , `reason` |
✅ | ❌ |

### Pod-level metrics (Hubble metrics)

These Prometheus metrics include source and destination pod information so that you can pinpoint network-related issues at a granular level. Metrics cover information like traffic volume, dropped packets, TCP resets, and Layer 4/Layer 7 packet flows. DNS metrics like DNS errors and DNS requests missing responses are collected by default for non-Cilium data planes. For Cilium data planes, a Cilium FQDN network policy is required to collect DNS metrics, or customers can also troubleshoot DNS using Hubble CLI and observing real-time logs.

The following table describes the metrics that are aggregated per pod (node information is preserved).

All metrics include labels:

`cluster`

`instance`

(node name)`source`

or`destination`

For

*outgoing traffic*, a`source`

label that indicates the source pod namespace and name is applied.For

*incoming traffic*, a`destination`

label that indicates the destination pod namespace and name is applied.


| Metric name | Description | Extra Labels | Linux | Windows |
|---|---|---|---|---|
hubble_dns_queries_total |
Total DNS requests by query | `source` or `destination` , `query` , `qtypes` (query type) |
✅ | ❌ |
hubble_dns_responses_total |
Total DNS responses by query/response | `source` or `destination` , `query` , `qtypes` (query type), `rcode` (return code), `ips_returned` (number of IPs) |
✅ | ❌ |
hubble_drop_total |
Total dropped packet count | `source` or `destination` , `protocol` , `reason` |
✅ | ❌ |
hubble_tcp_flags_total |
Total TCP packets count by flag | `source` or `destination` , `flag` |
✅ | ❌ |
hubble_flows_processed_total |
Total network flows processed (Layer 4/Layer 7 traffic) | `source` or `destination` , `protocol` , `verdict` , `type` , `subtype` |
✅ | ❌ |

## Container network metrics filtering (Preview)

Now that you have the ability to collect comprehensive metrics at both node and pod levels, you might find yourself dealing with a significant volume of data. To help reduce noise and optimize storage costs, Container Network Observability introduces **container network metrics filtering**. This feature enables you to filter metrics at the source before they are collected and stored, giving you control over which metrics are most relevant to your specific monitoring and troubleshooting needs. This feature is only available for Cilium clusters.

Container network metrics filtering is particularly valuable in large-scale production environments where the sheer volume of metrics can impact storage costs and query performance. By filtering out unnecessary metrics early in the collection process, you can focus on the data that matters most to your operations while maintaining the visibility you need for effective network monitoring.

The filtering capability supports multiple dimensions including namespace-based filtering to focus on specific applications, pod and label-based filtering for targeted monitoring, and metric-specific filtering to collect only the types of metrics that are essential for your use case. This flexibility allows you to strike the right balance between comprehensive observability and cost-effective operations.

To learn more on how to enable container network metrics filtering, see [How to Configure Container Network Metrics Filtering ](how-to-configure-container-network-metrics-filtering).

### Limitations

- Pod-level metrics are available only on Linux.
- Cilium data plane is supported starting with Kubernetes version 1.29.
- Metric labels have subtle differences between Cilium and non-Cilium clusters.
- For Cilium based clusters, DNS metrics are only available for pods that have Cilium Network policies (CNP) configured on their clusters, or customers can also troubleshoot DNS using Hubble CLI and observing real-time logs.
- Flow logs are not currently available in the air gapped cloud.
- Hubble relay may crash if one of the Hubble node agents goes down and may cause interruptions to Hubble CLI.
- When using Advanced Container Networking Services (ACNS) on non-Cilium data planes, FIPS support isn't available on Ubuntu 20.04 nodes due to kernel restrictions. To enable FIPS in this scenario, you must use an Azure Linux node pool. This limitation is expected to be resolved with the release of Ubuntu 22 FIPS. For updates, see the
[AKS issue tracker](https://github.com/Azure/AKS/issues/4857). - Container network metrics filtering is only available for Cilium Clusters.

Refer to the FIPS support matrix below:

| Operating System | FIPS Support |
|---|---|
| Azure Linux 3.0 | Yes |
| Azure Linux 2.0 | Yes |
| Ubuntu 20.04 | No |

This limitation does not apply when ACNS is running on Cilium data planes.

### Scale

The managed service for Prometheus in Azure Monitor and Azure Managed Grafana impose service-specific scale limitations. For more information, see [Scrape Prometheus metrics at scale in Azure Monitor](/en-us/azure/azure-monitor/essentials/prometheus-metrics-scrape-scale).

## Pricing

Important

Advanced Container Networking Services is a paid offering.

For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Related content

- To create an AKS cluster by using Container Network Observability to capture metrics, see
[Set up Container Network Observability for AKS](container-network-observability-how-to). - Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services. - Explore the
[Container Network Security feature](advanced-container-networking-services-overview#container-network-security)in Advanced Container Networking Services.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-aks-ipam-and-dataplane -->

# Update Azure CNI IPAM mode and data plane technology for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Existing Azure Kubernetes Service (AKS) clusters inevitably need an update to newer IP assignment management (IPAM) modes and data plane technologies to access the latest features and supportability. This article provides guidance on updating an existing AKS cluster to use Azure CNI Overlay for the IPAM mode and Azure CNI Powered by Cilium as the data plane.

## Update the IPAM mode to Azure CNI Overlay

Updating an existing cluster to Azure CNI Overlay is an irreversible process.

You can update an existing AKS cluster to Azure CNI Overlay if the cluster:

- Is on Kubernetes version 1.27 or later.
- Doesn't use the
[dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)feature. - Doesn't have network policies enabled. If you need to uninstall the network policy engine before updating your cluster, follow the steps in
[Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico). - Doesn't use any Windows node pools with Docker as the container runtime.

Before Windows OS build 20348.1668, there was a limitation around Windows overlay pods incorrectly routing packets from host network pods via Source Network Address Translation (SNAT). This limitation had a detrimental effect for clusters that were updating to Azure CNI Overlay. To avoid this issue, use Windows OS build 20348.1668 or later.

Warning

If you're using a custom

`azure-ip-masq-agent`

configuration to include additional IP ranges that shouldn't send SNAT packets from pods, updating to Azure CNI Overlay can break connectivity to these ranges. Pod IPs from the overlay space are unreachable by anything outside the cluster nodes.For old clusters, a ConfigMap might be left over from a previous version of

`azure-ip-masq-agent`

. If this ConfigMap (named`azure-ip-masq-agent-config`

) exists and isn't intentionally in place, you should delete it before updating.If you're not using a custom

`ip-masq-agent`

configuration, only the`azure-ip-masq-agent-config-reconciled`

ConfigMap should exist with respect to Azure`ip-masq-agent`

ConfigMap. It's updated automatically during the update process.

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately to Azure CNI Overlay isn't supported. Any disruptions to cluster networking are similar to a node image update or Kubernetes version upgrade where each node in a node pool is reimaged.

Update an existing Azure Container Networking Interface (CNI) cluster to use Azure CNI Overlay by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16
```


The `--pod-cidr`

parameter is required when you update from legacy CNI plugins because the pods need to get IPs from a new overlay space. The new overlay space doesn't overlap with the existing Azure CNI Node Subnet plugin.

Classless Inter-Domain Routing (CIDR) for the pod also can't overlap with any virtual network address of the node pools. For example, if your virtual network address is 10.0.0.0/8, and your nodes are in the subnet 10.240.0.0/16, the `--pod-cidr`

parameter can't overlap with 10.0.0.0/8 or the existing service CIDR on the cluster.

## Update the data plane to Azure CNI Powered by Cilium

When you enable Cilium in a cluster that uses a different network policy engine (Azure Network Policy Manager or Calico), the network policy engine is uninstalled and replaced with Cilium. For more information, see [Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico).

You can update an existing cluster to Azure CNI Powered by Cilium if the cluster doesn't have any Windows node pools.

Warning

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image update or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium begins enforcing network policies only after all nodes are reimaged.

To perform the update, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

Update an existing cluster to Azure CNI Powered by Cilium by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-dataplane cilium
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-byo-cni -->

# Bring your own CNI plugin with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes doesn't provide a network interface system by default. Instead, [network plugins](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/) provide this functionality. Azure Kubernetes Service (AKS) provides several supported Container Network Interface (CNI) plugins. For information on supported plugins, see [Networking concepts for applications in Azure Kubernetes Service](concepts-network).

The supported plugins meet most networking needs in Kubernetes. However, advanced AKS users might want the same CNI plugin that they used in on-premises Kubernetes environments. Or these users might want to use advanced functionalities available in other CNI plugins.

This article shows how to deploy an AKS cluster with no CNI plugin preinstalled. From there, you can install any CNI plugin that works in Azure.

## Support

Microsoft support can't assist with CNI-related issues in clusters that you deploy by bringing your own CNI plugin. For example, CNI-related issues would cover most east/west (pod to pod) traffic, along with `kubectl proxy`

and similar commands. If you want CNI-related support, use a supported AKS network plugin or seek support from the CNI plugin vendor.

Microsoft still provides support for issues that aren't related to CNI.

## Prerequisites

- For Azure Resource Manager or Bicep, use at least template version 2022-01-02-preview or 2022-06-01.
- For the Azure CLI, use at least version 2.39.0.
- The virtual network for the AKS cluster must allow outbound internet connectivity.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for the address range for the Kubernetes service, pods, or cluster virtual network. - The cluster identity that the AKS cluster uses must have at least
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)permissions on the subnet within your virtual network. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, the following permissions are required:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


- The subnet assigned to the AKS node pool can't be a
[delegated subnet](/en-us/azure/virtual-network/subnet-delegation-overview). - AKS doesn't apply network security groups (NSGs) to its subnet or modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure that the security rules in the NSGs allow traffic within the node's Classless Inter-Domain Routing (CIDR) range. For more information, see
[Network security groups](concepts-network#network-security-groups). - AKS doesn't create a route table in the managed virtual network.
- You must specify a Pod CIDR (IP address range for pods). The AKS control plane uses this range for internal traffic routing to pods, even though pod IP assignment will be managed by your custom CNI. If no pod CIDR is provided, control plane to pod communication may fail or be misrouted. You must select a pod CIDR that does not conflict with any other network in your environment and avoids Azure reserved ranges, such as,
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

. For example, you might use a range such as`10.XX.0.0/16`

that is unique to your cluster. This ensures that the control plane can route directly to pod IPs on your nodes, and no IP overlap will occur if you integrate with other networks or clusters.

## Create an AKS cluster with no CNI plugin preinstalled

Create an Azure resource group for your AKS cluster by using the

command.`az group create`

`az group create --location eastus --name myResourceGroup`

Create an AKS cluster by using the

command. Pass the`az aks create`

`--network-plugin`

parameter with the parameter value of`none`

.`az aks create \ --location eastus \ --resource-group myResourceGroup \ --name myAKSCluster \ --network-plugin none \ --pod-cidr "10.10.0.0/16" \ --generate-ssh-keys`


## Deploy a CNI plugin

After AKS provisioning finishes, the cluster is online. But all the nodes are in a `NotReady`

state, as shown in the following example:

```
$ kubectl get nodes
NAME STATUS ROLES AGE VERSION
aks-nodepool1-23902496-vmss000000 NotReady agent 6m9s v1.21.9
$ kubectl get node -o custom-columns='NAME:.metadata.name,STATUS:.status.conditions[?(@.type=="Ready")].message'
NAME STATUS
aks-nodepool1-23902496-vmss000000 container runtime network not ready: NetworkReady=false reason:NetworkPluginNotReady message:Network plugin returns error: cni plugin not initialized
```


At this point, the cluster is ready for installation of a CNI plugin.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-cvm -->

# Use Confidential Virtual Machines (CVM) in Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Confidential Virtual Machines (CVM)](/en-us/azure/confidential-computing/confidential-vm-overview) offer strong security and confidentiality for tenants. CVMs offer VM based Hardware Trusted Execution Environment (TEE) that leverage SEV-SNP security features to deny the hypervisor and other host management code access to VM memory and state, providing defense in depth protections against operator access. These features enable node pools with CVM to target the migration of highly sensitive container workloads to AKS without any code refactoring while benefiting from the features of AKS. For example, you may require CVM if you have the following:

- Workloads that handle security critical data and/or sensitive customer data
- Services that are required to meet various compliance requirements, especially for government contracts. Without a scalable solution for securing data, this could potentially lead to the loss of accreditations and contracts.

In this article, you learn how to create AKS node pools using Confidential VM sizes.

## AKS supported confidential VM sizes

Azure offers a choice of [Trusted Execution Environment (TEE)](/en-us/azure/confidential-computing/trusted-execution-environment) options from both AMD and Intel. These TEEs allow you to create Confidential VM environments with excellent price-to-performance ratios, all without requiring any code changes.

- AMD-based Confidential VMs, use AMD SEV-SNP technology, which is introduced with third Gen AMD EPYC™ processors.
- Intel-based Confidential VMs use Intel TDX, with fourth Gen Intel® Xeon® processors.

Both technologies have different implementations. However both provide similar protections from the cloud infrastructure stack. For more information, see [CVM VM sizes](/en-us/azure/confidential-computing/virtual-machine-options).

## Security Features

CVMs offer the following security enhancements as compared to other virtual machine (VM) sizes:

- Robust hardware-based isolation between virtual machines, hypervisor, and host management code.
- Customizable attestation policies to ensure the host's compliance before deployment.
- Cloud-based Confidential OS disk encryption before the first boot.
- VM encryption keys that the platform or the customer (optionally) owns and manages.
- Secure key release with cryptographic binding between the platform's successful attestation and the VM's encryption keys.
- Dedicated virtual Trusted Platform Module (TPM) instance for attestation and protection of keys and secrets in the virtual machine.
- Secure boot capability similar to Trusted launch for Azure VMs

## How does it work?

If you're running a workload that requires enhanced confidentiality and integrity, you can benefit from memory encryption and enhanced security without code changes in your application. All pods on your CVM node are part of the same trust boundary. The nodes in a node pool created with CVM use a customized [node image](node-images) specially configured for CVM.

### Supported OS Versions

You can create CVM node pools on Linux OS types (Ubuntu and Azure Linux). However, not all OS versions support CVM node pools.

This table includes the supported OS versions:

| OS Type | OS SKU | CVM support | CVM default |
|---|---|---|---|
| Linux | `Ubuntu` |
Supported | Ubuntu 20.04 is default for K8s version 1.24-1.33. Ubuntu 24.04 is the default for K8s version 1.34-1.38. |
| Linux | `Ubuntu2204` |
Not Supported | AKS doesn't support CVM for Ubuntu 22.04. |
| Linux | `Ubuntu2404` |
Supported | CVM is supported on `Ubuntu2404` in K8s 1.32-1.38. |
| Linux | `AzureLinux` |
Supported on Azure Linux 3.0 | Azure Linux 3 is default when enabling CVM for K8s version 1.28-1.36. |
| Linux | `flatcar` |
Not supported |
|

`AzureLinuxOSGuard`

[Azure Linux with OS Guard for AKS](use-azure-linux-os-guard)doesn't support CVM.When using `Ubuntu`

or `AzureLinux`

as the `osSKU`

, if the default OS version doesn't support CVM, AKS defaults to the most recent CVM-supported version of the OS. For example, Ubuntu 22.04 is default for Linux node pools. Since 22.04 doesn't currently support CVM, AKS defaults to Ubuntu 20.04 for Linux CVM-enabled node pools.

### Limitations

The following limitations apply when adding a node pool with CVM to AKS:

- You can't use FIPS, ARM64, Trusted Launch, or Pod Sandboxing.
- You can't update an existing node pool to migrate to a CVM size. To migrate, you'll need to
[resize your node pool](resize-node-pool). - You can't use CVM with Windows node pools.
- CVM with Azure Linux is currently in preview.

## Prerequisites

Before you begin, make sure you have the following:

- An existing AKS cluster.
- CVM sizes must be available for your subscription in the region where the cluster is created. You must have sufficient quota to create a node pool with a CVM size.
- If you're using Azure Linux os, you need to install the
`aks-preview`

extension, update the`aks-preview`

extension, and register the preview feature flag. If you're using Ubuntu, you can skip these steps.

### If you are using Azure Linux

CVMs for Ubuntu is GA, but CVMs with Azure Linux is currently still in preview. If you would like to use CVM node pools with Azure Linux as the OS of choice, ensure you enable the extension and register the flag.

#### Install `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

`az extension update --name aks-preview`


#### Register `AzureLinuxCVMPreview`

feature flag

Register the

`AzureLinuxCVMPreview`

feature flag using the [`az feature register`

][az-feature-register] command.`az feature register --namespace "Microsoft.ContainerService" --name "AzureLinuxCVMPreview"`

Verify the registration status using the [

`az feature show`

][az-feature-show] command. It takes a few minutes for the status to show*Registered*.`az feature show --namespace Microsoft.ContainerService --name AzureLinuxCVMPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using the [`az provider register`

][az-provider-register] command.`az provider register --namespace Microsoft.ContainerService`


## Add a node pool with a CVM to your AKS cluster

Add a node pool with a CVM to your AKS cluster using the

command and set the`az aks nodepool add`

`node-vm-size`

to a supported[VM size](/en-us/azure/confidential-computing/virtual-machine-options).`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --node-count 3 \ --node-vm-size Standard_DC4as_v5`


If you don't specify the `osSKU`

or `osType`

, AKS defaults to `--os-type Linux`

and `--os-sku Ubuntu`

.

## Upgrade an existing node pool with a CVM to Ubuntu 24.04

Upgrade an existing node pool with a CVM to Ubuntu 24.04 from Ubuntu 20.04 using the

command. Set the`az aks nodepool update`

`os-sku`

as`Ubuntu2404`

.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --os-sku Ubuntu2404`


Note

A node pool which is Ubuntu 24.04 with a CVM is supported from AKS cluster 1.33 version. Additionally, before Ubuntu 24.04 becomes GA, you need to register the `Ubuntu2404Preview`

feature. For more information, see [ here](/en-us/azure/aks/upgrade-os-version#register-ubuntu2404preview-feature-flag) to register the feature.

## Verify the node pool uses CVM

Verify a node pool uses CVM using the

command and verify the`az aks nodepool show`

`vmSize`

is`Standard_DCa4_v5`

.`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'vmSize'`

The following example command and output shows the node pool uses CVM:

`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'vmSize' "Standard_DC4as_v5"`

Verify a node pool uses a CVM image using the

command.`az aks nodepool list`

`az aks nodepool list \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'nodeImageVersion'`

The following example command and output shows the node pool uses an Ubuntu 20.04 CVM image:

`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'nodeImageVersion' "AKSUbuntu-2004cvmcontainerd-202507.02.0"`


## Remove a node pool with CVM from an AKS cluster

Remove a node pool with CVM from an AKS cluster using the

command.`az aks nodepool delete`

`az aks nodepool delete \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool`


## Next steps

In this article, you learned how to add a node pool with CVM to an AKS cluster.

- For more information about CVM, see
[Confidential VM node pools support on AKS](/en-us/azure/confidential-computing/confidential-node-pool-aks). - To migrate an existing node pool to a CVM vm size, you can
[resize your node pool](resize-node-pool). - If you're only interested in enabling Trusted Launch on your node pools, see
[Trusted Launch on AKS](use-trusted-launch).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/update-azure-cni -->

# Update Azure CNI IPAM mode and data plane technology for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Existing Azure Kubernetes Service (AKS) clusters inevitably need an update to newer IP assignment management (IPAM) modes and data plane technologies to access the latest features and supportability. This article provides guidance on updating an existing AKS cluster to use Azure CNI Overlay for the IPAM mode and Azure CNI Powered by Cilium as the data plane.

## Update the IPAM mode to Azure CNI Overlay

Updating an existing cluster to Azure CNI Overlay is an irreversible process.

You can update an existing AKS cluster to Azure CNI Overlay if the cluster:

- Is on Kubernetes version 1.27 or later.
- Doesn't use the
[dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)feature. - Doesn't have network policies enabled. If you need to uninstall the network policy engine before updating your cluster, follow the steps in
[Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico). - Doesn't use any Windows node pools with Docker as the container runtime.

Before Windows OS build 20348.1668, there was a limitation around Windows overlay pods incorrectly routing packets from host network pods via Source Network Address Translation (SNAT). This limitation had a detrimental effect for clusters that were updating to Azure CNI Overlay. To avoid this issue, use Windows OS build 20348.1668 or later.

Warning

If you're using a custom

`azure-ip-masq-agent`

configuration to include additional IP ranges that shouldn't send SNAT packets from pods, updating to Azure CNI Overlay can break connectivity to these ranges. Pod IPs from the overlay space are unreachable by anything outside the cluster nodes.For old clusters, a ConfigMap might be left over from a previous version of

`azure-ip-masq-agent`

. If this ConfigMap (named`azure-ip-masq-agent-config`

) exists and isn't intentionally in place, you should delete it before updating.If you're not using a custom

`ip-masq-agent`

configuration, only the`azure-ip-masq-agent-config-reconciled`

ConfigMap should exist with respect to Azure`ip-masq-agent`

ConfigMap. It's updated automatically during the update process.

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately to Azure CNI Overlay isn't supported. Any disruptions to cluster networking are similar to a node image update or Kubernetes version upgrade where each node in a node pool is reimaged.

Update an existing Azure Container Networking Interface (CNI) cluster to use Azure CNI Overlay by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16
```


The `--pod-cidr`

parameter is required when you update from legacy CNI plugins because the pods need to get IPs from a new overlay space. The new overlay space doesn't overlap with the existing Azure CNI Node Subnet plugin.

Classless Inter-Domain Routing (CIDR) for the pod also can't overlap with any virtual network address of the node pools. For example, if your virtual network address is 10.0.0.0/8, and your nodes are in the subnet 10.240.0.0/16, the `--pod-cidr`

parameter can't overlap with 10.0.0.0/8 or the existing service CIDR on the cluster.

## Update the data plane to Azure CNI Powered by Cilium

When you enable Cilium in a cluster that uses a different network policy engine (Azure Network Policy Manager or Calico), the network policy engine is uninstalled and replaced with Cilium. For more information, see [Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico).

You can update an existing cluster to Azure CNI Powered by Cilium if the cluster doesn't have any Windows node pools.

Warning

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image update or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium begins enforcing network policies only after all nodes are reimaged.

To perform the update, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

Update an existing cluster to Azure CNI Powered by Cilium by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-dataplane cilium
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-azure-cni -->

# Update Azure CNI IPAM mode and data plane technology for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Existing Azure Kubernetes Service (AKS) clusters inevitably need an update to newer IP assignment management (IPAM) modes and data plane technologies to access the latest features and supportability. This article provides guidance on updating an existing AKS cluster to use Azure CNI Overlay for the IPAM mode and Azure CNI Powered by Cilium as the data plane.

## Update the IPAM mode to Azure CNI Overlay

Updating an existing cluster to Azure CNI Overlay is an irreversible process.

You can update an existing AKS cluster to Azure CNI Overlay if the cluster:

- Is on Kubernetes version 1.27 or later.
- Doesn't use the
[dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)feature. - Doesn't have network policies enabled. If you need to uninstall the network policy engine before updating your cluster, follow the steps in
[Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico). - Doesn't use any Windows node pools with Docker as the container runtime.

Before Windows OS build 20348.1668, there was a limitation around Windows overlay pods incorrectly routing packets from host network pods via Source Network Address Translation (SNAT). This limitation had a detrimental effect for clusters that were updating to Azure CNI Overlay. To avoid this issue, use Windows OS build 20348.1668 or later.

Warning

If you're using a custom

`azure-ip-masq-agent`

configuration to include additional IP ranges that shouldn't send SNAT packets from pods, updating to Azure CNI Overlay can break connectivity to these ranges. Pod IPs from the overlay space are unreachable by anything outside the cluster nodes.For old clusters, a ConfigMap might be left over from a previous version of

`azure-ip-masq-agent`

. If this ConfigMap (named`azure-ip-masq-agent-config`

) exists and isn't intentionally in place, you should delete it before updating.If you're not using a custom

`ip-masq-agent`

configuration, only the`azure-ip-masq-agent-config-reconciled`

ConfigMap should exist with respect to Azure`ip-masq-agent`

ConfigMap. It's updated automatically during the update process.

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately to Azure CNI Overlay isn't supported. Any disruptions to cluster networking are similar to a node image update or Kubernetes version upgrade where each node in a node pool is reimaged.

Update an existing Azure Container Networking Interface (CNI) cluster to use Azure CNI Overlay by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16
```


The `--pod-cidr`

parameter is required when you update from legacy CNI plugins because the pods need to get IPs from a new overlay space. The new overlay space doesn't overlap with the existing Azure CNI Node Subnet plugin.

Classless Inter-Domain Routing (CIDR) for the pod also can't overlap with any virtual network address of the node pools. For example, if your virtual network address is 10.0.0.0/8, and your nodes are in the subnet 10.240.0.0/16, the `--pod-cidr`

parameter can't overlap with 10.0.0.0/8 or the existing service CIDR on the cluster.

## Update the data plane to Azure CNI Powered by Cilium

When you enable Cilium in a cluster that uses a different network policy engine (Azure Network Policy Manager or Calico), the network policy engine is uninstalled and replaced with Cilium. For more information, see [Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico).

You can update an existing cluster to Azure CNI Powered by Cilium if the cluster doesn't have any Windows node pools.

Warning

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image update or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium begins enforcing network policies only after all nodes are reimaged.

To perform the update, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

Update an existing cluster to Azure CNI Powered by Cilium by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-dataplane cilium
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-kms-etcd-encryption -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/localdns-custom -->

# Configure LocalDNS in Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

LocalDNS is a feature in Azure Kubernetes Service (AKS) designed to enhance the Domain Name System (DNS) resolution performance and resiliency for workloads running in your cluster. When you deploy a DNS proxy on each node, LocalDNS reduces DNS query latency, improves reliability during network disruptions, and provides advanced configuration options for DNS caching and forwarding. This article explains how LocalDNS works, its configuration options, and how to enable, verify, and troubleshoot LocalDNS in your AKS clusters.

To learn about what LocalDNS is, including architecture details, and key capabilities, refer to [DNS Resolution in Azure Kubernetes Service (AKS)](dns-concepts).

## Best practices for LocalDNS configuration

When implementing LocalDNS in your AKS clusters, consider the following best practices:

**Start with a minimal configuration**: Begin with a simple configuration that uses the`Preferred`

mode before moving to`Required`

mode. This setup allows you to validate that LocalDNS works as expected without breaking your cluster.**Implement proper caching strategies**: Configure cache settings based on your workload characteristics:- For frequently changing records, use shorter
`cacheDurationInSeconds`

values. When doing so, it's important to note that cacheDurationInSeconds acts as a cap on the DNS record TTL but doesn't increase it. The resulting TTL is the smaller of what is returned from upstream or what is set in the cache plugin. - For stable records, use longer cache durations to reduce DNS queries.
- Enable
`serveStale`

with appropriate settings to maintain service during DNS outages. - Caching with LocalDNS operates on a best effort basis and doesn't guarantee stale responses. The cache is divided into 256 shards and with a default maximum of 10,000 entries, allowing each shard to hold about 39 entries. When a shard is full and a new entry needs to be added, one of the existing entries is chosen at random to be evicted. There's no preference for older or expires entries. As a result, a stale record might not always be available, especially under high query volume.

- For frequently changing records, use shorter
**Monitor DNS performance**: After enabling LocalDNS, monitor your application's DNS performance using:- Application performance metrics.
- Node metrics to detect reduced network pressure.
- Log entries when
`queryLogging`

is set to`Log`

.

**Follow least privilege principle**: When configuring DNS forwarding rules, only allow access to the required DNS servers and domains.**Test before production deployment**: Always test LocalDNS configuration in a nonproduction environment before rolling it out to production clusters.**Use Infrastructure as Code (IaC)**: Store your*localdnsconfig.json*file in your infrastructure repository and include it in your AKS deployment templates.**Network configuration for TCP forwarding**: When using TCP for DNS forwarding to VnetDNS, ensure that your Network Security Groups (NSGs), firewalls, or Network Virtual Appliances (NVAs) don't block TCP traffic between CoreDNS/LocalDNS and VnetDNS servers.**Avoid enabling both NodeLocal DNSCache and LocalDNS**: It isn't recommended to enable both the upstream Kubernetes NodeLocal DNSCache and LocalDNS in your node pool. While AKS doesn't block this configuration, all DNS traffic is routed through LocalDNS, which might lead to unexpected behavior or reduced benefits from NodeLocal DNSCache.

## Prerequisites

- You must have an existing AKS cluster with Kubernetes versions 1.31 or later to use LocalDNS. If you need an AKS cluster, you can create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - This article requires version 2.80.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed.
- LocalDNS is only supported on node pools running Azure Linux or Ubuntu 22.04 or newer.
- The Virtual Machine (VM) SKU used for your node pool must have at least 4 vCPUs (cores) to support LocalDNS.
- LocalDNS isn't compatible with
[applied FQDN filter policies in Advanced Container Networking Services (ACNS)](how-to-apply-fqdn-filtering-policies).

## Manage LocalDNS on an AKS cluster

LocalDNS is configured at the node pool level in AKS, meaning you can enable or disable LocalDNS independently for each node pool in your cluster. This tailors DNS resolution behavior based on the specific requirements of different workloads or environments. To enable LocalDNS on a node pool, you need to provide a configuration file: *localdnsconfig.json* that defines how LocalDNS should operate for that node pool.

If you don't specify a custom configuration file, AKS automatically applies a default LocalDNS configuration.

Note

If you're using Node Auto-Provisioning (NAP), see [LocalDNS configuration](node-auto-provisioning-aksnodeclass#localdns-configuration) for instructions on how to enable LocalDNS with NAP.

To enable LocalDNS during node pool creation, use the following command with your custom configuration file:

```
az aks nodepool add --name mynodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --localdns-config ./localdnsconfig.json
```


To enable LocalDNS on an existing node pool, use the following command with your custom configuration file:

```
az aks nodepool update --name mynodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --localdns-config ./localdnsconfig.json
```


Important

Enabling LocalDNS on a node pool initiates a reimage operation on all nodes within that pool. This process can cause temporary disruption to running workloads and might lead to application downtime if not properly managed. You should plan for potential service interruptions and ensure that the applications are configured for high availability or have appropriate disruption budgets in place before enabling this setting.

## Create a custom server block in LocalDNS

CoreDNS matches queries to a specific server block based on an exact match for domain being queried and not on partial matches. If you have the need for custom server blocks, you can add them to your LocalDNS configuration by creating a file called *localdnsconfig.json* with the added configurations.

For example, if you have specific DNS needs when accessing microsoft.com, you could use the following server block:

```
"microsoft.com": {
"queryLogging": "Error",
"protocol": "ForceTCP",
"forwardDestination": "ClusterCoreDNS",
"forwardPolicy": "Sequential",
"maxConcurrent": 1000,
"cacheDurationInSeconds": 3600,
"serveStaleDurationInSeconds": 3600,
"serveStale": "Immediate"
}
```


## Monitor LocalDNS

LocalDNS exposes Prometheus metrics that you can use for monitoring and alerting. These [metrics](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-default#coredns) are exposed on port `9253`

of the Node IP and can be scraped from there.

The following example YAML shows a scrape configuration you can use with the [Azure Managed Prometheus add on as a DaemonSet](/en-us/azure/azure-monitor/essentials/prometheus-metrics-scrape-configuration):

```
kind: ConfigMap
apiVersion: v1
metadata:
name: ama-metrics-prometheus-config-node
namespace: kube-system
data:
prometheus-config: |-
global:
scrape_interval: 1m
scrape_configs:
- job_name: localdns-metrics
scrape_interval: 1m
scheme: http
metrics_path: /metrics
relabel_configs:
- source_labels: [__metrics_path__]
regex: (.*)
target_label: metrics_path
- source_labels: [__address__]
replacement: '$NODE_NAME'
target_label: instance
static_configs:
- targets: ['$NODE_IP:9253']
```


## Troubleshoot LocalDNS

### DNS queries to specific domains are failing

If DNS queries to specific domains are failing after enabling LocalDNS:

- Check if you have domain-specific overrides in your
*localdnsconfig.json*that might be misconfigured. - Temporarily try removing domain-specific overrides and using only the default
`.`

configuration. - Check if the issue occurs with both User Datagram Protocol (UDP) and Transmission Control Protocol (TCP) by adjusting the
`protocol`

setting.

### Update VNet DNS servers for LocalDNS

When you update custom DNS servers directly in the VNet configuration (using the Azure portal or CLI), these changes aren't automatically applied to your AKS cluster nodes. This happens because updating DNS settings at the VNet level only informs the Network Resource Provider (NRP), but doesn't notify the AKS Resource Provider. As a result, AKS nodes continue to use the previous DNS server settings until further action is taken.

To ensure AKS nodes pick up the new VNet DNS server settings:

Update the VNet DNS configuration using the Azure portal or APIs as needed.

Reimage the node pool through the AKS Resource Provider to apply and persist the DNS changes:

`az aks nodepool upgrade --resource-group myResourceGroup --cluster-name myAKSCluster --name mynodepool --node-image-only`


This process ensures the AKS Resource Provider is aware of the DNS changes and applies them to all nodes in the node pool.

## Next steps

For information on LocalDNS in AKS, see [LocalDNS in Azure Kubernetes Service (conceptual)](dns-concepts).

For comprehensive troubleshooting guidance on DNS issues when using LocalDNS, see [Troubleshoot LocalDNS issues in AKS](/en-us/troubleshoot/azure/azure-kubernetes/connectivity/dns/troubleshoot-localdns).

For details on how to customize CoreDNS in AKS, refer to the [CoreDNS customization guide](coredns-custom).

For information on the CoreDNS project, see [the CoreDNS upstream project page](https://coredns.io/).

To learn more about core network concepts, see [Network concepts for applications in AKS](concepts-network).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-node-pools -->

# Upgrade node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to upgrade a single node pool and how to upgrade the cluster control plane for multiple node pools in Azure Kubernetes Service (AKS).

Note

As a best practice, you should upgrade all node pools in an AKS cluster to the same Kubernetes version. The default behavior of [`az aks upgrade`

][az-aks-upgrade] is to upgrade all node pools together with the control plane to achieve this alignment. The ability to upgrade individual node pools lets you perform a rolling upgrade and schedule pods between node pools to maintain application uptime.

## Upgrade a single node pool

Note

The node pool operating system (OS) image version is tied to the Kubernetes version of the cluster. You only get OS image upgrades following a cluster upgrade.

Check for any available upgrades using the [

`az aks get-upgrades`

][az-aks-get-upgrades] command.`az aks get-upgrades --resource-group <resource-group-name> --name <cluster-name>`

Upgrade a specific node pool using the [

`az aks nodepool upgrade`

][az-aks-nodepool-upgrade] command.`az aks nodepool upgrade \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --kubernetes-version <kubernetes-version> \ --no-wait`

Check the status of your node pool using the [

`az aks nodepool list`

][az-aks-nodepool-list] command.`az aks nodepool list --resource-group <resource-group-name> --cluster-name <cluster-name>`

The following example output shows the node pool is in the

*Upgrading*state:`[ { ... "count": 3, ... "name": "<node-pool-name>", "orchestratorVersion": "<kubernetes-version>", ... "provisioningState": "Upgrading", ... "vmSize": "Standard_DS2_v2", ... }, { ... "count": 2, ... "name": "<node-pool-name-2>", "orchestratorVersion": "<kubernetes-version-2>", ... "provisioningState": "Succeeded", ... "vmSize": "Standard_DS2_v2", ... } ]`

It takes a few minutes to upgrade the nodes to the specified version. After the upgrade is complete, the node pool's

`provisioningState`

changes to*Succeeded*.

## Upgrade a cluster control plane with multiple node pools

An AKS cluster has two cluster resource objects with Kubernetes versions associated to them: the cluster control plane Kubernetes version and a node pool with a Kubernetes version.

### Upgrade behavior for the control plane and node pools

The control plane maps to one or many node pools. The behavior of an upgrade operation depends on which Azure CLI command you use and the flags you specify:

upgrades the control plane and all node pools in the cluster to the same Kubernetes version.`az aks upgrade`

with the`az aks upgrade`

`--control-plane-only`

flag upgrades only the cluster control plane and leaves all node pools unchanged.upgrades only the target node pool with the specified Kubernetes version.`az aks nodepool upgrade`


### Validation rules for upgrades

Note

Kubernetes uses the standard [Semantic Versioning](https://semver.org/) versioning scheme. The version number is expressed as *x.y.z*, where *x* is the major version, *y* is the minor version, and *z* is the patch version. For example, in version *1.12.6*, *1* is the major version, *12* is the minor version, and *6* is the patch version. The Kubernetes version of the control plane and the initial node pool are set during cluster creation. Other node pools have their Kubernetes version set when they are added to the cluster. The Kubernetes versions may differ between node pools and between a node pool and the control plane.

Kubernetes upgrades for a cluster control plane and node pools are validated using the following sets of rules:

**Rules for valid versions to upgrade node pools**:- The node pool version must have the same
*major*version as the control plane. - The node pool
*minor*version must be within two*minor*versions of the control plane version. - The node pool version can't be greater than the control
`major.minor.patch`

version.

- The node pool version must have the same
**Rules for submitting an upgrade operation**:- You can't downgrade the control plane or a node pool Kubernetes version.
- If a node pool Kubernetes version isn't specified, the behavior depends on the client. In Azure Resource Manager (ARM) templates, declaration falls back to the existing version defined for the node pool. If nothing is set, it falls back to the control plane version.
- You can't simultaneously submit multiple operations on a single control plane or node pool resource. You can either upgrade or scale a control plane or a node pool at a given time.


## Next steps: Manage node pools in AKS

To learn more about managing node pools in AKS, see [Manage node pools in Azure Kubernetes Service (AKS)](manage-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/stop-cluster-upgrade-api-breaking-changes -->

# Stop Azure Kubernetes Service (AKS) cluster upgrades automatically on API breaking changes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to stop Azure Kubernetes Service (AKS) cluster upgrades automatically on API breaking changes.

## Overview

To stay within a supported Kubernetes version, you have to upgrade your cluster at least once per year and prepare for all possible disruptions. These disruptions include ones caused by API breaking changes, deprecations, and dependencies such as Helm and Container Storage Interface (CSI). It can be difficult to anticipate these disruptions and migrate critical workloads without experiencing any downtime.

You can configure your AKS cluster to automatically stop upgrade operations consisting of a minor version change with deprecated APIs and alert you to the issue. This feature helps you avoid unexpected disruptions and gives you time to address the deprecated APIs before proceeding with the upgrade.

## Before you begin

Before you begin, make sure you meet the following prerequisites:

- The upgrade operation is a Kubernetes minor version change for the cluster control plane.
- The Kubernetes version you're upgrading to is 1.26 or later.
- The last seen usage of deprecated APIs for the targeted version you're upgrading to must occur within 12 hours before the upgrade operation. AKS records usage hourly, so any usage of deprecated APIs within one hour isn't guaranteed to appear in the detection.

## Mitigate stopped upgrade operations

If you meet the [prerequisites](#before-you-begin), attempt an upgrade, and receive an error message similar to the following example error message:

```
Bad Request({
"code": "ValidationError",
"message": "Control Plane upgrade is blocked due to recent usage of a Kubernetes API deprecated in the specified version. Please refer to https://kubernetes.io/docs/reference/using-api/deprecation-guide to migrate the usage. To bypass this error, set enable-force-upgrade in upgradeSettings.overrideSettings. Bypassing this error without migrating usage will result in the deprecated Kubernetes API calls failing. Usage details: 1 error occurred:\n\t* usage has been detected on API flowcontrol.apiserver.k8s.io.prioritylevelconfigurations.v1beta1, and was recently seen at: 2023-03-23 20:57:18 +0000 UTC, which will be removed in 1.26\n\n",
"subcode": "UpgradeBlockedOnDeprecatedAPIUsage"
})
```


You have two options to mitigate the issue: you can [remove usage of deprecated APIs (recommended)](#remove-usage-of-deprecated-apis-recommended) or [bypass validation to ignore API changes](#bypass-validation-to-ignore-api-changes).

### Remove usage of deprecated APIs (recommended)

In the Azure portal, navigate to your cluster resource and select

**Diagnose and solve problems**Select

**Create, Upgrade, Delete, and Scale**>**Kubernetes API deprecations**.Wait 12 hours from the time the last deprecated API usage was seen. Read-Only verbs are excluded from the deprecated api usage namely

[Get/List/Watch](https://kubernetes.io/docs/reference/using-api/api-concepts/).(You can also check past API usage by enabling[Container insights](/en-us/azure/azure-monitor/containers/container-insights-log-query#resource-logs)and exploring kube audit logs.)Retry your cluster upgrade.


### Bypass validation to ignore API changes

Note

This method requires you to use the Azure CLI version 2.57 or later. If you have the preview CLI extension installed, you need to update to version `3.0.0b10`

or later. This method isn't recommended, as deprecated APIs in the targeted Kubernetes version might not work long term. We recommend removing them as soon as possible after the upgrade completes.

Bypass validation to ignore API breaking changes and invoke an upgrade. Specify the

`enable-force-upgrade`

flag and set the`upgrade-override-until`

property to define the end of the window during which validation is bypassed. If no value is set, it defaults the window to three days from the current time. The date and time you specify must be in the future.`az aks upgrade --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME --kubernetes-version $KUBERNETES_VERSION --enable-force-upgrade --upgrade-override-until 2023-10-01T13:00:00Z`

Note

`Z`

is the zone designator for the zero UTC/GMT offset, also known as 'Zulu' time. This example sets the end of the window to`13:00:00`

GMT. For more information, see[Combined date and time representations](https://wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).

## Next steps

This article showed you how to stop AKS cluster upgrades automatically on API breaking changes. To learn more about more upgrade options for AKS clusters, see [Upgrade options for Azure Kubernetes Service (AKS) clusters](upgrade-cluster).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-metrics -->

# What is container network metrics?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Advanced Container Networking Services in Azure Kubernetes Service (AKS) facilitates the collection of comprehensive container network metrics to give you valuable insights into the performance of your containerized environment. The capability continuously captures essential metrics at the node level and pod level, including traffic volume, dropped packets, connection states, and Domain Name System (DNS) resolution times for effective monitoring and optimizing network performance.

Capturing these metrics is essential for understanding how containers communicate, how traffic flows between services, and where bottlenecks or disruptions might occur. Advanced Container Networking Services integrates seamlessly with monitoring tools like Prometheus and Grafana to give you a complete view of networking metrics. Use the metrics for in-depth troubleshooting, network optimization, and performance tuning.

In a cloud-native world, maintaining a healthy and efficient network in a dynamic containerized environment is vital to ensuring that applications perform as expected. Without proper visibility into network traffic and its patterns, identifying potential issues or inefficiencies becomes challenging.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Key benefits

Deep visibility into network performance

Enhanced troubleshooting and optimization

Proactive anomaly detection

Better resource management and scaling

Capacity planning and compliance

Source-level metrics filtering for cost optimization and noise reduction with

[container network metrics filtering](#container-network-metrics-filtering-preview)Simplified metrics storage and visualization options. Choose between:

**Azure managed service for Prometheus and Azure Managed Grafana**: Azure manages the infrastructure and maintenance, so you can focus on configuring metrics and visualizing metrics.**Bring your own (BYO) Prometheus and Grafana**: You deploy and configure your own instances of Prometheus and Grafana, and you manage the underlying infrastructure.


## Metrics captured

### Node-level metrics

Understanding the health of your container network at the node-level is crucial for maintaining optimal application performance. These metrics provide insights into traffic volume, dropped packets, number of connections, and other data by node. The metrics are stored in Prometheus format, so, you can view them in Grafana.

The following metrics are aggregated per node. All metrics include one of these labels:

`cluster`

`instance`

(node name)

For Cilium data plane scenarios, Container Network Observability provides metrics only for Linux. Windows is currently not supported. Cilium exposes several metrics including the following used by Container Network Observability.

| Metric name | Description | Extra labels | Linux | Windows |
|---|---|---|---|---|
cilium_forward_count_total |
Total forwarded packet count | `direction` |
✅ | ❌ |
cilium_forward_bytes_total |
Total forwarded byte count | `direction` |
✅ | ❌ |
cilium_drop_count_total |
Total dropped packet count | `direction` , `reason` |
✅ | ❌ |
cilium_drop_bytes_total |
Total dropped byte count | `direction` , `reason` |
✅ | ❌ |

### Pod-level metrics (Hubble metrics)

These Prometheus metrics include source and destination pod information so that you can pinpoint network-related issues at a granular level. Metrics cover information like traffic volume, dropped packets, TCP resets, and Layer 4/Layer 7 packet flows. DNS metrics like DNS errors and DNS requests missing responses are collected by default for non-Cilium data planes. For Cilium data planes, a Cilium FQDN network policy is required to collect DNS metrics, or customers can also troubleshoot DNS using Hubble CLI and observing real-time logs.

The following table describes the metrics that are aggregated per pod (node information is preserved).

All metrics include labels:

`cluster`

`instance`

(node name)`source`

or`destination`

For

*outgoing traffic*, a`source`

label that indicates the source pod namespace and name is applied.For

*incoming traffic*, a`destination`

label that indicates the destination pod namespace and name is applied.


| Metric name | Description | Extra Labels | Linux | Windows |
|---|---|---|---|---|
hubble_dns_queries_total |
Total DNS requests by query | `source` or `destination` , `query` , `qtypes` (query type) |
✅ | ❌ |
hubble_dns_responses_total |
Total DNS responses by query/response | `source` or `destination` , `query` , `qtypes` (query type), `rcode` (return code), `ips_returned` (number of IPs) |
✅ | ❌ |
hubble_drop_total |
Total dropped packet count | `source` or `destination` , `protocol` , `reason` |
✅ | ❌ |
hubble_tcp_flags_total |
Total TCP packets count by flag | `source` or `destination` , `flag` |
✅ | ❌ |
hubble_flows_processed_total |
Total network flows processed (Layer 4/Layer 7 traffic) | `source` or `destination` , `protocol` , `verdict` , `type` , `subtype` |
✅ | ❌ |

## Container network metrics filtering (Preview)

Now that you have the ability to collect comprehensive metrics at both node and pod levels, you might find yourself dealing with a significant volume of data. To help reduce noise and optimize storage costs, Container Network Observability introduces **container network metrics filtering**. This feature enables you to filter metrics at the source before they are collected and stored, giving you control over which metrics are most relevant to your specific monitoring and troubleshooting needs. This feature is only available for Cilium clusters.

Container network metrics filtering is particularly valuable in large-scale production environments where the sheer volume of metrics can impact storage costs and query performance. By filtering out unnecessary metrics early in the collection process, you can focus on the data that matters most to your operations while maintaining the visibility you need for effective network monitoring.

The filtering capability supports multiple dimensions including namespace-based filtering to focus on specific applications, pod and label-based filtering for targeted monitoring, and metric-specific filtering to collect only the types of metrics that are essential for your use case. This flexibility allows you to strike the right balance between comprehensive observability and cost-effective operations.

To learn more on how to enable container network metrics filtering, see [How to Configure Container Network Metrics Filtering ](how-to-configure-container-network-metrics-filtering).

### Limitations

- Pod-level metrics are available only on Linux.
- Cilium data plane is supported starting with Kubernetes version 1.29.
- Metric labels have subtle differences between Cilium and non-Cilium clusters.
- For Cilium based clusters, DNS metrics are only available for pods that have Cilium Network policies (CNP) configured on their clusters, or customers can also troubleshoot DNS using Hubble CLI and observing real-time logs.
- Flow logs are not currently available in the air gapped cloud.
- Hubble relay may crash if one of the Hubble node agents goes down and may cause interruptions to Hubble CLI.
- When using Advanced Container Networking Services (ACNS) on non-Cilium data planes, FIPS support isn't available on Ubuntu 20.04 nodes due to kernel restrictions. To enable FIPS in this scenario, you must use an Azure Linux node pool. This limitation is expected to be resolved with the release of Ubuntu 22 FIPS. For updates, see the
[AKS issue tracker](https://github.com/Azure/AKS/issues/4857). - Container network metrics filtering is only available for Cilium Clusters.

Refer to the FIPS support matrix below:

| Operating System | FIPS Support |
|---|---|
| Azure Linux 3.0 | Yes |
| Azure Linux 2.0 | Yes |
| Ubuntu 20.04 | No |

This limitation does not apply when ACNS is running on Cilium data planes.

### Scale

The managed service for Prometheus in Azure Monitor and Azure Managed Grafana impose service-specific scale limitations. For more information, see [Scrape Prometheus metrics at scale in Azure Monitor](/en-us/azure/azure-monitor/essentials/prometheus-metrics-scrape-scale).

## Pricing

Important

Advanced Container Networking Services is a paid offering.

For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Related content

- To create an AKS cluster by using Container Network Observability to capture metrics, see
[Set up Container Network Observability for AKS](container-network-observability-how-to). - Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services. - Explore the
[Container Network Security feature](advanced-container-networking-services-overview#container-network-security)in Advanced Container Networking Services.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-aks-ipam-and-dataplane -->

# Update Azure CNI IPAM mode and data plane technology for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Existing Azure Kubernetes Service (AKS) clusters inevitably need an update to newer IP assignment management (IPAM) modes and data plane technologies to access the latest features and supportability. This article provides guidance on updating an existing AKS cluster to use Azure CNI Overlay for the IPAM mode and Azure CNI Powered by Cilium as the data plane.

## Update the IPAM mode to Azure CNI Overlay

Updating an existing cluster to Azure CNI Overlay is an irreversible process.

You can update an existing AKS cluster to Azure CNI Overlay if the cluster:

- Is on Kubernetes version 1.27 or later.
- Doesn't use the
[dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)feature. - Doesn't have network policies enabled. If you need to uninstall the network policy engine before updating your cluster, follow the steps in
[Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico). - Doesn't use any Windows node pools with Docker as the container runtime.

Before Windows OS build 20348.1668, there was a limitation around Windows overlay pods incorrectly routing packets from host network pods via Source Network Address Translation (SNAT). This limitation had a detrimental effect for clusters that were updating to Azure CNI Overlay. To avoid this issue, use Windows OS build 20348.1668 or later.

Warning

If you're using a custom

`azure-ip-masq-agent`

configuration to include additional IP ranges that shouldn't send SNAT packets from pods, updating to Azure CNI Overlay can break connectivity to these ranges. Pod IPs from the overlay space are unreachable by anything outside the cluster nodes.For old clusters, a ConfigMap might be left over from a previous version of

`azure-ip-masq-agent`

. If this ConfigMap (named`azure-ip-masq-agent-config`

) exists and isn't intentionally in place, you should delete it before updating.If you're not using a custom

`ip-masq-agent`

configuration, only the`azure-ip-masq-agent-config-reconciled`

ConfigMap should exist with respect to Azure`ip-masq-agent`

ConfigMap. It's updated automatically during the update process.

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately to Azure CNI Overlay isn't supported. Any disruptions to cluster networking are similar to a node image update or Kubernetes version upgrade where each node in a node pool is reimaged.

Update an existing Azure Container Networking Interface (CNI) cluster to use Azure CNI Overlay by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16
```


The `--pod-cidr`

parameter is required when you update from legacy CNI plugins because the pods need to get IPs from a new overlay space. The new overlay space doesn't overlap with the existing Azure CNI Node Subnet plugin.

Classless Inter-Domain Routing (CIDR) for the pod also can't overlap with any virtual network address of the node pools. For example, if your virtual network address is 10.0.0.0/8, and your nodes are in the subnet 10.240.0.0/16, the `--pod-cidr`

parameter can't overlap with 10.0.0.0/8 or the existing service CIDR on the cluster.

## Update the data plane to Azure CNI Powered by Cilium

When you enable Cilium in a cluster that uses a different network policy engine (Azure Network Policy Manager or Calico), the network policy engine is uninstalled and replaced with Cilium. For more information, see [Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico).

You can update an existing cluster to Azure CNI Powered by Cilium if the cluster doesn't have any Windows node pools.

Warning

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image update or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium begins enforcing network policies only after all nodes are reimaged.

To perform the update, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

Update an existing cluster to Azure CNI Powered by Cilium by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-dataplane cilium
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-byo-cni -->

# Bring your own CNI plugin with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes doesn't provide a network interface system by default. Instead, [network plugins](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/) provide this functionality. Azure Kubernetes Service (AKS) provides several supported Container Network Interface (CNI) plugins. For information on supported plugins, see [Networking concepts for applications in Azure Kubernetes Service](concepts-network).

The supported plugins meet most networking needs in Kubernetes. However, advanced AKS users might want the same CNI plugin that they used in on-premises Kubernetes environments. Or these users might want to use advanced functionalities available in other CNI plugins.

This article shows how to deploy an AKS cluster with no CNI plugin preinstalled. From there, you can install any CNI plugin that works in Azure.

## Support

Microsoft support can't assist with CNI-related issues in clusters that you deploy by bringing your own CNI plugin. For example, CNI-related issues would cover most east/west (pod to pod) traffic, along with `kubectl proxy`

and similar commands. If you want CNI-related support, use a supported AKS network plugin or seek support from the CNI plugin vendor.

Microsoft still provides support for issues that aren't related to CNI.

## Prerequisites

- For Azure Resource Manager or Bicep, use at least template version 2022-01-02-preview or 2022-06-01.
- For the Azure CLI, use at least version 2.39.0.
- The virtual network for the AKS cluster must allow outbound internet connectivity.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for the address range for the Kubernetes service, pods, or cluster virtual network. - The cluster identity that the AKS cluster uses must have at least
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)permissions on the subnet within your virtual network. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, the following permissions are required:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


- The subnet assigned to the AKS node pool can't be a
[delegated subnet](/en-us/azure/virtual-network/subnet-delegation-overview). - AKS doesn't apply network security groups (NSGs) to its subnet or modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure that the security rules in the NSGs allow traffic within the node's Classless Inter-Domain Routing (CIDR) range. For more information, see
[Network security groups](concepts-network#network-security-groups). - AKS doesn't create a route table in the managed virtual network.
- You must specify a Pod CIDR (IP address range for pods). The AKS control plane uses this range for internal traffic routing to pods, even though pod IP assignment will be managed by your custom CNI. If no pod CIDR is provided, control plane to pod communication may fail or be misrouted. You must select a pod CIDR that does not conflict with any other network in your environment and avoids Azure reserved ranges, such as,
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

. For example, you might use a range such as`10.XX.0.0/16`

that is unique to your cluster. This ensures that the control plane can route directly to pod IPs on your nodes, and no IP overlap will occur if you integrate with other networks or clusters.

## Create an AKS cluster with no CNI plugin preinstalled

Create an Azure resource group for your AKS cluster by using the

command.`az group create`

`az group create --location eastus --name myResourceGroup`

Create an AKS cluster by using the

command. Pass the`az aks create`

`--network-plugin`

parameter with the parameter value of`none`

.`az aks create \ --location eastus \ --resource-group myResourceGroup \ --name myAKSCluster \ --network-plugin none \ --pod-cidr "10.10.0.0/16" \ --generate-ssh-keys`


## Deploy a CNI plugin

After AKS provisioning finishes, the cluster is online. But all the nodes are in a `NotReady`

state, as shown in the following example:

```
$ kubectl get nodes
NAME STATUS ROLES AGE VERSION
aks-nodepool1-23902496-vmss000000 NotReady agent 6m9s v1.21.9
$ kubectl get node -o custom-columns='NAME:.metadata.name,STATUS:.status.conditions[?(@.type=="Ready")].message'
NAME STATUS
aks-nodepool1-23902496-vmss000000 container runtime network not ready: NetworkReady=false reason:NetworkPluginNotReady message:Network plugin returns error: cni plugin not initialized
```


At this point, the cluster is ready for installation of a CNI plugin.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/open-service-mesh-deploy-addon-bicep -->

# Deploy the Open Service Mesh add-on using Bicep in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to deploy the Open Service Mesh (OSM) add-on to Azure Kubernetes Service (AKS) using a [Bicep](/en-us/azure/azure-resource-manager/bicep/) template.

Important

Starting on **September 30, 2027**, Azure Kubernetes Service (AKS) no longer supports the Open Service Mesh (OSM) add-on. The [Cloud Native Computing Foundation (CNCF)](https://docs.openservicemesh.io/) retired the upstream OSM project. [Migrate any existing OSM configurations to equivalent Istio configurations](/en-us/azure/aks/open-service-mesh-istio-migration-guidance). For more information on this retirement, see the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=open-service-mesh-add-on-for-aks-will-be-retired-on-september-30-2027). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Based on the version of Kubernetes your cluster is running, the OSM add-on installs a different version of OSM.

| Kubernetes version | OSM version installed |
|---|---|
| 1.24.0 or greater | 1.2.5 |
| Between 1.23.5 and 1.24.0 | 1.1.3 |
| Below 1.23.5 | 1.0.0 |

Older versions of OSM may not be available for install or be actively supported if the corresponding AKS version has reached end of life. You can check the [AKS Kubernetes release calendar](supported-kubernetes-versions#aks-kubernetes-release-calendar) for information on AKS version support windows.

[Bicep](/en-us/azure/azure-resource-manager/bicep/overview) is a domain-specific language that uses declarative syntax to deploy Azure resources. You can use Bicep in place of creating [Azure Resource Manager templates](/en-us/azure/azure-resource-manager/templates/overview) to deploy your infrastructure-as-code Azure resources.

## Before you begin

Before you begin, make sure you have the following prerequisites in place:

- The Azure CLI version 2.20.0 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - An SSH public key used for deploying AKS. For more information, see
[Create SSH keys using the Azure CLI](/en-us/azure/virtual-machines/ssh-keys-azure-cli). [Visual Studio Code](https://code.visualstudio.com/)with a Bash terminal.- The Visual Studio Code
[Bicep extension](/en-us/azure/azure-resource-manager/bicep/install).

## Install the OSM add-on for a new AKS cluster by using Bicep

For deployment of a new AKS cluster, you enable the OSM add-on at cluster creation. The following instructions use a generic Bicep template that deploys an AKS cluster by using ephemeral disks and the [ kubenet](configure-kubenet) container network interface, and then enables the OSM add-on. For more advanced deployment scenarios, see

[What is Bicep?](/en-us/azure/azure-resource-manager/bicep/overview)

### Create a resource group

Create a resource group using the

command.`az group create`

`az group create --name <my-osm-bicep-aks-cluster-rg> --location <azure-region>`


### Create the main and parameters Bicep files

Create a directory to store the necessary Bicep deployment files. The following example creates a directory named

*bicep-osm-aks-addon*and changes to the directory:`mkdir bicep-osm-aks-addon cd bicep-osm-aks-addon`

Create the main file and the parameters file.

`touch osm.aks.bicep && touch osm.aks.parameters.json`

Open the

*osm.aks.bicep*file and copy in the following content:`// https://learn.microsoft.com/azure/aks/troubleshooting#what-naming-restrictions-are-enforced-for-aks-resources-and-parameters @minLength(3) @maxLength(63) @description('Provide a name for the AKS cluster. The only allowed characters are letters, numbers, dashes, and underscore. The first and last character must be a letter or a number.') param clusterName string @minLength(3) @maxLength(54) @description('Provide a name for the AKS dnsPrefix. Valid characters include alphanumeric values and hyphens (-). The dnsPrefix can\'t include special characters such as a period (.)') param clusterDNSPrefix string param k8Version string param sshPubKey string param location string param adminUsername string resource aksCluster 'Microsoft.ContainerService/managedClusters@2021-03-01' = { name: clusterName location: location identity: { type: 'SystemAssigned' } properties: { kubernetesVersion: k8Version dnsPrefix: clusterDNSPrefix enableRBAC: true agentPoolProfiles: [ { name: 'agentpool' count: 3 vmSize: 'Standard_DS2_v2' osDiskSizeGB: 30 osDiskType: 'Ephemeral' osType: 'Linux' mode: 'System' } ] linuxProfile: { adminUsername: adminUserName ssh: { publicKeys: [ { keyData: sshPubKey } ] } } addonProfiles: { openServiceMesh: { enabled: true config: {} } } } }`

Open the

*osm.aks.parameters.json*file and copy in the following content. Make sure you replace the deployment parameter values with your own values.Note

The

*osm.aks.parameters.json*file is an example template parameters file needed for the Bicep deployment. Update the parameters specifically for your deployment environment. The parameters you need to add values for include:`clusterName`

,`clusterDNSPrefix`

,`k8Version`

,`sshPubKey`

,`location`

, and`adminUsername`

. To find a list of supported Kubernetes versions in your region, use the`az aks get-versions --location <region>`

command.`{ "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#", "contentVersion": "1.0.0.0", "parameters": { "clusterName": { "value": "<YOUR CLUSTER NAME HERE>" }, "clusterDNSPrefix": { "value": "<YOUR CLUSTER DNS PREFIX HERE>" }, "k8Version": { "value": "<YOUR SUPPORTED KUBERNETES VERSION HERE>" }, "sshPubKey": { "value": "<YOUR SSH KEY HERE>" }, "location": { "value": "<YOUR AZURE REGION HERE>" }, "adminUsername": { "value": "<YOUR ADMIN USERNAME HERE>" } } }`


### Deploy the Bicep files

Open a terminal and authenticate to your Azure account for the Azure CLI using the

`az login`

command.Deploy the Bicep files using the

command.`az deployment group create`

`az deployment group create \ --name OSMBicepDeployment \ --resource-group osm-bicep-test \ --template-file osm.aks.bicep \ --parameters @osm.aks.parameters.json`


## Validate installation of the OSM add-on

Query the add-on profiles of the cluster to check the enabled state of the installed add-ons. The following command should return

`true`

:`az aks list -g <my-osm-aks-cluster-rg> -o json | jq -r '.[].addonProfiles.openServiceMesh.enabled'`

Get the status of the

*osm-controller*using the following`kubectl`

commands.`kubectl get deployments -n kube-system --selector app=osm-controller kubectl get pods -n kube-system --selector app=osm-controller kubectl get services -n kube-system --selector app=osm-controller`


## Access the OSM add-on configuration

You can configure the OSM controller using the OSM MeshConfig resource, and you can view the OSM controller's configuration settings using the Azure CLI.

View the OSM controller's configuration settings using the

`kubectl get`

command.`kubectl get meshconfig osm-mesh-config -n kube-system -o yaml`

Here's an example output of MeshConfig:

`apiVersion: config.openservicemesh.io/v1alpha1 kind: MeshConfig metadata: creationTimestamp: "0000-00-00A00:00:00A" generation: 1 name: osm-mesh-config namespace: kube-system resourceVersion: "2494" uid: 6c4d67f3-c241-4aeb-bf4f-b029b08faa31 spec: certificate: serviceCertValidityDuration: 24h featureFlags: enableEgressPolicy: true enableMulticlusterMode: false enableWASMStats: true observability: enableDebugServer: true osmLogLevel: info tracing: address: jaeger.osm-system.svc.cluster.local enable: false endpoint: /api/v2/spans port: 9411 sidecar: configResyncInterval: 0s enablePrivilegedInitContainer: false envoyImage: mcr.microsoft.com/oss/envoyproxy/envoy:v1.18.3 initContainerImage: mcr.microsoft.com/oss/openservicemesh/init:v0.9.1 logLevel: error maxDataPlaneConnections: 0 resources: {} traffic: enableEgress: true enablePermissiveTrafficPolicyMode: true inboundExternalAuthorization: enable: false failureModeAllow: false statPrefix: inboundExtAuthz timeout: 1s useHTTPSIngress: false`

Notice that

`enablePermissiveTrafficPolicyMode`

is configured to`true`

. In OSM, permissive traffic policy mode bypasses[SMI](https://smi-spec.io/)traffic policy enforcement. In this mode, OSM automatically discovers services that are a part of the service mesh. The discovered services will have traffic policy rules programmed on each Envoy proxy sidecar to allow communications between these services.Warning

Before you proceed, verify that your permissive traffic policy mode is set to

`true`

. If it isn't, change it to`true`

using the following command:`kubectl patch meshconfig osm-mesh-config -n kube-system -p '{"spec":{"traffic":{"enablePermissiveTrafficPolicyMode":true}}}' --type=merge`


## Clean up resources

When you no longer need the Azure resources, delete the deployment's test resource group using the

command.`az group delete`

`az group delete --name osm-bicep-test`

Alternatively, you can uninstall the OSM add-on and the related resources from your cluster. For more information, see

[Uninstall the Open Service Mesh add-on from your AKS cluster](open-service-mesh-uninstall-add-on).

## Next steps

This article showed you how to install the OSM add-on on an AKS cluster and verify that it's installed and running. With the OSM add-on installed on your cluster, you can [deploy a sample application](https://release-v1-0.docs.openservicemesh.io/docs/getting_started/install_apps/) or [onboard an existing application](https://release-v1-0.docs.openservicemesh.io/docs/guides/app_onboarding/) to work with your OSM mesh.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/update-azure-cni -->

# Update Azure CNI IPAM mode and data plane technology for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Existing Azure Kubernetes Service (AKS) clusters inevitably need an update to newer IP assignment management (IPAM) modes and data plane technologies to access the latest features and supportability. This article provides guidance on updating an existing AKS cluster to use Azure CNI Overlay for the IPAM mode and Azure CNI Powered by Cilium as the data plane.

## Update the IPAM mode to Azure CNI Overlay

Updating an existing cluster to Azure CNI Overlay is an irreversible process.

You can update an existing AKS cluster to Azure CNI Overlay if the cluster:

- Is on Kubernetes version 1.27 or later.
- Doesn't use the
[dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)feature. - Doesn't have network policies enabled. If you need to uninstall the network policy engine before updating your cluster, follow the steps in
[Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico). - Doesn't use any Windows node pools with Docker as the container runtime.

Before Windows OS build 20348.1668, there was a limitation around Windows overlay pods incorrectly routing packets from host network pods via Source Network Address Translation (SNAT). This limitation had a detrimental effect for clusters that were updating to Azure CNI Overlay. To avoid this issue, use Windows OS build 20348.1668 or later.

Warning

If you're using a custom

`azure-ip-masq-agent`

configuration to include additional IP ranges that shouldn't send SNAT packets from pods, updating to Azure CNI Overlay can break connectivity to these ranges. Pod IPs from the overlay space are unreachable by anything outside the cluster nodes.For old clusters, a ConfigMap might be left over from a previous version of

`azure-ip-masq-agent`

. If this ConfigMap (named`azure-ip-masq-agent-config`

) exists and isn't intentionally in place, you should delete it before updating.If you're not using a custom

`ip-masq-agent`

configuration, only the`azure-ip-masq-agent-config-reconciled`

ConfigMap should exist with respect to Azure`ip-masq-agent`

ConfigMap. It's updated automatically during the update process.

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately to Azure CNI Overlay isn't supported. Any disruptions to cluster networking are similar to a node image update or Kubernetes version upgrade where each node in a node pool is reimaged.

Update an existing Azure Container Networking Interface (CNI) cluster to use Azure CNI Overlay by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16
```


The `--pod-cidr`

parameter is required when you update from legacy CNI plugins because the pods need to get IPs from a new overlay space. The new overlay space doesn't overlap with the existing Azure CNI Node Subnet plugin.

Classless Inter-Domain Routing (CIDR) for the pod also can't overlap with any virtual network address of the node pools. For example, if your virtual network address is 10.0.0.0/8, and your nodes are in the subnet 10.240.0.0/16, the `--pod-cidr`

parameter can't overlap with 10.0.0.0/8 or the existing service CIDR on the cluster.

## Update the data plane to Azure CNI Powered by Cilium

When you enable Cilium in a cluster that uses a different network policy engine (Azure Network Policy Manager or Calico), the network policy engine is uninstalled and replaced with Cilium. For more information, see [Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico).

You can update an existing cluster to Azure CNI Powered by Cilium if the cluster doesn't have any Windows node pools.

Warning

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image update or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium begins enforcing network policies only after all nodes are reimaged.

To perform the update, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

Update an existing cluster to Azure CNI Powered by Cilium by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-dataplane cilium
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-azure-cni -->

# Update Azure CNI IPAM mode and data plane technology for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Existing Azure Kubernetes Service (AKS) clusters inevitably need an update to newer IP assignment management (IPAM) modes and data plane technologies to access the latest features and supportability. This article provides guidance on updating an existing AKS cluster to use Azure CNI Overlay for the IPAM mode and Azure CNI Powered by Cilium as the data plane.

## Update the IPAM mode to Azure CNI Overlay

Updating an existing cluster to Azure CNI Overlay is an irreversible process.

You can update an existing AKS cluster to Azure CNI Overlay if the cluster:

- Is on Kubernetes version 1.27 or later.
- Doesn't use the
[dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)feature. - Doesn't have network policies enabled. If you need to uninstall the network policy engine before updating your cluster, follow the steps in
[Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico). - Doesn't use any Windows node pools with Docker as the container runtime.

Before Windows OS build 20348.1668, there was a limitation around Windows overlay pods incorrectly routing packets from host network pods via Source Network Address Translation (SNAT). This limitation had a detrimental effect for clusters that were updating to Azure CNI Overlay. To avoid this issue, use Windows OS build 20348.1668 or later.

Warning

If you're using a custom

`azure-ip-masq-agent`

configuration to include additional IP ranges that shouldn't send SNAT packets from pods, updating to Azure CNI Overlay can break connectivity to these ranges. Pod IPs from the overlay space are unreachable by anything outside the cluster nodes.For old clusters, a ConfigMap might be left over from a previous version of

`azure-ip-masq-agent`

. If this ConfigMap (named`azure-ip-masq-agent-config`

) exists and isn't intentionally in place, you should delete it before updating.If you're not using a custom

`ip-masq-agent`

configuration, only the`azure-ip-masq-agent-config-reconciled`

ConfigMap should exist with respect to Azure`ip-masq-agent`

ConfigMap. It's updated automatically during the update process.

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately to Azure CNI Overlay isn't supported. Any disruptions to cluster networking are similar to a node image update or Kubernetes version upgrade where each node in a node pool is reimaged.

Update an existing Azure Container Networking Interface (CNI) cluster to use Azure CNI Overlay by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16
```


The `--pod-cidr`

parameter is required when you update from legacy CNI plugins because the pods need to get IPs from a new overlay space. The new overlay space doesn't overlap with the existing Azure CNI Node Subnet plugin.

Classless Inter-Domain Routing (CIDR) for the pod also can't overlap with any virtual network address of the node pools. For example, if your virtual network address is 10.0.0.0/8, and your nodes are in the subnet 10.240.0.0/16, the `--pod-cidr`

parameter can't overlap with 10.0.0.0/8 or the existing service CIDR on the cluster.

## Update the data plane to Azure CNI Powered by Cilium

When you enable Cilium in a cluster that uses a different network policy engine (Azure Network Policy Manager or Calico), the network policy engine is uninstalled and replaced with Cilium. For more information, see [Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico).

You can update an existing cluster to Azure CNI Powered by Cilium if the cluster doesn't have any Windows node pools.

Warning

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image update or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium begins enforcing network policies only after all nodes are reimaged.

To perform the update, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

Update an existing cluster to Azure CNI Powered by Cilium by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-dataplane cilium
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-kms-etcd-encryption -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-node-pools -->

# Upgrade node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to upgrade a single node pool and how to upgrade the cluster control plane for multiple node pools in Azure Kubernetes Service (AKS).

Note

As a best practice, you should upgrade all node pools in an AKS cluster to the same Kubernetes version. The default behavior of [`az aks upgrade`

][az-aks-upgrade] is to upgrade all node pools together with the control plane to achieve this alignment. The ability to upgrade individual node pools lets you perform a rolling upgrade and schedule pods between node pools to maintain application uptime.

## Upgrade a single node pool

Note

The node pool operating system (OS) image version is tied to the Kubernetes version of the cluster. You only get OS image upgrades following a cluster upgrade.

Check for any available upgrades using the [

`az aks get-upgrades`

][az-aks-get-upgrades] command.`az aks get-upgrades --resource-group <resource-group-name> --name <cluster-name>`

Upgrade a specific node pool using the [

`az aks nodepool upgrade`

][az-aks-nodepool-upgrade] command.`az aks nodepool upgrade \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --kubernetes-version <kubernetes-version> \ --no-wait`

Check the status of your node pool using the [

`az aks nodepool list`

][az-aks-nodepool-list] command.`az aks nodepool list --resource-group <resource-group-name> --cluster-name <cluster-name>`

The following example output shows the node pool is in the

*Upgrading*state:`[ { ... "count": 3, ... "name": "<node-pool-name>", "orchestratorVersion": "<kubernetes-version>", ... "provisioningState": "Upgrading", ... "vmSize": "Standard_DS2_v2", ... }, { ... "count": 2, ... "name": "<node-pool-name-2>", "orchestratorVersion": "<kubernetes-version-2>", ... "provisioningState": "Succeeded", ... "vmSize": "Standard_DS2_v2", ... } ]`

It takes a few minutes to upgrade the nodes to the specified version. After the upgrade is complete, the node pool's

`provisioningState`

changes to*Succeeded*.

## Upgrade a cluster control plane with multiple node pools

An AKS cluster has two cluster resource objects with Kubernetes versions associated to them: the cluster control plane Kubernetes version and a node pool with a Kubernetes version.

### Upgrade behavior for the control plane and node pools

The control plane maps to one or many node pools. The behavior of an upgrade operation depends on which Azure CLI command you use and the flags you specify:

upgrades the control plane and all node pools in the cluster to the same Kubernetes version.`az aks upgrade`

with the`az aks upgrade`

`--control-plane-only`

flag upgrades only the cluster control plane and leaves all node pools unchanged.upgrades only the target node pool with the specified Kubernetes version.`az aks nodepool upgrade`


### Validation rules for upgrades

Note

Kubernetes uses the standard [Semantic Versioning](https://semver.org/) versioning scheme. The version number is expressed as *x.y.z*, where *x* is the major version, *y* is the minor version, and *z* is the patch version. For example, in version *1.12.6*, *1* is the major version, *12* is the minor version, and *6* is the patch version. The Kubernetes version of the control plane and the initial node pool are set during cluster creation. Other node pools have their Kubernetes version set when they are added to the cluster. The Kubernetes versions may differ between node pools and between a node pool and the control plane.

Kubernetes upgrades for a cluster control plane and node pools are validated using the following sets of rules:

**Rules for valid versions to upgrade node pools**:- The node pool version must have the same
*major*version as the control plane. - The node pool
*minor*version must be within two*minor*versions of the control plane version. - The node pool version can't be greater than the control
`major.minor.patch`

version.

- The node pool version must have the same
**Rules for submitting an upgrade operation**:- You can't downgrade the control plane or a node pool Kubernetes version.
- If a node pool Kubernetes version isn't specified, the behavior depends on the client. In Azure Resource Manager (ARM) templates, declaration falls back to the existing version defined for the node pool. If nothing is set, it falls back to the control plane version.
- You can't simultaneously submit multiple operations on a single control plane or node pool resource. You can either upgrade or scale a control plane or a node pool at a given time.


## Next steps: Manage node pools in AKS

To learn more about managing node pools in AKS, see [Manage node pools in Azure Kubernetes Service (AKS)](manage-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/stop-cluster-upgrade-api-breaking-changes -->

# Stop Azure Kubernetes Service (AKS) cluster upgrades automatically on API breaking changes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to stop Azure Kubernetes Service (AKS) cluster upgrades automatically on API breaking changes.

## Overview

To stay within a supported Kubernetes version, you have to upgrade your cluster at least once per year and prepare for all possible disruptions. These disruptions include ones caused by API breaking changes, deprecations, and dependencies such as Helm and Container Storage Interface (CSI). It can be difficult to anticipate these disruptions and migrate critical workloads without experiencing any downtime.

You can configure your AKS cluster to automatically stop upgrade operations consisting of a minor version change with deprecated APIs and alert you to the issue. This feature helps you avoid unexpected disruptions and gives you time to address the deprecated APIs before proceeding with the upgrade.

## Before you begin

Before you begin, make sure you meet the following prerequisites:

- The upgrade operation is a Kubernetes minor version change for the cluster control plane.
- The Kubernetes version you're upgrading to is 1.26 or later.
- The last seen usage of deprecated APIs for the targeted version you're upgrading to must occur within 12 hours before the upgrade operation. AKS records usage hourly, so any usage of deprecated APIs within one hour isn't guaranteed to appear in the detection.

## Mitigate stopped upgrade operations

If you meet the [prerequisites](#before-you-begin), attempt an upgrade, and receive an error message similar to the following example error message:

```
Bad Request({
"code": "ValidationError",
"message": "Control Plane upgrade is blocked due to recent usage of a Kubernetes API deprecated in the specified version. Please refer to https://kubernetes.io/docs/reference/using-api/deprecation-guide to migrate the usage. To bypass this error, set enable-force-upgrade in upgradeSettings.overrideSettings. Bypassing this error without migrating usage will result in the deprecated Kubernetes API calls failing. Usage details: 1 error occurred:\n\t* usage has been detected on API flowcontrol.apiserver.k8s.io.prioritylevelconfigurations.v1beta1, and was recently seen at: 2023-03-23 20:57:18 +0000 UTC, which will be removed in 1.26\n\n",
"subcode": "UpgradeBlockedOnDeprecatedAPIUsage"
})
```


You have two options to mitigate the issue: you can [remove usage of deprecated APIs (recommended)](#remove-usage-of-deprecated-apis-recommended) or [bypass validation to ignore API changes](#bypass-validation-to-ignore-api-changes).

### Remove usage of deprecated APIs (recommended)

In the Azure portal, navigate to your cluster resource and select

**Diagnose and solve problems**Select

**Create, Upgrade, Delete, and Scale**>**Kubernetes API deprecations**.Wait 12 hours from the time the last deprecated API usage was seen. Read-Only verbs are excluded from the deprecated api usage namely

[Get/List/Watch](https://kubernetes.io/docs/reference/using-api/api-concepts/).(You can also check past API usage by enabling[Container insights](/en-us/azure/azure-monitor/containers/container-insights-log-query#resource-logs)and exploring kube audit logs.)Retry your cluster upgrade.


### Bypass validation to ignore API changes

Note

This method requires you to use the Azure CLI version 2.57 or later. If you have the preview CLI extension installed, you need to update to version `3.0.0b10`

or later. This method isn't recommended, as deprecated APIs in the targeted Kubernetes version might not work long term. We recommend removing them as soon as possible after the upgrade completes.

Bypass validation to ignore API breaking changes and invoke an upgrade. Specify the

`enable-force-upgrade`

flag and set the`upgrade-override-until`

property to define the end of the window during which validation is bypassed. If no value is set, it defaults the window to three days from the current time. The date and time you specify must be in the future.`az aks upgrade --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME --kubernetes-version $KUBERNETES_VERSION --enable-force-upgrade --upgrade-override-until 2023-10-01T13:00:00Z`

Note

`Z`

is the zone designator for the zero UTC/GMT offset, also known as 'Zulu' time. This example sets the end of the window to`13:00:00`

GMT. For more information, see[Combined date and time representations](https://wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).

## Next steps

This article showed you how to stop AKS cluster upgrades automatically on API breaking changes. To learn more about more upgrade options for AKS clusters, see [Upgrade options for Azure Kubernetes Service (AKS) clusters](upgrade-cluster).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/availability-zones -->

# Configure availability zones in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Availability zones](/en-us/azure/reliability/availability-zones-overview) help protect your applications and data from datacenter failures. Zones are unique physical locations within an Azure region. Each zone includes one or more datacenters equipped with independent power, cooling, and networking.

Using Azure Kubernetes Service (AKS) with availability zones physically distributes resources across different availability zones within a single region, improving reliability. Deploying nodes in multiple zones doesn't incur additional costs. For more information on AKS reliability features including availability zones, multi-region configurations, reliability during service maintenance, and backup, see [Reliability in AKS](/en-us/azure/reliability/reliability-aks).

This article shows you how to configure AKS resources to use availability zones.

## AKS resources

This diagram shows the Azure resources that are created when you create an AKS cluster:

### AKS control plane

Microsoft hosts the [AKS control plane](/en-us/azure/aks/core-aks-concepts#control-plane), the Kubernetes API server, and services such as `scheduler`

and `etcd`

as a managed service. Microsoft replicates the control plane in multiple zones.

Other resources of your cluster deploy in a managed resource group in your Azure subscription. By default, this resource group is prefixed with *MC_* for *managed cluster* and contains the resources mentioned in the following sections.

### Node pools

Node pools are created as virtual machine scale sets in your Azure subscription.

When you create an AKS cluster, one [system node pool](/en-us/azure/aks/use-system-pools) is required and is created automatically. It hosts critical system pods such as `CoreDNS`

and `metrics-server`

. You can add more [user node pools](/en-us/azure/aks/create-node-pools) to your AKS cluster to host your applications.

There are three ways node pools can be deployed:

- Zone-spanning
- Zone-aligned
- Regional

The system node pool zones are configured when the cluster or node pool is created.

#### Zone-spanning

In this configuration, nodes are spread across all selected zones. These zones are specified by using the `--zones`

parameter.

```
# Create an AKS cluster, and create a zone-spanning system node pool in all three AZs, one node in each AZ
az aks create --resource-group example-rg --name example-cluster --node-count 3 --zones 1 2 3
# Add one new zone-spanning user node pool, two nodes in each
az aks nodepool add --resource-group example-rg --cluster-name example-cluster --name userpool-a --node-count 6 --zones 1 2 3
```


AKS automatically balances the number of nodes between zones.

If a zonal outage occurs, nodes within the affected zone might be affected, but nodes in other availability zones remain unaffected.

To validate node locations, run the following command:

```
kubectl get nodes -o custom-columns='NAME:metadata.name, REGION:metadata.labels.topology\.kubernetes\.io/region, ZONE:metadata.labels.topology\.kubernetes\.io/zone'
```


```
NAME REGION ZONE
aks-nodepool1-34917322-vmss000000 eastus eastus-1
aks-nodepool1-34917322-vmss000001 eastus eastus-2
aks-nodepool1-34917322-vmss000002 eastus eastus-3
```


#### Zone-aligned

In this configuration, each node is aligned (pinned) to a specific zone. To create three node pools for a region with three availability zones:

```
# # Add three new zone-aligned user node pools, two nodes in each
az aks nodepool add --resource-group example-rg --cluster-name example-cluster --name userpool-x --node-count 2 --zones 1
az aks nodepool add --resource-group example-rg --cluster-name example-cluster --name userpool-y --node-count 2 --zones 2
az aks nodepool add --resource-group example-rg --cluster-name example-cluster --name userpool-z --node-count 2 --zones 3
```


This configuration can be used when you need [lower latency between nodes](/en-us/azure/aks/reduce-latency-ppg). It also provides more granular control over scaling operations, or when you're using the [cluster autoscaler](cluster-autoscaler-overview).

Note

If a single workload is deployed across node pools, we recommend setting `--balance-similar-node-groups`

to `true`

to maintain a balanced distribution of nodes across zones for your workloads during scale-up operations.

#### Regional (not using availability zones)

Regional mode is used when the zone assignment isn't set in the deployment template (for example, `"zones"=[]`

or `"zones"=null`

).

In this configuration, the node pool creates regional (not zone-pinned) instances and implicitly places instances throughout the region. There's no guarantee that instances are balanced or spread across zones, or that instances are in the same availability zone.

In the rare case of a full zonal outage, any or all instances within the node pool might be affected.

To validate node locations, run the following command:

```
kubectl get nodes -o custom-columns='NAME:metadata.name, REGION:metadata.labels.topology\.kubernetes\.io/region, ZONE:metadata.labels.topology\.kubernetes\.io/zone'
```


```
NAME REGION ZONE
aks-nodepool1-34917322-vmss000000 eastus 0
aks-nodepool1-34917322-vmss000001 eastus 0
aks-nodepool1-34917322-vmss000002 eastus 0
```


## Deployments

### Pods

Kubernetes is aware of Azure availability zones, and can balance pods across nodes in different zones. In the event a zone becomes unavailable, Kubernetes moves pods away from affected nodes automatically.

As documented in the Kubernetes reference [Well-Known Labels, Annotations and Taints](https://kubernetes.io/docs/reference/labels-annotations-taints/), Kubernetes uses the `topology.kubernetes.io/zone`

label to automatically distribute pods in a replication controller or service across the various available zones available.

To see which pods and nodes are running, run the following command:

```
kubectl describe pod | grep -e "^Name:" -e "^Node:"
```


The `maxSkew`

parameter describes the degree to which pods might be unevenly distributed. Assuming three zones and three replicas, setting this value to `1`

ensures that each zone has at least one pod running:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: my-deployment
spec:
selector:
matchLabels:
app: my-app
template:
metadata:
labels:
app: my-app
spec:
topologySpreadConstraints:
- maxSkew: 1
topologyKey: topology.kubernetes.io/zone
whenUnsatisfiable: DoNotSchedule
labelSelector:
matchLabels:
app: my-app
containers:
- name: my-container
image: my-image
```


### Storage and volumes

By default, Kubernetes versions 1.29 and later use Azure Managed Disks by using zone-redundant storage for Persistent Volume Claims.

These disks are replicated between zones, to enhance the resilience of your applications. This action helps to safeguard your data against datacenter failures.

The following example shows a Persistent Volume Claim that uses Azure Standard SSD in zone-redundant storage:

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: azure-managed-disk
spec:
accessModes:
- ReadWriteOnce
storageClassName: managed-csi
#storageClassName: managed-csi-premium
resources:
requests:
storage: 5Gi
```


For zone-aligned deployments, you can create a new storage class with the `skuname`

parameter set to `LRS`

(locally redundant storage). You can then use the new storage class in your Persistent Volume Claim.

Although locally redundant storage disks are less expensive, they aren't zone-redundant, and attaching a disk to a node in a different zone isn't supported.

The following example shows a locally redundant storage Standard SSD storage class:

```
kind: StorageClass
metadata:
name: azuredisk-csi-standard-lrs
provisioner: disk.csi.azure.com
parameters:
skuname: StandardSSD_LRS
#skuname: PremiumV2_LRS
```


### Load balancers

Kubernetes deploys Azure Standard Load Balancer by default, which balances inbound traffic across all zones in a region. If a node becomes unavailable, the load balancer reroutes traffic to healthy nodes.

An example service that uses Azure Load Balancer:

```
apiVersion: v1
kind: Service
metadata:
name: example
spec:
type: LoadBalancer
selector:
app: myapp
ports:
- port: 80
targetPort: 8080
```


Important

Starting on **September 30, 2025**, Azure Kubernetes Service (AKS) no longer supports Basic Load Balancer. To avoid any potential service disruptions, we recommend using Standard Load Balancer for new deployments and [upgrading any existing deployments to the Standard Load Balancer](/en-us/azure/load-balancer/load-balancer-basic-upgrade-guidance). For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/5020) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates/azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer/). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Limitations

The following limitations apply when you're using availability zones:

- See
[Quotas, virtual machine size restrictions, and region availability in AKS](quotas-skus-regions#supported-vm-sizes). - The number of availability zones used
*can't be changed*after the node pool is created. - Most regions support availability zones.
[See a list of regions](/en-us/azure/reliability/regions-list).

## Related content

- Learn about
[Reliability in AKS](/en-us/azure/reliability/reliability-aks). - Learn about
[system node pools](/en-us/azure/aks/use-system-pools). - Learn about
[user node pools](/en-us/azure/aks/create-node-pools). - Learn about
[load balancers](/en-us/azure/aks/load-balancer-standard). - Get
[best practices for business continuity and disaster recovery in AKS](operator-best-practices-storage).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-aks-ipam-and-dataplane -->

# Update Azure CNI IPAM mode and data plane technology for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Existing Azure Kubernetes Service (AKS) clusters inevitably need an update to newer IP assignment management (IPAM) modes and data plane technologies to access the latest features and supportability. This article provides guidance on updating an existing AKS cluster to use Azure CNI Overlay for the IPAM mode and Azure CNI Powered by Cilium as the data plane.

## Update the IPAM mode to Azure CNI Overlay

Updating an existing cluster to Azure CNI Overlay is an irreversible process.

You can update an existing AKS cluster to Azure CNI Overlay if the cluster:

- Is on Kubernetes version 1.27 or later.
- Doesn't use the
[dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)feature. - Doesn't have network policies enabled. If you need to uninstall the network policy engine before updating your cluster, follow the steps in
[Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico). - Doesn't use any Windows node pools with Docker as the container runtime.

Before Windows OS build 20348.1668, there was a limitation around Windows overlay pods incorrectly routing packets from host network pods via Source Network Address Translation (SNAT). This limitation had a detrimental effect for clusters that were updating to Azure CNI Overlay. To avoid this issue, use Windows OS build 20348.1668 or later.

Warning

If you're using a custom

`azure-ip-masq-agent`

configuration to include additional IP ranges that shouldn't send SNAT packets from pods, updating to Azure CNI Overlay can break connectivity to these ranges. Pod IPs from the overlay space are unreachable by anything outside the cluster nodes.For old clusters, a ConfigMap might be left over from a previous version of

`azure-ip-masq-agent`

. If this ConfigMap (named`azure-ip-masq-agent-config`

) exists and isn't intentionally in place, you should delete it before updating.If you're not using a custom

`ip-masq-agent`

configuration, only the`azure-ip-masq-agent-config-reconciled`

ConfigMap should exist with respect to Azure`ip-masq-agent`

ConfigMap. It's updated automatically during the update process.

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately to Azure CNI Overlay isn't supported. Any disruptions to cluster networking are similar to a node image update or Kubernetes version upgrade where each node in a node pool is reimaged.

Update an existing Azure Container Networking Interface (CNI) cluster to use Azure CNI Overlay by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16
```


The `--pod-cidr`

parameter is required when you update from legacy CNI plugins because the pods need to get IPs from a new overlay space. The new overlay space doesn't overlap with the existing Azure CNI Node Subnet plugin.

Classless Inter-Domain Routing (CIDR) for the pod also can't overlap with any virtual network address of the node pools. For example, if your virtual network address is 10.0.0.0/8, and your nodes are in the subnet 10.240.0.0/16, the `--pod-cidr`

parameter can't overlap with 10.0.0.0/8 or the existing service CIDR on the cluster.

## Update the data plane to Azure CNI Powered by Cilium

When you enable Cilium in a cluster that uses a different network policy engine (Azure Network Policy Manager or Calico), the network policy engine is uninstalled and replaced with Cilium. For more information, see [Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico).

You can update an existing cluster to Azure CNI Powered by Cilium if the cluster doesn't have any Windows node pools.

Warning

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image update or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium begins enforcing network policies only after all nodes are reimaged.

To perform the update, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

Update an existing cluster to Azure CNI Powered by Cilium by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-dataplane cilium
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-byo-cni -->

# Bring your own CNI plugin with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes doesn't provide a network interface system by default. Instead, [network plugins](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/) provide this functionality. Azure Kubernetes Service (AKS) provides several supported Container Network Interface (CNI) plugins. For information on supported plugins, see [Networking concepts for applications in Azure Kubernetes Service](concepts-network).

The supported plugins meet most networking needs in Kubernetes. However, advanced AKS users might want the same CNI plugin that they used in on-premises Kubernetes environments. Or these users might want to use advanced functionalities available in other CNI plugins.

This article shows how to deploy an AKS cluster with no CNI plugin preinstalled. From there, you can install any CNI plugin that works in Azure.

## Support

Microsoft support can't assist with CNI-related issues in clusters that you deploy by bringing your own CNI plugin. For example, CNI-related issues would cover most east/west (pod to pod) traffic, along with `kubectl proxy`

and similar commands. If you want CNI-related support, use a supported AKS network plugin or seek support from the CNI plugin vendor.

Microsoft still provides support for issues that aren't related to CNI.

## Prerequisites

- For Azure Resource Manager or Bicep, use at least template version 2022-01-02-preview or 2022-06-01.
- For the Azure CLI, use at least version 2.39.0.
- The virtual network for the AKS cluster must allow outbound internet connectivity.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for the address range for the Kubernetes service, pods, or cluster virtual network. - The cluster identity that the AKS cluster uses must have at least
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)permissions on the subnet within your virtual network. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, the following permissions are required:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


- The subnet assigned to the AKS node pool can't be a
[delegated subnet](/en-us/azure/virtual-network/subnet-delegation-overview). - AKS doesn't apply network security groups (NSGs) to its subnet or modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure that the security rules in the NSGs allow traffic within the node's Classless Inter-Domain Routing (CIDR) range. For more information, see
[Network security groups](concepts-network#network-security-groups). - AKS doesn't create a route table in the managed virtual network.
- You must specify a Pod CIDR (IP address range for pods). The AKS control plane uses this range for internal traffic routing to pods, even though pod IP assignment will be managed by your custom CNI. If no pod CIDR is provided, control plane to pod communication may fail or be misrouted. You must select a pod CIDR that does not conflict with any other network in your environment and avoids Azure reserved ranges, such as,
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

. For example, you might use a range such as`10.XX.0.0/16`

that is unique to your cluster. This ensures that the control plane can route directly to pod IPs on your nodes, and no IP overlap will occur if you integrate with other networks or clusters.

## Create an AKS cluster with no CNI plugin preinstalled

Create an Azure resource group for your AKS cluster by using the

command.`az group create`

`az group create --location eastus --name myResourceGroup`

Create an AKS cluster by using the

command. Pass the`az aks create`

`--network-plugin`

parameter with the parameter value of`none`

.`az aks create \ --location eastus \ --resource-group myResourceGroup \ --name myAKSCluster \ --network-plugin none \ --pod-cidr "10.10.0.0/16" \ --generate-ssh-keys`


## Deploy a CNI plugin

After AKS provisioning finishes, the cluster is online. But all the nodes are in a `NotReady`

state, as shown in the following example:

```
$ kubectl get nodes
NAME STATUS ROLES AGE VERSION
aks-nodepool1-23902496-vmss000000 NotReady agent 6m9s v1.21.9
$ kubectl get node -o custom-columns='NAME:.metadata.name,STATUS:.status.conditions[?(@.type=="Ready")].message'
NAME STATUS
aks-nodepool1-23902496-vmss000000 container runtime network not ready: NetworkReady=false reason:NetworkPluginNotReady message:Network plugin returns error: cni plugin not initialized
```


At this point, the cluster is ready for installation of a CNI plugin.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/rdp -->

# Connect with RDP to Azure Kubernetes Service (AKS) cluster Windows Server nodes for maintenance or troubleshooting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Throughout the lifecycle of your Azure Kubernetes Service (AKS) cluster, you may need to access an AKS Windows Server node. This access could be for maintenance, log collection, or other troubleshooting operations. You can access the AKS Windows Server nodes using RDP. For security purposes, the AKS nodes aren't exposed to the internet.

Alternatively, if you want to SSH to your AKS Windows Server nodes, you need access to the same key-pair that was used during cluster creation. Follow the steps in [SSH into Azure Kubernetes Service (AKS) cluster nodes](ssh).

This article shows you how to create an RDP connection with an AKS node using their private IP addresses.

## Before you begin

This article assumes that you have an existing AKS cluster with a Windows Server node. If you need an AKS cluster, see the article on [creating an AKS cluster with a Windows container using the Azure CLI](learn/quick-windows-container-deploy-cli). You need the Windows administrator username and password for the Windows Server node you want to troubleshoot. You also need an RDP client such as [Microsoft Remote Desktop](https://aka.ms/rdmac).

If you need to reset the password, use `az aks update`

to change the password.

```
az aks update --resource-group myResourceGroup --name myAKSCluster --windows-admin-password $WINDOWS_ADMIN_PASSWORD
```


If you need to reset the username and password, see [Reset Remote Desktop Services or its administrator password in a Windows VM](/en-us/troubleshoot/azure/virtual-machines/reset-rdp).

You also need the Azure CLI version 2.0.61 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Deploy a virtual machine to the same subnet as your cluster

The Windows Server nodes of your AKS cluster don't have externally accessible IP addresses. To make an RDP connection, you can deploy a virtual machine with a publicly accessible IP address to the same subnet as your Windows Server nodes.

The following example creates a virtual machine named *myVM* in the *myResourceGroup* resource group.

You need to get the subnet ID used by your Windows Server node pool and query for:

- The cluster's node resource group
- The virtual network
- The subnet's name
- The subnet ID

```
CLUSTER_RG=$(az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv)
VNET_NAME=$(az network vnet list --resource-group $CLUSTER_RG --query [0].name -o tsv)
SUBNET_NAME=$(az network vnet subnet list --resource-group $CLUSTER_RG --vnet-name $VNET_NAME --query [0].name -o tsv)
SUBNET_ID=$(az network vnet subnet show --resource-group $CLUSTER_RG --vnet-name $VNET_NAME --name $SUBNET_NAME --query id -o tsv)
```


Now that you've the SUBNET_ID, run the following command in the same Azure Cloud Shell window to create the VM:

```
PUBLIC_IP_ADDRESS="myVMPublicIP"
az vm create \
--resource-group myResourceGroup \
--name myVM \
--image win2019datacenter \
--admin-username azureuser \
--admin-password {admin-password} \
--subnet $SUBNET_ID \
--nic-delete-option delete \
--os-disk-delete-option delete \
--nsg "" \
--public-ip-address $PUBLIC_IP_ADDRESS \
--query publicIpAddress -o tsv
```


The following example output shows the VM has been successfully created and displays the public IP address of the virtual machine.

```
13.62.204.18
```


Record the public IP address of the virtual machine. You'll use this address in a later step.

## Allow access to the virtual machine

AKS node pool subnets are protected with NSGs (Network Security Groups) by default. To get access to the virtual machine, you'll have to enabled access in the NSG.

Note

The NSGs are controlled by the AKS service. Any change you make to the NSG will be overwritten at any time by the control plane.

First, get the resource group and name of the NSG to add the rule to:

```
CLUSTER_RG=$(az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv)
NSG_NAME=$(az network nsg list --resource-group $CLUSTER_RG --query [].name -o tsv)
```


Then, create the NSG rule:

```
az network nsg rule create \
--name tempRDPAccess \
--resource-group $CLUSTER_RG \
--nsg-name $NSG_NAME \
--priority 100 \
--destination-port-range 3389 \
--protocol Tcp \
--description "Temporary RDP access to Windows nodes"
```


## Get the node address

To manage a Kubernetes cluster, you use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client. If you use Azure Cloud Shell, `kubectl`

is already installed. To install `kubectl`

locally, use the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command:

```
az aks install-cli
```


To configure `kubectl`

to connect to your Kubernetes cluster, use the [az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```


List the internal IP address of the Windows Server nodes using the [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command:

```
kubectl get nodes -o wide
```


The following example output shows the internal IP addresses of all the nodes in the cluster, including the Windows Server nodes.

```
$ kubectl get nodes -o wide
NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME
aks-nodepool1-42485177-vmss000000 Ready agent 18h v1.12.7 10.240.0.4 <none> Ubuntu 16.04.6 LTS 4.15.0-1040-azure docker://3.0.4
aksnpwin000000 Ready agent 13h v1.12.7 10.240.0.67 <none> Windows Server Datacenter 10.0.17763.437
```


Record the internal IP address of the Windows Server node you wish to troubleshoot. You'll use this address in a later step.

## Connect to the virtual machine and node

Connect to the public IP address of the virtual machine you created earlier using an RDP client such as [Microsoft Remote Desktop](https://aka.ms/rdmac).

After you have connected to your virtual machine, connect to the *internal IP address* of the Windows Server node you want to troubleshoot using an RDP client from within your virtual machine.

You're now connected to your Windows Server node.

You can now run any troubleshooting commands in the *cmd* window. Since Windows Server nodes use Windows Server Core, there's not a full GUI or other GUI tools when you connect to a Windows Server node over RDP.

## Remove RDP access

When done, exit the RDP connection to the Windows Server node then exit the RDP session to the virtual machine. After you exit both RDP sessions, delete the virtual machine with the [az vm delete](/en-us/cli/azure/vm#az-vm-delete) command:

```
# Delete the virtual machine
az vm delete \
--resource-group myResourceGroup \
--name myVM
```


Delete the public IP associated with the virtual machine:

```
az network public-ip delete \
--resource-group myResourceGroup \
--name $PUBLIC_IP_ADDRESS
```


Delete the NSG rule:

```
CLUSTER_RG=$(az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv)
NSG_NAME=$(az network nsg list --resource-group $CLUSTER_RG --query [].name -o tsv)
az network nsg rule delete \
--resource-group $CLUSTER_RG \
--nsg-name $NSG_NAME \
--name tempRDPAccess
```


## Connect with Azure Bastion

Alternatively, you can use [Azure Bastion](/en-us/azure/bastion/bastion-overview) to connect to your Windows Server node.

### Deploy Azure Bastion

To deploy Azure Bastion, you'll need to find the virtual network your AKS cluster is connected to.

- In the Azure portal, go to
**Virtual networks**. Select the virtual network your AKS cluster is connected to. - Under
**Settings**, select**Bastion**, then select**Deploy Bastion**. Wait until the process is finished before going to the next step.

### Connect to your Windows Server nodes using Azure Bastion

Go to the node resource group of the AKS cluster. Run the command below in the Azure Cloud Shell to get the name of your node resource group:

```
az aks show --name myAKSCluster --resource-group myResourceGroup --query 'nodeResourceGroup' -o tsv
```


- Select
**Overview**, and select your Windows node pool virtual machine scale set. - Under
**Settings**, select**Instances**. Select a Windows server node that you'd like to connect to. - Under
**Support + troubleshooting**, select**Bastion**. - Enter the credentials you set up when the AKS cluster was created. Select
**Connect**.

You can now run any troubleshooting commands in the *cmd* window. Since Windows Server nodes use Windows Server Core, there's not a full GUI or other GUI tools when you connect to a Windows Server node over RDP.

Note

If you close out of the terminal window, press **CTRL + ALT + End**, select **Task Manager**, select **More details**, select **File**, select **Run new task**, and enter **cmd.exe** to open another terminal. You can also logout and re-connect with Bastion.

### Remove Bastion access

When you're finished, exit the Bastion session and remove the Bastion resource.

- In the Azure portal, go to
**Bastion**and select the Bastion resource you created. - At the top of the page, select
**Delete**. Wait until the process is complete before proceeding to the next step. - In the Azure portal, go to
**Virtual networks**. Select the virtual network that your AKS cluster is connected to. - Under
**Settings**, select**Subnet**, and delete the**AzureBastionSubnet**subnet that was created for the Bastion resource.

## Next steps

If you need more troubleshooting data, you can [view the Kubernetes primary node logs](monitor-aks#aks-control-plane-resource-logs) or [Azure Monitor](/en-us/azure/azure-monitor/containers/container-insights-overview).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-blob-csi -->

# Azure storage CSI driver and volume provisioning

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Blob storage Container Storage Interface (CSI) driver is a
[CSI specification](https://github.com/container-storage-interface/spec/blob/master/spec.md)-compliant driver used by Azure Kubernetes Service (AKS) to
manage the lifecycle of Azure Blob storage. The CSI is a standard for exposing arbitrary block and
file storage systems to containerized workloads on Kubernetes.

By adopting and using CSI, AKS now can write, deploy, and iterate plug-ins to expose new or improve existing storage systems in Kubernetes. Using CSI drivers in AKS avoids having to touch the core Kubernetes code and wait for its release cycles.

When you mount Azure Blob storage as a file system into a container or pod, it enables you to use blob storage with many applications that work massive amounts of unstructured data. For example:

- Log file data
- Images, documents, and streaming video or audio
- Disaster recovery data

Applications access data stored in Azure Blob storage using either BlobFuse or the Network File System (NFS) 3.0 protocol. Before the introduction of the Azure Blob storage CSI driver, the only option was to manually install an unsupported driver to access Blob storage from your application running on AKS. When the Azure Blob storage CSI driver is enabled on AKS, there are two built-in storage classes:

- azureblob-fuse-premium
- azureblob-nfs-premium

To create an AKS cluster with CSI drivers support, see [CSI drivers on AKS](csi-storage-drivers). To
learn more about the differences in access between each of the Azure storage types using the NFS
protocol, see
[Compare access to Azure Files, Blob Storage, and Azure NetApp Files with NFS](/en-us/azure/storage/common/nfs-comparison).

The Azure Disks Container Storage Interface (CSI) driver is a
[CSI specification](https://github.com/container-storage-interface/spec/blob/master/spec.md)-compliant
driver used by Azure Kubernetes Service (AKS) to manage the lifecycle of Azure Disk.

The CSI is a standard for exposing arbitrary block and file storage systems to containerized
workloads on Kubernetes. By adopting and using CSI, AKS now can write, deploy, and iterate plug-ins
to expose new or improve existing storage systems in Kubernetes. Using CSI drivers in AKS avoids
having to touch the core Kubernetes code and wait for its release cycles. To create an AKS cluster
with CSI driver support, see [Enable CSI driver on AKS](csi-storage-drivers).

For more information on Kubernetes volumes, see [Storage options for applications in AKS](concepts-storage).

Note

*In-tree drivers* refer to the current storage drivers that are part of the core Kubernetes code versus the new CSI drivers, which are plug-ins.

The Azure Files Container Storage Interface (CSI) driver is a
[CSI specification](https://github.com/container-storage-interface/spec/blob/master/spec.md)-compliant driver used by Azure Kubernetes Service (AKS) to
manage the lifecycle of Azure file shares. The CSI is a standard for exposing arbitrary block and
file storage systems to containerized workloads on Kubernetes.

By adopting and using CSI, AKS now can write, deploy, and iterate plug-ins to expose new or improve existing storage systems in Kubernetes. Using CSI drivers in AKS avoids having to touch the core Kubernetes code and wait for its release cycles.

To create an AKS cluster with CSI drivers support, see [Enable CSI drivers on AKS](csi-storage-drivers).

Note

*In-tree drivers* refer to the current storage drivers that are part of the core Kubernetes code versus the new CSI drivers, which are plug-ins.

## Azure CSI driver features

Azure Blob storage CSI driver supports the following features:

- BlobFuse
- NFS 3.0 protocol

In addition to in-tree driver features, Azure Disk CSI driver supports the following features:

Performance improvements during concurrent disk attach and detach

- In-tree drivers attach or detach disks in serial, while CSI drivers attach or detach disks in batch. There's significant improvement when there are multiple disks attaching to one node.

Premium SSD v1 and v2 are supported.

`PremiumV2_LRS`

only supports`None`

caching mode

Zone-redundant storage (ZRS) disk support

`Premium_ZRS`

,`StandardSSD_ZRS`

disk types are supported. ZRS disk could be scheduled on the zone or non-zone node, without the restriction that disk volume should be colocated in the same zone as a given node. For more information, including which regions are supported, see[Zone-redundant storage for managed disks](/en-us/azure/virtual-machines/disks-redundancy).


Note

Depending on the VM SKU that's being used, the Azure Disk CSI driver might have a per-node volume limit. For some powerful VMs (for example, 16 cores), the limit is 64 volumes per node. To identify the limit per VM SKU, review the **Max data disks** column for each VM SKU offered. For a list of VM SKUs offered and their corresponding detailed capacity limits, see [General purpose virtual machine sizes](/en-us/azure/virtual-machines/sizes-general).

## Prerequisites

You must have the Azure CLI version 2.42 or later installed and configured. To find the version, run

`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). If you installed the Azure CLI`aks-preview`

extension, make sure that you update the extension to the latest version by calling`az extension update --name aks-preview`

.Perform the following steps to

[clean up the open source driver](https://github.com/kubernetes-sigs/blob-csi-driver/blob/master/docs/install-csi-driver-master.md#clean-up-blob-csi-driver)if you previously installed the[CSI Blob Storage open-source driver](https://github.com/kubernetes-sigs/blob-csi-driver)to access Azure Blob storage from your cluster.Your AKS cluster

*Control plane*identity (your AKS cluster name) is added to the[Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)role on the VNet and network security group.To support an [Azure Data Lake Storage Gen2 account][azure-datalake-storage-account] (ADLS) when using BlobFuse mount, perform the following actions:

- To create an ADLS account using the driver in dynamic provisioning, specify
`isHnsEnabled: "true"`

in the storage class parameters. - To enable BlobFuse access to an ADLS account in static provisioning, specify the mount option
`--use-adls=true`

in the persistent volume. - If you're going to enable a storage account with Hierarchical Namespace, existing persistent volumes (PVs) should be remounted with
`--use-adls=true`

mount option.

- To create an ADLS account using the driver in dynamic provisioning, specify
By default, the BlobFuse cache is located in the

`/mnt`

directory. If the virtual machine (VM) SKU provides a temporary disk, the`/mnt`

directory is mounted on the temporary disk. However, if the VM SKU doesn't provide a temporary disk, the`/mnt`

directory is mounted on the OS disk, you could set`--tmp-path=`

mount option to specify a different cache directory.

Note

If the **blobfuse-proxy** isn't enabled during the installation of the open source driver, the uninstallation of the open source driver disrupts existing blobfuse mounts. However, NFS mounts remain unaffected.

You must have an AKS cluster with the Azure Disk CSI driver enabled. The CSI driver is enabled by default on AKS clusters running Kubernetes version 1.21 or later.

Azure CLI version 2.37.0 or later is installed and configured. Run

`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The

`kubectl`

command-line tool is installed and configured to connect to your AKS cluster.A storage class configured to use the Azure Disk CSI driver (

`disk.csi.azure.com`

).The Azure Disk CSI driver has a per-node volume limit. The volume count changes based on the size of the node/node pool. Run the

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command to determine the number of volumes that can be allocated per node:`kubectl get CSINode <nodename> -o yaml`

If the per-node volume limit is an issue for your workload, consider using

[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction)for persistent volumes instead of CSI drivers.

**General requirements:**

You must have an AKS cluster with the Azure Files CSI driver enabled. The Azure Files CSI driver is enabled by default on AKS clusters running Kubernetes version 1.21 or later.

Azure CLI version 2.37.0 or later is installed and configured. To check your version, run

`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The

`kubectl`

command-line tool is installed and configured to connect to your AKS cluster.A storage class configured to use the Azure Files CSI driver (

`file.csi.azure.com`

).When choosing between standard and premium file shares, it's important you understand the provisioning model and requirements of the expected usage pattern you plan to run on Azure Files. For more information, see

[Choosing an Azure Files performance tier based on usage patterns](/en-us/azure/storage/files/understand-performance#choosing-a-performance-tier-based-on-usage-patterns).

**Network File Share (NFS) requirements:**

Your AKS cluster

*Control plane*identity (your AKS cluster name) is added to the[Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)role on the VNet and**NetworkSecurityGroup**.Your AKS cluster's service principal or managed service identity (MSI) must be added to the

**Contributor**role to the storage account.

**Managed Identity requirements:**

Ensure the

[user-assigned Kubelet identity](use-managed-identity#create-a-kubelet-managed-identity)is granted the`Storage File Data SMB MI Admin`

role on the storage account. If you use your own storage account, you need to assign`Storage File Data SMB MI Admin`

role to the user-assigned Kubelet identity on that storage account.If the CSI driver creates the storage account, grant the

`Storage File Data SMB MI Admin`

role to the resource group where the storage account resides.If you use the default built-in user-assigned Kubelet identity, it already has the required

`Storage File Data SMB MI Admin`

role on the managed node resource group.

Note

The Azure File CSI driver only permits the mounting of SMB file shares using key-based (NTLM v2) authentication, and therefore doesn't support the maximum security profile of Azure File share settings. On the other hand, mounting NFS file shares doesn't require key-based authentication.

## Enable CSI driver on a new or existing AKS cluster

Using the Azure CLI, you can enable the Blob storage CSI driver on a new or existing AKS cluster before you configure a persistent volume for use by pods in the cluster.

To enable the driver on a new cluster, include the

`--enable-blob-driver`

parameter with the`az aks create`

command as shown in the following example:`az aks create \ --enable-blob-driver \ --name myAKSCluster \ --resource-group myResourceGroup \ --generate-ssh-keys`

To enable the driver on an existing cluster, include the

`--enable-blob-driver`

parameter with the`az aks update`

command as shown in the following example:`az aks update --enable-blob-driver --name myAKSCluster --resource-group myResourceGroup`


You're prompted to confirm there isn't an open-source Blob CSI driver installed. After you confirm, it might take several minutes to complete this action. Once it's complete, you should see in the output the status of enabling the driver on your cluster. The following example resembles the section indicating the results of the previous command:

```
"storageProfile": {
"blobCsiDriver": {
"enabled": true
},
...
}
```


## Disable CSI driver on an existing AKS cluster

Using the Azure CLI, you can disable the Blob storage CSI driver on an existing AKS cluster after you remove the persistent volume from the cluster.

To disable the driver on an existing cluster, include the

`--disable-blob-driver`

parameter with the`az aks update`

command as shown in the following example:`az aks update --disable-blob-driver --name myAKSCluster --resource-group myResourceGroup`


## Use a persistent volume for storage

Kubernetes assigns a [persistent volume](concepts-storage#persistent-volumes) (PV) as a storage resource to one or more pods. You can provision PVs dynamically through Kubernetes or statically as an administrator.

If multiple pods need concurrent access to the same storage volume, you can use Azure Blob storage to connect by using NFS or BlobFuse. This article shows you how to dynamically create an Azure Blob storage container for use by multiple pods in an AKS cluster.

For more information on Kubernetes volumes, see [Storage options for applications in AKS](concepts-storage).

This article shows you how to dynamically create a PV with Azure disk for use by a single pod in an AKS cluster.

If multiple pods need concurrent access to the same storage volume, you can use Azure Files to
connect by using the [Server Message Block (SMB)](/en-us/windows/desktop/FileIO/microsoft-smb-protocol-and-cifs-protocol-overview) or
[Network File System (NFS)](/en-us/windows-server/storage/nfs/nfs-overview). This article shows you how to dynamically create an Azure
Files share for use by multiple pods in an AKS cluster.

**Dynamically provisioned volume:** Use this approach when you want Kubernetes to automatically
create and manage storage resources. It's ideal for scenarios where you need on-demand scaling,
prefer infrastructure-as-code, and want to minimize manual configuration steps.

**Statically provisioned volume:** Choose this method if you already have an Azure Blob storage
account or container that you want to use. It provides more control over storage setup, access, and
lifecycle, and is suitable when you need to connect to existing resources or reuse storage across
multiple clusters or workloads.

This section provides guidance for cluster administrators who want to provision one or more persistent volumes that include details of Blob storage for use by a workload. A persistent volume claim (PVC) uses the storage class object to dynamically provision an Azure Blob storage container.

To provision a persistent volume using Azure Blob storage with the provided storage class, follow these steps:

Create the

`StorageClass`

manifest by saving the following YAML to a file named`blob-fuse-sc.yaml`

:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: blob-fuse provisioner: blob.csi.azure.com parameters: skuName: Premium_LRS # available values: Standard_LRS, Premium_LRS, Standard_GRS, Standard_RAGRS, Standard_ZRS, Premium_ZRS protocol: fuse2 networkEndpointType: privateEndpoint reclaimPolicy: Delete volumeBindingMode: Immediate allowVolumeExpansion: true mountOptions: - -o allow_other - --file-cache-timeout-in-seconds=120 - --use-attr-cache=true - --cancel-list-on-mount-seconds=10 # prevent billing charges on mounting - -o attr_timeout=120 - -o entry_timeout=120 - -o negative_timeout=120 - --log-level=LOG_WARNING # LOG_WARNING, LOG_INFO, LOG_DEBUG - --cache-size-mb=1000 # Default will be 80% of available memory, eviction will happen beyond specified value.`

To create the storage class in your cluster, apply the

`StorageClass`

by running the following command:`kubectl apply -f blob-fuse-sc.yaml`


## Create a PVC using built-in storage class

A storage class is used to define how an Azure Blob storage container is created. A storage account is automatically created in the node resource group for use with the storage class to hold the Azure Blob storage container. Choose one of the following Azure storage redundancy SKUs for skuName:

**Standard_LRS**: Standard locally redundant storage**Premium_LRS**: Premium locally redundant storage**Standard_ZRS**: Standard zone redundant storage**Premium_ZRS**: Premium zone redundant storage**Standard_GRS**: Standard geo-redundant storage**Standard_RAGRS**: Standard read-access geo-redundant storage

When you use storage CSI drivers on AKS, there are two other built-in `StorageClasses`

that use the Azure Blob CSI storage driver.

The reclaim policy on both storage classes ensures that the underlying Azure Blob storage is deleted
when the respective PV is deleted. The storage classes also configure the container to be expandable
by default, as the `set allowVolumeExpansion`

parameter is set to **true**.

Note

Shrinking persistent volumes isn't supported.

Use the [kubectl get sc](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command to see the storage classes. The following example
shows the `azureblob-fuse-premium`

and `azureblob-nfs-premium`

storage classes available within an
AKS cluster:

```
NAME PROVISIONER RECLAIMPOLICY VOLUMEBINDINGMODE ALLOWVOLUMEEXPANSION AGE
azureblob-fuse-premium blob.csi.azure.com Delete Immediate true 23h
azureblob-nfs-premium blob.csi.azure.com Delete Immediate true 23h
```


To use these storage classes, create a PVC and respective pod that references and uses them. A PVC is used to automatically allocate storage based on a storage class. You can create a PVC using one of the built-in storage classes or a custom storage class. This PVC creates an Azure Blob storage container with your specified SKU, size, and protocol. When you create a pod definition, the PVC is specified to request the desired storage.

A PVC uses the storage class object to dynamically provision an Azure Blob storage container. The following YAML can be used to create a 5 GB PVC with *ReadWriteMany* access, using the built-in storage class. For more information on access modes, see the [Kubernetes persistent volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) documentation.

Create a file named

`blob-nfs-pvc.yaml`

and copy the following YAML:`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: azure-blob-storage spec: accessModes: - ReadWriteMany storageClassName: azureblob-nfs-premium resources: requests: storage: 5Gi`

Create the PVC with the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command:`kubectl create -f blob-nfs-pvc.yaml`


Once complete, the Blob storage container is created. You can use the [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)
command to view the status of the PVC:

```
kubectl get pvc azure-blob-storage
```


The output of the command resembles the following example:

```
NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE
azure-blob-storage Bound pvc-b88e36c5-c518-4d38-a5ee-337a7dda0a68 5Gi RWX azureblob-nfs-premium 92m
```


## Mount the PVC

The following YAML creates a pod that uses the PVC **azure-blob-storage** to mount the Azure Blob storage at the `/mnt/blob`

path.

Create a file named

`blob-nfs-pv`

, and copy the following YAML. Make sure that the**claimName**matches the PVC created in the previous step.`kind: Pod apiVersion: v1 metadata: name: mypod spec: containers: - name: mypod image: mcr.microsoft.com/oss/nginx/nginx:1.17.3-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: "/mnt/blob" name: volume readOnly: false volumes: - name: volume persistentVolumeClaim: claimName: azure-blob-storage`

Create the pod with the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f blob-nfs-pv.yaml`

After the pod is in the running state, run the following command to create a new file called

`test.txt`

.`kubectl exec mypod -- touch /mnt/blob/test.txt`

To validate the disk is correctly mounted, run the following command, and verify you see the

`test.txt`

file in the output:`kubectl exec mypod -- ls /mnt/blob`

The output of the command resembles the following example:

`test.txt`


## Create an Azure Blob custom storage class

The default storage classes suit the most common scenarios, but not all. In some cases, you might want to have your own storage class customized with your own parameters. In this section, we provide two examples with the first one using the NFS protocol, and the second one using BlobFuse.

In this example, the following manifest configures mounting a Blob storage container using the NFS
protocol. Use it to add the `tags`

parameter.

Create a file named

`blob-nfs-sc.yaml`

, and paste the following example manifest:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: azureblob-nfs-premium provisioner: blob.csi.azure.com parameters: protocol: nfs tags: environment=Development volumeBindingMode: Immediate allowVolumeExpansion: true mountOptions: - nconnect=4`

Create the storage class with the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f blob-nfs-sc.yaml`

The output of the command resembles the following example:

`storageclass.storage.k8s.io/blob-nfs-premium created`


## Mount an NFS or BlobFuse PV

In this section, you mount the PV using the NFS protocol or BlobFuse.

Mounting Blob storage using the NFS v3 protocol doesn't authenticate using an account key. Your AKS
cluster needs to reside in the same or peered virtual network as the agent node. The only way to
secure the data in your storage account is by using a virtual network and other network security
settings. For more information on how to set up NFS access to your storage account, see
[Mount Blob Storage by using the Network File System (NFS) 3.0 protocol](/en-us/azure/storage/blobs/network-file-system-protocol-support-how-to).

The following example demonstrates how to mount a Blob storage container as a persistent volume using the NFS protocol.

Create a file named

`pv-blob-nfs.yaml`

and copy in the following YAML. Under`storageClass`

, update`resourceGroup`

,`storageAccount`

, and`containerName`

.Note

The

`volumeHandle`

value within your YAML should be a unique volumeID for every identical storage blob container in the cluster.The characters

`#`

and`/`

are reserved for internal use and can't be used.`apiVersion: v1 kind: PersistentVolume metadata: annotations: pv.kubernetes.io/provisioned-by: blob.csi.azure.com name: pv-blob spec: capacity: storage: 1Pi accessModes: - ReadWriteMany persistentVolumeReclaimPolicy: Retain # If set as "Delete" container would be removed after pvc deletion storageClassName: azureblob-nfs-premium mountOptions: - nconnect=4 csi: driver: blob.csi.azure.com # make sure volumeid is unique for every identical storage blob container in the cluster # character `#` and `/` are reserved for internal use and cannot be used in volumehandle volumeHandle: account-name_container-name volumeAttributes: resourceGroup: resourceGroupName storageAccount: storageAccountName containerName: containerName protocol: nfs`

Note

While the

[Kubernetes API](https://github.com/kubernetes/kubernetes/blob/release-1.26/pkg/apis/core/types.go#L303-L306)**capacity**attribute is mandatory, this value isn't used by the Azure Blob storage CSI driver because you can flexibly write data until you reach your storage account's capacity limit. The value of the`capacity`

attribute is used only for size matching between*PVs*and*PVCs*. We recommend using a fictitious high value. The pod sees a mounted volume with a fictitious size of 5 Petabytes.Run the following command to create the persistent volume using the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command referencing the YAML file created earlier:`kubectl create -f pv-blob-nfs.yaml`

Create a

`pvc-blob-nfs.yaml`

file with a*PersistentVolumeClaim*. For example:`kind: PersistentVolumeClaim apiVersion: v1 metadata: name: pvc-blob spec: accessModes: - ReadWriteMany resources: requests: storage: 10Gi volumeName: pv-blob storageClassName: azureblob-nfs-premium`

Run the following command to create the persistent volume claim using the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command referencing the YAML file created earlier:`kubectl create -f pvc-blob-nfs.yaml`


## Create a pod

The following YAML creates a pod that uses the PV or PVC named **pvc-blob** created earlier, to mount the Azure Blob storage at the `/mnt/blob`

path.

Create a file named

`nginx-pod-blob.yaml`

, and copy in the following YAML. Make sure that the**claimName**matches the PVC created in the previous step when creating a PV for NFS or BlobFuse.`kind: Pod apiVersion: v1 metadata: name: nginx-blob spec: nodeSelector: "kubernetes.io/os": linux containers: - image: mcr.microsoft.com/oss/nginx/nginx:1.17.3-alpine name: nginx-blob volumeMounts: - name: blob01 mountPath: "/mnt/blob" readOnly: false volumes: - name: blob01 persistentVolumeClaim: claimName: pvc-blob`

Run the following command to create the pod and mount the PVC using the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command:`kubectl create -f nginx-pod-blob.yaml`

Run the following command to create an interactive shell session with the pod to verify if the Blob storage is mounted:

`kubectl exec -it nginx-blob -- df -h`

The output from the command resembles the following example:

`Filesystem Size Used Avail Use% Mounted on ... blobfuse 14G 41M 13G 1% /mnt/blob ...`


## Create a StatefulSet

To ensure your workload retains its storage volume across pod restarts or replacements, use a StatefulSet. StatefulSets simplify the process of associating persistent storage with pods, so that new pods created to replace failed ones can automatically access the same storage volumes. The following examples demonstrate how to set up a StatefulSet for Blob storage using either BlobFuse or the NFS protocol.

Create a file named

`azure-blob-nfs-ss.yaml`

and copy in the following YAML.`apiVersion: apps/v1 kind: StatefulSet metadata: name: statefulset-blob-nfs labels: app: nginx spec: serviceName: statefulset-blob-nfs replicas: 1 template: metadata: labels: app: nginx spec: nodeSelector: "kubernetes.io/os": linux containers: - name: statefulset-blob-nfs image: mcr.microsoft.com/azurelinux/base/nginx:1.25 volumeMounts: - name: persistent-storage mountPath: /mnt/blob updateStrategy: type: RollingUpdate selector: matchLabels: app: nginx volumeClaimTemplates: - metadata: name: persistent-storage spec: storageClassName: azureblob-nfs-premium accessModes: ["ReadWriteMany"] resources: requests: storage: 100Gi`

Create the StatefulSet with the

`kubectl create`

command:`kubectl create -f azure-blob-nfs-ss.yaml`


### Dynamic PVC storage class parameters

The following table includes parameters you can use to define a custom storage class for your dynamic PVC.

| Name | Description | Example | Mandatory | Default value |
|---|---|---|---|---|
| skuName | Specify an Azure storage account type (alias: `storageAccountType` ). |
`Standard_LRS` , `Premium_LRS` , `Standard_GRS` , `Standard_RAGRS` |
No | `Standard_LRS` |
| location | Specify an Azure location. | `eastus` |
No | If empty, the driver uses the same location name as current cluster. |
| resourceGroup | Specify an Azure resource group name. | myResourceGroup | No | If empty, the driver uses the same resource group name as current cluster. |
| storageAccount | Specify an Azure storage account name. | storageAccountName | No | When a specific storage account name isn't provided, the driver looks for a suitable storage account that matches the account settings within the same resource group. If it fails to find a matching storage account, it creates a new one. However, if a storage account name is specified, the storage account must already exist. |
networkEndpointType 1 |
Specify network endpoint type for the storage account created by driver. If privateEndpoint is specified, a
|

`privateEndpoint`

`fuse`

, `nfs`

`fuse`

`pvc-fuse`

for BlobFuse or `pvc-nfs`

for NFS v3.`<storage-account>.blob.core.windows.net`

.`<storage-account>.blob.core.windows.net`

or other sovereign cloud storage account DNS domain name.`true`

,`false`

`false`

`core.windows.net`

`true`

,`false`

`false`

1 If the storage account is created by the driver, then you only need to specify `networkEndpointType: privateEndpoint`

parameter in storage class. The CSI driver creates the private endpoint and private DNS zone (named `privatelink.blob.core.windows.net`

) together with the account. If you bring your own storage account, then you need to [create the private endpoint](/en-us/azure/storage/common/storage-private-endpoints) for the storage account. If you're using Azure Blob storage in a network isolated cluster, you must create a custom storage class with `networkEndpointType: privateEndpoint`

.

### Static PV provisioning parameters

The following table includes parameters you can use to define your static PV.

| Name | Description | Example | Mandatory | Default value |
|---|---|---|---|---|
| volumeHandle | Specify a value the driver can use to uniquely identify the storage blob container in the cluster. | A recommended way to produce a unique value is to combine the globally unique storage account name and container name: `{account-name}_{container-name}` . The `#` and `/` characters are reserved for internal use and can't be used in a volume handle. |
Yes | |
| volumeAttributes.resourceGroup | Specify Azure resource group name. | myResourceGroup | No | If empty, driver uses the same resource group name as current cluster. |
| volumeAttributes.storageAccount | Specify an existing Azure storage account name. | storageAccountName | Yes | |
| volumeAttributes.containerName | Specify existing container name. | container | Yes | |
| volumeAttributes.protocol | Specify BlobFuse mount or NFS v3 mount. | `fuse` , `nfs` |
No | `fuse` |

## Create Azure Disk PVs using built-in storage classes

A storage class is used to define how a unit of storage is dynamically created with a PV. For more information on Kubernetes storage classes, see [Kubernetes storage classes](https://kubernetes.io/docs/concepts/storage/storage-classes/).

When you use the Azure Disk CSI driver on AKS, there are two more built-in `StorageClasses`

that use the Azure Disk CSI storage driver. The other CSI storage classes are created with the cluster alongside the in-tree default storage classes.

`managed-csi`

: Creates managed disks using Azure Standard SSD with locally redundant storage (LRS). With Kubernetes version 1.29 for AKS clusters deployed across multiple availability zones, this storage class uses Azure Standard SSD zone-redundant storage (ZRS) to provision managed disks.`managed-csi-premium`

: Provisions managed disks using Azure Premium LRS. Beginning with Kubernetes version 1.29, for AKS clusters spanning multiple availability zones, this storage class automatically uses Azure Premium ZRS to create managed disks.

Effective starting with Kubernetes version 1.29, when you deploy Azure Kubernetes Service (AKS) clusters across multiple availability zones, AKS now utilizes zone-redundant storage (ZRS) to create managed disks within built-in storage classes.

ZRS ensures synchronous replication of your Azure managed disks across multiple Azure availability zones in your chosen region. This redundancy strategy enhances the resilience of your applications and safeguards your data against datacenter failures.

However, it's important to note that zone-redundant storage (ZRS) comes at a higher cost compared to locally redundant storage (LRS). If cost optimization is a priority, you can create a new storage class with the LRS SKU name parameter and use it in your persistent volume claim.


Reducing the size of a PVC isn't supported due to the risk of data loss. You can edit an existing storage class using the `kubectl edit sc`

command, or you can create your own custom storage class. For example, if you want to use a disk of size 4 TiB, you must create a storage class that defines `cachingmode: None`

because [disk caching isn't supported for disks 4 TiB and larger][disk-host-cache-setting]. For more information about storage classes and creating your own storage class, see [Storage options for applications in AKS](concepts-storage#storage-classes).

The reclaim policy in both storage classes ensures that the underlying Azure Disks are deleted when the respective PV is deleted. The storage classes also configure the PVs to be expandable. You just need to edit the PVC with the new size.

To use these storage classes, create a [PVC](concepts-storage#persistent-volume-claims) and respective pod that references and uses them. A PVC is used to automatically provision storage based on a storage class. A PVC can use one of the precreated storage classes or a user-defined storage class to create an Azure-managed disk for the desired SKU and size. When you create a pod definition, the PVC is specified to request the desired storage.

Note

Persistent volume claims are specified in GiB but Azure managed disks are billed based on the SKU for a specific size. These SKUs range from 32GiB for S4 or P4 disks to 32TiB for S80 or P80 disks (in preview). The throughput and IOPS performance of a Premium managed disk depends on both the SKU and the instance size of the nodes in the AKS cluster. For more information, see [Pricing and performance of managed disks](https://azure.microsoft.com/pricing/details/managed-disks/).

You can see the precreated storage classes using the [ kubectl get sc](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. The following example shows the precreated storage classes available within an AKS cluster:

```
kubectl get sc
```


The output of the command resembles the following example:

```
NAME PROVISIONER AGE
default (default) disk.csi.azure.com 1h
managed-csi disk.csi.azure.com 1h
```


A PVC automatically provisions storage based on a storage class. In this case, a PVC can use one of the precreated storage classes to create a standard or premium Azure managed disk.

Create a file named

`azure-pvc.yaml`

and copy in the following manifest. The claim requests a disk named`azure-managed-disk`

that's`5 GB`

in size with`ReadWriteOnce`

access. The*managed-csi*storage class is specified as the storage class.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: azure-managed-disk spec: accessModes: - ReadWriteOnce storageClassName: managed-csi resources: requests: storage: 5Gi`

Tip

To create a disk that uses premium storage, use

`storageClassName: managed-csi-premium`

rather than*managed-csi*.Create the persistent volume claim using the

command and specify your`kubectl apply`

*azure-pvc.yaml*file.`kubectl apply -f azure-pvc.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/azure-managed-disk created`


## Apply a PVC to a pod

After you create the persistent volume claim, you must verify it has a status of `Pending`

. The `Pending`

status indicates it's ready to be used by a pod.

Verify the status of the PVC using the

`kubectl describe pvc`

command.`kubectl describe pvc azure-managed-disk`

The output of the command resembles the following condensed example:

`Name: azure-managed-disk Namespace: default StorageClass: managed-csi Status: Pending [...]`

Create a file named

`azure-pvc-disk.yaml`

and copy in the following manifest. This manifest creates a basic NGINX pod that uses the persistent volume claim named`azure-managed-disk`

to mount the Azure Disk at the path`/mnt/azure`

. For Windows Server containers, specify a`mountPath`

using the Windows path convention, such as*'D:'*.`kind: Pod apiVersion: v1 metadata: name: mypod spec: containers: - name: mypod image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: "/mnt/azure" name: volume readOnly: false volumes: - name: volume persistentVolumeClaim: claimName: azure-managed-disk`

Create the pod using the

command.`kubectl apply`

`kubectl apply -f azure-pvc-disk.yaml`

The output of the command resembles the following example:

`pod/mypod created`

You now have a running pod with your Azure Disk mounted in the

`/mnt/azure`

directory. Check the pod configuration using thecommand.`kubectl describe`

`kubectl describe pod mypod`

The output of the command resembles the following example:

`[...] Volumes: volume: Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace) ClaimName: azure-managed-disk ReadOnly: false default-token-smm2n: Type: Secret (a volume populated by a Secret) SecretName: default-token-smm2n Optional: false [...] Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal Scheduled 2m default-scheduler Successfully assigned mypod to aks-nodepool1-79590246-0 Normal SuccessfulMountVolume 2m kubelet, aks-nodepool1-79590246-0 MountVolume.SetUp succeeded for volume "default-token-smm2n" Normal SuccessfulMountVolume 1m kubelet, aks-nodepool1-79590246-0 MountVolume.SetUp succeeded for volume "pvc-faf0f176-8b8d-11e8-923b-deb28c58d242" [...]`


## Dynamic storage class parameters for PVCs

The following table includes parameters you can use to define a custom storage class for your PVCs.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| skuName | Azure Disks storage account type (alias: `storageAccountType` ) |
`Standard_LRS` , `Premium_LRS` , `StandardSSD_LRS` , `PremiumV2_LRS` , `UltraSSD_LRS` , `Premium_ZRS` , `StandardSSD_ZRS` |
No | `StandardSSD_LRS` |
| fsType | File System Type | `ext4` , `ext3` , `ext2` , `xfs` , `btrfs` for Linux, `ntfs` for Windows |
No | `ext4` for Linux, `ntfs` for Windows |
| cachingMode | [Azure Data Disk Host Cache Setting][disk-host-cache-setting](PremiumV2_LRS and UltraSSD_LRS only support `None` caching mode) |
`None` , `ReadOnly` , `ReadWrite` |
No | `ReadOnly` |
| resourceGroup | Specify the resource group for the Azure Disks | Existing resource group name | No | If empty, driver uses the same resource group name as current AKS cluster |
| DiskIOPSReadWrite | [UltraSSD disk][ultra-ssd-disks] or [Premium SSD v2][premiumv2_lrs_disks] IOPS Capability (minimum: 2 IOPS/GiB) | 100~160000 | No | `500` |
| DiskMBpsReadWrite | [UltraSSD disk][ultra-ssd-disks] or [Premium SSD v2][premiumv2_lrs_disks] Throughput Capability(minimum: 0.032/GiB) | 1~2000 | No | `100` |
| LogicalSectorSize | Logical sector size in bytes for ultra disk. Supported values are 512 ad 4096. 4096 is the default. | `512` , `4096` |
No | `4096` |
| tags | Azure Disk [tags][azure-tags] | Tag format: `key1=val1,key2=val2` |
No | "" |
| diskEncryptionSetID | ResourceId of the disk encryption set to use for [enabling encryption at rest][disk-encryption] | format: `/subscriptions/{subs-id}/resourceGroups/{rg-name}/providers/Microsoft.Compute/diskEncryptionSets/{diskEncryptionSet-name}` |
No | "" |
| diskEncryptionType | Encryption type of the disk encryption set. | `EncryptionAtRestWithCustomerKey` (by default), `EncryptionAtRestWithPlatformAndCustomerKeys` |
No | "" |
| writeAcceleratorEnabled | [Write Accelerator on Azure Disks][azure-disk-write-accelerator] | `true` , `false` |
No | "" |
| networkAccessPolicy | NetworkAccessPolicy property to prevent generation of the SAS URI for a disk or a snapshot | `AllowAll` , `DenyAll` , `AllowPrivate` |
No | `AllowAll` |
| diskAccessID | Azure Resource ID of the DiskAccess resource to use private endpoints on disks | No | `` | |
| enableBursting | [Enable on-demand bursting][on-demand-bursting] beyond the provisioned performance target of the disk. On-demand bursting should only be applied to Premium disk and when the disk size > 512 GB. Ultra and shared disk isn't supported. Bursting is disabled by default. | `true` , `false` |
No | `false` |
| userAgent | The user agent is used for [customer usage attribution][customer-usage-attribution] | No | The generated user agent is formatted as `driverName/driverVersion compiler/version (OS-ARCH)` |
|
| subscriptionID | Specify Azure subscription ID where the Azure Disks is created. | Azure subscription ID | No | If not empty, `resourceGroup` must be provided. |

## Static provisioning parameters for a PV

The following table includes parameters you can use to define a PV.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| volumeHandle | Azure disk URI | `/subscriptions/{sub-id}/resourcegroups/{group-name}/providers/microsoft.compute/disks/{disk-id}` |
Yes | N/A |
| volumeAttributes.fsType | File system type | `ext4` , `ext3` , `ext2` , `xfs` , `btrfs` for Linux, `ntfs` for Windows |
No | `ext4` for Linux, `ntfs` for Windows |
| volumeAttributes.partition | Partition number of the existing disk (only supported on Linux) | `1` , `2` , `3` |
No | Empty (no partition) - Make sure partition format is like `-part1` |
| volumeAttributes.cachingMode | [Disk host cache setting][disk-host-cache-setting] | `None` , `ReadOnly` , `ReadWrite` |
No | `ReadOnly` |

## Create an Azure Disk custom storage class

The default storage classes are suitable for most common scenarios. For some cases, you might want
to have your own storage class customized with your own parameters. For example, you might want to
change the `volumeBindingMode`

class.

You can use a `volumeBindingMode: Immediate`

class that guarantees it occurs immediately once the
persistent volume claim (PVC) is created. When your node pools are topology constrained, for example
when using availability zones, PVs would be bound or provisioned without knowledge of the pod's
scheduling requirements.

To address this scenario, you can use `volumeBindingMode: WaitForFirstConsumer`

, which delays the binding and provisioning of a PV until a pod that uses the PVC is created. This approach ensures that the persistent volume (PV) is provisioned in the same availability zone or topology as required per the pod's scheduling constraints. The default storage classes use `volumeBindingMode: WaitForFirstConsumer`

class.

Create a file named

`sc-azuredisk-csi-waitforfirstconsumer.yaml`

, and then paste the following manifest. The storage class is the same as our`managed-csi`

storage class, but with a different`volumeBindingMode`

class. For example:`kind: StorageClass apiVersion: storage.k8s.io/v1 metadata: name: azuredisk-csi-waitforfirstconsumer provisioner: disk.csi.azure.com parameters: skuname: StandardSSD_LRS allowVolumeExpansion: true reclaimPolicy: Delete volumeBindingMode: WaitForFirstConsumer`

Create the storage class by running the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify your`sc-azuredisk-csi-waitforfirstconsumer.yaml`

file:`kubectl apply -f sc-azuredisk-csi-waitforfirstconsumer.yaml`

The output of the command resembles the following example:

`storageclass.storage.k8s.io/azuredisk-csi-waitforfirstconsumer created`


## Learn about volume snapshots

The Azure Disk CSI driver supports [volume snapshots](https://kubernetes-csi.github.io/docs/snapshot-restore-feature.html), enabling you to capture the state of persistent volumes at specific points in time for backup and restore operations. Volume snapshots let you create point-in-time copies of your persistent data without interrupting running applications. You can use these snapshots to create new volumes or restore existing ones to a previous state.

You can create two types of snapshots:

**Full snapshots**: Capture the complete state of the disk.**Incremental snapshots**: Capture only the changes since the last snapshot, offering better storage efficiency and cost savings.[Incremental snapshots](/en-us/azure/virtual-machines/disks-incremental-snapshots)are the default behavior when the`incremental`

parameter is set to`true`

in your VolumeSnapshotClass.

The following table provides details for these parameters.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| resourceGroup | Resource group for storing snapshot shots | EXISTING RESOURCE GROUP | No | If not specified, snapshots are stored in the same resource group as source Azure Disks |
| incremental | Take
|

`true`

, `false`

`true`

[tags](/en-us/azure/azure-resource-manager/management/tag-resources)[customer usage attribution](/en-us/azure/marketplace/azure-partner-customer-usage-attribution)`driverName/driverVersion compiler/version (OS-ARCH)`

`resourceGroup`

must be provided, `incremental`

must set as `false`

Volume snapshots support the following scenarios:

**Backup and restore**: Create point-in-time backups of stateful application data and restore when needed.**Data cloning**: Clone existing volumes to create new persistent volumes with the same data.**Disaster recovery**: Quickly recover from data loss or corruption.

### Create a volume snapshot

Note

Before proceeding, ensure that the application isn't writing data to the source disk.

For an example of this capability, create a

[volume snapshot class](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/storageclass-azuredisk-snapshot.yaml)with the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/storageclass-azuredisk-snapshot.yaml`

The output of the command resembles the following example:

`volumesnapshotclass.snapshot.storage.k8s.io/csi-azuredisk-vsc created`

Create a

[volume snapshot](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/azuredisk-volume-snapshot.yaml)from the PVC that was created earlier in this article.`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/azuredisk-volume-snapshot.yaml`

The output of the command resembles the following example:

`volumesnapshot.snapshot.storage.k8s.io/azuredisk-volume-snapshot created`

To verify that the snapshot was created correctly, run the following command:

`kubectl describe volumesnapshot azuredisk-volume-snapshot`

The output of the command resembles the following example:

`Name: azuredisk-volume-snapshot Namespace: default Labels: <none> Annotations: API Version: snapshot.storage.k8s.io/v1 Kind: VolumeSnapshot Metadata: Creation Timestamp: 2020-08-27T05:27:58Z Finalizers: snapshot.storage.kubernetes.io/volumesnapshot-as-source-protection snapshot.storage.kubernetes.io/volumesnapshot-bound-protection Generation: 1 Resource Version: 714582 Self Link: /apis/snapshot.storage.k8s.io/v1/namespaces/default/volumesnapshots/azuredisk-volume-snapshot UID: dd953ab5-6c24-42d4-ad4a-f33180e0ef87 Spec: Source: Persistent Volume Claim Name: pvc-azuredisk Volume Snapshot Class Name: csi-azuredisk-vsc Status: Bound Volume Snapshot Content Name: snapcontent-dd953ab5-6c24-42d4-ad4a-f33180e0ef87 Creation Time: 2020-08-31T05:27:59Z Ready To Use: true Restore Size: 10Gi Events: <none>`


### Create a new PVC based on a volume snapshot

You can create a new PVC based on a volume snapshot.

Use the snapshot created in the previous step, and create a

[new PVC](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/pvc-azuredisk-snapshot-restored.yaml)and a[new pod](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/nginx-pod-restored-snapshot.yaml)to consume it:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/pvc-azuredisk-snapshot-restored.yaml kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/nginx-pod-restored-snapshot.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azuredisk-snapshot-restored created pod/nginx-restored created`

To make sure it's the same PVC created before, check the contents by running the following command:

`kubectl exec nginx-restored -- ls /mnt/azuredisk`

The output of the command resembles the following example:

`lost+found outfile test.txt`


We can still see our previously created `test.txt`

file as expected.

## Clone volumes

A cloned volume is defined as a duplicate of an existing Kubernetes volume. For more information on cloning volumes in Kubernetes, see [volume cloning](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#volume-cloning).

Create a

[cloned volume](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/cloning/nginx-pod-restored-cloning.yaml)of the[previously created](#create-azure-disk-pvs-using-built-in-storage-classes)`azuredisk-pvc`

and a[new pod](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/cloning/nginx-pod-restored-cloning.yaml)to consume it.`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/cloning/pvc-azuredisk-cloning.yaml kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/cloning/nginx-pod-restored-cloning.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azuredisk-cloning created pod/nginx-restored-cloning created`

You can verify the content of the cloned volume by running the following command and confirming the file

`test.txt`

is created:`kubectl exec nginx-restored-cloning -- ls /mnt/azuredisk`

The output of the command resembles the following example:

`lost+found outfile test.txt`


## Resize an Azure Disk PV without downtime

You can request a larger volume for a PVC. Edit the PVC object, and specify a larger size. This change triggers the expansion of the underlying volume that backs the PV.

Note

A new PV is never created to satisfy the claim. Instead, an existing volume is resized.

In AKS, the built-in `managed-csi`

storage class already supports expansion, so use the [previously created](#create-azure-disk-pvs-using-built-in-storage-classes) one. The PVC requested a 10-Gi persistent volume. You can confirm by running the following command:

```
kubectl exec -it nginx-azuredisk -- df -h /mnt/azuredisk
```


The output of the command resembles the following example:

```
Filesystem Size Used Avail Use% Mounted on
/dev/sdc 9.8G 42M 9.8G 1% /mnt/azuredisk
```


Expand the PVC by increasing the

`spec.resources.requests.storage`

field running the following command:`kubectl patch pvc pvc-azuredisk --type merge --patch '{"spec": {"resources": {"requests": {"storage": "15Gi"}}}}'`

Note

Shrinking PVs is currently not supported. Trying to patch an existing PVC with a smaller size than the current one leads to the following error message:

`The persistentVolumeClaim "pvc-azuredisk" is invalid: spec.resources.requests.storage: Forbidden: field can not be less than previous value.`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azuredisk patched`

Run the following command to confirm the volume size increased:

`kubectl get pv`

The output of the command resembles the following example:

`NAME CAPACITY ACCESS MODES RECLAIM POLICY STATUS CLAIM STORAGECLASS REASON AGE pvc-391ea1a6-0191-4022-b915-c8dc4216174a 15Gi RWO Delete Bound default/pvc-azuredisk managed-csi 2d2h (...)`

And after a few minutes, run the following commands to confirm the size of the PVC:

`kubectl get pvc pvc-azuredisk`

The output of the command resembles the following example:

`NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE pvc-azuredisk Bound pvc-391ea1a6-0191-4022-b915-c8dc4216174a 15Gi RWO managed-csi 2d2h`

Run the following command to confirm the size of the disk inside the pod:

`kubectl exec -it nginx-azuredisk -- df -h /mnt/azuredisk`

The output of the command resembles the following example:

`Filesystem Size Used Avail Use% Mounted on /dev/sdc 15G 46M 15G 1% /mnt/azuredisk`


If your pod has *multiple containers*, you can specify which container by running the following command:

```
kubectl exec -it nginx-azuredisk -c <ContainerName> -- df -h /mnt/azuredisk
```


## Windows containers

The Azure Disk CSI driver supports Windows nodes and containers. If you want to use Windows containers, follow the [Windows containers quickstart](learn/quick-kubernetes-deploy-cli) to add a Windows node pool.

After you have a Windows node pool, you can now use the built-in storage classes like

`managed-csi`

. You can deploy an example[Windows-based stateful set](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/windows/statefulset.yaml)that saves timestamps into the file`data.txt`

by running the following[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/windows/statefulset.yaml`

The output of the command resembles the following example:

`statefulset.apps/busybox-azuredisk created`

To validate the content of the volume, run the following command:

`kubectl exec -it statefulset-azuredisk-win-0 -- powershell -c "type c:/mnt/azuredisk/data.txt"`

The output of the command resembles the following example:

`2020-08-27 08:13:41Z 2020-08-27 08:13:42Z 2020-08-27 08:13:44Z (...)`


## On-demand bursting

On-demand disk bursting model allows disk bursts whenever its needs exceed its current capacity. This model generates extra charges anytime the disk bursts. On-demand bursting is only available for premium SSDs larger than 512 GiB. For more information on premium SSDs provisioned IOPS and throughput per disk, see [Premium SSD size](/en-us/azure/virtual-machines/disks-types#premium-ssds). Alternatively, credit-based bursting is where the disk will burst only if it has burst credits accumulated in its credit bucket. Credit-based bursting doesn't generate extra charges when the disk bursts. Credit-based bursting is only available for premium SSDs 512 GiB and smaller, and standard SSDs 1,024 GiB and smaller. For more information on on-demand bursting, see [On-demand bursting](/en-us/azure/virtual-machines/disk-bursting#on-demand-bursting).

Important

The default `managed-csi-premium`

storage class has on-demand bursting disabled and uses credit-based bursting. Any premium SSD dynamically created by a persistent volume claim based on the default `managed-csi-premium`

storage class also has on-demand bursting disabled.

To create a premium SSD persistent volume with [on-demand bursting](/en-us/azure/virtual-machines/disk-bursting#on-demand-bursting) enabled, you can create a new storage class with the [enableBursting](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/docs/driver-parameters.md) parameter set to `true`

as shown in the following YAML template. For more information on enabling on-demand bursting, see [On-demand bursting](/en-us/azure/virtual-machines/disk-bursting#on-demand-bursting). For more information on building your own storage class with on-demand bursting enabled, see [Create a Burstable Managed CSI Premium Storage Class](https://github.com/Azure-Samples/burstable-managed-csi-premium).

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: burstable-managed-csi-premium
provisioner: disk.csi.azure.com
parameters:
skuname: Premium_LRS
enableBursting: "true"
reclaimPolicy: Delete
volumeBindingMode: WaitForFirstConsumer
allowVolumeExpansion: true
```


## Clean up resources

When you're done with the resources created in this article, you can remove them using the
`kubectl delete`

command.

```
# Remove the pod
kubectl delete -f azure-pvc-disk.yaml
# Remove the persistent volume claim
kubectl delete -f azure-pvc.yaml
```


## Provision Azure Files PVs

Azure Files supports Azure Premium file shares. The minimum file share capacity is 100 GiB. We recommend using Azure Premium file shares instead of Standard file shares because Premium file shares offer higher performance, low-latency disk support for I/O-intensive workloads. With Azure Files shares, there's no limit as to how many can be mounted on a node. For more information on Kubernetes volumes, see [Storage options for applications in AKS](concepts-storage).

When you use storage CSI drivers on AKS, there are two more built-in `StorageClasses`

that uses the Azure Files CSI storage drivers. The other CSI storage classes are created with the cluster alongside the in-tree default storage classes.

`azurefile-csi`

: Uses Azure Standard Storage to create an Azure file share.`azurefile-csi-premium`

: Uses Azure Premium Storage to create an Azure file share.

The reclaim policy on both storage classes ensures that the underlying Azure files share is deleted when the respective PV is deleted. Since the storage classes also configure the file shares to be expandable, you just need to edit the [PVC](concepts-storage#persistent-volume-claims) with the new size.

Note

To have the best experience with Azure Files, follow these best practices. The location to configure mount options (`mountOptions`

) depends on whether you're provisioning dynamic or static persistent volumes.

- If you're dynamically provisioning a volume with a storage class, specify the mount options on the storage class object (kind:
`StorageClass`

). - If you're statically provisioning a volume, specify the mount options on the PersistentVolume object (kind:
`PersistentVolume`

). - If you're mounting the file share as an inline volume, specify the mount options on the Pod object (kind:
`Pod`

).

We recommend FIO when running benchmarking tests. For more information, see [benchmarking tools and tests](/en-us/azure/storage/files/nfs-performance#benchmarking-tools-and-tests).

A storage class is used to define how an Azure file share is created. A storage account is automatically created in the [node resource group](faq) for use with the storage class to hold the Azure files share. Choose one of the following [Azure storage redundancy SKUs](/en-us/azure/storage/common/storage-redundancy) for *skuName*:

**Standard_LRS**: Standard locally redundant storage**Standard_GRS**: Standard geo-redundant storage**Standard_ZRS**: Standard zone-redundant storage**Standard_RAGRS**: Standard read-access geo-redundant storage**Standard_RAGZRS**: Standard read-access geo-zone-redundant storage**Premium_LRS**: Premium locally redundant storage**Premium_ZRS**: Premium zone-redundant storage

For more information on Kubernetes storage classes for Azure Files, see [Kubernetes Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/#azure-file).

Create a file named

`azure-file-sc.yaml`

and copy in the following example manifest. For more information on`mountOptions`

, see the[Mount options](#mount-options)section.`kind: StorageClass apiVersion: storage.k8s.io/v1 metadata: name: my-azurefile provisioner: file.csi.azure.com # replace with "kubernetes.io/azure-file" if aks version is less than 1.21 allowVolumeExpansion: true mountOptions: - dir_mode=0777 - file_mode=0777 - uid=0 - gid=0 - mfsymlinks - cache=strict - actimeo=30 - nobrl # disable sending byte range lock requests to the server and for applications which have challenges with posix locks parameters: skuName: Premium_LRS`

Create the storage class using the

command.`kubectl apply`

`kubectl apply -f azure-file-sc.yaml`


### Create a PVC

A PVC uses the storage class object to dynamically provision an Azure file share. You can use the following YAML to create a PVC that's *100 GB* in size with *ReadWriteMany* access. For more information on access modes, see [Kubernetes persistent volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes).

Create a file named

`azure-file-pvc.yaml`

and copy in the following YAML. Make sure the`storageClassName`

matches the storage class you created in the previous step.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: my-azurefile spec: accessModes: - ReadWriteMany storageClassName: my-azurefile resources: requests: storage: 100Gi`

Note

If using the

`Premium_LRS`

SKU for your storage class, the minimum value for`storage`

must be`100Gi`

.Create the PVC using the

command.`kubectl apply`

`kubectl apply -f azure-file-pvc.yaml`

Once completed, the file share is created. A Kubernetes secret is also created that includes connection information and credentials. You can use the

command to view the status of the PVC:`kubectl get`

`kubectl get pvc my-azurefile`

The output of the command resembles the following example:

`NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE my-azurefile Bound pvc-8436e62e-a0d9-11e5-8521-5a8664dc0477 100Gi RWX my-azurefile 5m`


### Mount the PVC

The following YAML creates a pod that uses the PVC *my-azurefile* to mount the Azure Files file share at the */mnt/azure* path. For Windows Server containers, specify a `mountPath`

using the Windows path convention, such as *"D:"*.

Create a file named

`azure-pvc-files.yaml`

, and copy in the following YAML. Make sure the`claimName`

matches the PVC you created in the previous step.`kind: Pod apiVersion: v1 metadata: name: mypod spec: containers: - name: mypod image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: /mnt/azure name: volume readOnly: false volumes: - name: volume persistentVolumeClaim: claimName: my-azurefile`

Create the pod using the

command.`kubectl apply`

`kubectl apply -f azure-pvc-files.yaml`

You now have a running pod with your Azure Files file share mounted in the

*/mnt/azure*directory. This configuration can be seen when inspecting your pod using thecommand. The following condensed example output shows the volume mounted in the container.`kubectl describe`

`Containers: mypod: Container ID: docker://053bc9c0df72232d755aa040bfba8b533fa696b123876108dec400e364d2523e Image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine Image ID: docker-pullable://nginx@sha256:d85914d547a6c92faa39ce7058bd7529baacab7e0cd4255442b04577c4d1f424 State: Running Started: Fri, 01 Mar 2019 23:56:16 +0000 Ready: True Mounts: /mnt/azure from volume (rw) /var/run/secrets/kubernetes.io/serviceaccount from default-token-8rv4z (ro) [...] Volumes: volume: Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace) ClaimName: my-azurefile ReadOnly: false [...]`


### Mount options

For Kubernetes versions 1.13.0 and later, the default values for `fileMode`

and `dirMode`

are `0777`

. When dynamically provisioning PVs using a storage class, you can define mount options directly in the storage class manifest. For details, see [Mount options](https://kubernetes.io/docs/concepts/storage/storage-classes/#mount-options). The following example demonstrates setting these permissions to `0777`

:

```
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
name: my-azurefile
provisioner: file.csi.azure.com # replace with "kubernetes.io/azure-file" if aks version is less than 1.21
allowVolumeExpansion: true
mountOptions:
- dir_mode=0777
- file_mode=0777
- uid=0
- gid=0
- mfsymlinks
- cache=strict
- actimeo=30
- nobrl # disable sending byte range lock requests to the server and for applications which have challenges with posix locks
parameters:
skuName: Premium_LRS
```


## Storage class parameters for dynamic volumes

The following table includes parameters you can use to define a custom storage class for your PVC.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| accountAccessTier |
|

`Hot`

or `Cool`

, and Premium account can only choose `Premium`

.`102400`

`true`

or `false`

`false`

`true`

or `false`

`false`

`true`

or `false`

`false`

`eastus`

.`true`

or `false`

`false`

1`privateEndpoint`

is specified, a private endpoint is created for the storage account. For other cases, a service endpoint is created by default.`privateEndpoint`

`smb`

, `nfs`

`smb`

`true`

or `false`

`false`

`true`

or `false`

`false`

`accountname.privatelink.file.core.windows.net`

.`accountname.file.core.windows.net`

or other sovereign cloud account address.[Access tier for file share](/en-us/azure/storage/files/storage-files-planning#storage-tiers)`TransactionOptimized`

(default), `Hot`

, and `Cool`

. Premium storage account type for file shares only.`storageAccountType`

)`Standard_LRS`

, `Standard_ZRS`

, `Standard_GRS`

, `Standard_RAGRS`

, `Standard_RAGZRS`

,`Premium_LRS`

, `Premium_ZRS`

, `StandardV2_LRS`

, `StandardV2_ZRS`

, `StandardV2_GRS`

, `StandardV2_GZRS`

, `PremiumV2_LRS`

, `PremiumV2_ZRS`

`Standard_LRS`

Minimum file share size for Premium account type is 100 GB.

ZRS account type is supported in limited regions.

NFS file share only supports Premium account type.

Standard V2 SKU names are for

[Azure Files provisioned v2 model](/en-us/azure/storage/files/understanding-billing#provisioned-v2-model).`core.windows.net`

, `core.chinacloudapi.cn`

, etc.`core.windows.net`

.[Tags](/en-us/azure/azure-resource-manager/management/tag-resources)are created in new storage account.1 If the storage account is created by the driver, then you only need to specify
`networkEndpointType: privateEndpoint`

parameter in storage class. The CSI driver creates the
private endpoint and private DNS zone (named `privatelink.file.core.windows.net`

) together with the
account. If you bring your own storage account, then you need to
[create the private endpoint](/en-us/azure/storage/common/storage-private-endpoints) for the storage account. If you're
using Azure Files storage in a network isolated cluster, you must create a custom storage class with
"networkEndpointType: privateEndpoint". You can follow this sample for reference:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: azurefile-csi
provisioner: file.csi.azure.com
allowVolumeExpansion: true
parameters:
skuName: Premium_LRS # available values: Premium_LRS, Premium_ZRS, Standard_LRS, Standard_GRS, Standard_ZRS, Standard_RAGRS, Standard_RAGZRS
networkEndpointType: privateEndpoint
reclaimPolicy: Delete
volumeBindingMode: Immediate
mountOptions:
- dir_mode=0777 # modify this permission if you want to enhance the security
- file_mode=0777
- mfsymlinks
- cache=strict # https://linux.die.net/man/8/mount.cifs
- nosharesock # reduce probability of reconnect race
- actimeo=30 # reduce latency for metadata-heavy workload
- nobrl # disable sending byte range lock requests to the server and for applications which have challenges with posix locks
```


## Static provisioning parameters for PVs

The following table includes parameters you can use to define a PV.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| volumeAttributes.resourceGroup | Specify an Azure resource group name. | myResourceGroup | No | If empty, driver uses the same resource group name as current cluster. |
| volumeAttributes.storageAccount | Specify an existing Azure storage account name. | storageAccountName | Yes | |
| volumeAttributes.shareName | Specify an Azure file share name. | fileShareName | Yes | |
| volumeAttributes.folderName | Specify a folder name in Azure file share. | folderName | No | If folder name doesn't exist in file share, mount would fail. |
| volumeAttributes.protocol | Specify file share protocol. | `smb` , `nfs` |
No | `smb` |
| volumeAttributes.server | Specify Azure storage account server address | Existing server address, for example `accountname.privatelink.file.core.windows.net` . |
No | If empty, driver uses default `accountname.file.core.windows.net` or other sovereign cloud account address. |

## Create a PV snapshot class

The Azure Files CSI driver supports creating [snapshots of persistent volumes](https://kubernetes-csi.github.io/docs/snapshot-restore-feature.html) and the underlying file shares.

Create a

[volume snapshot class](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/deploy/example/snapshot/volumesnapshotclass-azurefile.yaml)with the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azurefile-csi-driver/master/deploy/example/snapshot/volumesnapshotclass-azurefile.yaml`

The output of the command resembles the following example:

`volumesnapshotclass.snapshot.storage.k8s.io/csi-azurefile-vsc created`

Create a

[volume snapshot](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/deploy/example/snapshot/volumesnapshot-azurefile.yaml)from the PVC created earlier (`pvc-azurefile`

).`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azurefile-csi-driver/master/deploy/example/snapshot/volumesnapshot-azurefile.yaml`

The output of the command resembles the following example:

`volumesnapshot.snapshot.storage.k8s.io/azurefile-volume-snapshot created`

Verify the snapshot was created correctly by running the following command:

`kubectl describe volumesnapshot azurefile-volume-snapshot`

The output of the command resembles the following example:

`Name: azurefile-volume-snapshot Namespace: default Labels: <none> Annotations: API Version: snapshot.storage.k8s.io/v1beta1 Kind: VolumeSnapshot Metadata: Creation Timestamp: 2020-08-27T22:37:41Z Finalizers: snapshot.storage.kubernetes.io/volumesnapshot-as-source-protection snapshot.storage.kubernetes.io/volumesnapshot-bound-protection Generation: 1 Resource Version: 955091 Self Link: /apis/snapshot.storage.k8s.io/v1beta1/namespaces/default/volumesnapshots/azurefile-volume-snapshot UID: c359a38f-35c1-4fb1-9da9-2c06d35ca0f4 Spec: Source: Persistent Volume Claim Name: pvc-azurefile Volume Snapshot Class Name: csi-azurefile-vsc Status: Bound Volume Snapshot Content Name: snapcontent-c359a38f-35c1-4fb1-9da9-2c06d35ca0f4 Ready To Use: false Events: <none>`


## Resize an Azure Files PV

You can request a larger volume for a PVC. Edit the PVC object, and specify a larger size. This change triggers the expansion of the underlying volume that backs the PV.

Note

A new PV is never created to satisfy the claim. Instead, an existing volume is resized. Shrinking persistent volumes is currently not supported.

In AKS, the built-in `azurefile-csi`

storage class already supports expansion, so use the PVC we created earlier with this storage class. The PVC requested a 100 GiB file share. We can confirm that by running:

```
kubectl exec -it nginx-azurefile -- df -h /mnt/azurefile
```


The output of the command resembles the following example:

```
Filesystem Size Used Avail Use% Mounted on
//f149b5a219bd34caeb07de9.file.core.windows.net/pvc-5e5d9980-da38-492b-8581-17e3cad01770 100G 128K 100G 1% /mnt/azurefile
```


Expand the PVC by increasing the

`spec.resources.requests.storage`

field:`kubectl patch pvc pvc-azurefile --type merge --patch '{"spec": {"resources": {"requests": {"storage": "200Gi"}}}}'`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azurefile patched`

Verify that both the PVC and the file system inside the pod show the new size:

`kubectl get pvc pvc-azurefile NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE pvc-azurefile Bound pvc-5e5d9980-da38-492b-8581-17e3cad01770 200Gi RWX azurefile-csi 64m kubectl exec -it nginx-azurefile -- df -h /mnt/azurefile Filesystem Size Used Avail Use% Mounted on //f149b5a219bd34caeb07de9.file.core.windows.net/pvc-5e5d9980-da38-492b-8581-17e3cad01770 200G 128K 200G 1% /mnt/azurefile`


## Use a PV with private Azure Files storage (private endpoint)

If your Azure Files resources are protected with a private endpoint, you must create your own storage class. Make sure to configure your [DNS settings to resolve the private endpoint IP address to the FQDN of the connection string](/en-us/azure/private-link/private-endpoint-dns#azure-services-dns-zone-configuration).

Customize the following parameters:

`resourceGroup`

: The resource group where the storage account is deployed.`storageAccount`

: The storage account name.`server`

: The FQDN of the storage account's private endpoint.

Create a file named

`private-azure-file-sc.yaml`

, and then paste the following example manifest in the file. Replace the values for`<resourceGroup>`

and`<storageAccountName>`

. For example:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: private-azurefile-csi provisioner: file.csi.azure.com allowVolumeExpansion: true parameters: resourceGroup: <resourceGroup> storageAccount: <storageAccountName> server: <storageAccountName>.file.core.windows.net reclaimPolicy: Delete volumeBindingMode: Immediate mountOptions: - dir_mode=0777 - file_mode=0777 - uid=0 - gid=0 - mfsymlinks - cache=strict # https://linux.die.net/man/8/mount.cifs - nosharesock # reduce probability of reconnect race - actimeo=30 # reduce latency for metadata-heavy workload`

Create the storage class by using the

`kubectl apply`

command:`kubectl apply -f private-azure-file-sc.yaml`

The output of the command resembles the following example:

`storageclass.storage.k8s.io/private-azurefile-csi created`

Create a file named

`private-pvc.yaml`

, and then paste the following example manifest in the file:`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: private-azurefile-pvc spec: accessModes: - ReadWriteMany storageClassName: private-azurefile-csi resources: requests: storage: 100Gi`

Create the PVC by using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f private-pvc.yaml`


## Use Managed Identity to access Azure Files storage (Preview)

Azure Files now supports managed identity-based authentication for SMB access. With this capability, your applications running in AKS can securely access Azure Files shares without the need to store or manage storage account keys or credentials. Managed identities provide a streamlined and secure authentication mechanism, simplifying access management and reducing the risk associated with credential exposure. You can create a dynamic volume or a static volume.

Note

Managed identity support for Azure Files in AKS is available in preview starting with AKS version 1.34 on Linux nodes.

To enable managed identity for dynamically provisioned volumes, follow these steps:

Create a storage class with managed identity enabled using a YAML file, for example,

`azurefile-csi-managed-identity.yaml`

with the following sample content. Set`mountWithManagedIdentity: "true"`

under`parameters`

:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: azurefile-csi provisioner: file.csi.azure.com parameters: resourceGroup: EXISTING_RESOURCE_GROUP_NAME # optional, node resource group by default if it's not provided storageAccount: EXISTING_STORAGE_ACCOUNT_NAME # optional, a new account will be created if it's not provided mountWithManagedIdentity: "true" # optional, clientID of the managed identity, kubelet identity would be used by default if it's not provided clientID: "xxxxx-xxxx-xxx-xxx-xxxxxxx" reclaimPolicy: Delete volumeBindingMode: Immediate allowVolumeExpansion: true mountOptions: - dir_mode=0777 # modify this permission if you want to enhance the security - file_mode=0777 - uid=0 - gid=0 - mfsymlinks - cache=strict # https://linux.die.net/man/8/mount.cifs - nosharesock # reduce probability of reconnect race - actimeo=30 # reduce latency for metadata-heavy workload - nobrl # disable sending byte range lock requests to the server`

Apply this storage class by running the following command:

`kubectl apply -f azurefile-csi-managed-identity.yaml`

Deploy your

**StatefulSet**or workload using the new storage class that references this PVC to ensure that the volume is provisioned using managed identity authentication. In your PVC manifest, set`storageClassName: azurefile-csi-managed-identity`

. For example:`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: azurefile-managed-identity-pvc spec: accessModes: - ReadWriteMany storageClassName: azurefile-csi-managed-identity resources: requests: storage: 100Gi`


## Learn about Azure Files NFS

Azure Files supports the
[NFS v4.1 protocol](/en-us/azure/storage/files/storage-files-how-to-create-nfs-shares). NFS version 4.1
support for Azure Files provides you with a fully managed NFS system as a service built on highly
available, highly durable distributed resilient storage platform.

This option is optimized for random access workloads with in-place data updates and provides full POSIX file system support. This section shows you how to use NFS shares with the Azure File CSI driver on an AKS cluster.

Note

You can use a private endpoint instead of allowing access to the selected VNet.

This section explains how to maximize performance and security when using Azure Files NFS 4.1 with AKS. Learn how to:

Optimize NFS read and write size settings

Create and configure an NFS storage class

Deploy workloads that use NFS-backed volumes

Enable Encryption in Transit (EiT) to protect data as it moves between your AKS cluster and Azure Files.


This section provides information about how to approach performance tuning NFS with the Azure Files
CSI driver with the `rsize`

(read size) and `wsize`

(write size) options. The `rsize`

and `wsize`

options set the maximum transfer size of an NFS operation. If `rsize`

or `wsize`

aren't specified on
mount, the client and server negotiate the largest size supported by the two. Currently, both Azure
Files and modern Linux distributions support read and write sizes as large as 1,048,576 bytes (1
MiB).

Optimal performance is based on efficient client-server communication. Increasing or decreasing the
**mount** read and write option size values can improve NFS performance. The default size of the
read/write packets transferred between client and server are 8 KB for NFS version 2, and 32 KB for
NFS version 3 and 4. These defaults might be too large or too small. Reducing the `rsize`

and
`wsize`

might improve NFS performance in a congested network by sending smaller packets for each
NFS-read reply and write request. However, this reduction can increase the number of packets needed
to send data across the network, increasing total network traffic and CPU utilization on the client
and server.

It's important that you perform testing to find an `rsize`

and `wsize`

that sustains efficient
packet transfer, where it doesn't decrease throughput and increase latency.

For example, to configure a maximum `rsize`

and `wsize`

of 256-KiB, configure the `mountOptions`

in
the storage class as follows:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: azurefile-csi-nfs
provisioner: file.csi.azure.com
allowVolumeExpansion: true
parameters:
protocol: nfs
mountOptions:
- nconnect=4
- noresvport
- actimeo=30
- rsize=262144
- wsize=262144
```


## Other storage class examples

## Windows containers

The Azure Files CSI driver also supports Windows nodes and containers. To use Windows containers, follow the [Windows containers quickstart](learn/quick-windows-container-deploy-cli) to add a Windows node pool.

After you have a Windows node pool, use the built-in storage classes like

`azurefile-csi`

or create a custom one. You can deploy an example[Windows-based stateful set](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/deploy/example/windows/statefulset.yaml)that saves timestamps into a file`data.txt`

by running the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azurefile-csi-driver/master/deploy/example/windows/statefulset.yaml`

The output of the command resembles the following example:

`statefulset.apps/busybox-azurefile created`

Validate the contents of the volume by running the following

[kubectl exec](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec)command:`kubectl exec -it busybox-azurefile-0 -- cat c:\\mnt\\azurefile\\data.txt # on Linux or MacOS Bash kubectl exec -it busybox-azurefile-0 -- cat c:\mnt\azurefile\data.txt # on Windows Powershell or CMD`

The output of the commands resembles the following example:

`2020-08-27 22:11:01Z 2020-08-27 22:11:02Z 2020-08-27 22:11:04Z (...)`


## Next steps

- For Azure Files CSI driver parameters, see
[CSI driver parameters](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/docs/driver-parameters.md#static-provisionbring-your-own-file-share). - For more information about disk-based storage solutions, see
[Disk-based solutions in AKS](/en-us/azure/cloud-adoption-framework/scenarios/app-platform/aks/storage#disk-based-solutions). - For more information about storage best practices, see
[Best practices for storage and backups in Azure Kubernetes Service](operator-best-practices-storage). - For more information about Azure ultra disk, see [Use ultra disks on Azure Kubernetes Service (AKS)][use-ultra-disks].
- For more information about Azure tags, see
[Use Azure tags in Azure Kubernetes Service (AKS)](use-tags).
