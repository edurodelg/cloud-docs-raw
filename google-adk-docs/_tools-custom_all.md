---
merged_at: 2026-01-28T07:23:42.191386
merged_files: 7
---


---
<!-- Source: https://google.github.io/adk-docs/tools-custom/performance/ -->

# Increase tool performance with parallel execution¶

# Increase tool performance with parallel execution[¶](#increase-tool-performance-with-parallel-execution)

Starting with Agent Development Kit (ADK) version 1.10.0 for Python, the framework
attempts to run any agent-requested
[function tools](/adk-docs/tools-custom/function-tools/)
in parallel. This behavior can significantly improve the performance and
responsiveness of your agents, particularly for agents that rely on multiple
external APIs or long-running tasks. For example, if you have 3 tools that each
take 2 seconds, by running them in parallel, the total execution time will be
closer to 2 seconds, instead of 6 seconds. The ability to run tool functions
parallel can improve the performance of your agents, particularly in the
following scenarios:

**Research tasks:**Where the agent collects information from multiple sources before proceeding to the next stage of the workflow.**API calls:**Where the agent accesses several APIs independently, such as searching for available flights using APIs from multiple airlines.**Publishing and communication tasks:**When the agent needs to publish or communicate through multiple, independent channels or multiple recipients.

However, your custom tools must be built with asynchronous execution support to enable this performance improvement. This guide explains how parallel tool execution works in the ADK and how to build your tools to take full advantage of this processing feature.

Warning

Any ADK Tools that use synchronous processing in a set of tool function calls will block other tools from executing in parallel, even if the other tools allow for parallel execution.

## Build parallel-ready tools[¶](#build-parallel-ready-tools)

Enable parallel execution of your tool functions by defining them as
asynchronous functions. In Python code, this means using `async def`

and `await`

syntax which allows the ADK to run them concurrently in an `asyncio`

event loop.
The following sections show examples of agent tools built for parallel
processing and asynchronous operations.

### Example of http web call[¶](#example-of-http-web-call)

The following code example show how to modify the `get_weather()`

function to
operate asynchronously and allow for parallel execution:

async def get_weather(city: str) -> dict:
async with aiohttp.ClientSession() as session:
async with session.get(f"http://api.weather.com/{city}") as response:
return await response.json()


### Example of database call[¶](#example-of-database-call)

The following code example show how to write a database calling function to operate asynchronously:

async def query_database(query: str) -> list:
async with asyncpg.connect("postgresql://...") as conn:
return await conn.fetch(query)


### Example of yielding behavior for long loops[¶](#example-of-yielding-behavior-for-long-loops)

In cases where a tool is processing multiple requests or numerous long-running requests, consider adding yielding code to allow other tools to execute, as shown in the following code sample:

async def process_data(data: list) -> dict:
results = []
for i, item in enumerate(data):
processed = await process_item(item) # Yield point
results.append(processed)
# Add periodic yield points for long loops
if i % 100 == 0:
await asyncio.sleep(0) # Yield control
return {"results": results}


Important

Use the `asyncio.sleep()`

function for pauses to avoid blocking
execution of other functions.

### Example of thread pools for intensive operations[¶](#example-of-thread-pools-for-intensive-operations)

When performing processing-intensive functions, consider creating thread pools for better management of available computing resources, as shown in the following example:

async def cpu_intensive_tool(data: list) -> dict:
loop = asyncio.get_event_loop()
# Use thread pool for CPU-bound work
with ThreadPoolExecutor() as executor:
result = await loop.run_in_executor(
executor,
expensive_computation,
data
)
return {"result": result}


### Example of process chunking[¶](#example-of-process-chunking)

When performing processes on long lists or large amounts of data, consider combining a thread pool technique with dividing up processing into chunks of data, and yielding processing time between the chunks, as shown in the following example:

async def process_large_dataset(dataset: list) -> dict:
results = []
chunk_size = 1000
for i in range(0, len(dataset), chunk_size):
chunk = dataset[i:i + chunk_size]
# Process chunk in thread pool
loop = asyncio.get_event_loop()
with ThreadPoolExecutor() as executor:
chunk_result = await loop.run_in_executor(
executor, process_chunk, chunk
)
results.extend(chunk_result)
# Yield control between chunks
await asyncio.sleep(0)
return {"total_processed": len(results), "results": results}


## Write parallel-ready prompts and tool descriptions[¶](#write-parallel-ready-prompts-and-tool-descriptions)

When building prompts for AI models, consider explicitly specifying or hinting that function calls be made in parallel. The following example of an AI prompt directs the model to use tools in parallel:

When users ask for multiple pieces of information, always call functions in
parallel.
Examples:
- "Get weather for London and currency rate USD to EUR" → Call both functions
simultaneously
- "Compare cities A and B" → Call get_weather, get_population, get_distance in
parallel
- "Analyze multiple stocks" → Call get_stock_price for each stock in parallel
Always prefer multiple specific function calls over single complex calls.


The following example shows a tool function description that hints at more efficient use through parallel execution:

async def get_weather(city: str) -> dict:
"""Get current weather for a single city.
This function is optimized for parallel execution - call multiple times for different cities.
Args:
city: Name of the city, for example: 'London', 'New York'
Returns:
Weather data including temperature, conditions, humidity
"""
await asyncio.sleep(2) # Simulate API call
return {"city": city, "temp": 72, "condition": "sunny"}


## Next steps[¶](#next-steps)

For more information on building Tools for agents and function calling, see
[Function Tools](/adk-docs/tools-custom/function-tools/). For
more detailed examples of tools that take advantage of parallel processing, see
the samples in the
[adk-python](https://github.com/google/adk-python/tree/main/contributing/samples/parallel_functions)
repository.

---
<!-- Source: https://google.github.io/adk-docs/tools-custom/confirmation/ -->

# Get action confirmation for ADK Tools¶

# Get action confirmation for ADK Tools[¶](#get-action-confirmation-for-adk-tools)

Some agent workflows require confirmation for decision making, verification,
security, or general oversight. In these cases, you want to get a response from
a human or supervising system before proceeding with a workflow. The *Tool
Confirmation* feature in the Agent Development Kit (ADK) allows an ADK Tool to
pause its execution and interact with a user or other system for confirmation or
to gather structured data before proceeding. You can use Tool Confirmation with
an ADK Tool in the following ways:

You can configure a FunctionTool with a[Boolean Confirmation](#boolean-confirmation):`require_confirmation`

parameter. This option pauses the tool for a yes or no confirmation response.For scenarios requiring structured data responses, you can configure a[Advanced Confirmation](#advanced-confirmation):`FunctionTool`

with a text prompt to explain the confirmation and an expected response.

Experimental

The Tool Confirmation feature is experimental and has some
[known limitations](#known-limitations).
We welcome your
[feedback](https://github.com/google/adk-python/issues/new?template=feature_request.md&labels=tool%20confirmation)!

You can configure how a request is communicated to a user, and the system can
also use [remote responses](#remote-response) sent via the ADK
server's REST API. When using the confirmation feature with the ADK web user
interface, the agent workflow displays a dialog box to the user to request
input, as shown in Figure 1:

**Figure 1.** Example confirmation response request dialog box using an
advanced, tool response implementation.

The following sections describe how to use this feature for the confirmation
scenarios. For a complete code sample, see the
[human_tool_confirmation](https://github.com/google/adk-python/blob/fc90ce968f114f84b14829f8117797a4c256d710/contributing/samples/human_tool_confirmation/agent.py)
example. There are additional ways to incorporate human input into your agent
workflow, for more details, see the
[Human-in-the-loop](/adk-docs/agents/multi-agents/#human-in-the-loop-pattern)
agent pattern.

## Boolean confirmation[¶](#boolean-confirmation)

When your tool only requires a simple `yes`

or `no`

from the user, you can
append a confirmation step using the `FunctionTool`

class as a wrapper. For
example, if you have a tool called `reimburse`

, you can enable a confirmation
step by wrapping it with the `FunctionTool`

class and setting the
`require_confirmation`

parameter to `True`

, as shown in the following example:

# From agent.py
root_agent = Agent(
...
tools=[
# Set require_confirmation to True to require user confirmation
# for the tool call.
FunctionTool(reimburse, require_confirmation=True),
],
...


This implementation method requires minimal code, but is limited to simple
approvals from the user or confirming system. For a complete example of this
approach, see the
[human_tool_confirmation](https://github.com/google/adk-python/blob/fc90ce968f114f84b14829f8117797a4c256d710/contributing/samples/human_tool_confirmation/agent.py)
code sample.

### Require confirmation function[¶](#require-confirmation-function)

You can modify the behavior `require_confirmation`

response by replacing its
input value with a function that returns a boolean response. The following
example shows a function for determining if a confirmation is required:

async def confirmation_threshold(
amount: int, tool_context: ToolContext
) -> bool:
"""Returns true if the amount is greater than 1000."""
return amount > 1000


This function than then be set as the parameter value for the
`require_confirmation`

parameter:

root_agent = Agent(
...
tools=[
# Set require_confirmation to True to require user confirmation
FunctionTool(reimburse, require_confirmation=confirmation_threshold),
],
...


For a complete example of this implementation, see the
[human_tool_confirmation](https://github.com/google/adk-python/blob/fc90ce968f114f84b14829f8117797a4c256d710/contributing/samples/human_tool_confirmation/agent.py)
code sample.

## Advanced confirmation[¶](#advanced-confirmation)

When a tool confirmation requires more details for the user or a more complex
response, use a tool_confirmation implementation. This approach extends the
`ToolContext`

object to add a text description of the request for the user and
allows for more complex response data. When implementing tool confirmation this
way, you can pause a tool's execution, request specific information, and then
resume the tool with the provided data.

This confirmation flow has a request stage where the system assembles and sends an input request human response, and a response stage where the system receives and processes the returned data.

### Confirmation definition[¶](#confirmation-definition)

When creating a Tool with an advanced confirmation, create a function that
includes a ToolContext object. Then define the confirmation using a
tool_confirmation object, the `tool_context.request_confirmation()`

method with
`hint`

and `payload`

parameters. These properties are used as follows:

`hint`

: Descriptive message that explains what is needed from the user.`payload`

: The structure of the data you expect in return. This data type is Any and must be serializable into a JSON-formatted string, such as a dictionary or pydantic model.

The following code shows an example implementation for a tool that processes time off requests for an employee:

def request_time_off(days: int, tool_context: ToolContext):
"""Request day off for the employee."""
...
tool_confirmation = tool_context.tool_confirmation
if not tool_confirmation:
tool_context.request_confirmation(
hint=(
'Please approve or reject the tool call request_time_off() by'
' responding with a FunctionResponse with an expected'
' ToolConfirmation payload.'
),
payload={
'approved_days': 0,
},
)
# Return intermediate status indicating that the tool is waiting for
# a confirmation response:
return {'status': 'Manager approval is required.'}
approved_days = tool_confirmation.payload['approved_days']
approved_days = min(approved_days, days)
if approved_days == 0:
return {'status': 'The time off request is rejected.', 'approved_days': 0}
return {
'status': 'ok',
'approved_days': approved_days,
}


For a complete example of this approach, see the
[human_tool_confirmation](https://github.com/google/adk-python/blob/fc90ce968f114f84b14829f8117797a4c256d710/contributing/samples/human_tool_confirmation/agent.py)
code sample. Keep in mind that the agent workflow tool execution pauses while a
confirmation is obtained. After confirmation is received, you can access the
confirmation response in the `tool_confirmation.payload`

object and then proceed
with the execution of the workflow.

## Remote confirmation with REST API[¶](#remote-response)

If there is no active user interface for a human confirmation of an agent
workflow, you can handle the confirmation through a command-line interface or by
routing it through another channel like email or a chat application. To confirm
the tool call, the user or calling application needs to send a
`FunctionResponse`

event with the tool confirmation data.

You can send the request to the ADK API server's `/run`

or `/run_sse`

endpoint,
or directly to the ADK runner. The following example uses a `curl`

command to
send the confirmation to the `/run_sse`

endpoint:

curl -X POST http://localhost:8000/run_sse \
-H "Content-Type: application/json" \
-d '{
"app_name": "human_tool_confirmation",
"user_id": "user",
"session_id": "7828f575-2402-489f-8079-74ea95b6a300",
"new_message": {
"parts": [
{
"function_response": {
"id": "adk-13b84a8c-c95c-4d66-b006-d72b30447e35",
"name": "adk_request_confirmation",
"response": {
"confirmed": true
}
}
}
],
"role": "user"
}
}'


A REST-based response for a confirmation must meet the following requirements:

- The
`id`

in the`function_response`

should match the`function_call_id`

from the`RequestConfirmation`

`FunctionCall`

event. - The
`name`

should be`adk_request_confirmation`

. - The
`response`

object contains the confirmation status and any additional payload data required by the tool.

Note: Confirmation with Resume feature

If your ADK agent workflow is configured with the
[Resume](/adk-docs/runtime/resume/) feature, you also must include
the Invocation ID (`invocation_id`

) parameter with the confirmation
response. The Invocation ID you provide must be the same invocation
that generated the confirmation request, otherwise the system
starts a new invocation with the confirmation response. If your
agent uses the Resume feature, consider including the Invocation ID
as a parameter with your confirmation request, so it can be
included with the response. For more details on using the Resume
feature, see
[Resume stopped agents](/adk-docs/runtime/resume/).

## Known limitations[¶](#known-limitations)

The tool confirmation feature has the following limitations:

[DatabaseSessionService](/adk-docs/api-reference/python/google-adk.html#google.adk.sessions.DatabaseSessionService)is not supported by this feature.[VertexAiSessionService](/adk-docs/api-reference/python/google-adk.html#google.adk.sessions.VertexAiSessionService)is not supported by this feature.

## Next steps[¶](#next-steps)

For more information on building ADK tools for agent workflows, see [Function
tools](/adk-docs/tools-custom/function-tools/).

---
<!-- Source: https://google.github.io/adk-docs/tools-custom/openapi-tools/ -->

# Integrate REST APIs with OpenAPI¶

# Integrate REST APIs with OpenAPI[¶](#integrate-rest-apis-with-openapi)

ADK simplifies interacting with external REST APIs by automatically generating callable tools directly from an [OpenAPI Specification (v3.x)](https://swagger.io/specification/). This eliminates the need to manually define individual function tools for each API endpoint.

Core Benefit

Use `OpenAPIToolset`

to instantly create agent tools (`RestApiTool`

) from your existing API documentation (OpenAPI spec), enabling agents to seamlessly call your web services.

## Key Components[¶](#key-components)

: This is the primary class you'll use. You initialize it with your OpenAPI specification, and it handles the parsing and generation of tools.`OpenAPIToolset`

: This class represents a single, callable API operation (like`RestApiTool`

`GET /pets/{petId}`

or`POST /pets`

).`OpenAPIToolset`

creates one`RestApiTool`

instance for each operation defined in your spec.

## How it Works[¶](#how-it-works)

The process involves these main steps when you use `OpenAPIToolset`

:

-
**Initialization & Parsing**:- You provide the OpenAPI specification to
`OpenAPIToolset`

either as a Python dictionary, a JSON string, or a YAML string. - The toolset internally parses the spec, resolving any internal references (
`$ref`

) to understand the complete API structure.

- You provide the OpenAPI specification to
-
**Operation Discovery**:- It identifies all valid API operations (e.g.,
`GET`

,`POST`

,`PUT`

,`DELETE`

) defined within the`paths`

object of your specification.

- It identifies all valid API operations (e.g.,
-
**Tool Generation**:- For each discovered operation,
`OpenAPIToolset`

automatically creates a corresponding`RestApiTool`

instance. **Tool Name**: Derived from the`operationId`

in the spec (converted to`snake_case`

, max 60 chars). If`operationId`

is missing, a name is generated from the method and path.**Tool Description**: Uses the`summary`

or`description`

from the operation for the LLM.**API Details**: Stores the required HTTP method, path, server base URL, parameters (path, query, header, cookie), and request body schema internally.

- For each discovered operation,
-
: Each generated`RestApiTool`

Functionality`RestApiTool`

:**Schema Generation**: Dynamically creates a`FunctionDeclaration`

based on the operation's parameters and request body. This schema tells the LLM how to call the tool (what arguments are expected).**Execution**: When called by the LLM, it constructs the correct HTTP request (URL, headers, query params, body) using the arguments provided by the LLM and the details from the OpenAPI spec. It handles authentication (if configured) and executes the API call using the`requests`

library.**Response Handling**: Returns the API response (typically JSON) back to the agent flow.

-
**Authentication**: You can configure global authentication (like API keys or OAuth - see[Authentication](/adk-docs/tools/authentication/)for details) when initializing`OpenAPIToolset`

. This authentication configuration is automatically applied to all generated`RestApiTool`

instances.

## Usage Workflow[¶](#usage-workflow)

Follow these steps to integrate an OpenAPI spec into your agent:

**Obtain Spec**: Get your OpenAPI specification document (e.g., load from a`.json`

or`.yaml`

file, fetch from a URL).-
**Instantiate Toolset**: Create an`OpenAPIToolset`

instance, passing the spec content and type (`spec_str`

/`spec_dict`

,`spec_str_type`

). Provide authentication details (`auth_scheme`

,`auth_credential`

) if required by the API.[from google.adk.tools.openapi_tool.openapi_spec_parser.openapi_toolset import OpenAPIToolset](#__codelineno-0-1)[# Example with a JSON string](#__codelineno-0-3)[openapi_spec_json = '...' # Your OpenAPI JSON string](#__codelineno-0-4)[toolset = OpenAPIToolset(spec_str=openapi_spec_json, spec_str_type="json")](#__codelineno-0-5)[# Example with a dictionary](#__codelineno-0-7)[# openapi_spec_dict = {...} # Your OpenAPI spec as a dict](#__codelineno-0-8)[# toolset = OpenAPIToolset(spec_dict=openapi_spec_dict)](#__codelineno-0-9) -
**Add to Agent**: Include the retrieved tools in your`LlmAgent`

's`tools`

list. -
**Instruct Agent**: Update your agent's instructions to inform it about the new API capabilities and the names of the tools it can use (e.g.,`list_pets`

,`create_pet`

). The tool descriptions generated from the spec will also help the LLM. **Run Agent**: Execute your agent using the`Runner`

. When the LLM determines it needs to call one of the APIs, it will generate a function call targeting the appropriate`RestApiTool`

, which will then handle the HTTP request automatically.

## Example[¶](#example)

This example demonstrates generating tools from a simple Pet Store OpenAPI spec (using `httpbin.org`

for mock responses) and interacting with them via an agent.

## Code: Pet Store API

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
import uuid # For unique session IDs
from dotenv import load_dotenv
from google.adk.agents import LlmAgent
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.genai import types
# --- OpenAPI Tool Imports ---
from google.adk.tools.openapi_tool.openapi_spec_parser.openapi_toolset import OpenAPIToolset
# --- Load Environment Variables (If ADK tools need them, e.g., API keys) ---
load_dotenv() # Create a .env file in the same directory if needed
# --- Constants ---
APP_NAME_OPENAPI = "openapi_petstore_app"
USER_ID_OPENAPI = "user_openapi_1"
SESSION_ID_OPENAPI = f"session_openapi_{uuid.uuid4()}" # Unique session ID
AGENT_NAME_OPENAPI = "petstore_manager_agent"
GEMINI_MODEL = "gemini-2.0-flash"
# --- Sample OpenAPI Specification (JSON String) ---
# A basic Pet Store API example using httpbin.org as a mock server
openapi_spec_string = """
{
"openapi": "3.0.0",
"info": {
"title": "Simple Pet Store API (Mock)",
"version": "1.0.1",
"description": "An API to manage pets in a store, using httpbin for responses."
},
"servers": [
{
"url": "https://httpbin.org",
"description": "Mock server (httpbin.org)"
}
],
"paths": {
"/get": {
"get": {
"summary": "List all pets (Simulated)",
"operationId": "listPets",
"description": "Simulates returning a list of pets. Uses httpbin's /get endpoint which echoes query parameters.",
"parameters": [
{
"name": "limit",
"in": "query",
"description": "Maximum number of pets to return",
"required": false,
"schema": { "type": "integer", "format": "int32" }
},
{
"name": "status",
"in": "query",
"description": "Filter pets by status",
"required": false,
"schema": { "type": "string", "enum": ["available", "pending", "sold"] }
}
],
"responses": {
"200": {
"description": "A list of pets (echoed query params).",
"content": { "application/json": { "schema": { "type": "object" } } }
}
}
}
},
"/post": {
"post": {
"summary": "Create a pet (Simulated)",
"operationId": "createPet",
"description": "Simulates adding a new pet. Uses httpbin's /post endpoint which echoes the request body.",
"requestBody": {
"description": "Pet object to add",
"required": true,
"content": {
"application/json": {
"schema": {
"type": "object",
"required": ["name"],
"properties": {
"name": {"type": "string", "description": "Name of the pet"},
"tag": {"type": "string", "description": "Optional tag for the pet"}
}
}
}
}
},
"responses": {
"201": {
"description": "Pet created successfully (echoed request body).",
"content": { "application/json": { "schema": { "type": "object" } } }
}
}
}
},
"/get?petId={petId}": {
"get": {
"summary": "Info for a specific pet (Simulated)",
"operationId": "showPetById",
"description": "Simulates returning info for a pet ID. Uses httpbin's /get endpoint.",
"parameters": [
{
"name": "petId",
"in": "path",
"description": "This is actually passed as a query param to httpbin /get",
"required": true,
"schema": { "type": "integer", "format": "int64" }
}
],
"responses": {
"200": {
"description": "Information about the pet (echoed query params)",
"content": { "application/json": { "schema": { "type": "object" } } }
},
"404": { "description": "Pet not found (simulated)" }
}
}
}
}
}
"""
# --- Create OpenAPIToolset ---
petstore_toolset = OpenAPIToolset(
spec_str=openapi_spec_string,
spec_str_type='json',
# No authentication needed for httpbin.org
)
# --- Agent Definition ---
root_agent = LlmAgent(
name=AGENT_NAME_OPENAPI,
model=GEMINI_MODEL,
tools=[petstore_toolset], # Pass the list of RestApiTool objects
instruction="""You are a Pet Store assistant managing pets via an API.
Use the available tools to fulfill user requests.
When creating a pet, confirm the details echoed back by the API.
When listing pets, mention any filters used (like limit or status).
When showing a pet by ID, state the ID you requested.
""",
description="Manages a Pet Store using tools generated from an OpenAPI spec."
)
# --- Session and Runner Setup ---
async def setup_session_and_runner():
session_service_openapi = InMemorySessionService()
runner_openapi = Runner(
agent=root_agent,
app_name=APP_NAME_OPENAPI,
session_service=session_service_openapi,
)
await session_service_openapi.create_session(
app_name=APP_NAME_OPENAPI,
user_id=USER_ID_OPENAPI,
session_id=SESSION_ID_OPENAPI,
)
return runner_openapi
# --- Agent Interaction Function ---
async def call_openapi_agent_async(query, runner_openapi):
print("\n--- Running OpenAPI Pet Store Agent ---")
print(f"Query: {query}")
content = types.Content(role='user', parts=[types.Part(text=query)])
final_response_text = "Agent did not provide a final text response."
try:
async for event in runner_openapi.run_async(
user_id=USER_ID_OPENAPI, session_id=SESSION_ID_OPENAPI, new_message=content
):
# Optional: Detailed event logging for debugging
# print(f" DEBUG Event: Author={event.author}, Type={'Final' if event.is_final_response() else 'Intermediate'}, Content={str(event.content)[:100]}...")
if event.get_function_calls():
call = event.get_function_calls()[0]
print(f" Agent Action: Called function '{call.name}' with args {call.args}")
elif event.get_function_responses():
response = event.get_function_responses()[0]
print(f" Agent Action: Received response for '{response.name}'")
# print(f" Tool Response Snippet: {str(response.response)[:200]}...") # Uncomment for response details
elif event.is_final_response() and event.content and event.content.parts:
# Capture the last final text response
final_response_text = event.content.parts[0].text.strip()
print(f"Agent Final Response: {final_response_text}")
except Exception as e:
print(f"An error occurred during agent run: {e}")
import traceback
traceback.print_exc() # Print full traceback for errors
print("-" * 30)
# --- Run Examples ---
async def run_openapi_example():
runner_openapi = await setup_session_and_runner()
# Trigger listPets
await call_openapi_agent_async("Show me the pets available.", runner_openapi)
# Trigger createPet
await call_openapi_agent_async("Please add a new dog named 'Dukey'.", runner_openapi)
# Trigger showPetById
await call_openapi_agent_async("Get info for pet with ID 123.", runner_openapi)
# --- Execute ---
if __name__ == "__main__":
print("Executing OpenAPI example...")
# Use asyncio.run() for top-level execution
try:
asyncio.run(run_openapi_example())
except RuntimeError as e:
if "cannot be called from a running event loop" in str(e):
print("Info: Cannot run asyncio.run from a running event loop (e.g., Jupyter/Colab).")
# If in Jupyter/Colab, you might need to run like this:
# await run_openapi_example()
else:
raise e
print("OpenAPI example finished.")

---
<!-- Source: https://google.github.io/adk-docs/tools-custom/authentication/ -->

# Authenticating with Tools¶

# Authenticating with Tools[¶](#authenticating-with-tools)

Many tools need to access protected resources (like user data in Google Calendar, Salesforce records, etc.) and require authentication. ADK provides a system to handle various authentication methods securely.

The key components involved are:

: Defines`AuthScheme`

*how*an API expects authentication credentials (e.g., as an API Key in a header, an OAuth 2.0 Bearer token). ADK supports the same types of authentication schemes as OpenAPI 3.0. To know more about what each type of credential is, refer to[OpenAPI doc: Authentication](https://swagger.io/docs/specification/v3_0/authentication/). ADK uses specific classes like`APIKey`

,`HTTPBearer`

,`OAuth2`

,`OpenIdConnectWithConfig`

.: Holds the`AuthCredential`

*initial*information needed to*start*the authentication process (e.g., your application's OAuth Client ID/Secret, an API key value). It includes an`auth_type`

(like`API_KEY`

,`OAUTH2`

,`SERVICE_ACCOUNT`

) specifying the credential type.

The general flow involves providing these details when configuring a tool. ADK then attempts to automatically exchange the initial credential for a usable one (like an access token) before the tool makes an API call. For flows requiring user interaction (like OAuth consent), a specific interactive process involving the Agent Client application is triggered.

## Supported Initial Credential Types[¶](#supported-initial-credential-types)

**API_KEY:**For simple key/value authentication. Usually requires no exchange.**HTTP:**Can represent Basic Auth (not recommended/supported for exchange) or already obtained Bearer tokens. If it's a Bearer token, no exchange is needed.**OAUTH2:**For standard OAuth 2.0 flows. Requires configuration (client ID, secret, scopes) and often triggers the interactive flow for user consent.**OPEN_ID_CONNECT:**For authentication based on OpenID Connect. Similar to OAuth2, often requires configuration and user interaction.**SERVICE_ACCOUNT:**For Google Cloud Service Account credentials (JSON key or Application Default Credentials). Typically exchanged for a Bearer token.

## Configuring Authentication on Tools[¶](#configuring-authentication-on-tools)

You set up authentication when defining your tool:

-
**RestApiTool / OpenAPIToolset**: Pass`auth_scheme`

and`auth_credential`

during initialization -
**GoogleApiToolSet Tools**: ADK has built-in 1st party tools like Google Calendar, BigQuery etc,. Use the toolset's specific method. -
**APIHubToolset / ApplicationIntegrationToolset**: Pass`auth_scheme`

and`auth_credential`

during initialization, if the API managed in API Hub / provided by Application Integration requires authentication.

WARNING

Storing sensitive credentials like access tokens and especially refresh tokens directly in the session state might pose security risks depending on your session storage backend (`SessionService`

) and overall application security posture.

Suitable for testing and development, but data is lost when the process ends. Less risk as it's transient.`InMemorySessionService`

:**Database/Persistent Storage:****Strongly consider encrypting**the token data before storing it in the database using a robust encryption library (like`cryptography`

) and managing encryption keys securely (e.g., using a key management service).**Secure Secret Stores:**For production environments, storing sensitive credentials in a dedicated secret manager (like Google Cloud Secret Manager or HashiCorp Vault) is the**most recommended approach**. Your tool could potentially store only short-lived access tokens or secure references (not the refresh token itself) in the session state, fetching the necessary secrets from the secure store when needed.

## Journey 1: Building Agentic Applications with Authenticated Tools[¶](#journey-1-building-agentic-applications-with-authenticated-tools)

This section focuses on using pre-existing tools (like those from `RestApiTool/ OpenAPIToolset`

, `APIHubToolset`

, `GoogleApiToolSet`

) that require authentication within your agentic application. Your main responsibility is configuring the tools and handling the client-side part of interactive authentication flows (if required by the tool).

### 1. Configuring Tools with Authentication[¶](#1-configuring-tools-with-authentication)

When adding an authenticated tool to your agent, you need to provide its required `AuthScheme`

and your application's initial `AuthCredential`

.

**A. Using OpenAPI-based Toolsets ( OpenAPIToolset, APIHubToolset, etc.)**


Pass the scheme and credential during toolset initialization. The toolset applies them to all generated tools. Here are few ways to create tools with authentication in ADK.

Create a tool requiring an API Key.

from google.adk.tools.openapi_tool.auth.auth_helpers import token_to_scheme_credential
from google.adk.tools.openapi_tool.openapi_spec_parser.openapi_toolset import OpenAPIToolset
auth_scheme, auth_credential = token_to_scheme_credential(
"apikey", "query", "apikey", "YOUR_API_KEY_STRING"
)
sample_api_toolset = OpenAPIToolset(
spec_str="...", # Fill this with an OpenAPI spec string
spec_str_type="yaml",
auth_scheme=auth_scheme,
auth_credential=auth_credential,
)


Create a tool requiring OAuth2.

from google.adk.tools.openapi_tool.openapi_spec_parser.openapi_toolset import OpenAPIToolset
from fastapi.openapi.models import OAuth2
from fastapi.openapi.models import OAuthFlowAuthorizationCode
from fastapi.openapi.models import OAuthFlows
from google.adk.auth import AuthCredential
from google.adk.auth import AuthCredentialTypes
from google.adk.auth import OAuth2Auth
auth_scheme = OAuth2(
flows=OAuthFlows(
authorizationCode=OAuthFlowAuthorizationCode(
authorizationUrl="https://accounts.google.com/o/oauth2/auth",
tokenUrl="https://oauth2.googleapis.com/token",
scopes={
"https://www.googleapis.com/auth/calendar": "calendar scope"
},
)
)
)
auth_credential = AuthCredential(
auth_type=AuthCredentialTypes.OAUTH2,
oauth2=OAuth2Auth(
client_id=YOUR_OAUTH_CLIENT_ID,
client_secret=YOUR_OAUTH_CLIENT_SECRET
),
)
calendar_api_toolset = OpenAPIToolset(
spec_str=google_calendar_openapi_spec_str, # Fill this with an openapi spec
spec_str_type='yaml',
auth_scheme=auth_scheme,
auth_credential=auth_credential,
)


Create a tool requiring Service Account.

from google.adk.tools.openapi_tool.auth.auth_helpers import service_account_dict_to_scheme_credential
from google.adk.tools.openapi_tool.openapi_spec_parser.openapi_toolset import OpenAPIToolset
service_account_cred = json.loads(service_account_json_str)
auth_scheme, auth_credential = service_account_dict_to_scheme_credential(
config=service_account_cred,
scopes=["https://www.googleapis.com/auth/cloud-platform"],
)
sample_toolset = OpenAPIToolset(
spec_str=sa_openapi_spec_str, # Fill this with an openapi spec
spec_str_type='json',
auth_scheme=auth_scheme,
auth_credential=auth_credential,
)


Create a tool requiring OpenID connect.

from google.adk.auth.auth_schemes import OpenIdConnectWithConfig
from google.adk.auth.auth_credential import AuthCredential, AuthCredentialTypes, OAuth2Auth
from google.adk.tools.openapi_tool.openapi_spec_parser.openapi_toolset import OpenAPIToolset
auth_scheme = OpenIdConnectWithConfig(
authorization_endpoint=OAUTH2_AUTH_ENDPOINT_URL,
token_endpoint=OAUTH2_TOKEN_ENDPOINT_URL,
scopes=['openid', 'YOUR_OAUTH_SCOPES"]
)
auth_credential = AuthCredential(
auth_type=AuthCredentialTypes.OPEN_ID_CONNECT,
oauth2=OAuth2Auth(
client_id="...",
client_secret="...",
)
)
userinfo_toolset = OpenAPIToolset(
spec_str=content, # Fill in an actual spec
spec_str_type='yaml',
auth_scheme=auth_scheme,
auth_credential=auth_credential,
)


**B. Using Google API Toolsets (e.g., calendar_tool_set)**

These toolsets often have dedicated configuration methods.

Tip: For how to create a Google OAuth Client ID & Secret, see this guide: [Get your Google API Client ID](https://developers.google.com/identity/gsi/web/guides/get-google-api-clientid#get_your_google_api_client_id)

# Example: Configuring Google Calendar Tools
from google.adk.tools.google_api_tool import calendar_tool_set
client_id = "YOUR_GOOGLE_OAUTH_CLIENT_ID.apps.googleusercontent.com"
client_secret = "YOUR_GOOGLE_OAUTH_CLIENT_SECRET"
# Use the specific configure method for this toolset type
calendar_tool_set.configure_auth(
client_id=oauth_client_id, client_secret=oauth_client_secret
)
# agent = LlmAgent(..., tools=calendar_tool_set.get_tool('calendar_tool_set'))


The sequence diagram of auth request flow (where tools are requesting auth credentials) looks like below:

### 2. Handling the Interactive OAuth/OIDC Flow (Client-Side)[¶](#2-handling-the-interactive-oauthoidc-flow-client-side)

If a tool requires user login/consent (typically OAuth 2.0 or OIDC), the ADK framework pauses execution and signals your **Agent Client** application. There are two cases:

**Agent Client**application runs the agent directly (via`runner.run_async`

) in the same process. e.g. UI backend, CLI app, or Spark job etc.**Agent Client**application interacts with ADK's fastapi server via`/run`

or`/run_sse`

endpoint. While ADK's fastapi server could be setup on the same server or different server as**Agent Client**application

The second case is a special case of first case, because `/run`

or `/run_sse`

endpoint also invokes `runner.run_async`

. The only differences are:

- Whether to call a python function to run the agent (first case) or call a service endpoint to run the agent (second case).
- Whether the result events are in-memory objects (first case) or serialized json string in http response (second case).

Below sections focus on the first case and you should be able to map it to the second case very straightforward. We will also describe some differences to handle for the second case if necessary.

Here's the step-by-step process for your client application:

**Step 1: Run Agent & Detect Auth Request**

- Initiate the agent interaction using
`runner.run_async`

. - Iterate through the yielded events.
- Look for a specific function call event whose function call has a special name:
`adk_request_credential`

. This event signals that user interaction is needed. You can use helper functions to identify this event and extract necessary information. (For the second case, the logic is similar. You deserialize the event from the http response).

# runner = Runner(...)
# session = await session_service.create_session(...)
# content = types.Content(...) # User's initial query
print("\nRunning agent...")
events_async = runner.run_async(
session_id=session.id, user_id='user', new_message=content
)
auth_request_function_call_id, auth_config = None, None
async for event in events_async:
# Use helper to check for the specific auth request event
if (auth_request_function_call := get_auth_request_function_call(event)):
print("--> Authentication required by agent.")
# Store the ID needed to respond later
if not (auth_request_function_call_id := auth_request_function_call.id):
raise ValueError(f'Cannot get function call id from function call: {auth_request_function_call}')
# Get the AuthConfig containing the auth_uri etc.
auth_config = get_auth_config(auth_request_function_call)
break # Stop processing events for now, need user interaction
if not auth_request_function_call_id:
print("\nAuth not required or agent finished.")
# return # Or handle final response if received


*Helper functions helpers.py:*

from google.adk.events import Event
from google.adk.auth import AuthConfig # Import necessary type
from google.genai import types
def get_auth_request_function_call(event: Event) -> types.FunctionCall:
# Get the special auth request function call from the event
if not event.content or not event.content.parts:
return
for part in event.content.parts:
if (
part
and part.function_call
and part.function_call.name == 'adk_request_credential'
and event.long_running_tool_ids
and part.function_call.id in event.long_running_tool_ids
):
return part.function_call
def get_auth_config(auth_request_function_call: types.FunctionCall) -> AuthConfig:
# Extracts the AuthConfig object from the arguments of the auth request function call
if not auth_request_function_call.args or not (auth_config := auth_request_function_call.args.get('authConfig')):
raise ValueError(f'Cannot get auth config from function call: {auth_request_function_call}')
if isinstance(auth_config, dict):
auth_config = AuthConfig.model_validate(auth_config)
elif not isinstance(auth_config, AuthConfig):
raise ValueError(f'Cannot get auth config {auth_config} is not an instance of AuthConfig.')
return auth_config


**Step 2: Redirect User for Authorization**

- Get the authorization URL (
`auth_uri`

) from the`auth_config`

extracted in the previous step. **Crucially, append your application's**redirect_uri as a query parameter to this`auth_uri`

. This`redirect_uri`

must be pre-registered with your OAuth provider (e.g.,[Google Cloud Console](https://developers.google.com/identity/protocols/oauth2/web-server#creatingcred),[Okta admin panel](https://developer.okta.com/docs/guides/sign-into-web-app-redirect/spring-boot/main/#create-an-app-integration-in-the-admin-console)).- Direct the user to this complete URL (e.g., open it in their browser).

# (Continuing after detecting auth needed)
if auth_request_function_call_id and auth_config:
# Get the base authorization URL from the AuthConfig
base_auth_uri = auth_config.exchanged_auth_credential.oauth2.auth_uri
if base_auth_uri:
redirect_uri = 'http://localhost:8000/callback' # MUST match your OAuth client app config
# Append redirect_uri (use urlencode in production)
auth_request_uri = base_auth_uri + f'&redirect_uri={redirect_uri}'
# Now you need to redirect your end user to this auth_request_uri or ask them to open this auth_request_uri in their browser
# This auth_request_uri should be served by the corresponding auth provider and the end user should login and authorize your applicaiton to access their data
# And then the auth provider will redirect the end user to the redirect_uri you provided
# Next step: Get this callback URL from the user (or your web server handler)
else:
print("ERROR: Auth URI not found in auth_config.")
# Handle error


**Step 3. Handle the Redirect Callback (Client):**

- Your application must have a mechanism (e.g., a web server route at the
`redirect_uri`

) to receive the user after they authorize the application with the provider. - The provider redirects the user to your
`redirect_uri`

and appends an`authorization_code`

(and potentially`state`

,`scope`

) as query parameters to the URL. - Capture the
**full callback URL**from this incoming request. - (This step happens outside the main agent execution loop, in your web server or equivalent callback handler.)

**Step 4. Send Authentication Result Back to ADK (Client):**

- Once you have the full callback URL (containing the authorization code), retrieve the
`auth_request_function_call_id`

and the`auth_config`

object saved in Client Step 1. - Set the captured callback URL into the
`exchanged_auth_credential.oauth2.auth_response_uri`

field. Also ensure`exchanged_auth_credential.oauth2.redirect_uri`

contains the redirect URI you used. - Create a
`types.Content`

object containing a`types.Part`

with a`types.FunctionResponse`

.- Set
`name`

to`"adk_request_credential"`

. (Note: This is a special name for ADK to proceed with authentication. Do not use other names.) - Set
`id`

to the`auth_request_function_call_id`

you saved. - Set
`response`

to the*serialized*(e.g.,`.model_dump()`

) updated`AuthConfig`

object.

- Set
- Call
`runner.run_async`

**again**for the same session, passing this`FunctionResponse`

content as the`new_message`

.

# (Continuing after user interaction)
# Simulate getting the callback URL (e.g., from user paste or web handler)
auth_response_uri = await get_user_input(
f'Paste the full callback URL here:\n> '
)
auth_response_uri = auth_response_uri.strip() # Clean input
if not auth_response_uri:
print("Callback URL not provided. Aborting.")
return
# Update the received AuthConfig with the callback details
auth_config.exchanged_auth_credential.oauth2.auth_response_uri = auth_response_uri
# Also include the redirect_uri used, as the token exchange might need it
auth_config.exchanged_auth_credential.oauth2.redirect_uri = redirect_uri
# Construct the FunctionResponse Content object
auth_content = types.Content(
role='user', # Role can be 'user' when sending a FunctionResponse
parts=[
types.Part(
function_response=types.FunctionResponse(
id=auth_request_function_call_id, # Link to the original request
name='adk_request_credential', # Special framework function name
response=auth_config.model_dump() # Send back the *updated* AuthConfig
)
)
],
)
# --- Resume Execution ---
print("\nSubmitting authentication details back to the agent...")
events_async_after_auth = runner.run_async(
session_id=session.id,
user_id='user',
new_message=auth_content, # Send the FunctionResponse back
)
# --- Process Final Agent Output ---
print("\n--- Agent Response after Authentication ---")
async for event in events_async_after_auth:
# Process events normally, expecting the tool call to succeed now
print(event) # Print the full event for inspection


Note: Authorization response with Resume feature

If your ADK agent workflow is configured with the
[Resume](/adk-docs/runtime/resume/) feature, you also must include
the Invocation ID (`invocation_id`

) parameter with the authorization
response. The Invocation ID you provide must be the same invocation
that generated the authorization request, otherwise the system
starts a new invocation with the authorization response. If your
agent uses the Resume feature, consider including the Invocation ID
as a parameter with your authorization request, so it can be included
with the authorization response. For more details on using the Resume
feature, see
[Resume stopped agents](/adk-docs/runtime/resume/).

**Step 5: ADK Handles Token Exchange & Tool Retry and gets Tool result**

- ADK receives the
`FunctionResponse`

for`adk_request_credential`

. - It uses the information in the updated
`AuthConfig`

(including the callback URL containing the code) to perform the OAuth**token exchange**with the provider's token endpoint, obtaining the access token (and possibly refresh token). - ADK internally makes these tokens available by setting them in the session state).
- ADK
**automatically retries**the original tool call (the one that initially failed due to missing auth). - This time, the tool finds the valid tokens (via
`tool_context.get_auth_response()`

) and successfully executes the authenticated API call. - The agent receives the actual result from the tool and generates its final response to the user.

The sequence diagram of auth response flow (where Agent Client send back the auth response and ADK retries tool calling) looks like below:

## Journey 2: Building Custom Tools (`FunctionTool`

) Requiring Authentication[¶](#journey-2-building-custom-tools-functiontool-requiring-authentication)

This section focuses on implementing the authentication logic *inside* your custom Python function when creating a new ADK Tool. We will implement a `FunctionTool`

as an example.

### Prerequisites[¶](#prerequisites)

Your function signature *must* include [ tool_context: ToolContext](../#tool-context). ADK automatically injects this object, providing access to state and auth mechanisms.

from google.adk.tools import FunctionTool, ToolContext
from typing import Dict
def my_authenticated_tool_function(param1: str, ..., tool_context: ToolContext) -> dict:
# ... your logic ...
pass
my_tool = FunctionTool(func=my_authenticated_tool_function)


### Authentication Logic within the Tool Function[¶](#authentication-logic-within-the-tool-function)

Implement the following steps inside your function:

**Step 1: Check for Cached & Valid Credentials:**

Inside your tool function, first check if valid credentials (e.g., access/refresh tokens) are already stored from a previous run in this session. Credentials for the current sessions should be stored in `tool_context.invocation_context.session.state`

(a dictionary of state) Check existence of existing credentials by checking `tool_context.invocation_context.session.state.get(credential_name, None)`

.

from google.oauth2.credentials import Credentials
from google.auth.transport.requests import Request
# Inside your tool function
TOKEN_CACHE_KEY = "my_tool_tokens" # Choose a unique key
SCOPES = ["scope1", "scope2"] # Define required scopes
creds = None
cached_token_info = tool_context.state.get(TOKEN_CACHE_KEY)
if cached_token_info:
try:
creds = Credentials.from_authorized_user_info(cached_token_info, SCOPES)
if not creds.valid and creds.expired and creds.refresh_token:
creds.refresh(Request())
tool_context.state[TOKEN_CACHE_KEY] = json.loads(creds.to_json()) # Update cache
elif not creds.valid:
creds = None # Invalid, needs re-auth
tool_context.state[TOKEN_CACHE_KEY] = None
except Exception as e:
print(f"Error loading/refreshing cached creds: {e}")
creds = None
tool_context.state[TOKEN_CACHE_KEY] = None
if creds and creds.valid:
# Skip to Step 5: Make Authenticated API Call
pass
else:
# Proceed to Step 2...
pass


**Step 2: Check for Auth Response from Client**

- If Step 1 didn't yield valid credentials, check if the client just completed the interactive flow by calling
`exchanged_credential = tool_context.get_auth_response()`

. - This returns the updated
`exchanged_credential`

object sent back by the client (containing the callback URL in`auth_response_uri`

).

# Use auth_scheme and auth_credential configured in the tool.
# exchanged_credential: AuthCredential | None
exchanged_credential = tool_context.get_auth_response(AuthConfig(
auth_scheme=auth_scheme,
raw_auth_credential=auth_credential,
))
# If exchanged_credential is not None, then there is already an exchanged credetial from the auth response.
if exchanged_credential:
# ADK exchanged the access token already for us
access_token = exchanged_credential.oauth2.access_token
refresh_token = exchanged_credential.oauth2.refresh_token
creds = Credentials(
token=access_token,
refresh_token=refresh_token,
token_uri=auth_scheme.flows.authorizationCode.tokenUrl,
client_id=auth_credential.oauth2.client_id,
client_secret=auth_credential.oauth2.client_secret,
scopes=list(auth_scheme.flows.authorizationCode.scopes.keys()),
)
# Cache the token in session state and call the API, skip to step 5


**Step 3: Initiate Authentication Request**

If no valid credentials (Step 1.) and no auth response (Step 2.) are found, the tool needs to start the OAuth flow. Define the AuthScheme and initial AuthCredential and call `tool_context.request_credential()`

. Return a response indicating authorization is needed.

# Use auth_scheme and auth_credential configured in the tool.
tool_context.request_credential(AuthConfig(
auth_scheme=auth_scheme,
raw_auth_credential=auth_credential,
))
return {'pending': true, 'message': 'Awaiting user authentication.'}
# By setting request_credential, ADK detects a pending authentication event. It pauses execution and ask end user to login.


**Step 4: Exchange Authorization Code for Tokens**

ADK automatically generates oauth authorization URL and presents it to your Agent Client application. your Agent Client application should follow the same way described in Journey 1 to redirect the user to the authorization URL (with `redirect_uri`

appended). Once a user completes the login flow following the authorization URL and ADK extracts the authentication callback url from Agent Client applications, automatically parses the auth code, and generates auth token. At the next Tool call, `tool_context.get_auth_response`

in step 2 will contain a valid credential to use in subsequent API calls.

**Step 5: Cache Obtained Credentials**

After successfully obtaining the token from ADK (Step 2) or if the token is still valid (Step 1), **immediately store** the new `Credentials`

object in `tool_context.state`

(serialized, e.g., as JSON) using your cache key.

# Inside your tool function, after obtaining 'creds' (either refreshed or newly exchanged)
# Cache the new/refreshed tokens
tool_context.state[TOKEN_CACHE_KEY] = json.loads(creds.to_json())
print(f"DEBUG: Cached/updated tokens under key: {TOKEN_CACHE_KEY}")
# Proceed to Step 6 (Make API Call)


**Step 6: Make Authenticated API Call**

- Once you have a valid
`Credentials`

object (`creds`

from Step 1 or Step 4), use it to make the actual call to the protected API using the appropriate client library (e.g.,`googleapiclient`

,`requests`

). Pass the`credentials=creds`

argument. - Include error handling, especially for
`HttpError`

401/403, which might mean the token expired or was revoked between calls. If you get such an error, consider clearing the cached token (`tool_context.state.pop(...)`

) and potentially returning the`auth_required`

status again to force re-authentication.

# Inside your tool function, using the valid 'creds' object
# Ensure creds is valid before proceeding
if not creds or not creds.valid:
return {"status": "error", "error_message": "Cannot proceed without valid credentials."}
try:
service = build("calendar", "v3", credentials=creds) # Example
api_result = service.events().list(...).execute()
# Proceed to Step 7
except Exception as e:
# Handle API errors (e.g., check for 401/403, maybe clear cache and re-request auth)
print(f"ERROR: API call failed: {e}")
return {"status": "error", "error_message": f"API call failed: {e}"}


**Step 7: Return Tool Result**

- After a successful API call, process the result into a dictionary format that is useful for the LLM.
**Crucially, include a**along with the data.

# Inside your tool function, after successful API call
processed_result = [...] # Process api_result for the LLM
return {"status": "success", "data": processed_result}


## Full Code

import os
from google.adk.auth.auth_schemes import OpenIdConnectWithConfig
from google.adk.auth.auth_credential import AuthCredential, AuthCredentialTypes, OAuth2Auth
from google.adk.tools.openapi_tool.openapi_spec_parser.openapi_toolset import OpenAPIToolset
from google.adk.agents.llm_agent import LlmAgent
# --- Authentication Configuration ---
# This section configures how the agent will handle authentication using OpenID Connect (OIDC),
# often layered on top of OAuth 2.0.
# Define the Authentication Scheme using OpenID Connect.
# This object tells the ADK *how* to perform the OIDC/OAuth2 flow.
# It requires details specific to your Identity Provider (IDP), like Google OAuth, Okta, Auth0, etc.
# Note: Replace the example Okta URLs and credentials with your actual IDP details.
# All following fields are required, and available from your IDP.
auth_scheme = OpenIdConnectWithConfig(
# The URL of the IDP's authorization endpoint where the user is redirected to log in.
authorization_endpoint="https://your-endpoint.okta.com/oauth2/v1/authorize",
# The URL of the IDP's token endpoint where the authorization code is exchanged for tokens.
token_endpoint="https://your-token-endpoint.okta.com/oauth2/v1/token",
# The scopes (permissions) your application requests from the IDP.
# 'openid' is standard for OIDC. 'profile' and 'email' request user profile info.
scopes=['openid', 'profile', "email"]
)
# Define the Authentication Credentials for your specific application.
# This object holds the client identifier and secret that your application uses
# to identify itself to the IDP during the OAuth2 flow.
# !! SECURITY WARNING: Avoid hardcoding secrets in production code. !!
# !! Use environment variables or a secret management system instead. !!
auth_credential = AuthCredential(
auth_type=AuthCredentialTypes.OPEN_ID_CONNECT,
oauth2=OAuth2Auth(
client_id="CLIENT_ID",
client_secret="CIENT_SECRET",
)
)
# --- Toolset Configuration from OpenAPI Specification ---
# This section defines a sample set of tools the agent can use, configured with Authentication
# from steps above.
# This sample set of tools use endpoints protected by Okta and requires an OpenID Connect flow
# to acquire end user credentials.
with open(os.path.join(os.path.dirname(__file__), 'spec.yaml'), 'r') as f:
spec_content = f.read()
userinfo_toolset = OpenAPIToolset(
spec_str=spec_content,
spec_str_type='yaml',
# ** Crucially, associate the authentication scheme and credentials with these tools. **
# This tells the ADK that the tools require the defined OIDC/OAuth2 flow.
auth_scheme=auth_scheme,
auth_credential=auth_credential,
)
# --- Agent Configuration ---
# Configure and create the main LLM Agent.
root_agent = LlmAgent(
model='gemini-2.0-flash',
name='enterprise_assistant',
instruction='Help user integrate with multiple enterprise systems, including retrieving user information which may require authentication.',
tools=userinfo_toolset.get_tools(),
)
# --- Ready for Use ---
# The `root_agent` is now configured with tools protected by OIDC/OAuth2 authentication.
# When the agent attempts to use one of these tools, the ADK framework will automatically
# trigger the authentication flow defined by `auth_scheme` and `auth_credential`
# if valid credentials are not already available in the session.
# The subsequent interaction flow would guide the user through the login process and handle
# token exchanging, and automatically attach the exchanged token to the endpoint defined in
# the tool.


import asyncio
from dotenv import load_dotenv
from google.adk.artifacts.in_memory_artifact_service import InMemoryArtifactService
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.genai import types
from .helpers import is_pending_auth_event, get_function_call_id, get_function_call_auth_config, get_user_input
from .tools_and_agent import root_agent
load_dotenv()
agent = root_agent
async def async_main():
"""
Main asynchronous function orchestrating the agent interaction and authentication flow.
"""
# --- Step 1: Service Initialization ---
# Use in-memory services for session and artifact storage (suitable for demos/testing).
session_service = InMemorySessionService()
artifacts_service = InMemoryArtifactService()
# Create a new user session to maintain conversation state.
session = session_service.create_session(
state={}, # Optional state dictionary for session-specific data
app_name='my_app', # Application identifier
user_id='user' # User identifier
)
# --- Step 2: Initial User Query ---
# Define the user's initial request.
query = 'Show me my user info'
print(f"user: {query}")
# Format the query into the Content structure expected by the ADK Runner.
content = types.Content(role='user', parts=[types.Part(text=query)])
# Initialize the ADK Runner
runner = Runner(
app_name='my_app',
agent=agent,
artifact_service=artifacts_service,
session_service=session_service,
)
# --- Step 3: Send Query and Handle Potential Auth Request ---
print("\nRunning agent with initial query...")
events_async = runner.run_async(
session_id=session.id, user_id='user', new_message=content
)
# Variables to store details if an authentication request occurs.
auth_request_event_id, auth_config = None, None
# Iterate through the events generated by the first run.
async for event in events_async:
# Check if this event is the specific 'adk_request_credential' function call.
if is_pending_auth_event(event):
print("--> Authentication required by agent.")
auth_request_event_id = get_function_call_id(event)
auth_config = get_function_call_auth_config(event)
# Once the auth request is found and processed, exit this loop.
# We need to pause execution here to get user input for authentication.
break
# If no authentication request was detected after processing all events, exit.
if not auth_request_event_id or not auth_config:
print("\nAuthentication not required for this query or processing finished.")
return # Exit the main function
# --- Step 4: Manual Authentication Step (Simulated OAuth 2.0 Flow) ---
# This section simulates the user interaction part of an OAuth 2.0 flow.
# In a real web application, this would involve browser redirects.
# Define the Redirect URI. This *must* match one of the URIs registered
# with the OAuth provider for your application. The provider sends the user
# back here after they approve the request.
redirect_uri = 'http://localhost:8000/dev-ui' # Example for local development
# Construct the Authorization URL that the user must visit.
# This typically includes the provider's authorization endpoint URL,
# client ID, requested scopes, response type (e.g., 'code'), and the redirect URI.
# Here, we retrieve the base authorization URI from the AuthConfig provided by ADK
# and append the redirect_uri.
# NOTE: A robust implementation would use urlencode and potentially add state, scope, etc.
auth_request_uri = (
auth_config.exchanged_auth_credential.oauth2.auth_uri
+ f'&redirect_uri={redirect_uri}' # Simple concatenation; ensure correct query param format
)
print("\n--- User Action Required ---")
# Prompt the user to visit the authorization URL, log in, grant permissions,
# and then paste the *full* URL they are redirected back to (which contains the auth code).
auth_response_uri = await get_user_input(
f'1. Please open this URL in your browser to log in:\n {auth_request_uri}\n\n'
f'2. After successful login and authorization, your browser will be redirected.\n'
f' Copy the *entire* URL from the browser\'s address bar.\n\n'
f'3. Paste the copied URL here and press Enter:\n\n> '
)
# --- Step 5: Prepare Authentication Response for the Agent ---
# Update the AuthConfig object with the information gathered from the user.
# The ADK framework needs the full response URI (containing the code)
# and the original redirect URI to complete the OAuth token exchange process internally.
auth_config.exchanged_auth_credential.oauth2.auth_response_uri = auth_response_uri
auth_config.exchanged_auth_credential.oauth2.redirect_uri = redirect_uri
# Construct a FunctionResponse Content object to send back to the agent/runner.
# This response explicitly targets the 'adk_request_credential' function call
# identified earlier by its ID.
auth_content = types.Content(
role='user',
parts=[
types.Part(
function_response=types.FunctionResponse(
# Crucially, link this response to the original request using the saved ID.
id=auth_request_event_id,
# The special name of the function call we are responding to.
name='adk_request_credential',
# The payload containing all necessary authentication details.
response=auth_config.model_dump(),
)
)
],
)
# --- Step 6: Resume Execution with Authentication ---
print("\nSubmitting authentication details back to the agent...")
# Run the agent again, this time providing the `auth_content` (FunctionResponse).
# The ADK Runner intercepts this, processes the 'adk_request_credential' response
# (performs token exchange, stores credentials), and then allows the agent
# to retry the original tool call that required authentication, now succeeding with
# a valid access token embedded.
events_async = runner.run_async(
session_id=session.id,
user_id='user',
new_message=auth_content, # Provide the prepared auth response
)
# Process and print the final events from the agent after authentication is complete.
# This stream now contain the actual result from the tool (e.g., the user info).
print("\n--- Agent Response after Authentication ---")
async for event in events_async:
print(event)
if __name__ == '__main__':
asyncio.run(async_main())


from google.adk.auth import AuthConfig
from google.adk.events import Event
import asyncio
# --- Helper Functions ---
async def get_user_input(prompt: str) -> str:
"""
Asynchronously prompts the user for input in the console.
Uses asyncio's event loop and run_in_executor to avoid blocking the main
asynchronous execution thread while waiting for synchronous `input()`.
Args:
prompt: The message to display to the user.
Returns:
The string entered by the user.
"""
loop = asyncio.get_event_loop()
# Run the blocking `input()` function in a separate thread managed by the executor.
return await loop.run_in_executor(None, input, prompt)
def is_pending_auth_event(event: Event) -> bool:
"""
Checks if an ADK Event represents a request for user authentication credentials.
The ADK framework emits a specific function call ('adk_request_credential')
when a tool requires authentication that hasn't been previously satisfied.
Args:
event: The ADK Event object to inspect.
Returns:
True if the event is an 'adk_request_credential' function call, False otherwise.
"""
# Safely checks nested attributes to avoid errors if event structure is incomplete.
return (
event.content
and event.content.parts
and event.content.parts[0] # Assuming the function call is in the first part
and event.content.parts[0].function_call
# The specific function name indicating an auth request from the ADK framework.
and event.content.parts[0].function_call.name == 'adk_request_credential'
)
def get_function_call_id(event: Event) -> str:
"""
Extracts the unique ID of the function call from an ADK Event.
This ID is crucial for correlating a function *response* back to the specific
function *call* that the agent initiated to request for auth credentials.
Args:
event: The ADK Event object containing the function call.
Returns:
The unique identifier string of the function call.
Raises:
ValueError: If the function call ID cannot be found in the event structure.
(Corrected typo from `contents` to `content` below)
"""
# Navigate through the event structure to find the function call ID.
if (
event
and event.content
and event.content.parts
and event.content.parts[0] # Use content, not contents
and event.content.parts[0].function_call
and event.content.parts[0].function_call.id
):
return event.content.parts[0].function_call.id
# If the ID is missing, raise an error indicating an unexpected event format.
raise ValueError(f'Cannot get function call id from event {event}')
def get_function_call_auth_config(event: Event) -> AuthConfig:
"""
Extracts the authentication configuration details from an 'adk_request_credential' event.
Client should use this AuthConfig to necessary authentication details (like OAuth codes and state)
and sent it back to the ADK to continue OAuth token exchanging.
Args:
event: The ADK Event object containing the 'adk_request_credential' call.
Returns:
An AuthConfig object populated with details from the function call arguments.
Raises:
ValueError: If the 'auth_config' argument cannot be found in the event.
(Corrected typo from `contents` to `content` below)
"""
if (
event
and event.content
and event.content.parts
and event.content.parts[0] # Use content, not contents
and event.content.parts[0].function_call
and event.content.parts[0].function_call.args
and event.content.parts[0].function_call.args.get('auth_config')
):
# Reconstruct the AuthConfig object using the dictionary provided in the arguments.
# The ** operator unpacks the dictionary into keyword arguments for the constructor.
return AuthConfig(
**event.content.parts[0].function_call.args.get('auth_config')
)
raise ValueError(f'Cannot get auth config from event {event}')


openapi: 3.0.1
info:
title: Okta User Info API
version: 1.0.0
description: |-
API to retrieve user profile information based on a valid Okta OIDC Access Token.
Authentication is handled via OpenID Connect with Okta.
contact:
name: API Support
email: support@example.com # Replace with actual contact if available
servers:
- url: <substitute with your server name>
description: Production Environment
paths:
/okta-jwt-user-api:
get:
summary: Get Authenticated User Info
description: |-
Fetches profile details for the user
operationId: getUserInfo
tags:
- User Profile
security:
- okta_oidc:
- openid
- email
- profile
responses:
'200':
description: Successfully retrieved user information.
content:
application/json:
schema:
type: object
properties:
sub:
type: string
description: Subject identifier for the user.
example: "abcdefg"
name:
type: string
description: Full name of the user.
example: "Example LastName"
locale:
type: string
description: User's locale, e.g., en-US or en_US.
example: "en_US"
email:
type: string
format: email
description: User's primary email address.
example: "username@example.com"
preferred_username:
type: string
description: Preferred username of the user (often the email).
example: "username@example.com"
given_name:
type: string
description: Given name (first name) of the user.
example: "Example"
family_name:
type: string
description: Family name (last name) of the user.
example: "LastName"
zoneinfo:
type: string
description: User's timezone, e.g., America/Los_Angeles.
example: "America/Los_Angeles"
updated_at:
type: integer
format: int64 # Using int64 for Unix timestamp
description: Timestamp when the user's profile was last updated (Unix epoch time).
example: 1743617719
email_verified:
type: boolean
description: Indicates if the user's email address has been verified.
example: true
required:
- sub
- name
- locale
- email
- preferred_username
- given_name
- family_name
- zoneinfo
- updated_at
- email_verified
'401':
description: Unauthorized. The provided Bearer token is missing, invalid, or expired.
content:
application/json:
schema:
$ref: '#/components/schemas/Error'
'403':
description: Forbidden. The provided token does not have the required scopes or permissions to access this resource.
content:
application/json:
schema:
$ref: '#/components/schemas/Error'
components:
securitySchemes:
okta_oidc:
type: openIdConnect
description: Authentication via Okta using OpenID Connect. Requires a Bearer Access Token.
openIdConnectUrl: https://your-endpoint.okta.com/.well-known/openid-configuration
schemas:
Error:
type: object
properties:
code:
type: string
description: An error code.
message:
type: string
description: A human-readable error message.
required:
- code
- message

---
<!-- Source: https://google.github.io/adk-docs/tools-custom/mcp-tools/ -->

# Model Context Protocol Tools¶

# Model Context Protocol Tools[¶](#model-context-protocol-tools)

This guide walks you through two ways of integrating Model Context Protocol (MCP) with ADK.

## What is Model Context Protocol (MCP)?[¶](#what-is-model-context-protocol-mcp)

The Model Context Protocol (MCP) is an open standard designed to standardize how Large Language Models (LLMs) like Gemini and Claude communicate with external applications, data sources, and tools. Think of it as a universal connection mechanism that simplifies how LLMs obtain context, execute actions, and interact with various systems.

MCP follows a client-server architecture, defining how **data** (resources), **interactive templates** (prompts), and **actionable functions** (tools) are exposed by an **MCP server** and consumed by an **MCP client** (which could be an LLM host application or an AI agent).

This guide covers two primary integration patterns:

**Using Existing MCP Servers within ADK:**An ADK agent acts as an MCP client, leveraging tools provided by external MCP servers.**Exposing ADK Tools via an MCP Server:**Building an MCP server that wraps ADK tools, making them accessible to any MCP client.

## Prerequisites[¶](#prerequisites)

Before you begin, ensure you have the following set up:

**Set up ADK:**Follow the standard ADK[setup instructions](../../get-started/)in the quickstart.**Install/update Python/Java:**MCP requires Python version of 3.9 or higher for Python or Java 17 or higher.**Setup Node.js and npx:****(Python only)**Many community MCP servers are distributed as Node.js packages and run using`npx`

. Install Node.js (which includes npx) if you haven't already. For details, see[https://nodejs.org/en](https://nodejs.org/en).**Verify Installations:****(Python only)**Confirm`adk`

and`npx`

are in your PATH within the activated virtual environment:

## 1. Using MCP servers with ADK agents (ADK as an MCP client) in `adk web`

[¶](#1-using-mcp-servers-with-adk-agents-adk-as-an-mcp-client-in-adk-web)

This section demonstrates how to integrate tools from external MCP (Model Context Protocol) servers into your ADK agents. This is the **most common** integration pattern when your ADK agent needs to use capabilities provided by an existing service that exposes an MCP interface. You will see how the `McpToolset`

class can be directly added to your agent's `tools`

list, enabling seamless connection to an MCP server, discovery of its tools, and making them available for your agent to use. These examples primarily focus on interactions within the `adk web`

development environment.

`McpToolset`

class[¶](#mcptoolset-class)

The `McpToolset`

class is ADK's primary mechanism for integrating tools from an MCP server. When you include an `McpToolset`

instance in your agent's `tools`

list, it automatically handles the interaction with the specified MCP server. Here's how it works:

**Connection Management:**On initialization,`McpToolset`

establishes and manages the connection to the MCP server. This can be a local server process (using`StdioConnectionParams`

for communication over standard input/output) or a remote server (using`SseConnectionParams`

for Server-Sent Events). The toolset also handles the graceful shutdown of this connection when the agent or application terminates.**Tool Discovery & Adaptation:**Once connected,`McpToolset`

queries the MCP server for its available tools (via the`list_tools`

MCP method). It then converts the schemas of these discovered MCP tools into ADK-compatible`BaseTool`

instances.**Exposure to Agent:**These adapted tools are then made available to your`LlmAgent`

as if they were native ADK tools.**Proxying Tool Calls:**When your`LlmAgent`

decides to use one of these tools,`McpToolset`

transparently proxies the call (using the`call_tool`

MCP method) to the MCP server, sends the necessary arguments, and returns the server's response back to the agent.**Filtering (Optional):**You can use the`tool_filter`

parameter when creating an`McpToolset`

to select a specific subset of tools from the MCP server, rather than exposing all of them to your agent.

The following examples demonstrate how to use `McpToolset`

within the `adk web`

development environment. For scenarios where you need more fine-grained control over the MCP connection lifecycle or are not using `adk web`

, refer to the "Using MCP Tools in your own Agent out of `adk web`

" section later in this page.

### Example 1: File System MCP Server[¶](#example-1-file-system-mcp-server)

This Python example demonstrates connecting to a local MCP server that provides file system operations.

#### Step 1: Define your Agent with `McpToolset`

[¶](#step-1-define-your-agent-with-mcptoolset)

Create an `agent.py`

file (e.g., in `./adk_agent_samples/mcp_agent/agent.py`

). The `McpToolset`

is instantiated directly within the `tools`

list of your `LlmAgent`

.

**Important:**Replace`"/path/to/your/folder"`

in the`args`

list with the**absolute path**to an actual folder on your local system that the MCP server can access.**Important:**Place the`.env`

file in the parent directory of the`./adk_agent_samples`

directory.

# ./adk_agent_samples/mcp_agent/agent.py
import os # Required for path operations
from google.adk.agents import LlmAgent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
# It's good practice to define paths dynamically if possible,
# or ensure the user understands the need for an ABSOLUTE path.
# For this example, we'll construct a path relative to this file,
# assuming '/path/to/your/folder' is in the same directory as agent.py.
# REPLACE THIS with an actual absolute path if needed for your setup.
TARGET_FOLDER_PATH = os.path.join(os.path.dirname(os.path.abspath(__file__)), "/path/to/your/folder")
# Ensure TARGET_FOLDER_PATH is an absolute path for the MCP server.
# If you created ./adk_agent_samples/mcp_agent/your_folder,
root_agent = LlmAgent(
model='gemini-2.0-flash',
name='filesystem_assistant_agent',
instruction='Help the user manage their files. You can list files, read files, etc.',
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params = StdioServerParameters(
command='npx',
args=[
"-y", # Argument for npx to auto-confirm install
"@modelcontextprotocol/server-filesystem",
# IMPORTANT: This MUST be an ABSOLUTE path to a folder the
# npx process can access.
# Replace with a valid absolute path on your system.
# For example: "/Users/youruser/accessible_mcp_files"
# or use a dynamically constructed absolute path:
os.path.abspath(TARGET_FOLDER_PATH),
],
),
),
# Optional: Filter which tools from the MCP server are exposed
# tool_filter=['list_directory', 'read_file']
)
],
)


#### Step 2: Create an `__init__.py`

file[¶](#step-2-create-an-__init__py-file)

Ensure you have an `__init__.py`

in the same directory as `agent.py`

to make it a discoverable Python package for ADK.

#### Step 3: Run `adk web`

and Interact[¶](#step-3-run-adk-web-and-interact)

Navigate to the parent directory of `mcp_agent`

(e.g., `adk_agent_samples`

) in your terminal and run:

Note for Windows users

When hitting the `_make_subprocess_transport NotImplementedError`

, consider using `adk web --no-reload`

instead.

Once the ADK Web UI loads in your browser:

- Select the
`filesystem_assistant_agent`

from the agent dropdown. - Try prompts like:
- "List files in the current directory."
- "Can you read the file named sample.txt?" (assuming you created it in
`TARGET_FOLDER_PATH`

). - "What is the content of
`another_file.md`

?"


You should see the agent interacting with the MCP file system server, and the server's responses (file listings, file content) relayed through the agent. The `adk web`

console (terminal where you ran the command) might also show logs from the `npx`

process if it outputs to stderr.

For Java, refer to the following sample to define an agent that initializes the `McpToolset`

:

package agents;
import com.google.adk.JsonBaseModel;
import com.google.adk.agents.LlmAgent;
import com.google.adk.agents.RunConfig;
import com.google.adk.runner.InMemoryRunner;
import com.google.adk.tools.mcp.McpTool;
import com.google.adk.tools.mcp.McpToolset;
import com.google.adk.tools.mcp.McpToolset.McpToolsAndToolsetResult;
import com.google.genai.types.Content;
import com.google.genai.types.Part;
import io.modelcontextprotocol.client.transport.ServerParameters;
import java.util.List;
import java.util.concurrent.CompletableFuture;
public class McpAgentCreator {
/**
* Initializes an McpToolset, retrieves tools from an MCP server using stdio,
* creates an LlmAgent with these tools, sends a prompt to the agent,
* and ensures the toolset is closed.
* @param args Command line arguments (not used).
*/
public static void main(String[] args) {
//Note: you may have permissions issues if the folder is outside home
String yourFolderPath = "~/path/to/folder";
ServerParameters connectionParams = ServerParameters.builder("npx")
.args(List.of(
"-y",
"@modelcontextprotocol/server-filesystem",
yourFolderPath
))
.build();
try {
CompletableFuture<McpToolsAndToolsetResult> futureResult =
McpToolset.fromServer(connectionParams, JsonBaseModel.getMapper());
McpToolsAndToolsetResult result = futureResult.join();
try (McpToolset toolset = result.getToolset()) {
List<McpTool> tools = result.getTools();
LlmAgent agent = LlmAgent.builder()
.model("gemini-2.0-flash")
.name("enterprise_assistant")
.description("An agent to help users access their file systems")
.instruction(
"Help user accessing their file systems. You can list files in a directory."
)
.tools(tools)
.build();
System.out.println("Agent created: " + agent.name());
InMemoryRunner runner = new InMemoryRunner(agent);
String userId = "user123";
String sessionId = "1234";
String promptText = "Which files are in this directory - " + yourFolderPath + "?";
// Explicitly create the session first
try {
// appName for InMemoryRunner defaults to agent.name() if not specified in constructor
runner.sessionService().createSession(runner.appName(), userId, null, sessionId).blockingGet();
System.out.println("Session created: " + sessionId + " for user: " + userId);
} catch (Exception sessionCreationException) {
System.err.println("Failed to create session: " + sessionCreationException.getMessage());
sessionCreationException.printStackTrace();
return;
}
Content promptContent = Content.fromParts(Part.fromText(promptText));
System.out.println("\nSending prompt: \"" + promptText + "\" to agent...\n");
runner.runAsync(userId, sessionId, promptContent, RunConfig.builder().build())
.blockingForEach(event -> {
System.out.println("Event received: " + event.toJson());
});
}
} catch (Exception e) {
System.err.println("An error occurred: " + e.getMessage());
e.printStackTrace();
}
}
}


Assuming a folder containing three files named `first`

, `second`

and `third`

, successful response will look like this:

Event received: {"id":"163a449e-691a-48a2-9e38-8cadb6d1f136","invocationId":"e-c2458c56-e57a-45b2-97de-ae7292e505ef","author":"enterprise_assistant","content":{"parts":[{"functionCall":{"id":"adk-388b4ac2-d40e-4f6a-bda6-f051110c6498","args":{"path":"~/home-test"},"name":"list_directory"}}],"role":"model"},"actions":{"stateDelta":{},"artifactDelta":{},"requestedAuthConfigs":{}},"timestamp":1747377543788}
Event received: {"id":"8728380b-bfad-4d14-8421-fa98d09364f1","invocationId":"e-c2458c56-e57a-45b2-97de-ae7292e505ef","author":"enterprise_assistant","content":{"parts":[{"functionResponse":{"id":"adk-388b4ac2-d40e-4f6a-bda6-f051110c6498","name":"list_directory","response":{"text_output":[{"text":"[FILE] first\n[FILE] second\n[FILE] third"}]}}}],"role":"user"},"actions":{"stateDelta":{},"artifactDelta":{},"requestedAuthConfigs":{}},"timestamp":1747377544679}
Event received: {"id":"8fe7e594-3e47-4254-8b57-9106ad8463cb","invocationId":"e-c2458c56-e57a-45b2-97de-ae7292e505ef","author":"enterprise_assistant","content":{"parts":[{"text":"There are three files in the directory: first, second, and third."}],"role":"model"},"actions":{"stateDelta":{},"artifactDelta":{},"requestedAuthConfigs":{}},"timestamp":1747377544689}


For Typescript, you can define an agent that initializes the `MCPToolset`

as follows:

import 'dotenv/config';
import {LlmAgent, MCPToolset} from "@google/adk";
// REPLACE THIS with an actual absolute path for your setup.
const TARGET_FOLDER_PATH = "/path/to/your/folder";
export const rootAgent = new LlmAgent({
model: "gemini-2.5-flash",
name: "filesystem_assistant_agent",
instruction: "Help the user manage their files. You can list files, read files, etc.",
tools: [
// To filter tools, pass a list of tool names as the second argument
// to the MCPToolset constructor.
// e.g., new MCPToolset(connectionParams, ['list_directory', 'read_file'])
new MCPToolset(
{
type: "StdioConnectionParams",
serverParams: {
command: "npx",
args: [
"-y",
"@modelcontextprotocol/server-filesystem",
// IMPORTANT: This MUST be an ABSOLUTE path to a folder the
// npx process can access.
// Replace with a valid absolute path on your system.
// For example: "/Users/youruser/accessible_mcp_files"
TARGET_FOLDER_PATH,
],
},
}
)
],
});


### Example 2: Google Maps MCP Server[¶](#example-2-google-maps-mcp-server)

This example demonstrates connecting to the Google Maps MCP server.

#### Step 1: Get API Key and Enable APIs[¶](#step-1-get-api-key-and-enable-apis)

**Google Maps API Key:**Follow the directions at[Use API keys](https://developers.google.com/maps/documentation/javascript/get-api-key#create-api-keys)to obtain a Google Maps API Key.**Enable APIs:**In your Google Cloud project, ensure the following APIs are enabled:- Directions API
- Routes API
For instructions, see the
[Getting started with Google Maps Platform](https://developers.google.com/maps/get-started#enable-api-sdk)documentation.


#### Step 2: Define your Agent with `McpToolset`

for Google Maps[¶](#step-2-define-your-agent-with-mcptoolset-for-google-maps)

Modify your `agent.py`

file (e.g., in `./adk_agent_samples/mcp_agent/agent.py`

). Replace `YOUR_GOOGLE_MAPS_API_KEY`

with the actual API key you obtained.

# ./adk_agent_samples/mcp_agent/agent.py
import os
from google.adk.agents import LlmAgent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
# Retrieve the API key from an environment variable or directly insert it.
# Using an environment variable is generally safer.
# Ensure this environment variable is set in the terminal where you run 'adk web'.
# Example: export GOOGLE_MAPS_API_KEY="YOUR_ACTUAL_KEY"
google_maps_api_key = os.environ.get("GOOGLE_MAPS_API_KEY")
if not google_maps_api_key:
# Fallback or direct assignment for testing - NOT RECOMMENDED FOR PRODUCTION
google_maps_api_key = "YOUR_GOOGLE_MAPS_API_KEY_HERE" # Replace if not using env var
if google_maps_api_key == "YOUR_GOOGLE_MAPS_API_KEY_HERE":
print("WARNING: GOOGLE_MAPS_API_KEY is not set. Please set it as an environment variable or in the script.")
# You might want to raise an error or exit if the key is crucial and not found.
root_agent = LlmAgent(
model='gemini-2.0-flash',
name='maps_assistant_agent',
instruction='Help the user with mapping, directions, and finding places using Google Maps tools.',
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params = StdioServerParameters(
command='npx',
args=[
"-y",
"@modelcontextprotocol/server-google-maps",
],
# Pass the API key as an environment variable to the npx process
# This is how the MCP server for Google Maps expects the key.
env={
"GOOGLE_MAPS_API_KEY": google_maps_api_key
}
),
),
# You can filter for specific Maps tools if needed:
# tool_filter=['get_directions', 'find_place_by_id']
)
],
)


#### Step 3: Ensure `__init__.py`

Exists[¶](#step-3-ensure-__init__py-exists)

If you created this in Example 1, you can skip this. Otherwise, ensure you have an `__init__.py`

in the `./adk_agent_samples/mcp_agent/`

directory:

#### Step 4: Run `adk web`

and Interact[¶](#step-4-run-adk-web-and-interact)

-

Replace**Set Environment Variable (Recommended):**Before running`adk web`

, it's best to set your Google Maps API key as an environment variable in your terminal:`YOUR_ACTUAL_GOOGLE_MAPS_API_KEY`

with your key. -
**Run**: Navigate to the parent directory of`adk web`

`mcp_agent`

(e.g.,`adk_agent_samples`

) and run: -
**Interact in the UI**:- Select the
`maps_assistant_agent`

. - Try prompts like:
- "Get directions from GooglePlex to SFO."
- "Find coffee shops near Golden Gate Park."
- "What's the route from Paris, France to Berlin, Germany?"


- Select the

You should see the agent use the Google Maps MCP tools to provide directions or location-based information.

For Java, refer to the following sample to define an agent that initializes the `McpToolset`

:

package agents;
import com.google.adk.JsonBaseModel;
import com.google.adk.agents.LlmAgent;
import com.google.adk.agents.RunConfig;
import com.google.adk.runner.InMemoryRunner;
import com.google.adk.tools.mcp.McpTool;
import com.google.adk.tools.mcp.McpToolset;
import com.google.adk.tools.mcp.McpToolset.McpToolsAndToolsetResult;
import com.google.genai.types.Content;
import com.google.genai.types.Part;
import io.modelcontextprotocol.client.transport.ServerParameters;
import java.util.List;
import java.util.Map;
import java.util.Collections;
import java.util.HashMap;
import java.util.concurrent.CompletableFuture;
import java.util.Arrays;
public class MapsAgentCreator {
/**
* Initializes an McpToolset for Google Maps, retrieves tools,
* creates an LlmAgent, sends a map-related prompt, and closes the toolset.
* @param args Command line arguments (not used).
*/
public static void main(String[] args) {
// TODO: Replace with your actual Google Maps API key, on a project with the Places API enabled.
String googleMapsApiKey = "YOUR_GOOGLE_MAPS_API_KEY";
Map<String, String> envVariables = new HashMap<>();
envVariables.put("GOOGLE_MAPS_API_KEY", googleMapsApiKey);
ServerParameters connectionParams = ServerParameters.builder("npx")
.args(List.of(
"-y",
"@modelcontextprotocol/server-google-maps"
))
.env(Collections.unmodifiableMap(envVariables))
.build();
try {
CompletableFuture<McpToolsAndToolsetResult> futureResult =
McpToolset.fromServer(connectionParams, JsonBaseModel.getMapper());
McpToolsAndToolsetResult result = futureResult.join();
try (McpToolset toolset = result.getToolset()) {
List<McpTool> tools = result.getTools();
LlmAgent agent = LlmAgent.builder()
.model("gemini-2.0-flash")
.name("maps_assistant")
.description("Maps assistant")
.instruction("Help user with mapping and directions using available tools.")
.tools(tools)
.build();
System.out.println("Agent created: " + agent.name());
InMemoryRunner runner = new InMemoryRunner(agent);
String userId = "maps-user-" + System.currentTimeMillis();
String sessionId = "maps-session-" + System.currentTimeMillis();
String promptText = "Please give me directions to the nearest pharmacy to Madison Square Garden.";
try {
runner.sessionService().createSession(runner.appName(), userId, null, sessionId).blockingGet();
System.out.println("Session created: " + sessionId + " for user: " + userId);
} catch (Exception sessionCreationException) {
System.err.println("Failed to create session: " + sessionCreationException.getMessage());
sessionCreationException.printStackTrace();
return;
}
Content promptContent = Content.fromParts(Part.fromText(promptText))
System.out.println("\nSending prompt: \"" + promptText + "\" to agent...\n");
runner.runAsync(userId, sessionId, promptContent, RunConfig.builder().build())
.blockingForEach(event -> {
System.out.println("Event received: " + event.toJson());
});
}
} catch (Exception e) {
System.err.println("An error occurred: " + e.getMessage());
e.printStackTrace();
}
}
}


A successful response will look like this:

Event received: {"id":"1a4deb46-c496-4158-bd41-72702c773368","invocationId":"e-48994aa0-531c-47be-8c57-65215c3e0319","author":"maps_assistant","content":{"parts":[{"text":"OK. I see a few options. The closest one is CVS Pharmacy at 5 Pennsylvania Plaza, New York, NY 10001, United States. Would you like directions?\n"}],"role":"model"},"actions":{"stateDelta":{},"artifactDelta":{},"requestedAuthConfigs":{}},"timestamp":1747380026642}


For TypeScript, refer to the following sample to define an agent that initializes the `MCPToolset`

:

import 'dotenv/config';
import {LlmAgent, MCPToolset} from "@google/adk";
// Retrieve the API key from an environment variable.
// Ensure this environment variable is set in the terminal where you run 'adk web'.
// Example: export GOOGLE_MAPS_API_KEY="YOUR_ACTUAL_KEY"
const googleMapsApiKey = process.env.GOOGLE_MAPS_API_KEY;
if (!googleMapsApiKey) {
throw new Error('GOOGLE_MAPS_API_KEY is not provided, please run "export GOOGLE_MAPS_API_KEY=YOUR_ACTUAL_KEY" to add that.');
}
export const rootAgent = new LlmAgent({
model: "gemini-2.5-flash",
name: "maps_assistant_agent",
instruction: "Help the user with mapping, directions, and finding places using Google Maps tools.",
tools: [
new MCPToolset(
{
type: "StdioConnectionParams",
serverParams: {
command: "npx",
args: [
"-y",
"@modelcontextprotocol/server-google-maps",
],
// Pass the API key as an environment variable to the npx process
// This is how the MCP server for Google Maps expects the key.
env: {
"GOOGLE_MAPS_API_KEY": googleMapsApiKey
}
},
},
// You can filter for specific Maps tools if needed:
// ['get_directions', 'find_place_by_id']
)
],
});


A successful response will look like this:

Event received: {"id":"1a4deb46-c496-4158-bd41-72702c773368","invocationId":"e-48994aa0-531c-47be-8c57-65215c3e0319","author":"maps_assistant","content":{"parts":[{"text":"OK. I see a few options. The closest one is CVS Pharmacy at 5 Pennsylvania Plaza, New York, NY 10001, United States. Would you like directions?\n"}],"role":"model"},"actions":{"stateDelta":{},"artifactDelta":{},"requestedAuthConfigs":{}},"timestamp":1747380026642}


## 2. Building an MCP server with ADK tools (MCP server exposing ADK)[¶](#2-building-an-mcp-server-with-adk-tools-mcp-server-exposing-adk)

This pattern allows you to wrap existing ADK tools and make them available to any standard MCP client application. The example in this section exposes the ADK `load_web_page`

tool through a custom-built MCP server.

### Summary of steps[¶](#summary-of-steps)

You will create a standard Python MCP server application using the `mcp`

library. Within this server, you will:

- Instantiate the ADK tool(s) you want to expose (e.g.,
`FunctionTool(load_web_page)`

). - Implement the MCP server's
`@app.list_tools()`

handler to advertise the ADK tool(s). This involves converting the ADK tool definition to the MCP schema using the`adk_to_mcp_tool_type`

utility from`google.adk.tools.mcp_tool.conversion_utils`

. - Implement the MCP server's
`@app.call_tool()`

handler. This handler will:- Receive tool call requests from MCP clients.
- Identify if the request targets one of your wrapped ADK tools.
- Execute the ADK tool's
`.run_async()`

method. - Format the ADK tool's result into an MCP-compliant response (e.g.,
`mcp.types.TextContent`

).


### Prerequisites[¶](#prerequisites_1)

Install the MCP server library in the same Python environment as your ADK installation:

### Step 1: Create the MCP Server Script[¶](#step-1-create-the-mcp-server-script)

Create a new Python file for your MCP server, for example, `my_adk_mcp_server.py`

.

### Step 2: Implement the Server Logic[¶](#step-2-implement-the-server-logic)

Add the following code to `my_adk_mcp_server.py`

. This script sets up an MCP server that exposes the ADK `load_web_page`

tool.

# my_adk_mcp_server.py
import asyncio
import json
import os
from dotenv import load_dotenv
# MCP Server Imports
from mcp import types as mcp_types # Use alias to avoid conflict
from mcp.server.lowlevel import Server, NotificationOptions
from mcp.server.models import InitializationOptions
import mcp.server.stdio # For running as a stdio server
# ADK Tool Imports
from google.adk.tools.function_tool import FunctionTool
from google.adk.tools.load_web_page import load_web_page # Example ADK tool
# ADK <-> MCP Conversion Utility
from google.adk.tools.mcp_tool.conversion_utils import adk_to_mcp_tool_type
# --- Load Environment Variables (If ADK tools need them, e.g., API keys) ---
load_dotenv() # Create a .env file in the same directory if needed
# --- Prepare the ADK Tool ---
# Instantiate the ADK tool you want to expose.
# This tool will be wrapped and called by the MCP server.
print("Initializing ADK load_web_page tool...")
adk_tool_to_expose = FunctionTool(load_web_page)
print(f"ADK tool '{adk_tool_to_expose.name}' initialized and ready to be exposed via MCP.")
# --- End ADK Tool Prep ---
# --- MCP Server Setup ---
print("Creating MCP Server instance...")
# Create a named MCP Server instance using the mcp.server library
app = Server("adk-tool-exposing-mcp-server")
# Implement the MCP server's handler to list available tools
@app.list_tools()
async def list_mcp_tools() -> list[mcp_types.Tool]:
"""MCP handler to list tools this server exposes."""
print("MCP Server: Received list_tools request.")
# Convert the ADK tool's definition to the MCP Tool schema format
mcp_tool_schema = adk_to_mcp_tool_type(adk_tool_to_expose)
print(f"MCP Server: Advertising tool: {mcp_tool_schema.name}")
return [mcp_tool_schema]
# Implement the MCP server's handler to execute a tool call
@app.call_tool()
async def call_mcp_tool(
name: str, arguments: dict
) -> list[mcp_types.Content]: # MCP uses mcp_types.Content
"""MCP handler to execute a tool call requested by an MCP client."""
print(f"MCP Server: Received call_tool request for '{name}' with args: {arguments}")
# Check if the requested tool name matches our wrapped ADK tool
if name == adk_tool_to_expose.name:
try:
# Execute the ADK tool's run_async method.
# Note: tool_context is None here because this MCP server is
# running the ADK tool outside of a full ADK Runner invocation.
# If the ADK tool requires ToolContext features (like state or auth),
# this direct invocation might need more sophisticated handling.
adk_tool_response = await adk_tool_to_expose.run_async(
args=arguments,
tool_context=None,
)
print(f"MCP Server: ADK tool '{name}' executed. Response: {adk_tool_response}")
# Format the ADK tool's response (often a dict) into an MCP-compliant format.
# Here, we serialize the response dictionary as a JSON string within TextContent.
# Adjust formatting based on the ADK tool's output and client needs.
response_text = json.dumps(adk_tool_response, indent=2)
# MCP expects a list of mcp_types.Content parts
return [mcp_types.TextContent(type="text", text=response_text)]
except Exception as e:
print(f"MCP Server: Error executing ADK tool '{name}': {e}")
# Return an error message in MCP format
error_text = json.dumps({"error": f"Failed to execute tool '{name}': {str(e)}"})
return [mcp_types.TextContent(type="text", text=error_text)]
else:
# Handle calls to unknown tools
print(f"MCP Server: Tool '{name}' not found/exposed by this server.")
error_text = json.dumps({"error": f"Tool '{name}' not implemented by this server."})
return [mcp_types.TextContent(type="text", text=error_text)]
# --- MCP Server Runner ---
async def run_mcp_stdio_server():
"""Runs the MCP server, listening for connections over standard input/output."""
# Use the stdio_server context manager from the mcp.server.stdio library
async with mcp.server.stdio.stdio_server() as (read_stream, write_stream):
print("MCP Stdio Server: Starting handshake with client...")
await app.run(
read_stream,
write_stream,
InitializationOptions(
server_name=app.name, # Use the server name defined above
server_version="0.1.0",
capabilities=app.get_capabilities(
# Define server capabilities - consult MCP docs for options
notification_options=NotificationOptions(),
experimental_capabilities={},
),
),
)
print("MCP Stdio Server: Run loop finished or client disconnected.")
if __name__ == "__main__":
print("Launching MCP Server to expose ADK tools via stdio...")
try:
asyncio.run(run_mcp_stdio_server())
except KeyboardInterrupt:
print("\nMCP Server (stdio) stopped by user.")
except Exception as e:
print(f"MCP Server (stdio) encountered an error: {e}")
finally:
print("MCP Server (stdio) process exiting.")
# --- End MCP Server ---


### Step 3: Test your Custom MCP Server with an ADK Agent[¶](#step-3-test-your-custom-mcp-server-with-an-adk-agent)

Now, create an ADK agent that will act as a client to the MCP server you just built. This ADK agent will use `McpToolset`

to connect to your `my_adk_mcp_server.py`

script.

Create an `agent.py`

(e.g., in `./adk_agent_samples/mcp_client_agent/agent.py`

):

# ./adk_agent_samples/mcp_client_agent/agent.py
import os
from google.adk.agents import LlmAgent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
# IMPORTANT: Replace this with the ABSOLUTE path to your my_adk_mcp_server.py script
PATH_TO_YOUR_MCP_SERVER_SCRIPT = "/path/to/your/my_adk_mcp_server.py" # <<< REPLACE
if PATH_TO_YOUR_MCP_SERVER_SCRIPT == "/path/to/your/my_adk_mcp_server.py":
print("WARNING: PATH_TO_YOUR_MCP_SERVER_SCRIPT is not set. Please update it in agent.py.")
# Optionally, raise an error if the path is critical
root_agent = LlmAgent(
model='gemini-2.0-flash',
name='web_reader_mcp_client_agent',
instruction="Use the 'load_web_page' tool to fetch content from a URL provided by the user.",
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params = StdioServerParameters(
command='python3', # Command to run your MCP server script
args=[PATH_TO_YOUR_MCP_SERVER_SCRIPT], # Argument is the path to the script
)
)
# tool_filter=['load_web_page'] # Optional: ensure only specific tools are loaded
)
],
)


And an `__init__.py`

in the same directory:

**To run the test:**

-

It will print "Launching MCP Server..." and wait. The ADK agent (run via**Start your custom MCP server (optional, for separate observation):**You can run your`my_adk_mcp_server.py`

directly in one terminal to see its logs:`adk web`

) will then connect to this process if the`command`

in`StdioConnectionParams`

is set up to execute it.*(Alternatively,*`McpToolset`

will start this server script as a subprocess automatically when the agent initializes). -
**Run**Navigate to the parent directory of`adk web`

for the client agent:`mcp_client_agent`

(e.g.,`adk_agent_samples`

) and run: -
**Interact in the ADK Web UI:**- Select the
`web_reader_mcp_client_agent`

. - Try a prompt like: "Load the content from https://example.com"

- Select the

The ADK agent (`web_reader_mcp_client_agent`

) will use `McpToolset`

to start and connect to your `my_adk_mcp_server.py`

. Your MCP server will receive the `call_tool`

request, execute the ADK `load_web_page`

tool, and return the result. The ADK agent will then relay this information. You should see logs from both the ADK Web UI (and its terminal) and potentially from your `my_adk_mcp_server.py`

terminal if you ran it separately.

This example demonstrates how ADK tools can be encapsulated within an MCP server, making them accessible to a broader range of MCP-compliant clients, not just ADK agents.

Refer to the [documentation](https://modelcontextprotocol.io/quickstart/server#core-mcp-concepts), to try it out with Claude Desktop.

## Using MCP Tools in your own Agent out of `adk web`

[¶](#using-mcp-tools-in-your-own-agent-out-of-adk-web)

This section is relevant to you if:

- You are developing your own Agent using ADK
- And, you are
**NOT**using`adk web`

, - And, you are exposing the agent via your own UI

Using MCP Tools requires a different setup than using regular tools, due to the fact that specs for MCP Tools are fetched asynchronously from the MCP Server running remotely, or in another process.

The following example is modified from the "Example 1: File System MCP Server" example above. The main differences are:

- Your tool and agent are created asynchronously
- You need to properly manage the exit stack, so that your agents and tools are destructed properly when the connection to MCP Server is closed.

# agent.py (modify get_tools_async and other parts as needed)
# ./adk_agent_samples/mcp_agent/agent.py
import os
import asyncio
from dotenv import load_dotenv
from google.genai import types
from google.adk.agents.llm_agent import LlmAgent
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.adk.artifacts.in_memory_artifact_service import InMemoryArtifactService # Optional
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
# Load environment variables from .env file in the parent directory
# Place this near the top, before using env vars like API keys
load_dotenv('../.env')
# Ensure TARGET_FOLDER_PATH is an absolute path for the MCP server.
TARGET_FOLDER_PATH = os.path.join(os.path.dirname(os.path.abspath(__file__)), "/path/to/your/folder")
# --- Step 1: Agent Definition ---
async def get_agent_async():
"""Creates an ADK Agent equipped with tools from the MCP Server."""
toolset = McpToolset(
# Use StdioConnectionParams for local process communication
connection_params=StdioConnectionParams(
server_params = StdioServerParameters(
command='npx', # Command to run the server
args=["-y", # Arguments for the command
"@modelcontextprotocol/server-filesystem",
TARGET_FOLDER_PATH],
),
),
tool_filter=['read_file', 'list_directory'] # Optional: filter specific tools
# For remote servers, you would use SseConnectionParams instead:
# connection_params=SseConnectionParams(url="http://remote-server:port/path", headers={...})
)
# Use in an agent
root_agent = LlmAgent(
model='gemini-2.0-flash', # Adjust model name if needed based on availability
name='enterprise_assistant',
instruction='Help user accessing their file systems',
tools=[toolset], # Provide the MCP tools to the ADK agent
)
return root_agent, toolset
# --- Step 2: Main Execution Logic ---
async def async_main():
session_service = InMemorySessionService()
# Artifact service might not be needed for this example
artifacts_service = InMemoryArtifactService()
session = await session_service.create_session(
state={}, app_name='mcp_filesystem_app', user_id='user_fs'
)
# TODO: Change the query to be relevant to YOUR specified folder.
# e.g., "list files in the 'documents' subfolder" or "read the file 'notes.txt'"
query = "list files in the tests folder"
print(f"User Query: '{query}'")
content = types.Content(role='user', parts=[types.Part(text=query)])
root_agent, toolset = await get_agent_async()
runner = Runner(
app_name='mcp_filesystem_app',
agent=root_agent,
artifact_service=artifacts_service, # Optional
session_service=session_service,
)
print("Running agent...")
events_async = runner.run_async(
session_id=session.id, user_id=session.user_id, new_message=content
)
async for event in events_async:
print(f"Event received: {event}")
# Cleanup is handled automatically by the agent framework
# But you can also manually close if needed:
print("Closing MCP server connection...")
await toolset.close()
print("Cleanup complete.")
if __name__ == '__main__':
try:
asyncio.run(async_main())
except Exception as e:
print(f"An error occurred: {e}")


## Key considerations[¶](#key-considerations)

When working with MCP and ADK, keep these points in mind:

-
**Protocol vs. Library:**MCP is a protocol specification, defining communication rules. ADK is a Python library/framework for building agents. McpToolset bridges these by implementing the client side of the MCP protocol within the ADK framework. Conversely, building an MCP server in Python requires using the model-context-protocol library. -
**ADK Tools vs. MCP Tools:**- ADK Tools (BaseTool, FunctionTool, AgentTool, etc.) are Python objects designed for direct use within the ADK's LlmAgent and Runner.
- MCP Tools are capabilities exposed by an MCP Server according to the protocol's schema. McpToolset makes these look like ADK tools to an LlmAgent.

-
**Asynchronous nature:**Both ADK and the MCP Python library are heavily based on the asyncio Python library. Tool implementations and server handlers should generally be async functions. -
**Stateful sessions (MCP):**MCP establishes stateful, persistent connections between a client and server instance. This differs from typical stateless REST APIs.**Deployment:**This statefulness can pose challenges for scaling and deployment, especially for remote servers handling many users. The original MCP design often assumed client and server were co-located. Managing these persistent connections requires careful infrastructure considerations (e.g., load balancing, session affinity).**ADK McpToolset:**Manages this connection lifecycle. The exit_stack pattern shown in the examples is crucial for ensuring the connection (and potentially the server process) is properly terminated when the ADK agent finishes.


## Deploying Agents with MCP Tools[¶](#deploying-agents-with-mcp-tools)

When deploying ADK agents that use MCP tools to production environments like Cloud Run, GKE, or Vertex AI Agent Engine, you need to consider how MCP connections will work in containerized and distributed environments.

### Critical Deployment Requirement: Synchronous Agent Definition[¶](#critical-deployment-requirement-synchronous-agent-definition)

**⚠️ Important:** When deploying agents with MCP tools, the agent and its McpToolset must be defined **synchronously** in your `agent.py`

file. While `adk web`

allows for asynchronous agent creation, deployment environments require synchronous instantiation.

# ✅ CORRECT: Synchronous agent definition for deployment
import os
from google.adk.agents.llm_agent import LlmAgent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StdioConnectionParams
from mcp import StdioServerParameters
_allowed_path = os.path.dirname(os.path.abspath(__file__))
root_agent = LlmAgent(
model='gemini-2.0-flash',
name='enterprise_assistant',
instruction=f'Help user accessing their file systems. Allowed directory: {_allowed_path}',
tools=[
McpToolset(
connection_params=StdioConnectionParams(
server_params=StdioServerParameters(
command='npx',
args=['-y', '@modelcontextprotocol/server-filesystem', _allowed_path],
),
timeout=5, # Configure appropriate timeouts
),
# Filter tools for security in production
tool_filter=[
'read_file', 'read_multiple_files', 'list_directory',
'directory_tree', 'search_files', 'get_file_info',
'list_allowed_directories',
],
)
],
)


# ❌ WRONG: Asynchronous patterns don't work in deployment
async def get_agent(): # This won't work for deployment
toolset = await create_mcp_toolset_async()
return LlmAgent(tools=[toolset])


### Quick Deployment Commands[¶](#quick-deployment-commands)

#### Vertex AI Agent Engine[¶](#vertex-ai-agent-engine)

uv run adk deploy agent_engine \
--project=<your-gcp-project-id> \
--region=<your-gcp-region> \
--staging_bucket="gs://<your-gcs-bucket>" \
--display_name="My MCP Agent" \
./path/to/your/agent_directory


#### Cloud Run[¶](#cloud-run)

uv run adk deploy cloud_run \
--project=<your-gcp-project-id> \
--region=<your-gcp-region> \
--service_name=<your-service-name> \
./path/to/your/agent_directory


### Deployment Patterns[¶](#deployment-patterns)

#### Pattern 1: Self-Contained Stdio MCP Servers[¶](#pattern-1-self-contained-stdio-mcp-servers)

For MCP servers that can be packaged as npm packages or Python modules (like `@modelcontextprotocol/server-filesystem`

), you can include them directly in your agent container:

**Container Requirements:**

# Example for npm-based MCP servers
FROM python:3.13-slim
# Install Node.js and npm for MCP servers
RUN apt-get update && apt-get install -y nodejs npm && rm -rf /var/lib/apt/lists/*
# Install your Python dependencies
COPY requirements.txt .
RUN pip install -r requirements.txt
# Copy your agent code
COPY . .
# Your agent can now use StdioConnectionParams with 'npx' commands
CMD ["python", "main.py"]


**Agent Configuration:**

# This works in containers because npx and the MCP server run in the same environment
McpToolset(
connection_params=StdioConnectionParams(
server_params=StdioServerParameters(
command='npx',
args=["-y", "@modelcontextprotocol/server-filesystem", "/app/data"],
),
),
)


#### Pattern 2: Remote MCP Servers (Streamable HTTP)[¶](#pattern-2-remote-mcp-servers-streamable-http)

For production deployments requiring scalability, deploy MCP servers as separate services and connect via Streamable HTTP:

**MCP Server Deployment (Cloud Run):**

# deploy_mcp_server.py - Separate Cloud Run service using Streamable HTTP
import contextlib
import logging
from collections.abc import AsyncIterator
from typing import Any
import anyio
import click
import mcp.types as types
from mcp.server.lowlevel import Server
from mcp.server.streamable_http_manager import StreamableHTTPSessionManager
from starlette.applications import Starlette
from starlette.routing import Mount
from starlette.types import Receive, Scope, Send
logger = logging.getLogger(__name__)
def create_mcp_server():
"""Create and configure the MCP server."""
app = Server("adk-mcp-streamable-server")
@app.call_tool()
async def call_tool(name: str, arguments: dict[str, Any]) -> list[types.ContentBlock]:
"""Handle tool calls from MCP clients."""
# Example tool implementation - replace with your actual ADK tools
if name == "example_tool":
result = arguments.get("input", "No input provided")
return [
types.TextContent(
type="text",
text=f"Processed: {result}"
)
]
else:
raise ValueError(f"Unknown tool: {name}")
@app.list_tools()
async def list_tools() -> list[types.Tool]:
"""List available tools."""
return [
types.Tool(
name="example_tool",
description="Example tool for demonstration",
inputSchema={
"type": "object",
"properties": {
"input": {
"type": "string",
"description": "Input text to process"
}
},
"required": ["input"]
}
)
]
return app
def main(port: int = 8080, json_response: bool = False):
"""Main server function."""
logging.basicConfig(level=logging.INFO)
app = create_mcp_server()
# Create session manager with stateless mode for scalability
session_manager = StreamableHTTPSessionManager(
app=app,
event_store=None,
json_response=json_response,
stateless=True, # Important for Cloud Run scalability
)
async def handle_streamable_http(scope: Scope, receive: Receive, send: Send) -> None:
await session_manager.handle_request(scope, receive, send)
@contextlib.asynccontextmanager
async def lifespan(app: Starlette) -> AsyncIterator[None]:
"""Manage session manager lifecycle."""
async with session_manager.run():
logger.info("MCP Streamable HTTP server started!")
try:
yield
finally:
logger.info("MCP server shutting down...")
# Create ASGI application
starlette_app = Starlette(
debug=False, # Set to False for production
routes=[
Mount("/mcp", app=handle_streamable_http),
],
lifespan=lifespan,
)
import uvicorn
uvicorn.run(starlette_app, host="0.0.0.0", port=port)
if __name__ == "__main__":
main()


**Agent Configuration for Remote MCP:**

# Your ADK agent connects to the remote MCP service via Streamable HTTP
McpToolset(
connection_params=StreamableHTTPConnectionParams(
url="https://your-mcp-server-url.run.app/mcp",
headers={"Authorization": "Bearer your-auth-token"}
),
)


#### Pattern 3: Sidecar MCP Servers (GKE)[¶](#pattern-3-sidecar-mcp-servers-gke)

In Kubernetes environments, you can deploy MCP servers as sidecar containers:

# deployment.yaml - GKE with MCP sidecar
apiVersion: apps/v1
kind: Deployment
metadata:
name: adk-agent-with-mcp
spec:
template:
spec:
containers:
# Main ADK agent container
- name: adk-agent
image: your-adk-agent:latest
ports:
- containerPort: 8080
env:
- name: MCP_SERVER_URL
value: "http://localhost:8081"
# MCP server sidecar
- name: mcp-server
image: your-mcp-server:latest
ports:
- containerPort: 8081


### Connection Management Considerations[¶](#connection-management-considerations)

#### Stdio Connections[¶](#stdio-connections)

**Pros:**Simple setup, process isolation, works well in containers**Cons:**Process overhead, not suitable for high-scale deployments**Best for:**Development, single-tenant deployments, simple MCP servers

#### SSE/HTTP Connections[¶](#ssehttp-connections)

**Pros:**Network-based, scalable, can handle multiple clients**Cons:**Requires network infrastructure, authentication complexity**Best for:**Production deployments, multi-tenant systems, external MCP services

### Production Deployment Checklist[¶](#production-deployment-checklist)

When deploying agents with MCP tools to production:

**✅ Connection Lifecycle**
- Ensure proper cleanup of MCP connections using exit_stack patterns
- Configure appropriate timeouts for connection establishment and requests
- Implement retry logic for transient connection failures

**✅ Resource Management**
- Monitor memory usage for stdio MCP servers (each spawns a process)
- Configure appropriate CPU/memory limits for MCP server processes
- Consider connection pooling for remote MCP servers

**✅ Security**
- Use authentication headers for remote MCP connections
- Restrict network access between ADK agents and MCP servers
- **Filter MCP tools using tool_filter to limit exposed functionality**
- Validate MCP tool inputs to prevent injection attacks
- Use restrictive file paths for filesystem MCP servers (e.g.,

`os.path.dirname(os.path.abspath(__file__))`

)
- Consider read-only tool filters for production environments**✅ Monitoring & Observability**
- Log MCP connection establishment and teardown events
- Monitor MCP tool execution times and success rates
- Set up alerts for MCP connection failures

**✅ Scalability**
- For high-volume deployments, prefer remote MCP servers over stdio
- Configure session affinity if using stateful MCP servers
- Consider MCP server connection limits and implement circuit breakers

### Environment-Specific Configurations[¶](#environment-specific-configurations)

#### Cloud Run[¶](#cloud-run_1)

# Cloud Run environment variables for MCP configuration
import os
# Detect Cloud Run environment
if os.getenv('K_SERVICE'):
# Use remote MCP servers in Cloud Run
mcp_connection = SseConnectionParams(
url=os.getenv('MCP_SERVER_URL'),
headers={'Authorization': f"Bearer {os.getenv('MCP_AUTH_TOKEN')}"}
)
else:
# Use stdio for local development
mcp_connection = StdioConnectionParams(
server_params=StdioServerParameters(
command='npx',
args=["-y", "@modelcontextprotocol/server-filesystem", "/tmp"]
)
)
McpToolset(connection_params=mcp_connection)


#### GKE[¶](#gke)

# GKE-specific MCP configuration
# Use service discovery for MCP servers within the cluster
McpToolset(
connection_params=SseConnectionParams(
url="http://mcp-service.default.svc.cluster.local:8080/sse"
),
)


#### Vertex AI Agent Engine[¶](#vertex-ai-agent-engine_1)

# Agent Engine managed deployment
# Prefer lightweight, self-contained MCP servers or external services
McpToolset(
connection_params=SseConnectionParams(
url="https://your-managed-mcp-service.googleapis.com/sse",
headers={'Authorization': 'Bearer $(gcloud auth print-access-token)'}
),
)


### Troubleshooting Deployment Issues[¶](#troubleshooting-deployment-issues)

**Common MCP Deployment Problems:**

-
**Stdio Process Startup Failures** -
**Network Connectivity Issues** -
**Resource Exhaustion** - Monitor container memory usage when using stdio MCP servers
- Set appropriate limits in Kubernetes deployments
- Use remote MCP servers for resource-intensive operations

---
<!-- Source: https://google.github.io/adk-docs/tools-custom/function-tools/ -->

# Function tools¶

# Function tools[¶](#function-tools)

When pre-built ADK tools don't meet your requirements, you can create custom *function tools*. Building function tools allows you to create tailored functionality, such as connecting to proprietary databases or implementing unique algorithms.
For example, a function tool, `myfinancetool`

, might be a function that calculates a specific financial metric. ADK also supports long-running functions, so if that calculation takes a while, the agent can continue working on other tasks.

ADK offers several ways to create functions tools, each suited to different levels of complexity and control:

## Function Tools[¶](#function-tool)

Transforming a Python function into a tool is a straightforward way to integrate custom logic into your agents. When you assign a function to an agent’s `tools`

list, the framework automatically wraps it as a `FunctionTool`

.

### How it Works[¶](#how-it-works)

The ADK framework automatically inspects your Python function's signature—including its name, docstring, parameters, type hints, and default values—to generate a schema. This schema is what the LLM uses to understand the tool's purpose, when to use it, and what arguments it requires.

### Defining Function Signatures[¶](#defining-function-signatures)

A well-defined function signature is crucial for the LLM to use your tool correctly.

#### Parameters[¶](#parameters)

##### Required Parameters[¶](#required-parameters)

A parameter is considered **required** if it has a type hint but **no default value**. The LLM must provide a value for this argument when it calls the tool. The parameter's description is taken from the function's docstring.

## Example: Required Parameters

def get_weather(city: str, unit: str):
"""
Retrieves the weather for a city in the specified unit.
Args:
city (str): The city name.
unit (str): The temperature unit, either 'Celsius' or 'Fahrenheit'.
"""
# ... function logic ...
return {"status": "success", "report": f"Weather for {city} is sunny."}


In this example, both `city`

and `unit`

are mandatory. If the LLM tries to call `get_weather`

without one of them, the ADK will return an error to the LLM, prompting it to correct the call.

In Go, you use struct tags to control the JSON schema. The two primary tags are `json`

and `jsonschema`

.

A parameter is considered **required** if its struct field does **not** have the `omitempty`

or `omitzero`

option in its `json`

tag.

The `jsonschema`

tag is used to provide the argument's description. This is crucial for the LLM to understand what the argument is for.

## Example: Required Parameters

// GetWeatherParams defines the arguments for the getWeather tool.
type GetWeatherParams struct {
// This field is REQUIRED (no "omitempty").
// The jsonschema tag provides the description.
Location string `json:"location" jsonschema:"The city and state, e.g., San Francisco, CA"`
// This field is also REQUIRED.
Unit string `json:"unit" jsonschema:"The temperature unit, either 'celsius' or 'fahrenheit'"`
}


In this example, both `location`

and `unit`

are mandatory.

##### Optional Parameters[¶](#optional-parameters)

A parameter is considered **optional** if you provide a **default value**. This is the standard Python way to define optional arguments. You can also mark a parameter as optional using `typing.Optional[SomeType]`

or the `| None`

syntax (Python 3.10+).

## Example: Optional Parameters

def search_flights(destination: str, departure_date: str, flexible_days: int = 0):
"""
Searches for flights.
Args:
destination (str): The destination city.
departure_date (str): The desired departure date.
flexible_days (int, optional): Number of flexible days for the search. Defaults to 0.
"""
# ... function logic ...
if flexible_days > 0:
return {"status": "success", "report": f"Found flexible flights to {destination}."}
return {"status": "success", "report": f"Found flights to {destination} on {departure_date}."}


Here, `flexible_days`

is optional. The LLM can choose to provide it, but it's not required.

A parameter is considered **optional** if its struct field has the `omitempty`

or `omitzero`

option in its `json`

tag.

## Example: Optional Parameters

// GetWeatherParams defines the arguments for the getWeather tool.
type GetWeatherParams struct {
// Location is required.
Location string `json:"location" jsonschema:"The city and state, e.g., San Francisco, CA"`
// Unit is optional.
Unit string `json:"unit,omitempty" jsonschema:"The temperature unit, either 'celsius' or 'fahrenheit'"`
// Days is optional.
Days int `json:"days,omitzero" jsonschema:"The number of forecast days to return (defaults to 1)"`
}


Here, `unit`

and `days`

are optional. The LLM can choose to provide them, but they are not required.

##### Optional Parameters with `typing.Optional`

[¶](#optional-parameters-with-typingoptional)

You can also mark a parameter as optional using `typing.Optional[SomeType]`

or the `| None`

syntax (Python 3.10+). This signals that the parameter can be `None`

. When combined with a default value of `None`

, it behaves as a standard optional parameter.

## Example: `typing.Optional`


from typing import Optional
def create_user_profile(username: str, bio: Optional[str] = None):
"""
Creates a new user profile.
Args:
username (str): The user's unique username.
bio (str, optional): A short biography for the user. Defaults to None.
"""
# ... function logic ...
if bio:
return {"status": "success", "message": f"Profile for {username} created with a bio."}
return {"status": "success", "message": f"Profile for {username} created."}


##### Variadic Parameters (`*args`

and `**kwargs`

)[¶](#variadic-parameters-args-and-kwargs)

While you can include `*args`

(variable positional arguments) and `**kwargs`

(variable keyword arguments) in your function signature for other purposes, they are **ignored by the ADK framework** when generating the tool schema for the LLM. The LLM will not be aware of them and cannot pass arguments to them. It's best to rely on explicitly defined parameters for all data you expect from the LLM.

#### Return Type[¶](#return-type)

The preferred return type for a Function Tool is a **dictionary** in Python, a **Map** in Java, or an **object** in TypeScript. This allows you to structure the response with key-value pairs, providing context and clarity to the LLM. If your function returns a type other than a dictionary, the framework automatically wraps it into a dictionary with a single key named **"result"**.

Strive to make your return values as descriptive as possible. *For example,* instead of returning a numeric error code, return a dictionary with an "error_message" key containing a human-readable explanation. **Remember that the LLM**, not a piece of code, needs to understand the result. As a best practice, include a "status" key in your return dictionary to indicate the overall outcome (e.g., "success", "error", "pending"), providing the LLM with a clear signal about the operation's state.

#### Docstrings[¶](#docstrings)

The docstring of your function serves as the tool's **description** and is sent to the LLM. Therefore, a well-written and comprehensive docstring is crucial for the LLM to understand how to use the tool effectively. Clearly explain the purpose of the function, the meaning of its parameters, and the expected return values.

### Passing Data Between Tools[¶](#passing-data-between-tools)

When an agent calls multiple tools in a sequence, you might need to pass data from one tool to another. The recommended way to do this is by using the `temp:`

prefix in the session state.

A tool can write data to a `temp:`

variable, and a subsequent tool can read it. This data is only available for the current invocation and is discarded afterwards.

Shared Invocation Context

All tool calls within a single agent turn share the same `InvocationContext`

. This means they also share the same temporary (`temp:`

) state, which is how data can be passed between them.

### Example[¶](#example)

## Example

This tool is a python function which obtains the Stock price of a given Stock ticker/ symbol.

__Note__: You need to `pip install yfinance`

library before using this tool.

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
from google.genai import types
import yfinance as yf
APP_NAME = "stock_app"
USER_ID = "1234"
SESSION_ID = "session1234"
def get_stock_price(symbol: str):
"""
Retrieves the current stock price for a given symbol.
Args:
symbol (str): The stock symbol (e.g., "AAPL", "GOOG").
Returns:
float: The current stock price, or None if an error occurs.
"""
try:
stock = yf.Ticker(symbol)
historical_data = stock.history(period="1d")
if not historical_data.empty:
current_price = historical_data['Close'].iloc[-1]
return current_price
else:
return None
except Exception as e:
print(f"Error retrieving stock price for {symbol}: {e}")
return None
stock_price_agent = Agent(
model='gemini-2.0-flash',
name='stock_agent',
instruction= 'You are an agent who retrieves stock prices. If a ticker symbol is provided, fetch the current price. If only a company name is given, first perform a Google search to find the correct ticker symbol before retrieving the stock price. If the provided ticker symbol is invalid or data cannot be retrieved, inform the user that the stock price could not be found.',
description='This agent specializes in retrieving real-time stock prices. Given a stock ticker symbol (e.g., AAPL, GOOG, MSFT) or the stock name, use the tools and reliable data sources to provide the most up-to-date price.',
tools=[get_stock_price], # You can add Python functions directly to the tools list; they will be automatically wrapped as FunctionTools.
)
# Session and Runner
async def setup_session_and_runner():
session_service = InMemorySessionService()
session = await session_service.create_session(app_name=APP_NAME, user_id=USER_ID, session_id=SESSION_ID)
runner = Runner(agent=stock_price_agent, app_name=APP_NAME, session_service=session_service)
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
await call_agent_async("stock price of GOOG")


The return value from this tool will be wrapped into a dictionary.

This tool retrieves the mocked value of a stock price.

/**
* Copyright 2025 Google LLC
*
* Licensed under the Apache License, Version 2.0 (the "License");
* you may not use this file except in compliance with the License.
* You may obtain a copy of the License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed to in writing, software
* distributed under the License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
* See the License for the specific language governing permissions and
* limitations under the License.
*/
import {Content, Part, createUserContent} from '@google/genai';
import {
stringifyContent,
FunctionTool,
InMemoryRunner,
LlmAgent,
} from '@google/adk';
import {z} from 'zod';
// Define the function to get the stock price
async function getStockPrice({ticker}: {ticker: string}): Promise<Record<string, unknown>> {
console.log(`Getting stock price for ${ticker}`);
// In a real-world scenario, you would fetch the stock price from an API
const price = (Math.random() * 1000).toFixed(2);
return {price: `$${price}`};
}
async function main() {
// Define the schema for the tool's parameters using Zod
const getStockPriceSchema = z.object({
ticker: z.string().describe('The stock ticker symbol to look up.'),
});
// Create a FunctionTool from the function and schema
const stockPriceTool = new FunctionTool({
name: 'getStockPrice',
description: 'Gets the current price of a stock.',
parameters: getStockPriceSchema,
execute: getStockPrice,
});
// Define the agent that will use the tool
const stockAgent = new LlmAgent({
name: 'stock_agent',
model: 'gemini-2.5-flash',
instruction: 'You can get the stock price of a company.',
tools: [stockPriceTool],
});
// Create a runner for the agent
const runner = new InMemoryRunner({agent: stockAgent});
// Create a new session
const session = await runner.sessionService.createSession({
appName: runner.appName,
userId: 'test-user',
});
const userContent: Content = createUserContent('What is the stock price of GOOG?');
// Run the agent and get the response
const response = [];
for await (const event of runner.runAsync({
userId: session.userId,
sessionId: session.id,
newMessage: userContent,
})) {
response.push(event);
}
// Print the final response from the agent
const finalResponse = response[response.length - 1];
if (finalResponse?.content?.parts?.length) {
console.log(stringifyContent(finalResponse));
}
}
main();


The return value from this tool will be an object.

This tool retrieves the mocked value of a stock price.

import (
"google.golang.org/adk/agent"
"google.golang.org/adk/agent/llmagent"
"google.golang.org/adk/model/gemini"
"google.golang.org/adk/runner"
"google.golang.org/adk/session"
"google.golang.org/adk/tool"
"google.golang.org/adk/tool/functiontool"
"google.golang.org/genai"
)
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
"strings"
"google.golang.org/adk/agent"
"google.golang.org/adk/agent/llmagent"
"google.golang.org/adk/model/gemini"
"google.golang.org/adk/runner"
"google.golang.org/adk/session"
"google.golang.org/adk/tool"
"google.golang.org/adk/tool/agenttool"
"google.golang.org/adk/tool/functiontool"
"google.golang.org/genai"
)
// mockStockPrices provides a simple in-memory database of stock prices
// to simulate a real-world stock data API. This allows the example to
// demonstrate tool functionality without making external network calls.
var mockStockPrices = map[string]float64{
"GOOG": 300.6,
"AAPL": 123.4,
"MSFT": 234.5,
}
// getStockPriceArgs defines the schema for the arguments passed to the getStockPrice tool.
// Using a struct is the recommended approach in the Go ADK as it provides strong
// typing and clear validation for the expected inputs.
type getStockPriceArgs struct {
Symbol string `json:"symbol" jsonschema:"The stock ticker symbol, e.g., GOOG"`
}
// getStockPriceResults defines the output schema for the getStockPrice tool.
type getStockPriceResults struct {
Symbol string `json:"symbol"`
Price float64 `json:"price,omitempty"`
Error string `json:"error,omitempty"`
}
// getStockPrice is a tool that retrieves the stock price for a given ticker symbol
// from the mockStockPrices map. It demonstrates how a function can be used as a
// tool by an agent. If the symbol is found, it returns a struct containing the
// symbol and its price. Otherwise, it returns a struct with an error message.
func getStockPrice(ctx tool.Context, input getStockPriceArgs) (getStockPriceResults, error) {
symbolUpper := strings.ToUpper(input.Symbol)
if price, ok := mockStockPrices[symbolUpper]; ok {
fmt.Printf("Tool: Found price for %s: %f\n", input.Symbol, price)
return getStockPriceResults{Symbol: input.Symbol, Price: price}, nil
}
return getStockPriceResults{}, fmt.Errorf("no data found for symbol")
}
// createStockAgent initializes and configures an LlmAgent.
// This agent is equipped with the getStockPrice tool and is instructed
// on how to respond to user queries about stock prices. It uses the
// Gemini model to understand user intent and decide when to use its tools.
func createStockAgent(ctx context.Context) (agent.Agent, error) {
stockPriceTool, err := functiontool.New(
functiontool.Config{
Name: "get_stock_price",
Description: "Retrieves the current stock price for a given symbol.",
},
getStockPrice)
if err != nil {
return nil, err
}
model, err := gemini.NewModel(ctx, "gemini-2.5-flash", &genai.ClientConfig{})
if err != nil {
log.Fatalf("Failed to create model: %v", err)
}
return llmagent.New(llmagent.Config{
Name: "stock_agent",
Model: model,
Instruction: "You are an agent who retrieves stock prices. If a ticker symbol is provided, fetch the current price. If only a company name is given, first perform a Google search to find the correct ticker symbol before retrieving the stock price. If the provided ticker symbol is invalid or data cannot be retrieved, inform the user that the stock price could not be found.",
Description: "This agent specializes in retrieving real-time stock prices. Given a stock ticker symbol (e.g., AAPL, GOOG, MSFT) or the stock name, use the tools and reliable data sources to provide the most up-to-date price.",
Tools: []tool.Tool{
stockPriceTool,
},
})
}
// userID and appName are constants used to identify the user and application
// throughout the session. These values are important for logging, tracking,
// and managing state across different agent interactions.
const (
userID = "example_user_id"
appName = "example_app"
)
// callAgent orchestrates the execution of the agent for a given prompt.
// It sets up the necessary services, creates a session, and uses a runner
// to manage the agent's lifecycle. It streams the agent's responses and
// prints them to the console, handling any potential errors during the run.
func callAgent(ctx context.Context, a agent.Agent, prompt string) {
sessionService := session.InMemoryService()
// Create a new session for the agent interactions.
session, err := sessionService.Create(ctx, &session.CreateRequest{
AppName: appName,
UserID: userID,
})
if err != nil {
log.Fatalf("Failed to create the session service: %v", err)
}
config := runner.Config{
AppName: appName,
Agent: a,
SessionService: sessionService,
}
// Create the runner to manage the agent execution.
r, err := runner.New(config)
if err != nil {
log.Fatalf("Failed to create the runner: %v", err)
}
sessionID := session.Session.ID()
userMsg := &genai.Content{
Parts: []*genai.Part{
genai.NewPartFromText(prompt),
},
Role: string(genai.RoleUser),
}
for event, err := range r.Run(ctx, userID, sessionID, userMsg, agent.RunConfig{
StreamingMode: agent.StreamingModeNone,
}) {
if err != nil {
fmt.Printf("\nAGENT_ERROR: %v\n", err)
} else {
for _, p := range event.Content.Parts {
fmt.Print(p.Text)
}
}
}
}
// RunAgentSimulation serves as the entry point for this example.
// It creates the stock agent and then simulates a series of user interactions
// by sending different prompts to the agent. This function showcases how the
// agent responds to various queries, including both successful and unsuccessful
// attempts to retrieve stock prices.
func RunAgentSimulation() {
// Create the stock agent
agent, err := createStockAgent(context.Background())
if err != nil {
panic(err)
}
fmt.Println("Agent created:", agent.Name())
prompts := []string{
"stock price of GOOG",
"What's the price of MSFT?",
"Can you find the stock price for an unknown company XYZ?",
}
// Simulate running the agent with different prompts
for _, prompt := range prompts {
fmt.Printf("\nPrompt: %s\nResponse: ", prompt)
callAgent(context.Background(), agent, prompt)
fmt.Println("\n---")
}
}
// createSummarizerAgent creates an agent whose sole purpose is to summarize text.
func createSummarizerAgent(ctx context.Context) (agent.Agent, error) {
model, err := gemini.NewModel(ctx, "gemini-2.5-flash", &genai.ClientConfig{})
if err != nil {
return nil, err
}
return llmagent.New(llmagent.Config{
Name: "SummarizerAgent",
Model: model,
Instruction: "You are an expert at summarizing text. Take the user's input and provide a concise summary.",
Description: "An agent that summarizes text.",
})
}
// createMainAgent creates the primary agent that will use the summarizer agent as a tool.
func createMainAgent(ctx context.Context, tools ...tool.Tool) (agent.Agent, error) {
model, err := gemini.NewModel(ctx, "gemini-2.5-flash", &genai.ClientConfig{})
if err != nil {
return nil, err
}
return llmagent.New(llmagent.Config{
Name: "MainAgent",
Model: model,
Instruction: "You are a helpful assistant. If you are asked to summarize a long text, use the 'summarize' tool. " +
"After getting the summary, present it to the user by saying 'Here is a summary of the text:'.",
Description: "The main agent that can delegate tasks.",
Tools: tools,
})
}
func RunAgentAsToolSimulation() {
ctx := context.Background()
// 1. Create the Tool Agent (Summarizer)
summarizerAgent, err := createSummarizerAgent(ctx)
if err != nil {
log.Fatalf("Failed to create summarizer agent: %v", err)
}
// 2. Wrap the Tool Agent in an AgentTool
summarizeTool := agenttool.New(summarizerAgent, &agenttool.Config{
SkipSummarization: true,
})
// 3. Create the Main Agent and provide it with the AgentTool
mainAgent, err := createMainAgent(ctx, summarizeTool)
if err != nil {
log.Fatalf("Failed to create main agent: %v", err)
}
// 4. Run the main agent
prompt := `
Please summarize this text for me:
Quantum computing represents a fundamentally different approach to computation,
leveraging the bizarre principles of quantum mechanics to process information. Unlike classical computers
that rely on bits representing either 0 or 1, quantum computers use qubits which can exist in a state of superposition - effectively
being 0, 1, or a combination of both simultaneously. Furthermore, qubits can become entangled,
meaning their fates are intertwined regardless of distance, allowing for complex correlations. This parallelism and
interconnectedness grant quantum computers the potential to solve specific types of incredibly complex problems - such
as drug discovery, materials science, complex system optimization, and breaking certain types of cryptography - far
faster than even the most powerful classical supercomputers could ever achieve, although the technology is still largely in its developmental stages.
`
fmt.Printf("\nPrompt: %s\nResponse: ", prompt)
callAgent(context.Background(), mainAgent, prompt)
fmt.Println("\n---")
}
func main() {
fmt.Println("Attempting to run the agent simulation...")
RunAgentSimulation()
fmt.Println("\nAttempting to run the agent-as-a-tool simulation...")
RunAgentAsToolSimulation()
}


The return value from this tool will be a `getStockPriceResults`

instance.

This tool retrieves the mocked value of a stock price.

import com.google.adk.agents.LlmAgent;
import com.google.adk.events.Event;
import com.google.adk.runner.InMemoryRunner;
import com.google.adk.sessions.Session;
import com.google.adk.tools.Annotations.Schema;
import com.google.adk.tools.FunctionTool;
import com.google.genai.types.Content;
import com.google.genai.types.Part;
import io.reactivex.rxjava3.core.Flowable;
import java.util.HashMap;
import java.util.Map;
public class StockPriceAgent {
private static final String APP_NAME = "stock_agent";
private static final String USER_ID = "user1234";
// Mock data for various stocks functionality
// NOTE: This is a MOCK implementation. In a real Java application,
// you would use a financial data API or library.
private static final Map<String, Double> mockStockPrices = new HashMap<>();
static {
mockStockPrices.put("GOOG", 1.0);
mockStockPrices.put("AAPL", 1.0);
mockStockPrices.put("MSFT", 1.0);
}
@Schema(description = "Retrieves the current stock price for a given symbol.")
public static Map<String, Object> getStockPrice(
@Schema(description = "The stock symbol (e.g., \"AAPL\", \"GOOG\")",
name = "symbol")
String symbol) {
try {
if (mockStockPrices.containsKey(symbol.toUpperCase())) {
double currentPrice = mockStockPrices.get(symbol.toUpperCase());
System.out.println("Tool: Found price for " + symbol + ": " + currentPrice);
return Map.of("symbol", symbol, "price", currentPrice);
} else {
return Map.of("symbol", symbol, "error", "No data found for symbol");
}
} catch (Exception e) {
return Map.of("symbol", symbol, "error", e.getMessage());
}
}
public static void callAgent(String prompt) {
// Create the FunctionTool from the Java method
FunctionTool getStockPriceTool = FunctionTool.create(StockPriceAgent.class, "getStockPrice");
LlmAgent stockPriceAgent =
LlmAgent.builder()
.model("gemini-2.0-flash")
.name("stock_agent")
.instruction(
"You are an agent who retrieves stock prices. If a ticker symbol is provided, fetch the current price. If only a company name is given, first perform a Google search to find the correct ticker symbol before retrieving the stock price. If the provided ticker symbol is invalid or data cannot be retrieved, inform the user that the stock price could not be found.")
.description(
"This agent specializes in retrieving real-time stock prices. Given a stock ticker symbol (e.g., AAPL, GOOG, MSFT) or the stock name, use the tools and reliable data sources to provide the most up-to-date price.")
.tools(getStockPriceTool) // Add the Java FunctionTool
.build();
// Create an InMemoryRunner
InMemoryRunner runner = new InMemoryRunner(stockPriceAgent, APP_NAME);
// InMemoryRunner automatically creates a session service. Create a session using the service
Session session = runner.sessionService().createSession(APP_NAME, USER_ID).blockingGet();
Content userMessage = Content.fromParts(Part.fromText(prompt));
// Run the agent
Flowable<Event> eventStream = runner.runAsync(USER_ID, session.id(), userMessage);
// Stream event response
eventStream.blockingForEach(
event -> {
if (event.finalResponse()) {
System.out.println(event.stringifyContent());
}
});
}
public static void main(String[] args) {
callAgent("stock price of GOOG");
callAgent("What's the price of MSFT?");
callAgent("Can you find the stock price for an unknown company XYZ?");
}
}


The return value from this tool will be wrapped into a Map

### Best Practices[¶](#best-practices)

While you have considerable flexibility in defining your function, remember that simplicity enhances usability for the LLM. Consider these guidelines:

**Fewer Parameters are Better:**Minimize the number of parameters to reduce complexity.**Simple Data Types:**Favor primitive data types like`str`

and`int`

over custom classes whenever possible.**Meaningful Names:**The function's name and parameter names significantly influence how the LLM interprets and utilizes the tool. Choose names that clearly reflect the function's purpose and the meaning of its inputs. Avoid generic names like`do_stuff()`

or`beAgent()`

.**Build for Parallel Execution:**Improve function calling performance when multiple tools are run by building for asynchronous operation. For information on enabling parallel execution for tools, see[Increase tool performance with parallel execution](/adk-docs/tools-custom/performance/).

## Long Running Function Tools[¶](#long-run-tool)

This tool is designed to help you start and manage tasks that are handled outside the operation of your agent workflow, and require a significant amount of processing time, without blocking the agent's execution. This tool is a subclass of `FunctionTool`

.

When using a `LongRunningFunctionTool`

, your function can initiate the long-running operation and optionally return an **initial result**, such as a long-running operation id. Once a long running function tool is invoked the agent runner pauses the agent run and lets the agent client to decide whether to continue or wait until the long-running operation finishes. The agent client can query the progress of the long-running operation and send back an intermediate or final response. The agent can then continue with other tasks. An example is the human-in-the-loop scenario where the agent needs human approval before proceeding with a task.

Warning: Execution handling

Long Running Function Tools are designed to help you start and *manage* long running
tasks as part of your agent workflow, but ** not perform** the actual, long task.
For tasks that require significant time to complete, you should implement a separate
server to do the task.

Tip: Parallel execution

Depending on the type of tool you are building, designing for asynchronous
operation may be a better solution than creating a long running tool. For
more information, see
[Increase tool performance with parallel execution](/adk-docs/tools-custom/performance/).

### How it Works[¶](#how-it-works_1)

In Python, you wrap a function with `LongRunningFunctionTool`

. In Java, you pass a Method name to `LongRunningFunctionTool.create()`

. In TypeScript, you instantiate the `LongRunningFunctionTool`

class.

-
**Initiation:**When the LLM calls the tool, your function starts the long-running operation. -
**Initial Updates:**Your function should optionally return an initial result (e.g. the long-running operation id). The ADK framework takes the result and sends it back to the LLM packaged within a`FunctionResponse`

. This allows the LLM to inform the user (e.g., status, percentage complete, messages). And then the agent run is ended / paused. -
**Continue or Wait:**After each agent run is completed. Agent client can query the progress of the long-running operation and decide whether to continue the agent run with an intermediate response (to update the progress) or wait until a final response is retrieved. Agent client should send the intermediate or final response back to the agent for the next run. -
**Framework Handling:**The ADK framework manages the execution. It sends the intermediate or final`FunctionResponse`

sent by agent client to the LLM to generate a user friendly message.

### Creating the Tool[¶](#creating-the-tool)

Define your tool function and wrap it using the `LongRunningFunctionTool`

class:

# 1. Define the long running function
def ask_for_approval(
purpose: str, amount: float
) -> dict[str, Any]:
"""Ask for approval for the reimbursement."""
# create a ticket for the approval
# Send a notification to the approver with the link of the ticket
return {'status': 'pending', 'approver': 'Sean Zhou', 'purpose' : purpose, 'amount': amount, 'ticket-id': 'approval-ticket-1'}
def reimburse(purpose: str, amount: float) -> str:
"""Reimburse the amount of money to the employee."""
# send the reimbrusement request to payment vendor
return {'status': 'ok'}
# 2. Wrap the function with LongRunningFunctionTool
long_running_tool = LongRunningFunctionTool(func=ask_for_approval)


// 1. Define the long-running function
function askForApproval(args: {purpose: string; amount: number}) {
/**
* Ask for approval for the reimbursement.
*/
// create a ticket for the approval
// Send a notification to the approver with the link of the ticket
return {
"status": "pending",
"approver": "Sean Zhou",
"purpose": args.purpose,
"amount": args.amount,
"ticket-id": "approval-ticket-1",
};
}
// 2. Instantiate the LongRunningFunctionTool class with the long-running function
const longRunningTool = new LongRunningFunctionTool({
name: "ask_for_approval",
description: "Ask for approval for the reimbursement.",
parameters: z.object({
purpose: z.string().describe("The purpose of the reimbursement."),
amount: z.number().describe("The amount to reimburse."),
}),
execute: askForApproval,
});


import (
"google.golang.org/adk/agent"
"google.golang.org/adk/agent/llmagent"
"google.golang.org/adk/model/gemini"
"google.golang.org/adk/tool"
"google.golang.org/adk/tool/functiontool"
"google.golang.org/genai"
)
// CreateTicketArgs defines the arguments for our long-running tool.
type CreateTicketArgs struct {
Urgency string `json:"urgency" jsonschema:"The urgency level of the ticket."`
}
// CreateTicketResults defines the *initial* output of our long-running tool.
type CreateTicketResults struct {
Status string `json:"status"`
TicketId string `json:"ticket_id"`
}
// createTicketAsync simulates the *initiation* of a long-running ticket creation task.
func createTicketAsync(ctx tool.Context, args CreateTicketArgs) (CreateTicketResults, error) {
log.Printf("TOOL_EXEC: 'create_ticket_long_running' called with urgency: %s (Call ID: %s)\n", args.Urgency, ctx.FunctionCallID())
// "Generate" a ticket ID and return it in the initial response.
ticketID := "TICKET-ABC-123"
log.Printf("ACTION: Generated Ticket ID: %s for Call ID: %s\n", ticketID, ctx.FunctionCallID())
// In a real application, you would save the association between the
// FunctionCallID and the ticketID to handle the async response later.
return CreateTicketResults{
Status: "started",
TicketId: ticketID,
}, nil
}
func createTicketAgent(ctx context.Context) (agent.Agent, error) {
ticketTool, err := functiontool.New(
functiontool.Config{
Name: "create_ticket_long_running",
Description: "Creates a new support ticket with a specified urgency level.",
},
createTicketAsync,
)
if err != nil {
return nil, fmt.Errorf("failed to create long running tool: %w", err)
}
model, err := gemini.NewModel(ctx, "gemini-2.5-flash", &genai.ClientConfig{})
if err != nil {
return nil, fmt.Errorf("failed to create model: %v", err)
}
return llmagent.New(llmagent.Config{
Name: "ticket_agent",
Model: model,
Instruction: "You are a helpful assistant for creating support tickets. Provide the status of the ticket at each interaction.",
Tools: []tool.Tool{ticketTool},
})
}


import com.google.adk.agents.LlmAgent;
import com.google.adk.tools.LongRunningFunctionTool;
import java.util.HashMap;
import java.util.Map;
public class ExampleLongRunningFunction {
// Define your Long Running function.
// Ask for approval for the reimbursement.
public static Map<String, Object> askForApproval(String purpose, double amount) {
// Simulate creating a ticket and sending a notification
System.out.println(
"Simulating ticket creation for purpose: " + purpose + ", amount: " + amount);
// Send a notification to the approver with the link of the ticket
Map<String, Object> result = new HashMap<>();
result.put("status", "pending");
result.put("approver", "Sean Zhou");
result.put("purpose", purpose);
result.put("amount", amount);
result.put("ticket-id", "approval-ticket-1");
return result;
}
public static void main(String[] args) throws NoSuchMethodException {
// Pass the method to LongRunningFunctionTool.create
LongRunningFunctionTool approveTool =
LongRunningFunctionTool.create(ExampleLongRunningFunction.class, "askForApproval");
// Include the tool in the agent
LlmAgent approverAgent =
LlmAgent.builder()
// ...
.tools(approveTool)
.build();
}
}


### Intermediate / Final result Updates[¶](#intermediate-final-result-updates)

Agent client received an event with long running function calls and check the status of the ticket. Then Agent client can send the intermediate or final response back to update the progress. The framework packages this value (even if it's None) into the content of the `FunctionResponse`

sent back to the LLM.

Note: Long running function response with Resume feature

If your ADK agent workflow is configured with the
[Resume](/adk-docs/runtime/resume/) feature, you also must include
the Invocation ID (`invocation_id`

) parameter with the long running
function response. The Invocation ID you provide must be the same
invocation that generated the long running function request, otherwise
the system starts a new invocation with the response. If your
agent uses the Resume feature, consider including the Invocation ID
as a parameter with your long running function request, so it can be
included with the response. For more details on using the Resume
feature, see
[Resume stopped agents](/adk-docs/runtime/resume/).

## Applies to only Java ADK

When passing `ToolContext`

with Function Tools, ensure that one of the following is true:

-
The Schema is passed with the ToolContext parameter in the function signature, like:

OR -
The following

`-parameters`

flag is set to the mvn compiler plugin

# Agent Interaction
async def call_agent_async(query):
def get_long_running_function_call(event: Event) -> types.FunctionCall:
# Get the long running function call from the event
if not event.long_running_tool_ids or not event.content or not event.content.parts:
return
for part in event.content.parts:
if (
part
and part.function_call
and event.long_running_tool_ids
and part.function_call.id in event.long_running_tool_ids
):
return part.function_call
def get_function_response(event: Event, function_call_id: str) -> types.FunctionResponse:
# Get the function response for the fuction call with specified id.
if not event.content or not event.content.parts:
return
for part in event.content.parts:
if (
part
and part.function_response
and part.function_response.id == function_call_id
):
return part.function_response
content = types.Content(role='user', parts=[types.Part(text=query)])
session, runner = await setup_session_and_runner()
print("\nRunning agent...")
events_async = runner.run_async(
session_id=session.id, user_id=USER_ID, new_message=content
)
long_running_function_call, long_running_function_response, ticket_id = None, None, None
async for event in events_async:
# Use helper to check for the specific auth request event
if not long_running_function_call:
long_running_function_call = get_long_running_function_call(event)
else:
_potential_response = get_function_response(event, long_running_function_call.id)
if _potential_response: # Only update if we get a non-None response
long_running_function_response = _potential_response
ticket_id = long_running_function_response.response['ticket-id']
if event.content and event.content.parts:
if text := ''.join(part.text or '' for part in event.content.parts):
print(f'[{event.author}]: {text}')
if long_running_function_response:
# query the status of the correpsonding ticket via tciket_id
# send back an intermediate / final response
updated_response = long_running_function_response.model_copy(deep=True)
updated_response.response = {'status': 'approved'}
async for event in runner.run_async(
session_id=session.id, user_id=USER_ID, new_message=types.Content(parts=[types.Part(function_response = updated_response)], role='user')
):
if event.content and event.content.parts:
if text := ''.join(part.text or '' for part in event.content.parts):
print(f'[{event.author}]: {text}')


/**
* Copyright 2025 Google LLC
*
* Licensed under the Apache License, Version 2.0 (the "License");
* you may not use this file except in compliance with the License.
* You may obtain a copy of the License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed to in writing, software
* distributed under the License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
* See the License for the specific language governing permissions and
* limitations under the License.
*/
import {
LlmAgent,
Runner,
FunctionTool,
LongRunningFunctionTool,
InMemorySessionService,
Event,
stringifyContent,
} from "@google/adk";
import {z} from "zod";
import {Content, FunctionCall, FunctionResponse, createUserContent} from "@google/genai";
// 1. Define the long-running function
function askForApproval(args: {purpose: string; amount: number}) {
/**
* Ask for approval for the reimbursement.
*/
// create a ticket for the approval
// Send a notification to the approver with the link of the ticket
return {
"status": "pending",
"approver": "Sean Zhou",
"purpose": args.purpose,
"amount": args.amount,
"ticket-id": "approval-ticket-1",
};
}
// 2. Instantiate the LongRunningFunctionTool class with the long-running function
const longRunningTool = new LongRunningFunctionTool({
name: "ask_for_approval",
description: "Ask for approval for the reimbursement.",
parameters: z.object({
purpose: z.string().describe("The purpose of the reimbursement."),
amount: z.number().describe("The amount to reimburse."),
}),
execute: askForApproval,
});
function reimburse(args: {purpose: string; amount: number}) {
/**
* Reimburse the amount of money to the employee.
*/
// send the reimbursement request to payment vendor
return {status: "ok"};
}
const reimburseTool = new FunctionTool({
name: "reimburse",
description: "Reimburse the amount of money to the employee.",
parameters: z.object({
purpose: z.string().describe("The purpose of the reimbursement."),
amount: z.number().describe("The amount to reimburse."),
}),
execute: reimburse,
});
// 3. Use the tool in an Agent
const reimbursementAgent = new LlmAgent({
model: "gemini-2.5-flash",
name: "reimbursement_agent",
instruction: `
You are an agent whose job is to handle the reimbursement process for
the employees. If the amount is less than $100, you will automatically
approve the reimbursement.
If the amount is greater than $100, you will
ask for approval from the manager. If the manager approves, you will
call reimburse() to reimburse the amount to the employee. If the manager
rejects, you will inform the employee of the rejection.
`,
tools: [reimburseTool, longRunningTool],
});
const APP_NAME = "human_in_the_loop";
const USER_ID = "1234";
const SESSION_ID = "session1234";
// Session and Runner
async function setupSessionAndRunner() {
const sessionService = new InMemorySessionService();
const session = await sessionService.createSession({
appName: APP_NAME,
userId: USER_ID,
sessionId: SESSION_ID,
});
const runner = new Runner({
agent: reimbursementAgent,
appName: APP_NAME,
sessionService: sessionService,
});
return {session, runner};
}
function getLongRunningFunctionCall(event: Event): FunctionCall | undefined {
// Get the long-running function call from the event
if (
!event.longRunningToolIds ||
!event.content ||
!event.content.parts?.length
) {
return;
}
for (const part of event.content.parts) {
if (
part &&
part.functionCall &&
event.longRunningToolIds &&
part.functionCall.id &&
event.longRunningToolIds.includes(part.functionCall.id)
) {
return part.functionCall;
}
}
}
function getFunctionResponse(
event: Event,
functionCallId: string
): FunctionResponse | undefined {
// Get the function response for the function call with specified id.
if (!event.content || !event.content.parts?.length) {
return;
}
for (const part of event.content.parts) {
if (
part &&
part.functionResponse &&
part.functionResponse.id === functionCallId
) {
return part.functionResponse;
}
}
}
// Agent Interaction
async function callAgentAsync(query: string) {
let longRunningFunctionCall: FunctionCall | undefined;
let longRunningFunctionResponse: FunctionResponse | undefined;
let ticketId: string | undefined;
const content: Content = createUserContent(query);
const {session, runner} = await setupSessionAndRunner();
console.log("\nRunning agent...");
const events = runner.runAsync({
sessionId: session.id,
userId: USER_ID,
newMessage: content,
});
for await (const event of events) {
// Use helper to check for the specific auth request event
if (!longRunningFunctionCall) {
longRunningFunctionCall = getLongRunningFunctionCall(event);
} else {
const _potentialResponse = getFunctionResponse(
event,
longRunningFunctionCall.id!
);
if (_potentialResponse) {
// Only update if we get a non-None response
longRunningFunctionResponse = _potentialResponse;
ticketId = (
longRunningFunctionResponse.response as {[key: string]: any}
)[`ticket-id`];
}
}
const text = stringifyContent(event);
if (text) {
console.log(`[${event.author}]: ${text}`);
}
}
if (longRunningFunctionResponse) {
// query the status of the corresponding ticket via ticket_id
// send back an intermediate / final response
const updatedResponse = JSON.parse(
JSON.stringify(longRunningFunctionResponse)
);
updatedResponse.response = {status: "approved"};
for await (const event of runner.runAsync({
sessionId: session.id,
userId: USER_ID,
newMessage: createUserContent(JSON.stringify({functionResponse: updatedResponse})),
})) {
const text = stringifyContent(event);
if (text) {
console.log(`[${event.author}]: ${text}`);
}
}
}
}
async function main() {
// reimbursement that doesn't require approval
await callAgentAsync("Please reimburse 50$ for meals");
// reimbursement that requires approval
await callAgentAsync("Please reimburse 200$ for meals");
}
main();


The following example demonstrates a multi-turn workflow. First, the user asks the agent to create a ticket. The agent calls the long-running tool and the client captures the `FunctionCall`

ID. The client then simulates the asynchronous work completing by sending subsequent `FunctionResponse`

messages back to the agent to provide the ticket ID and final status.

// runTurn executes a single turn with the agent and returns the captured function call ID.
func runTurn(ctx context.Context, r *runner.Runner, sessionID, turnLabel string, content *genai.Content) string {
var funcCallID atomic.Value // Safely store the found ID.
fmt.Printf("\n--- %s ---\n", turnLabel)
for event, err := range r.Run(ctx, userID, sessionID, content, agent.RunConfig{
StreamingMode: agent.StreamingModeNone,
}) {
if err != nil {
fmt.Printf("\nAGENT_ERROR: %v\n", err)
continue
}
// Print a summary of the event for clarity.
printEventSummary(event, turnLabel)
// Capture the function call ID from the event.
for _, part := range event.Content.Parts {
if fc := part.FunctionCall; fc != nil {
if fc.Name == "create_ticket_long_running" {
funcCallID.Store(fc.ID)
}
}
}
}
if id, ok := funcCallID.Load().(string); ok {
return id
}
return ""
}
func main() {
ctx := context.Background()
ticketAgent, err := createTicketAgent(ctx)
if err != nil {
log.Fatalf("Failed to create agent: %v", err)
}
// Setup the runner and session.
sessionService := session.InMemoryService()
session, err := sessionService.Create(ctx, &session.CreateRequest{AppName: appName, UserID: userID})
if err != nil {
log.Fatalf("Failed to create session: %v", err)
}
r, err := runner.New(runner.Config{AppName: appName, Agent: ticketAgent, SessionService: sessionService})
if err != nil {
log.Fatalf("Failed to create runner: %v", err)
}
// --- Turn 1: User requests to create a ticket. ---
initialUserMessage := genai.NewContentFromText("Create a high urgency ticket for me.", genai.RoleUser)
funcCallID := runTurn(ctx, r, session.Session.ID(), "Turn 1: User Request", initialUserMessage)
if funcCallID == "" {
log.Fatal("ERROR: Tool 'create_ticket_long_running' not called in Turn 1.")
}
fmt.Printf("ACTION: Captured FunctionCall ID: %s\n", funcCallID)
// --- Turn 2: App provides the final status of the ticket. ---
// In a real application, the ticketID would be retrieved from a database
// using the funcCallID. For this example, we'll use the same ID.
ticketID := "TICKET-ABC-123"
willContinue := false // Signal that this is the final response.
ticketStatusResponse := &genai.FunctionResponse{
Name: "create_ticket_long_running",
ID: funcCallID,
Response: map[string]any{
"status": "approved",
"ticket_id": ticketID,
},
WillContinue: &willContinue,
}
appResponseWithStatus := &genai.Content{
Role: string(genai.RoleUser),
Parts: []*genai.Part{{FunctionResponse: ticketStatusResponse}},
}
runTurn(ctx, r, session.Session.ID(), "Turn 2: App provides ticket status", appResponseWithStatus)
fmt.Println("Long running function completed successfully.")
}
// printEventSummary provides a readable log of agent and LLM interactions.
func printEventSummary(event *session.Event, turnLabel string) {
for _, part := range event.Content.Parts {
// Check for a text part.
if part.Text != "" {
fmt.Printf("[%s][%s_TEXT]: %s\n", turnLabel, event.Author, part.Text)
}
// Check for a function call part.
if fc := part.FunctionCall; fc != nil {
fmt.Printf("[%s][%s_CALL]: %s(%v) ID: %s\n", turnLabel, event.Author, fc.Name, fc.Args, fc.ID)
}
}
}


import com.google.adk.agents.LlmAgent;
import com.google.adk.events.Event;
import com.google.adk.runner.InMemoryRunner;
import com.google.adk.runner.Runner;
import com.google.adk.sessions.Session;
import com.google.adk.tools.Annotations.Schema;
import com.google.adk.tools.LongRunningFunctionTool;
import com.google.adk.tools.ToolContext;
import com.google.common.collect.ImmutableList;
import com.google.common.collect.ImmutableMap;
import com.google.genai.types.Content;
import com.google.genai.types.FunctionCall;
import com.google.genai.types.FunctionResponse;
import com.google.genai.types.Part;
import java.util.Optional;
import java.util.UUID;
import java.util.concurrent.atomic.AtomicReference;
import java.util.stream.Collectors;
public class LongRunningFunctionExample {
private static String USER_ID = "user123";
@Schema(
name = "create_ticket_long_running",
description = """
Creates a new support ticket with a specified urgency level.
Examples of urgency are 'high', 'medium', or 'low'.
The ticket creation is a long-running process, and its ID will be provided when ready.
""")
public static void createTicketAsync(
@Schema(
name = "urgency",
description =
"The urgency level for the new ticket, such as 'high', 'medium', or 'low'.")
String urgency,
@Schema(name = "toolContext") // Ensures ADK injection
ToolContext toolContext) {
System.out.printf(
"TOOL_EXEC: 'create_ticket_long_running' called with urgency: %s (Call ID: %s)%n",
urgency, toolContext.functionCallId().orElse("N/A"));
}
public static void main(String[] args) {
LlmAgent agent =
LlmAgent.builder()
.name("ticket_agent")
.description("Agent for creating tickets via a long-running task.")
.model("gemini-2.0-flash")
.tools(
ImmutableList.of(
LongRunningFunctionTool.create(
LongRunningFunctionExample.class, "createTicketAsync")))
.build();
Runner runner = new InMemoryRunner(agent);
Session session =
runner.sessionService().createSession(agent.name(), USER_ID, null, null).blockingGet();
// --- Turn 1: User requests ticket ---
System.out.println("\n--- Turn 1: User Request ---");
Content initialUserMessage =
Content.fromParts(Part.fromText("Create a high urgency ticket for me."));
AtomicReference<String> funcCallIdRef = new AtomicReference<>();
runner
.runAsync(USER_ID, session.id(), initialUserMessage)
.blockingForEach(
event -> {
printEventSummary(event, "T1");
if (funcCallIdRef.get() == null) { // Capture the first relevant function call ID
event.content().flatMap(Content::parts).orElse(ImmutableList.of()).stream()
.map(Part::functionCall)
.flatMap(Optional::stream)
.filter(fc -> "create_ticket_long_running".equals(fc.name().orElse("")))
.findFirst()
.flatMap(FunctionCall::id)
.ifPresent(funcCallIdRef::set);
}
});
if (funcCallIdRef.get() == null) {
System.out.println("ERROR: Tool 'create_ticket_long_running' not called in Turn 1.");
return;
}
System.out.println("ACTION: Captured FunctionCall ID: " + funcCallIdRef.get());
// --- Turn 2: App provides initial ticket_id (simulating async tool completion) ---
System.out.println("\n--- Turn 2: App provides ticket_id ---");
String ticketId = "TICKET-" + UUID.randomUUID().toString().substring(0, 8).toUpperCase();
FunctionResponse ticketCreatedFuncResponse =
FunctionResponse.builder()
.name("create_ticket_long_running")
.id(funcCallIdRef.get())
.response(ImmutableMap.of("ticket_id", ticketId))
.build();
Content appResponseWithTicketId =
Content.builder()
.parts(
ImmutableList.of(
Part.builder().functionResponse(ticketCreatedFuncResponse).build()))
.role("user")
.build();
runner
.runAsync(USER_ID, session.id(), appResponseWithTicketId)
.blockingForEach(event -> printEventSummary(event, "T2"));
System.out.println("ACTION: Sent ticket_id " + ticketId + " to agent.");
// --- Turn 3: App provides ticket status update ---
System.out.println("\n--- Turn 3: App provides ticket status ---");
FunctionResponse ticketStatusFuncResponse =
FunctionResponse.builder()
.name("create_ticket_long_running")
.id(funcCallIdRef.get())
.response(ImmutableMap.of("status", "approved", "ticket_id", ticketId))
.build();
Content appResponseWithStatus =
Content.builder()
.parts(
ImmutableList.of(Part.builder().functionResponse(ticketStatusFuncResponse).build()))
.role("user")
.build();
runner
.runAsync(USER_ID, session.id(), appResponseWithStatus)
.blockingForEach(event -> printEventSummary(event, "T3_FINAL"));
System.out.println("Long running function completed successfully.");
}
private static void printEventSummary(Event event, String turnLabel) {
event
.content()
.ifPresent(
content -> {
String text =
content.parts().orElse(ImmutableList.of()).stream()
.map(part -> part.text().orElse(""))
.filter(s -> !s.isEmpty())
.collect(Collectors.joining(" "));
if (!text.isEmpty()) {
System.out.printf("[%s][%s_TEXT]: %s%n", turnLabel, event.author(), text);
}
content.parts().orElse(ImmutableList.of()).stream()
.map(Part::functionCall)
.flatMap(Optional::stream)
.findFirst() // Assuming one function call per relevant event for simplicity
.ifPresent(
fc ->
System.out.printf(
"[%s][%s_CALL]: %s(%s) ID: %s%n",
turnLabel,
event.author(),
fc.name().orElse("N/A"),
fc.args().orElse(ImmutableMap.of()),
fc.id().orElse("N/A")));
});
}
}


## Python complete example: File Processing Simulation

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
from typing import Any
from google.adk.agents import Agent
from google.adk.events import Event
from google.adk.runners import Runner
from google.adk.tools import LongRunningFunctionTool
from google.adk.sessions import InMemorySessionService
from google.genai import types
# 1. Define the long running function
def ask_for_approval(
purpose: str, amount: float
) -> dict[str, Any]:
"""Ask for approval for the reimbursement."""
# create a ticket for the approval
# Send a notification to the approver with the link of the ticket
return {'status': 'pending', 'approver': 'Sean Zhou', 'purpose' : purpose, 'amount': amount, 'ticket-id': 'approval-ticket-1'}
def reimburse(purpose: str, amount: float) -> str:
"""Reimburse the amount of money to the employee."""
# send the reimbrusement request to payment vendor
return {'status': 'ok'}
# 2. Wrap the function with LongRunningFunctionTool
long_running_tool = LongRunningFunctionTool(func=ask_for_approval)
# 3. Use the tool in an Agent
file_processor_agent = Agent(
# Use a model compatible with function calling
model="gemini-2.0-flash",
name='reimbursement_agent',
instruction="""
You are an agent whose job is to handle the reimbursement process for
the employees. If the amount is less than $100, you will automatically
approve the reimbursement.
If the amount is greater than $100, you will
ask for approval from the manager. If the manager approves, you will
call reimburse() to reimburse the amount to the employee. If the manager
rejects, you will inform the employee of the rejection.
""",
tools=[reimburse, long_running_tool]
)
APP_NAME = "human_in_the_loop"
USER_ID = "1234"
SESSION_ID = "session1234"
# Session and Runner
async def setup_session_and_runner():
session_service = InMemorySessionService()
session = await session_service.create_session(app_name=APP_NAME, user_id=USER_ID, session_id=SESSION_ID)
runner = Runner(agent=file_processor_agent, app_name=APP_NAME, session_service=session_service)
return session, runner
# Agent Interaction
async def call_agent_async(query):
def get_long_running_function_call(event: Event) -> types.FunctionCall:
# Get the long running function call from the event
if not event.long_running_tool_ids or not event.content or not event.content.parts:
return
for part in event.content.parts:
if (
part
and part.function_call
and event.long_running_tool_ids
and part.function_call.id in event.long_running_tool_ids
):
return part.function_call
def get_function_response(event: Event, function_call_id: str) -> types.FunctionResponse:
# Get the function response for the fuction call with specified id.
if not event.content or not event.content.parts:
return
for part in event.content.parts:
if (
part
and part.function_response
and part.function_response.id == function_call_id
):
return part.function_response
content = types.Content(role='user', parts=[types.Part(text=query)])
session, runner = await setup_session_and_runner()
print("\nRunning agent...")
events_async = runner.run_async(
session_id=session.id, user_id=USER_ID, new_message=content
)
long_running_function_call, long_running_function_response, ticket_id = None, None, None
async for event in events_async:
# Use helper to check for the specific auth request event
if not long_running_function_call:
long_running_function_call = get_long_running_function_call(event)
else:
_potential_response = get_function_response(event, long_running_function_call.id)
if _potential_response: # Only update if we get a non-None response
long_running_function_response = _potential_response
ticket_id = long_running_function_response.response['ticket-id']
if event.content and event.content.parts:
if text := ''.join(part.text or '' for part in event.content.parts):
print(f'[{event.author}]: {text}')
if long_running_function_response:
# query the status of the correpsonding ticket via tciket_id
# send back an intermediate / final response
updated_response = long_running_function_response.model_copy(deep=True)
updated_response.response = {'status': 'approved'}
async for event in runner.run_async(
session_id=session.id, user_id=USER_ID, new_message=types.Content(parts=[types.Part(function_response = updated_response)], role='user')
):
if event.content and event.content.parts:
if text := ''.join(part.text or '' for part in event.content.parts):
print(f'[{event.author}]: {text}')
# Note: In Colab, you can directly use 'await' at the top level.
# If running this code as a standalone Python script, you'll need to use asyncio.run() or manage the event loop.
# reimbursement that doesn't require approval
# asyncio.run(call_agent_async("Please reimburse 50$ for meals"))
await call_agent_async("Please reimburse 50$ for meals") # For Notebooks, uncomment this line and comment the above line
# reimbursement that requires approval
# asyncio.run(call_agent_async("Please reimburse 200$ for meals"))
await call_agent_async("Please reimburse 200$ for meals") # For Notebooks, uncomment this line and comment the above line


#### Key aspects of this example[¶](#key-aspects-of-this-example)

-
: Wraps the supplied method/function; the framework handles sending yielded updates and the final return value as sequential FunctionResponses.`LongRunningFunctionTool`

-
**Agent instruction**: Directs the LLM to use the tool and understand the incoming FunctionResponse stream (progress vs. completion) for user updates. -
**Final return**: The function returns the final result dictionary, which is sent in the concluding FunctionResponse to indicate completion.

## Agent-as-a-Tool[¶](#agent-tool)

This powerful feature allows you to leverage the capabilities of other agents within your system by calling them as tools. The Agent-as-a-Tool enables you to invoke another agent to perform a specific task, effectively **delegating responsibility**. This is conceptually similar to creating a Python function that calls another agent and uses the agent's response as the function's return value.

### Key difference from sub-agents[¶](#key-difference-from-sub-agents)

It's important to distinguish an Agent-as-a-Tool from a Sub-Agent.

-
**Agent-as-a-Tool:**When Agent A calls Agent B as a tool (using Agent-as-a-Tool), Agent B's answer is**passed back**to Agent A, which then summarizes the answer and generates a response to the user. Agent A retains control and continues to handle future user input. -
**Sub-agent:**When Agent A calls Agent B as a sub-agent, the responsibility of answering the user is completely**transferred to Agent B**. Agent A is effectively out of the loop. All subsequent user input will be answered by Agent B.

### Usage[¶](#usage)

To use an agent as a tool, wrap the agent with the AgentTool class.

### Customization[¶](#customization)

The `AgentTool`

class provides the following attributes for customizing its behavior:

**skip_summarization: bool:**If set to True, the framework will**bypass the LLM-based summarization**of the tool agent's response. This can be useful when the tool's response is already well-formatted and requires no further processing.

## Example

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
from google.adk.tools.agent_tool import AgentTool
from google.genai import types
APP_NAME="summary_agent"
USER_ID="user1234"
SESSION_ID="1234"
summary_agent = Agent(
model="gemini-2.0-flash",
name="summary_agent",
instruction="""You are an expert summarizer. Please read the following text and provide a concise summary.""",
description="Agent to summarize text",
)
root_agent = Agent(
model='gemini-2.0-flash',
name='root_agent',
instruction="""You are a helpful assistant. When the user provides a text, use the 'summarize' tool to generate a summary. Always forward the user's message exactly as received to the 'summarize' tool, without modifying or summarizing it yourself. Present the response from the tool to the user.""",
tools=[AgentTool(agent=summary_agent, skip_summarization=True)]
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
long_text = """Quantum computing represents a fundamentally different approach to computation,
leveraging the bizarre principles of quantum mechanics to process information. Unlike classical computers
that rely on bits representing either 0 or 1, quantum computers use qubits which can exist in a state of superposition - effectively
being 0, 1, or a combination of both simultaneously. Furthermore, qubits can become entangled,
meaning their fates are intertwined regardless of distance, allowing for complex correlations. This parallelism and
interconnectedness grant quantum computers the potential to solve specific types of incredibly complex problems - such
as drug discovery, materials science, complex system optimization, and breaking certain types of cryptography - far
faster than even the most powerful classical supercomputers could ever achieve, although the technology is still largely in its developmental stages."""
# Note: In Colab, you can directly use 'await' at the top level.
# If running this code as a standalone Python script, you'll need to use asyncio.run() or manage the event loop.
await call_agent_async(long_text)


/**
* Copyright 2025 Google LLC
*
* Licensed under the Apache License, Version 2.0 (the "License");
* you may not use this file except in compliance with the License.
* You may obtain a copy of the License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed to in writing, software
* distributed under the License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
* See the License for the specific language governing permissions and
* limitations under the License.
*/
import {
AgentTool,
InMemoryRunner,
LlmAgent,
} from '@google/adk';
import {Part, createUserContent} from '@google/genai';
/**
* This example demonstrates how to use an agent as a tool.
*/
async function main() {
// Define the summarization agent that will be used as a tool
const summaryAgent = new LlmAgent({
name: 'summary_agent',
model: 'gemini-2.5-flash',
description: 'Agent to summarize text',
instruction:
'You are an expert summarizer. Please read the following text and provide a concise summary.',
});
// Define the main agent that uses the summarization agent as a tool.
// skipSummarization is set to true, so the main_agent will directly output
// the result from the summary_agent without further processing.
const mainAgent = new LlmAgent({
name: 'main_agent',
model: 'gemini-2.5-flash',
instruction:
"You are a helpful assistant. When the user provides a text, use the 'summary_agent' tool to generate a summary. Always forward the user's message exactly as received to the 'summary_agent' tool, without modifying or summarizing it yourself. Present the response from the tool to the user.",
tools: [new AgentTool({agent: summaryAgent, skipSummarization: true})],
});
const appName = 'agent-as-a-tool-app';
const runner = new InMemoryRunner({agent: mainAgent, appName});
const longText = `Quantum computing represents a fundamentally different approach to computation,
leveraging the bizarre principles of quantum mechanics to process information. Unlike classical computers
that rely on bits representing either 0 or 1, quantum computers use qubits which can exist in a state of superposition - effectively
being 0, 1, or a combination of both simultaneously. Furthermore, qubits can become entangled,
meaning their fates are intertwined regardless of distance, allowing for complex correlations. This parallelism and
interconnectedness grant quantum computers the potential to solve specific types of incredibly complex problems - such
as drug discovery, materials science, complex system optimization, and breaking certain types of cryptography - far
faster than even the most powerful classical supercomputers could ever achieve, although the technology is still largely in its developmental stages.`;
// Create the session before running the agent
await runner.sessionService.createSession({
appName,
userId: 'user1',
sessionId: 'session1',
});
// Run the agent with the long text to summarize
const events = runner.runAsync({
userId: 'user1',
sessionId: 'session1',
newMessage: createUserContent(longText),
});
// Print the final response from the agent
console.log('Agent Response:');
for await (const event of events) {
if (event.content?.parts?.length) {
const responsePart = event.content.parts.find((p: Part) => p.functionResponse);
if (responsePart && responsePart.functionResponse) {
console.log(responsePart.functionResponse.response);
}
}
}
}
main();


import (
"google.golang.org/adk/agent"
"google.golang.org/adk/agent/llmagent"
"google.golang.org/adk/model/gemini"
"google.golang.org/adk/tool"
"google.golang.org/adk/tool/agenttool"
"google.golang.org/genai"
)
// createSummarizerAgent creates an agent whose sole purpose is to summarize text.
func createSummarizerAgent(ctx context.Context) (agent.Agent, error) {
model, err := gemini.NewModel(ctx, "gemini-2.5-flash", &genai.ClientConfig{})
if err != nil {
return nil, err
}
return llmagent.New(llmagent.Config{
Name: "SummarizerAgent",
Model: model,
Instruction: "You are an expert at summarizing text. Take the user's input and provide a concise summary.",
Description: "An agent that summarizes text.",
})
}
// createMainAgent creates the primary agent that will use the summarizer agent as a tool.
func createMainAgent(ctx context.Context, tools ...tool.Tool) (agent.Agent, error) {
model, err := gemini.NewModel(ctx, "gemini-2.5-flash", &genai.ClientConfig{})
if err != nil {
return nil, err
}
return llmagent.New(llmagent.Config{
Name: "MainAgent",
Model: model,
Instruction: "You are a helpful assistant. If you are asked to summarize a long text, use the 'summarize' tool. " +
"After getting the summary, present it to the user by saying 'Here is a summary of the text:'.",
Description: "The main agent that can delegate tasks.",
Tools: tools,
})
}
func RunAgentAsToolSimulation() {
ctx := context.Background()
// 1. Create the Tool Agent (Summarizer)
summarizerAgent, err := createSummarizerAgent(ctx)
if err != nil {
log.Fatalf("Failed to create summarizer agent: %v", err)
}
// 2. Wrap the Tool Agent in an AgentTool
summarizeTool := agenttool.New(summarizerAgent, &agenttool.Config{
SkipSummarization: true,
})
// 3. Create the Main Agent and provide it with the AgentTool
mainAgent, err := createMainAgent(ctx, summarizeTool)
if err != nil {
log.Fatalf("Failed to create main agent: %v", err)
}
// 4. Run the main agent
prompt := `
Please summarize this text for me:
Quantum computing represents a fundamentally different approach to computation,
leveraging the bizarre principles of quantum mechanics to process information. Unlike classical computers
that rely on bits representing either 0 or 1, quantum computers use qubits which can exist in a state of superposition - effectively
being 0, 1, or a combination of both simultaneously. Furthermore, qubits can become entangled,
meaning their fates are intertwined regardless of distance, allowing for complex correlations. This parallelism and
interconnectedness grant quantum computers the potential to solve specific types of incredibly complex problems - such
as drug discovery, materials science, complex system optimization, and breaking certain types of cryptography - far
faster than even the most powerful classical supercomputers could ever achieve, although the technology is still largely in its developmental stages.
`
fmt.Printf("\nPrompt: %s\nResponse: ", prompt)
callAgent(context.Background(), mainAgent, prompt)
fmt.Println("\n---")
}


import com.google.adk.agents.LlmAgent;
import com.google.adk.events.Event;
import com.google.adk.runner.InMemoryRunner;
import com.google.adk.sessions.Session;
import com.google.adk.tools.AgentTool;
import com.google.genai.types.Content;
import com.google.genai.types.Part;
import io.reactivex.rxjava3.core.Flowable;
public class AgentToolCustomization {
private static final String APP_NAME = "summary_agent";
private static final String USER_ID = "user1234";
public static void initAgentAndRun(String prompt) {
LlmAgent summaryAgent =
LlmAgent.builder()
.model("gemini-2.0-flash")
.name("summaryAgent")
.instruction(
"You are an expert summarizer. Please read the following text and provide a concise summary.")
.description("Agent to summarize text")
.build();
// Define root_agent
LlmAgent rootAgent =
LlmAgent.builder()
.model("gemini-2.0-flash")
.name("rootAgent")
.instruction(
"You are a helpful assistant. When the user provides a text, always use the 'summaryAgent' tool to generate a summary. Always forward the user's message exactly as received to the 'summaryAgent' tool, without modifying or summarizing it yourself. Present the response from the tool to the user.")
.description("Assistant agent")
.tools(AgentTool.create(summaryAgent, true)) // Set skipSummarization to true
.build();
// Create an InMemoryRunner
InMemoryRunner runner = new InMemoryRunner(rootAgent, APP_NAME);
// InMemoryRunner automatically creates a session service. Create a session using the service
Session session = runner.sessionService().createSession(APP_NAME, USER_ID).blockingGet();
Content userMessage = Content.fromParts(Part.fromText(prompt));
// Run the agent
Flowable<Event> eventStream = runner.runAsync(USER_ID, session.id(), userMessage);
// Stream event response
eventStream.blockingForEach(
event -> {
if (event.finalResponse()) {
System.out.println(event.stringifyContent());
}
});
}
public static void main(String[] args) {
String longText =
"""
Quantum computing represents a fundamentally different approach to computation,
leveraging the bizarre principles of quantum mechanics to process information. Unlike classical computers
that rely on bits representing either 0 or 1, quantum computers use qubits which can exist in a state of superposition - effectively
being 0, 1, or a combination of both simultaneously. Furthermore, qubits can become entangled,
meaning their fates are intertwined regardless of distance, allowing for complex correlations. This parallelism and
interconnectedness grant quantum computers the potential to solve specific types of incredibly complex problems - such
as drug discovery, materials science, complex system optimization, and breaking certain types of cryptography - far
faster than even the most powerful classical supercomputers could ever achieve, although the technology is still largely in its developmental stages.""";
initAgentAndRun(longText);
}
}


### How it works[¶](#how-it-works_2)

- When the
`main_agent`

receives the long text, its instruction tells it to use the 'summarize' tool for long texts. - The framework recognizes 'summarize' as an
`AgentTool`

that wraps the`summary_agent`

. - Behind the scenes, the
`main_agent`

will call the`summary_agent`

with the long text as input. - The
`summary_agent`

will process the text according to its instruction and generate a summary. **The response from the**`summary_agent`

is then passed back to the`main_agent`

.- The
`main_agent`

can then take the summary and formulate its final response to the user (e.g., "Here's a summary of the text: ...")

---
<!-- Source: https://google.github.io/adk-docs/tools-custom/ -->

# Custom Tools for ADK¶

# Custom Tools for ADK[¶](#custom-tools-for-adk)

In an ADK agent workflow, Tools are programming functions with structured input
and output that can be called by an ADK Agent to perform actions. ADK Tools
function similarly to how you use a
[Function Call](https://ai.google.dev/gemini-api/docs/function-calling)
with Gemini or other generative AI models. You can perform various actions and
programming functions with an ADK Tool, such as:

- Querying databases
- Making API requests: getting weather data, booking systems
- Searching the web
- Executing code snippets
- Retrieving information from documents (RAG)
- Interacting with other software or services

Before building your own Tools for ADK, check out the
** ADK Tools list**
for pre-built tools you can use with ADK Agents.

## What is a Tool?[¶](#what-is-a-tool)

In the context of ADK, a Tool represents a specific capability provided to an AI agent, enabling it to perform actions and interact with the world beyond its core text generation and reasoning abilities. What distinguishes capable agents from basic language models is often their effective use of tools.

Technically, a tool is typically a modular code component—**like a Python, Java, or TypeScript
function**, a class method, or even another specialized agent—designed to
execute a distinct, predefined task. These tasks often involve interacting with
external systems or data.

### Key Characteristics[¶](#key-characteristics)

**Action-Oriented:** Tools perform specific actions for an agent, such as
searching for information, calling an API, or performing calculations.

**Extends Agent capabilities:** They empower agents to access real-time information, affect external systems, and overcome the knowledge limitations inherent in their training data.

**Execute predefined logic:** Crucially, tools execute specific, developer-defined logic. They do not possess their own independent reasoning capabilities like the agent's core Large Language Model (LLM). The LLM reasons about which tool to use, when, and with what inputs, but the tool itself just executes its designated function.

## How Agents Use Tools[¶](#how-agents-use-tools)

Agents leverage tools dynamically through mechanisms often involving function calling. The process generally follows these steps:

**Reasoning:**The agent's LLM analyzes its system instruction, conversation history, and user request.**Selection:**Based on the analysis, the LLM decides on which tool, if any, to execute, based on the tools available to the agent and the docstrings that describes each tool.**Invocation:**The LLM generates the required arguments (inputs) for the selected tool and triggers its execution.**Observation:**The agent receives the output (result) returned by the tool.**Finalization:**The agent incorporates the tool's output into its ongoing reasoning process to formulate the next response, decide the subsequent step, or determine if the goal has been achieved.

Think of the tools as a specialized toolkit that the agent's intelligent core (the LLM) can access and utilize as needed to accomplish complex tasks.

## Tool Types in ADK[¶](#tool-types-in-adk)

ADK offers flexibility by supporting several types of tools:

Tools created by you, tailored to your specific application's needs.[Function Tools](/adk-docs/tools-custom/function-tools/):Define standard synchronous functions or methods in your code (e.g., Python def).[Functions/Methods](/adk-docs/tools-custom/function-tools/#1-function-tool):Use another, potentially specialized, agent as a tool for a parent agent.[Agents-as-Tools](/adk-docs/tools-custom/function-tools/#3-agent-as-a-tool):Support for tools that perform asynchronous operations or take significant time to complete.[Long Running Function Tools](/adk-docs/tools-custom/function-tools/#2-long-running-function-tool):

Ready-to-use tools provided by the framework for common tasks. Examples: Google Search, Code Execution, Retrieval-Augmented Generation (RAG).[Built-in Tools](/adk-docs/tools/built-in-tools/):**Third-Party Tools:**Integrate tools seamlessly from popular external libraries.

Navigate to the respective documentation pages linked above for detailed information and examples for each tool type.

## Referencing Tool in Agent’s Instructions[¶](#referencing-tool-in-agents-instructions)

Within an agent's instructions, you can directly reference a tool by using its **function name.** If the tool's **function name** and **docstring** are sufficiently descriptive, your instructions can primarily focus on **when the Large Language Model (LLM) should utilize the tool**. This promotes clarity and helps the model understand the intended use of each tool.

It is **crucial to clearly instruct the agent on how to handle different return values** that a tool might produce. For example, if a tool returns an error message, your instructions should specify whether the agent should retry the operation, give up on the task, or request additional information from the user.

Furthermore, ADK supports the sequential use of tools, where the output of one tool can serve as the input for another. When implementing such workflows, it's important to **describe the intended sequence of tool usage** within the agent's instructions to guide the model through the necessary steps.

### Example[¶](#example)

The following example showcases how an agent can use tools by **referencing their function names in its instructions**. It also demonstrates how to guide the agent to **handle different return values from tools**, such as success or error messages, and how to orchestrate the **sequential use of multiple tools** to accomplish a task.

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
from google.adk.tools import FunctionTool
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.genai import types
APP_NAME="weather_sentiment_agent"
USER_ID="user1234"
SESSION_ID="1234"
MODEL_ID="gemini-2.0-flash"
# Tool 1
def get_weather_report(city: str) -> dict:
"""Retrieves the current weather report for a specified city.
Returns:
dict: A dictionary containing the weather information with a 'status' key ('success' or 'error') and a 'report' key with the weather details if successful, or an 'error_message' if an error occurred.
"""
if city.lower() == "london":
return {"status": "success", "report": "The current weather in London is cloudy with a temperature of 18 degrees Celsius and a chance of rain."}
elif city.lower() == "paris":
return {"status": "success", "report": "The weather in Paris is sunny with a temperature of 25 degrees Celsius."}
else:
return {"status": "error", "error_message": f"Weather information for '{city}' is not available."}
weather_tool = FunctionTool(func=get_weather_report)
# Tool 2
def analyze_sentiment(text: str) -> dict:
"""Analyzes the sentiment of the given text.
Returns:
dict: A dictionary with 'sentiment' ('positive', 'negative', or 'neutral') and a 'confidence' score.
"""
if "good" in text.lower() or "sunny" in text.lower():
return {"sentiment": "positive", "confidence": 0.8}
elif "rain" in text.lower() or "bad" in text.lower():
return {"sentiment": "negative", "confidence": 0.7}
else:
return {"sentiment": "neutral", "confidence": 0.6}
sentiment_tool = FunctionTool(func=analyze_sentiment)
# Agent
weather_sentiment_agent = Agent(
model=MODEL_ID,
name='weather_sentiment_agent',
instruction="""You are a helpful assistant that provides weather information and analyzes the sentiment of user feedback.
**If the user asks about the weather in a specific city, use the 'get_weather_report' tool to retrieve the weather details.**
**If the 'get_weather_report' tool returns a 'success' status, provide the weather report to the user.**
**If the 'get_weather_report' tool returns an 'error' status, inform the user that the weather information for the specified city is not available and ask if they have another city in mind.**
**After providing a weather report, if the user gives feedback on the weather (e.g., 'That's good' or 'I don't like rain'), use the 'analyze_sentiment' tool to understand their sentiment.** Then, briefly acknowledge their sentiment.
You can handle these tasks sequentially if needed.""",
tools=[weather_tool, sentiment_tool]
)
async def main():
"""Main function to run the agent asynchronously."""
# Session and Runner Setup
session_service = InMemorySessionService()
# Use 'await' to correctly create the session
await session_service.create_session(app_name=APP_NAME, user_id=USER_ID, session_id=SESSION_ID)
runner = Runner(agent=weather_sentiment_agent, app_name=APP_NAME, session_service=session_service)
# Agent Interaction
query = "weather in london?"
print(f"User Query: {query}")
content = types.Content(role='user', parts=[types.Part(text=query)])
# The runner's run method handles the async loop internally
events = runner.run(user_id=USER_ID, session_id=SESSION_ID, new_message=content)
for event in events:
if event.is_final_response():
final_response = event.content.parts[0].text
print("Agent Response:", final_response)
# Standard way to run the main async function
if __name__ == "__main__":
asyncio.run(main())


/**
* Copyright 2025 Google LLC
*
* Licensed under the Apache License, Version 2.0 (the "License");
* you may not use this file except in compliance with the License.
* You may obtain a copy of the License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed to in writing, software
* distributed under the License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
* See the License for the specific language governing permissions and
* limitations under the License.
*/
import { LlmAgent, FunctionTool, InMemoryRunner, isFinalResponse, stringifyContent } from "@google/adk";
import { z } from "zod";
import { Content, createUserContent } from "@google/genai";
/**
* Retrieves the current weather report for a specified city.
*/
function getWeatherReport(params: { city: string }): Record<string, any> {
if (params.city.toLowerCase().includes("london")) {
return {
"status": "success",
"report": "The current weather in London is cloudy with a " +
"temperature of 18 degrees Celsius and a chance of rain.",
};
}
if (params.city.toLowerCase().includes("paris")) {
return {
"status": "success",
"report": "The weather in Paris is sunny with a temperature of 25 " +
"degrees Celsius.",
};
}
return {
"status": "error",
"error_message": `Weather information for '${params.city}' is not available.`,
};
}
/**
* Analyzes the sentiment of a given text.
*/
function analyzeSentiment(params: { text: string }): Record<string, any> {
if (params.text.includes("cloudy") || params.text.includes("rain")) {
return { "status": "success", "sentiment": "negative" };
}
if (params.text.includes("sunny")) {
return { "status": "success", "sentiment": "positive" };
}
return { "status": "success", "sentiment": "neutral" };
}
const weatherTool = new FunctionTool({
name: "get_weather_report",
description: "Retrieves the current weather report for a specified city.",
parameters: z.object({
city: z.string().describe("The city to get the weather for."),
}),
execute: getWeatherReport,
});
const sentimentTool = new FunctionTool({
name: "analyze_sentiment",
description: "Analyzes the sentiment of a given text.",
parameters: z.object({
text: z.string().describe("The text to analyze the sentiment of."),
}),
execute: analyzeSentiment,
});
const instruction = `
You are a helpful assistant that first checks the weather and then analyzes
its sentiment.
Follow these steps:
1. Use the 'get_weather_report' tool to get the weather for the requested
city.
2. If the 'get_weather_report' tool returns an error, inform the user about
the error and stop.
3. If the weather report is available, use the 'analyze_sentiment' tool to
determine the sentiment of the weather report.
4. Finally, provide a summary to the user, including the weather report and
its sentiment.
`;
const agent = new LlmAgent({
name: "weather_sentiment_agent",
instruction: instruction,
tools: [weatherTool, sentimentTool],
model: "gemini-2.5-flash"
});
async function main() {
const runner = new InMemoryRunner({ agent: agent, appName: "weather_sentiment_app" });
await runner.sessionService.createSession({
appName: "weather_sentiment_app",
userId: "user1",
sessionId: "session1"
});
const newMessage: Content = createUserContent("What is the weather in London?");
for await (const event of runner.runAsync({
userId: "user1",
sessionId: "session1",
newMessage: newMessage,
})) {
if (isFinalResponse(event) && event.content?.parts?.length) {
const text = stringifyContent(event).trim();
if (text) {
console.log(text);
}
}
}
}
main();


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
"strings"
"google.golang.org/adk/agent"
"google.golang.org/adk/agent/llmagent"
"google.golang.org/adk/model/gemini"
"google.golang.org/adk/runner"
"google.golang.org/adk/session"
"google.golang.org/adk/tool"
"google.golang.org/adk/tool/functiontool"
"google.golang.org/genai"
)
type getWeatherReportArgs struct {
City string `json:"city" jsonschema:"The city for which to get the weather report."`
}
type getWeatherReportResult struct {
Status string `json:"status"`
Report string `json:"report,omitempty"`
}
func getWeatherReport(ctx tool.Context, args getWeatherReportArgs) (getWeatherReportResult, error) {
if strings.ToLower(args.City) == "london" {
return getWeatherReportResult{Status: "success", Report: "The current weather in London is cloudy with a temperature of 18 degrees Celsius and a chance of rain."}, nil
}
if strings.ToLower(args.City) == "paris" {
return getWeatherReportResult{Status: "success", Report: "The weather in Paris is sunny with a temperature of 25 degrees Celsius."}, nil
}
return getWeatherReportResult{}, fmt.Errorf("weather information for '%s' is not available.", args.City)
}
type analyzeSentimentArgs struct {
Text string `json:"text" jsonschema:"The text to analyze for sentiment."`
}
type analyzeSentimentResult struct {
Sentiment string `json:"sentiment"`
Confidence float64 `json:"confidence"`
}
func analyzeSentiment(ctx tool.Context, args analyzeSentimentArgs) (analyzeSentimentResult, error) {
if strings.Contains(strings.ToLower(args.Text), "good") || strings.Contains(strings.ToLower(args.Text), "sunny") {
return analyzeSentimentResult{Sentiment: "positive", Confidence: 0.8}, nil
}
if strings.Contains(strings.ToLower(args.Text), "rain") || strings.Contains(strings.ToLower(args.Text), "bad") {
return analyzeSentimentResult{Sentiment: "negative", Confidence: 0.7}, nil
}
return analyzeSentimentResult{Sentiment: "neutral", Confidence: 0.6}, nil
}
func main() {
ctx := context.Background()
model, err := gemini.NewModel(ctx, "gemini-2.0-flash", &genai.ClientConfig{})
if err != nil {
log.Fatal(err)
}
weatherTool, err := functiontool.New(
functiontool.Config{
Name: "get_weather_report",
Description: "Retrieves the current weather report for a specified city.",
},
getWeatherReport,
)
if err != nil {
log.Fatal(err)
}
sentimentTool, err := functiontool.New(
functiontool.Config{
Name: "analyze_sentiment",
Description: "Analyzes the sentiment of the given text.",
},
analyzeSentiment,
)
if err != nil {
log.Fatal(err)
}
weatherSentimentAgent, err := llmagent.New(llmagent.Config{
Name: "weather_sentiment_agent",
Model: model,
Instruction: "You are a helpful assistant that provides weather information and analyzes the sentiment of user feedback. **If the user asks about the weather in a specific city, use the 'get_weather_report' tool to retrieve the weather details.** **If the 'get_weather_report' tool returns a 'success' status, provide the weather report to the user.** **If the 'get_weather_report' tool returns an 'error' status, inform the user that the weather information for the specified city is not available and ask if they have another city in mind.** **After providing a weather report, if the user gives feedback on the weather (e.g., 'That's good' or 'I don't like rain'), use the 'analyze_sentiment' tool to understand their sentiment.** Then, briefly acknowledge their sentiment. You can handle these tasks sequentially if needed.",
Tools: []tool.Tool{weatherTool, sentimentTool},
})
if err != nil {
log.Fatal(err)
}
sessionService := session.InMemoryService()
runner, err := runner.New(runner.Config{
AppName: "weather_sentiment_agent",
Agent: weatherSentimentAgent,
SessionService: sessionService,
})
if err != nil {
log.Fatal(err)
}
session, err := sessionService.Create(ctx, &session.CreateRequest{
AppName: "weather_sentiment_agent",
UserID: "user1234",
})
if err != nil {
log.Fatal(err)
}
run(ctx, runner, session.Session.ID(), "weather in london?")
run(ctx, runner, session.Session.ID(), "I don't like rain.")
}
func run(ctx context.Context, r *runner.Runner, sessionID string, prompt string) {
fmt.Printf("\n> %s\n", prompt)
events := r.Run(
ctx,
"user1234",
sessionID,
genai.NewContentFromText(prompt, genai.RoleUser),
agent.RunConfig{
StreamingMode: agent.StreamingModeNone,
},
)
for event, err := range events {
if err != nil {
log.Fatalf("ERROR during agent execution: %v", err)
}
if event.Content.Parts[0].Text != "" {
fmt.Printf("Agent Response: %s\n", event.Content.Parts[0].Text)
}
}
}


import com.google.adk.agents.BaseAgent;
import com.google.adk.agents.LlmAgent;
import com.google.adk.runner.Runner;
import com.google.adk.sessions.InMemorySessionService;
import com.google.adk.sessions.Session;
import com.google.adk.tools.Annotations.Schema;
import com.google.adk.tools.FunctionTool;
import com.google.adk.tools.ToolContext; // Ensure this import is correct
import com.google.common.collect.ImmutableList;
import com.google.genai.types.Content;
import com.google.genai.types.Part;
import java.util.HashMap;
import java.util.Locale;
import java.util.Map;
public class WeatherSentimentAgentApp {
private static final String APP_NAME = "weather_sentiment_agent";
private static final String USER_ID = "user1234";
private static final String SESSION_ID = "1234";
private static final String MODEL_ID = "gemini-2.0-flash";
/**
* Retrieves the current weather report for a specified city.
*
* @param city The city for which to retrieve the weather report.
* @param toolContext The context for the tool.
* @return A dictionary containing the weather information.
*/
public static Map<String, Object> getWeatherReport(
@Schema(name = "city")
String city,
@Schema(name = "toolContext")
ToolContext toolContext) {
Map<String, Object> response = new HashMap<>();
if (city.toLowerCase(Locale.ROOT).equals("london")) {
response.put("status", "success");
response.put(
"report",
"The current weather in London is cloudy with a temperature of 18 degrees Celsius and a"
+ " chance of rain.");
} else if (city.toLowerCase(Locale.ROOT).equals("paris")) {
response.put("status", "success");
response.put(
"report", "The weather in Paris is sunny with a temperature of 25 degrees Celsius.");
} else {
response.put("status", "error");
response.put(
"error_message", String.format("Weather information for '%s' is not available.", city));
}
return response;
}
/**
* Analyzes the sentiment of the given text.
*
* @param text The text to analyze.
* @param toolContext The context for the tool.
* @return A dictionary with sentiment and confidence score.
*/
public static Map<String, Object> analyzeSentiment(
@Schema(name = "text")
String text,
@Schema(name = "toolContext")
ToolContext toolContext) {
Map<String, Object> response = new HashMap<>();
String lowerText = text.toLowerCase(Locale.ROOT);
if (lowerText.contains("good") || lowerText.contains("sunny")) {
response.put("sentiment", "positive");
response.put("confidence", 0.8);
} else if (lowerText.contains("rain") || lowerText.contains("bad")) {
response.put("sentiment", "negative");
response.put("confidence", 0.7);
} else {
response.put("sentiment", "neutral");
response.put("confidence", 0.6);
}
return response;
}
/**
* Calls the agent with the given query and prints the final response.
*
* @param runner The runner to use.
* @param query The query to send to the agent.
*/
public static void callAgent(Runner runner, String query) {
Content content = Content.fromParts(Part.fromText(query));
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
public static void main(String[] args) throws NoSuchMethodException {
FunctionTool weatherTool =
FunctionTool.create(
WeatherSentimentAgentApp.class.getMethod(
"getWeatherReport", String.class, ToolContext.class));
FunctionTool sentimentTool =
FunctionTool.create(
WeatherSentimentAgentApp.class.getMethod(
"analyzeSentiment", String.class, ToolContext.class));
BaseAgent weatherSentimentAgent =
LlmAgent.builder()
.model(MODEL_ID)
.name("weather_sentiment_agent")
.description("Weather Sentiment Agent")
.instruction("""
You are a helpful assistant that provides weather information and analyzes the
sentiment of user feedback
**If the user asks about the weather in a specific city, use the
'get_weather_report' tool to retrieve the weather details.**
**If the 'get_weather_report' tool returns a 'success' status, provide the
weather report to the user.**
**If the 'get_weather_report' tool returns an 'error' status, inform the
user that the weather information for the specified city is not available
and ask if they have another city in mind.**
**After providing a weather report, if the user gives feedback on the
weather (e.g., 'That's good' or 'I don't like rain'), use the
'analyze_sentiment' tool to understand their sentiment.** Then, briefly
acknowledge their sentiment.
You can handle these tasks sequentially if needed.
""")
.tools(ImmutableList.of(weatherTool, sentimentTool))
.build();
InMemorySessionService sessionService = new InMemorySessionService();
Runner runner = new Runner(weatherSentimentAgent, APP_NAME, null, sessionService);
// Change the query to ensure the tool is called with a valid city that triggers a "success"
// response from the tool, like "london" (without the question mark).
callAgent(runner, "weather in paris");
}
}


## Tool Context[¶](#tool-context)

For more advanced scenarios, ADK allows you to access additional contextual information within your tool function by including the special parameter `tool_context: ToolContext`

. By including this in the function signature, ADK will **automatically** provide an **instance of the ToolContext** class when your tool is called during agent execution.

The **ToolContext** provides access to several key pieces of information and control levers:

-
`state: State`

: Read and modify the current session's state. Changes made here are tracked and persisted. -
`actions: EventActions`

: Influence the agent's subsequent actions after the tool runs (e.g., skip summarization, transfer to another agent). -
`function_call_id: str`

: The unique identifier assigned by the framework to this specific invocation of the tool. Useful for tracking and correlating with authentication responses. This can also be helpful when multiple tools are called within a single model response. -
`function_call_event_id: str`

: This attribute provides the unique identifier of the**event**that triggered the current tool call. This can be useful for tracking and logging purposes. -
`auth_response: Any`

: Contains the authentication response/credentials if an authentication flow was completed before this tool call. -
Access to Services: Methods to interact with configured services like Artifacts and Memory.


Note that you shouldn't include the `tool_context`

parameter in the tool function docstring. Since `ToolContext`

is automatically injected by the ADK framework *after* the LLM decides to call the tool function, it is not relevant for the LLM's decision-making and including it can confuse the LLM.

**State Management**[¶](#state-management)

The `tool_context.state`

attribute provides direct read and write access to the state associated with the current session. It behaves like a dictionary but ensures that any modifications are tracked as deltas and persisted by the session service. This enables tools to maintain and share information across different interactions and agent steps.

-
**Reading State**: Use standard dictionary access (`tool_context.state['my_key']`

) or the`.get()`

method (`tool_context.state.get('my_key', default_value)`

). -
**Writing State**: Assign values directly (`tool_context.state['new_key'] = 'new_value'`

). These changes are recorded in the state_delta of the resulting event. -
**State Prefixes**: Remember the standard state prefixes:-
`app:*`

: Shared across all users of the application. -
`user:*`

: Specific to the current user across all their sessions. -
(No prefix): Specific to the current session.

-
`temp:*`

: Temporary, not persisted across invocations (useful for passing data within a single run call but generally less useful inside a tool context which operates between LLM calls).

-

from google.adk.tools import ToolContext, FunctionTool
def update_user_preference(preference: str, value: str, tool_context: ToolContext):
"""Updates a user-specific preference."""
user_prefs_key = "user:preferences"
# Get current preferences or initialize if none exist
preferences = tool_context.state.get(user_prefs_key, {})
preferences[preference] = value
# Write the updated dictionary back to the state
tool_context.state[user_prefs_key] = preferences
print(f"Tool: Updated user preference '{preference}' to '{value}'")
return {"status": "success", "updated_preference": preference}
pref_tool = FunctionTool(func=update_user_preference)
# In an Agent:
# my_agent = Agent(..., tools=[pref_tool])
# When the LLM calls update_user_preference(preference='theme', value='dark', ...):
# The tool_context.state will be updated, and the change will be part of the
# resulting tool response event's actions.state_delta.


import { ToolContext } from "@google/adk";
// Updates a user-specific preference.
export function updateUserThemePreference(
value: string,
toolContext: ToolContext
): Record<string, any> {
const userPrefsKey = "user:preferences";
// Get current preferences or initialize if none exist
const preferences = toolContext.state.get(userPrefsKey, {}) as Record<string, any>;
preferences["theme"] = value;
// Write the updated dictionary back to the state
toolContext.state.set(userPrefsKey, preferences);
console.log(
`Tool: Updated user preference ${userPrefsKey} to ${JSON.stringify(toolContext.state.get(userPrefsKey))}`
);
return {
status: "success",
updated_preference: toolContext.state.get(userPrefsKey),
};
// When the LLM calls updateUserThemePreference("dark"):
// The toolContext.state will be updated, and the change will be part of the
// resulting tool response event's actions.stateDelta.
}


import (
"fmt"
"google.golang.org/adk/tool"
)
type updateUserPreferenceArgs struct {
Preference string `json:"preference" jsonschema:"The name of the preference to set."`
Value string `json:"value" jsonschema:"The value to set for the preference."`
}
type updateUserPreferenceResult struct {
UpdatedPreference string `json:"updated_preference"`
}
func updateUserPreference(ctx tool.Context, args updateUserPreferenceArgs) (*updateUserPreferenceResult, error) {
userPrefsKey := "user:preferences"
val, err := ctx.State().Get(userPrefsKey)
if err != nil {
val = make(map[string]any)
}
preferencesMap, ok := val.(map[string]any)
if !ok {
preferencesMap = make(map[string]any)
}
preferencesMap[args.Preference] = args.Value
if err := ctx.State().Set(userPrefsKey, preferencesMap); err != nil {
return nil, err
}
fmt.Printf("Tool: Updated user preference '%s' to '%s'\n", args.Preference, args.Value)
return &updateUserPreferenceResult{
UpdatedPreference: args.Preference,
}, nil
}


import com.google.adk.tools.FunctionTool;
import com.google.adk.tools.ToolContext;
// Updates a user-specific preference.
public Map<String, String> updateUserThemePreference(String value, ToolContext toolContext) {
String userPrefsKey = "user:preferences:theme";
// Get current preferences or initialize if none exist
String preference = toolContext.state().getOrDefault(userPrefsKey, "").toString();
if (preference.isEmpty()) {
preference = value;
}
// Write the updated dictionary back to the state
toolContext.state().put("user:preferences", preference);
System.out.printf("Tool: Updated user preference %s to %s", userPrefsKey, preference);
return Map.of("status", "success", "updated_preference", toolContext.state().get(userPrefsKey).toString());
// When the LLM calls updateUserThemePreference("dark"):
// The toolContext.state will be updated, and the change will be part of the
// resulting tool response event's actions.stateDelta.
}


**Controlling Agent Flow**[¶](#controlling-agent-flow)

The `tool_context.actions`

attribute in Python and TypeScript, `ToolContext.actions()`

in Java, and `tool.Context.Actions()`

in Go, holds an **EventActions** object. Modifying attributes on this object allows your tool to influence what the agent or framework does after the tool finishes execution.

-
: (Default: False) If set to True, instructs the ADK to bypass the LLM call that typically summarizes the tool's output. This is useful if your tool's return value is already a user-ready message.`skip_summarization: bool`

-
: Set this to the name of another agent. The framework will halt the current agent's execution and`transfer_to_agent: str`

**transfer control of the conversation to the specified agent**. This allows tools to dynamically hand off tasks to more specialized agents. -
: (Default: False) Setting this to True signals that the current agent cannot handle the request and should pass control up to its parent agent (if in a hierarchy). In a LoopAgent, setting`escalate: bool`

**escalate=True**in a sub-agent's tool will terminate the loop.

#### Example[¶](#example_1)

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
from google.adk.tools import FunctionTool
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.adk.tools import ToolContext
from google.genai import types
APP_NAME="customer_support_agent"
USER_ID="user1234"
SESSION_ID="1234"
def check_and_transfer(query: str, tool_context: ToolContext) -> str:
"""Checks if the query requires escalation and transfers to another agent if needed."""
if "urgent" in query.lower():
print("Tool: Detected urgency, transferring to the support agent.")
tool_context.actions.transfer_to_agent = "support_agent"
return "Transferring to the support agent..."
else:
return f"Processed query: '{query}'. No further action needed."
escalation_tool = FunctionTool(func=check_and_transfer)
main_agent = Agent(
model='gemini-2.0-flash',
name='main_agent',
instruction="""You are the first point of contact for customer support of an analytics tool. Answer general queries. If the user indicates urgency, use the 'check_and_transfer' tool.""",
tools=[check_and_transfer]
)
support_agent = Agent(
model='gemini-2.0-flash',
name='support_agent',
instruction="""You are the dedicated support agent. Mentioned you are a support handler and please help the user with their urgent issue."""
)
main_agent.sub_agents = [support_agent]
# Session and Runner
async def setup_session_and_runner():
session_service = InMemorySessionService()
session = await session_service.create_session(app_name=APP_NAME, user_id=USER_ID, session_id=SESSION_ID)
runner = Runner(agent=main_agent, app_name=APP_NAME, session_service=session_service)
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
await call_agent_async("this is urgent, i cant login")


/**
* Copyright 2025 Google LLC
*
* Licensed under the Apache License, Version 2.0 (the "License");
* you may not use this file except in compliance with the License.
* You may obtain a copy of the License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed to in writing, software
* distributed under the License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
* See the License for the specific language governing permissions and
* limitations under the License.
*/
import { LlmAgent, FunctionTool, ToolContext, InMemoryRunner, isFinalResponse, stringifyContent } from "@google/adk";
import { z } from "zod";
import { Content, createUserContent } from "@google/genai";
function checkAndTransfer(
params: { query: string },
toolContext?: ToolContext
): Record<string, any> {
if (!toolContext) {
// This should not happen in a normal ADK flow where the tool is called by an agent.
throw new Error("ToolContext is required to transfer agents.");
}
if (params.query.toLowerCase().includes("urgent")) {
console.log("Tool: Urgent query detected, transferring to support_agent.");
toolContext.actions.transferToAgent = "support_agent";
return { status: "success", message: "Transferring to support agent." };
}
console.log("Tool: Query is not urgent, handling normally.");
return { status: "success", message: "Query will be handled by the main agent." };
}
const transferTool = new FunctionTool({
name: "check_and_transfer",
description: "Checks the user's query and transfers to a support agent if urgent.",
parameters: z.object({
query: z.string().describe("The user query to analyze."),
}),
execute: checkAndTransfer,
});
const supportAgent = new LlmAgent({
name: "support_agent",
description: "Handles urgent user requests about accounts.",
instruction: "You are the support agent. Handle the user's urgent request.",
model: "gemini-2.5-flash"
});
const mainAgent = new LlmAgent({
name: "main_agent",
description: "The main agent that routes non-urgent queries.",
instruction: "You are the main agent. Use the check_and_transfer tool to analyze the user query. If the query is not urgent, handle it yourself.",
tools: [transferTool],
subAgents: [supportAgent],
model: "gemini-2.5-flash"
});
async function main() {
const runner = new InMemoryRunner({ agent: mainAgent, appName: "customer_support_app" });
console.log("--- Running with a non-urgent query ---");
await runner.sessionService.createSession({ appName: "customer_support_app", userId: "user1", sessionId: "session1" });
const nonUrgentMessage: Content = createUserContent("I have a general question about my account.");
for await (const event of runner.runAsync({ userId: "user1", sessionId: "session1", newMessage: nonUrgentMessage })) {
if (isFinalResponse(event) && event.content?.parts?.length) {
const text = stringifyContent(event).trim();
if (text) {
console.log(`Final Response: ${text}`);
}
}
}
console.log("\n--- Running with an urgent query ---");
await runner.sessionService.createSession({ appName: "customer_support_app", userId: "user1", sessionId: "session2" });
const urgentMessage: Content = createUserContent("My account is locked and this is urgent!");
for await (const event of runner.runAsync({ userId: "user1", sessionId: "session2", newMessage: urgentMessage })) {
if (isFinalResponse(event) && event.content?.parts?.length) {
const text = stringifyContent(event).trim();
if (text) {
console.log(`Final Response: ${text}`);
}
}
}
}
main();


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
"strings"
"google.golang.org/adk/agent"
"google.golang.org/adk/agent/llmagent"
"google.golang.org/adk/model/gemini"
"google.golang.org/adk/runner"
"google.golang.org/adk/session"
"google.golang.org/adk/tool"
"google.golang.org/adk/tool/functiontool"
"google.golang.org/genai"
)
type checkAndTransferArgs struct {
Query string `json:"query" jsonschema:"The user's query to check for urgency."`
}
type checkAndTransferResult struct {
Status string `json:"status"`
}
func checkAndTransfer(ctx tool.Context, args checkAndTransferArgs) (checkAndTransferResult, error) {
if strings.Contains(strings.ToLower(args.Query), "urgent") {
fmt.Println("Tool: Detected urgency, transferring to the support agent.")
ctx.Actions().TransferToAgent = "support_agent"
return checkAndTransferResult{Status: "Transferring to the support agent..."}, nil
}
return checkAndTransferResult{Status: fmt.Sprintf("Processed query: '%s'. No further action needed.", args.Query)}, nil
}
func main() {
ctx := context.Background()
model, err := gemini.NewModel(ctx, "gemini-2.0-flash", &genai.ClientConfig{})
if err != nil {
log.Fatal(err)
}
supportAgent, err := llmagent.New(llmagent.Config{
Name: "support_agent",
Model: model,
Instruction: "You are the dedicated support agent. Mentioned you are a support handler and please help the user with their urgent issue.",
})
if err != nil {
log.Fatal(err)
}
checkAndTransferTool, err := functiontool.New(
functiontool.Config{
Name: "check_and_transfer",
Description: "Checks if the query requires escalation and transfers to another agent if needed.",
},
checkAndTransfer,
)
if err != nil {
log.Fatal(err)
}
mainAgent, err := llmagent.New(llmagent.Config{
Name: "main_agent",
Model: model,
Instruction: "You are the first point of contact for customer support of an analytics tool. Answer general queries. If the user indicates urgency, use the 'check_and_transfer' tool.",
Tools: []tool.Tool{checkAndTransferTool},
SubAgents: []agent.Agent{supportAgent},
})
if err != nil {
log.Fatal(err)
}
sessionService := session.InMemoryService()
runner, err := runner.New(runner.Config{
AppName: "customer_support_agent",
Agent: mainAgent,
SessionService: sessionService,
})
if err != nil {
log.Fatal(err)
}
session, err := sessionService.Create(ctx, &session.CreateRequest{
AppName: "customer_support_agent",
UserID: "user1234",
})
if err != nil {
log.Fatal(err)
}
run(ctx, runner, session.Session.ID(), "this is urgent, i cant login")
}
func run(ctx context.Context, r *runner.Runner, sessionID string, prompt string) {
fmt.Printf("\n> %s\n", prompt)
events := r.Run(
ctx,
"user1234",
sessionID,
genai.NewContentFromText(prompt, genai.RoleUser),
agent.RunConfig{
StreamingMode: agent.StreamingModeNone,
},
)
for event, err := range events {
if err != nil {
log.Fatalf("ERROR during agent execution: %v", err)
}
if event.Content.Parts[0].Text != "" {
fmt.Printf("Agent Response: %s\n", event.Content.Parts[0].Text)
}
}
}


import com.google.adk.agents.LlmAgent;
import com.google.adk.runner.Runner;
import com.google.adk.sessions.InMemorySessionService;
import com.google.adk.sessions.Session;
import com.google.adk.tools.Annotations.Schema;
import com.google.adk.tools.FunctionTool;
import com.google.adk.tools.ToolContext;
import com.google.common.collect.ImmutableList;
import com.google.genai.types.Content;
import com.google.genai.types.Part;
import java.util.HashMap;
import java.util.Locale;
import java.util.Map;
public class CustomerSupportAgentApp {
private static final String APP_NAME = "customer_support_agent";
private static final String USER_ID = "user1234";
private static final String SESSION_ID = "1234";
private static final String MODEL_ID = "gemini-2.0-flash";
/**
* Checks if the query requires escalation and transfers to another agent if needed.
*
* @param query The user's query.
* @param toolContext The context for the tool.
* @return A map indicating the result of the check and transfer.
*/
public static Map<String, Object> checkAndTransfer(
@Schema(name = "query", description = "the user query")
String query,
@Schema(name = "toolContext", description = "the tool context")
ToolContext toolContext) {
Map<String, Object> response = new HashMap<>();
if (query.toLowerCase(Locale.ROOT).contains("urgent")) {
System.out.println("Tool: Detected urgency, transferring to the support agent.");
toolContext.actions().setTransferToAgent("support_agent");
response.put("status", "transferring");
response.put("message", "Transferring to the support agent...");
} else {
response.put("status", "processed");
response.put(
"message", String.format("Processed query: '%s'. No further action needed.", query));
}
return response;
}
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
// Fixed: session ID does not need to be an optional.
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
public static void main(String[] args) throws NoSuchMethodException {
FunctionTool escalationTool =
FunctionTool.create(
CustomerSupportAgentApp.class.getMethod(
"checkAndTransfer", String.class, ToolContext.class));
LlmAgent supportAgent =
LlmAgent.builder()
.model(MODEL_ID)
.name("support_agent")
.description("""
The dedicated support agent.
Mentions it is a support handler and helps the user with their urgent issue.
""")
.instruction("""
You are the dedicated support agent.
Mentioned you are a support handler and please help the user with their urgent issue.
""")
.build();
LlmAgent mainAgent =
LlmAgent.builder()
.model(MODEL_ID)
.name("main_agent")
.description("""
The first point of contact for customer support of an analytics tool.
Answers general queries.
If the user indicates urgency, uses the 'check_and_transfer' tool.
""")
.instruction("""
You are the first point of contact for customer support of an analytics tool.
Answer general queries.
If the user indicates urgency, use the 'check_and_transfer' tool.
""")
.tools(ImmutableList.of(escalationTool))
.subAgents(supportAgent)
.build();
// Fixed: LlmAgent.subAgents() expects 0 arguments.
// Sub-agents are now added to the main agent via its builder,
// as `subAgents` is a property that should be set during agent construction
// if it's not dynamically managed.
InMemorySessionService sessionService = new InMemorySessionService();
Runner runner = new Runner(mainAgent, APP_NAME, null, sessionService);
// Agent Interaction
callAgent(runner, "this is urgent, i cant login");
}
}


##### Explanation[¶](#explanation)

- We define two agents:
`main_agent`

and`support_agent`

. The`main_agent`

is designed to be the initial point of contact. - The
`check_and_transfer`

tool, when called by`main_agent`

, examines the user's query. - If the query contains the word "urgent", the tool accesses the
`tool_context`

, specifically, and sets the transfer_to_agent attribute to`tool_context.actions`

`support_agent`

. - This action signals to the framework to
**transfer the control of the conversation to the agent named**.`support_agent`

- When the
`main_agent`

processes the urgent query, the`check_and_transfer`

tool triggers the transfer. The subsequent response would ideally come from the`support_agent`

. - For a normal query without urgency, the tool simply processes it without triggering a transfer.

This example illustrates how a tool, through EventActions in its ToolContext, can dynamically influence the flow of the conversation by transferring control to another specialized agent.

**Authentication**[¶](#authentication)

ToolContext provides mechanisms for tools interacting with authenticated APIs. If your tool needs to handle authentication, you might use the following:

-
(in Python): Contains credentials (e.g., a token) if authentication was already handled by the framework before your tool was called (common with RestApiTool and OpenAPI security schemes). In TypeScript, this is retrieved via the getAuthResponse() method.`auth_response`

-
(in Python) or`request_credential(auth_config: dict)`

(in TypeScript): Call this method if your tool determines authentication is needed but credentials aren't available. This signals the framework to start an authentication flow based on the provided auth_config.`requestCredential(authConfig: AuthConfig)`

-
(in Python) or`get_auth_response()`

(in TypeScript): Call this in a subsequent invocation (after request_credential was successfully handled) to retrieve the credentials the user provided.`getAuthResponse(authConfig: AuthConfig)`


For detailed explanations of authentication flows, configuration, and examples, please refer to the dedicated Tool Authentication documentation page.

**Context-Aware Data Access Methods**[¶](#context-aware-data-access-methods)

These methods provide convenient ways for your tool to interact with persistent data associated with the session or user, managed by configured services.

-
(in Python) or`list_artifacts()`

(in Java and TypeScript): Returns a list of filenames (or keys) for all artifacts currently stored for the session via the artifact_service. Artifacts are typically files (images, documents, etc.) uploaded by the user or generated by tools/agents.`listArtifacts()`

-
: Retrieves a specific artifact by its filename from the`load_artifact(filename: str)`

**artifact_service**. You can optionally specify a version; if omitted, the latest version is returned. Returns a`google.genai.types.Part`

object containing the artifact data and mime type, or None if not found. -
: Saves a new version of an artifact to the artifact_service. Returns the new version number (starting from 0).`save_artifact(filename: str, artifact: types.Part)`

-
: (Support in ADK Python, Go and TypeScript) Queries the user's long-term memory using the configured`search_memory(query: str)`

`memory_service`

. This is useful for retrieving relevant information from past interactions or stored knowledge. The structure of the**SearchMemoryResponse**depends on the specific memory service implementation but typically contains relevant text snippets or conversation excerpts.

#### Example[¶](#example_2)

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
from google.adk.tools import ToolContext, FunctionTool
from google.genai import types
def process_document(
document_name: str, analysis_query: str, tool_context: ToolContext
) -> dict:
"""Analyzes a document using context from memory."""
# 1. Load the artifact
print(f"Tool: Attempting to load artifact: {document_name}")
document_part = tool_context.load_artifact(document_name)
if not document_part:
return {"status": "error", "message": f"Document '{document_name}' not found."}
document_text = document_part.text # Assuming it's text for simplicity
print(f"Tool: Loaded document '{document_name}' ({len(document_text)} chars).")
# 2. Search memory for related context
print(f"Tool: Searching memory for context related to: '{analysis_query}'")
memory_response = tool_context.search_memory(
f"Context for analyzing document about {analysis_query}"
)
memory_context = "\n".join(
[
m.events[0].content.parts[0].text
for m in memory_response.memories
if m.events and m.events[0].content
]
) # Simplified extraction
print(f"Tool: Found memory context: {memory_context[:100]}...")
# 3. Perform analysis (placeholder)
analysis_result = f"Analysis of '{document_name}' regarding '{analysis_query}' using memory context: [Placeholder Analysis Result]"
print("Tool: Performed analysis.")
# 4. Save the analysis result as a new artifact
analysis_part = types.Part.from_text(text=analysis_result)
new_artifact_name = f"analysis_{document_name}"
version = await tool_context.save_artifact(new_artifact_name, analysis_part)
print(f"Tool: Saved analysis result as '{new_artifact_name}' version {version}.")
return {
"status": "success",
"analysis_artifact": new_artifact_name,
"version": version,
}
doc_analysis_tool = FunctionTool(func=process_document)
# In an Agent:
# Assume artifact 'report.txt' was previously saved.
# Assume memory service is configured and has relevant past data.
# my_agent = Agent(..., tools=[doc_analysis_tool], artifact_service=..., memory_service=...)


import { Part } from "@google/genai";
import { ToolContext } from "@google/adk";
// Analyzes a document using context from memory.
export async function processDocument(
params: { documentName: string; analysisQuery: string },
toolContext?: ToolContext
): Promise<Record<string, any>> {
if (!toolContext) {
throw new Error("ToolContext is required for this tool.");
}
// 1. List all available artifacts
const artifacts = await toolContext.listArtifacts();
console.log(`Listing all available artifacts: ${artifacts}`);
// 2. Load an artifact
console.log(`Tool: Attempting to load artifact: ${params.documentName}`);
const documentPart = await toolContext.loadArtifact(params.documentName);
if (!documentPart) {
console.log(`Tool: Document '${params.documentName}' not found.`);
return {
status: "error",
message: `Document '${params.documentName}' not found.`,
};
}
const documentText = documentPart.text ?? "";
console.log(
`Tool: Loaded document '${params.documentName}' (${documentText.length} chars).`
);
// 3. Search memory for related context
console.log(`Tool: Searching memory for context related to '${params.analysisQuery}'`);
const memory_results = await toolContext.searchMemory(params.analysisQuery);
console.log(`Tool: Found ${memory_results.memories.length} relevant memories.`);
const context_from_memory = memory_results.memories
.map((m) => m.content.parts[0].text)
.join("\n");
// 4. Perform analysis (placeholder)
const analysisResult =
`Analysis of '${params.documentName}' regarding '${params.analysisQuery}':\n` +
`Context from Memory:\n${context_from_memory}\n` +
`[Placeholder Analysis Result]`;
console.log("Tool: Performed analysis.");
// 5. Save the analysis result as a new artifact
const analysisPart: Part = { text: analysisResult };
const newArtifactName = `analysis_${params.documentName}`;
await toolContext.saveArtifact(newArtifactName, analysisPart);
console.log(`Tool: Saved analysis result to '${newArtifactName}'.`);
return {
status: "success",
analysis_artifact: newArtifactName,
};
}


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
"fmt"
"google.golang.org/adk/tool"
"google.golang.org/genai"
)
type processDocumentArgs struct {
DocumentName string `json:"document_name" jsonschema:"The name of the document to be processed."`
AnalysisQuery string `json:"analysis_query" jsonschema:"The query for the analysis."`
}
type processDocumentResult struct {
Status string `json:"status"`
AnalysisArtifact string `json:"analysis_artifact,omitempty"`
Version int64 `json:"version,omitempty"`
Message string `json:"message,omitempty"`
}
func processDocument(ctx tool.Context, args processDocumentArgs) (*processDocumentResult, error) {
fmt.Printf("Tool: Attempting to load artifact: %s\n", args.DocumentName)
// List all artifacts
listResponse, err := ctx.Artifacts().List(ctx)
if err != nil {
return nil, fmt.Errorf("failed to list artifacts")
}
fmt.Println("Tool: Available artifacts:")
for _, file := range listResponse.FileNames {
fmt.Printf(" - %s\n", file)
}
documentPart, err := ctx.Artifacts().Load(ctx, args.DocumentName)
if err != nil {
return nil, fmt.Errorf("document '%s' not found", args.DocumentName)
}
fmt.Printf("Tool: Loaded document '%s' of size %d bytes.\n", args.DocumentName, len(documentPart.Part.InlineData.Data))
// 3. Search memory for related context
fmt.Printf("Tool: Searching memory for context related to: '%s'\n", args.AnalysisQuery)
memoryResp, err := ctx.SearchMemory(ctx, args.AnalysisQuery)
if err != nil {
fmt.Printf("Tool: Error searching memory: %v\n", err)
}
memoryResultCount := 0
if memoryResp != nil {
memoryResultCount = len(memoryResp.Memories)
}
fmt.Printf("Tool: Found %d memory results.\n", memoryResultCount)
analysisResult := fmt.Sprintf("Analysis of '%s' regarding '%s' using memory context: [Placeholder Analysis Result]", args.DocumentName, args.AnalysisQuery)
fmt.Println("Tool: Performed analysis.")
analysisPart := genai.NewPartFromText(analysisResult)
newArtifactName := fmt.Sprintf("analysis_%s", args.DocumentName)
version, err := ctx.Artifacts().Save(ctx, newArtifactName, analysisPart)
if err != nil {
return nil, fmt.Errorf("failed to save artifact")
}
fmt.Printf("Tool: Saved analysis result as '%s' version %d.\n", newArtifactName, version.Version)
return &processDocumentResult{
Status: "success",
AnalysisArtifact: newArtifactName,
Version: version.Version,
}, nil
}


// Analyzes a document using context from memory.
// You can also list, load and save artifacts using Callback Context or LoadArtifacts tool.
public static @NonNull Maybe<ImmutableMap<String, Object>> processDocument(
@Annotations.Schema(description = "The name of the document to analyze.") String documentName,
@Annotations.Schema(description = "The query for the analysis.") String analysisQuery,
ToolContext toolContext) {
// 1. List all available artifacts
System.out.printf(
"Listing all available artifacts %s:", toolContext.listArtifacts().blockingGet());
// 2. Load an artifact to memory
System.out.println("Tool: Attempting to load artifact: " + documentName);
Part documentPart = toolContext.loadArtifact(documentName, Optional.empty()).blockingGet();
if (documentPart == null) {
System.out.println("Tool: Document '" + documentName + "' not found.");
return Maybe.just(
ImmutableMap.<String, Object>of(
"status", "error", "message", "Document '" + documentName + "' not found."));
}
String documentText = documentPart.text().orElse("");
System.out.println(
"Tool: Loaded document '" + documentName + "' (" + documentText.length() + " chars).");
// 3. Perform analysis (placeholder)
String analysisResult =
"Analysis of '"
+ documentName
+ "' regarding '"
+ analysisQuery
+ " [Placeholder Analysis Result]";
System.out.println("Tool: Performed analysis.");
// 4. Save the analysis result as a new artifact
Part analysisPart = Part.fromText(analysisResult);
String newArtifactName = "analysis_" + documentName;
toolContext.saveArtifact(newArtifactName, analysisPart);
return Maybe.just(
ImmutableMap.<String, Object>builder()
.put("status", "success")
.put("analysis_artifact", newArtifactName)
.build());
}
// FunctionTool processDocumentTool =
// FunctionTool.create(ToolContextArtifactExample.class, "processDocument");
// In the Agent, include this function tool.
// LlmAgent agent = LlmAgent().builder().tools(processDocumentTool).build();


By leveraging the **ToolContext**, developers can create more sophisticated and context-aware custom tools that seamlessly integrate with ADK's architecture and enhance the overall capabilities of their agents.

## Defining Effective Tool Functions[¶](#defining-effective-tool-functions)

When using a method or function as an ADK Tool, how you define it significantly impacts the agent's ability to use it correctly. The agent's Large Language Model (LLM) relies heavily on the function's **name**, **parameters (arguments)**, **type hints**, and **docstring** / **source code comments** to understand its purpose and generate the correct call.

Here are key guidelines for defining effective tool functions:

-
**Function Name:**- Use descriptive, verb-noun based names that clearly indicate the action (e.g.,
`get_weather`

,`searchDocuments`

,`schedule_meeting`

). - Avoid generic names like
`run`

,`process`

,`handle_data`

, or overly ambiguous names like`doStuff`

. Even with a good description, a name like`do_stuff`

might confuse the model about when to use the tool versus, for example,`cancelFlight`

. - The LLM uses the function name as a primary identifier during tool selection.

- Use descriptive, verb-noun based names that clearly indicate the action (e.g.,
-
**Parameters (Arguments):**- Your function can have any number of parameters.
- Use clear and descriptive names (e.g.,
`city`

instead of`c`

,`search_query`

instead of`q`

). **Provide type hints in Python**for all parameters (e.g.,`city: str`

,`user_id: int`

,`items: list[str]`

). This is essential for ADK to generate the correct schema for the LLM.- Ensure all parameter types are
**JSON serializable**. All java primitives as well as standard Python types like`str`

,`int`

,`float`

,`bool`

,`list`

,`dict`

, and their combinations are generally safe. Avoid complex custom class instances as direct parameters unless they have a clear JSON representation. **Do not set default values**for parameters. E.g.,`def my_func(param1: str = "default")`

. Default values are not reliably supported or used by the underlying models during function call generation. All necessary information should be derived by the LLM from the context or explicitly requested if missing.Implicit parameters like`self`

/`cls`

Handled Automatically:`self`

(for instance methods) or`cls`

(for class methods) are automatically handled by ADK and excluded from the schema shown to the LLM. You only need to define type hints and descriptions for the logical parameters your tool requires the LLM to provide.

-
**Return Type:**- The function's return value
**must be a dictionary (**in Python, a`dict`

)**Map**in Java, or a plain**object**in TypeScript. - If your function returns a non-dictionary type (e.g., a string, number, list), the ADK framework will automatically wrap it into a dictionary/Map like
`{'result': your_original_return_value}`

before passing the result back to the model. - Design the dictionary/Map keys and values to be
**descriptive and easily understood**. Remember, the model reads this output to decide its next step.*by the LLM* - Include meaningful keys. For example, instead of returning just an error code like
`500`

, return`{'status': 'error', 'error_message': 'Database connection failed'}`

. - It's a
**highly recommended practice**to include a`status`

key (e.g.,`'success'`

,`'error'`

,`'pending'`

,`'ambiguous'`

) to clearly indicate the outcome of the tool execution for the model.

- The function's return value
-
**Docstring / Source Code Comments:****This is critical.**The docstring is the primary source of descriptive information for the LLM.**Clearly state what the tool**Be specific about its purpose and limitations.*does*.**Explain**Provide context or example scenarios to guide the LLM's decision-making.*when*the tool should be used.**Describe**Explain what information the LLM needs to provide for that argument.*each parameter*clearly.- Describe the
**structure and meaning of the expected**, especially the different`dict`

return value`status`

values and associated data keys. **Do not describe the injected ToolContext parameter**. Avoid mentioning the optional`tool_context: ToolContext`

parameter within the docstring description since it is not a parameter the LLM needs to know about. ToolContext is injected by ADK,*after*the LLM decides to call it.

**Example of a good definition:**

def lookup_order_status(order_id: str) -> dict:
"""Fetches the current status of a customer's order using its ID.
Use this tool ONLY when a user explicitly asks for the status of
a specific order and provides the order ID. Do not use it for
general inquiries.
Args:
order_id: The unique identifier of the order to look up.
Returns:
A dictionary indicating the outcome.
On success, status is 'success' and includes an 'order' dictionary.
On failure, status is 'error' and includes an 'error_message'.
Example success: {'status': 'success', 'order': {'state': 'shipped', 'tracking_number': '1Z9...'}}
Example error: {'status': 'error', 'error_message': 'Order ID not found.'}
"""
# ... function implementation to fetch status ...
if status_details := fetch_status_from_backend(order_id):
return {
"status": "success",
"order": {
"state": status_details.state,
"tracking_number": status_details.tracking,
},
}
else:
return {"status": "error", "error_message": f"Order ID {order_id} not found."}


/**
* Fetches the current status of a customer's order using its ID.
*
* Use this tool ONLY when a user explicitly asks for the status of
* a specific order and provides the order ID. Do not use it for
* general inquiries.
*
* @param params The parameters for the function.
* @param params.order_id The unique identifier of the order to look up.
* @returns A dictionary indicating the outcome.
* On success, status is 'success' and includes an 'order' dictionary.
* On failure, status is 'error' and includes an 'error_message'.
* Example success: {'status': 'success', 'order': {'state': 'shipped', 'tracking_number': '1Z9...'}}
* Example error: {'status': 'error', 'error_message': 'Order ID not found.'}
*/
async function lookupOrderStatus(params: { order_id: string }): Promise<Record<string, any>> {
// ... function implementation to fetch status from a backend ...
const status_details = await fetchStatusFromBackend(params.order_id);
if (status_details) {
return {
"status": "success",
"order": {
"state": status_details.state,
"tracking_number": status_details.tracking,
},
};
} else {
return { "status": "error", "error_message": `Order ID ${params.order_id} not found.` };
}
}
// Placeholder for a backend call
async function fetchStatusFromBackend(order_id: string): Promise<{state: string, tracking: string} | null> {
if (order_id === "12345") {
return { state: "shipped", tracking: "1Z9..." };
}
return null;
}


import (
"fmt"
"google.golang.org/adk/tool"
)
type lookupOrderStatusArgs struct {
OrderID string `json:"order_id" jsonschema:"The ID of the order to look up."`
}
type order struct {
State string `json:"state"`
TrackingNumber string `json:"tracking_number"`
}
type lookupOrderStatusResult struct {
Status string `json:"status"`
Order order `json:"order,omitempty"`
}
func lookupOrderStatus(ctx tool.Context, args lookupOrderStatusArgs) (*lookupOrderStatusResult, error) {
// ... function implementation to fetch status ...
statusDetails, ok := fetchStatusFromBackend(args.OrderID)
if !ok {
return nil, fmt.Errorf("order ID %s not found", args.OrderID)
}
return &lookupOrderStatusResult{
Status: "success",
Order: order{
State: statusDetails.State,
TrackingNumber: statusDetails.Tracking,
},
}, nil
}


/**
* Retrieves the current weather report for a specified city.
*
* @param city The city for which to retrieve the weather report.
* @param toolContext The context for the tool.
* @return A dictionary containing the weather information.
*/
public static Map<String, Object> getWeatherReport(String city, ToolContext toolContext) {
Map<String, Object> response = new HashMap<>();
if (city.toLowerCase(Locale.ROOT).equals("london")) {
response.put("status", "success");
response.put(
"report",
"The current weather in London is cloudy with a temperature of 18 degrees Celsius and a"
+ " chance of rain.");
} else if (city.toLowerCase(Locale.ROOT).equals("paris")) {
response.put("status", "success");
response.put("report", "The weather in Paris is sunny with a temperature of 25 degrees Celsius.");
} else {
response.put("status", "error");
response.put("error_message", String.format("Weather information for '%s' is not available.", city));
}
return response;
}


**Simplicity and Focus:****Keep Tools Focused:**Each tool should ideally perform one well-defined task.**Fewer Parameters are Better:**Models generally handle tools with fewer, clearly defined parameters more reliably than those with many optional or complex ones.**Use Simple Data Types:**Prefer basic types (`str`

,`int`

,`bool`

,`float`

,`List[str]`

, in**Python**;`int`

,`byte`

,`short`

,`long`

,`float`

,`double`

,`boolean`

and`char`

in**Java**; or`string`

,`number`

,`boolean`

, and arrays like`string[]`

in**TypeScript**) over complex custom classes or deeply nested structures as parameters when possible.**Decompose Complex Tasks:**Break down functions that perform multiple distinct logical steps into smaller, more focused tools. For instance, instead of a single`update_user_profile(profile: ProfileObject)`

tool, consider separate tools like`update_user_name(name: str)`

,`update_user_address(address: str)`

,`update_user_preferences(preferences: list[str])`

, etc. This makes it easier for the LLM to select and use the correct capability.


By adhering to these guidelines, you provide the LLM with the clarity and structure it needs to effectively utilize your custom function tools, leading to more capable and reliable agent behavior.

## Toolsets: Grouping and Dynamically Providing Tools[¶](#toolsets-grouping-and-dynamically-providing-tools)

Beyond individual tools, ADK introduces the concept of a **Toolset** via the `BaseToolset`

interface (defined in `google.adk.tools.base_toolset`

). A toolset allows you to manage and provide a collection of `BaseTool`

instances, often dynamically, to an agent.

This approach is beneficial for:

**Organizing Related Tools:**Grouping tools that serve a common purpose (e.g., all tools for mathematical operations, or all tools interacting with a specific API).**Dynamic Tool Availability:**Enabling an agent to have different tools available based on the current context (e.g., user permissions, session state, or other runtime conditions). The`get_tools`

method of a toolset can decide which tools to expose.**Integrating External Tool Providers:**Toolsets can act as adapters for tools coming from external systems, like an OpenAPI specification or an MCP server, converting them into ADK-compatible`BaseTool`

objects.

### The `BaseToolset`

Interface[¶](#the-basetoolset-interface)

Any class acting as a toolset in ADK should implement the `BaseToolset`

abstract base class. This interface primarily defines two methods:

-
This is the core method of a toolset. When an ADK agent needs to know its available tools, it will call`async def get_tools(...) -> list[BaseTool]:`

`get_tools()`

on each`BaseToolset`

instance provided in its`tools`

list.- It receives an optional
`readonly_context`

(an instance of`ReadonlyContext`

). This context provides read-only access to information like the current session state (`readonly_context.state`

), agent name, and invocation ID. The toolset can use this context to dynamically decide which tools to return. - It
**must**return a`list`

of`BaseTool`

instances (e.g.,`FunctionTool`

,`RestApiTool`

).

- It receives an optional
-
This asynchronous method is called by the ADK framework when the toolset is no longer needed, for example, when an agent server is shutting down or the`async def close(self) -> None:`

`Runner`

is being closed. Implement this method to perform any necessary cleanup, such as closing network connections, releasing file handles, or cleaning up other resources managed by the toolset.

### Using Toolsets with Agents[¶](#using-toolsets-with-agents)

You can include instances of your `BaseToolset`

implementations directly in an `LlmAgent`

's `tools`

list, alongside individual `BaseTool`

instances.

When the agent initializes or needs to determine its available capabilities, the ADK framework will iterate through the `tools`

list:

- If an item is a
`BaseTool`

instance, it's used directly. - If an item is a
`BaseToolset`

instance, its`get_tools()`

method is called (with the current`ReadonlyContext`

), and the returned list of`BaseTool`

s is added to the agent's available tools.

### Example: A Simple Math Toolset[¶](#example-a-simple-math-toolset)

Let's create a basic example of a toolset that provides simple arithmetic operations.

# 1. Define the individual tool functions
def add_numbers(a: int, b: int, tool_context: ToolContext) -> Dict[str, Any]:
"""Adds two integer numbers.
Args:
a: The first number.
b: The second number.
Returns:
A dictionary with the sum, e.g., {'status': 'success', 'result': 5}
"""
print(f"Tool: add_numbers called with a={a}, b={b}")
result = a + b
# Example: Storing something in tool_context state
tool_context.state["last_math_operation"] = "addition"
return {"status": "success", "result": result}
def subtract_numbers(a: int, b: int) -> Dict[str, Any]:
"""Subtracts the second number from the first.
Args:
a: The first number.
b: The second number.
Returns:
A dictionary with the difference, e.g., {'status': 'success', 'result': 1}
"""
print(f"Tool: subtract_numbers called with a={a}, b={b}")
return {"status": "success", "result": a - b}
# 2. Create the Toolset by implementing BaseToolset
class SimpleMathToolset(BaseToolset):
def __init__(self, prefix: str = "math_"):
self.prefix = prefix
# Create FunctionTool instances once
self._add_tool = FunctionTool(
func=add_numbers,
name=f"{self.prefix}add_numbers", # Toolset can customize names
)
self._subtract_tool = FunctionTool(
func=subtract_numbers, name=f"{self.prefix}subtract_numbers"
)
print(f"SimpleMathToolset initialized with prefix '{self.prefix}'")
async def get_tools(
self, readonly_context: Optional[ReadonlyContext] = None
) -> List[BaseTool]:
print(f"SimpleMathToolset.get_tools() called.")
# Example of dynamic behavior:
# Could use readonly_context.state to decide which tools to return
# For instance, if readonly_context.state.get("enable_advanced_math"):
# return [self._add_tool, self._subtract_tool, self._multiply_tool]
# For this simple example, always return both tools
tools_to_return = [self._add_tool, self._subtract_tool]
print(f"SimpleMathToolset providing tools: {[t.name for t in tools_to_return]}")
return tools_to_return
async def close(self) -> None:
# No resources to clean up in this simple example
print(f"SimpleMathToolset.close() called for prefix '{self.prefix}'.")
await asyncio.sleep(0) # Placeholder for async cleanup if needed
# 3. Define an individual tool (not part of the toolset)
def greet_user(name: str = "User") -> Dict[str, str]:
"""Greets the user."""
print(f"Tool: greet_user called with name={name}")
return {"greeting": f"Hello, {name}!"}
greet_tool = FunctionTool(func=greet_user)
# 4. Instantiate the toolset
math_toolset_instance = SimpleMathToolset(prefix="calculator_")
# 5. Define an agent that uses both the individual tool and the toolset
calculator_agent = LlmAgent(
name="CalculatorAgent",
model="gemini-2.0-flash", # Replace with your desired model
instruction="You are a helpful calculator and greeter. "
"Use 'greet_user' for greetings. "
"Use 'calculator_add_numbers' to add and 'calculator_subtract_numbers' to subtract. "
"Announce the state of 'last_math_operation' if it's set.",
tools=[greet_tool, math_toolset_instance], # Individual tool # Toolset instance
)


/**
* Copyright 2025 Google LLC
*
* Licensed under the Apache License, Version 2.0 (the "License");
* you may not use this file except in compliance with the License.
* You may obtain a copy of the License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed to in writing, software
* distributed under the License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
* See the License for the specific language governing permissions and
* limitations under the License.
*/
import { LlmAgent, FunctionTool, ToolContext, BaseToolset, InMemoryRunner, isFinalResponse, BaseTool, stringifyContent } from "@google/adk";
import { z } from "zod";
import { Content, createUserContent } from "@google/genai";
function addNumbers(params: { a: number; b: number }, toolContext?: ToolContext): Record<string, any> {
if (!toolContext) {
throw new Error("ToolContext is required for this tool.");
}
const result = params.a + params.b;
toolContext.state.set("last_math_result", result);
return { result: result };
}
function subtractNumbers(params: { a: number; b: number }): Record<string, any> {
return { result: params.a - params.b };
}
function greetUser(params: { name: string }): Record<string, any> {
return { greeting: `Hello, ${params.name}!` };
}
class SimpleMathToolset extends BaseToolset {
private readonly tools: BaseTool[];
constructor(prefix = "") {
super([]); // No filter
this.tools = [
new FunctionTool({
name: `${prefix}add_numbers`,
description: "Adds two numbers and stores the result in the session state.",
parameters: z.object({ a: z.number(), b: z.number() }),
execute: addNumbers,
}),
new FunctionTool({
name: `${prefix}subtract_numbers`,
description: "Subtracts the second number from the first.",
parameters: z.object({ a: z.number(), b: z.number() }),
execute: subtractNumbers,
}),
];
}
async getTools(): Promise<BaseTool[]> {
return this.tools;
}
async close(): Promise<void> {
console.log("SimpleMathToolset closed.");
}
}
async function main() {
const mathToolset = new SimpleMathToolset("calculator_");
const greetTool = new FunctionTool({
name: "greet_user",
description: "Greets the user.",
parameters: z.object({ name: z.string() }),
execute: greetUser,
});
const instruction =
`You are a calculator and a greeter.
If the user asks for a math operation, use the calculator tools.
If the user asks for a greeting, use the greet_user tool.
The result of the last math operation is stored in the 'last_math_result' state variable.`;
const calculatorAgent = new LlmAgent({
name: "calculator_agent",
instruction: instruction,
tools: [greetTool, mathToolset],
model: "gemini-2.5-flash",
});
const runner = new InMemoryRunner({ agent: calculatorAgent, appName: "toolset_app" });
await runner.sessionService.createSession({ appName: "toolset_app", userId: "user1", sessionId: "session1" });
const message: Content = createUserContent("What is 5 + 3?");
for await (const event of runner.runAsync({ userId: "user1", sessionId: "session1", newMessage: message })) {
if (isFinalResponse(event) && event.content?.parts?.length) {
const text = stringifyContent(event).trim();
if (text) {
console.log(`Response from agent: ${text}`);
}
}
}
await mathToolset.close();
}
main();


In this example:

`SimpleMathToolset`

implements`BaseToolset`

and its`get_tools()`

method returns`FunctionTool`

instances for`add_numbers`

and`subtract_numbers`

. It also customizes their names using a prefix.- The
`calculator_agent`

is configured with both an individual`greet_tool`

and an instance of`SimpleMathToolset`

. - When
`calculator_agent`

is run, ADK will call`math_toolset_instance.get_tools()`

. The agent's LLM will then have access to`greet_user`

,`calculator_add_numbers`

, and`calculator_subtract_numbers`

to handle user requests. - The
`add_numbers`

tool demonstrates writing to`tool_context.state`

, and the agent's instruction mentions reading this state. - The
`close()`

method is called to ensure any resources held by the toolset are released.

Toolsets offer a powerful way to organize, manage, and dynamically provide collections of tools to your ADK agents, leading to more modular, maintainable, and adaptable agentic applications.
