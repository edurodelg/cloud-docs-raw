---
source_url: https://google.github.io/adk-docs/deploy/cloud-run/
fetched_at: 2026-01-25T02:06:06.493814
---

# Deploy to Cloud Run¶

# Deploy to Cloud Run[¶](#deploy-to-cloud-run)

[Cloud Run](https://cloud.google.com/run)
is a fully managed platform that enables you to run your code directly on top of Google's scalable infrastructure.

To deploy your agent, you can use either the `adk deploy cloud_run`

command *(recommended for Python)*, or with `gcloud run deploy`

command through Cloud Run.

## Agent sample[¶](#agent-sample)

For each of the commands, we will reference the `Capital Agent`

sample defined on the [LLM agent](../../agents/llm-agents/) page. We will assume it's in a directory (eg: `capital_agent`

).

To proceed, confirm that your agent code is configured as follows:

- Agent code is in a file called
`agent.py`

within your agent directory. - Your agent variable is named
`root_agent`

. `__init__.py`

is within your agent directory and contains`from . import agent`

.- Your
`requirements.txt`

file is present in the agent directory.

- Your application's entry point (the main package and main() function) is in a single Go file. Using main.go is a strong convention.
- Your agent instance is passed to a launcher configuration, typically using agent.NewSingleLoader(yourAgent). The adkgo tool uses this launcher to start your agent with the correct services.
- Your go.mod and go.sum files are present in your project directory to manage dependencies.

Refer to the following section for more details. You can also find a [sample app](https://github.com/google/adk-docs/tree/main/examples/go/cloud-run) in the Github repo.

- Agent code is in a file called
`CapitalAgent.java`

within your agent directory. - Your agent variable is global and follows the format
`public static final BaseAgent ROOT_AGENT`

. - Your agent definition is present in a static class method.

Refer to the following section for more details. You can also find a [sample app](https://github.com/google/adk-docs/tree/main/examples/java/cloud-run) in the Github repo.

## Environment variables[¶](#environment-variables)

Set your environment variables as described in the [Setup and Installation](../../get-started/installation/) guide.

export GOOGLE_CLOUD_PROJECT=your-project-id
export GOOGLE_CLOUD_LOCATION=us-central1 # Or your preferred location
export GOOGLE_GENAI_USE_VERTEXAI=True


*(Replace your-project-id with your actual GCP project ID)*

Alternatively you can also use an API key from AI Studio

export GOOGLE_CLOUD_PROJECT=your-project-id
export GOOGLE_CLOUD_LOCATION=us-central1 # Or your preferred location
export GOOGLE_GENAI_USE_VERTEXAI=FALSE
export GOOGLE_API_KEY=your-api-key


*(Replace*

`your-project-id`

with your actual GCP project ID and `your-api-key`

with your actual API key from AI Studio)## Prerequisites[¶](#prerequisites)

- You should have a Google Cloud project. You need to know your:
- Project name (i.e. "my-project")
- Project location (i.e. "us-central1")
- Service account (i.e. "1234567890-compute@developer.gserviceaccount.com")
- GOOGLE_API_KEY


## Secret[¶](#secret)

Please make sure you have created a secret which can be read by your service account.

### Entry for GOOGLE_API_KEY secret[¶](#entry-for-google_api_key-secret)

You can create your secret manually or use CLI:

echo "<<put your GOOGLE_API_KEY here>>" | gcloud secrets create GOOGLE_API_KEY --project=my-project --data-file=-


### Permissions to read[¶](#permissions-to-read)

You should give appropriate permission for you service account to read this secret.

gcloud secrets add-iam-policy-binding GOOGLE_API_KEY --member="serviceAccount:1234567890-compute@developer.gserviceaccount.com" --role="roles/secretmanager.secretAccessor" --project=my-project


## Deployment payload[¶](#payload)

When you deploy your ADK agent workflow to the Google Cloud Run, the following content is uploaded to the service:

- Your ADK agent code
- Any dependencies declared in your ADK agent code
- ADK API server code version used by your agent

The default deployment *does not* include the ADK web user interface libraries,
unless you specify it as deployment setting, such as the `--with_ui`

option for
`adk deploy cloud_run`

command.

## Deployment commands[¶](#deployment-commands)

### adk CLI[¶](#adk-cli)

The `adk deploy cloud_run`

command deploys your agent code to Google Cloud Run.

Ensure you have authenticated with Google Cloud (`gcloud auth login`

and `gcloud config set project <your-project-id>`

).

#### Setup environment variables[¶](#setup-environment-variables)

Optional but recommended: Setting environment variables can make the deployment commands cleaner.

# Set your Google Cloud Project ID
export GOOGLE_CLOUD_PROJECT="your-gcp-project-id"
# Set your desired Google Cloud Location
export GOOGLE_CLOUD_LOCATION="us-central1" # Example location
# Set the path to your agent code directory
export AGENT_PATH="./capital_agent" # Assuming capital_agent is in the current directory
# Set a name for your Cloud Run service (optional)
export SERVICE_NAME="capital-agent-service"
# Set an application name (optional)
export APP_NAME="capital_agent_app"


#### Command usage[¶](#command-usage)

##### Minimal command[¶](#minimal-command)

adk deploy cloud_run \
--project=$GOOGLE_CLOUD_PROJECT \
--region=$GOOGLE_CLOUD_LOCATION \
$AGENT_PATH


##### Full command with optional flags[¶](#full-command-with-optional-flags)

adk deploy cloud_run \
--project=$GOOGLE_CLOUD_PROJECT \
--region=$GOOGLE_CLOUD_LOCATION \
--service_name=$SERVICE_NAME \
--app_name=$APP_NAME \
--with_ui \
$AGENT_PATH


##### Arguments[¶](#arguments)

`AGENT_PATH`

: (Required) Positional argument specifying the path to the directory containing your agent's source code (e.g.,`$AGENT_PATH`

in the examples, or`capital_agent/`

). This directory must contain at least an`__init__.py`

and your main agent file (e.g.,`agent.py`

).

##### Options[¶](#options)

`--project TEXT`

: (Required) Your Google Cloud project ID (e.g.,`$GOOGLE_CLOUD_PROJECT`

).`--region TEXT`

: (Required) The Google Cloud location for deployment (e.g.,`$GOOGLE_CLOUD_LOCATION`

,`us-central1`

).`--service_name TEXT`

: (Optional) The name for the Cloud Run service (e.g.,`$SERVICE_NAME`

). Defaults to`adk-default-service-name`

.`--app_name TEXT`

: (Optional) The application name for the ADK API server (e.g.,`$APP_NAME`

). Defaults to the name of the directory specified by`AGENT_PATH`

(e.g.,`capital_agent`

if`AGENT_PATH`

is`./capital_agent`

).`--agent_engine_id TEXT`

: (Optional) If you are using a managed session service via Vertex AI Agent Engine, provide its resource ID here.`--port INTEGER`

: (Optional) The port number the ADK API server will listen on within the container. Defaults to 8000.`--with_ui`

: (Optional) If included, deploys the ADK dev UI alongside the agent API server. By default, only the API server is deployed.`--temp_folder TEXT`

: (Optional) Specifies a directory for storing intermediate files generated during the deployment process. Defaults to a timestamped folder in the system's temporary directory.*(Note: This option is generally not needed unless troubleshooting issues).*`--help`

: Show the help message and exit.

##### Authenticated access[¶](#authenticated-access)

During the deployment process, you might be prompted: `Allow unauthenticated invocations to [your-service-name] (y/N)?`

.

- Enter
`y`

to allow public access to your agent's API endpoint without authentication. - Enter
`N`

(or press Enter for the default) to require authentication (e.g., using an identity token as shown in the "Testing your agent" section).

Upon successful execution, the command deploys your agent to Cloud Run and provide the URL of the deployed service.

### gcloud CLI for Python[¶](#gcloud-cli-for-python)

Alternatively, you can deploy using the standard `gcloud run deploy`

command with a `Dockerfile`

. This method requires more manual setup compared to the `adk`

command but offers flexibility, particularly if you want to embed your agent within a custom [FastAPI](https://fastapi.tiangolo.com/) application.

Ensure you have authenticated with Google Cloud (`gcloud auth login`

and `gcloud config set project <your-project-id>`

).

#### Project Structure[¶](#project-structure)

Organize your project files as follows:

your-project-directory/
├── capital_agent/
│ ├── __init__.py
│ └── agent.py # Your agent code (see "Agent sample" tab)
├── main.py # FastAPI application entry point
├── requirements.txt # Python dependencies
└── Dockerfile # Container build instructions


Create the following files (`main.py`

, `requirements.txt`

, `Dockerfile`

) in the root of `your-project-directory/`

.

#### Code files[¶](#code-files)

-
This file sets up the FastAPI application using

`get_fast_api_app()`

from ADK:main.py[import os](#__codelineno-8-1)[import uvicorn](#__codelineno-8-3)[from fastapi import FastAPI](#__codelineno-8-4)[from google.adk.cli.fast_api import get_fast_api_app](#__codelineno-8-5)[# Get the directory where main.py is located](#__codelineno-8-7)[AGENT_DIR = os.path.dirname(os.path.abspath(__file__))](#__codelineno-8-8)[# Example session service URI (e.g., SQLite)](#__codelineno-8-9)[# Note: Use 'sqlite+aiosqlite' instead of 'sqlite' because DatabaseSessionService requires an async driver](#__codelineno-8-10)[SESSION_SERVICE_URI = "sqlite+aiosqlite:///./sessions.db"](#__codelineno-8-11)[# Example allowed origins for CORS](#__codelineno-8-12)[ALLOWED_ORIGINS = ["http://localhost", "http://localhost:8080", "*"]](#__codelineno-8-13)[# Set web=True if you intend to serve a web interface, False otherwise](#__codelineno-8-14)[SERVE_WEB_INTERFACE = True](#__codelineno-8-15)[# Call the function to get the FastAPI app instance](#__codelineno-8-17)[# Ensure the agent directory name ('capital_agent') matches your agent folder](#__codelineno-8-18)[app: FastAPI = get_fast_api_app(](#__codelineno-8-19)[agents_dir=AGENT_DIR,](#__codelineno-8-20)[session_service_uri=SESSION_SERVICE_URI,](#__codelineno-8-21)[allow_origins=ALLOWED_ORIGINS,](#__codelineno-8-22)[web=SERVE_WEB_INTERFACE,](#__codelineno-8-23)[)](#__codelineno-8-24)[# You can add more FastAPI routes or configurations below if needed](#__codelineno-8-26)[# Example:](#__codelineno-8-27)[# @app.get("/hello")](#__codelineno-8-28)[# async def read_root():](#__codelineno-8-29)[# return {"Hello": "World"}](#__codelineno-8-30)[if __name__ == "__main__":](#__codelineno-8-32)[# Use the PORT environment variable provided by Cloud Run, defaulting to 8080](#__codelineno-8-33)[uvicorn.run(app, host="0.0.0.0", port=int(os.environ.get("PORT", 8080)))](#__codelineno-8-34)*Note: We specify*`agent_dir`

to the directory`main.py`

is in and use`os.environ.get("PORT", 8080)`

for Cloud Run compatibility. -
List the necessary Python packages:

-
Define the container image:

Dockerfile[FROM python:3.13-slim](#__codelineno-10-1)[WORKDIR /app](#__codelineno-10-2)[COPY requirements.txt .](#__codelineno-10-4)[RUN pip install --no-cache-dir -r requirements.txt](#__codelineno-10-5)[RUN adduser --disabled-password --gecos "" myuser && \](#__codelineno-10-7)[chown -R myuser:myuser /app](#__codelineno-10-8)[COPY . .](#__codelineno-10-10)[USER myuser](#__codelineno-10-12)[ENV PATH="/home/myuser/.local/bin:$PATH"](#__codelineno-10-14)[CMD ["sh", "-c", "uvicorn main:app --host 0.0.0.0 --port $PORT"]](#__codelineno-10-16)

#### Defining Multiple Agents[¶](#defining-multiple-agents)

You can define and deploy multiple agents within the same Cloud Run instance by creating separate folders in the root of `your-project-directory/`

. Each folder represents one agent and must define a `root_agent`

in its configuration.

Example structure:

your-project-directory/
├── capital_agent/
│ ├── __init__.py
│ └── agent.py # contains `root_agent` definition
├── population_agent/
│ ├── __init__.py
│ └── agent.py # contains `root_agent` definition
└── ...


#### Deploy using `gcloud`

[¶](#deploy-using-gcloud)

Navigate to `your-project-directory`

in your terminal.

gcloud run deploy capital-agent-service \
--source . \
--region $GOOGLE_CLOUD_LOCATION \
--project $GOOGLE_CLOUD_PROJECT \
--allow-unauthenticated \
--set-env-vars="GOOGLE_CLOUD_PROJECT=$GOOGLE_CLOUD_PROJECT,GOOGLE_CLOUD_LOCATION=$GOOGLE_CLOUD_LOCATION,GOOGLE_GENAI_USE_VERTEXAI=$GOOGLE_GENAI_USE_VERTEXAI"
# Add any other necessary environment variables your agent might need


`capital-agent-service`

: The name you want to give your Cloud Run service.`--source .`

: Tells gcloud to build the container image from the Dockerfile in the current directory.`--region`

: Specifies the deployment region.`--project`

: Specifies the GCP project.`--allow-unauthenticated`

: Allows public access to the service. Remove this flag for private services.`--set-env-vars`

: Passes necessary environment variables to the running container. Ensure you include all variables required by ADK and your agent (like API keys if not using Application Default Credentials).

`gcloud`

will build the Docker image, push it to Google Artifact Registry, and deploy it to Cloud Run. Upon completion, it will output the URL of your deployed service.

For a full list of deployment options, see the [ gcloud run deploy reference documentation](https://cloud.google.com/sdk/gcloud/reference/run/deploy).

### adk CLI[¶](#adk-cli_1)

The adkgo command is located in the google/adk-go repository under cmd/adkgo. Before using it, you need to build it from the root of the adk-go repository:

`go build ./cmd/adkgo`


The adkgo deploy cloudrun command automates the deployment of your application. You do not need to provide your own Dockerfile.

#### Agent Code Structure[¶](#agent-code-structure)

When using the adkgo tool, your main.go file must use the launcher framework. This is because the tool compiles your code and then runs the resulting executable with specific command-line arguments (like web, api, a2a) to start the required services. The launcher is designed to parse these arguments correctly.

Your main.go should look like this:

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
"os"
"strings"
"google.golang.org/adk/agent"
"google.golang.org/adk/agent/llmagent"
"google.golang.org/adk/cmd/launcher"
"google.golang.org/adk/cmd/launcher/full"
"google.golang.org/adk/model/gemini"
"google.golang.org/adk/tool"
"google.golang.org/adk/tool/functiontool"
"google.golang.org/genai"
)
type getCapitalCityArgs struct {
Country string `json:"country" jsonschema:"The country for which to find the capital city."`
}
func getCapitalCity(ctx tool.Context, args getCapitalCityArgs) (string, error) {
capitals := map[string]string{
"united states": "Washington, D.C.",
"canada": "Ottawa",
"france": "Paris",
"japan": "Tokyo",
}
capital, ok := capitals[strings.ToLower(args.Country)]
if !ok {
return "", fmt.Errorf("couldn't find the capital for %s", args.Country)
}
return capital, nil
}
func main() {
ctx := context.Background()
model, err := gemini.NewModel(ctx, "gemini-2.5-flash", &genai.ClientConfig{
APIKey: os.Getenv("GOOGLE_API_KEY"),
})
if err != nil {
log.Fatalf("Failed to create model: %v", err)
}
capitalTool, err := functiontool.New(
functiontool.Config{
Name: "get_capital_city",
Description: "Retrieves the capital city for a given country.",
},
getCapitalCity,
)
if err != nil {
log.Fatalf("Failed to create function tool: %v", err)
}
geoAgent, err := llmagent.New(llmagent.Config{
Name: "capital_agent",
Model: model,
Description: "Agent to find the capital city of a country.",
Instruction: "I can answer your questions about the capital city of a country.",
Tools: []tool.Tool{capitalTool},
})
if err != nil {
log.Fatalf("Failed to create agent: %v", err)
}
config := &launcher.Config{
AgentLoader: agent.NewSingleLoader(geoAgent),
}
l := full.NewLauncher()
err = l.Execute(ctx, config, os.Args[1:])
if err != nil {
log.Fatalf("run failed: %v\n\n%s", err, l.CommandLineSyntax())
}
}


#### How it Works[¶](#how-it-works)

- The adkgo tool compiles your main.go into a statically linked binary for Linux.
- It generates a Dockerfile that copies this binary into a minimal container.
- It uses gcloud to build and deploy this container to Cloud Run.
- After deployment, it starts a local proxy that securely connects to your new service.

Ensure you have authenticated with Google Cloud (`gcloud auth login`

and `gcloud config set project <your-project-id>`

).

#### Setup environment variables[¶](#setup-environment-variables_1)

Optional but recommended: Setting environment variables can make the deployment commands cleaner.

# Set your Google Cloud Project ID
export GOOGLE_CLOUD_PROJECT="your-gcp-project-id"
# Set your desired Google Cloud Location
export GOOGLE_CLOUD_LOCATION="us-central1"
# Set the path to your agent's main Go file
export AGENT_PATH="./examples/go/cloud-run/main.go"
# Set a name for your Cloud Run service
export SERVICE_NAME="capital-agent-service"


#### Command usage[¶](#command-usage_1)

./adkgo deploy cloudrun \
-p $GOOGLE_CLOUD_PROJECT \
-r $GOOGLE_CLOUD_LOCATION \
-s $SERVICE_NAME \
--proxy_port=8081 \
--server_port=8080 \
-e $AGENT_PATH \
--a2a --api --webui


##### Required[¶](#required)

`-p, --project_name`

: Your Google Cloud project ID (e.g., $GOOGLE_CLOUD_PROJECT).`-r, --region`

: The Google Cloud location for deployment (e.g., $GOOGLE_CLOUD_LOCATION, us-central1).`-s, --service_name`

: The name for the Cloud Run service (e.g., $SERVICE_NAME).`-e, --entry_point_path`

: Path to the main Go file containing your agent's source code (e.g., $AGENT_PATH).

##### Optional[¶](#optional)

`--proxy_port`

: The local port for the authenticating proxy to listen on. Defaults to 8081.`--server_port`

: The port number the server will listen on within the Cloud Run container. Defaults to 8080.`--a2a`

: If included, enables Agent2Agent communication. Enabled by default.`--a2a_agent_url`

: A2A agent card URL as advertised in the public agent card. This flag is only valid when used with the --a2a flag.`--api`

: If included, deploys the ADK API server. Enabled by default.`--webui`

: If included, deploys the ADK dev UI alongside the agent API server. Enabled by default.`--temp_dir`

: Temp directory for build artifacts. Defaults to os.TempDir().`--help`

: Show the help message and exit.

##### Authenticated access[¶](#authenticated-access_1)

The service is deployed with --no-allow-unauthenticated by default.

Upon successful execution, the command deploys your agent to Cloud Run and provide a local URL to access the service through the proxy.

### gcloud CLI for Java[¶](#gcloud-cli-for-java)

You can deploy Java Agents using the standard `gcloud run deploy`

command and a `Dockerfile`

. This is the current recommended way to deploy Java Agents to Google Cloud Run.

Ensure you are [authenticated](https://cloud.google.com/docs/authentication/gcloud) with Google Cloud.
Specifically, run the commands `gcloud auth login`

and `gcloud config set project <your-project-id>`

from your terminal.

#### Project Structure[¶](#project-structure_1)

Organize your project files as follows:

your-project-directory/
├── src/
│ └── main/
│ └── java/
│ └── agents/
│ ├── capitalagent/
│ └── CapitalAgent.java # Your agent code
├── pom.xml # Java adk and adk-dev dependencies
└── Dockerfile # Container build instructions


Create the `pom.xml`

and `Dockerfile`

in the root of your project directory. Your Agent code file (`CapitalAgent.java`

) inside a directory as shown above.

#### Code files[¶](#code-files_1)

-
This is our Agent definition. This is the same code as present in

[LLM agent](../../agents/llm-agents/)with two caveats:-
The Agent is now initialized as a

**global public static final variable**. -
The definition of the agent can be exposed in a static method or inlined during declaration.


See the code for the

`CapitalAgent`

example in the[examples](https://github.com/google/adk-docs/blob/main/examples/java/cloud-run/src/main/java/agents/capitalagent/CapitalAgent.java)repository. -
-
Add the following dependencies and plugin to the pom.xml file.

pom.xml[<dependencies>](#__codelineno-17-1)[<dependency>](#__codelineno-17-2)[<groupId>com.google.adk</groupId>](#__codelineno-17-3)[<artifactId>google-adk</artifactId>](#__codelineno-17-4)[<version>0.5.0</version>](#__codelineno-17-5)[</dependency>](#__codelineno-17-6)[<dependency>](#__codelineno-17-7)[<groupId>com.google.adk</groupId>](#__codelineno-17-8)[<artifactId>google-adk-dev</artifactId>](#__codelineno-17-9)[<version>0.5.0</version>](#__codelineno-17-10)[</dependency>](#__codelineno-17-11)[</dependencies>](#__codelineno-17-12)[<plugin>](#__codelineno-17-14)[<groupId>org.codehaus.mojo</groupId>](#__codelineno-17-15)[<artifactId>exec-maven-plugin</artifactId>](#__codelineno-17-16)[<version>3.2.0</version>](#__codelineno-17-17)[<configuration>](#__codelineno-17-18)[<mainClass>com.google.adk.web.AdkWebServer</mainClass>](#__codelineno-17-19)[<classpathScope>compile</classpathScope>](#__codelineno-17-20)[</configuration>](#__codelineno-17-21)[</plugin>](#__codelineno-17-22) -
Define the container image:

Dockerfile[# Use an official Maven image with a JDK. Choose a version appropriate for your project.](#__codelineno-18-1)[FROM maven:3.8-openjdk-17 AS builder](#__codelineno-18-2)[WORKDIR /app](#__codelineno-18-4)[COPY pom.xml .](#__codelineno-18-6)[RUN mvn dependency:go-offline -B](#__codelineno-18-7)[COPY src ./src](#__codelineno-18-9)[# Expose the port your application will listen on.](#__codelineno-18-11)[# Cloud Run will set the PORT environment variable, which your app should use.](#__codelineno-18-12)[EXPOSE 8080](#__codelineno-18-13)[# The command to run your application.](#__codelineno-18-15)[# Use a shell so ${PORT} expands and quote exec.args so agent source-dir is passed correctly.](#__codelineno-18-16)[ENTRYPOINT ["sh", "-c", "mvn compile exec:java \](#__codelineno-18-17)[-Dexec.mainClass=com.google.adk.web.AdkWebServer \](#__codelineno-18-18)[-Dexec.classpathScope=compile \](#__codelineno-18-19)[-Dexec.args='--server.port=${PORT:-8080} --adk.agents.source-dir=target'"]](#__codelineno-18-20)

#### Deploy using `gcloud`

[¶](#deploy-using-gcloud_1)

Navigate to `your-project-directory`

in your terminal.

gcloud run deploy capital-agent-service \
--source . \
--region $GOOGLE_CLOUD_LOCATION \
--project $GOOGLE_CLOUD_PROJECT \
--allow-unauthenticated \
--set-env-vars="GOOGLE_CLOUD_PROJECT=$GOOGLE_CLOUD_PROJECT,GOOGLE_CLOUD_LOCATION=$GOOGLE_CLOUD_LOCATION,GOOGLE_GENAI_USE_VERTEXAI=$GOOGLE_GENAI_USE_VERTEXAI"
# Add any other necessary environment variables your agent might need


`capital-agent-service`

: The name you want to give your Cloud Run service.`--source .`

: Tells gcloud to build the container image from the Dockerfile in the current directory.`--region`

: Specifies the deployment region.`--project`

: Specifies the GCP project.`--allow-unauthenticated`

: Allows public access to the service. Remove this flag for private services.`--set-env-vars`

: Passes necessary environment variables to the running container. Ensure you include all variables required by ADK and your agent (like API keys if not using Application Default Credentials).

`gcloud`

will build the Docker image, push it to Google Artifact Registry, and deploy it to Cloud Run. Upon completion, it will output the URL of your deployed service.

For a full list of deployment options, see the [ gcloud run deploy reference documentation](https://cloud.google.com/sdk/gcloud/reference/run/deploy).

## Testing your agent[¶](#testing-your-agent)

Once your agent is deployed to Cloud Run, you can interact with it via the deployed UI (if enabled) or directly with its API endpoints using tools like `curl`

. You'll need the service URL provided after deployment.

### UI Testing[¶](#ui-testing)

If you deployed your agent with the UI enabled:

**adk CLI:**You included the`--webui`

flag during deployment.**gcloud CLI:**You set`SERVE_WEB_INTERFACE = True`

in your`main.py`

.

You can test your agent by simply navigating to the Cloud Run service URL provided after deployment in your web browser.

The ADK dev UI allows you to interact with your agent, manage sessions, and view execution details directly in the browser.

To verify your agent is working as intended, you can:

- Select your agent from the dropdown menu.
- Type a message and verify that you receive an expected response from your agent.

If you experience any unexpected behavior, check the [Cloud Run](https://console.cloud.google.com/run) console logs.

### API Testing (curl)[¶](#api-testing-curl)

You can interact with the agent's API endpoints using tools like `curl`

. This is useful for programmatic interaction or if you deployed without the UI.

You'll need the service URL provided after deployment and potentially an identity token for authentication if your service isn't set to allow unauthenticated access.

#### Set the application URL[¶](#set-the-application-url)

Replace the example URL with the actual URL of your deployed Cloud Run service.

export APP_URL="YOUR_CLOUD_RUN_SERVICE_URL"
# Example: export APP_URL="https://adk-default-service-name-abc123xyz.a.run.app"


#### Get an identity token (if needed)[¶](#get-an-identity-token-if-needed)

If your service requires authentication (i.e., you didn't use `--allow-unauthenticated`

with `gcloud`

or answered 'N' to the prompt with `adk`

), obtain an identity token.

*If your service allows unauthenticated access, you can omit the -H "Authorization: Bearer $TOKEN" header from the curl commands below.*


#### List available apps[¶](#list-available-apps)

Verify the deployed application name.

*(Adjust the app_name in the following commands based on this output if needed. The default is often the agent directory name, e.g., capital_agent)*.


#### Create or Update a Session[¶](#create-or-update-a-session)

Initialize or update the state for a specific user and session. Replace `capital_agent`

with your actual app name if different. The values `user_123`

and `session_abc`

are example identifiers; you can replace them with your desired user and session IDs.

curl -X POST -H "Authorization: Bearer $TOKEN" \
$APP_URL/apps/capital_agent/users/user_123/sessions/session_abc \
-H "Content-Type: application/json" \
-d '{"preferred_language": "English", "visit_count": 5}'


#### Run the Agent[¶](#run-the-agent)

Send a prompt to your agent. Replace `capital_agent`

with your app name and adjust the user/session IDs and prompt as needed.

curl -X POST -H "Authorization: Bearer $TOKEN" \
$APP_URL/run_sse \
-H "Content-Type: application/json" \
-d '{
"app_name": "capital_agent",
"user_id": "user_123",
"session_id": "session_abc",
"new_message": {
"role": "user",
"parts": [{
"text": "What is the capital of Canada?"
}]
},
"streaming": false
}'


- Set
`"streaming": true`

if you want to receive Server-Sent Events (SSE). - The response will contain the agent's execution events, including the final answer.