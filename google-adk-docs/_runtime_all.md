---
merged_at: 2026-02-01T07:56:59.219881
merged_files: 7
---


---
<!-- Source: https://google.github.io/adk-docs/runtime/ -->

# Agent Runtime¶

# Agent Runtime[¶](#agent-runtime)

Supported in ADKPython v0.1.0TypeScript v0.2.0Go v0.1.0Java v0.1.0

ADK provides several ways to run and test your agents during development. Choose the method that best fits your development workflow.

## Ways to run agents[¶](#ways-to-run-agents)

-
**Dev UI**

Use

`adk web`

to launch a browser-based interface for interacting with your agents. -
**Command Line**

Use

`adk run`

to interact with your agents directly in the terminal. -
**API Server**

Use

`adk api_server`

to expose your agents through a RESTful API.

## Technical reference[¶](#technical-reference)

For more in-depth information on runtime configuration and behavior, see these pages:

: Understand the core event loop that powers ADK, including the yield/pause/resume cycle.[Event Loop](event-loop/): Learn how to resume agent execution from a previous state.[Resume Agents](resume/): Configure runtime behavior with RunConfig.[Runtime Config](runconfig/)

---
<!-- Source: https://google.github.io/adk-docs/runtime/web-interface/ -->

# Use the Web Interface¶

# Use the Web Interface[¶](#use-the-web-interface)

The ADK web interface lets you test your agents directly in the browser. This tool provides a simple way to interactively develop and debug your agents.

Caution: ADK Web for development only

ADK Web is ** not meant for use in production deployments**. You should
use ADK Web for development and debugging purposes only.

## Start the web interface[¶](#start-the-web-interface)

Use the following command to run your agent in the ADK web interface:

Make sure to update the port number.

With Maven, compile and run the ADK web server:

With Gradle, the `build.gradle`

or `build.gradle.kts`

build file should have the following Java plugin in its plugins section:

tasks.register('runADKWebServer', JavaExec) {
dependsOn classes
classpath = sourceSets.main.runtimeClasspath
mainClass = 'com.google.adk.web.AdkWebServer'
args '--adk.agents.source-dir=src/main/java/agents', '--server.port=8080'
}


Finally, on the command-line, run the following command:

In Java, the Web Interface and the API server are bundled together.

The server starts on `http://localhost:8000`

by default:

+-----------------------------------------------------------------------------+
| ADK Web Server started |
| |
| For local testing, access at http://localhost:8000. |
+-----------------------------------------------------------------------------+


## Features[¶](#features)

Key features of the ADK web interface include:

**Chat interface**: Send messages to your agents and view responses in real-time**Session management**: Create and switch between sessions**State inspection**: View and modify session state during development**Event history**: Inspect all events generated during agent execution

## Common options[¶](#common-options)

| Option | Description | Default |
|---|---|---|
`--port` |
Port to run the server on | `8000` |
`--host` |
Host binding address | `127.0.0.1` |
`--session_service_uri` |
Custom session storage URI | In-memory |
`--artifact_service_uri` |
Custom artifact storage URI | Local `.adk/artifacts` |
`--reload/--no-reload` |
Enable auto-reload on code changes | `true` |

---
<!-- Source: https://google.github.io/adk-docs/runtime/command-line/ -->

# Use the Command Line¶

# Use the Command Line[¶](#use-the-command-line)

ADK provides an interactive terminal interface for testing your agents. This is useful for quick testing, scripted interactions, and CI/CD pipelines.

## Run an agent[¶](#run-an-agent)

Use the following command to run your agent in the ADK command line interface:

Create an `AgentCliRunner`

class (see [Java Quickstart](../../get-started/java/)) and run:

This starts an interactive session where you can type queries and see agent responses directly in your terminal:

Running agent my_agent, type exit to exit.
[user]: What's the weather in New York?
[my_agent]: The weather in New York is sunny with a temperature of 25°C.
[user]: exit


## Session options[¶](#session-options)

The `adk run`

command includes options for saving, resuming, and replaying
sessions.

### Save sessions[¶](#save-sessions)

To save the session when you exit:

You'll be prompted to enter a session ID, and the session will be saved to
`path/to/my_agent/<session_id>.session.json`

.

You can also specify the session ID upfront:

### Resume sessions[¶](#resume-sessions)

To continue a previously saved session:

This loads the previous session state and event history, displays it, and allows you to continue the conversation.

### Replay sessions[¶](#replay-sessions)

To replay a session file without interactive input:

The input file should contain initial state and queries:

## Storage options[¶](#storage-options)

| Option | Description | Default |
|---|---|---|
`--session_service_uri` |
Custom session storage URI | SQLite under `.adk/session.db` |
`--artifact_service_uri` |
Custom artifact storage URI | Local `.adk/artifacts` |

### Example with storage options[¶](#example-with-storage-options)

## All options[¶](#all-options)

| Option | Description |
|---|---|
`--save_session` |
Save the session to a JSON file on exit |
`--session_id` |
Session ID to use when saving |
`--resume` |
Path to a saved session file to resume |
`--replay` |
Path to an input file for non-interactive replay |
`--session_service_uri` |
Custom session storage URI |
`--artifact_service_uri` |
Custom artifact storage URI |

---
<!-- Source: https://google.github.io/adk-docs/runtime/resume/ -->

# Resume stopped agents¶

# Resume stopped agents[¶](#resume-stopped-agents)

An ADK agent's execution can be interrupted by various factors including dropped network connections, power failure, or a required external system going offline. The Resume feature of ADK allows an agent workflow to pick up where it left off, avoiding the need to restart the entire workflow. In ADK Python 1.16 and higher, you can configure an ADK workflow to be resumable, so that it tracks the execution of workflow and then allows you to resume it after an unexpected interruption.

This guide explains how to configure your ADK agent workflow to be resumable.
If you use Custom Agents, you can update them to be resumable. For more
information, see
[Add resume to custom Agents](#custom-agents).

## Add resumable configuration[¶](#add-resumable-configuration)

Enable the Resume function for an agent workflow by applying a Resumability configuration to the App object of your ADK workflow, as shown in the following code example:

app = App(
name='my_resumable_agent',
root_agent=root_agent,
# Set the resumability config to enable resumability.
resumability_config=ResumabilityConfig(
is_resumable=True,
),
)


Caution: Long Running Functions, Confirmations, Authentication

For agents that use
[Long Running Functions](/adk-docs/tools-custom/function-tools/#long-run-tool),
[Confirmations](/adk-docs/tools-custom/confirmation/), or
[Authentication](/adk-docs/tools-custom/authentication/)
requiring user input, adding a resumable confirmation changes how these features
operate. For more information, see the documentation for those features.

Note: Custom Agents

Resume is not supported by default for Custom Agents. You must
update the agent code for a Custom Agent to support the Resume feature. For
information on modifying Custom Agents to support incremental resume
functionality, see
[Add resume to custom Agents](#custom-agents).

## Resume a stopped workflow[¶](#resume-a-stopped-workflow)

When an ADK workflow stops execution you can resume the workflow using a
command containing the Invocation ID for the workflow instance, which can be
found in the
[Event](/adk-docs/events/#understanding-and-using-events)
history of the workflow. Make sure the ADK API server is running, in case it was
interrupted or powered off, and then run the following command to resume the
workflow, as shown in the following API request example.

# restart the API server if needed:
adk api_server my_resumable_agent/
# resume the agent:
curl -X POST http://localhost:8000/run_sse \
-H "Content-Type: application/json" \
-d '{
"app_name": "my_resumable_agent",
"user_id": "u_123",
"session_id": "s_abc",
"invocation_id": "invocation-123",
}'


You can also resume a workflow using the Runner object Run Async method, as shown below:

runner.run_async(user_id='u_123', session_id='s_abc',
invocation_id='invocation-123')
# When new_message is set to a function response,
# we are trying to resume a long running function.


Note

Resuming a workflow from the ADK Web user interface or using the ADK command line (CLI) tool is not currently supported.

## How it works[¶](#how-it-works)

The Resume feature works by logging completed Agent workflow tasks,
including incremental steps using
[Events](/adk-docs/events/) and
[Event Actions](/adk-docs/events/#detecting-actions-and-side-effects).
tracking completion of agent tasks within a resumable workflow. If a workflow is
interrupted and then later restarted, the system resumes the workflow by setting
the completion state of each agent. If an agent did not complete, the workflow
system reinstates any completed Events for that agent, and restarts the workflow
from the partially completed state. For multi-agent workflows, the specific
resume behavior varies, based on the multi-agent classes in your workflow, as
described below:

**Sequential Agent**: Reads the current_sub_agent from its saved state to find the next sub-agent to run in the sequence.**Loop Agent**: Uses the current_sub_agent and times_looped values to continue the loop from the last completed iteration and sub-agent.**Parallel Agent**: Determines which sub-agents have already completed and only runs those that have not finished.

Event logging includes results from Tools which successfully returned a result. So if an agent successfully executed Function Tools A and B, and then failed during execution of tool C, the system reinstates the results from the tools A and B, and resumes the workflow by re-running the tool C request.

Caution: Tool execution behavior

When resuming a workflow with Tools, the Resume feature ensures
that the Tools in an agent are run ** at least once**, and may run more than
once when resuming a workflow. If your agent uses Tools where duplicate runs
would have a negative impact, such as purchases, you should modify the Tool to
check for and prevent duplicate runs.

Note: Workflow modification with Resume not supported

Do not modify a stopped agent workflow before resuming it. For example adding or removing agents from workflow that has stopped and then resuming that workflow is not supported.

## Add resume to custom Agents[¶](#custom-agents)

Custom agents have specific implementation requirements in order to support resumability. You must decide on and define workflow steps within your custom agent which produce a result which can be preserved before handing off to the next step of processing. The following steps outline how to modify a Custom Agent to support a workflow Resume.

**Create CustomAgentState class**: Extend the BaseAgentState to create an object that preserves the state of your agent.**Optionally, create WorkFlowStep class**: If your custom agent has sequential steps, consider creating a WorkFlowStep list object that defines the discrete, savable steps of the agent.

**Add initial agent state:**Modify your agent's async run function to set the initial state of your agent.**Add agent state checkpoints**: Modify your agent's async run function to generate and save the agent state for each completed step of the agent's overall task.**Add end of agent status to track agent state:**Modify your agent's async run function to include an`end_of_agent=True`

status upon successful completion of the agent's full task.

The following example shows the required code modifications to the example
StoryFlowAgent class shown in the
[Custom Agents](/adk-docs/agents/custom-agents/#full-code-example)
guide:

class WorkflowStep(int, Enum):
INITIAL_STORY_GENERATION = 1
CRITIC_REVISER_LOOP = 2
POST_PROCESSING = 3
CONDITIONAL_REGENERATION = 4
# Extend BaseAgentState
### class StoryFlowAgentState(BaseAgentState):
### step = WorkflowStep
@override
async def _run_async_impl(
self, ctx: InvocationContext
) -> AsyncGenerator[Event, None]:
"""
Implements the custom orchestration logic for the story workflow.
Uses the instance attributes assigned by Pydantic (e.g., self.story_generator).
"""
agent_state = self._load_agent_state(ctx, WorkflowStep)
if agent_state is None:
# Record the start of the agent
agent_state = StoryFlowAgentState(step=WorkflowStep.INITIAL_STORY_GENERATION)
yield self._create_agent_state_event(ctx, agent_state)
next_step = agent_state.step
logger.info(f"[{self.name}] Starting story generation workflow.")
# Step 1. Initial Story Generation
if next_step <= WorkflowStep.INITIAL_STORY_GENERATION:
logger.info(f"[{self.name}] Running StoryGenerator...")
async for event in self.story_generator.run_async(ctx):
yield event
# Check if story was generated before proceeding
if "current_story" not in ctx.session.state or not ctx.session.state[
"current_story"
]:
return # Stop processing if initial story failed
agent_state = StoryFlowAgentState(step=WorkflowStep.CRITIC_REVISER_LOOP)
yield self._create_agent_state_event(ctx, agent_state)
# Step 2. Critic-Reviser Loop
if next_step <= WorkflowStep.CRITIC_REVISER_LOOP:
logger.info(f"[{self.name}] Running CriticReviserLoop...")
async for event in self.loop_agent.run_async(ctx):
logger.info(
f"[{self.name}] Event from CriticReviserLoop: "
f"{event.model_dump_json(indent=2, exclude_none=True)}"
)
yield event
agent_state = StoryFlowAgentState(step=WorkflowStep.POST_PROCESSING)
yield self._create_agent_state_event(ctx, agent_state)
# Step 3. Sequential Post-Processing (Grammar and Tone Check)
if next_step <= WorkflowStep.POST_PROCESSING:
logger.info(f"[{self.name}] Running PostProcessing...")
async for event in self.sequential_agent.run_async(ctx):
logger.info(
f"[{self.name}] Event from PostProcessing: "
f"{event.model_dump_json(indent=2, exclude_none=True)}"
)
yield event
agent_state = StoryFlowAgentState(step=WorkflowStep.CONDITIONAL_REGENERATION)
yield self._create_agent_state_event(ctx, agent_state)
# Step 4. Tone-Based Conditional Logic
if next_step <= WorkflowStep.CONDITIONAL_REGENERATION:
tone_check_result = ctx.session.state.get("tone_check_result")
if tone_check_result == "negative":
logger.info(f"[{self.name}] Tone is negative. Regenerating story...")
async for event in self.story_generator.run_async(ctx):
logger.info(
f"[{self.name}] Event from StoryGenerator (Regen): "
f"{event.model_dump_json(indent=2, exclude_none=True)}"
)
yield event
else:
logger.info(f"[{self.name}] Tone is not negative. Keeping current story.")
logger.info(f"[{self.name}] Workflow finished.")
yield self._create_agent_state_event(ctx, end_of_agent=True)

---
<!-- Source: https://google.github.io/adk-docs/runtime/runconfig/ -->

# Runtime Configuration¶

# Runtime Configuration[¶](#runtime-configuration)

`RunConfig`

defines runtime behavior and options for agents in ADK. It controls
speech and streaming settings, function calling, artifact saving, and limits on
LLM calls.

When constructing an agent run, you can pass a `RunConfig`

to customize how the
agent interacts with models, handles audio, and streams responses. By default,
no streaming is enabled and inputs aren’t retained as artifacts. Use `RunConfig`

to override these defaults.

## Class Definition[¶](#class-definition)

The `RunConfig`

class holds configuration parameters for an agent's runtime behavior.

- Python ADK uses Pydantic for this validation.
- Go ADK has mutable structs by default.
-
Java ADK typically uses immutable data classes.

-
TypeScript ADK uses a standard interface, with type safety provided by the TypeScript compiler.


class RunConfig(BaseModel):
"""Configs for runtime behavior of agents."""
model_config = ConfigDict(
extra='forbid',
)
speech_config: Optional[types.SpeechConfig] = None
response_modalities: Optional[list[str]] = None
save_input_blobs_as_artifacts: bool = False
support_cfc: bool = False
streaming_mode: StreamingMode = StreamingMode.NONE
output_audio_transcription: Optional[types.AudioTranscriptionConfig] = None
max_llm_calls: int = 500


export interface RunConfig {
speechConfig?: SpeechConfig;
responseModalities?: Modality[];
saveInputBlobsAsArtifacts: boolean;
supportCfc: boolean;
streamingMode: StreamingMode;
outputAudioTranscription?: AudioTranscriptionConfig;
maxLlmCalls: number;
// ... and other properties
}
export enum StreamingMode {
NONE = 'none',
SSE = 'sse',
BIDI = 'bidi',
}


type StreamingMode string
const (
StreamingModeNone StreamingMode = "none"
StreamingModeSSE StreamingMode = "sse"
)
// RunConfig controls runtime behavior.
type RunConfig struct {
// Streaming mode, None or StreamingMode.SSE.
StreamingMode StreamingMode
// Whether or not to save the input blobs as artifacts
SaveInputBlobsAsArtifacts bool
}


public abstract class RunConfig {
public enum StreamingMode {
NONE,
SSE,
BIDI
}
public abstract @Nullable SpeechConfig speechConfig();
public abstract ImmutableList<Modality> responseModalities();
public abstract boolean saveInputBlobsAsArtifacts();
public abstract @Nullable AudioTranscriptionConfig outputAudioTranscription();
public abstract int maxLlmCalls();
// ...
}


## Runtime Parameters[¶](#runtime-parameters)

| Parameter | Python Type | TypeScript Type | Go Type | Java Type | Default (Py / TS / Go / Java) | Description |
|---|---|---|---|---|---|---|
`speech_config` |
`Optional[types.SpeechConfig]` |
`SpeechConfig` (optional) |
N/A | `SpeechConfig` (nullable via `@Nullable` ) |
`None` / `undefined` / N/A / `null` |
Configures speech synthesis (voice, language) using the `SpeechConfig` type. |
`response_modalities` |
`Optional[list[str]]` |
`Modality[]` (optional) |
N/A | `ImmutableList<Modality>` |
`None` / `undefined` / N/A / Empty `ImmutableList` |
List of desired output modalities (e.g., Python: `["TEXT", "AUDIO"]` ; Java/TS: uses structured `Modality` objects). |
`save_input_blobs_as_artifacts` |
`bool` |
`boolean` |
`bool` |
`boolean` |
`False` / `false` / `false` / `false` |
If `true` , saves input blobs (e.g., uploaded files) as run artifacts for debugging/auditing. |
`streaming_mode` |
`StreamingMode` |
`StreamingMode` |
`StreamingMode` |
`StreamingMode` |
`StreamingMode.NONE` / `StreamingMode.NONE` / `agent.StreamingModeNone` / `StreamingMode.NONE` |
Sets the streaming behavior: `NONE` (default), `SSE` (server-sent events), or `BIDI` (bidirectional). |
`output_audio_transcription` |
`Optional[types.AudioTranscriptionConfig]` |
`AudioTranscriptionConfig` (optional) |
N/A | `AudioTranscriptionConfig` (nullable via `@Nullable` ) |
`None` / `undefined` / N/A / `null` |
Configures transcription of generated audio output using the `AudioTranscriptionConfig` type. |
`max_llm_calls` |
`int` |
`number` |
N/A | `int` |
`500` / `500` / N/A / `500` |
Limits total LLM calls per run. `0` or negative means unlimited. Exceeding language limits (e.g. `sys.maxsize` , `Number.MAX_SAFE_INTEGER` ) raises an error. |
`support_cfc` |
`bool` |
`boolean` |
N/A | `bool` |
`False` / `false` / N/A / `false` |
Python/TypeScript: Enables Compositional Function Calling. Requires `streaming_mode=SSE` and uses the LIVE API. Experimental. |

`speech_config`

[¶](#speech_config)

Note

The interface or definition of `SpeechConfig`

is the same, irrespective of the language.

Speech configuration settings for live agents with audio capabilities. The
`SpeechConfig`

class has the following structure:

class SpeechConfig(_common.BaseModel):
"""The speech generation configuration."""
voice_config: Optional[VoiceConfig] = Field(
default=None,
description="""The configuration for the speaker to use.""",
)
language_code: Optional[str] = Field(
default=None,
description="""Language code (ISO 639. e.g. en-US) for the speech synthesization.
Only available for Live API.""",
)


The `voice_config`

parameter uses the `VoiceConfig`

class:

class VoiceConfig(_common.BaseModel):
"""The configuration for the voice to use."""
prebuilt_voice_config: Optional[PrebuiltVoiceConfig] = Field(
default=None,
description="""The configuration for the speaker to use.""",
)


And `PrebuiltVoiceConfig`

has the following structure:

class PrebuiltVoiceConfig(_common.BaseModel):
"""The configuration for the prebuilt speaker to use."""
voice_name: Optional[str] = Field(
default=None,
description="""The name of the prebuilt voice to use.""",
)


These nested configuration classes allow you to specify:

`voice_config`

: The name of the prebuilt voice to use (in the`PrebuiltVoiceConfig`

)`language_code`

: ISO 639 language code (e.g., "en-US") for speech synthesis

When implementing voice-enabled agents, configure these parameters to control how your agent sounds when speaking.

`response_modalities`

[¶](#response_modalities)

Defines the output modalities for the agent. If not set, defaults to AUDIO. Response modalities determine how the agent communicates with users through various channels (e.g., text, audio).

`save_input_blobs_as_artifacts`

[¶](#save_input_blobs_as_artifacts)

When enabled, input blobs will be saved as artifacts during agent execution. This is useful for debugging and audit purposes, allowing developers to review the exact data received by agents.

`support_cfc`

[¶](#support_cfc)

Enables Compositional Function Calling (CFC) support. Only applicable when using StreamingMode.SSE. When enabled, the LIVE API will be invoked as only it supports CFC functionality.

Experimental release

The `support_cfc`

feature is experimental and its API or behavior might
change in future releases.

`streaming_mode`

[¶](#streaming_mode)

Configures the streaming behavior of the agent. Possible values:

`StreamingMode.NONE`

: No streaming; responses delivered as complete units`StreamingMode.SSE`

: Server-Sent Events streaming; one-way streaming from server to client`StreamingMode.BIDI`

: Bidirectional streaming; simultaneous communication in both directions

Streaming modes affect both performance and user experience. SSE streaming lets users see partial responses as they're generated, while BIDI streaming enables real-time interactive experiences.

`output_audio_transcription`

[¶](#output_audio_transcription)

Configuration for transcribing audio outputs from live agents with audio response capability. This enables automatic transcription of audio responses for accessibility, record-keeping, and multi-modal applications.

`max_llm_calls`

[¶](#max_llm_calls)

Sets a limit on the total number of LLM calls for a given agent run.

- Values greater than 0 and less than
`sys.maxsize`

: Enforces a bound on LLM calls - Values less than or equal to 0: Allows unbounded LLM calls
*(not recommended for production)*

This parameter prevents excessive API usage and potential runaway processes. Since LLM calls often incur costs and consume resources, setting appropriate limits is crucial.

## Validation Rules[¶](#validation-rules)

The `RunConfig`

class validates its parameters to ensure proper agent operation. While Python ADK uses `Pydantic`

for automatic type validation, Java and TypeScript ADK rely on their static type systems and may include explicit checks in the `RunConfig`

's constructor.
For the `max_llm_calls`

parameter specifically:

-
Extremely large values (like

`sys.maxsize`

in Python,`Integer.MAX_VALUE`

in Java, or`Number.MAX_SAFE_INTEGER`

in TypeScript) are typically disallowed to prevent issues. -
Values of zero or less will usually trigger a warning about unlimited LLM interactions.


### Basic runtime configuration[¶](#basic-runtime-configuration)

This configuration creates a non-streaming agent with a limit of 100 LLM calls, suitable for simple task-oriented agents where complete responses are preferable.

### Enabling streaming[¶](#enabling-streaming)

Using SSE streaming allows users to see responses as they're generated, providing a more responsive feel for chatbots and assistants.

### Enabling speech support[¶](#enabling-speech-support)

from google.genai.adk import RunConfig, StreamingMode
from google.genai import types
config = RunConfig(
speech_config=types.SpeechConfig(
language_code="en-US",
voice_config=types.VoiceConfig(
prebuilt_voice_config=types.PrebuiltVoiceConfig(
voice_name="Kore"
)
),
),
response_modalities=["AUDIO", "TEXT"],
save_input_blobs_as_artifacts=True,
support_cfc=True,
streaming_mode=StreamingMode.SSE,
max_llm_calls=1000,
)


import { RunConfig, StreamingMode } from '@google/adk';
const config: RunConfig = {
speechConfig: {
languageCode: "en-US",
voiceConfig: {
prebuiltVoiceConfig: {
voiceName: "Kore"
}
},
},
responseModalities: [
{ modality: "AUDIO" },
{ modality: "TEXT" }
],
saveInputBlobsAsArtifacts: true,
supportCfc: true,
streamingMode: StreamingMode.SSE,
maxLlmCalls: 1000,
};


import com.google.adk.agents.RunConfig;
import com.google.adk.agents.RunConfig.StreamingMode;
import com.google.common.collect.ImmutableList;
import com.google.genai.types.Content;
import com.google.genai.types.Modality;
import com.google.genai.types.Part;
import com.google.genai.types.PrebuiltVoiceConfig;
import com.google.genai.types.SpeechConfig;
import com.google.genai.types.VoiceConfig;
RunConfig runConfig =
RunConfig.builder()
.setStreamingMode(StreamingMode.SSE)
.setMaxLlmCalls(1000)
.setSaveInputBlobsAsArtifacts(true)
.setResponseModalities(ImmutableList.of(new Modality("AUDIO"), new Modality("TEXT")))
.setSpeechConfig(
SpeechConfig.builder()
.voiceConfig(
VoiceConfig.builder()
.prebuiltVoiceConfig(
PrebuiltVoiceConfig.builder().voiceName("Kore").build())
.build())
.languageCode("en-US")
.build())
.build();


This comprehensive example configures an agent with:

- Speech capabilities using the "Kore" voice (US English)
- Both audio and text output modalities
- Artifact saving for input blobs (useful for debugging)
- Experimental CFC support enabled
**(Python and TypeScript)** - SSE streaming for responsive interaction
- A limit of 1000 LLM calls

### Enabling CFC Support[¶](#enabling-cfc-support)

Enabling Compositional Function Calling (CFC) creates an agent that can dynamically execute functions based on model outputs, powerful for applications requiring complex workflows.

Experimental release

The Compositional Function Calling (CFC) streaming feature is an experimental release.

---
<!-- Source: https://google.github.io/adk-docs/runtime/api-server/ -->

# Use the API Server¶

# Use the API Server[¶](#use-the-api-server)

Before you deploy your agent, you should test it to ensure that it is working as intended. Use the API server in ADK to expose your agents through a REST API for programmatic testing and integration.

## Start the API server[¶](#start-the-api-server)

Use the following command to run your agent in an ADK API server:

Make sure to update the port number.

With Maven, compile and run the ADK web server:

With Gradle, the `build.gradle`

or `build.gradle.kts`

build file should have the following Java plugin in its plugins section:

tasks.register('runADKWebServer', JavaExec) {
dependsOn classes
classpath = sourceSets.main.runtimeClasspath
mainClass = 'com.google.adk.web.AdkWebServer'
args '--adk.agents.source-dir=src/main/java/agents', '--server.port=8080'
}


Finally, on the command-line, run the following command:

In Java, both the Dev UI and the API server are bundled together.

This command will launch a local web server, where you can run cURL commands or
send API requests to test your agent. By default, the server runs on
`http://localhost:8000`

.

Advanced Usage and Debugging

For a complete reference on all available endpoints, request/response formats, and tips for debugging (including how to use the interactive API documentation), see the **ADK API Server Guide** below.

## Test locally[¶](#test-locally)

Testing locally involves launching a local web server, creating a session, and sending queries to your agent. First, ensure you are in the correct working directory.

For TypeScript, you should be inside the agent project directory itself.

parent_folder/
└── my_sample_agent/ <-- For TypeScript, run commands from here
└── agent.py (or Agent.java or agent.ts)


**Launch the Local Server**

Next, launch the local server using the commands listed above.

The output should appear similar to:

2025-05-13T23:32:08.972-06:00 INFO 37864 --- [ebServer.main()] o.s.b.w.embedded.tomcat.TomcatWebServer : Tomcat started on port 8080 (http) with context path '/'
2025-05-13T23:32:08.980-06:00 INFO 37864 --- [ebServer.main()] com.google.adk.web.AdkWebServer : Started AdkWebServer in 1.15 seconds (process running for 2.877)
2025-05-13T23:32:08.981-06:00 INFO 37864 --- [ebServer.main()] com.google.adk.web.AdkWebServer : AdkWebServer application started successfully.


Your server is now running locally. Ensure you use the correct ** port number** in all the subsequent commands.

**Create a new session**

With the API server still running, open a new terminal window or tab and create a new session with the agent using:

curl -X POST http://localhost:8000/apps/my_sample_agent/users/u_123/sessions/s_123 \
-H "Content-Type: application/json" \
-d '{"key1": "value1", "key2": 42}'


Let's break down what's happening:

`http://localhost:8000/apps/my_sample_agent/users/u_123/sessions/s_123`

: This creates a new session for your agent`my_sample_agent`

, which is the name of the agent folder, for a user ID (`u_123`

) and for a session ID (`s_123`

). You can replace`my_sample_agent`

with the name of your agent folder. You can replace`u_123`

with a specific user ID, and`s_123`

with a specific session ID.`{"key1": "value1", "key2": 42}`

: This is optional. You can use this to customize the agent's pre-existing state (dict) when creating the session.

This should return the session information if it was created successfully. The output should appear similar to:

{"id":"s_123","appName":"my_sample_agent","userId":"u_123","state":{"key1":"value1","key2":42},"events":[],"lastUpdateTime":1743711430.022186}


Info

You cannot create multiple sessions with exactly the same user ID and
session ID. If you try to, you may see a response, like:
`{"detail":"Session already exists: s_123"}`

. To fix this, you can either
delete that session (e.g., `s_123`

), or choose a different session ID.

**Send a query**

There are two ways to send queries via POST to your agent, via the `/run`

or
`/run_sse`

routes.

`POST http://localhost:8000/run`

: collects all events as a list and returns the list all at once. Suitable for most users (if you are unsure, we recommend using this one).`POST http://localhost:8000/run_sse`

: returns as Server-Sent-Events, which is a stream of event objects. Suitable for those who want to be notified as soon as the event is available. With`/run_sse`

, you can also set`streaming`

to`true`

to enable token-level streaming.

**Using /run**

curl -X POST http://localhost:8000/run \
-H "Content-Type: application/json" \
-d '{
"appName": "my_sample_agent",
"userId": "u_123",
"sessionId": "s_123",
"newMessage": {
"role": "user",
"parts": [{
"text": "Hey whats the weather in new york today"
}]
}
}'


In TypeScript, currently only `camelCase`

field names are supported (e.g. `appName`

, `userId`

, `sessionId`

, etc.).

If using `/run`

, you will see the full output of events at the same time, as a
list, which should appear similar to:

[{"content":{"parts":[{"functionCall":{"id":"af-e75e946d-c02a-4aad-931e-49e4ab859838","args":{"city":"new york"},"name":"get_weather"}}],"role":"model"},"invocationId":"e-71353f1e-aea1-4821-aa4b-46874a766853","author":"weather_time_agent","actions":{"stateDelta":{},"artifactDelta":{},"requestedAuthConfigs":{}},"longRunningToolIds":[],"id":"2Btee6zW","timestamp":1743712220.385936},{"content":{"parts":[{"functionResponse":{"id":"af-e75e946d-c02a-4aad-931e-49e4ab859838","name":"get_weather","response":{"status":"success","report":"The weather in New York is sunny with a temperature of 25 degrees Celsius (41 degrees Fahrenheit)."}}}],"role":"user"},"invocationId":"e-71353f1e-aea1-4821-aa4b-46874a766853","author":"weather_time_agent","actions":{"stateDelta":{},"artifactDelta":{},"requestedAuthConfigs":{}},"id":"PmWibL2m","timestamp":1743712221.895042},{"content":{"parts":[{"text":"OK. The weather in New York is sunny with a temperature of 25 degrees Celsius (41 degrees Fahrenheit).\n"}],"role":"model"},"invocationId":"e-71353f1e-aea1-4821-aa4b-46874a766853","author":"weather_time_agent","actions":{"stateDelta":{},"artifactDelta":{},"requestedAuthConfigs":{}},"id":"sYT42eVC","timestamp":1743712221.899018}]


**Using /run_sse**

curl -X POST http://localhost:8000/run_sse \
-H "Content-Type: application/json" \
-d '{
"appName": "my_sample_agent",
"userId": "u_123",
"sessionId": "s_123",
"newMessage": {
"role": "user",
"parts": [{
"text": "Hey whats the weather in new york today"
}]
},
"streaming": false
}'


You can set `streaming`

to `true`

to enable token-level streaming, which means
the response will be returned to you in multiple chunks and the output should
appear similar to:

data: {"content":{"parts":[{"functionCall":{"id":"af-f83f8af9-f732-46b6-8cb5-7b5b73bbf13d","args":{"city":"new york"},"name":"get_weather"}}],"role":"model"},"invocationId":"e-3f6d7765-5287-419e-9991-5fffa1a75565","author":"weather_time_agent","actions":{"stateDelta":{},"artifactDelta":{},"requestedAuthConfigs":{}},"longRunningToolIds":[],"id":"ptcjaZBa","timestamp":1743712255.313043}
data: {"content":{"parts":[{"functionResponse":{"id":"af-f83f8af9-f732-46b6-8cb5-7b5b73bbf13d","name":"get_weather","response":{"status":"success","report":"The weather in New York is sunny with a temperature of 25 degrees Celsius (41 degrees Fahrenheit)."}}}],"role":"user"},"invocationId":"e-3f6d7765-5287-419e-9991-5fffa1a75565","author":"weather_time_agent","actions":{"stateDelta":{},"artifactDelta":{},"requestedAuthConfigs":{}},"id":"5aocxjaq","timestamp":1743712257.387306}
data: {"content":{"parts":[{"text":"OK. The weather in New York is sunny with a temperature of 25 degrees Celsius (41 degrees Fahrenheit).\n"}],"role":"model"},"invocationId":"e-3f6d7765-5287-419e-9991-5fffa1a75565","author":"weather_time_agent","actions":{"stateDelta":{},"artifactDelta":{},"requestedAuthConfigs":{}},"id":"rAnWGSiV","timestamp":1743712257.391317}


**Send a query with a base64 encoded file using**

`/run`

or `/run_sse`

curl -X POST http://localhost:8000/run \
-H 'Content-Type: application/json' \
-d '{
"appName":"my_sample_agent",
"userId":"u_123",
"sessionId":"s_123",
"newMessage":{
"role":"user",
"parts":[
{
"text":"Describe this image"
},
{
"inlineData":{
"displayName":"my_image.png",
"data":"iVBORw0KGgoAAAANSUhEUgAAAgAAAAIACAYAAAD0eNT6AAAACXBIWXMAAAsTAAALEwEAmpw...",
"mimeType":"image/png"
}
}
]
},
"streaming":false
}'


Info

If you are using `/run_sse`

, you should see each event as soon as it becomes
available.

## Integrations[¶](#integrations)

ADK uses [Callbacks](../../callbacks/) to integrate with third-party
observability tools. These integrations capture detailed traces of agent calls
and interactions, which are crucial for understanding behavior, debugging
issues, and evaluating performance.

[Comet Opik](https://github.com/comet-ml/opik)is an open-source LLM observability and evaluation platform that[natively supports ADK](https://www.comet.com/docs/opik/tracing/integrations/adk).

## Deploy your agent[¶](#deploy-your-agent)

Now that you've verified the local operation of your agent, you're ready to move on to deploying your agent! Here are some ways you can deploy your agent:

- Deploy to
[Agent Engine](../../deploy/agent-engine/), a simple way to deploy your ADK agents to a managed service in Vertex AI on Google Cloud. - Deploy to
[Cloud Run](../../deploy/cloud-run/)and have full control over how you scale and manage your agents using serverless architecture on Google Cloud.

## Interactive API docs[¶](#interactive-api-docs)

The API server automatically generates interactive API documentation using Swagger UI. This is an invaluable tool for exploring endpoints, understanding request formats, and testing your agent directly from your browser.

To access the interactive docs, start the API server and navigate to [http://localhost:8000/docs](http://localhost:8000/docs) in your web browser.

You will see a complete, interactive list of all available API endpoints, which you can expand to see detailed information about parameters, request bodies, and response schemas. You can even click "Try it out" to send live requests to your running agents.

## API endpoints[¶](#api-endpoints)

The following sections detail the primary endpoints for interacting with your agents.

JSON Naming Convention

**Both Request and Response bodies**will use`camelCase`

for field names (e.g.,`"appName"`

).

### Utility endpoints[¶](#utility-endpoints)

#### List available agents[¶](#list-available-agents)

Returns a list of all agent applications discovered by the server.

**Method:**`GET`

**Path:**`/list-apps`


**Example Request**

**Example Response**

### Session management[¶](#session-management)

Sessions store the state and event history for a specific user's interaction with an agent.

#### Update a session[¶](#update-a-session)

Updates an existing session.

**Method:**`PATCH`

**Path:**`/apps/{app_name}/users/{user_id}/sessions/{session_id}`


**Request Body**

**Example Request**

curl -X PATCH http://localhost:8000/apps/my_sample_agent/users/u_123/sessions/s_abc \
-H "Content-Type: application/json" \
-d '{"stateDelta":{"visit_count": 5}}'


**Example Response**

{"id":"s_abc","appName":"my_sample_agent","userId":"u_123","state":{"visit_count":5},"events":[],"lastUpdateTime":1743711430.022186}


#### Get a session[¶](#get-a-session)

Retrieves the details of a specific session, including its current state and all associated events.

**Method:**`GET`

**Path:**`/apps/{app_name}/users/{user_id}/sessions/{session_id}`


**Example Request**

**Example Response**

{"id":"s_abc","appName":"my_sample_agent","userId":"u_123","state":{"visit_count":5},"events":[...],"lastUpdateTime":1743711430.022186}


#### Delete a session[¶](#delete-a-session)

Deletes a session and all of its associated data.

**Method:**`DELETE`

**Path:**`/apps/{app_name}/users/{user_id}/sessions/{session_id}`


**Example Request**

**Example Response**
A successful deletion returns an empty response with a `204 No Content`

status code.

### Agent execution[¶](#agent-execution)

These endpoints are used to send a new message to an agent and get a response.

#### Run agent (single response)[¶](#run-agent-single-response)

Executes the agent and returns all generated events in a single JSON array after the run is complete.

**Method:**`POST`

**Path:**`/run`


**Request Body**

{
"appName": "my_sample_agent",
"userId": "u_123",
"sessionId": "s_abc",
"newMessage": {
"role": "user",
"parts": [
{ "text": "What is the capital of France?" }
]
}
}


In TypeScript, currently only `camelCase`

field names are supported (e.g.
`appName`

, `userId`

, `sessionId`

, etc.).

**Example Request**

curl -X POST http://localhost:8000/run \
-H "Content-Type: application/json" \
-d '{
"appName": "my_sample_agent",
"userId": "u_123",
"sessionId": "s_abc",
"newMessage": {
"role": "user",
"parts": [{"text": "What is the capital of France?"}]
}
}'


#### Run agent (streaming)[¶](#run-agent-streaming)

Executes the agent and streams events back to the client as they are generated using [Server-Sent Events (SSE)](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events).

**Method:**`POST`

**Path:**`/run_sse`


**Request Body**
The request body is the same as for `/run`

, with an additional optional `streaming`

flag.

{
"appName": "my_sample_agent",
"userId": "u_123",
"sessionId": "s_abc",
"newMessage": {
"role": "user",
"parts": [
{ "text": "What is the weather in New York?" }
]
},
"streaming": true
}


`streaming`

: (Optional) Set to `true`

to enable token-level streaming for model responses. Defaults to `false`

.
**Example Request**

---
<!-- Source: https://google.github.io/adk-docs/runtime/event-loop/ -->

# Runtime Event Loop¶

# Runtime Event Loop[¶](#runtime-event-loop)

The ADK Runtime is the underlying engine that powers your agent application during user interactions. It's the system that takes your defined agents, tools, and callbacks and orchestrates their execution in response to user input, managing the flow of information, state changes, and interactions with external services like LLMs or storage.

Think of the Runtime as the **"engine"** of your agentic application. You define the parts (agents, tools), and the Runtime handles how they connect and run together to fulfill a user's request.

## Core Idea: The Event Loop[¶](#core-idea-the-event-loop)

At its heart, the ADK Runtime operates on an **Event Loop**. This loop facilitates a back-and-forth communication between the `Runner`

component and your defined "Execution Logic" (which includes your Agents, the LLM calls they make, Callbacks, and Tools).

In simple terms:

- The
`Runner`

receives a user query and asks the main`Agent`

to start processing. - The
`Agent`

(and its associated logic) runs until it has something to report (like a response, a request to use a tool, or a state change) – it then**yields**or**emits**an`Event`

. - The
`Runner`

receives this`Event`

, processes any associated actions (like saving state changes via`Services`

), and forwards the event onwards (e.g., to the user interface). - Only
*after*the`Runner`

has processed the event does the`Agent`

's logic**resume**from where it paused, now potentially seeing the effects of the changes committed by the Runner. - This cycle repeats until the agent has no more events to yield for the current user query.

This event-driven loop is the fundamental pattern governing how ADK executes your agent code.

## The Heartbeat: The Event Loop - Inner workings[¶](#the-heartbeat-the-event-loop-inner-workings)

The Event Loop is the core operational pattern defining the interaction between the `Runner`

and your custom code (Agents, Tools, Callbacks, collectively referred to as "Execution Logic" or "Logic Components" in the design document). It establishes a clear division of responsibilities:

Note

The specific method names and parameter names may vary slightly by SDK language (e.g., `agent.run_async(...)`

in Python, `agent.Run(...)`

in Go, `agent.runAsync(...)`

in Java and TypeScript). Refer to the language-specific API documentation for details.

### Runner's Role (Orchestrator)[¶](#runners-role-orchestrator)

The `Runner`

acts as the central coordinator for a single user invocation. Its responsibilities in the loop are:

**Initiation:**Receives the end user's query (`new_message`

) and typically appends it to the session history via the`SessionService`

.**Kick-off:**Starts the event generation process by calling the main agent's execution method (e.g.,`agent_to_run.run_async(...)`

).**Receive & Process:**Waits for the agent logic to`yield`

or`emit`

an`Event`

. Upon receiving an event, the Runner**promptly processes**it. This involves:- Using configured
`Services`

(`SessionService`

,`ArtifactService`

,`MemoryService`

) to commit changes indicated in`event.actions`

(like`state_delta`

,`artifact_delta`

). - Performing other internal bookkeeping.

- Using configured
**Yield Upstream:**Forwards the processed event onwards (e.g., to the calling application or UI for rendering).**Iterate:**Signals the agent logic that processing is complete for the yielded event, allowing it to resume and generate the*next*event.

*Conceptual Runner Loop:*

# Simplified view of Runner's main loop logic
def run(new_query, ...) -> Generator[Event]:
# 1. Append new_query to session event history (via SessionService)
session_service.append_event(session, Event(author='user', content=new_query))
# 2. Kick off event loop by calling the agent
agent_event_generator = agent_to_run.run_async(context)
async for event in agent_event_generator:
# 3. Process the generated event and commit changes
session_service.append_event(session, event) # Commits state/artifact deltas etc.
# memory_service.update_memory(...) # If applicable
# artifact_service might have already been called via context during agent run
# 4. Yield event for upstream processing (e.g., UI rendering)
yield event
# Runner implicitly signals agent generator can continue after yielding


// Simplified view of Runner's main loop logic
async * runAsync(newQuery: Content, ...): AsyncGenerator<Event, void, void> {
// 1. Append newQuery to session event history (via SessionService)
await sessionService.appendEvent({
session,
event: createEvent({author: 'user', content: newQuery})
});
// 2. Kick off event loop by calling the agent
const agentEventGenerator = agentToRun.runAsync(context);
for await (const event of agentEventGenerator) {
// 3. Process the generated event and commit changes
// Commits state/artifact deltas etc.
await sessionService.appendEvent({session, event});
// memoryService.updateMemory(...) // If applicable
// artifactService might have already been called via context during agent run
// 4. Yield event for upstream processing (e.g., UI rendering)
yield event;
// Runner implicitly signals agent generator can continue after yielding
}
}


// Simplified conceptual view of the Runner's main loop logic in Go
func (r *Runner) RunConceptual(ctx context.Context, session *session.Session, newQuery *genai.Content) iter.Seq2[*Event, error] {
return func(yield func(*Event, error) bool) {
// 1. Append new_query to session event history (via SessionService)
// ...
userEvent := session.NewEvent(ctx.InvocationID()) // Simplified for conceptual view
userEvent.Author = "user"
userEvent.LLMResponse = model.LLMResponse{Content: newQuery}
if _, err := r.sessionService.Append(ctx, &session.AppendRequest{Event: userEvent}); err != nil {
yield(nil, err)
return
}
// 2. Kick off event stream by calling the agent
// Assuming agent.Run also returns iter.Seq2[*Event, error]
agentEventsAndErrs := r.agent.Run(ctx, &agent.RunRequest{Session: session, Input: newQuery})
for event, err := range agentEventsAndErrs {
if err != nil {
if !yield(event, err) { // Yield event even if there's an error, then stop
return
}
return // Agent finished with an error
}
// 3. Process the generated event and commit changes
// Only commit non-partial event to a session service (as seen in actual code)
if !event.LLMResponse.Partial {
if _, err := r.sessionService.Append(ctx, &session.AppendRequest{Event: event}); err != nil {
yield(nil, err)
return
}
}
// memory_service.update_memory(...) // If applicable
// artifact_service might have already been called via context during agent run
// 4. Yield event for upstream processing
if !yield(event, nil) {
return // Upstream consumer stopped
}
}
// Agent finished successfully
}
}


// Simplified conceptual view of the Runner's main loop logic in Java.
public Flowable<Event> runConceptual(
Session session,
InvocationContext invocationContext,
Content newQuery
) {
// 1. Append new_query to session event history (via SessionService)
// ...
sessionService.appendEvent(session, userEvent).blockingGet();
// 2. Kick off event stream by calling the agent
Flowable<Event> agentEventStream = agentToRun.runAsync(invocationContext);
// 3. Process each generated event, commit changes, and "yield" or "emit"
return agentEventStream.map(event -> {
// This mutates the session object (adds event, applies stateDelta).
// The return value of appendEvent (a Single<Event>) is conceptually
// just the event itself after processing.
sessionService.appendEvent(session, event).blockingGet(); // Simplified blocking call
// memory_service.update_memory(...) // If applicable - conceptual
// artifact_service might have already been called via context during agent run
// 4. "Yield" event for upstream processing
// In RxJava, returning the event in map effectively yields it to the next operator or subscriber.
return event;
});
}


### Execution Logic's Role (Agent, Tool, Callback)[¶](#execution-logics-role-agent-tool-callback)

Your code within agents, tools, and callbacks is responsible for the actual computation and decision-making. Its interaction with the loop involves:

**Execute:**Runs its logic based on the current`InvocationContext`

, including the session state*as it was when execution resumed*.**Yield:**When the logic needs to communicate (send a message, call a tool, report a state change), it constructs an`Event`

containing the relevant content and actions, and then`yield`

s this event back to the`Runner`

.**Pause:**Crucially, execution of the agent logic**pauses immediately**after the`yield`

statement (or`return`

in RxJava). It waits for the`Runner`

to complete step 3 (processing and committing).**Resume:***Only after*the`Runner`

has processed the yielded event does the agent logic resume execution from the statement immediately following the`yield`

.**See Updated State:**Upon resumption, the agent logic can now reliably access the session state (`ctx.session.state`

) reflecting the changes that were committed by the`Runner`

from the*previously yielded*event.

*Conceptual Execution Logic:*

# Simplified view of logic inside Agent.run_async, callbacks, or tools
# ... previous code runs based on current state ...
# 1. Determine a change or output is needed, construct the event
# Example: Updating state
update_data = {'field_1': 'value_2'}
event_with_state_change = Event(
author=self.name,
actions=EventActions(state_delta=update_data),
content=types.Content(parts=[types.Part(text="State updated.")])
# ... other event fields ...
)
# 2. Yield the event to the Runner for processing & commit
yield event_with_state_change
# <<<<<<<<<<<< EXECUTION PAUSES HERE >>>>>>>>>>>>
# <<<<<<<<<<<< RUNNER PROCESSES & COMMITS THE EVENT >>>>>>>>>>>>
# 3. Resume execution ONLY after Runner is done processing the above event.
# Now, the state committed by the Runner is reliably reflected.
# Subsequent code can safely assume the change from the yielded event happened.
val = ctx.session.state['field_1']
# here `val` is guaranteed to be "value_2" (assuming Runner committed successfully)
print(f"Resumed execution. Value of field_1 is now: {val}")
# ... subsequent code continues ...
# Maybe yield another event later...


// Simplified view of logic inside Agent.runAsync, callbacks, or tools
// ... previous code runs based on current state ...
// 1. Determine a change or output is needed, construct the event
// Example: Updating state
const updateData = {'field_1': 'value_2'};
const eventWithStateChange = createEvent({
author: this.name,
actions: createEventActions({stateDelta: updateData}),
content: {parts: [{text: "State updated."}]}
// ... other event fields ...
});
// 2. Yield the event to the Runner for processing & commit
yield eventWithStateChange;
// <<<<<<<<<<<< EXECUTION PAUSES HERE >>>>>>>>>>>>
// <<<<<<<<<<<< RUNNER PROCESSES & COMMITS THE EVENT >>>>>>>>>>>>
// 3. Resume execution ONLY after Runner is done processing the above event.
// Now, the state committed by the Runner is reliably reflected.
// Subsequent code can safely assume the change from the yielded event happened.
const val = ctx.session.state['field_1'];
// here `val` is guaranteed to be "value_2" (assuming Runner committed successfully)
console.log(`Resumed execution. Value of field_1 is now: ${val}`);
// ... subsequent code continues ...
// Maybe yield another event later...


// Simplified view of logic inside Agent.Run, callbacks, or tools
// ... previous code runs based on current state ...
// 1. Determine a change or output is needed, construct the event
// Example: Updating state
updateData := map[string]interface{}{"field_1": "value_2"}
eventWithStateChange := &Event{
Author: self.Name(),
Actions: &EventActions{StateDelta: updateData},
Content: genai.NewContentFromText("State updated.", "model"),
// ... other event fields ...
}
// 2. Yield the event to the Runner for processing & commit
// In Go, this is done by sending the event to a channel.
eventsChan <- eventWithStateChange
// <<<<<<<<<<<< EXECUTION PAUSES HERE (conceptually) >>>>>>>>>>>>
// The Runner on the other side of the channel will receive and process the event.
// The agent's goroutine might continue, but the logical flow waits for the next input or step.
// <<<<<<<<<<<< RUNNER PROCESSES & COMMITS THE EVENT >>>>>>>>>>>>
// 3. Resume execution ONLY after Runner is done processing the above event.
// In a real Go implementation, this would likely be handled by the agent receiving
// a new RunRequest or context indicating the next step. The updated state
// would be part of the session object in that new request.
// For this conceptual example, we'll just check the state.
val := ctx.State.Get("field_1")
// here `val` is guaranteed to be "value_2" because the Runner would have
// updated the session state before calling the agent again.
fmt.Printf("Resumed execution. Value of field_1 is now: %v\n", val)
// ... subsequent code continues ...
// Maybe send another event to the channel later...


// Simplified view of logic inside Agent.runAsync, callbacks, or tools
// ... previous code runs based on current state ...
// 1. Determine a change or output is needed, construct the event
// Example: Updating state
ConcurrentMap<String, Object> updateData = new ConcurrentHashMap<>();
updateData.put("field_1", "value_2");
EventActions actions = EventActions.builder().stateDelta(updateData).build();
Content eventContent = Content.builder().parts(Part.fromText("State updated.")).build();
Event eventWithStateChange = Event.builder()
.author(self.name())
.actions(actions)
.content(Optional.of(eventContent))
// ... other event fields ...
.build();
// 2. "Yield" the event. In RxJava, this means emitting it into the stream.
// The Runner (or upstream consumer) will subscribe to this Flowable.
// When the Runner receives this event, it will process it (e.g., call sessionService.appendEvent).
// The 'appendEvent' in Java ADK mutates the 'Session' object held within 'ctx' (InvocationContext).
// <<<<<<<<<<<< CONCEPTUAL PAUSE POINT >>>>>>>>>>>>
// In RxJava, the emission of 'eventWithStateChange' happens, and then the stream
// might continue with a 'flatMap' or 'concatMap' operator that represents
// the logic *after* the Runner has processed this event.
// To model the "resume execution ONLY after Runner is done processing":
// The Runner's `appendEvent` is usually an async operation itself (returns Single<Event>).
// The agent's flow needs to be structured such that subsequent logic
// that depends on the committed state runs *after* that `appendEvent` completes.
// This is how the Runner typically orchestrates it:
// Runner:
// agent.runAsync(ctx)
// .concatMapEager(eventFromAgent ->
// sessionService.appendEvent(ctx.session(), eventFromAgent) // This updates ctx.session().state()
// .toFlowable() // Emits the event after it's processed
// )
// .subscribe(processedEvent -> { /* UI renders processedEvent */ });
// So, within the agent's own logic, if it needs to do something *after* an event it yielded
// has been processed and its state changes are reflected in ctx.session().state(),
// that subsequent logic would typically be in another step of its reactive chain.
// For this conceptual example, we'll emit the event, and then simulate the "resume"
// as a subsequent operation in the Flowable chain.
return Flowable.just(eventWithStateChange) // Step 2: Yield the event
.concatMap(yieldedEvent -> {
// <<<<<<<<<<<< RUNNER CONCEPTUALLY PROCESSES & COMMITS THE EVENT >>>>>>>>>>>>
// At this point, in a real runner, ctx.session().appendEvent(yieldedEvent) would have been called
// by the Runner, and ctx.session().state() would be updated.
// Since we are *inside* the agent's conceptual logic trying to model this,
// we assume the Runner's action has implicitly updated our 'ctx.session()'.
// 3. Resume execution.
// Now, the state committed by the Runner (via sessionService.appendEvent)
// is reliably reflected in ctx.session().state().
Object val = ctx.session().state().get("field_1");
// here `val` is guaranteed to be "value_2" because the `sessionService.appendEvent`
// called by the Runner would have updated the session state within the `ctx` object.
System.out.println("Resumed execution. Value of field_1 is now: " + val);
// ... subsequent code continues ...
// If this subsequent code needs to yield another event, it would do so here.


This cooperative yield/pause/resume cycle between the `Runner`

and your Execution Logic, mediated by `Event`

objects, forms the core of the ADK Runtime.

## Key components of the Runtime[¶](#key-components-of-the-runtime)

Several components work together within the ADK Runtime to execute an agent invocation. Understanding their roles clarifies how the event loop functions:

-
`Runner`

[¶](#runner)**Role:**The main entry point and orchestrator for a single user query (`run_async`

).**Function:**Manages the overall Event Loop, receives events yielded by the Execution Logic, coordinates with Services to process and commit event actions (state/artifact changes), and forwards processed events upstream (e.g., to the UI). It essentially drives the conversation turn by turn based on yielded events. (Defined in`google.adk.runners.runner`

).

-
### Execution Logic Components

[¶](#execution-logic-components)**Role:**The parts containing your custom code and the core agent capabilities.**Components:**`Agent`

(`BaseAgent`

,`LlmAgent`

, etc.): Your primary logic units that process information and decide on actions. They implement the`_run_async_impl`

method which yields events.`Tools`

(`BaseTool`

,`FunctionTool`

,`AgentTool`

, etc.): External functions or capabilities used by agents (often`LlmAgent`

) to interact with the outside world or perform specific tasks. They execute and return results, which are then wrapped in events.`Callbacks`

(Functions): User-defined functions attached to agents (e.g.,`before_agent_callback`

,`after_model_callback`

) that hook into specific points in the execution flow, potentially modifying behavior or state, whose effects are captured in events.**Function:**Perform the actual thinking, calculation, or external interaction. They communicate their results or needs by**yielding**and pausing until the Runner processes them.`Event`

objects

-
`Event`

[¶](#event)**Role:**The message passed back and forth between the`Runner`

and the Execution Logic.**Function:**Represents an atomic occurrence (user input, agent text, tool call/result, state change request, control signal). It carries both the content of the occurrence and the intended side effects (`actions`

like`state_delta`

).

-
`Services`

[¶](#services)**Role:**Backend components responsible for managing persistent or shared resources. Used primarily by the`Runner`

during event processing.**Components:**`SessionService`

(`BaseSessionService`

,`InMemorySessionService`

, etc.): Manages`Session`

objects, including saving/loading them, applying`state_delta`

to the session state, and appending events to the`event history`

.`ArtifactService`

(`BaseArtifactService`

,`InMemoryArtifactService`

,`GcsArtifactService`

, etc.): Manages the storage and retrieval of binary artifact data. Although`save_artifact`

is called via context during execution logic, the`artifact_delta`

in the event confirms the action for the Runner/SessionService.`MemoryService`

(`BaseMemoryService`

, etc.): (Optional) Manages long-term semantic memory across sessions for a user.**Function:**Provide the persistence layer. The`Runner`

interacts with them to ensure changes signaled by`event.actions`

are reliably stored*before*the Execution Logic resumes.

-
`Session`

[¶](#session)**Role:**A data container holding the state and history for*one specific conversation*between a user and the application.**Function:**Stores the current`state`

dictionary, the list of all past`events`

(`event history`

), and references to associated artifacts. It's the primary record of the interaction, managed by the`SessionService`

.

-
`Invocation`

[¶](#invocation)**Role:**A conceptual term representing everything that happens in response to a*single*user query, from the moment the`Runner`

receives it until the agent logic finishes yielding events for that query.**Function:**An invocation might involve multiple agent runs (if using agent transfer or`AgentTool`

), multiple LLM calls, tool executions, and callback executions, all tied together by a single`invocation_id`

within the`InvocationContext`

. State variables prefixed with`temp:`

are strictly scoped to a single invocation and discarded afterwards.


These players interact continuously through the Event Loop to process a user's request.

## How It Works: A Simplified Invocation[¶](#how-it-works-a-simplified-invocation)

Let's trace a simplified flow for a typical user query that involves an LLM agent calling a tool:

### Step-by-Step Breakdown[¶](#step-by-step-breakdown)

**User Input:**The User sends a query (e.g., "What's the capital of France?").**Runner Starts:**`Runner.run_async`

begins. It interacts with the`SessionService`

to load the relevant`Session`

and adds the user query as the first`Event`

to the session history. An`InvocationContext`

(`ctx`

) is prepared.**Agent Execution:**The`Runner`

calls`agent.run_async(ctx)`

on the designated root agent (e.g., an`LlmAgent`

).**LLM Call (Example):**The`Agent_Llm`

determines it needs information, perhaps by calling a tool. It prepares a request for the`LLM`

. Let's assume the LLM decides to call`MyTool`

.**Yield FunctionCall Event:**The`Agent_Llm`

receives the`FunctionCall`

response from the LLM, wraps it in an`Event(author='Agent_Llm', content=Content(parts=[Part(function_call=...)]))`

, and`yields`

or`emits`

this event.**Agent Pauses:**The`Agent_Llm`

's execution pauses immediately after the`yield`

.**Runner Processes:**The`Runner`

receives the FunctionCall event. It passes it to the`SessionService`

to record it in the history. The`Runner`

then yields the event upstream to the`User`

(or application).**Agent Resumes:**The`Runner`

signals that the event is processed, and`Agent_Llm`

resumes execution.**Tool Execution:**The`Agent_Llm`

's internal flow now proceeds to execute the requested`MyTool`

. It calls`tool.run_async(...)`

.**Tool Returns Result:**`MyTool`

executes and returns its result (e.g.,`{'result': 'Paris'}`

).**Yield FunctionResponse Event:**The agent (`Agent_Llm`

) wraps the tool result into an`Event`

containing a`FunctionResponse`

part (e.g.,`Event(author='Agent_Llm', content=Content(role='user', parts=[Part(function_response=...)]))`

). This event might also contain`actions`

if the tool modified state (`state_delta`

) or saved artifacts (`artifact_delta`

). The agent`yield`

s this event.**Agent Pauses:**`Agent_Llm`

pauses again.**Runner Processes:**`Runner`

receives the FunctionResponse event. It passes it to`SessionService`

which applies any`state_delta`

/`artifact_delta`

and adds the event to history.`Runner`

yields the event upstream.**Agent Resumes:**`Agent_Llm`

resumes, now knowing the tool result and any state changes are committed.**Final LLM Call (Example):**`Agent_Llm`

sends the tool result back to the`LLM`

to generate a natural language response.**Yield Final Text Event:**`Agent_Llm`

receives the final text from the`LLM`

, wraps it in an`Event(author='Agent_Llm', content=Content(parts=[Part(text=...)]))`

, and`yield`

s it.**Agent Pauses:**`Agent_Llm`

pauses.**Runner Processes:**`Runner`

receives the final text event, passes it to`SessionService`

for history, and yields it upstream to the`User`

. This is likely marked as the`is_final_response()`

.**Agent Resumes & Finishes:**`Agent_Llm`

resumes. Having completed its task for this invocation, its`run_async`

generator finishes.**Runner Completes:**The`Runner`

sees the agent's generator is exhausted and finishes its loop for this invocation.

This yield/pause/process/resume cycle ensures that state changes are consistently applied and that the execution logic always operates on the most recently committed state after yielding an event.

## Important Runtime Behaviors[¶](#important-runtime-behaviors)

Understanding a few key aspects of how the ADK Runtime handles state, streaming, and asynchronous operations is crucial for building predictable and efficient agents.

### State Updates & Commitment Timing[¶](#state-updates-commitment-timing)

-
**The Rule:**When your code (in an agent, tool, or callback) modifies the session state (e.g.,`context.state['my_key'] = 'new_value'`

), this change is initially recorded locally within the current`InvocationContext`

. The change is only**guaranteed to be persisted**(saved by the`SessionService`

)*after*the`Event`

carrying the corresponding`state_delta`

in its`actions`

has been`yield`

-ed by your code and subsequently processed by the`Runner`

. -
**Implication:**Code that runs*after*resuming from a`yield`

can reliably assume that the state changes signaled in the*yielded event*have been committed.

# Inside agent logic (conceptual)
# 1. Modify state
ctx.session.state['status'] = 'processing'
event1 = Event(..., actions=EventActions(state_delta={'status': 'processing'}))
# 2. Yield event with the delta
yield event1
# --- PAUSE --- Runner processes event1, SessionService commits 'status' = 'processing' ---
# 3. Resume execution
# Now it's safe to rely on the committed state
current_status = ctx.session.state['status'] # Guaranteed to be 'processing'
print(f"Status after resuming: {current_status}")


// Inside agent logic (conceptual)
// 1. Modify state
// In TypeScript, you modify state via the context, which tracks the change.
ctx.state.set('status', 'processing');
// The framework will automatically populate actions with the state
// delta from the context. For illustration, it's shown here.
const event1 = createEvent({
actions: createEventActions({stateDelta: {'status': 'processing'}}),
// ... other event fields
});
// 2. Yield event with the delta
yield event1;
// --- PAUSE --- Runner processes event1, SessionService commits 'status' = 'processing' ---
// 3. Resume execution
// Now it's safe to rely on the committed state in the session object.
const currentStatus = ctx.session.state['status']; // Guaranteed to be 'processing'
console.log(`Status after resuming: ${currentStatus}`);


// Inside agent logic (conceptual)
func (a *Agent) RunConceptual(ctx agent.InvocationContext) iter.Seq2[*session.Event, error] {
// The entire logic is wrapped in a function that will be returned as an iterator.
return func(yield func(*session.Event, error) bool) {
// ... previous code runs based on current state from the input `ctx` ...
// e.g., val := ctx.State().Get("field_1") might return "value_1" here.
// 1. Determine a change or output is needed, construct the event
updateData := map[string]interface{}{"field_1": "value_2"}
eventWithStateChange := session.NewEvent(ctx.InvocationID())
eventWithStateChange.Author = a.Name()
eventWithStateChange.Actions = &session.EventActions{StateDelta: updateData}
// ... other event fields ...
// 2. Yield the event to the Runner for processing & commit.
// The agent's execution continues immediately after this call.
if !yield(eventWithStateChange, nil) {
// If yield returns false, it means the consumer (the Runner)
// has stopped listening, so we should stop producing events.
return
}
// <<<<<<<<<<<< RUNNER PROCESSES & COMMITS THE EVENT >>>>>>>>>>>>
// This happens outside the agent, after the agent's iterator has
// produced the event.
// 3. The agent CANNOT immediately see the state change it just yielded.
// The state is immutable within a single `Run` invocation.
val := ctx.State().Get("field_1")
// `val` here is STILL "value_1" (or whatever it was at the start).
// The updated state ("value_2") will only be available in the `ctx`
// of the *next* `Run` invocation in a subsequent turn.
// ... subsequent code continues, potentially yielding more events ...
finalEvent := session.NewEvent(ctx.InvocationID())
finalEvent.Author = a.Name()
// ...
yield(finalEvent, nil)
}
}


// Inside agent logic (conceptual)
// ... previous code runs based on current state ...
// 1. Prepare state modification and construct the event
ConcurrentHashMap<String, Object> stateChanges = new ConcurrentHashMap<>();
stateChanges.put("status", "processing");
EventActions actions = EventActions.builder().stateDelta(stateChanges).build();
Content content = Content.builder().parts(Part.fromText("Status update: processing")).build();
Event event1 = Event.builder()
.actions(actions)
// ...
.build();
// 2. Yield event with the delta
return Flowable.just(event1)
.map(
emittedEvent -> {
// --- CONCEPTUAL PAUSE & RUNNER PROCESSING ---
// 3. Resume execution (conceptually)
// Now it's safe to rely on the committed state.
String currentStatus = (String) ctx.session().state().get("status");
System.out.println("Status after resuming (inside agent logic): " + currentStatus); // Guaranteed to be 'processing'
// The event itself (event1) is passed on.
// If subsequent logic within this agent step produced *another* event,
// you'd use concatMap to emit that new event.
return emittedEvent;
});
// ... subsequent agent logic might involve further reactive operators
// or emitting more events based on the now-updated `ctx.session().state()`.


### "Dirty Reads" of Session State[¶](#dirty-reads-of-session-state)

**Definition:**While commitment happens*after*the yield, code running*later within the same invocation*, but*before*the state-changing event is actually yielded and processed,**can often see the local, uncommitted changes**. This is sometimes called a "dirty read".**Example:**

# Code in before_agent_callback
callback_context.state['field_1'] = 'value_1'
# State is locally set to 'value_1', but not yet committed by Runner
# ... agent runs ...
# Code in a tool called later *within the same invocation*
# Readable (dirty read), but 'value_1' isn't guaranteed persistent yet.
val = tool_context.state['field_1'] # 'val' will likely be 'value_1' here
print(f"Dirty read value in tool: {val}")
# Assume the event carrying the state_delta={'field_1': 'value_1'}
# is yielded *after* this tool runs and is processed by the Runner.


// Code in beforeAgentCallback
callbackContext.state.set('field_1', 'value_1');
// State is locally set to 'value_1', but not yet committed by Runner
// --- agent runs ... ---
// --- Code in a tool called later *within the same invocation* ---
// Readable (dirty read), but 'value_1' isn't guaranteed persistent yet.
const val = toolContext.state.get('field_1'); // 'val' will likely be 'value_1' here
console.log(`Dirty read value in tool: ${val}`);
// Assume the event carrying the state_delta={'field_1': 'value_1'}
// is yielded *after* this tool runs and is processed by the Runner.


// Code in before_agent_callback
// The callback would modify the context's session state directly.
// This change is local to the current invocation context.
ctx.State.Set("field_1", "value_1")
// State is locally set to 'value_1', but not yet committed by Runner
// ... agent runs ...
// Code in a tool called later *within the same invocation*
// Readable (dirty read), but 'value_1' isn't guaranteed persistent yet.
val := ctx.State.Get("field_1") // 'val' will likely be 'value_1' here
fmt.Printf("Dirty read value in tool: %v\n", val)
// Assume the event carrying the state_delta={'field_1': 'value_1'}
// is yielded *after* this tool runs and is processed by the Runner.


// Modify state - Code in BeforeAgentCallback
// AND stages this change in callbackContext.eventActions().stateDelta().
callbackContext.state().put("field_1", "value_1");
// --- agent runs ... ---
// --- Code in a tool called later *within the same invocation* ---
// Readable (dirty read), but 'value_1' isn't guaranteed persistent yet.
Object val = toolContext.state().get("field_1"); // 'val' will likely be 'value_1' here
System.out.println("Dirty read value in tool: " + val);
// Assume the event carrying the state_delta={'field_1': 'value_1'}
// is yielded *after* this tool runs and is processed by the Runner.


**Implications:****Benefit:**Allows different parts of your logic within a single complex step (e.g., multiple callbacks or tool calls before the next LLM turn) to coordinate using state without waiting for a full yield/commit cycle.**Caveat:**Relying heavily on dirty reads for critical logic can be risky. If the invocation fails*before*the event carrying the`state_delta`

is yielded and processed by the`Runner`

, the uncommitted state change will be lost. For critical state transitions, ensure they are associated with an event that gets successfully processed.

### Streaming vs. Non-Streaming Output (`partial=True`

)[¶](#streaming-vs-non-streaming-output-partialtrue)

This primarily relates to how responses from the LLM are handled, especially when using streaming generation APIs.

**Streaming:**The LLM generates its response token-by-token or in small chunks.- The framework (often within
`BaseLlmFlow`

) yields multiple`Event`

objects for a single conceptual response. Most of these events will have`partial=True`

. - The
`Runner`

, upon receiving an event with`partial=True`

, typically**forwards it immediately**upstream (for UI display) but**skips processing its**(like`actions`

`state_delta`

). - Eventually, the framework yields a final event for that response, marked as non-partial (
`partial=False`

or implicitly via`turn_complete=True`

). - The
`Runner`

**fully processes only this final event**, committing any associated`state_delta`

or`artifact_delta`

. **Non-Streaming:**The LLM generates the entire response at once. The framework yields a single event marked as non-partial, which the`Runner`

processes fully.**Why it Matters:**Ensures that state changes are applied atomically and only once based on the*complete*response from the LLM, while still allowing the UI to display text progressively as it's generated.

## Async is Primary (`run_async`

)[¶](#async-is-primary-run_async)

**Core Design:**The ADK Runtime is fundamentally built on asynchronous patterns and libraries (like Python's`asyncio`

, Java's`RxJava`

, and native`Promise`

s and`AsyncGenerator`

s in TypeScript) to handle concurrent operations (like waiting for LLM responses or tool executions) efficiently without blocking.**Main Entry Point:**`Runner.run_async`

is the primary method for executing agent invocations. All core runnable components (Agents, specific flows) use`asynchronous`

methods internally.**Synchronous Convenience (**A synchronous`run`

):`Runner.run`

method exists mainly for convenience (e.g., in simple scripts or testing environments). However, internally,`Runner.run`

typically just calls`Runner.run_async`

and manages the async event loop execution for you.**Developer Experience:**We recommend designing your applications (e.g., web servers using ADK) to be asynchronous for best performance. In Python, this means using`asyncio`

; in Java, leverage`RxJava`

's reactive programming model; and in TypeScript, this means building using native`Promise`

s and`AsyncGenerator`

s.**Sync Callbacks/Tools:**The ADK framework supports both asynchronous and synchronous functions for tools and callbacks.**Blocking I/O:**For long-running synchronous I/O operations, the framework attempts to prevent stalls. Python ADK may use asyncio.to_thread, while Java ADK often relies on appropriate RxJava schedulers or wrappers for blocking calls. In TypeScript, the framework simply awaits the function; if a synchronous function performs blocking I/O, it will stall the event loop. Developers should use asynchronous I/O APIs (which return a Promise) whenever possible.**CPU-Bound Work:**Purely CPU-intensive synchronous tasks will still block their execution thread in both environments.


Understanding these behaviors helps you write more robust ADK applications and debug issues related to state consistency, streaming updates, and asynchronous execution.
