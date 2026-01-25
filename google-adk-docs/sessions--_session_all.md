---
merged_at: 2026-01-25T12:06:27.810242
merged_files: 3
---

# Documentos Fusionados

Este archivo contiene 3 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/sessions/session/migrate/ -->

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

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/sessions/session/rewind/ -->

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

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/sessions/session/ -->

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
