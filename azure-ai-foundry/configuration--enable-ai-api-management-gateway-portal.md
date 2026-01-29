---
source_url: https://learn.microsoft.com/en-us/azure/ai-foundry/configuration/enable-ai-api-management-gateway-portal
fetched_at: 2026-01-29T15:31:19.996098
---

# Configure AI Gateway in your Foundry resources

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Microsoft Foundry integrates with AI Gateway to enable advanced management and governance capabilities. This integration uses Azure API Management behind the scenes.

AI Gateway enables:

- Multi-team token containment (prevent one project from monopolizing capacity).
- Cost control by capping aggregate usage.
- Compliance boundaries for regulated workloads (enforce predictable usage ceilings).
- Registration of
[custom agents for governance](../control-plane/register-custom-agent?view=foundry).

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


## Understand AI Gateway scope

An AI Gateway sits between clients and Microsoft Foundry building blocks, including models or tools. All requests flow through the APIM instance once associated. Limits apply at the project level (each project can have its own TPM and quota settings).


## Choose API Management usage model

When you create a new AI Gateway, decide whether to:

- Create a new APIM instance.
- Use an existing APIM instance.

If you use an existing APIM instance, choose one that meets your organization's governance and networking requirements.

When you create a new instance from the Foundry portal flow, the SKU defaults to Basic v2.

Tip

AI Gateway in Azure API Management service is free for the first 100,000 API requests. For more information about costs and pricing for the API Management service, see [API Management Pricing](https://azure.microsoft.com/pricing/details/api-management/).

## Create an AI Gateway

Follow these steps in the Foundry portal to enable AI Gateway for a resource.

-
Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**. Select

**Operate**>**Admin console**.Open the

**AI Gateway**tab.Select

**Add AI Gateway**.Select the Foundry resource you want to connect with the gateway.

Select

**Create new**or**Use existing**APIM.Name the gateway, and select

**Add**to create or associate the APIM instance.Validate that the AI Gateway is listed now.

Once AI Gateway is configured for the Foundry resource, each project has its own configuration, including if they want to use AI Gateway or not. New projects created in the Foundry resource have AI Gateway enabled by default. However, existing projects must be enabled for AI Gateway.

To add existing projects to the AI Gateway, select the name of the AI Gateway you created. You see a list of all the projects in the Foundry resource with a column

**Gateway status**showing if the project has AI Gateway enabled or not. Locate your project and then select**Add project to gateway**. The column**Gateway status**shows**Enabled**.

## Governance scenarios

Once you configured AI Gateway for your resource and project, you can:

[Configure token limits for models](../control-plane/how-to-enforce-limits-models?view=foundry).[Add custom agents to Control Plane](../control-plane/register-custom-agent?view=foundry).- Govern MCP and A2A agent tools.

## Clean up resources

If you created a dedicated APIM instance for this purpose:

- Confirm that no other workloads depend on it.
- Disable the AI Gateway for all projects in the Foundry resource it's associated with.
- Remove linked resources in Azure portal.
- Delete the APIM instance with the same name as the AI gateway in Azure portal (if it isn't used for any other purpose).