---
merged_at: 2026-01-29T15:49:53.290939
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-triggers-python -->

# Azure Functions developer reference guide for Python apps

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions is a serverless compute service that enables you to run event-driven code without provisioning or managing infrastructure. Function executions are triggered by events such as HTTP requests, queue messages, timers, or changes in storage—and scale automatically based on demand.

This guide focuses specifically on building Python-based Azure Functions and helps you:

- Create and run function apps locally
- Understand the Python programming model
- Organize and configure your application
- Deploy and monitor your app in Azure
- Apply best practices for scaling and performance

Looking for a conceptual overview? See the

[Azure Functions Developer Reference].Interested in real-world use cases? Explore the

[Scenarios & Samples]page.

## Getting started

Choose the environment that fits your workflow and jump into Azure Functions for Python:

## Building your function app

This section covers the essential components for creating and structuring your Python function app. Topics include the [programming model](#programming-model), [project structure](#folder-structure), [triggers and bindings](#triggers-and-bindings), and [dependency management](#package-management).

### Programming model

Functions supports two versions of the Python programming model:

| Version | Description |
|---|---|
| 2.x | Use a decorator-based approach to define triggers and bindings directly in your Python code file. You implement each function as a global, stateless method in a `function_app.py` file or a referenced blueprint file. This model version is recommended for new Python apps. |
| 1.x | You define triggers and bindings for each function in a separate `function.json` file. You implement each function as a global, stateless method in your Python code file. This version of the model supports legacy apps. |

This article targets a specific Python model version. Choose your desired version at the [top of the article](#top).

Important

Use the v2 programming model for a **decorator-based approach** to define triggers and bindings directly in your code.

In the Python v1 programming model, each function is defined as a global, stateless `main()`

method inside a file named `__init__.py`

.
The function’s triggers and bindings are configured separately in a `function.json`

file, and the binding `name`

values are used as parameters in your `main()`

method.

**Example**

Here's a simple function that responds to an HTTP request:

```
# __init__.py
def main(req):
user = req.params.get('user')
return f'Hello, {user}!'
```


Here's the corresponding `function.json`

file:

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"get",
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "$return"
}
]
}
```


#### Key concepts

- The function has a single HTTP trigger.
- The
[HttpRequest](/en-us/python/api/azure-functions/azure.functions.httprequest)object contains request headers, query parameters, route parameters, and the message body. This function gets the value of the`name`

query parameter from the`params`

parameter of the[HttpRequest](/en-us/python/api/azure-functions/azure.functions.httprequest)object. - To send a name in this example, append
`?name={name}`

to the exposed function URL. For example, if running locally, the full URL might look like`http://localhost:7071/api/http_trigger?name=Test`

. For examples using bindings, see[Triggers and Bindings](#triggers-and-bindings).

Use the `azure-functions`

SDK and include **type annotations** to improve IntelliSense and editor support:

```
# __init__.py
import azure.functions as func
def http_trigger(req: func.HttpRequest) -> str:
```


```
# requirements.txt
azure-functions
```


#### The `azure-functions`

library

The `azure-functions`

Python library provides the core types used to interact with the Azure Functions runtime. To see all types and methods available, visit the [ azure-functions API](/en-us/python/api/azure-functions/).
Your function code can use

`azure-functions`

to:- Access trigger input data (for example,
`HttpRequest`

,`TimerRequest`

) - Create output values (such as
`HttpResponse`

) - Interact with runtime-provided context and binding data

If you're using `azure-functions`

in your app, it must be included in your project dependencies.

Note

The `azure-functions`

library defines the programming surface for Python Azure Functions, but it isn’t a general-purpose SDK. Use it specifically for authoring and running functions within the Azure Functions runtime.

### Alternative entry point

You can change the default behavior of a function by specifying the `scriptFile`

and `entryPoint`

properties in the `function.json`

file. For example,
the following `function.json`

file directs the runtime to use the `custom_entry()`

method in the `main.py`

file as the entry point for your Azure function.

```
{
"scriptFile": "main.py",
"entryPoint": "custom_entry",
"bindings": [
...
]
}
```


### Folder structure

Use the following structure for a Python Azure Functions project:

```
<project_root>/
│
├── .venv/ # (Optional) Local Python virtual environment
├── .vscode/ # (Optional) VS Code workspace settings
│
├── my_first_function/ # Function directory
│ └── __init__.py # Function code file
│ └── function.json # Function binding configuration file
│
├── my_second_function/
│ └── __init__.py
│ └── function.json
│
├── shared/ # (Optional) Pure helper code with no triggers/bindings
│ └── utils.py
│
├── additional_functions/ # (Optional) Contains blueprints for organizing related Functions
│ └── blueprint_1.py
│
├── tests/ # (Optional) Unit tests for your functions
│ └── test_my_function.py
│
├── .funcignore # Excludes files from being published
├── host.json # Global function app configuration
├── local.settings.json # Local-only app settings (not published)
├── requirements.txt # (Optional) Defines Python dependencies for remote build
├── Dockerfile # (Optional) For custom container deployment
```


#### Key files and folders

| File / Folder | Description | Required for app to run in Azure |
|---|---|---|
`my_first_function/` |
Directory for a single function. | ✅ |
`__init__.py/` |
Main script where the `my_first_function` function code is defined. |
✅ |
`function.json/` |
Contains the binding configuration for the `my_first_function` function. |
✅ |
`host.json` |
Global configuration for all functions in the app. | ✅ |
`requirements.txt` |
Python dependencies installed during publish when using
|

`local.settings.json`

`.funcignore`

`.venv/`

, `tests/`

, `local.settings.json`

).`.venv/`

`.vscode/`

`shared/`

`additional_functions/`

[blueprints](#organizing-with-blueprints).`tests/`

`Dockerfile`

In the Python v2 programming model, Azure Functions uses a **decorator-based approach** to define triggers and bindings directly in your code. Each function is implemented as a **global, stateless method** within a `function_app.py`

file.

**Example**

Here's a simple function that responds to an HTTP request:

```
import azure.functions as func
app = func.FunctionApp()
@app.route("hello")
def http_trigger(req):
user = req.params.get("user")
return f"Hello, {user}!"
```


```
# requirements.txt
azure-functions
```


#### Key concepts

- The code imports the
`azure-functions`

package and uses decorators and types to define the function app. - The function has a single HTTP trigger.
- The
[HttpRequest](/en-us/python/api/azure-functions/azure.functions.httprequest)object contains request headers, query parameters, route parameters, and the message body. This function gets the value of the`name`

query parameter from the`params`

parameter of the[HttpRequest](/en-us/python/api/azure-functions/azure.functions.httprequest)object. - To send a name in this example, append
`?name={name}`

to the exposed function URL. For example, if running locally, the full URL might look like`http://localhost:7071/api/http_trigger?name=Test`

. For examples using bindings, see[Triggers and Bindings](#triggers-and-bindings).

#### The `azure-functions`

library

The `azure-functions`

Python library is a core part of the Azure Functions programming model. It provides the decorators, trigger and binding types, and request/response objects used to define and interact with functions at runtime.
To see all types and decorators available, visit the [ azure-functions API](/en-us/python/api/azure-functions/).
Your function app code depends on this library to:

- Define all functions using the
`FunctionApp`

object - Declare triggers and bindings (for example,
`@app.route`

,`@app.timer_trigger`

) - Access typed inputs and outputs (such as
`HttpRequest`

and`HttpResponse`

, and Out`)

The `azure-functions`

must be included in your project dependencies. To learn more, see [package management](#package-management).

Note

The `azure-functions`

library defines the programming surface for Python Azure Functions, but it isn’t a general-purpose SDK. Use it specifically for authoring and running functions within the Azure Functions runtime.

Use **type annotations** to improve IntelliSense and editor support:

```
def http_trigger(req: func.HttpRequest) -> str:
```


### Organizing with blueprints

For larger or modular apps, use *blueprints* to define functions in separate Python files
and register them with your main app. This separation keeps your code organized and reusable.

To define and register a blueprint:

Define a blueprint in another Python file, such as

`http_blueprint.py`

:`import azure.functions as func bp = func.Blueprint() @bp.route(route="default_template") def default_template(req: func.HttpRequest) -> func.HttpResponse: return func.HttpResponse("Hello World!")`

Register the blueprint in main

`function_app.py`

file:`import azure.functions as func from http_blueprint import bp app = func.FunctionApp() app.register_functions(bp)`


By using blueprints, you can:

- Break up your app into reusable modules
- Keep related functions grouped by file or feature
- Extend or share blueprints across projects

Note

Durable Functions also supports blueprints by using [ azure-functions-durable](https://pypi.org/project/azure-functions-durable).

[View sample →](https://github.com/Azure/azure-functions-durable-python/tree/dev/samples-v2/blueprint)

### Folder structure

Use the following structure for a Python Azure Functions project:

```
<project_root>/
│
├── .venv/ # (Optional) Local Python virtual environment
├── .vscode/ # (Optional) VS Code workspace settings
│
├── function_app.py # Main function entry point (decorator model)
├── shared/ # (Optional) Pure helper code with no triggers/bindings
│ └── utils.py
│
├── additional_functions/ # (Optional) Contains blueprints for organizing related Functions
│ └── blueprint_1.py
│
├── tests/ # (Optional) Unit tests for your functions
│ └── test_my_function.py
│
├── .funcignore # Excludes files from being published
├── host.json # Global function app configuration
├── local.settings.json # Local-only app settings (not published)
├── requirements.txt # (Optional) Defines Python dependencies for remote build
├── Dockerfile # (Optional) For custom container deployment
```


#### Key files and folders

| File / Folder | Description | Required for app to run in Azure |
|---|---|---|
`function_app.py` |
Main script where Azure Functions and triggers are defined using decorators. | ✅ |
`host.json` |
Global configuration for all functions in the app. | ✅ |
`requirements.txt` |
Python dependencies installed during publish when using
|

`local.settings.json`

`.funcignore`

`.venv/`

, `tests/`

, `local.settings.json`

).`.venv/`

`.vscode/`

`shared/`

`additional_functions/`

[blueprints](#organizing-with-blueprints).`tests/`

`Dockerfile`

[NOTE!] Include a

`requirements.txt`

file when you deploy with[remote build]. If you don't use remote build or want to use another file for defining app dependencies, you can perform a[local build]and deploy the app with pre-built dependencies.

For guidance on unit testing, see

[Unit Testing]. For container deployments, see[Deploy with custom containers].

### Triggers and bindings

Azure Functions uses **triggers** to start function execution and **bindings** to connect your code to other services
like storage, queues, and databases. In the Python v2 programming model, you declare bindings by using decorators.

Two main types of bindings exist:

**Triggers**(input that starts the function)**Inputs and outputs**(extra data sources or destinations)

For more information about the available triggers and bindings, see [Triggers and Bindings in Azure Functions](functions-triggers-bindings).

#### Example: Timer Trigger with Blob Input

This function:

- Triggers every 10 minutes
- Reads from a Blob by using
[SDK Type Bindings](#sdk-type-bindings) - Caches results and writes to a temporary file

```
import azure.functions as func
import azurefunctions.extensions.bindings.blob as blob
import logging
import tempfile
CACHED_BLOB_DATA = None
app = func.FunctionApp()
@app.function_name(name="TimerTriggerWithBlob")
@app.schedule(schedule="0 */10 * * * *", arg_name="mytimer")
@app.blob_input(arg_name="client",
path="PATH/TO/BLOB",
connection="BLOB_CONNECTION_SETTING")
def timer_trigger_with_blob(mytimer: func.TimerRequest,
client: blob.BlobClient,
context: func.Context) -> None:
global CACHED_BLOB_DATA
if CACHED_BLOB_DATA is None:
# Download blob and save as a global variable
CACHED_BLOB_DATA = client.download_blob().readall()
# Create temp file prefix
my_prefix = context.invocation_id
temp_file = tempfile.NamedTemporaryFile(prefix=my_prefix)
temp_file.write(CACHED_BLOB_DATA)
logging.info(f"Cached data written to {temp_file.name}")
```


#### Key concepts

- Use SDK type bindings to work with rich types. For more information, see
[SDK type bindings](#sdk-type-bindings). - You can use global variables to cache expensive computations, but their state isn't guaranteed to persist across function executions.
- Temporary files are stored in
`tmp/`

and aren't guaranteed to persist across invocations or scale-out instances. - You can access the invocation context of a function through the
[Context class](/en-us/python/api/azure-functions/azure.functions.context).

#### Example: HTTP Trigger with Cosmos DB Input and Event Hub Output

This function:

- Triggers on an HTTP request
- Reads from a Cosmos DB
- Writes to an Event Hub output
- Returns an HTTP response

```
# __init__.py
import azure.functions as func
def main(req: func.HttpRequest,
documents: func.DocumentList,
event: func.Out[str]) -> func.HttpResponse:
# Content from HttpRequest and Cosmos DB input
http_content = req.params.get("body")
doc_id = documents[0]["id"] if documents else "No documents found"
event.set(f"HttpRequest content: {http_content} | CosmosDB ID: {doc_id}")
return func.HttpResponse(
"Function executed successfully.",
status_code=200
)
```


```
// function.json
{
"scriptFile": "__init__.py",
"entryPoint": "main",
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": ["get", "post"],
"route": "file"
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"type": "cosmosDB",
"direction": "in",
"name": "documents",
"databaseName": "test",
"containerName": "items",
"id": "cosmosdb-input-test",
"connection": "COSMOSDB_CONNECTION_SETTING"
},
{
"type": "eventHub",
"direction": "out",
"name": "event",
"eventHubName": "my-test-eventhub",
"connection": "EVENTHUB_CONNECTION_SETTING"
}
]
}
```


**Key concepts**

- Each function has a single trigger, but it can have multiple bindings.
- Add inputs by specifying the
`direction`

as "in" in`function.json`

. Outputs have a`direction`

of`out`

. - You can access request details through the
`HttpRequest`

object and construct a custom`HttpResponse`

with headers, status code, and body.

```
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="HttpTriggerWithCosmosDB")
@app.route(route="file")
@app.cosmos_db_input(arg_name="documents",
database_name="test",
container_name="items",
connection="COSMOSDB_CONNECTION_SETTING")
@app.event_hub_output(arg_name="event",
event_hub_name="my-test-eventhub",
connection="EVENTHUB_CONNECTION_SETTING")
def http_trigger_with_cosmosdb(req: func.HttpRequest,
documents: func.DocumentList,
event: func.Out[str]) -> func.HttpResponse:
# Content from HttpRequest and Cosmos DB input
http_content = req.params.get('body')
doc_id = documents[0]['id']
event.set("HttpRequest content: " + http_content
+ " | CosmosDB ID: " + doc_id)
return func.HttpResponse(
f"Function executed successfully.",
status_code=200
)
```


#### Key concepts

- Use
`@route()`

or trigger-specific decorators (`@timer_trigger`

,`@queue_trigger`

, and others) to define how your function is invoked. - Add inputs by using decorators like
`@blob_input`

,`@queue_input`

, and others. - Outputs can be:
- Returned directly (if only one output)
- Assigned by using
`Out`

bindings and the`.set()`

method for multiple outputs.

- You can access request details through the
`HttpRequest`

object and construct a custom`HttpResponse`

with headers, status code, and body.

### SDK type bindings

For select triggers and bindings, you can work with data types implemented by the underlying Azure SDKs and frameworks.
By using these *SDK type bindings*, you can interact with binding data as if you were using the underlying service SDK.
For more information, see [supported SDK type bindings](functions-triggers-bindings?pivots=programming-language-python#sdk-types).

Important

SDK type bindings support for Python is only available in the Python v2 programming model.

### Environment variables

Environment variables in Azure Functions let you securely manage configuration values, connection strings, and app secrets without hardcoding them in your function code.

You can define environment variables:

- Locally: in the
[local.settings.json file](functions-develop-local#local-settings-file), during local development. - In Azure: as
[Application Settings](functions-how-to-use-azure-function-app-settings#settings)in your Function App's configuration page in the Azure portal.

Access the variables directly in your code by using `os.environ`

or `os.getenv`

.

```
setting_value = os.getenv("myAppSetting", "default_value")
```


Note

Azure Functions also recognizes system environment variables that configure the Functions runtime and Python worker behavior. These variables aren't explicitly used in your function code but affect how your app runs. For a complete list of system environment variables, see [App settings reference](functions-app-settings).

### Package management

To use other Python packages in your Azure Functions app, list them in a `requirements.txt`

file at the root of your project. These packages are imported by Python's import system, and you can then reference those packages as usual.
To learn more about building and deployment options with external dependencies, see [Build Options for Python Function Apps](python-build-options).

For example, the following sample shows how the `requests`

module is included and used in the function app.

```
<requirements.txt>
requests==2.31.0
```


Install the package locally with `pip install -r requirements.txt`

.

Once the package is installed, you can import and use it in your function code:

```
import azure.functions as func
import requests
def main(req: func.HttpRequest) -> func.HttpResponse:
r = requests.get("https://api.github.com")
return func.HttpResponse(f"Status: {r.status_code}")
```


```
import azure.functions as func
import requests
app = func.FunctionApp()
@app.function_name(name="HttpExample")
@app.route(route="call_api")
def main(req: func.HttpRequest) -> func.HttpResponse:
r = requests.get("https://api.github.com")
return func.HttpResponse(f"Status: {r.status_code}")
```


#### Considerations

- Conflicts with built-in modules:
- Avoid naming your project folders after
[Python standard libraries](https://docs.python.org/3/library/)(for example,`email/`

,`json/`

). - Don't include Python native libraries (like
`logging`

,`asyncio`

, or`uuid`

) in`requirements.txt`

.

- Avoid naming your project folders after
- Deployment:
- To prevent
, ensure all required dependencies are listed in`ModuleNotFound`

errors`requirements.txt`

. - If you update your app's Python version, rebuild and redeploy your app on the new Python version to avoid dependency conflicts with previously built packages.

- To prevent
- Non-PyPI Dependencies:
- You can include dependencies that aren't available on PyPI in your app, such as local packages, wheel files, or private feeds. See
[Custom dependencies in Python Azure Functions](python-build-options#custom-dependencies)for setup instructions.

- You can include dependencies that aren't available on PyPI in your app, such as local packages, wheel files, or private feeds. See
- Azure Functions Python worker dependencies:
- If your package contains certain libraries that might collide with worker's dependencies (for example,
`protobuf`

or`grpcio`

), configure[PYTHON_ISOLATE_WORKER_DEPENDENCIES](functions-app-settings#python_isolate_worker_dependencies)to 1 in app settings to prevent your application from referring to worker's dependencies. For Python 3.13 and above,[this feature is enabled by default](#python-313-updates).

- If your package contains certain libraries that might collide with worker's dependencies (for example,

## Running and deploying

This section provides information about [running functions locally](#running-locally), [Python version support](#supported-python-versions), [build and deployment options](#build-and-deployment), and runtime configuration. Use this information to successfully run your function app in both local and Azure environments.

### Running locally

You can run and test your Python function app on your local machine before deploying to Azure.

#### Using Azure Functions Core Tools

Install [Azure Functions Core Tools](functions-run-local) and start the local runtime by running the `func start`

command from your project root:

```
func start
```


When you start the function app locally, Core Tools displays all the functions it finds for your app:

```
Functions:
http_trigger: http://localhost:7071/api/http_trigger
```


You can learn more about how to use Core Tools by visiting [Develop Azure Functions locally using Core Tools](functions-run-local).

#### Invoking the function directly

By using `azure-functions >= 1.21.0`

, you can also call functions directly by using the Python interpreter without running Core Tools. This approach is useful for quick unit tests:

```
# function_app.py
import azure.functions as func
app = func.FunctionApp(http_auth_level=func.AuthLevel.ANONYMOUS)
@app.route(route="http_trigger")
def http_trigger(req: func.HttpRequest) -> func.HttpResponse:
return "Hello, World!"
# Test the function directly
print(http_trigger(None))
```


To see the output, run the file directly with Python:

```
> python function_app.py
Hello, World!
```


```
# __init__.py
import azure.functions as func
def main(req: func.HttpRequest) -> func.HttpResponse:
return func.HttpResponse("Hello, World!")
# Test the function directly
print(main(None))
```


To see the output, run the file directly with Python:

```
> python __init__.py
Hello, World!
```


This approach doesn't require any extra packages or setup and is ideal for quick validation during development. For more in-depth testing, see [Unit Testing](#unit-testing)

### Supported Python versions

Azure Functions supports the Python versions listed in [Supported languages in Azure Functions](supported-languages).
For more general information, see the [Azure Functions runtime support policy](language-support-policy).

Important

If you change the Python version for your function app, you must rebuild and redeploy the app by using the new version. Existing deployment artifacts and dependencies aren't automatically rebuilt when the Python version changes.

## Build and Deployment

To learn more about the recommended build mechanism for your scenario, see [Build Options](python-build-options). For a general overview of deployment, see [Deployment technologies in Azure Functions](functions-deployment-technologies).

**Deployment Mechanisms Quick Comparison**

Tool / Platform |
Command / Action |
Best Use Case |
|---|---|---|
Azure Functions Core Tools |

`func azure functionapp publish <APP_NAME>`

**AZ CLI**`az functionapp deployment source config-zip`

**Visual Studio Code (Azure Functions Extension)****Command Palette → “Azure Functions: Deploy to Azure…”****GitHub Actions**`Azure/functions-action@v1`

**Azure Pipelines**`AzureFunctionApp@2`

task**Custom Container Deployment**`az functionapp create --image <container>`

**Portal-based Function Creation**[Azure portal](https://portal.azure.com)→ inline editor**simple**, dependency-free functions. Great for demos or learning, but**not recommended**for apps requiring third-party packages.Note

[ Portal-based Function Creation](functions-create-function-app-portal) doesn't support third-party dependencies and isn't recommended for creating production apps. You can't install or reference packages outside

`azure-functions`

and the built-in Python standard library.Important

After 30 September 2028, the option to host your function app on Linux in a Consumption plan is retired. To avoid disruptions, migrate your existing Consumption plan apps that run on Linux to the [Flex Consumption plan](flex-consumption-plan) before that date. Apps running on Windows in a Consumption plan aren't affected by this change.
For more information, see the [Linux Consumption plan retirement notice](https://go.microsoft.com/fwlink/?linkid=2335809).

### Python 3.13+ updates

Starting with Python 3.13, Azure Functions introduces several major runtime and performance improvements that affect how you build and run your apps. Key changes include:

Runtime version control: You can now optionally pin or upgrade your app to specific Python worker versions by referencing the

package in your`azure-functions-runtime`

`requirements.txt`

.Without version control enabled, your app runs on a default version of the Python runtime, which Functions manages. You must modify your

*requirements.txt*file to request the latest released version, a prereleased version, or to pin your app to a specific version of the Python runtime.You enable runtime version control by adding a reference to the Python runtime package to your

*requirements.txt*file, where the value assigned to the package determines the runtime version used.Avoid pinning any production app to prerelease (alpha, beta, or dev) runtime versions.

To be aware of changes, review

[Python runtime release notes](https://github.com/Azure/azure-functions-python-worker/releases)regularly.The following table indicates the versioning behavior based on the version value of this setting in your

*requirements.txt*file:Version Example Behavior No value set `azure-functions-runtime`

Your Python 3.13+ app runs on the latest available version of the Functions Python runtime. This option is best for staying current with platform improvements and features, since your app automatically receives the latest stable runtime updates. Pinned to a specific version `azure-functions-runtime==1.2.0`

Your Python 3.13+ app stays on the pinned runtime version and doesn't receive automatic updates. You must instead manually update your pinned version to take advantage of new features, fixes, and improvements in the runtime. Pinning is recommended for critical production workloads where stability and predictability are essential. Pinning also lets you test your app on prereleased runtime versions during development. No package reference n/a By not setting the `azure-functions-runtime`

, your Python 3.13+ app runs on a default version of the Python runtime that is behind the latest released version. Updates are made periodically by Functions. This option ensures stability and broad compatibility. However, access to the newest features and fixes are delayed until the default version is updated.

Dependency isolation: Your app’s dependencies (like

`grpcio`

or`protobuf`

) are fully isolated from the worker’s dependencies, preventing version conflicts. The app settingwill have no impact for apps running on Python 3.13 or later.`PYTHON_ISOLATE_WORKER_DEPENDENCIES`

Simplified

[HTTP streaming](functions-bindings-http-webhook-trigger?tabs=python-v2&pivots=programming-language-python#http-streams-1)setup—no special app settings required.Removed support for worker extensions and shared memory features.


Runtime version control: You can now optionally pin or upgrade your app to specific Python worker versions by referencing the

package in your`azure-functions-runtime-v1`

`requirements.txt`

.Without version control enabled, your app runs on a default version of the Python runtime, which Functions manages. You must modify your

*requirements.txt*file to request the latest released version, a prereleased version, or to pin your app to a specific version of the Python runtime.You enable runtime version control by adding a reference to the Python runtime package to your

*requirements.txt*file, where the value assigned to the package determines the runtime version used.Avoid pinning any production app to prerelease (alpha, beta, or dev) runtime versions.

To be aware of changes, review

[Python runtime release notes](https://github.com/Azure/azure-functions-python-worker/releases)regularly.The following table indicates the versioning behavior based on the version value of this setting in your

*requirements.txt*file:Version Example Behavior No value set `azure-functions-runtime-v1`

Your Python 3.13+ app runs on the latest available version of the Functions Python runtime. This option is best for staying current with platform improvements and features, since your app automatically receives the latest stable runtime updates. Pinned to a specific version `azure-functions-runtime-v1==1.2.0`

Your Python 3.13+ app stays on the pinned runtime version and doesn't receive automatic updates. You must instead manually update your pinned version to take advantage of new features, fixes, and improvements in the runtime. Pinning is recommended for critical production workloads where stability and predictability are essential. Pinning also lets you test your app on prereleased runtime versions during development. No package reference n/a By not setting the `azure-functions-runtime-v1`

, your Python 3.13+ app runs on a default version of the Python runtime that is behind the latest released version. Updates are made periodically by Functions. This option ensures stability and broad compatibility. However, access to the newest features and fixes are delayed until the default version is updated.

Dependency isolation: Your app’s dependencies (like

`grpcio`

or`protobuf`

) are fully isolated from the worker’s dependencies, preventing version conflicts. The app settingwill have no impact for apps running on Python 3.13 or later.`PYTHON_ISOLATE_WORKER_DEPENDENCIES`

Removed support for worker extensions and shared memory features.


## Observability and testing

This section covers [logging](#logging-and-monitoring), [monitoring](#opentelemetry-support), and [testing capabilities](#unit-testing) to help you debug problems, track performance, and ensure the reliability of your Python function apps.

### Logging and monitoring

Azure Functions exposes a root logger that you can use directly with Python's built-in `logging`

module. Any messages written using this logger are automatically sent to **Application Insights** when your app is running in Azure.

Logging allows you to capture runtime information and diagnose issues without needing any more setup.

#### Logging example with an HTTP trigger

```
import logging
import azure.functions as func
def main(req: func.HttpRequest) -> func.HttpResponse:
logging.debug("Example debug log")
logging.info("Example info log")
logging.warning("Example warning")
logging.error("Example error log")
return func.HttpResponse("OK")
```


```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.route(route="http_trigger")
def http_trigger(req) -> func.HttpResponse:
logging.debug("Example debug log")
logging.info("Example info log")
logging.warning("Example warning")
logging.error("Example error log")
return func.HttpResponse("OK")
```


You can use the full set of logging levels (`debug`

, `info`

, `warning`

, `error`

, `critical`

), and they appear in the Azure portal under Logs or Application Insights.

To learn more about monitoring Azure Functions in the portal, see [Monitor Azure Functions](functions-monitoring).

Note

To view debug logs in Application Insights, more setup is required. You can enable this feature by setting [PYTHON_ENABLE_DEBUG_LOGGING](functions-app-settings#python_enable_debug_logging) to `1`

and setting `logLevel`

to `trace`

or `debug`

in your [host.json file](functions-host-json#logging). By default, debug logs aren't visible in Application Insights.

#### Logging from background threads

If your function starts a new thread and needs to log from that thread, make sure to pass the `context`

argument into the thread. The `context`

contains thread-local storage and the current `invocation_id`

, which must be set on the worker thread in order for logs to be associated properly with the function execution.

```
import logging
import threading
import azure.functions as func
def main(req: func.HttpRequest, context) -> func.HttpResponse:
logging.info("Function started")
t = threading.Thread(target=log_from_thread, args=(context,))
t.start()
return "okay"
def log_from_thread(context):
# Associate the thread with the current invocation
context.thread_local_storage.invocation_id = context.invocation_id
logging.info("Logging from a background thread")
```


```
import azure.functions as func
import logging
import threading
app = func.FunctionApp()
@app.route(route="http_trigger")
def http_trigger(req, context) -> func.HttpResponse:
logging.info("Function started")
t = threading.Thread(target=log_from_thread, args=(context,))
t.start()
return "okay"
def log_from_thread(context):
# Associate the thread with the current invocation
context.thread_local_storage.invocation_id = context.invocation_id
logging.info("Logging from a background thread")
```


#### Configuring custom loggers

You can configure custom loggers in Python when you need more control over logging behavior, such as custom formatting, log filtering, or third-party integrations.
To configure a custom logger, use Python's `logging.getLogger()`

with a custom name and add handlers or formatters as needed.

```
import logging
custom_logger = logging.getLogger('my_custom_logger')
```


### OpenTelemetry support

Azure Functions for Python also supports **OpenTelemetry**, which enables you to emit traces, metrics, and logs in a standardized format. Using OpenTelemetry is especially valuable for distributed applications or scenarios where you want to export telemetry to tools outside of Application Insights (such as Grafana or Jaeger).

See our

[OpenTelemetry Quickstart for Azure Functions (Python)]for setup instructions and sample code.

### Unit testing

Write and run unit tests for your functions by using `pytest`

.
You can test Python functions like other Python code by using standard testing frameworks. For most bindings, you can create a mock input object by creating an instance of an appropriate class from the `azure.functions`

package.

By using `my_function`

as an example, the following example is a mock test of an HTTP-triggered function:

First, create the *<project_root>/function_app.py* file and implement the `my_function`

function as the HTTP trigger.

```
# <project_root>/function_app.py
import azure.functions as func
import logging
app = func.FunctionApp()
# Define the HTTP trigger that accepts the ?value=<int> query parameter
# Double the value and return the result in HttpResponse
@app.function_name(name="my_function")
@app.route(route="hello")
def my_function(req: func.HttpRequest) -> func.HttpResponse:
logging.info('Executing myfunction.')
initial_value: int = int(req.params.get('value'))
doubled_value: int = initial_value * 2
return func.HttpResponse(
body=f"{initial_value} * 2 = {doubled_value}",
status_code=200
)
```


You can start writing test cases for your HTTP trigger.

```
# <project_root>/test_my_function.py
import unittest
import azure.functions as func
from function_app import my_function
class TestFunction(unittest.TestCase):
def test_my_function(self):
# Construct a mock HTTP request.
req = func.HttpRequest(method='GET',
body=None,
url='/api/my_function',
params={'value': '21'})
# Call the function.
func_call = main.build().get_user_function()
resp = func_call(req)
# Check the output.
self.assertEqual(
resp.get_body(),
b'21 * 2 = 42',
)
```


Inside your Python virtual environment folder, you can run the following commands to test the app:

```
pip install pytest
pytest test_my_function.py
```


You see the `pytest`

results in the terminal, like this:

```
============================================================================================================ test session starts ============================================================================================================
collected 1 item
test_my_function.py . [100%]
============================================================================================================= 1 passed in 0.24s =============================================================================================================
```


## Optimization and advanced topics

To learn more about optimizing your Python functions apps, see these articles:

## Related articles

For more information about Functions, see these articles:

[Azure Functions package API documentation](/en-us/python/api/azure-functions/azure.functions)[Best practices for Azure Functions](functions-best-practices)[Azure Functions triggers and bindings](functions-triggers-bindings)[Blob Storage bindings](functions-bindings-storage-blob)[HTTP and webhook bindings](functions-bindings-http-webhook)[Queue Storage bindings](functions-bindings-storage-queue)[Timer triggers](functions-bindings-timer)

[Having issues with using Python? Let us know and file an issue.](https://github.com/Azure/azure-functions-python-worker/issues)

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/opentelemetry-howto -->

# Use OpenTelemetry with Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to configure your function app to export log and trace data in an OpenTelemetry format. Azure Functions generates telemetry data on your function executions from both the Functions host process and the language-specific worker process in which your function code runs. By default, this telemetry data is sent to Application Insights by using the Application Insights SDK. However, you can choose to export this data by using OpenTelemetry semantics. While you can still use an OpenTelemetry format to send your data to Application Insights, you can now also export the same data to any other OpenTelemetry-compliant endpoint.

You can obtain these benefits by enabling OpenTelemetry in your function app:

- Correlates data across traces and logs being generated both at the host and in your application code.
- Enables consistent, standards-based generation of exportable telemetry data.
- Integrates with other providers that can consume OpenTelemetry-compliant data.

Keep these considerations in mind when using this article:

Try the

[OpenTelemetry tutorial](monitor-functions-opentelemetry-distributed-tracing), which is designed to help you get started quickly with OpenTelemetry and Azure Functions. This article uses the Azure Developer CLI (`azd`

) to create and deploy a function app that uses OpenTelemetry integration for distributed tracing.Because this article is targeted at your development language of choice, remember to choose the correct language at the top of the article.


- OpenTelemetry currently isn't supported for
[C# in-process apps](functions-dotnet-class-library).

- OpenTelemetry is enabled at the function app level, both in host configuration (
`host.json`

) and in your code project. Functions also provides a client optimized experience for exporting OpenTelemetry data from your function code that's running in a language-specific worker process.

## Enable OpenTelemetry in the Functions host

When you enable OpenTelemetry output in the function app's `host.json`

file, your host exports OpenTelemetry output regardless of the language stack used by your app.

To enable OpenTelemetry output from the Functions host, update the [host.json file](functions-host-json) in your code project to add a `"telemetryMode": "OpenTelemetry"`

element to the root collection. With OpenTelemetry enabled, your host.json file might look like this:

```
{
"version": "2.0",
"telemetryMode": "OpenTelemetry",
...
}
```


## Configure application settings

When you enable OpenTelemetry in the `host.json`

file, the app's environment variables determine the endpoints for sending data based on which OpenTelemetry-supported application settings are available.

Create specific application settings in your function app based on the OpenTelemetry output destination. When you provide connection settings for both Application Insights and an OpenTelemetry protocol (OTLP) exporter, OpenTelemetry data is sent to both endpoints.

** APPLICATIONINSIGHTS_CONNECTION_STRING**: the connection string for an Application Insights workspace. When this setting exists, OpenTelemetry data is sent to that workspace. Use the same setting to connect to Application Insights without OpenTelemetry enabled. If your app doesn't already have this setting, you might need to

[Enable Application Insights integration](configure-monitoring#enable-application-insights-integration).

** JAVA_APPLICATIONINSIGHTS_ENABLE_TELEMETRY**: set to

`true`

so that the Functions host allows the Java worker process to stream OpenTelemetry logs directly, which prevents duplicate host-level entries.** PYTHON_APPLICATIONINSIGHTS_ENABLE_TELEMETRY**: set to

`true`

so that the Functions host allows the Python worker process to stream OpenTelemetry logs directly, which prevents duplicate host-level entries.## Enable OpenTelemetry in your app

After you configure the Functions host to use OpenTelemetry, update your application code to output OpenTelemetry data. When you enable OpenTelemetry in both the host and your application code, you get better correlation between traces and logs that the Functions host process and your language worker process emit.

How you instrument your application to use OpenTelemetry depends on your target OpenTelemetry endpoint:

Examples in this article assume your app uses `IHostApplicationBuilder`

, which is available in version 2.x and later version of [Microsoft.Azure.Functions.Worker](/en-us/dotnet/api/microsoft.extensions.hosting.ihostapplicationbuilder). For more information, see [Version 2.x](dotnet-isolated-process-guide#version-2x) in the C# isolated worker model guide.

Run these commands to install the required assemblies in your app:

`dotnet add package Microsoft.Azure.Functions.Worker.OpenTelemetry dotnet add package OpenTelemetry.Extensions.Hosting dotnet add package Azure.Monitor.OpenTelemetry.Exporter`

In your Program.cs project file, add this

`using`

statement:`using Azure.Monitor.OpenTelemetry.Exporter;`

Configure OpenTelemetry based on whether your project startup uses

`IHostBuilder`

or`IHostApplicationBuilder`

. The latter was introduced in v2.x of the .NET isolated worker model extension.In

*program.cs*, add this line of code after`ConfigureFunctionsWebApplication`

:`builder.Services.AddOpenTelemetry() .UseFunctionsWorkerDefaults() .UseAzureMonitorExporter();`

You can export to both OpenTelemetry endpoints from the same app.


Add the required libraries to your app. The way you add libraries depends on whether you deploy using Maven or Kotlin and if you want to also send data to Application Insights.

`<dependency> <groupId>com.microsoft.azure.functions</groupId> <artifactId>azure-functions-java-opentelemetry</artifactId> <version>1.0.0</version> </dependency> <dependency> <groupId>com.azure</groupId> <artifactId>azure-monitor-opentelemetry-autoconfigure</artifactId> <version>1.2.0</version> </dependency>`

(Optional) Add this code to create custom spans:

`import com.microsoft.azure.functions.opentelemetry.FunctionsOpenTelemetry; import io.opentelemetry.api.trace.Span; import io.opentelemetry.api.trace.SpanKind; import io.opentelemetry.context.Scope; Span span = FunctionsOpenTelemetry.startSpan( "com.contoso.PaymentFunction", // tracer name "validateCharge", // span name null, // parent = current context SpanKind.INTERNAL); try (Scope ignored = span.makeCurrent()) { // business logic here } finally { span.end(); }`


Install these npm packages in your project:

`npm install @opentelemetry/api npm install @opentelemetry/auto-instrumentations-node npm install @azure/monitor-opentelemetry-exporter npm install @azure/functions-opentelemetry-instrumentation`


Create a code file in your project, copy and paste the following code in this new file, and save the file as

`src/index.js`

:`const { AzureFunctionsInstrumentation } = require('@azure/functions-opentelemetry-instrumentation'); const { AzureMonitorLogExporter, AzureMonitorTraceExporter } = require('@azure/monitor-opentelemetry-exporter'); const { getNodeAutoInstrumentations, getResourceDetectors } = require('@opentelemetry/auto-instrumentations-node'); const { registerInstrumentations } = require('@opentelemetry/instrumentation'); const { detectResourcesSync } = require('@opentelemetry/resources'); const { LoggerProvider, SimpleLogRecordProcessor } = require('@opentelemetry/sdk-logs'); const { NodeTracerProvider, SimpleSpanProcessor } = require('@opentelemetry/sdk-trace-node'); const resource = detectResourcesSync({ detectors: getResourceDetectors() }); const tracerProvider = new NodeTracerProvider({ resource }); tracerProvider.addSpanProcessor(new SimpleSpanProcessor(new AzureMonitorTraceExporter())); tracerProvider.register(); const loggerProvider = new LoggerProvider({ resource }); loggerProvider.addLogRecordProcessor(new SimpleLogRecordProcessor(new AzureMonitorLogExporter())); registerInstrumentations({ tracerProvider, loggerProvider, instrumentations: [getNodeAutoInstrumentations(), new AzureFunctionsInstrumentation()], });`

Update the

`main`

field in your package.json file to include the new`src/index.js`

file. For example:`"main": "src/{index.js,functions/*.js}"`


Create a code file in your project, copy and paste the following code in this new file, and save the file as

`src/index.ts`

:`import { AzureFunctionsInstrumentation } from '@azure/functions-opentelemetry-instrumentation'; import { AzureMonitorLogExporter, AzureMonitorTraceExporter } from '@azure/monitor-opentelemetry-exporter'; import { getNodeAutoInstrumentations, getResourceDetectors } from '@opentelemetry/auto-instrumentations-node'; import { registerInstrumentations } from '@opentelemetry/instrumentation'; import { detectResourcesSync } from '@opentelemetry/resources'; import { LoggerProvider, SimpleLogRecordProcessor } from '@opentelemetry/sdk-logs'; import { NodeTracerProvider, SimpleSpanProcessor } from '@opentelemetry/sdk-trace-node'; const resource = detectResourcesSync({ detectors: getResourceDetectors() }); const tracerProvider = new NodeTracerProvider({ resource }); tracerProvider.addSpanProcessor(new SimpleSpanProcessor(new AzureMonitorTraceExporter())); tracerProvider.register(); const loggerProvider = new LoggerProvider({ resource }); loggerProvider.addLogRecordProcessor(new SimpleLogRecordProcessor(new AzureMonitorLogExporter())); registerInstrumentations({ tracerProvider, loggerProvider, instrumentations: [getNodeAutoInstrumentations(), new AzureFunctionsInstrumentation()], });`

Update the

`main`

field in your package.json file to include the output of this new`src/index.ts`

file, which might look like this:`"main": "dist/src/{index.js,functions/*.js}"`


Important

OpenTelemetry output to Application Insights from the language worker isn't currently supported for PowerShell apps. You might instead want to use an OTLP exporter endpoint. When you configure your host for OpenTelemetry output to Application Insights, the logs generated by the PowerShell worker process are still forwarded, but distributed tracing isn't supported at this time.

These instructions only apply for an OTLP exporter:

Add an application setting named

`OTEL_FUNCTIONS_WORKER_ENABLED`

with value of`True`

.Create an

[app-level](functions-reference-powershell#including-modules-in-app-content)in the root of your app and run the following command:`Modules`

folder`Save-Module -Name AzureFunctions.PowerShell.OpenTelemetry.SDK`

This command installs the required

`AzureFunctions.PowerShell.OpenTelemetry.SDK`

module directly in your app. You can't use the`requirements.psd1`

file to automatically install this dependency because[managed dependencies](functions-reference-powershell#dependency-management)isn't currently supported in the[Flex Consumption plan](flex-consumption-plan)preview.Add this code to your profile.ps1 file:

`Import-Module AzureFunctions.PowerShell.OpenTelemetry.SDK -Force -ErrorAction Stop Initialize-FunctionsOpenTelemetry`


Make sure these libraries are in your

`requirements.txt`

file, whether from uncommenting or adding yourself:`azure-monitor-opentelemetry`

Add this code to your

`function_app.py`

main entry point file:If you already added

`PYTHON_APPLICATIONINSIGHTS_ENABLE_TELEMETRY=true`

in your application settings, you can skip this step. To manually enable Application Insights collection without automatic instrumentation, add this code to your app:`from azure.monitor.opentelemetry import configure_azure_monitor configure_azure_monitor()`

Review

[Azure monitor Distro usage](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/monitor/azure-monitor-opentelemetry#usage)documentation for options on how to further configure the SDK.

## Considerations for OpenTelemetry

When you export your data by using OpenTelemetry, keep these considerations in mind.

The Azure portal supports

`Recent function invocation`

traces only if the telemetry is sent to Azure Monitor.When you configure the host to use OpenTelemetry, the Azure portal doesn't support log streaming.

If you set

`telemetryMode`

to`OpenTelemetry`

, the configuration in the`logging.applicationInsights`

section of host.json doesn't apply.

Custom spans automatically include all resource attributes and use the exporters configured in your app.

When your app runs outside Azure, including during local development, the resource detector sets the

`service.name`

attribute to`java-function-app`

by default.Use these Java Virtual Machine (JVM) flags to silence telemetry when running locally during unit tests:

`-Dotel.traces.exporter=none`

`-Dotel.metrics.exporter=none`

`-Dotel.logs.exporter=none`


- You don't need to manually register middleware; the Java worker autodiscovers
`OpenTelemetryInvocationMiddleware`

.

## Resource detectors and semantic conventions

In Azure Functions, resource attributes describe the function app process and its environment. Span attributes describe a single invocation.

### Default behavior (no action required)

In Azure Functions on App Service, resource detectors typically populate common attributes automatically, including:

`service.name`

(defaults to the function app name)- Azure cloud attributes such as
`cloud.provider`

,`cloud.region`

, and`cloud.resource_id`


In most cases, these defaults are sufficient for correct Application Map grouping and Azure context.

### When to override `service.name`

(Cloud Role Name)

Override only if you need a different, stable node name in Application Insights (Application Map grouping), for example to normalize naming across slots or environments.

Set `OTEL_SERVICE_NAME`

to override the detected value:

```
export OTEL_SERVICE_NAME="my-function-app"
```


### Invocation span attributes (usually automatic)

You won’t have to set these manually unless you’re creating a custom invocation span.

`faas.name`

(function name)`faas.trigger`

(for example`http`

,`servicebus`

,`eventhubs`

)`faas.execution`

(invocation/execution identifier)

Important

Function apps can host multiple functions in one process. Do not put function-specific values on the resource. Put per-invocation identity on spans.

Note

When running locally (Functions Core Tools) or in containerized/self-hosted environments where Azure metadata is unavailable, `service.name`

may default to a generic value. Set `OTEL_SERVICE_NAME`

locally to match production naming.

## Troubleshooting

When you export your data by using OpenTelemetry, keep these common issues and solutions in mind.

### Log filtering

To correctly configure log filtering in your function app, you need to understand the difference between the host process and the worker process.

The *host process* is the Azure Functions runtime that manages triggers, scaling, and emits system-level telemetry such as initialization logs, request traces, and runtime health information.

The *worker process* is language specific, executes your function code, and produces application logs and telemetry independently.

Important

Filters defined in host.json apply only to logs generated by the host process. You must use language-specific OpenTelemetry settings to filter logs from the worker process.

**Example: Filter host logs for all providers in host.json**

Use this approach to set a global log level across all providers managed by the host:

```
{
"version": "2.0",
"telemetryMode": "OpenTelemetry",
"logging": {
"logLevel": {
"default": "Warning"
}
}
}
```


**Example: Filter logs only for the OpenTelemetry logger provider**

Use this approach to target only the OpenTelemetry logger provider while leaving other providers (such as console or file logging) unaffected:

```
{
"version": "2.0",
"telemetryMode": "OpenTelemetry",
"logging": {
"OpenTelemetry": {
"logLevel": {
"default": "Warning"
}
}
}
}
```


### Console logging

The Functions host automatically captures anything written to stdout or stderr and forwards it to the telemetry pipeline. If you also use a ConsoleExporter or write directly to console in your code, duplicate logs can occur in your telemetry data.

Note

To avoid duplicate telemetry entries, don't add ConsoleExporter or write to console in production code.

### Microsoft Entra authentication

When you use Microsoft Entra authentication with OpenTelemetry, you must configure authentication separately for both the host process and the worker process.

To configure authentication for the host process, see [Require Microsoft Entra authentication](configure-monitoring#require-microsoft-entra-authentication).

To configure authentication for the worker process, see [Enable Microsoft Entra authentication](/en-us/azure/azure-monitor/app/azure-ad-authentication).

### Resource attributes support

Resource attributes support in Azure Monitor is currently in preview. To enable this feature, set the `OTEL_DOTNET_AZURE_MONITOR_ENABLE_RESOURCE_METRICS`

environment variable to `true`

. This setting ingests resource attributes into the custom metrics table.

### Duplicate request telemetry

The host process automatically emits request telemetry. If the worker process is also instrumented with request tracking libraries (for example, AspNetCoreInstrumentation in .NET), the same request is reported twice.

Note

Since the Azure Monitor Distro typically includes AspNetCoreInstrumentation in .NET and similar instrumentation in other languages, avoid using the Azure Monitor distro in the worker process to prevent duplicate telemetry.

### Logging scopes not included

By default, the worker process doesn't include scopes in its logs. To enable scopes, you must configure this setting explicitly in the worker. The following example shows how to enable scopes in .NET Isolated:

```
builder.Logging.AddOpenTelemetry(b => b.IncludeScopes = true);
```


### Missing request telemetry

Triggers such as HTTP, Service Bus, and Event Hubs depend on context propagation for distributed tracing. With parent-based sampling as the default behavior, request telemetry isn't generated when the incoming request or message isn't sampled.

### Duplicate OperationId

In Azure Functions, the `OperationId`

used for correlating telemetry comes directly from the `traceparent`

value in the incoming request or message. If multiple calls reuse the same `traceparent`

value, they all get the same `OperationId`

.

### Configure OpenTelemetry with environment variables

You can configure OpenTelemetry behavior by using its standard environment variables. These variables provide a consistent way to control behavior across different languages and runtimes. You can adjust sampling strategies, exporter settings, and resource attributes. For more information about supported environment variables, see the [OpenTelemetry documentation](https://opentelemetry.io/docs/languages/sdk-configuration/).

### Use diagnostics to troubleshoot monitoring issues

[Azure Functions diagnostics](functions-diagnostics) in the Azure portal is a useful resource for detecting and diagnosing potential monitoring-related issues.

To access diagnostics in your app:

In the

[Azure portal](https://portal.azure.com), go to your function app resource.In the left pane, select

**Diagnose and solve problems**and search for the*Function App missing telemetry Application Insights or OpenTelemetry*workflow.Select this workflow, choose your ingestion method, and select

**Next**.Review the guidelines and any recommendations provided by the troubleshooter.


## Next steps

Learn more about OpenTelemetry and monitoring Azure Functions:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-integrate-store-unstructured-data-cosmosdb -->

# Store unstructured data using Azure Functions and Azure Cosmos DB

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a great way to store unstructured and JSON data. Combined with Azure Functions, Azure Cosmos DB makes storing data quick and easy with much less code than required for storing data in a relational database.

Note

At this time, the Azure Cosmos DB trigger, input bindings, and output bindings work with SQL API and Graph API accounts only.

In Azure Functions, input and output bindings provide a declarative way to connect to external service data from your function. In this article, learn how to update an existing function to add an output binding that stores unstructured data in an Azure Cosmos DB document.

## Prerequisites

To complete this tutorial:

This article uses as its starting point the resources created in [Create your first function in the Azure portal](functions-create-function-app-portal). If you haven't already done so, complete these steps now to create your function app.

## Create an Azure Cosmos DB account

You must have an Azure Cosmos DB account that uses the SQL API before you create the output binding.

From the Azure portal menu or the

**Home page**, select**Create a resource**.Search for

**Azure Cosmos DB**. Select**Create**>**Azure Cosmos DB**.On the

**Create an Azure Cosmos DB account**page, select the**Create**option within the**Azure Cosmos DB for NoSQL**section.Azure Cosmos DB provides several APIs:

- NoSQL, for document data
- PostgreSQL
- MongoDB, for document data
- Apache Cassandra
- Table
- Apache Gremlin, for graph data

To learn more about the API for NoSQL, see

[Welcome to Azure Cosmos DB](/en-us/azure/cosmos-db/introduction).In the

**Create Azure Cosmos DB Account**page, enter the basic settings for the new Azure Cosmos DB account.Setting Value Description Subscription Subscription name Select the Azure subscription that you want to use for this Azure Cosmos DB account. Resource Group Resource group name Select a resource group, or select **Create new**, then enter a unique name for the new resource group.Account Name A unique name Enter a name to identify your Azure Cosmos DB account. Because *documents.azure.com*is appended to the name that you provide to create your URI, use a unique name. The name can contain only lowercase letters, numbers, and the hyphen (-) character. It must be 3-44 characters.Location The region closest to your users Select a geographic location to host your Azure Cosmos DB account. Use the location that is closest to your users to give them the fastest access to the data. Capacity mode **Provisioned throughput**or**Serverless**Select **Provisioned throughput**to create an account in[provisioned throughput](/en-us/azure/cosmos-db/set-throughput)mode. Select**Serverless**to create an account in[serverless](/en-us/azure/cosmos-db/serverless)mode.Apply Azure Cosmos DB free tier discount **Apply**or**Do not apply**With Azure Cosmos DB free tier, you get the first 1000 RU/s and 25 GB of storage for free in an account. Learn more about [free tier](https://azure.microsoft.com/pricing/details/cosmos-db/).Limit total account throughput Selected or not Limit the total amount of throughput that can be provisioned on this account. This limit prevents unexpected charges related to provisioned throughput. You can update or remove this limit after your account is created. You can have up to one free tier Azure Cosmos DB account per Azure subscription and must opt in when creating the account. If you don't see the option to apply the free tier discount, another account in the subscription has already been enabled with free tier.

Note

The following options are not available if you select

**Serverless**as the**Capacity mode**:- Apply Free Tier Discount
- Limit total account throughput

In the

**Global Distribution**tab, configure the following details. You can leave the default values for this quickstart:Setting Value Description Geo-Redundancy Disable Enable or disable global distribution on your account by pairing your region with a pair region. You can add more regions to your account later. Multi-region Writes Disable Multi-region writes capability allows you to take advantage of the provisioned throughput for your databases and containers across the globe. Availability Zones Disable Availability Zones help you further improve availability and resiliency of your application. Note

The following options are not available if you select

**Serverless**as the**Capacity mode**in the previous**Basics**page:- Geo-redundancy
- Multi-region Writes

Optionally, you can configure more details in the following tabs:

**Networking**. Configure[access from a virtual network](/en-us/azure/cosmos-db/how-to-configure-vnet-service-endpoint).**Backup Policy**. Configure either[periodic](/en-us/azure/cosmos-db/periodic-backup-restore-introduction)or[continuous](/en-us/azure/cosmos-db/provision-account-continuous-backup)backup policy.**Encryption**. Use either service-managed key or a[customer-managed key](/en-us/azure/cosmos-db/how-to-setup-cmk#create-a-new-azure-cosmos-account).**Tags**. Tags are name/value pairs that enable you to categorize resources and view consolidated billing by applying the same tag to multiple resources and resource groups.

Select

**Review + create**.Review the account settings, and then select

**Create**. It takes a few minutes to create the account. Wait for the portal page to display**Your deployment is complete**.Select

**Go to resource**to go to the Azure Cosmos DB account page.

## Add an output binding

In the Azure portal, navigate to and select the function app you created previously.

Select

**Functions**, and then select the HttpTrigger function.Select

**Integration**and**+ Add output**.Use the

**Create Output**settings as specified in the table:Setting Suggested value Description **Binding Type**Azure Cosmos DB Name of the binding type to select to create the output binding to Azure Cosmos DB. **Document parameter name**taskDocument Name that refers to the Azure Cosmos DB object in code. **Database name**taskDatabase Name of database to save documents. **Collection name**taskCollection Name of the database collection. **If true, creates the Azure Cosmos DB database and collection**Yes The collection doesn't already exist, so create it. **Azure Cosmos DB account connection**New setting Select **New**, then choose**Azure Cosmos DB Account**and the**Database account**you created earlier, and then select**OK**. Creates an application setting for your account connection. This setting is used by the binding to connection to the database.Select

**OK**to create the binding.

## Update the function code

Replace the existing function code with the following code, in your chosen language:

Replace the existing C# function with the following code:

```
#r "Newtonsoft.Json"
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Logging;
public static IActionResult Run(HttpRequest req, out object taskDocument, ILogger log)
{
string name = req.Query["name"];
string task = req.Query["task"];
string duedate = req.Query["duedate"];
// We need both name and task parameters.
if (!string.IsNullOrEmpty(name) && !string.IsNullOrEmpty(task))
{
taskDocument = new
{
name,
duedate,
task
};
return (ActionResult)new OkResult();
}
else
{
taskDocument = null;
return (ActionResult)new BadRequestResult();
}
}
```


This code sample reads the HTTP Request query strings and assigns them to fields in the `taskDocument`

object. The `taskDocument`

binding sends the object data from this binding parameter to be stored in the bound document database. The database is created the first time the function runs.

## Test the function and database

Select

**Test/Run**. Under**Query**, select**+ Add parameter**and add the following parameters to the query string:`name`

`task`

`duedate`


Select

**Run**and verify that a 200 status is returned.In the Azure portal, search for and select

**Azure Cosmos DB**.Choose your Azure Cosmos DB account, then select

**Data Explorer**.Expand the

**TaskCollection**nodes, select the new document, and confirm that the document contains your query string values, along with some additional metadata.

You've successfully added a binding to your HTTP trigger to store unstructured data in an Azure Cosmos DB instance.

## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, you can delete them by deleting the resource group:

From the Azure portal menu or home page, select

**Resource groups**>**myResourceGroup**.On the

**myResourceGroup**pane, make sure that the listed resources are the ones you want to delete.Select

**Delete resource group**. Type**myResourceGroup**in the text box to confirm, and then select**Delete**.

## Next steps

For more information about binding to an Azure Cosmos DB instance, see [Azure Functions Azure Cosmos DB bindings](functions-bindings-cosmosdb).

[Azure Functions triggers and bindings concepts](functions-triggers-bindings)

Learn how Functions integrates with other services.[Azure Functions developer reference](functions-reference)

Provides more technical information about the Functions runtime and a reference for coding functions and defining triggers and bindings.[Code and test Azure Functions locally](functions-develop-local)

Describes the options for developing your functions locally.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-signalr-service-trigger -->

# SignalR Service trigger binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the *SignalR* trigger binding to respond to messages sent from Azure SignalR Service. When function is triggered, messages passed to the function is parsed as a json object.

In SignalR Service serverless mode, SignalR Service uses the [Upstream](../azure-signalr/concept-upstream) feature to send messages from client to Function App. And Function App uses SignalR Service trigger binding to handle these messages. The general architecture is shown below:


For information on setup and configuration details, see the [overview](functions-bindings-signalr-service).

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following sample shows a C# function that receives a message event from clients and logs the message content.

```
[Function(nameof(OnClientMessage))]
public static void OnClientMessage(
[SignalRTrigger("Hub", "messages", "sendMessage", "content", ConnectionStringSetting = "SignalRConnection")]
SignalRInvocationContext invocationContext, string content, FunctionContext functionContext)
{
var logger = functionContext.GetLogger(nameof(OnClientMessage));
logger.LogInformation("Connection {connectionId} sent a message. Message content: {content}", invocationContext.ConnectionId, content);
}
```


Important

Class based model of SignalR Service bindings in C# isolated worker doesn't optimize how you write SignalR triggers due to the limitation of C# worker model. For more information about class based model, see [Class based model](../azure-signalr/signalr-concept-serverless-development-config#class-based-model).

SignalR trigger isn't currently supported for Java.

Here's binding data in the *function.json* file:

```
{
"type": "signalRTrigger",
"name": "invocation",
"hubName": "hubName1",
"category": "messages",
"event": "SendMessage",
"parameterNames": [
"message"
],
"direction": "in"
}
```


```
app.generic("function1",
{
trigger: { "type": "signalRTrigger", "name": "invocation", "direction": "in", "hubName": "hubName1", "event": "SendMessage", "category": "messages" },
handler: (triggerInput, context) => {
context.log(`Receive ${triggerInput.Arguments[0]} from ${triggerInput.ConnectionId}.`)
}
})
```


Complete PowerShell examples are pending.

Here's the Python code:

```
import logging
import json
import azure.functions as func
def main(invocation) -> None:
invocation_json = json.loads(invocation)
logging.info("Receive {0} from {1}".format(invocation_json['Arguments'][0], invocation_json['ConnectionId']))
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the `SignalRTrigger`

attribute to define the function. C# script instead uses a [function.json configuration file](#configuration).

The following table explains the properties of the `SignalRTrigger`

attribute.

| Attribute property | Description |
|---|---|
HubName |
This value must be set to the name of the SignalR hub for the function to be triggered. |
Category |
This value must be set as the category of messages for the function to be triggered. The category can be one of the following values:
|
Event |
This value must be set as the event of messages for the function to be triggered. For messages category, event is the target in
connections category, only connected and disconnected is used. |
ParameterNames |
(Optional) A list of names that binds to the parameters. |
ConnectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |

## Annotations

There isn't currently a supported Java annotation for a SignalR trigger.

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `SignalRTrigger` . |
direction |
Must be set to `in` . |
name |
Variable name used in function code for trigger invocation context object. |
hubName |
This value must be set to the name of the SignalR hub for the function to be triggered. |
category |
This value must be set as the category of messages for the function to be triggered. The category can be one of the following values:
|
event |
This value must be set as the event of messages for the function to be triggered. For messages category, event is the target in
connections category, only connected and disconnected is used. |
parameterNames |
(Optional) A list of names that binds to the parameters. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |

See the [Example section](#example) for complete examples.

## Usage

### Managed identity-based connections

For optimal security, your function app should use managed identities when connecting to the Azure SignalR service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize requests to Azure SignalR Service resources with Microsoft Entra managed identities](../azure-signalr/signalr-howto-authorize-managed-identity#azure-signalr-service-bindings-in-azure-functions).

### Payloads

The trigger input type is declared as either `InvocationContext`

or a custom type. If you choose `InvocationContext`

, you get full access to the request content. For a custom type, the runtime tries to parse the JSON request body to set the object properties.

### InvocationContext

`InvocationContext`

contains all the content in the message sent from a SignalR service, which includes the following properties:

| Property | Description |
|---|---|
| Arguments | Available for messages category. Contains arguments in
|
| Error | Available for disconnected event. It can be Empty if the connection closed with no error, or it contains the error messages. |
| Hub | The hub name that the message belongs to. |
| Category | The category of the message. |
| Event | The event of the message. |
| ConnectionId | The connection ID of the client that sends the message. |
| UserId | The user identity of the client that sends the message. |
| Headers | The headers of the request. |
| Query | The query of the request when clients connect to the service. |
| Claims | The claims of the client. |

### Using `ParameterNames`


The property `ParameterNames`

in `SignalRTrigger`

lets you bind arguments of invocation messages to the parameters of functions. You can use the name you defined as part of [binding expressions](functions-bindings-expressions-patterns) in other binding or as parameters in your code. That gives you a more convenient way to access arguments of `InvocationContext`

.

Say you have a JavaScript SignalR client trying to invoke method `broadcast`

in Azure Function with two arguments `message1`

, `message2`

.

```
await connection.invoke("broadcast", message1, message2);
```


After you set `parameterNames`

, the names you defined correspond to the arguments sent on the client side.

```
[SignalRTrigger(parameterNames: new string[] {"arg1, arg2"})]
```


Then, the `arg1`

contains the content of `message1`

, and `arg2`

contains the content of `message2`

.

`ParameterNames`

considerations

For the parameter binding, the order matters. If you're using `ParameterNames`

, the order in `ParameterNames`

matches the order of the arguments you invoke in the client. If you're using attribute `[SignalRParameter]`

in C#, the order of arguments in Azure Function methods matches the order of arguments in clients.

`ParameterNames`

and attribute `[SignalRParameter]`

**cannot** be used at the same time, or you'll get an exception.

### SignalR Service integration

SignalR Service needs a URL to access Function App when you're using SignalR Service trigger binding. The URL should be configured in **Upstream Settings** on the SignalR Service side.


When using SignalR Service trigger, the URL can be simple and formatted as follows:

```
<Function_App_URL>/runtime/webhooks/signalr?code=<API_KEY>
```


The `Function_App_URL`

can be found on Function App's Overview page and the `API_KEY`

is generated by Azure Function. You can get the `API_KEY`

from `signalr_extension`

in the **App keys** blade of Function App.

If you want to use more than one Function App together with one SignalR Service, upstream can also support complex routing rules. Find more details at [Upstream settings](../azure-signalr/concept-upstream).

### Step-by-step sample

You can follow the sample in GitHub to deploy a chat room on Function App with SignalR Service trigger binding and upstream feature: [Bidirectional chat room sample](https://github.com/aspnet/AzureSignalR-samples/tree/master/samples/BidirectionChat)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-custom-handlers -->

# Azure Functions custom handlers

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions executes your app code by using language-specific handlers. These language-specific handlers allow Functions to support [most key languages](supported-languages) by default. However, you might need to run code in another language or package.

Custom handlers are lightweight web servers that receive events from the Azure Functions host process. You can use custom handlers to deploy to Azure Functions any code project that supports HTTP primitives.

Custom handlers are best suited for situations where you want to:

- Implement a function app in a language that's not currently offered out-of-the-box, such as Go or Rust.
- Implement a function app in a runtime that's not currently featured by default, such as Deno.
[Deploy a server](#deploy-self-hosted-mcp-servers)built with the standard MCP SDKs to Azure Functions.

With custom handlers, you can use [triggers and input and output bindings](functions-triggers-bindings) via [extension bundles](functions-bindings-register).

Get started with Azure Functions custom handlers with [quickstarts in Go and Rust](create-first-function-vs-code-other).

## Overview

The following diagram shows the relationship between the Functions host and a web server implemented as a custom handler.

- Each event triggers a request sent to the Functions host. An event is any trigger that Azure Functions supports.
- The Functions host then issues a
[request payload](#request-payload)to the web server. The payload holds trigger and input binding data and other metadata for the function. - The web server executes the individual function, and returns a
[response payload](#response-payload)to the Functions host. - The Functions host passes data from the response to the function's output bindings for processing.

An Azure Functions app implemented as a custom handler must configure the *host.json*, *local.settings.json*, and *function.json* files according to a few conventions.

## Deploy self-hosted MCP servers

Custom handlers also enables you to host MCP servers that you build by using official MCP SDKs in Azure Functions. Custom handlers provides a simple and streamlined experience for hosting your MCP servers in Azure. For more information, see [Self-hosted remote MCP server on Azure Functions](self-hosted-mcp-servers).

Note

The ability to have Azure Functions host MCP servers you create using official MCP SDKs is currently in preview.

## Application structure

To implement a custom handler, your application needs the following aspects:

- A
*host.json*file at the root of your app - A
*local.settings.json*file at the root of your app - A
*function.json*file for each function (inside a folder that matches the function name) - A command, script, or executable that runs a web server

The following diagram shows how these files look on the file system for a function named "MyQueueFunction" and a custom handler executable named *handler.exe*.

```
| /MyQueueFunction
| function.json
|
| host.json
| local.settings.json
| handler.exe
```


### Configuration

You configure the application through the *host.json* and *local.settings.json* files.

#### host.json

*host.json* directs the Functions host where to send requests by pointing to a web server that can process HTTP events.

Define a custom handler by configuring the *host.json* file with details on how to run the web server through the `customHandler`

section.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
}
}
}
```


The `customHandler`

section points to a target as defined by the `defaultExecutablePath`

. The execution target can be a command, executable, or file where the web server is implemented.

Use the `arguments`

array to pass any arguments to the executable. Arguments support expansion of environment variables (application settings) by using `%%`

notation.

You can also change the working directory used by the executable with `workingDirectory`

.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "app/handler.exe",
"arguments": [
"--database-connection-string",
"%DATABASE_CONNECTION_STRING%"
],
"workingDirectory": "app"
}
}
}
```


##### Bindings support

Standard triggers along with input and output bindings are available by referencing [extension bundles](functions-bindings-register) in your *host.json* file.

#### local.settings.json

*local.settings.json* defines application settings used when running the function app locally. Because it might contain secrets, exclude *local.settings.json* from source control. In Azure, use application settings instead.

For custom handlers, set `FUNCTIONS_WORKER_RUNTIME`

to `Custom`

in *local.settings.json*.

```
{
"IsEncrypted": false,
"Values": {
"FUNCTIONS_WORKER_RUNTIME": "Custom"
}
}
```


### Function metadata

When you use a custom handler, the *function.json* contents are the same as when you define a function in any other context. The only requirement is that you must place *function.json* files in a folder named to match the function name.

The following *function.json* configures a function that has a queue trigger and a queue output binding. Because it's in a folder named *MyQueueFunction*, it defines a function named *MyQueueFunction*.

**MyQueueFunction/function.json**

```
{
"bindings": [
{
"name": "myQueueItem",
"type": "queueTrigger",
"direction": "in",
"queueName": "messages-incoming",
"connection": "AzureWebJobsStorage"
},
{
"name": "$return",
"type": "queue",
"direction": "out",
"queueName": "messages-outgoing",
"connection": "AzureWebJobsStorage"
}
]
}
```


### Request payload

When the Functions host receives a queue message, it sends an HTTP post request to the custom handler with a payload in the body.

The following code shows a sample request payload. The payload includes a JSON structure with two members: `Data`

and `Metadata`

.

The `Data`

member includes keys that match input and trigger names as defined in the bindings array in the *function.json* file.

The `Metadata`

member includes [metadata generated from the event source](functions-bindings-expressions-patterns#trigger-metadata).

```
{
"Data": {
"myQueueItem": "{ message: \"Message sent\" }"
},
"Metadata": {
"DequeueCount": 1,
"ExpirationTime": "2019-10-16T17:58:31+00:00",
"Id": "800ae4b3-bdd2-4c08-badd-f08e5a34b865",
"InsertionTime": "2019-10-09T17:58:31+00:00",
"NextVisibleTime": "2019-10-09T18:08:32+00:00",
"PopReceipt": "AgAAAAMAAAAAAAAAAgtnj8x+1QE=",
"sys": {
"MethodName": "QueueTrigger",
"UtcNow": "2019-10-09T17:58:32.2205399Z",
"RandGuid": "24ad4c06-24ad-4e5b-8294-3da9714877e9"
}
}
}
```


### Response payload

By convention, function responses are formatted as key/value pairs. Supported keys include:

| Data type | Remarks | |
|---|---|---|
`Outputs` |
object | Holds response values as defined by the `bindings` array in function.json.For instance, if a function is configured with a queue output binding named "myQueueOutput", then `Outputs` contains a key named `myQueueOutput` , which the custom handler sets to the messages that it sends to the queue. |
`Logs` |
array | Messages that appear in the Functions invocation logs. When running in Azure, messages appear in Application Insights. |
`ReturnValue` |
string | Used to provide a response when an output is configured as `$return` in the function.json file. |

This table shows an example of a response payload.

```
{
"Outputs": {
"res": {
"body": "Message enqueued"
},
"myQueueOutput": [
"queue message 1",
"queue message 2"
]
},
"Logs": [
"Log message 1",
"Log message 2"
],
"ReturnValue": "{\"hello\":\"world\"}"
}
```


## Examples

You can implement custom handlers in any language that supports receiving HTTP events. The following examples show how to implement a custom handler by using the Go programming language.

### Function with bindings

This example shows a function named `order`

that accepts a `POST`

request with a payload representing a product order. When you post an order to the function, it creates a Queue Storage message and returns an HTTP response.

#### Implementation

In a folder named *order*, the *function.json* file configures the HTTP-triggered function.

**order/function.json**

```
{
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": ["post"]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"type": "queue",
"name": "message",
"direction": "out",
"queueName": "orders",
"connection": "AzureWebJobsStorage"
}
]
}
```


This function is defined as an [HTTP triggered function](functions-bindings-http-webhook-trigger) that returns an [HTTP response](functions-bindings-http-webhook-output) and outputs a [Queue storage](functions-bindings-storage-queue-output) message.

At the root of the app, the *host.json* file is configured to run an executable file named `handler.exe`

(`handler`

in Linux or macOS).

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


This is the HTTP request sent to the Functions runtime.

```
POST http://127.0.0.1:7071/api/order HTTP/1.1
Content-Type: application/json
{
"id": 1005,
"quantity": 2,
"color": "black"
}
```


The Functions runtime sends the following HTTP request to the custom handler:

```
POST http://127.0.0.1:<FUNCTIONS_CUSTOMHANDLER_PORT>/order HTTP/1.1
Content-Type: application/json
{
"Data": {
"req": {
"Url": "http://localhost:7071/api/order",
"Method": "POST",
"Query": "{}",
"Headers": {
"Content-Type": [
"application/json"
]
},
"Params": {},
"Body": "{\"id\":1005,\"quantity\":2,\"color\":\"black\"}"
}
},
"Metadata": {
}
}
```


Note

Some portions of the payload were removed for brevity.

*handler.exe* is the compiled Go custom handler program that runs a web server and responds to function invocation requests from the Functions host.

```
package main
import (
"encoding/json"
"fmt"
"log"
"net/http"
"os"
)
type InvokeRequest struct {
Data map[string]json.RawMessage
Metadata map[string]interface{}
}
type InvokeResponse struct {
Outputs map[string]interface{}
Logs []string
ReturnValue interface{}
}
func orderHandler(w http.ResponseWriter, r *http.Request) {
var invokeRequest InvokeRequest
d := json.NewDecoder(r.Body)
d.Decode(&invokeRequest)
var reqData map[string]interface{}
json.Unmarshal(invokeRequest.Data["req"], &reqData)
outputs := make(map[string]interface{})
outputs["message"] = reqData["Body"]
resData := make(map[string]interface{})
resData["body"] = "Order enqueued"
outputs["res"] = resData
invokeResponse := InvokeResponse{outputs, nil, nil}
responseJson, _ := json.Marshal(invokeResponse)
w.Header().Set("Content-Type", "application/json")
w.Write(responseJson)
}
func main() {
customHandlerPort, exists := os.LookupEnv("FUNCTIONS_CUSTOMHANDLER_PORT")
if !exists {
customHandlerPort = "8080"
}
mux := http.NewServeMux()
mux.HandleFunc("/order", orderHandler)
fmt.Println("Go server Listening on: ", customHandlerPort)
log.Fatal(http.ListenAndServe(":"+customHandlerPort, mux))
}
```


In this example, the custom handler runs a web server to handle HTTP events and listens for requests via the `FUNCTIONS_CUSTOMHANDLER_PORT`

.

Even though the Functions host receives the original HTTP request at `/api/order`

, it invokes the custom handler by using the function name (its folder name). In this example, the function is defined at the path of `/order`

. The host sends the custom handler an HTTP request at the path of `/order`

.

When you send `POST`

requests to this function, the trigger data and function metadata are available via the HTTP request body. You can access the original HTTP request body in the payload's `Data.req.Body`

.

The function's response is formatted into key/value pairs where the `Outputs`

member holds a JSON value where the keys match the outputs as defined in the *function.json* file.

This is an example payload that this handler returns to the Functions host.

```
{
"Outputs": {
"message": "{\"id\":1005,\"quantity\":2,\"color\":\"black\"}",
"res": {
"body": "Order enqueued"
}
},
"Logs": null,
"ReturnValue": null
}
```


By setting the `message`

output equal to the order data that came in from the request, the function outputs that order data to the configured queue. The Functions host also returns the HTTP response configured in `res`

to the caller.

### HTTP-only function

For HTTP-triggered functions with no additional bindings or outputs, you might want your handler to work directly with the HTTP request and response instead of the custom handler [request](#request-payload) and [response](#response-payload) payloads. You can configure this behavior in *host.json* by using the `enableProxyingHttpRequest`

setting, which supports response streaming.

Important

The primary purpose of the custom handlers feature is to enable languages and runtimes that don't currently have first-class support on Azure Functions. While you might be able to run web applications by using custom handlers, Azure Functions isn't a standard reverse proxy. Some components of the HTTP request, such as certain headers and routes, might be restricted. Your application might also experience excessive [cold start](event-driven-scaling#cold-start).

To address these circumstances, consider running your web apps on [Azure App Service](../app-service/overview).

The following example demonstrates how to configure an HTTP-triggered function with no additional bindings or outputs. The scenario implemented in this example features a function named `hello`

that accepts a `GET`

or `POST`

.

#### Implementation

In a folder named *hello*, the *function.json* file configures the HTTP-triggered function.

**hello/function.json**

```
{
"bindings": [
{
"type": "httpTrigger",
"authLevel": "function",
"direction": "in",
"name": "req",
"methods": ["get", "post"]
},
{
"type": "http",
"direction": "out",
"name": "res"
}
]
}
```


The function is configured to accept both `GET`

and `POST`

requests, and the result value is provided through an argument named `res`

.

At the root of the app, the *host.json* file is configured to run `handler.exe`

and `enableProxyingHttpRequest`

is set to `true`

.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
},
"enableProxyingHttpRequest": true
}
}
```


The following is a POST request to the Functions host. The Functions host then sends the request to the custom handler.

```
POST http://127.0.0.1:7071/api/hello HTTP/1.1
Content-Type: application/json
{
"message": "Hello World!"
}
```


The *handler.go* file implements a web server and HTTP function.

```
package main
import (
"fmt"
"io/ioutil"
"log"
"net/http"
"os"
)
func helloHandler(w http.ResponseWriter, r *http.Request) {
w.Header().Set("Content-Type", "application/json")
if r.Method == "GET" {
w.Write([]byte("hello world"))
} else {
body, _ := ioutil.ReadAll(r.Body)
w.Write(body)
}
}
func main() {
customHandlerPort, exists := os.LookupEnv("FUNCTIONS_CUSTOMHANDLER_PORT")
if !exists {
customHandlerPort = "8080"
}
mux := http.NewServeMux()
mux.HandleFunc("/api/hello", helloHandler)
fmt.Println("Go server Listening on: ", customHandlerPort)
log.Fatal(http.ListenAndServe(":"+customHandlerPort, mux))
}
```


In this example, the custom handler creates a web server to handle HTTP events and listens for requests via the `FUNCTIONS_CUSTOMHANDLER_PORT`

.

`GET`

requests are handled by returning a string, and `POST`

requests have access to the request body.

The route for the order function here is `/api/hello`

, same as the original request.

Note

The `FUNCTIONS_CUSTOMHANDLER_PORT`

isn't the public facing port used to call the function. The Functions host uses this port to call the custom handler.

## Deploying

You can deploy a custom handler to every Azure Functions hosting option. If your handler requires operating system or platform dependencies (such as a language runtime), you might need to use a [custom container](functions-how-to-custom-container).

When you create a function app in Azure for custom handlers, select .NET Core as the stack.

To deploy a custom handler app by using Azure Functions Core Tools, run the following command.

```
func azure functionapp publish $functionAppName
```


Note

Ensure all files required to run your custom handler are in the folder and included in the deployment. If your custom handler is a binary executable or has platform-specific dependencies, ensure these files match the target deployment platform.

## Restrictions

- The custom handler web server needs to start within 60 seconds.

## Samples

For examples of how to implement functions in a variety of different languages, see the [custom handler samples GitHub repo](https://github.com/Azure-Samples/functions-custom-handlers).

## Troubleshooting and support

### Trace logging

If your custom handler process fails to start or if it has problems communicating with the Functions host, increase the function app's log level to `Trace`

to see more diagnostic messages from the host.

To change the function app's default log level, configure the `logLevel`

setting in the `logging`

section of *host.json*.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
}
},
"logging": {
"logLevel": {
"default": "Trace"
}
}
}
```


The Functions host outputs extra log messages, including information related to the custom handler process. Use the logs to investigate problems starting your custom handler process or invoking functions in your custom handler.

Locally, logs are printed to the console.

In Azure, [query Application Insights traces](analyze-telemetry-data#query-telemetry-data) to view the log messages. If your app produces a high volume of logs, only a subset of log messages are sent to Application Insights. [Disable sampling](configure-monitoring#configure-sampling) to ensure all messages are logged.

### Test custom handler in isolation

Custom handler apps are web server processes, so it might be helpful to start them on their own and test function invocations by sending mock [HTTP requests](#request-payload). For sending HTTP requests with payloads, make sure to choose a tool that keeps your data secure. For more information, see [HTTP test tools](functions-develop-local#http-test-tools).

You can also use this strategy in your CI/CD pipelines to run automated tests on your custom handler.

### Execution environment

Custom handlers run in the same environment as a typical Azure Functions app. Test your handler to ensure the environment contains all the dependencies it needs to run. For apps that require additional dependencies, you might need to run them by using a [custom container image](functions-how-to-custom-container) hosted on Azure Functions [Premium plan](functions-premium-plan).

### Get support

If you need help on a function app with custom handlers, you can submit a request through regular support channels. However, due to the wide variety of possible languages used to build custom handlers apps, support isn't unlimited.

Support is available if the Functions host has problems starting or communicating with the custom handler process. For problems specific to the inner workings of your custom handler process, such as issues with the chosen language or framework, our Support Team can't provide assistance in this context.

## Next steps

Get started building an Azure Functions app in Go or Rust with the [custom handlers quickstart](create-first-function-vs-code-other).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-vnet -->

# Tutorial: Integrate Azure Functions with an Azure virtual network by using private endpoints

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This tutorial shows you how to use Azure Functions to connect to resources in an Azure virtual network by using private endpoints. You create a new function app using a new storage account that's locked behind a virtual network by using the Azure portal. The virtual network uses a Service Bus queue trigger.

In this tutorial, you'll:

- Create a function app in the Elastic Premium plan with virtual network integration and private endpoints.
- Create Azure resources, such as the Service Bus
- Lock down your Service Bus behind a private endpoint.
- Deploy a function app that uses both the Service Bus and HTTP triggers.
- Test to see that your function app is secure inside the virtual network.
- Clean up resources.

## Create a function app in a Premium plan

You create a C# function app in an [Elastic Premium plan](functions-premium-plan), which supports networking capabilities such as virtual network integration on create along with serverless scale. This tutorial uses C# and Windows. Other languages and Linux are also supported.

On the Azure portal menu or the

**Home**page, select**Create a resource**.On the

**New**page, select**Compute**>**Function App**.On the

**Basics**page, use the following table to configure the function app settings.Setting Suggested value Description **Subscription**Your subscription Subscription under which this new function app is created. [Resource Group](../azure-resource-manager/management/overview)myResourceGroup Name for the new resource group where you create your function app. **Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

.**Publish**Code Choose to publish code files or a Docker container. **Runtime stack**.NET This tutorial uses .NET. **Version**6 (LTS) This tutorial uses .NET 6.0 running [in the same process as the Functions host](functions-dotnet-class-library).**Region**Preferred region Choose a [region](https://azure.microsoft.com/regions/)near you or near other services that your functions access.**Operating system**Windows This tutorial uses Windows but also works for Linux. [Plan](functions-scale)Functions Premium Hosting plan that defines how resources are allocated to your function app. By default, when you select **Premium**, a new App Service plan is created. The default**Sku and size**is**EP1**, where*EP*stands for*elastic premium*. For more information, see the list of[Premium SKUs](functions-premium-plan#available-instance-skus).

When you run JavaScript functions on a Premium plan, choose an instance that has fewer vCPUs. For more information, see[Choose single-core Premium plans](functions-reference-node#considerations-for-javascript-functions).Select

**Next: Storage**. On the**Storage**page, enter the following settings.Setting Suggested value Description [Storage account](../storage/common/storage-account-create)Globally unique name Create a storage account used by your function app. Storage account names must be between 3 and 24 characters long. They might contain numbers and lowercase letters only. You can also use an existing account that isn't restricted by firewall rules and meets the [storage account requirements](storage-considerations#storage-account-requirements). When you use Functions with a locked down storage account, you need a v2 storage account. This version is the default storage version created when creating a function app with networking capabilities through the Azure portal.Select

**Next: Networking**. On the**Networking**page, enter the following settings.Note

Some of these settings aren't visible until other options are selected.

Setting Suggested value Description **Enable public access**Off Deny public network access blocks all incoming traffic except that comes from private endpoints. **Enable network injection**On The ability to configure your application with virtual network integration at creation appears in the portal window after this option is switched to **On**.**Virtual Network**Create New Select the **Create New**field. In the pop-out screen, provide a name for your virtual network and select**Ok**. Options to restrict inbound and outbound access to your function app on create are displayed. You must explicitly enable virtual network integration in the**Outbound access**portion of the window to restrict outbound access.Enter the following settings for the

**Inbound access**section. This step creates a private endpoint on your function app.Tip

To continue interacting with your function app from the Azure portal, you need to add your local computer to the virtual network. If you don't wish to restrict inbound access, skip this step.

Setting Suggested value Description **Enable private endpoints**On The ability to configure your application with virtual network integration at creation appears in the portal after this option is enabled. **Private endpoint name**myInboundPrivateEndpointName Name that identifies your new function app private endpoint. **Inbound subnet**Create New This option creates a new subnet for your inbound private endpoint. Multiple private endpoints might be added to a singular subnet. Provide a **Subnet Name**. The**Subnet Address Block**might be left at the default value. Select**Ok**. To learn more about subnet sizing, see[Subnets](functions-networking-options#subnets).**DNS**Azure Private DNS Zone This value indicates which DNS server your private endpoint uses. In most cases if you're working within Azure, Azure Private DNS Zone is the DNS zone you should use as using **Manual**for custom DNS zones have increased complexity.Enter the following settings for the

**Outbound access**section. This step integrates your function app with a virtual network on creation. It also exposes options to create private endpoints on your storage account and restrict your storage account from network access on create. When function app is virtual network integrated, all outbound traffic by default goes[through the virtual network](../app-service/overview-vnet-integration#how-regional-virtual-network-integration-works).Setting Suggested value Description **Enable VNet Integration**On This setting integrates your function app with a virtual network on create and direct all outbound traffic through the virtual network. **Outbound subnet**Create new This setting creates a new subnet for your function app's virtual network integration. A function app can only be virtual network integrated with an empty subnet. Provide a **Subnet Name**. The**Subnet Address Block**might be left at the default value. Select**Ok**. The option to create**Storage private endpoints**is displayed. To use your function app with virtual networks, you need to join it to a subnet.Enter the following settings for the

**Storage private endpoint**section. This step creates private endpoints for the blob, queue, file, and table endpoints on your storage account on create. This approach effectively integrates your storage account with the virtual network.Setting Suggested value Description **Add storage private endpoint**On The ability to configure your application with virtual network integration at creation is displayed in the portal after this option is enabled. **Private endpoint name**myInboundPrivateEndpointName Name that identifies your storage account private endpoint. **Private endpoint subnet**Create New This setting creates a new subnet for your inbound private endpoint on the storage account. Multiple private endpoints might be added to a singular subnet. Provide a **Subnet Name**. The**Subnet Address Block**might be left at the default value. Select**Ok**.**DNS**Azure Private DNS Zone This value indicates which DNS server your private endpoint uses. In most cases if you're working within Azure, Azure Private DNS Zone is the DNS zone you should use as using **Manual**for custom DNS zones will have increased complexity.Select

**Next: Monitoring**. On the**Monitoring**page, enter the following settings.Setting Suggested value Description [Application Insights](functions-monitoring)Default Create an Application Insights resource of the same app name in the nearest supported region. Expand this setting if you need to change the **New resource name**or store your data in a different**Location**in an[Azure geography](https://azure.microsoft.com/global-infrastructure/geographies/).Select

**Review + create**to review the app configuration selections.On the

**Review + create**page, review your settings. Then select**Create**to create and deploy the function app.In the upper-right corner of the portal, select the

**Notifications**icon and watch for the**Deployment succeeded**message.Select

**Go to resource**to view your new function app. You can also select**Pin to dashboard**. Pinning makes it easier to return to this function app resource from your dashboard.

Congratulations! You successfully created your premium function app.

Note

Some deployments might occasionally fail to create the private endpoints in the storage account with the error `StorageAccountOperationInProgress`

. This failure occurs even though the function app itself gets created successfully. When you encounter such an error, delete the function app and retry the operation. You can instead create the private endpoints on the storage account manually.

### Create a Service Bus

Next, you create a Service Bus instance that is used to test the functionality of your function app's network capabilities in this tutorial.

On the Azure portal menu or the

**Home**page, select**Create a resource**.On the

**New**page, search for*Service Bus*. Then select**Create**.On the

**Basics**tab, use the following table to configure the Service Bus settings. All other settings can use the default values.Setting Suggested value Description **Subscription**Your subscription The subscription in which your resources are created. [Resource group](../azure-resource-manager/management/overview)myResourceGroup The resource group you created with your function app. **Namespace name**myServiceBus The name of the Service Bus instance for which the private endpoint is enabled. [Location](https://azure.microsoft.com/regions/)myFunctionRegion The region where you created your function app. **Pricing tier**Premium Choose this tier to use private endpoints with Azure Service Bus. Select

**Review + create**. After validation finishes, select**Create**.

## Lock down your Service Bus

Create the private endpoint to lock down your Service Bus:

In your new Service Bus, in the menu on the left, select

**Networking**.On the

**Private endpoint connections**tab, select**Private endpoint**.On the

**Basics**tab, use the private endpoint settings shown in the following table.Setting Suggested value Description **Subscription**Your subscription The subscription in which your resources are created. [Resource group](../azure-resource-manager/management/overview)myResourceGroup The resource group you created with your function app. **Name**sb-endpoint The name of the private endpoint for the service bus. [Region](https://azure.microsoft.com/regions/)myFunctionRegion The region where you created your storage account. On the

**Resource**tab, use the private endpoint settings shown in the following table.Setting Suggested value Description **Subscription**Your subscription The subscription under which your resources are created. **Resource type**Microsoft.ServiceBus/namespaces The resource type for the Service Bus. **Resource**myServiceBus The Service Bus you created earlier in the tutorial. **Target subresource**namespace The private endpoint that is used for the namespace from the Service Bus. On the

**Virtual Network**tab, for the**Subnet**setting, choose**default**.Select

**Review + create**. After validation finishes, select**Create**.After the private endpoint is created, return to the

**Networking**section of your Service Bus namespace and check the**Public Access**tab.Ensure

**Selected networks**is selected.Select

**+ Add existing virtual network**to add the recently created virtual network.On the

**Add networks**tab, use the network settings from the following table:Setting Suggested value Description **Subscription**Your subscription The subscription under which your resources are created. **Virtual networks**myVirtualNet The name of the virtual network to which your function app connects. **Subnets**functions The name of the subnet to which your function app connects. Select

**Add your client IP address**to give your current client IP access to the namespace.Note

Allowing your client IP address is necessary to enable the Azure portal to

[publish messages to the queue later in this tutorial](#test-your-locked-down-function-app).Select

**Enable**to enable the service endpoint.Select

**Add**to add the selected virtual network and subnet to the firewall rules for the Service Bus.Select

**Save**to save the updated firewall rules.

Resources in the virtual network can now communicate with the Service Bus using the private endpoint.

## Create a queue

Create the queue where your Azure Functions Service Bus trigger gets events:

In your Service Bus, in the menu on the left, select

**Queues**.Select

**Queue**. For the purposes of this tutorial, provide the name*queue*as the name of the new queue.Select

**Create**.

Important

This tutorial currently shows you how to connect to Service Bus using a connection string, which requires you to handle a share secret. For improved security, you should instead use managed identities when connecting to Service Bus from your app. For more information, see [Identity-based connections](functions-bindings-service-bus-trigger?tabs=extensionv5#identity-based-connections) in the Service Bus binding reference article.

## Get a Service Bus connection string

In your Service Bus, in the menu on the left, select

**Shared access policies**.Select

**RootManageSharedAccessKey**. Copy and save the**Primary Connection String**. You need this connection string when you configure the app settings.

## Configure your function app settings

In your function app, in the menu on the left, select

**Configuration**.To use your function app with virtual networks and service bus, update the app settings shown in the following table. To add or edit a setting, select

**+ New application setting**or the**Edit**icon in the rightmost column of the app settings table. When you finish, select**Save**.Setting Suggested value Description **SERVICEBUS_CONNECTION**myServiceBusConnectionString Create this app setting for the connection string of your Service Bus. This storage connection string is from the [Get a Service Bus connection string](#get-a-service-bus-connection-string)section.**WEBSITE_CONTENTOVERVNET**1 Create this app setting. A value of 1 enables your function app to scale when your storage account is restricted to a virtual network. Since you're using an Elastic Premium hosting plan, In the

**Configuration**view, select the**Function runtime settings**tab. Set**Runtime Scale Monitoring**to**On**. Then select**Save**. Runtime-driven scaling allows you to connect non-HTTP trigger functions to services that run inside your virtual network.

Note

Runtime scaling isn't needed for function apps hosted in a Dedicated App Service plan.

## Deploy a Service Bus trigger and HTTP trigger

Note

Enabling private endpoints on a function app also makes the Source Control Manager (SCM) site publicly inaccessible. The following instructions give deployment directions using the Deployment Center within the function app. Alternatively, use [zip deploy](functions-deployment-technologies#zip-deploy) or [self-hosted](/en-us/azure/devops/pipelines/agents/docker) agents that are deployed into a subnet on the virtual network.

In GitHub, go to the following sample repository. It contains a function app and two functions, an HTTP trigger, and a Service Bus queue trigger.

At the top of the page, select

**Fork**to create a fork of this repository in your own GitHub account or organization.In your function app, in the menu on the left, select

**Deployment Center**. Then select**Settings**.On the

**Settings**tab, use the deployment settings shown in the following table.Setting Suggested value Description **Source**GitHub You should have created a GitHub repository for the sample code in step 2. **Organization**myOrganization The organization your repo is checked into. It's usually your account. **Repository**functions-vnet-tutorial The repository forked from [https://github.com/Azure-Samples/functions-vnet-tutorial](https://github.com/Azure-Samples/functions-vnet-tutorial).**Branch**main The main branch of the repository you created. **Runtime stack**.NET The sample code is in C#. **Version**.NET Core 3.1 The runtime version. Select

**Save**.Your initial deployment might take a few minutes. When your app is successfully deployed, on the

**Logs**tab, you see a**Success (Active)**status message. If necessary, refresh the page.

Congratulations! You successfully deployed your sample function app.

### Test your locked-down function app

In your function app, in the menu on the left, select

**Functions**.Select

**ServiceBusQueueTrigger**.In the menu on the left, select

**Monitor**.

You see that you can't monitor your app. Your browser doesn't have access to the virtual network, so it can't directly access resources within the virtual network.

Here's an alternative way to monitor your function by using Application Insights:

In your function app, in the menu on the left, select

**Application Insights**. Then select**View Application Insights data**.In the menu on the left, select

**Live metrics**.Open a new tab. In your Service Bus, in the menu on the left, select

**Queues**.Select your queue.

In the menu on the left, select

**Service Bus Explorer**. Under**Send**, for**Content Type**, choose**Text/Plain**. Then enter a message.Select

**Send**to send the message.On the

**Live metrics**tab, you should see that your Service Bus queue trigger fired. If it hasn't, resend the message from**Service Bus Explorer**.

Congratulations! You successfully tested your function app setup with private endpoints.

## Understand private DNS zones

You used a private endpoint to connect to Azure resources. You're connecting to a private IP address instead of the public endpoint. Existing Azure services are configured to use an existing DNS to connect to the public endpoint. You must override the DNS configuration to connect to the private endpoint.

A private DNS zone is created for each Azure resource that was configured with a private endpoint. A DNS record is created for each private IP address associated with the private endpoint.

The following DNS zones were created in this tutorial:

- privatelink.file.core.windows.net
- privatelink.blob.core.windows.net
- privatelink.servicebus.windows.net
- privatelink.azurewebsites.net

## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, you can delete them by deleting the resource group:

From the Azure portal menu or home page, select

**Resource groups**>**myResourceGroup**.On the

**myResourceGroup**pane, make sure that the listed resources are the ones you want to delete.Select

**Delete resource group**. Type**myResourceGroup**in the text box to confirm, and then select**Delete**.

## Next steps

In this tutorial, you created a Premium function app, storage account, and Service Bus. You secured all of these resources behind private endpoints.

Use the following links to learn more Azure Functions networking options and private endpoints:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-output -->

# Azure Cache for Redis output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Cache for Redis output bindings lets you change the keys in a cache based on a set of available trigger on the cache.

For information on setup and configuration details, see the [overview](functions-bindings-cache).

## Scope of availability for functions bindings

| Binding Type | Azure Managed Redis | Azure Cache for Redis |
|---|---|---|
| Output | Yes | Yes |

Important

When using Azure Managed Redis or the Enterprise tiers of Azure Cache for Redis, use port 10000 rather than port 6380 or 6379.

Important

The Node.js v4 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Important

The Python v2 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v2 model works, refer to the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

## Example

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

The following example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

Important

For .NET functions, using the *isolated worker* model is recommended over the *in-process* model. For a comparison of the *in-process* and *isolated worker* models, see differences between the *isolated worker* model and the *in-process* model for .NET on Azure Functions.

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisOutputBinding
{
internal class SetDeleter
{
[Function(nameof(SetDeleter))]
[RedisOutput(Common.connectionString, "DEL")]
public static string Run(
[RedisPubSubTrigger(Common.connectionString, "__keyevent@0__:set")] string key,
ILogger logger)
{
logger.LogInformation($"Deleting recently SET key '{key}'");
return key;
}
}
}
```


```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.WebJobs.Extensions.Redis.Samples.RedisOutputBinding
{
internal class SetDeleter
{
[FunctionName(nameof(SetDeleter))]
public static void Run(
[RedisPubSubTrigger(Common.connectionStringSetting, "__keyevent@0__:set")] string key,
[Redis(Common.connectionStringSetting, "DEL")] out string[] arguments,
ILogger logger)
{
logger.LogInformation($"Deleting recently SET key '{key}'");
arguments = new string[] { key };
}
}
}
```


The following example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

```
package com.function.RedisOutputBinding;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class SetDeleter {
@FunctionName("SetDeleter")
@RedisOutput(
name = "value",
connection = "redisConnectionString",
command = "DEL")
public String run(
@RedisPubSubTrigger(
name = "key",
connection = "redisConnectionString",
channel = "__keyevent@0__:set")
String key,
final ExecutionContext context) {
context.getLogger().info("Deleting recently SET key '" + key + "'");
return key;
}
}
```


This example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

The bindings are defined in the `function.json`` file:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisConnectionString",
"command": "DEL",
"name": "$return",
"direction": "out"
}
],
"scriptFile": "index.js"
}
```


This code from the `index.js`

file takes the key from the trigger and returns it to the output binding to delete the cached item.

```
module.exports = async function (context, key) {
context.log("Deleting recently SET key '" + key + "'");
return key;
}
```


This example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

The bindings are defined in this `function.json`

file:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisLocalhost",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisLocalhost",
"command": "DEL",
"name": "retVal",
"direction": "out"
}
],
"scriptFile": "run.ps1"
}
```


This code from the `run.ps1`

file takes the key from the trigger and passes it to the output binding to delete the cached item.

```
param($key, $TriggerMetadata)
Write-Host "Deleting recently SET key '$key'"
Push-OutputBinding -Name retVal -Value $key
```


This example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

The bindings are defined in this `function.json`

file:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisLocalhost",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisLocalhost",
"command": "DEL",
"name": "$return",
"direction": "out"
}
],
"scriptFile": "__init__.py"
}
```


This code from the `__init__.py`

file takes the key from the trigger and passes it to the output binding to delete the cached item.

```
import logging
def main(key: str) -> str:
logging.info("Deleting recently SET key '" + key + "'")
return key
```


## Attributes

Note

All commands are supported for this binding.

The way in which you define an output binding parameter depends on whether your C# functions runs [in-process](functions-dotnet-class-library) or in an [isolated worker process](dotnet-isolated-process-guide).

The output binding is defined this way:

| Definition | Example | Description |
|---|---|---|
On an `out` parameter |
`[Redis(<Connection>, <Command>)] out string <Return_Variable>` |
The string variable returned by the method is a key value that the binding uses to execute the command against the specific cache. |

In this case, the type returned by the method is a key value that the binding uses to execute the command against the specific cache.

When your function has multiple output bindings, you can instead apply the binding attribute to the property of a type that is a key value, which the binding uses to execute the command against the specific cache. For more information, see [Multiple output bindings](dotnet-isolated-process-guide#multiple-output-bindings).

Regardless of the C# process mode, the same properties are supported by the output binding attribute:

| Attribute property | Description |
|---|---|
`Connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`Command`

`DEL`

.## Annotations

The `RedisOutput`

annotation supports these properties:

| Property | Description |
|---|---|
`name` |
The name of the specific input binding. |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`command`

`DEL`

.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| Property | Description |
|---|---|
`name` |
The name of the specific input binding. |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`command`

`DEL`

.See the [Example section](#example) for complete examples.

## Usage

The output returns a string, which is the key of the cache entry on which apply the specific command.

There are three types of connections that are allowed from an Azure Functions instance to a Redis Cache in your deployments. For local development, you can also use service principal secrets. Use the `appsettings`

to configure each of the following types of client authentication, assuming the `Connection`

was set to `Redis`

in the function.

Important

For optimal security, your function app should use Microsoft Entra ID with managed identities to authorize requests against your cache, if possible. Authorization by using Microsoft Entra ID and managed identities provides superior security and ease of use over shared access key authorization. For more information about using managed identities with your cache, see [Use Microsoft Entra ID for cache authentication](/en-us/azure/azure-cache-for-redis/cache-azure-active-directory-for-authentication).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-node-troubleshoot -->

# Troubleshoot Node.js apps in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The content of this article changes based on your choice of the Node.js programming model in the selector at the top of the page. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. Learn more about the differences between v3 and v4 in the [migration guide](functions-node-upgrade-v4).

This article provides a guide for troubleshooting common scenarios in Node.js function apps.

The **Diagnose and solve problems** tab in the [Azure portal](https://portal.azure.com) is a useful resource to monitor and diagnose possible issues related to your application. It also supplies potential solutions to your problems based on the diagnosis. For more information, see [Azure Function app diagnostics](functions-diagnostics).

Another useful resource is the **Logs** tab in the [Azure portal](https://portal.azure.com) for your Application Insights instance so that you can run custom [KQL queries](/en-us/azure/data-explorer/kusto/query/). The following example query shows how to view errors and warnings for your app in the past day:

```
let myAppName = "<your app name>";
let startTime = ago(1d);
let endTime = now();
union traces,requests,exceptions
| where cloud_RoleName =~ myAppName
| where timestamp between (startTime .. endTime)
| where severityLevel > 2
```


If those resources didn't solve your problem, the following sections provide advice for specific application issues:

## No functions found

If you see any of the following errors in your logs:

No HTTP triggers found.


No job functions found. Try making your job classes and methods public. If you're using binding extensions (e.g. Azure Storage, ServiceBus, Timers, etc.) make sure you've called the registration method for the extension(s) in your startup code (e.g. builder.AddAzureStorage(), builder.AddServiceBus(), builder.AddTimers(), etc.).


Try the following fixes:

- When running locally, make sure you're using Azure Functions Core Tools v4.0.5382 or higher.
- When running in Azure:
Make sure you're using

[Azure Functions Runtime Version](functions-versions)4.25 or higher.Make sure you're using Node.js v18 or higher.

Set the app setting

`FUNCTIONS_NODE_BLOCK_ON_ENTRY_POINT_ERROR`

to`true`

. This setting is recommended for all model v4 apps and ensures that all entry point errors are visible in your application insights logs. For more information, see[App settings reference for Azure Functions](functions-app-settings#functions_node_block_on_entry_point_error).Check your function app logs for entry point errors. The following example query shows how to view entry point errors for your app in the past day:

`let myAppName = "<your app name>"; let startTime = ago(1d); let endTime = now(); union traces,requests,exceptions | where cloud_RoleName =~ myAppName | where timestamp between (startTime .. endTime) | where severityLevel > 2 | where message has "entry point"`


- Make sure your app has the
[required folder structure](functions-reference-node?pivots=nodejs-model-v3#folder-structure)with a*host.json*at the root and a folder for each function containing a*function.json*file.

## Undici request is not a constructor

If you get the following error in your function app logs:

System.Private.CoreLib: Exception while executing function: Functions.httpTrigger1. System.Private.CoreLib: Result: Failure Exception: undici_1.Request is not a constructor


Make sure you're using Node.js version 18.x or higher.

## Failed to detect the Azure Functions runtime

If you get the following error in your function app logs:

WARNING: Failed to detect the Azure Functions runtime. Switching "@azure/functions" package to test mode - not all features are supported.


Check your `package.json`

file for a reference to `applicationinsights`

and make sure the version is `^2.7.1`

or higher. After updating the version, run `npm install`


## Get help from Microsoft

You can get more help from Microsoft in one of the following ways:

- Search the known issues in the
[Azure Functions Node.js repository](https://github.com/Azure/azure-functions-nodejs-library/issues). If you don't see your issue mentioned, create a new issue and let us know what has happened. - If you're not able to diagnose your problem using this guide, Microsoft support engineers are available to help diagnose issues with your application. Microsoft offers
[various support plans](https://azure.microsoft.com/support/plans). Create a support ticket in the**Support + troubleshooting**section of your function app page in the[Azure portal](https://portal.azure.com).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-trigger -->

# Dapr Input Bindings trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions can be triggered on a Dapr input binding using the following Dapr events.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).```
[FunctionName("ConsumeMessageFromKafka")]
public static void Run(
// Note: the value of BindingName must match the binding name in components/kafka-bindings.yaml
[DaprBindingTrigger(BindingName = "%KafkaBindingName%")] JObject triggerData,
ILogger log)
{
log.LogInformation("Hello from Kafka!");
log.LogInformation($"Trigger data: {triggerData}");
}
```


Here's the Java code for the Dapr Input Binding trigger:

```
@FunctionName("ConsumeMessageFromKafka")
public String run(
@DaprBindingTrigger(
bindingName = "%KafkaBindingName%")
)
```


Use the `app`

object to register the `daprBindingTrigger`

:

```
const { app, trigger } = require('@azure/functions');
app.generic('ConsumeMessageFromKafka', {
trigger: trigger.generic({
type: 'daprBindingTrigger',
bindingName: "%KafkaBindingName%",
name: "triggerData"
}),
handler: async (request, context) => {
context.log("Node function processed a ConsumeMessageFromKafka request from the Dapr Runtime.");
context.log(context.triggerMetadata.triggerData)
}
});
```


The following example shows Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprBindingTrigger`

:

```
{
"bindings": [
{
"type": "daprBindingTrigger",
"bindingName": "%KafkaBindingName%",
"name": "triggerData",
"direction": "in"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

In code:

```
using namespace System
using namespace Microsoft.Azure.WebJobs
using namespace Microsoft.Extensions.Logging
using namespace Microsoft.Azure.WebJobs.Extensions.Dapr
using namespace Newtonsoft.Json.Linq
param (
$triggerData
)
Write-Host "PowerShell function processed a ConsumeMessageFromKafka request from the Dapr Runtime."
$jsonString = $triggerData | ConvertTo-Json
Write-Host "Trigger data: $jsonString"
```


The following example shows a Dapr Input Binding trigger, which uses the [v2 Python programming model](functions-reference-python). To use the `daprBinding`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="ConsumeMessageFromKafka")
@app.dapr_binding_trigger(arg_name="triggerData", binding_name="%KafkaBindingName%")
def main(triggerData: str) -> None:
logging.info('Python function processed a ConsumeMessageFromKafka request from the Dapr Runtime.')
logging.info('Trigger data: ' + triggerData)
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprBindingTrigger`

to trigger a Dapr input binding, which supports the following properties.

| Parameter | Description |
|---|---|
BindingName |
The name of the Dapr trigger. If not specified, the name of the function is used as the trigger name. |

## Annotations

The `DaprBindingTrigger`

annotation allows you to create a function that gets triggered by the binding component you created.

| Element | Description |
|---|---|
bindingName |
The name of the Dapr binding. |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description |
|---|---|
bindingName |
The name of the binding. |

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description |
|---|---|
bindingName |
The name of the binding. |

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr Input Binding trigger, start by setting up a Dapr input binding component. You can learn more about which component to use and how to set it up in the official Dapr documentation.

To use the `daprBindingTrigger`

in Python v2, set up your project with the correct dependencies.

In your

`requirements.text`

file, add the following line:`azure-functions==1.18.0b3`

In the terminal, install the Python library.

`pip install -r .\requirements.txt`

Modify your

`local.setting.json`

file with the following configuration:`"PYTHON_ISOLATE_WORKER_DEPENDENCIES":1`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-table-output -->

# Azure Tables output bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use an Azure Tables output binding to write entities to a table in [Azure Cosmos DB for Table](/en-us/azure/cosmos-db/table/introduction) or [Azure Table Storage](../storage/tables/table-storage-overview).

For information on setup and configuration details, see the [overview](functions-bindings-storage-table)

Note

This output binding only supports creating new entities in a table. If you need to update an existing entity from your function code, instead use an Azure Tables SDK directly.

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Example

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following `MyTableData`

class represents a row of data in the table:

```
public class MyTableData : Azure.Data.Tables.ITableEntity
{
public string Text { get; set; }
public string PartitionKey { get; set; }
public string RowKey { get; set; }
public DateTimeOffset? Timestamp { get; set; }
public ETag ETag { get; set; }
}
```


The following function, which is started by a Queue Storage trigger, writes a new `MyDataTable`

entity to a table named **OutputTable**.

```
[Function("TableFunction")]
[TableOutput("OutputTable", Connection = "AzureWebJobsStorage")]
public static MyTableData Run(
[QueueTrigger("table-items")] string input,
[TableInput("MyTable", "<PartitionKey>", "{queueTrigger}")] MyTableData tableInput,
FunctionContext context)
{
var logger = context.GetLogger("TableFunction");
logger.LogInformation($"PK={tableInput.PartitionKey}, RK={tableInput.RowKey}, Text={tableInput.Text}");
return new MyTableData()
{
PartitionKey = "queue",
RowKey = Guid.NewGuid().ToString(),
Text = $"Output record with rowkey {input} created at {DateTime.Now}"
};
}
```


The following example shows a Java function that uses an HTTP trigger to write a single table row.

```
public class Person {
private String PartitionKey;
private String RowKey;
private String Name;
public String getPartitionKey() {return this.PartitionKey;}
public void setPartitionKey(String key) {this.PartitionKey = key; }
public String getRowKey() {return this.RowKey;}
public void setRowKey(String key) {this.RowKey = key; }
public String getName() {return this.Name;}
public void setName(String name) {this.Name = name; }
}
public class AddPerson {
@FunctionName("addPerson")
public HttpResponseMessage get(
@HttpTrigger(name = "postPerson", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.FUNCTION, route="persons/{partitionKey}/{rowKey}") HttpRequestMessage<Optional<Person>> request,
@BindingName("partitionKey") String partitionKey,
@BindingName("rowKey") String rowKey,
@TableOutput(name="person", partitionKey="{partitionKey}", rowKey = "{rowKey}", tableName="%MyTableName%", connection="MyConnectionString") OutputBinding<Person> person,
final ExecutionContext context) {
Person outPerson = new Person();
outPerson.setPartitionKey(partitionKey);
outPerson.setRowKey(rowKey);
outPerson.setName(request.getBody().get().getName());
person.setValue(outPerson);
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(outPerson)
.build();
}
}
```


The following example shows a Java function that uses an HTTP trigger to write multiple table rows.

```
public class Person {
private String PartitionKey;
private String RowKey;
private String Name;
public String getPartitionKey() {return this.PartitionKey;}
public void setPartitionKey(String key) {this.PartitionKey = key; }
public String getRowKey() {return this.RowKey;}
public void setRowKey(String key) {this.RowKey = key; }
public String getName() {return this.Name;}
public void setName(String name) {this.Name = name; }
}
public class AddPersons {
@FunctionName("addPersons")
public HttpResponseMessage get(
@HttpTrigger(name = "postPersons", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.FUNCTION, route="persons/") HttpRequestMessage<Optional<Person[]>> request,
@TableOutput(name="person", tableName="%MyTableName%", connection="MyConnectionString") OutputBinding<Person[]> persons,
final ExecutionContext context) {
persons.setValue(request.getBody().get());
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(request.getBody().get())
.build();
}
}
```


The following example shows a table output binding that writes multiple table entities.

```
import { app, HttpRequest, HttpResponseInit, InvocationContext, output } from '@azure/functions';
const tableOutput = output.table({
tableName: 'Person',
connection: 'MyStorageConnectionAppSetting',
});
interface PersonEntity {
PartitionKey: string;
RowKey: string;
Name: string;
}
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
const rows: PersonEntity[] = [];
for (let i = 1; i < 10; i++) {
rows.push({
PartitionKey: 'Test',
RowKey: i.toString(),
Name: `Name ${i}`,
});
}
context.extraOutputs.set(tableOutput, rows);
return { status: 201 };
}
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [tableOutput],
handler: httpTrigger1,
});
```


```
const { app, output } = require('@azure/functions');
const tableOutput = output.table({
tableName: 'Person',
connection: 'MyStorageConnectionAppSetting',
});
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [tableOutput],
handler: async (request, context) => {
const rows = [];
for (let i = 1; i < 10; i++) {
rows.push({
PartitionKey: 'Test',
RowKey: i.toString(),
Name: `Name ${i}`,
});
}
context.extraOutputs.set(tableOutput, rows);
return { status: 201 };
},
});
```


The following example demonstrates how to write multiple entities to a table from a function.

Binding configuration in *function.json*:

```
{
"bindings": [
{
"name": "InputData",
"type": "manualTrigger",
"direction": "in"
},
{
"tableName": "Person",
"connection": "MyStorageConnectionAppSetting",
"name": "TableBinding",
"type": "table",
"direction": "out"
}
],
"disabled": false
}
```


PowerShell code in *run.ps1*:

```
param($InputData, $TriggerMetadata)
foreach ($i in 1..10) {
Push-OutputBinding -Name TableBinding -Value @{
PartitionKey = 'Test'
RowKey = "$i"
Name = "Name $i"
}
}
```


The following example demonstrates how to use the Table storage output binding. Configure the `table`

binding in the *function.json* by assigning values to `name`

, `tableName`

, `partitionKey`

, and `connection`

:

The following function generates a unique UUI for the `rowKey`

value and persists the message into Table storage.

```
import logging
import uuid
import json
import azure.functions as func
app = func.FunctionApp()
@app.route(route="table_out_binding")
@app.table_output(arg_name="message",
connection="AzureWebJobsStorage",
table_name="messages")
def table_out_binding(req: func.HttpRequest, message: func.Out[str]):
row_key = str(uuid.uuid4())
data = {
"Name": "Output binding message",
"PartitionKey": "message",
"RowKey": row_key
}
table_json = json.dumps(data)
message.set(table_json)
return table_json
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#table-output).

In [C# class libraries](dotnet-isolated-process-guide), the `TableInputAttribute`

supports the following properties:

| Attribute property | Description |
|---|---|
TableName |
The name of the table to which to write. |
PartitionKey |
The partition key of the table entity to write. |
RowKey |
The row key of the table entity to write. |
Connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the [TableOutput](https://github.com/Azure/azure-functions-java-library/blob/master/src/main/java/com/microsoft/azure/functions/annotation/TableOutput.java/) annotation on parameters to write values into your tables. The attribute supports the following elements:

| Element | Description |
|---|---|
name |
The variable name used in function code that represents the table or entity. |
dataType |
Defines how Functions runtime should treat the parameter value. To learn more, see
|

**tableName****partitionKey****rowKey****connection**[Connections](#connections).## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `output.table()`

method.

| Property | Description |
|---|---|
tableName |
The name of the table to which to write. |
partitionKey |
The partition key of the table entity to write. |
rowKey |
The row key of the table entity to write. |
connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `table` . This property is set automatically when you create the binding in the Azure portal. |
direction |
Must be set to `out` . This property is set automatically when you create the binding in the Azure portal. |
name |
The variable name used in function code that represents the table or entity. Set to `$return` to reference the function return value. |
tableName |
The name of the table to which to write. |
partitionKey |
The partition key of the table entity to write. |
rowKey |
The row key of the table entity to write. |
connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Connections

The `connection`

property is a reference to environment configuration that specifies how the app should connect to your table service. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections)

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

To obtain a connection string for tables in Azure Table storage, follow the steps shown at [Manage storage account access keys](../storage/common/storage-account-keys-manage). To obtain a connection string for tables in Azure Cosmos DB for Table, follow the steps shown at the [Azure Cosmos DB for Table FAQ](/en-us/azure/cosmos-db/table/table-api-faq#what-is-the-connection-string-that-i-need-to-use-to-connect-to-the-api-for-table-).

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here. For example, if you set `connection`

to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage". If you leave `connection`

empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`

.

### Identity-based connections

If you're using [the Tables API extension](functions-bindings-storage-table#table-api-extension), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). This only applies when accessing tables in Azure Storage. To use an identity, you define settings under a common prefix that maps to the `connection`

property in the trigger and binding configuration.

If you're setting `connection`

to "AzureWebJobsStorage", see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity). For all other connections, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Table Service URI | `<CONNECTION_NAME_PREFIX>__tableServiceUri` 1 |
The data plane URI of the Azure Storage table service to which you're connecting, using the HTTPS scheme. | https://<storage_account_name>.table.core.windows.net |

1 `<CONNECTION_NAME_PREFIX>__serviceUri`

can be used as an alias. If both forms are provided, the `tableServiceUri`

form is used. The `serviceUri`

form can't be used when the overall connection configuration is to be used across blobs, queues, and/or tables.

Other properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

The `serviceUri`

form can't be used when the overall connection configuration is to be used across blobs, queues, and/or tables in Azure Storage. The URI can only designate the table service. As an alternative, you can provide a URI specifically for each service under the same prefix, allowing a single connection to be used.

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You'll need to create a role assignment that provides access to your Azure Storage table service at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The following table shows built-in roles that are recommended when using the Azure Tables extension against Azure Storage in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles (Azure Storage1) |
|---|---|
| Input binding |
|

[Storage Table Data Contributor](../role-based-access-control/built-in-roles#storage-table-data-contributor)1 If your app is instead connecting to tables in Azure Cosmos DB for Table, using an identity isn't supported and the connection must use a connection string.

## Usage

The usage of the binding depends on the extension package version, and the C# modality used in your function app, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see usage details for the mode and version.

When you want the function to write to a single entity, the Azure Tables output binding can bind to the following types:

| Type | Description |
|---|---|
| A JSON serializable type that implements [ITableEntity] | Functions attempts to serialize a plain-old CLR object (POCO) type as the entity. The type must implement [ITableEntity] or have a string `RowKey` property and a string `PartitionKey` property. |

When you want the function to write to multiple entities, the Azure Tables output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single entity types |
An array containing multiple entities. Each entry represents one entity. |

For other output scenarios, create and use a [TableClient](/en-us/dotnet/api/azure.data.tables.tableclient) with other types from [Azure.Data.Tables](/en-us/dotnet/api/azure.data.tables) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

There are two options for outputting a Table storage row from a function by using the [TableStorageOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.tableoutput) annotation:

| Options | Description |
|---|---|
Return value |
By applying the annotation to the function itself, the return value of the function persists as a Table storage row. |
Imperative |
To explicitly set the table row, apply the annotation to a specific parameter of the type
`OutputBinding<T>` |

`T`

includes the `PartitionKey`

and `RowKey`

properties. You can accompany these properties by implementing `ITableEntity`

or inheriting `TableEntity`

.To write to table data, use the `Push-OutputBinding`

cmdlet, set the `-Name TableBinding`

parameter and `-Value`

parameter equal to the row data. See the [PowerShell example](#example) for more detail.

There are two options for outputting a Table storage row message from a function:

| Options | Description |
|---|---|
Return value |
Set the `name` property in function.json to `$return` . With this configuration, the function's return value persists as a Table storage row. |
Imperative |
Pass a value to the
`set` is persisted as table row. |

For specific usage details, see [Example](#example).

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Table |
|

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-custom-handlers -->

# Azure Functions custom handlers

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions executes your app code by using language-specific handlers. These language-specific handlers allow Functions to support [most key languages](supported-languages) by default. However, you might need to run code in another language or package.

Custom handlers are lightweight web servers that receive events from the Azure Functions host process. You can use custom handlers to deploy to Azure Functions any code project that supports HTTP primitives.

Custom handlers are best suited for situations where you want to:

- Implement a function app in a language that's not currently offered out-of-the-box, such as Go or Rust.
- Implement a function app in a runtime that's not currently featured by default, such as Deno.
[Deploy a server](#deploy-self-hosted-mcp-servers)built with the standard MCP SDKs to Azure Functions.

With custom handlers, you can use [triggers and input and output bindings](functions-triggers-bindings) via [extension bundles](functions-bindings-register).

Get started with Azure Functions custom handlers with [quickstarts in Go and Rust](create-first-function-vs-code-other).

## Overview

The following diagram shows the relationship between the Functions host and a web server implemented as a custom handler.

- Each event triggers a request sent to the Functions host. An event is any trigger that Azure Functions supports.
- The Functions host then issues a
[request payload](#request-payload)to the web server. The payload holds trigger and input binding data and other metadata for the function. - The web server executes the individual function, and returns a
[response payload](#response-payload)to the Functions host. - The Functions host passes data from the response to the function's output bindings for processing.

An Azure Functions app implemented as a custom handler must configure the *host.json*, *local.settings.json*, and *function.json* files according to a few conventions.

## Deploy self-hosted MCP servers

Custom handlers also enables you to host MCP servers that you build by using official MCP SDKs in Azure Functions. Custom handlers provides a simple and streamlined experience for hosting your MCP servers in Azure. For more information, see [Self-hosted remote MCP server on Azure Functions](self-hosted-mcp-servers).

Note

The ability to have Azure Functions host MCP servers you create using official MCP SDKs is currently in preview.

## Application structure

To implement a custom handler, your application needs the following aspects:

- A
*host.json*file at the root of your app - A
*local.settings.json*file at the root of your app - A
*function.json*file for each function (inside a folder that matches the function name) - A command, script, or executable that runs a web server

The following diagram shows how these files look on the file system for a function named "MyQueueFunction" and a custom handler executable named *handler.exe*.

```
| /MyQueueFunction
| function.json
|
| host.json
| local.settings.json
| handler.exe
```


### Configuration

You configure the application through the *host.json* and *local.settings.json* files.

#### host.json

*host.json* directs the Functions host where to send requests by pointing to a web server that can process HTTP events.

Define a custom handler by configuring the *host.json* file with details on how to run the web server through the `customHandler`

section.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
}
}
}
```


The `customHandler`

section points to a target as defined by the `defaultExecutablePath`

. The execution target can be a command, executable, or file where the web server is implemented.

Use the `arguments`

array to pass any arguments to the executable. Arguments support expansion of environment variables (application settings) by using `%%`

notation.

You can also change the working directory used by the executable with `workingDirectory`

.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "app/handler.exe",
"arguments": [
"--database-connection-string",
"%DATABASE_CONNECTION_STRING%"
],
"workingDirectory": "app"
}
}
}
```


##### Bindings support

Standard triggers along with input and output bindings are available by referencing [extension bundles](functions-bindings-register) in your *host.json* file.

#### local.settings.json

*local.settings.json* defines application settings used when running the function app locally. Because it might contain secrets, exclude *local.settings.json* from source control. In Azure, use application settings instead.

For custom handlers, set `FUNCTIONS_WORKER_RUNTIME`

to `Custom`

in *local.settings.json*.

```
{
"IsEncrypted": false,
"Values": {
"FUNCTIONS_WORKER_RUNTIME": "Custom"
}
}
```


### Function metadata

When you use a custom handler, the *function.json* contents are the same as when you define a function in any other context. The only requirement is that you must place *function.json* files in a folder named to match the function name.

The following *function.json* configures a function that has a queue trigger and a queue output binding. Because it's in a folder named *MyQueueFunction*, it defines a function named *MyQueueFunction*.

**MyQueueFunction/function.json**

```
{
"bindings": [
{
"name": "myQueueItem",
"type": "queueTrigger",
"direction": "in",
"queueName": "messages-incoming",
"connection": "AzureWebJobsStorage"
},
{
"name": "$return",
"type": "queue",
"direction": "out",
"queueName": "messages-outgoing",
"connection": "AzureWebJobsStorage"
}
]
}
```


### Request payload

When the Functions host receives a queue message, it sends an HTTP post request to the custom handler with a payload in the body.

The following code shows a sample request payload. The payload includes a JSON structure with two members: `Data`

and `Metadata`

.

The `Data`

member includes keys that match input and trigger names as defined in the bindings array in the *function.json* file.

The `Metadata`

member includes [metadata generated from the event source](functions-bindings-expressions-patterns#trigger-metadata).

```
{
"Data": {
"myQueueItem": "{ message: \"Message sent\" }"
},
"Metadata": {
"DequeueCount": 1,
"ExpirationTime": "2019-10-16T17:58:31+00:00",
"Id": "800ae4b3-bdd2-4c08-badd-f08e5a34b865",
"InsertionTime": "2019-10-09T17:58:31+00:00",
"NextVisibleTime": "2019-10-09T18:08:32+00:00",
"PopReceipt": "AgAAAAMAAAAAAAAAAgtnj8x+1QE=",
"sys": {
"MethodName": "QueueTrigger",
"UtcNow": "2019-10-09T17:58:32.2205399Z",
"RandGuid": "24ad4c06-24ad-4e5b-8294-3da9714877e9"
}
}
}
```


### Response payload

By convention, function responses are formatted as key/value pairs. Supported keys include:

| Data type | Remarks | |
|---|---|---|
`Outputs` |
object | Holds response values as defined by the `bindings` array in function.json.For instance, if a function is configured with a queue output binding named "myQueueOutput", then `Outputs` contains a key named `myQueueOutput` , which the custom handler sets to the messages that it sends to the queue. |
`Logs` |
array | Messages that appear in the Functions invocation logs. When running in Azure, messages appear in Application Insights. |
`ReturnValue` |
string | Used to provide a response when an output is configured as `$return` in the function.json file. |

This table shows an example of a response payload.

```
{
"Outputs": {
"res": {
"body": "Message enqueued"
},
"myQueueOutput": [
"queue message 1",
"queue message 2"
]
},
"Logs": [
"Log message 1",
"Log message 2"
],
"ReturnValue": "{\"hello\":\"world\"}"
}
```


## Examples

You can implement custom handlers in any language that supports receiving HTTP events. The following examples show how to implement a custom handler by using the Go programming language.

### Function with bindings

This example shows a function named `order`

that accepts a `POST`

request with a payload representing a product order. When you post an order to the function, it creates a Queue Storage message and returns an HTTP response.

#### Implementation

In a folder named *order*, the *function.json* file configures the HTTP-triggered function.

**order/function.json**

```
{
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": ["post"]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"type": "queue",
"name": "message",
"direction": "out",
"queueName": "orders",
"connection": "AzureWebJobsStorage"
}
]
}
```


This function is defined as an [HTTP triggered function](functions-bindings-http-webhook-trigger) that returns an [HTTP response](functions-bindings-http-webhook-output) and outputs a [Queue storage](functions-bindings-storage-queue-output) message.

At the root of the app, the *host.json* file is configured to run an executable file named `handler.exe`

(`handler`

in Linux or macOS).

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


This is the HTTP request sent to the Functions runtime.

```
POST http://127.0.0.1:7071/api/order HTTP/1.1
Content-Type: application/json
{
"id": 1005,
"quantity": 2,
"color": "black"
}
```


The Functions runtime sends the following HTTP request to the custom handler:

```
POST http://127.0.0.1:<FUNCTIONS_CUSTOMHANDLER_PORT>/order HTTP/1.1
Content-Type: application/json
{
"Data": {
"req": {
"Url": "http://localhost:7071/api/order",
"Method": "POST",
"Query": "{}",
"Headers": {
"Content-Type": [
"application/json"
]
},
"Params": {},
"Body": "{\"id\":1005,\"quantity\":2,\"color\":\"black\"}"
}
},
"Metadata": {
}
}
```


Note

Some portions of the payload were removed for brevity.

*handler.exe* is the compiled Go custom handler program that runs a web server and responds to function invocation requests from the Functions host.

```
package main
import (
"encoding/json"
"fmt"
"log"
"net/http"
"os"
)
type InvokeRequest struct {
Data map[string]json.RawMessage
Metadata map[string]interface{}
}
type InvokeResponse struct {
Outputs map[string]interface{}
Logs []string
ReturnValue interface{}
}
func orderHandler(w http.ResponseWriter, r *http.Request) {
var invokeRequest InvokeRequest
d := json.NewDecoder(r.Body)
d.Decode(&invokeRequest)
var reqData map[string]interface{}
json.Unmarshal(invokeRequest.Data["req"], &reqData)
outputs := make(map[string]interface{})
outputs["message"] = reqData["Body"]
resData := make(map[string]interface{})
resData["body"] = "Order enqueued"
outputs["res"] = resData
invokeResponse := InvokeResponse{outputs, nil, nil}
responseJson, _ := json.Marshal(invokeResponse)
w.Header().Set("Content-Type", "application/json")
w.Write(responseJson)
}
func main() {
customHandlerPort, exists := os.LookupEnv("FUNCTIONS_CUSTOMHANDLER_PORT")
if !exists {
customHandlerPort = "8080"
}
mux := http.NewServeMux()
mux.HandleFunc("/order", orderHandler)
fmt.Println("Go server Listening on: ", customHandlerPort)
log.Fatal(http.ListenAndServe(":"+customHandlerPort, mux))
}
```


In this example, the custom handler runs a web server to handle HTTP events and listens for requests via the `FUNCTIONS_CUSTOMHANDLER_PORT`

.

Even though the Functions host receives the original HTTP request at `/api/order`

, it invokes the custom handler by using the function name (its folder name). In this example, the function is defined at the path of `/order`

. The host sends the custom handler an HTTP request at the path of `/order`

.

When you send `POST`

requests to this function, the trigger data and function metadata are available via the HTTP request body. You can access the original HTTP request body in the payload's `Data.req.Body`

.

The function's response is formatted into key/value pairs where the `Outputs`

member holds a JSON value where the keys match the outputs as defined in the *function.json* file.

This is an example payload that this handler returns to the Functions host.

```
{
"Outputs": {
"message": "{\"id\":1005,\"quantity\":2,\"color\":\"black\"}",
"res": {
"body": "Order enqueued"
}
},
"Logs": null,
"ReturnValue": null
}
```


By setting the `message`

output equal to the order data that came in from the request, the function outputs that order data to the configured queue. The Functions host also returns the HTTP response configured in `res`

to the caller.

### HTTP-only function

For HTTP-triggered functions with no additional bindings or outputs, you might want your handler to work directly with the HTTP request and response instead of the custom handler [request](#request-payload) and [response](#response-payload) payloads. You can configure this behavior in *host.json* by using the `enableProxyingHttpRequest`

setting, which supports response streaming.

Important

The primary purpose of the custom handlers feature is to enable languages and runtimes that don't currently have first-class support on Azure Functions. While you might be able to run web applications by using custom handlers, Azure Functions isn't a standard reverse proxy. Some components of the HTTP request, such as certain headers and routes, might be restricted. Your application might also experience excessive [cold start](event-driven-scaling#cold-start).

To address these circumstances, consider running your web apps on [Azure App Service](../app-service/overview).

The following example demonstrates how to configure an HTTP-triggered function with no additional bindings or outputs. The scenario implemented in this example features a function named `hello`

that accepts a `GET`

or `POST`

.

#### Implementation

In a folder named *hello*, the *function.json* file configures the HTTP-triggered function.

**hello/function.json**

```
{
"bindings": [
{
"type": "httpTrigger",
"authLevel": "function",
"direction": "in",
"name": "req",
"methods": ["get", "post"]
},
{
"type": "http",
"direction": "out",
"name": "res"
}
]
}
```


The function is configured to accept both `GET`

and `POST`

requests, and the result value is provided through an argument named `res`

.

At the root of the app, the *host.json* file is configured to run `handler.exe`

and `enableProxyingHttpRequest`

is set to `true`

.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
},
"enableProxyingHttpRequest": true
}
}
```


The following is a POST request to the Functions host. The Functions host then sends the request to the custom handler.

```
POST http://127.0.0.1:7071/api/hello HTTP/1.1
Content-Type: application/json
{
"message": "Hello World!"
}
```


The *handler.go* file implements a web server and HTTP function.

```
package main
import (
"fmt"
"io/ioutil"
"log"
"net/http"
"os"
)
func helloHandler(w http.ResponseWriter, r *http.Request) {
w.Header().Set("Content-Type", "application/json")
if r.Method == "GET" {
w.Write([]byte("hello world"))
} else {
body, _ := ioutil.ReadAll(r.Body)
w.Write(body)
}
}
func main() {
customHandlerPort, exists := os.LookupEnv("FUNCTIONS_CUSTOMHANDLER_PORT")
if !exists {
customHandlerPort = "8080"
}
mux := http.NewServeMux()
mux.HandleFunc("/api/hello", helloHandler)
fmt.Println("Go server Listening on: ", customHandlerPort)
log.Fatal(http.ListenAndServe(":"+customHandlerPort, mux))
}
```


In this example, the custom handler creates a web server to handle HTTP events and listens for requests via the `FUNCTIONS_CUSTOMHANDLER_PORT`

.

`GET`

requests are handled by returning a string, and `POST`

requests have access to the request body.

The route for the order function here is `/api/hello`

, same as the original request.

Note

The `FUNCTIONS_CUSTOMHANDLER_PORT`

isn't the public facing port used to call the function. The Functions host uses this port to call the custom handler.

## Deploying

You can deploy a custom handler to every Azure Functions hosting option. If your handler requires operating system or platform dependencies (such as a language runtime), you might need to use a [custom container](functions-how-to-custom-container).

When you create a function app in Azure for custom handlers, select .NET Core as the stack.

To deploy a custom handler app by using Azure Functions Core Tools, run the following command.

```
func azure functionapp publish $functionAppName
```


Note

Ensure all files required to run your custom handler are in the folder and included in the deployment. If your custom handler is a binary executable or has platform-specific dependencies, ensure these files match the target deployment platform.

## Restrictions

- The custom handler web server needs to start within 60 seconds.

## Samples

For examples of how to implement functions in a variety of different languages, see the [custom handler samples GitHub repo](https://github.com/Azure-Samples/functions-custom-handlers).

## Troubleshooting and support

### Trace logging

If your custom handler process fails to start or if it has problems communicating with the Functions host, increase the function app's log level to `Trace`

to see more diagnostic messages from the host.

To change the function app's default log level, configure the `logLevel`

setting in the `logging`

section of *host.json*.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
}
},
"logging": {
"logLevel": {
"default": "Trace"
}
}
}
```


The Functions host outputs extra log messages, including information related to the custom handler process. Use the logs to investigate problems starting your custom handler process or invoking functions in your custom handler.

Locally, logs are printed to the console.

In Azure, [query Application Insights traces](analyze-telemetry-data#query-telemetry-data) to view the log messages. If your app produces a high volume of logs, only a subset of log messages are sent to Application Insights. [Disable sampling](configure-monitoring#configure-sampling) to ensure all messages are logged.

### Test custom handler in isolation

Custom handler apps are web server processes, so it might be helpful to start them on their own and test function invocations by sending mock [HTTP requests](#request-payload). For sending HTTP requests with payloads, make sure to choose a tool that keeps your data secure. For more information, see [HTTP test tools](functions-develop-local#http-test-tools).

You can also use this strategy in your CI/CD pipelines to run automated tests on your custom handler.

### Execution environment

Custom handlers run in the same environment as a typical Azure Functions app. Test your handler to ensure the environment contains all the dependencies it needs to run. For apps that require additional dependencies, you might need to run them by using a [custom container image](functions-how-to-custom-container) hosted on Azure Functions [Premium plan](functions-premium-plan).

### Get support

If you need help on a function app with custom handlers, you can submit a request through regular support channels. However, due to the wide variety of possible languages used to build custom handlers apps, support isn't unlimited.

Support is available if the Functions host has problems starting or communicating with the custom handler process. For problems specific to the inner workings of your custom handler process, such as issues with the chosen language or framework, our Support Team can't provide assistance in this context.

## Next steps

Get started building an Azure Functions app in Go or Rust with the [custom handlers quickstart](create-first-function-vs-code-other).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-signalr-service-trigger -->

# SignalR Service trigger binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the *SignalR* trigger binding to respond to messages sent from Azure SignalR Service. When function is triggered, messages passed to the function is parsed as a json object.

In SignalR Service serverless mode, SignalR Service uses the [Upstream](../azure-signalr/concept-upstream) feature to send messages from client to Function App. And Function App uses SignalR Service trigger binding to handle these messages. The general architecture is shown below:


For information on setup and configuration details, see the [overview](functions-bindings-signalr-service).

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following sample shows a C# function that receives a message event from clients and logs the message content.

```
[Function(nameof(OnClientMessage))]
public static void OnClientMessage(
[SignalRTrigger("Hub", "messages", "sendMessage", "content", ConnectionStringSetting = "SignalRConnection")]
SignalRInvocationContext invocationContext, string content, FunctionContext functionContext)
{
var logger = functionContext.GetLogger(nameof(OnClientMessage));
logger.LogInformation("Connection {connectionId} sent a message. Message content: {content}", invocationContext.ConnectionId, content);
}
```


Important

Class based model of SignalR Service bindings in C# isolated worker doesn't optimize how you write SignalR triggers due to the limitation of C# worker model. For more information about class based model, see [Class based model](../azure-signalr/signalr-concept-serverless-development-config#class-based-model).

SignalR trigger isn't currently supported for Java.

Here's binding data in the *function.json* file:

```
{
"type": "signalRTrigger",
"name": "invocation",
"hubName": "hubName1",
"category": "messages",
"event": "SendMessage",
"parameterNames": [
"message"
],
"direction": "in"
}
```


```
app.generic("function1",
{
trigger: { "type": "signalRTrigger", "name": "invocation", "direction": "in", "hubName": "hubName1", "event": "SendMessage", "category": "messages" },
handler: (triggerInput, context) => {
context.log(`Receive ${triggerInput.Arguments[0]} from ${triggerInput.ConnectionId}.`)
}
})
```


Complete PowerShell examples are pending.

Here's the Python code:

```
import logging
import json
import azure.functions as func
def main(invocation) -> None:
invocation_json = json.loads(invocation)
logging.info("Receive {0} from {1}".format(invocation_json['Arguments'][0], invocation_json['ConnectionId']))
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the `SignalRTrigger`

attribute to define the function. C# script instead uses a [function.json configuration file](#configuration).

The following table explains the properties of the `SignalRTrigger`

attribute.

| Attribute property | Description |
|---|---|
HubName |
This value must be set to the name of the SignalR hub for the function to be triggered. |
Category |
This value must be set as the category of messages for the function to be triggered. The category can be one of the following values:
|
Event |
This value must be set as the event of messages for the function to be triggered. For messages category, event is the target in
connections category, only connected and disconnected is used. |
ParameterNames |
(Optional) A list of names that binds to the parameters. |
ConnectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |

## Annotations

There isn't currently a supported Java annotation for a SignalR trigger.

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `SignalRTrigger` . |
direction |
Must be set to `in` . |
name |
Variable name used in function code for trigger invocation context object. |
hubName |
This value must be set to the name of the SignalR hub for the function to be triggered. |
category |
This value must be set as the category of messages for the function to be triggered. The category can be one of the following values:
|
event |
This value must be set as the event of messages for the function to be triggered. For messages category, event is the target in
connections category, only connected and disconnected is used. |
parameterNames |
(Optional) A list of names that binds to the parameters. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |

See the [Example section](#example) for complete examples.

## Usage

### Managed identity-based connections

For optimal security, your function app should use managed identities when connecting to the Azure SignalR service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize requests to Azure SignalR Service resources with Microsoft Entra managed identities](../azure-signalr/signalr-howto-authorize-managed-identity#azure-signalr-service-bindings-in-azure-functions).

### Payloads

The trigger input type is declared as either `InvocationContext`

or a custom type. If you choose `InvocationContext`

, you get full access to the request content. For a custom type, the runtime tries to parse the JSON request body to set the object properties.

### InvocationContext

`InvocationContext`

contains all the content in the message sent from a SignalR service, which includes the following properties:

| Property | Description |
|---|---|
| Arguments | Available for messages category. Contains arguments in
|
| Error | Available for disconnected event. It can be Empty if the connection closed with no error, or it contains the error messages. |
| Hub | The hub name that the message belongs to. |
| Category | The category of the message. |
| Event | The event of the message. |
| ConnectionId | The connection ID of the client that sends the message. |
| UserId | The user identity of the client that sends the message. |
| Headers | The headers of the request. |
| Query | The query of the request when clients connect to the service. |
| Claims | The claims of the client. |

### Using `ParameterNames`


The property `ParameterNames`

in `SignalRTrigger`

lets you bind arguments of invocation messages to the parameters of functions. You can use the name you defined as part of [binding expressions](functions-bindings-expressions-patterns) in other binding or as parameters in your code. That gives you a more convenient way to access arguments of `InvocationContext`

.

Say you have a JavaScript SignalR client trying to invoke method `broadcast`

in Azure Function with two arguments `message1`

, `message2`

.

```
await connection.invoke("broadcast", message1, message2);
```


After you set `parameterNames`

, the names you defined correspond to the arguments sent on the client side.

```
[SignalRTrigger(parameterNames: new string[] {"arg1, arg2"})]
```


Then, the `arg1`

contains the content of `message1`

, and `arg2`

contains the content of `message2`

.

`ParameterNames`

considerations

For the parameter binding, the order matters. If you're using `ParameterNames`

, the order in `ParameterNames`

matches the order of the arguments you invoke in the client. If you're using attribute `[SignalRParameter]`

in C#, the order of arguments in Azure Function methods matches the order of arguments in clients.

`ParameterNames`

and attribute `[SignalRParameter]`

**cannot** be used at the same time, or you'll get an exception.

### SignalR Service integration

SignalR Service needs a URL to access Function App when you're using SignalR Service trigger binding. The URL should be configured in **Upstream Settings** on the SignalR Service side.


When using SignalR Service trigger, the URL can be simple and formatted as follows:

```
<Function_App_URL>/runtime/webhooks/signalr?code=<API_KEY>
```


The `Function_App_URL`

can be found on Function App's Overview page and the `API_KEY`

is generated by Azure Function. You can get the `API_KEY`

from `signalr_extension`

in the **App keys** blade of Function App.

If you want to use more than one Function App together with one SignalR Service, upstream can also support complex routing rules. Find more details at [Upstream settings](../azure-signalr/concept-upstream).

### Step-by-step sample

You can follow the sample in GitHub to deploy a chat room on Function App with SignalR Service trigger binding and upstream feature: [Bidirectional chat room sample](https://github.com/aspnet/AzureSignalR-samples/tree/master/samples/BidirectionChat)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-output -->

# Azure Cache for Redis output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Cache for Redis output bindings lets you change the keys in a cache based on a set of available trigger on the cache.

For information on setup and configuration details, see the [overview](functions-bindings-cache).

## Scope of availability for functions bindings

| Binding Type | Azure Managed Redis | Azure Cache for Redis |
|---|---|---|
| Output | Yes | Yes |

Important

When using Azure Managed Redis or the Enterprise tiers of Azure Cache for Redis, use port 10000 rather than port 6380 or 6379.

Important

The Node.js v4 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Important

The Python v2 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v2 model works, refer to the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

## Example

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

The following example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

Important

For .NET functions, using the *isolated worker* model is recommended over the *in-process* model. For a comparison of the *in-process* and *isolated worker* models, see differences between the *isolated worker* model and the *in-process* model for .NET on Azure Functions.

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisOutputBinding
{
internal class SetDeleter
{
[Function(nameof(SetDeleter))]
[RedisOutput(Common.connectionString, "DEL")]
public static string Run(
[RedisPubSubTrigger(Common.connectionString, "__keyevent@0__:set")] string key,
ILogger logger)
{
logger.LogInformation($"Deleting recently SET key '{key}'");
return key;
}
}
}
```


```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.WebJobs.Extensions.Redis.Samples.RedisOutputBinding
{
internal class SetDeleter
{
[FunctionName(nameof(SetDeleter))]
public static void Run(
[RedisPubSubTrigger(Common.connectionStringSetting, "__keyevent@0__:set")] string key,
[Redis(Common.connectionStringSetting, "DEL")] out string[] arguments,
ILogger logger)
{
logger.LogInformation($"Deleting recently SET key '{key}'");
arguments = new string[] { key };
}
}
}
```


The following example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

```
package com.function.RedisOutputBinding;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class SetDeleter {
@FunctionName("SetDeleter")
@RedisOutput(
name = "value",
connection = "redisConnectionString",
command = "DEL")
public String run(
@RedisPubSubTrigger(
name = "key",
connection = "redisConnectionString",
channel = "__keyevent@0__:set")
String key,
final ExecutionContext context) {
context.getLogger().info("Deleting recently SET key '" + key + "'");
return key;
}
}
```


This example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

The bindings are defined in the `function.json`` file:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisConnectionString",
"command": "DEL",
"name": "$return",
"direction": "out"
}
],
"scriptFile": "index.js"
}
```


This code from the `index.js`

file takes the key from the trigger and returns it to the output binding to delete the cached item.

```
module.exports = async function (context, key) {
context.log("Deleting recently SET key '" + key + "'");
return key;
}
```


This example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

The bindings are defined in this `function.json`

file:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisLocalhost",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisLocalhost",
"command": "DEL",
"name": "retVal",
"direction": "out"
}
],
"scriptFile": "run.ps1"
}
```


This code from the `run.ps1`

file takes the key from the trigger and passes it to the output binding to delete the cached item.

```
param($key, $TriggerMetadata)
Write-Host "Deleting recently SET key '$key'"
Push-OutputBinding -Name retVal -Value $key
```


This example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

The bindings are defined in this `function.json`

file:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisLocalhost",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisLocalhost",
"command": "DEL",
"name": "$return",
"direction": "out"
}
],
"scriptFile": "__init__.py"
}
```


This code from the `__init__.py`

file takes the key from the trigger and passes it to the output binding to delete the cached item.

```
import logging
def main(key: str) -> str:
logging.info("Deleting recently SET key '" + key + "'")
return key
```


## Attributes

Note

All commands are supported for this binding.

The way in which you define an output binding parameter depends on whether your C# functions runs [in-process](functions-dotnet-class-library) or in an [isolated worker process](dotnet-isolated-process-guide).

The output binding is defined this way:

| Definition | Example | Description |
|---|---|---|
On an `out` parameter |
`[Redis(<Connection>, <Command>)] out string <Return_Variable>` |
The string variable returned by the method is a key value that the binding uses to execute the command against the specific cache. |

In this case, the type returned by the method is a key value that the binding uses to execute the command against the specific cache.

When your function has multiple output bindings, you can instead apply the binding attribute to the property of a type that is a key value, which the binding uses to execute the command against the specific cache. For more information, see [Multiple output bindings](dotnet-isolated-process-guide#multiple-output-bindings).

Regardless of the C# process mode, the same properties are supported by the output binding attribute:

| Attribute property | Description |
|---|---|
`Connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`Command`

`DEL`

.## Annotations

The `RedisOutput`

annotation supports these properties:

| Property | Description |
|---|---|
`name` |
The name of the specific input binding. |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`command`

`DEL`

.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| Property | Description |
|---|---|
`name` |
The name of the specific input binding. |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`command`

`DEL`

.See the [Example section](#example) for complete examples.

## Usage

The output returns a string, which is the key of the cache entry on which apply the specific command.

There are three types of connections that are allowed from an Azure Functions instance to a Redis Cache in your deployments. For local development, you can also use service principal secrets. Use the `appsettings`

to configure each of the following types of client authentication, assuming the `Connection`

was set to `Redis`

in the function.

Important

For optimal security, your function app should use Microsoft Entra ID with managed identities to authorize requests against your cache, if possible. Authorization by using Microsoft Entra ID and managed identities provides superior security and ease of use over shared access key authorization. For more information about using managed identities with your cache, see [Use Microsoft Entra ID for cache authentication](/en-us/azure/azure-cache-for-redis/cache-azure-active-directory-for-authentication).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-vnet -->

# Tutorial: Integrate Azure Functions with an Azure virtual network by using private endpoints

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This tutorial shows you how to use Azure Functions to connect to resources in an Azure virtual network by using private endpoints. You create a new function app using a new storage account that's locked behind a virtual network by using the Azure portal. The virtual network uses a Service Bus queue trigger.

In this tutorial, you'll:

- Create a function app in the Elastic Premium plan with virtual network integration and private endpoints.
- Create Azure resources, such as the Service Bus
- Lock down your Service Bus behind a private endpoint.
- Deploy a function app that uses both the Service Bus and HTTP triggers.
- Test to see that your function app is secure inside the virtual network.
- Clean up resources.

## Create a function app in a Premium plan

You create a C# function app in an [Elastic Premium plan](functions-premium-plan), which supports networking capabilities such as virtual network integration on create along with serverless scale. This tutorial uses C# and Windows. Other languages and Linux are also supported.

On the Azure portal menu or the

**Home**page, select**Create a resource**.On the

**New**page, select**Compute**>**Function App**.On the

**Basics**page, use the following table to configure the function app settings.Setting Suggested value Description **Subscription**Your subscription Subscription under which this new function app is created. [Resource Group](../azure-resource-manager/management/overview)myResourceGroup Name for the new resource group where you create your function app. **Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

.**Publish**Code Choose to publish code files or a Docker container. **Runtime stack**.NET This tutorial uses .NET. **Version**6 (LTS) This tutorial uses .NET 6.0 running [in the same process as the Functions host](functions-dotnet-class-library).**Region**Preferred region Choose a [region](https://azure.microsoft.com/regions/)near you or near other services that your functions access.**Operating system**Windows This tutorial uses Windows but also works for Linux. [Plan](functions-scale)Functions Premium Hosting plan that defines how resources are allocated to your function app. By default, when you select **Premium**, a new App Service plan is created. The default**Sku and size**is**EP1**, where*EP*stands for*elastic premium*. For more information, see the list of[Premium SKUs](functions-premium-plan#available-instance-skus).

When you run JavaScript functions on a Premium plan, choose an instance that has fewer vCPUs. For more information, see[Choose single-core Premium plans](functions-reference-node#considerations-for-javascript-functions).Select

**Next: Storage**. On the**Storage**page, enter the following settings.Setting Suggested value Description [Storage account](../storage/common/storage-account-create)Globally unique name Create a storage account used by your function app. Storage account names must be between 3 and 24 characters long. They might contain numbers and lowercase letters only. You can also use an existing account that isn't restricted by firewall rules and meets the [storage account requirements](storage-considerations#storage-account-requirements). When you use Functions with a locked down storage account, you need a v2 storage account. This version is the default storage version created when creating a function app with networking capabilities through the Azure portal.Select

**Next: Networking**. On the**Networking**page, enter the following settings.Note

Some of these settings aren't visible until other options are selected.

Setting Suggested value Description **Enable public access**Off Deny public network access blocks all incoming traffic except that comes from private endpoints. **Enable network injection**On The ability to configure your application with virtual network integration at creation appears in the portal window after this option is switched to **On**.**Virtual Network**Create New Select the **Create New**field. In the pop-out screen, provide a name for your virtual network and select**Ok**. Options to restrict inbound and outbound access to your function app on create are displayed. You must explicitly enable virtual network integration in the**Outbound access**portion of the window to restrict outbound access.Enter the following settings for the

**Inbound access**section. This step creates a private endpoint on your function app.Tip

To continue interacting with your function app from the Azure portal, you need to add your local computer to the virtual network. If you don't wish to restrict inbound access, skip this step.

Setting Suggested value Description **Enable private endpoints**On The ability to configure your application with virtual network integration at creation appears in the portal after this option is enabled. **Private endpoint name**myInboundPrivateEndpointName Name that identifies your new function app private endpoint. **Inbound subnet**Create New This option creates a new subnet for your inbound private endpoint. Multiple private endpoints might be added to a singular subnet. Provide a **Subnet Name**. The**Subnet Address Block**might be left at the default value. Select**Ok**. To learn more about subnet sizing, see[Subnets](functions-networking-options#subnets).**DNS**Azure Private DNS Zone This value indicates which DNS server your private endpoint uses. In most cases if you're working within Azure, Azure Private DNS Zone is the DNS zone you should use as using **Manual**for custom DNS zones have increased complexity.Enter the following settings for the

**Outbound access**section. This step integrates your function app with a virtual network on creation. It also exposes options to create private endpoints on your storage account and restrict your storage account from network access on create. When function app is virtual network integrated, all outbound traffic by default goes[through the virtual network](../app-service/overview-vnet-integration#how-regional-virtual-network-integration-works).Setting Suggested value Description **Enable VNet Integration**On This setting integrates your function app with a virtual network on create and direct all outbound traffic through the virtual network. **Outbound subnet**Create new This setting creates a new subnet for your function app's virtual network integration. A function app can only be virtual network integrated with an empty subnet. Provide a **Subnet Name**. The**Subnet Address Block**might be left at the default value. Select**Ok**. The option to create**Storage private endpoints**is displayed. To use your function app with virtual networks, you need to join it to a subnet.Enter the following settings for the

**Storage private endpoint**section. This step creates private endpoints for the blob, queue, file, and table endpoints on your storage account on create. This approach effectively integrates your storage account with the virtual network.Setting Suggested value Description **Add storage private endpoint**On The ability to configure your application with virtual network integration at creation is displayed in the portal after this option is enabled. **Private endpoint name**myInboundPrivateEndpointName Name that identifies your storage account private endpoint. **Private endpoint subnet**Create New This setting creates a new subnet for your inbound private endpoint on the storage account. Multiple private endpoints might be added to a singular subnet. Provide a **Subnet Name**. The**Subnet Address Block**might be left at the default value. Select**Ok**.**DNS**Azure Private DNS Zone This value indicates which DNS server your private endpoint uses. In most cases if you're working within Azure, Azure Private DNS Zone is the DNS zone you should use as using **Manual**for custom DNS zones will have increased complexity.Select

**Next: Monitoring**. On the**Monitoring**page, enter the following settings.Setting Suggested value Description [Application Insights](functions-monitoring)Default Create an Application Insights resource of the same app name in the nearest supported region. Expand this setting if you need to change the **New resource name**or store your data in a different**Location**in an[Azure geography](https://azure.microsoft.com/global-infrastructure/geographies/).Select

**Review + create**to review the app configuration selections.On the

**Review + create**page, review your settings. Then select**Create**to create and deploy the function app.In the upper-right corner of the portal, select the

**Notifications**icon and watch for the**Deployment succeeded**message.Select

**Go to resource**to view your new function app. You can also select**Pin to dashboard**. Pinning makes it easier to return to this function app resource from your dashboard.

Congratulations! You successfully created your premium function app.

Note

Some deployments might occasionally fail to create the private endpoints in the storage account with the error `StorageAccountOperationInProgress`

. This failure occurs even though the function app itself gets created successfully. When you encounter such an error, delete the function app and retry the operation. You can instead create the private endpoints on the storage account manually.

### Create a Service Bus

Next, you create a Service Bus instance that is used to test the functionality of your function app's network capabilities in this tutorial.

On the Azure portal menu or the

**Home**page, select**Create a resource**.On the

**New**page, search for*Service Bus*. Then select**Create**.On the

**Basics**tab, use the following table to configure the Service Bus settings. All other settings can use the default values.Setting Suggested value Description **Subscription**Your subscription The subscription in which your resources are created. [Resource group](../azure-resource-manager/management/overview)myResourceGroup The resource group you created with your function app. **Namespace name**myServiceBus The name of the Service Bus instance for which the private endpoint is enabled. [Location](https://azure.microsoft.com/regions/)myFunctionRegion The region where you created your function app. **Pricing tier**Premium Choose this tier to use private endpoints with Azure Service Bus. Select

**Review + create**. After validation finishes, select**Create**.

## Lock down your Service Bus

Create the private endpoint to lock down your Service Bus:

In your new Service Bus, in the menu on the left, select

**Networking**.On the

**Private endpoint connections**tab, select**Private endpoint**.On the

**Basics**tab, use the private endpoint settings shown in the following table.Setting Suggested value Description **Subscription**Your subscription The subscription in which your resources are created. [Resource group](../azure-resource-manager/management/overview)myResourceGroup The resource group you created with your function app. **Name**sb-endpoint The name of the private endpoint for the service bus. [Region](https://azure.microsoft.com/regions/)myFunctionRegion The region where you created your storage account. On the

**Resource**tab, use the private endpoint settings shown in the following table.Setting Suggested value Description **Subscription**Your subscription The subscription under which your resources are created. **Resource type**Microsoft.ServiceBus/namespaces The resource type for the Service Bus. **Resource**myServiceBus The Service Bus you created earlier in the tutorial. **Target subresource**namespace The private endpoint that is used for the namespace from the Service Bus. On the

**Virtual Network**tab, for the**Subnet**setting, choose**default**.Select

**Review + create**. After validation finishes, select**Create**.After the private endpoint is created, return to the

**Networking**section of your Service Bus namespace and check the**Public Access**tab.Ensure

**Selected networks**is selected.Select

**+ Add existing virtual network**to add the recently created virtual network.On the

**Add networks**tab, use the network settings from the following table:Setting Suggested value Description **Subscription**Your subscription The subscription under which your resources are created. **Virtual networks**myVirtualNet The name of the virtual network to which your function app connects. **Subnets**functions The name of the subnet to which your function app connects. Select

**Add your client IP address**to give your current client IP access to the namespace.Note

Allowing your client IP address is necessary to enable the Azure portal to

[publish messages to the queue later in this tutorial](#test-your-locked-down-function-app).Select

**Enable**to enable the service endpoint.Select

**Add**to add the selected virtual network and subnet to the firewall rules for the Service Bus.Select

**Save**to save the updated firewall rules.

Resources in the virtual network can now communicate with the Service Bus using the private endpoint.

## Create a queue

Create the queue where your Azure Functions Service Bus trigger gets events:

In your Service Bus, in the menu on the left, select

**Queues**.Select

**Queue**. For the purposes of this tutorial, provide the name*queue*as the name of the new queue.Select

**Create**.

Important

This tutorial currently shows you how to connect to Service Bus using a connection string, which requires you to handle a share secret. For improved security, you should instead use managed identities when connecting to Service Bus from your app. For more information, see [Identity-based connections](functions-bindings-service-bus-trigger?tabs=extensionv5#identity-based-connections) in the Service Bus binding reference article.

## Get a Service Bus connection string

In your Service Bus, in the menu on the left, select

**Shared access policies**.Select

**RootManageSharedAccessKey**. Copy and save the**Primary Connection String**. You need this connection string when you configure the app settings.

## Configure your function app settings

In your function app, in the menu on the left, select

**Configuration**.To use your function app with virtual networks and service bus, update the app settings shown in the following table. To add or edit a setting, select

**+ New application setting**or the**Edit**icon in the rightmost column of the app settings table. When you finish, select**Save**.Setting Suggested value Description **SERVICEBUS_CONNECTION**myServiceBusConnectionString Create this app setting for the connection string of your Service Bus. This storage connection string is from the [Get a Service Bus connection string](#get-a-service-bus-connection-string)section.**WEBSITE_CONTENTOVERVNET**1 Create this app setting. A value of 1 enables your function app to scale when your storage account is restricted to a virtual network. Since you're using an Elastic Premium hosting plan, In the

**Configuration**view, select the**Function runtime settings**tab. Set**Runtime Scale Monitoring**to**On**. Then select**Save**. Runtime-driven scaling allows you to connect non-HTTP trigger functions to services that run inside your virtual network.

Note

Runtime scaling isn't needed for function apps hosted in a Dedicated App Service plan.

## Deploy a Service Bus trigger and HTTP trigger

Note

Enabling private endpoints on a function app also makes the Source Control Manager (SCM) site publicly inaccessible. The following instructions give deployment directions using the Deployment Center within the function app. Alternatively, use [zip deploy](functions-deployment-technologies#zip-deploy) or [self-hosted](/en-us/azure/devops/pipelines/agents/docker) agents that are deployed into a subnet on the virtual network.

In GitHub, go to the following sample repository. It contains a function app and two functions, an HTTP trigger, and a Service Bus queue trigger.

At the top of the page, select

**Fork**to create a fork of this repository in your own GitHub account or organization.In your function app, in the menu on the left, select

**Deployment Center**. Then select**Settings**.On the

**Settings**tab, use the deployment settings shown in the following table.Setting Suggested value Description **Source**GitHub You should have created a GitHub repository for the sample code in step 2. **Organization**myOrganization The organization your repo is checked into. It's usually your account. **Repository**functions-vnet-tutorial The repository forked from [https://github.com/Azure-Samples/functions-vnet-tutorial](https://github.com/Azure-Samples/functions-vnet-tutorial).**Branch**main The main branch of the repository you created. **Runtime stack**.NET The sample code is in C#. **Version**.NET Core 3.1 The runtime version. Select

**Save**.Your initial deployment might take a few minutes. When your app is successfully deployed, on the

**Logs**tab, you see a**Success (Active)**status message. If necessary, refresh the page.

Congratulations! You successfully deployed your sample function app.

### Test your locked-down function app

In your function app, in the menu on the left, select

**Functions**.Select

**ServiceBusQueueTrigger**.In the menu on the left, select

**Monitor**.

You see that you can't monitor your app. Your browser doesn't have access to the virtual network, so it can't directly access resources within the virtual network.

Here's an alternative way to monitor your function by using Application Insights:

In your function app, in the menu on the left, select

**Application Insights**. Then select**View Application Insights data**.In the menu on the left, select

**Live metrics**.Open a new tab. In your Service Bus, in the menu on the left, select

**Queues**.Select your queue.

In the menu on the left, select

**Service Bus Explorer**. Under**Send**, for**Content Type**, choose**Text/Plain**. Then enter a message.Select

**Send**to send the message.On the

**Live metrics**tab, you should see that your Service Bus queue trigger fired. If it hasn't, resend the message from**Service Bus Explorer**.

Congratulations! You successfully tested your function app setup with private endpoints.

## Understand private DNS zones

You used a private endpoint to connect to Azure resources. You're connecting to a private IP address instead of the public endpoint. Existing Azure services are configured to use an existing DNS to connect to the public endpoint. You must override the DNS configuration to connect to the private endpoint.

A private DNS zone is created for each Azure resource that was configured with a private endpoint. A DNS record is created for each private IP address associated with the private endpoint.

The following DNS zones were created in this tutorial:

- privatelink.file.core.windows.net
- privatelink.blob.core.windows.net
- privatelink.servicebus.windows.net
- privatelink.azurewebsites.net

## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, you can delete them by deleting the resource group:

From the Azure portal menu or home page, select

**Resource groups**>**myResourceGroup**.On the

**myResourceGroup**pane, make sure that the listed resources are the ones you want to delete.Select

**Delete resource group**. Type**myResourceGroup**in the text box to confirm, and then select**Delete**.

## Next steps

In this tutorial, you created a Premium function app, storage account, and Service Bus. You secured all of these resources behind private endpoints.

Use the following links to learn more Azure Functions networking options and private endpoints:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-table-output -->

# Azure Tables output bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use an Azure Tables output binding to write entities to a table in [Azure Cosmos DB for Table](/en-us/azure/cosmos-db/table/introduction) or [Azure Table Storage](../storage/tables/table-storage-overview).

For information on setup and configuration details, see the [overview](functions-bindings-storage-table)

Note

This output binding only supports creating new entities in a table. If you need to update an existing entity from your function code, instead use an Azure Tables SDK directly.

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Example

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following `MyTableData`

class represents a row of data in the table:

```
public class MyTableData : Azure.Data.Tables.ITableEntity
{
public string Text { get; set; }
public string PartitionKey { get; set; }
public string RowKey { get; set; }
public DateTimeOffset? Timestamp { get; set; }
public ETag ETag { get; set; }
}
```


The following function, which is started by a Queue Storage trigger, writes a new `MyDataTable`

entity to a table named **OutputTable**.

```
[Function("TableFunction")]
[TableOutput("OutputTable", Connection = "AzureWebJobsStorage")]
public static MyTableData Run(
[QueueTrigger("table-items")] string input,
[TableInput("MyTable", "<PartitionKey>", "{queueTrigger}")] MyTableData tableInput,
FunctionContext context)
{
var logger = context.GetLogger("TableFunction");
logger.LogInformation($"PK={tableInput.PartitionKey}, RK={tableInput.RowKey}, Text={tableInput.Text}");
return new MyTableData()
{
PartitionKey = "queue",
RowKey = Guid.NewGuid().ToString(),
Text = $"Output record with rowkey {input} created at {DateTime.Now}"
};
}
```


The following example shows a Java function that uses an HTTP trigger to write a single table row.

```
public class Person {
private String PartitionKey;
private String RowKey;
private String Name;
public String getPartitionKey() {return this.PartitionKey;}
public void setPartitionKey(String key) {this.PartitionKey = key; }
public String getRowKey() {return this.RowKey;}
public void setRowKey(String key) {this.RowKey = key; }
public String getName() {return this.Name;}
public void setName(String name) {this.Name = name; }
}
public class AddPerson {
@FunctionName("addPerson")
public HttpResponseMessage get(
@HttpTrigger(name = "postPerson", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.FUNCTION, route="persons/{partitionKey}/{rowKey}") HttpRequestMessage<Optional<Person>> request,
@BindingName("partitionKey") String partitionKey,
@BindingName("rowKey") String rowKey,
@TableOutput(name="person", partitionKey="{partitionKey}", rowKey = "{rowKey}", tableName="%MyTableName%", connection="MyConnectionString") OutputBinding<Person> person,
final ExecutionContext context) {
Person outPerson = new Person();
outPerson.setPartitionKey(partitionKey);
outPerson.setRowKey(rowKey);
outPerson.setName(request.getBody().get().getName());
person.setValue(outPerson);
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(outPerson)
.build();
}
}
```


The following example shows a Java function that uses an HTTP trigger to write multiple table rows.

```
public class Person {
private String PartitionKey;
private String RowKey;
private String Name;
public String getPartitionKey() {return this.PartitionKey;}
public void setPartitionKey(String key) {this.PartitionKey = key; }
public String getRowKey() {return this.RowKey;}
public void setRowKey(String key) {this.RowKey = key; }
public String getName() {return this.Name;}
public void setName(String name) {this.Name = name; }
}
public class AddPersons {
@FunctionName("addPersons")
public HttpResponseMessage get(
@HttpTrigger(name = "postPersons", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.FUNCTION, route="persons/") HttpRequestMessage<Optional<Person[]>> request,
@TableOutput(name="person", tableName="%MyTableName%", connection="MyConnectionString") OutputBinding<Person[]> persons,
final ExecutionContext context) {
persons.setValue(request.getBody().get());
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(request.getBody().get())
.build();
}
}
```


The following example shows a table output binding that writes multiple table entities.

```
import { app, HttpRequest, HttpResponseInit, InvocationContext, output } from '@azure/functions';
const tableOutput = output.table({
tableName: 'Person',
connection: 'MyStorageConnectionAppSetting',
});
interface PersonEntity {
PartitionKey: string;
RowKey: string;
Name: string;
}
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
const rows: PersonEntity[] = [];
for (let i = 1; i < 10; i++) {
rows.push({
PartitionKey: 'Test',
RowKey: i.toString(),
Name: `Name ${i}`,
});
}
context.extraOutputs.set(tableOutput, rows);
return { status: 201 };
}
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [tableOutput],
handler: httpTrigger1,
});
```


```
const { app, output } = require('@azure/functions');
const tableOutput = output.table({
tableName: 'Person',
connection: 'MyStorageConnectionAppSetting',
});
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [tableOutput],
handler: async (request, context) => {
const rows = [];
for (let i = 1; i < 10; i++) {
rows.push({
PartitionKey: 'Test',
RowKey: i.toString(),
Name: `Name ${i}`,
});
}
context.extraOutputs.set(tableOutput, rows);
return { status: 201 };
},
});
```


The following example demonstrates how to write multiple entities to a table from a function.

Binding configuration in *function.json*:

```
{
"bindings": [
{
"name": "InputData",
"type": "manualTrigger",
"direction": "in"
},
{
"tableName": "Person",
"connection": "MyStorageConnectionAppSetting",
"name": "TableBinding",
"type": "table",
"direction": "out"
}
],
"disabled": false
}
```


PowerShell code in *run.ps1*:

```
param($InputData, $TriggerMetadata)
foreach ($i in 1..10) {
Push-OutputBinding -Name TableBinding -Value @{
PartitionKey = 'Test'
RowKey = "$i"
Name = "Name $i"
}
}
```


The following example demonstrates how to use the Table storage output binding. Configure the `table`

binding in the *function.json* by assigning values to `name`

, `tableName`

, `partitionKey`

, and `connection`

:

The following function generates a unique UUI for the `rowKey`

value and persists the message into Table storage.

```
import logging
import uuid
import json
import azure.functions as func
app = func.FunctionApp()
@app.route(route="table_out_binding")
@app.table_output(arg_name="message",
connection="AzureWebJobsStorage",
table_name="messages")
def table_out_binding(req: func.HttpRequest, message: func.Out[str]):
row_key = str(uuid.uuid4())
data = {
"Name": "Output binding message",
"PartitionKey": "message",
"RowKey": row_key
}
table_json = json.dumps(data)
message.set(table_json)
return table_json
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#table-output).

In [C# class libraries](dotnet-isolated-process-guide), the `TableInputAttribute`

supports the following properties:

| Attribute property | Description |
|---|---|
TableName |
The name of the table to which to write. |
PartitionKey |
The partition key of the table entity to write. |
RowKey |
The row key of the table entity to write. |
Connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the [TableOutput](https://github.com/Azure/azure-functions-java-library/blob/master/src/main/java/com/microsoft/azure/functions/annotation/TableOutput.java/) annotation on parameters to write values into your tables. The attribute supports the following elements:

| Element | Description |
|---|---|
name |
The variable name used in function code that represents the table or entity. |
dataType |
Defines how Functions runtime should treat the parameter value. To learn more, see
|

**tableName****partitionKey****rowKey****connection**[Connections](#connections).## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `output.table()`

method.

| Property | Description |
|---|---|
tableName |
The name of the table to which to write. |
partitionKey |
The partition key of the table entity to write. |
rowKey |
The row key of the table entity to write. |
connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `table` . This property is set automatically when you create the binding in the Azure portal. |
direction |
Must be set to `out` . This property is set automatically when you create the binding in the Azure portal. |
name |
The variable name used in function code that represents the table or entity. Set to `$return` to reference the function return value. |
tableName |
The name of the table to which to write. |
partitionKey |
The partition key of the table entity to write. |
rowKey |
The row key of the table entity to write. |
connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Connections

The `connection`

property is a reference to environment configuration that specifies how the app should connect to your table service. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections)

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

To obtain a connection string for tables in Azure Table storage, follow the steps shown at [Manage storage account access keys](../storage/common/storage-account-keys-manage). To obtain a connection string for tables in Azure Cosmos DB for Table, follow the steps shown at the [Azure Cosmos DB for Table FAQ](/en-us/azure/cosmos-db/table/table-api-faq#what-is-the-connection-string-that-i-need-to-use-to-connect-to-the-api-for-table-).

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here. For example, if you set `connection`

to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage". If you leave `connection`

empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`

.

### Identity-based connections

If you're using [the Tables API extension](functions-bindings-storage-table#table-api-extension), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). This only applies when accessing tables in Azure Storage. To use an identity, you define settings under a common prefix that maps to the `connection`

property in the trigger and binding configuration.

If you're setting `connection`

to "AzureWebJobsStorage", see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity). For all other connections, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Table Service URI | `<CONNECTION_NAME_PREFIX>__tableServiceUri` 1 |
The data plane URI of the Azure Storage table service to which you're connecting, using the HTTPS scheme. | https://<storage_account_name>.table.core.windows.net |

1 `<CONNECTION_NAME_PREFIX>__serviceUri`

can be used as an alias. If both forms are provided, the `tableServiceUri`

form is used. The `serviceUri`

form can't be used when the overall connection configuration is to be used across blobs, queues, and/or tables.

Other properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

The `serviceUri`

form can't be used when the overall connection configuration is to be used across blobs, queues, and/or tables in Azure Storage. The URI can only designate the table service. As an alternative, you can provide a URI specifically for each service under the same prefix, allowing a single connection to be used.

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You'll need to create a role assignment that provides access to your Azure Storage table service at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The following table shows built-in roles that are recommended when using the Azure Tables extension against Azure Storage in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles (Azure Storage1) |
|---|---|
| Input binding |
|

[Storage Table Data Contributor](../role-based-access-control/built-in-roles#storage-table-data-contributor)1 If your app is instead connecting to tables in Azure Cosmos DB for Table, using an identity isn't supported and the connection must use a connection string.

## Usage

The usage of the binding depends on the extension package version, and the C# modality used in your function app, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see usage details for the mode and version.

When you want the function to write to a single entity, the Azure Tables output binding can bind to the following types:

| Type | Description |
|---|---|
| A JSON serializable type that implements [ITableEntity] | Functions attempts to serialize a plain-old CLR object (POCO) type as the entity. The type must implement [ITableEntity] or have a string `RowKey` property and a string `PartitionKey` property. |

When you want the function to write to multiple entities, the Azure Tables output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single entity types |
An array containing multiple entities. Each entry represents one entity. |

For other output scenarios, create and use a [TableClient](/en-us/dotnet/api/azure.data.tables.tableclient) with other types from [Azure.Data.Tables](/en-us/dotnet/api/azure.data.tables) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

There are two options for outputting a Table storage row from a function by using the [TableStorageOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.tableoutput) annotation:

| Options | Description |
|---|---|
Return value |
By applying the annotation to the function itself, the return value of the function persists as a Table storage row. |
Imperative |
To explicitly set the table row, apply the annotation to a specific parameter of the type
`OutputBinding<T>` |

`T`

includes the `PartitionKey`

and `RowKey`

properties. You can accompany these properties by implementing `ITableEntity`

or inheriting `TableEntity`

.To write to table data, use the `Push-OutputBinding`

cmdlet, set the `-Name TableBinding`

parameter and `-Value`

parameter equal to the row data. See the [PowerShell example](#example) for more detail.

There are two options for outputting a Table storage row message from a function:

| Options | Description |
|---|---|
Return value |
Set the `name` property in function.json to `$return` . With this configuration, the function's return value persists as a Table storage row. |
Imperative |
Pass a value to the
`set` is persisted as table row. |

For specific usage details, see [Example](#example).

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Table |
|

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-custom-handlers -->

# Azure Functions custom handlers

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions executes your app code by using language-specific handlers. These language-specific handlers allow Functions to support [most key languages](supported-languages) by default. However, you might need to run code in another language or package.

Custom handlers are lightweight web servers that receive events from the Azure Functions host process. You can use custom handlers to deploy to Azure Functions any code project that supports HTTP primitives.

Custom handlers are best suited for situations where you want to:

- Implement a function app in a language that's not currently offered out-of-the-box, such as Go or Rust.
- Implement a function app in a runtime that's not currently featured by default, such as Deno.
[Deploy a server](#deploy-self-hosted-mcp-servers)built with the standard MCP SDKs to Azure Functions.

With custom handlers, you can use [triggers and input and output bindings](functions-triggers-bindings) via [extension bundles](functions-bindings-register).

Get started with Azure Functions custom handlers with [quickstarts in Go and Rust](create-first-function-vs-code-other).

## Overview

The following diagram shows the relationship between the Functions host and a web server implemented as a custom handler.

- Each event triggers a request sent to the Functions host. An event is any trigger that Azure Functions supports.
- The Functions host then issues a
[request payload](#request-payload)to the web server. The payload holds trigger and input binding data and other metadata for the function. - The web server executes the individual function, and returns a
[response payload](#response-payload)to the Functions host. - The Functions host passes data from the response to the function's output bindings for processing.

An Azure Functions app implemented as a custom handler must configure the *host.json*, *local.settings.json*, and *function.json* files according to a few conventions.

## Deploy self-hosted MCP servers

Custom handlers also enables you to host MCP servers that you build by using official MCP SDKs in Azure Functions. Custom handlers provides a simple and streamlined experience for hosting your MCP servers in Azure. For more information, see [Self-hosted remote MCP server on Azure Functions](self-hosted-mcp-servers).

Note

The ability to have Azure Functions host MCP servers you create using official MCP SDKs is currently in preview.

## Application structure

To implement a custom handler, your application needs the following aspects:

- A
*host.json*file at the root of your app - A
*local.settings.json*file at the root of your app - A
*function.json*file for each function (inside a folder that matches the function name) - A command, script, or executable that runs a web server

The following diagram shows how these files look on the file system for a function named "MyQueueFunction" and a custom handler executable named *handler.exe*.

```
| /MyQueueFunction
| function.json
|
| host.json
| local.settings.json
| handler.exe
```


### Configuration

You configure the application through the *host.json* and *local.settings.json* files.

#### host.json

*host.json* directs the Functions host where to send requests by pointing to a web server that can process HTTP events.

Define a custom handler by configuring the *host.json* file with details on how to run the web server through the `customHandler`

section.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
}
}
}
```


The `customHandler`

section points to a target as defined by the `defaultExecutablePath`

. The execution target can be a command, executable, or file where the web server is implemented.

Use the `arguments`

array to pass any arguments to the executable. Arguments support expansion of environment variables (application settings) by using `%%`

notation.

You can also change the working directory used by the executable with `workingDirectory`

.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "app/handler.exe",
"arguments": [
"--database-connection-string",
"%DATABASE_CONNECTION_STRING%"
],
"workingDirectory": "app"
}
}
}
```


##### Bindings support

Standard triggers along with input and output bindings are available by referencing [extension bundles](functions-bindings-register) in your *host.json* file.

#### local.settings.json

*local.settings.json* defines application settings used when running the function app locally. Because it might contain secrets, exclude *local.settings.json* from source control. In Azure, use application settings instead.

For custom handlers, set `FUNCTIONS_WORKER_RUNTIME`

to `Custom`

in *local.settings.json*.

```
{
"IsEncrypted": false,
"Values": {
"FUNCTIONS_WORKER_RUNTIME": "Custom"
}
}
```


### Function metadata

When you use a custom handler, the *function.json* contents are the same as when you define a function in any other context. The only requirement is that you must place *function.json* files in a folder named to match the function name.

The following *function.json* configures a function that has a queue trigger and a queue output binding. Because it's in a folder named *MyQueueFunction*, it defines a function named *MyQueueFunction*.

**MyQueueFunction/function.json**

```
{
"bindings": [
{
"name": "myQueueItem",
"type": "queueTrigger",
"direction": "in",
"queueName": "messages-incoming",
"connection": "AzureWebJobsStorage"
},
{
"name": "$return",
"type": "queue",
"direction": "out",
"queueName": "messages-outgoing",
"connection": "AzureWebJobsStorage"
}
]
}
```


### Request payload

When the Functions host receives a queue message, it sends an HTTP post request to the custom handler with a payload in the body.

The following code shows a sample request payload. The payload includes a JSON structure with two members: `Data`

and `Metadata`

.

The `Data`

member includes keys that match input and trigger names as defined in the bindings array in the *function.json* file.

The `Metadata`

member includes [metadata generated from the event source](functions-bindings-expressions-patterns#trigger-metadata).

```
{
"Data": {
"myQueueItem": "{ message: \"Message sent\" }"
},
"Metadata": {
"DequeueCount": 1,
"ExpirationTime": "2019-10-16T17:58:31+00:00",
"Id": "800ae4b3-bdd2-4c08-badd-f08e5a34b865",
"InsertionTime": "2019-10-09T17:58:31+00:00",
"NextVisibleTime": "2019-10-09T18:08:32+00:00",
"PopReceipt": "AgAAAAMAAAAAAAAAAgtnj8x+1QE=",
"sys": {
"MethodName": "QueueTrigger",
"UtcNow": "2019-10-09T17:58:32.2205399Z",
"RandGuid": "24ad4c06-24ad-4e5b-8294-3da9714877e9"
}
}
}
```


### Response payload

By convention, function responses are formatted as key/value pairs. Supported keys include:

| Data type | Remarks | |
|---|---|---|
`Outputs` |
object | Holds response values as defined by the `bindings` array in function.json.For instance, if a function is configured with a queue output binding named "myQueueOutput", then `Outputs` contains a key named `myQueueOutput` , which the custom handler sets to the messages that it sends to the queue. |
`Logs` |
array | Messages that appear in the Functions invocation logs. When running in Azure, messages appear in Application Insights. |
`ReturnValue` |
string | Used to provide a response when an output is configured as `$return` in the function.json file. |

This table shows an example of a response payload.

```
{
"Outputs": {
"res": {
"body": "Message enqueued"
},
"myQueueOutput": [
"queue message 1",
"queue message 2"
]
},
"Logs": [
"Log message 1",
"Log message 2"
],
"ReturnValue": "{\"hello\":\"world\"}"
}
```


## Examples

You can implement custom handlers in any language that supports receiving HTTP events. The following examples show how to implement a custom handler by using the Go programming language.

### Function with bindings

This example shows a function named `order`

that accepts a `POST`

request with a payload representing a product order. When you post an order to the function, it creates a Queue Storage message and returns an HTTP response.

#### Implementation

In a folder named *order*, the *function.json* file configures the HTTP-triggered function.

**order/function.json**

```
{
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": ["post"]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"type": "queue",
"name": "message",
"direction": "out",
"queueName": "orders",
"connection": "AzureWebJobsStorage"
}
]
}
```


This function is defined as an [HTTP triggered function](functions-bindings-http-webhook-trigger) that returns an [HTTP response](functions-bindings-http-webhook-output) and outputs a [Queue storage](functions-bindings-storage-queue-output) message.

At the root of the app, the *host.json* file is configured to run an executable file named `handler.exe`

(`handler`

in Linux or macOS).

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


This is the HTTP request sent to the Functions runtime.

```
POST http://127.0.0.1:7071/api/order HTTP/1.1
Content-Type: application/json
{
"id": 1005,
"quantity": 2,
"color": "black"
}
```


The Functions runtime sends the following HTTP request to the custom handler:

```
POST http://127.0.0.1:<FUNCTIONS_CUSTOMHANDLER_PORT>/order HTTP/1.1
Content-Type: application/json
{
"Data": {
"req": {
"Url": "http://localhost:7071/api/order",
"Method": "POST",
"Query": "{}",
"Headers": {
"Content-Type": [
"application/json"
]
},
"Params": {},
"Body": "{\"id\":1005,\"quantity\":2,\"color\":\"black\"}"
}
},
"Metadata": {
}
}
```


Note

Some portions of the payload were removed for brevity.

*handler.exe* is the compiled Go custom handler program that runs a web server and responds to function invocation requests from the Functions host.

```
package main
import (
"encoding/json"
"fmt"
"log"
"net/http"
"os"
)
type InvokeRequest struct {
Data map[string]json.RawMessage
Metadata map[string]interface{}
}
type InvokeResponse struct {
Outputs map[string]interface{}
Logs []string
ReturnValue interface{}
}
func orderHandler(w http.ResponseWriter, r *http.Request) {
var invokeRequest InvokeRequest
d := json.NewDecoder(r.Body)
d.Decode(&invokeRequest)
var reqData map[string]interface{}
json.Unmarshal(invokeRequest.Data["req"], &reqData)
outputs := make(map[string]interface{})
outputs["message"] = reqData["Body"]
resData := make(map[string]interface{})
resData["body"] = "Order enqueued"
outputs["res"] = resData
invokeResponse := InvokeResponse{outputs, nil, nil}
responseJson, _ := json.Marshal(invokeResponse)
w.Header().Set("Content-Type", "application/json")
w.Write(responseJson)
}
func main() {
customHandlerPort, exists := os.LookupEnv("FUNCTIONS_CUSTOMHANDLER_PORT")
if !exists {
customHandlerPort = "8080"
}
mux := http.NewServeMux()
mux.HandleFunc("/order", orderHandler)
fmt.Println("Go server Listening on: ", customHandlerPort)
log.Fatal(http.ListenAndServe(":"+customHandlerPort, mux))
}
```


In this example, the custom handler runs a web server to handle HTTP events and listens for requests via the `FUNCTIONS_CUSTOMHANDLER_PORT`

.

Even though the Functions host receives the original HTTP request at `/api/order`

, it invokes the custom handler by using the function name (its folder name). In this example, the function is defined at the path of `/order`

. The host sends the custom handler an HTTP request at the path of `/order`

.

When you send `POST`

requests to this function, the trigger data and function metadata are available via the HTTP request body. You can access the original HTTP request body in the payload's `Data.req.Body`

.

The function's response is formatted into key/value pairs where the `Outputs`

member holds a JSON value where the keys match the outputs as defined in the *function.json* file.

This is an example payload that this handler returns to the Functions host.

```
{
"Outputs": {
"message": "{\"id\":1005,\"quantity\":2,\"color\":\"black\"}",
"res": {
"body": "Order enqueued"
}
},
"Logs": null,
"ReturnValue": null
}
```


By setting the `message`

output equal to the order data that came in from the request, the function outputs that order data to the configured queue. The Functions host also returns the HTTP response configured in `res`

to the caller.

### HTTP-only function

For HTTP-triggered functions with no additional bindings or outputs, you might want your handler to work directly with the HTTP request and response instead of the custom handler [request](#request-payload) and [response](#response-payload) payloads. You can configure this behavior in *host.json* by using the `enableProxyingHttpRequest`

setting, which supports response streaming.

Important

The primary purpose of the custom handlers feature is to enable languages and runtimes that don't currently have first-class support on Azure Functions. While you might be able to run web applications by using custom handlers, Azure Functions isn't a standard reverse proxy. Some components of the HTTP request, such as certain headers and routes, might be restricted. Your application might also experience excessive [cold start](event-driven-scaling#cold-start).

To address these circumstances, consider running your web apps on [Azure App Service](../app-service/overview).

The following example demonstrates how to configure an HTTP-triggered function with no additional bindings or outputs. The scenario implemented in this example features a function named `hello`

that accepts a `GET`

or `POST`

.

#### Implementation

In a folder named *hello*, the *function.json* file configures the HTTP-triggered function.

**hello/function.json**

```
{
"bindings": [
{
"type": "httpTrigger",
"authLevel": "function",
"direction": "in",
"name": "req",
"methods": ["get", "post"]
},
{
"type": "http",
"direction": "out",
"name": "res"
}
]
}
```


The function is configured to accept both `GET`

and `POST`

requests, and the result value is provided through an argument named `res`

.

At the root of the app, the *host.json* file is configured to run `handler.exe`

and `enableProxyingHttpRequest`

is set to `true`

.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
},
"enableProxyingHttpRequest": true
}
}
```


The following is a POST request to the Functions host. The Functions host then sends the request to the custom handler.

```
POST http://127.0.0.1:7071/api/hello HTTP/1.1
Content-Type: application/json
{
"message": "Hello World!"
}
```


The *handler.go* file implements a web server and HTTP function.

```
package main
import (
"fmt"
"io/ioutil"
"log"
"net/http"
"os"
)
func helloHandler(w http.ResponseWriter, r *http.Request) {
w.Header().Set("Content-Type", "application/json")
if r.Method == "GET" {
w.Write([]byte("hello world"))
} else {
body, _ := ioutil.ReadAll(r.Body)
w.Write(body)
}
}
func main() {
customHandlerPort, exists := os.LookupEnv("FUNCTIONS_CUSTOMHANDLER_PORT")
if !exists {
customHandlerPort = "8080"
}
mux := http.NewServeMux()
mux.HandleFunc("/api/hello", helloHandler)
fmt.Println("Go server Listening on: ", customHandlerPort)
log.Fatal(http.ListenAndServe(":"+customHandlerPort, mux))
}
```


In this example, the custom handler creates a web server to handle HTTP events and listens for requests via the `FUNCTIONS_CUSTOMHANDLER_PORT`

.

`GET`

requests are handled by returning a string, and `POST`

requests have access to the request body.

The route for the order function here is `/api/hello`

, same as the original request.

Note

The `FUNCTIONS_CUSTOMHANDLER_PORT`

isn't the public facing port used to call the function. The Functions host uses this port to call the custom handler.

## Deploying

You can deploy a custom handler to every Azure Functions hosting option. If your handler requires operating system or platform dependencies (such as a language runtime), you might need to use a [custom container](functions-how-to-custom-container).

When you create a function app in Azure for custom handlers, select .NET Core as the stack.

To deploy a custom handler app by using Azure Functions Core Tools, run the following command.

```
func azure functionapp publish $functionAppName
```


Note

Ensure all files required to run your custom handler are in the folder and included in the deployment. If your custom handler is a binary executable or has platform-specific dependencies, ensure these files match the target deployment platform.

## Restrictions

- The custom handler web server needs to start within 60 seconds.

## Samples

For examples of how to implement functions in a variety of different languages, see the [custom handler samples GitHub repo](https://github.com/Azure-Samples/functions-custom-handlers).

## Troubleshooting and support

### Trace logging

If your custom handler process fails to start or if it has problems communicating with the Functions host, increase the function app's log level to `Trace`

to see more diagnostic messages from the host.

To change the function app's default log level, configure the `logLevel`

setting in the `logging`

section of *host.json*.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
}
},
"logging": {
"logLevel": {
"default": "Trace"
}
}
}
```


The Functions host outputs extra log messages, including information related to the custom handler process. Use the logs to investigate problems starting your custom handler process or invoking functions in your custom handler.

Locally, logs are printed to the console.

In Azure, [query Application Insights traces](analyze-telemetry-data#query-telemetry-data) to view the log messages. If your app produces a high volume of logs, only a subset of log messages are sent to Application Insights. [Disable sampling](configure-monitoring#configure-sampling) to ensure all messages are logged.

### Test custom handler in isolation

Custom handler apps are web server processes, so it might be helpful to start them on their own and test function invocations by sending mock [HTTP requests](#request-payload). For sending HTTP requests with payloads, make sure to choose a tool that keeps your data secure. For more information, see [HTTP test tools](functions-develop-local#http-test-tools).

You can also use this strategy in your CI/CD pipelines to run automated tests on your custom handler.

### Execution environment

Custom handlers run in the same environment as a typical Azure Functions app. Test your handler to ensure the environment contains all the dependencies it needs to run. For apps that require additional dependencies, you might need to run them by using a [custom container image](functions-how-to-custom-container) hosted on Azure Functions [Premium plan](functions-premium-plan).

### Get support

If you need help on a function app with custom handlers, you can submit a request through regular support channels. However, due to the wide variety of possible languages used to build custom handlers apps, support isn't unlimited.

Support is available if the Functions host has problems starting or communicating with the custom handler process. For problems specific to the inner workings of your custom handler process, such as issues with the chosen language or framework, our Support Team can't provide assistance in this context.

## Next steps

Get started building an Azure Functions app in Go or Rust with the [custom handlers quickstart](create-first-function-vs-code-other).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-vnet -->

# Tutorial: Integrate Azure Functions with an Azure virtual network by using private endpoints

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This tutorial shows you how to use Azure Functions to connect to resources in an Azure virtual network by using private endpoints. You create a new function app using a new storage account that's locked behind a virtual network by using the Azure portal. The virtual network uses a Service Bus queue trigger.

In this tutorial, you'll:

- Create a function app in the Elastic Premium plan with virtual network integration and private endpoints.
- Create Azure resources, such as the Service Bus
- Lock down your Service Bus behind a private endpoint.
- Deploy a function app that uses both the Service Bus and HTTP triggers.
- Test to see that your function app is secure inside the virtual network.
- Clean up resources.

## Create a function app in a Premium plan

You create a C# function app in an [Elastic Premium plan](functions-premium-plan), which supports networking capabilities such as virtual network integration on create along with serverless scale. This tutorial uses C# and Windows. Other languages and Linux are also supported.

On the Azure portal menu or the

**Home**page, select**Create a resource**.On the

**New**page, select**Compute**>**Function App**.On the

**Basics**page, use the following table to configure the function app settings.Setting Suggested value Description **Subscription**Your subscription Subscription under which this new function app is created. [Resource Group](../azure-resource-manager/management/overview)myResourceGroup Name for the new resource group where you create your function app. **Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

.**Publish**Code Choose to publish code files or a Docker container. **Runtime stack**.NET This tutorial uses .NET. **Version**6 (LTS) This tutorial uses .NET 6.0 running [in the same process as the Functions host](functions-dotnet-class-library).**Region**Preferred region Choose a [region](https://azure.microsoft.com/regions/)near you or near other services that your functions access.**Operating system**Windows This tutorial uses Windows but also works for Linux. [Plan](functions-scale)Functions Premium Hosting plan that defines how resources are allocated to your function app. By default, when you select **Premium**, a new App Service plan is created. The default**Sku and size**is**EP1**, where*EP*stands for*elastic premium*. For more information, see the list of[Premium SKUs](functions-premium-plan#available-instance-skus).

When you run JavaScript functions on a Premium plan, choose an instance that has fewer vCPUs. For more information, see[Choose single-core Premium plans](functions-reference-node#considerations-for-javascript-functions).Select

**Next: Storage**. On the**Storage**page, enter the following settings.Setting Suggested value Description [Storage account](../storage/common/storage-account-create)Globally unique name Create a storage account used by your function app. Storage account names must be between 3 and 24 characters long. They might contain numbers and lowercase letters only. You can also use an existing account that isn't restricted by firewall rules and meets the [storage account requirements](storage-considerations#storage-account-requirements). When you use Functions with a locked down storage account, you need a v2 storage account. This version is the default storage version created when creating a function app with networking capabilities through the Azure portal.Select

**Next: Networking**. On the**Networking**page, enter the following settings.Note

Some of these settings aren't visible until other options are selected.

Setting Suggested value Description **Enable public access**Off Deny public network access blocks all incoming traffic except that comes from private endpoints. **Enable network injection**On The ability to configure your application with virtual network integration at creation appears in the portal window after this option is switched to **On**.**Virtual Network**Create New Select the **Create New**field. In the pop-out screen, provide a name for your virtual network and select**Ok**. Options to restrict inbound and outbound access to your function app on create are displayed. You must explicitly enable virtual network integration in the**Outbound access**portion of the window to restrict outbound access.Enter the following settings for the

**Inbound access**section. This step creates a private endpoint on your function app.Tip

To continue interacting with your function app from the Azure portal, you need to add your local computer to the virtual network. If you don't wish to restrict inbound access, skip this step.

Setting Suggested value Description **Enable private endpoints**On The ability to configure your application with virtual network integration at creation appears in the portal after this option is enabled. **Private endpoint name**myInboundPrivateEndpointName Name that identifies your new function app private endpoint. **Inbound subnet**Create New This option creates a new subnet for your inbound private endpoint. Multiple private endpoints might be added to a singular subnet. Provide a **Subnet Name**. The**Subnet Address Block**might be left at the default value. Select**Ok**. To learn more about subnet sizing, see[Subnets](functions-networking-options#subnets).**DNS**Azure Private DNS Zone This value indicates which DNS server your private endpoint uses. In most cases if you're working within Azure, Azure Private DNS Zone is the DNS zone you should use as using **Manual**for custom DNS zones have increased complexity.Enter the following settings for the

**Outbound access**section. This step integrates your function app with a virtual network on creation. It also exposes options to create private endpoints on your storage account and restrict your storage account from network access on create. When function app is virtual network integrated, all outbound traffic by default goes[through the virtual network](../app-service/overview-vnet-integration#how-regional-virtual-network-integration-works).Setting Suggested value Description **Enable VNet Integration**On This setting integrates your function app with a virtual network on create and direct all outbound traffic through the virtual network. **Outbound subnet**Create new This setting creates a new subnet for your function app's virtual network integration. A function app can only be virtual network integrated with an empty subnet. Provide a **Subnet Name**. The**Subnet Address Block**might be left at the default value. Select**Ok**. The option to create**Storage private endpoints**is displayed. To use your function app with virtual networks, you need to join it to a subnet.Enter the following settings for the

**Storage private endpoint**section. This step creates private endpoints for the blob, queue, file, and table endpoints on your storage account on create. This approach effectively integrates your storage account with the virtual network.Setting Suggested value Description **Add storage private endpoint**On The ability to configure your application with virtual network integration at creation is displayed in the portal after this option is enabled. **Private endpoint name**myInboundPrivateEndpointName Name that identifies your storage account private endpoint. **Private endpoint subnet**Create New This setting creates a new subnet for your inbound private endpoint on the storage account. Multiple private endpoints might be added to a singular subnet. Provide a **Subnet Name**. The**Subnet Address Block**might be left at the default value. Select**Ok**.**DNS**Azure Private DNS Zone This value indicates which DNS server your private endpoint uses. In most cases if you're working within Azure, Azure Private DNS Zone is the DNS zone you should use as using **Manual**for custom DNS zones will have increased complexity.Select

**Next: Monitoring**. On the**Monitoring**page, enter the following settings.Setting Suggested value Description [Application Insights](functions-monitoring)Default Create an Application Insights resource of the same app name in the nearest supported region. Expand this setting if you need to change the **New resource name**or store your data in a different**Location**in an[Azure geography](https://azure.microsoft.com/global-infrastructure/geographies/).Select

**Review + create**to review the app configuration selections.On the

**Review + create**page, review your settings. Then select**Create**to create and deploy the function app.In the upper-right corner of the portal, select the

**Notifications**icon and watch for the**Deployment succeeded**message.Select

**Go to resource**to view your new function app. You can also select**Pin to dashboard**. Pinning makes it easier to return to this function app resource from your dashboard.

Congratulations! You successfully created your premium function app.

Note

Some deployments might occasionally fail to create the private endpoints in the storage account with the error `StorageAccountOperationInProgress`

. This failure occurs even though the function app itself gets created successfully. When you encounter such an error, delete the function app and retry the operation. You can instead create the private endpoints on the storage account manually.

### Create a Service Bus

Next, you create a Service Bus instance that is used to test the functionality of your function app's network capabilities in this tutorial.

On the Azure portal menu or the

**Home**page, select**Create a resource**.On the

**New**page, search for*Service Bus*. Then select**Create**.On the

**Basics**tab, use the following table to configure the Service Bus settings. All other settings can use the default values.Setting Suggested value Description **Subscription**Your subscription The subscription in which your resources are created. [Resource group](../azure-resource-manager/management/overview)myResourceGroup The resource group you created with your function app. **Namespace name**myServiceBus The name of the Service Bus instance for which the private endpoint is enabled. [Location](https://azure.microsoft.com/regions/)myFunctionRegion The region where you created your function app. **Pricing tier**Premium Choose this tier to use private endpoints with Azure Service Bus. Select

**Review + create**. After validation finishes, select**Create**.

## Lock down your Service Bus

Create the private endpoint to lock down your Service Bus:

In your new Service Bus, in the menu on the left, select

**Networking**.On the

**Private endpoint connections**tab, select**Private endpoint**.On the

**Basics**tab, use the private endpoint settings shown in the following table.Setting Suggested value Description **Subscription**Your subscription The subscription in which your resources are created. [Resource group](../azure-resource-manager/management/overview)myResourceGroup The resource group you created with your function app. **Name**sb-endpoint The name of the private endpoint for the service bus. [Region](https://azure.microsoft.com/regions/)myFunctionRegion The region where you created your storage account. On the

**Resource**tab, use the private endpoint settings shown in the following table.Setting Suggested value Description **Subscription**Your subscription The subscription under which your resources are created. **Resource type**Microsoft.ServiceBus/namespaces The resource type for the Service Bus. **Resource**myServiceBus The Service Bus you created earlier in the tutorial. **Target subresource**namespace The private endpoint that is used for the namespace from the Service Bus. On the

**Virtual Network**tab, for the**Subnet**setting, choose**default**.Select

**Review + create**. After validation finishes, select**Create**.After the private endpoint is created, return to the

**Networking**section of your Service Bus namespace and check the**Public Access**tab.Ensure

**Selected networks**is selected.Select

**+ Add existing virtual network**to add the recently created virtual network.On the

**Add networks**tab, use the network settings from the following table:Setting Suggested value Description **Subscription**Your subscription The subscription under which your resources are created. **Virtual networks**myVirtualNet The name of the virtual network to which your function app connects. **Subnets**functions The name of the subnet to which your function app connects. Select

**Add your client IP address**to give your current client IP access to the namespace.Note

Allowing your client IP address is necessary to enable the Azure portal to

[publish messages to the queue later in this tutorial](#test-your-locked-down-function-app).Select

**Enable**to enable the service endpoint.Select

**Add**to add the selected virtual network and subnet to the firewall rules for the Service Bus.Select

**Save**to save the updated firewall rules.

Resources in the virtual network can now communicate with the Service Bus using the private endpoint.

## Create a queue

Create the queue where your Azure Functions Service Bus trigger gets events:

In your Service Bus, in the menu on the left, select

**Queues**.Select

**Queue**. For the purposes of this tutorial, provide the name*queue*as the name of the new queue.Select

**Create**.

Important

This tutorial currently shows you how to connect to Service Bus using a connection string, which requires you to handle a share secret. For improved security, you should instead use managed identities when connecting to Service Bus from your app. For more information, see [Identity-based connections](functions-bindings-service-bus-trigger?tabs=extensionv5#identity-based-connections) in the Service Bus binding reference article.

## Get a Service Bus connection string

In your Service Bus, in the menu on the left, select

**Shared access policies**.Select

**RootManageSharedAccessKey**. Copy and save the**Primary Connection String**. You need this connection string when you configure the app settings.

## Configure your function app settings

In your function app, in the menu on the left, select

**Configuration**.To use your function app with virtual networks and service bus, update the app settings shown in the following table. To add or edit a setting, select

**+ New application setting**or the**Edit**icon in the rightmost column of the app settings table. When you finish, select**Save**.Setting Suggested value Description **SERVICEBUS_CONNECTION**myServiceBusConnectionString Create this app setting for the connection string of your Service Bus. This storage connection string is from the [Get a Service Bus connection string](#get-a-service-bus-connection-string)section.**WEBSITE_CONTENTOVERVNET**1 Create this app setting. A value of 1 enables your function app to scale when your storage account is restricted to a virtual network. Since you're using an Elastic Premium hosting plan, In the

**Configuration**view, select the**Function runtime settings**tab. Set**Runtime Scale Monitoring**to**On**. Then select**Save**. Runtime-driven scaling allows you to connect non-HTTP trigger functions to services that run inside your virtual network.

Note

Runtime scaling isn't needed for function apps hosted in a Dedicated App Service plan.

## Deploy a Service Bus trigger and HTTP trigger

Note

Enabling private endpoints on a function app also makes the Source Control Manager (SCM) site publicly inaccessible. The following instructions give deployment directions using the Deployment Center within the function app. Alternatively, use [zip deploy](functions-deployment-technologies#zip-deploy) or [self-hosted](/en-us/azure/devops/pipelines/agents/docker) agents that are deployed into a subnet on the virtual network.

In GitHub, go to the following sample repository. It contains a function app and two functions, an HTTP trigger, and a Service Bus queue trigger.

At the top of the page, select

**Fork**to create a fork of this repository in your own GitHub account or organization.In your function app, in the menu on the left, select

**Deployment Center**. Then select**Settings**.On the

**Settings**tab, use the deployment settings shown in the following table.Setting Suggested value Description **Source**GitHub You should have created a GitHub repository for the sample code in step 2. **Organization**myOrganization The organization your repo is checked into. It's usually your account. **Repository**functions-vnet-tutorial The repository forked from [https://github.com/Azure-Samples/functions-vnet-tutorial](https://github.com/Azure-Samples/functions-vnet-tutorial).**Branch**main The main branch of the repository you created. **Runtime stack**.NET The sample code is in C#. **Version**.NET Core 3.1 The runtime version. Select

**Save**.Your initial deployment might take a few minutes. When your app is successfully deployed, on the

**Logs**tab, you see a**Success (Active)**status message. If necessary, refresh the page.

Congratulations! You successfully deployed your sample function app.

### Test your locked-down function app

In your function app, in the menu on the left, select

**Functions**.Select

**ServiceBusQueueTrigger**.In the menu on the left, select

**Monitor**.

You see that you can't monitor your app. Your browser doesn't have access to the virtual network, so it can't directly access resources within the virtual network.

Here's an alternative way to monitor your function by using Application Insights:

In your function app, in the menu on the left, select

**Application Insights**. Then select**View Application Insights data**.In the menu on the left, select

**Live metrics**.Open a new tab. In your Service Bus, in the menu on the left, select

**Queues**.Select your queue.

In the menu on the left, select

**Service Bus Explorer**. Under**Send**, for**Content Type**, choose**Text/Plain**. Then enter a message.Select

**Send**to send the message.On the

**Live metrics**tab, you should see that your Service Bus queue trigger fired. If it hasn't, resend the message from**Service Bus Explorer**.

Congratulations! You successfully tested your function app setup with private endpoints.

## Understand private DNS zones

You used a private endpoint to connect to Azure resources. You're connecting to a private IP address instead of the public endpoint. Existing Azure services are configured to use an existing DNS to connect to the public endpoint. You must override the DNS configuration to connect to the private endpoint.

A private DNS zone is created for each Azure resource that was configured with a private endpoint. A DNS record is created for each private IP address associated with the private endpoint.

The following DNS zones were created in this tutorial:

- privatelink.file.core.windows.net
- privatelink.blob.core.windows.net
- privatelink.servicebus.windows.net
- privatelink.azurewebsites.net

## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, you can delete them by deleting the resource group:

From the Azure portal menu or home page, select

**Resource groups**>**myResourceGroup**.On the

**myResourceGroup**pane, make sure that the listed resources are the ones you want to delete.Select

**Delete resource group**. Type**myResourceGroup**in the text box to confirm, and then select**Delete**.

## Next steps

In this tutorial, you created a Premium function app, storage account, and Service Bus. You secured all of these resources behind private endpoints.

Use the following links to learn more Azure Functions networking options and private endpoints:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-output -->

# Azure Cache for Redis output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Cache for Redis output bindings lets you change the keys in a cache based on a set of available trigger on the cache.

For information on setup and configuration details, see the [overview](functions-bindings-cache).

## Scope of availability for functions bindings

| Binding Type | Azure Managed Redis | Azure Cache for Redis |
|---|---|---|
| Output | Yes | Yes |

Important

When using Azure Managed Redis or the Enterprise tiers of Azure Cache for Redis, use port 10000 rather than port 6380 or 6379.

Important

The Node.js v4 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Important

The Python v2 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v2 model works, refer to the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

## Example

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

The following example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

Important

For .NET functions, using the *isolated worker* model is recommended over the *in-process* model. For a comparison of the *in-process* and *isolated worker* models, see differences between the *isolated worker* model and the *in-process* model for .NET on Azure Functions.

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisOutputBinding
{
internal class SetDeleter
{
[Function(nameof(SetDeleter))]
[RedisOutput(Common.connectionString, "DEL")]
public static string Run(
[RedisPubSubTrigger(Common.connectionString, "__keyevent@0__:set")] string key,
ILogger logger)
{
logger.LogInformation($"Deleting recently SET key '{key}'");
return key;
}
}
}
```


```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.WebJobs.Extensions.Redis.Samples.RedisOutputBinding
{
internal class SetDeleter
{
[FunctionName(nameof(SetDeleter))]
public static void Run(
[RedisPubSubTrigger(Common.connectionStringSetting, "__keyevent@0__:set")] string key,
[Redis(Common.connectionStringSetting, "DEL")] out string[] arguments,
ILogger logger)
{
logger.LogInformation($"Deleting recently SET key '{key}'");
arguments = new string[] { key };
}
}
}
```


The following example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

```
package com.function.RedisOutputBinding;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class SetDeleter {
@FunctionName("SetDeleter")
@RedisOutput(
name = "value",
connection = "redisConnectionString",
command = "DEL")
public String run(
@RedisPubSubTrigger(
name = "key",
connection = "redisConnectionString",
channel = "__keyevent@0__:set")
String key,
final ExecutionContext context) {
context.getLogger().info("Deleting recently SET key '" + key + "'");
return key;
}
}
```


This example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

The bindings are defined in the `function.json`` file:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisConnectionString",
"command": "DEL",
"name": "$return",
"direction": "out"
}
],
"scriptFile": "index.js"
}
```


This code from the `index.js`

file takes the key from the trigger and returns it to the output binding to delete the cached item.

```
module.exports = async function (context, key) {
context.log("Deleting recently SET key '" + key + "'");
return key;
}
```


This example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

The bindings are defined in this `function.json`

file:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisLocalhost",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisLocalhost",
"command": "DEL",
"name": "retVal",
"direction": "out"
}
],
"scriptFile": "run.ps1"
}
```


This code from the `run.ps1`

file takes the key from the trigger and passes it to the output binding to delete the cached item.

```
param($key, $TriggerMetadata)
Write-Host "Deleting recently SET key '$key'"
Push-OutputBinding -Name retVal -Value $key
```


This example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

The bindings are defined in this `function.json`

file:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisLocalhost",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisLocalhost",
"command": "DEL",
"name": "$return",
"direction": "out"
}
],
"scriptFile": "__init__.py"
}
```


This code from the `__init__.py`

file takes the key from the trigger and passes it to the output binding to delete the cached item.

```
import logging
def main(key: str) -> str:
logging.info("Deleting recently SET key '" + key + "'")
return key
```


## Attributes

Note

All commands are supported for this binding.

The way in which you define an output binding parameter depends on whether your C# functions runs [in-process](functions-dotnet-class-library) or in an [isolated worker process](dotnet-isolated-process-guide).

The output binding is defined this way:

| Definition | Example | Description |
|---|---|---|
On an `out` parameter |
`[Redis(<Connection>, <Command>)] out string <Return_Variable>` |
The string variable returned by the method is a key value that the binding uses to execute the command against the specific cache. |

In this case, the type returned by the method is a key value that the binding uses to execute the command against the specific cache.

When your function has multiple output bindings, you can instead apply the binding attribute to the property of a type that is a key value, which the binding uses to execute the command against the specific cache. For more information, see [Multiple output bindings](dotnet-isolated-process-guide#multiple-output-bindings).

Regardless of the C# process mode, the same properties are supported by the output binding attribute:

| Attribute property | Description |
|---|---|
`Connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`Command`

`DEL`

.## Annotations

The `RedisOutput`

annotation supports these properties:

| Property | Description |
|---|---|
`name` |
The name of the specific input binding. |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`command`

`DEL`

.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| Property | Description |
|---|---|
`name` |
The name of the specific input binding. |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`command`

`DEL`

.See the [Example section](#example) for complete examples.

## Usage

The output returns a string, which is the key of the cache entry on which apply the specific command.

There are three types of connections that are allowed from an Azure Functions instance to a Redis Cache in your deployments. For local development, you can also use service principal secrets. Use the `appsettings`

to configure each of the following types of client authentication, assuming the `Connection`

was set to `Redis`

in the function.

Important

For optimal security, your function app should use Microsoft Entra ID with managed identities to authorize requests against your cache, if possible. Authorization by using Microsoft Entra ID and managed identities provides superior security and ease of use over shared access key authorization. For more information about using managed identities with your cache, see [Use Microsoft Entra ID for cache authentication](/en-us/azure/azure-cache-for-redis/cache-azure-active-directory-for-authentication).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-node-troubleshoot -->

# Troubleshoot Node.js apps in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The content of this article changes based on your choice of the Node.js programming model in the selector at the top of the page. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. Learn more about the differences between v3 and v4 in the [migration guide](functions-node-upgrade-v4).

This article provides a guide for troubleshooting common scenarios in Node.js function apps.

The **Diagnose and solve problems** tab in the [Azure portal](https://portal.azure.com) is a useful resource to monitor and diagnose possible issues related to your application. It also supplies potential solutions to your problems based on the diagnosis. For more information, see [Azure Function app diagnostics](functions-diagnostics).

Another useful resource is the **Logs** tab in the [Azure portal](https://portal.azure.com) for your Application Insights instance so that you can run custom [KQL queries](/en-us/azure/data-explorer/kusto/query/). The following example query shows how to view errors and warnings for your app in the past day:

```
let myAppName = "<your app name>";
let startTime = ago(1d);
let endTime = now();
union traces,requests,exceptions
| where cloud_RoleName =~ myAppName
| where timestamp between (startTime .. endTime)
| where severityLevel > 2
```


If those resources didn't solve your problem, the following sections provide advice for specific application issues:

## No functions found

If you see any of the following errors in your logs:

No HTTP triggers found.


No job functions found. Try making your job classes and methods public. If you're using binding extensions (e.g. Azure Storage, ServiceBus, Timers, etc.) make sure you've called the registration method for the extension(s) in your startup code (e.g. builder.AddAzureStorage(), builder.AddServiceBus(), builder.AddTimers(), etc.).


Try the following fixes:

- When running locally, make sure you're using Azure Functions Core Tools v4.0.5382 or higher.
- When running in Azure:
Make sure you're using

[Azure Functions Runtime Version](functions-versions)4.25 or higher.Make sure you're using Node.js v18 or higher.

Set the app setting

`FUNCTIONS_NODE_BLOCK_ON_ENTRY_POINT_ERROR`

to`true`

. This setting is recommended for all model v4 apps and ensures that all entry point errors are visible in your application insights logs. For more information, see[App settings reference for Azure Functions](functions-app-settings#functions_node_block_on_entry_point_error).Check your function app logs for entry point errors. The following example query shows how to view entry point errors for your app in the past day:

`let myAppName = "<your app name>"; let startTime = ago(1d); let endTime = now(); union traces,requests,exceptions | where cloud_RoleName =~ myAppName | where timestamp between (startTime .. endTime) | where severityLevel > 2 | where message has "entry point"`


- Make sure your app has the
[required folder structure](functions-reference-node?pivots=nodejs-model-v3#folder-structure)with a*host.json*at the root and a folder for each function containing a*function.json*file.

## Undici request is not a constructor

If you get the following error in your function app logs:

System.Private.CoreLib: Exception while executing function: Functions.httpTrigger1. System.Private.CoreLib: Result: Failure Exception: undici_1.Request is not a constructor


Make sure you're using Node.js version 18.x or higher.

## Failed to detect the Azure Functions runtime

If you get the following error in your function app logs:

WARNING: Failed to detect the Azure Functions runtime. Switching "@azure/functions" package to test mode - not all features are supported.


Check your `package.json`

file for a reference to `applicationinsights`

and make sure the version is `^2.7.1`

or higher. After updating the version, run `npm install`


## Get help from Microsoft

You can get more help from Microsoft in one of the following ways:

- Search the known issues in the
[Azure Functions Node.js repository](https://github.com/Azure/azure-functions-nodejs-library/issues). If you don't see your issue mentioned, create a new issue and let us know what has happened. - If you're not able to diagnose your problem using this guide, Microsoft support engineers are available to help diagnose issues with your application. Microsoft offers
[various support plans](https://azure.microsoft.com/support/plans). Create a support ticket in the**Support + troubleshooting**section of your function app page in the[Azure portal](https://portal.azure.com).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-trigger -->

# Dapr Input Bindings trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions can be triggered on a Dapr input binding using the following Dapr events.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).```
[FunctionName("ConsumeMessageFromKafka")]
public static void Run(
// Note: the value of BindingName must match the binding name in components/kafka-bindings.yaml
[DaprBindingTrigger(BindingName = "%KafkaBindingName%")] JObject triggerData,
ILogger log)
{
log.LogInformation("Hello from Kafka!");
log.LogInformation($"Trigger data: {triggerData}");
}
```


Here's the Java code for the Dapr Input Binding trigger:

```
@FunctionName("ConsumeMessageFromKafka")
public String run(
@DaprBindingTrigger(
bindingName = "%KafkaBindingName%")
)
```


Use the `app`

object to register the `daprBindingTrigger`

:

```
const { app, trigger } = require('@azure/functions');
app.generic('ConsumeMessageFromKafka', {
trigger: trigger.generic({
type: 'daprBindingTrigger',
bindingName: "%KafkaBindingName%",
name: "triggerData"
}),
handler: async (request, context) => {
context.log("Node function processed a ConsumeMessageFromKafka request from the Dapr Runtime.");
context.log(context.triggerMetadata.triggerData)
}
});
```


The following example shows Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprBindingTrigger`

:

```
{
"bindings": [
{
"type": "daprBindingTrigger",
"bindingName": "%KafkaBindingName%",
"name": "triggerData",
"direction": "in"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

In code:

```
using namespace System
using namespace Microsoft.Azure.WebJobs
using namespace Microsoft.Extensions.Logging
using namespace Microsoft.Azure.WebJobs.Extensions.Dapr
using namespace Newtonsoft.Json.Linq
param (
$triggerData
)
Write-Host "PowerShell function processed a ConsumeMessageFromKafka request from the Dapr Runtime."
$jsonString = $triggerData | ConvertTo-Json
Write-Host "Trigger data: $jsonString"
```


The following example shows a Dapr Input Binding trigger, which uses the [v2 Python programming model](functions-reference-python). To use the `daprBinding`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="ConsumeMessageFromKafka")
@app.dapr_binding_trigger(arg_name="triggerData", binding_name="%KafkaBindingName%")
def main(triggerData: str) -> None:
logging.info('Python function processed a ConsumeMessageFromKafka request from the Dapr Runtime.')
logging.info('Trigger data: ' + triggerData)
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprBindingTrigger`

to trigger a Dapr input binding, which supports the following properties.

| Parameter | Description |
|---|---|
BindingName |
The name of the Dapr trigger. If not specified, the name of the function is used as the trigger name. |

## Annotations

The `DaprBindingTrigger`

annotation allows you to create a function that gets triggered by the binding component you created.

| Element | Description |
|---|---|
bindingName |
The name of the Dapr binding. |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description |
|---|---|
bindingName |
The name of the binding. |

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description |
|---|---|
bindingName |
The name of the binding. |

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr Input Binding trigger, start by setting up a Dapr input binding component. You can learn more about which component to use and how to set it up in the official Dapr documentation.

To use the `daprBindingTrigger`

in Python v2, set up your project with the correct dependencies.

In your

`requirements.text`

file, add the following line:`azure-functions==1.18.0b3`

In the terminal, install the Python library.

`pip install -r .\requirements.txt`

Modify your

`local.setting.json`

file with the following configuration:`"PYTHON_ISOLATE_WORKER_DEPENDENCIES":1`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-table-output -->

# Azure Tables output bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use an Azure Tables output binding to write entities to a table in [Azure Cosmos DB for Table](/en-us/azure/cosmos-db/table/introduction) or [Azure Table Storage](../storage/tables/table-storage-overview).

For information on setup and configuration details, see the [overview](functions-bindings-storage-table)

Note

This output binding only supports creating new entities in a table. If you need to update an existing entity from your function code, instead use an Azure Tables SDK directly.

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Example

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following `MyTableData`

class represents a row of data in the table:

```
public class MyTableData : Azure.Data.Tables.ITableEntity
{
public string Text { get; set; }
public string PartitionKey { get; set; }
public string RowKey { get; set; }
public DateTimeOffset? Timestamp { get; set; }
public ETag ETag { get; set; }
}
```


The following function, which is started by a Queue Storage trigger, writes a new `MyDataTable`

entity to a table named **OutputTable**.

```
[Function("TableFunction")]
[TableOutput("OutputTable", Connection = "AzureWebJobsStorage")]
public static MyTableData Run(
[QueueTrigger("table-items")] string input,
[TableInput("MyTable", "<PartitionKey>", "{queueTrigger}")] MyTableData tableInput,
FunctionContext context)
{
var logger = context.GetLogger("TableFunction");
logger.LogInformation($"PK={tableInput.PartitionKey}, RK={tableInput.RowKey}, Text={tableInput.Text}");
return new MyTableData()
{
PartitionKey = "queue",
RowKey = Guid.NewGuid().ToString(),
Text = $"Output record with rowkey {input} created at {DateTime.Now}"
};
}
```


The following example shows a Java function that uses an HTTP trigger to write a single table row.

```
public class Person {
private String PartitionKey;
private String RowKey;
private String Name;
public String getPartitionKey() {return this.PartitionKey;}
public void setPartitionKey(String key) {this.PartitionKey = key; }
public String getRowKey() {return this.RowKey;}
public void setRowKey(String key) {this.RowKey = key; }
public String getName() {return this.Name;}
public void setName(String name) {this.Name = name; }
}
public class AddPerson {
@FunctionName("addPerson")
public HttpResponseMessage get(
@HttpTrigger(name = "postPerson", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.FUNCTION, route="persons/{partitionKey}/{rowKey}") HttpRequestMessage<Optional<Person>> request,
@BindingName("partitionKey") String partitionKey,
@BindingName("rowKey") String rowKey,
@TableOutput(name="person", partitionKey="{partitionKey}", rowKey = "{rowKey}", tableName="%MyTableName%", connection="MyConnectionString") OutputBinding<Person> person,
final ExecutionContext context) {
Person outPerson = new Person();
outPerson.setPartitionKey(partitionKey);
outPerson.setRowKey(rowKey);
outPerson.setName(request.getBody().get().getName());
person.setValue(outPerson);
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(outPerson)
.build();
}
}
```


The following example shows a Java function that uses an HTTP trigger to write multiple table rows.

```
public class Person {
private String PartitionKey;
private String RowKey;
private String Name;
public String getPartitionKey() {return this.PartitionKey;}
public void setPartitionKey(String key) {this.PartitionKey = key; }
public String getRowKey() {return this.RowKey;}
public void setRowKey(String key) {this.RowKey = key; }
public String getName() {return this.Name;}
public void setName(String name) {this.Name = name; }
}
public class AddPersons {
@FunctionName("addPersons")
public HttpResponseMessage get(
@HttpTrigger(name = "postPersons", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.FUNCTION, route="persons/") HttpRequestMessage<Optional<Person[]>> request,
@TableOutput(name="person", tableName="%MyTableName%", connection="MyConnectionString") OutputBinding<Person[]> persons,
final ExecutionContext context) {
persons.setValue(request.getBody().get());
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(request.getBody().get())
.build();
}
}
```


The following example shows a table output binding that writes multiple table entities.

```
import { app, HttpRequest, HttpResponseInit, InvocationContext, output } from '@azure/functions';
const tableOutput = output.table({
tableName: 'Person',
connection: 'MyStorageConnectionAppSetting',
});
interface PersonEntity {
PartitionKey: string;
RowKey: string;
Name: string;
}
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
const rows: PersonEntity[] = [];
for (let i = 1; i < 10; i++) {
rows.push({
PartitionKey: 'Test',
RowKey: i.toString(),
Name: `Name ${i}`,
});
}
context.extraOutputs.set(tableOutput, rows);
return { status: 201 };
}
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [tableOutput],
handler: httpTrigger1,
});
```


```
const { app, output } = require('@azure/functions');
const tableOutput = output.table({
tableName: 'Person',
connection: 'MyStorageConnectionAppSetting',
});
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [tableOutput],
handler: async (request, context) => {
const rows = [];
for (let i = 1; i < 10; i++) {
rows.push({
PartitionKey: 'Test',
RowKey: i.toString(),
Name: `Name ${i}`,
});
}
context.extraOutputs.set(tableOutput, rows);
return { status: 201 };
},
});
```


The following example demonstrates how to write multiple entities to a table from a function.

Binding configuration in *function.json*:

```
{
"bindings": [
{
"name": "InputData",
"type": "manualTrigger",
"direction": "in"
},
{
"tableName": "Person",
"connection": "MyStorageConnectionAppSetting",
"name": "TableBinding",
"type": "table",
"direction": "out"
}
],
"disabled": false
}
```


PowerShell code in *run.ps1*:

```
param($InputData, $TriggerMetadata)
foreach ($i in 1..10) {
Push-OutputBinding -Name TableBinding -Value @{
PartitionKey = 'Test'
RowKey = "$i"
Name = "Name $i"
}
}
```


The following example demonstrates how to use the Table storage output binding. Configure the `table`

binding in the *function.json* by assigning values to `name`

, `tableName`

, `partitionKey`

, and `connection`

:

The following function generates a unique UUI for the `rowKey`

value and persists the message into Table storage.

```
import logging
import uuid
import json
import azure.functions as func
app = func.FunctionApp()
@app.route(route="table_out_binding")
@app.table_output(arg_name="message",
connection="AzureWebJobsStorage",
table_name="messages")
def table_out_binding(req: func.HttpRequest, message: func.Out[str]):
row_key = str(uuid.uuid4())
data = {
"Name": "Output binding message",
"PartitionKey": "message",
"RowKey": row_key
}
table_json = json.dumps(data)
message.set(table_json)
return table_json
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#table-output).

In [C# class libraries](dotnet-isolated-process-guide), the `TableInputAttribute`

supports the following properties:

| Attribute property | Description |
|---|---|
TableName |
The name of the table to which to write. |
PartitionKey |
The partition key of the table entity to write. |
RowKey |
The row key of the table entity to write. |
Connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the [TableOutput](https://github.com/Azure/azure-functions-java-library/blob/master/src/main/java/com/microsoft/azure/functions/annotation/TableOutput.java/) annotation on parameters to write values into your tables. The attribute supports the following elements:

| Element | Description |
|---|---|
name |
The variable name used in function code that represents the table or entity. |
dataType |
Defines how Functions runtime should treat the parameter value. To learn more, see
|

**tableName****partitionKey****rowKey****connection**[Connections](#connections).## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `output.table()`

method.

| Property | Description |
|---|---|
tableName |
The name of the table to which to write. |
partitionKey |
The partition key of the table entity to write. |
rowKey |
The row key of the table entity to write. |
connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `table` . This property is set automatically when you create the binding in the Azure portal. |
direction |
Must be set to `out` . This property is set automatically when you create the binding in the Azure portal. |
name |
The variable name used in function code that represents the table or entity. Set to `$return` to reference the function return value. |
tableName |
The name of the table to which to write. |
partitionKey |
The partition key of the table entity to write. |
rowKey |
The row key of the table entity to write. |
connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Connections

The `connection`

property is a reference to environment configuration that specifies how the app should connect to your table service. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections)

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

To obtain a connection string for tables in Azure Table storage, follow the steps shown at [Manage storage account access keys](../storage/common/storage-account-keys-manage). To obtain a connection string for tables in Azure Cosmos DB for Table, follow the steps shown at the [Azure Cosmos DB for Table FAQ](/en-us/azure/cosmos-db/table/table-api-faq#what-is-the-connection-string-that-i-need-to-use-to-connect-to-the-api-for-table-).

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here. For example, if you set `connection`

to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage". If you leave `connection`

empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`

.

### Identity-based connections

If you're using [the Tables API extension](functions-bindings-storage-table#table-api-extension), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). This only applies when accessing tables in Azure Storage. To use an identity, you define settings under a common prefix that maps to the `connection`

property in the trigger and binding configuration.

If you're setting `connection`

to "AzureWebJobsStorage", see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity). For all other connections, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Table Service URI | `<CONNECTION_NAME_PREFIX>__tableServiceUri` 1 |
The data plane URI of the Azure Storage table service to which you're connecting, using the HTTPS scheme. | https://<storage_account_name>.table.core.windows.net |

1 `<CONNECTION_NAME_PREFIX>__serviceUri`

can be used as an alias. If both forms are provided, the `tableServiceUri`

form is used. The `serviceUri`

form can't be used when the overall connection configuration is to be used across blobs, queues, and/or tables.

Other properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

The `serviceUri`

form can't be used when the overall connection configuration is to be used across blobs, queues, and/or tables in Azure Storage. The URI can only designate the table service. As an alternative, you can provide a URI specifically for each service under the same prefix, allowing a single connection to be used.

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You'll need to create a role assignment that provides access to your Azure Storage table service at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The following table shows built-in roles that are recommended when using the Azure Tables extension against Azure Storage in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles (Azure Storage1) |
|---|---|
| Input binding |
|

[Storage Table Data Contributor](../role-based-access-control/built-in-roles#storage-table-data-contributor)1 If your app is instead connecting to tables in Azure Cosmos DB for Table, using an identity isn't supported and the connection must use a connection string.

## Usage

The usage of the binding depends on the extension package version, and the C# modality used in your function app, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see usage details for the mode and version.

When you want the function to write to a single entity, the Azure Tables output binding can bind to the following types:

| Type | Description |
|---|---|
| A JSON serializable type that implements [ITableEntity] | Functions attempts to serialize a plain-old CLR object (POCO) type as the entity. The type must implement [ITableEntity] or have a string `RowKey` property and a string `PartitionKey` property. |

When you want the function to write to multiple entities, the Azure Tables output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single entity types |
An array containing multiple entities. Each entry represents one entity. |

For other output scenarios, create and use a [TableClient](/en-us/dotnet/api/azure.data.tables.tableclient) with other types from [Azure.Data.Tables](/en-us/dotnet/api/azure.data.tables) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

There are two options for outputting a Table storage row from a function by using the [TableStorageOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.tableoutput) annotation:

| Options | Description |
|---|---|
Return value |
By applying the annotation to the function itself, the return value of the function persists as a Table storage row. |
Imperative |
To explicitly set the table row, apply the annotation to a specific parameter of the type
`OutputBinding<T>` |

`T`

includes the `PartitionKey`

and `RowKey`

properties. You can accompany these properties by implementing `ITableEntity`

or inheriting `TableEntity`

.To write to table data, use the `Push-OutputBinding`

cmdlet, set the `-Name TableBinding`

parameter and `-Value`

parameter equal to the row data. See the [PowerShell example](#example) for more detail.

There are two options for outputting a Table storage row message from a function:

| Options | Description |
|---|---|
Return value |
Set the `name` property in function.json to `$return` . With this configuration, the function's return value persists as a Table storage row. |
Imperative |
Pass a value to the
`set` is persisted as table row. |

For specific usage details, see [Example](#example).

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Table |
|
