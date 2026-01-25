---
source_url: https://google.github.io/adk-docs/tools/google-cloud/apigee-api-hub/
fetched_at: 2026-01-25T02:04:38.530963
---

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