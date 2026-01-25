---
merged_at: 2026-01-25T12:06:27.775505
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: developer-best-practices-pod-security.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/developer-best-practices-pod-security -->

# Best practices for pod security in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you develop and run applications in Azure Kubernetes Service (AKS), the security of your pods is a key consideration. Your applications should be designed for the principle of least number of privileges required. Keeping private data secure is top of mind for customers. You don't want credentials like database connection strings, keys, or secrets and certificates exposed to the outside world where an attacker could take advantage of those secrets for malicious purposes. Don't add them to your code or embed them in your container images. This approach would create a risk for exposure and limit the ability to rotate those credentials as the container images will need to be rebuilt.

This best practices article focuses on how to secure pods in AKS. You learn how to:

- Use pod security context to limit access to processes and services or privilege escalation
- Authenticate with other Azure resources using Microsoft Entra Workload ID
- Request and retrieve credentials from a digital vault such as Azure Key Vault

You can also read the best practices for [cluster security](operator-best-practices-cluster-security) and for [container image management](operator-best-practices-container-image-management).

## Secure pod access to resources

**Best practice guidance** - To run as a different user or group and limit access to the underlying node processes and services, define pod security context settings. Assign the least number of privileges required.

For your applications to run correctly, pods should run as a defined user or group and not as *root*. The `securityContext`

for a pod or container lets you define settings such as *runAsUser* or *fsGroup* to assume the appropriate permissions. Only assign the required user or group permissions, and don't use the security context as a means to assume additional permissions. The *runAsUser*, privilege escalation, and other Linux capabilities settings are only available on Linux nodes and pods.

When you run as a non-root user, containers cannot bind to the privileged ports under 1024. In this scenario, Kubernetes Services can be used to disguise the fact that an app is running on a particular port.

A pod security context can also define additional capabilities or permissions for accessing processes and services. The following common security context definitions can be set:

**allowPrivilegeEscalation**defines if the pod can assume*root*privileges. Design your applications so this setting is always set to*false*.**Linux capabilities**let the pod access underlying node processes. Take care with assigning these capabilities. Assign the least number of privileges needed. For more information, see[Linux capabilities](http://man7.org/linux/man-pages/man7/capabilities.7.html).**SELinux labels**is a Linux kernel security module that lets you define access policies for services, processes, and filesystem access. Again, assign the least number of privileges needed. For more information, see[SELinux options in Kubernetes](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.27/#selinuxoptions-v1-core)**hostUsers: false**the pod runs using a user-namespace, a Linux kernel feature. This significatly improves the host isolation and limits the lateral movement in case of container breakouts. These improvements are significant whether the container is running as root or not. For more information, see[user-namespaces](secure-container-access#user-namespaces).

The following example pod YAML manifest sets security context settings to define:

- Pod runs as user ID
*1000*and part of group ID*2000* - Can't escalate privileges to use
`root`

- Allows Linux capabilities to access network interfaces and the host's real-time (hardware) clock

```
apiVersion: v1
kind: Pod
metadata:
name: security-context-demo
spec:
securityContext:
fsGroup: 2000
containers:
- name: security-context-demo
image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
securityContext:
runAsUser: 1000
allowPrivilegeEscalation: false
capabilities:
add: ["NET_ADMIN", "SYS_TIME"]
```


Work with your cluster operator to determine which security context settings you need. Design your applications to minimize other permissions and access the pod requires. There are other security features to limit access using AppArmor, seccomp (secure computing), and user-namespaces that can be implemented by cluster operators.

For more information, see [Secure container access to resources](operator-best-practices-cluster-security#secure-container-access-to-resources).

## Limit credential exposure

**Best practice guidance** - Don't define credentials in your application code. Use managed identities for Azure resources to let your pod request access to other resources. A digital vault, such as Azure Key Vault, should also be used to store and retrieve digital keys and credentials. Pod-managed identities are intended for use with Linux pods and container images only.

To limit the risk of credentials being exposed in your application code, avoid the use of fixed or shared credentials. Credentials or keys shouldn't be included directly in your code. If these credentials are exposed, the application needs to be updated and redeployed. A better approach is to give pods their own identity and way to authenticate themselves, or automatically retrieve credentials from a digital vault.

#### Use a Microsoft Entra Workload ID

A workload identity is an identity used by an application running on a pod that can authenticate itself against other Azure services that support it, such as Storage or SQL. It integrates with the capabilities native to Kubernetes to federate with external identity providers. In this security model, the AKS cluster acts as token issuer, Microsoft Entra ID uses OpenID Connect to discover public signing keys and verify the authenticity of the service account token before exchanging it for a Microsoft Entra token. Your workload can exchange a service account token projected to its volume for a Microsoft Entra token using the Azure Identity client library using the [Azure SDK](https://azure.microsoft.com/downloads/) or the [Microsoft Authentication Library](/en-us/azure/active-directory/develop/msal-overview) (MSAL).

For more information about workload identities, see [Configure an AKS cluster to use Microsoft Entra Workload ID with your applications](workload-identity-overview)

#### Use Azure Key Vault with Secrets Store CSI Driver

Using the [Microsoft Entra Workload ID](workload-identity-overview) enables authentication against supporting Azure services. For your own services or applications without managed identities for Azure resources, you can still authenticate using credentials or keys. A digital vault can be used to store these secret contents.

When applications need a credential, they communicate with the digital vault, retrieve the latest secret contents, and then connect to the required service. Azure Key Vault can be this digital vault. The simplified workflow for retrieving a credential from Azure Key Vault using pod managed identities is shown in the following diagram:


With Key Vault, you store and regularly rotate secrets such as credentials, storage account keys, or certificates. You can integrate Azure Key Vault with an AKS cluster using the [Azure Key Vault provider for the Secrets Store CSI Driver](csi-secrets-store-driver). The Secrets Store CSI driver enables the AKS cluster to natively retrieve secret contents from Key Vault and securely provide them only to the requesting pod. Work with your cluster operator to deploy the Secrets Store CSI Driver onto AKS worker nodes. You can use a Microsoft Entra Workload ID to request access to Key Vault and retrieve the secret contents needed through the Secrets Store CSI Driver.

## Next steps

This article focused on how to secure your pods. To implement some of these areas, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: azure-netapp-files.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-netapp-files -->

# Configure Azure NetApp Files for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A persistent volume represents a piece of storage that has been provisioned for use with Kubernetes pods. A persistent volume can be used by one or many pods, and it can be statically or dynamically provisioned. This article shows you how to configure [Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-introduction) to be used by pods on an Azure Kubernetes Service (AKS) cluster.

[Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-introduction) is an enterprise-class, high-performance, metered file storage service running on Azure and supports volumes using [NFS](azure-netapp-files-nfs) (NFSv3 or NFSv4.1), [SMB](azure-netapp-files-smb), and [dual-protocol](azure-netapp-files-dual-protocol) (NFSv3 and SMB, or NFSv4.1 and SMB). Kubernetes users have two options for using Azure NetApp Files volumes for Kubernetes workloads:

- Create Azure NetApp Files volumes
**statically**. In this scenario, the creation of volumes is external to AKS. Volumes are created using the Azure CLI or from the Azure portal, and are then exposed to Kubernetes by the creation of a`PersistentVolume`

. Statically created Azure NetApp Files volumes have many limitations (for example, inability to be expanded, needing to be over-provisioned, and so on). Statically created volumes aren't recommended for most use cases. - Create Azure NetApp Files volumes
**dynamically**, orchestrating through Kubernetes. This method is the**preferred**way to create multiple volumes directly through Kubernetes, and is achieved using[Trident](https://docs.netapp.com/us-en/trident/index.html). Trident is a CSI-compliant dynamic storage orchestrator that helps provision volumes natively through Kubernetes.

Note

Dual-protocol volumes can only be created **statically**. For more information on using dual-protocol volumes with Azure Kubernetes Service, see [Provision Azure NetApp Files dual-protocol volumes for Azure Kubernetes Service](azure-netapp-files-dual-protocol).

Using a CSI driver to directly consume Azure NetApp Files volumes from AKS workloads is the recommended configuration for most use cases. This requirement is accomplished using Trident, an open-source dynamic storage orchestrator for Kubernetes. Trident is an enterprise-grade storage orchestrator purpose-built for Kubernetes, and fully supported by NetApp. It simplifies access to storage from Kubernetes clusters by automating storage provisioning.

You can take advantage of Trident's Container Storage Interface (CSI) driver for Azure NetApp Files to abstract underlying details and create, expand, and snapshot volumes on-demand.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Before you begin

The following considerations apply when you use Azure NetApp Files:

- Your AKS cluster must be
[in a region that supports Azure NetApp Files](https://azure.microsoft.com/global-infrastructure/services/?products=netapp®ions=all). - The Azure CLI version 2.0.59 or higher installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - After the initial deployment of an AKS cluster, you can choose to provision Azure NetApp Files volumes statically or dynamically.
- To use dynamic provisioning with Azure NetApp Files with Network File System (NFS), install and configure
[Trident](https://docs.netapp.com/us-en/trident/index.html)version 19.07 or higher. To use dynamic provisioning with Azure NetApp Files with Secure Message Block (SMB), install and configure Trident version 22.10 or higher. Dynamic provisioning for SMB shares is only supported on windows worker nodes. - Before you deploy Azure NetApp Files SMB volumes, you must identify the AD DS integration requirements for Azure NetApp Files to ensure that Azure NetApp Files is well connected to AD DS. For more information, see
[Understand guidelines for Active Directory Domain Services site design and planning](/en-us/azure/azure-netapp-files/understand-guidelines-active-directory-domain-service-site). Both the AKS cluster and Azure NetApp Files must have connectivity to the same AD.

## Configure Azure NetApp Files for AKS workloads

This section describes how to set up Azure NetApp Files for AKS workloads. It's applicable for all scenarios within this article.

Define variables for later usage. Replace

*myresourcegroup*,*mylocation*,*myaccountname*,*mypool1*,*poolsize*,*premium*,*myvnet*,*myANFSubnet*, and*myprefix*with appropriate values for your environment.`RESOURCE_GROUP="myresourcegroup" LOCATION="mylocation" ANF_ACCOUNT_NAME="myaccountname" POOL_NAME="mypool1" SIZE="poolsize" # size in TiB SERVICE_LEVEL="Premium" # valid values are Standard, Premium and Ultra VNET_NAME="myvnet" SUBNET_NAME="myANFSubnet" ADDRESS_PREFIX="myprefix"`

Register the

*Microsoft.NetApp*resource provider by running the following command:`az provider register --namespace Microsoft.NetApp --wait`

Note

This operation can take several minutes to complete.

Create a new account by using the command

. When you create an Azure NetApp account for use with AKS, you can create the account in an existing resource group or create a new one in the same region as the AKS cluster.`az netappfiles account create`

`az netappfiles account create \ --resource-group $RESOURCE_GROUP \ --location $LOCATION \ --account-name $ANF_ACCOUNT_NAME`

Create a new capacity pool by using the command

. Replace the variables shown in the command with your Azure NetApp Files information. The`az netappfiles pool create`

`account_name`

should be the same as created in Step 3.`az netappfiles pool create \ --resource-group $RESOURCE_GROUP \ --location $LOCATION \ --account-name $ANF_ACCOUNT_NAME \ --pool-name $POOL_NAME \ --size $SIZE \ --service-level $SERVICE_LEVEL`

Create a subnet to

[delegate to Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-delegate-subnet)using the command. Specify the resource group hosting the existing virtual network for your AKS cluster. Replace the variables shown in the command with your Azure NetApp Files information.`az network vnet subnet create`

Note

This subnet must be in the same virtual network as your AKS cluster.

`az network vnet subnet create \ --resource-group $RESOURCE_GROUP \ --vnet-name $VNET_NAME \ --name $SUBNET_NAME \ --delegations "Microsoft.Netapp/volumes" \ --address-prefixes $ADDRESS_PREFIX`


## Statically or dynamically provision Azure NetApp Files volumes for NFS or SMB

After you [configure Azure NetApp Files for AKS workloads](#configure-azure-netapp-files-for-aks-workloads), you can statically or dynamically provision Azure NetApp Files using NFS, SMB, or dual-protocol volumes within the capacity pool. Follow instructions in:

[Provision Azure NetApp Files NFS volumes for Azure Kubernetes Service](azure-netapp-files-nfs)[Provision Azure NetApp Files SMB volumes for Azure Kubernetes Service](azure-netapp-files-smb)[Provision Azure NetApp Files dual-protocol volumes for Azure Kubernetes Service](azure-netapp-files-dual-protocol)

## Next steps

Trident supports many features with Azure NetApp Files. For more information, see:
