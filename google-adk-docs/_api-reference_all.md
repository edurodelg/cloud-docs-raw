---
merged_at: 2026-01-25T12:06:27.904175
merged_files: 7
---

# Documentos Fusionados

Este archivo contiene 7 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/ -->

# Agent Development Kit

JavaScript is disabled on your browser.
Skip navigation links
Overview
Tree
Index
Search
Agent Development Kit
Packages
Package
Description
com.google.adk
com.google.adk.agents
com.google.adk.artifacts
com.google.adk.events
com.google.adk.examples
com.google.adk.exceptions
com.google.adk.flows
com.google.adk.flows.llmflows
com.google.adk.flows.llmflows.audio
com.google.adk.memory
com.google.adk.models
com.google.adk.models.langchain4j
com.google.adk.network
com.google.adk.runner
com.google.adk.sessions
com.google.adk.tools
com.google.adk.tools.applicationintegrationtoolset
com.google.adk.tools.mcp
com.google.adk.tools.retrieval
com.google.adk.utils
com.google.adk.web
com.google.adk.web.config


---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/ -->

# API Reference¶

# API Reference[¶](#api-reference)

The Agent Development Kit (ADK) provides comprehensive API references for both Python and Java, allowing you to dive deep into all available classes, methods, and functionalities.

-
**Python API Reference**

Explore the complete API documentation for the Python Agent Development Kit. Discover detailed information on all modules, classes, functions, and examples to build sophisticated AI agents with Python.


-
**Go API Reference**

Explore the complete API documentation for the Go Agent Development Kit. Discover detailed information on all modules, classes, and functions to build sophisticated AI agents with Go.


-
**Java API Reference**

Access the comprehensive Javadoc for the Java Agent Development Kit. This reference provides detailed specifications for all packages, classes, interfaces, and methods, enabling you to develop robust AI agents using Java.


-
**Typescript API Reference**

Access the complete API documentation for the TypeScript Agent Development Kit. Find detailed information on all packages, classes, and methods to build powerful and flexible AI agents with TypeScript.


-
**CLI Reference**

Explore the complete API documentation for the CLI including all of the valid options and subcommands.


-
**Agent Config YAML reference**

View the full Agent Config syntax for configuring ADK with YAML text files.


-
**REST API Reference**

Explore the REST API for the ADK web server. This reference provides details on the available endpoints, request and response formats, and more.


---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/rest/ -->

# REST API Reference¶

# REST API Reference[¶](#rest-api-reference)

This page provides a reference for the REST API provided by the ADK web server.
For details on using the ADK REST API in practice, see
[Use the API Server](/adk-docs/runtime/api-server/).

Tip

You can view an updated API reference on a running ADK web server by browsing
the `/docs`

location, for example at: `http://localhost:8000/docs`


## Endpoints[¶](#endpoints)

`/run`

[¶](#run)

This endpoint executes an agent run. It takes a JSON payload with the details of the run and returns a list of events generated during the run.

**Request Body**

The request body should be a JSON object with the following fields:

`app_name`

(string, required): The name of the agent to run.`user_id`

(string, required): The ID of the user.`session_id`

(string, required): The ID of the session.`new_message`

(Content, required): The new message to send to the agent. See the[Content](#content-object)section for more details.`streaming`

(boolean, optional): Whether to use streaming. Defaults to`false`

.`state_delta`

(object, optional): A delta of the state to apply before the run.

**Response Body**

The response body is a JSON array of [Event](#event-object) objects.

`/run_sse`

[¶](#run_sse)

This endpoint executes an agent run using Server-Sent Events (SSE) for streaming responses. It takes the same JSON payload as the `/run`

endpoint.

**Request Body**

The request body is the same as for the `/run`

endpoint.

**Response Body**

The response is a stream of Server-Sent Events. Each event is a JSON object representing an [Event](#event-object).

## Objects[¶](#objects)

`Content`

object[¶](#content-object)

The `Content`

object represents the content of a message. It has the following structure:

`parts`

: A list of parts. Each part can be either text or a function call.`role`

: The role of the author of the message (e.g., "user", "model").

`Event`

object[¶](#event-object)

The `Event`

object represents an event that occurred during an agent run. It has a complex structure with many optional fields. The most important fields are:

`id`

: The ID of the event.`timestamp`

: The timestamp of the event.`author`

: The author of the event.`content`

: The content of the event.


---

<!-- DOCUMENTO FUSIONADO: _cli_merged.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/cli/ -->

# adk cli documentation¶

Add your content using reStructuredText syntax. See the reStructuredText documentation for details.

reStructuredText

Contents:


---

<!-- DOCUMENTO FUSIONADO: clihtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/cli/cli.html -->

# CLI Reference¶

# CLI Reference[¶](#cli-reference)

This page contains the auto-generated command-line reference for the adk tool.

## adk[¶](#adk)

Agent Development Kit CLI tools.

Usage

```
adk [OPTIONS] COMMAND [ARGS]...
```

Options

-
--version
[¶](#cmdoption-adk-version) Show the version and exit.


### api_server[¶](#adk-api-server)

Starts a FastAPI server for agents.

AGENTS_DIR: The directory of agents, where each sub-directory is a single agent, containing at least __init__.py and agent.py files.

Example:

adk api_server –session_service_uri=[uri] –port=[port] path/to/agents_dir


Usage

```
adk api_server [OPTIONS] [AGENTS_DIR]
```

Options

-
--host <host>
[¶](#cmdoption-adk-api_server-host) Optional. The binding host of the server

- Default:
`'127.0.0.1'`


-
--port <port>
[¶](#cmdoption-adk-api_server-port) Optional. The port of the server


-
--allow_origins <allow_origins>
[¶](#cmdoption-adk-api_server-allow_origins) Optional. Any additional origins to allow for CORS.


-
-v, --verbose
[¶](#cmdoption-adk-api_server-v) Enable verbose (DEBUG) logging. Shortcut for –log_level DEBUG.

- Default:
`False`


-
--log_level <log_level>
[¶](#cmdoption-adk-api_server-log_level) Optional. Set the logging level

- Options:
DEBUG | INFO | WARNING | ERROR | CRITICAL


-
--trace_to_cloud
[¶](#cmdoption-adk-api_server-trace_to_cloud) Optional. Whether to enable cloud trace for telemetry.

- Default:
`False`


-
--otel_to_cloud
[¶](#cmdoption-adk-api_server-otel_to_cloud) EXPERIMENTAL Optional. Whether to write OTel data to Google Cloud Observability services - Cloud Trace and Cloud Logging.

- Default:
`False`


-
--reload, --no-reload
[¶](#cmdoption-adk-api_server-reload) Optional. Whether to enable auto reload for server. Not supported for Cloud Run.


-
--a2a
[¶](#cmdoption-adk-api_server-a2a) Optional. Whether to enable A2A endpoint.

- Default:
`False`


-
--reload_agents
[¶](#cmdoption-adk-api_server-reload_agents) Optional. Whether to enable live reload for agents changes.

- Default:
`False`


-
--eval_storage_uri <eval_storage_uri>
[¶](#cmdoption-adk-api_server-eval_storage_uri) Optional. The evals storage URI to store agent evals, supported URIs: gs://<bucket name>.


-
--extra_plugins <extra_plugins>
[¶](#cmdoption-adk-api_server-extra_plugins) Optional. Comma-separated list of extra plugin classes or instances to enable (e.g., my.module.MyPluginClass or my.module.my_plugin_instance).


-
--url_prefix <url_prefix>
[¶](#cmdoption-adk-api_server-url_prefix) Optional. URL path prefix when the application is mounted behind a reverse proxy or API gateway (e.g., ‘/api/v1’, ‘/adk’). This ensures generated URLs and redirects work correctly when the app is not served at the root path. Must start with ‘/’ if provided.


-
--session_service_uri <session_service_uri>
[¶](#cmdoption-adk-api_server-session_service_uri) Optional. The URI of the session service. - Use ‘agentengine://<agent_engine>’ to connect to Agent Engine

sessions. <agent_engine> can either be the full qualified resource name ‘projects/abc/locations/us-central1/reasoningEngines/123’ or the resource id ‘123’.

Use ‘sqlite://<path_to_sqlite_file>’ to connect to an aio-sqlite based session service, which is good for local development.

Use ‘postgresql://<user>:<password>@<host>:<port>/<database_name>’ to connect to a PostgreSQL DB.

See

[https://docs.sqlalchemy.org/en/20/core/engines.html#backend-specific-urls](https://docs.sqlalchemy.org/en/20/core/engines.html#backend-specific-urls)for more details on other database URIs supported by SQLAlchemy.


-
--artifact_service_uri <artifact_service_uri>
[¶](#cmdoption-adk-api_server-artifact_service_uri) Optional. The URI of the artifact service, supported URIs: gs://<bucket name> for GCS artifact service.


-
--memory_service_uri <memory_service_uri>
[¶](#cmdoption-adk-api_server-memory_service_uri) Optional. The URI of the memory service. - Use ‘rag://<rag_corpus_id>’ to connect to Vertex AI Rag Memory Service. - Use ‘agentengine://<agent_engine>’ to connect to Agent Engine

sessions. <agent_engine> can either be the full qualified resource name ‘projects/abc/locations/us-central1/reasoningEngines/123’ or the resource id ‘123’.


-
--session_db_url <session_db_url>
[¶](#cmdoption-adk-api_server-session_db_url) Deprecated. Use –session_service_uri instead.


-
--artifact_storage_uri <artifact_storage_uri>
[¶](#cmdoption-adk-api_server-artifact_storage_uri) Deprecated. Use –artifact_service_uri instead.


Arguments

-
AGENTS_DIR
[¶](#cmdoption-adk-api_server-arg-AGENTS_DIR) Optional argument


### conformance[¶](#adk-conformance)

Conformance testing tools for ADK.

Usage

```
adk conformance [OPTIONS] COMMAND [ARGS]...
```

#### record[¶](#adk-conformance-record)

Generate ADK conformance test YAML files from TestCaseInput specifications.

NOTE: this is work in progress.

This command reads TestCaseInput specifications from input.yaml files, executes the specified test cases against agents, and generates conformance test files with recorded agent interactions as test.yaml files.

Expected directory structure: category/name/input.yaml (TestCaseInput) -> category/name/test.yaml (TestCase)

PATHS: One or more directories containing test case specifications. If no paths are provided, defaults to ‘tests/’ directory.

Examples:

Use default directory: adk conformance record

Custom directories: adk conformance record tests/core tests/tools

Usage

```
adk conformance record [OPTIONS] [PATHS]...
```

Arguments

-
PATHS
[¶](#cmdoption-adk-conformance-record-arg-PATHS) Optional argument(s)


#### test[¶](#adk-conformance-test)

Run conformance tests to verify agent behavior consistency.

Validates that agents produce consistent outputs by comparing against recorded interactions or evaluating live execution results.

PATHS can be any number of folder paths. Each folder can either: - Contain a spec.yaml file directly (single test case) - Contain subdirectories with spec.yaml files (multiple test cases)

If no paths are provided, defaults to searching the ‘tests’ folder.

TEST MODES:

DIRECTORY STRUCTURE:

Test cases must follow this structure:

EXAMPLES:

Usage

```
adk conformance test [OPTIONS] [PATHS]...
```

Options

-
--mode <mode>
[¶](#cmdoption-adk-conformance-test-mode) Test mode: ‘replay’ verifies against recorded interactions, ‘live’ runs evaluation-based verification.

- Default:
`'replay'`

- Options:
replay | live


Arguments

-
PATHS
[¶](#cmdoption-adk-conformance-test-arg-PATHS) Optional argument(s)


### create[¶](#adk-create)

Creates a new app in the current folder with prepopulated agent template.

APP_NAME: required, the folder of the agent source code.

Example:

adk create path/to/my_app


Usage

```
adk create [OPTIONS] APP_NAME
```

Options

-
--model <model>
[¶](#cmdoption-adk-create-model) Optional. The model used for the root agent.


-
--api_key <api_key>
[¶](#cmdoption-adk-create-api_key) Optional. The API Key needed to access the model, e.g. Google AI API Key.


-
--project <project>
[¶](#cmdoption-adk-create-project) Optional. The Google Cloud Project for using VertexAI as backend.


-
--region <region>
[¶](#cmdoption-adk-create-region) Optional. The Google Cloud Region for using VertexAI as backend.


Arguments

-
APP_NAME
[¶](#cmdoption-adk-create-arg-APP_NAME) Required argument


### deploy[¶](#adk-deploy)

Deploys agent to hosted environments.

Usage

```
adk deploy [OPTIONS] COMMAND [ARGS]...
```

#### agent_engine[¶](#adk-deploy-agent-engine)

Deploys an agent to Agent Engine.

Example:

# With Express Mode API Key adk deploy agent_engine –api_key=[api_key] my_agent

# With Google Cloud Project and Region adk deploy agent_engine –project=[project] –region=[region]

–staging_bucket=[staging_bucket] –display_name=[app_name] my_agent


Usage

```
adk deploy agent_engine [OPTIONS] AGENT
```

Options

-
--api_key <api_key>
[¶](#cmdoption-adk-deploy-agent_engine-api_key) Optional. The API key to use for Express Mode. If not provided, the API key from the GOOGLE_API_KEY environment variable will be used. It will only be used if GOOGLE_GENAI_USE_VERTEXAI is true. (It will override GOOGLE_API_KEY in the .env file if it exists.)


-
--project <project>
[¶](#cmdoption-adk-deploy-agent_engine-project) Optional. Google Cloud project to deploy the agent. It will override GOOGLE_CLOUD_PROJECT in the .env file (if it exists). It will be ignored if api_key is set.


-
--region <region>
[¶](#cmdoption-adk-deploy-agent_engine-region) Optional. Google Cloud region to deploy the agent. It will override GOOGLE_CLOUD_LOCATION in the .env file (if it exists). It will be ignored if api_key is set.


-
--staging_bucket <staging_bucket>
[¶](#cmdoption-adk-deploy-agent_engine-staging_bucket) Optional. GCS bucket for staging the deployment artifacts. It will be ignored if api_key is set.


-
--agent_engine_id <agent_engine_id>
[¶](#cmdoption-adk-deploy-agent_engine-agent_engine_id) Optional. ID of the Agent Engine instance to update if it exists (default: None, which means a new instance will be created). If project and region are set, this should be the resource ID, and the corresponding resource name in Agent Engine will be: projects/{project}/locations/{region}/reasoningEngines/{agent_engine_id}. If api_key is set, then agent_engine_id is required to be the full resource name (i.e. projects/*/locations/*/reasoningEngines/*).


-
--trace_to_cloud, --no-trace_to_cloud
[¶](#cmdoption-adk-deploy-agent_engine-trace_to_cloud) Optional. Whether to enable Cloud Trace for Agent Engine.


-
--display_name <display_name>
[¶](#cmdoption-adk-deploy-agent_engine-display_name) Optional. Display name of the agent in Agent Engine.

- Default:
`''`


-
--description <description>
[¶](#cmdoption-adk-deploy-agent_engine-description) Optional. Description of the agent in Agent Engine.

- Default:
`''`


-
--adk_app <adk_app>
[¶](#cmdoption-adk-deploy-agent_engine-adk_app) Optional. Python file for defining the ADK application (default: a file named agent_engine_app.py)


-
--temp_folder <temp_folder>
[¶](#cmdoption-adk-deploy-agent_engine-temp_folder) Optional. Temp folder for the generated Agent Engine source files. If the folder already exists, its contents will be removed. (default: a timestamped folder in the current working directory).


-
--adk_app_object <adk_app_object>
[¶](#cmdoption-adk-deploy-agent_engine-adk_app_object) Optional. Python object corresponding to the root ADK agent or app. It can only be root_agent or app. (default: root_agent)


-
--env_file <env_file>
[¶](#cmdoption-adk-deploy-agent_engine-env_file) Optional. The filepath to the .env file for environment variables. (default: the .env file in the agent directory, if any.)


-
--requirements_file <requirements_file>
[¶](#cmdoption-adk-deploy-agent_engine-requirements_file) Optional. The filepath to the requirements.txt file to use. (default: the requirements.txt file in the agent directory, if any.)


-
--absolutize_imports <absolutize_imports>
[¶](#cmdoption-adk-deploy-agent_engine-absolutize_imports) NOTE: This flag is deprecated and will be removed in the future.


-
--agent_engine_config_file <agent_engine_config_file>
[¶](#cmdoption-adk-deploy-agent_engine-agent_engine_config_file) Optional. The filepath to the .agent_engine_config.json file to use. The values in this file will be overridden by the values set by other flags. (default: the .agent_engine_config.json file in the agent directory, if any.)


Arguments

-
AGENT
[¶](#cmdoption-adk-deploy-agent_engine-arg-AGENT) Required argument


#### cloud_run[¶](#adk-deploy-cloud-run)

Deploys an agent to Cloud Run.

AGENT: The path to the agent source code folder.

Use ‘–’ to separate gcloud arguments from adk arguments.

Examples:

adk deploy cloud_run –project=[project] –region=[region] path/to/my_agent


- adk deploy cloud_run –project=[project] –region=[region] path/to/my_agent
– –no-allow-unauthenticated –min-instances=2


Usage

```
adk deploy cloud_run [OPTIONS] AGENT
```

Options

-
--project <project>
[¶](#cmdoption-adk-deploy-cloud_run-project) Required. Google Cloud project to deploy the agent. When absent, default project from gcloud config is used.


-
--region <region>
[¶](#cmdoption-adk-deploy-cloud_run-region) Required. Google Cloud region to deploy the agent. When absent, gcloud run deploy will prompt later.


-
--service_name <service_name>
[¶](#cmdoption-adk-deploy-cloud_run-service_name) Optional. The service name to use in Cloud Run (default: ‘adk-default-service-name’).


-
--app_name <app_name>
[¶](#cmdoption-adk-deploy-cloud_run-app_name) Optional. App name of the ADK API server (default: the folder name of the AGENT source code).


-
--port <port>
[¶](#cmdoption-adk-deploy-cloud_run-port) Optional. The port of the ADK API server (default: 8000).


-
--trace_to_cloud
[¶](#cmdoption-adk-deploy-cloud_run-trace_to_cloud) Optional. Whether to enable Cloud Trace for cloud run.

- Default:
`False`


-
--with_ui
[¶](#cmdoption-adk-deploy-cloud_run-with_ui) Optional. Deploy ADK Web UI if set. (default: deploy ADK API server only)

- Default:
`False`


-
--temp_folder <temp_folder>
[¶](#cmdoption-adk-deploy-cloud_run-temp_folder) Optional. Temp folder for the generated Cloud Run source files (default: a timestamped folder in the system temp directory).


-
--log_level <log_level>
[¶](#cmdoption-adk-deploy-cloud_run-log_level) Optional. Set the logging level

- Options:
DEBUG | INFO | WARNING | ERROR | CRITICAL


-
--verbosity <verbosity>
[¶](#cmdoption-adk-deploy-cloud_run-verbosity) Deprecated. Use –log_level instead.

- Options:
DEBUG | INFO | WARNING | ERROR | CRITICAL


-
--adk_version <adk_version>
[¶](#cmdoption-adk-deploy-cloud_run-adk_version) Optional. The ADK version used in Cloud Run deployment. (default: the version in the dev environment)

- Default:
`'1.19.0'`


-
--a2a
[¶](#cmdoption-adk-deploy-cloud_run-a2a) Optional. Whether to enable A2A endpoint.

- Default:
`False`


-
--allow_origins <allow_origins>
[¶](#cmdoption-adk-deploy-cloud_run-allow_origins) Optional. Any additional origins to allow for CORS.


-
--session_service_uri <session_service_uri>
[¶](#cmdoption-adk-deploy-cloud_run-session_service_uri) Optional. The URI of the session service. - Use ‘agentengine://<agent_engine>’ to connect to Agent Engine

sessions. <agent_engine> can either be the full qualified resource name ‘projects/abc/locations/us-central1/reasoningEngines/123’ or the resource id ‘123’.

Use ‘sqlite://<path_to_sqlite_file>’ to connect to an aio-sqlite based session service, which is good for local development.

Use ‘postgresql://<user>:<password>@<host>:<port>/<database_name>’ to connect to a PostgreSQL DB.

See

[https://docs.sqlalchemy.org/en/20/core/engines.html#backend-specific-urls](https://docs.sqlalchemy.org/en/20/core/engines.html#backend-specific-urls)for more details on other database URIs supported by SQLAlchemy.


-
--artifact_service_uri <artifact_service_uri>
[¶](#cmdoption-adk-deploy-cloud_run-artifact_service_uri) Optional. The URI of the artifact service, supported URIs: gs://<bucket name> for GCS artifact service.


-
--memory_service_uri <memory_service_uri>
[¶](#cmdoption-adk-deploy-cloud_run-memory_service_uri) Optional. The URI of the memory service. - Use ‘rag://<rag_corpus_id>’ to connect to Vertex AI Rag Memory Service. - Use ‘agentengine://<agent_engine>’ to connect to Agent Engine

sessions. <agent_engine> can either be the full qualified resource name ‘projects/abc/locations/us-central1/reasoningEngines/123’ or the resource id ‘123’.


-
--session_db_url <session_db_url>
[¶](#cmdoption-adk-deploy-cloud_run-session_db_url) Deprecated. Use –session_service_uri instead.


-
--artifact_storage_uri <artifact_storage_uri>
[¶](#cmdoption-adk-deploy-cloud_run-artifact_storage_uri) Deprecated. Use –artifact_service_uri instead.


Arguments

-
AGENT
[¶](#cmdoption-adk-deploy-cloud_run-arg-AGENT) Required argument


#### gke[¶](#adk-deploy-gke)

Deploys an agent to GKE.

AGENT: The path to the agent source code folder.

Example:


- adk deploy gke –project=[project] –region=[region]
–cluster_name=[cluster_name] path/to/my_agent


Usage

```
adk deploy gke [OPTIONS] AGENT
```

Options

-
--project <project>
[¶](#cmdoption-adk-deploy-gke-project) Required. Google Cloud project to deploy the agent. When absent, default project from gcloud config is used.


-
--region <region>
[¶](#cmdoption-adk-deploy-gke-region) Required. Google Cloud region to deploy the agent. When absent, gcloud run deploy will prompt later.


-
--cluster_name <cluster_name>
[¶](#cmdoption-adk-deploy-gke-cluster_name) Required. The name of the GKE cluster.


-
--service_name <service_name>
[¶](#cmdoption-adk-deploy-gke-service_name) Optional. The service name to use in GKE (default: ‘adk-default-service-name’).


-
--app_name <app_name>
[¶](#cmdoption-adk-deploy-gke-app_name) Optional. App name of the ADK API server (default: the folder name of the AGENT source code).


-
--port <port>
[¶](#cmdoption-adk-deploy-gke-port) Optional. The port of the ADK API server (default: 8000).


-
--trace_to_cloud
[¶](#cmdoption-adk-deploy-gke-trace_to_cloud) Optional. Whether to enable Cloud Trace for GKE.

- Default:
`False`


-
--with_ui
[¶](#cmdoption-adk-deploy-gke-with_ui) Optional. Deploy ADK Web UI if set. (default: deploy ADK API server only)

- Default:
`False`


-
--log_level <log_level>
[¶](#cmdoption-adk-deploy-gke-log_level) Optional. Set the logging level

- Options:
DEBUG | INFO | WARNING | ERROR | CRITICAL


-
--temp_folder <temp_folder>
[¶](#cmdoption-adk-deploy-gke-temp_folder) Optional. Temp folder for the generated GKE source files (default: a timestamped folder in the system temp directory).


-
--adk_version <adk_version>
[¶](#cmdoption-adk-deploy-gke-adk_version) Optional. The ADK version used in GKE deployment. (default: the version in the dev environment)

- Default:
`'1.19.0'`


-
--session_service_uri <session_service_uri>
[¶](#cmdoption-adk-deploy-gke-session_service_uri) Optional. The URI of the session service. - Use ‘agentengine://<agent_engine>’ to connect to Agent Engine

sessions. <agent_engine> can either be the full qualified resource name ‘projects/abc/locations/us-central1/reasoningEngines/123’ or the resource id ‘123’.

Use ‘sqlite://<path_to_sqlite_file>’ to connect to an aio-sqlite based session service, which is good for local development.

Use ‘postgresql://<user>:<password>@<host>:<port>/<database_name>’ to connect to a PostgreSQL DB.

See

[https://docs.sqlalchemy.org/en/20/core/engines.html#backend-specific-urls](https://docs.sqlalchemy.org/en/20/core/engines.html#backend-specific-urls)for more details on other database URIs supported by SQLAlchemy.


-
--artifact_service_uri <artifact_service_uri>
[¶](#cmdoption-adk-deploy-gke-artifact_service_uri) Optional. The URI of the artifact service, supported URIs: gs://<bucket name> for GCS artifact service.


-
--memory_service_uri <memory_service_uri>
[¶](#cmdoption-adk-deploy-gke-memory_service_uri) Optional. The URI of the memory service. - Use ‘rag://<rag_corpus_id>’ to connect to Vertex AI Rag Memory Service. - Use ‘agentengine://<agent_engine>’ to connect to Agent Engine

sessions. <agent_engine> can either be the full qualified resource name ‘projects/abc/locations/us-central1/reasoningEngines/123’ or the resource id ‘123’.


Arguments

-
AGENT
[¶](#cmdoption-adk-deploy-gke-arg-AGENT) Required argument


### eval[¶](#adk-eval)

Evaluates an agent given the eval sets.

AGENT_MODULE_FILE_PATH: The path to the __init__.py file that contains a module by the name “agent”. “agent” module contains a root_agent.

EVAL_SET_FILE_PATH_OR_ID: You can specify one or more eval set file paths or eval set id.

Mixing of eval set file paths with eval set ids is not allowed.

*Eval Set File Path*
For each file, all evals will be run by default.

If you want to run only specific evals from an eval set, first create a comma separated list of eval names and then add that as a suffix to the eval set file name, demarcated by a :.

For example, we have sample_eval_set_file.json file that has following the eval cases: sample_eval_set_file.json:

sample_eval_set_file.json:eval_1,eval_2,eval_3

This will only run eval_1, eval_2 and eval_3 from sample_eval_set_file.json.

*Eval Set ID*
For each eval set, all evals will be run by default.

If you want to run only specific evals from an eval set, first create a comma separated list of eval names and then add that as a suffix to the eval set file name, demarcated by a :.

For example, we have sample_eval_set_id that has following the eval cases: sample_eval_set_id:

- If we did:
sample_eval_set_id:eval_1,eval_2,eval_3


This will only run eval_1, eval_2 and eval_3 from sample_eval_set_id.

CONFIG_FILE_PATH: The path to config file.

PRINT_DETAILED_RESULTS: Prints detailed results on the console.

Usage

```
adk eval [OPTIONS] AGENT_MODULE_FILE_PATH [EVAL_SET_FILE_PATH_OR_ID]...
```

Options

-
--config_file_path <config_file_path>
[¶](#cmdoption-adk-eval-config_file_path) Optional. The path to config file.


-
--print_detailed_results
[¶](#cmdoption-adk-eval-print_detailed_results) Optional. Whether to print detailed results on console or not.

- Default:
`False`


-
--eval_storage_uri <eval_storage_uri>
[¶](#cmdoption-adk-eval-eval_storage_uri) Optional. The evals storage URI to store agent evals, supported URIs: gs://<bucket name>.


-
--log_level <log_level>
[¶](#cmdoption-adk-eval-log_level) Optional. Set the logging level

- Options:
DEBUG | INFO | WARNING | ERROR | CRITICAL


Arguments

-
AGENT_MODULE_FILE_PATH
[¶](#cmdoption-adk-eval-arg-AGENT_MODULE_FILE_PATH) Required argument


-
EVAL_SET_FILE_PATH_OR_ID
[¶](#cmdoption-adk-eval-arg-EVAL_SET_FILE_PATH_OR_ID) Optional argument(s)


### eval_set[¶](#adk-eval-set)

Manage Eval Sets.

Usage

```
adk eval_set [OPTIONS] COMMAND [ARGS]...
```

#### add_eval_case[¶](#adk-eval-set-add-eval-case)

Adds eval cases to the given eval set.

There are several ways that an eval case can be created, for now this method only supports adding one using a conversation scenarios file.

If an eval case for the generated id already exists, then we skip adding it.

Usage

```
adk eval_set add_eval_case [OPTIONS] AGENT_MODULE_FILE_PATH EVAL_SET_ID
```

Options

-
--scenarios_file <scenarios_file>
[¶](#cmdoption-adk-eval_set-add_eval_case-scenarios_file) **Required**A path to file containing JSON serialized ConversationScenarios.

-
--session_input_file <session_input_file>
[¶](#cmdoption-adk-eval_set-add_eval_case-session_input_file) **Required**Path to session file containing SessionInput in JSON format.

-
--eval_storage_uri <eval_storage_uri>
[¶](#cmdoption-adk-eval_set-add_eval_case-eval_storage_uri) Optional. The evals storage URI to store agent evals, supported URIs: gs://<bucket name>.


-
--log_level <log_level>
[¶](#cmdoption-adk-eval_set-add_eval_case-log_level) Optional. Set the logging level

- Options:
DEBUG | INFO | WARNING | ERROR | CRITICAL


Arguments

-
AGENT_MODULE_FILE_PATH
[¶](#cmdoption-adk-eval_set-add_eval_case-arg-AGENT_MODULE_FILE_PATH) Required argument


-
EVAL_SET_ID
[¶](#cmdoption-adk-eval_set-add_eval_case-arg-EVAL_SET_ID) Required argument


#### create[¶](#adk-eval-set-create)

Creates an empty EvalSet given the agent_module_file_path and eval_set_id.

Usage

```
adk eval_set create [OPTIONS] AGENT_MODULE_FILE_PATH EVAL_SET_ID
```

Options

-
--eval_storage_uri <eval_storage_uri>
[¶](#cmdoption-adk-eval_set-create-eval_storage_uri) Optional. The evals storage URI to store agent evals, supported URIs: gs://<bucket name>.


-
--log_level <log_level>
[¶](#cmdoption-adk-eval_set-create-log_level) Optional. Set the logging level

- Options:
DEBUG | INFO | WARNING | ERROR | CRITICAL


Arguments

-
AGENT_MODULE_FILE_PATH
[¶](#cmdoption-adk-eval_set-create-arg-AGENT_MODULE_FILE_PATH) Required argument


-
EVAL_SET_ID
[¶](#cmdoption-adk-eval_set-create-arg-EVAL_SET_ID) Required argument


### run[¶](#adk-run)

Runs an interactive CLI for a certain agent.

AGENT: The path to the agent source code folder.

Example:

adk run path/to/my_agent


Usage

```
adk run [OPTIONS] AGENT
```

Options

-
--save_session
[¶](#cmdoption-adk-run-save_session) Optional. Whether to save the session to a json file on exit.

- Default:
`False`


-
--session_id <session_id>
[¶](#cmdoption-adk-run-session_id) Optional. The session ID to save the session to on exit when –save_session is set to true. User will be prompted to enter a session ID if not set.


-
--replay <replay>
[¶](#cmdoption-adk-run-replay) The json file that contains the initial state of the session and user queries. A new session will be created using this state. And user queries are run against the newly created session. Users cannot continue to interact with the agent.


-
--resume <resume>
[¶](#cmdoption-adk-run-resume) The json file that contains a previously saved session (by –save_session option). The previous session will be re-displayed. And user can continue to interact with the agent.


Arguments

-
AGENT
[¶](#cmdoption-adk-run-arg-AGENT) Required argument


### web[¶](#adk-web)

Starts a FastAPI server with Web UI for agents.

AGENTS_DIR: The directory of agents, where each sub-directory is a single agent, containing at least __init__.py and agent.py files.

Example:

adk web –session_service_uri=[uri] –port=[port] path/to/agents_dir


Usage

```
adk web [OPTIONS] [AGENTS_DIR]
```

Options

-
--host <host>
[¶](#cmdoption-adk-web-host) Optional. The binding host of the server

- Default:
`'127.0.0.1'`


-
--port <port>
[¶](#cmdoption-adk-web-port) Optional. The port of the server


-
--allow_origins <allow_origins>
[¶](#cmdoption-adk-web-allow_origins) Optional. Any additional origins to allow for CORS.


-
-v, --verbose
[¶](#cmdoption-adk-web-v) Enable verbose (DEBUG) logging. Shortcut for –log_level DEBUG.

- Default:
`False`


-
--log_level <log_level>
[¶](#cmdoption-adk-web-log_level) Optional. Set the logging level

- Options:
DEBUG | INFO | WARNING | ERROR | CRITICAL


-
--trace_to_cloud
[¶](#cmdoption-adk-web-trace_to_cloud) Optional. Whether to enable cloud trace for telemetry.

- Default:
`False`


-
--otel_to_cloud
[¶](#cmdoption-adk-web-otel_to_cloud) EXPERIMENTAL Optional. Whether to write OTel data to Google Cloud Observability services - Cloud Trace and Cloud Logging.

- Default:
`False`


-
--reload, --no-reload
[¶](#cmdoption-adk-web-reload) Optional. Whether to enable auto reload for server. Not supported for Cloud Run.


-
--a2a
[¶](#cmdoption-adk-web-a2a) Optional. Whether to enable A2A endpoint.

- Default:
`False`


-
--reload_agents
[¶](#cmdoption-adk-web-reload_agents) Optional. Whether to enable live reload for agents changes.

- Default:
`False`


-
--eval_storage_uri <eval_storage_uri>
[¶](#cmdoption-adk-web-eval_storage_uri) Optional. The evals storage URI to store agent evals, supported URIs: gs://<bucket name>.


-
--extra_plugins <extra_plugins>
[¶](#cmdoption-adk-web-extra_plugins) Optional. Comma-separated list of extra plugin classes or instances to enable (e.g., my.module.MyPluginClass or my.module.my_plugin_instance).


-
--url_prefix <url_prefix>
[¶](#cmdoption-adk-web-url_prefix) Optional. URL path prefix when the application is mounted behind a reverse proxy or API gateway (e.g., ‘/api/v1’, ‘/adk’). This ensures generated URLs and redirects work correctly when the app is not served at the root path. Must start with ‘/’ if provided.


-
--logo-text <logo_text>
[¶](#cmdoption-adk-web-logo-text) Optional. The text to display in the logo of the web UI.


-
--logo-image-url <logo_image_url>
[¶](#cmdoption-adk-web-logo-image-url) Optional. The URL of the image to display in the logo of the web UI.


-
--session_service_uri <session_service_uri>
[¶](#cmdoption-adk-web-session_service_uri) Optional. The URI of the session service. - Use ‘agentengine://<agent_engine>’ to connect to Agent Engine

sessions. <agent_engine> can either be the full qualified resource name ‘projects/abc/locations/us-central1/reasoningEngines/123’ or the resource id ‘123’.

Use ‘sqlite://<path_to_sqlite_file>’ to connect to an aio-sqlite based session service, which is good for local development.

Use ‘postgresql://<user>:<password>@<host>:<port>/<database_name>’ to connect to a PostgreSQL DB.

See

[https://docs.sqlalchemy.org/en/20/core/engines.html#backend-specific-urls](https://docs.sqlalchemy.org/en/20/core/engines.html#backend-specific-urls)for more details on other database URIs supported by SQLAlchemy.


-
--artifact_service_uri <artifact_service_uri>
[¶](#cmdoption-adk-web-artifact_service_uri) Optional. The URI of the artifact service, supported URIs: gs://<bucket name> for GCS artifact service.


-
--memory_service_uri <memory_service_uri>
[¶](#cmdoption-adk-web-memory_service_uri) Optional. The URI of the memory service. - Use ‘rag://<rag_corpus_id>’ to connect to Vertex AI Rag Memory Service. - Use ‘agentengine://<agent_engine>’ to connect to Agent Engine

sessions. <agent_engine> can either be the full qualified resource name ‘projects/abc/locations/us-central1/reasoningEngines/123’ or the resource id ‘123’.


-
--session_db_url <session_db_url>
[¶](#cmdoption-adk-web-session_db_url) Deprecated. Use –session_service_uri instead.


-
--artifact_storage_uri <artifact_storage_uri>
[¶](#cmdoption-adk-web-artifact_storage_uri) Deprecated. Use –artifact_service_uri instead.


Arguments

-
AGENTS_DIR
[¶](#cmdoption-adk-web-arg-AGENTS_DIR) Optional argument


---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/agentconfig/ -->

# AgentConfig

The config for the YAML schema to create an agent.

The config for the YAML schema of a LlmAgent.

No Additional PropertiesThe value is used to uniquely identify the LlmAgent class. If it is empty, it is by default an LlmAgent.

Required. The name of the agent.

Optional. The description of the agent.

Optional. The sub-agents of the agent.

The config for the reference to another agent.

No Additional PropertiesOptional. The before*agent*callbacks of the agent.

Example:


```
before_agent_callbacks:
- name: my_library.security_callbacks.before_agent_callback
```


Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

No Additional PropertiesAn argument passed to a function or a class's constructor.

No Additional PropertiesOptional. The after*agent*callbacks of the agent.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. LlmAgent.model. If not set, the model will be inherited from the ancestor.

Required. LlmAgent.instruction.

Optional. LlmAgent.disallow*transfer*to_parent.

Optional. LlmAgent.disallow*transfer*to_peers.

Optional. LlmAgent.input_schema.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. LlmAgent.output_schema.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. LlmAgent.output_key.

Optional. LlmAgent.include_contents.

Optional. LlmAgent.tools.

Examples:

For ADK built-in tools in `google.adk.tools`

package, they can be referenced

directly with the name:


```
tools:
- name: google_search
- name: load_memory
```


For user-defined tools, they can be referenced with fully qualified name:


```
tools:
- name: my_library.my_tools.my_tool
```


For tools that needs to be created via functions:


```
tools:
- name: my_library.my_tools.create_tool
args:
- name: param1
value: value1
- name: param2
value: value2
```


For more advanced tools, instead of specifying arguments in config, it's

recommended to define them in Python files and reference them. E.g.,


```
# tools.py
my_mcp_toolset = MCPToolset(
connection_params=StdioServerParameters(
command="npx",
args=["-y", "@notionhq/notion-mcp-server"],
env={"OPENAPI_MCP_HEADERS": NOTION_HEADERS},
)
)
```


Then, reference the toolset in config:


```
tools:
- name: tools.my_mcp_toolset
```


The configuration for a tool.

The config supports these types of tools:

1. ADK built-in tools

2. User-defined tool instances

3. User-defined tool classes

4. User-defined functions that generate tool instances

5. User-defined function tools

For examples:

For ADK built-in tool instances or classes in `google.adk.tools`

package,

they can be referenced directly with the `name`

and optionally with

`args`

.

```
tools:
- name: google_search
- name: AgentTool
args:
agent: ./another_agent.yaml
skip_summarization: true
```


For user-defined tool instances, the `name`

is the fully qualified path

to the tool instance.

```
tools:
- name: my_package.my_module.my_tool
```


For user-defined tool classes (custom tools), the `name`

is the fully

qualified path to the tool class and `args`

is the arguments for the tool.

```
tools:
- name: my_package.my_module.my_tool_class
args:
my_tool_arg1: value1
my_tool_arg2: value2
```


For user-defined functions that generate tool instances, the `name`

is

the fully qualified path to the function and `args`

is passed to the

function as arguments.

```
tools:
- name: my_package.my_module.my_tool_function
args:
my_function_arg1: value1
my_function_arg2: value2
```


The function must have the following signature:

```
def my_function(args: ToolArgsConfig) -> BaseTool:
...
```


For user-defined function tools, the `name`

is the fully qualified path

to the function.

```
tools:
- name: my_package.my_module.my_function_tool
```


If the above use cases don't suffice, users can define a custom tool config

by extending BaseToolConfig and override from_config() in the custom tool.

The args for the tool.

Config to host free key-value pairs for the args in ToolConfig.

Additional Properties of any type are allowed.

Type: objectOptional. LlmAgent.before*model*callbacks.

Example:


```
before_model_callbacks:
- name: my_library.callbacks.before_model_callback
```


Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. LlmAgent.after*model*callbacks.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. LlmAgent.before*tool*callbacks.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. LlmAgent.after*tool*callbacks.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. LlmAgent.generate*content*config.

Optional model configuration parameters.

For more information, see ```
Content generation parameters
<https://cloud.google.com/vertex-ai/generative-ai/docs/multimodal/content-generation-parameters>
```

_.

Used to override HTTP request options.

HTTP options to be used in each of the requests.

No Additional PropertiesThe base URL for the AI platform service endpoint.

Specifies the version of the API to use.

Additional HTTP headers to be sent with the request.

Each additional property must conform to the following schema

Type: stringTimeout for the request in milliseconds.

Args passed to the HTTP client.

Additional Properties of any type are allowed.

Type: objectArgs passed to the async HTTP client.

Additional Properties of any type are allowed.

Type: objectExtra parameters to add to the request body.

The structure must match the backend API's request structure.

- VertexAI backend API docs: https://cloud.google.com/vertex-ai/docs/reference/rest

- GeminiAPI backend API docs: https://ai.google.dev/api/rest

Additional Properties of any type are allowed.

Type: objectHTTP retry options for the request.

HTTP retry options to be used in each of the requests.

No Additional PropertiesMaximum number of attempts, including the original request.

If 0 or 1, it means no retries.

Initial delay before the first retry, in fractions of a second.

Maximum delay between retries, in fractions of a second.

Multiplier by which the delay increases after each attempt.

Randomness factor for the delay.

List of HTTP status codes that should trigger a retry.

If not specified, a default set of retryable codes may be used.

Instructions for the model to steer it toward better performance.

For example, "Answer as concisely as possible" or "Don't use technical

terms in your response".

Contains the multi-part content of a message.

No Additional PropertiesList of parts that constitute a single message. Each part may have

a different IANA MIME type.

A datatype containing media content.

Exactly one field within a Part should be set, representing the specific type

of content being conveyed. Using multiple fields within the same `Part`


instance is considered invalid.

Metadata for a given video.

Describes how the video in the Part should be used by the model.

No Additional PropertiesThe frame rate of the video sent to the model. If not specified, the

default value will be 1.0. The fps range is (0.0, 24.0].

Optional. The end offset of the video.

Optional. The start offset of the video.

Indicates if the part is thought from the model.

Optional. Inlined bytes data.

Content blob.

No Additional PropertiesOptional. Display name of the blob. Used to provide a label or filename to distinguish blobs. This field is not currently used in the Gemini GenerateContent calls.

Required. Raw bytes.

Required. The IANA standard MIME type of the source data.

Optional. URI based data.

URI based data.

No Additional PropertiesOptional. Display name of the file data. Used to provide a label or filename to distinguish file datas. It is not currently used in the Gemini GenerateContent calls.

Required. URI.

Required. The IANA standard MIME type of the source data.

An opaque signature for the thought so it can be reused in subsequent requests.

Optional. Result of executing the [ExecutableCode].

Result of executing the [ExecutableCode].

Only generated when using the [CodeExecution] tool, and always follows a

`part`

containing the [ExecutableCode].

Required. Outcome of the code execution.

Required. Outcome of the code execution.

Optional. Contains stdout when code execution is successful, stderr or other description otherwise.

Optional. Code generated by the model that is meant to be executed.

Code generated by the model that is meant to be executed, and the result returned to the model.

Generated when using the [CodeExecution] tool, in which the code will be

automatically executed, and a corresponding [CodeExecutionResult] will also be

generated.

Required. The code to be executed.

Required. Programming language of the `code`

.

Required. Programming language of the `code`

.

Optional. A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] with the parameters and their values.

A function call.

No Additional PropertiesThe unique id of the function call. If populated, the client to execute the

`function_call`

and return the response with the matching `id`

.

Optional. The function parameters and values in JSON object format. See [FunctionDeclaration.parameters] for parameter details.

Additional Properties of any type are allowed.

Type: objectRequired. The name of the function to call. Matches [FunctionDeclaration.name].

Optional. The result output of a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function call. It is used as context to the model.

A function response.

No Additional PropertiesSignals that function call continues, and more responses will be returned, turning the function call into a generator. Is only applicable to NON*BLOCKING function calls (see FunctionDeclaration.behavior for details), ignored otherwise. If false, the default, future responses will not be considered. Is only applicable to NON*BLOCKING function calls, is ignored otherwise. If set to false, future responses will not be considered. It is allowed to return empty `response`

with `will_continue=False`

to signal that the function call is finished.

Specifies how the response should be scheduled in the conversation. Only applicable to NON*BLOCKING function calls, is ignored otherwise. Defaults to WHEN*IDLE.

Specifies how the response should be scheduled in the conversation.

Optional. The id of the function call this response is for. Populated by the client to match the corresponding function call `id`

.

Required. The name of the function to call. Matches [FunctionDeclaration.name] and [FunctionCall.name].

Required. The function response in JSON object format. Use "output" key to specify function output and "error" key to specify error details (if any). If "output" and "error" keys are not specified, then whole "response" is treated as function output.

Additional Properties of any type are allowed.

Type: objectOptional. Text part (can be code).

Optional. The producer of the content. Must be either 'user' or

'model'. Useful to set for multi-turn conversations, otherwise can be

empty. If role is not specified, SDK will determine the role.

A file uploaded to the API.

No Additional PropertiesThe `File`

resource name. The ID (name excluding the "files/" prefix) can contain up to 40 characters that are lowercase alphanumeric or dashes (-). The ID cannot start or end with a dash. If the name is empty on create, a unique name will be generated. Example: `files/123-456`


Optional. The human-readable display name for the `File`

. The display name must be no more than 512 characters in length, including spaces. Example: 'Welcome Image'

Output only. MIME type of the file.

Output only. Size of the file in bytes.

Output only. The timestamp of when the `File`

was created.

Output only. The timestamp of when the `File`

will be deleted. Only set if the `File`

is scheduled to expire.

Output only. The timestamp of when the `File`

was last updated.

Output only. SHA-256 hash of the uploaded bytes. The hash value is encoded in base64 format.

Output only. The URI of the `File`

.

Output only. The URI of the `File`

, only set for downloadable (generated) files.

Output only. Processing state of the File.

State for the lifecycle of a File.

Output only. The source of the `File`

.

Source of the File.

Output only. Metadata for a video.

Additional Properties of any type are allowed.

Type: objectOutput only. Error status if File processing failed.

Status of a File that uses a common error model.

No Additional PropertiesA list of messages that carry the error details. There is a common set of message types for APIs to use.

Additional Properties of any type are allowed.

Type: objectA list of messages that carry the error details. There is a common set of message types for APIs to use.

The status code. 0 for OK, 1 for CANCELLED

A datatype containing media content.

Exactly one field within a Part should be set, representing the specific type

of content being conveyed. Using multiple fields within the same `Part`


instance is considered invalid.

A datatype containing media content.

Exactly one field within a Part should be set, representing the specific type

of content being conveyed. Using multiple fields within the same `Part`


instance is considered invalid.

Value that controls the degree of randomness in token selection.

Lower temperatures are good for prompts that require a less open-ended or

creative response, while higher temperatures can lead to more diverse or

creative results.

Tokens are selected from the most to least probable until the sum

of their probabilities equals this value. Use a lower value for less

random responses and a higher value for more random responses.

For each token selection step, the `top_k`

tokens with the

highest probabilities are sampled. Then tokens are further filtered based

on `top_p`

with the final token selected using temperature sampling. Use

a lower number for less random responses and a higher number for more

random responses.

Number of response variations to return.

Maximum number of tokens that can be generated in the response.

List of strings that tells the model to stop generating text if one

of the strings is encountered in the response.

Whether to return the log probabilities of the tokens that were

chosen by the model at each step.

Number of top candidate tokens to return the log probabilities for

at each generation step.

Positive values penalize tokens that already appear in the

generated text, increasing the probability of generating more diverse

content.

Positive values penalize tokens that repeatedly appear in the

generated text, increasing the probability of generating more diverse

content.

When `seed`

is fixed to a specific number, the model makes a best

effort to provide the same response for repeated requests. By default, a

random number is used.

Output response mimetype of the generated candidate text.

Supported mimetype:

- `text/plain`

: (default) Text output.

- `application/json`

: JSON response in the candidates.

The model needs to be prompted to output the appropriate response type,

otherwise the behavior is undefined.

This is a preview feature.

The `Schema`

object allows the definition of input and output data types.

These types can be objects, but also primitives and arrays.

Represents a select subset of an [OpenAPI 3.0 schema
object](https://spec.openapis.org/oas/v3.0.3#schema).

`application/json`

: Schema for JSON response.Additional Properties of any type are allowed.

Type: objectSchema is used to define the format of input/output data.

Represents a select subset of an [OpenAPI 3.0 schema
object](https://spec.openapis.org/oas/v3.0.3#schema-object). More fields may

Optional. Can either be a boolean or an object; controls the presence of additional properties.

Optional. A map of definitions for use by `ref`

Only allowed at the root of the schema.

Each additional property must conform to the following schema

Schema is used to define the format of input/output data.

Represents a select subset of an [OpenAPI 3.0 schema
object](https://spec.openapis.org/oas/v3.0.3#schema-object). More fields may

Optional. Allows indirect references between schema nodes. The value should be a valid reference to a child of the root `defs`

. For example, the following schema defines a reference to a schema node named "Pet": type: object properties: pet: ref: #/defs/Pet defs: Pet: type: object properties: name: type: string The value of the "pet" property is a reference to the schema node named "Pet". See details in https://json-schema.org/understanding-json-schema/structuring

Optional. The value should be validated against any (one or more) of the subschemas in the list.

Schema is used to define the format of input/output data.

Represents a select subset of an [OpenAPI 3.0 schema
object](https://spec.openapis.org/oas/v3.0.3#schema-object). More fields may

Optional. Default value of the data.

Optional. The description of the data.

Optional. Possible values of the element of primitive type with enum format. Examples: 1. We can define direction as : {type:STRING, format:enum, enum:["EAST", NORTH", "SOUTH", "WEST"]} 2. We can define apartment number as : {type:INTEGER, format:enum, enum:["101", "201", "301"]}

Optional. Example of the object. Will only populated when the object is the root.

Optional. The format of the data. Supported formats: for NUMBER type: "float", "double" for INTEGER type: "int32", "int64" for STRING type: "email", "byte", etc

Optional. SCHEMA FIELDS FOR TYPE ARRAY Schema of the elements of Type.ARRAY.

Schema is used to define the format of input/output data.

Represents a select subset of an [OpenAPI 3.0 schema
object](https://spec.openapis.org/oas/v3.0.3#schema-object). More fields may

Optional. Maximum number of the elements for Type.ARRAY.

Optional. Maximum length of the Type.STRING

Optional. Maximum number of the properties for Type.OBJECT.

Optional. Maximum value of the Type.INTEGER and Type.NUMBER

Optional. Minimum number of the elements for Type.ARRAY.

Optional. SCHEMA FIELDS FOR TYPE STRING Minimum length of the Type.STRING

Optional. Minimum number of the properties for Type.OBJECT.

Optional. SCHEMA FIELDS FOR TYPE INTEGER and NUMBER Minimum value of the Type.INTEGER and Type.NUMBER

Optional. Indicates if the value may be null.

Optional. Pattern of the Type.STRING to restrict a string to a regular expression.

Optional. SCHEMA FIELDS FOR TYPE OBJECT Properties of Type.OBJECT.

Each additional property must conform to the following schema

Schema is used to define the format of input/output data.

Represents a select subset of an [OpenAPI 3.0 schema
object](https://spec.openapis.org/oas/v3.0.3#schema-object). More fields may

Optional. The order of the properties. Not a standard field in open api spec. Only used to support the order of the properties.

Optional. Required properties of Type.OBJECT.

Optional. The title of the Schema.

Optional. The type of the data.

Optional. The type of the data.

Optional. Output schema of the generated response.

This is an alternative to `response_schema`

that accepts [JSON
Schema](https://json-schema.org/). If set,

`response_schema`

must be`response_mime_type`

is required. While the full JSON Schema`$id`

- `$defs`

- `$ref`

- `$anchor`

`type`

- `format`

- `title`

- `description`

- `enum`

(for strings and`items`

- `prefixItems`

- `minItems`

- `maxItems`

- `minimum`

-`maximum`

- `anyOf`

- `oneOf`

(interpreted the same as `anyOf`

) -`properties`

- `additionalProperties`

- `required`

The non-standard`propertyOrdering`

property may also be set. Cyclic references are`$ref`

is set on a sub-schema, no other properties, except for than those`$`

, may be set.Configuration for model router requests.

The configuration for routing the request to a specific model.

No Additional PropertiesAutomated routing.

When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

No Additional PropertiesThe model routing preference.

Manual routing.

When manual routing is set, the specified model will be used directly.

No Additional PropertiesThe model name to use. Only the public LLM models are accepted. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/inference#supported-models).

Configuration for model selection.

Config for model selection.

No Additional PropertiesOptions for feature selection preference.

Options for feature selection preference.

Safety settings in the request to block unsafe content in the

response.

Safety settings.

No Additional PropertiesDetermines if the harm block method uses probability or probability

and severity scores.

Optional.

Specify if the threshold is used for probability or severity score. If not

specified, the threshold is used for probability score.

Required. Harm category.

Required. Harm category.

Required. The harm block threshold.

Required. The harm block threshold.

Code that enables the system to interact with external systems to

perform an action outside of the knowledge and scope of the model.

Tool details of a tool that the model may use to generate a response.

No Additional PropertiesList of function declarations that the tool supports.

Defines a function that the model can generate JSON inputs for.

The inputs are based on ```
OpenAPI 3.0 specifications
<https://spec.openapis.org/oas/v3.0.3>
```

_.

Defines the function behavior.

Defines the function behavior. Defaults to `BLOCKING`

.

Optional. Description and purpose of the function. Model uses it to decide how and whether to call the function.

Required. The name of the function to call. Must start with a letter or an underscore. Must be a-z, A-Z, 0-9, or contain underscores, dots and dashes, with a maximum length of 64.

Optional. Describes the parameters to this function in JSON Schema Object format. Reflects the Open API 3.03 Parameter Object. string Key: the name of the parameter. Parameter names are case sensitive. Schema Value: the Schema defining the type used for the parameter. For function with no parameters, this can be left unset. Parameter names must start with a letter or an underscore and must only contain chars a-z, A-Z, 0-9, or underscores with a maximum length of 64. Example with 1 required and 1 optional parameter: type: OBJECT properties: param1: type: STRING param2: type: INTEGER required: - param1

Schema is used to define the format of input/output data.

Represents a select subset of an [OpenAPI 3.0 schema
object](https://spec.openapis.org/oas/v3.0.3#schema-object). More fields may

Optional. Describes the parameters to the function in JSON Schema format. The schema must describe an object where the properties are the parameters to the function. For example: `{ "type": "object", "properties": { "name": { "type": "string" }, "age": { "type": "integer" } }, "additionalProperties": false, "required": ["name", "age"], "propertyOrdering": ["name", "age"] }`

This field is mutually exclusive with `parameters`

.

Optional. Describes the output from this function in JSON Schema format. Reflects the Open API 3.03 Response Object. The Schema defines the type used for the response value of the function.

Schema is used to define the format of input/output data.

Represents a select subset of an [OpenAPI 3.0 schema
object](https://spec.openapis.org/oas/v3.0.3#schema-object). More fields may

Optional. Describes the output from this function in JSON Schema format. The value specified by the schema is the response value of the function. This field is mutually exclusive with `response`

.

Optional. Retrieval tool type. System will always execute the provided retrieval tool(s) to get external knowledge to answer the prompt. Retrieval results are presented to the model for generation.

Defines a retrieval tool that model can call to access external knowledge.

No Additional PropertiesOptional. Deprecated. This option is no longer supported.

Use data source powered by external API for grounding.

Retrieve from data source powered by external API for grounding.

The external API is not owned by Google, but need to follow the pre-defined

API spec.

The authentication config to access the API. Deprecated. Please use auth_config instead.

The generic reusable api auth config.

Deprecated. Please use AuthConfig (google/cloud/aiplatform/master/auth.proto)

instead.

The API secret.

The API secret.

No Additional PropertiesRequired. The SecretManager secret version resource name storing API key. e.g. projects/{project}/secrets/{secret}/versions/{version}

The API key string. Either this or `api_key_secret_version`

must be set.

The API spec that the external API implements.

The API spec that the external API implements.

The authentication config to access the API.

Auth configuration to run the extension.

No Additional PropertiesConfig for API key auth.

Config for authentication with API key.

No Additional PropertiesThe API key to be used in the request directly.

Type of auth scheme.

Type of auth scheme.

Config for Google Service Account auth.

Config for Google Service Account Authentication.

No Additional PropertiesOptional. The service account that the extension execution service runs as. - If the service account is specified, the `iam.serviceAccounts.getAccessToken`

permission should be granted to Vertex AI Extension Service Agent (https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents) on the specified service account. - If not specified, the Vertex AI Extension Service Agent will be used to execute the Extension.

Config for HTTP Basic auth.

Config for HTTP Basic Authentication.

No Additional PropertiesRequired. The name of the SecretManager secret version resource storing the base64 encoded credentials. Format: `projects/{project}/secrets/{secrete}/versions/{version}`

- If specified, the `secretmanager.versions.access`

permission should be granted to Vertex AI Extension Service Agent (https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents) on the specified resource.

Config for user oauth.

Config for user oauth.

No Additional PropertiesAccess token for extension endpoint. Only used to propagate token from [[ExecuteExtensionRequest.runtime*auth*config]] at request time.

The service account used to generate access tokens for executing the Extension. - If the service account is specified, the `iam.serviceAccounts.getAccessToken`

permission should be granted to Vertex AI Extension Service Agent (https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents) on the provided service account.

Config for user OIDC auth.

Config for user OIDC auth.

No Additional PropertiesOpenID Connect formatted ID token for extension endpoint. Only used to propagate token from [[ExecuteExtensionRequest.runtime*auth*config]] at request time.

The service account used to generate an OpenID Connect (OIDC)-compatible JWT token signed by the Google OIDC Provider (accounts.google.com) for extension endpoint (https://cloud.google.com/iam/docs/create-short-lived-credentials-direct#sa-credentials-oidc). - The audience for the token will be set to the URL in the server url defined in the OpenApi spec. - If the service account is provided, the service account should grant `iam.serviceAccounts.getOpenIdToken`

permission to Vertex AI Extension Service Agent (https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents).

Parameters for the elastic search API.

The search parameters to use for the ELASTIC_SEARCH spec.

No Additional PropertiesThe ElasticSearch index to use.

Optional. Number of hits (chunks) to request. When specified, it is passed to Elasticsearch as the `num_hits`

param.

The ElasticSearch search template to use.

The endpoint of the external API. The system will call the API at this endpoint to retrieve the data for grounding. Example: https://acme.com:443/search

Parameters for the simple search API.

The search parameters to use for SIMPLE_SEARCH spec.

Set to use data source powered by Vertex AI Search.

Retrieve from Vertex AI Search datastore or engine for grounding.

datastore and engine are mutually exclusive. See

https://cloud.google.com/products/agent-builder

Specifications that define the specific DataStores to be searched, along with configurations for those data stores. This is only considered for Engines with multiple data stores. It should only be set if engine is used.

Define data stores within engine to filter on in a search call and configurations for those data stores.

For more information, see

https://cloud.google.com/generative-ai-app-builder/docs/reference/rpc/google.cloud.discoveryengine.v1#datastorespec

Full resource name of DataStore, such as Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`


Optional. Filter specification to filter documents in the data store specified by data_store field. For more information on filtering, see [Filtering](https://cloud.google.com/generative-ai-app-builder/docs/filter-search-metadata)

Optional. Fully-qualified Vertex AI Search data store resource ID. Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`


Optional. Fully-qualified Vertex AI Search engine resource ID. Format: `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}`


Optional. Filter strings to be passed to the search API.

Optional. Number of search results to return per query. The default value is 10. The maximumm allowed value is 10.

Set to use data source powered by Vertex RAG store. User data is uploaded via the VertexRagDataService.

Retrieve from Vertex RAG Store for grounding.

No Additional PropertiesOptional. Deprecated. Please use rag_resources instead.

Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support.

The definition of the Rag resource.

No Additional PropertiesOptional. RagCorpora resource name. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`


Optional. rag*file*id. The files should be in the same rag*corpus set in rag*corpus field.

Optional. The retrieval config for the Rag query.

Specifies the context retrieval config.

No Additional PropertiesOptional. Config for filters.

Config for filters.

No Additional PropertiesOptional. String for metadata filtering.

Optional. Only returns contexts with vector distance smaller than the threshold.

Optional. Only returns contexts with vector similarity larger than the threshold.

Optional. Config for Hybrid Search.

Config for Hybrid Search.

No Additional PropertiesOptional. Alpha value controls the weight between dense and sparse vector search results. The range is [0, 1], while 0 means sparse vector search only and 1 means dense vector search only. The default value is 0.5 which balances sparse and dense vector search equally.

Optional. Config for ranking and reranking.

Config for ranking and reranking.

No Additional PropertiesOptional. Config for LlmRanker.

Config for LlmRanker.

No Additional PropertiesOptional. The model name used for ranking. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/inference#supported-models).

Optional. Config for Rank Service.

Config for Rank Service.

No Additional PropertiesOptional. The model name of the rank service. Format: `semantic-ranker-512@latest`


Optional. The number of contexts to retrieve.

Optional. Number of top k results to return from the selected corpora.

Optional. Currently only supported for Gemini Multimodal Live API. In Gemini Multimodal Live API, if `store_context`

bool is specified, Gemini will leverage it to automatically memorize the interactions between the client and Gemini, and retrieve context when needed to augment the response generation for users' ongoing and future interactions.

Optional. Only return results with vector distance smaller than the threshold.

Optional. Google Search tool type. Specialized retrieval tool

that is powered by Google Search.

Tool to support Google Search in Model. Powered by Google.

No Additional PropertiesOptional. Filter search results to a specific time range.

If customers set a start time, they must set an end time (and vice versa).

Represents a time interval, encoded as a start time (inclusive) and an end time (exclusive).

The start time must be less than or equal to the end time.

When the start equals the end time, the interval is an empty interval.

(matches no time)

When both start and end are unspecified, the interval matches any time.

The start time of the interval.

The end time of the interval.

Optional. GoogleSearchRetrieval tool type. Specialized retrieval tool that is powered by Google search.

Tool to retrieve public web data for grounding, powered by Google.

No Additional PropertiesSpecifies the dynamic retrieval configuration for the given source.

Describes the options to customize dynamic retrieval.

No Additional PropertiesThe mode of the predictor to be used in dynamic retrieval.

Config for the dynamic retrieval config mode.

Optional. The threshold to be used in dynamic retrieval. If not set, a system default value is used.

Optional. Enterprise web search tool type. Specialized retrieval

tool that is powered by Vertex AI Search and Sec4 compliance.

Tool to search public web data, powered by Vertex AI Search and Sec4 compliance.

Optional. Google Maps tool type. Specialized retrieval tool

that is powered by Google Maps.

Tool to support Google Maps in Model.

No Additional PropertiesOptional. Auth config for the Google Maps tool.

Optional. Tool to support URL context retrieval.

Tool to support URL context retrieval.

Optional. CodeExecution tool type. Enables the model to execute code as part of generation.

Tool that executes code generated by the model, and automatically returns the result to the model.

See also [ExecutableCode]and [CodeExecutionResult] which are input and output

to this tool.

Optional. Tool to support the model interacting directly with the computer. If enabled, it automatically populates computer-use specific Function Declarations.

Tool to support computer use.

No Additional PropertiesRequired. The environment being operated.

Required. The environment being operated.

Definition for a tool the client can call.

Additional Properties of any type are allowed.

Type: objectAdditional Properties of any type are allowed.

Type: objectAdditional properties describing a Tool to clients.

NOTE: all properties in ToolAnnotations are **hints**.

They are not guaranteed to provide a faithful description of

tool behavior (including descriptive properties like `title`

).

Clients should never make tool use decisions based on ToolAnnotations

received from untrusted servers.

Additional Properties of any type are allowed.

Type: objectAdditional Properties of any type are allowed.

Type: objectAdditional Properties of any type are allowed.

Type: objectAssociates model output to a specific function call.

Tool config.

This config is shared for all tools provided in the request.

No Additional PropertiesOptional. Function calling config.

Function calling config.

No Additional PropertiesOptional. Function calling mode.

Config for the function calling config mode.

Optional. Function names to call. Only set when the Mode is ANY. Function names should match [FunctionDeclaration.name]. With mode set to ANY, model will predict a function call from the set of function names provided.

Optional. Retrieval config.

Retrieval config.

No Additional PropertiesOptional. The location of the user.

An object that represents a latitude/longitude pair.

This is expressed as a pair of doubles to represent degrees latitude and

degrees longitude. Unless specified otherwise, this object must conform to the

<a href="https://en.wikipedia.org/wiki/World_Geodetic_System#1984_version">

WGS84 standard</a>. Values must be within normalized ranges.

The latitude in degrees. It must be in the range [-90.0, +90.0].

The longitude in degrees. It must be in the range [-180.0, +180.0]

The language code of the user.

Labels with user-defined metadata to break down billed charges.

Each additional property must conform to the following schema

Type: stringResource name of a context cache that can be used in subsequent

requests.

The requested modalities of the response. Represents the set of

modalities that the model can return.

If specified, the media resolution specified will be used.

The media resolution to use.

The speech generation configuration.

The speech generation configuration.

No Additional PropertiesThe configuration for the speaker to use.

The configuration for the voice to use.

No Additional PropertiesThe configuration for the speaker to use.

The configuration for the prebuilt speaker to use.

No Additional PropertiesThe name of the prebuilt voice to use.

The configuration for the multi-speaker setup.

It is mutually exclusive with the voice_config field.

The configuration for the multi-speaker setup.

No Additional PropertiesThe configuration for the speaker to use.

The configuration for the speaker to use.

No Additional PropertiesThe name of the speaker to use. Should be the same as in the

prompt.

The configuration for the voice to use.

Language code (ISO 639. e.g. en-US) for the speech synthesization.

Only available for Live API.

If enabled, audio timestamp will be included in the request to the

model.

The configuration for automatic function calling.

The configuration for automatic function calling.

No Additional PropertiesWhether to disable automatic function calling.

If not set or set to False, will enable automatic function calling.

If set to True, will disable automatic function calling.

If automatic function calling is enabled,

maximum number of remote calls for automatic function calling.

This number should be a positive integer.

If not set, SDK will set maximum number of remote calls to 10.

The thinking features configuration.

The thinking features configuration.

No Additional PropertiesIndicates whether to include thoughts in the response. If true, thoughts are returned only if the model supports thought and thoughts are available.

Indicates the thinking budget in tokens. 0 is DISABLED. -1 is AUTOMATIC. The default values and allowed ranges are model dependent.

The config for the YAML schema of a LoopAgent.

No Additional PropertiesThe value is used to uniquely identify the LoopAgent class.

Specific value:`"LoopAgent"`

Required. The name of the agent.

Optional. The description of the agent.

Optional. The sub-agents of the agent.

The config for the reference to another agent.

Optional. The before*agent*callbacks of the agent.

Example:


```
before_agent_callbacks:
- name: my_library.security_callbacks.before_agent_callback
```


Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. The after*agent*callbacks of the agent.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. LoopAgent.max_iterations.

The config for the YAML schema of a ParallelAgent.

No Additional PropertiesThe value is used to uniquely identify the ParallelAgent class.

Specific value:`"ParallelAgent"`

Required. The name of the agent.

Optional. The description of the agent.

Optional. The sub-agents of the agent.

The config for the reference to another agent.

Optional. The before*agent*callbacks of the agent.

Example:


```
before_agent_callbacks:
- name: my_library.security_callbacks.before_agent_callback
```


Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. The after*agent*callbacks of the agent.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

The config for the YAML schema of a SequentialAgent.

No Additional PropertiesThe value is used to uniquely identify the SequentialAgent class.

Specific value:`"SequentialAgent"`

Required. The name of the agent.

Optional. The description of the agent.

Optional. The sub-agents of the agent.

The config for the reference to another agent.

Optional. The before*agent*callbacks of the agent.

Example:


```
before_agent_callbacks:
- name: my_library.security_callbacks.before_agent_callback
```


Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. The after*agent*callbacks of the agent.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

The config for the YAML schema of a BaseAgent.

Do not use this class directly. It's the base class for all agent configs.

Required. The class of the agent. The value is used to differentiate among different agent classes.

`"BaseAgent"`

Required. The name of the agent.

Optional. The description of the agent.

Optional. The sub-agents of the agent.

The config for the reference to another agent.

Optional. The before*agent*callbacks of the agent.

Example:


```
before_agent_callbacks:
- name: my_library.security_callbacks.before_agent_callback
```


Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. The after*agent*callbacks of the agent.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Additional Properties of any type are allowed.

Type: object


---

<!-- DOCUMENTO FUSIONADO: _typescript_all.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 3 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _enums_merged.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 3 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: loglevelhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/enums/LogLevel.html -->

# Enumeration LogLevel

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
LogLevel
Enumeration LogLevel
Log levels for the logger.
Enumeration Members
DEBUG
DEBUG
:
0
ERROR
ERROR
:
3
INFO
INFO
:
1
WARN
WARN
:
2
Enumeration Members
DEBUG
ERROR
INFO
WARN
ADK for TypeScript: API Reference
Loading...

Log levels for the logger.


---

<!-- DOCUMENTO FUSIONADO: streamingmodehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/enums/StreamingMode.html -->

# Enumeration StreamingMode

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
StreamingMode
Enumeration StreamingMode
The streaming mode for the run config.
Enumeration Members
BIDI
BIDI
:
"bidi"
NONE
NONE
:
"none"
SSE
SSE
:
"sse"
Enumeration Members
BIDI
NONE
SSE
ADK for TypeScript: API Reference
Loading...

The streaming mode for the run config.


---

<!-- DOCUMENTO FUSIONADO: policyoutcomehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/enums/PolicyOutcome.html -->

# Enumeration PolicyOutcome

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
PolicyOutcome
Enumeration PolicyOutcome
The outcome of a policy check.
Enumeration Members
ALLOW
ALLOW
:
"ALLOW"
CONFIRM
CONFIRM
:
"CONFIRM"
DENY
DENY
:
"DENY"
Enumeration Members
ALLOW
CONFIRM
DENY
ADK for TypeScript: API Reference
Loading...

The outcome of a policy check.


---

<!-- DOCUMENTO FUSIONADO: _typescript_merged.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/ -->

# ADK for TypeScript: API Reference

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
ADK for TypeScript: API Reference
Enumerations
LogLevel
PolicyOutcome
StreamingMode
Classes
AgentTool
BaseAgent
BaseLlm
BasePlugin
BaseSessionService
BaseTool
BaseToolset
CallbackContext
FunctionTool
GcsArtifactService
Gemini
InMemoryArtifactService
InMemoryMemoryService
InMemoryPolicyEngine
InMemoryRunner
InMemorySessionService
InvocationContext
LiveRequestQueue
LlmAgent
LLMRegistry
LoggingPlugin
LongRunningFunctionTool
LoopAgent
MCPSessionManager
MCPTool
MCPToolset
ParallelAgent
PluginManager
Runner
SecurityPlugin
SequentialAgent
ToolConfirmation
ToolContext
Interfaces
AppendEventRequest
BaseArtifactService
BaseCredentialService
BaseLlmConnection
BaseMemoryService
BasePolicyEngine
BaseToolParams
CreateSessionRequest
DeleteArtifactRequest
DeleteSessionRequest
Event
EventActions
GeminiParams
GetSessionConfig
GetSessionRequest
ListArtifactKeysRequest
ListSessionsRequest
ListSessionsResponse
ListVersionsRequest
LiveRequest
LlmRequest
LlmResponse
LoadArtifactRequest
OtelExportersConfig
OTelHooks
PolicyCheckResult
RunAsyncToolRequest
RunConfig
SaveArtifactRequest
SearchMemoryRequest
SearchMemoryResponse
Session
StdioConnectionParams
StreamableHTTPConnectionParams
ToolCallPolicyContext
ToolProcessLlmRequest
Type Aliases
AfterModelCallback
AfterToolCallback
BeforeModelCallback
BeforeToolCallback
MCPConnectionParams
SingleAfterModelCallback
SingleAfterToolCallback
SingleBeforeModelCallback
SingleBeforeToolCallback
Variables
functionsExportedForTestingOnly
GOOGLE_SEARCH
REQUEST_CONFIRMATION_FUNCTION_CALL_NAME
Functions
createEvent
createEventActions
createSession
getAskUserConfirmationFunctionCalls
getFunctionCalls
getFunctionResponses
getGcpExporters
getGcpResource
hasTrailingCodeExecutionResult
isFinalResponse
maybeSetOtelProviders
setLogLevel
stringifyContent
zodObjectToSchema
Enumerations
Log
Level
Policy
Outcome
Streaming
Mode
Classes
Agent
Tool
Base
Agent
Base
Llm
Base
Plugin
Base
Session
Service
Base
Tool
Base
Toolset
Callback
Context
Function
Tool
Gcs
Artifact
Service
Gemini
In
Memory
Artifact
Service
In
Memory
Memory
Service
In
Memory
Policy
Engine
In
Memory
Runner
In
Memory
Session
Service
Invocation
Context
Live
Request
Queue
Llm
Agent
LLM
Registry
Logging
Plugin
Long
Running
Function
Tool
Loop
Agent
MCP
Session
Manager
MCP
Tool
MCP
Toolset
Parallel
Agent
Plugin
Manager
Runner
Security
Plugin
Sequential
Agent
Tool
Confirmation
Tool
Context
Interfaces
Append
Event
Request
Base
Artifact
Service
Base
Credential
Service
Base
Llm
Connection
Base
Memory
Service
Base
Policy
Engine
Base
Tool
Params
Create
Session
Request
Delete
Artifact
Request
Delete
Session
Request
Event
Event
Actions
Gemini
Params
Get
Session
Config
Get
Session
Request
List
Artifact
Keys
Request
List
Sessions
Request
List
Sessions
Response
List
Versions
Request
Live
Request
Llm
Request
Llm
Response
Load
Artifact
Request
Otel
Exporters
Config
O
Tel
Hooks
Policy
Check
Result
Run
Async
Tool
Request
Run
Config
Save
Artifact
Request
Search
Memory
Request
Search
Memory
Response
Session
Stdio
Connection
Params
Streamable
HTTP
Connection
Params
Tool
Call
Policy
Context
Tool
Process
Llm
Request
Type Aliases
After
Model
Callback
After
Tool
Callback
Before
Model
Callback
Before
Tool
Callback
MCP
Connection
Params
Single
After
Model
Callback
Single
After
Tool
Callback
Single
Before
Model
Callback
Single
Before
Tool
Callback
Variables
functions
Exported
For
Testing
Only
GOOGLE_
SEARCH
REQUEST_
CONFIRMATION_
FUNCTION_
CALL_
NAME
Functions
create
Event
create
Event
Actions
create
Session
get
Ask
User
Confirmation
Function
Calls
get
Function
Calls
get
Function
Responses
get
Gcp
Exporters
get
Gcp
Resource
has
Trailing
Code
Execution
Result
is
Final
Response
maybe
Set
Otel
Providers
set
Log
Level
stringify
Content
zod
Object
To
Schema
ADK for TypeScript: API Reference
Loading...


---

<!-- DOCUMENTO FUSIONADO: indexhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/index.html -->

# ADK for TypeScript: API Reference

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
ADK for TypeScript: API Reference
Enumerations
LogLevel
PolicyOutcome
StreamingMode
Classes
AgentTool
BaseAgent
BaseLlm
BasePlugin
BaseSessionService
BaseTool
BaseToolset
CallbackContext
FunctionTool
GcsArtifactService
Gemini
InMemoryArtifactService
InMemoryMemoryService
InMemoryPolicyEngine
InMemoryRunner
InMemorySessionService
InvocationContext
LiveRequestQueue
LlmAgent
LLMRegistry
LoggingPlugin
LongRunningFunctionTool
LoopAgent
MCPSessionManager
MCPTool
MCPToolset
ParallelAgent
PluginManager
Runner
SecurityPlugin
SequentialAgent
ToolConfirmation
ToolContext
Interfaces
AppendEventRequest
BaseArtifactService
BaseCredentialService
BaseLlmConnection
BaseMemoryService
BasePolicyEngine
BaseToolParams
CreateSessionRequest
DeleteArtifactRequest
DeleteSessionRequest
Event
EventActions
GeminiParams
GetSessionConfig
GetSessionRequest
ListArtifactKeysRequest
ListSessionsRequest
ListSessionsResponse
ListVersionsRequest
LiveRequest
LlmRequest
LlmResponse
LoadArtifactRequest
OtelExportersConfig
OTelHooks
PolicyCheckResult
RunAsyncToolRequest
RunConfig
SaveArtifactRequest
SearchMemoryRequest
SearchMemoryResponse
Session
StdioConnectionParams
StreamableHTTPConnectionParams
ToolCallPolicyContext
ToolProcessLlmRequest
Type Aliases
AfterModelCallback
AfterToolCallback
BeforeModelCallback
BeforeToolCallback
MCPConnectionParams
SingleAfterModelCallback
SingleAfterToolCallback
SingleBeforeModelCallback
SingleBeforeToolCallback
Variables
functionsExportedForTestingOnly
GOOGLE_SEARCH
REQUEST_CONFIRMATION_FUNCTION_CALL_NAME
Functions
createEvent
createEventActions
createSession
getAskUserConfirmationFunctionCalls
getFunctionCalls
getFunctionResponses
getGcpExporters
getGcpResource
hasTrailingCodeExecutionResult
isFinalResponse
maybeSetOtelProviders
setLogLevel
stringifyContent
zodObjectToSchema
Enumerations
Log
Level
Policy
Outcome
Streaming
Mode
Classes
Agent
Tool
Base
Agent
Base
Llm
Base
Plugin
Base
Session
Service
Base
Tool
Base
Toolset
Callback
Context
Function
Tool
Gcs
Artifact
Service
Gemini
In
Memory
Artifact
Service
In
Memory
Memory
Service
In
Memory
Policy
Engine
In
Memory
Runner
In
Memory
Session
Service
Invocation
Context
Live
Request
Queue
Llm
Agent
LLM
Registry
Logging
Plugin
Long
Running
Function
Tool
Loop
Agent
MCP
Session
Manager
MCP
Tool
MCP
Toolset
Parallel
Agent
Plugin
Manager
Runner
Security
Plugin
Sequential
Agent
Tool
Confirmation
Tool
Context
Interfaces
Append
Event
Request
Base
Artifact
Service
Base
Credential
Service
Base
Llm
Connection
Base
Memory
Service
Base
Policy
Engine
Base
Tool
Params
Create
Session
Request
Delete
Artifact
Request
Delete
Session
Request
Event
Event
Actions
Gemini
Params
Get
Session
Config
Get
Session
Request
List
Artifact
Keys
Request
List
Sessions
Request
List
Sessions
Response
List
Versions
Request
Live
Request
Llm
Request
Llm
Response
Load
Artifact
Request
Otel
Exporters
Config
O
Tel
Hooks
Policy
Check
Result
Run
Async
Tool
Request
Run
Config
Save
Artifact
Request
Search
Memory
Request
Search
Memory
Response
Session
Stdio
Connection
Params
Streamable
HTTP
Connection
Params
Tool
Call
Policy
Context
Tool
Process
Llm
Request
Type Aliases
After
Model
Callback
After
Tool
Callback
Before
Model
Callback
Before
Tool
Callback
MCP
Connection
Params
Single
After
Model
Callback
Single
After
Tool
Callback
Single
Before
Model
Callback
Single
Before
Tool
Callback
Variables
functions
Exported
For
Testing
Only
GOOGLE_
SEARCH
REQUEST_
CONFIRMATION_
FUNCTION_
CALL_
NAME
Functions
create
Event
create
Event
Actions
create
Session
get
Ask
User
Confirmation
Function
Calls
get
Function
Calls
get
Function
Responses
get
Gcp
Exporters
get
Gcp
Resource
has
Trailing
Code
Execution
Result
is
Final
Response
maybe
Set
Otel
Providers
set
Log
Level
stringify
Content
zod
Object
To
Schema
ADK for TypeScript: API Reference
Loading...


---

<!-- DOCUMENTO FUSIONADO: _classes_merged.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 28 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: inmemoryrunnerhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/InMemoryRunner.html -->

# Class InMemoryRunner

Readonly

Optional

Runs the agent with the given message, and returns an async generator of events.

The user ID of the session.

The events generated by the agent.

Runs the agent with the given message, and returns an async generator of events.


---

<!-- DOCUMENTO FUSIONADO: llmregistryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/LLMRegistry.html -->

# Class LLMRegistry

Registry for LLMs.

Static

Creates a new LLM instance.

The model name.

The LLM instance.

Registers a new LLM class.

The class that implements the model.

Resolves the model to a BaseLlm subclass.

The BaseLlm subclass.

If the model is not found.

Registry for LLMs.


---

<!-- DOCUMENTO FUSIONADO: functiontoolhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/FunctionTool.html -->

# Class FunctionTool<TParameters>

The constructor acts as the user-friendly factory.

The configuration for the tool.

`Readonly`

description`Readonly`

is`Readonly`

nameThe Google API LLM variant to use.

Provide a schema for the function.

Processes the outgoing LLM request for this tool.

Use cases:

The request to process the LLM request.

The base class for all tools.


---

<!-- DOCUMENTO FUSIONADO: longrunningfunctiontoolhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/LongRunningFunctionTool.html -->

# Class LongRunningFunctionTool<TParameters>

The constructor acts as the user-friendly factory.

The configuration for the tool.

`Readonly`

description`Readonly`

is`Readonly`

nameThe Google API LLM variant to use.

Provide a schema for the function.

Processes the outgoing LLM request for this tool.

Use cases:

The request to process the LLM request.

The base class for all tools.


---

<!-- DOCUMENTO FUSIONADO: inmemorymemoryservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/InMemoryMemoryService.html -->

# Class InMemoryMemoryService

Adds a session to the memory.

The session to add to the memory.

A promise that resolves when the session is added to the memory.

Searches for sessions that match the query.

A promise that resolves to SearchMemoryResponse containing the matching memories.

An in-memory memory service for prototyping purpose only.

Uses keyword matching instead of semantic search.


---

<!-- DOCUMENTO FUSIONADO: inmemorypolicyenginehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/InMemoryPolicyEngine.html -->

# Class InMemoryPolicyEngine

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
InMemoryPolicyEngine
Class InMemoryPolicyEngine
Implements
BasePolicyEngine
Constructors
constructor
new
InMemoryPolicyEngine
()
:
InMemoryPolicyEngine
Returns
InMemoryPolicyEngine
Methods
evaluate
evaluate
(
context
:
ToolCallPolicyContext
)
:
Promise
<
PolicyCheckResult
>
Parameters
context
:
ToolCallPolicyContext
Returns
Promise
<
PolicyCheckResult
>
Constructors
constructor
Methods
evaluate
ADK for TypeScript: API Reference
Loading...


---

<!-- DOCUMENTO FUSIONADO: geminihtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/Gemini.html -->

# Class Gemini

The parameters for creating a Gemini instance.

`Readonly`

model`Static`

`Readonly`

supportedA list of model name patterns that are supported by this LLM.

Connects to the Gemini model and returns an llm connection.

LlmRequest, the request to send to the Gemini model.

BaseLlmConnection, the connection to the Gemini model.

Sends a request to the Gemini model.

LlmRequest, the request to send to the Gemini model.

bool = false, whether to do streaming call.

Appends a user content, so that model can continue to output.

LlmRequest, the request to send to the LLM.

Integration for Gemini models.


---

<!-- DOCUMENTO FUSIONADO: callbackcontexthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/CallbackContext.html -->

# Class CallbackContext

The current agent name.

The current invocation id.

The delta-aware state of the current session.

The user content that started this invocation.

Loads an artifact attached to the current session.

The filename of the artifact.

`Optional`

version: numberThe version of the artifact. If not provided, the latest version will be used.

A promise that resolves to the loaded artifact.

Saves an artifact attached to the current session.

The filename of the artifact.

The artifact to save.

A promise that resolves to the version of the saved artifact.

The context of various callbacks within an agent run.


---

<!-- DOCUMENTO FUSIONADO: inmemorysessionservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/InMemorySessionService.html -->

# Class InMemorySessionService

Appends an event to a session.

The request to append an event.

A promise that resolves to the event that was appended.

Creates a new session.

The request to create a session.

A promise that resolves to the newly created session instance.

Deletes a session.

The request to delete a session.

A promise that resolves when the session is deleted.

Gets a session.

The request to get a session.

A promise that resolves to the session instance or undefined if not found.

Lists sessions for a user.

The request to list sessions.

A promise that resolves to a list of sessions for the user.

An in-memory implementation of the session service.


---

<!-- DOCUMENTO FUSIONADO: liverequestqueuehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/LiveRequestQueue.html -->

# Class LiveRequestQueue

Implements the async iterator protocol.

Sends a close signal to the queue.

Retrieves a request from the queue. If the queue is empty, it will wait until a request is available.

A promise that resolves with the next available request.

Adds a request to the queue. If there is a pending `get()`

call, it
will be resolved with the given request.

The request to send.

Sends an activity end signal to mark the end of user input.

Sends an activity start signal to mark the beginning of user input.

Sends a content object to the queue.

The content to send.

Sends a blob to the model in realtime mode.

The blob to send.

Queue used to send LiveRequest in a live (bidirectional streaming) way.


---

<!-- DOCUMENTO FUSIONADO: basetoolhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/BaseTool.html -->

# Class BaseToolAbstract

`Abstract`

Base constructor for a tool.

The parameters for `BaseTool`

.

`Readonly`

description`Readonly`

is`Readonly`

nameThe Google API LLM variant to use.

Gets the OpenAPI specification of this tool in the form of a FunctionDeclaration.

NOTE

`processLlmRequest`

to add function declaration to LLM request.The FunctionDeclaration of this tool, or undefined if it doesn't need to be added to LlmRequest.config.

Processes the outgoing LLM request for this tool.

Use cases:

The request to process the LLM request.

`Abstract`

runRuns the tool with the given arguments and context.

NOTE

The request to run the tool.

A promise that resolves to the tool response.

The base class for all tools.


---

<!-- DOCUMENTO FUSIONADO: basellmhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/BaseLlm.html -->

# Class BaseLlmAbstract

`Abstract`

Creates an instance of BaseLLM.

The parameters for creating a BaseLlm instance.

The name of the LLM, e.g. gemini-1.5-flash or gemini-1.5-flash-001.

`Readonly`

model`Static`

`Readonly`

supportedList of supported models in regex for LlmRegistry.

`Abstract`

connectCreates a live connection to the LLM.

LlmRequest, the request to send to the LLM.

A live connection to the LLM.

`Abstract`

generateGenerates one content from the given contents and tools.

LlmRequest, the request to send to the LLM.

`Optional`

stream: booleanwhether to do streaming call. For non-streaming call, it will only yield one Content.

A generator of LlmResponse.

Appends a user content, so that model can continue to output.

LlmRequest, the request to send to the LLM.

The BaseLLM class.


---

<!-- DOCUMENTO FUSIONADO: basesessionservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/BaseSessionService.html -->

# Class BaseSessionServiceAbstract

`Abstract`

Appends an event to a session.

The request to append an event.

A promise that resolves to the event that was appended.

`Abstract`

createCreates a new session.

The request to create a session.

A promise that resolves to the newly created session instance.

`Abstract`

deleteDeletes a session.

The request to delete a session.

A promise that resolves when the session is deleted.

`Abstract`

getGets a session.

The request to get a session.

A promise that resolves to the session instance or undefined if not found.

`Abstract`

listLists sessions for a user.

The request to list sessions.

A promise that resolves to a list of sessions for the user.

Base class for session services.

The service provides a set of methods for managing sessions and events.


---

<!-- DOCUMENTO FUSIONADO: agenttoolhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/AgentTool.html -->

# Class AgentTool

`Readonly`

description`Readonly`

is`Readonly`

nameThe Google API LLM variant to use.

Gets the OpenAPI specification of this tool in the form of a FunctionDeclaration.

NOTE

`processLlmRequest`

to add function declaration to LLM request.The FunctionDeclaration of this tool, or undefined if it doesn't need to be added to LlmRequest.config.

Processes the outgoing LLM request for this tool.

Use cases:

The request to process the LLM request.

Runs the tool with the given arguments and context.

NOTE

The request to run the tool.

A promise that resolves to the tool response.

A tool that wraps an agent.

This tool allows an agent to be called as a tool within a larger application. The agent's input schema is used to define the tool's input parameters, and the agent's output is returned as the tool's result.

## Param: config:

The configuration of the agent tool.


---

<!-- DOCUMENTO FUSIONADO: mcpsessionmanagerhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/MCPSessionManager.html -->

# Class MCPSessionManager

Manages Model Context Protocol (MCP) client sessions.

This class is responsible for establishing and managing connections to MCP
servers. It supports different transport protocols like Standard I/O (Stdio)
and Server-Sent Events (SSE) over HTTP, determined by the provided
connection parameters.

The primary purpose of this manager is to abstract away the details of
session creation and connection handling, providing a simple interface for
creating new MCP client instances that can be used to interact with
remote tools.

Manages Model Context Protocol (MCP) client sessions.

This class is responsible for establishing and managing connections to MCP servers. It supports different transport protocols like Standard I/O (Stdio) and Server-Sent Events (SSE) over HTTP, determined by the provided connection parameters.

The primary purpose of this manager is to abstract away the details of session creation and connection handling, providing a simple interface for creating new MCP client instances that can be used to interact with remote tools.


---

<!-- DOCUMENTO FUSIONADO: basetoolsethtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/BaseToolset.html -->

# Class BaseToolsetAbstract

`Abstract`

`Abstract`

closeCloses the toolset.

NOTE: This method is invoked, for example, at the end of an agent server's lifecycle or when the toolset is no longer needed. Implementations should ensure that any open connections, files, or other managed resources are properly released to prevent leaks.

A Promise that resolves when the toolset is closed.

`Abstract`

getReturns the tools that should be exposed to LLM.

`Optional`

context: ReadonlyContextContext used to filter tools available to the agent. If not defined, all tools in the toolset are returned.

A Promise that resolves to the list of tools.

`Protected`

isReturns whether the tool should be exposed to LLM.

The tool to check.

Context used to filter tools available to the agent.

Whether the tool should be exposed to LLM.

Processes the outgoing LLM request for this toolset. This method will be called before each tool processes the llm request.

Use cases:

The context of the tool.

The outgoing LLM request, mutable this method.

Base class for toolset.

A toolset is a collection of tools that can be used by an agent.


---

<!-- DOCUMENTO FUSIONADO: gcsartifactservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/GcsArtifactService.html -->

# Class GcsArtifactService

Deletes an artifact.

The request to delete an artifact.

A promise that resolves when the artifact is deleted.

Lists all the artifact filenames within a session.

The request to list artifact keys.

A promise that resolves to a list of all artifact filenames within a session.

Lists all versions of an artifact.

The request to list versions.

A promise that resolves to a list of all available versions of the artifact.

Gets an artifact from the artifact service storage.

The artifact is a file identified by the app name, user ID, session ID, and filename.

The request to load an artifact.

A promise that resolves to the artifact or undefined if not found.

Saves an artifact to the artifact service storage.

The artifact is a file identified by the app name, user ID, session ID, and filename. After saving the artifact, a revision ID is returned to identify the artifact version.

The request to save an artifact.

A promise that resolves to The revision ID. The first version of the artifact has a revision ID of 0. This is incremented by 1 after each successful save.

Interface for artifact services.


---

<!-- DOCUMENTO FUSIONADO: inmemoryartifactservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/InMemoryArtifactService.html -->

# Class InMemoryArtifactService

Deletes an artifact.

The request to delete an artifact.

A promise that resolves when the artifact is deleted.

Lists all the artifact filenames within a session.

The request to list artifact keys.

A promise that resolves to a list of all artifact filenames within a session.

Lists all versions of an artifact.

The request to list versions.

A promise that resolves to a list of all available versions of the artifact.

Gets an artifact from the artifact service storage.

The artifact is a file identified by the app name, user ID, session ID, and filename.

The request to load an artifact.

A promise that resolves to the artifact or undefined if not found.

Saves an artifact to the artifact service storage.

The artifact is a file identified by the app name, user ID, session ID, and filename. After saving the artifact, a revision ID is returned to identify the artifact version.

The request to save an artifact.

A promise that resolves to The revision ID. The first version of the artifact has a revision ID of 0. This is incremented by 1 after each successful save.

An in-memory implementation of the ArtifactService.


---

<!-- DOCUMENTO FUSIONADO: mcptoolhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/MCPTool.html -->

# Class MCPTool

`Readonly`

description`Readonly`

is`Readonly`

nameThe Google API LLM variant to use.

Gets the OpenAPI specification of this tool in the form of a FunctionDeclaration.

NOTE

`processLlmRequest`

to add function declaration to LLM request.The FunctionDeclaration of this tool, or undefined if it doesn't need to be added to LlmRequest.config.

Processes the outgoing LLM request for this tool.

Use cases:

The request to process the LLM request.

Runs the tool with the given arguments and context.

NOTE

The request to run the tool.

A promise that resolves to the tool response.

Represents a tool exposed via the Model Context Protocol (MCP).

This class acts as a wrapper around a tool definition received from an MCP server. It translates the MCP tool's schema into a format compatible with the Gemini AI platform (FunctionDeclaration) and handles the remote execution of the tool by communicating with the MCP server through an MCPSessionManager.

When an LLM decides to call this tool, the

`runAsync`

method will be invoked, which in turn establishes an MCP session, sends a`callTool`

request with the provided arguments, and returns the result from the remote tool.


---

<!-- DOCUMENTO FUSIONADO: pluginmanagerhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/PluginManager.html -->

# Class PluginManager

Initializes the plugin service.

`Optional`

plugins: An optional list of plugins to register upon initialization.

Retrieves a registered plugin by its name.

The name of the plugin to retrieve.

The plugin instance if found, otherwise `undefined`

.

Runs the `afterAgentCallback`

for all plugins.

Runs the `afterModelCallback`

for all plugins.

Runs the `afterRunCallback`

for all plugins.

Runs the `afterToolCallback`

for all plugins.

Runs the `beforeAgentCallback`

for all plugins.

Runs the `beforeModelCallback`

for all plugins.

Runs the `beforeRunCallback`

for all plugins.

Runs the `beforeToolCallback`

for all plugins.

Runs the `onEventCallback`

for all plugins.

Runs the `onModelErrorCallback`

for all plugins.

Runs the `onToolErrorCallback`

for all plugins.

Runs the `onUserMessageCallback`

for all plugins.

Manages the registration and execution of plugins.

The PluginManager is an internal class that orchestrates the invocation of plugin callbacks at key points in the SDK's execution lifecycle. It maintains a list of registered plugins and ensures they are called in the order they were registered.

The core execution logic implements an "early exit" strategy: if any plugin callback returns a non-

`undefined`

value, the execution of subsequent plugins for that specific event is halted, and the returned value is propagated up the call stack. This allows plugins to short-circuit operations like agent runs, tool calls, or model requests.


---

<!-- DOCUMENTO FUSIONADO: mcptoolsethtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/MCPToolset.html -->

# Class MCPToolset

Closes the toolset.

NOTE: This method is invoked, for example, at the end of an agent server's lifecycle or when the toolset is no longer needed. Implementations should ensure that any open connections, files, or other managed resources are properly released to prevent leaks.

A Promise that resolves when the toolset is closed.

Returns the tools that should be exposed to LLM.

`Optional`

context: ReadonlyContextContext used to filter tools available to the agent. If not defined, all tools in the toolset are returned.

A Promise that resolves to the list of tools.

`Protected`

isReturns whether the tool should be exposed to LLM.

The tool to check.

Context used to filter tools available to the agent.

Whether the tool should be exposed to LLM.

Processes the outgoing LLM request for this toolset. This method will be called before each tool processes the llm request.

Use cases:

The context of the tool.

The outgoing LLM request, mutable this method.

A toolset that dynamically discovers and provides tools from a Model Context Protocol (MCP) server.

This class connects to an MCP server, retrieves the list of available tools, and wraps each of them in an MCPTool instance. This allows the agent to seamlessly use tools from an external MCP-compliant service.

The toolset can be configured with a filter to selectively expose a subset of the tools provided by the MCP server.

Usage: import { MCPToolset } from '@google/adk'; import { StreamableHTTPConnectionParamsSchema } from '@google/adk';

const connectionParams = StreamableHTTPConnectionParamsSchema.parse({ type: "StreamableHTTPConnectionParams", url: "http://localhost:8788/mcp" });

const mcpToolset = new MCPToolset(connectionParams); const tools = await mcpToolset.getTools();


---

<!-- DOCUMENTO FUSIONADO: invocationcontexthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/InvocationContext.html -->

# Class InvocationContext

The parameters for creating an invocation context.

`Optional`

activeThe running streaming tools of this invocation.

The current agent of this invocation context.

`Optional`

`Readonly`

artifact`Optional`

branchThe branch of the invocation context.

The format is like agent_1.agent_2.agent_3, where agent_1 is the parent of agent_2, and agent_2 is the parent of agent_3.

Branch is used when multiple sub-agents shouldn't see their peer agents' conversation history.

`Optional`

`Readonly`

credentialWhether to end this invocation. Set to True in callbacks or tools to terminate this invocation.

`Readonly`

invocationThe id of this invocation context.

`Optional`

liveThe queue to receive live requests.

`Optional`

`Readonly`

memoryThe manager for keeping track of plugins in this invocation.

`Optional`

runConfigurations for live agents under this invocation.

`Readonly`

sessionThe current session of this invocation context.

`Optional`

`Readonly`

session`Optional`

transcriptionCaches necessary, data audio or contents, that are needed by transcription.

`Optional`

`Readonly`

userThe user content that started this invocation.

An invocation context represents the data of a single invocation of an agent.

An invocation: 1. Starts with a user message and ends with a final response. 2. Can contain one or multiple agent calls. 3. Is handled by runner.runAsync().

An invocation runs an agent until it does not request to transfer to another agent.

An agent call: 1. Is handled by agent.runAsync(). 2. Ends when agent.runAsync() ends.

An LLM agent call is an agent with a BaseLLMFlow. An LLM agent call can contain one or multiple steps.

An LLM agent runs steps in a loop until:

A step:

The summarization of the function response is considered another step, since it is another llm call. A step ends when it's done calling llm and tools, or if the end_invocation is set to true at any time.


---

<!-- DOCUMENTO FUSIONADO: baseagenthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/BaseAgent.html -->

# Class BaseAgentAbstract

`Abstract`

`Readonly`

afterCallback or list of callbacks to be invoked after the agent run.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return undefined.

`Readonly`

beforeCallback or list of callbacks to be invoked before the agent run.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return undefined.

`Optional`

`Readonly`

descriptionDescription about the agent's capability.

The model uses this to determine whether to delegate control to the agent. One-line description is enough and preferred.

`Readonly`

nameThe agent's name. Agent name must be a JS identifier and unique within the agent tree. Agent name cannot be "user", since it's reserved for end-user's input.

`Optional`

parentThe parent agent of this agent.

Note that an agent can ONLY be added as sub-agent once.

If you want to add one agent twice as sub-agent, consider to create two agent instances with identical config, but with different name and add them to the agent tree.

The parent agent is the agent that created this agent.

`Readonly`

rootRoot agent of this agent.

`Readonly`

subThe sub-agents of this agent.

`Protected`

createCreates an invocation context for this agent.

The invocation context of the parent agent.

The invocation context for this agent.

Finds the agent with the given name in this agent and its descendants.

The name of the agent to find.

The agent with the given name, or undefined if not found.

Finds the agent with the given name in this agent's descendants.

The name of the agent to find.

The agent with the given name, or undefined if not found.

`Protected`

handleRuns the after agent callback if it exists.

The invocation context of the agent.

The event to return to the user, or undefined if no event is generated.

`Protected`

handleRuns the before agent callback if it exists.

The invocation context of the agent.

The event to return to the user, or undefined if no event is generated.

Entry method to run an agent via text-based conversation.

The invocation context of the parent agent.

An AsyncGenerator that yields the events generated by the agent.

`Protected`

`Abstract`

runCore logic to run this agent via text-based conversation.

The invocation context of the agent.

An AsyncGenerator that yields the events generated by the agent.

Entry method to run an agent via video/audio-based conversation.

The invocation context of the parent agent.

An AsyncGenerator that yields the events generated by the agent.

`Protected`

`Abstract`

runCore logic to run this agent via video/audio-based conversation.

The invocation context of the agent.

An AsyncGenerator that yields the events generated by the agent.

Base class for all agents in Agent Development Kit.


---

<!-- DOCUMENTO FUSIONADO: loopagenthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/LoopAgent.html -->

# Class LoopAgent

`Readonly`

afterCallback or list of callbacks to be invoked after the agent run.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return undefined.

`Readonly`

beforeCallback or list of callbacks to be invoked before the agent run.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return undefined.

`Optional`

`Readonly`

descriptionDescription about the agent's capability.

The model uses this to determine whether to delegate control to the agent. One-line description is enough and preferred.

`Readonly`

nameThe agent's name. Agent name must be a JS identifier and unique within the agent tree. Agent name cannot be "user", since it's reserved for end-user's input.

`Optional`

parentThe parent agent of this agent.

Note that an agent can ONLY be added as sub-agent once.

If you want to add one agent twice as sub-agent, consider to create two agent instances with identical config, but with different name and add them to the agent tree.

The parent agent is the agent that created this agent.

`Readonly`

rootRoot agent of this agent.

`Readonly`

subThe sub-agents of this agent.

`Protected`

createCreates an invocation context for this agent.

The invocation context of the parent agent.

The invocation context for this agent.

Finds the agent with the given name in this agent and its descendants.

The name of the agent to find.

The agent with the given name, or undefined if not found.

Finds the agent with the given name in this agent's descendants.

The name of the agent to find.

The agent with the given name, or undefined if not found.

`Protected`

handleRuns the after agent callback if it exists.

The invocation context of the agent.

The event to return to the user, or undefined if no event is generated.

`Protected`

handleRuns the before agent callback if it exists.

The invocation context of the agent.

The event to return to the user, or undefined if no event is generated.

Entry method to run an agent via text-based conversation.

The invocation context of the parent agent.

An AsyncGenerator that yields the events generated by the agent.

`Protected`

runCore logic to run this agent via text-based conversation.

The invocation context of the agent.

An AsyncGenerator that yields the events generated by the agent.

Entry method to run an agent via video/audio-based conversation.

The invocation context of the parent agent.

An AsyncGenerator that yields the events generated by the agent.

`Protected`

runCore logic to run this agent via video/audio-based conversation.

The invocation context of the agent.

An AsyncGenerator that yields the events generated by the agent.

A shell agent that run its sub-agents in a loop.

When sub-agent generates an event with escalate or max_iterations are reached, the loop agent will stop.


---

<!-- DOCUMENTO FUSIONADO: parallelagenthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/ParallelAgent.html -->

# Class ParallelAgent

`Readonly`

afterCallback or list of callbacks to be invoked after the agent run.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return undefined.

`Readonly`

beforeCallback or list of callbacks to be invoked before the agent run.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return undefined.

`Optional`

`Readonly`

descriptionDescription about the agent's capability.

The model uses this to determine whether to delegate control to the agent. One-line description is enough and preferred.

`Readonly`

nameThe agent's name. Agent name must be a JS identifier and unique within the agent tree. Agent name cannot be "user", since it's reserved for end-user's input.

`Optional`

parentThe parent agent of this agent.

Note that an agent can ONLY be added as sub-agent once.

If you want to add one agent twice as sub-agent, consider to create two agent instances with identical config, but with different name and add them to the agent tree.

The parent agent is the agent that created this agent.

`Readonly`

rootRoot agent of this agent.

`Readonly`

subThe sub-agents of this agent.

`Protected`

createCreates an invocation context for this agent.

The invocation context of the parent agent.

The invocation context for this agent.

Finds the agent with the given name in this agent and its descendants.

The name of the agent to find.

The agent with the given name, or undefined if not found.

Finds the agent with the given name in this agent's descendants.

The name of the agent to find.

The agent with the given name, or undefined if not found.

`Protected`

handleRuns the after agent callback if it exists.

The invocation context of the agent.

The event to return to the user, or undefined if no event is generated.

`Protected`

handleRuns the before agent callback if it exists.

The invocation context of the agent.

The event to return to the user, or undefined if no event is generated.

Entry method to run an agent via text-based conversation.

The invocation context of the parent agent.

An AsyncGenerator that yields the events generated by the agent.

`Protected`

runCore logic to run this agent via text-based conversation.

The invocation context of the agent.

An AsyncGenerator that yields the events generated by the agent.

Entry method to run an agent via video/audio-based conversation.

The invocation context of the parent agent.

An AsyncGenerator that yields the events generated by the agent.

`Protected`

runCore logic to run this agent via video/audio-based conversation.

The invocation context of the agent.

An AsyncGenerator that yields the events generated by the agent.

A shell agent that run its sub-agents in parallel in isolated manner.

This approach is beneficial for scenarios requiring multiple perspectives or attempts on a single task, such as:


---

<!-- DOCUMENTO FUSIONADO: llmagenthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/LlmAgent.html -->

# Class LlmAgent

`Readonly`

afterCallback or list of callbacks to be invoked after the agent run.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return undefined.

`Optional`

after`Optional`

after`Readonly`

beforeCallback or list of callbacks to be invoked before the agent run.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return undefined.

`Optional`

before`Optional`

before`Optional`

`Readonly`

descriptionDescription about the agent's capability.

The model uses this to determine whether to delegate control to the agent. One-line description is enough and preferred.

`Optional`

generate`Optional`

input`Optional`

model`Readonly`

nameThe agent's name. Agent name must be a JS identifier and unique within the agent tree. Agent name cannot be "user", since it's reserved for end-user's input.

`Optional`

output`Optional`

output`Optional`

parentThe parent agent of this agent.

Note that an agent can ONLY be added as sub-agent once.

If you want to add one agent twice as sub-agent, consider to create two agent instances with identical config, but with different name and add them to the agent tree.

The parent agent is the agent that created this agent.

`Readonly`

rootRoot agent of this agent.

`Readonly`

subThe sub-agents of this agent.

The resolved self.after_model_callback field as a list of SingleAfterModelCallback.

This method is only for use by Agent Development Kit.

The resolved self.after_tool_callback field as a list of AfterToolCallback.

This method is only for use by Agent Development Kit.

The resolved self.before_model_callback field as a list of SingleBeforeModelCallback.

This method is only for use by Agent Development Kit.

The resolved self.before_tool_callback field as a list of BeforeToolCallback.

This method is only for use by Agent Development Kit.

The resolved BaseLlm instance.

When not set, the agent will inherit the model from its ancestor.

The resolved self.instruction field to construct global instruction.

This method is only for use by Agent Development Kit.

The context to retrieve the session state.

The resolved self.global_instruction field.

The resolved self.instruction field to construct instruction for this agent.

This method is only for use by Agent Development Kit.

The context to retrieve the session state.

The resolved self.instruction field.

The resolved self.tools field as a list of BaseTool based on the context.

This method is only for use by Agent Development Kit.

`Optional`

context: ReadonlyContext`Protected`

createCreates an invocation context for this agent.

The invocation context of the parent agent.

The invocation context for this agent.

Finds the agent with the given name in this agent and its descendants.

The name of the agent to find.

The agent with the given name, or undefined if not found.

Finds the agent with the given name in this agent's descendants.

The name of the agent to find.

The agent with the given name, or undefined if not found.

`Protected`

handleRuns the after agent callback if it exists.

The invocation context of the agent.

The event to return to the user, or undefined if no event is generated.

`Protected`

handleRuns the before agent callback if it exists.

The invocation context of the agent.

The event to return to the user, or undefined if no event is generated.

Entry method to run an agent via text-based conversation.

The invocation context of the parent agent.

An AsyncGenerator that yields the events generated by the agent.

`Protected`

runCore logic to run this agent via text-based conversation.

The invocation context of the agent.

An AsyncGenerator that yields the events generated by the agent.

Entry method to run an agent via video/audio-based conversation.

The invocation context of the parent agent.

An AsyncGenerator that yields the events generated by the agent.

`Protected`

runCore logic to run this agent via video/audio-based conversation.

The invocation context of the agent.

An AsyncGenerator that yields the events generated by the agent.

An agent that uses a large language model to generate responses.


---

<!-- DOCUMENTO FUSIONADO: loggingpluginhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/LoggingPlugin.html -->

# Class LoggingPlugin

Initialize the logging plugin.

The name of the plugin instance.

Callback executed after an agent's primary logic has completed.

This callback can be used to inspect, log, or modify the agent's final result before it is returned.

The agent that has just run.

An optional `Content`

object. If a value is returned, it will
replace the agent's original result. Returning `undefined`

uses the
original, unmodified result.

Callback executed after a response is received from the model.

This is the ideal place to log model responses, collect metrics on token
usage, or perform post-processing on the raw `LlmResponse`

.

The context for the current agent call.

An optional value. A non-`undefined`

return may be used by the
framework to modify or replace the response. Returning `undefined`

allows the original response to be used.

Callback executed after an ADK runner run has completed.

This is the final callback in the ADK lifecycle, suitable for cleanup, final logging, or reporting tasks.

The context for the entire invocation.

undefined

Callback executed after a tool has been called.

This callback allows for inspecting, logging, or modifying the result returned by a tool.

The tool instance that has just been executed.

An optional dictionary. If a dictionary is returned, it will
**replace** the original result from the tool. This allows for
post-processing or altering tool outputs. Returning `undefined`

uses
the original, unmodified result.

Callback executed before an agent's primary logic is invoked.

This callback can be used for logging, setup, or to short-circuit the agent's execution by returning a value.

The agent that is about to run.

An optional `Content`

object. If a value is returned, it will
bypass the agent's callbacks and its execution, and return this value
directly. Returning `undefined`

allows the agent to proceed normally.

Callback executed before a request is sent to the model.

This provides an opportunity to inspect, log, or modify the `LlmRequest`

object. It can also be used to implement caching by returning a cached
`LlmResponse`

, which would skip the actual model call.

The context for the current agent call.

An optional value. The interpretation of a non-`undefined`

trigger an early exit and returns the response immediately. Returning
`undefined`

allows the LLM request to proceed normally.

Callback executed before the ADK runner runs.

This is the first callback to be called in the lifecycle, ideal for global setup or initialization tasks.

The context for the entire invocation, containing session information, the root agent, etc.

An optional `Event`

to be returned to the ADK. Returning a value
to halt execution of the runner and ends the runner with that event.
Return `undefined`

to proceed normally.

Callback executed before a tool is called.

This callback is useful for logging tool usage, input validation, or modifying the arguments before they are passed to the tool.

The tool instance that is about to be executed.

An optional dictionary. If a dictionary is returned, it will stop
the tool execution and return this response immediately. Returning
`undefined`

uses the original, unmodified arguments.

Callback executed after an event is yielded from runner.

This is the ideal place to make modification to the event before the event is handled by the underlying agent app.

The context for the entire invocation.

An optional value. A non-`undefined`

return may be used by the
framework to modify or replace the response. Returning `undefined`

allows the original response to be used.

Callback executed when a model call encounters an error.

This callback provides an opportunity to handle model errors gracefully, potentially providing alternative responses or recovery mechanisms.

The context for the current agent call.

An optional LlmResponse. If an LlmResponse is returned, it will be
used instead of propagating the error. Returning `undefined`

allows
the original error to be raised.

Callback executed when a tool call encounters an error.

This callback provides an opportunity to handle tool errors gracefully, potentially providing alternative responses or recovery mechanisms.

The tool instance that encountered an error.

An optional dictionary. If a dictionary is returned, it will be
used as the tool response instead of propagating the error. Returning
`undefined`

allows the original error to be raised.

Callback executed when a user message is received before an invocation starts.

This callback helps logging and modifying the user message before the runner starts the invocation.

The context for the entire invocation.

An optional `Content`

to be returned to the ADK. Returning a
value to replace the user message. Returning `undefined`

to proceed
normally.

A plugin that logs important information at each callback point.

This plugin helps printing all critical events in the console. It is not a replacement of existing logging in ADK. It rather helps terminal based debugging by showing all logs in the console, and serves as a simple demo for everyone to leverage when developing new plugins.

This plugin helps users track the invocation status by logging:

Example:


---

<!-- DOCUMENTO FUSIONADO: basepluginhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/classes/BasePlugin.html -->

# Class BasePluginAbstract

`Abstract`

Initializes the plugin.

A unique identifier for this plugin instance.

Callback executed after an agent's primary logic has completed.

This callback can be used to inspect, log, or modify the agent's final result before it is returned.

The agent that has just run.

An optional `Content`

object. If a value is returned, it will
replace the agent's original result. Returning `undefined`

uses the
original, unmodified result.

Callback executed after a response is received from the model.

This is the ideal place to log model responses, collect metrics on token
usage, or perform post-processing on the raw `LlmResponse`

.

The context for the current agent call.

An optional value. A non-`undefined`

return may be used by the
framework to modify or replace the response. Returning `undefined`

allows the original response to be used.

Callback executed after an ADK runner run has completed.

This is the final callback in the ADK lifecycle, suitable for cleanup, final logging, or reporting tasks.

The context for the entire invocation.

undefined

Callback executed after a tool has been called.

This callback allows for inspecting, logging, or modifying the result returned by a tool.

The tool instance that has just been executed.

An optional dictionary. If a dictionary is returned, it will
**replace** the original result from the tool. This allows for
post-processing or altering tool outputs. Returning `undefined`

uses
the original, unmodified result.

Callback executed before an agent's primary logic is invoked.

This callback can be used for logging, setup, or to short-circuit the agent's execution by returning a value.

The agent that is about to run.

An optional `Content`

object. If a value is returned, it will
bypass the agent's callbacks and its execution, and return this value
directly. Returning `undefined`

allows the agent to proceed normally.

Callback executed before a request is sent to the model.

This provides an opportunity to inspect, log, or modify the `LlmRequest`

object. It can also be used to implement caching by returning a cached
`LlmResponse`

, which would skip the actual model call.

The context for the current agent call.

An optional value. The interpretation of a non-`undefined`

trigger an early exit and returns the response immediately. Returning
`undefined`

allows the LLM request to proceed normally.

Callback executed before the ADK runner runs.

This is the first callback to be called in the lifecycle, ideal for global setup or initialization tasks.

The context for the entire invocation, containing session information, the root agent, etc.

An optional `Event`

to be returned to the ADK. Returning a value
to halt execution of the runner and ends the runner with that event.
Return `undefined`

to proceed normally.

Callback executed before a tool is called.

This callback is useful for logging tool usage, input validation, or modifying the arguments before they are passed to the tool.

The tool instance that is about to be executed.

An optional dictionary. If a dictionary is returned, it will stop
the tool execution and return this response immediately. Returning
`undefined`

uses the original, unmodified arguments.

Callback executed after an event is yielded from runner.

This is the ideal place to make modification to the event before the event is handled by the underlying agent app.

The context for the entire invocation.

An optional value. A non-`undefined`

return may be used by the
framework to modify or replace the response. Returning `undefined`

allows the original response to be used.

Callback executed when a model call encounters an error.

This callback provides an opportunity to handle model errors gracefully, potentially providing alternative responses or recovery mechanisms.

The context for the current agent call.

An optional LlmResponse. If an LlmResponse is returned, it will be
used instead of propagating the error. Returning `undefined`

allows
the original error to be raised.

Callback executed when a tool call encounters an error.

This callback provides an opportunity to handle tool errors gracefully, potentially providing alternative responses or recovery mechanisms.

The tool instance that encountered an error.

An optional dictionary. If a dictionary is returned, it will be
used as the tool response instead of propagating the error. Returning
`undefined`

allows the original error to be raised.

Callback executed when a user message is received before an invocation starts.

This callback helps logging and modifying the user message before the runner starts the invocation.

The context for the entire invocation.

An optional `Content`

to be returned to the ADK. Returning a
value to replace the user message. Returning `undefined`

to proceed
normally.

Base class for creating plugins.

Plugins provide a structured way to intercept and modify agent, tool, and LLM behaviors at critical execution points in a callback manner. While agent callbacks apply to a particular agent, plugins applies globally to all agents added in the runner. Plugins are best used for adding custom behaviors like logging, monitoring, caching, or modifying requests and responses at key stages.

A plugin can implement one or more methods of callbacks, but should not implement the same method of callback for multiple times.

Relation with Agent callbacks:

Execution OrderSimilar to Agent callbacks, Plugins are executed in the order they are registered. However, Plugin and Agent Callbacks are executed sequentially, with Plugins takes precedence over agent callbacks. When the callback in a plugin returns a value, it will short circuit all remaining plugins and agent callbacks, causing all remaining plugins and agent callbacks to be skipped.Change PropagationPlugins and agent callbacks can both modify the value of the input parameters, including agent input, tool input, and LLM request/response, etc. They work in the exactly same way. The modifications will be visible and passed to the next callback in the chain. For example, if a plugin modifies the tool input with before_tool_callback, the modified tool input will be passed to the before_tool_callback of the next plugin, and further passed to the agent callbacks if not short circuited.To use a plugin, implement the desired callback methods and pass an instance of your custom plugin class to the ADK Runner.

Example: A simple plugin that logs every tool call.


---

<!-- DOCUMENTO FUSIONADO: _python_merged.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/python/ -->

# google¶

# google[¶](#google)

[Submodules](google-adk.html)[google.adk.a2a module](google-adk.html#module-google.adk.a2a)[google.adk.agents module](google-adk.html#module-google.adk.agents)`Agent`

`BaseAgent`

`BaseAgent.after_agent_callback`

`BaseAgent.before_agent_callback`

`BaseAgent.description`

`BaseAgent.name`

`BaseAgent.parent_agent`

`BaseAgent.sub_agents`

`BaseAgent.config_type`

`BaseAgent.from_config()`

`BaseAgent.validate_name`

`BaseAgent.validate_sub_agents_unique_names`

`BaseAgent.clone()`

`BaseAgent.find_agent()`

`BaseAgent.find_sub_agent()`

`BaseAgent.model_post_init()`

`BaseAgent.run_async()`

`BaseAgent.run_live()`

`BaseAgent.canonical_after_agent_callbacks`

`BaseAgent.canonical_before_agent_callbacks`

`BaseAgent.root_agent`


`InvocationContext`

`InvocationContext.active_streaming_tools`

`InvocationContext.agent`

`InvocationContext.agent_states`

`InvocationContext.artifact_service`

`InvocationContext.branch`

`InvocationContext.canonical_tools_cache`

`InvocationContext.context_cache_config`

`InvocationContext.credential_service`

`InvocationContext.end_invocation`

`InvocationContext.end_of_agents`

`InvocationContext.input_realtime_cache`

`InvocationContext.invocation_id`

`InvocationContext.live_request_queue`

`InvocationContext.live_session_resumption_handle`

`InvocationContext.memory_service`

`InvocationContext.output_realtime_cache`

`InvocationContext.plugin_manager`

`InvocationContext.resumability_config`

`InvocationContext.run_config`

`InvocationContext.session`

`InvocationContext.session_service`

`InvocationContext.transcription_cache`

`InvocationContext.user_content`

`InvocationContext.increment_llm_call_count()`

`InvocationContext.model_post_init()`

`InvocationContext.populate_invocation_agent_states()`

`InvocationContext.reset_sub_agent_states()`

`InvocationContext.set_agent_state()`

`InvocationContext.should_pause_invocation()`

`InvocationContext.app_name`

`InvocationContext.is_resumable`

`InvocationContext.user_id`


`LiveRequest`

`LiveRequestQueue`

`LlmAgent`

`LlmAgent.after_model_callback`

`LlmAgent.after_tool_callback`

`LlmAgent.before_model_callback`

`LlmAgent.before_tool_callback`

`LlmAgent.code_executor`

`LlmAgent.disallow_transfer_to_parent`

`LlmAgent.disallow_transfer_to_peers`

`LlmAgent.generate_content_config`

`LlmAgent.global_instruction`

`LlmAgent.include_contents`

`LlmAgent.input_schema`

`LlmAgent.instruction`

`LlmAgent.model`

`LlmAgent.on_model_error_callback`

`LlmAgent.on_tool_error_callback`

`LlmAgent.output_key`

`LlmAgent.output_schema`

`LlmAgent.planner`

`LlmAgent.static_instruction`

`LlmAgent.tools`

`LlmAgent.config_type`

`LlmAgent.set_default_model()`

`LlmAgent.validate_generate_content_config`

`LlmAgent.canonical_global_instruction()`

`LlmAgent.canonical_instruction()`

`LlmAgent.canonical_tools()`

`LlmAgent.DEFAULT_MODEL`

`LlmAgent.canonical_after_model_callbacks`

`LlmAgent.canonical_after_tool_callbacks`

`LlmAgent.canonical_before_model_callbacks`

`LlmAgent.canonical_before_tool_callbacks`

`LlmAgent.canonical_model`

`LlmAgent.canonical_on_model_error_callbacks`

`LlmAgent.canonical_on_tool_error_callbacks`


`LoopAgent`

`McpInstructionProvider`

`ParallelAgent`

`RunConfig`

`RunConfig.context_window_compression`

`RunConfig.custom_metadata`

`RunConfig.enable_affective_dialog`

`RunConfig.input_audio_transcription`

`RunConfig.max_llm_calls`

`RunConfig.output_audio_transcription`

`RunConfig.proactivity`

`RunConfig.realtime_input_config`

`RunConfig.response_modalities`

`RunConfig.save_live_blob`

`RunConfig.session_resumption`

`RunConfig.speech_config`

`RunConfig.streaming_mode`

`RunConfig.support_cfc`

`RunConfig.check_for_deprecated_save_live_audio`

`RunConfig.validate_max_llm_calls`

`RunConfig.save_input_blobs_as_artifacts`

`RunConfig.save_live_audio`


`SequentialAgent`


[google.adk.artifacts module](google-adk.html#module-google.adk.artifacts)`BaseArtifactService`

`FileArtifactService`

`GcsArtifactService`

`InMemoryArtifactService`

`InMemoryArtifactService.artifacts`

`InMemoryArtifactService.delete_artifact()`

`InMemoryArtifactService.get_artifact_version()`

`InMemoryArtifactService.list_artifact_keys()`

`InMemoryArtifactService.list_artifact_versions()`

`InMemoryArtifactService.list_versions()`

`InMemoryArtifactService.load_artifact()`

`InMemoryArtifactService.save_artifact()`


[google.adk.apps package](google-adk.html#module-google.adk.apps)[google.adk.auth module](google-adk.html#module-google.adk.auth)[google.adk.cli module](google-adk.html#module-google.adk.cli)[google.adk.code_executors module](google-adk.html#module-google.adk.code_executors)`BaseCodeExecutor`

`BaseCodeExecutor.optimize_data_file`

`BaseCodeExecutor.stateful`

`BaseCodeExecutor.error_retry_attempts`

`BaseCodeExecutor.code_block_delimiters`

`BaseCodeExecutor.execution_result_delimiters`

`BaseCodeExecutor.code_block_delimiters`

`BaseCodeExecutor.error_retry_attempts`

`BaseCodeExecutor.execution_result_delimiters`

`BaseCodeExecutor.optimize_data_file`

`BaseCodeExecutor.stateful`

`BaseCodeExecutor.execute_code()`


`BuiltInCodeExecutor`

`CodeExecutorContext`

`CodeExecutorContext.add_input_files()`

`CodeExecutorContext.add_processed_file_names()`

`CodeExecutorContext.clear_input_files()`

`CodeExecutorContext.get_error_count()`

`CodeExecutorContext.get_execution_id()`

`CodeExecutorContext.get_input_files()`

`CodeExecutorContext.get_processed_file_names()`

`CodeExecutorContext.get_state_delta()`

`CodeExecutorContext.increment_error_count()`

`CodeExecutorContext.reset_error_count()`

`CodeExecutorContext.set_execution_id()`

`CodeExecutorContext.update_code_execution_result()`


`UnsafeLocalCodeExecutor`


[google.adk.errors module](google-adk.html#module-google.adk.errors)[google.adk.evaluation module](google-adk.html#module-google.adk.evaluation)[google.adk.events module](google-adk.html#module-google.adk.events)`Event`

`EventActions`

`EventActions.agent_state`

`EventActions.artifact_delta`

`EventActions.compaction`

`EventActions.end_of_agent`

`EventActions.escalate`

`EventActions.requested_auth_configs`

`EventActions.requested_tool_confirmations`

`EventActions.rewind_before_invocation_id`

`EventActions.skip_summarization`

`EventActions.state_delta`

`EventActions.transfer_to_agent`


[google.adk.examples module](google-adk.html#module-google.adk.examples)[google.adk.flows module](google-adk.html#module-google.adk.flows)[google.adk.memory module](google-adk.html#module-google.adk.memory)[google.adk.models module](google-adk.html#module-google.adk.models)[google.adk.planners module](google-adk.html#module-google.adk.planners)[google.adk.platform module](google-adk.html#module-google.adk.platform)[google.adk.plugins module](google-adk.html#module-google.adk.plugins)`BasePlugin`

`BasePlugin.after_agent_callback()`

`BasePlugin.after_model_callback()`

`BasePlugin.after_run_callback()`

`BasePlugin.after_tool_callback()`

`BasePlugin.before_agent_callback()`

`BasePlugin.before_model_callback()`

`BasePlugin.before_run_callback()`

`BasePlugin.before_tool_callback()`

`BasePlugin.close()`

`BasePlugin.on_event_callback()`

`BasePlugin.on_model_error_callback()`

`BasePlugin.on_tool_error_callback()`

`BasePlugin.on_user_message_callback()`


`LoggingPlugin`

`LoggingPlugin.after_agent_callback()`

`LoggingPlugin.after_model_callback()`

`LoggingPlugin.after_run_callback()`

`LoggingPlugin.after_tool_callback()`

`LoggingPlugin.before_agent_callback()`

`LoggingPlugin.before_model_callback()`

`LoggingPlugin.before_run_callback()`

`LoggingPlugin.before_tool_callback()`

`LoggingPlugin.on_event_callback()`

`LoggingPlugin.on_model_error_callback()`

`LoggingPlugin.on_tool_error_callback()`

`LoggingPlugin.on_user_message_callback()`


`PluginManager`

`PluginManager.close()`

`PluginManager.get_plugin()`

`PluginManager.register_plugin()`

`PluginManager.run_after_agent_callback()`

`PluginManager.run_after_model_callback()`

`PluginManager.run_after_run_callback()`

`PluginManager.run_after_tool_callback()`

`PluginManager.run_before_agent_callback()`

`PluginManager.run_before_model_callback()`

`PluginManager.run_before_run_callback()`

`PluginManager.run_before_tool_callback()`

`PluginManager.run_on_event_callback()`

`PluginManager.run_on_model_error_callback()`

`PluginManager.run_on_tool_error_callback()`

`PluginManager.run_on_user_message_callback()`


`ReflectAndRetryToolPlugin`


[google.adk.runners module](google-adk.html#module-google.adk.runners)`InMemoryRunner`

`Runner`

`Runner.app_name`

`Runner.agent`

`Runner.artifact_service`

`Runner.plugin_manager`

`Runner.session_service`

`Runner.memory_service`

`Runner.credential_service`

`Runner.context_cache_config`

`Runner.resumability_config`

`Runner.Self`

`Runner.agent`

`Runner.app_name`

`Runner.artifact_service`

`Runner.close()`

`Runner.context_cache_config`

`Runner.credential_service`

`Runner.memory_service`

`Runner.plugin_manager`

`Runner.resumability_config`

`Runner.rewind_async()`

`Runner.run()`

`Runner.run_async()`

`Runner.run_debug()`

`Runner.run_live()`

`Runner.session_service`


[google.adk.sessions module](google-adk.html#module-google.adk.sessions)`BaseSessionService`

`InMemorySessionService`

`InMemorySessionService.append_event()`

`InMemorySessionService.create_session()`

`InMemorySessionService.create_session_sync()`

`InMemorySessionService.delete_session()`

`InMemorySessionService.delete_session_sync()`

`InMemorySessionService.get_session()`

`InMemorySessionService.get_session_sync()`

`InMemorySessionService.list_sessions()`

`InMemorySessionService.list_sessions_sync()`


`Session`

`State`

`VertexAiSessionService`


[google.adk.telemetry module](google-adk.html#module-google.adk.telemetry)[google.adk.tools package](google-adk.html#module-google.adk.tools)[google.adk.tools.agent_tool module](google-adk.html#module-google.adk.tools.agent_tool)[google.adk.tools.apihub_tool module](google-adk.html#module-google.adk.tools.apihub_tool)[google.adk.tools.application_integration_tool module](google-adk.html#module-google.adk.tools.application_integration_tool)[google.adk.tools.authenticated_function_tool module](google-adk.html#module-google.adk.tools.authenticated_function_tool)[google.adk.tools.base_authenticated_tool module](google-adk.html#module-google.adk.tools.base_authenticated_tool)[google.adk.tools.base_tool module](google-adk.html#module-google.adk.tools.base_tool)[google.adk.tools.base_toolset module](google-adk.html#module-google.adk.tools.base_toolset)[google.adk.tools.bigquery module](google-adk.html#module-google.adk.tools.bigquery)[google.adk.tools.crewai_tool module](google-adk.html#google-adk-tools-crewai-tool-module)[google.adk.tools.enterprise_search_tool module](google-adk.html#module-google.adk.tools.enterprise_search_tool)[google.adk.tools.example_tool module](google-adk.html#module-google.adk.tools.example_tool)[google.adk.tools.exit_loop_tool module](google-adk.html#module-google.adk.tools.exit_loop_tool)[google.adk.tools.function_tool module](google-adk.html#module-google.adk.tools.function_tool)[google.adk.tools.get_user_choice_tool module](google-adk.html#module-google.adk.tools.get_user_choice_tool)[google.adk.tools.google_api_tool module](google-adk.html#module-google.adk.tools.google_api_tool)[google.adk.tools.google_maps_grounding_tool module](google-adk.html#google-adk-tools-google-maps-grounding-tool-module)[google.adk.tools.google_search_tool module](google-adk.html#module-google.adk.tools.google_search_tool)[google.adk.tools.langchain_tool module](google-adk.html#google-adk-tools-langchain-tool-module)[google.adk.tools.load_artifacts_tool module](google-adk.html#module-google.adk.tools.load_artifacts_tool)[google.adk.tools.load_memory_tool module](google-adk.html#module-google.adk.tools.load_memory_tool)[google.adk.tools.load_web_page module](google-adk.html#module-google.adk.tools.load_web_page)[google.adk.tools.long_running_tool module](google-adk.html#module-google.adk.tools.long_running_tool)[google.adk.tools.mcp_tool module](google-adk.html#module-google.adk.tools.mcp_tool)`MCPTool`

`MCPToolset`

`McpTool`

`McpToolset`

`SseConnectionParams`

`StdioConnectionParams`

`StreamableHTTPConnectionParams`

`StreamableHTTPConnectionParams.url`

`StreamableHTTPConnectionParams.headers`

`StreamableHTTPConnectionParams.timeout`

`StreamableHTTPConnectionParams.sse_read_timeout`

`StreamableHTTPConnectionParams.terminate_on_close`

`StreamableHTTPConnectionParams.httpx_client_factory`

`StreamableHTTPConnectionParams.headers`

`StreamableHTTPConnectionParams.httpx_client_factory`

`StreamableHTTPConnectionParams.sse_read_timeout`

`StreamableHTTPConnectionParams.terminate_on_close`

`StreamableHTTPConnectionParams.timeout`

`StreamableHTTPConnectionParams.url`


`adk_to_mcp_tool_type()`

`gemini_to_json_schema()`


[google.adk.tools.openapi_tool module](google-adk.html#module-google.adk.tools.openapi_tool)[google.adk.tools.preload_memory_tool module](google-adk.html#module-google.adk.tools.preload_memory_tool)[google.adk.tools.retrieval module](google-adk.html#module-google.adk.tools.retrieval)[google.adk.tools.tool_context module](google-adk.html#module-google.adk.tools.tool_context)[google.adk.tools.toolbox_toolset module](google-adk.html#google-adk-tools-toolbox-toolset-module)[google.adk.tools.transfer_to_agent_tool module](google-adk.html#module-google.adk.tools.transfer_to_agent_tool)[google.adk.tools.url_context_tool module](google-adk.html#module-google.adk.tools.url_context_tool)[google.adk.tools.vertex_ai_search_tool module](google-adk.html#module-google.adk.tools.vertex_ai_search_tool)[google.adk.utils module](google-adk.html#module-google.adk.utils)[google.adk.version module](google-adk.html#module-google.adk.version)


---

<!-- DOCUMENTO FUSIONADO: google-adkhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/python/google-adk.html -->

# Submodules¶

# Submodules[¶](#submodules)

# google.adk.a2a module[¶](#module-google.adk.a2a)

# google.adk.agents module[¶](#module-google.adk.agents)

-
*pydantic model*google.adk.agents.BaseAgent[¶](#google.adk.agents.BaseAgent) Bases:

`BaseModel`

Base class for all agents in Agent Development Kit.

## Show JSON schema

{ "$defs": { "BaseAgent": { "additionalProperties": false, "description": "Base class for all agents in Agent Development Kit.", "properties": { "name": { "title": "Name", "type": "string" }, "description": { "default": "", "title": "Description", "type": "string" }, "parent_agent": { "anyOf": [ { "$ref": "#/$defs/BaseAgent" }, { "type": "null" } ], "default": null }, "sub_agents": { "items": { "$ref": "#/$defs/BaseAgent" }, "title": "Sub Agents", "type": "array" }, "before_agent_callback": { "default": null, "title": "Before Agent Callback", "type": "null" }, "after_agent_callback": { "default": null, "title": "After Agent Callback", "type": "null" } }, "required": [ "name" ], "title": "BaseAgent", "type": "object" } }, "$ref": "#/$defs/BaseAgent" }

- Fields:
`after_agent_callback (Callable[[google.adk.agents.callback_context.CallbackContext], Awaitable[google.genai.types.Content | None] | google.genai.types.Content | None] | list[Callable[[google.adk.agents.callback_context.CallbackContext], Awaitable[google.genai.types.Content | None] | google.genai.types.Content | None]] | None)`

`before_agent_callback (Callable[[google.adk.agents.callback_context.CallbackContext], Awaitable[google.genai.types.Content | None] | google.genai.types.Content | None] | list[Callable[[google.adk.agents.callback_context.CallbackContext], Awaitable[google.genai.types.Content | None] | google.genai.types.Content | None]] | None)`

`description (str)`

`name (str)`

`parent_agent (google.adk.agents.base_agent.BaseAgent | None)`

`sub_agents (list[google.adk.agents.base_agent.BaseAgent])`


- Validators:
`validate_name`

»`name`

`validate_sub_agents_unique_names`

»`sub_agents`


-
*field*after_agent_callback*: AfterAgentCallback | None**= None*[¶](#google.adk.agents.BaseAgent.after_agent_callback) Callback or list of callbacks to be invoked after the agent run.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return None.

- Parameters:
**callback_context**– MUST be named ‘callback_context’ (enforced).- Returns:
- The content to return to the user.
When the content is present, an additional event with the provided content will be appended to event history as an additional agent response.


- Return type:
Optional[types.Content]


-
*field*before_agent_callback*: BeforeAgentCallback | None**= None*[¶](#google.adk.agents.BaseAgent.before_agent_callback) Callback or list of callbacks to be invoked before the agent run.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return None.

- Parameters:
**callback_context**– MUST be named ‘callback_context’ (enforced).- Returns:
- The content to return to the user.
When the content is present, the agent run will be skipped and the provided content will be returned to user.


- Return type:
Optional[types.Content]


-
*field*description*: str**= ''*[¶](#google.adk.agents.BaseAgent.description) Description about the agent’s capability.

The model uses this to determine whether to delegate control to the agent. One-line description is enough and preferred.


-
*field*name*: str**[Required]*[¶](#google.adk.agents.BaseAgent.name) The agent’s name.

Agent name must be a Python identifier and unique within the agent tree. Agent name cannot be “user”, since it’s reserved for end-user’s input.

- Validated by:
`validate_name`


-
*field*parent_agent*:*[BaseAgent](#google.adk.agents.BaseAgent)| None*= None*[¶](#google.adk.agents.BaseAgent.parent_agent) The parent agent of this agent.

Note that an agent can ONLY be added as sub-agent once.

If you want to add one agent twice as sub-agent, consider to create two agent instances with identical config, but with different name and add them to the agent tree.


-
*field*sub_agents*: list[*[BaseAgent](#google.adk.agents.BaseAgent)]*[Optional]*[¶](#google.adk.agents.BaseAgent.sub_agents) The sub-agents of this agent.

- Validated by:
`validate_sub_agents_unique_names`


-
config_type
[¶](#google.adk.agents.BaseAgent.config_type) alias of

`BaseAgentConfig`


-
*classmethod*from_config(*cls*,*config*,*config_abs_path*)[¶](#google.adk.agents.BaseAgent.from_config) Creates an agent from a config.

If sub-classes uses a custom agent config, override _from_config_kwargs method to return an updated kwargs for agent constructor.

- Return type:
`TypeVar`

(`SelfAgent`

, bound= BaseAgent)- Parameters:
**config**– The config to create the agent from.**config_abs_path**– The absolute path to the config file that contains the agent config.

- Returns:
The created agent.


-
*validator*validate_name*»**name*[¶](#google.adk.agents.BaseAgent.validate_name)

-
*validator*validate_sub_agents_unique_names*»**sub_agents*[¶](#google.adk.agents.BaseAgent.validate_sub_agents_unique_names) Validates that all sub-agents have unique names.

- Return type:
`list`

[]`BaseAgent`

- Parameters:
**value**– The list of sub-agents to validate.- Returns:
The validated list of sub-agents.


-
clone(
*update=None*)[¶](#google.adk.agents.BaseAgent.clone) Creates a copy of this agent instance.

- Return type:
`TypeVar`

(`SelfAgent`

, bound= BaseAgent)- Parameters:
**update**– Optional mapping of new values for the fields of the cloned agent. The keys of the mapping are the names of the fields to be updated, and the values are the new values for those fields. For example: {“name”: “cloned_agent”}- Returns:
A new agent instance with identical configuration as the original agent except for the fields specified in the update.


-
find_agent(
*name*)[¶](#google.adk.agents.BaseAgent.find_agent) Finds the agent with the given name in this agent and its descendants.

- Return type:
`Optional`

[]`BaseAgent`

- Parameters:
**name**– The name of the agent to find.- Returns:
The agent with the matching name, or None if no such agent is found.


-
find_sub_agent(
*name*)[¶](#google.adk.agents.BaseAgent.find_sub_agent) Finds the agent with the given name in this agent’s descendants.

- Return type:
`Optional`

[]`BaseAgent`

- Parameters:
**name**– The name of the agent to find.- Returns:
The agent with the matching name, or None if no such agent is found.


-
model_post_init(
*_BaseAgent__context*)[¶](#google.adk.agents.BaseAgent.model_post_init) Override this method to perform additional initialization after __init__ and model_construct. This is useful if you want to do some validation that requires the entire model to be initialized.

- Return type:
`None`


-
*async*run_async(*parent_context*)[¶](#google.adk.agents.BaseAgent.run_async) Entry method to run an agent via text-based conversation.

- Return type:
`AsyncGenerator`

[,`Event`

`None`

]- Parameters:
**parent_context**– InvocationContext, the invocation context of the parent agent.- Yields:
*Event*– the events generated by the agent.


-
*async*run_live(*parent_context*)[¶](#google.adk.agents.BaseAgent.run_live) Entry method to run an agent via video/audio-based conversation.

- Return type:
`AsyncGenerator`

[,`Event`

`None`

]- Parameters:
**parent_context**– InvocationContext, the invocation context of the parent agent.- Yields:
*Event*– the events generated by the agent.


-
*property*canonical_after_agent_callbacks*: list[Callable[[CallbackContext], Awaitable[Content | None] | Content | None]]*[¶](#google.adk.agents.BaseAgent.canonical_after_agent_callbacks) The resolved self.after_agent_callback field as a list of _SingleAgentCallback.

This method is only for use by Agent Development Kit.


-
*property*canonical_before_agent_callbacks*: list[Callable[[CallbackContext], Awaitable[Content | None] | Content | None]]*[¶](#google.adk.agents.BaseAgent.canonical_before_agent_callbacks) The resolved self.before_agent_callback field as a list of _SingleAgentCallback.

This method is only for use by Agent Development Kit.


-
*pydantic model*google.adk.agents.InvocationContext[¶](#google.adk.agents.InvocationContext) Bases:

`BaseModel`

An invocation context represents the data of a single invocation of an agent.

- An invocation:
Starts with a user message and ends with a final response.

Can contain one or multiple agent calls.

Is handled by runner.run_async().


An invocation runs an agent until it does not request to transfer to another agent.

- An agent call:
Is handled by agent.run().

Ends when agent.run() ends.


An LLM agent call is an agent with a BaseLLMFlow. An LLM agent call can contain one or multiple steps.

- An LLM agent runs steps in a loop until:
A final response is generated.

The agent transfers to another agent.

The end_invocation is set to true by any callbacks or tools.


- A step:
Calls the LLM only once and yields its response.

Calls the tools and yields their responses if requested.


The summarization of the function response is considered another step, since it is another llm call. A step ends when it’s done calling llm and tools, or if the end_invocation is set to true at any time.

[``](#id1)[`](#id3)┌─────────────────────── invocation ──────────────────────────┐ ┌──────────── llm_agent_call_1 ────────────┐ ┌─ agent_call_2 ─┐ ┌──── step_1 ────────┐ ┌───── step_2 ──────┐ [call_llm] [call_tool] [call_llm] [transfer]


## Show JSON schema

{ "title": "InvocationContext", "type": "object", "properties": { "artifact_service": { "default": null, "title": "Artifact Service" }, "session_service": { "default": null, "title": "Session Service" }, "memory_service": { "default": null, "title": "Memory Service" }, "credential_service": { "default": null, "title": "Credential Service" }, "context_cache_config": { "anyOf": [ { "$ref": "#/$defs/ContextCacheConfig" }, { "type": "null" } ], "default": null }, "invocation_id": { "title": "Invocation Id", "type": "string" }, "branch": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Branch" }, "agent": { "$ref": "#/$defs/BaseAgent" }, "user_content": { "anyOf": [ { "$ref": "#/$defs/Content" }, { "type": "null" } ], "default": null }, "session": { "$ref": "#/$defs/Session" }, "agent_states": { "additionalProperties": { "additionalProperties": true, "type": "object" }, "title": "Agent States", "type": "object" }, "end_of_agents": { "additionalProperties": { "type": "boolean" }, "title": "End Of Agents", "type": "object" }, "end_invocation": { "default": false, "title": "End Invocation", "type": "boolean" }, "live_request_queue": { "default": null, "title": "Live Request Queue" }, "active_streaming_tools": { "default": null, "title": "Active Streaming Tools" }, "transcription_cache": { "anyOf": [ { "items": { "$ref": "#/$defs/TranscriptionEntry" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Transcription Cache" }, "live_session_resumption_handle": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Live Session Resumption Handle" }, "input_realtime_cache": { "anyOf": [ { "items": { "$ref": "#/$defs/RealtimeCacheEntry" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Input Realtime Cache" }, "output_realtime_cache": { "anyOf": [ { "items": { "$ref": "#/$defs/RealtimeCacheEntry" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Output Realtime Cache" }, "run_config": { "anyOf": [ { "$ref": "#/$defs/RunConfig" }, { "type": "null" } ], "default": null }, "resumability_config": { "anyOf": [ { "$ref": "#/$defs/ResumabilityConfig" }, { "type": "null" } ], "default": null }, "plugin_manager": { "default": null, "title": "Plugin Manager" }, "canonical_tools_cache": { "default": null, "title": "Canonical Tools Cache" } }, "$defs": { "APIKey": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "apiKey" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "in": { "$ref": "#/$defs/APIKeyIn" }, "name": { "title": "Name", "type": "string" } }, "required": [ "in", "name" ], "title": "APIKey", "type": "object" }, "APIKeyIn": { "enum": [ "query", "header", "cookie" ], "title": "APIKeyIn", "type": "string" }, "ActivityHandling": { "description": "The different ways of handling user activity.", "enum": [ "ACTIVITY_HANDLING_UNSPECIFIED", "START_OF_ACTIVITY_INTERRUPTS", "NO_INTERRUPTION" ], "title": "ActivityHandling", "type": "string" }, "AudioTranscriptionConfig": { "additionalProperties": false, "description": "The audio transcription configuration in Setup.", "properties": {}, "title": "AudioTranscriptionConfig", "type": "object" }, "AuthConfig": { "additionalProperties": true, "description": "The auth config sent by tool asking client to collect auth credentials and\n\nadk and client will help to fill in the response", "properties": { "authScheme": { "anyOf": [ { "$ref": "#/$defs/APIKey" }, { "$ref": "#/$defs/HTTPBase" }, { "$ref": "#/$defs/OAuth2" }, { "$ref": "#/$defs/OpenIdConnect" }, { "$ref": "#/$defs/HTTPBearer" }, { "$ref": "#/$defs/OpenIdConnectWithConfig" } ], "title": "Authscheme" }, "rawAuthCredential": { "anyOf": [ { "$ref": "#/$defs/AuthCredential" }, { "type": "null" } ], "default": null }, "exchangedAuthCredential": { "anyOf": [ { "$ref": "#/$defs/AuthCredential" }, { "type": "null" } ], "default": null }, "credentialKey": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Credentialkey" } }, "required": [ "authScheme" ], "title": "AuthConfig", "type": "object" }, "AuthCredential": { "additionalProperties": true, "description": "Data class representing an authentication credential.\n\nTo exchange for the actual credential, please use\nCredentialExchanger.exchange_credential().\n\nExamples: API Key Auth\nAuthCredential(\n auth_type=AuthCredentialTypes.API_KEY,\n api_key=\"1234\",\n)\n\nExample: HTTP Auth\nAuthCredential(\n auth_type=AuthCredentialTypes.HTTP,\n http=HttpAuth(\n scheme=\"basic\",\n credentials=HttpCredentials(username=\"user\", password=\"password\"),\n ),\n)\n\nExample: OAuth2 Bearer Token in HTTP Header\nAuthCredential(\n auth_type=AuthCredentialTypes.HTTP,\n http=HttpAuth(\n scheme=\"bearer\",\n credentials=HttpCredentials(token=\"eyAkaknabna....\"),\n ),\n)\n\nExample: OAuth2 Auth with Authorization Code Flow\nAuthCredential(\n auth_type=AuthCredentialTypes.OAUTH2,\n oauth2=OAuth2Auth(\n client_id=\"1234\",\n client_secret=\"secret\",\n ),\n)\n\nExample: OpenID Connect Auth\nAuthCredential(\n auth_type=AuthCredentialTypes.OPEN_ID_CONNECT,\n oauth2=OAuth2Auth(\n client_id=\"1234\",\n client_secret=\"secret\",\n redirect_uri=\"https://example.com\",\n scopes=[\"scope1\", \"scope2\"],\n ),\n)\n\nExample: Auth with resource reference\nAuthCredential(\n auth_type=AuthCredentialTypes.API_KEY,\n resource_ref=\"projects/1234/locations/us-central1/resources/resource1\",\n)", "properties": { "authType": { "$ref": "#/$defs/AuthCredentialTypes" }, "resourceRef": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Resourceref" }, "apiKey": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Apikey" }, "http": { "anyOf": [ { "$ref": "#/$defs/HttpAuth" }, { "type": "null" } ], "default": null }, "serviceAccount": { "anyOf": [ { "$ref": "#/$defs/ServiceAccount" }, { "type": "null" } ], "default": null }, "oauth2": { "anyOf": [ { "$ref": "#/$defs/OAuth2Auth" }, { "type": "null" } ], "default": null } }, "required": [ "authType" ], "title": "AuthCredential", "type": "object" }, "AuthCredentialTypes": { "description": "Represents the type of authentication credential.", "enum": [ "apiKey", "http", "oauth2", "openIdConnect", "serviceAccount" ], "title": "AuthCredentialTypes", "type": "string" }, "AutomaticActivityDetection": { "additionalProperties": false, "description": "Configures automatic detection of activity.", "properties": { "disabled": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "If enabled, detected voice and text input count as activity. If disabled, the client must send activity signals.", "title": "Disabled" }, "startOfSpeechSensitivity": { "anyOf": [ { "$ref": "#/$defs/StartSensitivity" }, { "type": "null" } ], "default": null, "description": "Determines how likely speech is to be detected." }, "endOfSpeechSensitivity": { "anyOf": [ { "$ref": "#/$defs/EndSensitivity" }, { "type": "null" } ], "default": null, "description": "Determines how likely detected speech is ended." }, "prefixPaddingMs": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "The required duration of detected speech before start-of-speech is committed. The lower this value the more sensitive the start-of-speech detection is and the shorter speech can be recognized. However, this also increases the probability of false positives.", "title": "Prefixpaddingms" }, "silenceDurationMs": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "The required duration of detected non-speech (e.g. silence) before end-of-speech is committed. The larger this value, the longer speech gaps can be without interrupting the user's activity but this will increase the model's latency.", "title": "Silencedurationms" } }, "title": "AutomaticActivityDetection", "type": "object" }, "BaseAgent": { "additionalProperties": false, "description": "Base class for all agents in Agent Development Kit.", "properties": { "name": { "title": "Name", "type": "string" }, "description": { "default": "", "title": "Description", "type": "string" }, "parent_agent": { "anyOf": [ { "$ref": "#/$defs/BaseAgent" }, { "type": "null" } ], "default": null }, "sub_agents": { "items": { "$ref": "#/$defs/BaseAgent" }, "title": "Sub Agents", "type": "array" }, "before_agent_callback": { "default": null, "title": "Before Agent Callback", "type": "null" }, "after_agent_callback": { "default": null, "title": "After Agent Callback", "type": "null" } }, "required": [ "name" ], "title": "BaseAgent", "type": "object" }, "Blob": { "additionalProperties": false, "description": "Content blob.", "properties": { "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Raw bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob. Used to provide a label or filename to distinguish blobs. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "Blob", "type": "object" }, "CacheMetadata": { "additionalProperties": false, "description": "Metadata for context cache associated with LLM responses.\n\nThis class stores cache identification, usage tracking, and lifecycle\ninformation for a particular cache instance. It can be in two states:\n\n1. Active cache state: cache_name is set, all fields populated\n2. Fingerprint-only state: cache_name is None, only fingerprint and\n contents_count are set for prefix matching\n\nToken counts (cached and total) are available in the LlmResponse.usage_metadata\nand should be accessed from there to avoid duplication.\n\nAttributes:\n cache_name: The full resource name of the cached content (e.g.,\n 'projects/123/locations/us-central1/cachedContents/456').\n None when no active cache exists (fingerprint-only state).\n expire_time: Unix timestamp when the cache expires. None when no\n active cache exists.\n fingerprint: Hash of cacheable contents (instruction + tools + contents).\n Always present for prefix matching.\n invocations_used: Number of invocations this cache has been used for.\n None when no active cache exists.\n contents_count: Number of contents. When active cache exists, this is\n the count of cached contents. When no active cache exists, this is\n the total count of contents in the request.\n created_at: Unix timestamp when the cache was created. None when\n no active cache exists.", "properties": { "cache_name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Full resource name of the cached content (None if no active cache)", "title": "Cache Name" }, "expire_time": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Unix timestamp when cache expires (None if no active cache)", "title": "Expire Time" }, "fingerprint": { "description": "Hash of cacheable contents used to detect changes", "title": "Fingerprint", "type": "string" }, "invocations_used": { "anyOf": [ { "minimum": 0, "type": "integer" }, { "type": "null" } ], "default": null, "description": "Number of invocations this cache has been used for (None if no active cache)", "title": "Invocations Used" }, "contents_count": { "description": "Number of contents (cached contents when active cache exists, total contents in request when no active cache)", "minimum": 0, "title": "Contents Count", "type": "integer" }, "created_at": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Unix timestamp when cache was created (None if no active cache)", "title": "Created At" } }, "required": [ "fingerprint", "contents_count" ], "title": "CacheMetadata", "type": "object" }, "Citation": { "additionalProperties": false, "description": "Source attributions for content.\n\nThis data type is not supported in Gemini API.", "properties": { "endIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. End index into the content.", "title": "Endindex" }, "license": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. License of the attribution.", "title": "License" }, "publicationDate": { "anyOf": [ { "$ref": "#/$defs/GoogleTypeDate" }, { "type": "null" } ], "default": null, "description": "Output only. Publication date of the attribution." }, "startIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. Start index into the content.", "title": "Startindex" }, "title": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. Title of the attribution.", "title": "Title" }, "uri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. Url reference of the attribution.", "title": "Uri" } }, "title": "Citation", "type": "object" }, "CitationMetadata": { "additionalProperties": false, "description": "Citation information when the model quotes another source.", "properties": { "citations": { "anyOf": [ { "items": { "$ref": "#/$defs/Citation" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Contains citation information when the model directly quotes, at\n length, from another source. Can include traditional websites and code\n repositories.\n ", "title": "Citations" } }, "title": "CitationMetadata", "type": "object" }, "CodeExecutionResult": { "additionalProperties": false, "description": "Result of executing the [ExecutableCode].\n\nOnly generated when using the [CodeExecution] tool, and always follows a\n`part` containing the [ExecutableCode].", "properties": { "outcome": { "anyOf": [ { "$ref": "#/$defs/Outcome" }, { "type": "null" } ], "default": null, "description": "Required. Outcome of the code execution." }, "output": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Contains stdout when code execution is successful, stderr or other description otherwise.", "title": "Output" } }, "title": "CodeExecutionResult", "type": "object" }, "Content": { "additionalProperties": false, "description": "Contains the multi-part content of a message.", "properties": { "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/Part" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a single message. Each part may have\n a different IANA MIME type.", "title": "Parts" }, "role": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The producer of the content. Must be either 'user' or 'model'. Useful to set for multi-turn conversations, otherwise can be left blank or unset.", "title": "Role" } }, "title": "Content", "type": "object" }, "ContextCacheConfig": { "additionalProperties": false, "description": "Configuration for context caching across all agents in an app.\n\nThis configuration enables and controls context caching behavior for\nall LLM agents in an app. When this config is present on an app, context\ncaching is enabled for all agents. When absent (None), context caching\nis disabled.\n\nContext caching can significantly reduce costs and improve response times\nby reusing previously processed context across multiple requests.\n\nAttributes:\n cache_intervals: Maximum number of invocations to reuse the same cache before refreshing it\n ttl_seconds: Time-to-live for cache in seconds\n min_tokens: Minimum tokens required to enable caching", "properties": { "cache_intervals": { "default": 10, "description": "Maximum number of invocations to reuse the same cache before refreshing it", "maximum": 100, "minimum": 1, "title": "Cache Intervals", "type": "integer" }, "ttl_seconds": { "default": 1800, "description": "Time-to-live for cache in seconds", "exclusiveMinimum": 0, "title": "Ttl Seconds", "type": "integer" }, "min_tokens": { "default": 0, "description": "Minimum estimated request tokens required to enable caching. This compares against the estimated total tokens of the request (system instruction + tools + contents). Context cache storage may have cost. Set higher to avoid caching small requests where overhead may exceed benefits.", "minimum": 0, "title": "Min Tokens", "type": "integer" } }, "title": "ContextCacheConfig", "type": "object" }, "ContextWindowCompressionConfig": { "additionalProperties": false, "description": "Enables context window compression -- mechanism managing model context window so it does not exceed given length.", "properties": { "triggerTokens": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Number of tokens (before running turn) that triggers context window compression mechanism.", "title": "Triggertokens" }, "slidingWindow": { "anyOf": [ { "$ref": "#/$defs/SlidingWindow" }, { "type": "null" } ], "default": null, "description": "Sliding window compression mechanism." } }, "title": "ContextWindowCompressionConfig", "type": "object" }, "EndSensitivity": { "description": "End of speech sensitivity.", "enum": [ "END_SENSITIVITY_UNSPECIFIED", "END_SENSITIVITY_HIGH", "END_SENSITIVITY_LOW" ], "title": "EndSensitivity", "type": "string" }, "Event": { "additionalProperties": false, "description": "Represents an event in a conversation between agents and users.\n\nIt is used to store the content of the conversation, as well as the actions\ntaken by the agents like function calls, etc.", "properties": { "modelVersion": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Modelversion" }, "content": { "anyOf": [ { "$ref": "#/$defs/Content" }, { "type": "null" } ], "default": null }, "groundingMetadata": { "anyOf": [ { "$ref": "#/$defs/GroundingMetadata" }, { "type": "null" } ], "default": null }, "partial": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Partial" }, "turnComplete": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Turncomplete" }, "finishReason": { "anyOf": [ { "$ref": "#/$defs/FinishReason" }, { "type": "null" } ], "default": null }, "errorCode": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Errorcode" }, "errorMessage": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Errormessage" }, "interrupted": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Interrupted" }, "customMetadata": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "title": "Custommetadata" }, "usageMetadata": { "anyOf": [ { "$ref": "#/$defs/GenerateContentResponseUsageMetadata" }, { "type": "null" } ], "default": null }, "liveSessionResumptionUpdate": { "anyOf": [ { "$ref": "#/$defs/LiveServerSessionResumptionUpdate" }, { "type": "null" } ], "default": null }, "inputTranscription": { "anyOf": [ { "$ref": "#/$defs/Transcription" }, { "type": "null" } ], "default": null }, "outputTranscription": { "anyOf": [ { "$ref": "#/$defs/Transcription" }, { "type": "null" } ], "default": null }, "avgLogprobs": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "title": "Avglogprobs" }, "logprobsResult": { "anyOf": [ { "$ref": "#/$defs/LogprobsResult" }, { "type": "null" } ], "default": null }, "cacheMetadata": { "anyOf": [ { "$ref": "#/$defs/CacheMetadata" }, { "type": "null" } ], "default": null }, "citationMetadata": { "anyOf": [ { "$ref": "#/$defs/CitationMetadata" }, { "type": "null" } ], "default": null }, "interactionId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Interactionid" }, "invocationId": { "default": "", "title": "Invocationid", "type": "string" }, "author": { "title": "Author", "type": "string" }, "actions": { "$ref": "#/$defs/EventActions" }, "longRunningToolIds": { "anyOf": [ { "items": { "type": "string" }, "type": "array", "uniqueItems": true }, { "type": "null" } ], "default": null, "title": "Longrunningtoolids" }, "branch": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Branch" }, "id": { "default": "", "title": "Id", "type": "string" }, "timestamp": { "title": "Timestamp", "type": "number" } }, "required": [ "author" ], "title": "Event", "type": "object" }, "EventActions": { "additionalProperties": false, "description": "Represents the actions attached to an event.", "properties": { "skipSummarization": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Skipsummarization" }, "stateDelta": { "additionalProperties": true, "title": "Statedelta", "type": "object" }, "artifactDelta": { "additionalProperties": { "type": "integer" }, "title": "Artifactdelta", "type": "object" }, "transferToAgent": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Transfertoagent" }, "escalate": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Escalate" }, "requestedAuthConfigs": { "additionalProperties": { "$ref": "#/$defs/AuthConfig" }, "title": "Requestedauthconfigs", "type": "object" }, "requestedToolConfirmations": { "additionalProperties": { "$ref": "#/$defs/ToolConfirmation" }, "title": "Requestedtoolconfirmations", "type": "object" }, "compaction": { "anyOf": [ { "$ref": "#/$defs/EventCompaction" }, { "type": "null" } ], "default": null }, "endOfAgent": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Endofagent" }, "agentState": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "title": "Agentstate" }, "rewindBeforeInvocationId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Rewindbeforeinvocationid" } }, "title": "EventActions", "type": "object" }, "EventCompaction": { "additionalProperties": false, "description": "The compaction of the events.", "properties": { "startTimestamp": { "title": "Starttimestamp", "type": "number" }, "endTimestamp": { "title": "Endtimestamp", "type": "number" }, "compactedContent": { "$ref": "#/$defs/Content" } }, "required": [ "startTimestamp", "endTimestamp", "compactedContent" ], "title": "EventCompaction", "type": "object" }, "ExecutableCode": { "additionalProperties": false, "description": "Code generated by the model that is meant to be executed, and the result returned to the model.\n\nGenerated when using the [CodeExecution] tool, in which the code will be\nautomatically executed, and a corresponding [CodeExecutionResult] will also be\ngenerated.", "properties": { "code": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The code to be executed.", "title": "Code" }, "language": { "anyOf": [ { "$ref": "#/$defs/Language" }, { "type": "null" } ], "default": null, "description": "Required. Programming language of the `code`." } }, "title": "ExecutableCode", "type": "object" }, "FileData": { "additionalProperties": false, "description": "URI based data.", "properties": { "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file data. Used to provide a label or filename to distinguish file datas. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "FileData", "type": "object" }, "FinishReason": { "description": "Output only. The reason why the model stopped generating tokens.\n\nIf empty, the model has not stopped generating the tokens.", "enum": [ "FINISH_REASON_UNSPECIFIED", "STOP", "MAX_TOKENS", "SAFETY", "RECITATION", "LANGUAGE", "OTHER", "BLOCKLIST", "PROHIBITED_CONTENT", "SPII", "MALFORMED_FUNCTION_CALL", "IMAGE_SAFETY", "UNEXPECTED_TOOL_CALL", "IMAGE_PROHIBITED_CONTENT", "NO_IMAGE", "IMAGE_RECITATION", "IMAGE_OTHER" ], "title": "FinishReason", "type": "string" }, "FunctionCall": { "additionalProperties": false, "description": "A function call.", "properties": { "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The unique id of the function call. If populated, the client to execute the\n `function_call` and return the response with the matching `id`.", "title": "Id" }, "args": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Optional. The function parameters and values in JSON object format. See [FunctionDeclaration.parameters] for parameter details.", "title": "Args" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The name of the function to call. Matches [FunctionDeclaration.name].", "title": "Name" }, "partialArgs": { "anyOf": [ { "items": { "$ref": "#/$defs/PartialArg" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. The partial argument value of the function call. If provided, represents the arguments/fields that are streamed incrementally. This field is not supported in Gemini API.", "title": "Partialargs" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is the last part of the FunctionCall. If true, another partial message for the current FunctionCall is expected to follow. This field is not supported in Gemini API.", "title": "Willcontinue" } }, "title": "FunctionCall", "type": "object" }, "FunctionResponse": { "additionalProperties": false, "description": "A function response.", "properties": { "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Signals that function call continues, and more responses will be returned, turning the function call into a generator. Is only applicable to NON_BLOCKING function calls (see FunctionDeclaration.behavior for details), ignored otherwise. If false, the default, future responses will not be considered. Is only applicable to NON_BLOCKING function calls, is ignored otherwise. If set to false, future responses will not be considered. It is allowed to return empty `response` with `will_continue=False` to signal that the function call is finished.", "title": "Willcontinue" }, "scheduling": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseScheduling" }, { "type": "null" } ], "default": null, "description": "Specifies how the response should be scheduled in the conversation. Only applicable to NON_BLOCKING function calls, is ignored otherwise. Defaults to WHEN_IDLE." }, "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/FunctionResponsePart" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a function response. Each part may\n have a different IANA MIME type.", "title": "Parts" }, "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The id of the function call this response is for. Populated by the client to match the corresponding function call `id`.", "title": "Id" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The name of the function to call. Matches [FunctionDeclaration.name] and [FunctionCall.name].", "title": "Name" }, "response": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Required. The function response in JSON object format. Use \"output\" key to specify function output and \"error\" key to specify error details (if any). If \"output\" and \"error\" keys are not specified, then whole \"response\" is treated as function output.", "title": "Response" } }, "title": "FunctionResponse", "type": "object" }, "FunctionResponseBlob": { "additionalProperties": false, "description": "Raw media bytes for function response.\n\nText should not be sent as raw bytes, use the FunctionResponse.response\nfield.", "properties": { "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Inline media bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob.\n Used to provide a label or filename to distinguish blobs.", "title": "Displayname" } }, "title": "FunctionResponseBlob", "type": "object" }, "FunctionResponseFileData": { "additionalProperties": false, "description": "URI based data for function response.", "properties": { "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file.\n Used to provide a label or filename to distinguish files.", "title": "Displayname" } }, "title": "FunctionResponseFileData", "type": "object" }, "FunctionResponsePart": { "additionalProperties": false, "description": "A datatype containing media that is part of a `FunctionResponse` message.\n\nA `FunctionResponsePart` consists of data which has an associated datatype. A\n`FunctionResponsePart` can only contain one of the accepted types in\n`FunctionResponsePart.data`.\n\nA `FunctionResponsePart` must have a fixed IANA MIME type identifying the\ntype and subtype of the media if the `inline_data` field is filled with raw\nbytes.", "properties": { "inlineData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseBlob" }, { "type": "null" } ], "default": null, "description": "Optional. Inline media bytes." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseFileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." } }, "title": "FunctionResponsePart", "type": "object" }, "FunctionResponseScheduling": { "description": "Specifies how the response should be scheduled in the conversation.", "enum": [ "SCHEDULING_UNSPECIFIED", "SILENT", "WHEN_IDLE", "INTERRUPT" ], "title": "FunctionResponseScheduling", "type": "string" }, "GenerateContentResponseUsageMetadata": { "additionalProperties": false, "description": "Usage metadata about the content generation request and response.\n\nThis message provides a detailed breakdown of token usage and other relevant\nmetrics. This data type is not supported in Gemini API.", "properties": { "cacheTokensDetails": { "anyOf": [ { "items": { "$ref": "#/$defs/ModalityTokenCount" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Output only. A detailed breakdown of the token count for each modality in the cached content.", "title": "Cachetokensdetails" }, "cachedContentTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. The number of tokens in the cached content that was used for this request.", "title": "Cachedcontenttokencount" }, "candidatesTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "The total number of tokens in the generated candidates.", "title": "Candidatestokencount" }, "candidatesTokensDetails": { "anyOf": [ { "items": { "$ref": "#/$defs/ModalityTokenCount" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Output only. A detailed breakdown of the token count for each modality in the generated candidates.", "title": "Candidatestokensdetails" }, "promptTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "The total number of tokens in the prompt. This includes any text, images, or other media provided in the request. When `cached_content` is set, this also includes the number of tokens in the cached content.", "title": "Prompttokencount" }, "promptTokensDetails": { "anyOf": [ { "items": { "$ref": "#/$defs/ModalityTokenCount" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Output only. A detailed breakdown of the token count for each modality in the prompt.", "title": "Prompttokensdetails" }, "thoughtsTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. The number of tokens that were part of the model's generated \"thoughts\" output, if applicable.", "title": "Thoughtstokencount" }, "toolUsePromptTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. The number of tokens in the results from tool executions, which are provided back to the model as input, if applicable.", "title": "Tooluseprompttokencount" }, "toolUsePromptTokensDetails": { "anyOf": [ { "items": { "$ref": "#/$defs/ModalityTokenCount" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Output only. A detailed breakdown by modality of the token counts from the results of tool executions, which are provided back to the model as input.", "title": "Tooluseprompttokensdetails" }, "totalTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "The total number of tokens for the entire request. This is the sum of `prompt_token_count`, `candidates_token_count`, `tool_use_prompt_token_count`, and `thoughts_token_count`.", "title": "Totaltokencount" }, "trafficType": { "anyOf": [ { "$ref": "#/$defs/TrafficType" }, { "type": "null" } ], "default": null, "description": "Output only. The traffic type for this request." } }, "title": "GenerateContentResponseUsageMetadata", "type": "object" }, "GoogleTypeDate": { "additionalProperties": false, "description": "Represents a whole or partial calendar date, such as a birthday.\n\nThe time of day and time zone are either specified elsewhere or are\ninsignificant. The date is relative to the Gregorian Calendar. This can\nrepresent one of the following: * A full date, with non-zero year, month, and\nday values. * A month and day, with a zero year (for example, an anniversary).\n* A year on its own, with a zero month and a zero day. * A year and month,\nwith a zero day (for example, a credit card expiration date). Related types: *\ngoogle.type.TimeOfDay * google.type.DateTime * google.protobuf.Timestamp. This\ndata type is not supported in Gemini API.", "properties": { "day": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Day of a month. Must be from 1 to 31 and valid for the year and month, or 0 to specify a year by itself or a year and month where the day isn't significant.", "title": "Day" }, "month": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Month of a year. Must be from 1 to 12, or 0 to specify a year without a month and day.", "title": "Month" }, "year": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Year of the date. Must be from 1 to 9999, or 0 to specify a date without a year.", "title": "Year" } }, "title": "GoogleTypeDate", "type": "object" }, "GroundingChunk": { "additionalProperties": false, "description": "Grounding chunk.", "properties": { "maps": { "anyOf": [ { "$ref": "#/$defs/GroundingChunkMaps" }, { "type": "null" } ], "default": null, "description": "Grounding chunk from Google Maps. This field is not supported in Gemini API." }, "retrievedContext": { "anyOf": [ { "$ref": "#/$defs/GroundingChunkRetrievedContext" }, { "type": "null" } ], "default": null, "description": "Grounding chunk from context retrieved by the retrieval tools. This field is not supported in Gemini API." }, "web": { "anyOf": [ { "$ref": "#/$defs/GroundingChunkWeb" }, { "type": "null" } ], "default": null, "description": "Grounding chunk from the web." } }, "title": "GroundingChunk", "type": "object" }, "GroundingChunkMaps": { "additionalProperties": false, "description": "Chunk from Google Maps. This data type is not supported in Gemini API.", "properties": { "placeAnswerSources": { "anyOf": [ { "$ref": "#/$defs/GroundingChunkMapsPlaceAnswerSources" }, { "type": "null" } ], "default": null, "description": "Sources used to generate the place answer. This includes review snippets and photos that were used to generate the answer, as well as uris to flag content." }, "placeId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "This Place's resource name, in `places/{place_id}` format. Can be used to look up the Place.", "title": "Placeid" }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Text of the place answer.", "title": "Text" }, "title": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Title of the place.", "title": "Title" }, "uri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "URI reference of the place.", "title": "Uri" } }, "title": "GroundingChunkMaps", "type": "object" }, "GroundingChunkMapsPlaceAnswerSources": { "additionalProperties": false, "description": "Sources used to generate the place answer.\n\nThis data type is not supported in Gemini API.", "properties": { "flagContentUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A link where users can flag a problem with the generated answer.", "title": "Flagcontenturi" }, "reviewSnippets": { "anyOf": [ { "items": { "$ref": "#/$defs/GroundingChunkMapsPlaceAnswerSourcesReviewSnippet" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Snippets of reviews that are used to generate the answer.", "title": "Reviewsnippets" } }, "title": "GroundingChunkMapsPlaceAnswerSources", "type": "object" }, "GroundingChunkMapsPlaceAnswerSourcesAuthorAttribution": { "additionalProperties": false, "description": "Author attribution for a photo or review.\n\nThis data type is not supported in Gemini API.", "properties": { "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Name of the author of the Photo or Review.", "title": "Displayname" }, "photoUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Profile photo URI of the author of the Photo or Review.", "title": "Photouri" }, "uri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "URI of the author of the Photo or Review.", "title": "Uri" } }, "title": "GroundingChunkMapsPlaceAnswerSourcesAuthorAttribution", "type": "object" }, "GroundingChunkMapsPlaceAnswerSourcesReviewSnippet": { "additionalProperties": false, "description": "Encapsulates a review snippet.\n\nThis data type is not supported in Gemini API.", "properties": { "authorAttribution": { "anyOf": [ { "$ref": "#/$defs/GroundingChunkMapsPlaceAnswerSourcesAuthorAttribution" }, { "type": "null" } ], "default": null, "description": "This review's author." }, "flagContentUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A link where users can flag a problem with the review.", "title": "Flagcontenturi" }, "googleMapsUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A link to show the review on Google Maps.", "title": "Googlemapsuri" }, "relativePublishTimeDescription": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A string of formatted recent time, expressing the review time relative to the current time in a form appropriate for the language and country.", "title": "Relativepublishtimedescription" }, "review": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A reference representing this place review which may be used to look up this place review again.", "title": "Review" }, "reviewId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Id of the review referencing the place.", "title": "Reviewid" }, "title": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Title of the review.", "title": "Title" } }, "title": "GroundingChunkMapsPlaceAnswerSourcesReviewSnippet", "type": "object" }, "GroundingChunkRetrievedContext": { "additionalProperties": false, "description": "Chunk from context retrieved by the retrieval tools.\n\nThis data type is not supported in Gemini API.", "properties": { "documentName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. The full document name for the referenced Vertex AI Search document.", "title": "Documentname" }, "ragChunk": { "anyOf": [ { "$ref": "#/$defs/RagChunk" }, { "type": "null" } ], "default": null, "description": "Additional context for the RAG retrieval result. This is only populated when using the RAG retrieval tool." }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Text of the attribution.", "title": "Text" }, "title": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Title of the attribution.", "title": "Title" }, "uri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "URI reference of the attribution.", "title": "Uri" } }, "title": "GroundingChunkRetrievedContext", "type": "object" }, "GroundingChunkWeb": { "additionalProperties": false, "description": "Chunk from the web.", "properties": { "domain": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Domain of the (original) URI. This field is not supported in Gemini API.", "title": "Domain" }, "title": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Title of the chunk.", "title": "Title" }, "uri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "URI reference of the chunk.", "title": "Uri" } }, "title": "GroundingChunkWeb", "type": "object" }, "GroundingMetadata": { "additionalProperties": false, "description": "Metadata returned to client when grounding is enabled.", "properties": { "googleMapsWidgetContextToken": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Output only. Resource name of the Google Maps widget context token to be used with the PlacesContextElement widget to render contextual data. This is populated only for Google Maps grounding. This field is not supported in Gemini API.", "title": "Googlemapswidgetcontexttoken" }, "groundingChunks": { "anyOf": [ { "items": { "$ref": "#/$defs/GroundingChunk" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of supporting references retrieved from specified grounding source.", "title": "Groundingchunks" }, "groundingSupports": { "anyOf": [ { "items": { "$ref": "#/$defs/GroundingSupport" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. List of grounding support.", "title": "Groundingsupports" }, "retrievalMetadata": { "anyOf": [ { "$ref": "#/$defs/RetrievalMetadata" }, { "type": "null" } ], "default": null, "description": "Optional. Output only. Retrieval metadata." }, "retrievalQueries": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. Queries executed by the retrieval tools. This field is not supported in Gemini API.", "title": "Retrievalqueries" }, "searchEntryPoint": { "anyOf": [ { "$ref": "#/$defs/SearchEntryPoint" }, { "type": "null" } ], "default": null, "description": "Optional. Google search entry for the following-up web searches." }, "sourceFlaggingUris": { "anyOf": [ { "items": { "$ref": "#/$defs/GroundingMetadataSourceFlaggingUri" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. Output only. List of source flagging uris. This is currently populated only for Google Maps grounding. This field is not supported in Gemini API.", "title": "Sourceflagginguris" }, "webSearchQueries": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. Web search queries for the following-up web search.", "title": "Websearchqueries" } }, "title": "GroundingMetadata", "type": "object" }, "GroundingMetadataSourceFlaggingUri": { "additionalProperties": false, "description": "Source content flagging uri for a place or review.\n\nThis is currently populated only for Google Maps grounding. This data type is\nnot supported in Gemini API.", "properties": { "flagContentUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A link where users can flag a problem with the source (place or review).", "title": "Flagcontenturi" }, "sourceId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Id of the place or review.", "title": "Sourceid" } }, "title": "GroundingMetadataSourceFlaggingUri", "type": "object" }, "GroundingSupport": { "additionalProperties": false, "description": "Grounding support.", "properties": { "confidenceScores": { "anyOf": [ { "items": { "type": "number" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Confidence score of the support references. Ranges from 0 to 1. 1 is the most confident. For Gemini 2.0 and before, this list must have the same size as the grounding_chunk_indices. For Gemini 2.5 and after, this list will be empty and should be ignored.", "title": "Confidencescores" }, "groundingChunkIndices": { "anyOf": [ { "items": { "type": "integer" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "A list of indices (into 'grounding_chunk') specifying the citations associated with the claim. For instance [1,3,4] means that grounding_chunk[1], grounding_chunk[3], grounding_chunk[4] are the retrieved content attributed to the claim.", "title": "Groundingchunkindices" }, "segment": { "anyOf": [ { "$ref": "#/$defs/Segment" }, { "type": "null" } ], "default": null, "description": "Segment of the content this support belongs to." } }, "title": "GroundingSupport", "type": "object" }, "HTTPBase": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "http" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "scheme": { "title": "Scheme", "type": "string" } }, "required": [ "scheme" ], "title": "HTTPBase", "type": "object" }, "HTTPBearer": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "http" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "scheme": { "const": "bearer", "default": "bearer", "title": "Scheme", "type": "string" }, "bearerFormat": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Bearerformat" } }, "title": "HTTPBearer", "type": "object" }, "HttpAuth": { "additionalProperties": true, "description": "The credentials and metadata for HTTP authentication.", "properties": { "scheme": { "title": "Scheme", "type": "string" }, "credentials": { "$ref": "#/$defs/HttpCredentials" } }, "required": [ "scheme", "credentials" ], "title": "HttpAuth", "type": "object" }, "HttpCredentials": { "additionalProperties": true, "description": "Represents the secret token value for HTTP authentication, like user name, password, oauth token, etc.", "properties": { "username": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Username" }, "password": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Password" }, "token": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Token" } }, "title": "HttpCredentials", "type": "object" }, "Language": { "description": "Programming language of the `code`.", "enum": [ "LANGUAGE_UNSPECIFIED", "PYTHON" ], "title": "Language", "type": "string" }, "LiveServerSessionResumptionUpdate": { "additionalProperties": false, "description": "Update of the session resumption state.\n\nOnly sent if `session_resumption` was set in the connection config.", "properties": { "newHandle": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "New handle that represents state that can be resumed. Empty if `resumable`=false.", "title": "Newhandle" }, "resumable": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "True if session can be resumed at this point. It might be not possible to resume session at some points. In that case we send update empty new_handle and resumable=false. Example of such case could be model executing function calls or just generating. Resuming session (using previous session token) in such state will result in some data loss.", "title": "Resumable" }, "lastConsumedClientMessageIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Index of last message sent by client that is included in state represented by this SessionResumptionToken. Only sent when `SessionResumptionConfig.transparent` is set.\n\nPresence of this index allows users to transparently reconnect and avoid issue of losing some part of realtime audio input/video. If client wishes to temporarily disconnect (for example as result of receiving GoAway) they can do it without losing state by buffering messages sent since last `SessionResmumptionTokenUpdate`. This field will enable them to limit buffering (avoid keeping all requests in RAM).\n\nNote: This should not be used for when resuming a session at some time later -- in those cases partial audio and video frames arelikely not needed.", "title": "Lastconsumedclientmessageindex" } }, "title": "LiveServerSessionResumptionUpdate", "type": "object" }, "LogprobsResult": { "additionalProperties": false, "description": "Logprobs Result", "properties": { "chosenCandidates": { "anyOf": [ { "items": { "$ref": "#/$defs/LogprobsResultCandidate" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Length = total number of decoding steps. The chosen candidates may or may not be in top_candidates.", "title": "Chosencandidates" }, "topCandidates": { "anyOf": [ { "items": { "$ref": "#/$defs/LogprobsResultTopCandidates" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Length = total number of decoding steps.", "title": "Topcandidates" } }, "title": "LogprobsResult", "type": "object" }, "LogprobsResultCandidate": { "additionalProperties": false, "description": "Candidate for the logprobs token and score.", "properties": { "logProbability": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "The candidate's log probability.", "title": "Logprobability" }, "token": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The candidate's token string value.", "title": "Token" }, "tokenId": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "The candidate's token id value.", "title": "Tokenid" } }, "title": "LogprobsResultCandidate", "type": "object" }, "LogprobsResultTopCandidates": { "additionalProperties": false, "description": "Candidates with top log probabilities at each decoding step.", "properties": { "candidates": { "anyOf": [ { "items": { "$ref": "#/$defs/LogprobsResultCandidate" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Sorted by log probability in descending order.", "title": "Candidates" } }, "title": "LogprobsResultTopCandidates", "type": "object" }, "MediaModality": { "description": "Server content modalities.", "enum": [ "MODALITY_UNSPECIFIED", "TEXT", "IMAGE", "VIDEO", "AUDIO", "DOCUMENT" ], "title": "MediaModality", "type": "string" }, "ModalityTokenCount": { "additionalProperties": false, "description": "Represents token counting info for a single modality.", "properties": { "modality": { "anyOf": [ { "$ref": "#/$defs/MediaModality" }, { "type": "null" } ], "default": null, "description": "The modality associated with this token count." }, "tokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Number of tokens.", "title": "Tokencount" } }, "title": "ModalityTokenCount", "type": "object" }, "MultiSpeakerVoiceConfig": { "additionalProperties": false, "description": "Configuration for a multi-speaker text-to-speech request.", "properties": { "speakerVoiceConfigs": { "anyOf": [ { "items": { "$ref": "#/$defs/SpeakerVoiceConfig" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Required. A list of configurations for the voices of the speakers. Exactly two speaker voice configurations must be provided.", "title": "Speakervoiceconfigs" } }, "title": "MultiSpeakerVoiceConfig", "type": "object" }, "OAuth2": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "oauth2" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "flows": { "$ref": "#/$defs/OAuthFlows" } }, "required": [ "flows" ], "title": "OAuth2", "type": "object" }, "OAuth2Auth": { "additionalProperties": true, "description": "Represents credential value and its metadata for a OAuth2 credential.", "properties": { "clientId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Clientid" }, "clientSecret": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Clientsecret" }, "authUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Authuri" }, "state": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "State" }, "redirectUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Redirecturi" }, "authResponseUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Authresponseuri" }, "authCode": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Authcode" }, "accessToken": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Accesstoken" }, "refreshToken": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshtoken" }, "expiresAt": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "title": "Expiresat" }, "expiresIn": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "title": "Expiresin" }, "audience": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Audience" }, "tokenEndpointAuthMethod": { "anyOf": [ { "enum": [ "client_secret_basic", "client_secret_post", "client_secret_jwt", "private_key_jwt" ], "type": "string" }, { "type": "null" } ], "default": "client_secret_basic", "title": "Tokenendpointauthmethod" } }, "title": "OAuth2Auth", "type": "object" }, "OAuthFlowAuthorizationCode": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "authorizationUrl": { "title": "Authorizationurl", "type": "string" }, "tokenUrl": { "title": "Tokenurl", "type": "string" } }, "required": [ "authorizationUrl", "tokenUrl" ], "title": "OAuthFlowAuthorizationCode", "type": "object" }, "OAuthFlowClientCredentials": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "tokenUrl": { "title": "Tokenurl", "type": "string" } }, "required": [ "tokenUrl" ], "title": "OAuthFlowClientCredentials", "type": "object" }, "OAuthFlowImplicit": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "authorizationUrl": { "title": "Authorizationurl", "type": "string" } }, "required": [ "authorizationUrl" ], "title": "OAuthFlowImplicit", "type": "object" }, "OAuthFlowPassword": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "tokenUrl": { "title": "Tokenurl", "type": "string" } }, "required": [ "tokenUrl" ], "title": "OAuthFlowPassword", "type": "object" }, "OAuthFlows": { "additionalProperties": true, "properties": { "implicit": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowImplicit" }, { "type": "null" } ], "default": null }, "password": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowPassword" }, { "type": "null" } ], "default": null }, "clientCredentials": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowClientCredentials" }, { "type": "null" } ], "default": null }, "authorizationCode": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowAuthorizationCode" }, { "type": "null" } ], "default": null } }, "title": "OAuthFlows", "type": "object" }, "OpenIdConnect": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "openIdConnect" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "openIdConnectUrl": { "title": "Openidconnecturl", "type": "string" } }, "required": [ "openIdConnectUrl" ], "title": "OpenIdConnect", "type": "object" }, "OpenIdConnectWithConfig": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "openIdConnect" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "authorization_endpoint": { "title": "Authorization Endpoint", "type": "string" }, "token_endpoint": { "title": "Token Endpoint", "type": "string" }, "userinfo_endpoint": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Userinfo Endpoint" }, "revocation_endpoint": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Revocation Endpoint" }, "token_endpoint_auth_methods_supported": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Token Endpoint Auth Methods Supported" }, "grant_types_supported": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Grant Types Supported" }, "scopes": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Scopes" } }, "required": [ "authorization_endpoint", "token_endpoint" ], "title": "OpenIdConnectWithConfig", "type": "object" }, "Outcome": { "description": "Outcome of the code execution.", "enum": [ "OUTCOME_UNSPECIFIED", "OUTCOME_OK", "OUTCOME_FAILED", "OUTCOME_DEADLINE_EXCEEDED" ], "title": "Outcome", "type": "string" }, "Part": { "additionalProperties": false, "description": "A datatype containing media content.\n\nExactly one field within a Part should be set, representing the specific type\nof content being conveyed. Using multiple fields within the same `Part`\ninstance is considered invalid.", "properties": { "mediaResolution": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolution" }, { "type": "null" } ], "default": null, "description": "Media resolution for the input media.\n " }, "codeExecutionResult": { "anyOf": [ { "$ref": "#/$defs/CodeExecutionResult" }, { "type": "null" } ], "default": null, "description": "Optional. Result of executing the [ExecutableCode]." }, "executableCode": { "anyOf": [ { "$ref": "#/$defs/ExecutableCode" }, { "type": "null" } ], "default": null, "description": "Optional. Code generated by the model that is meant to be executed." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." }, "functionCall": { "anyOf": [ { "$ref": "#/$defs/FunctionCall" }, { "type": "null" } ], "default": null, "description": "Optional. A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] with the parameters and their values." }, "functionResponse": { "anyOf": [ { "$ref": "#/$defs/FunctionResponse" }, { "type": "null" } ], "default": null, "description": "Optional. The result output of a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function call. It is used as context to the model." }, "inlineData": { "anyOf": [ { "$ref": "#/$defs/Blob" }, { "type": "null" } ], "default": null, "description": "Optional. Inlined bytes data." }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Text part (can be code).", "title": "Text" }, "thought": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Indicates if the part is thought from the model.", "title": "Thought" }, "thoughtSignature": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. An opaque signature for the thought so it can be reused in subsequent requests.", "title": "Thoughtsignature" }, "videoMetadata": { "anyOf": [ { "$ref": "#/$defs/VideoMetadata" }, { "type": "null" } ], "default": null, "description": "Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data." } }, "title": "Part", "type": "object" }, "PartMediaResolution": { "additionalProperties": false, "description": "Media resolution for the input media.", "properties": { "level": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolutionLevel" }, { "type": "null" } ], "default": null, "description": "The tokenization quality used for given media.\n " }, "numTokens": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Specifies the required sequence length for media tokenization.\n ", "title": "Numtokens" } }, "title": "PartMediaResolution", "type": "object" }, "PartMediaResolutionLevel": { "description": "The tokenization quality used for given media.", "enum": [ "MEDIA_RESOLUTION_UNSPECIFIED", "MEDIA_RESOLUTION_LOW", "MEDIA_RESOLUTION_MEDIUM", "MEDIA_RESOLUTION_HIGH", "MEDIA_RESOLUTION_ULTRA_HIGH" ], "title": "PartMediaResolutionLevel", "type": "string" }, "PartialArg": { "additionalProperties": false, "description": "Partial argument value of the function call.\n\nThis data type is not supported in Gemini API.", "properties": { "nullValue": { "anyOf": [ { "const": "NULL_VALUE", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a null value.", "title": "Nullvalue" }, "numberValue": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a double value.", "title": "Numbervalue" }, "stringValue": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a string value.", "title": "Stringvalue" }, "boolValue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a boolean value.", "title": "Boolvalue" }, "jsonPath": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. A JSON Path (RFC 9535) to the argument being streamed. https://datatracker.ietf.org/doc/html/rfc9535. e.g. \"$.foo.bar[0].data\".", "title": "Jsonpath" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is not the last part of the same json_path. If true, another PartialArg message for the current json_path is expected to follow.", "title": "Willcontinue" } }, "title": "PartialArg", "type": "object" }, "PrebuiltVoiceConfig": { "additionalProperties": false, "description": "The configuration for the prebuilt speaker to use.", "properties": { "voiceName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The name of the preset voice to use.", "title": "Voicename" } }, "title": "PrebuiltVoiceConfig", "type": "object" }, "ProactivityConfig": { "additionalProperties": false, "description": "Config for proactivity features.", "properties": { "proactiveAudio": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "If enabled, the model can reject responding to the last prompt. For\n example, this allows the model to ignore out of context speech or to stay\n silent if the user did not make a request, yet.", "title": "Proactiveaudio" } }, "title": "ProactivityConfig", "type": "object" }, "RagChunk": { "additionalProperties": false, "description": "A RagChunk includes the content of a chunk of a RagFile, and associated metadata.\n\nThis data type is not supported in Gemini API.", "properties": { "pageSpan": { "anyOf": [ { "$ref": "#/$defs/RagChunkPageSpan" }, { "type": "null" } ], "default": null, "description": "If populated, represents where the chunk starts and ends in the document." }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The content of the chunk.", "title": "Text" } }, "title": "RagChunk", "type": "object" }, "RagChunkPageSpan": { "additionalProperties": false, "description": "Represents where the chunk starts and ends in the document.\n\nThis data type is not supported in Gemini API.", "properties": { "firstPage": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Page where chunk starts in the document. Inclusive. 1-indexed.", "title": "Firstpage" }, "lastPage": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Page where chunk ends in the document. Inclusive. 1-indexed.", "title": "Lastpage" } }, "title": "RagChunkPageSpan", "type": "object" }, "RealtimeCacheEntry": { "additionalProperties": false, "description": "Store audio data chunks for caching before flushing.", "properties": { "role": { "title": "Role", "type": "string" }, "data": { "$ref": "#/$defs/Blob" }, "timestamp": { "title": "Timestamp", "type": "number" } }, "required": [ "role", "data", "timestamp" ], "title": "RealtimeCacheEntry", "type": "object" }, "RealtimeInputConfig": { "additionalProperties": false, "description": "Marks the end of user activity.\n\nThis can only be sent if automatic (i.e. server-side) activity detection is\ndisabled.", "properties": { "automaticActivityDetection": { "anyOf": [ { "$ref": "#/$defs/AutomaticActivityDetection" }, { "type": "null" } ], "default": null, "description": "If not set, automatic activity detection is enabled by default. If automatic voice detection is disabled, the client must send activity signals." }, "activityHandling": { "anyOf": [ { "$ref": "#/$defs/ActivityHandling" }, { "type": "null" } ], "default": null, "description": "Defines what effect activity has." }, "turnCoverage": { "anyOf": [ { "$ref": "#/$defs/TurnCoverage" }, { "type": "null" } ], "default": null, "description": "Defines which input is included in the user's turn." } }, "title": "RealtimeInputConfig", "type": "object" }, "ReplicatedVoiceConfig": { "additionalProperties": false, "description": "ReplicatedVoiceConfig is used to configure replicated voice.", "properties": { "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The mime type of the replicated voice.\n ", "title": "Mimetype" }, "voiceSampleAudio": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "The sample audio of the replicated voice.\n ", "title": "Voicesampleaudio" } }, "title": "ReplicatedVoiceConfig", "type": "object" }, "ResumabilityConfig": { "description": "The config of the resumability for an application.\n\nThe \"resumability\" in ADK refers to the ability to:\n1. pause an invocation upon a long running function call.\n2. resume an invocation from the last event, if it's paused or failed midway\nthrough.\n\nNote: ADK resumes the invocation in a best-effort manner:\n1. Tool call to resume needs to be idempotent because we only guarantee\nan at-least-once behavior once resumed.\n2. Any temporary / in-memory state will be lost upon resumption.", "properties": { "is_resumable": { "default": false, "title": "Is Resumable", "type": "boolean" } }, "title": "ResumabilityConfig", "type": "object" }, "RetrievalMetadata": { "additionalProperties": false, "description": "Metadata related to retrieval in the grounding flow.", "properties": { "googleSearchDynamicRetrievalScore": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. Score indicating how likely information from Google Search could help answer the prompt. The score is in the range `[0, 1]`, where 0 is the least likely and 1 is the most likely. This score is only populated when Google Search grounding and dynamic retrieval is enabled. It will be compared to the threshold to determine whether to trigger Google Search.", "title": "Googlesearchdynamicretrievalscore" } }, "title": "RetrievalMetadata", "type": "object" }, "RunConfig": { "additionalProperties": false, "description": "Configs for runtime behavior of agents.\n\nThe configs here will be overridden by agent-specific configurations.", "properties": { "speech_config": { "anyOf": [ { "$ref": "#/$defs/SpeechConfig" }, { "type": "null" } ], "default": null }, "response_modalities": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Response Modalities" }, "save_input_blobs_as_artifacts": { "default": false, "deprecated": true, "description": "Whether or not to save the input blobs as artifacts. DEPRECATED: Use SaveFilesAsArtifactsPlugin instead for better control and flexibility. See google.adk.plugins.SaveFilesAsArtifactsPlugin.", "title": "Save Input Blobs As Artifacts", "type": "boolean" }, "support_cfc": { "default": false, "title": "Support Cfc", "type": "boolean" }, "streaming_mode": { "$ref": "#/$defs/StreamingMode", "default": null }, "output_audio_transcription": { "anyOf": [ { "$ref": "#/$defs/AudioTranscriptionConfig" }, { "type": "null" } ] }, "input_audio_transcription": { "anyOf": [ { "$ref": "#/$defs/AudioTranscriptionConfig" }, { "type": "null" } ] }, "realtime_input_config": { "anyOf": [ { "$ref": "#/$defs/RealtimeInputConfig" }, { "type": "null" } ], "default": null }, "enable_affective_dialog": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Enable Affective Dialog" }, "proactivity": { "anyOf": [ { "$ref": "#/$defs/ProactivityConfig" }, { "type": "null" } ], "default": null }, "session_resumption": { "anyOf": [ { "$ref": "#/$defs/SessionResumptionConfig" }, { "type": "null" } ], "default": null }, "context_window_compression": { "anyOf": [ { "$ref": "#/$defs/ContextWindowCompressionConfig" }, { "type": "null" } ], "default": null }, "save_live_blob": { "default": false, "title": "Save Live Blob", "type": "boolean" }, "save_live_audio": { "default": false, "deprecated": true, "description": "DEPRECATED: Use save_live_blob instead. If set to True, it saves live video and audio data to session and artifact service.", "title": "Save Live Audio", "type": "boolean" }, "max_llm_calls": { "default": 500, "title": "Max Llm Calls", "type": "integer" }, "custom_metadata": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "title": "Custom Metadata" } }, "title": "RunConfig", "type": "object" }, "SearchEntryPoint": { "additionalProperties": false, "description": "Google search entry point.", "properties": { "renderedContent": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Web content snippet that can be embedded in a web page or an app webview.", "title": "Renderedcontent" }, "sdkBlob": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Base64 encoded JSON representing array of tuple.", "title": "Sdkblob" } }, "title": "SearchEntryPoint", "type": "object" }, "SecuritySchemeType": { "enum": [ "apiKey", "http", "oauth2", "openIdConnect" ], "title": "SecuritySchemeType", "type": "string" }, "Segment": { "additionalProperties": false, "description": "Segment of the content.", "properties": { "endIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. End index in the given Part, measured in bytes. Offset from the start of the Part, exclusive, starting at zero.", "title": "Endindex" }, "partIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. The index of a Part object within its parent Content object.", "title": "Partindex" }, "startIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. Start index in the given Part, measured in bytes. Offset from the start of the Part, inclusive, starting at zero.", "title": "Startindex" }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. The text corresponding to the segment from the response.", "title": "Text" } }, "title": "Segment", "type": "object" }, "ServiceAccount": { "additionalProperties": true, "description": "Represents Google Service Account configuration.", "properties": { "serviceAccountCredential": { "anyOf": [ { "$ref": "#/$defs/ServiceAccountCredential" }, { "type": "null" } ], "default": null }, "scopes": { "items": { "type": "string" }, "title": "Scopes", "type": "array" }, "useDefaultCredential": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": false, "title": "Usedefaultcredential" } }, "required": [ "scopes" ], "title": "ServiceAccount", "type": "object" }, "ServiceAccountCredential": { "additionalProperties": true, "description": "Represents Google Service Account configuration.\n\nAttributes:\n type: The type should be \"service_account\".\n project_id: The project ID.\n private_key_id: The ID of the private key.\n private_key: The private key.\n client_email: The client email.\n client_id: The client ID.\n auth_uri: The authorization URI.\n token_uri: The token URI.\n auth_provider_x509_cert_url: URL for auth provider's X.509 cert.\n client_x509_cert_url: URL for the client's X.509 cert.\n universe_domain: The universe domain.\n\nExample:\n\n config = ServiceAccountCredential(\n type_=\"service_account\",\n project_id=\"your_project_id\",\n private_key_id=\"your_private_key_id\",\n private_key=\"-----BEGIN PRIVATE KEY-----...\",\n client_email=\"...@....iam.gserviceaccount.com\",\n client_id=\"your_client_id\",\n auth_uri=\"https://accounts.google.com/o/oauth2/auth\",\n token_uri=\"https://oauth2.googleapis.com/token\",\n auth_provider_x509_cert_url=\"https://www.googleapis.com/oauth2/v1/certs\",\n client_x509_cert_url=\"https://www.googleapis.com/robot/v1/metadata/x509/...\",\n universe_domain=\"googleapis.com\"\n )\n\n\n config = ServiceAccountConfig.model_construct(**{\n ...service account config dict\n })", "properties": { "type": { "default": "", "title": "Type", "type": "string" }, "projectId": { "title": "Projectid", "type": "string" }, "privateKeyId": { "title": "Privatekeyid", "type": "string" }, "privateKey": { "title": "Privatekey", "type": "string" }, "clientEmail": { "title": "Clientemail", "type": "string" }, "clientId": { "title": "Clientid", "type": "string" }, "authUri": { "title": "Authuri", "type": "string" }, "tokenUri": { "title": "Tokenuri", "type": "string" }, "authProviderX509CertUrl": { "title": "Authproviderx509Certurl", "type": "string" }, "clientX509CertUrl": { "title": "Clientx509Certurl", "type": "string" }, "universeDomain": { "title": "Universedomain", "type": "string" } }, "required": [ "projectId", "privateKeyId", "privateKey", "clientEmail", "clientId", "authUri", "tokenUri", "authProviderX509CertUrl", "clientX509CertUrl", "universeDomain" ], "title": "ServiceAccountCredential", "type": "object" }, "Session": { "additionalProperties": false, "description": "Represents a series of interactions between a user and agents.", "properties": { "id": { "title": "Id", "type": "string" }, "appName": { "title": "Appname", "type": "string" }, "userId": { "title": "Userid", "type": "string" }, "state": { "additionalProperties": true, "title": "State", "type": "object" }, "events": { "items": { "$ref": "#/$defs/Event" }, "title": "Events", "type": "array" }, "lastUpdateTime": { "default": 0.0, "title": "Lastupdatetime", "type": "number" } }, "required": [ "id", "appName", "userId" ], "title": "Session", "type": "object" }, "SessionResumptionConfig": { "additionalProperties": false, "description": "Configuration of session resumption mechanism.\n\nIncluded in `LiveConnectConfig.session_resumption`. If included server\nwill send `LiveServerSessionResumptionUpdate` messages.", "properties": { "handle": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Session resumption handle of previous session (session to restore).\n\nIf not present new session will be started.", "title": "Handle" }, "transparent": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "If set the server will send `last_consumed_client_message_index` in the `session_resumption_update` messages to allow for transparent reconnections.", "title": "Transparent" } }, "title": "SessionResumptionConfig", "type": "object" }, "SlidingWindow": { "additionalProperties": false, "description": "Context window will be truncated by keeping only suffix of it.\n\nContext window will always be cut at start of USER role turn. System\ninstructions and `BidiGenerateContentSetup.prefix_turns` will not be\nsubject to the sliding window mechanism, they will always stay at the\nbeginning of context window.", "properties": { "targetTokens": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Session reduction target -- how many tokens we should keep. Window shortening operation has some latency costs, so we should avoid running it on every turn. Should be < trigger_tokens. If not set, trigger_tokens/2 is assumed.", "title": "Targettokens" } }, "title": "SlidingWindow", "type": "object" }, "SpeakerVoiceConfig": { "additionalProperties": false, "description": "Configuration for a single speaker in a multi speaker setup.", "properties": { "speaker": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The name of the speaker. This should be the same as the speaker name used in the prompt.", "title": "Speaker" }, "voiceConfig": { "anyOf": [ { "$ref": "#/$defs/VoiceConfig" }, { "type": "null" } ], "default": null, "description": "Required. The configuration for the voice of this speaker." } }, "title": "SpeakerVoiceConfig", "type": "object" }, "SpeechConfig": { "additionalProperties": false, "properties": { "voiceConfig": { "anyOf": [ { "$ref": "#/$defs/VoiceConfig" }, { "type": "null" } ], "default": null, "description": "Configuration for the voice of the response." }, "languageCode": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Language code (ISO 639. e.g. en-US) for the speech synthesization.", "title": "Languagecode" }, "multiSpeakerVoiceConfig": { "anyOf": [ { "$ref": "#/$defs/MultiSpeakerVoiceConfig" }, { "type": "null" } ], "default": null, "description": "The configuration for a multi-speaker text-to-speech request. This field is mutually exclusive with `voice_config`." } }, "title": "SpeechConfig", "type": "object" }, "StartSensitivity": { "description": "Start of speech sensitivity.", "enum": [ "START_SENSITIVITY_UNSPECIFIED", "START_SENSITIVITY_HIGH", "START_SENSITIVITY_LOW" ], "title": "StartSensitivity", "type": "string" }, "StreamingMode": { "description": "Streaming modes for agent execution.\n\nThis enum defines different streaming behaviors for how the agent returns\nevents as model response.", "enum": [ null, "sse", "bidi" ], "title": "StreamingMode" }, "ToolConfirmation": { "additionalProperties": false, "description": "Represents a tool confirmation configuration.", "properties": { "hint": { "default": "", "title": "Hint", "type": "string" }, "confirmed": { "default": false, "title": "Confirmed", "type": "boolean" }, "payload": { "anyOf": [ {}, { "type": "null" } ], "default": null, "title": "Payload" } }, "title": "ToolConfirmation", "type": "object" }, "TrafficType": { "description": "Output only.\n\nThe traffic type for this request. This enum is not supported in Gemini API.", "enum": [ "TRAFFIC_TYPE_UNSPECIFIED", "ON_DEMAND", "PROVISIONED_THROUGHPUT" ], "title": "TrafficType", "type": "string" }, "Transcription": { "additionalProperties": false, "description": "Audio transcription in Server Conent.", "properties": { "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Transcription text.\n ", "title": "Text" }, "finished": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "The bool indicates the end of the transcription.\n ", "title": "Finished" } }, "title": "Transcription", "type": "object" }, "TranscriptionEntry": { "additionalProperties": false, "description": "Store the data that can be used for transcription.", "properties": { "role": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Role" }, "data": { "anyOf": [ { "$ref": "#/$defs/Blob" }, { "$ref": "#/$defs/Content" } ], "title": "Data" } }, "required": [ "data" ], "title": "TranscriptionEntry", "type": "object" }, "TurnCoverage": { "description": "Options about which input is included in the user's turn.", "enum": [ "TURN_COVERAGE_UNSPECIFIED", "TURN_INCLUDES_ONLY_ACTIVITY", "TURN_INCLUDES_ALL_INPUT" ], "title": "TurnCoverage", "type": "string" }, "VideoMetadata": { "additionalProperties": false, "description": "Metadata describes the input video content.", "properties": { "endOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The end offset of the video.", "title": "Endoffset" }, "fps": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. The frame rate of the video sent to the model. If not specified, the default value will be 1.0. The fps range is (0.0, 24.0].", "title": "Fps" }, "startOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The start offset of the video.", "title": "Startoffset" } }, "title": "VideoMetadata", "type": "object" }, "VoiceConfig": { "additionalProperties": false, "properties": { "replicatedVoiceConfig": { "anyOf": [ { "$ref": "#/$defs/ReplicatedVoiceConfig" }, { "type": "null" } ], "default": null, "description": "If true, the model will use a replicated voice for the response." }, "prebuiltVoiceConfig": { "anyOf": [ { "$ref": "#/$defs/PrebuiltVoiceConfig" }, { "type": "null" } ], "default": null, "description": "The configuration for the prebuilt voice to use." } }, "title": "VoiceConfig", "type": "object" } }, "additionalProperties": false, "required": [ "invocation_id", "agent", "session" ] }

- Fields:
`active_streaming_tools (dict[str, google.adk.agents.active_streaming_tool.ActiveStreamingTool] | None)`

`agent (google.adk.agents.base_agent.BaseAgent)`

`agent_states (dict[str, dict[str, Any]])`

`artifact_service (google.adk.artifacts.base_artifact_service.BaseArtifactService | None)`

`branch (str | None)`

`canonical_tools_cache (list[google.adk.tools.base_tool.BaseTool] | None)`

`context_cache_config (google.adk.agents.context_cache_config.ContextCacheConfig | None)`

`credential_service (google.adk.auth.credential_service.base_credential_service.BaseCredentialService | None)`

`end_invocation (bool)`

`end_of_agents (dict[str, bool])`

`input_realtime_cache (list[google.adk.agents.invocation_context.RealtimeCacheEntry] | None)`

`invocation_id (str)`

`live_request_queue (google.adk.agents.live_request_queue.LiveRequestQueue | None)`

`live_session_resumption_handle (str | None)`

`memory_service (google.adk.memory.base_memory_service.BaseMemoryService | None)`

`output_realtime_cache (list[google.adk.agents.invocation_context.RealtimeCacheEntry] | None)`

`plugin_manager (google.adk.plugins.plugin_manager.PluginManager)`

`resumability_config (google.adk.apps.app.ResumabilityConfig | None)`

`run_config (google.adk.agents.run_config.RunConfig | None)`

`session (google.adk.sessions.session.Session)`

`session_service (google.adk.sessions.base_session_service.BaseSessionService)`

`transcription_cache (list[google.adk.agents.transcription_entry.TranscriptionEntry] | None)`

`user_content (google.genai.types.Content | None)`


-
*field*active_streaming_tools*: dict[str, ActiveStreamingTool] | None**= None*[¶](#google.adk.agents.InvocationContext.active_streaming_tools) The running streaming tools of this invocation.


-
*field*agent_states*: dict[str, dict[str, Any]]**[Optional]*[¶](#google.adk.agents.InvocationContext.agent_states) The state of the agent for this invocation.


-
*field*artifact_service*:*[BaseArtifactService](#google.adk.artifacts.BaseArtifactService)| None*= None*[¶](#google.adk.agents.InvocationContext.artifact_service)

-
*field*branch*: str | None**= None*[¶](#google.adk.agents.InvocationContext.branch) The branch of the invocation context.

The format is like agent_1.agent_2.agent_3, where agent_1 is the parent of agent_2, and agent_2 is the parent of agent_3.

Branch is used when multiple sub-agents shouldn’t see their peer agents’ conversation history.


-
*field*canonical_tools_cache*: list[*[BaseTool](#google.adk.tools.BaseTool)] | None*= None*[¶](#google.adk.agents.InvocationContext.canonical_tools_cache) The cache of canonical tools for this invocation.


-
*field*context_cache_config*: ContextCacheConfig | None**= None*[¶](#google.adk.agents.InvocationContext.context_cache_config)

-
*field*credential_service*: BaseCredentialService | None**= None*[¶](#google.adk.agents.InvocationContext.credential_service)

-
*field*end_invocation*: bool**= False*[¶](#google.adk.agents.InvocationContext.end_invocation) Whether to end this invocation.

Set to True in callbacks or tools to terminate this invocation.


-
*field*end_of_agents*: dict[str, bool]**[Optional]*[¶](#google.adk.agents.InvocationContext.end_of_agents) The end of agent status for each agent in this invocation.


-
*field*input_realtime_cache*: list[RealtimeCacheEntry] | None**= None*[¶](#google.adk.agents.InvocationContext.input_realtime_cache) Caches input audio chunks before flushing to session and artifact services.


-
*field*invocation_id*: str**[Required]*[¶](#google.adk.agents.InvocationContext.invocation_id) The id of this invocation context. Readonly.


-
*field*live_request_queue*:*[LiveRequestQueue](#google.adk.agents.LiveRequestQueue)| None*= None*[¶](#google.adk.agents.InvocationContext.live_request_queue) The queue to receive live requests.


-
*field*live_session_resumption_handle*: str | None**= None*[¶](#google.adk.agents.InvocationContext.live_session_resumption_handle) The handle for live session resumption.


-
*field*memory_service*:*[BaseMemoryService](#google.adk.memory.BaseMemoryService)| None*= None*[¶](#google.adk.agents.InvocationContext.memory_service)

-
*field*output_realtime_cache*: list[RealtimeCacheEntry] | None**= None*[¶](#google.adk.agents.InvocationContext.output_realtime_cache) Caches output audio chunks before flushing to session and artifact services.


-
*field*plugin_manager*:*[PluginManager](#google.adk.plugins.PluginManager)*[Optional]*[¶](#google.adk.agents.InvocationContext.plugin_manager) The manager for keeping track of plugins in this invocation.


-
*field*resumability_config*:*[ResumabilityConfig](#google.adk.apps.ResumabilityConfig)| None*= None*[¶](#google.adk.agents.InvocationContext.resumability_config) The resumability config that applies to all agents under this invocation.


-
*field*session_service*:*[BaseSessionService](#google.adk.sessions.BaseSessionService)*[Required]*[¶](#google.adk.agents.InvocationContext.session_service)

-
*field*transcription_cache*: list[TranscriptionEntry] | None**= None*[¶](#google.adk.agents.InvocationContext.transcription_cache) Caches necessary data, audio or contents, that are needed by transcription.


-
*field*user_content*: types.Content | None**= None*[¶](#google.adk.agents.InvocationContext.user_content) The user content that started this invocation. Readonly.


-
increment_llm_call_count()
[¶](#google.adk.agents.InvocationContext.increment_llm_call_count) Tracks number of llm calls made.

- Raises:
**LlmCallsLimitExceededError**– If number of llm calls made exceed the set threshold.


-
model_post_init(
*context*,*/*)[¶](#google.adk.agents.InvocationContext.model_post_init) This function is meant to behave like a BaseModel method to initialise private attributes.

It takes context as an argument since that’s what pydantic-core passes when calling it.

- Return type:
`None`

- Parameters:
**self**– The BaseModel instance.**context**– The context.


-
populate_invocation_agent_states()
[¶](#google.adk.agents.InvocationContext.populate_invocation_agent_states) Populates agent states for the current invocation if it is resumable.

For history events that contain agent state information, set the agent_state and end_of_agent of the agent that generated the event.

For non-workflow agents, also set an initial agent_state if it has already generated some contents.

- Return type:
`None`


-
reset_sub_agent_states(
*agent_name*)[¶](#google.adk.agents.InvocationContext.reset_sub_agent_states) Resets the state of all sub-agents of the given agent in this invocation.

- Return type:
`None`

- Parameters:
**agent_name**– The name of the agent whose sub-agent states need to be reset.


-
set_agent_state(
*agent_name*,***,*agent_state=None*,*end_of_agent=False*)[¶](#google.adk.agents.InvocationContext.set_agent_state) Sets the state of an agent in this invocation.

If end_of_agent is True, will set the end_of_agent flag to True and clear the agent_state.

Otherwise, if agent_state is not None, will set the agent_state and reset the end_of_agent flag to False.

Otherwise, will clear the agent_state and end_of_agent flag, to allow the agent to re-run.


- Parameters:
**agent_name**– The name of the agent.**agent_state**– The state of the agent. Will be ignored if end_of_agent is True.**end_of_agent**– Whether the agent has finished running.

- Return type:
`None`


-
should_pause_invocation(
*event*)[¶](#google.adk.agents.InvocationContext.should_pause_invocation) Returns whether to pause the invocation right after this event.

“Pausing” an invocation is different from “ending” an invocation. A paused invocation can be resumed later, while an ended invocation cannot.

Pausing the current agent’s run will also pause all the agents that depend on its execution, i.e. the subsequent agents in a workflow, and the current agent’s ancestors, etc.

Note that parallel sibling agents won’t be affected, but their common ancestors will be paused after all the non-blocking sub-agents finished running.

- Return type:
`bool`


- Should meet all following conditions to pause an invocation:
The app is resumable.

The current event has a long running function call.


- Parameters:
**event**– The current event.- Returns:
Whether to pause the invocation right after this event.


-
*property*app_name*: str*[¶](#google.adk.agents.InvocationContext.app_name)

-
*property*is_resumable*: bool*[¶](#google.adk.agents.InvocationContext.is_resumable) Returns whether the current invocation is resumable.


-
*property*user_id*: str*[¶](#google.adk.agents.InvocationContext.user_id)


-
*pydantic model*google.adk.agents.LiveRequest[¶](#google.adk.agents.LiveRequest) Bases:

`BaseModel`

Request send to live agents.

## Show JSON schema

{ "title": "LiveRequest", "description": "Request send to live agents.", "type": "object", "properties": { "content": { "anyOf": [ { "$ref": "#/$defs/Content" }, { "type": "null" } ], "default": null }, "blob": { "anyOf": [ { "$ref": "#/$defs/Blob" }, { "type": "null" } ], "default": null }, "activity_start": { "anyOf": [ { "$ref": "#/$defs/ActivityStart" }, { "type": "null" } ], "default": null }, "activity_end": { "anyOf": [ { "$ref": "#/$defs/ActivityEnd" }, { "type": "null" } ], "default": null }, "close": { "default": false, "title": "Close", "type": "boolean" } }, "$defs": { "ActivityEnd": { "additionalProperties": false, "description": "Marks the end of user activity.\n\nThis can only be sent if automatic (i.e. server-side) activity detection is\ndisabled.", "properties": {}, "title": "ActivityEnd", "type": "object" }, "ActivityStart": { "additionalProperties": false, "description": "Marks the start of user activity.\n\nThis can only be sent if automatic (i.e. server-side) activity detection is\ndisabled.", "properties": {}, "title": "ActivityStart", "type": "object" }, "Blob": { "additionalProperties": false, "description": "Content blob.", "properties": { "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Raw bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob. Used to provide a label or filename to distinguish blobs. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "Blob", "type": "object" }, "CodeExecutionResult": { "additionalProperties": false, "description": "Result of executing the [ExecutableCode].\n\nOnly generated when using the [CodeExecution] tool, and always follows a\n`part` containing the [ExecutableCode].", "properties": { "outcome": { "anyOf": [ { "$ref": "#/$defs/Outcome" }, { "type": "null" } ], "default": null, "description": "Required. Outcome of the code execution." }, "output": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Contains stdout when code execution is successful, stderr or other description otherwise.", "title": "Output" } }, "title": "CodeExecutionResult", "type": "object" }, "Content": { "additionalProperties": false, "description": "Contains the multi-part content of a message.", "properties": { "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/Part" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a single message. Each part may have\n a different IANA MIME type.", "title": "Parts" }, "role": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The producer of the content. Must be either 'user' or 'model'. Useful to set for multi-turn conversations, otherwise can be left blank or unset.", "title": "Role" } }, "title": "Content", "type": "object" }, "ExecutableCode": { "additionalProperties": false, "description": "Code generated by the model that is meant to be executed, and the result returned to the model.\n\nGenerated when using the [CodeExecution] tool, in which the code will be\nautomatically executed, and a corresponding [CodeExecutionResult] will also be\ngenerated.", "properties": { "code": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The code to be executed.", "title": "Code" }, "language": { "anyOf": [ { "$ref": "#/$defs/Language" }, { "type": "null" } ], "default": null, "description": "Required. Programming language of the `code`." } }, "title": "ExecutableCode", "type": "object" }, "FileData": { "additionalProperties": false, "description": "URI based data.", "properties": { "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file data. Used to provide a label or filename to distinguish file datas. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "FileData", "type": "object" }, "FunctionCall": { "additionalProperties": false, "description": "A function call.", "properties": { "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The unique id of the function call. If populated, the client to execute the\n `function_call` and return the response with the matching `id`.", "title": "Id" }, "args": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Optional. The function parameters and values in JSON object format. See [FunctionDeclaration.parameters] for parameter details.", "title": "Args" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The name of the function to call. Matches [FunctionDeclaration.name].", "title": "Name" }, "partialArgs": { "anyOf": [ { "items": { "$ref": "#/$defs/PartialArg" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. The partial argument value of the function call. If provided, represents the arguments/fields that are streamed incrementally. This field is not supported in Gemini API.", "title": "Partialargs" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is the last part of the FunctionCall. If true, another partial message for the current FunctionCall is expected to follow. This field is not supported in Gemini API.", "title": "Willcontinue" } }, "title": "FunctionCall", "type": "object" }, "FunctionResponse": { "additionalProperties": false, "description": "A function response.", "properties": { "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Signals that function call continues, and more responses will be returned, turning the function call into a generator. Is only applicable to NON_BLOCKING function calls (see FunctionDeclaration.behavior for details), ignored otherwise. If false, the default, future responses will not be considered. Is only applicable to NON_BLOCKING function calls, is ignored otherwise. If set to false, future responses will not be considered. It is allowed to return empty `response` with `will_continue=False` to signal that the function call is finished.", "title": "Willcontinue" }, "scheduling": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseScheduling" }, { "type": "null" } ], "default": null, "description": "Specifies how the response should be scheduled in the conversation. Only applicable to NON_BLOCKING function calls, is ignored otherwise. Defaults to WHEN_IDLE." }, "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/FunctionResponsePart" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a function response. Each part may\n have a different IANA MIME type.", "title": "Parts" }, "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The id of the function call this response is for. Populated by the client to match the corresponding function call `id`.", "title": "Id" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The name of the function to call. Matches [FunctionDeclaration.name] and [FunctionCall.name].", "title": "Name" }, "response": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Required. The function response in JSON object format. Use \"output\" key to specify function output and \"error\" key to specify error details (if any). If \"output\" and \"error\" keys are not specified, then whole \"response\" is treated as function output.", "title": "Response" } }, "title": "FunctionResponse", "type": "object" }, "FunctionResponseBlob": { "additionalProperties": false, "description": "Raw media bytes for function response.\n\nText should not be sent as raw bytes, use the FunctionResponse.response\nfield.", "properties": { "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Inline media bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob.\n Used to provide a label or filename to distinguish blobs.", "title": "Displayname" } }, "title": "FunctionResponseBlob", "type": "object" }, "FunctionResponseFileData": { "additionalProperties": false, "description": "URI based data for function response.", "properties": { "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file.\n Used to provide a label or filename to distinguish files.", "title": "Displayname" } }, "title": "FunctionResponseFileData", "type": "object" }, "FunctionResponsePart": { "additionalProperties": false, "description": "A datatype containing media that is part of a `FunctionResponse` message.\n\nA `FunctionResponsePart` consists of data which has an associated datatype. A\n`FunctionResponsePart` can only contain one of the accepted types in\n`FunctionResponsePart.data`.\n\nA `FunctionResponsePart` must have a fixed IANA MIME type identifying the\ntype and subtype of the media if the `inline_data` field is filled with raw\nbytes.", "properties": { "inlineData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseBlob" }, { "type": "null" } ], "default": null, "description": "Optional. Inline media bytes." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseFileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." } }, "title": "FunctionResponsePart", "type": "object" }, "FunctionResponseScheduling": { "description": "Specifies how the response should be scheduled in the conversation.", "enum": [ "SCHEDULING_UNSPECIFIED", "SILENT", "WHEN_IDLE", "INTERRUPT" ], "title": "FunctionResponseScheduling", "type": "string" }, "Language": { "description": "Programming language of the `code`.", "enum": [ "LANGUAGE_UNSPECIFIED", "PYTHON" ], "title": "Language", "type": "string" }, "Outcome": { "description": "Outcome of the code execution.", "enum": [ "OUTCOME_UNSPECIFIED", "OUTCOME_OK", "OUTCOME_FAILED", "OUTCOME_DEADLINE_EXCEEDED" ], "title": "Outcome", "type": "string" }, "Part": { "additionalProperties": false, "description": "A datatype containing media content.\n\nExactly one field within a Part should be set, representing the specific type\nof content being conveyed. Using multiple fields within the same `Part`\ninstance is considered invalid.", "properties": { "mediaResolution": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolution" }, { "type": "null" } ], "default": null, "description": "Media resolution for the input media.\n " }, "codeExecutionResult": { "anyOf": [ { "$ref": "#/$defs/CodeExecutionResult" }, { "type": "null" } ], "default": null, "description": "Optional. Result of executing the [ExecutableCode]." }, "executableCode": { "anyOf": [ { "$ref": "#/$defs/ExecutableCode" }, { "type": "null" } ], "default": null, "description": "Optional. Code generated by the model that is meant to be executed." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." }, "functionCall": { "anyOf": [ { "$ref": "#/$defs/FunctionCall" }, { "type": "null" } ], "default": null, "description": "Optional. A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] with the parameters and their values." }, "functionResponse": { "anyOf": [ { "$ref": "#/$defs/FunctionResponse" }, { "type": "null" } ], "default": null, "description": "Optional. The result output of a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function call. It is used as context to the model." }, "inlineData": { "anyOf": [ { "$ref": "#/$defs/Blob" }, { "type": "null" } ], "default": null, "description": "Optional. Inlined bytes data." }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Text part (can be code).", "title": "Text" }, "thought": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Indicates if the part is thought from the model.", "title": "Thought" }, "thoughtSignature": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. An opaque signature for the thought so it can be reused in subsequent requests.", "title": "Thoughtsignature" }, "videoMetadata": { "anyOf": [ { "$ref": "#/$defs/VideoMetadata" }, { "type": "null" } ], "default": null, "description": "Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data." } }, "title": "Part", "type": "object" }, "PartMediaResolution": { "additionalProperties": false, "description": "Media resolution for the input media.", "properties": { "level": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolutionLevel" }, { "type": "null" } ], "default": null, "description": "The tokenization quality used for given media.\n " }, "numTokens": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Specifies the required sequence length for media tokenization.\n ", "title": "Numtokens" } }, "title": "PartMediaResolution", "type": "object" }, "PartMediaResolutionLevel": { "description": "The tokenization quality used for given media.", "enum": [ "MEDIA_RESOLUTION_UNSPECIFIED", "MEDIA_RESOLUTION_LOW", "MEDIA_RESOLUTION_MEDIUM", "MEDIA_RESOLUTION_HIGH", "MEDIA_RESOLUTION_ULTRA_HIGH" ], "title": "PartMediaResolutionLevel", "type": "string" }, "PartialArg": { "additionalProperties": false, "description": "Partial argument value of the function call.\n\nThis data type is not supported in Gemini API.", "properties": { "nullValue": { "anyOf": [ { "const": "NULL_VALUE", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a null value.", "title": "Nullvalue" }, "numberValue": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a double value.", "title": "Numbervalue" }, "stringValue": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a string value.", "title": "Stringvalue" }, "boolValue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a boolean value.", "title": "Boolvalue" }, "jsonPath": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. A JSON Path (RFC 9535) to the argument being streamed. https://datatracker.ietf.org/doc/html/rfc9535. e.g. \"$.foo.bar[0].data\".", "title": "Jsonpath" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is not the last part of the same json_path. If true, another PartialArg message for the current json_path is expected to follow.", "title": "Willcontinue" } }, "title": "PartialArg", "type": "object" }, "VideoMetadata": { "additionalProperties": false, "description": "Metadata describes the input video content.", "properties": { "endOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The end offset of the video.", "title": "Endoffset" }, "fps": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. The frame rate of the video sent to the model. If not specified, the default value will be 1.0. The fps range is (0.0, 24.0].", "title": "Fps" }, "startOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The start offset of the video.", "title": "Startoffset" } }, "title": "VideoMetadata", "type": "object" } } }

- Fields:
`activity_end (google.genai.types.ActivityEnd | None)`

`activity_start (google.genai.types.ActivityStart | None)`

`blob (google.genai.types.Blob | None)`

`close (bool)`

`content (google.genai.types.Content | None)`


-
*field*activity_end*: types.ActivityEnd | None**= None*[¶](#google.adk.agents.LiveRequest.activity_end) If set, signal the end of user activity to the model.


-
*field*activity_start*: types.ActivityStart | None**= None*[¶](#google.adk.agents.LiveRequest.activity_start) If set, signal the start of user activity to the model.


-
*field*blob*: types.Blob | None**= None*[¶](#google.adk.agents.LiveRequest.blob) If set, send the blob to the model in realtime mode.


-
*field*close*: bool**= False*[¶](#google.adk.agents.LiveRequest.close) If set, close the queue. queue.shutdown() is only supported in Python 3.13+.


-
*field*content*: types.Content | None**= None*[¶](#google.adk.agents.LiveRequest.content) If set, send the content to the model in turn-by-turn mode.


-
*class*google.adk.agents.LiveRequestQueue[¶](#google.adk.agents.LiveRequestQueue) Bases:

`object`

Queue used to send LiveRequest in a live(bidirectional streaming) way.

-
close()
[¶](#google.adk.agents.LiveRequestQueue.close)

-
*async*get()[¶](#google.adk.agents.LiveRequestQueue.get) - Return type:


-
send(
*req*)[¶](#google.adk.agents.LiveRequestQueue.send)

-
send_activity_end()
[¶](#google.adk.agents.LiveRequestQueue.send_activity_end) Sends an activity end signal to mark the end of user input.


-
send_activity_start()
[¶](#google.adk.agents.LiveRequestQueue.send_activity_start) Sends an activity start signal to mark the beginning of user input.


-
send_content(
*content*)[¶](#google.adk.agents.LiveRequestQueue.send_content)

-
send_realtime(
*blob*)[¶](#google.adk.agents.LiveRequestQueue.send_realtime)

-
close()

-
*pydantic model*google.adk.agents.LlmAgent[¶](#google.adk.agents.LlmAgent) Bases:

`BaseAgent`

LLM-based Agent.

## Show JSON schema

{ "title": "LlmAgent", "type": "object", "properties": { "name": { "title": "Name", "type": "string" }, "description": { "default": "", "title": "Description", "type": "string" }, "parent_agent": { "anyOf": [ { "$ref": "#/$defs/BaseAgent" }, { "type": "null" } ], "default": null }, "sub_agents": { "items": { "$ref": "#/$defs/BaseAgent" }, "title": "Sub Agents", "type": "array" }, "before_agent_callback": { "default": null, "title": "Before Agent Callback", "type": "null" }, "after_agent_callback": { "default": null, "title": "After Agent Callback", "type": "null" }, "model": { "anyOf": [ { "type": "string" }, { "$ref": "#/$defs/BaseLlm" } ], "default": "", "title": "Model" }, "instruction": { "default": "", "title": "Instruction", "type": "string" }, "global_instruction": { "default": "", "title": "Global Instruction", "type": "string" }, "static_instruction": { "anyOf": [ { "$ref": "#/$defs/Content" }, { "type": "string" }, { "$ref": "#/$defs/File" }, { "$ref": "#/$defs/Part" }, { "items": { "anyOf": [ { "type": "string" }, { "$ref": "#/$defs/File" }, { "$ref": "#/$defs/Part" } ] }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Static Instruction" }, "tools": { "items": { "anyOf": [] }, "title": "Tools", "type": "array" }, "generate_content_config": { "default": null, "title": "Generate Content Config" }, "disallow_transfer_to_parent": { "default": false, "title": "Disallow Transfer To Parent", "type": "boolean" }, "disallow_transfer_to_peers": { "default": false, "title": "Disallow Transfer To Peers", "type": "boolean" }, "include_contents": { "default": "default", "enum": [ "default", "none" ], "title": "Include Contents", "type": "string" }, "input_schema": { "anyOf": [ {}, { "type": "null" } ], "default": null, "title": "Input Schema" }, "output_schema": { "anyOf": [ {}, { "type": "null" } ], "default": null, "title": "Output Schema" }, "output_key": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Output Key" }, "planner": { "default": null, "title": "Planner" }, "code_executor": { "anyOf": [ { "$ref": "#/$defs/BaseCodeExecutor" }, { "type": "null" } ], "default": null }, "before_model_callback": { "default": null, "title": "Before Model Callback", "type": "null" }, "after_model_callback": { "default": null, "title": "After Model Callback", "type": "null" }, "on_model_error_callback": { "default": null, "title": "On Model Error Callback", "type": "null" }, "before_tool_callback": { "default": null, "title": "Before Tool Callback", "type": "null" }, "after_tool_callback": { "default": null, "title": "After Tool Callback", "type": "null" }, "on_tool_error_callback": { "default": null, "title": "On Tool Error Callback", "type": "null" } }, "$defs": { "BaseAgent": { "additionalProperties": false, "description": "Base class for all agents in Agent Development Kit.", "properties": { "name": { "title": "Name", "type": "string" }, "description": { "default": "", "title": "Description", "type": "string" }, "parent_agent": { "anyOf": [ { "$ref": "#/$defs/BaseAgent" }, { "type": "null" } ], "default": null }, "sub_agents": { "items": { "$ref": "#/$defs/BaseAgent" }, "title": "Sub Agents", "type": "array" }, "before_agent_callback": { "default": null, "title": "Before Agent Callback", "type": "null" }, "after_agent_callback": { "default": null, "title": "After Agent Callback", "type": "null" } }, "required": [ "name" ], "title": "BaseAgent", "type": "object" }, "BaseCodeExecutor": { "description": "Abstract base class for all code executors.\n\nThe code executor allows the agent to execute code blocks from model responses\nand incorporate the execution results into the final response.\n\nAttributes:\n optimize_data_file: If true, extract and process data files from the model\n request and attach them to the code executor. Supported data file\n MimeTypes are [text/csv]. Default to False.\n stateful: Whether the code executor is stateful. Default to False.\n error_retry_attempts: The number of attempts to retry on consecutive code\n execution errors. Default to 2.\n code_block_delimiters: The list of the enclosing delimiters to identify the\n code blocks.\n execution_result_delimiters: The delimiters to format the code execution\n result.", "properties": { "optimize_data_file": { "default": false, "title": "Optimize Data File", "type": "boolean" }, "stateful": { "default": false, "title": "Stateful", "type": "boolean" }, "error_retry_attempts": { "default": 2, "title": "Error Retry Attempts", "type": "integer" }, "code_block_delimiters": { "default": [ [ "```tool_code\n", "\n```" ], [ "```python\n", "\n```" ] ], "items": { "maxItems": 2, "minItems": 2, "prefixItems": [ { "type": "string" }, { "type": "string" } ], "type": "array" }, "title": "Code Block Delimiters", "type": "array" }, "execution_result_delimiters": { "default": [ "```tool_output\n", "\n```" ], "maxItems": 2, "minItems": 2, "prefixItems": [ { "type": "string" }, { "type": "string" } ], "title": "Execution Result Delimiters", "type": "array" } }, "title": "BaseCodeExecutor", "type": "object" }, "BaseLlm": { "description": "The BaseLLM class.", "properties": { "model": { "title": "Model", "type": "string" } }, "required": [ "model" ], "title": "BaseLlm", "type": "object" }, "Blob": { "additionalProperties": false, "description": "Content blob.", "properties": { "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Raw bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob. Used to provide a label or filename to distinguish blobs. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "Blob", "type": "object" }, "CodeExecutionResult": { "additionalProperties": false, "description": "Result of executing the [ExecutableCode].\n\nOnly generated when using the [CodeExecution] tool, and always follows a\n`part` containing the [ExecutableCode].", "properties": { "outcome": { "anyOf": [ { "$ref": "#/$defs/Outcome" }, { "type": "null" } ], "default": null, "description": "Required. Outcome of the code execution." }, "output": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Contains stdout when code execution is successful, stderr or other description otherwise.", "title": "Output" } }, "title": "CodeExecutionResult", "type": "object" }, "Content": { "additionalProperties": false, "description": "Contains the multi-part content of a message.", "properties": { "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/Part" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a single message. Each part may have\n a different IANA MIME type.", "title": "Parts" }, "role": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The producer of the content. Must be either 'user' or 'model'. Useful to set for multi-turn conversations, otherwise can be left blank or unset.", "title": "Role" } }, "title": "Content", "type": "object" }, "ExecutableCode": { "additionalProperties": false, "description": "Code generated by the model that is meant to be executed, and the result returned to the model.\n\nGenerated when using the [CodeExecution] tool, in which the code will be\nautomatically executed, and a corresponding [CodeExecutionResult] will also be\ngenerated.", "properties": { "code": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The code to be executed.", "title": "Code" }, "language": { "anyOf": [ { "$ref": "#/$defs/Language" }, { "type": "null" } ], "default": null, "description": "Required. Programming language of the `code`." } }, "title": "ExecutableCode", "type": "object" }, "File": { "additionalProperties": false, "description": "A file uploaded to the API.", "properties": { "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The `File` resource name. The ID (name excluding the \"files/\" prefix) can contain up to 40 characters that are lowercase alphanumeric or dashes (-). The ID cannot start or end with a dash. If the name is empty on create, a unique name will be generated. Example: `files/123-456`", "title": "Name" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The human-readable display name for the `File`. The display name must be no more than 512 characters in length, including spaces. Example: 'Welcome Image'", "title": "Displayname" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. MIME type of the file.", "title": "Mimetype" }, "sizeBytes": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. Size of the file in bytes.", "title": "Sizebytes" }, "createTime": { "anyOf": [ { "format": "date-time", "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. The timestamp of when the `File` was created.", "title": "Createtime" }, "expirationTime": { "anyOf": [ { "format": "date-time", "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. The timestamp of when the `File` will be deleted. Only set if the `File` is scheduled to expire.", "title": "Expirationtime" }, "updateTime": { "anyOf": [ { "format": "date-time", "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. The timestamp of when the `File` was last updated.", "title": "Updatetime" }, "sha256Hash": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. SHA-256 hash of the uploaded bytes. The hash value is encoded in base64 format.", "title": "Sha256Hash" }, "uri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. The URI of the `File`.", "title": "Uri" }, "downloadUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. The URI of the `File`, only set for downloadable (generated) files.", "title": "Downloaduri" }, "state": { "anyOf": [ { "$ref": "#/$defs/FileState" }, { "type": "null" } ], "default": null, "description": "Output only. Processing state of the File." }, "source": { "anyOf": [ { "$ref": "#/$defs/FileSource" }, { "type": "null" } ], "default": null, "description": "Output only. The source of the `File`." }, "videoMetadata": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Output only. Metadata for a video.", "title": "Videometadata" }, "error": { "anyOf": [ { "$ref": "#/$defs/FileStatus" }, { "type": "null" } ], "default": null, "description": "Output only. Error status if File processing failed." } }, "title": "File", "type": "object" }, "FileData": { "additionalProperties": false, "description": "URI based data.", "properties": { "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file data. Used to provide a label or filename to distinguish file datas. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "FileData", "type": "object" }, "FileSource": { "description": "Source of the File.", "enum": [ "SOURCE_UNSPECIFIED", "UPLOADED", "GENERATED", "REGISTERED" ], "title": "FileSource", "type": "string" }, "FileState": { "description": "State for the lifecycle of a File.", "enum": [ "STATE_UNSPECIFIED", "PROCESSING", "ACTIVE", "FAILED" ], "title": "FileState", "type": "string" }, "FileStatus": { "additionalProperties": false, "description": "Status of a File that uses a common error model.", "properties": { "details": { "anyOf": [ { "items": { "additionalProperties": true, "type": "object" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "A list of messages that carry the error details. There is a common set of message types for APIs to use.", "title": "Details" }, "message": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A list of messages that carry the error details. There is a common set of message types for APIs to use.", "title": "Message" }, "code": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "The status code. 0 for OK, 1 for CANCELLED", "title": "Code" } }, "title": "FileStatus", "type": "object" }, "FunctionCall": { "additionalProperties": false, "description": "A function call.", "properties": { "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The unique id of the function call. If populated, the client to execute the\n `function_call` and return the response with the matching `id`.", "title": "Id" }, "args": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Optional. The function parameters and values in JSON object format. See [FunctionDeclaration.parameters] for parameter details.", "title": "Args" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The name of the function to call. Matches [FunctionDeclaration.name].", "title": "Name" }, "partialArgs": { "anyOf": [ { "items": { "$ref": "#/$defs/PartialArg" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. The partial argument value of the function call. If provided, represents the arguments/fields that are streamed incrementally. This field is not supported in Gemini API.", "title": "Partialargs" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is the last part of the FunctionCall. If true, another partial message for the current FunctionCall is expected to follow. This field is not supported in Gemini API.", "title": "Willcontinue" } }, "title": "FunctionCall", "type": "object" }, "FunctionResponse": { "additionalProperties": false, "description": "A function response.", "properties": { "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Signals that function call continues, and more responses will be returned, turning the function call into a generator. Is only applicable to NON_BLOCKING function calls (see FunctionDeclaration.behavior for details), ignored otherwise. If false, the default, future responses will not be considered. Is only applicable to NON_BLOCKING function calls, is ignored otherwise. If set to false, future responses will not be considered. It is allowed to return empty `response` with `will_continue=False` to signal that the function call is finished.", "title": "Willcontinue" }, "scheduling": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseScheduling" }, { "type": "null" } ], "default": null, "description": "Specifies how the response should be scheduled in the conversation. Only applicable to NON_BLOCKING function calls, is ignored otherwise. Defaults to WHEN_IDLE." }, "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/FunctionResponsePart" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a function response. Each part may\n have a different IANA MIME type.", "title": "Parts" }, "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The id of the function call this response is for. Populated by the client to match the corresponding function call `id`.", "title": "Id" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The name of the function to call. Matches [FunctionDeclaration.name] and [FunctionCall.name].", "title": "Name" }, "response": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Required. The function response in JSON object format. Use \"output\" key to specify function output and \"error\" key to specify error details (if any). If \"output\" and \"error\" keys are not specified, then whole \"response\" is treated as function output.", "title": "Response" } }, "title": "FunctionResponse", "type": "object" }, "FunctionResponseBlob": { "additionalProperties": false, "description": "Raw media bytes for function response.\n\nText should not be sent as raw bytes, use the FunctionResponse.response\nfield.", "properties": { "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Inline media bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob.\n Used to provide a label or filename to distinguish blobs.", "title": "Displayname" } }, "title": "FunctionResponseBlob", "type": "object" }, "FunctionResponseFileData": { "additionalProperties": false, "description": "URI based data for function response.", "properties": { "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file.\n Used to provide a label or filename to distinguish files.", "title": "Displayname" } }, "title": "FunctionResponseFileData", "type": "object" }, "FunctionResponsePart": { "additionalProperties": false, "description": "A datatype containing media that is part of a `FunctionResponse` message.\n\nA `FunctionResponsePart` consists of data which has an associated datatype. A\n`FunctionResponsePart` can only contain one of the accepted types in\n`FunctionResponsePart.data`.\n\nA `FunctionResponsePart` must have a fixed IANA MIME type identifying the\ntype and subtype of the media if the `inline_data` field is filled with raw\nbytes.", "properties": { "inlineData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseBlob" }, { "type": "null" } ], "default": null, "description": "Optional. Inline media bytes." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseFileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." } }, "title": "FunctionResponsePart", "type": "object" }, "FunctionResponseScheduling": { "description": "Specifies how the response should be scheduled in the conversation.", "enum": [ "SCHEDULING_UNSPECIFIED", "SILENT", "WHEN_IDLE", "INTERRUPT" ], "title": "FunctionResponseScheduling", "type": "string" }, "Language": { "description": "Programming language of the `code`.", "enum": [ "LANGUAGE_UNSPECIFIED", "PYTHON" ], "title": "Language", "type": "string" }, "Outcome": { "description": "Outcome of the code execution.", "enum": [ "OUTCOME_UNSPECIFIED", "OUTCOME_OK", "OUTCOME_FAILED", "OUTCOME_DEADLINE_EXCEEDED" ], "title": "Outcome", "type": "string" }, "Part": { "additionalProperties": false, "description": "A datatype containing media content.\n\nExactly one field within a Part should be set, representing the specific type\nof content being conveyed. Using multiple fields within the same `Part`\ninstance is considered invalid.", "properties": { "mediaResolution": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolution" }, { "type": "null" } ], "default": null, "description": "Media resolution for the input media.\n " }, "codeExecutionResult": { "anyOf": [ { "$ref": "#/$defs/CodeExecutionResult" }, { "type": "null" } ], "default": null, "description": "Optional. Result of executing the [ExecutableCode]." }, "executableCode": { "anyOf": [ { "$ref": "#/$defs/ExecutableCode" }, { "type": "null" } ], "default": null, "description": "Optional. Code generated by the model that is meant to be executed." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." }, "functionCall": { "anyOf": [ { "$ref": "#/$defs/FunctionCall" }, { "type": "null" } ], "default": null, "description": "Optional. A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] with the parameters and their values." }, "functionResponse": { "anyOf": [ { "$ref": "#/$defs/FunctionResponse" }, { "type": "null" } ], "default": null, "description": "Optional. The result output of a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function call. It is used as context to the model." }, "inlineData": { "anyOf": [ { "$ref": "#/$defs/Blob" }, { "type": "null" } ], "default": null, "description": "Optional. Inlined bytes data." }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Text part (can be code).", "title": "Text" }, "thought": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Indicates if the part is thought from the model.", "title": "Thought" }, "thoughtSignature": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. An opaque signature for the thought so it can be reused in subsequent requests.", "title": "Thoughtsignature" }, "videoMetadata": { "anyOf": [ { "$ref": "#/$defs/VideoMetadata" }, { "type": "null" } ], "default": null, "description": "Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data." } }, "title": "Part", "type": "object" }, "PartMediaResolution": { "additionalProperties": false, "description": "Media resolution for the input media.", "properties": { "level": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolutionLevel" }, { "type": "null" } ], "default": null, "description": "The tokenization quality used for given media.\n " }, "numTokens": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Specifies the required sequence length for media tokenization.\n ", "title": "Numtokens" } }, "title": "PartMediaResolution", "type": "object" }, "PartMediaResolutionLevel": { "description": "The tokenization quality used for given media.", "enum": [ "MEDIA_RESOLUTION_UNSPECIFIED", "MEDIA_RESOLUTION_LOW", "MEDIA_RESOLUTION_MEDIUM", "MEDIA_RESOLUTION_HIGH", "MEDIA_RESOLUTION_ULTRA_HIGH" ], "title": "PartMediaResolutionLevel", "type": "string" }, "PartialArg": { "additionalProperties": false, "description": "Partial argument value of the function call.\n\nThis data type is not supported in Gemini API.", "properties": { "nullValue": { "anyOf": [ { "const": "NULL_VALUE", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a null value.", "title": "Nullvalue" }, "numberValue": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a double value.", "title": "Numbervalue" }, "stringValue": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a string value.", "title": "Stringvalue" }, "boolValue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a boolean value.", "title": "Boolvalue" }, "jsonPath": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. A JSON Path (RFC 9535) to the argument being streamed. https://datatracker.ietf.org/doc/html/rfc9535. e.g. \"$.foo.bar[0].data\".", "title": "Jsonpath" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is not the last part of the same json_path. If true, another PartialArg message for the current json_path is expected to follow.", "title": "Willcontinue" } }, "title": "PartialArg", "type": "object" }, "VideoMetadata": { "additionalProperties": false, "description": "Metadata describes the input video content.", "properties": { "endOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The end offset of the video.", "title": "Endoffset" }, "fps": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. The frame rate of the video sent to the model. If not specified, the default value will be 1.0. The fps range is (0.0, 24.0].", "title": "Fps" }, "startOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The start offset of the video.", "title": "Startoffset" } }, "title": "VideoMetadata", "type": "object" } }, "additionalProperties": false, "required": [ "name" ] }

- Fields:
`after_model_callback (Optional[AfterModelCallback])`

`after_tool_callback (Optional[AfterToolCallback])`

`before_model_callback (Optional[BeforeModelCallback])`

`before_tool_callback (Optional[BeforeToolCallback])`

`code_executor (Optional[BaseCodeExecutor])`

`disallow_transfer_to_parent (bool)`

`disallow_transfer_to_peers (bool)`

`generate_content_config (Optional[types.GenerateContentConfig])`

`global_instruction (Union[str, InstructionProvider])`

`include_contents (Literal['default', 'none'])`

`input_schema (Optional[type[BaseModel]])`

`instruction (Union[str, InstructionProvider])`

`model (Union[str, BaseLlm])`

`on_model_error_callback (Optional[OnModelErrorCallback])`

`on_tool_error_callback (Optional[OnToolErrorCallback])`

`output_key (Optional[str])`

`output_schema (Optional[type[BaseModel]])`

`planner (Optional[BasePlanner])`

`static_instruction (Optional[types.ContentUnion])`

`tools (list[ToolUnion])`


- Validators:
`__model_validator_after`

»`all fields`

`validate_generate_content_config`

»`generate_content_config`


-
*field*after_model_callback*: AfterModelCallback | None**= None*[¶](#google.adk.agents.LlmAgent.after_model_callback) Callback or list of callbacks to be called after calling the LLM.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return None.

- Parameters:
**callback_context**– CallbackContext,**llm_response**– LlmResponse, the actual model response.

- Returns:
The content to return to the user. When present, the actual model response will be ignored and the provided content will be returned to user.

- Validated by:
`__model_validator_after`


-
*field*after_tool_callback*: AfterToolCallback | None**= None*[¶](#google.adk.agents.LlmAgent.after_tool_callback) Callback or list of callbacks to be called after calling the tool.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return None.

- Parameters:
**tool**– The tool to be called.**args**– The arguments to the tool.**tool_context**– ToolContext,**tool_response**– The response from the tool.

- Returns:
When present, the returned dict will be used as tool result.

- Validated by:
`__model_validator_after`


-
*field*before_model_callback*: BeforeModelCallback | None**= None*[¶](#google.adk.agents.LlmAgent.before_model_callback) Callback or list of callbacks to be called before calling the LLM.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return None.

- Parameters:
**callback_context**– CallbackContext,**llm_request**– LlmRequest, The raw model request. Callback can mutate the**request.**

- Returns:
The content to return to the user. When present, the model call will be skipped and the provided content will be returned to user.

- Validated by:
`__model_validator_after`


-
*field*before_tool_callback*: BeforeToolCallback | None**= None*[¶](#google.adk.agents.LlmAgent.before_tool_callback) Callback or list of callbacks to be called before calling the tool.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return None.

- Parameters:
**tool**– The tool to be called.**args**– The arguments to the tool.**tool_context**– ToolContext,

- Returns:
The tool response. When present, the returned tool response will be used and the framework will skip calling the actual tool.

- Validated by:
`__model_validator_after`


-
*field*code_executor*:*[BaseCodeExecutor](#google.adk.code_executors.BaseCodeExecutor)| None*= None*[¶](#google.adk.agents.LlmAgent.code_executor) Allow agent to execute code blocks from model responses using the provided CodeExecutor.

Check out available code executions in google.adk.code_executor package.

Note

To use model’s built-in code executor, use the BuiltInCodeExecutor.

- Validated by:
`__model_validator_after`


-
*field*disallow_transfer_to_parent*: bool**= False*[¶](#google.adk.agents.LlmAgent.disallow_transfer_to_parent) Disallows LLM-controlled transferring to the parent agent.

NOTE: Setting this as True also prevents this agent from continuing to reply to the end-user, and will transfer control back to the parent agent in the next turn. This behavior prevents one-way transfer, in which end-user may be stuck with one agent that cannot transfer to other agents in the agent tree.

- Validated by:
`__model_validator_after`


-
*field*disallow_transfer_to_peers*: bool**= False*[¶](#google.adk.agents.LlmAgent.disallow_transfer_to_peers) Disallows LLM-controlled transferring to the peer agents.

- Validated by:
`__model_validator_after`


-
*field*generate_content_config*: types.GenerateContentConfig | None**= None*[¶](#google.adk.agents.LlmAgent.generate_content_config) The additional content generation configurations.

NOTE: not all fields are usable, e.g. tools must be configured via tools, thinking_config must be configured via planner in LlmAgent.

For example: use this config to adjust model temperature, configure safety settings, etc.

- Validated by:
`__model_validator_after`

`validate_generate_content_config`


-
*field*global_instruction*: str | InstructionProvider**= ''*[¶](#google.adk.agents.LlmAgent.global_instruction) Instructions for all the agents in the entire agent tree.

DEPRECATED: This field is deprecated and will be removed in a future version. Use GlobalInstructionPlugin instead, which provides the same functionality at the App level. See migration guide for details.

ONLY the global_instruction in root agent will take effect.

For example: use global_instruction to make all agents have a stable identity or personality.

- Validated by:
`__model_validator_after`


-
*field*include_contents*: Literal['default', 'none']**= 'default'*[¶](#google.adk.agents.LlmAgent.include_contents) Controls content inclusion in model requests.

- Options:
default: Model receives relevant conversation history none: Model receives no prior history, operates solely on current instruction and input


- Validated by:
`__model_validator_after`


-
*field*input_schema*: type[BaseModel] | None**= None*[¶](#google.adk.agents.LlmAgent.input_schema) The input schema when agent is used as a tool.

- Validated by:
`__model_validator_after`


-
*field*instruction*: str | InstructionProvider**= ''*[¶](#google.adk.agents.LlmAgent.instruction) Dynamic instructions for the LLM model, guiding the agent’s behavior.

These instructions can contain placeholders like {variable_name} that will be resolved at runtime using session state and context.

**Behavior depends on static_instruction:**- If static_instruction is None: instruction goes to system_instruction - If static_instruction is set: instruction goes to user content in the requestThis allows for context caching optimization where static content (static_instruction) comes first in the prompt, followed by dynamic content (instruction).

- Validated by:
`__model_validator_after`


-
*field*model*: str |*[BaseLlm](#google.adk.models.BaseLlm)*= ''*[¶](#google.adk.agents.LlmAgent.model) The model to use for the agent.

When not set, the agent will inherit the model from its ancestor. If no ancestor provides a model, the agent uses the default model configured via LlmAgent.set_default_model. The built-in default is gemini-2.5-flash.

- Validated by:
`__model_validator_after`


-
*field*on_model_error_callback*: OnModelErrorCallback | None**= None*[¶](#google.adk.agents.LlmAgent.on_model_error_callback) Callback or list of callbacks to be called when a model call encounters an error.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return None.

- Parameters:
**callback_context**– CallbackContext,**llm_request**– LlmRequest, The raw model request.**error**– The error from the model call.

- Returns:
The content to return to the user. When present, the error will be ignored and the provided content will be returned to user.

- Validated by:
`__model_validator_after`


-
*field*on_tool_error_callback*: OnToolErrorCallback | None**= None*[¶](#google.adk.agents.LlmAgent.on_tool_error_callback) Callback or list of callbacks to be called when a tool call encounters an error.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return None.

- Parameters:
**tool**– The tool to be called.**args**– The arguments to the tool.**tool_context**– ToolContext,**error**– The error from the tool call.

- Returns:
When present, the returned dict will be used as tool result.

- Validated by:
`__model_validator_after`


-
*field*output_key*: str | None**= None*[¶](#google.adk.agents.LlmAgent.output_key) The key in session state to store the output of the agent.

Typically use cases: - Extracts agent reply for later use, such as in tools, callbacks, etc. - Connects agents to coordinate with each other.

- Validated by:
`__model_validator_after`


-
*field*output_schema*: type[BaseModel] | None**= None*[¶](#google.adk.agents.LlmAgent.output_schema) The output schema when agent replies.

Note

When this is set, agent can ONLY reply and CANNOT use any tools, such as function tools, RAGs, agent transfer, etc.

- Validated by:
`__model_validator_after`


-
*field*planner*:*[BasePlanner](#google.adk.planners.BasePlanner)| None*= None*[¶](#google.adk.agents.LlmAgent.planner) Instructs the agent to make a plan and execute it step by step.

Note

To use model’s built-in thinking features, set the thinking_config field in google.adk.planners.built_in_planner.

- Validated by:
`__model_validator_after`


-
*field*static_instruction*: types.ContentUnion | None**= None*[¶](#google.adk.agents.LlmAgent.static_instruction) Static instruction content sent literally as system instruction at the beginning.

This field is for content that never changes and doesn’t contain placeholders. It’s sent directly to the model without any processing or variable substitution.

This field is primarily for context caching optimization. Static instructions are sent as system instruction at the beginning of the request, allowing for improved performance when the static portion remains unchanged. Live API has its own cache mechanism, thus this field doesn’t work with Live API.

**Impact on instruction field:**- When static_instruction is None: instruction → system_instruction - When static_instruction is set: instruction → user content (after static content)**Context Caching:**-**Implicit Cache**: Automatic caching by model providers (no config needed) -**Explicit Cache**: Cache explicitly created by user for instructions, tools and contentsSee below for more information of Implicit Cache and Explicit Cache Gemini API:

[https://ai.google.dev/gemini-api/docs/caching?lang=python](https://ai.google.dev/gemini-api/docs/caching?lang=python)Vertex API:[https://cloud.google.com/vertex-ai/generative-ai/docs/context-cache/context-cache-overview](https://cloud.google.com/vertex-ai/generative-ai/docs/context-cache/context-cache-overview)Setting static_instruction alone does NOT enable caching automatically. For explicit caching control, configure context_cache_config at App level.

**Content Support:**Accepts types.ContentUnion which includes: - str: Simple text instruction - types.Content: Rich content object - types.Part: Single part (text, inline_data, file_data, etc.) - PIL.Image.Image: Image object - types.File: File reference - list[PartUnion]: List of parts**Examples:**[``](#id9)[`](#id11)python # Simple string instruction static_instruction = “You are a helpful assistant.”# Rich content with files static_instruction = types.Content(

role=’user’, parts=[

types.Part(text=’You are a helpful assistant.’), types.Part(file_data=types.FileData(…))

]

## )

[¶](#id13)- Validated by:
`__model_validator_after`


-
*field*tools*: list[ToolUnion]**[Optional]*[¶](#google.adk.agents.LlmAgent.tools) Tools available to this agent.

- Validated by:
`__model_validator_after`


-
config_type
[¶](#google.adk.agents.LlmAgent.config_type) alias of

`LlmAgentConfig`


-
*classmethod*set_default_model(*model*)[¶](#google.adk.agents.LlmAgent.set_default_model) Overrides the default model used when an agent has no model set.

- Return type:
`None`


-
*validator*validate_generate_content_config*»**generate_content_config*[¶](#google.adk.agents.LlmAgent.validate_generate_content_config) - Return type:
`GenerateContentConfig`


-
*async*canonical_global_instruction(*ctx*)[¶](#google.adk.agents.LlmAgent.canonical_global_instruction) The resolved self.instruction field to construct global instruction.

This method is only for use by Agent Development Kit.

- Return type:
`tuple`

[`str`

,`bool`

]- Parameters:
**ctx**– The context to retrieve the session state.- Returns:
A tuple of (instruction, bypass_state_injection). instruction: The resolved self.global_instruction field. bypass_state_injection: Whether the instruction is based on InstructionProvider.


-
*async*canonical_instruction(*ctx*)[¶](#google.adk.agents.LlmAgent.canonical_instruction) The resolved self.instruction field to construct instruction for this agent.

This method is only for use by Agent Development Kit.

- Return type:
`tuple`

[`str`

,`bool`

]- Parameters:
**ctx**– The context to retrieve the session state.- Returns:
A tuple of (instruction, bypass_state_injection). instruction: The resolved self.instruction field. bypass_state_injection: Whether the instruction is based on InstructionProvider.


-
*async*canonical_tools(*ctx=None*)[¶](#google.adk.agents.LlmAgent.canonical_tools) The resolved self.tools field as a list of BaseTool based on the context.

This method is only for use by Agent Development Kit.

- Return type:
`list`

[]`BaseTool`


-
DEFAULT_MODEL
*: ClassVar[str]**= 'gemini-2.5-flash'*[¶](#google.adk.agents.LlmAgent.DEFAULT_MODEL) System default model used when no model is set on an agent.


-
*property*canonical_after_model_callbacks*: list[Callable[[CallbackContext, LlmResponse], Awaitable[LlmResponse | None] | LlmResponse | None]]*[¶](#google.adk.agents.LlmAgent.canonical_after_model_callbacks) The resolved self.after_model_callback field as a list of _SingleAfterModelCallback.

This method is only for use by Agent Development Kit.


-
*property*canonical_after_tool_callbacks*: list[Callable[[*[BaseTool](#google.adk.tools.base_tool.BaseTool), dict[str, Any],[ToolContext](#google.adk.tools.tool_context.ToolContext), dict], Awaitable[dict | None] | dict | None] | list[Callable[¶](#google.adk.agents.LlmAgent.canonical_after_tool_callbacks) The resolved self.after_tool_callback field as a list of AfterToolCallback.

This method is only for use by Agent Development Kit.


-
*property*canonical_before_model_callbacks*: list[Callable[[CallbackContext, LlmRequest], Awaitable[LlmResponse | None] | LlmResponse | None]]*[¶](#google.adk.agents.LlmAgent.canonical_before_model_callbacks) The resolved self.before_model_callback field as a list of _SingleBeforeModelCallback.

This method is only for use by Agent Development Kit.


-
*property*canonical_before_tool_callbacks*: list[Callable[[*[BaseTool](#google.adk.tools.base_tool.BaseTool), dict[str, Any],[ToolContext](#google.adk.tools.tool_context.ToolContext)], Awaitable[dict | None] | dict | None] | list[Callable[¶](#google.adk.agents.LlmAgent.canonical_before_tool_callbacks) The resolved self.before_tool_callback field as a list of BeforeToolCallback.

This method is only for use by Agent Development Kit.


-
*property*canonical_model*:*[BaseLlm](#google.adk.models.BaseLlm)[¶](#google.adk.agents.LlmAgent.canonical_model) The resolved self.model field as BaseLlm.

This method is only for use by Agent Development Kit.


-
*property*canonical_on_model_error_callbacks*: list[Callable[[CallbackContext, LlmRequest, Exception], Awaitable[LlmResponse | None] | LlmResponse | None]]*[¶](#google.adk.agents.LlmAgent.canonical_on_model_error_callbacks) The resolved self.on_model_error_callback field as a list of _SingleOnModelErrorCallback.

This method is only for use by Agent Development Kit.


-
*property*canonical_on_tool_error_callbacks*: list[Callable[[*[BaseTool](#google.adk.tools.base_tool.BaseTool), dict[str, Any],[ToolContext](#google.adk.tools.tool_context.ToolContext), Exception], Awaitable[dict | None] | dict | None] | list[Callable[¶](#google.adk.agents.LlmAgent.canonical_on_tool_error_callbacks) The resolved self.on_tool_error_callback field as a list of OnToolErrorCallback.

This method is only for use by Agent Development Kit.


-
*pydantic model*google.adk.agents.LoopAgent[¶](#google.adk.agents.LoopAgent) Bases:

`BaseAgent`

A shell agent that run its sub-agents in a loop.

When sub-agent generates an event with escalate or max_iterations are reached, the loop agent will stop.

## Show JSON schema

{ "title": "LoopAgent", "description": "A shell agent that run its sub-agents in a loop.\n\nWhen sub-agent generates an event with escalate or max_iterations are\nreached, the loop agent will stop.", "type": "object", "properties": { "name": { "title": "Name", "type": "string" }, "description": { "default": "", "title": "Description", "type": "string" }, "parent_agent": { "anyOf": [ { "$ref": "#/$defs/BaseAgent" }, { "type": "null" } ], "default": null }, "sub_agents": { "items": { "$ref": "#/$defs/BaseAgent" }, "title": "Sub Agents", "type": "array" }, "before_agent_callback": { "default": null, "title": "Before Agent Callback", "type": "null" }, "after_agent_callback": { "default": null, "title": "After Agent Callback", "type": "null" }, "max_iterations": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "title": "Max Iterations" } }, "$defs": { "BaseAgent": { "additionalProperties": false, "description": "Base class for all agents in Agent Development Kit.", "properties": { "name": { "title": "Name", "type": "string" }, "description": { "default": "", "title": "Description", "type": "string" }, "parent_agent": { "anyOf": [ { "$ref": "#/$defs/BaseAgent" }, { "type": "null" } ], "default": null }, "sub_agents": { "items": { "$ref": "#/$defs/BaseAgent" }, "title": "Sub Agents", "type": "array" }, "before_agent_callback": { "default": null, "title": "Before Agent Callback", "type": "null" }, "after_agent_callback": { "default": null, "title": "After Agent Callback", "type": "null" } }, "required": [ "name" ], "title": "BaseAgent", "type": "object" } }, "additionalProperties": false, "required": [ "name" ] }

- Fields:
`max_iterations (Optional[int])`


- Validators:

-
*field*max_iterations*: int | None**= None*[¶](#google.adk.agents.LoopAgent.max_iterations) The maximum number of iterations to run the loop agent.

If not set, the loop agent will run indefinitely until a sub-agent escalates.


-
config_type
[¶](#google.adk.agents.LoopAgent.config_type) alias of

`LoopAgentConfig`


-
*class*google.adk.agents.McpInstructionProvider(*connection_params*,*prompt_name*,*errlog=<_io.TextIOWrapper name='<stderr>' mode='w' encoding='utf-8'>*)[¶](#google.adk.agents.McpInstructionProvider) Bases:

`Callable`

[[`ReadonlyContext`

],`str`

|`Awaitable`

[`str`

]]Fetches agent instructions from an MCP server.

Initializes the McpInstructionProvider.

- Parameters:
**connection_params**– Parameters for connecting to the MCP server.**prompt_name**– The name of the MCP Prompt to fetch.**errlog**– TextIO stream for error logging.


-
*pydantic model*google.adk.agents.ParallelAgent[¶](#google.adk.agents.ParallelAgent) Bases:

`BaseAgent`

A shell agent that runs its sub-agents in parallel in an isolated manner.

This approach is beneficial for scenarios requiring multiple perspectives or attempts on a single task, such as:

Running different algorithms simultaneously.

Generating multiple responses for review by a subsequent evaluation agent.


## Show JSON schema

{ "title": "ParallelAgent", "description": "A shell agent that runs its sub-agents in parallel in an isolated manner.\n\nThis approach is beneficial for scenarios requiring multiple perspectives or\nattempts on a single task, such as:\n\n- Running different algorithms simultaneously.\n- Generating multiple responses for review by a subsequent evaluation agent.", "type": "object", "properties": { "name": { "title": "Name", "type": "string" }, "description": { "default": "", "title": "Description", "type": "string" }, "parent_agent": { "anyOf": [ { "$ref": "#/$defs/BaseAgent" }, { "type": "null" } ], "default": null }, "sub_agents": { "items": { "$ref": "#/$defs/BaseAgent" }, "title": "Sub Agents", "type": "array" }, "before_agent_callback": { "default": null, "title": "Before Agent Callback", "type": "null" }, "after_agent_callback": { "default": null, "title": "After Agent Callback", "type": "null" } }, "$defs": { "BaseAgent": { "additionalProperties": false, "description": "Base class for all agents in Agent Development Kit.", "properties": { "name": { "title": "Name", "type": "string" }, "description": { "default": "", "title": "Description", "type": "string" }, "parent_agent": { "anyOf": [ { "$ref": "#/$defs/BaseAgent" }, { "type": "null" } ], "default": null }, "sub_agents": { "items": { "$ref": "#/$defs/BaseAgent" }, "title": "Sub Agents", "type": "array" }, "before_agent_callback": { "default": null, "title": "Before Agent Callback", "type": "null" }, "after_agent_callback": { "default": null, "title": "After Agent Callback", "type": "null" } }, "required": [ "name" ], "title": "BaseAgent", "type": "object" } }, "additionalProperties": false, "required": [ "name" ] }

- Fields:
- Validators:

-
config_type
[¶](#google.adk.agents.ParallelAgent.config_type) alias of

`ParallelAgentConfig`


-
*pydantic model*google.adk.agents.RunConfig[¶](#google.adk.agents.RunConfig) Bases:

`BaseModel`

Configs for runtime behavior of agents.

The configs here will be overridden by agent-specific configurations.

## Show JSON schema

{ "title": "RunConfig", "description": "Configs for runtime behavior of agents.\n\nThe configs here will be overridden by agent-specific configurations.", "type": "object", "properties": { "speech_config": { "anyOf": [ { "$ref": "#/$defs/SpeechConfig" }, { "type": "null" } ], "default": null }, "response_modalities": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Response Modalities" }, "save_input_blobs_as_artifacts": { "default": false, "deprecated": true, "description": "Whether or not to save the input blobs as artifacts. DEPRECATED: Use SaveFilesAsArtifactsPlugin instead for better control and flexibility. See google.adk.plugins.SaveFilesAsArtifactsPlugin.", "title": "Save Input Blobs As Artifacts", "type": "boolean" }, "support_cfc": { "default": false, "title": "Support Cfc", "type": "boolean" }, "streaming_mode": { "$ref": "#/$defs/StreamingMode", "default": null }, "output_audio_transcription": { "anyOf": [ { "$ref": "#/$defs/AudioTranscriptionConfig" }, { "type": "null" } ] }, "input_audio_transcription": { "anyOf": [ { "$ref": "#/$defs/AudioTranscriptionConfig" }, { "type": "null" } ] }, "realtime_input_config": { "anyOf": [ { "$ref": "#/$defs/RealtimeInputConfig" }, { "type": "null" } ], "default": null }, "enable_affective_dialog": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Enable Affective Dialog" }, "proactivity": { "anyOf": [ { "$ref": "#/$defs/ProactivityConfig" }, { "type": "null" } ], "default": null }, "session_resumption": { "anyOf": [ { "$ref": "#/$defs/SessionResumptionConfig" }, { "type": "null" } ], "default": null }, "context_window_compression": { "anyOf": [ { "$ref": "#/$defs/ContextWindowCompressionConfig" }, { "type": "null" } ], "default": null }, "save_live_blob": { "default": false, "title": "Save Live Blob", "type": "boolean" }, "save_live_audio": { "default": false, "deprecated": true, "description": "DEPRECATED: Use save_live_blob instead. If set to True, it saves live video and audio data to session and artifact service.", "title": "Save Live Audio", "type": "boolean" }, "max_llm_calls": { "default": 500, "title": "Max Llm Calls", "type": "integer" }, "custom_metadata": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "title": "Custom Metadata" } }, "$defs": { "ActivityHandling": { "description": "The different ways of handling user activity.", "enum": [ "ACTIVITY_HANDLING_UNSPECIFIED", "START_OF_ACTIVITY_INTERRUPTS", "NO_INTERRUPTION" ], "title": "ActivityHandling", "type": "string" }, "AudioTranscriptionConfig": { "additionalProperties": false, "description": "The audio transcription configuration in Setup.", "properties": {}, "title": "AudioTranscriptionConfig", "type": "object" }, "AutomaticActivityDetection": { "additionalProperties": false, "description": "Configures automatic detection of activity.", "properties": { "disabled": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "If enabled, detected voice and text input count as activity. If disabled, the client must send activity signals.", "title": "Disabled" }, "startOfSpeechSensitivity": { "anyOf": [ { "$ref": "#/$defs/StartSensitivity" }, { "type": "null" } ], "default": null, "description": "Determines how likely speech is to be detected." }, "endOfSpeechSensitivity": { "anyOf": [ { "$ref": "#/$defs/EndSensitivity" }, { "type": "null" } ], "default": null, "description": "Determines how likely detected speech is ended." }, "prefixPaddingMs": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "The required duration of detected speech before start-of-speech is committed. The lower this value the more sensitive the start-of-speech detection is and the shorter speech can be recognized. However, this also increases the probability of false positives.", "title": "Prefixpaddingms" }, "silenceDurationMs": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "The required duration of detected non-speech (e.g. silence) before end-of-speech is committed. The larger this value, the longer speech gaps can be without interrupting the user's activity but this will increase the model's latency.", "title": "Silencedurationms" } }, "title": "AutomaticActivityDetection", "type": "object" }, "ContextWindowCompressionConfig": { "additionalProperties": false, "description": "Enables context window compression -- mechanism managing model context window so it does not exceed given length.", "properties": { "triggerTokens": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Number of tokens (before running turn) that triggers context window compression mechanism.", "title": "Triggertokens" }, "slidingWindow": { "anyOf": [ { "$ref": "#/$defs/SlidingWindow" }, { "type": "null" } ], "default": null, "description": "Sliding window compression mechanism." } }, "title": "ContextWindowCompressionConfig", "type": "object" }, "EndSensitivity": { "description": "End of speech sensitivity.", "enum": [ "END_SENSITIVITY_UNSPECIFIED", "END_SENSITIVITY_HIGH", "END_SENSITIVITY_LOW" ], "title": "EndSensitivity", "type": "string" }, "MultiSpeakerVoiceConfig": { "additionalProperties": false, "description": "Configuration for a multi-speaker text-to-speech request.", "properties": { "speakerVoiceConfigs": { "anyOf": [ { "items": { "$ref": "#/$defs/SpeakerVoiceConfig" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Required. A list of configurations for the voices of the speakers. Exactly two speaker voice configurations must be provided.", "title": "Speakervoiceconfigs" } }, "title": "MultiSpeakerVoiceConfig", "type": "object" }, "PrebuiltVoiceConfig": { "additionalProperties": false, "description": "The configuration for the prebuilt speaker to use.", "properties": { "voiceName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The name of the preset voice to use.", "title": "Voicename" } }, "title": "PrebuiltVoiceConfig", "type": "object" }, "ProactivityConfig": { "additionalProperties": false, "description": "Config for proactivity features.", "properties": { "proactiveAudio": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "If enabled, the model can reject responding to the last prompt. For\n example, this allows the model to ignore out of context speech or to stay\n silent if the user did not make a request, yet.", "title": "Proactiveaudio" } }, "title": "ProactivityConfig", "type": "object" }, "RealtimeInputConfig": { "additionalProperties": false, "description": "Marks the end of user activity.\n\nThis can only be sent if automatic (i.e. server-side) activity detection is\ndisabled.", "properties": { "automaticActivityDetection": { "anyOf": [ { "$ref": "#/$defs/AutomaticActivityDetection" }, { "type": "null" } ], "default": null, "description": "If not set, automatic activity detection is enabled by default. If automatic voice detection is disabled, the client must send activity signals." }, "activityHandling": { "anyOf": [ { "$ref": "#/$defs/ActivityHandling" }, { "type": "null" } ], "default": null, "description": "Defines what effect activity has." }, "turnCoverage": { "anyOf": [ { "$ref": "#/$defs/TurnCoverage" }, { "type": "null" } ], "default": null, "description": "Defines which input is included in the user's turn." } }, "title": "RealtimeInputConfig", "type": "object" }, "ReplicatedVoiceConfig": { "additionalProperties": false, "description": "ReplicatedVoiceConfig is used to configure replicated voice.", "properties": { "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The mime type of the replicated voice.\n ", "title": "Mimetype" }, "voiceSampleAudio": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "The sample audio of the replicated voice.\n ", "title": "Voicesampleaudio" } }, "title": "ReplicatedVoiceConfig", "type": "object" }, "SessionResumptionConfig": { "additionalProperties": false, "description": "Configuration of session resumption mechanism.\n\nIncluded in `LiveConnectConfig.session_resumption`. If included server\nwill send `LiveServerSessionResumptionUpdate` messages.", "properties": { "handle": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Session resumption handle of previous session (session to restore).\n\nIf not present new session will be started.", "title": "Handle" }, "transparent": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "If set the server will send `last_consumed_client_message_index` in the `session_resumption_update` messages to allow for transparent reconnections.", "title": "Transparent" } }, "title": "SessionResumptionConfig", "type": "object" }, "SlidingWindow": { "additionalProperties": false, "description": "Context window will be truncated by keeping only suffix of it.\n\nContext window will always be cut at start of USER role turn. System\ninstructions and `BidiGenerateContentSetup.prefix_turns` will not be\nsubject to the sliding window mechanism, they will always stay at the\nbeginning of context window.", "properties": { "targetTokens": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Session reduction target -- how many tokens we should keep. Window shortening operation has some latency costs, so we should avoid running it on every turn. Should be < trigger_tokens. If not set, trigger_tokens/2 is assumed.", "title": "Targettokens" } }, "title": "SlidingWindow", "type": "object" }, "SpeakerVoiceConfig": { "additionalProperties": false, "description": "Configuration for a single speaker in a multi speaker setup.", "properties": { "speaker": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The name of the speaker. This should be the same as the speaker name used in the prompt.", "title": "Speaker" }, "voiceConfig": { "anyOf": [ { "$ref": "#/$defs/VoiceConfig" }, { "type": "null" } ], "default": null, "description": "Required. The configuration for the voice of this speaker." } }, "title": "SpeakerVoiceConfig", "type": "object" }, "SpeechConfig": { "additionalProperties": false, "properties": { "voiceConfig": { "anyOf": [ { "$ref": "#/$defs/VoiceConfig" }, { "type": "null" } ], "default": null, "description": "Configuration for the voice of the response." }, "languageCode": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Language code (ISO 639. e.g. en-US) for the speech synthesization.", "title": "Languagecode" }, "multiSpeakerVoiceConfig": { "anyOf": [ { "$ref": "#/$defs/MultiSpeakerVoiceConfig" }, { "type": "null" } ], "default": null, "description": "The configuration for a multi-speaker text-to-speech request. This field is mutually exclusive with `voice_config`." } }, "title": "SpeechConfig", "type": "object" }, "StartSensitivity": { "description": "Start of speech sensitivity.", "enum": [ "START_SENSITIVITY_UNSPECIFIED", "START_SENSITIVITY_HIGH", "START_SENSITIVITY_LOW" ], "title": "StartSensitivity", "type": "string" }, "StreamingMode": { "description": "Streaming modes for agent execution.\n\nThis enum defines different streaming behaviors for how the agent returns\nevents as model response.", "enum": [ null, "sse", "bidi" ], "title": "StreamingMode" }, "TurnCoverage": { "description": "Options about which input is included in the user's turn.", "enum": [ "TURN_COVERAGE_UNSPECIFIED", "TURN_INCLUDES_ONLY_ACTIVITY", "TURN_INCLUDES_ALL_INPUT" ], "title": "TurnCoverage", "type": "string" }, "VoiceConfig": { "additionalProperties": false, "properties": { "replicatedVoiceConfig": { "anyOf": [ { "$ref": "#/$defs/ReplicatedVoiceConfig" }, { "type": "null" } ], "default": null, "description": "If true, the model will use a replicated voice for the response." }, "prebuiltVoiceConfig": { "anyOf": [ { "$ref": "#/$defs/PrebuiltVoiceConfig" }, { "type": "null" } ], "default": null, "description": "The configuration for the prebuilt voice to use." } }, "title": "VoiceConfig", "type": "object" } }, "additionalProperties": false }

- Fields:
`context_window_compression (google.genai.types.ContextWindowCompressionConfig | None)`

`custom_metadata (dict[str, Any] | None)`

`enable_affective_dialog (bool | None)`

`input_audio_transcription (google.genai.types.AudioTranscriptionConfig | None)`

`max_llm_calls (int)`

`output_audio_transcription (google.genai.types.AudioTranscriptionConfig | None)`

`proactivity (google.genai.types.ProactivityConfig | None)`

`realtime_input_config (google.genai.types.RealtimeInputConfig | None)`

`response_modalities (list[str] | None)`

`save_input_blobs_as_artifacts (bool)`

`save_live_audio (bool)`

`save_live_blob (bool)`

`session_resumption (google.genai.types.SessionResumptionConfig | None)`

`speech_config (google.genai.types.SpeechConfig | None)`

`streaming_mode (google.adk.agents.run_config.StreamingMode)`

`support_cfc (bool)`


- Validators:
`check_for_deprecated_save_live_audio`

»`all fields`

`validate_max_llm_calls`

»`max_llm_calls`


-
*field*context_window_compression*: types.ContextWindowCompressionConfig | None**= None*[¶](#google.adk.agents.RunConfig.context_window_compression) Configuration for context window compression. If set, this will enable context window compression for LLM input.

- Validated by:
`check_for_deprecated_save_live_audio`


-
*field*custom_metadata*: dict[str, Any] | None**= None*[¶](#google.adk.agents.RunConfig.custom_metadata) Custom metadata for the current invocation.

- Validated by:
`check_for_deprecated_save_live_audio`


-
*field*enable_affective_dialog*: bool | None**= None*[¶](#google.adk.agents.RunConfig.enable_affective_dialog) If enabled, the model will detect emotions and adapt its responses accordingly.

- Validated by:
`check_for_deprecated_save_live_audio`


-
*field*input_audio_transcription*: types.AudioTranscriptionConfig | None**[Optional]*[¶](#google.adk.agents.RunConfig.input_audio_transcription) Input transcription for live agents with audio input from user.

- Validated by:
`check_for_deprecated_save_live_audio`


-
*field*max_llm_calls*: int**= 500*[¶](#google.adk.agents.RunConfig.max_llm_calls) A limit on the total number of llm calls for a given run.

- Valid Values:
More than 0 and less than sys.maxsize: The bound on the number of llm calls is enforced, if the value is set in this range.

Less than or equal to 0: This allows for unbounded number of llm calls.


- Validated by:
`check_for_deprecated_save_live_audio`

`validate_max_llm_calls`


-
*field*output_audio_transcription*: types.AudioTranscriptionConfig | None**[Optional]*[¶](#google.adk.agents.RunConfig.output_audio_transcription) Output transcription for live agents with audio response.

- Validated by:
`check_for_deprecated_save_live_audio`


-
*field*proactivity*: types.ProactivityConfig | None**= None*[¶](#google.adk.agents.RunConfig.proactivity) Configures the proactivity of the model. This allows the model to respond proactively to the input and to ignore irrelevant input.

- Validated by:
`check_for_deprecated_save_live_audio`


-
*field*realtime_input_config*: types.RealtimeInputConfig | None**= None*[¶](#google.adk.agents.RunConfig.realtime_input_config) Realtime input config for live agents with audio input from user.

- Validated by:
`check_for_deprecated_save_live_audio`


-
*field*response_modalities*: list[str] | None**= None*[¶](#google.adk.agents.RunConfig.response_modalities) The output modalities. If not set, it’s default to AUDIO.

- Validated by:
`check_for_deprecated_save_live_audio`


-
*field*save_live_blob*: bool**= False*[¶](#google.adk.agents.RunConfig.save_live_blob) Saves live video and audio data to session and artifact service.

- Validated by:
`check_for_deprecated_save_live_audio`


-
*field*session_resumption*: types.SessionResumptionConfig | None**= None*[¶](#google.adk.agents.RunConfig.session_resumption) Configures session resumption mechanism. Only support transparent session resumption mode now.

- Validated by:
`check_for_deprecated_save_live_audio`


-
*field*speech_config*: types.SpeechConfig | None**= None*[¶](#google.adk.agents.RunConfig.speech_config) Speech configuration for the live agent.

- Validated by:
`check_for_deprecated_save_live_audio`


-
*field*streaming_mode*: StreamingMode**= StreamingMode.NONE*[¶](#google.adk.agents.RunConfig.streaming_mode) Streaming mode, None or StreamingMode.SSE or StreamingMode.BIDI.

- Validated by:
`check_for_deprecated_save_live_audio`


-
*field*support_cfc*: bool**= False*[¶](#google.adk.agents.RunConfig.support_cfc) Whether to support CFC (Compositional Function Calling). Only applicable for StreamingMode.SSE. If it’s true. the LIVE API will be invoked. Since only LIVE API supports CFC

Warning

This feature is

**experimental**and its API or behavior may change in future releases.- Validated by:
`check_for_deprecated_save_live_audio`


-
*validator*check_for_deprecated_save_live_audio*»**all fields*[¶](#google.adk.agents.RunConfig.check_for_deprecated_save_live_audio) If save_live_audio is passed, use it to set save_live_blob.

- Return type:
`Any`


-
*validator*validate_max_llm_calls*»**max_llm_calls*[¶](#google.adk.agents.RunConfig.validate_max_llm_calls) - Return type:
`int`


-
save_input_blobs_as_artifacts
*: bool*[¶](#google.adk.agents.RunConfig.save_input_blobs_as_artifacts) Read-only data descriptor used to emit a runtime deprecation warning before accessing a deprecated field.

-
msg
[¶](#google.adk.agents.RunConfig.msg) The deprecation message to be emitted.


-
wrapped_property
[¶](#google.adk.agents.RunConfig.wrapped_property) The property instance if the deprecated field is a computed field, or None.


-
field_name
[¶](#google.adk.agents.RunConfig.field_name) The name of the field being deprecated.


-
msg

-
save_live_audio
*: bool*[¶](#google.adk.agents.RunConfig.save_live_audio) Read-only data descriptor used to emit a runtime deprecation warning before accessing a deprecated field.

-
msg
[¶](#id0) The deprecation message to be emitted.


-
wrapped_property
[¶](#id14) The property instance if the deprecated field is a computed field, or None.


-
field_name
[¶](#id15) The name of the field being deprecated.


-
msg


-
*pydantic model*google.adk.agents.SequentialAgent[¶](#google.adk.agents.SequentialAgent) Bases:

`BaseAgent`

A shell agent that runs its sub-agents in sequence.

## Show JSON schema

{ "title": "SequentialAgent", "description": "A shell agent that runs its sub-agents in sequence.", "type": "object", "properties": { "name": { "title": "Name", "type": "string" }, "description": { "default": "", "title": "Description", "type": "string" }, "parent_agent": { "anyOf": [ { "$ref": "#/$defs/BaseAgent" }, { "type": "null" } ], "default": null }, "sub_agents": { "items": { "$ref": "#/$defs/BaseAgent" }, "title": "Sub Agents", "type": "array" }, "before_agent_callback": { "default": null, "title": "Before Agent Callback", "type": "null" }, "after_agent_callback": { "default": null, "title": "After Agent Callback", "type": "null" } }, "$defs": { "BaseAgent": { "additionalProperties": false, "description": "Base class for all agents in Agent Development Kit.", "properties": { "name": { "title": "Name", "type": "string" }, "description": { "default": "", "title": "Description", "type": "string" }, "parent_agent": { "anyOf": [ { "$ref": "#/$defs/BaseAgent" }, { "type": "null" } ], "default": null }, "sub_agents": { "items": { "$ref": "#/$defs/BaseAgent" }, "title": "Sub Agents", "type": "array" }, "before_agent_callback": { "default": null, "title": "Before Agent Callback", "type": "null" }, "after_agent_callback": { "default": null, "title": "After Agent Callback", "type": "null" } }, "required": [ "name" ], "title": "BaseAgent", "type": "object" } }, "additionalProperties": false, "required": [ "name" ] }

- Fields:
- Validators:

-
config_type
[¶](#google.adk.agents.SequentialAgent.config_type) alias of

`SequentialAgentConfig`


# google.adk.artifacts module[¶](#module-google.adk.artifacts)

-
*class*google.adk.artifacts.BaseArtifactService[¶](#google.adk.artifacts.BaseArtifactService) Bases:

`ABC`

Abstract base class for artifact services.

-
*abstractmethod async*delete_artifact(***,*app_name*,*user_id*,*filename*,*session_id=None*)[¶](#google.adk.artifacts.BaseArtifactService.delete_artifact) Deletes an artifact.

- Return type:
`None`

- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**filename**– The name of the artifact file.**session_id**– The ID of the session. If None, delete the user-scoped artifact.


-
*abstractmethod async*get_artifact_version(***,*app_name*,*user_id*,*filename*,*session_id=None*,*version=None*)[¶](#google.adk.artifacts.BaseArtifactService.get_artifact_version) Gets the metadata for a specific version of an artifact.

- Return type:
`Optional`

[`ArtifactVersion`

]- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**filename**– The name of the artifact file.**session_id**– The ID of the session. If None, the artifact will be fetched from the user-scoped artifacts. Otherwise, it will be fetched from the specified session.**version**– The version number of the artifact to retrieve. If None, the latest version will be returned.

- Returns:
An ArtifactVersion object containing the metadata of the specified artifact version, or None if the artifact version is not found.


-
*abstractmethod async*list_artifact_keys(***,*app_name*,*user_id*,*session_id=None*)[¶](#google.adk.artifacts.BaseArtifactService.list_artifact_keys) Lists all the artifact filenames within a session.

- Return type:
`list`

[`str`

]- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**session_id**– The ID of the session.

- Returns:
A list of artifact filenames. If session_id is provided, returns both session-scoped and user-scoped artifact filenames. If session_id is None, returns user-scoped artifact filenames.


-
*abstractmethod async*list_artifact_versions(***,*app_name*,*user_id*,*filename*,*session_id=None*)[¶](#google.adk.artifacts.BaseArtifactService.list_artifact_versions) Lists all versions and their metadata for a specific artifact.

- Return type:
`list`

[`ArtifactVersion`

]- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**filename**– The name of the artifact file.**session_id**– The ID of the session. If None, lists versions of the user-scoped artifact. Otherwise, lists versions of the artifact within the specified session.

- Returns:
A list of ArtifactVersion objects, each representing a version of the artifact and its associated metadata.


-
*abstractmethod async*list_versions(***,*app_name*,*user_id*,*filename*,*session_id=None*)[¶](#google.adk.artifacts.BaseArtifactService.list_versions) Lists all versions of an artifact.

- Return type:
`list`

[`int`

]- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**filename**– The name of the artifact file.**session_id**– The ID of the session. If None, only list the user-scoped artifacts versions.

- Returns:
A list of all available versions of the artifact.


-
*abstractmethod async*load_artifact(***,*app_name*,*user_id*,*filename*,*session_id=None*,*version=None*)[¶](#google.adk.artifacts.BaseArtifactService.load_artifact) Gets an artifact from the artifact service storage.

The artifact is a file identified by the app name, user ID, session ID, and filename.

- Return type:
`Optional`

[`Part`

]- Parameters:
**app_name**– The app name.**user_id**– The user ID.**filename**– The filename of the artifact.**session_id**– The session ID. If None, load the user-scoped artifact.**version**– The version of the artifact. If None, the latest version will be returned.

- Returns:
The artifact or None if not found.


-
*abstractmethod async*save_artifact(***,*app_name*,*user_id*,*filename*,*artifact*,*session_id=None*,*custom_metadata=None*)[¶](#google.adk.artifacts.BaseArtifactService.save_artifact) Saves an artifact to the artifact service storage.

The artifact is a file identified by the app name, user ID, session ID, and filename. After saving the artifact, a revision ID is returned to identify the artifact version.

- Return type:
`int`

- Parameters:
**app_name**– The app name.**user_id**– The user ID.**filename**– The filename of the artifact.**artifact**– The artifact to save. If the artifact consists of file_data, the artifact service assumes its content has been uploaded separately, and this method will associate the file_data with the artifact if necessary.**session_id**– The session ID. If None, the artifact is user-scoped.**custom_metadata**– custom metadata to associate with the artifact.

- Returns:
The revision ID. The first version of the artifact has a revision ID of 0. This is incremented by 1 after each successful save.


-

-
*class*google.adk.artifacts.FileArtifactService(*root_dir*)[¶](#google.adk.artifacts.FileArtifactService) Bases:

`BaseArtifactService`

Stores filesystem-backed artifacts beneath a configurable root directory.

Initializes the file-based artifact service.

- Parameters:
**root_dir**– The directory that will contain artifact data.

-
*async*delete_artifact(***,*app_name*,*user_id*,*filename*,*session_id=None*)[¶](#google.adk.artifacts.FileArtifactService.delete_artifact) Deletes an artifact.

- Return type:
`None`

- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**filename**– The name of the artifact file.**session_id**– The ID of the session. Leave unset for user-scoped artifacts.


-
*async*get_artifact_version(***,*app_name*,*user_id*,*filename*,*session_id=None*,*version=None*)[¶](#google.adk.artifacts.FileArtifactService.get_artifact_version) Gets metadata for a specific artifact version.

- Return type:
`Optional`

[`ArtifactVersion`

]


-
*async*list_artifact_keys(***,*app_name*,*user_id*,*session_id=None*)[¶](#google.adk.artifacts.FileArtifactService.list_artifact_keys) Lists all the artifact filenames within a session.

- Return type:
`list`

[`str`

]- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**session_id**– The ID of the session.

- Returns:
A list of artifact filenames. If session_id is provided, returns both session-scoped and user-scoped artifact filenames. If session_id is None, returns user-scoped artifact filenames.


-
*async*list_artifact_versions(***,*app_name*,*user_id*,*filename*,*session_id=None*)[¶](#google.adk.artifacts.FileArtifactService.list_artifact_versions) Lists metadata for each artifact version on disk.

- Return type:
`list`

[`ArtifactVersion`

]


-
*async*list_versions(***,*app_name*,*user_id*,*filename*,*session_id=None*)[¶](#google.adk.artifacts.FileArtifactService.list_versions) Lists all versions stored for an artifact.

- Return type:
`list`

[`int`

]


-
*async*load_artifact(***,*app_name*,*user_id*,*filename*,*session_id=None*,*version=None*)[¶](#google.adk.artifacts.FileArtifactService.load_artifact) Gets an artifact from the artifact service storage.

The artifact is a file identified by the app name, user ID, session ID, and filename.

- Return type:
`Optional`

[`Part`

]- Parameters:
**app_name**– The app name.**user_id**– The user ID.**filename**– The filename of the artifact.**session_id**– The session ID. If None, load the user-scoped artifact.**version**– The version of the artifact. If None, the latest version will be returned.

- Returns:
The artifact or None if not found.


-
*async*save_artifact(***,*app_name*,*user_id*,*filename*,*artifact*,*session_id=None*,*custom_metadata=None*)[¶](#google.adk.artifacts.FileArtifactService.save_artifact) Persists an artifact to disk.

Filenames may be simple (

`"report.txt"`

), nested (`"images/photo.png"`

), or explicitly user-scoped (`"user:shared/diagram.png"`

). All values are interpreted relative to the computed scope root; absolute paths or inputs that traverse outside that root (for example`"../../secret.txt"`

) raise`ValueError`

.- Return type:
`int`


-
*class*google.adk.artifacts.GcsArtifactService(*bucket_name*,***kwargs*)[¶](#google.adk.artifacts.GcsArtifactService) Bases:

`BaseArtifactService`

An artifact service implementation using Google Cloud Storage (GCS).

Initializes the GcsArtifactService.

- Parameters:
**bucket_name**– The name of the bucket to use.****kwargs**– Keyword arguments to pass to the Google Cloud Storage client.


-
*async*delete_artifact(***,*app_name*,*user_id*,*filename*,*session_id=None*)[¶](#google.adk.artifacts.GcsArtifactService.delete_artifact) Deletes an artifact.

- Return type:
`None`

- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**filename**– The name of the artifact file.**session_id**– The ID of the session. If None, delete the user-scoped artifact.


-
*async*get_artifact_version(***,*app_name*,*user_id*,*filename*,*session_id=None*,*version=None*)[¶](#google.adk.artifacts.GcsArtifactService.get_artifact_version) Gets the metadata for a specific version of an artifact.

- Return type:
`Optional`

[`ArtifactVersion`

]- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**filename**– The name of the artifact file.**session_id**– The ID of the session. If None, the artifact will be fetched from the user-scoped artifacts. Otherwise, it will be fetched from the specified session.**version**– The version number of the artifact to retrieve. If None, the latest version will be returned.

- Returns:
An ArtifactVersion object containing the metadata of the specified artifact version, or None if the artifact version is not found.


-
*async*list_artifact_keys(***,*app_name*,*user_id*,*session_id=None*)[¶](#google.adk.artifacts.GcsArtifactService.list_artifact_keys) Lists all the artifact filenames within a session.

- Return type:
`list`

[`str`

]- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**session_id**– The ID of the session.

- Returns:
A list of artifact filenames. If session_id is provided, returns both session-scoped and user-scoped artifact filenames. If session_id is None, returns user-scoped artifact filenames.


-
*async*list_artifact_versions(***,*app_name*,*user_id*,*filename*,*session_id=None*)[¶](#google.adk.artifacts.GcsArtifactService.list_artifact_versions) Lists all versions and their metadata for a specific artifact.

- Return type:
`list`

[`ArtifactVersion`

]- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**filename**– The name of the artifact file.**session_id**– The ID of the session. If None, lists versions of the user-scoped artifact. Otherwise, lists versions of the artifact within the specified session.

- Returns:
A list of ArtifactVersion objects, each representing a version of the artifact and its associated metadata.


-
*async*list_versions(***,*app_name*,*user_id*,*filename*,*session_id=None*)[¶](#google.adk.artifacts.GcsArtifactService.list_versions) Lists all versions of an artifact.

- Return type:
`list`

[`int`

]- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**filename**– The name of the artifact file.**session_id**– The ID of the session. If None, only list the user-scoped artifacts versions.

- Returns:
A list of all available versions of the artifact.


-
*async*load_artifact(***,*app_name*,*user_id*,*filename*,*session_id=None*,*version=None*)[¶](#google.adk.artifacts.GcsArtifactService.load_artifact) Gets an artifact from the artifact service storage.

The artifact is a file identified by the app name, user ID, session ID, and filename.

- Return type:
`Optional`

[`Part`

]- Parameters:
**app_name**– The app name.**user_id**– The user ID.**filename**– The filename of the artifact.**session_id**– The session ID. If None, load the user-scoped artifact.**version**– The version of the artifact. If None, the latest version will be returned.

- Returns:
The artifact or None if not found.


-
*async*save_artifact(***,*app_name*,*user_id*,*filename*,*artifact*,*session_id=None*,*custom_metadata=None*)[¶](#google.adk.artifacts.GcsArtifactService.save_artifact) Saves an artifact to the artifact service storage.

The artifact is a file identified by the app name, user ID, session ID, and filename. After saving the artifact, a revision ID is returned to identify the artifact version.

- Return type:
`int`

- Parameters:
**app_name**– The app name.**user_id**– The user ID.**filename**– The filename of the artifact.**artifact**– The artifact to save. If the artifact consists of file_data, the artifact service assumes its content has been uploaded separately, and this method will associate the file_data with the artifact if necessary.**session_id**– The session ID. If None, the artifact is user-scoped.**custom_metadata**– custom metadata to associate with the artifact.

- Returns:
The revision ID. The first version of the artifact has a revision ID of 0. This is incremented by 1 after each successful save.


-
*pydantic model*google.adk.artifacts.InMemoryArtifactService[¶](#google.adk.artifacts.InMemoryArtifactService) Bases:

,`BaseArtifactService`

`BaseModel`

An in-memory implementation of the artifact service.

It is not suitable for multi-threaded production environments. Use it for testing and development only.

## Show JSON schema

{ "title": "InMemoryArtifactService", "description": "An in-memory implementation of the artifact service.\n\nIt is not suitable for multi-threaded production environments. Use it for\ntesting and development only.", "type": "object", "properties": { "artifacts": { "additionalProperties": { "items": { "$ref": "#/$defs/_ArtifactEntry" }, "type": "array" }, "title": "Artifacts", "type": "object" } }, "$defs": { "ArtifactVersion": { "description": "Metadata describing a specific version of an artifact.", "properties": { "version": { "description": "Monotonically increasing identifier for the artifact version.", "title": "Version", "type": "integer" }, "canonicalUri": { "description": "Canonical URI referencing the persisted artifact payload.", "title": "Canonicaluri", "type": "string" }, "customMetadata": { "additionalProperties": true, "description": "Optional user-supplied metadata stored with the artifact.", "title": "Custommetadata", "type": "object" }, "createTime": { "description": "Unix timestamp (seconds) when the version record was created.", "title": "Createtime", "type": "number" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "MIME type when the artifact payload is stored as binary data.", "title": "Mimetype" } }, "required": [ "version", "canonicalUri" ], "title": "ArtifactVersion", "type": "object" }, "Blob": { "additionalProperties": false, "description": "Content blob.", "properties": { "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Raw bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob. Used to provide a label or filename to distinguish blobs. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "Blob", "type": "object" }, "CodeExecutionResult": { "additionalProperties": false, "description": "Result of executing the [ExecutableCode].\n\nOnly generated when using the [CodeExecution] tool, and always follows a\n`part` containing the [ExecutableCode].", "properties": { "outcome": { "anyOf": [ { "$ref": "#/$defs/Outcome" }, { "type": "null" } ], "default": null, "description": "Required. Outcome of the code execution." }, "output": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Contains stdout when code execution is successful, stderr or other description otherwise.", "title": "Output" } }, "title": "CodeExecutionResult", "type": "object" }, "ExecutableCode": { "additionalProperties": false, "description": "Code generated by the model that is meant to be executed, and the result returned to the model.\n\nGenerated when using the [CodeExecution] tool, in which the code will be\nautomatically executed, and a corresponding [CodeExecutionResult] will also be\ngenerated.", "properties": { "code": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The code to be executed.", "title": "Code" }, "language": { "anyOf": [ { "$ref": "#/$defs/Language" }, { "type": "null" } ], "default": null, "description": "Required. Programming language of the `code`." } }, "title": "ExecutableCode", "type": "object" }, "FileData": { "additionalProperties": false, "description": "URI based data.", "properties": { "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file data. Used to provide a label or filename to distinguish file datas. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "FileData", "type": "object" }, "FunctionCall": { "additionalProperties": false, "description": "A function call.", "properties": { "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The unique id of the function call. If populated, the client to execute the\n `function_call` and return the response with the matching `id`.", "title": "Id" }, "args": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Optional. The function parameters and values in JSON object format. See [FunctionDeclaration.parameters] for parameter details.", "title": "Args" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The name of the function to call. Matches [FunctionDeclaration.name].", "title": "Name" }, "partialArgs": { "anyOf": [ { "items": { "$ref": "#/$defs/PartialArg" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. The partial argument value of the function call. If provided, represents the arguments/fields that are streamed incrementally. This field is not supported in Gemini API.", "title": "Partialargs" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is the last part of the FunctionCall. If true, another partial message for the current FunctionCall is expected to follow. This field is not supported in Gemini API.", "title": "Willcontinue" } }, "title": "FunctionCall", "type": "object" }, "FunctionResponse": { "additionalProperties": false, "description": "A function response.", "properties": { "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Signals that function call continues, and more responses will be returned, turning the function call into a generator. Is only applicable to NON_BLOCKING function calls (see FunctionDeclaration.behavior for details), ignored otherwise. If false, the default, future responses will not be considered. Is only applicable to NON_BLOCKING function calls, is ignored otherwise. If set to false, future responses will not be considered. It is allowed to return empty `response` with `will_continue=False` to signal that the function call is finished.", "title": "Willcontinue" }, "scheduling": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseScheduling" }, { "type": "null" } ], "default": null, "description": "Specifies how the response should be scheduled in the conversation. Only applicable to NON_BLOCKING function calls, is ignored otherwise. Defaults to WHEN_IDLE." }, "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/FunctionResponsePart" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a function response. Each part may\n have a different IANA MIME type.", "title": "Parts" }, "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The id of the function call this response is for. Populated by the client to match the corresponding function call `id`.", "title": "Id" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The name of the function to call. Matches [FunctionDeclaration.name] and [FunctionCall.name].", "title": "Name" }, "response": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Required. The function response in JSON object format. Use \"output\" key to specify function output and \"error\" key to specify error details (if any). If \"output\" and \"error\" keys are not specified, then whole \"response\" is treated as function output.", "title": "Response" } }, "title": "FunctionResponse", "type": "object" }, "FunctionResponseBlob": { "additionalProperties": false, "description": "Raw media bytes for function response.\n\nText should not be sent as raw bytes, use the FunctionResponse.response\nfield.", "properties": { "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Inline media bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob.\n Used to provide a label or filename to distinguish blobs.", "title": "Displayname" } }, "title": "FunctionResponseBlob", "type": "object" }, "FunctionResponseFileData": { "additionalProperties": false, "description": "URI based data for function response.", "properties": { "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file.\n Used to provide a label or filename to distinguish files.", "title": "Displayname" } }, "title": "FunctionResponseFileData", "type": "object" }, "FunctionResponsePart": { "additionalProperties": false, "description": "A datatype containing media that is part of a `FunctionResponse` message.\n\nA `FunctionResponsePart` consists of data which has an associated datatype. A\n`FunctionResponsePart` can only contain one of the accepted types in\n`FunctionResponsePart.data`.\n\nA `FunctionResponsePart` must have a fixed IANA MIME type identifying the\ntype and subtype of the media if the `inline_data` field is filled with raw\nbytes.", "properties": { "inlineData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseBlob" }, { "type": "null" } ], "default": null, "description": "Optional. Inline media bytes." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseFileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." } }, "title": "FunctionResponsePart", "type": "object" }, "FunctionResponseScheduling": { "description": "Specifies how the response should be scheduled in the conversation.", "enum": [ "SCHEDULING_UNSPECIFIED", "SILENT", "WHEN_IDLE", "INTERRUPT" ], "title": "FunctionResponseScheduling", "type": "string" }, "Language": { "description": "Programming language of the `code`.", "enum": [ "LANGUAGE_UNSPECIFIED", "PYTHON" ], "title": "Language", "type": "string" }, "Outcome": { "description": "Outcome of the code execution.", "enum": [ "OUTCOME_UNSPECIFIED", "OUTCOME_OK", "OUTCOME_FAILED", "OUTCOME_DEADLINE_EXCEEDED" ], "title": "Outcome", "type": "string" }, "Part": { "additionalProperties": false, "description": "A datatype containing media content.\n\nExactly one field within a Part should be set, representing the specific type\nof content being conveyed. Using multiple fields within the same `Part`\ninstance is considered invalid.", "properties": { "mediaResolution": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolution" }, { "type": "null" } ], "default": null, "description": "Media resolution for the input media.\n " }, "codeExecutionResult": { "anyOf": [ { "$ref": "#/$defs/CodeExecutionResult" }, { "type": "null" } ], "default": null, "description": "Optional. Result of executing the [ExecutableCode]." }, "executableCode": { "anyOf": [ { "$ref": "#/$defs/ExecutableCode" }, { "type": "null" } ], "default": null, "description": "Optional. Code generated by the model that is meant to be executed." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." }, "functionCall": { "anyOf": [ { "$ref": "#/$defs/FunctionCall" }, { "type": "null" } ], "default": null, "description": "Optional. A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] with the parameters and their values." }, "functionResponse": { "anyOf": [ { "$ref": "#/$defs/FunctionResponse" }, { "type": "null" } ], "default": null, "description": "Optional. The result output of a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function call. It is used as context to the model." }, "inlineData": { "anyOf": [ { "$ref": "#/$defs/Blob" }, { "type": "null" } ], "default": null, "description": "Optional. Inlined bytes data." }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Text part (can be code).", "title": "Text" }, "thought": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Indicates if the part is thought from the model.", "title": "Thought" }, "thoughtSignature": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. An opaque signature for the thought so it can be reused in subsequent requests.", "title": "Thoughtsignature" }, "videoMetadata": { "anyOf": [ { "$ref": "#/$defs/VideoMetadata" }, { "type": "null" } ], "default": null, "description": "Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data." } }, "title": "Part", "type": "object" }, "PartMediaResolution": { "additionalProperties": false, "description": "Media resolution for the input media.", "properties": { "level": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolutionLevel" }, { "type": "null" } ], "default": null, "description": "The tokenization quality used for given media.\n " }, "numTokens": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Specifies the required sequence length for media tokenization.\n ", "title": "Numtokens" } }, "title": "PartMediaResolution", "type": "object" }, "PartMediaResolutionLevel": { "description": "The tokenization quality used for given media.", "enum": [ "MEDIA_RESOLUTION_UNSPECIFIED", "MEDIA_RESOLUTION_LOW", "MEDIA_RESOLUTION_MEDIUM", "MEDIA_RESOLUTION_HIGH", "MEDIA_RESOLUTION_ULTRA_HIGH" ], "title": "PartMediaResolutionLevel", "type": "string" }, "PartialArg": { "additionalProperties": false, "description": "Partial argument value of the function call.\n\nThis data type is not supported in Gemini API.", "properties": { "nullValue": { "anyOf": [ { "const": "NULL_VALUE", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a null value.", "title": "Nullvalue" }, "numberValue": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a double value.", "title": "Numbervalue" }, "stringValue": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a string value.", "title": "Stringvalue" }, "boolValue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a boolean value.", "title": "Boolvalue" }, "jsonPath": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. A JSON Path (RFC 9535) to the argument being streamed. https://datatracker.ietf.org/doc/html/rfc9535. e.g. \"$.foo.bar[0].data\".", "title": "Jsonpath" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is not the last part of the same json_path. If true, another PartialArg message for the current json_path is expected to follow.", "title": "Willcontinue" } }, "title": "PartialArg", "type": "object" }, "VideoMetadata": { "additionalProperties": false, "description": "Metadata describes the input video content.", "properties": { "endOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The end offset of the video.", "title": "Endoffset" }, "fps": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. The frame rate of the video sent to the model. If not specified, the default value will be 1.0. The fps range is (0.0, 24.0].", "title": "Fps" }, "startOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The start offset of the video.", "title": "Startoffset" } }, "title": "VideoMetadata", "type": "object" }, "_ArtifactEntry": { "properties": { "data": { "$ref": "#/$defs/Part" }, "artifact_version": { "$ref": "#/$defs/ArtifactVersion" } }, "required": [ "data", "artifact_version" ], "title": "_ArtifactEntry", "type": "object" } } }

- Fields:
`artifacts (dict[str, list[google.adk.artifacts.in_memory_artifact_service._ArtifactEntry]])`


-
*field*artifacts*: dict[str, list[_ArtifactEntry]]**[Optional]*[¶](#google.adk.artifacts.InMemoryArtifactService.artifacts)

-
*async*delete_artifact(***,*app_name*,*user_id*,*filename*,*session_id=None*)[¶](#google.adk.artifacts.InMemoryArtifactService.delete_artifact) Deletes an artifact.

- Return type:
`None`

- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**filename**– The name of the artifact file.**session_id**– The ID of the session. If None, delete the user-scoped artifact.


-
*async*get_artifact_version(***,*app_name*,*user_id*,*filename*,*session_id=None*,*version=None*)[¶](#google.adk.artifacts.InMemoryArtifactService.get_artifact_version) Gets the metadata for a specific version of an artifact.

- Return type:
`Optional`

[`ArtifactVersion`

]- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**filename**– The name of the artifact file.**session_id**– The ID of the session. If None, the artifact will be fetched from the user-scoped artifacts. Otherwise, it will be fetched from the specified session.**version**– The version number of the artifact to retrieve. If None, the latest version will be returned.

- Returns:
An ArtifactVersion object containing the metadata of the specified artifact version, or None if the artifact version is not found.


-
*async*list_artifact_keys(***,*app_name*,*user_id*,*session_id=None*)[¶](#google.adk.artifacts.InMemoryArtifactService.list_artifact_keys) Lists all the artifact filenames within a session.

- Return type:
`list`

[`str`

]- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**session_id**– The ID of the session.

- Returns:
A list of artifact filenames. If session_id is provided, returns both session-scoped and user-scoped artifact filenames. If session_id is None, returns user-scoped artifact filenames.


-
*async*list_artifact_versions(***,*app_name*,*user_id*,*filename*,*session_id=None*)[¶](#google.adk.artifacts.InMemoryArtifactService.list_artifact_versions) Lists all versions and their metadata for a specific artifact.

- Return type:
`list`

[`ArtifactVersion`

]- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**filename**– The name of the artifact file.**session_id**– The ID of the session. If None, lists versions of the user-scoped artifact. Otherwise, lists versions of the artifact within the specified session.

- Returns:
A list of ArtifactVersion objects, each representing a version of the artifact and its associated metadata.


-
*async*list_versions(***,*app_name*,*user_id*,*filename*,*session_id=None*)[¶](#google.adk.artifacts.InMemoryArtifactService.list_versions) Lists all versions of an artifact.

- Return type:
`list`

[`int`

]- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**filename**– The name of the artifact file.**session_id**– The ID of the session. If None, only list the user-scoped artifacts versions.

- Returns:
A list of all available versions of the artifact.


-
*async*load_artifact(***,*app_name*,*user_id*,*filename*,*session_id=None*,*version=None*)[¶](#google.adk.artifacts.InMemoryArtifactService.load_artifact) Gets an artifact from the artifact service storage.

The artifact is a file identified by the app name, user ID, session ID, and filename.

- Return type:
`Optional`

[`Part`

]- Parameters:
**app_name**– The app name.**user_id**– The user ID.**filename**– The filename of the artifact.**session_id**– The session ID. If None, load the user-scoped artifact.**version**– The version of the artifact. If None, the latest version will be returned.

- Returns:
The artifact or None if not found.


-
*async*save_artifact(***,*app_name*,*user_id*,*filename*,*artifact*,*session_id=None*,*custom_metadata=None*)[¶](#google.adk.artifacts.InMemoryArtifactService.save_artifact) Saves an artifact to the artifact service storage.

The artifact is a file identified by the app name, user ID, session ID, and filename. After saving the artifact, a revision ID is returned to identify the artifact version.

- Return type:
`int`

- Parameters:
**app_name**– The app name.**user_id**– The user ID.**filename**– The filename of the artifact.**artifact**– The artifact to save. If the artifact consists of file_data, the artifact service assumes its content has been uploaded separately, and this method will associate the file_data with the artifact if necessary.**session_id**– The session ID. If None, the artifact is user-scoped.**custom_metadata**– custom metadata to associate with the artifact.

- Returns:
The revision ID. The first version of the artifact has a revision ID of 0. This is incremented by 1 after each successful save.


# google.adk.apps package[¶](#module-google.adk.apps)

-
*pydantic model*google.adk.apps.App[¶](#google.adk.apps.App) Bases:

`BaseModel`

Represents an LLM-backed agentic application.

An App is the top-level container for an agentic system powered by LLMs. It manages a root agent (root_agent), which serves as the root of an agent tree, enabling coordination and communication across all agents in the hierarchy. The plugins are application-wide components that provide shared capabilities and services to the entire system.

## Show JSON schema

{ "title": "App", "type": "object", "properties": { "name": { "title": "Name", "type": "string" }, "root_agent": { "$ref": "#/$defs/BaseAgent" }, "plugins": { "default": null, "title": "Plugins" }, "events_compaction_config": { "default": null, "title": "Events Compaction Config" }, "context_cache_config": { "anyOf": [ { "$ref": "#/$defs/ContextCacheConfig" }, { "type": "null" } ], "default": null }, "resumability_config": { "anyOf": [ { "$ref": "#/$defs/ResumabilityConfig" }, { "type": "null" } ], "default": null } }, "$defs": { "BaseAgent": { "additionalProperties": false, "description": "Base class for all agents in Agent Development Kit.", "properties": { "name": { "title": "Name", "type": "string" }, "description": { "default": "", "title": "Description", "type": "string" }, "parent_agent": { "anyOf": [ { "$ref": "#/$defs/BaseAgent" }, { "type": "null" } ], "default": null }, "sub_agents": { "items": { "$ref": "#/$defs/BaseAgent" }, "title": "Sub Agents", "type": "array" }, "before_agent_callback": { "default": null, "title": "Before Agent Callback", "type": "null" }, "after_agent_callback": { "default": null, "title": "After Agent Callback", "type": "null" } }, "required": [ "name" ], "title": "BaseAgent", "type": "object" }, "ContextCacheConfig": { "additionalProperties": false, "description": "Configuration for context caching across all agents in an app.\n\nThis configuration enables and controls context caching behavior for\nall LLM agents in an app. When this config is present on an app, context\ncaching is enabled for all agents. When absent (None), context caching\nis disabled.\n\nContext caching can significantly reduce costs and improve response times\nby reusing previously processed context across multiple requests.\n\nAttributes:\n cache_intervals: Maximum number of invocations to reuse the same cache before refreshing it\n ttl_seconds: Time-to-live for cache in seconds\n min_tokens: Minimum tokens required to enable caching", "properties": { "cache_intervals": { "default": 10, "description": "Maximum number of invocations to reuse the same cache before refreshing it", "maximum": 100, "minimum": 1, "title": "Cache Intervals", "type": "integer" }, "ttl_seconds": { "default": 1800, "description": "Time-to-live for cache in seconds", "exclusiveMinimum": 0, "title": "Ttl Seconds", "type": "integer" }, "min_tokens": { "default": 0, "description": "Minimum estimated request tokens required to enable caching. This compares against the estimated total tokens of the request (system instruction + tools + contents). Context cache storage may have cost. Set higher to avoid caching small requests where overhead may exceed benefits.", "minimum": 0, "title": "Min Tokens", "type": "integer" } }, "title": "ContextCacheConfig", "type": "object" }, "ResumabilityConfig": { "description": "The config of the resumability for an application.\n\nThe \"resumability\" in ADK refers to the ability to:\n1. pause an invocation upon a long running function call.\n2. resume an invocation from the last event, if it's paused or failed midway\nthrough.\n\nNote: ADK resumes the invocation in a best-effort manner:\n1. Tool call to resume needs to be idempotent because we only guarantee\nan at-least-once behavior once resumed.\n2. Any temporary / in-memory state will be lost upon resumption.", "properties": { "is_resumable": { "default": false, "title": "Is Resumable", "type": "boolean" } }, "title": "ResumabilityConfig", "type": "object" } }, "additionalProperties": false, "required": [ "name", "root_agent" ] }

- Fields:
`context_cache_config (google.adk.agents.context_cache_config.ContextCacheConfig | None)`

`events_compaction_config (google.adk.apps.app.EventsCompactionConfig | None)`

`name (str)`

`plugins (list[google.adk.plugins.base_plugin.BasePlugin])`

`resumability_config (google.adk.apps.app.ResumabilityConfig | None)`

`root_agent (google.adk.agents.base_agent.BaseAgent)`


- Validators:
`_validate_name`

»`all fields`


-
*field*context_cache_config*: ContextCacheConfig | None**= None*[¶](#google.adk.apps.App.context_cache_config) Context cache configuration that applies to all LLM agents in the app.

- Validated by:
`_validate_name`


-
*field*events_compaction_config*: EventsCompactionConfig | None**= None*[¶](#google.adk.apps.App.events_compaction_config) The config of event compaction for the application.

- Validated by:
`_validate_name`


-
*field*name*: str**[Required]*[¶](#google.adk.apps.App.name) The name of the application.

- Validated by:
`_validate_name`


-
*field*plugins*: list[*[BasePlugin](#google.adk.plugins.BasePlugin)]*[Optional]*[¶](#google.adk.apps.App.plugins) The plugins in the application.

- Validated by:
`_validate_name`


-
*field*resumability_config*:*[ResumabilityConfig](#google.adk.apps.ResumabilityConfig)| None*= None*[¶](#google.adk.apps.App.resumability_config) The config of the resumability for the application. If configured, will be applied to all agents in the app.

- Validated by:
`_validate_name`


-
*pydantic model*google.adk.apps.ResumabilityConfig[¶](#google.adk.apps.ResumabilityConfig) Bases:

`BaseModel`

The config of the resumability for an application.

The “resumability” in ADK refers to the ability to: 1. pause an invocation upon a long running function call. 2. resume an invocation from the last event, if it’s paused or failed midway through.

Note: ADK resumes the invocation in a best-effort manner: 1. Tool call to resume needs to be idempotent because we only guarantee an at-least-once behavior once resumed. 2. Any temporary / in-memory state will be lost upon resumption.

## Show JSON schema

{ "title": "ResumabilityConfig", "description": "The config of the resumability for an application.\n\nThe \"resumability\" in ADK refers to the ability to:\n1. pause an invocation upon a long running function call.\n2. resume an invocation from the last event, if it's paused or failed midway\nthrough.\n\nNote: ADK resumes the invocation in a best-effort manner:\n1. Tool call to resume needs to be idempotent because we only guarantee\nan at-least-once behavior once resumed.\n2. Any temporary / in-memory state will be lost upon resumption.", "type": "object", "properties": { "is_resumable": { "default": false, "title": "Is Resumable", "type": "boolean" } } }

- Fields:
`is_resumable (bool)`


-
*field*is_resumable*: bool**= False*[¶](#google.adk.apps.ResumabilityConfig.is_resumable) Whether the app supports agent resumption. If enabled, the feature will be enabled for all agents in the app.


# google.adk.auth module[¶](#module-google.adk.auth)

# google.adk.cli module[¶](#module-google.adk.cli)

# google.adk.code_executors module[¶](#module-google.adk.code_executors)

-
*pydantic model*google.adk.code_executors.BaseCodeExecutor[¶](#google.adk.code_executors.BaseCodeExecutor) Bases:

`BaseModel`

Abstract base class for all code executors.

The code executor allows the agent to execute code blocks from model responses and incorporate the execution results into the final response.

-
optimize_data_file
[¶](#google.adk.code_executors.BaseCodeExecutor.optimize_data_file) If true, extract and process data files from the model request and attach them to the code executor. Supported data file MimeTypes are [text/csv]. Default to False.


-
stateful
[¶](#google.adk.code_executors.BaseCodeExecutor.stateful) Whether the code executor is stateful. Default to False.


-
error_retry_attempts
[¶](#google.adk.code_executors.BaseCodeExecutor.error_retry_attempts) The number of attempts to retry on consecutive code execution errors. Default to 2.


-
code_block_delimiters
[¶](#google.adk.code_executors.BaseCodeExecutor.code_block_delimiters) The list of the enclosing delimiters to identify the code blocks.


-
execution_result_delimiters
[¶](#google.adk.code_executors.BaseCodeExecutor.execution_result_delimiters) The delimiters to format the code execution result.


## Show JSON schema

{ "title": "BaseCodeExecutor", "description": "Abstract base class for all code executors.\n\nThe code executor allows the agent to execute code blocks from model responses\nand incorporate the execution results into the final response.\n\nAttributes:\n optimize_data_file: If true, extract and process data files from the model\n request and attach them to the code executor. Supported data file\n MimeTypes are [text/csv]. Default to False.\n stateful: Whether the code executor is stateful. Default to False.\n error_retry_attempts: The number of attempts to retry on consecutive code\n execution errors. Default to 2.\n code_block_delimiters: The list of the enclosing delimiters to identify the\n code blocks.\n execution_result_delimiters: The delimiters to format the code execution\n result.", "type": "object", "properties": { "optimize_data_file": { "default": false, "title": "Optimize Data File", "type": "boolean" }, "stateful": { "default": false, "title": "Stateful", "type": "boolean" }, "error_retry_attempts": { "default": 2, "title": "Error Retry Attempts", "type": "integer" }, "code_block_delimiters": { "default": [ [ "```tool_code\n", "\n```" ], [ "```python\n", "\n```" ] ], "items": { "maxItems": 2, "minItems": 2, "prefixItems": [ { "type": "string" }, { "type": "string" } ], "type": "array" }, "title": "Code Block Delimiters", "type": "array" }, "execution_result_delimiters": { "default": [ "```tool_output\n", "\n```" ], "maxItems": 2, "minItems": 2, "prefixItems": [ { "type": "string" }, { "type": "string" } ], "title": "Execution Result Delimiters", "type": "array" } } }

- Fields:
`code_block_delimiters (List[tuple[str, str]])`

`error_retry_attempts (int)`

`execution_result_delimiters (tuple[str, str])`

`optimize_data_file (bool)`

`stateful (bool)`


-
*field*code_block_delimiters*: List[tuple[str, str]]**= [('```tool_code\n', '\n```'), ('```python\n', '\n```')]*[¶](#id16) The list of the enclosing delimiters to identify the code blocks.

For example, the delimiter (’

``python\n', '\n``

’) can be used to identify code blocks with the following format:```python print("hello") ```


-
*field*error_retry_attempts*: int**= 2*[¶](#id17) The number of attempts to retry on consecutive code execution errors. Default to 2.


-
*field*execution_result_delimiters*: tuple[str, str]**= ('```tool_output\n', '\n```')*[¶](#id18) The delimiters to format the code execution result.


-
*field*optimize_data_file*: bool**= False*[¶](#id19) If true, extract and process data files from the model request and attach them to the code executor.

Supported data file MimeTypes are [text/csv]. Default to False.


-
*field*stateful*: bool**= False*[¶](#id20) Whether the code executor is stateful. Default to False.


-
*abstractmethod*execute_code(*invocation_context*,*code_execution_input*)[¶](#google.adk.code_executors.BaseCodeExecutor.execute_code) Executes code and return the code execution result.

- Return type:
`CodeExecutionResult`

- Parameters:
**invocation_context**– The invocation context of the code execution.**code_execution_input**– The code execution input.

- Returns:
The code execution result.


-
optimize_data_file

-
*pydantic model*google.adk.code_executors.BuiltInCodeExecutor[¶](#google.adk.code_executors.BuiltInCodeExecutor) Bases:

`BaseCodeExecutor`

A code executor that uses the Model’s built-in code executor.

Currently only supports Gemini 2.0+ models, but will be expanded to other models.

## Show JSON schema

{ "title": "BuiltInCodeExecutor", "description": "A code executor that uses the Model's built-in code executor.\n\nCurrently only supports Gemini 2.0+ models, but will be expanded to\nother models.", "type": "object", "properties": { "optimize_data_file": { "default": false, "title": "Optimize Data File", "type": "boolean" }, "stateful": { "default": false, "title": "Stateful", "type": "boolean" }, "error_retry_attempts": { "default": 2, "title": "Error Retry Attempts", "type": "integer" }, "code_block_delimiters": { "default": [ [ "```tool_code\n", "\n```" ], [ "```python\n", "\n```" ] ], "items": { "maxItems": 2, "minItems": 2, "prefixItems": [ { "type": "string" }, { "type": "string" } ], "type": "array" }, "title": "Code Block Delimiters", "type": "array" }, "execution_result_delimiters": { "default": [ "```tool_output\n", "\n```" ], "maxItems": 2, "minItems": 2, "prefixItems": [ { "type": "string" }, { "type": "string" } ], "title": "Execution Result Delimiters", "type": "array" } } }

- Fields:

-
execute_code(
*invocation_context*,*code_execution_input*)[¶](#google.adk.code_executors.BuiltInCodeExecutor.execute_code) Executes code and return the code execution result.

- Return type:
`CodeExecutionResult`

- Parameters:
**invocation_context**– The invocation context of the code execution.**code_execution_input**– The code execution input.

- Returns:
The code execution result.


-
process_llm_request(
*llm_request*)[¶](#google.adk.code_executors.BuiltInCodeExecutor.process_llm_request) Pre-process the LLM request for Gemini 2.0+ models to use the code execution tool.

- Return type:
`None`


-
*class*google.adk.code_executors.CodeExecutorContext(*session_state*)[¶](#google.adk.code_executors.CodeExecutorContext) Bases:

`object`

The persistent context used to configure the code executor.

Initializes the code executor context.

- Parameters:
**session_state**– The session state to get the code executor context from.

-
add_input_files(
*input_files*)[¶](#google.adk.code_executors.CodeExecutorContext.add_input_files) Adds the input files to the code executor context.

- Parameters:
**input_files**– The input files to add to the code executor context.


-
add_processed_file_names(
*file_names*)[¶](#google.adk.code_executors.CodeExecutorContext.add_processed_file_names) Adds the processed file name to the session state.

- Parameters:
**file_names**– The processed file names to add to the session state.


-
clear_input_files()
[¶](#google.adk.code_executors.CodeExecutorContext.clear_input_files) Removes the input files and processed file names to the code executor context.


-
get_error_count(
*invocation_id*)[¶](#google.adk.code_executors.CodeExecutorContext.get_error_count) Gets the error count from the session state.

- Return type:
`int`

- Parameters:
**invocation_id**– The invocation ID to get the error count for.- Returns:
The error count for the given invocation ID.


-
get_execution_id()
[¶](#google.adk.code_executors.CodeExecutorContext.get_execution_id) Gets the session ID for the code executor.

- Return type:
`Optional`

[`str`

]- Returns:
The session ID for the code executor context.


-
get_input_files()
[¶](#google.adk.code_executors.CodeExecutorContext.get_input_files) Gets the code executor input file names from the session state.

- Return type:
`list`

[`File`

]- Returns:
A list of input files in the code executor context.


-
get_processed_file_names()
[¶](#google.adk.code_executors.CodeExecutorContext.get_processed_file_names) Gets the processed file names from the session state.

- Return type:
`list`

[`str`

]- Returns:
A list of processed file names in the code executor context.


-
get_state_delta()
[¶](#google.adk.code_executors.CodeExecutorContext.get_state_delta) Gets the state delta to update in the persistent session state.

- Return type:
`dict`

[`str`

,`Any`

]- Returns:
The state delta to update in the persistent session state.


-
increment_error_count(
*invocation_id*)[¶](#google.adk.code_executors.CodeExecutorContext.increment_error_count) Increments the error count from the session state.

- Parameters:
**invocation_id**– The invocation ID to increment the error count for.


-
reset_error_count(
*invocation_id*)[¶](#google.adk.code_executors.CodeExecutorContext.reset_error_count) Resets the error count from the session state.

- Parameters:
**invocation_id**– The invocation ID to reset the error count for.


-
set_execution_id(
*session_id*)[¶](#google.adk.code_executors.CodeExecutorContext.set_execution_id) Sets the session ID for the code executor.

- Parameters:
**session_id**– The session ID for the code executor.


-
update_code_execution_result(
*invocation_id*,*code*,*result_stdout*,*result_stderr*)[¶](#google.adk.code_executors.CodeExecutorContext.update_code_execution_result) Updates the code execution result.

- Parameters:
**invocation_id**– The invocation ID to update the code execution result for.**code**– The code to execute.**result_stdout**– The standard output of the code execution.**result_stderr**– The standard error of the code execution.


-
*pydantic model*google.adk.code_executors.UnsafeLocalCodeExecutor[¶](#google.adk.code_executors.UnsafeLocalCodeExecutor) Bases:

`BaseCodeExecutor`

A code executor that unsafely execute code in the current local context.

Initializes the UnsafeLocalCodeExecutor.

## Show JSON schema

{ "title": "UnsafeLocalCodeExecutor", "description": "A code executor that unsafely execute code in the current local context.", "type": "object", "properties": { "optimize_data_file": { "default": false, "title": "Optimize Data File", "type": "boolean" }, "stateful": { "default": false, "title": "Stateful", "type": "boolean" }, "error_retry_attempts": { "default": 2, "title": "Error Retry Attempts", "type": "integer" }, "code_block_delimiters": { "default": [ [ "```tool_code\n", "\n```" ], [ "```python\n", "\n```" ] ], "items": { "maxItems": 2, "minItems": 2, "prefixItems": [ { "type": "string" }, { "type": "string" } ], "type": "array" }, "title": "Code Block Delimiters", "type": "array" }, "execution_result_delimiters": { "default": [ "```tool_output\n", "\n```" ], "maxItems": 2, "minItems": 2, "prefixItems": [ { "type": "string" }, { "type": "string" } ], "title": "Execution Result Delimiters", "type": "array" } } }

- Fields:
`optimize_data_file (bool)`

`stateful (bool)`


-
*field*optimize_data_file*: bool**= False*[¶](#google.adk.code_executors.UnsafeLocalCodeExecutor.optimize_data_file) If true, extract and process data files from the model request and attach them to the code executor.

Supported data file MimeTypes are [text/csv]. Default to False.


-
*field*stateful*: bool**= False*[¶](#google.adk.code_executors.UnsafeLocalCodeExecutor.stateful) Whether the code executor is stateful. Default to False.


-
execute_code(
*invocation_context*,*code_execution_input*)[¶](#google.adk.code_executors.UnsafeLocalCodeExecutor.execute_code) Executes code and return the code execution result.

- Return type:
`CodeExecutionResult`

- Parameters:
**invocation_context**– The invocation context of the code execution.**code_execution_input**– The code execution input.

- Returns:
The code execution result.


# google.adk.errors module[¶](#module-google.adk.errors)

# google.adk.evaluation module[¶](#module-google.adk.evaluation)

-
*class*google.adk.evaluation.AgentEvaluator[¶](#google.adk.evaluation.AgentEvaluator) Bases:

`object`

An evaluator for Agents, mainly intended for helping with test cases.

-
*async static*evaluate(*agent_module*,*eval_dataset_file_path_or_dir*,*num_runs=2*,*agent_name=None*,*initial_session_file=None*,*print_detailed_results=True*)[¶](#google.adk.evaluation.AgentEvaluator.evaluate) Evaluates an Agent given eval data.

- Parameters:
**agent_module**– The path to python module that contains the definition of the agent. There is convention in place here, where the code is going to look for ‘root_agent’ or ‘get_agent_async’ in the loaded module.**eval_dataset_file_path_or_dir**– The eval data set. This can be either a string representing full path to the file containing eval dataset, or a directory that is recursively explored for all files that have a .test.json suffix.**num_runs**– Number of times all entries in the eval dataset should be assessed.**agent_name**– The name of the agent.**initial_session_file**– File that contains initial session state that is needed by all the evals in the eval dataset.**print_detailed_results**– Whether to print detailed results for each metric evaluation.


-
*async static*evaluate_eval_set(*agent_module*,*eval_set*,*criteria=None*,*eval_config=None*,*num_runs=2*,*agent_name=None*,*print_detailed_results=True*)[¶](#google.adk.evaluation.AgentEvaluator.evaluate_eval_set) Evaluates an agent using the given EvalSet.

- Parameters:
**agent_module**– The path to python module that contains the definition of the agent. There is convention in place here, where the code is going to look for ‘root_agent’ or get_agent_async in the loaded module.**eval_set**– The eval set.**criteria**– Evaluation criteria, a dictionary of metric names to their respective thresholds. This field is deprecated.**eval_config**– The evaluation config.**num_runs**– Number of times all entries in the eval dataset should be assessed.**agent_name**– The name of the agent, if trying to evaluate something other than root agent. If left empty or none, then root agent is evaluated.**print_detailed_results**– Whether to print detailed results for each metric evaluation.


-
*static*find_config_for_test_file(*test_file*)[¶](#google.adk.evaluation.AgentEvaluator.find_config_for_test_file) Find the test_config.json file in the same folder as the test file.

- Return type:
`EvalConfig`


-
*static*migrate_eval_data_to_new_schema(*old_eval_data_file*,*new_eval_data_file*,*initial_session_file=None*)[¶](#google.adk.evaluation.AgentEvaluator.migrate_eval_data_to_new_schema) A utility for migrating eval data to new schema backed by EvalSet.


-

# google.adk.events module[¶](#module-google.adk.events)

-
*pydantic model*google.adk.events.Event[¶](#google.adk.events.Event) Bases:

`LlmResponse`

Represents an event in a conversation between agents and users.

It is used to store the content of the conversation, as well as the actions taken by the agents like function calls, etc.

## Show JSON schema

{ "title": "Event", "description": "Represents an event in a conversation between agents and users.\n\nIt is used to store the content of the conversation, as well as the actions\ntaken by the agents like function calls, etc.", "type": "object", "properties": { "modelVersion": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Modelversion" }, "content": { "anyOf": [ { "$ref": "#/$defs/Content" }, { "type": "null" } ], "default": null }, "groundingMetadata": { "anyOf": [ { "$ref": "#/$defs/GroundingMetadata" }, { "type": "null" } ], "default": null }, "partial": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Partial" }, "turnComplete": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Turncomplete" }, "finishReason": { "anyOf": [ { "$ref": "#/$defs/FinishReason" }, { "type": "null" } ], "default": null }, "errorCode": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Errorcode" }, "errorMessage": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Errormessage" }, "interrupted": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Interrupted" }, "customMetadata": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "title": "Custommetadata" }, "usageMetadata": { "anyOf": [ { "$ref": "#/$defs/GenerateContentResponseUsageMetadata" }, { "type": "null" } ], "default": null }, "liveSessionResumptionUpdate": { "anyOf": [ { "$ref": "#/$defs/LiveServerSessionResumptionUpdate" }, { "type": "null" } ], "default": null }, "inputTranscription": { "anyOf": [ { "$ref": "#/$defs/Transcription" }, { "type": "null" } ], "default": null }, "outputTranscription": { "anyOf": [ { "$ref": "#/$defs/Transcription" }, { "type": "null" } ], "default": null }, "avgLogprobs": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "title": "Avglogprobs" }, "logprobsResult": { "anyOf": [ { "$ref": "#/$defs/LogprobsResult" }, { "type": "null" } ], "default": null }, "cacheMetadata": { "anyOf": [ { "$ref": "#/$defs/CacheMetadata" }, { "type": "null" } ], "default": null }, "citationMetadata": { "anyOf": [ { "$ref": "#/$defs/CitationMetadata" }, { "type": "null" } ], "default": null }, "interactionId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Interactionid" }, "invocationId": { "default": "", "title": "Invocationid", "type": "string" }, "author": { "title": "Author", "type": "string" }, "actions": { "$ref": "#/$defs/EventActions" }, "longRunningToolIds": { "anyOf": [ { "items": { "type": "string" }, "type": "array", "uniqueItems": true }, { "type": "null" } ], "default": null, "title": "Longrunningtoolids" }, "branch": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Branch" }, "id": { "default": "", "title": "Id", "type": "string" }, "timestamp": { "title": "Timestamp", "type": "number" } }, "$defs": { "APIKey": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "apiKey" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "in": { "$ref": "#/$defs/APIKeyIn" }, "name": { "title": "Name", "type": "string" } }, "required": [ "in", "name" ], "title": "APIKey", "type": "object" }, "APIKeyIn": { "enum": [ "query", "header", "cookie" ], "title": "APIKeyIn", "type": "string" }, "AuthConfig": { "additionalProperties": true, "description": "The auth config sent by tool asking client to collect auth credentials and\n\nadk and client will help to fill in the response", "properties": { "authScheme": { "anyOf": [ { "$ref": "#/$defs/APIKey" }, { "$ref": "#/$defs/HTTPBase" }, { "$ref": "#/$defs/OAuth2" }, { "$ref": "#/$defs/OpenIdConnect" }, { "$ref": "#/$defs/HTTPBearer" }, { "$ref": "#/$defs/OpenIdConnectWithConfig" } ], "title": "Authscheme" }, "rawAuthCredential": { "anyOf": [ { "$ref": "#/$defs/AuthCredential" }, { "type": "null" } ], "default": null }, "exchangedAuthCredential": { "anyOf": [ { "$ref": "#/$defs/AuthCredential" }, { "type": "null" } ], "default": null }, "credentialKey": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Credentialkey" } }, "required": [ "authScheme" ], "title": "AuthConfig", "type": "object" }, "AuthCredential": { "additionalProperties": true, "description": "Data class representing an authentication credential.\n\nTo exchange for the actual credential, please use\nCredentialExchanger.exchange_credential().\n\nExamples: API Key Auth\nAuthCredential(\n auth_type=AuthCredentialTypes.API_KEY,\n api_key=\"1234\",\n)\n\nExample: HTTP Auth\nAuthCredential(\n auth_type=AuthCredentialTypes.HTTP,\n http=HttpAuth(\n scheme=\"basic\",\n credentials=HttpCredentials(username=\"user\", password=\"password\"),\n ),\n)\n\nExample: OAuth2 Bearer Token in HTTP Header\nAuthCredential(\n auth_type=AuthCredentialTypes.HTTP,\n http=HttpAuth(\n scheme=\"bearer\",\n credentials=HttpCredentials(token=\"eyAkaknabna....\"),\n ),\n)\n\nExample: OAuth2 Auth with Authorization Code Flow\nAuthCredential(\n auth_type=AuthCredentialTypes.OAUTH2,\n oauth2=OAuth2Auth(\n client_id=\"1234\",\n client_secret=\"secret\",\n ),\n)\n\nExample: OpenID Connect Auth\nAuthCredential(\n auth_type=AuthCredentialTypes.OPEN_ID_CONNECT,\n oauth2=OAuth2Auth(\n client_id=\"1234\",\n client_secret=\"secret\",\n redirect_uri=\"https://example.com\",\n scopes=[\"scope1\", \"scope2\"],\n ),\n)\n\nExample: Auth with resource reference\nAuthCredential(\n auth_type=AuthCredentialTypes.API_KEY,\n resource_ref=\"projects/1234/locations/us-central1/resources/resource1\",\n)", "properties": { "authType": { "$ref": "#/$defs/AuthCredentialTypes" }, "resourceRef": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Resourceref" }, "apiKey": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Apikey" }, "http": { "anyOf": [ { "$ref": "#/$defs/HttpAuth" }, { "type": "null" } ], "default": null }, "serviceAccount": { "anyOf": [ { "$ref": "#/$defs/ServiceAccount" }, { "type": "null" } ], "default": null }, "oauth2": { "anyOf": [ { "$ref": "#/$defs/OAuth2Auth" }, { "type": "null" } ], "default": null } }, "required": [ "authType" ], "title": "AuthCredential", "type": "object" }, "AuthCredentialTypes": { "description": "Represents the type of authentication credential.", "enum": [ "apiKey", "http", "oauth2", "openIdConnect", "serviceAccount" ], "title": "AuthCredentialTypes", "type": "string" }, "Blob": { "additionalProperties": false, "description": "Content blob.", "properties": { "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Raw bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob. Used to provide a label or filename to distinguish blobs. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "Blob", "type": "object" }, "CacheMetadata": { "additionalProperties": false, "description": "Metadata for context cache associated with LLM responses.\n\nThis class stores cache identification, usage tracking, and lifecycle\ninformation for a particular cache instance. It can be in two states:\n\n1. Active cache state: cache_name is set, all fields populated\n2. Fingerprint-only state: cache_name is None, only fingerprint and\n contents_count are set for prefix matching\n\nToken counts (cached and total) are available in the LlmResponse.usage_metadata\nand should be accessed from there to avoid duplication.\n\nAttributes:\n cache_name: The full resource name of the cached content (e.g.,\n 'projects/123/locations/us-central1/cachedContents/456').\n None when no active cache exists (fingerprint-only state).\n expire_time: Unix timestamp when the cache expires. None when no\n active cache exists.\n fingerprint: Hash of cacheable contents (instruction + tools + contents).\n Always present for prefix matching.\n invocations_used: Number of invocations this cache has been used for.\n None when no active cache exists.\n contents_count: Number of contents. When active cache exists, this is\n the count of cached contents. When no active cache exists, this is\n the total count of contents in the request.\n created_at: Unix timestamp when the cache was created. None when\n no active cache exists.", "properties": { "cache_name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Full resource name of the cached content (None if no active cache)", "title": "Cache Name" }, "expire_time": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Unix timestamp when cache expires (None if no active cache)", "title": "Expire Time" }, "fingerprint": { "description": "Hash of cacheable contents used to detect changes", "title": "Fingerprint", "type": "string" }, "invocations_used": { "anyOf": [ { "minimum": 0, "type": "integer" }, { "type": "null" } ], "default": null, "description": "Number of invocations this cache has been used for (None if no active cache)", "title": "Invocations Used" }, "contents_count": { "description": "Number of contents (cached contents when active cache exists, total contents in request when no active cache)", "minimum": 0, "title": "Contents Count", "type": "integer" }, "created_at": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Unix timestamp when cache was created (None if no active cache)", "title": "Created At" } }, "required": [ "fingerprint", "contents_count" ], "title": "CacheMetadata", "type": "object" }, "Citation": { "additionalProperties": false, "description": "Source attributions for content.\n\nThis data type is not supported in Gemini API.", "properties": { "endIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. End index into the content.", "title": "Endindex" }, "license": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. License of the attribution.", "title": "License" }, "publicationDate": { "anyOf": [ { "$ref": "#/$defs/GoogleTypeDate" }, { "type": "null" } ], "default": null, "description": "Output only. Publication date of the attribution." }, "startIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. Start index into the content.", "title": "Startindex" }, "title": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. Title of the attribution.", "title": "Title" }, "uri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. Url reference of the attribution.", "title": "Uri" } }, "title": "Citation", "type": "object" }, "CitationMetadata": { "additionalProperties": false, "description": "Citation information when the model quotes another source.", "properties": { "citations": { "anyOf": [ { "items": { "$ref": "#/$defs/Citation" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Contains citation information when the model directly quotes, at\n length, from another source. Can include traditional websites and code\n repositories.\n ", "title": "Citations" } }, "title": "CitationMetadata", "type": "object" }, "CodeExecutionResult": { "additionalProperties": false, "description": "Result of executing the [ExecutableCode].\n\nOnly generated when using the [CodeExecution] tool, and always follows a\n`part` containing the [ExecutableCode].", "properties": { "outcome": { "anyOf": [ { "$ref": "#/$defs/Outcome" }, { "type": "null" } ], "default": null, "description": "Required. Outcome of the code execution." }, "output": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Contains stdout when code execution is successful, stderr or other description otherwise.", "title": "Output" } }, "title": "CodeExecutionResult", "type": "object" }, "Content": { "additionalProperties": false, "description": "Contains the multi-part content of a message.", "properties": { "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/Part" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a single message. Each part may have\n a different IANA MIME type.", "title": "Parts" }, "role": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The producer of the content. Must be either 'user' or 'model'. Useful to set for multi-turn conversations, otherwise can be left blank or unset.", "title": "Role" } }, "title": "Content", "type": "object" }, "EventActions": { "additionalProperties": false, "description": "Represents the actions attached to an event.", "properties": { "skipSummarization": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Skipsummarization" }, "stateDelta": { "additionalProperties": true, "title": "Statedelta", "type": "object" }, "artifactDelta": { "additionalProperties": { "type": "integer" }, "title": "Artifactdelta", "type": "object" }, "transferToAgent": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Transfertoagent" }, "escalate": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Escalate" }, "requestedAuthConfigs": { "additionalProperties": { "$ref": "#/$defs/AuthConfig" }, "title": "Requestedauthconfigs", "type": "object" }, "requestedToolConfirmations": { "additionalProperties": { "$ref": "#/$defs/ToolConfirmation" }, "title": "Requestedtoolconfirmations", "type": "object" }, "compaction": { "anyOf": [ { "$ref": "#/$defs/EventCompaction" }, { "type": "null" } ], "default": null }, "endOfAgent": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Endofagent" }, "agentState": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "title": "Agentstate" }, "rewindBeforeInvocationId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Rewindbeforeinvocationid" } }, "title": "EventActions", "type": "object" }, "EventCompaction": { "additionalProperties": false, "description": "The compaction of the events.", "properties": { "startTimestamp": { "title": "Starttimestamp", "type": "number" }, "endTimestamp": { "title": "Endtimestamp", "type": "number" }, "compactedContent": { "$ref": "#/$defs/Content" } }, "required": [ "startTimestamp", "endTimestamp", "compactedContent" ], "title": "EventCompaction", "type": "object" }, "ExecutableCode": { "additionalProperties": false, "description": "Code generated by the model that is meant to be executed, and the result returned to the model.\n\nGenerated when using the [CodeExecution] tool, in which the code will be\nautomatically executed, and a corresponding [CodeExecutionResult] will also be\ngenerated.", "properties": { "code": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The code to be executed.", "title": "Code" }, "language": { "anyOf": [ { "$ref": "#/$defs/Language" }, { "type": "null" } ], "default": null, "description": "Required. Programming language of the `code`." } }, "title": "ExecutableCode", "type": "object" }, "FileData": { "additionalProperties": false, "description": "URI based data.", "properties": { "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file data. Used to provide a label or filename to distinguish file datas. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "FileData", "type": "object" }, "FinishReason": { "description": "Output only. The reason why the model stopped generating tokens.\n\nIf empty, the model has not stopped generating the tokens.", "enum": [ "FINISH_REASON_UNSPECIFIED", "STOP", "MAX_TOKENS", "SAFETY", "RECITATION", "LANGUAGE", "OTHER", "BLOCKLIST", "PROHIBITED_CONTENT", "SPII", "MALFORMED_FUNCTION_CALL", "IMAGE_SAFETY", "UNEXPECTED_TOOL_CALL", "IMAGE_PROHIBITED_CONTENT", "NO_IMAGE", "IMAGE_RECITATION", "IMAGE_OTHER" ], "title": "FinishReason", "type": "string" }, "FunctionCall": { "additionalProperties": false, "description": "A function call.", "properties": { "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The unique id of the function call. If populated, the client to execute the\n `function_call` and return the response with the matching `id`.", "title": "Id" }, "args": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Optional. The function parameters and values in JSON object format. See [FunctionDeclaration.parameters] for parameter details.", "title": "Args" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The name of the function to call. Matches [FunctionDeclaration.name].", "title": "Name" }, "partialArgs": { "anyOf": [ { "items": { "$ref": "#/$defs/PartialArg" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. The partial argument value of the function call. If provided, represents the arguments/fields that are streamed incrementally. This field is not supported in Gemini API.", "title": "Partialargs" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is the last part of the FunctionCall. If true, another partial message for the current FunctionCall is expected to follow. This field is not supported in Gemini API.", "title": "Willcontinue" } }, "title": "FunctionCall", "type": "object" }, "FunctionResponse": { "additionalProperties": false, "description": "A function response.", "properties": { "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Signals that function call continues, and more responses will be returned, turning the function call into a generator. Is only applicable to NON_BLOCKING function calls (see FunctionDeclaration.behavior for details), ignored otherwise. If false, the default, future responses will not be considered. Is only applicable to NON_BLOCKING function calls, is ignored otherwise. If set to false, future responses will not be considered. It is allowed to return empty `response` with `will_continue=False` to signal that the function call is finished.", "title": "Willcontinue" }, "scheduling": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseScheduling" }, { "type": "null" } ], "default": null, "description": "Specifies how the response should be scheduled in the conversation. Only applicable to NON_BLOCKING function calls, is ignored otherwise. Defaults to WHEN_IDLE." }, "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/FunctionResponsePart" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a function response. Each part may\n have a different IANA MIME type.", "title": "Parts" }, "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The id of the function call this response is for. Populated by the client to match the corresponding function call `id`.", "title": "Id" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The name of the function to call. Matches [FunctionDeclaration.name] and [FunctionCall.name].", "title": "Name" }, "response": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Required. The function response in JSON object format. Use \"output\" key to specify function output and \"error\" key to specify error details (if any). If \"output\" and \"error\" keys are not specified, then whole \"response\" is treated as function output.", "title": "Response" } }, "title": "FunctionResponse", "type": "object" }, "FunctionResponseBlob": { "additionalProperties": false, "description": "Raw media bytes for function response.\n\nText should not be sent as raw bytes, use the FunctionResponse.response\nfield.", "properties": { "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Inline media bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob.\n Used to provide a label or filename to distinguish blobs.", "title": "Displayname" } }, "title": "FunctionResponseBlob", "type": "object" }, "FunctionResponseFileData": { "additionalProperties": false, "description": "URI based data for function response.", "properties": { "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file.\n Used to provide a label or filename to distinguish files.", "title": "Displayname" } }, "title": "FunctionResponseFileData", "type": "object" }, "FunctionResponsePart": { "additionalProperties": false, "description": "A datatype containing media that is part of a `FunctionResponse` message.\n\nA `FunctionResponsePart` consists of data which has an associated datatype. A\n`FunctionResponsePart` can only contain one of the accepted types in\n`FunctionResponsePart.data`.\n\nA `FunctionResponsePart` must have a fixed IANA MIME type identifying the\ntype and subtype of the media if the `inline_data` field is filled with raw\nbytes.", "properties": { "inlineData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseBlob" }, { "type": "null" } ], "default": null, "description": "Optional. Inline media bytes." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseFileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." } }, "title": "FunctionResponsePart", "type": "object" }, "FunctionResponseScheduling": { "description": "Specifies how the response should be scheduled in the conversation.", "enum": [ "SCHEDULING_UNSPECIFIED", "SILENT", "WHEN_IDLE", "INTERRUPT" ], "title": "FunctionResponseScheduling", "type": "string" }, "GenerateContentResponseUsageMetadata": { "additionalProperties": false, "description": "Usage metadata about the content generation request and response.\n\nThis message provides a detailed breakdown of token usage and other relevant\nmetrics. This data type is not supported in Gemini API.", "properties": { "cacheTokensDetails": { "anyOf": [ { "items": { "$ref": "#/$defs/ModalityTokenCount" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Output only. A detailed breakdown of the token count for each modality in the cached content.", "title": "Cachetokensdetails" }, "cachedContentTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. The number of tokens in the cached content that was used for this request.", "title": "Cachedcontenttokencount" }, "candidatesTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "The total number of tokens in the generated candidates.", "title": "Candidatestokencount" }, "candidatesTokensDetails": { "anyOf": [ { "items": { "$ref": "#/$defs/ModalityTokenCount" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Output only. A detailed breakdown of the token count for each modality in the generated candidates.", "title": "Candidatestokensdetails" }, "promptTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "The total number of tokens in the prompt. This includes any text, images, or other media provided in the request. When `cached_content` is set, this also includes the number of tokens in the cached content.", "title": "Prompttokencount" }, "promptTokensDetails": { "anyOf": [ { "items": { "$ref": "#/$defs/ModalityTokenCount" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Output only. A detailed breakdown of the token count for each modality in the prompt.", "title": "Prompttokensdetails" }, "thoughtsTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. The number of tokens that were part of the model's generated \"thoughts\" output, if applicable.", "title": "Thoughtstokencount" }, "toolUsePromptTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. The number of tokens in the results from tool executions, which are provided back to the model as input, if applicable.", "title": "Tooluseprompttokencount" }, "toolUsePromptTokensDetails": { "anyOf": [ { "items": { "$ref": "#/$defs/ModalityTokenCount" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Output only. A detailed breakdown by modality of the token counts from the results of tool executions, which are provided back to the model as input.", "title": "Tooluseprompttokensdetails" }, "totalTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "The total number of tokens for the entire request. This is the sum of `prompt_token_count`, `candidates_token_count`, `tool_use_prompt_token_count`, and `thoughts_token_count`.", "title": "Totaltokencount" }, "trafficType": { "anyOf": [ { "$ref": "#/$defs/TrafficType" }, { "type": "null" } ], "default": null, "description": "Output only. The traffic type for this request." } }, "title": "GenerateContentResponseUsageMetadata", "type": "object" }, "GoogleTypeDate": { "additionalProperties": false, "description": "Represents a whole or partial calendar date, such as a birthday.\n\nThe time of day and time zone are either specified elsewhere or are\ninsignificant. The date is relative to the Gregorian Calendar. This can\nrepresent one of the following: * A full date, with non-zero year, month, and\nday values. * A month and day, with a zero year (for example, an anniversary).\n* A year on its own, with a zero month and a zero day. * A year and month,\nwith a zero day (for example, a credit card expiration date). Related types: *\ngoogle.type.TimeOfDay * google.type.DateTime * google.protobuf.Timestamp. This\ndata type is not supported in Gemini API.", "properties": { "day": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Day of a month. Must be from 1 to 31 and valid for the year and month, or 0 to specify a year by itself or a year and month where the day isn't significant.", "title": "Day" }, "month": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Month of a year. Must be from 1 to 12, or 0 to specify a year without a month and day.", "title": "Month" }, "year": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Year of the date. Must be from 1 to 9999, or 0 to specify a date without a year.", "title": "Year" } }, "title": "GoogleTypeDate", "type": "object" }, "GroundingChunk": { "additionalProperties": false, "description": "Grounding chunk.", "properties": { "maps": { "anyOf": [ { "$ref": "#/$defs/GroundingChunkMaps" }, { "type": "null" } ], "default": null, "description": "Grounding chunk from Google Maps. This field is not supported in Gemini API." }, "retrievedContext": { "anyOf": [ { "$ref": "#/$defs/GroundingChunkRetrievedContext" }, { "type": "null" } ], "default": null, "description": "Grounding chunk from context retrieved by the retrieval tools. This field is not supported in Gemini API." }, "web": { "anyOf": [ { "$ref": "#/$defs/GroundingChunkWeb" }, { "type": "null" } ], "default": null, "description": "Grounding chunk from the web." } }, "title": "GroundingChunk", "type": "object" }, "GroundingChunkMaps": { "additionalProperties": false, "description": "Chunk from Google Maps. This data type is not supported in Gemini API.", "properties": { "placeAnswerSources": { "anyOf": [ { "$ref": "#/$defs/GroundingChunkMapsPlaceAnswerSources" }, { "type": "null" } ], "default": null, "description": "Sources used to generate the place answer. This includes review snippets and photos that were used to generate the answer, as well as uris to flag content." }, "placeId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "This Place's resource name, in `places/{place_id}` format. Can be used to look up the Place.", "title": "Placeid" }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Text of the place answer.", "title": "Text" }, "title": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Title of the place.", "title": "Title" }, "uri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "URI reference of the place.", "title": "Uri" } }, "title": "GroundingChunkMaps", "type": "object" }, "GroundingChunkMapsPlaceAnswerSources": { "additionalProperties": false, "description": "Sources used to generate the place answer.\n\nThis data type is not supported in Gemini API.", "properties": { "flagContentUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A link where users can flag a problem with the generated answer.", "title": "Flagcontenturi" }, "reviewSnippets": { "anyOf": [ { "items": { "$ref": "#/$defs/GroundingChunkMapsPlaceAnswerSourcesReviewSnippet" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Snippets of reviews that are used to generate the answer.", "title": "Reviewsnippets" } }, "title": "GroundingChunkMapsPlaceAnswerSources", "type": "object" }, "GroundingChunkMapsPlaceAnswerSourcesAuthorAttribution": { "additionalProperties": false, "description": "Author attribution for a photo or review.\n\nThis data type is not supported in Gemini API.", "properties": { "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Name of the author of the Photo or Review.", "title": "Displayname" }, "photoUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Profile photo URI of the author of the Photo or Review.", "title": "Photouri" }, "uri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "URI of the author of the Photo or Review.", "title": "Uri" } }, "title": "GroundingChunkMapsPlaceAnswerSourcesAuthorAttribution", "type": "object" }, "GroundingChunkMapsPlaceAnswerSourcesReviewSnippet": { "additionalProperties": false, "description": "Encapsulates a review snippet.\n\nThis data type is not supported in Gemini API.", "properties": { "authorAttribution": { "anyOf": [ { "$ref": "#/$defs/GroundingChunkMapsPlaceAnswerSourcesAuthorAttribution" }, { "type": "null" } ], "default": null, "description": "This review's author." }, "flagContentUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A link where users can flag a problem with the review.", "title": "Flagcontenturi" }, "googleMapsUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A link to show the review on Google Maps.", "title": "Googlemapsuri" }, "relativePublishTimeDescription": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A string of formatted recent time, expressing the review time relative to the current time in a form appropriate for the language and country.", "title": "Relativepublishtimedescription" }, "review": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A reference representing this place review which may be used to look up this place review again.", "title": "Review" }, "reviewId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Id of the review referencing the place.", "title": "Reviewid" }, "title": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Title of the review.", "title": "Title" } }, "title": "GroundingChunkMapsPlaceAnswerSourcesReviewSnippet", "type": "object" }, "GroundingChunkRetrievedContext": { "additionalProperties": false, "description": "Chunk from context retrieved by the retrieval tools.\n\nThis data type is not supported in Gemini API.", "properties": { "documentName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. The full document name for the referenced Vertex AI Search document.", "title": "Documentname" }, "ragChunk": { "anyOf": [ { "$ref": "#/$defs/RagChunk" }, { "type": "null" } ], "default": null, "description": "Additional context for the RAG retrieval result. This is only populated when using the RAG retrieval tool." }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Text of the attribution.", "title": "Text" }, "title": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Title of the attribution.", "title": "Title" }, "uri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "URI reference of the attribution.", "title": "Uri" } }, "title": "GroundingChunkRetrievedContext", "type": "object" }, "GroundingChunkWeb": { "additionalProperties": false, "description": "Chunk from the web.", "properties": { "domain": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Domain of the (original) URI. This field is not supported in Gemini API.", "title": "Domain" }, "title": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Title of the chunk.", "title": "Title" }, "uri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "URI reference of the chunk.", "title": "Uri" } }, "title": "GroundingChunkWeb", "type": "object" }, "GroundingMetadata": { "additionalProperties": false, "description": "Metadata returned to client when grounding is enabled.", "properties": { "googleMapsWidgetContextToken": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Output only. Resource name of the Google Maps widget context token to be used with the PlacesContextElement widget to render contextual data. This is populated only for Google Maps grounding. This field is not supported in Gemini API.", "title": "Googlemapswidgetcontexttoken" }, "groundingChunks": { "anyOf": [ { "items": { "$ref": "#/$defs/GroundingChunk" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of supporting references retrieved from specified grounding source.", "title": "Groundingchunks" }, "groundingSupports": { "anyOf": [ { "items": { "$ref": "#/$defs/GroundingSupport" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. List of grounding support.", "title": "Groundingsupports" }, "retrievalMetadata": { "anyOf": [ { "$ref": "#/$defs/RetrievalMetadata" }, { "type": "null" } ], "default": null, "description": "Optional. Output only. Retrieval metadata." }, "retrievalQueries": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. Queries executed by the retrieval tools. This field is not supported in Gemini API.", "title": "Retrievalqueries" }, "searchEntryPoint": { "anyOf": [ { "$ref": "#/$defs/SearchEntryPoint" }, { "type": "null" } ], "default": null, "description": "Optional. Google search entry for the following-up web searches." }, "sourceFlaggingUris": { "anyOf": [ { "items": { "$ref": "#/$defs/GroundingMetadataSourceFlaggingUri" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. Output only. List of source flagging uris. This is currently populated only for Google Maps grounding. This field is not supported in Gemini API.", "title": "Sourceflagginguris" }, "webSearchQueries": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. Web search queries for the following-up web search.", "title": "Websearchqueries" } }, "title": "GroundingMetadata", "type": "object" }, "GroundingMetadataSourceFlaggingUri": { "additionalProperties": false, "description": "Source content flagging uri for a place or review.\n\nThis is currently populated only for Google Maps grounding. This data type is\nnot supported in Gemini API.", "properties": { "flagContentUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A link where users can flag a problem with the source (place or review).", "title": "Flagcontenturi" }, "sourceId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Id of the place or review.", "title": "Sourceid" } }, "title": "GroundingMetadataSourceFlaggingUri", "type": "object" }, "GroundingSupport": { "additionalProperties": false, "description": "Grounding support.", "properties": { "confidenceScores": { "anyOf": [ { "items": { "type": "number" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Confidence score of the support references. Ranges from 0 to 1. 1 is the most confident. For Gemini 2.0 and before, this list must have the same size as the grounding_chunk_indices. For Gemini 2.5 and after, this list will be empty and should be ignored.", "title": "Confidencescores" }, "groundingChunkIndices": { "anyOf": [ { "items": { "type": "integer" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "A list of indices (into 'grounding_chunk') specifying the citations associated with the claim. For instance [1,3,4] means that grounding_chunk[1], grounding_chunk[3], grounding_chunk[4] are the retrieved content attributed to the claim.", "title": "Groundingchunkindices" }, "segment": { "anyOf": [ { "$ref": "#/$defs/Segment" }, { "type": "null" } ], "default": null, "description": "Segment of the content this support belongs to." } }, "title": "GroundingSupport", "type": "object" }, "HTTPBase": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "http" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "scheme": { "title": "Scheme", "type": "string" } }, "required": [ "scheme" ], "title": "HTTPBase", "type": "object" }, "HTTPBearer": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "http" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "scheme": { "const": "bearer", "default": "bearer", "title": "Scheme", "type": "string" }, "bearerFormat": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Bearerformat" } }, "title": "HTTPBearer", "type": "object" }, "HttpAuth": { "additionalProperties": true, "description": "The credentials and metadata for HTTP authentication.", "properties": { "scheme": { "title": "Scheme", "type": "string" }, "credentials": { "$ref": "#/$defs/HttpCredentials" } }, "required": [ "scheme", "credentials" ], "title": "HttpAuth", "type": "object" }, "HttpCredentials": { "additionalProperties": true, "description": "Represents the secret token value for HTTP authentication, like user name, password, oauth token, etc.", "properties": { "username": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Username" }, "password": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Password" }, "token": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Token" } }, "title": "HttpCredentials", "type": "object" }, "Language": { "description": "Programming language of the `code`.", "enum": [ "LANGUAGE_UNSPECIFIED", "PYTHON" ], "title": "Language", "type": "string" }, "LiveServerSessionResumptionUpdate": { "additionalProperties": false, "description": "Update of the session resumption state.\n\nOnly sent if `session_resumption` was set in the connection config.", "properties": { "newHandle": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "New handle that represents state that can be resumed. Empty if `resumable`=false.", "title": "Newhandle" }, "resumable": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "True if session can be resumed at this point. It might be not possible to resume session at some points. In that case we send update empty new_handle and resumable=false. Example of such case could be model executing function calls or just generating. Resuming session (using previous session token) in such state will result in some data loss.", "title": "Resumable" }, "lastConsumedClientMessageIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Index of last message sent by client that is included in state represented by this SessionResumptionToken. Only sent when `SessionResumptionConfig.transparent` is set.\n\nPresence of this index allows users to transparently reconnect and avoid issue of losing some part of realtime audio input/video. If client wishes to temporarily disconnect (for example as result of receiving GoAway) they can do it without losing state by buffering messages sent since last `SessionResmumptionTokenUpdate`. This field will enable them to limit buffering (avoid keeping all requests in RAM).\n\nNote: This should not be used for when resuming a session at some time later -- in those cases partial audio and video frames arelikely not needed.", "title": "Lastconsumedclientmessageindex" } }, "title": "LiveServerSessionResumptionUpdate", "type": "object" }, "LogprobsResult": { "additionalProperties": false, "description": "Logprobs Result", "properties": { "chosenCandidates": { "anyOf": [ { "items": { "$ref": "#/$defs/LogprobsResultCandidate" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Length = total number of decoding steps. The chosen candidates may or may not be in top_candidates.", "title": "Chosencandidates" }, "topCandidates": { "anyOf": [ { "items": { "$ref": "#/$defs/LogprobsResultTopCandidates" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Length = total number of decoding steps.", "title": "Topcandidates" } }, "title": "LogprobsResult", "type": "object" }, "LogprobsResultCandidate": { "additionalProperties": false, "description": "Candidate for the logprobs token and score.", "properties": { "logProbability": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "The candidate's log probability.", "title": "Logprobability" }, "token": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The candidate's token string value.", "title": "Token" }, "tokenId": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "The candidate's token id value.", "title": "Tokenid" } }, "title": "LogprobsResultCandidate", "type": "object" }, "LogprobsResultTopCandidates": { "additionalProperties": false, "description": "Candidates with top log probabilities at each decoding step.", "properties": { "candidates": { "anyOf": [ { "items": { "$ref": "#/$defs/LogprobsResultCandidate" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Sorted by log probability in descending order.", "title": "Candidates" } }, "title": "LogprobsResultTopCandidates", "type": "object" }, "MediaModality": { "description": "Server content modalities.", "enum": [ "MODALITY_UNSPECIFIED", "TEXT", "IMAGE", "VIDEO", "AUDIO", "DOCUMENT" ], "title": "MediaModality", "type": "string" }, "ModalityTokenCount": { "additionalProperties": false, "description": "Represents token counting info for a single modality.", "properties": { "modality": { "anyOf": [ { "$ref": "#/$defs/MediaModality" }, { "type": "null" } ], "default": null, "description": "The modality associated with this token count." }, "tokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Number of tokens.", "title": "Tokencount" } }, "title": "ModalityTokenCount", "type": "object" }, "OAuth2": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "oauth2" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "flows": { "$ref": "#/$defs/OAuthFlows" } }, "required": [ "flows" ], "title": "OAuth2", "type": "object" }, "OAuth2Auth": { "additionalProperties": true, "description": "Represents credential value and its metadata for a OAuth2 credential.", "properties": { "clientId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Clientid" }, "clientSecret": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Clientsecret" }, "authUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Authuri" }, "state": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "State" }, "redirectUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Redirecturi" }, "authResponseUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Authresponseuri" }, "authCode": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Authcode" }, "accessToken": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Accesstoken" }, "refreshToken": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshtoken" }, "expiresAt": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "title": "Expiresat" }, "expiresIn": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "title": "Expiresin" }, "audience": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Audience" }, "tokenEndpointAuthMethod": { "anyOf": [ { "enum": [ "client_secret_basic", "client_secret_post", "client_secret_jwt", "private_key_jwt" ], "type": "string" }, { "type": "null" } ], "default": "client_secret_basic", "title": "Tokenendpointauthmethod" } }, "title": "OAuth2Auth", "type": "object" }, "OAuthFlowAuthorizationCode": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "authorizationUrl": { "title": "Authorizationurl", "type": "string" }, "tokenUrl": { "title": "Tokenurl", "type": "string" } }, "required": [ "authorizationUrl", "tokenUrl" ], "title": "OAuthFlowAuthorizationCode", "type": "object" }, "OAuthFlowClientCredentials": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "tokenUrl": { "title": "Tokenurl", "type": "string" } }, "required": [ "tokenUrl" ], "title": "OAuthFlowClientCredentials", "type": "object" }, "OAuthFlowImplicit": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "authorizationUrl": { "title": "Authorizationurl", "type": "string" } }, "required": [ "authorizationUrl" ], "title": "OAuthFlowImplicit", "type": "object" }, "OAuthFlowPassword": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "tokenUrl": { "title": "Tokenurl", "type": "string" } }, "required": [ "tokenUrl" ], "title": "OAuthFlowPassword", "type": "object" }, "OAuthFlows": { "additionalProperties": true, "properties": { "implicit": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowImplicit" }, { "type": "null" } ], "default": null }, "password": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowPassword" }, { "type": "null" } ], "default": null }, "clientCredentials": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowClientCredentials" }, { "type": "null" } ], "default": null }, "authorizationCode": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowAuthorizationCode" }, { "type": "null" } ], "default": null } }, "title": "OAuthFlows", "type": "object" }, "OpenIdConnect": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "openIdConnect" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "openIdConnectUrl": { "title": "Openidconnecturl", "type": "string" } }, "required": [ "openIdConnectUrl" ], "title": "OpenIdConnect", "type": "object" }, "OpenIdConnectWithConfig": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "openIdConnect" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "authorization_endpoint": { "title": "Authorization Endpoint", "type": "string" }, "token_endpoint": { "title": "Token Endpoint", "type": "string" }, "userinfo_endpoint": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Userinfo Endpoint" }, "revocation_endpoint": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Revocation Endpoint" }, "token_endpoint_auth_methods_supported": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Token Endpoint Auth Methods Supported" }, "grant_types_supported": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Grant Types Supported" }, "scopes": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Scopes" } }, "required": [ "authorization_endpoint", "token_endpoint" ], "title": "OpenIdConnectWithConfig", "type": "object" }, "Outcome": { "description": "Outcome of the code execution.", "enum": [ "OUTCOME_UNSPECIFIED", "OUTCOME_OK", "OUTCOME_FAILED", "OUTCOME_DEADLINE_EXCEEDED" ], "title": "Outcome", "type": "string" }, "Part": { "additionalProperties": false, "description": "A datatype containing media content.\n\nExactly one field within a Part should be set, representing the specific type\nof content being conveyed. Using multiple fields within the same `Part`\ninstance is considered invalid.", "properties": { "mediaResolution": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolution" }, { "type": "null" } ], "default": null, "description": "Media resolution for the input media.\n " }, "codeExecutionResult": { "anyOf": [ { "$ref": "#/$defs/CodeExecutionResult" }, { "type": "null" } ], "default": null, "description": "Optional. Result of executing the [ExecutableCode]." }, "executableCode": { "anyOf": [ { "$ref": "#/$defs/ExecutableCode" }, { "type": "null" } ], "default": null, "description": "Optional. Code generated by the model that is meant to be executed." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." }, "functionCall": { "anyOf": [ { "$ref": "#/$defs/FunctionCall" }, { "type": "null" } ], "default": null, "description": "Optional. A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] with the parameters and their values." }, "functionResponse": { "anyOf": [ { "$ref": "#/$defs/FunctionResponse" }, { "type": "null" } ], "default": null, "description": "Optional. The result output of a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function call. It is used as context to the model." }, "inlineData": { "anyOf": [ { "$ref": "#/$defs/Blob" }, { "type": "null" } ], "default": null, "description": "Optional. Inlined bytes data." }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Text part (can be code).", "title": "Text" }, "thought": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Indicates if the part is thought from the model.", "title": "Thought" }, "thoughtSignature": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. An opaque signature for the thought so it can be reused in subsequent requests.", "title": "Thoughtsignature" }, "videoMetadata": { "anyOf": [ { "$ref": "#/$defs/VideoMetadata" }, { "type": "null" } ], "default": null, "description": "Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data." } }, "title": "Part", "type": "object" }, "PartMediaResolution": { "additionalProperties": false, "description": "Media resolution for the input media.", "properties": { "level": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolutionLevel" }, { "type": "null" } ], "default": null, "description": "The tokenization quality used for given media.\n " }, "numTokens": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Specifies the required sequence length for media tokenization.\n ", "title": "Numtokens" } }, "title": "PartMediaResolution", "type": "object" }, "PartMediaResolutionLevel": { "description": "The tokenization quality used for given media.", "enum": [ "MEDIA_RESOLUTION_UNSPECIFIED", "MEDIA_RESOLUTION_LOW", "MEDIA_RESOLUTION_MEDIUM", "MEDIA_RESOLUTION_HIGH", "MEDIA_RESOLUTION_ULTRA_HIGH" ], "title": "PartMediaResolutionLevel", "type": "string" }, "PartialArg": { "additionalProperties": false, "description": "Partial argument value of the function call.\n\nThis data type is not supported in Gemini API.", "properties": { "nullValue": { "anyOf": [ { "const": "NULL_VALUE", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a null value.", "title": "Nullvalue" }, "numberValue": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a double value.", "title": "Numbervalue" }, "stringValue": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a string value.", "title": "Stringvalue" }, "boolValue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a boolean value.", "title": "Boolvalue" }, "jsonPath": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. A JSON Path (RFC 9535) to the argument being streamed. https://datatracker.ietf.org/doc/html/rfc9535. e.g. \"$.foo.bar[0].data\".", "title": "Jsonpath" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is not the last part of the same json_path. If true, another PartialArg message for the current json_path is expected to follow.", "title": "Willcontinue" } }, "title": "PartialArg", "type": "object" }, "RagChunk": { "additionalProperties": false, "description": "A RagChunk includes the content of a chunk of a RagFile, and associated metadata.\n\nThis data type is not supported in Gemini API.", "properties": { "pageSpan": { "anyOf": [ { "$ref": "#/$defs/RagChunkPageSpan" }, { "type": "null" } ], "default": null, "description": "If populated, represents where the chunk starts and ends in the document." }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The content of the chunk.", "title": "Text" } }, "title": "RagChunk", "type": "object" }, "RagChunkPageSpan": { "additionalProperties": false, "description": "Represents where the chunk starts and ends in the document.\n\nThis data type is not supported in Gemini API.", "properties": { "firstPage": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Page where chunk starts in the document. Inclusive. 1-indexed.", "title": "Firstpage" }, "lastPage": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Page where chunk ends in the document. Inclusive. 1-indexed.", "title": "Lastpage" } }, "title": "RagChunkPageSpan", "type": "object" }, "RetrievalMetadata": { "additionalProperties": false, "description": "Metadata related to retrieval in the grounding flow.", "properties": { "googleSearchDynamicRetrievalScore": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. Score indicating how likely information from Google Search could help answer the prompt. The score is in the range `[0, 1]`, where 0 is the least likely and 1 is the most likely. This score is only populated when Google Search grounding and dynamic retrieval is enabled. It will be compared to the threshold to determine whether to trigger Google Search.", "title": "Googlesearchdynamicretrievalscore" } }, "title": "RetrievalMetadata", "type": "object" }, "SearchEntryPoint": { "additionalProperties": false, "description": "Google search entry point.", "properties": { "renderedContent": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Web content snippet that can be embedded in a web page or an app webview.", "title": "Renderedcontent" }, "sdkBlob": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Base64 encoded JSON representing array of tuple.", "title": "Sdkblob" } }, "title": "SearchEntryPoint", "type": "object" }, "SecuritySchemeType": { "enum": [ "apiKey", "http", "oauth2", "openIdConnect" ], "title": "SecuritySchemeType", "type": "string" }, "Segment": { "additionalProperties": false, "description": "Segment of the content.", "properties": { "endIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. End index in the given Part, measured in bytes. Offset from the start of the Part, exclusive, starting at zero.", "title": "Endindex" }, "partIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. The index of a Part object within its parent Content object.", "title": "Partindex" }, "startIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. Start index in the given Part, measured in bytes. Offset from the start of the Part, inclusive, starting at zero.", "title": "Startindex" }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. The text corresponding to the segment from the response.", "title": "Text" } }, "title": "Segment", "type": "object" }, "ServiceAccount": { "additionalProperties": true, "description": "Represents Google Service Account configuration.", "properties": { "serviceAccountCredential": { "anyOf": [ { "$ref": "#/$defs/ServiceAccountCredential" }, { "type": "null" } ], "default": null }, "scopes": { "items": { "type": "string" }, "title": "Scopes", "type": "array" }, "useDefaultCredential": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": false, "title": "Usedefaultcredential" } }, "required": [ "scopes" ], "title": "ServiceAccount", "type": "object" }, "ServiceAccountCredential": { "additionalProperties": true, "description": "Represents Google Service Account configuration.\n\nAttributes:\n type: The type should be \"service_account\".\n project_id: The project ID.\n private_key_id: The ID of the private key.\n private_key: The private key.\n client_email: The client email.\n client_id: The client ID.\n auth_uri: The authorization URI.\n token_uri: The token URI.\n auth_provider_x509_cert_url: URL for auth provider's X.509 cert.\n client_x509_cert_url: URL for the client's X.509 cert.\n universe_domain: The universe domain.\n\nExample:\n\n config = ServiceAccountCredential(\n type_=\"service_account\",\n project_id=\"your_project_id\",\n private_key_id=\"your_private_key_id\",\n private_key=\"-----BEGIN PRIVATE KEY-----...\",\n client_email=\"...@....iam.gserviceaccount.com\",\n client_id=\"your_client_id\",\n auth_uri=\"https://accounts.google.com/o/oauth2/auth\",\n token_uri=\"https://oauth2.googleapis.com/token\",\n auth_provider_x509_cert_url=\"https://www.googleapis.com/oauth2/v1/certs\",\n client_x509_cert_url=\"https://www.googleapis.com/robot/v1/metadata/x509/...\",\n universe_domain=\"googleapis.com\"\n )\n\n\n config = ServiceAccountConfig.model_construct(**{\n ...service account config dict\n })", "properties": { "type": { "default": "", "title": "Type", "type": "string" }, "projectId": { "title": "Projectid", "type": "string" }, "privateKeyId": { "title": "Privatekeyid", "type": "string" }, "privateKey": { "title": "Privatekey", "type": "string" }, "clientEmail": { "title": "Clientemail", "type": "string" }, "clientId": { "title": "Clientid", "type": "string" }, "authUri": { "title": "Authuri", "type": "string" }, "tokenUri": { "title": "Tokenuri", "type": "string" }, "authProviderX509CertUrl": { "title": "Authproviderx509Certurl", "type": "string" }, "clientX509CertUrl": { "title": "Clientx509Certurl", "type": "string" }, "universeDomain": { "title": "Universedomain", "type": "string" } }, "required": [ "projectId", "privateKeyId", "privateKey", "clientEmail", "clientId", "authUri", "tokenUri", "authProviderX509CertUrl", "clientX509CertUrl", "universeDomain" ], "title": "ServiceAccountCredential", "type": "object" }, "ToolConfirmation": { "additionalProperties": false, "description": "Represents a tool confirmation configuration.", "properties": { "hint": { "default": "", "title": "Hint", "type": "string" }, "confirmed": { "default": false, "title": "Confirmed", "type": "boolean" }, "payload": { "anyOf": [ {}, { "type": "null" } ], "default": null, "title": "Payload" } }, "title": "ToolConfirmation", "type": "object" }, "TrafficType": { "description": "Output only.\n\nThe traffic type for this request. This enum is not supported in Gemini API.", "enum": [ "TRAFFIC_TYPE_UNSPECIFIED", "ON_DEMAND", "PROVISIONED_THROUGHPUT" ], "title": "TrafficType", "type": "string" }, "Transcription": { "additionalProperties": false, "description": "Audio transcription in Server Conent.", "properties": { "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Transcription text.\n ", "title": "Text" }, "finished": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "The bool indicates the end of the transcription.\n ", "title": "Finished" } }, "title": "Transcription", "type": "object" }, "VideoMetadata": { "additionalProperties": false, "description": "Metadata describes the input video content.", "properties": { "endOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The end offset of the video.", "title": "Endoffset" }, "fps": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. The frame rate of the video sent to the model. If not specified, the default value will be 1.0. The fps range is (0.0, 24.0].", "title": "Fps" }, "startOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The start offset of the video.", "title": "Startoffset" } }, "title": "VideoMetadata", "type": "object" } }, "additionalProperties": false, "required": [ "author" ] }

- Fields:
`actions (google.adk.events.event_actions.EventActions)`

`author (str)`

`branch (str | None)`

`id (str)`

`invocation_id (str)`

`long_running_tool_ids (set[str] | None)`

`timestamp (float)`


-
*field*actions*:*[EventActions](#google.adk.events.EventActions)*[Optional]*[¶](#google.adk.events.Event.actions) The actions taken by the agent.


-
*field*author*: str**[Required]*[¶](#google.adk.events.Event.author) ‘user’ or the name of the agent, indicating who appended the event to the session.


-
*field*branch*: str | None**= None*[¶](#google.adk.events.Event.branch) The branch of the event.

The format is like agent_1.agent_2.agent_3, where agent_1 is the parent of agent_2, and agent_2 is the parent of agent_3.

Branch is used when multiple sub-agent shouldn’t see their peer agents’ conversation history.


-
*field*id*: str**= ''*[¶](#google.adk.events.Event.id) The unique identifier of the event.


-
*field*invocation_id*: str**= ''**(alias 'invocationId')*[¶](#google.adk.events.Event.invocation_id) The invocation ID of the event. Should be non-empty before appending to a session.


-
*field*long_running_tool_ids*: set[str] | None**= None**(alias 'longRunningToolIds')*[¶](#google.adk.events.Event.long_running_tool_ids) Set of ids of the long running function calls. Agent client will know from this field about which function call is long running. only valid for function call event


-
*field*timestamp*: float**[Optional]*[¶](#google.adk.events.Event.timestamp) The timestamp of the event.


-
*static*new_id()[¶](#google.adk.events.Event.new_id)

-
get_function_calls()
[¶](#google.adk.events.Event.get_function_calls) Returns the function calls in the event.

- Return type:
`list`

[`FunctionCall`

]


-
get_function_responses()
[¶](#google.adk.events.Event.get_function_responses) Returns the function responses in the event.

- Return type:
`list`

[`FunctionResponse`

]


-
has_trailing_code_execution_result()
[¶](#google.adk.events.Event.has_trailing_code_execution_result) Returns whether the event has a trailing code execution result.

- Return type:
`bool`


-
is_final_response()
[¶](#google.adk.events.Event.is_final_response) Returns whether the event is the final response of an agent.

NOTE: This method is ONLY for use by Agent Development Kit.

Note that when multiple agents participate in one invocation, there could be one event has is_final_response() as True for each participating agent.

- Return type:
`bool`


-
model_post_init(
*_Event__context*)[¶](#google.adk.events.Event.model_post_init) Post initialization logic for the event.


-
*pydantic model*google.adk.events.EventActions[¶](#google.adk.events.EventActions) Bases:

`BaseModel`

Represents the actions attached to an event.

## Show JSON schema

{ "title": "EventActions", "description": "Represents the actions attached to an event.", "type": "object", "properties": { "skipSummarization": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Skipsummarization" }, "stateDelta": { "additionalProperties": true, "title": "Statedelta", "type": "object" }, "artifactDelta": { "additionalProperties": { "type": "integer" }, "title": "Artifactdelta", "type": "object" }, "transferToAgent": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Transfertoagent" }, "escalate": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Escalate" }, "requestedAuthConfigs": { "additionalProperties": { "$ref": "#/$defs/AuthConfig" }, "title": "Requestedauthconfigs", "type": "object" }, "requestedToolConfirmations": { "additionalProperties": { "$ref": "#/$defs/ToolConfirmation" }, "title": "Requestedtoolconfirmations", "type": "object" }, "compaction": { "anyOf": [ { "$ref": "#/$defs/EventCompaction" }, { "type": "null" } ], "default": null }, "endOfAgent": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Endofagent" }, "agentState": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "title": "Agentstate" }, "rewindBeforeInvocationId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Rewindbeforeinvocationid" } }, "$defs": { "APIKey": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "apiKey" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "in": { "$ref": "#/$defs/APIKeyIn" }, "name": { "title": "Name", "type": "string" } }, "required": [ "in", "name" ], "title": "APIKey", "type": "object" }, "APIKeyIn": { "enum": [ "query", "header", "cookie" ], "title": "APIKeyIn", "type": "string" }, "AuthConfig": { "additionalProperties": true, "description": "The auth config sent by tool asking client to collect auth credentials and\n\nadk and client will help to fill in the response", "properties": { "authScheme": { "anyOf": [ { "$ref": "#/$defs/APIKey" }, { "$ref": "#/$defs/HTTPBase" }, { "$ref": "#/$defs/OAuth2" }, { "$ref": "#/$defs/OpenIdConnect" }, { "$ref": "#/$defs/HTTPBearer" }, { "$ref": "#/$defs/OpenIdConnectWithConfig" } ], "title": "Authscheme" }, "rawAuthCredential": { "anyOf": [ { "$ref": "#/$defs/AuthCredential" }, { "type": "null" } ], "default": null }, "exchangedAuthCredential": { "anyOf": [ { "$ref": "#/$defs/AuthCredential" }, { "type": "null" } ], "default": null }, "credentialKey": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Credentialkey" } }, "required": [ "authScheme" ], "title": "AuthConfig", "type": "object" }, "AuthCredential": { "additionalProperties": true, "description": "Data class representing an authentication credential.\n\nTo exchange for the actual credential, please use\nCredentialExchanger.exchange_credential().\n\nExamples: API Key Auth\nAuthCredential(\n auth_type=AuthCredentialTypes.API_KEY,\n api_key=\"1234\",\n)\n\nExample: HTTP Auth\nAuthCredential(\n auth_type=AuthCredentialTypes.HTTP,\n http=HttpAuth(\n scheme=\"basic\",\n credentials=HttpCredentials(username=\"user\", password=\"password\"),\n ),\n)\n\nExample: OAuth2 Bearer Token in HTTP Header\nAuthCredential(\n auth_type=AuthCredentialTypes.HTTP,\n http=HttpAuth(\n scheme=\"bearer\",\n credentials=HttpCredentials(token=\"eyAkaknabna....\"),\n ),\n)\n\nExample: OAuth2 Auth with Authorization Code Flow\nAuthCredential(\n auth_type=AuthCredentialTypes.OAUTH2,\n oauth2=OAuth2Auth(\n client_id=\"1234\",\n client_secret=\"secret\",\n ),\n)\n\nExample: OpenID Connect Auth\nAuthCredential(\n auth_type=AuthCredentialTypes.OPEN_ID_CONNECT,\n oauth2=OAuth2Auth(\n client_id=\"1234\",\n client_secret=\"secret\",\n redirect_uri=\"https://example.com\",\n scopes=[\"scope1\", \"scope2\"],\n ),\n)\n\nExample: Auth with resource reference\nAuthCredential(\n auth_type=AuthCredentialTypes.API_KEY,\n resource_ref=\"projects/1234/locations/us-central1/resources/resource1\",\n)", "properties": { "authType": { "$ref": "#/$defs/AuthCredentialTypes" }, "resourceRef": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Resourceref" }, "apiKey": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Apikey" }, "http": { "anyOf": [ { "$ref": "#/$defs/HttpAuth" }, { "type": "null" } ], "default": null }, "serviceAccount": { "anyOf": [ { "$ref": "#/$defs/ServiceAccount" }, { "type": "null" } ], "default": null }, "oauth2": { "anyOf": [ { "$ref": "#/$defs/OAuth2Auth" }, { "type": "null" } ], "default": null } }, "required": [ "authType" ], "title": "AuthCredential", "type": "object" }, "AuthCredentialTypes": { "description": "Represents the type of authentication credential.", "enum": [ "apiKey", "http", "oauth2", "openIdConnect", "serviceAccount" ], "title": "AuthCredentialTypes", "type": "string" }, "Blob": { "additionalProperties": false, "description": "Content blob.", "properties": { "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Raw bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob. Used to provide a label or filename to distinguish blobs. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "Blob", "type": "object" }, "CodeExecutionResult": { "additionalProperties": false, "description": "Result of executing the [ExecutableCode].\n\nOnly generated when using the [CodeExecution] tool, and always follows a\n`part` containing the [ExecutableCode].", "properties": { "outcome": { "anyOf": [ { "$ref": "#/$defs/Outcome" }, { "type": "null" } ], "default": null, "description": "Required. Outcome of the code execution." }, "output": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Contains stdout when code execution is successful, stderr or other description otherwise.", "title": "Output" } }, "title": "CodeExecutionResult", "type": "object" }, "Content": { "additionalProperties": false, "description": "Contains the multi-part content of a message.", "properties": { "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/Part" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a single message. Each part may have\n a different IANA MIME type.", "title": "Parts" }, "role": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The producer of the content. Must be either 'user' or 'model'. Useful to set for multi-turn conversations, otherwise can be left blank or unset.", "title": "Role" } }, "title": "Content", "type": "object" }, "EventCompaction": { "additionalProperties": false, "description": "The compaction of the events.", "properties": { "startTimestamp": { "title": "Starttimestamp", "type": "number" }, "endTimestamp": { "title": "Endtimestamp", "type": "number" }, "compactedContent": { "$ref": "#/$defs/Content" } }, "required": [ "startTimestamp", "endTimestamp", "compactedContent" ], "title": "EventCompaction", "type": "object" }, "ExecutableCode": { "additionalProperties": false, "description": "Code generated by the model that is meant to be executed, and the result returned to the model.\n\nGenerated when using the [CodeExecution] tool, in which the code will be\nautomatically executed, and a corresponding [CodeExecutionResult] will also be\ngenerated.", "properties": { "code": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The code to be executed.", "title": "Code" }, "language": { "anyOf": [ { "$ref": "#/$defs/Language" }, { "type": "null" } ], "default": null, "description": "Required. Programming language of the `code`." } }, "title": "ExecutableCode", "type": "object" }, "FileData": { "additionalProperties": false, "description": "URI based data.", "properties": { "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file data. Used to provide a label or filename to distinguish file datas. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "FileData", "type": "object" }, "FunctionCall": { "additionalProperties": false, "description": "A function call.", "properties": { "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The unique id of the function call. If populated, the client to execute the\n `function_call` and return the response with the matching `id`.", "title": "Id" }, "args": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Optional. The function parameters and values in JSON object format. See [FunctionDeclaration.parameters] for parameter details.", "title": "Args" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The name of the function to call. Matches [FunctionDeclaration.name].", "title": "Name" }, "partialArgs": { "anyOf": [ { "items": { "$ref": "#/$defs/PartialArg" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. The partial argument value of the function call. If provided, represents the arguments/fields that are streamed incrementally. This field is not supported in Gemini API.", "title": "Partialargs" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is the last part of the FunctionCall. If true, another partial message for the current FunctionCall is expected to follow. This field is not supported in Gemini API.", "title": "Willcontinue" } }, "title": "FunctionCall", "type": "object" }, "FunctionResponse": { "additionalProperties": false, "description": "A function response.", "properties": { "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Signals that function call continues, and more responses will be returned, turning the function call into a generator. Is only applicable to NON_BLOCKING function calls (see FunctionDeclaration.behavior for details), ignored otherwise. If false, the default, future responses will not be considered. Is only applicable to NON_BLOCKING function calls, is ignored otherwise. If set to false, future responses will not be considered. It is allowed to return empty `response` with `will_continue=False` to signal that the function call is finished.", "title": "Willcontinue" }, "scheduling": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseScheduling" }, { "type": "null" } ], "default": null, "description": "Specifies how the response should be scheduled in the conversation. Only applicable to NON_BLOCKING function calls, is ignored otherwise. Defaults to WHEN_IDLE." }, "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/FunctionResponsePart" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a function response. Each part may\n have a different IANA MIME type.", "title": "Parts" }, "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The id of the function call this response is for. Populated by the client to match the corresponding function call `id`.", "title": "Id" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The name of the function to call. Matches [FunctionDeclaration.name] and [FunctionCall.name].", "title": "Name" }, "response": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Required. The function response in JSON object format. Use \"output\" key to specify function output and \"error\" key to specify error details (if any). If \"output\" and \"error\" keys are not specified, then whole \"response\" is treated as function output.", "title": "Response" } }, "title": "FunctionResponse", "type": "object" }, "FunctionResponseBlob": { "additionalProperties": false, "description": "Raw media bytes for function response.\n\nText should not be sent as raw bytes, use the FunctionResponse.response\nfield.", "properties": { "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Inline media bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob.\n Used to provide a label or filename to distinguish blobs.", "title": "Displayname" } }, "title": "FunctionResponseBlob", "type": "object" }, "FunctionResponseFileData": { "additionalProperties": false, "description": "URI based data for function response.", "properties": { "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file.\n Used to provide a label or filename to distinguish files.", "title": "Displayname" } }, "title": "FunctionResponseFileData", "type": "object" }, "FunctionResponsePart": { "additionalProperties": false, "description": "A datatype containing media that is part of a `FunctionResponse` message.\n\nA `FunctionResponsePart` consists of data which has an associated datatype. A\n`FunctionResponsePart` can only contain one of the accepted types in\n`FunctionResponsePart.data`.\n\nA `FunctionResponsePart` must have a fixed IANA MIME type identifying the\ntype and subtype of the media if the `inline_data` field is filled with raw\nbytes.", "properties": { "inlineData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseBlob" }, { "type": "null" } ], "default": null, "description": "Optional. Inline media bytes." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseFileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." } }, "title": "FunctionResponsePart", "type": "object" }, "FunctionResponseScheduling": { "description": "Specifies how the response should be scheduled in the conversation.", "enum": [ "SCHEDULING_UNSPECIFIED", "SILENT", "WHEN_IDLE", "INTERRUPT" ], "title": "FunctionResponseScheduling", "type": "string" }, "HTTPBase": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "http" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "scheme": { "title": "Scheme", "type": "string" } }, "required": [ "scheme" ], "title": "HTTPBase", "type": "object" }, "HTTPBearer": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "http" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "scheme": { "const": "bearer", "default": "bearer", "title": "Scheme", "type": "string" }, "bearerFormat": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Bearerformat" } }, "title": "HTTPBearer", "type": "object" }, "HttpAuth": { "additionalProperties": true, "description": "The credentials and metadata for HTTP authentication.", "properties": { "scheme": { "title": "Scheme", "type": "string" }, "credentials": { "$ref": "#/$defs/HttpCredentials" } }, "required": [ "scheme", "credentials" ], "title": "HttpAuth", "type": "object" }, "HttpCredentials": { "additionalProperties": true, "description": "Represents the secret token value for HTTP authentication, like user name, password, oauth token, etc.", "properties": { "username": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Username" }, "password": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Password" }, "token": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Token" } }, "title": "HttpCredentials", "type": "object" }, "Language": { "description": "Programming language of the `code`.", "enum": [ "LANGUAGE_UNSPECIFIED", "PYTHON" ], "title": "Language", "type": "string" }, "OAuth2": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "oauth2" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "flows": { "$ref": "#/$defs/OAuthFlows" } }, "required": [ "flows" ], "title": "OAuth2", "type": "object" }, "OAuth2Auth": { "additionalProperties": true, "description": "Represents credential value and its metadata for a OAuth2 credential.", "properties": { "clientId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Clientid" }, "clientSecret": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Clientsecret" }, "authUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Authuri" }, "state": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "State" }, "redirectUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Redirecturi" }, "authResponseUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Authresponseuri" }, "authCode": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Authcode" }, "accessToken": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Accesstoken" }, "refreshToken": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshtoken" }, "expiresAt": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "title": "Expiresat" }, "expiresIn": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "title": "Expiresin" }, "audience": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Audience" }, "tokenEndpointAuthMethod": { "anyOf": [ { "enum": [ "client_secret_basic", "client_secret_post", "client_secret_jwt", "private_key_jwt" ], "type": "string" }, { "type": "null" } ], "default": "client_secret_basic", "title": "Tokenendpointauthmethod" } }, "title": "OAuth2Auth", "type": "object" }, "OAuthFlowAuthorizationCode": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "authorizationUrl": { "title": "Authorizationurl", "type": "string" }, "tokenUrl": { "title": "Tokenurl", "type": "string" } }, "required": [ "authorizationUrl", "tokenUrl" ], "title": "OAuthFlowAuthorizationCode", "type": "object" }, "OAuthFlowClientCredentials": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "tokenUrl": { "title": "Tokenurl", "type": "string" } }, "required": [ "tokenUrl" ], "title": "OAuthFlowClientCredentials", "type": "object" }, "OAuthFlowImplicit": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "authorizationUrl": { "title": "Authorizationurl", "type": "string" } }, "required": [ "authorizationUrl" ], "title": "OAuthFlowImplicit", "type": "object" }, "OAuthFlowPassword": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "tokenUrl": { "title": "Tokenurl", "type": "string" } }, "required": [ "tokenUrl" ], "title": "OAuthFlowPassword", "type": "object" }, "OAuthFlows": { "additionalProperties": true, "properties": { "implicit": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowImplicit" }, { "type": "null" } ], "default": null }, "password": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowPassword" }, { "type": "null" } ], "default": null }, "clientCredentials": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowClientCredentials" }, { "type": "null" } ], "default": null }, "authorizationCode": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowAuthorizationCode" }, { "type": "null" } ], "default": null } }, "title": "OAuthFlows", "type": "object" }, "OpenIdConnect": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "openIdConnect" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "openIdConnectUrl": { "title": "Openidconnecturl", "type": "string" } }, "required": [ "openIdConnectUrl" ], "title": "OpenIdConnect", "type": "object" }, "OpenIdConnectWithConfig": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "openIdConnect" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "authorization_endpoint": { "title": "Authorization Endpoint", "type": "string" }, "token_endpoint": { "title": "Token Endpoint", "type": "string" }, "userinfo_endpoint": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Userinfo Endpoint" }, "revocation_endpoint": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Revocation Endpoint" }, "token_endpoint_auth_methods_supported": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Token Endpoint Auth Methods Supported" }, "grant_types_supported": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Grant Types Supported" }, "scopes": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Scopes" } }, "required": [ "authorization_endpoint", "token_endpoint" ], "title": "OpenIdConnectWithConfig", "type": "object" }, "Outcome": { "description": "Outcome of the code execution.", "enum": [ "OUTCOME_UNSPECIFIED", "OUTCOME_OK", "OUTCOME_FAILED", "OUTCOME_DEADLINE_EXCEEDED" ], "title": "Outcome", "type": "string" }, "Part": { "additionalProperties": false, "description": "A datatype containing media content.\n\nExactly one field within a Part should be set, representing the specific type\nof content being conveyed. Using multiple fields within the same `Part`\ninstance is considered invalid.", "properties": { "mediaResolution": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolution" }, { "type": "null" } ], "default": null, "description": "Media resolution for the input media.\n " }, "codeExecutionResult": { "anyOf": [ { "$ref": "#/$defs/CodeExecutionResult" }, { "type": "null" } ], "default": null, "description": "Optional. Result of executing the [ExecutableCode]." }, "executableCode": { "anyOf": [ { "$ref": "#/$defs/ExecutableCode" }, { "type": "null" } ], "default": null, "description": "Optional. Code generated by the model that is meant to be executed." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." }, "functionCall": { "anyOf": [ { "$ref": "#/$defs/FunctionCall" }, { "type": "null" } ], "default": null, "description": "Optional. A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] with the parameters and their values." }, "functionResponse": { "anyOf": [ { "$ref": "#/$defs/FunctionResponse" }, { "type": "null" } ], "default": null, "description": "Optional. The result output of a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function call. It is used as context to the model." }, "inlineData": { "anyOf": [ { "$ref": "#/$defs/Blob" }, { "type": "null" } ], "default": null, "description": "Optional. Inlined bytes data." }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Text part (can be code).", "title": "Text" }, "thought": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Indicates if the part is thought from the model.", "title": "Thought" }, "thoughtSignature": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. An opaque signature for the thought so it can be reused in subsequent requests.", "title": "Thoughtsignature" }, "videoMetadata": { "anyOf": [ { "$ref": "#/$defs/VideoMetadata" }, { "type": "null" } ], "default": null, "description": "Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data." } }, "title": "Part", "type": "object" }, "PartMediaResolution": { "additionalProperties": false, "description": "Media resolution for the input media.", "properties": { "level": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolutionLevel" }, { "type": "null" } ], "default": null, "description": "The tokenization quality used for given media.\n " }, "numTokens": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Specifies the required sequence length for media tokenization.\n ", "title": "Numtokens" } }, "title": "PartMediaResolution", "type": "object" }, "PartMediaResolutionLevel": { "description": "The tokenization quality used for given media.", "enum": [ "MEDIA_RESOLUTION_UNSPECIFIED", "MEDIA_RESOLUTION_LOW", "MEDIA_RESOLUTION_MEDIUM", "MEDIA_RESOLUTION_HIGH", "MEDIA_RESOLUTION_ULTRA_HIGH" ], "title": "PartMediaResolutionLevel", "type": "string" }, "PartialArg": { "additionalProperties": false, "description": "Partial argument value of the function call.\n\nThis data type is not supported in Gemini API.", "properties": { "nullValue": { "anyOf": [ { "const": "NULL_VALUE", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a null value.", "title": "Nullvalue" }, "numberValue": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a double value.", "title": "Numbervalue" }, "stringValue": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a string value.", "title": "Stringvalue" }, "boolValue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a boolean value.", "title": "Boolvalue" }, "jsonPath": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. A JSON Path (RFC 9535) to the argument being streamed. https://datatracker.ietf.org/doc/html/rfc9535. e.g. \"$.foo.bar[0].data\".", "title": "Jsonpath" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is not the last part of the same json_path. If true, another PartialArg message for the current json_path is expected to follow.", "title": "Willcontinue" } }, "title": "PartialArg", "type": "object" }, "SecuritySchemeType": { "enum": [ "apiKey", "http", "oauth2", "openIdConnect" ], "title": "SecuritySchemeType", "type": "string" }, "ServiceAccount": { "additionalProperties": true, "description": "Represents Google Service Account configuration.", "properties": { "serviceAccountCredential": { "anyOf": [ { "$ref": "#/$defs/ServiceAccountCredential" }, { "type": "null" } ], "default": null }, "scopes": { "items": { "type": "string" }, "title": "Scopes", "type": "array" }, "useDefaultCredential": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": false, "title": "Usedefaultcredential" } }, "required": [ "scopes" ], "title": "ServiceAccount", "type": "object" }, "ServiceAccountCredential": { "additionalProperties": true, "description": "Represents Google Service Account configuration.\n\nAttributes:\n type: The type should be \"service_account\".\n project_id: The project ID.\n private_key_id: The ID of the private key.\n private_key: The private key.\n client_email: The client email.\n client_id: The client ID.\n auth_uri: The authorization URI.\n token_uri: The token URI.\n auth_provider_x509_cert_url: URL for auth provider's X.509 cert.\n client_x509_cert_url: URL for the client's X.509 cert.\n universe_domain: The universe domain.\n\nExample:\n\n config = ServiceAccountCredential(\n type_=\"service_account\",\n project_id=\"your_project_id\",\n private_key_id=\"your_private_key_id\",\n private_key=\"-----BEGIN PRIVATE KEY-----...\",\n client_email=\"...@....iam.gserviceaccount.com\",\n client_id=\"your_client_id\",\n auth_uri=\"https://accounts.google.com/o/oauth2/auth\",\n token_uri=\"https://oauth2.googleapis.com/token\",\n auth_provider_x509_cert_url=\"https://www.googleapis.com/oauth2/v1/certs\",\n client_x509_cert_url=\"https://www.googleapis.com/robot/v1/metadata/x509/...\",\n universe_domain=\"googleapis.com\"\n )\n\n\n config = ServiceAccountConfig.model_construct(**{\n ...service account config dict\n })", "properties": { "type": { "default": "", "title": "Type", "type": "string" }, "projectId": { "title": "Projectid", "type": "string" }, "privateKeyId": { "title": "Privatekeyid", "type": "string" }, "privateKey": { "title": "Privatekey", "type": "string" }, "clientEmail": { "title": "Clientemail", "type": "string" }, "clientId": { "title": "Clientid", "type": "string" }, "authUri": { "title": "Authuri", "type": "string" }, "tokenUri": { "title": "Tokenuri", "type": "string" }, "authProviderX509CertUrl": { "title": "Authproviderx509Certurl", "type": "string" }, "clientX509CertUrl": { "title": "Clientx509Certurl", "type": "string" }, "universeDomain": { "title": "Universedomain", "type": "string" } }, "required": [ "projectId", "privateKeyId", "privateKey", "clientEmail", "clientId", "authUri", "tokenUri", "authProviderX509CertUrl", "clientX509CertUrl", "universeDomain" ], "title": "ServiceAccountCredential", "type": "object" }, "ToolConfirmation": { "additionalProperties": false, "description": "Represents a tool confirmation configuration.", "properties": { "hint": { "default": "", "title": "Hint", "type": "string" }, "confirmed": { "default": false, "title": "Confirmed", "type": "boolean" }, "payload": { "anyOf": [ {}, { "type": "null" } ], "default": null, "title": "Payload" } }, "title": "ToolConfirmation", "type": "object" }, "VideoMetadata": { "additionalProperties": false, "description": "Metadata describes the input video content.", "properties": { "endOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The end offset of the video.", "title": "Endoffset" }, "fps": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. The frame rate of the video sent to the model. If not specified, the default value will be 1.0. The fps range is (0.0, 24.0].", "title": "Fps" }, "startOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The start offset of the video.", "title": "Startoffset" } }, "title": "VideoMetadata", "type": "object" } }, "additionalProperties": false }

- Fields:
`agent_state (dict[str, Any] | None)`

`artifact_delta (dict[str, int])`

`compaction (google.adk.events.event_actions.EventCompaction | None)`

`end_of_agent (bool | None)`

`escalate (bool | None)`

`requested_auth_configs (dict[str, google.adk.auth.auth_tool.AuthConfig])`

`requested_tool_confirmations (dict[str, google.adk.tools.tool_confirmation.ToolConfirmation])`

`rewind_before_invocation_id (str | None)`

`skip_summarization (bool | None)`

`state_delta (dict[str, object])`

`transfer_to_agent (str | None)`


-
*field*agent_state*: dict[str, Any] | None**= None**(alias 'agentState')*[¶](#google.adk.events.EventActions.agent_state) The agent state at the current event, used for checkpoint and resume. This should only be set by ADK workflow.


-
*field*artifact_delta*: dict[str, int]**[Optional]**(alias 'artifactDelta')*[¶](#google.adk.events.EventActions.artifact_delta) Indicates that the event is updating an artifact. key is the filename, value is the version.


-
*field*compaction*: EventCompaction | None**= None*[¶](#google.adk.events.EventActions.compaction) The compaction of the events.


-
*field*end_of_agent*: bool | None**= None**(alias 'endOfAgent')*[¶](#google.adk.events.EventActions.end_of_agent) If true, the current agent has finished its current run. Note that there can be multiple events with end_of_agent=True for the same agent within one invocation when there is a loop. This should only be set by ADK workflow.


-
*field*escalate*: bool | None**= None*[¶](#google.adk.events.EventActions.escalate) The agent is escalating to a higher level agent.


-
*field*requested_auth_configs*: dict[str, AuthConfig]**[Optional]**(alias 'requestedAuthConfigs')*[¶](#google.adk.events.EventActions.requested_auth_configs) Authentication configurations requested by tool responses.

This field will only be set by a tool response event indicating tool request auth credential. - Keys: The function call id. Since one function response event could contain multiple function responses that correspond to multiple function calls. Each function call could request different auth configs. This id is used to identify the function call. - Values: The requested auth config.


-
*field*requested_tool_confirmations*: dict[str, ToolConfirmation]**[Optional]**(alias 'requestedToolConfirmations')*[¶](#google.adk.events.EventActions.requested_tool_confirmations) A dict of tool confirmation requested by this event, keyed by function call id.


-
*field*rewind_before_invocation_id*: str | None**= None**(alias 'rewindBeforeInvocationId')*[¶](#google.adk.events.EventActions.rewind_before_invocation_id) The invocation id to rewind to. This is only set for rewind event.


-
*field*skip_summarization*: bool | None**= None**(alias 'skipSummarization')*[¶](#google.adk.events.EventActions.skip_summarization) If true, it won’t call model to summarize function response.

Only used for function_response event.


-
*field*state_delta*: dict[str, object]**[Optional]**(alias 'stateDelta')*[¶](#google.adk.events.EventActions.state_delta) Indicates that the event is updating the state with the given delta.


-
*field*transfer_to_agent*: str | None**= None**(alias 'transferToAgent')*[¶](#google.adk.events.EventActions.transfer_to_agent) If set, the event transfers to the specified agent.


# google.adk.examples module[¶](#module-google.adk.examples)

-
*class*google.adk.examples.BaseExampleProvider[¶](#google.adk.examples.BaseExampleProvider) Bases:

`ABC`

Base class for example providers.

This class defines the interface for providing examples for a given query.


-
*pydantic model*google.adk.examples.Example[¶](#google.adk.examples.Example) Bases:

`BaseModel`

A few-shot example.

-
input
[¶](#google.adk.examples.Example.input) The input content for the example.


-
output
[¶](#google.adk.examples.Example.output) The expected output content for the example.


## Show JSON schema

{ "title": "Example", "description": "A few-shot example.\n\nAttributes:\n input: The input content for the example.\n output: The expected output content for the example.", "type": "object", "properties": { "input": { "$ref": "#/$defs/Content" }, "output": { "items": { "$ref": "#/$defs/Content" }, "title": "Output", "type": "array" } }, "$defs": { "Blob": { "additionalProperties": false, "description": "Content blob.", "properties": { "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Raw bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob. Used to provide a label or filename to distinguish blobs. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "Blob", "type": "object" }, "CodeExecutionResult": { "additionalProperties": false, "description": "Result of executing the [ExecutableCode].\n\nOnly generated when using the [CodeExecution] tool, and always follows a\n`part` containing the [ExecutableCode].", "properties": { "outcome": { "anyOf": [ { "$ref": "#/$defs/Outcome" }, { "type": "null" } ], "default": null, "description": "Required. Outcome of the code execution." }, "output": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Contains stdout when code execution is successful, stderr or other description otherwise.", "title": "Output" } }, "title": "CodeExecutionResult", "type": "object" }, "Content": { "additionalProperties": false, "description": "Contains the multi-part content of a message.", "properties": { "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/Part" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a single message. Each part may have\n a different IANA MIME type.", "title": "Parts" }, "role": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The producer of the content. Must be either 'user' or 'model'. Useful to set for multi-turn conversations, otherwise can be left blank or unset.", "title": "Role" } }, "title": "Content", "type": "object" }, "ExecutableCode": { "additionalProperties": false, "description": "Code generated by the model that is meant to be executed, and the result returned to the model.\n\nGenerated when using the [CodeExecution] tool, in which the code will be\nautomatically executed, and a corresponding [CodeExecutionResult] will also be\ngenerated.", "properties": { "code": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The code to be executed.", "title": "Code" }, "language": { "anyOf": [ { "$ref": "#/$defs/Language" }, { "type": "null" } ], "default": null, "description": "Required. Programming language of the `code`." } }, "title": "ExecutableCode", "type": "object" }, "FileData": { "additionalProperties": false, "description": "URI based data.", "properties": { "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file data. Used to provide a label or filename to distinguish file datas. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "FileData", "type": "object" }, "FunctionCall": { "additionalProperties": false, "description": "A function call.", "properties": { "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The unique id of the function call. If populated, the client to execute the\n `function_call` and return the response with the matching `id`.", "title": "Id" }, "args": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Optional. The function parameters and values in JSON object format. See [FunctionDeclaration.parameters] for parameter details.", "title": "Args" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The name of the function to call. Matches [FunctionDeclaration.name].", "title": "Name" }, "partialArgs": { "anyOf": [ { "items": { "$ref": "#/$defs/PartialArg" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. The partial argument value of the function call. If provided, represents the arguments/fields that are streamed incrementally. This field is not supported in Gemini API.", "title": "Partialargs" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is the last part of the FunctionCall. If true, another partial message for the current FunctionCall is expected to follow. This field is not supported in Gemini API.", "title": "Willcontinue" } }, "title": "FunctionCall", "type": "object" }, "FunctionResponse": { "additionalProperties": false, "description": "A function response.", "properties": { "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Signals that function call continues, and more responses will be returned, turning the function call into a generator. Is only applicable to NON_BLOCKING function calls (see FunctionDeclaration.behavior for details), ignored otherwise. If false, the default, future responses will not be considered. Is only applicable to NON_BLOCKING function calls, is ignored otherwise. If set to false, future responses will not be considered. It is allowed to return empty `response` with `will_continue=False` to signal that the function call is finished.", "title": "Willcontinue" }, "scheduling": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseScheduling" }, { "type": "null" } ], "default": null, "description": "Specifies how the response should be scheduled in the conversation. Only applicable to NON_BLOCKING function calls, is ignored otherwise. Defaults to WHEN_IDLE." }, "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/FunctionResponsePart" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a function response. Each part may\n have a different IANA MIME type.", "title": "Parts" }, "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The id of the function call this response is for. Populated by the client to match the corresponding function call `id`.", "title": "Id" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The name of the function to call. Matches [FunctionDeclaration.name] and [FunctionCall.name].", "title": "Name" }, "response": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Required. The function response in JSON object format. Use \"output\" key to specify function output and \"error\" key to specify error details (if any). If \"output\" and \"error\" keys are not specified, then whole \"response\" is treated as function output.", "title": "Response" } }, "title": "FunctionResponse", "type": "object" }, "FunctionResponseBlob": { "additionalProperties": false, "description": "Raw media bytes for function response.\n\nText should not be sent as raw bytes, use the FunctionResponse.response\nfield.", "properties": { "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Inline media bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob.\n Used to provide a label or filename to distinguish blobs.", "title": "Displayname" } }, "title": "FunctionResponseBlob", "type": "object" }, "FunctionResponseFileData": { "additionalProperties": false, "description": "URI based data for function response.", "properties": { "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file.\n Used to provide a label or filename to distinguish files.", "title": "Displayname" } }, "title": "FunctionResponseFileData", "type": "object" }, "FunctionResponsePart": { "additionalProperties": false, "description": "A datatype containing media that is part of a `FunctionResponse` message.\n\nA `FunctionResponsePart` consists of data which has an associated datatype. A\n`FunctionResponsePart` can only contain one of the accepted types in\n`FunctionResponsePart.data`.\n\nA `FunctionResponsePart` must have a fixed IANA MIME type identifying the\ntype and subtype of the media if the `inline_data` field is filled with raw\nbytes.", "properties": { "inlineData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseBlob" }, { "type": "null" } ], "default": null, "description": "Optional. Inline media bytes." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseFileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." } }, "title": "FunctionResponsePart", "type": "object" }, "FunctionResponseScheduling": { "description": "Specifies how the response should be scheduled in the conversation.", "enum": [ "SCHEDULING_UNSPECIFIED", "SILENT", "WHEN_IDLE", "INTERRUPT" ], "title": "FunctionResponseScheduling", "type": "string" }, "Language": { "description": "Programming language of the `code`.", "enum": [ "LANGUAGE_UNSPECIFIED", "PYTHON" ], "title": "Language", "type": "string" }, "Outcome": { "description": "Outcome of the code execution.", "enum": [ "OUTCOME_UNSPECIFIED", "OUTCOME_OK", "OUTCOME_FAILED", "OUTCOME_DEADLINE_EXCEEDED" ], "title": "Outcome", "type": "string" }, "Part": { "additionalProperties": false, "description": "A datatype containing media content.\n\nExactly one field within a Part should be set, representing the specific type\nof content being conveyed. Using multiple fields within the same `Part`\ninstance is considered invalid.", "properties": { "mediaResolution": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolution" }, { "type": "null" } ], "default": null, "description": "Media resolution for the input media.\n " }, "codeExecutionResult": { "anyOf": [ { "$ref": "#/$defs/CodeExecutionResult" }, { "type": "null" } ], "default": null, "description": "Optional. Result of executing the [ExecutableCode]." }, "executableCode": { "anyOf": [ { "$ref": "#/$defs/ExecutableCode" }, { "type": "null" } ], "default": null, "description": "Optional. Code generated by the model that is meant to be executed." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." }, "functionCall": { "anyOf": [ { "$ref": "#/$defs/FunctionCall" }, { "type": "null" } ], "default": null, "description": "Optional. A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] with the parameters and their values." }, "functionResponse": { "anyOf": [ { "$ref": "#/$defs/FunctionResponse" }, { "type": "null" } ], "default": null, "description": "Optional. The result output of a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function call. It is used as context to the model." }, "inlineData": { "anyOf": [ { "$ref": "#/$defs/Blob" }, { "type": "null" } ], "default": null, "description": "Optional. Inlined bytes data." }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Text part (can be code).", "title": "Text" }, "thought": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Indicates if the part is thought from the model.", "title": "Thought" }, "thoughtSignature": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. An opaque signature for the thought so it can be reused in subsequent requests.", "title": "Thoughtsignature" }, "videoMetadata": { "anyOf": [ { "$ref": "#/$defs/VideoMetadata" }, { "type": "null" } ], "default": null, "description": "Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data." } }, "title": "Part", "type": "object" }, "PartMediaResolution": { "additionalProperties": false, "description": "Media resolution for the input media.", "properties": { "level": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolutionLevel" }, { "type": "null" } ], "default": null, "description": "The tokenization quality used for given media.\n " }, "numTokens": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Specifies the required sequence length for media tokenization.\n ", "title": "Numtokens" } }, "title": "PartMediaResolution", "type": "object" }, "PartMediaResolutionLevel": { "description": "The tokenization quality used for given media.", "enum": [ "MEDIA_RESOLUTION_UNSPECIFIED", "MEDIA_RESOLUTION_LOW", "MEDIA_RESOLUTION_MEDIUM", "MEDIA_RESOLUTION_HIGH", "MEDIA_RESOLUTION_ULTRA_HIGH" ], "title": "PartMediaResolutionLevel", "type": "string" }, "PartialArg": { "additionalProperties": false, "description": "Partial argument value of the function call.\n\nThis data type is not supported in Gemini API.", "properties": { "nullValue": { "anyOf": [ { "const": "NULL_VALUE", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a null value.", "title": "Nullvalue" }, "numberValue": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a double value.", "title": "Numbervalue" }, "stringValue": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a string value.", "title": "Stringvalue" }, "boolValue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a boolean value.", "title": "Boolvalue" }, "jsonPath": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. A JSON Path (RFC 9535) to the argument being streamed. https://datatracker.ietf.org/doc/html/rfc9535. e.g. \"$.foo.bar[0].data\".", "title": "Jsonpath" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is not the last part of the same json_path. If true, another PartialArg message for the current json_path is expected to follow.", "title": "Willcontinue" } }, "title": "PartialArg", "type": "object" }, "VideoMetadata": { "additionalProperties": false, "description": "Metadata describes the input video content.", "properties": { "endOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The end offset of the video.", "title": "Endoffset" }, "fps": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. The frame rate of the video sent to the model. If not specified, the default value will be 1.0. The fps range is (0.0, 24.0].", "title": "Fps" }, "startOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The start offset of the video.", "title": "Startoffset" } }, "title": "VideoMetadata", "type": "object" } }, "required": [ "input", "output" ] }

- Fields:
`input (google.genai.types.Content)`

`output (list[google.genai.types.Content])`


-
*field*input*: Content**[Required]*[¶](#id21)

-
*field*output*: list[Content]**[Required]*[¶](#id22)

-
input

-
*class*google.adk.examples.VertexAiExampleStore(*examples_store_name*)[¶](#google.adk.examples.VertexAiExampleStore) Bases:

`BaseExampleProvider`

Provides examples from Vertex example store.

Initializes the VertexAiExampleStore.

- Parameters:
**examples_store_name**– The resource name of the vertex example store, in the format of`projects/{project}/locations/{location}/exampleStores/{example_store}`

.


# google.adk.flows module[¶](#module-google.adk.flows)

# google.adk.memory module[¶](#module-google.adk.memory)

-
*class*google.adk.memory.BaseMemoryService[¶](#google.adk.memory.BaseMemoryService) Bases:

`ABC`

Base class for memory services.

The service provides functionalities to ingest sessions into memory so that the memory can be used for user queries.

-
*abstractmethod async*add_session_to_memory(*session*)[¶](#google.adk.memory.BaseMemoryService.add_session_to_memory) Adds a session to the memory service.

A session may be added multiple times during its lifetime.

- Parameters:
**session**– The session to add.


-
*abstractmethod async*search_memory(***,*app_name*,*user_id*,*query*)[¶](#google.adk.memory.BaseMemoryService.search_memory) Searches for sessions that match the query.

- Return type:
`SearchMemoryResponse`

- Parameters:
**app_name**– The name of the application.**user_id**– The id of the user.**query**– The query to search for.

- Returns:
A SearchMemoryResponse containing the matching memories.


-

-
*class*google.adk.memory.InMemoryMemoryService[¶](#google.adk.memory.InMemoryMemoryService) Bases:

`BaseMemoryService`

An in-memory memory service for prototyping purpose only.

Uses keyword matching instead of semantic search.

This class is thread-safe, however, it should be used for testing and development only.

-
*async*add_session_to_memory(*session*)[¶](#google.adk.memory.InMemoryMemoryService.add_session_to_memory) Adds a session to the memory service.

A session may be added multiple times during its lifetime.

- Parameters:
**session**– The session to add.


-
*async*search_memory(***,*app_name*,*user_id*,*query*)[¶](#google.adk.memory.InMemoryMemoryService.search_memory) Searches for sessions that match the query.

- Return type:
`SearchMemoryResponse`

- Parameters:
**app_name**– The name of the application.**user_id**– The id of the user.**query**– The query to search for.

- Returns:
A SearchMemoryResponse containing the matching memories.


-

-
*class*google.adk.memory.VertexAiMemoryBankService(*project=None*,*location=None*,*agent_engine_id=None*,***,*express_mode_api_key=None*)[¶](#google.adk.memory.VertexAiMemoryBankService) Bases:

`BaseMemoryService`

Implementation of the BaseMemoryService using Vertex AI Memory Bank.

Initializes a VertexAiMemoryBankService.

- Parameters:
**project**– The project ID of the Memory Bank to use.**location**– The location of the Memory Bank to use.**agent_engine_id**– The ID of the agent engine to use for the Memory Bank, e.g. ‘456’ in ‘projects/my-project/locations/us-central1/reasoningEngines/456’. To extract from api_resource.name, use:`agent_engine.api_resource.name.split('/')[-1]`

**express_mode_api_key**– The API key to use for Express Mode. If not provided, the API key from the GOOGLE_API_KEY environment variable will be used. It will only be used if GOOGLE_GENAI_USE_VERTEXAI is true. Do not use Google AI Studio API key for this field. For more details, visit[https://cloud.google.com/vertex-ai/generative-ai/docs/start/express-mode/overview](https://cloud.google.com/vertex-ai/generative-ai/docs/start/express-mode/overview)


-
*async*add_session_to_memory(*session*)[¶](#google.adk.memory.VertexAiMemoryBankService.add_session_to_memory) Adds a session to the memory service.

A session may be added multiple times during its lifetime.

- Parameters:
**session**– The session to add.


-
*async*search_memory(***,*app_name*,*user_id*,*query*)[¶](#google.adk.memory.VertexAiMemoryBankService.search_memory) Searches for sessions that match the query.

- Parameters:
**app_name**– The name of the application.**user_id**– The id of the user.**query**– The query to search for.

- Returns:
A SearchMemoryResponse containing the matching memories.


-
*class*google.adk.memory.VertexAiRagMemoryService(*rag_corpus=None*,*similarity_top_k=None*,*vector_distance_threshold=10*)[¶](#google.adk.memory.VertexAiRagMemoryService) Bases:

`BaseMemoryService`

A memory service that uses Vertex AI RAG for storage and retrieval.

Initializes a VertexAiRagMemoryService.

- Parameters:
**rag_corpus**– The name of the Vertex AI RAG corpus to use. Format:`projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}`

or`{rag_corpus_id}`

**similarity_top_k**– The number of contexts to retrieve.**vector_distance_threshold**– Only returns contexts with vector distance smaller than the threshold..


-
*async*add_session_to_memory(*session*)[¶](#google.adk.memory.VertexAiRagMemoryService.add_session_to_memory) Adds a session to the memory service.

A session may be added multiple times during its lifetime.

- Parameters:
**session**– The session to add.


-
*async*search_memory(***,*app_name*,*user_id*,*query*)[¶](#google.adk.memory.VertexAiRagMemoryService.search_memory) Searches for sessions that match the query using rag.retrieval_query.

- Return type:
`SearchMemoryResponse`


# google.adk.models module[¶](#module-google.adk.models)

Defines the interface to support a model.

-
*pydantic model*google.adk.models.BaseLlm[¶](#google.adk.models.BaseLlm) Bases:

`BaseModel`

The BaseLLM class.

## Show JSON schema

{ "title": "BaseLlm", "description": "The BaseLLM class.", "type": "object", "properties": { "model": { "title": "Model", "type": "string" } }, "required": [ "model" ] }

- Fields:
`model (str)`


-
*field*model*: str**[Required]*[¶](#google.adk.models.BaseLlm.model) The name of the LLM, e.g. gemini-2.5-flash or gemini-2.5-pro.


-
*classmethod*supported_models()[¶](#google.adk.models.BaseLlm.supported_models) Returns a list of supported models in regex for LlmRegistry.

- Return type:
`list`

[`str`

]


-
connect(
*llm_request*)[¶](#google.adk.models.BaseLlm.connect) Creates a live connection to the LLM.

- Return type:
`BaseLlmConnection`

- Parameters:
**llm_request**– LlmRequest, the request to send to the LLM.- Returns:
BaseLlmConnection, the connection to the LLM.


-
*abstractmethod async*generate_content_async(*llm_request*,*stream=False*)[¶](#google.adk.models.BaseLlm.generate_content_async) Generates content for a single model turn.

This method handles Server-Sent Events (SSE) streaming for unidirectional content generation. For bidirectional streaming (e.g., Gemini Live API), use the connect() method instead.

- Args:
llm_request: LlmRequest, the request to send to the LLM. stream: bool = False, whether to enable SSE streaming mode.

- Yields:
LlmResponse objects representing the model’s response for one turn.

**Non-streaming mode (stream=False):**Yields exactly one LlmResponse containing the complete model output (text, function calls, bytes, etc.). This response has partial=False.

**Streaming mode (stream=True):**Yields multiple LlmResponse objects as chunks arrive:

Intermediate chunks: partial=True (progressive updates)

Final chunk: partial=False (aggregated content from entire turn, identical to stream=False output)

Text consolidation: Consecutive text parts of the same type (thought/non-thought) SHOULD merge without separator, but client code must not rely on this - unconsolidated parts are unusual but also valid


**Common content in partial chunks:**All intermediate chunks have partial=True regardless of content type. Common examples include:

Text: Streams incrementally as tokens arrive

Function calls: May arrive in separate chunks

Bytes (e.g., images): Typically arrive as single chunk, interleaved with text

Thoughts: Stream incrementally when thinking_config is enabled


**Examples:**Simple text streaming:

LlmResponse(partial=True, parts=["The weather"]) LlmResponse(partial=True, parts=[" in Tokyo is"]) LlmResponse(partial=True, parts=[" sunny."]) LlmResponse(partial=False, parts=["The weather in Tokyo is sunny."])

Text + function call:

LlmResponse(partial=True, parts=[Text("Let me check...")]) LlmResponse(partial=True, parts=[FunctionCall("get_weather", ...)]) LlmResponse(partial=False, parts=[Text("Let me check..."), FunctionCall("get_weather", ...)])

Parallel function calls across chunks:

LlmResponse(partial=True, parts=[Text("Checking both cities...")]) LlmResponse(partial=True, parts=[FunctionCall("get_weather", Tokyo)]) LlmResponse(partial=True, parts=[FunctionCall("get_weather", NYC)]) LlmResponse(partial=False, parts=[Text("Checking both cities..."), FunctionCall("get_weather", Tokyo), FunctionCall("get_weather", NYC)])

Text + bytes (image generation with gemini-2.5-flash-image):

LlmResponse(partial=True, parts=[Text("Here's an image of a dog.")]) LlmResponse(partial=True, parts=[Text("


- “)])
LlmResponse(partial=True, parts=[Blob(image/png, 1.6MB)]) LlmResponse(partial=True, parts=[Text(“It carries a bone”)]) LlmResponse(partial=True, parts=[Text(” and running around.”)]) LlmResponse(partial=False, parts=[Text(“Here’s an image of a dog.

- “),
Blob(image/png, 1.6MB), Text(“It carries a bone and running around.”)])

Note: Consecutive text parts before and after blob merge separately.

Text with thinking (gemini-2.5-flash with thinking_config):

LlmResponse(partial=True, parts=[Thought("Let me analyze...")]) LlmResponse(partial=True, parts=[Thought("The user wants...")]) LlmResponse(partial=True, parts=[Text("Based on my analysis,")]) LlmResponse(partial=True, parts=[Text(" the answer is 42.")]) LlmResponse(partial=False, parts=[Thought("Let me analyze...The user wants..."), Text("Based on my analysis, the answer is 42.")])

Note: Consecutive parts of same type merge (thoughts→thought, text→text).


**Important:**All yielded responses represent one logical model turn. The final response with partial=False should be identical to the response that would be received with stream=False.

- Return type:
`AsyncGenerator`

[`LlmResponse`

,`None`

]


-
*pydantic model*google.adk.models.Gemini[¶](#google.adk.models.Gemini) Bases:

`BaseLlm`

Integration for Gemini models.

-
model
[¶](#google.adk.models.Gemini.model) The name of the Gemini model.


-
use_interactions_api
[¶](#google.adk.models.Gemini.use_interactions_api) Whether to use the interactions API for model invocation.


## Show JSON schema

{ "title": "Gemini", "description": "Integration for Gemini models.\n\nAttributes:\n model: The name of the Gemini model.\n use_interactions_api: Whether to use the interactions API for model\n invocation.", "type": "object", "properties": { "model": { "default": "gemini-2.5-flash", "title": "Model", "type": "string" }, "speech_config": { "anyOf": [ { "$ref": "#/$defs/SpeechConfig" }, { "type": "null" } ], "default": null }, "use_interactions_api": { "default": false, "title": "Use Interactions Api", "type": "boolean" }, "retry_options": { "anyOf": [ { "$ref": "#/$defs/HttpRetryOptions" }, { "type": "null" } ], "default": null } }, "$defs": { "HttpRetryOptions": { "additionalProperties": false, "description": "HTTP retry options to be used in each of the requests.", "properties": { "attempts": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Maximum number of attempts, including the original request.\n If 0 or 1, it means no retries. If not specified, default to 5.", "title": "Attempts" }, "initialDelay": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Initial delay before the first retry, in fractions of a second. If not specified, default to 1.0 second.", "title": "Initialdelay" }, "maxDelay": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Maximum delay between retries, in fractions of a second. If not specified, default to 60.0 seconds.", "title": "Maxdelay" }, "expBase": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Multiplier by which the delay increases after each attempt. If not specified, default to 2.0.", "title": "Expbase" }, "jitter": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Randomness factor for the delay. If not specified, default to 1.0.", "title": "Jitter" }, "httpStatusCodes": { "anyOf": [ { "items": { "type": "integer" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of HTTP status codes that should trigger a retry.\n If not specified, a default set of retryable codes (408, 429, and 5xx) may be used.", "title": "Httpstatuscodes" } }, "title": "HttpRetryOptions", "type": "object" }, "MultiSpeakerVoiceConfig": { "additionalProperties": false, "description": "Configuration for a multi-speaker text-to-speech request.", "properties": { "speakerVoiceConfigs": { "anyOf": [ { "items": { "$ref": "#/$defs/SpeakerVoiceConfig" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Required. A list of configurations for the voices of the speakers. Exactly two speaker voice configurations must be provided.", "title": "Speakervoiceconfigs" } }, "title": "MultiSpeakerVoiceConfig", "type": "object" }, "PrebuiltVoiceConfig": { "additionalProperties": false, "description": "The configuration for the prebuilt speaker to use.", "properties": { "voiceName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The name of the preset voice to use.", "title": "Voicename" } }, "title": "PrebuiltVoiceConfig", "type": "object" }, "ReplicatedVoiceConfig": { "additionalProperties": false, "description": "ReplicatedVoiceConfig is used to configure replicated voice.", "properties": { "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The mime type of the replicated voice.\n ", "title": "Mimetype" }, "voiceSampleAudio": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "The sample audio of the replicated voice.\n ", "title": "Voicesampleaudio" } }, "title": "ReplicatedVoiceConfig", "type": "object" }, "SpeakerVoiceConfig": { "additionalProperties": false, "description": "Configuration for a single speaker in a multi speaker setup.", "properties": { "speaker": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The name of the speaker. This should be the same as the speaker name used in the prompt.", "title": "Speaker" }, "voiceConfig": { "anyOf": [ { "$ref": "#/$defs/VoiceConfig" }, { "type": "null" } ], "default": null, "description": "Required. The configuration for the voice of this speaker." } }, "title": "SpeakerVoiceConfig", "type": "object" }, "SpeechConfig": { "additionalProperties": false, "properties": { "voiceConfig": { "anyOf": [ { "$ref": "#/$defs/VoiceConfig" }, { "type": "null" } ], "default": null, "description": "Configuration for the voice of the response." }, "languageCode": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Language code (ISO 639. e.g. en-US) for the speech synthesization.", "title": "Languagecode" }, "multiSpeakerVoiceConfig": { "anyOf": [ { "$ref": "#/$defs/MultiSpeakerVoiceConfig" }, { "type": "null" } ], "default": null, "description": "The configuration for a multi-speaker text-to-speech request. This field is mutually exclusive with `voice_config`." } }, "title": "SpeechConfig", "type": "object" }, "VoiceConfig": { "additionalProperties": false, "properties": { "replicatedVoiceConfig": { "anyOf": [ { "$ref": "#/$defs/ReplicatedVoiceConfig" }, { "type": "null" } ], "default": null, "description": "If true, the model will use a replicated voice for the response." }, "prebuiltVoiceConfig": { "anyOf": [ { "$ref": "#/$defs/PrebuiltVoiceConfig" }, { "type": "null" } ], "default": null, "description": "The configuration for the prebuilt voice to use." } }, "title": "VoiceConfig", "type": "object" } } }

- Fields:
`model (str)`

`retry_options (Optional[types.HttpRetryOptions])`

`speech_config (Optional[types.SpeechConfig])`

`use_interactions_api (bool)`


-
*field*model*: str**= 'gemini-2.5-flash'*[¶](#id23) The name of the LLM, e.g. gemini-2.5-flash or gemini-2.5-pro.


-
*field*retry_options*: types.HttpRetryOptions | None**= None*[¶](#google.adk.models.Gemini.retry_options) Allow Gemini to retry failed responses.

Sample:

[``](#id24)[`](#id26)python from google.genai import types# …

- agent = Agent(
- model=Gemini(
retry_options=types.HttpRetryOptions(initial_delay=1, attempts=2),


)


## )

[¶](#id28)

-
*field*speech_config*: types.SpeechConfig | None**= None*[¶](#google.adk.models.Gemini.speech_config)

-
*field*use_interactions_api*: bool**= False*[¶](#id29) Whether to use the interactions API for model invocation.

When enabled, uses the interactions API (client.aio.interactions.create()) instead of the traditional generate_content API. The interactions API provides stateful conversation capabilities, allowing you to chain interactions using previous_interaction_id instead of sending full history. The response format will be converted to match the existing LlmResponse structure for compatibility.

Sample:

[``](#id30)[`](#id32)python agent = Agent(model=Gemini(use_interactions_api=True)

## )

[¶](#id34)

-
*classmethod*supported_models()[¶](#google.adk.models.Gemini.supported_models) Provides the list of supported models.

- Return type:
`list`

[`str`

]- Returns:
A list of supported models.


-
connect(
*llm_request*)[¶](#google.adk.models.Gemini.connect) Connects to the Gemini model and returns an llm connection.

- Return type:
`BaseLlmConnection`

- Parameters:
**llm_request**– LlmRequest, the request to send to the Gemini model.- Yields:
BaseLlmConnection, the connection to the Gemini model.


-
*async*generate_content_async(*llm_request*,*stream=False*)[¶](#google.adk.models.Gemini.generate_content_async) Sends a request to the Gemini model.

- Return type:
`AsyncGenerator`

[`LlmResponse`

,`None`

]- Parameters:
**llm_request**– LlmRequest, the request to send to the Gemini model.**stream**– bool = False, whether to do streaming call.

- Yields:
*LlmResponse*– The model response.


-
*property*api_client*: Client*[¶](#google.adk.models.Gemini.api_client) Provides the api client.

- Returns:
The api client.


-
model

-
*pydantic model*google.adk.models.Gemma[¶](#google.adk.models.Gemma) Bases:

`GemmaFunctionCallingMixin`

,`Gemini`

Integration for Gemma models exposed via the Gemini API.

Only Gemma 3 models are supported at this time. For agentic use cases, use of gemma-3-27b-it and gemma-3-12b-it are strongly recommended.

For full documentation, see:

[https://ai.google.dev/gemma/docs/core/](https://ai.google.dev/gemma/docs/core/)NOTE: Gemma does

**NOT**support system instructions. Any system instructions will be replaced with an initial*user*prompt in the LLM request. If system instructions change over the course of agent execution, the initial content**SHOULD**be replaced. Special care is warranted here. See:[https://ai.google.dev/gemma/docs/core/prompt-structure#system-instructions](https://ai.google.dev/gemma/docs/core/prompt-structure#system-instructions)NOTE: Gemma’s function calling support is limited. It does not have full access to the same built-in tools as Gemini. It also does not have special API support for tools and functions. Rather, tools must be passed in via a user prompt, and extracted from model responses based on approximate shape.

NOTE: Vertex AI API support for Gemma is not currently included. This

**ONLY**supports usage via the Gemini API.## Show JSON schema

{ "title": "Gemma", "description": "Integration for Gemma models exposed via the Gemini API.\n\nOnly Gemma 3 models are supported at this time. For agentic use cases,\nuse of gemma-3-27b-it and gemma-3-12b-it are strongly recommended.\n\nFor full documentation, see: https://ai.google.dev/gemma/docs/core/\n\nNOTE: Gemma does **NOT** support system instructions. Any system instructions\nwill be replaced with an initial *user* prompt in the LLM request. If system\ninstructions change over the course of agent execution, the initial content\n**SHOULD** be replaced. Special care is warranted here.\nSee:\nhttps://ai.google.dev/gemma/docs/core/prompt-structure#system-instructions\n\nNOTE: Gemma's function calling support is limited. It does not have full\naccess to the\nsame built-in tools as Gemini. It also does not have special API support for\ntools and\nfunctions. Rather, tools must be passed in via a `user` prompt, and extracted\nfrom model\nresponses based on approximate shape.\n\nNOTE: Vertex AI API support for Gemma is not currently included. This **ONLY**\nsupports\nusage via the Gemini API.", "type": "object", "properties": { "model": { "default": "gemma-3-27b-it", "title": "Model", "type": "string" }, "speech_config": { "anyOf": [ { "$ref": "#/$defs/SpeechConfig" }, { "type": "null" } ], "default": null }, "use_interactions_api": { "default": false, "title": "Use Interactions Api", "type": "boolean" }, "retry_options": { "anyOf": [ { "$ref": "#/$defs/HttpRetryOptions" }, { "type": "null" } ], "default": null } }, "$defs": { "HttpRetryOptions": { "additionalProperties": false, "description": "HTTP retry options to be used in each of the requests.", "properties": { "attempts": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Maximum number of attempts, including the original request.\n If 0 or 1, it means no retries. If not specified, default to 5.", "title": "Attempts" }, "initialDelay": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Initial delay before the first retry, in fractions of a second. If not specified, default to 1.0 second.", "title": "Initialdelay" }, "maxDelay": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Maximum delay between retries, in fractions of a second. If not specified, default to 60.0 seconds.", "title": "Maxdelay" }, "expBase": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Multiplier by which the delay increases after each attempt. If not specified, default to 2.0.", "title": "Expbase" }, "jitter": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Randomness factor for the delay. If not specified, default to 1.0.", "title": "Jitter" }, "httpStatusCodes": { "anyOf": [ { "items": { "type": "integer" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of HTTP status codes that should trigger a retry.\n If not specified, a default set of retryable codes (408, 429, and 5xx) may be used.", "title": "Httpstatuscodes" } }, "title": "HttpRetryOptions", "type": "object" }, "MultiSpeakerVoiceConfig": { "additionalProperties": false, "description": "Configuration for a multi-speaker text-to-speech request.", "properties": { "speakerVoiceConfigs": { "anyOf": [ { "items": { "$ref": "#/$defs/SpeakerVoiceConfig" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Required. A list of configurations for the voices of the speakers. Exactly two speaker voice configurations must be provided.", "title": "Speakervoiceconfigs" } }, "title": "MultiSpeakerVoiceConfig", "type": "object" }, "PrebuiltVoiceConfig": { "additionalProperties": false, "description": "The configuration for the prebuilt speaker to use.", "properties": { "voiceName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The name of the preset voice to use.", "title": "Voicename" } }, "title": "PrebuiltVoiceConfig", "type": "object" }, "ReplicatedVoiceConfig": { "additionalProperties": false, "description": "ReplicatedVoiceConfig is used to configure replicated voice.", "properties": { "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The mime type of the replicated voice.\n ", "title": "Mimetype" }, "voiceSampleAudio": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "The sample audio of the replicated voice.\n ", "title": "Voicesampleaudio" } }, "title": "ReplicatedVoiceConfig", "type": "object" }, "SpeakerVoiceConfig": { "additionalProperties": false, "description": "Configuration for a single speaker in a multi speaker setup.", "properties": { "speaker": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The name of the speaker. This should be the same as the speaker name used in the prompt.", "title": "Speaker" }, "voiceConfig": { "anyOf": [ { "$ref": "#/$defs/VoiceConfig" }, { "type": "null" } ], "default": null, "description": "Required. The configuration for the voice of this speaker." } }, "title": "SpeakerVoiceConfig", "type": "object" }, "SpeechConfig": { "additionalProperties": false, "properties": { "voiceConfig": { "anyOf": [ { "$ref": "#/$defs/VoiceConfig" }, { "type": "null" } ], "default": null, "description": "Configuration for the voice of the response." }, "languageCode": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Language code (ISO 639. e.g. en-US) for the speech synthesization.", "title": "Languagecode" }, "multiSpeakerVoiceConfig": { "anyOf": [ { "$ref": "#/$defs/MultiSpeakerVoiceConfig" }, { "type": "null" } ], "default": null, "description": "The configuration for a multi-speaker text-to-speech request. This field is mutually exclusive with `voice_config`." } }, "title": "SpeechConfig", "type": "object" }, "VoiceConfig": { "additionalProperties": false, "properties": { "replicatedVoiceConfig": { "anyOf": [ { "$ref": "#/$defs/ReplicatedVoiceConfig" }, { "type": "null" } ], "default": null, "description": "If true, the model will use a replicated voice for the response." }, "prebuiltVoiceConfig": { "anyOf": [ { "$ref": "#/$defs/PrebuiltVoiceConfig" }, { "type": "null" } ], "default": null, "description": "The configuration for the prebuilt voice to use." } }, "title": "VoiceConfig", "type": "object" } } }

- Fields:
`model (str)`


-
*field*model*: str**= 'gemma-3-27b-it'*[¶](#google.adk.models.Gemma.model) The name of the LLM, e.g. gemini-2.5-flash or gemini-2.5-pro.


-
*classmethod*supported_models()[¶](#google.adk.models.Gemma.supported_models) Provides the list of supported models.

Returns: A list of supported models.

- Return type:
`list`

[`str`

]


-
*async*generate_content_async(*llm_request*,*stream=False*)[¶](#google.adk.models.Gemma.generate_content_async) Sends a request to the Gemma model.

- Return type:
`AsyncGenerator`

[`LlmResponse`

,`None`

]- Parameters:
**llm_request**– LlmRequest, the request to send to the Gemini model.**stream**– bool = False, whether to do streaming call.

- Yields:
*LlmResponse*– The model response.


-
*class*google.adk.models.LLMRegistry[¶](#google.adk.models.LLMRegistry) Bases:

`object`

Registry for LLMs.

-
*static*new_llm(*model*)[¶](#google.adk.models.LLMRegistry.new_llm) Creates a new LLM instance.

- Return type:
- Parameters:
**model**– The model name.- Returns:
The LLM instance.


-
*static*register(*llm_cls*)[¶](#google.adk.models.LLMRegistry.register) Registers a new LLM class.

- Parameters:
**llm_cls**– The class that implements the model.


-

# google.adk.planners module[¶](#module-google.adk.planners)

-
*class*google.adk.planners.BasePlanner[¶](#google.adk.planners.BasePlanner) Bases:

`ABC`

Abstract base class for all planners.

The planner allows the agent to generate plans for the queries to guide its action.

-
*abstractmethod*build_planning_instruction(*readonly_context*,*llm_request*)[¶](#google.adk.planners.BasePlanner.build_planning_instruction) Builds the system instruction to be appended to the LLM request for planning.

- Return type:
`Optional`

[`str`

]- Parameters:
**readonly_context**– The readonly context of the invocation.**llm_request**– The LLM request. Readonly.

- Returns:
The planning system instruction, or None if no instruction is needed.


-
*abstractmethod*process_planning_response(*callback_context*,*response_parts*)[¶](#google.adk.planners.BasePlanner.process_planning_response) Processes the LLM response for planning.

- Return type:
`Optional`

[`List`

[`Part`

]]- Parameters:
**callback_context**– The callback context of the invocation.**response_parts**– The LLM response parts. Readonly.

- Returns:
The processed response parts, or None if no processing is needed.


-

-
*class*google.adk.planners.BuiltInPlanner(***,*thinking_config*)[¶](#google.adk.planners.BuiltInPlanner) Bases:

`BasePlanner`

The built-in planner that uses model’s built-in thinking features.

-
thinking_config
[¶](#google.adk.planners.BuiltInPlanner.thinking_config) Config for model built-in thinking features. An error will be returned if this field is set for models that don’t support thinking.


Initializes the built-in planner.

- Parameters:
**thinking_config**– Config for model built-in thinking features. An error will be returned if this field is set for models that don’t support thinking.

-
apply_thinking_config(
*llm_request*)[¶](#google.adk.planners.BuiltInPlanner.apply_thinking_config) Applies the thinking config to the LLM request.

- Return type:
`None`

- Parameters:
**llm_request**– The LLM request to apply the thinking config to.


-
build_planning_instruction(
*readonly_context*,*llm_request*)[¶](#google.adk.planners.BuiltInPlanner.build_planning_instruction) Builds the system instruction to be appended to the LLM request for planning.

- Return type:
`Optional`

[`str`

]- Parameters:
**readonly_context**– The readonly context of the invocation.**llm_request**– The LLM request. Readonly.

- Returns:
The planning system instruction, or None if no instruction is needed.


-
process_planning_response(
*callback_context*,*response_parts*)[¶](#google.adk.planners.BuiltInPlanner.process_planning_response) Processes the LLM response for planning.

- Return type:
`Optional`

[`List`

[`Part`

]]- Parameters:
**callback_context**– The callback context of the invocation.**response_parts**– The LLM response parts. Readonly.

- Returns:
The processed response parts, or None if no processing is needed.


-
thinking_config
*: ThinkingConfig*[¶](#id35) Config for model built-in thinking features. An error will be returned if this field is set for models that don’t support thinking.


-
thinking_config

-
*class*google.adk.planners.PlanReActPlanner[¶](#google.adk.planners.PlanReActPlanner) Bases:

`BasePlanner`

Plan-Re-Act planner that constrains the LLM response to generate a plan before any action/observation.

Note: this planner does not require the model to support built-in thinking features or setting the thinking config.

-
build_planning_instruction(
*readonly_context*,*llm_request*)[¶](#google.adk.planners.PlanReActPlanner.build_planning_instruction) Builds the system instruction to be appended to the LLM request for planning.

- Return type:
`str`

- Parameters:
**readonly_context**– The readonly context of the invocation.**llm_request**– The LLM request. Readonly.

- Returns:
The planning system instruction, or None if no instruction is needed.


-
process_planning_response(
*callback_context*,*response_parts*)[¶](#google.adk.planners.PlanReActPlanner.process_planning_response) Processes the LLM response for planning.

- Return type:
`Optional`

[`List`

[`Part`

]]- Parameters:
**callback_context**– The callback context of the invocation.**response_parts**– The LLM response parts. Readonly.

- Returns:
The processed response parts, or None if no processing is needed.


-
build_planning_instruction(

# google.adk.platform module[¶](#module-google.adk.platform)

# google.adk.plugins module[¶](#module-google.adk.plugins)

-
*class*google.adk.plugins.BasePlugin(*name*)[¶](#google.adk.plugins.BasePlugin) Bases:

`ABC`

Base class for creating plugins.

Plugins provide a structured way to intercept and modify agent, tool, and LLM behaviors at critical execution points in a callback manner. While agent callbacks apply to a particular agent, plugins applies globally to all agents added in the runner. Plugins are best used for adding custom behaviors like logging, monitoring, caching, or modifying requests and responses at key stages.

A plugin can implement one or more methods of callbacks, but should not implement the same method of callback for multiple times.

Relation with [Agent callbacks](

[https://google.github.io/adk-docs/callbacks/](https://google.github.io/adk-docs/callbacks/)):**Execution Order**Similar to Agent callbacks, Plugins are executed in the order they are registered. However, Plugin and Agent Callbacks are executed sequentially, with Plugins takes precedence over agent callbacks. When the callback in a plugin returns a value, it will short circuit all remaining plugins and agent callbacks, causing all remaining plugins and agent callbacks to be skipped.**Change Propagation**Plugins and agent callbacks can both modify the value of the input parameters, including agent input, tool input, and LLM request/response, etc. They work in the exactly same way. The modifications will be visible and passed to the next callback in the chain. For example, if a plugin modifies the tool input with before_tool_callback, the modified tool input will be passed to the before_tool_callback of the next plugin, and further passed to the agent callbacks if not short circuited.To use a plugin, implement the desired callback methods and pass an instance of your custom plugin class to the ADK Runner.

Examples

A simple plugin that logs every tool call.

>>> class ToolLoggerPlugin(BasePlugin): .. def __init__(self): .. super().__init__(name="tool_logger") .. .. async def before_tool_callback( .. self, *, tool: BaseTool, tool_args: dict[str, Any], tool_context: ToolContext .. ): .. print(f"[{self.name}] Calling tool '{tool.name}' with args: {tool_args}") .. .. async def after_tool_callback( .. self, *, tool: BaseTool, tool_args: dict, tool_context: ToolContext, result: dict .. ): .. print(f"[{self.name}] Tool '{tool.name}' finished with result: {result}") .. >>> # Add the plugin to ADK Runner >>> # runner = Runner( >>> # ... >>> # plugins=[ToolLoggerPlugin(), AgentPolicyPlugin()], >>> # )

Initializes the plugin.

- Parameters:
**name**– A unique identifier for this plugin instance.

-
*async*after_agent_callback(***,*agent*,*callback_context*)[¶](#google.adk.plugins.BasePlugin.after_agent_callback) Callback executed after an agent’s primary logic has completed.

- Return type:
`Optional`

[`Content`

]- Parameters:
**agent**– The agent that has just run.**callback_context**– The context for the agent invocation.

- Returns:
An optional types.Content object. The content to return to the user. When the content is present, the provided content will be used as agent response and appended to event history as agent response.


-
*async*after_model_callback(***,*callback_context*,*llm_response*)[¶](#google.adk.plugins.BasePlugin.after_model_callback) Callback executed after a response is received from the model.

This is the ideal place to log model responses, collect metrics on token usage, or perform post-processing on the raw LlmResponse.

- Return type:
`Optional`

[`LlmResponse`

]- Parameters:
**callback_context**– The context for the current agent call.**llm_response**– The response object received from the model.

- Returns:
An optional value. A non-None return may be used by the framework to modify or replace the response. Returning None allows the original response to be used.


-
*async*after_run_callback(***,*invocation_context*)[¶](#google.adk.plugins.BasePlugin.after_run_callback) Callback executed after an ADK runner run has completed.

This is the final callback in the ADK lifecycle, suitable for cleanup, final logging, or reporting tasks.

- Return type:
`None`

- Parameters:
**invocation_context**– The context for the entire invocation.- Returns:
None


-
*async*after_tool_callback(***,*tool*,*tool_args*,*tool_context*,*result*)[¶](#google.adk.plugins.BasePlugin.after_tool_callback) Callback executed after a tool has been called.

This callback allows for inspecting, logging, or modifying the result returned by a tool.

- Return type:
`Optional`

[`dict`

]- Parameters:
**tool**– The tool instance that has just been executed.**tool_args**– The original arguments that were passed to the tool.**tool_context**– The context specific to the tool execution.**result**– The dictionary returned by the tool invocation.

- Returns:
An optional dictionary. If a dictionary is returned, it will

**replace**the original result from the tool. This allows for post-processing or altering tool outputs. Returning None uses the original, unmodified result.


-
*async*before_agent_callback(***,*agent*,*callback_context*)[¶](#google.adk.plugins.BasePlugin.before_agent_callback) Callback executed before an agent’s primary logic is invoked.

This callback can be used for logging, setup, or to short-circuit the agent’s execution by returning a value.

- Return type:
`Optional`

[`Content`

]- Parameters:
**agent**– The agent that is about to run.**callback_context**– The context for the agent invocation.

- Returns:
An optional types.Content object. If a value is returned, it will bypass the agent’s callbacks and its execution, and return this value directly. Returning None allows the agent to proceed normally.


-
*async*before_model_callback(***,*callback_context*,*llm_request*)[¶](#google.adk.plugins.BasePlugin.before_model_callback) Callback executed before a request is sent to the model.

This provides an opportunity to inspect, log, or modify the LlmRequest object. It can also be used to implement caching by returning a cached LlmResponse, which would skip the actual model call.

- Return type:
`Optional`

[`LlmResponse`

]- Parameters:
**callback_context**– The context for the current agent call.**llm_request**– The prepared request object to be sent to the model.

- Returns:
An optional value. The interpretation of a non-None trigger an early exit and returns the response immediately. Returning None allows the LLM request to proceed normally.


-
*async*before_run_callback(***,*invocation_context*)[¶](#google.adk.plugins.BasePlugin.before_run_callback) Callback executed before the ADK runner runs.

This is the first callback to be called in the lifecycle, ideal for global setup or initialization tasks.

- Return type:
`Optional`

[`Content`

]- Parameters:
**invocation_context**– The context for the entire invocation, containing session information, the root agent, etc.- Returns:
An optional Event to be returned to the ADK. Returning a value to halt execution of the runner and ends the runner with that event. Return None to proceed normally.


-
*async*before_tool_callback(***,*tool*,*tool_args*,*tool_context*)[¶](#google.adk.plugins.BasePlugin.before_tool_callback) Callback executed before a tool is called.

This callback is useful for logging tool usage, input validation, or modifying the arguments before they are passed to the tool.

- Return type:
`Optional`

[`dict`

]- Parameters:
**tool**– The tool instance that is about to be executed.**tool_args**– The dictionary of arguments to be used for invoking the tool.**tool_context**– The context specific to the tool execution.

- Returns:
An optional dictionary. If a dictionary is returned, it will stop the tool execution and return this response immediately. Returning None uses the original, unmodified arguments.


-
*async*close()[¶](#google.adk.plugins.BasePlugin.close) Method executed when the runner is closed.

This method is used for cleanup tasks such as closing network connections or releasing resources.

- Return type:
`None`


-
*async*on_event_callback(***,*invocation_context*,*event*)[¶](#google.adk.plugins.BasePlugin.on_event_callback) Callback executed after an event is yielded from runner.

This is the ideal place to make modification to the event before the event is handled by the underlying agent app.

- Return type:
`Optional`

[]`Event`

- Parameters:
**invocation_context**– The context for the entire invocation.**event**– The event raised by the runner.

- Returns:
An optional value. A non-None return may be used by the framework to modify or replace the response. Returning None allows the original response to be used.


-
*async*on_model_error_callback(***,*callback_context*,*llm_request*,*error*)[¶](#google.adk.plugins.BasePlugin.on_model_error_callback) Callback executed when a model call encounters an error.

This callback provides an opportunity to handle model errors gracefully, potentially providing alternative responses or recovery mechanisms.

- Return type:
`Optional`

[`LlmResponse`

]- Parameters:
**callback_context**– The context for the current agent call.**llm_request**– The request that was sent to the model when the error occurred.**error**– The exception that was raised during model execution.

- Returns:
An optional LlmResponse. If an LlmResponse is returned, it will be used instead of propagating the error. Returning None allows the original error to be raised.


-
*async*on_tool_error_callback(***,*tool*,*tool_args*,*tool_context*,*error*)[¶](#google.adk.plugins.BasePlugin.on_tool_error_callback) Callback executed when a tool call encounters an error.

This callback provides an opportunity to handle tool errors gracefully, potentially providing alternative responses or recovery mechanisms.

- Return type:
`Optional`

[`dict`

]- Parameters:
**tool**– The tool instance that encountered an error.**tool_args**– The arguments that were passed to the tool.**tool_context**– The context specific to the tool execution.**error**– The exception that was raised during tool execution.

- Returns:
An optional dictionary. If a dictionary is returned, it will be used as the tool response instead of propagating the error. Returning None allows the original error to be raised.


-
*async*on_user_message_callback(***,*invocation_context*,*user_message*)[¶](#google.adk.plugins.BasePlugin.on_user_message_callback) Callback executed when a user message is received before an invocation starts.

This callback helps logging and modifying the user message before the runner starts the invocation.

- Return type:
`Optional`

[`Content`

]- Parameters:
**invocation_context**– The context for the entire invocation.**user_message**– The message content input by user.

- Returns:
An optional types.Content to be returned to the ADK. Returning a value to replace the user message. Returning None to proceed normally.


-
*class*google.adk.plugins.LoggingPlugin(*name='logging_plugin'*)[¶](#google.adk.plugins.LoggingPlugin) Bases:

`BasePlugin`

A plugin that logs important information at each callback point.

This plugin helps printing all critical events in the console. It is not a replacement of existing logging in ADK. It rather helps terminal based debugging by showing all logs in the console, and serves as a simple demo for everyone to leverage when developing new plugins.

This plugin helps users track the invocation status by logging: - User messages and invocation context - Agent execution flow - LLM requests and responses - Tool calls with arguments and results - Events and final responses - Errors during model and tool execution

Example

>>> logging_plugin = LoggingPlugin() >>> runner = Runner( ... agents=[my_agent], ... # ... ... plugins=[logging_plugin], ... )

Initialize the logging plugin.

- Parameters:
**name**– The name of the plugin instance.

-
*async*after_agent_callback(***,*agent*,*callback_context*)[¶](#google.adk.plugins.LoggingPlugin.after_agent_callback) Log agent execution completion.

- Return type:
`Optional`

[`Content`

]


-
*async*after_model_callback(***,*callback_context*,*llm_response*)[¶](#google.adk.plugins.LoggingPlugin.after_model_callback) Log LLM response after receiving from model.

- Return type:
`Optional`

[`LlmResponse`

]


-
*async*after_run_callback(***,*invocation_context*)[¶](#google.adk.plugins.LoggingPlugin.after_run_callback) Log invocation completion.

- Return type:
`None`


-
*async*after_tool_callback(***,*tool*,*tool_args*,*tool_context*,*result*)[¶](#google.adk.plugins.LoggingPlugin.after_tool_callback) Log tool execution completion.

- Return type:
`Optional`

[`dict`

]


-
*async*before_agent_callback(***,*agent*,*callback_context*)[¶](#google.adk.plugins.LoggingPlugin.before_agent_callback) Log agent execution start.

- Return type:
`Optional`

[`Content`

]


-
*async*before_model_callback(***,*callback_context*,*llm_request*)[¶](#google.adk.plugins.LoggingPlugin.before_model_callback) Log LLM request before sending to model.

- Return type:
`Optional`

[`LlmResponse`

]


-
*async*before_run_callback(***,*invocation_context*)[¶](#google.adk.plugins.LoggingPlugin.before_run_callback) Log invocation start.

- Return type:
`Optional`

[`Content`

]


-
*async*before_tool_callback(***,*tool*,*tool_args*,*tool_context*)[¶](#google.adk.plugins.LoggingPlugin.before_tool_callback) Log tool execution start.

- Return type:
`Optional`

[`dict`

]


-
*async*on_event_callback(***,*invocation_context*,*event*)[¶](#google.adk.plugins.LoggingPlugin.on_event_callback) Log events yielded from the runner.

- Return type:
`Optional`

[]`Event`


-
*async*on_model_error_callback(***,*callback_context*,*llm_request*,*error*)[¶](#google.adk.plugins.LoggingPlugin.on_model_error_callback) Log LLM error.

- Return type:
`Optional`

[`LlmResponse`

]


-
*async*on_tool_error_callback(***,*tool*,*tool_args*,*tool_context*,*error*)[¶](#google.adk.plugins.LoggingPlugin.on_tool_error_callback) Log tool error.

- Return type:
`Optional`

[`dict`

]


-
*async*on_user_message_callback(***,*invocation_context*,*user_message*)[¶](#google.adk.plugins.LoggingPlugin.on_user_message_callback) Log user message and invocation start.

- Return type:
`Optional`

[`Content`

]


-
*class*google.adk.plugins.PluginManager(*plugins=None*,*close_timeout=5.0*)[¶](#google.adk.plugins.PluginManager) Bases:

`object`

Manages the registration and execution of plugins.

The PluginManager is an internal class that orchestrates the invocation of plugin callbacks at key points in the SDK’s execution lifecycle. It maintains a list of registered plugins and ensures they are called in the order they were registered.

The core execution logic implements an “early exit” strategy: if any plugin callback returns a non-None value, the execution of subsequent plugins for that specific event is halted, and the returned value is propagated up the call stack. This allows plugins to short-circuit operations like agent runs, tool calls, or model requests.

Initializes the plugin service.

- Parameters:
**plugins**– An optional list of plugins to register upon initialization.**close_timeout**– The timeout in seconds for each plugin’s close method.


-
*async*close()[¶](#google.adk.plugins.PluginManager.close) Calls the close method on all registered plugins concurrently.

- Return type:
`None`

- Raises:
**RuntimeError**– If one or more plugins failed to close, containing details of all failures.


-
get_plugin(
*plugin_name*)[¶](#google.adk.plugins.PluginManager.get_plugin) Retrieves a registered plugin by its name.

- Return type:
`Optional`

[]`BasePlugin`

- Parameters:
**plugin_name**– The name of the plugin to retrieve.- Returns:
The plugin instance if found; otherwise, None.


-
register_plugin(
*plugin*)[¶](#google.adk.plugins.PluginManager.register_plugin) Registers a new plugin.

- Return type:
`None`

- Parameters:
**plugin**– The plugin instance to register.- Raises:
**ValueError**– If a plugin with the same name is already registered.


-
*async*run_after_agent_callback(***,*agent*,*callback_context*)[¶](#google.adk.plugins.PluginManager.run_after_agent_callback) Runs the after_agent_callback for all plugins.

- Return type:
`Optional`

[`Content`

]


-
*async*run_after_model_callback(***,*callback_context*,*llm_response*)[¶](#google.adk.plugins.PluginManager.run_after_model_callback) Runs the after_model_callback for all plugins.

- Return type:
`Optional`

[`LlmResponse`

]


-
*async*run_after_run_callback(***,*invocation_context*)[¶](#google.adk.plugins.PluginManager.run_after_run_callback) Runs the after_run_callback for all plugins.

- Return type:
`None`


-
*async*run_after_tool_callback(***,*tool*,*tool_args*,*tool_context*,*result*)[¶](#google.adk.plugins.PluginManager.run_after_tool_callback) Runs the after_tool_callback for all plugins.

- Return type:
`Optional`

[`dict`

]


-
*async*run_before_agent_callback(***,*agent*,*callback_context*)[¶](#google.adk.plugins.PluginManager.run_before_agent_callback) Runs the before_agent_callback for all plugins.

- Return type:
`Optional`

[`Content`

]


-
*async*run_before_model_callback(***,*callback_context*,*llm_request*)[¶](#google.adk.plugins.PluginManager.run_before_model_callback) Runs the before_model_callback for all plugins.

- Return type:
`Optional`

[`LlmResponse`

]


-
*async*run_before_run_callback(***,*invocation_context*)[¶](#google.adk.plugins.PluginManager.run_before_run_callback) Runs the before_run_callback for all plugins.

- Return type:
`Optional`

[`Content`

]


-
*async*run_before_tool_callback(***,*tool*,*tool_args*,*tool_context*)[¶](#google.adk.plugins.PluginManager.run_before_tool_callback) Runs the before_tool_callback for all plugins.

- Return type:
`Optional`

[`dict`

]


-
*async*run_on_event_callback(***,*invocation_context*,*event*)[¶](#google.adk.plugins.PluginManager.run_on_event_callback) Runs the on_event_callback for all plugins.

- Return type:
`Optional`

[]`Event`


-
*async*run_on_model_error_callback(***,*callback_context*,*llm_request*,*error*)[¶](#google.adk.plugins.PluginManager.run_on_model_error_callback) Runs the on_model_error_callback for all plugins.

- Return type:
`Optional`

[`LlmResponse`

]


-
*async*run_on_tool_error_callback(***,*tool*,*tool_args*,*tool_context*,*error*)[¶](#google.adk.plugins.PluginManager.run_on_tool_error_callback) Runs the on_tool_error_callback for all plugins.

- Return type:
`Optional`

[`dict`

]


-
*async*run_on_user_message_callback(***,*user_message*,*invocation_context*)[¶](#google.adk.plugins.PluginManager.run_on_user_message_callback) Runs the on_user_message_callback for all plugins.

- Return type:
`Optional`

[`Content`

]


-
*class*google.adk.plugins.ReflectAndRetryToolPlugin(*name='reflect_retry_tool_plugin'*,*max_retries=3*,*throw_exception_if_retry_exceeded=True*,*tracking_scope=TrackingScope.INVOCATION*)[¶](#google.adk.plugins.ReflectAndRetryToolPlugin) Bases:

`BasePlugin`

Provides self-healing, concurrent-safe error recovery for tool failures.

This plugin intercepts tool failures, provides structured guidance to the LLM for reflection and correction, and retries the operation up to a configurable limit.

**Key Features:****Concurrency Safe:**Uses locking to safely handle parallel tool

executions -

**Configurable Scope:**Tracks failures per-invocation (default) or globallyusing the TrackingScope enum.

**Extensible Scoping:**The _get_scope_key method can be overridden to implement custom tracking logic (e.g., per-user or per-session).**Granular Tracking:**Failure counts are tracked per-tool within the defined scope. A success with one tool resets its counter without affecting others.**Custom Error Extraction:**Supports detecting errors in normal tool

responses that

don’t throw exceptions, by overriding the extract_error_from_result method.

**Example:**[``](#id36)[`](#id38)python from my_project.plugins import ReflectAndRetryToolPlugin, TrackingScope# Example 1: (MOST COMMON USAGE): # Track failures only within the current agent invocation (default). error_handling_plugin = ReflectAndRetryToolPlugin(max_retries=3)

# Example 2: # Track failures globally across all turns and users. global_error_handling_plugin = ReflectAndRetryToolPlugin(max_retries=5, scope=TrackingScope.GLOBAL)

# Example 3: # Retry on failures but do not throw exceptions. error_handling_plugin =

ReflectAndRetryToolPlugin(max_retries=3, throw_exception_if_retry_exceeded=False)

# Example 4: # Track failures in successful tool responses that contain errors. class CustomRetryPlugin(ReflectAndRetryToolPlugin):

async def extract_error_from_result(self,

[*](#id40), tool, tool_args,tool_context, result):# Detect error based on response content if result.get(‘status’) == ‘error’:

return result

return None # No error detected

error_handling_plugin = CustomRetryPlugin(max_retries=5)

[``](#id42)[`](#id44)Initializes the ReflectAndRetryToolPlugin.

- Parameters:
**name**– Plugin instance identifier.**max_retries**– Maximum consecutive failures before giving up (0 = no retries).**throw_exception_if_retry_exceeded**– If True, raises the final exception when the retry limit is reached. If False, returns guidance instead.**tracking_scope**– Determines the lifecycle of the error tracking state. Defaults to TrackingScope.INVOCATION tracking per-invocation.


-
*async*after_tool_callback(***,*tool*,*tool_args*,*tool_context*,*result*)[¶](#google.adk.plugins.ReflectAndRetryToolPlugin.after_tool_callback) Handles successful tool calls or extracts and processes errors.

- Return type:
`Optional`

[`dict`

[`str`

,`Any`

]]- Parameters:
**tool**– The tool that was called.**tool_args**– The arguments passed to the tool.**tool_context**– The context of the tool call.**result**– The result of the tool call.

- Returns:
An optional dictionary containing reflection guidance if an error is detected, or None if the tool call was successful or the response is already a reflection message.


-
*async*extract_error_from_result(***,*tool*,*tool_args*,*tool_context*,*result*)[¶](#google.adk.plugins.ReflectAndRetryToolPlugin.extract_error_from_result) Extracts an error from a successful tool result and triggers retry logic.

This is useful when tool call finishes successfully but the result contains an error object like {“error”: …} that should be handled by the plugin.

By overriding this method, you can trigger retry logic on these successful results that contain errors.

- Return type:
`Optional`

[`dict`

[`str`

,`Any`

]]- Parameters:
**tool**– The tool that was called.**tool_args**– The arguments passed to the tool.**tool_context**– The context of the tool call.**result**– The result of the tool call.

- Returns:
The extracted error if any, or None if no error was detected.


-
*async*on_tool_error_callback(***,*tool*,*tool_args*,*tool_context*,*error*)[¶](#google.adk.plugins.ReflectAndRetryToolPlugin.on_tool_error_callback) Handles tool exceptions by providing reflection guidance.

- Return type:
`Optional`

[`dict`

[`str`

,`Any`

]]- Parameters:
**tool**– The tool that was called.**tool_args**– The arguments passed to the tool.**tool_context**– The context of the tool call.**error**– The exception raised by the tool.

- Returns:
An optional dictionary containing reflection guidance for the error.


# google.adk.runners module[¶](#module-google.adk.runners)

-
*class*google.adk.runners.InMemoryRunner(*agent=None*,***,*app_name=None*,*plugins=None*,*app=None*,*plugin_close_timeout=5.0*)[¶](#google.adk.runners.InMemoryRunner) Bases:

`Runner`

An in-memory Runner for testing and development.

This runner uses in-memory implementations for artifact, session, and memory services, providing a lightweight and self-contained environment for agent execution.

-
agent
[¶](#google.adk.runners.InMemoryRunner.agent) The root agent to run.


-
app_name
[¶](#google.adk.runners.InMemoryRunner.app_name) The application name of the runner. Defaults to ‘InMemoryRunner’.


Initializes the InMemoryRunner.

- Parameters:
**agent**– The root agent to run.**app_name**– The application name of the runner. Defaults to ‘InMemoryRunner’.**plugins**– Optional list of plugins for the runner.**app**– Optional App instance.**plugin_close_timeout**– The timeout in seconds for plugin close methods.


-
agent

-
*class*google.adk.runners.Runner(***,*app=None*,*app_name=None*,*agent=None*,*plugins=None*,*artifact_service=None*,*session_service*,*memory_service=None*,*credential_service=None*,*plugin_close_timeout=5.0*)[¶](#google.adk.runners.Runner) Bases:

`object`

The Runner class is used to run agents.

It manages the execution of an agent within a session, handling message processing, event generation, and interaction with various services like artifact storage, session management, and memory.

-
app_name
[¶](#google.adk.runners.Runner.app_name) The application name of the runner.


-
agent
[¶](#google.adk.runners.Runner.agent) The root agent to run.


-
artifact_service
[¶](#google.adk.runners.Runner.artifact_service) The artifact service for the runner.


-
plugin_manager
[¶](#google.adk.runners.Runner.plugin_manager) The plugin manager for the runner.


-
session_service
[¶](#google.adk.runners.Runner.session_service) The session service for the runner.


-
memory_service
[¶](#google.adk.runners.Runner.memory_service) The memory service for the runner.


-
credential_service
[¶](#google.adk.runners.Runner.credential_service) The credential service for the runner.


-
context_cache_config
[¶](#google.adk.runners.Runner.context_cache_config) The context cache config for the runner.


-
resumability_config
[¶](#google.adk.runners.Runner.resumability_config) The resumability config for the application.


Initializes the Runner.

Developers should provide either an app instance or both app_name and agent. Providing a mix of app and app_name/agent will result in a ValueError. Providing app is the recommended way to create a runner.

- Parameters:
**app**– An optional App instance. If provided, app_name and agent should not be specified.**app_name**– The application name of the runner. Required if app is not provided.**agent**– The root agent to run. Required if app is not provided.**plugins**– Deprecated. A list of plugins for the runner. Please use the app argument to provide plugins instead.**artifact_service**– The artifact service for the runner.**session_service**– The session service for the runner.**memory_service**– The memory service for the runner.**credential_service**– The credential service for the runner.**plugin_close_timeout**– The timeout in seconds for plugin close methods.

- Raises:
**ValueError**– If app is provided along with app_name or plugins, or if app is not provided but either app_name or agent is missing.

-
Self
*= typing.Self*[¶](#google.adk.runners.Runner.Self)

-
app_name
*: str*[¶](#id47) The app name of the runner.


-
artifact_service
*:*[BaseArtifactService](#google.adk.artifacts.BaseArtifactService)| None*= None*[¶](#id48) The artifact service for the runner.


-
*async*close()[¶](#google.adk.runners.Runner.close) Closes the runner.


-
context_cache_config
*: ContextCacheConfig | None**= None*[¶](#id49) The context cache config for the runner.


-
credential_service
*: BaseCredentialService | None**= None*[¶](#id50) The credential service for the runner.


-
memory_service
*:*[BaseMemoryService](#google.adk.memory.BaseMemoryService)| None*= None*[¶](#id51) The memory service for the runner.


-
plugin_manager
*:*[PluginManager](#google.adk.plugins.PluginManager)[¶](#id52) The plugin manager for the runner.


-
resumability_config
*:*[ResumabilityConfig](#google.adk.apps.ResumabilityConfig)| None*= None*[¶](#id53) The resumability config for the application.


-
*async*rewind_async(***,*user_id*,*session_id*,*rewind_before_invocation_id*)[¶](#google.adk.runners.Runner.rewind_async) Rewinds the session to before the specified invocation.

- Return type:
`None`


-
run(
***,*user_id*,*session_id*,*new_message*,*run_config=None*)[¶](#google.adk.runners.Runner.run) Runs the agent.

- Return type:
`Generator`

[,`Event`

`None`

,`None`

]

Note

This sync interface is only for local testing and convenience purpose. Consider using run_async for production usage.

If event compaction is enabled in the App configuration, it will be performed after all agent events for the current invocation have been yielded. The generator will only finish iterating after event compaction is complete.

- Parameters:
**user_id**– The user ID of the session.**session_id**– The session ID of the session.**new_message**– A new message to append to the session.**run_config**– The run config for the agent.

- Yields:
The events generated by the agent.


-
*async*run_async(***,*user_id*,*session_id*,*invocation_id=None*,*new_message=None*,*state_delta=None*,*run_config=None*)[¶](#google.adk.runners.Runner.run_async) Main entry method to run the agent in this runner.

If event compaction is enabled in the App configuration, it will be performed after all agent events for the current invocation have been yielded. The async generator will only finish iterating after event compaction is complete. However, this does not block new run_async calls for subsequent user queries, which can be started concurrently.

- Return type:
`AsyncGenerator`

[,`Event`

`None`

]- Parameters:
**user_id**– The user ID of the session.**session_id**– The session ID of the session.**invocation_id**– The invocation ID of the session, set this to resume an interrupted invocation.**new_message**– A new message to append to the session.**state_delta**– Optional state changes to apply to the session.**run_config**– The run config for the agent.

- Yields:
The events generated by the agent.

- Raises:
**ValueError**– If the session is not found; If both invocation_id and new_message are None.


-
*async*run_debug(*user_messages*,***,*user_id='debug_user_id'*,*session_id='debug_session_id'*,*run_config=None*,*quiet=False*,*verbose=False*)[¶](#google.adk.runners.Runner.run_debug) Debug helper for quick agent experimentation and testing.

This convenience method is designed for developers getting started with ADK who want to quickly test agents without dealing with session management, content formatting, or event streaming. It automatically handles common boilerplate while hiding complexity.

IMPORTANT: This is for debugging and experimentation only. For production use, please use the standard run_async() method which provides full control over session management, event streaming, and error handling.

- Return type:
`list`

[]`Event`

- Parameters:
**user_messages**– Message(s) to send to the agent. Can be: - Single string: “What is 2+2?” - List of strings: [“Hello!”, “What’s my name?”]**user_id**– User identifier. Defaults to “debug_user_id”.**session_id**– Session identifier for conversation persistence. Defaults to “debug_session_id”. Reuse the same ID to continue a conversation.**run_config**– Optional configuration for the agent execution.**quiet**– If True, suppresses console output. Defaults to False (output shown).**verbose**– If True, shows detailed tool calls and responses. Defaults to False for cleaner output showing only final agent responses.

- Returns:
All events from all messages.

- Return type:
list[

[Event](#google.adk.events.Event)]- Raises:
**ValueError**– If session creation/retrieval fails.

Examples

Quick debugging: >>> runner = InMemoryRunner(agent=my_agent) >>> await runner.run_debug(“What is 2+2?”)

Multiple queries in conversation: >>> await runner.run_debug([“Hello!”, “What’s my name?”])

Continue a debug session: >>> await runner.run_debug(“What did we discuss?”) # Continues default session

Separate debug sessions: >>> await runner.run_debug(“Hi”, user_id=”alice”, session_id=”debug1”) >>> await runner.run_debug(“Hi”, user_id=”bob”, session_id=”debug2”)

Capture events for inspection: >>> events = await runner.run_debug(“Analyze this”) >>> for event in events: … inspect_event(event)

Note

For production applications requiring: - Custom session/memory services (Spanner, Cloud SQL, etc.) - Fine-grained event processing and streaming - Error recovery and resumability - Performance optimization Please use run_async() with proper configuration.


-
*async*run_live(***,*user_id=None*,*session_id=None*,*live_request_queue*,*run_config=None*,*session=None*)[¶](#google.adk.runners.Runner.run_live) Runs the agent in live mode (experimental feature).

The run_live method yields a stream of Event objects, but not all yielded events are saved to the session. Here’s a breakdown:

- Return type:
`AsyncGenerator`

[,`Event`

`None`

]

**Events Yielded to Callers:*****Live Model Audio Events with Inline Data:**Events containing rawaudio Blob data(inline_data).

**Live Model Audio Events with File Data:**Both input and ouput audio data are aggregated into a audio file saved into artifacts. The reference to the file is saved in the event as file_data.**Usage Metadata:**Events containing token usage.**Transcription Events:**Both partial and non-partial transcription events are yielded.**Function Call and Response Events:**Always saved.**Other Control Events:**Most control events are saved.

**Events Saved to the Session:*****Live Model Audio Events with File Data:**Both input and ouput audiodata are aggregated into a audio file saved into artifacts. The reference to the file is saved as event in the file_data to session if RunConfig.save_live_model_audio_to_session is True.

**Usage Metadata Events:**Saved to the session.**Non-Partial Transcription Events:**Non-partial transcription events are saved.**Function Call and Response Events:**Always saved.**Other Control Events:**Most control events are saved.

**Events Not Saved to the Session:*****Live Model Audio Events with Inline Data:**Events containing rawaudio Blob data are

**not**saved to the session.- Parameters:
**user_id**– The user ID for the session. Required if session is None.**session_id**– The session ID for the session. Required if session is None.**live_request_queue**– The queue for live requests.**run_config**– The run config for the agent.**session**– The session to use. This parameter is deprecated, please use user_id and session_id instead.

- Yields:
*AsyncGenerator[Event, None]*– An asynchronous generator that yields Event objects as they are produced by the agent during its live execution.

Warning

This feature is

**experimental**and its API or behavior may change in future releases.Note

Either session or both user_id and session_id must be provided.


-
session_service
*:*[BaseSessionService](#google.adk.sessions.BaseSessionService)[¶](#id54) The session service for the runner.


-
app_name

# google.adk.sessions module[¶](#module-google.adk.sessions)

-
*class*google.adk.sessions.BaseSessionService[¶](#google.adk.sessions.BaseSessionService) Bases:

`ABC`

Base class for session services.

The service provides a set of methods for managing sessions and events.

-
*abstractmethod async*create_session(***,*app_name*,*user_id*,*state=None*,*session_id=None*)[¶](#google.adk.sessions.BaseSessionService.create_session) Creates a new session.

- Return type:
- Parameters:
**app_name**– the name of the app.**user_id**– the id of the user.**state**– the initial state of the session.**session_id**– the client-provided id of the session. If not provided, a generated ID will be used.

- Returns:
The newly created session instance.

- Return type:
session


-
*abstractmethod async*delete_session(***,*app_name*,*user_id*,*session_id*)[¶](#google.adk.sessions.BaseSessionService.delete_session) Deletes a session.

- Return type:
`None`


-
*abstractmethod async*get_session(***,*app_name*,*user_id*,*session_id*,*config=None*)[¶](#google.adk.sessions.BaseSessionService.get_session) Gets a session.

- Return type:
`Optional`

[]`Session`


-
*abstractmethod async*list_sessions(***,*app_name*,*user_id=None*)[¶](#google.adk.sessions.BaseSessionService.list_sessions) Lists all the sessions for a user.

- Return type:
`ListSessionsResponse`

- Parameters:
**app_name**– The name of the app.**user_id**– The ID of the user. If not provided, lists all sessions for all users.

- Returns:
A ListSessionsResponse containing the sessions.


-

-
*class*google.adk.sessions.InMemorySessionService[¶](#google.adk.sessions.InMemorySessionService) Bases:

`BaseSessionService`

An in-memory implementation of the session service.

It is not suitable for multi-threaded production environments. Use it for testing and development only.

-
*async*create_session(***,*app_name*,*user_id*,*state=None*,*session_id=None*)[¶](#google.adk.sessions.InMemorySessionService.create_session) Creates a new session.

- Return type:
- Parameters:
**app_name**– the name of the app.**user_id**– the id of the user.**state**– the initial state of the session.**session_id**– the client-provided id of the session. If not provided, a generated ID will be used.

- Returns:
The newly created session instance.

- Return type:
session


-
*async*delete_session(***,*app_name*,*user_id*,*session_id*)[¶](#google.adk.sessions.InMemorySessionService.delete_session) Deletes a session.

- Return type:
`None`


-
delete_session_sync(
***,*app_name*,*user_id*,*session_id*)[¶](#google.adk.sessions.InMemorySessionService.delete_session_sync) - Return type:
`None`


-
*async*get_session(***,*app_name*,*user_id*,*session_id*,*config=None*)[¶](#google.adk.sessions.InMemorySessionService.get_session) Gets a session.

- Return type:
`Optional`

[]`Session`


-
*async*list_sessions(***,*app_name*,*user_id=None*)[¶](#google.adk.sessions.InMemorySessionService.list_sessions) Lists all the sessions for a user.

- Return type:
`ListSessionsResponse`

- Parameters:
**app_name**– The name of the app.**user_id**– The ID of the user. If not provided, lists all sessions for all users.

- Returns:
A ListSessionsResponse containing the sessions.


-
list_sessions_sync(
***,*app_name*,*user_id=None*)[¶](#google.adk.sessions.InMemorySessionService.list_sessions_sync) - Return type:
`ListSessionsResponse`


-

-
*pydantic model*google.adk.sessions.Session[¶](#google.adk.sessions.Session) Bases:

`BaseModel`

Represents a series of interactions between a user and agents.

## Show JSON schema

{ "title": "Session", "description": "Represents a series of interactions between a user and agents.", "type": "object", "properties": { "id": { "title": "Id", "type": "string" }, "appName": { "title": "Appname", "type": "string" }, "userId": { "title": "Userid", "type": "string" }, "state": { "additionalProperties": true, "title": "State", "type": "object" }, "events": { "items": { "$ref": "#/$defs/Event" }, "title": "Events", "type": "array" }, "lastUpdateTime": { "default": 0.0, "title": "Lastupdatetime", "type": "number" } }, "$defs": { "APIKey": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "apiKey" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "in": { "$ref": "#/$defs/APIKeyIn" }, "name": { "title": "Name", "type": "string" } }, "required": [ "in", "name" ], "title": "APIKey", "type": "object" }, "APIKeyIn": { "enum": [ "query", "header", "cookie" ], "title": "APIKeyIn", "type": "string" }, "AuthConfig": { "additionalProperties": true, "description": "The auth config sent by tool asking client to collect auth credentials and\n\nadk and client will help to fill in the response", "properties": { "authScheme": { "anyOf": [ { "$ref": "#/$defs/APIKey" }, { "$ref": "#/$defs/HTTPBase" }, { "$ref": "#/$defs/OAuth2" }, { "$ref": "#/$defs/OpenIdConnect" }, { "$ref": "#/$defs/HTTPBearer" }, { "$ref": "#/$defs/OpenIdConnectWithConfig" } ], "title": "Authscheme" }, "rawAuthCredential": { "anyOf": [ { "$ref": "#/$defs/AuthCredential" }, { "type": "null" } ], "default": null }, "exchangedAuthCredential": { "anyOf": [ { "$ref": "#/$defs/AuthCredential" }, { "type": "null" } ], "default": null }, "credentialKey": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Credentialkey" } }, "required": [ "authScheme" ], "title": "AuthConfig", "type": "object" }, "AuthCredential": { "additionalProperties": true, "description": "Data class representing an authentication credential.\n\nTo exchange for the actual credential, please use\nCredentialExchanger.exchange_credential().\n\nExamples: API Key Auth\nAuthCredential(\n auth_type=AuthCredentialTypes.API_KEY,\n api_key=\"1234\",\n)\n\nExample: HTTP Auth\nAuthCredential(\n auth_type=AuthCredentialTypes.HTTP,\n http=HttpAuth(\n scheme=\"basic\",\n credentials=HttpCredentials(username=\"user\", password=\"password\"),\n ),\n)\n\nExample: OAuth2 Bearer Token in HTTP Header\nAuthCredential(\n auth_type=AuthCredentialTypes.HTTP,\n http=HttpAuth(\n scheme=\"bearer\",\n credentials=HttpCredentials(token=\"eyAkaknabna....\"),\n ),\n)\n\nExample: OAuth2 Auth with Authorization Code Flow\nAuthCredential(\n auth_type=AuthCredentialTypes.OAUTH2,\n oauth2=OAuth2Auth(\n client_id=\"1234\",\n client_secret=\"secret\",\n ),\n)\n\nExample: OpenID Connect Auth\nAuthCredential(\n auth_type=AuthCredentialTypes.OPEN_ID_CONNECT,\n oauth2=OAuth2Auth(\n client_id=\"1234\",\n client_secret=\"secret\",\n redirect_uri=\"https://example.com\",\n scopes=[\"scope1\", \"scope2\"],\n ),\n)\n\nExample: Auth with resource reference\nAuthCredential(\n auth_type=AuthCredentialTypes.API_KEY,\n resource_ref=\"projects/1234/locations/us-central1/resources/resource1\",\n)", "properties": { "authType": { "$ref": "#/$defs/AuthCredentialTypes" }, "resourceRef": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Resourceref" }, "apiKey": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Apikey" }, "http": { "anyOf": [ { "$ref": "#/$defs/HttpAuth" }, { "type": "null" } ], "default": null }, "serviceAccount": { "anyOf": [ { "$ref": "#/$defs/ServiceAccount" }, { "type": "null" } ], "default": null }, "oauth2": { "anyOf": [ { "$ref": "#/$defs/OAuth2Auth" }, { "type": "null" } ], "default": null } }, "required": [ "authType" ], "title": "AuthCredential", "type": "object" }, "AuthCredentialTypes": { "description": "Represents the type of authentication credential.", "enum": [ "apiKey", "http", "oauth2", "openIdConnect", "serviceAccount" ], "title": "AuthCredentialTypes", "type": "string" }, "Blob": { "additionalProperties": false, "description": "Content blob.", "properties": { "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Raw bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob. Used to provide a label or filename to distinguish blobs. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "Blob", "type": "object" }, "CacheMetadata": { "additionalProperties": false, "description": "Metadata for context cache associated with LLM responses.\n\nThis class stores cache identification, usage tracking, and lifecycle\ninformation for a particular cache instance. It can be in two states:\n\n1. Active cache state: cache_name is set, all fields populated\n2. Fingerprint-only state: cache_name is None, only fingerprint and\n contents_count are set for prefix matching\n\nToken counts (cached and total) are available in the LlmResponse.usage_metadata\nand should be accessed from there to avoid duplication.\n\nAttributes:\n cache_name: The full resource name of the cached content (e.g.,\n 'projects/123/locations/us-central1/cachedContents/456').\n None when no active cache exists (fingerprint-only state).\n expire_time: Unix timestamp when the cache expires. None when no\n active cache exists.\n fingerprint: Hash of cacheable contents (instruction + tools + contents).\n Always present for prefix matching.\n invocations_used: Number of invocations this cache has been used for.\n None when no active cache exists.\n contents_count: Number of contents. When active cache exists, this is\n the count of cached contents. When no active cache exists, this is\n the total count of contents in the request.\n created_at: Unix timestamp when the cache was created. None when\n no active cache exists.", "properties": { "cache_name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Full resource name of the cached content (None if no active cache)", "title": "Cache Name" }, "expire_time": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Unix timestamp when cache expires (None if no active cache)", "title": "Expire Time" }, "fingerprint": { "description": "Hash of cacheable contents used to detect changes", "title": "Fingerprint", "type": "string" }, "invocations_used": { "anyOf": [ { "minimum": 0, "type": "integer" }, { "type": "null" } ], "default": null, "description": "Number of invocations this cache has been used for (None if no active cache)", "title": "Invocations Used" }, "contents_count": { "description": "Number of contents (cached contents when active cache exists, total contents in request when no active cache)", "minimum": 0, "title": "Contents Count", "type": "integer" }, "created_at": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Unix timestamp when cache was created (None if no active cache)", "title": "Created At" } }, "required": [ "fingerprint", "contents_count" ], "title": "CacheMetadata", "type": "object" }, "Citation": { "additionalProperties": false, "description": "Source attributions for content.\n\nThis data type is not supported in Gemini API.", "properties": { "endIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. End index into the content.", "title": "Endindex" }, "license": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. License of the attribution.", "title": "License" }, "publicationDate": { "anyOf": [ { "$ref": "#/$defs/GoogleTypeDate" }, { "type": "null" } ], "default": null, "description": "Output only. Publication date of the attribution." }, "startIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. Start index into the content.", "title": "Startindex" }, "title": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. Title of the attribution.", "title": "Title" }, "uri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. Url reference of the attribution.", "title": "Uri" } }, "title": "Citation", "type": "object" }, "CitationMetadata": { "additionalProperties": false, "description": "Citation information when the model quotes another source.", "properties": { "citations": { "anyOf": [ { "items": { "$ref": "#/$defs/Citation" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Contains citation information when the model directly quotes, at\n length, from another source. Can include traditional websites and code\n repositories.\n ", "title": "Citations" } }, "title": "CitationMetadata", "type": "object" }, "CodeExecutionResult": { "additionalProperties": false, "description": "Result of executing the [ExecutableCode].\n\nOnly generated when using the [CodeExecution] tool, and always follows a\n`part` containing the [ExecutableCode].", "properties": { "outcome": { "anyOf": [ { "$ref": "#/$defs/Outcome" }, { "type": "null" } ], "default": null, "description": "Required. Outcome of the code execution." }, "output": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Contains stdout when code execution is successful, stderr or other description otherwise.", "title": "Output" } }, "title": "CodeExecutionResult", "type": "object" }, "Content": { "additionalProperties": false, "description": "Contains the multi-part content of a message.", "properties": { "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/Part" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a single message. Each part may have\n a different IANA MIME type.", "title": "Parts" }, "role": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The producer of the content. Must be either 'user' or 'model'. Useful to set for multi-turn conversations, otherwise can be left blank or unset.", "title": "Role" } }, "title": "Content", "type": "object" }, "Event": { "additionalProperties": false, "description": "Represents an event in a conversation between agents and users.\n\nIt is used to store the content of the conversation, as well as the actions\ntaken by the agents like function calls, etc.", "properties": { "modelVersion": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Modelversion" }, "content": { "anyOf": [ { "$ref": "#/$defs/Content" }, { "type": "null" } ], "default": null }, "groundingMetadata": { "anyOf": [ { "$ref": "#/$defs/GroundingMetadata" }, { "type": "null" } ], "default": null }, "partial": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Partial" }, "turnComplete": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Turncomplete" }, "finishReason": { "anyOf": [ { "$ref": "#/$defs/FinishReason" }, { "type": "null" } ], "default": null }, "errorCode": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Errorcode" }, "errorMessage": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Errormessage" }, "interrupted": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Interrupted" }, "customMetadata": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "title": "Custommetadata" }, "usageMetadata": { "anyOf": [ { "$ref": "#/$defs/GenerateContentResponseUsageMetadata" }, { "type": "null" } ], "default": null }, "liveSessionResumptionUpdate": { "anyOf": [ { "$ref": "#/$defs/LiveServerSessionResumptionUpdate" }, { "type": "null" } ], "default": null }, "inputTranscription": { "anyOf": [ { "$ref": "#/$defs/Transcription" }, { "type": "null" } ], "default": null }, "outputTranscription": { "anyOf": [ { "$ref": "#/$defs/Transcription" }, { "type": "null" } ], "default": null }, "avgLogprobs": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "title": "Avglogprobs" }, "logprobsResult": { "anyOf": [ { "$ref": "#/$defs/LogprobsResult" }, { "type": "null" } ], "default": null }, "cacheMetadata": { "anyOf": [ { "$ref": "#/$defs/CacheMetadata" }, { "type": "null" } ], "default": null }, "citationMetadata": { "anyOf": [ { "$ref": "#/$defs/CitationMetadata" }, { "type": "null" } ], "default": null }, "interactionId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Interactionid" }, "invocationId": { "default": "", "title": "Invocationid", "type": "string" }, "author": { "title": "Author", "type": "string" }, "actions": { "$ref": "#/$defs/EventActions" }, "longRunningToolIds": { "anyOf": [ { "items": { "type": "string" }, "type": "array", "uniqueItems": true }, { "type": "null" } ], "default": null, "title": "Longrunningtoolids" }, "branch": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Branch" }, "id": { "default": "", "title": "Id", "type": "string" }, "timestamp": { "title": "Timestamp", "type": "number" } }, "required": [ "author" ], "title": "Event", "type": "object" }, "EventActions": { "additionalProperties": false, "description": "Represents the actions attached to an event.", "properties": { "skipSummarization": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Skipsummarization" }, "stateDelta": { "additionalProperties": true, "title": "Statedelta", "type": "object" }, "artifactDelta": { "additionalProperties": { "type": "integer" }, "title": "Artifactdelta", "type": "object" }, "transferToAgent": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Transfertoagent" }, "escalate": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Escalate" }, "requestedAuthConfigs": { "additionalProperties": { "$ref": "#/$defs/AuthConfig" }, "title": "Requestedauthconfigs", "type": "object" }, "requestedToolConfirmations": { "additionalProperties": { "$ref": "#/$defs/ToolConfirmation" }, "title": "Requestedtoolconfirmations", "type": "object" }, "compaction": { "anyOf": [ { "$ref": "#/$defs/EventCompaction" }, { "type": "null" } ], "default": null }, "endOfAgent": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "title": "Endofagent" }, "agentState": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "title": "Agentstate" }, "rewindBeforeInvocationId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Rewindbeforeinvocationid" } }, "title": "EventActions", "type": "object" }, "EventCompaction": { "additionalProperties": false, "description": "The compaction of the events.", "properties": { "startTimestamp": { "title": "Starttimestamp", "type": "number" }, "endTimestamp": { "title": "Endtimestamp", "type": "number" }, "compactedContent": { "$ref": "#/$defs/Content" } }, "required": [ "startTimestamp", "endTimestamp", "compactedContent" ], "title": "EventCompaction", "type": "object" }, "ExecutableCode": { "additionalProperties": false, "description": "Code generated by the model that is meant to be executed, and the result returned to the model.\n\nGenerated when using the [CodeExecution] tool, in which the code will be\nautomatically executed, and a corresponding [CodeExecutionResult] will also be\ngenerated.", "properties": { "code": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The code to be executed.", "title": "Code" }, "language": { "anyOf": [ { "$ref": "#/$defs/Language" }, { "type": "null" } ], "default": null, "description": "Required. Programming language of the `code`." } }, "title": "ExecutableCode", "type": "object" }, "FileData": { "additionalProperties": false, "description": "URI based data.", "properties": { "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file data. Used to provide a label or filename to distinguish file datas. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "FileData", "type": "object" }, "FinishReason": { "description": "Output only. The reason why the model stopped generating tokens.\n\nIf empty, the model has not stopped generating the tokens.", "enum": [ "FINISH_REASON_UNSPECIFIED", "STOP", "MAX_TOKENS", "SAFETY", "RECITATION", "LANGUAGE", "OTHER", "BLOCKLIST", "PROHIBITED_CONTENT", "SPII", "MALFORMED_FUNCTION_CALL", "IMAGE_SAFETY", "UNEXPECTED_TOOL_CALL", "IMAGE_PROHIBITED_CONTENT", "NO_IMAGE", "IMAGE_RECITATION", "IMAGE_OTHER" ], "title": "FinishReason", "type": "string" }, "FunctionCall": { "additionalProperties": false, "description": "A function call.", "properties": { "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The unique id of the function call. If populated, the client to execute the\n `function_call` and return the response with the matching `id`.", "title": "Id" }, "args": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Optional. The function parameters and values in JSON object format. See [FunctionDeclaration.parameters] for parameter details.", "title": "Args" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The name of the function to call. Matches [FunctionDeclaration.name].", "title": "Name" }, "partialArgs": { "anyOf": [ { "items": { "$ref": "#/$defs/PartialArg" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. The partial argument value of the function call. If provided, represents the arguments/fields that are streamed incrementally. This field is not supported in Gemini API.", "title": "Partialargs" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is the last part of the FunctionCall. If true, another partial message for the current FunctionCall is expected to follow. This field is not supported in Gemini API.", "title": "Willcontinue" } }, "title": "FunctionCall", "type": "object" }, "FunctionResponse": { "additionalProperties": false, "description": "A function response.", "properties": { "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Signals that function call continues, and more responses will be returned, turning the function call into a generator. Is only applicable to NON_BLOCKING function calls (see FunctionDeclaration.behavior for details), ignored otherwise. If false, the default, future responses will not be considered. Is only applicable to NON_BLOCKING function calls, is ignored otherwise. If set to false, future responses will not be considered. It is allowed to return empty `response` with `will_continue=False` to signal that the function call is finished.", "title": "Willcontinue" }, "scheduling": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseScheduling" }, { "type": "null" } ], "default": null, "description": "Specifies how the response should be scheduled in the conversation. Only applicable to NON_BLOCKING function calls, is ignored otherwise. Defaults to WHEN_IDLE." }, "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/FunctionResponsePart" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a function response. Each part may\n have a different IANA MIME type.", "title": "Parts" }, "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The id of the function call this response is for. Populated by the client to match the corresponding function call `id`.", "title": "Id" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The name of the function to call. Matches [FunctionDeclaration.name] and [FunctionCall.name].", "title": "Name" }, "response": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Required. The function response in JSON object format. Use \"output\" key to specify function output and \"error\" key to specify error details (if any). If \"output\" and \"error\" keys are not specified, then whole \"response\" is treated as function output.", "title": "Response" } }, "title": "FunctionResponse", "type": "object" }, "FunctionResponseBlob": { "additionalProperties": false, "description": "Raw media bytes for function response.\n\nText should not be sent as raw bytes, use the FunctionResponse.response\nfield.", "properties": { "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Inline media bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob.\n Used to provide a label or filename to distinguish blobs.", "title": "Displayname" } }, "title": "FunctionResponseBlob", "type": "object" }, "FunctionResponseFileData": { "additionalProperties": false, "description": "URI based data for function response.", "properties": { "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file.\n Used to provide a label or filename to distinguish files.", "title": "Displayname" } }, "title": "FunctionResponseFileData", "type": "object" }, "FunctionResponsePart": { "additionalProperties": false, "description": "A datatype containing media that is part of a `FunctionResponse` message.\n\nA `FunctionResponsePart` consists of data which has an associated datatype. A\n`FunctionResponsePart` can only contain one of the accepted types in\n`FunctionResponsePart.data`.\n\nA `FunctionResponsePart` must have a fixed IANA MIME type identifying the\ntype and subtype of the media if the `inline_data` field is filled with raw\nbytes.", "properties": { "inlineData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseBlob" }, { "type": "null" } ], "default": null, "description": "Optional. Inline media bytes." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseFileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." } }, "title": "FunctionResponsePart", "type": "object" }, "FunctionResponseScheduling": { "description": "Specifies how the response should be scheduled in the conversation.", "enum": [ "SCHEDULING_UNSPECIFIED", "SILENT", "WHEN_IDLE", "INTERRUPT" ], "title": "FunctionResponseScheduling", "type": "string" }, "GenerateContentResponseUsageMetadata": { "additionalProperties": false, "description": "Usage metadata about the content generation request and response.\n\nThis message provides a detailed breakdown of token usage and other relevant\nmetrics. This data type is not supported in Gemini API.", "properties": { "cacheTokensDetails": { "anyOf": [ { "items": { "$ref": "#/$defs/ModalityTokenCount" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Output only. A detailed breakdown of the token count for each modality in the cached content.", "title": "Cachetokensdetails" }, "cachedContentTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. The number of tokens in the cached content that was used for this request.", "title": "Cachedcontenttokencount" }, "candidatesTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "The total number of tokens in the generated candidates.", "title": "Candidatestokencount" }, "candidatesTokensDetails": { "anyOf": [ { "items": { "$ref": "#/$defs/ModalityTokenCount" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Output only. A detailed breakdown of the token count for each modality in the generated candidates.", "title": "Candidatestokensdetails" }, "promptTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "The total number of tokens in the prompt. This includes any text, images, or other media provided in the request. When `cached_content` is set, this also includes the number of tokens in the cached content.", "title": "Prompttokencount" }, "promptTokensDetails": { "anyOf": [ { "items": { "$ref": "#/$defs/ModalityTokenCount" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Output only. A detailed breakdown of the token count for each modality in the prompt.", "title": "Prompttokensdetails" }, "thoughtsTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. The number of tokens that were part of the model's generated \"thoughts\" output, if applicable.", "title": "Thoughtstokencount" }, "toolUsePromptTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. The number of tokens in the results from tool executions, which are provided back to the model as input, if applicable.", "title": "Tooluseprompttokencount" }, "toolUsePromptTokensDetails": { "anyOf": [ { "items": { "$ref": "#/$defs/ModalityTokenCount" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Output only. A detailed breakdown by modality of the token counts from the results of tool executions, which are provided back to the model as input.", "title": "Tooluseprompttokensdetails" }, "totalTokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "The total number of tokens for the entire request. This is the sum of `prompt_token_count`, `candidates_token_count`, `tool_use_prompt_token_count`, and `thoughts_token_count`.", "title": "Totaltokencount" }, "trafficType": { "anyOf": [ { "$ref": "#/$defs/TrafficType" }, { "type": "null" } ], "default": null, "description": "Output only. The traffic type for this request." } }, "title": "GenerateContentResponseUsageMetadata", "type": "object" }, "GoogleTypeDate": { "additionalProperties": false, "description": "Represents a whole or partial calendar date, such as a birthday.\n\nThe time of day and time zone are either specified elsewhere or are\ninsignificant. The date is relative to the Gregorian Calendar. This can\nrepresent one of the following: * A full date, with non-zero year, month, and\nday values. * A month and day, with a zero year (for example, an anniversary).\n* A year on its own, with a zero month and a zero day. * A year and month,\nwith a zero day (for example, a credit card expiration date). Related types: *\ngoogle.type.TimeOfDay * google.type.DateTime * google.protobuf.Timestamp. This\ndata type is not supported in Gemini API.", "properties": { "day": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Day of a month. Must be from 1 to 31 and valid for the year and month, or 0 to specify a year by itself or a year and month where the day isn't significant.", "title": "Day" }, "month": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Month of a year. Must be from 1 to 12, or 0 to specify a year without a month and day.", "title": "Month" }, "year": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Year of the date. Must be from 1 to 9999, or 0 to specify a date without a year.", "title": "Year" } }, "title": "GoogleTypeDate", "type": "object" }, "GroundingChunk": { "additionalProperties": false, "description": "Grounding chunk.", "properties": { "maps": { "anyOf": [ { "$ref": "#/$defs/GroundingChunkMaps" }, { "type": "null" } ], "default": null, "description": "Grounding chunk from Google Maps. This field is not supported in Gemini API." }, "retrievedContext": { "anyOf": [ { "$ref": "#/$defs/GroundingChunkRetrievedContext" }, { "type": "null" } ], "default": null, "description": "Grounding chunk from context retrieved by the retrieval tools. This field is not supported in Gemini API." }, "web": { "anyOf": [ { "$ref": "#/$defs/GroundingChunkWeb" }, { "type": "null" } ], "default": null, "description": "Grounding chunk from the web." } }, "title": "GroundingChunk", "type": "object" }, "GroundingChunkMaps": { "additionalProperties": false, "description": "Chunk from Google Maps. This data type is not supported in Gemini API.", "properties": { "placeAnswerSources": { "anyOf": [ { "$ref": "#/$defs/GroundingChunkMapsPlaceAnswerSources" }, { "type": "null" } ], "default": null, "description": "Sources used to generate the place answer. This includes review snippets and photos that were used to generate the answer, as well as uris to flag content." }, "placeId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "This Place's resource name, in `places/{place_id}` format. Can be used to look up the Place.", "title": "Placeid" }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Text of the place answer.", "title": "Text" }, "title": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Title of the place.", "title": "Title" }, "uri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "URI reference of the place.", "title": "Uri" } }, "title": "GroundingChunkMaps", "type": "object" }, "GroundingChunkMapsPlaceAnswerSources": { "additionalProperties": false, "description": "Sources used to generate the place answer.\n\nThis data type is not supported in Gemini API.", "properties": { "flagContentUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A link where users can flag a problem with the generated answer.", "title": "Flagcontenturi" }, "reviewSnippets": { "anyOf": [ { "items": { "$ref": "#/$defs/GroundingChunkMapsPlaceAnswerSourcesReviewSnippet" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Snippets of reviews that are used to generate the answer.", "title": "Reviewsnippets" } }, "title": "GroundingChunkMapsPlaceAnswerSources", "type": "object" }, "GroundingChunkMapsPlaceAnswerSourcesAuthorAttribution": { "additionalProperties": false, "description": "Author attribution for a photo or review.\n\nThis data type is not supported in Gemini API.", "properties": { "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Name of the author of the Photo or Review.", "title": "Displayname" }, "photoUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Profile photo URI of the author of the Photo or Review.", "title": "Photouri" }, "uri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "URI of the author of the Photo or Review.", "title": "Uri" } }, "title": "GroundingChunkMapsPlaceAnswerSourcesAuthorAttribution", "type": "object" }, "GroundingChunkMapsPlaceAnswerSourcesReviewSnippet": { "additionalProperties": false, "description": "Encapsulates a review snippet.\n\nThis data type is not supported in Gemini API.", "properties": { "authorAttribution": { "anyOf": [ { "$ref": "#/$defs/GroundingChunkMapsPlaceAnswerSourcesAuthorAttribution" }, { "type": "null" } ], "default": null, "description": "This review's author." }, "flagContentUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A link where users can flag a problem with the review.", "title": "Flagcontenturi" }, "googleMapsUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A link to show the review on Google Maps.", "title": "Googlemapsuri" }, "relativePublishTimeDescription": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A string of formatted recent time, expressing the review time relative to the current time in a form appropriate for the language and country.", "title": "Relativepublishtimedescription" }, "review": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A reference representing this place review which may be used to look up this place review again.", "title": "Review" }, "reviewId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Id of the review referencing the place.", "title": "Reviewid" }, "title": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Title of the review.", "title": "Title" } }, "title": "GroundingChunkMapsPlaceAnswerSourcesReviewSnippet", "type": "object" }, "GroundingChunkRetrievedContext": { "additionalProperties": false, "description": "Chunk from context retrieved by the retrieval tools.\n\nThis data type is not supported in Gemini API.", "properties": { "documentName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. The full document name for the referenced Vertex AI Search document.", "title": "Documentname" }, "ragChunk": { "anyOf": [ { "$ref": "#/$defs/RagChunk" }, { "type": "null" } ], "default": null, "description": "Additional context for the RAG retrieval result. This is only populated when using the RAG retrieval tool." }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Text of the attribution.", "title": "Text" }, "title": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Title of the attribution.", "title": "Title" }, "uri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "URI reference of the attribution.", "title": "Uri" } }, "title": "GroundingChunkRetrievedContext", "type": "object" }, "GroundingChunkWeb": { "additionalProperties": false, "description": "Chunk from the web.", "properties": { "domain": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Domain of the (original) URI. This field is not supported in Gemini API.", "title": "Domain" }, "title": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Title of the chunk.", "title": "Title" }, "uri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "URI reference of the chunk.", "title": "Uri" } }, "title": "GroundingChunkWeb", "type": "object" }, "GroundingMetadata": { "additionalProperties": false, "description": "Metadata returned to client when grounding is enabled.", "properties": { "googleMapsWidgetContextToken": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Output only. Resource name of the Google Maps widget context token to be used with the PlacesContextElement widget to render contextual data. This is populated only for Google Maps grounding. This field is not supported in Gemini API.", "title": "Googlemapswidgetcontexttoken" }, "groundingChunks": { "anyOf": [ { "items": { "$ref": "#/$defs/GroundingChunk" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of supporting references retrieved from specified grounding source.", "title": "Groundingchunks" }, "groundingSupports": { "anyOf": [ { "items": { "$ref": "#/$defs/GroundingSupport" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. List of grounding support.", "title": "Groundingsupports" }, "retrievalMetadata": { "anyOf": [ { "$ref": "#/$defs/RetrievalMetadata" }, { "type": "null" } ], "default": null, "description": "Optional. Output only. Retrieval metadata." }, "retrievalQueries": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. Queries executed by the retrieval tools. This field is not supported in Gemini API.", "title": "Retrievalqueries" }, "searchEntryPoint": { "anyOf": [ { "$ref": "#/$defs/SearchEntryPoint" }, { "type": "null" } ], "default": null, "description": "Optional. Google search entry for the following-up web searches." }, "sourceFlaggingUris": { "anyOf": [ { "items": { "$ref": "#/$defs/GroundingMetadataSourceFlaggingUri" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. Output only. List of source flagging uris. This is currently populated only for Google Maps grounding. This field is not supported in Gemini API.", "title": "Sourceflagginguris" }, "webSearchQueries": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. Web search queries for the following-up web search.", "title": "Websearchqueries" } }, "title": "GroundingMetadata", "type": "object" }, "GroundingMetadataSourceFlaggingUri": { "additionalProperties": false, "description": "Source content flagging uri for a place or review.\n\nThis is currently populated only for Google Maps grounding. This data type is\nnot supported in Gemini API.", "properties": { "flagContentUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "A link where users can flag a problem with the source (place or review).", "title": "Flagcontenturi" }, "sourceId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Id of the place or review.", "title": "Sourceid" } }, "title": "GroundingMetadataSourceFlaggingUri", "type": "object" }, "GroundingSupport": { "additionalProperties": false, "description": "Grounding support.", "properties": { "confidenceScores": { "anyOf": [ { "items": { "type": "number" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Confidence score of the support references. Ranges from 0 to 1. 1 is the most confident. For Gemini 2.0 and before, this list must have the same size as the grounding_chunk_indices. For Gemini 2.5 and after, this list will be empty and should be ignored.", "title": "Confidencescores" }, "groundingChunkIndices": { "anyOf": [ { "items": { "type": "integer" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "A list of indices (into 'grounding_chunk') specifying the citations associated with the claim. For instance [1,3,4] means that grounding_chunk[1], grounding_chunk[3], grounding_chunk[4] are the retrieved content attributed to the claim.", "title": "Groundingchunkindices" }, "segment": { "anyOf": [ { "$ref": "#/$defs/Segment" }, { "type": "null" } ], "default": null, "description": "Segment of the content this support belongs to." } }, "title": "GroundingSupport", "type": "object" }, "HTTPBase": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "http" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "scheme": { "title": "Scheme", "type": "string" } }, "required": [ "scheme" ], "title": "HTTPBase", "type": "object" }, "HTTPBearer": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "http" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "scheme": { "const": "bearer", "default": "bearer", "title": "Scheme", "type": "string" }, "bearerFormat": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Bearerformat" } }, "title": "HTTPBearer", "type": "object" }, "HttpAuth": { "additionalProperties": true, "description": "The credentials and metadata for HTTP authentication.", "properties": { "scheme": { "title": "Scheme", "type": "string" }, "credentials": { "$ref": "#/$defs/HttpCredentials" } }, "required": [ "scheme", "credentials" ], "title": "HttpAuth", "type": "object" }, "HttpCredentials": { "additionalProperties": true, "description": "Represents the secret token value for HTTP authentication, like user name, password, oauth token, etc.", "properties": { "username": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Username" }, "password": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Password" }, "token": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Token" } }, "title": "HttpCredentials", "type": "object" }, "Language": { "description": "Programming language of the `code`.", "enum": [ "LANGUAGE_UNSPECIFIED", "PYTHON" ], "title": "Language", "type": "string" }, "LiveServerSessionResumptionUpdate": { "additionalProperties": false, "description": "Update of the session resumption state.\n\nOnly sent if `session_resumption` was set in the connection config.", "properties": { "newHandle": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "New handle that represents state that can be resumed. Empty if `resumable`=false.", "title": "Newhandle" }, "resumable": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "True if session can be resumed at this point. It might be not possible to resume session at some points. In that case we send update empty new_handle and resumable=false. Example of such case could be model executing function calls or just generating. Resuming session (using previous session token) in such state will result in some data loss.", "title": "Resumable" }, "lastConsumedClientMessageIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Index of last message sent by client that is included in state represented by this SessionResumptionToken. Only sent when `SessionResumptionConfig.transparent` is set.\n\nPresence of this index allows users to transparently reconnect and avoid issue of losing some part of realtime audio input/video. If client wishes to temporarily disconnect (for example as result of receiving GoAway) they can do it without losing state by buffering messages sent since last `SessionResmumptionTokenUpdate`. This field will enable them to limit buffering (avoid keeping all requests in RAM).\n\nNote: This should not be used for when resuming a session at some time later -- in those cases partial audio and video frames arelikely not needed.", "title": "Lastconsumedclientmessageindex" } }, "title": "LiveServerSessionResumptionUpdate", "type": "object" }, "LogprobsResult": { "additionalProperties": false, "description": "Logprobs Result", "properties": { "chosenCandidates": { "anyOf": [ { "items": { "$ref": "#/$defs/LogprobsResultCandidate" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Length = total number of decoding steps. The chosen candidates may or may not be in top_candidates.", "title": "Chosencandidates" }, "topCandidates": { "anyOf": [ { "items": { "$ref": "#/$defs/LogprobsResultTopCandidates" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Length = total number of decoding steps.", "title": "Topcandidates" } }, "title": "LogprobsResult", "type": "object" }, "LogprobsResultCandidate": { "additionalProperties": false, "description": "Candidate for the logprobs token and score.", "properties": { "logProbability": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "The candidate's log probability.", "title": "Logprobability" }, "token": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The candidate's token string value.", "title": "Token" }, "tokenId": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "The candidate's token id value.", "title": "Tokenid" } }, "title": "LogprobsResultCandidate", "type": "object" }, "LogprobsResultTopCandidates": { "additionalProperties": false, "description": "Candidates with top log probabilities at each decoding step.", "properties": { "candidates": { "anyOf": [ { "items": { "$ref": "#/$defs/LogprobsResultCandidate" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Sorted by log probability in descending order.", "title": "Candidates" } }, "title": "LogprobsResultTopCandidates", "type": "object" }, "MediaModality": { "description": "Server content modalities.", "enum": [ "MODALITY_UNSPECIFIED", "TEXT", "IMAGE", "VIDEO", "AUDIO", "DOCUMENT" ], "title": "MediaModality", "type": "string" }, "ModalityTokenCount": { "additionalProperties": false, "description": "Represents token counting info for a single modality.", "properties": { "modality": { "anyOf": [ { "$ref": "#/$defs/MediaModality" }, { "type": "null" } ], "default": null, "description": "The modality associated with this token count." }, "tokenCount": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Number of tokens.", "title": "Tokencount" } }, "title": "ModalityTokenCount", "type": "object" }, "OAuth2": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "oauth2" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "flows": { "$ref": "#/$defs/OAuthFlows" } }, "required": [ "flows" ], "title": "OAuth2", "type": "object" }, "OAuth2Auth": { "additionalProperties": true, "description": "Represents credential value and its metadata for a OAuth2 credential.", "properties": { "clientId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Clientid" }, "clientSecret": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Clientsecret" }, "authUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Authuri" }, "state": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "State" }, "redirectUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Redirecturi" }, "authResponseUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Authresponseuri" }, "authCode": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Authcode" }, "accessToken": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Accesstoken" }, "refreshToken": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshtoken" }, "expiresAt": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "title": "Expiresat" }, "expiresIn": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "title": "Expiresin" }, "audience": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Audience" }, "tokenEndpointAuthMethod": { "anyOf": [ { "enum": [ "client_secret_basic", "client_secret_post", "client_secret_jwt", "private_key_jwt" ], "type": "string" }, { "type": "null" } ], "default": "client_secret_basic", "title": "Tokenendpointauthmethod" } }, "title": "OAuth2Auth", "type": "object" }, "OAuthFlowAuthorizationCode": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "authorizationUrl": { "title": "Authorizationurl", "type": "string" }, "tokenUrl": { "title": "Tokenurl", "type": "string" } }, "required": [ "authorizationUrl", "tokenUrl" ], "title": "OAuthFlowAuthorizationCode", "type": "object" }, "OAuthFlowClientCredentials": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "tokenUrl": { "title": "Tokenurl", "type": "string" } }, "required": [ "tokenUrl" ], "title": "OAuthFlowClientCredentials", "type": "object" }, "OAuthFlowImplicit": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "authorizationUrl": { "title": "Authorizationurl", "type": "string" } }, "required": [ "authorizationUrl" ], "title": "OAuthFlowImplicit", "type": "object" }, "OAuthFlowPassword": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "tokenUrl": { "title": "Tokenurl", "type": "string" } }, "required": [ "tokenUrl" ], "title": "OAuthFlowPassword", "type": "object" }, "OAuthFlows": { "additionalProperties": true, "properties": { "implicit": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowImplicit" }, { "type": "null" } ], "default": null }, "password": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowPassword" }, { "type": "null" } ], "default": null }, "clientCredentials": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowClientCredentials" }, { "type": "null" } ], "default": null }, "authorizationCode": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowAuthorizationCode" }, { "type": "null" } ], "default": null } }, "title": "OAuthFlows", "type": "object" }, "OpenIdConnect": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "openIdConnect" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "openIdConnectUrl": { "title": "Openidconnecturl", "type": "string" } }, "required": [ "openIdConnectUrl" ], "title": "OpenIdConnect", "type": "object" }, "OpenIdConnectWithConfig": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "openIdConnect" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "authorization_endpoint": { "title": "Authorization Endpoint", "type": "string" }, "token_endpoint": { "title": "Token Endpoint", "type": "string" }, "userinfo_endpoint": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Userinfo Endpoint" }, "revocation_endpoint": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Revocation Endpoint" }, "token_endpoint_auth_methods_supported": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Token Endpoint Auth Methods Supported" }, "grant_types_supported": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Grant Types Supported" }, "scopes": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Scopes" } }, "required": [ "authorization_endpoint", "token_endpoint" ], "title": "OpenIdConnectWithConfig", "type": "object" }, "Outcome": { "description": "Outcome of the code execution.", "enum": [ "OUTCOME_UNSPECIFIED", "OUTCOME_OK", "OUTCOME_FAILED", "OUTCOME_DEADLINE_EXCEEDED" ], "title": "Outcome", "type": "string" }, "Part": { "additionalProperties": false, "description": "A datatype containing media content.\n\nExactly one field within a Part should be set, representing the specific type\nof content being conveyed. Using multiple fields within the same `Part`\ninstance is considered invalid.", "properties": { "mediaResolution": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolution" }, { "type": "null" } ], "default": null, "description": "Media resolution for the input media.\n " }, "codeExecutionResult": { "anyOf": [ { "$ref": "#/$defs/CodeExecutionResult" }, { "type": "null" } ], "default": null, "description": "Optional. Result of executing the [ExecutableCode]." }, "executableCode": { "anyOf": [ { "$ref": "#/$defs/ExecutableCode" }, { "type": "null" } ], "default": null, "description": "Optional. Code generated by the model that is meant to be executed." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." }, "functionCall": { "anyOf": [ { "$ref": "#/$defs/FunctionCall" }, { "type": "null" } ], "default": null, "description": "Optional. A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] with the parameters and their values." }, "functionResponse": { "anyOf": [ { "$ref": "#/$defs/FunctionResponse" }, { "type": "null" } ], "default": null, "description": "Optional. The result output of a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function call. It is used as context to the model." }, "inlineData": { "anyOf": [ { "$ref": "#/$defs/Blob" }, { "type": "null" } ], "default": null, "description": "Optional. Inlined bytes data." }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Text part (can be code).", "title": "Text" }, "thought": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Indicates if the part is thought from the model.", "title": "Thought" }, "thoughtSignature": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. An opaque signature for the thought so it can be reused in subsequent requests.", "title": "Thoughtsignature" }, "videoMetadata": { "anyOf": [ { "$ref": "#/$defs/VideoMetadata" }, { "type": "null" } ], "default": null, "description": "Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data." } }, "title": "Part", "type": "object" }, "PartMediaResolution": { "additionalProperties": false, "description": "Media resolution for the input media.", "properties": { "level": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolutionLevel" }, { "type": "null" } ], "default": null, "description": "The tokenization quality used for given media.\n " }, "numTokens": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Specifies the required sequence length for media tokenization.\n ", "title": "Numtokens" } }, "title": "PartMediaResolution", "type": "object" }, "PartMediaResolutionLevel": { "description": "The tokenization quality used for given media.", "enum": [ "MEDIA_RESOLUTION_UNSPECIFIED", "MEDIA_RESOLUTION_LOW", "MEDIA_RESOLUTION_MEDIUM", "MEDIA_RESOLUTION_HIGH", "MEDIA_RESOLUTION_ULTRA_HIGH" ], "title": "PartMediaResolutionLevel", "type": "string" }, "PartialArg": { "additionalProperties": false, "description": "Partial argument value of the function call.\n\nThis data type is not supported in Gemini API.", "properties": { "nullValue": { "anyOf": [ { "const": "NULL_VALUE", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a null value.", "title": "Nullvalue" }, "numberValue": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a double value.", "title": "Numbervalue" }, "stringValue": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a string value.", "title": "Stringvalue" }, "boolValue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a boolean value.", "title": "Boolvalue" }, "jsonPath": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. A JSON Path (RFC 9535) to the argument being streamed. https://datatracker.ietf.org/doc/html/rfc9535. e.g. \"$.foo.bar[0].data\".", "title": "Jsonpath" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is not the last part of the same json_path. If true, another PartialArg message for the current json_path is expected to follow.", "title": "Willcontinue" } }, "title": "PartialArg", "type": "object" }, "RagChunk": { "additionalProperties": false, "description": "A RagChunk includes the content of a chunk of a RagFile, and associated metadata.\n\nThis data type is not supported in Gemini API.", "properties": { "pageSpan": { "anyOf": [ { "$ref": "#/$defs/RagChunkPageSpan" }, { "type": "null" } ], "default": null, "description": "If populated, represents where the chunk starts and ends in the document." }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The content of the chunk.", "title": "Text" } }, "title": "RagChunk", "type": "object" }, "RagChunkPageSpan": { "additionalProperties": false, "description": "Represents where the chunk starts and ends in the document.\n\nThis data type is not supported in Gemini API.", "properties": { "firstPage": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Page where chunk starts in the document. Inclusive. 1-indexed.", "title": "Firstpage" }, "lastPage": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Page where chunk ends in the document. Inclusive. 1-indexed.", "title": "Lastpage" } }, "title": "RagChunkPageSpan", "type": "object" }, "RetrievalMetadata": { "additionalProperties": false, "description": "Metadata related to retrieval in the grounding flow.", "properties": { "googleSearchDynamicRetrievalScore": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. Score indicating how likely information from Google Search could help answer the prompt. The score is in the range `[0, 1]`, where 0 is the least likely and 1 is the most likely. This score is only populated when Google Search grounding and dynamic retrieval is enabled. It will be compared to the threshold to determine whether to trigger Google Search.", "title": "Googlesearchdynamicretrievalscore" } }, "title": "RetrievalMetadata", "type": "object" }, "SearchEntryPoint": { "additionalProperties": false, "description": "Google search entry point.", "properties": { "renderedContent": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Web content snippet that can be embedded in a web page or an app webview.", "title": "Renderedcontent" }, "sdkBlob": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Base64 encoded JSON representing array of tuple.", "title": "Sdkblob" } }, "title": "SearchEntryPoint", "type": "object" }, "SecuritySchemeType": { "enum": [ "apiKey", "http", "oauth2", "openIdConnect" ], "title": "SecuritySchemeType", "type": "string" }, "Segment": { "additionalProperties": false, "description": "Segment of the content.", "properties": { "endIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. End index in the given Part, measured in bytes. Offset from the start of the Part, exclusive, starting at zero.", "title": "Endindex" }, "partIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. The index of a Part object within its parent Content object.", "title": "Partindex" }, "startIndex": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Output only. Start index in the given Part, measured in bytes. Offset from the start of the Part, inclusive, starting at zero.", "title": "Startindex" }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Output only. The text corresponding to the segment from the response.", "title": "Text" } }, "title": "Segment", "type": "object" }, "ServiceAccount": { "additionalProperties": true, "description": "Represents Google Service Account configuration.", "properties": { "serviceAccountCredential": { "anyOf": [ { "$ref": "#/$defs/ServiceAccountCredential" }, { "type": "null" } ], "default": null }, "scopes": { "items": { "type": "string" }, "title": "Scopes", "type": "array" }, "useDefaultCredential": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": false, "title": "Usedefaultcredential" } }, "required": [ "scopes" ], "title": "ServiceAccount", "type": "object" }, "ServiceAccountCredential": { "additionalProperties": true, "description": "Represents Google Service Account configuration.\n\nAttributes:\n type: The type should be \"service_account\".\n project_id: The project ID.\n private_key_id: The ID of the private key.\n private_key: The private key.\n client_email: The client email.\n client_id: The client ID.\n auth_uri: The authorization URI.\n token_uri: The token URI.\n auth_provider_x509_cert_url: URL for auth provider's X.509 cert.\n client_x509_cert_url: URL for the client's X.509 cert.\n universe_domain: The universe domain.\n\nExample:\n\n config = ServiceAccountCredential(\n type_=\"service_account\",\n project_id=\"your_project_id\",\n private_key_id=\"your_private_key_id\",\n private_key=\"-----BEGIN PRIVATE KEY-----...\",\n client_email=\"...@....iam.gserviceaccount.com\",\n client_id=\"your_client_id\",\n auth_uri=\"https://accounts.google.com/o/oauth2/auth\",\n token_uri=\"https://oauth2.googleapis.com/token\",\n auth_provider_x509_cert_url=\"https://www.googleapis.com/oauth2/v1/certs\",\n client_x509_cert_url=\"https://www.googleapis.com/robot/v1/metadata/x509/...\",\n universe_domain=\"googleapis.com\"\n )\n\n\n config = ServiceAccountConfig.model_construct(**{\n ...service account config dict\n })", "properties": { "type": { "default": "", "title": "Type", "type": "string" }, "projectId": { "title": "Projectid", "type": "string" }, "privateKeyId": { "title": "Privatekeyid", "type": "string" }, "privateKey": { "title": "Privatekey", "type": "string" }, "clientEmail": { "title": "Clientemail", "type": "string" }, "clientId": { "title": "Clientid", "type": "string" }, "authUri": { "title": "Authuri", "type": "string" }, "tokenUri": { "title": "Tokenuri", "type": "string" }, "authProviderX509CertUrl": { "title": "Authproviderx509Certurl", "type": "string" }, "clientX509CertUrl": { "title": "Clientx509Certurl", "type": "string" }, "universeDomain": { "title": "Universedomain", "type": "string" } }, "required": [ "projectId", "privateKeyId", "privateKey", "clientEmail", "clientId", "authUri", "tokenUri", "authProviderX509CertUrl", "clientX509CertUrl", "universeDomain" ], "title": "ServiceAccountCredential", "type": "object" }, "ToolConfirmation": { "additionalProperties": false, "description": "Represents a tool confirmation configuration.", "properties": { "hint": { "default": "", "title": "Hint", "type": "string" }, "confirmed": { "default": false, "title": "Confirmed", "type": "boolean" }, "payload": { "anyOf": [ {}, { "type": "null" } ], "default": null, "title": "Payload" } }, "title": "ToolConfirmation", "type": "object" }, "TrafficType": { "description": "Output only.\n\nThe traffic type for this request. This enum is not supported in Gemini API.", "enum": [ "TRAFFIC_TYPE_UNSPECIFIED", "ON_DEMAND", "PROVISIONED_THROUGHPUT" ], "title": "TrafficType", "type": "string" }, "Transcription": { "additionalProperties": false, "description": "Audio transcription in Server Conent.", "properties": { "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Transcription text.\n ", "title": "Text" }, "finished": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "The bool indicates the end of the transcription.\n ", "title": "Finished" } }, "title": "Transcription", "type": "object" }, "VideoMetadata": { "additionalProperties": false, "description": "Metadata describes the input video content.", "properties": { "endOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The end offset of the video.", "title": "Endoffset" }, "fps": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. The frame rate of the video sent to the model. If not specified, the default value will be 1.0. The fps range is (0.0, 24.0].", "title": "Fps" }, "startOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The start offset of the video.", "title": "Startoffset" } }, "title": "VideoMetadata", "type": "object" } }, "additionalProperties": false, "required": [ "id", "appName", "userId" ] }

- Fields:
`app_name (str)`

`events (list[google.adk.events.event.Event])`

`id (str)`

`last_update_time (float)`

`state (dict[str, Any])`

`user_id (str)`


-
*field*app_name*: str**[Required]**(alias 'appName')*[¶](#google.adk.sessions.Session.app_name) The name of the app.


-
*field*events*: list[*[Event](#google.adk.events.Event)]*[Optional]*[¶](#google.adk.sessions.Session.events) The events of the session, e.g. user input, model response, function call/response, etc.


-
*field*id*: str**[Required]*[¶](#google.adk.sessions.Session.id) The unique identifier of the session.


-
*field*last_update_time*: float**= 0.0**(alias 'lastUpdateTime')*[¶](#google.adk.sessions.Session.last_update_time) The last update time of the session.


-
*field*state*: dict[str, Any]**[Optional]*[¶](#google.adk.sessions.Session.state) The state of the session.


-
*field*user_id*: str**[Required]**(alias 'userId')*[¶](#google.adk.sessions.Session.user_id) The id of the user.


-
*class*google.adk.sessions.State(*value*,*delta*)[¶](#google.adk.sessions.State) Bases:

`object`

A state dict that maintains the current value and the pending-commit delta.

- Parameters:
**value**– The current value of the state dict.**delta**– The delta change to the current value that hasn’t been committed.


-
APP_PREFIX
*= 'app:'*[¶](#google.adk.sessions.State.APP_PREFIX)

-
TEMP_PREFIX
*= 'temp:'*[¶](#google.adk.sessions.State.TEMP_PREFIX)

-
USER_PREFIX
*= 'user:'*[¶](#google.adk.sessions.State.USER_PREFIX)

-
get(
*key*,*default=None*)[¶](#google.adk.sessions.State.get) Returns the value of the state dict for the given key.

- Return type:
`Any`


-
has_delta()
[¶](#google.adk.sessions.State.has_delta) Whether the state has pending delta.

- Return type:
`bool`


-
setdefault(
*key*,*default=None*)[¶](#google.adk.sessions.State.setdefault) Gets the value of a key, or sets it to a default if the key doesn’t exist.

- Return type:
`Any`


-
to_dict()
[¶](#google.adk.sessions.State.to_dict) Returns the state dict.

- Return type:
`dict`

[`str`

,`Any`

]


-
update(
*delta*)[¶](#google.adk.sessions.State.update) Updates the state dict with the given delta.


-
*class*google.adk.sessions.VertexAiSessionService(*project=None*,*location=None*,*agent_engine_id=None*,***,*express_mode_api_key=None*)[¶](#google.adk.sessions.VertexAiSessionService) Bases:

`BaseSessionService`

Connects to the Vertex AI Agent Engine Session Service using Agent Engine SDK.

[https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/sessions/overview](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/sessions/overview)Initializes the VertexAiSessionService.

- Parameters:
**project**– The project id of the project to use.**location**– The location of the project to use.**agent_engine_id**– The resource ID of the agent engine to use.**express_mode_api_key**– The API key to use for Express Mode. If not provided, the API key from the GOOGLE_API_KEY environment variable will be used. It will only be used if GOOGLE_GENAI_USE_VERTEXAI is true. Do not use Google AI Studio API key for this field. For more details, visit[https://cloud.google.com/vertex-ai/generative-ai/docs/start/express-mode/overview](https://cloud.google.com/vertex-ai/generative-ai/docs/start/express-mode/overview)


-
*async*create_session(***,*app_name*,*user_id*,*state=None*,*session_id=None*,***kwargs*)[¶](#google.adk.sessions.VertexAiSessionService.create_session) Creates a new session.

- Return type:
- Parameters:
**app_name**– The name of the application.**user_id**– The ID of the user.**state**– The initial state of the session.**session_id**– The ID of the session.****kwargs**– Additional arguments to pass to the session creation. E.g. set expire_time=’2025-10-01T00:00:00Z’ to set the session expiration time. See[https://cloud.google.com/vertex-ai/generative-ai/docs/reference/rest/v1beta1/projects.locations.reasoningEngines.sessions](https://cloud.google.com/vertex-ai/generative-ai/docs/reference/rest/v1beta1/projects.locations.reasoningEngines.sessions)for more details.

- Returns:
The created session.


-
*async*delete_session(***,*app_name*,*user_id*,*session_id*)[¶](#google.adk.sessions.VertexAiSessionService.delete_session) Deletes a session.

- Return type:
`None`


-
*async*get_session(***,*app_name*,*user_id*,*session_id*,*config=None*)[¶](#google.adk.sessions.VertexAiSessionService.get_session) Gets a session.

- Return type:
`Optional`

[]`Session`


-
*async*list_sessions(***,*app_name*,*user_id=None*)[¶](#google.adk.sessions.VertexAiSessionService.list_sessions) Lists all the sessions for a user.

- Return type:
`ListSessionsResponse`

- Parameters:
**app_name**– The name of the app.**user_id**– The ID of the user. If not provided, lists all sessions for all users.

- Returns:
A ListSessionsResponse containing the sessions.


# google.adk.telemetry module[¶](#module-google.adk.telemetry)

-
google.adk.telemetry.trace_call_llm(
*invocation_context*,*event_id*,*llm_request*,*llm_response*)[¶](#google.adk.telemetry.trace_call_llm) Traces a call to the LLM.

This function records details about the LLM request and response as attributes on the current OpenTelemetry span.

- Parameters:
**invocation_context**– The invocation context for the current agent run.**event_id**– The ID of the event.**llm_request**– The LLM request object.**llm_response**– The LLM response object.


-
google.adk.telemetry.trace_merged_tool_calls(
*response_event_id*,*function_response_event*)[¶](#google.adk.telemetry.trace_merged_tool_calls) Traces merged tool call events.

Calling this function is not needed for telemetry purposes. This is provided for preventing /debug/trace requests (typically sent by web UI).

- Parameters:
**response_event_id**– The ID of the response event.**function_response_event**– The merged response event.


-
google.adk.telemetry.trace_send_data(
*invocation_context*,*event_id*,*data*)[¶](#google.adk.telemetry.trace_send_data) Traces the sending of data to the agent.

This function records details about the data sent to the agent as attributes on the current OpenTelemetry span.

- Parameters:
**invocation_context**– The invocation context for the current agent run.**event_id**– The ID of the event.**data**– A list of content objects.


-
google.adk.telemetry.trace_tool_call(
*tool*,*args*,*function_response_event*)[¶](#google.adk.telemetry.trace_tool_call) Traces tool call.

- Parameters:
**tool**– The tool that was called.**args**– The arguments to the tool call.**function_response_event**– The event with the function response details.


# google.adk.tools package[¶](#module-google.adk.tools)

-
*class*google.adk.tools.APIHubToolset(***,*apihub_resource_name*,*access_token=None*,*service_account_json=None*,*name=''*,*description=''*,*lazy_load_spec=False*,*auth_scheme=None*,*auth_credential=None*,*apihub_client=None*,*tool_filter=None*)[¶](#google.adk.tools.APIHubToolset) Bases:

`BaseToolset`

APIHubTool generates tools from a given API Hub resource.

Examples:

apihub_toolset = APIHubToolset( apihub_resource_name="projects/test-project/locations/us-central1/apis/test-api", service_account_json="...", tool_filter=lambda tool, ctx=None: tool.name in ('my_tool', 'my_other_tool') ) # Get all available tools agent = LlmAgent(tools=apihub_toolset)

**apihub_resource_name**is the resource name from API Hub. It must include API name, and can optionally include API version and spec name.If apihub_resource_name includes a spec resource name, the content of that spec will be used for generating the tools.

If apihub_resource_name includes only an api or a version name, the first spec of the first version of that API will be used.


Initializes the APIHubTool with the given parameters.

Examples:

apihub_toolset = APIHubToolset( apihub_resource_name="projects/test-project/locations/us-central1/apis/test-api", service_account_json="...", ) # Get all available tools agent = LlmAgent(tools=[apihub_toolset]) apihub_toolset = APIHubToolset( apihub_resource_name="projects/test-project/locations/us-central1/apis/test-api", service_account_json="...", tool_filter = ['my_tool'] ) # Get a specific tool agent = LlmAgent(tools=[ ..., apihub_toolset, ])

**apihub_resource_name**is the resource name from API Hub. It must include API name, and can optionally include API version and spec name.If apihub_resource_name includes a spec resource name, the content of that spec will be used for generating the tools.

If apihub_resource_name includes only an api or a version name, the first spec of the first version of that API will be used.


Example:

projects/xxx/locations/us-central1/apis/apiname/…

[https://console.cloud.google.com/apigee/api-hub/apis/apiname?project=xxx](https://console.cloud.google.com/apigee/api-hub/apis/apiname?project=xxx)

- Parameters:
**apihub_resource_name**– The resource name of the API in API Hub. Example:`projects/test-project/locations/us-central1/apis/test-api`

.**access_token**– Google Access token. Generate with gcloud cli`gcloud auth print-access-token`

. Used for fetching API Specs from API Hub.**service_account_json**– The service account config as a json string. Required if not using default service credential. It is used for creating the API Hub client and fetching the API Specs from API Hub.**apihub_client**– Optional custom API Hub client.**name**– Name of the toolset. Optional.**description**– Description of the toolset. Optional.**auth_scheme**– Auth scheme that applies to all the tool in the toolset.**auth_credential**– Auth credential that applies to all the tool in the toolset.**lazy_load_spec**– If True, the spec will be loaded lazily when needed. Otherwise, the spec will be loaded immediately and the tools will be generated during initialization.**tool_filter**– The filter used to filter the tools in the toolset. It can be either a tool predicate or a list of tool names of the tools to expose.


-
*async*close()[¶](#google.adk.tools.APIHubToolset.close) Performs cleanup and releases resources held by the toolset.

Note

This method is invoked, for example, at the end of an agent server’s lifecycle or when the toolset is no longer needed. Implementations should ensure that any open connections, files, or other managed resources are properly released to prevent leaks.


-
*async*get_tools(*readonly_context=None*)[¶](#google.adk.tools.APIHubToolset.get_tools) Retrieves all available tools.

- Return type:
`List`

[]`RestApiTool`

- Returns:
A list of all available RestApiTool objects.


-
*class*google.adk.tools.AgentTool(*agent*,*skip_summarization=False*,***,*include_plugins=True*)[¶](#google.adk.tools.AgentTool) Bases:

`BaseTool`

A tool that wraps an agent.

This tool allows an agent to be called as a tool within a larger application. The agent’s input schema is used to define the tool’s input parameters, and the agent’s output is returned as the tool’s result.

-
agent
[¶](#google.adk.tools.AgentTool.agent) The agent to wrap.


-
skip_summarization
[¶](#google.adk.tools.AgentTool.skip_summarization) Whether to skip summarization of the agent output.


-
include_plugins
[¶](#google.adk.tools.AgentTool.include_plugins) Whether to propagate plugins from the parent runner context to the agent’s runner. When True (default), the agent will inherit all plugins from its parent. Set to False to run the agent with an isolated plugin environment.


-
*classmethod*from_config(*config*,*config_abs_path*)[¶](#google.adk.tools.AgentTool.from_config) Creates a tool instance from a config.

This default implementation uses inspect to automatically map config values to constructor arguments based on their type hints. Subclasses should override this method for custom initialization logic.

- Return type:
- Parameters:
**config**– The config for the tool.**config_abs_path**– The absolute path to the config file that contains the tool config.

- Returns:
The tool instance.


-
populate_name()
[¶](#google.adk.tools.AgentTool.populate_name) - Return type:
`Any`


-
*async*run_async(***,*args*,*tool_context*)[¶](#google.adk.tools.AgentTool.run_async) Runs the tool with the given arguments and context.

- Return type:
`Any`


Note

Required if this tool needs to run at the client side.

Otherwise, can be skipped, e.g. for a built-in GoogleSearch tool for Gemini.


- Parameters:
**args**– The LLM-filled arguments.**tool_context**– The context of the tool.

- Returns:
The result of running the tool.


-
agent

-
*class*google.adk.tools.ApiRegistry(*api_registry_project_id*,*location='global'*,*header_provider=None*)[¶](#google.adk.tools.ApiRegistry) Bases:

`object`

Registry that provides McpToolsets for MCP servers registered in API Registry.

Initialize the API Registry.

- Parameters:
**api_registry_project_id**– The project ID for the Google Cloud API Registry.**location**– The location of the API Registry resources.**header_provider**– Optional function to provide additional headers for MCP server calls.


-
get_toolset(
*mcp_server_name*,*tool_filter=None*,*tool_name_prefix=None*)[¶](#google.adk.tools.ApiRegistry.get_toolset) Return the MCP Toolset based on the params.

- Return type:
- Parameters:
**mcp_server_name**– Filter to select the MCP server name to get tools from.**tool_filter**– Optional filter to select specific tools. Can be a list of tool names or a ToolPredicate function.**tool_name_prefix**– Optional prefix to prepend to the names of the tools returned by the toolset.

- Returns:
A toolset for the MCP server specified.

- Return type:


-
*pydantic model*google.adk.tools.AuthToolArguments[¶](#google.adk.tools.AuthToolArguments) Bases:

`BaseModelWithConfig`

the arguments for the special long running function tool that is used to

request end user credentials.

## Show JSON schema

{ "title": "AuthToolArguments", "description": "the arguments for the special long running function tool that is used to\n\nrequest end user credentials.", "type": "object", "properties": { "functionCallId": { "title": "Functioncallid", "type": "string" }, "authConfig": { "$ref": "#/$defs/AuthConfig" } }, "$defs": { "APIKey": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "apiKey" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "in": { "$ref": "#/$defs/APIKeyIn" }, "name": { "title": "Name", "type": "string" } }, "required": [ "in", "name" ], "title": "APIKey", "type": "object" }, "APIKeyIn": { "enum": [ "query", "header", "cookie" ], "title": "APIKeyIn", "type": "string" }, "AuthConfig": { "additionalProperties": true, "description": "The auth config sent by tool asking client to collect auth credentials and\n\nadk and client will help to fill in the response", "properties": { "authScheme": { "anyOf": [ { "$ref": "#/$defs/APIKey" }, { "$ref": "#/$defs/HTTPBase" }, { "$ref": "#/$defs/OAuth2" }, { "$ref": "#/$defs/OpenIdConnect" }, { "$ref": "#/$defs/HTTPBearer" }, { "$ref": "#/$defs/OpenIdConnectWithConfig" } ], "title": "Authscheme" }, "rawAuthCredential": { "anyOf": [ { "$ref": "#/$defs/AuthCredential" }, { "type": "null" } ], "default": null }, "exchangedAuthCredential": { "anyOf": [ { "$ref": "#/$defs/AuthCredential" }, { "type": "null" } ], "default": null }, "credentialKey": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Credentialkey" } }, "required": [ "authScheme" ], "title": "AuthConfig", "type": "object" }, "AuthCredential": { "additionalProperties": true, "description": "Data class representing an authentication credential.\n\nTo exchange for the actual credential, please use\nCredentialExchanger.exchange_credential().\n\nExamples: API Key Auth\nAuthCredential(\n auth_type=AuthCredentialTypes.API_KEY,\n api_key=\"1234\",\n)\n\nExample: HTTP Auth\nAuthCredential(\n auth_type=AuthCredentialTypes.HTTP,\n http=HttpAuth(\n scheme=\"basic\",\n credentials=HttpCredentials(username=\"user\", password=\"password\"),\n ),\n)\n\nExample: OAuth2 Bearer Token in HTTP Header\nAuthCredential(\n auth_type=AuthCredentialTypes.HTTP,\n http=HttpAuth(\n scheme=\"bearer\",\n credentials=HttpCredentials(token=\"eyAkaknabna....\"),\n ),\n)\n\nExample: OAuth2 Auth with Authorization Code Flow\nAuthCredential(\n auth_type=AuthCredentialTypes.OAUTH2,\n oauth2=OAuth2Auth(\n client_id=\"1234\",\n client_secret=\"secret\",\n ),\n)\n\nExample: OpenID Connect Auth\nAuthCredential(\n auth_type=AuthCredentialTypes.OPEN_ID_CONNECT,\n oauth2=OAuth2Auth(\n client_id=\"1234\",\n client_secret=\"secret\",\n redirect_uri=\"https://example.com\",\n scopes=[\"scope1\", \"scope2\"],\n ),\n)\n\nExample: Auth with resource reference\nAuthCredential(\n auth_type=AuthCredentialTypes.API_KEY,\n resource_ref=\"projects/1234/locations/us-central1/resources/resource1\",\n)", "properties": { "authType": { "$ref": "#/$defs/AuthCredentialTypes" }, "resourceRef": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Resourceref" }, "apiKey": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Apikey" }, "http": { "anyOf": [ { "$ref": "#/$defs/HttpAuth" }, { "type": "null" } ], "default": null }, "serviceAccount": { "anyOf": [ { "$ref": "#/$defs/ServiceAccount" }, { "type": "null" } ], "default": null }, "oauth2": { "anyOf": [ { "$ref": "#/$defs/OAuth2Auth" }, { "type": "null" } ], "default": null } }, "required": [ "authType" ], "title": "AuthCredential", "type": "object" }, "AuthCredentialTypes": { "description": "Represents the type of authentication credential.", "enum": [ "apiKey", "http", "oauth2", "openIdConnect", "serviceAccount" ], "title": "AuthCredentialTypes", "type": "string" }, "HTTPBase": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "http" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "scheme": { "title": "Scheme", "type": "string" } }, "required": [ "scheme" ], "title": "HTTPBase", "type": "object" }, "HTTPBearer": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "http" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "scheme": { "const": "bearer", "default": "bearer", "title": "Scheme", "type": "string" }, "bearerFormat": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Bearerformat" } }, "title": "HTTPBearer", "type": "object" }, "HttpAuth": { "additionalProperties": true, "description": "The credentials and metadata for HTTP authentication.", "properties": { "scheme": { "title": "Scheme", "type": "string" }, "credentials": { "$ref": "#/$defs/HttpCredentials" } }, "required": [ "scheme", "credentials" ], "title": "HttpAuth", "type": "object" }, "HttpCredentials": { "additionalProperties": true, "description": "Represents the secret token value for HTTP authentication, like user name, password, oauth token, etc.", "properties": { "username": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Username" }, "password": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Password" }, "token": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Token" } }, "title": "HttpCredentials", "type": "object" }, "OAuth2": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "oauth2" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "flows": { "$ref": "#/$defs/OAuthFlows" } }, "required": [ "flows" ], "title": "OAuth2", "type": "object" }, "OAuth2Auth": { "additionalProperties": true, "description": "Represents credential value and its metadata for a OAuth2 credential.", "properties": { "clientId": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Clientid" }, "clientSecret": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Clientsecret" }, "authUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Authuri" }, "state": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "State" }, "redirectUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Redirecturi" }, "authResponseUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Authresponseuri" }, "authCode": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Authcode" }, "accessToken": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Accesstoken" }, "refreshToken": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshtoken" }, "expiresAt": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "title": "Expiresat" }, "expiresIn": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "title": "Expiresin" }, "audience": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Audience" }, "tokenEndpointAuthMethod": { "anyOf": [ { "enum": [ "client_secret_basic", "client_secret_post", "client_secret_jwt", "private_key_jwt" ], "type": "string" }, { "type": "null" } ], "default": "client_secret_basic", "title": "Tokenendpointauthmethod" } }, "title": "OAuth2Auth", "type": "object" }, "OAuthFlowAuthorizationCode": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "authorizationUrl": { "title": "Authorizationurl", "type": "string" }, "tokenUrl": { "title": "Tokenurl", "type": "string" } }, "required": [ "authorizationUrl", "tokenUrl" ], "title": "OAuthFlowAuthorizationCode", "type": "object" }, "OAuthFlowClientCredentials": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "tokenUrl": { "title": "Tokenurl", "type": "string" } }, "required": [ "tokenUrl" ], "title": "OAuthFlowClientCredentials", "type": "object" }, "OAuthFlowImplicit": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "authorizationUrl": { "title": "Authorizationurl", "type": "string" } }, "required": [ "authorizationUrl" ], "title": "OAuthFlowImplicit", "type": "object" }, "OAuthFlowPassword": { "additionalProperties": true, "properties": { "refreshUrl": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Refreshurl" }, "scopes": { "additionalProperties": { "type": "string" }, "default": {}, "title": "Scopes", "type": "object" }, "tokenUrl": { "title": "Tokenurl", "type": "string" } }, "required": [ "tokenUrl" ], "title": "OAuthFlowPassword", "type": "object" }, "OAuthFlows": { "additionalProperties": true, "properties": { "implicit": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowImplicit" }, { "type": "null" } ], "default": null }, "password": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowPassword" }, { "type": "null" } ], "default": null }, "clientCredentials": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowClientCredentials" }, { "type": "null" } ], "default": null }, "authorizationCode": { "anyOf": [ { "$ref": "#/$defs/OAuthFlowAuthorizationCode" }, { "type": "null" } ], "default": null } }, "title": "OAuthFlows", "type": "object" }, "OpenIdConnect": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "openIdConnect" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "openIdConnectUrl": { "title": "Openidconnecturl", "type": "string" } }, "required": [ "openIdConnectUrl" ], "title": "OpenIdConnect", "type": "object" }, "OpenIdConnectWithConfig": { "additionalProperties": true, "properties": { "type": { "$ref": "#/$defs/SecuritySchemeType", "default": "openIdConnect" }, "description": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Description" }, "authorization_endpoint": { "title": "Authorization Endpoint", "type": "string" }, "token_endpoint": { "title": "Token Endpoint", "type": "string" }, "userinfo_endpoint": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Userinfo Endpoint" }, "revocation_endpoint": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Revocation Endpoint" }, "token_endpoint_auth_methods_supported": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Token Endpoint Auth Methods Supported" }, "grant_types_supported": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Grant Types Supported" }, "scopes": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Scopes" } }, "required": [ "authorization_endpoint", "token_endpoint" ], "title": "OpenIdConnectWithConfig", "type": "object" }, "SecuritySchemeType": { "enum": [ "apiKey", "http", "oauth2", "openIdConnect" ], "title": "SecuritySchemeType", "type": "string" }, "ServiceAccount": { "additionalProperties": true, "description": "Represents Google Service Account configuration.", "properties": { "serviceAccountCredential": { "anyOf": [ { "$ref": "#/$defs/ServiceAccountCredential" }, { "type": "null" } ], "default": null }, "scopes": { "items": { "type": "string" }, "title": "Scopes", "type": "array" }, "useDefaultCredential": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": false, "title": "Usedefaultcredential" } }, "required": [ "scopes" ], "title": "ServiceAccount", "type": "object" }, "ServiceAccountCredential": { "additionalProperties": true, "description": "Represents Google Service Account configuration.\n\nAttributes:\n type: The type should be \"service_account\".\n project_id: The project ID.\n private_key_id: The ID of the private key.\n private_key: The private key.\n client_email: The client email.\n client_id: The client ID.\n auth_uri: The authorization URI.\n token_uri: The token URI.\n auth_provider_x509_cert_url: URL for auth provider's X.509 cert.\n client_x509_cert_url: URL for the client's X.509 cert.\n universe_domain: The universe domain.\n\nExample:\n\n config = ServiceAccountCredential(\n type_=\"service_account\",\n project_id=\"your_project_id\",\n private_key_id=\"your_private_key_id\",\n private_key=\"-----BEGIN PRIVATE KEY-----...\",\n client_email=\"...@....iam.gserviceaccount.com\",\n client_id=\"your_client_id\",\n auth_uri=\"https://accounts.google.com/o/oauth2/auth\",\n token_uri=\"https://oauth2.googleapis.com/token\",\n auth_provider_x509_cert_url=\"https://www.googleapis.com/oauth2/v1/certs\",\n client_x509_cert_url=\"https://www.googleapis.com/robot/v1/metadata/x509/...\",\n universe_domain=\"googleapis.com\"\n )\n\n\n config = ServiceAccountConfig.model_construct(**{\n ...service account config dict\n })", "properties": { "type": { "default": "", "title": "Type", "type": "string" }, "projectId": { "title": "Projectid", "type": "string" }, "privateKeyId": { "title": "Privatekeyid", "type": "string" }, "privateKey": { "title": "Privatekey", "type": "string" }, "clientEmail": { "title": "Clientemail", "type": "string" }, "clientId": { "title": "Clientid", "type": "string" }, "authUri": { "title": "Authuri", "type": "string" }, "tokenUri": { "title": "Tokenuri", "type": "string" }, "authProviderX509CertUrl": { "title": "Authproviderx509Certurl", "type": "string" }, "clientX509CertUrl": { "title": "Clientx509Certurl", "type": "string" }, "universeDomain": { "title": "Universedomain", "type": "string" } }, "required": [ "projectId", "privateKeyId", "privateKey", "clientEmail", "clientId", "authUri", "tokenUri", "authProviderX509CertUrl", "clientX509CertUrl", "universeDomain" ], "title": "ServiceAccountCredential", "type": "object" } }, "additionalProperties": true, "required": [ "functionCallId", "authConfig" ] }

- Fields:
`auth_config (google.adk.auth.auth_tool.AuthConfig)`

`function_call_id (str)`


-
*field*auth_config*: AuthConfig**[Required]**(alias 'authConfig')*[¶](#google.adk.tools.AuthToolArguments.auth_config)

-
*field*function_call_id*: str**[Required]**(alias 'functionCallId')*[¶](#google.adk.tools.AuthToolArguments.function_call_id)


-
*class*google.adk.tools.BaseTool(***,*name*,*description*,*is_long_running=False*,*custom_metadata=None*)[¶](#google.adk.tools.BaseTool) Bases:

`ABC`

The base class for all tools.

-
custom_metadata
*: dict[str, Any] | None**= None*[¶](#google.adk.tools.BaseTool.custom_metadata) The custom metadata of the BaseTool.

An optional key-value pair for storing and retrieving tool-specific metadata, such as tool manifests, etc.

NOTE: the entire dict must be JSON serializable.


-
description
*: str*[¶](#google.adk.tools.BaseTool.description) The description of the tool.


-
*classmethod*from_config(*config*,*config_abs_path*)[¶](#google.adk.tools.BaseTool.from_config) Creates a tool instance from a config.

This default implementation uses inspect to automatically map config values to constructor arguments based on their type hints. Subclasses should override this method for custom initialization logic.

- Return type:
`TypeVar`

(`SelfTool`

, bound= BaseTool)- Parameters:
**config**– The config for the tool.**config_abs_path**– The absolute path to the config file that contains the tool config.

- Returns:
The tool instance.


-
is_long_running
*: bool**= False*[¶](#google.adk.tools.BaseTool.is_long_running) Whether the tool is a long running operation, which typically returns a resource id first and finishes the operation later.


-
name
*: str*[¶](#google.adk.tools.BaseTool.name) The name of the tool.


-
*async*process_llm_request(***,*tool_context*,*llm_request*)[¶](#google.adk.tools.BaseTool.process_llm_request) Processes the outgoing LLM request for this tool.

Use cases: - Most common use case is adding this tool to the LLM request. - Some tools may just preprocess the LLM request before it’s sent out.

- Return type:
`None`

- Parameters:
**tool_context**– The context of the tool.**llm_request**– The outgoing LLM request, mutable this method.


-
*async*run_async(***,*args*,*tool_context*)[¶](#google.adk.tools.BaseTool.run_async) Runs the tool with the given arguments and context.

- Return type:
`Any`


Note

Required if this tool needs to run at the client side.

Otherwise, can be skipped, e.g. for a built-in GoogleSearch tool for Gemini.


- Parameters:
**args**– The LLM-filled arguments.**tool_context**– The context of the tool.

- Returns:
The result of running the tool.


-
custom_metadata

-
*class*google.adk.tools.DiscoveryEngineSearchTool(*data_store_id=None*,*data_store_specs=None*,*search_engine_id=None*,*filter=None*,*max_results=None*)[¶](#google.adk.tools.DiscoveryEngineSearchTool) Bases:

`FunctionTool`

Tool for searching the discovery engine.

Initializes the DiscoveryEngineSearchTool.

- Parameters:
**data_store_id**– The Vertex AI search data store resource ID in the format of “projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}”.**data_store_specs**– Specifications that define the specific DataStores to be searched. It should only be set if engine is used.**search_engine_id**– The Vertex AI search engine resource ID in the format of “projects/{project}/locations/{location}/collections/{collection}/engines/{engine}”.**filter**– The filter to be applied to the search request. Default is None.**max_results**– The maximum number of results to return. Default is None.


-
discovery_engine_search(
*query*)[¶](#google.adk.tools.DiscoveryEngineSearchTool.discovery_engine_search) Search through Vertex AI Search’s discovery engine search API.

- Return type:
`dict`

[`str`

,`Any`

]- Parameters:
**query**– The search query.- Returns:
A dictionary containing the status of the request and the list of search results, which contains the title, url and content.


-
*class*google.adk.tools.ExampleTool(*examples*)[¶](#google.adk.tools.ExampleTool) Bases:

`BaseTool`

A tool that adds (few-shot) examples to the LLM request.

-
examples
[¶](#google.adk.tools.ExampleTool.examples) The examples to add to the LLM request.


-
*classmethod*from_config(*config*,*config_abs_path*)[¶](#google.adk.tools.ExampleTool.from_config) Creates a tool instance from a config.

This default implementation uses inspect to automatically map config values to constructor arguments based on their type hints. Subclasses should override this method for custom initialization logic.

- Return type:
- Parameters:
**config**– The config for the tool.**config_abs_path**– The absolute path to the config file that contains the tool config.

- Returns:
The tool instance.


-
*async*process_llm_request(***,*tool_context*,*llm_request*)[¶](#google.adk.tools.ExampleTool.process_llm_request) Processes the outgoing LLM request for this tool.

Use cases: - Most common use case is adding this tool to the LLM request. - Some tools may just preprocess the LLM request before it’s sent out.

- Return type:
`None`

- Parameters:
**tool_context**– The context of the tool.**llm_request**– The outgoing LLM request, mutable this method.


-
examples

-
*class*google.adk.tools.FunctionTool(*func*,***,*require_confirmation=False*)[¶](#google.adk.tools.FunctionTool) Bases:

`BaseTool`

A tool that wraps a user-defined Python function.

-
func
[¶](#google.adk.tools.FunctionTool.func) The function to wrap.


Initializes the FunctionTool. Extracts metadata from a callable object.

- Parameters:
**func**– The function to wrap.**require_confirmation**– Whether this tool requires confirmation. A boolean or a callable that takes the function’s arguments and returns a boolean. If the callable returns True, the tool will require confirmation from the user.


-
*async*run_async(***,*args*,*tool_context*)[¶](#google.adk.tools.FunctionTool.run_async) Runs the tool with the given arguments and context.

- Return type:
`Any`


Note

Required if this tool needs to run at the client side.

Otherwise, can be skipped, e.g. for a built-in GoogleSearch tool for Gemini.


- Parameters:
**args**– The LLM-filled arguments.**tool_context**– The context of the tool.

- Returns:
The result of running the tool.


-
func

-
*class*google.adk.tools.LongRunningFunctionTool(*func*)[¶](#google.adk.tools.LongRunningFunctionTool) Bases:

`FunctionTool`

A function tool that returns the result asynchronously.

This tool is used for long-running operations that may take a significant amount of time to complete. The framework will call the function. Once the function returns, the response will be returned asynchronously to the framework which is identified by the function_call_id.

Example:

``python tool = LongRunningFunctionTool(a_long_running_function) ``

-
is_long_running
[¶](#google.adk.tools.LongRunningFunctionTool.is_long_running) Whether the tool is a long running operation.


Initializes the FunctionTool. Extracts metadata from a callable object.

- Parameters:
**func**– The function to wrap.**require_confirmation**– Whether this tool requires confirmation. A boolean or a callable that takes the function’s arguments and returns a boolean. If the callable returns True, the tool will require confirmation from the user.


-
is_long_running

-
*class*google.adk.tools.MCPToolset(**args*,***kwargs*)[¶](#google.adk.tools.MCPToolset) Bases:

`McpToolset`

Deprecated name, use McpToolset instead.

Initializes the McpToolset.

- Parameters:
**connection_params**– The connection parameters to the MCP server. Can be:`StdioConnectionParams`

for using local mcp server (e.g. using`npx`

or`python3`

); or`SseConnectionParams`

for a local/remote SSE server; or`StreamableHTTPConnectionParams`

for local/remote Streamable http server. Note,`StdioServerParameters`

is also supported for using local mcp server (e.g. using`npx`

or`python3`

), but it does not support timeout, and we recommend to use`StdioConnectionParams`

instead when timeout is needed.**tool_filter**– Optional filter to select specific tools. Can be either: - A list of tool names to include - A ToolPredicate function for custom filtering logic**tool_name_prefix**– A prefix to be added to the name of each tool in this toolset.**errlog**– TextIO stream for error logging.**auth_scheme**– The auth scheme of the tool for tool calling**auth_credential**– The auth credential of the tool for tool calling**require_confirmation**– Whether tools in this toolset require confirmation. Can be a single boolean or a callable to apply to all tools.**header_provider**– A callable that takes a ReadonlyContext and returns a dictionary of headers to be used for the MCP session.


-
*class*google.adk.tools.McpToolset(***,*connection_params*,*tool_filter=None*,*tool_name_prefix=None*,*errlog=<_io.TextIOWrapper name='<stderr>' mode='w' encoding='utf-8'>*,*auth_scheme=None*,*auth_credential=None*,*require_confirmation=False*,*header_provider=None*)[¶](#google.adk.tools.McpToolset) Bases:

`BaseToolset`

Connects to a MCP Server, and retrieves MCP Tools into ADK Tools.

This toolset manages the connection to an MCP server and provides tools that can be used by an agent. It properly implements the BaseToolset interface for easy integration with the agent framework.

Usage:

toolset = McpToolset( connection_params=StdioServerParameters( command='npx', args=["-y", "@modelcontextprotocol/server-filesystem"], ), tool_filter=['read_file', 'list_directory'] # Optional: filter specific tools ) # Use in an agent agent = LlmAgent( model='gemini-2.0-flash', name='enterprise_assistant', instruction='Help user accessing their file systems', tools=[toolset], ) # Cleanup is handled automatically by the agent framework # But you can also manually close if needed: # await toolset.close()

Initializes the McpToolset.

- Parameters:
**connection_params**– The connection parameters to the MCP server. Can be:`StdioConnectionParams`

for using local mcp server (e.g. using`npx`

or`python3`

); or`SseConnectionParams`

for a local/remote SSE server; or`StreamableHTTPConnectionParams`

for local/remote Streamable http server. Note,`StdioServerParameters`

is also supported for using local mcp server (e.g. using`npx`

or`python3`

), but it does not support timeout, and we recommend to use`StdioConnectionParams`

instead when timeout is needed.**tool_filter**– Optional filter to select specific tools. Can be either: - A list of tool names to include - A ToolPredicate function for custom filtering logic**tool_name_prefix**– A prefix to be added to the name of each tool in this toolset.**errlog**– TextIO stream for error logging.**auth_scheme**– The auth scheme of the tool for tool calling**auth_credential**– The auth credential of the tool for tool calling**require_confirmation**– Whether tools in this toolset require confirmation. Can be a single boolean or a callable to apply to all tools.**header_provider**– A callable that takes a ReadonlyContext and returns a dictionary of headers to be used for the MCP session.


-
*async*close()[¶](#google.adk.tools.McpToolset.close) Performs cleanup and releases resources held by the toolset.

This method closes the MCP session and cleans up all associated resources. It’s designed to be safe to call multiple times and handles cleanup errors gracefully to avoid blocking application shutdown.

- Return type:
`None`


-
*classmethod*from_config(*config*,*config_abs_path*)[¶](#google.adk.tools.McpToolset.from_config) Creates an McpToolset from a configuration object.

- Return type:


-
*async*get_tools(*readonly_context=None*)[¶](#google.adk.tools.McpToolset.get_tools) Return all tools in the toolset based on the provided context.


-
*class*google.adk.tools.ToolContext(*invocation_context*,***,*function_call_id=None*,*event_actions=None*,*tool_confirmation=None*)[¶](#google.adk.tools.ToolContext) Bases:

`CallbackContext`

The context of the tool.

This class provides the context for a tool invocation, including access to the invocation context, function call ID, event actions, and authentication response. It also provides methods for requesting credentials, retrieving authentication responses, listing artifacts, and searching memory.

-
invocation_context
[¶](#google.adk.tools.ToolContext.invocation_context) The invocation context of the tool.


-
function_call_id
[¶](#google.adk.tools.ToolContext.function_call_id) The function call id of the current tool call. This id was returned in the function call event from LLM to identify a function call. If LLM didn’t return this id, ADK will assign one to it. This id is used to map function call response to the original function call.


-
event_actions
[¶](#google.adk.tools.ToolContext.event_actions) The event actions of the current tool call.


-
tool_confirmation
[¶](#google.adk.tools.ToolContext.tool_confirmation) The tool confirmation of the current tool call.


-
*property*actions*:*[EventActions](#google.adk.events.EventActions)[¶](#google.adk.tools.ToolContext.actions)

-
get_auth_response(
*auth_config*)[¶](#google.adk.tools.ToolContext.get_auth_response) - Return type:
`AuthCredential`


-
request_confirmation(
***,*hint=None*,*payload=None*)[¶](#google.adk.tools.ToolContext.request_confirmation) Requests confirmation for the given function call.

- Return type:
`None`

- Parameters:
**hint**– A hint to the user on how to confirm the tool call.**payload**– The payload used to confirm the tool call.


-
request_credential(
*auth_config*)[¶](#google.adk.tools.ToolContext.request_credential) - Return type:
`None`


-
*async*search_memory(*query*)[¶](#google.adk.tools.ToolContext.search_memory) Searches the memory of the current user.

- Return type:
`SearchMemoryResponse`


-
invocation_context

-
*class*google.adk.tools.TransferToAgentTool(*agent_names*)[¶](#google.adk.tools.TransferToAgentTool) Bases:

`FunctionTool`

A specialized FunctionTool for agent transfer with enum constraints.

This tool enhances the base transfer_to_agent function by adding JSON Schema enum constraints to the agent_name parameter. This prevents LLMs from hallucinating invalid agent names by restricting choices to only valid agents.

-
agent_names
[¶](#google.adk.tools.TransferToAgentTool.agent_names) List of valid agent names that can be transferred to.


Initialize the TransferToAgentTool.

- Parameters:
**agent_names**– List of valid agent names that can be transferred to.

-
agent_names

-
*class*google.adk.tools.VertexAiSearchTool(***,*data_store_id=None*,*data_store_specs=None*,*search_engine_id=None*,*filter=None*,*max_results=None*,*bypass_multi_tools_limit=False*)[¶](#google.adk.tools.VertexAiSearchTool) Bases:

`BaseTool`

A built-in tool using Vertex AI Search.

-
data_store_id
[¶](#google.adk.tools.VertexAiSearchTool.data_store_id) The Vertex AI search data store resource ID.


-
search_engine_id
[¶](#google.adk.tools.VertexAiSearchTool.search_engine_id) The Vertex AI search engine resource ID.


Initializes the Vertex AI Search tool.

- Parameters:
**data_store_id**– The Vertex AI search data store resource ID in the format of “projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}”.**data_store_specs**– Specifications that define the specific DataStores to be searched. It should only be set if engine is used.**search_engine_id**– The Vertex AI search engine resource ID in the format of “projects/{project}/locations/{location}/collections/{collection}/engines/{engine}”.**filter**– The filter to apply to the search results.**max_results**– The maximum number of results to return.**bypass_multi_tools_limit**– Whether to bypass the multi tools limitation, so that the tool can be used with other tools in the same agent.

- Raises:
**ValueError**– If both data_store_id and search_engine_id are not specified**or both are specified.**–


-
*async*process_llm_request(***,*tool_context*,*llm_request*)[¶](#google.adk.tools.VertexAiSearchTool.process_llm_request) Processes the outgoing LLM request for this tool.

Use cases: - Most common use case is adding this tool to the LLM request. - Some tools may just preprocess the LLM request before it’s sent out.

- Return type:
`None`

- Parameters:
**tool_context**– The context of the tool.**llm_request**– The outgoing LLM request, mutable this method.


-
data_store_id

-
google.adk.tools.exit_loop(
*tool_context*)[¶](#google.adk.tools.exit_loop) Exits the loop.

Call this function only when you are instructed to do so.


-
google.adk.tools.transfer_to_agent(
*agent_name*,*tool_context*)[¶](#google.adk.tools.transfer_to_agent) Transfer the question to another agent.

This tool hands off control to another agent when it’s more suitable to answer the user’s question according to the agent’s description.

- Return type:
`None`


Note

For most use cases, you should use TransferToAgentTool instead of this function directly. TransferToAgentTool provides additional enum constraints that prevent LLMs from hallucinating invalid agent names.

- Parameters:
**agent_name**– the agent name to transfer to.


# google.adk.tools.agent_tool module[¶](#module-google.adk.tools.agent_tool)

-
*class*google.adk.tools.agent_tool.AgentTool(*agent*,*skip_summarization=False*,***,*include_plugins=True*)[¶](#google.adk.tools.agent_tool.AgentTool) Bases:

`BaseTool`

A tool that wraps an agent.

This tool allows an agent to be called as a tool within a larger application. The agent’s input schema is used to define the tool’s input parameters, and the agent’s output is returned as the tool’s result.

-
agent
[¶](#google.adk.tools.agent_tool.AgentTool.agent) The agent to wrap.


-
skip_summarization
[¶](#google.adk.tools.agent_tool.AgentTool.skip_summarization) Whether to skip summarization of the agent output.


-
include_plugins
[¶](#google.adk.tools.agent_tool.AgentTool.include_plugins) Whether to propagate plugins from the parent runner context to the agent’s runner. When True (default), the agent will inherit all plugins from its parent. Set to False to run the agent with an isolated plugin environment.


-
*classmethod*from_config(*config*,*config_abs_path*)[¶](#google.adk.tools.agent_tool.AgentTool.from_config) Creates a tool instance from a config.

This default implementation uses inspect to automatically map config values to constructor arguments based on their type hints. Subclasses should override this method for custom initialization logic.

- Return type:
- Parameters:
**config**– The config for the tool.**config_abs_path**– The absolute path to the config file that contains the tool config.

- Returns:
The tool instance.


-
populate_name()
[¶](#google.adk.tools.agent_tool.AgentTool.populate_name) - Return type:
`Any`


-
*async*run_async(***,*args*,*tool_context*)[¶](#google.adk.tools.agent_tool.AgentTool.run_async) Runs the tool with the given arguments and context.

- Return type:
`Any`


Note

Required if this tool needs to run at the client side.

Otherwise, can be skipped, e.g. for a built-in GoogleSearch tool for Gemini.


- Parameters:
**args**– The LLM-filled arguments.**tool_context**– The context of the tool.

- Returns:
The result of running the tool.


-
agent

-
*pydantic model*google.adk.tools.agent_tool.AgentToolConfig[¶](#google.adk.tools.agent_tool.AgentToolConfig) Bases:

`BaseToolConfig`

The config for the AgentTool.

## Show JSON schema

{ "title": "AgentToolConfig", "description": "The config for the AgentTool.", "type": "object", "properties": { "agent": { "$ref": "#/$defs/AgentRefConfig" }, "skip_summarization": { "default": false, "title": "Skip Summarization", "type": "boolean" }, "include_plugins": { "default": true, "title": "Include Plugins", "type": "boolean" } }, "$defs": { "AgentRefConfig": { "additionalProperties": false, "description": "The config for the reference to another agent.", "properties": { "config_path": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Config Path" }, "code": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Code" } }, "title": "AgentRefConfig", "type": "object" } }, "additionalProperties": false, "required": [ "agent" ] }

- Fields:

-
*field*agent*: AgentRefConfig**[Required]*[¶](#google.adk.tools.agent_tool.AgentToolConfig.agent) The reference to the agent instance.


-
*field*include_plugins*: bool**= True*[¶](#google.adk.tools.agent_tool.AgentToolConfig.include_plugins) Whether to include plugins from parent runner context.


-
*field*skip_summarization*: bool**= False*[¶](#google.adk.tools.agent_tool.AgentToolConfig.skip_summarization) Whether to skip summarization of the agent output.


# google.adk.tools.apihub_tool module[¶](#module-google.adk.tools.apihub_tool)

-
*class*google.adk.tools.apihub_tool.APIHubToolset(***,*apihub_resource_name*,*access_token=None*,*service_account_json=None*,*name=''*,*description=''*,*lazy_load_spec=False*,*auth_scheme=None*,*auth_credential=None*,*apihub_client=None*,*tool_filter=None*)[¶](#google.adk.tools.apihub_tool.APIHubToolset) Bases:

`BaseToolset`

APIHubTool generates tools from a given API Hub resource.

Examples:

apihub_toolset = APIHubToolset( apihub_resource_name="projects/test-project/locations/us-central1/apis/test-api", service_account_json="...", tool_filter=lambda tool, ctx=None: tool.name in ('my_tool', 'my_other_tool') ) # Get all available tools agent = LlmAgent(tools=apihub_toolset)

**apihub_resource_name**is the resource name from API Hub. It must include API name, and can optionally include API version and spec name.If apihub_resource_name includes a spec resource name, the content of that spec will be used for generating the tools.

If apihub_resource_name includes only an api or a version name, the first spec of the first version of that API will be used.


Initializes the APIHubTool with the given parameters.

Examples:

apihub_toolset = APIHubToolset( apihub_resource_name="projects/test-project/locations/us-central1/apis/test-api", service_account_json="...", ) # Get all available tools agent = LlmAgent(tools=[apihub_toolset]) apihub_toolset = APIHubToolset( apihub_resource_name="projects/test-project/locations/us-central1/apis/test-api", service_account_json="...", tool_filter = ['my_tool'] ) # Get a specific tool agent = LlmAgent(tools=[ ..., apihub_toolset, ])

**apihub_resource_name**is the resource name from API Hub. It must include API name, and can optionally include API version and spec name.If apihub_resource_name includes a spec resource name, the content of that spec will be used for generating the tools.

If apihub_resource_name includes only an api or a version name, the first spec of the first version of that API will be used.


Example:

projects/xxx/locations/us-central1/apis/apiname/…

[https://console.cloud.google.com/apigee/api-hub/apis/apiname?project=xxx](https://console.cloud.google.com/apigee/api-hub/apis/apiname?project=xxx)

- Parameters:
**apihub_resource_name**– The resource name of the API in API Hub. Example:`projects/test-project/locations/us-central1/apis/test-api`

.**access_token**– Google Access token. Generate with gcloud cli`gcloud auth print-access-token`

. Used for fetching API Specs from API Hub.**service_account_json**– The service account config as a json string. Required if not using default service credential. It is used for creating the API Hub client and fetching the API Specs from API Hub.**apihub_client**– Optional custom API Hub client.**name**– Name of the toolset. Optional.**description**– Description of the toolset. Optional.**auth_scheme**– Auth scheme that applies to all the tool in the toolset.**auth_credential**– Auth credential that applies to all the tool in the toolset.**lazy_load_spec**– If True, the spec will be loaded lazily when needed. Otherwise, the spec will be loaded immediately and the tools will be generated during initialization.**tool_filter**– The filter used to filter the tools in the toolset. It can be either a tool predicate or a list of tool names of the tools to expose.


-
*async*close()[¶](#google.adk.tools.apihub_tool.APIHubToolset.close) Performs cleanup and releases resources held by the toolset.

Note

This method is invoked, for example, at the end of an agent server’s lifecycle or when the toolset is no longer needed. Implementations should ensure that any open connections, files, or other managed resources are properly released to prevent leaks.


-
*async*get_tools(*readonly_context=None*)[¶](#google.adk.tools.apihub_tool.APIHubToolset.get_tools) Retrieves all available tools.

- Return type:
`List`

[]`RestApiTool`

- Returns:
A list of all available RestApiTool objects.


# google.adk.tools.application_integration_tool module[¶](#module-google.adk.tools.application_integration_tool)

-
*class*google.adk.tools.application_integration_tool.ApplicationIntegrationToolset(*project*,*location*,*connection_template_override=None*,*integration=None*,*triggers=None*,*connection=None*,*entity_operations=None*,*actions=None*,*tool_name_prefix=''*,*tool_instructions=''*,*service_account_json=None*,*auth_scheme=None*,*auth_credential=None*,*tool_filter=None*)[¶](#google.adk.tools.application_integration_tool.ApplicationIntegrationToolset) Bases:

`BaseToolset`

ApplicationIntegrationToolset generates tools from a given Application Integration or Integration Connector resource.

Example Usage:

# Get all available tools for an integration with api trigger application_integration_toolset = ApplicationIntegrationToolset( project="test-project", location="us-central1" integration="test-integration", triggers=["api_trigger/test_trigger"], service_account_credentials={...}, ) # Get all available tools for a connection using entity operations and # actions # Note: Find the list of supported entity operations and actions for a # connection using integration connector apis: # https://cloud.google.com/integration-connectors/docs/reference/rest/v1/projects.locations.connections.connectionSchemaMetadata application_integration_toolset = ApplicationIntegrationToolset( project="test-project", location="us-central1" connection="test-connection", entity_operations=["EntityId1": ["LIST","CREATE"], "EntityId2": []], #empty list for actions means all operations on the entity are supported actions=["action1"], service_account_credentials={...}, ) # Feed the toolset to agent agent = LlmAgent(tools=[ ..., application_integration_toolset, ])

Args:

- Parameters:
**project**– The GCP project ID.**location**– The GCP location.**connection_template_override**– Overrides ExecuteConnection default integration name.**integration**– The integration name.**triggers**– The list of trigger names in the integration.**connection**– The connection name.**entity_operations**– The entity operations supported by the connection.**actions**– The actions supported by the connection.**tool_name_prefix**– The name prefix of the generated tools.**tool_instructions**– The instructions for the tool.**service_account_json**– The service account configuration as a dictionary. Required if not using default service credential. Used for fetching the Application Integration or Integration Connector resource.**tool_filter**– The filter used to filter the tools in the toolset. It can be either a tool predicate or a list of tool names of the tools to expose.

- Raises:
**ValueError**– If none of the following conditions are met: -`integration`

is provided. -`connection`

is provided and at least one of`entity_operations`

or`actions`

is provided.**Exception**– If there is an error during the initialization of the integration or connection client.


-
*async*close()[¶](#google.adk.tools.application_integration_tool.ApplicationIntegrationToolset.close) Performs cleanup and releases resources held by the toolset.

- Return type:
`None`


Note

This method is invoked, for example, at the end of an agent server’s lifecycle or when the toolset is no longer needed. Implementations should ensure that any open connections, files, or other managed resources are properly released to prevent leaks.


-
*async*get_tools(*readonly_context=None*)[¶](#google.adk.tools.application_integration_tool.ApplicationIntegrationToolset.get_tools) Return all tools in the toolset based on the provided context.

- Return type:
`List`

[]`RestApiTool`

- Parameters:
**readonly_context**(*ReadonlyContext**,**optional*) – Context used to filter tools available to the agent. If None, all tools in the toolset are returned.- Returns:
A list of tools available under the specified context.

- Return type:
list[

[BaseTool](#google.adk.tools.BaseTool)]


-
*class*google.adk.tools.application_integration_tool.IntegrationConnectorTool(*name*,*description*,*connection_name*,*connection_host*,*connection_service_name*,*entity*,*operation*,*action*,*rest_api_tool*,*auth_scheme=None*,*auth_credential=None*)[¶](#google.adk.tools.application_integration_tool.IntegrationConnectorTool) Bases:

`BaseTool`

A tool that wraps a RestApiTool to interact with a specific Application Integration endpoint.

This tool adds Application Integration specific context like connection details, entity, operation, and action to the underlying REST API call handled by RestApiTool. It prepares the arguments and then delegates the actual API call execution to the contained RestApiTool instance.

Generates request params and body

Attaches auth credentials to API call.


Example:

# Each API operation in the spec will be turned into its own tool # Name of the tool is the operationId of that operation, in snake case operations = OperationGenerator().parse(openapi_spec_dict) tool = [RestApiTool.from_parsed_operation(o) for o in operations]

Initializes the ApplicationIntegrationTool.

- Parameters:
**name**– The name of the tool, typically derived from the API operation. Should be unique and adhere to Gemini function naming conventions (e.g., less than 64 characters).**description**– A description of what the tool does, usually based on the API operation’s summary or description.**connection_name**– The name of the Integration Connector connection.**connection_host**– The hostname or IP address for the connection.**connection_service_name**– The specific service name within the host.**entity**– The Integration Connector entity being targeted.**operation**– The specific operation being performed on the entity.**action**– The action associated with the operation (e.g., ‘execute’).**rest_api_tool**– An initialized RestApiTool instance that handles the underlying REST API communication based on an OpenAPI specification operation. This tool will be called by ApplicationIntegrationTool with added connection and context arguments. tool = [RestApiTool.from_parsed_operation(o) for o in operations]


-
EXCLUDE_FIELDS
*= ['connection_name', 'service_name', 'host', 'entity', 'operation', 'action', 'dynamic_auth_config']*[¶](#google.adk.tools.application_integration_tool.IntegrationConnectorTool.EXCLUDE_FIELDS)

-
OPTIONAL_FIELDS
*= ['page_size', 'page_token', 'filter', 'sortByColumns']*[¶](#google.adk.tools.application_integration_tool.IntegrationConnectorTool.OPTIONAL_FIELDS)

-
*async*run_async(***,*args*,*tool_context*)[¶](#google.adk.tools.application_integration_tool.IntegrationConnectorTool.run_async) Runs the tool with the given arguments and context.

- Return type:
`Dict`

[`str`

,`Any`

]

Note

Required if this tool needs to run at the client side.

Otherwise, can be skipped, e.g. for a built-in GoogleSearch tool for Gemini.


- Parameters:
**args**– The LLM-filled arguments.**tool_context**– The context of the tool.

- Returns:
The result of running the tool.


# google.adk.tools.authenticated_function_tool module[¶](#module-google.adk.tools.authenticated_function_tool)

-
*class*google.adk.tools.authenticated_function_tool.AuthenticatedFunctionTool(***,*func*,*auth_config=None*,*response_for_auth_required=None*)[¶](#google.adk.tools.authenticated_function_tool.AuthenticatedFunctionTool) Bases:

`FunctionTool`

A FunctionTool that handles authentication before the actual tool logic gets called. Functions can accept a special credential argument which is the credential ready for use.(Experimental)

Initializes the AuthenticatedFunctionTool.

- Parameters:
**func**– The function to be called.**auth_config**– The authentication configuration.**response_for_auth_required**– The response to return when the tool is requesting auth credential from the client. There could be two case, the tool doesn’t configure any credentials (auth_config.raw_auth_credential is missing) or the credentials configured is not enough to authenticate the tool (e.g. an OAuth client id and client secret are configured) and needs client input (e.g. client need to involve the end user in an oauth flow and get back the oauth response.)


-
*async*run_async(***,*args*,*tool_context*)[¶](#google.adk.tools.authenticated_function_tool.AuthenticatedFunctionTool.run_async) Runs the tool with the given arguments and context.

- Return type:
`Any`


Note

Required if this tool needs to run at the client side.

Otherwise, can be skipped, e.g. for a built-in GoogleSearch tool for Gemini.


- Parameters:
**args**– The LLM-filled arguments.**tool_context**– The context of the tool.

- Returns:
The result of running the tool.


# google.adk.tools.base_authenticated_tool module[¶](#module-google.adk.tools.base_authenticated_tool)

-
*class*google.adk.tools.base_authenticated_tool.BaseAuthenticatedTool(***,*name*,*description*,*auth_config=None*,*response_for_auth_required=None*)[¶](#google.adk.tools.base_authenticated_tool.BaseAuthenticatedTool) Bases:

`BaseTool`

A base tool class that handles authentication before the actual tool logic gets called. Functions can accept a special credential argument which is the credential ready for use.(Experimental)

- Parameters:
**name**– The name of the tool.**description**– The description of the tool.**auth_config**– The auth configuration of the tool.**response_for_auth_required**– The response to return when the tool is requesting auth credential from the client. There could be two case, the tool doesn’t configure any credentials (auth_config.raw_auth_credential is missing) or the credentials configured is not enough to authenticate the tool (e.g. an OAuth client id and client secret are configured) and needs client input (e.g. client need to involve the end user in an oauth flow and get back the oauth response.)


-
*async*run_async(***,*args*,*tool_context*)[¶](#google.adk.tools.base_authenticated_tool.BaseAuthenticatedTool.run_async) Runs the tool with the given arguments and context.

- Return type:
`Any`


Note

Required if this tool needs to run at the client side.

Otherwise, can be skipped, e.g. for a built-in GoogleSearch tool for Gemini.


- Parameters:
**args**– The LLM-filled arguments.**tool_context**– The context of the tool.

- Returns:
The result of running the tool.


# google.adk.tools.base_tool module[¶](#module-google.adk.tools.base_tool)

-
*class*google.adk.tools.base_tool.BaseTool(***,*name*,*description*,*is_long_running=False*,*custom_metadata=None*)[¶](#google.adk.tools.base_tool.BaseTool) Bases:

`ABC`

The base class for all tools.

-
custom_metadata
*: dict[str, Any] | None**= None*[¶](#google.adk.tools.base_tool.BaseTool.custom_metadata) The custom metadata of the BaseTool.

An optional key-value pair for storing and retrieving tool-specific metadata, such as tool manifests, etc.

NOTE: the entire dict must be JSON serializable.


-
description
*: str*[¶](#google.adk.tools.base_tool.BaseTool.description) The description of the tool.


-
*classmethod*from_config(*config*,*config_abs_path*)[¶](#google.adk.tools.base_tool.BaseTool.from_config) Creates a tool instance from a config.

This default implementation uses inspect to automatically map config values to constructor arguments based on their type hints. Subclasses should override this method for custom initialization logic.

- Return type:
`TypeVar`

(`SelfTool`

, bound= BaseTool)- Parameters:
**config**– The config for the tool.**config_abs_path**– The absolute path to the config file that contains the tool config.

- Returns:
The tool instance.


-
is_long_running
*: bool**= False*[¶](#google.adk.tools.base_tool.BaseTool.is_long_running) Whether the tool is a long running operation, which typically returns a resource id first and finishes the operation later.


-
name
*: str*[¶](#google.adk.tools.base_tool.BaseTool.name) The name of the tool.


-
*async*process_llm_request(***,*tool_context*,*llm_request*)[¶](#google.adk.tools.base_tool.BaseTool.process_llm_request) Processes the outgoing LLM request for this tool.

Use cases: - Most common use case is adding this tool to the LLM request. - Some tools may just preprocess the LLM request before it’s sent out.

- Return type:
`None`

- Parameters:
**tool_context**– The context of the tool.**llm_request**– The outgoing LLM request, mutable this method.


-
*async*run_async(***,*args*,*tool_context*)[¶](#google.adk.tools.base_tool.BaseTool.run_async) Runs the tool with the given arguments and context.

- Return type:
`Any`


Note

Required if this tool needs to run at the client side.

Otherwise, can be skipped, e.g. for a built-in GoogleSearch tool for Gemini.


- Parameters:
**args**– The LLM-filled arguments.**tool_context**– The context of the tool.

- Returns:
The result of running the tool.


-
custom_metadata

# google.adk.tools.base_toolset module[¶](#module-google.adk.tools.base_toolset)

-
*class*google.adk.tools.base_toolset.BaseToolset(***,*tool_filter=None*,*tool_name_prefix=None*)[¶](#google.adk.tools.base_toolset.BaseToolset) Bases:

`ABC`

Base class for toolset.

A toolset is a collection of tools that can be used by an agent.

Initialize the toolset.

- Parameters:
**tool_filter**– Filter to apply to tools.**tool_name_prefix**– The prefix to prepend to the names of the tools returned by the toolset.


-
*async*close()[¶](#google.adk.tools.base_toolset.BaseToolset.close) Performs cleanup and releases resources held by the toolset.

- Return type:
`None`


Note

This method is invoked, for example, at the end of an agent server’s lifecycle or when the toolset is no longer needed. Implementations should ensure that any open connections, files, or other managed resources are properly released to prevent leaks.


-
*classmethod*from_config(*config*,*config_abs_path*)[¶](#google.adk.tools.base_toolset.BaseToolset.from_config) Creates a toolset instance from a config.

- Return type:
`TypeVar`

(`SelfToolset`

, bound= BaseToolset)- Parameters:
**config**– The config for the tool.**config_abs_path**– The absolute path to the config file that contains the tool config.

- Returns:
The toolset instance.


-
*abstractmethod async*get_tools(*readonly_context=None*)[¶](#google.adk.tools.base_toolset.BaseToolset.get_tools) Return all tools in the toolset based on the provided context.


-
*final async*get_tools_with_prefix(*readonly_context=None*)[¶](#google.adk.tools.base_toolset.BaseToolset.get_tools_with_prefix) Return all tools with optional prefix applied to tool names.

This method calls get_tools() and applies prefixing if tool_name_prefix is provided.


-
*async*process_llm_request(***,*tool_context*,*llm_request*)[¶](#google.adk.tools.base_toolset.BaseToolset.process_llm_request) Processes the outgoing LLM request for this toolset. This method will be called before each tool processes the llm request.

- Return type:
`None`


Use cases: - Instead of let each tool process the llm request, we can let the toolset

process the llm request. e.g. ComputerUseToolset can add computer use tool to the llm request.

- Parameters:
**tool_context**– The context of the tool.**llm_request**– The outgoing LLM request, mutable this method.


-
*class*google.adk.tools.base_toolset.ToolPredicate(**args*,***kwargs*)[¶](#google.adk.tools.base_toolset.ToolPredicate) Bases:

`Protocol`

Base class for a predicate that defines the interface to decide whether a

tool should be exposed to LLM. Toolset implementer could consider whether to accept such instance in the toolset’s constructor and apply the predicate in get_tools method.


# google.adk.tools.bigquery module[¶](#module-google.adk.tools.bigquery)

BigQuery Tools (Experimental).

BigQuery Tools under this module are hand crafted and customized while the tools under google.adk.tools.google_api_tool are auto generated based on API definition. The rationales to have customized tool are:

BigQuery APIs have functions overlaps and LLM can’t tell what tool to use

BigQuery APIs have a lot of parameters with some rarely used, which are not LLM-friendly

We want to provide more high-level tools like forecasting, RAG, segmentation, etc.

We want to provide extra access guardrails in those tools. For example, execute_sql can’t arbitrarily mutate existing data.


-
*pydantic model*google.adk.tools.bigquery.BigQueryCredentialsConfig[¶](#google.adk.tools.bigquery.BigQueryCredentialsConfig) Bases:

`BaseGoogleCredentialsConfig`

BigQuery Credentials Configuration for Google API tools (Experimental).

Please do not use this in production, as it may be deprecated later.

## Show JSON schema

{ "title": "BigQueryCredentialsConfig", "type": "object", "properties": { "credentials": { "default": null, "title": "Credentials" }, "client_id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Client Id" }, "client_secret": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Client Secret" }, "scopes": { "anyOf": [ { "items": { "type": "string" }, "type": "array" }, { "type": "null" } ], "default": null, "title": "Scopes" } }, "additionalProperties": false }

- Fields:
- Validators:
`__post_init__`

»`all fields`


-
model_post_init(
*context*,*/*)[¶](#google.adk.tools.bigquery.BigQueryCredentialsConfig.model_post_init) This function is meant to behave like a BaseModel method to initialise private attributes.

It takes context as an argument since that’s what pydantic-core passes when calling it.

- Return type:
`None`

- Parameters:
**self**– The BaseModel instance.**context**– The context.


-
*class*google.adk.tools.bigquery.BigQueryToolset(***,*tool_filter=None*,*credentials_config=None*,*bigquery_tool_config=None*)[¶](#google.adk.tools.bigquery.BigQueryToolset) Bases:

`BaseToolset`

BigQuery Toolset contains tools for interacting with BigQuery data and metadata.

Initialize the toolset.

- Parameters:
**tool_filter**– Filter to apply to tools.**tool_name_prefix**– The prefix to prepend to the names of the tools returned by the toolset.


-
*async*close()[¶](#google.adk.tools.bigquery.BigQueryToolset.close) Performs cleanup and releases resources held by the toolset.

Note

This method is invoked, for example, at the end of an agent server’s lifecycle or when the toolset is no longer needed. Implementations should ensure that any open connections, files, or other managed resources are properly released to prevent leaks.


# google.adk.tools.crewai_tool module[¶](#google-adk-tools-crewai-tool-module)

# google.adk.tools.enterprise_search_tool module[¶](#module-google.adk.tools.enterprise_search_tool)

-
*class*google.adk.tools.enterprise_search_tool.EnterpriseWebSearchTool[¶](#google.adk.tools.enterprise_search_tool.EnterpriseWebSearchTool) Bases:

`BaseTool`

A Gemini 2+ built-in tool using web grounding for Enterprise compliance.

NOTE: This tool is not the same as Vertex AI Search, which is used to be called “Enterprise Search”.

See the documentation for more details:

[https://cloud.google.com/vertex-ai/generative-ai/docs/grounding/web-grounding-enterprise](https://cloud.google.com/vertex-ai/generative-ai/docs/grounding/web-grounding-enterprise).Initializes the Enterprise Web Search tool.

-
*async*process_llm_request(***,*tool_context*,*llm_request*)[¶](#google.adk.tools.enterprise_search_tool.EnterpriseWebSearchTool.process_llm_request) Processes the outgoing LLM request for this tool.

Use cases: - Most common use case is adding this tool to the LLM request. - Some tools may just preprocess the LLM request before it’s sent out.

- Return type:
`None`

- Parameters:
**tool_context**– The context of the tool.**llm_request**– The outgoing LLM request, mutable this method.


-

# google.adk.tools.example_tool module[¶](#module-google.adk.tools.example_tool)

-
*class*google.adk.tools.example_tool.ExampleTool(*examples*)[¶](#google.adk.tools.example_tool.ExampleTool) Bases:

`BaseTool`

A tool that adds (few-shot) examples to the LLM request.

-
examples
[¶](#google.adk.tools.example_tool.ExampleTool.examples) The examples to add to the LLM request.


-
*classmethod*from_config(*config*,*config_abs_path*)[¶](#google.adk.tools.example_tool.ExampleTool.from_config) Creates a tool instance from a config.

This default implementation uses inspect to automatically map config values to constructor arguments based on their type hints. Subclasses should override this method for custom initialization logic.

- Return type:
- Parameters:
**config**– The config for the tool.**config_abs_path**– The absolute path to the config file that contains the tool config.

- Returns:
The tool instance.


-
*async*process_llm_request(***,*tool_context*,*llm_request*)[¶](#google.adk.tools.example_tool.ExampleTool.process_llm_request) Processes the outgoing LLM request for this tool.

Use cases: - Most common use case is adding this tool to the LLM request. - Some tools may just preprocess the LLM request before it’s sent out.

- Return type:
`None`

- Parameters:
**tool_context**– The context of the tool.**llm_request**– The outgoing LLM request, mutable this method.


-
examples

-
*pydantic model*google.adk.tools.example_tool.ExampleToolConfig[¶](#google.adk.tools.example_tool.ExampleToolConfig) Bases:

`BaseToolConfig`

## Show JSON schema

{ "title": "ExampleToolConfig", "type": "object", "properties": { "examples": { "anyOf": [ { "items": { "$ref": "#/$defs/Example" }, "type": "array" }, { "type": "string" } ], "title": "Examples" } }, "$defs": { "Blob": { "additionalProperties": false, "description": "Content blob.", "properties": { "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Raw bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob. Used to provide a label or filename to distinguish blobs. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "Blob", "type": "object" }, "CodeExecutionResult": { "additionalProperties": false, "description": "Result of executing the [ExecutableCode].\n\nOnly generated when using the [CodeExecution] tool, and always follows a\n`part` containing the [ExecutableCode].", "properties": { "outcome": { "anyOf": [ { "$ref": "#/$defs/Outcome" }, { "type": "null" } ], "default": null, "description": "Required. Outcome of the code execution." }, "output": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Contains stdout when code execution is successful, stderr or other description otherwise.", "title": "Output" } }, "title": "CodeExecutionResult", "type": "object" }, "Content": { "additionalProperties": false, "description": "Contains the multi-part content of a message.", "properties": { "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/Part" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a single message. Each part may have\n a different IANA MIME type.", "title": "Parts" }, "role": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The producer of the content. Must be either 'user' or 'model'. Useful to set for multi-turn conversations, otherwise can be left blank or unset.", "title": "Role" } }, "title": "Content", "type": "object" }, "Example": { "description": "A few-shot example.\n\nAttributes:\n input: The input content for the example.\n output: The expected output content for the example.", "properties": { "input": { "$ref": "#/$defs/Content" }, "output": { "items": { "$ref": "#/$defs/Content" }, "title": "Output", "type": "array" } }, "required": [ "input", "output" ], "title": "Example", "type": "object" }, "ExecutableCode": { "additionalProperties": false, "description": "Code generated by the model that is meant to be executed, and the result returned to the model.\n\nGenerated when using the [CodeExecution] tool, in which the code will be\nautomatically executed, and a corresponding [CodeExecutionResult] will also be\ngenerated.", "properties": { "code": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The code to be executed.", "title": "Code" }, "language": { "anyOf": [ { "$ref": "#/$defs/Language" }, { "type": "null" } ], "default": null, "description": "Required. Programming language of the `code`." } }, "title": "ExecutableCode", "type": "object" }, "FileData": { "additionalProperties": false, "description": "URI based data.", "properties": { "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file data. Used to provide a label or filename to distinguish file datas. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "FileData", "type": "object" }, "FunctionCall": { "additionalProperties": false, "description": "A function call.", "properties": { "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The unique id of the function call. If populated, the client to execute the\n `function_call` and return the response with the matching `id`.", "title": "Id" }, "args": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Optional. The function parameters and values in JSON object format. See [FunctionDeclaration.parameters] for parameter details.", "title": "Args" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The name of the function to call. Matches [FunctionDeclaration.name].", "title": "Name" }, "partialArgs": { "anyOf": [ { "items": { "$ref": "#/$defs/PartialArg" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. The partial argument value of the function call. If provided, represents the arguments/fields that are streamed incrementally. This field is not supported in Gemini API.", "title": "Partialargs" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is the last part of the FunctionCall. If true, another partial message for the current FunctionCall is expected to follow. This field is not supported in Gemini API.", "title": "Willcontinue" } }, "title": "FunctionCall", "type": "object" }, "FunctionResponse": { "additionalProperties": false, "description": "A function response.", "properties": { "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Signals that function call continues, and more responses will be returned, turning the function call into a generator. Is only applicable to NON_BLOCKING function calls (see FunctionDeclaration.behavior for details), ignored otherwise. If false, the default, future responses will not be considered. Is only applicable to NON_BLOCKING function calls, is ignored otherwise. If set to false, future responses will not be considered. It is allowed to return empty `response` with `will_continue=False` to signal that the function call is finished.", "title": "Willcontinue" }, "scheduling": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseScheduling" }, { "type": "null" } ], "default": null, "description": "Specifies how the response should be scheduled in the conversation. Only applicable to NON_BLOCKING function calls, is ignored otherwise. Defaults to WHEN_IDLE." }, "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/FunctionResponsePart" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a function response. Each part may\n have a different IANA MIME type.", "title": "Parts" }, "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The id of the function call this response is for. Populated by the client to match the corresponding function call `id`.", "title": "Id" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The name of the function to call. Matches [FunctionDeclaration.name] and [FunctionCall.name].", "title": "Name" }, "response": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Required. The function response in JSON object format. Use \"output\" key to specify function output and \"error\" key to specify error details (if any). If \"output\" and \"error\" keys are not specified, then whole \"response\" is treated as function output.", "title": "Response" } }, "title": "FunctionResponse", "type": "object" }, "FunctionResponseBlob": { "additionalProperties": false, "description": "Raw media bytes for function response.\n\nText should not be sent as raw bytes, use the FunctionResponse.response\nfield.", "properties": { "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Inline media bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob.\n Used to provide a label or filename to distinguish blobs.", "title": "Displayname" } }, "title": "FunctionResponseBlob", "type": "object" }, "FunctionResponseFileData": { "additionalProperties": false, "description": "URI based data for function response.", "properties": { "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file.\n Used to provide a label or filename to distinguish files.", "title": "Displayname" } }, "title": "FunctionResponseFileData", "type": "object" }, "FunctionResponsePart": { "additionalProperties": false, "description": "A datatype containing media that is part of a `FunctionResponse` message.\n\nA `FunctionResponsePart` consists of data which has an associated datatype. A\n`FunctionResponsePart` can only contain one of the accepted types in\n`FunctionResponsePart.data`.\n\nA `FunctionResponsePart` must have a fixed IANA MIME type identifying the\ntype and subtype of the media if the `inline_data` field is filled with raw\nbytes.", "properties": { "inlineData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseBlob" }, { "type": "null" } ], "default": null, "description": "Optional. Inline media bytes." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseFileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." } }, "title": "FunctionResponsePart", "type": "object" }, "FunctionResponseScheduling": { "description": "Specifies how the response should be scheduled in the conversation.", "enum": [ "SCHEDULING_UNSPECIFIED", "SILENT", "WHEN_IDLE", "INTERRUPT" ], "title": "FunctionResponseScheduling", "type": "string" }, "Language": { "description": "Programming language of the `code`.", "enum": [ "LANGUAGE_UNSPECIFIED", "PYTHON" ], "title": "Language", "type": "string" }, "Outcome": { "description": "Outcome of the code execution.", "enum": [ "OUTCOME_UNSPECIFIED", "OUTCOME_OK", "OUTCOME_FAILED", "OUTCOME_DEADLINE_EXCEEDED" ], "title": "Outcome", "type": "string" }, "Part": { "additionalProperties": false, "description": "A datatype containing media content.\n\nExactly one field within a Part should be set, representing the specific type\nof content being conveyed. Using multiple fields within the same `Part`\ninstance is considered invalid.", "properties": { "mediaResolution": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolution" }, { "type": "null" } ], "default": null, "description": "Media resolution for the input media.\n " }, "codeExecutionResult": { "anyOf": [ { "$ref": "#/$defs/CodeExecutionResult" }, { "type": "null" } ], "default": null, "description": "Optional. Result of executing the [ExecutableCode]." }, "executableCode": { "anyOf": [ { "$ref": "#/$defs/ExecutableCode" }, { "type": "null" } ], "default": null, "description": "Optional. Code generated by the model that is meant to be executed." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." }, "functionCall": { "anyOf": [ { "$ref": "#/$defs/FunctionCall" }, { "type": "null" } ], "default": null, "description": "Optional. A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] with the parameters and their values." }, "functionResponse": { "anyOf": [ { "$ref": "#/$defs/FunctionResponse" }, { "type": "null" } ], "default": null, "description": "Optional. The result output of a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function call. It is used as context to the model." }, "inlineData": { "anyOf": [ { "$ref": "#/$defs/Blob" }, { "type": "null" } ], "default": null, "description": "Optional. Inlined bytes data." }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Text part (can be code).", "title": "Text" }, "thought": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Indicates if the part is thought from the model.", "title": "Thought" }, "thoughtSignature": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. An opaque signature for the thought so it can be reused in subsequent requests.", "title": "Thoughtsignature" }, "videoMetadata": { "anyOf": [ { "$ref": "#/$defs/VideoMetadata" }, { "type": "null" } ], "default": null, "description": "Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data." } }, "title": "Part", "type": "object" }, "PartMediaResolution": { "additionalProperties": false, "description": "Media resolution for the input media.", "properties": { "level": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolutionLevel" }, { "type": "null" } ], "default": null, "description": "The tokenization quality used for given media.\n " }, "numTokens": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Specifies the required sequence length for media tokenization.\n ", "title": "Numtokens" } }, "title": "PartMediaResolution", "type": "object" }, "PartMediaResolutionLevel": { "description": "The tokenization quality used for given media.", "enum": [ "MEDIA_RESOLUTION_UNSPECIFIED", "MEDIA_RESOLUTION_LOW", "MEDIA_RESOLUTION_MEDIUM", "MEDIA_RESOLUTION_HIGH", "MEDIA_RESOLUTION_ULTRA_HIGH" ], "title": "PartMediaResolutionLevel", "type": "string" }, "PartialArg": { "additionalProperties": false, "description": "Partial argument value of the function call.\n\nThis data type is not supported in Gemini API.", "properties": { "nullValue": { "anyOf": [ { "const": "NULL_VALUE", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a null value.", "title": "Nullvalue" }, "numberValue": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a double value.", "title": "Numbervalue" }, "stringValue": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a string value.", "title": "Stringvalue" }, "boolValue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a boolean value.", "title": "Boolvalue" }, "jsonPath": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. A JSON Path (RFC 9535) to the argument being streamed. https://datatracker.ietf.org/doc/html/rfc9535. e.g. \"$.foo.bar[0].data\".", "title": "Jsonpath" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is not the last part of the same json_path. If true, another PartialArg message for the current json_path is expected to follow.", "title": "Willcontinue" } }, "title": "PartialArg", "type": "object" }, "VideoMetadata": { "additionalProperties": false, "description": "Metadata describes the input video content.", "properties": { "endOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The end offset of the video.", "title": "Endoffset" }, "fps": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. The frame rate of the video sent to the model. If not specified, the default value will be 1.0. The fps range is (0.0, 24.0].", "title": "Fps" }, "startOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The start offset of the video.", "title": "Startoffset" } }, "title": "VideoMetadata", "type": "object" } }, "additionalProperties": false, "required": [ "examples" ] }


# google.adk.tools.exit_loop_tool module[¶](#module-google.adk.tools.exit_loop_tool)

-
google.adk.tools.exit_loop_tool.exit_loop(
*tool_context*)[¶](#google.adk.tools.exit_loop_tool.exit_loop) Exits the loop.

Call this function only when you are instructed to do so.


# google.adk.tools.function_tool module[¶](#module-google.adk.tools.function_tool)

-
*class*google.adk.tools.function_tool.FunctionTool(*func*,***,*require_confirmation=False*)[¶](#google.adk.tools.function_tool.FunctionTool) Bases:

`BaseTool`

A tool that wraps a user-defined Python function.

-
func
[¶](#google.adk.tools.function_tool.FunctionTool.func) The function to wrap.


Initializes the FunctionTool. Extracts metadata from a callable object.

- Parameters:
**func**– The function to wrap.**require_confirmation**– Whether this tool requires confirmation. A boolean or a callable that takes the function’s arguments and returns a boolean. If the callable returns True, the tool will require confirmation from the user.


-
*async*run_async(***,*args*,*tool_context*)[¶](#google.adk.tools.function_tool.FunctionTool.run_async) Runs the tool with the given arguments and context.

- Return type:
`Any`


Note

Required if this tool needs to run at the client side.

Otherwise, can be skipped, e.g. for a built-in GoogleSearch tool for Gemini.


- Parameters:
**args**– The LLM-filled arguments.**tool_context**– The context of the tool.

- Returns:
The result of running the tool.


-
func

# google.adk.tools.get_user_choice_tool module[¶](#module-google.adk.tools.get_user_choice_tool)

-
google.adk.tools.get_user_choice_tool.get_user_choice(
*options*,*tool_context*)[¶](#google.adk.tools.get_user_choice_tool.get_user_choice) Provides the options to the user and asks them to choose one.

- Return type:
`Optional`

[`str`

]


# google.adk.tools.google_api_tool module[¶](#module-google.adk.tools.google_api_tool)

Auto-generated tools and toolsets for Google APIs.

These tools and toolsets are auto-generated based on the API specifications provided by the Google API Discovery API.

-
*class*google.adk.tools.google_api_tool.BigQueryToolset(*client_id=None*,*client_secret=None*,*tool_filter=None*,*service_account=None*,*tool_name_prefix=None*)[¶](#google.adk.tools.google_api_tool.BigQueryToolset) Bases:

`GoogleApiToolset`

Auto-generated BigQuery toolset based on Google BigQuery API v2 spec exposed by Google API discovery API.

- Parameters:
**client_id**– OAuth2 client ID for authentication.**client_secret**– OAuth2 client secret for authentication.**tool_filter**– Optional filter to include only specific tools or use a predicate function.**service_account**– Optional service account for authentication.**tool_name_prefix**– Optional prefix to add to all tool names in this toolset.


Initialize the toolset.

- Parameters:
**tool_filter**– Filter to apply to tools.**tool_name_prefix**– The prefix to prepend to the names of the tools returned by the toolset.


-
*class*google.adk.tools.google_api_tool.CalendarToolset(*client_id=None*,*client_secret=None*,*tool_filter=None*,*service_account=None*,*tool_name_prefix=None*)[¶](#google.adk.tools.google_api_tool.CalendarToolset) Bases:

`GoogleApiToolset`

Auto-generated Calendar toolset based on Google Calendar API v3 spec exposed by Google API discovery API.

- Parameters:
**client_id**– OAuth2 client ID for authentication.**client_secret**– OAuth2 client secret for authentication.**tool_filter**– Optional filter to include only specific tools or use a predicate function.**service_account**– Optional service account for authentication.**tool_name_prefix**– Optional prefix to add to all tool names in this toolset.


Initialize the toolset.

- Parameters:
**tool_filter**– Filter to apply to tools.**tool_name_prefix**– The prefix to prepend to the names of the tools returned by the toolset.


-
*class*google.adk.tools.google_api_tool.DocsToolset(*client_id=None*,*client_secret=None*,*tool_filter=None*,*service_account=None*,*tool_name_prefix=None*)[¶](#google.adk.tools.google_api_tool.DocsToolset) Bases:

`GoogleApiToolset`

Auto-generated Docs toolset based on Google Docs API v1 spec exposed by Google API discovery API.

- Parameters:
**client_id**– OAuth2 client ID for authentication.**client_secret**– OAuth2 client secret for authentication.**tool_filter**– Optional filter to include only specific tools or use a predicate function.**service_account**– Optional service account for authentication.**tool_name_prefix**– Optional prefix to add to all tool names in this toolset.


Initialize the toolset.

- Parameters:
**tool_filter**– Filter to apply to tools.**tool_name_prefix**– The prefix to prepend to the names of the tools returned by the toolset.


-
*class*google.adk.tools.google_api_tool.GmailToolset(*client_id=None*,*client_secret=None*,*tool_filter=None*,*service_account=None*,*tool_name_prefix=None*)[¶](#google.adk.tools.google_api_tool.GmailToolset) Bases:

`GoogleApiToolset`

Auto-generated Gmail toolset based on Google Gmail API v1 spec exposed by Google API discovery API.

- Parameters:
**client_id**– OAuth2 client ID for authentication.**client_secret**– OAuth2 client secret for authentication.**tool_filter**– Optional filter to include only specific tools or use a predicate function.**service_account**– Optional service account for authentication.**tool_name_prefix**– Optional prefix to add to all tool names in this toolset.


Initialize the toolset.

- Parameters:
**tool_filter**– Filter to apply to tools.**tool_name_prefix**– The prefix to prepend to the names of the tools returned by the toolset.


-
*class*google.adk.tools.google_api_tool.GoogleApiTool(*rest_api_tool*,*client_id=None*,*client_secret=None*,*service_account=None*,***,*additional_headers=None*)[¶](#google.adk.tools.google_api_tool.GoogleApiTool) Bases:

`BaseTool`

-
configure_auth(
*client_id*,*client_secret*)[¶](#google.adk.tools.google_api_tool.GoogleApiTool.configure_auth)

-
configure_sa_auth(
*service_account*)[¶](#google.adk.tools.google_api_tool.GoogleApiTool.configure_sa_auth)

-
*async*run_async(***,*args*,*tool_context*)[¶](#google.adk.tools.google_api_tool.GoogleApiTool.run_async) Runs the tool with the given arguments and context.

- Return type:
`Dict`

[`str`

,`Any`

]

Note

Required if this tool needs to run at the client side.

Otherwise, can be skipped, e.g. for a built-in GoogleSearch tool for Gemini.


- Parameters:
**args**– The LLM-filled arguments.**tool_context**– The context of the tool.

- Returns:
The result of running the tool.


-
configure_auth(

-
*class*google.adk.tools.google_api_tool.GoogleApiToolset(*api_name*,*api_version*,*client_id=None*,*client_secret=None*,*tool_filter=None*,*service_account=None*,*tool_name_prefix=None*,***,*additional_headers=None*)[¶](#google.adk.tools.google_api_tool.GoogleApiToolset) Bases:

`BaseToolset`

Google API Toolset contains tools for interacting with Google APIs.

Usually one toolsets will contain tools only related to one Google API, e.g. Google Bigquery API toolset will contain tools only related to Google Bigquery API, like list dataset tool, list table tool etc.

- Parameters:
**api_name**– The name of the Google API (e.g., “calendar”, “gmail”).**api_version**– The version of the API (e.g., “v3”, “v1”).**client_id**– OAuth2 client ID for authentication.**client_secret**– OAuth2 client secret for authentication.**tool_filter**– Optional filter to include only specific tools or use a predicate function.**service_account**– Optional service account for authentication.**tool_name_prefix**– Optional prefix to add to all tool names in this toolset.**additional_headers**– Optional dict of HTTP headers to inject into every request executed by this toolset.


Initialize the toolset.

- Parameters:
**tool_filter**– Filter to apply to tools.**tool_name_prefix**– The prefix to prepend to the names of the tools returned by the toolset.


-
*async*close()[¶](#google.adk.tools.google_api_tool.GoogleApiToolset.close) Performs cleanup and releases resources held by the toolset.

Note

This method is invoked, for example, at the end of an agent server’s lifecycle or when the toolset is no longer needed. Implementations should ensure that any open connections, files, or other managed resources are properly released to prevent leaks.


-
configure_auth(
*client_id*,*client_secret*)[¶](#google.adk.tools.google_api_tool.GoogleApiToolset.configure_auth)

-
configure_sa_auth(
*service_account*)[¶](#google.adk.tools.google_api_tool.GoogleApiToolset.configure_sa_auth)

-
*async*get_tools(*readonly_context=None*)[¶](#google.adk.tools.google_api_tool.GoogleApiToolset.get_tools) Get all tools in the toolset.

- Return type:
`List`

[]`GoogleApiTool`


-
set_tool_filter(
*tool_filter*)[¶](#google.adk.tools.google_api_tool.GoogleApiToolset.set_tool_filter)


-
*class*google.adk.tools.google_api_tool.SheetsToolset(*client_id=None*,*client_secret=None*,*tool_filter=None*,*service_account=None*,*tool_name_prefix=None*)[¶](#google.adk.tools.google_api_tool.SheetsToolset) Bases:

`GoogleApiToolset`

Auto-generated Sheets toolset based on Google Sheets API v4 spec exposed by Google API discovery API.

- Parameters:
**client_id**– OAuth2 client ID for authentication.**client_secret**– OAuth2 client secret for authentication.**tool_filter**– Optional filter to include only specific tools or use a predicate function.**service_account**– Optional service account for authentication.**tool_name_prefix**– Optional prefix to add to all tool names in this toolset.


Initialize the toolset.

- Parameters:
**tool_filter**– Filter to apply to tools.**tool_name_prefix**– The prefix to prepend to the names of the tools returned by the toolset.


-
*class*google.adk.tools.google_api_tool.SlidesToolset(*client_id=None*,*client_secret=None*,*tool_filter=None*,*service_account=None*,*tool_name_prefix=None*)[¶](#google.adk.tools.google_api_tool.SlidesToolset) Bases:

`GoogleApiToolset`

Auto-generated Slides toolset based on Google Slides API v1 spec exposed by Google API discovery API.

- Parameters:
**client_id**– OAuth2 client ID for authentication.**client_secret**– OAuth2 client secret for authentication.**tool_filter**– Optional filter to include only specific tools or use a predicate function.**service_account**– Optional service account for authentication.**tool_name_prefix**– Optional prefix to add to all tool names in this toolset.


Initialize the toolset.

- Parameters:
**tool_filter**– Filter to apply to tools.**tool_name_prefix**– The prefix to prepend to the names of the tools returned by the toolset.


-
*class*google.adk.tools.google_api_tool.YoutubeToolset(*client_id=None*,*client_secret=None*,*tool_filter=None*,*service_account=None*,*tool_name_prefix=None*)[¶](#google.adk.tools.google_api_tool.YoutubeToolset) Bases:

`GoogleApiToolset`

Auto-generated YouTube toolset based on YouTube API v3 spec exposed by Google API discovery API.

- Parameters:
**client_id**– OAuth2 client ID for authentication.**client_secret**– OAuth2 client secret for authentication.**tool_filter**– Optional filter to include only specific tools or use a predicate function.**service_account**– Optional service account for authentication.**tool_name_prefix**– Optional prefix to add to all tool names in this toolset.


Initialize the toolset.

- Parameters:
**tool_filter**– Filter to apply to tools.**tool_name_prefix**– The prefix to prepend to the names of the tools returned by the toolset.


# google.adk.tools.google_maps_grounding_tool module[¶](#google-adk-tools-google-maps-grounding-tool-module)

-
*class*google.adk.tools.google_maps_grounding_tool.GoogleMapsGroundingTool[¶](#google.adk.tools.google_maps_grounding_tool.GoogleMapsGroundingTool) Bases:

`BaseTool`

A built-in tool that is automatically invoked by Gemini 2 models to ground query results with Google Maps.

This tool operates internally within the model and does not require or perform local code execution.

Only available for use with the VertexAI Gemini API (e.g. GOOGLE_GENAI_USE_VERTEXAI=TRUE)

-
*async*process_llm_request(***,*tool_context*,*llm_request*)[¶](#google.adk.tools.google_maps_grounding_tool.GoogleMapsGroundingTool.process_llm_request) Processes the outgoing LLM request for this tool.

Use cases: - Most common use case is adding this tool to the LLM request. - Some tools may just preprocess the LLM request before it’s sent out.

- Return type:
`None`

- Parameters:
**tool_context**– The context of the tool.**llm_request**– The outgoing LLM request, mutable this method.


-

# google.adk.tools.google_search_tool module[¶](#module-google.adk.tools.google_search_tool)

-
*class*google.adk.tools.google_search_tool.GoogleSearchTool(***,*bypass_multi_tools_limit=False*)[¶](#google.adk.tools.google_search_tool.GoogleSearchTool) Bases:

`BaseTool`

A built-in tool that is automatically invoked by Gemini 2 models to retrieve search results from Google Search.

This tool operates internally within the model and does not require or perform local code execution.

Initializes the Google search tool.

- Parameters:
**bypass_multi_tools_limit**– Whether to bypass the multi tools limitation, so that the tool can be used with other tools in the same agent.

-
*async*process_llm_request(***,*tool_context*,*llm_request*)[¶](#google.adk.tools.google_search_tool.GoogleSearchTool.process_llm_request) Processes the outgoing LLM request for this tool.

Use cases: - Most common use case is adding this tool to the LLM request. - Some tools may just preprocess the LLM request before it’s sent out.

- Return type:
`None`

- Parameters:
**tool_context**– The context of the tool.**llm_request**– The outgoing LLM request, mutable this method.


# google.adk.tools.langchain_tool module[¶](#google-adk-tools-langchain-tool-module)

# google.adk.tools.load_artifacts_tool module[¶](#module-google.adk.tools.load_artifacts_tool)

-
*class*google.adk.tools.load_artifacts_tool.LoadArtifactsTool[¶](#google.adk.tools.load_artifacts_tool.LoadArtifactsTool) Bases:

`BaseTool`

A tool that loads the artifacts and adds them to the session.

-
*async*process_llm_request(***,*tool_context*,*llm_request*)[¶](#google.adk.tools.load_artifacts_tool.LoadArtifactsTool.process_llm_request) Processes the outgoing LLM request for this tool.

Use cases: - Most common use case is adding this tool to the LLM request. - Some tools may just preprocess the LLM request before it’s sent out.

- Return type:
`None`

- Parameters:
**tool_context**– The context of the tool.**llm_request**– The outgoing LLM request, mutable this method.


-
*async*run_async(***,*args*,*tool_context*)[¶](#google.adk.tools.load_artifacts_tool.LoadArtifactsTool.run_async) Runs the tool with the given arguments and context.

- Return type:
`Any`


Note

Required if this tool needs to run at the client side.

Otherwise, can be skipped, e.g. for a built-in GoogleSearch tool for Gemini.


- Parameters:
**args**– The LLM-filled arguments.**tool_context**– The context of the tool.

- Returns:
The result of running the tool.


-

# google.adk.tools.load_memory_tool module[¶](#module-google.adk.tools.load_memory_tool)

-
*pydantic model*google.adk.tools.load_memory_tool.LoadMemoryResponse[¶](#google.adk.tools.load_memory_tool.LoadMemoryResponse) Bases:

`BaseModel`

## Show JSON schema

{ "title": "LoadMemoryResponse", "type": "object", "properties": { "memories": { "items": { "$ref": "#/$defs/MemoryEntry" }, "title": "Memories", "type": "array" } }, "$defs": { "Blob": { "additionalProperties": false, "description": "Content blob.", "properties": { "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Raw bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob. Used to provide a label or filename to distinguish blobs. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "Blob", "type": "object" }, "CodeExecutionResult": { "additionalProperties": false, "description": "Result of executing the [ExecutableCode].\n\nOnly generated when using the [CodeExecution] tool, and always follows a\n`part` containing the [ExecutableCode].", "properties": { "outcome": { "anyOf": [ { "$ref": "#/$defs/Outcome" }, { "type": "null" } ], "default": null, "description": "Required. Outcome of the code execution." }, "output": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Contains stdout when code execution is successful, stderr or other description otherwise.", "title": "Output" } }, "title": "CodeExecutionResult", "type": "object" }, "Content": { "additionalProperties": false, "description": "Contains the multi-part content of a message.", "properties": { "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/Part" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a single message. Each part may have\n a different IANA MIME type.", "title": "Parts" }, "role": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The producer of the content. Must be either 'user' or 'model'. Useful to set for multi-turn conversations, otherwise can be left blank or unset.", "title": "Role" } }, "title": "Content", "type": "object" }, "ExecutableCode": { "additionalProperties": false, "description": "Code generated by the model that is meant to be executed, and the result returned to the model.\n\nGenerated when using the [CodeExecution] tool, in which the code will be\nautomatically executed, and a corresponding [CodeExecutionResult] will also be\ngenerated.", "properties": { "code": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The code to be executed.", "title": "Code" }, "language": { "anyOf": [ { "$ref": "#/$defs/Language" }, { "type": "null" } ], "default": null, "description": "Required. Programming language of the `code`." } }, "title": "ExecutableCode", "type": "object" }, "FileData": { "additionalProperties": false, "description": "URI based data.", "properties": { "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file data. Used to provide a label or filename to distinguish file datas. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. This field is not supported in Gemini API.", "title": "Displayname" }, "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" } }, "title": "FileData", "type": "object" }, "FunctionCall": { "additionalProperties": false, "description": "A function call.", "properties": { "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "The unique id of the function call. If populated, the client to execute the\n `function_call` and return the response with the matching `id`.", "title": "Id" }, "args": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Optional. The function parameters and values in JSON object format. See [FunctionDeclaration.parameters] for parameter details.", "title": "Args" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The name of the function to call. Matches [FunctionDeclaration.name].", "title": "Name" }, "partialArgs": { "anyOf": [ { "items": { "$ref": "#/$defs/PartialArg" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "Optional. The partial argument value of the function call. If provided, represents the arguments/fields that are streamed incrementally. This field is not supported in Gemini API.", "title": "Partialargs" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is the last part of the FunctionCall. If true, another partial message for the current FunctionCall is expected to follow. This field is not supported in Gemini API.", "title": "Willcontinue" } }, "title": "FunctionCall", "type": "object" }, "FunctionResponse": { "additionalProperties": false, "description": "A function response.", "properties": { "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Signals that function call continues, and more responses will be returned, turning the function call into a generator. Is only applicable to NON_BLOCKING function calls (see FunctionDeclaration.behavior for details), ignored otherwise. If false, the default, future responses will not be considered. Is only applicable to NON_BLOCKING function calls, is ignored otherwise. If set to false, future responses will not be considered. It is allowed to return empty `response` with `will_continue=False` to signal that the function call is finished.", "title": "Willcontinue" }, "scheduling": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseScheduling" }, { "type": "null" } ], "default": null, "description": "Specifies how the response should be scheduled in the conversation. Only applicable to NON_BLOCKING function calls, is ignored otherwise. Defaults to WHEN_IDLE." }, "parts": { "anyOf": [ { "items": { "$ref": "#/$defs/FunctionResponsePart" }, "type": "array" }, { "type": "null" } ], "default": null, "description": "List of parts that constitute a function response. Each part may\n have a different IANA MIME type.", "title": "Parts" }, "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The id of the function call this response is for. Populated by the client to match the corresponding function call `id`.", "title": "Id" }, "name": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The name of the function to call. Matches [FunctionDeclaration.name] and [FunctionCall.name].", "title": "Name" }, "response": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "description": "Required. The function response in JSON object format. Use \"output\" key to specify function output and \"error\" key to specify error details (if any). If \"output\" and \"error\" keys are not specified, then whole \"response\" is treated as function output.", "title": "Response" } }, "title": "FunctionResponse", "type": "object" }, "FunctionResponseBlob": { "additionalProperties": false, "description": "Raw media bytes for function response.\n\nText should not be sent as raw bytes, use the FunctionResponse.response\nfield.", "properties": { "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "data": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. Inline media bytes.", "title": "Data" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the blob.\n Used to provide a label or filename to distinguish blobs.", "title": "Displayname" } }, "title": "FunctionResponseBlob", "type": "object" }, "FunctionResponseFileData": { "additionalProperties": false, "description": "URI based data for function response.", "properties": { "fileUri": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. URI.", "title": "Fileuri" }, "mimeType": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. The IANA standard MIME type of the source data.", "title": "Mimetype" }, "displayName": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Display name of the file.\n Used to provide a label or filename to distinguish files.", "title": "Displayname" } }, "title": "FunctionResponseFileData", "type": "object" }, "FunctionResponsePart": { "additionalProperties": false, "description": "A datatype containing media that is part of a `FunctionResponse` message.\n\nA `FunctionResponsePart` consists of data which has an associated datatype. A\n`FunctionResponsePart` can only contain one of the accepted types in\n`FunctionResponsePart.data`.\n\nA `FunctionResponsePart` must have a fixed IANA MIME type identifying the\ntype and subtype of the media if the `inline_data` field is filled with raw\nbytes.", "properties": { "inlineData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseBlob" }, { "type": "null" } ], "default": null, "description": "Optional. Inline media bytes." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FunctionResponseFileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." } }, "title": "FunctionResponsePart", "type": "object" }, "FunctionResponseScheduling": { "description": "Specifies how the response should be scheduled in the conversation.", "enum": [ "SCHEDULING_UNSPECIFIED", "SILENT", "WHEN_IDLE", "INTERRUPT" ], "title": "FunctionResponseScheduling", "type": "string" }, "Language": { "description": "Programming language of the `code`.", "enum": [ "LANGUAGE_UNSPECIFIED", "PYTHON" ], "title": "Language", "type": "string" }, "MemoryEntry": { "description": "Represent one memory entry.", "properties": { "content": { "$ref": "#/$defs/Content" }, "custom_metadata": { "additionalProperties": true, "title": "Custom Metadata", "type": "object" }, "id": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Id" }, "author": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Author" }, "timestamp": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "title": "Timestamp" } }, "required": [ "content" ], "title": "MemoryEntry", "type": "object" }, "Outcome": { "description": "Outcome of the code execution.", "enum": [ "OUTCOME_UNSPECIFIED", "OUTCOME_OK", "OUTCOME_FAILED", "OUTCOME_DEADLINE_EXCEEDED" ], "title": "Outcome", "type": "string" }, "Part": { "additionalProperties": false, "description": "A datatype containing media content.\n\nExactly one field within a Part should be set, representing the specific type\nof content being conveyed. Using multiple fields within the same `Part`\ninstance is considered invalid.", "properties": { "mediaResolution": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolution" }, { "type": "null" } ], "default": null, "description": "Media resolution for the input media.\n " }, "codeExecutionResult": { "anyOf": [ { "$ref": "#/$defs/CodeExecutionResult" }, { "type": "null" } ], "default": null, "description": "Optional. Result of executing the [ExecutableCode]." }, "executableCode": { "anyOf": [ { "$ref": "#/$defs/ExecutableCode" }, { "type": "null" } ], "default": null, "description": "Optional. Code generated by the model that is meant to be executed." }, "fileData": { "anyOf": [ { "$ref": "#/$defs/FileData" }, { "type": "null" } ], "default": null, "description": "Optional. URI based data." }, "functionCall": { "anyOf": [ { "$ref": "#/$defs/FunctionCall" }, { "type": "null" } ], "default": null, "description": "Optional. A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] with the parameters and their values." }, "functionResponse": { "anyOf": [ { "$ref": "#/$defs/FunctionResponse" }, { "type": "null" } ], "default": null, "description": "Optional. The result output of a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function call. It is used as context to the model." }, "inlineData": { "anyOf": [ { "$ref": "#/$defs/Blob" }, { "type": "null" } ], "default": null, "description": "Optional. Inlined bytes data." }, "text": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Text part (can be code).", "title": "Text" }, "thought": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Indicates if the part is thought from the model.", "title": "Thought" }, "thoughtSignature": { "anyOf": [ { "format": "base64url", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. An opaque signature for the thought so it can be reused in subsequent requests.", "title": "Thoughtsignature" }, "videoMetadata": { "anyOf": [ { "$ref": "#/$defs/VideoMetadata" }, { "type": "null" } ], "default": null, "description": "Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data." } }, "title": "Part", "type": "object" }, "PartMediaResolution": { "additionalProperties": false, "description": "Media resolution for the input media.", "properties": { "level": { "anyOf": [ { "$ref": "#/$defs/PartMediaResolutionLevel" }, { "type": "null" } ], "default": null, "description": "The tokenization quality used for given media.\n " }, "numTokens": { "anyOf": [ { "type": "integer" }, { "type": "null" } ], "default": null, "description": "Specifies the required sequence length for media tokenization.\n ", "title": "Numtokens" } }, "title": "PartMediaResolution", "type": "object" }, "PartMediaResolutionLevel": { "description": "The tokenization quality used for given media.", "enum": [ "MEDIA_RESOLUTION_UNSPECIFIED", "MEDIA_RESOLUTION_LOW", "MEDIA_RESOLUTION_MEDIUM", "MEDIA_RESOLUTION_HIGH", "MEDIA_RESOLUTION_ULTRA_HIGH" ], "title": "PartMediaResolutionLevel", "type": "string" }, "PartialArg": { "additionalProperties": false, "description": "Partial argument value of the function call.\n\nThis data type is not supported in Gemini API.", "properties": { "nullValue": { "anyOf": [ { "const": "NULL_VALUE", "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a null value.", "title": "Nullvalue" }, "numberValue": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a double value.", "title": "Numbervalue" }, "stringValue": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a string value.", "title": "Stringvalue" }, "boolValue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Represents a boolean value.", "title": "Boolvalue" }, "jsonPath": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Required. A JSON Path (RFC 9535) to the argument being streamed. https://datatracker.ietf.org/doc/html/rfc9535. e.g. \"$.foo.bar[0].data\".", "title": "Jsonpath" }, "willContinue": { "anyOf": [ { "type": "boolean" }, { "type": "null" } ], "default": null, "description": "Optional. Whether this is not the last part of the same json_path. If true, another PartialArg message for the current json_path is expected to follow.", "title": "Willcontinue" } }, "title": "PartialArg", "type": "object" }, "VideoMetadata": { "additionalProperties": false, "description": "Metadata describes the input video content.", "properties": { "endOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The end offset of the video.", "title": "Endoffset" }, "fps": { "anyOf": [ { "type": "number" }, { "type": "null" } ], "default": null, "description": "Optional. The frame rate of the video sent to the model. If not specified, the default value will be 1.0. The fps range is (0.0, 24.0].", "title": "Fps" }, "startOffset": { "anyOf": [ { "type": "string" }, { "type": "null" } ], "default": null, "description": "Optional. The start offset of the video.", "title": "Startoffset" } }, "title": "VideoMetadata", "type": "object" } } }

-
*field*memories*: list[MemoryEntry]**[Optional]*[¶](#google.adk.tools.load_memory_tool.LoadMemoryResponse.memories)

-

-
*class*google.adk.tools.load_memory_tool.LoadMemoryTool[¶](#google.adk.tools.load_memory_tool.LoadMemoryTool) Bases:

`FunctionTool`

A tool that loads the memory for the current user.

NOTE: Currently this tool only uses text part from the memory.

Initializes the FunctionTool. Extracts metadata from a callable object.

- Parameters:
**func**– The function to wrap.**require_confirmation**– Whether this tool requires confirmation. A boolean or a callable that takes the function’s arguments and returns a boolean. If the callable returns True, the tool will require confirmation from the user.


-
*async*process_llm_request(***,*tool_context*,*llm_request*)[¶](#google.adk.tools.load_memory_tool.LoadMemoryTool.process_llm_request) Processes the outgoing LLM request for this tool.

Use cases: - Most common use case is adding this tool to the LLM request. - Some tools may just preprocess the LLM request before it’s sent out.

- Return type:
`None`

- Parameters:
**tool_context**– The context of the tool.**llm_request**– The outgoing LLM request, mutable this method.


-
*async*google.adk.tools.load_memory_tool.load_memory(*query*,*tool_context*)[¶](#google.adk.tools.load_memory_tool.load_memory) Loads the memory for the current user.

- Return type:
- Parameters:
**query**– The query to load the memory for.- Returns:
A list of memory results.


# google.adk.tools.load_web_page module[¶](#module-google.adk.tools.load_web_page)

Tool for web browse.

-
google.adk.tools.load_web_page.load_web_page(
*url*)[¶](#google.adk.tools.load_web_page.load_web_page) Fetches the content in the url and returns the text in it.

- Return type:
`str`

- Parameters:
**url**(*str*) – The url to browse.- Returns:
The text content of the url.

- Return type:
str


# google.adk.tools.long_running_tool module[¶](#module-google.adk.tools.long_running_tool)

-
*class*google.adk.tools.long_running_tool.LongRunningFunctionTool(*func*)[¶](#google.adk.tools.long_running_tool.LongRunningFunctionTool) Bases:

`FunctionTool`

A function tool that returns the result asynchronously.

This tool is used for long-running operations that may take a significant amount of time to complete. The framework will call the function. Once the function returns, the response will be returned asynchronously to the framework which is identified by the function_call_id.

Example:

``python tool = LongRunningFunctionTool(a_long_running_function) ``

-
is_long_running
[¶](#google.adk.tools.long_running_tool.LongRunningFunctionTool.is_long_running) Whether the tool is a long running operation.


Initializes the FunctionTool. Extracts metadata from a callable object.

- Parameters:
**func**– The function to wrap.**require_confirmation**– Whether this tool requires confirmation. A boolean or a callable that takes the function’s arguments and returns a boolean. If the callable returns True, the tool will require confirmation from the user.


-
is_long_running

# google.adk.tools.mcp_tool module[¶](#module-google.adk.tools.mcp_tool)

-
*class*google.adk.tools.mcp_tool.MCPTool(**args*,***kwargs*)[¶](#google.adk.tools.mcp_tool.MCPTool) Bases:

`McpTool`

Deprecated name, use McpTool instead.

Initializes an McpTool.

This tool wraps an MCP Tool interface and uses a session manager to communicate with the MCP server.

- Parameters:
**mcp_tool**– The MCP tool to wrap.**mcp_session_manager**– The MCP session manager to use for communication.**auth_scheme**– The authentication scheme to use.**auth_credential**– The authentication credential to use.**require_confirmation**– Whether this tool requires confirmation. A boolean or a callable that takes the function’s arguments and returns a boolean. If the callable returns True, the tool will require confirmation from the user.

- Raises:
**ValueError**– If mcp_tool or mcp_session_manager is None.


-
*class*google.adk.tools.mcp_tool.MCPToolset(**args*,***kwargs*)[¶](#google.adk.tools.mcp_tool.MCPToolset) Bases:

`McpToolset`

Deprecated name, use McpToolset instead.

Initializes the McpToolset.

- Parameters:
**connection_params**– The connection parameters to the MCP server. Can be:`StdioConnectionParams`

for using local mcp server (e.g. using`npx`

or`python3`

); or`SseConnectionParams`

for a local/remote SSE server; or`StreamableHTTPConnectionParams`

for local/remote Streamable http server. Note,`StdioServerParameters`

is also supported for using local mcp server (e.g. using`npx`

or`python3`

), but it does not support timeout, and we recommend to use`StdioConnectionParams`

instead when timeout is needed.**tool_filter**– Optional filter to select specific tools. Can be either: - A list of tool names to include - A ToolPredicate function for custom filtering logic**tool_name_prefix**– A prefix to be added to the name of each tool in this toolset.**errlog**– TextIO stream for error logging.**auth_scheme**– The auth scheme of the tool for tool calling**auth_credential**– The auth credential of the tool for tool calling**require_confirmation**– Whether tools in this toolset require confirmation. Can be a single boolean or a callable to apply to all tools.**header_provider**– A callable that takes a ReadonlyContext and returns a dictionary of headers to be used for the MCP session.


-
*class*google.adk.tools.mcp_tool.McpTool(***,*mcp_tool*,*mcp_session_manager*,*auth_scheme=None*,*auth_credential=None*,*require_confirmation=False*,*header_provider=None*)[¶](#google.adk.tools.mcp_tool.McpTool) Bases:

`BaseAuthenticatedTool`

Turns an MCP Tool into an ADK Tool.

Internally, the tool initializes from a MCP Tool, and uses the MCP Session to call the tool.

Note: For API key authentication, only header-based API keys are supported. Query and cookie-based API keys will result in authentication errors.

Initializes an McpTool.

This tool wraps an MCP Tool interface and uses a session manager to communicate with the MCP server.

- Parameters:
**mcp_tool**– The MCP tool to wrap.**mcp_session_manager**– The MCP session manager to use for communication.**auth_scheme**– The authentication scheme to use.**auth_credential**– The authentication credential to use.**require_confirmation**– Whether this tool requires confirmation. A boolean or a callable that takes the function’s arguments and returns a boolean. If the callable returns True, the tool will require confirmation from the user.

- Raises:
**ValueError**– If mcp_tool or mcp_session_manager is None.

-
*property*raw_mcp_tool*: Tool*[¶](#google.adk.tools.mcp_tool.McpTool.raw_mcp_tool) Returns the raw MCP tool.


-
*async*run_async(***,*args*,*tool_context*)[¶](#google.adk.tools.mcp_tool.McpTool.run_async) Runs the tool with the given arguments and context.

- Return type:
`Any`


Note

Required if this tool needs to run at the client side.

Otherwise, can be skipped, e.g. for a built-in GoogleSearch tool for Gemini.


- Parameters:
**args**– The LLM-filled arguments.**tool_context**– The context of the tool.

- Returns:
The result of running the tool.


-
*class*google.adk.tools.mcp_tool.McpToolset(***,*connection_params*,*tool_filter=None*,*tool_name_prefix=None*,*errlog=<_io.TextIOWrapper name='<stderr>' mode='w' encoding='utf-8'>*,*auth_scheme=None*,*auth_credential=None*,*require_confirmation=False*,*header_provider=None*)[¶](#google.adk.tools.mcp_tool.McpToolset) Bases:

`BaseToolset`

Connects to a MCP Server, and retrieves MCP Tools into ADK Tools.

This toolset manages the connection to an MCP server and provides tools that can be used by an agent. It properly implements the BaseToolset interface for easy integration with the agent framework.

Usage:

toolset = McpToolset( connection_params=StdioServerParameters( command='npx', args=["-y", "@modelcontextprotocol/server-filesystem"], ), tool_filter=['read_file', 'list_directory'] # Optional: filter specific tools ) # Use in an agent agent = LlmAgent( model='gemini-2.0-flash', name='enterprise_assistant', instruction='Help user accessing their file systems', tools=[toolset], ) # Cleanup is handled automatically by the agent framework # But you can also manually close if needed: # await toolset.close()

Initializes the McpToolset.

- Parameters:
**connection_params**– The connection parameters to the MCP server. Can be:`StdioConnectionParams`

for using local mcp server (e.g. using`npx`

or`python3`

); or`SseConnectionParams`

for a local/remote SSE server; or`StreamableHTTPConnectionParams`

for local/remote Streamable http server. Note,`StdioServerParameters`

is also supported for using local mcp server (e.g. using`npx`

or`python3`

), but it does not support timeout, and we recommend to use`StdioConnectionParams`

instead when timeout is needed.**tool_filter**– Optional filter to select specific tools. Can be either: - A list of tool names to include - A ToolPredicate function for custom filtering logic**tool_name_prefix**– A prefix to be added to the name of each tool in this toolset.**errlog**– TextIO stream for error logging.**auth_scheme**– The auth scheme of the tool for tool calling**auth_credential**– The auth credential of the tool for tool calling**require_confirmation**– Whether tools in this toolset require confirmation. Can be a single boolean or a callable to apply to all tools.**header_provider**– A callable that takes a ReadonlyContext and returns a dictionary of headers to be used for the MCP session.


-
*async*close()[¶](#google.adk.tools.mcp_tool.McpToolset.close) Performs cleanup and releases resources held by the toolset.

This method closes the MCP session and cleans up all associated resources. It’s designed to be safe to call multiple times and handles cleanup errors gracefully to avoid blocking application shutdown.

- Return type:
`None`


-
*classmethod*from_config(*config*,*config_abs_path*)[¶](#google.adk.tools.mcp_tool.McpToolset.from_config) Creates an McpToolset from a configuration object.

- Return type:


-
*async*get_tools(*readonly_context=None*)[¶](#google.adk.tools.mcp_tool.McpToolset.get_tools) Return all tools in the toolset based on the provided context.


-
*pydantic model*google.adk.tools.mcp_tool.SseConnectionParams[¶](#google.adk.tools.mcp_tool.SseConnectionParams) Bases:

`BaseModel`

Parameters for the MCP SSE connection.

See MCP SSE Client documentation for more details.

[https://github.com/modelcontextprotocol/python-sdk/blob/main/src/mcp/client/sse.py](https://github.com/modelcontextprotocol/python-sdk/blob/main/src/mcp/client/sse.py)-
url
[¶](#google.adk.tools.mcp_tool.SseConnectionParams.url) URL for the MCP SSE server.


-
headers
[¶](#google.adk.tools.mcp_tool.SseConnectionParams.headers) Headers for the MCP SSE connection.


-
timeout
[¶](#google.adk.tools.mcp_tool.SseConnectionParams.timeout) Timeout in seconds for establishing the connection to the MCP SSE server.


-
sse_read_timeout
[¶](#google.adk.tools.mcp_tool.SseConnectionParams.sse_read_timeout) Timeout in seconds for reading data from the MCP SSE server.


## Show JSON schema

{ "title": "SseConnectionParams", "description": "Parameters for the MCP SSE connection.\n\nSee MCP SSE Client documentation for more details.\nhttps://github.com/modelcontextprotocol/python-sdk/blob/main/src/mcp/client/sse.py\n\nAttributes:\n url: URL for the MCP SSE server.\n headers: Headers for the MCP SSE connection.\n timeout: Timeout in seconds for establishing the connection to the MCP SSE\n server.\n sse_read_timeout: Timeout in seconds for reading data from the MCP SSE\n server.", "type": "object", "properties": { "url": { "title": "Url", "type": "string" }, "headers": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "title": "Headers" }, "timeout": { "default": 5.0, "title": "Timeout", "type": "number" }, "sse_read_timeout": { "default": 300.0, "title": "Sse Read Timeout", "type": "number" } }, "required": [ "url" ] }

- Fields:
`headers (dict[str, Any] | None)`

`sse_read_timeout (float)`

`timeout (float)`

`url (str)`


-
*field*headers*: dict[str, Any] | None**= None*[¶](#id55)

-
*field*sse_read_timeout*: float**= 300.0*[¶](#id56)

-
*field*timeout*: float**= 5.0*[¶](#id57)

-
*field*url*: str**[Required]*[¶](#id58)

-
url

-
*pydantic model*google.adk.tools.mcp_tool.StdioConnectionParams[¶](#google.adk.tools.mcp_tool.StdioConnectionParams) Bases:

`BaseModel`

Parameters for the MCP Stdio connection.

-
server_params
[¶](#google.adk.tools.mcp_tool.StdioConnectionParams.server_params) Parameters for the MCP Stdio server.


-
timeout
[¶](#google.adk.tools.mcp_tool.StdioConnectionParams.timeout) Timeout in seconds for establishing the connection to the MCP stdio server.


## Show JSON schema

{ "title": "StdioConnectionParams", "description": "Parameters for the MCP Stdio connection.\n\nAttributes:\n server_params: Parameters for the MCP Stdio server.\n timeout: Timeout in seconds for establishing the connection to the MCP\n stdio server.", "type": "object", "properties": { "server_params": { "$ref": "#/$defs/StdioServerParameters" }, "timeout": { "default": 5.0, "title": "Timeout", "type": "number" } }, "$defs": { "StdioServerParameters": { "properties": { "command": { "title": "Command", "type": "string" }, "args": { "items": { "type": "string" }, "title": "Args", "type": "array" }, "env": { "anyOf": [ { "additionalProperties": { "type": "string" }, "type": "object" }, { "type": "null" } ], "default": null, "title": "Env" }, "cwd": { "anyOf": [ { "type": "string" }, { "format": "path", "type": "string" }, { "type": "null" } ], "default": null, "title": "Cwd" }, "encoding": { "default": "utf-8", "title": "Encoding", "type": "string" }, "encoding_error_handler": { "default": "strict", "enum": [ "strict", "ignore", "replace" ], "title": "Encoding Error Handler", "type": "string" } }, "required": [ "command" ], "title": "StdioServerParameters", "type": "object" } }, "required": [ "server_params" ] }

- Fields:
`server_params (mcp.client.stdio.StdioServerParameters)`

`timeout (float)`


-
*field*server_params*: StdioServerParameters**[Required]*[¶](#id59)

-
*field*timeout*: float**= 5.0*[¶](#id60)

-
server_params

-
*pydantic model*google.adk.tools.mcp_tool.StreamableHTTPConnectionParams[¶](#google.adk.tools.mcp_tool.StreamableHTTPConnectionParams) Bases:

`BaseModel`

Parameters for the MCP Streamable HTTP connection.

See MCP Streamable HTTP Client documentation for more details.

[https://github.com/modelcontextprotocol/python-sdk/blob/main/src/mcp/client/streamable_http.py](https://github.com/modelcontextprotocol/python-sdk/blob/main/src/mcp/client/streamable_http.py)-
url
[¶](#google.adk.tools.mcp_tool.StreamableHTTPConnectionParams.url) URL for the MCP Streamable HTTP server.


-
headers
[¶](#google.adk.tools.mcp_tool.StreamableHTTPConnectionParams.headers) Headers for the MCP Streamable HTTP connection.


-
timeout
[¶](#google.adk.tools.mcp_tool.StreamableHTTPConnectionParams.timeout) Timeout in seconds for establishing the connection to the MCP Streamable HTTP server.


-
sse_read_timeout
[¶](#google.adk.tools.mcp_tool.StreamableHTTPConnectionParams.sse_read_timeout) Timeout in seconds for reading data from the MCP Streamable HTTP server.


-
terminate_on_close
[¶](#google.adk.tools.mcp_tool.StreamableHTTPConnectionParams.terminate_on_close) Whether to terminate the MCP Streamable HTTP server when the connection is closed.


-
httpx_client_factory
[¶](#google.adk.tools.mcp_tool.StreamableHTTPConnectionParams.httpx_client_factory) Factory function to create a custom HTTPX client. If not provided, a default factory will be used.


## Show JSON schema

{ "title": "StreamableHTTPConnectionParams", "type": "object", "properties": { "url": { "title": "Url", "type": "string" }, "headers": { "anyOf": [ { "additionalProperties": true, "type": "object" }, { "type": "null" } ], "default": null, "title": "Headers" }, "timeout": { "default": 5.0, "title": "Timeout", "type": "number" }, "sse_read_timeout": { "default": 300.0, "title": "Sse Read Timeout", "type": "number" }, "terminate_on_close": { "default": true, "title": "Terminate On Close", "type": "boolean" }, "httpx_client_factory": { "default": null, "title": "Httpx Client Factory" } }, "required": [ "url" ] }

- Fields:
`headers (dict[str, Any] | None)`

`httpx_client_factory (google.adk.tools.mcp_tool.mcp_session_manager.CheckableMcpHttpClientFactory)`

`sse_read_timeout (float)`

`terminate_on_close (bool)`

`timeout (float)`

`url (str)`


-
*field*headers*: dict[str, Any] | None**= None*[¶](#id61)

-
*field*httpx_client_factory*: CheckableMcpHttpClientFactory**= <function create_mcp_http_client>*[¶](#id62)

-
*field*sse_read_timeout*: float**= 300.0*[¶](#id63)

-
*field*terminate_on_close*: bool**= True*[¶](#id64)

-
*field*timeout*: float**= 5.0*[¶](#id65)

-
*field*url*: str**[Required]*[¶](#id66)

-
url

-
google.adk.tools.mcp_tool.adk_to_mcp_tool_type(
*tool*)[¶](#google.adk.tools.mcp_tool.adk_to_mcp_tool_type) Convert a Tool in ADK into MCP tool type.

This function transforms an ADK tool definition into its equivalent representation in the MCP (Model Context Protocol) system.

- Return type:
`Tool`

- Parameters:
**tool**– The ADK tool to convert. It should be an instance of a class derived from BaseTool.- Returns:
An object of MCP Tool type, representing the converted tool.


Examples

# Assuming ‘my_tool’ is an instance of a BaseTool derived class mcp_tool = adk_to_mcp_tool_type(my_tool) print(mcp_tool)


-
google.adk.tools.mcp_tool.gemini_to_json_schema(
*gemini_schema*)[¶](#google.adk.tools.mcp_tool.gemini_to_json_schema) Converts a Gemini Schema object into a JSON Schema dictionary.

- Return type:
`Dict`

[`str`

,`Any`

]- Parameters:
**gemini_schema**– An instance of the Gemini Schema class.- Returns:
A dictionary representing the equivalent JSON Schema.

- Raises:
**TypeError**– If the input is not an instance of the expected Schema class.**ValueError**– If an invalid Gemini Type enum value is encountered.


# google.adk.tools.openapi_tool module[¶](#module-google.adk.tools.openapi_tool)

-
*class*google.adk.tools.openapi_tool.OpenAPIToolset(***,*spec_dict=None*,*spec_str=None*,*spec_str_type='json'*,*auth_scheme=None*,*auth_credential=None*,*tool_filter=None*,*tool_name_prefix=None*,*ssl_verify=None*,*header_provider=None*)[¶](#google.adk.tools.openapi_tool.OpenAPIToolset) Bases:

`BaseToolset`

Class for parsing OpenAPI spec into a list of RestApiTool.

Usage:

# Initialize OpenAPI toolset from a spec string. openapi_toolset = OpenAPIToolset(spec_str=openapi_spec_str, spec_str_type="json") # Or, initialize OpenAPI toolset from a spec dictionary. openapi_toolset = OpenAPIToolset(spec_dict=openapi_spec_dict) # Add all tools to an agent. agent = Agent( tools=[*openapi_toolset.get_tools()] ) # Or, add a single tool to an agent. agent = Agent( tools=[openapi_toolset.get_tool('tool_name')] )

Initializes the OpenAPIToolset.

Usage:

# Initialize OpenAPI toolset from a spec string. openapi_toolset = OpenAPIToolset(spec_str=openapi_spec_str, spec_str_type="json") # Or, initialize OpenAPI toolset from a spec dictionary. openapi_toolset = OpenAPIToolset(spec_dict=openapi_spec_dict) # Add all tools to an agent. agent = Agent( tools=[*openapi_toolset.get_tools()] ) # Or, add a single tool to an agent. agent = Agent( tools=[openapi_toolset.get_tool('tool_name')] )

- Parameters:
**spec_dict**– The OpenAPI spec dictionary. If provided, it will be used instead of loading the spec from a string.**spec_str**– The OpenAPI spec string in JSON or YAML format. It will be used when spec_dict is not provided.**spec_str_type**– The type of the OpenAPI spec string. Can be “json” or “yaml”.**auth_scheme**– The auth scheme to use for all tools. Use AuthScheme or use helpers in`google.adk.tools.openapi_tool.auth.auth_helpers`

**auth_credential**– The auth credential to use for all tools. Use AuthCredential or use helpers in`google.adk.tools.openapi_tool.auth.auth_helpers`

**tool_filter**– The filter used to filter the tools in the toolset. It can be either a tool predicate or a list of tool names of the tools to expose.**tool_name_prefix**– The prefix to prepend to the names of the tools returned by the toolset. Useful when multiple OpenAPI specs have tools with similar names.**ssl_verify**– SSL certificate verification option for all tools. Can be: - None: Use default verification (True) - True: Verify SSL certificates using system CA - False: Disable SSL verification (insecure, not recommended) - str: Path to a CA bundle file or directory for custom CA - ssl.SSLContext: Custom SSL context for advanced configuration This is useful for enterprise environments where requests go through a TLS-intercepting proxy with a custom CA certificate.**header_provider**– A callable that returns a dictionary of headers to be included in API requests. The callable receives the ReadonlyContext as an argument, allowing dynamic header generation based on the current context. Useful for adding custom headers like correlation IDs, authentication tokens, or other request metadata.


-
*async*close()[¶](#google.adk.tools.openapi_tool.OpenAPIToolset.close) Performs cleanup and releases resources held by the toolset.

Note

This method is invoked, for example, at the end of an agent server’s lifecycle or when the toolset is no longer needed. Implementations should ensure that any open connections, files, or other managed resources are properly released to prevent leaks.


-
configure_ssl_verify_all(
*ssl_verify=None*)[¶](#google.adk.tools.openapi_tool.OpenAPIToolset.configure_ssl_verify_all) Configure SSL certificate verification for all tools.

This is useful for enterprise environments where requests go through a TLS-intercepting proxy with a custom CA certificate.

- Parameters:
**ssl_verify**– SSL certificate verification option. Can be: - None: Use default verification (True) - True: Verify SSL certificates using system CA - False: Disable SSL verification (insecure, not recommended) - str: Path to a CA bundle file or directory for custom CA - ssl.SSLContext: Custom SSL context for advanced configuration


-
get_tool(
*tool_name*)[¶](#google.adk.tools.openapi_tool.OpenAPIToolset.get_tool) Get a tool by name.

- Return type:
`Optional`

[]`RestApiTool`


-
*async*get_tools(*readonly_context=None*)[¶](#google.adk.tools.openapi_tool.OpenAPIToolset.get_tools) Get all tools in the toolset.

- Return type:
`List`

[]`RestApiTool`


-
*class*google.adk.tools.openapi_tool.RestApiTool(*name*,*description*,*endpoint*,*operation*,*auth_scheme=None*,*auth_credential=None*,*should_parse_operation=True*,*ssl_verify=None*,*header_provider=None*)[¶](#google.adk.tools.openapi_tool.RestApiTool) Bases:

`BaseTool`

A generic tool that interacts with a REST API.

Generates request params and body

Attaches auth credentials to API call.


Example:

# Each API operation in the spec will be turned into its own tool # Name of the tool is the operationId of that operation, in snake case operations = OperationGenerator().parse(openapi_spec_dict) tool = [RestApiTool.from_parsed_operation(o) for o in operations]

Initializes the RestApiTool with the given parameters.

To generate RestApiTool from OpenAPI Specs, use OperationGenerator. Example:

# Each API operation in the spec will be turned into its own tool # Name of the tool is the operationId of that operation, in snake case operations = OperationGenerator().parse(openapi_spec_dict) tool = [RestApiTool.from_parsed_operation(o) for o in operations]

Hint: Use google.adk.tools.openapi_tool.auth.auth_helpers to construct auth_scheme and auth_credential.

- Parameters:
**name**– The name of the tool.**description**– The description of the tool.**endpoint**– Include the base_url, path, and method of the tool.**operation**– Pydantic object or a dict. Representing the OpenAPI Operation object ([https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operation-object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#operation-object))**auth_scheme**– The auth scheme of the tool. Representing the OpenAPI SecurityScheme object ([https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#security-scheme-object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#security-scheme-object))**auth_credential**– The authentication credential of the tool.**should_parse_operation**– Whether to parse the operation.**ssl_verify**– SSL certificate verification option. Can be: - None: Use default verification - True: Verify SSL certificates using system CA - False: Disable SSL verification (insecure, not recommended) - str: Path to a CA bundle file or directory for custom CA - ssl.SSLContext: Custom SSL context for advanced configuration**header_provider**– A callable that returns a dictionary of headers to be included in API requests. The callable receives the ReadonlyContext as an argument, allowing dynamic header generation based on the current context. Useful for adding custom headers like correlation IDs, authentication tokens, or other request metadata.


-
*async*call(***,*args*,*tool_context*)[¶](#google.adk.tools.openapi_tool.RestApiTool.call) Executes the REST API call.

- Return type:
`Dict`

[`str`

,`Any`

]- Parameters:
**args**– Keyword arguments representing the operation parameters.**tool_context**– The tool context (not used here, but required by the interface).

- Returns:
The API response as a dictionary.


-
configure_auth_credential(
*auth_credential=None*)[¶](#google.adk.tools.openapi_tool.RestApiTool.configure_auth_credential) Configures the authentication credential for the API call.

- Parameters:
**auth_credential**– AuthCredential|dict - The authentication credential. The dict is converted to an AuthCredential object.


-
configure_auth_scheme(
*auth_scheme*)[¶](#google.adk.tools.openapi_tool.RestApiTool.configure_auth_scheme) Configures the authentication scheme for the API call.

- Parameters:
**auth_scheme**– AuthScheme|dict -: The authentication scheme. The dict is converted to a AuthScheme object.


-
configure_ssl_verify(
*ssl_verify=None*)[¶](#google.adk.tools.openapi_tool.RestApiTool.configure_ssl_verify) Configures SSL certificate verification for the API call.

This is useful for enterprise environments where requests go through a TLS-intercepting proxy with a custom CA certificate.

- Parameters:
**ssl_verify**– SSL certificate verification option. Can be: - None: Use default verification (True) - True: Verify SSL certificates using system CA - False: Disable SSL verification (insecure, not recommended) - str: Path to a CA bundle file or directory for custom CA - ssl.SSLContext: Custom SSL context for advanced configuration


-
*classmethod*from_parsed_operation(*parsed*,*ssl_verify=None*,*header_provider=None*)[¶](#google.adk.tools.openapi_tool.RestApiTool.from_parsed_operation) Initializes the RestApiTool from a ParsedOperation object.

- Return type:
- Parameters:
**parsed**– A ParsedOperation object.**ssl_verify**– SSL certificate verification option.**header_provider**– A callable that returns a dictionary of headers to be included in API requests. The callable receives the ReadonlyContext as an argument, allowing dynamic header generation based on the current context. Useful for adding custom headers like correlation IDs, authentication tokens, or other request metadata.

- Returns:
A RestApiTool object.


-
*classmethod*from_parsed_operation_str(*parsed_operation_str*)[¶](#google.adk.tools.openapi_tool.RestApiTool.from_parsed_operation_str) Initializes the RestApiTool from a dict.

- Return type:
- Parameters:
**parsed**– A dict representation of a ParsedOperation object.- Returns:
A RestApiTool object.


-
*async*run_async(***,*args*,*tool_context*)[¶](#google.adk.tools.openapi_tool.RestApiTool.run_async) Runs the tool with the given arguments and context.

- Return type:
`Dict`

[`str`

,`Any`

]

Note

Required if this tool needs to run at the client side.

Otherwise, can be skipped, e.g. for a built-in GoogleSearch tool for Gemini.


- Parameters:
**args**– The LLM-filled arguments.**tool_context**– The context of the tool.

- Returns:
The result of running the tool.


-
set_default_headers(
*headers*)[¶](#google.adk.tools.openapi_tool.RestApiTool.set_default_headers) Sets default headers that are merged into every request.


# google.adk.tools.preload_memory_tool module[¶](#module-google.adk.tools.preload_memory_tool)

-
*class*google.adk.tools.preload_memory_tool.PreloadMemoryTool[¶](#google.adk.tools.preload_memory_tool.PreloadMemoryTool) Bases:

`BaseTool`

A tool that preloads the memory for the current user.

This tool will be automatically executed for each llm_request, and it won’t be called by the model.

NOTE: Currently this tool only uses text part from the memory.

-
*async*process_llm_request(***,*tool_context*,*llm_request*)[¶](#google.adk.tools.preload_memory_tool.PreloadMemoryTool.process_llm_request) Processes the outgoing LLM request for this tool.

Use cases: - Most common use case is adding this tool to the LLM request. - Some tools may just preprocess the LLM request before it’s sent out.

- Return type:
`None`

- Parameters:
**tool_context**– The context of the tool.**llm_request**– The outgoing LLM request, mutable this method.


-

# google.adk.tools.retrieval module[¶](#module-google.adk.tools.retrieval)

# google.adk.tools.tool_context module[¶](#module-google.adk.tools.tool_context)

-
*class*google.adk.tools.tool_context.ToolContext(*invocation_context*,***,*function_call_id=None*,*event_actions=None*,*tool_confirmation=None*)[¶](#google.adk.tools.tool_context.ToolContext) Bases:

`CallbackContext`

The context of the tool.

This class provides the context for a tool invocation, including access to the invocation context, function call ID, event actions, and authentication response. It also provides methods for requesting credentials, retrieving authentication responses, listing artifacts, and searching memory.

-
invocation_context
[¶](#google.adk.tools.tool_context.ToolContext.invocation_context) The invocation context of the tool.


-
function_call_id
[¶](#google.adk.tools.tool_context.ToolContext.function_call_id) The function call id of the current tool call. This id was returned in the function call event from LLM to identify a function call. If LLM didn’t return this id, ADK will assign one to it. This id is used to map function call response to the original function call.


-
event_actions
[¶](#google.adk.tools.tool_context.ToolContext.event_actions) The event actions of the current tool call.


-
tool_confirmation
[¶](#google.adk.tools.tool_context.ToolContext.tool_confirmation) The tool confirmation of the current tool call.


-
*property*actions*:*[EventActions](#google.adk.events.EventActions)[¶](#google.adk.tools.tool_context.ToolContext.actions)

-
get_auth_response(
*auth_config*)[¶](#google.adk.tools.tool_context.ToolContext.get_auth_response) - Return type:
`AuthCredential`


-
request_confirmation(
***,*hint=None*,*payload=None*)[¶](#google.adk.tools.tool_context.ToolContext.request_confirmation) Requests confirmation for the given function call.

- Return type:
`None`

- Parameters:
**hint**– A hint to the user on how to confirm the tool call.**payload**– The payload used to confirm the tool call.


-
request_credential(
*auth_config*)[¶](#google.adk.tools.tool_context.ToolContext.request_credential) - Return type:
`None`


-
*async*search_memory(*query*)[¶](#google.adk.tools.tool_context.ToolContext.search_memory) Searches the memory of the current user.

- Return type:
`SearchMemoryResponse`


-
invocation_context

# google.adk.tools.toolbox_toolset module[¶](#google-adk-tools-toolbox-toolset-module)

# google.adk.tools.transfer_to_agent_tool module[¶](#module-google.adk.tools.transfer_to_agent_tool)

-
*class*google.adk.tools.transfer_to_agent_tool.TransferToAgentTool(*agent_names*)[¶](#google.adk.tools.transfer_to_agent_tool.TransferToAgentTool) Bases:

`FunctionTool`

A specialized FunctionTool for agent transfer with enum constraints.

This tool enhances the base transfer_to_agent function by adding JSON Schema enum constraints to the agent_name parameter. This prevents LLMs from hallucinating invalid agent names by restricting choices to only valid agents.

-
agent_names
[¶](#google.adk.tools.transfer_to_agent_tool.TransferToAgentTool.agent_names) List of valid agent names that can be transferred to.


Initialize the TransferToAgentTool.

- Parameters:
**agent_names**– List of valid agent names that can be transferred to.

-
agent_names

-
google.adk.tools.transfer_to_agent_tool.transfer_to_agent(
*agent_name*,*tool_context*)[¶](#google.adk.tools.transfer_to_agent_tool.transfer_to_agent) Transfer the question to another agent.

This tool hands off control to another agent when it’s more suitable to answer the user’s question according to the agent’s description.

- Return type:
`None`


Note

For most use cases, you should use TransferToAgentTool instead of this function directly. TransferToAgentTool provides additional enum constraints that prevent LLMs from hallucinating invalid agent names.

- Parameters:
**agent_name**– the agent name to transfer to.


# google.adk.tools.url_context_tool module[¶](#module-google.adk.tools.url_context_tool)

-
*class*google.adk.tools.url_context_tool.UrlContextTool[¶](#google.adk.tools.url_context_tool.UrlContextTool) Bases:

`BaseTool`

A built-in tool that is automatically invoked by Gemini 2 models to retrieve content from the URLs and use that content to inform and shape its response.

This tool operates internally within the model and does not require or perform local code execution.

-
*async*process_llm_request(***,*tool_context*,*llm_request*)[¶](#google.adk.tools.url_context_tool.UrlContextTool.process_llm_request) Processes the outgoing LLM request for this tool.

Use cases: - Most common use case is adding this tool to the LLM request. - Some tools may just preprocess the LLM request before it’s sent out.

- Return type:
`None`

- Parameters:
**tool_context**– The context of the tool.**llm_request**– The outgoing LLM request, mutable this method.


-

# google.adk.tools.vertex_ai_search_tool module[¶](#module-google.adk.tools.vertex_ai_search_tool)

-
*class*google.adk.tools.vertex_ai_search_tool.VertexAiSearchTool(***,*data_store_id=None*,*data_store_specs=None*,*search_engine_id=None*,*filter=None*,*max_results=None*,*bypass_multi_tools_limit=False*)[¶](#google.adk.tools.vertex_ai_search_tool.VertexAiSearchTool) Bases:

`BaseTool`

A built-in tool using Vertex AI Search.

-
data_store_id
[¶](#google.adk.tools.vertex_ai_search_tool.VertexAiSearchTool.data_store_id) The Vertex AI search data store resource ID.


-
search_engine_id
[¶](#google.adk.tools.vertex_ai_search_tool.VertexAiSearchTool.search_engine_id) The Vertex AI search engine resource ID.


Initializes the Vertex AI Search tool.

- Parameters:
**data_store_id**– The Vertex AI search data store resource ID in the format of “projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}”.**data_store_specs**– Specifications that define the specific DataStores to be searched. It should only be set if engine is used.**search_engine_id**– The Vertex AI search engine resource ID in the format of “projects/{project}/locations/{location}/collections/{collection}/engines/{engine}”.**filter**– The filter to apply to the search results.**max_results**– The maximum number of results to return.**bypass_multi_tools_limit**– Whether to bypass the multi tools limitation, so that the tool can be used with other tools in the same agent.

- Raises:
**ValueError**– If both data_store_id and search_engine_id are not specified**or both are specified.**–


-
*async*process_llm_request(***,*tool_context*,*llm_request*)[¶](#google.adk.tools.vertex_ai_search_tool.VertexAiSearchTool.process_llm_request) Processes the outgoing LLM request for this tool.

Use cases: - Most common use case is adding this tool to the LLM request. - Some tools may just preprocess the LLM request before it’s sent out.

- Return type:
`None`

- Parameters:
**tool_context**– The context of the tool.**llm_request**– The outgoing LLM request, mutable this method.


-
data_store_id
