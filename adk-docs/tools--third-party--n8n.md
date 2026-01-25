---
source_url: https://google.github.io/adk-docs/tools/third-party/n8n/
fetched_at: 2026-01-25T03:11:56.585628
---

# n8n¶

# n8n[¶](#n8n)

The [n8n MCP Server](https://docs.n8n.io/advanced-ai/accessing-n8n-mcp-server/)
connects your ADK agent to [n8n](https://n8n.io/), an extendable workflow
automation tool. This integration allows your agent to securely connect to an
n8n instance to search, inspect, and trigger workflows directly from a natural
language interface.

Alternative: Workflow-level MCP Server

The configuration guide  covers **Instance-level MCP access**,
which connects your agent to a central hub of enabled workflows.
Alternatively, you can use the
[MCP Server Trigger node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-langchain.mcptrigger/)
to make a **single workflow** act as its own standalone MCP server. This
method is useful if you want to craft specific server behaviors or expose
tools isolated to one workflow.

## Use cases[¶](#use-cases)

-
**Execute Complex Workflows**: Trigger multi-step business processes defined in n8n directly from your agent, leveraging reliable branching logic, loops, and error handling to ensure consistency. -
**Connect to External Apps**: Access pre-built integrations through n8n without writing custom tools for each service, eliminating the need to manage API authentication, headers, or boilerplate code. -
**Data Processing**: Offload complex data transformation tasks to n8n workflows, such as converting natural language into API calls or scraping and summarizing webpages, utilizing custom Python or JavaScript nodes for precise data shaping.

## Prerequisites[¶](#prerequisites)

- An active n8n instance
- MCP access enabled in settings
- A valid MCP access token

Refer to the
[n8n MCP documentation](https://docs.n8n.io/advanced-ai/accessing-n8n-mcp-server/)
for detailed setup instructions.

## Use with agent[¶](#use-with-agent)

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
N8N_INSTANCE_URL = "https://localhost:5678"
N8N_MCP_TOKEN = "YOUR_N8N_MCP_TOKEN"
root_agent = Agent(
model="gemini-2.5-pro",
name="n8n_agent",
instruction="Help users manage and execute workflows in n8n",
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params=StdioServerParameters(
command="npx",
args=[
"-y",
"supergateway",
"--streamableHttp",
f"{N8N_INSTANCE_URL}/mcp-server/http",
"--header",
f"authorization:Bearer {N8N_MCP_TOKEN}"
]
),
timeout=300,
),
)
],
)


from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StreamableHTTPServerParams
N8N_INSTANCE_URL = "https://localhost:5678"
N8N_MCP_TOKEN = "YOUR_N8N_MCP_TOKEN"
root_agent = Agent(
model="gemini-2.5-pro",
name="n8n_agent",
instruction="Help users manage and execute workflows in n8n",
tools=[
McpToolset(
connection_params=StreamableHTTPServerParams(
url=f"{N8N_INSTANCE_URL}/mcp-server/http",
headers={
"Authorization": f"Bearer {N8N_MCP_TOKEN}",
},
),
)
],
)


## Available tools[¶](#available-tools)

| Tool | Description |
|---|---|
`search_workflows` |
Search for available workflows |
`execute_workflow` |
Execute a specific workflow |
`get_workflow_details` |
Retrieve metadata and schema information for a workflow |

## Configuration[¶](#configuration)

To make workflows accessible to your agent, they must meet the following criteria:

-
**Be Active**: The workflow must be activated in n8n. -
**Supported Trigger**: Contain a Webhook, Schedule, Chat, or Form trigger node. -
**Enabled for MCP**: You must toggle "Available in MCP" in the workflow settings or select "Enable MCP access" from the workflow card menu.