---
merged_at: 2026-01-25T12:25:33.966950
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: configure-aks-scheduler.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/configure-aks-scheduler -->

# Configure advanced scheduler profiles on Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy example scheduler profiles in Azure Kubernetes Service (AKS) to configure advanced scheduling behavior using in-tree scheduling plugins. This guide also explains how to verify the successful application of custom scheduler profiles targeting specific node pools or the entire AKS cluster.

## Limitations

- AKS currently doesn't manage the deployment of third-party schedulers or out-of-tree scheduling plugins.
- AKS doesn't support in-tree scheduling plugins targeting the
`aks-system`

scheduler. This restriction is in place to help prevent unexpected changes to AKS add-ons enabled on your cluster. Additionally, you can't define a`profile`

called`aks-system`

.

## Prerequisites

- The Azure CLI version
`2.76.0`

or later. Run`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - Kubernetes version
`1.33`

or later running on your AKS cluster. - The
version`aks-preview`

Azure CLI extension`18.0.0b27`

or later. [Register the](#register-the-user-defined-scheduler-configuration-preview-feature-flag)in your Azure subscription.`UserDefinedSchedulerConfigurationPreview`

feature flag- Review the
[supported advanced scheduling concepts](concepts-scheduler-configuration)and in-tree scheduling plugins on AKS.

### Install the `aks-preview`

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


### Register the User Defined Scheduler Configuration Preview feature flag

Register the

`UserDefinedSchedulerConfigurationPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "UserDefinedSchedulerConfigurationPreview"`

It takes a few minutes for the status to show

*Registered*.When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace "Microsoft.ContainerService"`


## Enable scheduler profile configuration on an AKS cluster

You can enable schedule profile configuration on a new or existing AKS cluster.

Create an AKS cluster with scheduler profile configuration enabled using the

command with the`az aks create`

`--enable-upstream-kubescheduler-user-configuration`

flag.`# Set environment variables export RESOURCE_GROUP=<resource-group-name> export CLUSTER_NAME=<aks-cluster-name> # Create an AKS cluster with schedule profile configuration enabled az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-upstream-kubescheduler-user-configuration \ --generate-ssh-keys`

Once the creation process completes, connect to the cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Verify installation of the scheduler controller

After enabling the feature on your AKS cluster, verify the custom resource definition (CRD) of the scheduler controller was successfully installed using the

`kubectl get`

command.`kubectl get crd schedulerconfigurations.aks.azure.com`

Note

This command won't succeed if the feature wasn't successfully enabled in the

[previous section](#enable-scheduler-profile-configuration-on-an-aks-cluster).

## Configure node bin-packing

Node bin-packing is a scheduling strategy that maximizes resource utilization by increasing pod density on nodes, within the set configuration. This strategy helps improve cluster efficiency by minimizing wasted resources and lowering the operational cost of maintaining idle or underutilized nodes.

In this example, the configured scheduler prioritizes scheduling pods on nodes with high CPU usage. Explicitly, this configuration avoids underutilizing nodes that still have free resources and helps to make better use of the resources already allocated to nodes. The CRD must be named `upstream`

.

Create a file named

`bin-pack-cpu-scheduler.yaml`

, with the CRD named`upstream`

, and paste in the following manifest:`apiVersion: aks.azure.com/v1alpha1 kind: SchedulerConfiguration metadata: name: upstream spec: rawConfig: | apiVersion: kubescheduler.config.k8s.io/v1 kind: KubeSchedulerConfiguration profiles: - schedulerName: node-binpacking-cpu-scheduler pluginConfig: - name: NodeResourcesFit args: scoringStrategy: type: MostAllocated resources: - name: cpu weight: 1`

`NodeResourcesFit`

ensures that the scheduler checks if a node has enough resources to run the pod.`scoringStrategy: MostAllocated`

tells the scheduler to prefer nodes with high CPU resource usage. This helps achieve**better resource utilization**by placing new pods on nodes that are already "highly used".`Resources`

specifies that`CPU`

is the primary resource being considered for scoring, and with a weight of`1`

, CPU usage is prioritized with a relatively equal level of importance in the scheduling decision.

Apply the scheduling configuration manifest using the

`kubectl apply`

command.`kubectl apply -f bin-pack-cpu-scheduler.yaml`

To target this scheduling mechanism for specific workloads, update your pod deployments with the following

`schedulerName`

:`... ... spec: schedulerName: node-binpacking-cpu-scheduler ... ...`


## Configure pod topology spread

Pod topology spread is a scheduling strategy that seeks to distribute pods evenly across failure domains (such as availability zones or regions) to ensure high availability and fault tolerance in the event of zone or node failures. This strategy helps prevent the risk of all replicas of a pod being placed in the same failure domain. For more configuration guidance, see the [Kubernetes Pod Topology Spread Constraints documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/). The CRD must be named `upstream`

.

Create a file named

`pod-topology-spreader-scheduler.yaml`

, with the CRD named`upstream`

, and paste in the following manifest:`apiVersion: aks.azure.com/v1alpha1 kind: SchedulerConfiguration metadata: name: upstream spec: rawConfig: | apiVersion: kubescheduler.config.k8s.io/v1 kind: KubeSchedulerConfiguration profiles: - schedulerName: pod-distribution-scheduler pluginConfig: - name: PodTopologySpread args: apiVersion: kubescheduler.config.k8s.io/v1 kind: PodTopologySpreadArgs defaultingType: List defaultConstraints: - maxSkew: 1 topologyKey: topology.kubernetes.io/zone whenUnsatisfiable: ScheduleAnyway`

`PodTopologySpread`

plugin instructs the scheduler to try and distribute pods as evenly as possible across availability zones.`whenUnsatisfiable: ScheduleAnyway`

specifies schedule to schedule pods despite the inability to meet the topology constraints. This avoids pod scheduling failures when exact distribution isn't feasible.`List`

type applies the default constraints as a list of rules. The scheduler uses the rules in the order they're defined, and they apply to all pods that don’t specify custom topology spread constraints.`maxSkew: 1`

means the number of pods can differ by at most*1*between any two availability zones.`topologyKey: topology.kubernetes.io/zone`

indicates that the scheduler should spread pods across availability zones.

Apply the scheduling configuration manifest using the

`kubectl apply`

command.`kubectl apply -f pod-topology-spreader-scheduler.yaml`

To target this scheduling mechanism for specific workloads, update your pod deployments with the following

`schedulerName`

:`... ... spec: schedulerName: pod-distribution-scheduler ... ...`


## Assign a scheduler profile to an entire AKS cluster

In your scheduler profile configuration, update the

`schedulerName`

field as follows:`... ... - schedulerName: default_scheduler ... ...`

Reapply the manifest using the

`kubectl apply`

command.`kubectl apply -f aks-scheduler-customization.yaml`

Now, this configuration will become the

**default**scheduling operation for your entire AKS cluster.

## Configure multiple scheduler profiles

You can customize the upstream scheduler with multiple profiles and customize each profile with multiple plugins while using the same configuration file. As a reminder, the CRD must be named `upstream`

and user-configured fields include `percentageOfNodesToScore`

, `podInitialBackoffSeconds`

, `podMaxBackoffSeconds`

, and `profiles`

.

In the following example, we create two scheduling profiles called **scheduler-one** and **scheduler-two**. The fields `percentageOfNodesToScore`

, `podInitialBackoffSeconds`

, `podMaxBackoffSeconds`

, apply globally to all profiles defined.

**global parameters**

`percentageOfNodesToScore`

specifies the percentage of cluster nodes the scheduler evaluates during scoring to balance scheduling accuracy and speed. So**percentageOfNodesToScore: 40**means the scheduler will sample 40% of nodes instead of the entire cluster.`podInitialBackoffSeconds`

defines the initial delay before retrying a failed scheduling attempt to prevent rapid, repeated retries. So**podInitialBackoffSeconds: 1**means the scheduler waits 1 second before the first retry.`podMaxBackoffSeconds`

sets the maximum delay the scheduler will wait between exponential backoff retries for unschedulable pods. So**podMaxBackoffSeconds: 8**means the retry delay will never exceed 8 seconds even as backoff increases.

**scheduler-one** prioritizes placing pods across zones and nodes for balanced distribution with the following settings:

- Enforces strict zonal distribution and
*preferred*node distribution using`PodTopologySpread`

. - Honors hard pod affinity rules and considers the soft affinity rules with
`InterPodAffinity`

. *Prefers*nodes in specific zones to reduce cross-zone networking using`NodeAffinity`

.

**scheduler-two** prioritizes placing pods on nodes with available storage, CPU, and memory resources for timely resource-efficient resource usage with the following settings:

- Ensures pods are placed on nodes where PVCs can bind to PVs using
`VolumeBinding`

. - Validates that nodes and volumes satisfy zonal requirements using
`VolumeZone`

to avoid cross-zone storage access. - Prioritizes nodes based on CPU, memory, and ephemeral storage utilization, with
`NodeResourcesFit`

. - Favors nodes that already have the required container images using
`ImageLocality`

.

Note

You might need to adjust zones and other parameters based on your workload type.

Create a file named

`aks-scheduler-customization.yaml`

, with the CRD named`upstream`

, and paste in the following manifest:`apiVersion: aks.azure.com/v1alpha1 kind: SchedulerConfiguration metadata: name: upstream spec: rawConfig: | apiVersion: kubescheduler.config.k8s.io/v1 kind: KubeSchedulerConfiguration percentageOfNodesToScore: 40 podInitialBackoffSeconds: 1 podMaxBackoffSeconds: 8 profiles: - schedulerName: scheduler-one plugins: multiPoint: enabled: - name: PodTopologySpread - name: InterPodAffinity - name: NodeAffinity pluginConfig: # PodTopologySpread with strict zonal distribution - name: PodTopologySpread args: defaultingType: List defaultConstraints: - maxSkew: 2 topologyKey: topology.kubernetes.io/zone whenUnsatisfiable: DoNotSchedule - maxSkew: 1 topologyKey: kubernetes.io/hostname whenUnsatisfiable: ScheduleAnyway - name: InterPodAffinity args: hardPodAffinityWeight: 1 ignorePreferredTermsOfExistingPods: false - name: NodeAffinity args: addedAffinity: preferredDuringSchedulingIgnoredDuringExecution: - weight: 100 preference: matchExpressions: - key: topology.kubernetes.io/zone operator: In values: [westus3-1, westus3-2, westus3-3] - schedulerName: scheduler-two plugins: multiPoint: enabled: - name: VolumeBinding - name: VolumeZone - name: NodeAffinity - name: NodeResourcesFit - name: PodTopologySpread - name: ImageLocality pluginConfig: - name: PodTopologySpread args: defaultingType: List defaultConstraints: - maxSkew: 1 topologyKey: kubernetes.io/hostname whenUnsatisfiable: DoNotSchedule - name: VolumeBinding args: apiVersion: kubescheduler.config.k8s.io/v1 kind: VolumeBindingArgs bindTimeoutSeconds: 300 - name: NodeAffinity args: apiVersion: kubescheduler.config.k8s.io/v1 kind: NodeAffinityArgs addedAffinity: preferredDuringSchedulingIgnoredDuringExecution: - weight: 100 preference: matchExpressions: - key: topology.kubernetes.io/zone operator: In values: [westus3-1, westus3-2] - name: NodeResourcesFit args: apiVersion: kubescheduler.config.k8s.io/v1 kind: NodeResourcesFitArgs scoringStrategy: type: MostAllocated resources: - name: cpu weight: 3 - name: memory weight: 1 - name: ephemeral-storage weight: 2`

Apply the manifest using the

`kubectl apply`

command.`kubectl apply -f aks-scheduler-customization.yaml`


## Disable an AKS scheduler profile configuration

To disable the AKS scheduler profile configuration and revert to AKS scheduler default configuration on the cluster, first delete the

`schedulerconfiguration`

resource using the`kubectl delete`

command.`kubectl delete schedulerconfiguration upstream || true`

Note

Ensure that the previous step is complete and confirm that the

`schedulerconfiguration`

resource was deleted before proceeding to disable this feature.Disable the feature using the

command with the`az aks update`

`--disable-upstream-kubescheduler-user-configuration`

flag.`az aks update --subscription="${SUBSCRIPTION_ID}" \ --resource-group="${RESOURCE_GROUP}" \ --name="${CLUSTER_NAME}" \ --disable-upstream-kubescheduler-user-configuration`

Verify the feature is disabled using the

command.`az aks show`

`az aks show --resource-group="${RESOURCE_GROUP}" \ --name="${CLUSTER_NAME}" \ --query='properties.schedulerProfile'`

Your output should indicate that the feature is no longer enabled on your AKS cluster.


## Frequently asked questions (FAQ)

### What happens if I apply misconfigured scheduler profile to my AKS cluster?

Once you apply a scheduler profile, AKS checks if it contains a valid configuration of plugins and arguments. If the configuration targets a disallowed scheduler or sets the in-tree scheduling plugins improperly, AKS rejects the configuration and reverts to the last known "accepted" scheduler configuration. This check aims to limit impact on new and existing AKS clusters due to scheduler misconfiguration.

### How can I monitor and validate that the scheduler honored my configuration?

There are *three* recommended methods for observing the results of your applied scheduler profile:

- View the AKS
`kube-scheduler`

control plane logs to ensure that the scheduler received the configuration from the CRD. - Run the
`kubectl get schedulerconfiguration`

command. The output displays the status of the`configuration: pending`

during the rollout and`Succeeded`

or`Failed`

after the configuration is accepted or rejected by the scheduler. - Run the
`kubectl describe schedulerconfiguration`

command. The output displays a more detailed state of the scheduler, including any error during the reconciliation, and the current scheduler configuration in effect.

## Next steps

To learn more about the AKS scheduler and best practices, see the following resources:


---

<!-- DOCUMENTO FUSIONADO: azure-ad-integration-cli.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-ad-integration-cli -->

# Integrate Microsoft Entra ID with Azure Kubernetes Service (AKS) using the Azure CLI (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Warning

The feature described in this document, Microsoft Entra Integration (legacy) was **deprecated on June 1st, 2023**. At this time, no new clusters can be created with Microsoft Entra Integration (legacy).

AKS has a new improved [AKS-managed Microsoft Entra ID](managed-azure-ad) experience that doesn't require you to manage server or client applications. If you want to migrate follow the instructions [here](managed-azure-ad#migrate-a-legacy-azure-ad-cluster-to-integration).

Azure Kubernetes Service (AKS) can be configured to use Microsoft Entra ID for user authentication. In this configuration, you can log into an AKS cluster using a Microsoft Entra authentication token. Cluster operators can also configure Kubernetes role-based access control (Kubernetes RBAC) based on a user's identity or directory group membership.

This article shows you how to create the required Microsoft Entra components, then deploy a Microsoft Entra ID-enabled cluster and create a basic Kubernetes role in the AKS cluster.

## Limitations

- Microsoft Entra ID can only be enabled on Kubernetes RBAC-enabled cluster.
- Microsoft Entra legacy integration can only be enabled during cluster creation.

## Before you begin

You need the Azure CLI version 2.0.61 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Go to [https://shell.azure.com](https://shell.azure.com) to open Cloud Shell in your browser.

For consistency and to help run the commands in this article, create a variable for your desired AKS cluster name. The following example uses the name *myakscluster*:

```
aksname="myakscluster"
```


## Microsoft Entra authentication overview

Microsoft Entra authentication is provided to AKS clusters with OpenID Connect. OpenID Connect is an identity layer built on top of the OAuth 2.0 protocol. For more information on OpenID Connect, see the [OpenID Connect documentation](/en-us/azure/active-directory/develop/v2-protocols-oidc).

From inside of the Kubernetes cluster, Webhook Token Authentication is used to verify authentication tokens. Webhook token authentication is configured and managed as part of the AKS cluster. For more information on Webhook token authentication, see the [webhook authentication documentation](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#webhook-token-authentication).

Note

When configuring Microsoft Entra ID for AKS authentication, two Microsoft Entra applications are configured. This operation must be completed by an Azure tenant administrator.

## Create Microsoft Entra server component

To integrate with AKS, you create and use a Microsoft Entra application that acts as an endpoint for the identity requests. The first Microsoft Entra application you need gets Microsoft Entra group membership for a user.

Create the server application component using the [az ad app create](/en-us/cli/azure/ad/app#az-ad-app-create) command, then update the group membership claims using the [az ad app update](/en-us/cli/azure/ad/app#az-ad-app-update) command. The following example uses the *aksname* variable defined in the [Before you begin](#before-you-begin) section, and creates a variable

```
# Create the Azure AD application
serverApplicationId=$(az ad app create \
--display-name "${aksname}Server" \
--identifier-uris "https://${aksname}Server" \
--query appId -o tsv)
# Update the application group membership claims
az ad app update --id $serverApplicationId --set groupMembershipClaims=All
```


Now create a service principal for the server app using the [az ad sp create](/en-us/cli/azure/ad/sp#az-ad-sp-create) command. This service principal is used to authenticate itself within the Azure platform. Then, get the service principal secret using the [az ad sp credential reset](/en-us/cli/azure/ad/sp/credential#az-ad-sp-credential-reset) command and assign to the variable named *serverApplicationSecret* for use in one of the following steps:

```
# Create a service principal for the Azure AD application
az ad sp create --id $serverApplicationId
# Get the service principal secret
serverApplicationSecret=$(az ad sp credential reset \
--name $serverApplicationId \
--credential-description "AKSPassword" \
--query password -o tsv)
```


The Microsoft Entra service principal needs permissions to perform the following actions:

- Read directory data
- Sign in and read user profile

Assign these permissions using the [az ad app permission add](/en-us/cli/azure/ad/app/permission#az-ad-app-permission-add) command:

```
az ad app permission add \
--id $serverApplicationId \
--api 00000003-0000-0000-c000-000000000000 \
--api-permissions e1fe6dd8-ba31-4d61-89e7-88639da4683d=Scope 06da0dbc-49e2-44d2-8312-53f166ab848a=Scope 7ab1d382-f21e-4acd-a863-ba3e13f7da61=Role
```


Finally, grant the permissions assigned in the previous step for the server application using the [az ad app permission grant](/en-us/cli/azure/ad/app/permission#az-ad-app-permission-grant) command. This step fails if the current account is not a tenant admin. You also need to add permissions for Microsoft Entra application to request information that may otherwise require administrative consent using the [az ad app permission admin-consent](/en-us/cli/azure/ad/app/permission#az-ad-app-permission-admin-consent):

```
az ad app permission grant --id $serverApplicationId --api 00000003-0000-0000-c000-000000000000
az ad app permission admin-consent --id $serverApplicationId
```


## Create Microsoft Entra client component

The second Microsoft Entra application is used when a user logs to the AKS cluster with the Kubernetes CLI (`kubectl`

). This client application takes the authentication request from the user and verifies their credentials and permissions. Create the Microsoft Entra app for the client component using the [az ad app create](/en-us/cli/azure/ad/app#az-ad-app-create) command:

```
clientApplicationId=$(az ad app create \
--display-name "${aksname}Client" \
--native-app \
--reply-urls "https://${aksname}Client" \
--query appId -o tsv)
```


Create a service principal for the client application using the [az ad sp create](/en-us/cli/azure/ad/sp#az-ad-sp-create) command:

```
az ad sp create --id $clientApplicationId
```


Get the oAuth2 ID for the server app to allow the authentication flow between the two app components using the [az ad app show](/en-us/cli/azure/ad/app#az-ad-app-show) command. This oAuth2 ID is used in the next step.

```
oAuthPermissionId=$(az ad app show --id $serverApplicationId --query "oauth2Permissions[0].id" -o tsv)
```


Add the permissions for the client application and server application components to use the oAuth2 communication flow using the [az ad app permission add](/en-us/cli/azure/ad/app/permission#az-ad-app-permission-add) command. Then, grant permissions for the client application to communication with the server application using the [az ad app permission grant](/en-us/cli/azure/ad/app/permission#az-ad-app-permission-grant) command:

```
az ad app permission add --id $clientApplicationId --api $serverApplicationId --api-permissions ${oAuthPermissionId}=Scope
az ad app permission grant --id $clientApplicationId --api $serverApplicationId
```


## Deploy the cluster

With the two Microsoft Entra applications created, now create the AKS cluster itself. First, create a resource group using the [az group create](/en-us/cli/azure/group#az-group-create) command. The following example creates the resource group in the *EastUS* region:

Create a resource group for the cluster:

```
az group create --name myResourceGroup --location EastUS
```


Get the tenant ID of your Azure subscription using the [az account show](/en-us/cli/azure/account#az-account-show) command. Then, create the AKS cluster using the [az aks create](/en-us/cli/azure/aks#az-aks-create) command. The command to create the AKS cluster provides the server and client application IDs, the server application service principal secret, and your tenant ID:

```
tenantId=$(az account show --query tenantId -o tsv)
az aks create \
--resource-group myResourceGroup \
--name $aksname \
--node-count 1 \
--generate-ssh-keys \
--aad-server-app-id $serverApplicationId \
--aad-server-app-secret $serverApplicationSecret \
--aad-client-app-id $clientApplicationId \
--aad-tenant-id $tenantId
```


Finally, get the cluster admin credentials using the [az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. In one of the following steps, you get the regular *user* cluster credentials to see the Microsoft Entra authentication flow in action.

```
az aks get-credentials --resource-group myResourceGroup --name $aksname --admin
```


## Create Kubernetes RBAC binding

Before a Microsoft Entra account can be used with the AKS cluster, a role binding or cluster role binding needs to be created. *Roles* define the permissions to grant, and *bindings* apply them to desired users. These assignments can be applied to a given namespace, or across the entire cluster. For more information, see [Using Kubernetes RBAC authorization](concepts-identity#kubernetes-rbac).

Get the user principal name (UPN) for the user currently logged in using the [az ad signed-in-user show](/en-us/cli/azure/ad/signed-in-user#az-ad-signed-in-user-show) command. This user account is enabled for Microsoft Entra integration in the next step.

```
az ad signed-in-user show --query userPrincipalName -o tsv
```


Important

If the user you grant the Kubernetes RBAC binding for is in the same Microsoft Entra tenant, assign permissions based on the *userPrincipalName*. If the user is in a different Microsoft Entra tenant, query for and use the *objectId* property instead.

Create a YAML manifest named `basic-azure-ad-binding.yaml`

and paste the following contents. On the last line, replace *userPrincipalName_or_objectId* with the UPN or object ID output from the previous command:

```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
name: contoso-cluster-admins
roleRef:
apiGroup: rbac.authorization.k8s.io
kind: ClusterRole
name: cluster-admin
subjects:
- apiGroup: rbac.authorization.k8s.io
kind: User
name: userPrincipalName_or_objectId
```


Create the ClusterRoleBinding using the [kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply) command and specify the filename of your YAML manifest:

```
kubectl apply -f basic-azure-ad-binding.yaml
```


## Access cluster with Microsoft Entra ID

Now let's test the integration of Microsoft Entra authentication for the AKS cluster. Set the `kubectl`

config context to use regular user credentials. This context passes all authentication requests back through Microsoft Entra ID.

```
az aks get-credentials --resource-group myResourceGroup --name $aksname --overwrite-existing
```


Now use the [kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command to view pods across all namespaces:

```
kubectl get pods --all-namespaces
```


You receive a sign in prompt to authenticate using Microsoft Entra credentials using a web browser. After you've successfully authenticated, the `kubectl`

command displays the pods in the AKS cluster, as shown in the following example output:

```
kubectl get pods --all-namespaces
```


```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code BYMK7UXVD to authenticate.
NAMESPACE NAME READY STATUS RESTARTS AGE
kube-system coredns-754f947b4-2v75r 1/1 Running 0 23h
kube-system coredns-754f947b4-tghwh 1/1 Running 0 23h
kube-system coredns-autoscaler-6fcdb7d64-4wkvp 1/1 Running 0 23h
kube-system heapster-5fb7488d97-t5wzk 2/2 Running 0 23h
kube-system kube-proxy-2nd5m 1/1 Running 0 23h
kube-system kube-svc-redirect-swp9r 2/2 Running 0 23h
kube-system kubernetes-dashboard-847bb4ddc6-trt7m 1/1 Running 0 23h
kube-system metrics-server-7b97f9cd9-btxzz 1/1 Running 0 23h
kube-system tunnelfront-6ff887cffb-xkfmq 1/1 Running 0 23h
```


The authentication token received for `kubectl`

is cached. You are only reprompted to sign in when the token has expired or the Kubernetes config file is re-created.

If you see an authorization error message after you've successfully signed in using a web browser as in the following example output, check the following possible issues:

```
error: You must be logged in to the server (Unauthorized)
```


- You defined the appropriate object ID or UPN, depending on if the user account is in the same Microsoft Entra tenant or not.
- The user is not a member of more than 200 groups.
- Secret defined in the application registration for server matches the value configured using
`--aad-server-app-secret`

- Be sure that only one version of kubectl is installed on your machine at a time. Conflicting versions can cause issues during authorization. To install the latest version, use
[az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli).

## Frequently asked questions about migration from Microsoft Entra Integration to AKS-managed Microsoft Entra ID

**1. What is the plan for migration?**

Microsoft Entra Integration (legacy) will be deprecated on 1st June 2023. After this date, you won't be able to create new clusters with Microsoft Entra ID (legacy). We'll migrate all Microsoft Entra Integration (legacy) AKS clusters to AKS-managed Microsoft Entra ID automatically starting from 1st August 2023. We send notification emails to impacted subscription admins biweekly to remind them of migration.

**2. What will happen if I don't take any action?**

Your Microsoft Entra Integration (legacy) AKS clusters will continue working after 1st June 2023. We'll automatically migrate your clusters to AKS-managed Microsoft Entra ID starting from 1st August 2023. You may experience API server downtime during the migration.

The kubeconfig content changes after the migration. You need to merge the new credentials into the kubeconfig file using the `az aks get-credentials --resource-group <AKS resource group name> --name <AKS cluster name>`

.

We recommend updating your AKS cluster to [AKS-managed Microsoft Entra ID](managed-azure-ad#migrate-a-legacy-azure-ad-cluster-to-integration) manually before 1st August. This way you can manage the downtime during non-business hours when it's more convenient.

**3. Why do I still receive the notification email after manual migration?**

It takes several days for the email to send. If your cluster wasn't migrated before we initiate the email-sending process, you may still receive a notification.

**4. How can I check whether my cluster my cluster is migrated to AKS-managed Microsoft Entra ID?**

Confirm your AKS cluster is migrated to the AKS-managed Microsoft Entra ID using the [ az aks show](/en-us/cli/azure/aks#az-aks-show) command.

```
az aks show -g <RGName> -n <ClusterName> --query "aadProfile"
```


If your cluster is using the AKS-managed Microsoft Entra ID, the output shows `managed`

is `true`

. For example:

```
{
"adminGroupObjectIDs": [
"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
],
"adminUsers": null,
"clientAppId": null,
"enableAzureRbac": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
```


## Next steps

For the complete script that contains the commands shown in this article, see the [Microsoft Entra integration script in the AKS samples repo][complete-script].

To use Microsoft Entra users and groups to control access to cluster resources, see [Control access to cluster resources using Kubernetes role-based access control and Microsoft Entra identities in AKS](azure-ad-rbac).

For more information about how to secure Kubernetes clusters, see [Access and identity options for AKS)](concepts-identity#kubernetes-rbac).

For best practices on identity and resource control, see [Best practices for authentication and authorization in AKS](operator-best-practices-identity).
