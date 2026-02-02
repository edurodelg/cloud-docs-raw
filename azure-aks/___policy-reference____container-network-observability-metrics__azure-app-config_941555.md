---
merged_at: 2026-02-02T15:56:31.827103
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-metrics -->

# What is container network metrics?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Advanced Container Networking Services in Azure Kubernetes Service (AKS) facilitates the collection of comprehensive container network metrics to give you valuable insights into the performance of your containerized environment. The capability continuously captures essential metrics at the node level and pod level, including traffic volume, dropped packets, connection states, and Domain Name System (DNS) resolution times for effective monitoring and optimizing network performance.

Capturing these metrics is essential for understanding how containers communicate, how traffic flows between services, and where bottlenecks or disruptions might occur. Advanced Container Networking Services integrates seamlessly with monitoring tools like Prometheus and Grafana to give you a complete view of networking metrics. Use the metrics for in-depth troubleshooting, network optimization, and performance tuning.

In a cloud-native world, maintaining a healthy and efficient network in a dynamic containerized environment is vital to ensuring that applications perform as expected. Without proper visibility into network traffic and its patterns, identifying potential issues or inefficiencies becomes challenging.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-app-configuration-quickstart -->

# Quickstart: Generate ConfigMap from Azure App Configuration

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can externalize the configurations of your Azure Kubernetes Service (AKS) workloads and manage them in [Azure App Configuration](/en-us/azure/azure-app-configuration/overview). The [Azure App Configuration Kubernetes provider](https://mcr.microsoft.com/artifact/mar/azure-app-configuration/kubernetes-provider/about) runs as a container in your cluster. Key benefits include:

**Seamless integration**: Pulls data from Azure App Configuration and Key Vault, making them accessible as ConfigMap and Secret without code changes in your workloads.**Dynamic update**: Built-in caching and refreshing capabilities for dynamic configuration, feature flagging, and automatic secret rotation.

The Azure App Configuration Kubernetes provider is available as an AKS extension. By following this document, you can easily install the extension and connect your AKS cluster with an App Configuration store using the Service Connector in the Azure portal. For information on setting up the provider using Helm, see the [Quickstart for Azure App Configuration Kubernetes provider](/en-us/azure/azure-app-configuration/quickstart-azure-kubernetes-service).

## Prerequisites

- An Azure Kubernetes Service (AKS) cluster.
[Create an AKS cluster](/en-us/azure/aks/tutorial-kubernetes-deploy-cluster#create-a-kubernetes-cluster). - A running workload in Azure Kubernetes Service (AKS) cluster. If you don't have one, you can
[create a demo application running in AKS](/en-us/azure/azure-app-configuration/quickstart-azure-kubernetes-service#create-an-application-running-in-aks).

## Create a service connection to App Configuration

Create a service connection between your AKS cluster and your App Configuration store using Microsoft Entra Workload Identity.

In the

[Azure portal](https://portal.azure.com), navigate to your AKS cluster resource.Select

**Settings**>**Service Connector**>**Create**.On the

**Basics**tab, configure the following settings:**Kubernetes namespace**: Specify the namespace you'd like to create ConfigMap or Secret to.**Service type**: Select**App Configuration**.**Use App Configuration Extension on Kubernetes**: Check the box to use the[Azure App Configuration AKS extension](azure-app-configuration)for this connection. Azure App Configuration AKS extension will be installed to current cluster if it's not yet.**Connection name**: Enter a connection name or use the default name.**Subscription**: Select the subscription of your App Configuration store.**App Configuration**: Select your App Configuration store. If you don't have one, click**Create new**to set one up.

Select

**Next: Authentication**. On the**Authentication**tab, keep the default selection of**Workload Identity**, select a**User assigned managed identity**you want to use. If you don't have one, click**Create new**to set one up.Select

**Next: Networking**and use the default settings.Select

**Next: Review + create**and wait for the validation to pass.Select

**Create**to create the service connection.

Note

The Service Connector simplifies the installation of the Azure App Configuration AKS extension from the Azure portal. You can also install it without Service Connector using Azure CLI, Bicep, or an ARM template. For more information, see [Install Azure App Configuration AKS extension](azure-app-configuration).

## Generate ConfigMap from App Configuration

Update the service connection to create and deploy an `AzureAppConfigurationProvider`

YAML resource in your AKS cluster. This resource generates a ConfigMap with data from your App Configuration store.

In the

[Azure portal](https://portal.azure.com), navigate to your AKS cluster resource and select**Settings**>**Service Connector**.Select the newly created connection, select

**Yaml snippet**in the top menu.On the

**AzureAppConfigurationProvider**tab, configure the following settings:**Using configuration as**: Choose to consume the configuration as a**mounted file**or**environment variables**.**Mounted file**: If selected, specify the**file type**and**file name**.**Selector**: Set the**Key filter**and**Label filter**to load data from your App Configuration store.

A YAML is generated based on your input. Click

**Apply**to add it to your AKS cluster. It will create a ConfigMap in your AKS cluster with data from your App Configuration store.Click

**Next**. On the**Workload**tab, configure the following settings:**File mount path**: Specify the file mount path if the mounted file option was selected.**Kubernetes Workload**: Select the workload where the generated ConfigMap will be injected.- Click
**Apply**to update the workload.


## Next Steps

To learn more about installing and customizing the Azure App Configuration AKS extension, refer to the following documents:

For a complete feature rundown of the Azure App Configuration Kubernetes Provider, see

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-autoprovision -->

# Overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS), including how it works, upgrade behavior, prerequisites, limitations, and resources to get started.

## What is node auto-provisioning in AKS?

When you deploy workloads onto AKS, you need to select the appropriate virtual machine (VM) size as part of your node pool configuration. As your workloads become more complex, you might have different workloads with varying resource requirements, which makes it more difficult to design your VM configuration for numerous resource requests.

Node auto-provisioning (NAP) simplifies this process by automatically provisioning and managing the optimal VM configuration for your workloads. NAP uses pending pod resource requirements to decide the optimal VM configuration to run your workloads in the most efficient and cost-effective manner.

NAP automatically deploys, configures, and manages Karpenter on your AKS clusters and is based on the open-source [Karpenter](https://karpenter.sh) and [AKS Karpenter provider](https://github.com/Azure/karpenter-provider-azure) projects.

## How does node auto-provisioning work?

Node auto-provisioning provisions, scales, and manages VMs (nodes) in a cluster in response to pending pod pressure.

### Key components of node auto-provisioning

NAP uses the following key components to help manage your cluster's nodes:

| Component | Description |
|---|---|
`NodePool` and `AKSNodeClass` |
Custom Resource Definitions (CRDs) that you create and manage to define node provisioning policies, VM specifications, and constraints for your workloads. |
`NodeClaims` |
Managed by NAP to represent the current state of provisioned nodes that you can monitor. |
| Workload resource requirements | CPU, memory, and other specifications from your Pods, Deployments, Jobs, and other Kubernetes resources that drive provisioning decisions. |

## Kubernetes upgrade behavior for node auto-provisioning nodes

Kubernetes upgrades for node auto-provisioning nodes follow the control plane Kubernetes version. If you perform a cluster upgrade, your nodes are automatically updated to follow the same versioning as your control plane.

We recommend setting a Kubernetes [auto-upgrade](/en-us/azure/aks/auto-upgrade-cluster#cluster-auto-upgrade-channels) channel, which automatically handles Kubernetes upgrades for your cluster. We also recommend setting a [planned maintenance window](planned-maintenance#create-a-maintenance-window) for your cluster. The `aksManagedAutoUpgradeSchedule`

maintenance window allows you to control when to perform cluster upgrades scheduled by your designated auto-upgrade channel. For more information, see [Use planned maintenance to schedule and control upgrades for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Prerequisites

To use node auto-provisioning in AKS, you need the following prerequisites:

- An Azure subscription. If you don't have one, you can create a
[free account](https://azure.microsoft.com/free). - Azure CLI version
`2.76.0`

or later. To find the version, run`az --version`

. For more information about installing or upgrading the Azure CLI, see[Install Azure CLI](/en-us/cli/azure/get-started-with-azure-cli).

## Limitations and unsupported features

The following limitations and unsupported features apply to node auto-provisioning in AKS:

- You can't enable NAP on clusters enabled with the
[cluster autoscaler](cluster-autoscaler). - Windows node pools aren't supported.
- IPv6 clusters aren't supported.
[Service principals](kubernetes-service-principal)aren't supported. You can use either a system-assigned or user-assigned managed identity.[Custom certificate authority (CA) certificates](custom-certificate-authority)aren't supported.- You can't
[stop a cluster](start-stop-cluster)enabled with NAP. [HTTP proxy](http-proxy)isn't supported.- You can't change the
[cluster egress outbound type](egress-outboundtype)after you create a cluster enabled with NAP. - When creating a NAP cluster in a custom virtual network (VNet), you must use a
[Standard Load Balancer](load-balancer-standard). The Basic Load Balancer isn't supported.

## Get started with node auto-provisioning on AKS

The following resources help you get started with node auto-provisioning on AKS:

[Enable or disable node auto-provisioning on an AKS cluster](use-node-auto-provisioning)[Use node auto-provisioning in a custom virtual network](node-auto-provisioning-custom-vnet)[Configure networking for node auto-provisioning on AKS](node-auto-provisioning-networking)[Configure node pools for node auto-provisioning on AKS](node-auto-provisioning-node-pools)[Configure disruption policies for node auto-provisioning on AKS](node-auto-provisioning-disruption)[Upgrade node images for node auto-provisioning on AKS](node-auto-provisioning-upgrade-image)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/validate-postgresql-ha -->

# Validate and test a PostgreSQL database deployment on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you perform various testing and validation steps on a PostgreSQL database deployed on AKS. This includes verifying the deployment, connecting to the database, and testing failover scenarios.

- If you haven't already deployed PostgreSQL, follow the steps in
[Deploy a highly available PostgreSQL database on AKS with Azure CLI](deploy-postgresql-ha)to get set up, and then you can return to this article.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Inspect the deployed PostgreSQL cluster

Validate that PostgreSQL is spread across multiple availability zones by retrieving the AKS node details using the [ kubectl get](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_get/) command.

```
kubectl get nodes \
--context $AKS_PRIMARY_CLUSTER_NAME \
--namespace $PG_NAMESPACE \
--output json | jq '.items[] | {node: .metadata.name, zone: .metadata.labels."failure-domain.beta.kubernetes.io/zone"}'
```


Your output should resemble the following example output with the availability zone shown for each node:

```
{
"node": "aks-postgres-15810965-vmss000000",
"zone": "westus3-1"
}
{
"node": "aks-postgres-15810965-vmss000001",
"zone": "westus3-2"
}
{
"node": "aks-postgres-15810965-vmss000002",
"zone": "westus3-3"
}
{
"node": "aks-systempool-26112968-vmss000000",
"zone": "westus3-1"
}
{
"node": "aks-systempool-26112968-vmss000001",
"zone": "westus3-2"
}
```


## Connect to PostgreSQL and create a sample dataset

In this section, you create a table and insert some data into the app database that was created in the CNPG Cluster CRD you deployed earlier. You use this data to validate the backup and restore operations for the PostgreSQL cluster.

Create a table and insert data into the app database using the following commands:

`kubectl cnpg psql $PG_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE`

`-- Create a small dataset CREATE TABLE datasample (id INTEGER, name VARCHAR(255)); INSERT INTO datasample (id, name) VALUES (1, 'John'); INSERT INTO datasample (id, name) VALUES (2, 'Jane'); INSERT INTO datasample (id, name) VALUES (3, 'Alice'); SELECT COUNT(*) FROM datasample;`

Type

`\q`

to exit psql when finished.Your output should resemble the following example output:

`CREATE TABLE INSERT 0 1 INSERT 0 1 INSERT 0 1 count ------- 3 (1 row)`


## Connect to PostgreSQL read-only replicas

Connect to the PostgreSQL read-only replicas and validate the sample dataset using the following commands:

`kubectl cnpg psql --replica $PG_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE`

`SELECT pg_is_in_recovery();`

Example output

`pg_is_in_recovery ------------------- t (1 row)`

`SELECT COUNT(*) FROM datasample;`

Example output

`count ------- 3 (1 row)`


## Set up on-demand and scheduled PostgreSQL backups using Barman

Note

CloudNativePG is expected to deprecate native Barman Cloud support in favor of the [Barman Cloud plugin](https://cloudnative-pg.io/plugin-barman-cloud/docs/intro/) in an upcoming 1.29 release. The steps in this guide continue to work today, but plan to migrate to the plugin once it stabilizes.

Validate that the PostgreSQL cluster can access the Azure storage account specified in the CNPG Cluster CRD and that

`Working WAL archiving`

reports as`OK`

using the following command:`kubectl cnpg status $PG_PRIMARY_CLUSTER_NAME 1 \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE`

Example output

`Continuous Backup status First Point of Recoverability: Not Available Working WAL archiving: OK WALs waiting to be archived: 0 Last Archived WAL: 00000001000000000000000A @ 2024-07-09T17:18:13.982859Z Last Failed WAL: -`

Deploy an on-demand backup to Azure Storage, which uses the AKS workload identity integration, using the YAML file with the

command.`kubectl apply`

`export BACKUP_ONDEMAND_NAME="on-demand-backup-1" cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -v 9 -f - apiVersion: postgresql.cnpg.io/v1 kind: Backup metadata: name: $BACKUP_ONDEMAND_NAME spec: method: barmanObjectStore cluster: name: $PG_PRIMARY_CLUSTER_NAME EOF`

Validate the status of the on-demand backup using the

command.`kubectl describe`

`kubectl describe backup $BACKUP_ONDEMAND_NAME \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE`

Example output

`Type Reason Age From Message ---- ------ ---- ---- ------- Normal Starting 6s cloudnative-pg-backup Starting backup for cluster pg-primary-cnpg-r8c7unrw Normal Starting 5s instance-manager Backup started Normal Completed 1s instance-manager Backup completed`

Validate that the cluster has a first point of recoverability using the following command:

`kubectl cnpg status $PG_PRIMARY_CLUSTER_NAME 1 \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE`

Example output

`Continuous Backup status First Point of Recoverability: 2024-06-05T13:47:18Z Working WAL archiving: OK`

Configure a scheduled backup for

*every hour at 15 minutes past the hour*using the YAML file with thecommand.`kubectl apply`

`export BACKUP_SCHEDULED_NAME="scheduled-backup-1" cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -v 9 -f - apiVersion: postgresql.cnpg.io/v1 kind: ScheduledBackup metadata: name: $BACKUP_SCHEDULED_NAME spec: # Backup once per hour schedule: "0 15 * ? * *" backupOwnerReference: self cluster: name: $PG_PRIMARY_CLUSTER_NAME EOF`

Validate the status of the scheduled backup using the

command.`kubectl describe`

`kubectl describe scheduledbackup $BACKUP_SCHEDULED_NAME \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE`

View the backup files stored on Azure blob storage for the primary cluster using the

command.`az storage blob list`

`az storage blob list \ --account-name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --container-name backups \ --query "[*].name" \ --only-show-errors`

Your output should resemble the following example output, validating the backup was successful:

`[ "pg-primary-cnpg-r8c7unrw/base/20240605T134715/backup.info", "pg-primary-cnpg-r8c7unrw/base/20240605T134715/data.tar", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000001", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000002", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000003", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000003.00000028.backup", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000004", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000005", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000005.00000028.backup", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000006", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000007", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000008", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000009" ]`


## Restore the on-demand backup to a new PostgreSQL cluster

In this section, you restore the on-demand backup you created earlier using the CNPG operator into a new instance using the bootstrap Cluster CRD. A single instance cluster is used for simplicity. Remember that the AKS workload identity (via CNPG inheritFromAzureAD) accesses the backup files, and that the recovery cluster name is used to generate a new Kubernetes service account specific to the recovery cluster.

You also create a second federated credential to map the new recovery cluster service account to the existing UAMI that has "Storage Blob Data Contributor" access to the backup files on blob storage.

Create a second federated identity credential using the

command.`az identity federated-credential create`

`export PG_PRIMARY_CLUSTER_NAME_RECOVERED="$PG_PRIMARY_CLUSTER_NAME-recovered-db" az identity federated-credential create \ --name $PG_PRIMARY_CLUSTER_NAME_RECOVERED \ --identity-name $AKS_UAMI_CLUSTER_IDENTITY_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --issuer "${AKS_PRIMARY_CLUSTER_OIDC_ISSUER}" \ --subject system:serviceaccount:"${PG_NAMESPACE}":"${PG_PRIMARY_CLUSTER_NAME_RECOVERED}" \ --audience api://AzureADTokenExchange`

Restore the on-demand backup using the Cluster CRD with the

command.`kubectl apply`

`cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -v 9 -f - apiVersion: postgresql.cnpg.io/v1 kind: Cluster metadata: name: $PG_PRIMARY_CLUSTER_NAME_RECOVERED spec: inheritedMetadata: annotations: service.beta.kubernetes.io/azure-dns-label-name: $AKS_PRIMARY_CLUSTER_PG_DNSPREFIX labels: azure.workload.identity/use: "true" instances: 1 affinity: nodeSelector: workload: postgres # Point to cluster backup created earlier and stored on Azure Blob Storage bootstrap: recovery: source: clusterBackup storage: size: 2Gi pvcTemplate: accessModes: - ReadWriteOnce resources: requests: storage: 2Gi storageClassName: managed-csi-premium volumeMode: Filesystem walStorage: size: 2Gi pvcTemplate: accessModes: - ReadWriteOnce resources: requests: storage: 2Gi storageClassName: managed-csi-premium volumeMode: Filesystem serviceAccountTemplate: metadata: annotations: azure.workload.identity/client-id: "$AKS_UAMI_WORKLOAD_CLIENTID" labels: azure.workload.identity/use: "true" externalClusters: - name: clusterBackup barmanObjectStore: destinationPath: https://${PG_PRIMARY_STORAGE_ACCOUNT_NAME}.blob.core.windows.net/backups serverName: $PG_PRIMARY_CLUSTER_NAME azureCredentials: inheritFromAzureAD: true wal: maxParallel: 8 EOF`

Connect to the recovered instance, then validate that the dataset created on the original cluster where the full backup was taken is present using the following command:

`kubectl cnpg psql $PG_PRIMARY_CLUSTER_NAME_RECOVERED --namespace $PG_NAMESPACE`

`SELECT COUNT(*) FROM datasample;`

Example output

`count ------- 3 (1 row) Type \q to exit psql`

Delete the recovered cluster using the following command:

`kubectl cnpg destroy $PG_PRIMARY_CLUSTER_NAME_RECOVERED 1 \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE`

Delete the federated identity credential using the

command.`az identity federated-credential delete`

`az identity federated-credential delete \ --name $PG_PRIMARY_CLUSTER_NAME_RECOVERED \ --identity-name $AKS_UAMI_CLUSTER_IDENTITY_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --yes`


## Expose the PostgreSQL cluster using a public load balancer

In this section, you configure the necessary infrastructure to publicly expose the PostgreSQL read-write and read-only endpoints with IP source restrictions to the public IP address of your client workstation.

You also retrieve the following endpoints from the Cluster IP service:

*One*primary read-write endpoint that ends with`*-rw`

.*Zero to N*(depending on the number of replicas) read-only endpoints that end with`*-ro`

.*One*replication endpoint that ends with`*-r`

.

Get the Cluster IP service details using the

command.`kubectl get`

`kubectl get services \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE \ -l cnpg.io/cluster=$PG_PRIMARY_CLUSTER_NAME`

Example output

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE pg-primary-cnpg-sryti1qf-r ClusterIP 10.0.193.27 <none> 5432/TCP 3h57m pg-primary-cnpg-sryti1qf-ro ClusterIP 10.0.237.19 <none> 5432/TCP 3h57m pg-primary-cnpg-sryti1qf-rw ClusterIP 10.0.244.125 <none> 5432/TCP 3h57m`

Note

There are three services:

`namespace/cluster-name-ro`

mapped to port 5433,`namespace/cluster-name-rw`

, and`namespace/cluster-name-r`

mapped to port 5433. It’s important to avoid using the same port as the read/write node of the PostgreSQL database cluster. If you want applications to access only the read-only replica of the PostgreSQL database cluster, direct them to port 5433. The final service is typically used for data backups but can also function as a read-only node.Get the service details using the

command.`kubectl get`

`export PG_PRIMARY_CLUSTER_RW_SERVICE=$(kubectl get services \ --namespace $PG_NAMESPACE \ --context $AKS_PRIMARY_CLUSTER_NAME \ -l "cnpg.io/cluster" \ --output json | jq -r '.items[] | select(.metadata.name | endswith("-rw")) | .metadata.name') echo $PG_PRIMARY_CLUSTER_RW_SERVICE export PG_PRIMARY_CLUSTER_RO_SERVICE=$(kubectl get services \ --namespace $PG_NAMESPACE \ --context $AKS_PRIMARY_CLUSTER_NAME \ -l "cnpg.io/cluster" \ --output json | jq -r '.items[] | select(.metadata.name | endswith("-ro")) | .metadata.name') echo $PG_PRIMARY_CLUSTER_RO_SERVICE`

Configure the load balancer service with the following YAML files using the

command.`kubectl apply`

`cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME -f - apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-load-balancer-resource-group: $AKS_PRIMARY_CLUSTER_NODERG_NAME service.beta.kubernetes.io/azure-pip-name: $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME service.beta.kubernetes.io/azure-dns-label-name: $AKS_PRIMARY_CLUSTER_PG_DNSPREFIX name: cnpg-cluster-load-balancer-rw namespace: "${PG_NAMESPACE}" spec: type: LoadBalancer ports: - protocol: TCP port: 5432 targetPort: 5432 selector: cnpg.io/instanceRole: primary cnpg.io/podRole: instance loadBalancerSourceRanges: - "$MY_PUBLIC_CLIENT_IP/32" EOF cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME -f - apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-load-balancer-resource-group: $AKS_PRIMARY_CLUSTER_NODERG_NAME service.beta.kubernetes.io/azure-pip-name: $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME service.beta.kubernetes.io/azure-dns-label-name: $AKS_PRIMARY_CLUSTER_PG_DNSPREFIX name: cnpg-cluster-load-balancer-ro namespace: "${PG_NAMESPACE}" spec: type: LoadBalancer ports: - protocol: TCP port: 5433 targetPort: 5432 selector: cnpg.io/instanceRole: replica cnpg.io/podRole: instance loadBalancerSourceRanges: - "$MY_PUBLIC_CLIENT_IP/32" EOF`

Get the service details using the

command.`kubectl describe`

`kubectl describe service cnpg-cluster-load-balancer-rw \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE kubectl describe service cnpg-cluster-load-balancer-ro \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE export AKS_PRIMARY_CLUSTER_ALB_DNSNAME="$(az network public-ip show \ --resource-group $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --name $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME \ --query "dnsSettings.fqdn" --output tsv)" echo $AKS_PRIMARY_CLUSTER_ALB_DNSNAME`


### Validate public PostgreSQL endpoints

In this section, you validate that the Azure Load Balancer is properly set up using the static IP that you created earlier and routing connections to the primary read-write and read-only replicas and use the psql CLI to connect to both.

Remember that the primary read-write endpoint maps to TCP port 5432 and the read-only replica endpoints map to port 5433 to allow the same PostgreSQL DNS name to be used for readers and writers.

Note

You need the value of the app user password for PostgreSQL basic auth that was generated earlier and stored in the `$PG_DATABASE_APPUSER_SECRET`

environment variable.

Validate the public PostgreSQL endpoints using the following

`psql`

commands:`echo "Public endpoint for PostgreSQL cluster: $AKS_PRIMARY_CLUSTER_ALB_DNSNAME" # Query the primary, pg_is_in_recovery = false psql -h $AKS_PRIMARY_CLUSTER_ALB_DNSNAME \ -p 5432 -U app -d appdb -W -c "SELECT pg_is_in_recovery();"`

Example output

`pg_is_in_recovery ------------------- f (1 row)`

`echo "Query a replica, pg_is_in_recovery = true" psql -h $AKS_PRIMARY_CLUSTER_ALB_DNSNAME \ -p 5433 -U app -d appdb -W -c "SELECT pg_is_in_recovery();"`

Example output

`# Example output pg_is_in_recovery ------------------- t (1 row)`

When successfully connected to the primary read-write endpoint, the PostgreSQL function returns

`f`

for*false*, indicating that the current connection is writable.When connected to a replica, the function returns

`t`

for*true*, indicating the database is in recovery and read-only.

## Simulate an unplanned failover

In this section, you trigger a sudden failure by deleting the pod running the primary, which simulates a sudden crash or loss of network connectivity to the node hosting the PostgreSQL primary.

Check the status of the running pod instances using the following command:

`kubectl cnpg status $PG_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE`

Example output

`Name Current LSN Rep role Status Node --------------------------- ----------- -------- ------- ----------- pg-primary-cnpg-sryti1qf-1 0/9000060 Primary OK aks-postgres-32388626-vmss000000 pg-primary-cnpg-sryti1qf-2 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000001 pg-primary-cnpg-sryti1qf-3 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000002`

Delete the primary pod using the

command.`kubectl delete`

`PRIMARY_POD=$(kubectl get pod \ --namespace $PG_NAMESPACE \ --no-headers \ -o custom-columns=":metadata.name" \ -l role=primary) kubectl delete pod $PRIMARY_POD --grace-period=1 --namespace $PG_NAMESPACE`

Validate that the

`pg-primary-cnpg-sryti1qf-2`

pod instance is now the primary using the following command:`kubectl cnpg status $PG_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE`

Example output

`pg-primary-cnpg-sryti1qf-2 0/9000060 Primary OK aks-postgres-32388626-vmss000001 pg-primary-cnpg-sryti1qf-1 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000000 pg-primary-cnpg-sryti1qf-3 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000002`

Reset the

`pg-primary-cnpg-sryti1qf-1`

pod instance as the primary using the following command:`kubectl cnpg promote $PG_PRIMARY_CLUSTER_NAME 1 --namespace $PG_NAMESPACE`

Validate that the pod instances have returned to their original state before the unplanned failover test using the following command:

`kubectl cnpg status $PG_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE`

Example output

`Name Current LSN Rep role Status Node --------------------------- ----------- -------- ------- ----------- pg-primary-cnpg-sryti1qf-1 0/9000060 Primary OK aks-postgres-32388626-vmss000000 pg-primary-cnpg-sryti1qf-2 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000001 pg-primary-cnpg-sryti1qf-3 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000002`


## Clean up resources

Once you're finished reviewing your deployment, delete all the resources you created in this guide using the

command.`az group delete`

`az group delete --resource-group $RESOURCE_GROUP_NAME --no-wait --yes`


## Next steps

In this how-to guide, you learned how to:

- Use Azure CLI to create a multi-zone AKS cluster.
- Deploy a highly available PostgreSQL cluster and database using the CNPG operator.
- Set up monitoring for PostgreSQL using Prometheus and Grafana.
- Deploy a sample dataset to the PostgreSQL database.
- Simulate a cluster interruption and PostgreSQL replica failover.
- Perform a backup and restore of the PostgreSQL database.

To learn more about how you can use AKS for your workloads, see [What is Azure Kubernetes Service (AKS)?](what-is-aks) To learn more about Azure Database for PostgreSQL, see [What is Azure Database for PostgreSQL?](/en-us/azure/postgresql/flexible-server/overview)

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Ken Kilty | Principal TPM
- Russell de Pina | Principal TPM
- Adrian Joian | Senior Customer Engineer
- Jenny Hayes | Senior Content Developer
- Carol Smith | Senior Content Developer
- Erin Schaffer | Content Developer 2
- Adam Sharif | Customer Engineer 2

## Acknowledgment

This documentation was jointly developed with EnterpriseDB, the maintainers of the CloudNativePG operator. We thank [Gabriele Bartolini](https://cloudnative-pg.io/authors/gbartolini/) for reviewing earlier drafts of this document and offering technical improvements.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/app-routing-nginx-configuration -->

# Advanced NGINX ingress controller and ingress configurations with the application routing add-on for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article walks you through two ways to configure ingress controllers and ingress objects with the application routing add-on for Azure Kubernetes Service (AKS):

[Configuration of the NGINX ingress controller](#control-the-default-nginx-ingress-controller-configuration)such as creating multiple controllers, configuring private load balancers, and setting static IP addresses.[Configuration per ingress resource](#configuration-per-ingress-resource-through-annotations)through annotations.

## Prerequisites

- An AKS cluster with the
[application routing add-on](app-routing)enabled. `kubectl`

configured to connect to your AKS cluster. For more information, see[Connect to your AKS cluster](#connect-to-your-aks-cluster).

### Connect to your AKS cluster

To connect to the Kubernetes cluster from your local computer, you use `kubectl`

, the Kubernetes command-line client. You can install it locally using the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. If you use the Azure Cloud Shell,

`kubectl`

is already installed.Configure kubectl to connect to your Kubernetes cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Configuration properties for NGINX ingress controllers

The application routing add-on uses a Kubernetes [custom resource definition (CRD)](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) called [ NginxIngressController](https://github.com/Azure/aks-app-routing-operator/blob/main/config/crd/bases/approuting.kubernetes.azure.com_nginxingresscontrollers.yaml) to configure NGINX ingress controllers. You can create more ingress controllers or modify existing configurations.

The following table lists properties you can set to configure an `NginxIngressController`

:

| Field | Type | Description | Required | Default |
|---|---|---|---|---|
`controllerNamePrefix` |
string | Name for the managed NGINX Ingress Controller resources. | Yes | `nginx` |
`customHTTPErrors` |
array | Array of error codes to be sent to the default backend if there's an error. | No | |
`defaultBackendService` |
object | Service to route unmatched HTTP traffic. Contains nested properties: | No | |
`name` |
string | Service name. | Yes | |
`namespace` |
string | Service namespace. | Yes | |
`defaultSSLCertificate` |
object | Contains the default certificate for accessing the default backend service. Contains nested properties: | No | |
`forceSSLRedirect` |
boolean | Forces HTTPS redirection when a certificate is set. | No | `false` |
`keyVaultURI` |
string | URI for a Key Vault secret storing the certificate. | No | |
`secret` |
object | Holds secret information for the default SSL certificate. Contains nested properties: | No | |
`name` |
string | Secret name. | Yes | |
`namespace` |
string | Secret namespace. | Yes | |
`httpDisabled` |
boolean | Flag to disable HTTP traffic to the controller. | No | |
`ingressClassName` |
string | IngressClass name used by the controller. | Yes | `nginx.approuting.kubernetes.azure.com` |
`loadBalancerAnnotations` |
object | A map of annotations to control the behavior of the NGINX ingress controller's service by setting
|

`scaling`

`maxReplicas`

`100`

`minReplicas`

`2`

`threshold`

**scales quickly for sudden spikes,**`rapid`

**favors cost-effectiveness, and**`steady`

**is a mix.**`balanced`

`balanced`

## Control the default NGINX ingress controller configuration

When you enable the application routing add-on with NGINX, it creates an ingress controller called `default`

in the `app-routing-namespace`

configured with a public facing Azure load balancer. That ingress controller uses an ingress class name of `webapprouting.kubernetes.azure.com`

.

You can also control if the default gets a public or an internal IP, or if it gets created at all when enabling the add-on.

Possible configuration options include:

: The default NGINX ingress controller isn't created and isn't deleted if it already exists. You should manually delete the default`None`

`NginxIngressController`

custom resource if desired.: The default NGINX ingress controller is created with an internal load balancer. Any annotation changes on the`Internal`

`NginxIngressController`

custom resource to make it external are overwritten.: The default NGINX ingress controller created with an external load balancer. Any annotation changes on the`External`

`NginxIngressController`

custom resource to make it internal are overwritten.(default): The default NGINX ingress controller is created with an external load balancer. You can edit the default`AnnotationControlled`

`NginxIngressController`

custom resource to configure load balancer annotations.)

### Control the default ingress controller configuration on a new cluster

Enable application routing on a new cluster using the

command with the`az aks create`

`--enable-app-routing`

and`--app-routing-default-nginx-controller`

flags. You need to set the`<DefaultIngressControllerType>`

to one of the configuration options described in[Control the default NGINX ingress controller configuration](#control-the-default-nginx-ingress-controller-configuration).`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --location $LOCATION \ --enable-app-routing \ --app-routing-default-nginx-controller <DefaultIngressControllerType>`


### Update the default ingress controller configuration on an existing cluster

Update the application routing default ingress controller configuration on an existing cluster using the

command with the`az aks approuting update`

`--nginx`

flag. You need to set the`<DefaultIngressControllerType>`

to one of the configuration options described in[Control the default NGINX ingress controller configuration](#control-the-default-nginx-ingress-controller-configuration).`az aks approuting update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --nginx <DefaultIngressControllerType>`


## Create another public facing NGINX ingress controller

Copy the following YAML manifest into a new file named

`nginx-public-controller.yaml`

and save the file to your local computer.`apiVersion: approuting.kubernetes.azure.com/v1alpha1 kind: NginxIngressController metadata: name: nginx-public spec: ingressClassName: nginx-public controllerNamePrefix: nginx-public`

Create the NGINX ingress controller resources using the

command.`kubectl apply`

`kubectl apply -f nginx-public-controller.yaml`

The following example output shows the created resource:

`nginxingresscontroller.approuting.kubernetes.azure.com/nginx-public created`


## Create an internal NGINX ingress controller with a private IP address

Copy the following YAML manifest into a new file named

`nginx-internal-controller.yaml`

and save the file to your local computer.`apiVersion: approuting.kubernetes.azure.com/v1alpha1 kind: NginxIngressController metadata: name: nginx-internal spec: ingressClassName: nginx-internal controllerNamePrefix: nginx-internal loadBalancerAnnotations: service.beta.kubernetes.io/azure-load-balancer-internal: "true"`

Create the NGINX ingress controller resources using the

command.`kubectl apply`

`kubectl apply -f nginx-internal-controller.yaml`

The following example output shows the created resource:

`nginxingresscontroller.approuting.kubernetes.azure.com/nginx-internal created`


## Create an NGINX ingress controller with a static IP address

Create an Azure resource group using the

command.`az group create`

`az group create --name $NETWORK_RESOURCE_GROUP --location $LOCATION`

Create a static public IP address using the

command.`az network public ip create`

`az network public-ip create \ --resource-group $NETWORK_RESOURCE_GROUP \ --name $PUBLIC_IP_NAME \ --sku Standard \ --allocation-method static`

Note

If you're using a

*Basic*SKU load balancer in your AKS cluster, use`Basic`

for the`--sku`

parameter when defining a public IP. Only`Basic`

SKU IPs work with the*Basic*SKU load balancer and only`Standard`

SKU IPs work with the*Standard*SKU load balancers.Ensure the cluster identity used by the AKS cluster has delegated permissions to the public IP's resource group using the

command.`az role assignment create`

`CLIENT_ID=$(az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query identity.principalId -o tsv) RG_SCOPE=$(az group show --name $NETWORK_RESOURCE_GROUP --query id -o tsv) az role assignment create \ --assignee ${CLIENT_ID} \ --role "Network Contributor" \ --scope ${RG_SCOPE}`

Copy the following YAML manifest into a new file named

`nginx-staticip-controller.yaml`

and save the file to your local computer.Note

You can either use

`service.beta.kubernetes.io/azure-pip-name`

for public IP name, or use`service.beta.kubernetes.io/azure-load-balancer-ipv4`

for an IPv4 address and`service.beta.kubernetes.io/azure-load-balancer-ipv6`

for an IPv6 address, as shown in the example YAML. Adding the`service.beta.kubernetes.io/azure-pip-name`

annotation ensures the most efficient Load Balancer creation and is highly recommended to avoid potential throttling.`apiVersion: approuting.kubernetes.azure.com/v1alpha1 kind: NginxIngressController metadata: name: nginx-static spec: ingressClassName: nginx-static controllerNamePrefix: nginx-static loadBalancerAnnotations: service.beta.kubernetes.io/azure-pip-name: "$PUBLIC_IP_NAME" service.beta.kubernetes.io/azure-load-balancer-resource-group: "$NETWORK_RESOURCE_GROUP"`

Create the NGINX ingress controller resources using the

command.`kubectl apply`

`kubectl apply -f nginx-staticip-controller.yaml`

The following example output shows the created resource:

`nginxingresscontroller.approuting.kubernetes.azure.com/nginx-static created`


## Verify the ingress controller was created

Verify the status of the NGINX ingress controller using the

command.`kubectl get nginxingresscontroller`

`kubectl get nginxingresscontroller --name $INGRESS_CONTROLLER_NAME`

The following example output shows the created resource. It may take a few minutes for the controller to be available:

`NAME INGRESSCLASS CONTROLLERNAMEPREFIX AVAILABLE nginx-public nginx-public nginx True`


### View the conditions of the ingress controller

View the conditions of the ingress controller to troubleshoot any issues using the

command.`kubectl get nginxingresscontroller`

`kubectl get nginxingresscontroller --name $INGRESS_CONTROLLER_NAME -o jsonpath='{range .items[*].status.conditions[*]}{.lastTransitionTime}{"\t"}{.status}{"\t"}{.type}{"\t"}{.message}{"\n"}{end}'`

The following example output shows the conditions of a healthy ingress controller:

`2023-11-29T19:59:24Z True IngressClassReady Ingress Class is up-to-date 2023-11-29T19:59:50Z True Available Controller Deployment has minimum availability and IngressClass is up-to-date 2023-11-29T19:59:50Z True ControllerAvailable Controller Deployment is available 2023-11-29T19:59:25Z True Progressing Controller Deployment has successfully progressed`


## Use the ingress controller in an ingress

Copy the following YAML manifest into a new file named

`ingress.yaml`

and save the file to your local computer.Note

Update

`<HostName>`

with your DNS host name. The`<IngressClassName>`

is the one you defined when creating the`NginxIngressController`

.`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: aks-helloworld namespace: hello-web-app-routing spec: ingressClassName: <IngressClassName> rules: - host: <HostName> http: paths: - backend: service: name: aks-helloworld port: number: 80 path: / pathType: Prefix`

Create the cluster resources using the

command.`kubectl apply`

`kubectl apply -f ingress.yaml --namespace hello-web-app-routing`

The following example output shows the created resource:

`ingress.networking.k8s.io/aks-helloworld created`


## Verify the managed ingress was created

Verify the managed ingress was created using the

command.`kubectl get ingress`

`kubectl get ingress --namespace hello-web-app-routing`

Your output should resemble the following example output:

`NAME CLASS HOSTS ADDRESS PORTS AGE aks-helloworld webapprouting.kubernetes.azure.com myapp.contoso.com 20.51.92.19 80, 443 4m`


## Remove ingress controllers

Remove the NGINX ingress controller using the

command.`kubectl delete nginxingresscontroller`

`kubectl delete nginxingresscontroller --name $INGRESS_CONTROLLER_NAME`


## Configuration per ingress resource through annotations

The NGINX ingress controller supports adding [annotations to specific ingress objects](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/) to customize their behavior.

You can [annotate](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) the ingress object by adding the respective annotation in the `metadata.annotations`

field.

Note

Annotation keys and values can only be strings. Other types, such as boolean or numeric values must be quoted. For example: `"true"`

, `"false"`

, `"100"`

.

The following sections provide examples for common configurations. For a full list, see the [NGINX ingress annotations documentation](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/).

### Custom max body size

For NGINX, a 413 error is returned to the client when the size in a request exceeds the maximum allowed size of the client request body. To override the default value, use the annotation:

```
nginx.ingress.kubernetes.io/proxy-body-size: 4m
```


Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/proxy-body-size: 4m
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- backend:
service:
name: aks-helloworld
port:
number: 80
path: /
pathType: Prefix
```


### Custom connection timeout

You can change the timeout that the NGINX ingress controller waits to close a connection with your workload. All timeout values are unitless and in seconds. To override the default timeout, use the following annotation to set a valid 120-seconds proxy read timeout:

```
nginx.ingress.kubernetes.io/proxy-read-timeout: "120"
```


Review [custom timeouts](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#custom-timeouts) for other configuration options.

Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/proxy-read-timeout: "120"
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- backend:
service:
name: aks-helloworld
port:
number: 80
path: /
pathType: Prefix
```


### Backend protocol

The NGINX ingress controller uses `HTTP`

to reach the services by default. To configure alternative backend protocols such as `HTTPS`

or `GRPC`

, use one of the following annotations:

```
# HTTPS annotation
nginx.ingress.kubernetes.io/backend-protocol: "HTTPS"
# GRPC annotation
nginx.ingress.kubernetes.io/backend-protocol: "GRPC"
```


Review [backend protocols](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#backend-protocol) for other configuration options.

Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/backend-protocol: "HTTPS"
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- backend:
service:
name: aks-helloworld
port:
number: 80
path: /
pathType: Prefix
```


### Cross-Origin Resource Sharing (CORS)

To enable Cross-Origin Resource Sharing (CORS) in an Ingress rule, use the following annotation:

```
nginx.ingress.kubernetes.io/enable-cors: "true"
```


Review [enable CORS](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#enable-cors) for other configuration options.

Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/enable-cors: "true"
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- backend:
service:
name: aks-helloworld
port:
number: 80
path: /
pathType: Prefix
```


### Disable SSL redirect

The controller redirects (308) to HTTPS if TLS is enabled for an ingress by default. To disable this feature for specific ingress resources, use the following annotation:

```
nginx.ingress.kubernetes.io/ssl-redirect: "false"
```


Review [server-side HTTPS enforcement through redirect](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#server-side-https-enforcement-through-redirect) for other configuration options.

Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/ssl-redirect: "false"
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- backend:
service:
name: aks-helloworld
port:
number: 80
path: /
pathType: Prefix
```


### URL rewriting

In some scenarios, the exposed URL in the backend service differs from the specified path in the ingress rule. Without a rewrite any request returns 404. This configuration is useful with [path-based routing](https://kubernetes.github.io/ingress-nginx/user-guide/ingress-path-matching/) where you can serve two different web applications under the same domain. You can set path expected by the service using the following annotation:

```
nginx.ingress.kubernetes.io/rewrite-target: /$2
```


Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/rewrite-target: /$2
nginx.ingress.kubernetes.io/use-regex: "true"
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- path: /app-one(/|$)(.*)
pathType: Prefix
backend:
service:
name: app-one
port:
number: 80
- path: /app-two(/|$)(.*)
pathType: Prefix
backend:
service:
name: app-two
port:
number: 80
```


### NGINX health probe path update

The default health probe path for the Azure Load Balancer associated with the NGINX ingress controller must be set to `"/healthz"`

. To ensure correct health checks, verify that the ingress controller service has the following annotation:

```
metadata:
annotations:
service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path: "/healthz"
```


If you're using Helm to manage your NGINX ingress controller, you can define the Azure Load Balancer health-probe annotation in a values file and apply it during an upgrade:

```
controller:
service:
annotations:
service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path: "/healthz"
```


This configuration helps maintain service availability and avoids unexpected traffic disruption during upgrades.

## Next steps

Learn about monitoring the ingress-nginx controller metrics included with the application routing add-on with [with Prometheus in Grafana](app-routing-nginx-prometheus) as part of analyzing the performance and usage of your application.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator -->

# Deploy an AI model on Azure Kubernetes Service (AKS) with the AI toolchain operator add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use the AI toolchain operator add-on to efficiently self-host large language models on Kubernetes, reducing costs and resource complexity, enhancing customization, and maintaining full control over your data.

## About KAITO

Self-hosting large language models (LLMs) on Kubernetes is gaining momentum among organizations with inference workloads at scale, such as batch processing, chatbots, agents, and AI-driven applications. These organizations often have access to commercial-grade GPUs and are seeking alternatives to costly per-token API pricing models, which can quickly scale out of control. Many also require the ability to fine-tune or customize their models, a capability typically restricted by closed-source API providers. Additionally, companies handling sensitive or proprietary data - especially in regulated sectors such as finance, healthcare, or defense - prioritize self-hosting to maintain strict control over data and prevent exposure through third-party systems.

To address these needs and more, the [Kubernetes AI Toolchain Operator (KAITO)](https://github.com/kaito-project/kaito), a Cloud Native Computing Foundation (CNCF) Sandbox project, simplifies the process of deploying and managing open-source LLM workloads on Kubernetes. KAITO integrates with vLLM, a high-throughput inference engine designed to serve large language models efficiently. vLLM as an inference engine helps reduce memory and GPU requirements without significantly compromising accuracy.

Built on top of the open-source KAITO project, the AI toolchain operator managed add-on offers a modular, plug-and-play setup that allows teams to quickly deploy models and expose them via production-ready APIs. It includes built-in features like OpenAI-compatible APIs, prompt formatting, and streaming response support. When deployed on an AKS cluster, KAITO ensures data stays within your organization’s controlled environment, providing a secure, compliant alternative to cloud-hosted LLM APIs.

## Before you begin

- This article assumes a basic understanding of Kubernetes concepts. For more information, see
[Kubernetes core concepts for AKS](concepts-clusters-workloads). - For
and default resource configuration, see the**all hosted model preset images**[KAITO GitHub repository](https://github.com/kaito-project/kaito/tree/main/presets). - The AI toolchain operator add-on currently supports KAITO
**version 0.6.0**, please make a note of this in considering your choice of model from the KAITO model repository.

## Limitations

`AzureLinux`

and`Windows`

OS SKU are not currently supported.- AMD GPU VM sizes are not supported
`instanceType`

in a KAITO workspace. - AI toolchain operator add-on is supported in
**public**Azure regions.

## Prerequisites

If you don't have an Azure subscription, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.If you have multiple Azure subscriptions, make sure you select the correct subscription in which the resources will be created and charged using the

[az account set](/en-us/cli/azure/account#az-account-set)command.Note

Your Azure subscription must have GPU VM quota recommended for your model deployment in the same Azure region as your AKS resources.


Azure CLI version 2.76.0 or later installed and configured. Run

`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The Kubernetes command-line client, kubectl, installed and configured. For more information, see

[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

### Export environment variables

To simplify the configuration steps in this article, you can define environment variables using the following commands. Make sure to replace the placeholder values with your own.

`export AZURE_SUBSCRIPTION_ID="mySubscriptionID" export AZURE_RESOURCE_GROUP="myResourceGroup" export AZURE_LOCATION="myLocation" export CLUSTER_NAME="myClusterName"`


## Enable the AI toolchain operator add-on on an AKS cluster

The following sections describe how to create an AKS cluster with the AI toolchain operator add-on enabled and deploy a default hosted AI model.

### Create an AKS cluster with the AI toolchain operator add-on enabled

Create an Azure resource group using the

[az group create](/en-us/cli/azure/group#az-group-create)command.`az group create --name $AZURE_RESOURCE_GROUP --location $AZURE_LOCATION`

Create an AKS cluster with the AI toolchain operator add-on enabled using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command with the`--enable-ai-toolchain-operator`

and`--enable-oidc-issuer`

flags.`az aks create --location $AZURE_LOCATION \ --resource-group $AZURE_RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-ai-toolchain-operator \ --enable-oidc-issuer \ --generate-ssh-keys`

On an existing AKS cluster, you can enable the AI toolchain operator add-on using the

[az aks update](/en-us/cli/azure/aks#az-aks-update)command.`az aks update --name $CLUSTER_NAME \ --resource-group $AZURE_RESOURCE_GROUP \ --enable-ai-toolchain-operator \ --enable-oidc-issuer`


## Connect to your cluster

Configure

`kubectl`

to connect to your cluster using the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command.`az aks get-credentials --resource-group $AZURE_RESOURCE_GROUP --name $CLUSTER_NAME`

Verify the connection to your cluster using the

`kubectl get`

command.`kubectl get nodes`


## Deploy a default hosted AI model

KAITO offers a range of small to large language models hosted as public container images, which can be deployed in one step using a KAITO workspace. You can browse the preset LLM images available in the [KAITO model registry](https://github.com/kaito-project/kaito/tree/main/presets). In this section, we'll use the high-performant multimodal [Microsoft Phi-4-mini](https://techcommunity.microsoft.com/blog/educatordeveloperblog/welcome-to-the-new-phi-4-models---microsoft-phi-4-mini--phi-4-multimodal/4386037) language model as an example:

Deploy the

[Phi-4-mini instruct](https://huggingface.co/microsoft/Phi-4-mini-instruct)model preset for inference from the KAITO model repository using the`kubectl apply`

command.`kubectl apply -f https://raw.githubusercontent.com/kaito-project/kaito/refs/heads/main/examples/inference/kaito_workspace_phi_4_mini.yaml`

Track the live resource changes in your workspace using the

`kubectl get`

command.`kubectl get workspace workspace-phi-4-mini -w`

Note

As you track the KAITO workspace deployment, note that machine readiness can take up to 10 minutes, and workspace readiness up to 20 minutes depending on the size of your model.

Check your inference service and get the service IP address using the

`kubectl get svc`

command.`export SERVICE_IP=$(kubectl get svc workspace-phi-4-mini -o jsonpath='{.spec.clusterIP}')`

Test the Phi-4-mini instruct inference service with a sample input of your choice using the

[OpenAI chat completions API format](https://platform.openai.com/docs/api-reference/chat):`kubectl run -it --rm --restart=Never curl --image=curlimages/curl -- curl -X POST http://$SERVICE_IP/v1/completions -H "Content-Type: application/json" \ -d '{ "model": "phi-4-mini-instruct", "prompt": "How should I dress for the weather today?", "max_tokens": 10 }'`


## Deploy a custom or domain-specific LLM

Open-source LLMs are often trained in different contexts and domains, and the hosted model presets may not always fit the requirements of your application or data. In this case, KAITO also supports inference deployment of newer or domain-specific language models from [HuggingFace](https://huggingface.co/). Try out a custom model inference deployment with KAITO by following [this article](kaito-custom-inference-model).

## Clean up resources

If you no longer need these resources, you can delete them to avoid incurring extra Azure compute charges.

Delete the KAITO workspace using the

`kubectl delete workspace`

command.`kubectl delete workspace workspace-phi-4-mini`

You need to manually delete the GPU node pools provisioned by the KAITO deployment. Use the node label created by

[Phi-4-mini instruct workspace](https://raw.githubusercontent.com/kaito-project/kaito/refs/heads/main/examples/inference/kaito_workspace_phi_4_mini.yaml)to get the node pool name using thecommand. In this example, the node label is "kaito.sh/workspace": "workspace-phi-4-mini".`az aks nodepool list`

`az aks nodepool list --resource-group $AZURE_RESOURCE_GROUP --cluster-name $CLUSTER_NAME`

[Delete the node pool](delete-node-pool)with this name from your AKS cluster and repeat the steps in this section for each KAITO workspace that will be removed.

## Common troubleshooting scenarios

After applying the KAITO model inference workspace, your resource readiness and workspace conditions might not update to `True`

for the following reasons:

- Your Azure subscription doesn't have quota for the minimum GPU instance type specified in your KAITO workspace. You'll need to
[request a quota increase](/en-us/azure/quotas/quickstart-increase-quota-portal)for the GPU VM family in your Azure subscription. - The GPU instance type isn't available in your AKS region. Confirm the
[GPU instance availability in your specific region](https://azure.microsoft.com/explore/global-infrastructure/products-by-region/?regions=&products=virtual-machines)and switch the Azure region if your GPU VM family isn't available.

## Next steps

Learn more about KAITO model deployment options below:

- Deploy LLMs with your application on AKS using
[KAITO in Visual Studio Code](aks-extension-kaito). [Monitor your KAITO inference workload](ai-toolchain-operator-monitoring).[Fine tune a model](ai-toolchain-operator-fine-tune)with the AI toolchain operator add-on on AKS.- Configure and test
[tool calling with KAITO inference](ai-toolchain-operator-tool-calling). - Integrate an
[MCP server with the AI toolchain operator](ai-toolchain-operator-mcp)add-on on AKS.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-apply-l7-policies -->

# Set up Layer 7(L7) policies with Advanced Container Networking Services

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article demonstrates how to set up L7 policies with Advanced Container Networking Services in AKS clusters. Continue only after you have reviewed the limitations and considerations listed on the [Layer 7 Policy Overview](container-network-security-l7-policy-concepts) page.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of Azure CLI required for the steps in this article is 2.79.0. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Install the `aks-preview`

Azure CLI extension

Install or update the Azure CLI preview extension using the [ az extension add](/en-us/cli/azure/extension#az-extension-add) or

[command.](/en-us/cli/azure/extension#az-extension-update)

`az extension update`

The minimum version of the aks-preview Azure CLI extension is `14.0.0b6`


```
# Install the aks-preview extension
az extension add --name aks-preview
# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```


### Register the `AdvancedNetworkingL7PolicyPreview`

feature flag

Register the `AdvancedNetworkingL7PolicyPreview`

feature flag using the [ az feature register](/en-us/cli/azure/feature#az-feature-register) command.

```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"
```


Verify successful registration using the [ az feature show](/en-us/cli/azure/feature#az-feature-show) command. It takes a few minutes for the registration to complete.

```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"
```


Once the feature shows `Registered`

, refresh the registration of the `Microsoft.ContainerService`

resource provider using the [ az provider register](/en-us/cli/azure/provider#az-provider-register) command.

### Enable Advanced Container Networking Services

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. These features encompass:

**Container Network Observability:**Provides insights into your network traffic. To learn more visit[Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability).**Container Network Security:**Offers security features like Fully Qualified Domain Name (FQDN) filtering. To learn more visit[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security).

Note

Clusters with the Cilium data plane support Container Network Observability and Container Network security starting with Kubernetes version 1.29.

For this demo, the `--acns-advanced-networkpolicies`

parameter must be set to "L7" to enable L7 policies. Setting this parameter to "L7" also enables FQDN filtering. If you only want to enable FQDN filtering, set the parameter to "FQDN". To disable both features, you can follow the instructions provided in [Disable Container Network Security](advanced-container-networking-services-overview).

```
export CLUSTER_NAME="<aks-cluster-name>"
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--network-plugin azure \
--network-dataplane cilium \
--enable-acns \
--acns-advanced-networkpolicies L7
```


### Enable Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the Advanced Container Networking Services flag,

`--enable-acns`

, updates an existing AKS cluster with all Advanced Container Networking Services features which includes [Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability)and the

[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security)feature.

Note

Only clusters with the Cilium data plane support Container Network Security features of Advanced Container Networking Services.

For this demo, the `--acns-advanced-networkpolicies`

parameter must be set to "L7" to enable L7 policies. Setting this parameter to "L7" also enables FQDN filtering. If you only want to enable FQDN filtering, set the parameter to "FQDN". To disable both features, you can follow the instructions provided in [Disable Container Network Security](advanced-container-networking-services-overview).

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns \
--acns-advanced-networkpolicies L7
```


## Get cluster credentials

Get your cluster credentials using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Set up http-server application on your AKS cluster

Apply the below YAML to your AKS cluster to set up the `http-server`

application.

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: http-server
labels:
app: http-server
spec:
replicas: 1
selector:
matchLabels:
app: http-server
template:
metadata:
labels:
app: http-server
spec:
containers:
- name: http-server
image: nginx:latest
ports:
- containerPort: 8080
volumeMounts:
- name: config-volume
mountPath: /etc/nginx/conf.d
volumes:
- name: config-volume
configMap:
name: nginx-config
---
apiVersion: v1
kind: Service
metadata:
name: http-server
spec:
selector:
app: http-server
ports:
- protocol: TCP
port: 80
targetPort: 8080
---
apiVersion: v1
kind: ConfigMap
metadata:
name: nginx-config
data:
default.conf: |
server {
listen 8080;
location / {
return 200 "Hello from the server root!\n";
}
location /products {
return 200 "Listing products...\n";
}
}
```


## Set up http-client application on your AKS Cluster

Apply the below YAML to your AKS cluster to set up the `http-client`

application.

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: http-client
labels:
app: http-client
spec:
replicas: 1
selector:
matchLabels:
app: http-client
template:
metadata:
labels:
app: http-client
spec:
containers:
- name: http-client
image: curlimages/curl:latest
command: ["sleep", "infinity"]
```


## Test connectivity with a policy

Next, apply the following Layer 7 policy to allow only `GET`

requests from the `http-client`

application to the `/products`

endpoint on the `http-server`

:

```
apiVersion: cilium.io/v2
kind: CiliumNetworkPolicy
metadata:
name: allow-get-products
spec:
description: "Allow only GET requests to /products from http-client to http-server"
endpointSelector:
matchLabels:
app: http-server
ingress:
- fromEndpoints:
- matchLabels:
app: http-client
toPorts:
- ports:
- port: "8080"
protocol: TCP
rules:
http:
- method: "GET"
path: "/products"
```


### Verify policy

To verify the policy's enforcement, execute these commands from the `http-client`

pod:

```
kubectl exec -it <your-http-client-pod-name> -n default -- curl -v http://http-server:80/products
```


You should expect an output like `Listing products...`

when you run the above command

```
kubectl exec -it <your-http-client-pod-name> -n default -- curl -v -XPOST http://http-server:80/products -d "test=data"
```


You should expect an output like `Access Denied`

when you run the above command

### Observing L7 metrics

If you have Advanced Container Network Service's container network observability enabled, you can visualize the traffic on Grafana.

To simplify the analysis of these L7 metrics, we provide preconfigured Azure Managed Grafana dashboards. You can find them under the **Dashboards > Azure Managed Prometheus** folder, with filenames like **"Kubernetes/Networking/L7 (Namespace)"** and **"Kubernetes/Networking/L7 (Workload)"**.

You should see metrics similar to the following:

## Clean up resources

If you don't plan on using this application, delete the other resources you created in this article using the [ az group delete](/en-us/cli/azure/#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP
```


## Next steps

In this how-to article, you learned how to enable and apply L7 Policies with Advanced Container Networking Services for your AKS cluster.

- For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see
[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/configure-kubenet -->

# Use kubenet networking with your own IP address ranges in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

On **31 March 2028**, kubenet networking for Azure Kubernetes Service (AKS) will be retired.

To avoid service disruptions, **you'll need to** [upgrade to Azure Container Networking Interface (CNI) overlay](/en-us/azure/aks/upgrade-aks-ipam-and-dataplane#upgrade-an-existing-cluster-to-azure-cni-overlay) **before that date**, when workloads running on kubenet for AKS will no longer be supported.

AKS clusters use kubenet and create an Azure virtual network and subnet for you by default. With kubenet, nodes get an IP address from the Azure virtual network subnet. Pods receive an IP address from a logically different address space to the Azure virtual network subnet of the nodes. Network address translation (NAT) is then configured so the pods can reach resources on the Azure virtual network. The source IP address of the traffic is NAT'd to the node's primary IP address. This approach greatly reduces the number of IP addresses you need to reserve in your network space for pods to use.

With [Azure Container Networking Interface (CNI)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md), every pod gets an IP address from the subnet and can be accessed directly. These IP addresses must be planned in advance and unique across your network space. Each node has a configuration parameter for the maximum number of pods it supports. The equivalent number of IP addresses per node are then reserved up front for that node. This approach requires more planning, and often leads to IP address exhaustion or the need to rebuild clusters in a larger subnet as your application demands grow. You can configure the maximum pods deployable to a node at cluster creation time or when creating new node pools. If you don't specify `maxPods`

when creating new node pools, you receive a default value of *110* for kubenet.

This article shows you how to use kubenet networking to create and use a virtual network subnet for an AKS cluster. For more information on network options and considerations, see [Network concepts for Kubernetes and AKS](concepts-network).

## Prerequisites

- The virtual network for the AKS cluster must allow outbound internet connectivity.
- Don't create more than one AKS cluster in the same subnet.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for the Kubernetes service address range, pod address range, or cluster virtual network address range. The range can't be updated after you create your cluster. - The cluster identity used by the AKS cluster must at least have the
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)role on the subnet within your virtual network. CLI helps set the role assignment automatically. If you're using an ARM template or other clients, you need to manually set the role assignment. You must also have the appropriate permissions, such as the subscription owner, to create a cluster identity and assign it permissions. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, you need the following permissions:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


Warning

To use Windows Server node pools, you must use Azure CNI. The kubenet network model isn't available for Windows Server containers.

## Before you begin

You need the Azure CLI version 2.0.65 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Overview of kubenet networking with your own subnet

In many environments, you have defined virtual networks and subnets with allocated IP address ranges, and you use these resources to support multiple services and applications. To provide network connectivity, AKS clusters can use *kubenet* (basic networking) or Azure CNI (*advanced networking*).

With *kubenet*, only the nodes receive an IP address in the virtual network subnet. Pods can't communicate directly with each other. Instead, User Defined Routing (UDR) and IP forwarding handle connectivity between pods across nodes. UDRs and IP forwarding configuration is created and maintained by the AKS service by default, but you can [bring your own route table for custom route management](#bring-your-own-subnet-and-route-table-with-kubenet) if you want. You can also deploy pods behind a service that receives an assigned IP address and load balances traffic for the application. The following diagram shows how the AKS nodes receive an IP address in the virtual network subnet, but not the pods:

Azure supports a maximum of *400* routes in a UDR, so you can't have an AKS cluster larger than 400 nodes. AKS [virtual nodes](virtual-nodes-cli) and Azure Network Policies aren't supported with *kubenet*. [Calico Network Policies](https://docs.projectcalico.org/v3.9/security/calico-network-policy) are supported.

With *Azure CNI*, each pod receives an IP address in the IP subnet and can communicate directly with other pods and services. Your clusters can be as large as the IP address range you specify. However, you must plan the IP address range in advance, and all the IP addresses are consumed by the AKS nodes based on the maximum number of pods they can support. Advanced network features and scenarios such as [virtual nodes](virtual-nodes-cli) or Network Policies (either Azure or Calico) are supported with *Azure CNI*.

### Limitations & considerations for kubenet

- An additional hop is required in the design of kubenet, which adds minor latency to pod communication.
- Route tables and user-defined routes are required for using kubenet, which adds complexity to operations.
- For more information, see
[Customize cluster egress with a user-defined routing table in AKS](egress-udr)and[Customize cluster egress with outbound types in AKS](egress-outboundtype).

- For more information, see
- Direct pod addressing isn't supported for kubenet due to kubenet design.
- Unlike Azure CNI clusters, multiple kubenet clusters can't share a subnet.
- AKS doesn't apply Network Security Groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure the security rules in the NSGs allow traffic between the node and pod CIDR. For more details, see
[Network security groups](concepts-network#network-security-groups). - Features
**not supported on kubenet**include:

Note

Some of the system pods such as **konnectivity** within the cluster use the host node IP address rather than an IP from the overlay address space. The system pods will only use the node IP and not an IP address from the virtual network.

### IP address availability and exhaustion

A common issue with *Azure CNI* is that the assigned IP address range is too small to then add more nodes when you scale or upgrade a cluster. The network team also might not be able to issue a large enough IP address range to support your expected application demands.

As a compromise, you can create an AKS cluster that uses *kubenet* and connect to an existing virtual network subnet. This approach lets the nodes receive defined IP addresses without the need to reserve a large number of IP addresses up front for any potential pods that could run in the cluster. With *kubenet*, you can use a much smaller IP address range and support large clusters and application demands. For example, with a */27* IP address range on your subnet, you can run a 20-25 node cluster with enough room to scale or upgrade. This cluster size can support up to *2,200-2,750* pods (with a default maximum of 110 pods per node). The maximum number of pods per node that you can configure with *kubenet* in AKS is 250.

The following basic calculations compare the difference in network models:

**kubenet**: A simple*/24*IP address range can support up to*251*nodes in the cluster. Each Azure virtual network subnet reserves the first three IP addresses for management operations. This node count can support up to*27,610*pods, with a default maximum of 110 pods per node.**Azure CNI**: That same basic*/24*subnet range can only support a maximum of*eight*nodes in the cluster. This node count can only support up to*240*pods, with a default maximum of 30 pods per node.

Note

These maximums don't take into account upgrade or scale operations. In practice, you can't run the maximum number of nodes the subnet IP address range supports. You must leave some IP addresses available for scaling or upgrading operations.

### Virtual network peering and ExpressRoute connections

To provide on-premises connectivity, both *kubenet* and *Azure-CNI* network approaches can use [Azure virtual network peering](/en-us/azure/virtual-network/virtual-network-peering-overview) or [ExpressRoute connections](/en-us/azure/expressroute/expressroute-introduction). Plan your IP address ranges carefully to prevent overlap and incorrect traffic routing. For example, many on-premises networks use a *10.0.0.0/8* address range that's advertised over the ExpressRoute connection. We recommend creating your AKS clusters in Azure virtual network subnets outside this address range, such as *172.16.0.0/16*.

### Choose a network model to use

The following considerations help outline when each network model may be the most appropriate:

**Use kubenet when**:

- You have limited IP address space.
- Most of the pod communication is within the cluster.
- You don't need advanced AKS features, such as virtual nodes or Azure Network Policy.

**Use Azure CNI when**:

- You have available IP address space.
- Most of the pod communication is to resources outside of the cluster.
- You don't want to manage user defined routes for pod connectivity.
- You need AKS advanced features, such as virtual nodes or Azure Network Policy.

For more information to help you decide which network model to use, see [Compare network models and their support scope](concepts-network-cni-overview).

## Create a virtual network and subnet

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

If you don't have an existing virtual network and subnet to use, create these network resources using the

command. The following example command creates a virtual network named`az network vnet create`

*myAKSVnet*with the address prefix of*192.168.0.0/16*and a subnet named*myAKSSubnet*with the address prefix*192.168.1.0/24*:`az network vnet create \ --resource-group myResourceGroup \ --name myAKSVnet \ --address-prefixes 192.168.0.0/16 \ --subnet-name myAKSSubnet \ --subnet-prefix 192.168.1.0/24 \ --location eastus`

Get the subnet resource ID using the

command and store it as a variable named`az network vnet subnet show`

`SUBNET_ID`

for later use.`SUBNET_ID=$(az network vnet subnet show --resource-group myResourceGroup --vnet-name myAKSVnet --name myAKSSubnet --query id -o tsv)`


## Create an AKS cluster in the virtual network

### Create an AKS cluster with system-assigned managed identities

Note

When using system-assigned identity, the Azure CLI grants the Network Contributor role to the system-assigned identity after the cluster is created. If you're using an ARM template or other clients, you need to use the [user-assigned managed identity](configure-kubenet#create-an-aks-cluster-with-user-assigned-managed-identity) instead.

Create an AKS cluster with system-assigned managed identities using the

command.`az aks create`

`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --network-plugin kubenet \ --service-cidr 10.0.0.0/16 \ --dns-service-ip 10.0.0.10 \ --pod-cidr 10.244.0.0/16 \ --vnet-subnet-id $SUBNET_ID \ --generate-ssh-keys`

Deployment parameters:

*--service-cidr*is optional. This address is used to assign internal services in the AKS cluster an IP address. This IP address range should be an address space that isn't in use elsewhere in your network environment, including any on-premises network ranges if you connect, or plan to connect, your Azure virtual networks using Express Route or a Site-to-Site VPN connection. The default value is 10.0.0.0/16.*--dns-service-ip*is optional. The address should be the*.10*address of your service IP address range. The default value is 10.0.0.10.*--pod-cidr*is optional. This address should be a large address space that isn't in use elsewhere in your network environment. This range includes any on-premises network ranges if you connect, or plan to connect, your Azure virtual networks using Express Route or a Site-to-Site VPN connection. The default value is 10.244.0.0/16.- This address range must be large enough to accommodate the number of nodes that you expect to scale up to. You can't change this address range once the cluster is deployed.
- The pod IP address range is used to assign a
*/24*address space to each node in the cluster. In the following example, the*--pod-cidr*of*10.244.0.0/16*assigns the first node*10.244.0.0/24*, the second node*10.244.1.0/24*, and the third node*10.244.2.0/24*. - As the cluster scales or upgrades, the Azure platform continues to assign a pod IP address range to each new node.


### Create an AKS cluster with user-assigned managed identity

#### Create a managed identity

Create a managed identity using the

command. If you have an existing managed identity, find the principal ID using the`az identity`

`az identity show --ids <identity-resource-id>`

command instead.`az identity create --name myIdentity --resource-group myResourceGroup`

Your output should resemble the following example output:

`{ "clientId": "<client-id>", "clientSecretUrl": "<clientSecretUrl>", "id": "/subscriptions/<subscriptionid>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myIdentity", "location": "westus2", "name": "myIdentity", "principalId": "<principal-id>", "resourceGroup": "myResourceGroup", "tags": {}, "tenantId": "<tenant-id>", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


#### Add role assignment for managed identity

If you're using the Azure CLI, the role is automatically added and you can skip this step. If you're using an ARM template or other clients, you need to use the Principal ID of the cluster managed identity to perform a role assignment.

Get the virtual network resource ID using the

command and store it as a variable named`az network vnet show`

`VNET_ID`

.`VNET_ID=$(az network vnet show --resource-group myResourceGroup --name myAKSVnet --query id -o tsv)`

Assign the managed identity for your AKS cluster

*Network Contributor*permissions on the virtual network using thecommand and provide the`az role assignment create`

*<principalId>*.`az role assignment create --assignee <control-plane-identity-principal-id> --scope $VNET_ID --role "Network Contributor" # Example command az role assignment create --assignee 22222222-2222-2222-2222-222222222222 --scope "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myAKSVnet" --role "Network Contributor"`


Note

Permission granted to your cluster's managed identity used by Azure may take up 60 minutes to populate.

#### Create an AKS cluster

Create an AKS cluster using the

command and provide the control plane's managed identity resource ID for the`az aks create`

`assign-identity`

argument to assign the user-assigned managed identity.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 3 \ --network-plugin kubenet \ --vnet-subnet-id $SUBNET_ID \ --assign-identity <identity-resource-id> \ --generate-ssh-keys`


When you create an AKS cluster, a network security group and route table are automatically created. These network resources are managed by the AKS control plane. The network security group is automatically associated with the virtual NICs on your nodes. The route table is automatically associated with the virtual network subnet. Network security group rules and route tables are automatically updated as you create and expose services.

## Bring your own subnet and route table with kubenet

With kubenet, a route table must exist on your cluster subnet(s). AKS supports bringing your own existing subnet and route table. If your custom subnet doesn't contain a route table, AKS creates one for you and adds rules throughout the cluster lifecycle. If your custom subnet contains a route table when you create your cluster, AKS acknowledges the existing route table during cluster operations and adds/updates rules accordingly for cloud provider operations.

Warning

You can add/update custom rules on the custom route table. However, rules are added by the Kubernetes cloud provider which can't be updated or removed. Rules such as *0.0.0.0/0* generally exist on a given route table (unless the egress outbound type is `none`

) and map to the target of your internet gateway, such as an NVA or other egress gateway. Take caution when updating rules.

Learn more about setting up a [custom route table](/en-us/azure/virtual-network/manage-route-table).

Kubenet networking requires organized route table rules to successfully route requests. Due to this design, route tables must be carefully maintained for each cluster that relies on it. Multiple clusters can't share a route table because pod CIDRs from different clusters might overlap which causes unexpected and broken routing scenarios. When configuring multiple clusters on the same virtual network or dedicating a virtual network to each cluster, consider the following limitations:

- A custom route table must be associated to the subnet before you create the AKS cluster.
- The associated route table resource can't be updated after cluster creation. However, custom rules can be modified on the route table.
- Each AKS cluster must use a single, unique route table for all subnets associated with the cluster. You can't reuse a route table with multiple clusters due to the potential for overlapping pod CIDRs and conflicting routing rules.
- For system-assigned managed identity, it's only supported to provide your own subnet and route table via Azure CLI because Azure CLI automatically adds the role assignment. If you're using an ARM template or other clients, you must use a
[user-assigned managed identity](configure-kubenet#create-an-aks-cluster-with-user-assigned-managed-identity), assign permissions before cluster creation, and ensure the user-assigned identity has write permissions to your custom subnet and custom route table. - Using the same route table with multiple AKS clusters isn't supported.

Note

When you create and use your own VNet and route table with the kubenet network plugin, you must configure a [user-assigned managed identity](use-managed-identity#create-a-user-assigned-managed-identity) for the cluster. With a system-assigned managed identity, you can't retrieve the identity ID before creating a cluster, which causes a delay during role assignment.

Both system-assigned and user-assigned managed identities are supported when you create and use your own VNet and route table with the Azure network plugin. We highly recommend using a user-assigned managed identity for BYO scenarios.

### Add a route table with a user-assigned managed identity to your AKS cluster

After creating a custom route table and associating it with a subnet in your virtual network, you can create a new AKS cluster specifying your route table with a user-assigned managed identity. You need to use the subnet ID for where you plan to deploy your AKS cluster. This subnet also must be associated with your custom route table.

Get the subnet ID using the

command.`az network vnet subnet list`

`az network vnet subnet list --resource-group myResourceGroup --vnet-name myAKSVnet [--subscription]`

Create an AKS cluster with a custom subnet pre-configured with a route table using the

command and providing your values for the`az aks create`

`--vnet-subnet-id`

and`--assign-identity`

parameters.`az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --vnet-subnet-id mySubnetIDResourceID \ --assign-identity controlPlaneIdentityResourceID \ --generate-ssh-keys`


## Next steps

This article showed you how to deploy your AKS cluster into your existing virtual network subnet. Now, you can start [creating new apps using Helm](quickstart-helm) or [deploying existing apps using Helm](kubernetes-helm).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/migrate-from-npm-to-cilium-network-policy -->

# Migrate from Network Policy Manager (NPM) to Cilium Network Policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, we provide a comprehensive guide to plan, execute, and validate the migration from Network Policy Manager (NPM) to Cilium Network Policy. The goal is to ensure policy parity, minimize service disruption, and align with Azure CNI's strategic direction toward eBPF-based networking and enhanced observability.

Important

This guide applies exclusively to AKS clusters running Linux nodes. Cilium Network Policy isn't currently supported for Windows nodes in AKS.

## Key considerations before you begin

- Policy Compatibility: NPM and Cilium differ in enforcement models. Before migration you need to validate that existing policies are compatible or identify required changes. Refer to the Pre-Migration Validation section for guidance.
- Downtime Expectations: Policy enforcement might be temporarily inconsistent during node reimaging.
- Windows Node Pools: Cilium Network Policy isn't currently supported for Windows nodes in AKS.

## Pre-migration validation

Before migrating from Network Policy Manager (NPM) to Cilium Network Policy, it's important to assess the compatibility of your existing network policies. While most policies continue to function as expected post-migration, there are specific scenarios where behavior might differ between NPM and Cilium. These differences could require updates to your policies either before or after the migration to ensure consistent enforcement and avoid unintended traffic drops. In this section, we outline known scenarios where policy adjustments might be necessary. We explain why it matters, and provide guidance on what actions—if any—are required to make your policies Cilium-compatible.

### NetworkPolicy with endPort

Note

Cilium started supporting the `endPort`

field in Kubernetes NetworkPolicy in version 1.17.

The endPort field allows you to define a range of ports in a single rule, rather than specifying individual ports.

Here's an example of a Kubernetes NetworkPolicy that uses the endPort field:

```
egress:
- to:
- ipBlock:
cidr: 10.0.0.0/24
ports:
- protocol: TCP
port: 32000
endPort: 32768
```


**Action Required:**

- If your AKS cluster is running Cilium version 1.17 or later, no changes are needed as endPort is fully supported.
- If your cluster is running a Cilium version earlier than 1.17, remove the endPort field from any policies before migrating. Use explicit single-port entries instead.

### NetworkPolicy with ipBlock

The ipBlock field in Kubernetes NetworkPolicy allows you to define CIDR ranges for ingress sources or egress destinations. These ranges can include external IPs, Pod IPs, or Node IPs. However, Cilium doesn't allow egress to Pod or Node IPs using ipBlock, even if those IPs fall within the specified CIDR range.

For example, the following NetworkPolicy uses an ipBlock to allow all egress traffic to 0.0.0.0/0:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: example-ipblock
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 0.0.0.0/0
```


- Under NPM, this policy would allow egress to all destinations, including Pods and Nodes.
- After migrating to Cilium, egress to Pod and Node IPs will be blocked, even though they fall within the 0.0.0.0/0 range.

**Action Required:**

- To allow traffic to Pod IPs, before migration replace the ipBlock with a combination of namespaceSelector and podSelector.

Here's an example of using namespaceSelector and podSelector:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: example-ipblock
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 0.0.0.0/0
- namespaceSelector: {}
- podSelector: {}
```


- For Node IPs, there's no pre-migration workaround. After migration, you must create a CiliumNetworkPolicy that explicitly allows egress to the host and/or remote-node entities. Until this policy is in place, egress traffic to Node IPs is blocked.

Here's an example of CiliumNetworkPolicy to allow traffic from/to local and remote nodes:

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
name: allow-node-egress
namespace: ipblock-test
spec:
endpointSelector: {} # Applies to all pods in the namespace
egress:
- toEntities:
- host # host allows traffic from/to the local node's host network namespace
- remote-node # remote-node allows traffic from/to the remote node's host network namespace
```


### NetworkPolicy with named Ports

Kubernetes NetworkPolicy allows you to reference ports by name instead of number. If you're using named ports in your NetworkPolicies, Cilium might fail to enforce rules correctly and lead to unexpected traffic being blocked. This issue happens when the same port name is used for different ports.
For more information, see [Cilium GitHub issue #30003](https://github.com/cilium/cilium/issues/30003).

Here's an example of NetworkPolicy uses Named port to allow egress traffic:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
annotations:
name: allow-egress
namespace: default
spec:
podSelector:
matchLabels:
network-rules-egress: cilium-np-test
egress:
- ports:
- port: http-test # Named port
protocol: TCP
policyTypes:
- Egress
```


**Action Required:**

- Before migration, replace all named ports in your policies with their corresponding numeric values.

### NetworkPolicy with Egress Policies

Kubernetes NetworkPolicy on NPM doesn't block egress traffic from a pod to its own node's IP, this traffic is implicitly allowed. After you migrate to Cilium, this behavior will change, and traffic to local nodes that was previously allowed will be blocked unless explicitly allowed.

For example, the following policy allows egress only to an internal API subnet:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: allow-egress
namespace: default
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 10.20.30.0/24
```


- With NPM: Egress traffic to 10.20.30.0/24 is allowed explicitly, and egress traffic to the local node is allowed implicitly.
- With Cilium: Only traffic to 10.20.30.0/24 is allowed; egress to the node IP is blocked unless you permit it explicitly.

**Action Required:**

- Review all existing egress policies for your workloads.
- If your applications rely on NPM's implicit allow behavior for egress to the local node, you must add explicit egress rules to maintain connectivity after migration.
- You can add a CiliumNetworkPolicy after migration to explicitly allow egress traffic to the local host.

### Ingress policy behavior changes

Under Network Policy Manager (NPM), ingress traffic arriving via a LoadBalancer or NodePort service with "externalTrafficPolicy=Cluster" - which is the default setting - isn't subject to ingress policy enforcement. This behavior means that even if a pod has a restrictive ingress policy, traffic from external sources might still reach it via loadbalancer or nodeport services.

In contrast, Cilium enforces ingress policies on all traffic, including traffic routed internally due to externalTrafficPolicy=Cluster. As a result, after migration, traffic that was previously allowed might be dropped if the appropriate ingress rules aren't explicitly defined.

For example, Customer creates a network policy to deny all in ingress traffic

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: default-deny-ingress
spec:
podSelector: {}
policyTypes:
- Ingress
```


- With NPM: Direct connection to the pod or via ClusterIP service is blocked. However, access through NodePort or LoadBalancer is still allowed despite the deny-all policy.
- With Cilium: All ingress traffic is blocked, including traffic via NodePort or LoadBalancer, unless explicitly allowed.

**Action Required:**

- Review all ingress policies for workloads behind LoadBalancer or NodePort services using externalTrafficPolicy=Cluster.
- Ensure that ingress rules explicitly allow traffic from the expected external sources (for example, IP ranges, namespaces, or labels).
- If your policy currently relies on the implicit allow behavior under NPM, you must add explicit ingress rules to maintain connectivity after migration.

## Upgrade to Azure CNI Powered by Cilium

To use Cilium Network Policy, your AKS cluster must be running Azure CNI powered by Cilium. When you enable Cilium in a cluster currently using NPM, the existing NPM engine is automatically uninstalled and replaced with Cilium.

Warning

The upgrade process triggers each node pool to be reimaged simultaneously. Upgrading each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image upgrade or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium will begin enforcing network policies only after all nodes are reimaged.

Important

These instructions apply to clusters upgrading from Azure CNI to Azure CNI with the Cilium dataplane. Upgrades from bring-your-own CNIs or changes the IPAM mode aren't covered here. For more information, see [Upgrade Azure CNI documentation](update-azure-cni).

To perform the upgrade, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Use the following command to upgrade an existing cluster to Azure CNI Powered by Cilium. Replace the values for `clusterName`

and `resourceGroupName`

:

```
az aks update --name <clusterName> --resource-group <resourceGroupName> --network-dataplane cilium
```


## Next steps

For more information about using Cilium FQDN network policy on AKS, see

[Set up FQDN filtering feature for Container Network Security in Advanced Container Networking Services](how-to-apply-fqdn-filtering-policies).For more information about using Cilium L7 network policy on AKS, see

[Set up Layer 7(L7) policies with Advanced Container Networking Services](how-to-apply-l7-policies).For more information about network policy best practices on aks, see

[Best practices for network policies in Azure Kubernetes Service (AKS)](network-policy-best-practices)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-system-pools -->

# Manage system node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure Kubernetes Service (AKS), nodes of the same configuration are grouped together into *node pools*. Node pools contain the underlying VMs that run your applications. System node pools and user node pools are two different node pool modes for your AKS clusters. System node pools serve the primary purpose of hosting critical system pods such as `CoreDNS`

and `metrics-server`

. User node pools serve the primary purpose of hosting your application pods. However, application pods can be scheduled on system node pools if you wish to only have one pool in your AKS cluster. Every AKS cluster must contain at least one system node pool with at least two nodes.

Important

If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool.

This article explains how to manage system node pools in AKS. For information about how to use multiple node pools, see [use multiple node pools](use-multiple-node-pools).

## Before you begin

You need the Azure CLI version 2.3.1 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Limitations

The following limitations apply when you create and manage AKS clusters that support system node pools.

- See
[Quotas, VM size restrictions, and region availability in AKS](quotas-skus-regions). - An API version of 2020-03-01 or greater must be used to set a node pool mode. Clusters created on API versions older than 2020-03-01 contain only user node pools, but can be migrated to contain system node pools by following
[update pool mode steps](#update-existing-cluster-system-and-user-node-pools). - The name of a node pool may only contain lowercase alphanumeric characters and must begin with a lowercase letter. For Linux node pools, the length must be between 1 and 12 characters. For Windows node pools, the length must be between one and six characters.
- The mode of a node pool is a required property and must be explicitly set when using ARM templates or direct API calls.

## System and user node pools

For a system node pool, AKS automatically assigns the label **kubernetes.azure.com/mode: system** to its nodes. This causes AKS to prefer scheduling system pods on node pools that contain this label. This label doesn't prevent you from scheduling application pods on system node pools. However, we recommend you isolate critical system pods from your application pods to prevent misconfigured or rogue application pods from accidentally deleting system pods.

You can enforce this behavior by creating a dedicated system node pool. Use the `CriticalAddonsOnly=true:NoSchedule`

taint to prevent application pods from being scheduled on system node pools.

System node pools have the following restrictions:

- System node pools must support at least 30 pods as described by the
[minimum and maximum value formula for pods](concepts-network-ip-address-planning#maximum-pods-per-node). - System pools osType must be Linux.
- User node pools osType may be Linux or Windows.
- System pools must contain at least two nodes, and user node pools may contain zero or more nodes.
- System node pools require a VM SKU of at least 4 vCPUs and 4GB memory.
[B series VMs](/en-us/azure/virtual-machines/sizes-b-series-burstable)are not supported for system node pools.- A minimum of three nodes of 8 vCPUs or two nodes of at least 16 vCPUs is recommended (for example, Standard_DS4_v2), especially for large clusters (Multiple CoreDNS Pod replicas, 3-4+ add-ons, etc.).
- Spot node pools require user node pools.
- Adding another system node pool or changing which node pool is a system node pool
*does not*automatically move system pods. System pods can continue to run on the same node pool, even if you change it to a user node pool. If you delete or scale down a node pool running system pods that were previously a system node pool, those system pods are redeployed with preferred scheduling to the new system node pool.

You can do the following operations with node pools:

- Create a dedicated system node pool (prefer scheduling of system pods to node pools of
`mode:system`

) - Change a system node pool to be a user node pool, provided you have another system node pool to take its place in the AKS cluster.
- Change a user node pool to be a system node pool.
- Delete user node pools.
- You can delete system node pools, provided you have another system node pool to take its place in the AKS cluster.
- An AKS cluster may have multiple system node pools and requires at least one system node pool.
- If you want to change various immutable settings on existing node pools, you can create new node pools to replace them. One example is to add a new node pool with a new maxPods setting and delete the old node pool.
- Use
[node affinity](operator-best-practices-advanced-scheduler#node-affinity)to*require*or*prefer*which nodes can be scheduled based on node labels. You can set`key`

to`kubernetes.azure.com`

,`operator`

to`In`

, and`values`

of either`user`

or`system`

to your YAML, applying this definition using`kubectl apply -f yourYAML.yaml`

.

## Create a new AKS cluster with a system node pool

When you create a new AKS cluster, the initial node pool defaults to a mode of type `system`

. When you create new node pools with `az aks nodepool add`

, those node pools are user node pools unless you explicitly specify the mode parameter.

The following example creates a resource group named *myResourceGroup* in the *eastus* region.

```
az group create --name myResourceGroup --location eastus
```


Use the [az aks create](/en-us/cli/azure/aks#az-aks-create) command to create an AKS cluster. The following example creates a cluster named *myAKSCluster* with one dedicated system pool containing two nodes. For your production workloads, ensure you're using system node pools with at least three nodes. This operation may take several minutes to complete.

```
# Create a new AKS cluster with a single system pool
az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 2 --generate-ssh-keys
```


## Add a dedicated system node pool to an existing AKS cluster

You can add one or more system node pools to existing AKS clusters. It's recommended to schedule your application pods on user node pools, and dedicate system node pools to only critical system pods. This prevents rogue application pods from accidentally deleting system pods. Enforce this behavior with the `CriticalAddonsOnly=true:NoSchedule`

[taint](manage-node-pools#set-node-pool-taints) for your system node pools.

The following command adds a dedicated node pool of mode type system with a default count of three nodes.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name systempool \
--node-count 3 \
--node-taints CriticalAddonsOnly=true:NoSchedule \
--mode System
```


## Show details for your node pool

You can check the details of your node pool with the following command.

```
az aks nodepool show --resource-group myResourceGroup --cluster-name myAKSCluster --name systempool
```


A mode of type **System** is defined for system node pools, and a mode of type **User** is defined for user node pools. For a system pool, verify the taint is set to `CriticalAddonsOnly=true:NoSchedule`

, which will prevent application pods from beings scheduled on this node pool.

```
{
"agentPoolType": "VirtualMachineScaleSets",
"availabilityZones": null,
"count": 3,
"enableAutoScaling": null,
"enableNodePublicIp": false,
"id": "/subscriptions/yourSubscriptionId/resourcegroups/myResourceGroup/providers/Microsoft.ContainerService/managedClusters/myAKSCluster/agentPools/systempool",
"maxCount": null,
"maxPods": 110,
"minCount": null,
"mode": "System",
"name": "systempool",
"nodeImageVersion": "AKSUbuntu-1604-2020.06.30",
"nodeLabels": {},
"nodeTaints": [
"CriticalAddonsOnly=true:NoSchedule"
],
"orchestratorVersion": "1.16.10",
"osDiskSizeGb": 128,
"osType": "Linux",
"provisioningState": "Succeeded",
"proximityPlacementGroupId": null,
"resourceGroup": "myResourceGroup",
"scaleSetEvictionPolicy": null,
"scaleSetPriority": null,
"spotMaxPrice": null,
"tags": null,
"type": "Microsoft.ContainerService/managedClusters/agentPools",
"upgradeSettings": {
"maxSurge": null
},
"vmSize": "Standard_DS2_v2",
"vnetSubnetId": null
}
```


## Update existing cluster system and user node pools

Note

An API version of 2020-03-01 or greater must be used to set a system node pool mode. Clusters created on API versions older than 2020-03-01 contain only user node pools as a result. To receive system node pool functionality and benefits on older clusters, update the mode of existing node pools with the following commands on the latest Azure CLI version.

You can change modes for both system and user node pools. You can change a system node pool to a user pool only if another system node pool already exists on the AKS cluster.

This command changes a system node pool to a user node pool.

```
az aks nodepool update --resource-group myResourceGroup --cluster-name myAKSCluster --name mynodepool --mode user
```


This command changes a user node pool to a system node pool.

```
az aks nodepool update --resource-group myResourceGroup --cluster-name myAKSCluster --name mynodepool --mode system
```


## Delete a system node pool

Note

To use system node pools on AKS clusters before API version 2020-03-02, add a new system node pool, then delete the original default node pool.

You must have at least two system node pools on your AKS cluster before you can delete one of them.

```
az aks nodepool delete --resource-group myResourceGroup --cluster-name myAKSCluster --name mynodepool
```


## Clean up resources

To delete the cluster, use the [az group delete](/en-us/cli/azure/group#az-group-delete) command to delete the AKS resource group:

```
az group delete --name myResourceGroup --yes --no-wait
```


## Next steps

In this article, you learned how to create and manage system node pools in an AKS cluster. For information about how to start and stop AKS node pools, see [start and stop AKS node pools](start-stop-nodepools).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-confidential-containers-default-policy -->

# Deploy an AKS cluster with Confidential Containers and an automatically generated policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you use the Azure CLI to deploy an Azure Kubernetes Service (AKS) cluster and configure Confidential Containers (preview) with an automatically generated security policy. You then deploy an application as a Confidential container. To learn more, read the [overview of AKS Confidential Containers](confidential-containers-overview).

In general, getting started with AKS Confidential Containers involves the following steps.

- Deploy or upgrade an AKS cluster using the Azure CLI
- Add an annotation to your pod YAML manifest to mark the pod as using confidential containers
- Add a security policy to your pod YAML manifest
- Deploy your application in confidential computing

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Prerequisites

The Azure CLI version 2.44.1 or later. Run

`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The

`aks-preview`

Azure CLI extension version 0.5.169 or later.The

`confcom`

Confidential Container Azure CLI extension 0.3.3 or later.`confcom`

is required to generate a[security policy](/en-us/azure/confidential-computing/confidential-containers-aks-security-policy).Register the

`Preview`

feature in your Azure subscription.AKS supports Confidential Containers (preview) on version 1.25.0 and higher.

A workload identity and a federated identity credential. The workload identity credential enables Kubernetes applications access to Azure resources securely with a Microsoft Entra ID based on annotated service accounts. If you aren't familiar with Microsoft Entra Workload ID, see the

[Microsoft Entra Workload ID overview](/en-us/azure/active-directory/workload-identities/workload-identities-overview)and review how[Workload Identity works with AKS](workload-identity-overview).The identity you're using to create your cluster has the appropriate minimum permissions. For more information about access and identity for AKS, see

[Access and identity options for Azure Kubernetes Service (AKS)](concepts-identity).To manage a Kubernetes cluster, use the Kubernetes command-line client

[kubectl](https://kubernetes.io/docs/reference/kubectl/). Azure Cloud Shell comes with`kubectl`

. You can install kubectl locally using the[az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli)command.Confidential containers on AKS provide a sidecar open source container for attestation and secure key release. The sidecar integrates with a Key Management Service (KMS), like Azure Key Vault, for releasing a key to the container group after validation is completed. Deploying an

[Azure Key Vault Managed HSM](/en-us/azure/key-vault/managed-hsm/overview)(Hardware Security Module) is optional but recommended to support container-level integrity and attestation. See[Provision and activate a Managed HSM](/en-us/azure/key-vault/managed-hsm/quick-create-cli)to deploy Managed HSM.

### Install the aks-preview Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

To install the aks-preview extension, run the following command:

```
az extension add --name aks-preview
```


Run the following command to update to the latest version of the extension:

```
az extension update --name aks-preview
```


### Install the confcom Azure CLI extension

To install the confcom extension, run the following command:

```
az extension add --name confcom
```


Run the following command to update to the latest version of the extension:

```
az extension update --name confcom
```


### Register the KataCcIsolationPreview feature flag

Register the `KataCcIsolationPreview`

feature flag by using the [az feature register](/en-us/cli/azure/feature#az-feature-register) command, as shown in the following example:

```
az feature register --namespace "Microsoft.ContainerService" --name "KataCcIsolationPreview"
```


It takes a few minutes for the status to show *Registered*. Verify the registration status by using the [az feature show](/en-us/cli/azure/feature#az-feature-show) command:

```
az feature show --namespace "Microsoft.ContainerService" --name "KataCcIsolationPreview"
```


When the status reflects *Registered*, refresh the registration of the *Microsoft.ContainerService* resource provider by using the [az provider register](/en-us/cli/azure/provider#az-provider-register) command:

```
az provider register --namespace "Microsoft.ContainerService"
```


## Deploy a new cluster

Create an AKS cluster using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command and specifying the following parameters:**--os-sku**:*AzureLinux*. Only the Azure Linux os-sku supports this feature in this preview release.**--node-vm-size**: Any Azure VM size that supports AMD SEV-SNP protected child VMs works. For example,[Standard_DC8as_cc_v5](/en-us/azure/virtual-machines/dcasccv5-dcadsccv5-series)VMs.**--enable-workload-identity**: Enables creating a Microsoft Entra Workload ID enabling pods to use a Kubernetes identity.**--enable-oidc-issuer**: Enables OpenID Connect (OIDC) Issuer. It allows a Microsoft Entra ID or other cloud provider identity and access management platform the ability to discover the API server's public signing keys.**--workload-runtime**: Specify*KataCcIsolation*to enable the Confidential Containers feature on the node pool.

`az aks create --resource-group myResourceGroup --name myAKSCluster --kubernetes-version <1.25.0 and above> --os-sku AzureLinux --node-vm-size Standard_DC8as_cc_v5 --workload-runtime KataCcIsolation --node-count 1 --enable-oidc-issuer --enable-workload-identity --generate-ssh-keys`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

When the cluster is ready, get the cluster credentials using the

[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Deploy to an existing cluster

To use this feature with an existing AKS cluster, the following requirements must be met:

- Follow the steps to
[register the KataCcIsolationPreview](#register-the-kataccisolationpreview-feature-flag)feature flag. - Verify the cluster is running Kubernetes version 1.25.0 and higher.
[Enable workload identity](workload-identity-deploy-cluster#deploy-and-configure-microsoft-entra-workload-id-on-an-azure-kubernetes-service-aks-cluster)on the cluster if it isn't already.

Use the following command to enable Confidential Containers (preview) by creating a node pool to host it.

Add a node pool to your AKS cluster using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command. Specify the following parameters:**--resource-group**: Enter the name of an existing resource group to create the AKS cluster in.**--cluster-name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--name**: Enter a unique name for your clusters node pool, such as*nodepool2*.**--workload-runtime**: Specify*KataCcIsolation*to enable the feature on the node pool. Along with the`--workload-runtime`

parameter, these other parameters shall satisfy the following requirements. Otherwise, the command fails and reports an issue with the corresponding parameter(s).**--os-sku**:*AzureLinux*. Only the Azure Linux os-sku supports this feature in this preview release.**--node-vm-size**: Any Azure VM size that supports AMD SEV-SNP protected child VMs nested virtualization works. For example,[Standard_DC8as_cc_v5](/en-us/azure/virtual-machines/dcasccv5-dcadsccv5-series)VMs.

The following example adds a user node pool to

*myAKSCluster*with two nodes in*nodepool2*in the*myResourceGroup*:`az aks nodepool add --resource-group myResourceGroup --name nodepool2 –-cluster-name myAKSCluster --node-count 2 --os-sku AzureLinux --node-vm-size Standard_DC8as_cc_v5 --workload-runtime KataCcIsolation`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

Run the

[az aks update](/en-us/cli/azure/aks#az-aks-update)command to enable Confidential Containers (preview) on the cluster.`az aks update --name myAKSCluster --resource-group myResourceGroup`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

When the cluster is ready, get the cluster credentials using the

[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Configure container

Before you configure access to the Azure Key Vault and secret, and deploy an application as a Confidential container, you need to complete the configuration of the workload identity.

To configure the workload identity, perform the following steps described in the [Deploy and configure workload identity](workload-identity-deploy-cluster) article:

- Retrieve the OIDC Issuer URL
- Create a managed identity
- Create Kubernetes service account
- Establish federated identity credential

Important

You need to set the *environment variables* from the section **Export environmental variables** in the [Deploy and configure workload identity](workload-identity-deploy-cluster) article to continue completing this tutorial. Remember to set the variable `SERVICE_ACCOUNT_NAMESPACE`

to `kafka`

, and execute the command `kubectl create namespace kafka`

before configuring workload identity.

## Deploy a trusted application with kata-cc and attestation container

The following steps configure end-to-end encryption for Kafka messages using encryption keys managed by [Azure Managed Hardware Security Modules](/en-us/azure/key-vault/managed-hsm/overview) (mHSM). The key is only released when the Kafka consumer runs within a Confidential Container with an Azure attestation secret provisioning container injected in to the pod.

This configuration is based on the following four components:

- Kafka Cluster: A simple Kafka cluster deployed in the Kafka namespace on the cluster.
- Kafka Producer: A Kafka producer running as a vanilla Kubernetes pod that sends encrypted user-configured messages using a public key to a Kafka topic.
- Kafka Consumer: A Kafka consumer pod running with the kata-cc runtime, equipped with a secure key release container to retrieve the private key for decrypting Kafka messages and render the messages to web UI.

For this preview release, we recommend for test and evaluation purposes to either create or use an existing Azure Key Vault Premium tier resource to support storing keys in a hardware security module (HSM). We don't recommend using your production key vault. If you don't have an Azure Key Vault, see [Create a key vault using the Azure CLI](/en-us/azure/key-vault/general/quick-create-cli).

Grant the managed identity you created earlier, and your account, access to the key vault.

[Assign](/en-us/azure/key-vault/general/rbac-guide#assign-role)both identities the**Key Vault Crypto Officer**and**Key Vault Crypto User**Azure RBAC roles.Note

The managed identity is the value you assign to the

`USER_ASSIGNED_IDENTITY_NAME`

variable.To add role assignments, you must have

`Microsoft.Authorization/roleAssignments/write`

and`Microsoft.Authorization/roleAssignments/delete`

permissions, such as[Key Vault Data Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#key-vault-data-access-administrator),[User Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator), or[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner).You must use the Key Vault Premium SKU to support HSM-protected keys.


Run the following command to set the scope:

`AKV_SCOPE=$(az keyvault show --name <AZURE_AKV_RESOURCE_NAME> --query id --output tsv)`

Run the following command to assign the

**Key Vault Crypto Officer**role.`az role assignment create --role "Key Vault Crypto Officer" --assignee "${USER_ASSIGNED_IDENTITY_NAME}" --scope $AKV_SCOPE`

Run the following command to assign the

**Key Vault Crypto User**role.`az role assignment create --role "Key Vault Crypto User" --assignee "${USER_ASSIGNED_IDENTITY_NAME}" --scope $AKV_SCOPE`

Install the Kafka cluster in the kafka namespace by running the following command:

`kubectl create -f 'https://strimzi.io/install/latest?namespace=kafka' -n kafka`

Run the following command to apply the

`kafka`

cluster CR file.`kubectl apply -f https://strimzi.io/examples/latest/kafka/kafka-persistent-single.yaml -n kafka`

Prepare the RSA Encryption/Decryption key using the

[bash script](https://github.com/microsoft/confidential-container-demos/raw/main/kafka/setup-key.sh)for the workload from GitHub. Save the file as`setup-key.sh`

.Set the

`MAA_ENDPOINT`

environment variable with the FQDN of Attest URI by running the following command.`export MAA_ENDPOINT="$(az attestation show --name "myattestationprovider" --resource-group "MyResourceGroup" --query 'attestUri' -o tsv | cut -c 9-)"`

Check if the FQDN of Attest URI is in correct format (the MAA_ENDPOINT should not include the prefix "https://"):

`echo $MAA_ENDPOINT`

Note

To set up Microsoft Azure Attestation, see

[Quickstart: Set up Azure Attestation with Azure CLI](/en-us/azure/attestation/quickstart-azure-cli).Copy the following YAML manifest and save it as

`consumer.yaml`

.`apiVersion: v1 kind: Pod metadata: name: kafka-golang-consumer namespace: kafka labels: azure.workload.identity/use: "true" app.kubernetes.io/name: kafka-golang-consumer spec: serviceAccountName: workload-identity-sa runtimeClassName: kata-cc-isolation containers: - image: "mcr.microsoft.com/aci/skr:2.7" imagePullPolicy: Always name: skr env: - name: SkrSideCarArgs value: ewogICAgImNlcnRjYWNoZSI6IHsKCQkiZW5kcG9pbnRfdHlwZSI6ICJMb2NhbFRISU0iLAoJCSJlbmRwb2ludCI6ICIxNjkuMjU0LjE2OS4yNTQvbWV0YWRhdGEvVEhJTS9hbWQvY2VydGlmaWNhdGlvbiIKCX0gIAp9 command: - /bin/skr volumeMounts: - mountPath: /opt/confidential-containers/share/kata-containers/reference-info-base64 name: endor-loc - image: "mcr.microsoft.com/acc/samples/kafka/consumer:1.0" imagePullPolicy: Always name: kafka-golang-consumer env: - name: SkrClientKID value: kafka-encryption-demo - name: SkrClientMAAEndpoint value: sharedeus2.eus2.test.attest.azure.net - name: SkrClientAKVEndpoint value: "myKeyVault.vault.azure.net" - name: TOPIC value: kafka-demo-topic command: - /consume ports: - containerPort: 3333 name: kafka-consumer resources: limits: memory: 1Gi cpu: 200m volumes: - name: endor-loc hostPath: path: /opt/confidential-containers/share/kata-containers/reference-info-base64 --- apiVersion: v1 kind: Service metadata: name: consumer namespace: kafka spec: type: LoadBalancer selector: app.kubernetes.io/name: kafka-golang-consumer ports: - protocol: TCP port: 80 targetPort: kafka-consumer`

Note

Update the value for the pod environment variable

`SkrClientAKVEndpoint`

to match the URL of your Azure Key Vault, excluding the protocol value`https://`

. The current value placeholder value is`myKeyVault.vault.azure.net`

. Update the value for the pod environment variable`SkrClientMAAEndpoint`

with the value of`MAA_ENDPOINT`

. You can find the value of`MAA_ENDPOINT`

by running the command`echo $MAA_ENDPOINT`

or the command`az attestation show --name "myattestationprovider" --resource-group "MyResourceGroup" --query 'attestUri' -o tsv | cut -c 9-`

.Generate the security policy for the Kafka consumer YAML manifest and obtain the hash of the security policy stored in the

`WORKLOAD_MEASUREMENT`

variable by running the following command:`export WORKLOAD_MEASUREMENT=$(az confcom katapolicygen -y consumer.yaml --print-policy | base64 -d | sha256sum | cut -d' ' -f1)`

To generate an RSA asymmetric key pair (public and private keys), run the

`setup-key.sh`

script using the following command. The`<Azure Key Vault URL>`

value should be`<your-unique-keyvault-name>.vault.azure.net`

`export MANAGED_IDENTITY=${USER_ASSIGNED_CLIENT_ID} bash setup-key.sh "kafka-encryption-demo" <Azure Key Vault URL>`

Note

The envionment variable

`MANAGED_IDENTITY`

is required by the bash script`setup-key.sh`

.The public key will be saved as

`kafka-encryption-demo-pub.pem`

after executing the bash script.

Important

If you receive the error

`ForbiddenByRbac`

,you might need to wait up to 24 hours as the backend services for managed identities maintain a cache per resource URI for up to 24 hours. See also:[Troubleshoot Azure RBAC](/en-us/azure/role-based-access-control/troubleshooting#symptom---role-assignment-changes-are-not-being-detected).To verify the keys have been successfully uploaded to the key vault, run the following commands:

`az account set --subscription <Subscription ID> az keyvault key list --vault-name <KeyVault Name> -o table`

Copy the following YAML manifest and save it as

`producer.yaml`

.`apiVersion: v1 kind: Pod metadata: name: kafka-producer namespace: kafka spec: containers: - image: "mcr.microsoft.com/acc/samples/kafka/producer:1.0" name: kafka-producer command: - /produce env: - name: TOPIC value: kafka-demo-topic - name: MSG value: "Azure Confidential Computing" - name: PUBKEY value: |- -----BEGIN PUBLIC KEY----- MIIBojAN***AE= -----END PUBLIC KEY----- resources: limits: memory: 1Gi cpu: 200m`

Note

Update the value which begin with

`-----BEGIN PUBLIC KEY-----`

and ends with`-----END PUBLIC KEY-----`

strings with the content from`kafka-encryption-demo-pub.pem`

which was created in the previous step.Deploy the

`consumer`

and`producer`

YAML manifests using the files you saved earlier.`kubectl apply -f consumer.yaml`

`kubectl apply -f producer.yaml`

Get the IP address of the web service using the following command:

`kubectl get svc consumer -n kafka`

Copy and paste the external IP address of the consumer service into your browser and observe the decrypted message.

The following example resembles the output of the command:

`Welcome to Confidential Containers on AKS! Encrypted Kafka Message: Msg 1: Azure Confidential Computing`

You should also attempt to run the consumer as a regular Kubernetes pod by removing the

`skr container`

and`kata-cc runtime class`

spec. Since you aren't running the consumer with kata-cc runtime class, you no longer need the policy.Remove the entire policy and observe the messages again in the browser after redeploying the workload. Messages appear as base64-encoded ciphertext because the private encryption key can't be retrieved. The key can't be retrieved because the consumer is no longer running in a confidential environment, and the

`skr container`

is missing, preventing decryption of messages.

## Cleanup

When you're finished evaluating this feature, to avoid Azure charges, clean up your unnecessary resources. If you deployed a new cluster as part of your evaluation or testing, you can delete the cluster using the [az aks delete](/en-us/cli/azure/aks#az-aks-delete) command.

```
az aks delete --resource-group myResourceGroup --name myAKSCluster
```


If you enabled Confidential Containers (preview) on an existing cluster, you can remove the pod(s) using the [kubectl delete pod](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#delete) command.

```
kubectl delete pod pod-name
```


## Next steps

- Learn more about
[Azure Dedicated hosts](/en-us/azure/virtual-machines/dedicated-hosts)for nodes with your AKS cluster to use hardware isolation and control over Azure platform maintenance events.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning -->

# Overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS), including how it works, upgrade behavior, prerequisites, limitations, and resources to get started.

## What is node auto-provisioning in AKS?

When you deploy workloads onto AKS, you need to select the appropriate virtual machine (VM) size as part of your node pool configuration. As your workloads become more complex, you might have different workloads with varying resource requirements, which makes it more difficult to design your VM configuration for numerous resource requests.

Node auto-provisioning (NAP) simplifies this process by automatically provisioning and managing the optimal VM configuration for your workloads. NAP uses pending pod resource requirements to decide the optimal VM configuration to run your workloads in the most efficient and cost-effective manner.

NAP automatically deploys, configures, and manages Karpenter on your AKS clusters and is based on the open-source [Karpenter](https://karpenter.sh) and [AKS Karpenter provider](https://github.com/Azure/karpenter-provider-azure) projects.

## How does node auto-provisioning work?

Node auto-provisioning provisions, scales, and manages VMs (nodes) in a cluster in response to pending pod pressure.

### Key components of node auto-provisioning

NAP uses the following key components to help manage your cluster's nodes:

| Component | Description |
|---|---|
`NodePool` and `AKSNodeClass` |
Custom Resource Definitions (CRDs) that you create and manage to define node provisioning policies, VM specifications, and constraints for your workloads. |
`NodeClaims` |
Managed by NAP to represent the current state of provisioned nodes that you can monitor. |
| Workload resource requirements | CPU, memory, and other specifications from your Pods, Deployments, Jobs, and other Kubernetes resources that drive provisioning decisions. |

## Kubernetes upgrade behavior for node auto-provisioning nodes

Kubernetes upgrades for node auto-provisioning nodes follow the control plane Kubernetes version. If you perform a cluster upgrade, your nodes are automatically updated to follow the same versioning as your control plane.

We recommend setting a Kubernetes [auto-upgrade](/en-us/azure/aks/auto-upgrade-cluster#cluster-auto-upgrade-channels) channel, which automatically handles Kubernetes upgrades for your cluster. We also recommend setting a [planned maintenance window](planned-maintenance#create-a-maintenance-window) for your cluster. The `aksManagedAutoUpgradeSchedule`

maintenance window allows you to control when to perform cluster upgrades scheduled by your designated auto-upgrade channel. For more information, see [Use planned maintenance to schedule and control upgrades for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Prerequisites

To use node auto-provisioning in AKS, you need the following prerequisites:

- An Azure subscription. If you don't have one, you can create a
[free account](https://azure.microsoft.com/free). - Azure CLI version
`2.76.0`

or later. To find the version, run`az --version`

. For more information about installing or upgrading the Azure CLI, see[Install Azure CLI](/en-us/cli/azure/get-started-with-azure-cli).

## Limitations and unsupported features

The following limitations and unsupported features apply to node auto-provisioning in AKS:

- You can't enable NAP on clusters enabled with the
[cluster autoscaler](cluster-autoscaler). - Windows node pools aren't supported.
- IPv6 clusters aren't supported.
[Service principals](kubernetes-service-principal)aren't supported. You can use either a system-assigned or user-assigned managed identity.[Custom certificate authority (CA) certificates](custom-certificate-authority)aren't supported.- You can't
[stop a cluster](start-stop-cluster)enabled with NAP. [HTTP proxy](http-proxy)isn't supported.- You can't change the
[cluster egress outbound type](egress-outboundtype)after you create a cluster enabled with NAP. - When creating a NAP cluster in a custom virtual network (VNet), you must use a
[Standard Load Balancer](load-balancer-standard). The Basic Load Balancer isn't supported.

## Get started with node auto-provisioning on AKS

The following resources help you get started with node auto-provisioning on AKS:

[Enable or disable node auto-provisioning on an AKS cluster](use-node-auto-provisioning)[Use node auto-provisioning in a custom virtual network](node-auto-provisioning-custom-vnet)[Configure networking for node auto-provisioning on AKS](node-auto-provisioning-networking)[Configure node pools for node auto-provisioning on AKS](node-auto-provisioning-node-pools)[Configure disruption policies for node auto-provisioning on AKS](node-auto-provisioning-disruption)[Upgrade node images for node auto-provisioning on AKS](node-auto-provisioning-upgrade-image)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-cluster-isolation -->

# Best practices for cluster isolation in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you manage clusters in Azure Kubernetes Service (AKS), you often need to isolate teams and workloads. AKS allows flexibility in how you run multi-tenant clusters and isolate resources. To maximize your investment in Kubernetes, it's important you understand AKS multi-tenancy and isolation features.

This best practices article focuses on isolation for cluster operators. In this article, you learn how to:

- Plan for multi-tenant clusters and separation of resources.
- Use logical or physical isolation in your AKS clusters.

## Design clusters for multi-tenancy

Kubernetes lets you logically isolate teams and workloads in the same cluster. The goal is to provide the least number of privileges scoped to the resources each team needs. A Kubernetes [Namespace](concepts-clusters-workloads#namespaces) creates a logical isolation boundary. Other Kubernetes features and considerations for isolation and multi-tenancy include the following areas:

### Scheduling

*Scheduling* uses basic features like resource quotas and pod disruption budgets. For more information about these features, see [Best practices for basic scheduler features in AKS](operator-best-practices-scheduler).

More advanced scheduler features include:

- Taints and tolerations.
- Node selectors.
- Node and pod affinity or anti-affinity.

For more information about these features, see [Best practices for advanced scheduler features in AKS](operator-best-practices-advanced-scheduler).

### Networking

*Networking* uses network policies to control the flow of traffic in and out of pods.

For more information, see [Secure traffic between pods using network policies in AKS](use-network-policies).

### Authentication and authorization

*Authentication and authorization* uses:

- Role-based access control (RBAC).
- Microsoft Entra integration.
- Pod identities.
- Secrets in Azure Key Vault.

For more information about these features, see [Best practices for authentication and authorization in AKS](operator-best-practices-identity).

### Containers

*Containers* include:

- The Azure Policy add-on for AKS to enforce pod security.
- Pod security admission.
- Scanning images and runtime for vulnerabilities.
- Using App Armor or Seccomp (Secure Computing) to restrict container access to the underlying node.

## Logically isolated clusters


Best practice guidanceSeparate teams and projects using

logical isolation. Minimize the number of physical AKS clusters you deploy to isolate teams or applications.

With logical isolation, you can use a single AKS cluster for multiple workloads, teams, or environments. Kubernetes [Namespaces](concepts-clusters-workloads#namespaces) form the logical isolation boundary for workloads and resources.

Logical separation of clusters usually provides a higher pod density than physically isolated clusters, with less excess compute capacity sitting idle in the cluster. When combined with the Kubernetes cluster autoscaler, you can scale the number of nodes up or down to meet demands. This best practice approach minimizes costs by running only the required number of nodes.

Kubernetes environments aren't entirely safe for hostile multi-tenant usage. In a multi-tenant environment, multiple tenants work on a shared infrastructure. If all tenants can't be trusted, you need extra planning to prevent tenants from impacting the security and service of others.

Other security features, like Kubernetes RBAC for nodes, efficiently block exploits. For true security when running hostile multi-tenant workloads, you should only trust a hypervisor. The security domain for Kubernetes becomes the entire cluster and not an individual node.

For these types of hostile multi-tenant workloads, you should use physically isolated clusters.

## Physically isolated clusters


Best practice guidanceMinimize the use of physical isolation for each separate team or application deployment and use

logicalisolation instead.

Physically separating AKS clusters is a common approach to cluster isolation. In this isolation model, teams or workloads are assigned their own AKS cluster. While physical isolation might look like the easiest way to isolate workloads or teams, it adds management and financial overhead. With physically isolated clusters, you must maintain multiple clusters and individually provide access and assign permissions. You're also billed for each individual node.

Physically isolated clusters usually have a low pod density. Since each team or workload has their own AKS cluster, the cluster is often over-provisioned with compute resources. Often, a few pods are scheduled on those nodes. Unclaimed node capacity can't be used for applications or services in development by other teams. These excess resources contribute to the extra costs in physically isolated clusters.

## Next steps

This article focused on cluster isolation. For more information about cluster operations in AKS, see the following best practice articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/virtual-machines-node-pools -->

# Use Virtual Machines node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you'll learn about the new Virtual Machines node pool type for AKS.

With Virtual Machines node pools, AKS directly manages the provisioning and bootstrapping of every single node. For Virtual Machine Scale Sets node pools, AKS manages the model of the Virtual Machine Scale Sets and uses it to achieve consistency across all nodes in the node pool. Virtual Machines node pools enable you to orchestrate your cluster with virtual machines that best fit your individual workloads.

## Overview

### How it works

A node pool consists of a set of virtual machines, where different virtual machine sizes are designated to support different types of workloads. These virtual machine sizes, referred to as SKUs, are categorized into different families that are optimized for specific purposes. For more information, see [VM SKUs](/en-us/azure/virtual-machines/sizes/overview).

To enable scaling of multiple virtual machine sizes, the Virtual Machines node pool type uses a `ScaleProfile`

that contains configurations indicating how the node pool can scale, specifically the desired list of virtual machine size and the count of each size. A `ManualScaleProfile`

is a scale profile that specifies one desired virtual machine size and the total count of that type in the nodepool. Only one virtual machine size is allowed in a `ManualScaleProfile`

. You need to create a separate `ManualScaleProfile`

for each virtual machine size in your node pool. When creating a new Virtual Machines node pool, you add an initial manual scale profile for a virtual machine size using the `vm-size`

field and including a `node-count`

, per the instructions below. You can also add additional manual scale profiles following the instructions for [adding manual scale profiles](/en-us/azure/aks/virtual-machines-node-pools#add-a-manual-scale-profile-to-a-node-pool).

Note

When creating a new Virtual Machines node pool, you can have multiple scale profiles, and you need at least one manual scale profile in your nodepool.

### Advantages

Advantages of the Virtual Machines node pool type include:

**Flexibility**: Node specifications can be updated to adapt to your current workload and needs.**Fine-tuned control**: Single node-level controls allow specifying and mixing nodes of different specs to lift restrictions from a single model and improve consistency.**Efficiency**: You can reduce the node footprint for your cluster, simplifying your operational requirements.

Virtual Machines node pools provide a better experience for dynamic workloads and high availability requirements. Virtual Machines node pools enable you to set up multiple similar-family virtual machines in one node pool. Your workload will be automatically scheduled on the available resources that you configure.

### Feature comparison

The following table highlights how Virtual Machines node pools compare with standard [Scale Set](/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-orchestration-modes) node pools.

| Node pool type | Capabilities |
|---|---|
| Virtual Machines node pool | You can add, remove, or update nodes in a node pool. Virtual machine types can be any virtual machine of the same family type (for example, D-series, A-Series, etc.). |
| Virtual Machine Scale Set based node pool | You can add or remove nodes of the same size and type in a node pool. If you add a new virtual machine size to the cluster, you need to create a new node pool. |

### Limitations

[Cluster autoscaler](cluster-autoscaler-overview)is currently not supported.[InifiniBand](/en-us/azure/virtual-machines/extensions/enable-infiniband)isn't available.[Node pool snapshot](node-pool-snapshot)isn't supported.- All VM sizes selected in a node pool need to be from a similar virtual machine family. For example, you can't mix an N-Series virtual machine type with a D-Series virtual machine type in the same node pool.
- Virtual Machines node pools allow up to five different virtual machine sizes per node pool.

## Prerequisites

- An Azure subscription. If you don't have one, you can
[create a free account](https://azure.microsoft.com/free). - Azure CLI version 2.73.0 or later installed and configured. To find the version, run
`az --version`

. For more information about installing or upgrading the Azure CLI, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli#install-azure-cli) - This feature requires kubernetes version 1.27 or greater. To upgrade your kubernetes version, see
[Upgrade AKS cluster](upgrade-aks-cluster)

## Create an AKS cluster with Virtual Machines node pools

Note

Only *one* VM size is allowed in a scale profile, and the maximum limit is *five* VM scale profiles overall for a Virtual Machines node pool.

Create an AKS cluster with Virtual Machines node pools using the

command with the`az aks create`

`--vm-set-type`

flag set to`"VirtualMachines"`

.The following example creates a cluster named

*myAKSCluster*with a Virtual Machines node pool containing two nodes, generates SSH keys, sets the load balancer SKU to*standard*, and sets the Kubernetes version to*1.31.0*:`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --vm-set-type "VirtualMachines" \ --vm-sizes "Standard_D4s_v3" --node-count 2 \ --kubernetes-version 1.31.0`


## Create a cluster with Windows enabled and a Windows Virtual Machine node pool

Virtual Machine node pools are available in Windows enabled clusters. The following example creates a cluster named *myAKSCluster* with a Virtual Machines node pool. These steps create a Linux system pool at first.

Create a username to use as administrator credentials for the Windows Server nodes on your cluster. The following commands prompt you for a username and sets it to

*WINDOWS_USERNAME*for use in a later command.`echo "Please enter the username to use as administrator credentials for Windows Server nodes on your cluster: " && read WINDOWS_USERNAME`

Create a password for the administrator username you created in the previous step. The password must be a minimum of 14 characters and meet the

[Windows Server password complexity requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference).`echo "Please enter the password to use as administrator credentials for Windows Server nodes on your cluster: " && read WINDOWS_PASSWORD`

Create an AKS cluster with Windows enabled and Virtual Machines type node pools using the

command with the`az aks create`

`--vm-set-type`

flag set to`"VirtualMachines"`

.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 2 \ --enable-addons monitoring \ --generate-ssh-keys \ --windows-admin-username $WINDOWS_USERNAME \ --windows-admin-password $WINDOWS_PASSWORD \ --vm-set-type "VirtualMachines" \ --network-plugin azure`

Add a Virtual Machines node pool to an existing Windows enabled cluster using the

command with the`az aks nodepool add`

`--vm-set-type`

flag set to`"VirtualMachines"`

. The following example adds a Virtual Machines node pool named*npwin*to the*myAKSCluster*cluster:`az aks nodepool add --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --os-type Windows \ --name npwin \ --vm-sizes "Standard_D2s_V3" \ --node-count 1 --vm-set-type "VirtualMachines"`


## Add a Virtual Machines node pool to an existing cluster

Add a Virtual Machines node pool to an existing cluster using the

command with the`az aks nodepool add`

`--vm-set-type`

flag set to`"VirtualMachines"`

.The following example adds a Virtual Machines node pool named

*myvmpool*to the*myAKSCluster*cluster. The node pool creates a ManualScaleProfile with`--vm-sizes`

set to*Standard_D4s_v3*and a`--node-count`

of 3:`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myvmpool \ --vm-set-type "VirtualMachines" \ --vm-sizes "Standard_D4s_v3" \ --node-count 3`


## Add a manual scale profile to a node pool

Add a manual scale profile to a node pool using the

with the`az aks nodepool manual-scale add`

`--vm-sizes`

flag set to`"Standard_D2s_v3"`

and the`node-count`

set to 2.The following example adds a manual scale profile to node pool

*myvmpool*in cluster*myAKSCluster*. The node pool includes two nodes with a VM SKU of*Standard_D2s_v3*:`az aks nodepool manual-scale add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myvmpool \ --vm-sizes "Standard_D2s_v3" \ --node-count 2`


## Update an existing manual scale profile

Update an existing manual scale profile in a node pool using the

command with the`az aks nodepool manual-scale update`

`--vm-sizes`

flag set to`"Standard_D2s_v3"`

.Note

Use the

`--current-vm-sizes`

parameter to specify the size of the existing node pool that you want to update. You can update`--vm-sizes`

and/or`--node-count`

. When using other tools or REST APIs, you need to pass in a full`agentPoolProfiles.virtualMachinesProfile.scale`

field when updating the node pool scale profile.The following example updates a manual scale profile to the

*myvmpool*node pool in the*myAKSCluster*cluster. The command updates the number of nodes to five and changes the VM SKU from*Standard_D4s_v3*to*Standard_D8s_v3*:`az aks nodepool manual-scale update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myvmpool \ --current-vm-sizes "Standard_D4s_v3" \ --vm-sizes "Standard_D8s_v3" \ --node-count 5`


## Delete a manual scale profile

Delete an existing manual scale profile using the

command.`az aks nodepool manual-scale delete`

Note

The

`--current-vm-sizes`

parameter specifies the size of the existing node pool to be deleted. When using other tools or REST APIs to update the node pool scale profile, pass in a full`agentPoolProfiles.virtualMachinesProfile.scale`

field.The following example deletes the manual scale profile for the

*Standard_D8s_v3*VM SKU in the*myvmpool*node pool.`az aks nodepool manual-scale delete \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myvmpool \ --current-vm-sizes "Standard_D8s_v3"`


## Next steps

In this article, you learned how to use Virtual Machines node pools in AKS. To learn more about node pools in AKS, see [Create node pools](create-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/monitor-aks-reference -->

# Azure Kubernetes Service monitoring data reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article contains all the monitoring reference information for this service.

See [Monitor Azure Kubernetes Service (AKS)](monitor-aks) for details on the data you can collect for AKS and how to use it.

## Metrics

This section lists all the automatically collected platform metrics for this service. These metrics are also part of the global list of [all platform metrics supported in Azure Monitor](/en-us/azure/azure-monitor/reference/supported-metrics/metrics-index#supported-metrics-per-resource-type).

For information on metric retention, see [Azure Monitor Metrics overview](/en-us/azure/azure-monitor/essentials/data-platform-metrics#retention-of-metrics).

### Supported metrics for Microsoft.ContainerService/managedClusters

The following table lists the metrics available for the Microsoft.ContainerService/managedClusters resource type.

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

### Category: API Server

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
API Server CPU Usage PercentageMaximum CPU percentage (based off current limit) used by API server pod across instances |
`apiserver_cpu_usage_percentage` |
Percent | Maximum, Average | <none> | PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
API Server Memory Usage PercentageMaximum memory percentage (based off current limit) used by API server pod across instances |
`apiserver_memory_usage_percentage` |
Percent | Maximum, Average | <none> | PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |

### Category: API Server (PREVIEW)

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Inflight RequestsMaximum number of currently used inflight requests on the apiserver per request kind in the last second |
`apiserver_current_inflight_requests` |
Count | Total (Sum), Average | `requestKind` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |

### Category: Cluster Autoscaler (PREVIEW)

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Cluster HealthDetermines whether or not cluster autoscaler will take action on the cluster |
`cluster_autoscaler_cluster_safe_to_autoscale` |
Count | Total (Sum), Average | <none> | PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Scale Down CooldownDetermines if the scale down is in cooldown - No nodes will be removed during this timeframe |
`cluster_autoscaler_scale_down_in_cooldown` |
Count | Total (Sum), Average | <none> | PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Unneeded NodesCluster auotscaler marks those nodes as candidates for deletion and are eventually deleted |
`cluster_autoscaler_unneeded_nodes_count` |
Count | Total (Sum), Average | <none> | PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Unschedulable PodsNumber of pods that are currently unschedulable in the cluster |
`cluster_autoscaler_unschedulable_pods_count` |
Count | Total (Sum), Average | <none> | PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |

### Category: ETCD

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
ETCD CPU Usage PercentageMaximum CPU percentage (based off current limit) used by ETCD pod across instances |
`etcd_cpu_usage_percentage` |
Percent | Maximum, Average | <none> | PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
ETCD Database Usage PercentageMaximum utilization of the ETCD database across instances |
`etcd_database_usage_percentage` |
Percent | Maximum, Average | <none> | PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
ETCD Memory Usage PercentageMaximum memory percentage (based off current limit) used by ETCD pod across instances |
`etcd_memory_usage_percentage` |
Percent | Maximum, Average | <none> | PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |

### Category: Nodes

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Total number of available cpu cores in a managed clusterTotal number of available cpu cores in a managed cluster |
`kube_node_status_allocatable_cpu_cores` |
Count | Total (Sum), Average | <none> | PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Total amount of available memory in a managed clusterTotal amount of available memory in a managed cluster |
`kube_node_status_allocatable_memory_bytes` |
Bytes | Total (Sum), Average | <none> | PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Statuses for various node conditionsStatuses for various node conditions |
`kube_node_status_condition` |
Count | Total (Sum), Average | `condition` , `status` , `status2` , `node` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |

### Category: Nodes (PREVIEW)

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
CPU Usage MillicoresAggregated measurement of CPU utilization in millicores across the cluster |
`node_cpu_usage_millicores` |
MilliCores | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
CPU Usage PercentageAggregated average CPU utilization measured in percentage across the cluster |
`node_cpu_usage_percentage` |
Percent | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Disk Used BytesDisk space used in bytes by device |
`node_disk_usage_bytes` |
Bytes | Maximum, Average | `node` , `nodepool` , `device` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Disk Used PercentageDisk space used in percent by device |
`node_disk_usage_percentage` |
Percent | Maximum, Average | `node` , `nodepool` , `device` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Memory RSS BytesContainer RSS memory used in bytes |
`node_memory_rss_bytes` |
Bytes | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Memory RSS PercentageContainer RSS memory used in percent |
`node_memory_rss_percentage` |
Percent | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Memory Working Set BytesContainer working set memory used in bytes |
`node_memory_working_set_bytes` |
Bytes | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Memory Working Set PercentageContainer working set memory used in percent |
`node_memory_working_set_percentage` |
Percent | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Network In BytesNetwork received bytes |
`node_network_in_bytes` |
Bytes | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Network Out BytesNetwork transmitted bytes |
`node_network_out_bytes` |
Bytes | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |

### Category: Pods

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Number of pods by phaseNumber of pods by phase |
`kube_pod_status_phase` |
Count | Total (Sum), Average | `phase` , `namespace` , `pod` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Number of pods in Ready stateNumber of pods in Ready state |
`kube_pod_status_ready` |
Count | Total (Sum), Average | `namespace` , `pod` , `condition` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |

### Supported metrics for microsoft.kubernetes/connectedClusters

The following table lists the metrics available for the microsoft.kubernetes/connectedClusters resource type.

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

### Category: Availability

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Total number of cpu cores in a connected clusterTotal number of cpu cores in a connected cluster |
`capacity_cpu_cores` |
Count | Total (Sum), Average | <none> | PT1M | Yes |

### Category: Nodes (PREVIEW)

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
CPU Usage PercentageAggregated average CPU utilization measured in percentage across the cluster |
`node_cpu_usage_percentage` |
Percent | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Disk Used PercentageDisk space used in percent by device |
`node_disk_usage_percentage` |
Percent | Maximum, Average | `node` , `nodepool` , `device` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Memory RSS PercentageContainer RSS memory used in percent |
`node_memory_rss_percentage` |
Percent | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Memory Working Set PercentageContainer working set memory used in percent |
`node_memory_working_set_percentage` |
Percent | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |

### Supported metrics for microsoft.kubernetesconfiguration/extensions

The following table lists the metrics available for the microsoft.kubernetesconfiguration/extensions resource type.

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

### Category: Latency

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Api Request Duration in SecondsHistogram of request durations |
`ApiRequestDurationSeconds` |
Seconds | Average | `AppName` , `GpuEnabled` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Ingestion TimeTotal ingestion time in minutes |
`IngestionTimeMinutes` |
Seconds | Average | `AppName` , `GpuEnabled` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Input Preprocessing Time (Milliseconds)Input preprocessing time in milliseconds |
`InputPreprocessingTimeMilliseconds` |
Milliseconds | Average | `GpuEnabled` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Call LLM Total Time in SecondsTotal call_llm time in seconds |
`TotalCallLLMTimeSeconds` |
Seconds | Average | `AppName` , `GpuEnabled` , `LLMProvider` , `OutputLength` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Embedding Generation Total Time in SecondsTotal time taken to generate embeddings from local model |
`TotalGenerateEmbeddingsTimeSeconds` |
Seconds | Average | `AppName` , `GpuEnabled` , `InputLength` , `OutputLength` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Hybrid Search Embedding Generation Total Time in SecondsTotal time taken to generate Hybrid Search embeddings from local model |
`TotalGenerateHybridSearchEmbeddingsTimeSeconds` |
Seconds | Average | `AppName` , `GpuEnabled` , `InputLength` , `OutputLength` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Reranking Generation Total Time in SecondsTotal time taken to generate Reranking |
`TotalGenerateRerankingTimeSeconds` |
Seconds | Average | `AppName` , `GpuEnabled` , `InputLength` , `OutputLength` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Get Chat History Summary Total Time in MillisecondsTotal get_chat_history_summary time in milliseconds |
`TotalGetChatHistorySummaryTimeMilliseconds` |
Milliseconds | Average | `AppName` , `GpuEnabled` , `InputHistoryPairs` , `LLMProvider` , `MaxTokens` , `OutputLength` , `Temperature` , `TopP` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Get LLM Payload Total Time in MillisecondsTotal get_llm_payload time in milliseconds |
`TotalGetLLMPayloadTimeMilliseconds` |
Milliseconds | Average | `AppName` , `DiversityPenalty` , `GpuEnabled` , `LengthPenalty` , `LLMProvider` , `MaxTokens` , `RepetitionPenalty` , `Temperature` , `TopP` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Get Hybrid Search Total Time in MillisecondsTotal hybrid search time in milliseconds |
`TotalHybridSearchTimeMilliseconds` |
Milliseconds | Average | `AppName` , `ChunkMinScore` , `GpuEnabled` , `IndexType` , `InputLength` , `MetricType` , `TopK` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Inference Total Time in SecondsTotal inference time in seconds |
`TotalInferenceTimeSeconds` |
Seconds | Average | `AppName` , `DiversityPenalty` , `GpuEnabled` , `InputLength` , `LLMProvider` , `MaxTokens` , `OutputLength` , `RepetitionPenalty` , `Temperature` , `TopK` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Chunks Search Total Time in MillisecondsTotal search chunks time in milliseconds |
`TotalSearchChunksTimeMilliseconds` |
Milliseconds | Average | `AppName` , `EmbeddingIndexName` , `GpuEnabled` , `InputLength` , `OutputChunks` , `TopK` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Search Total Time in MillisecondsTotal time taken to search |
`TotalSearchTimeMilliseconds` |
Milliseconds | Average | `AppName` , `ChunkMinScore` , `GpuEnabled` , `InputLength` , `QueryType` , `TopK` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Similarity Search Total Time in MillisecondsTotal time taken to search for similar documents |
`TotalSimilaritySearchTimeMilliseconds` |
Milliseconds | Average | `AppName` , `GpuEnabled` , `InputLength` , `ChunkMinScore` , `IndexType` , `MetricType` , `TopK` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |

### Category: Traffic

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Active PDU SessionsNumber of Active PDU Sessions |
`ActiveSessionCount` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | No |
API Failure CountCount of failed API requests |
`ApiFailureCount` |
Count | Count | `EndpointName` , `GpuEnabled` , `StatusCode` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
API Request CountTotal number of API requests |
`ApiRequestCount` |
Count | Count | `AppName` , `GpuEnabled` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
API Success CountCount of successful API requests |
`ApiSuccessCount` |
Count | Count | `EndpointName` , `GpuEnabled` , `StatusCode` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Authentication AttemptsAuthentication attempts rate (per minute) |
`AuthAttempt` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Authentication FailuresAuthentication failure rate (per minute) |
`AuthFailure` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` , `Result` |
PT1M | Yes |
Authentication SuccessesAuthentication success rate (per minute) |
`AuthSuccess` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Connected NodeBsNumber of connected gNodeBs or eNodeBs |
`ConnectedNodebs` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
DeRegistration AttemptsUE deregistration attempts rate (per minute) |
`DeRegistrationAttempt` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
DeRegistration SuccessesUE deregistration success rate (per minute) |
`DeRegistrationSuccess` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Evaluation API Request CountTotal number of Evaluation API requests |
`EvaluationApiRequestCount` |
Count | Count | `AppName` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Failed Skipped CountCount of failed or skipped files |
`FailedSkippedCount` |
Count | Count | `Category` , `GpuEnabled` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
File Ingestion RateTotal files ingested per Job |
`FileIngestionRate` |
Count | Total (Sum) | `AppName` , `GpuEnabled` , `FileType` , `JobID` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Hybrid Search Model API Request CountTotal number of Hybrid Search Model API requests |
`HybridSearchModelApiRequestCount` |
Count | Count | `AppName` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Inference Answer FeedbackInference Answer Feedback |
`InferenceAnswerFeedback` |
Count | Count | `AppName` , `ChunkMinScore` , `ChunkScores` , `GpuEnabled` , `LLMProvider` , `RunId` , `Thumb` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Inference API Request CountNumber of Inference API requests |
`InferenceApiRequestCount` |
Count | Count | `AppName` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Ingestion API Request CountNumber of Ingestion API requests |
`IngestionApiRequestCount` |
Count | Count | `AppName` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Number of EvaluationsNumber of Evaluations |
`NumberOfEvaluations` |
Count | Count | `AppName` , `GpuEnabled` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Number of JobsNumber of jobs |
`NumberOfJobs` |
Count | Count | `AppName` , `GpuEnabled` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Paging AttemptsPaging attempts rate (per minute) |
`PagingAttempt` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Paging FailuresPaging failure rate (per minute) |
`PagingFailure` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Provisioned SubscribersNumber of provisioned subscribers |
`ProvisionedSubscribers` |
Count | Total (Sum) | `PccpId` , `SiteId` |
PT1M | No |
RAN Setup FailuresRAN setup failure rate (per minute) |
`RanSetupFailure` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` , `Cause` |
PT1M | Yes |
RAN Setup RequestsRAN setup reuests rate (per minute) |
`RanSetupRequest` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
RAN Setup ResponsesRAN setup response rate (per minute) |
`RanSetupResponse` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Registered SubscribersNumber of registered subscribers |
`RegisteredSubscribers` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Registered Subscribers ConnectedNumber of registered and connected subscribers |
`RegisteredSubscribersConnected` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Registered Subscribers IdleNumber of registered and idle subscribers |
`RegisteredSubscribersIdle` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Registration AttemptsRegistration attempts rate (per minute) |
`RegistrationAttempt` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Registration FailuresRegistration failure rate (per minute) |
`RegistrationFailure` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` , `Result` |
PT1M | Yes |
Registration SuccessesRegistration success rate (per minute) |
`RegistrationSuccess` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Service Request AttemptsService request attempts rate (per minute) |
`ServiceRequestAttempt` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Service Request FailuresService request failure rate (per minute) |
`ServiceRequestFailure` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` , `Result` , `Tai` |
PT1M | Yes |
Service Request SuccessesService request success rate (per minute) |
`ServiceRequestSuccess` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Session Establishment AttemptsPDU session establishment attempts rate (per minute) |
`SessionEstablishmentAttempt` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` , `Dnn` |
PT1M | Yes |
Session Establishment FailuresPDU session establishment failure rate (per minute) |
`SessionEstablishmentFailure` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` , `Dnn` |
PT1M | Yes |
Session Establishment SuccessesPDU session establishment success rate (per minute) |
`SessionEstablishmentSuccess` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` , `Dnn` |
PT1M | Yes |
Session ReleasesSession release rate (per minute) |
`SessionRelease` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
UE Context Release CommandsUE context release command message rate (per minute) |
`UeContextReleaseCommand` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
UE Context Release CompletesUE context release complete message rate (per minute) |
`UeContextReleaseComplete` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
UE Context Release RequestsUE context release request message rate (per minute) |
`UeContextReleaseRequest` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
User Plane BandwidthUser plane bandwidth in bits/second. |
`UserPlaneBandwidth` |
BitsPerSecond | Total (Sum) | `PcdpId` , `SiteId` , `Direction` , `Interface` |
PT1M | No |
User Plane Packet Drop RateUser plane packet drop rate (packets/sec) |
`UserPlanePacketDropRate` |
CountPerSecond | Total (Sum) | `PcdpId` , `SiteId` , `Cause` , `Direction` , `Interface` |
PT1M | No |
User Plane Packet RateUser plane packet rate (packets/sec) |
`UserPlanePacketRate` |
CountPerSecond | Total (Sum) | `PcdpId` , `SiteId` , `Direction` , `Interface` |
PT1M | No |
VectorDB API Request CountTotal number of API requests to VectorDB |
`VectorDbApiRequestCount` |
Count | Count | `AppName` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Xn Handover AttemptsHandover attempts rate (per minute) |
`XnHandoverAttempt` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Xn Handover FailuresHandover failure rate (per minute) |
`XnHandoverFailure` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Xn Handover SuccessesHandover success rate (per minute) |
`XnHandoverSuccess` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |

### Supported metrics for Microsoft.Compute/virtualMachines

The following table lists the metrics available for the Microsoft.Compute/virtualMachines resource type.

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

### Category: Other

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Available Memory BytesAmount of physical memory, in bytes, immediately available for allocation to a process or for system use in the Virtual Machine |
`Available Memory Bytes` |
Bytes | Average | <none> | PT1M | Yes |
Available Memory PercentageAmount of physical memory, in percentage, immediately available for allocation to a process or for system use in the Virtual Machine |
`Available Memory Percentage` |
Percent | Average | <none> | PT1M | Yes |
CPU Credits ConsumedTotal number of credits consumed by the Virtual Machine. Only available on B-series burstable VMs |
`CPU Credits Consumed` |
Count | Average | <none> | PT1M | Yes |
CPU Credits RemainingTotal number of credits available to burst. Only available on B-series burstable VMs |
`CPU Credits Remaining` |
Count | Average | <none> | PT1M | Yes |
Data Disk Bandwidth Consumed PercentagePercentage of data disk bandwidth consumed per minute. Only available on VM series that support premium storage. |
`Data Disk Bandwidth Consumed Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
Data Disk IOPS Consumed PercentagePercentage of data disk I/Os consumed per minute. Only available on VM series that support premium storage. |
`Data Disk IOPS Consumed Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
Data Disk LatencyAverage time to complete each IO during monitoring period for Data Disk. Values are in milliseconds. |
`Data Disk Latency` |
Milliseconds | Average | `LUN` |
PT1M | Yes |
Data Disk Max Burst BandwidthMaximum bytes per second throughput Data Disk can achieve with bursting |
`Data Disk Max Burst Bandwidth` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Max Burst IOPSMaximum IOPS Data Disk can achieve with bursting |
`Data Disk Max Burst IOPS` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Queue DepthData Disk Queue Depth(or Queue Length) |
`Data Disk Queue Depth` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period |
`Data Disk Read Bytes/sec` |
BytesPerSecond | Average | `LUN` |
PT1M | Yes |
Data Disk Read Operations/SecRead IOPS from a single disk during monitoring period |
`Data Disk Read Operations/Sec` |
CountPerSecond | Average | `LUN` |
PT1M | Yes |
Data Disk Target BandwidthBaseline bytes per second throughput Data Disk can achieve without bursting |
`Data Disk Target Bandwidth` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Target IOPSBaseline IOPS Data Disk can achieve without bursting |
`Data Disk Target IOPS` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Used Burst BPS Credits PercentagePercentage of Data Disk burst bandwidth credits used so far |
`Data Disk Used Burst BPS Credits Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
Data Disk Used Burst IO Credits PercentagePercentage of Data Disk burst I/O credits used so far |
`Data Disk Used Burst IO Credits Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
Data Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period |
`Data Disk Write Bytes/sec` |
BytesPerSecond | Average | `LUN` |
PT1M | Yes |
Data Disk Write Operations/SecWrite IOPS from a single disk during monitoring period |
`Data Disk Write Operations/Sec` |
CountPerSecond | Average | `LUN` |
PT1M | Yes |
Disk Read BytesBytes read from disk during monitoring period |
`Disk Read Bytes` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Disk Read Operations/SecDisk Read IOPS |
`Disk Read Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
Disk Write BytesBytes written to disk during monitoring period |
`Disk Write Bytes` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Disk Write Operations/SecDisk Write IOPS |
`Disk Write Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
Inbound FlowsInbound Flows are number of current flows in the inbound direction (traffic going into the VM) |
`Inbound Flows` |
Count | Average | <none> | PT1M | Yes |
Inbound Flows Maximum Creation RateThe maximum creation rate of inbound flows (traffic going into the VM) |
`Inbound Flows Maximum Creation Rate` |
CountPerSecond | Average | <none> | PT1M | Yes |
Network In Billable (Deprecated)The number of billable bytes received on all network interfaces by the Virtual Machine(s) (Incoming Traffic) (Deprecated) |
`Network In` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Network In TotalThe number of bytes received on all network interfaces by the Virtual Machine(s) (Incoming Traffic) |
`Network In Total` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Network Out Billable (Deprecated)The number of billable bytes out on all network interfaces by the Virtual Machine(s) (Outgoing Traffic) (Deprecated) |
`Network Out` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Network Out TotalThe number of bytes out on all network interfaces by the Virtual Machine(s) (Outgoing Traffic) |
`Network Out Total` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
OS Disk Bandwidth Consumed PercentagePercentage of operating system disk bandwidth consumed per minute. Only available on VM series that support premium storage. |
`OS Disk Bandwidth Consumed Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
OS Disk IOPS Consumed PercentagePercentage of operating system disk I/Os consumed per minute. Only available on VM series that support premium storage. |
`OS Disk IOPS Consumed Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
OS Disk LatencyAverage time to complete each IO during monitoring period for OS Disk. Values are in milliseconds. |
`OS Disk Latency` |
Milliseconds | Average | <none> | PT1M | Yes |
OS Disk Max Burst BandwidthMaximum bytes per second throughput OS Disk can achieve with bursting |
`OS Disk Max Burst Bandwidth` |
Count | Average | `LUN` |
PT1M | Yes |
OS Disk Max Burst IOPSMaximum IOPS OS Disk can achieve with bursting |
`OS Disk Max Burst IOPS` |
Count | Average | `LUN` |
PT1M | Yes |
OS Disk Queue DepthOS Disk Queue Depth(or Queue Length) |
`OS Disk Queue Depth` |
Count | Average | <none> | PT1M | Yes |
OS Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period for OS disk |
`OS Disk Read Bytes/sec` |
BytesPerSecond | Average | <none> | PT1M | Yes |
OS Disk Read Operations/SecRead IOPS from a single disk during monitoring period for OS disk |
`OS Disk Read Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
OS Disk Target BandwidthBaseline bytes per second throughput OS Disk can achieve without bursting |
`OS Disk Target Bandwidth` |
Count | Average | `LUN` |
PT1M | Yes |
OS Disk Target IOPSBaseline IOPS OS Disk can achieve without bursting |
`OS Disk Target IOPS` |
Count | Average | `LUN` |
PT1M | Yes |
OS Disk Used Burst BPS Credits PercentagePercentage of OS Disk burst bandwidth credits used so far |
`OS Disk Used Burst BPS Credits Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
OS Disk Used Burst IO Credits PercentagePercentage of OS Disk burst I/O credits used so far |
`OS Disk Used Burst IO Credits Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
OS Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period for OS disk |
`OS Disk Write Bytes/sec` |
BytesPerSecond | Average | <none> | PT1M | Yes |
OS Disk Write Operations/SecWrite IOPS from a single disk during monitoring period for OS disk |
`OS Disk Write Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
Outbound FlowsOutbound Flows are number of current flows in the outbound direction (traffic going out of the VM) |
`Outbound Flows` |
Count | Average | <none> | PT1M | Yes |
Outbound Flows Maximum Creation RateThe maximum creation rate of outbound flows (traffic going out of the VM) |
`Outbound Flows Maximum Creation Rate` |
CountPerSecond | Average | <none> | PT1M | Yes |
Percentage CPUThe percentage of allocated compute units that are currently in use by the Virtual Machine(s) |
`Percentage CPU` |
Percent | Average | <none> | PT1M | Yes |
Premium Data Disk Cache Read HitPremium Data Disk Cache Read Hit |
`Premium Data Disk Cache Read Hit` |
Percent | Average | `LUN` |
PT1M | Yes |
Premium Data Disk Cache Read MissPremium Data Disk Cache Read Miss |
`Premium Data Disk Cache Read Miss` |
Percent | Average | `LUN` |
PT1M | Yes |
Premium OS Disk Cache Read HitPremium OS Disk Cache Read Hit |
`Premium OS Disk Cache Read Hit` |
Percent | Average | <none> | PT1M | Yes |
Premium OS Disk Cache Read MissPremium OS Disk Cache Read Miss |
`Premium OS Disk Cache Read Miss` |
Percent | Average | <none> | PT1M | Yes |
Temp Disk Latency (Preview)Average time to complete each IO during monitoring period for Temp Disk. Values are in milliseconds. |
`Temp Disk Latency` |
Milliseconds | Average | <none> | PT1M | Yes |
Temp Disk Queue DepthTemp Disk Queue Depth(or Queue Length). |
`Temp Disk Queue Depth` |
Count | Average | <none> | PT1M | Yes |
Temp Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period for Temp Disk. |
`Temp Disk Read Bytes/sec` |
BytesPerSecond | Average | <none> | PT1M | Yes |
Temp Disk Read Operations/SecRead IOPS from a single disk during monitoring period for Temp Disk. |
`Temp Disk Read Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
Temp Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period for Temp Disk. |
`Temp Disk Write Bytes/sec` |
BytesPerSecond | Average | <none> | PT1M | Yes |
Temp Disk Write Operations/SecWrite IOPS from a single disk during monitoring period for Temp Disk. |
`Temp Disk Write Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
VM Cached Bandwidth Consumed PercentagePercentage of cached disk bandwidth consumed by the VM. Only available on VM series that support premium storage. |
`VM Cached Bandwidth Consumed Percentage` |
Percent | Average | <none> | PT1M | Yes |
VM Cached IOPS Consumed PercentagePercentage of cached disk IOPS consumed by the VM. Only available on VM series that support premium storage. |
`VM Cached IOPS Consumed Percentage` |
Percent | Average | <none> | PT1M | Yes |
VM Cached Used Burst BPS Credits PercentagePercentage of Cached Burst BPS Credits used by the VM. |
`VM Local Used Burst BPS Credits Percentage` |
Percent | Average, Minimum, Maximum | <none> | PT1M | Yes |
VM Cached Used Burst IO Credits PercentagePercentage of Cached Burst IO Credits used by the VM. |
`VM Local Used Burst IO Credits Percentage` |
Percent | Average, Minimum, Maximum | <none> | PT1M | Yes |
VM Uncached Used Burst BPS Credits PercentagePercentage of Uncached Burst BPS Credits used by the VM. |
`VM Remote Used Burst BPS Credits Percentage` |
Percent | Average, Minimum, Maximum | <none> | PT1M | Yes |
VM Uncached Used Burst IO Credits PercentagePercentage of Uncached Burst IO Credits used by the VM. |
`VM Remote Used Burst IO Credits Percentage` |
Percent | Average, Minimum, Maximum | <none> | PT1M | Yes |
VM Uncached Bandwidth Consumed PercentagePercentage of uncached disk bandwidth consumed by the VM. Only available on VM series that support premium storage. |
`VM Uncached Bandwidth Consumed Percentage` |
Percent | Average | <none> | PT1M | Yes |
VM Uncached IOPS Consumed PercentagePercentage of uncached disk IOPS consumed by the VM. Only available on VM series that support premium storage. |
`VM Uncached IOPS Consumed Percentage` |
Percent | Average | <none> | PT1M | Yes |
VM Availability Metric (Preview)Measure of Availability of Virtual machines over time. |
`VmAvailabilityMetric` |
Count | Average, Minimum, Maximum | `Context` |
PT1M | Yes |

### Supported metrics for Microsoft.Compute/virtualmachineScaleSets

The following table lists the metrics available for the Microsoft.Compute/virtualmachineScaleSets resource type.

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Available Memory BytesAmount of physical memory, in bytes, immediately available for allocation to a process or for system use in the Virtual Machine |
`Available Memory Bytes` |
Bytes | Average | `VMName` |
PT1M | Yes |
Available Memory PercentageAmount of physical memory, in percentage, immediately available for allocation to a process or for system use in the Virtual Machine |
`Available Memory Percentage` |
Percent | Average | `VMName` |
PT1M | Yes |
CPU Credits ConsumedTotal number of credits consumed by the Virtual Machine. Only available on B-series burstable VMs |
`CPU Credits Consumed` |
Count | Average | `VMName` |
PT1M | Yes |
CPU Credits RemainingTotal number of credits available to burst. Only available on B-series burstable VMs |
`CPU Credits Remaining` |
Count | Average | `VMName` |
PT1M | Yes |
Data Disk Bandwidth Consumed PercentagePercentage of data disk bandwidth consumed per minute. Only available on VM series that support premium storage. |
`Data Disk Bandwidth Consumed Percentage` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk IOPS Consumed PercentagePercentage of data disk I/Os consumed per minute. Only available on VM series that support premium storage. |
`Data Disk IOPS Consumed Percentage` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk LatencyAverage time to complete each IO during monitoring period for Data Disk. Values are in milliseconds. |
`Data Disk Latency` |
Milliseconds | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Max Burst BandwidthMaximum bytes per second throughput Data Disk can achieve with bursting |
`Data Disk Max Burst Bandwidth` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Max Burst IOPSMaximum IOPS Data Disk can achieve with bursting |
`Data Disk Max Burst IOPS` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Queue DepthData Disk Queue Depth(or Queue Length) |
`Data Disk Queue Depth` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period |
`Data Disk Read Bytes/sec` |
BytesPerSecond | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Read Operations/SecRead IOPS from a single disk during monitoring period |
`Data Disk Read Operations/Sec` |
CountPerSecond | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Target BandwidthBaseline bytes per second throughput Data Disk can achieve without bursting |
`Data Disk Target Bandwidth` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Target IOPSBaseline IOPS Data Disk can achieve without bursting |
`Data Disk Target IOPS` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Used Burst BPS Credits PercentagePercentage of Data Disk burst bandwidth credits used so far |
`Data Disk Used Burst BPS Credits Percentage` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Used Burst IO Credits PercentagePercentage of Data Disk burst I/O credits used so far |
`Data Disk Used Burst IO Credits Percentage` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period |
`Data Disk Write Bytes/sec` |
BytesPerSecond | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Write Operations/SecWrite IOPS from a single disk during monitoring period |
`Data Disk Write Operations/Sec` |
CountPerSecond | Average | `LUN` , `VMName` |
PT1M | Yes |
Disk Read BytesBytes read from disk during monitoring period |
`Disk Read Bytes` |
Bytes | Total (Sum) | `VMName` |
PT1M | Yes |
Disk Read Operations/SecDisk Read IOPS |
`Disk Read Operations/Sec` |
CountPerSecond | Average | `VMName` |
PT1M | Yes |
Disk Write BytesBytes written to disk during monitoring period |
`Disk Write Bytes` |
Bytes | Total (Sum) | `VMName` |
PT1M | Yes |
Disk Write Operations/SecDisk Write IOPS |
`Disk Write Operations/Sec` |
CountPerSecond | Average | `VMName` |
PT1M | Yes |
Inbound FlowsInbound Flows are number of current flows in the inbound direction (traffic going into the VM) |
`Inbound Flows` |
Count | Average | `VMName` |
PT1M | Yes |
Inbound Flows Maximum Creation RateThe maximum creation rate of inbound flows (traffic going into the VM) |
`Inbound Flows Maximum Creation Rate` |
CountPerSecond | Average | `VMName` |
PT1M | Yes |
Network In Billable (Deprecated)The number of billable bytes received on all network interfaces by the Virtual Machine(s) (Incoming Traffic) (Deprecated) |
`Network In` |
Bytes | Total (Sum) | `VMName` |
PT1M | Yes |
Network In TotalThe number of bytes received on all network interfaces by the Virtual Machine(s) (Incoming Traffic) |
`Network In Total` |
Bytes | Total (Sum) | `VMName` |
PT1M | Yes |
Network Out Billable (Deprecated)The number of billable bytes out on all network interfaces by the Virtual Machine(s) (Outgoing Traffic) (Deprecated) |
`Network Out` |
Bytes | Total (Sum) | `VMName` |
PT1M | Yes |
Network Out TotalThe number of bytes out on all network interfaces by the Virtual Machine(s) (Outgoing Traffic) |
`Network Out Total` |
Bytes | Total (Sum) | `VMName` |
PT1M | Yes |
OS Disk Bandwidth Consumed PercentagePercentage of operating system disk bandwidth consumed per minute. Only available on VM series that support premium storage. |
`OS Disk Bandwidth Consumed Percentage` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
OS Disk IOPS Consumed PercentagePercentage of operating system disk I/Os consumed per minute. Only available on VM series that support premium storage. |
`OS Disk IOPS Consumed Percentage` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
OS Disk LatencyAverage time to complete each IO during monitoring period for OS Disk. Values are in milliseconds. |
`OS Disk Latency` |
Milliseconds | Average | `VMName` |
PT1M | Yes |
OS Disk Max Burst BandwidthMaximum bytes per second throughput OS Disk can achieve with bursting |
`OS Disk Max Burst Bandwidth` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
OS Disk Max Burst IOPSMaximum IOPS OS Disk can achieve with bursting |
`OS Disk Max Burst IOPS` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
OS Disk Queue DepthOS Disk Queue Depth(or Queue Length) |
`OS Disk Queue Depth` |
Count | Average | `VMName` |
PT1M | Yes |
OS Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period for OS disk |
`OS Disk Read Bytes/sec` |
BytesPerSecond | Average | `VMName` |
PT1M | Yes |
OS Disk Read Operations/SecRead IOPS from a single disk during monitoring period for OS disk |
`OS Disk Read Operations/Sec` |
CountPerSecond | Average | `VMName` |
PT1M | Yes |
OS Disk Target BandwidthBaseline bytes per second throughput OS Disk can achieve without bursting |
`OS Disk Target Bandwidth` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
OS Disk Target IOPSBaseline IOPS OS Disk can achieve without bursting |
`OS Disk Target IOPS` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
OS Disk Used Burst BPS Credits PercentagePercentage of OS Disk burst bandwidth credits used so far |
`OS Disk Used Burst BPS Credits Percentage` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
OS Disk Used Burst IO Credits PercentagePercentage of OS Disk burst I/O credits used so far |
`OS Disk Used Burst IO Credits Percentage` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
OS Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period for OS disk |
`OS Disk Write Bytes/sec` |
BytesPerSecond | Average | `VMName` |
PT1M | Yes |
OS Disk Write Operations/SecWrite IOPS from a single disk during monitoring period for OS disk |
`OS Disk Write Operations/Sec` |
CountPerSecond | Average | `VMName` |
PT1M | Yes |
Outbound FlowsOutbound Flows are number of current flows in the outbound direction (traffic going out of the VM) |
`Outbound Flows` |
Count | Average | `VMName` |
PT1M | Yes |
Outbound Flows Maximum Creation RateThe maximum creation rate of outbound flows (traffic going out of the VM) |
`Outbound Flows Maximum Creation Rate` |
CountPerSecond | Average | `VMName` |
PT1M | Yes |
Percentage CPUThe percentage of allocated compute units that are currently in use by the Virtual Machine(s) |
`Percentage CPU` |
Percent | Average | `VMName` |
PT1M | Yes |
Premium Data Disk Cache Read HitPremium Data Disk Cache Read Hit |
`Premium Data Disk Cache Read Hit` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
Premium Data Disk Cache Read MissPremium Data Disk Cache Read Miss |
`Premium Data Disk Cache Read Miss` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
Premium OS Disk Cache Read HitPremium OS Disk Cache Read Hit |
`Premium OS Disk Cache Read Hit` |
Percent | Average | `VMName` |
PT1M | Yes |
Premium OS Disk Cache Read MissPremium OS Disk Cache Read Miss |
`Premium OS Disk Cache Read Miss` |
Percent | Average | `VMName` |
PT1M | Yes |
Temp Disk Latency (Preview)Average time to complete each IO during monitoring period for Temp Disk. Values are in milliseconds. |
`Temp Disk Latency` |
Milliseconds | Average | `VMName` |
PT1M | Yes |
Temp Disk Queue DepthTemp Disk Queue Depth(or Queue Length). |
`Temp Disk Queue Depth` |
Count | Average | `VMName` |
PT1M | Yes |
Temp Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period for Temp Disk. |
`Temp Disk Read Bytes/sec` |
BytesPerSecond | Average | `VMName` |
PT1M | Yes |
Temp Disk Read Operations/SecRead IOPS from a single disk during monitoring period for Temp Disk. |
`Temp Disk Read Operations/Sec` |
CountPerSecond | Average | `VMName` |
PT1M | Yes |
Temp Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period for Temp Disk. |
`Temp Disk Write Bytes/sec` |
BytesPerSecond | Average | `VMName` |
PT1M | Yes |
Temp Disk Write Operations/SecWrite IOPS from a single disk during monitoring period for Temp Disk. |
`Temp Disk Write Operations/Sec` |
CountPerSecond | Average | `VMName` |
PT1M | Yes |
VM Cached Bandwidth Consumed PercentagePercentage of cached disk bandwidth consumed by the VM. Only available on VM series that support premium storage. |
`VM Cached Bandwidth Consumed Percentage` |
Percent | Average | `VMName` |
PT1M | Yes |
VM Cached IOPS Consumed PercentagePercentage of cached disk IOPS consumed by the VM. Only available on VM series that support premium storage. |
`VM Cached IOPS Consumed Percentage` |
Percent | Average | `VMName` |
PT1M | Yes |
VM Cached Used Burst BPS Credits PercentagePercentage of Cached Burst BPS Credits used by the VM. |
`VM Local Used Burst BPS Credits Percentage` |
Percent | Average, Minimum, Maximum | `VMName` |
PT1M | Yes |
VM Cached Used Burst IO Credits PercentagePercentage of Cached Burst IO Credits used by the VM. |
`VM Local Used Burst IO Credits Percentage` |
Percent | Average, Minimum, Maximum | `VMName` |
PT1M | Yes |
VM Uncached Used Burst BPS Credits PercentagePercentage of Uncached Burst BPS Credits used by the VM. |
`VM Remote Used Burst BPS Credits Percentage` |
Percent | Average, Minimum, Maximum | `VMName` |
PT1M | Yes |
VM Uncached Used Burst IO Credits PercentagePercentage of Uncached Burst IO Credits used by the VM. |
`VM Remote Used Burst IO Credits Percentage` |
Percent | Average, Minimum, Maximum | `VMName` |
PT1M | Yes |
VM Uncached Bandwidth Consumed PercentagePercentage of uncached disk bandwidth consumed by the VM. Only available on VM series that support premium storage. |
`VM Uncached Bandwidth Consumed Percentage` |
Percent | Average | `VMName` |
PT1M | Yes |
VM Uncached IOPS Consumed PercentagePercentage of uncached disk IOPS consumed by the VM. Only available on VM series that support premium storage. |
`VM Uncached IOPS Consumed Percentage` |
Percent | Average | `VMName` |
PT1M | Yes |
VM Availability Metric (Preview)Measure of Availability of Virtual machines over time. |
`VmAvailabilityMetric` |
Count | Average, Minimum, Maximum | `VMName` , `Context` |
PT1M | Yes |

### Supported metrics for Microsoft.Compute/virtualMachineScaleSets/virtualMachines

The following table lists the metrics available for the Microsoft.Compute/virtualMachineScaleSets/virtualMachines resource type.

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Available Memory BytesAmount of physical memory, in bytes, immediately available for allocation to a process or for system use in the Virtual Machine |
`Available Memory Bytes` |
Bytes | Average | <none> | PT1M | Yes |
Available Memory PercentageAmount of physical memory, in percentage, immediately available for allocation to a process or for system use in the Virtual Machine |
`Available Memory Percentage` |
Percent | Average | <none> | PT1M | Yes |
CPU Credits ConsumedTotal number of credits consumed by the Virtual Machine. Only available on B-series burstable VMs |
`CPU Credits Consumed` |
Count | Average | <none> | PT1M | Yes |
CPU Credits RemainingTotal number of credits available to burst. Only available on B-series burstable VMs |
`CPU Credits Remaining` |
Count | Average | <none> | PT1M | Yes |
Data Disk Bandwidth Consumed PercentagePercentage of data disk bandwidth consumed per minute. Only available on VM series that support premium storage. |
`Data Disk Bandwidth Consumed Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
Data Disk IOPS Consumed PercentagePercentage of data disk I/Os consumed per minute. Only available on VM series that support premium storage. |
`Data Disk IOPS Consumed Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
Data Disk LatencyAverage time to complete each IO during monitoring period for Data Disk. Values are in milliseconds. |
`Data Disk Latency` |
Milliseconds | Average | `LUN` |
PT1M | Yes |
Data Disk Max Burst BandwidthMaximum bytes per second throughput Data Disk can achieve with bursting |
`Data Disk Max Burst Bandwidth` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Max Burst IOPSMaximum IOPS Data Disk can achieve with bursting |
`Data Disk Max Burst IOPS` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Queue DepthData Disk Queue Depth(or Queue Length) |
`Data Disk Queue Depth` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period |
`Data Disk Read Bytes/sec` |
BytesPerSecond | Average | `LUN` |
PT1M | Yes |
Data Disk Read Operations/SecRead IOPS from a single disk during monitoring period |
`Data Disk Read Operations/Sec` |
CountPerSecond | Average | `LUN` |
PT1M | Yes |
Data Disk Target BandwidthBaseline bytes per second throughput Data Disk can achieve without bursting |
`Data Disk Target Bandwidth` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Target IOPSBaseline IOPS Data Disk can achieve without bursting |
`Data Disk Target IOPS` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Used Burst BPS Credits PercentagePercentage of Data Disk burst bandwidth credits used so far |
`Data Disk Used Burst BPS Credits Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
Data Disk Used Burst IO Credits PercentagePercentage of Data Disk burst I/O credits used so far |
`Data Disk Used Burst IO Credits Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
Data Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period |
`Data Disk Write Bytes/sec` |
BytesPerSecond | Average | `LUN` |
PT1M | Yes |
Data Disk Write Operations/SecWrite IOPS from a single disk during monitoring period |
`Data Disk Write Operations/Sec` |
CountPerSecond | Average | `LUN` |
PT1M | Yes |
Disk Read BytesBytes read from disk during monitoring period |
`Disk Read Bytes` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Disk Read Operations/SecDisk Read IOPS |
`Disk Read Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
Disk Write BytesBytes written to disk during monitoring period |
`Disk Write Bytes` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Disk Write Operations/SecDisk Write IOPS |
`Disk Write Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
Inbound FlowsInbound Flows are number of current flows in the inbound direction (traffic going into the VM) |
`Inbound Flows` |
Count | Average | <none> | PT1M | Yes |
Inbound Flows Maximum Creation RateThe maximum creation rate of inbound flows (traffic going into the VM) |
`Inbound Flows Maximum Creation Rate` |
CountPerSecond | Average | <none> | PT1M | Yes |
Network In Billable (Deprecated)The number of billable bytes received on all network interfaces by the Virtual Machine(s) (Incoming Traffic) (Deprecated) |
`Network In` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Network In TotalThe number of bytes received on all network interfaces by the Virtual Machine(s) (Incoming Traffic) |
`Network In Total` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Network Out Billable (Deprecated)The number of billable bytes out on all network interfaces by the Virtual Machine(s) (Outgoing Traffic) (Deprecated) |
`Network Out` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Network Out TotalThe number of bytes out on all network interfaces by the Virtual Machine(s) (Outgoing Traffic) |
`Network Out Total` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
OS Disk Bandwidth Consumed PercentagePercentage of operating system disk bandwidth consumed per minute. Only available on VM series that support premium storage. |
`OS Disk Bandwidth Consumed Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
OS Disk IOPS Consumed PercentagePercentage of operating system disk I/Os consumed per minute. Only available on VM series that support premium storage. |
`OS Disk IOPS Consumed Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
OS Disk LatencyAverage time to complete each IO during monitoring period for OS Disk. Values are in milliseconds. |
`OS Disk Latency` |
Milliseconds | Average | <none> | PT1M | Yes |
OS Disk Max Burst BandwidthMaximum bytes per second throughput OS Disk can achieve with bursting |
`OS Disk Max Burst Bandwidth` |
Count | Average | `LUN` |
PT1M | Yes |
OS Disk Max Burst IOPSMaximum IOPS OS Disk can achieve with bursting |
`OS Disk Max Burst IOPS` |
Count | Average | `LUN` |
PT1M | Yes |
OS Disk Queue DepthOS Disk Queue Depth(or Queue Length) |
`OS Disk Queue Depth` |
Count | Average | <none> | PT1M | Yes |
OS Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period for OS disk |
`OS Disk Read Bytes/sec` |
BytesPerSecond | Average | <none> | PT1M | Yes |
OS Disk Read Operations/SecRead IOPS from a single disk during monitoring period for OS disk |
`OS Disk Read Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
OS Disk Target BandwidthBaseline bytes per second throughput OS Disk can achieve without bursting |
`OS Disk Target Bandwidth` |
Count | Average | `LUN` |
PT1M | Yes |
OS Disk Target IOPSBaseline IOPS OS Disk can achieve without bursting |
`OS Disk Target IOPS` |
Count | Average | `LUN` |
PT1M | Yes |
OS Disk Used Burst BPS Credits PercentagePercentage of OS Disk burst bandwidth credits used so far |
`OS Disk Used Burst BPS Credits Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
OS Disk Used Burst IO Credits PercentagePercentage of OS Disk burst I/O credits used so far |
`OS Disk Used Burst IO Credits Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
OS Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period for OS disk |
`OS Disk Write Bytes/sec` |
BytesPerSecond | Average | <none> | PT1M | Yes |
OS Disk Write Operations/SecWrite IOPS from a single disk during monitoring period for OS disk |
`OS Disk Write Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
Outbound FlowsOutbound Flows are number of current flows in the outbound direction (traffic going out of the VM) |
`Outbound Flows` |
Count | Average | <none> | PT1M | Yes |
Outbound Flows Maximum Creation RateThe maximum creation rate of outbound flows (traffic going out of the VM) |
`Outbound Flows Maximum Creation Rate` |
CountPerSecond | Average | <none> | PT1M | Yes |
Percentage CPUThe percentage of allocated compute units that are currently in use by the Virtual Machine(s) |
`Percentage CPU` |
Percent | Average | <none> | PT1M | Yes |
Premium Data Disk Cache Read HitPremium Data Disk Cache Read Hit |
`Premium Data Disk Cache Read Hit` |
Percent | Average | `LUN` |
PT1M | Yes |
Premium Data Disk Cache Read MissPremium Data Disk Cache Read Miss |
`Premium Data Disk Cache Read Miss` |
Percent | Average | `LUN` |
PT1M | Yes |
Premium OS Disk Cache Read HitPremium OS Disk Cache Read Hit |
`Premium OS Disk Cache Read Hit` |
Percent | Average | <none> | PT1M | Yes |
Premium OS Disk Cache Read MissPremium OS Disk Cache Read Miss |
`Premium OS Disk Cache Read Miss` |
Percent | Average | <none> | PT1M | Yes |
Temp Disk Latency (Preview)Average time to complete each IO during monitoring period for Temp Disk. Values are in milliseconds. |
`Temp Disk Latency` |
Milliseconds | Average | <none> | PT1M | Yes |
Temp Disk Queue DepthTemp Disk Queue Depth(or Queue Length). |
`Temp Disk Queue Depth` |
Count | Average | <none> | PT1M | Yes |
Temp Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period for Temp Disk. |
`Temp Disk Read Bytes/sec` |
BytesPerSecond | Average | <none> | PT1M | Yes |
Temp Disk Read Operations/SecRead IOPS from a single disk during monitoring period for Temp Disk. |
`Temp Disk Read Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
Temp Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period for Temp Disk. |
`Temp Disk Write Bytes/sec` |
BytesPerSecond | Average | <none> | PT1M | Yes |
Temp Disk Write Operations/SecWrite IOPS from a single disk during monitoring period for Temp Disk. |
`Temp Disk Write Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
VM Cached Bandwidth Consumed PercentagePercentage of cached disk bandwidth consumed by the VM. Only available on VM series that support premium storage. |
`VM Cached Bandwidth Consumed Percentage` |
Percent | Average | <none> | PT1M | Yes |
VM Cached IOPS Consumed PercentagePercentage of cached disk IOPS consumed by the VM. Only available on VM series that support premium storage. |
`VM Cached IOPS Consumed Percentage` |
Percent | Average | <none> | PT1M | Yes |
VM Cached Used Burst BPS Credits PercentagePercentage of Cached Burst BPS Credits used by the VM. |
`VM Local Used Burst BPS Credits Percentage` |
Percent | Average, Minimum, Maximum | <none> | PT1M | Yes |
VM Cached Used Burst IO Credits PercentagePercentage of Cached Burst IO Credits used by the VM. |
`VM Local Used Burst IO Credits Percentage` |
Percent | Average, Minimum, Maximum | <none> | PT1M | Yes |
VM Uncached Used Burst BPS Credits PercentagePercentage of Uncached Burst BPS Credits used by the VM. |
`VM Remote Used Burst BPS Credits Percentage` |
Percent | Average, Minimum, Maximum | <none> | PT1M | Yes |
VM Uncached Used Burst IO Credits PercentagePercentage of Uncached Burst IO Credits used by the VM. |
`VM Remote Used Burst IO Credits Percentage` |
Percent | Average, Minimum, Maximum | <none> | PT1M | Yes |
VM Uncached Bandwidth Consumed PercentagePercentage of uncached disk bandwidth consumed by the VM. Only available on VM series that support premium storage. |
`VM Uncached Bandwidth Consumed Percentage` |
Percent | Average | <none> | PT1M | Yes |
VM Uncached IOPS Consumed PercentagePercentage of uncached disk IOPS consumed by the VM. Only available on VM series that support premium storage. |
`VM Uncached IOPS Consumed Percentage` |
Percent | Average | <none> | PT1M | Yes |
VM Availability Metric (Preview)Measure of Availability of Virtual machines over time. |
`VmAvailabilityMetric` |
Count | Average, Minimum, Maximum | <none> | PT1M | Yes |

## Minimal ingestion profile for control plane Metrics in Managed Prometheus

Azure Monitor metrics addon collects many Prometheus metrics by default. `Minimal ingestion profile`

is a setting that helps reduce ingestion volume of metrics, as only metrics used by default dashboards, default recording rules and default alerts are collected. This section describes how this setting is configured specifically for control plane metrics. This section also lists metrics collected by default when `minimal ingestion profile`

is enabled.

Note

For addon based collection, `Minimal ingestion profile`

setting is enabled by default. The discussion here is focused on control plane metrics. The current set of default targets and metrics is listed [here](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-configuration-minimal).

Following targets are **enabled/ON** by default - meaning you don't have to provide any scrape job configuration for scraping these targets, as metrics addon scrapes these targets automatically by default:

`controlplane-apiserver`

(job=`controlplane-apiserver`

)`controlplane-etcd`

(job=`controlplane-etcd`

)

Following targets are available to scrape, but scraping isn't enabled (**disabled/OFF**) by default. Meaning you don't have to provide any scrape job configuration for scraping these targets, and you need to turn **ON/enable** scraping for these targets using the [ama-metrics-settings-configmap](https://github.com/Azure/prometheus-collector/blob/89e865a73601c0798410016e9beb323f1ecba335/otelcollector/configmaps/ama-metrics-settings-configmap.yaml) under the `default-scrape-settings-enabled`

section.

`controlplane-cluster-autoscaler`

`controlplane-node-auto-provisioning`

`controlplane-kube-scheduler`

`controlplane-kube-controller-manager`


Note

The default scrape frequency for all default targets and scrapes is `30 seconds`

. You can override it for each target using the [ama-metrics-settings-configmap](https://github.com/Azure/prometheus-collector/blob/89e865a73601c0798410016e9beb323f1ecba335/otelcollector/configmaps/ama-metrics-settings-configmap.yaml) under `default-targets-scrape-interval-settings`

section.

### Minimal ingestion for default ON targets

The following metrics are allow-listed with `minimalingestionprofile=true`

for default **ON** targets. The below metrics are collected by default, as these targets are scraped by default.

controlplane-apiserver:

`apiserver_request_total`

`apiserver_cache_list_fetched_objects_total`

`apiserver_cache_list_returned_objects_total`

`apiserver_flowcontrol_demand_seats_average`

`apiserver_flowcontrol_current_limit_seats`

`apiserver_request_sli_duration_seconds_bucket`

`apiserver_request_sli_duration_seconds_sum`

`apiserver_request_sli_duration_seconds_count`

`process_start_time_seconds`

`apiserver_request_duration_seconds_bucket`

`apiserver_request_duration_seconds_sum`

`apiserver_request_duration_seconds_count`

`apiserver_storage_list_fetched_objects_total`

`apiserver_storage_list_returned_objects_total`

`apiserver_current_inflight_requests`


Note

`apiserver_request_sli_duration_seconds_bucket`

and `apiserver_request_duration_seconds_bucket`

are not collected now with a recent release. These are high cardinality metrics which may increase the number of metrics stored based on the number of custom resources in the cluster. If you would like to collect these bucket metrics, you can add it to the keep list. We highly recommend not turning off the minimal ingestion profile for the control plane components

controlplane-etcd:

`etcd_server_has_leader`

`rest_client_requests_total`

`etcd_mvcc_db_total_size_in_bytes`

`etcd_mvcc_db_total_size_in_use_in_bytes`

`etcd_server_slow_read_indexes_total`

`etcd_server_slow_apply_total`

`etcd_network_client_grpc_sent_bytes_total`

`etcd_server_heartbeat_send_failures_total`


### Minimal ingestion for default OFF targets

The following are metrics that are allow-listed with `minimalingestionprofile=true`

for default **OFF** targets. These metrics aren't collected by default. You can turn **ON** scraping for these targets using `default-scrape-settings-enabled.<target-name>=true`

using the [ama-metrics-settings-configmap](https://github.com/Azure/prometheus-collector/blob/89e865a73601c0798410016e9beb323f1ecba335/otelcollector/configmaps/ama-metrics-settings-configmap.yaml) under the `default-scrape-settings-enabled`

section.

controlplane-kube-controller-manager:

`workqueue_depth`

`rest_client_requests_total`

`rest_client_request_duration_seconds`


controlplane-kube-scheduler:

`scheduler_pending_pods`

`scheduler_unschedulable_pods`

`scheduler_queue_incoming_pods_total`

`scheduler_schedule_attempts_total`

`scheduler_preemption_attempts_total`


controlplane-cluster-autoscaler:

`rest_client_requests_total`

`cluster_autoscaler_last_activity`

`cluster_autoscaler_cluster_safe_to_autoscale`

`cluster_autoscaler_failed_scale_ups_total`

`cluster_autoscaler_scale_down_in_cooldown`

`cluster_autoscaler_scaled_up_nodes_total`

`cluster_autoscaler_unneeded_nodes_count`

`cluster_autoscaler_unschedulable_pods_count`

`cluster_autoscaler_nodes_count`

`cloudprovider_azure_api_request_errors`

`cloudprovider_azure_api_request_duration_seconds_bucket`

`cloudprovider_azure_api_request_duration_seconds_count`


controlplane-node-auto-provisioning:

`karpenter_pods_state`

`karpenter_nodes_created_total`

`karpenter_nodes_terminated_total`

`karpenter_nodeclaims_disrupted_total`

`karpenter_voluntary_disruption_eligible_nodes`

`karpenter_voluntary_disruption_decisions_total`


Note

The CPU and memory usage metrics for all control-plane targets are not exposed irrespective of the profile.

## Metric dimensions

For information about what metric dimensions are, see [Multi-dimensional metrics](/en-us/azure/azure-monitor/platform/data-platform-metrics#multi-dimensional-metrics).

This service has the following dimensions associated with its metrics.

| Dimension Name | Description |
|---|---|
| requestKind | Used by metrics such as Inflight Requests to split by type of request. |
| condition | Used by metrics such as Statuses for various node conditions, Number of pods in Ready state to split by condition type. |
| status | Used by metrics such as Statuses for various node conditions to split by status of the condition. |
| status2 | Used by metrics such as Statuses for various node conditions to split by status of the condition. |
| node | Used by metrics such as CPU Usage Millicores to split by the name of the node. |
| phase | Used by metrics such as Number of pods by phase to split by the phase of the pod. |
| namespace | Used by metrics such as Number of pods by phase to split by the namespace of the pod. |
| pod | Used by metrics such as Number of pods by phase to split by the name of the pod. |
| nodepool | Used by metrics such as Disk Used Bytes to split by the name of the nodepool. |
| device | Used by metrics such as Disk Used Bytes to split by the name of the device. |
| 3gppGen | Used by metrics such as Number of Active PDU Sessions. |
| Cause | Used by metrics such as User plane packet drop rate. |
| Direction | Used by metrics such as User plane bandwidth. |
| Dnn | Used by metrics such as PDU session establishment attempts rate. |
| Interface | Used by metrics such as User plane bandwidth. |
| LUN | Used by metrics such as Percentage of data disk bandwidth consumed. |
| PccpId | Used by metrics such as Number of Active PDU Sessions. |
| Result | Used by metrics such as Authentication failure rate. |
| SiteId | Used by metrics such as Number of Active PDU Sessions. |
| Tai | Used by metrics such as Service request failure rate. |
| VMName | Used by metrics such as Amount of physical memory. |

## Resource logs

This section lists the types of resource logs you can collect for this service. The section pulls from the list of [all resource logs category types supported in Azure Monitor](/en-us/azure/azure-monitor/platform/resource-logs-schema).

### Supported resource logs for Microsoft.ContainerService/fleets

| Category | Category display name | Log table |
|
|---|

[Supports ingestion-time transformation](/en-us/azure/azure-monitor/essentials/data-collection-transformations)

`cloud-controller-manager`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`fleet-hub-agent`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`fleet-hub-net-controller-manager`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`guard`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-apiserver`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-audit`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-audit-admin`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-controller-manager`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-scheduler`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)### Supported resource logs for Microsoft.ContainerService/managedClusters

| Category | Category display name | Log table |
|
|---|

[Supports ingestion-time transformation](/en-us/azure/azure-monitor/essentials/data-collection-transformations)

`cloud-controller-manager`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`cluster-autoscaler`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`csi-azuredisk-controller`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`csi-azurefile-controller`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`csi-snapshot-controller`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`fleet-mcs-controller-manager`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`fleet-member-agent`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`fleet-member-net-controller-manager`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`guard`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`karpenter-events`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-apiserver`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-audit`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-audit-admin`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-controller-manager`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-scheduler`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)### Supported resource logs for microsoft.kubernetes/connectedClusters

| Category | Category display name | Log table |
|
|---|

[Supports ingestion-time transformation](/en-us/azure/azure-monitor/essentials/data-collection-transformations)

`cloud-controller-manager`

`cluster-autoscaler`

`csi-aksarcdisk-controller`

`csi-aksarcnfs-controller`

`csi-aksarcsmb-controller`

`guard`

`kube-apiserver`

[ArcK8sControlPlane](/en-us/azure/azure-monitor/reference/tables/arck8scontrolplane)Contains diagnostic logs for the Kubernetes API Server, Controller Manager, Scheduler, Cluster Autoscaler, Cloud Controller Manager, Guard, and the Azure CSI storage drivers. These diagnostic logs have distinct Category entries corresponding their diagnostic log setting (e.g. kube-apiserver, kube-audit-admin). Requires Diagnostic Settings to use the Resource Specific destination table.

`kube-audit`

[ArcK8sAudit](/en-us/azure/azure-monitor/reference/tables/arck8saudit)Contains all Kubernetes API Server audit logs including events with the get and list verbs. These events are useful for monitoring all of the interactions with the Kubernetes API. To limit the scope to modifying operations see the ArcK8sAuditAdmin table. Requires Diagnostic Settings to use the Resource Specific destination table.

`kube-audit-admin`

[ArcK8sAuditAdmin](/en-us/azure/azure-monitor/reference/tables/arck8sauditadmin)Contains Kubernetes API Server audit logs excluding events with the get and list verbs. These events are useful for monitoring resource modification requests made to the Kubernetes API. To see all modifying and non-modifying operations see the ArcK8sAudit table. Requires Diagnostic Settings to use the Resource Specific destination table.

`kube-controller-manager`

`kube-scheduler`

### Supported resource logs for Microsoft.Compute/virtualMachines

| Category | Category display name | Log table |
|
|---|

[Supports ingestion-time transformation](/en-us/azure/azure-monitor/essentials/data-collection-transformations)

`SoftwareUpdateProfile`

`SoftwareUpdates`

## Azure Monitor Logs tables

This section lists the Azure Monitor Logs tables relevant to this service, which are available for query by Log Analytics using Kusto queries. The tables contain resource log data and possibly more depending on what is collected and routed to them.

### AKS Microsoft.ContainerService/managedClusters

[AzureActivity](/en-us/azure/azure-monitor/reference/tables/azureactivity#columns)[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics#columns)[AzureMetrics](/en-us/azure/azure-monitor/reference/tables/azuremetrics#columns)[ContainerImageInventory](/en-us/azure/azure-monitor/reference/tables/containerimageinventory#columns)[ContainerInventory](/en-us/azure/azure-monitor/reference/tables/containerinventory#columns)[ContainerLog](/en-us/azure/azure-monitor/reference/tables/containerlog#columns)[ContainerLogV2](/en-us/azure/azure-monitor/reference/tables/containerlogv2#columns)[ContainerNodeInventory](/en-us/azure/azure-monitor/reference/tables/containernodeinventory#columns)[ContainerServiceLog](/en-us/azure/azure-monitor/reference/tables/containerservicelog#columns)[Heartbeat](/en-us/azure/azure-monitor/reference/tables/heartbeat#columns)[InsightsMetrics](/en-us/azure/azure-monitor/reference/tables/insightsmetrics#columns)[KubeEvents](/en-us/azure/azure-monitor/reference/tables/kubeevents#columns)[KubeMonAgentEvents](/en-us/azure/azure-monitor/reference/tables/kubemonagentevents#columns)[KubeNodeInventory](/en-us/azure/azure-monitor/reference/tables/kubenodeinventory#columns)[KubePodInventory](/en-us/azure/azure-monitor/reference/tables/kubepodinventory#columns)[KubePVInventory](/en-us/azure/azure-monitor/reference/tables/kubepvinventory#columns)[KubeServices](/en-us/azure/azure-monitor/reference/tables/kubeservices#columns)[Perf](/en-us/azure/azure-monitor/reference/tables/perf#columns)[Syslog](/en-us/azure/azure-monitor/reference/tables/syslog#columns)[AKSAudit](/en-us/azure/azure-monitor/reference/tables/aksaudit#columns)[AKSAuditAdmin](/en-us/azure/azure-monitor/reference/tables/aksauditAdmin#columns)[AKSControlPlane](/en-us/azure/azure-monitor/reference/tables/akscontrolplane#columns)

## Activity log

The linked table lists the operations that can be recorded in the activity log for this service. These operations are a subset of [all the possible resource provider operations in the activity log](/en-us/azure/role-based-access-control/resource-provider-operations).

For more information on the schema of activity log entries, see [Activity Log schema](/en-us/azure/azure-monitor/essentials/activity-log-schema).

The following table lists a few example operations related to AKS that might be created in the Activity log. Use the Activity log to track information such as when a cluster is created or had its configuration change. You can view this information in the portal or by using [other methods](/en-us/azure/azure-monitor/essentials/activity-log#other-methods-to-retrieve-activity-log-events). You can also use it to create an Activity log alert to be proactively notified when an event occurs.

| Operation | Description |
|---|---|
| Microsoft.ContainerService/managedClusters/write | Create or update managed cluster |
| Microsoft.ContainerService/managedClusters/delete | Delete Managed Cluster |
| Microsoft.ContainerService/managedClusters/listClusterMonitoringUserCredential/action | List clusterMonitoringUser credential |
| Microsoft.ContainerService/managedClusters/listClusterAdminCredential/action | List clusterAdmin credential |
| Microsoft.ContainerService/managedClusters/agentpools/write | Create or Update Agent Pool |

## Related content

- See
[Monitor Azure Kubernetes Service](monitor-aks)for a description of monitoring AKS. - See
[Monitor Azure resources with Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource)for details on monitoring Azure resources.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/gpu-health-monitoring -->

# GPU health monitoring in Node Problem Detector (NPD) in Azure Kubernetes Service (AKS) nodes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how Azure Kubernetes Service (AKS) uses Node Problem Detector (NPD) to monitor the health of GPU-enabled node pools. NPD is a Kubernetes component that detects and reports node-level issues, including hardware faults, driver errors, and connectivity problems that can affect the performance and availability of GPU workloads.

## About GPU health monitoring in NPD

AKS supports GPU health monitoring through [Node Problem Detector (NPD)](node-problem-detector), enabling automatic detection and reporting of issues that affect GPU-enabled node pools on an AKS cluster. GPU health monitoring helps Kubernetes operators keep GPU nodes healthy and performant by surfacing hardware faults, communication failures, and system-level errors. NPD sets GPU-related node conditions and enable platform engineering teams to take action before issues impact application performance or availability.

These health signals are vital for ensuring optimal performance and reliability across a range of GPU workloads, including:

- Machine learning (ML) training and inference.
- AI model development.
- High-performance computing (HPC).
- Graphics rendering and data-intensive simulations.

## Limitations

AKS Node Problem Detector * does not* run GPU health checks on node pools with

`--gpu-driver none`

, where **self-managed**or custom GPU driver was installed on the nodes.

## Supported GPU health checks

NPD regularly monitors GPU-enabled node pools and sets conditions when anomalies are detected. The following GPU health checks are currently supported:

**GPUMissing**: NPD verifies that the number of GPUs detected by the`nvidia-smi`

utility matches the expected GPU count for the VM SKU assigned to the node.- A mismatch might indicate a hardware fault, driver issue, or misconfiguration. Accurate GPU enumeration is critical for ensuring scheduling accuracy and workload availability on GPU nodes.

**GPUXIDErrors**: Checks for XID (eXecution ID) errors emitted by the GPU driver in the kernel logs. XID errors are low-level GPU faults that typically occur when:- The driver misprograms the GPU.
- There's a corruption in the command stream sent to the GPU.
- A hardware failure or instability affects GPU operation.

For more information, see

[XID errors on NVIDIA GPUs](https://docs.nvidia.com/deploy/xid-errors/index.html).**NVLink Status**: For NVIDIA VM SKUs that support NVLink, this condition confirms that NVLink is active and functioning.- NVLink is a high-speed interconnect used to facilitate data transfer between multiple GPUs.
- If NVLink is inactive or degraded, multi-GPU workloads might experience reduced performance or communication bottlenecks.

For more information, see

[NVIDIA NVLink](https://www.nvidia.com/en-us/data-center/nvlink/).**InfiniBand Link Flapping**: NPD monitors for InfiniBand (IB) link flapping, or intermittent connectivity of the IB network device.- Link flapping shouldn't occur under normal operating conditions and might result in degraded inter-node communication for distributed workloads.
- It can also signal physical layer issues, misconfigured firmware, or driver instability.

**NVIDIA GRID Driver License Check**: For NVIDIA VM SKUs that support GRID driver, this condition verifies license status of the installed GRID driver on[supported NVIDIA VM SKUs](/en-us/azure/virtual-machines/sizes/gpu-accelerated/nvadsa10v5-series).- Invalid might indicate the installed GRID driver is not licensed.


## Frequently asked questions

### Does Node Problem Detector (NPD) automatically remediate GPU node issues?

NPD doesn't take direct action to remediate GPU-enabled node issues. NPD detects and reports problems by publishing Kubernetes node conditions and events. Any remediation (for example: draining a node, restarting workloads, or replacing faulty hardware) must be handled manually, through external automation, or alerting systems configured by the Kubernetes operator.

### On which Azure VM sizes does AKS conduct GPU health monitoring through NPD?

Currently, NPD conducts health checks on GPU nodes provisioned with the `Standard_ND96asr_v4`

or `Standard_ND96isr_H100_v5`

VM size on AKS. Also on [A10 SKU](/en-us/azure/virtual-machines/sizes/gpu-accelerated/nvadsa10v5-series) for GRID Driver License checks.

### Does NPD monitor the health of multi-instance GPU (MIG) node pools?

Yes, NPD health monitoring is supported on [MIG-enabled AKS node pools](gpu-multi-instance).

## Next steps

- Provision GPUs on
[Linux](use-nvidia-gpu)or[Windows](use-windows-gpu)node pools in your AKS cluster. - Learn more about the
[types of node conditions and events](node-problem-detector)set by NPD on AKS. [Monitor general GPU metrics](monitor-gpu-metrics)using a self-managed metrics exporter.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/cluster-extensions -->

# Deploy and manage cluster extensions for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Cluster extensions provide an Azure Resource Manager driven experience for installation and lifecycle management of services like Azure Machine Learning or Kubernetes applications on an AKS cluster. This feature enables:

- Azure Resource Manager-based deployment of extensions, including at-scale deployments across AKS clusters.
- Lifecycle management of the extension (Update, Delete) from Azure Resource Manager.

## Categories of cluster extensions

There are two categories of cluster extensions, *Core* and *Standard* that can be deployed onto AKS clusters.

### Core extensions

Core Kubernetes extensions have broader region availability, a more integrated AKS experience, and release alignment to AKS version releases. Azure Backup is a core extension.

#### AKS native experience

Core extensions can be managed using `az aks`

CLI command.

```
az aks extension create \
--name <core extension name> \
--extension-type <type> \
--cluster-name <name> \
--resource-group <group>
```


For more information about the commands, see [ az aks](/en-us/cli/azure/aks).

#### Release policy

Minor and major upgrades of core extensions occur alongside AKS minor and major version updates to avoid introducing breaking changes and provide better reliability.

### Standard extensions

For information about the other cluster extensions, see the table in [Currently available extensions](cluster-extensions#currently-available-extensions) and the [Kubernetes apps](deploy-marketplace) deployed via Azure Marketplace are of the Standard Extension type.

Standard extensions can be managed using the `az k8s-extension`

CLI command. For more information, see [Deploy and manage cluster extensions by using Azure CLI](deploy-extensions-az-cli).

```
az k8s-extension create \
--name <standard extension name> \
--extension-type <extension-type> \
--scope cluster \
--cluster-name <clusterName> \
--resource-group <resourceGroupName> \
--cluster-type managedClusters
```


## Cluster extension requirements

The cluster extensions platform is supported in all regions where AKS is deployed, except Qatar Central and US air gapped clouds. Although the platform is available in all regions, check the region availability for individual extensions.

Important

Ensure that your AKS cluster is created with a managed identity, as cluster extensions don't work with service principal-based clusters.

For new clusters created with `az aks create`

, managed identity is configured by default. For existing service principal-based clusters that need to be switched over to managed identity, it can be enabled by running `az aks update`

with the `--enable-managed-identity`

flag. For more information, see [Use managed identity](use-managed-identity).

Note

If you enabled [Microsoft Entra pod-managed identity](use-azure-ad-pod-identity) on your AKS cluster or are considering implementing it,
we recommend you first review [Workload identity overview](workload-identity-overview) to understand our
recommendations and options to set up your cluster to use a Microsoft Entra Workload ID (preview).
This authentication method replaces pod-managed identity (preview), which integrates with the Kubernetes native capabilities
to federate with any external identity providers.
The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service was deprecated as of October 24, 2022.

## Currently available extensions

| Extension | Description |
|---|---|
|

`Dapr`

is a portable, event-driven runtime that makes it easy for any developer to build resilient, stateless, and stateful applications that run on cloud and edge.[Azure App Configuration](azure-app-configuration-quickstart)[Azure Machine Learning](/en-us/azure/machine-learning/how-to-attach-kubernetes-anywhere)[Flux (GitOps)](/en-us/azure/azure-arc/kubernetes/conceptual-gitops-flux2)[supported versions of Flux (GitOps)](/en-us/azure/azure-arc/kubernetes/extensions-release#flux-gitops)and[Tutorial: Deploy applications using GitOps with Flux v2](/en-us/azure/azure-arc/kubernetes/tutorial-use-gitops-flux2).[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction)[Azure Backup for AKS](/en-us/azure/backup/azure-kubernetes-service-backup-overview)You can also [select and deploy Kubernetes applications available through Marketplace](deploy-marketplace).

Note

Cluster extensions provide a platform for different extensions to be installed and managed on an AKS cluster. If you're facing issues while using any of these extensions, open a support ticket with the respective service.

## Next steps

- Learn how to
[deploy cluster extensions by using Azure CLI](deploy-extensions-az-cli). - Read about
[cluster extensions](/en-us/azure/azure-arc/kubernetes/conceptual-extensions).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices -->

# Cluster operator and developer best practices to build and manage applications on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Building and running applications successfully in Azure Kubernetes Service (AKS) requires understanding and implementation of some key concepts, including:

- Multi-tenancy and scheduler features.
- Cluster and pod security.
- Business continuity and disaster recovery.

The AKS product group, engineering teams, and field teams (including global black belts (GBBs)) contributed to, wrote, and grouped the following best practices and conceptual articles. Their purpose is to help cluster operators and developers better understand the concepts above and implement the appropriate features.

## Cluster operator best practices

If you're a cluster operator, work with application owners and developers to understand their needs. Then, you can use the following best practices to configure your AKS clusters to fit your needs.

An important practice that you should include as part of your application development and deployment process is remembering to follow commonly used deployment and testing patterns. Testing your application before deployment is an important step to ensure its quality, functionality, and compatibility with the target environment. It can help you identify and fix any errors, bugs, or issues that might affect the performance, security, or usability of the application or underlying infrastructure.

### Multi-tenancy

[Best practices for cluster isolation](operator-best-practices-cluster-isolation)- Includes multi-tenancy core components and logical isolation with namespaces.

[Best practices for basic scheduler features](operator-best-practices-scheduler)- Includes using resource quotas and pod disruption budgets.

[Best practices for advanced scheduler features](operator-best-practices-advanced-scheduler)- Includes using taints and tolerations, node selectors and affinity, and inter-pod affinity and anti-affinity.

[Best practices for authentication and authorization](operator-best-practices-identity)- Includes integration with Microsoft Entra ID, using Kubernetes role-based access control (Kubernetes RBAC), using Azure RBAC, and pod identities.


### Security

[Best practices for cluster security and upgrades](operator-best-practices-cluster-security)- Includes securing access to the API server, limiting container access, and managing upgrades and node reboots.

[Best practices for container image management and security](operator-best-practices-container-image-management)- Includes securing the image and runtimes and automated builds on base image updates.

[Best practices for pod security](developer-best-practices-pod-security)- Includes securing access to resources, limiting credential exposure, and using pod identities and digital key vaults.


### Network and storage

[Best practices for network connectivity](operator-best-practices-network)- Includes different network models, using ingress and web application firewalls (WAF), and securing node SSH access.

[Best practices for storage and backups](operator-best-practices-storage)- Includes choosing the appropriate storage type and node size, dynamically provisioning volumes, and data backups.


### Running enterprise-ready workloads

[Best practices for business continuity and disaster recovery](operator-best-practices-multi-region)- Includes using region pairs, multiple clusters with Azure Traffic Manager, and geo-replication of container images.


## Developer best practices

If you're a developer or application owner, you can simplify your development experience and define required application performance features.

[Best practices for application developers to manage resources](developer-best-practices-resource-management)- Includes defining pod resource requests and limits, configuring development tools, and checking for application issues.

[Best practices for pod security](developer-best-practices-pod-security)- Includes securing access to resources, limiting credential exposure, and using pod identities and digital key vaults.

[Best practices for deployment and cluster reliability](best-practices-app-cluster-reliability)- Includes deployment, cluster, and node pool level best practices.


## Kubernetes and AKS concepts

The following conceptual articles cover some of the fundamental features and components for clusters in AKS:

[Kubernetes core concepts](concepts-clusters-workloads)[Access and identity](concepts-identity)[Security concepts](concepts-security)[Network concepts](concepts-network)[Storage options](concepts-storage)[Scaling options](concepts-scale)

## Next steps

For guidance on a designing an enterprise-scale implementation of AKS, see [Plan your AKS design](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/events -->

# Use Kubernetes events for troubleshooting in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Kubernetes events to monitor and troubleshoot issues in your Azure Kubernetes Service (AKS) clusters.

## What are Kubernetes events?

Events are one of the most prominent sources for monitoring and troubleshooting issues in Kubernetes. They capture and record information about the lifecycle of various Kubernetes objects, such as pods, nodes, services, and deployments. By monitoring events, you can gain visibility into your cluster's activities, identify issues, and troubleshoot problems effectively.

Kubernetes events don't persist throughout your cluster lifecycle, as there's no retention mechanism. Events are **only available for one hour after the event is generated**. To store events for a longer time period, enable

[Container insights](/en-us/azure/azure-monitor/containers/container-insights-enable-aks).

## Kubernetes event objects

The following table lists some key Kubernetes event objects:

| Field name | Description |
|---|---|
| type | The type is based on the severity of the event:Warning events signal potentially problematic situations, such as a pod repeatedly failing or a node running out of resources. They require attention, but might not result in immediate failure.Normal events represent routine operations, such as a pod being scheduled or a deployment scaling up. They usually indicate healthy cluster behavior. |
| reason | The reason why the event was generated. For example, FailedScheduling or CrashLoopBackoff. |
| message | A human-readable message that describes the event. |
| namespace | The namespace of the Kubernetes object that the event is associated with. |
| firstSeen | Timestamp when the event was first observed. |
| lastSeen | Timestamp of when the event was last observed. |
| reportingController | The name of the controller that reported the event. For example, `kubernetes.io/kubelet` . |
| object | The name of the Kubernetes object that the event is associated with. |

For more information, see the official [Kubernetes documentation](https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/event-v1/).

## View Kubernetes events

List all events in your cluster using the `kubectl get events`

command.

Assuming your cluster is already created and available (per doc prerequisites), get credentials (note the `--overwrite-existing`

flag is set to avoid kubeconfig errors):

```
az aks get-credentials --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER --overwrite-existing
```


Now list all events in your cluster:

```
kubectl get events
```


Results:

```
LAST SEEN TYPE REASON OBJECT MESSAGE
xxm Normal Scheduled pod/my-pod-xxxxx Successfully assigned default/my-pod-xxxxx to aks-nodepoolxx-xxxxxxx-vmss000000
xxm Normal Pulled pod/my-pod-xxxxx Container image "nginx" already present on machine
xxm Normal Created pod/my-pod-xxxxx Created container nginx
xxm Normal Started pod/my-pod-xxxxx Started container nginx
...
```


Look at a specific pod's events by first finding the name of the pod and then using the `kubectl describe pod`

command.

List the pods in the current namespace:

```
kubectl get pods
```


Results:

```
NAME READY STATUS RESTARTS AGE
my-pod-xxxxx 1/1 Running 0 xxm
nginx-deployment-xxxxx 1/1 Running 0 xxm
...
```


Replace `<pod-name>`

below with your actual pod name. For automation, here's an example for the first pod in the list:

```
POD_NAME=$(kubectl get pods -o jsonpath="{.items[0].metadata.name}")
kubectl describe pod $POD_NAME
```


## Best practices for troubleshooting with events

### Filtering events for relevance

You might have various namespaces and services running in your AKS cluster. Filtering events based on object type, namespace, or reason can help narrow down the results to the most relevant information.

For example, you can use the following command to filter events within the default namespace:

```
kubectl get events --namespace default
```


### Automating event notifications

To ensure timely response to critical events in your AKS cluster, set up automated notifications. Azure offers integration with monitoring and alerting services like [Azure Monitor](monitor-aks). You can configure alerts to trigger based on specific event patterns. This way, you're immediately informed about crucial issues that require attention.

### Regularly reviewing events

Make a habit of regularly reviewing events in your AKS cluster. This proactive approach can help you identify trends, catch potential problems early, and prevent escalations. By staying on top of events, you can maintain the stability and performance of your applications.

## Next steps

Now that you understand Kubernetes events, you can continue your monitoring and observability journey by [enabling Container insights](/en-us/azure/azure-monitor/containers/container-insights-enable-aks).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/validate-postgresql-ha -->

# Validate and test a PostgreSQL database deployment on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you perform various testing and validation steps on a PostgreSQL database deployed on AKS. This includes verifying the deployment, connecting to the database, and testing failover scenarios.

- If you haven't already deployed PostgreSQL, follow the steps in
[Deploy a highly available PostgreSQL database on AKS with Azure CLI](deploy-postgresql-ha)to get set up, and then you can return to this article.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Inspect the deployed PostgreSQL cluster

Validate that PostgreSQL is spread across multiple availability zones by retrieving the AKS node details using the [ kubectl get](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_get/) command.

```
kubectl get nodes \
--context $AKS_PRIMARY_CLUSTER_NAME \
--namespace $PG_NAMESPACE \
--output json | jq '.items[] | {node: .metadata.name, zone: .metadata.labels."failure-domain.beta.kubernetes.io/zone"}'
```


Your output should resemble the following example output with the availability zone shown for each node:

```
{
"node": "aks-postgres-15810965-vmss000000",
"zone": "westus3-1"
}
{
"node": "aks-postgres-15810965-vmss000001",
"zone": "westus3-2"
}
{
"node": "aks-postgres-15810965-vmss000002",
"zone": "westus3-3"
}
{
"node": "aks-systempool-26112968-vmss000000",
"zone": "westus3-1"
}
{
"node": "aks-systempool-26112968-vmss000001",
"zone": "westus3-2"
}
```


## Connect to PostgreSQL and create a sample dataset

In this section, you create a table and insert some data into the app database that was created in the CNPG Cluster CRD you deployed earlier. You use this data to validate the backup and restore operations for the PostgreSQL cluster.

Create a table and insert data into the app database using the following commands:

`kubectl cnpg psql $PG_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE`

`-- Create a small dataset CREATE TABLE datasample (id INTEGER, name VARCHAR(255)); INSERT INTO datasample (id, name) VALUES (1, 'John'); INSERT INTO datasample (id, name) VALUES (2, 'Jane'); INSERT INTO datasample (id, name) VALUES (3, 'Alice'); SELECT COUNT(*) FROM datasample;`

Type

`\q`

to exit psql when finished.Your output should resemble the following example output:

`CREATE TABLE INSERT 0 1 INSERT 0 1 INSERT 0 1 count ------- 3 (1 row)`


## Connect to PostgreSQL read-only replicas

Connect to the PostgreSQL read-only replicas and validate the sample dataset using the following commands:

`kubectl cnpg psql --replica $PG_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE`

`SELECT pg_is_in_recovery();`

Example output

`pg_is_in_recovery ------------------- t (1 row)`

`SELECT COUNT(*) FROM datasample;`

Example output

`count ------- 3 (1 row)`


## Set up on-demand and scheduled PostgreSQL backups using Barman

Note

CloudNativePG is expected to deprecate native Barman Cloud support in favor of the [Barman Cloud plugin](https://cloudnative-pg.io/plugin-barman-cloud/docs/intro/) in an upcoming 1.29 release. The steps in this guide continue to work today, but plan to migrate to the plugin once it stabilizes.

Validate that the PostgreSQL cluster can access the Azure storage account specified in the CNPG Cluster CRD and that

`Working WAL archiving`

reports as`OK`

using the following command:`kubectl cnpg status $PG_PRIMARY_CLUSTER_NAME 1 \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE`

Example output

`Continuous Backup status First Point of Recoverability: Not Available Working WAL archiving: OK WALs waiting to be archived: 0 Last Archived WAL: 00000001000000000000000A @ 2024-07-09T17:18:13.982859Z Last Failed WAL: -`

Deploy an on-demand backup to Azure Storage, which uses the AKS workload identity integration, using the YAML file with the

command.`kubectl apply`

`export BACKUP_ONDEMAND_NAME="on-demand-backup-1" cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -v 9 -f - apiVersion: postgresql.cnpg.io/v1 kind: Backup metadata: name: $BACKUP_ONDEMAND_NAME spec: method: barmanObjectStore cluster: name: $PG_PRIMARY_CLUSTER_NAME EOF`

Validate the status of the on-demand backup using the

command.`kubectl describe`

`kubectl describe backup $BACKUP_ONDEMAND_NAME \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE`

Example output

`Type Reason Age From Message ---- ------ ---- ---- ------- Normal Starting 6s cloudnative-pg-backup Starting backup for cluster pg-primary-cnpg-r8c7unrw Normal Starting 5s instance-manager Backup started Normal Completed 1s instance-manager Backup completed`

Validate that the cluster has a first point of recoverability using the following command:

`kubectl cnpg status $PG_PRIMARY_CLUSTER_NAME 1 \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE`

Example output

`Continuous Backup status First Point of Recoverability: 2024-06-05T13:47:18Z Working WAL archiving: OK`

Configure a scheduled backup for

*every hour at 15 minutes past the hour*using the YAML file with thecommand.`kubectl apply`

`export BACKUP_SCHEDULED_NAME="scheduled-backup-1" cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -v 9 -f - apiVersion: postgresql.cnpg.io/v1 kind: ScheduledBackup metadata: name: $BACKUP_SCHEDULED_NAME spec: # Backup once per hour schedule: "0 15 * ? * *" backupOwnerReference: self cluster: name: $PG_PRIMARY_CLUSTER_NAME EOF`

Validate the status of the scheduled backup using the

command.`kubectl describe`

`kubectl describe scheduledbackup $BACKUP_SCHEDULED_NAME \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE`

View the backup files stored on Azure blob storage for the primary cluster using the

command.`az storage blob list`

`az storage blob list \ --account-name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --container-name backups \ --query "[*].name" \ --only-show-errors`

Your output should resemble the following example output, validating the backup was successful:

`[ "pg-primary-cnpg-r8c7unrw/base/20240605T134715/backup.info", "pg-primary-cnpg-r8c7unrw/base/20240605T134715/data.tar", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000001", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000002", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000003", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000003.00000028.backup", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000004", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000005", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000005.00000028.backup", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000006", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000007", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000008", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000009" ]`


## Restore the on-demand backup to a new PostgreSQL cluster

In this section, you restore the on-demand backup you created earlier using the CNPG operator into a new instance using the bootstrap Cluster CRD. A single instance cluster is used for simplicity. Remember that the AKS workload identity (via CNPG inheritFromAzureAD) accesses the backup files, and that the recovery cluster name is used to generate a new Kubernetes service account specific to the recovery cluster.

You also create a second federated credential to map the new recovery cluster service account to the existing UAMI that has "Storage Blob Data Contributor" access to the backup files on blob storage.

Create a second federated identity credential using the

command.`az identity federated-credential create`

`export PG_PRIMARY_CLUSTER_NAME_RECOVERED="$PG_PRIMARY_CLUSTER_NAME-recovered-db" az identity federated-credential create \ --name $PG_PRIMARY_CLUSTER_NAME_RECOVERED \ --identity-name $AKS_UAMI_CLUSTER_IDENTITY_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --issuer "${AKS_PRIMARY_CLUSTER_OIDC_ISSUER}" \ --subject system:serviceaccount:"${PG_NAMESPACE}":"${PG_PRIMARY_CLUSTER_NAME_RECOVERED}" \ --audience api://AzureADTokenExchange`

Restore the on-demand backup using the Cluster CRD with the

command.`kubectl apply`

`cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -v 9 -f - apiVersion: postgresql.cnpg.io/v1 kind: Cluster metadata: name: $PG_PRIMARY_CLUSTER_NAME_RECOVERED spec: inheritedMetadata: annotations: service.beta.kubernetes.io/azure-dns-label-name: $AKS_PRIMARY_CLUSTER_PG_DNSPREFIX labels: azure.workload.identity/use: "true" instances: 1 affinity: nodeSelector: workload: postgres # Point to cluster backup created earlier and stored on Azure Blob Storage bootstrap: recovery: source: clusterBackup storage: size: 2Gi pvcTemplate: accessModes: - ReadWriteOnce resources: requests: storage: 2Gi storageClassName: managed-csi-premium volumeMode: Filesystem walStorage: size: 2Gi pvcTemplate: accessModes: - ReadWriteOnce resources: requests: storage: 2Gi storageClassName: managed-csi-premium volumeMode: Filesystem serviceAccountTemplate: metadata: annotations: azure.workload.identity/client-id: "$AKS_UAMI_WORKLOAD_CLIENTID" labels: azure.workload.identity/use: "true" externalClusters: - name: clusterBackup barmanObjectStore: destinationPath: https://${PG_PRIMARY_STORAGE_ACCOUNT_NAME}.blob.core.windows.net/backups serverName: $PG_PRIMARY_CLUSTER_NAME azureCredentials: inheritFromAzureAD: true wal: maxParallel: 8 EOF`

Connect to the recovered instance, then validate that the dataset created on the original cluster where the full backup was taken is present using the following command:

`kubectl cnpg psql $PG_PRIMARY_CLUSTER_NAME_RECOVERED --namespace $PG_NAMESPACE`

`SELECT COUNT(*) FROM datasample;`

Example output

`count ------- 3 (1 row) Type \q to exit psql`

Delete the recovered cluster using the following command:

`kubectl cnpg destroy $PG_PRIMARY_CLUSTER_NAME_RECOVERED 1 \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE`

Delete the federated identity credential using the

command.`az identity federated-credential delete`

`az identity federated-credential delete \ --name $PG_PRIMARY_CLUSTER_NAME_RECOVERED \ --identity-name $AKS_UAMI_CLUSTER_IDENTITY_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --yes`


## Expose the PostgreSQL cluster using a public load balancer

In this section, you configure the necessary infrastructure to publicly expose the PostgreSQL read-write and read-only endpoints with IP source restrictions to the public IP address of your client workstation.

You also retrieve the following endpoints from the Cluster IP service:

*One*primary read-write endpoint that ends with`*-rw`

.*Zero to N*(depending on the number of replicas) read-only endpoints that end with`*-ro`

.*One*replication endpoint that ends with`*-r`

.

Get the Cluster IP service details using the

command.`kubectl get`

`kubectl get services \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE \ -l cnpg.io/cluster=$PG_PRIMARY_CLUSTER_NAME`

Example output

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE pg-primary-cnpg-sryti1qf-r ClusterIP 10.0.193.27 <none> 5432/TCP 3h57m pg-primary-cnpg-sryti1qf-ro ClusterIP 10.0.237.19 <none> 5432/TCP 3h57m pg-primary-cnpg-sryti1qf-rw ClusterIP 10.0.244.125 <none> 5432/TCP 3h57m`

Note

There are three services:

`namespace/cluster-name-ro`

mapped to port 5433,`namespace/cluster-name-rw`

, and`namespace/cluster-name-r`

mapped to port 5433. It’s important to avoid using the same port as the read/write node of the PostgreSQL database cluster. If you want applications to access only the read-only replica of the PostgreSQL database cluster, direct them to port 5433. The final service is typically used for data backups but can also function as a read-only node.Get the service details using the

command.`kubectl get`

`export PG_PRIMARY_CLUSTER_RW_SERVICE=$(kubectl get services \ --namespace $PG_NAMESPACE \ --context $AKS_PRIMARY_CLUSTER_NAME \ -l "cnpg.io/cluster" \ --output json | jq -r '.items[] | select(.metadata.name | endswith("-rw")) | .metadata.name') echo $PG_PRIMARY_CLUSTER_RW_SERVICE export PG_PRIMARY_CLUSTER_RO_SERVICE=$(kubectl get services \ --namespace $PG_NAMESPACE \ --context $AKS_PRIMARY_CLUSTER_NAME \ -l "cnpg.io/cluster" \ --output json | jq -r '.items[] | select(.metadata.name | endswith("-ro")) | .metadata.name') echo $PG_PRIMARY_CLUSTER_RO_SERVICE`

Configure the load balancer service with the following YAML files using the

command.`kubectl apply`

`cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME -f - apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-load-balancer-resource-group: $AKS_PRIMARY_CLUSTER_NODERG_NAME service.beta.kubernetes.io/azure-pip-name: $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME service.beta.kubernetes.io/azure-dns-label-name: $AKS_PRIMARY_CLUSTER_PG_DNSPREFIX name: cnpg-cluster-load-balancer-rw namespace: "${PG_NAMESPACE}" spec: type: LoadBalancer ports: - protocol: TCP port: 5432 targetPort: 5432 selector: cnpg.io/instanceRole: primary cnpg.io/podRole: instance loadBalancerSourceRanges: - "$MY_PUBLIC_CLIENT_IP/32" EOF cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME -f - apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-load-balancer-resource-group: $AKS_PRIMARY_CLUSTER_NODERG_NAME service.beta.kubernetes.io/azure-pip-name: $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME service.beta.kubernetes.io/azure-dns-label-name: $AKS_PRIMARY_CLUSTER_PG_DNSPREFIX name: cnpg-cluster-load-balancer-ro namespace: "${PG_NAMESPACE}" spec: type: LoadBalancer ports: - protocol: TCP port: 5433 targetPort: 5432 selector: cnpg.io/instanceRole: replica cnpg.io/podRole: instance loadBalancerSourceRanges: - "$MY_PUBLIC_CLIENT_IP/32" EOF`

Get the service details using the

command.`kubectl describe`

`kubectl describe service cnpg-cluster-load-balancer-rw \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE kubectl describe service cnpg-cluster-load-balancer-ro \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE export AKS_PRIMARY_CLUSTER_ALB_DNSNAME="$(az network public-ip show \ --resource-group $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --name $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME \ --query "dnsSettings.fqdn" --output tsv)" echo $AKS_PRIMARY_CLUSTER_ALB_DNSNAME`


### Validate public PostgreSQL endpoints

In this section, you validate that the Azure Load Balancer is properly set up using the static IP that you created earlier and routing connections to the primary read-write and read-only replicas and use the psql CLI to connect to both.

Remember that the primary read-write endpoint maps to TCP port 5432 and the read-only replica endpoints map to port 5433 to allow the same PostgreSQL DNS name to be used for readers and writers.

Note

You need the value of the app user password for PostgreSQL basic auth that was generated earlier and stored in the `$PG_DATABASE_APPUSER_SECRET`

environment variable.

Validate the public PostgreSQL endpoints using the following

`psql`

commands:`echo "Public endpoint for PostgreSQL cluster: $AKS_PRIMARY_CLUSTER_ALB_DNSNAME" # Query the primary, pg_is_in_recovery = false psql -h $AKS_PRIMARY_CLUSTER_ALB_DNSNAME \ -p 5432 -U app -d appdb -W -c "SELECT pg_is_in_recovery();"`

Example output

`pg_is_in_recovery ------------------- f (1 row)`

`echo "Query a replica, pg_is_in_recovery = true" psql -h $AKS_PRIMARY_CLUSTER_ALB_DNSNAME \ -p 5433 -U app -d appdb -W -c "SELECT pg_is_in_recovery();"`

Example output

`# Example output pg_is_in_recovery ------------------- t (1 row)`

When successfully connected to the primary read-write endpoint, the PostgreSQL function returns

`f`

for*false*, indicating that the current connection is writable.When connected to a replica, the function returns

`t`

for*true*, indicating the database is in recovery and read-only.

## Simulate an unplanned failover

In this section, you trigger a sudden failure by deleting the pod running the primary, which simulates a sudden crash or loss of network connectivity to the node hosting the PostgreSQL primary.

Check the status of the running pod instances using the following command:

`kubectl cnpg status $PG_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE`

Example output

`Name Current LSN Rep role Status Node --------------------------- ----------- -------- ------- ----------- pg-primary-cnpg-sryti1qf-1 0/9000060 Primary OK aks-postgres-32388626-vmss000000 pg-primary-cnpg-sryti1qf-2 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000001 pg-primary-cnpg-sryti1qf-3 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000002`

Delete the primary pod using the

command.`kubectl delete`

`PRIMARY_POD=$(kubectl get pod \ --namespace $PG_NAMESPACE \ --no-headers \ -o custom-columns=":metadata.name" \ -l role=primary) kubectl delete pod $PRIMARY_POD --grace-period=1 --namespace $PG_NAMESPACE`

Validate that the

`pg-primary-cnpg-sryti1qf-2`

pod instance is now the primary using the following command:`kubectl cnpg status $PG_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE`

Example output

`pg-primary-cnpg-sryti1qf-2 0/9000060 Primary OK aks-postgres-32388626-vmss000001 pg-primary-cnpg-sryti1qf-1 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000000 pg-primary-cnpg-sryti1qf-3 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000002`

Reset the

`pg-primary-cnpg-sryti1qf-1`

pod instance as the primary using the following command:`kubectl cnpg promote $PG_PRIMARY_CLUSTER_NAME 1 --namespace $PG_NAMESPACE`

Validate that the pod instances have returned to their original state before the unplanned failover test using the following command:

`kubectl cnpg status $PG_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE`

Example output

`Name Current LSN Rep role Status Node --------------------------- ----------- -------- ------- ----------- pg-primary-cnpg-sryti1qf-1 0/9000060 Primary OK aks-postgres-32388626-vmss000000 pg-primary-cnpg-sryti1qf-2 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000001 pg-primary-cnpg-sryti1qf-3 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000002`


## Clean up resources

Once you're finished reviewing your deployment, delete all the resources you created in this guide using the

command.`az group delete`

`az group delete --resource-group $RESOURCE_GROUP_NAME --no-wait --yes`


## Next steps

In this how-to guide, you learned how to:

- Use Azure CLI to create a multi-zone AKS cluster.
- Deploy a highly available PostgreSQL cluster and database using the CNPG operator.
- Set up monitoring for PostgreSQL using Prometheus and Grafana.
- Deploy a sample dataset to the PostgreSQL database.
- Simulate a cluster interruption and PostgreSQL replica failover.
- Perform a backup and restore of the PostgreSQL database.

To learn more about how you can use AKS for your workloads, see [What is Azure Kubernetes Service (AKS)?](what-is-aks) To learn more about Azure Database for PostgreSQL, see [What is Azure Database for PostgreSQL?](/en-us/azure/postgresql/flexible-server/overview)

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Ken Kilty | Principal TPM
- Russell de Pina | Principal TPM
- Adrian Joian | Senior Customer Engineer
- Jenny Hayes | Senior Content Developer
- Carol Smith | Senior Content Developer
- Erin Schaffer | Content Developer 2
- Adam Sharif | Customer Engineer 2

## Acknowledgment

This documentation was jointly developed with EnterpriseDB, the maintainers of the CloudNativePG operator. We thank [Gabriele Bartolini](https://cloudnative-pg.io/authors/gbartolini/) for reviewing earlier drafts of this document and offering technical improvements.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/app-routing-nginx-configuration -->

# Advanced NGINX ingress controller and ingress configurations with the application routing add-on for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article walks you through two ways to configure ingress controllers and ingress objects with the application routing add-on for Azure Kubernetes Service (AKS):

[Configuration of the NGINX ingress controller](#control-the-default-nginx-ingress-controller-configuration)such as creating multiple controllers, configuring private load balancers, and setting static IP addresses.[Configuration per ingress resource](#configuration-per-ingress-resource-through-annotations)through annotations.

## Prerequisites

- An AKS cluster with the
[application routing add-on](app-routing)enabled. `kubectl`

configured to connect to your AKS cluster. For more information, see[Connect to your AKS cluster](#connect-to-your-aks-cluster).

### Connect to your AKS cluster

To connect to the Kubernetes cluster from your local computer, you use `kubectl`

, the Kubernetes command-line client. You can install it locally using the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. If you use the Azure Cloud Shell,

`kubectl`

is already installed.Configure kubectl to connect to your Kubernetes cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Configuration properties for NGINX ingress controllers

The application routing add-on uses a Kubernetes [custom resource definition (CRD)](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) called [ NginxIngressController](https://github.com/Azure/aks-app-routing-operator/blob/main/config/crd/bases/approuting.kubernetes.azure.com_nginxingresscontrollers.yaml) to configure NGINX ingress controllers. You can create more ingress controllers or modify existing configurations.

The following table lists properties you can set to configure an `NginxIngressController`

:

| Field | Type | Description | Required | Default |
|---|---|---|---|---|
`controllerNamePrefix` |
string | Name for the managed NGINX Ingress Controller resources. | Yes | `nginx` |
`customHTTPErrors` |
array | Array of error codes to be sent to the default backend if there's an error. | No | |
`defaultBackendService` |
object | Service to route unmatched HTTP traffic. Contains nested properties: | No | |
`name` |
string | Service name. | Yes | |
`namespace` |
string | Service namespace. | Yes | |
`defaultSSLCertificate` |
object | Contains the default certificate for accessing the default backend service. Contains nested properties: | No | |
`forceSSLRedirect` |
boolean | Forces HTTPS redirection when a certificate is set. | No | `false` |
`keyVaultURI` |
string | URI for a Key Vault secret storing the certificate. | No | |
`secret` |
object | Holds secret information for the default SSL certificate. Contains nested properties: | No | |
`name` |
string | Secret name. | Yes | |
`namespace` |
string | Secret namespace. | Yes | |
`httpDisabled` |
boolean | Flag to disable HTTP traffic to the controller. | No | |
`ingressClassName` |
string | IngressClass name used by the controller. | Yes | `nginx.approuting.kubernetes.azure.com` |
`loadBalancerAnnotations` |
object | A map of annotations to control the behavior of the NGINX ingress controller's service by setting
|

`scaling`

`maxReplicas`

`100`

`minReplicas`

`2`

`threshold`

**scales quickly for sudden spikes,**`rapid`

**favors cost-effectiveness, and**`steady`

**is a mix.**`balanced`

`balanced`

## Control the default NGINX ingress controller configuration

When you enable the application routing add-on with NGINX, it creates an ingress controller called `default`

in the `app-routing-namespace`

configured with a public facing Azure load balancer. That ingress controller uses an ingress class name of `webapprouting.kubernetes.azure.com`

.

You can also control if the default gets a public or an internal IP, or if it gets created at all when enabling the add-on.

Possible configuration options include:

: The default NGINX ingress controller isn't created and isn't deleted if it already exists. You should manually delete the default`None`

`NginxIngressController`

custom resource if desired.: The default NGINX ingress controller is created with an internal load balancer. Any annotation changes on the`Internal`

`NginxIngressController`

custom resource to make it external are overwritten.: The default NGINX ingress controller created with an external load balancer. Any annotation changes on the`External`

`NginxIngressController`

custom resource to make it internal are overwritten.(default): The default NGINX ingress controller is created with an external load balancer. You can edit the default`AnnotationControlled`

`NginxIngressController`

custom resource to configure load balancer annotations.)

### Control the default ingress controller configuration on a new cluster

Enable application routing on a new cluster using the

command with the`az aks create`

`--enable-app-routing`

and`--app-routing-default-nginx-controller`

flags. You need to set the`<DefaultIngressControllerType>`

to one of the configuration options described in[Control the default NGINX ingress controller configuration](#control-the-default-nginx-ingress-controller-configuration).`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --location $LOCATION \ --enable-app-routing \ --app-routing-default-nginx-controller <DefaultIngressControllerType>`


### Update the default ingress controller configuration on an existing cluster

Update the application routing default ingress controller configuration on an existing cluster using the

command with the`az aks approuting update`

`--nginx`

flag. You need to set the`<DefaultIngressControllerType>`

to one of the configuration options described in[Control the default NGINX ingress controller configuration](#control-the-default-nginx-ingress-controller-configuration).`az aks approuting update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --nginx <DefaultIngressControllerType>`


## Create another public facing NGINX ingress controller

Copy the following YAML manifest into a new file named

`nginx-public-controller.yaml`

and save the file to your local computer.`apiVersion: approuting.kubernetes.azure.com/v1alpha1 kind: NginxIngressController metadata: name: nginx-public spec: ingressClassName: nginx-public controllerNamePrefix: nginx-public`

Create the NGINX ingress controller resources using the

command.`kubectl apply`

`kubectl apply -f nginx-public-controller.yaml`

The following example output shows the created resource:

`nginxingresscontroller.approuting.kubernetes.azure.com/nginx-public created`


## Create an internal NGINX ingress controller with a private IP address

Copy the following YAML manifest into a new file named

`nginx-internal-controller.yaml`

and save the file to your local computer.`apiVersion: approuting.kubernetes.azure.com/v1alpha1 kind: NginxIngressController metadata: name: nginx-internal spec: ingressClassName: nginx-internal controllerNamePrefix: nginx-internal loadBalancerAnnotations: service.beta.kubernetes.io/azure-load-balancer-internal: "true"`

Create the NGINX ingress controller resources using the

command.`kubectl apply`

`kubectl apply -f nginx-internal-controller.yaml`

The following example output shows the created resource:

`nginxingresscontroller.approuting.kubernetes.azure.com/nginx-internal created`


## Create an NGINX ingress controller with a static IP address

Create an Azure resource group using the

command.`az group create`

`az group create --name $NETWORK_RESOURCE_GROUP --location $LOCATION`

Create a static public IP address using the

command.`az network public ip create`

`az network public-ip create \ --resource-group $NETWORK_RESOURCE_GROUP \ --name $PUBLIC_IP_NAME \ --sku Standard \ --allocation-method static`

Note

If you're using a

*Basic*SKU load balancer in your AKS cluster, use`Basic`

for the`--sku`

parameter when defining a public IP. Only`Basic`

SKU IPs work with the*Basic*SKU load balancer and only`Standard`

SKU IPs work with the*Standard*SKU load balancers.Ensure the cluster identity used by the AKS cluster has delegated permissions to the public IP's resource group using the

command.`az role assignment create`

`CLIENT_ID=$(az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query identity.principalId -o tsv) RG_SCOPE=$(az group show --name $NETWORK_RESOURCE_GROUP --query id -o tsv) az role assignment create \ --assignee ${CLIENT_ID} \ --role "Network Contributor" \ --scope ${RG_SCOPE}`

Copy the following YAML manifest into a new file named

`nginx-staticip-controller.yaml`

and save the file to your local computer.Note

You can either use

`service.beta.kubernetes.io/azure-pip-name`

for public IP name, or use`service.beta.kubernetes.io/azure-load-balancer-ipv4`

for an IPv4 address and`service.beta.kubernetes.io/azure-load-balancer-ipv6`

for an IPv6 address, as shown in the example YAML. Adding the`service.beta.kubernetes.io/azure-pip-name`

annotation ensures the most efficient Load Balancer creation and is highly recommended to avoid potential throttling.`apiVersion: approuting.kubernetes.azure.com/v1alpha1 kind: NginxIngressController metadata: name: nginx-static spec: ingressClassName: nginx-static controllerNamePrefix: nginx-static loadBalancerAnnotations: service.beta.kubernetes.io/azure-pip-name: "$PUBLIC_IP_NAME" service.beta.kubernetes.io/azure-load-balancer-resource-group: "$NETWORK_RESOURCE_GROUP"`

Create the NGINX ingress controller resources using the

command.`kubectl apply`

`kubectl apply -f nginx-staticip-controller.yaml`

The following example output shows the created resource:

`nginxingresscontroller.approuting.kubernetes.azure.com/nginx-static created`


## Verify the ingress controller was created

Verify the status of the NGINX ingress controller using the

command.`kubectl get nginxingresscontroller`

`kubectl get nginxingresscontroller --name $INGRESS_CONTROLLER_NAME`

The following example output shows the created resource. It may take a few minutes for the controller to be available:

`NAME INGRESSCLASS CONTROLLERNAMEPREFIX AVAILABLE nginx-public nginx-public nginx True`


### View the conditions of the ingress controller

View the conditions of the ingress controller to troubleshoot any issues using the

command.`kubectl get nginxingresscontroller`

`kubectl get nginxingresscontroller --name $INGRESS_CONTROLLER_NAME -o jsonpath='{range .items[*].status.conditions[*]}{.lastTransitionTime}{"\t"}{.status}{"\t"}{.type}{"\t"}{.message}{"\n"}{end}'`

The following example output shows the conditions of a healthy ingress controller:

`2023-11-29T19:59:24Z True IngressClassReady Ingress Class is up-to-date 2023-11-29T19:59:50Z True Available Controller Deployment has minimum availability and IngressClass is up-to-date 2023-11-29T19:59:50Z True ControllerAvailable Controller Deployment is available 2023-11-29T19:59:25Z True Progressing Controller Deployment has successfully progressed`


## Use the ingress controller in an ingress

Copy the following YAML manifest into a new file named

`ingress.yaml`

and save the file to your local computer.Note

Update

`<HostName>`

with your DNS host name. The`<IngressClassName>`

is the one you defined when creating the`NginxIngressController`

.`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: aks-helloworld namespace: hello-web-app-routing spec: ingressClassName: <IngressClassName> rules: - host: <HostName> http: paths: - backend: service: name: aks-helloworld port: number: 80 path: / pathType: Prefix`

Create the cluster resources using the

command.`kubectl apply`

`kubectl apply -f ingress.yaml --namespace hello-web-app-routing`

The following example output shows the created resource:

`ingress.networking.k8s.io/aks-helloworld created`


## Verify the managed ingress was created

Verify the managed ingress was created using the

command.`kubectl get ingress`

`kubectl get ingress --namespace hello-web-app-routing`

Your output should resemble the following example output:

`NAME CLASS HOSTS ADDRESS PORTS AGE aks-helloworld webapprouting.kubernetes.azure.com myapp.contoso.com 20.51.92.19 80, 443 4m`


## Remove ingress controllers

Remove the NGINX ingress controller using the

command.`kubectl delete nginxingresscontroller`

`kubectl delete nginxingresscontroller --name $INGRESS_CONTROLLER_NAME`


## Configuration per ingress resource through annotations

The NGINX ingress controller supports adding [annotations to specific ingress objects](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/) to customize their behavior.

You can [annotate](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) the ingress object by adding the respective annotation in the `metadata.annotations`

field.

Note

Annotation keys and values can only be strings. Other types, such as boolean or numeric values must be quoted. For example: `"true"`

, `"false"`

, `"100"`

.

The following sections provide examples for common configurations. For a full list, see the [NGINX ingress annotations documentation](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/).

### Custom max body size

For NGINX, a 413 error is returned to the client when the size in a request exceeds the maximum allowed size of the client request body. To override the default value, use the annotation:

```
nginx.ingress.kubernetes.io/proxy-body-size: 4m
```


Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/proxy-body-size: 4m
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- backend:
service:
name: aks-helloworld
port:
number: 80
path: /
pathType: Prefix
```


### Custom connection timeout

You can change the timeout that the NGINX ingress controller waits to close a connection with your workload. All timeout values are unitless and in seconds. To override the default timeout, use the following annotation to set a valid 120-seconds proxy read timeout:

```
nginx.ingress.kubernetes.io/proxy-read-timeout: "120"
```


Review [custom timeouts](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#custom-timeouts) for other configuration options.

Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/proxy-read-timeout: "120"
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- backend:
service:
name: aks-helloworld
port:
number: 80
path: /
pathType: Prefix
```


### Backend protocol

The NGINX ingress controller uses `HTTP`

to reach the services by default. To configure alternative backend protocols such as `HTTPS`

or `GRPC`

, use one of the following annotations:

```
# HTTPS annotation
nginx.ingress.kubernetes.io/backend-protocol: "HTTPS"
# GRPC annotation
nginx.ingress.kubernetes.io/backend-protocol: "GRPC"
```


Review [backend protocols](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#backend-protocol) for other configuration options.

Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/backend-protocol: "HTTPS"
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- backend:
service:
name: aks-helloworld
port:
number: 80
path: /
pathType: Prefix
```


### Cross-Origin Resource Sharing (CORS)

To enable Cross-Origin Resource Sharing (CORS) in an Ingress rule, use the following annotation:

```
nginx.ingress.kubernetes.io/enable-cors: "true"
```


Review [enable CORS](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#enable-cors) for other configuration options.

Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/enable-cors: "true"
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- backend:
service:
name: aks-helloworld
port:
number: 80
path: /
pathType: Prefix
```


### Disable SSL redirect

The controller redirects (308) to HTTPS if TLS is enabled for an ingress by default. To disable this feature for specific ingress resources, use the following annotation:

```
nginx.ingress.kubernetes.io/ssl-redirect: "false"
```


Review [server-side HTTPS enforcement through redirect](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#server-side-https-enforcement-through-redirect) for other configuration options.

Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/ssl-redirect: "false"
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- backend:
service:
name: aks-helloworld
port:
number: 80
path: /
pathType: Prefix
```


### URL rewriting

In some scenarios, the exposed URL in the backend service differs from the specified path in the ingress rule. Without a rewrite any request returns 404. This configuration is useful with [path-based routing](https://kubernetes.github.io/ingress-nginx/user-guide/ingress-path-matching/) where you can serve two different web applications under the same domain. You can set path expected by the service using the following annotation:

```
nginx.ingress.kubernetes.io/rewrite-target: /$2
```


Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/rewrite-target: /$2
nginx.ingress.kubernetes.io/use-regex: "true"
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- path: /app-one(/|$)(.*)
pathType: Prefix
backend:
service:
name: app-one
port:
number: 80
- path: /app-two(/|$)(.*)
pathType: Prefix
backend:
service:
name: app-two
port:
number: 80
```


### NGINX health probe path update

The default health probe path for the Azure Load Balancer associated with the NGINX ingress controller must be set to `"/healthz"`

. To ensure correct health checks, verify that the ingress controller service has the following annotation:

```
metadata:
annotations:
service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path: "/healthz"
```


If you're using Helm to manage your NGINX ingress controller, you can define the Azure Load Balancer health-probe annotation in a values file and apply it during an upgrade:

```
controller:
service:
annotations:
service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path: "/healthz"
```


This configuration helps maintain service availability and avoids unexpected traffic disruption during upgrades.

## Next steps

Learn about monitoring the ingress-nginx controller metrics included with the application routing add-on with [with Prometheus in Grafana](app-routing-nginx-prometheus) as part of analyzing the performance and usage of your application.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-app-configuration-quickstart -->

# Quickstart: Generate ConfigMap from Azure App Configuration

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can externalize the configurations of your Azure Kubernetes Service (AKS) workloads and manage them in [Azure App Configuration](/en-us/azure/azure-app-configuration/overview). The [Azure App Configuration Kubernetes provider](https://mcr.microsoft.com/artifact/mar/azure-app-configuration/kubernetes-provider/about) runs as a container in your cluster. Key benefits include:

**Seamless integration**: Pulls data from Azure App Configuration and Key Vault, making them accessible as ConfigMap and Secret without code changes in your workloads.**Dynamic update**: Built-in caching and refreshing capabilities for dynamic configuration, feature flagging, and automatic secret rotation.

The Azure App Configuration Kubernetes provider is available as an AKS extension. By following this document, you can easily install the extension and connect your AKS cluster with an App Configuration store using the Service Connector in the Azure portal. For information on setting up the provider using Helm, see the [Quickstart for Azure App Configuration Kubernetes provider](/en-us/azure/azure-app-configuration/quickstart-azure-kubernetes-service).

## Prerequisites

- An Azure Kubernetes Service (AKS) cluster.
[Create an AKS cluster](/en-us/azure/aks/tutorial-kubernetes-deploy-cluster#create-a-kubernetes-cluster). - A running workload in Azure Kubernetes Service (AKS) cluster. If you don't have one, you can
[create a demo application running in AKS](/en-us/azure/azure-app-configuration/quickstart-azure-kubernetes-service#create-an-application-running-in-aks).

## Create a service connection to App Configuration

Create a service connection between your AKS cluster and your App Configuration store using Microsoft Entra Workload Identity.

In the

[Azure portal](https://portal.azure.com), navigate to your AKS cluster resource.Select

**Settings**>**Service Connector**>**Create**.On the

**Basics**tab, configure the following settings:**Kubernetes namespace**: Specify the namespace you'd like to create ConfigMap or Secret to.**Service type**: Select**App Configuration**.**Use App Configuration Extension on Kubernetes**: Check the box to use the[Azure App Configuration AKS extension](azure-app-configuration)for this connection. Azure App Configuration AKS extension will be installed to current cluster if it's not yet.**Connection name**: Enter a connection name or use the default name.**Subscription**: Select the subscription of your App Configuration store.**App Configuration**: Select your App Configuration store. If you don't have one, click**Create new**to set one up.

Select

**Next: Authentication**. On the**Authentication**tab, keep the default selection of**Workload Identity**, select a**User assigned managed identity**you want to use. If you don't have one, click**Create new**to set one up.Select

**Next: Networking**and use the default settings.Select

**Next: Review + create**and wait for the validation to pass.Select

**Create**to create the service connection.

Note

The Service Connector simplifies the installation of the Azure App Configuration AKS extension from the Azure portal. You can also install it without Service Connector using Azure CLI, Bicep, or an ARM template. For more information, see [Install Azure App Configuration AKS extension](azure-app-configuration).

## Generate ConfigMap from App Configuration

Update the service connection to create and deploy an `AzureAppConfigurationProvider`

YAML resource in your AKS cluster. This resource generates a ConfigMap with data from your App Configuration store.

In the

[Azure portal](https://portal.azure.com), navigate to your AKS cluster resource and select**Settings**>**Service Connector**.Select the newly created connection, select

**Yaml snippet**in the top menu.On the

**AzureAppConfigurationProvider**tab, configure the following settings:**Using configuration as**: Choose to consume the configuration as a**mounted file**or**environment variables**.**Mounted file**: If selected, specify the**file type**and**file name**.**Selector**: Set the**Key filter**and**Label filter**to load data from your App Configuration store.

A YAML is generated based on your input. Click

**Apply**to add it to your AKS cluster. It will create a ConfigMap in your AKS cluster with data from your App Configuration store.Click

**Next**. On the**Workload**tab, configure the following settings:**File mount path**: Specify the file mount path if the mounted file option was selected.**Kubernetes Workload**: Select the workload where the generated ConfigMap will be injected.- Click
**Apply**to update the workload.


## Next Steps

To learn more about installing and customizing the Azure App Configuration AKS extension, refer to the following documents:

For a complete feature rundown of the Azure App Configuration Kubernetes Provider, see

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-autoprovision -->

# Overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS), including how it works, upgrade behavior, prerequisites, limitations, and resources to get started.

## What is node auto-provisioning in AKS?

When you deploy workloads onto AKS, you need to select the appropriate virtual machine (VM) size as part of your node pool configuration. As your workloads become more complex, you might have different workloads with varying resource requirements, which makes it more difficult to design your VM configuration for numerous resource requests.

Node auto-provisioning (NAP) simplifies this process by automatically provisioning and managing the optimal VM configuration for your workloads. NAP uses pending pod resource requirements to decide the optimal VM configuration to run your workloads in the most efficient and cost-effective manner.

NAP automatically deploys, configures, and manages Karpenter on your AKS clusters and is based on the open-source [Karpenter](https://karpenter.sh) and [AKS Karpenter provider](https://github.com/Azure/karpenter-provider-azure) projects.

## How does node auto-provisioning work?

Node auto-provisioning provisions, scales, and manages VMs (nodes) in a cluster in response to pending pod pressure.

### Key components of node auto-provisioning

NAP uses the following key components to help manage your cluster's nodes:

| Component | Description |
|---|---|
`NodePool` and `AKSNodeClass` |
Custom Resource Definitions (CRDs) that you create and manage to define node provisioning policies, VM specifications, and constraints for your workloads. |
`NodeClaims` |
Managed by NAP to represent the current state of provisioned nodes that you can monitor. |
| Workload resource requirements | CPU, memory, and other specifications from your Pods, Deployments, Jobs, and other Kubernetes resources that drive provisioning decisions. |

## Kubernetes upgrade behavior for node auto-provisioning nodes

Kubernetes upgrades for node auto-provisioning nodes follow the control plane Kubernetes version. If you perform a cluster upgrade, your nodes are automatically updated to follow the same versioning as your control plane.

We recommend setting a Kubernetes [auto-upgrade](/en-us/azure/aks/auto-upgrade-cluster#cluster-auto-upgrade-channels) channel, which automatically handles Kubernetes upgrades for your cluster. We also recommend setting a [planned maintenance window](planned-maintenance#create-a-maintenance-window) for your cluster. The `aksManagedAutoUpgradeSchedule`

maintenance window allows you to control when to perform cluster upgrades scheduled by your designated auto-upgrade channel. For more information, see [Use planned maintenance to schedule and control upgrades for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Prerequisites

To use node auto-provisioning in AKS, you need the following prerequisites:

- An Azure subscription. If you don't have one, you can create a
[free account](https://azure.microsoft.com/free). - Azure CLI version
`2.76.0`

or later. To find the version, run`az --version`

. For more information about installing or upgrading the Azure CLI, see[Install Azure CLI](/en-us/cli/azure/get-started-with-azure-cli).

## Limitations and unsupported features

The following limitations and unsupported features apply to node auto-provisioning in AKS:

- You can't enable NAP on clusters enabled with the
[cluster autoscaler](cluster-autoscaler). - Windows node pools aren't supported.
- IPv6 clusters aren't supported.
[Service principals](kubernetes-service-principal)aren't supported. You can use either a system-assigned or user-assigned managed identity.[Custom certificate authority (CA) certificates](custom-certificate-authority)aren't supported.- You can't
[stop a cluster](start-stop-cluster)enabled with NAP. [HTTP proxy](http-proxy)isn't supported.- You can't change the
[cluster egress outbound type](egress-outboundtype)after you create a cluster enabled with NAP. - When creating a NAP cluster in a custom virtual network (VNet), you must use a
[Standard Load Balancer](load-balancer-standard). The Basic Load Balancer isn't supported.

## Get started with node auto-provisioning on AKS

The following resources help you get started with node auto-provisioning on AKS:

[Enable or disable node auto-provisioning on an AKS cluster](use-node-auto-provisioning)[Use node auto-provisioning in a custom virtual network](node-auto-provisioning-custom-vnet)[Configure networking for node auto-provisioning on AKS](node-auto-provisioning-networking)[Configure node pools for node auto-provisioning on AKS](node-auto-provisioning-node-pools)[Configure disruption policies for node auto-provisioning on AKS](node-auto-provisioning-disruption)[Upgrade node images for node auto-provisioning on AKS](node-auto-provisioning-upgrade-image)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator -->

# Deploy an AI model on Azure Kubernetes Service (AKS) with the AI toolchain operator add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use the AI toolchain operator add-on to efficiently self-host large language models on Kubernetes, reducing costs and resource complexity, enhancing customization, and maintaining full control over your data.

## About KAITO

Self-hosting large language models (LLMs) on Kubernetes is gaining momentum among organizations with inference workloads at scale, such as batch processing, chatbots, agents, and AI-driven applications. These organizations often have access to commercial-grade GPUs and are seeking alternatives to costly per-token API pricing models, which can quickly scale out of control. Many also require the ability to fine-tune or customize their models, a capability typically restricted by closed-source API providers. Additionally, companies handling sensitive or proprietary data - especially in regulated sectors such as finance, healthcare, or defense - prioritize self-hosting to maintain strict control over data and prevent exposure through third-party systems.

To address these needs and more, the [Kubernetes AI Toolchain Operator (KAITO)](https://github.com/kaito-project/kaito), a Cloud Native Computing Foundation (CNCF) Sandbox project, simplifies the process of deploying and managing open-source LLM workloads on Kubernetes. KAITO integrates with vLLM, a high-throughput inference engine designed to serve large language models efficiently. vLLM as an inference engine helps reduce memory and GPU requirements without significantly compromising accuracy.

Built on top of the open-source KAITO project, the AI toolchain operator managed add-on offers a modular, plug-and-play setup that allows teams to quickly deploy models and expose them via production-ready APIs. It includes built-in features like OpenAI-compatible APIs, prompt formatting, and streaming response support. When deployed on an AKS cluster, KAITO ensures data stays within your organization’s controlled environment, providing a secure, compliant alternative to cloud-hosted LLM APIs.

## Before you begin

- This article assumes a basic understanding of Kubernetes concepts. For more information, see
[Kubernetes core concepts for AKS](concepts-clusters-workloads). - For
and default resource configuration, see the**all hosted model preset images**[KAITO GitHub repository](https://github.com/kaito-project/kaito/tree/main/presets). - The AI toolchain operator add-on currently supports KAITO
**version 0.6.0**, please make a note of this in considering your choice of model from the KAITO model repository.

## Limitations

`AzureLinux`

and`Windows`

OS SKU are not currently supported.- AMD GPU VM sizes are not supported
`instanceType`

in a KAITO workspace. - AI toolchain operator add-on is supported in
**public**Azure regions.

## Prerequisites

If you don't have an Azure subscription, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.If you have multiple Azure subscriptions, make sure you select the correct subscription in which the resources will be created and charged using the

[az account set](/en-us/cli/azure/account#az-account-set)command.Note

Your Azure subscription must have GPU VM quota recommended for your model deployment in the same Azure region as your AKS resources.


Azure CLI version 2.76.0 or later installed and configured. Run

`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The Kubernetes command-line client, kubectl, installed and configured. For more information, see

[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

### Export environment variables

To simplify the configuration steps in this article, you can define environment variables using the following commands. Make sure to replace the placeholder values with your own.

`export AZURE_SUBSCRIPTION_ID="mySubscriptionID" export AZURE_RESOURCE_GROUP="myResourceGroup" export AZURE_LOCATION="myLocation" export CLUSTER_NAME="myClusterName"`


## Enable the AI toolchain operator add-on on an AKS cluster

The following sections describe how to create an AKS cluster with the AI toolchain operator add-on enabled and deploy a default hosted AI model.

### Create an AKS cluster with the AI toolchain operator add-on enabled

Create an Azure resource group using the

[az group create](/en-us/cli/azure/group#az-group-create)command.`az group create --name $AZURE_RESOURCE_GROUP --location $AZURE_LOCATION`

Create an AKS cluster with the AI toolchain operator add-on enabled using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command with the`--enable-ai-toolchain-operator`

and`--enable-oidc-issuer`

flags.`az aks create --location $AZURE_LOCATION \ --resource-group $AZURE_RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-ai-toolchain-operator \ --enable-oidc-issuer \ --generate-ssh-keys`

On an existing AKS cluster, you can enable the AI toolchain operator add-on using the

[az aks update](/en-us/cli/azure/aks#az-aks-update)command.`az aks update --name $CLUSTER_NAME \ --resource-group $AZURE_RESOURCE_GROUP \ --enable-ai-toolchain-operator \ --enable-oidc-issuer`


## Connect to your cluster

Configure

`kubectl`

to connect to your cluster using the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command.`az aks get-credentials --resource-group $AZURE_RESOURCE_GROUP --name $CLUSTER_NAME`

Verify the connection to your cluster using the

`kubectl get`

command.`kubectl get nodes`


## Deploy a default hosted AI model

KAITO offers a range of small to large language models hosted as public container images, which can be deployed in one step using a KAITO workspace. You can browse the preset LLM images available in the [KAITO model registry](https://github.com/kaito-project/kaito/tree/main/presets). In this section, we'll use the high-performant multimodal [Microsoft Phi-4-mini](https://techcommunity.microsoft.com/blog/educatordeveloperblog/welcome-to-the-new-phi-4-models---microsoft-phi-4-mini--phi-4-multimodal/4386037) language model as an example:

Deploy the

[Phi-4-mini instruct](https://huggingface.co/microsoft/Phi-4-mini-instruct)model preset for inference from the KAITO model repository using the`kubectl apply`

command.`kubectl apply -f https://raw.githubusercontent.com/kaito-project/kaito/refs/heads/main/examples/inference/kaito_workspace_phi_4_mini.yaml`

Track the live resource changes in your workspace using the

`kubectl get`

command.`kubectl get workspace workspace-phi-4-mini -w`

Note

As you track the KAITO workspace deployment, note that machine readiness can take up to 10 minutes, and workspace readiness up to 20 minutes depending on the size of your model.

Check your inference service and get the service IP address using the

`kubectl get svc`

command.`export SERVICE_IP=$(kubectl get svc workspace-phi-4-mini -o jsonpath='{.spec.clusterIP}')`

Test the Phi-4-mini instruct inference service with a sample input of your choice using the

[OpenAI chat completions API format](https://platform.openai.com/docs/api-reference/chat):`kubectl run -it --rm --restart=Never curl --image=curlimages/curl -- curl -X POST http://$SERVICE_IP/v1/completions -H "Content-Type: application/json" \ -d '{ "model": "phi-4-mini-instruct", "prompt": "How should I dress for the weather today?", "max_tokens": 10 }'`


## Deploy a custom or domain-specific LLM

Open-source LLMs are often trained in different contexts and domains, and the hosted model presets may not always fit the requirements of your application or data. In this case, KAITO also supports inference deployment of newer or domain-specific language models from [HuggingFace](https://huggingface.co/). Try out a custom model inference deployment with KAITO by following [this article](kaito-custom-inference-model).

## Clean up resources

If you no longer need these resources, you can delete them to avoid incurring extra Azure compute charges.

Delete the KAITO workspace using the

`kubectl delete workspace`

command.`kubectl delete workspace workspace-phi-4-mini`

You need to manually delete the GPU node pools provisioned by the KAITO deployment. Use the node label created by

[Phi-4-mini instruct workspace](https://raw.githubusercontent.com/kaito-project/kaito/refs/heads/main/examples/inference/kaito_workspace_phi_4_mini.yaml)to get the node pool name using thecommand. In this example, the node label is "kaito.sh/workspace": "workspace-phi-4-mini".`az aks nodepool list`

`az aks nodepool list --resource-group $AZURE_RESOURCE_GROUP --cluster-name $CLUSTER_NAME`

[Delete the node pool](delete-node-pool)with this name from your AKS cluster and repeat the steps in this section for each KAITO workspace that will be removed.

## Common troubleshooting scenarios

After applying the KAITO model inference workspace, your resource readiness and workspace conditions might not update to `True`

for the following reasons:

- Your Azure subscription doesn't have quota for the minimum GPU instance type specified in your KAITO workspace. You'll need to
[request a quota increase](/en-us/azure/quotas/quickstart-increase-quota-portal)for the GPU VM family in your Azure subscription. - The GPU instance type isn't available in your AKS region. Confirm the
[GPU instance availability in your specific region](https://azure.microsoft.com/explore/global-infrastructure/products-by-region/?regions=&products=virtual-machines)and switch the Azure region if your GPU VM family isn't available.

## Next steps

Learn more about KAITO model deployment options below:

- Deploy LLMs with your application on AKS using
[KAITO in Visual Studio Code](aks-extension-kaito). [Monitor your KAITO inference workload](ai-toolchain-operator-monitoring).[Fine tune a model](ai-toolchain-operator-fine-tune)with the AI toolchain operator add-on on AKS.- Configure and test
[tool calling with KAITO inference](ai-toolchain-operator-tool-calling). - Integrate an
[MCP server with the AI toolchain operator](ai-toolchain-operator-mcp)add-on on AKS.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-confidential-containers-default-policy -->

# Deploy an AKS cluster with Confidential Containers and an automatically generated policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you use the Azure CLI to deploy an Azure Kubernetes Service (AKS) cluster and configure Confidential Containers (preview) with an automatically generated security policy. You then deploy an application as a Confidential container. To learn more, read the [overview of AKS Confidential Containers](confidential-containers-overview).

In general, getting started with AKS Confidential Containers involves the following steps.

- Deploy or upgrade an AKS cluster using the Azure CLI
- Add an annotation to your pod YAML manifest to mark the pod as using confidential containers
- Add a security policy to your pod YAML manifest
- Deploy your application in confidential computing

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

The Azure CLI version 2.44.1 or later. Run

`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The

`aks-preview`

Azure CLI extension version 0.5.169 or later.The

`confcom`

Confidential Container Azure CLI extension 0.3.3 or later.`confcom`

is required to generate a[security policy](/en-us/azure/confidential-computing/confidential-containers-aks-security-policy).Register the

`Preview`

feature in your Azure subscription.AKS supports Confidential Containers (preview) on version 1.25.0 and higher.

A workload identity and a federated identity credential. The workload identity credential enables Kubernetes applications access to Azure resources securely with a Microsoft Entra ID based on annotated service accounts. If you aren't familiar with Microsoft Entra Workload ID, see the

[Microsoft Entra Workload ID overview](/en-us/azure/active-directory/workload-identities/workload-identities-overview)and review how[Workload Identity works with AKS](workload-identity-overview).The identity you're using to create your cluster has the appropriate minimum permissions. For more information about access and identity for AKS, see

[Access and identity options for Azure Kubernetes Service (AKS)](concepts-identity).To manage a Kubernetes cluster, use the Kubernetes command-line client

[kubectl](https://kubernetes.io/docs/reference/kubectl/). Azure Cloud Shell comes with`kubectl`

. You can install kubectl locally using the[az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli)command.Confidential containers on AKS provide a sidecar open source container for attestation and secure key release. The sidecar integrates with a Key Management Service (KMS), like Azure Key Vault, for releasing a key to the container group after validation is completed. Deploying an

[Azure Key Vault Managed HSM](/en-us/azure/key-vault/managed-hsm/overview)(Hardware Security Module) is optional but recommended to support container-level integrity and attestation. See[Provision and activate a Managed HSM](/en-us/azure/key-vault/managed-hsm/quick-create-cli)to deploy Managed HSM.

### Install the aks-preview Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

To install the aks-preview extension, run the following command:

```
az extension add --name aks-preview
```


Run the following command to update to the latest version of the extension:

```
az extension update --name aks-preview
```


### Install the confcom Azure CLI extension

To install the confcom extension, run the following command:

```
az extension add --name confcom
```


Run the following command to update to the latest version of the extension:

```
az extension update --name confcom
```


### Register the KataCcIsolationPreview feature flag

Register the `KataCcIsolationPreview`

feature flag by using the [az feature register](/en-us/cli/azure/feature#az-feature-register) command, as shown in the following example:

```
az feature register --namespace "Microsoft.ContainerService" --name "KataCcIsolationPreview"
```


It takes a few minutes for the status to show *Registered*. Verify the registration status by using the [az feature show](/en-us/cli/azure/feature#az-feature-show) command:

```
az feature show --namespace "Microsoft.ContainerService" --name "KataCcIsolationPreview"
```


When the status reflects *Registered*, refresh the registration of the *Microsoft.ContainerService* resource provider by using the [az provider register](/en-us/cli/azure/provider#az-provider-register) command:

```
az provider register --namespace "Microsoft.ContainerService"
```


## Deploy a new cluster

Create an AKS cluster using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command and specifying the following parameters:**--os-sku**:*AzureLinux*. Only the Azure Linux os-sku supports this feature in this preview release.**--node-vm-size**: Any Azure VM size that supports AMD SEV-SNP protected child VMs works. For example,[Standard_DC8as_cc_v5](/en-us/azure/virtual-machines/dcasccv5-dcadsccv5-series)VMs.**--enable-workload-identity**: Enables creating a Microsoft Entra Workload ID enabling pods to use a Kubernetes identity.**--enable-oidc-issuer**: Enables OpenID Connect (OIDC) Issuer. It allows a Microsoft Entra ID or other cloud provider identity and access management platform the ability to discover the API server's public signing keys.**--workload-runtime**: Specify*KataCcIsolation*to enable the Confidential Containers feature on the node pool.

`az aks create --resource-group myResourceGroup --name myAKSCluster --kubernetes-version <1.25.0 and above> --os-sku AzureLinux --node-vm-size Standard_DC8as_cc_v5 --workload-runtime KataCcIsolation --node-count 1 --enable-oidc-issuer --enable-workload-identity --generate-ssh-keys`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

When the cluster is ready, get the cluster credentials using the

[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Deploy to an existing cluster

To use this feature with an existing AKS cluster, the following requirements must be met:

- Follow the steps to
[register the KataCcIsolationPreview](#register-the-kataccisolationpreview-feature-flag)feature flag. - Verify the cluster is running Kubernetes version 1.25.0 and higher.
[Enable workload identity](workload-identity-deploy-cluster#deploy-and-configure-microsoft-entra-workload-id-on-an-azure-kubernetes-service-aks-cluster)on the cluster if it isn't already.

Use the following command to enable Confidential Containers (preview) by creating a node pool to host it.

Add a node pool to your AKS cluster using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command. Specify the following parameters:**--resource-group**: Enter the name of an existing resource group to create the AKS cluster in.**--cluster-name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--name**: Enter a unique name for your clusters node pool, such as*nodepool2*.**--workload-runtime**: Specify*KataCcIsolation*to enable the feature on the node pool. Along with the`--workload-runtime`

parameter, these other parameters shall satisfy the following requirements. Otherwise, the command fails and reports an issue with the corresponding parameter(s).**--os-sku**:*AzureLinux*. Only the Azure Linux os-sku supports this feature in this preview release.**--node-vm-size**: Any Azure VM size that supports AMD SEV-SNP protected child VMs nested virtualization works. For example,[Standard_DC8as_cc_v5](/en-us/azure/virtual-machines/dcasccv5-dcadsccv5-series)VMs.

The following example adds a user node pool to

*myAKSCluster*with two nodes in*nodepool2*in the*myResourceGroup*:`az aks nodepool add --resource-group myResourceGroup --name nodepool2 –-cluster-name myAKSCluster --node-count 2 --os-sku AzureLinux --node-vm-size Standard_DC8as_cc_v5 --workload-runtime KataCcIsolation`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

Run the

[az aks update](/en-us/cli/azure/aks#az-aks-update)command to enable Confidential Containers (preview) on the cluster.`az aks update --name myAKSCluster --resource-group myResourceGroup`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

When the cluster is ready, get the cluster credentials using the

[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Configure container

Before you configure access to the Azure Key Vault and secret, and deploy an application as a Confidential container, you need to complete the configuration of the workload identity.

To configure the workload identity, perform the following steps described in the [Deploy and configure workload identity](workload-identity-deploy-cluster) article:

- Retrieve the OIDC Issuer URL
- Create a managed identity
- Create Kubernetes service account
- Establish federated identity credential

Important

You need to set the *environment variables* from the section **Export environmental variables** in the [Deploy and configure workload identity](workload-identity-deploy-cluster) article to continue completing this tutorial. Remember to set the variable `SERVICE_ACCOUNT_NAMESPACE`

to `kafka`

, and execute the command `kubectl create namespace kafka`

before configuring workload identity.

## Deploy a trusted application with kata-cc and attestation container

The following steps configure end-to-end encryption for Kafka messages using encryption keys managed by [Azure Managed Hardware Security Modules](/en-us/azure/key-vault/managed-hsm/overview) (mHSM). The key is only released when the Kafka consumer runs within a Confidential Container with an Azure attestation secret provisioning container injected in to the pod.

This configuration is based on the following four components:

- Kafka Cluster: A simple Kafka cluster deployed in the Kafka namespace on the cluster.
- Kafka Producer: A Kafka producer running as a vanilla Kubernetes pod that sends encrypted user-configured messages using a public key to a Kafka topic.
- Kafka Consumer: A Kafka consumer pod running with the kata-cc runtime, equipped with a secure key release container to retrieve the private key for decrypting Kafka messages and render the messages to web UI.

For this preview release, we recommend for test and evaluation purposes to either create or use an existing Azure Key Vault Premium tier resource to support storing keys in a hardware security module (HSM). We don't recommend using your production key vault. If you don't have an Azure Key Vault, see [Create a key vault using the Azure CLI](/en-us/azure/key-vault/general/quick-create-cli).

Grant the managed identity you created earlier, and your account, access to the key vault.

[Assign](/en-us/azure/key-vault/general/rbac-guide#assign-role)both identities the**Key Vault Crypto Officer**and**Key Vault Crypto User**Azure RBAC roles.Note

The managed identity is the value you assign to the

`USER_ASSIGNED_IDENTITY_NAME`

variable.To add role assignments, you must have

`Microsoft.Authorization/roleAssignments/write`

and`Microsoft.Authorization/roleAssignments/delete`

permissions, such as[Key Vault Data Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#key-vault-data-access-administrator),[User Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator), or[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner).You must use the Key Vault Premium SKU to support HSM-protected keys.


Run the following command to set the scope:

`AKV_SCOPE=$(az keyvault show --name <AZURE_AKV_RESOURCE_NAME> --query id --output tsv)`

Run the following command to assign the

**Key Vault Crypto Officer**role.`az role assignment create --role "Key Vault Crypto Officer" --assignee "${USER_ASSIGNED_IDENTITY_NAME}" --scope $AKV_SCOPE`

Run the following command to assign the

**Key Vault Crypto User**role.`az role assignment create --role "Key Vault Crypto User" --assignee "${USER_ASSIGNED_IDENTITY_NAME}" --scope $AKV_SCOPE`

Install the Kafka cluster in the kafka namespace by running the following command:

`kubectl create -f 'https://strimzi.io/install/latest?namespace=kafka' -n kafka`

Run the following command to apply the

`kafka`

cluster CR file.`kubectl apply -f https://strimzi.io/examples/latest/kafka/kafka-persistent-single.yaml -n kafka`

Prepare the RSA Encryption/Decryption key using the

[bash script](https://github.com/microsoft/confidential-container-demos/raw/main/kafka/setup-key.sh)for the workload from GitHub. Save the file as`setup-key.sh`

.Set the

`MAA_ENDPOINT`

environment variable with the FQDN of Attest URI by running the following command.`export MAA_ENDPOINT="$(az attestation show --name "myattestationprovider" --resource-group "MyResourceGroup" --query 'attestUri' -o tsv | cut -c 9-)"`

Check if the FQDN of Attest URI is in correct format (the MAA_ENDPOINT should not include the prefix "https://"):

`echo $MAA_ENDPOINT`

Note

To set up Microsoft Azure Attestation, see

[Quickstart: Set up Azure Attestation with Azure CLI](/en-us/azure/attestation/quickstart-azure-cli).Copy the following YAML manifest and save it as

`consumer.yaml`

.`apiVersion: v1 kind: Pod metadata: name: kafka-golang-consumer namespace: kafka labels: azure.workload.identity/use: "true" app.kubernetes.io/name: kafka-golang-consumer spec: serviceAccountName: workload-identity-sa runtimeClassName: kata-cc-isolation containers: - image: "mcr.microsoft.com/aci/skr:2.7" imagePullPolicy: Always name: skr env: - name: SkrSideCarArgs value: ewogICAgImNlcnRjYWNoZSI6IHsKCQkiZW5kcG9pbnRfdHlwZSI6ICJMb2NhbFRISU0iLAoJCSJlbmRwb2ludCI6ICIxNjkuMjU0LjE2OS4yNTQvbWV0YWRhdGEvVEhJTS9hbWQvY2VydGlmaWNhdGlvbiIKCX0gIAp9 command: - /bin/skr volumeMounts: - mountPath: /opt/confidential-containers/share/kata-containers/reference-info-base64 name: endor-loc - image: "mcr.microsoft.com/acc/samples/kafka/consumer:1.0" imagePullPolicy: Always name: kafka-golang-consumer env: - name: SkrClientKID value: kafka-encryption-demo - name: SkrClientMAAEndpoint value: sharedeus2.eus2.test.attest.azure.net - name: SkrClientAKVEndpoint value: "myKeyVault.vault.azure.net" - name: TOPIC value: kafka-demo-topic command: - /consume ports: - containerPort: 3333 name: kafka-consumer resources: limits: memory: 1Gi cpu: 200m volumes: - name: endor-loc hostPath: path: /opt/confidential-containers/share/kata-containers/reference-info-base64 --- apiVersion: v1 kind: Service metadata: name: consumer namespace: kafka spec: type: LoadBalancer selector: app.kubernetes.io/name: kafka-golang-consumer ports: - protocol: TCP port: 80 targetPort: kafka-consumer`

Note

Update the value for the pod environment variable

`SkrClientAKVEndpoint`

to match the URL of your Azure Key Vault, excluding the protocol value`https://`

. The current value placeholder value is`myKeyVault.vault.azure.net`

. Update the value for the pod environment variable`SkrClientMAAEndpoint`

with the value of`MAA_ENDPOINT`

. You can find the value of`MAA_ENDPOINT`

by running the command`echo $MAA_ENDPOINT`

or the command`az attestation show --name "myattestationprovider" --resource-group "MyResourceGroup" --query 'attestUri' -o tsv | cut -c 9-`

.Generate the security policy for the Kafka consumer YAML manifest and obtain the hash of the security policy stored in the

`WORKLOAD_MEASUREMENT`

variable by running the following command:`export WORKLOAD_MEASUREMENT=$(az confcom katapolicygen -y consumer.yaml --print-policy | base64 -d | sha256sum | cut -d' ' -f1)`

To generate an RSA asymmetric key pair (public and private keys), run the

`setup-key.sh`

script using the following command. The`<Azure Key Vault URL>`

value should be`<your-unique-keyvault-name>.vault.azure.net`

`export MANAGED_IDENTITY=${USER_ASSIGNED_CLIENT_ID} bash setup-key.sh "kafka-encryption-demo" <Azure Key Vault URL>`

Note

The envionment variable

`MANAGED_IDENTITY`

is required by the bash script`setup-key.sh`

.The public key will be saved as

`kafka-encryption-demo-pub.pem`

after executing the bash script.

Important

If you receive the error

`ForbiddenByRbac`

,you might need to wait up to 24 hours as the backend services for managed identities maintain a cache per resource URI for up to 24 hours. See also:[Troubleshoot Azure RBAC](/en-us/azure/role-based-access-control/troubleshooting#symptom---role-assignment-changes-are-not-being-detected).To verify the keys have been successfully uploaded to the key vault, run the following commands:

`az account set --subscription <Subscription ID> az keyvault key list --vault-name <KeyVault Name> -o table`

Copy the following YAML manifest and save it as

`producer.yaml`

.`apiVersion: v1 kind: Pod metadata: name: kafka-producer namespace: kafka spec: containers: - image: "mcr.microsoft.com/acc/samples/kafka/producer:1.0" name: kafka-producer command: - /produce env: - name: TOPIC value: kafka-demo-topic - name: MSG value: "Azure Confidential Computing" - name: PUBKEY value: |- -----BEGIN PUBLIC KEY----- MIIBojAN***AE= -----END PUBLIC KEY----- resources: limits: memory: 1Gi cpu: 200m`

Note

Update the value which begin with

`-----BEGIN PUBLIC KEY-----`

and ends with`-----END PUBLIC KEY-----`

strings with the content from`kafka-encryption-demo-pub.pem`

which was created in the previous step.Deploy the

`consumer`

and`producer`

YAML manifests using the files you saved earlier.`kubectl apply -f consumer.yaml`

`kubectl apply -f producer.yaml`

Get the IP address of the web service using the following command:

`kubectl get svc consumer -n kafka`

Copy and paste the external IP address of the consumer service into your browser and observe the decrypted message.

The following example resembles the output of the command:

`Welcome to Confidential Containers on AKS! Encrypted Kafka Message: Msg 1: Azure Confidential Computing`

You should also attempt to run the consumer as a regular Kubernetes pod by removing the

`skr container`

and`kata-cc runtime class`

spec. Since you aren't running the consumer with kata-cc runtime class, you no longer need the policy.Remove the entire policy and observe the messages again in the browser after redeploying the workload. Messages appear as base64-encoded ciphertext because the private encryption key can't be retrieved. The key can't be retrieved because the consumer is no longer running in a confidential environment, and the

`skr container`

is missing, preventing decryption of messages.

## Cleanup

When you're finished evaluating this feature, to avoid Azure charges, clean up your unnecessary resources. If you deployed a new cluster as part of your evaluation or testing, you can delete the cluster using the [az aks delete](/en-us/cli/azure/aks#az-aks-delete) command.

```
az aks delete --resource-group myResourceGroup --name myAKSCluster
```


If you enabled Confidential Containers (preview) on an existing cluster, you can remove the pod(s) using the [kubectl delete pod](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#delete) command.

```
kubectl delete pod pod-name
```


## Next steps

- Learn more about
[Azure Dedicated hosts](/en-us/azure/virtual-machines/dedicated-hosts)for nodes with your AKS cluster to use hardware isolation and control over Azure platform maintenance events.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-apply-l7-policies -->

# Set up Layer 7(L7) policies with Advanced Container Networking Services

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article demonstrates how to set up L7 policies with Advanced Container Networking Services in AKS clusters. Continue only after you have reviewed the limitations and considerations listed on the [Layer 7 Policy Overview](container-network-security-l7-policy-concepts) page.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of Azure CLI required for the steps in this article is 2.79.0. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Install the `aks-preview`

Azure CLI extension

Install or update the Azure CLI preview extension using the [ az extension add](/en-us/cli/azure/extension#az-extension-add) or

[command.](/en-us/cli/azure/extension#az-extension-update)

`az extension update`

The minimum version of the aks-preview Azure CLI extension is `14.0.0b6`


```
# Install the aks-preview extension
az extension add --name aks-preview
# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```


### Register the `AdvancedNetworkingL7PolicyPreview`

feature flag

Register the `AdvancedNetworkingL7PolicyPreview`

feature flag using the [ az feature register](/en-us/cli/azure/feature#az-feature-register) command.

```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"
```


Verify successful registration using the [ az feature show](/en-us/cli/azure/feature#az-feature-show) command. It takes a few minutes for the registration to complete.

```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"
```


Once the feature shows `Registered`

, refresh the registration of the `Microsoft.ContainerService`

resource provider using the [ az provider register](/en-us/cli/azure/provider#az-provider-register) command.

### Enable Advanced Container Networking Services

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. These features encompass:

**Container Network Observability:**Provides insights into your network traffic. To learn more visit[Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability).**Container Network Security:**Offers security features like Fully Qualified Domain Name (FQDN) filtering. To learn more visit[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security).

Note

Clusters with the Cilium data plane support Container Network Observability and Container Network security starting with Kubernetes version 1.29.

For this demo, the `--acns-advanced-networkpolicies`

parameter must be set to "L7" to enable L7 policies. Setting this parameter to "L7" also enables FQDN filtering. If you only want to enable FQDN filtering, set the parameter to "FQDN". To disable both features, you can follow the instructions provided in [Disable Container Network Security](advanced-container-networking-services-overview).

```
export CLUSTER_NAME="<aks-cluster-name>"
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--network-plugin azure \
--network-dataplane cilium \
--enable-acns \
--acns-advanced-networkpolicies L7
```


### Enable Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the Advanced Container Networking Services flag,

`--enable-acns`

, updates an existing AKS cluster with all Advanced Container Networking Services features which includes [Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability)and the

[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security)feature.

Note

Only clusters with the Cilium data plane support Container Network Security features of Advanced Container Networking Services.

For this demo, the `--acns-advanced-networkpolicies`

parameter must be set to "L7" to enable L7 policies. Setting this parameter to "L7" also enables FQDN filtering. If you only want to enable FQDN filtering, set the parameter to "FQDN". To disable both features, you can follow the instructions provided in [Disable Container Network Security](advanced-container-networking-services-overview).

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns \
--acns-advanced-networkpolicies L7
```


## Get cluster credentials

Get your cluster credentials using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Set up http-server application on your AKS cluster

Apply the below YAML to your AKS cluster to set up the `http-server`

application.

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: http-server
labels:
app: http-server
spec:
replicas: 1
selector:
matchLabels:
app: http-server
template:
metadata:
labels:
app: http-server
spec:
containers:
- name: http-server
image: nginx:latest
ports:
- containerPort: 8080
volumeMounts:
- name: config-volume
mountPath: /etc/nginx/conf.d
volumes:
- name: config-volume
configMap:
name: nginx-config
---
apiVersion: v1
kind: Service
metadata:
name: http-server
spec:
selector:
app: http-server
ports:
- protocol: TCP
port: 80
targetPort: 8080
---
apiVersion: v1
kind: ConfigMap
metadata:
name: nginx-config
data:
default.conf: |
server {
listen 8080;
location / {
return 200 "Hello from the server root!\n";
}
location /products {
return 200 "Listing products...\n";
}
}
```


## Set up http-client application on your AKS Cluster

Apply the below YAML to your AKS cluster to set up the `http-client`

application.

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: http-client
labels:
app: http-client
spec:
replicas: 1
selector:
matchLabels:
app: http-client
template:
metadata:
labels:
app: http-client
spec:
containers:
- name: http-client
image: curlimages/curl:latest
command: ["sleep", "infinity"]
```


## Test connectivity with a policy

Next, apply the following Layer 7 policy to allow only `GET`

requests from the `http-client`

application to the `/products`

endpoint on the `http-server`

:

```
apiVersion: cilium.io/v2
kind: CiliumNetworkPolicy
metadata:
name: allow-get-products
spec:
description: "Allow only GET requests to /products from http-client to http-server"
endpointSelector:
matchLabels:
app: http-server
ingress:
- fromEndpoints:
- matchLabels:
app: http-client
toPorts:
- ports:
- port: "8080"
protocol: TCP
rules:
http:
- method: "GET"
path: "/products"
```


### Verify policy

To verify the policy's enforcement, execute these commands from the `http-client`

pod:

```
kubectl exec -it <your-http-client-pod-name> -n default -- curl -v http://http-server:80/products
```


You should expect an output like `Listing products...`

when you run the above command

```
kubectl exec -it <your-http-client-pod-name> -n default -- curl -v -XPOST http://http-server:80/products -d "test=data"
```


You should expect an output like `Access Denied`

when you run the above command

### Observing L7 metrics

If you have Advanced Container Network Service's container network observability enabled, you can visualize the traffic on Grafana.

To simplify the analysis of these L7 metrics, we provide preconfigured Azure Managed Grafana dashboards. You can find them under the **Dashboards > Azure Managed Prometheus** folder, with filenames like **"Kubernetes/Networking/L7 (Namespace)"** and **"Kubernetes/Networking/L7 (Workload)"**.

You should see metrics similar to the following:

## Clean up resources

If you don't plan on using this application, delete the other resources you created in this article using the [ az group delete](/en-us/cli/azure/#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP
```


## Next steps

In this how-to article, you learned how to enable and apply L7 Policies with Advanced Container Networking Services for your AKS cluster.

- For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see
[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/confidential-containers-overview -->

# Confidential Containers (preview) with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Confidential Containers preview is set to sunset in **March 2026**. After this date, customers with existing Confidential Container node pools should expect to see reduced functionality, and you won't be able to spin up any new nodes with the `KataCcIsolation`

runtime. Customers currently using Confidential Container node pools can continue using them as normal. If you want to move off Confidential Containers, consider the following alternatives:

[Confidential VMs on AKS](/en-us/azure/confidential-computing/confidential-node-pool-aks): Offers a similar hardware-based TEE that leverages AMD SEV-SNP security features, without the addition of per-VM isolation for workloads seen in Confidential Containers.[Application enclave support](/en-us/azure/confidential-computing/confidential-nodes-aks-overview): Provides users with Intel SGX confidential computing VM nodes that support hardware-based, process-level container isolation through the Intel SGX trusted execution environment.[Confidential Containers on Azure Container Instances](/en-us/azure/confidential-computing/confidential-containers): Allows for lift-and-shift deployments on containers backed by AMD SEV-SNP. Functionality includes performing full guest attestation, access to toolings to generate policies, and utilizing sidecar containers for secure key releases. ACI nodes can be run on AKS via[virtual nodes](/en-us/azure/container-instances/container-instances-virtual-nodes).[Azure RedHat OpenShift Confidential Containers](/en-us/azure/openshift/confidential-containers-overview): Offers a similar AMD SEV-SNP backed TEE and utilizes the Kata runtime for per-container level isolation.[Open source Confidential Containers](https://github.com/confidential-containers): Gives a similar AMD SEV-SNP backed TEE that comes with per-container isolation through Kata.

If you have additional questions, please create a [support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest) or post an issue in [AKS issues](https://github.com/Azure/AKS/issues).

Confidential Containers provide a set of features and capabilities to further secure your standard container workloads to achieve higher data security, data privacy and runtime code integrity goals. Azure Kubernetes Service (AKS) includes Confidential Containers (preview) on AKS.

Confidential Containers builds on Kata Confidential Containers and hardware-based encryption to encrypt container memory. It establishes a new level of data confidentiality by preventing data in memory during computation from being in clear text, readable format. Trust is earned in the container through hardware attestation, allowing access to the encrypted data by trusted entities.

Together with [Pod Sandboxing](use-pod-sandboxing), you can run sensitive workloads isolated in Azure to protect your data and workloads. What makes a container confidential:

- Transparency: The confidential container environment where your sensitive application is shared, you can see and verify if it's safe. All components of the Trusted Computing Base (TCB) are to be open sourced.
- Auditability: You have the ability to verify and see what version of the CoCo environment package including Linux Guest OS and all the components are current. Microsoft signs to the guest OS and container runtime environment for verifications through attestation. It also releases a secure hash algorithm (SHA) of guest OS builds to build a string audibility and control story.
- Full attestation: Anything that is part of the TEE shall be fully measured by the CPU with ability to verify remotely. The hardware report from AMD SEV-SNP processor shall reflect container layers and container runtime configuration hash through the attestation claims. Application can fetch the hardware report locally including the report that reflects Guest OS image and container runtime.
- Code integrity: Runtime enforcement is always available through customer defined policies for containers and container configuration, such as immutable policies and container signing.
- Isolation from operator: Security designs that assume least privilege and highest isolation shielding from all untrusted parties including customer/tenant admins. It includes hardening existing Kubernetes control plane access (kubelet) to confidential pods.

With other security measures or data protection controls, as part of your overall architecture, these capabilities help you meet regulatory, industry, or governance compliance requirements for securing sensitive information.

This article helps you understand the Confidential Containers feature, and how to implement and configure the following:

- Deploy or upgrade an AKS cluster using the Azure CLI
- Add an annotation to your pod YAML to mark the pod as being run as a confidential container
- Add a
[security policy](/en-us/azure/confidential-computing/confidential-containers-aks-security-policy)to your pod YAML - Deploy your application in confidential computing

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Supported scenarios

Confidential Containers (preview) are appropriate for deployment scenarios that involve sensitive data. For example, personally identifiable information (PII) or any data with strong security needed for regulatory compliance. Some common scenarios with containers are:

- Run big data analytics using Apache Spark for fraud pattern recognition in the financial sector.
- Running self-hosted GitHub runners to securely sign code as part of Continuous Integration and Continuous Deployment (CI/CD) DevOps practices.
- Machine Learning inferencing and training of ML models using an encrypted data set from a trusted source. It only decrypts inside a confidential container environment to preserve privacy.
- Building big data clean rooms for ID matching as part of multi-party computation in industries like retail with digital advertising.
- Building confidential computing Zero Trust landing zones to meet privacy regulations for application migrations to cloud.

## Considerations

The following are considerations with this preview of Confidential Containers:

- An increase in pod startup time compared to runc pods and kernel-isolated pods.
- Version 1 container images aren't supported.
- Ephemeral containers and other troubleshooting methods like
`exec`

into a container, log outputs from containers, and`stdio`

require a policy modification and redeployment to enable ExecProcessRequest, ReadStreamRequest, WriteStreamRequest, and CloseStdinRequest. - Due to container image layer measurements being encoded in the security policy, we don't recommend using the
`latest`

tag when specifying containers. - Services, Load Balancers, and EndpointSlices only support the TCP protocol.
- The policy generator only supports pods that use IPv4 addresses.
- Pod environment variables based on ConfigMaps and Secrets can't be changed after the pod is deployed.
- Pod termination logs aren't supported. While pods write termination logs to
`/dev/termination-log`

or to a custom location if specified in the pod manifest, the host/kubelet can't read those logs. Changes from the pod to that file aren't reflected on the host. - Confidential Containers currently only supports Azure Linux.

## Resource allocation overview

It's important you understand the memory and processor resource allocation behavior in this release.

- CPU: The shim assigns one vCPU to the base OS inside the pod. If no resource
`limits`

are specified, the workloads don't have separate CPU shares assigned, the vCPU is then shared with that workload. If CPU limits are specified, CPU shares are explicitly allocated for workloads. - Memory: The Kata-CC handler uses 2 GB memory for the UVM OS and X MB additional memory where X is the resource
`limits`

if specified in the YAML manifest (resulting in a 2-GB VM when no limit is given, without implicit memory for containers). The[Kata](https://katacontainers.io/docs/)handler uses 256 MB base memory for the UVM OS and X MB additional memory when resource`limits`

are specified in the YAML manifest. If limits are unspecified, an implicit limit of 1,792 MB is added resulting in a 2 GB VM and 1,792 MB implicit memory for containers.

In this release, specifying resource requests in the pod manifests isn't supported. containerd doesn't pass the requests to the Kata Shim, and as a result, reserving resources based on the pod manifest resource requests is not implemented. Use resource `limits`

instead of resource `requests`

to allocate memory or CPU resources for workloads or containers.

With the local container filesystem backed by VM memory, writing to the container filesystem (including logging) can fill up the available memory provided to the pod. This condition can result in potential pod crashes.

## Next steps

- See the overview of
[Confidential Containers security policy](/en-us/azure/confidential-computing/confidential-containers-aks-security-policy)to learn about how workloads and their data in a pod is protected. [Deploy Confidential Containers on AKS](deploy-confidential-containers-default-policy)with an automatically generated security policy.- Learn more about
[Azure Dedicated hosts](/en-us/azure/virtual-machines/dedicated-hosts)for nodes with your AKS cluster to use hardware isolation and control over Azure platform maintenance events.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/configure-kubenet -->

# Use kubenet networking with your own IP address ranges in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

On **31 March 2028**, kubenet networking for Azure Kubernetes Service (AKS) will be retired.

To avoid service disruptions, **you'll need to** [upgrade to Azure Container Networking Interface (CNI) overlay](/en-us/azure/aks/upgrade-aks-ipam-and-dataplane#upgrade-an-existing-cluster-to-azure-cni-overlay) **before that date**, when workloads running on kubenet for AKS will no longer be supported.

AKS clusters use kubenet and create an Azure virtual network and subnet for you by default. With kubenet, nodes get an IP address from the Azure virtual network subnet. Pods receive an IP address from a logically different address space to the Azure virtual network subnet of the nodes. Network address translation (NAT) is then configured so the pods can reach resources on the Azure virtual network. The source IP address of the traffic is NAT'd to the node's primary IP address. This approach greatly reduces the number of IP addresses you need to reserve in your network space for pods to use.

With [Azure Container Networking Interface (CNI)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md), every pod gets an IP address from the subnet and can be accessed directly. These IP addresses must be planned in advance and unique across your network space. Each node has a configuration parameter for the maximum number of pods it supports. The equivalent number of IP addresses per node are then reserved up front for that node. This approach requires more planning, and often leads to IP address exhaustion or the need to rebuild clusters in a larger subnet as your application demands grow. You can configure the maximum pods deployable to a node at cluster creation time or when creating new node pools. If you don't specify `maxPods`

when creating new node pools, you receive a default value of *110* for kubenet.

This article shows you how to use kubenet networking to create and use a virtual network subnet for an AKS cluster. For more information on network options and considerations, see [Network concepts for Kubernetes and AKS](concepts-network).

## Prerequisites

- The virtual network for the AKS cluster must allow outbound internet connectivity.
- Don't create more than one AKS cluster in the same subnet.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for the Kubernetes service address range, pod address range, or cluster virtual network address range. The range can't be updated after you create your cluster. - The cluster identity used by the AKS cluster must at least have the
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)role on the subnet within your virtual network. CLI helps set the role assignment automatically. If you're using an ARM template or other clients, you need to manually set the role assignment. You must also have the appropriate permissions, such as the subscription owner, to create a cluster identity and assign it permissions. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, you need the following permissions:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


Warning

To use Windows Server node pools, you must use Azure CNI. The kubenet network model isn't available for Windows Server containers.

## Before you begin

You need the Azure CLI version 2.0.65 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Overview of kubenet networking with your own subnet

In many environments, you have defined virtual networks and subnets with allocated IP address ranges, and you use these resources to support multiple services and applications. To provide network connectivity, AKS clusters can use *kubenet* (basic networking) or Azure CNI (*advanced networking*).

With *kubenet*, only the nodes receive an IP address in the virtual network subnet. Pods can't communicate directly with each other. Instead, User Defined Routing (UDR) and IP forwarding handle connectivity between pods across nodes. UDRs and IP forwarding configuration is created and maintained by the AKS service by default, but you can [bring your own route table for custom route management](#bring-your-own-subnet-and-route-table-with-kubenet) if you want. You can also deploy pods behind a service that receives an assigned IP address and load balances traffic for the application. The following diagram shows how the AKS nodes receive an IP address in the virtual network subnet, but not the pods:

Azure supports a maximum of *400* routes in a UDR, so you can't have an AKS cluster larger than 400 nodes. AKS [virtual nodes](virtual-nodes-cli) and Azure Network Policies aren't supported with *kubenet*. [Calico Network Policies](https://docs.projectcalico.org/v3.9/security/calico-network-policy) are supported.

With *Azure CNI*, each pod receives an IP address in the IP subnet and can communicate directly with other pods and services. Your clusters can be as large as the IP address range you specify. However, you must plan the IP address range in advance, and all the IP addresses are consumed by the AKS nodes based on the maximum number of pods they can support. Advanced network features and scenarios such as [virtual nodes](virtual-nodes-cli) or Network Policies (either Azure or Calico) are supported with *Azure CNI*.

### Limitations & considerations for kubenet

- An additional hop is required in the design of kubenet, which adds minor latency to pod communication.
- Route tables and user-defined routes are required for using kubenet, which adds complexity to operations.
- For more information, see
[Customize cluster egress with a user-defined routing table in AKS](egress-udr)and[Customize cluster egress with outbound types in AKS](egress-outboundtype).

- For more information, see
- Direct pod addressing isn't supported for kubenet due to kubenet design.
- Unlike Azure CNI clusters, multiple kubenet clusters can't share a subnet.
- AKS doesn't apply Network Security Groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure the security rules in the NSGs allow traffic between the node and pod CIDR. For more details, see
[Network security groups](concepts-network#network-security-groups). - Features
**not supported on kubenet**include:

Note

Some of the system pods such as **konnectivity** within the cluster use the host node IP address rather than an IP from the overlay address space. The system pods will only use the node IP and not an IP address from the virtual network.

### IP address availability and exhaustion

A common issue with *Azure CNI* is that the assigned IP address range is too small to then add more nodes when you scale or upgrade a cluster. The network team also might not be able to issue a large enough IP address range to support your expected application demands.

As a compromise, you can create an AKS cluster that uses *kubenet* and connect to an existing virtual network subnet. This approach lets the nodes receive defined IP addresses without the need to reserve a large number of IP addresses up front for any potential pods that could run in the cluster. With *kubenet*, you can use a much smaller IP address range and support large clusters and application demands. For example, with a */27* IP address range on your subnet, you can run a 20-25 node cluster with enough room to scale or upgrade. This cluster size can support up to *2,200-2,750* pods (with a default maximum of 110 pods per node). The maximum number of pods per node that you can configure with *kubenet* in AKS is 250.

The following basic calculations compare the difference in network models:

**kubenet**: A simple*/24*IP address range can support up to*251*nodes in the cluster. Each Azure virtual network subnet reserves the first three IP addresses for management operations. This node count can support up to*27,610*pods, with a default maximum of 110 pods per node.**Azure CNI**: That same basic*/24*subnet range can only support a maximum of*eight*nodes in the cluster. This node count can only support up to*240*pods, with a default maximum of 30 pods per node.

Note

These maximums don't take into account upgrade or scale operations. In practice, you can't run the maximum number of nodes the subnet IP address range supports. You must leave some IP addresses available for scaling or upgrading operations.

### Virtual network peering and ExpressRoute connections

To provide on-premises connectivity, both *kubenet* and *Azure-CNI* network approaches can use [Azure virtual network peering](/en-us/azure/virtual-network/virtual-network-peering-overview) or [ExpressRoute connections](/en-us/azure/expressroute/expressroute-introduction). Plan your IP address ranges carefully to prevent overlap and incorrect traffic routing. For example, many on-premises networks use a *10.0.0.0/8* address range that's advertised over the ExpressRoute connection. We recommend creating your AKS clusters in Azure virtual network subnets outside this address range, such as *172.16.0.0/16*.

### Choose a network model to use

The following considerations help outline when each network model may be the most appropriate:

**Use kubenet when**:

- You have limited IP address space.
- Most of the pod communication is within the cluster.
- You don't need advanced AKS features, such as virtual nodes or Azure Network Policy.

**Use Azure CNI when**:

- You have available IP address space.
- Most of the pod communication is to resources outside of the cluster.
- You don't want to manage user defined routes for pod connectivity.
- You need AKS advanced features, such as virtual nodes or Azure Network Policy.

For more information to help you decide which network model to use, see [Compare network models and their support scope](concepts-network-cni-overview).

## Create a virtual network and subnet

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

If you don't have an existing virtual network and subnet to use, create these network resources using the

command. The following example command creates a virtual network named`az network vnet create`

*myAKSVnet*with the address prefix of*192.168.0.0/16*and a subnet named*myAKSSubnet*with the address prefix*192.168.1.0/24*:`az network vnet create \ --resource-group myResourceGroup \ --name myAKSVnet \ --address-prefixes 192.168.0.0/16 \ --subnet-name myAKSSubnet \ --subnet-prefix 192.168.1.0/24 \ --location eastus`

Get the subnet resource ID using the

command and store it as a variable named`az network vnet subnet show`

`SUBNET_ID`

for later use.`SUBNET_ID=$(az network vnet subnet show --resource-group myResourceGroup --vnet-name myAKSVnet --name myAKSSubnet --query id -o tsv)`


## Create an AKS cluster in the virtual network

### Create an AKS cluster with system-assigned managed identities

Note

When using system-assigned identity, the Azure CLI grants the Network Contributor role to the system-assigned identity after the cluster is created. If you're using an ARM template or other clients, you need to use the [user-assigned managed identity](configure-kubenet#create-an-aks-cluster-with-user-assigned-managed-identity) instead.

Create an AKS cluster with system-assigned managed identities using the

command.`az aks create`

`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --network-plugin kubenet \ --service-cidr 10.0.0.0/16 \ --dns-service-ip 10.0.0.10 \ --pod-cidr 10.244.0.0/16 \ --vnet-subnet-id $SUBNET_ID \ --generate-ssh-keys`

Deployment parameters:

*--service-cidr*is optional. This address is used to assign internal services in the AKS cluster an IP address. This IP address range should be an address space that isn't in use elsewhere in your network environment, including any on-premises network ranges if you connect, or plan to connect, your Azure virtual networks using Express Route or a Site-to-Site VPN connection. The default value is 10.0.0.0/16.*--dns-service-ip*is optional. The address should be the*.10*address of your service IP address range. The default value is 10.0.0.10.*--pod-cidr*is optional. This address should be a large address space that isn't in use elsewhere in your network environment. This range includes any on-premises network ranges if you connect, or plan to connect, your Azure virtual networks using Express Route or a Site-to-Site VPN connection. The default value is 10.244.0.0/16.- This address range must be large enough to accommodate the number of nodes that you expect to scale up to. You can't change this address range once the cluster is deployed.
- The pod IP address range is used to assign a
*/24*address space to each node in the cluster. In the following example, the*--pod-cidr*of*10.244.0.0/16*assigns the first node*10.244.0.0/24*, the second node*10.244.1.0/24*, and the third node*10.244.2.0/24*. - As the cluster scales or upgrades, the Azure platform continues to assign a pod IP address range to each new node.


### Create an AKS cluster with user-assigned managed identity

#### Create a managed identity

Create a managed identity using the

command. If you have an existing managed identity, find the principal ID using the`az identity`

`az identity show --ids <identity-resource-id>`

command instead.`az identity create --name myIdentity --resource-group myResourceGroup`

Your output should resemble the following example output:

`{ "clientId": "<client-id>", "clientSecretUrl": "<clientSecretUrl>", "id": "/subscriptions/<subscriptionid>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myIdentity", "location": "westus2", "name": "myIdentity", "principalId": "<principal-id>", "resourceGroup": "myResourceGroup", "tags": {}, "tenantId": "<tenant-id>", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


#### Add role assignment for managed identity

If you're using the Azure CLI, the role is automatically added and you can skip this step. If you're using an ARM template or other clients, you need to use the Principal ID of the cluster managed identity to perform a role assignment.

Get the virtual network resource ID using the

command and store it as a variable named`az network vnet show`

`VNET_ID`

.`VNET_ID=$(az network vnet show --resource-group myResourceGroup --name myAKSVnet --query id -o tsv)`

Assign the managed identity for your AKS cluster

*Network Contributor*permissions on the virtual network using thecommand and provide the`az role assignment create`

*<principalId>*.`az role assignment create --assignee <control-plane-identity-principal-id> --scope $VNET_ID --role "Network Contributor" # Example command az role assignment create --assignee 22222222-2222-2222-2222-222222222222 --scope "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myAKSVnet" --role "Network Contributor"`


Note

Permission granted to your cluster's managed identity used by Azure may take up 60 minutes to populate.

#### Create an AKS cluster

Create an AKS cluster using the

command and provide the control plane's managed identity resource ID for the`az aks create`

`assign-identity`

argument to assign the user-assigned managed identity.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 3 \ --network-plugin kubenet \ --vnet-subnet-id $SUBNET_ID \ --assign-identity <identity-resource-id> \ --generate-ssh-keys`


When you create an AKS cluster, a network security group and route table are automatically created. These network resources are managed by the AKS control plane. The network security group is automatically associated with the virtual NICs on your nodes. The route table is automatically associated with the virtual network subnet. Network security group rules and route tables are automatically updated as you create and expose services.

## Bring your own subnet and route table with kubenet

With kubenet, a route table must exist on your cluster subnet(s). AKS supports bringing your own existing subnet and route table. If your custom subnet doesn't contain a route table, AKS creates one for you and adds rules throughout the cluster lifecycle. If your custom subnet contains a route table when you create your cluster, AKS acknowledges the existing route table during cluster operations and adds/updates rules accordingly for cloud provider operations.

Warning

You can add/update custom rules on the custom route table. However, rules are added by the Kubernetes cloud provider which can't be updated or removed. Rules such as *0.0.0.0/0* generally exist on a given route table (unless the egress outbound type is `none`

) and map to the target of your internet gateway, such as an NVA or other egress gateway. Take caution when updating rules.

Learn more about setting up a [custom route table](/en-us/azure/virtual-network/manage-route-table).

Kubenet networking requires organized route table rules to successfully route requests. Due to this design, route tables must be carefully maintained for each cluster that relies on it. Multiple clusters can't share a route table because pod CIDRs from different clusters might overlap which causes unexpected and broken routing scenarios. When configuring multiple clusters on the same virtual network or dedicating a virtual network to each cluster, consider the following limitations:

- A custom route table must be associated to the subnet before you create the AKS cluster.
- The associated route table resource can't be updated after cluster creation. However, custom rules can be modified on the route table.
- Each AKS cluster must use a single, unique route table for all subnets associated with the cluster. You can't reuse a route table with multiple clusters due to the potential for overlapping pod CIDRs and conflicting routing rules.
- For system-assigned managed identity, it's only supported to provide your own subnet and route table via Azure CLI because Azure CLI automatically adds the role assignment. If you're using an ARM template or other clients, you must use a
[user-assigned managed identity](configure-kubenet#create-an-aks-cluster-with-user-assigned-managed-identity), assign permissions before cluster creation, and ensure the user-assigned identity has write permissions to your custom subnet and custom route table. - Using the same route table with multiple AKS clusters isn't supported.

Note

When you create and use your own VNet and route table with the kubenet network plugin, you must configure a [user-assigned managed identity](use-managed-identity#create-a-user-assigned-managed-identity) for the cluster. With a system-assigned managed identity, you can't retrieve the identity ID before creating a cluster, which causes a delay during role assignment.

Both system-assigned and user-assigned managed identities are supported when you create and use your own VNet and route table with the Azure network plugin. We highly recommend using a user-assigned managed identity for BYO scenarios.

### Add a route table with a user-assigned managed identity to your AKS cluster

After creating a custom route table and associating it with a subnet in your virtual network, you can create a new AKS cluster specifying your route table with a user-assigned managed identity. You need to use the subnet ID for where you plan to deploy your AKS cluster. This subnet also must be associated with your custom route table.

Get the subnet ID using the

command.`az network vnet subnet list`

`az network vnet subnet list --resource-group myResourceGroup --vnet-name myAKSVnet [--subscription]`

Create an AKS cluster with a custom subnet pre-configured with a route table using the

command and providing your values for the`az aks create`

`--vnet-subnet-id`

and`--assign-identity`

parameters.`az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --vnet-subnet-id mySubnetIDResourceID \ --assign-identity controlPlaneIdentityResourceID \ --generate-ssh-keys`


## Next steps

This article showed you how to deploy your AKS cluster into your existing virtual network subnet. Now, you can start [creating new apps using Helm](quickstart-helm) or [deploying existing apps using Helm](kubernetes-helm).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/migrate-from-npm-to-cilium-network-policy -->

# Migrate from Network Policy Manager (NPM) to Cilium Network Policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, we provide a comprehensive guide to plan, execute, and validate the migration from Network Policy Manager (NPM) to Cilium Network Policy. The goal is to ensure policy parity, minimize service disruption, and align with Azure CNI's strategic direction toward eBPF-based networking and enhanced observability.

Important

This guide applies exclusively to AKS clusters running Linux nodes. Cilium Network Policy isn't currently supported for Windows nodes in AKS.

## Key considerations before you begin

- Policy Compatibility: NPM and Cilium differ in enforcement models. Before migration you need to validate that existing policies are compatible or identify required changes. Refer to the Pre-Migration Validation section for guidance.
- Downtime Expectations: Policy enforcement might be temporarily inconsistent during node reimaging.
- Windows Node Pools: Cilium Network Policy isn't currently supported for Windows nodes in AKS.

## Pre-migration validation

Before migrating from Network Policy Manager (NPM) to Cilium Network Policy, it's important to assess the compatibility of your existing network policies. While most policies continue to function as expected post-migration, there are specific scenarios where behavior might differ between NPM and Cilium. These differences could require updates to your policies either before or after the migration to ensure consistent enforcement and avoid unintended traffic drops. In this section, we outline known scenarios where policy adjustments might be necessary. We explain why it matters, and provide guidance on what actions—if any—are required to make your policies Cilium-compatible.

### NetworkPolicy with endPort

Note

Cilium started supporting the `endPort`

field in Kubernetes NetworkPolicy in version 1.17.

The endPort field allows you to define a range of ports in a single rule, rather than specifying individual ports.

Here's an example of a Kubernetes NetworkPolicy that uses the endPort field:

```
egress:
- to:
- ipBlock:
cidr: 10.0.0.0/24
ports:
- protocol: TCP
port: 32000
endPort: 32768
```


**Action Required:**

- If your AKS cluster is running Cilium version 1.17 or later, no changes are needed as endPort is fully supported.
- If your cluster is running a Cilium version earlier than 1.17, remove the endPort field from any policies before migrating. Use explicit single-port entries instead.

### NetworkPolicy with ipBlock

The ipBlock field in Kubernetes NetworkPolicy allows you to define CIDR ranges for ingress sources or egress destinations. These ranges can include external IPs, Pod IPs, or Node IPs. However, Cilium doesn't allow egress to Pod or Node IPs using ipBlock, even if those IPs fall within the specified CIDR range.

For example, the following NetworkPolicy uses an ipBlock to allow all egress traffic to 0.0.0.0/0:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: example-ipblock
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 0.0.0.0/0
```


- Under NPM, this policy would allow egress to all destinations, including Pods and Nodes.
- After migrating to Cilium, egress to Pod and Node IPs will be blocked, even though they fall within the 0.0.0.0/0 range.

**Action Required:**

- To allow traffic to Pod IPs, before migration replace the ipBlock with a combination of namespaceSelector and podSelector.

Here's an example of using namespaceSelector and podSelector:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: example-ipblock
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 0.0.0.0/0
- namespaceSelector: {}
- podSelector: {}
```


- For Node IPs, there's no pre-migration workaround. After migration, you must create a CiliumNetworkPolicy that explicitly allows egress to the host and/or remote-node entities. Until this policy is in place, egress traffic to Node IPs is blocked.

Here's an example of CiliumNetworkPolicy to allow traffic from/to local and remote nodes:

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
name: allow-node-egress
namespace: ipblock-test
spec:
endpointSelector: {} # Applies to all pods in the namespace
egress:
- toEntities:
- host # host allows traffic from/to the local node's host network namespace
- remote-node # remote-node allows traffic from/to the remote node's host network namespace
```


### NetworkPolicy with named Ports

Kubernetes NetworkPolicy allows you to reference ports by name instead of number. If you're using named ports in your NetworkPolicies, Cilium might fail to enforce rules correctly and lead to unexpected traffic being blocked. This issue happens when the same port name is used for different ports.
For more information, see [Cilium GitHub issue #30003](https://github.com/cilium/cilium/issues/30003).

Here's an example of NetworkPolicy uses Named port to allow egress traffic:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
annotations:
name: allow-egress
namespace: default
spec:
podSelector:
matchLabels:
network-rules-egress: cilium-np-test
egress:
- ports:
- port: http-test # Named port
protocol: TCP
policyTypes:
- Egress
```


**Action Required:**

- Before migration, replace all named ports in your policies with their corresponding numeric values.

### NetworkPolicy with Egress Policies

Kubernetes NetworkPolicy on NPM doesn't block egress traffic from a pod to its own node's IP, this traffic is implicitly allowed. After you migrate to Cilium, this behavior will change, and traffic to local nodes that was previously allowed will be blocked unless explicitly allowed.

For example, the following policy allows egress only to an internal API subnet:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: allow-egress
namespace: default
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 10.20.30.0/24
```


- With NPM: Egress traffic to 10.20.30.0/24 is allowed explicitly, and egress traffic to the local node is allowed implicitly.
- With Cilium: Only traffic to 10.20.30.0/24 is allowed; egress to the node IP is blocked unless you permit it explicitly.

**Action Required:**

- Review all existing egress policies for your workloads.
- If your applications rely on NPM's implicit allow behavior for egress to the local node, you must add explicit egress rules to maintain connectivity after migration.
- You can add a CiliumNetworkPolicy after migration to explicitly allow egress traffic to the local host.

### Ingress policy behavior changes

Under Network Policy Manager (NPM), ingress traffic arriving via a LoadBalancer or NodePort service with "externalTrafficPolicy=Cluster" - which is the default setting - isn't subject to ingress policy enforcement. This behavior means that even if a pod has a restrictive ingress policy, traffic from external sources might still reach it via loadbalancer or nodeport services.

In contrast, Cilium enforces ingress policies on all traffic, including traffic routed internally due to externalTrafficPolicy=Cluster. As a result, after migration, traffic that was previously allowed might be dropped if the appropriate ingress rules aren't explicitly defined.

For example, Customer creates a network policy to deny all in ingress traffic

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: default-deny-ingress
spec:
podSelector: {}
policyTypes:
- Ingress
```


- With NPM: Direct connection to the pod or via ClusterIP service is blocked. However, access through NodePort or LoadBalancer is still allowed despite the deny-all policy.
- With Cilium: All ingress traffic is blocked, including traffic via NodePort or LoadBalancer, unless explicitly allowed.

**Action Required:**

- Review all ingress policies for workloads behind LoadBalancer or NodePort services using externalTrafficPolicy=Cluster.
- Ensure that ingress rules explicitly allow traffic from the expected external sources (for example, IP ranges, namespaces, or labels).
- If your policy currently relies on the implicit allow behavior under NPM, you must add explicit ingress rules to maintain connectivity after migration.

## Upgrade to Azure CNI Powered by Cilium

To use Cilium Network Policy, your AKS cluster must be running Azure CNI powered by Cilium. When you enable Cilium in a cluster currently using NPM, the existing NPM engine is automatically uninstalled and replaced with Cilium.

Warning

The upgrade process triggers each node pool to be reimaged simultaneously. Upgrading each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image upgrade or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium will begin enforcing network policies only after all nodes are reimaged.

Important

These instructions apply to clusters upgrading from Azure CNI to Azure CNI with the Cilium dataplane. Upgrades from bring-your-own CNIs or changes the IPAM mode aren't covered here. For more information, see [Upgrade Azure CNI documentation](update-azure-cni).

To perform the upgrade, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Use the following command to upgrade an existing cluster to Azure CNI Powered by Cilium. Replace the values for `clusterName`

and `resourceGroupName`

:

```
az aks update --name <clusterName> --resource-group <resourceGroupName> --network-dataplane cilium
```


## Next steps

For more information about using Cilium FQDN network policy on AKS, see

[Set up FQDN filtering feature for Container Network Security in Advanced Container Networking Services](how-to-apply-fqdn-filtering-policies).For more information about using Cilium L7 network policy on AKS, see

[Set up Layer 7(L7) policies with Advanced Container Networking Services](how-to-apply-l7-policies).For more information about network policy best practices on aks, see

[Best practices for network policies in Azure Kubernetes Service (AKS)](network-policy-best-practices)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/core-aks-concepts -->

# Core concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes core concepts of Azure Kubernetes Service (AKS), a managed Kubernetes service that you can use to deploy and operate containerized applications at scale on Azure.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## What is Kubernetes?

Kubernetes is an open-source container orchestration platform for automating the deployment, scaling, and management of containerized applications. For more information, see the official [Kubernetes documentation](https://kubernetes.io/docs/home/).

## What is AKS?

AKS is a managed Kubernetes service that simplifies deploying, managing, and scaling containerized applications that use Kubernetes. For more information, see [What is Azure Kubernetes Service (AKS)?](what-is-aks).

## Cluster components

An AKS cluster is divided into two main components:

**Control plane**: The control plane provides the core Kubernetes services and orchestration of application workloads.**Nodes**: Nodes are the underlying virtual machines (VMs) that run your applications.

Note

AKS managed components have the label `kubernetes.azure.com/managedby`

: `aks`

.

AKS manages the Helm releases with the prefix `aks-managed`

. Continuously increasing revisions on these releases are expected and safe.

### Control plane

The Azure managed control plane is composed of several components that help manage the cluster:

| Component | Description |
|---|---|
`kube-apiserver` |
The API server (
|

`etcd`

[etcd](https://kubernetes.io/docs/concepts/overview/components/#etcd)helps to maintain the state of your Kubernetes cluster and configuration.`kube-scheduler`

[kube-scheduler](https://kubernetes.io/docs/concepts/overview/components/#kube-scheduler)) helps to make scheduling decisions. It watches for new pods with no assigned node and selects a node for them to run on.`kube-controller-manager`

[kube-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#kube-controller-manager)) runs controller processes, such as noticing and responding when nodes go down.`cloud-controller-manager`

[cloud-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#cloud-controller-manager)) embeds cloud-specific control logic to run controllers specific to the cloud provider.### Nodes

Each AKS cluster has at least one node, which is an Azure VM that runs Kubernetes node components. The following components run on each node:

| Component | Description |
|---|---|
`kubelet` |
The
|

`kube-proxy`

[kube-proxy](https://kubernetes.io/docs/concepts/overview/components/#kube-proxy)is a network proxy that maintains network rules on nodes.`container runtime`

[container runtime](https://kubernetes.io/docs/concepts/overview/components/#container-runtime)manages the execution and lifecycle of containers.## Node configuration

Configure the following settings for nodes.

### VM size and image

The *Azure VM size* for your nodes defines CPUs, memory, size, and the storage type available, such as a high-performance solid-state drive or a regular hard-disk drive. The VM size you choose depends on the workload requirements and the number of pods that you plan to run on each node. As of May 2025, the default VM SKU and size will be dynamically selected by AKS based on available capacity and quota if the parameter is left blank during deployment. For more information, see [Supported VM sizes in Azure Kubernetes Service (AKS)](quotas-skus-regions#supported-vm-sizes).

In AKS, the *VM image* for your cluster's nodes is based on Ubuntu Linux, [Azure Linux](use-azure-linux), or Windows Server 2022. When you create an AKS cluster or scale out the number of nodes, the Azure platform automatically creates and configures the requested number of VMs. Agent nodes are billed as standard VMs. Any VM size discounts, including [Azure reservations](/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations), are automatically applied.

### OS disks

Default OS disk sizing is used on new clusters or node pools only when a default OS disk size isn't specified. This behavior applies to both managed and ephemeral OS disks. For more information, see [Default OS disk sizing](concepts-storage#default-os-disk-sizing).

### Resource reservations

AKS uses node resources to help the nodes function as part of the cluster. This usage can cause a discrepancy between the node's total resources and the allocatable resources in AKS. To maintain node performance and functionality, AKS reserves two types of resources, CPU and memory, on each node. For more information, see [Resource reservations in AKS](node-resource-reservations).

### OS

AKS supports two linux distros: Ubuntu and Azure Linux. Ubuntu is the default Linux distro on AKS. Windows node pools are also supported on AKS with the [Long Term Servicing Channel (LTSC)](/en-us/windows-server/get-started/servicing-channels-comparison) as the default channel on AKS. For more information on default OS versions, see documentation on [node images](node-images).

### Container runtime

A container runtime is software that executes containers and manages container images on a node. The runtime helps abstract away system calls or OS-specific functionality to run containers on Linux or Windows. For Linux node pools, [containerd](https://containerd.io/) is used on Kubernetes version 1.19 and higher. For Windows Server 2019 and 2022 node pools, [containerd](https://containerd.io/) is generally available and is the only runtime option on Kubernetes version 1.23 and higher.

## Pods

A *pod* is a group of one or more containers that share the same network and storage resources and a specification for how to run the containers. Pods typically have a 1:1 mapping with a container, but you can run multiple containers in a pod.

## Node pools

In AKS, nodes of the same configuration are grouped together into *node pools*. These node pools contain the underlying virtual machine scale sets and virtual machines (VMs) that run your applications.

When you create an AKS cluster, you define the initial number of nodes and their size (version), which creates a [system node pool](use-system-pools). System node pools serve the primary purpose of hosting critical system pods, such as CoreDNS and `konnectivity`

.

To support applications that have different compute or storage demands, you can create *user node pools*. User node pools serve the primary purpose of hosting your application pods.

For more information, see [Create node pools in AKS](create-node-pools) and [Manage node pools in AKS](manage-node-pools).

## Node resource group

When you create an AKS cluster in an Azure resource group, the AKS resource provider automatically creates a second resource group called the *node resource group*. This resource group contains all the infrastructure resources associated with the cluster, including VMs, virtual machine scale sets, and storage.

For more information, see the following resources:

[Why are two resource groups created with AKS?](faq)[Can I provide my own name for the AKS node resource group?](faq)[Can I modify tags and other properties of the resources in the AKS node resource group?](faq)

## Namespaces

Kubernetes resources, such as pods and deployments, are logically grouped into *namespaces* to divide an AKS cluster and create, view, or manage access to resources.

The following namespaces are created by default in an AKS cluster:

| Namespace | Description |
|---|---|
`default` |
The
|

`kube-node-lease`

[kube-node-lease](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace enables nodes to communicate their availability to the control plane.`kube-public`

[kube-public](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace isn't typically used, but you can use it so that resources are visible across the whole cluster by any user.`kube-system`

[kube-system](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace is used by Kubernetes to manage cluster resources, such as`coredns`

, `konnectivity-agent`

, and `metrics-server`

. It is not recommended to deploy your own applications to this namespace. For rare cases where deploying your own applications to this namespace is necessary, see the [FAQ](faq#can-admission-controller-webhooks-affect-kube-system-and-internal-aks-namespaces-)to learn how.## Cluster modes

In AKS, you can create a cluster with the Automatic or Standard mode. AKS Automatic provides a more fully managed experience. You can manage cluster configuration, including nodes, scaling, security, and other preconfigured settings. AKS Standard provides more control over the cluster configuration, including the ability to manage node pools, scaling, and other settings.

For more information, see [AKS Automatic and Standard feature comparison](intro-aks-automatic#aks-automatic-and-standard-feature-comparison).

## Pricing tiers

AKS offers three pricing tiers for cluster management: Free, Standard, and Premium. The pricing tier you choose determines the features that are available for managing your cluster.

For more information, see [Pricing tiers for AKS cluster management](free-standard-pricing-tiers).

## Supported Kubernetes versions

For more information, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions).

## Related content

For information on more core concepts for AKS, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-apply-l7-policies -->

# Set up Layer 7(L7) policies with Advanced Container Networking Services

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article demonstrates how to set up L7 policies with Advanced Container Networking Services in AKS clusters. Continue only after you have reviewed the limitations and considerations listed on the [Layer 7 Policy Overview](container-network-security-l7-policy-concepts) page.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of Azure CLI required for the steps in this article is 2.79.0. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Install the `aks-preview`

Azure CLI extension

Install or update the Azure CLI preview extension using the [ az extension add](/en-us/cli/azure/extension#az-extension-add) or

[command.](/en-us/cli/azure/extension#az-extension-update)

`az extension update`

The minimum version of the aks-preview Azure CLI extension is `14.0.0b6`


```
# Install the aks-preview extension
az extension add --name aks-preview
# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```


### Register the `AdvancedNetworkingL7PolicyPreview`

feature flag

Register the `AdvancedNetworkingL7PolicyPreview`

feature flag using the [ az feature register](/en-us/cli/azure/feature#az-feature-register) command.

```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"
```


Verify successful registration using the [ az feature show](/en-us/cli/azure/feature#az-feature-show) command. It takes a few minutes for the registration to complete.

```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"
```


Once the feature shows `Registered`

, refresh the registration of the `Microsoft.ContainerService`

resource provider using the [ az provider register](/en-us/cli/azure/provider#az-provider-register) command.

### Enable Advanced Container Networking Services

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. These features encompass:

**Container Network Observability:**Provides insights into your network traffic. To learn more visit[Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability).**Container Network Security:**Offers security features like Fully Qualified Domain Name (FQDN) filtering. To learn more visit[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security).

Note

Clusters with the Cilium data plane support Container Network Observability and Container Network security starting with Kubernetes version 1.29.

For this demo, the `--acns-advanced-networkpolicies`

parameter must be set to "L7" to enable L7 policies. Setting this parameter to "L7" also enables FQDN filtering. If you only want to enable FQDN filtering, set the parameter to "FQDN". To disable both features, you can follow the instructions provided in [Disable Container Network Security](advanced-container-networking-services-overview).

```
export CLUSTER_NAME="<aks-cluster-name>"
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--network-plugin azure \
--network-dataplane cilium \
--enable-acns \
--acns-advanced-networkpolicies L7
```


### Enable Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the Advanced Container Networking Services flag,

`--enable-acns`

, updates an existing AKS cluster with all Advanced Container Networking Services features which includes [Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability)and the

[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security)feature.

Note

Only clusters with the Cilium data plane support Container Network Security features of Advanced Container Networking Services.

For this demo, the `--acns-advanced-networkpolicies`

parameter must be set to "L7" to enable L7 policies. Setting this parameter to "L7" also enables FQDN filtering. If you only want to enable FQDN filtering, set the parameter to "FQDN". To disable both features, you can follow the instructions provided in [Disable Container Network Security](advanced-container-networking-services-overview).

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns \
--acns-advanced-networkpolicies L7
```


## Get cluster credentials

Get your cluster credentials using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Set up http-server application on your AKS cluster

Apply the below YAML to your AKS cluster to set up the `http-server`

application.

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: http-server
labels:
app: http-server
spec:
replicas: 1
selector:
matchLabels:
app: http-server
template:
metadata:
labels:
app: http-server
spec:
containers:
- name: http-server
image: nginx:latest
ports:
- containerPort: 8080
volumeMounts:
- name: config-volume
mountPath: /etc/nginx/conf.d
volumes:
- name: config-volume
configMap:
name: nginx-config
---
apiVersion: v1
kind: Service
metadata:
name: http-server
spec:
selector:
app: http-server
ports:
- protocol: TCP
port: 80
targetPort: 8080
---
apiVersion: v1
kind: ConfigMap
metadata:
name: nginx-config
data:
default.conf: |
server {
listen 8080;
location / {
return 200 "Hello from the server root!\n";
}
location /products {
return 200 "Listing products...\n";
}
}
```


## Set up http-client application on your AKS Cluster

Apply the below YAML to your AKS cluster to set up the `http-client`

application.

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: http-client
labels:
app: http-client
spec:
replicas: 1
selector:
matchLabels:
app: http-client
template:
metadata:
labels:
app: http-client
spec:
containers:
- name: http-client
image: curlimages/curl:latest
command: ["sleep", "infinity"]
```


## Test connectivity with a policy

Next, apply the following Layer 7 policy to allow only `GET`

requests from the `http-client`

application to the `/products`

endpoint on the `http-server`

:

```
apiVersion: cilium.io/v2
kind: CiliumNetworkPolicy
metadata:
name: allow-get-products
spec:
description: "Allow only GET requests to /products from http-client to http-server"
endpointSelector:
matchLabels:
app: http-server
ingress:
- fromEndpoints:
- matchLabels:
app: http-client
toPorts:
- ports:
- port: "8080"
protocol: TCP
rules:
http:
- method: "GET"
path: "/products"
```


### Verify policy

To verify the policy's enforcement, execute these commands from the `http-client`

pod:

```
kubectl exec -it <your-http-client-pod-name> -n default -- curl -v http://http-server:80/products
```


You should expect an output like `Listing products...`

when you run the above command

```
kubectl exec -it <your-http-client-pod-name> -n default -- curl -v -XPOST http://http-server:80/products -d "test=data"
```


You should expect an output like `Access Denied`

when you run the above command

### Observing L7 metrics

If you have Advanced Container Network Service's container network observability enabled, you can visualize the traffic on Grafana.

To simplify the analysis of these L7 metrics, we provide preconfigured Azure Managed Grafana dashboards. You can find them under the **Dashboards > Azure Managed Prometheus** folder, with filenames like **"Kubernetes/Networking/L7 (Namespace)"** and **"Kubernetes/Networking/L7 (Workload)"**.

You should see metrics similar to the following:

## Clean up resources

If you don't plan on using this application, delete the other resources you created in this article using the [ az group delete](/en-us/cli/azure/#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP
```


## Next steps

In this how-to article, you learned how to enable and apply L7 Policies with Advanced Container Networking Services for your AKS cluster.

- For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see
[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/migrate-from-npm-to-cilium-network-policy -->

# Migrate from Network Policy Manager (NPM) to Cilium Network Policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, we provide a comprehensive guide to plan, execute, and validate the migration from Network Policy Manager (NPM) to Cilium Network Policy. The goal is to ensure policy parity, minimize service disruption, and align with Azure CNI's strategic direction toward eBPF-based networking and enhanced observability.

Important

This guide applies exclusively to AKS clusters running Linux nodes. Cilium Network Policy isn't currently supported for Windows nodes in AKS.

## Key considerations before you begin

- Policy Compatibility: NPM and Cilium differ in enforcement models. Before migration you need to validate that existing policies are compatible or identify required changes. Refer to the Pre-Migration Validation section for guidance.
- Downtime Expectations: Policy enforcement might be temporarily inconsistent during node reimaging.
- Windows Node Pools: Cilium Network Policy isn't currently supported for Windows nodes in AKS.

## Pre-migration validation

Before migrating from Network Policy Manager (NPM) to Cilium Network Policy, it's important to assess the compatibility of your existing network policies. While most policies continue to function as expected post-migration, there are specific scenarios where behavior might differ between NPM and Cilium. These differences could require updates to your policies either before or after the migration to ensure consistent enforcement and avoid unintended traffic drops. In this section, we outline known scenarios where policy adjustments might be necessary. We explain why it matters, and provide guidance on what actions—if any—are required to make your policies Cilium-compatible.

### NetworkPolicy with endPort

Note

Cilium started supporting the `endPort`

field in Kubernetes NetworkPolicy in version 1.17.

The endPort field allows you to define a range of ports in a single rule, rather than specifying individual ports.

Here's an example of a Kubernetes NetworkPolicy that uses the endPort field:

```
egress:
- to:
- ipBlock:
cidr: 10.0.0.0/24
ports:
- protocol: TCP
port: 32000
endPort: 32768
```


**Action Required:**

- If your AKS cluster is running Cilium version 1.17 or later, no changes are needed as endPort is fully supported.
- If your cluster is running a Cilium version earlier than 1.17, remove the endPort field from any policies before migrating. Use explicit single-port entries instead.

### NetworkPolicy with ipBlock

The ipBlock field in Kubernetes NetworkPolicy allows you to define CIDR ranges for ingress sources or egress destinations. These ranges can include external IPs, Pod IPs, or Node IPs. However, Cilium doesn't allow egress to Pod or Node IPs using ipBlock, even if those IPs fall within the specified CIDR range.

For example, the following NetworkPolicy uses an ipBlock to allow all egress traffic to 0.0.0.0/0:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: example-ipblock
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 0.0.0.0/0
```


- Under NPM, this policy would allow egress to all destinations, including Pods and Nodes.
- After migrating to Cilium, egress to Pod and Node IPs will be blocked, even though they fall within the 0.0.0.0/0 range.

**Action Required:**

- To allow traffic to Pod IPs, before migration replace the ipBlock with a combination of namespaceSelector and podSelector.

Here's an example of using namespaceSelector and podSelector:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: example-ipblock
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 0.0.0.0/0
- namespaceSelector: {}
- podSelector: {}
```


- For Node IPs, there's no pre-migration workaround. After migration, you must create a CiliumNetworkPolicy that explicitly allows egress to the host and/or remote-node entities. Until this policy is in place, egress traffic to Node IPs is blocked.

Here's an example of CiliumNetworkPolicy to allow traffic from/to local and remote nodes:

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
name: allow-node-egress
namespace: ipblock-test
spec:
endpointSelector: {} # Applies to all pods in the namespace
egress:
- toEntities:
- host # host allows traffic from/to the local node's host network namespace
- remote-node # remote-node allows traffic from/to the remote node's host network namespace
```


### NetworkPolicy with named Ports

Kubernetes NetworkPolicy allows you to reference ports by name instead of number. If you're using named ports in your NetworkPolicies, Cilium might fail to enforce rules correctly and lead to unexpected traffic being blocked. This issue happens when the same port name is used for different ports.
For more information, see [Cilium GitHub issue #30003](https://github.com/cilium/cilium/issues/30003).

Here's an example of NetworkPolicy uses Named port to allow egress traffic:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
annotations:
name: allow-egress
namespace: default
spec:
podSelector:
matchLabels:
network-rules-egress: cilium-np-test
egress:
- ports:
- port: http-test # Named port
protocol: TCP
policyTypes:
- Egress
```


**Action Required:**

- Before migration, replace all named ports in your policies with their corresponding numeric values.

### NetworkPolicy with Egress Policies

Kubernetes NetworkPolicy on NPM doesn't block egress traffic from a pod to its own node's IP, this traffic is implicitly allowed. After you migrate to Cilium, this behavior will change, and traffic to local nodes that was previously allowed will be blocked unless explicitly allowed.

For example, the following policy allows egress only to an internal API subnet:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: allow-egress
namespace: default
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 10.20.30.0/24
```


- With NPM: Egress traffic to 10.20.30.0/24 is allowed explicitly, and egress traffic to the local node is allowed implicitly.
- With Cilium: Only traffic to 10.20.30.0/24 is allowed; egress to the node IP is blocked unless you permit it explicitly.

**Action Required:**

- Review all existing egress policies for your workloads.
- If your applications rely on NPM's implicit allow behavior for egress to the local node, you must add explicit egress rules to maintain connectivity after migration.
- You can add a CiliumNetworkPolicy after migration to explicitly allow egress traffic to the local host.

### Ingress policy behavior changes

Under Network Policy Manager (NPM), ingress traffic arriving via a LoadBalancer or NodePort service with "externalTrafficPolicy=Cluster" - which is the default setting - isn't subject to ingress policy enforcement. This behavior means that even if a pod has a restrictive ingress policy, traffic from external sources might still reach it via loadbalancer or nodeport services.

In contrast, Cilium enforces ingress policies on all traffic, including traffic routed internally due to externalTrafficPolicy=Cluster. As a result, after migration, traffic that was previously allowed might be dropped if the appropriate ingress rules aren't explicitly defined.

For example, Customer creates a network policy to deny all in ingress traffic

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: default-deny-ingress
spec:
podSelector: {}
policyTypes:
- Ingress
```


- With NPM: Direct connection to the pod or via ClusterIP service is blocked. However, access through NodePort or LoadBalancer is still allowed despite the deny-all policy.
- With Cilium: All ingress traffic is blocked, including traffic via NodePort or LoadBalancer, unless explicitly allowed.

**Action Required:**

- Review all ingress policies for workloads behind LoadBalancer or NodePort services using externalTrafficPolicy=Cluster.
- Ensure that ingress rules explicitly allow traffic from the expected external sources (for example, IP ranges, namespaces, or labels).
- If your policy currently relies on the implicit allow behavior under NPM, you must add explicit ingress rules to maintain connectivity after migration.

## Upgrade to Azure CNI Powered by Cilium

To use Cilium Network Policy, your AKS cluster must be running Azure CNI powered by Cilium. When you enable Cilium in a cluster currently using NPM, the existing NPM engine is automatically uninstalled and replaced with Cilium.

Warning

The upgrade process triggers each node pool to be reimaged simultaneously. Upgrading each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image upgrade or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium will begin enforcing network policies only after all nodes are reimaged.

Important

These instructions apply to clusters upgrading from Azure CNI to Azure CNI with the Cilium dataplane. Upgrades from bring-your-own CNIs or changes the IPAM mode aren't covered here. For more information, see [Upgrade Azure CNI documentation](update-azure-cni).

To perform the upgrade, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Use the following command to upgrade an existing cluster to Azure CNI Powered by Cilium. Replace the values for `clusterName`

and `resourceGroupName`

:

```
az aks update --name <clusterName> --resource-group <resourceGroupName> --network-dataplane cilium
```


## Next steps

For more information about using Cilium FQDN network policy on AKS, see

[Set up FQDN filtering feature for Container Network Security in Advanced Container Networking Services](how-to-apply-fqdn-filtering-policies).For more information about using Cilium L7 network policy on AKS, see

[Set up Layer 7(L7) policies with Advanced Container Networking Services](how-to-apply-l7-policies).For more information about network policy best practices on aks, see

[Best practices for network policies in Azure Kubernetes Service (AKS)](network-policy-best-practices)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/configure-kubenet -->

# Use kubenet networking with your own IP address ranges in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

On **31 March 2028**, kubenet networking for Azure Kubernetes Service (AKS) will be retired.

To avoid service disruptions, **you'll need to** [upgrade to Azure Container Networking Interface (CNI) overlay](/en-us/azure/aks/upgrade-aks-ipam-and-dataplane#upgrade-an-existing-cluster-to-azure-cni-overlay) **before that date**, when workloads running on kubenet for AKS will no longer be supported.

AKS clusters use kubenet and create an Azure virtual network and subnet for you by default. With kubenet, nodes get an IP address from the Azure virtual network subnet. Pods receive an IP address from a logically different address space to the Azure virtual network subnet of the nodes. Network address translation (NAT) is then configured so the pods can reach resources on the Azure virtual network. The source IP address of the traffic is NAT'd to the node's primary IP address. This approach greatly reduces the number of IP addresses you need to reserve in your network space for pods to use.

With [Azure Container Networking Interface (CNI)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md), every pod gets an IP address from the subnet and can be accessed directly. These IP addresses must be planned in advance and unique across your network space. Each node has a configuration parameter for the maximum number of pods it supports. The equivalent number of IP addresses per node are then reserved up front for that node. This approach requires more planning, and often leads to IP address exhaustion or the need to rebuild clusters in a larger subnet as your application demands grow. You can configure the maximum pods deployable to a node at cluster creation time or when creating new node pools. If you don't specify `maxPods`

when creating new node pools, you receive a default value of *110* for kubenet.

This article shows you how to use kubenet networking to create and use a virtual network subnet for an AKS cluster. For more information on network options and considerations, see [Network concepts for Kubernetes and AKS](concepts-network).

## Prerequisites

- The virtual network for the AKS cluster must allow outbound internet connectivity.
- Don't create more than one AKS cluster in the same subnet.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for the Kubernetes service address range, pod address range, or cluster virtual network address range. The range can't be updated after you create your cluster. - The cluster identity used by the AKS cluster must at least have the
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)role on the subnet within your virtual network. CLI helps set the role assignment automatically. If you're using an ARM template or other clients, you need to manually set the role assignment. You must also have the appropriate permissions, such as the subscription owner, to create a cluster identity and assign it permissions. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, you need the following permissions:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


Warning

To use Windows Server node pools, you must use Azure CNI. The kubenet network model isn't available for Windows Server containers.

## Before you begin

You need the Azure CLI version 2.0.65 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Overview of kubenet networking with your own subnet

In many environments, you have defined virtual networks and subnets with allocated IP address ranges, and you use these resources to support multiple services and applications. To provide network connectivity, AKS clusters can use *kubenet* (basic networking) or Azure CNI (*advanced networking*).

With *kubenet*, only the nodes receive an IP address in the virtual network subnet. Pods can't communicate directly with each other. Instead, User Defined Routing (UDR) and IP forwarding handle connectivity between pods across nodes. UDRs and IP forwarding configuration is created and maintained by the AKS service by default, but you can [bring your own route table for custom route management](#bring-your-own-subnet-and-route-table-with-kubenet) if you want. You can also deploy pods behind a service that receives an assigned IP address and load balances traffic for the application. The following diagram shows how the AKS nodes receive an IP address in the virtual network subnet, but not the pods:

Azure supports a maximum of *400* routes in a UDR, so you can't have an AKS cluster larger than 400 nodes. AKS [virtual nodes](virtual-nodes-cli) and Azure Network Policies aren't supported with *kubenet*. [Calico Network Policies](https://docs.projectcalico.org/v3.9/security/calico-network-policy) are supported.

With *Azure CNI*, each pod receives an IP address in the IP subnet and can communicate directly with other pods and services. Your clusters can be as large as the IP address range you specify. However, you must plan the IP address range in advance, and all the IP addresses are consumed by the AKS nodes based on the maximum number of pods they can support. Advanced network features and scenarios such as [virtual nodes](virtual-nodes-cli) or Network Policies (either Azure or Calico) are supported with *Azure CNI*.

### Limitations & considerations for kubenet

- An additional hop is required in the design of kubenet, which adds minor latency to pod communication.
- Route tables and user-defined routes are required for using kubenet, which adds complexity to operations.
- For more information, see
[Customize cluster egress with a user-defined routing table in AKS](egress-udr)and[Customize cluster egress with outbound types in AKS](egress-outboundtype).

- For more information, see
- Direct pod addressing isn't supported for kubenet due to kubenet design.
- Unlike Azure CNI clusters, multiple kubenet clusters can't share a subnet.
- AKS doesn't apply Network Security Groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure the security rules in the NSGs allow traffic between the node and pod CIDR. For more details, see
[Network security groups](concepts-network#network-security-groups). - Features
**not supported on kubenet**include:

Note

Some of the system pods such as **konnectivity** within the cluster use the host node IP address rather than an IP from the overlay address space. The system pods will only use the node IP and not an IP address from the virtual network.

### IP address availability and exhaustion

A common issue with *Azure CNI* is that the assigned IP address range is too small to then add more nodes when you scale or upgrade a cluster. The network team also might not be able to issue a large enough IP address range to support your expected application demands.

As a compromise, you can create an AKS cluster that uses *kubenet* and connect to an existing virtual network subnet. This approach lets the nodes receive defined IP addresses without the need to reserve a large number of IP addresses up front for any potential pods that could run in the cluster. With *kubenet*, you can use a much smaller IP address range and support large clusters and application demands. For example, with a */27* IP address range on your subnet, you can run a 20-25 node cluster with enough room to scale or upgrade. This cluster size can support up to *2,200-2,750* pods (with a default maximum of 110 pods per node). The maximum number of pods per node that you can configure with *kubenet* in AKS is 250.

The following basic calculations compare the difference in network models:

**kubenet**: A simple*/24*IP address range can support up to*251*nodes in the cluster. Each Azure virtual network subnet reserves the first three IP addresses for management operations. This node count can support up to*27,610*pods, with a default maximum of 110 pods per node.**Azure CNI**: That same basic*/24*subnet range can only support a maximum of*eight*nodes in the cluster. This node count can only support up to*240*pods, with a default maximum of 30 pods per node.

Note

These maximums don't take into account upgrade or scale operations. In practice, you can't run the maximum number of nodes the subnet IP address range supports. You must leave some IP addresses available for scaling or upgrading operations.

### Virtual network peering and ExpressRoute connections

To provide on-premises connectivity, both *kubenet* and *Azure-CNI* network approaches can use [Azure virtual network peering](/en-us/azure/virtual-network/virtual-network-peering-overview) or [ExpressRoute connections](/en-us/azure/expressroute/expressroute-introduction). Plan your IP address ranges carefully to prevent overlap and incorrect traffic routing. For example, many on-premises networks use a *10.0.0.0/8* address range that's advertised over the ExpressRoute connection. We recommend creating your AKS clusters in Azure virtual network subnets outside this address range, such as *172.16.0.0/16*.

### Choose a network model to use

The following considerations help outline when each network model may be the most appropriate:

**Use kubenet when**:

- You have limited IP address space.
- Most of the pod communication is within the cluster.
- You don't need advanced AKS features, such as virtual nodes or Azure Network Policy.

**Use Azure CNI when**:

- You have available IP address space.
- Most of the pod communication is to resources outside of the cluster.
- You don't want to manage user defined routes for pod connectivity.
- You need AKS advanced features, such as virtual nodes or Azure Network Policy.

For more information to help you decide which network model to use, see [Compare network models and their support scope](concepts-network-cni-overview).

## Create a virtual network and subnet

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

If you don't have an existing virtual network and subnet to use, create these network resources using the

command. The following example command creates a virtual network named`az network vnet create`

*myAKSVnet*with the address prefix of*192.168.0.0/16*and a subnet named*myAKSSubnet*with the address prefix*192.168.1.0/24*:`az network vnet create \ --resource-group myResourceGroup \ --name myAKSVnet \ --address-prefixes 192.168.0.0/16 \ --subnet-name myAKSSubnet \ --subnet-prefix 192.168.1.0/24 \ --location eastus`

Get the subnet resource ID using the

command and store it as a variable named`az network vnet subnet show`

`SUBNET_ID`

for later use.`SUBNET_ID=$(az network vnet subnet show --resource-group myResourceGroup --vnet-name myAKSVnet --name myAKSSubnet --query id -o tsv)`


## Create an AKS cluster in the virtual network

### Create an AKS cluster with system-assigned managed identities

Note

When using system-assigned identity, the Azure CLI grants the Network Contributor role to the system-assigned identity after the cluster is created. If you're using an ARM template or other clients, you need to use the [user-assigned managed identity](configure-kubenet#create-an-aks-cluster-with-user-assigned-managed-identity) instead.

Create an AKS cluster with system-assigned managed identities using the

command.`az aks create`

`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --network-plugin kubenet \ --service-cidr 10.0.0.0/16 \ --dns-service-ip 10.0.0.10 \ --pod-cidr 10.244.0.0/16 \ --vnet-subnet-id $SUBNET_ID \ --generate-ssh-keys`

Deployment parameters:

*--service-cidr*is optional. This address is used to assign internal services in the AKS cluster an IP address. This IP address range should be an address space that isn't in use elsewhere in your network environment, including any on-premises network ranges if you connect, or plan to connect, your Azure virtual networks using Express Route or a Site-to-Site VPN connection. The default value is 10.0.0.0/16.*--dns-service-ip*is optional. The address should be the*.10*address of your service IP address range. The default value is 10.0.0.10.*--pod-cidr*is optional. This address should be a large address space that isn't in use elsewhere in your network environment. This range includes any on-premises network ranges if you connect, or plan to connect, your Azure virtual networks using Express Route or a Site-to-Site VPN connection. The default value is 10.244.0.0/16.- This address range must be large enough to accommodate the number of nodes that you expect to scale up to. You can't change this address range once the cluster is deployed.
- The pod IP address range is used to assign a
*/24*address space to each node in the cluster. In the following example, the*--pod-cidr*of*10.244.0.0/16*assigns the first node*10.244.0.0/24*, the second node*10.244.1.0/24*, and the third node*10.244.2.0/24*. - As the cluster scales or upgrades, the Azure platform continues to assign a pod IP address range to each new node.


### Create an AKS cluster with user-assigned managed identity

#### Create a managed identity

Create a managed identity using the

command. If you have an existing managed identity, find the principal ID using the`az identity`

`az identity show --ids <identity-resource-id>`

command instead.`az identity create --name myIdentity --resource-group myResourceGroup`

Your output should resemble the following example output:

`{ "clientId": "<client-id>", "clientSecretUrl": "<clientSecretUrl>", "id": "/subscriptions/<subscriptionid>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myIdentity", "location": "westus2", "name": "myIdentity", "principalId": "<principal-id>", "resourceGroup": "myResourceGroup", "tags": {}, "tenantId": "<tenant-id>", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


#### Add role assignment for managed identity

If you're using the Azure CLI, the role is automatically added and you can skip this step. If you're using an ARM template or other clients, you need to use the Principal ID of the cluster managed identity to perform a role assignment.

Get the virtual network resource ID using the

command and store it as a variable named`az network vnet show`

`VNET_ID`

.`VNET_ID=$(az network vnet show --resource-group myResourceGroup --name myAKSVnet --query id -o tsv)`

Assign the managed identity for your AKS cluster

*Network Contributor*permissions on the virtual network using thecommand and provide the`az role assignment create`

*<principalId>*.`az role assignment create --assignee <control-plane-identity-principal-id> --scope $VNET_ID --role "Network Contributor" # Example command az role assignment create --assignee 22222222-2222-2222-2222-222222222222 --scope "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myAKSVnet" --role "Network Contributor"`


Note

Permission granted to your cluster's managed identity used by Azure may take up 60 minutes to populate.

#### Create an AKS cluster

Create an AKS cluster using the

command and provide the control plane's managed identity resource ID for the`az aks create`

`assign-identity`

argument to assign the user-assigned managed identity.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 3 \ --network-plugin kubenet \ --vnet-subnet-id $SUBNET_ID \ --assign-identity <identity-resource-id> \ --generate-ssh-keys`


When you create an AKS cluster, a network security group and route table are automatically created. These network resources are managed by the AKS control plane. The network security group is automatically associated with the virtual NICs on your nodes. The route table is automatically associated with the virtual network subnet. Network security group rules and route tables are automatically updated as you create and expose services.

## Bring your own subnet and route table with kubenet

With kubenet, a route table must exist on your cluster subnet(s). AKS supports bringing your own existing subnet and route table. If your custom subnet doesn't contain a route table, AKS creates one for you and adds rules throughout the cluster lifecycle. If your custom subnet contains a route table when you create your cluster, AKS acknowledges the existing route table during cluster operations and adds/updates rules accordingly for cloud provider operations.

Warning

You can add/update custom rules on the custom route table. However, rules are added by the Kubernetes cloud provider which can't be updated or removed. Rules such as *0.0.0.0/0* generally exist on a given route table (unless the egress outbound type is `none`

) and map to the target of your internet gateway, such as an NVA or other egress gateway. Take caution when updating rules.

Learn more about setting up a [custom route table](/en-us/azure/virtual-network/manage-route-table).

Kubenet networking requires organized route table rules to successfully route requests. Due to this design, route tables must be carefully maintained for each cluster that relies on it. Multiple clusters can't share a route table because pod CIDRs from different clusters might overlap which causes unexpected and broken routing scenarios. When configuring multiple clusters on the same virtual network or dedicating a virtual network to each cluster, consider the following limitations:

- A custom route table must be associated to the subnet before you create the AKS cluster.
- The associated route table resource can't be updated after cluster creation. However, custom rules can be modified on the route table.
- Each AKS cluster must use a single, unique route table for all subnets associated with the cluster. You can't reuse a route table with multiple clusters due to the potential for overlapping pod CIDRs and conflicting routing rules.
- For system-assigned managed identity, it's only supported to provide your own subnet and route table via Azure CLI because Azure CLI automatically adds the role assignment. If you're using an ARM template or other clients, you must use a
[user-assigned managed identity](configure-kubenet#create-an-aks-cluster-with-user-assigned-managed-identity), assign permissions before cluster creation, and ensure the user-assigned identity has write permissions to your custom subnet and custom route table. - Using the same route table with multiple AKS clusters isn't supported.

Note

When you create and use your own VNet and route table with the kubenet network plugin, you must configure a [user-assigned managed identity](use-managed-identity#create-a-user-assigned-managed-identity) for the cluster. With a system-assigned managed identity, you can't retrieve the identity ID before creating a cluster, which causes a delay during role assignment.

Both system-assigned and user-assigned managed identities are supported when you create and use your own VNet and route table with the Azure network plugin. We highly recommend using a user-assigned managed identity for BYO scenarios.

### Add a route table with a user-assigned managed identity to your AKS cluster

After creating a custom route table and associating it with a subnet in your virtual network, you can create a new AKS cluster specifying your route table with a user-assigned managed identity. You need to use the subnet ID for where you plan to deploy your AKS cluster. This subnet also must be associated with your custom route table.

Get the subnet ID using the

command.`az network vnet subnet list`

`az network vnet subnet list --resource-group myResourceGroup --vnet-name myAKSVnet [--subscription]`

Create an AKS cluster with a custom subnet pre-configured with a route table using the

command and providing your values for the`az aks create`

`--vnet-subnet-id`

and`--assign-identity`

parameters.`az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --vnet-subnet-id mySubnetIDResourceID \ --assign-identity controlPlaneIdentityResourceID \ --generate-ssh-keys`


## Next steps

This article showed you how to deploy your AKS cluster into your existing virtual network subnet. Now, you can start [creating new apps using Helm](quickstart-helm) or [deploying existing apps using Helm](kubernetes-helm).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-confidential-containers-default-policy -->

# Deploy an AKS cluster with Confidential Containers and an automatically generated policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you use the Azure CLI to deploy an Azure Kubernetes Service (AKS) cluster and configure Confidential Containers (preview) with an automatically generated security policy. You then deploy an application as a Confidential container. To learn more, read the [overview of AKS Confidential Containers](confidential-containers-overview).

In general, getting started with AKS Confidential Containers involves the following steps.

- Deploy or upgrade an AKS cluster using the Azure CLI
- Add an annotation to your pod YAML manifest to mark the pod as using confidential containers
- Add a security policy to your pod YAML manifest
- Deploy your application in confidential computing

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Prerequisites

The Azure CLI version 2.44.1 or later. Run

`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The

`aks-preview`

Azure CLI extension version 0.5.169 or later.The

`confcom`

Confidential Container Azure CLI extension 0.3.3 or later.`confcom`

is required to generate a[security policy](/en-us/azure/confidential-computing/confidential-containers-aks-security-policy).Register the

`Preview`

feature in your Azure subscription.AKS supports Confidential Containers (preview) on version 1.25.0 and higher.

A workload identity and a federated identity credential. The workload identity credential enables Kubernetes applications access to Azure resources securely with a Microsoft Entra ID based on annotated service accounts. If you aren't familiar with Microsoft Entra Workload ID, see the

[Microsoft Entra Workload ID overview](/en-us/azure/active-directory/workload-identities/workload-identities-overview)and review how[Workload Identity works with AKS](workload-identity-overview).The identity you're using to create your cluster has the appropriate minimum permissions. For more information about access and identity for AKS, see

[Access and identity options for Azure Kubernetes Service (AKS)](concepts-identity).To manage a Kubernetes cluster, use the Kubernetes command-line client

[kubectl](https://kubernetes.io/docs/reference/kubectl/). Azure Cloud Shell comes with`kubectl`

. You can install kubectl locally using the[az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli)command.Confidential containers on AKS provide a sidecar open source container for attestation and secure key release. The sidecar integrates with a Key Management Service (KMS), like Azure Key Vault, for releasing a key to the container group after validation is completed. Deploying an

[Azure Key Vault Managed HSM](/en-us/azure/key-vault/managed-hsm/overview)(Hardware Security Module) is optional but recommended to support container-level integrity and attestation. See[Provision and activate a Managed HSM](/en-us/azure/key-vault/managed-hsm/quick-create-cli)to deploy Managed HSM.

### Install the aks-preview Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

To install the aks-preview extension, run the following command:

```
az extension add --name aks-preview
```


Run the following command to update to the latest version of the extension:

```
az extension update --name aks-preview
```


### Install the confcom Azure CLI extension

To install the confcom extension, run the following command:

```
az extension add --name confcom
```


Run the following command to update to the latest version of the extension:

```
az extension update --name confcom
```


### Register the KataCcIsolationPreview feature flag

Register the `KataCcIsolationPreview`

feature flag by using the [az feature register](/en-us/cli/azure/feature#az-feature-register) command, as shown in the following example:

```
az feature register --namespace "Microsoft.ContainerService" --name "KataCcIsolationPreview"
```


It takes a few minutes for the status to show *Registered*. Verify the registration status by using the [az feature show](/en-us/cli/azure/feature#az-feature-show) command:

```
az feature show --namespace "Microsoft.ContainerService" --name "KataCcIsolationPreview"
```


When the status reflects *Registered*, refresh the registration of the *Microsoft.ContainerService* resource provider by using the [az provider register](/en-us/cli/azure/provider#az-provider-register) command:

```
az provider register --namespace "Microsoft.ContainerService"
```


## Deploy a new cluster

Create an AKS cluster using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command and specifying the following parameters:**--os-sku**:*AzureLinux*. Only the Azure Linux os-sku supports this feature in this preview release.**--node-vm-size**: Any Azure VM size that supports AMD SEV-SNP protected child VMs works. For example,[Standard_DC8as_cc_v5](/en-us/azure/virtual-machines/dcasccv5-dcadsccv5-series)VMs.**--enable-workload-identity**: Enables creating a Microsoft Entra Workload ID enabling pods to use a Kubernetes identity.**--enable-oidc-issuer**: Enables OpenID Connect (OIDC) Issuer. It allows a Microsoft Entra ID or other cloud provider identity and access management platform the ability to discover the API server's public signing keys.**--workload-runtime**: Specify*KataCcIsolation*to enable the Confidential Containers feature on the node pool.

`az aks create --resource-group myResourceGroup --name myAKSCluster --kubernetes-version <1.25.0 and above> --os-sku AzureLinux --node-vm-size Standard_DC8as_cc_v5 --workload-runtime KataCcIsolation --node-count 1 --enable-oidc-issuer --enable-workload-identity --generate-ssh-keys`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

When the cluster is ready, get the cluster credentials using the

[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Deploy to an existing cluster

To use this feature with an existing AKS cluster, the following requirements must be met:

- Follow the steps to
[register the KataCcIsolationPreview](#register-the-kataccisolationpreview-feature-flag)feature flag. - Verify the cluster is running Kubernetes version 1.25.0 and higher.
[Enable workload identity](workload-identity-deploy-cluster#deploy-and-configure-microsoft-entra-workload-id-on-an-azure-kubernetes-service-aks-cluster)on the cluster if it isn't already.

Use the following command to enable Confidential Containers (preview) by creating a node pool to host it.

Add a node pool to your AKS cluster using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command. Specify the following parameters:**--resource-group**: Enter the name of an existing resource group to create the AKS cluster in.**--cluster-name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--name**: Enter a unique name for your clusters node pool, such as*nodepool2*.**--workload-runtime**: Specify*KataCcIsolation*to enable the feature on the node pool. Along with the`--workload-runtime`

parameter, these other parameters shall satisfy the following requirements. Otherwise, the command fails and reports an issue with the corresponding parameter(s).**--os-sku**:*AzureLinux*. Only the Azure Linux os-sku supports this feature in this preview release.**--node-vm-size**: Any Azure VM size that supports AMD SEV-SNP protected child VMs nested virtualization works. For example,[Standard_DC8as_cc_v5](/en-us/azure/virtual-machines/dcasccv5-dcadsccv5-series)VMs.

The following example adds a user node pool to

*myAKSCluster*with two nodes in*nodepool2*in the*myResourceGroup*:`az aks nodepool add --resource-group myResourceGroup --name nodepool2 –-cluster-name myAKSCluster --node-count 2 --os-sku AzureLinux --node-vm-size Standard_DC8as_cc_v5 --workload-runtime KataCcIsolation`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

Run the

[az aks update](/en-us/cli/azure/aks#az-aks-update)command to enable Confidential Containers (preview) on the cluster.`az aks update --name myAKSCluster --resource-group myResourceGroup`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

When the cluster is ready, get the cluster credentials using the

[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Configure container

Before you configure access to the Azure Key Vault and secret, and deploy an application as a Confidential container, you need to complete the configuration of the workload identity.

To configure the workload identity, perform the following steps described in the [Deploy and configure workload identity](workload-identity-deploy-cluster) article:

- Retrieve the OIDC Issuer URL
- Create a managed identity
- Create Kubernetes service account
- Establish federated identity credential

Important

You need to set the *environment variables* from the section **Export environmental variables** in the [Deploy and configure workload identity](workload-identity-deploy-cluster) article to continue completing this tutorial. Remember to set the variable `SERVICE_ACCOUNT_NAMESPACE`

to `kafka`

, and execute the command `kubectl create namespace kafka`

before configuring workload identity.

## Deploy a trusted application with kata-cc and attestation container

The following steps configure end-to-end encryption for Kafka messages using encryption keys managed by [Azure Managed Hardware Security Modules](/en-us/azure/key-vault/managed-hsm/overview) (mHSM). The key is only released when the Kafka consumer runs within a Confidential Container with an Azure attestation secret provisioning container injected in to the pod.

This configuration is based on the following four components:

- Kafka Cluster: A simple Kafka cluster deployed in the Kafka namespace on the cluster.
- Kafka Producer: A Kafka producer running as a vanilla Kubernetes pod that sends encrypted user-configured messages using a public key to a Kafka topic.
- Kafka Consumer: A Kafka consumer pod running with the kata-cc runtime, equipped with a secure key release container to retrieve the private key for decrypting Kafka messages and render the messages to web UI.

For this preview release, we recommend for test and evaluation purposes to either create or use an existing Azure Key Vault Premium tier resource to support storing keys in a hardware security module (HSM). We don't recommend using your production key vault. If you don't have an Azure Key Vault, see [Create a key vault using the Azure CLI](/en-us/azure/key-vault/general/quick-create-cli).

Grant the managed identity you created earlier, and your account, access to the key vault.

[Assign](/en-us/azure/key-vault/general/rbac-guide#assign-role)both identities the**Key Vault Crypto Officer**and**Key Vault Crypto User**Azure RBAC roles.Note

The managed identity is the value you assign to the

`USER_ASSIGNED_IDENTITY_NAME`

variable.To add role assignments, you must have

`Microsoft.Authorization/roleAssignments/write`

and`Microsoft.Authorization/roleAssignments/delete`

permissions, such as[Key Vault Data Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#key-vault-data-access-administrator),[User Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator), or[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner).You must use the Key Vault Premium SKU to support HSM-protected keys.


Run the following command to set the scope:

`AKV_SCOPE=$(az keyvault show --name <AZURE_AKV_RESOURCE_NAME> --query id --output tsv)`

Run the following command to assign the

**Key Vault Crypto Officer**role.`az role assignment create --role "Key Vault Crypto Officer" --assignee "${USER_ASSIGNED_IDENTITY_NAME}" --scope $AKV_SCOPE`

Run the following command to assign the

**Key Vault Crypto User**role.`az role assignment create --role "Key Vault Crypto User" --assignee "${USER_ASSIGNED_IDENTITY_NAME}" --scope $AKV_SCOPE`

Install the Kafka cluster in the kafka namespace by running the following command:

`kubectl create -f 'https://strimzi.io/install/latest?namespace=kafka' -n kafka`

Run the following command to apply the

`kafka`

cluster CR file.`kubectl apply -f https://strimzi.io/examples/latest/kafka/kafka-persistent-single.yaml -n kafka`

Prepare the RSA Encryption/Decryption key using the

[bash script](https://github.com/microsoft/confidential-container-demos/raw/main/kafka/setup-key.sh)for the workload from GitHub. Save the file as`setup-key.sh`

.Set the

`MAA_ENDPOINT`

environment variable with the FQDN of Attest URI by running the following command.`export MAA_ENDPOINT="$(az attestation show --name "myattestationprovider" --resource-group "MyResourceGroup" --query 'attestUri' -o tsv | cut -c 9-)"`

Check if the FQDN of Attest URI is in correct format (the MAA_ENDPOINT should not include the prefix "https://"):

`echo $MAA_ENDPOINT`

Note

To set up Microsoft Azure Attestation, see

[Quickstart: Set up Azure Attestation with Azure CLI](/en-us/azure/attestation/quickstart-azure-cli).Copy the following YAML manifest and save it as

`consumer.yaml`

.`apiVersion: v1 kind: Pod metadata: name: kafka-golang-consumer namespace: kafka labels: azure.workload.identity/use: "true" app.kubernetes.io/name: kafka-golang-consumer spec: serviceAccountName: workload-identity-sa runtimeClassName: kata-cc-isolation containers: - image: "mcr.microsoft.com/aci/skr:2.7" imagePullPolicy: Always name: skr env: - name: SkrSideCarArgs value: ewogICAgImNlcnRjYWNoZSI6IHsKCQkiZW5kcG9pbnRfdHlwZSI6ICJMb2NhbFRISU0iLAoJCSJlbmRwb2ludCI6ICIxNjkuMjU0LjE2OS4yNTQvbWV0YWRhdGEvVEhJTS9hbWQvY2VydGlmaWNhdGlvbiIKCX0gIAp9 command: - /bin/skr volumeMounts: - mountPath: /opt/confidential-containers/share/kata-containers/reference-info-base64 name: endor-loc - image: "mcr.microsoft.com/acc/samples/kafka/consumer:1.0" imagePullPolicy: Always name: kafka-golang-consumer env: - name: SkrClientKID value: kafka-encryption-demo - name: SkrClientMAAEndpoint value: sharedeus2.eus2.test.attest.azure.net - name: SkrClientAKVEndpoint value: "myKeyVault.vault.azure.net" - name: TOPIC value: kafka-demo-topic command: - /consume ports: - containerPort: 3333 name: kafka-consumer resources: limits: memory: 1Gi cpu: 200m volumes: - name: endor-loc hostPath: path: /opt/confidential-containers/share/kata-containers/reference-info-base64 --- apiVersion: v1 kind: Service metadata: name: consumer namespace: kafka spec: type: LoadBalancer selector: app.kubernetes.io/name: kafka-golang-consumer ports: - protocol: TCP port: 80 targetPort: kafka-consumer`

Note

Update the value for the pod environment variable

`SkrClientAKVEndpoint`

to match the URL of your Azure Key Vault, excluding the protocol value`https://`

. The current value placeholder value is`myKeyVault.vault.azure.net`

. Update the value for the pod environment variable`SkrClientMAAEndpoint`

with the value of`MAA_ENDPOINT`

. You can find the value of`MAA_ENDPOINT`

by running the command`echo $MAA_ENDPOINT`

or the command`az attestation show --name "myattestationprovider" --resource-group "MyResourceGroup" --query 'attestUri' -o tsv | cut -c 9-`

.Generate the security policy for the Kafka consumer YAML manifest and obtain the hash of the security policy stored in the

`WORKLOAD_MEASUREMENT`

variable by running the following command:`export WORKLOAD_MEASUREMENT=$(az confcom katapolicygen -y consumer.yaml --print-policy | base64 -d | sha256sum | cut -d' ' -f1)`

To generate an RSA asymmetric key pair (public and private keys), run the

`setup-key.sh`

script using the following command. The`<Azure Key Vault URL>`

value should be`<your-unique-keyvault-name>.vault.azure.net`

`export MANAGED_IDENTITY=${USER_ASSIGNED_CLIENT_ID} bash setup-key.sh "kafka-encryption-demo" <Azure Key Vault URL>`

Note

The envionment variable

`MANAGED_IDENTITY`

is required by the bash script`setup-key.sh`

.The public key will be saved as

`kafka-encryption-demo-pub.pem`

after executing the bash script.

Important

If you receive the error

`ForbiddenByRbac`

,you might need to wait up to 24 hours as the backend services for managed identities maintain a cache per resource URI for up to 24 hours. See also:[Troubleshoot Azure RBAC](/en-us/azure/role-based-access-control/troubleshooting#symptom---role-assignment-changes-are-not-being-detected).To verify the keys have been successfully uploaded to the key vault, run the following commands:

`az account set --subscription <Subscription ID> az keyvault key list --vault-name <KeyVault Name> -o table`

Copy the following YAML manifest and save it as

`producer.yaml`

.`apiVersion: v1 kind: Pod metadata: name: kafka-producer namespace: kafka spec: containers: - image: "mcr.microsoft.com/acc/samples/kafka/producer:1.0" name: kafka-producer command: - /produce env: - name: TOPIC value: kafka-demo-topic - name: MSG value: "Azure Confidential Computing" - name: PUBKEY value: |- -----BEGIN PUBLIC KEY----- MIIBojAN***AE= -----END PUBLIC KEY----- resources: limits: memory: 1Gi cpu: 200m`

Note

Update the value which begin with

`-----BEGIN PUBLIC KEY-----`

and ends with`-----END PUBLIC KEY-----`

strings with the content from`kafka-encryption-demo-pub.pem`

which was created in the previous step.Deploy the

`consumer`

and`producer`

YAML manifests using the files you saved earlier.`kubectl apply -f consumer.yaml`

`kubectl apply -f producer.yaml`

Get the IP address of the web service using the following command:

`kubectl get svc consumer -n kafka`

Copy and paste the external IP address of the consumer service into your browser and observe the decrypted message.

The following example resembles the output of the command:

`Welcome to Confidential Containers on AKS! Encrypted Kafka Message: Msg 1: Azure Confidential Computing`

You should also attempt to run the consumer as a regular Kubernetes pod by removing the

`skr container`

and`kata-cc runtime class`

spec. Since you aren't running the consumer with kata-cc runtime class, you no longer need the policy.Remove the entire policy and observe the messages again in the browser after redeploying the workload. Messages appear as base64-encoded ciphertext because the private encryption key can't be retrieved. The key can't be retrieved because the consumer is no longer running in a confidential environment, and the

`skr container`

is missing, preventing decryption of messages.

## Cleanup

When you're finished evaluating this feature, to avoid Azure charges, clean up your unnecessary resources. If you deployed a new cluster as part of your evaluation or testing, you can delete the cluster using the [az aks delete](/en-us/cli/azure/aks#az-aks-delete) command.

```
az aks delete --resource-group myResourceGroup --name myAKSCluster
```


If you enabled Confidential Containers (preview) on an existing cluster, you can remove the pod(s) using the [kubectl delete pod](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#delete) command.

```
kubectl delete pod pod-name
```


## Next steps

- Learn more about
[Azure Dedicated hosts](/en-us/azure/virtual-machines/dedicated-hosts)for nodes with your AKS cluster to use hardware isolation and control over Azure platform maintenance events.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-system-pools -->

# Manage system node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure Kubernetes Service (AKS), nodes of the same configuration are grouped together into *node pools*. Node pools contain the underlying VMs that run your applications. System node pools and user node pools are two different node pool modes for your AKS clusters. System node pools serve the primary purpose of hosting critical system pods such as `CoreDNS`

and `metrics-server`

. User node pools serve the primary purpose of hosting your application pods. However, application pods can be scheduled on system node pools if you wish to only have one pool in your AKS cluster. Every AKS cluster must contain at least one system node pool with at least two nodes.

Important

If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool.

This article explains how to manage system node pools in AKS. For information about how to use multiple node pools, see [use multiple node pools](use-multiple-node-pools).

## Before you begin

You need the Azure CLI version 2.3.1 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Limitations

The following limitations apply when you create and manage AKS clusters that support system node pools.

- See
[Quotas, VM size restrictions, and region availability in AKS](quotas-skus-regions). - An API version of 2020-03-01 or greater must be used to set a node pool mode. Clusters created on API versions older than 2020-03-01 contain only user node pools, but can be migrated to contain system node pools by following
[update pool mode steps](#update-existing-cluster-system-and-user-node-pools). - The name of a node pool may only contain lowercase alphanumeric characters and must begin with a lowercase letter. For Linux node pools, the length must be between 1 and 12 characters. For Windows node pools, the length must be between one and six characters.
- The mode of a node pool is a required property and must be explicitly set when using ARM templates or direct API calls.

## System and user node pools

For a system node pool, AKS automatically assigns the label **kubernetes.azure.com/mode: system** to its nodes. This causes AKS to prefer scheduling system pods on node pools that contain this label. This label doesn't prevent you from scheduling application pods on system node pools. However, we recommend you isolate critical system pods from your application pods to prevent misconfigured or rogue application pods from accidentally deleting system pods.

You can enforce this behavior by creating a dedicated system node pool. Use the `CriticalAddonsOnly=true:NoSchedule`

taint to prevent application pods from being scheduled on system node pools.

System node pools have the following restrictions:

- System node pools must support at least 30 pods as described by the
[minimum and maximum value formula for pods](concepts-network-ip-address-planning#maximum-pods-per-node). - System pools osType must be Linux.
- User node pools osType may be Linux or Windows.
- System pools must contain at least two nodes, and user node pools may contain zero or more nodes.
- System node pools require a VM SKU of at least 4 vCPUs and 4GB memory.
[B series VMs](/en-us/azure/virtual-machines/sizes-b-series-burstable)are not supported for system node pools.- A minimum of three nodes of 8 vCPUs or two nodes of at least 16 vCPUs is recommended (for example, Standard_DS4_v2), especially for large clusters (Multiple CoreDNS Pod replicas, 3-4+ add-ons, etc.).
- Spot node pools require user node pools.
- Adding another system node pool or changing which node pool is a system node pool
*does not*automatically move system pods. System pods can continue to run on the same node pool, even if you change it to a user node pool. If you delete or scale down a node pool running system pods that were previously a system node pool, those system pods are redeployed with preferred scheduling to the new system node pool.

You can do the following operations with node pools:

- Create a dedicated system node pool (prefer scheduling of system pods to node pools of
`mode:system`

) - Change a system node pool to be a user node pool, provided you have another system node pool to take its place in the AKS cluster.
- Change a user node pool to be a system node pool.
- Delete user node pools.
- You can delete system node pools, provided you have another system node pool to take its place in the AKS cluster.
- An AKS cluster may have multiple system node pools and requires at least one system node pool.
- If you want to change various immutable settings on existing node pools, you can create new node pools to replace them. One example is to add a new node pool with a new maxPods setting and delete the old node pool.
- Use
[node affinity](operator-best-practices-advanced-scheduler#node-affinity)to*require*or*prefer*which nodes can be scheduled based on node labels. You can set`key`

to`kubernetes.azure.com`

,`operator`

to`In`

, and`values`

of either`user`

or`system`

to your YAML, applying this definition using`kubectl apply -f yourYAML.yaml`

.

## Create a new AKS cluster with a system node pool

When you create a new AKS cluster, the initial node pool defaults to a mode of type `system`

. When you create new node pools with `az aks nodepool add`

, those node pools are user node pools unless you explicitly specify the mode parameter.

The following example creates a resource group named *myResourceGroup* in the *eastus* region.

```
az group create --name myResourceGroup --location eastus
```


Use the [az aks create](/en-us/cli/azure/aks#az-aks-create) command to create an AKS cluster. The following example creates a cluster named *myAKSCluster* with one dedicated system pool containing two nodes. For your production workloads, ensure you're using system node pools with at least three nodes. This operation may take several minutes to complete.

```
# Create a new AKS cluster with a single system pool
az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 2 --generate-ssh-keys
```


## Add a dedicated system node pool to an existing AKS cluster

You can add one or more system node pools to existing AKS clusters. It's recommended to schedule your application pods on user node pools, and dedicate system node pools to only critical system pods. This prevents rogue application pods from accidentally deleting system pods. Enforce this behavior with the `CriticalAddonsOnly=true:NoSchedule`

[taint](manage-node-pools#set-node-pool-taints) for your system node pools.

The following command adds a dedicated node pool of mode type system with a default count of three nodes.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name systempool \
--node-count 3 \
--node-taints CriticalAddonsOnly=true:NoSchedule \
--mode System
```


## Show details for your node pool

You can check the details of your node pool with the following command.

```
az aks nodepool show --resource-group myResourceGroup --cluster-name myAKSCluster --name systempool
```


A mode of type **System** is defined for system node pools, and a mode of type **User** is defined for user node pools. For a system pool, verify the taint is set to `CriticalAddonsOnly=true:NoSchedule`

, which will prevent application pods from beings scheduled on this node pool.

```
{
"agentPoolType": "VirtualMachineScaleSets",
"availabilityZones": null,
"count": 3,
"enableAutoScaling": null,
"enableNodePublicIp": false,
"id": "/subscriptions/yourSubscriptionId/resourcegroups/myResourceGroup/providers/Microsoft.ContainerService/managedClusters/myAKSCluster/agentPools/systempool",
"maxCount": null,
"maxPods": 110,
"minCount": null,
"mode": "System",
"name": "systempool",
"nodeImageVersion": "AKSUbuntu-1604-2020.06.30",
"nodeLabels": {},
"nodeTaints": [
"CriticalAddonsOnly=true:NoSchedule"
],
"orchestratorVersion": "1.16.10",
"osDiskSizeGb": 128,
"osType": "Linux",
"provisioningState": "Succeeded",
"proximityPlacementGroupId": null,
"resourceGroup": "myResourceGroup",
"scaleSetEvictionPolicy": null,
"scaleSetPriority": null,
"spotMaxPrice": null,
"tags": null,
"type": "Microsoft.ContainerService/managedClusters/agentPools",
"upgradeSettings": {
"maxSurge": null
},
"vmSize": "Standard_DS2_v2",
"vnetSubnetId": null
}
```


## Update existing cluster system and user node pools

Note

An API version of 2020-03-01 or greater must be used to set a system node pool mode. Clusters created on API versions older than 2020-03-01 contain only user node pools as a result. To receive system node pool functionality and benefits on older clusters, update the mode of existing node pools with the following commands on the latest Azure CLI version.

You can change modes for both system and user node pools. You can change a system node pool to a user pool only if another system node pool already exists on the AKS cluster.

This command changes a system node pool to a user node pool.

```
az aks nodepool update --resource-group myResourceGroup --cluster-name myAKSCluster --name mynodepool --mode user
```


This command changes a user node pool to a system node pool.

```
az aks nodepool update --resource-group myResourceGroup --cluster-name myAKSCluster --name mynodepool --mode system
```


## Delete a system node pool

Note

To use system node pools on AKS clusters before API version 2020-03-02, add a new system node pool, then delete the original default node pool.

You must have at least two system node pools on your AKS cluster before you can delete one of them.

```
az aks nodepool delete --resource-group myResourceGroup --cluster-name myAKSCluster --name mynodepool
```


## Clean up resources

To delete the cluster, use the [az group delete](/en-us/cli/azure/group#az-group-delete) command to delete the AKS resource group:

```
az group delete --name myResourceGroup --yes --no-wait
```


## Next steps

In this article, you learned how to create and manage system node pools in an AKS cluster. For information about how to start and stop AKS node pools, see [start and stop AKS node pools](start-stop-nodepools).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning -->

# Overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS), including how it works, upgrade behavior, prerequisites, limitations, and resources to get started.

## What is node auto-provisioning in AKS?

When you deploy workloads onto AKS, you need to select the appropriate virtual machine (VM) size as part of your node pool configuration. As your workloads become more complex, you might have different workloads with varying resource requirements, which makes it more difficult to design your VM configuration for numerous resource requests.

Node auto-provisioning (NAP) simplifies this process by automatically provisioning and managing the optimal VM configuration for your workloads. NAP uses pending pod resource requirements to decide the optimal VM configuration to run your workloads in the most efficient and cost-effective manner.

NAP automatically deploys, configures, and manages Karpenter on your AKS clusters and is based on the open-source [Karpenter](https://karpenter.sh) and [AKS Karpenter provider](https://github.com/Azure/karpenter-provider-azure) projects.

## How does node auto-provisioning work?

Node auto-provisioning provisions, scales, and manages VMs (nodes) in a cluster in response to pending pod pressure.

### Key components of node auto-provisioning

NAP uses the following key components to help manage your cluster's nodes:

| Component | Description |
|---|---|
`NodePool` and `AKSNodeClass` |
Custom Resource Definitions (CRDs) that you create and manage to define node provisioning policies, VM specifications, and constraints for your workloads. |
`NodeClaims` |
Managed by NAP to represent the current state of provisioned nodes that you can monitor. |
| Workload resource requirements | CPU, memory, and other specifications from your Pods, Deployments, Jobs, and other Kubernetes resources that drive provisioning decisions. |

## Kubernetes upgrade behavior for node auto-provisioning nodes

Kubernetes upgrades for node auto-provisioning nodes follow the control plane Kubernetes version. If you perform a cluster upgrade, your nodes are automatically updated to follow the same versioning as your control plane.

We recommend setting a Kubernetes [auto-upgrade](/en-us/azure/aks/auto-upgrade-cluster#cluster-auto-upgrade-channels) channel, which automatically handles Kubernetes upgrades for your cluster. We also recommend setting a [planned maintenance window](planned-maintenance#create-a-maintenance-window) for your cluster. The `aksManagedAutoUpgradeSchedule`

maintenance window allows you to control when to perform cluster upgrades scheduled by your designated auto-upgrade channel. For more information, see [Use planned maintenance to schedule and control upgrades for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Prerequisites

To use node auto-provisioning in AKS, you need the following prerequisites:

- An Azure subscription. If you don't have one, you can create a
[free account](https://azure.microsoft.com/free). - Azure CLI version
`2.76.0`

or later. To find the version, run`az --version`

. For more information about installing or upgrading the Azure CLI, see[Install Azure CLI](/en-us/cli/azure/get-started-with-azure-cli).

## Limitations and unsupported features

The following limitations and unsupported features apply to node auto-provisioning in AKS:

- You can't enable NAP on clusters enabled with the
[cluster autoscaler](cluster-autoscaler). - Windows node pools aren't supported.
- IPv6 clusters aren't supported.
[Service principals](kubernetes-service-principal)aren't supported. You can use either a system-assigned or user-assigned managed identity.[Custom certificate authority (CA) certificates](custom-certificate-authority)aren't supported.- You can't
[stop a cluster](start-stop-cluster)enabled with NAP. [HTTP proxy](http-proxy)isn't supported.- You can't change the
[cluster egress outbound type](egress-outboundtype)after you create a cluster enabled with NAP. - When creating a NAP cluster in a custom virtual network (VNet), you must use a
[Standard Load Balancer](load-balancer-standard). The Basic Load Balancer isn't supported.

## Get started with node auto-provisioning on AKS

The following resources help you get started with node auto-provisioning on AKS:

[Enable or disable node auto-provisioning on an AKS cluster](use-node-auto-provisioning)[Use node auto-provisioning in a custom virtual network](node-auto-provisioning-custom-vnet)[Configure networking for node auto-provisioning on AKS](node-auto-provisioning-networking)[Configure node pools for node auto-provisioning on AKS](node-auto-provisioning-node-pools)[Configure disruption policies for node auto-provisioning on AKS](node-auto-provisioning-disruption)[Upgrade node images for node auto-provisioning on AKS](node-auto-provisioning-upgrade-image)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-cluster-isolation -->

# Best practices for cluster isolation in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you manage clusters in Azure Kubernetes Service (AKS), you often need to isolate teams and workloads. AKS allows flexibility in how you run multi-tenant clusters and isolate resources. To maximize your investment in Kubernetes, it's important you understand AKS multi-tenancy and isolation features.

This best practices article focuses on isolation for cluster operators. In this article, you learn how to:

- Plan for multi-tenant clusters and separation of resources.
- Use logical or physical isolation in your AKS clusters.

## Design clusters for multi-tenancy

Kubernetes lets you logically isolate teams and workloads in the same cluster. The goal is to provide the least number of privileges scoped to the resources each team needs. A Kubernetes [Namespace](concepts-clusters-workloads#namespaces) creates a logical isolation boundary. Other Kubernetes features and considerations for isolation and multi-tenancy include the following areas:

### Scheduling

*Scheduling* uses basic features like resource quotas and pod disruption budgets. For more information about these features, see [Best practices for basic scheduler features in AKS](operator-best-practices-scheduler).

More advanced scheduler features include:

- Taints and tolerations.
- Node selectors.
- Node and pod affinity or anti-affinity.

For more information about these features, see [Best practices for advanced scheduler features in AKS](operator-best-practices-advanced-scheduler).

### Networking

*Networking* uses network policies to control the flow of traffic in and out of pods.

For more information, see [Secure traffic between pods using network policies in AKS](use-network-policies).

### Authentication and authorization

*Authentication and authorization* uses:

- Role-based access control (RBAC).
- Microsoft Entra integration.
- Pod identities.
- Secrets in Azure Key Vault.

For more information about these features, see [Best practices for authentication and authorization in AKS](operator-best-practices-identity).

### Containers

*Containers* include:

- The Azure Policy add-on for AKS to enforce pod security.
- Pod security admission.
- Scanning images and runtime for vulnerabilities.
- Using App Armor or Seccomp (Secure Computing) to restrict container access to the underlying node.

## Logically isolated clusters


Best practice guidanceSeparate teams and projects using

logical isolation. Minimize the number of physical AKS clusters you deploy to isolate teams or applications.

With logical isolation, you can use a single AKS cluster for multiple workloads, teams, or environments. Kubernetes [Namespaces](concepts-clusters-workloads#namespaces) form the logical isolation boundary for workloads and resources.

Logical separation of clusters usually provides a higher pod density than physically isolated clusters, with less excess compute capacity sitting idle in the cluster. When combined with the Kubernetes cluster autoscaler, you can scale the number of nodes up or down to meet demands. This best practice approach minimizes costs by running only the required number of nodes.

Kubernetes environments aren't entirely safe for hostile multi-tenant usage. In a multi-tenant environment, multiple tenants work on a shared infrastructure. If all tenants can't be trusted, you need extra planning to prevent tenants from impacting the security and service of others.

Other security features, like Kubernetes RBAC for nodes, efficiently block exploits. For true security when running hostile multi-tenant workloads, you should only trust a hypervisor. The security domain for Kubernetes becomes the entire cluster and not an individual node.

For these types of hostile multi-tenant workloads, you should use physically isolated clusters.

## Physically isolated clusters


Best practice guidanceMinimize the use of physical isolation for each separate team or application deployment and use

logicalisolation instead.

Physically separating AKS clusters is a common approach to cluster isolation. In this isolation model, teams or workloads are assigned their own AKS cluster. While physical isolation might look like the easiest way to isolate workloads or teams, it adds management and financial overhead. With physically isolated clusters, you must maintain multiple clusters and individually provide access and assign permissions. You're also billed for each individual node.

Physically isolated clusters usually have a low pod density. Since each team or workload has their own AKS cluster, the cluster is often over-provisioned with compute resources. Often, a few pods are scheduled on those nodes. Unclaimed node capacity can't be used for applications or services in development by other teams. These excess resources contribute to the extra costs in physically isolated clusters.

## Next steps

This article focused on cluster isolation. For more information about cluster operations in AKS, see the following best practice articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/virtual-machines-node-pools -->

# Use Virtual Machines node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you'll learn about the new Virtual Machines node pool type for AKS.

With Virtual Machines node pools, AKS directly manages the provisioning and bootstrapping of every single node. For Virtual Machine Scale Sets node pools, AKS manages the model of the Virtual Machine Scale Sets and uses it to achieve consistency across all nodes in the node pool. Virtual Machines node pools enable you to orchestrate your cluster with virtual machines that best fit your individual workloads.

## Overview

### How it works

A node pool consists of a set of virtual machines, where different virtual machine sizes are designated to support different types of workloads. These virtual machine sizes, referred to as SKUs, are categorized into different families that are optimized for specific purposes. For more information, see [VM SKUs](/en-us/azure/virtual-machines/sizes/overview).

To enable scaling of multiple virtual machine sizes, the Virtual Machines node pool type uses a `ScaleProfile`

that contains configurations indicating how the node pool can scale, specifically the desired list of virtual machine size and the count of each size. A `ManualScaleProfile`

is a scale profile that specifies one desired virtual machine size and the total count of that type in the nodepool. Only one virtual machine size is allowed in a `ManualScaleProfile`

. You need to create a separate `ManualScaleProfile`

for each virtual machine size in your node pool. When creating a new Virtual Machines node pool, you add an initial manual scale profile for a virtual machine size using the `vm-size`

field and including a `node-count`

, per the instructions below. You can also add additional manual scale profiles following the instructions for [adding manual scale profiles](/en-us/azure/aks/virtual-machines-node-pools#add-a-manual-scale-profile-to-a-node-pool).

Note

When creating a new Virtual Machines node pool, you can have multiple scale profiles, and you need at least one manual scale profile in your nodepool.

### Advantages

Advantages of the Virtual Machines node pool type include:

**Flexibility**: Node specifications can be updated to adapt to your current workload and needs.**Fine-tuned control**: Single node-level controls allow specifying and mixing nodes of different specs to lift restrictions from a single model and improve consistency.**Efficiency**: You can reduce the node footprint for your cluster, simplifying your operational requirements.

Virtual Machines node pools provide a better experience for dynamic workloads and high availability requirements. Virtual Machines node pools enable you to set up multiple similar-family virtual machines in one node pool. Your workload will be automatically scheduled on the available resources that you configure.

### Feature comparison

The following table highlights how Virtual Machines node pools compare with standard [Scale Set](/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-orchestration-modes) node pools.

| Node pool type | Capabilities |
|---|---|
| Virtual Machines node pool | You can add, remove, or update nodes in a node pool. Virtual machine types can be any virtual machine of the same family type (for example, D-series, A-Series, etc.). |
| Virtual Machine Scale Set based node pool | You can add or remove nodes of the same size and type in a node pool. If you add a new virtual machine size to the cluster, you need to create a new node pool. |

### Limitations

[Cluster autoscaler](cluster-autoscaler-overview)is currently not supported.[InifiniBand](/en-us/azure/virtual-machines/extensions/enable-infiniband)isn't available.[Node pool snapshot](node-pool-snapshot)isn't supported.- All VM sizes selected in a node pool need to be from a similar virtual machine family. For example, you can't mix an N-Series virtual machine type with a D-Series virtual machine type in the same node pool.
- Virtual Machines node pools allow up to five different virtual machine sizes per node pool.

## Prerequisites

- An Azure subscription. If you don't have one, you can
[create a free account](https://azure.microsoft.com/free). - Azure CLI version 2.73.0 or later installed and configured. To find the version, run
`az --version`

. For more information about installing or upgrading the Azure CLI, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli#install-azure-cli) - This feature requires kubernetes version 1.27 or greater. To upgrade your kubernetes version, see
[Upgrade AKS cluster](upgrade-aks-cluster)

## Create an AKS cluster with Virtual Machines node pools

Note

Only *one* VM size is allowed in a scale profile, and the maximum limit is *five* VM scale profiles overall for a Virtual Machines node pool.

Create an AKS cluster with Virtual Machines node pools using the

command with the`az aks create`

`--vm-set-type`

flag set to`"VirtualMachines"`

.The following example creates a cluster named

*myAKSCluster*with a Virtual Machines node pool containing two nodes, generates SSH keys, sets the load balancer SKU to*standard*, and sets the Kubernetes version to*1.31.0*:`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --vm-set-type "VirtualMachines" \ --vm-sizes "Standard_D4s_v3" --node-count 2 \ --kubernetes-version 1.31.0`


## Create a cluster with Windows enabled and a Windows Virtual Machine node pool

Virtual Machine node pools are available in Windows enabled clusters. The following example creates a cluster named *myAKSCluster* with a Virtual Machines node pool. These steps create a Linux system pool at first.

Create a username to use as administrator credentials for the Windows Server nodes on your cluster. The following commands prompt you for a username and sets it to

*WINDOWS_USERNAME*for use in a later command.`echo "Please enter the username to use as administrator credentials for Windows Server nodes on your cluster: " && read WINDOWS_USERNAME`

Create a password for the administrator username you created in the previous step. The password must be a minimum of 14 characters and meet the

[Windows Server password complexity requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference).`echo "Please enter the password to use as administrator credentials for Windows Server nodes on your cluster: " && read WINDOWS_PASSWORD`

Create an AKS cluster with Windows enabled and Virtual Machines type node pools using the

command with the`az aks create`

`--vm-set-type`

flag set to`"VirtualMachines"`

.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 2 \ --enable-addons monitoring \ --generate-ssh-keys \ --windows-admin-username $WINDOWS_USERNAME \ --windows-admin-password $WINDOWS_PASSWORD \ --vm-set-type "VirtualMachines" \ --network-plugin azure`

Add a Virtual Machines node pool to an existing Windows enabled cluster using the

command with the`az aks nodepool add`

`--vm-set-type`

flag set to`"VirtualMachines"`

. The following example adds a Virtual Machines node pool named*npwin*to the*myAKSCluster*cluster:`az aks nodepool add --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --os-type Windows \ --name npwin \ --vm-sizes "Standard_D2s_V3" \ --node-count 1 --vm-set-type "VirtualMachines"`


## Add a Virtual Machines node pool to an existing cluster

Add a Virtual Machines node pool to an existing cluster using the

command with the`az aks nodepool add`

`--vm-set-type`

flag set to`"VirtualMachines"`

.The following example adds a Virtual Machines node pool named

*myvmpool*to the*myAKSCluster*cluster. The node pool creates a ManualScaleProfile with`--vm-sizes`

set to*Standard_D4s_v3*and a`--node-count`

of 3:`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myvmpool \ --vm-set-type "VirtualMachines" \ --vm-sizes "Standard_D4s_v3" \ --node-count 3`


## Add a manual scale profile to a node pool

Add a manual scale profile to a node pool using the

with the`az aks nodepool manual-scale add`

`--vm-sizes`

flag set to`"Standard_D2s_v3"`

and the`node-count`

set to 2.The following example adds a manual scale profile to node pool

*myvmpool*in cluster*myAKSCluster*. The node pool includes two nodes with a VM SKU of*Standard_D2s_v3*:`az aks nodepool manual-scale add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myvmpool \ --vm-sizes "Standard_D2s_v3" \ --node-count 2`


## Update an existing manual scale profile

Update an existing manual scale profile in a node pool using the

command with the`az aks nodepool manual-scale update`

`--vm-sizes`

flag set to`"Standard_D2s_v3"`

.Note

Use the

`--current-vm-sizes`

parameter to specify the size of the existing node pool that you want to update. You can update`--vm-sizes`

and/or`--node-count`

. When using other tools or REST APIs, you need to pass in a full`agentPoolProfiles.virtualMachinesProfile.scale`

field when updating the node pool scale profile.The following example updates a manual scale profile to the

*myvmpool*node pool in the*myAKSCluster*cluster. The command updates the number of nodes to five and changes the VM SKU from*Standard_D4s_v3*to*Standard_D8s_v3*:`az aks nodepool manual-scale update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myvmpool \ --current-vm-sizes "Standard_D4s_v3" \ --vm-sizes "Standard_D8s_v3" \ --node-count 5`


## Delete a manual scale profile

Delete an existing manual scale profile using the

command.`az aks nodepool manual-scale delete`

Note

The

`--current-vm-sizes`

parameter specifies the size of the existing node pool to be deleted. When using other tools or REST APIs to update the node pool scale profile, pass in a full`agentPoolProfiles.virtualMachinesProfile.scale`

field.The following example deletes the manual scale profile for the

*Standard_D8s_v3*VM SKU in the*myvmpool*node pool.`az aks nodepool manual-scale delete \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myvmpool \ --current-vm-sizes "Standard_D8s_v3"`


## Next steps

In this article, you learned how to use Virtual Machines node pools in AKS. To learn more about node pools in AKS, see [Create node pools](create-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-windows-os -->

# Upgrade the operating system (OS) version for your Azure Kubernetes Service (AKS) Windows workloads

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When upgrading the OS version of a running Windows workload on Azure Kubernetes Service (AKS), you need to deploy a new node pool to ensure the Windows versions match on each node pool. This article describes the steps to upgrade the OS version for Windows workloads on AKS.

## Windows Server OS version support

When a new Windows Server OS version is released, AKS is committed to supporting it. We recommend that you upgrade to the latest version to take advantage of the fixes, improvements, and new functionality. AKS provides a five-year support lifecycle for every Windows Server version, starting with Windows Server 2022. During this period, AKS releases a new version that supports a newer version of Windows Server OS for you to upgrade to. After the five-year lifecycle ends, you must migrate workloads to newer supported versions to ensure compatibility, security updates, and continued support from AKS.

Important

Starting on March 01, 2026, Azure Kubernetes Service (AKS) no longer supports Windows Server 2019 node pools. Node pools running Kubernetes version 1.33+ can't use Windows Server 2019. Starting on April 01, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4091) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=aks-will-stop-support-for-windows-server-2019-on-march-1-2026). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on March 15, 2027, Azure Kubernetes Service (AKS) no longer supports Windows Server 2022 node pools. Node pools running Kubernetes version 1.36+ can't use Windows Server 2022. Starting on April 01, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4168) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=ws2022-retirement-aks). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Limitations

- Node pool update to migrate from one Windows Server version to another isn't supported.
- Different Windows Server versions can't coexist on the same node pool on AKS. You need to create a new node pool to host the new OS version. It's important that you match the permissions and access of the previous node pool to the new one.
- Windows Server 2025 (preview) is supported starting in Kubernetes version 1.32.

## Before you begin

- Update the
`FROM`

statement in your Dockerfile to the new OS version. - Check your application and verify the container app works on the new OS version.
- Deploy the verified container app on AKS to a development or testing environment.
- Take note of the new image name or tag for use in this article.

Note

To learn how to build a Dockerfile for Windows workloads, see [Dockerfile on Windows](/en-us/virtualization/windowscontainers/manage-docker/manage-windows-dockerfile) and [Optimize Windows Dockerfiles](/en-us/virtualization/windowscontainers/manage-docker/optimize-windows-dockerfile).

### Install `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


### Register `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using the [`az feature register`

][az-feature-register] command.`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the [

`az feature show`

][az-feature-show] command. It takes a few minutes for the status to show*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using the [`az provider register`

][az-provider-register] command.`az provider register --namespace Microsoft.ContainerService`


## Add a new node pool to an existing cluster

Add a node pool with your desired OS version to your existing cluster:

[Use CLI to add a Windows node pool](learn/quick-windows-container-deploy-cli)to an existing cluster.[Use Portal to add a Windows node pool](learn/quick-windows-container-deploy-portal)to an existing cluster.[Use PowerShell to add a Windows node pool](learn/quick-windows-container-deploy-powershell)to an existing cluster.[Use Terraform to add a Windows node pool](learn/quick-windows-container-deploy-terraform)to an existing cluster.

## Update the YAML file

Node Selector is the most common and recommended option for placement of Windows pods on Windows nodes.

Add Node Selector to your YAML file by adding the following annotation:

`nodeSelector: "kubernetes.io/os": windows`

The annotation finds any available Windows node and places the pod on that node (following all other scheduling rules). When upgrading your OS version, you need to enforce the placement on a Windows node and a node running the latest OS version. To accomplish this, one option is to use a different annotation. Update

`<OSSKU>`

to match the ossku your desired Windows OS version, for example`Windows2025`

.`nodeSelector: "kubernetes.azure.com/os-sku": <OSSKU>`

Once you update the

`nodeSelector`

in the YAML file, you also need to update the container image you want to use. You can get this information from the previous step in which you created a new version of the containerized application by changing the`FROM`

statement on your Dockerfile.Note

You should use the same YAML file you used to initially deploy the application. This ensures that no other configuration changes besides the

`nodeSelector`

and container image.

## Apply the updated YAML file to the existing workload

View the nodes on your cluster using the

`kubectl get nodes`

command.`kubectl get nodes -o wide`

The following example output shows all nodes on the cluster, including the new node pool you created and the existing node pools:

`NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME aks-agentpool-18877473-vmss000000 Ready agent 5h40m v1.23.8 10.240.0.4 <none> Ubuntu 18.04.6 LTS 5.4.0-1085-azure containerd://1.5.11+azure-2 akspoolws000000 Ready agent 3h15m v1.23.8 10.240.0.208 <none> Windows Server 2022 Datacenter 10.0.20348.825 containerd://1.6.6+azure akspoolws000001 Ready agent 3h17m v1.23.8 10.240.0.239 <none> Windows Server 2022 Datacenter 10.0.20348.825 containerd://1.6.6+azure akspoolws000002 Ready agent 3h17m v1.23.8 10.240.1.14 <none> Windows Server 2022 Datacenter 10.0.20348.825 containerd://1.6.6+azure akswspool000000 Ready agent 5h37m v1.23.8 10.240.0.115 <none> Windows Server 2019 Datacenter 10.0.17763.3165 containerd://1.6.6+azure akswspool000001 Ready agent 5h37m v1.23.8 10.240.0.146 <none> Windows Server 2019 Datacenter 10.0.17763.3165 containerd://1.6.6+azure akswspool000002 Ready agent 5h37m v1.23.8 10.240.0.177 <none> Windows Server 2019 Datacenter 10.0.17763.3165 containerd://1.6.6+azure`

Apply the updated YAML file to the existing workload using the

`kubectl apply`

command and specify the name of the YAML file.`kubectl apply -f <filename>`

The following example output shows a

*configured*status for the deployment:`deployment.apps/sample configured service/sample unchanged`

At this point, AKS starts the process of terminating the existing pods and deploying new pods to the nodes with the

`nodeSelector`

annotation.Check the status of the deployment using the

`kubectl get pods`

command.`kubectl get pods -o wide`

The following example output shows the pods in the

`default`

namespace:`NAME READY STATUS RESTARTS AGE IP NODE NOMINATED NODE READINESS GATES sample-7794bfcc4c-k62cq 1/1 Running 0 2m49s 10.240.0.238 akspoolws000000 <none> <none> sample-7794bfcc4c-rswq9 1/1 Running 0 2m49s 10.240.1.10 akspoolws000001 <none> <none> sample-7794bfcc4c-sh78c 1/1 Running 0 2m49s 10.240.0.228 akspoolws000000 <none> <none>`


## Security and authentication considerations

If you're using Group Managed Service Accounts (gMSA), you need to update the Managed Identity configuration for the new node pool. gMSA uses a secret (user account and password) so the node that runs the Windows pod can authenticate the container against Microsoft Entra ID. To access that secret on Azure Key Vault, the node uses a Managed Identity that allows the node to access the resource. Since Managed Identities are configured per node pool, and the pod now resides on a new node pool, you need to update that configuration. For more information, see [Enable Group Managed Service Accounts (GMSA) for your Windows Server nodes on your Azure Kubernetes Service (AKS) cluster](use-group-managed-service-accounts).

The same principle applies to Managed Identities for any other pod or node pool when accessing other Azure resources. You need to update any access that Managed Identity provides to reflect the new node pool. To view update and sign-in activities, see [How to view Managed Identity activity](/en-us/azure/active-directory/managed-identities-azure-resources/how-to-view-managed-identity-activity).

## Next steps

In this article, you learned how to upgrade the OS version for Windows workloads on AKS. To learn more about Windows workloads on AKS, see [Deploy a Windows container application on Azure Kubernetes Service (AKS)](learn/quick-windows-container-deploy-cli).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/confidential-containers-overview -->

# Confidential Containers (preview) with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Confidential Containers preview is set to sunset in **March 2026**. After this date, customers with existing Confidential Container node pools should expect to see reduced functionality, and you won't be able to spin up any new nodes with the `KataCcIsolation`

runtime. Customers currently using Confidential Container node pools can continue using them as normal. If you want to move off Confidential Containers, consider the following alternatives:

[Confidential VMs on AKS](/en-us/azure/confidential-computing/confidential-node-pool-aks): Offers a similar hardware-based TEE that leverages AMD SEV-SNP security features, without the addition of per-VM isolation for workloads seen in Confidential Containers.[Application enclave support](/en-us/azure/confidential-computing/confidential-nodes-aks-overview): Provides users with Intel SGX confidential computing VM nodes that support hardware-based, process-level container isolation through the Intel SGX trusted execution environment.[Confidential Containers on Azure Container Instances](/en-us/azure/confidential-computing/confidential-containers): Allows for lift-and-shift deployments on containers backed by AMD SEV-SNP. Functionality includes performing full guest attestation, access to toolings to generate policies, and utilizing sidecar containers for secure key releases. ACI nodes can be run on AKS via[virtual nodes](/en-us/azure/container-instances/container-instances-virtual-nodes).[Azure RedHat OpenShift Confidential Containers](/en-us/azure/openshift/confidential-containers-overview): Offers a similar AMD SEV-SNP backed TEE and utilizes the Kata runtime for per-container level isolation.[Open source Confidential Containers](https://github.com/confidential-containers): Gives a similar AMD SEV-SNP backed TEE that comes with per-container isolation through Kata.

If you have additional questions, please create a [support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest) or post an issue in [AKS issues](https://github.com/Azure/AKS/issues).

Confidential Containers provide a set of features and capabilities to further secure your standard container workloads to achieve higher data security, data privacy and runtime code integrity goals. Azure Kubernetes Service (AKS) includes Confidential Containers (preview) on AKS.

Confidential Containers builds on Kata Confidential Containers and hardware-based encryption to encrypt container memory. It establishes a new level of data confidentiality by preventing data in memory during computation from being in clear text, readable format. Trust is earned in the container through hardware attestation, allowing access to the encrypted data by trusted entities.

Together with [Pod Sandboxing](use-pod-sandboxing), you can run sensitive workloads isolated in Azure to protect your data and workloads. What makes a container confidential:

- Transparency: The confidential container environment where your sensitive application is shared, you can see and verify if it's safe. All components of the Trusted Computing Base (TCB) are to be open sourced.
- Auditability: You have the ability to verify and see what version of the CoCo environment package including Linux Guest OS and all the components are current. Microsoft signs to the guest OS and container runtime environment for verifications through attestation. It also releases a secure hash algorithm (SHA) of guest OS builds to build a string audibility and control story.
- Full attestation: Anything that is part of the TEE shall be fully measured by the CPU with ability to verify remotely. The hardware report from AMD SEV-SNP processor shall reflect container layers and container runtime configuration hash through the attestation claims. Application can fetch the hardware report locally including the report that reflects Guest OS image and container runtime.
- Code integrity: Runtime enforcement is always available through customer defined policies for containers and container configuration, such as immutable policies and container signing.
- Isolation from operator: Security designs that assume least privilege and highest isolation shielding from all untrusted parties including customer/tenant admins. It includes hardening existing Kubernetes control plane access (kubelet) to confidential pods.

With other security measures or data protection controls, as part of your overall architecture, these capabilities help you meet regulatory, industry, or governance compliance requirements for securing sensitive information.

This article helps you understand the Confidential Containers feature, and how to implement and configure the following:

- Deploy or upgrade an AKS cluster using the Azure CLI
- Add an annotation to your pod YAML to mark the pod as being run as a confidential container
- Add a
[security policy](/en-us/azure/confidential-computing/confidential-containers-aks-security-policy)to your pod YAML - Deploy your application in confidential computing

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Supported scenarios

Confidential Containers (preview) are appropriate for deployment scenarios that involve sensitive data. For example, personally identifiable information (PII) or any data with strong security needed for regulatory compliance. Some common scenarios with containers are:

- Run big data analytics using Apache Spark for fraud pattern recognition in the financial sector.
- Running self-hosted GitHub runners to securely sign code as part of Continuous Integration and Continuous Deployment (CI/CD) DevOps practices.
- Machine Learning inferencing and training of ML models using an encrypted data set from a trusted source. It only decrypts inside a confidential container environment to preserve privacy.
- Building big data clean rooms for ID matching as part of multi-party computation in industries like retail with digital advertising.
- Building confidential computing Zero Trust landing zones to meet privacy regulations for application migrations to cloud.

## Considerations

The following are considerations with this preview of Confidential Containers:

- An increase in pod startup time compared to runc pods and kernel-isolated pods.
- Version 1 container images aren't supported.
- Ephemeral containers and other troubleshooting methods like
`exec`

into a container, log outputs from containers, and`stdio`

require a policy modification and redeployment to enable ExecProcessRequest, ReadStreamRequest, WriteStreamRequest, and CloseStdinRequest. - Due to container image layer measurements being encoded in the security policy, we don't recommend using the
`latest`

tag when specifying containers. - Services, Load Balancers, and EndpointSlices only support the TCP protocol.
- The policy generator only supports pods that use IPv4 addresses.
- Pod environment variables based on ConfigMaps and Secrets can't be changed after the pod is deployed.
- Pod termination logs aren't supported. While pods write termination logs to
`/dev/termination-log`

or to a custom location if specified in the pod manifest, the host/kubelet can't read those logs. Changes from the pod to that file aren't reflected on the host. - Confidential Containers currently only supports Azure Linux.

## Resource allocation overview

It's important you understand the memory and processor resource allocation behavior in this release.

- CPU: The shim assigns one vCPU to the base OS inside the pod. If no resource
`limits`

are specified, the workloads don't have separate CPU shares assigned, the vCPU is then shared with that workload. If CPU limits are specified, CPU shares are explicitly allocated for workloads. - Memory: The Kata-CC handler uses 2 GB memory for the UVM OS and X MB additional memory where X is the resource
`limits`

if specified in the YAML manifest (resulting in a 2-GB VM when no limit is given, without implicit memory for containers). The[Kata](https://katacontainers.io/docs/)handler uses 256 MB base memory for the UVM OS and X MB additional memory when resource`limits`

are specified in the YAML manifest. If limits are unspecified, an implicit limit of 1,792 MB is added resulting in a 2 GB VM and 1,792 MB implicit memory for containers.

In this release, specifying resource requests in the pod manifests isn't supported. containerd doesn't pass the requests to the Kata Shim, and as a result, reserving resources based on the pod manifest resource requests is not implemented. Use resource `limits`

instead of resource `requests`

to allocate memory or CPU resources for workloads or containers.

With the local container filesystem backed by VM memory, writing to the container filesystem (including logging) can fill up the available memory provided to the pod. This condition can result in potential pod crashes.

## Next steps

- See the overview of
[Confidential Containers security policy](/en-us/azure/confidential-computing/confidential-containers-aks-security-policy)to learn about how workloads and their data in a pod is protected. [Deploy Confidential Containers on AKS](deploy-confidential-containers-default-policy)with an automatically generated security policy.- Learn more about
[Azure Dedicated hosts](/en-us/azure/virtual-machines/dedicated-hosts)for nodes with your AKS cluster to use hardware isolation and control over Azure platform maintenance events.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-windows-2019-2022 -->

# Upgrade the operating system (OS) version for your Azure Kubernetes Service (AKS) Windows workloads

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When upgrading the OS version of a running Windows workload on Azure Kubernetes Service (AKS), you need to deploy a new node pool to ensure the Windows versions match on each node pool. This article describes the steps to upgrade the OS version for Windows workloads on AKS.

## Windows Server OS version support

When a new Windows Server OS version is released, AKS is committed to supporting it. We recommend that you upgrade to the latest version to take advantage of the fixes, improvements, and new functionality. AKS provides a five-year support lifecycle for every Windows Server version, starting with Windows Server 2022. During this period, AKS releases a new version that supports a newer version of Windows Server OS for you to upgrade to. After the five-year lifecycle ends, you must migrate workloads to newer supported versions to ensure compatibility, security updates, and continued support from AKS.

Important

Starting on March 01, 2026, Azure Kubernetes Service (AKS) no longer supports Windows Server 2019 node pools. Node pools running Kubernetes version 1.33+ can't use Windows Server 2019. Starting on April 01, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4091) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=aks-will-stop-support-for-windows-server-2019-on-march-1-2026). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on March 15, 2027, Azure Kubernetes Service (AKS) no longer supports Windows Server 2022 node pools. Node pools running Kubernetes version 1.36+ can't use Windows Server 2022. Starting on April 01, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4168) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=ws2022-retirement-aks). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Limitations

- Node pool update to migrate from one Windows Server version to another isn't supported.
- Different Windows Server versions can't coexist on the same node pool on AKS. You need to create a new node pool to host the new OS version. It's important that you match the permissions and access of the previous node pool to the new one.
- Windows Server 2025 (preview) is supported starting in Kubernetes version 1.32.

## Before you begin

- Update the
`FROM`

statement in your Dockerfile to the new OS version. - Check your application and verify the container app works on the new OS version.
- Deploy the verified container app on AKS to a development or testing environment.
- Take note of the new image name or tag for use in this article.

Note

To learn how to build a Dockerfile for Windows workloads, see [Dockerfile on Windows](/en-us/virtualization/windowscontainers/manage-docker/manage-windows-dockerfile) and [Optimize Windows Dockerfiles](/en-us/virtualization/windowscontainers/manage-docker/optimize-windows-dockerfile).

### Install `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


### Register `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using the [`az feature register`

][az-feature-register] command.`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the [

`az feature show`

][az-feature-show] command. It takes a few minutes for the status to show*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using the [`az provider register`

][az-provider-register] command.`az provider register --namespace Microsoft.ContainerService`


## Add a new node pool to an existing cluster

Add a node pool with your desired OS version to your existing cluster:

[Use CLI to add a Windows node pool](learn/quick-windows-container-deploy-cli)to an existing cluster.[Use Portal to add a Windows node pool](learn/quick-windows-container-deploy-portal)to an existing cluster.[Use PowerShell to add a Windows node pool](learn/quick-windows-container-deploy-powershell)to an existing cluster.[Use Terraform to add a Windows node pool](learn/quick-windows-container-deploy-terraform)to an existing cluster.

## Update the YAML file

Node Selector is the most common and recommended option for placement of Windows pods on Windows nodes.

Add Node Selector to your YAML file by adding the following annotation:

`nodeSelector: "kubernetes.io/os": windows`

The annotation finds any available Windows node and places the pod on that node (following all other scheduling rules). When upgrading your OS version, you need to enforce the placement on a Windows node and a node running the latest OS version. To accomplish this, one option is to use a different annotation. Update

`<OSSKU>`

to match the ossku your desired Windows OS version, for example`Windows2025`

.`nodeSelector: "kubernetes.azure.com/os-sku": <OSSKU>`

Once you update the

`nodeSelector`

in the YAML file, you also need to update the container image you want to use. You can get this information from the previous step in which you created a new version of the containerized application by changing the`FROM`

statement on your Dockerfile.Note

You should use the same YAML file you used to initially deploy the application. This ensures that no other configuration changes besides the

`nodeSelector`

and container image.

## Apply the updated YAML file to the existing workload

View the nodes on your cluster using the

`kubectl get nodes`

command.`kubectl get nodes -o wide`

The following example output shows all nodes on the cluster, including the new node pool you created and the existing node pools:

`NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME aks-agentpool-18877473-vmss000000 Ready agent 5h40m v1.23.8 10.240.0.4 <none> Ubuntu 18.04.6 LTS 5.4.0-1085-azure containerd://1.5.11+azure-2 akspoolws000000 Ready agent 3h15m v1.23.8 10.240.0.208 <none> Windows Server 2022 Datacenter 10.0.20348.825 containerd://1.6.6+azure akspoolws000001 Ready agent 3h17m v1.23.8 10.240.0.239 <none> Windows Server 2022 Datacenter 10.0.20348.825 containerd://1.6.6+azure akspoolws000002 Ready agent 3h17m v1.23.8 10.240.1.14 <none> Windows Server 2022 Datacenter 10.0.20348.825 containerd://1.6.6+azure akswspool000000 Ready agent 5h37m v1.23.8 10.240.0.115 <none> Windows Server 2019 Datacenter 10.0.17763.3165 containerd://1.6.6+azure akswspool000001 Ready agent 5h37m v1.23.8 10.240.0.146 <none> Windows Server 2019 Datacenter 10.0.17763.3165 containerd://1.6.6+azure akswspool000002 Ready agent 5h37m v1.23.8 10.240.0.177 <none> Windows Server 2019 Datacenter 10.0.17763.3165 containerd://1.6.6+azure`

Apply the updated YAML file to the existing workload using the

`kubectl apply`

command and specify the name of the YAML file.`kubectl apply -f <filename>`

The following example output shows a

*configured*status for the deployment:`deployment.apps/sample configured service/sample unchanged`

At this point, AKS starts the process of terminating the existing pods and deploying new pods to the nodes with the

`nodeSelector`

annotation.Check the status of the deployment using the

`kubectl get pods`

command.`kubectl get pods -o wide`

The following example output shows the pods in the

`default`

namespace:`NAME READY STATUS RESTARTS AGE IP NODE NOMINATED NODE READINESS GATES sample-7794bfcc4c-k62cq 1/1 Running 0 2m49s 10.240.0.238 akspoolws000000 <none> <none> sample-7794bfcc4c-rswq9 1/1 Running 0 2m49s 10.240.1.10 akspoolws000001 <none> <none> sample-7794bfcc4c-sh78c 1/1 Running 0 2m49s 10.240.0.228 akspoolws000000 <none> <none>`


## Security and authentication considerations

If you're using Group Managed Service Accounts (gMSA), you need to update the Managed Identity configuration for the new node pool. gMSA uses a secret (user account and password) so the node that runs the Windows pod can authenticate the container against Microsoft Entra ID. To access that secret on Azure Key Vault, the node uses a Managed Identity that allows the node to access the resource. Since Managed Identities are configured per node pool, and the pod now resides on a new node pool, you need to update that configuration. For more information, see [Enable Group Managed Service Accounts (GMSA) for your Windows Server nodes on your Azure Kubernetes Service (AKS) cluster](use-group-managed-service-accounts).

The same principle applies to Managed Identities for any other pod or node pool when accessing other Azure resources. You need to update any access that Managed Identity provides to reflect the new node pool. To view update and sign-in activities, see [How to view Managed Identity activity](/en-us/azure/active-directory/managed-identities-azure-resources/how-to-view-managed-identity-activity).

## Next steps

In this article, you learned how to upgrade the OS version for Windows workloads on AKS. To learn more about Windows workloads on AKS, see [Deploy a Windows container application on Azure Kubernetes Service (AKS)](learn/quick-windows-container-deploy-cli).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/app-routing-dns-ssl -->

# Set up a custom domain name and SSL certificate with the application routing add-on for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to configure custom domain names and SSL/TLS certificates for AKS ingress using [Azure Key Vault](/en-us/azure/key-vault/general/overview) and [Azure DNS](/en-us/azure/dns/dns-overview) with the [application routing add-on for AKS](app-routing).

## Prerequisites

An AKS cluster with the

[application routing add-on](app-routing).Azure Key Vault if you want to configure SSL termination and store certificates in the vault hosted in Azure. If you don't have one, see

[Create a key vault using the Azure CLI](/en-us/azure/key-vault/general/quick-create-cli).To enable support for HTTPS traffic, you need an SSL certificate. If you don't have one, see

[create a certificate](#create-and-export-a-self-signed-ssl-certificate).Azure DNS if you want to configure global and private zone management and host them in Azure. If you don't have an Azure DNS zone, you can

[create one](#create-a-global-azure-dns-zone). To enable support for DNS zones:- All global Azure DNS zones need to be in the same resource group, which could be different from the cluster resource group.
- All private Azure DNS zones need to be in the same resource group, which could be different from the cluster resource group.
- The resource group doesn't need to be in the same subscription as the cluster.


### Required Azure permissions

**Your user account needs**: [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner), [Azure account administrator](/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles#classic-subscription-administrator-roles), or [Azure co-administrator](/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles#classic-subscription-administrator-roles) role on your Azure subscription.

**What the commands do**: When you run `az aks approuting update --attach-kv`

or `az aks approuting zone add --attach-zones`

, these commands use your role assignment permissions to automatically grant the application routing add-on's managed identity the following roles:

**Key Vault Certificate User**role on your Azure Key Vault (for certificate access).**DNS Zone Contributor**role on your Azure DNS zones (for DNS record management).

For more information on AKS managed identities, see [Summary of managed identities](managed-identity-overview#summary-of-managed-identities-used-by-aks).

## Connect to your AKS cluster

To connect to the Kubernetes cluster from your local computer, you use `kubectl`

, the Kubernetes command-line client. You can install it locally using the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. If you use the Azure Cloud Shell,

`kubectl`

is already installed.Configure kubectl to connect to your Kubernetes cluster using the

command.`az aks get-credentials`

`# Set environment variables for your resource group and cluster name export RESOURCE_GROUP=<resource-group-name> export CLUSTER_NAME=<cluster-name> # Get the AKS cluster credentials az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Create and export a self-signed SSL certificate

For testing, you can use a self-signed public certificate instead of a Certificate Authority (CA)-signed certificate. If you already have a certificate, you can skip this step.

Caution

Self-signed certificates are digital certificates that aren't signed by a trusted third-party CA. The company or developer responsible for the website or software creates, issues, and signs these certificates. This is why self-signed certificates are considered unsafe for public-facing websites and applications. Azure Key Vault has a [trusted partnership with the some Certificate Authorities](/en-us/azure/key-vault/certificates/how-to-integrate-certificate-authority).

Create a self-signed SSL certificate to use with the ingress using the

`openssl req`

command. Make sure you replacewith the DNS name you're using.`<host-name>`

`openssl req -new -x509 -nodes -out aks-ingress-tls.crt -keyout aks-ingress-tls.key -subj "/CN=<host-name>" -addext "subjectAltName=DNS:<host-name>"`

Export the SSL certificate and skip the password prompt using the

`openssl pkcs12 -export`

command.`openssl pkcs12 -export -in aks-ingress-tls.crt -inkey aks-ingress-tls.key -out aks-ingress-tls.pfx`


## Import a self-signed SSL certificate into Azure Key Vault

Import the SSL certificate into Azure Key Vault using the

command. If your certificate is password protected, you can pass the password through the`az keyvault certificate import`

`--password`

flag.`# Set environment variables for your key vault name and certificate name export KEY_VAULT_NAME=<key-vault-name> export KEY_VAULT_CERT_NAME=<key-vault-certificate-name> # Import the SSL certificate into Azure Key Vault az keyvault certificate import --vault-name $KEY_VAULT_NAME --name $KEY_VAULT_CERT_NAME --file aks-ingress-tls.pfx [--password <certificate password if specified>]`


Note

To enable the application routing add-on to reload certificates from Azure Key Vault when they change, you should enable the [secret autorotation feature](csi-secrets-store-configuration-options#manage-auto-rotation) of the Secrets Store CSI driver. When autorotation is enabled, the driver updates the pod mount and the Kubernetes secret by polling for changes periodically, based on the rotation poll interval you define. The default rotation poll interval is two minutes.

## Enable Azure Key Vault integration

Azure Key Vault offers [two authorization systems](/en-us/azure/key-vault/general/rbac-access-policy): **Azure role-based access control (Azure RBAC)**, which operates on the management plane, and the **access policy model**, which operates on both the management plane and the data plane. The `--attach-kv`

operation selects the appropriate access model to use.

Get the resource ID for the key vault using the

command and set the output to an environment variable.`az keyvault show`

`KEY_VAULT_ID=$(az keyvault show --name <KeyVaultName> --query "id" --output tsv)`

Update the application routing add-on to enable the Azure Key Vault provider for Secrets Store CSI Driver and apply the required role assignments using the

command with the`az aks approuting update`

`--enable-kv`

and`--attach-kv`

arguments.`az aks approuting update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --enable-kv --attach-kv ${KEY_VAULT_ID}`


## Create a global Azure DNS zone

If you already have an Azure DNS zone, you can skip this step.

Create an Azure DNS zone using the

command.`az network dns zone create`

`# Set environment variables for your resource group and DNS zone name export RESOURCE_GROUP=<resource-group-name> export ZONE_NAME=<zone-name> # Create the Azure DNS zone az network dns zone create --resource-group $RESOURCE_GROUP --name $ZONE_NAME`


## Enable Azure DNS integration

Get the resource ID for the DNS zone using the

command and set the output to an environment variable.`az network dns zone show`

`ZONE_ID=$(az network dns zone show --resource-group $RESOURCE_GROUP --name $ZONE_NAME --query "id" --output tsv)`

Update the application routing add-on to enable Azure DNS integration using the

command. You can pass a comma-separated list of DNS zone resource IDs.`az aks approuting zone`

`az aks approuting zone add --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --ids=${ZONE_ID} --attach-zones`


## Create an Ingress class that uses a host name and a certificate from Azure Key Vault

The application routing add-on creates an Ingress class on the cluster named *webapprouting.kubernetes.azure.com*. When you create an Ingress object with this class, it activates the add-on.

Get the certificate URI to use in the ingress from Azure Key Vault using the

command.`az keyvault certificate show`

`az keyvault certificate show --vault-name $KEY_VAULT_NAME --name $KEY_VAULT_CERT_NAME --query "id" --output tsv`

The following example output shows the certificate URI returned from the command:

`https://KeyVaultName.vault.azure.net/certificates/KeyVaultCertificateName/ab12c34567d89e01f2345g6h78ijkl90`

Copy the following YAML manifest into a new file named

**ingress.yaml**and save the file to your local computer.Update

with the name of your DNS host and`<host-name>`

with the URI returned from the previous command. The string value for`<key-vault-certificate-uri>`

should only include`<key-vault-certificate-uri>`

`https://yourkeyvault.vault.azure.net/certificates/certname`

. Remove the*Certificate Version*at the end of the URI string to get the current version.The

key in the`secretName`

`tls`

section defines the name of the secret that contains the certificate for this Ingress resource. This certificate is presented in the browser when a client browses to the URL specified in the`<host-name>`

key. Make sure that the value of`secretName`

is equal to`keyvault-`

followed by the value of the Ingress resource name (from`metadata.name`

). In the example YAML,`secretName`

needs to be equal to`keyvault-<your-ingress-name>`

.`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: annotations: kubernetes.azure.com/tls-cert-keyvault-uri: <key-vault-certificate-uri> name: aks-helloworld namespace: hello-web-app-routing spec: ingressClassName: webapprouting.kubernetes.azure.com rules: - host: <host-name> http: paths: - backend: service: name: aks-helloworld port: number: 80 path: / pathType: Prefix tls: - hosts: - <host-name> secretName: keyvault-<your-ingress-name>`

Create the cluster resources using the

command.`kubectl apply`

`kubectl apply -f ingress.yaml -n hello-web-app-routing`

The following example output shows the created resource:

`Ingress.networking.k8s.io/aks-helloworld created`


## Verify the managed ingress was created

Verify the managed ingress was created using the

command.`kubectl get ingress`

`kubectl get ingress -n hello-web-app-routing`

The following example output shows the created managed ingress:

`NAME CLASS HOSTS ADDRESS PORTS AGE aks-helloworld webapprouting.kubernetes.azure.com myapp.contoso.com 20.51.92.19 80, 443 4m`


## Related content

Learn about monitoring the Ingress NGINX controller metrics included with the application routing add-on with [with Prometheus in Grafana](app-routing-nginx-prometheus) as part of analyzing the performance and usage of your application.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/image-integrity -->

# Use Image Integrity to validate signed images before deploying them to your Azure Kubernetes Service (AKS) clusters (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) and its underlying container model provide increased scalability and manageability for cloud native applications. With AKS, you can launch flexible software applications according to the runtime needs of your system. However, this flexibility can introduce new challenges.

In these application environments, using signed container images helps verify that your deployments are built from a trusted entity and that images haven't been tampered with since their creation. Image Integrity is a service that allows you to add an Azure Policy built-in definition to verify that only signed images are deployed to your AKS clusters.

Note

Image Integrity is a feature based on [Ratify](https://github.com/deislabs/ratify). On an AKS cluster, the feature name and property name is `ImageIntegrity`

, while the relevant Image Integrity pods' names contain `Ratify`

.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Prerequisites

An Azure subscription. If you don't have an Azure subscription, you can create a

[free account](https://azure.microsoft.com/free).`aks-preview`

CLI extension version 0.5.96 or later.Ensure that the Azure Policy add-on for AKS is enabled on your cluster. If you don't have this add-on installed, see

[Install Azure Policy add-on for AKS](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks).An AKS cluster enabled with OIDC Issuer. To create a new cluster or update an existing cluster, see

[Configure an AKS cluster with OIDC Issuer](use-oidc-issuer).The

`EnableImageIntegrityPreview`

feature flags registered on your Azure subscription. Register the feature flags using the following commands:Register the

`EnableImageIntegrityPreview`

feature flags using thecommand.`az feature register`

`# Register the EnableImageIntegrityPreview feature flag az feature register --namespace "Microsoft.ContainerService" --name "EnableImageIntegrityPreview" It may take a few minutes for the status to show as *Registered*.`

Verify the registration status using the

command.`az feature show`

`# Verify the EnableImageIntegrityPreview feature flag registration status az feature show --namespace "Microsoft.ContainerService" --name "EnableImageIntegrityPreview"`

Once the status shows

*Registered*, refresh the registration of the`Microsoft.ContainerService`

resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Considerations and limitations

- Your AKS clusters must run Kubernetes version 1.26 or above.
- You shouldn't use this feature for production Azure Container Registry (ACR) registries or workloads.
- Image Integrity supports a maximum of 200 unique signatures concurrently cluster-wide.
- Notation is the only supported verifier.
- Audit is the only supported verification policy effect.

## How Image Integrity works

Image Integrity uses Ratify, Azure Policy, and Gatekeeper to validate signed images before deploying them to your AKS clusters. Enabling Image Integrity on your cluster deploys a `Ratify`

pod. This `Ratify`

pod performs the following tasks:

- Reconciles certificates from Azure Key Vault per the configuration you set up through
`Ratify`

CRDs. - Accesses images stored in ACR when validation requests come from
[Azure Policy](/en-us/azure/governance/policy/concepts/policy-for-kubernetes). To enable this experience, Azure Policy extends Gatekeeper, an admission controller webhook for[Open Policy Agent (OPA)](https://www.openpolicyagent.org/). - Determines whether the target image is signed with a trusted cert and therefore considered as
*trusted*. `AzurePolicy`

and`Gatekeeper`

consume the validation results as the compliance state to decide whether to allow the deployment request.

## Enable Image Integrity on your AKS cluster

Note

Image signature verification is a governance-oriented scenario and leverages [Azure Policy](/en-us/azure/governance/policy/concepts/policy-for-kubernetes) to verify image signatures on AKS clusters at-scale. We recommend using AKS's Image Integrity built-in Azure Policy initiative, which is available in [Azure Policy's built-in definition library](/en-us/azure/governance/policy/samples/built-in-policies#kubernetes).

Create a policy assignment with the AKS policy initiative

using the`[Preview]: Use Image Integrity to ensure only trusted images are deployed`

command.`az policy assignment create`

`export SCOPE="/subscriptions/${SUBSCRIPTION}/resourceGroups/${RESOURCE_GROUP}" export LOCATION=$(az group show --name ${RESOURCE_GROUP} --query location -o tsv) az policy assignment create --name 'deploy-trustedimages' --policy-set-definition 'af28bf8b-c669-4dd3-9137-1e68fdc61bd6' --display-name 'Audit deployment with unsigned container images' --scope ${SCOPE} --mi-system-assigned --role Contributor --identity-scope ${SCOPE} --location ${LOCATION}`

The

`Ratify`

pod deploys after you enable the feature.

Note

The policy deploys the Image Integrity feature on your cluster when it detects any update operation on the cluster. If you want to enable the feature immediately, you need to create a policy remediation using the [ az policy remediation create](/en-us/cli/azure/policy/remediation#az-policy-remediation-create) command.

```
assignment_id=$(az policy assignment show --name 'deploy-trustedimages' --scope ${SCOPE} --query id -o tsv)
az policy remediation create --policy-assignment "$assignment_id" --definition-reference-id deployAKSImageIntegrity --name remediation --resource-group ${RESOURCE_GROUP}
```


## Set up verification configurations

For Image Integrity to properly verify the target signed image, you need to set up `Ratify`

configurations through K8s [CRDs](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/#customresourcedefinitions) using `kubectl`

.

In this article, we use a self-signed CA cert from the official Ratify documentation to set up verification configurations. For more examples, see [Ratify CRDs](https://ratify.dev/docs/1.0/ratify-configuration).

Create a

`VerifyConfig`

file named`verify-config.yaml`

and copy in the following YAML:`apiVersion: config.ratify.deislabs.io/v1beta1 kind: KeyManagementProvider metadata: name: certstore-inline spec: provider: inline parameters: value: | -----BEGIN CERTIFICATE----- MIIDQzCCAiugAwIBAgIUDxHQ9JxxmnrLWTA5rAtIZCzY8mMwDQYJKoZIhvcNAQEL BQAwKTEPMA0GA1UECgwGUmF0aWZ5MRYwFAYDVQQDDA1SYXRpZnkgU2FtcGxlMB4X DTIzMDYyOTA1MjgzMloXDTMzMDYyNjA1MjgzMlowKTEPMA0GA1UECgwGUmF0aWZ5 MRYwFAYDVQQDDA1SYXRpZnkgU2FtcGxlMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8A MIIBCgKCAQEAshmsL2VM9ojhgTVUUuEsZro9jfI27VKZJ4naWSHJihmOki7IoZS8 3/3ATpkE1lGbduJ77M9UxQbEW1PnESB0bWtMQtjIbser3mFCn15yz4nBXiTIu/K4 FYv6HVdc6/cds3jgfEFNw/8RVMBUGNUiSEWa1lV1zDM2v/8GekUr6SNvMyqtY8oo ItwxfUvlhgMNlLgd96mVnnPVLmPkCmXFN9iBMhSce6sn6P9oDIB+pr1ZpE4F5bwa gRBg2tWN3Tz9H/z2a51Xbn7hCT5OLBRlkorHJl2HKKRoXz1hBgR8xOL+zRySH9Qo 3yx6WvluYDNfVbCREzKJf9fFiQeVe0EJOwIDAQABo2MwYTAdBgNVHQ4EFgQUKzci EKCDwPBn4I1YZ+sDdnxEir4wHwYDVR0jBBgwFoAUKzciEKCDwPBn4I1YZ+sDdnxE ir4wDwYDVR0TAQH/BAUwAwEB/zAOBgNVHQ8BAf8EBAMCAgQwDQYJKoZIhvcNAQEL BQADggEBAGh6duwc1MvV+PUYvIkDfgj158KtYX+bv4PmcV/aemQUoArqM1ECYFjt BlBVmTRJA0lijU5I0oZje80zW7P8M8pra0BM6x3cPnh/oZGrsuMizd4h5b5TnwuJ hRvKFFUVeHn9kORbyQwRQ5SpL8cRGyYp+T6ncEmo0jdIOM5dgfdhwHgb+i3TejcF 90sUs65zovUjv1wa11SqOdu12cCj/MYp+H8j2lpaLL2t0cbFJlBY6DNJgxr5qync cz8gbXrZmNbzC7W5QK5J7fcx6tlffOpt5cm427f9NiK2tira50HU7gC3HJkbiSTp Xw10iXXMZzSbQ0/Hj2BF4B40WfAkgRg= -----END CERTIFICATE----- --- apiVersion: config.ratify.deislabs.io/v1beta1 kind: Store metadata: name: store-oras spec: name: oras # If you want to you use Workload Identity for Ratify to access Azure Container Registry, # uncomment the following lines, and fill the proper ClientID: # See more: https://ratify.dev/docs/reference/oras-auth-provider # parameters: # authProvider: # name: azureWorkloadIdentity # clientID: XXX --- apiVersion: config.ratify.deislabs.io/v1beta1 kind: Verifier metadata: name: verifier-notary-inline spec: name: notation artifactTypes: application/vnd.cncf.notary.signature parameters: verificationCertStores: # certificates for validating signatures certs: # name of the trustStore - certstore-inline # name of the certificate store CRD to include in this trustStore trustPolicyDoc: # policy language that indicates which identities are trusted to produce artifacts version: "1.0" trustPolicies: - name: default registryScopes: - "*" signatureVerification: level: strict trustStores: - ca:certs trustedIdentities: - "*"`

Apply the

`VerifyConfig`

to your cluster using the`kubectl apply`

command.`kubectl apply -f verify-config.yaml`


## Deploy sample images to your AKS cluster

Deploy a signed image using the

`kubectl run demo`

command.`kubectl run demo-signed --image=ghcr.io/deislabs/ratify/notary-image:signed`

The following example output shows that Image Integrity allows the deployment:

`ghcr.io/deislabs/ratify/notary-image:signed pod/demo-signed created`


If you want to use your own images, see the [guidance for image signing](/en-us/azure/container-registry/container-registry-tutorial-sign-build-push).

## Disable Image Integrity

### Remove policy initiative

First you should remove the policy initiative using the

command.`az policy assignment delete`

`az policy assignment delete --name 'deploy-trustedimages'`


### Diable add-on

Then disable Image Integrity add-on on your cluster using the

command with the`az aks update`

`--disable-image-integrity`

flag.`az aks update --resource-group myResourceGroup --name MyManagedCluster --disable-image-integrity`


## Next steps

In this article, you learned how to use Image Integrity to validate signed images before deploying them to your Azure Kubernetes Service (AKS) clusters. If you want to learn how to sign your own containers, see [Build, sign, and verify container images using Notary and Azure Key Vault (Preview)](/en-us/azure/container-registry/container-registry-tutorial-sign-build-push).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kueue-overview -->

# Install and Configure Kueue on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to install and configure Kueue to schedule batch workloads on an Azure Kubernetes Service (AKS) cluster. You also explore different Kueue concepts, installation methods to enable advanced Kueue features, and learn how to verify your deployments.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## What are batch workloads?

Batch deployments are typically non-interactive workloads that are retriable, have a finite duration, and might experience spiky or bursty resource usage. These workloads include, but aren't limited to:

- Data processing jobs.
- Security vulnerability scans.
- Media encoding or video transcoding.
- Report generation or financial analysis.
- GPU workloads that require all resources to be available and might tolerate a delayed start but can't tolerate partial GPU allocation.

These workloads are often modeled using a Kubernetes Job, CronJob, or custom resource definition (CRD) like [RayJob](https://docs.ray.io/en/latest/cluster/kubernetes/getting-started/rayjob-quick-start.html) or [Kubeflow MPIJob](https://www.kubeflow.org/docs/components/trainer/legacy-v1/user-guides/mpi/). Batch deployments present the following set of distinct requirements from general purpose deployments:

- Scheduling logic beyond selecting the first available node.
- Fairness, queueing, and resource awareness.
- Lifecycle awareness of jobs and pods.

The default AKS scheduler satisfies the requirements of Kubernetes services but provides limited configuration for batch workloads that require a job queueing system.

## What is Kueue?

[Kueue](https://kueue.sigs.k8s.io/docs/overview/) is an open-source Kubernetes-native job queueing project designed to manage batch workloads and ensure efficient, fair, and policy-driven scheduling in Kubernetes clusters. Kueue integrates with the [Kubernetes scheduling](https://github.com/kubernetes/community/blob/master/sig-scheduling/README.md) ecosystem to coordinate resource allocation, prioritization, and capacity control for batch jobs.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

Kueue introduces a two-level queuing model:

- A
`ClusterQueue`

represents shared resource pools (such as CPU, memory, GPU quotas). - A
`LocalQueue`

represents a tenant-facing queue in a namespace (where users submit their batch jobs).

Workloads submitted to a `LocalQueue`

are matched to a `ClusterQueue`

to determine if they can be admitted.

Note

A `LocalQueue`

is always needed for users to submit batch workloads, and the `LocalQueue`

tells Kueue about which ClusterQueue to assign the job to. The `ClusterQueue`

determines if sufficient resources are available for the job to be admitted and run.

## Who can use Kueue?

Batch workload administrators (including platform or cluster administrators and DevOps engineers) and batch users (data scientists, developers, and ML engineers) can benefit from deploying workloads with Kueue on AKS.

A batch admin focuses on configuring, managing, and securing the platform-level infrastructure to support batch workloads, and have the following responsibilities:

- Provision and manage AKS node pools.
- Define resource quotas, ClusterQueues, and policies for workload isolation.
- Tune autoscaling and cost-efficiency (such as the Cluster Autoscaler or Kueue quotas).
- Monitor cluster and queue health.
- Create and maintain templates and reusable workflows.

A batch user runs compute-intensive or parallel jobs using the platform-level infrastructure configured by a batch admin, and typically:

- Submit batch jobs (such as Job, Workload, or custom controller CRDs) and monitor job status and outputs
- Select appropriate queue or resource flavor for jobs (based on guidance from batch admins)
- Optimize job specs for resource and performance needs

| Queue Type | Scope | Created By | Used For |
|---|---|---|---|
ClusterQueue |
Cluster-wide | Platform admin | Define shared compute capacity and quota management |
LocalQueue |
Namespace | Namespace owner | Enable workload submission, mapped to ClusterQueue |

## Prerequisites

- An existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Azure CLI installed on your local machine. To install or upgrade, see
[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). [Helm version 3 or above](https://helm.sh/docs/intro/install/)installed.

## Install Kueue with Helm

While most features and scheduling policies that you might require are enabled by default, some aren't like `TopologyAwareScheduling`

. If needed, reconfigure your Kueue installation by changing the default [Feature Gates](https://kueue.sigs.k8s.io/docs/installation/#feature-gates-for-alpha-and-beta-features) or by configuring [Kueue paramater values](https://github.com/kubernetes-sigs/kueue/blob/main/charts/kueue/README.md#configuration) in the `values.yaml`

file of the Helm chart.

Kueue supports multiple workload [Frameworks](https://kueue.sigs.k8s.io/docs/tasks/run/) that you need to explicitly enable to use Kueue’s scheduling and resource management capabilities when running [MPI Operator](https://www.kubeflow.org/docs/components/training/mpi/) MPIJobs, [KubeRay's](https://github.com/ray-project/kuberay) [RayJob](https://docs.ray.io/en/latest/cluster/kubernetes/getting-started/rayjob-quick-start.html) and more.

In this guide, Kueue is configured to include `LocalQueueMetrics`

and `Topology Aware Scheduling`

and frameworks from Kubeflow, Ray, and [JobSet](https://jobset.sigs.k8s.io/docs/concepts/).

`LocalQueueMetrics`

provides detailed Prometheus metrics specific to the state and activity of LocalQueues, enabling fine-grained monitoring of workload admission, quota reservation, and resource utilization.`TopologyAwareScheduling`

allows scheduling of pods based on the topology of nodes in a pool or cluster to improve available bandwidth between the pods.

Note

Update version as needed: [kueue/releases](https://github.com/kubernetes-sigs/kueue/releases)

Create and save a

`values.yaml`

file to optionally customize your Kueue configuration.`cat <<EOF > values.yaml controllerManager: featureGates: - name: TopologyAwareScheduling enabled: true - name: LocalQueueMetrics enabled: true managerConfig: controllerManagerConfigYaml: | apiVersion: config.kueue.x-k8s.io/v1beta1 kind: Configuration integrations: frameworks: - batch/job - kubeflow.org/mpijob - ray.io/rayjob - ray.io/raycluster - jobset.x-k8s.io/jobset - kubeflow.org/paddlejob - kubeflow.org/pytorchjob - kubeflow.org/tfjob - kubeflow.org/xgboostjob - kubeflow.org/jaxjob EOF`

Install the latest version of the Kueue controller and CRDs in a dedicated namespace using the

`helm install`

command.`LATEST_VERSION=$(curl -s https://api.github.com/repos/kubernetes-sigs/kueue/releases/latest | grep tag_name | cut -d '"' -f 4 | sed 's/^v//') helm install kueue oci://registry.k8s.io/kueue/charts/kueue \ --version=${LATEST_VERSION} \ --create-namespace --namespace=kueue-system \ --values values.yaml`

Confirm the deployment status using the

`helm list`

command.`helm list --namespace kueue-system`

Your output should include a

`Status`

of`deployed`

and look like:`Pulled: registry.k8s.io/kueue/charts/kueue:0.13.4 Digest: - NAME: kueue LAST DEPLOYED: - NAMESPACE: kueue-system STATUS: deployed REVISION: 1 TEST SUITE: None`


## Confirm deployment status

Verify that controller pods are running properly.

`kubectl get deploy -n kueue-system`

Your output should look similar to the following example output:

`NAME READY UP-TO-DATE AVAILABLE AGE kueue-controller-manager 1/1 1 1 7s`

Confirm the installation of Kueue resources on your AKS cluster:

`kubectl get crds | grep kueue`

Your output should include the following Kueue CRDs:

`admissionchecks.kueue.x-k8s.io 2025-09-11T18:20:48Z clusterqueues.kueue.x-k8s.io 2025-09-11T18:20:48Z cohorts.kueue.x-k8s.io 2025-09-11T18:20:48Z localqueues.kueue.x-k8s.io 2025-09-11T18:20:48Z multikueueclusters.kueue.x-k8s.io 2025-09-11T18:20:48Z multikueueconfigs.kueue.x-k8s.io 2025-09-11T18:20:48Z provisioningrequestconfigs.kueue.x-k8s.io 2025-09-11T18:20:48Z resourceflavors.kueue.x-k8s.io 2025-09-11T18:20:48Z topologies.kueue.x-k8s.io 2025-09-11T18:20:48Z workloadpriorityclasses.kueue.x-k8s.io 2025-09-11T18:20:48Z workloads.kueue.x-k8s.io 2025-09-11T18:20:48Z`


## Uninstall Kueue

If you no longer need to use the Kueue controller manager or Kueue custom resources in your AKS cluster, you can uninstall the Helm repository and remove the dedicated namespace and resources.

Uninstall the Kueue Helm repository using the

`helm uninstall`

command.`helm uninstall kueue --namespace kueue-system`

Remove the dedicated namespace and resources using the

`kubectl delete`

command.`kubectl delete namespace kueue-system`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/core-aks-concepts -->

# Core concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes core concepts of Azure Kubernetes Service (AKS), a managed Kubernetes service that you can use to deploy and operate containerized applications at scale on Azure.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## What is Kubernetes?

Kubernetes is an open-source container orchestration platform for automating the deployment, scaling, and management of containerized applications. For more information, see the official [Kubernetes documentation](https://kubernetes.io/docs/home/).

## What is AKS?

AKS is a managed Kubernetes service that simplifies deploying, managing, and scaling containerized applications that use Kubernetes. For more information, see [What is Azure Kubernetes Service (AKS)?](what-is-aks).

## Cluster components

An AKS cluster is divided into two main components:

**Control plane**: The control plane provides the core Kubernetes services and orchestration of application workloads.**Nodes**: Nodes are the underlying virtual machines (VMs) that run your applications.

Note

AKS managed components have the label `kubernetes.azure.com/managedby`

: `aks`

.

AKS manages the Helm releases with the prefix `aks-managed`

. Continuously increasing revisions on these releases are expected and safe.

### Control plane

The Azure managed control plane is composed of several components that help manage the cluster:

| Component | Description |
|---|---|
`kube-apiserver` |
The API server (
|

`etcd`

[etcd](https://kubernetes.io/docs/concepts/overview/components/#etcd)helps to maintain the state of your Kubernetes cluster and configuration.`kube-scheduler`

[kube-scheduler](https://kubernetes.io/docs/concepts/overview/components/#kube-scheduler)) helps to make scheduling decisions. It watches for new pods with no assigned node and selects a node for them to run on.`kube-controller-manager`

[kube-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#kube-controller-manager)) runs controller processes, such as noticing and responding when nodes go down.`cloud-controller-manager`

[cloud-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#cloud-controller-manager)) embeds cloud-specific control logic to run controllers specific to the cloud provider.### Nodes

Each AKS cluster has at least one node, which is an Azure VM that runs Kubernetes node components. The following components run on each node:

| Component | Description |
|---|---|
`kubelet` |
The
|

`kube-proxy`

[kube-proxy](https://kubernetes.io/docs/concepts/overview/components/#kube-proxy)is a network proxy that maintains network rules on nodes.`container runtime`

[container runtime](https://kubernetes.io/docs/concepts/overview/components/#container-runtime)manages the execution and lifecycle of containers.## Node configuration

Configure the following settings for nodes.

### VM size and image

The *Azure VM size* for your nodes defines CPUs, memory, size, and the storage type available, such as a high-performance solid-state drive or a regular hard-disk drive. The VM size you choose depends on the workload requirements and the number of pods that you plan to run on each node. As of May 2025, the default VM SKU and size will be dynamically selected by AKS based on available capacity and quota if the parameter is left blank during deployment. For more information, see [Supported VM sizes in Azure Kubernetes Service (AKS)](quotas-skus-regions#supported-vm-sizes).

In AKS, the *VM image* for your cluster's nodes is based on Ubuntu Linux, [Azure Linux](use-azure-linux), or Windows Server 2022. When you create an AKS cluster or scale out the number of nodes, the Azure platform automatically creates and configures the requested number of VMs. Agent nodes are billed as standard VMs. Any VM size discounts, including [Azure reservations](/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations), are automatically applied.

### OS disks

Default OS disk sizing is used on new clusters or node pools only when a default OS disk size isn't specified. This behavior applies to both managed and ephemeral OS disks. For more information, see [Default OS disk sizing](concepts-storage#default-os-disk-sizing).

### Resource reservations

AKS uses node resources to help the nodes function as part of the cluster. This usage can cause a discrepancy between the node's total resources and the allocatable resources in AKS. To maintain node performance and functionality, AKS reserves two types of resources, CPU and memory, on each node. For more information, see [Resource reservations in AKS](node-resource-reservations).

### OS

AKS supports two linux distros: Ubuntu and Azure Linux. Ubuntu is the default Linux distro on AKS. Windows node pools are also supported on AKS with the [Long Term Servicing Channel (LTSC)](/en-us/windows-server/get-started/servicing-channels-comparison) as the default channel on AKS. For more information on default OS versions, see documentation on [node images](node-images).

### Container runtime

A container runtime is software that executes containers and manages container images on a node. The runtime helps abstract away system calls or OS-specific functionality to run containers on Linux or Windows. For Linux node pools, [containerd](https://containerd.io/) is used on Kubernetes version 1.19 and higher. For Windows Server 2019 and 2022 node pools, [containerd](https://containerd.io/) is generally available and is the only runtime option on Kubernetes version 1.23 and higher.

## Pods

A *pod* is a group of one or more containers that share the same network and storage resources and a specification for how to run the containers. Pods typically have a 1:1 mapping with a container, but you can run multiple containers in a pod.

## Node pools

In AKS, nodes of the same configuration are grouped together into *node pools*. These node pools contain the underlying virtual machine scale sets and virtual machines (VMs) that run your applications.

When you create an AKS cluster, you define the initial number of nodes and their size (version), which creates a [system node pool](use-system-pools). System node pools serve the primary purpose of hosting critical system pods, such as CoreDNS and `konnectivity`

.

To support applications that have different compute or storage demands, you can create *user node pools*. User node pools serve the primary purpose of hosting your application pods.

For more information, see [Create node pools in AKS](create-node-pools) and [Manage node pools in AKS](manage-node-pools).

## Node resource group

When you create an AKS cluster in an Azure resource group, the AKS resource provider automatically creates a second resource group called the *node resource group*. This resource group contains all the infrastructure resources associated with the cluster, including VMs, virtual machine scale sets, and storage.

For more information, see the following resources:

[Why are two resource groups created with AKS?](faq)[Can I provide my own name for the AKS node resource group?](faq)[Can I modify tags and other properties of the resources in the AKS node resource group?](faq)

## Namespaces

Kubernetes resources, such as pods and deployments, are logically grouped into *namespaces* to divide an AKS cluster and create, view, or manage access to resources.

The following namespaces are created by default in an AKS cluster:

| Namespace | Description |
|---|---|
`default` |
The
|

`kube-node-lease`

[kube-node-lease](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace enables nodes to communicate their availability to the control plane.`kube-public`

[kube-public](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace isn't typically used, but you can use it so that resources are visible across the whole cluster by any user.`kube-system`

[kube-system](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace is used by Kubernetes to manage cluster resources, such as`coredns`

, `konnectivity-agent`

, and `metrics-server`

. It is not recommended to deploy your own applications to this namespace. For rare cases where deploying your own applications to this namespace is necessary, see the [FAQ](faq#can-admission-controller-webhooks-affect-kube-system-and-internal-aks-namespaces-)to learn how.## Cluster modes

In AKS, you can create a cluster with the Automatic or Standard mode. AKS Automatic provides a more fully managed experience. You can manage cluster configuration, including nodes, scaling, security, and other preconfigured settings. AKS Standard provides more control over the cluster configuration, including the ability to manage node pools, scaling, and other settings.

For more information, see [AKS Automatic and Standard feature comparison](intro-aks-automatic#aks-automatic-and-standard-feature-comparison).

## Pricing tiers

AKS offers three pricing tiers for cluster management: Free, Standard, and Premium. The pricing tier you choose determines the features that are available for managing your cluster.

For more information, see [Pricing tiers for AKS cluster management](free-standard-pricing-tiers).

## Supported Kubernetes versions

For more information, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions).

## Related content

For information on more core concepts for AKS, see the following resources:
