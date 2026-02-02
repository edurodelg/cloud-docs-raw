---
merged_at: 2026-02-02T16:04:42.281997
merged_files: 9
---


---
<!-- Source: https://google.github.io/adk-docs/tools/performance/ -->

# Redirecting...

You're being redirected to a
new destination
.

---
<!-- Source: https://google.github.io/adk-docs/tools/built-in-tools/ -->

# Redirecting...

You're being redirected to a
new destination
.

---
<!-- Source: https://google.github.io/adk-docs/tools/function-tools/ -->

# Redirecting...

You're being redirected to a
new destination
.

---
<!-- Source: https://google.github.io/adk-docs/tools/authentication/ -->

# Redirecting...

You're being redirected to a
new destination
.

---
<!-- Source: https://google.github.io/adk-docs/tools/limitations/ -->

# Limitations for ADK tools¶

# Limitations for ADK tools[¶](#limitations-for-adk-tools)

Some ADK tools have limitations that can impact how you implement them within an agent workflow. This page lists these tool limitations and workarounds, if available.

## One tool per agent limitation[¶](#one-tool-one-agent)

ONLY for Search in ADK Python v1.15.0 and lower

This limitation only applies to the use of Google Search and Vertex AI Search tools in ADK Python v1.15.0 and lower. ADK Python release v1.16.0 and higher provides a built-in workaround to remove this limitation.

In general, you can use more than one tool in an agent, but use of specific tools within an agent excludes the use of any other tools in that agent. The following ADK Tools can only be used by themselves, without any other tools, in a single agent object:

[Code Execution](/adk-docs/tools/gemini-api/code-execution/)with Gemini API[Google Search](/adk-docs/tools/gemini-api/google-search/)with Gemini API[Vertex AI Search](/adk-docs/tools/google-cloud/vertex-ai-search/)

For example, the following approach that uses one of these tools along with
other tools, within a single agent, is ** not supported**:

### Workaround #1: AgentTool.create() method[¶](#workaround-1-agenttoolcreate-method)

The following code sample demonstrates how to use multiple built-in tools or how to use built-in tools with other tools by using multiple agents:

from google.adk.tools.agent_tool import AgentTool
from google.adk.agents import Agent
from google.adk.tools import google_search
from google.adk.code_executors import BuiltInCodeExecutor
search_agent = Agent(
model='gemini-2.0-flash',
name='SearchAgent',
instruction="""
You're a specialist in Google Search
""",
tools=[google_search],
)
coding_agent = Agent(
model='gemini-2.0-flash',
name='CodeAgent',
instruction="""
You're a specialist in Code Execution
""",
code_executor=BuiltInCodeExecutor(),
)
root_agent = Agent(
name="RootAgent",
model="gemini-2.0-flash",
description="Root Agent",
tools=[AgentTool(agent=search_agent), AgentTool(agent=coding_agent)],
)


import com.google.adk.agents.BaseAgent;
import com.google.adk.agents.LlmAgent;
import com.google.adk.tools.AgentTool;
import com.google.adk.tools.BuiltInCodeExecutionTool;
import com.google.adk.tools.GoogleSearchTool;
import com.google.common.collect.ImmutableList;
public class NestedAgentApp {
private static final String MODEL_ID = "gemini-2.0-flash";
public static void main(String[] args) {
// Define the SearchAgent
LlmAgent searchAgent =
LlmAgent.builder()
.model(MODEL_ID)
.name("SearchAgent")
.instruction("You're a specialist in Google Search")
.tools(new GoogleSearchTool()) // Instantiate GoogleSearchTool
.build();
// Define the CodingAgent
LlmAgent codingAgent =
LlmAgent.builder()
.model(MODEL_ID)
.name("CodeAgent")
.instruction("You're a specialist in Code Execution")
.tools(new BuiltInCodeExecutionTool()) // Instantiate BuiltInCodeExecutionTool
.build();
// Define the RootAgent, which uses AgentTool.create() to wrap SearchAgent and CodingAgent
BaseAgent rootAgent =
LlmAgent.builder()
.name("RootAgent")
.model(MODEL_ID)
.description("Root Agent")
.tools(
AgentTool.create(searchAgent), // Use create method
AgentTool.create(codingAgent) // Use create method
)
.build();
// Note: This sample only demonstrates the agent definitions.
// To run these agents, you'd need to integrate them with a Runner and SessionService,
// similar to the previous examples.
System.out.println("Agents defined successfully:");
System.out.println(" Root Agent: " + rootAgent.name());
System.out.println(" Search Agent (nested): " + searchAgent.name());
System.out.println(" Code Agent (nested): " + codingAgent.name());
}
}


### Workaround #2: bypass_multi_tools_limit[¶](#workaround-2-bypass_multi_tools_limit)

ADK Python has a built-in workaround which bypasses this limitation for
`GoogleSearchTool`

and `VertexAiSearchTool`

(use `bypass_multi_tools_limit=True`

to enable it),
as shown in the
[built_in_multi_tools](https://github.com/google/adk-python/tree/main/contributing/samples/built_in_multi_tools).
sample agent.

Warning

Built-in tools cannot be used within a sub-agent, with the exception of
`GoogleSearchTool`

and `VertexAiSearchTool`

in ADK Python because of the
workaround mentioned above.

For example, the following approach that uses built-in tools within sub-agents
is **not supported**:

url_context_agent = Agent(
model='gemini-2.5-flash',
name='UrlContextAgent',
instruction="""
You're a specialist in URL Context
""",
tools=[url_context],
)
coding_agent = Agent(
model='gemini-2.5-flash',
name='CodeAgent',
instruction="""
You're a specialist in Code Execution
""",
code_executor=BuiltInCodeExecutor(),
)
root_agent = Agent(
name="RootAgent",
model="gemini-2.5-flash",
description="Root Agent",
sub_agents=[
url_context_agent,
coding_agent
],
)


LlmAgent searchAgent =
LlmAgent.builder()
.model("gemini-2.5-flash")
.name("SearchAgent")
.instruction("You're a specialist in Google Search")
.tools(new GoogleSearchTool())
.build();
LlmAgent codingAgent =
LlmAgent.builder()
.model("gemini-2.5-flash")
.name("CodeAgent")
.instruction("You're a specialist in Code Execution")
.tools(new BuiltInCodeExecutionTool())
.build();
LlmAgent rootAgent =
LlmAgent.builder()
.name("RootAgent")
.model("gemini-2.5-flash")
.description("Root Agent")
.subAgents(searchAgent, codingAgent) // Not supported, as the sub agents use built in tools.
.build();

---
<!-- Source: https://google.github.io/adk-docs/tools/ -->

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
](/adk-docs/tools/third-party/chroma/)

### Chroma

Store and retrieve information using semantic vector search

[
](/adk-docs/tools/third-party/daytona/)

### Daytona

Execute code, run shell commands, and manage files in secure sandboxes

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
](/adk-docs/tools/third-party/mongodb/)

### MongoDB

Query collections, manage databases, and analyze schemas

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

---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/tools/gemini-api/ -->

# Gemini API tools¶

Gemini API tools¶ Check out the following Gemini tools that you can use with ADK agents: Google Search Perform web searches using Google Search with Gemini Code Execution Execute code and debug using Gemini models Computer Use Operate computer user interfaces using Gemini models

---
<!-- Source: https://google.github.io/adk-docs/tools/gemini-api/computer-use/ -->

# Computer Use Toolset with Gemini API¶

# Computer Use Toolset with Gemini API[¶](#computer-use-toolset-with-gemini-api)

The Computer Use Toolset allows an agent to operate a user interface
of a computer, such as browsers, to complete tasks. This tool uses
a specific Gemini model and the [Playwright](https://playwright.dev/)
testing tool to control a Chromium browser and can interact with
web pages by taking screenshots, clicking, typing, and navigating.

For more information about the computer use model, see
Gemini API [Computer use](https://ai.google.dev/gemini-api/docs/computer-use)
or the Google Cloud Vertex AI API
[Computer use](https://cloud.google.com/vertex-ai/generative-ai/docs/computer-use).

Preview release

The Computer Use model and tool is a Preview release. For
more information, see the
[launch stage descriptions](https://cloud.google.com/products#product-launch-stages).

## Setup[¶](#setup)

You must install Playwright and its dependencies, including Chromium, to be able to use the Computer Use Toolset.

## Recommended: create and activate a Python virtual environment

Create a Python virtual environment:

Activate the Python virtual environment:

To set up the required software libraries for the Computer Use Toolset:

- Install Python dependencies:
- Install the Playwright dependencies, including the Chromium browser:

## Use the tool[¶](#use-the-tool)

Use the Computer Use Toolset by adding it as a tool to your agent. When you
configure the tool, you must provide a implementation of the `BaseComputer`

class which defines an interface for an agent to use a computer. In the
following example, the `PlaywrightComputer`

class is defined for this purpose.
You can find the code for this implementation in `playwright.py`

file of the
[computer_use](https://github.com/google/adk-python/blob/main/contributing/samples/computer_use/playwright.py)
agent sample project.

from google.adk import Agent
from google.adk.models.google_llm import Gemini
from google.adk.tools.computer_use.computer_use_toolset import ComputerUseToolset
from typing_extensions import override
from .playwright import PlaywrightComputer
root_agent = Agent(
model='gemini-2.5-computer-use-preview-10-2025',
name='hello_world_agent',
description=(
'computer use agent that can operate a browser on a computer to finish'
' user tasks'
),
instruction='you are a computer use agent',
tools=[
ComputerUseToolset(computer=PlaywrightComputer(screen_size=(1280, 936)))
],
)


For a complete code example, see the
[computer_use](https://github.com/google/adk-python/tree/main/contributing/samples/computer_use)
agent sample project.

---
<!-- Source: https://google.github.io/adk-docs/tools/gemini-api/code-execution/ -->

# Code Execution with Gemini API¶

# Code Execution with Gemini API[¶](#code-execution-with-gemini-api)

Supported in ADKPython v0.1.0Java v0.2.0

The `built_in_code_execution`

tool enables the agent to execute code,
specifically when using Gemini 2 and higher models. This allows the model to
perform tasks like calculations, data manipulation, or running small scripts.

Warning: Single tool per agent limitation

This tool can only be used ** by itself** within an agent instance.
For more information about this limitation and workarounds, see

[Limitations for ADK tools](/adk-docs/tools/limitations/#one-tool-one-agent).

# Copyright 2025 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
import asyncio
from google.adk.agents import LlmAgent
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.adk.code_executors import BuiltInCodeExecutor
from google.genai import types
AGENT_NAME = "calculator_agent"
APP_NAME = "calculator"
USER_ID = "user1234"
SESSION_ID = "session_code_exec_async"
GEMINI_MODEL = "gemini-2.0-flash"
# Agent Definition
code_agent = LlmAgent(
name=AGENT_NAME,
model=GEMINI_MODEL,
code_executor=BuiltInCodeExecutor(),
instruction="""You are a calculator agent.
When given a mathematical expression, write and execute Python code to calculate the result.
Return only the final numerical result as plain text, without markdown or code blocks.
""",
description="Executes Python code to perform calculations.",
)
# Session and Runner
session_service = InMemorySessionService()
session = asyncio.run(session_service.create_session(
app_name=APP_NAME, user_id=USER_ID, session_id=SESSION_ID
))
runner = Runner(agent=code_agent, app_name=APP_NAME,
session_service=session_service)
# Agent Interaction (Async)
async def call_agent_async(query):
content = types.Content(role="user", parts=[types.Part(text=query)])
print(f"\n--- Running Query: {query} ---")
final_response_text = "No final text response captured."
try:
# Use run_async
async for event in runner.run_async(
user_id=USER_ID, session_id=SESSION_ID, new_message=content
):
print(f"Event ID: {event.id}, Author: {event.author}")
# --- Check for specific parts FIRST ---
has_specific_part = False
if event.content and event.content.parts:
for part in event.content.parts: # Iterate through all parts
if part.executable_code:
# Access the actual code string via .code
print(
f" Debug: Agent generated code:\n```python\n{part.executable_code.code}\n```"
)
has_specific_part = True
elif part.code_execution_result:
# Access outcome and output correctly
print(
f" Debug: Code Execution Result: {part.code_execution_result.outcome} - Output:\n{part.code_execution_result.output}"
)
has_specific_part = True
# Also print any text parts found in any event for debugging
elif part.text and not part.text.isspace():
print(f" Text: '{part.text.strip()}'")
# Do not set has_specific_part=True here, as we want the final response logic below
# --- Check for final response AFTER specific parts ---
# Only consider it final if it doesn't have the specific code parts we just handled
if not has_specific_part and event.is_final_response():
if (
event.content
and event.content.parts
and event.content.parts[0].text
):
final_response_text = event.content.parts[0].text.strip()
print(f"==> Final Agent Response: {final_response_text}")
else:
print(
"==> Final Agent Response: [No text content in final event]")
except Exception as e:
print(f"ERROR during agent run: {e}")
print("-" * 30)
# Main async function to run the examples
async def main():
await call_agent_async("Calculate the value of (5 + 7) * 3")
await call_agent_async("What is 10 factorial?")
# Execute the main async function
try:
asyncio.run(main())
except RuntimeError as e:
# Handle specific error when running asyncio.run in an already running loop (like Jupyter/Colab)
if "cannot be called from a running event loop" in str(e):
print("\nRunning in an existing event loop (like Colab/Jupyter).")
print("Please run `await main()` in a notebook cell instead.")
# If in an interactive environment like a notebook, you might need to run:
# await main()
else:
raise e # Re-raise other runtime errors


import com.google.adk.agents.BaseAgent;
import com.google.adk.agents.LlmAgent;
import com.google.adk.runner.Runner;
import com.google.adk.sessions.InMemorySessionService;
import com.google.adk.sessions.Session;
import com.google.adk.tools.BuiltInCodeExecutionTool;
import com.google.common.collect.ImmutableList;
import com.google.genai.types.Content;
import com.google.genai.types.Part;
public class CodeExecutionAgentApp {
private static final String AGENT_NAME = "calculator_agent";
private static final String APP_NAME = "calculator";
private static final String USER_ID = "user1234";
private static final String SESSION_ID = "session_code_exec_sync";
private static final String GEMINI_MODEL = "gemini-2.0-flash";
/**
* Calls the agent with a query and prints the interaction events and final response.
*
* @param runner The runner instance for the agent.
* @param query The query to send to the agent.
*/
public static void callAgent(Runner runner, String query) {
Content content =
Content.builder().role("user").parts(ImmutableList.of(Part.fromText(query))).build();
InMemorySessionService sessionService = (InMemorySessionService) runner.sessionService();
Session session =
sessionService
.createSession(APP_NAME, USER_ID, /* state= */ null, SESSION_ID)
.blockingGet();
System.out.println("\n--- Running Query: " + query + " ---");
final String[] finalResponseText = {"No final text response captured."};
try {
runner
.runAsync(session.userId(), session.id(), content)
.forEach(
event -> {
System.out.println("Event ID: " + event.id() + ", Author: " + event.author());
boolean hasSpecificPart = false;
if (event.content().isPresent() && event.content().get().parts().isPresent()) {
for (Part part : event.content().get().parts().get()) {
if (part.executableCode().isPresent()) {
System.out.println(
" Debug: Agent generated code:\n```python\n"
+ part.executableCode().get().code()
+ "\n```");
hasSpecificPart = true;
} else if (part.codeExecutionResult().isPresent()) {
System.out.println(
" Debug: Code Execution Result: "
+ part.codeExecutionResult().get().outcome()
+ " - Output:\n"
+ part.codeExecutionResult().get().output());
hasSpecificPart = true;
} else if (part.text().isPresent() && !part.text().get().trim().isEmpty()) {
System.out.println(" Text: '" + part.text().get().trim() + "'");
}
}
}
if (!hasSpecificPart && event.finalResponse()) {
if (event.content().isPresent()
&& event.content().get().parts().isPresent()
&& !event.content().get().parts().get().isEmpty()
&& event.content().get().parts().get().get(0).text().isPresent()) {
finalResponseText[0] =
event.content().get().parts().get().get(0).text().get().trim();
System.out.println("==> Final Agent Response: " + finalResponseText[0]);
} else {
System.out.println(
"==> Final Agent Response: [No text content in final event]");
}
}
});
} catch (Exception e) {
System.err.println("ERROR during agent run: " + e.getMessage());
e.printStackTrace();
}
System.out.println("------------------------------");
}
public static void main(String[] args) {
BuiltInCodeExecutionTool codeExecutionTool = new BuiltInCodeExecutionTool();
BaseAgent codeAgent =
LlmAgent.builder()
.name(AGENT_NAME)
.model(GEMINI_MODEL)
.tools(ImmutableList.of(codeExecutionTool))
.instruction(
"""
You are a calculator agent.
When given a mathematical expression, write and execute Python code to calculate the result.
Return only the final numerical result as plain text, without markdown or code blocks.
""")
.description("Executes Python code to perform calculations.")
.build();
InMemorySessionService sessionService = new InMemorySessionService();
Runner runner = new Runner(codeAgent, APP_NAME, null, sessionService);
callAgent(runner, "Calculate the value of (5 + 7) * 3");
callAgent(runner, "What is 10 factorial?");
}
}

---
<!-- Source: https://google.github.io/adk-docs/tools/gemini-api/google-search/ -->

# Google Search tool for ADK¶

# Google Search tool for ADK[¶](#google-search-tool-for-adk)

The `google_search`

tool allows the agent to perform web searches using Google Search. The `google_search`

tool is only compatible with Gemini 2 models. For further details of the tool, see [Understanding Google Search grounding](/adk-docs/grounding/google_search_grounding/).

Additional requirements when using the `google_search`

tool

When you use grounding with Google Search, and you receive Search suggestions in your response, you must display the Search suggestions in production and in your applications.
For more information on grounding with Google Search, see Grounding with Google Search documentation for [Google AI Studio](https://ai.google.dev/gemini-api/docs/grounding/search-suggestions) or [Vertex AI](https://cloud.google.com/vertex-ai/generative-ai/docs/grounding/grounding-search-suggestions). The UI code (HTML) is returned in the Gemini response as `renderedContent`

, and you will need to show the HTML in your app, in accordance with the policy.

Warning: Single tool per agent limitation

This tool can only be used ** by itself** within an agent instance.
For more information about this limitation and workarounds, see

[Limitations for ADK tools](/adk-docs/tools/limitations/#one-tool-one-agent).

# Copyright 2025 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
from google.adk.agents import Agent
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.adk.tools import google_search
from google.genai import types
APP_NAME="google_search_agent"
USER_ID="user1234"
SESSION_ID="1234"
root_agent = Agent(
name="basic_search_agent",
model="gemini-2.0-flash",
description="Agent to answer questions using Google Search.",
instruction="I can answer your questions by searching the internet. Just ask me anything!",
# google_search is a pre-built tool which allows the agent to perform Google searches.
tools=[google_search]
)
# Session and Runner
async def setup_session_and_runner():
session_service = InMemorySessionService()
session = await session_service.create_session(app_name=APP_NAME, user_id=USER_ID, session_id=SESSION_ID)
runner = Runner(agent=root_agent, app_name=APP_NAME, session_service=session_service)
return session, runner
# Agent Interaction
async def call_agent_async(query):
content = types.Content(role='user', parts=[types.Part(text=query)])
session, runner = await setup_session_and_runner()
events = runner.run_async(user_id=USER_ID, session_id=SESSION_ID, new_message=content)
async for event in events:
if event.is_final_response():
final_response = event.content.parts[0].text
print("Agent Response: ", final_response)
# Note: In Colab, you can directly use 'await' at the top level.
# If running this code as a standalone Python script, you'll need to use asyncio.run() or manage the event loop.
await call_agent_async("what's the latest ai news?")


import {GOOGLE_SEARCH, LlmAgent} from '@google/adk';
export const rootAgent = new LlmAgent({
model: 'gemini-2.5-flash',
name: 'root_agent',
description:
'an agent whose job it is to perform Google search queries and answer questions about the results.',
instruction:
'You are an agent whose job is to perform Google search queries and answer questions about the results.',
tools: [GOOGLE_SEARCH],
});


// Copyright 2025 Google LLC
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at
//
// http://www.apache.org/licenses/LICENSE-2.0
//
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.
package main
import (
"context"
"fmt"
"log"
"google.golang.org/adk/agent"
"google.golang.org/adk/agent/llmagent"
"google.golang.org/adk/model/gemini"
"google.golang.org/adk/runner"
"google.golang.org/adk/session"
"google.golang.org/adk/tool"
"google.golang.org/adk/tool/geminitool"
"google.golang.org/genai"
)
func createSearchAgent(ctx context.Context) (agent.Agent, error) {
model, err := gemini.NewModel(ctx, "gemini-2.5-flash", &genai.ClientConfig{})
if err != nil {
return nil, fmt.Errorf("failed to create model: %v", err)
}
return llmagent.New(llmagent.Config{
Name: "basic_search_agent",
Model: model,
Description: "Agent to answer questions using Google Search.",
Instruction: "I can answer your questions by searching the web. Just ask me anything!",
Tools: []tool.Tool{geminitool.GoogleSearch{}},
})
}
const (
userID = "user1234"
appName = "Google Search_agent"
)
func callAgent(ctx context.Context, a agent.Agent, prompt string) error {
sessionService := session.InMemoryService()
session, err := sessionService.Create(ctx, &session.CreateRequest{
AppName: appName,
UserID: userID,
})
if err != nil {
return fmt.Errorf("failed to create the session service: %v", err)
}
config := runner.Config{
AppName: appName,
Agent: a,
SessionService: sessionService,
}
r, err := runner.New(config)
if err != nil {
return fmt.Errorf("failed to create the runner: %v", err)
}
sessionID := session.Session.ID()
userMsg := &genai.Content{
Parts: []*genai.Part{{Text: prompt}},
Role: string(genai.RoleUser),
}
// The r.Run method streams events and errors.
// The loop iterates over the results, handling them as they arrive.
for event, err := range r.Run(ctx, userID, sessionID, userMsg, agent.RunConfig{
StreamingMode: agent.StreamingModeSSE,
}) {
if err != nil {
fmt.Printf("\nAGENT_ERROR: %v\n", err)
} else if event.Partial {
for _, p := range event.LLMResponse.Content.Parts {
fmt.Print(p.Text)
}
}
}
return nil
}
func main() {
agent, err := createSearchAgent(context.Background())
if err != nil {
log.Fatalf("Failed to create agent: %v", err)
}
fmt.Println("Agent created:", agent.Name())
prompt := "what's the latest ai news?"
fmt.Printf("\nPrompt: %s\nResponse: ", prompt)
if err := callAgent(context.Background(), agent, prompt); err != nil {
log.Fatalf("Error calling agent: %v", err)
}
fmt.Println("\n---")
}


import com.google.adk.agents.BaseAgent;
import com.google.adk.agents.LlmAgent;
import com.google.adk.runner.Runner;
import com.google.adk.sessions.InMemorySessionService;
import com.google.adk.sessions.Session;
import com.google.adk.tools.GoogleSearchTool;
import com.google.common.collect.ImmutableList;
import com.google.genai.types.Content;
import com.google.genai.types.Part;
public class GoogleSearchAgentApp {
private static final String APP_NAME = "Google Search_agent";
private static final String USER_ID = "user1234";
private static final String SESSION_ID = "1234";
/**
* Calls the agent with the given query and prints the final response.
*
* @param runner The runner to use.
* @param query The query to send to the agent.
*/
public static void callAgent(Runner runner, String query) {
Content content =
Content.fromParts(Part.fromText(query));
InMemorySessionService sessionService = (InMemorySessionService) runner.sessionService();
Session session =
sessionService
.createSession(APP_NAME, USER_ID, /* state= */ null, SESSION_ID)
.blockingGet();
runner
.runAsync(session.userId(), session.id(), content)
.forEach(
event -> {
if (event.finalResponse()
&& event.content().isPresent()
&& event.content().get().parts().isPresent()
&& !event.content().get().parts().get().isEmpty()
&& event.content().get().parts().get().get(0).text().isPresent()) {
String finalResponse = event.content().get().parts().get().get(0).text().get();
System.out.println("Agent Response: " + finalResponse);
}
});
}
public static void main(String[] args) {
// Google Search is a pre-built tool which allows the agent to perform Google searches.
GoogleSearchTool googleSearchTool = new GoogleSearchTool();
BaseAgent rootAgent =
LlmAgent.builder()
.name("basic_search_agent")
.model("gemini-2.0-flash") // Ensure to use a Gemini 2.0 model for Google Search Tool
.description("Agent to answer questions using Google Search.")
.instruction(
"I can answer your questions by searching the internet. Just ask me anything!")
.tools(ImmutableList.of(googleSearchTool))
.build();
// Session and Runner
InMemorySessionService sessionService = new InMemorySessionService();
Runner runner = new Runner(rootAgent, APP_NAME, null, sessionService);
// Agent Interaction
callAgent(runner, "what's the latest ai news?");
}
}

---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/daytona/ -->

# Daytona¶

# Daytona[¶](#daytona)

The [Daytona ADK plugin](https://github.com/daytonaio/daytona-adk-plugin) connects your ADK
agent to [Daytona](https://www.daytona.io/) sandboxes. This integration gives
your agent the ability to execute code, run shell commands, and manage files in
isolated environments, enabling secure execution of AI-generated code.

## Use cases[¶](#use-cases)

-
**Secure Code Execution**: Run Python, JavaScript, and TypeScript code in isolated sandboxes without risking your local environment. -
**Shell Command Automation**: Execute shell commands with configurable timeouts and working directories for build tasks, installations, or system operations. -
**File Management**: Upload scripts and datasets to sandboxes, then retrieve generated outputs and results.

## Prerequisites[¶](#prerequisites)

- A
[Daytona](https://www.daytona.io/)account - Daytona API key

## Installation[¶](#installation)

## Use with agent[¶](#use-with-agent)

from daytona_adk import DaytonaPlugin
from google.adk.agents import Agent
plugin = DaytonaPlugin(
api_key="your-daytona-api-key" # Or set DAYTONA_API_KEY environment variable
)
root_agent = Agent(
model="gemini-2.5-pro",
name="sandbox_agent",
instruction="Help users execute code and commands in a secure sandbox",
tools=plugin.get_tools(),
)


## Available tools[¶](#available-tools)

| Tool | Description |
|---|---|
`execute_code_in_daytona` |
Execute Python, JavaScript, or TypeScript code |
`execute_command_in_daytona` |
Run shell commands |
`upload_file_to_daytona` |
Upload scripts or data files to the sandbox |
`read_file_from_daytona` |
Read script outputs or generated files |
`start_long_running_command_daytona` |
Start background processes (servers, watchers) |

## Learn more[¶](#learn-more)

For a detailed guide on building a code generator agent that writes, tests, and
verifies code in secure sandboxes, check out
[this guide](https://www.daytona.io/docs/en/google-adk-code-generator).

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/ -->

# Third-Party Tools¶

# Third-Party Tools[¶](#third-party-tools)

Check out the following third-party tools that you can use with ADK agents:

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
](/adk-docs/tools/third-party/chroma/)

### Chroma

Store and retrieve information using semantic vector search

[
](/adk-docs/tools/third-party/daytona/)

### Daytona

Execute code, run shell commands, and manage files in secure sandboxes

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
](/adk-docs/tools/third-party/mongodb/)

### MongoDB

Query collections, manage databases, and analyze schemas

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

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/asana/ -->

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


import { LlmAgent, MCPToolset } from "@google/adk";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "asana_agent",
instruction: "Help users manage projects, tasks, and goals in Asana",
tools: [
new MCPToolset({
type: "StdioConnectionParams",
serverParams: {
command: "npx",
args: [
"-y",
"mcp-remote",
"https://mcp.asana.com/sse",
],
},
}),
],
});
export { rootAgent };


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

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/cartesia/ -->

# Cartesia¶

# Cartesia[¶](#cartesia)

The [Cartesia MCP Server](https://github.com/cartesia-ai/cartesia-mcp) connects
your ADK agent to the [Cartesia](https://cartesia.ai/) AI audio platform. This
integration gives your agent the ability to generate speech, localize voices
across languages, and create audio content using natural language.

## Use cases[¶](#use-cases)

-
**Text-to-Speech Generation**: Convert text into natural-sounding speech using Cartesia's diverse voice library, with control over voice selection and output format. -
**Voice Localization**: Transform existing voices into different languages while preserving the original speaker's characteristics—ideal for multilingual content creation. -
**Audio Infill**: Fill gaps between audio segments to create smooth transitions, useful for podcast editing or audiobook production. -
**Voice Transformation**: Convert audio clips to sound like different voices from Cartesia's library.

## Prerequisites[¶](#prerequisites)

- Sign up for a
[Cartesia account](https://play.cartesia.ai/sign-in) - Generate an
[API key](https://play.cartesia.ai/keys)from the Cartesia playground

## Use with agent[¶](#use-with-agent)

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
CARTESIA_API_KEY = "YOUR_CARTESIA_API_KEY"
root_agent = Agent(
model="gemini-2.5-pro",
name="cartesia_agent",
instruction="Help users generate speech and work with audio content",
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params=StdioServerParameters(
command="uvx",
args=["cartesia-mcp"],
env={
"CARTESIA_API_KEY": CARTESIA_API_KEY,
# "OUTPUT_DIRECTORY": "/path/to/output", # Optional
}
),
timeout=30,
),
)
],
)


import { LlmAgent, MCPToolset } from "@google/adk";
const CARTESIA_API_KEY = "YOUR_CARTESIA_API_KEY";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "cartesia_agent",
instruction: "Help users generate speech and work with audio content",
tools: [
new MCPToolset({
type: "StdioConnectionParams",
serverParams: {
command: "uvx",
args: ["cartesia-mcp"],
env: {
CARTESIA_API_KEY: CARTESIA_API_KEY,
// OUTPUT_DIRECTORY: "/path/to/output", // Optional
},
},
}),
],
});
export { rootAgent };


## Available tools[¶](#available-tools)

| Tool | Description |
|---|---|
`text_to_speech` |
Convert text to audio using a specified voice |
`list_voices` |
List all available Cartesia voices |
`get_voice` |
Get details about a specific voice |
`clone_voice` |
Clone a voice from audio samples |
`update_voice` |
Update an existing voice |
`delete_voice` |
Delete a voice from your library |
`localize_voice` |
Transform a voice into a different language |
`voice_change` |
Convert an audio file to use a different voice |
`infill` |
Fill gaps between audio segments |

## Configuration[¶](#configuration)

The Cartesia MCP server can be configured using environment variables:

| Variable | Description | Required |
|---|---|---|
`CARTESIA_API_KEY` |
Your Cartesia API key | Yes |
`OUTPUT_DIRECTORY` |
Directory to store generated audio files | No |

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/ag-ui/ -->

# Build chat experiences with AG-UI and CopilotKit¶

# Build chat experiences with AG-UI and CopilotKit[¶](#build-chat-experiences-with-ag-ui-and-copilotkit)

As an agent builder, you want users to interact with your agents through a rich
and responsive interface. Building UIs from scratch requires a lot of effort,
especially to support streaming events and client state. That's exactly what
[AG-UI](https://docs.ag-ui.com/) was designed for - rich user experiences
directly connected to an agent.

[AG-UI](https://github.com/ag-ui-protocol/ag-ui) provides a consistent interface
to empower rich clients across technology stacks, from mobile to the web and
even the command line. There are a number of different clients that support
AG-UI:

[CopilotKit](https://copilotkit.ai)provides tooling and components to tightly integrate your agent with web applications- Clients for
[Kotlin](https://github.com/ag-ui-protocol/ag-ui/tree/main/sdks/community/kotlin),[Java](https://github.com/ag-ui-protocol/ag-ui/tree/main/sdks/community/java),[Go](https://github.com/ag-ui-protocol/ag-ui/tree/main/sdks/community/go/example/client), and[CLI implementations](https://github.com/ag-ui-protocol/ag-ui/tree/main/apps/client-cli-example/src)in TypeScript

This tutorial uses CopilotKit to create a sample app backed by an ADK agent that demonstrates some of the features supported by AG-UI.

## Quickstart[¶](#quickstart)

To get started, let's create a sample application with an ADK agent and a simple web client:

### Chat[¶](#chat)

Chat is a familiar interface for exposing your agent, and AG-UI handles streaming messages between your users and agents:

<CopilotSidebar
clickOutsideToClose={false}
defaultOpen={true}
labels={{
title: "Popup Assistant",
initial: "👋 Hi, there! You're chatting with an agent. This agent comes with a few tools to get you started..."
}}
/>


Learn more about the chat UI
[in the CopilotKit docs](https://docs.copilotkit.ai/adk/agentic-chat-ui).

### Tool Based Generative UI (Rendering Tools)[¶](#tool-based-generative-ui-rendering-tools)

AG-UI lets you share tool information with a Generative UI so that it can be displayed to users:

useCopilotAction({
name: "get_weather",
description: "Get the weather for a given location.",
available: "disabled",
parameters: [
{ name: "location", type: "string", required: true },
],
render: ({ args }) => {
return <WeatherCard location={args.location} themeColor={themeColor} />
},
});


Learn more about the Tool-based Generative UI
[in the CopilotKit docs](https://docs.copilotkit.ai/adk/generative-ui/tool-based).

### Shared State[¶](#shared-state)

ADK agents can be stateful, and synchronizing that state between your agents and your UIs enables powerful and fluid user experiences. State can be synchronized both ways so agents are automatically aware of changes made by your user or other parts of your application:

const { state, setState } = useCoAgent<AgentState>({
name: "my_agent",
initialState: {
proverbs: [
"CopilotKit may be new, but its the best thing since sliced bread.",
],
},
})


Learn more about shared state
[in the CopilotKit docs](https://docs.copilotkit.ai/adk/shared-state).

### Try it out![¶](#try-it-out)

## Resources[¶](#resources)

To see what other features you can build into your UI with AG-UI, refer to the CopilotKit docs:

Or try them out in the [AG-UI Dojo](https://dojo.ag-ui.com).

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/notion/ -->

# Notion¶

# Notion[¶](#notion)

Supported in ADKPython v0.1.0TypeScript v0.2.0

The [Notion MCP Server](https://github.com/makenotion/notion-mcp-server)
connects your ADK agent to Notion, allowing it to search, create, and manage
pages, databases, and more within a workspace. This gives your agent the ability
to query, create, and organize content in your Notion workspace using natural
language.

## Use cases[¶](#use-cases)

-
**Search your workspace**: Find project pages, meeting notes, or documents based on content. -
**Create new content**: Generate new pages for meeting notes, project plans, or tasks. -
**Manage tasks and databases**: Update the status of a task, add items to a database, or change properties. -
**Organize your workspace**: Move pages, duplicate templates, or add comments to documents.

## Prerequisites[¶](#prerequisites)

- Obtain a Notion integration token by going to
[Notion Integrations](https://www.notion.so/profile/integrations)in your profile. Refer to the[authorization documentation](https://developers.notion.com/docs/authorization)for more details. - Ensure relevant pages and databases can be accessed by your integration. Visit
the Access tab in your
[Notion Integration](https://www.notion.so/profile/integrations)settings, then grant access by selecting the pages you'd like to use.

## Use with agent[¶](#use-with-agent)

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
NOTION_TOKEN = "YOUR_NOTION_TOKEN"
root_agent = Agent(
model="gemini-2.5-pro",
name="notion_agent",
instruction="Help users get information from Notion",
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params = StdioServerParameters(
command="npx",
args=[
"-y",
"@notionhq/notion-mcp-server",
],
env={
"NOTION_TOKEN": NOTION_TOKEN,
}
),
timeout=30,
),
)
],
)


import { LlmAgent, MCPToolset } from "@google/adk";
const NOTION_TOKEN = "YOUR_NOTION_TOKEN";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "notion_agent",
instruction: "Help users get information from Notion",
tools: [
new MCPToolset({
type: "StdioConnectionParams",
serverParams: {
command: "npx",
args: ["-y", "@notionhq/notion-mcp-server"],
env: {
NOTION_TOKEN: NOTION_TOKEN,
},
},
}),
],
});
export { rootAgent };


## Available tools[¶](#available-tools)

| Tool | Description |
|---|---|
`notion-search` |
Search across your Notion workspace and connected tools like Slack, Google Drive, and Jira. Falls back to basic workspace search if AI features aren’t available. |
`notion-fetch` |
Retrieves content from a Notion page or database by its URL |
`notion-create-pages` |
Creates one or more Notion pages with specified properties and content. |
`notion-update-page` |
Update a Notion page's properties or content. |
`notion-move-pages` |
Move one or more Notion pages or databases to a new parent. |
`notion-duplicate-page` |
Duplicate a Notion page within your workspace. This action is completed async. |
`notion-create-database` |
Creates a new Notion database, initial data source, and initial view with the specified properties. |
`notion-update-database` |
Update a Notion data source's properties, name, description, or other attributes. |
`notion-create-comment` |
Add a comment to a page |
`notion-get-comments` |
Lists all comments on a specific page, including threaded discussions. |
`notion-get-teams` |
Retrieves a list of teams (teamspaces) in the current workspace. |
`notion-get-users` |
Lists all users in the workspace with their details. |
`notion-get-user` |
Retrieve your user information by ID |
`notion-get-self` |
Retrieves information about your own bot user and the Notion workspace you’re connected to. |

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/gitlab/ -->

# GitLab¶

# GitLab[¶](#gitlab)

The
[GitLab MCP Server](https://docs.gitlab.com/user/gitlab_duo/model_context_protocol/mcp_server/)
connects your ADK agent directly to [GitLab.com](https://gitlab.com/) or your
self-managed GitLab instance. This integration gives your agent the ability to
manage issues and merge requests, inspect CI/CD pipelines, perform semantic code
searches, and automate development workflows using natural language.

## Use cases[¶](#use-cases)

-
**Semantic Code Exploration**: Navigate your codebase using natural language. Unlike standard text search, you can query the logic and intent of your code to quickly understand complex implementations. -
**Accelerate Merge Request Reviews**: Get up to speed on code changes instantly. Retrieve full merge request contexts, analyze specific diffs, and review commit history to provide faster, more meaningful feedback to your team. -
**Troubleshoot CI/CD Pipelines**: Diagnose build failures without leaving your chat. Inspect pipeline statuses and retrieve detailed job logs to pinpoint exactly why a specific merge request or commit failed its checks.

## Prerequisites[¶](#prerequisites)

- A GitLab account with a Premium or Ultimate subscription and
[GitLab Duo](https://docs.gitlab.com/user/gitlab_duo/)enabled [Beta and experimental features](https://docs.gitlab.com/user/gitlab_duo/turn_on_off/#turn-on-beta-and-experimental-features)enabled in your GitLab settings

## Use with agent[¶](#use-with-agent)

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
# Replace with your instance URL if self-hosted (e.g., "gitlab.example.com")
GITLAB_INSTANCE_URL = "gitlab.com"
root_agent = Agent(
model="gemini-2.5-pro",
name="gitlab_agent",
instruction="Help users get information from GitLab",
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params = StdioServerParameters(
command="npx",
args=[
"-y",
"mcp-remote",
f"https://{GITLAB_INSTANCE_URL}/api/v4/mcp",
"--static-oauth-client-metadata",
"{\"scope\": \"mcp\"}",
],
),
timeout=30,
),
)
],
)


import { LlmAgent, MCPToolset } from "@google/adk";
// Replace with your instance URL if self-hosted (e.g., "gitlab.example.com")
const GITLAB_INSTANCE_URL = "gitlab.com";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "gitlab_agent",
instruction: "Help users get information from GitLab",
tools: [
new MCPToolset({
type: "StdioConnectionParams",
serverParams: {
command: "npx",
args: [
"-y",
"mcp-remote",
`https://${GITLAB_INSTANCE_URL}/api/v4/mcp`,
"--static-oauth-client-metadata",
'{"scope": "mcp"}',
],
},
}),
],
});
export { rootAgent };


Note

When you run this agent for the first time, a browser window will open automatically (and an authorization URL will be printed) requesting OAuth permissions. You must approve this request to allow the agent to access your GitLab data.

## Available tools[¶](#available-tools)

| Tool | Description |
|---|---|
`get_mcp_server_version` |
Returns the current version of the GitLab MCP server |
`create_issue` |
Creates a new issue in a GitLab project |
`get_issue` |
Retrieves detailed information about a specific GitLab issue |
`create_merge_request` |
Creates a merge request in a project |
`get_merge_request` |
Retrieves detailed information about a specific GitLab merge request |
`get_merge_request_commits` |
Retrieves the list of commits in a specific merge request |
`get_merge_request_diffs` |
Retrieves the diffs for a specific merge request |
`get_merge_request_pipelines` |
Retrieves the pipelines for a specific merge request |
`get_pipeline_jobs` |
Retrieves the jobs for a specific CI/CD pipeline |
`gitlab_search` |
Searches for a term across the entire GitLab instance with the search API |
`semantic_code_search` |
Searches for relevant code snippets in a project |

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/qdrant/ -->

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


import { LlmAgent, MCPToolset } from "@google/adk";
const QDRANT_URL = "http://localhost:6333"; // Or your Qdrant Cloud URL
const COLLECTION_NAME = "my_collection";
// const QDRANT_API_KEY = "YOUR_QDRANT_API_KEY";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "qdrant_agent",
instruction: "Help users store and retrieve information using semantic search",
tools: [
new MCPToolset({
type: "StdioConnectionParams",
serverParams: {
command: "uvx",
args: ["mcp-server-qdrant"],
env: {
QDRANT_URL: QDRANT_URL,
COLLECTION_NAME: COLLECTION_NAME,
// QDRANT_API_KEY: QDRANT_API_KEY,
},
},
}),
],
});
export { rootAgent };


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

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/github/ -->

# GitHub¶

# GitHub[¶](#github)

Supported in ADKPython v0.1.0TypeScript v0.2.0

The [GitHub MCP Server](https://github.com/github/github-mcp-server) connects AI
tools directly to GitHub's platform. This gives your ADK agent the ability to
read repositories and code files, manage issues and PRs, analyze code, and
automate workflows using natural language.

## Use cases[¶](#use-cases)

**Repository Management**: Browse and query code, search files, analyze commits, and understand project structure across any repository you have access to.**Issue & PR Automation**: Create, update, and manage issues and pull requests. Let AI help triage bugs, review code changes, and maintain project boards.**Code Analysis**: Examine security findings, review Dependabot alerts, understand code patterns, and get comprehensive insights into your codebase.

## Prerequisites[¶](#prerequisites)

- Create a
[Personal Access Token](https://github.com/settings/personal-access-tokens/new)in GitHub. Refer to the[documentation](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)for more information.

## Use with agent[¶](#use-with-agent)

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StreamableHTTPServerParams
GITHUB_TOKEN = "YOUR_GITHUB_TOKEN"
root_agent = Agent(
model="gemini-2.5-pro",
name="github_agent",
instruction="Help users get information from GitHub",
tools=[
McpToolset(
connection_params=StreamableHTTPServerParams(
url="https://api.githubcopilot.com/mcp/",
headers={
"Authorization": f"Bearer {GITHUB_TOKEN}",
"X-MCP-Toolsets": "all",
"X-MCP-Readonly": "true"
},
),
)
],
)


import { LlmAgent, MCPToolset } from "@google/adk";
const GITHUB_TOKEN = "YOUR_GITHUB_TOKEN";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "github_agent",
instruction: "Help users get information from GitHub",
tools: [
new MCPToolset({
type: "StreamableHTTPConnectionParams",
url: "https://api.githubcopilot.com/mcp/",
header: {
Authorization: `Bearer ${GITHUB_TOKEN}`,
"X-MCP-Toolsets": "all",
"X-MCP-Readonly": "true",
},
}),
],
});
export { rootAgent };


## Available tools[¶](#available-tools)

| Tool | Description |
|---|---|
`context` |
Tools that provide context about the current user and GitHub context you are operating in |
`copilot` |
Copilot related tools (e.g. Copilot Coding Agent) |
`copilot_spaces` |
Copilot Spaces related tools |
`actions` |
GitHub Actions workflows and CI/CD operations |
`code_security` |
Code security related tools, such as GitHub Code Scanning |
`dependabot` |
Dependabot tools |
`discussions` |
GitHub Discussions related tools |
`experiments` |
Experimental features that are not considered stable yet |
`gists` |
GitHub Gist related tools |
`github_support_docs_search` |
Search docs to answer GitHub product and support questions |
`issues` |
GitHub Issues related tools |
`labels` |
GitHub Labels related tools |
`notifications` |
GitHub Notifications related tools |
`orgs` |
GitHub Organization related tools |
`projects` |
GitHub Projects related tools |
`pull_requests` |
GitHub Pull Request related tools |
`repos` |
GitHub Repository related tools |
`secret_protection` |
Secret protection related tools, such as GitHub Secret Scanning |
`security_advisories` |
Security advisories related tools |
`stargazers` |
GitHub Stargazers related tools |
`users` |
GitHub User related tools |

## Configuration[¶](#configuration)

The Remote GitHub MCP server has optional headers that can be used to configure available toolsets and read-only mode:

-
`X-MCP-Toolsets`

: Comma-separated list of toolsets to enable. (e.g., "repos,issues")- If the list is empty, default toolsets will be used. If a bad toolset is provided, the server will fail to start and emit a 400 bad request status. Whitespace is ignored.

-
`X-MCP-Readonly`

: Enables only "read" tools.- If this header is empty, "false", "f", "no", "n", "0", or "off" (ignoring whitespace and case), it will be interpreted as false. All other values are interpreted as true.

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/atlassian/ -->

# Atlassian¶

# Atlassian[¶](#atlassian)

The [Atlassian MCP Server](https://github.com/atlassian/atlassian-mcp-server)
connects your ADK agent to the [Atlassian](https://www.atlassian.com/)
ecosystem, bridging the gap between project tracking in Jira and knowledge
management in Confluence. This integration gives your agent the ability to
manage issues, search and update documentation pages, and streamline
collaboration workflows using natural language.

## Use cases[¶](#use-cases)

-
**Unified Knowledge Search**: Search across both Jira issues and Confluence pages simultaneously to find project specs, decisions, or historical context. -
**Automate Issue Management**: Create, edit, and transition Jira issues, or add comments to existing tickets. -
**Documentation Assistant**: Retrieve page content, generate drafts, or add inline comments to Confluence documents directly from your agent.

## Prerequisites[¶](#prerequisites)

- Sign up for an
[Atlassian account](https://id.atlassian.com/signup) - An Atlassian Cloud site with Jira and/or Confluence

## Use with agent[¶](#use-with-agent)

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
root_agent = Agent(
model="gemini-2.5-pro",
name="atlassian_agent",
instruction="Help users work with data in Atlassian products",
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params=StdioServerParameters(
command="npx",
args=[
"-y",
"mcp-remote",
"https://mcp.atlassian.com/v1/mcp",
]
),
timeout=30,
),
)
],
)


import { LlmAgent, MCPToolset } from "@google/adk";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "atlassian_agent",
instruction: "Help users work with data in Atlassian products",
tools: [
new MCPToolset({
type: "StdioConnectionParams",
serverParams: {
command: "npx",
args: [
"-y",
"mcp-remote",
"https://mcp.atlassian.com/v1/mcp",
],
},
}),
],
});
export { rootAgent };


Note

When you run this agent for the first time, a browser window opens automatically to request access via OAuth. Alternatively, you can use the authorization URL printed in the console. You must approve this request to allow the agent to access your Atlassian data.

## Available tools[¶](#available-tools)

| Tool | Description |
|---|---|
`atlassianUserInfo` |
Get information about the user |
`getAccessibleAtlassianResources` |
Get information about accessible Atlassian resources |
`getJiraIssue` |
Get information about a Jira issue |
`editJiraIssue` |
Edit a Jira issue |
`createJiraIssue` |
Create a new Jira issue |
`getTransitionsForJiraIssue` |
Get transitions for a Jira issue |
`transitionJiraIssue` |
Transition a Jira issue |
`lookupJiraAccountId` |
Lookup a Jira account ID |
`searchJiraIssuesUsingJql` |
Search Jira issues using JQL |
`addCommentToJiraIssue` |
Add a comment to a Jira issue |
`getJiraIssueRemoteIssueLinks` |
Get remote issue links for a Jira issue |
`getVisibleJiraProjects` |
Get visible Jira projects |
`getJiraProjectIssueTypesMetadata` |
Get issue types metadata for a Jira project |
`getJiraIssueTypeMetaWithFields` |
Get issue type metadata with fields for a Jira issue |
`getConfluenceSpaces` |
Get information about Confluence spaces |
`getConfluencePage` |
Get information about a Confluence page |
`getPagesInConfluenceSpace` |
Get information about pages in a Confluence space |
`getConfluencePageFooterComments` |
Get information about footer comments in a Confluence page |
`getConfluencePageInlineComments` |
Get information about inline comments in a Confluence page |
`getConfluencePageDescendants` |
Get information about descendants of a Confluence page |
`createConfluencePage` |
Create a new Confluence page |
`updateConfluencePage` |
Update an existing Confluence page |
`createConfluenceFooterComment` |
Create a footer comment in a Confluence page |
`createConfluenceInlineComment` |
Create an inline comment in a Confluence page |
`searchConfluenceUsingCql` |
Search Confluence using CQL |
`search` |
Search for information |
`fetch` |
Fetch information |

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/postman/ -->

# Postman¶

# Postman[¶](#postman)

The [Postman MCP Server](https://github.com/postmanlabs/postman-mcp-server)
connects your ADK agent to the [Postman](https://www.postman.com/) ecosystem.
This integration gives your agent the ability to access workspaces, manage
collections and environments, evaluate APIs, and automate workflows through
natural language interactions.

## Use cases[¶](#use-cases)

-
**API testing**: Continuously test your APIs using your Postman collections. -
**Collection management**: Create and tag collections, update documentation, add comments, or perform actions across multiple collections without leaving your editor. -
**Workspace and environment management**: Create workspaces and environments, and manage your environment variables. -
**Client code generation**: Generate production-ready client code that consumes APIs following best practices and project conventions.

## Prerequisites[¶](#prerequisites)

- Create a
[Postman account](https://identity.getpostman.com/signup) - Generate a
[Postman API key](https://postman.postman.co/settings/me/api-keys)

## Use with agent[¶](#use-with-agent)

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
POSTMAN_API_KEY = "YOUR_POSTMAN_API_KEY"
root_agent = Agent(
model="gemini-2.5-pro",
name="postman_agent",
instruction="Help users manage their Postman workspaces and collections",
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params=StdioServerParameters(
command="npx",
args=[
"-y",
"@postman/postman-mcp-server",
# "--full", # Use all 100+ tools
# "--code", # Use code generation tools
# "--region", "eu", # Use EU region
],
env={
"POSTMAN_API_KEY": POSTMAN_API_KEY,
},
),
timeout=30,
),
)
],
)


from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StreamableHTTPServerParams
POSTMAN_API_KEY = "YOUR_POSTMAN_API_KEY"
root_agent = Agent(
model="gemini-2.5-pro",
name="postman_agent",
instruction="Help users manage their Postman workspaces and collections",
tools=[
McpToolset(
connection_params=StreamableHTTPServerParams(
url="https://mcp.postman.com/mcp",
# (Optional) Use "/minimal" for essential tools only
# (Optional) Use "/code" for code generation tools
# (Optional) Use "https://mcp.eu.postman.com" for EU region
headers={
"Authorization": f"Bearer {POSTMAN_API_KEY}",
},
),
)
],
)


import { LlmAgent, MCPToolset } from "@google/adk";
const POSTMAN_API_KEY = "YOUR_POSTMAN_API_KEY";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "postman_agent",
instruction: "Help users manage their Postman workspaces and collections",
tools: [
new MCPToolset({
type: "StdioConnectionParams",
serverParams: {
command: "npx",
args: [
"-y",
"@postman/postman-mcp-server",
// "--full", // Use all 100+ tools
// "--code", // Use code generation tools
// "--region", "eu", // Use EU region
],
env: {
POSTMAN_API_KEY: POSTMAN_API_KEY,
},
},
}),
],
});
export { rootAgent };


import { LlmAgent, MCPToolset } from "@google/adk";
const POSTMAN_API_KEY = "YOUR_POSTMAN_API_KEY";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "postman_agent",
instruction: "Help users manage their Postman workspaces and collections",
tools: [
new MCPToolset({
type: "StreamableHTTPConnectionParams",
url: "https://mcp.postman.com/mcp",
// (Optional) Use "/minimal" for essential tools only
// (Optional) Use "/code" for code generation tools
// (Optional) Use "https://mcp.eu.postman.com" for EU region
header: {
Authorization: `Bearer ${POSTMAN_API_KEY}`,
},
}),
],
});
export { rootAgent };


## Configuration[¶](#configuration)

Postman offers three tool configurations:

**Minimal**(default): Essential tools for basic Postman operations. Best for simple modifications to collections, workspaces, or environments.**Full**: All available Postman API tools (100+ tools). Ideal for advanced collaboration and enterprise features.**Code**: Tools for searching API definitions and generating client code. Perfect for developers who need to consume APIs.

To select a configuration:

**Local server**: Add`--full`

or`--code`

to the`args`

list.**Remote server**: Change the URL path to`/minimal`

,`/mcp`

(full), or`/code`

.

For EU region, use `--region eu`

(local) or `https://mcp.eu.postman.com`

(remote).

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/n8n/ -->

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


import { LlmAgent, MCPToolset } from "@google/adk";
const N8N_INSTANCE_URL = "https://localhost:5678";
const N8N_MCP_TOKEN = "YOUR_N8N_MCP_TOKEN";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "n8n_agent",
instruction: "Help users manage and execute workflows in n8n",
tools: [
new MCPToolset({
type: "StdioConnectionParams",
serverParams: {
command: "npx",
args: [
"-y",
"supergateway",
"--streamableHttp",
`${N8N_INSTANCE_URL}/mcp-server/http`,
"--header",
`authorization:Bearer ${N8N_MCP_TOKEN}`,
],
},
}),
],
});
export { rootAgent };


import { LlmAgent, MCPToolset } from "@google/adk";
const N8N_INSTANCE_URL = "https://localhost:5678";
const N8N_MCP_TOKEN = "YOUR_N8N_MCP_TOKEN";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "n8n_agent",
instruction: "Help users manage and execute workflows in n8n",
tools: [
new MCPToolset({
type: "StreamableHTTPConnectionParams",
url: `${N8N_INSTANCE_URL}/mcp-server/http`,
header: {
Authorization: `Bearer ${N8N_MCP_TOKEN}`,
},
}),
],
});
export { rootAgent };


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

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/stripe/ -->

# Stripe¶

# Stripe[¶](#stripe)

The [Stripe MCP Server](https://docs.stripe.com/mcp) connects your ADK agent to
the [Stripe](https://stripe.com/) ecosystem. This integration gives your agent
the ability to manage payments, customers, subscriptions, and invoices using
natural language, enabling automated commerce workflows and financial
operations.

## Use cases[¶](#use-cases)

-
**Automate Payment Operations**: Create payment links, process refunds, and list payment intents through conversational commands. -
**Streamline Invoicing**: Generate and finalize invoices, add line items, and track outstanding payments without leaving your development environment. -
**Access Business Insights**: Query account balances, list products and prices, and search across Stripe resources to make data-driven decisions.

## Prerequisites[¶](#prerequisites)

- Create a
[Stripe account](https://dashboard.stripe.com/register) - Generate a
[Restricted API key](https://dashboard.stripe.com/apikeys)from the Stripe Dashboard

## Use with agent[¶](#use-with-agent)

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
STRIPE_SECRET_KEY = "YOUR_STRIPE_SECRET_KEY"
root_agent = Agent(
model="gemini-2.5-pro",
name="stripe_agent",
instruction="Help users manage their Stripe account",
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params=StdioServerParameters(
command="npx",
args=[
"-y",
"@stripe/mcp",
"--tools=all",
# (Optional) Specify which tools to enable
# "--tools=customers.read,invoices.read,products.read",
],
env={
"STRIPE_SECRET_KEY": STRIPE_SECRET_KEY,
}
),
timeout=30,
),
)
],
)


from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StreamableHTTPServerParams
STRIPE_SECRET_KEY = "YOUR_STRIPE_SECRET_KEY"
root_agent = Agent(
model="gemini-2.5-pro",
name="stripe_agent",
instruction="Help users manage their Stripe account",
tools=[
McpToolset(
connection_params=StreamableHTTPServerParams(
url="https://mcp.stripe.com",
headers={
"Authorization": f"Bearer {STRIPE_SECRET_KEY}",
},
),
)
],
)


import { LlmAgent, MCPToolset } from "@google/adk";
const STRIPE_SECRET_KEY = "YOUR_STRIPE_SECRET_KEY";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "stripe_agent",
instruction: "Help users manage their Stripe account",
tools: [
new MCPToolset({
type: "StdioConnectionParams",
serverParams: {
command: "npx",
args: [
"-y",
"@stripe/mcp",
"--tools=all",
// (Optional) Specify which tools to enable
// "--tools=customers.read,invoices.read,products.read",
],
env: {
STRIPE_SECRET_KEY: STRIPE_SECRET_KEY,
},
},
}),
],
});
export { rootAgent };


import { LlmAgent, MCPToolset } from "@google/adk";
const STRIPE_SECRET_KEY = "YOUR_STRIPE_SECRET_KEY";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "stripe_agent",
instruction: "Help users manage their Stripe account",
tools: [
new MCPToolset({
type: "StreamableHTTPConnectionParams",
url: "https://mcp.stripe.com",
header: {
Authorization: `Bearer ${STRIPE_SECRET_KEY}`,
},
}),
],
});
export { rootAgent };


Best practices

Enable human confirmation of tool actions and exercise caution when using the Stripe MCP server alongside other MCP servers to mitigate prompt injection risks.

## Available tools[¶](#available-tools)

| Resource | Tool | API |
|---|---|---|
| Account | `get_stripe_account_info` |
Retrieve account |
| Balance | `retrieve_balance` |
Retrieve balance |
| Coupon | `create_coupon` |
Create coupon |
| Coupon | `list_coupons` |
List coupons |
| Customer | `create_customer` |
Create customer |
| Customer | `list_customers` |
List customers |
| Dispute | `list_disputes` |
List disputes |
| Dispute | `update_dispute` |
Update dispute |
| Invoice | `create_invoice` |
Create invoice |
| Invoice | `create_invoice_item` |
Create invoice item |
| Invoice | `finalize_invoice` |
Finalize invoice |
| Invoice | `list_invoices` |
List invoices |
| Payment Link | `create_payment_link` |
Create payment link |
| PaymentIntent | `list_payment_intents` |
List PaymentIntents |
| Price | `create_price` |
Create price |
| Price | `list_prices` |
List prices |
| Product | `create_product` |
Create product |
| Product | `list_products` |
List products |
| Refund | `create_refund` |
Create refund |
| Subscription | `cancel_subscription` |
Cancel subscription |
| Subscription | `list_subscriptions` |
List subscriptions |
| Subscription | `update_subscription` |
Update subscription |
| Others | `search_stripe_resources` |
Search Stripe resources |
| Others | `fetch_stripe_resources` |
Fetch Stripe object |
| Others | `search_stripe_documentation` |
Search Stripe knowledge |

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/hugging-face/ -->

# Hugging Face¶

# Hugging Face[¶](#hugging-face)

Supported in ADKPython v0.1.0TypeScript v0.2.0

The [Hugging Face MCP Server](https://github.com/huggingface/hf-mcp-server) can be used to connect
your ADK agent to the Hugging Face Hub and thousands of Gradio AI Applications.

## Use cases[¶](#use-cases)

**Discover AI/ML Assets**: Search and filter the Hub for models, datasets, and papers based on tasks, libraries, or keywords.**Build Multi-Step Workflows**: Chain tools together, such as transcribing audio with one tool and then summarizing the resulting text with another.**Find AI Applications**: Search for Gradio Spaces that can perform a specific task, like background removal or text-to-speech.

## Prerequisites[¶](#prerequisites)

- Create a
[user access token](https://huggingface.co/settings/tokens)in Hugging Face. Refer to the[documentation](https://huggingface.co/docs/hub/en/security-tokens)for more information.

## Use with agent[¶](#use-with-agent)

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
HUGGING_FACE_TOKEN = "YOUR_HUGGING_FACE_TOKEN"
root_agent = Agent(
model="gemini-2.5-pro",
name="hugging_face_agent",
instruction="Help users get information from Hugging Face",
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params = StdioServerParameters(
command="npx",
args=[
"-y",
"@llmindset/hf-mcp-server",
],
env={
"HF_TOKEN": HUGGING_FACE_TOKEN,
}
),
timeout=30,
),
)
],
)


from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StreamableHTTPServerParams
HUGGING_FACE_TOKEN = "YOUR_HUGGING_FACE_TOKEN"
root_agent = Agent(
model="gemini-2.5-pro",
name="hugging_face_agent",
instruction="Help users get information from Hugging Face",
tools=[
McpToolset(
connection_params=StreamableHTTPServerParams(
url="https://huggingface.co/mcp",
headers={
"Authorization": f"Bearer {HUGGING_FACE_TOKEN}",
},
),
)
],
)


import { LlmAgent, MCPToolset } from "@google/adk";
const HUGGING_FACE_TOKEN = "YOUR_HUGGING_FACE_TOKEN";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "hugging_face_agent",
instruction: "Help users get information from Hugging Face",
tools: [
new MCPToolset({
type: "StdioConnectionParams",
serverParams: {
command: "npx",
args: ["-y", "@llmindset/hf-mcp-server"],
env: {
HF_TOKEN: HUGGING_FACE_TOKEN,
},
},
}),
],
});
export { rootAgent };


import { LlmAgent, MCPToolset } from "@google/adk";
const HUGGING_FACE_TOKEN = "YOUR_HUGGING_FACE_TOKEN";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "hugging_face_agent",
instruction: "Help users get information from Hugging Face",
tools: [
new MCPToolset({
type: "StreamableHTTPConnectionParams",
url: "https://huggingface.co/mcp",
header: {
Authorization: `Bearer ${HUGGING_FACE_TOKEN}`,
},
}),
],
});
export { rootAgent };


## Available tools[¶](#available-tools)

| Tool | Description |
|---|---|
| Spaces Semantic Search | Find the best AI Apps via natural language queries |
| Papers Semantic Search | Find ML Research Papers via natural language queries |
| Model Search | Search for ML models with filters for task, library, etc… |
| Dataset Search | Search for datasets with filters for author, tags, etc… |
| Documentation Semantic Search | Search the Hugging Face documentation library |
| Hub Repository Details | Get detailed information about Models, Datasets and Spaces |

## Configuration[¶](#configuration)

To configure which tools are available in your Hugging Face Hub MCP server,
visit the [MCP Settings Page](https://huggingface.co/settings/mcp) in your
Hugging Face account.

To configure the local MCP server, you can use the following environment variables:

`TRANSPORT`

: The transport type to use (`stdio`

,`sse`

,`streamableHttp`

, or`streamableHttpJson`

)`DEFAULT_HF_TOKEN`

: ⚠️ Requests are serviced with the`HF_TOKEN`

received in the Authorization: Bearer header. The DEFAULT_HF_TOKEN is used if no header was sent. Only set this in Development / Test environments or for local STDIO Deployments. ⚠️- If running with stdio transport,
`HF_TOKEN`

is used if`DEFAULT_HF_TOKEN`

is not set. `HF_API_TIMEOUT`

: Timeout for Hugging Face API requests in milliseconds (default: 12500ms / 12.5 seconds)`USER_CONFIG_API`

: URL to use for User settings (defaults to Local front-end)`MCP_STRICT_COMPLIANCE`

: set to True for GET 405 rejects in JSON Mode (default serves a welcome page).`AUTHENTICATE_TOOL`

: whether to include an Authenticate tool to issue an OAuth challenge when called`SEARCH_ENABLES_FETCH`

: When set to true, automatically enables the hf_doc_fetch tool whenever hf_doc_search is enabled

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/linear/ -->

# Linear¶

# Linear[¶](#linear)

The [Linear MCP Server](https://linear.app/docs/mcp) connects your ADK agent to
[Linear](https://linear.app/), a purpose-built tool for planning and building
products. This integration gives your agent the ability to manage issues, track
project cycles, and automate development workflows using natural language.

## Use cases[¶](#use-cases)

-
**Streamline Issue Management**: Create, update, and organize issues using natural language. Let your agent handle logging bugs, assigning tasks, and updating statuses. -
**Track Projects and Cycles**: Get instant visibility into your team's momentum. Query the status of active cycles, check project milestones, and retrieve deadlines. -
**Contextual Search & Summarization**: Quickly catch up on long discussion threads or find specific project specifications. Your agent can search documentation and summarize complex issues.

## Prerequisites[¶](#prerequisites)

[Sign up](https://linear.app/signup)for a Linear account- Generate an API key in
[Linear Settings > Security & access](https://linear.app/docs/security-and-access)(if using API authentication)

## Use with agent[¶](#use-with-agent)

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
root_agent = Agent(
model="gemini-2.5-pro",
name="linear_agent",
instruction="Help users manage issues, projects, and cycles in Linear",
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params=StdioServerParameters(
command="npx",
args=[
"-y",
"mcp-remote",
"https://mcp.linear.app/mcp",
]
),
timeout=30,
),
)
],
)


Note

When you run this agent for the first time, a browser window will open automatically to request access via OAuth. Alternatively, you can use the authorization URL printed in the console. You must approve this request to allow the agent to access your Linear data.

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StreamableHTTPServerParams
LINEAR_API_KEY = "YOUR_LINEAR_API_KEY"
root_agent = Agent(
model="gemini-2.5-pro",
name="linear_agent",
instruction="Help users manage issues, projects, and cycles in Linear",
tools=[
McpToolset(
connection_params=StreamableHTTPServerParams(
url="https://mcp.linear.app/mcp",
headers={
"Authorization": f"Bearer {LINEAR_API_KEY}",
},
),
)
],
)


Note

This code example uses an API key for authentication. To use a
browser-based OAuth authentication flow instead, remove the `headers`

parameter and run the agent.

import { LlmAgent, MCPToolset } from "@google/adk";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "linear_agent",
instruction: "Help users manage issues, projects, and cycles in Linear",
tools: [
new MCPToolset({
type: "StdioConnectionParams",
serverParams: {
command: "npx",
args: ["-y", "mcp-remote", "https://mcp.linear.app/mcp"],
},
}),
],
});
export { rootAgent };


Note

When you run this agent for the first time, a browser window will open automatically to request access via OAuth. Alternatively, you can use the authorization URL printed in the console. You must approve this request to allow the agent to access your Linear data.

import { LlmAgent, MCPToolset } from "@google/adk";
const LINEAR_API_KEY = "YOUR_LINEAR_API_KEY";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "linear_agent",
instruction: "Help users manage issues, projects, and cycles in Linear",
tools: [
new MCPToolset({
type: "StreamableHTTPConnectionParams",
url: "https://mcp.linear.app/mcp",
header: {
Authorization: `Bearer ${LINEAR_API_KEY}`,
},
}),
],
});
export { rootAgent };


Note

This code example uses an API key for authentication. To use a
browser-based OAuth authentication flow instead, remove the `header`

property and run the agent.

## Available tools[¶](#available-tools)

| Tool | Description |
|---|---|
`list_comments` |
List comments on an issue |
`create_comment` |
Create a comment on an issue |
`list_cycles` |
List cycles in a project |
`get_document` |
Get a document |
`list_documents` |
List documents |
`get_issue` |
Get an issue |
`list_issues` |
List issues |
`create_issue` |
Create an issue |
`update_issue` |
Update an issue |
`list_issue_statuses` |
List issue statuses |
`get_issue_status` |
Get an issue status |
`list_issue_labels` |
List issue labels |
`create_issue_label` |
Create an issue label |
`list_projects` |
List projects |
`get_project` |
Get a project |
`create_project` |
Create a project |
`update_project` |
Update a project |
`list_project_labels` |
List project labels |
`list_teams` |
List teams |
`get_team` |
Get a team |
`list_users` |
List users |
`get_user` |
Get a user |
`search_documentation` |
Search documentation |

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/elevenlabs/ -->

# ElevenLabs¶

# ElevenLabs[¶](#elevenlabs)

The [ElevenLabs MCP Server](https://github.com/elevenlabs/elevenlabs-mcp)
connects your ADK agent to the [ElevenLabs](https://elevenlabs.io/) AI audio
platform. This integration gives your agent the ability to generate speech,
clone voices, transcribe audio, create sound effects, and build conversational
AI experiences using natural language.

## Use cases[¶](#use-cases)

-
**Text-to-Speech Generation**: Convert text into natural-sounding speech using a variety of voices, with fine-grained control over stability, style, and similarity settings. -
**Voice Cloning & Design**: Clone voices from audio samples or generate new voices from text descriptions of desired characteristics like age, gender, accent, and tone. -
**Audio Processing**: Isolate speech from background noise, convert audio to sound like different voices, or transcribe speech to text with speaker identification. -
**Sound Effects & Soundscapes**: Generate sound effects and ambient soundscapes from text descriptions, such as "a thunderstorm in a dense jungle with animals reacting to the weather."

## Prerequisites[¶](#prerequisites)

- Sign up for an
[ElevenLabs account](https://elevenlabs.io/app/sign-up) - Generate an
[API key](https://elevenlabs.io/app/settings/api-keys)from your account settings

## Use with agent[¶](#use-with-agent)

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
ELEVENLABS_API_KEY = "YOUR_ELEVENLABS_API_KEY"
root_agent = Agent(
model="gemini-2.5-pro",
name="elevenlabs_agent",
instruction="Help users generate speech, clone voices, and process audio",
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params=StdioServerParameters(
command="uvx",
args=["elevenlabs-mcp"],
env={
"ELEVENLABS_API_KEY": ELEVENLABS_API_KEY,
}
),
timeout=30,
),
)
],
)


import { LlmAgent, MCPToolset } from "@google/adk";
const ELEVENLABS_API_KEY = "YOUR_ELEVENLABS_API_KEY";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "elevenlabs_agent",
instruction: "Help users generate speech, clone voices, and process audio",
tools: [
new MCPToolset({
type: "StdioConnectionParams",
serverParams: {
command: "uvx",
args: ["elevenlabs-mcp"],
env: {
ELEVENLABS_API_KEY: ELEVENLABS_API_KEY,
},
},
}),
],
});
export { rootAgent };


## Available tools[¶](#available-tools)

### Text-to-speech and voice[¶](#text-to-speech-and-voice)

| Tool | Description |
|---|---|
`text_to_speech` |
Generate speech from text using a specified voice |
`speech_to_speech` |
Transform audio to sound like a different voice |
`text_to_voice` |
Generate a voice preview from text description |
`create_voice_from_preview` |
Save a generated voice preview to your library |
`voice_clone` |
Clone a voice from audio samples |
`get_voice` |
Get details about a specific voice |
`search_voices` |
Search for voices in your library |
`search_voice_library` |
Search the public voice library |
`list_models` |
List available text-to-speech models |

### Audio processing[¶](#audio-processing)

| Tool | Description |
|---|---|
`speech_to_text` |
Transcribe audio to text with speaker identification |
`text_to_sound_effects` |
Generate sound effects from text descriptions |
`isolate_audio` |
Separate speech from background noise and music |
`play_audio` |
Play an audio file locally |
`compose_music` |
Generate music from a description |
`create_composition_plan` |
Create a plan for music composition |

### Conversational AI[¶](#conversational-ai)

| Tool | Description |
|---|---|
`create_agent` |
Create a conversational AI agent |
`get_agent` |
Get details about a specific agent |
`list_agents` |
List all your conversational AI agents |
`add_knowledge_base_to_agent` |
Add a knowledge base to an agent |
`make_outbound_call` |
Initiate an outbound phone call using an agent |
`list_phone_numbers` |
List available phone numbers |
`get_conversation` |
Get details about a specific conversation |
`list_conversations` |
List all conversations |

### Account[¶](#account)

| Tool | Description |
|---|---|
`check_subscription` |
Check your subscription and credit usage |

## Configuration[¶](#configuration)

The ElevenLabs MCP server can be configured using environment variables:

| Variable | Description | Default |
|---|---|---|
`ELEVENLABS_API_KEY` |
Your ElevenLabs API key | Required |
`ELEVENLABS_MCP_BASE_PATH` |
Base path for file operations | `~/Desktop` |
`ELEVENLABS_MCP_OUTPUT_MODE` |
How generated files are returned | `files` |
`ELEVENLABS_API_RESIDENCY` |
Data residency region (enterprise only) | `us` |

### Output modes[¶](#output-modes)

The `ELEVENLABS_MCP_OUTPUT_MODE`

environment variable supports three modes:

(default): Save files to disk and return file paths`files`

: Return files as MCP resources (base64-encoded binary data)`resources`

: Save files to disk AND return as MCP resources`both`

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/chroma/ -->

# Chroma¶

# Chroma[¶](#chroma)

The [Chroma MCP Server](https://github.com/chroma-core/chroma-mcp) connects your
ADK agent to [Chroma](https://www.trychroma.com/), an open-source embedding
database. This integration gives your agent the ability to create collections,
store documents, and retrieve information using semantic search, full text
search, and metadata filtering.

## Use cases[¶](#use-cases)

-
**Semantic Memory for Agents**: Store conversation context, facts, or learned information that agents can retrieve later using natural language queries. -
**Knowledge Base Retrieval**: Build a retrieval-augmented generation (RAG) system by storing documents and retrieving relevant context for responses. -
**Persistent Context Across Sessions**: Maintain long-term memory across conversations, allowing agents to reference past interactions and accumulated knowledge.

## Prerequisites[¶](#prerequisites)

**For local storage**: A directory path to persist data**For Chroma Cloud**: A[Chroma Cloud](https://www.trychroma.com/)account with tenant ID, database name, and API key

## Use with agent[¶](#use-with-agent)

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
# For local storage, use:
DATA_DIR = "/path/to/your/data/directory"
# For Chroma Cloud, use:
# CHROMA_TENANT = "your-tenant-id"
# CHROMA_DATABASE = "your-database-name"
# CHROMA_API_KEY = "your-api-key"
root_agent = Agent(
model="gemini-2.5-pro",
name="chroma_agent",
instruction="Help users store and retrieve information using semantic search",
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params=StdioServerParameters(
command="uvx",
args=[
"chroma-mcp",
# For local storage, use:
"--client-type",
"persistent",
"--data-dir",
DATA_DIR,
# For Chroma Cloud, use:
# "--client-type",
# "cloud",
# "--tenant",
# CHROMA_TENANT,
# "--database",
# CHROMA_DATABASE,
# "--api-key",
# CHROMA_API_KEY,
],
),
timeout=30,
),
)
],
)


import { LlmAgent, MCPToolset } from "@google/adk";
// For local storage, use:
const DATA_DIR = "/path/to/your/data/directory";
// For Chroma Cloud, use:
// const CHROMA_TENANT = "your-tenant-id";
// const CHROMA_DATABASE = "your-database-name";
// const CHROMA_API_KEY = "your-api-key";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "chroma_agent",
instruction: "Help users store and retrieve information using semantic search",
tools: [
new MCPToolset({
type: "StdioConnectionParams",
serverParams: {
command: "uvx",
args: [
"chroma-mcp",
// For local storage, use:
"--client-type",
"persistent",
"--data-dir",
DATA_DIR,
// For Chroma Cloud, use:
// "--client-type",
// "cloud",
// "--tenant",
// CHROMA_TENANT,
// "--database",
// CHROMA_DATABASE,
// "--api-key",
// CHROMA_API_KEY,
],
},
}),
],
});
export { rootAgent };


## Available tools[¶](#available-tools)

### Collection management[¶](#collection-management)

| Tool | Description |
|---|---|
`chroma_list_collections` |
List all collections with pagination support |
`chroma_create_collection` |
Create a new collection with optional HNSW configuration |
`chroma_get_collection_info` |
Get detailed information about a collection |
`chroma_get_collection_count` |
Get the number of documents in a collection |
`chroma_modify_collection` |
Update a collection's name or metadata |
`chroma_delete_collection` |
Delete a collection |
`chroma_peek_collection` |
View a sample of documents in a collection |

### Document operations[¶](#document-operations)

| Tool | Description |
|---|---|
`chroma_add_documents` |
Add documents with optional metadata and custom IDs |
`chroma_query_documents` |
Query documents using semantic search with advanced filtering |
`chroma_get_documents` |
Retrieve documents by IDs or filters with pagination |
`chroma_update_documents` |
Update existing documents' content, metadata, or embeddings |
`chroma_delete_documents` |
Delete specific documents from a collection |

## Configuration[¶](#configuration)

The Chroma MCP server supports multiple client types to suit different needs:

### Client types[¶](#client-types)

| Client Type | Description | Key Arguments |
|---|---|---|
`ephemeral` |
In-memory storage, cleared on restart. Useful for testing. | None (default) |
`persistent` |
File-based storage on your local machine | `--data-dir` |
`http` |
Connect to a self-hosted Chroma server | `--host` , `--port` , `--ssl` , `--custom-auth-credentials` |
`cloud` |
Connect to Chroma Cloud (api.trychroma.com) | `--tenant` , `--database` , `--api-key` |

### Environment variables[¶](#environment-variables)

You can also configure the client using environment variables. Command-line arguments take precedence over environment variables.

| Variable | Description |
|---|---|
`CHROMA_CLIENT_TYPE` |
Client type: `ephemeral` , `persistent` , `http` , or `cloud` |
`CHROMA_DATA_DIR` |
Path for persistent local storage |
`CHROMA_TENANT` |
Tenant ID for Chroma Cloud |
`CHROMA_DATABASE` |
Database name for Chroma Cloud |
`CHROMA_API_KEY` |
API key for Chroma Cloud |
`CHROMA_HOST` |
Host for self-hosted HTTP client |
`CHROMA_PORT` |
Port for self-hosted HTTP client |
`CHROMA_SSL` |
Enable SSL for HTTP client (`true` or `false` ) |
`CHROMA_DOTENV_PATH` |
Path to `.env` file (defaults to `.chroma_env` ) |

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/mongodb/ -->

# MongoDB¶

# MongoDB[¶](#mongodb)

The [MongoDB MCP Server](https://github.com/mongodb-js/mongodb-mcp-server)
connects your ADK agent to [MongoDB](https://www.mongodb.com/) databases and
MongoDB Atlas clusters. This integration gives your agent the ability to query
collections, manage databases, and interact with MongoDB Atlas infrastructure
using natural language.

## Use cases[¶](#use-cases)

-
**Data Exploration and Analysis**: Query MongoDB collections using natural language, run aggregations, and analyze document schemas without writing complex queries manually. -
**Database Administration**: List databases and collections, create indexes, manage users, and monitor database statistics through conversational commands. -
**Atlas Infrastructure Management**: Create and manage MongoDB Atlas clusters, configure access lists, and view performance recommendations directly from your agent.

## Prerequisites[¶](#prerequisites)

**For database access**: A MongoDB connection string (local, self-hosted, or Atlas cluster)**For Atlas management**: A[MongoDB Atlas](https://www.mongodb.com/atlas)service account with API credentials (client ID and secret)

## Use with agent[¶](#use-with-agent)

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
# For database access, use a connection string:
CONNECTION_STRING = "mongodb://localhost:27017/myDatabase"
# For Atlas management, use API credentials:
# ATLAS_CLIENT_ID = "YOUR_ATLAS_CLIENT_ID"
# ATLAS_CLIENT_SECRET = "YOUR_ATLAS_CLIENT_SECRET"
root_agent = Agent(
model="gemini-2.5-pro",
name="mongodb_agent",
instruction="Help users query and manage MongoDB databases",
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params=StdioServerParameters(
command="npx",
args=[
"-y",
"mongodb-mcp-server",
"--readOnly", # Remove for write operations
],
env={
# For database access, use:
"MDB_MCP_CONNECTION_STRING": CONNECTION_STRING,
# For Atlas management, use:
# "MDB_MCP_API_CLIENT_ID": ATLAS_CLIENT_ID,
# "MDB_MCP_API_CLIENT_SECRET": ATLAS_CLIENT_SECRET,
},
),
timeout=30,
),
)
],
)


import { LlmAgent, MCPToolset } from "@google/adk";
// For database access, use a connection string:
const CONNECTION_STRING = "mongodb://localhost:27017/myDatabase";
// For Atlas management, use API credentials:
// const ATLAS_CLIENT_ID = "YOUR_ATLAS_CLIENT_ID";
// const ATLAS_CLIENT_SECRET = "YOUR_ATLAS_CLIENT_SECRET";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "mongodb_agent",
instruction: "Help users query and manage MongoDB databases",
tools: [
new MCPToolset({
type: "StdioConnectionParams",
serverParams: {
command: "npx",
args: [
"-y",
"mongodb-mcp-server",
"--readOnly", // Remove for write operations
],
env: {
// For database access, use:
MDB_MCP_CONNECTION_STRING: CONNECTION_STRING,
// For Atlas management, use:
// MDB_MCP_API_CLIENT_ID: ATLAS_CLIENT_ID,
// MDB_MCP_API_CLIENT_SECRET: ATLAS_CLIENT_SECRET,
},
},
}),
],
});
export { rootAgent };


## Available tools[¶](#available-tools)

### MongoDB database tools[¶](#mongodb-database-tools)

| Tool | Description |
|---|---|
`find` |
Run a find query against a MongoDB collection |
`aggregate` |
Run an aggregation against a MongoDB collection |
`count` |
Get the number of documents in a collection |
`list-databases` |
List all databases for a MongoDB connection |
`list-collections` |
List all collections for a given database |
`collection-schema` |
Describe the schema for a collection |
`collection-indexes` |
Describe the indexes for a collection |
`insert-many` |
Insert documents into a collection |
`update-many` |
Update documents matching a filter |
`delete-many` |
Remove documents matching a filter |
`create-collection` |
Create a new collection |
`drop-collection` |
Remove a collection from the database |
`drop-database` |
Remove a database |
`create-index` |
Create an index for a collection |
`drop-index` |
Drop an index from a collection |
`rename-collection` |
Rename a collection |
`db-stats` |
Get statistics for a database |
`explain` |
Get query execution statistics |
`export` |
Export query results in EJSON format |

### MongoDB Atlas tools[¶](#mongodb-atlas-tools)

Note

Atlas tools require API credentials. Set `MDB_MCP_API_CLIENT_ID`

and
`MDB_MCP_API_CLIENT_SECRET`

environment variables to enable them.

| Tool | Description |
|---|---|
`atlas-list-orgs` |
List MongoDB Atlas organizations |
`atlas-list-projects` |
List MongoDB Atlas projects |
`atlas-list-clusters` |
List MongoDB Atlas clusters |
`atlas-inspect-cluster` |
Inspect metadata of a cluster |
`atlas-list-db-users` |
List database users |
`atlas-create-free-cluster` |
Create a free Atlas cluster |
`atlas-create-project` |
Create an Atlas project |
`atlas-create-db-user` |
Create a database user |
`atlas-create-access-list` |
Configure IP access list |
`atlas-inspect-access-list` |
View IP access list entries |
`atlas-list-alerts` |
List Atlas alerts |
`atlas-get-performance-advisor` |
Get performance recommendations |

## Configuration[¶](#configuration)

### Environment variables[¶](#environment-variables)

| Variable | Description |
|---|---|
`MDB_MCP_CONNECTION_STRING` |
MongoDB connection string for database access |
`MDB_MCP_API_CLIENT_ID` |
Atlas API client ID for Atlas tools |
`MDB_MCP_API_CLIENT_SECRET` |
Atlas API client secret for Atlas tools |
`MDB_MCP_READ_ONLY` |
Enable read-only mode (`true` or `false` ) |
`MDB_MCP_DISABLED_TOOLS` |
Comma-separated list of tools to disable |
`MDB_MCP_LOG_PATH` |
Directory for log files |

### Read-only mode[¶](#read-only-mode)

The `--readOnly`

flag restricts the server to read, connect, and metadata
operations only. This prevents any create, update, or delete operations,
making it safe for data exploration without risk of accidental modifications.

### Disabling tools[¶](#disabling-tools)

You can disable specific tools or categories using `MDB_MCP_DISABLED_TOOLS`

:

- Tool names:
`find`

,`aggregate`

,`insert-many`

, etc. - Categories:
`atlas`

(all Atlas tools),`mongodb`

(all database tools) - Operation types:
`create`

,`update`

,`delete`

,`read`

,`metadata`

---
<!-- Source: https://google.github.io/adk-docs/tools/third-party/paypal/ -->

# PayPal¶

# PayPal[¶](#paypal)

The [PayPal MCP Server](https://github.com/paypal/paypal-mcp-server) connects
your ADK agent to the [PayPal](https://www.paypal.com/) ecosystem. This
integration gives your agent the ability to manage payments, invoices,
subscriptions, and disputes using natural language, enabling automated commerce
workflows and business insights.

## Use cases[¶](#use-cases)

-
**Streamline Financial Operations**: Create orders, send invoices, and process refunds directly through chat without switching context. You can instruct your agent to "bill Client X" or "refund order Y" immediately. -
**Manage Subscriptions & Products**: Handle the full lifecycle of recurring billing by creating products, setting up subscription plans, and managing subscriber details using natural language. -
**Resolve Issues & Track Performance**: Summarize and accept dispute claims, track shipment statuses, and retrieve merchant insights to make data-driven decisions on the fly.

## Prerequisites[¶](#prerequisites)

- Create a
[PayPal Developer account](https://developer.paypal.com/) - Create an app and retrieve your credentials from the
[PayPal Developer Dashboard](https://developer.paypal.com/) [Generate an access token](https://developer.paypal.com/reference/get-an-access-token/)from your credentials

## Use with agent[¶](#use-with-agent)

from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
PAYPAL_ENVIRONMENT = "SANDBOX" # Options: "SANDBOX" or "PRODUCTION"
PAYPAL_ACCESS_TOKEN = "YOUR_PAYPAL_ACCESS_TOKEN"
root_agent = Agent(
model="gemini-2.5-pro",
name="paypal_agent",
instruction="Help users manage their PayPal account",
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params=StdioServerParameters(
command="npx",
args=[
"-y",
"@paypal/mcp",
"--tools=all",
# (Optional) Specify which tools to enable
# "--tools=subscriptionPlans.list,subscriptionPlans.show",
],
env={
"PAYPAL_ACCESS_TOKEN": PAYPAL_ACCESS_TOKEN,
"PAYPAL_ENVIRONMENT": PAYPAL_ENVIRONMENT,
}
),
timeout=300,
),
)
],
)


from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import SseConnectionParams
PAYPAL_MCP_ENDPOINT = "https://mcp.sandbox.paypal.com/sse" # Production: https://mcp.paypal.com/sse
PAYPAL_ACCESS_TOKEN = "YOUR_PAYPAL_ACCESS_TOKEN"
root_agent = Agent(
model="gemini-2.5-pro",
name="paypal_agent",
instruction="Help users manage their PayPal account",
tools=[
McpToolset(
connection_params=SseConnectionParams(
url=PAYPAL_MCP_ENDPOINT,
headers={
"Authorization": f"Bearer {PAYPAL_ACCESS_TOKEN}",
},
),
)
],
)


import { LlmAgent, MCPToolset } from "@google/adk";
const PAYPAL_ENVIRONMENT = "SANDBOX"; // Options: "SANDBOX" or "PRODUCTION"
const PAYPAL_ACCESS_TOKEN = "YOUR_PAYPAL_ACCESS_TOKEN";
const rootAgent = new LlmAgent({
model: "gemini-2.5-pro",
name: "paypal_agent",
instruction: "Help users manage their PayPal account",
tools: [
new MCPToolset({
type: "StdioConnectionParams",
serverParams: {
command: "npx",
args: [
"-y",
"@paypal/mcp",
"--tools=all",
// (Optional) Specify which tools to enable
// "--tools=subscriptionPlans.list,subscriptionPlans.show",
],
env: {
PAYPAL_ACCESS_TOKEN: PAYPAL_ACCESS_TOKEN,
PAYPAL_ENVIRONMENT: PAYPAL_ENVIRONMENT,
},
},
}),
],
});
export { rootAgent };


Note

**Token Expiration**: PayPal Access Tokens have a limited lifespan of 3-8
hours. If your agent stops working, ensure your token has not expired and
generate a new one if necessary. You should implement token refresh logic to
handle token expiration.

## Available tools[¶](#available-tools)

### Catalog management[¶](#catalog-management)

| Tool | Description |
|---|---|
`create_product` |
Create a new product in the PayPal catalog |
`list_products` |
List products from the PayPal catalog |
`show_product_details` |
Show details of a specific product from the PayPal catalog |
`update_product` |
Update an existing product in the PayPal catalog |

### Dispute management[¶](#dispute-management)

| Tool | Description |
|---|---|
`list_disputes` |
Retrieve a summary of all disputes with optional filtering |
`get_dispute` |
Retrieve detailed information about a specific dispute |
`accept_dispute_claim` |
Accept a dispute claim, resolving it in favor of the buyer |

### Invoices[¶](#invoices)

| Tool | Description |
|---|---|
`create_invoice` |
Create a new invoice in the PayPal system |
`list_invoices` |
List invoices |
`get_invoice` |
Retrieve details about a specific invoice |
`send_invoice` |
Send an existing invoice to the specified recipient |
`send_invoice_reminder` |
Send a reminder for an existing invoice |
`cancel_sent_invoice` |
Cancel a sent invoice |
`generate_invoice_qr_code` |
Generate a QR code for an invoice |

### Payments[¶](#payments)

| Tool | Description |
|---|---|
`create_order` |
Create an order in the PayPal system based on the provided details |
`create_refund` |
Process a refund for a captured payment |
`get_order` |
Get details of a specific payment |
`get_refund` |
Get the details for a specific refund |
`pay_order` |
Capture payment for an authorized order |

### Reporting and insights[¶](#reporting-and-insights)

| Tool | Description |
|---|---|
`get_merchant_insights` |
Retrieve business intelligence metrics and analytics for a merchant |
`list_transactions` |
List all transactions |

### Shipment tracking[¶](#shipment-tracking)

| Tool | Description |
|---|---|
`create_shipment_tracking` |
Create shipment tracking information for a PayPal transaction |
`get_shipment_tracking` |
Get shipment tracking information for a specific shipment |
`update_shipment_tracking` |
Update shipment tracking information for a specific shipment |

### Subscription management[¶](#subscription-management)

| Tool | Description |
|---|---|
`cancel_subscription` |
Cancel an active subscription |
`create_subscription` |
Create a new subscription |
`create_subscription_plan` |
Create a new subscription plan |
`update_subscription` |
Update an existing subscription |
`list_subscription_plans` |
List subscription plans |
`show_subscription_details` |
Show details of a specific subscription |
`show_subscription_plan_details` |
Show details of a specific subscription plan |

## Configuration[¶](#configuration)

You can control which tools are enabled using the `--tools`

command-line
argument. This is useful for limiting the scope of the agent's permissions.

You can enable all tools with `--tools=all`

or specify a comma-separated list of
specific tool identifiers.

**Note**: The configuration identifiers below use dot notation (e.g.,
`invoices.create`

) which differs from the tool names exposed to the agent (e.g.,
`create_invoice`

).

**Products**: `products.create`

, `products.list`

, `products.update`

,
`products.show`


**Disputes**:
`disputes.list`

, `disputes.get`

, `disputes.create`


**Invoices**: `invoices.create`

, `invoices.list`

, `invoices.get`

,
`invoices.send`

, `invoices.sendReminder`

, `invoices.cancel`

,
`invoices.generateQRC`


**Orders & Payments**: `orders.create`

, `orders.get`

, `orders.capture`

,
`payments.createRefund`

, `payments.getRefunds`


**Transactions**:
`transactions.list`


**Shipment**:
`shipment.create`

, `shipment.get`


**Subscriptions**: `subscriptionPlans.create`

, `subscriptionPlans.list`

,
`subscriptionPlans.show`

, `subscriptions.create`

, `subscriptions.show`

,
`subscriptions.cancel`

---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/tools/google-cloud/ -->

# Google Cloud Tools¶

# Google Cloud Tools[¶](#google-cloud-tools)

Google Cloud tools make it easier to connect your agents to Google Cloud’s products and services. With just a few lines of code you can use these tools to connect your agents with:

**Any custom APIs**that developers host in Apigee.**100s**of**prebuilt connectors**to enterprise systems such as Salesforce, Workday, and SAP.**Automation workflows**built using application integration.**Databases**such as Spanner, AlloyDB, Postgres and more using the MCP Toolbox for databases.

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

[
](/adk-docs/tools/google-cloud/pubsub/)

### Pub/Sub Tools

Publish, pull, and acknowledge messages from Google Cloud Pub/Sub

---
<!-- Source: https://google.github.io/adk-docs/tools/google-cloud/vertex-ai-rag-engine/ -->

# Vertex AI RAG Engine tool for ADK¶

# Vertex AI RAG Engine tool for ADK[¶](#vertex-ai-rag-engine-tool-for-adk)

Supported in ADKPython v0.1.0Java v0.2.0

The `vertex_ai_rag_retrieval`

tool allows the agent to perform private data retrieval using Vertex
AI RAG Engine.

When you use grounding with Vertex AI RAG Engine, you need to prepare a RAG corpus beforehand.
Please refer to the [RAG ADK agent sample](https://github.com/google/adk-samples/blob/main/python/agents/RAG/rag/shared_libraries/prepare_corpus_and_data.py) or [Vertex AI RAG Engine page](https://cloud.google.com/vertex-ai/generative-ai/docs/rag-engine/rag-quickstart) for setting it up.

Warning: Single tool per agent limitation

This tool can only be used ** by itself** within an agent instance.
For more information about this limitation and workarounds, see

[Limitations for ADK tools](/adk-docs/tools/limitations/).

# Copyright 2025 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
import os
from google.adk.agents import Agent
from google.adk.tools.retrieval.vertex_ai_rag_retrieval import VertexAiRagRetrieval
from vertexai.preview import rag
from dotenv import load_dotenv
from .prompts import return_instructions_root
load_dotenv()
ask_vertex_retrieval = VertexAiRagRetrieval(
name='retrieve_rag_documentation',
description=(
'Use this tool to retrieve documentation and reference materials for the question from the RAG corpus,'
),
rag_resources=[
rag.RagResource(
# please fill in your own rag corpus
# here is a sample rag corpus for testing purpose
# e.g. projects/123/locations/us-central1/ragCorpora/456
rag_corpus=os.environ.get("RAG_CORPUS")
)
],
similarity_top_k=10,
vector_distance_threshold=0.6,
)
root_agent = Agent(
model='gemini-2.0-flash-001',
name='ask_rag_agent',
instruction=return_instructions_root(),
tools=[
ask_vertex_retrieval,
]
)

---
<!-- Source: https://google.github.io/adk-docs/tools/google-cloud/apigee-api-hub/ -->

# Apigee API Hub tools for ADK¶

# Apigee API Hub tools for ADK[¶](#apigee-api-hub-tools-for-adk)

**ApiHubToolset** lets you turn any documented API from Apigee API hub into a
tool with a few lines of code. This section shows you the step-by-step
instructions including setting up authentication for a secure connection to your
APIs.

**Prerequisites**

[Install ADK](/adk-docs/get-started/installation/)- Install the
[Google Cloud CLI](https://cloud.google.com/sdk/docs/install?db=bigtable-docs#installation_instructions). [Apigee API hub](https://cloud.google.com/apigee/docs/apihub/what-is-api-hub)instance with documented (i.e. OpenAPI spec) APIs- Set up your project structure and create required files

## Create an API Hub Toolset[¶](#create-an-api-hub-toolset)

Note: This tutorial includes an agent creation. If you already have an agent, you only need to follow a subset of these steps.

-
Get your access token, so that APIHubToolset can fetch spec from API Hub API. In your terminal run the following command

-
Ensure that the account used has the required permissions. You can use the pre-defined role

`roles/apihub.viewer`

or assign the following permissions:**apihub.specs.get (required)**- apihub.apis.get (optional)
- apihub.apis.list (optional)
- apihub.versions.get (optional)
- apihub.versions.list (optional)
- apihub.specs.list (optional)

-
Create a tool with

`APIHubToolset`

. Add the below to`tools.py`

If your API requires authentication, you must configure authentication for the tool. The following code sample demonstrates how to configure an API key. ADK supports token based auth (API Key, Bearer token), service account, and OpenID Connect. We will soon add support for various OAuth2 flows.

[from google.adk.tools.openapi_tool.auth.auth_helpers import token_to_scheme_credential](#__codelineno-2-1)[from google.adk.tools.apihub_tool.apihub_toolset import APIHubToolset](#__codelineno-2-2)[# Provide authentication for your APIs. Not required if your APIs don't required authentication.](#__codelineno-2-4)[auth_scheme, auth_credential = token_to_scheme_credential(](#__codelineno-2-5)["apikey", "query", "apikey", apikey_credential_str](#__codelineno-2-6)[)](#__codelineno-2-7)[sample_toolset = APIHubToolset(](#__codelineno-2-9)[name="apihub-sample-tool",](#__codelineno-2-10)[description="Sample Tool",](#__codelineno-2-11)[access_token="...", # Copy your access token generated in step 1](#__codelineno-2-12)[apihub_resource_name="...", # API Hub resource name](#__codelineno-2-13)[auth_scheme=auth_scheme,](#__codelineno-2-14)[auth_credential=auth_credential,](#__codelineno-2-15)[)](#__codelineno-2-16)For production deployment we recommend using a service account instead of an access token. In the code snippet above, use

`service_account_json=service_account_cred_json_str`

and provide your security account credentials instead of the token.For apihub_resource_name, if you know the specific ID of the OpenAPI Spec being used for your API, use

``projects/my-project-id/locations/us-west1/apis/my-api-id/versions/version-id/specs/spec-id``

. If you would like the Toolset to automatically pull the first available spec from the API, use``projects/my-project-id/locations/us-west1/apis/my-api-id``

-
Create your agent file Agent.py and add the created tools to your agent definition:

-
Configure your

`__init__.py`

to expose your agent -
Start the Google ADK Web UI and try your agent:


Then go to [http://localhost:8000](http://localhost:8000) to try your agent from the Web UI.

---
<!-- Source: https://google.github.io/adk-docs/tools/google-cloud/bigquery/ -->

# BigQuery tools for ADK¶

# BigQuery tools for ADK[¶](#bigquery-tools-for-adk)

Supported in ADKPython v1.1.0

These are a set of tools aimed to provide integration with BigQuery, namely:

: Fetches BigQuery dataset ids present in a GCP project.`list_dataset_ids`

: Fetches metadata about a BigQuery dataset.`get_dataset_info`

: Fetches table ids present in a BigQuery dataset.`list_table_ids`

: Fetches metadata about a BigQuery table.`get_table_info`

: Runs a SQL query in BigQuery and fetch the result.`execute_sql`

: Runs a BigQuery AI time series forecast using the`forecast`

`AI.FORECAST`

function.: Answers questions about data in BigQuery tables using natural language.`ask_data_insights`


They are packaged in the toolset `BigQueryToolset`

.

# Copyright 2025 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
import asyncio
from google.adk.agents import Agent
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.adk.tools.bigquery import BigQueryCredentialsConfig
from google.adk.tools.bigquery import BigQueryToolset
from google.adk.tools.bigquery.config import BigQueryToolConfig
from google.adk.tools.bigquery.config import WriteMode
from google.genai import types
import google.auth
# Define constants for this example agent
AGENT_NAME = "bigquery_agent"
APP_NAME = "bigquery_app"
USER_ID = "user1234"
SESSION_ID = "1234"
GEMINI_MODEL = "gemini-2.0-flash"
# Define a tool configuration to block any write operations
tool_config = BigQueryToolConfig(write_mode=WriteMode.BLOCKED)
# Use Application Default Credentials (ADC) for BigQuery authentication
# https://cloud.google.com/docs/authentication/provide-credentials-adc
application_default_credentials, _ = google.auth.default()
credentials_config = BigQueryCredentialsConfig(
credentials=application_default_credentials
)
# Instantiate a BigQuery toolset
bigquery_toolset = BigQueryToolset(
credentials_config=credentials_config, bigquery_tool_config=tool_config
)
# Agent Definition
bigquery_agent = Agent(
model=GEMINI_MODEL,
name=AGENT_NAME,
description=(
"Agent to answer questions about BigQuery data and models and execute"
" SQL queries."
),
instruction="""\
You are a data science agent with access to several BigQuery tools.
Make use of those tools to answer the user's questions.
""",
tools=[bigquery_toolset],
)
# Session and Runner
session_service = InMemorySessionService()
session = asyncio.run(
session_service.create_session(
app_name=APP_NAME, user_id=USER_ID, session_id=SESSION_ID
)
)
runner = Runner(
agent=bigquery_agent, app_name=APP_NAME, session_service=session_service
)
# Agent Interaction
def call_agent(query):
"""
Helper function to call the agent with a query.
"""
content = types.Content(role="user", parts=[types.Part(text=query)])
events = runner.run(user_id=USER_ID, session_id=SESSION_ID, new_message=content)
print("USER:", query)
for event in events:
if event.is_final_response():
final_response = event.content.parts[0].text
print("AGENT:", final_response)
call_agent("Are there any ml datasets in bigquery-public-data project?")
call_agent("Tell me more about ml_datasets.")
call_agent("Which all tables does it have?")
call_agent("Tell me more about the census_adult_income table.")
call_agent("How many rows are there per income bracket?")
call_agent(
"What is the statistical correlation between education_num, age, and the income_bracket?"
)


Note: If you want to access a BigQuery data agent as a tool, see [Data Agents tools for ADK](../data-agent/).

---
<!-- Source: https://google.github.io/adk-docs/tools/google-cloud/gke-code-executor/ -->

# GKE Code Executor tool for ADK¶

# GKE Code Executor tool for ADK[¶](#gke-code-executor-tool-for-adk)

The GKE Code Executor (`GkeCodeExecutor`

) provides a secure and scalable method
for running LLM-generated code by leveraging the GKE (Google Kubernetes Engine)
Sandbox environment, which uses gVisor for workload isolation. For each code
execution request, it dynamically creates an ephemeral, sandboxed Kubernetes Job
with a hardened Pod configuration. You should use this executor for production
environments on GKE where security and isolation are critical.

## How it Works[¶](#how-it-works)

When a request to execute code is made, the `GkeCodeExecutor`

performs the following steps:

**Creates a ConfigMap:**A Kubernetes ConfigMap is created to store the Python code that needs to be executed.**Creates a Sandboxed Pod:**A new Kubernetes Job is created, which in turn creates a Pod with a hardened security context and the gVisor runtime enabled. The code from the ConfigMap is mounted into this Pod.**Executes the Code:**The code is executed within the sandboxed Pod, isolated from the underlying node and other workloads.**Retrieves the Result:**The standard output and error streams from the execution are captured from the Pod's logs.**Cleans Up Resources:**Once the execution is complete, the Job and the associated ConfigMap are automatically deleted, ensuring that no artifacts are left behind.

## Key Benefits[¶](#key-benefits)

**Enhanced Security:**Code is executed in a gVisor-sandboxed environment with kernel-level isolation.**Ephemeral Environments:**Each code execution runs in its own ephemeral Pod, to prevent state transfer between executions.**Resource Control:**You can configure CPU and memory limits for the execution Pods to prevent resource abuse.**Scalability:**Allows you to run a large number of code executions in parallel, with GKE handling the scheduling and scaling of the underlying nodes.

## System requirements[¶](#system-requirements)

The following requirements must be met to successfully deploy your ADK project with the GKE Code Executor tool:

- GKE cluster with a
**gVisor-enabled node pool**. - Agent's service account requires specific
**RBAC permissions**, which allow it to:- Create, watch, and delete
**Jobs**for each execution request. - Manage
**ConfigMaps**to inject code into the Job's pod. - List
**Pods**and read their**logs**to retrieve the execution result

- Create, watch, and delete
- Install the client library with GKE extras:
`pip install google-adk[gke]`


For a complete, ready-to-use configuration, see the
[deployment_rbac.yaml](https://github.com/google/adk-python/blob/main/contributing/samples/gke_agent_sandbox/deployment_rbac.yaml)
sample. For more information on deploying ADK workflows to GKE, see
[Deploy to Google Kubernetes Engine (GKE)](/adk-docs/deploy/gke/).

from google.adk.agents import LlmAgent
from google.adk.code_executors import GkeCodeExecutor
# Initialize the executor, targeting the namespace where its ServiceAccount
# has the required RBAC permissions.
# This example also sets a custom timeout and resource limits.
gke_executor = GkeCodeExecutor(
namespace="agent-sandbox",
timeout_seconds=600,
cpu_limit="1000m", # 1 CPU core
mem_limit="1Gi",
)
# The agent now uses this executor for any code it generates.
gke_agent = LlmAgent(
name="gke_coding_agent",
model="gemini-2.0-flash",
instruction="You are a helpful AI agent that writes and executes Python code.",
code_executor=gke_executor,
)


## Configuration parameters[¶](#configuration-parameters)

The `GkeCodeExecutor`

can be configured with the following parameters:

| Parameter | Type | Description |
|---|---|---|
`namespace` |
`str` |
Kubernetes namespace where the execution Jobs will be created. Defaults to `"default"` . |
`image` |
`str` |
Container image to use for the execution Pod. Defaults to `"python:3.11-slim"` . |
`timeout_seconds` |
`int` |
Timeout in seconds for the code execution. Defaults to `300` . |
`cpu_requested` |
`str` |
Amount of CPU to request for the execution Pod. Defaults to `"200m"` . |
`mem_requested` |
`str` |
Amount of memory to request for the execution Pod. Defaults to `"256Mi"` . |
`cpu_limit` |
`str` |
Maximum amount of CPU the execution Pod can use. Defaults to `"500m"` . |
`mem_limit` |
`str` |
Maximum amount of memory the execution Pod can use. Defaults to `"512Mi"` . |
`kubeconfig_path` |
`str` |
Path to a kubeconfig file to use for authentication. Falls back to in-cluster config or the default local kubeconfig. |
`kubeconfig_context` |
`str` |
The `kubeconfig` context to use. |

---
<!-- Source: https://google.github.io/adk-docs/tools/google-cloud/data-agent/ -->

# Data Agents tools for ADK¶

# Data Agents tools for ADK[¶](#data-agents-tools-for-adk)

Supported in ADKPython v1.23.0

These are a set of tools aimed to provide integration with Data Agents powered by [Conversational Analytics API](https://docs.cloud.google.com/gemini/docs/conversational-analytics-api/overview).

Data Agents are AI-powered agents that help you analyze your data using natural language. When configuring a Data Agent, you can choose from supported data sources, including **BigQuery**, **Looker**, and **Looker Studio**.

**Prerequisites**

Before using these tools, you must build and configure your Data Agents in Google Cloud:

[Build a data agent using HTTP and Python](https://docs.cloud.google.com/gemini/docs/conversational-analytics-api/build-agent-http)[Build a data agent using the Python SDK](https://docs.cloud.google.com/gemini/docs/conversational-analytics-api/build-agent-sdk)[Create a data agent in BigQuery Studio](https://docs.cloud.google.com/bigquery/docs/create-data-agents#create_a_data_agent)

The `DataAgentToolset`

includes the following tools:

: Lists Data Agents you have permission to access in the configured GCP project.`list_accessible_data_agents`

: Retrieves details about a specific Data Agent given its full resource name.`get_data_agent_info`

: Chats with a specific Data Agent using natural language.`ask_data_agent`


They are packaged in the toolset `DataAgentToolset`

.

# Copyright 2026 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
import asyncio
from google.adk.agents import Agent
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.adk.tools.data_agent.config import DataAgentToolConfig
from google.adk.tools.data_agent.credentials import DataAgentCredentialsConfig
from google.adk.tools.data_agent.data_agent_toolset import DataAgentToolset
from google.genai import types
import google.auth
# Define constants for this example agent
AGENT_NAME = "data_agent_example"
APP_NAME = "data_agent_app"
USER_ID = "user1234"
SESSION_ID = "1234"
GEMINI_MODEL = "gemini-2.5-flash"
# Define tool configuration
tool_config = DataAgentToolConfig(
max_query_result_rows=100,
)
# Use Application Default Credentials (ADC)
# https://cloud.google.com/docs/authentication/provide-credentials-adc
application_default_credentials, _ = google.auth.default()
credentials_config = DataAgentCredentialsConfig(
credentials=application_default_credentials
)
# Instantiate a Data Agent toolset
da_toolset = DataAgentToolset(
credentials_config=credentials_config,
data_agent_tool_config=tool_config,
tool_filter=[
"list_accessible_data_agents",
"get_data_agent_info",
"ask_data_agent",
],
)
# Agent Definition
data_agent = Agent(
name=AGENT_NAME,
model=GEMINI_MODEL,
description="Agent to answer user questions using Data Agents.",
instruction=(
"## Persona\nYou are a helpful assistant that uses Data Agents"
" to answer user questions about their data.\n\n"
),
tools=[da_toolset],
)
# Session and Runner
session_service = InMemorySessionService()
session = asyncio.run(
session_service.create_session(
app_name=APP_NAME, user_id=USER_ID, session_id=SESSION_ID
)
)
runner = Runner(
agent=data_agent, app_name=APP_NAME, session_service=session_service
)
# Agent Interaction
def call_agent(query):
"""
Helper function to call the agent with a query.
"""
content = types.Content(role="user", parts=[types.Part(text=query)])
events = runner.run(user_id=USER_ID, session_id=SESSION_ID, new_message=content)
print("USER:", query)
for event in events:
if event.is_final_response():
final_response = event.content.parts[0].text
print("AGENT:", final_response)
call_agent("List accessible data agents in project <PROJECT_ID>.")
call_agent("Get information about <DATA_AGENT_NAME>.")
# The data agent in this example is configured with the BigQuery table:
# `bigquery-public-data.san_francisco.street_trees`
call_agent("Ask <DATA_AGENT_NAME> to count the rows in the table.")
call_agent("What are the columns in the table?")
call_agent("What are the top 5 tree species?")
call_agent("For those species, what is the distribution of legal status?")

---
<!-- Source: https://google.github.io/adk-docs/tools/google-cloud/vertex-ai-search/ -->

# Vertex AI Search tool for ADK¶

# Vertex AI Search tool for ADK[¶](#vertex-ai-search-tool-for-adk)

Supported in ADKPython v0.1.0

The `vertex_ai_search_tool`

uses Google Cloud Vertex AI Search, enabling the
agent to search across your private, configured data stores (e.g., internal
documents, company policies, knowledge bases). This built-in tool requires you
to provide the specific data store ID during configuration. For further details
of the tool, see
[Understanding Vertex AI Search grounding](/adk-docs/grounding/vertex_ai_search_grounding/).

Warning: Single tool per agent limitation

This tool can only be used ** by itself** within an agent instance.
For more information about this limitation and workarounds, see

[Limitations for ADK tools](/adk-docs/tools/limitations/#one-tool-one-agent).

# Copyright 2024 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
import asyncio
from google.adk.agents import LlmAgent
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.genai import types
from google.adk.tools import VertexAiSearchTool
# Replace with your Vertex AI Search Datastore ID, and respective region (e.g. us-central1 or global).
# Format: projects/<PROJECT_ID>/locations/<REGION>/collections/default_collection/dataStores/<DATASTORE_ID>
DATASTORE_PATH = "DATASTORE_PATH_HERE"
# Constants
APP_NAME_VSEARCH = "vertex_search_app"
USER_ID_VSEARCH = "user_vsearch_1"
SESSION_ID_VSEARCH = "session_vsearch_1"
AGENT_NAME_VSEARCH = "doc_qa_agent"
GEMINI_2_FLASH = "gemini-2.0-flash"
# Tool Instantiation
# You MUST provide your datastore ID here.
vertex_search_tool = VertexAiSearchTool(data_store_id=DATASTORE_PATH)
# Agent Definition
doc_qa_agent = LlmAgent(
name=AGENT_NAME_VSEARCH,
model=GEMINI_2_FLASH, # Requires Gemini model
tools=[vertex_search_tool],
instruction=f"""You are a helpful assistant that answers questions based on information found in the document store: {DATASTORE_PATH}.
Use the search tool to find relevant information before answering.
If the answer isn't in the documents, say that you couldn't find the information.
""",
description="Answers questions using a specific Vertex AI Search datastore.",
)
# Session and Runner Setup
session_service_vsearch = InMemorySessionService()
runner_vsearch = Runner(
agent=doc_qa_agent, app_name=APP_NAME_VSEARCH, session_service=session_service_vsearch
)
session_vsearch = session_service_vsearch.create_session(
app_name=APP_NAME_VSEARCH, user_id=USER_ID_VSEARCH, session_id=SESSION_ID_VSEARCH
)
# Agent Interaction Function
async def call_vsearch_agent_async(query):
print("\n--- Running Vertex AI Search Agent ---")
print(f"Query: {query}")
if "DATASTORE_PATH_HERE" in DATASTORE_PATH:
print("Skipping execution: Please replace DATASTORE_PATH_HERE with your actual datastore ID.")
print("-" * 30)
return
content = types.Content(role='user', parts=[types.Part(text=query)])
final_response_text = "No response received."
try:
async for event in runner_vsearch.run_async(
user_id=USER_ID_VSEARCH, session_id=SESSION_ID_VSEARCH, new_message=content
):
# Like Google Search, results are often embedded in the model's response.
if event.is_final_response() and event.content and event.content.parts:
final_response_text = event.content.parts[0].text.strip()
print(f"Agent Response: {final_response_text}")
# You can inspect event.grounding_metadata for source citations
if event.grounding_metadata:
print(f" (Grounding metadata found with {len(event.grounding_metadata.grounding_attributions)} attributions)")
except Exception as e:
print(f"An error occurred: {e}")
print("Ensure your datastore ID is correct and the service account has permissions.")
print("-" * 30)
# --- Run Example ---
async def run_vsearch_example():
# Replace with a question relevant to YOUR datastore content
await call_vsearch_agent_async("Summarize the main points about the Q2 strategy document.")
await call_vsearch_agent_async("What safety procedures are mentioned for lab X?")
# Execute the example
# await run_vsearch_example()
# Running locally due to potential colab asyncio issues with multiple awaits
try:
asyncio.run(run_vsearch_example())
except RuntimeError as e:
if "cannot be called from a running event loop" in str(e):
print("Skipping execution in running event loop (like Colab/Jupyter). Run locally.")
else:
raise e

---
<!-- Source: https://google.github.io/adk-docs/tools/google-cloud/express-mode/ -->

# Vertex AI express mode¶

# Vertex AI express mode[¶](#vertex-ai-express-mode)

Google Cloud Vertex AI express mode provides a no-cost access tier for prototyping and development, allowing you to use Vertex AI services without creating a full Google Cloud Project. This service includes access to many powerful Vertex AI services, including:

You can sign up for an express mode account using a Gmail account and receive an
API key to use with the ADK. Obtain an API key through the
[Google Cloud Console](https://console.cloud.google.com/expressmode).
For more information, see
[Vertex AI express mode](https://cloud.google.com/vertex-ai/generative-ai/docs/start/express-mode/overview).

Preview release

The Vertex AI express mode feature is a Preview release. For
more information, see the
[launch stage descriptions](https://cloud.google.com/products#product-launch-stages).

## Vertex AI express mode limitations

Vertex AI express mode projects are only valid for 90 days and only select services are available to be used with limited quota. For example, the number of Agent Engines is restricted to 10 and deployment to Agent Engine requires paid access. To remove the quota restrictions and use all of Vertex AI's services, add a billing account to your express mode project.

## Configure Agent Engine container[¶](#configure-agent-engine-container)

When using Vertex AI express mode, create an `AgentEngine`

object to enable
Vertex AI management of agent components such as `Session`

and `Memory`

objects.
With this approach, `Session`

objects are handled as children of the
`AgentEngine`

object. Before running your agent make sure your environment
variables are set correctly, as shown below:

Next, create your Agent Engine instance using the Vertex AI SDK.

-
Import Vertex AI SDK.

-
Initialize the Vertex AI Client with your API key and create an agent engine instance.

-
Get the Agent Engine name and ID from the response to use with Memories and Sessions.


## Manage Sessions with `VertexAiSessionService`

[¶](#vertex-ai-session-service)

[ VertexAiSessionService](/adk-docs/sessions/session.md#sessionservice-implementations)
is compatible with Vertex AI express mode API Keys. You can instead initialize
the session object without any project or location.

# Requires: pip install google-adk[vertexai]
# Plus environment variable setup:
# GOOGLE_GENAI_USE_VERTEXAI=TRUE
# GOOGLE_API_KEY=PASTE_YOUR_ACTUAL_EXPRESS_MODE_API_KEY_HERE
from google.adk.sessions import VertexAiSessionService
# The app_name used with this service should be the Reasoning Engine ID or name
APP_ID = "your-reasoning-engine-id"
# Project and location are not required when initializing with Vertex express mode
session_service = VertexAiSessionService(agent_engine_id=APP_ID)
# Use REASONING_ENGINE_APP_ID when calling service methods, e.g.:
# session = await session_service.create_session(app_name=APP_ID, user_id= ...)


Session Service Quotas

For Free express mode Projects, `VertexAiSessionService`

has the following quota:

- 10 Create, delete, or update Vertex AI Agent Engine sessions per minute
- 30 Append event to Vertex AI Agent Engine sessions per minute

## Manage Memory with `VertexAiMemoryBankService`

[¶](#vertex-ai-memory-bank)

[ VertexAiMemoryBankService](/adk-docs/sessions/memory.md#vertex-ai-memory-bank)
is compatible with Vertex AI express mode API Keys. You can instead initialize
the memory object without any project or location.

# Requires: pip install google-adk[vertexai]
# Plus environment variable setup:
# GOOGLE_GENAI_USE_VERTEXAI=TRUE
# GOOGLE_API_KEY=PASTE_YOUR_ACTUAL_EXPRESS_MODE_API_KEY_HERE
from google.adk.memory import VertexAiMemoryBankService
# The app_name used with this service should be the Reasoning Engine ID or name
APP_ID = "your-reasoning-engine-id"
# Project and location are not required when initializing with express mode
memory_service = VertexAiMemoryBankService(agent_engine_id=APP_ID)
# Generate a memory from that session so the Agent can remember relevant details about the user
# memory = await memory_service.add_session_to_memory(session)


Memory Service Quotas

For Free express mode Projects, `VertexAiMemoryBankService`

has the following quota:

- 10 Create, delete, or update Vertex AI Agent Engine memory resources per minute
- 10 Get, list, or retrieve from Vertex AI Agent Engine Memory Bank per minute

### Code Sample: Weather Agent with Session and Memory[¶](#code-sample-weather-agent-with-session-and-memory)

This code sample shows a weather agent that utilizes both
`VertexAiSessionService`

and `VertexAiMemoryBankService`

for context management,
allowing your agent to recall user preferences and conversations.

[Weather Agent with Session and Memory](https://github.com/google/adk-docs/blob/main/examples/python/notebooks/express-mode-weather-agent.ipynb)using Vertex AI express mode

---
<!-- Source: https://google.github.io/adk-docs/tools/google-cloud/bigtable/ -->

# Bigtable database tool for ADK¶

# Bigtable database tool for ADK[¶](#bigtable-database-tool-for-adk)

Supported in ADKPython v1.12.0

These are a set of tools aimed to provide integration with Bigtable, namely:

: Fetches Bigtable instances in a Google Cloud project.`list_instances`

: Fetches metadata instance information in a Google Cloud project.`get_instance_info`

: Fetches tables in a GCP Bigtable instance.`list_tables`

: Fetches metadata table information in a GCP Bigtable.`get_table_info`

: Runs a SQL query in Bigtable table and fetch the result.`execute_sql`


They are packaged in the toolset `BigtableToolset`

.

# Copyright 2025 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
import asyncio
from google.adk.agents import Agent
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.adk.tools.google_tool import GoogleTool
from google.adk.tools.bigtable import query_tool
from google.adk.tools.bigtable.settings import BigtableToolSettings
from google.adk.tools.bigtable.bigtable_credentials import BigtableCredentialsConfig
from google.adk.tools.bigtable.bigtable_toolset import BigtableToolset
from google.genai import types
from google.adk.tools.tool_context import ToolContext
import google.auth
from google.auth.credentials import Credentials
# Define constants for this example agent
AGENT_NAME = "bigtable_agent"
APP_NAME = "bigtable_app"
USER_ID = "user1234"
SESSION_ID = "1234"
GEMINI_MODEL = "gemini-2.5-flash"
# Define Bigtable tool config with read capability set to allowed.
tool_settings = BigtableToolSettings()
# Define a credentials config - in this example we are using application default
# credentials
# https://cloud.google.com/docs/authentication/provide-credentials-adc
application_default_credentials, _ = google.auth.default()
credentials_config = BigtableCredentialsConfig(
credentials=application_default_credentials
)
# Instantiate a Bigtable toolset
bigtable_toolset = BigtableToolset(
credentials_config=credentials_config, bigtable_tool_settings=tool_settings
)
# Optional
# Create a wrapped function tool for the agent on top of the built-in
# `execute_sql` tool in the bigtable toolset.
# For example, this customized tool can perform a dynamically-built query.
def count_rows_tool(
table_name: str,
credentials: Credentials, # GoogleTool handles `credentials`
settings: BigtableToolSettings, # GoogleTool handles `settings`
tool_context: ToolContext, # GoogleTool handles `tool_context`
):
"""Counts the total number of rows for a specified table.
Args:
table_name: The name of the table for which to count rows.
Returns:
The total number of rows in the table.
"""
# Replace the following settings for a specific bigtable database.
PROJECT_ID = "<PROJECT_ID>"
INSTANCE_ID = "<INSTANCE_ID>"
query = f"""
SELECT count(*) FROM {table_name}
"""
return query_tool.execute_sql(
project_id=PROJECT_ID,
instance_id=INSTANCE_ID,
query=query,
credentials=credentials,
settings=settings,
tool_context=tool_context,
)
# Agent Definition
bigtable_agent = Agent(
model=GEMINI_MODEL,
name=AGENT_NAME,
description=(
"Agent to answer questions about bigtable database and execute SQL queries."
),
instruction="""\
You are a data assistant agent with access to several bigtable tools.
Make use of those tools to answer the user's questions.
""",
tools=[
bigtable_toolset,
# Add customized bigtable tool based on the built-in bigtable toolset.
GoogleTool(
func=count_rows_tool,
credentials_config=credentials_config,
tool_settings=tool_settings,
),
],
)
# Session and Runner
session_service = InMemorySessionService()
session = asyncio.run(
session_service.create_session(
app_name=APP_NAME, user_id=USER_ID, session_id=SESSION_ID
)
)
runner = Runner(
agent=bigtable_agent, app_name=APP_NAME, session_service=session_service
)
# Agent Interaction
def call_agent(query):
"""
Helper function to call the agent with a query.
"""
content = types.Content(role="user", parts=[types.Part(text=query)])
events = runner.run(user_id=USER_ID, session_id=SESSION_ID, new_message=content)
print("USER:", query)
for event in events:
if event.is_final_response():
final_response = event.content.parts[0].text
print("AGENT:", final_response)
# Replace the bigtable instance and table names below with your own.
call_agent("List all tables in projects/<PROJECT_ID>/instances/<INSTANCE_ID>")
call_agent("List the top 5 rows in <TABLE_NAME>")

---
<!-- Source: https://google.github.io/adk-docs/tools/google-cloud/pubsub/ -->

# Pub/Sub tool for ADK¶

# Pub/Sub tool for ADK[¶](#pubsub-tool-for-adk)

Supported in ADKPython v1.22.0

The `PubSubToolset`

allows agents to interact with
[Google Cloud Pub/Sub](https://cloud.google.com/pubsub)
service to publish, pull, and acknowledge messages.

## Prerequisites[¶](#prerequisites)

Before using the `PubSubToolset`

, you need to:

**Enable the Pub/Sub API**in your Google Cloud project.**Authenticate and authorize**: Ensure that the principal (e.g., user, service account) running the agent has the necessary IAM permissions to perform Pub/Sub operations. For more information on Pub/Sub roles, see the[Pub/Sub access control documentation](https://cloud.google.com/pubsub/docs/access-control).**Create a topic or subscription**:[Create a topic](https://cloud.google.com/pubsub/docs/create-topic)to publish messages and[create a subscription](https://cloud.google.com/pubsub/docs/create-subscription)to receive them.

## Usage[¶](#usage)

# Copyright 2025 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
import asyncio
import os
from google.adk.agents import Agent
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.adk.tools.pubsub.config import PubSubToolConfig
from google.adk.tools.pubsub.pubsub_credentials import PubSubCredentialsConfig
from google.adk.tools.pubsub.pubsub_toolset import PubSubToolset
from google.genai import types
import google.auth
# Define constants for this example agent
AGENT_NAME = "pubsub_agent"
APP_NAME = "pubsub_app"
USER_ID = "user1234"
SESSION_ID = "1234"
GEMINI_MODEL = "gemini-2.0-flash"
# Define Pub/Sub tool config.
# You can optionally set the project_id here, or let the agent infer it from context/user input.
tool_config = PubSubToolConfig(project_id=os.getenv("GOOGLE_CLOUD_PROJECT"))
# Uses externally-managed Application Default Credentials (ADC) by default.
# This decouples authentication from the agent / tool lifecycle.
# https://cloud.google.com/docs/authentication/provide-credentials-adc
application_default_credentials, _ = google.auth.default()
credentials_config = PubSubCredentialsConfig(
credentials=application_default_credentials
)
# Instantiate a Pub/Sub toolset
pubsub_toolset = PubSubToolset(
credentials_config=credentials_config, pubsub_tool_config=tool_config
)
# Agent Definition
pubsub_agent = Agent(
model=GEMINI_MODEL,
name=AGENT_NAME,
description=(
"Agent to publish, pull, and acknowledge messages from Google Cloud"
" Pub/Sub."
),
instruction="""\
You are a cloud engineer agent with access to Google Cloud Pub/Sub tools.
You can publish messages to topics, pull messages from subscriptions, and acknowledge messages.
""",
tools=[pubsub_toolset],
)
# Session and Runner
session_service = InMemorySessionService()
session = asyncio.run(
session_service.create_session(
app_name=APP_NAME, user_id=USER_ID, session_id=SESSION_ID
)
)
runner = Runner(
agent=pubsub_agent, app_name=APP_NAME, session_service=session_service
)
# Agent Interaction
def call_agent(query):
"""
Helper function to call the agent with a query.
"""
content = types.Content(role="user", parts=[types.Part(text=query)])
events = runner.run(user_id=USER_ID, session_id=SESSION_ID, new_message=content)
print("USER:", query)
for event in events:
if event.is_final_response():
final_response = event.content.parts[0].text
print("AGENT:", final_response)
call_agent("publish 'Hello World' to 'my-topic'")
call_agent("pull messages from 'my-subscription'")


## Tools[¶](#tools)

The `PubSubToolset`

includes the following tools:

`publish_message`

[¶](#publish_message)

Publishes a message to a Pub/Sub topic.

| Parameter | Type | Description |
|---|---|---|
`topic_name` |
`str` |
The name of the Pub/Sub topic (e.g., `projects/my-project/topics/my-topic` ). |
`message` |
`str` |
The message content to publish. |
`attributes` |
`dict[str, str]` |
(Optional) Attributes to attach to the message. |
`ordering_key` |
`str` |
(Optional) The ordering key for the message. If you set this parameter, messages are published in order. |

`pull_messages`

[¶](#pull_messages)

Pulls messages from a Pub/Sub subscription.

| Parameter | Type | Description |
|---|---|---|
`subscription_name` |
`str` |
The name of the Pub/Sub subscription (e.g., `projects/my-project/subscriptions/my-sub` ). |
`max_messages` |
`int` |
(Optional) The maximum number of messages to pull. Defaults to `1` . |
`auto_ack` |
`bool` |
(Optional) Whether to automatically acknowledge the messages. Defaults to `False` . |

`acknowledge_messages`

[¶](#acknowledge_messages)

Acknowledges one or more messages on a Pub/Sub subscription.

| Parameter | Type | Description |
|---|---|---|
`subscription_name` |
`str` |
The name of the Pub/Sub subscription (e.g., `projects/my-project/subscriptions/my-sub` ). |
`ack_ids` |
`list[str]` |
A list of acknowledgment IDs to acknowledge. |

---
<!-- Source: https://google.github.io/adk-docs/tools/google-cloud/spanner/ -->

# Spanner database tool for ADK¶

# Spanner database tool for ADK[¶](#spanner-database-tool-for-adk)

Supported in ADKPython v1.11.0

These are a set of tools aimed to provide integration with Spanner, namely:

: Fetches table names present in a GCP Spanner database.`list_table_names`

: Fetches table indexes present in a GCP Spanner database.`list_table_indexes`

: Fetches table index columns present in a GCP Spanner database.`list_table_index_columns`

: Fetches named schema for a Spanner database.`list_named_schemas`

: Fetches Spanner database table schema and metadata information.`get_table_schema`

: Runs a SQL query in Spanner database and fetch the result.`execute_sql`

: Similarity search in Spanner using a text query.`similarity_search`


They are packaged in the toolset `SpannerToolset`

.

# Copyright 2025 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
import asyncio
from google.adk.agents import Agent
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
# from google.adk.sessions import DatabaseSessionService
from google.adk.tools.google_tool import GoogleTool
from google.adk.tools.spanner import query_tool
from google.adk.tools.spanner.settings import SpannerToolSettings
from google.adk.tools.spanner.settings import Capabilities
from google.adk.tools.spanner.spanner_credentials import SpannerCredentialsConfig
from google.adk.tools.spanner.spanner_toolset import SpannerToolset
from google.genai import types
from google.adk.tools.tool_context import ToolContext
import google.auth
from google.auth.credentials import Credentials
# Define constants for this example agent
AGENT_NAME = "spanner_agent"
APP_NAME = "spanner_app"
USER_ID = "user1234"
SESSION_ID = "1234"
GEMINI_MODEL = "gemini-2.5-flash"
# Define Spanner tool config with read capability set to allowed.
tool_settings = SpannerToolSettings(capabilities=[Capabilities.DATA_READ])
# Define a credentials config - in this example we are using application default
# credentials
# https://cloud.google.com/docs/authentication/provide-credentials-adc
application_default_credentials, _ = google.auth.default()
credentials_config = SpannerCredentialsConfig(
credentials=application_default_credentials
)
# Instantiate a Spanner toolset
spanner_toolset = SpannerToolset(
credentials_config=credentials_config, spanner_tool_settings=tool_settings
)
# Optional
# Create a wrapped function tool for the agent on top of the built-in
# `execute_sql` tool in the Spanner toolset.
# For example, this customized tool can perform a dynamically-built query.
def count_rows_tool(
table_name: str,
credentials: Credentials, # GoogleTool handles `credentials`
settings: SpannerToolSettings, # GoogleTool handles `settings`
tool_context: ToolContext, # GoogleTool handles `tool_context`
):
"""Counts the total number of rows for a specified table.
Args:
table_name: The name of the table for which to count rows.
Returns:
The total number of rows in the table.
"""
# Replace the following settings for a specific Spanner database.
PROJECT_ID = "<PROJECT_ID>"
INSTANCE_ID = "<INSTANCE_ID>"
DATABASE_ID = "<DATABASE_ID>"
query = f"""
SELECT count(*) FROM {table_name}
"""
return query_tool.execute_sql(
project_id=PROJECT_ID,
instance_id=INSTANCE_ID,
database_id=DATABASE_ID,
query=query,
credentials=credentials,
settings=settings,
tool_context=tool_context,
)
# Agent Definition
spanner_agent = Agent(
model=GEMINI_MODEL,
name=AGENT_NAME,
description=(
"Agent to answer questions about Spanner database and execute SQL queries."
),
instruction="""\
You are a data assistant agent with access to several Spanner tools.
Make use of those tools to answer the user's questions.
""",
tools=[
spanner_toolset,
# Add customized Spanner tool based on the built-in Spanner toolset.
GoogleTool(
func=count_rows_tool,
credentials_config=credentials_config,
tool_settings=tool_settings,
),
],
)
# Session and Runner
session_service = InMemorySessionService()
# Optionally, Spanner can be used as the Database Session Service for production.
# Note that it's suggested to use a dedicated instance/database for storing sessions.
# session_service_spanner_db_url = "spanner+spanner:///projects/PROJECT_ID/instances/INSTANCE_ID/databases/my-adk-session"
# session_service = DatabaseSessionService(db_url=session_service_spanner_db_url)
session = asyncio.run(
session_service.create_session(
app_name=APP_NAME, user_id=USER_ID, session_id=SESSION_ID
)
)
runner = Runner(
agent=spanner_agent, app_name=APP_NAME, session_service=session_service
)
# Agent Interaction
def call_agent(query):
"""
Helper function to call the agent with a query.
"""
content = types.Content(role="user", parts=[types.Part(text=query)])
events = runner.run(user_id=USER_ID, session_id=SESSION_ID, new_message=content)
print("USER:", query)
for event in events:
if event.is_final_response():
final_response = event.content.parts[0].text
print("AGENT:", final_response)
# Replace the Spanner database and table names below with your own.
call_agent("List all tables in projects/<PROJECT_ID>/instances/<INSTANCE_ID>/databases/<DATABASE_ID>")
call_agent("Describe the schema of <TABLE_NAME>")
call_agent("List the top 5 rows in <TABLE_NAME>")

---
<!-- Source: https://google.github.io/adk-docs/tools/google-cloud/api-registry/ -->

# Connect MCP tools from Cloud API Registry¶

# Connect MCP tools from Cloud API Registry[¶](#connect-mcp-tools-from-cloud-api-registry)

The Google Cloud API Registry connector tool for Agent Development Kit (ADK)
lets you access a wide range of Google Cloud services for your agents as Model
Context Protocol (MCP) servers through the
[Google Cloud API Registry](https://docs.cloud.google.com/api-registry/docs/overview).
You can configure this tool to connect your agent to your Google Cloud projects
and dynamically access Cloud services enabled for that project.

Preview release

The Google Cloud API Registry feature is a Preview release. For
more information, see the
[launch stage descriptions](https://cloud.google.com/products#product-launch-stages).

## Prerequisites[¶](#prerequisites)

Before using the API Registry with your agent, you need to ensure the following:

-
**Google Cloud project:**Configure your agent to access AI models using an existing Google Cloud project. -
**API Registry access:**The environment where your agent runs needs Google Cloud[Application Default Credentials](https://docs.cloud.google.com/docs/authentication/provide-credentials-adc)with the`apiregistry.viewer`

role to list available MCP servers. -
**Cloud APIs:**In your Google Cloud project, enable the*cloudapiregistry.googleapis.com*and*apihub.googleapis.com*Google Cloud APIs. -
**MCP Server and Tool access:**Make sure you enable the MCP Servers in the API Registry for the Google Cloud services in your Cloud Project that you want access with your agent. You can enable this in the Cloud Console or use a gcloud command such as:`gcloud beta api-registry mcp enable bigquery.googleapis.com --project={PROJECT_ID}`

. The credentials used by the agent must have permissions to access the MCP server and the underlying services used by the tools. For example, to use BigQuery tools, the service account needs BigQuery IAM roles like`bigquery.dataViewer`

and`bigquery.jobUser`

. For more information about required permissions, see[Authentication and access](#auth).

You can check what MCP servers are enabled with API Registry using the following gcloud command:

## Use with agent[¶](#use-with-agent)

When configuring the API Registry connector tool with an agent, you first
initialize the ** ApiRegistry** class to establish a connection with Cloud
services, and then use the

`get_toolset()`

function to retrieve a toolset for a
specific MCP server registered in the API Registry. The following code example
demonstrates how to create an agent that uses tools from an MCP server listed in
API Registry. This agent is designed to interact with BigQuery:import os
from google.adk.agents.llm_agent import LlmAgent
from google.adk.tools.api_registry import ApiRegistry
# Configure with your Google Cloud Project ID and registered MCP server name
PROJECT_ID = "your-google-cloud-project-id"
MCP_SERVER_NAME = "projects/your-google-cloud-project-id/locations/global/mcpServers/your-mcp-server-name"
# Example header provider for BigQuery, a project header is required.
def header_provider(context):
return {"x-goog-user-project": PROJECT_ID}
# Initialize ApiRegistry
api_registry = ApiRegistry(
api_registry_project_id=PROJECT_ID,
header_provider=header_provider
)
# Get the toolset for the specific MCP server
registry_tools = api_registry.get_toolset(
mcp_server_name=MCP_SERVER_NAME,
# Optionally filter tools:
#tool_filter=["list_datasets", "run_query"]
)
# Create an agent with the tools
root_agent = LlmAgent(
model="gemini-1.5-flash", # Or your preferred model
name="bigquery_assistant",
instruction="""
Help user access their BigQuery data using the available tools.
""",
tools=[registry_tools],
)


For the complete code for this example, see the
[api_registry_agent](https://github.com/google/adk-python/tree/main/contributing/samples/api_registry_agent/)
sample. For information on the configuration options, see
[Configuration](#configuration).
For information on the authentication for this tool, see
[Authentication and access](#auth).

## Authentication and access[¶](#auth)

Using the API Registry with your agent requires authentication for the services
the agent accesses. By default the tool uses Google Cloud
[Application Default Credentials](https://docs.cloud.google.com/docs/authentication/provide-credentials-adc)
for authentication. When using this tool make sure your agent has the following
permissions and access:

-
**API Registry access:**The`ApiRegistry`

class uses Application Default Credentials (`google.auth.default()`

) to authenticate requests to the Google Cloud API Registry to list the available MCP servers. Ensure the environment where the agent runs has credentials with the necessary permissions to view the API Registry resources, such as`apiregistry.viewer`

. -
**MCP Server and Tool access:**The`McpToolset`

returned by`get_toolset`

also uses the Google Cloud Application Default Credentials by default to authenticate calls to the actual MCP server endpoint. The credentials used must have the necessary permissions for both:- Accessing the MCP server itself.
- Utilizing the underlying services and resources that the tools interact with.

-
**MCP Tool user role:**Allow the account used by your agent to call MCP tools through the API registry by granting the MCP tool user role:`gcloud projects add-iam-policy-binding {PROJECT_ID} --member={member} --role="roles/mcp.toolUser"`


For example, when using MCP server tools that interact with BigQuery, the
account associated with the credentials, such as a service account, must be
granted appropriate BigQuery IAM roles, such as `bigquery.dataViewer`

or
`bigquery.jobUser`

, within your Google Cloud project to access datasets and run
queries. In the case of the bigquery MCP server, a ```
"x-goog-user-project":
PROJECT_ID
```

header is required to use its tools Additional headers for
authentication or project context can be injected via the `header_provider`

argument in the `ApiRegistry`

constructor.

## Configuration[¶](#configuration)

The ** APIRegistry** object has the following configuration options:

-
(str): The Google Cloud Project ID where the API Registry is located.`api_registry_project_id`

-
(str, optional): The location of the API Registry resources. Defaults to`location`

`"global"`

. -
(Callable, optional): A function that takes the call context and returns a dictionary of additional HTTP headers to be sent with requests to the MCP server. This is often used for dynamic authentication or project-specific headers.`header_provider`


The `get_toolset()`

function has the following configuration options:

-
(str): The full name of the registered MCP server from which to load tools, for example:`mcp_server_name`

`projects/my-project/locations/global/mcpServers/my-server`

. -
(Union[ToolPredicate, List[str]], optional): Specifies which tools to include in the toolset.`tool_filter`

- If a list of strings, only tools with names in the list are included.
- If a
`ToolPredicate`

function, the function is called for each tool, and only tools for which it returns`True`

are included. - If
`None`

, all tools from the MCP server are included.

-
(str, optional): A prefix to add to the name of each tool in the resulting toolset.`tool_name_prefix`


## Additional resources[¶](#additional-resources)

[api_registry_agent](https://github.com/google/adk-python/tree/main/contributing/samples/api_registry_agent/)ADK code sample[Google Cloud API Registry](https://docs.cloud.google.com/api-registry/docs/overview)documentation

---
<!-- Source: https://google.github.io/adk-docs/tools/google-cloud/mcp-toolbox-for-databases/ -->

# MCP Toolbox for Databases¶

# MCP Toolbox for Databases[¶](#mcp-toolbox-for-databases)

[MCP Toolbox for Databases](https://github.com/googleapis/genai-toolbox) is an
open source MCP server for databases. It was designed with enterprise-grade and
production-quality in mind. It enables you to develop tools easier, faster, and
more securely by handling the complexities such as connection pooling,
authentication, and more.

Google’s Agent Development Kit (ADK) has built in support for Toolbox. For more
information on
[getting started](https://googleapis.github.io/genai-toolbox/getting-started/) or
[configuring](https://googleapis.github.io/genai-toolbox/getting-started/configure/)
Toolbox, see the
[documentation](https://googleapis.github.io/genai-toolbox/getting-started/introduction/).

## Supported Data Sources[¶](#supported-data-sources)

MCP Toolbox provides out-of-the-box toolsets for the following databases and data platforms:

### Google Cloud[¶](#google-cloud)

[BigQuery](https://googleapis.github.io/genai-toolbox/resources/sources/bigquery/)(including tools for SQL execution, schema discovery, and AI-powered time series forecasting)[AlloyDB](https://googleapis.github.io/genai-toolbox/resources/sources/alloydb-pg/)(PostgreSQL-compatible, with tools for both standard queries and natural language queries)[AlloyDB Admin](https://googleapis.github.io/genai-toolbox/resources/sources/alloydb-admin/)[Spanner](https://googleapis.github.io/genai-toolbox/resources/sources/spanner/)(supporting both GoogleSQL and PostgreSQL dialects)- Cloud SQL (with dedicated support for
[Cloud SQL for PostgreSQL](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-sql-pg/),[Cloud SQL for MySQL](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-sql-mysql/), and[Cloud SQL for SQL Server](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-sql-mssql/)) [Cloud SQL Admin](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-sql-admin/)[Firestore](https://googleapis.github.io/genai-toolbox/resources/sources/firestore/)[Bigtable](https://googleapis.github.io/genai-toolbox/resources/sources/bigtable/)[Dataplex](https://googleapis.github.io/genai-toolbox/resources/sources/dataplex/)(for data discovery and metadata search)[Cloud Monitoring](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-monitoring/)

### Relational & SQL Databases[¶](#relational-sql-databases)

[PostgreSQL](https://googleapis.github.io/genai-toolbox/resources/sources/postgres/)(generic)[MySQL](https://googleapis.github.io/genai-toolbox/resources/sources/mysql/)(generic)[Microsoft SQL Server](https://googleapis.github.io/genai-toolbox/resources/sources/mssql/)(generic)[ClickHouse](https://googleapis.github.io/genai-toolbox/resources/sources/clickhouse/)[TiDB](https://googleapis.github.io/genai-toolbox/resources/sources/tidb/)[OceanBase](https://googleapis.github.io/genai-toolbox/resources/sources/oceanbase/)[Firebird](https://googleapis.github.io/genai-toolbox/resources/sources/firebird/)[SQLite](https://googleapis.github.io/genai-toolbox/resources/sources/sqlite/)[YugabyteDB](https://googleapis.github.io/genai-toolbox/resources/sources/yugabytedb/)

### NoSQL & Key-Value Stores[¶](#nosql-key-value-stores)

### Graph Databases[¶](#graph-databases)

### Data Platforms & Federation[¶](#data-platforms-federation)

[Looker](https://googleapis.github.io/genai-toolbox/resources/sources/looker/)(for running Looks, queries, and building dashboards via the Looker API)[Trino](https://googleapis.github.io/genai-toolbox/resources/sources/trino/)(for running federated queries across multiple sources)

### Other[¶](#other)

## Configure and deploy[¶](#configure-and-deploy)

Toolbox is an open source server that you deploy and manage yourself. For more instructions on deploying and configuring, see the official Toolbox documentation:

## Install Client SDK for ADK[¶](#install-client-sdk-for-adk)

ADK relies on the `toolbox-adk`

python package to use Toolbox. Install the
package before getting started:

### Loading Toolbox Tools[¶](#loading-toolbox-tools)

Once your Toolbox server is configured, up and running, you can load tools from your server using ADK:

from google.adk.agents import Agent
from google.adk.tools.toolbox_toolset import ToolboxToolset
toolset = ToolboxToolset(
server_url="http://127.0.0.1:5000"
)
root_agent = Agent(
...,
tools=[toolset] # Provide the toolset to the Agent
)


### Authentication[¶](#authentication)

The `ToolboxToolset`

supports various authentication strategies including Workload Identity (ADC), User Identity (OAuth2), and API Keys. For full documentation, see the [Toolbox ADK Authentication Guide](https://github.com/googleapis/mcp-toolbox-sdk-python/tree/main/packages/toolbox-adk#authentication).

**Example: Workload Identity (ADC)**

Recommended for Cloud Run, GKE, or local development with `gcloud auth login`

.

from google.adk.tools.toolbox_toolset import ToolboxToolset
from toolbox_adk import CredentialStrategy
# target_audience: The URL of your Toolbox server
creds = CredentialStrategy.workload_identity(target_audience="<TOOLBOX_URL>")
toolset = ToolboxToolset(
server_url="<TOOLBOX_URL>",
credentials=creds
)


### Advanced Configuration[¶](#advanced-configuration)

You can configure parameter binding, request hooks, and additional headers. See the [Toolbox ADK documentation](https://github.com/googleapis/mcp-toolbox-sdk-python/tree/main/packages/toolbox-adk) for details.

#### Parameter Binding[¶](#parameter-binding)

Bind values to tool parameters globally. These values are hidden from the model.

toolset = ToolboxToolset(
server_url="...",
bound_params={
"region": "us-central1",
"api_key": lambda: get_api_key() # Can be a callable
}
)


#### Usage with Hooks[¶](#usage-with-hooks)

Attach `pre_hook`

and `post_hook`

functions to execute logic before and after tool invocation.

ADK relies on the `@toolbox-sdk/adk`

TS package to use Toolbox. Install the
package before getting started:

### Loading Toolbox Tools[¶](#loading-toolbox-tools_1)

Once you’re Toolbox server is configured and up and running, you can load tools from your server using ADK:

import {InMemoryRunner, LlmAgent} from '@google/adk';
import {Content} from '@google/genai';
import {ToolboxClient} from '@toolbox-sdk/adk'
const toolboxClient = new ToolboxClient("http://127.0.0.1:5000");
const loadedTools = await toolboxClient.loadToolset();
export const rootAgent = new LlmAgent({
name: 'weather_time_agent',
model: 'gemini-2.5-flash',
description:
'Agent to answer questions about the time and weather in a city.',
instruction:
'You are a helpful agent who can answer user questions about the time and weather in a city.',
tools: loadedTools,
});
async function main() {
const userId = 'test_user';
const appName = rootAgent.name;
const runner = new InMemoryRunner({agent: rootAgent, appName});
const session = await runner.sessionService.createSession({
appName,
userId,
});
const prompt = 'What is the weather in New York? And the time?';
const content: Content = {
role: 'user',
parts: [{text: prompt}],
};
console.log(content);
for await (const e of runner.runAsync({
userId,
sessionId: session.id,
newMessage: content,
})) {
if (e.content?.parts?.[0]?.text) {
console.log(`${e.author}: ${JSON.stringify(e.content, null, 2)}`);
}
}
}
main().catch(console.error);


ADK relies on the `mcp-toolbox-sdk-go`

go module to use Toolbox. Install the
module before getting started:

### Loading Toolbox Tools[¶](#loading-toolbox-tools_2)

Once you’re Toolbox server is configured and up and running, you can load tools from your server using ADK:

package main
import (
"context"
"fmt"
"github.com/googleapis/mcp-toolbox-sdk-go/tbadk"
"google.golang.org/adk/agent/llmagent"
)
func main() {
toolboxClient, err := tbadk.NewToolboxClient("https://127.0.0.1:5000")
if err != nil {
log.Fatalf("Failed to create MCP Toolbox client: %v", err)
}
// Load a specific set of tools
toolboxtools, err := toolboxClient.LoadToolset("my-toolset-name", ctx)
if err != nil {
return fmt.Sprintln("Could not load Toolbox Toolset", err)
}
toolsList := make([]tool.Tool, len(toolboxtools))
for i := range toolboxtools {
toolsList[i] = &toolboxtools[i]
}
llmagent, err := llmagent.New(llmagent.Config{
...,
Tools: toolsList,
})
// Load a single tool
tool, err := client.LoadTool("my-tool-name", ctx)
if err != nil {
return fmt.Sprintln("Could not load Toolbox Tool", err)
}
llmagent, err := llmagent.New(llmagent.Config{
...,
Tools: []tool.Tool{&toolboxtool},
})
}


## Advanced Toolbox Features[¶](#advanced-toolbox-features)

Toolbox has a variety of features to make developing Gen AI tools for databases. For more information, read more about the following features:

[Authenticated Parameters](https://googleapis.github.io/genai-toolbox/resources/tools/#authenticated-parameters): bind tool inputs to values from OIDC tokens automatically, making it easy to run sensitive queries without potentially leaking data[Authorized Invocations:](https://googleapis.github.io/genai-toolbox/resources/tools/#authorized-invocations)restrict access to use a tool based on the users Auth token[OpenTelemetry](https://googleapis.github.io/genai-toolbox/how-to/export_telemetry/): get metrics and tracing from Toolbox with OpenTelemetry

---
<!-- Source: https://google.github.io/adk-docs/tools/google-cloud/code-exec-agent-engine/ -->

# Code Execution Tool with Agent Engine¶

# Code Execution Tool with Agent Engine[¶](#code-execution-tool-with-agent-engine)

The Agent Engine Code Execution ADK Tool provides a low-latency, highly
efficient method for running AI-generated code using the
[Google Cloud Agent Engine](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview)
service. This tool is designed for fast execution, tailored for agentic workflows,
and uses sandboxed environments for improved security. The Code Execution tool
allows code and data to persist over multiple requests, enabling complex,
multi-step coding tasks, including:

**Code development and debugging:**Create agent tasks that test and iterate on versions of code over multiple requests.**Code with data analysis:**Upload data files up to 100MB, and run multiple code-based analyses without the need to reload data for each code run.

This code execution tool is part of the Agent Engine suite, however you do not
have to deploy your agent to Agent Engine to use it. You can run your agent
locally or with other services and use this tool. For more information about the
Code Execution feature in Agent Engine, see the
[Agent Engine Code Execution](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/code-execution/overview)
documentation.

Preview release

The Agent Engine Code Execution feature is a Preview release. For
more information, see the
[launch stage descriptions](https://cloud.google.com/products#product-launch-stages).

## Use the Tool[¶](#use-the-tool)

Using the Agent Engine Code Execution tool requires that you create a sandbox environment with Google Cloud Agent Engine before using the tool with an ADK agent.

To use the Code Execution tool with your ADK agent:

- Follow the instructions in the Agent Engine
[Code Execution quickstart](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/code-execution/quickstart)to create a code execution sandbox environment. - Create an ADK agent with settings to access the Google Cloud project where you created the sandbox environment.
- The following code example shows an agent configured to use the Code
Executor tool. Replace
`SANDBOX_RESOURCE_NAME`

with the sandbox environment resource name you created.

from google.adk.agents.llm_agent import Agent
from google.adk.code_executors.agent_engine_sandbox_code_executor import AgentEngineSandboxCodeExecutor
root_agent = Agent(
model="gemini-2.5-flash",
name="agent_engine_code_execution_agent",
instruction="You are a helpful agent that can write and execute code to answer questions and solve problems.",
code_executor=AgentEngineSandboxCodeExecutor(
sandbox_resource_name="SANDBOX_RESOURCE_NAME",
),
)


For details on the expected format of the `sandbox_resource_name`

value, and the
alternative `agent_engine_resource_name`

parameter, see [Configuration
parameters](#config-parameters). For a more advanced example, including
recommended system instructions for the tool, see the [Advanced
example](#advanced-example) or the full
[agent code example](https://github.com/google/adk-python/tree/main/contributing/samples/agent_engine_code_execution).

## How it works[¶](#how-it-works)

The `AgentEngineCodeExecutor`

Tool maintains a single sandbox throughout an
agent's task, meaning the sandbox's state persists across all operations within
an ADK workflow session.

**Sandbox creation:**For multi-step tasks requiring code execution, the Agent Engine creates a sandbox with specified language and machine configurations, isolating the code execution environment. If no sandbox is pre-created, the code execution tool will automatically create one using default settings.**Code execution with persistence:**AI-generated code for a tool call is streamed to the sandbox and then executed within the isolated environment. After execution, the sandbox*remains active*for subsequent tool calls within the same session, preserving variables, imported modules, and file state for the next tool call from the same agent.**Result retrieval:**The standard output, and any captured error streams are collected and passed back to the calling agent.**Sandbox clean up:**Once the agent task or conversation concludes, the agent can explicitly delete the sandbox, or rely on the TTL feature of the sandbox specified when creating the sandbox.

## Key benefits[¶](#key-benefits)

**Persistent state:**Solve complex tasks where data manipulation or variable context must carry over between multiple tool calls.**Targeted Isolation:**Provides robust process-level isolation, ensuring that tool code execution is safe while remaining lightweight.**Agent Engine integration:**Tightly integrated into the Agent Engine tool-use and orchestration layer.**Low-latency performance:**Designed for speed, allowing agents to execute complex tool-use workflows efficiently without significant overhead.**Flexible compute configurations:**Create sandboxes with specific programming language, processing power, and memory configurations.

## System requirements¶[¶](#system-requirements)

The following requirements must be met to successfully use the Agent Engine Code Execution tool with your ADK agents:

- Google Cloud project with Vertex API enabled
- Agent's service account requires
**roles/aiplatform.user**role, which allow it to:- Create, get, list and delete code execution sandboxes
- Execute code execution sandbox


## Configuration parameters[¶](#config-parameters)

The Agent Engine Code Execution tool has the following parameters. You must set one of the following resource parameters:

: A sandbox resource path to an existing sandbox environment it uses for each tool call. The expected string format is as follows:`sandbox_resource_name`

: Agent Engine resource name where the tool creates a sandbox environment. The expected string format is as follows:`agent_engine_resource_name`


You can use Google Cloud Agent Engine's API to configure Agent Engine sandbox environments separately using a Google Cloud client connection, including the following settings:

**Programming languages,**including Python and JavaScript**Compute environment**, including CPU and memory sizes

For more information on connecting to Google Cloud Agent Engine and configuring
sandbox environments, see the Agent Engine
[Code Execution quickstart](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/code-execution/quickstart#create_a_sandbox).

## Advanced example[¶](#advanced-example)

The following example code shows how to implement use of the Code Executor tool
in an ADK agent. This example includes a `base_system_instruction`

clause to set
the operating guidelines for code execution. This instruction clause is
optional, but strongly recommended for getting the best results from this tool.

from google.adk.agents.llm_agent import Agent
from google.adk.code_executors.agent_engine_sandbox_code_executor import AgentEngineSandboxCodeExecutor
def base_system_instruction():
"""Returns: data science agent system instruction."""
return """
# Guidelines
**Objective:** Assist the user in achieving their data analysis goals, **with emphasis on avoiding assumptions and ensuring accuracy.** Reaching that goal can involve multiple steps. When you need to generate code, you **don't** need to solve the goal in one go. Only generate the next step at a time.
**Code Execution:** All code snippets provided will be executed within the sandbox environment.
**Statefulness:** All code snippets are executed and the variables stays in the environment. You NEVER need to re-initialize variables. You NEVER need to reload files. You NEVER need to re-import libraries.
**Output Visibility:** Always print the output of code execution to visualize results, especially for data exploration and analysis. For example:
- To look a the shape of a pandas.DataFrame do:
```tool_code
print(df.shape)
```
The output will be presented to you as:
```tool_outputs
(49, 7)
```
- To display the result of a numerical computation:
```tool_code
x = 10 ** 9 - 12 ** 5
print(f'{{x=}}')
```
The output will be presented to you as:
```tool_outputs
x=999751168
```
- You **never** generate ```tool_outputs yourself.
- You can then use this output to decide on next steps.
- Print just variables (e.g., `print(f'{{variable=}}')`.
**No Assumptions:** **Crucially, avoid making assumptions about the nature of the data or column names.** Base findings solely on the data itself. Always use the information obtained from `explore_df` to guide your analysis.
**Available files:** Only use the files that are available as specified in the list of available files.
**Data in prompt:** Some queries contain the input data directly in the prompt. You have to parse that data into a pandas DataFrame. ALWAYS parse all the data. NEVER edit the data that are given to you.
**Answerability:** Some queries may not be answerable with the available data. In those cases, inform the user why you cannot process their query and suggest what type of data would be needed to fulfill their request.
"""
root_agent = Agent(
model="gemini-2.5-flash",
name="agent_engine_code_execution_agent",
instruction=base_system_instruction() + """
You need to assist the user with their queries by looking at the data and the context in the conversation.
You final answer should summarize the code and code execution relevant to the user query.
You should include all pieces of data to answer the user query, such as the table from code execution results.
If you cannot answer the question directly, you should follow the guidelines above to generate the next step.
If the question can be answered directly with writing any code, you should do that.
If you doesn't have enough data to answer the question, you should ask for clarification from the user.
You should NEVER install any package on your own like `pip install ...`.
When plotting trends, you should make sure to sort and order the data by the x-axis.
""",
code_executor=AgentEngineSandboxCodeExecutor(
# Replace with your sandbox resource name if you already have one.
sandbox_resource_name="SANDBOX_RESOURCE_NAME",
# Replace with agent engine resource name used for creating sandbox if
# sandbox_resource_name is not set:
# agent_engine_resource_name="AGENT_ENGINE_RESOURCE_NAME",
),
)


For a complete version of an ADK agent using this example code, see the
[agent_engine_code_execution sample](https://github.com/google/adk-python/tree/main/contributing/samples/agent_engine_code_execution).

---
<!-- Source: https://google.github.io/adk-docs/tools/google-cloud/application-integration/ -->

# Application Integration Tools for ADK¶

# Application Integration Tools for ADK[¶](#application-integration-tools-for-adk)

With **ApplicationIntegrationToolset**, you can seamlessly give your agents
secure and governed access to enterprise applications using Integration
Connectors' 100+ pre-built connectors for systems like Salesforce, ServiceNow,
JIRA, SAP, and more.

It supports both on-premise and SaaS applications. In addition, you can turn your existing Application Integration process automations into agentic workflows by providing application integration workflows as tools to your ADK agents.

Federated search within Application Integration lets you use ADK agents to query multiple enterprise applications and data sources simultaneously.

[ See how ADK Federated Search in Application Integration works in this video walkthrough](https://www.youtube.com/watch?v=JdlWOQe5RgU)

## Prerequisites[¶](#prerequisites)

### 1. Install ADK[¶](#1-install-adk)

Install Agent Development Kit following the steps in the
[installation guide](/adk-docs/get-started/installation/).

### 2. Install CLI[¶](#2-install-cli)

Install the
[Google Cloud CLI](https://cloud.google.com/sdk/docs/install#installation_instructions).
To use the tool with default credentials, run the following commands:

gcloud config set project <project-id>
gcloud auth application-default login
gcloud auth application-default set-quota-project <project-id>


Replace `<project-id>`

with the unique ID of your Google Cloud project.

### 3. Provision Application Integration workflow and publish Connection Tool[¶](#3-provision-application-integration-workflow-and-publish-connection-tool)

Use an existing
[Application Integration](https://cloud.google.com/application-integration/docs/overview)
workflow or
[Integrations Connector](https://cloud.google.com/integration-connectors/docs/overview)
connection you want to use with your agent. You can also create a new
[Application Integration workflow](https://cloud.google.com/application-integration/docs/setup-application-integration)
or a
[connection](https://cloud.google.com/integration-connectors/docs/connectors/neo4j/configure#configure-the-connector).

Import and publish the
[Connection Tool](https://console.cloud.google.com/integrations/templates/connection-tool/locations/global)
from the template library.

**Note**: To use a connector from Integration Connectors, you need to provision
the Application Integration in the same region as your connection.

### 4. Create project structure[¶](#4-create-project-structure)

Set up your project structure and create the required files:

When running the agent, make sure to run `adk web`

from the `project_root_folder`

.

### 5. Set roles and permissions[¶](#5-set-roles-and-permissions)

To get the permissions that you need to set up
**ApplicationIntegrationToolset**, you must have the following IAM roles on the
project (common to both Integration Connectors and Application Integration
Workflows):

```
- roles/integrations.integrationEditor
- roles/connectors.invoker
- roles/secretmanager.secretAccessor
```


**Note:** When using Agent Engine (AE) for deployment, don't use
`roles/integrations.integrationInvoker`

, as it can result in 403 errors. Use
`roles/integrations.integrationEditor`

instead.

## Use Integration Connectors[¶](#use-integration-connectors)

Connect your agent to enterprise applications using
[Integration Connectors](https://cloud.google.com/integration-connectors/docs/overview).

### Before you begin[¶](#before-you-begin)

**Note:** The *ExecuteConnection* integration is typically created automatically when you provision Application Integration in a given region. If the *ExecuteConnection* doesn't exist in the [list of integrations](https://console.cloud.google.com/integrations/list), you must follow these steps to create it:

- To use a connector from Integration Connectors, click
**QUICK SETUP**and[provision](https://console.cloud.google.com/integrations)Application Integration in the same region as your connection.

-
Go to the

[Connection Tool](https://console.cloud.google.com/integrations/templates/connection-tool/locations/us-central1)template in the template library and click**USE TEMPLATE**. -
Enter the Integration Name as

*ExecuteConnection*(it is mandatory to use this exact integration name only). Then, select the region to match your connection region and click**CREATE**. -
Click

**PUBLISH**to publish the integration in the*Application Integration*editor.

### Create an Application Integration Toolset[¶](#create-an-application-integration-toolset)

To create an Application Integration Toolset for Integration Connectors, follow these steps:

-
Create a tool with

`ApplicationIntegrationToolset`

in the`tools.py`

file:[from google.adk.tools.application_integration_tool.application_integration_toolset import ApplicationIntegrationToolset](#__codelineno-3-1)[connector_tool = ApplicationIntegrationToolset(](#__codelineno-3-3)[project="test-project", # TODO: replace with GCP project of the connection](#__codelineno-3-4)[location="us-central1", #TODO: replace with location of the connection](#__codelineno-3-5)[connection="test-connection", #TODO: replace with connection name](#__codelineno-3-6)[entity_operations={"Entity_One": ["LIST","CREATE"], "Entity_Two": []},#empty list for actions means all operations on the entity are supported.](#__codelineno-3-7)[actions=["action1"], #TODO: replace with actions](#__codelineno-3-8)[service_account_json='{...}', # optional. Stringified json for service account key](#__codelineno-3-9)[tool_name_prefix="tool_prefix2",](#__codelineno-3-10)[tool_instructions="..."](#__codelineno-3-11)[)](#__codelineno-3-12)**Note:**- You can provide a service account to be used instead of default credentials by generating a
[Service Account Key](https://cloud.google.com/iam/docs/keys-create-delete#creating), and providing the right[Application Integration and Integration Connector IAM roles](#prerequisites)to the service account. - To find the list of supported entities and actions for a connection, use the Connectors APIs:
[listActions](https://cloud.google.com/integration-connectors/docs/reference/rest/v1/projects.locations.connections.connectionSchemaMetadata/listActions)or[listEntityTypes](https://cloud.google.com/integration-connectors/docs/reference/rest/v1/projects.locations.connections.connectionSchemaMetadata/listEntityTypes).

`ApplicationIntegrationToolset`

supports`auth_scheme`

and`auth_credential`

for**dynamic OAuth2 authentication**for Integration Connectors. To use it, create a tool similar to this in the`tools.py`

file:[from google.adk.tools.application_integration_tool.application_integration_toolset import ApplicationIntegrationToolset](#__codelineno-4-1)[from google.adk.tools.openapi_tool.auth.auth_helpers import dict_to_auth_scheme](#__codelineno-4-2)[from google.adk.auth import AuthCredential](#__codelineno-4-3)[from google.adk.auth import AuthCredentialTypes](#__codelineno-4-4)[from google.adk.auth import OAuth2Auth](#__codelineno-4-5)[oauth2_data_google_cloud = {](#__codelineno-4-7)["type": "oauth2",](#__codelineno-4-8)["flows": {](#__codelineno-4-9)["authorizationCode": {](#__codelineno-4-10)["authorizationUrl": "https://accounts.google.com/o/oauth2/auth",](#__codelineno-4-11)["tokenUrl": "https://oauth2.googleapis.com/token",](#__codelineno-4-12)["scopes": {](#__codelineno-4-13)["https://www.googleapis.com/auth/cloud-platform": (](#__codelineno-4-14)["View and manage your data across Google Cloud Platform"](#__codelineno-4-15)[" services"](#__codelineno-4-16)[),](#__codelineno-4-17)["https://www.googleapis.com/auth/calendar.readonly": "View your calendars"](#__codelineno-4-18)[},](#__codelineno-4-19)[}](#__codelineno-4-20)[},](#__codelineno-4-21)[}](#__codelineno-4-22)[oauth_scheme = dict_to_auth_scheme(oauth2_data_google_cloud)](#__codelineno-4-24)[auth_credential = AuthCredential(](#__codelineno-4-26)[auth_type=AuthCredentialTypes.OAUTH2,](#__codelineno-4-27)[oauth2=OAuth2Auth(](#__codelineno-4-28)[client_id="...", #TODO: replace with client_id](#__codelineno-4-29)[client_secret="...", #TODO: replace with client_secret](#__codelineno-4-30)[),](#__codelineno-4-31)[)](#__codelineno-4-32)[connector_tool = ApplicationIntegrationToolset(](#__codelineno-4-34)[project="test-project", # TODO: replace with GCP project of the connection](#__codelineno-4-35)[location="us-central1", #TODO: replace with location of the connection](#__codelineno-4-36)[connection="test-connection", #TODO: replace with connection name](#__codelineno-4-37)[entity_operations={"Entity_One": ["LIST","CREATE"], "Entity_Two": []},#empty list for actions means all operations on the entity are supported.](#__codelineno-4-38)[actions=["GET_calendars/%7BcalendarId%7D/events"], #TODO: replace with actions. this one is for list events](#__codelineno-4-39)[service_account_json='{...}', # optional. Stringified json for service account key](#__codelineno-4-40)[tool_name_prefix="tool_prefix2",](#__codelineno-4-41)[tool_instructions="...",](#__codelineno-4-42)[auth_scheme=oauth_scheme,](#__codelineno-4-43)[auth_credential=auth_credential](#__codelineno-4-44)[)](#__codelineno-4-45) - You can provide a service account to be used instead of default credentials by generating a
-
Update the

`agent.py`

file and add tool to your agent: -
Configure

`__init__.py`

to expose your agent: -
Start the Google ADK Web UI and use your agent:


After completing the above steps, go to [http://localhost:8000](http://localhost:8000), and choose
`my\_agent`

agent (which is the same as the agent folder name).

## Use Application Integration Workflows[¶](#use-application-integration-workflows)

Use an existing
[Application Integration](https://cloud.google.com/application-integration/docs/overview)
workflow as a tool for your agent or create a new one.

### 1. Create a tool[¶](#1-create-a-tool)

To create a tool with `ApplicationIntegrationToolset`

in the `tools.py`

file, use the following code:

integration_tool = ApplicationIntegrationToolset(
project="test-project", # TODO: replace with GCP project of the connection
location="us-central1", #TODO: replace with location of the connection
integration="test-integration", #TODO: replace with integration name
triggers=["api_trigger/test_trigger"],#TODO: replace with trigger id(s). Empty list would mean all api triggers in the integration to be considered.
service_account_json='{...}', #optional. Stringified json for service account key
tool_name_prefix="tool_prefix1",
tool_instructions="..."
)


**Note:** You can provide a service account to be used instead of using default credentials. To do this, generate a [Service Account Key](https://cloud.google.com/iam/docs/keys-create-delete#creating) and provide the correct
[Application Integration and Integration Connector IAM roles](#prerequisites) to the service account. For more details about the IAM roles, refer to the [Prerequisites](#prerequisites) section.

To create a tool with `ApplicationIntegrationToolset`

in the `tools.java`

file, use the following code:

import com.google.adk.tools.applicationintegrationtoolset.ApplicationIntegrationToolset;
import com.google.common.collect.ImmutableList;
import com.google.common.collect.ImmutableMap;
public class Tools {
private static ApplicationIntegrationToolset integrationTool;
private static ApplicationIntegrationToolset connectionsTool;
static {
integrationTool = new ApplicationIntegrationToolset(
"test-project",
"us-central1",
"test-integration",
ImmutableList.of("api_trigger/test-api"),
null,
null,
null,
"{...}",
"tool_prefix1",
"...");
connectionsTool = new ApplicationIntegrationToolset(
"test-project",
"us-central1",
null,
null,
"test-connection",
ImmutableMap.of("Issue", ImmutableList.of("GET")),
ImmutableList.of("ExecuteCustomQuery"),
"{...}",
"tool_prefix",
"...");
}
}


**Note:** You can provide a service account to be used instead of using default credentials. To do this, generate a [Service Account Key](https://cloud.google.com/iam/docs/keys-create-delete#creating) and provide the correct [Application Integration and Integration Connector IAM roles](#prerequisites) to the service account. For more details about the IAM roles, refer to the [Prerequisites](#prerequisites) section.

### 2. Add the tool to your agent[¶](#2-add-the-tool-to-your-agent)

To update the `agent.py`

file and add the tool to your agent, use the following code:

To update the `agent.java`

file and add the tool to your agent, use the following code:

```java import com.google.adk.agent.LlmAgent; import com.google.adk.tools.BaseTool; import com.google.common.collect.ImmutableList;

```
public class MyAgent {
public static void main(String[] args) {
// Assuming Tools class is defined as in the previous step
ImmutableList<BaseTool> tools = ImmutableList.<BaseTool>builder()
.add(Tools.integrationTool)
.add(Tools.connectionsTool)
.build();
// Finally, create your agent with the tools generated automatically.
LlmAgent rootAgent = LlmAgent.builder()
.name("science-teacher")
.description("Science teacher agent")
.model("gemini-2.0-flash")
.instruction(
"Help user, leverage the tools you have access to."
)
.tools(tools)
.build();
// You can now use rootAgent to interact with the LLM
// For example, you can start a conversation with the agent.
}
}
```
```


**Note:** To find the list of supported entities and actions for a
connection, use these Connector APIs: `listActions`

, `listEntityTypes`

.

### 3. Expose your agent[¶](#3-expose-your-agent)

### 4. Use your agent[¶](#4-use-your-agent)

To start the Google ADK Web UI and use your agent, use the following commands:

After completing the above steps, go to[http://localhost:8000](http://localhost:8000), and choose the

`my_agent`

agent (which is the same as the agent folder name).
To start the Google ADK Web UI and use your agent, use the following commands:

mvn install
mvn exec:java \
-Dexec.mainClass="com.google.adk.web.AdkWebServer" \
-Dexec.args="--adk.agents.source-dir=src/main/java" \
-Dexec.classpathScope="compile"


After completing the above steps, go to [http://localhost:8000](http://localhost:8000), and choose the `my_agent`

agent (which is the same as the agent folder name).
