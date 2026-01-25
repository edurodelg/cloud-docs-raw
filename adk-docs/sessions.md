---
source_url: https://google.github.io/adk-docs/sessions/
fetched_at: 2026-01-25T03:13:24.836157
---

# Introduction to Conversational Context: Session, State, and Memory¶

# Introduction to Conversational Context: Session, State, and Memory[¶](#introduction-to-conversational-context-session-state-and-memory)

Meaningful, multi-turn conversations require agents to understand context. Just
like humans, they need to recall the conversation history: what's been said and
done to maintain continuity and avoid repetition. The Agent Development Kit
(ADK) provides structured ways to manage this context through `Session`

,
`State`

, and `Memory`

.

## Core Concepts[¶](#core-concepts)

Think of different instances of your conversations with the agent as distinct
**conversation threads**, potentially drawing upon **long-term knowledge**.

-
: The Current Conversation Thread`Session`

- Represents a
*single, ongoing interaction*between a user and your agent system. - Contains the chronological sequence of messages and actions taken by the
agent (referred to
`Events`

) during*that specific interaction*. - A
`Session`

can also hold temporary data (`State`

) relevant only*during this conversation*.

- Represents a
-
: Data Within the Current Conversation`State`

(`session.state`

)- Data stored within a specific
`Session`

. - Used to manage information relevant
*only*to the*current, active*conversation thread (e.g., items in a shopping cart*during this chat*, user preferences mentioned*in this session*).

- Data stored within a specific
-
: Searchable, Cross-Session Information`Memory`

- Represents a store of information that might span
*multiple past sessions*or include external data sources. - It acts as a knowledge base the agent can
*search*to recall information or context beyond the immediate conversation.

- Represents a store of information that might span

## Managing Context: Services[¶](#managing-context-services)

ADK provides services to manage these concepts:

-
: Manages the different conversation threads (`SessionService`

`Session`

objects)- Handles the lifecycle: creating, retrieving, updating (appending
`Events`

, modifying`State`

), and deleting individual`Session`

s.

- Handles the lifecycle: creating, retrieving, updating (appending
-
: Manages the Long-Term Knowledge Store (`MemoryService`

`Memory`

)- Handles ingesting information (often from completed
`Session`

s) into the long-term store. - Provides methods to search this stored knowledge based on queries.

- Handles ingesting information (often from completed

**Implementations**: ADK offers different implementations for both
`SessionService`

and `MemoryService`

, allowing you to choose the storage backend
that best fits your application's needs. Notably, **in-memory implementations**
are provided for both services; these are designed specifically for **local
testing and fast development**. It's important to remember that **all data
stored using these in-memory options (sessions, state, or long-term knowledge)
is lost when your application restarts**. For persistence and scalability beyond
local testing, ADK also offers cloud-based and database service options.

**In Summary:**

: Focus on the`Session`

&`State`

**current interaction**– the history and data of the*single, active conversation*. Managed primarily by a`SessionService`

.**Memory**: Focuses on the**past and external information**– a*searchable archive*potentially spanning across conversations. Managed by a`MemoryService`

.

## What's Next?[¶](#whats-next)

In the following sections, we'll dive deeper into each of these components:

: Understanding its structure and`Session`

`Events`

.: How to effectively read, write, and manage session-specific data.`State`

: Choosing the right storage backend for your sessions.`SessionService`

: Exploring options for storing and retrieving broader context.`MemoryService`


Understanding these concepts is fundamental to building agents that can engage in complex, stateful, and context-aware conversations.