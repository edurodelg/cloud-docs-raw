---
source_url: https://learn.microsoft.com/en-us/azure/search/security-controls-policy
fetched_at: 2026-01-25T02:10:37.284939
---

# Azure Policy Regulatory Compliance controls for Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If you are using [Azure Policy](/en-us/azure/governance/policy/overview) to enforce the recommendations in
[Microsoft cloud security benchmark](/en-us/azure/security/benchmarks/introduction), then you probably already know
that you can create policies for identifying and fixing non-compliant services. These policies might
be custom, or they might be based on built-in definitions that provide compliance criteria and
appropriate solutions for well-understood best practices.

For Azure AI Search, there is currently one built-definition, listed below, that you can use
in a policy assignment. The built-in is for logging and monitoring. By using this built-in
definition in a [policy that you create](/en-us/azure/governance/policy/assign-policy-portal), the system
will scan for search services that do not have [resource logging](monitor-azure-cognitive-search), and
then enable it accordingly.

[Regulatory Compliance in Azure Policy](/en-us/azure/governance/policy/concepts/regulatory-compliance)
provides Microsoft-created and managed initiative definitions, known as *built-ins*, for the
**compliance domains** and **security controls** related to different compliance standards. This
page lists the **compliance domains** and **security controls** for Azure AI Search. You can
assign the built-ins for a **security control** individually to help make your Azure resources
compliant with the specific standard.

The title of each built-in policy definition links to the policy definition in the Azure portal. Use the link in the **Policy Version** column to view the source on the
[Azure Policy GitHub repo](https://github.com/Azure/azure-policy).

Important

Each control is associated with one or more [Azure Policy](/en-us/azure/governance/policy/overview) definitions. These policies might help you [assess compliance](/en-us/azure/governance/policy/how-to/get-compliance-data) with the control.
However, there often isn't a one-to-one or complete match between a control and one or more policies. As such, **Compliant** in Azure Policy refers only to the policies themselves. This doesn't ensure that you're fully compliant with all requirements of a control. In addition, the compliance standard includes controls that aren't addressed by any Azure Policy definitions at this time.
Therefore, compliance in Azure Policy is only a partial view of your overall compliance status. The associations between controls and Azure Policy Regulatory Compliance definitions for these compliance standards can change over time.

## CIS Microsoft Azure Foundations Benchmark 1.3.0

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - CIS Microsoft Azure Foundations Benchmark 1.3.0](/en-us/azure/governance/policy/samples/cis-azure-1-3-0).
For more information about this compliance standard, see
[CIS Microsoft Azure Foundations Benchmark](https://www.cisecurity.org/benchmark/azure/).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| 5 Logging and Monitoring | 5.3 | Ensure that Diagnostic Logs are enabled for all services which support it. |
|

[5.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/AuditDiagnosticLog_Audit.json)## CIS Microsoft Azure Foundations Benchmark 1.4.0

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance details for CIS v1.4.0](/en-us/azure/governance/policy/samples/cis-azure-1-4-0).
For more information about this compliance standard, see
[CIS Microsoft Azure Foundations Benchmark](https://www.cisecurity.org/benchmark/azure/).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| 5 Logging and Monitoring | 5.3 | Ensure that Diagnostic Logs Are Enabled for All Services that Support it. |
|

[5.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/AuditDiagnosticLog_Audit.json)## CIS Microsoft Azure Foundations Benchmark 2.0.0

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance details for CIS v2.0.0](/en-us/azure/governance/policy/samples/cis-azure-2-0-0).
For more information about this compliance standard, see
[CIS Microsoft Azure Foundations Benchmark](https://www.cisecurity.org/benchmark/azure/).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| 5 | 5.4 | Ensure that Azure Monitor Resource Logging is Enabled for All Services that Support it |
|

[5.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/AuditDiagnosticLog_Audit.json)## CMMC Level 3

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - CMMC Level 3](/en-us/azure/governance/policy/samples/cmmc-l3).
For more information about this compliance standard, see
[Cybersecurity Maturity Model Certification (CMMC)](https://dodcio.defense.gov/CMMC/).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| Access Control | AC.1.001 | Limit information system access to authorized users, processes acting on behalf of authorized users, and devices (including other information systems). |
|

[3.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/NetworkAcls_Audit.json)[Azure AI Services resources should restrict network access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F037eea7a-bd0a-46c5-9a66-03aea78705d3)[3.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/NetworkAcls_Audit.json)[Azure AI Services resources should restrict network access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F037eea7a-bd0a-46c5-9a66-03aea78705d3)[3.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/NetworkAcls_Audit.json)[Azure AI Services resources should restrict network access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F037eea7a-bd0a-46c5-9a66-03aea78705d3)[3.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/NetworkAcls_Audit.json)[Azure AI Services resources should restrict network access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F037eea7a-bd0a-46c5-9a66-03aea78705d3)[3.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/NetworkAcls_Audit.json)[Azure AI Services resources should restrict network access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F037eea7a-bd0a-46c5-9a66-03aea78705d3)[3.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/NetworkAcls_Audit.json)## FedRAMP High

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - FedRAMP High](/en-us/azure/governance/policy/samples/fedramp-high).
For more information about this compliance standard, see
[FedRAMP High](https://www.fedramp.gov/).

## FedRAMP Moderate

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - FedRAMP Moderate](/en-us/azure/governance/policy/samples/fedramp-moderate).
For more information about this compliance standard, see
[FedRAMP Moderate](https://www.fedramp.gov/).

## HIPAA HITRUST

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - HIPAA HITRUST](/en-us/azure/governance/policy/samples/hipaa-hitrust).
For more information about this compliance standard, see
[HIPAA HITRUST](https://www.hhs.gov/hipaa/for-professionals/security/laws-regulations/index.html).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| 12 Audit Logging & Monitoring | 1208.09aa3System.1-09.aa | 1208.09aa3System.1-09.aa 09.10 Monitoring |
|

[5.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/AuditDiagnosticLog_Audit.json)## Microsoft cloud security benchmark

The [Microsoft cloud security benchmark](/en-us/security/benchmark/azure/introduction) provides recommendations on
how you can secure your cloud solutions on Azure. To see how this service completely maps to the
Microsoft cloud security benchmark, see the
[Azure Security Benchmark mapping files](https://github.com/MicrosoftDocs/SecurityBenchmarks/tree/master/Azure%20Offer%20Security%20Baselines).

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - Microsoft cloud security benchmark](/en-us/azure/governance/policy/samples/azure-security-benchmark).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| Network Security | NS-2 | NS-2 Secure cloud services with network controls |
|

[3.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/NetworkAcls_Audit.json)[Azure AI Services resources should use Azure Private Link](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd6759c02-b87f-42b7-892e-71b3f471d782)[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/EnablePrivateEndpoints_Audit.json)[Azure AI Services resources should have key access disabled (disable local authentication)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F71ef260a-8f18-47b7-abcb-62d0673d94dc)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/DisableLocalAuth_Audit.json)[Diagnostic logs in Azure AI services resources should be enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1b4d1c4e-934c-4703-944c-27c82c06bebb)[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/DiagnosticLogs_Audit.json)[Resource logs in Search services should be enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb4330a05-a843-4bc8-bf9a-cacce50c67f4)[5.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/AuditDiagnosticLog_Audit.json)## NIST SP 800-171 R2

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - NIST SP 800-171 R2](/en-us/azure/governance/policy/samples/nist-sp-800-171-r2).
For more information about this compliance standard, see
[NIST SP 800-171 R2](https://csrc.nist.gov/publications/detail/sp/800-171/rev-2/final).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| Access Control | 3.1.1 | Limit system access to authorized users, processes acting on behalf of authorized users, and devices (including other systems). |
|

[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/RequirePrivateLinkSupportedResource_Deny.json)[Azure AI Services resources should have key access disabled (disable local authentication)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F71ef260a-8f18-47b7-abcb-62d0673d94dc)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/DisableLocalAuth_Audit.json)[Azure AI Search service should use a SKU that supports private link](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa049bf77-880b-470f-ba6d-9f21c530cf83)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/RequirePrivateLinkSupportedResource_Deny.json)[Azure AI Search service should use a SKU that supports private link](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa049bf77-880b-470f-ba6d-9f21c530cf83)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/RequirePrivateLinkSupportedResource_Deny.json)[Azure AI Search service should use a SKU that supports private link](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa049bf77-880b-470f-ba6d-9f21c530cf83)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/RequirePrivateLinkSupportedResource_Deny.json)[Azure AI Services resources should have key access disabled (disable local authentication)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F71ef260a-8f18-47b7-abcb-62d0673d94dc)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/DisableLocalAuth_Audit.json)[Azure AI Search service should use a SKU that supports private link](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa049bf77-880b-470f-ba6d-9f21c530cf83)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/RequirePrivateLinkSupportedResource_Deny.json)[Azure AI Search services should disable public network access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fee980b6d-0eca-4501-8d54-f6290fd512c3)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/RequirePublicNetworkAccessDisabled_Deny.json)[Azure AI Services resources should restrict network access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F037eea7a-bd0a-46c5-9a66-03aea78705d3)[3.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/NetworkAcls_Audit.json)[Azure AI Search service should use a SKU that supports private link](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa049bf77-880b-470f-ba6d-9f21c530cf83)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/RequirePrivateLinkSupportedResource_Deny.json)[Azure AI Search services should disable public network access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fee980b6d-0eca-4501-8d54-f6290fd512c3)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/RequirePublicNetworkAccessDisabled_Deny.json)[Azure AI Services resources should restrict network access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F037eea7a-bd0a-46c5-9a66-03aea78705d3)[3.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/NetworkAcls_Audit.json)[Azure AI Search service should use a SKU that supports private link](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa049bf77-880b-470f-ba6d-9f21c530cf83)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/RequirePrivateLinkSupportedResource_Deny.json)[Azure AI Search services should disable public network access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fee980b6d-0eca-4501-8d54-f6290fd512c3)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/RequirePublicNetworkAccessDisabled_Deny.json)[Azure AI Services resources should restrict network access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F037eea7a-bd0a-46c5-9a66-03aea78705d3)[3.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/NetworkAcls_Audit.json)[Azure AI Search service should use a SKU that supports private link](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa049bf77-880b-470f-ba6d-9f21c530cf83)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/RequirePrivateLinkSupportedResource_Deny.json)[Azure AI Search services should disable public network access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fee980b6d-0eca-4501-8d54-f6290fd512c3)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/RequirePublicNetworkAccessDisabled_Deny.json)[Azure AI Services resources should restrict network access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F037eea7a-bd0a-46c5-9a66-03aea78705d3)[3.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/NetworkAcls_Audit.json)[Azure AI Search services should disable public network access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fee980b6d-0eca-4501-8d54-f6290fd512c3)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/RequirePublicNetworkAccessDisabled_Deny.json)[Azure AI Services resources should restrict network access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F037eea7a-bd0a-46c5-9a66-03aea78705d3)[3.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/NetworkAcls_Audit.json)[Resource logs in Search services should be enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb4330a05-a843-4bc8-bf9a-cacce50c67f4)[5.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/AuditDiagnosticLog_Audit.json)[Resource logs in Search services should be enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb4330a05-a843-4bc8-bf9a-cacce50c67f4)[5.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/AuditDiagnosticLog_Audit.json)[Azure AI Services resources should have key access disabled (disable local authentication)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F71ef260a-8f18-47b7-abcb-62d0673d94dc)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/DisableLocalAuth_Audit.json)[Azure AI Services resources should have key access disabled (disable local authentication)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F71ef260a-8f18-47b7-abcb-62d0673d94dc)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/DisableLocalAuth_Audit.json)[Azure AI Services resources should have key access disabled (disable local authentication)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F71ef260a-8f18-47b7-abcb-62d0673d94dc)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/DisableLocalAuth_Audit.json)[Azure AI Services resources should have key access disabled (disable local authentication)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F71ef260a-8f18-47b7-abcb-62d0673d94dc)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/DisableLocalAuth_Audit.json)## NIST SP 800-53 Rev. 4

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - NIST SP 800-53 Rev. 4](/en-us/azure/governance/policy/samples/nist-sp-800-53-r4).
For more information about this compliance standard, see
[NIST SP 800-53 Rev. 4](https://nvd.nist.gov/800-53).

## NIST SP 800-53 Rev. 5

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - NIST SP 800-53 Rev. 5](/en-us/azure/governance/policy/samples/nist-sp-800-53-r5).
For more information about this compliance standard, see
[NIST SP 800-53 Rev. 5](https://nvd.nist.gov/800-53).

## NL BIO Cloud Theme

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance details for NL BIO Cloud Theme](/en-us/azure/governance/policy/samples/nl-bio-cloud-theme).
For more information about this compliance standard, see
[Baseline Information Security Government Cybersecurity - Digital Government (digitaleoverheid.nl)](https://www.digitaleoverheid.nl/overzicht-van-alle-onderwerpen/cybersecurity/kaders-voor-cybersecurity/baseline-informatiebeveiliging-overheid/).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| U.07.1 Data separation - Isolated | U.07.1 | Permanent isolation of data is a multi-tenant architecture. Patches are realized in a controlled manner. |
|

[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/RequirePrivateLinkSupportedResource_Deny.json)[Azure AI Search services should disable public network access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fee980b6d-0eca-4501-8d54-f6290fd512c3)[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/RequirePublicNetworkAccessDisabled_Deny.json)[Azure AI Services resources should restrict network access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F037eea7a-bd0a-46c5-9a66-03aea78705d3)[3.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/NetworkAcls_Audit.json)[Azure AI Services resources should have key access disabled (disable local authentication)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F71ef260a-8f18-47b7-abcb-62d0673d94dc)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/DisableLocalAuth_Audit.json)[Azure AI Services resources should have key access disabled (disable local authentication)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F71ef260a-8f18-47b7-abcb-62d0673d94dc)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/DisableLocalAuth_Audit.json)[Azure AI Services resources should have key access disabled (disable local authentication)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F71ef260a-8f18-47b7-abcb-62d0673d94dc)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/DisableLocalAuth_Audit.json)[Azure AI Services resources should have key access disabled (disable local authentication)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F71ef260a-8f18-47b7-abcb-62d0673d94dc)[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/DisableLocalAuth_Audit.json)[Resource logs in Search services should be enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb4330a05-a843-4bc8-bf9a-cacce50c67f4)[5.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/AuditDiagnosticLog_Audit.json)## Reserve Bank of India IT Framework for Banks v2016

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - RBI ITF Banks v2016](/en-us/azure/governance/policy/samples/rbi-itf-banks-2016).
For more information about this compliance standard, see
[RBI ITF Banks v2016 (PDF)](https://rbidocs.rbi.org.in/rdocs/notification/PDFs/NT41893F697BC1D57443BB76AFC7AB56272EB.PDF).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| Anti-Phishing | Anti-Phishing-14.1 |
|

[3.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Ai%20Services/NetworkAcls_Audit.json)## RMIT Malaysia

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance - RMIT Malaysia](/en-us/azure/governance/policy/samples/rmit-malaysia).
For more information about this compliance standard, see
[RMIT Malaysia](https://www.bnm.gov.my/documents/20124/963937/Risk+Management+in+Technology+(RMiT).pdf/810b088e-6f4f-aa35-b603-1208ace33619?t=1592866162078).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| Security of Digital Services | 10.66 | Security of Digital Services - 10.66 |
|

[2.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Monitoring/Search_DeployDiagnosticLog_Deploy_EventHub.json)[Deploy Diagnostic Settings for Search Services to Log Analytics workspace](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F08ba64b8-738f-4918-9686-730d2ed79c7d)[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Monitoring/Search_DeployDiagnosticLog_Deploy_LogAnalytics.json)## Spain ENS

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance details for Spain ENS](/en-us/azure/governance/policy/samples/spain-ens).
For more information about this compliance standard, see
[CCN-STIC 884](https://www.ccn-cert.cni.es/es/comunicacion-eventos/comunicados-ccn-cert/9519-disponible-la-guia-ccn-stic-884-perfil-de-cumplimiento-especifico-para-azure-servicio-de-cloud-corporativo).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| Operational framework | op.exp.7 | Operation |
|

[5.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/AuditDiagnosticLog_Audit.json)## SWIFT CSP-CSCF v2021

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance details for SWIFT CSP-CSCF v2021](/en-us/azure/governance/policy/samples/swift-csp-cscf-2021).
For more information about this compliance standard, see
[SWIFT CSP CSCF v2021](https://www.swift.com/myswift/customer-security-programme-csp).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| Detect Anomalous Activity to Systems or Transaction Records | 6.4 | Logging and Monitoring |
|

[5.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/AuditDiagnosticLog_Audit.json)## SWIFT CSP-CSCF v2022

To review how the available Azure Policy built-ins for all Azure services map to this compliance
standard, see
[Azure Policy Regulatory Compliance details for SWIFT CSP-CSCF v2022](/en-us/azure/governance/policy/samples/swift-csp-cscf-2022).
For more information about this compliance standard, see
[SWIFT CSP CSCF v2022](https://www.swift.com/myswift/customer-security-programme-csp).

| Domain | Control ID | Control title | Policy(Azure portal) |
Policy version(GitHub) |
|---|---|---|---|---|
| 6. Detect Anomalous Activity to Systems or Transaction Records | 6.4 | Record security events and detect anomalous actions and operations within the local SWIFT environment. |
|

[5.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/AuditDiagnosticLog_Audit.json)## Next steps

- Learn more about
[Azure Policy Regulatory Compliance](/en-us/azure/governance/policy/concepts/regulatory-compliance). - See the built-ins on the
[Azure Policy GitHub repo](https://github.com/Azure/azure-policy).