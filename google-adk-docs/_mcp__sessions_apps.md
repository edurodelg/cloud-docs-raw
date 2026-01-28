---
merged_at: 2026-01-28T07:23:42.228026
merged_files: 2
---


---
<!-- Source: https://google.github.io/adk-docs/mcp/ -->

# Model Context Protocol (MCP)¶

# Model Context Protocol (MCP)[¶](#model-context-protocol-mcp)

The
[Model Context Protocol (MCP)](https://modelcontextprotocol.io/introduction) is
an open standard designed to standardize how Large Language Models (LLMs) like
Gemini and Claude communicate with external applications, data sources, and
tools. Think of it as a universal connection mechanism that simplifies how LLMs
obtain context, execute actions, and interact with various systems.

## How does MCP work?[¶](#how-does-mcp-work)

MCP follows a client-server architecture, defining how data (resources), interactive templates (prompts), and actionable functions (tools) are exposed by an MCP server and consumed by an MCP client (which could be an LLM host application or an AI agent).

## MCP Tools in ADK[¶](#mcp-tools-in-adk)

ADK helps you both use and consume MCP tools in your agents, whether you're trying to build a tool to call an MCP service, or exposing an MCP server for other developers or agents to interact with your tools.

Refer to the [MCP Tools documentation](/adk-docs/tools-custom/mcp-tools/) for code samples
and design patterns that help you use ADK together with MCP servers, including:

**Using Existing MCP Servers within ADK**: An ADK agent can act as an MCP client and use tools provided by external MCP servers.**Exposing ADK Tools via an MCP Server**: How to build an MCP server that wraps ADK tools, making them accessible to any MCP client.

## MCP Toolbox for Databases[¶](#mcp-toolbox-for-databases)

[MCP Toolbox for Databases](https://github.com/googleapis/genai-toolbox) is an
open-source MCP server that securely exposes your backend data sources as a
set of pre-built, production-ready tools for Gen AI agents. It functions as a
universal abstraction layer, allowing your ADK agent to securely query, analyze,
and retrieve information from a wide array of databases with built-in support.

The MCP Toolbox server includes a comprehensive library of connectors, ensuring that agents can safely interact with your complex data estate.

### Supported Data Sources[¶](#supported-data-sources)

MCP Toolbox provides out-of-the-box toolsets for the following databases and data platforms:

#### Google Cloud[¶](#google-cloud)

[BigQuery](https://googleapis.github.io/genai-toolbox/resources/sources/bigquery/)(including tools for SQL execution, schema discovery, and AI-powered time series forecasting)[AlloyDB](https://googleapis.github.io/genai-toolbox/resources/sources/alloydb-pg/)(PostgreSQL-compatible, with tools for both standard queries and natural language queries)[AlloyDB Admin](https://googleapis.github.io/genai-toolbox/resources/sources/alloydb-admin/)[Spanner](https://googleapis.github.io/genai-toolbox/resources/sources/spanner/)(supporting both GoogleSQL and PostgreSQL dialects)- Cloud SQL (with dedicated support for
[Cloud SQL for PostgreSQL](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-sql-pg/),[Cloud SQL for MySQL](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-sql-mysql/), and[Cloud SQL for SQL Server](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-sql-mssql/)) [Cloud SQL Admin](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-sql-admin/)[Firestore](https://googleapis.github.io/genai-toolbox/resources/sources/firestore/)[Bigtable](https://googleapis.github.io/genai-toolbox/resources/sources/bigtable/)[Dataplex](https://googleapis.github.io/genai-toolbox/resources/sources/dataplex/)(for data discovery and metadata search)[Cloud Monitoring](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-monitoring/)

#### Relational & SQL Databases[¶](#relational-sql-databases)

[PostgreSQL](https://googleapis.github.io/genai-toolbox/resources/sources/postgres/)(generic)[MySQL](https://googleapis.github.io/genai-toolbox/resources/sources/mysql/)(generic)[Microsoft SQL Server](https://googleapis.github.io/genai-toolbox/resources/sources/mssql/)(generic)[ClickHouse](https://googleapis.github.io/genai-toolbox/resources/sources/clickhouse/)[TiDB](https://googleapis.github.io/genai-toolbox/resources/sources/tidb/)[OceanBase](https://googleapis.github.io/genai-toolbox/resources/sources/oceanbase/)[Firebird](https://googleapis.github.io/genai-toolbox/resources/sources/firebird/)[SQLite](https://googleapis.github.io/genai-toolbox/resources/sources/sqlite/)[YugabyteDB](https://googleapis.github.io/genai-toolbox/resources/sources/yugabytedb/)

#### NoSQL & Key-Value Stores[¶](#nosql-key-value-stores)

#### Graph Databases[¶](#graph-databases)

#### Data Platforms & Federation[¶](#data-platforms-federation)

[Looker](https://googleapis.github.io/genai-toolbox/resources/sources/looker/)(for running Looks, queries, and building dashboards via the Looker API)[Trino](https://googleapis.github.io/genai-toolbox/resources/sources/trino/)(for running federated queries across multiple sources)

#### Other[¶](#other)

### Documentation[¶](#documentation)

Refer to the
[MCP Toolbox for Databases](/adk-docs/tools/google-cloud/mcp-toolbox-for-databases/)
documentation on how you can use ADK together with the MCP Toolbox for
Databases. For getting started with the MCP Toolbox for Databases, a blog post [Tutorial : MCP Toolbox for Databases - Exposing Big Query Datasets](https://medium.com/google-cloud/tutorial-mcp-toolbox-for-databases-exposing-big-query-datasets-9321f0064f4e) and Codelab [MCP Toolbox for Databases:Making BigQuery datasets available to MCP clients](https://codelabs.developers.google.com/mcp-toolbox-bigquery-dataset?hl=en#0) are also available.

## ADK Agent and FastMCP server[¶](#adk-agent-and-fastmcp-server)

[FastMCP](https://github.com/jlowin/fastmcp) handles all the complex MCP protocol details and server management, so you can focus on building great tools. It's designed to be high-level and Pythonic; in most cases, decorating a function is all you need.

Refer to the [MCP Tools documentation](/adk-docs/tools-custom/mcp-tools/) documentation on
how you can use ADK together with the FastMCP server running on Cloud Run.

## MCP Servers for Google Cloud Genmedia[¶](#mcp-servers-for-google-cloud-genmedia)

[MCP Tools for Genmedia Services](https://github.com/GoogleCloudPlatform/vertex-ai-creative-studio/tree/main/experiments/mcp-genmedia)
is a set of open-source MCP servers that enable you to integrate Google Cloud
generative media services—such as Imagen, Veo, Chirp 3 HD voices, and Lyria—into
your AI applications.

Agent Development Kit (ADK) and [Genkit](https://genkit.dev/) provide built-in
support for these MCP tools, allowing your AI agents to effectively orchestrate
generative media workflows. For implementation guidance, refer to the [ADK
example
agent](https://github.com/GoogleCloudPlatform/vertex-ai-creative-studio/tree/main/experiments/mcp-genmedia/sample-agents/adk)
and the
[Genkit example](https://github.com/GoogleCloudPlatform/vertex-ai-creative-studio/tree/main/experiments/mcp-genmedia/sample-agents/genkit).

---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/sessions/ -->

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

---
<!-- Source: https://google.github.io/adk-docs/apps/ -->

# Apps: workflow management class¶

# Apps: workflow management class[¶](#apps-workflow-management-class)

The ** App** class is a top-level container for an entire Agent Development Kit
(ADK) agent workflow. It is designed to manage the lifecycle, configuration, and
state for a collection of agents grouped by a

**. The**

*root agent***App**class separates the concerns of an agent workflow's overall operational infrastructure from individual agents' task-oriented reasoning.

Defining an ** App** object in your ADK workflow is optional and changes how you
organize your agent code and run your agents. From a practical perspective, you
use the

**class to configure the following features for your agent workflow:**

*App*This guide explains how to use the App class for configuring and managing your ADK agent workflows.

## Purpose of App Class[¶](#purpose-of-app-class)

The ** App** class addresses several architectural issues that arise when
building complex agentic systems:

**Centralized configuration:**Provides a single, centralized location for managing shared resources like API keys and database clients, avoiding the need to pass configuration down through every agent.**Lifecycle management:**Theclass includes*App*and*on startup*hooks, which allow for reliable management of persistent resources such as database connection pools or in-memory caches that need to exist across multiple invocations.*on shutdown***State scope:**It defines an explicit boundary for application-level state with an`app:*`

prefix making the scope and lifetime of this state clear to developers.**Unit of deployment:**Theconcept establishes a formal*App**deployable unit*, simplifying versioning, testing, and serving of agentic applications.

## Define an App object[¶](#define-an-app-object)

The ** App** class is used as the primary container of your agent workflow and
contains the root agent of the project. The

**is the container for the primary controller agent and any additional sub-agents.**

*root agent*### Define app with root agent[¶](#define-app-with-root-agent)

Create a ** root agent** for your workflow by creating a subclass from the

**base class. Then define an**

*Agent***object and configure it with the**

*App***object and optional features, as shown in the following sample code:**

*root agent*from google.adk.agents.llm_agent import Agent
from google.adk.apps import App
root_agent = Agent(
model='gemini-2.5-flash',
name='greeter_agent',
description='An agent that provides a friendly greeting.',
instruction='Reply with Hello, World!',
)
app = App(
name="agents",
root_agent=root_agent,
# Optionally include App-level features:
# plugins, context_cache_config, resumability_config
)


Recommended: Use `app`

variable name

In your agent project code, set your ** App** object to the variable name

`app`

so it is compatible with the ADK command line interface runner tools. ### Run your App agent[¶](#run-your-app-agent)

You can use the ** Runner** class to run your agent workflow using the

`app`

parameter, as shown in the following code sample:import asyncio
from dotenv import load_dotenv
from google.adk.runners import InMemoryRunner
from agent import app # import code from agent.py
load_dotenv() # load API keys and settings
# Set a Runner using the imported application object
runner = InMemoryRunner(app=app)
async def main():
try: # run_debug() requires ADK Python 1.18 or higher:
response = await runner.run_debug("Hello there!")
except Exception as e:
print(f"An error occurred during agent execution: {e}")
if __name__ == "__main__":
asyncio.run(main())


Version requirement for `Runner.run_debug()`


The `Runner.run_debug()`

command requires ADK Python v1.18.0 or higher.
You can also use `Runner.run()`

, which requires more setup code. For
more details, see the

Run your App agent with the `main.py`

code using the following command:

## Next steps[¶](#next-steps)

For a more complete sample code implementation, see the
[Hello World App](https://github.com/google/adk-python/tree/main/contributing/samples/hello_world_app)
code example.
