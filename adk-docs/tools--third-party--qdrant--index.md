---
source_url: https://google.github.io/adk-docs/tools/third-party/qdrant/
fetched_at: 2026-01-25T02:05:20.608366
---

# Qdrant¶

# Qdrant[¶](#qdrant)

The [Qdrant MCP Server](https://github.com/qdrant/mcp-server-qdrant) connects
your ADK agent to [Qdrant](https://qdrant.tech/), an open-source vector search engine. This integration gives your agent the ability to store and
retrieve information using semantic search.

## Use cases[¶](#use-cases)

-
**Semantic Memory for Agents**: Store conversation context, facts, or learned information that agents can retrieve later using natural language queries. -
**Code Repository Search**: Build a searchable index of code snippets, documentation, and implementation patterns that can be queried semantically. -
**Knowledge Base Retrieval**: Create a retrieval-augmented generation (RAG) system by storing documents and retrieving relevant context for responses.

## Prerequisites[¶](#prerequisites)

- A running Qdrant instance. You can:
- Use
[Qdrant Cloud](https://cloud.qdrant.io/)(managed service) - Run locally with Docker:
`docker run -p 6333:6333 qdrant/qdrant`


- Use
- (Optional) A Qdrant API key for authentication

## Use with agent[¶](#use-with-agent)

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
QDRANT_URL = "http://localhost:6333" # Or your Qdrant Cloud URL
COLLECTION_NAME = "my_collection"
# QDRANT_API_KEY = "YOUR_QDRANT_API_KEY"
root_agent = Agent(
model="gemini-2.5-pro",
name="qdrant_agent",
instruction="Help users store and retrieve information using semantic search",
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params=StdioServerParameters(
command="uvx",
args=["mcp-server-qdrant"],
env={
"QDRANT_URL": QDRANT_URL,
"COLLECTION_NAME": COLLECTION_NAME,
# "QDRANT_API_KEY": QDRANT_API_KEY,
}
),
timeout=30,
),
)
],
)


## Available tools[¶](#available-tools)

| Tool | Description |
|---|---|
`qdrant-store` |
Store information in Qdrant with optional metadata |
`qdrant-find` |
Search for relevant information using natural language queries |

## Configuration[¶](#configuration)

The Qdrant MCP server can be configured using environment variables:

| Variable | Description | Default |
|---|---|---|
`QDRANT_URL` |
URL of the Qdrant server | `None` (required) |
`QDRANT_API_KEY` |
API key for Qdrant Cloud authentication | `None` |
`COLLECTION_NAME` |
Name of the collection to use | `None` |
`QDRANT_LOCAL_PATH` |
Path for local persistent storage (alternative to URL) | `None` |
`EMBEDDING_MODEL` |
Embedding model to use | `sentence-transformers/all-MiniLM-L6-v2` |
`EMBEDDING_PROVIDER` |
Provider for embeddings (`fastembed` or `ollama` ) |
`fastembed` |
`TOOL_STORE_DESCRIPTION` |
Custom description for the store tool | Default description |
`TOOL_FIND_DESCRIPTION` |
Custom description for the find tool | Default description |

### Custom tool descriptions[¶](#custom-tool-descriptions)

You can customize the tool descriptions to guide the agent's behavior:

env={
"QDRANT_URL": "http://localhost:6333",
"COLLECTION_NAME": "code-snippets",
"TOOL_STORE_DESCRIPTION": "Store code snippets with descriptions. The 'information' parameter should contain a description of what the code does, while the actual code should be in 'metadata.code'.",
"TOOL_FIND_DESCRIPTION": "Search for relevant code snippets using natural language. Describe the functionality you're looking for.",
}