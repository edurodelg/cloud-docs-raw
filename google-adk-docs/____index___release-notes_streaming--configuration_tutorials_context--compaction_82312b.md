---
merged_at: 2026-01-30T23:51:11.584343
merged_files: 2
---


---
<!-- Source: N/A -->

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

---
<!-- Source: https://google.github.io/adk-docs/evaluate/criteria/ -->

# Evaluation Criteria¶

# Evaluation Criteria[¶](#evaluation-criteria)

This page outlines the evaluation criteria provided by ADK to assess agent performance, including tool use trajectory, response quality, and safety.

| Criterion | Description | Reference-Based | Requires Rubrics | LLM-as-a-Judge | Supports
|
|---|

`tool_trajectory_avg_score`

`response_match_score`

`final_response_match_v2`

`rubric_based_final_response_quality_v1`

`rubric_based_tool_use_quality_v1`

`hallucinations_v1`

`safety_v1`

`per_turn_user_simulator_quality_v1`

## tool_trajectory_avg_score[¶](#tool_trajectory_avg_score)

This criterion compares the sequence of tools called by the agent against a list
of expected calls and computes an average score based on one of the match types:
`EXACT`

, `IN_ORDER`

, or `ANY_ORDER`

.

#### When To Use This Criterion?[¶](#when-to-use-this-criterion)

This criterion is ideal for scenarios where agent correctness depends on tool
calls. Depending on how strictly tool calls need to be followed, you can choose
from one of three match types: `EXACT`

, `IN_ORDER`

, and `ANY_ORDER`

.

This metric is particularly valuable for:

**Regression testing:**Ensuring that agent updates do not unintentionally alter tool call behavior for established test cases.**Workflow validation:**Verifying that agents correctly follow predefined workflows that require specific API calls in a specific order.**High-precision tasks:**Evaluating tasks where slight deviations in tool parameters or call order can lead to significantly different or incorrect outcomes.

Use `EXACT`

match when you need to enforce a specific tool execution path and
consider any deviation—whether in tool name, arguments, or order—as a failure.

Use `IN_ORDER`

match when you want to ensure certain key tool calls occur in a
specific order, but allow for other tool calls to happen in between. This option is
useful in assuring if certain key actions or tool calls occur and in certain order,
leaving some scope for other tools calls to happen as well.

Use `ANY_ORDER`

match when you want to ensure certain key tool calls occur, but
do not care about their order, and allow for other tool calls to happen in
between. This criteria is helpful for cases where multiple tool calls about the
same concept occur, like your agent issues 5 search queries. You don't really
care the order in which the search queries are issued, till they occur.

#### Details[¶](#details)

For each invocation that is being evaluated, this criterion compares the list of tool calls produced by the agent against the list of expected tool calls using one of three match types. If the tool calls match based on the selected match type, a score of 1.0 is awarded for that invocation, otherwise the score is 0.0. The final value is the average of these scores across all invocations in the eval case.

The comparison can be done using one of following match types:

: Requires a perfect match between the actual and expected tool calls, with no extra or missing tool calls.`EXACT`

: Requires all tool calls from the expected list to be present in the actual list, in the same order, but allows for other tool calls to appear in between.`IN_ORDER`

: Requires all tool calls from the expected list to be present in the actual list, in any order, and allows for other tool calls to appear in between.`ANY_ORDER`


#### How To Use This Criterion?[¶](#how-to-use-this-criterion)

By default, `tool_trajectory_avg_score`

uses `EXACT`

match type. You can specify
just a threshold for this criterion in `EvalConfig`

under the `criteria`

dictionary for `EXACT`

match type. The value should be a float between 0.0 and
1.0, which represents the minimum acceptable score for the eval case to pass. If
you expect tool trajectories to match exactly in all invocations, you should set
the threshold to 1.0.

Example `EvalConfig`

entry for `EXACT`

match:

Or you could specify the `match_type`

explicitly:

If you want to use `IN_ORDER`

or `ANY_ORDER`

match type, you can specify it via
`match_type`

field along with threshold.

Example `EvalConfig`

entry for `IN_ORDER`

match:

Example `EvalConfig`

entry for `ANY_ORDER`

match:

#### Output And How To Interpret[¶](#output-and-how-to-interpret)

The output is a score between 0.0 and 1.0, where 1.0 indicates a perfect match between actual and expected tool trajectories for all invocations, and 0.0 indicates a complete mismatch for all invocations. Higher scores are better. A score below 1.0 means that for at least one invocation, the agent's tool call trajectory deviated from the expected one.

## response_match_score[¶](#response_match_score)

This criterion evaluates if agent's final response matches a golden/expected final response using Rouge-1.

### When To Use This Criterion?[¶](#when-to-use-this-criterion_1)

Use this criterion when you need a quantitative measure of how closely the agent's output matches the expected output in terms of content overlap.

### Details[¶](#details_1)

ROUGE-1 specifically measures the overlap of unigrams (single words) between the
system-generated text (candidate summary) and the a reference text. It
essentially checks how many individual words from the reference text are present
in the candidate text. To learn more, see details on
[ROUGE-1](https://github.com/google-research/google-research/tree/master/rouge).

### How To Use This Criterion?[¶](#how-to-use-this-criterion_1)

You can specify a threshold for this criterion in `EvalConfig`

under the
`criteria`

dictionary. The value should be a float between 0.0 and 1.0, which
represents the minimum acceptable score for the eval case to pass.

Example `EvalConfig`

entry:

### Output And How To Interpret[¶](#output-and-how-to-interpret_1)

Value range for this criterion is [0,1], with values closer to 1 more desirable.

## final_response_match_v2[¶](#final_response_match_v2)

This criterion evaluates if the agent's final response matches a golden/expected final response using LLM as a judge.

### When To Use This Criterion?[¶](#when-to-use-this-criterion_2)

Use this criterion when you need to evaluate the correctness of an agent's final
response against a reference, but require flexibility in how the answer is
presented. It is suitable for cases where different phrasings or formats are
acceptable, as long as the core meaning and information match the reference.
This criterion is a good choice for evaluating question-answering,
summarization, or other generative tasks where semantic equivalence is more
important than exact lexical overlap, making it a more sophisticated alternative
to `response_match_score`

.

### Details[¶](#details_2)

This criterion uses a Large Language Model (LLM) as a judge to determine if the
agent's final response is semantically equivalent to the provided reference
response. It is designed to be more flexible than lexical matching metrics (like
`response_match_score`

), as it focuses on whether the agent's response contains
the correct information, while tolerating differences in formatting, phrasing,
or the inclusion of additional correct details.

For each invocation, the criterion prompts a judge LLM to rate the agent's
response as "valid" or "invalid" compared to the reference. This is repeated
multiple times for robustness (configurable via `num_samples`

), and a majority
vote determines if the invocation receives a score of 1.0 (valid) or 0.0
(invalid). The final criterion score is the fraction of invocations deemed valid
across the entire eval case.

### How To Use This Criterion?[¶](#how-to-use-this-criterion_2)

This criterion uses `LlmAsAJudgeCriterion`

, allowing you to configure the
evaluation threshold, the judge model, and the number of samples per invocation.

Example `EvalConfig`

entry:

{
"criteria": {
"final_response_match_v2": {
"threshold": 0.8,
"judge_model_options": {
"judge_model": "gemini-2.5-flash",
"num_samples": 5
}
}
}
}
}


### Output And How To Interpret[¶](#output-and-how-to-interpret_2)

The criterion returns a score between 0.0 and 1.0. A score of 1.0 means the LLM judge considered the agent's final response to be valid for all invocations, while a score closer to 0.0 indicates that many responses were judged as invalid when compared to the reference responses. Higher values are better.

## rubric_based_final_response_quality_v1[¶](#rubric_based_final_response_quality_v1)

This criterion assesses the quality of an agent's final response against a user-defined set of rubrics using LLM as a judge.

### When To Use This Criterion?[¶](#when-to-use-this-criterion_3)

Use this criterion when you need to evaluate aspects of response quality that go beyond simple correctness or semantic equivalence with a reference. It is ideal for assessing nuanced attributes like tone, style, helpfulness, or adherence to specific conversational guidelines defined in your rubrics. This criterion is particularly useful when no single reference response exists, or when quality depends on multiple subjective factors.

### Details[¶](#details_3)

This criterion provides a flexible way to evaluate response quality based on specific criteria that you define as rubrics. For example, you could define rubrics to check if a response is concise, if it correctly infers user intent, or if it avoids jargon.

The criterion uses an LLM-as-a-judge to evaluate the agent's final response
against each rubric, producing a `yes`

(1.0) or `no`

(0.0) verdict for each.
Like other LLM-based metrics, it samples the judge model multiple times per
invocation and uses a majority vote to determine the score for each rubric in
that invocation. The overall score for an invocation is the average of its
rubric scores. The final criterion score for the eval case is the average of
these overall scores across all invocations.

### How To Use This Criterion?[¶](#how-to-use-this-criterion_3)

This criterion uses `RubricsBasedCriterion`

, which requires a list of rubrics to
be provided in the `EvalConfig`

. Each rubric should be defined with a unique ID
and its content.

Example `EvalConfig`

entry:

{
"criteria": {
"rubric_based_final_response_quality_v1": {
"threshold": 0.8,
"judge_model_options": {
"judge_model": "gemini-2.5-flash",
"num_samples": 5
},
"rubrics": [
{
"rubric_id": "conciseness",
"rubric_content": {
"text_property": "The agent's response is direct and to the point."
}
},
{
"rubric_id": "intent_inference",
"rubric_content": {
"text_property": "The agent's response accurately infers the user's underlying goal from ambiguous queries."
}
}
]
}
}
}


### Output And How To Interpret[¶](#output-and-how-to-interpret_3)

The criterion outputs an overall score between 0.0 and 1.0, where 1.0 indicates that the agent's responses satisfied all rubrics across all invocations, and 0.0 indicates that no rubrics were satisfied. The results also include detailed per-rubric scores for each invocation. Higher values are better.

## rubric_based_tool_use_quality_v1[¶](#rubric_based_tool_use_quality_v1)

This criterion assesses the quality of an agent's tool usage against a user-defined set of rubrics using LLM as a judge.

### When To Use This Criterion?[¶](#when-to-use-this-criterion_4)

Use this criterion when you need to evaluate *how* an agent uses tools, rather
than just *if* the final response is correct. It is ideal for assessing whether
the agent selected the right tool, used the correct parameters, or followed a
specific sequence of tool calls. This is useful for validating agent reasoning
processes, debugging tool-use errors, and ensuring adherence to prescribed
workflows, especially in cases where multiple tool-use paths could lead to a
similar final answer but only one path is considered correct.

### Details[¶](#details_4)

This criterion provides a flexible way to evaluate tool usage based on specific rules that you define as rubrics. For example, you could define rubrics to check if a specific tool was called, if its parameters were correct, or if tools were called in a particular order.

The criterion uses an LLM-as-a-judge to evaluate the agent's tool calls and
responses against each rubric, producing a `yes`

(1.0) or `no`

(0.0) verdict for
each. Like other LLM-based metrics, it samples the judge model multiple times
per invocation and uses a majority vote to determine the score for each rubric
in that invocation. The overall score for an invocation is the average of its
rubric scores. The final criterion score for the eval case is the average of
these overall scores across all invocations.

### How To Use This Criterion?[¶](#how-to-use-this-criterion_4)

This criterion uses `RubricsBasedCriterion`

, which requires a list of rubrics to
be provided in the `EvalConfig`

. Each rubric should be defined with a unique ID
and its content, describing a specific aspect of tool use to evaluate.

Example `EvalConfig`

entry:

{
"criteria": {
"rubric_based_tool_use_quality_v1": {
"threshold": 1.0,
"judge_model_options": {
"judge_model": "gemini-2.5-flash",
"num_samples": 5
},
"rubrics": [
{
"rubric_id": "geocoding_called",
"rubric_content": {
"text_property": "The agent calls the GeoCoding tool before calling the GetWeather tool."
}
},
{
"rubric_id": "getweather_called",
"rubric_content": {
"text_property": "The agent calls the GetWeather tool with coordinates derived from the user's location."
}
}
]
}
}
}


### Output And How To Interpret[¶](#output-and-how-to-interpret_4)

The criterion outputs an overall score between 0.0 and 1.0, where 1.0 indicates that the agent's tool usage satisfied all rubrics across all invocations, and 0.0 indicates that no rubrics were satisfied. The results also include detailed per-rubric scores for each invocation. Higher values are better.

## hallucinations_v1[¶](#hallucinations_v1)

This criterion assesses whether a model response contains any false, contradictory, or unsupported claims.

### When To Use This Criterion?[¶](#when-to-use-this-criterion_5)

Use this criterion to ensure the agent's response is grounded in the provided context (e.g., tool outputs, user query, instructions) and does not contain hallucinations.

### Details[¶](#details_5)

This criterion assesses whether a model response contains any false, contradictory, or unsupported claims based on context that includes developer instructions, user prompt, tool definitions, and tool invocations and their results. It uses LLM-as-a-judge and follows a two-step process:

**Segmenter**: Segments the agent response into individual sentences.**Sentence Validator**: Evaluates each segmented sentence against the provided context for grounding. Each sentence is labeled as`supported`

,`unsupported`

,`contradictory`

,`disputed`

or`not_applicable`

.

The metric computes an Accuracy Score: the percentage of sentences that are
`supported`

or `not_applicable`

. By default, only the final response is
evaluated. If `evaluate_intermediate_nl_responses`

is set to true in the
criterion, intermediate natural language responses from agents are also
evaluated.

### How To Use This Criterion?[¶](#how-to-use-this-criterion_5)

This criterion uses `HallucinationsCriterion`

, allowing you to configure the
evaluation threshold, the judge model, the number of samples per invocation and
whether to evaluate intermediate natural language responses.

Example `EvalConfig`

entry:

{
"criteria": {
"hallucinations_v1": {
"threshold": 0.8,
"judge_model_options": {
"judge_model": "gemini-2.5-flash",
},
"evaluate_intermediate_nl_responses": true
}
}
}


### Output And How To Interpret[¶](#output-and-how-to-interpret_5)

The criterion returns a score between 0.0 and 1.0. A score of 1.0 means all sentences in agent's response are grounded in the context, while a score closer to 0.0 indicates that many sentences are false, contradictory, or unsupported. Higher values are better.

## safety_v1[¶](#safety_v1)

This criterion evaluates the safety (harmlessness) of an Agent's Response.

### When To Use This Criterion?[¶](#when-to-use-this-criterion_6)

This criterion should be used when you need to ensure that agent responses comply with safety guidelines and do not produce harmful or inappropriate content. It is essential for user-facing applications or any system where response safety is a priority.

### Details[¶](#details_6)

This criterion assesses whether the agent's response contains any harmful
content, such as hate speech, harassment, or dangerous information. Unlike other
metrics implemented natively within ADK, `safety_v1`

delegates the evaluation to
the Vertex AI General AI Eval SDK.

### How To Use This Criterion?[¶](#how-to-use-this-criterion_6)

Using this criterion requires a Google Cloud Project. You must have
`GOOGLE_CLOUD_PROJECT`

and `GOOGLE_CLOUD_LOCATION`

environment variables set,
typically in an `.env`

file in your agent's directory, for the Vertex AI SDK to
function correctly.

You can specify a threshold for this criterion in `EvalConfig`

under the
`criteria`

dictionary. The value should be a float between 0.0 and 1.0,
representing the minimum safety score for a response to be considered passing.

Example `EvalConfig`

entry:

### Output And How To Interpret[¶](#output-and-how-to-interpret_6)

The criterion returns a score between 0.0 and 1.0. Scores closer to 1.0 indicate that the response is safe, while scores closer to 0.0 indicate potential safety issues.

## per_turn_user_simulator_quality_v1[¶](#per_turn_user_simulator_quality_v1)

This criterion evaluates whether a user simulator is faithful to a conversation plan.

#### When To Use This Criterion?[¶](#when-to-use-this-criterion_7)

Use this criterion when you need to evaluate a user simulator in a multi-turn
conversation. It is designed to assess whether the simulator follows the
conversation plan defined in the `ConversationScenario`

.

#### Details[¶](#details_7)

This criterion determines whether the a user simulator follows a defined
`ConversationScenario`

in a multi-turn conversation.

For the first turn, this criterion checks if user simulator response matches the
`starting_prompt`

in the `ConversationScenario`

. For subsequent turns, it uses
LLM-as-a-judge to evaluate if the user response follows the `conversation_plan`

in the `ConversationScenario`

.

#### How To Use This Criterion?[¶](#how-to-use-this-criterion_7)

This criterion allows you to configure the evaluation threshold, the judge model
and the number of samples per invocation. The criterion also lets you specify a
`stop_signal`

, which signals the LLM judge that the conversation was completed.
For best results, use the stop signal in `LlmBackedUserSimulator`

.

Example `EvalConfig`

entry:

{
"criteria": {
"per_turn_user_simulator_quality_v1": {
"threshold": 1.0,
"judge_model_options": {
"judge_model": "gemini-2.5-flash",
"num_samples": 5
},
"stop_signal": "</finished>"
}
}
}


#### Output And How To Interpret[¶](#output-and-how-to-interpret_7)

The criterion returns a score between 0.0 and 1.0, representing the fraction of turns in which the user simulator's response was judged to be valid according to the conversation scenario. A score of 1.0 indicates that the simulator behaved as expected in all turns, while a score closer to 0.0 indicates that the simulator deviated in many turns. Higher values are better.
