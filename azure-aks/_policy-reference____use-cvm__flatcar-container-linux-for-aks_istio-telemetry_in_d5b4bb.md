---
merged_at: 2026-01-26T20:54:26.155965
merged_files: 2
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/policy-reference -->

# Azure Policy built-in definitions for Azure Kubernetes Service

[[Preview]: [Image Integrity] Kubernetes clusters should only use images signed by notation](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fcf426bb8-b320-4321-8545-1b784a5df3a4) |
Use images signed by notation to ensure that images come from trusted sources and will not be maliciously modified. For more info, visit [https://aka.ms/aks/image-integrity](https://aka.ms/aks/image-integrity) |
Audit, Disabled |
[1.1.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ImageIntegrityNotationVerification.json) |
[[Preview]: Azure Backup Extension should be installed in AKS clusters](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffda9cd0b-094c-4cd5-ac2a-5e06e5277c45) |
Ensure protection installation of backup extension in your AKS Clusters to leverage Azure Backup. Azure Backup for AKS is a secure and cloud native data protection solution for AKS clusters |
AuditIfNotExists, Disabled |
[1.0.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Backup/Kubernetes_InstallAzureBackupExtension_Audit.json) |
[[Preview]: Azure Backup should be enabled for AKS clusters](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0b0434ec-2bad-4229-965f-bb7ae5a71257) |
Ensure protection of your AKS Clusters by enabling Azure Backup. Azure Backup for AKS is a secure and cloud native data protection solution for AKS clusters. |
AuditIfNotExists, Disabled |
[1.0.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Backup/Kubernetes_EnableAzureBackup_Audit.json) |
[[Preview]: Azure Kubernetes Service Managed Clusters should be Zone Redundant](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F2dec5f47-bc40-40d1-8c7d-a39d9d6808d1) |
Azure Kubernetes Service Managed Clusters can be configured to be Zone Redundant or not. The policy checks the node pools in the cluster and ensures that avaialbilty zones are set for all the node pools. |
Audit, Deny, Disabled |
[1.0.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Resilience/ContainerService_managedclusters_ZoneRedundant_Audit.json) |
[[Preview]: Deploy Image Integrity on Azure Kubernetes Service](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F5dc99dae-cfb2-42cc-8762-9aae02b74e27) |
Deploy both Image Integrity and Policy Add-Ons Azure Kubernetes clusters. For more info, visit [https://aka.ms/aks/image-integrity](https://aka.ms/aks/image-integrity) |
DeployIfNotExists, Disabled |
[1.2.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_ImageIntegrity_DINE.json) |
[[Preview]: Install Azure Backup Extension in AKS clusters (Managed Cluster) with a given tag.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fbdff5235-9f40-4a32-893f-38a03d5d607c) |
Installing the Azure Backup Extension is a pre-requisite for protecting your AKS Clusters. Enforce installation of backup extension on all AKS clusters containing a given tag. Doing this can help you manage Backup of AKS Clusters at scale. |
AuditIfNotExists, DeployIfNotExists, Disabled |
[1.0.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Backup/Kubernetes_InstallAzureBackupExtensionWithTag_DINE.json) |
[[Preview]: Install Azure Backup Extension in AKS clusters (Managed Cluster) without a given tag.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F9a021087-bba6-42fd-b535-bba75297566b) |
Installing the Azure Backup Extension is a pre-requisite for protecting your AKS Clusters. Enforce installation of backup extension on all AKS clusters without a particular tag value. Doing this can help you manage Backup of AKS Clusters at scale. |
AuditIfNotExists, DeployIfNotExists, Disabled |
[1.0.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Backup/Kubernetes_InstallAzureBackupExtensionWithoutTag_DINE.json) |
[[Preview]: Kubernetes cluster containers should use only allowed sysctl interfaces](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F5e5a0673-649e-4d50-bf9d-5a387a4e2081) |
Containers should use only allowed sysctl interfaces in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
Audit, Deny, Disabled |
[1.0.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedSysctlInterfaces.json) |
[[Preview]: Kubernetes cluster should implement accurate Pod Disruption Budgets](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd9e8f2c1-4c5a-4f5c-8b5a-2abf1e9f7b4d) |
Prevents faulty Pod Disruption Budgets, ensuring a minimum number of operational pods. Refer to the official Kubernetes documentation for details. Relies on Gatekeeper data replication and syncs all Deployment, StatefulSet, and PodDisruptionBudget resources scoped to it into OPA. Before applying this policy, ensure that the synced resources won't strain your memory capacity. All resources of these kinds across namespaces will sync. Note: currently in preview for Kubernetes Service (AKS). |
Audit, Deny, Disabled |
[1.3.1-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/DisallowedBadPodDisruptionBudgets.json) |
[[Preview]: Kubernetes clusters should restrict creation of given resource type](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb81f454c-eebb-4e4f-9dfe-dca060e8a8fd) |
Given Kubernetes resource type should not be deployed in certain namespace. |
Audit, Deny, Disabled |
[2.3.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockResource.json) |
[[Preview]: Prevents containers from being ran as root by setting runAsNotRoot to true.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F2fe7ba7d-f670-41f5-8b70-b61dc7dfbe18) |
Setting runAsNotRoot to true increases security by preventing containers from being ran as root. |
Mutate, Disabled |
[1.1.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateRunAsNonRoot.json) |
[[Preview]: Prevents init containers from being ran as root by setting runAsNotRoot to true.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffed6510d-00b9-40db-a347-933125a6a327) |
Setting runAsNotRoot to true increases security by preventing containers from being ran as root. |
Mutate, Disabled |
[1.1.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateRunAsNonRootInitContainers.json) |
[[Preview]: Sets Kubernetes cluster container securityContext.runAsUser fields to 1000, a non-root user id](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa8e3ce3c-cac3-4402-a28a-03ee3ede9790) |
Reduces attack surface introduced by escalating privileges as root user in the presence of security vulnerabilities. |
Mutate, Disabled |
[1.1.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateRunAsNonRootUserContainers.json) |
[[Preview]: Sets Kubernetes cluster containers' secure computing mode profile type to RuntimeDefault if not present.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F6f87d474-38a9-46c9-bdfe-d7fa3b9836bf) |
Setting secure computing mode profile type for containers to prevent unauthorized and potentially harmful system calls to the kernel from user space. |
Mutate, Disabled |
[1.2.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateSeccompProfileContainers.json) |
[[Preview]: Sets Kubernetes cluster init containers securityContext.runAsUser fields to 1000, a non-root user id](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F97de439f-fd35-4d43-a693-3644f51a51fd) |
Reduces attack surface introduced by escalating privileges as root user in the presence of security vulnerabilities. |
Mutate, Disabled |
[1.1.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateRunAsNonRootUserInitContainers.json) |
[[Preview]: Sets Kubernetes cluster init containers' secure computing mode profile type to RuntimeDefault if not present.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F6bcd4321-fb89-4e3e-bf6c-999c13d47f43) |
Setting secure computing mode profile type for init containers to prevent unauthorized and potentially harmful system calls to the kernel from user space. |
Mutate, Disabled |
[1.2.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateSeccompProfileInitContainers.json) |
[[Preview]: Sets Kubernetes cluster Pod securityContext.runAsUser fields to 1000, a non-root user id](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffe74a23d-79e4-401c-bd0d-fd7a5b35af32) |
Reduces attack surface introduced by escalating privileges as root user in the presence of security vulnerabilities. |
Mutate, Disabled |
[1.1.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateRunAsNonRootUserPod.json) |
[[Preview]: Sets Privilege escalation in the Pod spec in init containers to false.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F4ee3ee6a-96ea-4d25-9c00-17f11d2e02c8) |
Setting Privilege escalation to false in init containers increases security by preventing containers from allowing privilege escalation such as via set-user-ID or set-group-ID file mode. |
Mutate, Disabled |
[1.2.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutatePrivilegeEscalationInitContainers.json) |
[[Preview]: Sets Privilege escalation in the Pod spec to false.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd77df159-718b-4aca-b94b-8e8890a98231) |
Setting Privilege escalation to false increases security by preventing containers from allowing privilege escalation such as via set-user-ID or set-group-ID file mode. |
Mutate, Disabled |
[1.2.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutatePrivilegeEscalationContainers.json) |
[[Preview]: Sets UnhealthyPodEvictionPolicy to 'AlwaysAllow'](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F5c58d54b-87f0-4dcd-83ea-e855fc988997) |
Sets Pod Disruption Budget's UnhealthyPodEvictionPolicy to 'AlwaysAllow' to allow for evicting even unhealthy pods when performing cluster administration |
Mutate, Disabled |
[1.1.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateUnhealthyPodEvictionPolicy.json) |
[Authorized IP ranges should be defined on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0e246bcf-5f6f-4f87-bc6f-775d4712c7ea) |
Restrict access to the Kubernetes Service Management API by granting API access only to IP addresses in specific ranges. It is recommended to limit access to authorized IP ranges to ensure that only applications from allowed networks can access the cluster. |
Audit, Disabled |
[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableIpRanges_KubernetesService_Audit.json) |
[Azure Kubernetes Clusters should disable SSH](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F28257686-e9db-403e-b9e2-a5eecbe03da9) |
Disable SSH gives you the ability to secure your cluster and reduce the attack surface. To learn more, visit: aka.ms/aks/disablessh |
Audit, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_DisableSSH_Audit.json) |
[Azure Kubernetes Clusters should enable Container Storage Interface(CSI)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc5110b6e-5272-4989-9935-59ad06fdf341) |
The Container Storage Interface (CSI) is a standard for exposing arbitrary block and file storage systems to containerized workloads on Azure Kubernetes Service. To learn more, [https://aka.ms/aks-csi-driver](https://aka.ms/aks-csi-driver) |
Audit, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_CSI.json) |
[Azure Kubernetes Clusters should enable Key Management Service (KMS)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fdbbdc317-9734-4dd8-9074-993b29c69008) |
Use Key Management Service (KMS) to encrypt secret data at rest in etcd for Kubernetes cluster security. Learn more at: [https://aka.ms/aks/kmsetcdencryption](https://aka.ms/aks/kmsetcdencryption). |
Audit, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_EnableKMS.json) |
[Azure Kubernetes Clusters should use Azure CNI](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F46238e2f-3f6f-4589-9f3f-77bed4116e67) |
Azure CNI is a prerequisite for some Azure Kubernetes Service features, including Azure network policies, Windows node pools and virtual nodes add-on. Learn more at: [https://aka.ms/aks-azure-cni](https://aka.ms/aks-azure-cni) |
Audit, Disabled |
[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_EnableCNI.json) |
[Azure Kubernetes Service clusters should be a member of an Azure Kubernetes Fleet Manager.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc7f49635-e3f0-4986-b072-90d0c7c3d4cd) |
Detect and report any AKS clusters that are not members of an Azure Kubernetes Fleet Manager. To learn more, visit [https://aka.ms/kubernetes-fleet/policy](https://aka.ms/kubernetes-fleet/policy) |
AuditIfNotExists, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_Detect_Non_Fleet_Manager_Member_Audit.json) |
[Azure Kubernetes Service Clusters should disable Command Invoke](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F89f2d532-c53c-4f8f-9afa-4927b1114a0d) |
Disabling command invoke can enhance the security by avoiding bypass of restricted network access or Kubernetes role-based access control |
Audit, Disabled |
[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_DisableRunCommand_Audit.json) |
[Azure Kubernetes Service Clusters should enable cluster auto-upgrade](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F5c345cdf-2049-47e0-b8fe-b0e96bc2df35) |
AKS cluster auto-upgrade can ensure your clusters are up to date and don't miss the latest features or patches from AKS and upstream Kubernetes. Learn more at: [https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-cluster](/en-us/azure/aks/auto-upgrade-cluster). |
Audit, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_Autoupgrade_Cluster_Audit.json) |
[Azure Kubernetes Service Clusters should enable Image Cleaner](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Faf3c26b2-6fad-493e-9236-9c68928516ab) |
Image Cleaner performs automatic vulnerable, unused image identification and removal, which mitigates the risk of stale images and reduces the time required to clean them up. Learn more at: [https://aka.ms/aks/image-cleaner](https://aka.ms/aks/image-cleaner). |
Audit, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_ImageCleaner_Audit.json) |
[Azure Kubernetes Service Clusters should enable Microsoft Entra ID integration](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F450d2877-ebea-41e8-b00c-e286317d21bf) |
AKS-managed Microsoft Entra ID integration can manage the access to the clusters by configuring Kubernetes role-based access control (Kubernetes RBAC) based on a user's identity or directory group membership. Learn more at: [https://aka.ms/aks-managed-aad](https://aka.ms/aks-managed-aad). |
Audit, Disabled |
[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_AAD_Integration_Audit.json) |
[Azure Kubernetes Service Clusters should enable node os auto-upgrade](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F04408ca5-aa10-42ce-8536-98955cdddd4c) |
AKS node OS auto-upgrade controls node-level OS security updates. Learn more at: [https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-node-image](/en-us/azure/aks/auto-upgrade-node-image). |
Audit, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_Autoupgrade_NodeOS_Audit.json) |
[Azure Kubernetes Service Clusters should enable workload identity](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F2cc2e023-0dac-4046-875b-178f683929d5) |
Workload identity allows to assign a unique identity to each Kubernetes Pod and associate it with Azure AD protected resources such as Azure Key Vault, enabling secure access to these resources from within the Pod. Learn more at: [https://aka.ms/aks/wi](https://aka.ms/aks/wi). |
Audit, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_WorkloadIdentity_Audit.json) |
[Azure Kubernetes Service clusters should have Defender profile enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa1840de2-8088-4ea8-b153-b4c723e9cb01) |
Microsoft Defender for Containers provides cloud-native Kubernetes security capabilities including environment hardening, workload protection, and run-time protection. When you enable the SecurityProfile.AzureDefender on your Azure Kubernetes Service cluster, an agent is deployed to your cluster to collect security event data. Learn more about Microsoft Defender for Containers in [https://docs.microsoft.com/azure/defender-for-cloud/defender-for-containers-introduction?tabs=defender-for-container-arch-aks](/en-us/azure/defender-for-cloud/defender-for-containers-introduction) |
Audit, Disabled |
[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ASC_Azure_Defender_AKS_SecurityProfile_Audit.json) |
[Azure Kubernetes Service Clusters should have local authentication methods disabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F993c2fcd-2b29-49d2-9eb0-df2c3a730c32) |
Disabling local authentication methods improves security by ensuring that Azure Kubernetes Service Clusters should exclusively require Azure Active Directory identities for authentication. Learn more at: [https://aka.ms/aks-disable-local-accounts](https://aka.ms/aks-disable-local-accounts). |
Audit, Deny, Disabled |
[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_DisableLocalAccounts_Deny.json) |
[Azure Kubernetes Service Clusters should use managed identities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fda6e2401-19da-4532-9141-fb8fbde08431) |
Use managed identities to wrap around service principals, simplify cluster management and avoid the complexity required to managed service principals. Learn more at: [https://aka.ms/aks-update-managed-identities](https://aka.ms/aks-update-managed-identities) |
Audit, Disabled |
[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_MSI_Audit.json) |
[Azure Kubernetes Service Private Clusters should be enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F040732e8-d947-40b8-95d6-854c95024bf8) |
Enable the private cluster feature for your Azure Kubernetes Service cluster to ensure network traffic between your API server and your node pools remains on the private network only. This is a common requirement in many regulatory and industry compliance standards. |
Audit, Deny, Disabled |
[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_PrivateCluster_Deny.json) |
[Azure Policy Add-on for Kubernetes service (AKS) should be installed and enabled on your clusters](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0a15ec92-a229-4763-bb14-0ea34a568f8d) |
Azure Policy Add-on for Kubernetes service (AKS) extends Gatekeeper v3, an admission controller webhook for Open Policy Agent (OPA), to apply at-scale enforcements and safeguards on your clusters in a centralized, consistent manner. |
Audit, Disabled |
[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_AzurePolicyAddOn_Audit.json) |
[Azure running container images should have vulnerabilities resolved (powered by Microsoft Defender Vulnerability Management)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F17f4b1cc-c55c-4d94-b1f9-2978f6ac2957) |
Container image vulnerability assessment scans your registry for commonly known vulnerabilities (CVEs) and provides a detailed vulnerability report for each image. This recommendation provides visibility to vulnerable images currently running in your Kubernetes clusters. Remediating vulnerabilities in container images that are currently running is key to improving your security posture, significantly reducing the attack surface for your containerized workloads. |
AuditIfNotExists, Disabled |
[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/MDC_K8sRuningImagesVulnerabilityAssessmentBasedOnMDVM_Audit.json) |
[Both operating systems and data disks in Azure Kubernetes Service clusters should be encrypted by customer-managed keys](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F7d7be79c-23ba-4033-84dd-45e2a5ccdd67) |
Encrypting OS and data disks using customer-managed keys provides more control and greater flexibility in key management. This is a common requirement in many regulatory and industry compliance standards. |
Audit, Deny, Disabled |
[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_CMK_Deny.json) |
[Cannot Edit Individual Nodes](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F53a4a537-990c-495a-92e0-7c21a465442c) |
Cannot Edit Individual Nodes. Users should not edit individual nodes. Please edit node pools. Modifying individual nodes can lead to inconsistent settings, operational challenges, and potential security risks. |
Audit, Deny, Disabled |
[1.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/CannotEditIndividualNodes.json) |
[Configure AKS clusters to automatically join the specified Azure Kubernetes Fleet Manager](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fcadd9445-aeb8-4ee4-b505-c279db2f737f) |
Detect and ensure that AKS clusters join a given Azure Kubernetes Fleet Manager. Optionally, select a look-up tag to specify what fleet update group to join. To learn more, visit [https://aka.ms/kubernetes-fleet/policy](https://aka.ms/kubernetes-fleet/policy) |
DeployIfNotExists, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_Autojoin_Fleet_Manager_DINE.json) |
[Configure Azure Kubernetes Service clusters to enable Defender profile](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F64def556-fbad-4622-930e-72d1d5589bf5) |
Microsoft Defender for Containers provides cloud-native Kubernetes security capabilities including environment hardening, workload protection, and run-time protection. When you enable the SecurityProfile.Defender on your Azure Kubernetes Service cluster, an agent is deployed to your cluster to collect security event data. Learn more about Microsoft Defender for Containers: [https://docs.microsoft.com/azure/defender-for-cloud/defender-for-containers-introduction?tabs=defender-for-container-arch-aks](/en-us/azure/defender-for-cloud/defender-for-containers-introduction). |
DeployIfNotExists, Disabled |
[4.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ASC_Azure_Defender_AKS_SecurityProfile_DINE.json) |
[Configure installation of Flux extension on Kubernetes cluster](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff9175d5f-abc8-1dc3-bd3c-5d7476ada3d1) |
Install Flux extension on Kubernetes cluster to enable deployment of 'fluxconfigurations' in the cluster |
DeployIfNotExists, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-Flux2-Extension-to-Kubernetes-cluster_DINE.json) |
[Configure Kubernetes clusters with Flux v2 configuration using Bucket source and secrets in KeyVault](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F5174c1db-ca42-e0d4-b320-4f1cf6a1fa93) |
Deploy a 'fluxConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined Bucket. This definition requires a Bucket SecretKey stored in Key Vault. For instructions, visit [https://aka.ms/GitOpsFlux2Policy](https://aka.ms/GitOpsFlux2Policy). |
DeployIfNotExists, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/GitOps-Flux2-to-Kubernetes-cluster-Bucket-KVSecret_DINE.json) |
[Configure Kubernetes clusters with Flux v2 configuration using Git repository and HTTPS CA Certificate](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F2630c91f-8a20-8f43-14a2-2485b648e2a9) |
Deploy a 'fluxConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined Git repository. This definition requires a HTTPS CA Certificate. For instructions, visit [https://aka.ms/GitOpsFlux2Policy](https://aka.ms/GitOpsFlux2Policy). |
DeployIfNotExists, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-Flux2-to-Kubernetes-cluster-HTTPs-CA-Cert_DINE.json) |
[Configure Kubernetes clusters with Flux v2 configuration using Git repository and HTTPS secrets](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fbf1a31be-3b79-5ba8-c9e0-9a8c9ad9f749) |
Deploy a 'fluxConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined Git repository. This definition requires a HTTPS key secret stored in Key Vault. For instructions, visit [https://aka.ms/GitOpsFlux2Policy](https://aka.ms/GitOpsFlux2Policy). |
DeployIfNotExists, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-Flux2-to-Kubernetes-cluster-HTTPS-secrets_DINE.json) |
[Configure Kubernetes clusters with Flux v2 configuration using Git repository and local secrets](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb6c7fd52-4723-5f4d-a157-3d39bd16a1d7) |
Deploy a 'fluxConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined Git repository. This definition requires local authentication secrets stored in the Kubernetes cluster. For instructions, visit [https://aka.ms/GitOpsFlux2Policy](https://aka.ms/GitOpsFlux2Policy). |
DeployIfNotExists, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-Flux2-to-Kubernetes-cluster-LocalAuthRef_DINE.json) |
[Configure Kubernetes clusters with Flux v2 configuration using Git repository and SSH secrets](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F9e980dca-f3e1-8da3-6717-ad37b1ca6b27) |
Deploy a 'fluxConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined Git repository. This definition requires a SSH private key secret stored in Key Vault. For instructions, visit [https://aka.ms/GitOpsFlux2Policy](https://aka.ms/GitOpsFlux2Policy). |
DeployIfNotExists, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-Flux2-to-Kubernetes-cluster-SSH_DINE.json) |
[Configure Kubernetes clusters with Flux v2 configuration using public Git repository](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F83ea2fd1-9eaf-2f6d-f672-cd7b2ac798f6) |
Deploy a 'fluxConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined Git repository. This definition requires no secrets. For instructions, visit [https://aka.ms/GitOpsFlux2Policy](https://aka.ms/GitOpsFlux2Policy). |
DeployIfNotExists, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-Flux2-to-Kubernetes-cluster-no-secrets_DINE.json) |
[Configure Kubernetes clusters with specified Flux v2 Bucket source using local secrets](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb8c1d6c1-6137-97c6-9c34-d4627e54ca26) |
Deploy a 'fluxConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined Bucket. This definition requires local authentication secrets stored in the Kubernetes cluster. For instructions, visit [https://aka.ms/GitOpsFlux2Policy](https://aka.ms/GitOpsFlux2Policy). |
DeployIfNotExists, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/GitOps-Flux2-to-Kubernetes-cluster-Bucket-K8sSecret_DINE.json) |
[Configure Kubernetes clusters with specified GitOps configuration using HTTPS secrets](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa6f560f4-f582-4b67-b123-a37dcd1bf7ea) |
Deploy a 'sourceControlConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined git repo. This definition requires HTTPS user and key secrets stored in Key Vault. For instructions, visit [https://aka.ms/K8sGitOpsPolicy](https://aka.ms/K8sGitOpsPolicy). |
auditIfNotExists, AuditIfNotExists, deployIfNotExists, DeployIfNotExists, disabled, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-to-Kubernetes-cluster-HTTPS-secrets_DINE.json) |
[Configure Kubernetes clusters with specified GitOps configuration using no secrets](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1d61c4d2-aef2-432b-87fc-7f96b019b7e1) |
Deploy a 'sourceControlConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined git repo. This definition requires no secrets. For instructions, visit [https://aka.ms/K8sGitOpsPolicy](https://aka.ms/K8sGitOpsPolicy). |
auditIfNotExists, AuditIfNotExists, deployIfNotExists, DeployIfNotExists, disabled, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-to-Kubernetes-cluster-no-secrets_DINE.json) |
[Configure Kubernetes clusters with specified GitOps configuration using SSH secrets](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc050047b-b21b-4822-8a2d-c1e37c3c0c6a) |
Deploy a 'sourceControlConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined git repo. This definition requires a SSH private key secret in Key Vault. For instructions, visit [https://aka.ms/K8sGitOpsPolicy](https://aka.ms/K8sGitOpsPolicy). |
auditIfNotExists, AuditIfNotExists, deployIfNotExists, DeployIfNotExists, disabled, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-to-Kubernetes-cluster-SSH-secrets_DINE.json) |
[Configure Microsoft Entra ID integrated Azure Kubernetes Service Clusters with required Admin Group Access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F36a27de4-199b-40fb-b336-945a8475d6c5) |
Ensure to improve cluster security by centrally govern Administrator access to Microsoft Entra ID integrated AKS clusters. |
DeployIfNotExists, Disabled |
[2.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_AAD_AdminGroup_DINE.json) |
[Configure Node OS Auto upgrade on Azure Kubernetes Cluster](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F40f1aee2-4db4-4b74-acb1-c6972e24cca8) |
Use Node OS auto-upgrade to control node-level OS security updates of Azure Kubernetes Service (AKS) clusters. For more info, visit [https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-node-image](/en-us/azure/aks/auto-upgrade-node-image). |
DeployIfNotExists, Disabled |
[1.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_Autoupgrade_NodeOS_DINE.json) |
[Deploy - Configure diagnostic settings for Azure Kubernetes Service to Log Analytics workspace](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F6c66c325-74c8-42fd-a286-a74b0e2939d8) |
Deploys the diagnostic settings for Azure Kubernetes Service to stream resource logs to a Log Analytics workspace. |
DeployIfNotExists, Disabled |
[3.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/DataConnectorsAzureKubernetes_DINE.json) |
[Deploy Azure Policy Add-on to Azure Kubernetes Service clusters](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa8eff44f-8c92-45c3-a3fb-9880802d67a7) |
Use Azure Policy Add-on to manage and report on the compliance state of your Azure Kubernetes Service (AKS) clusters. For more information, see [https://aka.ms/akspolicydoc](https://aka.ms/akspolicydoc). |
DeployIfNotExists, Disabled |
[4.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_AzurePolicyAddOn_DINE.json) |
[Deploy Image Cleaner on Azure Kubernetes Service](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F7e49285c-4bed-4564-b26a-5225ccc311f3) |
Deploy Image Cleaner on Azure Kubernetes clusters. For more info, visit [https://aka.ms/aks/image-cleaner](https://aka.ms/aks/image-cleaner) |
DeployIfNotExists, Disabled |
[1.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_ImageCleaner_DINE.json) |
[Deploy Planned Maintenance to schedule and control upgrades for your Azure Kubernetes Service (AKS) cluster](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe1352e44-d34d-4e4d-a22e-451a15f759a1) |
Planned Maintenance allows you to schedule weekly maintenance windows to perform updates and minimize workload impact. Once scheduled, upgrades occur only during the window you selected. Learn more at: [https://aka.ms/aks/planned-maintenance](https://aka.ms/aks/planned-maintenance) |
DeployIfNotExists, AuditIfNotExists, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_Maintenance_DINE.json) |
[Disable Command Invoke on Azure Kubernetes Service clusters](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1b708b0a-3380-40e9-8b79-821f9fa224cc) |
Disabling command invoke can enhance the security by rejecting invoke-command access to the cluster |
DeployIfNotExists, Disabled |
[1.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_DisableRunCommand_DINE.json) |
[Ensure cluster containers have readiness or liveness probes configured](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb1a9997f-2883-4f12-bdff-2280f99b5915) |
This policy enforces that all pods have a readiness and/or liveness probes configured. Probe Types can be any of tcpSocket, httpGet and exec. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For instructions on using this policy, visit [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
Audit, Deny, Disabled |
[3.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerEnforceProbes.json) |
[Kubernetes cluster container images must include the preStop hook](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1a3b9003-eac6-4d39-a184-4a567ace7645) |
Requires that container images include a preStop hook to gracefully terminate processes during pod shutdowns. |
Audit, Deny, Disabled |
[1.1.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerEnforcePreStopHook.json) |
[Kubernetes cluster container images should not include latest image tag](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F021f8078-41a0-40e6-81b6-c6597da9f3ee) |
Requires that container images do not use the latest tag in Kubernetes, it is a best practice to ensure reproducibility, prevent unintended updates, and facilitate easier debugging and rollbacks by using explicit and versioned container images. |
Audit, Deny, Disabled |
[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ImagesDoNotUseLatest.json) |
[Kubernetes cluster containers CPU and memory resource limits should not exceed the specified limits](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe345eecc-fa47-480f-9e88-67dcc122b164) |
Enforce container CPU and memory resource limits to prevent resource exhaustion attacks in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[9.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerResourceLimits.json) |
[Kubernetes cluster containers CPU and memory resource requests must be defined](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F03a4ecdb-0684-4039-be91-2762979e1bc8) |
Enforce container CPU and memory resource requests to ensure scheduled node has required resources. |
Audit, Deny, Disabled |
[1.0.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerResourceRequests.json) |
[Kubernetes cluster containers should not share host namespaces](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F47a1ee2f-2a2a-4576-bf2a-e0e36709c2b8) |
Block pod containers from sharing the host process ID namespace, host IPC namespace, and host network namespace in a Kubernetes cluster. This recommendation aligns with the Kubernetes Pod Security Standards for host namespaces and is part of CIS 5.2.1, 5.2.2 and 5.2.3 which are intended to improve the security of your Kubernetes environments. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
Audit, Deny, Disabled |
[6.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockHostNamespace.json) |
[Kubernetes cluster containers should not use forbidden sysctl interfaces](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F56d0a13f-712f-466b-8416-56fb354fb823) |
Containers should not use forbidden sysctl interfaces in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[7.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ForbiddenSysctlInterfaces.json) |
[Kubernetes cluster containers should only pull images when image pull secrets are present](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F12db3749-7e03-4b9f-b443-d37d3fb9f8d9) |
Restrict containers' image pulls to enforce the presence of ImagePullSecrets, ensuring secure and authorized access to images within a Kubernetes cluster |
Audit, Deny, Disabled |
[1.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerRestrictedImagePulls.json) |
[Kubernetes cluster containers should only use allowed AppArmor profiles](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F511f5417-5d12-434d-ab2e-816901e72a5e) |
Containers should only use allowed AppArmor profiles in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[6.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/EnforceAppArmorProfile.json) |
[Kubernetes cluster containers should only use allowed capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc26596ff-4d70-4e6a-9a30-c2506bd2f80c) |
Restrict the capabilities to reduce the attack surface of containers in a Kubernetes cluster. This recommendation is part of CIS 5.2.8 and CIS 5.2.9 which are intended to improve the security of your Kubernetes environments. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[6.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedCapabilities.json) |
[Kubernetes cluster containers should only use allowed images](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffebd0533-8e55-448f-b837-bd0e06f16469) |
Use images from trusted registries to reduce the Kubernetes cluster's exposure risk to unknown vulnerabilities, security issues and malicious images. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[9.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedImages.json) |
[Kubernetes cluster containers should only use allowed ProcMountType](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff85eb0dd-92ee-40e9-8a76-db25a507d6d3) |
Pod containers can only use allowed ProcMountTypes in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedProcMountType.json) |
[Kubernetes cluster containers should only use allowed pull policy](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F50c83470-d2f0-4dda-a716-1938a4825f62) |
Restrict containers' pull policy to enforce containers to use only allowed images on deployments |
Audit, Deny, Disabled |
[3.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedPullPolicy.json) |
[Kubernetes cluster containers should only use allowed seccomp profiles](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F975ce327-682c-4f2e-aa46-b9598289b86c) |
Pod containers can only use allowed seccomp profiles in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[7.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedSeccompProfile.json) |
[Kubernetes cluster containers should run with a read only root file system](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fdf49d893-a74c-421d-bc95-c663042e5b80) |
Run containers with a read only root file system to protect from changes at run-time with malicious binaries being added to PATH in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[6.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ReadOnlyRootFileSystem.json) |
[Kubernetes cluster pod FlexVolume volumes should only use allowed drivers](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff4a8fce0-2dd5-4c21-9a36-8f0ec809d663) |
Pod FlexVolume volumes should only use allowed drivers in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[5.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/FlexVolumeDrivers.json) |
[Kubernetes cluster pod hostPath volumes should only use allowed host paths](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F098fc59e-46c7-4d99-9b16-64990e543d75) |
Limit pod HostPath volume mounts to the allowed host paths in a Kubernetes Cluster. This policy is generally available for Kubernetes Service (AKS), and Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[6.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedHostPaths.json) |
[Kubernetes cluster pods and containers should follow SELinux security standards](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe1e6c427-07d9-46ab-9689-bfa85431e636) |
This policy enforces Kubernetes Pod Security Standards for SELinux options. Under PSS mode, 'user' and 'role' fields must be empty, and 'type' field must be one of the allowed values. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
Audit, Deny, Disabled |
[8.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/SELinux.json) |
[Kubernetes cluster pods and containers should only run with approved user and group IDs](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff06ddb64-5fa3-4b77-b166-acb36f7f6042) |
Control the user, primary group, supplemental group and file system group IDs that pods and containers can use to run in a Kubernetes Cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[6.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedUsersGroups.json) |
[Kubernetes cluster pods should only use allowed volume types](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F16697877-1118-4fb1-9b65-9898ec2509ec) |
Pods can only use allowed volume types in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[5.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedVolumeTypes.json) |
[Kubernetes cluster pods should only use approved host network and port list](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F82985f06-dc18-4a48-bc1c-b9f4f0098cfe) |
Restrict pod access to the host network and the allowable host ports in a Kubernetes cluster. This recommendation is part of CIS 5.2.4 which is intended to improve the security of your Kubernetes environments and aligns with Pod Security Standards (PSS) for hostPorts. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
Audit, Deny, Disabled |
[7.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/HostNetworkPorts.json) |
[Kubernetes cluster pods should use specified labels](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F46592696-4c7b-4bf3-9e45-6c2763bdc0a6) |
Use specified labels to identify the pods in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[7.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/PodEnforceLabels.json) |
[Kubernetes cluster services should listen only on allowed ports](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F233a2a17-77ca-4fb1-9b6b-69223d272a44) |
Restrict services to listen only on allowed ports to secure access to the Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ServiceAllowedPorts.json) |
[Kubernetes cluster services should only use allowed external IPs](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd46c275d-1680-448d-b2ec-e495a3b6cc89) |
Use allowed external IPs to avoid the potential attack (CVE-2020-8554) in a Kubernetes cluster. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[5.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedExternalIPs.json) |
[Kubernetes cluster services should use unique selectors](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb0fdedee-7b9e-4a17-9f5d-5e8e912d2f01) |
Ensure Services in a Namespace Have Unique Selectors. A unique service selector ensures that each service within a namespace is uniquely identifiable based on specific criteria. This policy syncs service resources into OPA via Gatekeeper. Before applying, verify Gatekeeper pods memory capacity won't be exceeded. Parameters apply to specific namespaces, but it syncs all resources of that type across all namespaces. Currently in preview for Kubernetes Service (AKS). |
Audit, Deny, Disabled |
[1.2.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/UniqueServiceSelectors.json) |
[Kubernetes cluster should not allow privileged containers](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F95edb821-ddaf-4404-9732-666045e056b4) |
Do not allow privileged containers creation in a Kubernetes cluster. This recommendation is part of CIS 5.2.1 which is intended to improve the security of your Kubernetes environments. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[9.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerNoPrivilege.json) |
[Kubernetes cluster should not use naked pods](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F65280eef-c8b4-425e-9aec-af55e55bf581) |
Block usage of naked Pods. Naked Pods will not be rescheduled in the event of a node failure. Pods should be managed by Deployment, Replicset, Daemonset or Jobs |
Audit, Deny, Disabled |
[2.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockNakedPods.json) |
[Kubernetes cluster Windows containers should not overcommit cpu and memory](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa2abc456-f0ae-464b-bd3a-07a3cdbd7fb1) |
Windows container resource requests should be less or equal to the resource limit or unspecified to avoid overcommit. If Windows memory is over-provisioned it will process pages in disk - which can slow down performance - instead of terminating the container with out-of-memory |
Audit, Deny, Disabled |
[2.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/WindowsContainerResourceLimits.json) |
[Kubernetes cluster Windows containers should not run as ContainerAdministrator](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F5485eac0-7e8f-4964-998b-a44f4f0c1e75) |
Prevent usage of ContainerAdministrator as the user to execute the container processes for Windows pods or containers. This recommendation is intended to improve the security of Windows nodes. For more information, see [https://kubernetes.io/docs/concepts/windows/intro/](https://kubernetes.io/docs/concepts/windows/intro/) . |
Audit, Deny, Disabled |
[1.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/WindowsBlockContainerAdmin.json) |
[Kubernetes cluster Windows containers should only run with approved user and domain user group](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F57dde185-5c62-4063-b965-afbb201e9c1c) |
Control the user that Windows pods and containers can use to run in a Kubernetes Cluster. This recommendation is part of Pod Security Policies on Windows nodes which are intended to improve the security of your Kubernetes environments. |
Audit, Deny, Disabled |
[2.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/WindowsContainerAllowedUsername.json) |
[Kubernetes cluster Windows pods should not run HostProcess containers](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F077f0ce1-86d6-4058-bc60-de05067e8622) |
Prevent prviledged access to the windows node. This recommendation is intended to improve the security of Windows nodes. For more information, see [https://kubernetes.io/docs/concepts/windows/intro/](https://kubernetes.io/docs/concepts/windows/intro/) . |
Audit, Deny, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/WindowsBlockHostProcess.json) |
[Kubernetes clusters should be accessible only over HTTPS](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1a5b4dca-0b6f-4cf5-907c-56316bc1bf3d) |
Use of HTTPS ensures authentication and protects data in transit from network layer eavesdropping attacks. This capability is currently generally available for Kubernetes Service (AKS), and in preview for Azure Arc enabled Kubernetes. For more info, visit [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc) |
audit, Audit, deny, Deny, disabled, Disabled |
[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/IngressHttpsOnly.json) |
[Kubernetes clusters should disable automounting API credentials](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F423dd1ba-798e-40e4-9c4d-b6902674b423) |
Disable automounting API credentials to prevent a potentially compromised Pod resource to run API commands against Kubernetes clusters. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[4.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockAutomountToken.json) |
[Kubernetes clusters should ensure that the cluster-admin role is only used where required](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa3dc4946-dba6-43e6-950d-f96532848c9f) |
The role 'cluster-admin' provides wide-ranging powers over the environment and should be used only where and when needed. |
Audit, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockAdminRolebindings.json) |
[Kubernetes clusters should minimize wildcard use in role and cluster role](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fca8d5704-aa2b-40cf-b110-dc19052825ad) |
Using wildcards '*' can be a security risk because it grants broad permissions that may not be necessary for a specific role. If a role has too many permissions, it could potentially be abused by an attacker or compromised user to gain unauthorized access to resources in the cluster. |
Audit, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockWildcardRoles.json) |
[Kubernetes clusters should not allow container privilege escalation](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1c6e92c9-99f0-4e55-9cf2-0c234dc48f99) |
Do not allow containers to run with privilege escalation to root in a Kubernetes cluster. This recommendation is part of CIS 5.2.5 which is intended to improve the security of your Kubernetes environments. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
Audit, Deny, Disabled |
[8.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerNoPrivilegeEscalation.json) |
[Kubernetes clusters should not allow endpoint edit permissions of ClusterRole/system:aggregate-to-edit](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1ddac26b-ed48-4c30-8cc5-3a68c79b8001) |
ClusterRole/system:aggregate-to-edit should not allow endpoint edit permissions due to CVE-2021-25740, Endpoint & EndpointSlice permissions allow cross-Namespace forwarding, [https://github.com/kubernetes/kubernetes/issues/103675](https://github.com/kubernetes/kubernetes/issues/103675). This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
Audit, Disabled |
[3.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockEndpointEditDefaultRole.json) |
[Kubernetes clusters should not grant CAP_SYS_ADMIN security capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd2e7ea85-6b44-4317-a0be-1b951587f626) |
To reduce the attack surface of your containers, restrict CAP_SYS_ADMIN Linux capabilities. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[5.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerDisallowedSysAdminCapability.json) |
[Kubernetes clusters should not use specific security capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa27c700f-8a22-44ec-961c-41625264370b) |
Prevent specific security capabilities in Kubernetes clusters to prevent ungranted privileges on the Pod resource. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[5.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerDisallowedCapabilities.json) |
[Kubernetes clusters should not use the default namespace](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F9f061a12-e40d-4183-a00e-171812443373) |
Prevent usage of the default namespace in Kubernetes clusters to protect against unauthorized access for ConfigMap, Pod, Secret, Service, and ServiceAccount resource types. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[4.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockDefaultNamespace.json) |
[Kubernetes clusters should specify host in ingress resource rules](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd8c942c6-16a3-400b-8f2e-785f44030036) |
Ensure specifying host in ingress resource rules to prevent unintentional exposure of backend services to unauthorized access. This policy evaluates Kubernetes Ingress resources to ensure that each rule has a specified host field. |
Audit, Deny, Disabled |
[1.1.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/RequireIngressHost.json) |
[Kubernetes clusters should use Container Storage Interface(CSI) driver StorageClass](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F4f3823b6-6dac-4b5a-9c61-ce1afb829f17) |
The Container Storage Interface (CSI) is a standard for exposing arbitrary block and file storage systems to containerized workloads on Kubernetes. In-tree provisioner StorageClass should be deprecated since AKS version 1.21. To learn more, [https://aka.ms/aks-csi-driver](https://aka.ms/aks-csi-driver) |
Audit, Deny, Disabled |
[2.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/EnforceCSIDriver.json) |
[Kubernetes clusters should use internal load balancers](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F3fc4dc25-5baf-40d8-9b05-7fe74c1bc64e) |
Use internal load balancers to make a Kubernetes service accessible only to applications running in the same virtual network as the Kubernetes cluster. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/LoadbalancerNoPublicIPs.json) |
[Kubernetes resources should have required annotations](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F9a5f4e39-e427-4d5d-ae73-93db00328bec) |
Ensure that required annotations are attached on a given Kubernetes resource kind for improved resource management of your Kubernetes resources. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
Audit, Deny, Disabled |
[3.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/EnforceResourceAnnotation.json) |
[Kubernetes Services should be upgraded to a non-vulnerable Kubernetes version](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffb893a29-21bb-418c-a157-e99480ec364c) |
Upgrade your Kubernetes service cluster to a later Kubernetes version to protect against known vulnerabilities in your current Kubernetes version. Vulnerability CVE-2019-9946 has been patched in Kubernetes versions 1.11.9+, 1.12.7+, 1.13.5+, and 1.14.0+ |
Audit, Disabled |
[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_UpgradeVersion_KubernetesService_Audit.json) |
[Must Have Anti Affinity Rules or Topology Spread Constraints Set](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F34c88cd4-5d72-4dbb-bf77-12c3cafe8791) |
This policy ensures that pods are scheduled on different nodes within the cluster. By enforcing anti-affinity rules or pod topology spread constraints, availability is maintained even if one of the nodes becomes unavailable. Pods will continue to run on other nodes, enhancing resilience. |
Audit, Deny, Disabled |
[1.2.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MustHaveAntiAffinityRulesSet.json) |
[Mutate K8s Container to drop all capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc873b3ba-c605-42e4-a64b-a142a93826fc) |
Mutates securityContext.capabilities.drop to add in "ALL". This drops all capabilities for k8s linux containers |
Mutate, Disabled |
[1.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateContainerAllowedCapabilitiesContainers.json) |
[Mutate K8s Init Container to drop all capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc812272d-7488-495f-a505-047d34b83f58) |
Mutates securityContext.capabilities.drop to add in "ALL". This drops all capabilities for k8s linux init containers |
Mutate, Disabled |
[1.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateContainerAllowedCapabilitiesInitContainers.json) |
[No AKS Specific Labels](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa22123bd-b9da-4c86-9424-24903e91fd55) |
Prevents customers from applying AKS specific labels. AKS uses labels prefixed with `kubernetes.azure.com` to denote AKS owned components. The customer should not use these labels. |
Audit, Deny, Disabled |
[1.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/NoAKSSpecificLabels.json) |
[Prints a message if a mutation is applied](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe24df237-32cb-4a6c-a2f6-85b499cda9f2) |
Looks up the mutation annotations applied and prints a message if annotation exists. |
Audit, Disabled |
[1.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/PrintMutationsAnnotations.json) |
[Reserved System Pool Taints](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F48940d92-ff05-449e-9111-e742d9280451) |
Restricts the CriticalAddonsOnly taint to just the system pool. AKS uses the CriticalAddonsOnly taint to keep customer pods away from the system pool. It ensures a clear separation between AKS components and customer pods, as well as prevents customer pods from being evicted if they do not tolerate the CriticalAddonsOnly taint. |
Audit, Deny, Disabled |
[1.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ReservedSystemPoolTaints.json) |
[Resource logs in Azure Kubernetes Service should be enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F245fc9df-fa96-4414-9a0b-3738c2f7341c) |
Azure Kubernetes Service's resource logs can help recreate activity trails when investigating security incidents. Enable it to make sure the logs will exist when needed |
AuditIfNotExists, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AuditDiagnosticLog_Audit.json) |
[Restricts the CriticalAddonsOnly taint to just the system pool.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe16d171b-bfe5-4d79-a525-19736b396e92) |
To avoid eviction of user apps from user pools and maintain separation of concerns between the user and system pools, the 'CriticalAddonsOnly' taint should not be applied to user pools. |
Mutate, Disabled |
[1.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateReservedSystemPoolTaints.json) |
[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457) |
To provide granular filtering on the actions that users can perform, use Role-Based Access Control (RBAC) to manage permissions in Kubernetes Service Clusters and configure relevant authorization policies. |
Audit, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json) |
[Sets automountServiceAccountToken in the Pod spec in containers to false.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F57f274ef-580a-4ed2-bcf8-5c6fa3775253) |
Setting automountServiceAccountToken to false increases security by avoiding the default auto-mounting of service account tokens |
Mutate, Disabled |
[1.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateMountServiceAccountToken.json) |
[Sets Kubernetes cluster containers CPU limits to default values in case not present.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F42ba1d72-e90f-42f8-bf99-5a1351eed2b1) |
Setting container CPU limits to prevent resource exhaustion attacks in a Kubernetes cluster. |
Mutate, Disabled |
[1.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateResourceCPULimits.json) |
[Sets Kubernetes cluster containers memory limits to default values in case not present.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F5f86d473-38a8-46c9-bdfe-d7fa3b9836bf) |
Setting container memory limits to prevent resource exhaustion attacks in a Kubernetes cluster. |
Mutate, Disabled |
[1.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateResourceMemoryLimits.json) |
[Sets maxUnavailable pods to 1 for PodDisruptionBudget resources](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd77f191e-2338-45d0-b6d4-4ee1c586a192) |
Setting your max unavailable pod value to 1 ensures that your application or service is available during a disruption |
Mutate, Disabled |
[1.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateMaxUnavailablePods.json) |
[Sets readOnlyRootFileSystem in the Pod spec in init containers to true if it is not set.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F2ae2f266-ecc3-4d26-82c5-8c3cb7774f45) |
Setting readOnlyRootFileSystem to true increases security by preventing containers from writing into the root filesystem. This works only for linux containers. |
Mutate, Disabled |
[1.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateReadOnlyRootFilesystemInitContainers.json) |
[Sets readOnlyRootFileSystem in the Pod spec to true if it is not set.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F8e875f96-2c56-40ca-86db-b9f6a0be7347) |
Setting readOnlyRootFileSystem to true increases security by preventing containers from writing into the root filesystem |
Mutate, Disabled |
[1.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateReadOnlyRootFilesystem.json) |
[Temp disks and cache for agent node pools in Azure Kubernetes Service clusters should be encrypted at host](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F41425d9f-d1a5-499a-9932-f8ed8453932c) |
To enhance data security, the data stored on the virtual machine (VM) host of your Azure Kubernetes Service nodes VMs should be encrypted at rest. This is a common requirement in many regulatory and industry compliance standards. |
Audit, Deny, Disabled |
[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_EncryptionAtHost_Deny.json) |

---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __use-cvm__flatcar-container-linux-for-aks_istio-telemetry_ingress-basic.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _use-cvm__flatcar-container-linux-for-aks_istio-telemetry.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-cvm.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-cvm -->

# Use Confidential Virtual Machines (CVM) in Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Confidential Virtual Machines (CVM)](/en-us/azure/confidential-computing/confidential-vm-overview) offer strong security and confidentiality for tenants. CVMs offer VM based Hardware Trusted Execution Environment (TEE) that leverage SEV-SNP security features to deny the hypervisor and other host management code access to VM memory and state, providing defense in depth protections against operator access. These features enable node pools with CVM to target the migration of highly sensitive container workloads to AKS without any code refactoring while benefiting from the features of AKS. For example, you may require CVM if you have the following:

- Workloads that handle security critical data and/or sensitive customer data
- Services that are required to meet various compliance requirements, especially for government contracts. Without a scalable solution for securing data, this could potentially lead to the loss of accreditations and contracts.

In this article, you learn how to create AKS node pools using Confidential VM sizes.

## AKS supported confidential VM sizes

Azure offers a choice of [Trusted Execution Environment (TEE)](/en-us/azure/confidential-computing/trusted-execution-environment) options from both AMD and Intel. These TEEs allow you to create Confidential VM environments with excellent price-to-performance ratios, all without requiring any code changes.

- AMD-based Confidential VMs, use AMD SEV-SNP technology, which is introduced with third Gen AMD EPYC™ processors.
- Intel-based Confidential VMs use Intel TDX, with fourth Gen Intel® Xeon® processors.

Both technologies have different implementations. However both provide similar protections from the cloud infrastructure stack. For more information, see [CVM VM sizes](/en-us/azure/confidential-computing/virtual-machine-options).

## Security Features

CVMs offer the following security enhancements as compared to other virtual machine (VM) sizes:

- Robust hardware-based isolation between virtual machines, hypervisor, and host management code.
- Customizable attestation policies to ensure the host's compliance before deployment.
- Cloud-based Confidential OS disk encryption before the first boot.
- VM encryption keys that the platform or the customer (optionally) owns and manages.
- Secure key release with cryptographic binding between the platform's successful attestation and the VM's encryption keys.
- Dedicated virtual Trusted Platform Module (TPM) instance for attestation and protection of keys and secrets in the virtual machine.
- Secure boot capability similar to Trusted launch for Azure VMs

## How does it work?

If you're running a workload that requires enhanced confidentiality and integrity, you can benefit from memory encryption and enhanced security without code changes in your application. All pods on your CVM node are part of the same trust boundary. The nodes in a node pool created with CVM use a customized [node image](node-images) specially configured for CVM.

### Supported OS Versions

You can create CVM node pools on Linux OS types (Ubuntu and Azure Linux). However, not all OS versions support CVM node pools.

This table includes the supported OS versions:

| OS Type | OS SKU | CVM support | CVM default |
|---|---|---|---|
| Linux | `Ubuntu` |
Supported | Ubuntu 20.04 is default for K8s version 1.24-1.33. Ubuntu 24.04 is the default for K8s version 1.34-1.38. |
| Linux | `Ubuntu2204` |
Not Supported | AKS doesn't support CVM for Ubuntu 22.04. |
| Linux | `Ubuntu2404` |
Supported | CVM is supported on `Ubuntu2404` in K8s 1.32-1.38. |
| Linux | `AzureLinux` |
Supported on Azure Linux 3.0 | Azure Linux 3 is default when enabling CVM for K8s version 1.28-1.36. |
| Linux | `flatcar` |
Not supported |
|

`AzureLinuxOSGuard`

[Azure Linux with OS Guard for AKS](use-azure-linux-os-guard)doesn't support CVM.When using `Ubuntu`

or `AzureLinux`

as the `osSKU`

, if the default OS version doesn't support CVM, AKS defaults to the most recent CVM-supported version of the OS. For example, Ubuntu 22.04 is default for Linux node pools. Since 22.04 doesn't currently support CVM, AKS defaults to Ubuntu 20.04 for Linux CVM-enabled node pools.

### Limitations

The following limitations apply when adding a node pool with CVM to AKS:

- You can't use FIPS, ARM64, Trusted Launch, or Pod Sandboxing.
- You can't update an existing node pool to migrate to a CVM size. To migrate, you'll need to
[resize your node pool](resize-node-pool). - You can't use CVM with Windows node pools.
- CVM with Azure Linux is currently in preview.

## Prerequisites

Before you begin, make sure you have the following:

- An existing AKS cluster.
- CVM sizes must be available for your subscription in the region where the cluster is created. You must have sufficient quota to create a node pool with a CVM size.
- If you're using Azure Linux os, you need to install the
`aks-preview`

extension, update the`aks-preview`

extension, and register the preview feature flag. If you're using Ubuntu, you can skip these steps.

### If you are using Azure Linux

CVMs for Ubuntu is GA, but CVMs with Azure Linux is currently still in preview. If you would like to use CVM node pools with Azure Linux as the OS of choice, ensure you enable the extension and register the flag.

#### Install `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

`az extension update --name aks-preview`


#### Register `AzureLinuxCVMPreview`

feature flag

Register the

`AzureLinuxCVMPreview`

feature flag using the [`az feature register`

][az-feature-register] command.`az feature register --namespace "Microsoft.ContainerService" --name "AzureLinuxCVMPreview"`

Verify the registration status using the [

`az feature show`

][az-feature-show] command. It takes a few minutes for the status to show*Registered*.`az feature show --namespace Microsoft.ContainerService --name AzureLinuxCVMPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using the [`az provider register`

][az-provider-register] command.`az provider register --namespace Microsoft.ContainerService`


## Add a node pool with a CVM to your AKS cluster

Add a node pool with a CVM to your AKS cluster using the

command and set the`az aks nodepool add`

`node-vm-size`

to a supported[VM size](/en-us/azure/confidential-computing/virtual-machine-options).`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --node-count 3 \ --node-vm-size Standard_DC4as_v5`


If you don't specify the `osSKU`

or `osType`

, AKS defaults to `--os-type Linux`

and `--os-sku Ubuntu`

.

## Upgrade an existing node pool with a CVM to Ubuntu 24.04

Upgrade an existing node pool with a CVM to Ubuntu 24.04 from Ubuntu 20.04 using the

command. Set the`az aks nodepool update`

`os-sku`

as`Ubuntu2404`

.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --os-sku Ubuntu2404`


Note

A node pool which is Ubuntu 24.04 with a CVM is supported from AKS cluster 1.33 version. Additionally, before Ubuntu 24.04 becomes GA, you need to register the `Ubuntu2404Preview`

feature. For more information, see [ here](/en-us/azure/aks/upgrade-os-version#register-ubuntu2404preview-feature-flag) to register the feature.

## Verify the node pool uses CVM

Verify a node pool uses CVM using the

command and verify the`az aks nodepool show`

`vmSize`

is`Standard_DCa4_v5`

.`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'vmSize'`

The following example command and output shows the node pool uses CVM:

`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'vmSize' "Standard_DC4as_v5"`

Verify a node pool uses a CVM image using the

command.`az aks nodepool list`

`az aks nodepool list \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'nodeImageVersion'`

The following example command and output shows the node pool uses an Ubuntu 20.04 CVM image:

`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'nodeImageVersion' "AKSUbuntu-2004cvmcontainerd-202507.02.0"`


## Remove a node pool with CVM from an AKS cluster

Remove a node pool with CVM from an AKS cluster using the

command.`az aks nodepool delete`

`az aks nodepool delete \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool`


## Next steps

In this article, you learned how to add a node pool with CVM to an AKS cluster.

- For more information about CVM, see
[Confidential VM node pools support on AKS](/en-us/azure/confidential-computing/confidential-node-pool-aks). - To migrate an existing node pool to a CVM vm size, you can
[resize your node pool](resize-node-pool). - If you're only interested in enabling Trusted Launch on your node pools, see
[Trusted Launch on AKS](use-trusted-launch).


---

<!-- DOCUMENTO FUSIONADO: _flatcar-container-linux-for-aks_istio-telemetry.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: flatcar-container-linux-for-aks.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/flatcar-container-linux-for-aks -->

# Use Flatcar Container Linux for Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of Flatcar Container Linux for AKS, a Cloud Native Compute Foundation (CNCF) project that provides security, reliability, and cross-cloud capabilities. Flatcar Container Linux is available in preview as an OS option on AKS. You can deploy Flatcar Container Linux node pools in a new AKS cluster or add Flatcar Container Linux node pools to your existing clusters. To learn more about Flatcar Container Linux, see the [Flatcar documentation](https://www.flatcar.org/).

## Flatcar Container Linux for AKS benefits

Flatcar uses an immutable OS filesystem, and it eliminates configuration drift and prevents unauthorized changes, ensuring robust protection for your workloads across multiple cloud platforms. Designed for versatility, Flatcar enables cross-cloud deployment, empowering businesses to scale effortlessly and securely.

## Limitations

Flatcar Container Linux for AKS has the following limitations:

[FIPS](enable-fips-nodes)isn't supported with Flatcar Container Linux.[Trusted Launch](use-trusted-launch)isn't supported with Flatcar Container Linux.[Confidential VM sizes](use-cvm)aren't supported with Flatcar Container Linux.- The
`SecurityPatch`

[node OS upgrade channel](auto-upgrade-node-os-image)isn't supported with Flatcar Container Linux. - During preview, AKS doesn't support in-place updates with Flatcar Container Linux.
[Artifact Streaming](artifact-streaming)(preview) isn't supported with Flatcar Container Linux.[Generation 1 VMs](aks-virtual-machine-sizes)aren't supported with Flatcar Container Linux, which means you can't use VM sizes that only support Generation 1.[Pod Sandboxing (preview)](use-pod-sandboxing)isn't supported with Flatcar Container Linux.[Node auto-provisioning](node-autoprovision)isn't supported with Flatcar Container Linux.[Azure Monitor VM(SS) extension](/en-us/azure/azure-monitor/agents/azure-monitor-agent-manage?tabs=azure-portal#:%7E:text=Virtual%20machine%20(VM)%20extension)isn't supported.

Note

If you have an existing cluster with any of the above features enabled, you might not be able to add a node pool using Flatcar Container Linux.

## Get started with Flatcar Container Linux for AKS

To get started using the Flatcar Container Linux for AKS, see the following resources:

- Deploy an Azure Kubernetes Service (AKS) cluster with Flatcar Container Linux for AKS (preview) using
[Azure CLI](learn/quick-flatcar-deploy-cli) - Deploy an Azure Kubernetes Service (AKS) cluster with Flatcar Container Linux for AKS (preview) using an
[ARM template](learn/quick-flatcar-deploy-arm-template) - Create an AKS cluster with a single Flatcar Container Linux for AKS (preview) node pool using
[Azure CLI or an ARM template](create-node-pools) - Add a Flatcar Container Linux for AKS (preview) node pool to an existing cluster using
[Azure CLI or an ARM template](create-node-pools)

## OS migrations and upgrades with Flatcar Container Linux

AKS doesn't support in-place migrations from existing Linux clusters or node pools to Flatcar Container Linux clusters or node pools. To migrate existing workloads to Flatcar Container Linux for AKS, you need to recreate your node pools using `--os-sku flatcar`

.

Flatcar Container Linux for AKS releases weekly AKS node images. Versioning follows the AKS date-based format (for example: 202506.13.0). You can check the node images in the release notes and by using the [ az aks nodepool list](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-list) command to view the

`nodeImageVersion`

. For example:```
az aks nodepool list --resource-group <resource-group-name> --cluster-name <aks-cluster-name> --query '[].{name: name, nodeImageVersion: nodeImageVersion}'
```


Example output:

```
[
{
"name": "nodes",
"nodeImageVersion": "AKSFlatcar-flatcargen2-202508.06.0"
}
]
```


You can check the Flatcar version number (for example: Flatcar 4372.0.1) in the release notes and by using `kubectl get nodes`

command. For example:

```
kubectl get nodes -o wide
```


Example output:

```
NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME
aks-nodes-16363508-vmss000000 Ready <none> 2m33s v1.32.6 10.224.0.4 <none> Flatcar Container Linux by Kinvolk 4372.0.1 (Oklo) 6.12.35-flatcar containerd://2.0.4
```


Flatcar's inbuilt automatic A/B update for the OS partition is disabled and only full node image updates are supported.

## Next steps

To learn more about Flatcar Container Linux, see the [Flatcar documentation](https://www.flatcar.org/).


---

<!-- DOCUMENTO FUSIONADO: istio-telemetry.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-telemetry -->

# Telemetry API for Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Istio can [generate metrics, distributed traces, and access logs](https://istio.io/latest/docs/concepts/observability/) for all workloads in the mesh. The Istio-based service mesh add-on for Azure Kubernetes Service (AKS) provides telemetry customization options through the [shared MeshConfig](istio-meshconfig) and the Istio Telemetry API `v1`

for Istio add-on minor revisions `asm-1-22`

and higher.

Note

While the [Istio MeshConfig](istio-meshconfig) also provides options for configuring telemetry globally across the mesh, the Telemetry API offers more granular control over telemetry settings on a per-service or per-workload basis. As the Istio community continues to invest in the Telemetry API, it is now the preferred method for telemetry configuration. We encourage migrating to the Telemetry API for configuring telemetry to be collected in the mesh.

## Prerequisites

- You must be on revision
`asm-1-22`

or higher. For information on how to perform minor version upgrades, see the[Istio add-on upgrade documentation](istio-upgrade).

## Configure Telemetry resources

The following example demonstrates how Envoy access logging can be enabled across the mesh for the Istio add-on via the Telemetry API using `asm-1-22`

(adjust the revision as needed). For guidance on other Telemetry API customizations for the add-on, see the [Telemetry API support scope](#telemetry-api-support-scope) section and the [Istio documentation](https://istio.io/latest/docs/reference/config/telemetry/).

### Deploy sample applications

Label the namespace for sidecar injection:

```
kubectl label ns default istio.io/rev=asm-1-22
```


Deploy the `sleep`

application and set the `SOURCE_POD`

environment variable:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.22/samples/sleep/sleep.yaml
export SOURCE_POD=$(kubectl get pod -l app=sleep -o jsonpath={.items..metadata.name})
```


Then, deploy the `httpbin`

application:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.22/samples/httpbin/httpbin.yaml
```


### Enable Envoy access logging with the Istio Telemetry API

Deploy the following Istio `v1`

Telemetry API resource to enable Envoy access logging for the entire mesh:

```
cat <<EOF | kubectl apply -n aks-istio-system -f -
apiVersion: telemetry.istio.io/v1
kind: Telemetry
metadata:
name: mesh-logging-default
spec:
accessLogging:
- providers:
- name: envoy
EOF
```


### Test access logs

Send a request from `sleep`

to `httpbin`

:

```
kubectl exec "$SOURCE_POD" -c sleep -- curl -sS -v httpbin:8000/status/418
```


Verify that access logs are visible for the `sleep`

pod:

```
kubectl logs -l app=sleep -c istio-proxy
```


You should see the following output:

```
[2024-08-13T00:31:47.690Z] "GET /status/418 HTTP/1.1" 418 - via_upstream - "-" 0 135 12 11 "-" "curl/8.9.1" "cdecaca5-5964-48f3-b42d-f474dfa623d5" "httpbin:8000" "10.244.0.13:8080" outbound|8000||httpbin.default.svc.cluster.local 10.244.0.12:53336 10.0.112.220:8000 10.244.0.12:42360 - default
```


Now, verify that access logs are visible for the `httpbin`

pod:

```
kubectl logs -l app=httpbin -c istio-proxy
```


You should see the following output:

```
[2024-08-13T00:31:47.696Z] "GET /status/418 HTTP/1.1" 418 - via_upstream - "-" 0 135 2 1 "-" "curl/8.9.1" "cdecaca5-5964-48f3-b42d-f474dfa623d5" "httpbin:8000" "10.244.0.13:8080" inbound|8080|| 127.0.0.6:55401 10.244.0.13:8080 10.244.0.12:53336 outbound_.8000_._.httpbin.default.svc.cluster.local default
```


## Telemetry API support scope

For the Istio service mesh add-on for AKS, Telemetry API fields are classified as `allowed`

, `supported`

, and `blocked`

values. For more information about the Istio add-on's support policy for features and mesh configurations, see the Istio add-on [support policy document](istio-support-policy#allowed-supported-and-blocked-customizations).

The following Telemetry API configurations are either `allowed`

or `supported`

for the Istio add-on. Any field not included in this table is `blocked`

.

Telemetry API Field |
Supported/Allowed |
Notes |
|---|---|---|
`accessLogging.match` |
Supported | - |
`accessLogging.disabled` |
Supported | - |
`accessLogging.providers` |
Allowed | The default `envoy` access log provider is supported. For a managed experience for log collection and querying, see
`allowed` but unsupported. |
`metrics.overrides` |
Supported | - |
`metrics.providers` |
Allowed | Metrics collection with
`allowed` but unsupported. |

`tracing.*`

`allowed`

but unsupported.


---

<!-- DOCUMENTO FUSIONADO: ingress-basic.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/ingress-basic -->

# Create an unmanaged ingress controller

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

An ingress controller is a piece of software that provides reverse proxy, configurable traffic routing, and TLS termination for Kubernetes services. Kubernetes ingress resources are used to configure the ingress rules and routes for individual Kubernetes services. When you use an ingress controller and ingress rules, a single IP address can be used to route traffic to multiple services in a Kubernetes cluster.

This article shows you how to deploy the [NGINX ingress controller](https://github.com/kubernetes/ingress-nginx) in an Azure Kubernetes Service (AKS) cluster. Two applications are then run in the AKS cluster, each of which is accessible over the single IP address.

Important

The Application routing add-on is recommended for ingress in AKS. For more information, see [Managed nginx Ingress with the application routing add-on](/en-us/azure/aks/app-routing).

Note

There are two open source ingress controllers for Kubernetes based on Nginx: one is maintained by the Kubernetes community ([kubernetes/ingress-nginx](https://github.com/kubernetes/ingress-nginx)), and one is maintained by NGINX, Inc. ([nginxinc/kubernetes-ingress](https://github.com/nginxinc/kubernetes-ingress)). This article will be using the Kubernetes community ingress controller.

## Before you begin

- This article uses Helm 3 to install the NGINX ingress controller on a
[supported version of Kubernetes](/en-us/azure/aks/supported-kubernetes-versions). Make sure that you're using the latest release of Helm and have access to the*ingress-nginx*Helm repository. The steps outlined in this article may not be compatible with previous versions of the Helm chart, NGINX ingress controller, or Kubernetes. - This article assumes you have an existing AKS cluster with an integrated Azure Container Registry (ACR). For more information on creating an AKS cluster with an integrated ACR, see
[Authenticate with Azure Container Registry from Azure Kubernetes Service](/en-us/azure/aks/cluster-container-registry-integration#create-a-new-acr). - The Kubernetes API health endpoint,
`healthz`

was deprecated in Kubernetes v1.16. You can replace this endpoint with the`livez`

and`readyz`

endpoints instead. See[Kubernetes API endpoints for health](https://kubernetes.io/docs/reference/using-api/health-checks/#api-endpoints-for-health)to determine which endpoint to use for your scenario. - If you're using Azure CLI, this article requires that you're running the Azure CLI version 2.0.64 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI][azure-cli-install]. - If you're using Azure PowerShell, this article requires that you're running Azure PowerShell version 5.9.0 or later. Run
`Get-InstalledModule -Name Az`

to find the version. If you need to install or upgrade, see[Install Azure PowerShell](/en-us/powershell/azure/install-azure-powershell).

## Basic configuration

To create a basic NGINX ingress controller without customizing the defaults, you'll use Helm. The following configuration uses the default configuration for simplicity. You can add parameters for customizing the deployment, like `--set controller.replicaCount=3`

.

Note

If you would like to enable [client source IP preservation](/en-us/azure/aks/concepts-network-ingress#ingress-controllers) for requests to containers in your cluster, add `--set controller.service.externalTrafficPolicy=Local`

to the Helm install command. The client source IP is stored in the request header under *X-Forwarded-For*. When you're using an ingress controller with client source IP preservation enabled, TLS pass-through won't work.

```
NAMESPACE=ingress-basic
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install ingress-nginx ingress-nginx/ingress-nginx \
--create-namespace \
--namespace $NAMESPACE \
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz \
--set controller.service.externalTrafficPolicy=Local
```


Note

In this tutorial, `service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path`

is being set to `/healthz`

. This means if the response code of the requests to `/healthz`

is not `200`

, the entire ingress controller will be down. You can modify the value to other URI in your own scenario. You cannot delete this part or unset the value, or the ingress controller will still be down.
The package `ingress-nginx`

used in this tutorial, which is provided by [Kubernetes official](https://github.com/kubernetes/ingress-nginx), will always return `200`

response code if requesting `/healthz`

, as it is designed as [default backend](https://kubernetes.github.io/ingress-nginx/user-guide/default-backend/) for users to have a quick start, unless it is being overwritten by ingress rules.

## Customized configuration

As an alternative to the basic configuration presented in the above section, the next set of steps will show how to deploy a customized ingress controller. You'll have the option of using an internal static IP address, or using a dynamic public IP address.

### Import the images used by the Helm chart into your ACR

To control image versions, you'll want to import them into your own Azure Container Registry. The [NGINX ingress controller Helm chart](https://github.com/kubernetes/ingress-nginx/tree/main/charts/ingress-nginx) relies on three container images. Use `az acr import`

to import those images into your ACR.

```
REGISTRY_NAME=<REGISTRY_NAME>
SOURCE_REGISTRY=registry.k8s.io
CONTROLLER_IMAGE=ingress-nginx/controller
CONTROLLER_TAG=v1.8.1
PATCH_IMAGE=ingress-nginx/kube-webhook-certgen
PATCH_TAG=v20230407
DEFAULTBACKEND_IMAGE=defaultbackend-amd64
DEFAULTBACKEND_TAG=1.5
az acr import --name $REGISTRY_NAME --source $SOURCE_REGISTRY/$CONTROLLER_IMAGE:$CONTROLLER_TAG --image $CONTROLLER_IMAGE:$CONTROLLER_TAG
az acr import --name $REGISTRY_NAME --source $SOURCE_REGISTRY/$PATCH_IMAGE:$PATCH_TAG --image $PATCH_IMAGE:$PATCH_TAG
az acr import --name $REGISTRY_NAME --source $SOURCE_REGISTRY/$DEFAULTBACKEND_IMAGE:$DEFAULTBACKEND_TAG --image $DEFAULTBACKEND_IMAGE:$DEFAULTBACKEND_TAG
```


Note

In addition to importing container images into your ACR, you can also import Helm charts into your ACR. For more information, see [Push and pull Helm charts to an Azure Container Registry](/en-us/azure/container-registry/container-registry-helm-repos).

### Create an ingress controller

To create the ingress controller, use Helm to install *ingress-nginx*. The ingress controller needs to be scheduled on a Linux node. Windows Server nodes shouldn't run the ingress controller. A node selector is specified using the `--set nodeSelector`

parameter to tell the Kubernetes scheduler to run the NGINX ingress controller on a Linux-based node.

For added redundancy, two replicas of the NGINX ingress controllers are deployed with the `--set controller.replicaCount`

parameter. To fully benefit from running replicas of the ingress controller, make sure there's more than one node in your AKS cluster.

The following example creates a Kubernetes namespace for the ingress resources named *ingress-basic* and is intended to work within that namespace. Specify a namespace for your own environment as needed. If your AKS cluster isn't Kubernetes role-based access control enabled, add `--set rbac.create=false`

to the Helm commands.

Note

If you would like to enable [client source IP preservation](/en-us/azure/aks/concepts-network-ingress#ingress-controllers) for requests to containers in your cluster, add `--set controller.service.externalTrafficPolicy=Local`

to the Helm install command. The client source IP is stored in the request header under *X-Forwarded-For*. When you're using an ingress controller with client source IP preservation enabled, TLS pass-through won't work.

```
# Add the ingress-nginx repository
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
# Set variable for ACR location to use for pulling images
ACR_LOGIN_SERVER=<REGISTRY_LOGIN_SERVER>
# Use Helm to deploy an NGINX ingress controller
helm install ingress-nginx ingress-nginx/ingress-nginx \
--version 4.7.1 \
--namespace ingress-basic \
--create-namespace \
--set controller.replicaCount=2 \
--set controller.nodeSelector."kubernetes\.io/os"=linux \
--set controller.image.registry=$ACR_LOGIN_SERVER \
--set controller.image.image=$CONTROLLER_IMAGE \
--set controller.image.tag=$CONTROLLER_TAG \
--set controller.image.digest="" \
--set controller.admissionWebhooks.patch.nodeSelector."kubernetes\.io/os"=linux \
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz \
--set controller.service.externalTrafficPolicy=Local \
--set controller.admissionWebhooks.patch.image.registry=$ACR_LOGIN_SERVER \
--set controller.admissionWebhooks.patch.image.image=$PATCH_IMAGE \
--set controller.admissionWebhooks.patch.image.tag=$PATCH_TAG \
--set controller.admissionWebhooks.patch.image.digest="" \
--set defaultBackend.nodeSelector."kubernetes\.io/os"=linux \
--set defaultBackend.image.registry=$ACR_LOGIN_SERVER \
--set defaultBackend.image.image=$DEFAULTBACKEND_IMAGE \
--set defaultBackend.image.tag=$DEFAULTBACKEND_TAG \
--set defaultBackend.image.digest=""
```


### Create an ingress controller using an internal IP address

By default, an NGINX ingress controller is created with a dynamic public IP address assignment. A common configuration requirement is to use an internal, private network and IP address. This approach allows you to restrict access to your services to internal users, with no external access.

Use the `--set controller.service.loadBalancerIP`

and `--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-internal"=true`

parameters to assign an internal IP address to your ingress controller. Provide your own internal IP address for use with the ingress controller. Make sure that this IP address isn't already in use within your virtual network. If you're using an existing virtual network and subnet, you must configure your AKS cluster with the correct permissions to manage the virtual network and subnet. For more information, see [Use kubenet networking with your own IP address ranges in Azure Kubernetes Service (AKS)](/en-us/azure/aks/configure-kubenet) or [Configure Azure CNI networking in Azure Kubernetes Service (AKS)](/en-us/azure/aks/configure-azure-cni?tabs=configure-networking-portal).

```
# Add the ingress-nginx repository
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
# Set variable for ACR location to use for pulling images
ACR_LOGIN_SERVER=<REGISTRY_LOGIN_SERVER>
# Use Helm to deploy an NGINX ingress controller
helm install ingress-nginx ingress-nginx/ingress-nginx \
--version 4.7.1 \
--namespace ingress-basic \
--create-namespace \
--set controller.replicaCount=2 \
--set controller.nodeSelector."kubernetes\.io/os"=linux \
--set controller.image.registry=$ACR_LOGIN_SERVER \
--set controller.image.image=$CONTROLLER_IMAGE \
--set controller.image.tag=$CONTROLLER_TAG \
--set controller.image.digest="" \
--set controller.admissionWebhooks.patch.nodeSelector."kubernetes\.io/os"=linux \
--set controller.service.loadBalancerIP=10.224.0.42 \
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-internal"=true \
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz \
--set controller.admissionWebhooks.patch.image.registry=$ACR_LOGIN_SERVER \
--set controller.admissionWebhooks.patch.image.image=$PATCH_IMAGE \
--set controller.admissionWebhooks.patch.image.tag=$PATCH_TAG \
--set controller.admissionWebhooks.patch.image.digest="" \
--set defaultBackend.nodeSelector."kubernetes\.io/os"=linux \
--set defaultBackend.image.registry=$ACR_LOGIN_SERVER \
--set defaultBackend.image.image=$DEFAULTBACKEND_IMAGE \
--set defaultBackend.image.tag=$DEFAULTBACKEND_TAG \
--set defaultBackend.image.digest=""
```


## Check the load balancer service

Check the load balancer service by using `kubectl get services`

.

```
kubectl get services --namespace ingress-basic -o wide -w ingress-nginx-controller
```


When the Kubernetes load balancer service is created for the NGINX ingress controller, an IP address is assigned under *EXTERNAL-IP*, as shown in the following example output:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE SELECTOR
ingress-nginx-controller LoadBalancer 10.0.65.205 EXTERNAL-IP 80:30957/TCP,443:32414/TCP 1m app.kubernetes.io/component=controller,app.kubernetes.io/instance=ingress-nginx,app.kubernetes.io/name=ingress-nginx
```


If you browse to the external IP address at this stage, you see a 404 page displayed. This is because you still need to set up the connection to the external IP, which is done in the next sections.

## Run demo applications

To see the ingress controller in action, run two demo applications in your AKS cluster. In this example, you use `kubectl apply`

to deploy two instances of a simple *Hello world* application.

Create an

`aks-helloworld-one.yaml`

file and copy in the following example YAML:`apiVersion: apps/v1 kind: Deployment metadata: name: aks-helloworld-one spec: replicas: 1 selector: matchLabels: app: aks-helloworld-one template: metadata: labels: app: aks-helloworld-one spec: containers: - name: aks-helloworld-one image: mcr.microsoft.com/azuredocs/aks-helloworld:v1 ports: - containerPort: 80 env: - name: TITLE value: "Welcome to Azure Kubernetes Service (AKS)" --- apiVersion: v1 kind: Service metadata: name: aks-helloworld-one spec: type: ClusterIP ports: - port: 80 selector: app: aks-helloworld-one`

Create an

`aks-helloworld-two.yaml`

file and copy in the following example YAML:`apiVersion: apps/v1 kind: Deployment metadata: name: aks-helloworld-two spec: replicas: 1 selector: matchLabels: app: aks-helloworld-two template: metadata: labels: app: aks-helloworld-two spec: containers: - name: aks-helloworld-two image: mcr.microsoft.com/azuredocs/aks-helloworld:v1 ports: - containerPort: 80 env: - name: TITLE value: "AKS Ingress Demo" --- apiVersion: v1 kind: Service metadata: name: aks-helloworld-two spec: type: ClusterIP ports: - port: 80 selector: app: aks-helloworld-two`

Run the two demo applications using

`kubectl apply`

:`kubectl apply -f aks-helloworld-one.yaml --namespace ingress-basic kubectl apply -f aks-helloworld-two.yaml --namespace ingress-basic`


## Create an ingress route

Both applications are now running on your Kubernetes cluster. To route traffic to each application, create a Kubernetes ingress resource. The ingress resource configures the rules that route traffic to one of the two applications.

In the following example, traffic to *EXTERNAL_IP/hello-world-one* is routed to the service named `aks-helloworld-one`

. Traffic to *EXTERNAL_IP/hello-world-two* is routed to the `aks-helloworld-two`

service. Traffic to *EXTERNAL_IP/static* is routed to the service named `aks-helloworld-one`

for static assets.

Create a file named

`hello-world-ingress.yaml`

and copy in the following example YAML:`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: hello-world-ingress annotations: nginx.ingress.kubernetes.io/ssl-redirect: "false" nginx.ingress.kubernetes.io/use-regex: "true" nginx.ingress.kubernetes.io/rewrite-target: /$2 spec: ingressClassName: nginx rules: - http: paths: - path: /hello-world-one(/|$)(.*) pathType: Prefix backend: service: name: aks-helloworld-one port: number: 80 - path: /hello-world-two(/|$)(.*) pathType: Prefix backend: service: name: aks-helloworld-two port: number: 80 - path: /(.*) pathType: Prefix backend: service: name: aks-helloworld-one port: number: 80 --- apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: hello-world-ingress-static annotations: nginx.ingress.kubernetes.io/ssl-redirect: "false" nginx.ingress.kubernetes.io/rewrite-target: /static/$2 spec: ingressClassName: nginx rules: - http: paths: - path: /static(/|$)(.*) pathType: Prefix backend: service: name: aks-helloworld-one port: number: 80`

Create the ingress resource using the

`kubectl apply`

command.`kubectl apply -f hello-world-ingress.yaml --namespace ingress-basic`


## Test the ingress controller

To test the routes for the ingress controller, browse to the two applications. Open a web browser to the IP address of your NGINX ingress controller, such as *EXTERNAL_IP*. The first demo application is displayed in the web browser, as shown in the following example:

Now add the */hello-world-two* path to the IP address, such as *EXTERNAL_IP/hello-world-two*. The second demo application with the custom title is displayed:

### Test an internal IP address

Create a test pod and attach a terminal session to it.

`kubectl run -it --rm aks-ingress-test --image=mcr.microsoft.com/dotnet/runtime-deps:6.0 --namespace ingress-basic`

Install

`curl`

in the pod using`apt-get`

.`apt-get update && apt-get install -y curl`

Access the address of your Kubernetes ingress controller using

`curl`

, such as. Provide your own internal IP address specified when you deployed the ingress controller.[http://10.224.0.42](http://10.224.0.42)`curl -L http://10.224.0.42`

No path was provided with the address, so the ingress controller defaults to the

*/*route. The first demo application is returned, as shown in the following condensed example output:`<!DOCTYPE html> <html xmlns="http://www.w3.org/1999/xhtml"> <head> <link rel="stylesheet" type="text/css" href="/static/default.css"> <title>Welcome to Azure Kubernetes Service (AKS)</title> [...]`

Add the

*/hello-world-two*path to the address, such as.[http://10.224.0.42/hello-world-two](http://10.224.0.42/hello-world-two)`curl -L -k http://10.224.0.42/hello-world-two`

The second demo application with the custom title is returned, as shown in the following condensed example output:

`<!DOCTYPE html> <html xmlns="http://www.w3.org/1999/xhtml"> <head> <link rel="stylesheet" type="text/css" href="/static/default.css"> <title>AKS Ingress Demo</title> [...]`


## Clean up resources

This article used Helm to install the ingress components and sample apps. When you deploy a Helm chart, many Kubernetes resources are created. These resources include pods, deployments, and services. To clean up these resources, you can either delete the entire sample namespace, or the individual resources.

### Delete the sample namespace and all resources

To delete the entire sample namespace, use the `kubectl delete`

command and specify your namespace name. All the resources in the namespace are deleted.

```
kubectl delete namespace ingress-basic
```


### Delete resources individually

Alternatively, a more granular approach is to delete the individual resources created.

List the Helm releases with the

`helm list`

command.`helm list --namespace ingress-basic`

Look for charts named

*ingress-nginx*and*aks-helloworld*, as shown in the following example output:`NAME NAMESPACE REVISION UPDATED STATUS CHART APP VERSION ingress-nginx ingress-basic 1 2020-01-06 19:55:46.358275 -0600 CST deployed nginx-ingress-1.27.1 0.26.1`

Uninstall the releases with the

`helm uninstall`

command.`helm uninstall ingress-nginx --namespace ingress-basic`

Remove the two sample applications.

`kubectl delete -f aks-helloworld-one.yaml --namespace ingress-basic kubectl delete -f aks-helloworld-two.yaml --namespace ingress-basic`

Remove the ingress route that directed traffic to the sample apps.

`kubectl delete -f hello-world-ingress.yaml`

Delete the namespace using the

`kubectl delete`

command and specifying your namespace name.`kubectl delete namespace ingress-basic`


## Next steps

To configure TLS with your existing ingress components, see [Use TLS with an ingress controller](/en-us/previous-versions/azure/aks/ingress-tls).

To configure your AKS cluster to use application routing, see [Application routing add-on](/en-us/azure/aks/app-routing).

This article included some external components to AKS. To learn more about these components, see the following project pages:


---

<!-- DOCUMENTO FUSIONADO: _csi-migrate-in-tree-volumes__localdns-custom_container-network-observability-me_016e93.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: csi-migrate-in-tree-volumes.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/csi-migrate-in-tree-volumes -->

# Migrate from in-tree storage class to CSI drivers on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The implementation of the [Container Storage Interface (CSI) driver](csi-storage-drivers) was introduced in Azure Kubernetes Service (AKS) starting with version 1.21. By adopting and using CSI as the standard, your existing stateful workloads using in-tree Persistent Volumes (PVs) should be migrated or upgraded to use the CSI driver.

To make this process as simple as possible, and to ensure no data loss, this article provides different migration options. These options include scripts to help ensure a smooth migration from in-tree to Azure Disks and Azure Files CSI drivers.

## Before you begin

- The Azure CLI version 2.37.0 or later. Run
`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - Kubectl and cluster administrators have access to create, get, list, delete access to a PVC or PV, volume snapshot, or volume snapshot content. For a Microsoft Entra RBAC enabled cluster, you're a member of the
[Azure Kubernetes Service RBAC Cluster Admin](manage-azure-rbac#create-role-assignments-for-cluster-access)role.

## Migrate Disk volumes

Note

The labels `failure-domain.beta.kubernetes.io/zone`

and `failure-domain.beta.kubernetes.io/region`

have been deprecated in AKS 1.24 and removed in 1.28. If your existing persistent volumes are still using nodeAffinity matching these two labels, you need to change them to `topology.kubernetes.io/zone`

and `topology.kubernetes.io/region`

labels in the new persistent volume setting.

Migration from in-tree to CSI is supported using two migration options:

- Create a static volume
- Create a dynamic volume

### Create a static volume

Using this option, you create a PV by statically assigning `claimRef`

to a new PVC that you'll create later, and specify the `volumeName`

for the *PersistentVolumeClaim*.


The benefits of this approach are:

- It's simple and can be automated.
- No need to clean up original configuration using in-tree storage class.
- Low risk as you're only performing a logical deletion of Kubernetes PV/PVC, the actual physical data isn't deleted.
- No extra cost incurred as the result of not having to create additional Azure objects, such as disk, snapshots, etc.

The following are important considerations to evaluate:

- Transition to static volumes from original dynamic-style volumes requires constructing and managing PV objects manually for all options.
- Potential application downtime when redeploying the new application with reference to the new PVC object.

#### Migration

Update the existing PV

`ReclaimPolicy`

from**Delete**to**Retain**by running the following command:`kubectl patch pv pvName -p '{"spec":{"persistentVolumeReclaimPolicy":"Retain"}}'`

Replace

**pvName**with the name of your selected PersistentVolume. Alternatively, if you want to update the reclaimPolicy for multiple PVs, create a file named**patchReclaimPVs.sh**and copy in the following code.`#!/bin/bash # Patch the Persistent Volume in case ReclaimPolicy is Delete NAMESPACE=$1 i=1 for PVC in $(kubectl get pvc -n $NAMESPACE | awk '{ print $1}'); do # Ignore first record as it contains header if [ $i -eq 1 ]; then i=$((i + 1)) else PV="$(kubectl get pvc $PVC -n $NAMESPACE -o jsonpath='{.spec.volumeName}')" RECLAIMPOLICY="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.persistentVolumeReclaimPolicy}')" echo "Reclaim Policy for Persistent Volume $PV is $RECLAIMPOLICY" if [[ $RECLAIMPOLICY == "Delete" ]]; then echo "Updating ReclaimPolicy for $pv to Retain" kubectl patch pv $PV -p '{"spec":{"persistentVolumeReclaimPolicy":"Retain"}}' fi fi done`

Execute the script with the

`namespace`

parameter to specify the cluster namespace`./PatchReclaimPolicy.sh <namespace>`

.Get a list of all of the PVCs in namespace sorted by

**creationTimestamp**by running the following command. Set the namespace using the`--namespace`

argument along with the actual cluster namespace.`kubectl get pvc -n <namespace> --sort-by=.metadata.creationTimestamp -o custom-columns=NAME:.metadata.name,CreationTime:.metadata.creationTimestamp,StorageClass:.spec.storageClassName,Size:.spec.resources.requests.storage`

This step is helpful if you have a large number of PVs that need to be migrated, and you want to migrate a few at a time. Running this command enables you to identify which PVCs were created in a given time frame. When you run the

*CreatePV.sh*script, two of the parameters are start time and end time that enable you to only migrate the PVCs during that period of time.Create a file named

**CreatePV.sh**and copy in the following code. The script does the following:- Creates a new PersistentVolume with name
`existing-pv-csi`

for all PersistentVolumes in namespaces for storage class`storageClassName`

. - Configure new PVC name as
`existing-pvc-csi`

. - Creates a new PVC with the PV name you specify.

`#!/bin/bash #kubectl get pvc -n <namespace> --sort-by=.metadata.creationTimestamp -o custom-columns=NAME:.metadata.name,CreationTime:.metadata.creationTimestamp,StorageClass:.spec.storageClassName,Size:.spec.resources.requests.storage # TimeFormat 2022-04-20T13:19:56Z NAMESPACE=$1 FILENAME=$(date +%Y%m%d%H%M)-$NAMESPACE EXISTING_STORAGE_CLASS=$2 STORAGE_CLASS_NEW=$3 STARTTIMESTAMP=$4 ENDTIMESTAMP=$5 i=1 for PVC in $(kubectl get pvc -n $NAMESPACE | awk '{ print $1}'); do # Ignore first record as it contains header if [ $i -eq 1 ]; then i=$((i + 1)) else PVC_CREATION_TIME=$(kubectl get pvc $PVC -n $NAMESPACE -o jsonpath='{.metadata.creationTimestamp}') if [[ $PVC_CREATION_TIME >= $STARTTIMESTAMP ]]; then if [[ $ENDTIMESTAMP > $PVC_CREATION_TIME ]]; then PV="$(kubectl get pvc $PVC -n $NAMESPACE -o jsonpath='{.spec.volumeName}')" RECLAIM_POLICY="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.persistentVolumeReclaimPolicy}')" STORAGECLASS="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.storageClassName}')" echo $PVC RECLAIM_POLICY="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.persistentVolumeReclaimPolicy}')" if [[ $RECLAIM_POLICY == "Retain" ]]; then if [[ $STORAGECLASS == $EXISTING_STORAGE_CLASS ]]; then STORAGE_SIZE="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.capacity.storage}')" SKU_NAME="$(kubectl get storageClass $STORAGE_CLASS_NEW -o jsonpath='{.parameters.skuname}')" DISK_URI="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.azureDisk.diskURI}')" PERSISTENT_VOLUME_RECLAIM_POLICY="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.persistentVolumeReclaimPolicy}')" cat >$PVC-csi.yaml <<EOF apiVersion: v1 kind: PersistentVolume metadata: annotations: pv.kubernetes.io/provisioned-by: disk.csi.azure.com name: $PV-csi spec: accessModes: - ReadWriteOnce capacity: storage: $STORAGE_SIZE claimRef: apiVersion: v1 kind: PersistentVolumeClaim name: $PVC-csi namespace: $NAMESPACE csi: driver: disk.csi.azure.com volumeAttributes: csi.storage.k8s.io/pv/name: $PV-csi csi.storage.k8s.io/pvc/name: $PVC-csi csi.storage.k8s.io/pvc/namespace: $NAMESPACE requestedsizegib: "$STORAGE_SIZE" skuname: $SKU_NAME volumeHandle: $DISK_URI persistentVolumeReclaimPolicy: $PERSISTENT_VOLUME_RECLAIM_POLICY storageClassName: $STORAGE_CLASS_NEW --- apiVersion: v1 kind: PersistentVolumeClaim metadata: name: $PVC-csi namespace: $NAMESPACE spec: accessModes: - ReadWriteOnce storageClassName: $STORAGE_CLASS_NEW resources: requests: storage: $STORAGE_SIZE volumeName: $PV-csi EOF kubectl apply -f $PVC-csi.yaml LINE="PVC:$PVC,PV:$PV,StorageClassTarget:$STORAGE_CLASS_NEW" printf '%s\n' "$LINE" >>$FILENAME fi fi fi fi fi done`

- Creates a new PersistentVolume with name
To create a new PersistentVolume for all PersistentVolumes in the namespace, execute the script

**CreatePV.sh**with the following parameters:`namespace`

- The cluster namespace`sourceStorageClass`

- The in-tree storage driver-based StorageClass`targetCSIStorageClass`

- The CSI storage driver-based StorageClass, which can be either one of the default storage classes that have the provisioner set to**disk.csi.azure.com**or**file.csi.azure.com**. Or you can create a custom storage class as long as it is set to either one of those two provisioners.`startTimeStamp`

- Provide a start time**before**PVC creation time in the format**yyyy-mm-ddthh:mm:ssz**`endTimeStamp`

- Provide an end time in the format**yyyy-mm-ddthh:mm:ssz**.

`./CreatePV.sh <namespace> <sourceIntreeStorageClass> <targetCSIStorageClass> <startTimestamp> <endTimestamp>`

Update your application to use the new PVC.


### Create a dynamic volume

Using this option, you dynamically create a Persistent Volume from a Persistent Volume Claim.


The benefits of this approach are:

It's less risky because all new objects are created while retaining other copies with snapshots.

No need to construct PVs separately and add volume name in PVC manifest.


The following are important considerations to evaluate:

While this approach is less risky, it does create multiple objects that will increase your storage costs.

During creation of the new volume(s), your application is unavailable.

Deletion steps should be performed with caution. Temporary

[resource locks](/en-us/azure/azure-resource-manager/management/lock-resources)can be applied to your resource group until migration is completed and your application is successfully verified.Perform data validation/verification as new disks are created from snapshots.


#### Migration

Before proceeding, verify the following:

For specific workloads where data is written to memory before being written to disk, the application should be stopped and to allow in-memory data to be flushed to disk.

`VolumeSnapshot`

class should exist as shown in the following example YAML:`apiVersion: snapshot.storage.k8s.io/v1 kind: VolumeSnapshotClass metadata: name: custom-disk-snapshot-sc driver: disk.csi.azure.com deletionPolicy: Delete parameters: incremental: "false"`


Get list of all the PVCs in a specified namespace sorted by

*creationTimestamp*by running the following command. Set the namespace using the`--namespace`

argument along with the actual cluster namespace.`kubectl get pvc --namespace <namespace> --sort-by=.metadata.creationTimestamp -o custom-columns=NAME:.metadata.name,CreationTime:.metadata.creationTimestamp,StorageClass:.spec.storageClassName,Size:.spec.resources.requests.storage`

This step is helpful if you have a large number of PVs that need to be migrated, and you want to migrate a few at a time. Running this command enables you to identify which PVCs were created in a given time frame. When you run the

*MigrateCSI.sh*script, two of the parameters are start time and end time that enable you to only migrate the PVCs during that period of time.Create a file named

**MigrateToCSI.sh**and copy in the following code. The script does the following:- Creates a full disk snapshot using the Azure CLI
- Creates
`VolumesnapshotContent`

- Creates
`VolumeSnapshot`

- Creates a new PVC from
`VolumeSnapshot`

- Creates a new file with the filename
`<namespace>-timestamp`

, which contains a list of all old resources that needs to be cleaned up.

`#!/bin/bash #kubectl get pvc -n <namespace> --sort-by=.metadata.creationTimestamp -o custom-columns=NAME:.metadata.name,CreationTime:.metadata.creationTimestamp,StorageClass:.spec.storageClassName,Size:.spec.resources.requests.storage # TimeFormat 2022-04-20T13:19:56Z NAMESPACE=$1 FILENAME=$NAMESPACE-$(date +%Y%m%d%H%M) EXISTING_STORAGE_CLASS=$2 STORAGE_CLASS_NEW=$3 VOLUME_STORAGE_CLASS=$4 START_TIME_STAMP=$5 END_TIME_STAMP=$6 i=1 for PVC in $(kubectl get pvc -n $NAMESPACE | awk '{ print $1}'); do # Ignore first record as it contains header if [ $i -eq 1 ]; then i=$((i + 1)) else PVC_CREATION_TIME=$(kubectl get pvc $PVC -n $NAMESPACE -o jsonpath='{.metadata.creationTimestamp}') if [[ $PVC_CREATION_TIME > $START_TIME_STAMP ]]; then if [[ $END_TIME_STAMP > $PVC_CREATION_TIME ]]; then PV="$(kubectl get pvc $PVC -n $NAMESPACE -o jsonpath='{.spec.volumeName}')" RECLAIM_POLICY="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.persistentVolumeReclaimPolicy}')" STORAGE_CLASS="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.storageClassName}')" echo $PVC RECLAIM_POLICY="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.persistentVolumeReclaimPolicy}')" if [[ $STORAGE_CLASS == $EXISTING_STORAGE_CLASS ]]; then STORAGE_SIZE="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.capacity.storage}')" SKU_NAME="$(kubectl get storageClass $STORAGE_CLASS_NEW -o jsonpath='{.parameters.skuname}')" DISK_URI="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.azureDisk.diskURI}')" TARGET_RESOURCE_GROUP="$(cut -d'/' -f5 <<<"$DISK_URI")" echo $DISK_URI SUBSCRIPTION_ID="$(echo $DISK_URI | grep -o 'subscriptions/[^/]*' | sed 's#subscriptions/##g')" echo $TARGET_RESOURCE_GROUP PERSISTENT_VOLUME_RECLAIM_POLICY="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.persistentVolumeReclaimPolicy}')" az snapshot create --resource-group $TARGET_RESOURCE_GROUP --name $PVC-$FILENAME --source "$DISK_URI" --subscription ${SUBSCRIPTION_ID} SNAPSHOT_PATH=$(az snapshot list --resource-group $TARGET_RESOURCE_GROUP --query "[?name == '$PVC-$FILENAME'].id | [0]" --subscription ${SUBSCRIPTION_ID}) SNAPSHOT_HANDLE=$(echo "$SNAPSHOT_PATH" | tr -d '"') echo $SNAPSHOT_HANDLE sleep 10 # Create Restore File cat <<EOF >$PVC-csi.yml apiVersion: snapshot.storage.k8s.io/v1 kind: VolumeSnapshotContent metadata: name: $PVC-$FILENAME spec: deletionPolicy: 'Delete' driver: 'disk.csi.azure.com' volumeSnapshotClassName: $VOLUME_STORAGE_CLASS source: snapshotHandle: $SNAPSHOT_HANDLE volumeSnapshotRef: apiVersion: snapshot.storage.k8s.io/v1 kind: VolumeSnapshot name: $PVC-$FILENAME namespace: $1 --- apiVersion: snapshot.storage.k8s.io/v1 kind: VolumeSnapshot metadata: name: $PVC-$FILENAME namespace: $1 spec: volumeSnapshotClassName: $VOLUME_STORAGE_CLASS source: volumeSnapshotContentName: $PVC-$FILENAME --- apiVersion: v1 kind: PersistentVolumeClaim metadata: name: csi-$PVC namespace: $1 spec: accessModes: - ReadWriteOnce storageClassName: $STORAGE_CLASS_NEW resources: requests: storage: $STORAGE_SIZE dataSource: name: $PVC-$FILENAME kind: VolumeSnapshot apiGroup: snapshot.storage.k8s.io EOF kubectl create -f $PVC-csi.yml LINE="OLDPVC:$PVC,OLDPV:$PV,VolumeSnapshotContent:volumeSnapshotContent-$FILENAME,VolumeSnapshot:volumesnapshot$FILENAME,OLDdisk:$DISK_URI" printf '%s\n' "$LINE" >>$FILENAME fi fi fi fi done`

To migrate the disk volumes, execute the script

**MigrateToCSI.sh**with the following parameters:`namespace`

- The cluster namespace`sourceStorageClass`

- The in-tree storage driver-based StorageClass`targetCSIStorageClass`

- The CSI storage driver-based StorageClass`volumeSnapshotClass`

- Name of the volume snapshot class. For example,`custom-disk-snapshot-sc`

.`startTimeStamp`

- Provide a start time in the format**yyyy-mm-ddthh:mm:ssz**.`endTimeStamp`

- Provide an end time in the format**yyyy-mm-ddthh:mm:ssz**.

`./MigrateToCSI.sh <namespace> <sourceStorageClass> <TargetCSIstorageClass> <VolumeSnapshotClass> <startTimestamp> <endTimestamp>`

Update your application to use the new PVC.

Manually delete the older resources including in-tree PVC/PV, VolumeSnapshot, and VolumeSnapshotContent. Otherwise, maintaining the in-tree PVC/PC and snapshot objects will generate more cost.


## Migrate File share volumes

Migration from in-tree to CSI is supported by creating a static volume:

- No need to clean up original configuration using in-tree storage class.
- Low risk as you're only performing a logical deletion of Kubernetes PV/PVC, the actual physical data isn't deleted.
- No extra cost incurred as the result of not having to create additional Azure objects, such as file shares, etc.

### Migration

Update the existing PV

`ReclaimPolicy`

from**Delete**to**Retain**by running the following command:`kubectl patch pv pvName -p '{"spec":{"persistentVolumeReclaimPolicy":"Retain"}}'`

Replace

**pvName**with the name of your selected PersistentVolume. Alternatively, if you want to update the reclaimPolicy for multiple PVs, create a file named**patchReclaimPVs.sh**and copy in the following code.`#!/bin/bash # Patch the Persistent Volume in case ReclaimPolicy is Delete namespace=$1 i=1 for pvc in $(kubectl get pvc -n $namespace | awk '{ print $1}'); do # Ignore first record as it contains header if [ $i -eq 1 ]; then i=$((i + 1)) else pv="$(kubectl get pvc $pvc -n $namespace -o jsonpath='{.spec.volumeName}')" reclaimPolicy="$(kubectl get pv $pv -n $namespace -o jsonpath='{.spec.persistentVolumeReclaimPolicy}')" echo "Reclaim Policy for Persistent Volume $pv is $reclaimPolicy" if [[ $reclaimPolicy == "Delete" ]]; then echo "Updating ReclaimPolicy for $pv to Retain" kubectl patch pv $pv -p '{"spec":{"persistentVolumeReclaimPolicy":"Retain"}}' fi fi done`

Execute the script with the

`namespace`

parameter to specify the cluster namespace`./PatchReclaimPolicy.sh <namespace>`

.Create a new Storage Class with the provisioner set to

`file.csi.azure.com`

, or you can use one of the default StorageClasses with the CSI file provisioner.Get the

`secretName`

and`shareName`

from the existing*PersistentVolumes*by running the following command:`kubectl describe pv pvName`

Create a new PV using the new StorageClass, and the

`shareName`

and`secretName`

from the in-tree PV. Create a file named*azurefile-mount-pv.yaml*and copy in the following code. Under`csi`

, update`resourceGroup`

,`volumeHandle`

, and`shareName`

. For mount options, the default value for*fileMode*and*dirMode*is*0777*.The default value for

`fileMode`

and`dirMode`

is**0777**.`apiVersion: v1 kind: PersistentVolume metadata: annotations: pv.kubernetes.io/provisioned-by: file.csi.azure.com name: azurefile spec: capacity: storage: 5Gi accessModes: - ReadWriteMany persistentVolumeReclaimPolicy: Retain storageClassName: azurefile-csi csi: driver: file.csi.azure.com readOnly: false volumeHandle: "{resource-group-name}#{account-name}#{file-share-name}" # make sure this volumeid is unique for every identical share in the cluster volumeAttributes: resourceGroup: EXISTING_RESOURCE_GROUP_NAME # optional, only set this when storage account is not in the same resource group as the cluster nodes shareName: aksshare nodeStageSecretRef: name: azure-secret namespace: default mountOptions: - dir_mode=0777 - file_mode=0777 - uid=0 - gid=0 - mfsymlinks - cache=strict - nosharesock - nobrl # disable sending byte range lock requests to the server and for applications which have challenges with posix locks`

Create a file named

*azurefile-mount-pvc.yaml*file with a*PersistentVolumeClaim*that uses the*PersistentVolume*using the following code.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: azurefile spec: accessModes: - ReadWriteMany storageClassName: azurefile-csi volumeName: azurefile resources: requests: storage: 5Gi`

Use the

`kubectl`

command to create the*PersistentVolume*.`kubectl apply -f azurefile-mount-pv.yaml`

Use the

`kubectl`

command to create the*PersistentVolumeClaim*.`kubectl apply -f azurefile-mount-pvc.yaml`

Verify your

*PersistentVolumeClaim*is created and bound to the*PersistentVolume*by running the following command.`kubectl get pvc azurefile`

The output resembles the following:

`NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE azurefile Bound azurefile 5Gi RWX azurefile 5s`

Update your container spec to reference your

*PersistentVolumeClaim*and update your pod. For example, copy the following code and create a file named*azure-files-pod.yaml*.`... volumes: - name: azure persistentVolumeClaim: claimName: azurefile`

The pod spec can't be updated in place. Use the following

`kubectl`

commands to delete and then re-create the pod.`kubectl delete pod mypod`

`kubectl apply -f azure-files-pod.yaml`


## Next steps

- For more information about storage best practices, see
[Best practices for storage and backups in Azure Kubernetes Service](operator-best-practices-storage). - Protect your newly migrated CSI Driver based PVs by
[backing them up using Azure Backup for AKS](/en-us/azure/backup/azure-kubernetes-service-cluster-backup).


---

<!-- DOCUMENTO FUSIONADO: _localdns-custom_container-network-observability-metrics.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: localdns-custom.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/localdns-custom -->

# Configure LocalDNS in Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

LocalDNS is a feature in Azure Kubernetes Service (AKS) designed to enhance the Domain Name System (DNS) resolution performance and resiliency for workloads running in your cluster. When you deploy a DNS proxy on each node, LocalDNS reduces DNS query latency, improves reliability during network disruptions, and provides advanced configuration options for DNS caching and forwarding. This article explains how LocalDNS works, its configuration options, and how to enable, verify, and troubleshoot LocalDNS in your AKS clusters.

To learn about what LocalDNS is, including architecture details, and key capabilities, refer to [DNS Resolution in Azure Kubernetes Service (AKS)](dns-concepts).

## Best practices for LocalDNS configuration

When implementing LocalDNS in your AKS clusters, consider the following best practices:

**Start with a minimal configuration**: Begin with a simple configuration that uses the`Preferred`

mode before moving to`Required`

mode. This setup allows you to validate that LocalDNS works as expected without breaking your cluster.**Implement proper caching strategies**: Configure cache settings based on your workload characteristics:- For frequently changing records, use shorter
`cacheDurationInSeconds`

values. When doing so, it's important to note that cacheDurationInSeconds acts as a cap on the DNS record TTL but doesn't increase it. The resulting TTL is the smaller of what is returned from upstream or what is set in the cache plugin. - For stable records, use longer cache durations to reduce DNS queries.
- Enable
`serveStale`

with appropriate settings to maintain service during DNS outages. - Caching with LocalDNS operates on a best effort basis and doesn't guarantee stale responses. The cache is divided into 256 shards and with a default maximum of 10,000 entries, allowing each shard to hold about 39 entries. When a shard is full and a new entry needs to be added, one of the existing entries is chosen at random to be evicted. There's no preference for older or expires entries. As a result, a stale record might not always be available, especially under high query volume.

- For frequently changing records, use shorter
**Monitor DNS performance**: After enabling LocalDNS, monitor your application's DNS performance using:- Application performance metrics.
- Node metrics to detect reduced network pressure.
- Log entries when
`queryLogging`

is set to`Log`

.

**Follow least privilege principle**: When configuring DNS forwarding rules, only allow access to the required DNS servers and domains.**Test before production deployment**: Always test LocalDNS configuration in a nonproduction environment before rolling it out to production clusters.**Use Infrastructure as Code (IaC)**: Store your*localdnsconfig.json*file in your infrastructure repository and include it in your AKS deployment templates.**Network configuration for TCP forwarding**: When using TCP for DNS forwarding to VnetDNS, ensure that your Network Security Groups (NSGs), firewalls, or Network Virtual Appliances (NVAs) don't block TCP traffic between CoreDNS/LocalDNS and VnetDNS servers.**Avoid enabling both NodeLocal DNSCache and LocalDNS**: It isn't recommended to enable both the upstream Kubernetes NodeLocal DNSCache and LocalDNS in your node pool. While AKS doesn't block this configuration, all DNS traffic is routed through LocalDNS, which might lead to unexpected behavior or reduced benefits from NodeLocal DNSCache.

## Prerequisites

- You must have an existing AKS cluster with Kubernetes versions 1.31 or later to use LocalDNS. If you need an AKS cluster, you can create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - This article requires version 2.80.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed.
- LocalDNS is only supported on node pools running Azure Linux or Ubuntu 22.04 or newer.
- The Virtual Machine (VM) SKU used for your node pool must have at least 4 vCPUs (cores) to support LocalDNS.
- LocalDNS isn't compatible with
[applied FQDN filter policies in Advanced Container Networking Services (ACNS)](how-to-apply-fqdn-filtering-policies).

## Manage LocalDNS on an AKS cluster

LocalDNS is configured at the node pool level in AKS, meaning you can enable or disable LocalDNS independently for each node pool in your cluster. This tailors DNS resolution behavior based on the specific requirements of different workloads or environments. To enable LocalDNS on a node pool, you need to provide a configuration file: *localdnsconfig.json* that defines how LocalDNS should operate for that node pool.

If you don't specify a custom configuration file, AKS automatically applies a default LocalDNS configuration.

Note

If you're using Node Auto-Provisioning (NAP), see [LocalDNS configuration](node-auto-provisioning-aksnodeclass#localdns-configuration) for instructions on how to enable LocalDNS with NAP.

To enable LocalDNS during node pool creation, use the following command with your custom configuration file:

```
az aks nodepool add --name mynodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --localdns-config ./localdnsconfig.json
```


To enable LocalDNS on an existing node pool, use the following command with your custom configuration file:

```
az aks nodepool update --name mynodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --localdns-config ./localdnsconfig.json
```


Important

Enabling LocalDNS on a node pool initiates a reimage operation on all nodes within that pool. This process can cause temporary disruption to running workloads and might lead to application downtime if not properly managed. You should plan for potential service interruptions and ensure that the applications are configured for high availability or have appropriate disruption budgets in place before enabling this setting.

## Create a custom server block in LocalDNS

CoreDNS matches queries to a specific server block based on an exact match for domain being queried and not on partial matches. If you have the need for custom server blocks, you can add them to your LocalDNS configuration by creating a file called *localdnsconfig.json* with the added configurations.

For example, if you have specific DNS needs when accessing microsoft.com, you could use the following server block:

```
"microsoft.com": {
"queryLogging": "Error",
"protocol": "ForceTCP",
"forwardDestination": "ClusterCoreDNS",
"forwardPolicy": "Sequential",
"maxConcurrent": 1000,
"cacheDurationInSeconds": 3600,
"serveStaleDurationInSeconds": 3600,
"serveStale": "Immediate"
}
```


## Monitor LocalDNS

LocalDNS exposes Prometheus metrics that you can use for monitoring and alerting. These [metrics](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-default#coredns) are exposed on port `9253`

of the Node IP and can be scraped from there.

The following example YAML shows a scrape configuration you can use with the [Azure Managed Prometheus add on as a DaemonSet](/en-us/azure/azure-monitor/essentials/prometheus-metrics-scrape-configuration):

```
kind: ConfigMap
apiVersion: v1
metadata:
name: ama-metrics-prometheus-config-node
namespace: kube-system
data:
prometheus-config: |-
global:
scrape_interval: 1m
scrape_configs:
- job_name: localdns-metrics
scrape_interval: 1m
scheme: http
metrics_path: /metrics
relabel_configs:
- source_labels: [__metrics_path__]
regex: (.*)
target_label: metrics_path
- source_labels: [__address__]
replacement: '$NODE_NAME'
target_label: instance
static_configs:
- targets: ['$NODE_IP:9253']
```


## Troubleshoot LocalDNS

### DNS queries to specific domains are failing

If DNS queries to specific domains are failing after enabling LocalDNS:

- Check if you have domain-specific overrides in your
*localdnsconfig.json*that might be misconfigured. - Temporarily try removing domain-specific overrides and using only the default
`.`

configuration. - Check if the issue occurs with both User Datagram Protocol (UDP) and Transmission Control Protocol (TCP) by adjusting the
`protocol`

setting.

### Update VNet DNS servers for LocalDNS

When you update custom DNS servers directly in the VNet configuration (using the Azure portal or CLI), these changes aren't automatically applied to your AKS cluster nodes. This happens because updating DNS settings at the VNet level only informs the Network Resource Provider (NRP), but doesn't notify the AKS Resource Provider. As a result, AKS nodes continue to use the previous DNS server settings until further action is taken.

To ensure AKS nodes pick up the new VNet DNS server settings:

Update the VNet DNS configuration using the Azure portal or APIs as needed.

Reimage the node pool through the AKS Resource Provider to apply and persist the DNS changes:

`az aks nodepool upgrade --resource-group myResourceGroup --cluster-name myAKSCluster --name mynodepool --node-image-only`


This process ensures the AKS Resource Provider is aware of the DNS changes and applies them to all nodes in the node pool.

## Next steps

For information on LocalDNS in AKS, see [LocalDNS in Azure Kubernetes Service (conceptual)](dns-concepts).

For comprehensive troubleshooting guidance on DNS issues when using LocalDNS, see [Troubleshoot LocalDNS issues in AKS](/en-us/troubleshoot/azure/azure-kubernetes/connectivity/dns/troubleshoot-localdns).

For details on how to customize CoreDNS in AKS, refer to the [CoreDNS customization guide](coredns-custom).

For information on the CoreDNS project, see [the CoreDNS upstream project page](https://coredns.io/).

To learn more about core network concepts, see [Network concepts for applications in AKS](concepts-network).


---

<!-- DOCUMENTO FUSIONADO: container-network-observability-metrics.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-metrics -->

# What is container network metrics?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Advanced Container Networking Services in Azure Kubernetes Service (AKS) facilitates the collection of comprehensive container network metrics to give you valuable insights into the performance of your containerized environment. The capability continuously captures essential metrics at the node level and pod level, including traffic volume, dropped packets, connection states, and Domain Name System (DNS) resolution times for effective monitoring and optimizing network performance.

Capturing these metrics is essential for understanding how containers communicate, how traffic flows between services, and where bottlenecks or disruptions might occur. Advanced Container Networking Services integrates seamlessly with monitoring tools like Prometheus and Grafana to give you a complete view of networking metrics. Use the metrics for in-depth troubleshooting, network optimization, and performance tuning.

In a cloud-native world, maintaining a healthy and efficient network in a dynamic containerized environment is vital to ensuring that applications perform as expected. Without proper visibility into network traffic and its patterns, identifying potential issues or inefficiencies becomes challenging.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Key benefits

Deep visibility into network performance

Enhanced troubleshooting and optimization

Proactive anomaly detection

Better resource management and scaling

Capacity planning and compliance

Source-level metrics filtering for cost optimization and noise reduction with

[container network metrics filtering](#container-network-metrics-filtering-preview)Simplified metrics storage and visualization options. Choose between:

**Azure managed service for Prometheus and Azure Managed Grafana**: Azure manages the infrastructure and maintenance, so you can focus on configuring metrics and visualizing metrics.**Bring your own (BYO) Prometheus and Grafana**: You deploy and configure your own instances of Prometheus and Grafana, and you manage the underlying infrastructure.


## Metrics captured

### Node-level metrics

Understanding the health of your container network at the node-level is crucial for maintaining optimal application performance. These metrics provide insights into traffic volume, dropped packets, number of connections, and other data by node. The metrics are stored in Prometheus format, so, you can view them in Grafana.

The following metrics are aggregated per node. All metrics include one of these labels:

`cluster`

`instance`

(node name)

For Cilium data plane scenarios, Container Network Observability provides metrics only for Linux. Windows is currently not supported. Cilium exposes several metrics including the following used by Container Network Observability.

| Metric name | Description | Extra labels | Linux | Windows |
|---|---|---|---|---|
cilium_forward_count_total |
Total forwarded packet count | `direction` |
✅ | ❌ |
cilium_forward_bytes_total |
Total forwarded byte count | `direction` |
✅ | ❌ |
cilium_drop_count_total |
Total dropped packet count | `direction` , `reason` |
✅ | ❌ |
cilium_drop_bytes_total |
Total dropped byte count | `direction` , `reason` |
✅ | ❌ |

### Pod-level metrics (Hubble metrics)

These Prometheus metrics include source and destination pod information so that you can pinpoint network-related issues at a granular level. Metrics cover information like traffic volume, dropped packets, TCP resets, and Layer 4/Layer 7 packet flows. DNS metrics like DNS errors and DNS requests missing responses are collected by default for non-Cilium data planes. For Cilium data planes, a Cilium FQDN network policy is required to collect DNS metrics, or customers can also troubleshoot DNS using Hubble CLI and observing real-time logs.

The following table describes the metrics that are aggregated per pod (node information is preserved).

All metrics include labels:

`cluster`

`instance`

(node name)`source`

or`destination`

For

*outgoing traffic*, a`source`

label that indicates the source pod namespace and name is applied.For

*incoming traffic*, a`destination`

label that indicates the destination pod namespace and name is applied.


| Metric name | Description | Extra Labels | Linux | Windows |
|---|---|---|---|---|
hubble_dns_queries_total |
Total DNS requests by query | `source` or `destination` , `query` , `qtypes` (query type) |
✅ | ❌ |
hubble_dns_responses_total |
Total DNS responses by query/response | `source` or `destination` , `query` , `qtypes` (query type), `rcode` (return code), `ips_returned` (number of IPs) |
✅ | ❌ |
hubble_drop_total |
Total dropped packet count | `source` or `destination` , `protocol` , `reason` |
✅ | ❌ |
hubble_tcp_flags_total |
Total TCP packets count by flag | `source` or `destination` , `flag` |
✅ | ❌ |
hubble_flows_processed_total |
Total network flows processed (Layer 4/Layer 7 traffic) | `source` or `destination` , `protocol` , `verdict` , `type` , `subtype` |
✅ | ❌ |

## Container network metrics filtering (Preview)

Now that you have the ability to collect comprehensive metrics at both node and pod levels, you might find yourself dealing with a significant volume of data. To help reduce noise and optimize storage costs, Container Network Observability introduces **container network metrics filtering**. This feature enables you to filter metrics at the source before they are collected and stored, giving you control over which metrics are most relevant to your specific monitoring and troubleshooting needs. This feature is only available for Cilium clusters.

Container network metrics filtering is particularly valuable in large-scale production environments where the sheer volume of metrics can impact storage costs and query performance. By filtering out unnecessary metrics early in the collection process, you can focus on the data that matters most to your operations while maintaining the visibility you need for effective network monitoring.

The filtering capability supports multiple dimensions including namespace-based filtering to focus on specific applications, pod and label-based filtering for targeted monitoring, and metric-specific filtering to collect only the types of metrics that are essential for your use case. This flexibility allows you to strike the right balance between comprehensive observability and cost-effective operations.

To learn more on how to enable container network metrics filtering, see [How to Configure Container Network Metrics Filtering ](how-to-configure-container-network-metrics-filtering).

### Limitations

- Pod-level metrics are available only on Linux.
- Cilium data plane is supported starting with Kubernetes version 1.29.
- Metric labels have subtle differences between Cilium and non-Cilium clusters.
- For Cilium based clusters, DNS metrics are only available for pods that have Cilium Network policies (CNP) configured on their clusters, or customers can also troubleshoot DNS using Hubble CLI and observing real-time logs.
- Flow logs are not currently available in the air gapped cloud.
- Hubble relay may crash if one of the Hubble node agents goes down and may cause interruptions to Hubble CLI.
- When using Advanced Container Networking Services (ACNS) on non-Cilium data planes, FIPS support isn't available on Ubuntu 20.04 nodes due to kernel restrictions. To enable FIPS in this scenario, you must use an Azure Linux node pool. This limitation is expected to be resolved with the release of Ubuntu 22 FIPS. For updates, see the
[AKS issue tracker](https://github.com/Azure/AKS/issues/4857). - Container network metrics filtering is only available for Cilium Clusters.

Refer to the FIPS support matrix below:

| Operating System | FIPS Support |
|---|---|
| Azure Linux 3.0 | Yes |
| Azure Linux 2.0 | Yes |
| Ubuntu 20.04 | No |

This limitation does not apply when ACNS is running on Cilium data planes.

### Scale

The managed service for Prometheus in Azure Monitor and Azure Managed Grafana impose service-specific scale limitations. For more information, see [Scrape Prometheus metrics at scale in Azure Monitor](/en-us/azure/azure-monitor/essentials/prometheus-metrics-scrape-scale).

## Pricing

Important

Advanced Container Networking Services is a paid offering.

For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Related content

- To create an AKS cluster by using Container Network Observability to capture metrics, see
[Set up Container Network Observability for AKS](container-network-observability-how-to). - Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services. - Explore the
[Container Network Security feature](advanced-container-networking-services-overview#container-network-security)in Advanced Container Networking Services.
