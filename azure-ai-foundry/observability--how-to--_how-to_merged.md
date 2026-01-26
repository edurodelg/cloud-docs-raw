---
merged_at: 2026-01-26T23:20:36.843823
merged_files: 7
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/observability/how-to/optimization-dashboard -->

# Monitoring dashboard insights in Microsoft Foundry with Ask AI (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

After your agent is in production, set up and view various metrics in the monitoring dashboard or control plane dashboard. Use Ask AI—the built-in chat assistant—to get a summary of your dashboard data and recommendations for next steps without leaving the Foundry portal.

This article describes the integrated user experience and system behavior for getting a dashboard summary or insights through Ask AI.

## Prerequisites

Before you begin:

- You have access to the
**Microsoft Foundry portal**. - You have one or more published agents.
- You have access to
**Ask AI**(the chat assistant).

## Start a chat with Ask AI

You can start a chat with Ask AI from any page in the Foundry portal.

Select the

**Ask AI**icon at the top of the page.Select one of the predefined prompts from the

*Ask AI*banner under*Build/Model/Monitor*,*Build/Agent/Monitor*, or overview page.

## Get a summary or insight of your dashboard

You can ask questions like:

- "Give me a summary of the dashboard"
- "Analyze the performance trend of my dashboard"

Or you can select a predefined prompt under the *Ask AI* banner, and the question is passed to Ask AI.

Ask AI provides highlights and abnormal behavior insights on your dashboard for the selected time period and provides an annotated link to the chart it refers to. When you select an annotated link, it scrolls directly to the chart with a highlighted background, making it easy to distinguish.

## Get recommended next steps

Ask any free-form questions related to your dashboard to get recommended next steps. Suggested action items include:

- "Investigate the cause of the latency increase on [the abnormal date] to ensure it isn't a recurring or growing issue."
- "Monitor whether future requests show similar latency patterns when usage increases."
- "Consider load testing or profiling to identify potential bottlenecks causing slower response times."
- "Optimize prompt and completion token usage to reduce load and costs as usage scales."
- "Monitor token consumption and request frequency trends for early signs of performance degradation."

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/observability/how-to/optimization-model-upgrade -->

# Upgrade/switch models in Microsoft Foundry with Ask AI (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

When new model versions are released or older versions are deprecated, use Ask AI—the built-in chat assistant—to detect, evaluate, and upgrade models without leaving the Foundry portal.

Ask AI provides conversational guidance, context-aware recommendations, and one-click actions for upgrading, evaluating, and deploying models.

This article describes the integrated user experience and system behavior when you initiate or manage model upgrades through Ask AI.

## Prerequisites

Before you begin:

- Have access to the
**Microsoft Foundry portal**. - Have one or more deployed models or agents.
- Have access to
**Ask AI**(the chat assistant). - Have at least one evaluation dataset in CSV or JSONL format.
- Have sufficient permission to deploy and evaluate.

## Start a chat with Ask AI

You can start a chat with Ask AI from any page in the Foundry portal.

- Select the
**Ask AI**icon at the top of the page. - Select one of the predefined prompts from the
**Ask AI**banner under*Build/Model/Monitor*or*Build/Agent/Monitor*page, or in Ask AI.

## Get recommendations on model replacement or upgrade

Ask AI questions like:

- "Is any model I’m using deprecated?"
- "Should I upgrade my model?"
- "What’s new in the latest GPT-5 version?"

It gives responses and options for recommended models. Select a model to view details in the model catalog, or go to the model deployment page to deploy a model. To learn how to deploy a model, see [Add and configure models to Foundry Models](../../foundry-models/how-to/create-model-deployments?view=foundry).

## Evaluate the new model and compare the performance

After deploying a new model, ask Ask AI to start an evaluation of the model using the same agent instructions and configurations. Either use the link provided by Ask AI and follow the steps in [creating a new evaluation](../../how-to/evaluate-generative-ai-app?view=foundry&preserve-view=true), or ask Ask AI to create it for you.

After the evaluation is complete, view the result on the evaluation detail page to check if the new model performs better than the current model. Use [compare](../../how-to/evaluate-results?view=foundry&preserve-view=true#compare-the-evaluation-results) or [cluster analysis](cluster-analysis?view=foundry) to gain deeper insights into the evaluation result.

If the new model isn't satisfactory, test other models and repeat the steps to create new evaluation runs. The new run is added to the evaluation when you create the first evaluation.

## Update your agent with the new model

To update your agent with the new model, chat with Ask AI to start the process or go to the Agent Playground page to update it manually. The new model updates the agent with a new version.

Chat with Ask AI to scan your project, find agents in similar situations, and apply the change to them.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/observability/how-to/human-evaluation -->

# Set up human evaluation for your agents (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

In this article, you’ll learn how to set up human evaluation for your Foundry agent. As an agent builder, you can create evaluation question templates focused on key aspects of interest and enable them to be answered for each agent response in the agent’s preview experience. This enables human evaluations by peers, data scientists, or compliance team members based on the defined templates. Once evaluations are completed, you can view and download the results directly from the Foundry portal for further analysis.

## Prerequisites

Before you begin:

- You have access to the
**Microsoft Foundry portal**. - You have one or more agents built.
- You have configured Application Insights for your project

## Create a human evaluation template

To begin human evaluation for your Foundry agent, you’ll first define a template that contains the set of questions you want human reviewers to complete based on agent responses.

### Steps to create a template

- Select the agent you want to evaluate from the agent table in the
**Agents**tab. - Navigate to the
**Human Evaluation**tab under**Evaluation**. - Select
**Create new template**to start the template creation process. - In the
**Create Human Evaluation Template**pop-up, assign a name and description, edit or delete sample questions, and add new questions based on your evaluation goals. Supported question types include thumbs up/down, slider, multiple choice, and free-form text. - After configuring the template, select
**Create**to finalize it.

## Manage your evaluation templates

You can create multiple evaluation templates based on your assessment needs. The template table allows you to edit, delete, and set templates as active or inactive.

### Manage templates

- You can edit a template using the
**Edit**button in the template table. The template opens in an editable pop-up for updates. - You can delete a template using the
**Delete**button in the template table.Note

Once deleted, the template and its associated evaluation results cannot be retrieved from the UI.

- To set a template as active, select
**Set as active**in the template table. Only one template can be active at any given time. Activating a new template automatically deactivates the previous one. You can also deactivate the current active template to stop capturing human evaluation results by selecting**Set as inactive**.

## Conduct human evaluation

Once the evaluation template is configured and set as active for the target agent, human reviewers can begin their evaluation using the preview web app functionality.

Note

Human reviewers need access to the Foundry project where the agent resides in to interact with the preview web app.

### Steps to conduct human evaluation

- Select
**Preview**in the top-right corner of the agent builder experience to open the agent in a web app interface. - Start testing the agent by entering input and selecting
**Send**to trigger an agent run. - After the agent responds, select the
**Feedback**button to provide human evaluation for that response.- A side panel appears, displaying the evaluation template configured by the agent builder.
- Reviewers can answer some or all questions in the form.

- When finished, select
**Save**to store the evaluation data for agent builders to review.- Select
**Cancel**to discard the answers.

- Select
- Continue evaluating additional responses by interacting with the agent for new outputs or navigating to previous responses.
- Reviewers can skip evaluations for certain responses or provide multiple evaluations for the same agent response as needed.


## Review human evaluation results

Once human reviewers have completed their evaluations, agent builders can preview and download the results for further analysis through the Foundry portal.

### Steps to review results

- Navigate to the template table within the
**Human Evaluation**tab and select the template you want to review results for. - After selecting a template, all corresponding evaluation results will appear under the
**Evaluation Results**section. Each instance is displayed with its timestamp for reference. - Select an evaluation instance to view its JSON summary in the
**JSON Output**section. The JSON includes:- Timestamp
- User prompt
- Agent response
- Questions from the evaluation template
- Reviewer answers

- To download all evaluation results for a template, select
**Download Results**after selecting the template. The results are exported as a CSV file containing all information from the JSON view for each evaluation instance.

Note

Evaluation data is stored in Application Insights and will follow its retention policy. Download and persist the data elsewhere if you need to keep it long term.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/observability/how-to/cluster-analysis -->

# Evaluation cluster analysis (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

After you run one or more evaluation runs, you can generate an evaluation cluster analysis to understand your evaluation results. This analysis provides an intuitive way to identify the top patterns and errors in your evaluation runs, along with recommended next steps to improve evaluator scores.

This article explains how to generate and interact with an evaluation cluster analysis.

## Prerequisites

Before you begin:

- Make sure you have access to the
**Microsoft Foundry portal**. - Ensure you have one or more deployed agents.
- Verify that you have one or more evaluation runs in one evaluation.

## Generate an evaluation cluster analysis

On the evaluation detail page, select one or more runs and then select **Cluster analysis**. A window appears and prompts you to select a model to generate the cluster analysis. It also shows an estimated time and tokens based on the samples selected from the evaluation runs.

## View cluster analysis

Cluster analysis provides an intuitive visualization of performance by grouping evaluation result samples with similar issues or response patterns. It helps you quickly identify recurring failure types, understand the distribution across error categories, and prioritize areas for improvement.

At the top of the view, summary statistics for the evaluation run are displayed:

- Total samples: Total number of evaluated responses (for example, 48).
- Clusters – Number of automatically identified clusters (for example, 2).
- Passed/failed: Breakdown of successful versus problematic samples.
- Avg Score – The overall average quality score for the run.
- Hover/click: Hovering over a dot or cluster label reveals detailed information, including example responses and evaluator feedback.

### Visualization

Each dot represents a sample from your evaluation dataset. Dots are grouped by semantic similarity, using embedding-based clustering of model outputs and feedback signals.

- Color: Indicates the cluster assignment (for example, inadequate final answer or incorrect response).
- Position: Samples closer together share similar characteristics or issues.

### Detail panel

#### Cluster

Selecting a cluster opens a side panel that includes:

- Selected cluster – Name of the top-level issue group.
- Entry count – Total number of samples within this cluster.
- Subclusters – Breakdown of related subcategories.
- Description – Automatically generated diagnostic summary explaining the likely cause or characteristic pattern
- Recommendations: Suggested next steps for mitigation or agent improvement.

#### Subcluster

Selecting a subcluster opens a side panel that includes:

- Cluster – Indicates the parent cluster this subcluster belongs to (for example, inadequate_final_answer).
- Selected subcluster – The specific subset being examined (for example, invalid_or_missing_api_key).
- Entry Count – Number of individual samples grouped under this subcluster.
- Tabs
- Analysis – Provides summary statistics, score averages, and qualitative insights (when available).
- Entries – Lists each sample (Entry ID) in the subcluster with their individual scores such as fluency, groundedness, or accuracy.


#### Entry ID

Selecting a dot / entry ID opens a side panel that includes:

- Cluster hierarchy
- Displays the full path of where this entry belongs: Cluster → Subcluster → Entry ID For example, inadequate_final_answer → invalid_or_missing_api_key → Entry ID: 17-fluency.

- Tabs
- Conversation – Shows the full text interaction for the selected sample:
- Context Summary (if applicable) – Any background or preceding context used in the evaluation.
- Query – The model prompt or user question (for example, "How do I submit an FSA reimbursement claim?").
- Response – The model’s generated output for that query.

- Metadata – Contains additional evaluation information such as scores, evaluators, timestamps, agent IDs, and trace IDs.

### Filter panel

The Filter Panel on the right side of the Cluster Analysis view allows users to customize how clusters are displayed and filtered for targeted inspection.

- Color by
- Lets you adjust how the samples are color-coded on the visualization.
- Options typically include:
- Cluster – Colors samples by top-level issue category.
- Subcluster – Colors samples by more granular subcategories within each cluster.
- Or evaluation result, evaluation type, score, and agent ID.


- Advanced filtering
- Provides tools to focus the visualization on specific subsets of data.
- You can define filters based on metadata or evaluation attributes.
- Select Parameter – Choose which field to filter on (for example, score, evaluator type, timestamp).
- Equal / Contains / Not equal – Define the condition for filtering.
- Select Value – Choose or input the specific value to match.
- Add Filter – Apply the condition to update the view dynamically.


## Download the analysis

To view the analysis offline, select **download** to get a copy of the analysis in CSV format and view it in other applications.

Note

The analysis result isn't stored. If you leave the page, the analysis result is lost.

## Next steps

The cluster analysis view helps you move from surface-level evaluation metrics to actionable insights. By combining semantic grouping, diagnostic summaries, and per-sample context, it bridges the gap between quantitative scoring and qualitative understanding.

Use the insights discovered here to:

- Refine prompts or models based on recurring issue patterns.
- Validate improvements after fine-tuning or retraining, and reevaluate to compare the old and new analysis results.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/observability/how-to/trace-agent-setup -->

# Set up tracing in Microsoft Foundry (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Tracing (preview) helps you understand how your agent works. Use traces to identify issues like latency spikes, runtime exceptions, incorrect prompts, and retrieval problems.

## Prerequisites

- A Foundry project. For more information, see
[Create a Foundry project](../../how-to/create-projects?view=foundry) - An
[Azure Monitor Application Insights resource](/en-us/azure/azure-monitor/app/app-insights-overview)to store traces (create a new one or connect an existing one). - Access to the Application Insights resource connected to your project.

Note

Agent tracing availability varies by region. For current limitations, see [Availability and limitations](../concepts/trace-agent-concept?view=foundry#availability-and-limitations).

## Connect Application Insights to your Foundry project

Foundry stores traces in [Azure Application Insights](/en-us/azure/azure-monitor/app/app-insights-overview) by using [OpenTelemetry semantic conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/).

- Sign in to
[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**. - Open your Foundry project.
- In the left navigation, select
**Tracing**. - Create or connect an Application Insights resource:
- To connect an existing resource, select the resource and then select
**Connect**. - To create a new resource, select**Create new**and complete the wizard.

After you connect the resource, your project is ready to use tracing.

Important

Make sure you have the permissions you need to query telemetry.

- For log-based queries, start by assigning the
[Log Analytics Reader role](/en-us/azure/azure-monitor/logs/manage-access?tabs=portal#log-analytics-reader). - To learn how to assign roles, see
[Assign Azure roles using the Azure portal](/en-us/azure/role-based-access-control/role-assignments-portal). - To manage access at scale, use
[Microsoft Entra groups](../../concepts/rbac-foundry?view=foundry#use-microsoft-entra-groups-with-foundry).

## Instrument AI agents

Choose the approach that matches how you build and run your agent.

### Server-side traces in the Foundry portal

Start with server-side traces. Foundry logs traces for common agent and workflow scenarios without changing your code.

- Foundry automatically logs server-side traces for Prompt agents, Host agents, and workflows in the Foundry portal. Once tracing is enabled in your Foundry project, you'll have access to out-of-the-box traces for the past 90 days.
- Foundry also allows for easy
[integration](trace-agent-framework?view=foundry)with top agent frameworks.

### Client-side traces with the Microsoft Foundry SDK (Python)

Install OpenTelemetry and the Azure SDK tracing plugin using:

```
pip install azure-ai-projects azure-identity opentelemetry-sdk azure-core-tracing-opentelemetry
```


Important

Using a project's endpoint in your application requires configuring Microsoft Entra ID. If you don't configure Microsoft Entra ID, use the Azure Application Insights connection string.

After running your agent, you can begin to [view and analyze traces in Foundry portal](#view-traces-in-the-foundry-portal).

For detailed instructions and SDK-specific code examples, see [Tracing with azure-ai-projects (Python SDK)](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/ai/azure-ai-projects#tracing) and [Telemetry samples for agents](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/ai/azure-ai-projects/samples/agents/telemetry).

### Trace locally with AI Toolkit in VS Code

AI Toolkit lets you trace locally in VS Code using a local OTLP-compatible collector, which is ideal for development and debugging.

The toolkit supports AI frameworks such as Foundry Agents Service, OpenAI, Anthropic, and LangChain through OpenTelemetry. You can see traces instantly in VS Code without needing cloud access.

For detailed setup instructions and SDK-specific code examples, see [Tracing in AI Toolkit](https://code.visualstudio.com/docs/intelligentapps/tracing).

## View and analyze traces

### View traces in the Foundry portal

In your Foundry project, go to the **Traces** tab in your agents or workflows. You can search, filter, or sort ingested traces from the last 90 days.

Select a trace to step through each span, identify issues, and observe how your application responds. This helps you debug and pinpoint issues in your application.

### View traces in Azure Monitor

Your traces are sent to Azure Monitor Application Insights, so you can view them there.

For more information on how to send traces to Azure Monitor and create an Azure Monitor resource, see [Azure Monitor OpenTelemetry documentation](/en-us/azure/azure-monitor/app/opentelemetry-enable).

### View conversation results

A **Conversation** is the persistent context of an end-to-end dialogue history between a user and an agent. In the Foundry portal, you can view **Conversation** results for your agent run out of the box along with traces on the **Traces** page.

You can search for a known Conversation ID, search by a Response ID, or search by a Trace ID that maps to this conversation. Then, select **Conversation ID** to review the conversation:

- Conversation history details
- Response information and tokens in a run
- Ordered actions, run steps, and tool calls
- Inputs and outputs between a user and an agent

## Verify tracing works

- Confirm your project is connected to Application Insights. If needed, follow the steps in
[Connect Application Insights to your Foundry project](#connect-application-insights-to-your-foundry-project). - Run your agent or workflow at least once (for example, by using the portal or your app).
- In your Foundry project, open the
**Traces**view and confirm a new trace appears.

If you don't see new traces, wait a few minutes and refresh, and then see [Troubleshooting](#troubleshooting).

## Security and privacy

Tracing can capture sensitive information (for example, user inputs, model outputs, and tool arguments and results). Use these practices to reduce risk:

- Don't store secrets, credentials, or tokens in prompts, tool arguments, or span attributes.
- Redact or minimize personal data and other sensitive content before it appears in telemetry.
- Treat trace data as production telemetry and apply the same access controls and retention policies you use for logs and metrics.

For more guidance, see [Security and privacy](../concepts/trace-agent-concept?view=foundry#security-and-privacy).

## Data retention and cost

Foundry stores traces in the Application Insights resource connected to your project. Data retention and billing follow your Application Insights and Log Analytics configuration.

## Troubleshooting

| Issue | Cause | Resolution |
|---|---|---|
| You don't see any traces in the Foundry portal | Tracing isn't connected, there is no recent traffic, or ingestion is delayed | Confirm the Application Insights connection, generate new agent traffic, and refresh after a few minutes. |
| You see authorization errors when you query or view telemetry | Missing RBAC permissions on Application Insights or Log Analytics | Confirm access in Access control (IAM) for the connected resources. For log queries, assign the
|
| Client-side traces don't appear | Instrumentation isn't installed or configured | Recheck your package installation and follow the SDK guidance linked in
|

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/observability/how-to/how-to-monitor-agents-dashboard -->

# Monitor AI agents with the Agent Monitoring Dashboard (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Use the Agent Monitoring Dashboard in Microsoft Foundry to track operational metrics and evaluation results for your agents. This dashboard helps you understand token usage, latency, success rates, and evaluation outcomes for production traffic.

## Prerequisites

- A Foundry project. For more information, see
[Create a Foundry project](../../how-to/create-projects?view=foundry). - At least one deployed agent in your Foundry project.
- An
[Azure Monitor Application Insights resource](/en-us/azure/azure-monitor/app/app-insights-overview)connected to your project. - Azure role-based access control (RBAC) access to the Application Insights resource. For log-based views, you might also need access to the associated Log Analytics workspace.

### Confirm you can view telemetry

To view data in the dashboard, make sure your account has access to the connected Application Insights resource.

In the Azure portal, open the Application Insights resource that's connected to your Foundry project.

Select

**Access control (IAM)**.Assign an appropriate role to your user or group.

If you use log-based views, start by granting the

[Log Analytics Reader role](/en-us/azure/azure-monitor/logs/manage-access?tabs=portal#log-analytics-reader).

## Connect Application Insights

The Agent Monitoring Dashboard reads telemetry from the Application Insights resource connected to your Foundry project. If you haven't connected Application Insights yet, follow the tracing setup steps and then return to this article.

## View agent metrics

To view metrics for an agent in the Foundry portal:

-
Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**. Navigate to the

**Build**page using the top navigation and select the agent you'd like to view data for.Select the

**Monitor**tab to view operational, evaluation, and red-teaming data for your agent.

The dashboard is designed for quick insights and deep analysis of your agent's performance. It consists of two main areas:

Summary cards at the top for high-level metrics.

Charts and graphs below for granular details. These visualizations reflect data for the selected time range.


## Understand the dashboard metrics

Use these definitions to interpret the dashboard:

**Token usage**: Token counts for agent traffic in the selected time range.**Latency**: Response time for agent runs.**Run success rate**: The percentage of runs that complete successfully.**Evaluation metrics**: Scores produced by evaluators that run on sampled agent outputs.**Red teaming results**: Outcomes from scheduled red team scans, if enabled.

## Data retention and cost

Monitoring data is stored in the connected Application Insights resource. Retention and billing follow your Application Insights configuration.

## Configure settings

Use the Monitor settings panel to configure telemetry, evaluations, and security checks for your agents. These settings control which charts the dashboard shows and which evaluations run.

The following table describes the monitoring features available in the Monitor Settings panel:

| Setting | Purpose | Configuration Options |
|---|---|---|
Continuous evaluation |
Runs evaluations on sampled agent responses. | Enable or disable Add evaluators Set the sample rate |
Scheduled evaluations |
Runs evaluations on a schedule to validate performance against benchmarks. | Enable or disable Select an evaluation template and run Set a schedule |
Red team scans |
Runs adversarial tests to detect risks such as data leakage or prohibited actions. | Enable or disable Select an evaluation template and run Set a schedule |
Alerts |
Detects performance anomalies, evaluation failures, and security risks. | Configure alerts for latency, token usage, evaluation scores, or red team findings |

## Set up continuous evaluation (Python SDK)

Use the Python SDK to set up continuous evaluation rules for agent responses.

```
pip install "azure-ai-projects>=2.0.0b1" python-dotenv
```


Set these environment variables with your own values:

`AZURE_AI_PROJECT_ENDPOINT`

: The Azure AI Project endpoint, as found on the project overview page in the Microsoft Foundry portal.`AZURE_AI_AGENT_NAME`

: The name of the AI agent to use for evaluation.`AZURE_AI_MODEL_DEPLOYMENT_NAME`

: The deployment name of the AI model.

### Assign permissions for continuous evaluation

To enable continuous evaluation rules, assign the project managed identity the **Azure AI User** role.

- In the Azure portal, open the resource for your Foundry project.
- Select
**Access control (IAM)**, and then select**Add**. - Create a role assignment for
**Azure AI User**. - For the member, select your Foundry project's managed identity.

### Create an agent

```
import os
from dotenv import load_dotenv
from azure.identity import DefaultAzureCredential
from azure.ai.projects import AIProjectClient
from azure.ai.projects.models import (
PromptAgentDefinition,
)
load_dotenv()
endpoint = os.environ["AZURE_AI_PROJECT_ENDPOINT"]
with (
DefaultAzureCredential() as credential,
AIProjectClient(endpoint=endpoint, credential=credential) as project_client,
project_client.get_openai_client() as openai_client,
):
agent = project_client.agents.create_version(
agent_name=os.environ["AZURE_AI_AGENT_NAME"],
definition=PromptAgentDefinition(
model=os.environ["AZURE_AI_MODEL_DEPLOYMENT_NAME"],
instructions="You are a helpful assistant that answers general questions",
),
)
print(f"Agent created (id: {agent.id}, name: {agent.name}, version: {agent.version})")
```


References: [AIProjectClient](/en-us/python/api/azure-ai-projects/azure.ai.projects.aiprojectclient), [DefaultAzureCredential](/en-us/python/api/azure-identity/azure.identity.defaultazurecredential)

### Create a continuous evaluation rule

Define the evaluation and the rule that runs when a response completes. To learn more about supported evaluators, see [What are evaluators?](../../concepts/observability?view=foundry#what-are-evaluators).

```
from azure.ai.projects.models import (
EvaluationRule,
ContinuousEvaluationRuleAction,
EvaluationRuleFilter,
EvaluationRuleEventType,
)
data_source_config = {"type": "azure_ai_source", "scenario": "responses"}
testing_criteria = [
{"type": "azure_ai_evaluator", "name": "violence_detection", "evaluator_name": "builtin.violence"}
]
eval_object = openai_client.evals.create(
name="Continuous Evaluation",
data_source_config=data_source_config, # type: ignore
testing_criteria=testing_criteria, # type: ignore
)
print(f"Evaluation created (id: {eval_object.id}, name: {eval_object.name})")
continuous_eval_rule = project_client.evaluation_rules.create_or_update(
id="my-continuous-eval-rule",
evaluation_rule=EvaluationRule(
display_name="My Continuous Eval Rule",
description="An eval rule that runs on agent response completions",
action=ContinuousEvaluationRuleAction(eval_id=eval_object.id, max_hourly_runs=100),
event_type=EvaluationRuleEventType.RESPONSE_COMPLETED,
filter=EvaluationRuleFilter(agent_name=agent.name),
enabled=True,
),
)
print(
f"Continuous Evaluation Rule created (id: {continuous_eval_rule.id}, name: {continuous_eval_rule.display_name})"
)
```


References: [EvaluationRuleEventType](/en-us/python/api/azure-ai-projects/azure.ai.projects.models.evaluationruleeventtype), [EvaluationRule](/en-us/python/api/azure-ai-projects/azure.ai.projects.models.evaluationrule)

## Verify continuous evaluation results

- Generate agent traffic (for example, run your app or test the agent in the portal).
- In the Foundry portal, open the agent and select
**Monitor**. - Review evaluation-related charts for the selected time range.

You can also list recent evaluation runs and open the report URL:

```
eval_run_list = openai_client.evals.runs.list(
eval_id=eval_object.id,
order="desc",
limit=10,
)
if len(eval_run_list.data) > 0 and eval_run_list.data[0].report_url:
print(f"Report URL: {eval_run_list.data[0].report_url}")
```


## Full sample code

To view the full sample code, see:

## Troubleshooting

| Issue | Cause | Resolution |
|---|---|---|
| Dashboard charts are empty | No recent traffic, time range excludes data, or ingestion delay | Generate new agent traffic, expand the time range, and refresh after a few minutes. |
| You see authorization errors | Missing RBAC permissions on Application Insights or Log Analytics | Confirm access in Access control (IAM) for the connected resources. For log access, assign the
|
| Continuous evaluation results don't appear | Continuous evaluation isn't enabled or rule creation failed | Confirm that your rule is enabled and that agent traffic is flowing. If you use the Python SDK setup, confirm the project managed identity has the Azure AI User role. |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/observability/how-to/trace-agent-framework -->

# Tracing integrations (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Microsoft Foundry makes it easy to capture agent traces with minimal code changes by using integrations with Microsoft Agent Framework, Semantic Kernel, LangChain, LangGraph, and OpenAI Agents SDK.

## Prerequisites

- A Foundry project. For more information, see
[Create a Foundry project](../../how-to/create-projects?view=foundry). - Tracing connected to an Azure Monitor Application Insights resource. To set it up, see
[Set up tracing in Microsoft Foundry](trace-agent-setup?view=foundry). - Access to the connected Application Insights resource. For log-based queries, you might also need access to the associated Log Analytics workspace.
- If you use LangChain or LangGraph, a Python environment.

### Confirm you can view telemetry

To view trace data, make sure your account has access to the connected Application Insights resource.

In the Azure portal, open the Application Insights resource connected to your Foundry project.

Select

**Access control (IAM)**.Assign an appropriate role to your user or group.

If you use log-based queries, start by granting the

[Log Analytics Reader role](/en-us/azure/azure-monitor/logs/manage-access?tabs=portal#log-analytics-reader).

Note

Agent tracing availability varies by region. For current limitations, see [Availability and limitations](../concepts/trace-agent-concept?view=foundry#availability-and-limitations).

## Security and privacy

Tracing can capture sensitive information (for example, user inputs, model outputs, and tool arguments and results).

- Enable content recording only when you need it. In the samples in this article, this is controlled by settings like
`enable_content_recording`

and`OTEL_RECORD_CONTENT`

. - Don't store secrets, credentials, or tokens in prompts or tool arguments.

For more guidance, see [Security and privacy](../concepts/trace-agent-concept?view=foundry#security-and-privacy).

## Microsoft Agent Framework

Foundry has native integrations with Microsoft Agent Framework. Agents built with Microsoft Agent Framework get out-of-the-box tracing in observability after you enable tracing for your Foundry project.

To learn more about tracing and observability in Microsoft Agent Framework, see [Microsoft Agent Framework Workflows - Observability](/en-us/agent-framework/user-guide/workflows/observability).

## Semantic Kernel

Foundry has native integrations with Semantic Kernel. Agents built with Semantic Kernel get out-of-the-box tracing in observability after you enable tracing for your Foundry project.

Learn more about tracing and observability in [Semantic Kernel](/en-us/semantic-kernel/concepts/enterprise-readiness/observability).

## LangChain & LangGraph

Note

Tracing integration for LangChain and LangGraph is currently available only in Python.
LangChain and LangGraph "v1" releases are currently under active development. API surface and tracing behavior can change as part of this release. Track updates at the [LangChain v1.0 release notes page](https://docs.langchain.com/oss/python/releases/langchain-v1).

Use the `langchain-azure-ai`

package to emit OpenTelemetry-compliant spans for LangChain and LangGraph operations so you can view rich traces in Foundry.

- OpenTelemetry semantic conventions:
[https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/](https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/) - Package and usage guidance:
[https://pypi.org/project/langchain-azure-ai/](https://pypi.org/project/langchain-azure-ai/)

### Sample: LangChain v1 agent with Azure AI tracing

Use this end-to-end sample to instrument a LangChain v1 agent using the `langchain-azure-ai`

tracer, which implements the latest OpenTelemetry (OTel) spec so you can view rich traces in Observability.

#### LangChain v1: Install packages

```
pip install \
langchain-azure-ai \
langchain \
langgraph \
langchain-openai \
azure-identity \
python-dotenv \
rich
```


#### LangChain v1: Configure environment

`APPLICATION_INSIGHTS_CONNECTION_STRING`

: Azure Monitor Application Insights connection string for tracing.`AZURE_OPENAI_ENDPOINT`

: Your Azure OpenAI endpoint URL.`AZURE_OPENAI_CHAT_DEPLOYMENT`

: The chat model deployment name.`AZURE_OPENAI_VERSION`

: API version, for example`2024-08-01-preview`

.- Azure credentials are resolved via
`DefaultAzureCredential`

(supports environment variables, managed identity, VS Code sign-in, etc.).

You can store these in a `.env`

file for local development.

#### LangChain v1: Tracer setup

```
from dotenv import load_dotenv
import os
from langchain_azure_ai.callbacks.tracers import AzureAIOpenTelemetryTracer
load_dotenv(override=True)
azure_tracer = AzureAIOpenTelemetryTracer(
connection_string=os.environ.get("APPLICATION_INSIGHTS_CONNECTION_STRING"),
enable_content_recording=True,
name="Weather information agent",
id="weather_info_agent_771929",
)
tracers = [azure_tracer]
```


#### LangChain v1: Model setup (Azure OpenAI)

```
import os
import azure.identity
from langchain_openai import AzureChatOpenAI
token_provider = azure.identity.get_bearer_token_provider(
azure.identity.DefaultAzureCredential(),
"https://cognitiveservices.azure.com/.default",
)
model = AzureChatOpenAI(
azure_endpoint=os.environ.get("AZURE_OPENAI_ENDPOINT"),
azure_deployment=os.environ.get("AZURE_OPENAI_CHAT_DEPLOYMENT"),
openai_api_version=os.environ.get("AZURE_OPENAI_VERSION"),
azure_ad_token_provider=token_provider,
)
```


#### LangChain v1: Define tools and prompt

```
from dataclasses import dataclass
from langchain_core.tools import tool
system_prompt = """You are an expert weather forecaster, who speaks in puns.
You have access to two tools:
- get_weather_for_location: use this to get the weather for a specific location
- get_user_location: use this to get the user's location
If a user asks you for the weather, make sure you know the location.
If you can tell from the question that they mean wherever they are,
use the get_user_location tool to find their location."""
# Mock user locations keyed by user id (string)
USER_LOCATION = {
"1": "Florida",
"2": "SF",
}
@dataclass
class UserContext:
user_id: str
@tool
def get_weather(city: str) -> str:
"""Get weather for a given city."""
return f"It's always sunny in {city}!"
```


#### LangChain v1: Use runtime context and define a user-info tool

```
from langgraph.runtime import get_runtime
from langchain_core.runnables import RunnableConfig
@tool
def get_user_info(config: RunnableConfig) -> str:
"""Retrieve user information based on user ID."""
runtime = get_runtime(UserContext)
user_id = runtime.context.user_id
return USER_LOCATION[user_id]
```


#### LangChain v1: Create the agent

```
from langchain.agents import create_agent
from langgraph.checkpoint.memory import InMemorySaver
from dataclasses import dataclass
@dataclass
class WeatherResponse:
conditions: str
punny_response: str
checkpointer = InMemorySaver()
agent = create_agent(
model=model,
prompt=system_prompt,
tools=[get_user_info, get_weather],
response_format=WeatherResponse,
checkpointer=checkpointer,
)
```


#### LangChain v1: Run the agent with tracing

```
from rich import print
def main():
config = {"configurable": {"thread_id": "1"}, "callbacks": [azure_tracer]}
context = UserContext(user_id="1")
r1 = agent.invoke(
{"messages": [{"role": "user", "content": "what is the weather outside?"}]},
config=config,
context=context,
)
print(r1.get("structured_response"))
r2 = agent.invoke(
{"messages": [{"role": "user", "content": "Thanks"}]},
config=config,
context=context,
)
print(r2.get("structured_response"))
if __name__ == "__main__":
main()
```


With `langchain-azure-ai`

enabled, all LangChain v1 operations (LLM calls, tool invocations, agent steps) are traced using the latest OpenTelemetry semantic conventions and appear in Observability, linked to your Application Insights resource.

### Sample: LangGraph agent with Azure AI tracing

This sample shows a simple LangGraph agent instrumented with `langchain-azure-ai`

to emit OpenTelemetry-compliant traces for graph steps, tool calls, and model invocations.

#### LangGraph: Install packages

```
pip install \
langchain-azure-ai \
langgraph==1.0.0a4 \
langchain==1.0.0a10 \
langchain-openai \
azure-identity \
python-dotenv
```


#### LangGraph: Configure environment

`APPLICATION_INSIGHTS_CONNECTION_STRING`

: Azure Monitor Application Insights connection string for tracing.`AZURE_OPENAI_ENDPOINT`

: Your Azure OpenAI endpoint URL.`AZURE_OPENAI_CHAT_DEPLOYMENT`

: The chat model deployment name.`AZURE_OPENAI_VERSION`

: API version, for example`2024-08-01-preview`

.

You can store these in a `.env`

file for local development.

#### LangGraph tracer setup

```
import os
from dotenv import load_dotenv
from langchain_azure_ai.callbacks.tracers import AzureAIOpenTelemetryTracer
load_dotenv(override=True)
azure_tracer = AzureAIOpenTelemetryTracer(
connection_string=os.environ.get("APPLICATION_INSIGHTS_CONNECTION_STRING"),
enable_content_recording=os.getenv("OTEL_RECORD_CONTENT", "true").lower() == "true",
name="Music Player Agent",
)
```


#### LangGraph: Tools

```
from langchain_core.tools import tool
@tool
def play_song_on_spotify(song: str):
"""Play a song on Spotify"""
# Integrate with Spotify API here.
return f"Successfully played {song} on Spotify!"
@tool
def play_song_on_apple(song: str):
"""Play a song on Apple Music"""
# Integrate with Apple Music API here.
return f"Successfully played {song} on Apple Music!"
tools = [play_song_on_apple, play_song_on_spotify]
```


#### LangGraph: Model setup (Azure OpenAI)

```
import os
import azure.identity
from langchain_openai import AzureChatOpenAI
token_provider = azure.identity.get_bearer_token_provider(
azure.identity.DefaultAzureCredential(),
"https://cognitiveservices.azure.com/.default",
)
model = AzureChatOpenAI(
azure_endpoint=os.environ.get("AZURE_OPENAI_ENDPOINT"),
azure_deployment=os.environ.get("AZURE_OPENAI_CHAT_DEPLOYMENT"),
openai_api_version=os.environ.get("AZURE_OPENAI_VERSION"),
azure_ad_token_provider=token_provider,
).bind_tools(tools, parallel_tool_calls=False)
```


#### Build the LangGraph workflow

```
from langgraph.graph import END, START, MessagesState, StateGraph
from langgraph.prebuilt import ToolNode
from langgraph.checkpoint.memory import MemorySaver
tool_node = ToolNode(tools)
def should_continue(state: MessagesState):
messages = state["messages"]
last_message = messages[-1]
return "continue" if getattr(last_message, "tool_calls", None) else "end"
def call_model(state: MessagesState):
messages = state["messages"]
response = model.invoke(messages)
return {"messages": [response]}
workflow = StateGraph(MessagesState)
workflow.add_node("agent", call_model)
workflow.add_node("action", tool_node)
workflow.add_edge(START, "agent")
workflow.add_conditional_edges(
"agent",
should_continue,
{
"continue": "action",
"end": END,
},
)
workflow.add_edge("action", "agent")
memory = MemorySaver()
app = workflow.compile(checkpointer=memory)
```


#### LangGraph: Run with tracing

```
from langchain_core.messages import HumanMessage
config = {"configurable": {"thread_id": "1"}, "callbacks": [azure_tracer]}
input_message = HumanMessage(content="Can you play Taylor Swift's most popular song?")
for event in app.stream({"messages": [input_message]}, config, stream_mode="values"):
event["messages"][-1].pretty_print()
```


With `langchain-azure-ai`

enabled, your LangGraph execution emits OpenTelemetry-compliant spans for model calls, tool invocations, and graph transitions. These traces flow to Application Insights and surface in Observability.

### Sample: LangChain 0.3 setup with Azure AI tracing

This minimal setup shows how to enable Azure AI tracing in a LangChain 0.3 application using the `langchain-azure-ai`

tracer and `AzureChatOpenAI`

.

#### LangChain 0.3: Install packages

```
pip install \
"langchain>=0.3,<0.4" \
langchain-openai \
langchain-azure-ai \
python-dotenv
```


#### LangChain 0.3: Configure environment

`APPLICATION_INSIGHTS_CONNECTION_STRING`

: Application Insights connection string for tracing.`AZURE_OPENAI_ENDPOINT`

: Azure OpenAI endpoint URL.`AZURE_OPENAI_CHAT_DEPLOYMENT`

: Chat model deployment name.`AZURE_OPENAI_VERSION`

: API version, for example`2024-08-01-preview`

.`AZURE_OPENAI_API_KEY`

: Azure OpenAI API key.

#### LangChain 0.3: Tracer and model setup

```
import os
from dotenv import load_dotenv
from langchain_azure_ai.callbacks.tracers import AzureAIOpenTelemetryTracer
from langchain_openai import AzureChatOpenAI
load_dotenv(override=True)
# Tracer: emits spans conforming to updated OTel spec
azure_tracer = AzureAIOpenTelemetryTracer(
connection_string=os.environ.get("APPLICATION_INSIGHTS_CONNECTION_STRING"),
enable_content_recording=True,
name="Trip Planner Orchestrator",
id="trip_planner_orchestrator_v3",
)
tracers = [azure_tracer]
# Model: Azure OpenAI with callbacks for tracing
llm = AzureChatOpenAI(
azure_deployment=os.environ.get("AZURE_OPENAI_CHAT_DEPLOYMENT"),
api_key=os.environ.get("AZURE_OPENAI_API_KEY"),
azure_endpoint=os.environ.get("AZURE_OPENAI_ENDPOINT"),
api_version=os.environ.get("AZURE_OPENAI_VERSION"),
temperature=0.2,
callbacks=tracers,
)
```


Attach `callbacks=[azure_tracer]`

to your chains, tools, or agents to ensure LangChain 0.3 operations are traced and visible in Observability.

## OpenAI Agents SDK

Use this snippet to configure OpenTelemetry tracing for the OpenAI Agents SDK and instrument the framework. It exports to Azure Monitor if `APPLICATION_INSIGHTS_CONNECTION_STRING`

is set; otherwise, it falls back to the console.

```
import os
from opentelemetry import trace
from opentelemetry.instrumentation.openai_agents import OpenAIAgentsInstrumentor
from opentelemetry.sdk.resources import Resource
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor, ConsoleSpanExporter
# Configure tracer provider + exporter
resource = Resource.create({
"service.name": os.getenv("OTEL_SERVICE_NAME", "openai-agents-app"),
})
provider = TracerProvider(resource=resource)
conn = os.getenv("APPLICATION_INSIGHTS_CONNECTION_STRING")
if conn:
from azure.monitor.opentelemetry.exporter import AzureMonitorTraceExporter
provider.add_span_processor(
BatchSpanProcessor(AzureMonitorTraceExporter.from_connection_string(conn))
)
else:
provider.add_span_processor(BatchSpanProcessor(ConsoleSpanExporter()))
trace.set_tracer_provider(provider)
# Instrument the OpenAI Agents SDK
OpenAIAgentsInstrumentor().instrument(tracer_provider=trace.get_tracer_provider())
# Example: create a session span around your agent run
tracer = trace.get_tracer(__name__)
with tracer.start_as_current_span("agent_session[openai.agents]"):
# ... run your agent here
pass
```


## Verify traces appear

- Sign in to
[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**. - Confirm tracing is connected for your project. If needed, follow
[Set up tracing in Microsoft Foundry](trace-agent-setup?view=foundry). - Run your agent at least once.
- In your Foundry project, open the traces view and confirm a new trace appears.

If you don't see new traces, wait a few minutes and refresh, and then see [Troubleshooting](#troubleshooting).

## Troubleshooting

| Issue | Cause | Resolution |
|---|---|---|
| You don't see traces in Foundry | Tracing isn't connected, there is no recent traffic, or ingestion is delayed | Confirm the Application Insights connection, generate new traffic, and refresh after a few minutes. |
| You don't see LangChain or LangGraph spans | Tracing callbacks aren't attached to the run | Confirm you pass the tracer in `callbacks` (for example, `config = {"callbacks": [azure_tracer]}` ) for the run you want to trace. |
| You see authorization errors when you query telemetry | Missing RBAC permissions on Application Insights or Log Analytics | Confirm access in Access control (IAM) for the connected resources. For log queries, assign the
|
| Sensitive content appears in traces | Content recording is enabled and prompts, tool arguments, or outputs include sensitive data | Disable content recording when you don't need it and redact sensitive data before it enters telemetry. |
