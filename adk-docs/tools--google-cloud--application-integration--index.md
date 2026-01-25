---
source_url: https://google.github.io/adk-docs/tools/google-cloud/application-integration/
fetched_at: 2026-01-25T02:04:40.651839
---

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