---
merged_at: 2026-01-26T23:20:36.826850
merged_files: 15
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/how-to/configure-marketplace -->

# Azure Marketplace requirements for Foundry Models from partners

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Certain Microsoft Foundry Models are offered directly by the model provider through the Azure Marketplace. This article explains the requirements to use Azure Marketplace if you plan to use such models in your workloads. Models sold directly by Azure, like DeepSeek, Black Forest Labs, or Azure OpenAI in Foundry Models, don't have this requirement.

## Permissions required to subscribe to Models from Partners and Community

[Foundry Models from partners and community](../concepts/models-from-partners?view=foundry-classic) available for deployment (for example, Cohere models) require Azure Marketplace. Model providers define the license terms and set the price for use of their models using Azure Marketplace.

When deploying third-party models, ensure you have the following permissions in your account:

- On the Azure subscription:
`Microsoft.MarketplaceOrdering/agreements/offers/plans/read`

`Microsoft.MarketplaceOrdering/agreements/offers/plans/sign/action`

`Microsoft.MarketplaceOrdering/offerTypes/publishers/offers/plans/agreements/read`

`Microsoft.Marketplace/offerTypes/publishers/offers/plans/agreements/read`

`Microsoft.SaaS/register/action`


- On the resource group—to create and use the SaaS resource:
`Microsoft.SaaS/resources/read`

`Microsoft.SaaS/resources/write`


## Country availability

Users can access models from partners and community with pay-as-you-go billing only if their Azure subscription belongs to a billing account in a country or region where the model offer is available. Availability varies per model provider and model SKU. For more information, see [Region availability for models](../../how-to/deploy-models-serverless-availability?view=foundry-classic).

## Troubleshooting

Use the following troubleshooting guide to find and solve errors when deploying third-party models in Foundry Models:

| Error | Description |
|---|---|
| This offer is not made available by the provider in the country where your account and Azure Subscription are registered. | The model provider didn't make the specific model SKU available in the country where you registered your subscription. Each model provider decides which countries to make the offer available in, and availability can vary by model SKU. You need to deploy the model to a subscription with billing in a supported country. See the list of countries at
|

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/how-to/quickstart-github-models -->

# Upgrade from GitHub Models to Microsoft Foundry Models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

In this article, you learn to develop a generative AI application by starting from GitHub Models and then upgrade your experience by deploying a Foundry Tools resource with Microsoft Foundry Models.

[GitHub Models](https://docs.github.com/en/github-models/) are useful when you want to find and experiment with AI models for free as you develop a generative AI application. When you're ready to bring your application to production, upgrade your experience by deploying a Foundry Tools resource in an Azure subscription and start using Foundry Models. You don't need to change anything else in your code.

The playground and free API usage for GitHub Models are [rate limited](https://docs.github.com/en/github-models/prototyping-with-ai-models#rate-limits) by requests per minute, requests per day, tokens per request, and concurrent requests. If you get rate limited, you need to wait for the rate limit that you hit to reset before you can make more requests.

## Prerequisites

To complete this tutorial, you need:

- A GitHub account with access to
[GitHub Models](https://docs.github.com/en/github-models/). - An Azure subscription with a valid payment method. If you don't have an Azure subscription, create a
[paid Azure account](https://azure.microsoft.com/pricing/purchase-options/pay-as-you-go)to begin. Alternatively, you can wait until you're ready to deploy your model to production, at which point you'll be prompted to create or update your Azure account to a standard account. [Foundry Models from partners and community](../concepts/models-from-partners?view=foundry-classic)require access to**Azure Marketplace**. Ensure you have the[permissions required to subscribe to model offerings](configure-marketplace?view=foundry-classic).[Foundry Models sold directly by Azure](../concepts/models-sold-directly-by-azure?view=foundry-classic)don't have this requirement.

## Upgrade to Foundry Models

The rate limits for the playground and free API usage help you experiment with models and develop your AI application. When you're ready to bring your application to production, use a key and endpoint from a paid Azure account. You don't need to change anything else in your code.

To get the key and endpoint:

Go to

[GitHub Models](https://github.com/marketplace/models)and select a model to land on its playground. This article uses Mistral Medium 3 (25.05).Type in some prompts or use some of the suggested prompts to interact with the model in the playground.

Select

**Use this model**from the playground. This action opens up a window to "Get started with Models in your codebase".In the "Configure authentication" step, select

**Get Microsoft Foundry key**from the "Azure AI" section.If you're already signed in to your Azure account, skip this step. However, if you don't have an Azure account or you're not signed in to your account, follow these steps:

If you don't have an Azure account, select

**Create my account**and follow the steps to create one.Alternatively, if you have an Azure account, select

**Sign back in**. If your existing account is a free account, you first have to upgrade to a standard plan.Return to the model's playground and select

**Get Microsoft Foundry key**again.Sign in to your Azure account.


You're taken to

[Foundry > GitHub](https://ai.azure.com/GitHub)and land on the home page in a Foundry project. The Foundry experience that opens up depends on the one you last used, either:You might land in the Foundry (new) experience. Notice the

**New Foundry**toggle is on in the upper-right navigation.Alternatively, you might land in the Foundry (classic) experience. Notice the

**New Foundry**toggle is off in the upper-right navigation.

Toggle the

**New Foundry**switcher if you prefer to switch to a different Foundry experience.Follow the steps in

[Deploy a model](deploy-foundry-models?view=foundry-classic#deploy-a-model)to deploy the model of your choice, test it in the Playground, and inference the deployed model with code.

Important

Unlike GitHub Models where all the models are already configured, the Foundry Tools resource allows you to control which models are available in your endpoint and under which configuration. Add as many models as you plan to use before indicating them in the `model`

parameter. Learn how to [add more models](../../model-inference/how-to/create-model-deployments?view=foundry-classic) to your resource.

## Explore additional features

Foundry Models supports extra features that aren't available in GitHub Models, including:

- The Model catalog
- Keyless authentication with Microsoft Entra ID
- Content filtering
- Rate limiting for specific models
- Additional
[deployment SKUs for specific models](../concepts/deployment-types?view=foundry-classic).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/how-to/configure-project-connection -->

# Configure a connection to use Microsoft Foundry Models in your AI project

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

You can use Microsoft Foundry Models in your projects in Foundry to create rich applications and interact/manage the models available. To use the Foundry Models service in your project, you need to create a connection to the Foundry resource (formerly known Azure AI Services).

The following article explains how to create a connection to the Foundry resource (formerly known Azure AI Services) to use Foundry Models.

## Prerequisites

To complete this article, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry resource (formerly known as Azure AI Services). For more information, see

[Create and configure all the resources for Foundry Models](quickstart-create-resources?view=foundry-classic).

## Add a connection

You can create a connection to a Foundry Tools resource using the following steps:

Go to

[Foundry portal](https://ai.azure.com/?cid=learnDocs).In the lower left corner of the screen, select

**Management center**.In the section

**Connected resources**select**New connection**.Select

**Foundry Tools**.In the browser, look for an existing Foundry Tools resource in your subscription.

Select

**Add connection**.The new connection is added to your Hub.

Return to the project's landing page to continue and now select the new created connection. Refresh the page if it doesn't show up immediately.


## See model deployments in the connected resource

You can see the model deployments available in the connected resource by following these steps:

Go to

[Foundry portal](https://ai.azure.com/?cid=learnDocs).On the left pane, select

**Models + endpoints**.The page displays the model deployments available to your, grouped by connection name. Locate the connection you have just created, which should be of type

**Foundry Tools**.Select any model deployment you want to inspect.

The details page shows information about the specific deployment. If you want to test the model, you can use the option

**Open in playground**.The Foundry playground is displayed, where you can interact with the given model.


You can use Microsoft Foundry Models in your projects in Foundry to create rich applications and interact/manage the models available. To use the Foundry Models service in your project, you need to create a connection to the Foundry resource (formerly known Azure AI Services).

The following article explains how to create a connection to the Foundry resource (formerly known Azure AI Services) to use Foundry Models.

## Prerequisites

To complete this article, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry resource (formerly known as Azure AI Services). For more information, see

[Create and configure all the resources for Foundry Models](quickstart-create-resources?view=foundry-classic).

Install the

[Azure CLI](/en-us/cli/azure/)and the`ml`

extension for Microsoft Foundry:`az extension add -n ml`

Identify the following information:

Your Azure subscription ID.

Your Foundry Tools resource name.

The resource group where the Foundry Tools resource is deployed.


### Add a connection

To add a model, you first need to identify the model that you want to deploy. You can query the available models as follows:

Log in into your Azure subscription:

`az login`

Configure the CLI to point to the project:

`az account set --subscription <subscription> az configure --defaults workspace=<project-name> group=<resource-group> location=<location>`

Create a connection definition:

**connection.yml**`name: <connection-name> type: aiservices endpoint: https://<ai-services-resourcename>.services.ai.azure.com api_key: <resource-api-key>`

Create the connection:

`az ml connection create -f connection.yml`

At this point, the connection is available for consumption.


You can use Microsoft Foundry Models in your projects in Foundry to create rich applications and interact/manage the models available. To use the Foundry Models service in your project, you need to create a connection to the Foundry resource (formerly known Azure AI Services).

The following article explains how to create a connection to the Foundry resource (formerly known Azure AI Services) to use Foundry Models.

## Prerequisites

To complete this article, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry resource (formerly known as Azure AI Services). For more information, see

[Create and configure all the resources for Foundry Models](quickstart-create-resources?view=foundry-classic).

A Foundry project with an AI Hub.

Install the

[Azure CLI](/en-us/cli/azure/).Identify the following information:

Your Azure subscription ID.

Your Foundry Tools resource name.

Your Foundry Tools resource ID.

The name of the Azure AI Hub where the project is deployed.

The resource group where the Foundry Tools resource is deployed.


## Add a connection

Use the template

`ai-services-connection-template.bicep`

to describe connection:**ai-services-connection-template.bicep**`@description('Name of the hub where the connection will be created') param hubName string @description('Name of the connection') param name string @description('Category of the connection') param category string = 'AIServices' @allowed(['AAD', 'ApiKey', 'ManagedIdentity', 'None']) param authType string = 'AAD' @description('The endpoint URI of the connected service') param endpointUri string @description('The resource ID of the connected service') param resourceId string = '' @secure() param key string = '' resource connection 'Microsoft.MachineLearningServices/workspaces/connections@2024-04-01-preview' = { name: '${hubName}/${name}' properties: { category: category target: endpointUri authType: authType isSharedToAll: true credentials: authType == 'ApiKey' ? { key: key } : null metadata: { ApiType: 'Azure' ResourceId: resourceId } } }`

Run the deployment:

`RESOURCE_GROUP="<resource-group-name>" ACCOUNT_NAME="<azure-ai-model-inference-name>" ENDPOINT_URI="https://<azure-ai-model-inference-name>.services.ai.azure.com" RESOURCE_ID="<resource-id>" HUB_NAME="<hub-name>" az deployment group create \ --resource-group $RESOURCE_GROUP \ --template-file ai-services-connection-template.bicep \ --parameters accountName=$ACCOUNT_NAME hubName=$HUB_NAME endpointUri=$ENDPOINT_URI resourceId=$RESOURCE_ID`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/how-to/configure-deployment-policies -->

# Control model deployment with custom policies

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

When you deploy models in Microsoft Foundry or Azure OpenAI, you might need Azure Policy to control which [deployment types](../../model-inference/concepts/deployment-types?view=foundry-classic) are available to users or which specific models they can deploy. This article shows you how to create a custom Azure Policy definition that denies non-approved model deployments.

Tip

The steps in this article apply to both a Foundry project and hub-based project.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - Permissions to create and assign policies. To create and assign policies, you must be an
[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner)or[Resource Policy Contributor](/en-us/azure/role-based-access-control/built-in-roles#resource-policy-contributor)at the Azure subscription or resource group level. - Familiarity with Azure Policy.

## Policy rule examples

Use one of the following examples as the starting point for your policy definition. Paste this JSON into the **Policy rule** editor when you create the policy definition.

Use this policy to control which specific models and versions are available for deployment.

```
{
"mode": "All",
"policyRule": {
"if": {
"allOf": [
{
"field": "type",
"equals": "Microsoft.CognitiveServices/accounts/deployments"
},
{
"not": {
"value": "[concat(field('Microsoft.CognitiveServices/accounts/deployments/model.name'), ',', field('Microsoft.CognitiveServices/accounts/deployments/model.version'))]",
"in": "[parameters('allowedModels')]"
}
}
]
},
"then": {
"effect": "deny"
}
},
"parameters": {
"allowedModels": {
"type": "Array",
"metadata": {
"displayName": "Allowed AI models",
"description": "The list of allowed models to be deployed."
}
}
}
}
```


This policy denies deployment creation or updates when the model name and version aren't included in the `allowedModels`

parameter.

References:

- Reference:
[Azure Policy definition structure basics](/en-us/azure/governance/policy/concepts/definition-structure-basics) - Reference:
[Azure Policy definition structure policy rule](/en-us/azure/governance/policy/concepts/definition-structure-policy-rule) - Reference:
[Azure Policy definition structure aliases](/en-us/azure/governance/policy/concepts/definition-structure-alias) - Reference:
[Azure Policy definitions deny effect](/en-us/azure/governance/policy/concepts/effect-deny) - Reference:
[Azure Policy definition schema](https://schema.management.azure.com/schemas/2020-10-01/policyDefinition.json)

Note

The resource provider name for Foundry Tools and Azure OpenAI is still `Microsoft.CognitiveServices`

. Azure Cognitive Services is a former name of Foundry Tools.

## Create and assign a custom policy

Follow these steps to create and assign an example custom policy to control model deployments:

From the

[Azure portal](https://portal.azure.com), select**Policy**from the left side of the page. You can also search for**Policy**in the search bar at the top of the page.From the left side of the Azure Policy Dashboard, select

**Authoring**,**Definitions**, and then select**+ Policy definition**from the top of the page.In the

**Policy Definition**form, use the following values:**Definition location**: Select the subscription or management group where you want to store the policy definition.**Name**: Enter a unique name for the policy definition. For example,`Custom allowed Foundry Tools and Azure OpenAI models`

.**Description**: Enter a description for the policy definition.**Category**: You can either create a new category or use an existing one. For example, "AI model governance."

On

**Policy rule**, paste one of the examples from the[Policy rule examples](#policy-rule-examples)section.Select

**Save**to save the policy definition. After saving, you arrive at the policy definition's overview page.From the policy definition's overview page, select

**Assign policy**to assign the policy definition.From the

**Assign policy**page, use the following values on the**Basics**tab:**Scope**: Select the scope where you want to assign the policy. The scope can be a management group, subscription, or resource group.**Policy definition**: This field is prepopulated with the title of policy definition you created previously.**Assignment name**: Enter a unique name for the assignment.**Policy enforcement**: Make sure that the**Policy enforcement**field is set to**Enabled**. If it's not enabled, the policy isn't enforced.

Select

**Next**at the bottom of the page, or the**Parameters**tab at the top of the page.Configure the parameters for the policy (if any):

From the

**Parameters**tab, set**Allowed AI models**to a JSON array of strings in the format`"<modelName>,<version>"`

. For example,`["gpt-4,0613", "gpt-35-turbo,0613"]`

.Tip

You can find the model name and version in the

[Foundry model catalog](https://ai.azure.com/explore/models). Select a model to view its details.Optionally, select the

**Non-compliance messages**tab at the top of the page and set a custom message for noncompliance.Select the

**Review + create**tab and verify that the policy assignment is correct. When ready, select**Create**to assign the policy.Notify your developers that the policy is in place. They receive an error message if they try to deploy a model that isn't in the list of allowed models.


## Verify policy assignment

To verify that the policy is assigned, go to **Policy** in the Azure portal, and then select **Assignments** under **Authoring**. You should see the policy listed.

To verify that the policy is enforced, try to create a deployment that violates the policy. The request is denied.

## Monitor compliance

To monitor compliance with the policy, follow these steps:

From the

[Azure portal](https://portal.azure.com), select**Policy**from the left side of the page. You can also search for**Policy**in the search bar at the top of the page.From the left side of the Azure Policy Dashboard, select

**Compliance**. Each policy assignment is listed with the compliance status. To view more details, select the policy assignment. The following example shows the compliance report for a policy that blocks deployments of type*Global standard*.

## Update the policy assignment

To update an existing policy assignment with new models, follow these steps:

- From the
[Azure portal](https://portal.azure.com), select**Policy**from the left side of the page. You can also search for**Policy**in the search bar at the top of the page. - From the left side of the Azure Policy Dashboard, select
**Assignments**and find the existing policy assignment. Select the ellipsis (...) next to the assignment and select**Edit assignment**. - From the
**Parameters**tab, update the**Allowed models**parameter with the new models. - From the
**Review + Save**tab, select**Save**to update the policy assignment.

## Best practices

**Granular scoping**: Assign policies at the appropriate scope to balance control and flexibility. For example, apply at the subscription level to control all resources in the subscription, or apply at the resource group level to control resources in a specific group.**Policy naming**: Use a consistent naming convention for policy assignments to make it easier to identify the purpose of the policy. Include information such as the purpose and scope in the name.**Documentation**: Keep records of policy assignments and configurations for auditing purposes. Document any changes made to the policy over time.**Regular reviews**: Periodically review policy assignments to ensure they align with your organization's requirements.**Testing**: Test policies in a nonproduction environment before applying them to production resources.**Communication**: Make sure developers are aware of the policies in place and understand the implications for their work.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/how-to/use-chat-completions -->

# Azure OpenAI in Microsoft Foundry Models API lifecycle

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article is to help you understand the support lifecycle for Azure OpenAI APIs.

Note

New API response objects may be added to the API response at any time. We recommend you only parse the response objects you require.

## API evolution

Previously, Azure OpenAI received monthly updates of new API versions. Taking advantage of new features required constantly updating code and environment variables with each new API release. Azure OpenAI also required the extra step of using Azure specific clients which created overhead when migrating code between OpenAI and Azure OpenAI.

Starting in August 2025, you can now opt in to our next generation v1 Azure OpenAI APIs which add support for:

- Ongoing access to the latest features with no need to specify new
`api-version`

's each month. - Faster API release cycle with new features launching more frequently.
- OpenAI client support with minimal code changes to swap between OpenAI and Azure OpenAI when using key-based authentication.
- OpenAI client support for token based authentication and automatic token refresh without the need to take a dependency on a separate Azure OpenAI client.
- Make chat completions calls with models from other providers like DeepSeek and Grok which support the v1 chat completions syntax.

Access to new API calls that are still in preview will be controlled by passing feature specific preview headers allowing you to opt in to the features you want, without having to swap API versions. Alternatively, some features will indicate preview status through their API path and don't require an additional header.

Examples:

`/openai/v1/evals`

is in preview and requires passing an`"aoai-evals":"preview"`

header.`/openai/v1/fine_tuning/alpha/graders/`

is in preview and requires no custom header due to the presence of`alpha`

in the API path.

For the initial v1 Generally Available (GA) API launch we're only supporting a subset of the inference and authoring API capabilities. All GA features are supported for use in production. We'll be rapidly adding support for more capabilities soon.

## Code changes

### v1 API

**API Key**:

```
import os
from openai import OpenAI
client = OpenAI(
api_key=os.getenv("AZURE_OPENAI_API_KEY"),
base_url="https://YOUR-RESOURCE-NAME.openai.azure.com/openai/v1/"
)
response = client.responses.create(
model="gpt-4.1-nano", # Replace with your model deployment name
input="This is a test.",
)
print(response.model_dump_json(indent=2))
```


`OpenAI()`

client is used instead of`AzureOpenAI()`

.`base_url`

passes the Azure OpenAI endpoint and`/openai/v1`

is appended to the endpoint address.`api-version`

is no longer a required parameter with the v1 GA API.

**API Key** with environment variables set for `OPENAI_BASE_URL`

and `OPENAI_API_KEY`

:

```
client = OpenAI()
```


**Microsoft Entra ID**:

Important

Handling automatic token refresh was previously handled through use of the `AzureOpenAI()`

client. The v1 API removes this dependency, by adding automatic token refresh support to the `OpenAI()`

client.

```
from openai import OpenAI
from azure.identity import DefaultAzureCredential, get_bearer_token_provider
token_provider = get_bearer_token_provider(
DefaultAzureCredential(), "https://cognitiveservices.azure.com/.default"
)
client = OpenAI(
base_url = "https://YOUR-RESOURCE-NAME.openai.azure.com/openai/v1/",
api_key = token_provider
)
response = client.responses.create(
model="gpt-4.1-nano",
input= "This is a test"
)
print(response.model_dump_json(indent=2))
```


`base_url`

passes the Azure OpenAI endpoint and`/openai/v1`

is appended to the endpoint address.`api_key`

parameter is set to`token_provider`

, enabling automatic retrieval and refresh of an authentication token instead of using a static API key.

## Model support

For Azure OpenAI models we recommend using the [Responses API](supported-languages?view=foundry-classic), however, the v1 API also allows you to make chat completions calls with models from other providers like DeepSeek and Grok which support the OpenAI v1 chat completions syntax.

`base_url`

will accept both `https://YOUR-RESOURCE-NAME.openai.azure.com/openai/v1/`

and `https://YOUR-RESOURCE-NAME.services.ai.azure.com/openai/v1/`

formats.

Note

Responses API also works with Foundry Models sold directly by Azure, such as Microsoft AI, DeepSeek, and Grok models. To learn how to use the Responses API with these models, see [How to generate text responses with Microsoft Foundry Models](../foundry-models/how-to/generate-responses?view=foundry-classic).

```
from openai import OpenAI
from azure.identity import DefaultAzureCredential, get_bearer_token_provider
token_provider = get_bearer_token_provider(
DefaultAzureCredential(), "https://cognitiveservices.azure.com/.default"
)
client = OpenAI(
base_url = "https://YOUR-RESOURCE-NAME.openai.azure.com/openai/v1/",
api_key=token_provider,
)
completion = client.chat.completions.create(
model="MAI-DS-R1", # Replace with your model deployment name.
messages=[
{"role": "system", "content": "You are a helpful assistant."},
{"role": "user", "content": "Tell me about the attention is all you need paper"}
]
)
#print(completion.choices[0].message)
print(completion.model_dump_json(indent=2))
```


## v1 API support

### Status

Generally Available features are supported for use in production.

| API Path | Status |
|---|---|
`/openai/v1/chat/completions` |
Generally Available |
`/openai/v1/embeddings` |
Generally Available |
`/openai/v1/evals` |
Preview |
`/openai/v1/files` |
Generally Available |
`/openai/v1/fine_tuning/jobs/{fine_tuning_job_id}/checkpoints/{fine_tuning_checkpoint_id}/copy` |
Preview |
`/openai/v1/fine_tuning/alpha/graders/` |
Preview |
`/openai/v1/fine_tuning/` |
Generally Available |
`/openai/v1/models` |
Generally Available |
`/openai/v1/responses` |
Generally Available |
`/openai/v1/vector_stores` |
Generally Available |

### Preview headers

| API Path | Header |
|---|---|
`/openai/v1/evals` |
`"aoai-evals":"preview"` |
`/openai/v1/fine_tuning/jobs/{fine_tuning_job_id}/checkpoints/{fine_tuning_checkpoint_id}/copy` |
`"aoai-copy-ft-checkpoints" : "preview"` |

## Changes between v1 preview release and 2025-04-01-preview

[v1 preview API](#api-evolution)[Video generation support](concepts/video-generation?view=foundry-classic)**NEW**Responses API features:- Remote Model Context Protocol (MCP) servers tool integration
- Support for asynchronous background tasks
- Encrypted reasoning items
- Image generation


## Changes between 2025-04-01-preview and 2025-03-01-preview

## Changes between 2025-03-01-preview and 2025-02-01-preview

[Responses API](how-to/responses?view=foundry-classic)- Computer use

## Changes between 2025-02-01-preview and 2025-01-01-preview

- Stored completions (distillation API support).

## Changes between 2025-01-01-preview and 2024-12-01-preview

`prediction`

parameter added for[predicted outputs](how-to/predicted-outputs?view=foundry-classic)support.`gpt-4o-audio-preview`

[model support](audio-completions-quickstart?view=foundry-classic).

## Changes between 2024-12-01-preview and 2024-10-01-preview

`store`

, and`metadata`

parameters added for stored completions support.`reasoning_effort`

added for latest[reasoning models](how-to/reasoning?view=foundry-classic).`user_security_context`

added for[Microsoft Defender for Cloud integration](https://aka.ms/TP4AI/Documentation/EndUserContext).

## Changes between 2024-09-01-preview and 2024-08-01-preview

`max_completion_tokens`

added to support`o1-preview`

and`o1-mini`

models.`max_tokens`

doesn't work with the**o1 series**models.`parallel_tool_calls`

added.`completion_tokens_details`

&`reasoning_tokens`

added.`stream_options`

&`include_usage`

added.

## Changes between 2024-07-01-preview and 2024-08-01-preview API specification

[Structured outputs support](how-to/structured-outputs?view=foundry-classic).- Large file upload API added.
- On your data changes:
- Mongo DB integration.
`role_information`

parameter removed.added to citation object.`rerank_score`

- AML datasource removed.
- AI Search vectorization integration improvements.


## Changes between 2024-5-01-preview and 2024-07-01-preview API specification

[Batch API support added](how-to/batch?view=foundry-classic)[Vector store chunking strategy parameters](/en-us/azure/ai-foundry/openai/reference-preview?#request-body-17)`max_num_results`

that the file search tool should output.

## Changes between 2024-04-01-preview and 2024-05-01-preview API specification

- Assistants v2 support -
[File search tool and vector storage](https://go.microsoft.com/fwlink/?linkid=2272425) - Fine-tuning
[checkpoints](https://github.com/Azure/azure-rest-api-specs/blob/9583ed6c26ce1f10bbea92346e28a46394a784b4/specification/cognitiveservices/data-plane/AzureOpenAI/authoring/preview/2024-05-01-preview/azureopenai.json#L586),[seed](https://github.com/Azure/azure-rest-api-specs/blob/9583ed6c26ce1f10bbea92346e28a46394a784b4/specification/cognitiveservices/data-plane/AzureOpenAI/authoring/preview/2024-05-01-preview/azureopenai.json#L1574),[events](https://github.com/Azure/azure-rest-api-specs/blob/9583ed6c26ce1f10bbea92346e28a46394a784b4/specification/cognitiveservices/data-plane/AzureOpenAI/authoring/preview/2024-05-01-preview/azureopenai.json#L529) - On your data updates
- DALL-E 2 now supports model deployment and can be used with the latest preview API.
- Content filtering updates

## Changes between 2024-03-01-preview and 2024-04-01-preview API specification

**Breaking Change**: Enhancements parameters removed. This impacts the`gpt-4`

**Version:**`vision-preview`

model.[timestamp_granularities](https://github.com/Azure/azure-rest-api-specs/blob/fbc90d63f236986f7eddfffe3dca6d9d734da0b2/specification/cognitiveservices/data-plane/AzureOpenAI/inference/preview/2024-04-01-preview/inference.json#L5217)parameter added.object added.`audioWord`

- Additional TTS
.`response_formats: wav & pcm`


## Known issues

- The
`2025-04-01-preview`

Azure OpenAI spec uses OpenAPI 3.1, is a known issue that this is currently not fully supported by[Azure API Management](/en-us/azure/api-management/api-management-key-concepts)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/how-to/quickstart-ai-project -->

# Configure your AI project to use Microsoft Foundry Models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

If you already have an AI project in Microsoft Foundry, the model catalog deploys models from partner model providers as stand-alone endpoints in your project by default. Each model deployment has its own set of URI and credentials to access it. On the other hand, Azure OpenAI models are deployed to the Foundry resource or to the Azure OpenAI in Foundry Models resource.

Important

If you're currently using an Azure AI Inference beta SDK with Microsoft Foundry Models or Azure OpenAI service, we strongly recommend that you transition to the generally available [OpenAI/v1 API](https://aka.ms/openai/v1), which uses an OpenAI stable SDK.

For more information on how to migrate to the OpenAI/v1 API by using an SDK in your programming language of choice, see [Migrate from Azure AI Inference SDK to OpenAI SDK](../../how-to/model-inference-to-openai-migration?view=foundry-classic).

You can change this behavior and deploy both types of models to Foundry resources. Once configured, *deployments of models as serverless API deployments happen to the connected Foundry resource* instead to the project itself, giving you a single set of endpoint and credentials to access all the models deployed in Foundry. You can manage models from Azure OpenAI and partner model providers in the same way.

Additionally, deploying models to Foundry Models brings the extra benefits of:

[Routing capability](inference?view=foundry-classic#routing)[Custom content filters](../../model-inference/concepts/content-filter?view=foundry-classic)- Global capacity deployment type
[Key-less authentication with Microsoft Entra ID](../../model-inference/how-to/configure-entra-id?view=foundry-classic)

In this article, you learn how to configure your project to use Foundry Models deployments.

## Prerequisites

To complete this tutorial, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. To learn more, see[Upgrade from GitHub Models to Foundry Models](../../model-inference/how-to/quickstart-github-models?view=foundry-classic).A Foundry resource. For more information, see

[Create your first Foundry resource](../../../ai-services/multi-service-resource?view=foundry-classic).A Foundry project and hub. For more information, see

[How to create and manage a Foundry hub](../../how-to/create-azure-ai-resource?view=foundry-classic).Tip

When your AI hub is provisioned, a Foundry resource is created with it and the two resources are connected. To see which resource is connected to your project, go to the

[Foundry portal](https://ai.azure.com/?cid=learnDocs)>**Management center**>**Connected resources**, and find the connections of type**Foundry Tools**.

## Configure the project to use Foundry Models

To configure the project to use the Foundry Models capability in Foundry, follow these steps:

In the landing page of your project, select

**Management center**at the bottom of the sidebar menu. Identify the Foundry resource connected to your project.If no resource is listed, your AI hub doesn't have a Foundry resource connected to it. Create a new connection.

Select

**+New connection**, then choose**Microsoft Foundry**from the tiles.In the window, look for an existing resource in your subscription and then select

**Add connection**.The new connection is added to your hub.


Return to the project's landing page.

Under

**Included capabilities**, ensure you select**Azure AI Inference**. The**Azure AI model inference endpoint**URI is displayed along with the credentials to get access to it.Tip

Each Foundry resource has a single

**Azure AI model inference endpoint**that can be used to access any model deployment on it. The same endpoint serves multiple models depending on which ones are configured. To learn how the endpoint works, see[Azure OpenAI inference endpoint](inference?view=foundry-classic#azure-openai-inference-endpoint).Take note of the endpoint URL and credentials.


### Create the model deployment in Foundry Models

For each model you want to deploy under Foundry Models, follow these steps:

Go to the

**Model catalog**in[Foundry portal](https://ai.azure.com/explore/models).Scroll to the model you're interested in and select it.

You can review the details of the model in the model card.

Select

**Use this model**.For model providers that require more contract terms, you're asked to accept those terms by selecting

**Agree and proceed**.You can configure the deployment settings at this time. By default, the deployment receives the name of the model you're deploying. The deployment name is used in the

`model`

parameter for request to route to this particular model deployment. It allows you to configure specific names for your models when you attach specific configurations. For instance,`o1-preview-safe`

for a model with a strict content filter.We automatically select a Foundry connection depending on your project because you turned on the feature

**Deploy models to Azure AI model inference service**. Select**Customize**to change the connection based on your needs. If you're deploying under the**serverless API**deployment type, the models need to be available in the region of the Foundry resource.Select

**Deploy**.Once the deployment finishes, you see the endpoint URL and credentials to get access to the model. Notice that now the provided URL and credentials are the same as displayed in the landing page of the project for the

**Foundry Models endpoint**.You can view all the models available under the resource by going to

**Models + endpoints**section and locating the group for the connection to your resource:

### Upgrade your code with the new endpoint

Once your Foundry resource is configured, you can start consuming it from your code. You need the endpoint URL and key for it, which can be found in the **Overview** section:

You can use any of the supported SDKs to get predictions out from the endpoint. The following SDKs are officially supported:

- OpenAI SDK
- Azure OpenAI SDK
- Azure AI Inference package
- Azure AI Projects package

For more information and examples, see [Supported programming languages for Azure AI Inference SDK](../../model-inference/supported-languages?view=foundry-classic). The following example shows how to use the Azure AI Inference package with the newly deployed model:

Install the package `azure-ai-inference`

using your package manager, like pip:

```
pip install azure-ai-inference
```


Then, you can use the package to consume the model. The following example shows how to create a client to consume chat completions:

```
import os
from azure.ai.inference import ChatCompletionsClient
from azure.core.credentials import AzureKeyCredential
client = ChatCompletionsClient(
endpoint="https://<resource>.services.ai.azure.com/models",
credential=AzureKeyCredential(os.environ["AZURE_INFERENCE_CREDENTIAL"]),
)
```


Explore our [samples](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/ai/azure-ai-inference/samples) and read the [API reference documentation](https://aka.ms/azsdk/azure-ai-inference/python/reference) to get yourself started.

Generate your first chat completion:

```
from azure.ai.inference.models import SystemMessage, UserMessage
response = client.complete(
messages=[
SystemMessage(content="You are a helpful assistant."),
UserMessage(content="Explain Riemann's conjecture in 1 paragraph"),
],
model="mistral-large"
)
print(response.choices[0].message.content)
```


Use the parameter `model="<deployment-name>`

to route your request to this deployment. *Deployments work as an alias of a given model under certain configurations*. To learn how Foundry Models routes deployments, see [Routing](inference?view=foundry-classic#routing).

## Move from serverless API deployments to Foundry Models

Although you configured the project to use Foundry Models, existing model deployments continue to exist within the project as serverless API deployments. Those deployments aren't moved for you. Hence, you can progressively upgrade any existing code that references previous model deployments. To start moving the model deployments, we recommend the following workflow:

Recreate the model deployment in Foundry Models. This model deployment is accessible under the

**Foundry Models endpoint**.Upgrade your code to use the new endpoint.

Clean up the project by removing the serverless API deployment.


### Upgrade your code with the new endpoint

Once the models are deployed under Foundry, you can upgrade your code to use the Foundry Models endpoint. The main difference between how serverless API deployments and Foundry Models work resides in the endpoint URL and model parameter. While serverless API deployments have a set of URI and key per each model deployment, Foundry Models has only one for all of them.

The following table summarizes the changes you have to introduce:

| Property | serverless API deployments | Foundry Models |
|---|---|---|
| Endpoint | `https://<endpoint-name>.<region>.inference.ai.azure.com` |
`https://<ai-resource>.services.ai.azure.com/models` |
| Credentials | One per model/endpoint. | One per Foundry resource. You can use Microsoft Entra ID too. |
| Model parameter | None. | Required. Use the name of the model deployment. |

### Clean-up existing serverless API deployments from your project

After you refactored your code, you might want to delete the existing serverless API deployments inside of the project (if any).

For each model deployed as serverless API deployments, follow these steps:

Go to the

[Foundry portal](https://ai.azure.com/?cid=learnDocs).Select

**Models + endpoints**, then choose the**Service endpoints**tab.Identify the endpoints of type

**serverless API deployment**and select the one you want to delete.Select the option

**Delete**.Warning

This operation can't be reverted. Ensure that the endpoint isn't currently used by any other user or piece of code.

Confirm the operation by selecting

**Delete**.If you created a

**serverless API deployment connection**to this endpoint from other projects, such connections aren't removed and continue to point to the inexistent endpoint. Delete any of those connections for avoiding errors.

## Limitations

Consider the following limitations when configuring your project to use Foundry Models:

- Only models that support serverless API deployments are available for deployment to Foundry Models. Models requiring compute quota from your subscription (managed compute), including custom models, can only be deployed within a given project as Managed Online Endpoints and continue to be accessible using their own set of endpoint URI and credentials.
- Models available as both serverless API deployments and managed compute offerings are, by default, deployed to Foundry Models in Foundry resources. Foundry portal doesn't offer a way to deploy them to Managed Online Endpoints. You have to turn off the feature mentioned at
[Configure the project to use Foundry Models](#configure-the-project-to-use-foundry-models)or use the Azure CLI/Azure ML SDK/ARM templates to perform the deployment.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/how-to/create-model-deployments -->

# Deploy models using Azure CLI and Bicep

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Important

If you're currently using an Azure AI Inference beta SDK with Microsoft Foundry Models or Azure OpenAI service, we strongly recommend that you transition to the generally available [OpenAI/v1 API](https://aka.ms/openai/v1), which uses an OpenAI stable SDK.

For more information on how to migrate to the OpenAI/v1 API by using an SDK in your programming language of choice, see [Migrate from Azure AI Inference SDK to OpenAI SDK](../../how-to/model-inference-to-openai-migration?view=foundry-classic).

In this article, you'll learn how to add a new model deployment to a Foundry Models endpoint. The deployment is available for inference in your Foundry resource when you specify the deployment name in your requests.

## Prerequisites

To complete this article, you need the following:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. For more information, see[Upgrade from GitHub Models to Foundry Models](quickstart-github-models?view=foundry-classic).A Foundry project. This project type is managed under a Foundry resource (formerly known as Azure AI Services resource). If you don't have a Foundry project, see

[Create a project for Microsoft Foundry](../../how-to/create-projects?view=foundry-classic).Azure role-based access control (RBAC) permissions to create and manage deployments. You need the

**Cognitive Services Contributor**role or equivalent permissions for the Foundry resource.[Foundry Models from partners and community](../concepts/models-from-partners?view=foundry-classic)require access to**Azure Marketplace**. Ensure you have the[permissions required to subscribe to model offerings](configure-marketplace?view=foundry-classic).[Foundry Models sold directly by Azure](../concepts/models-sold-directly-by-azure?view=foundry-classic)don't have this requirement.

Install the

[Azure CLI](/en-us/cli/azure/)and the`cognitiveservices`

extension for Foundry Tools.`az extension add -n cognitiveservices`

Some commands in this tutorial use the

`jq`

tool, which might not be installed on your system. For installation instructions, see[Download](https://stedolan.github.io/jq/download/).`jq`

Identify the following information:

Your Azure subscription ID

Your Foundry Tools resource name

The resource group where you deployed the Foundry Tools resource


## Add models

To add a model, first identify the model that you want to deploy. Query the available models as follows:

Sign in to your Azure subscription.

`az login`

If you have more than one subscription, select the subscription where your resource is located.

`az account set --subscription $subscriptionId`

Set the following environment variables with the name of the Foundry Tools resource you plan to use and resource group.

`accountName="<ai-services-resource-name>" resourceGroupName="<resource-group>" location="eastus2"`

If you haven't created a Foundry Tools account yet, create one.

`az cognitiveservices account create -n $accountName -g $resourceGroupName --custom-domain $accountName --location $location --kind AIServices --sku S0`

Reference:

[az cognitiveservices account](/en-us/cli/azure/cognitiveservices/account)Check which models are available to you and under which SKU. SKUs, also known as

[deployment types](../concepts/deployment-types?view=foundry-classic), define how Azure infrastructure processes requests. Models might offer different deployment types. The following command lists all the model definitions available:`az cognitiveservices account list-models \ -n $accountName \ -g $resourceGroupName \ | jq '.[] | { name: .name, format: .format, version: .version, sku: .skus[0].name, capacity: .skus[0].capacity.default }'`

The output includes available models with their properties:

`{ "name": "Phi-3.5-vision-instruct", "format": "Microsoft", "version": "2", "sku": "GlobalStandard", "capacity": 1 }`

Reference:

[az cognitiveservices account list-models](/en-us/cli/azure/cognitiveservices/account#az-cognitiveservices-account-list-models)Identify the model you want to deploy. You need the properties

`name`

,`format`

,`version`

, and`sku`

. The property`format`

indicates the provider offering the model. Depending on the type of deployment, you might also need capacity.Add the model deployment to the resource. The following example adds

`Phi-3.5-vision-instruct`

:`az cognitiveservices account deployment create \ -n $accountName \ -g $resourceGroupName \ --deployment-name Phi-3.5-vision-instruct \ --model-name Phi-3.5-vision-instruct \ --model-version 2 \ --model-format Microsoft \ --sku-capacity 1 \ --sku-name GlobalStandard`

Reference:

[az cognitiveservices account deployment](/en-us/cli/azure/cognitiveservices/account/deployment)The model is ready to use.


You can deploy the same model multiple times if needed as long as it's under a different deployment name. This capability is useful if you want to test different configurations for a given model, including content filters.

## Use the model

Note

This section is identical for both the CLI and Bicep approaches.

You can consume deployed models using the [Endpoints for Foundry Models](../concepts/endpoints?view=foundry-classic) for the resource. When you construct your request, specify the parameter `model`

and insert the model deployment name you created. You can programmatically get the URI for the inference endpoint by using the following code:

**Inference endpoint**

```
az cognitiveservices account show -n $accountName -g $resourceGroupName | jq '.properties.endpoints["Azure AI Model Inference API"]'
```


To make requests to the Foundry Models endpoint, append the route `models`

. For example: `https://<resource>.services.ai.azure.com/models`

. You can see the API reference for the endpoint at [Azure AI Model Inference API reference page](https://aka.ms/azureai/modelinference).

**Inference keys**

```
az cognitiveservices account keys list -n $accountName -g $resourceGroupName
```


## Manage deployments

You can see all the deployments available using the CLI:

Run the following command to see all the active deployments:

`az cognitiveservices account deployment list -n $accountName -g $resourceGroupName`

Reference:

[az cognitiveservices account deployment list](/en-us/cli/azure/cognitiveservices/account/deployment#az-cognitiveservices-account-deployment-list)You can see the details of a given deployment:

`az cognitiveservices account deployment show \ --deployment-name "Phi-3.5-vision-instruct" \ -n $accountName \ -g $resourceGroupName`

Reference:

[az cognitiveservices account deployment show](/en-us/cli/azure/cognitiveservices/account/deployment#az-cognitiveservices-account-deployment-show)You can delete a given deployment as follows:

`az cognitiveservices account deployment delete \ --deployment-name "Phi-3.5-vision-instruct" \ -n $accountName \ -g $resourceGroupName`


Install the

[Azure CLI](/en-us/cli/azure/).Identify the following information:

- Your Azure subscription ID

Your Foundry resource (formerly known as Azure AI Services resource) name

The resource group where the Foundry resource is deployed

The model name, provider, version, and SKU you want to deploy. You can use the Foundry portal or the Azure CLI to find this information. In this example, you deploy the following model:

**Model name**:`Phi-3.5-vision-instruct`

**Provider**:`Microsoft`

**Version**:`2`

**Deployment type**: Global standard


## Set up the environment

The example in this article is based on code samples contained in the [Azure-Samples/azureai-model-inference-bicep](https://github.com/Azure-Samples/azureai-model-inference-bicep) repository. To run the commands locally without having to copy or paste file content, clone the repository:

```
git clone https://github.com/Azure-Samples/azureai-model-inference-bicep
```


The files for this example are in:

```
cd azureai-model-inference-bicep/infra
```


## Permissions required to subscribe to Models from Partners and Community

[Foundry Models from partners and community](../concepts/models-from-partners?view=foundry-classic) available for deployment (for example, Cohere models) require Azure Marketplace. Model providers define the license terms and set the price for use of their models using Azure Marketplace.

When deploying third-party models, ensure you have the following permissions in your account:

- On the Azure subscription:
`Microsoft.MarketplaceOrdering/agreements/offers/plans/read`

`Microsoft.MarketplaceOrdering/agreements/offers/plans/sign/action`

`Microsoft.MarketplaceOrdering/offerTypes/publishers/offers/plans/agreements/read`

`Microsoft.Marketplace/offerTypes/publishers/offers/plans/agreements/read`

`Microsoft.SaaS/register/action`


- On the resource group—to create and use the SaaS resource:
`Microsoft.SaaS/resources/read`

`Microsoft.SaaS/resources/write`


## Add the model

Use the template

`ai-services-deployment-template.bicep`

to describe model deployments:**ai-services-deployment-template.bicep**`@description('Name of the Azure AI services account') param accountName string @description('Name of the model to deploy') param modelName string @description('Version of the model to deploy') param modelVersion string @allowed([ 'AI21 Labs' 'Cohere' 'Core42' 'DeepSeek' 'xAI' 'Meta' 'Microsoft' 'Mistral AI' 'OpenAI' ]) @description('Model provider') param modelPublisherFormat string @allowed([ 'GlobalStandard' 'DataZoneStandard' 'Standard' 'GlobalProvisioned' 'Provisioned' ]) @description('Model deployment SKU name') param skuName string = 'GlobalStandard' @description('Content filter policy name') param contentFilterPolicyName string = 'Microsoft.DefaultV2' @description('Model deployment capacity') param capacity int = 1 resource modelDeployment 'Microsoft.CognitiveServices/accounts/deployments@2024-04-01-preview' = { name: '${accountName}/${modelName}' sku: { name: skuName capacity: capacity } properties: { model: { format: modelPublisherFormat name: modelName version: modelVersion } raiPolicyName: contentFilterPolicyName == null ? 'Microsoft.Nill' : contentFilterPolicyName } }`

Run the deployment:

`RESOURCE_GROUP="<resource-group-name>" ACCOUNT_NAME="<azure-ai-model-inference-name>" MODEL_NAME="Phi-3.5-vision-instruct" PROVIDER="Microsoft" VERSION=2 az deployment group create \ --resource-group $RESOURCE_GROUP \ --template-file ai-services-deployment-template.bicep \ --parameters accountName=$ACCOUNT_NAME modelName=$MODEL_NAME modelVersion=$VERSION modelPublisherFormat=$PROVIDER`


## Use the model

Note

This section is identical for both the CLI and Bicep approaches.

You can consume deployed models using the [Endpoints for Foundry Models](../concepts/endpoints?view=foundry-classic) for the resource. When you construct your request, specify the parameter `model`

and insert the model deployment name you created. You can programmatically get the URI for the inference endpoint by using the following code:

**Inference endpoint**

```
az cognitiveservices account show -n $accountName -g $resourceGroupName | jq '.properties.endpoints["Azure AI Model Inference API"]'
```


To make requests to the Foundry Models endpoint, append the route `models`

. For example: `https://<resource>.services.ai.azure.com/models`

. You can see the API reference for the endpoint at [Azure AI Model Inference API reference page](https://aka.ms/azureai/modelinference).

**Inference keys**

```
az cognitiveservices account keys list -n $accountName -g $resourceGroupName
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/how-to/monitor-models -->

# Monitor model deployments in Microsoft Foundry Models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

When you have critical applications and business processes that rely on Azure resources, you need to monitor and get alerts for your system. The Azure Monitor service collects and aggregates metrics and logs from every component of your system, including Foundry Models deployments. You can use this information to view availability, performance, and resilience, and get notifications of issues.

This article explains how you can use metrics and logs to monitor model deployments in Foundry Models.

Note

Monitoring is only supported for OpenAI, Globalbatch sku & non-whisper models.

## Prerequisites

To use monitoring capabilities for model deployments in Foundry Models, you need the following:

-
Tip

If you're using serverless API endpoints and you want to take advantage of monitoring capabilities explained in this article,

[migrate your serverless API endpoints to Foundry Models](../../model-inference/how-to/quickstart-ai-project?view=foundry-classic). At least one model deployment.

Access to diagnostic information for the resource.


## Metrics

Azure Monitor collects metrics from Foundry Models automatically. *No configuration is required*. These metrics are:

- Stored in the Azure Monitor time-series metrics database.
- Lightweight and capable of supporting near real-time alerting.
- Used to track the performance of a resource over time.

### View metrics

Azure Monitor metrics can be queried using multiple tools, including:

#### Foundry portal

You can view metrics within the Foundry portal. To view them, follow these steps:

Go to the

[Foundry portal](https://ai.azure.com/?cid=learnDocs).Under

**My assets**in the sidebar menu, select**Models + endpoints**, and then select the name of the deployment you want to see metrics about.Select the

**Metrics**tab.You can access an overview of common metrics that might be of interest. For cost-related metrics, select the

**Azure Cost Management**link, which provides access to detailed post-consumption cost metrics in the**Cost analysis**section located in the Azure portal.Cost data in the Azure portal displays actual post-consumption charges for model consumption, including other AI resources within Foundry. For a full list of AI resources, see

[Build with customizable APIs and models](https://azure.microsoft.com/products/ai-services#tabs-pill-bar-oc14f0_tab0). There's approximately a five- hour delay from the billing event to when it can be viewed in Azure portal cost analysis.Important

The

**Azure Cost Management**link provides a direct link within the Azure portal, allowing users to access detailed cost metrics for deployed AI models. This deep link integrates with the Azure Cost Analysis service view, offering transparent and actionable insights into model-level costs.The deep link directs users to the Cost Analysis view in the Azure portal, providing a one-click experience to view deployments per resource, including input/output token cost/consumption. To view cost data, you need at least

*read*access for an Azure account. For information about assigning access to Cost Management data, see[Assign access to data](/en-us/azure/cost-management-billing/costs/assign-access-acm-data).You can view and analyze metrics with Azure Monitor

[metrics explorer](#metrics-explorer)to further slice and filter your model deployment metrics.

#### Metrics explorer

Metrics explorer is a tool in the Azure portal that allows you to view and analyze metrics for Azure resources. For more information, see [Analyze metrics with Azure Monitor metrics explorer](/en-us/azure/azure-monitor/metrics/analyze-metrics).

To use Azure Monitor, follow these steps:

Go to the

[Azure portal](https://portal.azure.com).Type and select

**Monitor**on the search box.Select

**Metrics**in the sidebar menu.On

**Select scope**, select the resources you want to monitor. You can either select one resource or select a resource group or subscription. If that's the case, ensure you select**Resource types**as**Foundry Tools**.The metrics explorer appears. Select the

[metrics](#metrics-reference)that you want to explore. The following example shows the number of requests made to the model deployments in the resource.Important

Metrics in the

**Azure OpenAI**category contain metrics for Azure OpenAI models in the resource. The**Models**category contains all the models available in the resource, including Azure OpenAI, DeepSeek, and Phi. We recommend switching to this new set of metrics.You can add as many metrics as needed to either the same chart or to a new chart.

If you need, you can filter metrics by any of their available dimensions.

It's useful to break down specific metrics by some of the dimensions. The following example shows how to break down the number of requests made to the resource by model by using the option

**Add splitting**:You can save your dashboards at any time to avoid having to configure them each time.


#### Kusto query language (KQL)

If you [configure diagnostic settings](#configure-diagnostic-settings) to send metrics to Log Analytics, you can use the Azure portal to query and analyze log data by using the Kusto query language (KQL).

To query metrics, follow these steps:

Ensure that you

[configure diagnostic settings](#configure-diagnostic-settings)for your resource.Go to the

[Azure portal](https://portal.azure.com).Locate the Foundry resource you want to query.

Under

**Monitoring**in the sidebar menu, select**Logs**.Select the Log Analytics workspace that you configured with diagnostics.

From the Log Analytics workspace page, under

**Overview**on the sidebar menu, select Logs. The Azure portal displays a Queries window with sample queries and suggestions by default. You can close this window.To examine the Azure Metrics, use the table

`AzureMetrics`

for your resource, and run the following query:`AzureMetrics | take 100 | project TimeGenerated, MetricName, Total, Count, Maximum, Minimum, Average, TimeGrain, UnitName`

Note

When you select

**Monitoring**>**Logs**in the menu for your resource, Log Analytics opens with the query scope set to the current resource. The visible log queries include data from that specific resource only. To run a query that includes data from other resources or data from other Azure services, select**Logs**from the**Azure Monitor**menu in the Azure portal. For more information, see[Log query scope and time range in Azure Monitor Log Analytics](/en-us/azure/azure-monitor/logs/scope).

#### Other tools

Tools that allow more complex visualization include:

[Workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview): customizable reports that you can create in the Azure portal. Workbooks can include text, metrics, and log queries.[Grafana](/en-us/azure/azure-monitor/visualize/grafana-plugin): an open platform tool that excels in operational dashboards. You can use Grafana to create dashboards that include data from multiple sources other than Azure Monitor.[Power BI](/en-us/azure/azure-monitor/logs/log-powerbi): a business analytics service that provides interactive visualizations across various data sources. You can configure Power BI to automatically import log data from Azure Monitor to take advantage of these visualizations.

### Metrics reference

The following categories of metrics are available:

#### Models - Requests

| Metric | Internal name | Unit | Aggregation | Dimensions |
|---|---|---|---|---|
Model Availability RateAvailability percentage with the following calculation: (Total Calls - Server Errors)/Total Calls. Server Errors include any HTTP responses >=500. |
`ModelAvailabilityRate` |
Percent | Minimum, Maximum, Average | `ApiName` , `OperationName` , `Region` , `StreamType` , `ModelDeploymentName` , `ModelName` , `ModelVersion` |
Model RequestsNumber of calls made to the model inference API over a period of time that resulted in a service error (>500). |
`ModelRequests ` |
Count | Total (Sum) | `ApiName` , `OperationName` , `Region` , `StreamType` , `ModelDeploymentName` , `ModelName` , `ModelVersion` , `StatusCode` |

#### Models - Latency

| Metric | Internal name | Unit | Aggregation | Dimensions |
|---|---|---|---|---|
Time To ResponseRecommended latency (responsiveness) measure for streaming requests. Applies to PTU and PTU-managed deployments. Calculated as time taken for the first response to appear after a user sends a prompt, as measured by the API gateway. This number increases as the prompt size increases and/or cache hit size reduces. Note: this metric is an approximation as measured latency is heavily dependent on multiple factors, including concurrent calls and overall workload pattern. In addition, it doesn't account for any client-side latency that might exist between your client and the API endpoint. Refer to your own logging for optimal latency tracking. |
`TimeToResponse` |
Milliseconds | Maximum, Minimum, Average | `ApiName` , `OperationName` , `Region` , `StreamType` , `ModelDeploymentName` , `ModelName` , `ModelVersion` , `StatusCode` |
Normalized Time Between TokensFor streaming requests; model token generation rate, measured in milliseconds. Applies to PTU and PTU-managed deployments. |
`NormalizedTimeBetweenTokens` |
Milliseconds | Maximum, Minimum, Average | `ApiName` , `OperationName` , `Region` , `StreamType` , `ModelDeploymentName` , `ModelName` , `ModelVersion` |

#### Models - Usage

| Metric | Internal name | Unit | Aggregation | Dimensions |
|---|---|---|---|---|
Input TokensNumber of prompt tokens processed (input) on a model. Applies to PTU, PTU-managed and standard deployments. |
`InputTokens` |
Count | Total (Sum) | `ApiName` , `Region` , `ModelDeploymentName` , `ModelName` , `ModelVersion` |
Output TokensNumber of tokens generated (output) from a model. Applies to PTU, PTU-managed and standard deployments. |
`OutputTokens` |
Count | Total (Sum) | `ApiName` , `Region` , `ModelDeploymentName` , `ModelName` , `ModelVersion` |
Total TokensNumber of inference tokens processed on a model. Calculated as prompt tokens (input) plus generated tokens (output). Applies to PTU, PTU-managed and standard deployments. |
`TotalTokens` |
Count | Total (Sum) | `ApiName` , `Region` , `ModelDeploymentName` , `ModelName` , `ModelVersion` |
Tokens Cache Match RatePercentage of prompt tokens that hit the cache. Applies to PTU and PTU-managed deployments. |
`TokensCacheMatchRate` |
Percentage | Average | `Region` , `ModelDeploymentName` , `ModelName` , `ModelVersion` |
Provisioned UtilizationUtilization % for a provisoned-managed deployment, calculated as (PTUs consumed / PTUs deployed) x 100. When utilization is greater than or equal to 100%, calls are throttled and error code 429 returned. |
`TokensCacheMatchRate ` |
Percentage | Average | `Region` , `ModelDeploymentName` , `ModelName` , `ModelVersion` |
Provisioned Consumed TokensTotal tokens minus cached tokens over a period of time. Applies to PTU and PTU-managed deployments. |
`ProvisionedConsumedTokens` |
Count | Total (Sum) | `Region` , `ModelDeploymentName` , `ModelName` , `ModelVersion` |
Audio Input TokensNumber of audio prompt tokens processed (input) on a model. Applies to PTU-managed model deployments. |
`AudioInputTokens` |
Count | Total (Sum) | `Region` , `ModelDeploymentName` , `ModelName` , `ModelVersion` |
Audio Output TokensNumber of audio prompt tokens generated (output) on a model. Applies to PTU-managed model deployments. |
`AudioOutputTokens` |
Count | Total (Sum) | `Region` , `ModelDeploymentName` , `ModelName` , `ModelVersion` |

## Logs

Resource logs provide insight into operations that were done by an Azure resource. Logs are generated automatically, but you must route them to Azure Monitor logs to save or query by [configuring a diagnostic setting](#configure-diagnostic-settings). Logs are organized in categories when you create a diagnostic setting, you specify which categories of logs to collect.

## Configure diagnostic settings

All of the metrics are exportable with diagnostic settings in Azure Monitor. To analyze logs and metrics data with Azure Monitor Log Analytics queries, you need to configure diagnostic settings for your Foundry Tools resource. You need to perform this operation on each resource.


There's a cost for collecting data in a Log Analytics workspace, so only collect the categories you require for each service. The data volume for resource logs varies significantly between services.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/how-to/configure-content-filters -->

# How to configure content filters for models in Microsoft Foundry

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Important

If you're currently using an Azure AI Inference beta SDK with Microsoft Foundry Models or Azure OpenAI service, we strongly recommend that you transition to the generally available [OpenAI/v1 API](https://aka.ms/openai/v1), which uses an OpenAI stable SDK.

For more information on how to migrate to the OpenAI/v1 API by using an SDK in your programming language of choice, see [Migrate from Azure AI Inference SDK to OpenAI SDK](../../how-to/model-inference-to-openai-migration?view=foundry-classic).

The content filtering system integrated into Microsoft Foundry runs alongside Foundry Models. It uses an ensemble of multi-class classification models to detect four categories of harmful content (violence, hate, sexual, and self-harm) at four severity levels (safe, low, medium, and high). It offers optional binary classifiers for detecting jailbreak risk, existing text, and code in public repositories. For more information about content categories, severity levels, and the behavior of the content filtering system, see [the following article](../concepts/content-filter?view=foundry-classic).

The [default content filtering](../concepts/default-safety-policies?view=foundry-classic) configuration filters content at the medium severity threshold for all four harmful categories for both prompts and completions. Content detected at medium or high severity level is filtered out, while content detected at low or safe severity level isn't filtered.

You can configure content filters at the resource level and associate them with one or more deployments.

## Prerequisites

To complete this article, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Foundry](quickstart-github-models?view=foundry-classic).A Foundry resource (formerly known as Azure AI Services resource). For more information, see

[Create a Foundry resource](quickstart-create-resources?view=foundry-classic).

- An AI project connected to your Foundry Tools resource. You can follow the steps at
[Configure Microsoft Foundry Models service in my project](configure-project-connection?view=foundry-classic)in Foundry.

## Create a custom content filter

Follow these steps to create a custom content filter:

Go to the

[Foundry portal](https://ai.azure.com/explore/models).Select

**Guardrails & controls**from the left pane.Select the

**Content filters**tab, then select**Create content filter**.On the

**Basic information**page, enter a name for the content filter.For

**Connection**, select the connection to the**Foundry Tools**resource that is connected to your project.Select

**Next**to go to the**Input filter**page.Configure the input filter depending on your requirements. This configuration is applied before the request reaches the model itself.

Select

**Next**to go to the**Output filter**page.Configure the output filter depending on your requirements. This configuration is applied after the model is executed and content is generated.

Select

**Next**to go to the**Connection**page., you have the option to associate model deployments with the created content filter. You can change the associated model deployments at any time.

Select

**Next**to review the filter settings. Then, select**Create filter**.When the deployment completes, the new content filter is applied to the model deployment.


## Account for content filtering in your code

When you apply content filtering to your model deployment, the service can intercept requests based on the inputs and outputs. If a content filter triggers, the service returns a 400 error code with a description of the rule that triggered the error.

Install the package `azure-ai-inference`

using your package manager, like pip:

```
pip install azure-ai-inference
```


Then, you can use the package to consume the model. The following example shows how to create a client to consume chat completions:

```
import os
from azure.ai.inference import ChatCompletionsClient
from azure.core.credentials import AzureKeyCredential
client = ChatCompletionsClient(
endpoint="https://<resource>.services.ai.azure.com/models",
credential=AzureKeyCredential(os.environ["AZURE_INFERENCE_CREDENTIAL"]),
)
```


Explore our [samples](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/ai/azure-ai-inference/samples) and read the [API reference documentation](https://aka.ms/azsdk/azure-ai-inference/python/reference) to get yourself started.

The following example shows the response for a chat completion request that has triggered Guardrails & controls.

```
from azure.ai.inference.models import AssistantMessage, UserMessage, SystemMessage
from azure.core.exceptions import HttpResponseError
try:
response = model.complete(
messages=[
SystemMessage(content="You are an AI assistant that helps people find information."),
UserMessage(content="Chopping tomatoes and cutting them into cubes or wedges are great ways to practice your knife skills."),
]
)
print(response.choices[0].message.content)
except HttpResponseError as ex:
if ex.status_code == 400:
response = json.loads(ex.response._content.decode('utf-8'))
if isinstance(response, dict) and "error" in response:
print(f"Your request triggered an {response['error']['code']} error:\n\t {response['error']['message']}")
else:
raise ex
else:
raise ex
```


## Follow best practices

To address potential harms that are relevant for a specific model, application, and deployment scenario, use an iterative identification process (such as red team testing, stress-testing, and analysis) and a measurement process to inform your content filtering configuration decisions. After you implement mitigations like content filtering, repeat measurement to test effectiveness.

For recommendations and best practices on Responsible AI for Azure OpenAI, grounded in the [Microsoft Responsible AI Standard](https://aka.ms/RAI), see the [Responsible AI Overview for Azure OpenAI](/en-us/azure/ai-foundry/responsible-ai/openai/overview).

The content filtering system integrated into Microsoft Foundry runs alongside Foundry Models. It uses an ensemble of multi-class classification models to detect four categories of harmful content (violence, hate, sexual, and self-harm) at four severity levels (safe, low, medium, and high). It offers optional binary classifiers for detecting jailbreak risk, existing text, and code in public repositories. For more information about content categories, severity levels, and the behavior of the content filtering system, see [the following article](../concepts/content-filter?view=foundry-classic).

The [default content filtering](../concepts/default-safety-policies?view=foundry-classic) configuration filters content at the medium severity threshold for all four harmful categories for both prompts and completions. Content detected at medium or high severity level is filtered out, while content detected at low or safe severity level isn't filtered.

You can configure content filters at the resource level and associate them with one or more deployments.

## Prerequisites

To complete this article, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Foundry](quickstart-github-models?view=foundry-classic).A Foundry resource (formerly known as Azure AI Services resource). For more information, see

[Create a Foundry resource](quickstart-create-resources?view=foundry-classic).

## Add a model deployment with custom content filtering

We recommend creating content filters using either Microsoft Foundry portal or in code using Bicep. Creating custom content filters or applying them to deployments is not supported using the Azure CLI.

## Account for content filtering in your code

When you apply content filtering to your model deployment, the service can intercept requests based on the inputs and outputs. If a content filter triggers, the service returns a 400 error code with a description of the rule that triggered the error.

Install the package `azure-ai-inference`

using your package manager, like pip:

```
pip install azure-ai-inference
```


Then, you can use the package to consume the model. The following example shows how to create a client to consume chat completions:

```
import os
from azure.ai.inference import ChatCompletionsClient
from azure.core.credentials import AzureKeyCredential
client = ChatCompletionsClient(
endpoint="https://<resource>.services.ai.azure.com/models",
credential=AzureKeyCredential(os.environ["AZURE_INFERENCE_CREDENTIAL"]),
)
```


Explore our [samples](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/ai/azure-ai-inference/samples) and read the [API reference documentation](https://aka.ms/azsdk/azure-ai-inference/python/reference) to get yourself started.

The following example shows the response for a chat completion request that has triggered Guardrails & controls.

```
from azure.ai.inference.models import AssistantMessage, UserMessage, SystemMessage
from azure.core.exceptions import HttpResponseError
try:
response = model.complete(
messages=[
SystemMessage(content="You are an AI assistant that helps people find information."),
UserMessage(content="Chopping tomatoes and cutting them into cubes or wedges are great ways to practice your knife skills."),
]
)
print(response.choices[0].message.content)
except HttpResponseError as ex:
if ex.status_code == 400:
response = json.loads(ex.response._content.decode('utf-8'))
if isinstance(response, dict) and "error" in response:
print(f"Your request triggered an {response['error']['code']} error:\n\t {response['error']['message']}")
else:
raise ex
else:
raise ex
```


## Follow best practices

To address potential harms that are relevant for a specific model, application, and deployment scenario, use an iterative identification process (such as red team testing, stress-testing, and analysis) and a measurement process to inform your content filtering configuration decisions. After you implement mitigations like content filtering, repeat measurement to test effectiveness.

For recommendations and best practices on Responsible AI for Azure OpenAI, grounded in the [Microsoft Responsible AI Standard](https://aka.ms/RAI), see the [Responsible AI Overview for Azure OpenAI](/en-us/azure/ai-foundry/responsible-ai/openai/overview).

The content filtering system integrated into Microsoft Foundry runs alongside Foundry Models. It uses an ensemble of multi-class classification models to detect four categories of harmful content (violence, hate, sexual, and self-harm) at four severity levels (safe, low, medium, and high). It offers optional binary classifiers for detecting jailbreak risk, existing text, and code in public repositories. For more information about content categories, severity levels, and the behavior of the content filtering system, see [the following article](../concepts/content-filter?view=foundry-classic).

The [default content filtering](../concepts/default-safety-policies?view=foundry-classic) configuration filters content at the medium severity threshold for all four harmful categories for both prompts and completions. Content detected at medium or high severity level is filtered out, while content detected at low or safe severity level isn't filtered.

You can configure content filters at the resource level and associate them with one or more deployments.

## Prerequisites

To complete this article, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Foundry](quickstart-github-models?view=foundry-classic).A Foundry resource (formerly known as Azure AI Services resource). For more information, see

[Create a Foundry resource](quickstart-create-resources?view=foundry-classic).

Install the

[Azure CLI](/en-us/cli/azure/).Identify the following information:

Your Azure subscription ID.

Your Foundry Tools resource name.

The resource group where you deployed the Foundry Tools resource.

The model name, provider, version, and SKU you want to deploy. You can use the Microsoft Foundry portal or the Azure CLI to find this information. In this example, deploy the following model:

**Model name:**:`Phi-4-mini-instruct`

**Provider**:`Microsoft`

**Version**:`1`

**Deployment type**: Global standard


## Add a model deployment with custom content filtering

Use the template

`ai-services-content-filter-template.bicep`

to describe the content filter policy:**ai-services-content-filter-template.bicep**`@description('Name of the Azure AI Services account where the policy will be created') param accountName string @description('Name of the policy to be created') param policyName string @allowed(['Asynchronous_filter', 'Blocking', 'Default', 'Deferred']) param mode string = 'Default' @description('Base policy to be used for the new policy') param basePolicyName string = 'Microsoft.DefaultV2' param contentFilters array = [ { name: 'Violence' severityThreshold: 'Medium' blocking: true enabled: true source: 'Prompt' } { name: 'Hate' severityThreshold: 'Medium' blocking: true enabled: true source: 'Prompt' } { name: 'Sexual' severityThreshold: 'Medium' blocking: true enabled: true source: 'Prompt' } { name: 'Selfharm' severityThreshold: 'Medium' blocking: true enabled: true source: 'Prompt' } { name: 'Jailbreak' blocking: true enabled: true source: 'Prompt' } { name: 'Indirect Attack' blocking: true enabled: true source: 'Prompt' } { name: 'Profanity' blocking: true enabled: true source: 'Prompt' } { name: 'Violence' severityThreshold: 'Medium' blocking: true enabled: true source: 'Completion' } { name: 'Hate' severityThreshold: 'Medium' blocking: true enabled: true source: 'Completion' } { name: 'Sexual' severityThreshold: 'Medium' blocking: true enabled: true source: 'Completion' } { name: 'Selfharm' severityThreshold: 'Medium' blocking: true enabled: true source: 'Completion' } { name: 'Protected Material Text' blocking: true enabled: true source: 'Completion' } { name: 'Protected Material Code' blocking: false enabled: true source: 'Completion' } { name: 'Profanity' blocking: true enabled: true source: 'Completion' } ] resource raiPolicy 'Microsoft.CognitiveServices/accounts/raiPolicies@2024-06-01-preview' = { name: '${accountName}/${policyName}' properties: { mode: mode basePolicyName: basePolicyName contentFilters: contentFilters } }`

Use the template

`ai-services-deployment-template.bicep`

to describe model deployments:**ai-services-deployment-template.bicep**`@description('Name of the Azure AI services account') param accountName string @description('Name of the model to deploy') param modelName string @description('Version of the model to deploy') param modelVersion string @allowed([ 'AI21 Labs' 'Cohere' 'Core42' 'DeepSeek' 'xAI' 'Meta' 'Microsoft' 'Mistral AI' 'OpenAI' ]) @description('Model provider') param modelPublisherFormat string @allowed([ 'GlobalStandard' 'DataZoneStandard' 'Standard' 'GlobalProvisioned' 'Provisioned' ]) @description('Model deployment SKU name') param skuName string = 'GlobalStandard' @description('Content filter policy name') param contentFilterPolicyName string = 'Microsoft.DefaultV2' @description('Model deployment capacity') param capacity int = 1 resource modelDeployment 'Microsoft.CognitiveServices/accounts/deployments@2024-04-01-preview' = { name: '${accountName}/${modelName}' sku: { name: skuName capacity: capacity } properties: { model: { format: modelPublisherFormat name: modelName version: modelVersion } raiPolicyName: contentFilterPolicyName == null ? 'Microsoft.Nill' : contentFilterPolicyName } }`

Create the main deployment definition:

**main.bicep**`param accountName string param modelName string param modelVersion string param modelPublisherFormat string param contentFilterPolicyName string module raiPolicy 'ai-services-content-filter-template.bicep' = { name: 'raiPolicy' scope: resourceGroup(resourceGroupName) params: { accountName: accountName policyName: contentFilterPolicyName } } module modelDeployment 'ai-services-deployment-template.bicep' = { name: 'modelDeployment' scope: resourceGroup(resourceGroupName) params: { accountName: accountName modelName: modelName modelVersion: modelVersion modelPublisherFormat: modelPublisherFormat contentFilterPolicyName: contentFilterPolicyName } dependsOn: [ raiPolicy ] }`

Run the deployment:

`RESOURCE_GROUP="<resource-group-name>" ACCOUNT_NAME="<azure-ai-model-inference-name>" MODEL_NAME="Phi-4-mini-instruct" PROVIDER="Microsoft" VERSION=1 RAI_POLICY_NAME="custom-policy" az deployment group create \ --resource-group $RESOURCE_GROUP \ --template-file main.bicep \ --parameters accountName=$ACCOUNT_NAME raiPolicyName=$RAI_POLICY_NAME modelName=$MODEL_NAME modelVersion=$VERSION modelPublisherFormat=$PROVIDER`


## Account for content filtering in your code

When you apply content filtering to your model deployment, the service can intercept requests based on the inputs and outputs. If a content filter triggers, the service returns a 400 error code with a description of the rule that triggered the error.

Install the package `azure-ai-inference`

using your package manager, like pip:

```
pip install azure-ai-inference
```


Then, you can use the package to consume the model. The following example shows how to create a client to consume chat completions:

```
import os
from azure.ai.inference import ChatCompletionsClient
from azure.core.credentials import AzureKeyCredential
client = ChatCompletionsClient(
endpoint="https://<resource>.services.ai.azure.com/models",
credential=AzureKeyCredential(os.environ["AZURE_INFERENCE_CREDENTIAL"]),
)
```


Explore our [samples](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/ai/azure-ai-inference/samples) and read the [API reference documentation](https://aka.ms/azsdk/azure-ai-inference/python/reference) to get yourself started.

The following example shows the response for a chat completion request that has triggered Guardrails & controls.

```
from azure.ai.inference.models import AssistantMessage, UserMessage, SystemMessage
from azure.core.exceptions import HttpResponseError
try:
response = model.complete(
messages=[
SystemMessage(content="You are an AI assistant that helps people find information."),
UserMessage(content="Chopping tomatoes and cutting them into cubes or wedges are great ways to practice your knife skills."),
]
)
print(response.choices[0].message.content)
except HttpResponseError as ex:
if ex.status_code == 400:
response = json.loads(ex.response._content.decode('utf-8'))
if isinstance(response, dict) and "error" in response:
print(f"Your request triggered an {response['error']['code']} error:\n\t {response['error']['message']}")
else:
raise ex
else:
raise ex
```


## Follow best practices

To address potential harms that are relevant for a specific model, application, and deployment scenario, use an iterative identification process (such as red team testing, stress-testing, and analysis) and a measurement process to inform your content filtering configuration decisions. After you implement mitigations like content filtering, repeat measurement to test effectiveness.

For recommendations and best practices on Responsible AI for Azure OpenAI, grounded in the [Microsoft Responsible AI Standard](https://aka.ms/RAI), see the [Responsible AI Overview for Azure OpenAI](/en-us/azure/ai-foundry/responsible-ai/openai/overview).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/how-to/use-image-embeddings -->

# How to generate image embeddings with Microsoft Foundry Models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

This article explains how to use image embeddings API with Microsoft Foundry Models.

## Prerequisites

To use embedding models in your application, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Microsoft Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry project. This kind of project is managed under a Foundry resource. If you don't have a Foundry project, see

[Create a project for Foundry (Foundry projects)](../../how-to/create-projects?view=foundry-classic).The endpoint's URL.

The endpoint's key (if you choose to use API key for authentication).


Install the

[Azure AI inference package for Python](https://aka.ms/azsdk/azure-ai-inference/python/reference)with the following command:`pip install -U azure-ai-inference`


An image embeddings model deployment. If you don't have one, read

[Add and configure Foundry Models](create-model-deployments?view=foundry-classic)to add an embeddings model to your resource.- This example uses
`Cohere-embed-v3-english`

from Cohere.

- This example uses

## Use image embeddings

First, create the client to consume the model. The following code uses an endpoint URL and key that are stored in environment variables.

```
import os
from azure.ai.inference import ImageEmbeddingsClient
from azure.core.credentials import AzureKeyCredential
client = ImageEmbeddingsClient(
endpoint="https://<resource>.services.ai.azure.com/models",
credential=AzureKeyCredential(os.environ["AZURE_INFERENCE_CREDENTIAL"]),
model="Cohere-embed-v3-english"
)
```


If you configured the resource to with **Microsoft Entra ID** support, you can use the following code snippet to create a client.

```
import os
from azure.ai.inference import ImageEmbeddingsClient
from azure.identity import DefaultAzureCredential
client = ImageEmbeddingsClient(
endpoint="https://<resource>.services.ai.azure.com/models",
credential=DefaultAzureCredential(),
model="Cohere-embed-v3-english"
)
```


### Create embeddings

To create image embeddings, you need to pass the image data as part of your request. Image data should be in PNG format and encoded as base64.

```
from azure.ai.inference.models import ImageEmbeddingInput
image_input= ImageEmbeddingInput.load(image_file="sample1.png", image_format="png")
response = client.embed(
input=[ image_input ],
)
```


Tip

When creating a request, take into account the token's input limit for the model. If you need to embed larger portions of text, you would need a chunking strategy.

The response is as follows, where you can see the model's usage statistics:

```
import numpy as np
for embed in response.data:
print("Embedding of size:", np.asarray(embed.embedding).shape)
print("Model:", response.model)
print("Usage:", response.usage)
```


Important

Computing embeddings in batches may not be supported for all the models. For example, for `Cohere-embed-v3-english`

model, you need to send one image at a time.

#### Embedding images and text pairs

Some models can generate embeddings from images and text pairs. In this case, you can use the `image`

and `text`

fields in the request to pass the image and text to the model. The following example shows how to create embeddings for images and text pairs:

```
text_image_input= ImageEmbeddingInput.load(image_file="sample1.png", image_format="png")
text_image_input.text = "A cute baby sea otter"
response = client.embed(
input=[ text_image_input ],
)
```


#### Create different types of embeddings

Some models can generate multiple embeddings for the same input depending on how you plan to use them. This capability allows you to retrieve more accurate embeddings for RAG patterns.

The following example shows how to create embeddings that are used to create an embedding for a document that will be stored in a vector database:

```
from azure.ai.inference.models import EmbeddingInputType
response = client.embed(
input=[ image_input ],
input_type=EmbeddingInputType.DOCUMENT,
)
```


When you work on a query to retrieve such a document, you can use the following code snippet to create the embeddings for the query and maximize the retrieval performance.

```
from azure.ai.inference.models import EmbeddingInputType
response = client.embed(
input=[ image_input ],
input_type=EmbeddingInputType.QUERY,
)
```


Notice that not all the embedding models support indicating the input type in the request and on those cases a 422 error is returned.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

This article explains how to use image embeddings API with Microsoft Foundry Models.

## Prerequisites

To use embedding models in your application, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Microsoft Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry project. This kind of project is managed under a Foundry resource. If you don't have a Foundry project, see

[Create a project for Foundry (Foundry projects)](../../how-to/create-projects?view=foundry-classic).The endpoint's URL.

The endpoint's key (if you choose to use API key for authentication).


Install the

[Azure Inference library for JavaScript](https://aka.ms/azsdk/azure-ai-inference/javascript/reference)with the following command:`npm install @azure-rest/ai-inference npm install @azure/core-auth npm install @azure/identity`

If you are using Node.js, you can configure the dependencies in

**package.json**:**package.json**`{ "name": "main_app", "version": "1.0.0", "description": "", "main": "app.js", "type": "module", "dependencies": { "@azure-rest/ai-inference": "1.0.0-beta.6", "@azure/core-auth": "1.9.0", "@azure/core-sse": "2.2.0", "@azure/identity": "4.8.0" } }`

Import the following:

`import ModelClient from "@azure-rest/ai-inference"; import { isUnexpected } from "@azure-rest/ai-inference"; import { createSseStream } from "@azure/core-sse"; import { AzureKeyCredential } from "@azure/core-auth"; import { DefaultAzureCredential } from "@azure/identity";`


An image embeddings model deployment. If you don't have one read

[Add and configure Foundry Models](create-model-deployments?view=foundry-classic)to add an embeddings model to your resource.- This example uses
`Cohere-embed-v3-english`

from Cohere.

- This example uses

## Use image embeddings

First, create the client to consume the model. The following code uses an endpoint URL and key that are stored in environment variables.

```
const client = ModelClient(
"https://<resource>.services.ai.azure.com/models",
new AzureKeyCredential(process.env.AZURE_INFERENCE_CREDENTIAL)
);
```


If you've configured the resource with **Microsoft Entra ID** support, you can use the following code snippet to create a client.

```
const clientOptions = { credentials: { "https://cognitiveservices.azure.com" } };
const client = ModelClient(
"https://<resource>.services.ai.azure.com/models",
new DefaultAzureCredential()
clientOptions,
);
```


### Create embeddings

To create image embeddings, you need to pass the image data as part of your request. Image data should be in PNG format and encoded as base64.

```
var image_path = "sample1.png";
var image_data = fs.readFileSync(image_path);
var image_data_base64 = Buffer.from(image_data).toString("base64");
var response = await client.path("/images/embeddings").post({
body: {
input: [ { image: image_data_base64 } ],
model: "Cohere-embed-v3-english",
}
});
```


Tip

When creating a request, take into account the token's input limit for the model. If you need to embed larger portions of text, you would need a chunking strategy.

The response is as follows, where you can see the model's usage statistics:

```
if (isUnexpected(response)) {
throw response.body.error;
}
console.log(response.embedding);
console.log(response.body.model);
console.log(response.body.usage);
```


Important

Computing embeddings in batches may not be supported for all the models. For example, for `Cohere-embed-v3-english`

model, you need to send one image at a time.

#### Embedding images and text pairs

Some models can generate embeddings from images and text pairs. In this case, you can use the `image`

and `text`

fields in the request to pass the image and text to the model. The following example shows how to create embeddings for images and text pairs:

```
var image_path = "sample1.png";
var image_data = fs.readFileSync(image_path);
var image_data_base64 = Buffer.from(image_data).toString("base64");
var response = await client.path("/images/embeddings").post({
body: {
input: [
{
text: "A cute baby sea otter",
image: image_data_base64
}
],
model: "Cohere-embed-v3-english",
}
});
```


#### Create different types of embeddings

Some models can generate multiple embeddings for the same input depending on how you plan to use them. This capability allows you to retrieve more accurate embeddings for RAG patterns.

The following example shows how to create embeddings that are used to create an embedding for a document that will be stored in a vector database:

```
var response = await client.path("/images/embeddings").post({
body: {
input: [ { image: image_data_base64 } ],
input_type: "document",
model: "Cohere-embed-v3-english",
}
});
```


When you work on a query to retrieve such a document, you can use the following code snippet to create the embeddings for the query and maximize the retrieval performance.

```
var response = await client.path("/images/embeddings").post({
body: {
input: [ { image: image_data_base64 } ],
input_type: "query",
model: "Cohere-embed-v3-english",
}
});
```


Notice that not all the embedding models support indicating the input type in the request and on those cases a 422 error is returned.

Note

Using image embeddings is only supported using Python, JavaScript, C#, or REST requests.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

This article explains how to use image embeddings API with Microsoft Foundry Models.

## Prerequisites

To use embedding models in your application, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Microsoft Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry project. This kind of project is managed under a Foundry resource. If you don't have a Foundry project, see

[Create a project for Foundry (Foundry projects)](../../how-to/create-projects?view=foundry-classic).The endpoint's URL.

The endpoint's key (if you choose to use API key for authentication).


Install the

[Azure AI inference package](https://aka.ms/azsdk/azure-ai-inference/python/reference)with the following command:`dotnet add package Azure.AI.Inference --prerelease`

If you are using Entra ID, you also need the following package:

`dotnet add package Azure.Identity`


An image embeddings model deployment. If you don't have one, read

[Add and configure Foundry Models](create-model-deployments?view=foundry-classic)to add an embeddings model to your resource.- This example uses
`Cohere-embed-v3-english`

from Cohere.

- This example uses

## Use image embeddings

First, create the client to consume the model. The following code uses an endpoint URL and key that are stored in environment variables.

```
ImageEmbeddingsClient client = new ImageEmbeddingsClient(
new Uri("https://<resource>.services.ai.azure.com/models"),
new AzureKeyCredential(Environment.GetEnvironmentVariable("AZURE_INFERENCE_CREDENTIAL"))
);
```


If you configured the resource with **Microsoft Entra ID** support, you can use the following code snippet to create a client. Notice that `includeInteractiveCredentials`

is set to `true`

only for demonstration purposes so authentication can happen using the web browser. For production workloads, you should remove the parameter.

```
TokenCredential credential = new DefaultAzureCredential(includeInteractiveCredentials: true);
AzureAIInferenceClientOptions clientOptions = new AzureAIInferenceClientOptions();
BearerTokenAuthenticationPolicy tokenPolicy = new BearerTokenAuthenticationPolicy(credential, new string[] { "https://cognitiveservices.azure.com/.default" });
clientOptions.AddPolicy(tokenPolicy, HttpPipelinePosition.PerRetry);
ImageEmbeddingsClient client = new ImageEmbeddingsClient(
new Uri("https://<resource>.services.ai.azure.com/models"),
credential,
clientOptions
);
```


### Create embeddings

To create image embeddings, you need to pass the image data as part of your request. Image data should be in PNG format and encoded as base64.

```
List<ImageEmbeddingInput> input = new List<ImageEmbeddingInput>
{
ImageEmbeddingInput.Load(imageFilePath:"sampleImage.png", imageFormat:"png")
};
var requestOptions = new ImageEmbeddingsOptions()
{
Input = input,
Model = "Cohere-embed-v3-english"
};
Response<EmbeddingsResult> response = client.Embed(requestOptions);
```


Tip

When creating a request, take into account the token's input limit for the model. If you need to embed larger portions of text, you would need a chunking strategy.

The response is as follows, where you can see the model's usage statistics:

```
foreach (EmbeddingItem item in response.Value.Data)
{
List<float> embedding = item.Embedding.ToObjectFromJson<List<float>>();
Console.WriteLine($"Index: {item.Index}, Embedding: <{string.Join(", ", embedding)}>");
}
```


Important

Computing embeddings in batches might not be supported for all the models. For example, for `Cohere-embed-v3-english`

model, you need to send one image at a time.

#### Embedding images and text pairs

Some models can generate embeddings from images and text pairs. In this case, you can use the `image`

and `text`

fields in the request to pass the image and text to the model. The following example shows how to create embeddings for images and text pairs:

```
var image_input = ImageEmbeddingInput.Load(imageFilePath:"sampleImage.png", imageFormat:"png")
image_input.text = "A cute baby sea otter"
var requestOptions = new ImageEmbeddingsOptions()
{
Input = new List<ImageEmbeddingInput>
{
image_input
},
Model = "Cohere-embed-v3-english"
};
Response<EmbeddingsResult> response = client.Embed(requestOptions);
```


#### Create different types of embeddings

Some models can generate multiple embeddings for the same input depending on how you plan to use them. This capability allows you to retrieve more accurate embeddings for RAG patterns.

The following example shows how to create embeddings for a document that will be stored in a vector database:

```
var requestOptions = new EmbeddingsOptions()
{
Input = image_input,
InputType = EmbeddingInputType.DOCUMENT,
Model = "Cohere-embed-v3-english"
};
Response<EmbeddingsResult> response = client.Embed(requestOptions);
```


When you work on a query to retrieve such a document, you can use the following code snippet to create the embeddings for the query and maximize the retrieval performance.

```
var requestOptions = new EmbeddingsOptions()
{
Input = image_input,
InputType = EmbeddingInputType.QUERY,
Model = "Cohere-embed-v3-english"
};
Response<EmbeddingsResult> response = client.Embed(requestOptions);
```


Notice that not all the embedding models support indicating the input type in the request and on those cases a 422 error is returned.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

This article explains how to use image embeddings API with Microsoft Foundry Models.

## Prerequisites

To use embedding models in your application, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Microsoft Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry project. This kind of project is managed under a Foundry resource. If you don't have a Foundry project, see

[Create a project for Foundry (Foundry projects)](../../how-to/create-projects?view=foundry-classic).The endpoint's URL.

The endpoint's key (if you choose to use API key for authentication).


An image embeddings model deployment. If you don't have one read

[Add and configure Foundry Models](create-model-deployments?view=foundry-classic)to add an embeddings model to your resource.- This example uses
`Cohere-embed-v3-english`

from Cohere.

- This example uses

## Use image embeddings

To use the text embeddings, use the route `/images/embeddings`

appended to your base URL along with your credential indicated in `api-key`

. `Authorization`

header is also supported with the format `Bearer <key>`

.

```
POST https://<resource>.services.ai.azure.com/models/images/embeddings?api-version=2024-05-01-preview
Content-Type: application/json
api-key: <key>
```


If you have configured the resource with **Microsoft Entra ID** support, pass you token in the `Authorization`

header with the format `Bearer <token>`

. Use scope `https://cognitiveservices.azure.com/.default`

.

```
POST https://<resource>.services.ai.azure.com/models/images/embeddings?api-version=2024-05-01-preview
Content-Type: application/json
Authorization: Bearer <token>
```


Using Microsoft Entra ID may require additional configuration in your resource to grant access. Learn how to [configure key-less authentication with Microsoft Entra ID](configure-entra-id?view=foundry-classic).

### Create embeddings

To create image embeddings, you need to pass the image data as part of your request. Image data should be in PNG format and encoded as base64.

```
{
"model": "Cohere-embed-v3-english",
"input": [
{
"image": "data:image/png;base64,iVBORw0KGgoAAAANSUh..."
}
]
}
```


Tip

When creating a request, take into account the token's input limit for the model. If you need to embed larger portions of text, you would need a chunking strategy.

The response is as follows, where you can see the model's usage statistics:

```
{
"id": "0ab1234c-d5e6-7fgh-i890-j1234k123456",
"object": "list",
"data": [
{
"index": 0,
"object": "embedding",
"embedding": [
0.017196655,
// ...
-0.000687122,
-0.025054932,
-0.015777588
]
}
],
"model": "Cohere-embed-v3-english",
"usage": {
"prompt_tokens": 9,
"completion_tokens": 0,
"total_tokens": 9
}
}
```


Important

Computing embeddings in batches may not be supported for all the models. For example, for `Cohere-embed-v3-english`

model, you need to send one image at a time.

#### Embedding images and text pairs

Some models can generate embeddings from images and text pairs. In this case, you can use the `image`

and `text`

fields in the request to pass the image and text to the model. The following example shows how to create embeddings for images and text pairs:

```
{
"model": "Cohere-embed-v3-english",
"input": [
{
"image": "data:image/png;base64,iVBORw0KGgoAAAANSUh...",
"text": "A photo of a cat"
}
]
}
```


#### Create different types of embeddings

Some models can generate multiple embeddings for the same input depending on how you plan to use them. This capability allows you to retrieve more accurate embeddings for RAG patterns.

The following example shows how to create embeddings that are used to create an embedding for a document that will be stored in a vector database:

```
{
"model": "Cohere-embed-v3-english",
"input": [
{
"image": "data:image/png;base64,iVBORw0KGgoAAAANSUh..."
}
],
"input_type": "document"
}
```


When you work on a query to retrieve such a document, you can use the following code snippet to create the embeddings for the query and maximize the retrieval performance.

```
{
"model": "Cohere-embed-v3-english",
"input": [
{
"image": "data:image/png;base64,iVBORw0KGgoAAAANSUh..."
}
],
"input_type": "query"
}
```


Notice that not all the embedding models support indicating the input type in the request and on those cases a 422 error is returned.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/how-to/inference -->

# Endpoints for Microsoft Foundry Models

Microsoft Foundry Models enables you to access the most powerful models from leading model providers through a single endpoint and set of credentials. This capability lets you switch between models and use them in your application without changing any code.

This article explains how the Foundry services organize models and how to use the inference endpoint to access them.

A Foundry resource can have many model deployments. You only pay for inference performed on model deployments. Deployments are Azure resources, so they're subject to Azure policies.

## Endpoints

Foundry services provide multiple endpoints depending on the type of work you want to perform:

## Azure AI inference endpoint

The **Azure AI inference endpoint**, usually of the form `https://<resource-name>.services.ai.azure.com/models`

, enables you to use a single endpoint with the same authentication and schema to generate inference for the deployed models in the resource. All Foundry Models support this capability. This endpoint follows the [Azure AI Model Inference API](../../model-inference/reference/reference-model-inference-api?view=foundry-classic), which supports the following modalities:

- Text embeddings
- Image embeddings
- Chat completions

### Routing

The inference endpoint routes requests to a specific deployment by matching the `name`

parameter in the request to the name of the deployment. This setup means that *deployments work as an alias for a model under certain configurations*. This flexibility lets you deploy a model multiple times in the service but with different configurations if needed.

[
](../media/endpoint/endpoint-routing.png?view=foundry-classic#lightbox)

For example, if you create a deployment named `Mistral-large`

, you can invoke that deployment as follows:

Install the package `azure-ai-inference`

using your package manager, like pip:

```
pip install azure-ai-inference
```


Then, you can use the package to consume the model. The following example shows how to create a client to consume chat completions:

```
import os
from azure.ai.inference import ChatCompletionsClient
from azure.core.credentials import AzureKeyCredential
client = ChatCompletionsClient(
endpoint="https://<resource>.services.ai.azure.com/models",
credential=AzureKeyCredential(os.environ["AZURE_INFERENCE_CREDENTIAL"]),
)
```


Explore our [samples](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/ai/azure-ai-inference/samples) and read the [API reference documentation](https://aka.ms/azsdk/azure-ai-inference/python/reference) to get yourself started.

Install the package `@azure-rest/ai-inference`

using npm:

```
npm install @azure-rest/ai-inference
```


Then, you can use the package to consume the model. The following example shows how to create a client to consume chat completions:

```
import ModelClient from "@azure-rest/ai-inference";
import { isUnexpected } from "@azure-rest/ai-inference";
import { AzureKeyCredential } from "@azure/core-auth";
const client = new ModelClient(
"https://<resource>.services.ai.azure.com/models",
new AzureKeyCredential(process.env.AZURE_INFERENCE_CREDENTIAL)
);
```


Explore our [samples](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/ai/ai-inference-rest/samples) and read the [API reference documentation](/en-us/javascript/api/@azure-rest/ai-inference) to get yourself started.

Install the Azure AI inference library with the following command:

```
dotnet add package Azure.AI.Inference --prerelease
```


Import the following namespaces:

```
using Azure;
using Azure.Identity;
using Azure.AI.Inference;
```


Then, you can use the package to consume the model. The following example shows how to create a client to consume chat completions:

```
ChatCompletionsClient client = new ChatCompletionsClient(
new Uri("https://<resource>.services.ai.azure.com/models"),
new AzureKeyCredential(Environment.GetEnvironmentVariable("AZURE_INFERENCE_CREDENTIAL"))
);
```


Explore our [samples](https://aka.ms/azsdk/azure-ai-inference/csharp/samples) and read the [API reference documentation](https://aka.ms/azsdk/azure-ai-inference/csharp/reference) to get yourself started.

Add the package to your project:

```
<dependency>
<groupId>com.azure</groupId>
<artifactId>azure-ai-inference</artifactId>
<version>1.0.0-beta.1</version>
</dependency>
```


Then, you can use the package to consume the model. The following example shows how to create a client to consume chat completions:

```
ChatCompletionsClient client = new ChatCompletionsClientBuilder()
.credential(new AzureKeyCredential("{key}"))
.endpoint("https://<resource>.services.ai.azure.com/models")
.buildClient();
```


Explore our [samples](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/ai/azure-ai-inference/src/samples) and read the [API reference documentation](https://aka.ms/azsdk/azure-ai-inference/java/reference) to get yourself started.

Use the reference section to explore the API design and which parameters are available. For example, the reference section for [Chat completions](../../model-inference/reference/reference-model-inference-chat-completions?view=foundry-classic) details how to use the route `/chat/completions`

to generate predictions based on chat-formatted instructions. Notice that the path `/models`

is included to the root of the URL:

**Request**

```
POST https://<resource>.services.ai.azure.com/models/chat/completions?api-version=2024-05-01-preview
api-key: <api-key>
Content-Type: application/json
```


For a chat model, you can create a request as follows:

```
from azure.ai.inference.models import SystemMessage, UserMessage
response = client.complete(
messages=[
SystemMessage(content="You are a helpful assistant."),
UserMessage(content="Explain Riemann's conjecture in 1 paragraph"),
],
model="mistral-large"
)
print(response.choices[0].message.content)
```


```
var messages = [
{ role: "system", content: "You are a helpful assistant" },
{ role: "user", content: "Explain Riemann's conjecture in 1 paragraph" },
];
var response = await client.path("/chat/completions").post({
body: {
messages: messages,
model: "mistral-large"
}
});
console.log(response.body.choices[0].message.content)
```


```
requestOptions = new ChatCompletionsOptions()
{
Messages = {
new ChatRequestSystemMessage("You are a helpful assistant."),
new ChatRequestUserMessage("Explain Riemann's conjecture in 1 paragraph")
},
Model = "mistral-large"
};
response = client.Complete(requestOptions);
Console.WriteLine($"Response: {response.Value.Content}");
```


```
List<ChatRequestMessage> chatMessages = new ArrayList<>();
chatMessages.add(new ChatRequestSystemMessage("You are a helpful assistant"));
chatMessages.add(new ChatRequestUserMessage("Explain Riemann's conjecture in 1 paragraph"));
ChatCompletions chatCompletions = client.complete(new ChatCompletionsOptions(chatMessages));
for (ChatChoice choice : chatCompletions.getChoices()) {
ChatResponseMessage message = choice.getMessage();
System.out.println("Response:" + message.getContent());
}
```


**Request**

```
POST https://<resource>.services.ai.azure.com/models/chat/completions?api-version=2024-05-01-preview
api-key: <api-key>
Content-Type: application/json
```


```
{
"messages": [
{
"role": "system",
"content": "You are a helpful assistant"
},
{
"role": "user",
"content": "Explain Riemann's conjecture in 1 paragraph"
}
],
"model": "mistral-large"
}
```


If you specify a model name that doesn't match any model deployment, you get an error that the model doesn't exist. You control which models are available to users by creating model deployments. For more information, see [add and configure model deployments](../../model-inference/how-to/create-model-deployments?view=foundry-classic).

Install the package `openai`

using your package manager, like pip:

```
pip install openai --upgrade
```


Then, you can use the package to consume the model. The following example shows how to create a client to consume chat completions:

```
import os
from openai import AzureOpenAI
client = AzureOpenAI(
azure_endpoint = "https://<resource>.services.ai.azure.com"
api_key=os.getenv("AZURE_INFERENCE_CREDENTIAL"),
api_version="2024-10-21",
)
```


Install the package `openai`

using npm:

```
npm install openai
```


Then, you can use the package to consume the model. The following example shows how to create a client to consume chat completions:

```
import { AzureKeyCredential } from "@azure/openai";
const endpoint = "https://<resource>.services.ai.azure.com";
const apiKey = new AzureKeyCredential(process.env.AZURE_INFERENCE_CREDENTIAL);
const apiVersion = "2024-10-21"
const client = new AzureOpenAI({
endpoint,
apiKey,
apiVersion,
"deepseek-v3-0324"
});
```


Here, `deepseek-v3-0324`

is the name of a model deployment in the Microsoft Foundry resource.

Install the OpenAI library with the following command:

```
dotnet add package Azure.AI.OpenAI --prerelease
```


You can use the package to consume the model. The following example shows how to create a client to consume chat completions:

```
AzureOpenAIClient client = new(
new Uri("https://<resource>.services.ai.azure.com"),
new ApiKeyCredential(Environment.GetEnvironmentVariable("AZURE_INFERENCE_CREDENTIAL"))
);
```


Add the package to your project:

```
<dependency>
<groupId>com.azure</groupId>
<artifactId>azure-ai-openai</artifactId>
<version>1.0.0-beta.16</version>
</dependency>
```


Then, you can use the package to consume the model. The following example shows how to create a client to consume chat completions:

```
OpenAIClient client = new OpenAIClientBuilder()
.credential(new AzureKeyCredential("{key}"))
.endpoint("https://<resource>.services.ai.azure.com")
.buildClient();
```


Use the reference section to explore the API design and which parameters are available. For example, the reference section for Chat completions details how to use the route `/chat/completions`

to generate predictions based on chat-formatted instructions:

**Request**

```
POST https://<resource>.services.ai.azure.com/openai/deployments/deepseek-v3-0324/chat/completions?api-version=2024-10-21
api-key: <api-key>
Content-Type: application/json
```


Here, `deepseek-v3-0324`

is the name of a model deployment in the Foundry resource.

```
response = client.chat.completions.create(
model="deepseek-v3-0324", # Replace with your model deployment name.
messages=[
{"role": "system", "content": "You are a helpful assistant."},
{"role": "user", "content": "Explain Riemann's conjecture in 1 paragraph"}
]
)
print(response.model_dump_json(indent=2)
```


```
var messages = [
{ role: "system", content: "You are a helpful assistant" },
{ role: "user", content: "Explain Riemann's conjecture in 1 paragraph" },
];
const response = await client.chat.completions.create({ messages, model: "deepseek-v3-0324" });
console.log(response.choices[0].message.content)
```


```
ChatCompletion response = chatClient.CompleteChat(
[
new SystemChatMessage("You are a helpful assistant."),
new UserChatMessage("Explain Riemann's conjecture in 1 paragraph"),
]);
Console.WriteLine($"{response.Role}: {response.Content[0].Text}");
```


```
List<ChatRequestMessage> chatMessages = new ArrayList<>();
chatMessages.add(new ChatRequestSystemMessage("You are a helpful assistant"));
chatMessages.add(new ChatRequestUserMessage("Explain Riemann's conjecture in 1 paragraph"));
ChatCompletions chatCompletions = client.getChatCompletions("deepseek-v3-0324",
new ChatCompletionsOptions(chatMessages));
System.out.printf("Model ID=%s is created at %s.%n", chatCompletions.getId(), chatCompletions.getCreatedAt());
for (ChatChoice choice : chatCompletions.getChoices()) {
ChatResponseMessage message = choice.getMessage();
System.out.printf("Index: %d, Chat Role: %s.%n", choice.getIndex(), message.getRole());
System.out.println("Message:");
System.out.println(message.getContent());
}
```


Here, `deepseek-v3-0324`

is the name of a model deployment in the Microsoft Foundry resource.

**Request**

```
POST https://<resource>.services.ai.azure.com/openai/deployments/deepseek-v3-0324/chat/completions?api-version=2024-10-21
api-key: <api-key>
Content-Type: application/json
```


```
{
"messages": [
{
"role": "system",
"content": "You are a helpful assistant"
},
{
"role": "user",
"content": "Explain Riemann's conjecture in 1 paragraph"
}
]
}
```


Here, `deepseek-v3-0324`

is the name of a model deployment in the Foundry resource.

Models deployed to Foundry Models in Foundry Tools support keyless authorization by using Microsoft Entra ID. Keyless authorization enhances security, simplifies the user experience, reduces operational complexity, and provides robust compliance support for modern development. It makes keyless authorization a strong choice for organizations adopting secure and scalable identity management solutions.

Install the OpenAI SDK using a package manager like pip:

```
pip install openai
```


For Microsoft Entra ID authentication, also install:

```
pip install azure-identity
```


Use the package to consume the model. The following example shows how to create a client to consume chat completions with Microsoft Entra ID and make a test call to the chat completions endpoint with your model deployment.

Replace `<resource>`

with your Foundry resource name. Find it in the Azure portal or by running `az cognitiveservices account list`

. Replace `DeepSeek-V3.1`

with your actual deployment name.

```
from openai import OpenAI
from azure.identity import DefaultAzureCredential, get_bearer_token_provider
token_provider = get_bearer_token_provider(
DefaultAzureCredential(),
"https://cognitiveservices.azure.com/.default"
)
client = OpenAI(
base_url="https://<resource>.openai.azure.com/openai/v1/",
api_key=token_provider,
)
completion = client.chat.completions.create(
model="DeepSeek-V3.1", # Required: your deployment name
messages=[
{"role": "system", "content": "You are a helpful assistant."},
{"role": "user", "content": "What is Azure AI?"}
]
)
print(completion.choices[0].message.content)
```


Expected output

```
Azure AI is a comprehensive suite of artificial intelligence services and tools from Microsoft that enables developers to build intelligent applications. It includes services for natural language processing, computer vision, speech recognition, and machine learning capabilities.
```


Reference: [OpenAI Python SDK](https://github.com/openai/openai-python) and [DefaultAzureCredential class](/en-us/python/api/azure-identity/azure.identity.defaultazurecredential).

Install the OpenAI SDK:

```
dotnet add package OpenAI
```


For Microsoft Entra ID authentication, also install the `Azure.Identity`

package:

```
dotnet add package Azure.Identity
```


Import the following namespaces:

```
using Azure.Identity;
using OpenAI;
using OpenAI.Chat;
using System.ClientModel.Primitives;
```


Then, use the package to consume the model. The following example shows how to create a client to consume chat completions with Microsoft Entra ID, and then make a test call to the chat completions endpoint with your model deployment.

Replace `<resource>`

with your Foundry resource name (find it in the Azure portal). Replace `gpt-4o-mini`

with your actual deployment name.

```
#pragma warning disable OPENAI001
BearerTokenPolicy tokenPolicy = new(
new DefaultAzureCredential(),
"https://cognitiveservices.azure.com/.default"
);
ChatClient client = new(
model: "gpt-4o-mini", // Your deployment name
authenticationPolicy: tokenPolicy,
options: new OpenAIClientOptions() {
Endpoint = new Uri("https://<resource>.openai.azure.com/openai/v1/")
}
);
ChatCompletion completion = client.CompleteChat(
new SystemChatMessage("You are a helpful assistant."),
new UserChatMessage("What is Azure AI?")
);
Console.WriteLine(completion.Content[0].Text);
```


Expected output:

```
Azure AI is a comprehensive suite of artificial intelligence services and tools from Microsoft that enables developers to build intelligent applications. It includes services for natural language processing, computer vision, speech recognition, and machine learning capabilities.
```


Reference: [OpenAI .NET SDK](https://github.com/openai/openai-dotnet) and [DefaultAzureCredential class](/en-us/dotnet/api/azure.identity.defaultazurecredential).

Install the OpenAI SDK with npm:

```
npm install openai
```


For Microsoft Entra ID authentication, also install:

```
npm install @azure/identity
```


Then, use the package to consume the model. The following example shows how to create a client to consume chat completions with Microsoft Entra ID, and then make a test call to the chat completions endpoint with your model deployment.

Replace `<resource>`

with your Foundry resource name (find it in the Azure portal or by running `az cognitiveservices account list`

). Replace `DeepSeek-V3.1`

with your actual deployment name.

```
import { DefaultAzureCredential, getBearerTokenProvider } from "@azure/identity";
import { OpenAI } from "openai";
const tokenProvider = getBearerTokenProvider(
new DefaultAzureCredential(),
'https://cognitiveservices.azure.com/.default'
);
const client = new OpenAI({
baseURL: "https://<resource>.openai.azure.com/openai/v1/",
apiKey: tokenProvider
});
const completion = await client.chat.completions.create({
model: "DeepSeek-V3.1", // Required: your deployment name
messages: [
{ role: "system", content: "You are a helpful assistant." },
{ role: "user", content: "What is Azure AI?" }
]
});
console.log(completion.choices[0].message.content);
```


Expected output:

```
Azure AI is a comprehensive suite of artificial intelligence services and tools from Microsoft that enables developers to build intelligent applications. It includes services for natural language processing, computer vision, speech recognition, and machine learning capabilities.
```


Reference: [OpenAI Node.js SDK](https://github.com/openai/openai-node) and [DefaultAzureCredential class](/en-us/javascript/api/@azure/identity/defaultazurecredential).

Add the OpenAI SDK to your project. Check the [OpenAI Java GitHub repository](https://github.com/openai/openai-java) for the latest version and installation instructions.

For Microsoft Entra ID authentication, also add:

```
<dependency>
<groupId>com.azure</groupId>
<artifactId>azure-identity</artifactId>
<version>1.18.0</version>
</dependency>
```


Then, use the package to consume the model. The following example shows how to create a client to consume chat completions with Microsoft Entra ID, and then make a test call to the chat completions endpoint with your model deployment.

Replace `<resource>`

with your Foundry resource name (find it in the Azure portal). Replace `DeepSeek-V3.1`

with your actual deployment name.

```
import com.openai.client.OpenAIClient;
import com.openai.client.okhttp.OpenAIOkHttpClient;
import com.azure.identity.DefaultAzureCredential;
import com.azure.identity.DefaultAzureCredentialBuilder;
import com.openai.models.chat.completions.*;
DefaultAzureCredential tokenCredential = new DefaultAzureCredentialBuilder().build();
OpenAIClient client = OpenAIOkHttpClient.builder()
.baseUrl("https://<resource>.openai.azure.com/openai/v1/")
.credential(BearerTokenCredential.create(
AuthenticationUtil.getBearerTokenSupplier(
tokenCredential,
"https://cognitiveservices.azure.com/.default"
)
))
.build();
ChatCompletionCreateParams params = ChatCompletionCreateParams.builder()
.addSystemMessage("You are a helpful assistant.")
.addUserMessage("What is Azure AI?")
.model("DeepSeek-V3.1") // Required: your deployment name
.build();
ChatCompletion completion = client.chat().completions().create(params);
System.out.println(completion.choices().get(0).message().content());
```


Expected output:

```
Azure AI is a comprehensive suite of artificial intelligence services and tools from Microsoft that enables developers to build intelligent applications. It includes services for natural language processing, computer vision, speech recognition, and machine learning capabilities.
```


Reference: [OpenAI Java SDK](https://github.com/openai/openai-java) and [DefaultAzureCredential class](/en-us/java/api/com.azure.identity.defaultazurecredential).

Explore the API design in the reference section to see which parameters are available. Indicate the authentication token in the header `Authorization`

. For example, the [Chat completion](../../openai/latest?view=foundry-classic#create-chat-completion) reference section details how to use the `/chat/completions`

route to generate predictions based on chat-formatted instructions. The path `/models`

is included in the root of the URL:

**Request**

Replace `<resource>`

with your Foundry resource name (find it in the Azure portal or by running `az cognitiveservices account list`

). Replace `MAI-DS-R1`

with your actual deployment name.

The base_url will accept both `https://<resource>.openai.azure.com/openai/v1/`

and `https://<resource>.services.ai.azure.com/openai/v1/`

formats.

```
curl -X POST https://<resource>.openai.azure.com/openai/v1/chat/completions \
-H "Content-Type: application/json" \
-H "Authorization: Bearer $AZURE_OPENAI_AUTH_TOKEN" \
-d '{
"model": "MAI-DS-R1",
"messages": [
{
"role": "system",
"content": "You are a helpful assistant."
},
{
"role": "user",
"content": "Explain what the bitter lesson is?"
}
]
}'
```


**Response**

If authentication is successful, you receive a `200 OK`

response with chat completion results in the response body:

```
{
"id": "chatcmpl-...",
"object": "chat.completion",
"created": 1738368234,
"model": "MAI-DS-R1",
"choices": [
{
"index": 0,
"message": {
"role": "assistant",
"content": "The bitter lesson refers to a key insight in AI research that emphasizes the importance of general-purpose learning methods that leverage computation, rather than human-designed domain-specific approaches. It suggests that methods which scale with increased computation tend to be more effective in the long run."
},
"finish_reason": "stop"
}
],
"usage": {
"prompt_tokens": 28,
"completion_tokens": 52,
"total_tokens": 80
}
}
```


Tokens must be issued with scope `https://cognitiveservices.azure.com/.default`

.

For testing purposes, the easiest way to get a valid token for your user account is to use the Azure CLI. In a console, run the following Azure CLI command:

```
az account get-access-token --resource https://cognitiveservices.azure.com --query "accessToken" --output tsv
```


This command outputs an access token that you can store in the `$AZURE_OPENAI_AUTH_TOKEN`

environment variable.

Reference: [Chat Completions API](../../openai/latest?view=foundry-classic#create-chat-completion)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/how-to/quickstart-create-resources -->

# Create and configure all the resources for Microsoft Foundry Models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

In this article, you learn how to create the resources required to use Microsoft Foundry Models in your projects.

## Understand the resources

Foundry Models is a capability in Foundry Services (formerly known Azure AI Services). You can create model deployments under the resource to consume their predictions. You can also connect the resource to Azure AI Hubs and Projects in Foundry to create intelligent applications if needed. The following picture shows the high level architecture.

Foundry Services don't require AI projects or AI hubs to operate and you can create them to consume flagship models from your applications. However, additional capabilities are available if you **deploy a Foundry project and hub**, including playground, or agents.

The tutorial helps you create:

- A Foundry resource.
- A model deployment for each of the models supported with serverless API deployments.
- (Optionally) A Foundry project and hub.
- (Optionally) A connection between the hub and the models in Foundry.

## Prerequisites

To complete this article, you need:

- An Azure subscription. If you're using
[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Foundry](quickstart-github-models?view=foundry-classic)if that's your case.

## Create the resources

To create a project with a Microsoft Foundry (formerly known Azure AI Services) resource, follow these steps:

Go to

[Foundry portal](https://ai.azure.com/?cid=learnDocs).On the landing page, select

**Create project**.Give the project a name, for example "my-project".

In this tutorial, we create a brand new project under a new AI hub, hence, select

**Create new hub**.Give the hub a name, for example "my-hub" and select

**Next**.The wizard updates with details about the resources that are going to be created. Select

**Azure resources to be created**to see the details.You can see that the following resources are created:

Property Description Resource group The main container for all the resources in Azure. This helps get resources that work together organized. It also helps to have a scope for the costs associated with the entire project. Location The region of the resources that you're creating. Hub The main container for AI projects in Foundry. Hubs promote collaboration and allow you to store information for your projects. Foundry In this tutorial, a new account is created, but Foundry Services can be shared across multiple hubs and projects. Hubs use a connection to the resource to have access to the model deployments available there. To learn how, you can create connections between projects and Foundry to consume Foundry Models you can read [Connect your AI project](configure-project-connection?view=foundry-classic).Select

**Create**. The resources creation process starts.Once completed, your project is ready to be configured.

To use Foundry Models, you need to add model deployments.


## Next steps

You can decide and configure which models are available for inference in your Microsoft Foundry resource. When you configure a model, you can generate predictions from it by specifying its model name or deployment name in your requests. You don't need to make any other changes in your code to use the model.

In this article, you learn how to add a new model to a Foundry Models endpoint.

## Prerequisites

To complete this article, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry project. This kind of project is managed under a Foundry resource (formerly known as Azure AI Services resource). If you don't have a Foundry project, see

[Create a project for Microsoft Foundry](../../how-to/create-projects?view=foundry-classic).[Foundry Models from partners and community](../concepts/models-from-partners?view=foundry-classic)require access to**Azure Marketplace**. Ensure you have the[permissions required to subscribe to model offerings](configure-marketplace?view=foundry-classic).[Foundry Models sold directly by Azure](../concepts/models-sold-directly-by-azure?view=foundry-classic)don't have this requirement.Install the

[Azure CLI](/en-us/cli/azure/)and the`cognitiveservices`

extension for Foundry Tools.`az extension add -n cognitiveservices`

Some of the commands in this tutorial use the

`jq`

tool, which might not be installed on your system. For installation instructions, see[Download](https://stedolan.github.io/jq/download/).`jq`

Identify the following information:

Your Azure subscription ID.

Your Foundry Tools resource name.

The resource group where you deployed the Foundry Tools resource.


## Add models

To add a model, first identify the model that you want to deploy. You can query the available models as follows:

Sign in to your Azure subscription.

`az login`

If you have more than one subscription, select the subscription where your resource is located.

`az account set --subscription $subscriptionId`

Set the following environment variables with the name of the Foundry Tools resource you plan to use and resource group.

`accountName="<ai-services-resource-name>" resourceGroupName="<resource-group>" location="eastus2"`

If you didn't create a Foundry Tools account yet, create one.

`az cognitiveservices account create -n $accountName -g $resourceGroupName --custom-domain $accountName --location $location --kind AIServices --sku S0`

Check which models are available to you and under which SKU. SKUs, also known as

[deployment types](../concepts/deployment-types?view=foundry-classic), define how Azure infrastructure is used to process requests. Models might offer different deployment types. The following command lists all the model definitions available:`az cognitiveservices account list-models \ -n $accountName \ -g $resourceGroupName \ | jq '.[] | { name: .name, format: .format, version: .version, sku: .skus[0].name, capacity: .skus[0].capacity.default }'`

Outputs look as follows:

`{ "name": "Phi-3.5-vision-instruct", "format": "Microsoft", "version": "2", "sku": "GlobalStandard", "capacity": 1 }`

Identify the model you want to deploy. You need the properties

`name`

,`format`

,`version`

, and`sku`

. The property`format`

indicates the provider offering the model. You might also need capacity depending on the type of deployment.Add the model deployment to the resource. The following example adds

`Phi-3.5-vision-instruct`

:`az cognitiveservices account deployment create \ -n $accountName \ -g $resourceGroupName \ --deployment-name Phi-3.5-vision-instruct \ --model-name Phi-3.5-vision-instruct \ --model-version 2 \ --model-format Microsoft \ --sku-capacity 1 \ --sku-name GlobalStandard`

The model is ready to use.


You can deploy the same model multiple times if needed as long as it's under a different deployment name. This capability might be useful if you want to test different configurations for a given model, including content filters.

## Use the model

Deployed models in can be consumed using the [Azure AI model's inference endpoint](../concepts/endpoints?view=foundry-classic) for the resource. When constructing your request, indicate the parameter `model`

and insert the model deployment name you have created. You can programmatically get the URI for the inference endpoint using the following code:

**Inference endpoint**

```
az cognitiveservices account show -n $accountName -g $resourceGroupName | jq '.properties.endpoints["Azure AI Model Inference API"]'
```


To make requests to the Microsoft Foundry Models endpoint, append the route `models`

, for example `https://<resource>.services.ai.azure.com/models`

. You can see the API reference for the endpoint at [Azure AI Model Inference API reference page](https://aka.ms/azureai/modelinference).

**Inference keys**

```
az cognitiveservices account keys list -n $accountName -g $resourceGroupName
```


## Manage deployments

You can see all the deployments available using the CLI:

Run the following command to see all the active deployments:

`az cognitiveservices account deployment list -n $accountName -g $resourceGroupName`

You can see the details of a given deployment:

`az cognitiveservices account deployment show \ --deployment-name "Phi-3.5-vision-instruct" \ -n $accountName \ -g $resourceGroupName`

You can delete a given deployment as follows:

`az cognitiveservices account deployment delete \ --deployment-name "Phi-3.5-vision-instruct" \ -n $accountName \ -g $resourceGroupName`


Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

In this article, you learn how to create the resources required to use Microsoft Foundry Models in your projects.

## Understand the resources

Foundry Models is a capability in Foundry Services (formerly known Azure AI Services). You can create model deployments under the resource to consume their predictions. You can also connect the resource to Azure AI Hubs and Projects in Foundry to create intelligent applications if needed. The following picture shows the high level architecture.

Foundry Services don't require AI projects or AI hubs to operate and you can create them to consume flagship models from your applications. However, additional capabilities are available if you **deploy a Foundry project and hub**, including playground, or agents.

The tutorial helps you create:

- A Foundry resource.
- A model deployment for each of the models supported with serverless API deployments.
- (Optionally) A Foundry project and hub.
- (Optionally) A connection between the hub and the models in Foundry.

## Prerequisites

To complete this article, you need:

- An Azure subscription. If you're using
[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Foundry](quickstart-github-models?view=foundry-classic)if that's your case.

Install the

[Azure CLI](/en-us/cli/azure/).Identify the following information:

- Your Azure subscription ID.


## About this tutorial

The example in this article is based on code samples contained in the [Azure-Samples/azureai-model-inference-bicep](https://github.com/Azure-Samples/azureai-model-inference-bicep) repository. To run the commands locally without having to copy or paste file content, use the following commands to clone the repository and go to the folder for your coding language:

```
git clone https://github.com/Azure-Samples/azureai-model-inference-bicep
```


The files for this example are in:

```
cd azureai-model-inference-bicep/infra
```


## Permissions required to subscribe to Models from Partners and Community

[Foundry Models from partners and community](../concepts/models-from-partners?view=foundry-classic) available for deployment (for example, Cohere models) require Azure Marketplace. Model providers define the license terms and set the price for use of their models using Azure Marketplace.

When deploying third-party models, ensure you have the following permissions in your account:

- On the Azure subscription:
`Microsoft.MarketplaceOrdering/agreements/offers/plans/read`

`Microsoft.MarketplaceOrdering/agreements/offers/plans/sign/action`

`Microsoft.MarketplaceOrdering/offerTypes/publishers/offers/plans/agreements/read`

`Microsoft.Marketplace/offerTypes/publishers/offers/plans/agreements/read`

`Microsoft.SaaS/register/action`


- On the resource group—to create and use the SaaS resource:
`Microsoft.SaaS/resources/read`

`Microsoft.SaaS/resources/write`


## Create the resources

Follow these steps:

Use the template

`modules/ai-services-template.bicep`

to describe your Foundry Tools resource:**modules/ai-services-template.bicep**`@description('Location of the resource.') param location string = resourceGroup().location @description('Name of the Azure AI Services account.') param accountName string @description('The resource model definition representing SKU') param sku string = 'S0' @description('Whether or not to allow keys for this account.') param allowKeys bool = true @allowed([ 'Enabled' 'Disabled' ]) @description('Whether or not public endpoint access is allowed for this account.') param publicNetworkAccess string = 'Enabled' @allowed([ 'Allow' 'Deny' ]) @description('The default action for network ACLs.') param networkAclsDefaultAction string = 'Allow' resource account 'Microsoft.CognitiveServices/accounts@2023-05-01' = { name: accountName location: location identity: { type: 'SystemAssigned' } sku: { name: sku } kind: 'AIServices' properties: { customSubDomainName: accountName publicNetworkAccess: publicNetworkAccess networkAcls: { defaultAction: networkAclsDefaultAction } disableLocalAuth: allowKeys } } output endpointUri string = 'https://${account.outputs.name}.services.ai.azure.com/models' output id string = account.id`

Use the template

`modules/ai-services-deployment-template.bicep`

to describe model deployments:**modules/ai-services-deployment-template.bicep**`@description('Name of the Azure AI services account') param accountName string @description('Name of the model to deploy') param modelName string @description('Version of the model to deploy') param modelVersion string @allowed([ 'AI21 Labs' 'Cohere' 'Core42' 'DeepSeek' 'xAI' 'Meta' 'Microsoft' 'Mistral AI' 'OpenAI' ]) @description('Model provider') param modelPublisherFormat string @allowed([ 'GlobalStandard' 'DataZoneStandard' 'Standard' 'GlobalProvisioned' 'Provisioned' ]) @description('Model deployment SKU name') param skuName string = 'GlobalStandard' @description('Content filter policy name') param contentFilterPolicyName string = 'Microsoft.DefaultV2' @description('Model deployment capacity') param capacity int = 1 resource modelDeployment 'Microsoft.CognitiveServices/accounts/deployments@2024-04-01-preview' = { name: '${accountName}/${modelName}' sku: { name: skuName capacity: capacity } properties: { model: { format: modelPublisherFormat name: modelName version: modelVersion } raiPolicyName: contentFilterPolicyName == null ? 'Microsoft.Nill' : contentFilterPolicyName } }`

For convenience, we define the model we want to have available in the service using a JSON file. The file

contains a list of JSON object with keys**infra/models.json**`name`

,`version`

,`provider`

, and`sku`

, which defines the models the deployment will provision. Since the models support serverless API deployments, adding model deployments doesn't incur on extra cost. Modify the file by**removing/adding the model entries you want to have available**. The following example**shows only the first 7 lines**of the JSON file:**models.json**`[ { "name": "Cohere-command-a", "version": "1", "provider": "Cohere", "sku": "GlobalStandard" },`

If you plan to use projects (recommended), you need the templates for creating a project, hub, and a connection to the Foundry Tools resource:

**modules/project-hub-template.bicep**`param location string = resourceGroup().location @description('Name of the Azure AI hub') param hubName string = 'hub-dev' @description('Name of the Azure AI project') param projectName string = 'intelligent-apps' @description('Name of the storage account used for the workspace.') param storageAccountName string = replace(hubName, '-', '') param keyVaultName string = replace(hubName, 'hub', 'kv') param applicationInsightsName string = replace(hubName, 'hub', 'log') @description('The container registry resource id if you want to create a link to the workspace.') param containerRegistryName string = replace(hubName, '-', '') @description('The tags for the resources') param tagValues object = { owner: 'santiagxf' project: 'intelligent-apps' environment: 'dev' } var tenantId = subscription().tenantId var resourceGroupName = resourceGroup().name var storageAccountId = resourceId(resourceGroupName, 'Microsoft.Storage/storageAccounts', storageAccountName) var keyVaultId = resourceId(resourceGroupName, 'Microsoft.KeyVault/vaults', keyVaultName) var applicationInsightsId = resourceId(resourceGroupName, 'Microsoft.Insights/components', applicationInsightsName) var containerRegistryId = resourceId( resourceGroupName, 'Microsoft.ContainerRegistry/registries', containerRegistryName ) resource storageAccount 'Microsoft.Storage/storageAccounts@2019-04-01' = { name: storageAccountName location: location sku: { name: 'Standard_LRS' } kind: 'StorageV2' properties: { encryption: { services: { blob: { enabled: true } file: { enabled: true } } keySource: 'Microsoft.Storage' } supportsHttpsTrafficOnly: true } tags: tagValues } resource keyVault 'Microsoft.KeyVault/vaults@2019-09-01' = { name: keyVaultName location: location properties: { tenantId: tenantId sku: { name: 'standard' family: 'A' } enableRbacAuthorization: true accessPolicies: [] } tags: tagValues } resource applicationInsights 'Microsoft.Insights/components@2018-05-01-preview' = { name: applicationInsightsName location: location kind: 'web' properties: { Application_Type: 'web' } tags: tagValues } resource containerRegistry 'Microsoft.ContainerRegistry/registries@2019-05-01' = { name: containerRegistryName location: location sku: { name: 'Standard' } properties: { adminUserEnabled: true } tags: tagValues } resource hub 'Microsoft.MachineLearningServices/workspaces@2024-07-01-preview' = { name: hubName kind: 'Hub' location: location identity: { type: 'systemAssigned' } sku: { tier: 'Standard' name: 'standard' } properties: { description: 'Azure AI hub' friendlyName: hubName storageAccount: storageAccountId keyVault: keyVaultId applicationInsights: applicationInsightsId containerRegistry: (empty(containerRegistryName) ? null : containerRegistryId) encryption: { status: 'Disabled' keyVaultProperties: { keyVaultArmId: keyVaultId keyIdentifier: '' } } hbiWorkspace: false } tags: tagValues } resource project 'Microsoft.MachineLearningServices/workspaces@2024-07-01-preview' = { name: projectName kind: 'Project' location: location identity: { type: 'systemAssigned' } sku: { tier: 'Standard' name: 'standard' } properties: { description: 'Azure AI project' friendlyName: projectName hbiWorkspace: false hubResourceId: hub.id } tags: tagValues }`

**modules/ai-services-connection-template.bicep**`@description('Name of the hub where the connection will be created') param hubName string @description('Name of the connection') param name string @description('Category of the connection') param category string = 'AIServices' @allowed(['AAD', 'ApiKey', 'ManagedIdentity', 'None']) param authType string = 'AAD' @description('The endpoint URI of the connected service') param endpointUri string @description('The resource ID of the connected service') param resourceId string = '' @secure() param key string = '' resource connection 'Microsoft.MachineLearningServices/workspaces/connections@2024-04-01-preview' = { name: '${hubName}/${name}' properties: { category: category target: endpointUri authType: authType isSharedToAll: true credentials: authType == 'ApiKey' ? { key: key } : null metadata: { ApiType: 'Azure' ResourceId: resourceId } } }`

Define the main deployment:

**deploy-with-project.bicep**`@description('Location to create the resources in') param location string = resourceGroup().location @description('Name of the resource group to create the resources in') param resourceGroupName string = resourceGroup().name @description('Name of the AI Services account to create') param accountName string = 'azurei-models-dev' @description('Name of the project hub to create') param hubName string = 'hub-azurei-dev' @description('Name of the project to create in the project hub') param projectName string = 'intelligent-apps' @description('Path to a JSON file with the list of models to deploy. Each model is a JSON object with the following properties: name, version, provider') var models = json(loadTextContent('models.json')) module aiServicesAccount 'modules/ai-services-template.bicep' = { name: 'aiServicesAccount' scope: resourceGroup(resourceGroupName) params: { accountName: accountName location: location } } module projectHub 'modules/project-hub-template.bicep' = { name: 'projectHub' scope: resourceGroup(resourceGroupName) params: { hubName: hubName projectName: projectName } } module aiServicesConnection 'modules/ai-services-connection-template.bicep' = { name: 'aiServicesConnection' scope: resourceGroup(resourceGroupName) params: { name: accountName authType: 'AAD' endpointUri: aiServicesAccount.outputs.endpointUri resourceId: aiServicesAccount.outputs.id hubName: hubName } dependsOn: [ projectHub ] } @batchSize(1) module modelDeployments 'modules/ai-services-deployment-template.bicep' = [ for (item, i) in models: { name: 'deployment-${item.name}' scope: resourceGroup(resourceGroupName) params: { accountName: accountName modelName: item.name modelVersion: item.version modelPublisherFormat: item.provider skuName: item.sku } dependsOn: [ aiServicesAccount ] } ] output endpoint string = aiServicesAccount.outputs.endpointUri`

Log into Azure:

`az login`

Ensure you are in the right subscription:

`az account set --subscription "<subscription-id>"`

Run the deployment:

`RESOURCE_GROUP="<resource-group-name>" az deployment group create \ --resource-group $RESOURCE_GROUP \ --template-file deploy-with-project.bicep`

If you want to deploy only the Foundry Tools resource and the model deployments, use the following deployment file:

**deploy.bicep**`@description('Location to create the resources in') param location string = resourceGroup().location @description('Name of the resource group to create the resources in') param resourceGroupName string = resourceGroup().name @description('Name of the AI Services account to create') param accountName string = 'azurei-models-dev' @description('Path to a JSON file with the list of models to deploy. Each model is a JSON object with the following properties: name, version, provider') var models = json(loadTextContent('models.json')) module aiServicesAccount 'modules/ai-services-template.bicep' = { name: 'aiServicesAccount' scope: resourceGroup(resourceGroupName) params: { accountName: accountName location: location } } @batchSize(1) module modelDeployments 'modules/ai-services-deployment-template.bicep' = [ for (item, i) in models: { name: 'deployment-${item.name}' scope: resourceGroup(resourceGroupName) params: { accountName: accountName modelName: item.name modelVersion: item.version modelPublisherFormat: item.provider skuName: item.sku } dependsOn: [ aiServicesAccount ] } ] output endpoint string = aiServicesAccount.outputs.endpointUri`

Run the deployment:

`RESOURCE_GROUP="<resource-group-name>" az deployment group create \ --resource-group $RESOURCE_GROUP \ --template-file deploy.bicep`

The template outputs the Microsoft Foundry Models endpoint that you can use to consume any of the model deployments you have created.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/how-to/use-embeddings -->

# How to generate embeddings with Microsoft Foundry Models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Important

If you're currently using an Azure AI Inference beta SDK with Microsoft Foundry Models or Azure OpenAI service, we strongly recommend that you transition to the generally available [OpenAI/v1 API](https://aka.ms/openai/v1), which uses an OpenAI stable SDK.

For more information on how to migrate to the OpenAI/v1 API by using an SDK in your programming language of choice, see [Migrate from Azure AI Inference SDK to OpenAI SDK](../../how-to/model-inference-to-openai-migration?view=foundry-classic).

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

This article explains how to use embeddings API with models deployed in Microsoft Foundry Models.

## Prerequisites

To use embedding models in your application, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Microsoft Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry project. This kind of project is managed under a Foundry resource. If you don't have a Foundry project, see

[Create a project for Foundry (Foundry projects)](../../how-to/create-projects?view=foundry-classic).The endpoint's URL.

The endpoint's key (if you choose to use API key for authentication).


Install the

[Azure AI inference package for Python](https://aka.ms/azsdk/azure-ai-inference/python/reference)with the following command:`pip install -U azure-ai-inference`


- An embeddings model deployment. If you don't have one read
[Add and configure Foundry Models](create-model-deployments?view=foundry-classic)to add an embeddings model to your resource.

## Use embeddings

First, create the client to consume the model. The following code uses an endpoint URL and key that are stored in environment variables.

```
import os
from azure.ai.inference import EmbeddingsClient
from azure.core.credentials import AzureKeyCredential
model = EmbeddingsClient(
endpoint="https://<resource>.services.ai.azure.com/models",
credential=AzureKeyCredential(os.environ["AZURE_INFERENCE_CREDENTIAL"]),
model="text-embedding-3-small"
)
```


If you have configured the resource to with **Microsoft Entra ID** support, you can use the following code snippet to create a client.

```
import os
from azure.ai.inference import EmbeddingsClient
from azure.identity import DefaultAzureCredential
model = EmbeddingsClient(
endpoint="https://<resource>.services.ai.azure.com/models",
credential=DefaultAzureCredential(),
model="text-embedding-3-small"
)
```


### Create embeddings

Create an embedding request to see the output of the model.

```
response = model.embed(
input=["The ultimate answer to the question of life"],
)
```


Tip

When creating a request, take into account the token's input limit for the model. If you need to embed larger portions of text, you would need a chunking strategy.

The response is as follows, where you can see the model's usage statistics:

```
import numpy as np
for embed in response.data:
print("Embedding of size:", np.asarray(embed.embedding).shape)
print("Model:", response.model)
print("Usage:", response.usage)
```


It can be useful to compute embeddings in input batches. The parameter `inputs`

can be a list of strings, where each string is a different input. In turn the response is a list of embeddings, where each embedding corresponds to the input in the same position.

```
response = model.embed(
input=[
"The ultimate answer to the question of life",
"The largest planet in our solar system is Jupiter",
],
)
```


The response is as follows, where you can see the model's usage statistics:

```
import numpy as np
for embed in response.data:
print("Embedding of size:", np.asarray(embed.embedding).shape)
print("Model:", response.model)
print("Usage:", response.usage)
```


Tip

When creating batches of request, take into account the batch limit for each of the models. Most models have a 1024 batch limit.

#### Specify embeddings dimensions

You can specify the number of dimensions for the embeddings. The following example code shows how to create embeddings with 1024 dimensions. Notice that not all the embedding models support indicating the number of dimensions in the request and on those cases a 422 error is returned.

```
response = model.embed(
input=["The ultimate answer to the question of life"],
dimensions=1024,
)
```


#### Create different types of embeddings

Some models can generate multiple embeddings for the same input depending on how you plan to use them. This capability allows you to retrieve more accurate embeddings for RAG patterns.

The following example shows how to create embeddings that are used to create an embedding for a document that will be stored in a vector database:

```
from azure.ai.inference.models import EmbeddingInputType
response = model.embed(
input=["The answer to the ultimate question of life, the universe, and everything is 42"],
input_type=EmbeddingInputType.DOCUMENT,
)
```


When you work on a query to retrieve such a document, you can use the following code snippet to create the embeddings for the query and maximize the retrieval performance.

```
from azure.ai.inference.models import EmbeddingInputType
response = model.embed(
input=["What's the ultimate meaning of life?"],
input_type=EmbeddingInputType.QUERY,
)
```


Notice that not all the embedding models support indicating the input type in the request and on those cases a 422 error is returned. By default, embeddings of type `Text`

are returned.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

This article explains how to use embeddings API with models deployed in Microsoft Foundry Models.

## Prerequisites

To use embedding models in your application, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Microsoft Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry project. This kind of project is managed under a Foundry resource. If you don't have a Foundry project, see

[Create a project for Foundry (Foundry projects)](../../how-to/create-projects?view=foundry-classic).The endpoint's URL.

The endpoint's key (if you choose to use API key for authentication).


Install the

[Azure Inference library for JavaScript](https://aka.ms/azsdk/azure-ai-inference/javascript/reference)with the following command:`npm install @azure-rest/ai-inference npm install @azure/core-auth npm install @azure/identity`

If you are using Node.js, you can configure the dependencies in

**package.json**:**package.json**`{ "name": "main_app", "version": "1.0.0", "description": "", "main": "app.js", "type": "module", "dependencies": { "@azure-rest/ai-inference": "1.0.0-beta.6", "@azure/core-auth": "1.9.0", "@azure/core-sse": "2.2.0", "@azure/identity": "4.8.0" } }`

Import the following:

`import ModelClient from "@azure-rest/ai-inference"; import { isUnexpected } from "@azure-rest/ai-inference"; import { createSseStream } from "@azure/core-sse"; import { AzureKeyCredential } from "@azure/core-auth"; import { DefaultAzureCredential } from "@azure/identity";`


- An embeddings model deployment. If you don't have one read
[Add and configure Foundry Models](create-model-deployments?view=foundry-classic)to add an embeddings model to your resource.

## Use embeddings

First, create the client to consume the model. The following code uses an endpoint URL and key that are stored in environment variables.

```
const client = ModelClient(
"https://<resource>.services.ai.azure.com/models",
new AzureKeyCredential(process.env.AZURE_INFERENCE_CREDENTIAL)
);
```


If you've configured the resource with **Microsoft Entra ID** support, you can use the following code snippet to create a client.

```
const clientOptions = { credentials: { "https://cognitiveservices.azure.com" } };
const client = ModelClient(
"https://<resource>.services.ai.azure.com/models",
new DefaultAzureCredential()
clientOptions,
);
```


### Create embeddings

Create an embedding request to see the output of the model.

```
var response = await client.path("/embeddings").post({
body: {
model: "text-embedding-3-small",
input: ["The ultimate answer to the question of life"],
}
});
```


Tip

When creating a request, take into account the token's input limit for the model. If you need to embed larger portions of text, you would need a chunking strategy.

The response is as follows, where you can see the model's usage statistics:

```
if (isUnexpected(response)) {
throw response.body.error;
}
console.log(response.embedding);
console.log(response.body.model);
console.log(response.body.usage);
```


It can be useful to compute embeddings in input batches. The parameter `inputs`

can be a list of strings, where each string is a different input. In turn the response is a list of embeddings, where each embedding corresponds to the input in the same position.

```
var response = await client.path("/embeddings").post({
body: {
model: "text-embedding-3-small",
input: [
"The ultimate answer to the question of life",
"The largest planet in our solar system is Jupiter",
],
}
});
```


The response is as follows, where you can see the model's usage statistics:

```
if (isUnexpected(response)) {
throw response.body.error;
}
console.log(response.embedding);
console.log(response.body.model);
console.log(response.body.usage);
```


Tip

When creating batches of request, take into account the batch limit for each of the models. Most models have a 1024 batch limit.

#### Specify embeddings dimensions

You can specify the number of dimensions for the embeddings. The following example code shows how to create embeddings with 1024 dimensions. Notice that not all the embedding models support indicating the number of dimensions in the request and on those cases a 422 error is returned.

```
var response = await client.path("/embeddings").post({
body: {
model: "text-embedding-3-small",
input: ["The ultimate answer to the question of life"],
dimensions: 1024,
}
});
```


#### Create different types of embeddings

Some models can generate multiple embeddings for the same input depending on how you plan to use them. This capability allows you to retrieve more accurate embeddings for RAG patterns.

The following example shows how to create embeddings that are used to create an embedding for a document that will be stored in a vector database:

```
var response = await client.path("/embeddings").post({
body: {
model: "text-embedding-3-small",
input: ["The answer to the ultimate question of life, the universe, and everything is 42"],
input_type: "document",
}
});
```


When you work on a query to retrieve such a document, you can use the following code snippet to create the embeddings for the query and maximize the retrieval performance.

```
var response = await client.path("/embeddings").post({
body: {
model: "text-embedding-3-small",
input: ["What's the ultimate meaning of life?"],
input_type: "query",
}
});
```


Notice that not all the embedding models support indicating the input type in the request and on those cases a 422 error is returned. By default, embeddings of type `Text`

are returned.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

This article explains how to use embeddings API with models deployed in Microsoft Foundry Models.

## Prerequisites

To use embedding models in your application, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Microsoft Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry project. This kind of project is managed under a Foundry resource. If you don't have a Foundry project, see

[Create a project for Foundry (Foundry projects)](../../how-to/create-projects?view=foundry-classic).The endpoint's URL.

The endpoint's key (if you choose to use API key for authentication).


Add the

[Azure AI inference package](https://aka.ms/azsdk/azure-ai-inference/java/reference)to your project:`<dependency> <groupId>com.azure</groupId> <artifactId>azure-ai-inference</artifactId> <version>1.0.0-beta.4</version> </dependency>`

If you are using Entra ID, you also need the following package:

`<dependency> <groupId>com.azure</groupId> <artifactId>azure-identity</artifactId> <version>1.15.3</version> </dependency>`

Import the following namespace:

`package com.azure.ai.inference.usage; import com.azure.ai.inference.EmbeddingsClient; import com.azure.ai.inference.EmbeddingsClientBuilder; import com.azure.ai.inference.ChatCompletionsClient; import com.azure.ai.inference.ChatCompletionsClientBuilder; import com.azure.ai.inference.models.EmbeddingsResult; import com.azure.ai.inference.models.EmbeddingItem; import com.azure.ai.inference.models.ChatCompletions; import com.azure.core.credential.AzureKeyCredential; import com.azure.core.util.Configuration; import java.util.ArrayList; import java.util.List;`


Import the following namespace:

`package com.azure.ai.inference.usage; import com.azure.ai.inference.EmbeddingsClient; import com.azure.ai.inference.EmbeddingsClientBuilder; import com.azure.ai.inference.models.EmbeddingsResult; import com.azure.ai.inference.models.EmbeddingItem; import com.azure.core.credential.AzureKeyCredential; import com.azure.core.util.Configuration; import java.util.ArrayList; import java.util.List;`

An embeddings model deployment. If you don't have one read

[Add and configure Foundry Models](create-model-deployments?view=foundry-classic)to add an embeddings model to your resource.

## Use embeddings

First, create the client to consume the model. The following code uses an endpoint URL and key that are stored in environment variables.

```
EmbeddingsClient client = new EmbeddingsClient(
URI.create(System.getProperty("AZURE_INFERENCE_ENDPOINT")),
new AzureKeyCredential(System.getProperty("AZURE_INFERENCE_CREDENTIAL")),
"text-embedding-3-small"
);
```


If you have configured the resource to with **Microsoft Entra ID** support, you can use the following code snippet to create a client.

```
client = new EmbeddingsClient(
URI.create(System.getProperty("AZURE_INFERENCE_ENDPOINT")),
new DefaultAzureCredential(),
"text-embedding-3-small"
);
```


### Create embeddings

Create an embedding request to see the output of the model.

```
EmbeddingsOptions requestOptions = new EmbeddingsOptions()
.setInput(Arrays.asList("The ultimate answer to the question of life"));
Response<EmbeddingsResult> response = client.embed(requestOptions);
```


Tip

When creating a request, take into account the token's input limit for the model. If you need to embed larger portions of text, you would need a chunking strategy.

The response is as follows, where you can see the model's usage statistics:

```
System.out.println("Embedding: " + response.getValue().getData());
System.out.println("Model: " + response.getValue().getModel());
System.out.println("Usage:");
System.out.println("\tPrompt tokens: " + response.getValue().getUsage().getPromptTokens());
System.out.println("\tTotal tokens: " + response.getValue().getUsage().getTotalTokens());
```


It can be useful to compute embeddings in input batches. The parameter `inputs`

can be a list of strings, where each string is a different input. In turn the response is a list of embeddings, where each embedding corresponds to the input in the same position.

```
requestOptions = new EmbeddingsOptions()
.setInput(Arrays.asList(
"The ultimate answer to the question of life",
"The largest planet in our solar system is Jupiter"
));
response = client.embed(requestOptions);
```


The response is as follows, where you can see the model's usage statistics:

Tip

When creating batches of request, take into account the batch limit for each of the models. Most models have a 1024 batch limit.

#### Specify embeddings dimensions

You can specify the number of dimensions for the embeddings. The following example code shows how to create embeddings with 1024 dimensions. Notice that not all the embedding models support indicating the number of dimensions in the request and on those cases a 422 error is returned.

#### Create different types of embeddings

Some models can generate multiple embeddings for the same input depending on how you plan to use them. This capability allows you to retrieve more accurate embeddings for RAG patterns.

The following example shows how to create embeddings that are used to create an embedding for a document that will be stored in a vector database:

```
List<String> input = Arrays.asList("The answer to the ultimate question of life, the universe, and everything is 42");
requestOptions = new EmbeddingsOptions(input, EmbeddingInputType.DOCUMENT);
response = client.embed(requestOptions);
```


When you work on a query to retrieve such a document, you can use the following code snippet to create the embeddings for the query and maximize the retrieval performance.

```
input = Arrays.asList("What's the ultimate meaning of life?");
requestOptions = new EmbeddingsOptions(input, EmbeddingInputType.QUERY);
response = client.embed(requestOptions);
```


Notice that not all the embedding models support indicating the input type in the request and on those cases a 422 error is returned. By default, embeddings of type `Text`

are returned.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

This article explains how to use embeddings API with models deployed in Microsoft Foundry Models.

## Prerequisites

To use embedding models in your application, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Microsoft Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry project. This kind of project is managed under a Foundry resource. If you don't have a Foundry project, see

[Create a project for Foundry (Foundry projects)](../../how-to/create-projects?view=foundry-classic).The endpoint's URL.

The endpoint's key (if you choose to use API key for authentication).


Install the

[Azure AI inference package](https://aka.ms/azsdk/azure-ai-inference/python/reference)with the following command:`dotnet add package Azure.AI.Inference --prerelease`

If you are using Entra ID, you also need the following package:

`dotnet add package Azure.Identity`


- An embeddings model deployment. If you don't have one read
[Add and configure Foundry Models](create-model-deployments?view=foundry-classic)to add an embeddings model to your resource.

## Use embeddings

First, create the client to consume the model. The following code uses an endpoint URL and key that are stored in environment variables.

```
EmbeddingsClient client = new EmbeddingsClient(
new Uri(Environment.GetEnvironmentVariable("AZURE_INFERENCE_ENDPOINT")),
new AzureKeyCredential(Environment.GetEnvironmentVariable("AZURE_INFERENCE_CREDENTIAL"))
);
```


If you configured the resource to with **Microsoft Entra ID** support, you can use the following code snippet to create a client. Note that here `includeInteractiveCredentials`

is set to `true`

only for demonstration purposes so authentication can happen using the web browser. On production workloads, you should remove such parameter.

```
TokenCredential credential = new DefaultAzureCredential(includeInteractiveCredentials: true);
AzureAIInferenceClientOptions clientOptions = new AzureAIInferenceClientOptions();
BearerTokenAuthenticationPolicy tokenPolicy = new BearerTokenAuthenticationPolicy(credential, new string[] { "https://cognitiveservices.azure.com/.default" });
clientOptions.AddPolicy(tokenPolicy, HttpPipelinePosition.PerRetry);
client = new EmbeddingsClient(
new Uri("https://<resource>.services.ai.azure.com/models"),
credential,
clientOptions,
);
```


### Create embeddings

Create an embedding request to see the output of the model.

```
EmbeddingsOptions requestOptions = new EmbeddingsOptions()
{
Input = {
"The ultimate answer to the question of life"
},
Model = "text-embedding-3-small"
};
Response<EmbeddingsResult> response = client.Embed(requestOptions);
```


Tip

When creating a request, take into account the token's input limit for the model. If you need to embed larger portions of text, you would need a chunking strategy.

The response is as follows, where you can see the model's usage statistics:

```
Console.WriteLine($"Embedding: {response.Value.Data}");
Console.WriteLine($"Model: {response.Value.Model}");
Console.WriteLine("Usage:");
Console.WriteLine($"\tPrompt tokens: {response.Value.Usage.PromptTokens}");
Console.WriteLine($"\tTotal tokens: {response.Value.Usage.TotalTokens}");
```


It can be useful to compute embeddings in input batches. The parameter `inputs`

can be a list of strings, where each string is a different input. In turn the response is a list of embeddings, where each embedding corresponds to the input in the same position.

```
EmbeddingsOptions requestOptions = new EmbeddingsOptions()
{
Input = {
"The ultimate answer to the question of life",
"The largest planet in our solar system is Jupiter"
},
Model = "text-embedding-3-small"
};
Response<EmbeddingsResult> response = client.Embed(requestOptions);
```


The response is as follows, where you can see the model's usage statistics:

Tip

When creating batches of request, take into account the batch limit for each of the models. Most models have a 1024 batch limit.

#### Specify embeddings dimensions

You can specify the number of dimensions for the embeddings. The following example code shows how to create embeddings with 1024 dimensions. Notice that not all the embedding models support indicating the number of dimensions in the request and on those cases a 422 error is returned.

#### Create different types of embeddings

Some models can generate multiple embeddings for the same input depending on how you plan to use them. This capability allows you to retrieve more accurate embeddings for RAG patterns.

The following example shows how to create embeddings that are used to create an embedding for a document that will be stored in a vector database:

```
var input = new List<string> {
"The answer to the ultimate question of life, the universe, and everything is 42"
};
var requestOptions = new EmbeddingsOptions()
{
Input = input,
InputType = EmbeddingInputType.DOCUMENT,
Model = "text-embedding-3-small"
};
Response<EmbeddingsResult> response = client.Embed(requestOptions);
```


When you work on a query to retrieve such a document, you can use the following code snippet to create the embeddings for the query and maximize the retrieval performance.

```
var input = new List<string> {
"What's the ultimate meaning of life?"
};
var requestOptions = new EmbeddingsOptions()
{
Input = input,
InputType = EmbeddingInputType.QUERY,
Model = "text-embedding-3-small"
};
Response<EmbeddingsResult> response = client.Embed(requestOptions);
```


Notice that not all the embedding models support indicating the input type in the request and on those cases a 422 error is returned. By default, embeddings of type `Text`

are returned.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

This article explains how to use embeddings API with models deployed in Microsoft Foundry Models.

## Prerequisites

To use embedding models in your application, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Microsoft Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry project. This kind of project is managed under a Foundry resource. If you don't have a Foundry project, see

[Create a project for Foundry (Foundry projects)](../../how-to/create-projects?view=foundry-classic).The endpoint's URL.

The endpoint's key (if you choose to use API key for authentication).


- An embeddings model deployment. If you don't have one read
[Add and configure Foundry Models](create-model-deployments?view=foundry-classic)to add an embeddings model to your resource.

## Use embeddings

To use the text embeddings, use the route `/embeddings`

appended to the base URL along with your credential indicated in `api-key`

. `Authorization`

header is also supported with the format `Bearer <key>`

.

```
POST https://<resource>.services.ai.azure.com/models/embeddings?api-version=2024-05-01-preview
Content-Type: application/json
api-key: <key>
```


If you have configured the resource with **Microsoft Entra ID** support, pass you token in the `Authorization`

header with the format `Bearer <token>`

. Use scope `https://cognitiveservices.azure.com/.default`

.

```
POST https://<resource>.services.ai.azure.com/models/embeddings?api-version=2024-05-01-preview
Content-Type: application/json
Authorization: Bearer <token>
```


Using Microsoft Entra ID may require additional configuration in your resource to grant access. Learn how to [configure key-less authentication with Microsoft Entra ID](configure-entra-id?view=foundry-classic).

### Create embeddings

Create an embedding request to see the output of the model.

```
{
"model": "text-embedding-3-small",
"input": [
"The ultimate answer to the question of life"
]
}
```


Tip

When creating a request, take into account the token's input limit for the model. If you need to embed larger portions of text, you would need a chunking strategy.

The response is as follows, where you can see the model's usage statistics:

```
{
"id": "0ab1234c-d5e6-7fgh-i890-j1234k123456",
"object": "list",
"data": [
{
"index": 0,
"object": "embedding",
"embedding": [
0.017196655,
// ...
-0.000687122,
-0.025054932,
-0.015777588
]
}
],
"model": "text-embedding-3-small",
"usage": {
"prompt_tokens": 9,
"completion_tokens": 0,
"total_tokens": 9
}
}
```


It can be useful to compute embeddings in input batches. The parameter `inputs`

can be a list of strings, where each string is a different input. In turn the response is a list of embeddings, where each embedding corresponds to the input in the same position.

```
{
"model": "text-embedding-3-small",
"input": [
"The ultimate answer to the question of life",
"The largest planet in our solar system is Jupiter"
]
}
```


The response is as follows, where you can see the model's usage statistics:

```
{
"id": "0ab1234c-d5e6-7fgh-i890-j1234k123456",
"object": "list",
"data": [
{
"index": 0,
"object": "embedding",
"embedding": [
0.017196655,
// ...
-0.000687122,
-0.025054932,
-0.015777588
]
},
{
"index": 1,
"object": "embedding",
"embedding": [
0.017196655,
// ...
-0.000687122,
-0.025054932,
-0.015777588
]
}
],
"model": "text-embedding-3-small",
"usage": {
"prompt_tokens": 19,
"completion_tokens": 0,
"total_tokens": 19
}
}
```


Tip

When creating batches of request, take into account the batch limit for each of the models. Most models have a 1024 batch limit.

#### Specify embeddings dimensions

You can specify the number of dimensions for the embeddings. The following example code shows how to create embeddings with 1024 dimensions. Notice that not all the embedding models support indicating the number of dimensions in the request and on those cases a 422 error is returned.

```
{
"model": "text-embedding-3-small",
"input": [
"The ultimate answer to the question of life"
],
"dimensions": 1024
}
```


#### Create different types of embeddings

Some models can generate multiple embeddings for the same input depending on how you plan to use them. This capability allows you to retrieve more accurate embeddings for RAG patterns.

The following example shows how to create embeddings that are used to create an embedding for a document that will be stored in a vector database. Since `text-embedding-3-small`

doesn't support this capability, we are using an embedding model from Cohere in the following example:

```
{
"model": "cohere-embed-v3-english",
"input": [
"The answer to the ultimate question of life, the universe, and everything is 42"
],
"input_type": "document"
}
```


When you work on a query to retrieve such a document, you can use the following code snippet to create the embeddings for the query and maximize the retrieval performance. Since `text-embedding-3-small`

doesn't support this capability, we are using an embedding model from Cohere in the following example:

```
{
"model": "cohere-embed-v3-english",
"input": [
"What's the ultimate meaning of life?"
],
"input_type": "query"
}
```


Notice that not all the embedding models support indicating the input type in the request and on those cases a 422 error is returned. By default, embeddings of type `Text`

are returned.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/how-to/configure-entra-id -->

# Configure keyless authentication with Microsoft Entra ID

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

This article explains how to configure keyless authentication with Microsoft Entra ID for Microsoft Foundry Models. Keyless authentication enhances security by eliminating the need for API keys, simplifies the user experience with role-based access control (RBAC), and reduces operational complexity while providing robust compliance support.

## Prerequisites

To complete this article, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Microsoft Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry project. This kind of project is managed under a Foundry resource. If you don't have a Foundry project, see

[Create a project for Foundry (Foundry projects)](../../how-to/create-projects?view=foundry-classic)The endpoint's URL.

An account with

`Microsoft.Authorization/roleAssignments/write`

and`Microsoft.Authorization/roleAssignments/delete`

permissions, such as the**Administrator**role-based access control. See the next section on[Required Azure roles and permissions](#required-azure-roles-and-permissions)for more details.

### Required Azure roles and permissions

Microsoft Entra ID uses role-based access control (RBAC) to manage access to Azure resources. You need different roles, depending on whether you're setting up authentication (administrator) or using it to make API calls (developer).

#### For setting up authentication

**Subscription owner or administrator**: An account with`Microsoft.Authorization/roleAssignments/write`

and`Microsoft.Authorization/roleAssignments/delete`

permissions, such as the**Owner**or**User Access Administrator**role, required to assign the**Cognitive Services User**role to developers.

#### For making authenticated API calls

**Cognitive Services User**role: Required for developers to authenticate and make inference API calls using Microsoft Entra ID. This role must be assigned at the scope of your Foundry resource.

#### Role assignment requirements

When assigning roles, specify these three elements:

**Security principal**: Your user account, service principal, or security group (recommended for managing multiple users)**Role definition**: The**Cognitive Services User**role**Scope**: Your specific Foundry resource

Tip

Azure role assignments can take up to 5 minutes to propagate. When using security groups, changes to group membership propagate immediately.

#### Custom role (optional)

If you prefer a custom role instead of **Cognitive Services User**, make sure it includes these permissions:

```
{
"permissions": [
{
"dataActions": [
"Microsoft.CognitiveServices/accounts/MaaS/*"
]
}
]
}
```


For more context on how roles work with Azure resources, see [Understand roles in the context of resource in Azure](#understand-roles-in-the-context-of-resource-in-azure).

## Configure Microsoft Entra ID for inference

This section lists the steps to configure Microsoft Entra ID for inference from the Microsoft Foundry resource page in the [Azure portal](https://portal.azure.com).

#### Find the Foundry resource page in Azure portal

If you're in the Foundry portal, you can navigate to the Foundry resource page in the Azure portal.

Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is off. These steps refer to**Foundry (classic)**.Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**.On the landing page, select

**Management center**.Go to the

**Connected resources**section and select the connection to the Foundry resource that you want to configure. If it isn't listed, select**View all**to see the full list.On the

**Connection details**section, under**Resource**, select the name of the Azure resource. This action opens the resource in the Azure portal.

#### Configure Microsoft Entra ID from the resource page

Select the resource name to open it.

In the left pane, select

**Access control (IAM)**, and then select**Add**>**Add role assignment**.Tip

Use the

**View my access**option to verify which roles are already assigned to you.In

**Job function roles**, type**Cognitive Services User**.Select the role and select

**Next**.On

**Members**, select the user or group you want to grant access to. Use security groups whenever possible because they're easier to manage and maintain.Select

**Next**and finish the wizard.The selected user can now use Microsoft Entra ID for inference.

Tip

Azure role assignments can take up to five minutes to propagate. When working with security groups, adding or removing users from the security group propagates immediately.

Verify the role assignment:

On the left pane in the Azure portal, select

**Access control (IAM)**.Select

**Check access**.Search for the user or security group you assigned the role to.

Verify that

**Cognitive Services User**appears in their assigned roles.


Key-based access is still possible for users who already have keys available to them. To revoke the keys, in Azure portal, on the left navigation, select **Resource Management** > **Keys and Endpoints** > **Regenerate Key1** and **Regenerate Key2**.

## Use Microsoft Entra ID in your code

After you configure Microsoft Entra ID in your resource, update your code to use it when you consume the inference endpoint. This example shows how to use a chat completions model:

Install the OpenAI SDK using a package manager like pip:

```
pip install openai
```


For Microsoft Entra ID authentication, also install:

```
pip install azure-identity
```


Use the package to consume the model. The following example shows how to create a client to consume chat completions with Microsoft Entra ID and make a test call to the chat completions endpoint with your model deployment.

Replace `<resource>`

with your Foundry resource name. Find it in the Azure portal or by running `az cognitiveservices account list`

. Replace `DeepSeek-V3.1`

with your actual deployment name.

```
from openai import OpenAI
from azure.identity import DefaultAzureCredential, get_bearer_token_provider
token_provider = get_bearer_token_provider(
DefaultAzureCredential(),
"https://cognitiveservices.azure.com/.default"
)
client = OpenAI(
base_url="https://<resource>.openai.azure.com/openai/v1/",
api_key=token_provider,
)
completion = client.chat.completions.create(
model="DeepSeek-V3.1", # Required: your deployment name
messages=[
{"role": "system", "content": "You are a helpful assistant."},
{"role": "user", "content": "What is Azure AI?"}
]
)
print(completion.choices[0].message.content)
```


Expected output

```
Azure AI is a comprehensive suite of artificial intelligence services and tools from Microsoft that enables developers to build intelligent applications. It includes services for natural language processing, computer vision, speech recognition, and machine learning capabilities.
```


Reference: [OpenAI Python SDK](https://github.com/openai/openai-python) and [DefaultAzureCredential class](/en-us/python/api/azure-identity/azure.identity.defaultazurecredential).

### Options for credential when using Microsoft Entra ID

`DefaultAzureCredential`

is an opinionated, ordered sequence of mechanisms for authenticating to Microsoft Entra ID. Each authentication mechanism is a class that's derived from the `TokenCredential`

class and is known as a credential. At runtime, `DefaultAzureCredential`

attempts to authenticate using the first credential. If that credential fails to acquire an access token, the next credential in the sequence is attempted, and so on, until an access token is obtained. In this way, your app can use different credentials in different environments without writing environment-specific code.

When the preceding code runs on your local development workstation, it looks in the environment variables for an application service principal or at locally installed developer tools, like Visual Studio, for a set of developer credentials. You can use either approach to authenticate the app to Azure resources during local development.

When deployed to Azure, this same code can also authenticate your app to other Azure resources. `DefaultAzureCredential`

can retrieve environment settings and managed identity configurations to authenticate to other services automatically.

### Best practices

Use deterministic credentials in production environments: Strongly consider moving from

`DefaultAzureCredential`

to one of the following deterministic solutions in production environments:- A specific
`TokenCredential`

implementation, like`ManagedIdentityCredential`

. See the[Derived list for options](/en-us/dotnet/api/azure.core.tokencredential#definition). - A pared-down
`ChainedTokenCredential`

implementation that's optimized for the Azure environment in which your app runs.`ChainedTokenCredential`

essentially creates a specific allowlist of acceptable credential options, like`ManagedIdentity`

for production and`VisualStudioCredential`

for development.

- A specific
Configure system-assigned or user-assigned managed identities to the Azure resources where your code runs, if possible. Configure Microsoft Entra ID access to those specific identities.


## Use Microsoft Entra ID in your project

Even when your resource has Microsoft Entra ID configured, your projects might still use keys to consume predictions from the resource. When you use the Foundry playground, Foundry uses the credentials associated with the connection in your project.

To change this behavior, update the connections in your projects to use Microsoft Entra ID. Follow these steps:

Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is off. These steps refer to**Foundry (classic)**.Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**.Go to the projects or hubs that use the Foundry resource through a connection.

Select

**Management center**.Go to the

**Connected resources**section and select the connection to the Foundry resource that you want to configure. If it's not listed, select**View all**to see the full list.In the

**Connection details**section, next to**Access details**, select the edit icon.Under

**Authentication**, change the value to**Microsoft Entra ID**.Select

**Update**.Your connection is configured to work with Microsoft Entra ID.


## Disable key-based authentication in the resource

Disable key-based authentication when you implement Microsoft Entra ID and fully address compatibility or fallback concerns in all applications that consume the service. You can disable key-based authentication by using Azure CLI or when deploying with Bicep or ARM.

Key-based access is still possible for users that already have keys available to them. To revoke the keys, in the Azure portal, on the left navigation, select **Resource Management** > **Keys and Endpoints** > **Regenerate Key1** and **Regenerate Key2**.

Install the

[Azure CLI](/en-us/cli/azure/)Identify the following information:

Your Azure subscription ID

Your Microsoft Foundry resource name

The resource group where you deployed the Foundry resource


## Configure Microsoft Entra ID for inference

To configure Microsoft Entra ID for inference, follow these steps:

Sign in to your Azure subscription.

`# Authenticate with Azure and sign in interactively az login`

If you have more than one subscription, select the subscription where your resource is located.

`# Set the active subscription context az account set --subscription "<subscription-id>"`

Set the following environment variables with the name of the resource and resource group you plan to use.

`# Store resource identifiers for reuse in subsequent commands ACCOUNT_NAME="<ai-services-resource-name>" RESOURCE_GROUP="<resource-group>"`

Get the full name of your resource.

`# Retrieve the full Azure Resource Manager ID for role assignment scoping RESOURCE_ID=$(az resource show -g $RESOURCE_GROUP -n $ACCOUNT_NAME --resource-type "Microsoft.CognitiveServices/accounts" --query id --output tsv)`

Get the object ID of the security principal you want to assign permissions to. The following examples show how to get the object ID associated with:

**Your own signed in account:**`# Get your user's Microsoft Entra ID object ID OBJECT_ID=$(az ad signed-in-user show --query id --output tsv)`

**A security group:**`# Get the object ID for a security group (recommended for production) OBJECT_ID=$(az ad group show --group "<group-name>" --query id --output tsv)`

**A service principal:**`# Get the object ID for a service principal (for app authentication) OBJECT_ID=$(az ad sp show --id "<service-principal-guid>" --query id --output tsv)`

Assign the

**Cognitive Services User**role to the service principal (scoped to the resource). By assigning a role, you grant the service principal access to this resource.`# Grant inference access by assigning the Cognitive Services User role az role assignment create --assignee-object-id $OBJECT_ID --role "Cognitive Services User" --scope $RESOURCE_ID`

The selected user can now use Microsoft Entra ID for inference.

Tip

Keep in mind that Azure role assignments can take up to five minutes to propagate. Adding or removing users from a security group propagates immediately.

Verify the role assignment:

`az role assignment list --scope $RESOURCE_ID --assignee $OBJECT_ID --query "[?roleDefinitionName=='Cognitive Services User'].{principalName:principalName, roleDefinitionName:roleDefinitionName}" --output table`

The output should show the

**Cognitive Services User**role assigned to your principal.

## Use Microsoft Entra ID in your code

After you configure Microsoft Entra ID in your resource, update your code to use it when you consume the inference endpoint. The following example shows how to use a chat completions model:

Install the OpenAI SDK using a package manager like pip:

```
pip install openai
```


For Microsoft Entra ID authentication, also install:

```
pip install azure-identity
```


Use the package to consume the model. The following example shows how to create a client to consume chat completions with Microsoft Entra ID and make a test call to the chat completions endpoint with your model deployment.

Replace `<resource>`

with your Foundry resource name. Find it in the Azure portal or by running `az cognitiveservices account list`

. Replace `DeepSeek-V3.1`

with your actual deployment name.

```
from openai import OpenAI
from azure.identity import DefaultAzureCredential, get_bearer_token_provider
token_provider = get_bearer_token_provider(
DefaultAzureCredential(),
"https://cognitiveservices.azure.com/.default"
)
client = OpenAI(
base_url="https://<resource>.openai.azure.com/openai/v1/",
api_key=token_provider,
)
completion = client.chat.completions.create(
model="DeepSeek-V3.1", # Required: your deployment name
messages=[
{"role": "system", "content": "You are a helpful assistant."},
{"role": "user", "content": "What is Azure AI?"}
]
)
print(completion.choices[0].message.content)
```


Expected output

```
Azure AI is a comprehensive suite of artificial intelligence services and tools from Microsoft that enables developers to build intelligent applications. It includes services for natural language processing, computer vision, speech recognition, and machine learning capabilities.
```


Reference: [OpenAI Python SDK](https://github.com/openai/openai-python) and [DefaultAzureCredential class](/en-us/python/api/azure-identity/azure.identity.defaultazurecredential).

### Options for credential when using Microsoft Entra ID

`DefaultAzureCredential`

is an opinionated, ordered sequence of mechanisms for authenticating to Microsoft Entra ID. Each authentication mechanism is a class that's derived from the `TokenCredential`

class and is known as a credential. At runtime, `DefaultAzureCredential`

attempts to authenticate using the first credential. If that credential fails to acquire an access token, the next credential in the sequence is attempted, and so on, until an access token is obtained. In this way, your app can use different credentials in different environments without writing environment-specific code.

When the preceding code runs on your local development workstation, it looks in the environment variables for an application service principal or at locally installed developer tools, like Visual Studio, for a set of developer credentials. You can use either approach to authenticate the app to Azure resources during local development.

When deployed to Azure, this same code can also authenticate your app to other Azure resources. `DefaultAzureCredential`

can retrieve environment settings and managed identity configurations to authenticate to other services automatically.

### Best practices

Use deterministic credentials in production environments: Strongly consider moving from

`DefaultAzureCredential`

to one of the following deterministic solutions in production environments:- A specific
`TokenCredential`

implementation, like`ManagedIdentityCredential`

. See the[Derived list for options](/en-us/dotnet/api/azure.core.tokencredential#definition). - A pared-down
`ChainedTokenCredential`

implementation that's optimized for the Azure environment in which your app runs.`ChainedTokenCredential`

essentially creates a specific allowlist of acceptable credential options, like`ManagedIdentity`

for production and`VisualStudioCredential`

for development.

- A specific
Configure system-assigned or user-assigned managed identities to the Azure resources where your code runs, if possible. Configure Microsoft Entra ID access to those specific identities.


## Disable key-based authentication in the resource

Disable key-based authentication when you implement Microsoft Entra ID and fully address compatibility or fallback concerns in all the applications that consume the service.
Use PowerShell with the Azure CLI to disable local authentication for an individual resource. First sign in with the `Connect-AzAccount`

command. Then use the `Set-AzCognitiveServicesAccount`

cmdlet with the parameter `-DisableLocalAuth $true`

, like the following example:

```
Set-AzCognitiveServicesAccount -ResourceGroupName "my-resource-group" -Name "my-resource-name" -DisableLocalAuth $true
```


For more information about how to use the Azure CLI to disable or reenable local authentication and verify authentication status, see [Disable local authentication in Foundry Tools](../../../ai-services/disable-local-auth?view=foundry-classic).

Install the

[Azure CLI](/en-us/cli/azure/)Identify the following information:

- Your Azure subscription ID


## About this tutorial

The example in this article is based on code samples in the [Azure-Samples/azureai-model-inference-bicep](https://github.com/Azure-Samples/azureai-model-inference-bicep) repository. To run the commands locally without copying or pasting file content, clone the repository with these commands and go to the folder for your coding language:

```
git clone https://github.com/Azure-Samples/azureai-model-inference-bicep
```


The files for this example are in the following directory:

```
cd azureai-model-inference-bicep/infra
```


## Understand the resources

In this tutorial, you create the following resources:

- A Microsoft Foundry resource with key access disabled. For simplicity, this template doesn't deploy models.
- A role assignment for a given security principal with the role
**Cognitive Services User**.

To create these resources, use the following assets:

Use the template

`modules/ai-services-template.bicep`

to describe your Foundry resource.**modules/ai-services-template.bicep**`@description('Location of the resource.') param location string = resourceGroup().location @description('Name of the Azure AI Services account.') param accountName string @description('The resource model definition representing SKU') param sku string = 'S0' @description('Whether or not to allow keys for this account.') param allowKeys bool = true @allowed([ 'Enabled' 'Disabled' ]) @description('Whether or not public endpoint access is allowed for this account.') param publicNetworkAccess string = 'Enabled' @allowed([ 'Allow' 'Deny' ]) @description('The default action for network ACLs.') param networkAclsDefaultAction string = 'Allow' resource account 'Microsoft.CognitiveServices/accounts@2023-05-01' = { name: accountName location: location identity: { type: 'SystemAssigned' } sku: { name: sku } kind: 'AIServices' properties: { customSubDomainName: accountName publicNetworkAccess: publicNetworkAccess networkAcls: { defaultAction: networkAclsDefaultAction } disableLocalAuth: allowKeys } } output endpointUri string = 'https://${account.outputs.name}.services.ai.azure.com/models' output id string = account.id`

Tip

This template accepts the

`allowKeys`

parameter. Set it to`false`

to disable key access in the resource.Use the template

`modules/role-assignment-template.bicep`

to describe a role assignment in Azure:**modules/role-assignment-template.bicep**`@description('Specifies the role definition ID used in the role assignment.') param roleDefinitionID string @description('Specifies the principal ID assigned to the role.') param principalId string @description('Specifies the resource ID of the resource to assign the role to.') param scopeResourceId string = resourceGroup().id var roleAssignmentName= guid(principalId, roleDefinitionID, scopeResourceId) resource roleAssignment 'Microsoft.Authorization/roleAssignments@2022-04-01' = { name: roleAssignmentName properties: { roleDefinitionId: resourceId('Microsoft.Authorization/roleDefinitions', roleDefinitionID) principalId: principalId } } output name string = roleAssignment.name output resourceId string = roleAssignment.id`


## Create the resources

In your console, follow these steps:

Define the main deployment:

**deploy-entra-id.bicep**`@description('Location to create the resources in') param location string = resourceGroup().location @description('Name of the resource group to create the resources in') param resourceGroupName string = resourceGroup().name @description('Name of the AI Services account to create') param accountName string = 'azurei-models-dev' @description('ID of the developers to assign the user role to') param securityPrincipalId string module aiServicesAccount 'modules/ai-services-template.bicep' = { name: 'aiServicesAccount' scope: resourceGroup(resourceGroupName) params: { accountName: accountName location: location allowKeys: false } } module roleAssignmentDeveloperAccount 'modules/role-assignment-template.bicep' = { name: 'roleAssignmentDeveloperAccount' scope: resourceGroup(resourceGroupName) params: { roleDefinitionID: 'a97b65f3-24c7-4388-baec-2e87135dc908' // Azure Cognitive Services User principalId: securityPrincipalId } } output endpoint string = aiServicesAccount.outputs.endpointUri`

Sign in to Azure:

`az login`

Make sure you're in the right subscription:

`az account set --subscription "<subscription-id>"`

Run the deployment:

`RESOURCE_GROUP="<resource-group-name>" SECURITY_PRINCIPAL_ID="<your-security-principal-id>" az deployment group create \ --resource-group $RESOURCE_GROUP \ --parameters securityPrincipalId=$SECURITY_PRINCIPAL_ID \ --template-file deploy-entra-id.bicep`

The template outputs the Foundry Models endpoint that you can use to consume any of the model deployments you created.

Verify the deployment and role assignment:

`# Get the endpoint from deployment output ENDPOINT=$(az deployment group show --resource-group $RESOURCE_GROUP --name deploy-entra-id --query properties.outputs.endpoint.value --output tsv) # Verify role assignment RESOURCE_ID=$(az deployment group show --resource-group $RESOURCE_GROUP --name deploy-entra-id --query properties.outputs.resourceId.value --output tsv) az role assignment list --scope $RESOURCE_ID --assignee $SECURITY_PRINCIPAL_ID --query "[?roleDefinitionName=='Cognitive Services User'].roleDefinitionName" --output tsv # Test authentication by getting an access token az account get-access-token --resource https://cognitiveservices.azure.com --query "accessToken" --output tsv`

If successful, you see

**Cognitive Services User**from the role assignment check and an access token from the authentication test. You can now use this endpoint and Microsoft Entra ID authentication in your code.

## Use Microsoft Entra ID in your code

After you configure Microsoft Entra ID in your resource, update your code to use it when you consume the inference endpoint. The following example shows how to use a chat completions model.

Install the OpenAI SDK using a package manager like pip:

```
pip install openai
```


For Microsoft Entra ID authentication, also install:

```
pip install azure-identity
```


Use the package to consume the model. The following example shows how to create a client to consume chat completions with Microsoft Entra ID and make a test call to the chat completions endpoint with your model deployment.

Replace `<resource>`

with your Foundry resource name. Find it in the Azure portal or by running `az cognitiveservices account list`

. Replace `DeepSeek-V3.1`

with your actual deployment name.

```
from openai import OpenAI
from azure.identity import DefaultAzureCredential, get_bearer_token_provider
token_provider = get_bearer_token_provider(
DefaultAzureCredential(),
"https://cognitiveservices.azure.com/.default"
)
client = OpenAI(
base_url="https://<resource>.openai.azure.com/openai/v1/",
api_key=token_provider,
)
completion = client.chat.completions.create(
model="DeepSeek-V3.1", # Required: your deployment name
messages=[
{"role": "system", "content": "You are a helpful assistant."},
{"role": "user", "content": "What is Azure AI?"}
]
)
print(completion.choices[0].message.content)
```


Expected output

```
Azure AI is a comprehensive suite of artificial intelligence services and tools from Microsoft that enables developers to build intelligent applications. It includes services for natural language processing, computer vision, speech recognition, and machine learning capabilities.
```


Reference: [OpenAI Python SDK](https://github.com/openai/openai-python) and [DefaultAzureCredential class](/en-us/python/api/azure-identity/azure.identity.defaultazurecredential).

### Options for credential when using Microsoft Entra ID

`DefaultAzureCredential`

is an opinionated, ordered sequence of mechanisms for authenticating to Microsoft Entra ID. Each authentication mechanism is a class that's derived from the `TokenCredential`

class and is known as a credential. At runtime, `DefaultAzureCredential`

attempts to authenticate using the first credential. If that credential fails to acquire an access token, the next credential in the sequence is attempted, and so on, until an access token is obtained. In this way, your app can use different credentials in different environments without writing environment-specific code.

When the preceding code runs on your local development workstation, it looks in the environment variables for an application service principal or at locally installed developer tools, like Visual Studio, for a set of developer credentials. You can use either approach to authenticate the app to Azure resources during local development.

When deployed to Azure, this same code can also authenticate your app to other Azure resources. `DefaultAzureCredential`

can retrieve environment settings and managed identity configurations to authenticate to other services automatically.

### Best practices

Use deterministic credentials in production environments: Strongly consider moving from

`DefaultAzureCredential`

to one of the following deterministic solutions in production environments:- A specific
`TokenCredential`

implementation, like`ManagedIdentityCredential`

. See the[Derived list for options](/en-us/dotnet/api/azure.core.tokencredential#definition). - A pared-down
`ChainedTokenCredential`

implementation that's optimized for the Azure environment in which your app runs.`ChainedTokenCredential`

essentially creates a specific allowlist of acceptable credential options, like`ManagedIdentity`

for production and`VisualStudioCredential`

for development.

- A specific
Configure system-assigned or user-assigned managed identities to the Azure resources where your code runs, if possible. Configure Microsoft Entra ID access to those specific identities.


## Disable key-based authentication in the resource

Disable key-based authentication when you implement Microsoft Entra ID and fully address compatibility or fallback concerns in all applications that consume the service. Change the `disableLocalAuth`

property to disable key-based authentication.

For more information about how to disable local authentication when you're using a Bicep or ARM template, see [How to disable local authentication](../../../ai-services/disable-local-auth?view=foundry-classic#how-to-disable-local-authentication).

**modules/ai-services-template.bicep**

```
@description('Location of the resource.')
param location string = resourceGroup().location
@description('Name of the Azure AI Services account.')
param accountName string
@description('The resource model definition representing SKU')
param sku string = 'S0'
@description('Whether or not to allow keys for this account.')
param allowKeys bool = true
@allowed([
'Enabled'
'Disabled'
])
@description('Whether or not public endpoint access is allowed for this account.')
param publicNetworkAccess string = 'Enabled'
@allowed([
'Allow'
'Deny'
])
@description('The default action for network ACLs.')
param networkAclsDefaultAction string = 'Allow'
resource account 'Microsoft.CognitiveServices/accounts@2023-05-01' = {
name: accountName
location: location
identity: {
type: 'SystemAssigned'
}
sku: {
name: sku
}
kind: 'AIServices'
properties: {
customSubDomainName: accountName
publicNetworkAccess: publicNetworkAccess
networkAcls: {
defaultAction: networkAclsDefaultAction
}
disableLocalAuth: allowKeys
}
}
output endpointUri string = 'https://${account.outputs.name}.services.ai.azure.com/models'
output id string = account.id
```


## Understand roles in the context of resource in Azure

Microsoft Entra ID uses role-based access control (RBAC) for authorization, which controls what actions users can perform on Azure resources. Roles are central to managing access to cloud resources. A role is a collection of permissions that define what actions can be performed on specific Azure resources. By assigning roles to users, groups, service principals, or managed identities—collectively known as security principals—you control their access within your Azure environment to specific resources.

When you assign a role, you specify the security principal, role definition, and scope. This combination is known as a role assignment. Foundry Models is a capability of the Foundry Tools resources, therefore, roles assigned to that particular resource control the access for inference.

There are two types of access to the resources:

**Administration access**: Actions related to the administration of the resource. These actions usually change the resource state and its configuration. In Azure, these operations are control-plane operations that you can execute using the Azure portal, Azure CLI, or infrastructure as code. Examples include creating new model deployments, changing content filtering configurations, changing the version of the model served, or changing the SKU of a deployment.**Developer access**: Actions related to consuming the resources, such as invoking the chat completions API. However, the user can't change the resource state and its configuration.

In Azure, Microsoft Entra ID always performs administration operations. Roles like **Cognitive Services Contributor** allow you to perform those operations. Developer operations can be performed using either access keys or Microsoft Entra ID. Roles like **Cognitive Services User** allow you to perform those operations.

Important

Having administration access to a resource doesn't grant developer access to it. Explicit access by granting roles is still required. This is analogous to how database servers work. Having administrator access to the database server doesn't mean you can read the data inside of a database.

## Troubleshooting

Before you troubleshoot, verify that you have the right permissions assigned:

Go to the

[Azure portal](https://portal.azure.com)and locate the**Microsoft Foundry resource**that you're using.On the left pane, select

**Access control (IAM)**and then select**Check access**.Type the name of the user or identity you're using to connect to the service.

Verify that the role

**Cognitive Services User**is listed (or a role that contains the required permissions, as explained in the Prerequisites section).Important

Roles like

**Owner**or**Contributor**don't provide access via Microsoft Entra ID.If the role isn't listed, follow the steps in this guide before you continue.


The following table contains multiple scenarios that can help you troubleshoot Microsoft Entra ID:

| Error / Scenario | Root cause | Solution |
|---|---|---|
| You're using an SDK | Known issues | Before you troubleshoot further, install the latest version of the software you're using to connect to the service. Authentication bugs might already be fixed in a newer version of the software you're using. |
`401 Principal does not have access to API/Operation` |
The request indicates authentication in the correct way, but the user principal doesn't have the required permissions to use the inference endpoint. | Ensure you have: 1. Assigned the role Cognitive Services User to your principal to the Foundry resource. Notice that Cognitive Services OpenAI User grants only access to OpenAI models. Owner or Contributor don't provide access either.1. Waited at least 5 minutes before making the first call. |
`401 HTTP/1.1 401 PermissionDenied` |
The request indicates authentication in the correct way, but the user principal doesn't have the required permissions to use the inference endpoint. | Assigned the role Cognitive Services User to your principal in the Foundry resource. Roles like Administrator or Contributor don't grant inference access. Wait at least 5 minutes before making the first call. |
You're using REST API calls and you get `401 Unauthorized. Access token is missing, invalid, audience is incorrect, or have expired.` |
The request fails to authenticate with Microsoft Entra ID. | Ensure the `Authentication` header contains a valid token with a scope `https://cognitiveservices.azure.com/.default` . |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/how-to/use-chat-reasoning -->

# How to use reasoning models with Microsoft Foundry Models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Important

If you're currently using an Azure AI Inference beta SDK with Microsoft Foundry Models or Azure OpenAI service, we strongly recommend that you transition to the generally available [OpenAI/v1 API](https://aka.ms/openai/v1), which uses an OpenAI stable SDK.

For more information on how to migrate to the OpenAI/v1 API by using an SDK in your programming language of choice, see [Migrate from Azure AI Inference SDK to OpenAI SDK](../../how-to/model-inference-to-openai-migration?view=foundry-classic).

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

This article explains how to use the reasoning capabilities of chat completions models deployed in Microsoft Foundry Models.

## Reasoning models

Reasoning models can reach higher levels of performance in domains like math, coding, science, strategy, and logistics. The way these models produce outputs is by explicitly using chain of thought to explore all possible paths before generating an answer. They verify their answers as they produce them, which helps to arrive at more accurate conclusions. As a result, reasoning models might require less context prompts in order to produce effective results.

Reasoning models produce two types of content as outputs:

- Reasoning completions
- Output completions

Both of these completions count towards content generated from the model. Therefore, they contribute to the token limits and costs associated with the model. Some models, like `DeepSeek-R1`

, might respond with the reasoning content. Others, like `o1`

, output only the completions.

## Prerequisites

To complete this tutorial, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Microsoft Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry project. This kind of project is managed under a Foundry resource. If you don't have a Foundry project, see

[Create a project for Foundry (Foundry projects)](../../how-to/create-projects?view=foundry-classic).The endpoint's URL.

The endpoint's key (if you choose to use API key for authentication).


Install the SDK with the following command:

`pip install -U openai`


A model with reasoning capabilities model deployment. If you don't have one read

[Add and configure Foundry Models](create-model-deployments?view=foundry-classic)to add a reasoning model.- This example uses
`DeepSeek-R1`

.

- This example uses

## Use reasoning capabilities with chat

First, create the client to consume the model. The following code uses an endpoint URL and key that are stored in environment variables.

```
import os
from openai import AzureOpenAI
client = AzureOpenAI(
azure_endpoint = "https://<resource>.services.ai.azure.com",
api_key=os.getenv("AZURE_INFERENCE_CREDENTIAL"),
api_version="2024-10-21",
)
```


If you have configured the resource to with **Microsoft Entra ID** support, you can use the following code snippet to create a client.

```
import os
from openai import AzureOpenAI
from azure.identity import DefaultAzureCredential, get_bearer_token_provider
token_provider = get_bearer_token_provider(
DefaultAzureCredential(), "https://cognitiveservices.azure.com/.default"
)
client = AzureOpenAI(
azure_endpoint = "https://<resource>.services.ai.azure.com",
azure_ad_token_provider=token_provider,
api_version="2024-10-21",
)
```


### Prompt reasoning models

When building prompts for reasoning models, take the following into consideration:

- Use simple instructions and avoid using chain-of-thought techniques.
- Built-in reasoning capabilities make simple zero-shot prompts as effective as more complex methods.
- When providing additional context or documents, like in RAG scenarios, including only the most relevant information might help prevent the model from over-complicating its response.
- Reasoning models may support the use of system messages. However, they might not follow them as strictly as other non-reasoning models.
- When creating multi-turn applications, consider appending only the final answer from the model, without it's reasoning content, as explained in the
[Reasoning content](#reasoning-content)section.

Notice that reasoning models can take longer times to generate responses. They use long reasoning chains of thought that enable deeper and more structured problem-solving. They also perform self-verification to cross-check their answers and correct their mistakes, thereby showcasing emergent self-reflective behaviors.

### Create a chat completion request

The following example shows how you can create a basic chat request to the model.

```
response = client.chat.completions.create(
model="deepseek-r1",
messages=[
{"role": "user", "content": "How many languages are in the world?"}
]
)
```


The response is as follows, where you can see the model's usage statistics:

```
print("Response:", response.choices[0].message.content)
print("Model:", response.model)
print("Usage:")
print("\tPrompt tokens:", response.usage.prompt_tokens)
print("\tTotal tokens:", response.usage.total_tokens)
print("\tCompletion tokens:", response.usage.completion_tokens)
```


```
Response: As of now, it's estimated that there are about 7,000 languages spoken around the world. However, this number can vary as some languages become extinct and new ones develop. It's also important to note that the number of speakers can greatly vary between languages, with some having millions of speakers and others only a few hundred.
Model: deepseek-r1
Usage:
Prompt tokens: 11
Total tokens: 897
Completion tokens: 886
```


### Reasoning content

Note

This information on reasoning content does not apply to Azure OpenAI models. Azure OpenAI reasoning models use the [reasoning summaries feature](../../openai/how-to/reasoning?view=foundry-classic#reasoning-summary).

Some reasoning models, like DeepSeek-R1, generate completions and include the reasoning behind it.

The reasoning associated with the completion is included in the field `reasoning_content`

. The model may select on which scenarios to generate reasoning content.

```
print("Thinking:", response.choices[0].message.reasoning_content)
```


```
Thinking: Okay, the user is asking how many languages exist in the world. I need to provide a clear and accurate answer...
```


When making multi-turn conversations, it's useful to avoid sending the reasoning content in the chat history as reasoning tends to generate long explanations.

### Stream content

By default, the completions API returns the entire generated content in a single response. If you're generating long completions, waiting for the response can take many seconds.

You can *stream* the content to get it as it's being generated. Streaming content allows you to start processing the completion as content becomes available. This mode returns an object that streams back the response as [data-only server-sent events](https://html.spec.whatwg.org/multipage/server-sent-events.html#server-sent-events). Extract chunks from the delta field, rather than the message field.

To stream completions, set `stream=True`

when you call the model.

```
response = client.chat.completions.create(
model="deepseek-r1",
messages=[
{"role": "user", "content": "How many languages are in the world?"}
],
stream=True
)
```


To visualize the output, define a helper function to print the stream. The following example implements a routing that stream only the answer without the reasoning content:

Reasoning content is also included inside of the delta pieces of the response, in the key `reasoning_content`

.

```
def print_stream(completion):
"""
Prints the chat completion with streaming.
"""
is_thinking = False
for event in completion:
if event.choices:
content = event.choices[0].delta.content
reasoning_content = event.choices[0].delta.reasoning_content if hasattr(event.choices[0].delta, "reasoning_content") else None
if reasoning_content and not is_thinking:
is_thinking = True
print("🧠 Thinking...", end="", flush=True)
elif content:
if is_thinking:
is_thinking = False
print("🛑\n\n")
print(content or reasoning_content, end="", flush=True)
print_stream(response)
```


You can visualize how streaming generates content:

```
print_stream(response)
```


### Parameters

In general, reasoning models don't support the following parameters you can find in chat completion models:

- Temperature
- Presence penalty
- Repetition penalty
- Parameter
`top_p`


Some models support the use of tools or structured outputs (including JSON-schemas). Read the [Models](../concepts/models?view=foundry-classic) details page to understand each model's support.

### Apply Guardrails and controls

The Azure AI Model Inference API supports [Azure AI Content Safety](https://aka.ms/azureaicontentsafety). When you use deployments with Azure AI Content Safety turned on, inputs and outputs pass through an ensemble of classification models aimed at detecting and preventing the output of harmful content. The content filtering system detects and takes action on specific categories of potentially harmful content in both input prompts and output completions.

The following example shows how to handle events when the model detects harmful content in the input prompt.

```
try:
response = client.chat.completions.create(
model="deepseek-r1",
messages=[
{"role": "user", "content": "Chopping tomatoes and cutting them into cubes or wedges are great ways to practice your knife skills."}
],
)
print(response.choices[0].message.content)
except HttpResponseError as ex:
if ex.status_code == 400:
response = ex.response.json()
if isinstance(response, dict) and "error" in response:
print(f"Your request triggered an {response['error']['code']} error:\n\t {response['error']['message']}")
else:
raise
raise
```


Tip

To learn more about how you can configure and control Azure AI Content Safety settings, check the [Azure AI Content Safety documentation](https://aka.ms/azureaicontentsafety).

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

This article explains how to use the reasoning capabilities of chat completions models deployed in Microsoft Foundry Models.

## Reasoning models

Reasoning models can reach higher levels of performance in domains like math, coding, science, strategy, and logistics. The way these models produce outputs is by explicitly using chain of thought to explore all possible paths before generating an answer. They verify their answers as they produce them, which helps to arrive at more accurate conclusions. As a result, reasoning models might require less context prompts in order to produce effective results.

Reasoning models produce two types of content as outputs:

- Reasoning completions
- Output completions

Both of these completions count towards content generated from the model. Therefore, they contribute to the token limits and costs associated with the model. Some models, like `DeepSeek-R1`

, might respond with the reasoning content. Others, like `o1`

, output only the completions.

## Prerequisites

To complete this tutorial, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Microsoft Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry project. This kind of project is managed under a Foundry resource. If you don't have a Foundry project, see

[Create a project for Foundry (Foundry projects)](../../how-to/create-projects?view=foundry-classic).The endpoint's URL.

The endpoint's key (if you choose to use API key for authentication).


Install the

[Azure Inference library for JavaScript](https://aka.ms/azsdk/azure-ai-inference/javascript/reference)with the following command:`npm install @azure-rest/ai-inference npm install @azure/core-auth npm install @azure/identity`

If you are using Node.js, you can configure the dependencies in

**package.json**:**package.json**`{ "name": "main_app", "version": "1.0.0", "description": "", "main": "app.js", "type": "module", "dependencies": { "@azure-rest/ai-inference": "1.0.0-beta.6", "@azure/core-auth": "1.9.0", "@azure/core-sse": "2.2.0", "@azure/identity": "4.8.0" } }`

Import the following:

`import ModelClient from "@azure-rest/ai-inference"; import { isUnexpected } from "@azure-rest/ai-inference"; import { createSseStream } from "@azure/core-sse"; import { AzureKeyCredential } from "@azure/core-auth"; import { DefaultAzureCredential } from "@azure/identity";`


A model with reasoning capabilities model deployment. If you don't have one read

[Add and configure Foundry Models](create-model-deployments?view=foundry-classic)to add a reasoning model.- This example uses
`DeepSeek-R1`

.

- This example uses

## Use reasoning capabilities with chat

First, create the client to consume the model. The following code uses an endpoint URL and key that are stored in environment variables.

```
const client = ModelClient(
"https://<resource>.services.ai.azure.com/models",
new AzureKeyCredential(process.env.AZURE_INFERENCE_CREDENTIAL)
);
```


If you've configured the resource with **Microsoft Entra ID** support, you can use the following code snippet to create a client.

```
const clientOptions = { credentials: { "https://cognitiveservices.azure.com/.default" } };
const client = ModelClient(
"https://<resource>.services.ai.azure.com/models",
new DefaultAzureCredential()
clientOptions,
);
```


### Prompt reasoning models

When building prompts for reasoning models, take the following into consideration:

- Use simple instructions and avoid using chain-of-thought techniques.
- Built-in reasoning capabilities make simple zero-shot prompts as effective as more complex methods.
- When providing additional context or documents, like in RAG scenarios, including only the most relevant information might help prevent the model from over-complicating its response.
- Reasoning models may support the use of system messages. However, they might not follow them as strictly as other non-reasoning models.
- When creating multi-turn applications, consider appending only the final answer from the model, without it's reasoning content, as explained in the
[Reasoning content](#reasoning-content)section.

Notice that reasoning models can take longer times to generate responses. They use long reasoning chains of thought that enable deeper and more structured problem-solving. They also perform self-verification to cross-check their answers and correct their mistakes, thereby showcasing emergent self-reflective behaviors.

### Create a chat completion request

The following example shows how you can create a basic chat request to the model.

```
var messages = [
{ role: "user", content: "How many languages are in the world?" },
];
var response = await client.path("/chat/completions").post({
body: {
model: "DeepSeek-R1",
messages: messages,
}
});
```


The response is as follows, where you can see the model's usage statistics:

```
if (isUnexpected(response)) {
throw response.body.error;
}
console.log("Response: ", response.body.choices[0].message.content);
console.log("Model: ", response.body.model);
console.log("Usage:");
console.log("\tPrompt tokens:", response.body.usage.prompt_tokens);
console.log("\tTotal tokens:", response.body.usage.total_tokens);
console.log("\tCompletion tokens:", response.body.usage.completion_tokens);
```


```
Response: <think>Okay, the user is asking how many languages exist in the world. I need to provide a clear and accurate answer...</think>As of now, it's estimated that there are about 7,000 languages spoken around the world. However, this number can vary as some languages become extinct and new ones develop. It's also important to note that the number of speakers can greatly vary between languages, with some having millions of speakers and others only a few hundred.
Model: deepseek-r1
Usage:
Prompt tokens: 11
Total tokens: 897
Completion tokens: 886
```


### Reasoning content

Note

This information on reasoning content does not apply to Azure OpenAI models. Azure OpenAI reasoning models use the [reasoning summaries feature](../../openai/how-to/reasoning?view=foundry-classic#reasoning-summary).

Some reasoning models, like DeepSeek-R1, generate completions and include the reasoning behind it. The reasoning associated with the completion is included in the response's content within the tags `<think>`

and `</think>`

. The model may select on which scenarios to generate reasoning content. You can extract the reasoning content from the response to understand the model's thought process as follows:

```
var content = response.body.choices[0].message.content
var match = content.match(/<think>(.*?)<\/think>(.*)/s);
console.log("Response:");
if (match) {
console.log("\tThinking:", match[1]);
console.log("\Answer:", match[2]);
}
else {
console.log("Response:", content);
}
console.log("Model: ", response.body.model);
console.log("Usage:");
console.log("\tPrompt tokens:", response.body.usage.prompt_tokens);
console.log("\tTotal tokens:", response.body.usage.total_tokens);
console.log("\tCompletion tokens:", response.body.usage.completion_tokens);
```


```
Thinking: Okay, the user is asking how many languages exist in the world. I need to provide a clear and accurate answer. Let's start by recalling the general consensus from linguistic sources. I remember that the number often cited is around 7,000, but maybe I should check some reputable organizations.\n\nEthnologue is a well-known resource for language data, and I think they list about 7,000 languages. But wait, do they update their numbers? It might be around 7,100 or so. Also, the exact count can vary because some sources might categorize dialects differently or have more recent data. \n\nAnother thing to consider is language endangerment. Many languages are endangered, with some having only a few speakers left. Organizations like UNESCO track endangered languages, so mentioning that adds context. Also, the distribution isn't even. Some countries have hundreds of languages, like Papua New Guinea with over 800, while others have just a few. \n\nA user might also wonder why the exact number is hard to pin down. It's because the distinction between a language and a dialect can be political or cultural. For example, Mandarin and Cantonese are considered dialects of Chinese by some, but they're mutually unintelligible, so others classify them as separate languages. Also, some regions are under-researched, making it hard to document all languages. \n\nI should also touch on language families. The 7,000 languages are grouped into families like Indo-European, Sino-Tibetan, Niger-Congo, etc. Maybe mention a few of the largest families. But wait, the question is just about the count, not the families. Still, it's good to provide a bit more context. \n\nI need to make sure the information is up-to-date. Let me think – recent estimates still hover around 7,000. However, languages are dying out rapidly, so the number decreases over time. Including that note about endangerment and language extinction rates could be helpful. For instance, it's often stated that a language dies every few weeks. \n\nAnother point is sign languages. Does the count include them? Ethnologue includes some, but not all sources might. If the user is including sign languages, that adds more to the count, but I think the 7,000 figure typically refers to spoken languages. For thoroughness, maybe mention that there are also over 300 sign languages. \n\nSummarizing, the answer should state around 7,000, mention Ethnologue's figure, explain why the exact number varies, touch on endangerment, and possibly note sign languages as a separate category. Also, a brief mention of Papua New Guinea as the most linguistically diverse country. \n\nWait, let me verify Ethnologue's current number. As of their latest edition (25th, 2022), they list 7,168 living languages. But I should check if that's the case. Some sources might round to 7,000. Also, SIL International publishes Ethnologue, so citing them as reference makes sense. \n\nOther sources, like Glottolog, might have a different count because they use different criteria. Glottolog might list around 7,000 as well, but exact numbers vary. It's important to highlight that the count isn't exact because of differing definitions and ongoing research. \n\nIn conclusion, the approximate number is 7,000, with Ethnologue being a key source, considerations of endangerment, and the challenges in counting due to dialect vs. language distinctions. I should make sure the answer is clear, acknowledges the variability, and provides key points succinctly.
Answer: The exact number of languages in the world is challenging to determine due to differences in definitions (e.g., distinguishing languages from dialects) and ongoing documentation efforts. However, widely cited estimates suggest there are approximately **7,000 languages** globally.
Model: DeepSeek-R1
Usage:
Prompt tokens: 11
Total tokens: 897
Completion tokens: 886
```


When making multi-turn conversations, it's useful to avoid sending the reasoning content in the chat history as reasoning tends to generate long explanations.

### Stream content

By default, the completions API returns the entire generated content in a single response. If you're generating long completions, waiting for the response can take many seconds.

You can *stream* the content to get it as it's being generated. Streaming content allows you to start processing the completion as content becomes available. This mode returns an object that streams back the response as [data-only server-sent events](https://html.spec.whatwg.org/multipage/server-sent-events.html#server-sent-events). Extract chunks from the delta field, rather than the message field.

To stream completions, set `stream=True`

when you call the model.

```
var messages = [
{ role: "user", content: "How many languages are in the world?" },
];
var response = await client.path("/chat/completions").post({
body: {
model: "DeepSeek-R1",
messages: messages,
stream: true
}
}).asNodeStream();
```


To visualize the output, define a helper function to print the stream. The following example implements a routing that stream only the answer without the reasoning content:

```
async function printStream(sses) {
let isThinking = false;
for await (const event of sses) {
if (event.data === "[DONE]") {
return;
}
for (const choice of (JSON.parse(event.data)).choices) {
const content = choice.delta?.content ?? "";
if (content === "<think>") {
isThinking = true;
process.stdout.write("🧠 Thinking...");
} else if (content === "</think>") {
isThinking = false;
console.log("🛑\n\n");
} else if (content) {
process.stdout.write(content);
}
}
}
}
```


You can visualize how streaming generates content:

```
var sses = createSseStream(response.body);
await printStream(sses)
```


### Parameters

In general, reasoning models don't support the following parameters you can find in chat completion models:

- Temperature
- Presence penalty
- Repetition penalty
- Parameter
`top_p`


Some models support the use of tools or structured outputs (including JSON-schemas). Read the [Models](../concepts/models?view=foundry-classic) details page to understand each model's support.

### Apply Guardrails and controls

The Azure AI Model Inference API supports [Azure AI Content Safety](https://aka.ms/azureaicontentsafety). When you use deployments with Azure AI Content Safety turned on, inputs and outputs pass through an ensemble of classification models aimed at detecting and preventing the output of harmful content. The content filtering system detects and takes action on specific categories of potentially harmful content in both input prompts and output completions.

The following example shows how to handle events when the model detects harmful content in the input prompt.

```
try {
var messages = [
{ role: "system", content: "You are an AI assistant that helps people find information." },
{ role: "user", content: "Chopping tomatoes and cutting them into cubes or wedges are great ways to practice your knife skills." },
];
var response = await client.path("/chat/completions").post({
model: "DeepSeek-R1",
body: {
messages: messages,
}
});
console.log(response.body.choices[0].message.content);
}
catch (error) {
if (error.status_code == 400) {
var response = JSON.parse(error.response._content);
if (response.error) {
console.log(`Your request triggered an ${response.error.code} error:\n\t ${response.error.message}`);
}
else
{
throw error;
}
}
}
```


Tip

To learn more about how you can configure and control Azure AI Content Safety settings, check the [Azure AI Content Safety documentation](https://aka.ms/azureaicontentsafety).

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

This article explains how to use the reasoning capabilities of chat completions models deployed in Microsoft Foundry Models.

## Reasoning models

Reasoning models can reach higher levels of performance in domains like math, coding, science, strategy, and logistics. The way these models produce outputs is by explicitly using chain of thought to explore all possible paths before generating an answer. They verify their answers as they produce them, which helps to arrive at more accurate conclusions. As a result, reasoning models might require less context prompts in order to produce effective results.

Reasoning models produce two types of content as outputs:

- Reasoning completions
- Output completions

Both of these completions count towards content generated from the model. Therefore, they contribute to the token limits and costs associated with the model. Some models, like `DeepSeek-R1`

, might respond with the reasoning content. Others, like `o1`

, output only the completions.

## Prerequisites

To complete this tutorial, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Microsoft Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry project. This kind of project is managed under a Foundry resource. If you don't have a Foundry project, see

[Create a project for Foundry (Foundry projects)](../../how-to/create-projects?view=foundry-classic).The endpoint's URL.

The endpoint's key (if you choose to use API key for authentication).


Add the

[Azure AI inference package](https://aka.ms/azsdk/azure-ai-inference/java/reference)to your project:`<dependency> <groupId>com.azure</groupId> <artifactId>azure-ai-inference</artifactId> <version>1.0.0-beta.4</version> </dependency>`

If you are using Entra ID, you also need the following package:

`<dependency> <groupId>com.azure</groupId> <artifactId>azure-identity</artifactId> <version>1.15.3</version> </dependency>`

Import the following namespace:

`package com.azure.ai.inference.usage; import com.azure.ai.inference.EmbeddingsClient; import com.azure.ai.inference.EmbeddingsClientBuilder; import com.azure.ai.inference.ChatCompletionsClient; import com.azure.ai.inference.ChatCompletionsClientBuilder; import com.azure.ai.inference.models.EmbeddingsResult; import com.azure.ai.inference.models.EmbeddingItem; import com.azure.ai.inference.models.ChatCompletions; import com.azure.core.credential.AzureKeyCredential; import com.azure.core.util.Configuration; import java.util.ArrayList; import java.util.List;`


A model with reasoning capabilities model deployment. If you don't have one read

[Add and configure Foundry Models](create-model-deployments?view=foundry-classic)to add a reasoning model.- This example uses
`DeepSeek-R1`

.

- This example uses

## Use reasoning capabilities with chat

First, create the client to consume the model. The following code uses an endpoint URL and key that are stored in environment variables.

```
ChatCompletionsClient client = new ChatCompletionsClient(
new URI("https://<resource>.services.ai.azure.com/models"),
new AzureKeyCredential(System.getProperty("AZURE_INFERENCE_CREDENTIAL")),
```


Tip

Verify that you have deployed the model to Foundry Tools resource with the Azure AI Model Inference API. `Deepseek-R1`

is also available as serverless API deployments. However, those endpoints don't take the parameter `model`

as explained in this tutorial. You can verify that by going to [Foundry portal] > Models + endpoints, and verify that the model is listed under the section **Foundry Tools**.

If you have configured the resource to with **Microsoft Entra ID** support, you can use the following code snippet to create a client.

```
client = new ChatCompletionsClient(
new URI("https://<resource>.services.ai.azure.com/models"),
new DefaultAzureCredentialBuilder().build()
);
```


### Prompt reasoning models

When building prompts for reasoning models, take the following into consideration:

- Use simple instructions and avoid using chain-of-thought techniques.
- Built-in reasoning capabilities make simple zero-shot prompts as effective as more complex methods.
- When providing additional context or documents, like in RAG scenarios, including only the most relevant information might help prevent the model from over-complicating its response.
- Reasoning models may support the use of system messages. However, they might not follow them as strictly as other non-reasoning models.
- When creating multi-turn applications, consider appending only the final answer from the model, without it's reasoning content, as explained in the
[Reasoning content](#reasoning-content)section.

Notice that reasoning models can take longer times to generate responses. They use long reasoning chains of thought that enable deeper and more structured problem-solving. They also perform self-verification to cross-check their answers and correct their mistakes, thereby showcasing emergent self-reflective behaviors.

### Create a chat completion request

The following example shows how you can create a basic chat request to the model.

```
ChatCompletionsOptions requestOptions = new ChatCompletionsOptions()
.setModel("DeepSeek-R1")
.setMessages(Arrays.asList(
new ChatRequestUserMessage("How many languages are in the world?")
));
Response<ChatCompletions> response = client.complete(requestOptions);
```


The response is as follows, where you can see the model's usage statistics:

```
System.out.println("Response: " + response.getValue().getChoices().get(0).getMessage().getContent());
System.out.println("Model: " + response.getValue().getModel());
System.out.println("Usage:");
System.out.println("\tPrompt tokens: " + response.getValue().getUsage().getPromptTokens());
System.out.println("\tTotal tokens: " + response.getValue().getUsage().getTotalTokens());
System.out.println("\tCompletion tokens: " + response.getValue().getUsage().getCompletionTokens());
```


```
Response: <think>Okay, the user is asking how many languages exist in the world. I need to provide a clear and accurate...</think>The exact number of languages in the world is challenging to determine due to differences in definitions (e.g., distinguishing languages from dialects) and ongoing documentation efforts. However, widely cited estimates suggest there are approximately **7,000 languages** globally.
Model: deepseek-r1
Usage:
Prompt tokens: 11
Total tokens: 897
Completion tokens: 886
```


### Reasoning content

Note

This information on reasoning content does not apply to Azure OpenAI models. Azure OpenAI reasoning models use the [reasoning summaries feature](../../openai/how-to/reasoning?view=foundry-classic#reasoning-summary).

Some reasoning models, like DeepSeek-R1, generate completions and include the reasoning behind it. The reasoning associated with the completion is included in the response's content within the tags `<think>`

and `</think>`

. The model may select on which scenarios to generate reasoning content. You can extract the reasoning content from the response to understand the model's thought process as follows:

```
String content = response.getValue().getChoices().get(0).getMessage().getContent()
Pattern pattern = Pattern.compile("<think>(.*?)</think>(.*)", Pattern.DOTALL);
Matcher matcher = pattern.matcher(content);
System.out.println("Response:");
if (matcher.find()) {
System.out.println("\tThinking: " + matcher.group(1));
System.out.println("\tAnswer: " + matcher.group(2));
}
else {
System.out.println("Response: " + content);
}
System.out.println("Model: " + response.getValue().getModel());
System.out.println("Usage:");
System.out.println("\tPrompt tokens: " + response.getValue().getUsage().getPromptTokens());
System.out.println("\tTotal tokens: " + response.getValue().getUsage().getTotalTokens());
System.out.println("\tCompletion tokens: " + response.getValue().getUsage().getCompletionTokens());
```


```
Thinking: Okay, the user is asking how many languages exist in the world. I need to provide a clear and accurate answer. Let's start by recalling the general consensus from linguistic sources. I remember that the number often cited is around 7,000, but maybe I should check some reputable organizations.\n\nEthnologue is a well-known resource for language data, and I think they list about 7,000 languages. But wait, do they update their numbers? It might be around 7,100 or so. Also, the exact count can vary because some sources might categorize dialects differently or have more recent data. \n\nAnother thing to consider is language endangerment. Many languages are endangered, with some having only a few speakers left. Organizations like UNESCO track endangered languages, so mentioning that adds context. Also, the distribution isn't even. Some countries have hundreds of languages, like Papua New Guinea with over 800, while others have just a few. \n\nA user might also wonder why the exact number is hard to pin down. It's because the distinction between a language and a dialect can be political or cultural. For example, Mandarin and Cantonese are considered dialects of Chinese by some, but they're mutually unintelligible, so others classify them as separate languages. Also, some regions are under-researched, making it hard to document all languages. \n\nI should also touch on language families. The 7,000 languages are grouped into families like Indo-European, Sino-Tibetan, Niger-Congo, etc. Maybe mention a few of the largest families. But wait, the question is just about the count, not the families. Still, it's good to provide a bit more context. \n\nI need to make sure the information is up-to-date. Let me think – recent estimates still hover around 7,000. However, languages are dying out rapidly, so the number decreases over time. Including that note about endangerment and language extinction rates could be helpful. For instance, it's often stated that a language dies every few weeks. \n\nAnother point is sign languages. Does the count include them? Ethnologue includes some, but not all sources might. If the user is including sign languages, that adds more to the count, but I think the 7,000 figure typically refers to spoken languages. For thoroughness, maybe mention that there are also over 300 sign languages. \n\nSummarizing, the answer should state around 7,000, mention Ethnologue's figure, explain why the exact number varies, touch on endangerment, and possibly note sign languages as a separate category. Also, a brief mention of Papua New Guinea as the most linguistically diverse country. \n\nWait, let me verify Ethnologue's current number. As of their latest edition (25th, 2022), they list 7,168 living languages. But I should check if that's the case. Some sources might round to 7,000. Also, SIL International publishes Ethnologue, so citing them as reference makes sense. \n\nOther sources, like Glottolog, might have a different count because they use different criteria. Glottolog might list around 7,000 as well, but exact numbers vary. It's important to highlight that the count isn't exact because of differing definitions and ongoing research. \n\nIn conclusion, the approximate number is 7,000, with Ethnologue being a key source, considerations of endangerment, and the challenges in counting due to dialect vs. language distinctions. I should make sure the answer is clear, acknowledges the variability, and provides key points succinctly.
Answer: The exact number of languages in the world is challenging to determine due to differences in definitions (e.g., distinguishing languages from dialects) and ongoing documentation efforts. However, widely cited estimates suggest there are approximately **7,000 languages** globally.
Model: DeepSeek-R1
Usage:
Prompt tokens: 11
Total tokens: 897
Completion tokens: 886
```


When making multi-turn conversations, it's useful to avoid sending the reasoning content in the chat history as reasoning tends to generate long explanations.

### Stream content

By default, the completions API returns the entire generated content in a single response. If you're generating long completions, waiting for the response can take many seconds.

You can *stream* the content to get it as it's being generated. Streaming content allows you to start processing the completion as content becomes available. This mode returns an object that streams back the response as [data-only server-sent events](https://html.spec.whatwg.org/multipage/server-sent-events.html#server-sent-events). Extract chunks from the delta field, rather than the message field.

```
ChatCompletionsOptions requestOptions = new ChatCompletionsOptions()
.setModel("DeepSeek-R1")
.setMessages(Arrays.asList(
new ChatRequestUserMessage("How many languages are in the world? Write an essay about it.")
))
.setMaxTokens(4096);
return client.completeStreamingAsync(requestOptions).thenAcceptAsync(response -> {
try {
printStream(response);
} catch (Exception e) {
throw new RuntimeException(e);
}
});
```


To visualize the output, define a helper function to print the stream. The following example implements a routing that stream only the answer without the reasoning content:

```
public void printStream(StreamingResponse<StreamingChatCompletionsUpdate> response) throws Exception {
boolean isThinking = false;
for (StreamingChatCompletionsUpdate chatUpdate : response) {
if (chatUpdate.getContentUpdate() != null && !chatUpdate.getContentUpdate().isEmpty()) {
String content = chatUpdate.getContentUpdate();
if ("<think>".equals(content)) {
isThinking = true;
System.out.print("🧠 Thinking...");
System.out.flush();
} else if ("</think>".equals(content)) {
isThinking = false;
System.out.println("🛑\n\n");
} else if (content != null && !content.isEmpty()) {
System.out.print(content);
System.out.flush();
}
}
}
}
```


You can visualize how streaming generates content:

```
try {
streamMessageAsync(client).get();
} catch (Exception e) {
throw new RuntimeException(e);
}
```


### Parameters

In general, reasoning models don't support the following parameters you can find in chat completion models:

- Temperature
- Presence penalty
- Repetition penalty
- Parameter
`top_p`


Some models support the use of tools or structured outputs (including JSON-schemas). Read the [Models](../concepts/models?view=foundry-classic) details page to understand each model's support.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

This article explains how to use the reasoning capabilities of chat completions models deployed in Microsoft Foundry Models.

## Reasoning models

Reasoning models can reach higher levels of performance in domains like math, coding, science, strategy, and logistics. The way these models produce outputs is by explicitly using chain of thought to explore all possible paths before generating an answer. They verify their answers as they produce them, which helps to arrive at more accurate conclusions. As a result, reasoning models might require less context prompts in order to produce effective results.

Reasoning models produce two types of content as outputs:

- Reasoning completions
- Output completions

Both of these completions count towards content generated from the model. Therefore, they contribute to the token limits and costs associated with the model. Some models, like `DeepSeek-R1`

, might respond with the reasoning content. Others, like `o1`

, output only the completions.

## Prerequisites

To complete this tutorial, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Microsoft Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry project. This kind of project is managed under a Foundry resource. If you don't have a Foundry project, see

[Create a project for Foundry (Foundry projects)](../../how-to/create-projects?view=foundry-classic).The endpoint's URL.

The endpoint's key (if you choose to use API key for authentication).


Install the

[Azure AI inference package](https://aka.ms/azsdk/azure-ai-inference/python/reference)with the following command:`dotnet add package Azure.AI.Inference --prerelease`

If you are using Entra ID, you also need the following package:

`dotnet add package Azure.Identity`


A model with reasoning capabilities model deployment. If you don't have one read

[Add and configure Foundry Models](create-model-deployments?view=foundry-classic)to add a reasoning model.- This example uses
`DeepSeek-R1`

.

- This example uses

## Use reasoning capabilities with chat

First, create the client to consume the model. The following code uses an endpoint URL and key that are stored in environment variables.

```
AzureAIInferenceClientOptions clientOptions = new AzureAIInferenceClientOptions(apiVersion);
ChatCompletionsClient client = new ChatCompletionsClient(
new Uri("https://<resource>.services.ai.azure.com/models"),
new AzureKeyCredential(Environment.GetEnvironmentVariable("AZURE_INFERENCE_CREDENTIAL")),
clientOptions
);
```


If you have configured the resource to with **Microsoft Entra ID** support, you can use the following code snippet to create a client.

```
AzureAIInferenceClientOptions clientOptions = new AzureAIInferenceClientOptions(
"2024-05-01-preview",
new string[] { "https://cognitiveservices.azure.com/.default" }
);
client = new ChatCompletionsClient(
new Uri("https://<resource>.services.ai.azure.com/models"),
new DefaultAzureCredential(),
clientOptions,
);
```


### Prompt reasoning models

When building prompts for reasoning models, take the following into consideration:

- Use simple instructions and avoid using chain-of-thought techniques.
- Built-in reasoning capabilities make simple zero-shot prompts as effective as more complex methods.
- When providing additional context or documents, like in RAG scenarios, including only the most relevant information might help prevent the model from over-complicating its response.
- Reasoning models may support the use of system messages. However, they might not follow them as strictly as other non-reasoning models.
- When creating multi-turn applications, consider appending only the final answer from the model, without it's reasoning content, as explained in the
[Reasoning content](#reasoning-content)section.

Notice that reasoning models can take longer times to generate responses. They use long reasoning chains of thought that enable deeper and more structured problem-solving. They also perform self-verification to cross-check their answers and correct their mistakes, thereby showcasing emergent self-reflective behaviors.

### Create a chat completion request

The following example shows how you can create a basic chat request to the model.

```
ChatCompletionsOptions requestOptions = new ChatCompletionsOptions()
{
Messages = {
new ChatRequestUserMessage("How many languages are in the world?")
},
Model = "deepseek-r1",
};
Response<ChatCompletions> response = client.Complete(requestOptions);
```


The response is as follows, where you can see the model's usage statistics:

```
Console.WriteLine($"Response: {response.Value.Content}");
Console.WriteLine($"Model: {response.Value.Model}");
Console.WriteLine("Usage:");
Console.WriteLine($"\tPrompt tokens: {response.Value.Usage.PromptTokens}");
Console.WriteLine($"\tTotal tokens: {response.Value.Usage.TotalTokens}");
Console.WriteLine($"\tCompletion tokens: {response.Value.Usage.CompletionTokens}");
```


```
Response: <think>Okay, the user is asking how many languages exist in the world. I need to provide a clear and accurate...</think>The exact number of languages in the world is challenging to determine due to differences in definitions (e.g., distinguishing languages from dialects) and ongoing documentation efforts. However, widely cited estimates suggest there are approximately **7,000 languages** globally.
Model: deepseek-r1
Usage:
Prompt tokens: 11
Total tokens: 897
Completion tokens: 886
```


### Reasoning content

Note

This information on reasoning content does not apply to Azure OpenAI models. Azure OpenAI reasoning models use the [reasoning summaries feature](../../openai/how-to/reasoning?view=foundry-classic#reasoning-summary).

Some reasoning models, like DeepSeek-R1, generate completions and include the reasoning behind it. The reasoning associated with the completion is included in the response's content within the tags `<think>`

and `</think>`

. The model may select on which scenarios to generate reasoning content. You can extract the reasoning content from the response to understand the model's thought process as follows:

```
Regex regex = new Regex(pattern, RegexOptions.Singleline);
Match match = regex.Match(response.Value.Content);
Console.WriteLine("Response:");
if (match.Success)
{
Console.WriteLine($"\tThinking: {match.Groups[1].Value}");
Console.WriteLine($"\tAnswer: {match.Groups[2].Value}");
else
{
Console.WriteLine($"Response: {response.Value.Content}");
}
Console.WriteLine($"Model: {response.Value.Model}");
Console.WriteLine("Usage:");
Console.WriteLine($"\tPrompt tokens: {response.Value.Usage.PromptTokens}");
Console.WriteLine($"\tTotal tokens: {response.Value.Usage.TotalTokens}");
Console.WriteLine($"\tCompletion tokens: {response.Value.Usage.CompletionTokens}");
```


```
Thinking: Okay, the user is asking how many languages exist in the world. I need to provide a clear and accurate answer. Let's start by recalling the general consensus from linguistic sources. I remember that the number often cited is around 7,000, but maybe I should check some reputable organizations.\n\nEthnologue is a well-known resource for language data, and I think they list about 7,000 languages. But wait, do they update their numbers? It might be around 7,100 or so. Also, the exact count can vary because some sources might categorize dialects differently or have more recent data. \n\nAnother thing to consider is language endangerment. Many languages are endangered, with some having only a few speakers left. Organizations like UNESCO track endangered languages, so mentioning that adds context. Also, the distribution isn't even. Some countries have hundreds of languages, like Papua New Guinea with over 800, while others have just a few. \n\nA user might also wonder why the exact number is hard to pin down. It's because the distinction between a language and a dialect can be political or cultural. For example, Mandarin and Cantonese are considered dialects of Chinese by some, but they're mutually unintelligible, so others classify them as separate languages. Also, some regions are under-researched, making it hard to document all languages. \n\nI should also touch on language families. The 7,000 languages are grouped into families like Indo-European, Sino-Tibetan, Niger-Congo, etc. Maybe mention a few of the largest families. But wait, the question is just about the count, not the families. Still, it's good to provide a bit more context. \n\nI need to make sure the information is up-to-date. Let me think – recent estimates still hover around 7,000. However, languages are dying out rapidly, so the number decreases over time. Including that note about endangerment and language extinction rates could be helpful. For instance, it's often stated that a language dies every few weeks. \n\nAnother point is sign languages. Does the count include them? Ethnologue includes some, but not all sources might. If the user is including sign languages, that adds more to the count, but I think the 7,000 figure typically refers to spoken languages. For thoroughness, maybe mention that there are also over 300 sign languages. \n\nSummarizing, the answer should state around 7,000, mention Ethnologue's figure, explain why the exact number varies, touch on endangerment, and possibly note sign languages as a separate category. Also, a brief mention of Papua New Guinea as the most linguistically diverse country. \n\nWait, let me verify Ethnologue's current number. As of their latest edition (25th, 2022), they list 7,168 living languages. But I should check if that's the case. Some sources might round to 7,000. Also, SIL International publishes Ethnologue, so citing them as reference makes sense. \n\nOther sources, like Glottolog, might have a different count because they use different criteria. Glottolog might list around 7,000 as well, but exact numbers vary. It's important to highlight that the count isn't exact because of differing definitions and ongoing research. \n\nIn conclusion, the approximate number is 7,000, with Ethnologue being a key source, considerations of endangerment, and the challenges in counting due to dialect vs. language distinctions. I should make sure the answer is clear, acknowledges the variability, and provides key points succinctly.
Answer: The exact number of languages in the world is challenging to determine due to differences in definitions (e.g., distinguishing languages from dialects) and ongoing documentation efforts. However, widely cited estimates suggest there are approximately **7,000 languages** globally.
Model: DeepSeek-R1
Usage:
Prompt tokens: 11
Total tokens: 897
Completion tokens: 886
```


When making multi-turn conversations, it's useful to avoid sending the reasoning content in the chat history as reasoning tends to generate long explanations.

### Stream content

By default, the completions API returns the entire generated content in a single response. If you're generating long completions, waiting for the response can take many seconds.

You can *stream* the content to get it as it's being generated. Streaming content allows you to start processing the completion as content becomes available. This mode returns an object that streams back the response as [data-only server-sent events](https://html.spec.whatwg.org/multipage/server-sent-events.html#server-sent-events). Extract chunks from the delta field, rather than the message field.

```
static async Task StreamMessageAsync(ChatCompletionsClient client)
{
ChatCompletionsOptions requestOptions = new ChatCompletionsOptions()
{
Messages = {
new ChatRequestUserMessage("How many languages are in the world?")
},
MaxTokens=4096,
Model = "deepseek-r1",
};
StreamingResponse<StreamingChatCompletionsUpdate> streamResponse = await client.CompleteStreamingAsync(requestOptions);
await PrintStream(streamResponse);
}
```


To visualize the output, define a helper function to print the stream. The following example implements a routing that stream only the answer without the reasoning content:

```
static void PrintStream(StreamingResponse<StreamingChatCompletionsUpdate> response)
{
bool isThinking = false;
await foreach (StreamingChatCompletionsUpdate chatUpdate in response)
{
if (!string.IsNullOrEmpty(chatUpdate.ContentUpdate))
{
string content = chatUpdate.ContentUpdate;
if (content == "<think>")
{
isThinking = true;
Console.Write("🧠 Thinking...");
Console.Out.Flush();
}
else if (content == "</think>")
{
isThinking = false;
Console.WriteLine("🛑\n\n");
}
else if (!string.IsNullOrEmpty(content))
{
Console.Write(content);
Console.Out.Flush();
}
}
}
}
```


You can visualize how streaming generates content:

```
StreamMessageAsync(client).GetAwaiter().GetResult();
```


### Parameters

In general, reasoning models don't support the following parameters you can find in chat completion models:

- Temperature
- Presence penalty
- Repetition penalty
- Parameter
`top_p`


Some models support the use of tools or structured outputs (including JSON-schemas). Read the [Models](../concepts/models?view=foundry-classic) details page to understand each model's support.

### Apply Guardrails and controls

The Azure AI Model Inference API supports [Azure AI Content Safety](https://aka.ms/azureaicontentsafety). When you use deployments with Azure AI Content Safety turned on, inputs and outputs pass through an ensemble of classification models aimed at detecting and preventing the output of harmful content. The content filtering system detects and takes action on specific categories of potentially harmful content in both input prompts and output completions.

The following example shows how to handle events when the model detects harmful content in the input prompt.

```
try
{
requestOptions = new ChatCompletionsOptions()
{
Messages = {
new ChatRequestSystemMessage("You are an AI assistant that helps people find information."),
new ChatRequestUserMessage(
"Chopping tomatoes and cutting them into cubes or wedges are great ways to practice your knife skills."
),
},
Model = "deepseek-r1",
};
response = client.Complete(requestOptions);
Console.WriteLine(response.Value.Content);
}
catch (RequestFailedException ex)
{
if (ex.ErrorCode == "content_filter")
{
Console.WriteLine($"Your query has trigger Azure Content Safety: {ex.Message}");
}
else
{
throw;
}
}
```


Tip

To learn more about how you can configure and control Azure AI Content Safety settings, check the [Azure AI Content Safety documentation](https://aka.ms/azureaicontentsafety).

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

This article explains how to use the reasoning capabilities of chat completions models deployed in Microsoft Foundry Models.

## Reasoning models

Reasoning models can reach higher levels of performance in domains like math, coding, science, strategy, and logistics. The way these models produce outputs is by explicitly using chain of thought to explore all possible paths before generating an answer. They verify their answers as they produce them, which helps to arrive at more accurate conclusions. As a result, reasoning models might require less context prompts in order to produce effective results.

Reasoning models produce two types of content as outputs:

- Reasoning completions
- Output completions

Both of these completions count towards content generated from the model. Therefore, they contribute to the token limits and costs associated with the model. Some models, like `DeepSeek-R1`

, might respond with the reasoning content. Others, like `o1`

, output only the completions.

## Prerequisites

To complete this tutorial, you need:

An Azure subscription. If you're using

[GitHub Models](https://docs.github.com/en/github-models/), you can upgrade your experience and create an Azure subscription in the process. Read[Upgrade from GitHub Models to Microsoft Foundry Models](quickstart-github-models?view=foundry-classic)if that's your case.A Foundry project. This kind of project is managed under a Foundry resource. If you don't have a Foundry project, see

[Create a project for Foundry (Foundry projects)](../../how-to/create-projects?view=foundry-classic).The endpoint's URL.

The endpoint's key (if you choose to use API key for authentication).


A model with reasoning capabilities model deployment. If you don't have one read

[Add and configure Foundry Models](create-model-deployments?view=foundry-classic)to add a reasoning model.- This example uses
`DeepSeek-R1`

.

- This example uses

## Use reasoning capabilities with chat

First, create the client to consume the model. The following code uses an endpoint URL and key that are stored in environment variables.

```
POST https://<resource>.services.ai.azure.com/openai/deployments/deepseek-r1/chat/completions?api-version=2024-10-21
Content-Type: application/json
api-key: <key>
```


If you have configured the resource with **Microsoft Entra ID** support, pass you token in the `Authorization`

header with the format `Bearer <token>`

. Use scope `https://cognitiveservices.azure.com/.default`

.

```
POST https://<resource>.services.ai.azure.com/openai/deployments/deepseek-r1/chat/completions?api-version=2024-10-21
Content-Type: application/json
Authorization: Bearer <token>
```


Using Microsoft Entra ID may require additional configuration in your resource to grant access. Learn how to [configure key-less authentication with Microsoft Entra ID](configure-entra-id?view=foundry-classic).

### Prompt reasoning models

When building prompts for reasoning models, take the following into consideration:

- Use simple instructions and avoid using chain-of-thought techniques.
- Built-in reasoning capabilities make simple zero-shot prompts as effective as more complex methods.
- When providing additional context or documents, like in RAG scenarios, including only the most relevant information might help prevent the model from over-complicating its response.
- Reasoning models may support the use of system messages. However, they might not follow them as strictly as other non-reasoning models.
- When creating multi-turn applications, consider appending only the final answer from the model, without it's reasoning content, as explained in the
[Reasoning content](#reasoning-content)section.

Notice that reasoning models can take longer times to generate responses. They use long reasoning chains of thought that enable deeper and more structured problem-solving. They also perform self-verification to cross-check their answers and correct their mistakes, thereby showcasing emergent self-reflective behaviors.

### Create a chat completion request

The following example shows how you can create a basic chat request to the model.

```
{
"model": "deepseek-r1",
"messages": [
{
"role": "user",
"content": "How many languages are in the world?"
}
]
}
```


The response is as follows, where you can see the model's usage statistics:

```
{
"id": "0a1234b5de6789f01gh2i345j6789klm",
"object": "chat.completion",
"created": 1718726686,
"model": "DeepSeek-R1",
"choices": [
{
"index": 0,
"message": {
"role": "assistant",
"reasoning_content": "Okay, the user is asking how many languages exist in the world. I need to provide a clear and accurate answer. Let's start by recalling the general consensus from linguistic sources. I remember that the number often cited is around 7,000, but maybe I should check some reputable organizations.\n\nEthnologue is a well-known resource for language data, and I think they list about 7,000 languages. But wait, do they update their numbers? It might be around 7,100 or so. Also, the exact count can vary because some sources might categorize dialects differently or have more recent data. \n\nAnother thing to consider is language endangerment. Many languages are endangered, with some having only a few speakers left. Organizations like UNESCO track endangered languages, so mentioning that adds context. Also, the distribution isn't even. Some countries have hundreds of languages, like Papua New Guinea with over 800, while others have just a few. \n\nA user might also wonder why the exact number is hard to pin down. It's because the distinction between a language and a dialect can be political or cultural. For example, Mandarin and Cantonese are considered dialects of Chinese by some, but they're mutually unintelligible, so others classify them as separate languages. Also, some regions are under-researched, making it hard to document all languages. \n\nI should also touch on language families. The 7,000 languages are grouped into families like Indo-European, Sino-Tibetan, Niger-Congo, etc. Maybe mention a few of the largest families. But wait, the question is just about the count, not the families. Still, it's good to provide a bit more context. \n\nI need to make sure the information is up-to-date. Let me think – recent estimates still hover around 7,000. However, languages are dying out rapidly, so the number decreases over time. Including that note about endangerment and language extinction rates could be helpful. For instance, it's often stated that a language dies every few weeks. \n\nAnother point is sign languages. Does the count include them? Ethnologue includes some, but not all sources might. If the user is including sign languages, that adds more to the count, but I think the 7,000 figure typically refers to spoken languages. For thoroughness, maybe mention that there are also over 300 sign languages. \n\nSummarizing, the answer should state around 7,000, mention Ethnologue's figure, explain why the exact number varies, touch on endangerment, and possibly note sign languages as a separate category. Also, a brief mention of Papua New Guinea as the most linguistically diverse country. \n\nWait, let me verify Ethnologue's current number. As of their latest edition (25th, 2022), they list 7,168 living languages. But I should check if that's the case. Some sources might round to 7,000. Also, SIL International publishes Ethnologue, so citing them as reference makes sense. \n\nOther sources, like Glottolog, might have a different count because they use different criteria. Glottolog might list around 7,000 as well, but exact numbers vary. It's important to highlight that the count isn't exact because of differing definitions and ongoing research. \n\nIn conclusion, the approximate number is 7,000, with Ethnologue being a key source, considerations of endangerment, and the challenges in counting due to dialect vs. language distinctions. I should make sure the answer is clear, acknowledges the variability, and provides key points succinctly.\n",
"content": "The exact number of languages in the world is challenging to determine due to differences in definitions (e.g., distinguishing languages from dialects) and ongoing documentation efforts. However, widely cited estimates suggest there are approximately **7,000 languages** globally.",
"tool_calls": null
},
"finish_reason": "stop"
}
],
"usage": {
"prompt_tokens": 11,
"total_tokens": 897,
"completion_tokens": 886
}
}
```


### Reasoning content

Note

This information on reasoning content does not apply to Azure OpenAI models. Azure OpenAI reasoning models use the [reasoning summaries feature](../../openai/how-to/reasoning?view=foundry-classic#reasoning-summary).

Some reasoning models, like DeepSeek-R1, generate completions and include the reasoning behind it.

The reasoning associated with the completion is included in the field `reasoning_content`

. The model may select on which scenarios to generate reasoning content.

When making multi-turn conversations, it's useful to avoid sending the reasoning content in the chat history as reasoning tends to generate long explanations.

### Stream content

By default, the completions API returns the entire generated content in a single response. If you're generating long completions, waiting for the response can take many seconds.

You can *stream* the content to get it as it's being generated. Streaming content allows you to start processing the completion as content becomes available. This mode returns an object that streams back the response as [data-only server-sent events](https://html.spec.whatwg.org/multipage/server-sent-events.html#server-sent-events). Extract chunks from the delta field, rather than the message field.

To stream completions, set `"stream": true`

when you call the model.

```
{
"model": "DeepSeek-R1",
"messages": [
{
"role": "user",
"content": "How many languages are in the world?"
}
],
"stream": true,
"max_tokens": 2048
}
```


To visualize the output, define a helper function to print the stream. The following example implements a routing that stream only the answer without the reasoning content:

```
{
"id": "23b54589eba14564ad8a2e6978775a39",
"object": "chat.completion.chunk",
"created": 1718726371,
"model": "DeepSeek-R1",
"choices": [
{
"index": 0,
"delta": {
"role": "assistant",
"reasoning_content": "Okay,",
"content": ""
},
"finish_reason": null,
"logprobs": null
}
]
}
```


The last message in the stream has `finish_reason`

set, indicating the reason for the generation process to stop.

```
{
"id": "23b54589eba14564ad8a2e6978775a39",
"object": "chat.completion.chunk",
"created": 1718726371,
"model": "DeepSeek-R1",
"choices": [
{
"index": 0,
"delta": {
"reasoning_content": "",
"content": ""
},
"finish_reason": "stop",
"logprobs": null
}
],
"usage": {
"prompt_tokens": 11,
"total_tokens": 897,
"completion_tokens": 886
}
}
```


### Parameters

In general, reasoning models don't support the following parameters you can find in chat completion models:

- Temperature
- Presence penalty
- Repetition penalty
- Parameter
`top_p`


Some models support the use of tools or structured outputs (including JSON-schemas). Read the [Models](../concepts/models?view=foundry-classic) details page to understand each model's support.

### Apply Guardrails and controls

The Azure AI Model Inference API supports [Azure AI Content Safety](https://aka.ms/azureaicontentsafety). When you use deployments with Azure AI Content Safety turned on, inputs and outputs pass through an ensemble of classification models aimed at detecting and preventing the output of harmful content. The content filtering system detects and takes action on specific categories of potentially harmful content in both input prompts and output completions.

The following example shows how to handle events when the model detects harmful content in the input prompt.

```
{
"model": "DeepSeek-R1",
"messages": [
{
"role": "user",
"content": "Chopping tomatoes and cutting them into cubes or wedges are great ways to practice your knife skills."
}
]
}
```


```
{
"error": {
"message": "The response was filtered due to the prompt triggering Microsoft's content management policy. Please modify your prompt and retry.",
"type": null,
"param": "prompt",
"code": "content_filter",
"status": 400
}
}
```


Tip

To learn more about how you can configure and control Azure AI Content Safety settings, check the [Azure AI Content Safety documentation](https://aka.ms/azureaicontentsafety).
