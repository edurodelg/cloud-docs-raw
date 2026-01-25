---
merged_at: 2026-01-25T12:25:33.956186
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: optimized-addon-scaling.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/optimized-addon-scaling -->

# Enable cost optimized add-on scaling on your Azure Kubernetes Service (AKS) cluster (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of cost optimized add-on scaling in Azure Kubernetes Service (AKS). With cost-optimized add-on scaling, you can manage add-ons that require custom CPU and memory by overriding default configurations or enabling autoscaling. This feature ensures that resources aren't overly allocated to add-on pods, improving cost savings and cluster efficiency.

## Overview

Enabling cost optimized add-on scaling installs the [Vertical Pod Autoscaler (VPA)add-on](vertical-pod-autoscaler), allowing supported add-ons to autoscale based on usage.

This feature also allows you to customize the resource's default CPU/ memory requests and limits in Deployments and DaemonSets, the maximum and minimum allowed CPU/ memory, and the VPA update mode within VPA custom resources. For more information, see [customize the resource configuration for AKS add-ons](customize-resource-configuration).

### Supported AKS add-ons

The following AKS managed add-ons support the cost optimized add-on scaling feature:

| Add-on | Enablement behavior | VPA custom resource name | Command to check VPA custom resource |
|---|---|---|---|
|

`coredns`

`kubectl get vpa coredns --namespace kube-system`

[Workload identity](workload-identity-deploy-cluster)`azure-wi-webhook-controller-manager`

`kubectl get vpa azure-wi-webhook-controller-manager --namespace kube-system`

[Image Integrity](image-integrity)`ratify`

`kubectl get vpa ratify --namespace gatekeeper-system`

[Network Observability (Retina)](container-network-observability-how-to)`retina-agent`

and `retina-operator`

`kubectl get vpa retina-agent --namespace kube-system`

and `kubectl get vpa retina-operator --namespace kube-system`

### Supported VPA modes for cost optimized add-on scaling

VPA currently supports the following modes for cost optimized add-on scaling:

*Off*: The VPA provides resource recommendation data but doesn't apply it to the target pod.*Initial*(default mode): The VPA automatically applies CPU and memory recommendations to the target pod when it restarts, but it doesn't initiate the restart itself.*Auto*: The VPA automatically updates CPU and memory requests for pods based on recommendations.

Note

When enabling cost optimized add-on scaling, consider the following information:

- If you delete the Deployment, DaemonSet, or VPA custom resource, the changes revert back to the AKS add-on's initial configuration.
- The cost optimized add-on scaling feature enables the
[VPA add-on](vertical-pod-autoscaler)to autoscale the supported AKS add-ons. It doesn't work with self-hosted VPA. - AKS restarts the add-on pods when enabling cost optimized add-on scaling. CoreDNS is currently the only exception to avoid potential disruptions during the restart. For more information, see
[CoreDNS autoscaling behavior](coredns-autoscale).

Warning

Make sure you have enough compute resources on the system node pool for your addons when you enable cost optimized add-on scaling. AKS recommends turning on the [cluster autoscaler](cluster-autoscaler-overview) or [node autoprovision](node-autoprovision) to ensure right-sizing of your compute resources automatically.
Monitor for pending add-on pods when using the cost-optimized add-on scaling feature. VPA might recommend resource requests that exceed available node capacity, potentially leading to unschedulable pods. You can control this behavior by [customizing min/max values](customize-resource-configuration) for requests and limits of supported addons.

## Prerequisites

- An AKS cluster running Kubernetes version 1.25 or later.
- The Azure CLI version 2.60.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). [Install the](#install-the-aks-preview-azure-cli-extension)and`aks-preview`

Azure CLI extension[register the cost optimized add-on scaling preview feature](#register-the-cost-optimized-add-on-scaling-preview-feature).

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Install the `aks-preview`

Azure CLI extension

Install the

`aks-preview`

extension using the`az extension add`

command.`az extension add --name aks-preview`

Update to the latest version of the extension using the

`az extension update`

command.`az extension update --name aks-preview`


### Register the cost optimized add-on scaling preview feature

Register the cost optimized add-on scaling preview feature using the

`az feature register`

command.`az feature register --namespace "Microsoft.ContainerService" --name "AKS-AddonAutoscalingPreview"`

It takes a few minutes for the status to show as

*Registered*.Verify the registration status using the

`az feature show`

command.`az feature show --namespace "Microsoft.ContainerService" --name "AKS-AddonAutoscalingPreview"`

When the status shows as

*Registered*, refresh the registration of the Microsoft.ContainerService provider using the`az provider register`

command.`az provider register --namespace Microsoft.ContainerService`


## Enable cost optimized add-on scaling on an AKS cluster

When enabling the add-on, the AKS cluster automatically installs the [VPA add-on](vertical-pod-autoscaler). The [AKS add-ons that support the cost optimized add-on scaling feature](#supported-aks-add-ons) have different enablement behavior.

Note

If you're using Bicep, ARM templates, or Terraform, set `VerticalPodAutoscaler`

to `"True"`

and `AddonAutoscaling`

to `"enabled"`

.

### Enable cost optimized add-on scaling on a new cluster

Enable cost optimized add-on scaling on a new AKS cluster using the

command with the`az aks create`

`--enable-optimized-addon-scaling`

flag.`az aks create --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --enable-optimized-addon-scaling`


### Enable cost optimized add-on scaling on an existing cluster

Enable cost optimized add-on scaling on an existing AKS cluster using the

command with the`az aks update`

`--enable-optimized-addon-scaling`

flag.`az aks update --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --enable-optimized-addon-scaling`


## Disable cost optimized add-on scaling on an AKS cluster

Disable cost optimized add-on scaling on an AKS cluster using the

command with the`az aks update`

`--disable-optimized-addon-scaling`

flag.`az aks update --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME --disable-optimized-addon-scaling`


Note

Disabling the cost optimized add-on scaling feature doesn't disable the VPA add-on by default. To disable VPA, see [Disable VPA on an AKS cluster](use-vertical-pod-autoscaler#disable-the-vertical-pod-autoscaler-on-an-existing-cluster).

## Customize default resource configuration

With the cost optimized add-on scaling feature enabled on your cluster, you can customize the default CPU/memory settings for the add-on resources as well as the default VPA configuration for supported AKS add-ons. For more information, see [customize the resource configuration for AKS add-ons](customize-resource-configuration).

## Applying the VPA recommended values manually

Note

With *Initial* mode, the VPA applies the recommended CPU and memory requests only when a pod is created or updated. If you want the recommendations to take effect immediately, please update the pods manually. Before manually applying the recommended values, [make sure the VPA update mode is set to Initial or Auto in the VPA custom resource](customize-resource-configuration#customize-resource-update-mode).

Check the pod status and CPU/memory utilization to verify that the pod is running as expected.

The following example uses the

`kubectl get pod`

command to check a CoreDNS pod status:`kubectl get pod <coredns-pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a CoreDNS pod:

`apiVersion: v1 kind: Pod metadata: name: <coredns-pod-name> namespace: kube-system spec: ... containers: - name: coredns resources: limits: cpu: "3" memory: "500Mi" requests: cpu: "100m" memory: "70Mi"`

Get the VPA recommended value using the

`kubectl get vpa`

command.`kubectl get vpa coredns --namespace kube-system`

The following output shows an example of the VPA recommended value for a CoreDNS pod:

`NAME MODE CPU MEM PROVIDED AGE coredns Initial 11m 23574998 True 44m`

If you want to use the values recommended by VPA, manually delete the pod using the

`kubectl delete pod`

command to restart the pod with the VPA recommended values.`kubectl delete pod <coredns-pod-name> --namespace kube-system`

After the pod restarts, verify the pod status and CPU/memory updates using the

`kubectl get pod`

command.`kubectl get pod <coredns-pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a CoreDNS pod after applying the VPA recommended values:

`apiVersion: v1 kind: Pod metadata: name: <coredns-pod-name> namespace: kube-system spec: ... containers: - name: coredns resources: limits: cpu: "330m" memory: "168392842" requests: cpu: "11m" memory: "23574998"`


## Troubleshooting

With the cost optimized add-on scaling feature enabled on your cluster, you can customize the default CPU and memory settings for add-on resources, as well as modify the default VPA configuration for supported AKS managed add-ons

If your autoscaling enabled add-on pods are in a pending state, or you don't see any VPA recommendations for autoscaling enabled add-ons, follow these steps to troubleshoot the issue.

### Check AKS-managed VPA add-on status

Check if all VPA system components are running using the

`kubectl get pods`

command.`kubectl get pods --namespace kube-system | grep vpa`

The output should show three pods (vpa-admission-controller, vpa-recommender, and vpa-updater) running in the

`kube-system`

namespace, similar to the following example:`vpa-admission-controller 2/2 2 2 4m11s vpa-recommender 1/1 1 1 4m11s vpa-updater 1/1 1 1 4m11s`

For each of the three VPA pods, check the logs for any errors using the

`kubectl logs`

command. Make sure to replace`<pod-name>`

with the names of the VPA pods.`kubectl logs <pod-name> --namespace kube-system | grep -e '^E[0-9]\{4\}'`

Confirm the custom resource definition (CRD) was creating using the

`kubectl get`

command.`kubectl get customresourcedefinition | grep verticalpodautoscalers`


### Check pod status and CPU/memory utilization

Check the pod's status using the

`kubectl get pod`

command.`kubectl get pod <pod-name> --namespace=kube-system`

If the pod has a status of

`Pending`

, check the pod's status property to determine the reason the pod isn't running.`kubectl describe pod <pod-name> --namespace kube-system -o yaml`

The following output shows an example status of a pod with a status of

`Pending`

:`apiVersion: v1 kind: Pod ... status: conditions: - lastProbeTime: null lastTransitionTime: "2023-05-03T17:05:26Z" message: '0/1 nodes are available: 1 Insufficient cpu, 1 Insufficient memory. preemption: 0/1 nodes are available: 1 Insufficient cpu, 1 Insufficient memory..' reason: Unschedulable status: "False" type: PodScheduled phase: Pending qosClass: Guaranteed`

If the output shows that the pod is

`Pending`

due to insufficient CPU or memory, consider the following actions:- Add more nodes so that pods can be scheduled in nodes with lower resource usage.
- Disable VPA for the target add-on pod by changing the update mode to
*Off*, and then[manually update the requests/limits](customize-resource-configuration)to the available resource values on the node. Be cautious when setting resource limits to extremely low values, as this may result in the pod encountering OOM kills or CPU throttling if it attempts to use more resources than are available on the node.


## Next steps

- Configure
[Cluster Autoscaler](cluster-autoscaler-overview)or[Node Autoprovisioning](node-autoprovision)in your cluster to automatically scale the cluster.


---

<!-- DOCUMENTO FUSIONADO: kubelogin-authentication.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/kubelogin-authentication -->

# Use kubelogin to authenticate users in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The kubelogin plugin in Azure is a client-go credential [plugin](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#client-go-credential-plugins) that implements Microsoft Entra authentication. The kubelogin plugin offers features that aren't available in the kubectl command-line tool. For more information, see the [kubelogin introduction](https://azure.github.io/kubelogin/index.html) and the [kubectl introduction](https://kubernetes.io/docs/reference/kubectl/introduction/).

This article provides an overview and examples of how to use kubelogin for all supported Microsoft Entra authentication methods in AKS.

## Kubelogin authentication in AKS limitations

- Groups that are created in Microsoft Entra are included only by their
**ObjectID**value, and not by their display name. The`sAMAccountName`

command is available only for groups that are synchronized from on-premises Windows Server Active Directory.

- The service principal authentication method works only with managed Microsoft Entra, and not with the earlier version Azure Active Directory.
- The service principal can be a member of a maximum of 200
[Microsoft Entra groups](/en-us/entra/identity/hybrid/connect/how-to-connect-fed-group-claims). If you have more than 200 groups, consider using[application roles](/en-us/entra/external-id/customers/how-to-use-app-roles-customers).

- The device code authentication method doesn't work when a Microsoft Entra Conditional Access policy is set on a Microsoft Entra tenant. In that scenario, use web browser interactive authentication instead.

- The Azure CLI authentication method works only with AKS managed Microsoft Entra.

## How authentication works

Note

Keep in mind the following information about kubelogin authentication for AKS clusters integrated with Microsoft Entra:

**Clusters running Kubernetes version 1.24 or later**automatically use the kubelogin format.**Clusters running Kubernetes 1.24 or earlier**require manual conversion. You can use the device code authentication method to convert the kubeconfig file to use the exec plugin format.

For most interactions with kubelogin, you use the `convert-kubeconfig`

subcommand. The subcommand uses the kubeconfig file that's specified in `--kubeconfig`

or in the `KUBECONFIG`

environment variable to convert the final kubeconfig file to exec format based on the specified authentication method.

The authentication methods that kubelogin implements are Microsoft Entra OAuth 2.0 token grant flows. In each authentication method, the token isn't cached on the file system.

## Device code authentication

Device code is the default authentication method for the `convert-kubeconfig`

subcommand. This authentication method prompts the device code for the user to sign in from a browser session.

Note

Before the kubelogin and exec plugins were introduced, the Azure authentication method in kubectl supported only the device code flow. It used an earlier version of a library that produces a token that has the `audience`

claim with an `spn:`

prefix. It isn't compatible with [AKS managed Microsoft Entra](managed-azure-ad), which uses an [on-behalf-of (OBO)](/en-us/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) flow. When you run the `convert-kubeconfig`

subcommand, kubelogin removes the `spn:`

prefix from the audience claim.

### Parameters for device code authentication

The following table outlines parameters that you can use with device code authentication:

| Parameter | Description |
|---|---|
`-l devicecode` (optional) |
Specifies the kubelogin authentication method. This parameter is optional because device code is the default method. |
`--legacy` |
Uses legacy behavior for earlier versions of Azure Active Directory clusters. If you're using the kubeconfig file in an earlier version Azure Active Directory cluster, kubelogin automatically adds the `--legacy` flag. |
`--token-cache-dir` |
Overrides the default path of the token cache directory, which is ${HOME}/.kube/cache/kubelogin. |

## Azure CLI authentication

The Azure CLI (command: `-l azurecli`

) authentication method uses the signed-in context that the Azure CLI establishes to get the access token. The token is issued in the same Microsoft Entra tenant as `az login`

. kubelogin doesn't write tokens to the token cache file because the Azure CLI already manages them.

### Parameters for Azure CLI authentication

The following table outlines parameters that you can use with Azure CLI authentication:

| Parameter | Description |
|---|---|
`-l azurecli` |
Specifies the kubelogin authentication method. |
`--azure-config-dir` |
Specifies the Azure CLI configuration directory. The default directory is ${HOME}/.azure. |

## Sign in to Azure

Sign in to Azure using the [ az login](/en-us/cli/azure/authenticate-azure-cli-interactively#interactive-login) command.

```
az login
```


## Web browser interactive authentication

The web browser interactive (command: `-l interactive`

) method of authentication automatically opens a web browser to sign in the user. After the user is authenticated, the browser redirects to the local web server using the verified credentials. This authentication method complies with Conditional Access policy.

You can use either a bearer token or a Proof-of-Possession (PoP) token with this authentication method.

### Parameters for bearer token authentication

The following table outlines parameters that you can use with bearer token authentication:

| Parameter | Description |
|---|---|
`-l interactive` |
Specifies the kubelogin authentication method. |
`--token-cache-dir` |
Overrides the default path of the token cache directory, which is ${HOME}/.kube/cache/kubelogin. |

### Parameters for PoP token authentication

The following table outlines parameters that you can use with PoP token authentication:

| Parameter | Description |
|---|---|
`-l interactive` |
Specifies the kubelogin authentication method. |
`--pop-enabled` |
Enables PoP token authentication. |
`--pop-claims` |
Specifies the PoP token claims in a key-value pair format. For example, `u=/ARM/ID/OF/CLUSTER` . |

## Service principal authentication

The service principal (command: `-l spn`

) authentication method uses a service principal to sign in the user. You can provide the credential by setting an environment variable or by using the credential in a command-line argument. The supported credentials that you can use are a password or a Personal Information Exchange (PFX) client certificate.

### Parameters for service principal authentication

The following table outlines parameters that you can use with service principal authentication:

| Parameter | Description |
|---|---|
`-l spn` |
Specifies the kubelogin authentication method. |
`--client-id` |
The application ID (client-id) of the service principal. |
`--client-secret` |
The client secret of the service principal. |

## Managed identity authentication

Use the [managed identity](/en-us/entra/identity/managed-identities-azure-resources/overview) (command: `-l msi`

) authentication method for applications that connect to resources that support Microsoft Entra authentication. Examples include accessing Azure resources like an Azure virtual machine (VM), a virtual machine scale set, or Azure Cloud Shell.

You can use the default managed identity that's assigned to the resource or a specific user-assigned managed identity.

### Parameters for managed identity authentication

The following table outlines parameters that you can use with managed identity authentication:

| Parameter | Description |
|---|---|
`-l msi` |
Specifies the kubelogin authentication method. |
`--client-id` |
The application ID (client-id) of the user-assigned managed identity. If you don't specify this parameter, the default managed identity is used. |

## Workload identity authentication

The workload identity (command: `-l workloadidentity`

) authentication method uses identity credentials that are federated with Microsoft Entra to authenticate access to AKS clusters. The method uses Microsoft Entra integrated authentication. It works by setting the following environment variables:

| Variable | Description |
|---|---|
`AZURE_CLIENT_ID` |
The Microsoft Entra application ID that is federated with the workload identity. |
`AZURE_TENANT_ID` |
The Microsoft Entra tenant ID. |
`AZURE_FEDERATED_TOKEN_FILE` |
The file that contains a signed assertion of the workload identity, like a Kubernetes projected service account (JWT) token. |
`AZURE_AUTHORITY_HOST` |
The base URL of a Microsoft Entra authority. For example, `https://login.microsoftonline.com/` . |

You can use a [workload identity](/en-us/entra/workload-id/workload-identities-overview) to access Kubernetes clusters from CI/CD systems like GitHub or ArgoCD without storing service principal credentials in the external systems. To configure OpenID Connect (OIDC) federation from GitHub, see the [OIDC federation example](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-azure).

### Parameters for workload identity authentication

The following table outlines parameters that you can use with workload identity authentication:

| Parameter | Description |
|---|---|
`-l workloadidentity` |
Specifies the kubelogin authentication method. |

## Export the kubeconfig file path

Before you run the `convert-kubeconfig`

subcommand, export the kubeconfig file path to the `KUBECONFIG`

environment variable. For example:

```
export KUBECONFIG=/path/to/kubeconfig
```


## Convert the kubeconfig file

Run the `convert-kubeconfig`

subcommand to convert the kubeconfig file to use the exec plugin for your chosen authentication method.

```
kubelogin convert-kubeconfig
```


```
kubelogin convert-kubeconfig -l azurecli
```


```
# Bearer token authentication
kubelogin convert-kubeconfig -l interactive
# Proof-of-Possession (PoP) token authentication
kubelogin convert-kubeconfig -l interactive --pop-enabled --pop-claims "u=/ARM/ID/OF/CLUSTER"
```


-
[Use environment variables](#tabpanel_1_environment-variables) -
[Use command-line arguments](#tabpanel_1_command-line-arguments) -
[Use a client certificate](#tabpanel_1_client-certificate) -
[Use a PoP token with environment variables](#tabpanel_1_pop-token-environment-variables)

Run the

`convert-kubeconfig`

subcommand to convert the kubeconfig file to use the exec plugin.`kubelogin convert-kubeconfig -l spn`

Set the environment variables for the client ID and client secret or client certificate. For example:

`export AZURE_CLIENT_ID=<service-principal-client-id> export AZURE_CLIENT_SECRET=<service-principal-client-secret>`


```
# Default managed identity authentication
kubelogin convert-kubeconfig -l msi
# Specific managed identity authentication
kubelogin convert-kubeconfig -l msi --client-id <managed-identity-client-id>
```


```
kubelogin convert-kubeconfig -l workloadidentity
```


## Remove cached tokens

Remove cached tokens using the `kubelogin remove-tokens`

command.

```
kubelogin remove-tokens
```


## Get node information

Get node information using the `kubectl get`

command.

```
kubectl get nodes
```


## How to use kubelogin with AKS

AKS uses a pair of first-party Microsoft Entra applications. These application IDs are the same in all environments.

The AKS Microsoft Entra server application ID (server-id) that the server side uses is `6dae42f8-4368-4678-94ff-3960e28e3630`

. The access token that accesses AKS clusters must be issued for this application. In most kubelogin authentication methods, you must use `--server-id`

with `kubelogin get-token`

.

The AKS Microsoft Entra client application ID (client-id) that kubelogin uses to perform public client authentication on behalf of the user is `80faf920-1908-4b52-b5ef-a8e7bedfc67a`

. The client application ID is used in device code and web browser interactive authentication methods.

## Related content

- Learn how to integrate AKS with Microsoft Entra in the
[AKS managed Microsoft Entra integration](managed-azure-ad)how-to article. - To get started with managed identities in AKS, see
[Use a managed identity in AKS](use-managed-identity). - To get started with workload identities in AKS, see
[Use a workload identity in AKS](workload-identity-overview).
