---
merged_at: 2026-01-28T07:43:39.504629
merged_files: 2
---


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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-manually-run-non-http -->

# Manually run a non HTTP-triggered function

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article demonstrates how to manually run a non HTTP-triggered function via specially formatted HTTP request.

In some contexts, such as during development and troubleshooting, you might need to run "on-demand" an Azure Function that is indirectly triggered. Examples of indirect triggers include [functions on a schedule](functions-create-scheduled-function) or functions that run as the [result of events](functions-create-storage-blob-triggered-function).

The procedure described in this article is equivalent to using the **Test/Run** functionality of a function's **Code + Test** tab in the Azure portal. You can also use Visual Studio Code to [manually run functions](functions-develop-vs-code#run-functions).

## Prerequisites

The examples in this article use an HTTP test tool. Make sure to choose a tool that keeps your data secure. For more information, see [HTTP test tools](functions-develop-local#http-test-tools).

## Define the request location

To run a non HTTP-triggered function, you need a way to send a request to Azure to run the function. The URL used to make this request takes a specific form.

**Host name:**The function app's public location that is made up from the function app's name plus*azurewebsites.net*or your custom domain. When you work with[deployment slots](functions-deployment-slots)used for staging, the host name portion is the production host name with`-<slotname>`

appended to it. In the previous example, the URL would be`myfunctiondemos-staging.azurewebsites.net`

for a slot named`staging`

.**Folder path:**To access non HTTP-triggered functions via an HTTP request, you have to send the request through the path`admin/functions`

. APIs under the`/admin/`

path are only accessible with authorization.**Function name:**The name of the function you want to run.

The following considerations apply when making requests to administrator endpoints in your function app:

- When making requests to any endpoint under the
`/admin/`

path, you must supply your app's master key in the`x-functions-key`

header of the request. - When you run locally, authorization isn't enforced and the function's master key isn't required. You can directly
[call the function](#call-the-function)omitting the`x-functions-key`

header. - When accessing function app endpoints in a
[deployment slot](functions-deployment-slots), make sure you use the slot-specific host name in the request URL, along with the slot-specific master key.

## Get the master key

You can get the master key from either the Azure portal or by using the Azure CLI.

Caution

Due to the elevated permissions in your function app granted by the master key, you shouldn't share this key with third parties or distribute it in an application. The key should only be sent to an HTTPS endpoint.

Navigate to your function app in the

[Azure portal](https://portal.azure.com), select**App Keys**, and then the`_master`

key.In the

**Edit key**section, copy the key value to your clipboard, and then select**OK**.

## Call the function

In the Azure portal, navigate top your function app and choose your function.

Select

**Code + Test**, and then select**Logs**. You see messages from the function logged here when you manually run the function from your HTTP test tool.In your HTTP test tool, use the request location you defined as the request URL, make sure that the HTTP request method is POST, and include these two request headers:

Key Value `x-functions-key`

The master key value pasted from the clipboard. `Content-Type`

`application/json`

Make sure that the POST request payload/body is

`{ "input": "<TRIGGER_INPUT>" }`

. The specific`<TRIGGER_INPUT>`

you supply depends on the type of trigger, but it can only be a string, numeric, or boolean value. For services that use JSON payloads, such as Azure Service Bus, the test JSON payload should be escaped and serialized as a string.If you don't want to pass input data to the function, you must still supply an empty dictionary

`{}`

as the body of the POST request. For more information, see the reference article for the specific non-HTTP trigger.Send the HTTP POST request. The response should be an HTTP 202 (Accepted) response.

Next, return to your function in the Azure portal. Review the logs and you see messages coming from the manual call to the function.


The way that you access data sent to the trigger depends on the type of trigger and your function language. For more information, see the reference examples for your [specific trigger](functions-triggers-bindings).

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
