---
source_url: https://google.github.io/adk-docs/tools/
fetched_at: 2026-01-25T02:04:29.309726
---

# Tools for Agents¶

# Tools for Agents[¶](#tools-for-agents)

Check out the following pre-built tools that you can use with ADK agents:

### Gemini tools[¶](#gemini-tools)

[
](/adk-docs/tools/gemini-api/google-search/)

### Google Search

Perform web searches using Google Search with Gemini

[
](/adk-docs/tools/gemini-api/code-execution/)

### Code Execution

Execute code and debug using Gemini models

[
](/adk-docs/tools/gemini-api/computer-use/)

### Computer Use

Operate computer user interfaces using Gemini models

### Google Cloud tools[¶](#google-cloud-tools)

[
](/adk-docs/tools/google-cloud/apigee-api-hub/)

### Apigee API Hub

Turn any documented API from Apigee API hub into a tool

[
](/adk-docs/tools/google-cloud/api-registry/)

### API Registry

Dynamically connect with Google Cloud services as MCP tools

[
](/adk-docs/tools/google-cloud/application-integration/)

### Application Integration

Link your agents to enterprise apps using Integration Connectors

[
](/adk-docs/observability/bigquery-agent-analytics/)

### BigQuery Agent Analytics

Analyze and debug agent behavior at scale

[
](/adk-docs/tools/google-cloud/bigquery/)

### BigQuery Tools

Connect with BigQuery to retrieve data and perform analysis

[
](/adk-docs/tools/google-cloud/bigtable/)

### Bigtable Tools

Interact with Bigtable to retrieve data and execute SQL

[
](/adk-docs/tools/google-cloud/gke-code-executor/)

### GKE Code Executor

Run AI-generated code in a secure and scalable GKE environment

[
](/adk-docs/tools/google-cloud/spanner/)

### Spanner Tools

Interact with Spanner to retrieve data, search, and execute SQL

[
](/adk-docs/tools/google-cloud/mcp-toolbox-for-databases/)

### MCP Toolbox for Databases

Connect over 30 different data sources to your agents

[
](/adk-docs/tools/google-cloud/vertex-ai-rag-engine/)

### Vertex AI RAG Engine

Perform private data retrieval using Vertex AI RAG Engine

[
](/adk-docs/tools/google-cloud/vertex-ai-search/)

### Vertex AI Search

Search across your private, configured data stores in Vertex AI Search

### Third-party tools[¶](#third-party-tools)

[
](/adk-docs/tools/third-party/asana/)

### Asana

Manage projects, tasks, and goals for team collaboration

[
](/adk-docs/tools/third-party/atlassian/)

### Atlassian

Manage issues, search pages, and update team content

[
](/adk-docs/tools/third-party/cartesia/)

### Cartesia

Generate speech, localize voices, and create audio content

[
](/adk-docs/tools/third-party/elevenlabs/)

### ElevenLabs

Generate speech, clone voices, transcribe audio, and create sound effects

[
](/adk-docs/tools/third-party/github/)

### GitHub

Analyze code, manage issues and PRs, and automate workflows

[
](/adk-docs/tools/third-party/gitlab/)

### GitLab

Perform semantic code search, inspect pipelines, manage merge requests

[
](/adk-docs/tools/third-party/hugging-face/)

### Hugging Face

Access models, datasets, research papers, and AI tools

[
](/adk-docs/tools/third-party/linear/)

### Linear

Manage issues, track projects, and streamline development

[
](/adk-docs/tools/third-party/n8n/)

### n8n

Trigger automated workflows, connect apps, and process data

[
](/adk-docs/tools/third-party/notion/)

### Notion

Search workspaces, create pages, and manage tasks and databases

[
](/adk-docs/tools/third-party/postman/)

### Postman

Manage API collections, workspaces, and generate client code

[
](/adk-docs/tools/third-party/paypal/)

### Paypal

Manage payments, send invoices, and handle subscriptions

[
](/adk-docs/tools/third-party/qdrant/)

### Qdrant

Store and retrieve information using semantic vector search

[
](/adk-docs/tools/third-party/stripe/)

### Stripe

Manage payments, customers, subscriptions, and invoices

## Use pre-built tools with ADK agents[¶](#use-pre-built-tools-with-adk-agents)

Follow these general steps to include tools in your ADK agents:

**Import:**Import the desired tool from the tools module. This is`agents.tools`

in Python,`@google/adk`

in TypeScript,`google.golang.org/adk/tool`

in Go, or`com.google.adk.tools`

in Java.**Configure:**Initialize the tool, providing required parameters if any.**Register:**Add the initialized tool to thelist of your Agent.*tools*

Once added to an agent, the agent can decide to use the tool based on the user prompt and its instructions. The framework handles the execution of the tool when the agent calls it.

Note: Limitations on using multiple tools

Some ADK tools ** cannot be used with other tools in the same agent**.
For more information on tools with these limitations, see

[Limitations for ADK tools](/adk-docs/tools/limitations/#one-tool-one-agent).

## Build tools for agents[¶](#build-tools-for-agents)

If the above tools don't meet your needs, you can build tools for your ADK workflows using the following guides:

: Build custom tools for your specific ADK agent needs.[Function Tools](/adk-docs/tools-custom/function-tools/): Connect MCP servers as tools for your ADK agents.[MCP Tools](/adk-docs/tools-custom/mcp-tools/): Generate callable tools directly from an OpenAPI Specification.[OpenAPI Integration](/adk-docs/tools-custom/openapi-tools/)