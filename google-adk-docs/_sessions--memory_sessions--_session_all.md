---
merged_at: 2026-02-09T09:31:35.620867
merged_files: 2
---


---
<!-- Source: https://google.github.io/adk-docs/sessions/memory/ -->

# Memory: Long-Term Knowledge with MemoryService¶

# Memory: Long-Term Knowledge with `MemoryService`

[¶](#memory-long-term-knowledge-with-memoryservice)

We've seen how `Session`

tracks the history (`events`

) and temporary data (`state`

) for a *single, ongoing conversation*. But what if an agent needs to recall information from *past* conversations? This is where the concept of **Long-Term Knowledge** and the ** MemoryService** come into play.

Think of it this way:

Like your short-term memory during one specific chat.`Session`

/`State`

:**Long-Term Knowledge (**: Like a searchable archive or knowledge library the agent can consult, potentially containing information from many past chats or other sources.`MemoryService`

)

## The `MemoryService`

Role[¶](#the-memoryservice-role)

The `BaseMemoryService`

defines the interface for managing this searchable, long-term knowledge store. Its primary responsibilities are:

**Ingesting Information (**Taking the contents of a (usually completed)`add_session_to_memory`

):`Session`

and adding relevant information to the long-term knowledge store.**Searching Information (**Allowing an agent (typically via a`search_memory`

):`Tool`

) to query the knowledge store and retrieve relevant snippets or context based on a search query.

## Choosing the Right Memory Service[¶](#choosing-the-right-memory-service)

The ADK offers two distinct `MemoryService`

implementations, each tailored to different use cases. Use the table below to decide which is the best fit for your agent.

Feature |
InMemoryMemoryService |
VertexAiMemoryBankService |
|---|---|---|
Persistence |
None (data is lost on restart) | Yes (Managed by Vertex AI) |
Primary Use Case |
Prototyping, local development, and simple testing. | Building meaningful, evolving memories from user conversations. |
Memory Extraction |
Stores full conversation | Extracts
|

**Search Capability****Setup Complexity**[Agent Engine](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/memory-bank/overview)instance in Vertex AI.**Dependencies****When to use it**## In-Memory Memory[¶](#in-memory-memory)

The `InMemoryMemoryService`

stores session information in the application's memory and performs basic keyword matching for searches. It requires no setup and is best for prototyping and simple testing scenarios where persistence isn't required.

**Example: Adding and Searching Memory**

This example demonstrates the basic flow using the `InMemoryMemoryService`

for simplicity.

import asyncio
from google.adk.agents import LlmAgent
from google.adk.sessions import InMemorySessionService, Session
from google.adk.memory import InMemoryMemoryService # Import MemoryService
from google.adk.runners import Runner
from google.adk.tools import load_memory # Tool to query memory
from google.genai.types import Content, Part
# --- Constants ---
APP_NAME = "memory_example_app"
USER_ID = "mem_user"
MODEL = "gemini-2.0-flash" # Use a valid model
# --- Agent Definitions ---
# Agent 1: Simple agent to capture information
info_capture_agent = LlmAgent(
model=MODEL,
name="InfoCaptureAgent",
instruction="Acknowledge the user's statement.",
)
# Agent 2: Agent that can use memory
memory_recall_agent = LlmAgent(
model=MODEL,
name="MemoryRecallAgent",
instruction="Answer the user's question. Use the 'load_memory' tool "
"if the answer might be in past conversations.",
tools=[load_memory] # Give the agent the tool
)
# --- Services ---
# Services must be shared across runners to share state and memory
session_service = InMemorySessionService()
memory_service = InMemoryMemoryService() # Use in-memory for demo
async def run_scenario():
# --- Scenario ---
# Turn 1: Capture some information in a session
print("--- Turn 1: Capturing Information ---")
runner1 = Runner(
# Start with the info capture agent
agent=info_capture_agent,
app_name=APP_NAME,
session_service=session_service,
memory_service=memory_service # Provide the memory service to the Runner
)
session1_id = "session_info"
await runner1.session_service.create_session(app_name=APP_NAME, user_id=USER_ID, session_id=session1_id)
user_input1 = Content(parts=[Part(text="My favorite project is Project Alpha.")], role="user")
# Run the agent
final_response_text = "(No final response)"
async for event in runner1.run_async(user_id=USER_ID, session_id=session1_id, new_message=user_input1):
if event.is_final_response() and event.content and event.content.parts:
final_response_text = event.content.parts[0].text
print(f"Agent 1 Response: {final_response_text}")
# Get the completed session
completed_session1 = await runner1.session_service.get_session(app_name=APP_NAME, user_id=USER_ID, session_id=session1_id)
# Add this session's content to the Memory Service
print("\n--- Adding Session 1 to Memory ---")
await memory_service.add_session_to_memory(completed_session1)
print("Session added to memory.")
# Turn 2: Recall the information in a new session
print("\n--- Turn 2: Recalling Information ---")
runner2 = Runner(
# Use the second agent, which has the memory tool
agent=memory_recall_agent,
app_name=APP_NAME,
session_service=session_service, # Reuse the same service
memory_service=memory_service # Reuse the same service
)
session2_id = "session_recall"
await runner2.session_service.create_session(app_name=APP_NAME, user_id=USER_ID, session_id=session2_id)
user_input2 = Content(parts=[Part(text="What is my favorite project?")], role="user")
# Run the second agent
final_response_text_2 = "(No final response)"
async for event in runner2.run_async(user_id=USER_ID, session_id=session2_id, new_message=user_input2):
if event.is_final_response() and event.content and event.content.parts:
final_response_text_2 = event.content.parts[0].text
print(f"Agent 2 Response: {final_response_text_2}")
# To run this example, you can use the following snippet:
# asyncio.run(run_scenario())
# await run_scenario()


import (
"context"
"fmt"
"log"
"strings"
"google.golang.org/adk/agent"
"google.golang.org/adk/agent/llmagent"
"google.golang.org/adk/memory"
"google.golang.org/adk/model/gemini"
"google.golang.org/adk/runner"
"google.golang.org/adk/session"
"google.golang.org/adk/tool"
"google.golang.org/adk/tool/functiontool"
"google.golang.org/genai"
)
const (
appName = "go_memory_example_app"
userID = "go_mem_user"
modelID = "gemini-2.5-pro"
)
// Args defines the input structure for the memory search tool.
type Args struct {
Query string `json:"query" jsonschema:"The query to search for in the memory."`
}
// Result defines the output structure for the memory search tool.
type Result struct {
Results []string `json:"results"`
}
// memorySearchToolFunc is the implementation of the memory search tool.
// This function demonstrates accessing memory via tool.Context.
func memorySearchToolFunc(tctx tool.Context, args Args) (Result, error) {
fmt.Printf("Tool: Searching memory for query: '%s'\n", args.Query)
// The SearchMemory function is available on the context.
searchResults, err := tctx.SearchMemory(context.Background(), args.Query)
if err != nil {
log.Printf("Error searching memory: %v", err)
return Result{}, fmt.Errorf("failed memory search")
}
var results []string
for _, res := range searchResults.Memories {
if res.Content != nil {
results = append(results, textParts(res.Content)...)
}
}
return Result{Results: results}, nil
}
// Define a tool that can search memory.
var memorySearchTool = must(functiontool.New(
functiontool.Config{
Name: "search_past_conversations",
Description: "Searches past conversations for relevant information.",
},
memorySearchToolFunc,
))
// This example demonstrates how to use the MemoryService in the Go ADK.
// It covers two main scenarios:
// 1. Adding a completed session to memory and recalling it in a new session.
// 2. Searching memory from within a custom tool using the tool.Context.
func main() {
ctx := context.Background()
// --- Services ---
// Services must be shared across runners to share state and memory.
sessionService := session.InMemoryService()
memoryService := memory.InMemoryService() // Use in-memory for this demo.
// --- Scenario 1: Capture information in one session ---
fmt.Println("--- Turn 1: Capturing Information ---")
infoCaptureAgent := must(llmagent.New(llmagent.Config{
Name: "InfoCaptureAgent",
Model: must(gemini.NewModel(ctx, modelID, nil)),
Instruction: "Acknowledge the user's statement.",
}))
runner1 := must(runner.New(runner.Config{
AppName: appName,
Agent: infoCaptureAgent,
SessionService: sessionService,
MemoryService: memoryService, // Provide the memory service to the Runner
}))
session1ID := "session_info"
must(sessionService.Create(ctx, &session.CreateRequest{AppName: appName, UserID: userID, SessionID: session1ID}))
userInput1 := genai.NewContentFromText("My favorite project is Project Alpha.", "user")
var finalResponseText string
for event, err := range runner1.Run(ctx, userID, session1ID, userInput1, agent.RunConfig{}) {
if err != nil {
log.Printf("Agent 1 Error: %v", err)
continue
}
if event.Content != nil && !event.LLMResponse.Partial {
finalResponseText = strings.Join(textParts(event.LLMResponse.Content), "")
}
}
fmt.Printf("Agent 1 Response: %s\n", finalResponseText)
// Add the completed session to the Memory Service
fmt.Println("\n--- Adding Session 1 to Memory ---")
resp, err := sessionService.Get(ctx, &session.GetRequest{AppName: appName, UserID: userID, SessionID: session1ID})
if err != nil {
log.Fatalf("Failed to get completed session: %v", err)
}
if err := memoryService.AddSession(ctx, resp.Session); err != nil {
log.Fatalf("Failed to add session to memory: %v", err)
}
fmt.Println("Session added to memory.")
// --- Scenario 2: Recall the information in a new session using a tool ---
fmt.Println("\n--- Turn 2: Recalling Information ---")
memoryRecallAgent := must(llmagent.New(llmagent.Config{
Name: "MemoryRecallAgent",
Model: must(gemini.NewModel(ctx, modelID, nil)),
Instruction: "Answer the user's question. Use the 'search_past_conversations' tool if the answer might be in past conversations.",
Tools: []tool.Tool{memorySearchTool}, // Give the agent the tool
}))
runner2 := must(runner.New(runner.Config{
Agent: memoryRecallAgent,
AppName: appName,
SessionService: sessionService,
MemoryService: memoryService,
}))
session2ID := "session_recall"
must(sessionService.Create(ctx, &session.CreateRequest{AppName: appName, UserID: userID, SessionID: session2ID}))
userInput2 := genai.NewContentFromText("What is my favorite project?", "user")
var finalResponseText2 string
for event, err := range runner2.Run(ctx, userID, session2ID, userInput2, agent.RunConfig{}) {
if err != nil {
log.Printf("Agent 2 Error: %v", err)
continue
}
if event.Content != nil && !event.LLMResponse.Partial {
finalResponseText2 = strings.Join(textParts(event.LLMResponse.Content), "")
}
}
fmt.Printf("Agent 2 Response: %s\n", finalResponseText2)
}


### Searching Memory Within a Tool[¶](#searching-memory-within-a-tool)

You can also search memory from within a custom tool by using the `tool.Context`

.

// memorySearchToolFunc is the implementation of the memory search tool.
// This function demonstrates accessing memory via tool.Context.
func memorySearchToolFunc(tctx tool.Context, args Args) (Result, error) {
fmt.Printf("Tool: Searching memory for query: '%s'\n", args.Query)
// The SearchMemory function is available on the context.
searchResults, err := tctx.SearchMemory(context.Background(), args.Query)
if err != nil {
log.Printf("Error searching memory: %v", err)
return Result{}, fmt.Errorf("failed memory search")
}
var results []string
for _, res := range searchResults.Memories {
if res.Content != nil {
results = append(results, textParts(res.Content)...)
}
}
return Result{Results: results}, nil
}
// Define a tool that can search memory.
var memorySearchTool = must(functiontool.New(
functiontool.Config{
Name: "search_past_conversations",
Description: "Searches past conversations for relevant information.",
},
memorySearchToolFunc,
))


## Vertex AI Memory Bank[¶](#vertex-ai-memory-bank)

The `VertexAiMemoryBankService`

connects your agent to [Vertex AI Memory Bank](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/memory-bank/overview), a fully managed Google Cloud service that provides sophisticated, persistent memory capabilities for conversational agents.

### How It Works[¶](#how-it-works)

The service handles two key operations:

**Generating Memories:**At the end of a conversation, you can send the session's events to the Memory Bank, which intelligently processes and stores the information as "memories."**Retrieving Memories:**Your agent code can issue a search query against the Memory Bank to retrieve relevant memories from past conversations.

### Prerequisites[¶](#prerequisites)

Before you can use this feature, you must have:

**A Google Cloud Project:**With the Vertex AI API enabled.**An Agent Engine:**You need to create an Agent Engine in Vertex AI. You do not need to deploy your agent to Agent Engine Runtime to use Memory Bank. This will provide you with the**Agent Engine ID**required for configuration.**Authentication:**Ensure your local environment is authenticated to access Google Cloud services. The simplest way is to run:**Environment Variables:**The service requires your Google Cloud Project ID and Location. Set them as environment variables:

### Configuration[¶](#configuration)

To connect your agent to the Memory Bank, you use the `--memory_service_uri`

flag when starting the ADK server (`adk web`

or `adk api_server`

). The URI must be in the format `agentengine://<agent_engine_id>`

.

Or, you can configure your agent to use the Memory Bank by manually instantiating the `VertexAiMemoryBankService`

and passing it to the `Runner`

.

from google.adk.memory import VertexAiMemoryBankService
agent_engine_id = agent_engine.api_resource.name.split("/")[-1]
memory_service = VertexAiMemoryBankService(
project="PROJECT_ID",
location="LOCATION",
agent_engine_id=agent_engine_id
)
runner = adk.Runner(
...
memory_service=memory_service
)


## Using Memory in Your Agent[¶](#using-memory-in-your-agent)

When a memory service is configured, your agent can use a tool or callback to retrieve memories. ADK includes two pre-built tools for retrieving memories:

`PreloadMemory`

: Always retrieve memory at the beginning of each turn (similar to a callback).`LoadMemory`

: Retrieve memory when your agent decides it would be helpful.

**Example:**

from google.adk.agents import Agent
from google.adk.tools.preload_memory_tool import PreloadMemoryTool
agent = Agent(
model=MODEL_ID,
name='weather_sentiment_agent',
instruction="...",
tools=[PreloadMemoryTool()]
)


To extract memories from your session, you need to call `add_session_to_memory`

. For example, you can automate this via a callback:

from google import adk
async def auto_save_session_to_memory_callback(callback_context):
await callback_context._invocation_context.memory_service.add_session_to_memory(
callback_context._invocation_context.session)
agent = Agent(
model=MODEL,
name="Generic_QA_Agent",
instruction="Answer the user's questions",
tools=[adk.tools.preload_memory_tool.PreloadMemoryTool()],
after_agent_callback=auto_save_session_to_memory_callback,
)


## Advanced Concepts[¶](#advanced-concepts)

### How Memory Works in Practice[¶](#how-memory-works-in-practice)

The memory workflow internally involves these steps:

**Session Interaction:**A user interacts with an agent via a`Session`

, managed by a`SessionService`

. Events are added, and state might be updated.**Ingestion into Memory:**At some point (often when a session is considered complete or has yielded significant information), your application calls`memory_service.add_session_to_memory(session)`

. This extracts relevant information from the session's events and adds it to the long-term knowledge store (in-memory dictionary or Agent Engine Memory Bank).**Later Query:**In a*different*(or the same) session, the user might ask a question requiring past context (e.g., "What did we discuss about project X last week?").**Agent Uses Memory Tool:**An agent equipped with a memory-retrieval tool (like the built-in`load_memory`

tool) recognizes the need for past context. It calls the tool, providing a search query (e.g., "discussion project X last week").**Search Execution:**The tool internally calls`memory_service.search_memory(app_name, user_id, query)`

.**Results Returned:**The`MemoryService`

searches its store (using keyword matching or semantic search) and returns relevant snippets as a`SearchMemoryResponse`

containing a list of`MemoryResult`

objects (each potentially holding events from a relevant past session).**Agent Uses Results:**The tool returns these results to the agent, usually as part of the context or function response. The agent can then use this retrieved information to formulate its final answer to the user.

### Can an agent have access to more than one memory service?[¶](#can-an-agent-have-access-to-more-than-one-memory-service)

-
**Through Standard Configuration: No.**The framework (`adk web`

,`adk api_server`

) is designed to be configured with one single memory service at a time via the`--memory_service_uri`

flag. This single service is then provided to the agent and accessed through the built-in`self.search_memory()`

method. From a configuration standpoint, you can only choose one backend (`InMemory`

,`VertexAiMemoryBankService`

) for all agents served by that process. -
**Within Your Agent's Code: Yes, absolutely.**There is nothing preventing you from manually importing and instantiating another memory service directly inside your agent's code. This allows you to access multiple memory sources within a single agent turn.

For example, your agent could use the framework-configured `InMemoryMemoryService`

to recall conversational history, and also manually instantiate a `VertexAiMemoryBankService`

to look up information in a technical manual.

#### Example: Using Two Memory Services[¶](#example-using-two-memory-services)

Here’s how you could implement that in your agent's code:

from google.adk.agents import Agent
from google.adk.memory import InMemoryMemoryService, VertexAiMemoryBankService
from google.genai import types
class MultiMemoryAgent(Agent):
def __init__(self, **kwargs):
super().__init__(**kwargs)
self.memory_service = InMemoryMemoryService()
# Manually instantiate a second memory service for document lookups
self.vertexai_memorybank_service = VertexAiMemoryBankService(
project="PROJECT_ID",
location="LOCATION",
agent_engine_id="AGENT_ENGINE_ID"
)
async def run(self, request: types.Content, **kwargs) -> types.Content:
user_query = request.parts[0].text
# 1. Search conversational history using the framework-provided memory
# (This would be InMemoryMemoryService if configured)
conversation_context = await self.memory_service.search_memory(query=user_query)
# 2. Search the document knowledge base using the manually created service
document_context = await self.vertexai_memorybank_service.search_memory(query=user_query)
# Combine the context from both sources to generate a better response
prompt = "From our past conversations, I remember:\n"
prompt += f"{conversation_context.memories}\n\n"
prompt += "From the technical manuals, I found:\n"
prompt += f"{document_context.memories}\n\n"
prompt += f"Based on all this, here is my answer to '{user_query}':"
return await self.llm.generate_content_async(prompt)

---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/sessions/session/migrate/ -->

# Session database schema migration¶

# Session database schema migration[¶](#session-database-schema-migration)

If you are using `DatabaseSessionService`

and upgrading to ADK Python release
v1.22.0 or higher, you should migrate your database to the new session database
schema. Starting with ADK Python release v1.22.0, the database schema for
`DatabaseSessionService`

has been updated from `v0`

, which is a pickle-based
serialization, to `v1`

, which uses JSON-based serialization. Previous `v0`

session
schema databases will continue to work with ADK Python v1.22.0 and higher versions,
but the `v1`

schema may be required in future releases.

## Migrate session database[¶](#migrate-session-database)

A migration script is provided to facilitate the migration process. The script
reads data from your existing database, converts it to the new format, and
writes it to a new database. You can run the migration using the ADK Command
Line Interface (CLI) `migrate session`

command, as shown in the following examples:

Required: ADK Python v1.22.1 or higher

ADK Python v1.22.1 is required for this procedure because it includes the migration command line interface function and bug fixes to support the session database schema change.

After running the migration, update your `DatabaseSessionService`

configuration
to use the new database URL you specified for `dest_db_url`

.

---
<!-- Source: https://google.github.io/adk-docs/sessions/session/rewind/ -->

# Rewind sessions for agents¶

# Rewind sessions for agents[¶](#rewind-sessions-for-agents)

The ADK session Rewind feature allows you to revert a session to a previous request state, enabling you to undo mistakes, explore alternative paths, or restart a process from a known good point. This document provides an overview of the feature, how to use it, and its limitations.

## Rewind a session[¶](#rewind-a-session)

When you rewind a session, you specify a user request, or ** invocation**, that
you want to undo, and the system undoes that request and the requests after it.
So if you have three requests (A, B, C) and you want to return to the state at
request A, you specify B, which undoes the changes from requests B and C. You
rewind a session by using the rewind method on a

**instance, specifying the user, session, and invocation id, as shown in the following code snippet:**

*Runner*# Create runner
runner = InMemoryRunner(
agent=agent.root_agent,
app_name=APP_NAME,
)
# Create a session
session = await runner.session_service.create_session(
app_name=APP_NAME, user_id=USER_ID
)
# call agent with wrapper function "call_agent_async()"
await call_agent_async(
runner, USER_ID, session.id, "set state color to red"
)
# ... more agent calls ...
events_list = await call_agent_async(
runner, USER_ID, session.id, "update state color to blue"
)
# get invocation id
rewind_invocation_id=events_list[1].invocation_id
# rewind invocations (state color: red)
await runner.rewind_async(
user_id=USER_ID,
session_id=session.id,
rewind_before_invocation_id=rewind_invocation_id,
)


When you call the ** rewind** method, all ADK managed session-level resources
are restored to the state they were in

*before*the request you specified with the

**. However, global resources, such as app-level or user-level state and artifacts, are not restored. For a complete example of an agent session rewind, see the**

*invocation id*[rewind_session](https://github.com/google/adk-python/tree/main/contributing/samples/rewind_session)sample code. For more information on the limitations of the Rewind feature, see

[Limitations](#limitations).

## How it works[¶](#how-it-works)

The Rewind feature creates a special ** rewind** request that restores the
session's state and artifacts to their condition

*before*the rewind point specified by an invocation id. This approach means that all requests, including rewound requests, are preserved in the log for later debugging, analysis, or auditing. After the rewind, the system ignores the rewound requests when it prepares the next requests for the AI model. This behavior means the AI model used by the agent effectively forgets any interactions from the rewind point up to the next request.

## Limitations[¶](#limitations)

The Rewind feature has some limitations that you should be aware of when using it with your agent workflow:

**Global agent resources:**App-level and user-level state and artifacts are*not*restored by the rewind feature. Only session-level state and artifacts are restored.**External dependencies:**The rewind feature does not manage external dependencies. If a tool in your agent interacts with external systems, it is your responsibility to handle the restoration of those systems to their prior state.**Atomicity:**State updates, artifact updates, and event persistence are not performed in a single atomic transaction. Therefore, you should avoid rewinding active sessions or concurrently manipulating session artifacts during a rewind to prevent inconsistencies.

---
<!-- Source: https://google.github.io/adk-docs/sessions/session/ -->

# Session: Tracking Individual Conversations¶

# Session: Tracking Individual Conversations[¶](#session-tracking-individual-conversations)

Following our Introduction, let's dive into the `Session`

. Think back to the
idea of a "conversation thread." Just like you wouldn't start every text message
from scratch, agents need context regarding the ongoing interaction.
** Session** is the ADK object designed specifically to track and manage these
individual conversation threads.

## The `Session`

Object[¶](#the-session-object)

When a user starts interacting with your agent, the `SessionService`

creates a
`Session`

object (`google.adk.sessions.Session`

). This object acts as the
container holding everything related to that *one specific chat thread*. Here
are its key properties:

**Identification (**Unique labels for the conversation.`id`

,`appName`

,`userId`

):`id`

: A unique identifier for*this specific*conversation thread, essential for retrieving it later. A SessionService object can handle multiple`Session`

(s). This field identifies which particular session object are we referring to. For example, "test_id_modification".`app_name`

: Identifies which agent application this conversation belongs to. For example, "id_modifier_workflow".`userId`

: Links the conversation to a particular user.

**History (**A chronological sequence of all interactions (`events`

):`Event`

objects – user messages, agent responses, tool actions) that have occurred within this specific thread.**Session State (**A place to store temporary data relevant`state`

):*only*to this specific, ongoing conversation. This acts as a scratchpad for the agent during the interaction. We will cover how to use and manage`state`

in detail in the next section.**Activity Tracking (**A timestamp indicating the last time an event occurred in this conversation thread.`lastUpdateTime`

):

### Example: Examining Session Properties[¶](#example-examining-session-properties)

from google.adk.sessions import InMemorySessionService, Session
# Create a simple session to examine its properties
temp_service = InMemorySessionService()
example_session = await temp_service.create_session(
app_name="my_app",
user_id="example_user",
state={"initial_key": "initial_value"} # State can be initialized
)
print(f"--- Examining Session Properties ---")
print(f"ID (`id`): {example_session.id}")
print(f"Application Name (`app_name`): {example_session.app_name}")
print(f"User ID (`user_id`): {example_session.user_id}")
print(f"State (`state`): {example_session.state}") # Note: Only shows initial state here
print(f"Events (`events`): {example_session.events}") # Initially empty
print(f"Last Update (`last_update_time`): {example_session.last_update_time:.2f}")
print(f"---------------------------------")
# Clean up (optional for this example)
temp_service = await temp_service.delete_session(app_name=example_session.app_name,
user_id=example_session.user_id, session_id=example_session.id)
print("The final status of temp_service - ", temp_service)


import { InMemorySessionService } from "@google/adk";
// Create a simple session to examine its properties
const tempService = new InMemorySessionService();
const exampleSession = await tempService.createSession({
appName: "my_app",
userId: "example_user",
state: {"initial_key": "initial_value"} // State can be initialized
});
console.log("--- Examining Session Properties ---");
console.log(`ID ('id'): ${exampleSession.id}`);
console.log(`Application Name ('appName'): ${exampleSession.appName}`);
console.log(`User ID ('userId'): ${exampleSession.userId}`);
console.log(`State ('state'): ${JSON.stringify(exampleSession.state)}`); // Note: Only shows initial state here
console.log(`Events ('events'): ${JSON.stringify(exampleSession.events)}`); // Initially empty
console.log(`Last Update ('lastUpdateTime'): ${exampleSession.lastUpdateTime}`);
console.log("---------------------------------");
// Clean up (optional for this example)
const finalStatus = await tempService.deleteSession({
appName: exampleSession.appName,
userId: exampleSession.userId,
sessionId: exampleSession.id
});
console.log("The final status of temp_service - ", finalStatus);


appName := "my_go_app"
userID := "example_go_user"
initialState := map[string]any{"initial_key": "initial_value"}
// Create a session to examine its properties.
createResp, err := inMemoryService.Create(ctx, &session.CreateRequest{
AppName: appName,
UserID: userID,
State: initialState,
})
if err != nil {
log.Fatalf("Failed to create session: %v", err)
}
exampleSession := createResp.Session
fmt.Println("\n--- Examining Session Properties ---")
fmt.Printf("ID (`ID()`): %s\n", exampleSession.ID())
fmt.Printf("Application Name (`AppName()`): %s\n", exampleSession.AppName())
// To access state, you call Get().
val, _ := exampleSession.State().Get("initial_key")
fmt.Printf("State (`State().Get()`): initial_key = %v\n", val)
// Events are initially empty.
fmt.Printf("Events (`Events().Len()`): %d\n", exampleSession.Events().Len())
fmt.Printf("Last Update (`LastUpdateTime()`): %s\n", exampleSession.LastUpdateTime().Format("2006-01-02 15:04:05"))
fmt.Println("---------------------------------")
// Clean up the session.
err = inMemoryService.Delete(ctx, &session.DeleteRequest{
AppName: exampleSession.AppName(),
UserID: exampleSession.UserID(),
SessionID: exampleSession.ID(),
})
if err != nil {
log.Fatalf("Failed to delete session: %v", err)
}
fmt.Println("Session deleted successfully.")


import com.google.adk.sessions.InMemorySessionService;
import com.google.adk.sessions.Session;
import java.util.concurrent.ConcurrentMap;
import java.util.concurrent.ConcurrentHashMap;
String sessionId = "123";
String appName = "example-app"; // Example app name
String userId = "example-user"; // Example user id
ConcurrentMap<String, Object> initialState = new ConcurrentHashMap<>(Map.of("newKey", "newValue"));
InMemorySessionService exampleSessionService = new InMemorySessionService();
// Create Session
Session exampleSession = exampleSessionService.createSession(
appName, userId, initialState, Optional.of(sessionId)).blockingGet();
System.out.println("Session created successfully.");
System.out.println("--- Examining Session Properties ---");
System.out.printf("ID (`id`): %s%n", exampleSession.id());
System.out.printf("Application Name (`appName`): %s%n", exampleSession.appName());
System.out.printf("User ID (`userId`): %s%n", exampleSession.userId());
System.out.printf("State (`state`): %s%n", exampleSession.state());
System.out.println("------------------------------------");
// Clean up (optional for this example)
var unused = exampleSessionService.deleteSession(appName, userId, sessionId);


*(**Note:** The state shown above is only the initial state. State updates
happen via events, as discussed in the State section.)*

## Managing Sessions with a `SessionService`

[¶](#managing-sessions-with-a-sessionservice)

As seen above, you don't typically create or manage `Session`

objects directly.
Instead, you use a ** SessionService**. This service acts as the central
manager responsible for the entire lifecycle of your conversation sessions.

Its core responsibilities include:

**Starting New Conversations:**Creating fresh`Session`

objects when a user begins an interaction.**Resuming Existing Conversations:**Retrieving a specific`Session`

(using its ID) so the agent can continue where it left off.**Saving Progress:**Appending new interactions (`Event`

objects) to a session's history. This is also the mechanism through which session`state`

gets updated (more in the`State`

section).**Listing Conversations:**Finding the active session threads for a particular user and application.**Cleaning Up:**Deleting`Session`

objects and their associated data when conversations are finished or no longer needed.

`SessionService`

implementations[¶](#sessionservice-implementations)

ADK provides different `SessionService`

implementations, allowing you to choose
the storage backend that best suits your needs:

`InMemorySessionService`

[¶](#inmemorysessionservice)

**How it works:**Stores all session data directly in the application's memory.**Persistence:**None.**All conversation data is lost if the application restarts.****Requires:**Nothing extra.**Best for:**Quick development, local testing, examples, and scenarios where long-term persistence isn't required.

`VertexAiSessionService`

[¶](#vertexaisessionservice)

**How it works:**Uses Google Cloud Vertex AI infrastructure via API calls for session management.**Persistence:**Yes. Data is managed reliably and scalably via[Vertex AI Agent Engine](https://google.github.io/adk-docs/deploy/agent-engine/).**Requires:**- A Google Cloud project (
`pip install vertexai`

) - A Google Cloud storage bucket that can be configured by this
[step](https://cloud.google.com/vertex-ai/docs/pipelines/configure-project#storage). - A Reasoning Engine resource name/ID that can setup following this
[tutorial](https://google.github.io/adk-docs/deploy/agent-engine/). - If you do not have a Google Cloud project and you want to try the VertexAiSessionService, see
[Vertex AI Express Mode](/adk-docs/tools/google-cloud/express-mode/).

- A Google Cloud project (
**Best for:**Scalable production applications deployed on Google Cloud, especially when integrating with other Vertex AI features.

# Requires: pip install google-adk[vertexai]
# Plus GCP setup and authentication
from google.adk.sessions import VertexAiSessionService
PROJECT_ID = "your-gcp-project-id"
LOCATION = "us-central1"
# The app_name used with this service should be the Reasoning Engine ID or name
REASONING_ENGINE_APP_NAME = "projects/your-gcp-project-id/locations/us-central1/reasoningEngines/your-engine-id"
session_service = VertexAiSessionService(project=PROJECT_ID, location=LOCATION)
# Use REASONING_ENGINE_APP_NAME when calling service methods, e.g.:
# session_service = await session_service.create_session(app_name=REASONING_ENGINE_APP_NAME, ...)


import "google.golang.org/adk/session"
// 2. VertexAIService
// Before running, ensure your environment is authenticated:
// gcloud auth application-default login
// export GOOGLE_CLOUD_PROJECT="your-gcp-project-id"
// export GOOGLE_CLOUD_LOCATION="your-gcp-location"
modelName := "gemini-flash-latest" // Replace with your desired model
vertexService, err := session.VertexAIService(ctx, modelName)
if err != nil {
log.Printf("Could not initialize VertexAIService (this is expected if the gcloud project is not set): %v", err)
} else {
fmt.Println("Successfully initialized VertexAIService.")
}


// Please look at the set of requirements above, consequently export the following in your bashrc file:
// export GOOGLE_CLOUD_PROJECT=my_gcp_project
// export GOOGLE_CLOUD_LOCATION=us-central1
// export GOOGLE_API_KEY=my_api_key
import com.google.adk.sessions.VertexAiSessionService;
import java.util.UUID;
String sessionId = UUID.randomUUID().toString();
String reasoningEngineAppName = "123456789";
String userId = "u_123"; // Example user id
ConcurrentMap<String, Object> initialState = new
ConcurrentHashMap<>(); // No initial state needed for this example
VertexAiSessionService sessionService = new VertexAiSessionService();
Session mySession =
sessionService
.createSession(reasoningEngineAppName, userId, initialState, Optional.of(sessionId))
.blockingGet();


`DatabaseSessionService`

[¶](#databasesessionservice)

**How it works:**Connects to a relational database (e.g., PostgreSQL, MySQL, SQLite) to store session data persistently in tables.**Persistence:**Yes. Data survives application restarts.**Requires:**A configured database.**Best for:**Applications needing reliable, persistent storage that you manage yourself.

from google.adk.sessions import DatabaseSessionService
# Example using a local SQLite file:
# Note: The implementation requires an async database driver.
# For SQLite, use 'sqlite+aiosqlite' instead of 'sqlite' to ensure async compatibility.
db_url = "sqlite+aiosqlite:///./my_agent_data.db"
session_service = DatabaseSessionService(db_url=db_url)


Async Driver Requirement

`DatabaseSessionService`

requires an async database driver. When using SQLite,
you must use `sqlite+aiosqlite`

instead of `sqlite`

in your connection string.
For other databases (PostgreSQL, MySQL), ensure you're using an async-compatible
driver, such as `asyncpg`

for PostgreSQL, `aiomysql`

for MySQL.

Session database schema change in ADK Python v1.22.0

The schema for the session database changed in ADK Python v1.22.0, which
requires migration of the Session Database. For more information, see
[Session database schema migration](/adk-docs/sessions/session/migrate/).

## The Session Lifecycle[¶](#the-session-lifecycle)

Here’s a simplified flow of how `Session`

and `SessionService`

work together
during a conversation turn:

**Start or Resume:**Your application needs to use the`SessionService`

to either`create_session`

(for a new chat) or use an existing session id.**Context Provided:**The`Runner`

gets the appropriate`Session`

object from the appropriate service method, providing the agent with access to the corresponding Session's`state`

and`events`

.**Agent Processing:**The user prompts the agent with a query. The agent analyzes the query and potentially the session`state`

and`events`

history to determine the response.**Response & State Update:**The agent generates a response (and potentially flags data to be updated in the`state`

). The`Runner`

packages this as an`Event`

.**Save Interaction:**The`Runner`

calls`sessionService.append_event(session, event)`

with the`session`

and the new`event`

as the arguments. The service adds the`Event`

to the history and updates the session's`state`

in storage based on information within the event. The session's`last_update_time`

also get updated.**Ready for Next:**The agent's response goes to the user. The updated`Session`

is now stored by the`SessionService`

, ready for the next turn (which restarts the cycle at step 1, usually with the continuation of the conversation in the current session).**End Conversation:**When the conversation is over, your application calls`sessionService.delete_session(...)`

to clean up the stored session data if it is no longer required.

This cycle highlights how the `SessionService`

ensures conversational continuity
by managing the history and state associated with each `Session`

object.
