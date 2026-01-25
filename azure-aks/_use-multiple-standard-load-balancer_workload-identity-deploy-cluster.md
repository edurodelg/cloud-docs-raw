---
merged_at: 2026-01-25T12:06:27.855001
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-multiple-standard-load-balancer.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-multiple-standard-load-balancer -->

# Use multiple load balancers in Azure Kubernetes Service (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) normally provisions one Standard Load Balancer (SLB) for all `LoadBalancer`

Services in a cluster. Because each node NIC is limited to [ 300 inbound load‑balancing rules and 8 private‑link services](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#load-balancer), large clusters or port‑heavy workloads can quickly exhaust these limits.

The **multiple SLB preview** removes that bottleneck by letting you create several SLBs inside the same cluster and shard nodes and Services across them. You define *load‑balancer configurations*, each tied to a primary agent pool and optional namespace, label, or node selectors—and AKS automatically places nodes and Services on the appropriate SLB. Outbound SNAT behavior is unchanged if `outboundType`

is `loadBalancer`

. Outbound traffic still flows through the first SLB.

Use this feature to:

- Scale beyond 300 inbound rules without adding clusters.
- Isolate tenant or workload traffic by binding a dedicated SLB to its own agent pool.
- Distribute private‑link services across multiple SLBs when you approach the per‑SLB limit.

## Prerequisites

`aks-preview`

extension 18.0.0b1 or later.- Subscription feature flag
`Microsoft.ContainerService/MultipleStandardLoadBalancersPreview`

registered. - Kubernetes version 1.28 or later.
- Cluster created with
`--load-balancer-backend-pool-type nodeIP`

or update and existing cluster using`az aks update`

.

### Install the aks-preview Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the aks-preview extension using the

command.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the extension released using the

command.`az extension update`

`az extension update --name aks-preview`


### Register the `MultipleStandardLoadBalancersPreview`

feature flag

Register the

`MultipleStandardLoadBalancersPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "MultipleStandardLoadBalancersPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command:`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "MultipleStandardLoadBalancersPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## How AKS chooses a load balancer (node & Service placement)

AKS uses multiple inputs to determine where to place nodes and expose LoadBalancer Services. These inputs are defined in each load balancer configuration and influence which SLB is selected for each resource.

| Input type | Applies to | Description |
|---|---|---|
Primary agent pool`--primary-agent-pool-name` |
Nodes | Required. All nodes in this pool are always added to the SLB’s backend pool. Ensures each SLB has at least one healthy node. |
Node selector`--node-selector` |
Nodes | Optional. Adds any node with matching labels to the SLB, in addition to the primary pool. |
Service namespace selector`--service-namespace-selector` |
Services | Optional. Only Services in namespaces with matching labels are considered for this SLB. |
Service label selector`--service-label-selector` |
Services | Optional. Only Services with matching labels are eligible for this SLB. |
Service annotation`service.beta.kubernetes.io/azure-load-balancer-configurations` |
Services | Optional. Limits placement to one or more explicitly named SLB configurations. Without it, any matching configuration is eligible. |

Note

Selectors define eligibility. The annotation (if used) restricts the controller to a specific subset of SLBs.

### How AKS uses these inputs

The AKS control plane continuously reconciles node and Service state using the rules above:

#### Node placement

When a node is added or updated, AKS checks which SLBs it qualifies for based on primary pool and node selector.

- If multiple SLBs match, the controller picks the one with the fewest current nodes.
- The node is added to that SLB’s backend pool.

#### Service placement

When a LoadBalancer Service is created or updated:

- AKS finds SLBs whose namespace and label selectors match the Service.
- If the Service annotation is present, only those named SLBs are considered.
- SLBs that have allowServicePlacement=false or that would exceed Azure limits (300 rules or 8 private-link services) are excluded.
- Among valid options, the SLB with the fewest rules is chosen.

### externalTrafficPolicy (ETP) behavior

AKS handles Services differently depending on the value of `externalTrafficPolicy`

.

| Mode | How load balancer selection works | How backend pool membership is built | Notes |
|---|---|---|---|
Cluster (default) |
The controller follows the standard placement rules described above. A single load-balancing rule targets the shared kubernetes backend pool on the chosen SLB. |
All nodes in that SLB’s `kubernetes` pool are healthy targets. Nodes without matching Pods are removed automatically by health probes. |
Same behavior as today in single-SLB clusters. |
Local |
The controller still uses the selector-based algorithm to pick an SLB, but creates a dedicated backend pool per Service instead of using the shared pool. |
Membership is synced from the Service’s `EndpointSlice` objects, so only nodes that actually host ready Pods are added. Health probes continue to use `healthCheckNodePort` to drop unhealthy nodes. |
Guarantees client IP preservation and avoids routing through nodes that lack Pods, even when nodes are sharded across multiple SLBs. |


Why a dedicated pool for ETP Local?

In multi-SLB mode, nodes that host Pods for a given Service may reside on different SLBs from the client-facing VIP. A shared backend pool would often contain zero eligible nodes, breaking traffic. By allocating a per-Service pool and syncing it from`EndpointSlice`

, AKS ensures the Service’s SLB always points at the correct nodes.

**Impact on quotas**

- Each ETP Local Service adds one backend pool and one load-balancing rule to its SLB.
- These count toward the 300-rule limit, so monitor rule usage when you have many ETP Local Services.

**No change to outbound traffic**

Outbound SNAT still flows through the first SLB’s `aksOutboundBackendPool`

when `outboundType`

is `loadBalancer`

, independent of ETP settings.

#### Optional: Rebalancing

You can manually rebalance node distribution later using `az aks loadbalancer rebalance`

.

This design lets you define flexible, label-driven routing for both infrastructure and workloads, while AKS handles placement automatically to maintain balance and avoid quota issues.

## Add the first load balancer configuration

Add a configuration named `kubernetes`

and bind it to a *primary* agent pool that always has at least one node. Removing every configuration switches the cluster back to single‑SLB mode.

Important

To enable multiple‑SLB mode you **must** add a load‑balancer configuration named `kubernetes`

and attach it to a *primary* agent pool that always has at least one ready node.

The presence of this configuration toggles multi‑SLB support; in service selection, it has no special priority and is treated like any other load balancer configuration.

If you delete every load‑balancer configuration, the cluster automatically falls back to single‑SLB mode, which can briefly disrupt service routing or SNAT flows.

Set environment variables for use throughout this tutorial. You can replace all placeholder values with your own except

`DEFAULT_LB_NAME`

, which must remain as`kubernetes`

.`RESOURCE_GROUP="rg-aks-multislb" CLUSTER_NAME="aks-multi-slb" LOCATION="westus" DEFAULT_LB_NAME="kubernetes" PRIMARY_POOL="nodepool1"`

Create resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`

Create an AKS cluster using the

command.\`az aks create`

`az aks create --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME \ --load-balancer-backend-pool-type nodeIP \ --node-count 3`

Add a default load balancer using the

command.`az aks loadbalancer add`

`az aks loadbalancer add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME \ --name $DEFAULT_LB_NAME \ --primary-agent-pool-name $PRIMARY_POOL \ --allow-service-placement true`


## Add additional load balancers

Create tenant‑specific configurations by specifying a different primary pool plus optional namespace, label, or node selectors.

Team 1 will run its own workloads in a separate node pool. Assign a

`tenant=team1`

label so workloads can be scheduled using selectors:`TEAM1_POOL="team1pool" TEAM1_LB_NAME="team1-lb"`

Create a second node pool for team 1 using the

command.`az aks nodepool add`

`az aks nodepool add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME \ --name $TEAM1_POOL \ --labels tenant=team1 \ --node-count 2`

Create a load balancer for team 1 using the

command.`az aks loadbalancer add`

`az aks loadbalancer add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME \ --name $TEAM1_LB_NAME \ --primary-agent-pool-name $TEAM1_POOL \ --service-namespace-selector "tenant=team1" \ --node-selector "tenant=team1"`

Label the target namespace (e.g.,

`team1-apps`

) to match the selector using thecommand.`az aks command invoke`

`az aks command invoke \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --command " kubectl create namespace team1-apps --dry-run=client -o yaml | kubectl apply -f - kubectl label namespace team1-apps tenant=team1 --overwrite "`

You can now list the load balancers in the cluster to see the multiple configurations using the

command.`az aks loadbalancer list`

`az aks loadbalancer list --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --output table`

Example output:

`AllowServicePlacement ETag Name PrimaryAgentPoolName ProvisioningState ResourceGroup ----------------------- ------- ---------- ---------------------- ------------------- --------------- True <ETAG> kubernetes nodepool1 Succeeded rg-aks-multislb True <ETAG> team1-lb team1pool Succeeded rg-aks-multislb`


### Deploy a Service to a specific load balancer

Add the annotation `service.beta.kubernetes.io/azure-load-balancer-configurations`

with a comma‑separated list of configuration names. If the annotation is omitted, the controller chooses automatically.

```
az aks command invoke \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--command "
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Service
metadata:
name: lb-svc-1
namespace: team1-apps
labels:
app: nginx-test
annotations:
service.beta.kubernetes.io/azure-load-balancer-configurations: \"team1-lb\"
# service.beta.kubernetes.io/azure-load-balancer-internal: "true" # If you want to create an internal load balancer.
spec:
selector:
app: nginx-test
ports:
- name: port1
port: 80
targetPort: 80
protocol: TCP
type: LoadBalancer
---
apiVersion: apps/v1
kind: Deployment
metadata:
name: nginx-test
namespace: team1-apps
labels:
app: nginx
spec:
replicas: 1
selector:
matchLabels:
app: nginx-test
template:
metadata:
labels:
app: nginx-test
spec:
containers:
- image: nginx
imagePullPolicy: Always
name: nginx
ports:
- containerPort: 80
protocol: TCP
resources:
limits:
cpu: \"150m\"
memory: \"300Mi\"
EOF
"
```


### Rebalance nodes (optional)

Run a rebalance operation after scaling if rule counts become unbalanced using the [ az aks loadbalancer rebalance](/en-us/cli/azure/aks/loadbalancer#az-aks-loadbalancer-rebalance) command. This command disrupts active flows, so schedule it during a maintenance window.

```
az aks loadbalancer rebalance --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME
```


## Monitoring and troubleshooting

- Watch controller events (
`kubectl get events …`

) to confirm that Services are reconciled. - If external connectivity is blocked, open a node shell and curl the Service VIP to confirm kube‑proxy routing.

## Limitations and known issues

| Limitation | Details |
|---|---|
| Outbound SNAT | Always uses the first SLB; outbound flows aren’t sharded. |
| Backend pool type | Create or update and existing cluster to use `nodeIP` backend pools. |
| Autoscaler zeros | A primary agent pool can’t scale to 0 nodes. |
ETP `local` Rule Growth |
Each ETP `local` Service uses its own rule and backend pool, so rule counts can grow faster than with `cluster` mode. |
| Rebalance disruption | Removing a node from a backend pool drops in‑flight connections. Plan maintenance windows. |
| Configuration reload timing | After running `az aks loadbalancer` , changes may not take effect immediately. The AKS operation finishes quickly, but the cloud-controller-manager may take longer to apply updates. Wait for the `EnsuredLoadBalancer` event to confirm the changes are active. |

## Clean up resources

Delete the resource group when you’re finished to remove the cluster and load balancers using the [ az group delete](/en-us/cli/azure/group#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP --yes --no-wait
```


## Next steps

The multiple SLB feature helps scale and isolate workloads at the networking layer while maintaining simplicity through Azure-managed configuration. For more information, see the following resources:


---

<!-- DOCUMENTO FUSIONADO: workload-identity-deploy-cluster.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/workload-identity-deploy-cluster -->

# Deploy and configure Microsoft Entra Workload ID on an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy and configure an Azure Kubernetes Service (AKS) cluster with [Microsoft Entra Workload ID](workload-identity-overview). The steps in this article include:

- Create a new or update an existing AKS cluster using the Azure CLI with OpenID Connect (OIDC) issuer and Microsoft Entra Workload ID enabled.
- Create a workload identity and Kubernetes service account.
- Configure the managed identity for token federation.
- Deploy the workload and verify authentication with the workload identity.
- Optionally grant a pod in the cluster access to secrets in an Azure key vault.

## Prerequisites

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - This article requires version 2.47.0 or later of the Azure CLI. If using Azure Cloud Shell, the latest version is already installed.
- Make sure that the identity that you're using to create your cluster has the appropriate minimum permissions. For more information, see
[Access and identity options for Azure Kubernetes Service (AKS)](concepts-identity). - If you have multiple Azure subscriptions, select the appropriate subscription ID in which the resources should be billed using the
command.`az account set`


Note

You can use *Service Connector* to help you configure some steps automatically. For more information, see [Tutorial: Connect to Azure storage account in Azure Kubernetes Service (AKS) with Service Connector using Microsoft Entra Workload ID](/en-us/azure/service-connector/tutorial-python-aks-storage-workload-identity).

## Create a resource group

Create a resource group using the

command.`az group create`

`export RANDOM_ID="$(openssl rand -hex 3)" export RESOURCE_GROUP="myResourceGroup$RANDOM_ID" export LOCATION="<your-preferred-region>" az group create --name "${RESOURCE_GROUP}" --location "${LOCATION}"`


## Enable OIDC issuer and Microsoft Entra Workload ID on an AKS cluster

You can enable OIDC issuer and Microsoft Entra Workload ID on a new or existing AKS cluster.

Create an AKS cluster using the

command with the`az aks create`

`--enable-oidc-issuer`

parameter to enable OIDC issuer and the`--enable-workload-identity`

parameter to enable Microsoft Entra Workload ID. The following example creates a cluster with a single node:`export CLUSTER_NAME="myAKSCluster$RANDOM_ID" az aks create \ --resource-group "${RESOURCE_GROUP}" \ --name "${CLUSTER_NAME}" \ --enable-oidc-issuer \ --enable-workload-identity \ --generate-ssh-keys`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.


## Retrieve the OIDC issuer URL

Get the OIDC issuer URL and save it to an environmental variable using the [

`az aks show`

][az-aks-show] command.`export AKS_OIDC_ISSUER="$(az aks show --name "${CLUSTER_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --query "oidcIssuerProfile.issuerUrl" \ --output tsv)"`

The environment variable should contain the issuer URL, similar to the following example:

`https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/11111111-1111-1111-1111-111111111111/`

By default, the issuer is set to use the base URL

`https://{region}.oic.prod-aks.azure.com/{tenant_id}/{uuid}`

, where the value for`{region}`

matches the location to which the AKS cluster is deployed. The value`{uuid}`

represents the OIDC key, which is a randomly generated and immutable GUID for each cluster.

## Create a managed identity

Get your subscription ID and save it to an environment variable using the [

`az account show`

][az-account-show] command.`export SUBSCRIPTION="$(az account show --query id --output tsv)"`

Create a user-assigned managed identity using the

command.`az identity create`

`export USER_ASSIGNED_IDENTITY_NAME="myIdentity$RANDOM_ID" az identity create \ --name "${USER_ASSIGNED_IDENTITY_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --location "${LOCATION}" \ --subscription "${SUBSCRIPTION}"`

The following output example shows successful creation of a managed identity:

`{ "clientId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroupxxxxxx/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myIdentityxxxxxx", "location": "eastus", "name": "myIdentityxxxxxx", "principalId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "resourceGroup": "myResourceGroupxxxxxx", "systemData": null, "tags": {}, "tenantId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`

Get the client ID of the managed identity and save it to an environment variable using the [

`az identity show`

][az-identity-show] command.`export USER_ASSIGNED_CLIENT_ID="$(az identity show \ --resource-group "${RESOURCE_GROUP}" \ --name "${USER_ASSIGNED_IDENTITY_NAME}" \ --query 'clientId' \ --output tsv)"`


## Create a Kubernetes service account

Connect to your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --name "${CLUSTER_NAME}" --resource-group "${RESOURCE_GROUP}"`

Create a Kubernetes service account and annotate it with the client ID of the managed identity by applying the following manifest using the

`kubectl apply`

command:`export SERVICE_ACCOUNT_NAME="workload-identity-sa$RANDOM_ID" export SERVICE_ACCOUNT_NAMESPACE="default" cat <<EOF | kubectl apply -f - apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: "${USER_ASSIGNED_CLIENT_ID}" name: "${SERVICE_ACCOUNT_NAME}" namespace: "${SERVICE_ACCOUNT_NAMESPACE}" EOF`

The following output shows successful creation of the workload identity:

`serviceaccount/workload-identity-sa created`


## Create the federated identity credential

Create a federated identity credential between the managed identity, the service account issuer, and the subject using the

command.`az identity federated-credential create`

`export FEDERATED_IDENTITY_CREDENTIAL_NAME="myFedIdentity$RANDOM_ID" az identity federated-credential create \ --name ${FEDERATED_IDENTITY_CREDENTIAL_NAME} \ --identity-name "${USER_ASSIGNED_IDENTITY_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --issuer "${AKS_OIDC_ISSUER}" \ --subject system:serviceaccount:"${SERVICE_ACCOUNT_NAMESPACE}":"${SERVICE_ACCOUNT_NAME}" \ --audience api://AzureADTokenExchange`

Note

It takes a few seconds for the federated identity credential to propagate after it's added. If a token request is made immediately after adding the federated identity credential, the request might fail until the cache is refreshed. To avoid this issue, you can add a slight delay after adding the federated identity credential.


For more information about federated identity credentials in Microsoft Entra, see [Overview of federated identity credentials in Microsoft Entra ID](/en-us/graph/api/resources/federatedidentitycredentials-overview).

## Create a key vault with Azure RBAC authorization

The following example shows how to use the Azure role-based access control (Azure RBAC) permission model to grant the pod access to the key vault. For more information about the Azure RBAC permission model for Azure Key Vault, see [Grant permission to applications to access an Azure key vault using Azure RBAC](/en-us/azure/key-vault/general/rbac-guide).

Create a key vault with purge protection and Azure RBAC authorization enabled using the [

`az keyvault create`

][az-keyvault-create] command. You can also use an existing key vault if it's configured for both purge protection and Azure RBAC authorization:`export KEYVAULT_NAME="keyvault-workload-id$RANDOM_ID" # Ensure the key vault name is between 3-24 characters az keyvault create \ --name "${KEYVAULT_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --location "${LOCATION}" \ --enable-purge-protection \ --enable-rbac-authorization`

Get the key vault resource ID and save it to an environment variable using the [

`az keyvault show`

][az-keyvault-show] command.`export KEYVAULT_RESOURCE_ID=$(az keyvault show --resource-group "${RESOURCE_GROUP}" \ --name "${KEYVAULT_NAME}" \ --query id \ --output tsv)`


### Assign RBAC permissions for key vault management

Get the caller object ID and save it to an environment variable using the [

`az ad signed-in-user show`

][az-ad-signed-in-user-show] command.`export CALLER_OBJECT_ID=$(az ad signed-in-user show --query id -o tsv)`

Assign yourself the Azure RBAC

[Key Vault Secrets Officer](/en-us/azure/role-based-access-control/built-in-roles/security#key-vault-secrets-officer)role so that you can create a secret in the new key vault using the [`az role assignment create`

][az-role-assignment-create] command.`az role assignment create --assignee "${CALLER_OBJECT_ID}" \ --role "Key Vault Secrets Officer" \ --scope "${KEYVAULT_RESOURCE_ID}"`


### Create and configure secret access

Create a secret in the key vault using the [

`az keyvault secret set`

][az-keyvault-secret-set] command.`export KEYVAULT_SECRET_NAME="my-secret$RANDOM_ID" az keyvault secret set \ --vault-name "${KEYVAULT_NAME}" \ --name "${KEYVAULT_SECRET_NAME}" \ --value "Hello\!"`

Get the principal ID of the user-assigned managed identity and save it to an environment variable using the [

`az identity show`

][az-identity-show] command.`export IDENTITY_PRINCIPAL_ID=$(az identity show \ --name "${USER_ASSIGNED_IDENTITY_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --query principalId \ --output tsv)`

Assign the

[Key Vault Secrets User](/en-us/azure/role-based-access-control/built-in-roles/security#key-vault-secrets-user)role to the user-assigned managed identity using the [`az role assignment create`

][az-role-assignment-create] command. This step gives the managed identity permission to read secrets from the key vault.`az role assignment create \ --assignee-object-id "${IDENTITY_PRINCIPAL_ID}" \ --role "Key Vault Secrets User" \ --scope "${KEYVAULT_RESOURCE_ID}" \ --assignee-principal-type ServicePrincipal`

Create an environment variable for the key vault URL using the [

`az keyvault show`

][az-keyvault-show] command:`export KEYVAULT_URL="$(az keyvault show \ --resource-group "${RESOURCE_GROUP}" \ --name ${KEYVAULT_NAME} \ --query properties.vaultUri \ --output tsv)"`


## Deploy a verification pod and test access

Deploy a pod to verify that the workload identity can access the secret in the key vault. The following example uses the

`ghcr.io/azure/azure-workload-identity/msal-go`

image, which contains a sample application that retrieves a secret from Azure Key Vault using Microsoft Entra Workload ID:`kubectl apply -f - <<EOF apiVersion: v1 kind: Pod metadata: name: sample-workload-identity-key-vault namespace: ${SERVICE_ACCOUNT_NAMESPACE} labels: azure.workload.identity/use: "true" spec: serviceAccountName: ${SERVICE_ACCOUNT_NAME} containers: - image: ghcr.io/azure/azure-workload-identity/msal-go name: oidc env: - name: KEYVAULT_URL value: ${KEYVAULT_URL} - name: SECRET_NAME value: ${KEYVAULT_SECRET_NAME} nodeSelector: kubernetes.io/os: linux EOF`

Wait for the pod to be in the

`Ready`

state using the`kubectl wait`

command.`kubectl wait --namespace ${SERVICE_ACCOUNT_NAMESPACE} --for=condition=Ready pod/sample-workload-identity-key-vault --timeout=120s`

Check that the

`SECRET_NAME`

environment variable is set in the pod using thecommand.`kubectl describe`

`kubectl describe pod sample-workload-identity-key-vault | grep "SECRET_NAME:"`

If successful, the output should be similar to the following example:

`SECRET_NAME: ${KEYVAULT_SECRET_NAME}`

Verify that pods can get a token and access the resource using the

`kubectl logs`

command.`kubectl logs sample-workload-identity-key-vault`

If successful, the output should be similar to the following example:

`I0114 10:35:09.795900 1 main.go:63] "successfully got secret" secret="Hello\\!"`

Important

Azure RBAC role assignments can take up to 10 minutes to propagate. If the pod is unable to access the secret, you might need to wait for the role assignment to propagate. For more information, see

[Troubleshoot Azure RBAC](/en-us/azure/role-based-access-control/troubleshooting#).

## Disable Microsoft Entra Workload ID on an AKS cluster

Disable Microsoft Entra Workload ID on the AKS cluster where it's been enabled and configured, update the AKS cluster using the

command with the`az aks update`

`--disable-workload-identity`

parameter.`az aks update \ --resource-group "${RESOURCE_GROUP}" \ --name "${CLUSTER_NAME}" \ --disable-workload-identity`


## Related content

In this article, you deployed a Kubernetes cluster and configured it to use Microsoft Entra Workload ID in preparation for application workloads to authenticate with that credential. Now you're ready to deploy your application and configure it to use the workload identity with the latest version of the [Azure Identity](/en-us/azure/active-directory/develop/reference-v2-libraries) client library. If you can't rewrite your application to use the latest client library version, you can [set up your application pod](workload-identity-migrate-from-pod-identity) to authenticate using managed identity with workload identity as a short-term migration solution.

The [Service Connector](/en-us/azure/service-connector/overview) integration helps simplify the connection configuration for AKS workloads and Azure backing services. It securely handles authentication and network configurations and follows best practices for connecting to Azure services. For more information, see [Connect to Azure OpenAI in Foundry Models in AKS using Microsoft Entra Workload Identity](/en-us/azure/service-connector/tutorial-python-aks-openai-workload-identity) and the [Service Connector introduction](https://blog.aks.azure.com/2024/05/23/service-connector-intro).
