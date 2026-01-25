---
merged_at: 2026-01-25T15:41:11.640923
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-triggers-python.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-triggers-python -->

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

<!-- DOCUMENTO FUSIONADO: __functions-bindings-rabbitmq-trigger_functions-add-output-binding-storage-queue_d6e460.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-rabbitmq-trigger_functions-add-output-binding-storage-queue-_9a1cb9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-rabbitmq-trigger.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-rabbitmq-trigger -->

# RabbitMQ trigger for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the RabbitMQ trigger to respond to messages from a RabbitMQ queue.

Note

The RabbitMQ bindings are only fully supported on [Elastic Premium](functions-premium-plan) and [Dedicated (App Service)](dedicated-plan) plans. [Flex Consumption](flex-consumption-plan) and [Consumption](consumption-plan) plans aren't yet supported.

RabbitMQ bindings aren't supported by the Azure Functions v1.x runtime.

For information on setup and configuration details, see the [overview](functions-bindings-rabbitmq).

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

```
[Function(nameof(RabbitMQFunction))]
[RabbitMQOutput(QueueName = "destinationQueue", ConnectionStringSetting = "RabbitMQConnection")]
public static string Run([RabbitMQTrigger("queue", ConnectionStringSetting = "RabbitMQConnection")] string item,
FunctionContext context)
{
var logger = context.GetLogger(nameof(RabbitMQFunction));
logger.LogInformation(item);
var message = $"Output message created at {DateTime.Now}";
return message;
}
```


The following Java function uses the `@RabbitMQTrigger`

annotation from the [Java RabbitMQ types](https://mvnrepository.com/artifact/com.microsoft.azure.functions/azure-functions-java-library-rabbitmq) to describe the configuration for a RabbitMQ queue trigger. The function grabs the message placed on the queue and adds it to the logs.

```
@FunctionName("RabbitMQTriggerExample")
public void run(
@RabbitMQTrigger(connectionStringSetting = "rabbitMQConnectionAppSetting", queueName = "queue") String input,
final ExecutionContext context)
{
context.getLogger().info("Java HTTP trigger processed a request." + input);
}
```


The following example shows a RabbitMQ trigger binding in a *function.json* file and a [JavaScript function](functions-reference-node) that uses the binding. The function reads and logs a RabbitMQ message.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"name": "myQueueItem",
"type": "rabbitMQTrigger",
"direction": "in",
"queueName": "queue",
"connectionStringSetting": "rabbitMQConnectionAppSetting"
}
]
}
```


Here's the JavaScript script code:

```
module.exports = async function (context, myQueueItem) {
context.log('JavaScript RabbitMQ trigger function processed work item', myQueueItem);
};
```


The following example demonstrates how to read a RabbitMQ queue message via a trigger.

A RabbitMQ binding is defined in *function.json* where *type* is set to `RabbitMQTrigger`

.

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"name": "myQueueItem",
"type": "rabbitMQTrigger",
"direction": "in",
"queueName": "queue",
"connectionStringSetting": "rabbitMQConnectionAppSetting"
}
]
}
```


```
import logging
import azure.functions as func
def main(myQueueItem) -> None:
logging.info('Python RabbitMQ trigger function processed a queue item: %s', myQueueItem)
```


PowerShell examples aren't currently available.

## Attributes

Both [isolated worker process](dotnet-isolated-process-guide) and [in-process](functions-dotnet-class-library) C# libraries use `RabbitMQTriggerAttribute`

to define the function, where specific properties of the attribute depend on the extension version.

The attribute's constructor accepts these parameters:

| Parameter | Description |
|---|---|
QueueName |
Name of the queue from which to receive messages. |
HostName |
This parameter is no longer supported and is ignored. It will be removed in a future version. |
ConnectionStringSetting |
The name of the app setting that contains the connection string for your RabbitMQ server. This setting only takes an app setting key name, you can't directly set a connection string value. For more information, see
|

**UserNameSetting****PasswordSetting****Port**`5672`

.## Annotations

The `RabbitMQTrigger`

annotation allows you to create a function that runs when a RabbitMQ message is created.

The annotation supports the following configuration options:

| Parameter | Description |
|---|---|
queueName |
Name of the queue from which to receive messages. |
connectionStringSetting |
The name of the app setting that contains the connection string for your RabbitMQ server. This setting only takes an app setting key name, you can't directly set a connection string value. For more information, see
|

**disableCertificateValidation**`true`

indicating that certificate validation should be disabled. Default value is `false`

. Not recommended for production. Does not apply when SSL is disabled.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `RabbitMQTrigger` . |
direction |
Must be set to `in` . |
name |
The name of the variable that represents the queue in function code. |
queueName |
Name of the queue from which to receive messages. |
connectionStringSetting |
The name of the app setting that contains the connection string for your RabbitMQ server. This setting only takes an app setting key name, you can't directly set a connection string value. For more information, see
|

**disableCertificateValidation**`true`

indicating that certificate validation should be disabled. Default value is `false`

. Not recommended for production. Does not apply when SSL is disabled.When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

See the [Example section](#example) for complete examples.

## Usage

The parameter type supported by the RabbitMQ trigger depends on the C# modality used.

The RabbitMQ bindings currently support only string and serializable object types when running in an isolated process.

The queue message is available via `context.bindings.<NAME>`

where `<NAME>`

matches the name defined in function.json. If the payload is JSON, the value is deserialized into an object.

### Connections

Important

The RabbitMQ binding doesn't support Microsoft Entra authentication and managed identities. You can use Azure Key Vault to centrally managed your RabbitMQ connection strings. To learn more, see [Manage Connections](manage-connections).

Starting with version 2.x of the extension, `hostName`

, `userNameSetting`

, and `passwordSetting`

are no longer supported to define a connection to the RabbitMQ server. You must instead use `connectionStringSetting`

.

The `connectionStringSetting`

property can only accept the name of a key-value pair in app settings. You can't directly set a connection string value in the binding.

For example, when you have set `connectionStringSetting`

to `rabbitMQConnection`

in your binding definition, your function app must have an app setting named `rabbitMQConnection`

that returns either a connection value like `amqp://myuser:***@contoso.rabbitmq.example.com:5672`

or an [Azure Key Vault reference](../app-service/app-service-key-vault-references).

When running locally, you must also have the key value for `connectionStringSetting`

defined in your *local.settings.json* file. Otherwise, your app can't connect to the service from your local computer and an error occurs.

### Dead letter queues

Dead letter queues and exchanges can't be controlled or configured from the RabbitMQ trigger. To use dead letter queues, pre-configure the queue used by the trigger in RabbitMQ. Refer to the [RabbitMQ documentation](https://www.rabbitmq.com/dlx.html).

### Enable Runtime Scaling

In order for the RabbitMQ trigger to scale out to multiple instances, the **Runtime Scale Monitoring** setting must be enabled.

In the portal, this setting can be found under **Configuration** > **Function runtime settings** for your function app.


In the Azure CLI, you can enable **Runtime Scale Monitoring** by using this command:

```
az resource update -resource-group <RESOURCE_GROUP> -name <APP_NAME>/config/web \
--set properties.functionsRuntimeScaleMonitoringEnabled=1 \
--resource-type Microsoft.Web/sites
```


### Monitoring a RabbitMQ endpoint

To monitor your queues and exchanges for a certain RabbitMQ endpoint:

- Enable the
[RabbitMQ management plugin](https://www.rabbitmq.com/management.html) - Browse to
`http://{node-hostname}:15672`

and log in with your user name and password.


---

<!-- DOCUMENTO FUSIONADO: functions-add-output-binding-storage-queue-vs.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-output-binding-storage-queue-vs -->

# Connect functions to Azure Storage using Visual Studio

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions lets you connect Azure services and other resources to functions without having to write your own integration code. These *bindings*, which represent both input and output, are declared within the function definition. Data from bindings is provided to the function as parameters. A *trigger* is a special type of input binding. Although a function has only one trigger, it can have multiple input and output bindings. To learn more, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

This article shows you how to use Visual Studio to connect the function you created in the [previous quickstart article](functions-create-your-first-function-visual-studio) to Azure Storage. The output binding that you add to this function writes data from the HTTP request to a message in an Azure Queue storage queue.

Most bindings require a stored connection string that Functions uses to access the bound service. To make it easier, you use the Storage account that you created with your function app. The connection to this account is already stored in an app setting named `AzureWebJobsStorage`

.

## Prerequisites

Before you start this article, you must:

- Complete
[part 1 of the Visual Studio quickstart](functions-create-your-first-function-visual-studio). - Install
[Azure Storage Explorer](https://storageexplorer.com/). Storage Explorer is a tool that you'll use to examine queue messages generated by your output binding. Storage Explorer is supported on macOS, Windows, and Linux-based operating systems. - Sign in to your Azure subscription from Visual Studio.

## Download the function app settings

In the [previous quickstart article](how-to-create-function-vs-code?pivot=programming-language-csharp), you created a function app in Azure along with the required Storage account. The connection string for this account is stored securely in app settings in Azure. In this article, you write messages to a Storage queue in the same account. To connect to your Storage account when running the function locally, you must download app settings to the *local.settings.json* file.

In

**Solution Explorer**, right-click the project and select**Publish**.In the

**Publish**tab under**Hosting**, expand the three dots (**...**) and select**Manage Azure App Service settings**.Under

**AzureWebJobsStorage**, copy the**Remote**string value to**Local**, and then select**OK**.

The storage binding, which uses the `AzureWebJobsStorage`

setting for the connection, can now connect to your Queue storage when running locally.

## Register binding extensions

Because you're using a Queue storage output binding, you need the Storage bindings extension installed before you run the project. Except for HTTP and timer triggers, bindings are implemented as extension packages.

From the

**Tools**menu, select**NuGet Package Manager**>**Package Manager Console**.In the console, run the following

[Install-Package](/en-us/nuget/tools/ps-ref-install-package)command to install the Storage extensions:`Install-Package Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues`


Now, you can add the storage output binding to your project.

## Add an output binding

In a C# project, the bindings are defined as binding attributes on the function method. Specific definitions depend on whether your app runs in-process (C# class library) or in an isolated worker process.

Open the *HttpExample.cs* project file and add the following `MultiResponse`

class:

```
public class MultiResponse
{
[QueueOutput("outqueue",Connection = "AzureWebJobsStorage")]
public string[] Messages { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


The `MultiResponse`

class allows you to write to a storage queue named `outqueue`

and an HTTP success message. Multiple messages could be sent to the queue because the `QueueOutput`

attribute is applied to a string array.

The `Connection`

property sets the connection string for the storage account. In this case, you could omit `Connection`

because you're already using the default storage account.

## Add code that uses the output binding

After the binding is defined, you can use the `name`

of the binding to access it as an attribute in the function signature. By using an output binding, you don't have to use the Azure Storage SDK code for authentication, getting a queue reference, or writing data. The Functions runtime and queue output binding do those tasks for you.

Replace the existing `HttpExample`

class with the following code:

```
[Function("HttpExample")]
public static MultiResponse Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req,
FunctionContext executionContext)
{
var logger = executionContext.GetLogger("HttpExample");
logger.LogInformation("C# HTTP trigger function processed a request.");
var message = "Welcome to Azure Functions!";
var response = req.CreateResponse(HttpStatusCode.OK);
response.Headers.Add("Content-Type", "text/plain; charset=utf-8");
response.WriteString(message);
// Return a response to both HTTP trigger and storage output binding.
return new MultiResponse()
{
// Write a single message.
Messages = new string[] { message },
HttpResponse = response
};
}
}
```


## Run the function locally

To run your function, press

`F5`in Visual Studio. You might need to enable a firewall exception so that the tools can handle HTTP requests. Authorization levels are never enforced when you run a function locally.Copy the URL of your function from the Azure Functions runtime output.

Paste the URL for the HTTP request into your browser's address bar and run the request. The following image shows the response in the browser to the local GET request returned by the function:

To stop debugging, press

`Shift`+`F5`in Visual Studio.

A new queue named `outqueue`

is created in your storage account by the Functions runtime when the output binding is first used. You'll use Storage Explorer to verify that the queue was created along with the new message.

### Connect Storage Explorer to your account

Skip this section if you've already installed Azure Storage Explorer and connected it to your Azure account.

Run the

[Azure Storage Explorer](https://storageexplorer.com/)tool, select the connect icon on the left, and select**Add an account**.In the

**Connect**dialog, choose**Add an Azure account**, choose your**Azure environment**, and then select**Sign in...**.

After you successfully sign in to your account, you see all of the Azure subscriptions associated with your account. Choose your subscription and select **Open Explorer**.

### Examine the output queue

In Storage Explorer, expand the

**Queues**node, and then select the queue named**outqueue**.The queue contains the message that the queue output binding created when you ran the HTTP-triggered function. If you invoked the function with the default

`name`

value of*Azure*, the queue message is*Name passed to the function: Azure*.Run the function again, send another request, and you see a new message in the queue.


Now, it's time to republish the updated function app to Azure.

## Redeploy and verify the updated app

In

**Solution Explorer**, right-click the project and select**Publish**, then choose**Publish**to republish the project to Azure.After deployment completes, you can again use the browser to test the redeployed function. As before, append the query string

`&name=<yourname>`

to the URL.Again

[view the message in the storage queue](#examine-the-output-queue)to verify that the output binding again generates a new message in the queue.

## Clean up resources

Other quickstarts in this collection build upon this quickstart. If you plan to work with subsequent quickstarts, tutorials, or with any of the services you've created in this quickstart, don't clean up the resources.

*Resources* in Azure refer to function apps, functions, storage accounts, and so forth. They're grouped into *resource groups*, and you can delete everything in a group by deleting the group.

You've created resources to complete these quickstarts. You might be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). If you don't need the resources anymore, here's how to delete them:

In the Azure portal, go to the

**Resource group**page.To get to that page from the function app page, select the

**Overview**tab, and then select the link under**Resource group**.To get to that page from the dashboard, select

**Resource groups**, and then select the resource group that you used for this article.In the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**and follow the instructions.Deletion might take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.


## Next steps

You've updated your HTTP triggered function to write data to a Storage queue. To learn more about developing Functions, see [Develop Azure Functions using Visual Studio](functions-develop-vs).

Next, you should enable Application Insights monitoring for your function app:


---

<!-- DOCUMENTO FUSIONADO: __functions-bindings-azure-mysql_functions-bindings-http-webhook_functions-bindi_14a29d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-azure-mysql_functions-bindings-http-webhook.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-azure-mysql.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-mysql -->

# Overview of Azure Database for MySQL bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to work with [Azure Database for MySQL](/en-us/azure/mysql/index) bindings in Azure Functions. Azure Functions supports input bindings, output bindings and trigger bindings in general availability for Azure Database for MySQL

| Action | Type |
|---|---|
| Read data from a database |
|

[Output binding](functions-bindings-azure-mysql-output)[Trigger binding](functions-bindings-azure-mysql-trigger)## Install the extension

The extension NuGet package that you install depends on the C# mode you're using in your function app:

Functions run in an isolated C# worker process. To learn more, see [Guide for running C# Azure functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing [this NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.MySql/1.0.129/).

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.MySql --version 1.0.129
```


## Install the bundle

The extension for Azure Database for MySQL bindings is part of the v4 [extension bundle](extension-bundles). This bundle is specified in your host.json project file.

### Bundle v4.x

You can use the extension bundle by adding or replacing the following code in your host.json file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


## Install the bundle

The extension for Azure Database for MySQL bindings is part of the v4 [extension bundle](extension-bundles). This bundle is specified in your host.json project file.

### Bundle v4.x

You can use the extension bundle by adding or replacing the following code in your host.json file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


## Install the bundle

The extension for Azure Database for MySQL bindings is part of the v4 [extension bundle](extension-bundles). This bundle is specified in your host.json project file.

### Bundle v4.x

You can use the extension bundle by adding or replacing the following code in your host.json file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


## Update packages

You can use the extension bundle with an update to the pom.xml file in your Java Azure Functions project, as shown in the following snippet:

```
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-library-mysql</artifactId>
<version>1.0.2</version>
</dependency>
```


## MySQL connection string

Azure Database for MySQL bindings for Azure Functions have a required property for the connection string. These bindings pass the connection string to the MySql.Data.MySqlClient library and provide support as defined in the [MySqlClient ConnectionString documentation](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html). Notable keywords include:

`server`

: The host on which the server instance is running. The value can be a host name, IPv4 address, or IPv6 address.`uid`

: The MySQL user account to provide for the authentication process.`pwd`

: The password to use for the authentication process.`database`

: The default database for the connection. If no database is specified, the connection has no default database.

## Considerations

- Azure Database for MySQL bindings support version 4.x and later of the Azure Functions runtime.
- You can find source code for the Azure Database for MySQL bindings in
[this GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/src). - These bindings require connectivity to Azure Database for MySQL.
- Output bindings against tables with columns of spatial data types
`GEOMETRY`

,`POINT`

, and`POLYGON`

aren't supported. Data upserts fail.

## Samples

In addition to the samples for C#, Java, JavaScript, PowerShell, and Python available in the [GitHub repository for Azure Database for MySQL bindings](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples), more are available in [Azure Samples](https://github.com/Azure-Samples).


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-http-webhook.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook -->

# Azure Functions HTTP triggers and bindings overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions may be invoked via HTTP requests to build serverless APIs and respond to [webhooks](https://en.wikipedia.org/wiki/Webhook).

| Action | Type |
|---|---|
| Run a function from an HTTP request |
|

[Output binding](functions-bindings-http-webhook-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Http), version 3.x.

Note

An additional extension package is needed for [ASP.NET Core integration in .NET Isolated](dotnet-isolated-process-guide#aspnet-core-integration)

## Install bundle

To be able to use this binding extension in your app, make sure that the *host.json* file in the root of your project contains this `extensionBundle`

reference:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
}
}
```


In this example, the `version`

value of `[4.0.0, 5.0.0)`

instructs the Functions host to use a bundle version that is at least `4.0.0`

but less than `5.0.0`

, which includes all potential versions of 4.x. This notation effectively maintains your app on the latest available minor version of the v4.x extension bundle.

When possible, you should use the latest extension bundle major version and allow the runtime to automatically maintain the latest minor version. You can view the contents of the latest bundle on the [extension bundles release page](https://github.com/Azure/azure-functions-extension-bundles/releases/latest). For more information, see [Azure Functions extension bundles](extension-bundles).

## host.json settings

This section describes the configuration settings available for this binding in version 2.x and later. Settings in the host.json file apply to all functions in a function app instance. For more information about function app configuration settings, see [host.json reference for Azure Functions](functions-host-json).

Note

For a reference of host.json in Functions 1.x, see [host.json reference for Azure Functions 1.x](functions-host-json-v1#http).

```
{
"extensions": {
"http": {
"routePrefix": "api",
"maxOutstandingRequests": 200,
"maxConcurrentRequests": 100,
"dynamicThrottlesEnabled": true,
"hsts": {
"isEnabled": true,
"maxAge": "10"
},
"customHeaders": {
"X-Content-Type-Options": "nosniff"
}
}
}
}
```


| Property | Default | Description | ||||||||||
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| customHeaders | none | Allows you to set custom headers in the HTTP response. The previous example adds the `X-Content-Type-Options` header to the response to avoid content type sniffing. This custom header applies to all HTTP triggered functions in the function app. |
||||||||||
| dynamicThrottlesEnabled | true* |
When enabled, this setting causes the request processing pipeline to periodically check system performance counters like `connections/threads/processes/memory/cpu/etc` and if any of those counters are over a built-in high threshold (80%), requests will be rejected with a `429 "Too Busy"` response until the counter(s) return to normal levels.*The default in a Consumption plan is `true` . The default in the Premium and Dedicated plans is `false` . |
||||||||||
| hsts | not enabled | When `isEnabled` is set to `true` , the
`HstsOptions` class |

| Property | Description |
|---|---|
| excludedHosts | A string array of host names for which the HSTS header isn't added. |
| includeSubDomains | Boolean value that indicates whether the includeSubDomain parameter of the Strict-Transport-Security header is enabled. |
| maxAge | String that defines the max-age parameter of the Strict-Transport-Security header. |
| preload | Boolean that indicates whether the preload parameter of the Strict-Transport-Security header is enabled. |

**The default for a Consumption plan is 100. The default for the Premium and Dedicated plans is unbounded (`-1`

).**The default for a Consumption plan is 200. The default for the Premium and Dedicated plans is unbounded (`-1`

).


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-mobile-apps.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-mobile-apps -->

# Mobile Apps bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

Azure Mobile Apps bindings are only available to Azure Functions 1.x. They are not supported in Azure Functions 2.x and higher.

Important

[Support will end for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1). We highly recommend that you [migrate your apps to version 4.x](migrate-version-1-version-4) for full support.

This article explains how to work with [Azure Mobile Apps](/en-us/previous-versions/azure/app-service-mobile/app-service-mobile-value-prop) bindings in Azure Functions. Azure Functions supports input and output bindings for Mobile Apps.

The Mobile Apps bindings let you read and update data tables in mobile apps.

## Packages - Functions 1.x

Mobile Apps bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.MobileApps](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps) NuGet package, version 1.x. Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.MobileApps/) GitHub repository.

The following table lists how to add support for output binding in each development environment.

| Development environment | To add support in Functions 1.x |
|---|---|
| Local development: C# class library |
|

## Input

The Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function. In C# and F# functions, any changes made to the record are automatically sent back to the table when the function exits successfully.

## Input - example

See the language-specific example:

The following example shows a Mobile Apps input binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function is triggered by a queue message that has a record identifier. The function reads the specified record and modifies its `Text`

property.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"name": "myQueueItem",
"queueName": "myqueue-items",
"connection": "",
"type": "queueTrigger",
"direction": "in"
},
{
"name": "record",
"type": "mobileTable",
"tableName": "MyTable",
"id": "{queueTrigger}",
"connection": "My_MobileApp_Url",
"apiKey": "My_MobileApp_Key",
"direction": "in"
}
]
}
```


The [configuration](#input---configuration) section explains these properties.

Here's the C# script code:

```
#r "Newtonsoft.Json"
using Newtonsoft.Json.Linq;
public static void Run(string myQueueItem, JObject record)
{
if (record != null)
{
record["Text"] = "This has changed.";
}
}
```


## Input - attributes

In [C# class libraries](functions-dotnet-class-library), use the [MobileTable](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) attribute.

For information about attribute properties that you can configure, see [the following configuration section](#input---configuration).

## Input - configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `MobileTable`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to "mobileTable" |
direction |
n/a | Must be set to "in" |
name |
n/a | Name of input parameter in function signature. |
tableName |
TableName |
Name of the mobile app's data table |
id |
Id |
The identifier of the record to retrieve. Can be static or based on the trigger that invokes the function. For example, if you use a queue trigger for your function, then `"id": "{queueTrigger}"` uses the string value of the queue message as the record ID to retrieve. |
connection |
Connection |
The name of an app setting that has the mobile app's URL. The function uses this URL to construct the required REST operations against your mobile app. Create an app setting in your function app that contains the mobile app's URL, then specify the name of the app setting in the `connection` property in your input binding. The URL looks like `https://<appname>.azurewebsites.net` . |
apiKey |
ApiKey |
The name of an app setting that has your mobile app's API key. Provide the API key if you implement an API key in your Node.js mobile app, or implement an API key in your .NET mobile app. To provide the key, create an app setting in your function app that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

Important

Don't share the API key with your mobile app clients. It should only be distributed securely to service-side clients, like Azure Functions. Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository. This safeguards your sensitive information.

## Input - usage

In C# functions, when the record with the specified ID is found, it is passed into the named
[JObject](https://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter. When the record is not found, the parameter value is `null`

.

In JavaScript functions, the record is passed into the `context.bindings.<name>`

object. When the record is not found, the parameter value is `null`

.

In C# and F# functions, any changes you make to the input record (input parameter) are automatically sent back to the table when the function exits successfully. You can't modify a record in JavaScript functions.

## Output

Use the Mobile Apps output binding to write a new record to a Mobile Apps table.

## Output - example

The following example shows a [C# function](functions-dotnet-class-library) that is triggered by a queue message and creates a record in a mobile app table.

```
[FunctionName("MobileAppsOutput")]
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run(
[QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem,
TraceWriter log)
{
return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```


## Output - attributes

In [C# class libraries](functions-dotnet-class-library), use the [MobileTable](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) attribute.

For information about attribute properties that you can configure, see [Output - configuration](#output---configuration). Here's a `MobileTable`

attribute example in a method signature:

```
[FunctionName("MobileAppsOutput")]
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run(
[QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem,
TraceWriter log)
{
...
}
```


## Output - configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `MobileTable`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to "mobileTable" |
direction |
n/a | Must be set to "out" |
name |
n/a | Name of output parameter in function signature. |
tableName |
TableName |
Name of the mobile app's data table |
connection |
MobileAppUriSetting |
The name of an app setting that has the mobile app's URL. The function uses this URL to construct the required REST operations against your mobile app. Create an app setting in your function app that contains the mobile app's URL, then specify the name of the app setting in the `connection` property in your input binding. The URL looks like `https://<appname>.azurewebsites.net` . |
apiKey |
ApiKeySetting |
The name of an app setting that has your mobile app's API key. Provide the API key if you implement an API key in your Node.js mobile app backend, or implement an API key in your .NET mobile app backend. To provide the key, create an app setting in your function app that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

Important

Don't share the API key with your mobile app clients. It should only be distributed securely to service-side clients, like Azure Functions. Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository. This safeguards your sensitive information.

## Output - usage

In C# script functions, use a named output parameter of type `out object`

to access the output record. In C# class libraries, the `MobileTable`

attribute can be used with any of the following types:

`ICollector<T>`

or`IAsyncCollector<T>`

, where`T`

is either`JObject`

or any type with a`public string Id`

property.`out JObject`

`out T`

or`out T[]`

, where`T`

is any Type with a`public string Id`

property.

In Node.js functions, use `context.bindings.<name>`

to access the output record.
