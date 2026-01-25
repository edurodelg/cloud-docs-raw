---
merged_at: 2026-01-25T12:25:33.974847
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: create-postgresql-ha.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/create-postgresql-ha -->

# Create infrastructure for deploying a highly available PostgreSQL database on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you create the infrastructure resources needed to deploy a highly available PostgreSQL database on AKS using the [CloudNativePG (CNPG)](https://cloudnative-pg.io/) operator.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Before you begin

- Review the deployment overview and make sure you meet all the prerequisites in
[How to deploy a highly available PostgreSQL database on AKS with Azure CLI](postgresql-ha-overview). [Set environment variables](#set-environment-variables)for use throughout this guide.[Install the required extensions](#install-required-extensions).

## Set environment variables

Set the following environment variables for use throughout this guide:

```
export SUFFIX=$(cat /dev/urandom | LC_ALL=C tr -dc 'a-z0-9' | fold -w 8 | head -n 1)
export LOCAL_NAME="cnpg"
export TAGS="owner=user"
export RESOURCE_GROUP_NAME="rg-${LOCAL_NAME}-${SUFFIX}"
export PRIMARY_CLUSTER_REGION="canadacentral"
export AKS_PRIMARY_CLUSTER_NAME="aks-primary-${LOCAL_NAME}-${SUFFIX}"
export AKS_PRIMARY_MANAGED_RG_NAME="rg-${LOCAL_NAME}-primary-aksmanaged-${SUFFIX}"
export AKS_PRIMARY_CLUSTER_FED_CREDENTIAL_NAME="pg-primary-fedcred1-${LOCAL_NAME}-${SUFFIX}"
export AKS_PRIMARY_CLUSTER_PG_DNSPREFIX=$(echo $(echo "a$(openssl rand -hex 5 | cut -c1-11)"))
export AKS_UAMI_CLUSTER_IDENTITY_NAME="mi-aks-${LOCAL_NAME}-${SUFFIX}"
export AKS_CLUSTER_VERSION="1.32"
export PG_NAMESPACE="cnpg-database"
export PG_SYSTEM_NAMESPACE="cnpg-system"
export PG_PRIMARY_CLUSTER_NAME="pg-primary-${LOCAL_NAME}-${SUFFIX}"
export PG_PRIMARY_STORAGE_ACCOUNT_NAME="hacnpgpsa${SUFFIX}"
export PG_STORAGE_BACKUP_CONTAINER_NAME="backups"
export MY_PUBLIC_CLIENT_IP=$(dig +short myip.opendns.com @resolver3.opendns.com)
```


## Install required extensions

Install the extensions needed for Kubernetes integration and monitoring:

```
az extension add --upgrade --name k8s-extension --yes
az extension add --upgrade --name amg --yes
```


As a prerequisite for using `kubectl`

, you need to first install [Krew](https://krew.sigs.k8s.io/), followed by the installation of the [CNPG plugin](https://cloudnative-pg.io/documentation/current/kubectl-plugin/#using-krew). These installations enable the management of the PostgreSQL operator using the subsequent commands.

```
(
set -x; cd "$(mktemp -d)" &&
OS="$(uname | tr '[:upper:]' '[:lower:]')" &&
ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(arm\)\(64\)\?.*/\1\2/' -e 's/aarch64$/arm64/')" &&
KREW="krew-${OS}_${ARCH}" &&
curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/${KREW}.tar.gz" &&
tar zxvf "${KREW}.tar.gz" &&
./"${KREW}" install krew
)
export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"
kubectl krew install cnpg
```


## Create a resource group

Create a resource group to hold the resources you create in this guide using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create \
--name $RESOURCE_GROUP_NAME \
--location $PRIMARY_CLUSTER_REGION \
--tags $TAGS \
--query 'properties.provisioningState' \
--output tsv
```


## Create a user-assigned managed identity

In this section, you create a user-assigned managed identity (UAMI) to allow the CNPG PostgreSQL to use an AKS workload identity to access Azure Blob Storage. This configuration allows the PostgreSQL cluster on AKS to connect to Azure Blob Storage without a secret.

Create a user-assigned managed identity using the

command.`az identity create`

`AKS_UAMI_WI_IDENTITY=$(az identity create \ --name $AKS_UAMI_CLUSTER_IDENTITY_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --output json)`

Enable AKS workload identity and generate a service account to use later in this guide using the following commands:

`export AKS_UAMI_WORKLOAD_OBJECTID=$( \ echo "${AKS_UAMI_WI_IDENTITY}" | jq -r '.principalId') export AKS_UAMI_WORKLOAD_RESOURCEID=$( \ echo "${AKS_UAMI_WI_IDENTITY}" | jq -r '.id') export AKS_UAMI_WORKLOAD_CLIENTID=$( \ echo "${AKS_UAMI_WI_IDENTITY}" | jq -r '.clientId') echo "ObjectId: $AKS_UAMI_WORKLOAD_OBJECTID" echo "ResourceId: $AKS_UAMI_WORKLOAD_RESOURCEID" echo "ClientId: $AKS_UAMI_WORKLOAD_CLIENTID"`


The object ID is a unique identifier for the client ID (also known as the application ID) that uniquely identifies a security principal of type *Application* within the Microsoft Entra ID tenant. The resource ID is a unique identifier to manage and locate a resource in Azure. These values are required to enabled AKS workload identity.

The CNPG operator automatically generates a service account called *postgres* that you use later in the guide to create a federated credential that enables OAuth access from PostgreSQL to Azure Storage.

## Create a storage account in the primary region

Create an object storage account to store PostgreSQL backups in the primary region using the

command.`az storage account create`

`az storage account create \ --name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --sku Standard_ZRS \ --kind StorageV2 \ --query 'provisioningState' \ --output tsv`

Create the storage container to store the Write Ahead Logs (WAL) and regular PostgreSQL on-demand and scheduled backups using the

command.`az storage container create`

`az storage container create \ --name $PG_STORAGE_BACKUP_CONTAINER_NAME \ --account-name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --auth-mode login`

Example output:

`{ "created": true }`

Note

If you encounter the error message:

`The request may be blocked by network rules of storage account. Please check network rule set using 'az storage account show -n accountname --query networkRuleSet'. If you want to change the default action to apply when no rule matches, please use 'az storage account update'`

. Make sure to verify user permissions for Azure Blob Storage and, if**necessary**, elevate your role to`Storage Blob Data Owner`

using the commands provided and after retry thecommand.`az storage container create`

`export USER_ID=$(az ad signed-in-user show --query id --output tsv) export STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID=$(az storage account show \ --name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query "id" \ --output tsv) az role assignment list --scope $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID --output table az role assignment create \ --assignee-object-id $USER_ID \ --assignee-principal-type User \ --scope $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID \ --role "Storage Blob Data Owner" \ --output tsv`


## Assign RBAC to storage accounts

To enable backups, the PostgreSQL cluster needs to read and write to an object store. The PostgreSQL cluster running on AKS uses a workload identity to access the storage account via the CNPG operator configuration parameter [ inheritFromAzureAD](https://cloudnative-pg.io/documentation/1.23/appendixes/object_stores/#azure-blob-storage).

Get the primary resource ID for the storage account using the

command.`az storage account show`

`export STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID=$(az storage account show \ --name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query "id" \ --output tsv) echo $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID`

Assign the "Storage Blob Data Contributor" Azure built-in role to the object ID with the storage account resource ID scope for the UAMI associated with the managed identity for each AKS cluster using the

command.`az role assignment create`

`az role assignment create \ --role "Storage Blob Data Contributor" \ --assignee-object-id $AKS_UAMI_WORKLOAD_OBJECTID \ --assignee-principal-type ServicePrincipal \ --scope $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID \ --query "id" \ --output tsv`


## Set up monitoring infrastructure

In this section, you deploy an instance of Azure Managed Grafana, an Azure Monitor workspace, and an Azure Monitor Log Analytics workspace to enable monitoring of the PostgreSQL cluster. You also store references to the created monitoring infrastructure to use as input during the AKS cluster creation process later in the guide. This section might take some time to complete.

Note

Azure Managed Grafana instances and AKS clusters are billed independently. For more pricing information, see [Azure Managed Grafana pricing](https://azure.microsoft.com/pricing/details/managed-grafana/).

Create an Azure Managed Grafana instance using the

command.`az grafana create`

`export GRAFANA_PRIMARY="grafana-${LOCAL_NAME}-${SUFFIX}" export GRAFANA_RESOURCE_ID=$(az grafana create \ --resource-group $RESOURCE_GROUP_NAME \ --name $GRAFANA_PRIMARY \ --location $PRIMARY_CLUSTER_REGION \ --zone-redundancy Enabled \ --tags $TAGS \ --query "id" \ --output tsv) echo $GRAFANA_RESOURCE_ID`

Create an Azure Monitor workspace using the

command.`az monitor account create`

`export AMW_PRIMARY="amw-${LOCAL_NAME}-${SUFFIX}" export AMW_RESOURCE_ID=$(az monitor account create \ --name $AMW_PRIMARY \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --tags $TAGS \ --query "id" \ --output tsv) echo $AMW_RESOURCE_ID`

Create an Azure Monitor Log Analytics workspace using the

command.`az monitor log-analytics workspace create`

`export ALA_PRIMARY="ala-${LOCAL_NAME}-${SUFFIX}" export ALA_RESOURCE_ID=$(az monitor log-analytics workspace create \ --resource-group $RESOURCE_GROUP_NAME \ --workspace-name $ALA_PRIMARY \ --location $PRIMARY_CLUSTER_REGION \ --query "id" \ --output tsv) echo $ALA_RESOURCE_ID`


## Create the AKS cluster to host the PostgreSQL cluster

In this section, you create a multizone AKS cluster with a system node pool. The AKS cluster hosts the PostgreSQL cluster primary replica and two standby replicas, each aligned to a different availability zone to enable zonal redundancy.

You also add a user node pool to the AKS cluster to host the PostgreSQL cluster. Using a separate node pool allows for control over the Azure VM SKUs used for PostgreSQL and enables the AKS system pool to optimize performance and costs. You apply a label to the user node pool that you can reference for node selection when deploying the CNPG operator later in this guide. This section might take some time to complete.

Important

If you opt to use local NVMe as your PostgreSQL storage in the later parts of this guide, you need to choose a VM SKU that supports local NVMe drives, for example, [Storage optimized VM SKUs](/en-us/azure/virtual-machines/sizes/overview#storage-optimized) or [GPU accelerated VM SKUs](/en-us/azure/virtual-machines/sizes/overview#gpu-accelerated). Update `$USER_NODE_POOL_VMSKU`

accordingly.

Create an AKS cluster using the

command.`az aks create`

`export SYSTEM_NODE_POOL_VMSKU="standard_d2s_v3" export USER_NODE_POOL_NAME="postgres" export USER_NODE_POOL_VMSKU="standard_d4s_v3" az aks create \ --name $AKS_PRIMARY_CLUSTER_NAME \ --tags $TAGS \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --generate-ssh-keys \ --node-resource-group $AKS_PRIMARY_MANAGED_RG_NAME \ --enable-managed-identity \ --assign-identity $AKS_UAMI_WORKLOAD_RESOURCEID \ --network-plugin azure \ --network-plugin-mode overlay \ --network-dataplane cilium \ --nodepool-name systempool \ --enable-oidc-issuer \ --enable-workload-identity \ --enable-cluster-autoscaler \ --min-count 2 \ --max-count 3 \ --node-vm-size $SYSTEM_NODE_POOL_VMSKU \ --enable-azure-monitor-metrics \ --azure-monitor-workspace-resource-id $AMW_RESOURCE_ID \ --grafana-resource-id $GRAFANA_RESOURCE_ID \ --api-server-authorized-ip-ranges $MY_PUBLIC_CLIENT_IP \ --tier standard \ --kubernetes-version $AKS_CLUSTER_VERSION \ --zones 1 2 3 \ --output table`

Wait for the initial cluster operation to complete using the

command so additional updates, such as adding the user node pool, don’t collide with an in-progress managed-cluster update:`az aks wait`

`az aks wait \ --resource-group $RESOURCE_GROUP_NAME \ --name $AKS_PRIMARY_CLUSTER_NAME \ --created`

Add a user node pool to the AKS cluster using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $AKS_PRIMARY_CLUSTER_NAME \ --name $USER_NODE_POOL_NAME \ --enable-cluster-autoscaler \ --min-count 3 \ --max-count 6 \ --node-vm-size $USER_NODE_POOL_VMSKU \ --zones 1 2 3 \ --labels workload=postgres \ --output table`


## Connect to the AKS cluster and create namespaces

In this section, you get the AKS cluster credentials, which serve as the keys that allow you to authenticate and interact with the cluster. Once connected, you create two namespaces: one for the CNPG controller manager services and one for the PostgreSQL cluster and its related services.

Get the AKS cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials \ --resource-group $RESOURCE_GROUP_NAME \ --name $AKS_PRIMARY_CLUSTER_NAME \ --output none`

Create the namespace for the CNPG controller manager services, the PostgreSQL cluster, and its related services by using the

command.`kubectl create namespace`

`kubectl create namespace $PG_NAMESPACE --context $AKS_PRIMARY_CLUSTER_NAME kubectl create namespace $PG_SYSTEM_NAMESPACE --context $AKS_PRIMARY_CLUSTER_NAME`


You can now define another environment variable based on your desired storage option, which you reference later in the guide when deploying PostgreSQL.

You can reference the default preinstalled Premium SSD Azure Disks CSI driver storage class:

```
export POSTGRES_STORAGE_CLASS="managed-csi-premium"
```


## Update the monitoring infrastructure

The Azure Monitor workspace for Managed Prometheus and Azure Managed Grafana are automatically linked to the AKS cluster for metrics and visualization during the cluster creation process. In this section, you enable log collection with AKS Container insights and validate that Managed Prometheus is scraping metrics and Container insights is ingesting logs.

Enable Container insights monitoring on the AKS cluster using the

command.`az aks enable-addons`

`az aks enable-addons \ --addon monitoring \ --name $AKS_PRIMARY_CLUSTER_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --workspace-resource-id $ALA_RESOURCE_ID \ --output table`

Validate that Managed Prometheus is scraping metrics and Container insights is ingesting logs from the AKS cluster by inspecting the DaemonSet using the

command and the`kubectl get`

command.`az aks show`

`kubectl get ds ama-metrics-node \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace=kube-system kubectl get ds ama-logs \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace=kube-system az aks show \ --resource-group $RESOURCE_GROUP_NAME \ --name $AKS_PRIMARY_CLUSTER_NAME \ --query addonProfiles`

Your output should resemble the following example output, with

*six*nodes total (three for the system node pool and three for the PostgreSQL node pool) and the Container insights showing`"enabled": true`

:`NAME DESIRED CURRENT READY UP-TO-DATE AVAILABLE NODE SELECTOR ama-metrics-node 6 6 6 6 6 <none> NAME DESIRED CURRENT READY UP-TO-DATE AVAILABLE NODE SELECTOR ama-logs 6 6 6 6 6 <none> { "omsagent": { "config": { "logAnalyticsWorkspaceResourceID": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/rg-cnpg-9vbin3p8/providers/Microsoft.OperationalInsights/workspaces/ala-cnpg-9vbin3p8", "useAADAuth": "true" }, "enabled": true, "identity": null } }`


## Create a public static IP for PostgreSQL cluster ingress

To validate deployment of the PostgreSQL cluster and use client PostgreSQL tooling, such as *psql* and *PgAdmin*, you need to expose the primary and read-only replicas to ingress. In this section, you create an Azure public IP resource that you later supply to an Azure load balancer to expose PostgreSQL endpoints for query.

Get the name of the AKS cluster node resource group using the

command.`az aks show`

`export AKS_PRIMARY_CLUSTER_NODERG_NAME=$(az aks show \ --name $AKS_PRIMARY_CLUSTER_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query nodeResourceGroup \ --output tsv) echo $AKS_PRIMARY_CLUSTER_NODERG_NAME`

Create the public IP address using the

command.`az network public-ip create`

`export AKS_PRIMARY_CLUSTER_PUBLICIP_NAME="$AKS_PRIMARY_CLUSTER_NAME-pip" az network public-ip create \ --resource-group $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --name $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --sku Standard \ --zone 1 2 3 \ --allocation-method static \ --output table`

Get the newly created public IP address using the

command.`az network public-ip show`

`export AKS_PRIMARY_CLUSTER_PUBLICIP_ADDRESS=$(az network public-ip show \ --resource-group $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --name $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME \ --query ipAddress \ --output tsv) echo $AKS_PRIMARY_CLUSTER_PUBLICIP_ADDRESS`

Get the resource ID of the node resource group using the

command.`az group show`

`export AKS_PRIMARY_CLUSTER_NODERG_NAME_SCOPE=$(az group show --name \ $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --query id \ --output tsv) echo $AKS_PRIMARY_CLUSTER_NODERG_NAME_SCOPE`

Assign the "Network Contributor" role to the UAMI object ID using the node resource group scope using the

command.`az role assignment create`

`az role assignment create \ --assignee-object-id ${AKS_UAMI_WORKLOAD_OBJECTID} \ --assignee-principal-type ServicePrincipal \ --role "Network Contributor" \ --scope ${AKS_PRIMARY_CLUSTER_NODERG_NAME_SCOPE}`


## Install the CNPG operator in the AKS cluster

In this section, you install the CNPG operator in the AKS cluster using Helm or a YAML manifest.

Add the CNPG Helm repo using the

command.`helm repo add`

`helm repo add cnpg https://cloudnative-pg.github.io/charts`

Upgrade the CNPG Helm repo and install it on the AKS cluster using the

command with the`helm upgrade`

`--install`

flag.`helm upgrade --install cnpg \ --namespace $PG_SYSTEM_NAMESPACE \ --create-namespace \ --kube-context=$AKS_PRIMARY_CLUSTER_NAME \ cnpg/cloudnative-pg`

Verify the operator installation on the AKS cluster using the

command.`kubectl get`

`kubectl get deployment \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_SYSTEM_NAMESPACE cnpg-cloudnative-pg`


## Next steps

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Ken Kilty | Principal TPM
- Russell de Pina | Principal TPM
- Adrian Joian | Senior Customer Engineer
- Jenny Hayes | Senior Content Developer
- Carol Smith | Senior Content Developer
- Erin Schaffer | Content Developer 2

## Acknowledgment

This documentation was jointly developed with EnterpriseDB, the maintainers of the CloudNativePG operator. We thank [Gabriele Bartolini](https://cloudnative-pg.io/authors/gbartolini/) for reviewing earlier drafts of this document and offering technical improvements.


---

<!-- DOCUMENTO FUSIONADO: http-proxy.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/http-proxy -->

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
