---
merged_at: 2026-02-06T17:00:26.585972
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
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/observability/concepts/trace-agent-concept -->

# Agent tracing overview (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Microsoft Foundry provides an observability platform for monitoring and tracing AI agents. It can capture key details during an agent run, such as inputs, outputs, tool usage, retries, latencies, and costs. Understanding the reasoning behind your agent's executions is important for troubleshooting and debugging. However, it can be difficult for complex agents for many reasons:

- There could be a high number of steps involved in generating a response, making it hard to keep track of all of them.
- The sequence of steps might vary based on user input.
- The inputs/outputs at each stage might be long and deserve more detailed inspection.
- Each step of an agent's runtime might also involve nesting. For example, an agent might invoke a tool, which uses another process, which then invokes another tool. If you notice strange or incorrect output from a top-level agent run, it might be difficult to determine exactly where in the execution the issue was introduced.

Trace results solve this by allowing you to view the inputs and outputs of each primitive involved in a particular agent run, displayed in the order they were invoked, making it easy to understand and debug your AI agent's behavior.

Note

Agent tracing is only available in Sweden Central in Foundry (new).

## Before you begin

To use tracing end-to-end, you need:

- A Foundry project with tracing enabled. To set it up, see
[How to set up tracing in Microsoft Foundry](../how-to/trace-agent-setup?view=foundry). - Access to the Azure Application Insights resource connected to your project. For background, see
[Azure Application Insights](/en-us/azure/azure-monitor/app/app-insights-overview).

## OpenTelemetry in Foundry

OpenTelemetry (OTel) provides standardized protocols for collecting and routing telemetry data. Foundry uses OpenTelemetry semantic conventions so traces are consistent across supported tools and integrations.

## Trace key concepts

Here's a brief overview of key concepts before getting started:

| Key concepts | Description |
|---|---|
| Traces | Traces capture the journey of a request or workflow through your application by recording events and state changes (function calls, values, system events). See
|

[OpenTelemetry's Semantic Conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/).[How to set up tracing in Microsoft Foundry](../how-to/trace-agent-setup?view=foundry).## How tracing works in Foundry

Tracing helps you answer questions like "Where did this response come from?" and "Which step introduced an error or latency spike?"

At a high level, tracing captures:

- User inputs and agent outputs.
- Tool usage, including tool calls and results.
- Timing signals such as latency.

Once tracing is enabled for your project, you can inspect traces in the Foundry portal and in Azure Monitor Application Insights. For the step-by-step setup and viewing options, see [How to set up tracing in Microsoft Foundry](../how-to/trace-agent-setup?view=foundry).

## Extending OpenTelemetry with multi-agent observability

Microsoft, in collaboration with Cisco Outshift, has introduced new semantic conventions for multi-agent systems, built on [OpenTelemetry](https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/) and [W3C Trace Context](https://www.w3.org/TR/trace-context/). These conventions standardize telemetry for multi-agent workflows, enabling consistent logging of metrics for quality, performance, safety, and cost, including tool invocations and collaboration.

These enhancements are integrated into:

- Foundry
- Microsoft Agent Framework
- Semantic Kernel
- LangChain
- LangGraph
- OpenAI Agents SDK

To learn more, see [tracing integrations](../how-to/trace-agent-framework?view=foundry).

| Type | Context/Parent Span | Name/Attribute/Event | Purpose |
|---|---|---|---|
| Span | — | execute_task | Captures task planning and event propagation, providing insights into how tasks are decomposed and distributed. |
| Child Span | invoke_agent | agent_to_agent_interaction | Traces communication between agents. |
| Child Span | invoke_agent | agent.state.management | Effective context, short or long term memory management. |
| Child Span | invoke_agent | agent_planning | Logs the agent's internal planning steps. |
| Child Span | invoke_agent | agent orchestration | Captures agent-to-agent orchestration. |
| Attribute | invoke_agent | tool_definitions | Describes the tool's purpose or configuration. |
| Attribute | invoke_agent | llm_spans | Records model call spans. |
| Attribute | execute_tool | tool.call.arguments | Logs the arguments passed during tool invocation. |
| Attribute | execute_tool | tool.call.results | Records the results returned by the tool. |
| Event | — | Evaluation (name, error.type, label) | Enables structured evaluation of agent performance and decision-making. |

## Best practices

- Use consistent span attributes.
- Correlate evaluation run IDs for quality + performance analysis.
- Redact sensitive content; avoid storing secrets in attributes.

## Security and privacy

Tracing can capture sensitive information (for example, user inputs, model outputs, and tool arguments and results). Use these practices to reduce risk:

- Don't store secrets, credentials, or tokens in prompts, tool arguments, or span attributes.
- Redact or minimize personal data and other sensitive content before it appears in telemetry.
- Treat trace data as production telemetry and apply the same access controls and retention policies you use for logs and metrics.

## Availability and limitations

- Agent tracing is available only in Sweden Central in Foundry (new).
- Some tracing integrations can be language- or framework-specific. For details, see
[Tracing integrations](../how-to/trace-agent-framework?view=foundry).

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

– Build advanced automation using SDKs for C# and Python that enable collaborative agent behavior and complex workflow execution.[Multi-Agent Orchestration and Workflows](agents/concepts/workflow?view=foundry&preserve-view=true)– Publish agents to Microsoft 365, Teams, and BizChat, plus leverage containerized deployments for greater portability.[Expanded Integration Options](agents/how-to/publish-copilot?view=foundry&preserve-view=true)– Access the Foundry tool catalog (preview) with a public tool catalog and your own private catalogs, connecting over 1,400 tools in Microsoft Foundry.[Expanded Tool Access](agents/concepts/tool-catalog?view=foundry&preserve-view=true)– Use memory to help your agent retain and recall contextual information across interactions. Memory maintains continuity, adapts to user needs, and delivers tailored experiences without requiring repeated input.[Enhanced Memory Capabilities](agents/concepts/what-is-memory?view=foundry&preserve-view=true)– Connect your agent to a Foundry IQ (powered by Azure AI Search) knowledge base to ground responses in enterprise or web content. This integration provides reliable, citation-backed answers for multi-turn conversations.[Knowledge Integration](agents/how-to/tools/knowledge-retrieval?view=foundry&preserve-view=true)– Monitor performance and governance using built-in metrics and model tracking tools.[Real-Time Observability](how-to/continuous-evaluation-agents?view=foundry&preserve-view=true)**Enhanced Enterprise Support**– Use open protocols in Foundry Agent Service with full authentication support in MCP and A2A tool, AI gateway integration, and Azure Policy integration.**Centralized AI asset management**- Observe, optimize, and manage 100% of your AI assets (agents, models, tools) in one place, the**Operate**section. Register agents from other clouds, get alerts when an agent or model requires your attention, and effectively manage your AI fleet health as that fleet scales.**Optimized Developer Experience**– Experience faster load times and dynamic prefetching for smooth development and deployment.**Streamlined Navigation**– Navigate efficiently with a redesigned interface that places key controls where you need them, improving workflow efficiency.

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

You can [explore Foundry portal (classic) (including the model catalog)](how-to/model-catalog-overview?view=foundry-classic) without signing in.

But for full functionality, you need an [Azure account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

You need an [Azure account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). Then sign in to [Microsoft Foundry](https://ai.azure.com?cid=learnDocs) and toggle the **Try the new Foundry** on.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/agents/transparency-note -->

# Transparency Note for Azure Agent Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Non-English translations are provided for convenience only. Please consult the [ EN-US version of this document](/en-us/azure/ai-foundry/responsible-ai/openai/customer-copyright-commitment) for the definitive version.

## What is a Transparency Note?

An AI system includes not only the technology, but also the people who will use it, the people who will be affected by it, and the environment in which it is deployed. Creating a system that is fit for its intended purpose requires an understanding of how the technology works, what its capabilities and limitations are, and how to achieve the best performance. Microsoft’s Transparency Notes are intended to help you understand how our AI technology works, the choices system owners can make that influence system performance and behavior, and the importance of thinking about the whole system, including the technology, the people, and the environment. You can use Transparency Notes when developing or deploying your own system or share them with the people who will use or be affected by your system.

Microsoft’s Transparency Notes are part of a broader effort at Microsoft to put our AI Principles into practice. To find out more, see the [Microsoft AI principles](https://www.microsoft.com/ai/responsible-ai).

## The basics of Azure AI Agent Service

### Introduction

Azure AI Agent Service is a fully managed service designed to empower developers to securely build, deploy, and scale high-quality and extensible AI agents without needing to manage the underlying compute and storage resources. Azure AI Agent Service provides integrated access to **models, tools, and technology** and enables you to extend the functionality of agents with knowledge from connected sources (such as Bing Search, SharePoint, Fabric, Azure Blob storage, and licensed data) and with actions using tools such as Azure Logic Apps, Azure Functions, OpenAPI 3.0 specified tools, and Code Interpreter. [Learn more](/en-us/azure/ai-services/agents/overview).

### General Disclaimer about Agents

Agentic AI systems are designed to use agentic capabilities to achieve a high-level goal specified by a user. Systems should be designed to allow users to incorporate human oversight as appropriate to ensure the system is performing the actions and tasks as intended. Should an Agent exhibit unintended or undesirable behaviors, users should have the ability to intervene and take appropriate measures to mitigate potential risks.

### Disclaimer about Agents in sensitive domains

Users should exercise caution when designing and deploying agentic AI systems in sensitive domains where Agent actions are irreversible or highly consequential. Such domains include, but are not limited to, finance and insurance, healthcare, legal, and housing. Additional precautions should also be taken when creating autonomous agentic AI as described further in our [Code of Conduct](https://aka.ms/AI-CoC). You are responsible for complying with all applicable laws and safety standards relevant to the Agents you create using any Foundry Tools and solutions, including Agents Catalog, underlying Code Samples, and similar resources and information (see below [Considerations when choosing a use case](#considerations-when-choosing-a-use-case)).

### Key terms

The following are key components of the Azure AI Agent Service SDK (and the [Microsoft Foundry portal](https://ai.azure.com?cid=learnDocs) experience powered by it):

Term |
Definition |
|---|---|
| Developer | A customer of Azure AI Agent Service who builds an Agent. |
| User | A person who uses and/or operates an Agent that is created by a developer. |
| Agent | An application or a system that uses generative AI models with tools to access and interact with real-world data sources, APIs, and systems to achieve user-specified goals such as answer questions, perform actions, or completely automate workflows, with or without human supervision. |
| Tool | A built-in or custom-defined functionality that enables an Agent to perform simple or complex tasks or interact with information sources, applications, and/or services via the Agent Service SDK or
|

### Relevant capability concepts

Term |
Definition |
|---|---|
| Agentic AI system | An umbrella term that includes the following common capabilities that developers may enable in their Agents when they use the Azure AI Agent Service. |
| Autonomy | The ability to independently execute actions and exercise control over system behavior with varying degrees of human supervision. |
| Reasoning | The ability to process information while understanding context and outcomes of various potential courses of actions, tasks, or engagements with third-party users. |
| Planning | The ability to break down complex, user-specified goals and actions into tasks and subtasks for execution. Planned tasks are created by one or more agents. |
| Memory | The ability to store or retain information or context from previous observations, interactions, or system behaviors. |
| Adaptability | The ability to change or adjust behavior and improve performance based on information gathered from the environment or prior experience. |
| Extensibility | The ability to call resources (for example, such as external knowledge sources) and execute functions (for example, sending an email) from connected systems, software, or platforms, including using tools. |

## Capabilities

### System behavior

Azure AI Agent Service provides integration with securely managed data, out-of-the-box tools and automatic tool calling that enable developers to build Agents that can have the ability to reason, plan, and execute tasks from a high-level goal specified by a user. Azure AI Agent Service enables rapid Agent development with built-in memory management and a sophisticated interface to seamlessly integrate with popular compute platforms, bridging LLM capabilities with general purpose, programmatic actions.


Key features of Azure AI Agent Service include:

**Rapidly develop and automate processes:**Agents need to seamlessly integrate with the right tools, systems, and APIs to perform deterministic or non-deterministic actions.**Integrate with extensive memory and knowledge connectors:**Agents need to manage conversation state and connect with internal and external knowledge sources to have the right context to complete a process.**Flexible model choice:**Agents built with the appropriate model for their tasks can enable better integration of information from multiple data types, yield better results for task-specific scenarios, and improve cost efficiencies in scaled deployments.**Built-in enterprise readiness:**Agents need to be able to support an organization's unique data privacy and compliance needs, scale with an organization's needs, and complete tasks reliably and with high quality.

### Extensibility capabilities

Extensibility capabilities of Azure AI Agent Service enable Agents to interact with knowledge sources, systems, and platforms to ground and enhance Agent functionality. Specifically:

#### Secure grounding of Agent outputs with a rich ecosystem of knowledge sources

Developers can configure a rich ecosystem of knowledge sources to enable an Agent to access and process data from multiple sources, improving accuracy of responses and outputs. Connectors to these data sources operate within your designated network parameters. Knowledge Tools built into Azure AI Agent Service include:

**File Search**(a built-in retrieval-augmented generation (RAG) tool to process and search through private data in Azure AI Search, Azure Blob Storage, and local files)**Grounding with Bing Search**(a web search tool that uses Bing Search to extract information from the web)**SharePoint**(built-in tools that connect an organization’s internal documents in SharePoint for grounded responses)**Fabric Data Agent**(a built-in tool to chat with structured data on Microsoft Fabric using generative AI)**Bring your licensed data**(a tool that enables grounding using proprietary data accessed using a licensed API key obtained by the developer from the data provider, for example, TripAdvisor)

Agents simplify secure data access to SharePoint and Fabric AI Skills through on-behalf-of (OBO) authentication, allowing the Agent to access only the SharePoint or Fabric files for which the user has permissions.

#### Enabling autonomous actions with or without human input through Action Tools

Developers can connect an Agent to external systems, APIs, and services through Action Tools, enabling the Agent to perform tasks and take actions on behalf of users. Action Tools built into Azure AI Agent Service include:

**Code Interpreter**(a tool that can write and run Python code in a secure environment, handle diverse data formats and generate files with data and visuals)**Azure Logic Apps**(a cloud-based PaaS tool that enables automated workflows using 1,400+ built-in connectors)**Azure Functions**(a tool that enables an Agent to execute serverless code for synchronous, asynchronous, long-running, and event-driven actions)**OpenAPI 3.0 specified tools**(a custom function defined with OpenAPI 3.0 specification to connect an Agent to external OpenAPI-based APIs securely)**Model Context Protocol tools**(a custom service connected via Model Context Protocol through an existing remote MCP server to an Agent).**Deep Research tool**: (a tool that enables multi-step web-based research with the o3-deep-research model and Grounding with Bing Search.).**Computer Use**: (a tool to perform tasks by interacting with computer systems and applications through their UIs)**Browser Automation Tool**(a tool that can perform real-world browser tasks through natural language prompts, enabling automated browsing activities without human intervention in the middle)**Image Generation**(a tool to generate and edit images)**Agent2Agent**(a custom service connected using the agent-to-agent protocol through an existing agent endpoint to a Foundry agent).

#### Orchestrating multi-agent systems

Multi-agent systems using Azure AI Agent Service can be designed to achieve performant autonomous workflows for specific scenarios. In multi-agent systems, multiple context-aware autonomous agents, whether humans or AI systems, interact or work together to achieve individual or collective goals specified by the user. Azure AI Agent Service works out-of-the-box with multi-agent orchestration frameworks that are wireline compatible1 with the Responses API, such as [Microsoft Agent Framework](https://devblogs.microsoft.com/foundry/introducing-microsoft-agent-framework-the-open-source-engine-for-agentic-ai-apps/), an open-source SDK and runtime designed to let developers build, deploy, and manage sophisticated multi-agent systems with ease.

When building a new multi-agent solution, start with building singleton agents with Azure AI Agent Service to get the most reliable, scalable, and secure agents. You can then orchestrate these agents together, using supported orchestration frameworks. Microsoft Agent Framework is constantly evolving to find the best collaboration patterns for agents (and humans) to work together. Features that show production value with Microsoft Agent Framework can then be moved into Microsoft Foundry Agent Service if you're looking for production support and non-breaking changes.

See the [Agent Framework transparency FAQ](https://github.com/microsoft/agent-framework/blob/main/TRANSPARENCY_FAQ.md) to learn about additional considerations and risks when creating multi-agent orchestrations using Microsoft Agent Framework.

Foundry workflows extend multi-agent orchestration by providing a visual designer and YAML-based configuration for building, testing, and deploying agentic processes. Each workflow can coordinate multiple agents, enabling modular automation andtracability. he workflow designer supports versioning, change logs, and visual monitoring, making it easier to manage complex logic and ensure transparency.

1*Wireline compatible* means that an API can communicate and exchange data in a way that is fully compatible with an existing protocol, existing data formats and communication standards, in this case the Responses API protocol. It means that two systems can work together seamlessly without needing changes to their core implementation.

### Use cases

#### Intended uses

Azure AI Agent Service is **flexible and use-case agnostic.** This presents multiple possibilities to automate routine tasks and unlock new possibilities for knowledge work - whether it is personal productivity agents that send emails and schedule meetings, research agents that continuously monitor market trends and automate report creation, sales agents that can research leads and automatically qualify them, customer service agents that proactively follow up with personalized messages, or developer agents that can upgrade your code base or evolve a code repository interactively. Here are examples of intended uses of agents developed using Azure AI Agent Service:

**Healthcare: Streamlined Staff Orientation and Basic Administrative Support:**A hospital’s administrative assistant deploys an agent to collate standard operational procedures, staff directories, and shift policies into concise orientations for new nurses; final materials are reviewed and approved by HR, reducing repetitive work without compromising content quality.**Retail: Personalized Shopping Guidance:**A local boutique owner can deploy an agent that recommends gift options based on a customer’s stated needs and past purchases, guiding shoppers responsibly through complex product catalogs without pushing biased or misleading information.**Government: Citizen Request Triage and Community Event Coordination:**A city clerk uses an agent to categorize incoming service requests (for example, pothole repairs), assign them to the right departments, and compile simple status updates; officials review and finalize communications to maintain transparency and accuracy.**Education: Assisting with Research and Reference Gathering:**A teacher relies on an agent to gather age-appropriate articles and resources from reputable sources for a planetary science lesson; the teacher verifies the materials for factual accuracy and adjusts them to fit the curriculum, ensuring students receive trustworthy content.**Manufacturing: Inventory Oversight and Task Scheduling:**A factory supervisor deploys an agent to monitor inventory levels, schedule restocking when supplies run low, and optimize shift rosters; management confirms the agent’s suggestions and retains final decision-making authority.**Deep Research Tool**: Learn more about intended uses, capabilities, limitations, risks, and considerations when choosing a use case model with deep research technology in the[Azure OpenAI transparency note](/en-us/azure/ai-foundry/responsible-ai/openai/transparency-note?tabs=text).**Computer Use**: The Computer Use tool comes with additional significant security and privacy risks, including prompt injection attacks. Learn more about intended uses, capabilities, limitations, risks, and considerations when choosing a use case in the[Azure OpenAI transparency note](../openai/transparency-note?view=foundry-classic&tabs=image).**Image Generation Tool**: The Image Generation tool is empowered by the gpt-image-1 model. Learn more about intended uses, capabilities, limitations, risks, and considerations when choosing a use case model in the[Azure OpenAI transparency note](/en-us/azure/ai-foundry/responsible-ai/openai/transparency-note?branch=main&tabs=image).

Agent samples have specific intended uses that are configurable by developers to carefully build upon, implement, and deploy agents. See [list of Agent samples](/en-us/azure/ai-foundry/agents/overview#agent-catalog).

#### Considerations when choosing a use case

We encourage customers to use Azure AI Agent Service in their innovative solutions or applications. However, here are some things to consider when choosing a use case:

**Avoid scenarios where use or misuse of the system could result in significant physical or psychological injury to an individual**. For example, scenarios that diagnose patients or prescribe medications have the potential to cause significant harm.**Avoid scenarios where use or misuse of the system could have a consequential impact on life opportunities or legal status**. Examples include scenarios where the AI system or agent could affect an individual's legal status, legal rights, or their access to credit, education, employment, healthcare, housing, insurance, social welfare benefits, services, opportunities, or the terms on which they're provided.**Avoid high-stakes scenarios that could lead to harm**. The model used in an agent may reflect certain societal views, biases, and other undesirable content present in the training data or the examples provided in the prompt. As a result, we caution against using agents in high-stakes scenarios where unfair, unreliable, or offensive behavior might be extremely costly or lead to harm.**Carefully consider use cases in high stakes domains or industry where Agent actions are irreversible or highly consequential**. Such industries include but are not limited to healthcare, medicine, finance, or legal domains. For example: the ability to make financial transactions or give financial advice, the ability to directly interact with outside services, the ability to administer medicine or give health-related advice, the ability to share sensitive information publicly, or the ability to grant access to critical systems.**Legal and regulatory considerations**. Microsoft takes safety and compliance with legal and regulatory obligations seriously. We always strive to abide by applicable laws, regulations, and standards in developing and deploying AI technologies, including the Microsoft Responsible AI Standard. It is your organization’s responsibility to evaluate safety implications and potential specific legal and regulatory obligations when using any Foundry Tools and solutions, including agents, and underlying Agent samples. AI responses may be inaccurate, and AI actions should be monitored appropriately with human oversight. Certain uses and offerings may be subject to legal and regulatory requirements, may require licenses, or may not be suitable for all industries, scenarios, or use cases. Additionally, agents, and underlying Agent samples may not be used in ways prohibited by applicable laws, regulations, terms of service, or relevant codes of conduct.- Microsoft did not create, test, or verify any third-party systems, APIs, servers, agents and services you may decide to connect to. When you connect to a third-party (non-Microsoft) system, API, server, agent, or service, some data will be shared with that service, and your application or agent may receive data in return. We recommend reviewing what data will be shared and being cognizant of third-party practices for retention and location of data. Consider and manage carefully whether your data will flow outside of your organization’s compliance and geographic boundaries and any related implications. Microsoft has no responsibility to you or others in relation to your use of any remote systems, APIs, servers, tools, agents or services. Your use of these services is governed by your agreement with the provider. You are responsible for any usage and associated costs.
**Browser Automation Tool carries substantial security risks and user responsibility**. Browser Automation Tool comes with significant security risks. Both errors in judgment by the AI and the presence of malicious or confusing instructions on web pages which the AI encounters may cause it to execute commands you or others do not intend, which could compromise the security of your or other users’ browsers, computers, and any accounts to which the browser or AI has access, including personal, financial, or enterprise systems. By using the Browser Automation Tool, you are acknowledging that you bear responsibility and liability for any use of it and of any resulting agents you create with it, including with respect to any other users to whom you make Browser Automation Tool functionality available, including through resulting agents.

## Limitations

### Technical limitations, operational factors, and ranges

**Generative AI model limitations:**Because Azure AI Agent Service works with a variety of models, the overall system inherits the limitations specific to those models. Before selecting a model to incorporate into your agent, carefully[evaluate the model](/en-us/azure/ai-studio/how-to/model-catalog-overview#overview-of-model-catalog-capabilities)to understand its limitations. Consider reviewing the[Azure OpenAI Transparency Note](/en-us/azure/ai-foundry/responsible-ai/openai/transparency-note?tabs=text#best-practices-for-improving-system-performance)for additional information about generative AI limitations that are also likely to be relevant to the system and review other best practices for incorporating generative AI into your agent application.**Tool orchestration complexities:**AI Agents depend on multiple integrated tools and data connectors (such as Bing Search, SharePoint, and Azure Logic Apps). If any of these tools are misconfigured, unavailable, or return inconsistent results, or a high number of tools are configured on a single agent, the agent’s guidance may become fragmented, outdated, or misleading.**Unequal representation and support:**When serving diverse user groups, AI Agents can show uneven performance if language varieties, regional data, or specialized knowledge domains are underrepresented. A retail agent, for example, might offer less reliable product recommendations to customers who speak under-represented languages.**Opaque decision-making processes:**As agents combine large language models with external systems, tracing the “why” behind their decisions can become challenging. A user using such an agent may find it difficult to understand why certain tools or combination of tools were chosen to answer a query, complicating trust and verification of the agent’s outputs or actions.**Evolving best practices and standards:**Agents are an emerging technology, and guidance on safe integration, transparent tool usage, and responsible deployment continues to evolve. Keeping up with the latest best practices and auditing procedures is crucial, as even well-intentioned uses can become risky without ongoing review and refinement.

## System performance

### Best practices for improving system performance

**Evaluate agent performance**: Evaluate agents for how well they reliably identify user requests, select appropriate tools and processes, and adhere to assigned tasks. Use the following[Microsoft Azure AI Evaluation SDK](/en-us/azure/ai-foundry/how-to/develop/agent-evaluate-sdk)evaluators:[Intent resolution](https://aka.ms/intentresolution-sample): Measures how well the agent identifies the user’s request, including how well it scopes the user intent, asks clarifying questions, and reminds end users of its scope of capabilities.[Tool call accuracy](https://aka.ms/toolcallaccuracy-sample): Evaluates the agent’s ability to select the appropriate tools, and process correct parameters from previous steps.[Task adherence](https://aka.ms/taskadherence-sample): Measures how well the agent’s final response adheres to its assigned tasks, according to its system message and prior steps.

**Provide trusted data:**Retrieving or uploading untrusted data into your systems could compromise the security of your systems or applications. To mitigate these risks in your applications using the Azure AI Agent Service, we recommend logging and monitoring LLM interactions (inputs/outputs) to detect and analyze potential prompt injections, clearly delineating user input to minimize risk of prompt injection, restricting the LLM’s access to sensitive resources, limiting its capabilities to the minimum required, and isolating it from critical systems and resources. Learn about additional mitigation approaches in[Security guidance for Large Language Models.](/en-us/ai/playbook/technology-guidance/generative-ai/mlops-in-openai/security/security-recommend)**Choose and integrate tools thoughtfully:**Select tools that are stable, well-documented, and suited to the agent’s intended uses and objectives. For instance, use a reliable database connector for factual lookups or a well-tested API for executing specific actions. Limit the number of tools to those that genuinely enhance functionality and specify how and when the agent should use them.**Provide user proactive controls for system boundaries:**Consider creating user controls to give users operating the AI agent the ability to proactively set boundaries on what actions or tools are permitted, and what domains the agent can operate in.**Establish real-time oversight and human-in-the-loop processes:**Consider providing users with adequate real-time controls to authorize, verify, review, and approve agentic system behavior, including actions, planned tasks, operating environments or domain boundaries, and knowledge or action tool access. Particularly for critical or high-stakes tasks, consider incorporating mandatory human review and approval steps by the user. Ensure that a user or human operator can easily intervene, correct, or override the agent’s decisions, especially when those decisions have safety or legal implications. For more information, see[Overreliance on AI](/en-us/ai/playbook/technology-guidance/overreliance-on-ai/overreliance-on-ai?wt.mc_id=reliance_v1_multichannel_cnl_csadai).**Ensure intelligibility and traceability for human decision-making**: Provide users with information before, during, and after actions are taken to help them understand justifications for decisions, identify where to intervene, and troubleshoot issues. Incorporate instrumentation or logging within the system, such as OpenTelemetry traces from Azure AI Agent Service, to trace outputs, including prompts, model steps, and tool calls. This enables reconstruction of the agent’s reasoning process, isolation of issues, tuning of prompts, refinement of tool integration, and verification of guideline adherence. For more information, see[Tracing using Application Insights](/en-us/azure/ai-services/agents/concepts/tracing).**Layer agent instructions and guidance:**Break down complex tasks into steps or sub-instructions within the system prompt. This can help the agent tackle multi-step reasoning more effectively, reducing errors and improving the clarity of the final output.**Recognize complexity thresholds for scaling:**When a single agent’s system message consistently struggles to handle the complexity, breadth, or depth of a task—such as frequently producing incomplete results, hitting reasoning bottlenecks, or requiring extensive domain-specific knowledge—the system may benefit from transitioning to a multi-agent architecture. As a best practice, monitor performance indicators like response accuracy, latency, and error frequency. If refinements to the single agent’s prompt no longer yield improved outcomes, consider decomposing the workload into specialized subtasks, each governed by its own agent. By segmenting complex tasks (for example, splitting policy research and policy interpretation into separate agents), you can maintain modularity, use specialized domain knowledge more effectively, and reduce cognitive overload on any single agent.

## Evaluating and integrating Azure AI Agent Service for your use

**Map Agent risks and impacts.**Before developing or deploying your agentic application, carefully consider the impact of the intended actions and the consequences of actions or tool use not working as intended – such as generating or taking action on inaccurate information or causing biased or unfair outcomes – at different stages.**Ensure adequate human oversight and control.**Consider including controls to help users verify, review and/or approve actions in a timely manner, which may include reviewing planned tasks or calls to external data sources, for example, as appropriate for your system. Consider including controls for adequate user remediation of system failures, particularly in high-risk scenarios and use cases. As an example, the MCP tool allows you to pass custom headers such as authentication keys or schema as may be needed by a remote MCP server. In cases such as this, we recommend you review all data being shared with remote servers and optionally logging it for auditing purposes. Be cognizant of third party practices for retention and location of data.**Clearly define actions and associated requirements.**Clearly defining which actions are allowed (action boundaries), prohibited, or need explicit authorization may help your agentic system operate as expected and with the appropriate level of human oversight.**Clearly define intended operating environments.**Clearly define the intended operating environments (domain boundaries) where your agent is designed to perform effectively.**Ensure appropriate intelligibility in decision making.**Providing information to users before, during, and after actions are taken and/or tools are called may help them understand action justification or why certain actions were taken or the application is behaving a certain way, where to intervene, and how to troubleshoot issues.

- Follow additional generative AI best practices as appropriate for your system, including recommendations in the
[Azure OpenAI Transparency Note](/en-us/azure/ai-foundry/responsible-ai/openai/transparency-note?tabs=text#best-practices-for-improving-system-performance).

## Learn more about responsible AI

[Microsoft AI principles](https://www.microsoft.com/ai/responsible-ai)[Microsoft responsible AI resources](https://www.microsoft.com/ai/responsible-ai-resources)[Microsoft Azure Learning courses on responsible AI](/en-us/training/paths/responsible-ai-business-principles/)
