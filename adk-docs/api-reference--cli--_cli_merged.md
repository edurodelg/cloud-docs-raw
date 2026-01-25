---
merged_at: 2026-01-25T03:28:16.333378
merged_files: 3
---

# Documentos Fusionados

Este archivo contiene 3 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/cli/ -->

# adk cli documentation¶

Add your content using reStructuredText syntax. See the reStructuredText documentation for details.

reStructuredText

Contents:


---

<!-- DOCUMENTO FUSIONADO: indexhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/cli/index.html -->

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
