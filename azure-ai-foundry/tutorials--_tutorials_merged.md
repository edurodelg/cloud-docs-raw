---
merged_at: 2026-02-06T17:00:26.028283
merged_files: 6
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/tutorials/quickstart-create-foundry-resources -->

# Quickstart: Set up Microsoft Foundry resources

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you create a [Microsoft Foundry](https://ai.azure.com) project and deploy a model. If you're managing a team, you also grant access to team members. After you complete these steps, you or your team can start building AI applications using the deployed model.

Tip

This quickstart shows you how to create resources to build an agent with a basic setup. For more advanced scenarios that use your own resources, see [Set up your environment for agent development](../agents/environment-setup?view=foundry).

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - If you're creating the project for yourself:
- Access to a role that allows you to create a Foundry resource, such as
**Azure Account AI Owner**or**Azure AI Owner**on the subscription or resource group. For more information about permissions, see[Role-based access control for Microsoft Foundry](../concepts/rbac-foundry?view=foundry#permissions-for-each-built-in-role).

- Access to a role that allows you to create a Foundry resource, such as
- If you're creating the project for a team:
- Access to a role that allows you to complete role assignments, such as
**Owner**. For more information about permissions, see[Role-based access control for Microsoft Foundry](../concepts/rbac-foundry?view=foundry#permissions-for-each-built-in-role). - A list of user email addresses or Microsoft Entra security group IDs for team members who need access.

- Access to a role that allows you to complete role assignments, such as

Select your preferred method by using the following tabs:

Install the

[Azure CLI](/en-us/cli/azure/install-azure-cli).Sign in to Azure:

`az login`


## Create a project

Create a Foundry project to organize your work. The project contains models, agents, and other resources your team uses.

Create a resource group or use an existing one. For example, create

`my-foundry-rg`

in`eastus`

:`az group create --name my-foundry-rg --location eastus`

Create the Foundry resource. For example, create

`my-foundry-resource`

in the`my-foundry-rg`

resource group:`az cognitiveservices account create \ --name my-foundry-resource \ --resource-group my-foundry-rg \ --kind AIServices \ --sku s0 \ --location eastus \ --allow-project-management`

The

`--allow-project-management`

flag enables project creation within this resource.Create a custom subdomain for the resource. The custom domain name must be globally unique. If

`my-foundry-resource`

is taken, try a more unique name.`az cognitiveservices account update \ --name my-foundry-resource \ --resource-group my-foundry-rg \ --custom-domain my-foundry-resource`

Create the project. For example, create

`my-foundry-project`

in the`my-foundry-resource`

:`az cognitiveservices account project create \ --name my-foundry-resource \ --resource-group my-foundry-rg \ --project-name my-foundry-project \ --location eastus`

Verify the project was created:

`az cognitiveservices account project show \ --name my-foundry-resource \ --resource-group my-foundry-rg \ --project-name my-foundry-project`

The output displays the project properties, including its resource ID.


Reference: [az cognitiveservices account](/en-us/cli/azure/cognitiveservices/account)

## Deploy a model

Deploy a model that you can use. This example uses **gpt-4.1-mini**, but you can choose any available model.

```
az cognitiveservices account deployment create \
--name my-foundry-resource \
--resource-group my-foundry-rg \
--deployment-name gpt-4.1-mini \
--model-name gpt-4.1-mini \
--model-version "2025-04-14" \
--model-format OpenAI \
--sku-capacity 10 \
--sku-name Standard
```


Verify the deployment succeeded:

```
az cognitiveservices account deployment show \
--name my-foundry-resource \
--resource-group my-foundry-rg \
--deployment-name gpt-4.1-mini
```


When the deployment is ready, the output shows `"provisioningState": "Succeeded"`

.

Reference: [az cognitiveservices account deployment](/en-us/cli/azure/cognitiveservices/account/deployment)

## Get your project connection details

You need the following information to connect to the project in other quickstarts and tutorials.

If you're administering this project for others, send them this information.

- Sign in to
[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs)by using your Azure account. Select your project to start building. - Find your project endpoint on the welcome screen of the project.
- Get started with
[Microsoft Foundry quickstart](../quickstarts/get-started-code?view=foundry).

## For administrators - grant access

If you're administering a team, assign the **Azure AI User** role to team members so they can use the project and deployed models. This role provides the minimum permissions needed to build and test AI applications.

Get the project's resource ID:

`PROJECT_ID=$(az cognitiveservices account project show \ --name my-foundry-resource \ --resource-group my-foundry-rg \ --project-name my-foundry-project \ --query id -o tsv)`

Assign the

**Azure AI User**role to a team member:`az role assignment create \ --role "Azure AI User" \ --assignee "user@contoso.com" \ --scope $PROJECT_ID`

To add a security group instead of an individual user:

`az role assignment create \ --role "Azure AI User" \ --assignee-object-id "<security-group-object-id>" \ --assignee-principal-type Group \ --scope $PROJECT_ID`

Verify the role assignment:

`az role assignment list \ --scope $PROJECT_ID \ --role "Azure AI User" \ --output table`


Reference: [az role assignment](/en-us/cli/azure/role/assignment)

### Verify team member access

Ask a team member to verify their access by signing in to [Microsoft Foundry](https://ai.azure.com), selecting the project from the project list, and confirming the deployed model appears under **Build** > **Models**.

If the team member can't access the project, verify that the role assignment completed successfully. Check that you used the correct email address or security group ID. Make sure the team member's Azure account is in the same Microsoft Entra tenant.

## Clean up resources

When you no longer want this project, delete the resource group to delete all resources associated with it.

```
az group delete --name my-foundry-rg --yes --no-wait
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/tutorials/copilot-sdk-evaluate -->

# Tutorial: Part 3 - Evaluate a custom chat application with the Microsoft Foundry SDK

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

In this tutorial, you evaluate the chat app you built in [Part 2 of the tutorial series](copilot-sdk-build-rag?view=foundry-classic). You assess your app's quality across multiple metrics and then iterate on improvements. In this part, you:

- Create an evaluation dataset
- Evaluate the chat app with Azure AI evaluators
- Iterate and improve your app

This tutorial builds on [Part 2: Build a custom chat app with the Microsoft Foundry SDK](copilot-sdk-build-rag?view=foundry-classic).

## Prerequisites

Important

This article provides legacy support for hub-based projects. It will not work for **Foundry projects**. See [How do I know which type of project I have?](../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have)

**SDK compatibility note**: Code examples require a specific Microsoft Foundry SDK version. If you encounter compatibility issues, consider [migrating from a hub-based to a Foundry project](../how-to/migrate-project?view=foundry-classic).

- An Azure account with an active subscription. If you don't have one, create a
[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - If you don't have one,
[create a hub-based project](../how-to/hub-create-projects?view=foundry-classic).

- Complete
[Part 2 of the tutorial series](copilot-sdk-build-rag?view=foundry-classic)to build the chat application. - Use the same
**hub-based**project you created in Part 1. **Azure AI permissions**: Owner or Contributor role to modify model endpoint rate limits and run evaluation jobs.- Make sure you complete the steps to
[add telemetry logging](copilot-sdk-build-rag?view=foundry-classic#add-telemetry-logging)from Part 2.

## Create evaluation dataset

Use the following evaluation dataset, which contains example questions and expected answers. Use this dataset with an evaluator and the `get_chat_response()`

target function to assess your chat app's performance across relevance, groundedness, and coherence metrics.

Create a file named

**chat_eval_data.jsonl**in your**assets**folder.Paste this dataset into the file:

`{"query": "Which tent is the most waterproof?", "truth": "The Alpine Explorer Tent has the highest rainfly waterproof rating at 3000m"} {"query": "Which camping table holds the most weight?", "truth": "The Adventure Dining Table has a higher weight capacity than all of the other camping tables mentioned"} {"query": "How much do the TrailWalker Hiking Shoes cost? ", "truth": "The Trailewalker Hiking Shoes are priced at $110"} {"query": "What is the proper care for trailwalker hiking shoes? ", "truth": "After each use, remove any dirt or debris by brushing or wiping the shoes with a damp cloth."} {"query": "What brand is TrailMaster tent? ", "truth": "OutdoorLiving"} {"query": "How do I carry the TrailMaster tent around? ", "truth": " Carry bag included for convenient storage and transportation"} {"query": "What is the floor area for Floor Area? ", "truth": "80 square feet"} {"query": "What is the material for TrailBlaze Hiking Pants?", "truth": "Made of high-quality nylon fabric"} {"query": "What color does TrailBlaze Hiking Pants come in?", "truth": "Khaki"} {"query": "Can the warrenty for TrailBlaze pants be transfered? ", "truth": "The warranty is non-transferable and applies only to the original purchaser of the TrailBlaze Hiking Pants. It is valid only when the product is purchased from an authorized retailer."} {"query": "How long are the TrailBlaze pants under warranty for? ", "truth": " The TrailBlaze Hiking Pants are backed by a 1-year limited warranty from the date of purchase."} {"query": "What is the material for PowerBurner Camping Stove? ", "truth": "Stainless Steel"} {"query": "Is France in Europe?", "truth": "Sorry, I can only queries related to outdoor/camping gear and equipment"}`

References:

[JSONL format for evaluation datasets](../how-to/evaluate-results?view=foundry-classic).

## Evaluate with Azure AI evaluators

Create an evaluation script that generates a target function wrapper, loads your dataset, runs the evaluation, and logs results to your Foundry project.

Create a file named

**evaluate.py**in your main folder.Add the following code to import the required libraries, create a project client, and configure some settings:

`import os import pandas as pd from azure.ai.projects import AIProjectClient from azure.ai.projects.models import ConnectionType from azure.ai.evaluation import evaluate, GroundednessEvaluator from azure.identity import DefaultAzureCredential from chat_with_products import chat_with_products # load environment variables from the .env file at the root of this repo from dotenv import load_dotenv load_dotenv() # create a project client using environment variables loaded from the .env file project = AIProjectClient.from_connection_string( conn_str=os.environ["AIPROJECT_CONNECTION_STRING"], credential=DefaultAzureCredential() ) connection = project.connections.get_default(connection_type=ConnectionType.AZURE_OPEN_AI, include_credentials=True) evaluator_model = { "azure_endpoint": connection.endpoint_url, "azure_deployment": os.environ["EVALUATION_MODEL"], "api_version": "2024-06-01", "api_key": connection.key, } groundedness = GroundednessEvaluator(evaluator_model)`

References:

[AIProjectClient](/en-us/python/api/azure-ai-projects/azure.ai.projects.AIProjectClient),[DefaultAzureCredential](/en-us/python/api/azure-identity/azure.identity.DefaultAzureCredential),[azure-ai-evaluation](https://pypi.org/project/azure-ai-evaluation/).Add code to create a wrapper function that implements the evaluation interface for query and response evaluation:

`def evaluate_chat_with_products(query): response = chat_with_products(messages=[{"role": "user", "content": query}]) return {"response": response["message"].content, "context": response["context"]["grounding_data"]}`

References:

[azure-ai-evaluation](https://pypi.org/project/azure-ai-evaluation/), evaluation target functions.Finally, add code to run the evaluation, view the results locally, and get a link to the evaluation results in Foundry portal:

`# Evaluate must be called inside of __main__, not on import if __name__ == "__main__": from config import ASSET_PATH # workaround for multiprocessing issue on linux from pprint import pprint from pathlib import Path import multiprocessing import contextlib with contextlib.suppress(RuntimeError): multiprocessing.set_start_method("spawn", force=True) # run evaluation with a dataset and target function, log to the project result = evaluate( data=Path(ASSET_PATH) / "chat_eval_data.jsonl", target=evaluate_chat_with_products, evaluation_name="evaluate_chat_with_products", evaluators={ "groundedness": groundedness, }, evaluator_config={ "default": { "query": {"${data.query}"}, "response": {"${target.response}"}, "context": {"${target.context}"}, } }, azure_ai_project=project.scope, output_path="./myevalresults.json", ) tabular_result = pd.DataFrame(result.get("rows")) pprint("-----Summarized Metrics-----") pprint(result["metrics"]) pprint("-----Tabular Result-----") pprint(tabular_result) pprint(f"View evaluation results in AI Studio: {result['studio_url']}")`

References:

[azure-ai-evaluation](https://pypi.org/project/azure-ai-evaluation/),[AIProjectClient](/en-us/python/api/azure-ai-projects/azure.ai.projects.AIProjectClient).

### Configure the evaluation model

The evaluation script calls the model many times. Consider increasing the number of tokens per minute for the evaluation model.

In Part 1 of this tutorial series, you created an **.env** file that specifies the name of the evaluation model, `gpt-4o-mini`

. Try to increase the tokens per minute limit for this model, if you have available quota. If you don't have enough quota to increase the value, don't worry. The script is designed to handle limit errors.

- In your project in Foundry portal, select
**Models + endpoints**. - Select
**gpt-4o-mini**. - Select
**Edit**. - If you have quota, increase the
**Tokens per Minute Rate Limit**to 30 or more. - Select
**Save and close**.

### Run the evaluation script

From your console, sign in to your Azure account by using the Azure CLI:

`az login`

Install the required packages:

`pip install openai pip install azure-ai-evaluation[remote]`

References:

[azure-ai-evaluation SDK](https://pypi.org/project/azure-ai-evaluation/), Evaluation SDK documentation.

### Verify your evaluation setup

Before running the full evaluation (which takes 5–10 minutes), verify that the SDK and your project connection are working by running this quick test:

```
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential
# Test that you can connect to your project
project = AIProjectClient.from_connection_string(
conn_str=os.environ["AIPROJECT_CONNECTION_STRING"], credential=DefaultAzureCredential()
)
print("Evaluation SDK is ready! You can now run evaluate.py")
```


If you see `"Evaluation SDK is ready!"`

, your setup is complete and you can proceed.

References: [AIProjectClient](/en-us/python/api/azure-ai-projects/azure.ai.projects.AIProjectClient), [DefaultAzureCredential](/en-us/python/api/azure-identity/azure.identity.DefaultAzureCredential).

### Start the evaluation

Run the evaluation script:

`python evaluate.py`


The evaluation takes 5–10 minutes to complete. You might see timeout warnings and rate-limit errors. The script handles these errors automatically and continues processing.

### Interpret the evaluation output

In the console output, you see an answer for each question, followed by a table with summarized metrics showing relevance, groundedness, and coherence scores. Scores range from 0 (worst) to 4 (best) for GPT-assisted metrics. Look for low groundedness scores to identify responses that aren't well-supported by the reference documents, and low relevance scores to identify off-topic responses.

You might see many `WARNING:opentelemetry.attributes:`

messages and timeout errors. You can safely ignore these messages. They don't affect the evaluation results. The evaluation script is designed to handle rate-limit errors and continue processing.

The evaluation results output also includes a link to view detailed results in the Foundry portal, where you can compare evaluation runs side-by-side and track improvements over time.

```
====================================================
'-----Summarized Metrics-----'
{'groundedness.gpt_groundedness': 1.6666666666666667,
'groundedness.groundedness': 1.6666666666666667}
'-----Tabular Result-----'
outputs.response ... line_number
0 Could you specify which tent you are referring... ... 0
1 Could you please specify which camping table y... ... 1
2 Sorry, I only can answer queries related to ou... ... 2
3 Could you please clarify which aspects of care... ... 3
4 Sorry, I only can answer queries related to ou... ... 4
5 The TrailMaster X4 Tent comes with an included... ... 5
6 (Failed) ... 6
7 The TrailBlaze Hiking Pants are crafted from h... ... 7
8 Sorry, I only can answer queries related to ou... ... 8
9 Sorry, I only can answer queries related to ou... ... 9
10 Sorry, I only can answer queries related to ou... ... 10
11 The PowerBurner Camping Stove is designed with... ... 11
12 Sorry, I only can answer queries related to ou... ... 12
[13 rows x 8 columns]
('View evaluation results in Foundry portal: '
'https://xxxxxxxxxxxxxxxxxxxxxxx')
```


## Iterate and improve

The evaluation results reveal that responses often aren't well-grounded in the reference documents. To improve groundedness, modify your system prompt in the **assets/grounded_chat.prompty** file to encourage the model to use the reference documents more directly.

**Current prompt (problematic)**:

```
If the question is not related to outdoor/camping gear and clothing, just say 'Sorry, I only can answer queries related to outdoor/camping gear and clothing. So, how can I help?'
If the question is related to outdoor/camping gear and clothing but vague, ask clarifying questions.
```


**Improved prompt**:

```
If the question is related to outdoor/camping gear and clothing, answer based on the reference documents provided.
If you cannot find information in the reference documents, say: 'I don't have information about that specific topic. Let me help with related products or try a different question.'
For vague questions, ask clarifying questions to better assist.
```


After updating the prompt:

Save the file.

Run the evaluation script again:

`python evaluate.py`

Compare the new evaluation results to the previous run. You should see improved groundedness scores.


Try additional modifications like:

- Changing the system prompt to focus on accuracy over completeness
- Testing with a different model (for example,
`gpt-4-turbo`

if available) - Adjusting the context retrieval to return more relevant documents

Each iteration helps you understand which changes improve specific metrics.

## Clean up resources

To avoid incurring unnecessary Azure costs, delete the resources you created in this tutorial if they're no longer needed. To manage resources, you can use the [Azure portal](https://portal.azure.com?azure-portal=true).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/tutorials/copilot-sdk-create-resources -->

# Tutorial:  Part 1 - Set up project and development environment to build a custom knowledge retrieval (RAG) app with the Microsoft Foundry SDK

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

In this tutorial, you set up the resources needed to build a custom knowledge retrieval (RAG) chat app with the Microsoft Foundry SDK. This is part one of a three-part tutorial series. You create the resources here, build the app in part two, and evaluate it in part three. In this part, you:

- Create a project
- Create an Azure AI Search index
- Install the Azure CLI and sign in
- Install Python and packages
- Deploy models into your project
- Configure your environment variables

If you completed other tutorials or quickstarts, you might have already created some of the resources needed for this tutorial. If you did, feel free to skip those steps.

## Prerequisites

Important

This article provides legacy support for hub-based projects. It will not work for **Foundry projects**. See [How do I know which type of project I have?](../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have)

**SDK compatibility note**: Code examples require a specific Microsoft Foundry SDK version. If you encounter compatibility issues, consider [migrating from a hub-based to a Foundry project](../how-to/migrate-project?view=foundry-classic).

- An Azure account with an active subscription and
**Owner**or**Contributor**role assigned. If you don't have one,[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). **Microsoft Foundry**: Owner or Contributor role to create a project.

## Create a hub-based project

To create a hub-based project in [Microsoft Foundry](https://ai.azure.com/?cid=learnDocs), follow these steps:

-
Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is off. These steps refer to**Foundry (classic)**. -
What you do next depends on where you are:

**If you don't have any existing projects**: Follow the steps in[Quickstart: Get started with Microsoft Foundry](../quickstarts/get-started-code?view=foundry-classic)to create your first project.**If you're in a project**: Select the project breadcrumb, then select**Create new resource**.**If you're not in a project**: Select**Create new**in the top right to create a new Foundry project

Select

**AI hub resource**, then select**Next**.Enter a name for the project.

If you have a hub, you'll see the one you most recently used selected.

If you don't have a hub, a default one is created for you.

Select

**Create**.

## Deploy models

You need two models to build a RAG-based chat app: an Azure OpenAI chat model (`gpt-4o-mini`

) and an Azure OpenAI embedding model (`text-embedding-ada-002`

). Deploy these models in your Foundry project by using this set of steps for each model.

These steps deploy a model to a real-time endpoint from the Foundry portal [model catalog](../concepts/foundry-models-overview?view=foundry-classic):

Tip

Because you can [customize the left pane](../what-is-foundry?view=foundry-classic#customize-the-left-pane) in the Microsoft Foundry portal, you might see different items than shown in these steps. If you don't see what you're looking for, select **... More** at the bottom of the left pane.

On the left pane, select

**Model catalog**.Select the

**gpt-4o-mini**model from the list of models. You can use the search bar to find it.On the model details page, select

**Use this model**.Leave the default

**Deployment name**and select**Deploy**. Or, if the model isn't available in your region, a different region is selected for you and connected to your project. In this case, select**Connect and deploy**.

After you deploy the **gpt-4o-mini**, repeat the steps to deploy the **text-embedding-ada-002** model.

## Create an Azure AI Search service

The goal of this application is to ground the model responses in your custom data. The search index retrieves relevant documents based on the user's question.

You need an Azure AI Search service and connection to create a search index.

Note

Creating an [Azure AI Search service](/en-us/azure/search/) and subsequent search indexes incurs costs. To confirm the cost before creating the resource, check the pricing and pricing tiers for the Azure AI Search service on the creation page. For this tutorial, use a pricing tier of **Basic** or higher.

If you already have an Azure AI Search service, go to the [next section](#connect-the-azure-ai-search-to-your-project).

Otherwise, create an Azure AI Search service by using the Azure portal.

Tip

This step is the only time you use the Azure portal in this tutorial series. You do the rest of your work in the Foundry portal or in your local development environment.

[Create an Azure AI Search service](https://portal.azure.com/#create/Microsoft.Search)in the Azure portal.- Select your resource group and instance details. Check the pricing and pricing tiers . For this tutorial, use a pricing tier of
**Basic**or higher. - Continue through the wizard and select
**Review + assign**to create the resource. - Confirm the details of your Azure AI Search service, including the estimated cost.
- Select
**Create**to create the Azure AI Search service.

### Connect the Azure AI Search to your project

If your project already has an Azure AI Search connection, go to [Install the Azure CLI and sign in](#install-the-azure-cli-and-sign-in).

In the Foundry portal, check for an Azure AI Search connected resource.

In

[Foundry](https://ai.azure.com/?cid=learnDocs), go to your project and select**Management center**from the left pane.In the

**Connected resources**section, look to see if you have a connection of type**Azure AI Search**.If you have an Azure AI Search connection, you can skip the next steps.

Otherwise, select

**New connection**and then**Azure AI Search**.Find your Azure AI Search service in the options and select

**Add connection**.Use

**API key**for**Authentication**.Important

The

**API key**option isn't recommended for production. The recommended approach is**Microsoft Entra ID**authentication, which requires the*Search Index Data Contributor*and*Search Service Contributor*roles (configured in Prerequisites). For more information, see[Connect to Azure AI Search using roles](../../search/search-security-rbac?view=foundry-classic). For this tutorial,**API key**is acceptable if you want to proceed quickly. Switch to Entra ID before deploying to production.Select

**Add connection**.

## Create a new Python environment

In the IDE of your choice, create a new folder for your project. Open a terminal window in that folder.

First, create a new Python environment. Don't install packages into your global Python installation. Always use a virtual or conda environment when installing Python packages. Otherwise, you can break your global install of Python.

### If needed, install Python

Use Python 3.10 or later, but at least Python 3.9 is required. If you don't have a suitable version of Python installed, follow the instructions in the [VS Code Python Tutorial](https://code.visualstudio.com/docs/python/python-tutorial#_install-a-python-interpreter) for the easiest way of installing Python on your operating system.

### Create a virtual environment

If you already have Python 3.10 or higher installed, create a virtual environment by using the following commands:

When you activate the Python environment, running `python`

or `pip`

from the command line uses the Python interpreter in the `.venv`

folder of your application.

Note

Use the `deactivate`

command to exit the Python virtual environment. You can reactivate it later when needed.

## Install packages

Install the required packages.

Create a file named

**requirements.txt**in your project folder. Add the following packages to the file:`azure-ai-projects==1.0.0b10 azure-ai-inference[prompts] azure-identity azure-search-documents pandas python-dotenv opentelemetry-api`

References:

[Azure AI Projects client library](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/ai/azure-ai-projects),[azure-ai-inference](https://pypi.org/project/azure-ai-inference/),[python-dotenv](https://pypi.org/project/python-dotenv/).Install the required packages:

`pip install -r requirements.txt`


## Configure environment variables

Your project connection string is required to call Azure OpenAI in Microsoft Foundry Models from your code. In this quickstart, you save this value in a `.env`

file, which is a file that contains environment variables that your application can read.

Create a `.env`

file, and paste the following code:

```
AIPROJECT_CONNECTION_STRING=<your-connection-string>
AISEARCH_INDEX_NAME="example-index"
EMBEDDINGS_MODEL="text-embedding-ada-002"
INTENT_MAPPING_MODEL="gpt-4o-mini"
CHAT_MODEL="gpt-4o-mini"
EVALUATION_MODEL="gpt-4o-mini"
```


Find your connection string in the Foundry project you created in the

[Foundry playground quickstart](../quickstarts/get-started-playground?view=foundry-classic). Open the project, then find the connection string on the**Overview**page. Copy the connection string and paste it into the`.env`

file.If you don't yet have a search index, keep the value "example-index" for

`AISEARCH_INDEX_NAME`

. In Part 2 of this tutorial you'll create the index using this name. If you have previously created a search index that you want to use instead, update the value to match the name of that search index.If you changed the names of the models when you deployed them, update the values in the

`.env`

file to match the names you used.

Tip

If you're working in VS Code, close and reopen the terminal window after you've saved changes in the `.env`

file.

Warning

Ensure that your `.env`

is in your `.gitignore`

file so that you don't accidentally check it into your git repository.

## Install the Azure CLI and sign in

You install the [Azure CLI](/en-us/cli/azure/what-is-azure-cli) and sign in from your local development environment, so that you can use your user credentials to call Azure OpenAI in Microsoft Foundry Models.

In most cases you can install Azure CLI from your terminal using the following command:

You can follow instructions [How to install the Azure CLI](/en-us/cli/azure/install-azure-cli) if these commands don't work for your particular operating system or setup.

After you install the Azure CLI, sign in using the `az login`

command and sign-in using the browser:

```
az login
```


Alternatively, you can sign in manually via the browser with a device code.

```
az login --use-device-code
```


Keep this terminal window open to run your python scripts from here as well, now that you signed in.

## Verify your setup

Verify that your environment is set up correctly by running a quick test:

```
import os
from azure.identity import DefaultAzureCredential
import azure.ai.projects
# Check the SDK version
print(f"Azure AI Projects SDK version: {azure.ai.projects.__version__}")
# Test that you can connect to your project
project = AIProjectClient.from_connection_string(
conn_str=os.environ["AIPROJECT_CONNECTION_STRING"], credential=DefaultAzureCredential()
)
print("✓ Setup verified! Ready to build your RAG app.")
```


If you see `"Setup successful!"`

, your Azure credentials and SDK are configured correctly.

Tip

This tutorial requires Azure AI Projects SDK version `1.0.0b10`

. The SDK version displayed above helps you verify compatibility. If you have a different version, the `from_connection_string()`

method may not be available. To install the required version, run `pip install azure-ai-projects==1.0.0b10`

.

References: [Azure AI Projects client library](/en-us/python/api/azure-ai-projects/azure.ai.projects), [DefaultAzureCredential](/en-us/python/api/azure-identity/azure.identity.DefaultAzureCredential).

## Create helper script

Create a folder for your work. Create a file named **config.py** in this folder. You'll use this helper script in the next two parts of the tutorial series. The script loads your environment variables and initializes the Azure AI Projects client. Add the following code:

```
# ruff: noqa: ANN201, ANN001
import os
import sys
import pathlib
import logging
from azure.identity import DefaultAzureCredential
from azure.ai.projects import AIProjectClient
from azure.ai.inference.tracing import AIInferenceInstrumentor
# load environment variables from the .env file
from dotenv import load_dotenv
load_dotenv()
# Set "./assets" as the path where assets are stored, resolving the absolute path:
ASSET_PATH = pathlib.Path(__file__).parent.resolve() / "assets"
# Configure an root app logger that prints info level logs to stdout
logger = logging.getLogger("app")
logger.setLevel(logging.INFO)
logger.addHandler(logging.StreamHandler(stream=sys.stdout))
# Returns a module-specific logger, inheriting from the root app logger
def get_logger(module_name):
return logging.getLogger(f"app.{module_name}")
# Enable instrumentation and logging of telemetry to the project
def enable_telemetry(log_to_project: bool = False):
AIInferenceInstrumentor().instrument()
# enable logging message contents
os.environ["AZURE_TRACING_GEN_AI_CONTENT_RECORDING_ENABLED"] = "true"
if log_to_project:
from azure.monitor.opentelemetry import configure_azure_monitor
project = AIProjectClient.from_connection_string(
conn_str=os.environ["AIPROJECT_CONNECTION_STRING"], credential=DefaultAzureCredential()
)
tracing_link = f"https://ai.azure.com/tracing?wsid=/subscriptions/{project.scope['subscription_id']}/resourceGroups/{project.scope['resource_group_name']}/providers/Microsoft.MachineLearningServices/workspaces/{project.scope['project_name']}"
application_insights_connection_string = project.telemetry.get_connection_string()
if not application_insights_connection_string:
logger.warning(
"No application insights configured, telemetry will not be logged to project. Add application insights at:"
)
logger.warning(tracing_link)
return
configure_azure_monitor(connection_string=application_insights_connection_string)
logger.info("Enabled telemetry logging to project, view traces at:")
logger.info(tracing_link)
```


References: [AIProjectClient](/en-us/python/api/azure-ai-projects/azure.ai.projects.AIProjectClient), [DefaultAzureCredential](/en-us/python/api/azure-identity/azure.identity.DefaultAzureCredential), [load_dotenv](https://pypi.org/project/python-dotenv/).

Note

This script also uses a package you haven't installed yet, `azure.monitor.opentelemetry`

. You'll install this package in the next part of the tutorial series.

## Clean up resources

To avoid incurring unnecessary Azure costs, delete the resources you created in this tutorial if they're no longer needed. To manage resources, you can use the [Azure portal](https://portal.azure.com?azure-portal=true).

But don't delete them yet if you want to build a chat app in [the next part of this tutorial series](copilot-sdk-build-rag?view=foundry-classic).

## Next step

In this tutorial, you set up everything you need to build a custom chat app with the Azure AI SDK. In the next part of this tutorial series, you build the custom app.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/tutorials/deploy-chat-web-app -->

# Tutorial: Deploy an enterprise chat web app

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

In this article, you deploy an enterprise chat web app that uses your data with a large language model in Microsoft Foundry portal.

Your data source grounds the model with specific data. Grounding means the model uses your data to understand the context of your question. You don't change the deployed model itself. Your data stays separate and secure in your original data source.

The steps in this tutorial are:

- Configure resources.
- Add your data.
- Test the model with your data.
- Deploy your web app.

## Prerequisites

Important

This article provides legacy support for hub-based projects. It will not work for **Foundry projects**. See [How do I know which type of project I have?](../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have)

**SDK compatibility note**: Code examples require a specific Microsoft Foundry SDK version. If you encounter compatibility issues, consider [migrating from a hub-based to a Foundry project](../how-to/migrate-project?view=foundry-classic).

- An Azure account with an active subscription. If you don't have one, create a
[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - If you don't have one,
[create a hub-based project](../how-to/hub-create-projects?view=foundry-classic).

A

[deployed Azure OpenAI](../foundry-models/how-to/deploy-foundry-models?view=foundry-classic)chat model. Finish the[Foundry playground quickstart](../quickstarts/get-started-playground?view=foundry-classic)to create this resource if you don't have one.A Search service connection to index the sample product data. If you don't have one, follow the steps to

[create](copilot-sdk-create-resources?view=foundry-classic#create-an-azure-ai-search-service)and[connect](copilot-sdk-create-resources?view=foundry-classic#connect-the-azure-ai-search-to-your-project)a search service.A local copy of product data. The

[Azure-Samples/rag-data-openai-python-promptflow repository on GitHub](https://github.com/Azure-Samples/rag-data-openai-python-promptflow/)has sample retail product information for this tutorial scenario. The`product_info_11.md`

file has product information about the TrailWalker hiking shoes for this tutorial example.[Download the example Contoso Trek retail product data in a ZIP file](https://github.com/Azure-Samples/rag-data-openai-python-promptflow/raw/refs/heads/main/tutorial/data/product-info.zip)to your local machine.A

**Microsoft.Web**resource provider registered in the selected subscription so you can deploy to a web app. For more information on registering a resource provider, see[Register resource provider](/en-us/azure/azure-resource-manager/management/resource-providers-and-types#register-resource-provider-1).Necessary permissions to add role assignments in your Azure subscription. Only the Owner of the specific Azure resources can grant permissions by role assignment.


## Foundry portal and Azure portal

In this tutorial, you perform some tasks in the Foundry portal and some tasks in the Azure portal.

The Foundry portal is a web-based environment for building, training, and deploying AI models. As a developer, it's where you build and deploy your chat web application.

The Azure portal lets an admin manage and monitor Azure resources. As an admin, you use the portal to set up settings for different Azure services required for access from the web app.

## Configure resources

Important

You must have the necessary permissions to add role assignments in your Azure subscription. Granting permissions by role assignment is only allowed by the Owner of the specific Azure resources. You might need to ask your Azure subscription owner (who might be your IT admin) to complete this section for you.

To make the resources work correctly in a web app, set up the correct permissions in the Azure portal.

First, identify the resources you need to set up in the Foundry portal.

Open the

[Foundry portal](https://ai.azure.com/?cid=learnDocs), then select the hub-based project you used to deploy the Azure OpenAI chat model.Select

**Management center**from the left pane.Select

**Connected resources**under your project.Identify the three resources you need to configure: the

**Azure OpenAI**, the**Azure AI Search**, and the**Azure Blob storage**that corresponds to your**workspaceblobstore**.Tip

If you don't see

**Type**in the table, select**Columns**in the upper right corner and add to or reorder the**Selected columns**. If you have multiple**Azure OpenAI**resources, use the one that contains your deployed chat model.Search for each of these names in the

[Azure portal](https://portal.azure.com). Open each one in a new browser tab so that you can switch between them.When you're done, you have three new browser tabs open:

**Search service**,**Foundry**, and**blobstore Container**. Keep all three tabs open because you switch between them to set up the resources.

### Enable managed identity

In the browser tab for the **Search service** resource in the Azure portal, enable managed identity:

- In the left pane, under
**Settings**, select**Identity**. - Switch
**Status**to**On**. - Select
**Save**.

In the browser tab for the **Foundry** resource in the Azure portal, enable managed identity:

- In the left pane, under
**Resource Management**, select**Identity**. - Switch
**Status**to**On**. - Select
**Save**.

### Set access control for search

In the browser tab for the **Search service** resource in the Azure portal, set the API access policy:

- In the left pane, under
**Settings**, select**Keys**. - Under
**API Access control**, select**Both**. - When prompted, select
**Yes**to confirm.

### Assign roles

Repeat this pattern for each resource in the steps below.

The general pattern for assigning role-based access control (RBAC) for any resource is:

- Navigate to the Azure portal for the given resource.
- From the left page in the Azure portal, select
**Access control (IAM)**. - Select
**+ Add**>**Add role assignment**. - Search for the role you need to assign and select it. Then select
**Next**. - When assigning a role to yourself:
- Select
**User, group, or service principal**. - Select
**Select members**. - Search for your name and select it.

- Select
- When assigning a role to another resource:
- Select
**Managed identity**. - Select
**Select members**. - Use the dropdown to find the type of resource you want to assign. For example,
**Foundry Tools**or**Search service**. - Select the resource from the list that appears. There might only be one, but you still need to select it.

- Select
- Continue through the wizard and select
**Review + assign**to add the role assignment.

Use these steps to assign roles for the resources you set up in this tutorial:

Assign these roles in the browser tab for

**Search service**in the Azure portal:**Search Index Data Reader**to the**Foundry**managed identity**Search Service Contributor**to the**Foundry**managed identity**Contributor**to yourself (to find**Contributor**, switch to the**Privileged administrator roles**tab at the top. All other roles are in the**Job function roles**tab.)

Assign these roles in the browser tab for

**Foundry**in the Azure portal:**Cognitive Services OpenAI Contributor**to the**Search service**managed identity**Contributor**to yourself.

Assign these roles in the browser tab for

**Azure Blob storage**in the Azure portal:**Storage Blob Data Contributor**to the**Foundry**managed identity**Storage Blob Data Reader**to the**Search service**managed identity**Contributor**to yourself


You're done setting up resources. You can close the Azure portal browser tabs now if you want.

## Add your data and try the chat model again

In the [Foundry playground quickstart](../quickstarts/get-started-playground?view=foundry-classic) (that's a prerequisite for this tutorial), you see how your model responds without your data. Add your data to the model so it can answer questions about your products.

To complete this section, you need a local copy of product data. The [Azure-Samples/rag-data-openai-python-promptflow repository on GitHub](https://github.com/Azure-Samples/rag-data-openai-python-promptflow/) contains sample retail product information that's relevant for this tutorial scenario. Specifically, the `product_info_11.md`

file contains product information about the TrailWalker hiking shoes that's relevant for this tutorial example. [Download the example Contoso Trek retail product data in a ZIP file](https://github.com/Azure-Samples/rag-data-openai-python-promptflow/raw/refs/heads/main/tutorial/data/product-info.zip) to your local machine.

Follow these steps to add your data in the chat playground to help the assistant answer questions about your products. You're not changing the deployed model itself. Your data is stored separately and securely in your Azure subscription.

Go to your project in

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs).Select

**Playgrounds**from the left pane.Select

**Try the chat playground**.Select your deployed chat model from the

**Deployment**dropdown.On the left side of the chat playground, select

**Add your data**>**+ Add a new data source**.In the

**Data source**dropdown, select**Upload files**.Select

**Upload**>**Upload files**to browse your local files.Select the files you want to upload. Select the product information files that you

[downloaded](https://github.com/Azure-Samples/rag-data-openai-python-promptflow/raw/refs/heads/main/tutorial/data/product-info.zip)or created earlier. Add all of the files now. You won't be able to add more files later in the same playground session.Select

**Upload**to upload the file to your Azure Blob storage account. Then select**Next**.Select your

**Azure AI Search**service.For the

**Vector index name**, enter*product-info*and select**Next**.On the

**Search settings**page under**Vector settings**, deselect the**Add vector search to this search resource**checkbox. This setting helps determine how the model responds to requests. Then select**Next**.Note

If you add vector search, more options would be available here for an additional cost.

Review your settings and select

**Create vector index**.In the playground, you can see that your data ingestion is in progress. This process might take several minutes. Before proceeding, wait until you see the data source and index name in place of the status.

You can now chat with the model asking the same question as before ("How much are the TrailWalker hiking shoes"), and this time it uses information from your data to construct the response. You can expand the

**references**button to see the data that was used.

## Deploy your web app

When you're satisfied with the experience in the Foundry portal, deploy the model as a standalone web application.

### Find your resource group in the Azure portal

In this tutorial, deploy your web app to the same resource group as your [Foundry hub](../how-to/create-secure-ai-hub?view=foundry-classic). You'll set up authentication for the web app in the Azure portal.

Follow these steps to go to your resource group in the Azure portal:

Go to your project in

[Foundry](https://ai.azure.com/?cid=learnDocs). Select**Management center**from the left pane.Under the

**Project**heading, select**Overview**.Select the resource group name to open the resource group in the Azure portal. In this example, the resource group is named

`rg-sdg-ai`

.You're now in the Azure portal, viewing the contents of the resource group where you deployed the hub. Note the resource group name and location. You'll use this information in the next section.

Keep this page open in a browser tab. You'll return to it later.


### Deploy the web app

Publishing creates an Azure App Service in your subscription. You might incur costs depending on the [pricing plan](https://azure.microsoft.com/pricing/details/app-service/windows/) you select. When you're done with your app, delete it from the Azure portal.

To deploy the web app:

Important

Register [ Microsoft.Web as a resource provider](/en-us/azure/azure-resource-manager/management/resource-providers-and-types#register-resource-provider-1) before you deploy to a web app.

Complete the steps in the previous section to

[add your data](#add-your-data-and-try-the-chat-model-again)to the playground. You can deploy a web app with or without your own data, but you need a deployed model as described in the[Foundry playground quickstart](../quickstarts/get-started-playground?view=foundry-classic).Select

**Deploy > ...as a web app**.On the

**Deploy to a web app**page, enter the following details:**Name**: A unique name for your web app.**Subscription**: Your Azure subscription. If you don't see any available subscriptions, first[register](/en-us/azure/azure-resource-manager/management/resource-providers-and-types#register-resource-provider-1).**Microsoft.Web**as a resource provider**Resource group**: Select a resource group in which to deploy the web app. Use the same resource group as the hub.**Location**: Select a location in which to deploy the web app. Use the same location as the hub.**Pricing plan**: Choose a pricing plan for the web app.**Enable chat history in the web app**: For the tutorial, the chat history box isn't selected. If you enable the feature, your users have access to their individual previous queries and responses. For more information, see[chat history remarks](#understand-chat-history).

Select

**Deploy**.Wait for the app to deploy. This process might take a few minutes.

When it's ready, the

**Launch**button is enabled on the toolbar. Don't launch the app yet, and don't close the chat playground page—you'll return to it later.

### Configure web app authentication

By default, only you can access the web app. In this tutorial, add authentication to restrict access to members of your Azure tenant. Users sign in with their Microsoft Entra account to access your app. You can follow a similar process to add another identity provider if you prefer. The app only uses the user's sign-in information to verify they're a member of your tenant.

Return to the browser tab with the Azure portal, or open the

[Azure portal](https://portal.azure.com?azure-portal=true)in a new browser tab. View the contents of the resource group where you deployed the web app. You might need to refresh the view to see the web app.Select the

**App Service**resource from the list of resources in the resource group.From the collapsible left menu under

**Settings**, select**Authentication**.If you see

**Microsoft**listed an Identity provider , nothing further is needed. You can skip the next step.Add an identity provider with the following settings:

**Identity provider**: Select Microsoft as the identity provider. The default settings  restrict the app to your tenant only, so you don't need to change anything else here.**Tenant type**: Workforce**App registration**: Create a new app registration**Name**:*The name of your web app service***Supported account types**: Current tenant - Single tenant**Restrict access**: Requires authentication**Unauthenticated requests**: HTTP 302 Found redirect - recommended for websites


### Use the web app

You're almost there. Now you can test the web app.

If you changed settings, wait about 10 minutes for the authentication settings to take effect.

Return to the browser tab with the chat playground page in the Foundry portal.

Select

**Launch**to open the deployed web app. If prompted, accept the permissions request.If you don't see

**Launch**in the playground, select**Web apps**from the left pane, then select your app from the list to open it.*If the authentication settings aren't active yet, close the browser tab for your web app and return to the chat playground in the Foundry portal. Wait a little longer, then try again.*In your web app, ask the same question as before ("How much are the TrailWalker hiking shoes"). This time, the app uses information from your data to construct the response. Expand the

**reference**button to see the data used.

## Understand chat history

With the chat history feature, your users can see their previous queries and responses.

Enable chat history when you [deploy the web app](#deploy-the-web-app). Select the **Enable chat history in the web app** checkbox.

Important

Enabling chat history creates a [Cosmos DB instance](/en-us/azure/cosmos-db/introduction) in your resource group, and incurs [additional charges](https://azure.microsoft.com/pricing/details/cosmos-db/autoscale-provisioned/) for the storage used.
Deleting your web app doesn't delete your Cosmos DB instance automatically. To delete your Cosmos DB instance and all stored chats, go to the associated resource in the Azure portal and delete it.

After you enable chat history, your users can show or hide it in the top right corner of the app. When the history is shown, they can rename or delete conversations. As they're signed in to the app, conversations are ordered from newest to oldest and named based on the first query in the conversation.

If you delete the Cosmos DB resource but keep the chat history option enabled in the studio, your users see a connection error but can keep using the web app without chat history.

## Update the web app

Use the playground to add more data or test the model with different scenarios. When you're ready to update the web app with the new model, select **Deploy > ...as a web app** again. Select **Update an existing web app**, and choose the existing web app from the list. The new model deploys to the existing web app.

## Clean up resources

To avoid unnecessary Azure costs, delete the resources you created in this quickstart if you don't need them. Manage resources in the [Azure portal](https://portal.azure.com?azure-portal=true).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/tutorials/developer-journey-idea-to-prototype -->

# Tutorial: Idea to prototype - Build and evaluate an enterprise agent

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This tutorial covers the first stage of the Microsoft Foundry developer journey: from an initial idea to a working prototype. You build a **modern workplace assistant** that combines internal company knowledge with external technical guidance by using the Microsoft Foundry SDK.

**Business scenario**: Create an AI assistant that helps employees by combining:

**Company policies**(from SharePoint documents)**Technical implementation guidance**(from Microsoft Learn via MCP)**Complete solutions**(combining both sources for business implementation)**Batch evaluation**to validate agent performance on realistic business scenarios

**Tutorial outcome**: By the end you have a running Modern Workplace Assistant that can answer policy, technical, and combined implementation questions; a repeatable batch evaluation script; and clear extension points (other tools, multi‑agent patterns, richer evaluation).

**You will:**

- Build a Modern Workplace Assistant with SharePoint and MCP integration.
- Demonstrate real business scenarios combining internal and external knowledge.
- Implement robust error handling and graceful degradation.
- Create evaluation framework for business-focused testing.
- Prepare foundation for governance and production deployment.

This minimal sample demonstrates enterprise-ready patterns with realistic business scenarios.

Important

Code in this article uses packages that are currently in preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Prerequisites

Azure subscription and CLI authentication (

`az login`

)Azure CLI 2.67.0 or later (check with

`az version`

)A Foundry

**project**with a deployed model (for example,`gpt-4o-mini`

). If you don't have one:[Create a project](../how-to/create-projects?view=foundry)and then deploy a model (see model overview:[Model catalog](../concepts/foundry-models-overview?view=foundry)).Python 3.10 or later

.NET SDK (for the C# sample)

SharePoint connection configured in your project (

[SharePoint tool documentation](../agents/how-to/tools/sharepoint?view=foundry))Note

To configure your Foundry project for SharePoint connectivity, see the

[SharePoint tool documentation](../agents/how-to/tools/sharepoint?view=foundry).(Optional) Git installed for cloning the sample repository


## Step 1: Get the sample code

Instead of navigating a large repository tree, use one of these approaches:

#### Option A (clone entire samples repo)

Tip

Code uses **Azure AI Projects 2.x (preview)** and is incompatible with Azure AI Projects 1.x.

```
git clone --depth 1 https://github.com/microsoft-foundry/foundry-samples.git
cd foundry-samples/samples/python/enterprise-agent-tutorial/1-idea-to-prototype
```


#### Option B (sparse checkout only this tutorial - reduced download)

```
git clone --no-checkout https://github.com/microsoft-foundry/foundry-samples.git
cd foundry-samples
git sparse-checkout init --cone
git sparse-checkout set samples/python/enterprise-agent-tutorial/1-idea-to-prototype
git checkout
cd samples/python/enterprise-agent-tutorial/1-idea-to-prototype
```


#### Option C (Download ZIP of repository)

Download the repository ZIP, extract it to your local environment, and go to the tutorial folder.

Important

For production adoption, use a standalone repository. This tutorial uses the shared samples repo. Sparse checkout minimizes local noise.

After you extract the ZIP, go to `samples/python/enterprise-agent-tutorial/1-idea-to-prototype`

.

The minimal structure contains only essential files:

```
enterprise-agent-tutorial/
└── 1-idea-to-prototype/
├── .env # Create this file (local environment variables)
├── .gitkeep
├── evaluate.py # Business evaluation framework
├── evaluation_results.json
├── main.py # Modern Workplace Assistant
├── questions.jsonl # Business test scenarios (4 questions)
├── requirements.txt # Python dependencies
└── sharepoint-sample-data/ # Sample business documents for SharePoint
├── collaboration-standards.docx
├── data-governance-policy.docx
├── remote-work-policy.docx
└── security-guidelines.docx
```


## Step 2: Run the sample immediately

Start by running the agent so you see working functionality before diving into implementation details.

### Environment setup and virtual environment

Install the required language runtimes, global tools, and VS Code extensions as described in

[Prepare your development environment](../how-to/develop/install-cli-sdk?view=foundry).Verify that your

`requirements.txt`

uses these published package versions (MCP support requires a prerelease of`azure-ai-agents`

):`azure-ai-agents==1.2.0b6 azure-ai-projects==1.0.0 azure-identity python-dotenv`

Install dependencies:

-
Find your project endpoint on the welcome screen of the project.

Configure

`.env`

.Set the environment values required for your language.


```
# Foundry configuration
PROJECT_ENDPOINT=https://<your-project>.aiservices.azure.com
MODEL_DEPLOYMENT_NAME=gpt-4o-mini
# The Microsoft Learn MCP Server (optional)
MCP_SERVER_URL=https://learn.microsoft.com/api/mcp
# SharePoint integration (optional - requires connection setup)
SHAREPOINT_RESOURCE_NAME=<your-sharepoint-connection-name>
```


Tip

To get your **tenant ID**, run:

```
# Get tenant ID
az account show --query tenantId -o tsv
```


To get your **project endpoint**, open your project in the [Foundry portal](https://ai.azure.com) and copy the value shown there.

### Run agent and evaluation

### Expected output (agent first run)

Successful run with SharePoint:

```
🤖 Creating Modern Workplace Assistant...
✅ SharePoint connected: YourConnection
✅ Agent created: asst_abc123
```


Graceful degradation without SharePoint:

```
⚠️ SharePoint connection not found: Connection 'YourConnection' not found
✅ Agent created: asst_abc123
```


Now that you have a working agent, the next sections explain how it works. You don't need to take any action while reading these sections—they're for explanation.

## Step 3: Set up sample SharePoint business documents

- Go to your SharePoint site (configured in the connection).
- Create document library "Company Policies" (or use existing "Documents").
- Upload the four sample Word documents provided in the
`sharepoint-sample-data`

folder:`remote-work-policy.docx`

`security-guidelines.docx`

`collaboration-standards.docx`

`data-governance-policy.docx`


### Sample structure

```
📁 Company Policies/
├── remote-work-policy.docx # VPN, MFA, device requirements
├── security-guidelines.docx # Azure security standards
├── collaboration-standards.docx # Teams, SharePoint usage
└── data-governance-policy.docx # Data classification, retention
```


## Step 4: Understand the assistant implementation

This section explains the core code in `main.py`

(Python) or `ModernWorkplaceAssistant/Program.cs`

(C#). You already ran the agent. This section is conceptual and requires no changes. After reading it, you can:

- Add new internal and external data tools.
- Extend dynamic instructions.
- Introduce multi-agent orchestration.
- Enhance observability and diagnostics.

The code breaks down into the following main sections, ordered as they appear in the full sample code:

[Configure imports and authentication](#imports-and-authentication-setup)[Configure authentication to Azure](#configure-authentication-in-azure)[Configure the SharePoint tool](#create-the-sharepoint-tool-for-the-agent)[Configure MCP tool](#create-the-mcp-tool-for-the-agent)[Create the agent and connect the tools](#create-the-agent-and-connect-the-tools)[Converse with the agent](#converse-with-the-agent)

Important

Code in this article uses packages that are currently in preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

### Imports and authentication setup

The code uses several client libraries from the Microsoft Foundry SDK to create a robust enterprise agent.

```
import os
import time
from azure.ai.agents import AgentsClient
from azure.ai.agents.models import (
SharepointTool,
SharepointGroundingToolParameters,
McpTool,
RunHandler,
ToolApproval
)
from azure.identity import DefaultAzureCredential
from dotenv import load_dotenv
# Import for connection resolution
try:
from azure.ai.projects import AIProjectClient
from azure.ai.projects.models import ConnectionType
HAS_PROJECT_CLIENT = True
except ImportError:
HAS_PROJECT_CLIENT = False
```


### Configure authentication in Azure

Before you create your agent, set up authentication to the Foundry.

```
# Support default Azure credentials
credential = DefaultAzureCredential()
agents_client = AgentsClient(
endpoint=os.environ["PROJECT_ENDPOINT"],
credential=credential,
)
print(f"✅ Connected to Azure AI Foundry: {os.environ['PROJECT_ENDPOINT']}")
```


### Create the SharePoint tool for the agent

The agent uses SharePoint and can access company policy and procedure documents stored there. Set up the connection to SharePoint in your code.

```
# Create SharePoint tool with the full ARM resource ID
sharepoint_tool = SharepointTool(connection_id=connection_id)
print(f"✅ SharePoint tool configured successfully")
```


### Create the MCP tool for the agent

```
# MCP (Model Context Protocol) enables agents to access external data sources
# like Microsoft Learn documentation. The approval flow is handled automatically
# in the chat_with_assistant function.
from azure.ai.agents.models import McpTool
mcp_server_url = os.environ.get("MCP_SERVER_URL")
mcp_tool = None
if mcp_server_url:
print(f"📚 Configuring Microsoft Learn MCP integration...")
print(f" Server URL: {mcp_server_url}")
try:
# Create MCP tool for Microsoft Learn documentation access
# server_label must match pattern: ^[a-zA-Z0-9_]+$ (alphanumeric and underscores only)
mcp_tool = McpTool(
server_url=mcp_server_url,
server_label="Microsoft_Learn_Documentation"
)
print(f"✅ MCP tool configured successfully")
except Exception as e:
print(f"⚠️ MCP tool unavailable: {e}")
print(f" Agent will operate without Microsoft Learn access")
mcp_tool = None
else:
print(f"📚 MCP integration skipped (MCP_SERVER_URL not set)")
```


### Create the agent and connect the tools

Create the agent and connect the SharePoint and MCP tools.

```
# Create the agent using Agent SDK v2 with available tools
print(f"🛠️ Creating agent with model: {os.environ['MODEL_DEPLOYMENT_NAME']}")
# Build tools list with proper serialization
tools = []
# Add SharePoint tool using .definitions property
if sharepoint_tool:
tools.extend(sharepoint_tool.definitions)
print(f" ✓ SharePoint tool added")
# Add MCP tool using .definitions property
if mcp_tool:
tools.extend(mcp_tool.definitions)
print(f" ✓ MCP tool added")
print(f" Total tools: {len(tools)}")
# Create agent with or without tools
if tools:
agent = agents_client.create_agent(
model=os.environ["MODEL_DEPLOYMENT_NAME"],
name="Modern Workplace Assistant",
instructions=instructions,
tools=tools
)
else:
agent = agents_client.create_agent(
model=os.environ["MODEL_DEPLOYMENT_NAME"],
name="Modern Workplace Assistant",
instructions=instructions,
)
print(f"✅ Agent created successfully: {agent.id}")
return agent
```


### Converse with the agent

Finally, implement an interactive loop to converse with the agent.

```
# Get response from the agent
print("🤖 ASSISTANT RESPONSE:")
response, status = chat_with_assistant(agent.id, scenario['question'])
```


### Expected output from agent sample code

When you run the agent, you see output similar to the following example. The output shows successful tool configuration and agent responses to business scenarios:

```
✅ Connected to Foundry
🚀 Foundry - Modern Workplace Assistant
Tutorial 1: Building Enterprise Agents with Microsoft Foundry Project SDK
======================================================================
🤖 Creating Modern Workplace Assistant...
📁 Configuring SharePoint integration...
Connection name: ContosoCorpPoliciesProcedures
🔍 Resolving connection name to ARM resource ID...
✅ Resolved
✅ SharePoint tool configured successfully
📚 Configuring Microsoft Learn MCP integration...
Server URL: https://learn.microsoft.com/api/mcp
✅ MCP tool configured successfully
🛠️ Creating agent with model: gpt-4o-mini
✓ SharePoint tool added
✓ MCP tool added
Total tools: 2
✅ Agent created successfully
======================================================================
🏢 MODERN WORKPLACE ASSISTANT - BUSINESS SCENARIO DEMONSTRATION
======================================================================
This demonstration shows how AI agents solve real business problems
using the Azure AI Agents SDK v2.
======================================================================
📊 SCENARIO 1/3: 📋 Company Policy Question (SharePoint Only)
--------------------------------------------------
❓ QUESTION: What is Contosoʹs remote work policy?
🎯 BUSINESS CONTEXT: Employee needs to understand company-specific remote work requirements
🎓 LEARNING POINT: SharePoint tool retrieves internal company policies
--------------------------------------------------
🤖 ASSISTANT RESPONSE:
✅ SUCCESS: Contosoʹs remote work policy, effective January 2024, outlines the following key points:
### Overview
Contoso Corp supports flexible work arrangements, including remote work, to enhance employee productivity and work-life balance.
### Eligibility
- **Full-time Employees**: Must have completed a 90...
📏 Full response: 1530 characters
📈 STATUS: completed
--------------------------------------------------
📊 SCENARIO 2/3: 📚 Technical Documentation Question (MCP Only)
--------------------------------------------------
❓ QUESTION: According to Microsoft Learn, what is the correct way to implement Azure AD Conditional Access policies? Please include reference links to the official documentation.
🎯 BUSINESS CONTEXT: IT administrator needs authoritative Microsoft technical guidance
🎓 LEARNING POINT: MCP tool accesses Microsoft Learn for official documentation with links
--------------------------------------------------
🤖 ASSISTANT RESPONSE:
✅ SUCCESS: To implement Azure AD Conditional Access policies correctly, follow these key steps outlined in the Microsoft Learn documentation:
### 1. Understanding Conditional Access
Conditional Access policies act as "if-then" statements that enforce organizational access controls based on various signals. Th...
📏 Full response: 2459 characters
📈 STATUS: completed
--------------------------------------------------
📊 SCENARIO 3/3: 🔄 Combined Implementation Question (SharePoint + MCP)
--------------------------------------------------
❓ QUESTION: Based on our companyʹs remote work security policy, how should I configure my Azure environment to comply? Please include links to Microsoft documentation showing how to implement each requirement.
🎯 BUSINESS CONTEXT: Need to map company policy to technical implementation with official guidance
🎓 LEARNING POINT: Both tools work together: SharePoint for policy + MCP for implementation docs
--------------------------------------------------
🤖 ASSISTANT RESPONSE:
✅ SUCCESS: To configure your Azure environment in compliance with Contoso Corpʹs remote work security policy, you need to focus on several key areas, including enabling Multi-Factor Authentication (MFA), utilizing Azure Security Center, and implementing proper access management. Below are specific steps and li...
📏 Full response: 3436 characters
📈 STATUS: completed
--------------------------------------------------
✅ DEMONSTRATION COMPLETED!
🎓 Key Learning Outcomes:
• Microsoft Foundry Project SDK usage for enterprise AI
• Proper thread and message management
• Real business value through AI assistance
• Foundation for governance and monitoring (Tutorials 2-3)
🎯 Try interactive mode? (y/n): n
🎉 Sample completed successfully!
📚 This foundation supports Tutorial 2 (Governance) and Tutorial 3 (Production)
🔗 Next: Add evaluation metrics, monitoring, and production deployment
```


## Step 5: Evaluate the assistant by using cloud evaluation

The evaluation framework tests realistic business scenarios by using the **cloud evaluation** capability of the Microsoft Foundry SDK. Instead of a custom local approach, this pattern uses the built-in evaluators (`builtin.violence`

, `builtin.fluency`

, `builtin.task_adherence`

) and the `openai_client.evals`

API to run scalable, repeatable evaluations in the cloud.

This evaluation framework demonstrates:

**Agent targeting**: The evaluation runs queries directly against your agent by using`azure_ai_target_completions`

.**Built-in evaluators**: Safety (violence detection), quality (fluency), and task adherence metrics.**Cloud-based execution**: Eliminates local compute requirements and supports CI/CD integration.**Structured results**: Pass/fail labels, scores, and reasoning for each test case.

The code breaks down into the following main sections:

Tip

For detailed guidance on cloud evaluations, see [Run evaluations in the cloud](../how-to/develop/cloud-evaluation?view=foundry). To find a comprehensive list of built-in evaluators available in Foundry, see [Observability in generative AI](../concepts/observability?view=foundry).

Note

The C# SDK uses **protocol methods** with `BinaryData`

and `BinaryContent`

instead of typed objects. This approach requires helper methods to parse JSON responses. See the [C# Evaluations SDK sample](https://github.com/Azure/azure-sdk-for-net/blob/feature/ai-foundry/agents-v2/sdk/ai/Azure.AI.Projects/samples/Sample21_Evaluations.md) for the complete pattern.

### Configure the evaluation

First, create an evaluation object that defines your data schema and testing criteria. The evaluation uses built-in evaluators for violence detection, fluency, and task adherence.

In Python, use the OpenAI client directly. In C#, get an `EvaluationClient`

from the project client:

```
load_dotenv()
endpoint = os.environ["AZURE_AI_PROJECT_ENDPOINT"]
model_deployment_name = os.environ.get("AZURE_AI_MODEL_DEPLOYMENT_NAME", "gpt-4o-mini")
with (
DefaultAzureCredential() as credential,
AIProjectClient(endpoint=endpoint, credential=credential) as project_client,
project_client.get_openai_client() as openai_client,
):
# Create or retrieve the agent to evaluate
agent = project_client.agents.create_version(
agent_name=os.environ.get("AZURE_AI_AGENT_NAME", "Modern Workplace Assistant"),
definition=PromptAgentDefinition(
model=model_deployment_name,
instructions="You are a helpful Modern Workplace Assistant that answers questions about company policies and technical guidance.",
),
)
print(f"Agent created (id: {agent.id}, name: {agent.name}, version: {agent.version})")
# Define the data schema for evaluation
data_source_config = DataSourceConfigCustom(
type="custom",
item_schema={
"type": "object",
"properties": {"query": {"type": "string"}},
"required": ["query"]
},
include_sample_schema=True,
)
# Define testing criteria with built-in evaluators
# data_mapping: sample.output_text = agent string response, sample.output_items = structured JSON with tool calls
testing_criteria = [
{
"type": "azure_ai_evaluator",
"name": "violence_detection",
"evaluator_name": "builtin.violence",
"data_mapping": {"query": "{{item.query}}", "response": "{{sample.output_text}}"},
},
{
"type": "azure_ai_evaluator",
"name": "fluency",
"evaluator_name": "builtin.fluency",
"initialization_parameters": {"deployment_name": f"{model_deployment_name}"},
"data_mapping": {"query": "{{item.query}}", "response": "{{sample.output_text}}"},
},
{
"type": "azure_ai_evaluator",
"name": "task_adherence",
"evaluator_name": "builtin.task_adherence",
"initialization_parameters": {"deployment_name": f"{model_deployment_name}"},
"data_mapping": {"query": "{{item.query}}", "response": "{{sample.output_items}}"},
},
]
# Create the evaluation object
eval_object = openai_client.evals.create(
name="Agent Evaluation",
data_source_config=data_source_config,
testing_criteria=testing_criteria,
)
print(f"Evaluation created (id: {eval_object.id}, name: {eval_object.name})")
```


The `testing_criteria`

array specifies which evaluators to run:

`builtin.violence`

: Detects violent or harmful content in responses.`builtin.fluency`

: Assesses response quality and readability (requires a model deployment).`builtin.task_adherence`

: Evaluates whether the agent followed instructions correctly.

### Run the cloud evaluation

Create an evaluation run that targets your agent. The `azure_ai_target_completions`

data source sends queries to your agent and captures responses for evaluation:

```
# Define the data source for the evaluation run
# This targets the agent with test queries
data_source = {
"type": "azure_ai_target_completions",
"source": {
"type": "file_content",
"content": [
{"item": {"query": "What is Contoso's remote work policy?"}},
{"item": {"query": "What are the security requirements for remote employees?"}},
{"item": {"query": "According to Microsoft Learn, how do I configure Azure AD Conditional Access?"}},
{"item": {"query": "Based on our company policy, how should I configure Azure security to comply?"}},
],
},
"input_messages": {
"type": "template",
"template": [
{"type": "message", "role": "user", "content": {"type": "input_text", "text": "{{item.query}}"}}
],
},
"target": {
"type": "azure_ai_agent",
"name": agent.name,
"version": agent.version,
},
}
# Create and submit the evaluation run
agent_eval_run: Union[RunCreateResponse, RunRetrieveResponse] = openai_client.evals.runs.create(
eval_id=eval_object.id,
name=f"Evaluation Run for Agent {agent.name}",
data_source=data_source,
)
print(f"Evaluation run created (id: {agent_eval_run.id})")
```


The `data_source`

configuration:

**type**:`azure_ai_target_completions`

routes queries through your agent**source**: Inline content with test queries (you can also use a dataset file ID)**input_messages**: Template that formats each query for the agent**target**: Specifies the agent name and version to evaluate

### Retrieve evaluation results

Poll the evaluation run until it completes, then retrieve the detailed output items:

```
# Poll until the evaluation run completes
while agent_eval_run.status not in ["completed", "failed"]:
agent_eval_run = openai_client.evals.runs.retrieve(
run_id=agent_eval_run.id,
eval_id=eval_object.id
)
print(f"Waiting for eval run to complete... current status: {agent_eval_run.status}")
time.sleep(5)
if agent_eval_run.status == "completed":
print("\n✓ Evaluation run completed successfully!")
print(f"Result Counts: {agent_eval_run.result_counts}")
# Retrieve detailed output items
output_items = list(
openai_client.evals.runs.output_items.list(
run_id=agent_eval_run.id,
eval_id=eval_object.id
)
)
print(f"\nOUTPUT ITEMS (Total: {len(output_items)})")
print(f"{'-'*60}")
pprint(output_items)
print(f"{'-'*60}")
print(f"Eval Run Report URL: {agent_eval_run.report_url}")
else:
print("\n✗ Evaluation run failed.")
# Cleanup
openai_client.evals.delete(eval_id=eval_object.id)
print("Evaluation deleted")
project_client.agents.delete(agent_name=agent.name)
print("Agent deleted")
```


Each output item includes:

**Label**: Binary "pass" or "fail" result**Score**: Numeric score on the evaluator's scale**Reason**: Explanation of why the score was assigned (for LLM-based evaluators)

### Expected output from cloud evaluation (evaluate.py)

When you run the evaluation script, you see output similar to the following example. The output shows the evaluation object creation, run submission, and results retrieval:

```
python evaluate.py
Agent created (id: asst_abc123, name: Modern Workplace Assistant, version: 1)
Evaluation created (id: eval_xyz789, name: Agent Evaluation)
Evaluation run created (id: run_def456)
Waiting for eval run to complete... current status: running
Waiting for eval run to complete... current status: running
✓ Evaluation run completed successfully!
Result Counts: {'passed': 2, 'failed': 0, 'errored': 0}
OUTPUT ITEMS (Total: 2)
------------------------------------------------------------
[OutputItem(id='item_1',
sample={'query': 'What is the largest city in France?',
'output_text': 'The largest city in France is Paris...'},
results=[{'name': 'violence_detection', 'passed': True, 'score': 0},
{'name': 'fluency', 'passed': True, 'score': 4,
'reason': 'Response is clear and well-structured'},
{'name': 'task_adherence', 'passed': True, 'score': 5}]),
OutputItem(id='item_2', ...)]
------------------------------------------------------------
Eval Run Report URL: https://ai.azure.com/...
Evaluation deleted
Agent deleted
```


### Understanding evaluation results

Cloud evaluations provide structured results that you can view in the Foundry portal or retrieve programmatically. Each output item includes:

| Field | Description |
|---|---|
Label |
Binary "pass" or "fail" based on the threshold |
Score |
Numeric score (scale depends on evaluator type) |
Threshold |
The cutoff value that determines pass/fail |
Reason |
LLM-generated explanation for the score (when applicable) |

**Score scales by evaluator type:**

**Quality evaluators**(fluency, coherence): 1-5 scale**Safety evaluators**(violence, self-harm): 0-7 severity scale (lower is safer)**Task evaluators**(task_adherence): 1-5 scale

You can also view detailed results in the Foundry portal by selecting **Evaluation** from your project and selecting the evaluation run. The portal provides visualizations, filtering, and export options.

Tip

For production scenarios, consider running evaluations as part of your CI/CD pipeline. See [How to run an evaluation in Azure DevOps](../how-to/evaluation-azure-devops?view=foundry), and [Continuously evaluate your AI agents](../how-to/continuous-evaluation-agents?view=foundry) for integration patterns.

## Summary

You now have:

- A working single-agent prototype grounded in internal and external knowledge.
- A repeatable evaluation script demonstrating enterprise validation patterns.
- A clear upgrade path: more tools, multi-agent orchestration, richer evaluation, deployment.

These patterns reduce prototype-to-production friction: you can add data sources, enforce governance, and integrate monitoring without rewriting core logic.

## Next steps

This tutorial demonstrates **Stage 1** of the developer journey - from idea to prototype. This minimal sample provides the foundation for enterprise AI development. To continue your journey, explore the next stages:

### Suggested additional enhancements

- Add more data sources (
[Azure AI Search](../agents/how-to/tools/ai-search?view=foundry),[other sources](../how-to/connections-add?view=foundry)). - Implement advanced evaluation methods (
[AI-assisted evaluation](../how-to/develop/evaluate-sdk?view=foundry)). - Create
[custom tools](../agents/how-to/private-tool-catalog?view=foundry)for business-specific operations. - Add
[conversation memory and personalization](/en-us/azure/cosmos-db/gen-ai/azure-agent-service).

### Stage 2: Prototype to production

[Implement safety assessment with red-team testing](../how-to/develop/run-scans-ai-red-teaming-agent?view=foundry).[Create comprehensive evaluation datasets with quality metrics](../fine-tuning/data-generation?view=foundry).[Apply organization-wide governance policies and model comparison](../how-to/built-in-policy-model-deployment?view=foundry).[Configure fleet monitoring, CI/CD integration, and production deployment endpoints](../concepts/deployments-overview?view=foundry).

### Stage 3: Production to adoption

[Collect trace data and user feedback from production deployments](../observability/how-to/trace-agent-framework?view=foundry).[Fine-tune models and generate evaluation insights for continuous improvement](../openai/how-to/fine-tuning?view=foundry).[Integrate Azure API Management gateway with continuous quality monitoring](../configuration/enable-ai-api-management-gateway-portal?view=foundry).[Implement fleet governance, compliance controls, and cost optimization](/en-us/azure/cloud-adoption-framework/scenarios/ai/platform/governance).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/tutorials/copilot-sdk-build-rag -->

# Tutorial:  Part 2 - Build a custom knowledge retrieval (RAG) app with the Microsoft Foundry SDK

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

In this tutorial, you use the [Microsoft Foundry](https://ai.azure.com/?cid=learnDocs) SDK and other libraries to build, configure, and evaluate a chat app for your retail company called Contoso Trek. Your retail company specializes in outdoor camping gear and clothing. The chat app answers questions about your products and services. For example, the chat app can answer questions such as "which tent is the most waterproof?" or "what is the best sleeping bag for cold weather?".

This part two shows you how to enhance a basic chat application by adding [retrieval augmented generation (RAG)](../concepts/retrieval-augmented-generation?view=foundry-classic) to ground the responses in your custom data. Retrieval Augmented Generation (RAG) is a pattern that uses your data with a large language model (LLM) to generate answers specific to your data. In this part two, you learn how to:

- Get example data
- Create a search index of the data for the chat app to use
- Develop custom RAG code

This tutorial builds on [Tutorial: Part 1 - Create resources for building a custom chat application with the Microsoft Foundry SDK](copilot-sdk-create-resources?view=foundry-classic).

Important

This example uses Azure AI Inference beta SDK. We recommend that you transition to the generally available [OpenAI/v1 API](https://aka.ms/openai/v1), which uses an OpenAI stable SDK.

For more information on how to migrate to the OpenAI/v1 API by using an SDK in your programming language of choice, see [Migrate from Azure AI Inference SDK to OpenAI SDK](../how-to/model-inference-to-openai-migration?view=foundry-classic).

## Prerequisites

Important

This article provides legacy support for hub-based projects. It will not work for **Foundry projects**. See [How do I know which type of project I have?](../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have)

**SDK compatibility note**: Code examples require a specific Microsoft Foundry SDK version. If you encounter compatibility issues, consider [migrating from a hub-based to a Foundry project](../how-to/migrate-project?view=foundry-classic).

- An Azure account with an active subscription. If you don't have one, create a
[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - If you don't have one,
[create a hub-based project](../how-to/hub-create-projects?view=foundry-classic).

- Complete
[Tutorial: Part 1 - Create resources for building a custom chat application with the Microsoft Foundry SDK](copilot-sdk-create-resources?view=foundry-classic)to:- Create a project with a connected Azure AI Search index.
- Install the Azure CLI, Python, and required packages.
- Configure your environment variables.

- Use the same
**hub-based**project you created in Part 1. **Azure AI permissions**: Owner or Contributor role to create search indexes and deploy models; Cognitive Services Contributor or higher for AI Services resources.

## Verify your setup

Before building the RAG app, confirm that your environment is properly configured by running a quick connection test:

```
import os
from azure.identity import DefaultAzureCredential
import azure.ai.projects
# Check the SDK version
print(f"Azure AI Projects SDK version: {azure.ai.projects.__version__}")
# Test that you can connect to your project
project = AIProjectClient.from_connection_string(
conn_str=os.environ["AIPROJECT_CONNECTION_STRING"], credential=DefaultAzureCredential()
)
print("✓ Setup verified! Ready to build your RAG app.")
```


If you see the success message, your Azure credentials and SDK are configured correctly. If you encounter authentication errors, verify your `FOUNDRY_*`

environment variables are set correctly (see Part 1 prerequisites).

Tip

This tutorial requires Azure AI Projects SDK version `1.0.0b10`

. The SDK version displayed above helps you verify compatibility. If you have a different version, the `from_connection_string()`

method may not be available. To install the required version, run `pip install azure-ai-projects==1.0.0b10`

.

References: [AIProjectClient](/en-us/python/api/azure-ai-projects/azure.ai.projects.AIProjectClient), [DefaultAzureCredential](/en-us/python/api/azure-identity/azure.identity.DefaultAzureCredential).

## Create example data for your chat app

The goal with this RAG-based application is to ground the model responses in your custom data. You use an Azure AI Search index that stores vectorized data from the embeddings model. The search index is used to retrieve relevant documents based on the user's question.

If you already have a search index with data, you can skip to [Get product documents](#get-product-documents). Otherwise, you can create a simple example data set to use in your chat app.

Create an **assets** directory and add this example data to a **products.csv** file:

```
id,name,price,category,brand,description
1,TrailMaster X4 Tent,250.0,Tents,OutdoorLiving,"Unveiling the TrailMaster X4 Tent from OutdoorLiving, your home away from home for your next camping adventure. Crafted from durable polyester, this tent boasts a spacious interior perfect for four occupants. It ensures your dryness under drizzly skies thanks to its water-resistant construction, and the accompanying rainfly adds an extra layer of weather protection. It offers refreshing airflow and bug defence, courtesy of its mesh panels. Accessibility is not an issue with its multiple doors and interior pockets that keep small items tidy. Reflective guy lines grant better visibility at night, and the freestanding design simplifies setup and relocation. With the included carry bag, transporting this convenient abode becomes a breeze. Be it an overnight getaway or a week-long nature escapade, the TrailMaster X4 Tent provides comfort, convenience, and concord with the great outdoors. Comes with a two-year limited warranty to ensure customer satisfaction."
2,Adventurer Pro Backpack,90.0,Backpacks,HikeMate,"Venture into the wilderness with the HikeMate's Adventurer Pro Backpack! Uniquely designed with ergonomic comfort in mind, this backpack ensures a steadfast journey no matter the mileage. It boasts a generous 40L capacity wrapped up in durable nylon fabric ensuring its long-lasting performance on even the most rugged pursuits. It's meticulously fashioned with multiple compartments and pockets for organized storage, hydration system compatibility, and adjustable padded shoulder straps all in a lightweight construction. The added features of a sternum strap and hip belt enhance stability without compromising on comfort. The Adventurer Pro Backpack also prioritizes your safety with its reflective accents for when night falls. This buoyant beauty does more than carry your essentials; it carries the promise of a stress-free adventure!"
3,Summit Breeze Jacket,120.0,Hiking Clothing,MountainStyle,"Discover the joy of hiking with MountainStyle's Summit Breeze Jacket. This lightweight jacket is your perfect companion for outdoor adventures. Sporting a trail-ready, windproof design and a water-resistant fabric, it's ready to withstand any weather. The breathable polyester material and adjustable cuffs keep you comfortable, whether you're ascending a mountain or strolling through a park. And its sleek black color adds style to function. The jacket features a full-zip front closure, adjustable hood, and secure zippered pockets. Experience the comfort of its inner lining and the convenience of its packable design. Crafted for night trekkers too, the jacket has reflective accents for enhanced visibility. Rugged yet chic, the Summit Breeze Jacket is more than a hiking essential, it's the gear that inspires you to reach new heights. Choose adventure, choose the Summit Breeze Jacket."
4,TrekReady Hiking Boots,140.0,Hiking Footwear,TrekReady,"Introducing the TrekReady Hiking Boots - stepping up your hiking game, one footprint at a time! Crafted from leather, these stylistic Trailmates are made to last. TrekReady infuses durability with its reinforced stitching and toe protection, making sure your journey is never stopped short. Comfort? They have that covered too! The boots are a haven with their breathable materials, cushioned insole, with padded collar and tongue; all nestled neatly within their lightweight design. As they say, it's what's inside that counts - so inside you'll find a moisture-wicking lining that quarantines stank and keeps your feet fresh as that mountaintop breeze. Remember the fear of slippery surfaces? With these boots, you can finally tell it to 'take a hike'! Their shock-absorbing midsoles and excellent traction capabilities promise stability at your every step. Beautifully finished in a traditional lace-up system, every adventurer deserves a pair of TrekReady Hiking Boots. Hike more, worry less!"
5,BaseCamp Folding Table,60.0,Camping Tables,CampBuddy,"CampBuddy's BaseCamp Folding Table is an adventurer's best friend. Lightweight yet powerful, the table is a testament to fun-meets-function and will elevate any outing to new heights. Crafted from resilient, rust-resistant aluminum, the table boasts a generously sized 48 x 24 inches tabletop, perfect for meal times, games and more. The foldable design is a godsend for on-the-go explorers. Adjustable legs rise to the occasion to conquer uneven terrains and offer height versatility, while the built-in handle simplifies transportation. Additional features like non-slip feet, integrated cup holders and mesh pockets add a pinch of finesse. Quick to set up without the need for extra tools, this table is a silent yet indispensable sidekick during camping, picnics, and other outdoor events. Don't miss out on the opportunity to take your outdoor experiences to a new level with the BaseCamp Folding Table. Get yours today and embark on new adventures tomorrow! "
6,EcoFire Camping Stove,80.0,Camping Stoves,EcoFire,"Introducing EcoFire's Camping Stove, your ultimate companion for every outdoor adventure! This portable wonder is precision-engineered with a lightweight and compact design, perfect for capturing that spirit of wanderlust. Made from high-quality stainless steel, it promises durability and steadfast performance. This stove is not only fuel-efficient but also offers an easy, intuitive operation that ensures hassle-free cooking. Plus, it's flexible, accommodating a variety of cooking methods whether you're boiling, grilling, or simmering under the starry sky. Its stable construction, quick setup, and adjustable flame control make cooking a breeze, while safety features protect you from any potential mishaps. And did we mention it also includes an effective wind protector and a carry case for easy transportation? But that's not all! The EcoFire Camping Stove is eco-friendly, designed to minimize environmental impact. So get ready to enhance your camping experience and enjoy delicious outdoor feasts with this unique, versatile stove!"
7,CozyNights Sleeping Bag,100.0,Sleeping Bags,CozyNights,"Embrace the great outdoors in any season with the lightweight CozyNights Sleeping Bag! This durable three-season bag is superbly designed to give hikers, campers, and backpackers comfort and warmth during spring, summer, and fall. With a compact design that folds down into a convenient stuff sack, you can whisk it away on any adventure without a hitch. The sleeping bag takes comfort seriously, featuring a handy hood, ample room and padding, and a reliable temperature rating. Crafted from high-quality polyester, it ensures long-lasting use and can even be zipped together with another bag for shared comfort. Whether you're gazing at stars or catching a quick nap between trails, the CozyNights Sleeping Bag makes it a treat. Don't just sleep— dream with CozyNights."
8,Alpine Explorer Tent,350.0,Tents,AlpineGear,"Welcome to the joy of camping with the Alpine Explorer Tent! This robust, 8-person, 3-season marvel is from the responsible hands of the AlpineGear brand. Promising an enviable setup that is as straightforward as counting sheep, your camping experience is transformed into a breezy pastime. Looking for privacy? The detachable divider provides separate spaces at a moment's notice. Love a tent that breathes? The numerous mesh windows and adjustable vents fend off any condensation dragon trying to dampen your adventure fun. The waterproof assurance keeps you worry-free during unexpected rain dances. With a built-in gear loft to stash away your outdoor essentials, the Alpine Explorer Tent emerges as a smooth balance of privacy, comfort, and convenience. Simply put, this tent isn't just a shelter - it's your second home in the heart of nature! Whether you're a seasoned camper or a nature-loving novice, this tent makes exploring the outdoors a joyous journey."
9,SummitClimber Backpack,120.0,Backpacks,HikeMate,"Adventure waits for no one! Introducing the HikeMate SummitClimber Backpack, your reliable partner for every exhilarating journey. With a generous 60-liter capacity and multiple compartments and pockets, packing is a breeze. Every feature points to comfort and convenience; the ergonomic design and adjustable hip belt ensure a pleasantly personalized fit, while padded shoulder straps protect you from the burden of carrying. Venturing into wet weather? Fear not! The integrated rain cover has your back, literally. Stay hydrated thanks to the backpack's hydration system compatibility. Travelling during twilight? Reflective accents keep you visible in low-light conditions. The SummitClimber Backpack isn't merely a carrier; it's a wearable base camp constructed from ruggedly durable nylon and thoughtfully designed for the great outdoors adventurer, promising to withstand tough conditions and provide years of service. So, set off on that quest - the wild beckons! The SummitClimber Backpack - your hearty companion on every expedition!"
10,TrailBlaze Hiking Pants,75.0,Hiking Clothing,MountainStyle,"Meet the TrailBlaze Hiking Pants from MountainStyle, the stylish khaki champions of the trails. These are not just pants; they're your passport to outdoor adventure. Crafted from high-quality nylon fabric, these dapper troopers are lightweight and fast-drying, with a water-resistant armor that laughs off light rain. Their breathable design whisks away sweat while their articulated knees grant you the flexibility of a mountain goat. Zippered pockets guard your essentials, making them a hiker's best ally. Designed with durability for all your trekking trials, these pants come with a comfortable, ergonomic fit that will make you forget you're wearing them. Sneak a peek, and you are sure to be tempted by the sleek allure that is the TrailBlaze Hiking Pants. Your outdoors wardrobe wouldn't be quite complete without them."
11,TrailWalker Hiking Shoes,110.0,Hiking Footwear,TrekReady,"Meet the TrekReady TrailWalker Hiking Shoes, the ideal companion for all your outdoor adventures. Constructed with synthetic leather and breathable mesh, these shoes are tough as nails yet surprisingly airy. Their cushioned insoles offer fabulous comfort for long hikes, while the supportive midsoles and traction outsoles with multidirectional lugs ensure stability and excellent grip. A quick-lace system, padded collar and tongue, and reflective accents make these shoes a dream to wear. From combating rough terrain with the reinforced toe cap and heel, to keeping off trail debris with the protective mudguard, the TrailWalker Hiking Shoes have you covered. These waterproof warriors are made to endure all weather conditions. But they're not just about being rugged, they're light as a feather too, minimizing fatigue during epic hikes. Each pair can be customized for a perfect fit with removable insoles and availability in multiple sizes and widths. Navigate hikes comfortably and confidently with the TrailWalker Hiking Shoes. Adventure, here you come!"
12,TrekMaster Camping Chair,50.0,Camping Tables,CampBuddy,"Gravitate towards comfort with the TrekMaster Camping Chair from CampBuddy. This trusty outdoor companion boasts sturdy construction using high-quality materials that promise durability and enjoyment for seasons to come. Impeccably lightweight and portable, it's designed to be your go-to seat whether you're camping, at a picnic, cheering at a sporting event, or simply relishing in your backyard pleasures. Beyond its foldable design ensuring compact storage and easy transportation, its ergonomic magic is in the details. An adjustable recline, padded seat and backrest, integrated cup holder, and side pockets ensure the greatest outdoor comfort. Weather resistant, easy to clean, and capable of supporting diverse body types, this versatile chair also comes with a carry bag, ready for your next adventure."
13,PowerBurner Camping Stove,100.0,Camping Stoves,PowerBurner,"Unleash your inner explorer with the PowerBurner Dual Burner Camping Stove. It's designed for the adventurous heart, with sturdy construction and a high heat output that makes boiling and cooking a breeze. This stove isn't just about strength—it's got finesse too. With adjustable flame control, you can simmer, sauté, or sizzle with absolute precision. Its compact design and integrated carrying handle make transportation effortless. Moreover, it's crafted to defy the elements, boasting a wind-resistant exterior and piezo ignition system for quick, reliable starts. And when the cooking's done, its removable grates make cleanup swift and easy. Rugged, versatile and reliable, the PowerBurner marks a perfect blend of practicality and performance. So, why wait? Let's turn up the heat on your outdoor culinary adventures today."
14,MountainDream Sleeping Bag,130.0,Sleeping Bags,MountainDream,"Meet the MountainDream Sleeping Bag: your new must-have companion for every outdoor adventure. Designed to handle 3-season camping with ease, it comes equipped with a premium synthetic insulation that will keep you cozy even when temperatures fall down to 15°F! Sporting a durable water-resistant nylon shell and soft breathable polyester lining, this bag doesn't sacrifice comfort for toughness. The star of the show is the contoured mummy shape that not only provides optimal heat retention but also cuts down on the weight. A smooth, snag-free YKK zipper with a unique anti-snag design allows for hassle-free operation, while the adjustable hood and full-length zipper baffle work together to ensure you stay warm all night long. Need to bring along some essentials? Not to worry! There's an interior pocket just for that. And when it's time to pack up? Just slip it into the included compression sack for easy storage and transport. Whether you're a backpacking pro or a camping novice, the MountainDream Sleeping Bag is the perfect blend of durability, warmth, and comfort that you've been looking for."
15,SkyView 2-Person Tent,200.0,Tents,OutdoorLiving,"Introducing the OutdoorLiving SkyView 2-Person Tent, a perfect companion for your camping and hiking adventures. This tent offers a spacious interior that houses two people comfortably, with room to spare. Crafted from durable waterproof materials to shield you from the elements, it is the fortress you need in the wild. Setup is a breeze thanks to its intuitive design and color-coded poles, while two large doors allow for easy access. Stay organized with interior pockets, and store additional gear in its two vestibules. The tent also features mesh panels for effective ventilation, and it comes with a rainfly for extra weather protection. Light enough for on-the-go adventurers, it packs compactly into a carrying bag for seamless transportation. Reflective guy lines ensure visibility at night for added safety, and the tent stands freely for versatile placement. Experience the reliability of double-stitched seams that guarantee increased durability, and rest easy under the stars with OutdoorLiving's SkyView 2-Person Tent. It's not just a tent; it's your home away from home."
16,TrailLite Daypack,60.0,Backpacks,HikeMate,"Step up your hiking game with HikeMate's TrailLite Daypack. Built for comfort and efficiency, this lightweight and durable backpack offers a spacious main compartment, multiple pockets, and organization-friendly features all in one sleek package. The adjustable shoulder straps and padded back panel ensure optimal comfort during those long exhilarating treks. Course through nature without worry as the daypack's water-resistant fabric protects your essentials from unexpected showers. Plus, never run dry with the integrated hydration system. And did we mention it comes in a plethora of colors and designs? So you can choose one that truly speaks to your outdoorsy soul! Keeping your visibility in mind, we've added reflective accents that light up in low-light conditions. Don't just carry a backpack, adorn a companion that takes you a step ahead in your adventures. Trust the TrailLite Daypack for a hassle-free, enjoyable hiking experience."
17,RainGuard Hiking Jacket,110.0,Hiking Clothing,MountainStyle,"Introducing the MountainStyle RainGuard Hiking Jacket - the ultimate solution for weatherproof comfort during your outdoor undertakings! Designed with waterproof, breathable fabric, this jacket promises an outdoor experience that's as dry as it is comfortable. The rugged construction assures durability, while the adjustable hood provides a customizable fit against wind and rain. Featuring multiple pockets for safe, convenient storage and adjustable cuffs and hem, you can tailor the jacket to suit your needs on-the-go. And, don't worry about overheating during intense activities - it's equipped with ventilation zippers for increased airflow. Reflective details ensure visibility even during low-light conditions, making it perfect for evening treks. With its lightweight, packable design, carrying it inside your backpack requires minimal effort. With options for men and women, the RainGuard Hiking Jacket is perfect for hiking, camping, trekking and countless other outdoor adventures. Don't let the weather stand in your way - embrace the outdoors with MountainStyle RainGuard Hiking Jacket!"
18,TrekStar Hiking Sandals,70.0,Hiking Footwear,TrekReady,"Meet the TrekStar Hiking Sandals from TrekReady - the ultimate trail companion for your feet. Designed for comfort and durability, these lightweight sandals are perfect for those who prefer to see the world from a hiking trail. They feature adjustable straps for a snug, secure fit, perfect for adapting to the contours of your feet. With a breathable design, your feet will stay cool and dry, escaping the discomfort of sweaty hiking boots on long summer treks. The deep tread rubber outsole ensures excellent traction on any terrain, while the cushioned footbed promises enhanced comfort with every step. For those wild and unpredictable trails, the added toe protection and shock-absorbing midsole protect your feet from rocky surprises. Ingeniously, the removable insole makes for easy cleaning and maintenance, extending the lifespan of your sandals. Available in various sizes and a handsome brown color, the versatile TrekStar Hiking Sandals are just as comfortable on a casual walk in the park as they are navigating rocky slopes. Explore more with TrekReady!"
19,Adventure Dining Table,90.0,Camping Tables,CampBuddy,"Discover the joy of outdoor adventures with the CampBuddy Adventure Dining Table. This feature-packed camping essential brings both comfort and convenience to your memorable trips. Made from high-quality aluminum, it promises long-lasting performance, weather resistance, and easy maintenance - all key for the great outdoors! It's light, portable, and comes with adjustable height settings to suit various seating arrangements and the spacious surface comfortably accommodates meals, drinks, and other essentials. The sturdy yet lightweight frame holds food, dishes, and utensils with ease. When it's time to pack up, it fold and stows away with no fuss, ready for the next adventure! Perfect for camping, picnics, barbecues, and beach outings - its versatility shines as brightly as the summer sun! Durable, sturdy and a breeze to set up, the Adventure Dining Table will be a loyal companion on every trip. Embark on your next adventure and make lifetime memories with CampBuddy. As with all good experiences, it'll leave you wanting more! "
20,CompactCook Camping Stove,60.0,Camping Stoves,CompactCook,"Step into the great outdoors with the CompactCook Camping Stove, a convenient, lightweight companion perfect for all your culinary camping needs. Boasting a robust design built for harsh environments, you can whip up meals anytime, anywhere. Its wind-resistant and fuel-versatile features coupled with an efficient cooking performance, ensures you won't have to worry about the elements or helpless taste buds while on adventures. The easy ignition technology and adjustable flame control make cooking as easy as a walk in the park, while its compact, foldable design makes packing a breeze. Whether you're camping with family or hiking solo, this reliable, portable stove is an essential addition to your gear. With its sturdy construction and safety-focused design, the CompactCook Camping Stove is a step above the rest, providing durability, quality, and peace of mind. Be wild, be free, be cooked for with the CompactCook Camping Stove!"
```


This CSV file contains product information that the search index stores and retrieves to ground the chat responses.

## Create a search index

You use the search index to store vectorized data from the embeddings model. The search index retrieves relevant documents based on the user's question.

Create the file

**create_search_index.py**in your main folder (that is, the same directory where you placed your**assets**folder, not inside the**assets**folder).Copy and paste the following code into your

**create_search_index.py**file.Add the code to import the required libraries, create a project client, and configure some settings:

`import os from azure.ai.projects import AIProjectClient from azure.ai.projects.models import ConnectionType from azure.identity import DefaultAzureCredential from azure.core.credentials import AzureKeyCredential from azure.search.documents import SearchClient from azure.search.documents.indexes import SearchIndexClient from config import get_logger # initialize logging object logger = get_logger(__name__) # create a project client using environment variables loaded from the .env file project = AIProjectClient.from_connection_string( conn_str=os.environ["AIPROJECT_CONNECTION_STRING"], credential=DefaultAzureCredential() ) # create a vector embeddings client that will be used to generate vector embeddings embeddings = project.inference.get_embeddings_client() # use the project client to get the default search connection search_connection = project.connections.get_default( connection_type=ConnectionType.AZURE_AI_SEARCH, include_credentials=True ) # Create a search index client using the search connection # This client will be used to create and delete search indexes index_client = SearchIndexClient( endpoint=search_connection.endpoint_url, credential=AzureKeyCredential(key=search_connection.key) )`

The imports include

`AIProjectClient`

to connect to your project,`SearchClient`

to manage the search index, and`EmbeddingsModel`

to vectorize documents.References:

[AIProjectClient](/en-us/python/api/azure-ai-projects/azure.ai.projects.AIProjectClient),[SearchClient](/en-us/python/api/azure-search-documents/azure.search.documents.SearchClient),[azure-ai-projects](https://pypi.org/project/azure-ai-projects/).Now add the function to define a search index:

`import pandas as pd from azure.search.documents.indexes.models import ( SemanticSearch, SearchField, SimpleField, SearchableField, SearchFieldDataType, SemanticConfiguration, SemanticPrioritizedFields, SemanticField, VectorSearch, HnswAlgorithmConfiguration, VectorSearchAlgorithmKind, HnswParameters, VectorSearchAlgorithmMetric, ExhaustiveKnnAlgorithmConfiguration, ExhaustiveKnnParameters, VectorSearchProfile, SearchIndex, ) def create_index_definition(index_name: str, model: str) -> SearchIndex: dimensions = 1536 # text-embedding-ada-002 if model == "text-embedding-3-large": dimensions = 3072 # The fields we want to index. The "embedding" field is a vector field that will # be used for vector search. fields = [ SimpleField(name="id", type=SearchFieldDataType.String, key=True), SearchableField(name="content", type=SearchFieldDataType.String), SimpleField(name="filepath", type=SearchFieldDataType.String), SearchableField(name="title", type=SearchFieldDataType.String), SimpleField(name="url", type=SearchFieldDataType.String), SearchField( name="contentVector", type=SearchFieldDataType.Collection(SearchFieldDataType.Single), searchable=True, # Size of the vector created by the text-embedding-ada-002 model. vector_search_dimensions=dimensions, vector_search_profile_name="myHnswProfile", ), ] # The "content" field should be prioritized for semantic ranking. semantic_config = SemanticConfiguration( name="default", prioritized_fields=SemanticPrioritizedFields( title_field=SemanticField(field_name="title"), keywords_fields=[], content_fields=[SemanticField(field_name="content")], ), ) # For vector search, we want to use the HNSW (Hierarchical Navigable Small World) # algorithm (a type of approximate nearest neighbor search algorithm) with cosine # distance. vector_search = VectorSearch( algorithms=[ HnswAlgorithmConfiguration( name="myHnsw", kind=VectorSearchAlgorithmKind.HNSW, parameters=HnswParameters( m=4, ef_construction=1000, ef_search=1000, metric=VectorSearchAlgorithmMetric.COSINE, ), ), ExhaustiveKnnAlgorithmConfiguration( name="myExhaustiveKnn", kind=VectorSearchAlgorithmKind.EXHAUSTIVE_KNN, parameters=ExhaustiveKnnParameters(metric=VectorSearchAlgorithmMetric.COSINE), ), ], profiles=[ VectorSearchProfile( name="myHnswProfile", algorithm_configuration_name="myHnsw", ), VectorSearchProfile( name="myExhaustiveKnnProfile", algorithm_configuration_name="myExhaustiveKnn", ), ], ) # Create the semantic settings with the configuration semantic_search = SemanticSearch(configurations=[semantic_config]) # Create the search index definition return SearchIndex( name=index_name, fields=fields, semantic_search=semantic_search, vector_search=vector_search, )`

References:

[SearchIndex](/en-us/python/api/azure-search-documents/azure.search.documents.indexes.models.SearchIndex),[SearchIndexClient](/en-us/python/api/azure-search-documents/azure.search.documents.indexes.SearchIndexClient).Create the function to add a CSV file to the index:

`# define a function for indexing a csv file, that adds each row as a document # and generates vector embeddings for the specified content_column def create_docs_from_csv(path: str, content_column: str, model: str) -> list[dict[str, any]]: products = pd.read_csv(path) items = [] for product in products.to_dict("records"): content = product[content_column] id = str(product["id"]) title = product["name"] url = f"/products/{title.lower().replace(' ', '-')}" emb = embeddings.embed(input=content, model=model) rec = { "id": id, "content": content, "filepath": f"{title.lower().replace(' ', '-')}", "title": title, "url": url, "contentVector": emb.data[0].embedding, } items.append(rec) return items def create_index_from_csv(index_name, csv_file): # If a search index already exists, delete it: try: index_definition = index_client.get_index(index_name) index_client.delete_index(index_name) logger.info(f"🗑️ Found existing index named '{index_name}', and deleted it") except Exception: pass # create an empty search index index_definition = create_index_definition(index_name, model=os.environ["EMBEDDINGS_MODEL"]) index_client.create_index(index_definition) # create documents from the products.csv file, generating vector embeddings for the "description" column docs = create_docs_from_csv(path=csv_file, content_column="description", model=os.environ["EMBEDDINGS_MODEL"]) # Add the documents to the index using the Azure AI Search client search_client = SearchClient( endpoint=search_connection.endpoint_url, index_name=index_name, credential=AzureKeyCredential(key=search_connection.key), ) search_client.upload_documents(docs) logger.info(f"➕ Uploaded {len(docs)} documents to '{index_name}' index")`

References:

[azure-ai-projects](https://pypi.org/project/azure-ai-projects/),[SearchClient.upload_documents](/en-us/python/api/azure-search-documents/azure.search.documents.SearchClient).Finally, run the functions to build the index and register it to the cloud project:

`if __name__ == "__main__": import argparse parser = argparse.ArgumentParser() parser.add_argument( "--index-name", type=str, help="index name to use when creating the AI Search index", default=os.environ["AISEARCH_INDEX_NAME"], ) parser.add_argument( "--csv-file", type=str, help="path to data for creating search index", default="assets/products.csv" ) args = parser.parse_args() index_name = args.index_name csv_file = args.csv_file create_index_from_csv(index_name, csv_file)`

References:

[AIProjectClient.agents](/en-us/python/api/azure-ai-projects/azure.ai.projects.AIProjectClient),[SearchIndexClient.create_or_update_index](/en-us/python/api/azure-search-documents/azure.search.documents.indexes.SearchIndexClient).From your console, sign in to your Azure account and follow instructions for authenticating your account:

`az login`

Run the code to build your index locally and register it to the cloud project:

`python create_search_index.py`

Successful completion displays:

`➕ Uploaded 20 documents to 'example-index' index`

.

## Get product documents

Next, create a script to query the search index and retrieve product documents that match user questions. When the chat app receives a query, it searches for relevant documents to ground the response in your data.

### Create script to get product documents

Create the

**get_product_documents.py**file in your main directory. Copy and paste the following code into the file.Start with code to import the required libraries, create a project client, and configure settings:

`import os from pathlib import Path from opentelemetry import trace from azure.ai.projects import AIProjectClient from azure.ai.projects.models import ConnectionType from azure.identity import DefaultAzureCredential from azure.core.credentials import AzureKeyCredential from azure.search.documents import SearchClient from config import ASSET_PATH, get_logger # initialize logging and tracing objects logger = get_logger(__name__) tracer = trace.get_tracer(__name__) # create a project client using environment variables loaded from the .env file project = AIProjectClient.from_connection_string( conn_str=os.environ["AIPROJECT_CONNECTION_STRING"], credential=DefaultAzureCredential() ) # create a vector embeddings client that will be used to generate vector embeddings chat = project.inference.get_chat_completions_client() embeddings = project.inference.get_embeddings_client() # use the project client to get the default search connection search_connection = project.connections.get_default( connection_type=ConnectionType.AZURE_AI_SEARCH, include_credentials=True ) # Create a search index client using the search connection # This client will be used to create and delete search indexes search_client = SearchClient( index_name=os.environ["AISEARCH_INDEX_NAME"], endpoint=search_connection.endpoint_url, credential=AzureKeyCredential(key=search_connection.key), )`

Key imports:

`SearchClient`

(to query the search index) and`PromptTemplate`

(to construct search queries from user intent).References:

[AIProjectClient](/en-us/python/api/azure-ai-projects/azure.ai.projects.AIProjectClient),[SearchClient](/en-us/python/api/azure-search-documents/azure.search.documents.SearchClient),[promptflow](https://pypi.org/project/promptflow/).Add the function to get product documents:

`from azure.ai.inference.prompts import PromptTemplate from azure.search.documents.models import VectorizedQuery @tracer.start_as_current_span(name="get_product_documents") def get_product_documents(messages: list, context: dict = None) -> dict: if context is None: context = {} overrides = context.get("overrides", {}) top = overrides.get("top", 5) # generate a search query from the chat messages intent_prompty = PromptTemplate.from_prompty(Path(ASSET_PATH) / "intent_mapping.prompty") intent_mapping_response = chat.complete( model=os.environ["INTENT_MAPPING_MODEL"], messages=intent_prompty.create_messages(conversation=messages), **intent_prompty.parameters, ) search_query = intent_mapping_response.choices[0].message.content logger.debug(f"🧠 Intent mapping: {search_query}") # generate a vector representation of the search query embedding = embeddings.embed(model=os.environ["EMBEDDINGS_MODEL"], input=search_query) search_vector = embedding.data[0].embedding # search the index for products matching the search query vector_query = VectorizedQuery(vector=search_vector, k_nearest_neighbors=top, fields="contentVector") search_results = search_client.search( search_text=search_query, vector_queries=[vector_query], select=["id", "content", "filepath", "title", "url"] ) documents = [ { "id": result["id"], "content": result["content"], "filepath": result["filepath"], "title": result["title"], "url": result["url"], } for result in search_results ] # add results to the provided context if "thoughts" not in context: context["thoughts"] = [] # add thoughts and documents to the context object so it can be returned to the caller context["thoughts"].append( { "title": "Generated search query", "description": search_query, } ) if "grounding_data" not in context: context["grounding_data"] = [] context["grounding_data"].append(documents) logger.debug(f"📄 {len(documents)} documents retrieved: {documents}") return documents`

References:

[SearchClient.search](/en-us/python/api/azure-search-documents/azure.search.documents.SearchClient),[AIProjectClient.inference](/en-us/python/api/azure-ai-projects/azure.ai.projects.AIProjectClient).Finally, add code to test the function when you run the script directly:

`if __name__ == "__main__": import logging import argparse # set logging level to debug when running this module directly logger.setLevel(logging.DEBUG) # load command line arguments parser = argparse.ArgumentParser() parser.add_argument( "--query", type=str, help="Query to use to search product", default="I need a new tent for 4 people, what would you recommend?", ) args = parser.parse_args() query = args.query result = get_product_documents(messages=[{"role": "user", "content": query}])`

References:

[AIProjectClient.from_config](/en-us/python/api/azure-ai-projects/azure.ai.projects.AIProjectClient),[argparse](https://docs.python.org/3/library/argparse.html).

### Create prompt template for intent mapping

The **get_product_documents.py** script uses a prompt template named **intent_mapping.prompty** to transform the user's question into an optimized search query. This transformation helps the search index find the most relevant product documents.

Before running the script, create the prompt template. Add the file **intent_mapping.prompty** to your **assets** folder:

```
---
name: Chat Prompt
description: A prompty that extract users query intent based on the current_query and chat_history of the conversation
model:
api: chat
configuration:
azure_deployment: gpt-4o
inputs:
conversation:
type: array
---
system:
# Instructions
- You are an AI assistant reading a current user query and chat_history.
- Given the chat_history, and current user's query, infer the user's intent expressed in the current user query.
- Once you infer the intent, respond with a search query that can be used to retrieve relevant documents for the current user's query based on the intent
- Be specific in what the user is asking about, but disregard parts of the chat history that are not relevant to the user's intent.
- Provide responses in json format
# Examples
Example 1:
With a conversation like below:
```
- user: are the trailwalker shoes waterproof?
- assistant: Yes, the TrailWalker Hiking Shoes are waterproof. They are designed with a durable and waterproof construction to withstand various terrains and weather conditions.
- user: how much do they cost?
```
Respond with:
{
"intent": "The user wants to know how much the Trailwalker Hiking Shoes cost.",
"search_query": "price of Trailwalker Hiking Shoes"
}
Example 2:
With a conversation like below:
```
- user: are the trailwalker shoes waterproof?
- assistant: Yes, the TrailWalker Hiking Shoes are waterproof. They are designed with a durable and waterproof construction to withstand various terrains and weather conditions.
- user: how much do they cost?
- assistant: The TrailWalker Hiking Shoes are priced at $110.
- user: do you have waterproof tents?
- assistant: Yes, we have waterproof tents available. Can you please provide more information about the type or size of tent you are looking for?
- user: which is your most waterproof tent?
- assistant: Our most waterproof tent is the Alpine Explorer Tent. It is designed with a waterproof material and has a rainfly with a waterproof rating of 3000mm. This tent provides reliable protection against rain and moisture.
- user: how much does it cost?
```
Respond with:
{
"intent": "The user would like to know how much the Alpine Explorer Tent costs.",
"search_query": "price of Alpine Explorer Tent"
}
user:
Return the search query for the messages in the following conversation:
{{#conversation}}
- {{role}}: {{content}}
{{/conversation}}
```


This template instructs the model to extract the user's intent and convert it into a concise search query.

### Test the product document retrieval script

Now that you have both the script and template, run the script to test what documents the search index returns from a query. In a terminal window, run:

```
python get_product_documents.py --query "I need a new tent for 4 people, what would you recommend?"
```


The script returns a list of product documents from your search index that match the query. You should see JSON output showing product names, descriptions, and prices relevant to a 4-person tent.

## Develop custom knowledge retrieval (RAG) code

Next, you create custom code to add retrieval augmented generation (RAG) capabilities to a basic chat application.

### Create a chat script with RAG capabilities

In your main folder, create a new file named

**chat_with_products.py**. This script retrieves product documents and generates a response to a user's question.Add the code to import the required libraries, create a project client, and configure settings:

`import os from pathlib import Path from opentelemetry import trace from azure.ai.projects import AIProjectClient from azure.identity import DefaultAzureCredential from config import ASSET_PATH, get_logger, enable_telemetry from get_product_documents import get_product_documents # initialize logging and tracing objects logger = get_logger(__name__) tracer = trace.get_tracer(__name__) # create a project client using environment variables loaded from the .env file project = AIProjectClient.from_connection_string( conn_str=os.environ["AIPROJECT_CONNECTION_STRING"], credential=DefaultAzureCredential() ) # create a chat client we can use for testing chat = project.inference.get_chat_completions_client()`

Key imports:

`AIProjectClient`

(connects to your project),`chat`

function (from prompt flow), and`get_product_documents`

(your retrieval function).References:

[AIProjectClient](/en-us/python/api/azure-ai-projects/azure.ai.projects.AIProjectClient),[promptflow](https://pypi.org/project/promptflow/).Create the chat function that uses the RAG capabilities:

`from azure.ai.inference.prompts import PromptTemplate @tracer.start_as_current_span(name="chat_with_products") def chat_with_products(messages: list, context: dict = None) -> dict: if context is None: context = {} documents = get_product_documents(messages, context) # do a grounded chat call using the search results grounded_chat_prompt = PromptTemplate.from_prompty(Path(ASSET_PATH) / "grounded_chat.prompty") system_message = grounded_chat_prompt.create_messages(documents=documents, context=context) response = chat.complete( model=os.environ["CHAT_MODEL"], messages=system_message + messages, **grounded_chat_prompt.parameters, ) logger.info(f"💬 Response: {response.choices[0].message}") # Return a chat protocol compliant response return {"message": response.choices[0].message, "context": context}`

References:

[azure-ai-projects](https://pypi.org/project/azure-ai-projects/),[AIProjectClient.inference](/en-us/python/api/azure-ai-projects/azure.ai.projects.AIProjectClient).Finally, add the code to run the chat function:

`if __name__ == "__main__": import argparse # load command line arguments parser = argparse.ArgumentParser() parser.add_argument( "--query", type=str, help="Query to use to search product", default="I need a new tent for 4 people, what would you recommend?", ) parser.add_argument( "--enable-telemetry", action="store_true", help="Enable sending telemetry back to the project", ) args = parser.parse_args() if args.enable_telemetry: enable_telemetry(True) # run chat with products response = chat_with_products(messages=[{"role": "user", "content": args.query}])`

References:

[argparse](https://docs.python.org/3/library/argparse.html),[AIProjectClient.from_config](/en-us/python/api/azure-ai-projects/azure.ai.projects.AIProjectClient).

### Create a grounded chat prompt template

The **chat_with_products.py** script calls a prompt template named **grounded_chat.prompty** to generate responses. This template instructs the model to use the retrieved product documents to ground answers and stay on-topic for your retail business.

In your **assets** folder, add the file **grounded_chat.prompty**:

```
---
name: Chat with documents
description: Uses a chat completions model to respond to queries grounded in relevant documents
model:
api: chat
configuration:
azure_deployment: gpt-4o
inputs:
conversation:
type: array
---
system:
You are an AI assistant helping users with queries related to outdoor outdooor/camping gear and clothing.
If the question is not related to outdoor/camping gear and clothing, just say 'Sorry, I only can answer queries related to outdoor/camping gear and clothing. So, how can I help?'
Don't try to make up any answers.
If the question is related to outdoor/camping gear and clothing but vague, ask for clarifying questions instead of referencing documents. If the question is general, for example it uses "it" or "they", ask the user to specify what product they are asking about.
Use the following pieces of context to answer the questions about outdoor/camping gear and clothing as completely, correctly, and concisely as possible.
Do not add documentation reference in the response.
# Documents
{{#documents}}
## Document {{id}}: {{title}}
{{content}}
{{/documents}}
```


This template ensures responses are based on your product data rather than general knowledge.

### Run the chat script with RAG capabilities

Now that you have both the script and the template, run the script to test your chat app with RAG capabilities:

```
python chat_with_products.py --query "I need a new tent for 4 people, what would you recommend?"
```


The script returns a conversational response grounded in your product data. The response references specific products from your search index rather than generic advice.

### Add telemetry logging

To enable logging of telemetry to your project so you can track and monitor chat interactions:

Register the

**Microsoft.OperationalInsights**and**microsoft.insights**resource providers in your subscription. For more information, see[Register resource provider](/en-us/azure/azure-resource-manager/management/resource-providers-and-types#register-resource-provider-1).Add an Application Insights resource to your project. Navigate to the

**Tracing**tab in the[Foundry portal](https://ai.azure.com/?cid=learnDocs), and create a new resource if you don't already have one.Install the telemetry SDK:

`pip install azure-monitor-opentelemetry`

References:

[azure-monitor-opentelemetry](https://pypi.org/project/azure-monitor-opentelemetry/),[OpenTelemetry](/en-us/python/api/azure-monitor-opentelemetry).Add the

`--enable-telemetry`

flag when you use the`chat_with_products.py`

script:`python chat_with_products.py --query "I need a new tent for 4 people, what would you recommend?" --enable-telemetry`


Follow the link in the console output to see the telemetry data in your Application Insights resource. If it doesn't appear right away, wait a few minutes and select **Refresh** in the toolbar.

## Clean up resources

To avoid incurring unnecessary Azure costs, delete the resources you created in this tutorial if they're no longer needed. To manage resources, you can use the [Azure portal](https://portal.azure.com?azure-portal=true).

Don't delete the resources if you want to deploy your chat app to Azure in [the next part of this tutorial series](copilot-sdk-evaluate?view=foundry-classic).
