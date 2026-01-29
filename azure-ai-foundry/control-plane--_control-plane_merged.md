---
merged_at: 2026-01-29T15:40:29.542723
merged_files: 7
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/control-plane/how-to-optimize-cost-performance -->

# Optimize model cost and performance

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When your model or agent costs start increasing, use the **Ask AI agent** — the built-in chat assistant — to quickly diagnose issues, take action, and verify improvements. You can access the Ask AI agent from the top navigation bar in the Foundry portal.

This article walks you through a recommended workflow, from identifying cost spikes to switching models and validating performance improvements — all within the Foundry portal.

Tip

The **Operate** > **Overview** page includes pre-built prompts specific to agent optimization and performance. Select one of these prompts to start a conversation with the Ask AI agent, or open the Ask AI agent from the top navigation bar and type your own question.

## Prerequisites

-
An Azure account with an active subscription. If you don't have one, create a

[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). A Foundry project. If you don't have one,

[create a project](../how-to/create-projects?view=foundry).

At least one deployed or published agent with cost data. For meaningful trend analysis, you need a minimum of 7 days of usage data.

You have access to the

**Ask AI agent**(the chat assistant).An evaluation dataset configured for your project. To set one up, see

[Create and manage evaluation datasets](../how-to/develop/evaluate-sdk?view=foundry).

## Detect cost increases

Start by opening the Ask AI agent from the top navigation bar, or go to **Operate** > **Overview** to use one of the pre-built prompts. Ask the assistant to provide a summary of your metrics and cost data from the **Foundry Control Plane** dashboard.

You can select a predefined prompt on the **Operate** overview page, or type your own question, such as:

"Summarize my recent cost trend."

"Which agents contributed most to my cost increase?"


The Ask AI agent generates a summary that highlights key cost drivers, such as high token usage, longer completion length, or frequent evaluation runs. The summary includes annotated links to the dashboard charts for deeper inspection.

## Investigate high-cost agents

After reviewing the summary, you can explore detailed insights for specific agents by asking:

"Show me cost and performance details for [agent name]."

"Break down cost by model or deployment for this agent."


You can also select **Assets** in the left pane. Select **View Agent details** to view the **Assets** page, where you can compare your agents with cost and token usage, and see which agent costs the most.

## Switch to a cost-efficient model

When you identify a model as a cost driver, ask the Ask AI agent:

"Recommend a cheaper model with similar performance."

"Switch this agent's deployment to a more cost-efficient model."


The Ask AI agent:

Recommends alternative models available in the

**Model Catalog**.Provides performance and cost comparisons.

Upon confirmation, provides a link to the model deployment page.


Follow the instructions in the model deployment page, or continue to chat with the Ask AI agent to complete the model deployment step.

## Evaluate model differences

After switching models, you can ask the Ask AI agent to run an evaluation that compares the old and new models:

- "Evaluate performance and cost difference between the old and new model."

The Ask AI agent provides guidance on how to create an evaluation and gives you a link to the evaluation creation wizard. You can follow the instructions step by step to create two evaluation runs on the two models.

View the results after both evaluation runs complete.

## Update your agent

When you confirm the new model performs better than the current model, go to **Agent Playground** to update the model and save a new version.

## Track improvements

Later, return to the Ask AI agent and ask:

- "Show me the summary on the latest data for cost."

The Ask AI agent retrieves the latest metrics from your continuous evaluation and summarizes improvements in cost and performance trends. This feature helps you continuously monitor ROI and efficiency.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/control-plane/how-to-enforce-limits-models -->

# Enforce token limits for models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Microsoft Foundry Control Plane enforces tokens-per-minute (TPM) rate limits and total token quotas for model deployments at the project scope to prevent runaway token consumption and align usage with organizational guardrails. Control Planes integrates with AI Gateway to provide advance policy enforcement for models.

This article explains how to configure token rate limiting and token quotas.

## Prerequisites

Before getting started, make sure you have:

-
An Azure account with an active subscription. If you don't have one, create a

[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). A Foundry resource with AI Gateway configured. Learn more about

[how to enable AI Gateway for a Foundry resource](../configuration/enable-ai-api-management-gateway-portal?view=foundry).A Foundry project added to the configured AI Gateway.

Tip

You need

**API Management Service Contributor**(or**Owner**) on the Azure API Management resource to enable AI Gateway at a given project.

## Understand AI Gateway

Control Planes integrates with AI Gateway to provide advanced policy enforcement for models. AI Gateway sits between clients and model deployments, making all requests flow through the API Management instance associated with it. Limits apply at the project level (each project can have its own TPM and quota settings).


Use AI Gateway for:

- Multi-team token containment (prevent one project from monopolizing capacity).
- Cost control by capping aggregate usage.
- Compliance boundaries for regulated workloads (enforce predictable usage ceilings).

## Configure token limits

You can configure token limits for specific model deployments within your projects.

Select the gateway you want to use from the

**AI Gateway**gateway list.Select

**Token management**in the gateway details pane that appears.Select

**+ Add limit**to create a new limit for a model deployment.Select the project and deployment you want to restrict, and enter a value for

**Limit (Token-per-minute)**.Select

**Create**to save your changes.

Subsequent requests that exceed the TPM threshold receive rate-limit responses. Requests that exceed the quota produce quota-exceeded responses indicating `429 Too Many Requests`

if the rate limit is exceeded, or `403 Forbidden`

if the total token quota is exhausted.

## Understand quota windows

Token limits have two complementary enforcement dimensions:

Tokens per minute (TPM) rate limit: Limits token consumption to a configured maximum per minute. When the TPM limit is exceeded, the caller receives a

`429 Too Many Requests`

response status code.Total token quota: Limits token consumption to a configured maximum per quota period (for example, hourly, daily, weekly, monthly, or yearly). When the quota is exceeded, the caller receives a

`403 Forbidden`

response status code.

If you send many requests concurrently, token consumption can temporarily exceed the configured limits until responses are processed.

Adjusting a quota or TPM value affects subsequent enforcement decisions.

For more information, see [AI Gateway capabilities in Azure API Management](/en-us/azure/api-management/genai-gateway-capabilities) and [Limit large language model API token usage](/en-us/azure/api-management/llm-token-limit-policy).

## Verify enforcement

Send test requests to a model deployment endpoint by using the project's gateway URL and key.

Gradually increase request frequency until the TPM limit triggers.

Track cumulative tokens until the quota triggers.

Validate that

`429 Too Many Requests`

is returned once the TPM limit is exceeded, and`403 Forbidden`

is returned once the quota is exhausted.

Success criteria:

- Rate-limited responses appear once TPM exceeded.
- Quota error appears once total token allocation exhausted.

## Adjust limits

Return to project

**AI Gateway**settings.Modify TPM or quota values.

Save; new limits apply immediately to subsequent requests.


## Troubleshooting

| Issue | Possible cause | Action |
|---|---|---|
| APIM instance doesn't appear | Provisioning delay | Refresh after a few minutes. |
| Limits aren't enforced | Misconfiguration or project not linked | Reopen settings; confirm enforcement toggle is on. Confirm that the AI Gateway is enabled for the project and if correct limits are configured. |
| High latency after enablement | APIM cold start or region mismatch | Check APIM region vs resource region. Call the model directly and compare the result with the call proxied through the AI Gateway to identify if performance issues are related to the gateway. |

If the Admin console is slow, retry after a brief interval.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/control-plane/monitoring-across-fleet -->

# Monitor agent health and performance across your fleet

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As your organization scales from isolated copilots to autonomous multi-agent fleets, maintaining visibility and control becomes critical. The Foundry Control Plane provides a unified command center where you can monitor all agents, models, and tools across your enterprise from build to production. Fleet monitoring serves multiple roles:

**Team managers**gain oversight of agent operations and team productivity**Administrators**enforce governance policies and track compliance posture**Cost managers**optimize spending and identify resource inefficiencies**Security teams**monitor for prohibited behaviors and policy violations

This article shows you how to use the Foundry Control Plane's capabilities to track agent health, performance, compliance, and cost efficiency at scale. With centralized monitoring, you can identify issues early, optimize resource consumption, and ensure your AI systems operate safely and reliably.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Prerequisites

-
An Azure account with an active subscription. If you don't have one, create a

[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). A Foundry project. If you don't have one,

[create a project](../how-to/create-projects?view=foundry).

- You need the following permissions:
- Read access to the project and subscription you want to view data for.
[Log Analytics Reader](/en-us/azure/role-based-access-control/built-in-roles/monitor#log-analytics-reader)role (or above) on the Azure Application Insights resource associated with your agent.[Cost Management reader](https://go.microsoft.com/fwlink/?linkid=2345241)role.


Note

This capability is available only in the Foundry (new) portal. Look for in the portal banner to confirm you're using Foundry (new).

## How monitoring works

Control Plane discovers all the agents you have access to and uses the Azure Application Insights associated with the resources hosting your agent to help you monitor and diagnose your agents.

Control Plane supports:

- Foundry agents, including
[prompt-based agents](../agents/overview?view=foundry),[workflows](../agents/concepts/workflow?view=foundry), and[hosted-agents](../agents/concepts/hosted-agents?view=foundry). [Azure SRE Agent](/en-us/azure/sre-agent/)[Azure Logic App agent loops](/en-us/azure/logic-apps/agent-workflows-concepts)[Custom agents](register-custom-agent?view=foundry)registered manually

Because Control Plane aggregates information across resources within the subscription, different users may see different agents listed depending on their access.

Control Plane **aggregates logs and metrics available across each of the Azure Application Insights** connected to each of the agents:

Control Plane requires agents to log diagnostic information following OpenTelemetry standard with semantic conventions for Generative AI applications. Configuring Azure Application Insights on each resource isn't mandatory but **it's strongly advisable**. When such telemetry is available, Control Plane can:

**Fleet health metrics**: Track active agents, run completion rates, and error trends across your entire fleet**Cost and performance tracking**: Monitor token usage, budget consumption, and resource efficiency across all agents**Anomaly detection**: Identify cost spikes, performance degradation, and emerging issues through trend analysis**Drill-down analysis**: Navigate from fleet-level metrics to individual agent traces and logs for detailed investigation

Important

Agents running on resource without Azure Application Insights don't have health metrics, cost tracking, or drill-down traces.

## Configure monitoring

Follow these steps for each project where you want to configure monitoring:

Select

**Operate**>**Admin console**.Under

**All projects**, use the search box to look for your project.Select the project.

Select the tab

**Connected resources**.Ensure there's a resource associated under the category

**Application Insights**.If there is no resource associated, add one by selecting

**Add connection**and select**Application Insights**.Tip

You can sink traces to either different Azure Application Insight resources or to the same one depending on your governance and security requirements.

Your project is configured for observability and tracing.


### Permissions

Once you configured observability, ensure you have the following permissions:

[Log Analytics Reader](/en-us/azure/role-based-access-control/built-in-roles/monitor#log-analytics-reader)role (or above) on the Azure Application Insights resource.[Cost Management reader](https://go.microsoft.com/fwlink/?linkid=2345241)role.

## View metrics

You can view aggregated metrics for all agents within a selected project by using Foundry. The **Overview** pane provides insights into fleet health, compliance, and performance trends.

-
Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**. Select

**Operate**from the upper-right navigation.The

**Overview**pane displays common metrics and insights for all discovered agents within the subscription by default:Use the project drop-down to scope down the metrics to specific projects if needed.

Configure the dates range you are seeing using the date selectors located in the upper right corner.


## View agents' metrics

You can view all your assets under a specific project along with top-level metrics from Foundry.

-
Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**. Select

**Operate**from the upper-right navigation.Select

**Assets**in the left pane.Select the

**Agents**tab.You can see the details of agents discovered within the subscription. See

[agent inventory](how-to-manage-agents?view=foundry#agents-inventory)to learn about the details of this page.To view more granular information on the performance of an individual agent, the side panel provides quick insights into the selected agent's health and recent activity. You can use it to identify issues and take corrective actions.

In this section, you see:

Active alerts: View policy, security, and evaluation alerts grouped by severity and take action.

Activity: See key metrics such as error rate over time, total run information, and information on token usage.


To learn more about how to manage individual agents see

[Manage agents at scale](how-to-manage-agents?view=foundry).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/control-plane/overview -->

# What is the Microsoft Foundry Control Plane?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Microsoft Foundry Control Plane** is a unified management interface that provides visibility, governance, and control for AI agents, models, and tools across your Foundry enterprise. The Foundry Control Plane serves as your central location for managing every aspect of your AI fleet, from build to production.

As organizations evolve from isolated copilots to autonomous multi-agent fleets, they need unified oversight. The Foundry Control Plane provides the visibility, governance, and control needed to scale with confidence.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Core Functionalities

The Foundry Control Plane consolidates **inventory, observability, compliance, and security** into one role-aware interface. It integrates seamlessly with Microsoft security and governance systems (Defender, Purview, Microsoft Entra) to deliver **trust at scale**.

The Foundry Control Plane allows you to:

### Manage your fleet across Foundry, Microsoft, and third-party agents in one place

Track key performance indicators such as active agents, run completion, compliance posture, cost efficiency, and prohibited behaviors across

[supported agent platforms](how-to-manage-agents?view=foundry#supported-agent-platforms).Use deep links to evaluation and monitoring experiences for rapid debugging, diagnosis, and remediation.

Visualize fleet health through intuitive dashboards that surface trends and anomalies instantly.


### Observe, protect, and improve

Correlate alerts, evaluation results, and trace data to pinpoint issues instantly.

[Continuously evaluate](../how-to/continuous-evaluation-agents?view=foundry)agent performance, quality, and risk dimensions such as[Task Adherence, Intent Resolution, Tool Call Success](../concepts/evaluation-evaluators/agent-evaluators?view=foundry),[Groundedness](../concepts/evaluation-evaluators/rag-evaluators?view=foundry), Sensitive Data Leakage, and Jailbreak/XPIA exposure.Use the

and**AI Red Teaming Agent**for automated vulnerability probing and error root-cause discovery.**cluster analysis**Let

**Foundry Agent**recommend improvements, from prompt refinements to model version upgrades.

### Govern and enforce with guardrails

Define enterprise-wide guardrail policies for safety, compliance, and quality.

Apply

**bulk remediation**to instantly correct noncompliant configurations across your fleet.

### Secure agents

Schedule

**automated red-teaming scans**and**drift monitoring**for ongoing agent testing.View Defender and Purview alerts directly in the Control Plane dashboard.

Track rate limits, token usage, and cost anomalies to prevent inefficiency or abuse.


## Key features

The Foundry Control Plane experience begins in the **Operate** tab, your command center on the upper right-hand side of the Foundry workspace. From Operate, you can monitor, govern, and optimize every agent, model, and deployment within your subscription. Each sub-tab within Operate is designed around a specific job-to-be-done (JTBD), helping different roles, from builders to administrators, manage AI systems confidently at scale.

### Overview

Use this page to understand fleet health, performance, and compliance at a glance.

The Fleet Overview page provides a high-level snapshot of your AI estate, aggregating key operational and compliance metrics in one view.

- View key stats such as active agents, cost trends, run completion rate, and prevented behaviors.
- Drill into anomalies or cost spikes through contextual charts and direct links to Inventory, Observability, or Policy pages.
- Identify potential risks early with trend-based health scores and alert summaries.

### Assets

Use this view to track, analyze, and manage every agent, model, and tool from one place.

The **Inventory** view provides a unified, searchable table of all AI assets across projects within a subscription. It brings together critical metadata and health indicators, so you can assess and act on your AI estate efficiently.

- Filter and sort by key attributes such as version, tags, health score (%), cost, alerts, and token usage to locate assets quickly.
- Drill down from any entry in the
**Agent Inventory**table intoor[Evaluation](../how-to/continuous-evaluation-agents?view=foundry)tabs for pre- and post-deployment insights.[Monitoring](../how-to/monitor-applications?view=foundry) - Surface inline recommendations to refine prompts, upgrade models, or optimize configurations based on performance and cost signals.
- Correlate runtime logs with evaluation results to uncover root causes of errors or performance degradation.
- Visualize drift, latency, and error clusters across runs or builds to detect emerging issues early.
- Integrate with the
to automate vulnerability probing, regression testing, and issue reproduction.**AI Red Teaming Agent** - Observe and modify model and agent guardrails.

Together, these capabilities turn the Inventory into the operational backbone of the Control Plane, a single pane to understand, improve, and secure every AI asset in your environment.

### Compliance

Use this tab to govern your AI systems and enforce the right guardrails.

The **Policy & Security** tab empowers organizations to define, apply, and continuously monitor guardrails and compliance policies across their AI estate. It provides a unified interface to operationalize Responsible AI principles while ensuring enterprise-grade safety and regulatory alignment.

- Define and enforce protections through deep integrations with
**Azure Policy**,**Microsoft Defender**, and**Purview**, ensuring that identity, data, and threat safeguards work in concert. - Apply versioned policies and track assignments to maintain full auditability and traceability across agents and environments.
- Monitor compliance posture in real time, surfacing noncompliant assets and enabling bulk remediation directly from the Control Plane.

Policy Management in Foundry allows administrators and developers alike to embed quality and safety requirements into the development and deployment lifecycle. These policies ensure that all models operate safely, adhering to organizational and regulatory standards.

### Quota

Use this tab to view, adjust, and request quotas.

The **Quota** tab allows customers to easily see their model deployments and how much quota each deployment is consuming. It gives insights into usage patterns and helps manage resources effectively.

### Admin

Use this tab to view, organize, and administer all projects, users, and connected resources across your Foundry environment.

The ** Admin** tab extends your operational view beyond a single project. While most work in Foundry takes place within a project context,

**Admin**provides an enterprise-level lens to oversee and configure multiple projects, user permissions, and linked Azure resources from one place.

From **Operate → Admin**, administrators and power users can:

- Gain visibility into all projects across their subscription or tenant, including active, inactive, and archived workspaces.
- View detailed project information such as owners, region, connected services, and compliance posture.
- Add or remove users directly from a project, defining granular access levels aligned with organizational roles.
- Attach or manage connected resources, such as storage accounts, compute clusters, and Foundry Tools, ensuring projects remain properly provisioned.
- Assign access at parent scope (subscription or resource group) to apply consistent governance and permissions inheritance across multiple projects.

Together, these capabilities make **Admin** the Control Plane's administrative backbone. It's a centralized console to ensure every Foundry project remains properly configured, compliant, and connected to the right people and infrastructure.

## Get started

The Foundry Control Plane is a feature available in the Foundry (new) portal. To get started:

- Configure AI Gateway in your Foundry projects to enable advanced governance features.[Configure AI Gateway](../configuration/enable-ai-api-management-gateway-portal?view=foundry)- Configure observability features in your project to enable metrics and diagnostic information.[Configure monitoring for your agents fleet](monitoring-across-fleet?view=foundry)- See which agents are available in your subscription and manage them in a centralized location.[Discover agents in your subscription](how-to-manage-agents?view=foundry)- Extend your governance surface by bringing third-party or external agents into the Foundry Control Plane registry.[Register custom Agents](register-custom-agent?view=foundry)

## Related content

- Learn how to enforce Responsible AI policies, integrate Defender and Purview signals, and respond to compliance alerts.[Ensure Compliance and Security](how-to-manage-compliance-security?view=foundry)- Analyze cost drivers, token usage, and resource consumption to achieve higher ROI from your agent fleet.[Optimize model cost and performance](how-to-optimize-cost-performance?view=foundry)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/control-plane/how-to-manage-agents -->

# Manage agents at scale

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Microsoft Foundry Control Plane provides centralized management and observability for agents running across different platforms and infrastructures.

This article explains how to manage agents across a subscription using Microsoft Foundry Control Plane.

## Agents inventory

The **Assets** page provides a unified, searchable table of all AI assets across projects within a subscription. It brings together critical metadata and health indicators, so you can assess and act on your AI estate efficiently.

Control Plane automatically discovers [supported agents](#supported-agent-platforms) within resources in the selected subscription and displays them in the **Operate > Assets > Agents** page.

The following information is displayed:

| Column | Description |
|
|---|

**Name****Source**[supported platforms](#supported-agent-platforms).**Project**Custom

**Status**[lifecycle operations](#lifecycle-operations). Possible values are:**Version****Published as**[published as an agent application](../agents/how-to/publish-agent?view=foundry). Published agents in Foundry have their own endpoint for invocation.**Error rate**[observability configured](#observe-agents).**Estimated cost**[observability configured](#observe-agents).**Token usage**[observability configured](#observe-agents).**Runs**[observability configured](#observe-agents).**Monitoring features**[The three stages of GenAIOps evaluation](../concepts/observability?view=foundry#the-three-stages-of-genaiops-evaluation).**Entra ID**[Agent identity concepts in Microsoft Foundry](../agents/concepts/agent-identity?view=foundry).### Permission's model

Control Plane automatically discovers agents that users have access to. Because Control Plane aggregates information across resources within the subscription, different users may see different agents listed in the **Assets** page depending on the access level on each of those resources.

## Supported agent platforms

Control Plane automatically discovers agents in the following platforms:

- Foundry agents, including
[prompt-based agents](../agents/overview?view=foundry),[workflows](../agents/concepts/workflow?view=foundry), and[hosted-agents](../agents/concepts/hosted-agents?view=foundry). [Azure SRE Agent](/en-us/azure/sre-agent/)[Azure Logic App agent loops](/en-us/azure/logic-apps/agent-workflows-concepts)

For agentic platforms not supported by Control Plane, you can [manually register the agent in a Microsoft Foundry project](register-custom-agent?view=foundry) to enable management.

### Foundry agents

Control Plane can help you manage agents across all your Foundry projects. When you create an agent or workflow in a Foundry project, the agent shows in the inventory page. Control Plane lists all the agents across all the projects within a subscription.

For each agent, you see:

The latest version of the agent.

Versions

[published as agent applications](../agents/how-to/publish-agent?view=foundry).

In this way, you can monitor versions consumed by your users and new versions under development. The following example shows multiple Foundry agents listed. Agent `format-agent`

version 6 was published, however, version 7 (latest) is still under development.

Note

Foundry classic agents and Azure OpenAI Assistants aren't supported.

### Azure SRE agent

Azure SRE Agent helps you maintain the health and performance of your Azure resources through AI-powered monitoring and assistance. Agents continuously watch your resources for problems, provide troubleshooting help, and suggest remediation steps in a natural-language chat interface. Learn more about [Azure SRE Agent](/en-us/azure/sre-agent/).

Control Plane discovers Azure SRE agent resources in your subscription and shows them in the inventory page.

### Azure Logic Apps agent loop

Azure Logic Apps supports workflows that complete tasks by using agent loops with large language models (LLMs). An agent loop uses an iterative process to solve complex, multi-step problems. Learn more about [Workflows with AI agents and models in Azure Logic Apps](/en-us/azure/logic-apps/agent-workflows-concepts).

Control Plane discovers Azure Logic Apps resources containing agent loop workflows and lists them in the inventory page.

Note

Observability features, including traces and metrics, aren't supported in Azure Logic Apps agent loops.

### Custom agents

You can register custom agents—running in Azure compute services or other cloud environments—to gain visibility into their operations and control their behavior. You can register a custom agent in the Control Plane and develop the agent in the technology of your choice, both platform and infrastructure solutions.

Learn how to [register an agent in Control Plane](register-custom-agent?view=foundry) to enable management.

## Observe agents

Control Plane uses the Azure Application Insights associated with the resources hosting your agent to help you monitor and diagnose your agents. When such telemetry is available, Control Plane can:

- Compute runs and error rates
- Compute usage metrics, including token usage and cost
- Collect execution traces

If you don't see such information for your agent, [you need to configure Azure Application Insights](monitoring-across-fleet?view=foundry#configure-monitoring). Ensure you also have [the appropriate permissions to view Azure Application Insights data and cost metrics](monitoring-across-fleet?view=foundry#permissions).

Tip

We strongly advise configuring Azure Application Insights for each of the resources hosting agents. For Foundry agents, Azure Applications Insights is configured per Foundry project. However, you can connect multiple Foundry projects to the same Azure Applications Insights to optimize resources.

### View traces

You can view traces and logs sent to Foundry. Traces are stored in Azure Application Insights and can be queried using Microsoft Foundry portal or any other compatible tool.

To view them:

Select

**Operate**from the upper-right navigation.Select

**Assets**in the left pane.Select the agent.

Select the

**Traces**tab.You see one entry for each call made to the agent.

Two columns contain IDs associated with the call,

**Trace ID**and**Conversation ID**. Traces are stored in Azure Application Insights and contain telemetry to diagnose behavior.**Conversation ID**column applies for Foundry agents, which contains the*conversation*associated with the trace. Conversations are stored in Microsoft Foundry service:To see the details, select a value under

**Trace ID**column.:Tip

Custom agents require extra configuration to see details including tools and LLMs spans. Learn more at

[Instrument custom code agents](register-custom-agent?view=foundry#instrument-custom-code-agents).

## Lifecycle operations

Control Plane helps organizations to control agents to manage usage and infrastructure cost. Different agent platforms support different operations.

The following table summarizes supported actions for each platform. Foundry agent's support depends on the agent kind and its publishing state:

| Platform | Agent kind | Published | Supported actions | Notes |
|---|---|---|---|---|
| Foundry | Prompt Workflow |
No | None | Unpublished agents don't have dedicated deployments and they use the project's endpoint to receive requests. Hence, their lifecycle is attached to the project's lifecycle. To stop an unpublished prompt agent or workflow, you must delete them. |
| Foundry | Hosted | No | Start/stop | Stopping a hosted agent stops the deployment associated with it. Any compute attached to is deallocated. |
| Foundry | Prompt Workflow Hosted |
Yes | Start/stop | Stopping a published agent stops the deployment associated with it. It deallocates any compute attached. |
| Azure SRE | NA | NA | Start/stop | |
| Azure Logic Apps | NA | NA | Start/stop | You can start/stop an Azure Logic Apps agent loop by stopping the Logic App resource that hosts them. Stopping a Logic App resource stops all the workflows associated with it. |
| Custom | NA | NA | Block/unblock | Foundry doesn't have access to the underlying infrastructure where the agent runs, so start and stop operations aren't available. However, Foundry can block incoming requests to the agent, preventing clients from consuming it. |

### Start and stop agents

Stopping an agent stops the infrastructure that is associated with this agent and moves the agent to the **Stopped** state.

Stopping an agent deprovisions its infrastructure and prevents new runs. Any workflows or resources connected to this agent can't access it. Notice that this operation **doesn't terminating existing runs**.

To stop an agent:

Select

**Operate**from the upper-right navigation.Select

**Assets**in the left pane.Select the agent you want to stop. The information panel appears.

Select

**Update status**and then select**Stop**.Confirm the operation.


After you stopped the agent, the **Status** of the agent in Foundry shows as **Stopped**.

To start the agent:

Select

**Update status**and then select**Start**.Confirm the operation.


### Block and unblock agents

For [custom agents](register-custom-agent?view=foundry), Foundry doesn't have access to the underlying infrastructure where the agent runs, so start and stop operations aren't available. However, Foundry can block incoming requests to the agent, preventing clients from consuming it. This capability allows administrators to disable an agent if it misbehaves.

To block incoming requests to your agent:

Select

**Operate**from the upper-right navigation.Select

**Assets**in the left pane.Select the agent you want to block. The information panel appears.

Select

**Update status**and then select**Block**.Confirm the operation.


After you block the agent, the **Status** of the agent in Foundry shows as **Blocked**. Agents in the **Blocked** state run in their associated infrastructure but can't take incoming requests. Foundry blocks any attempt to interface with the agent.

To unblock the agent:

Select

**Update status**and then select**Unblock**.Confirm the operation.


### Unknown states

Under certain circumstances, agents can display the status **Unknown**. On those cases, Control Plane is unable to determine the status of the agent either because the source platform is unavailable or because the agent failed to report its state back.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/control-plane/how-to-manage-compliance-security -->

# Manage compliance and security in Microsoft Foundry

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn how Foundry Control Plane helps you manage compliance, enforce guardrail controls, and integrate security tooling such as Microsoft Defender for Cloud across subscriptions.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Use the compliance workspace tabs to reach the right surface quickly.

| Tab | Navigation | Outcome |
|---|---|---|
| Policies | Operate > Compliance > Policies |
Review guardrail policies, check compliance, and create or edit enforcement rules. |
| Assets | Operate > Compliance > Assets |
Inspect individual model deployments, view policy violations, and jump to remediation. |
| Guardrails | Operate > Compliance > Guardrails |
Compare guardrail configurations across deployments and spot coverage gaps. |
| Security | Operate > Compliance > Security |
Review Microsoft Defender for Cloud recommendations and manage Microsoft Purview enablement. |

## Prerequisites

-
An Azure account with an active subscription. If you don't have one, create a

[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). A Foundry project. If you don't have one,

[create a project](../how-to/create-projects?view=foundry).

If you use agents, you need Agents v2 or later for full compliance feature support.

Appropriate permissions based on the tasks you want to perform:

- To
**view**compliance status and guardrail policies: No special permissions required beyond project access. - To
**create or edit**guardrail policies: You must be anor**Owner**at the Azure subscription or resource group level. See**Resource Policy Contributor**[Overview of Azure Policy](/en-us/azure/governance/policy/overview#azure-policy-and-azure-rbac). - To
**enable Microsoft Defender for Cloud**: You need the**Security Admin**role or be a subscription**Owner**so you can turn on Defender plans and agentless protections. - To
**configure Purview integration**: The**Azure AI Account Owner**role is required.

- To

Note

This capability is available only in the Foundry (new) portal. Look for in the portal banner to confirm you're using Foundry (new).

## Create, review, and manage guardrail policies

Guardrail policies let you mandate minimum guardrail controls for your model deployments across a subscription or within a resource group. Guardrail controls include content filtering, abuse monitoring, and other safety measures that protect your model deployments from generating harmful content or being misused.

To learn more about guardrail policies, visit [Guardrails and controls overview](../guardrails/guardrails-overview?view=foundry).

Note

Most users don't have permission to create guardrail policies because they need the appropriate Azure RBAC roles for Azure Policy. See [Overview of Azure Policy](/en-us/azure/governance/policy/overview#azure-policy-and-azure-rbac). Most users in Foundry can still view the compliance status of individual guardrail policies and model deployments.

Tip

Access the compliance workspace by selecting **Operate** in the top navigation, then choosing **Compliance** in the left pane. Use the subscription and project filters to scope your view before switching tabs.

### View and fix compliance violations

Determine whether any model deployments don't comply with organizational guardrail policies. To assess compliance status and address issues, follow these steps:

Select the

**Policies**tab. Review all applicable guardrail policies within your subscription and project. To expand the scope beyond a single project, adjust the project filter to**All projects**for an overview of the entire subscription. You can also switch subscriptions.Identify any noncompliant guardrail policy by locating those with a

**Violations detected**value in the**Policy Compliance**column.Select a guardrail policy. Refer to the right-hand side panel and select an asset to compare its guardrail settings with the requirements that the guardrail policy specifies.

To update the guardrail configuration of a noncompliant asset, select

**Fix now**. This selection opens the model deployment's guardrail configuration page where you can adjust settings to meet the guardrail policy requirements. After saving your changes, the compliance status updates within a few minutes.

Additionally, you can review compliance status by asset rather than by guardrail policy:

Select the

**Assets**tab by using the**Policy/Assets**toggle.Review model deployments within the chosen subscription and project.

Examine any assets marked as

**Violation detected**in the**Policy Compliance**column. Select these rows to access further details. Assets might appear multiple times if they're subject to several guardrail policies.Review the governing guardrail policies and the specifics of any noncompliant guardrail policy in the right-hand panel.

Select

**View in Build**to modify the guardrail configuration and bring the model deployment into compliance. Review all relevant guardrail policies for each asset to ensure all necessary adjustments are made to achieve full compliance.

### Create a guardrail policy

To create a guardrail policy, follow these steps:

In the compliance workspace, select

**Create new policy**.Choose and configure controls, such as content filters, prompt shields, or abuse detection. Select

**Add control**after configuring each control.Select

**Next**to set the policy scope. The scope determines which resources the policy applies to. Choose a subscription to apply the policy broadly, or choose a specific resource group for targeted governance.Select

**Next**to add exceptions for model deployments or, if scoped to a subscription, resource groups. You can exclude specific model deployments or resource groups from the policy requirements. Use exceptions for testing environments or legacy deployments that can't meet new requirements.Select

**Next**when exceptions are complete.Enter a descriptive policy name. This name appears in the compliance dashboard.

Select

**Create**to finalize your guardrail policy.Allow up to 30 minutes for the guardrail policy to appear in the Foundry portal. Compliance results appear once Azure Policy completes its scan. The duration of the scan varies by scope size and resources.


After you create the guardrail policy, you see it listed in the **Policies** tab. The compliance status updates automatically as Azure Policy evaluates your resources.

### Edit a guardrail policy

To edit an existing guardrail policy, follow these steps:

In the compliance workspace, select the

**Policies**tab. Locate and select the guardrail policy you want to edit.Select

**Edit policy**from the guardrail policy details panel.Modify the controls, scope, or exceptions as needed.

Select

**Save**to apply your changes.Wait up to 30 minutes for the updated guardrail policy to take effect. Compliance results update once Azure Policy reevaluates your resources.


## Review guardrails across your subscription

When you monitor your model deployments for compliance, review and compare the different guardrail controls for your assets throughout a project or subscription. Even if the controls aren't directly linked to guardrail policy compliance, this process helps you spot gaps in guardrail policy assignments, like missing controls. You can also uncover potential risks that might go unnoticed - such as subscriptions lacking content filtering entirely.

Here's how you can do this:

In the compliance workspace, select the

**Guardrails**tab.Check that your scope is correct by reviewing and adjusting the subscription and project dropdowns as needed.

Examine the configurations across your projects, using column sorting to quickly find problems. For example, you can see which filters are disabled.

If you find a problem, choose one of these options:

**Option 1: Update individual deployments**- Select
**Build**from the upper-right navigation. - Select
**Guardrails**in the relevant project. - Update existing guardrail settings or add new ones for your model deployments.

**Option 2: Create a guardrail policy for enforcement**- In the compliance workspace, select the
**Policies**tab. - Create a new guardrail policy to enforce guardrail requirements across all deployments.

- Select

## Set up security recommendations and alerts

Microsoft Defender for Cloud provides security posture gaps and recommendations for remediation. Your security posture represents the overall security status of your Azure resources, including potential vulnerabilities, misconfigurations, and recommended improvements. Defender assesses your resources and workloads against built-in and custom security standards.

To get security posture recommendations from Microsoft Defender for Cloud, [enable it on your Azure subscription](/en-us/azure/defender-for-cloud/connect-azure-subscription). To get threat protection alerts for jailbreak attacks based on Foundry's user input attack risk detection, [enable threat protection for Foundry Tools](/en-us/azure/defender-for-cloud/ai-onboarding). Jailbreak attacks attempt to bypass AI safety measures by using carefully crafted prompts. Foundry detects these attack patterns in user input.

### Review your security recommendations

To review Defender security recommendations, follow these steps:

In the compliance workspace, select the

**Security**tab.[Enable Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/connect-azure-subscription)for your subscription if you need to do so.View recommendations in the

**Microsoft Defender for Cloud**section, including the affected resource and the associated risk level. Recommendations might include enabling additional security features, fixing misconfigurations, or addressing potential vulnerabilities in your AI deployments.Select a recommendation to view details and links to take action to remediate in Azure portal.


## Enable enterprise-grade data security and compliance for Foundry with Microsoft Purview [Preview]

Note

This feature requires a Microsoft Purview license in the tenant. To learn about Microsoft Purview, see [Microsoft Purview DSPM for AI](/en-us/purview/ai-microsoft-purview).

By enabling Microsoft Purview on your Azure subscription, you can access, process, and store prompt and response data – including associated metadata – from Microsoft Foundry apps and agents. This integration supports key data security and compliance scenarios such as:

- Microsoft Purview Audit
- Sensitive information type (SIT) classification
- Analytics and Reporting through Microsoft Purview DSPM for AI
- Insider Risk Management
- Communication Compliance
- Data Lifecycle Management
- eDiscovery

This capability helps your organization manage and monitor AI-generated data in alignment with enterprise policies and regulatory requirements.

Note

Purview Data Security Policies for Foundry Services interactions are supported for those API calls that use Microsoft Entra ID authentication with a user-context token, or for API calls that explicitly include user context. To learn more, see

[Gain end-user context for Azure AI API calls](../openai/latest?view=foundry#azureusersecuritycontext). For all other authentication scenarios, user interactions captured in Purview show up only in Purview Audit and AI Interactions with classifications within DSPM for AI Activity Explorer.Purview Audit is included as part of Microsoft Purview license for Foundry services. For data security policies setup in Purview by your enterprise security admins, billing is based on

[pay-as-you-go](https://azure.microsoft.com/pricing/details/purview/)meters.Integration with Purview for the above features in Microsoft Foundry doesn't yet support Network Isolation.

Integration with Purview is currently available only for calls made on the OpenAI Completions API.


### Enable Purview in Foundry

**Prerequisite:** You must have the **Azure AI Account Owner** role to enable Purview integration.

To enable Purview in Foundry:

Go to

**Operate**>**Compliance**.Select the

**Security posture**tab.Select the Azure subscription.

Enable

**Microsoft Purview**with the toggle.

Repeat the preceding steps for other Azure subscriptions, as appropriate.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/control-plane/register-custom-agent -->

# Register and manage custom agents

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Microsoft Foundry Control Plane provides centralized management and observability for agents running across different platforms and infrastructures. You can register custom agents—running in Azure compute services or other cloud environments—to gain visibility into their operations and control their behavior.

This article shows you how to register a custom agent in the Foundry Control Plane. You learn how to configure your agent for registration, set up telemetry collection, and use the Control Plane's management capabilities.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Prerequisites

Before getting started, make sure you have:

-
An Azure account with an active subscription. If you don't have one, create a

[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). A Foundry project. If you don't have one,

[create a project](../how-to/create-projects?view=foundry).

Foundry uses Azure API Management to register agents as APIs.

[Configure AI Gateway in your Foundry resource](../configuration/enable-ai-api-management-gateway-portal?view=foundry#create-an-ai-gateway).An agent that you deploy and expose through a reachable endpoint (either a public endpoint or an endpoint reachable from the network where you deploy the Foundry resource).


Note

This capability is available only in the Foundry (new) portal. Look for in the portal banner to confirm you're using Foundry (new).

## Add a custom agent

You can register a custom agent in the Control Plane. Develop the agent in the technology of your choice, both platform and infrastructure solutions.

When you register a custom agent, Foundry uses Azure API Management to act as a proxy for communications to your agent, so it can control access and monitor activity.

When you register a custom agent the resulting architecture is as follows:

### Verify your agent

Verify that your agent meets the requirements for registration:

- Your agent exposes an exclusive endpoint.
- The network where you deploy the Foundry resource can reach the agent's endpoint.
- The agent communicates by using one of the supported protocols: either general HTTP or specifically A2A.
- Your agent emits telemetry by using the OpenTelemetry semantic conventions for GenAI solutions (or you don't need this capability).
- You can configure the endpoint that end users use to communicate with the agent. Once an agent is registered in Control Plane, a new URL is generated.
**Clients and end users must use this URL to communicate with the agent**.

### Prepare your Foundry project

Custom agents are added to Foundry projects. Before registering the agent, let's make sure you configured the project correctly.

-
Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**. Ensure AI Gateway is configured in your project:

Select

**Operate**>**Admin console**.Open the

**AI Gateway**tab.The page lists all the AI Gateways configured and mapped to a Foundry resource. Check if the Foundry resource you want to use has an AI Gateway associated.

If the Foundry resource you want to use doesn't have an AI Gateway configured (it isn't listed), add one using the option

**Add AI Gateway**. AI Gateway is free to set up and unlocks powerful governance features like security, telemetry, and rate limits for your agents, tools, and models.For more details about how to configure AI Gateway, see

[Create an AI Gateway](../configuration/enable-ai-api-management-gateway-portal?view=foundry#create-an-ai-gateway).

Ensure you have observability configured in the project. Control Plane uses the Azure Application Insights resource associated with your selected project for emitting telemetry to help you diagnose your agent:

Select

**Operate**>**Admin console**.Under

**All projects**, use the search box to look for your project.Select the project.

Select the tab

**Connected resources**.Ensure there is a resource associated under the category

**Application Insights**.If there is no resource associated, add one by selecting

**Add connection**and select**Application Insights**.Your project is configured for observability and tracing.


### Register the agent

To register the agent, follow these steps:

Select

**Operate**from the upper-right navigation.Select the

**Overview**pane.Select

**Register agent**.The registration wizard appears. First, complete the details about the agent you want to register. The following properties describe the agent as it runs on its platform

Property Description Required **Agent URL**It represents the endpoint (URL) where your agent runs and receives requests. In general, but depending on your protocol, you indicate the base URL that your clients use. For example, if your agent talks OpenAI Chat Completions API, you indicate `https://<host>/v1/`

- without`/chat/completions`

as clients generally add it.Yes **Protocol**The communication protocol supported by your agent. Use HTTP in general, or if your agent supports more specifically A2A, indicate that one Yes **A2A agent card URL**Path to the agent card JSON specification. If you don't specify it, the system uses the default `/.well-known/agent-card.json`

.No **OpenTelemetry Agent ID**The Agent ID your agent uses to emit traces according to OpenTelemetry Generative AI semantic conventions. Traces indicate it in attribute `gen_ai.agents.id`

for spans with operation name`create_agent`

. If you don't specify this, the system uses the**Agent name**value to find traces and logs that this new agent reports.No **Admin portal URL**The administration portal URL where you can perform further administration operations for this agent. Foundry can store this value for easy access convenience. Foundry doesn't have any access to perform operations directly to such management portal. No Then, configure how you want the agent to show up in the Control Plane:

Property Description Required **Project**The project where you register the agent. Foundry uses the AI Gateway configured in the resource where the project lives to configure the inbound endpoint to the agent. You can only select projects with AI Gateway enabled in their resources. If you don't see any, [configure AI Gateway in your Foundry resource](../configuration/enable-ai-api-management-gateway-portal?view=foundry#create-an-ai-gateway). It's also advisable to configure Azure Application Insights in the selected project. Foundry uses the project's Azure Application Insights resource to sink traces and logs.Yes **Agent name**The name of the agent as you want it to appear in Foundry. The system might also use this name to find relevant traces and logs in Azure Application Insights if you don't specify a different value in the field **OpenTelemetry Agent ID**.Yes **Description**A clear description about this agent. No Save the changes.

Foundry adds the new agent. Select the

**Assets**tab in the left pane to check the list of agents.To show only custom agents, use the

**Source**filter and select**Custom**.

### Connect clients to the agent

When you register your agent in Foundry, you get a new URL for your clients to use. Foundry acts as a proxy for communications to your agent, so it can control access and monitor activity.

To distribute the new URL for your clients to call the agent:

Select the custom agent using the radio selector.

On the details panel on the right, under

**Agent URL**, select the copy option.Use the new URL to call the agent instead of the original endpoint.


In this example, you deploy a LangGraph agent and clients use the LangGraph SDK to consume it. The client uses the **new agent URL** value. This code creates a thread, sends a message asking about the weather, and streams the response back.

```
from langgraph_sdk import get_client
client = get_client(url="https://apim-my-foundry-resource.azure-api.net/my-custom-agent/")
async def stream_run():
thread = await client.threads.create()
input_data = {"messages": [{"role": "human", "content": "What's the weather in LA?"}]}
async for chunk in client.runs.stream(thread['thread_id'], assistant_id="your_assistant_id", input=input_data):
print(chunk)
```


**Expected output**: The agent processes the message and streams back responses as chunks. Each chunk contains partial results from the agent's execution, which might include tool calls to the weather function and the final response about Los Angeles weather.

Note

Foundry acts as a proxy for incoming requests for your agent. However, the original authorization and authentication schema in the original endpoint still applies. When you consume the new endpoint, **provide the same authentication mechanism as if you use the original endpoint.**

## Block and unblock the agent

For custom agents, Foundry doesn't have access to the underlying infrastructure where the agent runs, so start and stop operations aren't available. However, Foundry can block incoming requests to the agent, preventing clients from consuming it. This capability allows administrators to disable an agent if it misbehaves.

To block incoming requests to your agent:

Select

**Operate**from the upper-right navigation.Select

**Assets**in the left pane.Select the agent you want to block. The information panel appears.

Select

**Update status**and then select**Block**.Confirm the operation.


After you block the agent, the **Status** of the agent in Foundry shows as **Blocked**. Agents in the **Blocked** state run in their associated infrastructure but can't take incoming requests. Foundry blocks any attempt to interface with the agent.

To unblock the agent:

Select

**Update status**and then select**Unblock**.Confirm the operation.


## Enable telemetry for your agent

Foundry uses the OpenTelemetry open standard to understand what agents are doing. If your project has Azure Application Insights configured, Foundry logs requests into Azure Application Insights by default. This telemetry is also used to compute:

- Runs
- Error rate
- Usage (if available)

To get the best level of fidelity, Foundry expects custom agents to comply with the [semantic conventions for Generative AI solution in the OpenTelemetry standard](https://opentelemetry.io/docs/specs/semconv/gen-ai/).

### View runs and traces

You can view traces and logs sent to Foundry. To view them:

Select

**Operate**from the upper-right navigation.Select

**Assets**in the left pane.Select the agent.

**Traces**sections show up.You see one entry for each HTTP call made to the agent's endpoint.

To see the details, select an entry:

Tip

In this example, you can see how clients use the new agent's endpoint to communicate with the agent. The example shows an agent served with the Agent Protocol from LangChain. Clients use the route

`/runs/stream`

.Notice in this example that no further details besides the HTTP post are present in the trace. This is because no further instrumentation was added to the agent's code. See the next section to learn how to instrument your code and gain further details like tool calls, LLM calls, etc.


### Instrument custom code agents

If you build your agent with custom code, you need to instrument your solution to emit traces according to the OpenTelemetry standard and sink them to Azure Application Insights. Instrumentation allows Foundry to have access to higher level of detail about what your agent is doing.

Send traces to the Azure Application Insights resource of your project by using its instrumentation key. To get the instrumentation key associated with your project, follow the instructions at [Enable tracing in your project](../how-to/develop/trace-application?view=foundry#enable-tracing-in-your-project).

In this example, you configure an agent developed with LangGraph to emit traces in the OpenTelemetry standard. The tracer captures all agent operations, including tool calls and model interactions, and sends them to Azure Application Insights for monitoring.

This code uses [langchain-azure-ai](http://pypi.org/project/langchain-azure-ai) package. Learn how to instrument specific solutions with OpenTelemetry depending on the programming language and the framework used in your solution at [Language APIs & SDKs.](https://opentelemetry.io/docs/languages/).

```
pip install -U langchain-azure-ai[opentelemetry]
```


Then, instrument your agent:

```
from langchain.agents import create_agent
from langchain_azure_ai.callbacks.tracers import AzureAIOpenTelemetryTracer
application_insights_connection_string = 'InstrumentationKey="12345678...'
tracer = AzureAIOpenTelemetryTracer(
connection_string=application_insights_connection_string,
enable_content_recording=True,
)
def get_weather(city: str) -> str:
"""Get weather for a given city."""
return f"It's always sunny in {city}!"
agent = create_agent(
model="openai:gpt-5.1",
tools=[get_weather],
system_prompt="You are a helpful assistant",
).with_config({ "callbacks": [tracer] })
```


**Expected output**: The agent runs normally while automatically emitting OpenTelemetry traces to Azure Application Insights. Traces include operation names, durations, model calls, tool invocations, and token usage. You can view these traces in the Foundry portal under the Traces section.

Tip

You can pass the connection string to Azure Application Insights by using the environment variable `APPLICATIONINSIGHTS_CONNECTION_STRING`

.

### Instrumenting platform solutions

If your agent runs on a platform solution that supports OpenTelemetry but doesn't support Azure Application Insights, you need to deploy an OpenTelemetry Collector and configure your software to send OTLP data to the Collector (standard OpenTelemetry configuration).

Configure the Collector with the Azure Monitor exporter to forward data to Application Insights by using your connection string. For details about how to implement, see [Configure Azure Monitor OpenTelemetry](/en-us/azure/azure-monitor/app/opentelemetry-configuration).

### Troubleshooting traces

If you don't see traces, check the following:

- The project where you register your agent has Azure Application Insights configured. If you configured Azure Application Insights
**after**you registered the custom agent, you need to**unregister**the agent and register it again. Azure Application Insights configuration is not automatically updated after registration if changed. - You configure the agent (running on its infrastructure) to send traces to Azure Application Insights and you are using
**the same**Azure Application Insights resource than your project. - Instrumentation complies with OpenTelemetry semantic conventions for Generative AI.
- Traces include spans with attributes
`operation="create_agent"`

, and`gen_ai.agents.id="<agent-id>"`

or`gen_ai.agents.name="<agent-id>"`

; where`"<agent-id>"`

is the**OpenTelemetry Agent ID**you configure during registration.
