---
merged_at: 2026-01-25T12:06:27.844036
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: windows-best-practices.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/windows-best-practices -->

# Best practices for Windows containers on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In AKS, you can create node pools that run Linux or Windows Server as the operating system (OS) on the nodes. Windows Server nodes can run native Windows container applications, such as .NET Framework. The Linux OS and Windows OS have different container support and configuration considerations. For more information, see [Windows container considerations in Kubernetes](windows-vs-linux-containers). To learn more about how various industries are using Windows containers on AKS, see [Windows AKS customer stories](windows-aks-customer-stories).

This article outlines best practices for running Windows containers on AKS.

## Create an AKS cluster with Linux and Windows node pools

When you create a new AKS cluster, the Azure platform creates a Linux node pool by default. This node pool contains system services needed for the cluster to function. Azure also creates and manages a control plane abstracted from the user, which means you aren't exposed to the underlying OS of the nodes hosting the main control plane components. We recommend that you run at least *two nodes* on the default Linux node pool to ensure the reliability and performance of your cluster. You can't delete the default Linux node pool unless you delete the entire cluster.

There are some cases where you should consider deploying a Linux node pool when planning to run Windows-based workloads on your AKS cluster, such as:

- If you want to run Linux and Windows workloads, you can deploy a Linux node pool and a Windows node pool in the same cluster.
- If you want to deploy infrastructure-related components based on Linux, such as NGINX, you need a Linux node pool alongside your Windows node pool. You can use control plane nodes for development and testing scenarios. For production workloads, we recommend that you deploy separate Linux node pools to ensure reliability and performance.

## Modernize existing applications with Windows on AKS

You might want to containerize existing applications and run them using Windows on AKS. Before starting the containerization process, it's important to understand the application architecture and dependencies. For more information, see [Containerize existing applications using Windows containers](/en-us/virtualization/windowscontainers/quick-start/lift-shift-to-containers).

## Windows OS version


Best practice guidanceWindows Server 2022 provides improved security and performance and is the recommended OS for Windows node pools on AKS. AKS uses Windows Server 2022 as the host OS version and only supports process isolation.


AKS supports two options for the Windows Server operating system: Long Term Servicing Channel Releases (LTSC) and Windows Server Annual Channel for Containers.

AKS supports Long Term Servicing Channel Releases (LTSC), including Windows Server 2025 (preview), Windows Server 2022, and Windows Server 2019. This channel is released every three years and is supported for five years. Customers using Long Term Support (LTS) should use Windows Server 2022.

AKS uses Windows Server 2019 and Windows Server 2022 as the host OS versions and only supports process isolation. AKS doesn't support container images built by other versions of Windows Server. For more information, see

[Windows container version compatibility](/en-us/virtualization/windowscontainers/deploy-containers/version-compatibility). Windows Server 2022 is the default OS for Kubernetes version 1.25 and later.Note

[Windows Server 2019 retires on March 1, 2026](https://github.com/Azure/AKS/issues/4091). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2019 on any Kubernetes version. All existing node pools with Windows Server 2019 will be unsupported. Windows Server 2019 is not supported in Kubernetes version 1.33 and above. Starting on April 1, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail.[Windows Server 2022 retires on March 15, 2027](https://github.com/Azure/AKS/issues/4168). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2022 on any Kubernetes version. All existing node pools with Windows Server 2022 will be unsupported. Windows Server 2022 is not supported in Kubernetes version 1.36 and above. Starting on April 1, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail.

For more information, see

[AKS release notes](https://github.com/Azure/AKS/releases). To stay up to date on the latest Windows Server OS versions and learn more about our roadmap of what's planned for support on AKS, see our[AKS public roadmap](https://github.com/azure/aks/projects/1).AKS supports

[Windows Server Annual Channel for Containers](https://techcommunity.microsoft.com/t5/windows-server-news-and-best/windows-server-annual-channel-for-containers/ba-p/3866248)(preview). This channel is released annually and is supported for two years. This channel is beneficial for customers requiring increased innovation cycles and portability. The portability functionality enables the Windows Server 2022-based container image OS to run on newer versions of Windows Server host OS, such as the new annual channel release.Windows Annual Channel versions are based on the Kubernetes version of your node pool. To upgrade from one Annual Channel version to the next,

[upgrade to a Kubernetes version](upgrade-aks-cluster)that supports the next Annual Channel version. For more information, see[Windows Server Annual Channel for Containers on AKS](windows-annual-channel).

## Monitoring


Best practice guidanceWindows Exporter is installed on all Windows nodes in certain regions. To view regional rollout, see

[AKS Github]. With Managed Prometheus and Grafana, you can monitor default collectors included in Windows Exporter on AKS. For more information, see[default Prometheus metrics configured in Azure Monitor].

Windows Exporter allows customers to see their metrics through Managed Prometheus or Prometheus OSS deployments and enjoy enhanced observability around their node and pod performance, health, and resource usage. These metrics are also visible with Managed Grafana.

- When enabling managed prometheus, add this required parameter for correct dashboard data presentation for Windows:
`--enable-windows-recording-rules`

. - Grafana includes dashboards for showing Windows resources, such as:
- Kubernetes / Compute Resources / Cluster (Windows)
- Kubernetes / Compute Resources / Namespace (Windows)
- Kubernetes / Compute Resources / Pod (Windows)
- Kubernetes / USE Method / Cluster (Windows)
- Kubernetes / USE Method / Node (Windows)


The default collectors included in Windows Exporter on AKS are: cpu, cpu_info, cs, container, logical_disk, memory, net, os, process, service, system, textfile. The metrics are exposed on port **19182** on the windows node. For more information on what metrics you can see using these collectors, please see [prometheus-community/windows_exporter](https://github.com/prometheus-community/windows_exporter#collectors).

## Networking

### Networking modes


Best practice guidanceAKS clusters with Windows node pools only support Azure Container Networking Interface (Azure CNI) and use it by default.


Windows doesn't support kubenet networking. AKS clusters with Windows node pools must use Azure CNI. For more information, see [Network concepts for applications in AKS](concepts-network).

Azure CNI offers two networking modes based on your workload requirements:

is an overlay network similar to kubenet. The overlay network allows you to use virtual network (VNet) IPs for nodes and private address spaces for pods within those nodes that you can reuse across the cluster. Azure CNI Overlay is the**Azure CNI Overlay****recommended networking mode**. It provides simplified network configuration and management and the best scalability in AKS networking.requires extra planning and consideration for IP address management. This mode provides VNet IPs for nodes**Azure CNI with Dynamic IP Allocation***and*pods. This configuration allows you direct access to pod IPs. However, it comes with increased complexity and reduced scalability.

To help you decide which networking mode to use, see [Choosing a network model](concepts-network-azure-cni-overlay#choose-a-network-model).

### Network policies


Best practice guidanceUse network policies to secure traffic between pods. Windows supports Azure Network Policy Manager and Calico Network Policy. For more information, see

[Differences between Network Policy engines: Cilium, Azure NPM, and Calico].

When managing traffic between pods, you should apply the principle of least privilege. The Network Policy feature in Kubernetes allows you to define and enforce ingress and egress traffic rules between the pods in your cluster. For more information, see [Secure traffic between pods using network policies in AKS](use-network-policies).

Windows pods on AKS clusters that use the Calico Network Policy enable Floating IP by default.

## Upgrades and updates

It's important to keep your Windows environment up-to-date to ensure your systems have the latest security updates, feature sets, and compliance requirements. In a Kubernetes environment like AKS, you need to maintain the Kubernetes version, Windows nodes, and Windows container images and pods.

### Kubernetes version upgrades

As a managed Kubernetes service, AKS provides the necessary tools to upgrade your cluster to the latest Kubernetes version. For more information, see [Upgrade an AKS cluster](upgrade-cluster).

### Windows node monthly updates

Windows nodes on AKS follow a monthly update schedule. Every month, AKS creates a new VHD with the latest available updates for Windows node pools. The VHD includes the host image, latest Nano Server image, latest Server Core image, and container. We recommend performing monthly updates to your Windows node pools to ensure your nodes have the latest security patches. For more information, see [Upgrade AKS node images](node-image-upgrade).

Note

Upgrades on Windows systems include both OS version upgrades and monthly node OS updates.

You can stay up to date with the availability of new monthly releases using the [AKS release tracker](https://releases.aks.azure.com/) and [AKS release notes](https://github.com/Azure/AKS/releases).

### Windows node OS version upgrades

Windows has a release cadence for new versions of the OS, including Windows Server 2025 (preview), Windows Server 2022, and Windows Server 2019. When upgrading your Windows node OS version, ensure the Windows container image version matches the Windows container host version and the node pools have only one version of Windows Server.

To upgrade the Windows node OS version, you need to complete the following steps:

- Create a new node pool with the new Windows Server version.
- Deploy your workloads with the new Windows container images to the new node pool.
- Decommission the old node pool.

For more information, see [Upgrade Windows Server workloads on AKS](upgrade-windows-2019-2022).

Note

Windows announced a new [Windows Server Annual Channel for Containers](https://techcommunity.microsoft.com/t5/windows-server-news-and-best/windows-server-annual-channel-for-containers/ba-p/3866248) that supports portability and mixed versions of Windows nodes and containers. This feature isn't yet supported in AKS.

To track AKS feature plans, see the [Public AKS roadmap](https://github.com/Azure/AKS/projects/1#card-90806240).

## Next steps

To learn more about Windows containers on AKS, see the following resources:

[Learn how to deploy, manage, and monitor Windows containers on AKS](/en-us/training/paths/deploy-manage-monitor-wincontainers-aks).- Open an issue or provide feedback in the
[Windows containers GitHub repository](https://github.com/microsoft/Windows-Containers/issues). - Review the
[third-party partner solutions for Windows on AKS](windows-aks-partner-solutions).


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
