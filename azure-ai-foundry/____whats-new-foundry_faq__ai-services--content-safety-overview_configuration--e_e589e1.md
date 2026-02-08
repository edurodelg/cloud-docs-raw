---
merged_at: 2026-02-08T01:11:03.854961
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/whats-new-foundry -->

# What's new in Microsoft Foundry documentation?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Welcome! This article highlights key changes and updates in Microsoft Foundry documentation for December 2025.

This month marks a significant update to our documentation structure. With the introduction of the new Microsoft Foundry portal, we now maintain two corresponding versions of the documentation to support each portal experience. This dual-version approach ensures that users can access accurate, version-specific guidance tailored to their portal environment.

## New articles

Available in Foundry (new) only:

[Developer journey: Idea to prototype](tutorials/developer-journey-idea-to-prototype?view=foundry-classic)[Publish agents in Microsoft Foundry](agents/how-to/publish-agent?view=foundry-classic)[Agent memory concepts](agents/concepts/what-is-memory?view=foundry-classic)[Build your own MCP server](mcp/build-your-own-mcp-server?view=foundry-classic)[Manage agent identities with Microsoft Entra ID](agents/concepts/agent-identity?view=foundry-classic)[Optimization model upgrade](observability/how-to/optimization-model-upgrade?view=foundry-classic)[Cluster analysis](observability/how-to/cluster-analysis?view=foundry-classic)[Optimization dashboard](observability/how-to/optimization-dashboard?view=foundry-classic)[Human evaluation](observability/how-to/human-evaluation?view=foundry-classic)[Azure Language tools and agents](../ai-services/language-service/concepts/foundry-tools-agents?view=foundry-classic)[Azure Language CLU Multi-turn conversations](../ai-services/language-service/conversational-language-understanding/concepts/multi-turn-conversations?view=foundry-classic)

Available in both Foundry (new) and Foundry (classic):

[Install CLI SDK](how-to/develop/install-cli-sdk?view=foundry-classic)[SDK overview](how-to/develop/sdk-overview?view=foundry-classic)[High availability and resiliency](how-to/high-availability-resiliency?view=foundry-classic)[Agent service disaster recovery](how-to/agent-service-disaster-recovery?view=foundry-classic)[Agent service operator disaster recovery](how-to/agent-service-operator-disaster-recovery?view=foundry-classic)[Agent service platform disaster recovery](how-to/agent-service-platform-disaster-recovery?view=foundry-classic)[Integrate with other apps](how-to/integrate-with-other-apps?view=foundry-classic)[Create a custom photo avatar](../ai-services/speech-service/text-to-speech-avatar/custom-photo-avatar-create?view=foundry-classic)[Customize voice live](../ai-services/speech-service/voice-live-how-to-customize?view=foundry-classic)[Bring your own model](../ai-services/speech-service/how-to-bring-your-own-model?view=foundry-classic)[Use the LLM-speech API](../ai-services/speech-service/llm-speech?view=foundry-classic)[Priority processing for Foundry Models](openai/concepts/priority-processing?view=foundry-classic)[Classification in Content Understanding Studio](../ai-services/content-understanding/how-to/classification-content-understanding-studio?view=foundry-classic)[Foundry playgrounds](concepts/concept-playgrounds?view=foundry-classic)[Use Claude in Foundry Models](foundry-models/how-to/use-foundry-models-claude?view=foundry-classic)[Monitor and manage agents with Foundry control plane](control-plane/overview?view=foundry-classic)

### Updated articles

All articles were updated in some way this month:

- Articles that apply to the new version were updated to add version-specific information.
- Articles that apply to both the new Microsoft Foundry and classic versions include banners that you can use to switch between the two versions to see the relevant content for each.
- Articles that apply only to the classic version include a banner indicating this limitation.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/faq -->

# Microsoft Foundry (classic) frequently asked questions

FAQ for [Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). If you can't find answers to your questions in this document, and still need help check the [Foundry Tools support options guide](../ai-services/cognitive-services-support-options?view=foundry-classic&context=/azure/ai-foundry/openai/context/context). Azure OpenAI is part of Foundry Tools.

## General questions

### Who is Microsoft Foundry (classic) intended for?

Microsoft Foundry (classic) is intended for AI software developers - including cloud architects and technical decision-makers who want to create generative AI applications and custom copilot experiences.

### How can customers access Microsoft Foundry (classic)?

Customers can explore Microsoft Foundry (classic) unauthenticated - including its cutting-edge AI capabilities. When you're ready to begin using templates, tools, and the robust model catalog to stitch together your own AI solutions, you're prompted to register or sign in to your Azure account. Currently, there's no extra charge for using Microsoft Foundry. When deploying solutions, you're billed for the Foundry Tools, Azure Machine Learning, and other Azure resources used inside of Microsoft Foundry (classic) at their existing rates.

### What regions is Microsoft Foundry (classic) available in?

Microsoft Foundry (classic) is available in most regions where Foundry Tools are available. For more information, see [region support for Microsoft Foundry](reference/region-support?view=foundry-classic).

### Can I integrate Microsoft Fabric data into Microsoft Foundry?

Yes. Microsoft Foundry (classic) supports seamless access to data in the Microsoft Fabric datastore Lakehouse without having to move or copy data. Data from Amazon S3 bucket can be accessed via Fabric shortcuts in Microsoft Foundry (classic) portal directly from Amazon S3 location without having to create a copy of the data in Azure.

### Can I use models other than ChatGPT in Microsoft Foundry (classic) portal?

Yes. Microsoft Foundry (classic) includes a robust and growing catalog of frontier and open-source models from OpenAI, Hugging Face, Meta, and more that can be applied over your data. You can even compare models by task using open-source datasets and evaluate the model with your own test data to see how the pretrained model would perform to fit your own use case.

### Will there be multiple varying model benchmarks in Microsoft Foundry (classic) portal based on individual projects and data sources?

In the model benchmarks view, customers can view varying model benchmarks published by Microsoft Foundry.

### Is prompt flow Microsoft's equivalent to LangChain?

Prompt flow is complementary to LangChain and Semantic Kernel and it can work with either. Prompt flow supports LLMOps for generative AI solutions, providing evaluation, connection management, and flow logic to help debug applications, manage deployment, and monitor at scale.

### How is prompt injection handled, and how do we ensure no malicious code is running from prompt injection?

Prompt templates in prompt flow provide robust examples and instructions for avoiding prompt injection attacks in the application. Azure AI Content Safety helps detect offensive or inappropriate content in text and images. Content moderation also checks for jailbreaks.

### What is the billing model for serverless API deployments?

Microsoft Foundry (classic) offers serverless API deployment models and hosted fine-tuning for [Llama 2 family models](concepts/models-inference-examples?view=foundry-classic). Currently, there's no extra charge for Microsoft Foundry (classic) outside of typical Foundry Tools and other Azure resource charges.

### Can all models be secured with content filtering?

Azure AI Content Safety can be used for AI-generated content from Azure OpenAI in Microsoft Foundry (classic) Models, open-source, and frontier models. For more information, see [How Azure AI Content Safety helps protect users from the classroom to the chatroom](https://aka.ms/contentsafety_GA_blog).

### Do you use my company data to train any of the models?

Azure OpenAI doesn't use customer data to retrain models. For more information, see the [Azure OpenAI data, privacy, and security guide](/en-us/azure/ai-foundry/responsible-ai/openai/data-privacy).

## Learning more and where to ask questions

### Where can I get training to get started learning and build my skills around Azure OpenAI?

Check out our [introduction to Azure OpenAI training course](/en-us/training/modules/explore-azure-openai/).

### Where can I post questions and see answers to other common questions?

- We recommend posting questions on
[Microsoft Q&A](/en-us/answers/tags/387/azure-openai) - Alternatively, you can post questions on
[Stack Overflow](https://stackoverflow.com/search?q=azure+openai)

### Where do I go for Foundry Tools customer support?

You can learn about all the support options for Foundry Tools in the [support and help options guide](../ai-services/cognitive-services-support-options?view=foundry-classic&context=/azure/cognitive-services/openai/context/context).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/ai-services/content-safety-overview -->

# Content Safety in the Microsoft Foundry portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Azure AI Content Safety is an AI service that detects harmful user-generated and AI-generated content in applications and services. Azure AI Content Safety includes APIs that help you detect and prevent the output of harmful content. The interactive Content Safety **try it out** page in the [Microsoft Foundry portal](https://ai.azure.com/?cid=learnDocs) lets you view, explore, and try out sample code for detecting harmful content across different modalities.

## Features

Use Azure AI Content Safety for the following scenarios:

### Text content

**Moderate text content**: Scans and moderates text content. It identifies and categorizes text based on different levels of severity to ensure appropriate responses.**Groundedness detection**: Determines if the AI's responses are based on trusted, user-provided sources. This feature ensures that the answers are "grounded" in the intended material. Groundedness detection helps improve the reliability and factual accuracy of responses.**Protected material detection for text**: Identifies protected text material, such as known song lyrics, articles, or other content. This feature ensures that the AI doesn't output this content without permission.**Protected material detection for code**: Detects code segments in the model's output that match known code from public repositories. This feature helps prevent uncredited or unauthorized reproduction of source code.**Prompt shields**: Provides a unified API to address "Jailbreak" and "Indirect Attacks":- Jailbreak Attacks: Attempts by users to manipulate the AI into bypassing its safety protocols or ethical guidelines. Examples include prompts designed to trick the AI into giving inappropriate responses or performing tasks it was programmed to avoid.
- Indirect Attacks: Also known as Cross-Domain Prompt Injection Attacks. Indirect attacks involve embedding malicious prompts within documents that the AI might process. For example, if a document contains hidden instructions, the AI might inadvertently follow them, leading to unintended or unsafe outputs.


### Image content

**Moderate image content**: Similar to text moderation, this feature filters and assesses image content to detect inappropriate or harmful visuals.**Moderate multimodal content**: Designed to handle a combination of text and images. It assesses the overall context and any potential risks across multiple types of content.

### Custom filtering

**Custom categories**: Allows users to define specific categories for moderating and filtering content. Tailors safety protocols to unique needs.**Safety system message**: Provides a method for setting up a "System Message" to instruct the AI on desired behavior and limitations. It reinforces safety boundaries and helps prevent unwanted outputs.

## Understand harm categories

### Harm categories

| Category | Description | API term |
|---|---|---|
| Hate and Fairness | Hate and fairness harms refer to any content that attacks or uses discriminatory language with reference to a person or identity group based on certain differentiating attributes of these groups. This includes, but isn't limited to:
|
`Hate` |
| Sexual | Sexual describes language related to anatomical organs and genitals, romantic relationships and sexual acts, acts portrayed in erotic or affectionate terms, including those portrayed as an assault or a forced sexual violent act against one's will. This includes but isn't limited to:
|
`Sexual` |
| Violence | Violence describes language related to physical actions intended to hurt, injure, damage, or kill someone or something; describes weapons, guns, and related entities. This includes, but isn't limited to:
|
`Violence` |
| Self-Harm | Self-harm describes language related to physical actions intended to purposely hurt, injure, damage one's body or kill oneself. This includes, but isn't limited to:
|
`SelfHarm` |

### Severity levels

| Level | Description |
|---|---|
| Safe | Content might be related to violence, self-harm, sexual, or hate categories. However, the terms are used in general, journalistic, scientific, medical, and similar professional contexts, which are appropriate for most audiences. |
| Low | Content that expresses prejudiced, judgmental, or opinionated views, includes offensive use of language, stereotyping, use-cases exploring a fictional world (for example, gaming, literature) and depictions at low intensity. |
| Medium | Content that uses offensive, insulting, mocking, intimidating, or demeaning language towards specific identity groups, includes depictions of seeking and executing harmful instructions, fantasies, glorification, promotion of harm at medium intensity. |
| High | Content that displays explicit and severe harmful instructions, actions, damage, or abuse; includes endorsement, glorification, or promotion of severe harmful acts, extreme or illegal forms of harm, radicalization, or nonconsensual power exchange or abuse. |

## Limitations

For supported regions, rate limits, and input requirements for all features, see the [Content Safety service overview](/en-us/azure/ai-services/content-safety/overview). For supported languages, see the [Language support](/en-us/azure/ai-services/content-safety/language-support) page.

## Next step

Get started using Azure AI Content Safety in Foundry portal by following the [How-to guide](/en-us/azure/ai-services/content-safety/how-to/foundry).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/configuration/enable-ai-api-management-gateway-portal -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-use-of-ai-overview -->

# Responsible AI for Microsoft Foundry

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

This article provides an overview of the resources for building and deploying trustworthy AI agents. This includes end-to end security, observability, and governance with controls and checkpoints at all stages of the agent lifecycle. Our recommended essential development steps are grounded in the [Microsoft Responsible AI Standard](https://aka.ms/RAI), which sets policy requirements that our own engineering teams follow. Much of the content of the Standard follows a pattern, asking teams to Discover, Protect, and Govern potential content risks.

At Microsoft, our approach is guided by a governance framework rooted in AI principles, which establish product requirements and serve as our "north star." When we identify a business use case for generative AI, we first discover and assess the potential risks of the AI system to pinpoint critical focus areas.

Once we identify these risks, we evaluate their prevalence within the AI system through systematic measurement, helping us prioritize areas that need attention. We then apply appropriate protection at the model and agent level against those risks.

Finally, we examine strategies for managing risks in production, including deployment and operational readiness and setting up monitoring to support ongoing governance to ensure compliance and surface new risks after the application is live.

In alignment with Microsoft's RAI practices, these recommendations are organized into three stages:

**Discover**agent quality, safety, and security risks before and after deployment.**Protect**– at both the model output and agent runtime levels – against security risks, undesirable outputs, and unsafe actions.**Govern**agents through tracing and monitoring tools and compliance integrations.

## Security alerts and recommendations

You can view Defender for Cloud security alerts and recommendations to improve your security posture in the **Risks + alerts** section. Security alerts are the notifications generated by Defender for Foundry Tools plan when threats are identified in your AI workloads. You can take action in Azure portal or in the Defender portal to address these alerts.

- To learn more about security alerts, see
[Alerts for AI workloads (Preview)](/en-us/azure/defender-for-cloud/alerts-ai-workloads). - To learn more about security recommendations, see
[Review security recommendations](/en-us/azure/defender-for-cloud/review-security-recommendations).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/ -->

# Microsoft Foundry documentation

Overview

[What is Microsoft Foundry?](what-is-foundry?view=foundry-classic)

This browser is no longer supported.

Upgrade to Microsoft Edge to take advantage of the latest features, security updates, and technical support.

The agent factory - Design, customize, manage, and support AI applications and agents at scale.

Overview

Concept

How-To Guide

Concept

Get started with the Foundry SDK in your favorite programming language.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-status-dashboard-documentation -->

# Microsoft Foundry status dashboard

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

The [Microsoft Foundry Status Dashboard](https://status.ai.azure.com/) provides visibility into the health and availability of key Foundry services. It helps customers monitor service status, stay informed about ongoing incidents, and plan around scheduled maintenance windows.

This dashboard is currently in **preview**, and it might not reflect all components or issues.

## Prerequisites

- A web browser.

## Check service status

- Open the
[Microsoft Foundry Status Dashboard](https://status.ai.azure.com/). - Review the overall status at the top of the page.
- Select a component to view details and recent status changes.
- Select
**Incidents**to review incident history. - Select
**Subscribe to updates**to get notified about updates.

## Key features

**Live status indicators**for core Foundry services.**Incident reports**with timelines, resolutions, and root cause summaries.**Historical uptime**to help assess service reliability over time.

## Frequently asked questions

**Q: Is this data real-time?**

The dashboard updates as incident and maintenance status changes are posted.

**Q: What does it mean that this dashboard is in “Preview”?**

During preview, service coverage is expanding and the experience is still being refined. Some services might not appear, and update timing might vary.

**Q: Can I subscribe to updates?**

Yes. Select **Subscribe to updates** in the dashboard.

**Q: Does the dashboard cover all regions and environments?**

The dashboard is in preview, and coverage might vary by component.

**Q: How should I report discrepancies or missing status updates?**

If you notice a gap between your experience and what you see on the dashboard, contact Microsoft support or create an Azure support request.

## Feedback and support

If you have questions, suggestions, or run into problems, contact Microsoft support.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/guardrails/intervention-points -->

# Intervention points

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Agentic AI expands both capability and attack surface. As soon as an agent can call external tools, write to databases, or trigger downstream processes, malfunctions or malicious attacks can lead to steering it off course, leaking sensitive data, or executing harmful actions. Relying solely on guardrails applied to models can leave these vectors exposed. To close this gap Microsoft Foundry allows guardrails to be applied directly to agents and allows the individual controls within those guardrails to be applied to four different intervention points:

| Intervention Point | Description | Example Control at this Intervention Point |
|---|---|---|
| User input | A query sent from a user to a model or agent. Sometimes referred to as "prompt." Some controls at this intervention point require the inclusion of document embedding by the user to take effect. | Risk: User input attacksAction: Annotate and blockWhen this control is specified in an agent's or model's guardrail, the user's input is scanned by a classification model that detects jailbreak attacks. If an attack is detected, the user's input is blocked from being sent to the model, halting the model. |
| Tool call (Preview) | The next action the agent is proposing to take, as generated by its underlying model. The tool call consists of which tool is called and the arguments it's called with, including data being sent to the tool. | Risk: Hate (High) Action: Annotate and blockWhen this control is specified, every time the agent is about to execute a tool call, the proposed content being sent to the tool is scanned for hateful content. If any is detected, the tool call won't be executed, and the agent stops functioning until there is another user input. |
| Tool response (Preview) | The content sent back by a tool, internal to an agent's orchestration and before the content is to the agent's memory or given back to the end user. | Risk: Indirect attackAction: Annotate and blockWhen this control is specified, the full payload sent back from each tool to this agent is scanned for attempted indirect prompt injection attacks. If detected, the agent stops operating immediately, and prevents the malicious content from being saved by the agent and from maliciously steering the agent off-track. |
| Output | The final content sent back to the end user in response to their query. | Risk: Protected Material for TextAction: Annotate onlyWhen this control is specified, the final content meant to be displayed to the user is scanned for certain types of copyrighted text. If detected, there is a flag in the annotation response for the API used to call this model or agent. |

Important

Only certain types of tools are subject to controls at the tool call and tool response intervention points. Currently, Azure AI Search, Azure Functions, OpenAPI, Sharepoint Grounding, Fabric Data Agent, Bing Grounding, Bing Custom Search, and Browser Automation support moderation.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/guardrails/guardrails-overview -->

# Guardrails and controls overview in Microsoft Foundry

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Microsoft Foundry offers safety and security guardrails that can be applied to core models, including image generation models, and agents. Agent guardrails are in preview. Guardrails consist of a set of controls. The controls define a risk to be detected, intervention points to scan for the risk, and the response action to take in the model or agent when the risk is detected. For example, a risk detection could be the annotation of the risk or blocking the model or agent from further output.

Risks are flagged via a set of classification models designed to detect and prevent the output of undesirable behavior and/or harmful content. Four intervention points are currently supported: user input, tool call (Preview), tool response (Preview), and output. Tool call and tool responses intervention points are applicable to agents only and scan the tool call made as well as content sent to the tool, and the output back from the tool, respectively.

Variations in API configurations and application design might affect completions and thus filtering behavior.

Important

The guardrail system applies to all Models sold directly by Azure, except for prompts and completions processed by the audio models such as Whisper. For more information, see [Audio models in Azure OpenAI](../openai/concepts/models?view=foundry#audio-models). The guardrail system currently applies only to agents developed in the Foundry Agent Service, not to other agents registered in the Foundry Control Plane.

## Guardrails for agents vs models

An individual Foundry guardrail can be applied to one or many models and one or many agents in a project. Some controls within a guardrail may not be relevant to models because the risk, intervention point, or action is specific to agentic behavior or tool calls. Those controls aren't run on models using that guardrail.

Some risks in Preview aren't yet supported for agents. When controls involving that risks are created in a guardrail, and the guardrail is applied to an agent, that control won't take effect in that agent. It's still applied to models using the same guardrail.

### Risk applicability

The following table summarizes which risks are applicable to models and agents:

| Risk | Applicable to Models | Applicable to Agents (Preview) |
|---|---|---|
| Hate | ✅ | ✅ |
| Sexual | ✅ | ✅ |
| Self-harm | ✅ | ✅ |
| Violence | ✅ | ✅ |
| User prompt attacks | ✅ | ✅ |
| Indirect attacks | ✅ | ✅ |
| Spotlighting (Preview) | ✅ | ❌ |
| Protected material for code | ✅ | ✅ |
| Protected material for text | ✅ | ✅ |
| Groundedness (Preview) | ✅ | ❌ |
| Personally identifiable information (Preview) | ✅ | ✅ |

### Intervention point applicability

The following table summarizes which intervention points are applicable to models and agents:

| Intervention point | Applicable to Models | Applicable to Agents (Preview) |
|---|---|---|
| User input (prompt) | ✅ | ✅ |
| Tool call (Preview) | ❌ | ✅ |
| Tool response (Preview) | ❌ | ✅ |
| Output (completion) | ✅ | ✅ |

### Action applicability

The following table summarizes which actions are applicable to models and agents:

| Action | Applicable to Models | Applicable to Agents (Preview) |
|---|---|---|
| Annotate | ✅ | ❌ |
| Annotate and block | ✅ | ✅ |

### Guardrail inheritance and override

Important

Risks are detected in an agent based on the guardrail it's assigned, not the guardrail of its underlying model. The agentic guardrail fully overrides the model's guardrail.

**Example scenario:**

- A model deployment has a control with Violence detection set to
**High**for user input and output - An agent using that model has a control with Violence detection set to
**Low**for user input and output. The agent has no controls for Violence detection at all for tool calls and responses

**Expected behavior for Violence detection in that agent:**

- User queries to the agent are scanned for Violence at a
**Low**level - Tool calls generated internally to the agent by its underlying model, including the content then sent to that tool during the tool call's execution, will
**not**be scanned for Violence - The response back from the tool will
**not**be scanned for Violence - The final output returned to the user in response to their original query are scanned for Violence at a
**Low**level

## Default guardrails

By default, models are assigned the **Microsoft.DefaultV2** guardrail. For more information on what is included in the Microsoft Default, see Default safety policy.

Unless another custom guardrail is specified upon creation, agents are assigned by default the guardrails of the model deployment being used by that agent. In other words, if no custom guardrails are specified for an agent, and that agent leverages a GPT-4o mini deployment using a guardrail named "MyCustomGuardrails," the agent will also use "MyCustomGuardrails" until another guardrail is specifically assigned to the agent. An agent will only inherit the Microsoft Default guardrails if its model is using that guardrail or if it's specifically assigned the default manually.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/what-is-foundry -->

# What is Microsoft Foundry?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

**Microsoft Foundry** is a unified Azure platform-as-a-service offering for enterprise AI operations, model builders, and application development. This foundation combines production-grade infrastructure with friendly interfaces, enabling developers to focus on building applications rather than managing infrastructure.

Microsoft Foundry unifies agents, models, and tools under a single management grouping with built-in enterprise-readiness capabilities including tracing, monitoring, evaluations, and customizable enterprise setup configurations. The platform provides streamlined management through unified Role-based access control (RBAC), networking, and policies under one Azure resource provider namespace.

Tip

Azure AI Foundry is now Microsoft Foundry. Screenshots appearing throughout this documentation are in the process of being updated.

Tip

Azure AI Foundry is now Microsoft Foundry. Screenshots appearing throughout this documentation are in the process of being updated.

## Microsoft Foundry portals

There are two different portals for you to use to interact with Microsoft Foundry. A toggle in the portal banner allows you to switch between the two versions.

| Portal | Banner display | When to use |
|---|---|---|
| Microsoft Foundry (classic) | Choose this portal when working with multiple resource types: Azure OpenAI, Foundry resources, hub-based projects, or Foundry projects. | |
| Microsoft Foundry (new) | Choose this portal for a seamless experience that combines simplicity with powerful and secure tools to build, manage and grow multi-agent applications. Only Foundry projects are visible here - use (classic) for all other resource types. |

Tip

All links to [Microsoft Foundry](https://ai.azure.com/?cid=learnDocs) open whichever version you last used.

## Microsoft Foundry (classic)

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs) (classic) is designed for developers to:

- Build generative AI applications and AI agents on an enterprise-grade platform.
- Explore, build, test, and deploy using cutting-edge AI tools and ML models, grounded in responsible AI practices.
- Collaborate with a team for the full life-cycle of application development.
- Work across model providers with a consistent API contract.

With Microsoft Foundry, you can explore a wide variety of models, services and capabilities, and get to building AI applications that best serve your goals. Microsoft Foundry facilitates scalability for transforming proof of concepts into full-fledged production applications with ease. Continuous monitoring and refinement support long-term success.

## Microsoft Foundry (new)

**Microsoft Foundry (new)** delivers a modernized experience with powerful enhancements designed for flexibility and scale:

– Build advanced automation using SDKs for C# and Python that enable collaborative agent behavior and complex workflow execution.[Multi-Agent Orchestration and Workflows](agents/concepts/workflow?view=foundry&preserve-view=true)– Publish agents to Microsoft 365, Teams, and BizChat, plus leverage containerized deployments for greater portability.[Expanded Integration Options](agents/how-to/publish-copilot?view=foundry&preserve-view=true)– Access the Foundry tool catalog (preview) with a public tool catalog and your own private catalogs, connecting over 1,400 tools in Microsoft Foundry.[Expanded Tool Access](agents/concepts/tool-catalog?view=foundry&preserve-view=true)– Use memory to help your agent retain and recall contextual information across interactions. Memory maintains continuity, adapts to user needs, and delivers tailored experiences without requiring repeated input.[Enhanced Memory Capabilities](agents/concepts/what-is-memory?view=foundry&preserve-view=true)– Connect your agent to a Foundry IQ knowledge base to ground responses in enterprise or web content. This integration provides reliable, citation-backed answers for multi-turn conversations.[Knowledge Integration](agents/concepts/what-is-foundry-iq?view=foundry&preserve-view=true)– Monitor performance and governance using built-in metrics and model tracking tools.[Real-Time Observability](how-to/continuous-evaluation-agents?view=foundry&preserve-view=true)**Enhanced Enterprise Support**– Use open protocols in Foundry Agent Service with full authentication support in MCP and A2A tool, AI gateway integration, and Azure Policy integration.**Centralized AI asset management**- Observe, optimize, and manage 100% of your AI assets (agents, models, tools) in one place, the**Operate**section. Register agents from other clouds, get alerts when an agent or model requires your attention, and effectively manage your AI fleet health as that fleet scales.**Optimized Developer Experience**– Experience faster load times and dynamic prefetching for smooth development and deployment.**Streamlined Navigation**– Navigate efficiently with a redesigned interface that places key controls where you need them, improving workflow efficiency.

## Choosing a project

In the Foundry (new) portal, the project you're working with appears in the upper-left corner of most pages.

- If you see a long list of projects instead, select a project to begin. This brings you to the
**Home**page with the project name in the upper-left corner. - To switch to another recently used project, select the project name in the upper-left corner, then select the other project.
- To see all of your Foundry projects, select the project name in the upper-left corner, the select
**View all projects**. Select the next project you want to work on.

## Find other resources

The Foundry (new) portal displays only the **default** project for each Foundry resource, not other resources or hub-based projects you might have created in Foundry (classic). If you created multiple projects under the same Foundry resource, you can identify which project is the default by checking the Microsoft Foundry (classic) portal. The default project is marked with (default) next to its name.

To find these other resources, select the project name in the upper-left corner, then select **View all resources**. A new browser tab opens the Foundry (classic) portal. [Switch to Microsoft Foundry (classic) documentation](?view=foundry-classic&preserve-view=true) to work with these other resources in the Foundry (classic) portal.

## Work in a Foundry project

A Foundry project is where you do most of your development work. You can work with your project in the Foundry portal, or use the SDK in your preferred development environment.

Foundry projects provide developers with self-serve capabilities to independently create new environments for exploring ideas and building prototypes, while managing data in isolation. Projects act as secure units of isolation and collaboration where agents share file storage, thread storage (conversation history), and search indexes. You can also bring your own Azure resources for compliance and control over sensitive data.

## Microsoft Foundry API and SDKs

The [Microsoft Foundry API](/en-us/rest/api/aifoundry/) is designed specifically for building agentic applications and provides a consistent contract for working across different model providers. The API is complemented by SDKs to make it easy to integrate AI capabilities into your applications. [SDK Client libraries](how-to/develop/sdk-overview?view=foundry-classic) are available for:

- Python
- C#
- JavaScript/TypeScript (preview)
- Java (preview)

The [Microsoft Foundry for VS Code Extension](how-to/develop/get-started-projects-vs-code?view=foundry-classic) helps you explore models and develop agents directly in your development environment.

## Types of projects

Microsoft Foundry (classic) supports two types of projects: a **hub-based project** and a **Foundry project**. In most cases, you want to use a Foundry project.

-
A

**Foundry project**is managed under a Microsoft Foundry resource. It's a container for access management, data upload and integration, and monitoring. This lets you keep your work separated between use cases without needing to create extra Azure resources. -
A

**hub-based project**is hosted by a[Microsoft Foundry hub](concepts/ai-resources?view=foundry-classic). If your company has an administrative team that created a hub for you, you can create a project from that hub. If you're working on your own, you can create a project and a default hub is automatically be created for you. To understand how the newer Foundry project differs from the hub-based project, see

[New Foundry projects overview](how-to/migrate-project?view=foundry-classic#new-foundry-projects-overview).

### Which type of project do I need?

- In general, you should use a Foundry project if you're looking to build agents or work with models.
- Use a hub-based project when you need features that aren't available in a Foundry project. See the following table for more on feature availability.

Note

New agents and model-centric capabilities are only available on Foundry projects, including access to the Foundry API and Foundry Agent Service in general availability. To migrate your hub-based project to a Foundry project, see [Migrate from hub-based to Foundry projects](how-to/migrate-project?view=foundry-classic).

This table summarizes features available in the two project types:

| Capability | Foundry project | hub-based project |
|---|---|---|
| Agents | ✅ (GA) | ✅ (Preview only) |
| Models sold directly by Azure - Azure OpenAI, DeepSeek, xAI, etc. | ✅ | Available via connections |
| Partner & Community Models sold through Marketplace - Stability, Cohere, etc. | ✅ | Available via connections |
| Models deployed on managed compute (e.g. HuggingFace) | ✅ | |
| Foundry SDK and API | ✅ | Limited* |
| OpenAI SDK and API | ✅ | Available via connections |
| Evaluations | ✅ (preview) | ✅ |
| Playgrounds | ✅ | ✅ |
| Content understanding | ✅ | ✅ |
| Azure Language resource | ✅ | |
| Model router | ✅ | ✅ |
| Datasets | ✅ | ✅ |
| Indexes | ✅ | ✅ |
| Project files API (Foundry-managed storage) | ✅ | Limited |
| Project-level isolation of files and outputs | ✅ | Limited |
| Bring-your-own Key Vault to store connection secrets | ✅ | ✅ |
| Bring-your-own Storage for Agent service | ✅ | ✅ |
| Prompt flow | ✅ |

*New feature enhancements primarily land on the [Microsoft Foundry resource type](concepts/resource-types?view=foundry-classic).

### How do I know which type of project I have?

Here are some of the ways to identify your project type:

From the

**breadcrumb navigation**section- A Foundry project displays
**(Foundry)**on the second line - A hub-based project displays
**(Hub)**on the second line

- A Foundry project displays
From the

**All resources**page- A Foundry project displays
**(Foundry)**as the parent resource - A hub-based project displays
**(Hub)**as the parent resource

- A Foundry project displays

## Navigate in the Foundry (classic) portal

In the Foundry (classic) portal, you can navigate among all your resources using the breadcrumbs at the top of the page. The breadcrumbs show recent resources, along with a link to all resources.

The left pane is organized around your goals. Generally, as you develop with Azure AI, you'll likely go through a few distinct stages of project development:

**Define and explore**. In this stage you define your project goals, and then explore and test models and services against your use case to find the ones that enable you to achieve your goals.**Build and customize**. In this stage, you're actively building solutions and applications with the models, tools, and capabilities you selected. You can also customize models to perform better for your use case by fine-tuning, grounding in your data, and more. Building and customizing might be something you choose to do in the Foundry portal, or through code and the Foundry SDKs. Either way, a project provides you with everything you need.- Once you're actively developing in your project, the
**Overview**page shows the things you want easy access to, like your endpoints and keys.

- Once you're actively developing in your project, the
**Observe and improve**. In this stage, you're looking for where you can improve your application's performance. You might choose to use tools like tracing to debug your application or compare evaluations to hone in on how you want your application to behave. You can also integrate with safety & security systems so you can be confident when you take your application to production.

If you're an admin, or leading a development team, and need to manage the team's resources, project access, quota, and more, you can do that in the Management Center.

## Customize the left pane

The left pane of the Foundry (classic) portal is your main navigation tool. Customize this area to show the parts of the portal you want to use.

Pin or unpin items into the left pane. When you unpin an item, it's hidden from the left pane but can be found again in the **...More** menu.

- Select
**... More**at the bottom of the pane to see items to pin and unpin. - Customize each project separately. The left pane isn't shared across projects.
- The left pane isn't shared across users. Each user customizes their own left pane for each project.

## Management center

The management center is a part of the Foundry (classic) portal that streamlines governance and management activities. In the management center, you can view and manage:

- Projects and resources
- Quotas and usage metrics
- Govern access and permissions

For more information, see [Management center overview](concepts/management-center?view=foundry-classic).

## Pricing and billing

Microsoft Foundry is monetized through individual products customer access and consume in the platform, including API and models, complete AI toolchain, and responsible AI and enterprise grade production at scale products. Each product has its own billing model and price.

The platform is free to use and explore. Pricing occurs at deployment level.

Using Foundry also incurs cost associated with the underlying services. To learn more, read [Plan and manage costs for Foundry Tools](concepts/manage-costs?view=foundry-classic).

## Region availability

Foundry is available in most regions where Foundry Tools are available. For more information, see [region support for Microsoft Foundry](reference/region-support?view=foundry-classic).

## How to get access

You can [explore Foundry portal (classic) (including the model catalog)](concepts/foundry-models-overview?view=foundry-classic) without signing in.

But for full functionality, you need an [Azure account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

You need an [Azure account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). Then sign in to [Microsoft Foundry](https://ai.azure.com?cid=learnDocs) and toggle the **Try the new Foundry** on.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/quotas-limits -->

# Foundry Agent Service quotas and limits

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

This article describes the quotas and limits for Foundry Agent Service.

## How quotas and limits apply

Foundry Agent Service enforces limits in two places:

**Agent Service limits**. Limits for agent and thread artifacts, such as file uploads, vector store attachments, message counts, and tool registration.**Model limits**. Quotas and rate limits for the model deployments your agents call.

If you're using threads and messages, see [Threads, runs, and messages in Foundry Agent Service](concepts/threads-runs-messages?view=foundry-classic). If you're using file search, see [Vector stores for file search](concepts/vector-stores?view=foundry&preserve-view=true).

## Default quotas and limits for the service

The following table lists default limits enforced by the Agent Service.

| Limit name | Limit value |
|---|---|
| Maximum number of files per agent/thread | 10,000 |
| Maximum file size for agents | 512 MB |
| Maximum size for all uploaded files for agents | 300 GB |
| Maximum file size in tokens for attaching to a vector store | 2,000,000 tokens |
| Maximum number of messages per thread | 100,000 |
Maximum size of `text` content per message |
1,500,000 characters |
| Maximum number of tools registered per agent | 128 |

## What happens when you reach a limit

When you exceed one of the limits in this article, the related operation fails. For example:

**File exceeds the maximum size**: Uploading the file fails. Split the content into smaller files or reduce file size before you upload.**Vector store token limit**: Attaching a file to a vector store fails if the file exceeds the token limit. Reduce the file content or split it into multiple files.**Thread message cap**: Adding messages can fail after a thread reaches the message limit. Create a new thread for a new conversation session, or archive and rotate threads as part of your application design.**Message content size**: Creating a message can fail if the`text`

content is too large. Send smaller messages, or move large content into files and use file search.**Tool registration cap**: Creating or updating an agent can fail if you register too many tools. Register only the tools you need, and prefer fewer, reusable tools.

For file search scenarios, see [Vector stores for file search](concepts/vector-stores?view=foundry&preserve-view=true) for guidance on managing vector store growth.

## Best practices to stay within limits

Use the following practices to reduce limit-related failures:

**Keep files small and focused**. Prefer multiple smaller documents over a single large document.**Avoid very large messages**. Put long content in uploaded files and query it by using file search.**Plan for long conversations**. Treat threads as session state and rotate to new threads when conversations become very long.**Register only required tools**. Remove unused tools from agent definitions.**Monitor usage trends**. Track agent activity and tokens to identify growth early.

## Quotas and limits for models

Agents follow the quotas and rate limits for the model deployments they use.

For current model quotas and limits, see:

To view or request more model quota, see [Manage and increase quotas for resources with Microsoft Foundry (Foundry projects)](../how-to/quota?view=foundry-classic).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/environment-setup -->

# Set up your environment

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Creating your first agent with Foundry Agent Service is a two-step process:

- Set up your agent environment.
- Create and configure your agent using either the SDK of your choice or the Azure Foundry portal.

Use this article to learn more about setting up your agent environment.

### Required permissions

| Action | Required Role |
|---|---|
| Create an account and project | Azure AI Account Owner |
|

## Set up your agent environment

To get started, you need a Microsoft Foundry resource and a Foundry project.

Agents are created within a specific project, and each project acts as an isolated workspace. This means:

- All agents in the same project share access to the same file storage, thread storage (conversation history), and search indexes.
- Data is isolated between projects. Agents in one project cannot access resources from another.
Projects are currently the unit of sharing and isolation in Foundry. See the
[what is AI foundry](../what-is-foundry?view=foundry-classic)article for more information on Foundry projects.

### Prerequisites

- An Azure subscription -
[Create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - Ensure that the individual creating the account and project has the
**Azure AI Account Owner**role at the subscription scope - If configuring a
[standard setup](#choose-your-setup), the same individual must also have permissions to assign roles to required resources (Cosmos DB, Azure AI Search, Azure Blob Storage). For more information on RBAC roles, specific to Agent Service, see[Agent Service RBAC roles](../concepts/rbac-foundry?view=foundry-classic).- The built-in role needed is
**Role Based Access Administrator**. - Alternatively, having the
**Owner**role at the subscription level also satisfies this requirement. - The key permission needed is:
`Microsoft.Authorization/roleAssignments/write`


- The built-in role needed is

### Choose your setup

Agent Service offers three environment configuration modes to suit different needs:

**Basic Setup**:This setup is compatible with OpenAI Assistants and manages agent states using the platform's built-in storage. It includes the same tools and capabilities as the Assistants API, with added support for non-OpenAI models and tools such as Azure AI Search, and Bing.

**Standard Setup**:Includes everything in the basic setup and fine-grained control over your data by allowing you to use your own Azure resources. All customer data—including files, threads, and vector stores—are stored in your own Azure resources, giving you full ownership and control.

**Standard Setup with Bring Your Own (BYO) Virtual Network**:Includes everything in the Standard Setup, with the added ability to operate entirely within your own virtual network. This setup supports Bring Your Own Virtual Network (BYO virtual network), allowing for strict control over data movement and helping prevent data exfiltration by keeping traffic confined to your network environment.


### Compare setup options

Note

Private Network Isolation in the table below refers to Secured Agent outbound communication. Basic setup doesn't apply, and you can use Private Network Isolation for your Agents with Standard Setup only.

Inbound secured communication can be applied to all of setups below, by adding a private endpoint and disabling the inbound public access for your Foundry Account.

| Use Cases | Basic Setup | Standard Setup with Public Networking | Standard Setup with Private Networking |
|---|---|---|---|
| Get started quickly without managing resources | ✅ | ||
| All conversation history, file, and vector stores are stored in your own resources | ✅ | ✅ | |
| Support for Customer Managed Keys (CMK) | ✅ | ✅ | |
| Private Network Isolation (Bring your own virtual network) | ✅ |

### Deployment options

To customize these templates, see [use your own resources](how-to/use-your-own-resources?view=foundry-classic).

If you want support for Private Network Isolation see [network-secured setup](how-to/virtual-networks?view=foundry-classic) for more information on how to bring your own virtual network.

### [Optional] Model selection in autodeploy template

Important

**Don't change the modelFormat parameter.**

The templates only support deployment of Azure OpenAI models. See which Azure OpenAI models are supported in the [model support](concepts/model-region-support?view=foundry-classic) article.

You can customize the model used by your agent by editing the model parameters in the autodeploy template. To deploy a different model, you need to update at least the `modelName`

and `modelVersion`

parameters.

By default, the deployment template is configured with the following values:

| Model Parameter | Default Value |
|---|---|
| modelName | gpt-4o |
| modelFormat | OpenAI (for Azure OpenAI) |
| modelVersion | 2024-11-20 |
| modelSkuName | GlobalStandard |
| modelLocation | eastus |

### What's next?

- Explore more:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/faq -->

# Foundry Agent Service frequently asked questions

Find answers to common questions about Foundry Agent Service.

If you can't find answers to your questions in this article and you still need help, see [Foundry Tools support and help options](../../ai-services/cognitive-services-support-options?view=foundry-classic). Foundry Agent Service is part of Foundry Tools.

For getting started, see:

## Setup and access

### What's the difference between basic setup and standard setup?

**Basic setup** stores agent state in Microsoft-managed resources.

**Standard setup** stores agent data (threads, files, and vector stores) in your Azure resources that you connect through capability hosts.

To compare setup options and choose the right one, see [Set up your environment](environment-setup?view=foundry-classic#choose-your-setup) and [Capability hosts](concepts/capability-hosts?view=foundry-classic).

### What permissions (RBAC roles) do I need?

Role requirements depend on what you're doing. For example, you typically need permissions to create an account and project, and separate permissions to create and edit agents.

For the current role requirements, see [Required permissions](environment-setup?view=foundry-classic#required-permissions) and [Role-based access control (RBAC) in Microsoft Foundry](../concepts/rbac-foundry?view=foundry-classic).

### Where should I start if I'm new to Foundry Agent Service?

Start with [Set up your environment](environment-setup?view=foundry-classic), then create your first agent.

- Classic experience:
[Quickstart: Create a new agent](quickstart?view=foundry-classic) - New Foundry experience:
[Quickstart: Get started with agents in code](../quickstarts/get-started-code?view=foundry-classic)

## General

### Do you store any data used in the Foundry Agent Service API?

Yes. Foundry Agent Service is a stateful API, which means that it retains data. Two types of data are stored in the Foundry Agent Service API:

**Stateful entities**: Conversations and responses created during usage.**Files and vector stores**: Data uploaded during Foundry Agent Service setup or as part of a response generation.

To learn how conversations and responses work, see [Agent runtime components](concepts/runtime-components?view=foundry-classic).

### Where is this data stored?

**Basic setup**: Data is stored in a secure, Microsoft-managed storage account that's logically separated.**Standard setup**: Data is stored in your own Azure resources, so you have full ownership and control.

To learn about setup options that control where data is stored, see [Set up your environment](environment-setup?view=foundry-classic#choose-your-setup).

### How long is this data stored?

Data persists unless you explicitly delete it.

For concepts and terminology (for example, conversation and response), see [Agent runtime components](concepts/runtime-components?view=foundry-classic).

### Does Foundry Agent Service support CMK encryption?

- Basic setup supports Microsoft-managed keys only.
- Standard setup supports customer-managed keys (CMKs).

### Does Microsoft use my data for training models?

No, Microsoft doesn't use your data for training models. For more information, see the [Responsible AI documentation](/en-us/azure/ai-foundry/responsible-ai/openai/data-privacy).

### Where is data stored geographically?

Foundry Agent Service endpoints are regional, and data is stored in the same region as the endpoint. For more information, see the [Azure data residency documentation](https://azure.microsoft.com/explore/global-infrastructure/data-residency/#overview).

### How am I charged for Foundry Agent Service?

You're charged for inference cost (input and output) of the base model that you're using for each agent (for example, gpt-4-0125). If you created multiple agents, you're charged for the base model attached to each agent.

If you enabled the Code Interpreter tool, you're charged for its use per session. For example, if your agent calls Code Interpreter simultaneously in two threads, this activity creates two Code Interpreter sessions. Each of those sessions is charged.

By default, each session is active for one hour. If your user keeps giving instructions to Code Interpreter in the same thread for up to one hour, you pay this fee only once.

File search is billed based on the vector storage that you use.


For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/ai-foundry/).

### Is there any additional pricing or quota for using Foundry Agent Service?

No. All [quotas](quotas-limits?view=foundry-classic) apply to using models with Foundry Agent Service.

## Tools and integrations

### Where can I learn about tools like Code Interpreter and File Search?

Start with [Tools overview](how-to/tools-classic/overview?view=foundry-classic), then see the tool-specific guidance:

### How do I bring my own storage, Azure Cosmos DB, or Azure AI Search for agent data?

Use capability hosts and connect your own resources.

- Concepts:
[Capability hosts](concepts/capability-hosts?view=foundry-classic) - How-to:
[Use your own resources](how-to/use-your-own-resources?view=foundry-classic)

## Monitoring and operations

### How do I monitor Foundry Agent Service?

To understand usage and monitoring options, see [Metrics](how-to/metrics?view=foundry-classic) and [Monitor the service](reference/monitor-service?view=foundry-classic).

### What should I do for business continuity and disaster recovery (BCDR)?

Agent Service BCDR guidance depends on your setup and the resources you provision. For the current guidance, see [BCDR for agents](overview?view=foundry-classic#bcdr-for-agents).

## Virtual networking

### What is virtual network isolation?

Virtual networks help secure inbound and outbound access to your Azure resources. You achieve network isolation through virtual network integrations in Azure.

For Agent Service private networking requirements and limitations, see [How to use a virtual network with Foundry Agent Service](how-to/virtual-networks?view=foundry-classic).

### Why do I need subnet delegation?

Agent Service networking uses Azure Container Apps. When you deploy into your virtual network, you must use a dedicated subnet delegated to `Microsoft.App/environments`

.

For details, see [How to use a virtual network with Foundry Agent Service](how-to/virtual-networks?view=foundry-classic) and [Virtual network configuration](/en-us/azure/container-apps/custom-virtual-networks?tabs=workload-profiles-env#subnet).

### What regions are supported for Class A?

Region availability and limitations can change. For the current requirements and limitations, see [How to use a virtual network with Foundry Agent Service](how-to/virtual-networks?view=foundry-classic).

### What class range is supported for public or private Class A, B, and C subnets?

Only private Class A, B, and C ranges are supported. No public class ranges are supported.

### What is the minimum size for the agent subnet, and how many IPs should I use?

The recommended delegated agent subnet size is /24. The minimum is /27.

For sizing guidance and how IPs are consumed, see [How to use a virtual network with Foundry Agent Service](how-to/virtual-networks?view=foundry-classic) and [Virtual network configuration](/en-us/azure/container-apps/custom-virtual-networks?tabs=workload-profiles-env#subnet).

### What is the minimum and recommended address range for virtual networks in Foundry Agent Service?

As long as the agent subnet and private endpoints have address space, the address range for virtual networks can be anything.

### Can I use peered virtual networks? Can I have resources in different virtual networks?

Yes. The virtual network is in your subscription, and you should be able to peer with any virtual network. But data transfer is costly, so we don't recommend it. The requirement is that all resources must be in the same region as the Microsoft Foundry resource.

### Do I need to add any FQDNs to an allow list if I'm using an Azure firewall?

Yes. Allow the required fully qualified domain names (FQDNs) for managed identity as described in [Use Azure Firewall with Azure Container Apps](/en-us/azure/container-apps/use-azure-firewall), or allow the `AzureActiveDirectory`

service tag.

For Agent Service private networking guidance, see [How to use a virtual network with Foundry Agent Service](how-to/virtual-networks?view=foundry-classic).

### Can multiple Microsoft Foundry resources reuse the virtual network?

Yes, multiple Microsoft Foundry resources can reuse a virtual network. But the agent runtime subnet is per Microsoft Foundry account.

### Does the virtual network need to be in the same resource group as Foundry?

They don't need to be in the same resource group, but they do need to be in the same region.

### What additional configuration do I need if I want to add tools to my agents?

If you're using a network-secured setup, some tools require additional configuration, such as private endpoints and resource connections.

For the current guidance and limitations, see [How to use a virtual network with Foundry Agent Service](how-to/virtual-networks?view=foundry-classic).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/overview -->

# What is Foundry Agent Service?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Most businesses don't want just chatbots. They want automation that's faster and has fewer errors. That desire might mean summarizing documents, processing invoices, managing support tickets, or publishing blog posts. In all cases, the goal is the same: freeing people and resources to focus on higher-value work by offloading repetitive and predictable tasks.

Large language models (LLMs) introduce a new type of automation with systems that can understand unstructured data, make decisions, and generate content. In practice, businesses can have difficulty moving beyond demos and into production. LLMs can drift, be incorrect, and lack accountability. Without visibility, policy enforcement, and orchestration, these models are hard to trust in real business workflows.

*Microsoft Foundry* is designed to change that. It's a platform that combines models, tools, frameworks, and governance into a unified system for building intelligent agents. At the center of this system is *Foundry Agent Service*, which enables the operation of agents across development, deployment, and production.

Agent Service connects the core pieces of Foundry, such as models, tools, and frameworks, into a single runtime. It manages conversations, orchestrates tool calls, enforces content safety, and integrates with identity, networking, and observability systems. These capabilities help you build agents that are secure, scalable, and production ready.

By abstracting away infrastructure complexity and enforcing trust and safety by design, Agent Service can help you move from prototype to production with confidence.

## Prerequisites

- An Azure subscription with permission to create and manage Foundry resources.
- A Foundry project. If you haven't created one yet, start with
[environment setup](environment-setup?view=foundry-classic). - A deployed model that your agent can use. Model and region availability can vary; see
[models that inform agents](concepts/model-region-support?view=foundry-classic).

## Availability, regions, and limits

Agent Service capabilities can vary based on the Foundry experience you're using and the model and region you choose.

- For service limits, quotas, and throttling considerations, see
[Quotas and limits for Agent Service](quotas-limits?view=foundry-classic). - For model and region support, see
[models that inform agents](concepts/model-region-support?view=foundry-classic).

If you're building your first agent, start with the quickstart links in [Get started with Foundry Agent Service](#get-started-with-foundry-agent-service) to make sure you're on the right API path for your Foundry experience.

## What is an AI agent?

Agents make decisions, invoke tools, and participate in workflows. They perform these tasks sometimes independently and sometimes in collaboration with other agents or humans. They're foundational to real process automation.

Agents you create through Foundry aren't monoliths. They're composable units. Each agent has a specific role, is powered by the right model, and is equipped with the right tools. You deploy each agent within a secure, observable, and governable runtime.

An agent has three core components:

**Model (LLM)**: Powers reasoning and language understanding.**Instructions**: Define the agent's goals, behavior, and constraints. They can have the following types:- Declarative:
- Prompt based: A declaratively defined single agent that combines model configuration, instruction, tools, and natural language prompts to drive behavior.
- Workflow: An agentic workflow that can be expressed as a YAML or other code to orchestrate multiple agents together, or to trigger an action on certain criteria.

- Hosted: Containerized agents that are created and deployed in code and are hosted by Foundry.

- Declarative:
**Tools**: Let the agent retrieve knowledge or take action.

Agents receive unstructured inputs such as user prompts, alerts, or messages from other agents. They produce outputs in the form of tool results or messages. Along the way, they might call tools to perform retrieval or trigger actions.

## How do agents in Foundry work?

Think of Foundry as an assembly line for intelligent agents. Like any modern factory, Foundry brings together specialized stations that are each responsible for shaping part of the final product. Instead of machines and conveyor belts, the agent factory uses models, tools, policies, and orchestration to build agents that are secure, testable, and production ready. Here's how the factory works step by step:

### 1. Models

The assembly line starts when you select a model that gives your agent its intelligence. Choose from a growing catalog of large language models (LLMs), including GPT-4o, GPT-4, GPT-3.5 (Azure OpenAI), and others like Llama. The model is the reasoning core of the agent that informs its decisions.

### 2. Customizability

Shape the model to fit your use case. Customize your agent with fine-tuning, distillation, or domain-specific prompts. Encode agent behavior, role-specific knowledge, and patterns from prior performance by using data captured from real conversation content and tool results.

### 3. Knowledge and tools

Equip your agent with tools. These tools let the agent access enterprise knowledge (such as Bing, SharePoint, and Azure AI Search) and take real-world actions (via Azure Logic Apps, Azure Functions, OpenAPI, and more). This step enhances the agent's ability to expand its capabilities.

### 4. Orchestration

The agent needs coordination. [Connected agents](how-to/connected-agents?view=foundry-classic) orchestrate the full lifecycle, such as handling tool calls, updating conversation state, managing retries, and logging outputs.

The agent needs coordination. [Workflows](concepts/workflow?view=foundry-classic) orchestrate the full lifecycle, such as handling tool calls, updating conversation state, managing retries, and logging outputs.

### 5. Observability

Test and monitor agents. Foundry can capture logs, traces, and evaluations at every step. With full conversation-level visibility and Application Insights integration, teams can inspect every decision and continuously improve agents over time.

### 6. Trust

Ensure that agents are suitable and reliable for the workload they're assigned to. Foundry applies enterprise-grade trust features, including identity via Microsoft Entra, role-based access control (RBAC), content filters, encryption, and network isolation. You choose how and where your agents run, by using platform-managed or bring-your-own infrastructure.

The result is an agent that's ready for production: reliable, extensible, and safe to deploy across your workflows.

## Why use Foundry Agent Service?

Agent Service provides a production-ready foundation for deploying intelligent agents in enterprise environments. Here's how it compares across key capabilities:

| Capability | Agent Service |
|---|---|
Visibility into conversations |
Full access to structured
|

**Multiple-agent coordination****Tool orchestration****Trust and safety**[content filters](../openai/how-to/content-filters?view=foundry-classic)to help prevent misuse and mitigate prompt injection risks, including cross-prompt injection attacks (XPIA). All outputs are policy governed.**Enterprise integration**[storage](how-to/use-your-own-resources?view=foundry-classic#use-an-existing-azure-cosmos-db-for-nosql-account-for-conversation-storage),[Azure AI Search index](how-to/use-your-own-resources?view=foundry-classic#use-an-existing-azure-ai-search-resource), and[virtual network](how-to/virtual-networks?view=foundry-classic)to meet compliance needs.**Observability and debugging**[Full traceability](../how-to/develop/trace-agents-sdk?view=foundry-classic)of conversations, tool invocations, and message traces;[Application Insights integration](how-to/metrics?view=foundry-classic)for usage data.**Identity and policy control**## Security, privacy, and compliance

Agent Service is designed for enterprise workloads where you need strong controls over identity, networking, data handling, and safety.

**Safety controls**: Use integrated[content filters](../openai/how-to/content-filters?view=foundry-classic)to help reduce unsafe outputs and mitigate prompt injection risks, including cross-prompt injection attacks (XPIA).**Network isolation and data residency controls**: Use[virtual networks](how-to/virtual-networks?view=foundry-classic)and bring-your-own resources to meet your requirements.**Bring your own resources**: Use your own Azure resources (for example, storage, Azure AI Search, and Azure Cosmos DB for conversation state) to meet compliance and operational needs. See[Use your own resources](how-to/use-your-own-resources?view=foundry-classic).**Responsible AI guidance**: For a broader set of recommendations and governance resources, see[Responsible AI for Microsoft Foundry](../responsible-use-of-ai-overview?view=foundry-classic).

## Get started with Foundry Agent Service

To get started with Agent Service, create a Foundry project in your Azure subscription.

If you're building in code, see [Microsoft Foundry SDKs](../how-to/develop/sdk-overview?view=foundry-classic) for SDK options and guidance.

If it's your first time using the service, start with the [environment setup](environment-setup?view=foundry-classic) and [quickstart](quickstart?view=foundry-classic) guides.

If it's your first time using the service, start with the [environment setup](environment-setup?view=foundry-classic) and [quickstart](../tutorials/quickstart-create-foundry-resources?view=foundry-classic) guides.

Create a project with the required resources. After you create a project, deploy a compatible model such as GPT-4o. When you have a deployed model, you can start making API calls to Agent Service by using the SDKs.

You can find a list of official samples with the new Python agent SDK on [GitHub](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/ai/azure-ai-projects).

## BCDR for agents

To support service resilience, Agent Service relies on customer-provisioned Azure Cosmos DB accounts for business continuity and disaster recovery (BCDR). This approach helps ensure that your agent state can be preserved and recovered in the event of a regional outage.

As an Azure Standard customer, you provision and manage your own single-tenant Azure Cosmos DB account. You store all agent state in this account. You control backup and recovery through native capabilities in Azure Cosmos DB.

If the primary region becomes unavailable, the agent automatically connects to the same Azure Cosmos DB account in the secondary region. Because Cosmos DB preserves all history, the agent can continue operation with minimal disruption.

Provision and maintain your Azure Cosmos DB account, and configure appropriate backup and recovery policies. This effort helps ensure seamless continuity if the primary region becomes unavailable.

For configuration guidance, see [Use your own resources](how-to/use-your-own-resources?view=foundry-classic) and [virtual networks](how-to/virtual-networks?view=foundry-classic).

## Costs

Using Agent Service can incur costs from the model you deploy and the Azure resources you use for your project (for example, logging and any customer-managed resources you connect).

To understand and manage cost drivers, see [Plan and manage costs](../concepts/manage-costs?view=foundry-classic).

## Troubleshooting

If you're blocked getting started, check these common issues:

**Model isn't available in your region**: See[models that inform agents](concepts/model-region-support?view=foundry-classic).**Requests are throttled or fail due to quota**: See[Quotas and limits for Agent Service](quotas-limits?view=foundry-classic).**You can't access resources or deployments**: Confirm your role assignments and follow[environment setup](environment-setup?view=foundry-classic).**You need to debug tool calls or agent behavior**: Start with[trace agents with the SDK](../how-to/develop/trace-agents-sdk?view=foundry-classic)and[metrics](how-to/metrics?view=foundry-classic).

## Related content

- Learn more about the
[models that inform agents](concepts/model-region-support?view=foundry-classic). - Learn about the
[Microsoft Foundry SDKs](../how-to/develop/sdk-overview?view=foundry-classic).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/quickstart -->

# Quickstart: Create a new agent

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Note

This quickstart is for the previous version of agents. See the [ quickstart for Microsoft Foundry](../quickstarts/get-started-code?view=foundry&preserve-view=true) to use the new version of the API.

Foundry Agent Service allows you to create AI agents tailored to your needs through custom instructions and augmented by advanced tools like code interpreter, and custom functions.

## Prerequisites

- An Azure subscription -
[Create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - Ensure that the individual creating the account and project has the
**Azure AI Account Owner**role at the subscription scope, which will grant the necessary permissions for creating the project- Alternatively, having the
**Contributor**or**Owner**role at the subscription level will allow the creation of the project

- Alternatively, having the
- Once the project is created, ensure that the individual creating the agent within the project has the
**Azure AI User**role at the project level

Important

The Microsoft Foundry portal only supports basic agent setup at this time. If you want to perform a standard agent setup, see the [Environment setup](environment-setup?view=foundry-classic) article to learn about more.

## Create a Foundry account and project in Foundry portal

To create an account and project in Foundry, follow these steps:

Go to Foundry. If you are in a project, select Foundry at the top left of the page to go to the Home page.

Use the Agent getting started creation flow for the fastest experience. Click

**Create an agent**.Enter a name for the project. If you want to customize the default values, select

**Advanced options**.Select

**Create**.Wait for your resources to be provisioned.

- An account and project (child resource of your account) will be created.
- The gpt-4o model will automatically be deployed
- A default agent will be created

Once complete, you will land directly in the agent playground and you can start creating agents. You can give your agent instructions on what to do and how to do it. For example:

*"You are a helpful agent that can answer questions about geography."*Then you can start chatting with your agent.Note

If you are getting permission error when trying to configure or create agents ensure you have the

**Azure AI User**on the project.

| [Reference documentation](/en-us/dotnet/api/overview/azure/ai.agents.persistent-readme) | [Samples](https://github.com/azure-ai-foundry/foundry-samples/tree/main/samples-classic/csharp/getting-started-agents) | [Library source code](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/ai/Azure.AI.Agents.Persistent) | [Package (NuGet)](https://www.nuget.org/packages/Azure.AI.Agents.Persistent) |

## Prerequisites

[A set up agent environment](environment-setup?view=foundry-classic)- Assign the
**Azure AI User**[RBAC role](../concepts/rbac-foundry?view=foundry-classic)to each team member who needs to create or edit agents using the SDK or Agent Playground- This role must be assigned at the project scope
- Minimum required permissions:
**agents/*/read**,**agents/*/action**,**agents/*/delete**


## Configure and run an agent

Create a .NET Console project.

```
dotnet new console
```


Install the .NET package to your project. For example if you're using the .NET CLI, run the following command.

```
dotnet add package Azure.AI.Agents.Persistent
dotnet add package Azure.Identity
```


Next, to authenticate your API requests and run the program, use the [az login](/en-us/cli/azure/authenticate-azure-cli-interactively) command to sign into your Azure subscription.

```
az login
```


Use the following code to create and run an agent. To run this code, you will need to get the endpoint for your project. This string is in the format:

`https://<AIFoundryResourceName>.services.ai.azure.com/api/projects/<ProjectName>`


Important

Starting in May 2025, the Azure AI Agent Service uses an endpoint for [Foundry projects](../what-is-foundry?view=foundry-classic#types-of-projects) instead of the connection string that was previously used for hub-based projects. If you're using a hub-based project, you won't be able to use the current versions of the SDK and REST API. For more information, see [SDK usage with hub-based projects](how-to/use-your-own-resources?view=foundry-classic#sdk-usage-with-hub-based-projects).

You can find your endpoint in the **overview** for your project in the [Microsoft Foundry portal](https://ai.azure.com/?cid=learnDocs), under **Libraries** > **Foundry**.

Set this endpoint in an environment variable named `ProjectEndpoint`

.

You also need your model's deployment name. You can find it in **Models + Endpoints** in the left navigation menu.

Save the name of your model deployment name as an environment variable named `ModelDeploymentName`

.

```
using Azure;
using Azure.AI.Agents.Persistent;
using Azure.Identity;
using System.Diagnostics;
var projectEndpoint = System.Environment.GetEnvironmentVariable("ProjectEndpoint");
var modelDeploymentName = System.Environment.GetEnvironmentVariable("ModelDeploymentName");
//Create a PersistentAgentsClient and PersistentAgent.
PersistentAgentsClient client = new(projectEndpoint, new DefaultAzureCredential());
//Give PersistentAgent a tool to execute code using CodeInterpreterToolDefinition.
PersistentAgent agent = client.Administration.CreateAgent(
model: modelDeploymentName,
name: "My Test Agent",
instructions: "You politely help with math questions. Use the code interpreter tool when asked to visualize numbers.",
tools: [new CodeInterpreterToolDefinition()]
);
//Create a thread to establish a session between Agent and a User.
PersistentAgentThread thread = client.Threads.CreateThread();
//Ask a question of the Agent.
client.Messages.CreateMessage(
thread.Id,
MessageRole.User,
"Hi, Agent! Draw a graph for a line with a slope of 4 and y-intercept of 9.");
//Have Agent begin processing user's question with some additional instructions associated with the ThreadRun.
ThreadRun run = client.Runs.CreateRun(
thread.Id,
agent.Id,
additionalInstructions: "Please address the user as Jane Doe. The user has a premium account.");
//Poll for completion.
do
{
Thread.Sleep(TimeSpan.FromMilliseconds(500));
run = client.Runs.GetRun(thread.Id, run.Id);
}
while (run.Status == RunStatus.Queued
|| run.Status == RunStatus.InProgress
|| run.Status == RunStatus.RequiresAction);
//Get the messages in the PersistentAgentThread. Includes Agent (Assistant Role) and User (User Role) messages.
Pageable<PersistentThreadMessage> messages = client.Messages.GetMessages(
threadId: thread.Id,
order: ListSortOrder.Ascending);
//Display each message and open the image generated using CodeInterpreterToolDefinition.
foreach (PersistentThreadMessage threadMessage in messages)
{
foreach (MessageContent content in threadMessage.ContentItems)
{
switch (content)
{
case MessageTextContent textItem:
Console.WriteLine($"[{threadMessage.Role}]: {textItem.Text}");
break;
case MessageImageFileContent imageFileContent:
Console.WriteLine($"[{threadMessage.Role}]: Image content file ID = {imageFileContent.FileId}");
BinaryData imageContent = client.Files.GetFileContent(imageFileContent.FileId);
string tempFilePath = Path.Combine(AppContext.BaseDirectory, $"{Guid.NewGuid()}.png");
File.WriteAllBytes(tempFilePath, imageContent.ToArray());
client.Files.DeleteFile(imageFileContent.FileId);
ProcessStartInfo psi = new()
{
FileName = tempFilePath,
UseShellExecute = true
};
Process.Start(psi);
break;
}
}
}
//If you want to delete your agent, uncomment the following lines:
//client.Threads.DeleteThread(threadId: thread.Id);
//client.Administration.DeleteAgent(agentId: agent.Id);
```


| [Reference documentation](https://aka.ms/azsdk/azure-ai-projects/python/reference) | [Samples](https://aka.ms/azsdk/azure-ai-projects/python/samples/) | [Library source code](https://aka.ms/azsdk/azure-ai-projects/python/code) | [Package (PyPi)](https://aka.ms/azsdk/azure-ai-projects/python/package) |

## Prerequisites

[A set up agent environment](environment-setup?view=foundry-classic)- Assign the
**Azure AI User**[RBAC role](../concepts/rbac-foundry?view=foundry-classic)to each team member who needs to create or edit agents using the SDK or Agent Playground- This role must be assigned at the project scope
- Minimum required permissions:
**agents/*/read**,**agents/*/action**,**agents/*/delete**


## Configure and run an agent

Run the following commands to install the python packages.

```
pip install azure-ai-projects
pip install azure-identity
```


Next, to authenticate your API requests and run the program, use the [az login](/en-us/cli/azure/authenticate-azure-cli-interactively) command to sign into your Azure subscription.

```
az login
```


Use the following code to create and run an agent. To run this code, you will need to get the endpoint for your project. This string is in the format:

`https://<AIFoundryResourceName>.services.ai.azure.com/api/projects/<ProjectName>`


Important

Starting in May 2025, the Azure AI Agent Service uses an endpoint for [Foundry projects](../what-is-foundry?view=foundry-classic#types-of-projects) instead of the connection string that was previously used for hub-based projects. If you're using a hub-based project, you won't be able to use the current versions of the SDK and REST API. For more information, see [SDK usage with hub-based projects](how-to/use-your-own-resources?view=foundry-classic#sdk-usage-with-hub-based-projects).

You can find your endpoint in the **overview** for your project in the [Microsoft Foundry portal](https://ai.azure.com/?cid=learnDocs), under **Libraries** > **Foundry**.

Set this endpoint as an environment variable named `PROJECT_ENDPOINT`

.

You also need your model's deployment name. You can find it in **Models + Endpoints** in the left navigation menu.

Save the name of your model deployment name as an environment variable named `MODEL_DEPLOYMENT_NAME`

.

```
import os
from pathlib import Path
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential
from azure.ai.agents.models import CodeInterpreterTool
# Create an AIProjectClient instance
project_client = AIProjectClient(
endpoint=os.getenv("PROJECT_ENDPOINT"),
credential=DefaultAzureCredential(),
# Use Azure Default Credential for authentication
)
with project_client:
code_interpreter = CodeInterpreterTool()
agent = project_client.agents.create_agent(
model=os.getenv("MODEL_DEPLOYMENT_NAME"), # Model deployment name
name="my-agent", # Name of the agent
instructions="""You politely help with math questions.
Use the Code Interpreter tool when asked to visualize numbers.""",
# Instructions for the agent
tools=code_interpreter.definitions, # Attach the tool
tool_resources=code_interpreter.resources, # Attach tool resources
)
print(f"Created agent, ID: {agent.id}")
# Create a thread for communication
thread = project_client.agents.threads.create()
print(f"Created thread, ID: {thread.id}")
question = """Draw a graph for a line with a slope of 4
and y-intercept of 9 and provide the file to me?"""
# Add a message to the thread
message = project_client.agents.messages.create(
thread_id=thread.id,
role="user", # Role of the message sender
content=question, # Message content
)
print(f"Created message, ID: {message['id']}")
# Create and process an agent run
run = project_client.agents.runs.create_and_process(
thread_id=thread.id,
agent_id=agent.id,
additional_instructions="""Please address the user as Jane Doe.
The user has a premium account.""",
)
print(f"Run finished with status: {run.status}")
# Check if the run failed
if run.status == "failed":
print(f"Run failed: {run.last_error}")
# Fetch and log all messages
messages = project_client.agents.messages.list(thread_id=thread.id)
print(f"Messages: {messages}")
for message in messages:
print(f"Role: {message.role}, Content: {message.content}")
for this_content in message.content:
print(f"Content Type: {this_content.type}, Content Data: {this_content}")
if this_content.text.annotations:
for annotation in this_content.text.annotations:
print(f"Annotation Type: {annotation.type}, Text: {annotation.text}")
print(f"Start Index: {annotation.start_index}")
print(f"End Index: {annotation.end_index}")
print(f"File ID: {annotation.file_path.file_id}")
# Save every image file in the message
file_id = annotation.file_path.file_id
file_name = f"{file_id}_image_file.png"
project_client.agents.files.save(file_id=file_id, file_name=file_name)
print(f"Saved image file to: {Path.cwd() / file_name}")
#Uncomment these lines to delete the agent when done
#project_client.agents.delete_agent(agent.id)
#print("Deleted agent")
```


| [Reference documentation](/en-us/javascript/api/overview/azure/ai-projects-readme) | [Samples](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/ai/ai-projects/README.md) | [Library source code](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/ai/ai-projects) | [Package (npm)](https://www.npmjs.com/package/@azure/ai-projects) |

## Prerequisites

[A set up agent environment](environment-setup?view=foundry-classic)- Assign the
**Azure AI User**[RBAC role](../concepts/rbac-foundry?view=foundry-classic)to each team member who needs to create or edit agents using the SDK or Agent Playground- This role must be assigned at the project scope
- Minimum required permissions:
**agents/*/read**,**agents/*/action**,**agents/*/delete**


## Configure and run an agent

Key objects in this code include:

First, initialize a new TypeScript project by running:

```
npm init -y
npm pkg set type="module"
```


Run the following commands to install the npm packages required.

```
npm install @azure/ai-agents @azure/identity
npm install @types/node typescript --save-dev
```


Next, to authenticate your API requests and run the program, use the [az login](/en-us/cli/azure/authenticate-azure-cli-interactively) command to sign into your Azure subscription.

```
az login
```


Use the following code to answer the math question `I need to solve the equation '3x + 11 = 14'. Can you help me?`

. To run this code, you'll need to get the endpoint for your project. This string is in the format:

`https://<AIFoundryResourceName>.services.ai.azure.com/api/projects/<ProjectName>`


You can find your endpoint in the **overview** for your project in the [Microsoft Foundry portal](https://ai.azure.com/?cid=learnDocs), under **Libraries** > **Foundry**.

Set this endpoint as an environment variable named `PROJECT_ENDPOINT`

in a `.env`

file.

You also need your model's deployment name. You can find it in **Models + Endpoints** in the left navigation menu.

Save the name of your model deployment name as an environment variable named `MODEL_DEPLOYMENT_NAME`

.

Important

- This quickstart code uses environment variables for sensitive configuration. Never commit your
`.env`

file to version control by making sure`.env`

is listed in your`.gitignore`

file. *Remember: If you accidentally commit sensitive information, consider those credentials compromised and rotate them immediately.*

Create a tsconfig.json file with the following content:

```
{
"compilerOptions": {
"module": "nodenext",
"target": "esnext",
"types": ["node"],
"lib": ["esnext"],
"sourceMap": true,
"declaration": true,
"declarationMap": true,
"noUncheckedIndexedAccess": true,
"exactOptionalPropertyTypes": true,
"strict": true,
"verbatimModuleSyntax": true,
"isolatedModules": true,
"noUncheckedSideEffectImports": true,
"moduleDetection": "force",
"skipLibCheck": true,
}
}
```


Next, create an `index.ts`

file and paste in the following code:

```
import { AgentsClient } from "@azure/ai-agents";
import { DefaultAzureCredential } from "@azure/identity";
const projectEndpoint = process.env["PROJECT_ENDPOINT"] || "<project endpoint>";
const modelDeploymentName = process.env["MODEL_DEPLOYMENT_NAME"] || "gpt-4o";
export async function main(): Promise<void> {
// Create an Azure AI Client
const client = new AgentsClient(projectEndpoint, new DefaultAzureCredential());
// Create an agent
const agent = await client.createAgent(modelDeploymentName, {
name: "my-agent",
instructions: "You are a helpful agent specialized in math. When providing mathematical explanations, use plain text formatting with simple characters like +, -, *, / for operations. Do not use LaTeX formatting with backslashes or special notation. Make your explanations clear and easy to read in a terminal.",
});
console.log(`Created agent, agent ID : ${agent.id}`);
// Create a thread
const thread = await client.threads.create();
console.log(`Created thread, thread ID : ${thread.id}`);
// List all threads for the agent
const threads = client.threads.list();
console.log(`Threads for agent ${agent.id}:`);
for await (const t of threads) {
console.log(`Thread ID: ${t.id} created at: ${t.createdAt}`);
}
// Create a message
const message = await client.messages.create(thread.id, "user", "I need to solve the equation `3x + 11 = 14`. Can you help me?");
console.log(`Created message, message ID : ${message.id}`);
// Create and poll a run
console.log("Creating run...");
const run = await client.runs.createAndPoll(thread.id, agent.id, {
pollingOptions: {
intervalInMs: 2000,
},
onResponse: (response): void => {
const parsedBody =
typeof response.parsedBody === "object" && response.parsedBody !== null
? response.parsedBody
: null;
const status = parsedBody && "status" in parsedBody ? parsedBody.status : "unknown";
console.log(`Received response with status: ${status}`);
},
});
console.log(`Run finished with status: ${run.status}`);
const messagesIterator = client.messages.list(thread.id);
console.log("\n\n========================================================");
console.log("=================== CONVERSATION RESULTS ===================");
console.log("========================================================\n");
// Collect all messages first
const messages = [];
for await (const m of messagesIterator) {
messages.push(m);
}
// Reverse the order of messages (or sort by timestamp if available)
messages.reverse();
// Display messages in the new order
for (const m of messages) {
if (m.role === "user") {
console.log(`\n❓ USER QUESTION: ${
Array.isArray(m.content) && m.content[0]?.type === "text" && 'text' in m.content[0]
? m.content[0].text.value
: JSON.stringify(m.content)
}`);
} else if (m.role === "assistant") {
console.log("\n🤖 ASSISTANT'S ANSWER:");
console.log("--------------------------------------------------");
// Extract and print the text content in a more readable format
if (m.content && Array.isArray(m.content)) {
for (const content of m.content) {
if (content.type === "text" && 'text' in content) {
console.log(content.text?.value);
} else {
console.log(content);
}
}
} else {
console.log(JSON.stringify(m.content, null, 2));
}
console.log("--------------------------------------------------\n");
}
}
console.log("\n========================================================");
console.log("====================== END OF RESULTS ======================");
console.log("========================================================\n");
// Clean up
await client.threads.delete(thread.id);
await client.deleteAgent(agent.id);
}
main().catch((err) => {
console.error("The sample encountered an error:", err);
});
```


Run the code using `npx tsx -r dotenv/config index.ts`

. This code answers the question `I need to solve the equation '3x + 11 = 14'. Can you help me?`

. Responses aren't deterministic, your output will look similar to the below output:

```
Created agent, agent ID : asst_X4yDNWrdWKb8LN0SQ6xlzhWk
Created thread, thread ID : thread_TxqZcHL2BqkNWl9dFzBYMIU6
Threads for agent asst_X4yDNWrdWKb8LN0SQ6xlzhWk:
...
Created message, message ID : msg_R0zDsXdc2UbfsNXvS1zeS6hk
Creating run...
Received response with status: queued
Received response with status: in_progress
Received response with status: completed
Run finished with status: completed
========================================================
=================== CONVERSATION RESULTS ===================
========================================================
❓ USER QUESTION: I need to solve the equation `3x + 11 = 14`. Can you help me?
🤖 ASSISTANT'S ANSWER:
--------------------------------------------------
Certainly! Let's solve the equation step by step:
We have:
3x + 11 = 14
### Step 1: Eliminate the constant (+11) on the left-hand side.
Subtract 11 from both sides:
3x + 11 - 11 = 14 - 11
This simplifies to:
3x = 3
We have:
3x + 11 = 14
### Step 1: Eliminate the constant (+11) on the left-hand side.
Subtract 11 from both sides:
3x + 11 - 11 = 14 - 11
This simplifies to:
3x = 3
### Step 2: Solve for x.
Divide both sides by 3:
3x / 3 = 3 / 3
This simplifies to:
x = 1
### Final Answer:
x = 1
--------------------------------------------------
========================================================
====================== END OF RESULTS ======================
========================================================
```


Full [sample source code](https://github.com/Azure-Samples/azure-sdk-for-js-docs/blob/main/samples/foundry/azure-ai-agents-quickstart-math) available.

| [Reference documentation](/en-us/java/api/overview/azure/ai-agents-persistent-readme) | [Samples](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/ai/azure-ai-agents-persistent/src/samples/java/com/azure/ai/agents/persistent) | [Library source code](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/ai/azure-ai-agents-persistent) | [Package (Maven)](https://central.sonatype.com/artifact/com.azure/azure-ai-agents-persistent) |

## Prerequisites

[A set up agent environment](environment-setup?view=foundry-classic)- Assign the
**Azure AI User**[RBAC role](../concepts/rbac-foundry?view=foundry-classic)to each team member who needs to create or edit agents using the SDK or Agent Playground- This role must be assigned at the project scope
- Minimum required permissions:
**agents/*/read**,**agents/*/action**,**agents/*/delete**


## Configure and run an agent

First, create a New Java console project. You'll need the following dependencies to run the code:

```
<dependencies>
<dependency>
<groupId>com.azure</groupId>
<artifactId>azure-ai-agents-persistent</artifactId>
<version>1.0.0-beta.2</version>
</dependency>
<dependency>
<groupId>com.azure</groupId>
<artifactId>azure-identity</artifactId>
<version>1.17.0-beta.1</version>
</dependency>
</dependencies>
```


Next, to authenticate your API requests and run the program, use the [az login](/en-us/cli/azure/authenticate-azure-cli-interactively) command to sign into your Azure subscription.

```
az login
```


Use the following code to create and run an agent. To run this code, you'll need to get the endpoint for your project. This string is in the format:

`https://<AIFoundryResourceName>.services.ai.azure.com/api/projects/<ProjectName>`


Important

Starting in May 2025, the Azure AI Agent Service uses an endpoint for [Foundry projects](../what-is-foundry?view=foundry-classic#types-of-projects) instead of the connection string that was previously used for hub-based projects. If you're using a hub-based project, you won't be able to use the current versions of the SDK and REST API. For more information, see [SDK usage with hub-based projects](how-to/use-your-own-resources?view=foundry-classic#sdk-usage-with-hub-based-projects).

You can find your endpoint in the **overview** for your project in the [Microsoft Foundry portal](https://ai.azure.com/?cid=learnDocs), under **Libraries** > **Foundry**.

Set this endpoint in an environment variable named `PROJECT_ENDPOINT`

.

You also need your model's deployment name. You can find it in **Models + Endpoints** in the left navigation menu.

Save the name of your model deployment name as an environment variable named `MODEL_DEPLOYMENT_NAME`

.

## Code example

```
package com.example.agents;
import com.azure.ai.agents.persistent.MessagesClient;
import com.azure.ai.agents.persistent.PersistentAgentsAdministrationClient;
import com.azure.ai.agents.persistent.PersistentAgentsClient;
import com.azure.ai.agents.persistent.PersistentAgentsClientBuilder;
import com.azure.ai.agents.persistent.RunsClient;
import com.azure.ai.agents.persistent.ThreadsClient;
import com.azure.ai.agents.persistent.models.CodeInterpreterToolDefinition;
import com.azure.ai.agents.persistent.models.CreateAgentOptions;
import com.azure.ai.agents.persistent.models.CreateRunOptions;
import com.azure.ai.agents.persistent.models.MessageImageFileContent;
import com.azure.ai.agents.persistent.models.MessageRole;
import com.azure.ai.agents.persistent.models.MessageTextContent;
import com.azure.ai.agents.persistent.models.PersistentAgent;
import com.azure.ai.agents.persistent.models.PersistentAgentThread;
import com.azure.ai.agents.persistent.models.RunStatus;
import com.azure.ai.agents.persistent.models.ThreadMessage;
import com.azure.ai.agents.persistent.models.ThreadRun;
import com.azure.ai.agents.persistent.models.MessageContent;
import com.azure.core.http.rest.PagedIterable;
import com.azure.identity.DefaultAzureCredentialBuilder;
import java.util.Arrays;
public class AgentSample {
public static void main(String[] args) {
// variables for authenticating requests to the agent service
String projectEndpoint = System.getenv("PROJECT_ENDPOINT");
String modelName = System.getenv("MODEL_DEPLOYMENT_NAME");
// initialize clients to manage various aspects of agent runtime
PersistentAgentsClientBuilder clientBuilder = new PersistentAgentsClientBuilder()
.endpoint(projectEndpoint)
.credential(new DefaultAzureCredentialBuilder().build());
PersistentAgentsClient agentsClient = clientBuilder.buildClient();
PersistentAgentsAdministrationClient administrationClient = agentsClient.getPersistentAgentsAdministrationClient();
ThreadsClient threadsClient = agentsClient.getThreadsClient();
MessagesClient messagesClient = agentsClient.getMessagesClient();
RunsClient runsClient = agentsClient.getRunsClient();
String agentName = "my-agent"; // the name of the agent
CreateAgentOptions createAgentOptions = new CreateAgentOptions(modelName)
.setName(agentName)
.setInstructions("You are a helpful agent") // system instructions
.setTools(Arrays.asList(new CodeInterpreterToolDefinition()));
PersistentAgent agent = administrationClient.createAgent(createAgentOptions);
PersistentAgentThread thread = threadsClient.createThread();
ThreadMessage createdMessage = messagesClient.createMessage(
thread.getId(),
MessageRole.USER,
"I need to solve the equation `3x + 11 = 14`. Can you help me?"); // The message to the agent
try {
//run the agent
CreateRunOptions createRunOptions = new CreateRunOptions(thread.getId(), agent.getId())
.setAdditionalInstructions("");
ThreadRun threadRun = runsClient.createRun(createRunOptions);
// wait for the run to complete before printing the message
waitForRunCompletion(thread.getId(), threadRun, runsClient);
printRunMessages(messagesClient, thread.getId());
} catch (InterruptedException e) {
throw new RuntimeException(e);
} finally {
//cleanup - uncomment these lines if you want to delete the agent
//threadsClient.deleteThread(thread.getId());
//administrationClient.deleteAgent(agent.getId());
}
}
// A helper function to print messages from the agent
public static void printRunMessages(MessagesClient messagesClient, String threadId) {
PagedIterable<ThreadMessage> runMessages = messagesClient.listMessages(threadId);
for (ThreadMessage message : runMessages) {
System.out.print(String.format("%1$s - %2$s : ", message.getCreatedAt(), message.getRole()));
for (MessageContent contentItem : message.getContent()) {
if (contentItem instanceof MessageTextContent) {
System.out.print((((MessageTextContent) contentItem).getText().getValue()));
} else if (contentItem instanceof MessageImageFileContent) {
String imageFileId = (((MessageImageFileContent) contentItem).getImageFile().getFileId());
System.out.print("Image from ID: " + imageFileId);
}
System.out.println();
}
}
}
// a helper function to wait until a run has completed running
public static void waitForRunCompletion(String threadId, ThreadRun threadRun, RunsClient runsClient)
throws InterruptedException {
do {
Thread.sleep(500);
threadRun = runsClient.getRun(threadId, threadRun.getId());
}
while (
threadRun.getStatus() == RunStatus.QUEUED
|| threadRun.getStatus() == RunStatus.IN_PROGRESS
|| threadRun.getStatus() == RunStatus.REQUIRES_ACTION);
if (threadRun.getStatus() == RunStatus.FAILED) {
System.out.println(threadRun.getLastError().getMessage());
}
}
}
```


## Prerequisites

[A set up agent environment](environment-setup?view=foundry-classic)- Assign the
**Azure AI User**[RBAC role](../concepts/rbac-foundry?view=foundry-classic)to each team member who needs to create or edit agents using the SDK or Agent Playground- This role must be assigned at the project scope
- Minimum required permissions:
**agents/*/read**,**agents/*/action**,**agents/*/delete**


## Configure and run an agent

To authenticate your API requests, use the [az login](/en-us/cli/azure/authenticate-azure-cli-interactively) command to sign into your Azure subscription.

```
az login
```


Next, you'll need to fetch the Entra ID token to provide as authorization to the API calls. Fetch the token using the CLI command:

```
az account get-access-token --resource 'https://ai.azure.com' | jq -r .accessToken | tr -d '"'
```


Set the access token as an environment variable named `AGENT_TOKEN`

.

To successfully make REST API calls to Foundry Agent Service, you will need to use your project's endpoint:

`https://<your_ai_service_name>.services.ai.azure.com/api/projects/<your_project_name>`


For example, your endpoint will look something like:

`https://exampleaiservice.services.ai.azure.com/api/projects/project`


Set this endpoint as an environment variable named `AZURE_AI_FOUNDRY_PROJECT_ENDPOINT`

.

Note

- For
`api-version`

parameter, the GA API version is`2025-05-01`

and the latest preview API version is`2025-05-15-preview`

. You must use the preview API for tools that are in preview. - Consider making your API version an environment variable, such as
`$API_VERSION`

.

### Create an agent

Note

With Azure AI Agents Service the `model`

parameter requires model deployment name. If your model deployment name is different than the underlying model name, then you would adjust your code to ` "model": "{your-custom-model-deployment-name}"`

.

```
curl --request POST \
--url $AZURE_AI_FOUNDRY_PROJECT_ENDPOINT/assistants?api-version=2025-05-01 \
-H "Authorization: Bearer $AGENT_TOKEN" \
-H "Content-Type: application/json" \
-d '{
"instructions": "You are a helpful agent.",
"name": "my-agent",
"tools": [{"type": "code_interpreter"}],
"model": "gpt-4o-mini"
}'
```


### Create a thread

```
curl --request POST \
--url $AZURE_AI_FOUNDRY_PROJECT_ENDPOINT/threads?api-version=2025-05-01 \
-H "Authorization: Bearer $AGENT_TOKEN" \
-H "Content-Type: application/json" \
-d ''
```


### Add a user question to the thread

```
curl --request POST \
--url $AZURE_AI_FOUNDRY_PROJECT_ENDPOINT/threads/thread_abc123/messages?api-version=2025-05-01 \
-H "Authorization: Bearer $AGENT_TOKEN" \
-H "Content-Type: application/json" \
-d '{
"role": "user",
"content": "I need to solve the equation `3x + 11 = 14`. Can you help me?"
}'
```


### Run the thread

```
curl --request POST \
--url $AZURE_AI_FOUNDRY_PROJECT_ENDPOINT/threads/thread_abc123/runs?api-version=2025-05-01 \
-H "Authorization: Bearer $AGENT_TOKEN" \
-H "Content-Type: application/json" \
-d '{
"assistant_id": "asst_abc123",
}'
```


### Retrieve the status of the run

```
curl --request GET \
--url $AZURE_AI_FOUNDRY_PROJECT_ENDPOINT/threads/thread_abc123/runs/run_abc123?api-version=2025-05-01 \
-H "Authorization: Bearer $AGENT_TOKEN"
```


### Retrieve the agent response

```
curl --request GET \
--url $AZURE_AI_FOUNDRY_PROJECT_ENDPOINT/threads/thread_abc123/messages?api-version=2025-05-01 \
-H "Authorization: Bearer $AGENT_TOKEN"
```


## Next steps

Learn about the [ tools](how-to/tools/overview?view=foundry-classic) you can use to extend your agents' capabilities, such as accessing the web, provide grounding information, and more.
