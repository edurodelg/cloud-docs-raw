---
source_url: https://google.github.io/adk-docs/tools/third-party/asana/
fetched_at: 2026-01-25T02:05:01.708038
---

# Asana¶

# Asana[¶](#asana)

The [Asana MCP Server](https://developers.asana.com/docs/using-asanas-mcp-server)
connects your ADK agent to the [Asana](https://asana.com/) work management
platform. This integration gives your agent the ability to manage projects,
tasks, goals, and team collaboration using natural language.

## Use cases[¶](#use-cases)

-
**Track Project Status**: Get real-time updates on project progress, view status reports, and retrieve information about milestones and deadlines. -
**Manage Tasks**: Create, update, and organize tasks using natural language. Let your agent handle task assignments, status changes, and priority updates. -
**Monitor Goals**: Access and update Asana Goals to track team objectives and key results across your organization.

## Prerequisites[¶](#prerequisites)

- An
[Asana](https://asana.com/)account with access to a workspace

## Use with agent[¶](#use-with-agent)

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
root_agent = Agent(
model="gemini-2.5-pro",
name="asana_agent",
instruction="Help users manage projects, tasks, and goals in Asana",
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params=StdioServerParameters(
command="npx",
args=[
"-y",
"mcp-remote",
"https://mcp.asana.com/sse",
]
),
timeout=30,
),
)
],
)


Note

When you run this agent for the first time, a browser window opens automatically to request access via OAuth. Alternatively, you can use the authorization URL printed in the console. You must approve this request to allow the agent to access your Asana data.

## Available tools[¶](#available-tools)

Asana's MCP server includes 30+ tools organized by category. Tools are
automatically discovered when your agent connects. Use the
[ADK Web UI](/adk-docs/runtime/web-interface/) to view available tools in the
trace graph after running your agent.

| Category | Description |
|---|---|
| Project tracking | Get project status updates and reports |
| Task management | Create, update, and organize tasks |
| User information | Access user details and assignments |
| Goals | Track and update Asana Goals |
| Team organization | Manage team structures and membership |
| Object search | Quick typeahead search across Asana objects |