---
merged_at: 2026-01-26T23:04:06.008585
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-multiple-standard-load-balancer -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/workload-identity-deploy-cluster -->

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

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-identity -->

# Best practices for authentication and authorization in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you deploy and maintain clusters in Azure Kubernetes Service (AKS), you implement ways to manage access to resources and services. Without these controls:

- Accounts could have access to unnecessary resources and services.
- Tracking credentials used to make changes can be difficult.

In this article, we discuss what recommended practices a cluster operator can follow to manage access and identity for AKS clusters. You'll learn how to:

- Authenticate AKS cluster users with Microsoft Entra ID.
- Control access to resources with Kubernetes role-based access control (Kubernetes RBAC).
- Use Azure RBAC to granularly control access to the AKS resource, the Kubernetes API at scale, and the
`kubeconfig`

. - Use a
[workload identity](workload-identity-overview)to access Azure resources from your pods.

Warning

The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service has been deprecated as of 10/24/2022.

If you have [Microsoft Entra pod-managed identity](use-azure-ad-pod-identity) enabled on your AKS cluster or are considering implementing it,
we recommend you **review the workload identity overview article** to understand our
recommendations and options to set up your cluster to use a Microsoft Entra Workload ID (preview).
This authentication method replaces pod-managed identity (preview), which integrates with the Kubernetes native capabilities
to federate with any external identity providers.

## Use Microsoft Entra ID


Best practice guidanceDeploy AKS clusters with

[Microsoft Entra integration]. Using Microsoft Entra ID centralizes the identity management layer. Any change in user account or group status is automatically updated in access to the AKS cluster. Scope users or groups to the minimum permissions amount using[Roles, ClusterRoles, or Bindings].

Your Kubernetes cluster developers and application owners need access to different resources. Kubernetes lacks an identity management solution for you to control the resources with which users can interact. Instead, you can integrate your cluster with an existing identity solution like Microsoft Entra ID, an enterprise-ready identity management solution.

With Microsoft Entra integrated clusters in AKS, you create *Roles* or *ClusterRoles* defining access permissions to resources. You then *bind* the roles to users or groups from Microsoft Entra ID. Learn more about these Kubernetes RBAC in [the next section](#use-kubernetes-role-based-access-control-kubernetes-rbac). Microsoft Entra integration and how you control access to resources can be seen in the following diagram:

- Developer authenticates with Microsoft Entra ID.
- The Microsoft Entra token issuance endpoint issues the access token.
- The developer performs an action using the Microsoft Entra token, such as
`kubectl create pod`

. - Kubernetes validates the token with Microsoft Entra ID and fetches the developer's group memberships.
- Kubernetes RBAC and cluster policies are applied.
- The developer's request is successful based on previous validation of Microsoft Entra group membership and Kubernetes RBAC and policies.

To create an AKS cluster that uses Microsoft Entra ID, see [Integrate Microsoft Entra ID with AKS](enable-authentication-microsoft-entra-id).

## Use Kubernetes role-based access control (Kubernetes RBAC)


Best practice guidanceDefine user or group permissions to cluster resources with Kubernetes RBAC. Create roles and bindings that assign the least amount of permissions required. Integrate with Microsoft Entra ID to automatically update any user status or group membership change and keep access to cluster resources current.


In Kubernetes, you provide granular access control to cluster resources. You define permissions at the cluster level, or to specific namespaces. You determine what resources can be managed and with what permissions. You then apply these roles to users or groups with a binding. For more information about *Roles*, *ClusterRoles*, and *Bindings*, see [Access and identity options for Azure Kubernetes Service (AKS)](concepts-identity).

For example, you create a role with full access to resources in the namespace named *finance-app*, as shown in the following example YAML manifest:

```
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
name: finance-app-full-access-role
namespace: finance-app
rules:
- apiGroups: [""]
resources: ["*"]
verbs: ["*"]
```


You then create a *RoleBinding* and bind the Microsoft Entra user *developer1@contoso.com* to it, as shown in the following YAML manifest:

```
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
name: finance-app-full-access-role-binding
namespace: finance-app
subjects:
- kind: User
name: developer1@contoso.com
apiGroup: rbac.authorization.k8s.io
roleRef:
kind: Role
name: finance-app-full-access-role
apiGroup: rbac.authorization.k8s.io
```


When *developer1@contoso.com* is authenticated against the AKS cluster, they have full permissions to resources in the *finance-app* namespace. In this way, you logically separate and control access to resources. Use Kubernetes RBAC with Microsoft Entra ID-integration.

To learn how to use Microsoft Entra groups to control access to Kubernetes resources using Kubernetes RBAC, see [Control access to cluster resources using role-based access control and Microsoft Entra identities in AKS](azure-ad-rbac).

## Use Azure RBAC


Best practice guidanceUse Azure RBAC to define the minimum required user and group permissions to AKS resources in one or more subscriptions.


There are two levels of access needed to fully operate an AKS cluster:

Access the AKS resource on your Azure subscription.

This access level allows you to:

- Control scaling or upgrading your cluster using the AKS APIs
- Pull your
`kubeconfig`

.

To learn how to control access to the AKS resource and the

`kubeconfig`

, see[Limit access to cluster configuration file](control-kubeconfig-access).Access to the Kubernetes API.

This access level is controlled either by:

[Kubernetes RBAC](#use-kubernetes-role-based-access-control-kubernetes-rbac)(traditionally) or- By integrating Azure RBAC with AKS for kubernetes authorization.

To learn how to granularly grant permissions to the Kubernetes API using Azure RBAC, see

[Use Azure RBAC for Kubernetes authorization](manage-azure-rbac).

## Use pod-managed identities

Warning

The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service has been deprecated as of 10/24/2022.

If you have [Microsoft Entra pod-managed identity](use-azure-ad-pod-identity) enabled on your AKS cluster or are considering implementing it,
we recommend you **review the workload identity overview article** to understand our
recommendations and options to set up your cluster to use a Microsoft Entra Workload ID (preview).
This authentication method replaces pod-managed identity (preview), which integrates with the Kubernetes native capabilities
to federate with any external identity providers.

Don't use fixed credentials within pods or container images, as they are at risk of exposure or abuse. Instead, use *pod identities* to automatically request access using Microsoft Entra ID.

To access other Azure resources, like Azure Cosmos DB, Key Vault, or Blob storage, the pod needs authentication credentials. You could define authentication credentials with the container image or inject them as a Kubernetes secret. Either way, you would need to manually create and assign them. Usually, these credentials are reused across pods and aren't regularly rotated.

With pod-managed identities (preview) for Azure resources, you automatically request access to services through Microsoft Entra ID. Pod-managed identities is currently in preview for AKS. Refer to the [Use Microsoft Entra pod-managed identities in Azure Kubernetes Service (Preview)](use-azure-ad-pod-identity) documentation to get started.

Microsoft Entra pod-managed identity (preview) supports two modes of operation:

**Standard**mode: In this mode, the following 2 components are deployed to the AKS cluster:[Managed Identity Controller(MIC)](https://azure.github.io/aad-pod-identity/docs/concepts/mic/): A Kubernetes controller that watches for changes to pods,[AzureIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentity/)and[AzureIdentityBinding](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentitybinding/)through the Kubernetes API Server. When it detects a relevant change, the MIC adds or deletes[AzureAssignedIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureassignedidentity/)as needed. Specifically, when a pod is scheduled, the MIC assigns the managed identity on Azure to the underlying virtual machine scale set used by the node pool during the creation phase. When all pods using the identity are deleted, it removes the identity from the virtual machine scale set of the node pool, unless the same managed identity is used by other pods. The MIC takes similar actions when AzureIdentity or AzureIdentityBinding are created or deleted.[Node Managed Identity (NMI)](https://azure.github.io/aad-pod-identity/docs/concepts/nmi/): is a pod that runs as a DaemonSet on each node in the AKS cluster. NMI intercepts security token requests to the[Azure Instance Metadata Service](/en-us/azure/virtual-machines/linux/instance-metadata-service?tabs=linux)on each node. It redirects requests to itself and validates if the pod has access to the identity it's requesting a token for, and fetch the token from the Microsoft Entra tenant on behalf of the application.

**Managed**mode: In this mode, there's only NMI. The identity needs to be manually assigned and managed by the user. For more information, see[Pod Identity in Managed Mode](https://azure.github.io/aad-pod-identity/docs/configure/pod_identity_in_managed_mode/). In this mode, when you use the[az aks pod-identity add](/en-us/cli/azure/aks/pod-identity#az-aks-pod-identity-add)command to add a pod identity to an Azure Kubernetes Service (AKS) cluster, it creates the[AzureIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentity/)and[AzureIdentityBinding](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentitybinding/)in the namespace specified by the`--namespace`

parameter, while the AKS resource provider assigns the managed identity specified by the`--identity-resource-id`

parameter to virtual machine scale set of each node pool in the AKS cluster.

Note

If you instead decide to install the Microsoft Entra pod-managed identity using the [AKS cluster add-on](use-azure-ad-pod-identity), setup uses the `managed`

mode.

The `managed`

mode provides the following advantages over the `standard`

:

- Identity assignment on the virtual machine scale set of a node pool can take up 40-60s. With cronjobs or applications that require access to the identity and can't tolerate the assignment delay, it's best to use
`managed`

mode as the identity is pre-assigned to the virtual machine scale set of the node pool. Either manually or using the[az aks pod-identity add](/en-us/cli/azure/aks/pod-identity#az-aks-pod-identity-add)command. - In
`standard`

mode, MIC requires write permissions on the virtual machine scale set used by the AKS cluster and`Managed Identity Operator`

permission on the user-assigned managed identities. When running in`managed mode`

, since there's no MIC, the role assignments aren't required.

Instead of manually defining credentials for pods, pod-managed identities request an access token in real time, using it to access only their assigned resources. In AKS, there are two components that handle the operations to allow pods to use managed identities:

**The Node Management Identity (NMI) server**is a pod that runs as a DaemonSet on each node in the AKS cluster. The NMI server listens for pod requests to Azure services.**The Azure Resource Provider**queries the Kubernetes API server and checks for an Azure identity mapping that corresponds to a pod.

When pods request a security token from Microsoft Entra ID to access to an Azure resource, network rules redirect the traffic to the NMI server.

The NMI server:

- Identifies pods requesting access to Azure resources based on their remote address.
- Queries the Azure Resource Provider.

The Azure Resource Provider checks for Azure identity mappings in the AKS cluster.

The NMI server requests an access token from Microsoft Entra ID based on the pod's identity mapping.

Microsoft Entra ID provides access to the NMI server, which is returned to the pod.

- This access token can be used by the pod to then request access to resources in Azure.


In the following example, a developer creates a pod that uses a managed identity to request access to Azure SQL Database:

- Cluster operator creates a service account to map identities when pods request access to resources.
- The NMI server is deployed to relay any pod requests, along with the Azure Resource Provider, for access tokens to Microsoft Entra ID.
- A developer deploys a pod with a managed identity that requests an access token through the NMI server.
- The token is returned to the pod and used to access Azure SQL Database

To use Pod-managed identities, see [Use Microsoft Entra pod-managed identities in Azure Kubernetes Service (preview)](use-azure-ad-pod-identity).

## Next steps

This best practices article focused on authentication and authorization for your cluster and resources. To implement some of these best practices, see the following articles:

[Integrate Microsoft Entra ID with AKS](enable-authentication-microsoft-entra-id)[Use Microsoft Entra pod-managed identities in Azure Kubernetes Service (preview)](use-azure-ad-pod-identity)

For more information about cluster operations in AKS, see the following best practices:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-configure-container-network-metrics-filtering -->

# Configure container network metrics filtering for Azure Kubernetes Service (AKS) (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to configure container network metrics filtering for Azure Kubernetes Service (AKS) with Cilium to optimize data collection, reduce storage costs, and focus on the metrics most relevant to your monitoring needs.

Configure container network metrics filtering enables dynamic management of Hubble metrics cardinality through Kubernetes Custom Resource Definitions (CRDs). This feature allows you to dynamically control the cardinality, dimensions, and targets of Hubble metrics without restarting Cilium agents or Prometheus servers.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of the Azure CLI required to complete the steps in this article is

**2.73.0**. To find your version, run`az --version`

in the Azure CLI. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).An AKS cluster with Cilium data plane and

[Advanced Container Networking Services](advanced-container-networking-services-overview)enabled.Kubernetes version 1.32 or later.

Container network metrics filtering works specifically with Cilium data planes.

The minimum version of the

`aks-preview`

Azure CLI extension to complete the steps in this article is`18.0.0b2`

.

### Install the aks-preview Azure CLI extension

Install or update the Azure CLI preview extension by using the [ az extension add](/en-us/cli/azure/extension#az_extension_add) or

[command.](/en-us/cli/azure/extension#az_extension_update)

`az extension update`

```
# Install the aks-preview extension
az extension add --name aks-preview
# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```


### Register the AdvancedNetworkingDynamicMetricsPreview feature flag

- First, register the AdvancedNetworkingDynamicMetricsPreview feature flag by using the
command:`az feature register`


```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingDynamicMetricsPreview"
```


- Verify successful registration by using the
command. It takes a few minutes for registration to complete.`az feature show`


```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingDynamicMetricsPreview"
```


- When the feature shows
**Registered**, refresh the registration of the`Microsoft.ContainerService`

resource provider by using thecommand.`az provider register`


```
az provider register --namespace Microsoft.ContainerService
```


### Create a new AKS cluster with Cilium

If you already have an existing cluster, you can skip this step.

Use the `az aks create`

command with the `--enable-acns`

flag to create a new AKS cluster that has all Advanced Container Networking Services features. These features include:

**Container Network Observability:**Provides insight into your network traffic. To learn more, see[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more, see[Container Network Security](advanced-container-networking-services-overview#container-network-security).

```
# Set environment variables
export RESOURCE_GROUP="cnm-testing-rg"
export CLUSTER_NAME="cnm-cilium-cluster"
export LOCATION="eastus2euap" # Use canary region for preview features
# Create resource group
az group create --name $RESOURCE_GROUP --location $LOCATION
# Create AKS cluster with Cilium and ACNS enabled
az aks create \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--location $LOCATION \
--network-plugin azure \
--network-dataplane cilium \
--enable-acns \
--enable-managed-identity \
--generate-ssh-keys \
--kubernetes-version 1.32
```


### Get cluster credentials

Get your cluster credentials by using the [ az aks get-credentials](/en-us/cli/azure/aks#az_aks_get_credentials) command:

```
az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --overwrite-existing
```


## Configure custom resources for metrics filtering

Container network metrics filtering uses the `ContainerNetworkMetric`

Custom Resource Definition (CRD) to define filtering rules. Only one CRD can exist per cluster, and changes take approximately 30 seconds to reconcile. If the CRD is not applied, all metrics will be collected.

```
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: : container-network-metric # Cluster scoped
spec:
filters:
- metric: flow
includeFilters: # List of include filters
- name: sample-filter # Filter name
from:
namespacedPod: # List of source namespace/pods. Prepend namespace with /
- sample-namespace/sample-pod
labelSelector: # Standard k8s label selector
matchLabels:
app: frontend
k8s.io/namespace: sample-namespace
matchExpressions:
- key: environment
operator: In
values:
- production
- staging
ip: # List of source IPs; can be CIDR
- "192.168.1.10"
- "10.0.0.1"
to:
namespacedPod:
- sample-namespace2/sample-pod2
labelSelector:
matchLabels:
app: backend
k8s.io/namespace: sample-namespace2
matchExpressions:
- key: tier
operator: NotIn
values:
- dev
ip:
- "192.168.1.20"
- "10.0.1.1"
protocol: # List of protocols; can be tcp, udp, dns
- tcp
- udp
- dns
verdict: # List of verdicts; can be forwarded, dropped
- forwarded
- dropped
metric: dns
excludeFilters: # List of exclude filters
- name: sample-filter # Filter name
from:
namespacedPod: # List of source namespace/pods. Prepend namespace with /
- sample-namespace/sample-pod
labelSelector: # Standard k8s label selector
matchLabels:
app: frontend
k8s.io/namespace: sample-namespace
```


The following table describes the fields in the custom resource definition:

| Field | Type | Description | Required |
|---|---|---|---|
`filters.metric` |
String | Name of the metric you would like to apply the filter on. This is mandatory. The supported values are `dns` , `flow` , `tcp` , `drop` |
Mandatory |
`includeFilters` or `excludeFilters` |
[]filter | A list of filters that define network flows to include. Each filter specifies the source, destination, protocol, and other matching criteria. You must have at least one include or exclude filter. | Mandatory |
`filters.name` |
String | The name of the filter. | Optional |
`filters.protocol` |
[]string | The protocols to match for this filter. Valid values are `tcp` , `udp` , and `dns` . Because it's an optional parameter, if it isn't specified, logs with all protocols are included. |
Optional |
`filters.verdict` |
[]string | The verdict of the flow to match. Valid values are `forwarded` and `dropped` . Because it's an optional parameter, if it isn't specified, logs with all verdicts are included. |
Optional |
`filters.from` |
Endpoint | Specifies the source of the network flow. Can include IP addresses, label selectors, and namespace/pod pairs. | Optional |
`Endpoint.ip` |
[]string | It can be a single IP or a CIDR. | Optional |
`Endpoint.labelSelector` |
Object | A label selector is a mechanism to filter and query resources based on labels, so you can identify specific subsets of resources. A label selector can include two components: `matchLabels` and `matchExpressions` . Use `matchLabels` for straightforward matching by specifying a key/value pair (for example, `{"app": "frontend"}` ). For more advanced criteria, use `matchExpressions` , where you define a label key, an operator (such as `In` , `NotIn` , `Exists` , or `DoesNotExist` ), and an optional list of values. Ensure that the conditions in both `matchLabels` and `matchExpressions` are met, because they're logically combined by `AND` . If no conditions are specified, the selector matches all resources. To match none, leave the selector null. Carefully define your label selector to target the correct set of resources. |
Optional |
`Endpoint.namespacedPod` |
[]string | A list of namespace and pod pairs (formatted as `namespace/pod` ) for matching the source. `name` should match the RegEx pattern `^.+$` . |
Optional |
`filters.to` |
Endpoint | Specifies the destination of the network flow. Can include IP addresses, label selectors, or namespace/pod pairs. | Optional |
`Endpoint.ip` |
[]string | It can be a single IP or a CIDR. | Optional |
`Endpoint.labelSelector` |
Object | A label selector to match resources based on their labels. | Optional |
`Endpoint.namespacedPod` |
[]string | A list of namespace and pod pairs (formatted as `namespace/pod` ) to match the destination. |
Optional |

Apply the `ContainerNetworkMetric`

custom resource to enable log collection at the cluster:

```
kubectl apply -f <crd.yaml>
```


## Clean up and reset

To clean up filtering configuration:

```
# Delete the CRD
kubectl delete ContainerNetworkMetric container-network-metric
```


## Example filtering configuration

- Create a basic filtering configuration that focuses on DNS metrics:

```
# basic-dns-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: dns # Supported: dns, flow, tcp, drop
excludeFilters:
- from:
namespacedPod: ["kube-system/coredns"]
```


- Configure filtering for TCP metrics with include and exclude filters:

```
# tcp-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: tcp
includeFilters:
- from:
labelSelector:
matchLabels:
tier: "frontend"
excludeFilters:
- to:
namespacedPod: ["kube-system/metrics-server"]
```


- Configure filtering for network flow metrics:

```
# flow-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: flow
includeFilters:
- from:
labelSelector:
matchLabels:
tier: "frontend"
- to:
labelSelector:
matchLabels:
tier: "backend"
excludeFilters:
- from:
namespacedPod: ["default/test"]
```


- Configure filtering for dropped packet metrics:

```
# drop-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: drop
excludeFilters:
- from:
namespacedPod: ["kube-system/"]
```


- Configure filtering for multiple metric types in a single CRD:

```
# multi-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: dns
includeFilters:
- protocol: ["dns"]
excludeFilters:
- from:
namespacedPod: ["kube-system/*"]
- metric: tcp
includeFilters:
- protocol: ["tcp"]
- from:
labelSelector:
matchLabels:
environment: "production"
- metric: flow
excludeFilters:
- from:
namespacedPod: ["default/debug-*"]
- metric: drop
includeFilters:
- reason: ["Policy denied", "Invalid"]
```


## Best practices

Ensure you do not have conflicting include and exclude filter on the CRD.

Leverage Kubernetes label selectors for flexible filtering.

Always validate filtering configurations in development or staging

Regularly review filtered metrics to ensure important data isn't lost.

Remember that only one CRD can exist per cluster.


## Troubleshooting

### Common issues

**Issue**: CRD configuration not applied

**Solution**: Check that the feature flag is registered and only one CRD exists:

```
# Verify feature registration
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingDynamicMetricsPreview"
# Check existing CRDs
kubectl get ContainerNetworkMetric
```


**Issue**: Metrics still showing after applying excludeFilters

**Solution**: Remember that preexisting metrics persist in Prometheus. You may need to wait for new metrics to be generated to see the filtering effects.

## Limitations

- This feature is specifically designed for Cilium data planes only
- Only one
`ContainerNetworkMetric`

CRD can exist per cluster - Preexisting metrics persist in Prometheus; new filtering rules apply to newly generated metrics
- Requires Kubernetes version 1.32 or later

## Related content

- To learn about container network metrics capabilities, see
[Container network metrics overview](container-network-observability-metrics). - To create an AKS cluster with Advanced Container Networking Services, see
[Set up Container Network Observability for AKS](container-network-observability-how-to). - Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-how-to -->

# Set up Container Network Observability for Azure Kubernetes Service (AKS) - Azure managed Prometheus and Grafana

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to set up Container Network Observability for Azure Kubernetes Service (AKS) using Managed Prometheus and Grafana and BYO Prometheus and Grafana and to visualize the scraped metrics

You can use Container Network Observability to collect data about the network traffic of your AKS clusters. It enables a centralized platform for monitoring application and network health. Currently, metrics are stored in Prometheus and Grafana can be used to visualize them. Container Network Observability also offers the ability to enable Hubble. These capabilities are supported for both Cilium and non-Cilium clusters.

Container Network Observability is one of the features of Advanced Container Networking Services. For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see [What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview)

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- The minimum version of Azure CLI required for the steps in this article is 2.56.0. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Enable Advanced Container Networking Services

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. These features encompass:

**Container Network Observability:**Provides insights into your network traffic. To learn more visit[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more visit[Container Network Security](advanced-container-networking-services-overview#container-network-security).

Note

Clusters with the Cilium data plane support Container Network Observability and Container Network security starting with Kubernetes version 1.29.

```
# Set an environment variable for the AKS cluster name. Make sure to replace the placeholder with your own value.
export CLUSTER_NAME="<aks-cluster-name>"
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--location eastus \
--max-pods 250 \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--node-count 2 \
--pod-cidr 192.168.0.0/16 \
--kubernetes-version 1.29 \
--enable-acns
```


### Enable Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the Advanced Container Networking Services flag,

`--enable-acns`

, updates an existing AKS cluster with all Advanced Container Networking Services features that includes [Container Network Observability](advanced-container-networking-services-overview#container-network-observability)and the

[Container Network Security](advanced-container-networking-services-overview#container-network-security)feature.

Note

Only clusters with the Cilium data plane support Container Network Security features of Advanced Container Networking Services.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns
```


## Get cluster credentials

Once you have Get your cluster credentials using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Azure managed Prometheus and Grafana

Skip this Section if using BYO Prometheus and Grafana

Use the following example to install and enable Prometheus and Grafana for your AKS cluster.

### Create Azure Monitor resource

```
#Set an environment variable for the Grafana name. Make sure to replace the placeholder with your own value.
export AZURE_MONITOR_NAME="<azure-monitor-name>"
# Create Azure monitor resource
az resource create \
--resource-group $RESOURCE_GROUP \
--namespace microsoft.monitor \
--resource-type accounts \
--name $AZURE_MONITOR_NAME \
--location eastus \
--properties '{}'
```


### Create Azure Managed Grafana instance

Use [az grafana create](/en-us/cli/azure/grafana#az-grafana-create) to create a Grafana instance. The name of the Grafana instance must be unique.

```
# Set an environment variable for the Grafana name. Make sure to replace the placeholder with your own value.
export GRAFANA_NAME="<grafana-name>"
# Create Grafana instance
az grafana create \
--name $GRAFANA_NAME \
--resource-group $RESOURCE_GROUP
```


### Place the Azure Managed Grafana and Azure Monitor resource IDs in variables

Use [az grafana show](/en-us/cli/azure/grafana#az-grafana-show) to place the Grafana resource ID in a variable. Use [az resource show](/en-us/cli/azure/resource#az-resource-show) to place the Azure Monitor resource ID in a variable. Replace **myGrafana** with the name of your Grafana instance.

```
grafanaId=$(az grafana show \
--name $GRAFANA_NAME \
--resource-group $RESOURCE_GROUP \
--query id \
--output tsv)
azuremonitorId=$(az resource show \
--resource-group $RESOURCE_GROUP \
--name $AZURE_MONITOR_NAME \
--resource-type "Microsoft.Monitor/accounts" \
--query id \
--output tsv)
```


### Link Azure Monitor and Azure Managed Grafana to the AKS cluster

Use [az aks update](/en-us/cli/azure/aks#az-aks-update) to link the Azure Monitor and Grafana resources to your AKS cluster.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--enable-azure-monitor-metrics \
--azure-monitor-workspace-resource-id $azuremonitorId \
--grafana-resource-id $grafanaId
```


## Visualization

### Visualization using Azure Managed Grafana

Skip this step if using BYO Grafana

Note

The `hubble_flows_processed_total`

metric isn't scraped by default due to high metric cardinality in large scale clusters.
Because of this, the *Pods Flows* dashboards have panels with missing data. To enable this metric and populate the missing data, you need to modify the ama-metrics-settings-configmap. Specifically, update the default-targets-metrics-keep-list section. Follow the below steps to update the configmap:

- Get the latest ama-metrics-settings-configmap.(
[https://github.com/Azure/prometheus-collector/blob/main/otelcollector/configmaps/ama-metrics-settings-configmap.yaml](https://github.com/Azure/prometheus-collector/blob/main/otelcollector/configmaps/ama-metrics-settings-configmap.yaml)) - Locate the networkobservabilityHubble = ""
- Change it to networkobservabilityHubble = "hubble.*"
- Now the Pod flow metrics should populate.

To learn more about what minimal ingestion, see the [Minimal Ingestion Documentation](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-configuration-minimal).

Make sure the Azure Monitor pods are running using the

`kubectl get pods`

command.`kubectl get pods -o wide -n kube-system | grep ama-`

Your output should look similar to the following example output:

`ama-metrics-5bc6c6d948-zkgc9 2/2 Running 0 (21h ago) 26h ama-metrics-ksm-556d86b5dc-2ndkv 1/1 Running 0 (26h ago) 26h ama-metrics-node-lbwcj 2/2 Running 0 (21h ago) 26h ama-metrics-node-rzkzn 2/2 Running 0 (21h ago) 26h ama-metrics-win-node-gqnkw 2/2 Running 0 (26h ago) 26h ama-metrics-win-node-tkrm8 2/2 Running 0 (26h ago) 26h`

We have created sample dashboards. They can be found under the

**Dashboards > Azure Managed Prometheus**folder. They have names like**"Kubernetes / Networking /**. The suite of dashboards includes:`<name>`

"**Clusters:**shows Node-level metrics for your clusters.**DNS (Cluster):**shows DNS metrics on a cluster or selection of Nodes.**DNS (Workload):**shows DNS metrics for the specified workload (for example, Pods of a DaemonSet or Deployment such as CoreDNS).**Drops (Workload):**shows drops to/from the specified workload (for example, Pods of a Deployment or DaemonSet).**Pod Flows (Namespace):**shows L4/L7 packet flows to/from the specified namespace (i.e. Pods in the Namespace).**Pod Flows (Workload):**shows L4/L7 packet flows to/from the specified workload (for example, Pods of a Deployment or DaemonSet).


### Visualization using BYO Grafana

Skip this step if using Azure managed Grafana

Add the following scrape job to your existing Prometheus configuration and restart your Prometheus server:

`- job_name: networkobservability-hubble kubernetes_sd_configs: - role: pod relabel_configs: - target_label: cluster replacement: myAKSCluster action: replace - source_labels: [__meta_kubernetes_namespace, __meta_kubernetes_pod_label_k8s_app] regex: kube-system;(retina|cilium) action: keep - source_labels: [__address__] action: replace regex: ([^:]+)(?::\d+)? replacement: $1:9965 target_label: __address__ - source_labels: [__meta_kubernetes_pod_node_name] target_label: instance action: replace metric_relabel_configs: - source_labels: [__name__] regex: '|hubble_dns_queries_total|hubble_dns_responses_total|hubble_drop_total|hubble_tcp_flags_total' # if desired, add |hubble_flows_processed_total action: keep`

In

**Targets**of Prometheus, verify the**network-obs-pods**are present.Sign in to Grafana and import following example dashboards using the following IDs:

**Clusters:**shows Node-level metrics for your clusters. (ID:[18814](https://grafana.com/grafana/dashboards/18814-kubernetes-networking-clusters/))**DNS (Cluster):**shows DNS metrics on a cluster or selection of Nodes.(ID:[20925](https://grafana.com/grafana/dashboards/20925-kubernetes-networking-dns-cluster/))**DNS (Workload):**shows DNS metrics for the specified workload (for example, Pods of a DaemonSet or Deployment such as CoreDNS). (ID: [20926][https://grafana.com/grafana/dashboards/20926-kubernetes-networking-dns-workload/](https://grafana.com/grafana/dashboards/20926-kubernetes-networking-dns-workload/))**Drops (Workload):**shows drops to/from the specified workload (for example, Pods of a Deployment or DaemonSet).(ID:[20927](https://grafana.com/grafana/dashboards/20927-kubernetes-networking-drops-workload/)).**Pod Flows (Namespace):**shows L4/L7 packet flows to/from the specified namespace (i.e. Pods in the Namespace). (ID:[20928](https://grafana.com/grafana/dashboards/20928-kubernetes-networking-pod-flows-namespace/))**Pod Flows (Workload):**shows L4/L7 packet flows to/from the specified workload (for example, Pods of a Deployment or DaemonSet). (ID:[20929](https://grafana.com/grafana/dashboards/20929-kubernetes-networking-pod-flows-workload/))

Note

- Depending on your Prometheus/Grafana instances' settings, some dashboard panels require specific tweaks to display all data.
- Cilium doesn't currently support DNS metrics/dashboards.


## Clean up resources

If you don't plan on using this application, delete the other resources you created in this article using the [ az group delete](/en-us/cli/azure/#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP
```


## Next steps

In this how-to article, you learned how to install and enable Container Network Observability for your AKS cluster.

For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).For more information on Container Network Security and its capabilities, see

[What is Container Network Security?](container-network-security-concepts).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/stateful-workload-upgrades -->

# Stateful workload upgrade patterns

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Upgrade clusters that run databases and stateful applications without data loss by using these proven patterns.

## What this article covers

This article provides database-specific upgrade patterns for Azure Kubernetes Service (AKS) clusters with stateful workloads, such as:

- PostgreSQL Ferris wheel pattern for ~30-second downtime.
- Redis rolling replacement for zero-downtime cache upgrades.
- MongoDB step-down cascades for replica set safety.
- Emergency upgrade checklists for security responses.
- Validation and rollback procedures for data protection.

These patterns are best for use by database administrators for applications with persistent data and mission-critical stateful services.

For more information, see these related articles:

- To upgrade your production AKS clusters, see
[AKS production upgrade strategies](aks-production-upgrade-strategies). - To check for and apply basic upgrades to your AKS cluster, see
[Upgrade an Azure Kubernetes Service cluster](upgrade-aks-cluster). - To use the scenario hub to help you choose the right AKS upgrade approach, see
[AKS upgrade scenarios: Choose your path](upgrade-scenarios-hub).

For a quick start, select a link for instructions:

[Do you need an emergency upgrade?](#emergency-upgrade-checklist)[Do you need help with a PostgreSQL cluster?](#the-ferris-wheel-pattern-postgresql)[Do you need a Redis cache rolling replace?](#redis-cluster-rolling-replace)

## Choose your pattern

| Database type | Upgrade pattern | Downtime | Complexity | Best for |
|---|---|---|---|---|
| PostgreSQL |
|

[Rolling replace](#redis-cluster-rolling-replace)[Step-down cascade](#mongodb-replica-set-step-down)*(coming soon)**(coming soon)*## Emergency upgrade checklist

Do you need to upgrade now because of security issues?

Run the following commands for an immediate safety check (two minutes):

`# Verify all replicas are healthy kubectl get pods -l tier=database -o wide # Check replication lag ./scripts/check-replica-health.sh # Ensure recent backup exists kubectl get job backup-job -o jsonpath='{.status.completionTime}'`

Choose an emergency pattern (one minute):

**PostgreSQL/MySQL:**Use[Ferris wheel](#the-ferris-wheel-pattern-postgresql)(30-second downtime).**Redis/Memcached:**Use[Rolling replace](#redis-cluster-rolling-replace)(zero downtime).**MongoDB/CouchDB:**Use[Step-down cascade](#mongodb-replica-set-step-down)(10-second downtime).

Run with a safety net (15-minute to 30-minute window):

- Always test rollback procedures in advance.
- Monitor application metrics during the upgrade.
- Keep the database team on standby.


## The Ferris wheel pattern: PostgreSQL

This pattern is best for 3-node PostgreSQL clusters with primary/replica setup across availability zones.

Visual pattern:

```
Initial: [PRIMARY] [REPLICA-1] [REPLICA-2]
Step 1: [PRIMARY] [REPLICA-1] [NEW-NODE] ← Add new node
Step 2: [REPLICA-1] [NEW-NODE] [REPLICA-2] ← Promote & remove old primary
Step 3: [NEW-PRIMARY] [NEW-NODE] [REPLICA-2] ← Complete rotation
```


### Quick implementation (20 minutes)

```
# 1. Add new node to cluster
kubectl scale statefulset postgres-cluster --replicas=4
# 2. Wait for new replica to sync
kubectl wait --for=condition=ready pod postgres-cluster-3 --timeout=300s
# 3. Promote new primary and failover (30-second downtime window)
kubectl exec postgres-cluster-3 -- pg_ctl promote -D /var/lib/postgresql/data
# 4. Update service endpoint
kubectl patch service postgres-primary --patch '{"spec":{"selector":{"app":"postgres-cluster","role":"primary","pod":"postgres-cluster-3"}}}'
# 5. Remove old primary node
kubectl delete pod postgres-cluster-0
```


**Detailed step-by-step guide**

#### Prerequisites validation

```
#!/bin/bash
# pre-upgrade-validation.sh
echo "=== PostgreSQL Cluster Health Check ==="
# Check replication status
kubectl exec postgres-primary-0 -- psql -c "SELECT * FROM pg_stat_replication;"
# Verify sync replication (must show 'sync' state)
SYNC_COUNT=$(kubectl exec postgres-primary-0 -- psql -t -c "SELECT count(*) FROM pg_stat_replication WHERE sync_state='sync';")
if [ "$SYNC_COUNT" -lt 2 ]; then
echo "ERROR: Need at least 2 synchronous replicas"
exit 1
fi
# Confirm recent backup exists
LAST_BACKUP=$(kubectl get job postgres-backup -o jsonpath='{.status.completionTime}')
echo "Last backup: $LAST_BACKUP"
# Test failover capability in staging first
echo "✅ Prerequisites validated"
```


#### Step 1: Scale up with a new node

```
# Add new node with upgraded Kubernetes version
kubectl patch statefulset postgres-cluster --patch '{
"spec": {
"replicas": 4,
"template": {
"spec": {
"nodeSelector": {
"kubernetes.io/arch": "amd64",
"aks-nodepool": "upgraded-pool"
}
}
}
}
}'
# Monitor new pod startup
kubectl get pods -l app=postgres-cluster -w
# Verify new replica joins cluster
kubectl exec postgres-cluster-3 -- psql -c "SELECT * FROM pg_stat_replication;"
```


#### Step 2: Run a controlled failover

```
#!/bin/bash
# controlled-failover.sh
echo "=== Starting Controlled Failover ==="
# Ensure minimal replication lag (< 0.1-second)
LAG=$(kubectl exec postgres-primary-0 -- psql -t -c "SELECT EXTRACT(EPOCH FROM now() - pg_last_xact_replay_timestamp());")
if (( $(echo "$LAG > 0.1" | bc -l) )); then
echo "ERROR: Replication lag too high ($LAG seconds)"
exit 1
fi
# Pause application writes (use connection pool drain)
kubectl patch configmap pgbouncer-config --patch '{"data":{"pgbouncer.ini":"[databases]\napp_db = host=postgres-primary port=5432 dbname=appdb pool_mode=statement max_db_connections=0"}}'
# Wait for active transactions to complete
sleep 10
# Promote new primary (this is the 30-second downtime window)
kubectl exec postgres-cluster-3 -- pg_ctl promote -D /var/lib/postgresql/data
# Update service selector to new primary
kubectl patch service postgres-primary --patch '{
"spec": {
"selector": {
"statefulset.kubernetes.io/pod-name": "postgres-cluster-3"
}
}
}'
# Resume application writes
kubectl patch configmap pgbouncer-config --patch '{"data":{"pgbouncer.ini":"[databases]\napp_db = host=postgres-primary port=5432 dbname=appdb pool_mode=statement"}}'
echo "✅ Failover completed"
```


#### Step 3: Clean up and validate

```
# Remove old primary node
kubectl delete pod postgres-cluster-0 --force
# Scale back to 3 replicas
kubectl patch statefulset postgres-cluster --patch '{"spec":{"replicas":3}}'
# Validate cluster health
kubectl exec postgres-cluster-3 -- psql -c "SELECT * FROM pg_stat_replication;"
# Test application connectivity
kubectl run test-db-connection --image=postgres:15 --rm -it -- psql -h postgres-primary -U app_user -d app_db -c "SELECT version();"
```


### Advanced configuration

For mission-critical databases that require a <10-second downtime:

```
# Use synchronous replication with multiple standbys
# postgresql.conf
synchronous_standby_names = 'ANY 2 (standby1, standby2, standby3)'
synchronous_commit = 'remote_apply'
```


### Success validation

To validate your progress, use the following checklist:

- New primary accepts reads and writes.
- All replicas show healthy replication.
- Application reconnects automatically.
- No data loss detected.
- Backup/restore tested on new primary.

### Emergency rollback

##### For immediate issues (<2 minutes)

Redirect traffic to the previous primary:

```
kubectl patch service postgres-primary --patch '{
"spec": {
"selector": {
"statefulset.kubernetes.io/pod-name": "postgres-cluster-1"
}
}
}'
```


##### For comprehensive failover recovery (5-10 minutes)

Stop writes to the current primary:

`kubectl exec postgres-primary-0 -- psql -c "SELECT pg_reload_conf();"`

Redirect service to a healthy replica:

`kubectl patch service postgres-primary --patch '{"spec":{"selector":{"statefulset.kubernetes.io/pod-name":"postgres-replica-1-0"}}}'`

Promote a replica to the new primary:

`kubectl exec postgres-replica-1-0 -- pg_ctl promote -D /var/lib/postgresql/data kubectl wait --for=condition=ready pod postgres-replica-1-0 --timeout=60s`

Update connection strings:

`kubectl patch configmap postgres-config --patch '{"data":{"primary-host":"postgres-replica-1-0.postgres"}}'`

Verify that the new primary accepts writes:

`kubectl exec postgres-replica-1-0 -- psql -c "CREATE TABLE upgrade_test (id serial, timestamp timestamp default now());" kubectl exec postgres-replica-1-0 -- psql -c "INSERT INTO upgrade_test DEFAULT VALUES;"`


**Expected outcome:** Approximately 30-second downtime, zero data loss, and an upgraded node that runs the current version of Kubernetes.

#### Step 3: Upgrade Node1 (former primary)

```
#!/bin/bash
# upgrade-node1.sh
echo "=== Step 3: Upgrade Node1 (Former Primary) ==="
# Drain Node1 gracefully
kubectl drain aks-nodepool1-12345678-vmss000000 --grace-period=300 --delete-emptydir-data --ignore-daemonsets
# Trigger node upgrade
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--kubernetes-version 1.29.0 \
--max-surge 0 \
--max-unavailable 1
# Monitor upgrade progress
while kubectl get node aks-nodepool1-12345678-vmss000000 -o jsonpath='{.status.conditions[?(@.type=="Ready")].status}' | grep -q "False"; do
echo "Waiting for node upgrade to complete..."
sleep 30
done
echo "Node1 upgrade completed"
```


#### Step 4: Rejoin Node1 as a replica

```
#!/bin/bash
# rejoin-node1.sh
echo "=== Step 4: Rejoin Node1 as Replica ==="
# Wait for postgres pod to be scheduled on upgraded node
kubectl wait --for=condition=ready pod postgres-primary-0 --timeout=300s
# Reconfigure as replica pointing to new primary (Node2)
kubectl exec postgres-primary-0 -- bash -c "
echo 'standby_mode = on' >> /var/lib/postgresql/data/recovery.conf
echo 'primary_conninfo = \"host=postgres-replica-1-0.postgres port=5432\"' >> /var/lib/postgresql/data/recovery.conf
"
# Restart postgres to apply replica configuration
kubectl delete pod postgres-primary-0
kubectl wait --for=condition=ready pod postgres-primary-0 --timeout=120s
# Verify replication is working
kubectl exec postgres-replica-1-0 -- psql -c "SELECT * FROM pg_stat_replication WHERE application_name='postgres-primary-0';"
echo "Node1 successfully rejoined as replica"
```


#### Step 5: Upgrade Node3 (Replica-2)

```
#!/bin/bash
# upgrade-node3.sh
echo "=== Step 5: Upgrade Node3 (Replica-2) ==="
# Similar process for Node3
kubectl drain aks-nodepool1-12345678-vmss000002 --grace-period=300 --delete-emptydir-data --ignore-daemonsets
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--kubernetes-version 1.29.0 \
--max-surge 0 \
--max-unavailable 1
# Wait for upgrade and pod readiness
kubectl wait --for=condition=ready pod postgres-replica-2-0 --timeout=300s
# Verify all replicas are in sync
kubectl exec postgres-replica-1-0 -- psql -c "SELECT application_name, state, sync_state FROM pg_stat_replication;"
```


#### Step 6: Final failover (Node2 → Node3)

```
#!/bin/bash
# final-failover.sh
echo "=== Step 6: Final Failover and Node2 Upgrade ==="
# Failover primary from Node2 to Node3
kubectl patch service postgres-primary --patch '{"spec":{"selector":{"statefulset.kubernetes.io/pod-name":"postgres-replica-2-0"}}}'
kubectl exec postgres-replica-2-0 -- pg_ctl promote -D /var/lib/postgresql/data
# Upgrade Node2
kubectl drain aks-nodepool1-12345678-vmss000001 --grace-period=300 --delete-emptydir-data --ignore-daemonsets
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--kubernetes-version 1.29.0 \
--max-surge 0 \
--max-unavailable 1
# Rejoin Node2 as replica
kubectl wait --for=condition=ready pod postgres-replica-1-0 --timeout=300s
echo "All nodes upgraded successfully. PostgreSQL cluster operational."
```


### Validation and monitoring

```
#!/bin/bash
# post-upgrade-validation.sh
echo "=== Post-Upgrade Validation ==="
# Verify cluster topology
kubectl get pods -l app=postgres -o wide
# Check all replicas are connected
kubectl exec postgres-replica-2-0 -- psql -c "SELECT application_name, client_addr, state FROM pg_stat_replication;"
# Validate data integrity
kubectl exec postgres-replica-2-0 -- psql -c "SELECT COUNT(*) FROM upgrade_test;"
# Performance validation
kubectl exec postgres-replica-2-0 -- psql -c "EXPLAIN ANALYZE SELECT * FROM pg_stat_activity;"
echo "Upgrade validation completed successfully"
```


## Redis cluster rolling replace

In this scenario, a six-node Redis cluster (three primaries and three replicas) requires zero downtime.

### Implementation

```
#!/bin/bash
# redis-cluster-upgrade.sh
echo "=== Redis Cluster Rolling Upgrade ==="
# Get cluster topology
kubectl exec redis-0 -- redis-cli cluster nodes
# Upgrade replica nodes first (no impact to writes)
for replica in redis-1 redis-3 redis-5; do
echo "Upgrading replica: $replica"
# Remove replica from cluster temporarily
REPLICA_ID=$(kubectl exec redis-0 -- redis-cli cluster nodes | grep $replica | cut -d' ' -f1)
kubectl exec redis-0 -- redis-cli cluster forget $REPLICA_ID
# Drain and upgrade node
kubectl delete pod $replica
kubectl wait --for=condition=ready pod $replica --timeout=120s
# Rejoin cluster
kubectl exec redis-0 -- redis-cli cluster meet $(kubectl get pod $replica -o jsonpath='{.status.podIP}') 6379
echo "Replica $replica upgraded and rejoined"
done
# Upgrade master nodes with failover
for master in redis-0 redis-2 redis-4; do
echo "Upgrading master: $master"
# Trigger failover to replica
kubectl exec $master -- redis-cli cluster failover
# Wait for failover completion
sleep 10
# Upgrade the demoted master (now replica)
kubectl delete pod $master
kubectl wait --for=condition=ready pod $master --timeout=120s
echo "Master $master upgraded"
done
echo "Redis cluster upgrade completed"
```


## MongoDB replica set step-down

In this scenario, a three-member MongoDB replica set requires coordinated primary step-down.

### Implementation

```
#!/bin/bash
# MongoDB upgrade script
Echo "=== MongoDB Replica Set Upgrade ==="
# Check replica set status
kubectl exec mongo-0 --mongo --eval "rs.status()"
```

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-paas-services -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/vertical-pod-autoscaler-api-reference -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-logs -->

# What is container network logs (preview)?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Component renaming (starting November 11, 2025)

We are renaming components in the Container Network Logs feature to improve clarity and consistency:

What's changing

**CRD**:`RetinaNetworkFlowLogs`

→`ContainerNetworkLog`

**CLI flag**:`--enable-retinanetworkflowlog`

→`--enable-container-network-logs`

**Log Analytics table**:`RetinaNetworkFlowLogs`

→`ContainerNetworkLog`


Action items for existing users to enable new naming

**Update Azure CLI**(MUST - First step!):`az upgrade`

**Update Preview CLI Extension**(MUST):`az extension update --name aks-preview`

**Disable Monitoring**:`az aks disable-addons -a monitoring -n <cluster-name> -g <resource-group>`

**Re-enable Monitoring**:`az aks enable-addons -a monitoring --enable-high-log-scale-mode -g <resource-group> -n <cluster-name>`

**Re-enable ACNS Container Network Logs**:`az aks update --enable-acns --enable-container-network-logs -g <resource-group> -n <cluster-name>`

**Apply new ContainerNetworkLog CRD**: Apply your updated CRD configuration with the new naming.**Reimport Grafana Dashboards**: Import the updated dashboards to reflect the new table names.

Note

- Previously collected data stays in your workspace in old table RetinaNetworkFlowLogs.
- After re-enabling, allow a short delay before new data appears in new table ContainerNetworkLog.

Container network logs in [Advanced Container Networking Services](advanced-container-networking-services-overview) for Azure Kubernetes Service (AKS) provide comprehensive, context-rich visibility into every network flow within your cluster. While metrics tell you *what* is happening in your network (such as bandwidth usage or error rates), container network logs tell you *why* by capturing the complete story of each connection—including who initiated it, what protocols were used, and whether the traffic was allowed or blocked.

These logs capture essential metadata for every network flow, including source and destination IP addresses, pod and service names, namespaces, ports, protocols, traffic direction, and policy verdicts. This deep contextual information enables you to correlate network behavior with specific workloads, troubleshoot connectivity issues, validate security policies, and perform forensic analysis.

Container network logs capture Layer 3 (IP), Layer 4 (TCP/UDP), and Layer 7 (HTTP/gRPC/Kafka) traffic, providing the detailed insights you need to monitor connectivity, troubleshoot issues, visualize network topology, enforce security policies, and ensure compliance.

Choose from two modes:

- Stored logs
- On-demand logs

## Stored logs

Stored logs mode ensures continuous log generation and collection in the AKS cluster when you enable Advanced Container Networking Services and set up custom filters. By default, log collection is disabled.

To enable log collection, you define *custom resources* to specify the types of traffic to monitor. Examples include namespaces, pods, services, and protocols. This feature remains active until you disable it.

Stored logs mode supports extended log retention and traffic filtering. For reduced storage costs and easier analysis, you can collect and retain only the logs that are relevant to you.

### How stored logs mode works

Advanced Container Networking Services uses eBPF technology with Cilium to fetch logs from nodes in your cluster. To start collecting logs, you define one or more custom resources to specify the types of traffic to monitor.

Custom resources provide fine-grained control to define and capture the traffic that is relevant to you. The Cilium agent running on each node collects network traffic that matches the criteria set in the custom resources. The logs are stored in JSON format on the host, providing a structured and accessible format for further use.

Alternatively, if the Azure Monitoring add-on is enabled, agents for Container insights collect the logs from the host, apply the default throttling limits, and send them to a Log Analytics workspace. The system aggregates and stores logs efficiently to provide visibility into network traffic for monitoring, troubleshooting, and security enforcement.

To read more about throttling and Container insights, see the [Container insights documentation](https://aka.ms/ContainerNetworkLogsDoc_CI).

### Key capabilities of stored logs mode

*Customizable filters.*You can configure logging by defining custom resources of the[ContainerNetworkLog](how-to-configure-container-network-logs#containernetworklog-crd-template)type. Use custom resources to apply granular filters by namespace, pod, service, port, protocol, verdict, or traffic direction (ingress or egress). This flexibility ensures precise data collection tailored to specific use cases. Only relevant traffic is logged, and storage is optimized for improved performance, compliance, and troubleshooting.*Log storage options.*The container network logs feature has two primary storage options: unmanaged storage and managed storage.**Unmanaged storage:**When a custom resource is applied to begin log collection, network flow logs are stored locally on the host nodes at the`/var/log/acns/hubble`

fixed mount location. This storage location is temporary because the node itself isn't a persistent storage solution. When the log files reach a size of 50 MB, they're automatically rotated and older logs are overwritten. This storage solution is suitable for real-time monitoring, but it doesn't support long-term storage or retention.For additional log management capabilities, you can integrate partner logging services like an OpenTelemetry collector. Partner integrations provide flexibility to manage logs outside the Azure ecosystem and are useful if you've already deployed a specific log management platform.

**Managed storage:**For long-term retention and advanced analytics, we recommend that you configure Azure monitoring in your AKS cluster to collect and store logs in a Log Analytics workspace. This setup ensures secure and compliant log storage. It also provides access to powerful capabilities like anomaly detection, performance tuning, and historical data analysis. You can use historical logs to identify trends, baseline behaviors, and proactively address recurring issues.For example, you can use the managed service for Prometheus to configure alerts on both metrics and logs for real-time monitoring and rapid detection of outliers.

You use the same workspace for log storage. You set up log storage space during onboarding. Both Analytics and Basic log table plans are supported for this feature. For more detailed information on table plans, see

[Azure Monitor Logs](/en-us/azure/azure-monitor/logs/data-platform-logs).

*Simple visualization in Log Analytics and Grafana dashboards.*Logs and data presented in Grafana dashboards simplify complex information, facilitate data comprehension, and help you make decisions more quickly.

### Logs visualization in the Azure portal

You can visualize, query, and analyze flow logs in the Azure portal in the Log Analytics workspace for your cluster.

### Logs visualization in Grafana dashboards

Access the flow logs in an Azure Managed Grafana instance.

To simplify your analysis of logs, we provide two preconfigured Grafana dashboards:

Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs**. This dashboard shows which AKS workloads are communicating with each other, including network requests, responses, drops, and errors. Currently, as an interim step during preview, you must import Grafana dashboards by using a user ID to view the flow logs dashboard in the Azure portal.Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs (External Traffic)**. This dashboard shows which AKS workloads send and receive communications from outside an AKS cluster, including network requests, responses, drops, and errors.For more information, see

[Set up Azure Managed Grafana with Advanced Container Networking Services](how-to-configure-container-network-logs#visualization-in-grafana-dashboards).

Access the flow logs in the Azure portal via the

**Dashboards with Grafana**option.

The Azure portal dashboards have the following major components:

*A comprehensive overview of network health.*You see key metrics like total flow logs, unique requests, dropped requests, and forwarded requests for quick anomaly detection and efficient troubleshooting. The dashboard categorizes statistics by protocol and behavior, including DNS dropped requests, HTTP 2xx responses, Layer 4 request and response rates, and dropped request counts. A service dependency graph visualizes application or cluster interactions, highlighting traffic flow, bottlenecks, and dependencies for performance optimization.*Flow logs and error logs for quick analysis.*You can filter flow logs for root-cause analysis. For example, to troubleshoot Domain Name System (DNS) issues, filter error logs by the DNS protocol.Separating flow logs and error logs helps you analyze issues more quickly. You can identify and address errors without sifting through unrelated information, which improves efficiency in troubleshooting and debugging processes.

Use clear labels and timestamps for each log entry to more easily pinpoint specific events or errors in your systems or processes.

*Top namespaces, workloads, and DNS errors.*Network flow log visualization is vital for monitoring and analyzing communication in an AKS cluster. It provides insight into namespaces, workloads, port usage, and query usage. It helps you identify trends, detect bottlenecks, and diagnose issues. Spot significant network activity, view dropped requests, and assess protocol distribution (for example, TCP versus UDP). This overview section of the dashboard supports cluster health, resource optimization, and security by detecting and displaying unusual traffic patterns.

## On-demand logs

Advanced Container Networking Services offers on-demand capture of network flow logs. Get real-time visibility without prior configuration or persistent storage by using the Hubble CLI and the Hubble UI. This on-demand logs mode is available. To learn how to set up on-demand log storage, see [Configure the Hubble CLI and Hubble UI](how-to-configure-container-network-logs#configure-on-demand-logs-mode).

### Hubble CLI

The Hubble command-line interface (CLI) provides a flexible and interactive way to query, filter, and analyze flow logs directly in the terminal. You can execute real-time commands to inspect traffic flows, view packet metadata, and troubleshoot network issues without leaving your operational environment.

### Hubble UI

The Hubble web-based interface offers an intuitive and visual platform for monitoring. With features like live traffic dashboards, flow summaries, and searchable logs, you can easily track service-to-service communication, detect anomalies, and gain insights into cluster activity.

The Hubble UI tools provide real-time visibility and actionable insights for faster troubleshooting and improved network management.

### Key benefits of on-demand logs

*Faster issue resolution.*With detailed and actionable insights into network traffic, you can identify and resolve connectivity or performance issues more quickly, minimizing downtime and disruptions.*Optimized operational efficiency.*Aggregated and efficiently stored logs reduce data management overhead. Your team can focus on analysis and decision-making instead of managing large volumes of raw data.*Enhanced application reliability.*By monitoring service-to-service communication and detecting anomalies, you can proactively address potential issues and ensure a smoother and more reliable application experience.*Improved decision-making.*Visualizing network patterns in Azure Managed Grafana and applying service maps provide clear insights into your application's network behavior. This leads to improved infrastructure planning and optimization.*Cost savings.*Efficient log aggregation and customizable logging scopes reduce storage and data ingestion costs, providing a cost-effective solution for long-term network monitoring.*Streamlined compliance and security.*Persistent and comprehensive logs support audit trails, regulatory compliance, and quick identification of suspicious traffic. They help you maintain a secure and compliant environment.

## Limitations

- Container network logs in stored logs mode currently works only with the Cilium data plane.
- Layer 7 flow logs are captured only when Layer 7 policy support is enabled. For more information, see
[Configure a Layer 7 policy](how-to-apply-l7-policies). - DNS flows and metrics are captured only when a Cilium Fully Qualified Domain (FQDN) network policy is applied. For more information, see
[Configure an FQDN policy](how-to-apply-fqdn-filtering-policies). - Onboarding by using Terraform currently isn't supported.
- When Log Analytics isn't configured for log storage, container network logs are limited to a maximum of 50 MB of storage. When this limit is reached, new entries overwrite older logs.
- If the table plan is set to Basic logs, prebuilt Grafana dashboards don't work.
- The Auxiliary logs table plan isn't supported.

## Pricing

Important

Advanced Container Networking Services is a paid offering.

For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Related content

- Learn how to set up
[container network logs](how-to-configure-container-network-logs). - Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services. - Explore the
[Container Network Security feature](advanced-container-networking-services-overview#container-network-security)in Advanced Container Networking Services.
