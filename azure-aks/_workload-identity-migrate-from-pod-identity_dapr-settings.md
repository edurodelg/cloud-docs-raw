---
merged_at: 2026-01-25T12:25:33.959486
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

<!-- DOCUMENTO FUSIONADO: dapr-settings.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/dapr-settings -->

# Configure the Dapr extension for your Azure Kubernetes Service (AKS) and Arc-enabled Kubernetes project

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

After [completing the prerequisites for installing the Dapr extension](dapr), you can configure the [Dapr](https://dapr.io/) extension to work best for you and your project using various configuration options, like:

- Rotating expiring certificates
- Provisioning Dapr with high availability (HA) enabled
- Limiting which of your nodes use the Dapr extension
- Setting automatic custom resource definition (CRD) updates
- Configuring the Dapr release namespace

The extension enables you to set Dapr configuration options by using the `--configuration-settings`

parameter in the Azure CLI or `configurationSettings`

property in a Bicep template.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Update configuration settings

Important

Some configuration options cannot be modified post-creation. Adjustments to these options require deletion and recreation of the extension, applicable to the following settings:

`global.ha.*`

`dapr_placement.*`


HA is enabled by default. Disabling it requires deletion and recreation of the extension.

To update your Dapr configuration settings, recreate the extension with the desired state. For example, let's say you previously created and installed the extension using the following configuration:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2"
```


To update the `dapr_operator.replicaCount`

from two to three, use the following command:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=3"
```


## Manage mTLS certificates

The Dapr extension supports in-transit encryption of communication between Dapr instances using the Dapr Sentry service control plane, which is a central Certificate Authority (CA). With the Sentry service, you can encrypt communication using self-signed or user-supplied x.509 certificates. [Learn more about setting up mTLS certificates in the open-source Dapr documentation.](https://docs.dapr.io/operations/security/mtls/#dapr-generated-self-signed-certificates)

You can [bring in your own certificates](https://docs.dapr.io/operations/security/mtls/#bringing-your-own-certificates), or let [Dapr automatically create and persist self-signed root and issuer certificates](https://docs.dapr.io/operations/security/mtls/#dapr-generated-self-signed-certificates).

Important

If you don't explicitly configure certificates, [Dapr defaults to generating self-signed certificates](#manage-dapr-generated-self-signed-certificates), which are generally valid for 1 year. **Currently, using self-signed certificates generated by Dapr is not recommended.** Best practice is to generate custom certificates and update them manually.

### Manage Dapr-generated self-signed certificates

If you haven't provided any custom certificates, Dapr automatically creates and persists self-signed certificates, valid for 1 year. The Dapr extension installs the `dapr-trust-bundle`

secret, which contains certificate information under the default `dapr-system`

namespace.

#### Check expiry of current Dapr-generated self-signed certificates

You can check when the Dapr root certificate of your Kubernetes cluster expires by using [the Dapr CLI](https://docs.dapr.io/getting-started/install-dapr-cli/).

```
dapr mtls expiry
```


**Expected output:**

```
Root certificate expires in 8759 hours. Expiry date: 2025-12-06 18:14:20 +0000 UTC
```


You can also find the expiration date for your current certificate in the Kubernetes `dapr-trust-bundle`

secret data.

```
kubectl get secret dapr-trust-bundle -n dapr-system -o jsonpath='{.data.issuer\.crt}' | base64 -d | openssl x509 -noout -dates
```


**Expected output:**

```
notBefore=Dec 6 17:59:20 2024 GMT
notAfter=Dec 6 18:14:20 2025 GMT
```


#### Generate a new Dapr-generated self-signed certificate

**Via the Dapr CLI (recommended)**

Refer to Dapr's[Root and issuer certificate upgrade using CLI](https://docs.dapr.io/operations/security/mtls/#root-and-issuer-certificate-upgrade-using-cli-recommended)guide.**Via**Refer to Dapr's`kubectl`

commands[Updating root or issuer certs using Kubectl](https://docs.dapr.io/operations/security/mtls/#updating-root-or-issuer-certs-using-kubectl)guide.

### Manage your own user-supplied x.509 certificates

You can also bring your own custom certificates.

**Generate custom certificates**

Create your own custom certificate; for example,[an Azure Key Vault certificate](/en-us/azure/key-vault/certificates/certificate-scenarios).**Update your custom certficate manually**

Follow[the instructions provided in the Dapr open source documentation to update your custom certificates manually](https://docs.dapr.io/operations/security/mtls/#custom-certificates-bring-your-own)using.`kubectl`


## Provision Dapr with high availability (HA) enabled

Provision Dapr with high availability (HA) enabled by setting the `global.ha.enabled`

parameter to `true`

.

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2"
```


Note

If configuration settings are sensitive and need to be protected (for example, cert-related information), pass the `--configuration-protected-settings`

parameter and the value will be protected from being read.

If no configuration-settings are passed, the Dapr configuration defaults to:

```
ha:
enabled: true
replicaCount: 3
disruption:
minimumAvailable: ""
maximumUnavailable: "25%"
prometheus:
enabled: true
port: 9090
mtls:
enabled: true
workloadCertTTL: 24h
allowedClockSkew: 15m
```


For a list of available options, see [Dapr configuration](https://github.com/dapr/dapr/blob/master/charts/dapr/README.md#configuration).

## Limit the extension to certain nodes

In some configurations, you may only want to run Dapr on certain nodes. You can limit the extension by passing a `nodeSelector`

in the extension configuration. If the desired `nodeSelector`

contains `.`

, you must escape them from the shell and the extension. For example, the following configuration installs Dapr only to nodes with `topology.kubernetes.io/zone: "us-east-1c"`

:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2" \
--configuration-settings "global.nodeSelector.kubernetes\.io/zone=us-east-1c"
```


For managing OS and architecture, use the [supported versions](https://github.com/dapr/dapr/blob/b8ae13bf3f0a84c25051fcdacbfd8ac8e32695df/docker/docker.mk#L50) of the `global.daprControlPlaneOs`

and `global.daprControlPlaneArch`

configuration:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2" \
--configuration-settings "global.daprControlPlaneOs=linux" \
--configuration-settings "global.daprControlPlaneArch=amd64"
```


## Install Dapr in multiple availability zones while in HA mode

By default, the placement service uses a storage class of type `standard_LRS`

. It's recommended to create a **zone redundant storage class** while installing Dapr in HA mode across multiple availability zones. For example, to create a `zrs`

type storage class, add the `storageaccounttype`

parameter:

```
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
name: custom-zone-redundant-storage
provisioner: disk.csi.azure.com
reclaimPolicy: Delete
allowVolumeExpansion: true
volumeBindingMode: WaitForFirstConsumer
parameters:
storageaccounttype: Premium_ZRS
```


When installing Dapr, use the storage class you used in the YAML file:

```
az k8s-extension create --cluster-type managedClusters
--cluster-name XXX
--resource-group XXX
--name XXX
--extension-type Microsoft.Dapr
--auto-upgrade-minor-version XXX
--version XXX
--configuration-settings "dapr_placement.volumeclaims.storageClassName=custom-zone-redundant-storage"
```


## Configure the Dapr release namespace

You can configure the release namespace.

The Dapr extension gets installed in the `dapr-system`

namespace by default. To override it, use `--release-namespace`

. To redefine the namespace, include the cluster `--scope`

.

```
az k8s-extension create \
--cluster-type managedClusters \
--cluster-name dapr-aks \
--resource-group dapr-rg \
--name my-dapr-ext \
--extension-type microsoft.dapr \
--release-train stable \
--auto-upgrade false \
--version 1.9.2 \
--scope cluster \
--release-namespace dapr-custom
```


## Show current configuration settings

Use the `az k8s-extension show`

command to show the current Dapr configuration settings:

```
az k8s-extension show --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr
```


## Set Dapr monitoring log levels

You can configure settings for the Dapr monitoring component with your AKS cluster extension. For exmaple, to update `dapr_monitoring`

log levels to "warn" (only notified when receiving a warning or error), set the following `configuration-settings`

:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_monitoring.logLevel=warn"
```


## Set the outbound proxy for Dapr extension for Azure Arc on-premises

If you want to use an outbound proxy with the Dapr extension for AKS, you can do so by:

- Setting the proxy environment variables using the
:`dapr.io/env`

annotations`HTTP_PROXY`

`HTTPS_PROXY`

`NO_PROXY`


[Installing the proxy certificate in the sidecar](https://docs.dapr.io/operations/configuration/install-certificates/).

## Updating your Dapr installation version

If you are on a specific Dapr version and you don't have `--auto-upgrade-minor-version`

available, you can use the following command to upgrade or downgrade Dapr:

```
az k8s-extension update --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--version 1.12.0 # Version to upgrade or downgrade to
```


The preceding command updates the Dapr control plane *only.* To update the Dapr sidecars, restart your application deployments:

```
kubectl rollout restart deploy/<DEPLOYMENT-NAME>
```


## Using Azure Linux-based images

From Dapr version 1.8.0, you can use Azure Linux images with the Dapr extension. To use them, set the `global.tag`

flag:

```
az k8s-extension update --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--set global.tag=1.10.0-mariner
```


[Learn more about using Mariner-based images with Dapr](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-deploy/#using-mariner-based-images).[Learn more about deploying Azure Linux on AKS](cluster-configuration#azure-linux-container-host-for-aks).

## Disable automatic CRD updates

From Dapr version 1.9.2, CRDs are automatically upgraded when the extension upgrades. To disable this setting, you can set `hooks.applyCrds`

to `false`

.

```
az k8s-extension update --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--configuration-settings "hooks.applyCrds=false"
```


Note

CRDs are only applied in case of upgrades and are skipped during downgrades.

## Meet network requirements

The Dapr extension requires the following outbound URLs on `https://:443`

to function on AKS and Arc for Kubernetes:

`https://mcr.microsoft.com/daprio`

URL for pulling Dapr artifacts.- The
[outbound URLs required for AKS or Arc for Kubernetes](/en-us/azure/azure-arc/kubernetes/network-requirements).
