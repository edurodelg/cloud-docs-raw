---
merged_at: 2026-01-25T15:23:29.953168
merged_files: 4
---

# Documentos Fusionados

Este archivo contiene 4 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/deploy/agent-engine/ -->

# Deploy to Vertex AI Agent Engine¶

# Deploy to Vertex AI Agent Engine[¶](#deploy-to-vertex-ai-agent-engine)

Google Cloud Vertex AI
[Agent Engine](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview)
is a set of modular services that help developers scale and govern agents in
production. The Agent Engine runtime enables you to deploy agents in production
with end-to-end managed infrastructure so you can focus on creating intelligent
and impactful agents. When you deploy an ADK agent to Agent Engine, your code
runs in the *Agent Engine runtime* environment, which is part of the larger set
of agent services provided by the Agent Engine product.

This guide includes the following deployment paths, which serve different purposes:

-
: Follow this standard deployment path if you have an existing Google Cloud project and if you want to carefully manage deploying an ADK agent to the Agent Engine runtime. This deployment path uses Cloud Console, ADK command line interface, and provides step-by-step instructions. This path is recommended for users who are already familiar with configuring Google Cloud projects, and users preparing for production deployments.[Standard deployment](/adk-docs/deploy/agent-engine/deploy/) -
: Follow this accelerated deployment path if you do not have an existing Google Cloud project and are creating a project specifically for development and testing. The Agent Starter Pack (ASP) helps you deploy ADK projects quickly and it configures Google Cloud services that are not strictly necessary for running an ADK agent with the Agent Engine runtime.[Agent Starter Pack deployment](/adk-docs/deploy/agent-engine/asp/)

Agent Engine service on Google Cloud

Agent Engine is a paid service and you may incur costs if you go
above the no-cost access tier. More information can be found on the
[Agent Engine pricing page](https://cloud.google.com/vertex-ai/pricing#vertex-ai-agent-engine).

## Deployment payload[¶](#payload)

When you deploy your ADK agent project to Agent Engine, the following content is uploaded to the service:

- Your ADK agent code
- Any dependencies declared in your ADK agent code

The deployment *does not* include the ADK API server or the ADK web user
interface libraries. The Agent Engine service provides the libraries for ADK API
server functionality.


---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/deploy/agent-engine/asp/ -->

# Deploy to Agent Engine with Agent Starter Pack¶

# Deploy to Agent Engine with Agent Starter Pack[¶](#deploy-to-agent-engine-with-agent-starter-pack)

This deployment procedure describes how to perform a deployment using the
[Agent Starter Pack](https://github.com/GoogleCloudPlatform/agent-starter-pack)
(ASP) and the ADK command line interface (CLI) tool. Using ASP for deployment to
the Agent Engine runtime is an accelerated path, and you should use it for
* development and testing* only. The ASP tool configures Google Cloud resources
that are not strictly necessary for running an ADK agent workflow, and you
should thoroughly review that configuration before using it in a production
deployment.

This deployment guide uses the ASP tool to apply a project template to your existing project, add deployment artifacts, and prepare your agent project for deployment. These instructions show you how to use ASP to provision a Google Cloud project with services needed for deploying your ADK project, as follows:

[Prerequisites](#prerequisites-ad): Setup Google Cloud account, a project, and install required software.[Prepare your ADK project](#prepare-ad): Modify your existing ADK project files to get ready for deployment.[Connect to your Google Cloud project](#connect-ad): Connect your development environment to Google Cloud and your Google Cloud project.[Deploy your ADK project](#deploy-ad): Provision required services in your Google Cloud project and upload your ADK project code.

For information on testing a deployed agent, see [Test deployed agent](../test/).
For more information on using Agent Starter Pack and its command line tools,
see the
[CLI reference](https://googlecloudplatform.github.io/agent-starter-pack/cli/enhance.html)
and
[Development guide](https://googlecloudplatform.github.io/agent-starter-pack/guide/development-guide.html).

### Prerequisites[¶](#prerequisites-ad)

You need the following resources configured to use this deployment path:

**Google Cloud account**: with administrator access to the following:**Google Cloud Project**: An empty Google Cloud project with[billing enabled](https://cloud.google.com/billing/docs/how-to/modify-project). For information on creating projects, see[Creating and managing projects](https://cloud.google.com/resource-manager/docs/creating-managing-projects).

**Python Environment**: A Python version supported by the[ASP project](https://googlecloudplatform.github.io/agent-starter-pack/guide/getting-started.html).**uv Tool:**Manage Python development environment and running ASP tools. For installation details, see[Install uv](https://docs.astral.sh/uv/getting-started/installation/).**Google Cloud CLI tool**: The gcloud command line interface. For installation details, see[Google Cloud Command Line Interface](https://cloud.google.com/sdk/docs/install).**Make tool**: Build automation tool. This tool is part of most Unix-based systems, for installation details, see the[Make tool](https://www.gnu.org/software/make/)documentation.

### Prepare your ADK project[¶](#prepare-ad)

When you deploy an ADK project to Agent Engine, you need some additional files to support the deployment operation. The following ASP command backs up your project and then adds files to your project for deployment purposes.

These instructions assume you have an existing ADK project that you are modifying
for deployment. If you do not have an ADK project, or want to use a test
project, complete the Python
[Quickstart](/adk-docs/get-started/quickstart/) guide,
which creates a
[multi_tool_agent](https://github.com/google/adk-docs/tree/main/examples/python/snippets/get-started/multi_tool_agent)
project. The following instructions use the `multi_tool_agent`

project as an
example.

To prepare your ADK project for deployment to Agent Engine:

-
In a terminal window of your development environment, navigate to the

**parent directory**that contains your agent folder. For example, if your project structure is:Navigate to

`your-project-directory/`

-
Run the ASP

`enhance`

command to add the files required for deployment into your project. -
Follow the instructions from the ASP tool. In general, you can accept the default answers to all questions. However for the

**GCP region**, option, make sure you select one of the[supported regions](https://docs.cloud.google.com/agent-builder/locations#supported-regions-agent-engine)for Agent Engine.

When you successfully complete this process, the tool shows the following message:

Note

The ASP tool may show a reminder to connect to Google Cloud while
running, but that connection is *not required* at this stage.

For more information about the changes ASP makes to your ADK project, see
[Changes to your ADK project](#adk-asp-changes).

### Connect to your Google Cloud project[¶](#connect-ad)

Before you deploy your ADK project, you must connect to Google Cloud and your project. After logging into your Google Cloud account, you should verify that your deployment target project is visible from your account and that it is configured as your current project.

To connect to Google Cloud and list your project:

-
In a terminal window of your development environment, login to your Google Cloud account:

-
Set your target project using the Google Cloud Project ID:

-
Verify your Google Cloud target project is set:


Once you have successfully connected to Google Cloud and set your Cloud Project ID, you are ready to deploy your ADK project files to Agent Engine.

### Deploy your ADK project[¶](#deploy-ad)

When using the ASP tool, you deploy in stages. In the first stage, you run a
`make`

command that provisions the services needed to run your ADK workflow on
Agent Engine. In the second stage, the tool uploads your project code to the
Agent Engine service and runs it in the hosted environment

Important

*Make sure your Google Cloud target deployment project is set as your ***current
project*** before performing these steps*. The `make backend`

command uses
your currently set Google Cloud project when it performs a deployment. For
information on setting and checking your current project, see
[Connect to your Google Cloud project](#connect-ad).

To deploy your ADK project to Agent Engine in your Google Cloud project:

-
In a terminal window, ensure you are in the parent directory (e.g.,

`your-project-directory/`

) that contains your agent folder. -
Deploy the code from the updated local project into the Google Cloud development environment, by running the following ASP make command:


Once this process completes successfully, you should be able to interact with
the agent running on Google Cloud Agent Engine. For details on testing the
deployed agent, see
[Test deployed agent](/adk-docs/deploy/agent-engine/test/).

### Changes to your ADK project[¶](#adk-asp-changes)

The ASP tools add more files to your project for deployment. The procedure
below backs up your existing project files before modifying them. This guide
uses the
[multi_tool_agent](https://github.com/google/adk-docs/tree/main/examples/python/snippets/get-started/multi_tool_agent)
project as a reference example. The original project has the following file
structure to start with:

After running the ASP enhance command to add Agent Engine deployment information, the new structure is as follows:

multi-tool-agent/
├─ app/ # Core application code
│ ├─ agent.py # Main agent logic
│ ├─ agent_engine_app.py # Agent Engine application logic
│ └─ utils/ # Utility functions and helpers
├─ .cloudbuild/ # CI/CD pipeline configurations for Google Cloud Build
├─ deployment/ # Infrastructure and deployment scripts
├─ notebooks/ # Jupyter notebooks for prototyping and evaluation
├─ tests/ # Unit, integration, and load tests
├─ Makefile # Makefile for common commands
├─ GEMINI.md # AI-assisted development guide
└─ pyproject.toml # Project dependencies and configuration


See the *README.md* file in your updated ADK project folder for more information.
For more information on using Agent Starter Pack, see the
[Development guide](https://googlecloudplatform.github.io/agent-starter-pack/guide/development-guide.html).

## Test deployed agents[¶](#test-deployed-agents)

After completing deployment of your ADK agent you should test the workflow in
its new hosted environment. For more information on testing an ADK agent
deployed to Agent Engine, see
[Test deployed agents in Agent Engine](/adk-docs/deploy/agent-engine/test/).


---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/deploy/agent-engine/deploy/ -->

# Deploy to Vertex AI Agent Engine¶

# Deploy to Vertex AI Agent Engine[¶](#deploy-to-vertex-ai-agent-engine)

This deployment procedure describes how to perform a standard deployment of
ADK agent code to Google Cloud
[Agent Engine](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview).
You should follow this deployment path if you have an existing Google Cloud
project and if you want to carefully manage deploying an ADK agent to Agent
Engine runtime environment. These instructions use Cloud Console, the gcloud
command line interface, and the ADK command line interface (ADK CLI). This path
is recommended for users who are already familiar with configuring Google Cloud
projects, and users preparing for production deployments.

These instructions describe how to deploy an ADK project to Google Cloud Agent Engine runtime environment, which includes the following stages:

## Setup Google Cloud project[¶](#setup-cloud-project)

To deploy your agent to Agent Engine, you need a Google Cloud project:

-
**Sign into Google Cloud**:- If you're an
**existing user**of Google Cloud:- Sign in via
[https://console.cloud.google.com](https://console.cloud.google.com) - If you previously used a Free Trial that has expired, you may need to
upgrade to a
[Paid billing account](https://docs.cloud.google.com/free/docs/free-cloud-features#how-to-upgrade).

- Sign in via
- If you are a
**new user**of Google Cloud:- You can sign up for the
[Free Trial program](https://docs.cloud.google.com/free/docs/free-cloud-features). The Free Trial gets you a $300 Welcome credit to spend over 91 days on various[Google Cloud products](https://docs.cloud.google.com/free/docs/free-cloud-features#during-free-trial)and you won't be billed. During the Free Trial, you also get access to the[Google Cloud Free Tier](https://docs.cloud.google.com/free/docs/free-cloud-features#free-tier), which gives you free usage of select products up to specified monthly limits, and to product-specific free trials.

- You can sign up for the

- If you're an
-
**Create a Google Cloud project**- If you already have an existing Google Cloud project, you can use it, but be aware this process is likely to add new services to the project.
- If you want to create a new Google Cloud project, you can create a new one
on the
[Create Project](https://console.cloud.google.com/projectcreate)page.

-
**Get your Google Cloud Project ID**- You need your Google Cloud Project ID, which you can find on your GCP
homepage. Make sure to note the Project ID (alphanumeric with hyphens),
*not*the project number (numeric).

- You need your Google Cloud Project ID, which you can find on your GCP
homepage. Make sure to note the Project ID (alphanumeric with hyphens),
-
**Enable Vertex AI in your project**- To use Agent Engine, you need to
[enable the Vertex AI API](https://console.cloud.google.com/apis/library/aiplatform.googleapis.com). Click on the "Enable" button to enable the API. Once enabled, it should say "API Enabled".

- To use Agent Engine, you need to
-
**Enable Cloud Resource Manager API in your project**- To use Agent Engine, you need to
[enable the Cloud Resource Manager API](https://console.developers.google.com/apis/api/cloudresourcemanager.googleapis.com/overview). Click on the "Enable" button to enable the API. Once enabled, it should say "API Enabled".

- To use Agent Engine, you need to

## Set up your coding environment[¶](#prerequisites-coding-env)

Now that you prepared your Google Cloud project, you can return to your coding environment. These steps require access to a terminal within your coding environment to run command line instructions.

### Authenticate your coding environment with Google Cloud[¶](#authenticate-your-coding-environment-with-google-cloud)

-
You need to authenticate your coding environment so that you and your code can interact with Google Cloud. To do so, you need the gcloud CLI. If you have never used the gcloud CLI, you need to first

[download and install it](https://docs.cloud.google.com/sdk/docs/install-sdk)before continuing with the steps below: -
Run the following command in your terminal to access your Google Cloud project as a user:

After authenticating, you should see the message

`You are now authenticated with the gcloud CLI!`

. -
Run the following command to authenticate your code so that it can work with Google Cloud:

After authenticating, you should see the message

`You are now authenticated with the gcloud CLI!`

. -
(Optional) If you need to set or change your default project in gcloud, you can use:


### Define your agent[¶](#define-your-agent)

With your Google Cloud and coding environment prepared, you're ready to deploy your agent. The instructions assume that you have an agent project folder, such as:

For more details on the project files and format, see the
[multi_tool_agent](https://github.com/google/adk-docs/tree/main/examples/python/snippets/get-started/multi_tool_agent)
code sample.

## Deploy the agent[¶](#deploy-agent)

You can deploy from your terminal using the `adk deploy`

command line tool. This
process packages your code, builds it into a container, and deploys it to the
managed Agent Engine service. This process can take several minutes.

The following example deploy command uses the `multi_tool_agent`

sample code as
the project to be deployed:

PROJECT_ID=my-project-id
LOCATION_ID=us-central1
adk deploy agent_engine \
--project=$PROJECT_ID \
--region=$LOCATION_ID \
--display_name="My First Agent" \
multi_tool_agent


For `region`

, you can find a list of the supported regions on the
[Vertex AI Agent Builder locations page](https://docs.cloud.google.com/agent-builder/locations#supported-regions-agent-engine).
To learn about the CLI options for the `adk deploy agent_engine`

command, see the
[ADK CLI Reference](https://google.github.io/adk-docs/api-reference/cli/cli.html#adk-deploy-agent-engine).

### Deploy command output[¶](#deploy-command-output)

Once successfully deployed, you should see the following output:

Creating AgentEngine
Create AgentEngine backing LRO: projects/123456789/locations/us-central1/reasoningEngines/751619551677906944/operations/2356952072064073728
View progress and logs at https://console.cloud.google.com/logs/query?project=hopeful-sunset-478017-q0
AgentEngine created. Resource name: projects/123456789/locations/us-central1/reasoningEngines/751619551677906944
To use this AgentEngine in another session:
agent_engine = vertexai.agent_engines.get('projects/123456789/locations/us-central1/reasoningEngines/751619551677906944')
Cleaning up the temp folder: /var/folders/k5/pv70z5m92s30k0n7hfkxszfr00mz24/T/agent_engine_deploy_src/20251219_134245


Note that you now have a `RESOURCE_ID`

where your agent has been deployed (which
in the example above is `751619551677906944`

). You need this ID number along
with the other values to use your agent on Agent Engine.

## Using an agent on Agent Engine[¶](#using-an-agent-on-agent-engine)

Once you have completed deployment of your ADK project, you can query the agent using the Vertex AI SDK, Python requests library, or a REST API client. This section provides some information on what you need to interact with your agent and how to construct URLs to interact with your agent's REST API.

To interact with your agent on Agent Engine, you need the following:

**PROJECT_ID**(example: "my-project-id") which you can find on your[project details page](https://console.cloud.google.com/iam-admin/settings)**LOCATION_ID**(example: "us-central1"), that you used to deploy your agent**RESOURCE_ID**(example: "751619551677906944"), which you can find on the[Agent Engine UI](https://console.cloud.google.com/vertex-ai/agents/agent-engines)

The query URL structure is as follows:

https://$(LOCATION_ID)-aiplatform.googleapis.com/v1/projects/$(PROJECT_ID)/locations/$(LOCATION_ID)/reasoningEngines/$(RESOURCE_ID):query


You can make requests from your agent using this URL structure. For more information
on how to make requests, see the instructions in the Agent Engine documentation
[Use an Agent Development Kit agent](https://docs.cloud.google.com/agent-builder/agent-engine/use/adk#rest-api).
You can also check the Agent Engine documentation to learn about how to manage your
[deployed agent](https://docs.cloud.google.com/agent-builder/agent-engine/manage/overview).
For more information on testing and interacting with a deployed agent, see
[Test deployed agents in Agent Engine](/adk-docs/deploy/agent-engine/test/).

### Monitoring and verification[¶](#monitoring-and-verification)

- You can monitor the deployment status in the
[Agent Engine UI](https://console.cloud.google.com/vertex-ai/agents/agent-engines)in the Google Cloud Console. - For additional details, you can visit the Agent Engine documentation
[deploying an agent](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/deploy)and[managing deployed agents](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/manage/overview).

## Test deployed agents[¶](#test-deployed-agents)

After completing deployment of your ADK agent you should test the workflow in
its new hosted environment. For more information on testing an ADK agent
deployed to Agent Engine, see
[Test deployed agents in Agent Engine](/adk-docs/deploy/agent-engine/test/).


---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/deploy/agent-engine/test/ -->

# Test deployed agents in Agent Engine¶

# Test deployed agents in Agent Engine[¶](#test-deployed-agents-in-agent-engine)

These instructions explain how to test an ADK agent deployed to the
[Agent Engine](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview)
runtime environment. Before using these instructions, you need to have completed
the deployment of your agent to the Agent Engine runtime environment using one
of the [available methods](/adk-docs/deploy/agent-engine/). This guide shows you
how to view, interact, and test your deployed agent through the Google Cloud
Console, and interact with the agent using REST API calls or the Vertex AI SDK
for Python.

## View deployed agent in Cloud Console[¶](#view-deployed-agent-in-cloud-console)

To view your deployed agent in the Cloud Console:

- Navigate to the Agent Engine page in the Google Cloud Console:
[https://console.cloud.google.com/vertex-ai/agents/agent-engines](https://console.cloud.google.com/vertex-ai/agents/agent-engines)

This page lists all deployed agents in your currently selected Google Cloud
project. If you do not see your agent listed, make sure you have your
target project selected in Google Cloud Console. For more information on
selecting an existing Google Cloud project, see
[Creating and managing projects](https://cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects).

## Find Google Cloud project information[¶](#find-google-cloud-project-information)

You need the address and resource identification for your project (`PROJECT_ID`

,
`LOCATION_ID`

, `RESOURCE_ID`

) to be able to test your deployment. You can use Cloud
Console or the `gcloud`

command line tool to find this information.

## Vertex AI express mode API key

If you are using Vertex AI express mode, you can skip this step and use your API key.

To find your project information with Google Cloud Console:

-
In the Google Cloud Console, navigate to the Agent Engine page:

[https://console.cloud.google.com/vertex-ai/agents/agent-engines](https://console.cloud.google.com/vertex-ai/agents/agent-engines) -
At the top of the page, select

**API URLs**, and then copy the**Query URL**string for your deployed agent, which should be in this format:`https://$(LOCATION_ID)-aiplatform.googleapis.com/v1/projects/$(PROJECT_ID)/locations/$(LOCATION_ID)/reasoningEngines/$(RESOURCE_ID):query`


To find your project information with the `gcloud`

command line tool:

-
In your development environment, make sure you are authenticated to Google Cloud and run the following command to list your project:

-
With the Project ID you used for deployment, run this command to get the additional details:


## Test using REST calls[¶](#test-using-rest-calls)

A simple way to interact with your deployed agent in Agent Engine is to use REST
calls with the `curl`

tool. This section describes how to check your
connection to the agent and also to test processing of a request by the deployed
agent.

### Check connection to agent[¶](#check-connection-to-agent)

You can check your connection to the running agent using the **Query URL**
available in the Agent Engine section of the Cloud Console. This check does not
execute the deployed agent, but returns information about the agent.

To send a REST call and get a response from deployed agent:

-
In a terminal window of your development environment, build a request and execute it:


If your deployment was successful, this request responds with a list of valid requests and expected data formats.

Remove `:query`

parameter for connection URL

If you use the **Query URL** available in the Agent Engine section of the Cloud
Console, make sure to remove the `:query`

parameter from end of the address.

Access for agent connections

This connection test requires the calling user has a valid access token for the deployed agent. When testing from other environments, make sure the calling user has access to connect to the agent in your Google Cloud project.

### Send an agent request[¶](#send-an-agent-request)

When getting responses from your agent project, you must first create a session, receive a Session ID, and then send your requests using that Session ID. This process is described in the following instructions.

To test interaction with the deployed agent via REST:

-
In a terminal window of your development environment, create a session by building a request using this template:

[curl \](#__codelineno-4-1)[-H "Authorization: Bearer $(gcloud auth print-access-token)" \](#__codelineno-4-2)[-H "Content-Type: application/json" \](#__codelineno-4-3)[https://$(LOCATION_ID)-aiplatform.googleapis.com/v1/projects/$(PROJECT_ID)/locations/$(LOCATION_ID)/reasoningEngines/$(RESOURCE_ID):query \](#__codelineno-4-4)[-d '{"class_method": "async_create_session", "input": {"user_id": "u_123"},}'](#__codelineno-4-5) -
In the response from the previous command, extract the created

**Session ID**from the**id**field: -
In a terminal window of your development environment, send a message to your agent by building a request using this template and the Session ID created in the previous step:

[curl \](#__codelineno-7-1)[-H "Authorization: Bearer $(gcloud auth print-access-token)" \](#__codelineno-7-2)[-H "Content-Type: application/json" \](#__codelineno-7-3)[https://$(LOCATION_ID)-aiplatform.googleapis.com/v1/projects/$(PROJECT_ID)/locations/$(LOCATION_ID)/reasoningEngines/$(RESOURCE_ID):query?alt=sse -d '{](#__codelineno-7-4)["class_method": "async_stream_query",](#__codelineno-7-5)["input": {](#__codelineno-7-6)["user_id": "u_123",](#__codelineno-7-7)["session_id": "4857885913439920384",](#__codelineno-7-8)["message": "Hey whats the weather in new york today?",](#__codelineno-7-9)[}](#__codelineno-7-10)[}'](#__codelineno-7-11)[curl \](#__codelineno-8-1)[-H "x-goog-api-key:YOUR-EXPRESS-MODE-API-KEY" \](#__codelineno-8-2)[-H "Content-Type: application/json" \](#__codelineno-8-3)[https://aiplatform.googleapis.com/v1/reasoningEngines/$(RESOURCE_ID):query?alt=sse -d '{](#__codelineno-8-4)["class_method": "async_stream_query",](#__codelineno-8-5)["input": {](#__codelineno-8-6)["user_id": "u_123",](#__codelineno-8-7)["session_id": "4857885913439920384",](#__codelineno-8-8)["message": "Hey whats the weather in new york today?",](#__codelineno-8-9)[}](#__codelineno-8-10)[}'](#__codelineno-8-11)

This request should generate a response from your deployed agent code in JSON
format. For more information about interacting with a deployed ADK agent in
Agent Engine using REST calls, see
[Manage deployed agents](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/manage/overview#console)
and
[Use an Agent Development Kit agent](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/use/adk)
in the Agent Engine documentation.

## Test using Python[¶](#test-using-python)

You can use Python code for more sophisticated and repeatable testing of your agent deployed in Agent Engine. These instructions describe how to create a session with the deployed agent, and then send a request to the agent for processing.

### Create a remote session[¶](#create-a-remote-session)

Use the `remote_app`

object to create a connection to a deployed, remote agent:

# If you are in a new script or used the ADK CLI to deploy, you can connect like this:
# remote_app = agent_engines.get("your-agent-resource-name")
remote_session = await remote_app.async_create_session(user_id="u_456")
print(remote_session)


Expected output for `create_session`

(remote):

{'events': [],
'user_id': 'u_456',
'state': {},
'id': '7543472750996750336',
'app_name': '7917477678498709504',
'last_update_time': 1743683353.030133}


The `id`

value is the session ID, and `app_name`

is the resource ID of the
deployed agent on Agent Engine.

#### Send queries to your remote agent[¶](#send-queries-to-your-remote-agent)

async for event in remote_app.async_stream_query(
user_id="u_456",
session_id=remote_session["id"],
message="whats the weather in new york",
):
print(event)


Expected output for `async_stream_query`

(remote):

{'parts': [{'function_call': {'id': 'af-f1906423-a531-4ecf-a1ef-723b05e85321', 'args': {'city': 'new york'}, 'name': 'get_weather'}}], 'role': 'model'}
{'parts': [{'function_response': {'id': 'af-f1906423-a531-4ecf-a1ef-723b05e85321', 'name': 'get_weather', 'response': {'status': 'success', 'report': 'The weather in New York is sunny with a temperature of 25 degrees Celsius (41 degrees Fahrenheit).'}}}], 'role': 'user'}
{'parts': [{'text': 'The weather in New York is sunny with a temperature of 25 degrees Celsius (41 degrees Fahrenheit).'}], 'role': 'model'}


For more information about interacting with a deployed ADK agent in
Agent Engine, see
[Manage deployed agents](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/manage/overview)
and
[Use a Agent Development Kit agent](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/use/adk)
in the Agent Engine documentation.

### Sending Multimodal Queries[¶](#sending-multimodal-queries)

To send multimodal queries (e.g., including images) to your agent, you can construct the `message`

parameter of `async_stream_query`

with a list of `types.Part`

objects. Each part can be text or an image.

To include an image, you can use `types.Part.from_uri`

, providing a Google Cloud Storage (GCS) URI for the image.

from google.genai import types
image_part = types.Part.from_uri(
file_uri="gs://cloud-samples-data/generative-ai/image/scones.jpg",
mime_type="image/jpeg",
)
text_part = types.Part.from_text(
text="What is in this image?",
)
async for event in remote_app.async_stream_query(
user_id="u_456",
session_id=remote_session["id"],
message=[text_part, image_part],
):
print(event)


Note

While the underlying communication with the model may involve Base64 encoding for images, the recommended and supported method for sending image data to an agent deployed on Agent Engine is by providing a GCS URI.

## Clean up deployments[¶](#clean-up-deployments)

If you have performed deployments as tests, it is a good practice to clean up your cloud resources after you have finished. You can delete the deployed Agent Engine instance to avoid any unexpected charges on your Google Cloud account.

The `force=True`

parameter also deletes any child resources that were generated
from the deployed agent, such as sessions. You can also delete your deployed
agent via the
[Agent Engine UI](https://console.cloud.google.com/vertex-ai/agents/agent-engines)
on Google Cloud.
