---
merged_at: 2026-01-25T12:06:27.851033
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: workload-identity-migrate-from-pod-identity.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/workload-identity-migrate-from-pod-identity -->

# Migrate Azure Kubernetes Service (AKS) pods from pod-managed identity to Microsoft Entra Workload ID

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Migrate AKS pods from pod-managed identities to [Microsoft Entra Workload ID](workload-identity-overview) (workload identity) using one of three approaches based on your current [Azure Identity SDK](/en-us/entra/identity-platform/reference-v2-libraries) version: latest SDK parallel deployment, migration sidecar proxy (Linux only), or SDK rewrite.

## Prerequisites

- Azure CLI version 2.47.0 or later. Run the
`az --version`

command to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Set environment variables

The following table lists the environment variables used in the commands throughout this article. Make sure to replace the placeholder values with your own values.

| Environment variable | Description | Example value |
|---|---|---|
`SUBSCRIPTION_ID` |
The ID of the Azure subscription where the AKS cluster and managed identity are created. | `00000000-0000-0000-0000-000000000000` |
`RESOURCE_GROUP` |
The name of the resource group where the AKS cluster and managed identity are created. | `myResourceGroup` |
`LOCATION` |
The Azure region where the AKS cluster and managed identity are created. | `eastus` |
`CLUSTER_NAME` |
The name of the AKS cluster. | `myAKSCluster` |
`MANAGED_IDENTITY_NAME` |
The name of the user-assigned managed identity. | `myManagedIdentity` |
`SERVICE_ACCOUNT_NAME` |
The name of the Kubernetes service account to create or associate with the managed identity. | `workload-identity-sa` |
`SERVICE_ACCOUNT_NAMESPACE` |
The namespace of the Kubernetes service account. | `default` |
`FEDERATED_IDENTITY_NAME` |
The name of the federated identity credential to create. | `myFederatedIdentity` |

## Choose a migration path

Select the appropriate migration approach based on your current Azure Identity SDK version:

**Latest Azure Identity SDK**: If your application already uses the latest version of Azure Identity SDK, you can migrate by deploying Microsoft Entra Workload ID in parallel with existing pod-managed identity.**Older SDK with migration sidecar**- If your application uses an older SDK version and runs on Linux containers, you can use a temporary migration sidecar to proxy Instance Metadata Service (IMDS) transactions while planning your SDK upgrade.**Older SDK rewrite approach**: If your application uses an older SDK version, you can update your application code to use the latest Azure Identity SDK, then migrate to workload identity.

## Prepare for migration

For all migration paths, you need to have the federated trust set up before you update your application to use Microsoft Entra Workload ID. The following are the minimum steps required:

[Create a managed identity](#create-a-managed-identity)credential.- Associate the user-assigned managed identity with the Kubernetes service account already used for the pod-managed identity or
[create a new Kubernetes service account](#create-kubernetes-service-account)and then associate it with the managed identity. [Establish a federated trust relationship](#establish-federated-identity-credential-trust)between the managed identity and Microsoft Entra ID using the[OpenID Connect (OIDC)](/en-us/azure/active-directory/develop/v2-protocols-oidc)issuer URL and the service account.

## Migrate from latest version of Azure Identity SDK

**This migration path applies when** your application already uses the latest version of the Azure Identity SDK and you want to migrate with minimal code changes.

**Migration approach**: Deploy Microsoft Entra Workload ID in parallel with pod-managed identity, verify functionality, then remove pod-managed identity.

**Steps**:

- Deploy Microsoft Entra Workload ID in parallel with existing pod-managed identity.
- Restart your application deployment to begin using Microsoft Entra Workload ID (OIDC annotations are injected automatically).
- Verify the application can authenticate successfully using workload identity.
[Remove the pod-managed identity](#remove-pod-managed-identity)annotations from your application.- Remove the pod-managed identity add-on from your cluster.

## Use a migration sidecar (Linux containers only)

**This migration path applies when** your application uses an older version of the Azure Identity SDK, runs on Linux containers, and you need a temporary solution while planning SDK updates.

**Migration approach**: Deploy a migration sidecar that proxies IMDS transactions to OIDC, allowing your existing application code to work without immediate changes.

**Important limitations**:

**Linux containers only**. Windows containers aren't supported.**Temporary solution**that's not intended for long-term production use.**Planning required**to schedule SDK updates for long-term support.

**Steps**:

[Deploy the workload with migration sidecar](#deploy-the-workload-with-migration-sidecar)to proxy IMDS transactions.- Verify authentication transactions complete successfully.
- Schedule application SDK updates to supported Azure Identity versions.
- Once SDKs are updated, remove the proxy sidecar and redeploy applications.

## Rewrite application for latest Azure Identity SDK

**This migration path applies when** your application uses an older version of the Azure Identity SDK and you want to update to the latest supported SDK before migrating.

**Migration approach**: Update your application code to use the latest Azure Identity SDK, then migrate to Microsoft Entra Workload ID with the updated code.

**Technical outcomes**:

- Uses current Azure Identity SDK versions (no deprecation timeline).
- Supports both Linux and Windows containers (unlike sidecar approach).
- Eliminates proxy components and IMDS translation overhead.

**Steps**:

- Update your application code to use the latest
[Azure Identity SDK](workload-identity-overview#prerequisites). - Test the updated application with pod-managed identity.
- Restart your application deployment to begin authenticating using Microsoft Entra Workload ID (OIDC annotations are injected automatically).
- Verify authentication transactions complete successfully.
[Remove the pod-managed identity](#remove-pod-managed-identity)annotations and add-on.

## Set an active Azure subscription

Set a specific Azure subscription as the current active subscription using the

command.`az account set`

`az account set --subscription $SUBSCRIPTION_ID`


## Create a managed identity

Create a managed identity using the

command.`az identity create`

`az identity create --name $MANAGED_IDENTITY_NAME --resource-group $RESOURCE_GROUP --location $LOCATION --subscription $SUBSCRIPTION_ID`


## Get managed identity client ID

Get the client ID of the managed identity and save it to an environmental variable using the

command.`az identity show`

`export USER_ASSIGNED_CLIENT_ID="$(az identity show --resource-group $RESOURCE_GROUP --name $MANAGED_IDENTITY_NAME --query 'clientId' -otsv)"`


## Grant managed identity access to Azure resources

- Grant the managed identity the permissions needed to access the required Azure resources. Follow the steps in
[Assign a managed identity access to a resource](/en-us/azure/role-based-access-control/role-assignments-portal-managed-identity)to assign the appropriate role to the managed identity.

## Get OIDC issuer URL

Get the OIDC issuer URL and save it to an environmental variable using the

command.`az aks show`

`export AKS_OIDC_ISSUER="$(az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query "oidcIssuerProfile.issuerUrl" -o tsv)"`

The variable should contain an issuer URL similar to the following example:

`https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/00000000-0000-0000-0000-000000000000/`

By default, the issuer uses the base URL

`https://{region}.oic.prod-aks.azure.com/{uuid}`

, where the value for`{region}`

matches the location the AKS cluster is deployed in. The value`{uuid}`

represents the OIDC key.

## Get AKS cluster credentials

Get the AKS cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP`


## Create Kubernetes service account

Create a Kubernetes service account and annotate it with the managed identity client ID using the

`kubectl apply`

command. Make sure to replace the placeholder values with your own values.`cat <<EOF | kubectl apply -f - apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: ${USER_ASSIGNED_CLIENT_ID} name: ${SERVICE_ACCOUNT_NAME} namespace: ${SERVICE_ACCOUNT_NAMESPACE} EOF`

The following output resembles successful creation of the identity:

`Serviceaccount/workload-identity-sa created`


## Establish federated identity credential trust

Create the federated identity credential between the managed identity, service account issuer, and subject using the

command.`az identity federated-credential create`

`az identity federated-credential create --name $FEDERATED_IDENTITY_NAME --identity-name $MANAGED_IDENTITY_NAME --resource-group $RESOURCE_GROUP --issuer ${AKS_OIDC_ISSUER} --subject system:serviceaccount:${SERVICE_ACCOUNT_NAMESPACE}:${SERVICE_ACCOUNT_NAME} --audience api://AzureADTokenExchange`

The federated identity credential takes a few minutes to propagate after being added. If a token request is made immediately after adding the federated identity credential, the token request might fail because the Azure AD directory cache contains outdated information.


## Deploy the workload with migration sidecar

If your application uses user-assigned managed identity and still relies on IMDS to get an access token you can use the migration sidecar to start migrating to Microsoft Entra Workload ID. In long-term applications, you should modify the code to use the latest Azure Identity SDKs that support client assertion.

To update or deploy the workload, add the following [pod annotations](workload-identity-overview#pod-annotations) to your pod specification (only if you want to use the migration sidecar):

| Pod annotation | Description | Value |
|---|---|---|
`azure.workload.identity/inject-proxy-sidecar` |
Indicates whether to inject the proxy sidecar into the pod. | `true` or `false` |
`azure.workload.identity/proxy-sidecar-port` |
Desired port for the proxy sidecar. | Default value: `8000` |

When you create a pod with these annotations, the Microsoft Entra Workload ID mutating webhook automatically injects the `init-container`

and proxy sidecar to the pod spec. The following YAML shows an example of what the mutating webhook adds to the pod deployment:

```
apiVersion: v1
kind: Pod
metadata:
name: httpbin-pod
labels:
app: httpbin
azure.workload.identity/use: "true"
annotations:
azure.workload.identity/inject-proxy-sidecar: "true"
spec:
serviceAccountName: workload-identity-sa
initContainers:
- name: init-networking
image: mcr.microsoft.com/oss/azure/workload-identity/proxy-init:v1.1.0
securityContext:
capabilities:
add:
- NET_ADMIN
drop:
- ALL
privileged: true
runAsUser: 0
env:
- name: PROXY_PORT
value: "8000"
containers:
- name: nginx
image: nginx:alpine
ports:
- containerPort: 80
- name: proxy
image: mcr.microsoft.com/oss/azure/workload-identity/proxy:v1.1.0
ports:
- containerPort: 8000
```


## Verify the workload with migration sidecar

Verify the pod is in a running state using the

command. Replace`kubectl describe pod`

`<pod-name>`

with the name of your pod.`kubectl describe pods <pod-name>`

Verify the pod is passing IMDS transactions using the

command. Replace`kubectl logs`

`<pod-name>`

with the name of your pod.`kubectl logs <pod-name>`

The following example log output resembles successful communication through the proxy sidecar. Verify the logs show a token is successfully acquired and the

`GET`

operation is successful.`I0926 00:29:29.968723 1 proxy.go:97] proxy "msg"="starting the proxy server" "port"=8080 "userAgent"="azure-workload-identity/proxy/v0.13.0-12-gc8527f3 (linux/amd64) c8527f3/2022-09-26-00:19" I0926 00:29:29.972496 1 proxy.go:173] proxy "msg"="received readyz request" "method"="GET" "uri"="/readyz" I0926 00:29:30.936769 1 proxy.go:107] proxy "msg"="received token request" "method"="GET" "uri"="/metadata/identity/oauth2/token?resource=https://management.core.windows.net/api-version=2018-02-01&client_id=<client_id>" I0926 00:29:31.101998 1 proxy.go:129] proxy "msg"="successfully acquired token" "method"="GET" "uri"="/metadata/identity/oauth2/token?resource=https://management.core.windows.net/api-version=2018-02-01&client_id=<client_id>"`


## Remove pod-managed identity

After you complete your testing and the application can successfully get a token using the proxy sidecar, you can remove the identity and pod-managed identity mapping from your AKS cluster

Remove the pod-managed identity binding from your pod using the

command. Replace`az aks pod-identity delete`

`<pod-identity-name>`

and`<pod-identity-namespace>`

with the name and namespace of your pod identity.`az aks pod-identity delete --name <pod-identity-name> --namespace <pod-identity-namespace> --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME`


## Related content

For more information about Microsoft Entra Workload ID, see the [Overview](workload-identity-overview) article.


---

<!-- DOCUMENTO FUSIONADO: use-node-taints.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-node-taints -->

# Use node taints in an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to use node taints in an Azure Kubernetes Service (AKS) cluster.

## Overview

The AKS scheduling mechanism is responsible for placing pods onto nodes and is based upon the upstream Kubernetes scheduler, [kube-scheduler](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/). You can constrain a pod to run on particular nodes by attaching the pods to a set of nodes using [node affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity) or by instructing the node to repel a set of pods using [node taints](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/), which interact with the AKS scheduler.

Node taints work by marking a node so that the scheduler avoids placing certain pods on the marked nodes. You can place [tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) on a pod to allow the scheduler to schedule that pod on a node with a matching taint. Taints and tolerations work together to help you control how the scheduler places pods onto nodes. For more information, see [example use cases of taints and tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/#example-use-cases:%7E:text=not%20be%20evicted.-,Example%20Use%20Cases,-Taints%20and%20tolerations).

Taints are key-value pairs with an [effect](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/). There are three values for the effect field when using node taints: `NoExecute`

, `NoSchedule`

, and `PreferNoSchedule`

.

`NoExecute`

: Pods already running on the node are immediately evicted if they don't have a matching toleration. If a pod has a matching toleration, it might be evicted if`tolerationSeconds`

are specified.`NoSchedule`

: Only pods with a matching toleration are placed on this node. Existing pods aren't evicted.`PreferNoSchedule`

: The scheduler avoids placing any pods that don't have a matching toleration.

### Node taint options

There are two types of node taints that can be applied to your AKS nodes: **node taints** and **node initialization taints**.

**Node taints**are meant to remain permanently on the node for scheduling pods with node affinity. Node taints can only be added, updated, or removed completely using the AKS API.**Node initialization taints**are placed on the node at boot time and are meant to be used temporarily, such as in scenarios where you might need extra time to set up your nodes. You can remove node initialization taint using the Kubernetes API and they aren't guaranteed during the node lifecycle. They will appear on new replicas of the node when it is scaled up or on all replicas when a node is upgraded. If you want to remove the initialization taints completely, you can remove them using the AKS API after untainting the nodes using the Kubernetes API. Once you remove the initialization taints from the cluster spec using the AKS API, newly created nodes don't come up with those initialization taints. If the initialization taint is still present on existing nodes, you can permanently remove it by performing a node image upgrade operation.

Note

Node taints and labels applied using the AKS node pool API aren't modifiable from the Kubernetes API and vice versa. Modifications to system taints aren't allowed.

This doesn't apply to node initialization taints.

## Use node taints

### Prerequisites

This article assumes you have an existing AKS cluster. If you need an AKS cluster, you can create one using [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

### Create a node pool with a node taint

Create a node pool with a taint using the

command and use the`az aks nodepool add`

`--node-taints`

parameter to specify`sku=gpu:NoSchedule`

for the taint.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-count 1 \ --node-taints "sku=gpu:NoSchedule" \ --no-wait`


### Update a node pool to add a node taint

Update a node pool to add a node taint using the

command and use the`az aks nodepool update`

`--node-taints`

parameter to specify`sku=gpu:NoSchedule`

for the taint.`az aks nodepool update \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-taints "sku=gpu:NoSchedule" \ --no-wait`


## Use node initialization taints (preview)

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Prerequisites and limitations

- You need the Azure CLI version
`3.0.0b3`

or later installed and configured. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You can only apply initialization taints via cluster create or upgrade when using the AKS API. If using ARM template that will result in a Managed Cluster level operation, you can specify node initialization taints during node pool creation and update. Agentpool level operations are blocked when
`NodeInitializationTaints`

are present in the request body. - You can't apply initialization taints to Windows node pools using the Azure CLI.

### Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME`


### Install the `aks-preview`

Azure CLI extension

Register or update the aks-preview extension using the

or`az extension add`

command.`az extension update`

`# Register the aks-preview extension az extension add --name aks-preview # Update the aks-preview extension az extension update --name aks-preview`


### Register the `NodeInitializationTaintsPreview`

feature flag

Register the

`NodeInitializationTaintsPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "NodeInitializationTaintsPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "NodeInitializationTaintsPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create a cluster with a node initialization taint

Create a cluster with a node initialization taint using the

command and the`az aks create`

`--node-initialization-taints`

parameter to specify`sku=gpu:NoSchedule`

for the taint.Important

The node initialization taints you specify apply to all of the node pools in the cluster. To apply the initialization taint to a specific node, you can use an ARM template instead of the CLI.

`az aks create \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --node-count 1 \ --node-init-taints "sku=gpu:NoSchedule" \ --generate-ssh-keys`


### Update a cluster to add a node initialization taint

Update a cluster to add a node initialization taint using the

command and the`az aks update`

`--node-initialization-taints`

parameter to specify`sku=gpu:NoSchedule`

for the taint.Important

When updating a cluster with a node initialization taint, the taints apply to all node pools in the cluster. If your nodes are using VMSS, you can view updates to node initialization taints on the node after the node's VMSS model is updated (for example, after a node image version upgrade operation). Initialization taints will not appear on your nodes until an operation that triggers a VMSS model update occurs.

`az aks update \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --node-init-taints "sku=gpu:NoSchedule"`


## Check the status of the node pool

After applying the node taint or initialization taint, check the status of the node pool using the

command.`az aks nodepool list`

`az aks nodepool list --resource-group $RESOURCE_GROUP_NAME --cluster-name $CLUSTER_NAME`

If you applied node taints, the following example output shows that the

`<node-pool-name>`

node pool is`Creating`

nodes with the specified`nodeTaints`

:`[ { ... "count": 1, ... "name": "<node-pool-name>", "orchestratorVersion": "1.15.7", ... "provisioningState": "Creating", ... "nodeTaints": [ "sku=gpu:NoSchedule" ], ... }, ... ]`

If you applied node initialization taints, the following example output shows that the

`<node-pool-name>`

node pool is`Creating`

nodes with the specified`nodeInitializationTaints`

:`[ { ... "count": 1, ... "name": "<node-pool-name>", "orchestratorVersion": "1.15.7", ... "provisioningState": "Creating", ... "nodeInitializationTaints": [ "sku=gpu:NoSchedule" ], ... }, ... ]`


## Check that the taint is set on the node

Check the node taints and node initialization taints in the node configuration using the

`kubectl describe node`

command.`kubectl describe node $NODE_NAME`

If you applied node taints, the following example output shows that the

`<node-pool-name>`

node pool has the specified`Taints`

:`[ ... Name: <node-pool-name> ... Taints: sku=gpu:NoSchedule ... ], ... ... ]`


Important

If your nodes are using VMSS, node initialization taints will not be visible on actual nodes in your cluster until an operation that triggers VMSS model update occurs (for example, Kubernetes version upgrade or node image version upgrade).

## Remove node taints

### Remove a specific node taint

Remove node taints using the

command. The following example command removes the`az aks nodepool update`

`"sku=gpu:NoSchedule"`

node taint from the node pool.`az aks nodepool update \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --node-taints ""`


### Remove all node taints

Remove all node taints from a node pool using the

command. The following example command removes all node taints from the node pool.`az aks nodepool update`

`az aks nodepool update \ --cluster-name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --name $NODE_POOL_NAME \ --node-taints ""`


## Remove node initialization taints

You have the following options to remove node initialization taints from the node:

**Remove node initialization taints temporarily**using the Kubernetes API. If you remove them this way, the taints reappear after node scaling or upgrade occurs. New nodes still have the node initialization taint after scaling. Node initialization taints appear on all nodes after upgrading.**Remove node initialization taints permanently**by untainting the node using the Kubernetes API, and then removing the taint using the AKS API. Once the initialization taints are removed from cluster spec using AKS API, newly created nodes after reimage operations no longer have initialization taints.

When you remove all initialization taint occurrences from node pool replicas, the existing initialization taint might reappear after an upgrade with any new initialization taints.

### Remove node initialization taints temporarily

Remove node initialization taints temporarily using the

`kubectl taint nodes`

command.This command removes the taint from only the specified node. If you want to remove the taint from every node in the node pool, you need to run the command for every node that you want the taint removed from.

`kubectl taint nodes $NODE_POOL_NAME sku=gpu:NoSchedule-`

Once removed, node initialization taints reappear after node scaling or upgrading occurs.


### Remove node initialization taints permanently

Follow steps in

[Remove node initialization taints temporarily](#remove-node-initialization-taints-temporarily)to remove the node initialization taint using the Kubernetes API.Remove the taint from the node using the AKS API using the

command. This command removes the node initialization taint from every node in the cluster.`az aks update`

`az aks update \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --node-init-taints ""`


## Check that the taint has been removed from the node

Check the node taints and node initialization taints in the node configuration using the

`kubectl describe node`

command.`kubectl describe node $NODE_NAME`

If you removed a node taint, the following example output shows that the

`<node-pool-name>`

node pool doesn't have the removed taint under`Taints`

:`[ ... Name: <node-pool-name> ... Taints: ... ], ... ... ]`


## Next steps

- Learn more about example use cases for
[taints and tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/#example-use-cases:%7E:text=not%20be%20evicted.-,Example%20Use%20Cases,-Taints%20and%20tolerations). - Learn more about
[best practices for advanced AKS scheduler features](operator-best-practices-advanced-scheduler). - Learn more about Kubernetes labels in the
[Kubernetes labels documentation](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).
