---
source_url: https://learn.microsoft.com/en-us/azure/ai-foundry/configuration/enable-ai-api-management-gateway-portal
fetched_at: 2026-02-08T01:03:23.434980
---

# Configure AI Gateway in your Foundry resources

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to enable AI Gateway for a Microsoft Foundry resource using the Foundry portal. AI Gateway uses Azure API Management behind the scenes to provide token limits, quotas, and governance for model deployments.

## Prerequisites

Azure subscription (

[create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)).Permissions to create or reuse an Azure API Management (APIM) instance:

- To create an APIM instance:
**Contributor**or**Owner**on the target resource group (or subscription). - To manage an existing APIM instance:
**API Management Service Contributor**(or**Owner**) on the APIM instance. For more information, see[How to use role-based access control in Azure API Management](/en-us/azure/api-management/api-management-role-based-access-control).

- To create an APIM instance:
Access to the Foundry portal (

**Admin console**) for the target Foundry resource.- For example:
**Azure AI Account Owner**or**Azure AI Owner**on the Foundry resource. For more information, see[Role-based access control for Microsoft Foundry](../concepts/rbac-foundry?view=foundry).

- For example:
Decision on whether to create a dedicated APIM instance or reuse an existing one.


## Create an AI Gateway

Follow these steps in the Foundry portal to enable AI Gateway for a resource.

-
Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**. Select

**Operate**>**Admin console**.Open the

**AI Gateway**tab.Select

**Add AI Gateway**.Select the Foundry resource you want to connect with the gateway.

Select

**Create new**or**Use existing**APIM.**Create new**: Creates a Basic v2 SKU instance. Basic v2 is designed for development and testing with SLA support.**Use existing**: Select an instance that meets your organization's governance and networking requirements.

Tip

AI Gateway in Azure API Management service is free for the first 100,000 API requests. For more information about costs and pricing, see

[API Management Pricing](https://azure.microsoft.com/pricing/details/api-management/).Name the gateway, and select

**Add**to create or associate the APIM instance.Verify the AI Gateway appears in the list with a status of

**Enabled**. If the status shows**Provisioning**, wait a few minutes and refresh the page.New projects created in the Foundry resource have AI Gateway enabled by default. Existing projects must be enabled manually.

To enable an existing project, select the AI Gateway name to view associated projects.

In the project list, locate the project you want to enable. The

**Gateway status**column shows current status.Select

**Add project to gateway**. The**Gateway status**column updates to**Enabled**.

## Verify the gateway is working

Confirm that traffic routes through AI Gateway:

- In the Azure portal, open the API Management instance connected to your Foundry resource.
- Select
**Metrics**or**Logs**to confirm requests appear when you call a model deployment. - If you configured token limits, verify they apply by testing a request that exceeds the limit.

## Understand AI Gateway architecture

AI Gateway sits between clients and Foundry building blocks, including models and tools. All requests flow through the APIM instance once associated. Limits apply at the project level, so each project can have its own TPM and quota settings.


AI Gateway enables:

- Multi-team token containment (prevent one project from monopolizing capacity).
- Cost control by capping aggregate usage.
- Compliance boundaries for regulated workloads (enforce predictable usage ceilings).
- Registration of
[custom agents for governance](../control-plane/register-custom-agent?view=foundry).

## Governance scenarios

Once you configured AI Gateway for your resource and project, you can:

[Configure token limits for models](../control-plane/how-to-enforce-limits-models?view=foundry).[Add custom agents to Control Plane](../control-plane/register-custom-agent?view=foundry).- Govern MCP and A2A agent tools.

## Troubleshooting

| Issue | Cause | Resolution |
|---|---|---|
| AI Gateway doesn't appear after creation. | Provisioning is still in progress. | Wait a few minutes and refresh the page. Basic v2 instances typically provision within 5-10 minutes. |
Project shows Gateway status as Disabled. |
Existing projects aren't automatically enabled for AI Gateway. | Select the AI Gateway, locate the project, and select Add project to gateway. |
| Requests bypass the gateway. | The project wasn't enabled before requests were made, or the gateway isn't fully provisioned. | Verify the gateway status shows Enabled for both the resource and project. |
| Permission error when creating gateway. | Missing required RBAC role. | Verify you have Contributor or Owner on the resource group (to create) or API Management Service Contributor on an existing instance. |
| Token limits don't apply to requests. | Limits aren't configured, or the project isn't using the gateway. | Verify the project is enabled for AI Gateway, then configure token limits in the Admin console. |

For tools-specific troubleshooting, see [Tools governance with AI Gateway](/en-us/azure/ai-foundry/agents/how-to/tools/governance#troubleshooting).

## Clean up resources

If you created a dedicated APIM instance for this purpose:

- Confirm that no other workloads depend on it.
- Disable the AI Gateway for all projects in the Foundry resource it's associated with.
- Remove linked resources in Azure portal.
- Delete the APIM instance with the same name as the AI gateway in Azure portal (if it isn't used for any other purpose).