---
merged_at: 2026-01-29T15:32:00.693565
merged_files: 2
---


---
<!-- Source: https://google.github.io/adk-docs/grounding/vertex_ai_search_grounding/ -->

# Understanding Vertex AI Search Grounding¶

# Understanding Vertex AI Search Grounding[¶](#understanding-vertex-ai-search-grounding)

[Vertex AI Search](/adk-docs/tools/google-cloud/vertex-ai-search/) is a powerful tool for the Agent Development Kit (ADK) that enables AI agents to access information from your private enterprise documents and data repositories. By connecting your agents to indexed enterprise content, you can provide users with answers grounded in your organization's knowledge base.

This feature is particularly valuable for enterprise-specific queries requiring information from internal documentation, policies, research papers, or any proprietary content that has been indexed in your [Vertex AI Search](https://cloud.google.com/enterprise-search) datastore. When your agent determines that information from your knowledge base is needed, it automatically searches your indexed documents and incorporates the results into its response with proper attribution.

## What You'll Learn[¶](#what-youll-learn)

In this guide, you'll discover:

**Quick Setup**: How to create and run a Vertex AI Search-enabled agent from scratch**Grounding Architecture**: The data flow and technical process behind enterprise document grounding**Response Structure**: How to interpret grounded responses and their metadata**Best Practices**: Guidelines for displaying citations and document references to users

## Vertex AI Search Grounding Quickstart[¶](#vertex-ai-search-grounding-quickstart)

This quickstart guides you through creating an ADK agent with Vertex AI Search grounding feature. This quickstart assumes a local IDE (VS Code or PyCharm, etc.) with Python 3.10+ and terminal access.

### 1. Prepare Vertex AI Search[¶](#prepare-vertex-ai-search)

If you already have a Vertex AI Search Data Store and its Data Store ID, you can skip this section. If not, follow the instruction in the [Get started with custom search](https://cloud.google.com/generative-ai-app-builder/docs/try-enterprise-search#unstructured-data) until the end of [Create a data store](https://cloud.google.com/generative-ai-app-builder/docs/try-enterprise-search#create_a_data_store), with selecting the `Unstructured data`

tab. With this instruction, you will build a sample Data Store with earning report PDFs from the [Alphabet investor site](https://abc.xyz/).

After finishing the Create a data store section, open the [Data Stores](https://console.cloud.google.com/gen-app-builder/data-stores/) and select the data store you created, and find the `Data store ID`

:

Note this `Data store ID`

as we will use this later.

### 2. Set up Environment & Install ADK[¶](#set-up-environment-install-adk)

Below are the steps for setting up your environment and installing the ADK for both Python and TypeScript projects.

### 3. Create Agent Project[¶](#create-agent-project)

Under a project directory, run the following commands:

# Step 1: Create a new directory for your agent
mkdir vertex_search_agent
# Step 2: Create __init__.py for the agent
echo "from . import agent" > vertex_search_agent/__init__.py
# Step 3: Create an agent.py (the agent definition) and .env (authentication config)
touch vertex_search_agent/agent.py .env


# Step 1: Create a new directory for your agent
mkdir vertex_search_agent
# Step 2: Create __init__.py for the agent
echo "from . import agent" > vertex_search_agent/__init__.py
# Step 3: Create an agent.py (the agent definition) and .env (authentication config)
type nul > vertex_search_agent\agent.py
type nul > google_search_agent\.env


#### Edit `agent.py`

[¶](#edit-agentpy)

Copy and paste the following code into `agent.py`

, and replace `YOUR_PROJECT_ID`

and `YOUR_DATASTORE_ID`

at the `Configuration`

part with your project ID and Data Store ID accordingly:

from google.adk.agents import Agent
from google.adk.tools import VertexAiSearchTool
# Configuration
DATASTORE_ID = "projects/YOUR_PROJECT_ID/locations/global/collections/default_collection/dataStores/YOUR_DATASTORE_ID"
root_agent = Agent(
name="vertex_search_agent",
model="gemini-2.5-flash",
instruction="Answer questions using Vertex AI Search to find information from internal documents. Always cite sources when available.",
description="Enterprise document search assistant with Vertex AI Search capabilities",
tools=[VertexAiSearchTool(data_store_id=DATASTORE_ID)]
)


Now you would have the following directory structure:

### 4. Authentication Setup[¶](#authentication-setup)

**Note: Vertex AI Search requires Google Cloud Platform (Vertex AI) authentication. Google AI Studio is not supported for this tool.**

- Set up the
[gcloud CLI](https://cloud.google.com/vertex-ai/generative-ai/docs/start/quickstarts/quickstart-multimodal#setup-local) - Authenticate to Google Cloud, from the terminal by running
`gcloud auth login`

. -
Open the

file and copy-paste the following code and update the project ID and location.`.env`


### 5. Run Your Agent[¶](#run-your-agent)

There are multiple ways to interact with your agent:

Run the following command to launch the **dev UI**.

Note for Windows users

When hitting the `_make_subprocess_transport NotImplementedError`

, consider using `adk web --no-reload`

instead.

**Step 1:** Open the URL provided (usually `http://localhost:8000`

or
`http://127.0.0.1:8000`

) directly in your browser.

**Step 2.** In the top-left corner of the UI, you can select your agent in
the dropdown. Select "vertex_search_agent".

Troubleshooting

If you do not see "vertex_search_agent" in the dropdown menu, make sure you
are running `adk web`

in the **parent folder** of your agent folder
(i.e. the parent folder of vertex_search_agent).

**Step 3.** Now you can chat with your agent using the textbox.

### Example prompts to try[¶](#example-prompts-to-try)

With those questions, you can confirm that the agent is actually calling Vertex AI Search to get information from the Alphabet reports:

- What is the revenue of Google Cloud in 2022 Q1?
- What about YouTube?

You've successfully created and interacted with your Vertex AI Search agent using ADK!

## How grounding with Vertex AI Search works[¶](#how-grounding-with-vertex-ai-search-works)

Grounding with Vertex AI Search is the process that connects your agent to your organization's indexed documents and data, allowing it to generate accurate responses based on private enterprise content. When a user's prompt requires information from your internal knowledge base, the agent's underlying LLM intelligently decides to invoke the `VertexAiSearchTool`

to find relevant facts from your indexed documents.

**Data Flow Diagram**[¶](#data-flow-diagram)

This diagram illustrates the step-by-step process of how a user query results in a grounded response.

**Detailed Description**[¶](#detailed-description)

The grounding agent uses the data flow described in the diagram to retrieve, process, and incorporate enterprise information into the final answer presented to the user.

-
**User Query**: An end-user interacts with your agent by asking a question about internal documents or enterprise data. -
**ADK Orchestration**: The Agent Development Kit orchestrates the agent's behavior and passes the user's message to the core of your agent. -
**LLM Analysis and Tool-Calling**: The agent's LLM (e.g., a Gemini model) analyzes the prompt. If it determines that information from your indexed documents is required, it triggers the grounding mechanism by calling the VertexAiSearchTool. This is ideal for answering queries about company policies, technical documentation, or proprietary research. -
**Vertex AI Search Service Interaction**: The VertexAiSearchTool interacts with your configured Vertex AI Search datastore, which contains your indexed enterprise documents. The service formulates and executes search queries against your private content. -
**Document Retrieval & Ranking**: Vertex AI Search retrieves and ranks the most relevant document chunks from your datastore based on semantic similarity and relevance scoring. -
**Context Injection**: The search service integrates the retrieved document snippets into the model's context before the final response is generated. This crucial step allows the model to "reason" over your organization's factual data. -
**Grounded Response Generation**: The LLM, now informed by relevant enterprise content, generates a response that incorporates the retrieved information from your documents. -
**Response Presentation with Sources**: The ADK receives the final grounded response, which includes the necessary source document references and groundingMetadata, and presents it to the user with attribution. This allows end-users to verify the information against your enterprise sources.

## Understanding grounding with Vertex AI Search response[¶](#understanding-grounding-with-vertex-ai-search-response)

When the agent uses Vertex AI Search to ground a response, it returns detailed information that includes the final text answer and metadata about the documents used to generate that answer. This metadata is crucial for verifying the response and providing attribution to your enterprise sources.

### Example of a Grounded Response[¶](#example-of-a-grounded-response)

The following is an example of the content object returned by the model after a grounded query against enterprise documents.

**Final Answer Text:**

"Developing models for a medical scribe presents several significant challenges, primarily due to the complex nature of medical documentation, the sensitive data involved, and the demanding requirements of clinical workflows. Key challenges include: **Accuracy and Reliability:** Medical documentation requires extremely high levels of accuracy, as errors can lead to misdiagnoses, incorrect treatments, and legal repercussions. Ensuring that AI models can reliably capture nuanced medical language, distinguish between subjective and objective information, and accurately transcribe physician-patient interactions is a major hurdle. **Natural Language Understanding (NLU) and Speech Recognition:** Medical conversations are often rapid, involve highly specialized jargon, acronyms, and abbreviations, and can be spoken by individuals with diverse accents or speech patterns... [response continues with detailed analysis of privacy, integration, and technical challenges]"


**Grounding Metadata Snippet:**

This is the grounding metadata you will receive. On `adk web`

, you can find this on the `Response`

tab:

{
"groundingMetadata": {
"groundingChunks": [
{
"document": {
"title": "AI in Medical Scribing: Technical Challenges",
"uri": "projects/your-project/locations/global/dataStores/your-datastore-id/documents/doc-medical-scribe-ai-tech-challenges",
"id": "doc-medical-scribe-ai-tech-challenges"
}
},
{
"document": {
"title": "Regulatory and Ethical Hurdles for AI in Healthcare",
"uri": "projects/your-project/locations/global/dataStores/your-datastore-id/documents/doc-ai-healthcare-ethics",
"id": "doc-ai-healthcare-ethics"
}
}
// ... additional documents
],
"groundingSupports": [
{
"groundingChunkIndices": [0, 1],
"segment": {
"endIndex": 637,
"startIndex": 433,
"text": "Ensuring that AI models can reliably capture nuanced medical language..."
}
}
// ... additional supports linking text segments to source documents
],
"retrievalQueries": [
"challenges in natural language processing medical domain",
"AI medical scribe challenges",
"difficulties in developing AI for medical scribes"
// ... additional search queries executed
]
}
}


### How to Interpret the Response[¶](#how-to-interpret-the-response)

The metadata provides a link between the text generated by the model and the enterprise documents that support it. Here is a step-by-step breakdown:

-
**groundingChunks**: This is a list of the enterprise documents the model consulted. Each chunk contains the document title, uri (document path), and id. -
**groundingSupports**: This list connects specific sentences in the final answer back to the`groundingChunks`

. -
**segment**: This object identifies a specific portion of the final text answer, defined by its`startIndex`

,`endIndex`

, and the`text`

itself. -
**groundingChunkIndices**: This array contains the index numbers that correspond to the sources listed in the`groundingChunks`

. For example, the text about "HIPAA compliance" is supported by information from`groundingChunks`

at index 1 (the "Regulatory and Ethical Hurdles" document). -
**retrievalQueries**: This array shows the specific search queries that were executed against your datastore to find relevant information.

## How to display grounding responses with Vertex AI Search[¶](#how-to-display-grounding-responses-with-vertex-ai-search)

Unlike Google Search grounding, Vertex AI Search grounding does not require specific display components. However, displaying citations and document references builds trust and allows users to verify information against your organization's authoritative sources.

### Optional Citation Display[¶](#optional-citation-display)

Since grounding metadata is provided, you can choose to implement citation displays based on your application needs:

**Simple Text Display (Minimal Implementation):**

for event in events:
if event.is_final_response():
print(event.content.parts[0].text)
# Optional: Show source count
if event.grounding_metadata:
print(f"\nBased on {len(event.grounding_metadata.grounding_chunks)} documents")


**Enhanced Citation Display (Optional):** You can implement interactive citations that show which documents support each statement. The grounding metadata provides all necessary information to map text segments to source documents.

### Implementation Considerations[¶](#implementation-considerations)

When implementing Vertex AI Search grounding displays:

**Document Access**: Verify user permissions for referenced documents**Simple Integration**: Basic text output requires no additional display logic**Optional Enhancements**: Add citations only if your use case benefits from source attribution**Document Links**: Convert document URIs to accessible internal links when needed**Search Queries**: The retrievalQueries array shows what searches were performed against your datastore

## Summary[¶](#summary)

Vertex AI Search Grounding transforms AI agents from general-purpose assistants into enterprise-specific knowledge systems capable of providing accurate, source-attributed information from your organization's private documents. By integrating this feature into your ADK agents, you enable them to:

- Access proprietary information from your indexed document repositories
- Provide source attribution for transparency and trust
- Deliver comprehensive answers with verifiable enterprise facts
- Maintain data privacy within your Google Cloud environment

The grounding process seamlessly connects user queries to your organization's knowledge base, enriching responses with relevant context from your private documents while maintaining the conversational flow. With proper implementation, your agents become powerful tools for enterprise information discovery and decision-making.

---
<!-- Source: N/A -->

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
