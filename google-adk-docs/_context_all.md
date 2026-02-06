---
merged_at: 2026-02-06T16:54:52.633380
merged_files: 3
---


---
<!-- Source: https://google.github.io/adk-docs/context/caching/ -->

# Context caching with Gemini¶

# Context caching with Gemini[¶](#context-caching-with-gemini)

When working with agents to complete tasks, you may want to reuse extended instructions or large sets of data across multiple agent requests to a generative AI model. Resending this data for each agent request is slow, inefficient, and can be expensive. Using context caching features in generative AI models can significantly speed up responses and lower the number of tokens sent to the model for each request.

The ADK Context Caching feature allows you to cache request data with generative AI models that support it, including Gemini 2.0 and higher models. This document explains how to configure and use this feature.

## Configure context caching[¶](#configure-context-caching)

You configure the context caching feature at the ADK `App`

object level,
which wraps your agent. Use the `ContextCacheConfig`

class to configure
these settings, as shown in the following code sample:

from google.adk import Agent
from google.adk.apps.app import App
from google.adk.agents.context_cache_config import ContextCacheConfig
root_agent = Agent(
# configure an agent using Gemini 2.0 or higher
)
# Create the app with context caching configuration
app = App(
name='my-caching-agent-app',
root_agent=root_agent,
context_cache_config=ContextCacheConfig(
min_tokens=2048, # Minimum tokens to trigger caching
ttl_seconds=600, # Store for up to 10 minutes
cache_intervals=5, # Refresh after 5 uses
),
)


## Configuration settings[¶](#configuration-settings)

The `ContextCacheConfig`

class has the following settings that control how
caching works for your agent. When you configure these settings, they apply to
all agents within your app.

(int): The minimum number of tokens required in a request to enable caching. This setting allows you to avoid the overhead of caching for very small requests where the performance benefit would be negligible. Defaults to`min_tokens`

`0`

.(int): The time-to-live (TTL) for the cache in seconds. This setting determines how long the cached content is stored before it is refreshed. Defaults to`ttl_seconds`

`1800`

(30 minutes).(int): The maximum number of times the same cached content can be used before it expires. This setting allows you to control how frequently the cache is updated, even if the TTL has not expired. Defaults to`cache_intervals`

`10`

.

## Next steps[¶](#next-steps)

For a full implementation of how to use and test the context caching feature, see the following sample:

: A code sample that demonstrates how to analyze the performance of context caching.`cache_analysis`


If your use case requires that you provide instructions that are used throughout
a session, consider using the `static_instruction`

parameter for an agent, which
allows you to amend the system instructions for a generative model. For more
details, see this sample code:

: An implementation of a digital pet agent using static instructions.`static_instruction`

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
<!-- Source: https://google.github.io/adk-docs/context/ -->

# Context¶

# Context[¶](#context)

In the Agent Development Kit (ADK), "context" refers to the crucial bundle of information available to your agent and its tools during specific operations. Think of it as the necessary background knowledge and resources needed to handle a current task or conversation turn effectively.

Agents often need more than just the latest user message to perform well. Context is essential because it enables:

**Maintaining State:**Remembering details across multiple steps in a conversation (e.g., user preferences, previous calculations, items in a shopping cart). This is primarily managed through**session state**.**Passing Data:**Sharing information discovered or generated in one step (like an LLM call or a tool execution) with subsequent steps. Session state is key here too.**Accessing Services:**Interacting with framework capabilities like:**Artifact Storage:**Saving or loading files or data blobs (like PDFs, images, configuration files) associated with the session.**Memory:**Searching for relevant information from past interactions or external knowledge sources connected to the user.**Authentication:**Requesting and retrieving credentials needed by tools to access external APIs securely.

**Identity and Tracking:**Knowing which agent is currently running (`agent.name`

) and uniquely identifying the current request-response cycle (`invocation_id`

) for logging and debugging.**Tool-Specific Actions:**Enabling specialized operations within tools, such as requesting authentication or searching memory, which require access to the current interaction's details.

The central piece holding all this information together for a single, complete user-request-to-final-response cycle (an **invocation**) is the `InvocationContext`

. However, you typically won't create or manage this object directly. The ADK framework creates it when an invocation starts (e.g., via `runner.run_async`

) and passes the relevant contextual information implicitly to your agent code, callbacks, and tools.

# Conceptual Pseudocode: How the framework provides context (Internal Logic)
# runner = Runner(agent=my_root_agent, session_service=..., artifact_service=...)
# user_message = types.Content(...)
# session = session_service.get_session(...) # Or create new
# --- Inside runner.run_async(...) ---
# 1. Framework creates the main context for this specific run
# invocation_context = InvocationContext(
# invocation_id="unique-id-for-this-run",
# session=session,
# user_content=user_message,
# agent=my_root_agent, # The starting agent
# session_service=session_service,
# artifact_service=artifact_service,
# memory_service=memory_service,
# # ... other necessary fields ...
# )
#
# 2. Framework calls the agent's run method, passing the context implicitly
# (The agent's method signature will receive it, e.g., runAsyncImpl(InvocationContext invocationContext))
# await my_root_agent.run_async(invocation_context)
# --- End Internal Logic ---
#
# As a developer, you work with the context objects provided in method arguments.


/* Conceptual Pseudocode: How the framework provides context (Internal Logic) */
const runner = new InMemoryRunner({ agent: myRootAgent });
const session = await runner.sessionService.createSession({ ... });
const userMessage = createUserContent(...);
// --- Inside runner.runAsync(...) ---
// 1. Framework creates the main context for this specific run
const invocationContext = new InvocationContext({
invocationId: "unique-id-for-this-run",
session: session,
userContent: userMessage,
agent: myRootAgent, // The starting agent
sessionService: runner.sessionService,
pluginManager: runner.pluginManager,
// ... other necessary fields ...
});
//
// 2. Framework calls the agent's run method, passing the context implicitly
await myRootAgent.runAsync(invocationContext);
// --- End Internal Logic ---
// As a developer, you work with the context objects provided in method arguments.


/* Conceptual Pseudocode: How the framework provides context (Internal Logic) */
sessionService := session.InMemoryService()
r, err := runner.New(runner.Config{
AppName: appName,
Agent: myAgent,
SessionService: sessionService,
})
if err != nil {
log.Fatalf("Failed to create runner: %v", err)
}
s, err := sessionService.Create(ctx, &session.CreateRequest{
AppName: appName,
UserID: userID,
})
if err != nil {
log.Fatalf("FATAL: Failed to create session: %v", err)
}
scanner := bufio.NewScanner(os.Stdin)
for {
fmt.Print("\nYou > ")
if !scanner.Scan() {
break
}
userInput := scanner.Text()
if strings.EqualFold(userInput, "quit") {
break
}
userMsg := genai.NewContentFromText(userInput, genai.RoleUser)
events := r.Run(ctx, s.Session.UserID(), s.Session.ID(), userMsg, agent.RunConfig{
StreamingMode: agent.StreamingModeNone,
})
fmt.Print("\nAgent > ")
for event, err := range events {
if err != nil {
log.Printf("ERROR during agent execution: %v", err)
break
}
fmt.Print(event.Content.Parts[0].Text)
}
}


/* Conceptual Pseudocode: How the framework provides context (Internal Logic) */
InMemoryRunner runner = new InMemoryRunner(agent);
Session session = runner
.sessionService()
.createSession(runner.appName(), USER_ID, initialState, SESSION_ID )
.blockingGet();
try (Scanner scanner = new Scanner(System.in, StandardCharsets.UTF_8)) {
while (true) {
System.out.print("\nYou > ");
}
String userInput = scanner.nextLine();
if ("quit".equalsIgnoreCase(userInput)) {
break;
}
Content userMsg = Content.fromParts(Part.fromText(userInput));
Flowable<Event> events = runner.runAsync(session.userId(), session.id(), userMsg);
System.out.print("\nAgent > ");
events.blockingForEach(event -> System.out.print(event.stringifyContent()));
}


## The Different types of Context[¶](#the-different-types-of-context)

While `InvocationContext`

acts as the comprehensive internal container, ADK provides specialized context objects tailored to specific situations. This ensures you have the right tools and permissions for the task at hand without needing to handle the full complexity of the internal context everywhere. Here are the different "flavors" you'll encounter:

-
`InvocationContext`

**Where Used:**Received as the`ctx`

argument directly within an agent's core implementation methods (`_run_async_impl`

,`_run_live_impl`

).**Purpose:**Provides access to the*entire*state of the current invocation. This is the most comprehensive context object.**Key Contents:**Direct access to`session`

(including`state`

and`events`

), the current`agent`

instance,`invocation_id`

, initial`user_content`

, references to configured services (`artifact_service`

,`memory_service`

,`session_service`

), and fields related to live/streaming modes.**Use Case:**Primarily used when the agent's core logic needs direct access to the overall session or services, though often state and artifact interactions are delegated to callbacks/tools which use their own contexts. Also used to control the invocation itself (e.g., setting`ctx.end_invocation = True`

).

[# Pseudocode: Agent implementation receiving InvocationContext](#__codelineno-4-1)[from google.adk.agents import BaseAgent](#__codelineno-4-2)[from google.adk.agents.invocation_context import InvocationContext](#__codelineno-4-3)[from google.adk.events import Event](#__codelineno-4-4)[from typing import AsyncGenerator](#__codelineno-4-5)[class MyAgent(BaseAgent):](#__codelineno-4-7)[async def _run_async_impl(self, ctx: InvocationContext) -> AsyncGenerator[Event, None]:](#__codelineno-4-8)[# Direct access example](#__codelineno-4-9)[agent_name = ctx.agent.name](#__codelineno-4-10)[session_id = ctx.session.id](#__codelineno-4-11)[print(f"Agent {agent_name} running in session {session_id} for invocation {ctx.invocation_id}")](#__codelineno-4-12)[# ... agent logic using ctx ...](#__codelineno-4-13)[yield # ... event ...](#__codelineno-4-14)[// Pseudocode: Agent implementation receiving InvocationContext](#__codelineno-5-1)[import { BaseAgent, InvocationContext, Event } from '@google/adk';](#__codelineno-5-2)[class MyAgent extends BaseAgent {](#__codelineno-5-4)[async *runAsyncImpl(ctx: InvocationContext): AsyncGenerator<Event, void, undefined> {](#__codelineno-5-5)[// Direct access example](#__codelineno-5-6)[const agentName = ctx.agent.name;](#__codelineno-5-7)[const sessionId = ctx.session.id;](#__codelineno-5-8)[console.log(`Agent ${agentName} running in session ${sessionId} for invocation ${ctx.invocationId}`);](#__codelineno-5-9)[// ... agent logic using ctx ...](#__codelineno-5-10)[yield; // ... event ...](#__codelineno-5-11)[}](#__codelineno-5-12)[}](#__codelineno-5-13)[import (](#__codelineno-6-1)["google.golang.org/adk/agent"](#__codelineno-6-2)["google.golang.org/adk/session"](#__codelineno-6-3)[)](#__codelineno-6-4)[// Pseudocode: Agent implementation receiving InvocationContext](#__codelineno-6-6)[type MyAgent struct {](#__codelineno-6-7)[}](#__codelineno-6-8)[func (a *MyAgent) Run(ctx agent.InvocationContext) iter.Seq2[*session.Event, error] {](#__codelineno-6-10)[return func(yield func(*session.Event, error) bool) {](#__codelineno-6-11)[// Direct access example](#__codelineno-6-12)[agentName := ctx.Agent().Name()](#__codelineno-6-13)[sessionID := ctx.Session().ID()](#__codelineno-6-14)[fmt.Printf("Agent %s running in session %s for invocation %s\n", agentName, sessionID, ctx.InvocationID())](#__codelineno-6-15)[// ... agent logic using ctx ...](#__codelineno-6-16)[yield(&session.Event{Author: agentName}, nil)](#__codelineno-6-17)[}](#__codelineno-6-18)[}](#__codelineno-6-19)[// Pseudocode: Agent implementation receiving InvocationContext](#__codelineno-7-1)[import com.google.adk.agents.BaseAgent;](#__codelineno-7-2)[import com.google.adk.agents.InvocationContext;](#__codelineno-7-3)[LlmAgent root_agent =](#__codelineno-7-5)[LlmAgent.builder()](#__codelineno-7-6)[.model("gemini-***")](#__codelineno-7-7)[.name("sample_agent")](#__codelineno-7-8)[.description("Answers user questions.")](#__codelineno-7-9)[.instruction(](#__codelineno-7-10)["""](#__codelineno-7-11)[provide instruction for the agent here.](#__codelineno-7-12)["""](#__codelineno-7-13)[)](#__codelineno-7-14)[.tools(sampleTool)](#__codelineno-7-15)[.outputKey("YOUR_KEY")](#__codelineno-7-16)[.build();](#__codelineno-7-17)[ConcurrentMap<String, Object> initialState = new ConcurrentHashMap<>();](#__codelineno-7-19)[initialState.put("YOUR_KEY", "");](#__codelineno-7-20)[InMemoryRunner runner = new InMemoryRunner(agent);](#__codelineno-7-22)[Session session =](#__codelineno-7-23)[runner](#__codelineno-7-24)[.sessionService()](#__codelineno-7-25)[.createSession(runner.appName(), USER_ID, initialState, SESSION_ID )](#__codelineno-7-26)[.blockingGet();](#__codelineno-7-27)[try (Scanner scanner = new Scanner(System.in, StandardCharsets.UTF_8)) {](#__codelineno-7-29)[while (true) {](#__codelineno-7-30)[System.out.print("\nYou > ");](#__codelineno-7-31)[String userInput = scanner.nextLine();](#__codelineno-7-32)[if ("quit".equalsIgnoreCase(userInput)) {](#__codelineno-7-34)[break;](#__codelineno-7-35)[}](#__codelineno-7-36)[Content userMsg = Content.fromParts(Part.fromText(userInput));](#__codelineno-7-38)[Flowable<Event> events =](#__codelineno-7-39)[runner.runAsync(session.userId(), session.id(), userMsg);](#__codelineno-7-40)[System.out.print("\nAgent > ");](#__codelineno-7-42)[events.blockingForEach(event ->](#__codelineno-7-43)[System.out.print(event.stringifyContent()));](#__codelineno-7-44)[}](#__codelineno-7-45)[protected Flowable<Event> runAsyncImpl(InvocationContext invocationContext) {](#__codelineno-7-47)[// Direct access example](#__codelineno-7-48)[String agentName = invocationContext.agent.name](#__codelineno-7-49)[String sessionId = invocationContext.session.id](#__codelineno-7-50)[String invocationId = invocationContext.invocationId](#__codelineno-7-51)[System.out.println("Agent " + agent_name + " running in session " + session_id + " for invocation " + invocationId)](#__codelineno-7-52)[// ... agent logic using ctx ...](#__codelineno-7-53)[}](#__codelineno-7-54) -
`ReadonlyContext`

**Where Used:**Provided in scenarios where only read access to basic information is needed and mutation is disallowed (e.g.,`InstructionProvider`

functions). It's also the base class for other contexts.**Purpose:**Offers a safe, read-only view of fundamental contextual details.**Key Contents:**`invocation_id`

,`agent_name`

, and a read-only*view*of the current`state`

.

[# Pseudocode: Instruction provider receiving ReadonlyContext](#__codelineno-8-1)[from google.adk.agents.readonly_context import ReadonlyContext](#__codelineno-8-2)[def my_instruction_provider(context: ReadonlyContext) -> str:](#__codelineno-8-4)[# Read-only access example](#__codelineno-8-5)[user_tier = context.state().get("user_tier", "standard") # Can read state](#__codelineno-8-6)[# context.state['new_key'] = 'value' # This would typically cause an error or be ineffective](#__codelineno-8-7)[return f"Process the request for a {user_tier} user."](#__codelineno-8-8)[// Pseudocode: Instruction provider receiving ReadonlyContext](#__codelineno-9-1)[import { ReadonlyContext } from '@google/adk';](#__codelineno-9-2)[function myInstructionProvider(context: ReadonlyContext): string {](#__codelineno-9-4)[// Read-only access example](#__codelineno-9-5)[// The state object is read-only](#__codelineno-9-6)[const userTier = context.state.get('user_tier') ?? 'standard';](#__codelineno-9-7)[// context.state.set('new_key', 'value'); // This would fail or throw an error](#__codelineno-9-8)[return `Process the request for a ${userTier} user.`;](#__codelineno-9-9)[}](#__codelineno-9-10)[import "google.golang.org/adk/agent"](#__codelineno-10-1)[// Pseudocode: Instruction provider receiving ReadonlyContext](#__codelineno-10-3)[func myInstructionProvider(ctx agent.ReadonlyContext) (string, error) {](#__codelineno-10-4)[// Read-only access example](#__codelineno-10-5)[userTier, err := ctx.ReadonlyState().Get("user_tier")](#__codelineno-10-6)[if err != nil {](#__codelineno-10-7)[userTier = "standard" // Default value](#__codelineno-10-8)[}](#__codelineno-10-9)[// ctx.ReadonlyState() has no Set method since State() is read-only.](#__codelineno-10-10)[return fmt.Sprintf("Process the request for a %v user.", userTier), nil](#__codelineno-10-11)[}](#__codelineno-10-12)[// Pseudocode: Instruction provider receiving ReadonlyContext](#__codelineno-11-1)[import com.google.adk.agents.ReadonlyContext;](#__codelineno-11-2)[public String myInstructionProvider(ReadonlyContext context){](#__codelineno-11-4)[// Read-only access example](#__codelineno-11-5)[String userTier = context.state().get("user_tier", "standard");](#__codelineno-11-6)[context.state().put('new_key', 'value'); //This would typically cause an error](#__codelineno-11-7)[return "Process the request for a " + userTier + " user."](#__codelineno-11-8)[}](#__codelineno-11-9) -
`CallbackContext`

**Where Used:**Passed as`callback_context`

to agent lifecycle callbacks (`before_agent_callback`

,`after_agent_callback`

) and model interaction callbacks (`before_model_callback`

,`after_model_callback`

).**Purpose:**Facilitates inspecting and modifying state, interacting with artifacts, and accessing invocation details*specifically within callbacks*.**Key Capabilities (Adds to**`ReadonlyContext`

):**Mutable**Allows reading`state`

Property:*and writing*to session state. Changes made here (`callback_context.state['key'] = value`

) are tracked and associated with the event generated by the framework after the callback.**Artifact Methods:**`load_artifact(filename)`

and`save_artifact(filename, part)`

methods for interacting with the configured`artifact_service`

.- Direct
`user_content`

access.


[# Pseudocode: Callback receiving CallbackContext](#__codelineno-12-1)[from google.adk.agents.callback_context import CallbackContext](#__codelineno-12-2)[from google.adk.models import LlmRequest](#__codelineno-12-3)[from google.genai import types](#__codelineno-12-4)[from typing import Optional](#__codelineno-12-5)[def my_before_model_cb(callback_context: CallbackContext, request: LlmRequest) -> Optional[types.Content]:](#__codelineno-12-7)[# Read/Write state example](#__codelineno-12-8)[call_count = callback_context.state.get("model_calls", 0)](#__codelineno-12-9)[callback_context.state["model_calls"] = call_count + 1 # Modify state](#__codelineno-12-10)[# Optionally load an artifact](#__codelineno-12-12)[# config_part = callback_context.load_artifact("model_config.json")](#__codelineno-12-13)[print(f"Preparing model call #{call_count + 1} for invocation {callback_context.invocation_id}")](#__codelineno-12-14)[return None # Allow model call to proceed](#__codelineno-12-15)[// Pseudocode: Callback receiving CallbackContext](#__codelineno-13-1)[import { CallbackContext, LlmRequest } from '@google/adk';](#__codelineno-13-2)[import { Content } from '@google/genai';](#__codelineno-13-3)[function myBeforeModelCb(callbackContext: CallbackContext, request: LlmRequest): Content | undefined {](#__codelineno-13-5)[// Read/Write state example](#__codelineno-13-6)[const callCount = (callbackContext.state.get('model_calls') as number) || 0;](#__codelineno-13-7)[callbackContext.state.set('model_calls', callCount + 1); // Modify state](#__codelineno-13-8)[// Optionally load an artifact](#__codelineno-13-10)[// const configPart = await callbackContext.loadArtifact('model_config.json');](#__codelineno-13-11)[console.log(`Preparing model call #${callCount + 1} for invocation ${callbackContext.invocationId}`);](#__codelineno-13-12)[return undefined; // Allow model call to proceed](#__codelineno-13-13)[}](#__codelineno-13-14)[import (](#__codelineno-14-1)["google.golang.org/adk/agent"](#__codelineno-14-2)["google.golang.org/adk/model"](#__codelineno-14-3)[)](#__codelineno-14-4)[// Pseudocode: Callback receiving CallbackContext](#__codelineno-14-6)[func myBeforeModelCb(ctx agent.CallbackContext, req *model.LLMRequest) (*model.LLMResponse, error) {](#__codelineno-14-7)[// Read/Write state example](#__codelineno-14-8)[callCount, err := ctx.State().Get("model_calls")](#__codelineno-14-9)[if err != nil {](#__codelineno-14-10)[callCount = 0 // Default value](#__codelineno-14-11)[}](#__codelineno-14-12)[newCount := callCount.(int) + 1](#__codelineno-14-13)[if err := ctx.State().Set("model_calls", newCount); err != nil {](#__codelineno-14-14)[return nil, err](#__codelineno-14-15)[}](#__codelineno-14-16)[// Optionally load an artifact](#__codelineno-14-18)[// configPart, err := ctx.Artifacts().Load("model_config.json")](#__codelineno-14-19)[fmt.Printf("Preparing model call #%d for invocation %s\n", newCount, ctx.InvocationID())](#__codelineno-14-20)[return nil, nil // Allow model call to proceed](#__codelineno-14-21)[}](#__codelineno-14-22)[// Pseudocode: Callback receiving CallbackContext](#__codelineno-15-1)[import com.google.adk.agents.CallbackContext;](#__codelineno-15-2)[import com.google.adk.models.LlmRequest;](#__codelineno-15-3)[import com.google.genai.types.Content;](#__codelineno-15-4)[import java.util.Optional;](#__codelineno-15-5)[public Maybe<LlmResponse> myBeforeModelCb(CallbackContext callbackContext, LlmRequest request){](#__codelineno-15-7)[// Read/Write state example](#__codelineno-15-8)[callCount = callbackContext.state().get("model_calls", 0)](#__codelineno-15-9)[callbackContext.state().put("model_calls") = callCount + 1 # Modify state](#__codelineno-15-10)[// Optionally load an artifact](#__codelineno-15-12)[// Maybe<Part> configPart = callbackContext.loadArtifact("model_config.json");](#__codelineno-15-13)[System.out.println("Preparing model call " + callCount + 1);](#__codelineno-15-14)[return Maybe.empty(); // Allow model call to proceed](#__codelineno-15-15)[}](#__codelineno-15-16) -
`ToolContext`

**Where Used:**Passed as`tool_context`

to the functions backing`FunctionTool`

s and to tool execution callbacks (`before_tool_callback`

,`after_tool_callback`

).**Purpose:**Provides everything`CallbackContext`

does, plus specialized methods essential for tool execution, like handling authentication, searching memory, and listing artifacts.**Key Capabilities (Adds to**`CallbackContext`

):**Authentication Methods:**`request_credential(auth_config)`

to trigger an auth flow, and`get_auth_response(auth_config)`

to retrieve credentials provided by the user/system.**Artifact Listing:**`list_artifacts()`

to discover available artifacts in the session.**Memory Search:**`search_memory(query)`

to query the configured`memory_service`

.Identifies the specific function call from the LLM that triggered this tool execution, crucial for linking authentication requests or responses back correctly.`function_call_id`

Property:Direct access to the`actions`

Property:`EventActions`

object for this step, allowing the tool to signal state changes, auth requests, etc.


[# Pseudocode: Tool function receiving ToolContext](#__codelineno-16-1)[from google.adk.tools import ToolContext](#__codelineno-16-2)[from typing import Dict, Any](#__codelineno-16-3)[# Assume this function is wrapped by a FunctionTool](#__codelineno-16-5)[def search_external_api(query: str, tool_context: ToolContext) -> Dict[str, Any]:](#__codelineno-16-6)[api_key = tool_context.state.get("api_key")](#__codelineno-16-7)[if not api_key:](#__codelineno-16-8)[# Define required auth config](#__codelineno-16-9)[# auth_config = AuthConfig(...)](#__codelineno-16-10)[# tool_context.request_credential(auth_config) # Request credentials](#__codelineno-16-11)[# Use the 'actions' property to signal the auth request has been made](#__codelineno-16-12)[# tool_context.actions.requested_auth_configs[tool_context.function_call_id] = auth_config](#__codelineno-16-13)[return {"status": "Auth Required"}](#__codelineno-16-14)[# Use the API key...](#__codelineno-16-16)[print(f"Tool executing for query '{query}' using API key. Invocation: {tool_context.invocation_id}")](#__codelineno-16-17)[# Optionally search memory or list artifacts](#__codelineno-16-19)[# relevant_docs = tool_context.search_memory(f"info related to {query}")](#__codelineno-16-20)[# available_files = tool_context.list_artifacts()](#__codelineno-16-21)[return {"result": f"Data for {query} fetched."}](#__codelineno-16-23)[// Pseudocode: Tool function receiving ToolContext](#__codelineno-17-1)[import { ToolContext } from '@google/adk';](#__codelineno-17-2)[// __Assume this function is wrapped by a FunctionTool__](#__codelineno-17-4)[function searchExternalApi(query: string, toolContext: ToolContext): { [key: string]: string } {](#__codelineno-17-5)[const apiKey = toolContext.state.get('api_key') as string;](#__codelineno-17-6)[if (!apiKey) {](#__codelineno-17-7)[// Define required auth config](#__codelineno-17-8)[// const authConfig = new AuthConfig(...);](#__codelineno-17-9)[// toolContext.requestCredential(authConfig); // Request credentials](#__codelineno-17-10)[// The 'actions' property is now automatically updated by requestCredential](#__codelineno-17-11)[return { status: 'Auth Required' };](#__codelineno-17-12)[}](#__codelineno-17-13)[// Use the API key...](#__codelineno-17-15)[console.log(`Tool executing for query '${query}' using API key. Invocation: ${toolContext.invocationId}`);](#__codelineno-17-16)[// Optionally search memory or list artifacts](#__codelineno-17-18)[// Note: accessing services like memory/artifacts is typically async in TS,](#__codelineno-17-19)[// so you would need to mark this function 'async' if you reused them.](#__codelineno-17-20)[// toolContext.searchMemory(`info related to ${query}`).then(...)](#__codelineno-17-21)[// toolContext.listArtifacts().then(...)](#__codelineno-17-22)[return { result: `Data for ${query} fetched.` };](#__codelineno-17-24)[}](#__codelineno-17-25)[import "google.golang.org/adk/tool"](#__codelineno-18-1)[// Pseudocode: Tool function receiving ToolContext](#__codelineno-18-3)[type searchExternalAPIArgs struct {](#__codelineno-18-4)[Query string `json:"query" jsonschema:"The query to search for."`](#__codelineno-18-5)[}](#__codelineno-18-6)[func searchExternalAPI(tc tool.Context, input searchExternalAPIArgs) (string, error) {](#__codelineno-18-8)[apiKey, err := tc.State().Get("api_key")](#__codelineno-18-9)[if err != nil || apiKey == "" {](#__codelineno-18-10)[// In a real scenario, you would define and request credentials here.](#__codelineno-18-11)[// This is a conceptual placeholder.](#__codelineno-18-12)[return "", fmt.Errorf("auth required")](#__codelineno-18-13)[}](#__codelineno-18-14)[// Use the API key...](#__codelineno-18-16)[fmt.Printf("Tool executing for query '%s' using API key. Invocation: %s\n", input.Query, tc.InvocationID())](#__codelineno-18-17)[// Optionally search memory or list artifacts](#__codelineno-18-19)[// relevantDocs, _ := tc.SearchMemory(tc, "info related to %s", input.Query))](#__codelineno-18-20)[// availableFiles, _ := tc.Artifacts().List()](#__codelineno-18-21)[return fmt.Sprintf("Data for %s fetched.", input.Query), nil](#__codelineno-18-23)[}](#__codelineno-18-24)[// Pseudocode: Tool function receiving ToolContext](#__codelineno-19-1)[import com.google.adk.tools.ToolContext;](#__codelineno-19-2)[import java.util.HashMap;](#__codelineno-19-3)[import java.util.Map;](#__codelineno-19-4)[// Assume this function is wrapped by a FunctionTool](#__codelineno-19-6)[public Map<String, Object> searchExternalApi(String query, ToolContext toolContext){](#__codelineno-19-7)[String apiKey = toolContext.state.get("api_key");](#__codelineno-19-8)[if(apiKey.isEmpty()){](#__codelineno-19-9)[// Define required auth config](#__codelineno-19-10)[// authConfig = AuthConfig(...);](#__codelineno-19-11)[// toolContext.requestCredential(authConfig); # Request credentials](#__codelineno-19-12)[// Use the 'actions' property to signal the auth request has been made](#__codelineno-19-13)[...](#__codelineno-19-14)[return Map.of("status", "Auth Required");](#__codelineno-19-15)[// Use the API key...](#__codelineno-19-17)[System.out.println("Tool executing for query " + query + " using API key. ");](#__codelineno-19-18)[// Optionally list artifacts](#__codelineno-19-20)[// Single<List<String>> availableFiles = toolContext.listArtifacts();](#__codelineno-19-21)[return Map.of("result", "Data for " + query + " fetched");](#__codelineno-19-23)[}](#__codelineno-19-24)

Understanding these different context objects and when to use them is key to effectively managing state, accessing services, and controlling the flow of your ADK application. The next section will detail common tasks you can perform using these contexts.

## Common Tasks Using Context[¶](#common-tasks-using-context)

Now that you understand the different context objects, let's focus on how to use them for common tasks when building your agents and tools.

### Accessing Information[¶](#accessing-information)

You'll frequently need to read information stored within the context.

-
**Reading Session State:**Access data saved in previous steps or user/app-level settings. Use dictionary-like access on the`state`

property.[# Pseudocode: In a Tool function](#__codelineno-20-1)[from google.adk.tools import ToolContext](#__codelineno-20-2)[def my_tool(tool_context: ToolContext, **kwargs):](#__codelineno-20-4)[user_pref = tool_context.state.get("user_display_preference", "default_mode")](#__codelineno-20-5)[api_endpoint = tool_context.state.get("app:api_endpoint") # Read app-level state](#__codelineno-20-6)[if user_pref == "dark_mode":](#__codelineno-20-8)[# ... apply dark mode logic ...](#__codelineno-20-9)[pass](#__codelineno-20-10)[print(f"Using API endpoint: {api_endpoint}")](#__codelineno-20-11)[# ... rest of tool logic ...](#__codelineno-20-12)[# Pseudocode: In a Callback function](#__codelineno-20-14)[from google.adk.agents.callback_context import CallbackContext](#__codelineno-20-15)[def my_callback(callback_context: CallbackContext, **kwargs):](#__codelineno-20-17)[last_tool_result = callback_context.state.get("temp:last_api_result") # Read temporary state](#__codelineno-20-18)[if last_tool_result:](#__codelineno-20-19)[print(f"Found temporary result from last tool: {last_tool_result}")](#__codelineno-20-20)[# ... callback logic ...](#__codelineno-20-21)[// Pseudocode: In a Tool function](#__codelineno-21-1)[import { ToolContext } from '@google/adk';](#__codelineno-21-2)[async function myTool(toolContext: ToolContext) {](#__codelineno-21-4)[const userPref = toolContext.state.get('user_display_preference', 'default_mode');](#__codelineno-21-5)[const apiEndpoint = toolContext.state.get('app:api_endpoint'); // Read app-level state](#__codelineno-21-6)[if (userPref === 'dark_mode') {](#__codelineno-21-8)[// ... apply dark mode logic ...](#__codelineno-21-9)[}](#__codelineno-21-10)[console.log(`Using API endpoint: ${apiEndpoint}`);](#__codelineno-21-11)[// ... rest of tool logic ...](#__codelineno-21-12)[}](#__codelineno-21-13)[// Pseudocode: In a Callback function](#__codelineno-21-15)[import { CallbackContext } from '@google/adk';](#__codelineno-21-16)[function myCallback(callbackContext: CallbackContext) {](#__codelineno-21-18)[const lastToolResult = callbackContext.state.get('temp:last_api_result'); // Read temporary state](#__codelineno-21-19)[if (lastToolResult) {](#__codelineno-21-20)[console.log(`Found temporary result from last tool: ${lastToolResult}`);](#__codelineno-21-21)[}](#__codelineno-21-22)[// ... callback logic ...](#__codelineno-21-23)[}](#__codelineno-21-24)[import (](#__codelineno-22-1)["google.golang.org/adk/agent"](#__codelineno-22-2)["google.golang.org/adk/session"](#__codelineno-22-3)["google.golang.org/adk/tool"](#__codelineno-22-4)["google.golang.org/genai"](#__codelineno-22-5)[)](#__codelineno-22-6)[// Pseudocode: In a Tool function](#__codelineno-22-8)[type toolArgs struct {](#__codelineno-22-9)[// Define tool-specific arguments here](#__codelineno-22-10)[}](#__codelineno-22-11)[type toolResults struct {](#__codelineno-22-13)[// Define tool-specific results here](#__codelineno-22-14)[}](#__codelineno-22-15)[// Example tool function demonstrating state access](#__codelineno-22-17)[func myTool(tc tool.Context, input toolArgs) (toolResults, error) {](#__codelineno-22-18)[userPref, err := tc.State().Get("user_display_preference")](#__codelineno-22-19)[if err != nil {](#__codelineno-22-20)[userPref = "default_mode"](#__codelineno-22-21)[}](#__codelineno-22-22)[apiEndpoint, _ := tc.State().Get("app:api_endpoint") // Read app-level state](#__codelineno-22-23)[if userPref == "dark_mode" {](#__codelineno-22-25)[// ... apply dark mode logic ...](#__codelineno-22-26)[}](#__codelineno-22-27)[fmt.Printf("Using API endpoint: %v\n", apiEndpoint)](#__codelineno-22-28)[// ... rest of tool logic ...](#__codelineno-22-29)[return toolResults{}, nil](#__codelineno-22-30)[}](#__codelineno-22-31)[// Pseudocode: In a Callback function](#__codelineno-22-34)[func myCallback(ctx agent.CallbackContext) (*genai.Content, error) {](#__codelineno-22-35)[lastToolResult, err := ctx.State().Get("temp:last_api_result") // Read temporary state](#__codelineno-22-36)[if err == nil {](#__codelineno-22-37)[fmt.Printf("Found temporary result from last tool: %v\n", lastToolResult)](#__codelineno-22-38)[} else {](#__codelineno-22-39)[fmt.Println("No temporary result found.")](#__codelineno-22-40)[}](#__codelineno-22-41)[// ... callback logic ...](#__codelineno-22-42)[return nil, nil](#__codelineno-22-43)[}](#__codelineno-22-44)[// Pseudocode: In a Tool function](#__codelineno-23-1)[import com.google.adk.tools.ToolContext;](#__codelineno-23-2)[public void myTool(ToolContext toolContext){](#__codelineno-23-4)[String userPref = toolContext.state().get("user_display_preference");](#__codelineno-23-5)[String apiEndpoint = toolContext.state().get("app:api_endpoint"); // Read app-level state](#__codelineno-23-6)[if(userPref.equals("dark_mode")){](#__codelineno-23-7)[// ... apply dark mode logic ...](#__codelineno-23-8)[pass](#__codelineno-23-9)[}](#__codelineno-23-10)[System.out.println("Using API endpoint: " + api_endpoint);](#__codelineno-23-11)[// ... rest of tool logic ...](#__codelineno-23-12)[}](#__codelineno-23-13)[// Pseudocode: In a Callback function](#__codelineno-23-16)[import com.google.adk.agents.CallbackContext;](#__codelineno-23-17)[public void myCallback(CallbackContext callbackContext){](#__codelineno-23-19)[String lastToolResult = (String) callbackContext.state().get("temp:last_api_result"); // Read temporary state](#__codelineno-23-20)[}](#__codelineno-23-21)[if(!(lastToolResult.isEmpty())){](#__codelineno-23-22)[System.out.println("Found temporary result from last tool: " + lastToolResult);](#__codelineno-23-23)[}](#__codelineno-23-24)[// ... callback logic ...](#__codelineno-23-25) -
**Getting Current Identifiers:**Useful for logging or custom logic based on the current operation.[# Pseudocode: In any context (ToolContext shown)](#__codelineno-24-1)[from google.adk.tools import ToolContext](#__codelineno-24-2)[def log_tool_usage(tool_context: ToolContext, **kwargs):](#__codelineno-24-4)[agent_name = tool_context.agent_name](#__codelineno-24-5)[inv_id = tool_context.invocation_id](#__codelineno-24-6)[func_call_id = getattr(tool_context, 'function_call_id', 'N/A') # Specific to ToolContext](#__codelineno-24-7)[print(f"Log: Invocation={inv_id}, Agent={agent_name}, FunctionCallID={func_call_id} - Tool Executed.")](#__codelineno-24-9)[// Pseudocode: In any context (ToolContext shown)](#__codelineno-25-1)[import { ToolContext } from '@google/adk';](#__codelineno-25-2)[function logToolUsage(toolContext: ToolContext) {](#__codelineno-25-4)[const agentName = toolContext.agentName;](#__codelineno-25-5)[const invId = toolContext.invocationId;](#__codelineno-25-6)[const functionCallId = toolContext.functionCallId ?? 'N/A'; // Specific to ToolContext](#__codelineno-25-7)[console.log(`Log: Invocation=${invId}, Agent=${agentName}, FunctionCallID=${functionCallId} - Tool Executed.`);](#__codelineno-25-9)[}](#__codelineno-25-10)[import "google.golang.org/adk/tool"](#__codelineno-26-1)[// Pseudocode: In any context (ToolContext shown)](#__codelineno-26-3)[type logToolUsageArgs struct{}](#__codelineno-26-4)[type logToolUsageResult struct {](#__codelineno-26-5)[Status string `json:"status"`](#__codelineno-26-6)[}](#__codelineno-26-7)[func logToolUsage(tc tool.Context, args logToolUsageArgs) (logToolUsageResult, error) {](#__codelineno-26-9)[agentName := tc.AgentName()](#__codelineno-26-10)[invID := tc.InvocationID()](#__codelineno-26-11)[funcCallID := tc.FunctionCallID()](#__codelineno-26-12)[fmt.Printf("Log: Invocation=%s, Agent=%s, FunctionCallID=%s - Tool Executed.\n", invID, agentName, funcCallID)](#__codelineno-26-14)[return logToolUsageResult{Status: "Logged successfully"}, nil](#__codelineno-26-15)[}](#__codelineno-26-16)[// Pseudocode: In any context (ToolContext shown)](#__codelineno-27-1)[import com.google.adk.tools.ToolContext;](#__codelineno-27-2)[public void logToolUsage(ToolContext toolContext){](#__codelineno-27-4)[String agentName = toolContext.agentName;](#__codelineno-27-5)[String invId = toolContext.invocationId;](#__codelineno-27-6)[String functionCallId = toolContext.functionCallId().get(); // Specific to ToolContext](#__codelineno-27-7)[System.out.println("Log: Invocation= " + invId &+ " Agent= " + agentName);](#__codelineno-27-8)[}](#__codelineno-27-9) -
**Accessing the Initial User Input:**Refer back to the message that started the current invocation.[# Pseudocode: In a Callback](#__codelineno-28-1)[from google.adk.agents.callback_context import CallbackContext](#__codelineno-28-2)[def check_initial_intent(callback_context: CallbackContext, **kwargs):](#__codelineno-28-4)[initial_text = "N/A"](#__codelineno-28-5)[if callback_context.user_content and callback_context.user_content.parts:](#__codelineno-28-6)[initial_text = callback_context.user_content.parts[0].text or "Non-text input"](#__codelineno-28-7)[print(f"This invocation started with user input: '{initial_text}'")](#__codelineno-28-9)[# Pseudocode: In an Agent's _run_async_impl](#__codelineno-28-11)[# async def _run_async_impl(self, ctx: InvocationContext) -> AsyncGenerator[Event, None]:](#__codelineno-28-12)[# if ctx.user_content and ctx.user_content.parts:](#__codelineno-28-13)[# initial_text = ctx.user_content.parts[0].text](#__codelineno-28-14)[# print(f"Agent logic remembering initial query: {initial_text}")](#__codelineno-28-15)[# ...](#__codelineno-28-16)[// Pseudocode: In a Callback](#__codelineno-29-1)[import { CallbackContext } from '@google/adk';](#__codelineno-29-2)[function checkInitialIntent(callbackContext: CallbackContext) {](#__codelineno-29-4)[let initialText = 'N/A';](#__codelineno-29-5)[const userContent = callbackContext.userContent;](#__codelineno-29-6)[if (userContent?.parts?.length) {](#__codelineno-29-7)[initialText = userContent.parts[0].text ?? 'Non-text input';](#__codelineno-29-8)[}](#__codelineno-29-9)[console.log(`This invocation started with user input: '${initialText}'`);](#__codelineno-29-11)[}](#__codelineno-29-12)[import (](#__codelineno-30-1)["google.golang.org/adk/agent"](#__codelineno-30-2)["google.golang.org/genai"](#__codelineno-30-3)[)](#__codelineno-30-4)[// Pseudocode: In a Callback](#__codelineno-30-6)[func logInitialUserInput(ctx agent.CallbackContext) (*genai.Content, error) {](#__codelineno-30-7)[userContent := ctx.UserContent()](#__codelineno-30-8)[if userContent != nil && len(userContent.Parts) > 0 {](#__codelineno-30-9)[if text := userContent.Parts[0].Text; text != "" {](#__codelineno-30-10)[fmt.Printf("User's initial input for this turn: '%s'\n", text)](#__codelineno-30-11)[}](#__codelineno-30-12)[}](#__codelineno-30-13)[return nil, nil // No modification](#__codelineno-30-14)[}](#__codelineno-30-15)[// Pseudocode: In a Callback](#__codelineno-31-1)[import com.google.adk.agents.CallbackContext;](#__codelineno-31-2)[public void checkInitialIntent(CallbackContext callbackContext){](#__codelineno-31-4)[String initialText = "N/A";](#__codelineno-31-5)[if((!(callbackContext.userContent().isEmpty())) && (!(callbackContext.userContent().parts.isEmpty()))){](#__codelineno-31-6)[initialText = cbx.userContent().get().parts().get().get(0).text().get();](#__codelineno-31-7)[...](#__codelineno-31-8)[System.out.println("This invocation started with user input: " + initialText)](#__codelineno-31-9)[}](#__codelineno-31-10)[}](#__codelineno-31-11)

### Managing State[¶](#managing-state)

State is crucial for memory and data flow. When you modify state using `CallbackContext`

or `ToolContext`

, the changes are automatically tracked and persisted by the framework.

-
**How it Works:**Writing to`callback_context.state['my_key'] = my_value`

or`tool_context.state['my_key'] = my_value`

adds this change to the`EventActions.state_delta`

associated with the current step's event. The`SessionService`

then applies these deltas when persisting the event. -
**Passing Data Between Tools**[# Pseudocode: Tool 1 - Fetches user ID](#__codelineno-32-1)[from google.adk.tools import ToolContext](#__codelineno-32-2)[import uuid](#__codelineno-32-3)[def get_user_profile(tool_context: ToolContext) -> dict:](#__codelineno-32-5)[user_id = str(uuid.uuid4()) # Simulate fetching ID](#__codelineno-32-6)[# Save the ID to state for the next tool](#__codelineno-32-7)[tool_context.state["temp:current_user_id"] = user_id](#__codelineno-32-8)[return {"profile_status": "ID generated"}](#__codelineno-32-9)[# Pseudocode: Tool 2 - Uses user ID from state](#__codelineno-32-11)[def get_user_orders(tool_context: ToolContext) -> dict:](#__codelineno-32-12)[user_id = tool_context.state.get("temp:current_user_id")](#__codelineno-32-13)[if not user_id:](#__codelineno-32-14)[return {"error": "User ID not found in state"}](#__codelineno-32-15)[print(f"Fetching orders for user ID: {user_id}")](#__codelineno-32-17)[# ... logic to fetch orders using user_id ...](#__codelineno-32-18)[return {"orders": ["order123", "order456"]}](#__codelineno-32-19)[// Pseudocode: Tool 1 - Fetches user ID](#__codelineno-33-1)[import { ToolContext } from '@google/adk';](#__codelineno-33-2)[import { v4 as uuidv4 } from 'uuid';](#__codelineno-33-3)[function getUserProfile(toolContext: ToolContext): Record<string, string> {](#__codelineno-33-5)[const userId = uuidv4(); // Simulate fetching ID](#__codelineno-33-6)[// Save the ID to state for the next tool](#__codelineno-33-7)[toolContext.state.set('temp:current_user_id', userId);](#__codelineno-33-8)[return { profile_status: 'ID generated' };](#__codelineno-33-9)[}](#__codelineno-33-10)[// Pseudocode: Tool 2 - Uses user ID from state](#__codelineno-33-12)[function getUserOrders(toolContext: ToolContext): Record<string, string | string[]> {](#__codelineno-33-13)[const userId = toolContext.state.get('temp:current_user_id');](#__codelineno-33-14)[if (!userId) {](#__codelineno-33-15)[return { error: 'User ID not found in state' };](#__codelineno-33-16)[}](#__codelineno-33-17)[console.log(`Fetching orders for user ID: ${userId}`);](#__codelineno-33-19)[// ... logic to fetch orders using user_id ...](#__codelineno-33-20)[return { orders: ['order123', 'order456'] };](#__codelineno-33-21)[}](#__codelineno-33-22)[import "google.golang.org/adk/tool"](#__codelineno-34-1)[// Pseudocode: Tool 1 - Fetches user ID](#__codelineno-34-3)[type GetUserProfileArgs struct {](#__codelineno-34-4)[}](#__codelineno-34-5)[func getUserProfile(tc tool.Context, input GetUserProfileArgs) (string, error) {](#__codelineno-34-7)[// A random user ID for demonstration purposes](#__codelineno-34-8)[userID := "random_user_456"](#__codelineno-34-9)[// Save the ID to state for the next tool](#__codelineno-34-11)[if err := tc.State().Set("temp:current_user_id", userID); err != nil {](#__codelineno-34-12)[return "", fmt.Errorf("failed to set user ID in state: %w", err)](#__codelineno-34-13)[}](#__codelineno-34-14)[return "ID generated", nil](#__codelineno-34-15)[}](#__codelineno-34-16)[// Pseudocode: Tool 2 - Uses user ID from state](#__codelineno-34-19)[type GetUserOrdersArgs struct {](#__codelineno-34-20)[}](#__codelineno-34-21)[type getUserOrdersResult struct {](#__codelineno-34-23)[Orders []string `json:"orders"`](#__codelineno-34-24)[}](#__codelineno-34-25)[func getUserOrders(tc tool.Context, input GetUserOrdersArgs) (*getUserOrdersResult, error) {](#__codelineno-34-27)[userID, err := tc.State().Get("temp:current_user_id")](#__codelineno-34-28)[if err != nil {](#__codelineno-34-29)[return &getUserOrdersResult{}, fmt.Errorf("user ID not found in state")](#__codelineno-34-30)[}](#__codelineno-34-31)[fmt.Printf("Fetching orders for user ID: %v\n", userID)](#__codelineno-34-33)[// ... logic to fetch orders using user_id ...](#__codelineno-34-34)[return &getUserOrdersResult{Orders: []string{"order123", "order456"}}, nil](#__codelineno-34-35)[}](#__codelineno-34-36)[// Pseudocode: Tool 1 - Fetches user ID](#__codelineno-35-1)[import com.google.adk.tools.ToolContext;](#__codelineno-35-2)[import java.util.UUID;](#__codelineno-35-3)[public Map<String, String> getUserProfile(ToolContext toolContext){](#__codelineno-35-5)[String userId = UUID.randomUUID().toString();](#__codelineno-35-6)[// Save the ID to state for the next tool](#__codelineno-35-7)[toolContext.state().put("temp:current_user_id", user_id);](#__codelineno-35-8)[return Map.of("profile_status", "ID generated");](#__codelineno-35-9)[}](#__codelineno-35-10)[// Pseudocode: Tool 2 - Uses user ID from state](#__codelineno-35-12)[public Map<String, String> getUserOrders(ToolContext toolContext){](#__codelineno-35-13)[String userId = toolContext.state().get("temp:current_user_id");](#__codelineno-35-14)[if(userId.isEmpty()){](#__codelineno-35-15)[return Map.of("error", "User ID not found in state");](#__codelineno-35-16)[}](#__codelineno-35-17)[System.out.println("Fetching orders for user id: " + userId);](#__codelineno-35-18)[// ... logic to fetch orders using user_id ...](#__codelineno-35-19)[return Map.of("orders", "order123");](#__codelineno-35-20)[}](#__codelineno-35-21) -
**Updating User Preferences:**[# Pseudocode: Tool or Callback identifies a preference](#__codelineno-36-1)[from google.adk.tools import ToolContext # Or CallbackContext](#__codelineno-36-2)[def set_user_preference(tool_context: ToolContext, preference: str, value: str) -> dict:](#__codelineno-36-4)[# Use 'user:' prefix for user-level state (if using a persistent SessionService)](#__codelineno-36-5)[state_key = f"user:{preference}"](#__codelineno-36-6)[tool_context.state[state_key] = value](#__codelineno-36-7)[print(f"Set user preference '{preference}' to '{value}'")](#__codelineno-36-8)[return {"status": "Preference updated"}](#__codelineno-36-9)[// Pseudocode: Tool or Callback identifies a preference](#__codelineno-37-1)[import { ToolContext } from '@google/adk'; // Or CallbackContext](#__codelineno-37-2)[function setUserPreference(toolContext: ToolContext, preference: string, value: string): Record<string, string> {](#__codelineno-37-4)[// Use 'user:' prefix for user-level state (if using a persistent SessionService)](#__codelineno-37-5)[const stateKey = `user:${preference}`;](#__codelineno-37-6)[toolContext.state.set(stateKey, value);](#__codelineno-37-7)[console.log(`Set user preference '${preference}' to '${value}'`);](#__codelineno-37-8)[return { status: 'Preference updated' };](#__codelineno-37-9)[}](#__codelineno-37-10)[import "google.golang.org/adk/tool"](#__codelineno-38-1)[// Pseudocode: Tool or Callback identifies a preference](#__codelineno-38-3)[type setUserPreferenceArgs struct {](#__codelineno-38-4)[Preference string `json:"preference" jsonschema:"The name of the preference to set."`](#__codelineno-38-5)[Value string `json:"value" jsonschema:"The value to set for the preference."`](#__codelineno-38-6)[}](#__codelineno-38-7)[type setUserPreferenceResult struct {](#__codelineno-38-9)[Status string `json:"status"`](#__codelineno-38-10)[}](#__codelineno-38-11)[func setUserPreference(tc tool.Context, args setUserPreferenceArgs) (setUserPreferenceResult, error) {](#__codelineno-38-13)[// Use 'user:' prefix for user-level state (if using a persistent SessionService)](#__codelineno-38-14)[stateKey := fmt.Sprintf("user:%s", args.Preference)](#__codelineno-38-15)[if err := tc.State().Set(stateKey, args.Value); err != nil {](#__codelineno-38-16)[return setUserPreferenceResult{}, fmt.Errorf("failed to set preference in state: %w", err)](#__codelineno-38-17)[}](#__codelineno-38-18)[fmt.Printf("Set user preference '%s' to '%s'\n", args.Preference, args.Value)](#__codelineno-38-19)[return setUserPreferenceResult{Status: "Preference updated"}, nil](#__codelineno-38-20)[}](#__codelineno-38-21)[// Pseudocode: Tool or Callback identifies a preference](#__codelineno-39-1)[import com.google.adk.tools.ToolContext; // Or CallbackContext](#__codelineno-39-2)[public Map<String, String> setUserPreference(ToolContext toolContext, String preference, String value){](#__codelineno-39-4)[// Use 'user:' prefix for user-level state (if using a persistent SessionService)](#__codelineno-39-5)[String stateKey = "user:" + preference;](#__codelineno-39-6)[toolContext.state().put(stateKey, value);](#__codelineno-39-7)[System.out.println("Set user preference '" + preference + "' to '" + value + "'");](#__codelineno-39-8)[return Map.of("status", "Preference updated");](#__codelineno-39-9)[}](#__codelineno-39-10) -
**State Prefixes:**While basic state is session-specific, prefixes like`app:`

and`user:`

can be used with persistent`SessionService`

implementations (like`DatabaseSessionService`

or`VertexAiSessionService`

) to indicate broader scope (app-wide or user-wide across sessions).`temp:`

can denote data only relevant within the current invocation.

### Working with Artifacts[¶](#working-with-artifacts)

Use artifacts to handle files or large data blobs associated with the session. Common use case: processing uploaded documents.

-
**Document Summarizer Example Flow:**-
**Ingest Reference (e.g., in a Setup Tool or Callback):**Save the*path or URI*of the document, not the entire content, as an artifact.[# Pseudocode: In a callback or initial tool](#__codelineno-40-1)[from google.adk.agents.callback_context import CallbackContext # Or ToolContext](#__codelineno-40-2)[from google.genai import types](#__codelineno-40-3)[def save_document_reference(context: CallbackContext, file_path: str) -> None:](#__codelineno-40-5)[# Assume file_path is something like "gs://my-bucket/docs/report.pdf" or "/local/path/to/report.pdf"](#__codelineno-40-6)[try:](#__codelineno-40-7)[# Create a Part containing the path/URI text](#__codelineno-40-8)[artifact_part = types.Part(text=file_path)](#__codelineno-40-9)[version = context.save_artifact("document_to_summarize.txt", artifact_part)](#__codelineno-40-10)[print(f"Saved document reference '{file_path}' as artifact version {version}")](#__codelineno-40-11)[# Store the filename in state if needed by other tools](#__codelineno-40-12)[context.state["temp:doc_artifact_name"] = "document_to_summarize.txt"](#__codelineno-40-13)[except ValueError as e:](#__codelineno-40-14)[print(f"Error saving artifact: {e}") # E.g., Artifact service not configured](#__codelineno-40-15)[except Exception as e:](#__codelineno-40-16)[print(f"Unexpected error saving artifact reference: {e}")](#__codelineno-40-17)[# Example usage:](#__codelineno-40-19)[# save_document_reference(callback_context, "gs://my-bucket/docs/report.pdf")](#__codelineno-40-20)[// Pseudocode: In a callback or initial tool](#__codelineno-41-1)[import { CallbackContext } from '@google/adk'; // Or ToolContext](#__codelineno-41-2)[import type { Part } from '@google/genai';](#__codelineno-41-3)[async function saveDocumentReference(context: CallbackContext, filePath: string) {](#__codelineno-41-5)[// Assume filePath is something like "gs://my-bucket/docs/report.pdf" or "/local/path/to/report.pdf"](#__codelineno-41-6)[try {](#__codelineno-41-7)[// Create a Part containing the path/URI text](#__codelineno-41-8)[const artifactPart: Part = { text: filePath };](#__codelineno-41-9)[const version = await context.saveArtifact('document_to_summarize.txt', artifactPart);](#__codelineno-41-10)[console.log(`Saved document reference '${filePath}' as artifact version ${version}`);](#__codelineno-41-11)[// Store the filename in state if needed by other tools](#__codelineno-41-12)[context.state.set('temp:doc_artifact_name', 'document_to_summarize.txt');](#__codelineno-41-13)[} catch (e) {](#__codelineno-41-14)[console.error(`Unexpected error saving artifact reference: ${e}`);](#__codelineno-41-15)[}](#__codelineno-41-16)[}](#__codelineno-41-17)[// Example usage:](#__codelineno-41-19)[// saveDocumentReference(callbackContext, "gs://my-bucket/docs/report.pdf");](#__codelineno-41-20)[import (](#__codelineno-42-1)["google.golang.org/adk/tool"](#__codelineno-42-2)["google.golang.org/genai"](#__codelineno-42-3)[)](#__codelineno-42-4)[// Adapt the saveDocumentReference callback into a tool for this example.](#__codelineno-42-6)[type saveDocRefArgs struct {](#__codelineno-42-7)[FilePath string `json:"file_path" jsonschema:"The path to the file to save."`](#__codelineno-42-8)[}](#__codelineno-42-9)[type saveDocRefResult struct {](#__codelineno-42-11)[Status string `json:"status"`](#__codelineno-42-12)[}](#__codelineno-42-13)[func saveDocRef(tc tool.Context, args saveDocRefArgs) (saveDocRefResult, error) {](#__codelineno-42-15)[artifactPart := genai.NewPartFromText(args.FilePath)](#__codelineno-42-16)[_, err := tc.Artifacts().Save(tc, "document_to_summarize.txt", artifactPart)](#__codelineno-42-17)[if err != nil {](#__codelineno-42-18)[return saveDocRefResult{}, err](#__codelineno-42-19)[}](#__codelineno-42-20)[fmt.Printf("Saved document reference '%s' as artifact\n", args.FilePath)](#__codelineno-42-21)[if err := tc.State().Set("temp:doc_artifact_name", "document_to_summarize.txt"); err != nil {](#__codelineno-42-22)[return saveDocRefResult{}, fmt.Errorf("failed to set artifact name in state")](#__codelineno-42-23)[}](#__codelineno-42-24)[return saveDocRefResult{"Reference saved"}, nil](#__codelineno-42-25)[}](#__codelineno-42-26)[// Pseudocode: In a callback or initial tool](#__codelineno-43-1)[import com.google.adk.agents.CallbackContext;](#__codelineno-43-2)[import com.google.genai.types.Content;](#__codelineno-43-3)[import com.google.genai.types.Part;](#__codelineno-43-4)[pubic void saveDocumentReference(CallbackContext context, String filePath){](#__codelineno-43-7)[// Assume file_path is something like "gs://my-bucket/docs/report.pdf" or "/local/path/to/report.pdf"](#__codelineno-43-8)[try{](#__codelineno-43-9)[// Create a Part containing the path/URI text](#__codelineno-43-10)[Part artifactPart = types.Part(filePath)](#__codelineno-43-11)[Optional<Integer> version = context.saveArtifact("document_to_summarize.txt", artifactPart)](#__codelineno-43-12)[System.out.println("Saved document reference" + filePath + " as artifact version " + version);](#__codelineno-43-13)[// Store the filename in state if needed by other tools](#__codelineno-43-14)[context.state().put("temp:doc_artifact_name", "document_to_summarize.txt");](#__codelineno-43-15)[} catch(Exception e){](#__codelineno-43-16)[System.out.println("Unexpected error saving artifact reference: " + e);](#__codelineno-43-17)[}](#__codelineno-43-18)[}](#__codelineno-43-19)[// Example usage:](#__codelineno-43-21)[// saveDocumentReference(context, "gs://my-bucket/docs/report.pdf")](#__codelineno-43-22) -
**Summarizer Tool:**Load the artifact to get the path/URI, read the actual document content using appropriate libraries, summarize, and return the result.[# Pseudocode: In the Summarizer tool function](#__codelineno-44-1)[from google.adk.tools import ToolContext](#__codelineno-44-2)[from google.genai import types](#__codelineno-44-3)[# Assume libraries like google.cloud.storage or built-in open are available](#__codelineno-44-4)[# Assume a 'summarize_text' function exists](#__codelineno-44-5)[# from my_summarizer_lib import summarize_text](#__codelineno-44-6)[def summarize_document_tool(tool_context: ToolContext) -> dict:](#__codelineno-44-8)[artifact_name = tool_context.state.get("temp:doc_artifact_name")](#__codelineno-44-9)[if not artifact_name:](#__codelineno-44-10)[return {"error": "Document artifact name not found in state."}](#__codelineno-44-11)[try:](#__codelineno-44-13)[# 1. Load the artifact part containing the path/URI](#__codelineno-44-14)[artifact_part = tool_context.load_artifact(artifact_name)](#__codelineno-44-15)[if not artifact_part or not artifact_part.text:](#__codelineno-44-16)[return {"error": f"Could not load artifact or artifact has no text path: {artifact_name}"}](#__codelineno-44-17)[file_path = artifact_part.text](#__codelineno-44-19)[print(f"Loaded document reference: {file_path}")](#__codelineno-44-20)[# 2. Read the actual document content (outside ADK context)](#__codelineno-44-22)[document_content = ""](#__codelineno-44-23)[if file_path.startswith("gs://"):](#__codelineno-44-24)[# Example: Use GCS client library to download/read](#__codelineno-44-25)[# from google.cloud import storage](#__codelineno-44-26)[# client = storage.Client()](#__codelineno-44-27)[# blob = storage.Blob.from_string(file_path, client=client)](#__codelineno-44-28)[# document_content = blob.download_as_text() # Or bytes depending on format](#__codelineno-44-29)[pass # Replace with actual GCS reading logic](#__codelineno-44-30)[elif file_path.startswith("/"):](#__codelineno-44-31)[# Example: Use local file system](#__codelineno-44-32)[with open(file_path, 'r', encoding='utf-8') as f:](#__codelineno-44-33)[document_content = f.read()](#__codelineno-44-34)[else:](#__codelineno-44-35)[return {"error": f"Unsupported file path scheme: {file_path}"}](#__codelineno-44-36)[# 3. Summarize the content](#__codelineno-44-38)[if not document_content:](#__codelineno-44-39)[return {"error": "Failed to read document content."}](#__codelineno-44-40)[# summary = summarize_text(document_content) # Call your summarization logic](#__codelineno-44-42)[summary = f"Summary of content from {file_path}" # Placeholder](#__codelineno-44-43)[return {"summary": summary}](#__codelineno-44-45)[except ValueError as e:](#__codelineno-44-47)[return {"error": f"Artifact service error: {e}"}](#__codelineno-44-48)[except FileNotFoundError:](#__codelineno-44-49)[return {"error": f"Local file not found: {file_path}"}](#__codelineno-44-50)[# except Exception as e: # Catch specific exceptions for GCS etc.](#__codelineno-44-51)[# return {"error": f"Error reading document {file_path}: {e}"}](#__codelineno-44-52)[// Pseudocode: In the Summarizer tool function](#__codelineno-45-1)[import { ToolContext } from '@google/adk';](#__codelineno-45-2)[async function summarizeDocumentTool(toolContext: ToolContext): Promise<Record<string, string>> {](#__codelineno-45-4)[const artifactName = toolContext.state.get('temp:doc_artifact_name') as string;](#__codelineno-45-5)[if (!artifactName) {](#__codelineno-45-6)[return { error: 'Document artifact name not found in state.' };](#__codelineno-45-7)[}](#__codelineno-45-8)[try {](#__codelineno-45-10)[// 1. Load the artifact part containing the path/URI](#__codelineno-45-11)[const artifactPart = await toolContext.loadArtifact(artifactName);](#__codelineno-45-12)[if (!artifactPart?.text) {](#__codelineno-45-13)[return { error: `Could not load artifact or artifact has no text path: ${artifactName}` };](#__codelineno-45-14)[}](#__codelineno-45-15)[const filePath = artifactPart.text;](#__codelineno-45-17)[console.log(`Loaded document reference: ${filePath}`);](#__codelineno-45-18)[// 2. Read the actual document content (outside ADK context)](#__codelineno-45-20)[let documentContent = '';](#__codelineno-45-21)[if (filePath.startsWith('gs://')) {](#__codelineno-45-22)[// Example: Use GCS client library to download/read](#__codelineno-45-23)[// const storage = new Storage();](#__codelineno-45-24)[// const bucket = storage.bucket('my-bucket');](#__codelineno-45-25)[// const file = bucket.file(filePath.replace('gs://my-bucket/', ''));](#__codelineno-45-26)[// const [contents] = await file.download();](#__codelineno-45-27)[// documentContent = contents.toString();](#__codelineno-45-28)[} else if (filePath.startsWith('/')) {](#__codelineno-45-29)[// Example: Use local file system](#__codelineno-45-30)[// import { readFile } from 'fs/promises';](#__codelineno-45-31)[// documentContent = await readFile(filePath, 'utf8');](#__codelineno-45-32)[} else {](#__codelineno-45-33)[return { error: `Unsupported file path scheme: ${filePath}` };](#__codelineno-45-34)[}](#__codelineno-45-35)[// 3. Summarize the content](#__codelineno-45-37)[if (!documentContent) {](#__codelineno-45-38)[return { error: 'Failed to read document content.' };](#__codelineno-45-39)[}](#__codelineno-45-40)[// const summary = summarizeText(documentContent); // Call your summarization logic](#__codelineno-45-42)[const summary = `Summary of content from ${filePath}`; // Placeholder](#__codelineno-45-43)[return { summary };](#__codelineno-45-45)[} catch (e) {](#__codelineno-45-47)[return { error: `Error processing artifact: ${e}` };](#__codelineno-45-48)[}](#__codelineno-45-49)[}](#__codelineno-45-50)[import "google.golang.org/adk/tool"](#__codelineno-46-1)[// Pseudocode: In the Summarizer tool function](#__codelineno-46-3)[type summarizeDocumentArgs struct{}](#__codelineno-46-4)[type summarizeDocumentResult struct {](#__codelineno-46-6)[Summary string `json:"summary"`](#__codelineno-46-7)[}](#__codelineno-46-8)[func summarizeDocumentTool(tc tool.Context, input summarizeDocumentArgs) (summarizeDocumentResult, error) {](#__codelineno-46-10)[artifactName, err := tc.State().Get("temp:doc_artifact_name")](#__codelineno-46-11)[if err != nil {](#__codelineno-46-12)[return summarizeDocumentResult{}, fmt.Errorf("No document artifact name found in state")](#__codelineno-46-13)[}](#__codelineno-46-14)[// 1. Load the artifact part containing the path/URI](#__codelineno-46-16)[artifactPart, err := tc.Artifacts().Load(tc, artifactName.(string))](#__codelineno-46-17)[if err != nil {](#__codelineno-46-18)[return summarizeDocumentResult{}, err](#__codelineno-46-19)[}](#__codelineno-46-20)[if artifactPart.Part.Text == "" {](#__codelineno-46-22)[return summarizeDocumentResult{}, fmt.Errorf("Could not load artifact or artifact has no text path.")](#__codelineno-46-23)[}](#__codelineno-46-24)[filePath := artifactPart.Part.Text](#__codelineno-46-25)[fmt.Printf("Loaded document reference: %s\n", filePath)](#__codelineno-46-26)[// 2. Read the actual document content (outside ADK context)](#__codelineno-46-28)[// In a real implementation, you would use a GCS client or local file reader.](#__codelineno-46-29)[documentContent := "This is the fake content of the document at " + filePath](#__codelineno-46-30)[_ = documentContent // Avoid unused variable error.](#__codelineno-46-31)[// 3. Summarize the content](#__codelineno-46-33)[summary := "Summary of content from " + filePath // Placeholder](#__codelineno-46-34)[return summarizeDocumentResult{Summary: summary}, nil](#__codelineno-46-36)[}](#__codelineno-46-37)[// Pseudocode: In the Summarizer tool function](#__codelineno-47-1)[import com.google.adk.tools.ToolContext;](#__codelineno-47-2)[import com.google.genai.types.Content;](#__codelineno-47-3)[import com.google.genai.types.Part;](#__codelineno-47-4)[public Map<String, String> summarizeDocumentTool(ToolContext toolContext){](#__codelineno-47-6)[String artifactName = toolContext.state().get("temp:doc_artifact_name");](#__codelineno-47-7)[if(artifactName.isEmpty()){](#__codelineno-47-8)[return Map.of("error", "Document artifact name not found in state.");](#__codelineno-47-9)[}](#__codelineno-47-10)[try{](#__codelineno-47-11)[// 1. Load the artifact part containing the path/URI](#__codelineno-47-12)[Maybe<Part> artifactPart = toolContext.loadArtifact(artifactName);](#__codelineno-47-13)[if((artifactPart == null) || (artifactPart.text().isEmpty())){](#__codelineno-47-14)[return Map.of("error", "Could not load artifact or artifact has no text path: " + artifactName);](#__codelineno-47-15)[}](#__codelineno-47-16)[filePath = artifactPart.text();](#__codelineno-47-17)[System.out.println("Loaded document reference: " + filePath);](#__codelineno-47-18)[// 2. Read the actual document content (outside ADK context)](#__codelineno-47-20)[String documentContent = "";](#__codelineno-47-21)[if(filePath.startsWith("gs://")){](#__codelineno-47-22)[// Example: Use GCS client library to download/read into documentContent](#__codelineno-47-23)[pass; // Replace with actual GCS reading logic](#__codelineno-47-24)[} else if(){](#__codelineno-47-25)[// Example: Use local file system to download/read into documentContent](#__codelineno-47-26)[} else{](#__codelineno-47-27)[return Map.of("error", "Unsupported file path scheme: " + filePath);](#__codelineno-47-28)[}](#__codelineno-47-29)[// 3. Summarize the content](#__codelineno-47-31)[if(documentContent.isEmpty()){](#__codelineno-47-32)[return Map.of("error", "Failed to read document content.");](#__codelineno-47-33)[}](#__codelineno-47-34)[// summary = summarizeText(documentContent) // Call your summarization logic](#__codelineno-47-36)[summary = "Summary of content from " + filePath; // Placeholder](#__codelineno-47-37)[return Map.of("summary", summary);](#__codelineno-47-39)[} catch(IllegalArgumentException e){](#__codelineno-47-40)[return Map.of("error", "Artifact service error " + filePath + e);](#__codelineno-47-41)[} catch(FileNotFoundException e){](#__codelineno-47-42)[return Map.of("error", "Local file not found " + filePath + e);](#__codelineno-47-43)[} catch(Exception e){](#__codelineno-47-44)[return Map.of("error", "Error reading document " + filePath + e);](#__codelineno-47-45)[}](#__codelineno-47-46)[}](#__codelineno-47-47)

-
-
**Listing Artifacts:**Discover what files are available.[# Pseudocode: In a tool function](#__codelineno-48-1)[from google.adk.tools import ToolContext](#__codelineno-48-2)[def check_available_docs(tool_context: ToolContext) -> dict:](#__codelineno-48-4)[try:](#__codelineno-48-5)[artifact_keys = tool_context.list_artifacts()](#__codelineno-48-6)[print(f"Available artifacts: {artifact_keys}")](#__codelineno-48-7)[return {"available_docs": artifact_keys}](#__codelineno-48-8)[except ValueError as e:](#__codelineno-48-9)[return {"error": f"Artifact service error: {e}"}](#__codelineno-48-10)[// Pseudocode: In a tool function](#__codelineno-49-1)[import { ToolContext } from '@google/adk';](#__codelineno-49-2)[async function checkAvailableDocs(toolContext: ToolContext): Promise<Record<string, string[] | string>> {](#__codelineno-49-4)[try {](#__codelineno-49-5)[const artifactKeys = await toolContext.listArtifacts();](#__codelineno-49-6)[console.log(`Available artifacts: ${artifactKeys}`);](#__codelineno-49-7)[return { available_docs: artifactKeys };](#__codelineno-49-8)[} catch (e) {](#__codelineno-49-9)[return { error: `Artifact service error: ${e}` };](#__codelineno-49-10)[}](#__codelineno-49-11)[}](#__codelineno-49-12)[import "google.golang.org/adk/tool"](#__codelineno-50-1)[// Pseudocode: In a tool function](#__codelineno-50-3)[type checkAvailableDocsArgs struct{}](#__codelineno-50-4)[type checkAvailableDocsResult struct {](#__codelineno-50-6)[AvailableDocs []string `json:"available_docs"`](#__codelineno-50-7)[}](#__codelineno-50-8)[func checkAvailableDocs(tc tool.Context, args checkAvailableDocsArgs) (checkAvailableDocsResult, error) {](#__codelineno-50-10)[artifactKeys, err := tc.Artifacts().List(tc)](#__codelineno-50-11)[if err != nil {](#__codelineno-50-12)[return checkAvailableDocsResult{}, err](#__codelineno-50-13)[}](#__codelineno-50-14)[fmt.Printf("Available artifacts: %v\n", artifactKeys)](#__codelineno-50-15)[return checkAvailableDocsResult{AvailableDocs: artifactKeys.FileNames}, nil](#__codelineno-50-16)[}](#__codelineno-50-17)[// Pseudocode: In a tool function](#__codelineno-51-1)[import com.google.adk.tools.ToolContext;](#__codelineno-51-2)[public Map<String, String> checkAvailableDocs(ToolContext toolContext){](#__codelineno-51-4)[try{](#__codelineno-51-5)[Single<List<String>> artifactKeys = toolContext.listArtifacts();](#__codelineno-51-6)[System.out.println("Available artifacts" + artifactKeys.tostring());](#__codelineno-51-7)[return Map.of("availableDocs", "artifactKeys");](#__codelineno-51-8)[} catch(IllegalArgumentException e){](#__codelineno-51-9)[return Map.of("error", "Artifact service error: " + e);](#__codelineno-51-10)[}](#__codelineno-51-11)[}](#__codelineno-51-12)

### Handling Tool Authentication[¶](#handling-tool-authentication)

Securely manage API keys or other credentials needed by tools.

# Pseudocode: Tool requiring auth
from google.adk.tools import ToolContext
from google.adk.auth import AuthConfig # Assume appropriate AuthConfig is defined
# Define your required auth configuration (e.g., OAuth, API Key)
MY_API_AUTH_CONFIG = AuthConfig(...)
AUTH_STATE_KEY = "user:my_api_credential" # Key to store retrieved credential
def call_secure_api(tool_context: ToolContext, request_data: str) -> dict:
# 1. Check if credential already exists in state
credential = tool_context.state.get(AUTH_STATE_KEY)
if not credential:
# 2. If not, request it
print("Credential not found, requesting...")
try:
tool_context.request_credential(MY_API_AUTH_CONFIG)
# The framework handles yielding the event. The tool execution stops here for this turn.
return {"status": "Authentication required. Please provide credentials."}
except ValueError as e:
return {"error": f"Auth error: {e}"} # e.g., function_call_id missing
except Exception as e:
return {"error": f"Failed to request credential: {e}"}
# 3. If credential exists (might be from a previous turn after request)
# or if this is a subsequent call after auth flow completed externally
try:
# Optionally, re-validate/retrieve if needed, or use directly
# This might retrieve the credential if the external flow just completed
auth_credential_obj = tool_context.get_auth_response(MY_API_AUTH_CONFIG)
api_key = auth_credential_obj.api_key # Or access_token, etc.
# Store it back in state for future calls within the session
tool_context.state[AUTH_STATE_KEY] = auth_credential_obj.model_dump() # Persist retrieved credential
print(f"Using retrieved credential to call API with data: {request_data}")
# ... Make the actual API call using api_key ...
api_result = f"API result for {request_data}"
return {"result": api_result}
except Exception as e:
# Handle errors retrieving/using the credential
print(f"Error using credential: {e}")
# Maybe clear the state key if credential is invalid?
# tool_context.state[AUTH_STATE_KEY] = None
return {"error": "Failed to use credential"}


// Pseudocode: Tool requiring auth
import { ToolContext } from '@google/adk'; // AuthConfig from ADK or custom
// Define a local AuthConfig interface as it's not publicly exported by ADK
interface AuthConfig {
credentialKey: string;
authScheme: { type: string }; // Minimal representation for the example
// Add other properties if they become relevant for the example
}
// Define your required auth configuration (e.g., OAuth, API Key)
const MY_API_AUTH_CONFIG: AuthConfig = {
credentialKey: 'my-api-key', // Example key
authScheme: { type: 'api-key' }, // Example scheme type
};
const AUTH_STATE_KEY = 'user:my_api_credential'; // Key to store retrieved credential
async function callSecureApi(toolContext: ToolContext, requestData: string): Promise<Record<string, string>> {
// 1. Check if credential already exists in state
const credential = toolContext.state.get(AUTH_STATE_KEY);
if (!credential) {
// 2. If not, request it
console.log('Credential not found, requesting...');
try {
toolContext.requestCredential(MY_API_AUTH_CONFIG);
// The framework handles yielding the event. The tool execution stops here for this turn.
return { status: 'Authentication required. Please provide credentials.' };
} catch (e) {
return { error: `Auth or credential request error: ${e}` };
}
}
// 3. If credential exists (might be from a previous turn after request)
// or if this is a subsequent call after auth flow completed externally
try {
// Optionally, re-validate/retrieve if needed, or use directly
// This might retrieve the credential if the external flow just completed
const authCredentialObj = toolContext.getAuthResponse(MY_API_AUTH_CONFIG);
const apiKey = authCredentialObj?.apiKey; // Or accessToken, etc.
// Store it back in state for future calls within the session
// Note: In strict TS, might need to cast or serialize authCredentialObj
toolContext.state.set(AUTH_STATE_KEY, JSON.stringify(authCredentialObj));
console.log(`Using retrieved credential to call API with data: ${requestData}`);
// ... Make the actual API call using apiKey ...
const apiResult = `API result for ${requestData}`;
return { result: apiResult };
} catch (e) {
// Handle errors retrieving/using the credential
console.error(`Error using credential: ${e}`);
// Maybe clear the state key if credential is invalid?
// toolContext.state.set(AUTH_STATE_KEY, null);
return { error: 'Failed to use credential' };
}
}


*Remember: request_credential pauses the tool and signals the need for authentication. The user/system provides credentials, and on a subsequent call, get_auth_response (or checking state again) allows the tool to proceed.* The


`tool_context.function_call_id`

is used implicitly by the framework to link the request and response.### Leveraging Memory[¶](#leveraging-memory)

Access relevant information from the past or external sources.

# Pseudocode: Tool using memory search
from google.adk.tools import ToolContext
def find_related_info(tool_context: ToolContext, topic: str) -> dict:
try:
search_results = tool_context.search_memory(f"Information about {topic}")
if search_results.results:
print(f"Found {len(search_results.results)} memory results for '{topic}'")
# Process search_results.results (which are SearchMemoryResponseEntry)
top_result_text = search_results.results[0].text
return {"memory_snippet": top_result_text}
else:
return {"message": "No relevant memories found."}
except ValueError as e:
return {"error": f"Memory service error: {e}"} # e.g., Service not configured
except Exception as e:
return {"error": f"Unexpected error searching memory: {e}"}


// Pseudocode: Tool using memory search
import { ToolContext } from '@google/adk';
async function findRelatedInfo(toolContext: ToolContext, topic: string): Promise<Record<string, string>> {
try {
const searchResults = await toolContext.searchMemory(`Information about ${topic}`);
if (searchResults.results?.length) {
console.log(`Found ${searchResults.results.length} memory results for '${topic}'`);
// Process searchResults.results
const topResultText = searchResults.results[0].text;
return { memory_snippet: topResultText };
} else {
return { message: 'No relevant memories found.' };
}
} catch (e) {
return { error: `Memory service error: ${e}` }; // e.g., Service not configured
}
}


### Advanced: Direct `InvocationContext`

Usage[¶](#advanced-direct-invocationcontext-usage)

While most interactions happen via `CallbackContext`

or `ToolContext`

, sometimes the agent's core logic (`_run_async_impl`

/`_run_live_impl`

) needs direct access.

# Pseudocode: Inside agent's _run_async_impl
from google.adk.agents import BaseAgent
from google.adk.agents.invocation_context import InvocationContext
from google.adk.events import Event
from typing import AsyncGenerator
class MyControllingAgent(BaseAgent):
async def _run_async_impl(self, ctx: InvocationContext) -> AsyncGenerator[Event, None]:
# Example: Check if a specific service is available
if not ctx.memory_service:
print("Memory service is not available for this invocation.")
# Potentially change agent behavior
# Example: Early termination based on some condition
if ctx.session.state.get("critical_error_flag"):
print("Critical error detected, ending invocation.")
ctx.end_invocation = True # Signal framework to stop processing
yield Event(author=self.name, invocation_id=ctx.invocation_id, content="Stopping due to critical error.")
return # Stop this agent's execution
# ... Normal agent processing ...
yield # ... event ...


// Pseudocode: Inside agent's runAsyncImpl
import { BaseAgent, InvocationContext } from '@google/adk';
import type { Event } from '@google/adk';
class MyControllingAgent extends BaseAgent {
async *runAsyncImpl(ctx: InvocationContext): AsyncGenerator<Event, void, undefined> {
// Example: Check if a specific service is available
if (!ctx.memoryService) {
console.log('Memory service is not available for this invocation.');
// Potentially change agent behavior
}
// Example: Early termination based on some condition
// Direct access to state via ctx.session.state or through ctx.session.state property if wrapped
if ((ctx.session.state as { 'critical_error_flag': boolean })['critical_error_flag']) {
console.log('Critical error detected, ending invocation.');
ctx.endInvocation = true; // Signal framework to stop processing
yield {
author: this.name,
invocationId: ctx.invocationId,
content: { parts: [{ text: 'Stopping due to critical error.' }] }
} as Event;
return; // Stop this agent's execution
}
// ... Normal agent processing ...
yield; // ... event ...
}
}


Setting `ctx.end_invocation = True`

is a way to gracefully stop the entire request-response cycle from within the agent or its callbacks/tools (via their respective context objects which also have access to modify the underlying `InvocationContext`

's flag).

## Key Takeaways & Best Practices[¶](#key-takeaways-best-practices)

**Use the Right Context:**Always use the most specific context object provided (`ToolContext`

in tools/tool-callbacks,`CallbackContext`

in agent/model-callbacks,`ReadonlyContext`

where applicable). Use the full`InvocationContext`

(`ctx`

) directly in`_run_async_impl`

/`_run_live_impl`

only when necessary.**State for Data Flow:**`context.state`

is the primary way to share data, remember preferences, and manage conversational memory*within*an invocation. Use prefixes (`app:`

,`user:`

,`temp:`

) thoughtfully when using persistent storage.**Artifacts for Files:**Use`context.save_artifact`

and`context.load_artifact`

for managing file references (like paths or URIs) or larger data blobs. Store references, load content on demand.**Tracked Changes:**Modifications to state or artifacts made via context methods are automatically linked to the current step's`EventActions`

and handled by the`SessionService`

.**Start Simple:**Focus on`state`

and basic artifact usage first. Explore authentication, memory, and advanced`InvocationContext`

fields (like those for live streaming) as your needs become more complex.

By understanding and effectively using these context objects, you can build more sophisticated, stateful, and capable agents with ADK.
