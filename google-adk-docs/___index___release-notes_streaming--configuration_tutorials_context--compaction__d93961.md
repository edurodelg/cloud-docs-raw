---
merged_at: 2026-01-28T07:23:42.228712
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/ -->

# Agent Development Kit

Agent Development Kit (ADK) is a flexible and modular framework for **developing
and deploying AI agents**. While optimized for Gemini and the Google ecosystem,
ADK is **model-agnostic**, **deployment-agnostic**, and is built for
**compatibility with other frameworks**. ADK was designed to make agent
development feel more like software development, to make it easier for
developers to create, deploy, and orchestrate agentic architectures that range
from simple tasks to complex workflows.

Get started:

[Start with Python](/adk-docs/get-started/python/)
[Start with TypeScript](/adk-docs/get-started/typescript/)
[Start with Go](/adk-docs/get-started/go/)
[Start with Java](/adk-docs/get-started/java/)

## Learn more[¶](#learn-more)

[ Watch "Introducing Agent Development Kit"!](https://www.youtube.com/watch?v=zgrOwow_uTQ)

-
**Flexible Orchestration**

Define workflows using workflow agents (

`Sequential`

,`Parallel`

,`Loop`

) for predictable pipelines, or leverage LLM-driven dynamic routing (`LlmAgent`

transfer) for adaptive behavior. -
**Multi-Agent Architecture**

Build modular and scalable applications by composing multiple specialized agents in a hierarchy. Enable complex coordination and delegation.

-
**Rich Tool Ecosystem**

Equip agents with diverse capabilities: use pre-built tools (Search, Code Exec), create custom functions, integrate 3rd-party libraries, or even use other agents as tools.

-
**Deployment Ready**

Containerize and deploy your agents anywhere – run locally, scale with Vertex AI Agent Engine, or integrate into custom infrastructure using Cloud Run or Docker.

-
**Built-in Evaluation**

Systematically assess agent performance by evaluating both the final response quality and the step-by-step execution trajectory against predefined test cases.

-
**Building Safe and Secure Agents**

Learn how to building powerful and trustworthy agents by implementing security and safety patterns and best practices into your agent's design.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/release-notes/ -->

# ADK release notes¶

# ADK release notes[¶](#adk-release-notes)

You can find the release notes in the code repositories for each supported language. For detailed information on ADK releases, see these locations:

You can find the release notes in the code repositories for each supported language. For detailed information on ADK releases, see these locations:

---
<!-- Source: https://google.github.io/adk-docs/streaming/configuration/ -->

# Configuring streaming behaviour¶

# Configuring streaming behaviour[¶](#configuring-streaming-behaviour)

Supported in ADKPython v0.5.0Experimental

There are some configurations you can set for live(streaming) agents.

It's set by [RunConfig](https://github.com/google/adk-python/blob/main/src/google/adk/agents/run_config.py). You should use RunConfig with your [Runner.run_live(...)](https://github.com/google/adk-python/blob/main/src/google/adk/runners.py).

For example, if you want to set voice config, you can leverage speech_config.

---
<!-- Source: https://google.github.io/adk-docs/tutorials/ -->

# Build your agent with ADK¶

# Build your agent with ADK[¶](#build-your-agent-with-adk)

Get started with the Agent Development Kit (ADK) through our collection of practical guides. These tutorials are designed in a simple, progressive, step-by-step fashion, introducing you to different ADK features and capabilities.

This approach allows you to learn and build incrementally – starting with foundational concepts and gradually tackling more advanced agent development techniques. You'll explore how to apply these features effectively across various use cases, equipping you to build your own sophisticated agentic applications with ADK. Explore our collection below and happy building:

-
**Multi-tool agent**

Create a workflow that uses multiple tools.

-
**Agent team**

Build an multi-agent workflow including agent delegation, session management, and safety callbacks.

-
**Streaming agent**

Create an agent for handling streamed content.

-
**Discover sample agents**

Discover sample agents for retail, travel, customer service, and more!

---
<!-- Source: https://google.github.io/adk-docs/context/compaction/ -->

# Compress agent context for performance¶

# Compress agent context for performance[¶](#compress-agent-context-for-performance)

As an ADK agent runs it collects *context* information, including user
instructions, retrieved data, tool responses, and generated content. As the size
of this context data grows, agent processing times typically also increase.
More and more data is sent to the generative AI model used by the agent,
increasing processing time and slowing down responses. The ADK Context
Compaction feature is designed to reduce the size of context as an agent
is running by summarizing older parts of the agent workflow event history.

The Context Compaction feature uses a *sliding window* approach for collecting
and summarizing agent workflow event data within a
[Session](/adk-docs/sessions/session/). When you configure this feature in your
agent, it summarizes data from older events once it reaches a threshold of a
specific number of workflow events, or invocations, with the current Session.

## Configure context compaction[¶](#configure-context-compaction)

Add context compaction to your agent workflow by adding an Events Compaction Configuration setting to the App object of your workflow. As part of the configuration, you must specify a compaction interval and overlap size, as shown in the following sample code:

from google.adk.apps.app import App
from google.adk.apps.app import EventsCompactionConfig
app = App(
name='my-agent',
root_agent=root_agent,
events_compaction_config=EventsCompactionConfig(
compaction_interval=3, # Trigger compaction every 3 new invocations.
overlap_size=1 # Include last invocation from the previous window.
),
)


Once configured, the ADK `Runner`

handles the compaction process in the
background each time the session reaches the interval.

## Example of context compaction[¶](#example-of-context-compaction)

If you set `compaction_interval`

to 3 and `overlap_size`

to 1, the event data is
compressed upon completion of events 3, 6, 9, and so on. The overlap setting
increases size of the second summary compression, and each summary afterwards,
as shown in Figure 1.

**Figure 1.** Ilustration of event compaction configuration with a interval of 3
and overlap of 1.

With this example configuration, the context compression tasks happen as follows:

**Event 3 completes**: All 3 events are compressed into a summary**Event 6 completes**: Events 3 to 6 are compressed, including the overlap of 1 prior event**Event 9 completes**: Events 6 to 9 are compressed, including the overlap of 1 prior event

## Configuration settings[¶](#configuration-settings)

The configuration settings for this feature control how frequently event data is compressed and how much data is retained as the agent workflow runs. Optionally, you can configure a compactor object

: Set the number of completed events that triggers compaction of the prior event data.`compaction_interval`

: Set how many of the previously compacted events are included in a newly compacted context set.`overlap_size`

: (Optional) Define a summarizer object including a specific AI model to use for summarization. For more information, see`summarizer`

[Define a Summarizer](#define-summarizer).

### Define a Summarizer[¶](#define-summarizer)

You can customize the process of context compression by defining a summarizer. The LlmEventSummarizer class allows you to specify a particular model for summarization. The following code example demonstrates how to define and configure a custom summarizer:

from google.adk.apps.app import App, EventsCompactionConfig
from google.adk.apps.llm_event_summarizer import LlmEventSummarizer
from google.adk.models import Gemini
# Define the AI model to be used for summarization:
summarization_llm = Gemini(model="gemini-2.5-flash")
# Create the summarizer with the custom model:
my_summarizer = LlmEventSummarizer(llm=summarization_llm)
# Configure the App with the custom summarizer and compaction settings:
app = App(
name='my-agent',
root_agent=root_agent,
events_compaction_config=EventsCompactionConfig(
compaction_interval=3,
overlap_size=1,
summarizer=my_summarizer,
),
)


You can further refine the operation of the `SlidingWindowCompactor`

by
by modifying its summarizer class `LlmEventSummarizer`

including changing
the `prompt_template`

setting of that class. For more details, see the
[ LlmEventSummarizer code](https://github.com/google/adk-python/blob/main/src/google/adk/apps/llm_event_summarizer.py#L60).

---
<!-- Source: https://google.github.io/adk-docs/callbacks/design-patterns-and-best-practices/ -->

# Design Patterns and Best Practices for Callbacks¶

# Design Patterns and Best Practices for Callbacks[¶](#design-patterns-and-best-practices-for-callbacks)

Callbacks offer powerful hooks into the agent lifecycle. Here are common design patterns illustrating how to leverage them effectively in ADK, followed by best practices for implementation.

## Design Patterns[¶](#design-patterns)

These patterns demonstrate typical ways to enhance or control agent behavior using callbacks:

### 1. Guardrails & Policy Enforcement[¶](#guardrails-policy-enforcement)

**Pattern Overview:**
Intercept requests before they reach the LLM or tools to enforce rules.

**Implementation:**
- Use `before_model_callback`

to inspect the `LlmRequest`

prompt
- Use `before_tool_callback`

to inspect tool arguments
- If a policy violation is detected (e.g., forbidden topics, profanity):
- Return a predefined response (`LlmResponse`

or `dict`

/`Map`

) to block the operation
- Optionally update `context.state`

to log the violation

**Example Use Case:**
A `before_model_callback`

checks `llm_request.contents`

for sensitive keywords and returns a standard "Cannot process this request" `LlmResponse`

if found, preventing the LLM call.

### 2. Dynamic State Management[¶](#dynamic-state-management)

**Pattern Overview:**
Read from and write to session state within callbacks to make agent behavior context-aware and pass data between steps.

**Implementation:**
- Access `callback_context.state`

or `tool_context.state`

- Modifications (`state['key'] = value`

) are automatically tracked in the subsequent `Event.actions.state_delta`

- Changes are persisted by the `SessionService`


**Example Use Case:**
An `after_tool_callback`

saves a `transaction_id`

from the tool's result to `tool_context.state['last_transaction_id']`

. A later `before_agent_callback`

might read `state['user_tier']`

to customize the agent's greeting.

### 3. Logging and Monitoring[¶](#logging-and-monitoring)

**Pattern Overview:**
Add detailed logging at specific lifecycle points for observability and debugging.

**Implementation:**
- Implement callbacks (e.g., `before_agent_callback`

, `after_tool_callback`

, `after_model_callback`

)
- Print or send structured logs containing:
- Agent name
- Tool name
- Invocation ID
- Relevant data from the context or arguments

**Example Use Case:**
Log messages like `INFO: [Invocation: e-123] Before Tool: search_api - Args: {'query': 'ADK'}`

.

### 4. Caching[¶](#caching)

**Pattern Overview:**
Avoid redundant LLM calls or tool executions by caching results.

**Implementation Steps:**
1. **Before Operation:** In `before_model_callback`

or `before_tool_callback`

:
- Generate a cache key based on the request/arguments
- Check `context.state`

(or an external cache) for this key
- If found, return the cached `LlmResponse`

or result directly

**After Operation:**If cache miss occurred:- Use the corresponding
`after_`

callback to store the new result in the cache using the key

**Example Use Case:**
`before_tool_callback`

for `get_stock_price(symbol)`

checks `state[f"cache:stock:{symbol}"]`

. If present, returns the cached price; otherwise, allows the API call and `after_tool_callback`

saves the result to the state key.

### 5. Request/Response Modification[¶](#request-response-modification)

**Pattern Overview:**
Alter data just before it's sent to the LLM/tool or just after it's received.

**Implementation Options:**
- ** before_model_callback:** Modify

`llm_request`

(e.g., add system instructions based on `state`

)
- **Modify the returned**

`after_model_callback`

:`LlmResponse`

(e.g., format text, filter content)
- **Modify the tool**

`before_tool_callback`

:`args`

dictionary (or Map in Java)
- **Modify the**

`after_tool_callback`

:`tool_response`

dictionary (or Map in Java)**Example Use Case:**
`before_model_callback`

appends "User language preference: Spanish" to `llm_request.config.system_instruction`

if `context.state['lang'] == 'es'`

.

### 6. Conditional Skipping of Steps[¶](#conditional-skipping-of-steps)

**Pattern Overview:**
Prevent standard operations (agent run, LLM call, tool execution) based on certain conditions.

**Implementation:**
- Return a value from a `before_`

callback to skip the normal execution:
- `Content`

from `before_agent_callback`

- `LlmResponse`

from `before_model_callback`

- `dict`

from `before_tool_callback`

- The framework interprets this returned value as the result for that step

**Example Use Case:**
`before_tool_callback`

checks `tool_context.state['api_quota_exceeded']`

. If `True`

, it returns `{'error': 'API quota exceeded'}`

, preventing the actual tool function from running.

### 7. Tool-Specific Actions (Authentication & Summarization Control)[¶](#tool-specific-actions-authentication-summarization-control)

**Pattern Overview:**
Handle actions specific to the tool lifecycle, primarily authentication and controlling LLM summarization of tool results.

**Implementation:**
Use `ToolContext`

within tool callbacks (`before_tool_callback`

, `after_tool_callback`

):

**Authentication:**Call`tool_context.request_credential(auth_config)`

in`before_tool_callback`

if credentials are required but not found (e.g., via`tool_context.get_auth_response`

or state check). This initiates the auth flow.**Summarization:**Set`tool_context.actions.skip_summarization = True`

if the raw dictionary output of the tool should be passed back to the LLM or potentially displayed directly, bypassing the default LLM summarization step.

**Example Use Case:**
A `before_tool_callback`

for a secure API checks for an auth token in state; if missing, it calls `request_credential`

. An `after_tool_callback`

for a tool returning structured JSON might set `skip_summarization = True`

.

### 8. Artifact Handling[¶](#artifact-handling)

**Pattern Overview:**
Save or load session-related files or large data blobs during the agent lifecycle.

**Implementation:**
- **Saving:** Use `callback_context.save_artifact`

/ `await tool_context.save_artifact`

to store data:
- Generated reports
- Logs
- Intermediate data
- **Loading:** Use `load_artifact`

to retrieve previously stored artifacts
- **Tracking:** Changes are tracked via `Event.actions.artifact_delta`


**Example Use Case:**
An `after_tool_callback`

for a "generate_report" tool saves the output file using `await tool_context.save_artifact("report.pdf", report_part)`

. A `before_agent_callback`

might load a configuration artifact using `callback_context.load_artifact("agent_config.json")`

.

## Best Practices for Callbacks[¶](#best-practices-for-callbacks)

### Design Principles[¶](#design-principles)

**Keep Focused:**
Design each callback for a single, well-defined purpose (e.g., just logging, just validation). Avoid monolithic callbacks.

**Mind Performance:**
Callbacks execute synchronously within the agent's processing loop. Avoid long-running or blocking operations (network calls, heavy computation). Offload if necessary, but be aware this adds complexity.

### Error Handling[¶](#error-handling)

**Handle Errors Gracefully:**
- Use `try...except/catch`

blocks within your callback functions
- Log errors appropriately
- Decide if the agent invocation should halt or attempt recovery
- Don't let callback errors crash the entire process

### State Management[¶](#state-management)

**Manage State Carefully:**
- Be deliberate about reading from and writing to `context.state`

- Changes are immediately visible within the *current* invocation and persisted at the end of the event processing
- Use specific state keys rather than modifying broad structures to avoid unintended side effects
- Consider using state prefixes (`State.APP_PREFIX`

, `State.USER_PREFIX`

, `State.TEMP_PREFIX`

) for clarity, especially with persistent `SessionService`

implementations

### Reliability[¶](#reliability)

**Consider Idempotency:**
If a callback performs actions with external side effects (e.g., incrementing an external counter), design it to be idempotent (safe to run multiple times with the same input) if possible, to handle potential retries in the framework or your application.

### Testing & Documentation[¶](#testing-documentation)

**Test Thoroughly:**
- Unit test your callback functions using mock context objects
- Perform integration tests to ensure callbacks function correctly within the full agent flow

**Ensure Clarity:**
- Use descriptive names for your callback functions
- Add clear docstrings explaining their purpose, when they run, and any side effects (especially state modifications)

**Use Correct Context Type:**
Always use the specific context type provided (`CallbackContext`

for agent/model, `ToolContext`

for tools) to ensure access to the appropriate methods and properties.

By applying these patterns and best practices, you can effectively use callbacks to create more robust, observable, and customized agent behaviors in ADK.
