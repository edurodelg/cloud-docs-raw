---
merged_at: 2026-01-26T23:04:05.986732
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-group-managed-service-accounts -->

# Enable Group Managed Service Accounts (GMSA) for your Windows Server nodes on your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Group Managed Service Accounts (GMSA)](/en-us/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview) is a managed domain account for multiple servers that provides automatic password management, simplified service principal name (SPN) management, and the ability to delegate management to other administrators. With Azure Kubernetes Service (AKS), you can enable GMSA on your Windows Server nodes, which allows containers running on Windows Server nodes to integrate with and be managed by GMSA.

## Prerequisites

- Kubernetes 1.19 or greater. To check your version, see
[Check for available upgrades](upgrade-aks-cluster#check-for-available-aks-cluster-upgrades). To upgrade your version, see[Upgrade AKS cluster](upgrade-aks-cluster). - Azure CLI version 2.35.0 or greater. To find the version, run
`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). [Managed identities](use-managed-identity)enabled on your AKS cluster.- Permissions to create or update an Azure Key Vault.
- Permissions to configure GMSA on Active Directory Domain Service or on-premises Active Directory.
- The domain controller must have Active Directory Web Services enabled and must be reachable on port 9389 by the AKS cluster.

Note

Microsoft also provides a purpose-built PowerShell module to configure gMSA on AKS. For more information, see [gMSA on Azure Kubernetes Service](/en-us/virtualization/windowscontainers/manage-containers/gmsa-aks-ps-module).

## Configure GMSA on Active Directory domain controller

To use GMSA with AKS, you need a standard domain user credential to access the GMSA credential configured on your domain controller. To configure GMSA on your domain controller, see [Get started with Group Managed Service Accounts](/en-us/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts). For the standard domain user credential, you can use an existing user or create a new one, as long as it has access to the GMSA credential.

Important

You must use either Active Directory Domain Service or on-premises Active Directory. At this time, you can't use Microsoft Entra ID to configure GMSA with an AKS cluster.

## Store the standard domain user credentials in Azure Key Vault

Your AKS cluster uses the standard domain user credentials to access the GMSA credentials from the domain controller. To provide secure access to those credentials for the AKS cluster, you should store them in Azure Key Vault.

If you don't already have an Azure key vault, create one using the

command.`az keyvault create`

`az keyvault create --resource-group myResourceGroup --name myGMSAVault`

Store the standard domain user credential as a secret in your key vault using the

command. The following example stores the domain user credential with the key`az keyvault secret set`

*GMSADomainUserCred*in the*myGMSAVault*key vault.`az keyvault secret set --vault-name myGMSAVault --name "GMSADomainUserCred" --value "$Domain\\$DomainUsername:$DomainUserPassword"`

Note

Make sure to use the fully qualified domain name for the domain.


### Optional: Use a custom virtual network with custom DNS

You need to configure your domain controller through DNS so it's reachable by the AKS cluster. You can configure your network and DNS outside of your AKS cluster to allow your cluster to access the domain controller. Alternatively, you can use Azure CNI to configure a custom virtual network with a custom DNS on your AKS cluster to provide access to your domain controller. For more information, see [Configure Azure CNI networking in Azure Kubernetes Service (AKS)](configure-azure-cni).

### Optional: Configure more than one DNS server

If you want to configure more than one DNS server for Windows GMSA in your AKS cluster, don't specify `--gmsa-dns-server`

or `v--gmsa-root-domain-name`

. Instead, you can add multiple DNS servers in the virtual network by selecting *Custom DNS* and adding the DNS servers.

### Optional: Use your own kubelet identity for your cluster

To provide the AKS cluster access to your key vault, the cluster kubelet identity needs access to your key vault. When you create a cluster with managed identity enabled, a kubelet identity is automatically created by default.

You can either [grant access to your key vault for the identity after cluster creation](#enable-gmsa-on-existing-cluster) or create your own identity before cluster creation using the following steps:

Create a kubelet identity using the

command.`az identity create`

`az identity create --name myIdentity --resource-group myResourceGroup`

Get the ID of the identity using the

command and set it to a variable named`az identity list`

`MANAGED_ID`

.`MANAGED_ID=$(az identity list --query "[].id" -o tsv)`

Grant the identity access to your key vault using the

command.`az keyvault set-policy`

`az keyvault set-policy --name "myGMSAVault" --object-id $MANAGED_ID --secret-permissions get`


## Enable GMSA on a new AKS cluster

Create administrator credentials to use during cluster creation. The following commands prompt you for a username and set it to

`WINDOWS_USERNAME`

for use in a later command.`echo "Please enter the username to use as administrator credentials for Windows Server nodes on your cluster: " && read WINDOWS_USERNAME`

Create an AKS cluster using the

command with the following parameters:`az aks create`

`--enable-windows-gmsa`

: Enables GMSA for the cluster.`--gmsa-dns-server`

: The IP address of the DNS server.`--gmsa-root-domain-name`

: The root domain name of the DNS server.

`DNS_SERVER=<IP address of DNS server> ROOT_DOMAIN_NAME="contoso.com" az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --vm-set-type VirtualMachineScaleSets \ --network-plugin azure \ --load-balancer-sku standard \ --windows-admin-username $WINDOWS_USERNAME \ --enable-windows-gmsa \ --gmsa-dns-server $DNS_SERVER \ --gmsa-root-domain-name $ROOT_DOMAIN_NAME \ --generate-ssh-keys`

Note

If you're using a custom virtual network, you need to specify the virtual network ID using the

`vnet-subnet-id`

parameter, and you might need to also add the`docker-bridge-address`

,`dns-service-ip`

, and`service-cidr`

parameters depending on your configuration.If you created your own identity for the kubelet identity, use the

`assign-kubelet-identity`

parameter to specify your identity.When you specify the

`--gmsa-dns-server`

and`--gmsa-root-domain-name`

parameters, a DNS forward rule is added to the`kube-system/coredns`

ConfigMap. This rule forwards the DNS requests for`$ROOT_DOMAIN_NAME`

from the pods to the`$DNS_SERVER`

.`$ROOT_DOMAIN_NAME:53 { errors cache 30 log forward . $DNS_SERVER }`


Add a Windows Server node pool using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --os-type Windows \ --name npwin \ --node-count 1`


### Enable GMSA on existing cluster

Enable GMSA on an existing cluster with Windows Server nodes and managed identities enabled using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--resource-group myResourceGroup \
--name myAKSCluster \
--enable-windows-gmsa \
--gmsa-dns-server $DNS_SERVER \
--gmsa-root-domain-name $ROOT_DOMAIN_NAME
```


## Grant access to your key vault for the kubelet identity

Note

Skip this step if you provided your own identity for the kubelet identity.

Grant access to your key vault for the kubelet identity using the [ az keyvault set-policy](/en-us/cli/azure/keyvault#az-keyvault-set-policy) command.

```
MANAGED_ID=$(az aks show -g myResourceGroup -n myAKSCluster --query "identityProfile.kubeletidentity.objectId" -o tsv)
az keyvault set-policy --name "myGMSAVault" --object-id $MANAGED_ID --secret-permissions get
```


## Install GMSA cred spec

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Create a new YAML named

*gmsa-spec.yaml*and paste in the following YAML. Make sure you replace the placeholders with your own values. Placeholders are indicated with angle brackets (`<>`

), for example replace`<GMSA_ACCOUNT_USERNAME>`

with an account name like`gmsa-account`

.`apiVersion: windows.k8s.io/v1 kind: GMSACredentialSpec metadata: name: aks-gmsa-spec # This name can be changed, but it will be used as a reference in the pod spec credspec: ActiveDirectoryConfig: GroupManagedServiceAccounts: - Name: <GMSA_ACCOUNT_USERNAME> # GMSA account username like gmsa-account Scope: <NETBIOS_DOMAIN_NAME> # NetBIOS domain name like contoso - Name: <GMSA_ACCOUNT_USERNAME> # GMSA account username like gmsa-account Scope: <DNS_DOMAIN_NAME> # Fully qualified domain name like contoso.com HostAccountConfig: PluginGUID: '{CCC2A336-D7F3-4818-A213-272B7924213E}' PortableCcgVersion: "1" PluginInput: "ObjectId=<MANAGED_IDENTITY_OBJECT_ID>;SecretUri=https://<KEY_VAULT_NAME>.vault.azure.net/secrets/<KEY_VAULT_SECRET_NAME>" # MANAGED_IDENTITY_OBJECT_ID is managed identity object ID GUID # KEY_VAULT_NAME is the name of your key vault, like myGMSAVault # KEY_VAULT_SECRET_NAME is the name of the key vault secret you created, like GMSADomainUserCred CmsPlugins: - ActiveDirectory DomainJoinConfig: DnsName: <DNS_DOMAIN_NAME> # Fully qualified domain name like contoso.com DnsTreeName: <DNS_ROOT_DOMAIN_NAME> # Root domain name like contoso.com Guid: <AD_DOMAIN_OBJECT_GUID> # Domain object GUID like 66aa66aa-bb77-cc88-dd99-00ee00ee00ee MachineAccountName: <GMSA_ACCOUNT_USERNAME> # GMSA account username like gmsa-account NetBiosName: <NETBIOS_DOMAIN_NAME> # NetBIOS domain name like contoso Sid: <AD_DOMAIN_OBJECT_SID> # Domain object SID like S-1-5-21-1111111111-2222222222-3333333333`


Note

AKS upgraded the `apiVersion`

of `GMSACredentialSpec`

from `windows.k8s.io/v1alpha1`

to `windows.k8s.io/v1`

in release v20230903.

Create a new YAML named

*gmsa-role.yaml*and paste in the following YAML.`apiVersion: rbac.authorization.k8s.io/v1 kind: ClusterRole metadata: name: aks-gmsa-role rules: - apiGroups: ["windows.k8s.io"] resources: ["gmsacredentialspecs"] verbs: ["use"] resourceNames: ["aks-gmsa-spec"]`

Create a new YAML file named

*gmsa-role-binding.yaml*and paste in the following YAML.`apiVersion: rbac.authorization.k8s.io/v1 kind: RoleBinding metadata: name: allow-default-svc-account-read-on-aks-gmsa-spec namespace: default subjects: - kind: ServiceAccount name: default namespace: default roleRef: kind: ClusterRole name: aks-gmsa-role apiGroup: rbac.authorization.k8s.io`

Apply the changes from

*gmsa-spec.yaml*,*gmsa-role.yaml*, and*gmsa-role-binding.yaml*using the`kubectl apply`

command.`kubectl apply -f gmsa-spec.yaml kubectl apply -f gmsa-role.yaml kubectl apply -f gmsa-role-binding.yaml`


## Verify GMSA installation

Create a new YAML named

*gmsa-demo.yaml*and paste in the following YAML.`--- kind: ConfigMap apiVersion: v1 metadata: labels: app: gmsa-demo name: gmsa-demo namespace: default data: run.ps1: | $ErrorActionPreference = "Stop" Write-Output "Configuring IIS with authentication." # Add required Windows features, since they are not installed by default. Install-WindowsFeature "Web-Windows-Auth", "Web-Asp-Net45" # Create simple ASP.NET page. New-Item -Force -ItemType Directory -Path 'C:\inetpub\wwwroot\app' Set-Content -Path 'C:\inetpub\wwwroot\app\default.aspx' -Value 'Authenticated as <B><%=User.Identity.Name%></B>, Type of Authentication: <B><%=User.Identity.AuthenticationType%></B>' # Configure IIS with authentication. Import-Module IISAdministration Start-IISCommitDelay (Get-IISConfigSection -SectionPath 'system.webServer/security/authentication/windowsAuthentication').Attributes['enabled'].value = $true (Get-IISConfigSection -SectionPath 'system.webServer/security/authentication/anonymousAuthentication').Attributes['enabled'].value = $false (Get-IISServerManager).Sites[0].Applications[0].VirtualDirectories[0].PhysicalPath = 'C:\inetpub\wwwroot\app' Stop-IISCommitDelay Write-Output "IIS with authentication is ready." C:\ServiceMonitor.exe w3svc --- apiVersion: apps/v1 kind: Deployment metadata: labels: app: gmsa-demo name: gmsa-demo namespace: default spec: replicas: 1 selector: matchLabels: app: gmsa-demo template: metadata: labels: app: gmsa-demo spec: securityContext: windowsOptions: gmsaCredentialSpecName: aks-gmsa-spec containers: - name: iis image: mcr.microsoft.com/windows/servercore/iis:windowsservercore-ltsc2019 imagePullPolicy: IfNotPresent command: - powershell args: - -File - /gmsa-demo/run.ps1 volumeMounts: - name: gmsa-demo mountPath: /gmsa-demo volumes: - configMap: defaultMode: 420 name: gmsa-demo name: gmsa-demo nodeSelector: kubernetes.io/os: windows --- apiVersion: v1 kind: Service metadata: labels: app: gmsa-demo name: gmsa-demo namespace: default spec: ports: - port: 80 targetPort: 80 selector: app: gmsa-demo type: LoadBalancer`

Apply the changes from

*gmsa-demo.yaml*using the`kubectl apply`

command.`kubectl apply -f gmsa-demo.yaml`

Get the IP address of the sample application using the

`kubectl get service`

command.`kubectl get service gmsa-demo --watch`

Initially, the

`EXTERNAL-IP`

for the`gmsa-demo`

service shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE gmsa-demo LoadBalancer 10.0.37.27 <pending> 80:30572/TCP 6s`

When the

`EXTERNAL-IP`

address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`gmsa-demo LoadBalancer 10.0.37.27 EXTERNAL-IP 80:30572/TCP 2m`

Open a web browser to the external IP address of the

`gmsa-demo`

service.Authenticate with the

`$NETBIOS_DOMAIN_NAME\$AD_USERNAME`

and password and confirm you see`Authenticated as $NETBIOS_DOMAIN_NAME\$AD_USERNAME, Type of Authentication: Negotiate`

.

### Disable GMSA on an existing cluster

Disable GMSA on an existing cluster with Windows Server nodes using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--resource-group myResourceGroup \
--name myAKSCluster \
--disable-windows-gmsa
```


You can reenable GMSA on an existing cluster by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

## Troubleshooting

### No authentication is prompted when loading the page

If the page loads, but you aren't prompted to authenticate, use the `kubectl logs POD_NAME`

command to display the logs of your pod and verify you see *IIS with authentication is ready*.

Windows containers don't show logs on kubectl by default. To enable Windows containers to show logs, you need to embed the Log Monitor tool on your Windows image. For more information, see [Windows Container Tools](https://github.com/microsoft/windows-container-tools).

### Connection timeout when trying to load the page

If you receive a connection timeout when trying to load the page, verify the sample app is running using the `kubectl get pods --watch`

command. Sometimes the external IP address for the sample app service is available before the sample app pod is running.

### Pod fails to start and a winapi error shows in the pod events

If your pod doesn't start after running the `kubectl get pods --watch`

command and waiting several minutes, use the `kubectl describe pod POD_NAME`

command. If you see a *winapi error* in the pod events, it's likely an error in your GMSA cred spec configuration. Verify all the replacement values in *gmsa-spec.yaml* are correct, rerun `kubectl apply -f gmsa-spec.yaml`

, and redeploy the sample application.

### Container Credential Guard event logs show the directory service isn't available errors

If you see this error message, it might indicate that DNS queries are failing due to blocked TCP fallback.

When gMSA is enabled, the system performs DNS lookups to locate domain controllers, for example `_ldap._tcp.dc._msdcs.<domain>`

. In large Active Directory environments, these responses can exceed the 512-byte UDP limit. When the UDP limit is reached, the DNS server sets the truncated (TC) flag, prompting CoreDNS to retry the query over TCP, as required by [RFC5966](https://datatracker.ietf.org/doc/html/rfc5966). This fallback to TCP is essential for completing the authentication flow. If network security group (NSG) or firewall rules block TCP traffic on port 53, the DNS resolution, and therefore gMSA sign in fails.

To verify if this error is occurring in your environment, enable [CoreDNS query logging](coredns-custom) and use the `kubectl logs --namespace kube-system -l k8s-app=kube-dns`

command to view CoreDNS logs.

Look for patterns like this, where UDP responses are truncated and TCP retries fail:

```
[INFO] 10.123.123.200:62380 - 2 "ANY IN _ldap._tcp.dc._msdcs.contoso.com. udp 49 false 512" NOERROR qr,aa,tc,rd,ra 1357 0.003399698s
[INFO] 10.123.123.200:64233 - 2 "ANY IN _ldap._tcp.dc._msdcs.contoso.com. tcp 49 false 65535" - - 0 6.009670817s
[ERROR] plugin/errors: 2 _ldap._tcp.dc._msdcs.contoso.com. ANY: read tcp 10.123.123.11:55216-><DNS server IP>:53: i/o timeout
```


To resolve this error, we recommend updating your NSG or firewall rules to explicitly allow DNS traffic over TCP on port 53. This update will ensure that large DNS responses can be successfully retried over TCP, enabling the authentication flow to complete as expected.

## Next steps

For more information, see [Windows containers considerations with Azure Kubernetes Service (AKS)](windows-vs-linux-containers).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/managed-identity-overview -->

# Overview of managed identities in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of system-assigned and user-assigned managed identities in AKS, including how they work, role assignments, and AKS-specific managed identity features.

To enable a managed identity on a new or existing AKS cluster, see [Use a managed identity in Azure Kubernetes Service (AKS)](use-managed-identity). For more information about managed identities in Azure, see the [Managed identities for Azure resources documentation](/en-us/entra/identity/managed-identities-azure-resources/).

Note

The system-assigned and user-assigned identity types differ from a [workload identity](workload-identity-overview), which is intended for use by an application running on a pod.

## AKS managed identity authorization flow

AKS clusters use system-assigned or user-assigned [managed identities](/en-us/entra/identity/managed-identities-azure-resources/overview) to request tokens from Microsoft Entra. These tokens help authorize access to other resources running in Azure. You assign an [Azure role-based access control (Azure RBAC)](/en-us/azure/role-based-access-control/overview) role to the managed identity to grant it permissions to a particular Azure resource. For example, you can grant permissions to a managed identity to access secrets in an Azure key vault for use by the cluster.

### Managed identity behavior in AKS

When you deploy an AKS cluster, a system-assigned managed identity is created for you by default. You can also create the cluster with a user-assigned managed identity, or update an existing cluster to a different type of managed identity.

If your cluster already uses a managed identity and you change the identity type (for example, from system-assigned to user-assigned), there's a delay while control plane components switch to the new identity. Control plane components continue to use the old identity until its token expires. After the token refreshes, they switch to the new identity. This process can take several hours.

Note

It's also possible to create a cluster with an application [service principal](kubernetes-service-principal) rather that a managed identity. However, we recommend using a managed identity over an application service principal for security and ease of use. If you have an existing cluster that uses an application service principal, you can update it to use a managed identity.

### AKS identity and credential management

The Azure platform manages both system-assigned and user-assigned managed identities and their credentials, so you can authorize access from your applications without needing to provision or rotate any secrets.

## System-assigned managed identity

The following table summarizes the key characteristics of a system-assigned managed identity in AKS:

| Creation | Lifecycle | Sharing across resources | Common use cases |
|---|---|---|---|
| Created as part of an Azure resource, such as an AKS cluster | Tied to the lifecycle of the parent resource, so it gets deleted when the parent resource is deleted | Can only be associated with a single resource | • Workloads contained within a single Azure resource • Workloads that require independent identities |

### User-assigned managed identity

The following table summarizes the key characteristics of a user-assigned managed identity in AKS:

| Creation | Lifecycle | Sharing across resources | Common use cases |
|---|---|---|---|
| Created as a standalone Azure resource, and must exist prior to cluster creation | Independent of the lifecycle of any specific resource, so it requires manual deletion if no longer needed | Can be shared across multiple resources | • Workloads that run on multiple resources and can share a single identity • Workloads that require preauthorization to a secure resource as part of a provisioning process • Workloads where resources are recycled frequently but need consistent permissions |

### Pre-created kubelet managed identity

A pre-created kubelet managed identity is an optional user-assigned identity that kubelet can use to access other resources in Azure. This feature enables scenarios such as connection to Azure Container Registry (ACR) during cluster creation. If you don't specify a user-assigned managed identity for kubelet, AKS creates a user-assigned kubelet identity in the node resource group. For a user-assigned kubelet identity outside the default worker node resource group, you need to assign the [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) role on the kubelet identity for control plane managed identity.

## Role assignments for managed identities in AKS

You can assign an Azure RBAC role to a managed identity to grant the cluster permissions on another Azure resource. Azure RBAC supports both built-in and custom role definitions that specify levels of permissions. To assign a role, see [Steps to assign an Azure role](/en-us/azure/role-based-access-control/role-assignments-steps).

When you assign an Azure RBAC role to a managed identity, you must define the scope for the role. In general, it's a best practice to limit the scope of a role to the minimum privileges required by the managed identity. For more information on scoping Azure RBAC roles, see [Understand scope for Azure RBAC](/en-us/azure/role-based-access-control/scope-overview).

### Control plane managed identity role assignments

When you create and use your own VNet, attached Azure disks, static IP address, route table, or user-assigned kubelet identity where the resources are outside of the worker node resource group, the Azure CLI adds the role assignment automatically. If you're using an ARM template or another method, use the principal ID of the managed identity to perform a role assignment.

If you're not using the Azure CLI, but you're using your own VNet, attached Azure disks, static IP address, route table, or user-assigned kubelet identity that's outside of the worker node resource group, we recommend using a [user-assigned managed identity for the control plane](use-managed-identity#create-a-user-assigned-managed-identity).

When the control plane uses a system-assigned managed identity, the identity is created at the same time as the cluster, so the role assignment can't be performed until after cluster creation.

## Summary of managed identities used by AKS

AKS uses several managed identities for built-in services and add-ons. The following table summarizes the managed identities used by AKS, their use cases, default permissions, and whether you can bring your own identity:

| Identity | Name | Use case | Default permissions | Bring your own identity |
|---|---|---|---|---|
| Control plane | AKS cluster name | Used by AKS control plane components to manage cluster resources including ingress load balancers and AKS-managed public IPs, Cluster Autoscaler, Azure Disk, File, Blob CSI drivers | Contributor role for Node resource group | Supported |
| Kubelet | AKS cluster name-agentpool | Authentication with Azure Container Registry (ACR) | N/A for Kubernetes version 1.15 and later | Supported |
| Add-on | AzureNPM | No identity required | N/A | Unsupported |
| Add-on | AzureCNI network monitoring | No identity required | N/A | Unsupported |
| Add-on | azure-policy (gatekeeper) | No identity required | N/A | Unsupported |
| Add-on | Calico | No identity required | N/A | Unsupported |
| Add-on | application-routing | Manages Azure DNS and Azure Key Vault certificates | Key Vault Secrets User role for Key Vault, DNS Zone Contributor role for DNS zones, Private DNS Zone Contributor role for private DNS zones | Unsupported |
| Add-on | HTTPApplicationRouting | Manages required network resources | Reader role for node resource group, contributor role for DNS zone | Unsupported |
| Add-on | Ingress application gateway | Manages required network resources | Contributor role for node resource group | Unsupported |
| Add-on | omsagent | Used to send AKS metrics to Azure Monitor | Monitoring Metrics Publisher role | Unsupported |
| Add-on | Virtual-Node (ACIConnector) | Manages required network resources for Azure Container Instances (ACI) | Contributor role for node resource group | Unsupported |
| Add-on | Cost analysis | Used to gather cost allocation data | N/A | Supported |
| Workload identity | Microsoft Entra Workload ID | Enables applications to access cloud resources securely with Microsoft Entra Workload ID | N/A | Unsupported |

## Next step: Enable managed identities in AKS

To learn how to enable managed identities on a new or existing AKS cluster, see [Use a managed identity in Azure Kubernetes Service (AKS)](use-managed-identity).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/nvidia-gpu-operator -->

# Use NVIDIA GPU Operator on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The NVIDIA GPU Operator automates the management and deployment of all NVIDIA software components needed to provision GPU including driver installation, the [NVIDIA device plugin for Kubernetes](https://github.com/NVIDIA/k8s-device-plugin?tab=readme-ov-file), the NVIDIA container runtime, and more. Since the NVIDIA GPU Operator handles these components, it's not necessary to separately install the NVIDIA device plugin on your AKS cluster. This also means that the automatic GPU driver installation should be skipped in order to use the NVIDIA GPU Operator on AKS.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the Azure CLI version 2.72.2 or later installed to set the
`--gpu-driver`

field. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Note

GPU-enabled VMs contain specialized hardware subject to higher pricing and region availability. For more information, see the [pricing](free-standard-pricing-tiers) tool and [region availability](quotas-skus-regions).

## Limitations

- NVIDIA GPU Operator isn't supported for the following OS options: Windows Server versions,
[Flatcar Container Linux for AKS (preview)](flatcar-container-linux-for-aks), and[Azure Linux with OS Guard for AKS (preview)](use-azure-linux-os-guard).

## Get the credentials for your cluster

Get the credentials for your AKS cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. The following example command gets the credentials for the cluster

`myAKSCluster`

in the `myResourceGroup`

resource group:```
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```


Note

The NVIDIA GPU Operator is not compatible with multiple OS versions on the same AKS cluster.

Skip automatic GPU driver installation by creating an NVIDIA GPU-enabled node pool using the [

`az aks nodepool add`

][az-aks-nodepool-add] command and setting the API field`--gpu-driver`

to the value`none`

. Setting this API field to`none`

during node pool creation skips the default GPU driver installation, see[this example](gpu-cluster#skip-gpu-driver-installation). Any existing nodes aren't changed. You can scale the node pool to zero and then back up to make the change take effect.Follow the NVIDIA documentation to

[Install the GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html).Now that you successfully installed the GPU Operator, you can check that your

[GPUs are schedulable](gpu-cluster#confirm-that-gpus-are-schedulable)and[run a GPU workload](gpu-cluster#run-a-gpu-enabled-workload).

Note

There might be additional considerations to take when using the NVIDIA GPU Operator and deploying on SPOT instances. Please refer to [https://github.com/NVIDIA/gpu-operator/issues/577](https://github.com/NVIDIA/gpu-operator/issues/577)

## Next steps

[Monitor NVIDIA GPU metrics](monitor-gpu-metrics)using Azure Managed Prometheus and Azure Managed Grafana.- Learn more about
[Ray clusters on AKS](ray-overview).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-app-configuration-settings -->

# Configure the Azure App Configuration extension for your Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Once you [created the Azure App Configuration extension](azure-app-configuration), you can configure the extension to work best for you and your project using various configuration options, like:

- Configuring the replica count.
- Configuring the log verbosity.
- Configuring the installation namespace.

The extension enables you to configure Azure App Configuration extension settings by using the `--configuration-settings`

parameter in the Azure CLI.

Tip

For a list of available options, see [Azure App Configuration Kubernetes Provider helm values](https://raw.githubusercontent.com/Azure/AppConfiguration-KubernetesProvider/main/deploy/parameter/helm-values.yaml).

## Configure the replica count

The default replica count is `1`

. Create Azure App Configuration extension with customized replica count:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--configuration-settings "replicaCount=3"
```


Note

If configuration settings are sensitive and need to be protected (for example, cert-related information), pass the `--configuration-protected-settings`

parameter and the value will be protected from being read.

## Configure the log verbosity

The default log verbosity is `1`

. Create Azure App Configuration extension with customized log verbosity:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--configuration-settings "logVerbosity=3"
```


Log verbosity levels follow the [klog](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-instrumentation/logging.md#what-method-to-use) convention:

`0`

: Warning and error only.`1`

: Informational, this level is default.`2`

: Detailed steady state information.`3`

: Extended information about changes.`4`

: Debug level verbosity.`5`

: Trace level verbosity.

## Configure the Azure App Configuration extension namespace

The Azure App Configuration extension gets installed in the `azappconfig-system`

namespace by default. To override it, use `--release-namespace`

. Include the cluster `--scope`

to redefine the namespace.

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--scope cluster \
--release-namespace custom-namespace
```


## Show current configuration settings

Use the `az k8s-extension show`

command to show the current Azure App Configuration extension settings:

```
az k8s-extension show --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider
```


## Update configuration settings

To update your Azure App Configuration extension settings, recreate the extension with the desired state. For example, assume we installed the extension using the following configuration:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--configuration-settings "replicaCount=2"
```


To update the `replicaCount`

from two to three, use the following command:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version true \
--configuration-settings "replicaCount=3"
```


## Next Steps

Once you successfully install Azure App Configuration extension in your AKS cluster, try [quickstart](/en-us/azure/azure-app-configuration/quickstart-azure-kubernetes-service) to learn how to use it.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/optimize-aks-costs -->

# Optimize Azure Kubernetes Service (AKS) usage and costs

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides guidance on how to optimize your Azure Kubernetes Service (AKS) usage and costs. It covers guidance on the following topics:

## Automatic scaling

### Horizontal pod autoscaling

The * Horizontal Pod Autoscaler (HPA)* monitors resource demand and automatically updates a workload resource to automatically scale the number of pods to match demand. The response to increased load is to deploy more pods. If the load decreases and the number of pods is above the configured minimum, the autoscaler tells the workload resource to scale down.

The Metrics API gets data from the kubelet every 60 seconds, and the HPA checks the Metrics API every 15 seconds for any needed changes by default. This means that the HPA updates every 60 seconds. When you configure the HPA for a deployment, you define the minimum and maximum number of replicas that can run and the metrics that the HPA uses to determine when to scale.

For more information, see [Horizontal Pod Autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) and [Autoscale pods in AKS](tutorial-kubernetes-scale#autoscale-pods).

### Kubernetes event-driven autoscaling

The [Kubernetes Event-driven Autoscaler (KEDA)](https://keda.sh/) applies event-driven autoscaling to your workloads. KEDA works with the HPA and can extend functionality without overwriting or duplication.

You can use the KEDA add-on for AKS to scale your applications and leverage a [rich catalog of Azure KEDA scalers](https://keda.sh/docs/2.16/scalers/). For more information, see [Application autoscaling with the KEDA add-on](keda-about) and [Install the KEDA add-on for AKS](keda-deploy-add-on-cli).

### Vertical pod autoscaling

The * Vertical Pod Autoscaler (VPA)* automatically sets resource requests and limits on containers per workload based on past usage. The VPA frees up CPU and Memory for pods to ensure effective utilization of your AKS clusters. Over time, the VPA provides recommendations for resource usage.

For more information, see [Vertical pod autoscaling in Azure Kubernetes Service (AKS)](vertical-pod-autoscaler) and [Use the Vertical Pod Autoscaler (VPA) in Azure Kubernetes Service (AKS)](use-vertical-pod-autoscaler).

## Cluster right-sizing

### Right-size your cluster

It's important to * right-size your clusters* to optimize costs and performance. You can manually resize a cluster by adding or removing the nodes to meet the needs of your applications. You can also autoscale your cluster to automatically adjust the number of nodes in response to changing demands.

For more information, see [Resize Azure Kubernetes Service (AKS) clusters](resize-cluster).

### Cluster autoscaling

With the * cluster autoscaler*, you can automatically scale node pools based on resource usage and constraints, such as scaling up to schedule pending pods or scaling down to reduce costs for unused nodes. The

[cluster autoscaler profile](cluster-autoscaler-overview#cluster-autoscaler-profile)is a set of parameters that you can fine-tune to control the behavior of the cluster autoscaler.

For more information, see [Cluster autoscaling in Azure Kubernetes Service (AKS) overview](cluster-autoscaler-overview) and [Use the cluster autoscaler in Azure Kubernetes Service (AKS)](cluster-autoscaler).

### Node autoprovisioning (preview)

* Node autoprovisioning (NAP)* (preview), based on the open-source

[Karpenter](https://karpenter.sh/)project, helps you provision the right infrastructure based on the pending pod resource requirements of your workloads. With efficient bin-packing, you can consolidate your workloads onto the right-sized infrastructure to reduce operating costs.

For more information, see [Node autoprovisioning (preview) in Azure Kubernetes Service (AKS)](node-autoprovision).

## GPU optimizations

### GPU partitioning and sharing

GPU partitioning helps combat underutilization by splitting up or sharing GPUs across multiple workloads. The following sections cover different ways to partition and share GPUs in AKS.

#### Time-slicing

The [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/overview.html) enables the * time-slicing* of GPUs in Kubernetes clusters. With time-slicing, a system administrator can define a set of

*replicas*for a GPU, each of which can be handed out independently to a pod to run workloads on. You can apply cluster-wide default time-slicing configurations and node-specific configurations.


For more information, see [Time-slicing GPUs in Kubernetes](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/gpu-sharing.html).

#### Multi-processing service (MPS)

A single process might not utilize all the memory and compute bandwidth capacity available on a GPU. The * Multi-Process Service (MPS)* enables logical partitioning of memory and compute resources between workloads and allows kernel and memcopy operations from different processes to overlap on the GPU. MPS helps you achieve higher GPU utilization and shorter running times.


For more information, see [Multi-Process Service (MPS)](https://docs.nvidia.com/deploy/mps/index.html#mps).

#### Multi-instance GPUs (MIGs)

* Multi-instance GPUs (MIGs)* enable you to partition GPUs based on the NVIDIA Ampere and later architectures into separate and secure GPU instances for CUDA applications.


For more information, see [GPU Operator with MIG](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/gpu-operator-mig.html) and [Create a multi-instance GPU node pool in Azure Kubernetes Service (AKS)](gpu-multi-instance).

## Multitenancy

Multitenancy refers to the sharing of infrastructure across tenants, teams, and business units. The following table outlines different ways to implement multitenancy in AKS:

| Multitenancy type | Multitenancy level | Cluster pod density | Cost allocation | Ideal use case | Potential risks |
|---|---|---|---|---|---|
Dedicated cluster |

• Lower pod density and more overprovisioned resources

**Dedicated node pool**• Requires extra cluster configurations, like network policies, quota management, role-based access control (RBAC), etc.

**Dedicated namespace**• Requires extra cluster configurations, like network policies, quota management, role-based access control (RBAC), etc.

### Dedicated cluster

With * dedicated cluster multitenancy*, clusters are dedicated to a single workload or team.


The following table outlines pros and cons of using a dedicated cluster:

| Pros | Cons |
|---|---|
| • Easier isolation method • Straightforward cost allocation and chargeback • Great for cases where tenants don't trust each other (often from security and resource sharing perspectives) |
• High management and financial overhead • Generally low pod density and overprovisioned resources |

### Dedicated node pool

With * dedicated node pool multitenancy*, clusters are shared by many tenants.


The following table outlines pros and cons of using a dedicated node pool:

| Pros | Cons |
|---|---|
| • Medium pod density • Some shared infrastructure • Apply Azure tags to node pools dedicated to a single tenant (tags propagate to nodes and persist through upgrades) |
• Requires trust between the tenants • Requires extra cluster configurations, like network policies, quota management, role-based access control (RBAC), etc. |

### Dedicated namespace

With * dedicated namespace multitenancy*, clusters are shared by many tenants, with namespaces serving as the isolation boundary.


The following table outlines pros and cons of using a dedicated namespace:

| Pros | Cons |
|---|---|
| • Higher pod density • Best binpacking • Sharing infrastructure to maximize resource utilization |
• Unsafe for hostile environments by default • Requires extra security measures in place if all tenants can't be trusted |

## Azure discounts

To take savings one step further, take advantage of Azure discounts such as Azure Savings Plans, Reserved Instances, and Azure Hybrid Benefits.

| Azure discount type | Details |
|---|---|
Azure Savings Plans |

• Save up to 65% compared to pay-as-you-go

• Flexible, with no SKU family or region restrictions

• Best for workloads with consistent costs with resources in various SKUs and regions

**Reserved Instances**• Save up to 72% compared to pay-as-you-go

• Restricted to specific SKU families and regions

• Best for stable workloads running continuously (with no unexpected SKU or region changes)

**Azure Hybrid Benefits**• Use any qualifying on-premises licenses that have an active Software Assurance (SA) or qualifying subscription

## Next steps

To learn more about cost in AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-upgrade-github-actions -->

# Apply automatic security upgrades to Azure Kubernetes Service (AKS) nodes using GitHub Actions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Security updates are a key part of maintaining your AKS cluster's security and compliance with the latest fixes for the underlying OS. These updates include OS security fixes or kernel updates. Some updates require a node reboot to complete the process.

This article shows you how you can automate the update process of AKS nodes using GitHub Actions and Azure CLI to create an update task based on `cron`

that runs automatically.

Note

You can also perform node image upgrades automatically and schedule these upgrades using planned maintenance. For more information, see [Automatically upgrade node images](auto-upgrade-node-image).

## Before you begin

- This article assumes you have an existing AKS cluster. If you need an AKS cluster, create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[the Azure portal](learn/quick-kubernetes-deploy-portal). - This article also assumes you have a
[GitHub account](https://github.com)and a[profile repository](https://docs.github.com/en/free-pro-team@latest/github/setting-up-and-managing-your-github-profile/about-your-profile)to host your actions. If you don't have a repository, create one with the same name as your GitHub username. - You need the Azure CLI version 2.0.59 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Update nodes with `az aks upgrade`


The `az aks upgrade`

command gives you a zero downtime way to apply updates. The command performs the following actions:

- Applies the latest updates to all your cluster's nodes.
- Cordons (makes the node unavailable for the scheduling of new workloads) and drains (moves the existent workloads to other node) traffic to the nodes.
- Restarts the nodes.
- Enables the updated nodes to receive traffic again.

AKS doesn't automatically restart your nodes if you update them using a different method.

Note

Running `az aks upgrade`

with the `--node-image-only`

flag only upgrades the node images. Running the command without the flag upgrades both the node images and the Kubernetes control plane version. For more information, see the [docs for managed upgrades on nodes](node-image-upgrade) and the [docs for cluster upgrades](upgrade-cluster).

All Kubernetes nodes run in a standard Windows or Linux-based Azure virtual machine (VM). The Linux-based VMs use an Ubuntu image with the OS configured to automatically check for updates every night.

When you use the `az aks upgrade`

command, Azure CLI creates a surge of new nodes with the latest security and kernel updates. These new nodes are initially cordoned to prevent any apps from being scheduled to them until the update completes. After the update completes, Azure cordons and drains the older nodes and uncordons the new ones, transferring all the scheduled applications to the new nodes.

This process is better than updating Linux-based kernels manually because Linux requires a reboot when a new kernel update is installed. If you update the OS manually, you also need to reboot the VM, manually cordoning and draining all the apps.

## Create a timed GitHub Action

`cron`

is a utility that allows you to run a set of commands, or *jobs*, on an automated schedule. To create a job to update your AKS nodes on an automated schedule, you need a repository to host your actions. GitHub Actions are usually configured in the same repository as your application, but you can use any repository.

Navigate to your repository on GitHub.

Select

**Actions**.Select

**New workflow**>**Set up a workflow yourself**.Create a GitHub Action named

*Upgrade cluster node images*with a schedule trigger to run every 15 days at 3am. Copy the following code into the YAML:`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *'`

Create a job named

*upgrade-node*that runs on an Ubuntu agent and connects to your Azure CLI account to execute the node upgrade command. Copy the following code into the YAML under the`on`

key:`jobs: upgrade-node: runs-on: ubuntu-latest`


## Set up the Azure CLI in the workflow

In the

**Search Marketplace for Actions**bar, search for**Azure Login**.Select

**Azure Login**.Under

**Installation**, select a version, such as*v1.4.6*, and copy the installation code snippet.Add the

`steps`

key and the following information from the installation code snippet to the YAML:`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *' jobs: upgrade-node: runs-on: ubuntu-latest steps: - name: Azure Login uses: Azure/login@v1.4.6 with: creds: ${{ secrets.AZURE_CREDENTIALS }}`


## Create credentials for the Azure CLI

In a new browser window, create a new service principal using the

command. Make sure you replace`az ad sp create-for-rbac`

`*{subscriptionID}*`

with your own subscription ID.Note

This example creates the

`Contributor`

role at the*Subscription*scope. You can provide the role and scope that meets your needs. For more information, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles)and[Azure RBAC scope levels](/en-us/azure/role-based-access-control/scope-overview#scope-format).`az ad sp create-for-rbac --role Contributor --scopes /subscriptions/{subscriptionID} -o json`

Your output should be similar to the following example output:

`{ "appId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "displayName": "xxxxx-xxx-xxxx-xx-xx-xx-xx-xx", "password": "xxxxxxxxxxxxxxxxxxxxxxxxxxxx", "tenant": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" }`

Copy the output and navigate to your GitHub repository.

Select

**Settings**>**Secrets and variables**>**Actions**>**New repository secret**.For

**Name**, enter`AZURE_CREDENTIALS`

.For

**Secret**, copy in the contents of the output you received when you created the service principal.Select

**Add Secret**.

## Create the steps to execute the Azure CLI commands

Navigate to your window with the workflow YAML.

In the

**Search Marketplace for Actions**bar, search for**Azure CLI Action**.Select

**Azure CLI Action**.Under

**Installation**, select a version, such as*v1.0.8*, and copy the installation code snippet.Paste the contents of the action into the YAML below the

`*Azure Login*`

step, similar to the following example:`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *' jobs: upgrade-node: runs-on: ubuntu-latest steps: - name: Azure Login uses: Azure/login@v1.4.6 with: creds: ${{ secrets.AZURE_CREDENTIALS }} - name: Upgrade node images uses: Azure/cli@v1.0.8 with: inlineScript: az aks upgrade --resource-group <resourceGroupName> --name <aksClusterName> --node-image-only --yes`

Tip

You can decouple the

`--resource-group`

and`--name`

parameters from the command by creating new repository secrets like you did for`AZURE_CREDENTIALS`

.If you create secrets for these parameters, you need to replace the

`<resourceGroupName>`

and`<aksClusterName>`

placeholders with their secret counterparts. For example,`${{secrets.RESOURCE_GROUP_NAME}}`

and`${{secrets.AKS_CLUSTER_NAME}}`

Rename the YAML to

`upgrade-node-images.yml`

.Select

**Commit changes...**, add a commit message, and then select**Commit changes**.

## Run the GitHub Action manually

You can run the workflow manually in addition to the scheduled run by adding a new `on`

trigger called `workflow_dispatch`

.

Note

If you want to upgrade a single node pool instead of all node pools on the cluster, add the `--name`

parameter to the `az aks nodepool upgrade`

command to specify the node pool name. For example:

```
az aks nodepool upgrade --resource-group <resourceGroupName> --cluster-name <aksClusterName> --name <nodePoolName> --node-image-only
```


Add the

`workflow_dispatch`

trigger under the`on`

key:`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *' workflow_dispatch:`

The YAML should look similar to the following example:

`name: Upgrade cluster node images on: schedule: - cron: '0 3 */15 * *' workflow_dispatch: jobs: upgrade-node: runs-on: ubuntu-latest steps: - name: Azure Login uses: Azure/login@v1.4.6 with: creds: ${{ secrets.AZURE_CREDENTIALS }} - name: Upgrade node images uses: Azure/cli@v1.0.8 with: inlineScript: az aks upgrade -g {resourceGroupName} -n {aksClusterName} --node-image-only --yes # Code for upgrading one or more node pools`


## Next steps

For more information about AKS upgrades, see the following articles and resources:

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/managed-namespaces -->

# Use managed namespaces in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic ✔️ AKS Standard

Managed namespaces in Azure Kubernetes Service (AKS) provide a way to logically isolate workloads and teams within a cluster. This feature enables administrators to enforce resource quotas, apply network policies, and manage access control at the namespace level. For a detailed overview of managed namespaces, see the [managed namespaces overview](concepts-managed-namespaces).

## Before you begin

### Prerequisites

- An Azure account with an active subscription. If you don't have one, you can
[create an account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F). - An
[AKS cluster](automatic/quick-automatic-managed-network)set up in your Azure environment with[Azure role-based access control for Kubernetes authorization](manage-azure-rbac)is required if you intend to utilize Azure RBAC roles. - To use the network policy feature, the AKS cluster needs to be
[configured with a network policy engine](use-network-policies#network-policy-options-in-aks). Cilium is our recommended engine.

| Prerequisite | Notes |
|---|---|
Azure CLI |
`2.80.0` or later installed. To find the CLI version, run `az --version` . If you need to install or upgrade, see
|
AKS API Version |
`2025-09-01` or later. |
Required permission(s) |
`Microsoft.ContainerService/managedClusters/managedNamespaces/*` or `Azure Kubernetes Service Namespace Contributor` built-in role. `Microsoft.Resources/deployments/*` on the resource group containing the cluster. For more information, see
|

### Limitations

- Trying to on-board system namespaces such as
`kube-system`

,`app-routing-system`

,`istio-system`

,`gatekeeper-system`

, etc. to be managed namespaces isn't allowed. - When a namespace is a managed namespace, changes to the namespace via the Kubernetes API are blocked.

- Listing existing namespaces to convert in the portal doesn't work with private clusters. You can add new namespaces.

## Create a managed namespace on a cluster and assign users

Note

When you create a managed namespace, a component is installed on the cluster to reconcile the namespace with the state in Azure Resource Manager. This component blocks changes to the managed fields and resources from the Kubernetes API, ensuring consistency with the desired configuration.

The following Bicep example demonstrates how to create a managed namespace as a subresource of a managed cluster. Make sure to select the appropriate value for `defaultNetworkPolicy`

, `adoptionPolicy`

, and `deletePolicy`

. For more information about what those parameters mean, see the [managed namespaces overview](concepts-managed-namespaces).

```
resource existingCluster 'Microsoft.ContainerService/managedClusters@2024-03-01' existing = {
name: 'contoso-cluster'
}
resource managedNamespace 'Microsoft.ContainerService/managedClusters/managedNamespaces@2025-09-01' = {
parent: existingCluster
name: 'retail-team'
location: location
properties: {
defaultResourceQuota: {
cpuRequest: '1000m'
cpuLimit: '2000m'
memoryRequest: '512Mi'
memoryLimit: '1Gi'
}
defaultNetworkPolicy: {
ingress: 'AllowSameNamespace'
egress: 'AllowAll'
}
adoptionPolicy: 'IfIdentical'
deletePolicy: 'Keep'
labels: {
environment: 'dev'
}
annotations: {
owner: 'retail'
}
}
}
```


Save the Bicep file **managedNamespace.bicep** to your local computer.

Deploy the Bicep file using the Azure CLI.

```
az deployment group create --resource-group <resource-group> --template-file managedNamespace.bicep
```


### Define variables

Define the following variables to be used in the subsequent steps.

```
RG_NAME=cluster-rg
CLUSTER_NAME=contoso-cluster
NAMESPACE_NAME=retail-team
LABELS="environment=dev"
ANNOTATIONS="owner=retail"
```


### Create the managed namespace

To customize its configuration, managed namespaces have various parameter options to choose from during creation. Make sure to select the appropriate value for `ingress-network-policy`

, `egress-network-policy`

, `adoption-policy`

, and `delete-policy`

. For more information about what those parameters mean, see the [managed namespaces overview](concepts-managed-namespaces).

```
az aks namespace add \
--name ${NAMESPACE_NAME} \
--cluster-name ${CLUSTER_NAME} \
--resource-group ${RG_NAME} \
--cpu-request 1000m \
--cpu-limit 2000m \
--memory-request 512Mi \
--memory-limit 1Gi \
--ingress-policy [AllowSameNamespace|AllowAll|DenyAll] \
--egress-policy [AllowSameNamespace|AllowAll|DenyAll] \
--adoption-policy [Never|IfIdentical|Always] \
--delete-policy [Keep|Delete] \
--labels ${LABELS} \
--annotations ${ANNOTATIONS}
```


### Assign role

After the namespace is created, you can assign [one of the built-in roles](concepts-managed-namespaces#managed-namespaces-built-in-roles) for the control plane and data plane.

```
ASSIGNEE="user@contoso.com"
NAMESPACE_ID=$(az aks namespace show --name ${NAMESPACE_NAME} --cluster-name ${CLUSTER_NAME} --resource-group ${RG_NAME} --query id -o tsv)
```


Assign a control plane role to be able to view the managed namespace in the portal, Azure CLI output, and Azure Resource Manager. This role also allows the user to retrieve the credentials to connect to this namespace.

```
az role assignment create \
--assignee ${ASSIGNEE} \
--role "Azure Kubernetes Service Namespace User" \
--scope ${NAMESPACE_ID}
```


Assign data plane role to be able to get access to create resources within the namespace using the Kubernetes API.

```
az role assignment create \
--assignee ${ASSIGNEE} \
--role "Azure Kubernetes Service RBAC Writer" \
--scope ${NAMESPACE_ID}
```


- Sign in to the
[Azure portal](https://portal.azure.com). - On the Azure portal home page, select
**Create a resource**. - In the
**Categories**section, select**Managed Kubernetes Namespaces**. - On the
**Basics**tab, under**Project details**configure the following settings:- Select the target
**cluster**to create the namespace on. - If you're creating a new namespace, leave the default
**create new**, otherwise choose**change existing to managed**to convert an existing namespace.

- Select the target
- Configure the
**networking policy**to be applied on the namespace. - Configure the
**resource requests and limits**for the namespace. - Select the
**members (users or groups)**and their**role**.- Assign the
**Azure Kubernetes Service Namespace User**role to give them access to view the managed namespace in the portal, Azure CLI output, and Azure Resource Manager. This role also allows the user to retrieve the credentials to connect to this namespace. - Assign the
**Azure Kubernetes Service RBAC Writer**role to give them access to create resources within the namespace using the Kubernetes API.

- Assign the
- Select
**Review + create**to run validation on the configuration. After validation completes, select**Create**.

## List managed namespaces

You can list managed namespaces at different scopes using the Azure CLI.

### Subscription level

Run the following command to list all managed namespaces in a subscription.

```
az aks namespace list --subscription <subscription-id>
```


### Resource group level

Run the following command to list all managed namespaces in a specific resource group.

```
az aks namespace list --resource-group <rg-name>
```


### Cluster level

Run the following command to list all managed namespaces in a specific cluster.

```
az aks namespace list --resource-group <rg-name> --cluster-name <cluster-name>
```


## List managed namespaces

You can list managed namespaces at different scopes using the Azure CLI.

### Subscription level

Run the following command to list all managed namespaces in a subscription.

```
az aks namespace list --subscription <subscription-id>
```


### Resource group level

Run the following command to list all managed namespaces in a specific resource group.

```
az aks namespace list --resource-group <rg-name>
```


### Cluster level

Run the following command to list all managed namespaces in a specific cluster.

```
az aks namespace list --resource-group <rg-name> --cluster-name <cluster-name>
```


## Connect to the cluster

You can retrieve the credentials to connect to a namespace via the following command.

```
az aks namespace get-credentials --name <namespace-name> --resource-group <rg-name> --cluster-name <cluster-name>
```


## Connect to the cluster

You can retrieve the credentials to connect to a namespace via the following command.

```
az aks namespace get-credentials --name <namespace-name> --resource-group <rg-name> --cluster-name <cluster-name>
```


## Next steps

This article focused on using the managed namespaces feature to logically isolate teams and applications. You can further explore other guardrails and best practices to apply via [deployment safeguards](deployment-safeguards).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-labels -->

# Use labels in an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If you have multiple node pools, you may want to add a label during node pool creation. [Kubernetes labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) handle the scheduling rules for nodes. You can add labels to a node pool anytime and apply them to all nodes in the node pool.

In this how-to guide, you learn how to use labels in an Azure Kubernetes Service (AKS) cluster.

## Prerequisites

You need the Azure CLI version 2.2.0 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create an AKS cluster with a label

You can create an AKS cluster with node labels to set key/value metadata for workload scheduling.

```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="myResourceGroup$RANDOM_SUFFIX"
export AKS_CLUSTER_NAME="myAKSCluster$RANDOM_SUFFIX"
az group create --name $RESOURCE_GROUP --location $REGION
```


Results:

```
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx",
"location": "eastus2",
"managedBy": null,
"name": "myResourceGroupxxx",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null,
"type": "Microsoft.Resources/resourceGroups"
}
```


Create the AKS cluster specifying node labels (e.g., dept=IT, costcenter=9000):

```
az aks create \
--resource-group $RESOURCE_GROUP \
--name $AKS_CLUSTER_NAME \
--node-count 2 \
--nodepool-labels dept=IT costcenter=9000 \
--generate-ssh-keys --location $REGION
```


Results:

```
{
"aadProfile": null,
"addonProfiles": {},
"agentPoolProfiles": [
{
"count": 2,
"enableAutoScaling": null,
"mode": "System",
"name": "nodepool1",
"nodeLabels": {
"costcenter": "9000",
"dept": "IT"
}
}
],
"dnsPrefix": "myaksclusterxxx-dns",
"fqdn": "myaksclusterxxx-xxxxxxxx.hcp.eastus2.azmk8s.io",
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.ContainerService/managedClusters/myAKSClusterxxx",
"location": "eastus2",
"name": "myAKSClusterxxx",
"resourceGroup": "myResourceGroupxxx"
}
```


Verify the labels were set:

```
az aks get-credentials --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER_NAME --overwrite-existing
kubectl get nodes --show-labels | grep -e "costcenter=9000" -e "dept=IT"
```


## Create a node pool with a label

You can create an additional node pool with labels for specific scheduling needs.

```
export NODEPOOL_NAME="labelnp"
az aks nodepool add \
--resource-group $RESOURCE_GROUP \
--cluster-name $AKS_CLUSTER_NAME \
--name $NODEPOOL_NAME \
--node-count 1 \
--labels dept=HR costcenter=5000
```


The following is example output from the [ az aks nodepool list](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-list) command showing the

*labelnp*node pool is

*Creating*nodes with the specified

*nodeLabels*:

```
az aks nodepool list --resource-group $RESOURCE_GROUP --cluster-name $AKS_CLUSTER_NAME
```


Results:

```
[
{
"count": 2,
"name": "nodepool1",
"nodeLabels": {
"costcenter": "9000",
"dept": "IT"
}
},
{
"count": 1,
"name": "labelnp",
"nodeLabels": {
"costcenter": "5000",
"dept": "HR"
},
"provisioningState": "Creating"
}
]
```


Verify the labels were set:

```
kubectl get nodes --show-labels | grep -e "costcenter=5000" -e "dept=HR"
```


## Updating labels on existing node pools

You can update the labels on an existing node pool. Note that updating labels will overwrite the old labels.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $AKS_CLUSTER_NAME \
--name $NODEPOOL_NAME \
--labels dept=ACCT costcenter=6000
```


Verify the new labels are set:

```
kubectl get nodes --show-labels | grep -e "costcenter=6000" -e "dept=ACCT"
```


## Unavailable labels

### Reserved system labels

Since the [2021-08-19 AKS release](https://github.com/Azure/AKS/releases/tag/2021-08-19), AKS stopped the ability to make changes to AKS reserved labels. Attempting to change these labels results in an error message.

The following labels are AKS reserved labels. *Virtual node usage* specifies if these labels could be a supported system feature on virtual nodes. Some properties that these system features change aren't available on the virtual nodes because they require modifying the host.

| Label | Value | Example/Options | Virtual node usage |
|---|---|---|---|
`kubernetes.azure.com/agentpool` |
<agent pool name> | `nodepool1` |
Same |
`kubernetes.io/arch` |
<runtime.GOARCH> | `amd64 ` |
N/A |
`kubernetes.io/os` |
<OS Type> | `Linux/Windows` |
Same |
`node.kubernetes.io/instance-type` |
<VM size> | `Standard_NC6s_v3` |
Virtual |
`topology.kubernetes.io/region` |
<Azure region> | `westus2` |
Same |
`topology.kubernetes.io/zone` |
<Azure zone> | `0` |
Same |
`kubernetes.azure.com/cluster` |
<MC_RgName> | `MC_aks_myAKSCluster_westus2` |
Same |
`kubernetes.azure.com/managedby` |
`aks` |
`aks` |
N/A |
`kubernetes.azure.com/mode` |
<mode> | `User` or `system` |
User |
`kubernetes.azure.com/role` |
agent | `Agent` |
Same |
`kubernetes.azure.com/scalesetpriority` |
<VMSS priority> | `spot` or `regular` |
N/A |
`kubernetes.io/hostname` |
<hostname> | `aks-nodepool-00000000-vmss000000` |
Same |
`kubernetes.azure.com/storageprofile` |
<OS disk storage profile> | `Managed` |
N/A |
`kubernetes.azure.com/storagetier` |
<OS disk storage tier> | `Premium_LRS` |
N/A |
`kubernetes.azure.com/node-image-version` |
<VHD version> | `AKSUbuntu-1804-2020.03.05` |
Virtual node version |
`kubernetes.azure.com/network-name` |
<nodepool vnet name> | `vnetName` |
Virtual node virtual network |
`kubernetes.azure.com/network-subnet` |
<nodepool subnet name> | `subnetName` |
Virtual node subnet name |
`kubernetes.azure.com/ppg` |
<nodepool ppg name> | `ppgName` |
N/A |
`kubernetes.azure.com/encrypted-set` |
<nodepool encrypted-set name> | `encrypted-set-name` |
N/A |
`kubernetes.azure.com/accelerator` |
<accelerator> | `nvidia` |
N/A |
`kubernetes.azure.com/fips_enabled` |
<is FIPS enabled?> | `true` |
N/A |
`kubernetes.azure.com/os-sku` |
<os/sku> |
|

`kubernetes.azure.com/os-sku-effective`

`Ubuntu2204`

or similar (never Ubuntu, always has the version specified)`kubernetes.azure.com/os-sku-requested`

`Ubuntu`

, `Ubuntu2204`

, or similar (exactly matches requested sku from API)`kubernetes.azure.com/sku-cpu`

`4`

`kubernetes.azure.com/sku-memory`

`16`

`kubernetes.azure.com/nodepool-type`

`VirtualMachineScaleSets`

*Same*is included in places where the expected values for the labels don't differ between a standard node pool and a virtual node pool. As virtual node pods don't expose any underlying virtual machine (VM), the VM SKU values are replaced with the SKU*Virtual*.*Virtual node version*refers to the current version of the[virtual Kubelet-ACI connector release](https://github.com/virtual-kubelet/azure-aci/releases).*Virtual node subnet name*is the name of the subnet where virtual node pods are deployed into Azure Container Instance (ACI).*Virtual node virtual network*is the name of the virtual network, which contains the subnet where virtual node pods are deployed on ACI.*Node Auto Provisioning (Karpenter)*nodes have additional labels corresponding to the supported[selectors](/en-us/azure/aks/node-auto-provisioning-node-pools#well-known-labels-and-sku-selectors).`kubernetes.azure.com/network-name`

and`kubernetes.azure.com/network-subnet`

will be truncated if the underlying resource names are greater than 64 characters long.

### Reserved prefixes

The following prefixes are AKS reserved prefixes and can't be used for any node:

- kubernetes.azure.com/
- kubernetes.io/

For more information on reserved prefixes, see [Kubernetes well-known labels, annotations, and taints](https://kubernetes.io/docs/reference/labels-annotations-taints/).

### Deprecated labels

The following labels are planned for deprecation with the release of [Kubernetes v1.24](supported-kubernetes-versions#aks-kubernetes-release-calendar). You should change any label references to the recommended substitute.

| Label | Recommended substitute | Maintainer |
|---|---|---|
| failure-domain.beta.kubernetes.io/region | topology.kubernetes.io/region |
|

[Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)[Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)[Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)[Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)*Newly deprecated. For more information, see the [Release Notes](https://github.com/Azure/AKS/releases).

## Next steps

Learn more about Kubernetes labels in the [Kubernetes labels documentation](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).
