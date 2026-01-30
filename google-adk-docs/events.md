---
source_url: https://google.github.io/adk-docs/events/
fetched_at: 2026-01-30T23:34:45.176124
---

# Events¶

# Events[¶](#events)

Events are the fundamental units of information flow within the Agent Development Kit (ADK). They represent every significant occurrence during an agent's interaction lifecycle, from initial user input to the final response and all the steps in between. Understanding events is crucial because they are the primary way components communicate, state is managed, and control flow is directed.

## What Events Are and Why They Matter[¶](#what-events-are-and-why-they-matter)

An `Event`

in ADK is an immutable record representing a specific point in the agent's execution. It captures user messages, agent replies, requests to use tools (function calls), tool results, state changes, control signals, and errors.

Technically, it's an instance of the `google.adk.events.Event`

class, which builds upon the basic `LlmResponse`

structure by adding essential ADK-specific metadata and an `actions`

payload.

# Conceptual Structure of an Event (Python)
# from google.adk.events import Event, EventActions
# from google.genai import types
# class Event(LlmResponse): # Simplified view
# # --- LlmResponse fields ---
# content: Optional[types.Content]
# partial: Optional[bool]
# # ... other response fields ...
# # --- ADK specific additions ---
# author: str # 'user' or agent name
# invocation_id: str # ID for the whole interaction run
# id: str # Unique ID for this specific event
# timestamp: float # Creation time
# actions: EventActions # Important for side-effects & control
# branch: Optional[str] # Hierarchy path
# # ...


In Go, this is a struct of type `google.golang.org/adk/session.Event`

.

// Conceptual Structure of an Event (Go - See session/session.go)
// Simplified view based on the session.Event struct
type Event struct {
// --- Fields from embedded model.LLMResponse ---
model.LLMResponse
// --- ADK specific additions ---
Author string // 'user' or agent name
InvocationID string // ID for the whole interaction run
ID string // Unique ID for this specific event
Timestamp time.Time // Creation time
Actions EventActions // Important for side-effects & control
Branch string // Hierarchy path
// ... other fields
}
// model.LLMResponse contains the Content field
type LLMResponse struct {
Content *genai.Content
// ... other fields
}


In Java, this is an instance of the `com.google.adk.events.Event`

class. It also builds upon a basic response structure by adding essential ADK-specific metadata and an `actions`

payload.

// Conceptual Structure of an Event (Java - See com.google.adk.events.Event.java)
// Simplified view based on the provided com.google.adk.events.Event.java
// public class Event extends JsonBaseModel {
// // --- Fields analogous to LlmResponse ---
// private Optional<Content> content;
// private Optional<Boolean> partial;
// // ... other response fields like errorCode, errorMessage ...
// // --- ADK specific additions ---
// private String author; // 'user' or agent name
// private String invocationId; // ID for the whole interaction run
// private String id; // Unique ID for this specific event
// private long timestamp; // Creation time (epoch milliseconds)
// private EventActions actions; // Important for side-effects & control
// private Optional<String> branch; // Hierarchy path
// // ... other fields like turnComplete, longRunningToolIds etc.
// }


Events are central to ADK's operation for several key reasons:

-
**Communication:**They serve as the standard message format between the user interface, the`Runner`

, agents, the LLM, and tools. Everything flows as an`Event`

. -
**Signaling State & Artifact Changes:**Events carry instructions for state modifications and track artifact updates. The`SessionService`

uses these signals to ensure persistence. In Python changes are signaled via`event.actions.state_delta`

and`event.actions.artifact_delta`

. -
**Control Flow:**Specific fields like`event.actions.transfer_to_agent`

or`event.actions.escalate`

act as signals that direct the framework, determining which agent runs next or if a loop should terminate. -
**History & Observability:**The sequence of events recorded in`session.events`

provides a complete, chronological history of an interaction, invaluable for debugging, auditing, and understanding agent behavior step-by-step.

In essence, the entire process, from a user's query to the agent's final answer, is orchestrated through the generation, interpretation, and processing of `Event`

objects.

## Understanding and Using Events[¶](#understanding-and-using-events)

As a developer, you'll primarily interact with the stream of events yielded by the `Runner`

. Here's how to understand and extract information from them:

Note

The specific parameters or method names for the primitives may vary slightly by SDK language (e.g., `event.content()`

in Python, `event.content().get().parts()`

in Java). Refer to the language-specific API documentation for details.

### Identifying Event Origin and Type[¶](#identifying-event-origin-and-type)

Quickly determine what an event represents by checking:

**Who sent it? (**`event.author`

)`'user'`

: Indicates input directly from the end-user.`'AgentName'`

: Indicates output or action from a specific agent (e.g.,`'WeatherAgent'`

,`'SummarizerAgent'`

).

-
**What's the main payload? (**`event.content`

and`event.content.parts`

)**Text:**Indicates a conversational message. For Python, check if`event.content.parts[0].text`

exists. For Java, check if`event.content()`

is present, its`parts()`

are present and not empty, and the first part's`text()`

is present.**Tool Call Request:**Check`event.get_function_calls()`

. If not empty, the LLM is asking to execute one or more tools. Each item in the list has`.name`

and`.args`

.**Tool Result:**Check`event.get_function_responses()`

. If not empty, this event carries the result(s) from tool execution(s). Each item has`.name`

and`.response`

(the dictionary returned by the tool).*Note:*For history structuring, the`role`

inside the`content`

is often`'user'`

, but the event`author`

is typically the agent that requested the tool call.

-
**Is it streaming output? (**Indicates whether this is an incomplete chunk of text from the LLM.`event.partial`

)`True`

: More text will follow.`False`

or`None`

/`Optional.empty()`

: This part of the content is complete (though the overall turn might not be finished if`turn_complete`

is also false).


# Pseudocode: Basic event identification (Python)
# async for event in runner.run_async(...):
# print(f"Event from: {event.author}")
#
# if event.content and event.content.parts:
# if event.get_function_calls():
# print(" Type: Tool Call Request")
# elif event.get_function_responses():
# print(" Type: Tool Result")
# elif event.content.parts[0].text:
# if event.partial:
# print(" Type: Streaming Text Chunk")
# else:
# print(" Type: Complete Text Message")
# else:
# print(" Type: Other Content (e.g., code result)")
# elif event.actions and (event.actions.state_delta or event.actions.artifact_delta):
# print(" Type: State/Artifact Update")
# else:
# print(" Type: Control Signal or Other")


// Pseudocode: Basic event identification (Go)
import (
"fmt"
"google.golang.org/adk/session"
"google.golang.org/genai"
)
func hasFunctionCalls(content *genai.Content) bool {
if content == nil {
return false
}
for _, part := range content.Parts {
if part.FunctionCall != nil {
return true
}
}
return false
}
func hasFunctionResponses(content *genai.Content) bool {
if content == nil {
return false
}
for _, part := range content.Parts {
if part.FunctionResponse != nil {
return true
}
}
return false
}
func processEvents(events <-chan *session.Event) {
for event := range events {
fmt.Printf("Event from: %s\n", event.Author)
if event.LLMResponse != nil && event.LLMResponse.Content != nil {
if hasFunctionCalls(event.LLMResponse.Content) {
fmt.Println(" Type: Tool Call Request")
} else if hasFunctionResponses(event.LLMResponse.Content) {
fmt.Println(" Type: Tool Result")
} else if len(event.LLMResponse.Content.Parts) > 0 {
if event.LLMResponse.Content.Parts[0].Text != "" {
if event.LLMResponse.Partial {
fmt.Println(" Type: Streaming Text Chunk")
} else {
fmt.Println(" Type: Complete Text Message")
}
} else {
fmt.Println(" Type: Other Content (e.g., code result)")
}
}
} else if len(event.Actions.StateDelta) > 0 {
fmt.Println(" Type: State Update")
} else {
fmt.Println(" Type: Control Signal or Other")
}
}
}


// Pseudocode: Basic event identification (Java)
// import com.google.genai.types.Content;
// import com.google.adk.events.Event;
// import com.google.adk.events.EventActions;
// runner.runAsync(...).forEach(event -> { // Assuming a synchronous stream or reactive stream
// System.out.println("Event from: " + event.author());
//
// if (event.content().isPresent()) {
// Content content = event.content().get();
// if (!event.functionCalls().isEmpty()) {
// System.out.println(" Type: Tool Call Request");
// } else if (!event.functionResponses().isEmpty()) {
// System.out.println(" Type: Tool Result");
// } else if (content.parts().isPresent() && !content.parts().get().isEmpty() &&
// content.parts().get().get(0).text().isPresent()) {
// if (event.partial().orElse(false)) {
// System.out.println(" Type: Streaming Text Chunk");
// } else {
// System.out.println(" Type: Complete Text Message");
// }
// } else {
// System.out.println(" Type: Other Content (e.g., code result)");
// }
// } else if (event.actions() != null &&
// ((event.actions().stateDelta() != null && !event.actions().stateDelta().isEmpty()) ||
// (event.actions().artifactDelta() != null && !event.actions().artifactDelta().isEmpty()))) {
// System.out.println(" Type: State/Artifact Update");
// } else {
// System.out.println(" Type: Control Signal or Other");
// }
// });


### Extracting Key Information[¶](#extracting-key-information)

Once you know the event type, access the relevant data:

-
**Text Content:**Always check for the presence of content and parts before accessing text. In Python its`text = event.content.parts[0].text`

. -
**Function Call Details:**[import (](#__codelineno-7-1)["fmt"](#__codelineno-7-2)["google.golang.org/adk/session"](#__codelineno-7-3)["google.golang.org/genai"](#__codelineno-7-4)[)](#__codelineno-7-5)[func handleFunctionCalls(event *session.Event) {](#__codelineno-7-7)[if event.LLMResponse == nil || event.LLMResponse.Content == nil {](#__codelineno-7-8)[return](#__codelineno-7-9)[}](#__codelineno-7-10)[calls := event.Content.FunctionCalls()](#__codelineno-7-11)[if len(calls) > 0 {](#__codelineno-7-12)[for _, call := range calls {](#__codelineno-7-13)[toolName := call.Name](#__codelineno-7-14)[arguments := call.Args](#__codelineno-7-15)[fmt.Printf(" Tool: %s, Args: %v\n", toolName, arguments)](#__codelineno-7-16)[// Application might dispatch execution based on this](#__codelineno-7-17)[}](#__codelineno-7-18)[}](#__codelineno-7-19)[}](#__codelineno-7-20)[import com.google.genai.types.FunctionCall;](#__codelineno-8-1)[import com.google.common.collect.ImmutableList;](#__codelineno-8-2)[import java.util.Map;](#__codelineno-8-3)[ImmutableList<FunctionCall> calls = event.functionCalls(); // from Event.java](#__codelineno-8-5)[if (!calls.isEmpty()) {](#__codelineno-8-6)[for (FunctionCall call : calls) {](#__codelineno-8-7)[String toolName = call.name().get();](#__codelineno-8-8)[// args is Optional<Map<String, Object>>](#__codelineno-8-9)[Map<String, Object> arguments = call.args().get();](#__codelineno-8-10)[System.out.println(" Tool: " + toolName + ", Args: " + arguments);](#__codelineno-8-11)[// Application might dispatch execution based on this](#__codelineno-8-12)[}](#__codelineno-8-13)[}](#__codelineno-8-14) -
**Function Response Details:**[import (](#__codelineno-10-1)["fmt"](#__codelineno-10-2)["google.golang.org/adk/session"](#__codelineno-10-3)["google.golang.org/genai"](#__codelineno-10-4)[)](#__codelineno-10-5)[func handleFunctionResponses(event *session.Event) {](#__codelineno-10-7)[if event.LLMResponse == nil || event.LLMResponse.Content == nil {](#__codelineno-10-8)[return](#__codelineno-10-9)[}](#__codelineno-10-10)[responses := event.Content.FunctionResponses()](#__codelineno-10-11)[if len(responses) > 0 {](#__codelineno-10-12)[for _, response := range responses {](#__codelineno-10-13)[toolName := response.Name](#__codelineno-10-14)[result := response.Response](#__codelineno-10-15)[fmt.Printf(" Tool Result: %s -> %v\n", toolName, result)](#__codelineno-10-16)[}](#__codelineno-10-17)[}](#__codelineno-10-18)[}](#__codelineno-10-19)[import com.google.genai.types.FunctionResponse;](#__codelineno-11-1)[import com.google.common.collect.ImmutableList;](#__codelineno-11-2)[import java.util.Map;](#__codelineno-11-3)[ImmutableList<FunctionResponse> responses = event.functionResponses(); // from Event.java](#__codelineno-11-5)[if (!responses.isEmpty()) {](#__codelineno-11-6)[for (FunctionResponse response : responses) {](#__codelineno-11-7)[String toolName = response.name().get();](#__codelineno-11-8)[Map<String, String> result= response.response().get(); // Check before getting the response](#__codelineno-11-9)[System.out.println(" Tool Result: " + toolName + " -> " + result);](#__codelineno-11-10)[}](#__codelineno-11-11)[}](#__codelineno-11-12) -
**Identifiers:**`event.id`

: Unique ID for this specific event instance.`event.invocation_id`

: ID for the entire user-request-to-final-response cycle this event belongs to. Useful for logging and tracing.


### Detecting Actions and Side Effects[¶](#detecting-actions-and-side-effects)

The `event.actions`

object signals changes that occurred or should occur. Always check if `event.actions`

and it's fields/ methods exists before accessing them.

-
**State Changes:**Gives you a collection of key-value pairs that were modified in the session state during the step that produced this event.`delta = event.actions.state_delta`

(a dictionary of`{key: value}`

pairs).`delta := event.Actions.StateDelta`

(a`map[string]any`

)`ConcurrentMap<String, Object> delta = event.actions().stateDelta();`

[import java.util.concurrent.ConcurrentMap;](#__codelineno-14-1)[import com.google.adk.events.EventActions;](#__codelineno-14-2)[EventActions actions = event.actions(); // Assuming event.actions() is not null](#__codelineno-14-4)[if (actions != null && actions.stateDelta() != null && !actions.stateDelta().isEmpty()) {](#__codelineno-14-5)[ConcurrentMap<String, Object> stateChanges = actions.stateDelta();](#__codelineno-14-6)[System.out.println(" State changes: " + stateChanges);](#__codelineno-14-7)[// Update local UI or application state if necessary](#__codelineno-14-8)[}](#__codelineno-14-9) -
**Artifact Saves:**Gives you a collection indicating which artifacts were saved and their new version number (or relevant`Part`

information).`artifact_changes = event.actions.artifact_delta`

(a dictionary of`{filename: version}`

).`artifactChanges := event.Actions.ArtifactDelta`

(a`map[string]artifact.Artifact`

)[import (](#__codelineno-16-1)["fmt"](#__codelineno-16-2)["google.golang.org/adk/artifact"](#__codelineno-16-3)["google.golang.org/adk/session"](#__codelineno-16-4)[)](#__codelineno-16-5)[func handleArtifactChanges(event *session.Event) {](#__codelineno-16-7)[if len(event.Actions.ArtifactDelta) > 0 {](#__codelineno-16-8)[fmt.Printf(" Artifacts saved: %v\n", event.Actions.ArtifactDelta)](#__codelineno-16-9)[// UI might refresh an artifact list](#__codelineno-16-10)[// Iterate through event.Actions.ArtifactDelta to get filename and artifact.Artifact details](#__codelineno-16-11)[for filename, art := range event.Actions.ArtifactDelta {](#__codelineno-16-12)[fmt.Printf(" Filename: %s, Version: %d, MIMEType: %s\n", filename, art.Version, art.MIMEType)](#__codelineno-16-13)[}](#__codelineno-16-14)[}](#__codelineno-16-15)[}](#__codelineno-16-16)`ConcurrentMap<String, Part> artifactChanges = event.actions().artifactDelta();`

[import java.util.concurrent.ConcurrentMap;](#__codelineno-17-1)[import com.google.genai.types.Part;](#__codelineno-17-2)[import com.google.adk.events.EventActions;](#__codelineno-17-3)[EventActions actions = event.actions(); // Assuming event.actions() is not null](#__codelineno-17-5)[if (actions != null && actions.artifactDelta() != null && !actions.artifactDelta().isEmpty()) {](#__codelineno-17-6)[ConcurrentMap<String, Part> artifactChanges = actions.artifactDelta();](#__codelineno-17-7)[System.out.println(" Artifacts saved: " + artifactChanges);](#__codelineno-17-8)[// UI might refresh an artifact list](#__codelineno-17-9)[// Iterate through artifactChanges.entrySet() to get filename and Part details](#__codelineno-17-10)[}](#__codelineno-17-11) -
**Control Flow Signals:**Check boolean flags or string values:`event.actions.transfer_to_agent`

(string): Control should pass to the named agent.`event.actions.escalate`

(bool): A loop should terminate.`event.actions.skip_summarization`

(bool): A tool result should not be summarized by the LLM.

`event.Actions.TransferToAgent`

(string): Control should pass to the named agent.`event.Actions.Escalate`

(bool): A loop should terminate.`event.Actions.SkipSummarization`

(bool): A tool result should not be summarized by the LLM.[import (](#__codelineno-19-1)["fmt"](#__codelineno-19-2)["google.golang.org/adk/session"](#__codelineno-19-3)[)](#__codelineno-19-4)[func handleControlFlow(event *session.Event) {](#__codelineno-19-6)[if event.Actions.TransferToAgent != "" {](#__codelineno-19-7)[fmt.Printf(" Signal: Transfer to %s\n", event.Actions.TransferToAgent)](#__codelineno-19-8)[}](#__codelineno-19-9)[if event.Actions.Escalate {](#__codelineno-19-10)[fmt.Println(" Signal: Escalate (terminate loop)")](#__codelineno-19-11)[}](#__codelineno-19-12)[if event.Actions.SkipSummarization {](#__codelineno-19-13)[fmt.Println(" Signal: Skip summarization for tool result")](#__codelineno-19-14)[}](#__codelineno-19-15)[}](#__codelineno-19-16)

`event.actions().transferToAgent()`

(returns`Optional<String>`

): Control should pass to the named agent.`event.actions().escalate()`

(returns`Optional<Boolean>`

): A loop should terminate.`event.actions().skipSummarization()`

(returns`Optional<Boolean>`

): A tool result should not be summarized by the LLM.

[import com.google.adk.events.EventActions;](#__codelineno-20-1)[import java.util.Optional;](#__codelineno-20-2)[EventActions actions = event.actions(); // Assuming event.actions() is not null](#__codelineno-20-4)[if (actions != null) {](#__codelineno-20-5)[Optional<String> transferAgent = actions.transferToAgent();](#__codelineno-20-6)[if (transferAgent.isPresent()) {](#__codelineno-20-7)[System.out.println(" Signal: Transfer to " + transferAgent.get());](#__codelineno-20-8)[}](#__codelineno-20-9)[Optional<Boolean> escalate = actions.escalate();](#__codelineno-20-11)[if (escalate.orElse(false)) { // or escalate.isPresent() && escalate.get()](#__codelineno-20-12)[System.out.println(" Signal: Escalate (terminate loop)");](#__codelineno-20-13)[}](#__codelineno-20-14)[Optional<Boolean> skipSummarization = actions.skipSummarization();](#__codelineno-20-16)[if (skipSummarization.orElse(false)) { // or skipSummarization.isPresent() && skipSummarization.get()](#__codelineno-20-17)[System.out.println(" Signal: Skip summarization for tool result");](#__codelineno-20-18)[}](#__codelineno-20-19)[}](#__codelineno-20-20)

### Determining if an Event is a "Final" Response[¶](#determining-if-an-event-is-a-final-response)

Use the built-in helper method `event.is_final_response()`

to identify events suitable for display as the agent's complete output for a turn.

**Purpose:**Filters out intermediate steps (like tool calls, partial streaming text, internal state updates) from the final user-facing message(s).**When**`True`

?- The event contains a tool result (
`function_response`

) and`skip_summarization`

is`True`

. - The event contains a tool call (
`function_call`

) for a tool marked as`is_long_running=True`

. In Java, check if the`longRunningToolIds`

list is empty:`event.longRunningToolIds().isPresent() && !event.longRunningToolIds().get().isEmpty()`

is`true`

.

- OR,
**all**of the following are met:- No function calls (
`get_function_calls()`

is empty). - No function responses (
`get_function_responses()`

is empty). - Not a partial stream chunk (
`partial`

is not`True`

). - Doesn't end with a code execution result that might need further processing/display.

- No function calls (

- The event contains a tool result (
-
**Usage:**Filter the event stream in your application logic.[# Pseudocode: Handling final responses in application (Python)](#__codelineno-21-1)[# full_response_text = ""](#__codelineno-21-2)[# async for event in runner.run_async(...):](#__codelineno-21-3)[# # Accumulate streaming text if needed...](#__codelineno-21-4)[# if event.partial and event.content and event.content.parts and event.content.parts[0].text:](#__codelineno-21-5)[# full_response_text += event.content.parts[0].text](#__codelineno-21-6)[#](#__codelineno-21-7)[# # Check if it's a final, displayable event](#__codelineno-21-8)[# if event.is_final_response():](#__codelineno-21-9)[# print("\n--- Final Output Detected ---")](#__codelineno-21-10)[# if event.content and event.content.parts and event.content.parts[0].text:](#__codelineno-21-11)[# # If it's the final part of a stream, use accumulated text](#__codelineno-21-12)[# final_text = full_response_text + (event.content.parts[0].text if not event.partial else "")](#__codelineno-21-13)[# print(f"Display to user: {final_text.strip()}")](#__codelineno-21-14)[# full_response_text = "" # Reset accumulator](#__codelineno-21-15)[# elif event.actions and event.actions.skip_summarization and event.get_function_responses():](#__codelineno-21-16)[# # Handle displaying the raw tool result if needed](#__codelineno-21-17)[# response_data = event.get_function_responses()[0].response](#__codelineno-21-18)[# print(f"Display raw tool result: {response_data}")](#__codelineno-21-19)[# elif hasattr(event, 'long_running_tool_ids') and event.long_running_tool_ids:](#__codelineno-21-20)[# print("Display message: Tool is running in background...")](#__codelineno-21-21)[# else:](#__codelineno-21-22)[# # Handle other types of final responses if applicable](#__codelineno-21-23)[# print("Display: Final non-textual response or signal.")](#__codelineno-21-24)[// Pseudocode: Handling final responses in application (Go)](#__codelineno-22-1)[import (](#__codelineno-22-2)["fmt"](#__codelineno-22-3)["strings"](#__codelineno-22-4)["google.golang.org/adk/session"](#__codelineno-22-5)["google.golang.org/genai"](#__codelineno-22-6)[)](#__codelineno-22-7)[// isFinalResponse checks if an event is a final response suitable for display.](#__codelineno-22-9)[func isFinalResponse(event *session.Event) bool {](#__codelineno-22-10)[if event.LLMResponse != nil {](#__codelineno-22-11)[// Condition 1: Tool result with skip summarization.](#__codelineno-22-12)[if event.LLMResponse.Content != nil && len(event.LLMResponse.Content.FunctionResponses()) > 0 && event.Actions.SkipSummarization {](#__codelineno-22-13)[return true](#__codelineno-22-14)[}](#__codelineno-22-15)[// Condition 2: Long-running tool call.](#__codelineno-22-16)[if len(event.LongRunningToolIDs) > 0 {](#__codelineno-22-17)[return true](#__codelineno-22-18)[}](#__codelineno-22-19)[// Condition 3: A complete message without tool calls or responses.](#__codelineno-22-20)[if (event.LLMResponse.Content == nil ||](#__codelineno-22-21)[(len(event.LLMResponse.Content.FunctionCalls()) == 0 && len(event.LLMResponse.Content.FunctionResponses()) == 0)) &&](#__codelineno-22-22)[!event.LLMResponse.Partial {](#__codelineno-22-23)[return true](#__codelineno-22-24)[}](#__codelineno-22-25)[}](#__codelineno-22-26)[return false](#__codelineno-22-27)[}](#__codelineno-22-28)[func handleFinalResponses() {](#__codelineno-22-30)[var fullResponseText strings.Builder](#__codelineno-22-31)[// for event := range runner.Run(...) { // Example loop](#__codelineno-22-32)[// // Accumulate streaming text if needed...](#__codelineno-22-33)[// if event.LLMResponse != nil && event.LLMResponse.Partial && event.LLMResponse.Content != nil {](#__codelineno-22-34)[// if len(event.LLMResponse.Content.Parts) > 0 && event.LLMResponse.Content.Parts[0].Text != "" {](#__codelineno-22-35)[// fullResponseText.WriteString(event.LLMResponse.Content.Parts[0].Text)](#__codelineno-22-36)[// }](#__codelineno-22-37)[// }](#__codelineno-22-38)[//](#__codelineno-22-39)[// // Check if it's a final, displayable event](#__codelineno-22-40)[// if isFinalResponse(event) {](#__codelineno-22-41)[// fmt.Println("\n--- Final Output Detected ---")](#__codelineno-22-42)[// if event.LLMResponse != nil && event.LLMResponse.Content != nil {](#__codelineno-22-43)[// if len(event.LLMResponse.Content.Parts) > 0 && event.LLMResponse.Content.Parts[0].Text != "" {](#__codelineno-22-44)[// // If it's the final part of a stream, use accumulated text](#__codelineno-22-45)[// finalText := fullResponseText.String()](#__codelineno-22-46)[// if !event.LLMResponse.Partial {](#__codelineno-22-47)[// finalText += event.LLMResponse.Content.Parts[0].Text](#__codelineno-22-48)[// }](#__codelineno-22-49)[// fmt.Printf("Display to user: %s\n", strings.TrimSpace(finalText))](#__codelineno-22-50)[// fullResponseText.Reset() // Reset accumulator](#__codelineno-22-51)[// }](#__codelineno-22-52)[// } else if event.Actions.SkipSummarization && event.LLMResponse.Content != nil && len(event.LLMResponse.Content.FunctionResponses()) > 0 {](#__codelineno-22-53)[// // Handle displaying the raw tool result if needed](#__codelineno-22-54)[// responseData := event.LLMResponse.Content.FunctionResponses()[0].Response](#__codelineno-22-55)[// fmt.Printf("Display raw tool result: %v\n", responseData)](#__codelineno-22-56)[// } else if len(event.LongRunningToolIDs) > 0 {](#__codelineno-22-57)[// fmt.Println("Display message: Tool is running in background...")](#__codelineno-22-58)[// } else {](#__codelineno-22-59)[// // Handle other types of final responses if applicable](#__codelineno-22-60)[// fmt.Println("Display: Final non-textual response or signal.")](#__codelineno-22-61)[// }](#__codelineno-22-62)[// }](#__codelineno-22-63)[// }](#__codelineno-22-64)[}](#__codelineno-22-65)[// Pseudocode: Handling final responses in application (Java)](#__codelineno-23-1)[import com.google.adk.events.Event;](#__codelineno-23-2)[import com.google.genai.types.Content;](#__codelineno-23-3)[import com.google.genai.types.FunctionResponse;](#__codelineno-23-4)[import java.util.Map;](#__codelineno-23-5)[StringBuilder fullResponseText = new StringBuilder();](#__codelineno-23-7)[runner.run(...).forEach(event -> { // Assuming a stream of events](#__codelineno-23-8)[// Accumulate streaming text if needed...](#__codelineno-23-9)[if (event.partial().orElse(false) && event.content().isPresent()) {](#__codelineno-23-10)[event.content().flatMap(Content::parts).ifPresent(parts -> {](#__codelineno-23-11)[if (!parts.isEmpty() && parts.get(0).text().isPresent()) {](#__codelineno-23-12)[fullResponseText.append(parts.get(0).text().get());](#__codelineno-23-13)[}](#__codelineno-23-14)[});](#__codelineno-23-15)[}](#__codelineno-23-16)[// Check if it's a final, displayable event](#__codelineno-23-18)[if (event.finalResponse()) { // Using the method from Event.java](#__codelineno-23-19)[System.out.println("\n--- Final Output Detected ---");](#__codelineno-23-20)[if (event.content().isPresent() &&](#__codelineno-23-21)[event.content().flatMap(Content::parts).map(parts -> !parts.isEmpty() && parts.get(0).text().isPresent()).orElse(false)) {](#__codelineno-23-22)[// If it's the final part of a stream, use accumulated text](#__codelineno-23-23)[String eventText = event.content().get().parts().get().get(0).text().get();](#__codelineno-23-24)[String finalText = fullResponseText.toString() + (event.partial().orElse(false) ? "" : eventText);](#__codelineno-23-25)[System.out.println("Display to user: " + finalText.trim());](#__codelineno-23-26)[fullResponseText.setLength(0); // Reset accumulator](#__codelineno-23-27)[} else if (event.actions() != null && event.actions().skipSummarization().orElse(false)](#__codelineno-23-28)[&& !event.functionResponses().isEmpty()) {](#__codelineno-23-29)[// Handle displaying the raw tool result if needed,](#__codelineno-23-30)[// especially if finalResponse() was true due to other conditions](#__codelineno-23-31)[// or if you want to display skipped summarization results regardless of finalResponse()](#__codelineno-23-32)[Map<String, Object> responseData = event.functionResponses().get(0).response().get();](#__codelineno-23-33)[System.out.println("Display raw tool result: " + responseData);](#__codelineno-23-34)[} else if (event.longRunningToolIds().isPresent() && !event.longRunningToolIds().get().isEmpty()) {](#__codelineno-23-35)[// This case is covered by event.finalResponse()](#__codelineno-23-36)[System.out.println("Display message: Tool is running in background...");](#__codelineno-23-37)[} else {](#__codelineno-23-38)[// Handle other types of final responses if applicable](#__codelineno-23-39)[System.out.println("Display: Final non-textual response or signal.");](#__codelineno-23-40)[}](#__codelineno-23-41)[}](#__codelineno-23-42)[});](#__codelineno-23-43)

By carefully examining these aspects of an event, you can build robust applications that react appropriately to the rich information flowing through the ADK system.

## How Events Flow: Generation and Processing[¶](#how-events-flow-generation-and-processing)

Events are created at different points and processed systematically by the framework. Understanding this flow helps clarify how actions and history are managed.

-
**Generation Sources:****User Input:**The`Runner`

typically wraps initial user messages or mid-conversation inputs into an`Event`

with`author='user'`

.**Agent Logic:**Agents (`BaseAgent`

,`LlmAgent`

) explicitly`yield Event(...)`

objects (setting`author=self.name`

) to communicate responses or signal actions.**LLM Responses:**The ADK model integration layer translates raw LLM output (text, function calls, errors) into`Event`

objects, authored by the calling agent.**Tool Results:**After a tool executes, the framework generates an`Event`

containing the`function_response`

. The`author`

is typically the agent that requested the tool, while the`role`

inside the`content`

is set to`'user'`

for the LLM history.

-
**Processing Flow:****Yield/Return:**An event is generated and yielded (Python) or returned/emitted (Java) by its source.**Runner Receives:**The main`Runner`

executing the agent receives the event.**SessionService Processing:**The`Runner`

sends the event to the configured`SessionService`

. This is a critical step:**Applies Deltas:**The service merges`event.actions.state_delta`

into`session.state`

and updates internal records based on`event.actions.artifact_delta`

. (Note: The actual artifact*saving*usually happened earlier when`context.save_artifact`

was called).**Finalizes Metadata:**Assigns a unique`event.id`

if not present, may update`event.timestamp`

.**Persists to History:**Appends the processed event to the`session.events`

list.

**External Yield:**The`Runner`

yields (Python) or returns/emits (Java) the processed event outwards to the calling application (e.g., the code that invoked`runner.run_async`

).


This flow ensures that state changes and history are consistently recorded alongside the communication content of each event.

## Common Event Examples (Illustrative Patterns)[¶](#common-event-examples-illustrative-patterns)

Here are concise examples of typical events you might see in the stream:

**User Input:****Agent Final Text Response:**(`is_final_response() == True`

)**Agent Streaming Text Response:**(`is_final_response() == False`

)**Tool Call Request (by LLM):**(`is_final_response() == False`

)**Tool Result Provided (to LLM):**(`is_final_response()`

depends on`skip_summarization`

)[{](#__codelineno-28-1)["author": "TravelAgent", // Author is agent that requested the call](#__codelineno-28-2)["invocation_id": "e-xyz...",](#__codelineno-28-3)["content": {](#__codelineno-28-4)["role": "user", // Role for LLM history](#__codelineno-28-5)["parts": [{"function_response": {"name": "find_airports", "response": {"result": ["LHR", "LGW", "STN"]}}}]](#__codelineno-28-6)[}](#__codelineno-28-7)[// actions might have skip_summarization=True](#__codelineno-28-8)[}](#__codelineno-28-9)**State/Artifact Update Only:**(`is_final_response() == False`

)**Agent Transfer Signal:**(`is_final_response() == False`

)**Loop Escalation Signal:**(`is_final_response() == False`

)

## Additional Context and Event Details[¶](#additional-context-and-event-details)

Beyond the core concepts, here are a few specific details about context and events that are important for certain use cases:

-
`ToolContext.function_call_id`

(Linking Tool Actions):- When an LLM requests a tool (FunctionCall), that request has an ID. The
`ToolContext`

provided to your tool function includes this`function_call_id`

. **Importance:**This ID is crucial for linking actions like authentication back to the specific tool request that initiated them, especially if multiple tools are called in one turn. The framework uses this ID internally.

- When an LLM requests a tool (FunctionCall), that request has an ID. The
-
**How State/Artifact Changes are Recorded:**- When you modify state or save an artifact using
`CallbackContext`

or`ToolContext`

, these changes aren't immediately written to persistent storage. - Instead, they populate the
`state_delta`

and`artifact_delta`

fields within the`EventActions`

object. - This
`EventActions`

object is attached to the*next event*generated after the change (e.g., the agent's response or a tool result event). - The
`SessionService.append_event`

method reads these deltas from the incoming event and applies them to the session's persistent state and artifact records. This ensures changes are tied chronologically to the event stream.

- When you modify state or save an artifact using
-
**State Scope Prefixes (**`app:`

,`user:`

,`temp:`

):- When managing state via
`context.state`

, you can optionally use prefixes:`app:my_setting`

: Suggests state relevant to the entire application (requires a persistent`SessionService`

).`user:user_preference`

: Suggests state relevant to the specific user across sessions (requires a persistent`SessionService`

).`temp:intermediate_result`

or no prefix: Typically session-specific or temporary state for the current invocation.

- The underlying
`SessionService`

determines how these prefixes are handled for persistence.

- When managing state via
-
**Error Events:**- An
`Event`

can represent an error. Check the`event.error_code`

and`event.error_message`

fields (inherited from`LlmResponse`

). - Errors might originate from the LLM (e.g., safety filters, resource limits) or potentially be packaged by the framework if a tool fails critically. Check tool
`FunctionResponse`

content for typical tool-specific errors.

- An

These details provide a more complete picture for advanced use cases involving tool authentication, state persistence scope, and error handling within the event stream.

## Best Practices for Working with Events[¶](#best-practices-for-working-with-events)

To use events effectively in your ADK applications:

-
**Clear Authorship:**When building custom agents, ensure correct attribution for agent actions in the history. The framework generally handles authorship correctly for LLM/tool events.Use

`yield Event(author=self.name, ...)`

in`BaseAgent`

subclasses.In custom agent

`Run`

methods, the framework typically handles authorship. If creating an event manually, set the author:`yield(&session.Event{Author: a.name, ...}, nil)`

When constructing an

`Event`

in your custom agent logic, set the author, for example:`Event.builder().author(this.getAgentName()) // ... .build();`

-
**Semantic Content & Actions:**Use`event.content`

for the core message/data (text, function call/response). Use`event.actions`

specifically for signaling side effects (state/artifact deltas) or control flow (`transfer`

,`escalate`

,`skip_summarization`

). **Idempotency Awareness:**Understand that the`SessionService`

is responsible for applying the state/artifact changes signaled in`event.actions`

. While ADK services aim for consistency, consider potential downstream effects if your application logic re-processes events.**Use**Rely on this helper method in your application/UI layer to identify complete, user-facing text responses. Avoid manually replicating its logic.`is_final_response()`

:**Leverage History:**The session's event list is your primary debugging tool. Examine the sequence of authors, content, and actions to trace execution and diagnose issues.**Use Metadata:**Use`invocation_id`

to correlate all events within a single user interaction. Use`event.id`

to reference specific, unique occurrences.

Treating events as structured messages with clear purposes for their content and actions is key to building, debugging, and managing complex agent behaviors in ADK.