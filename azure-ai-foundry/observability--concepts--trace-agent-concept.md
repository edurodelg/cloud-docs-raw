---
source_url: https://learn.microsoft.com/en-us/azure/ai-foundry/observability/concepts/trace-agent-concept
fetched_at: 2026-01-25T15:27:37.517268
---

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