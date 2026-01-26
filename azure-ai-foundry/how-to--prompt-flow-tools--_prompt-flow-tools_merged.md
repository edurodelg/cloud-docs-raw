---
merged_at: 2026-01-26T23:20:36.864169
merged_files: 4
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/prompt-flow-tools/embedding-tool -->

# Embedding tool for flows in Microsoft Foundry portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

The prompt flow Embedding tool enables you to convert text into dense vector representations for various natural language processing tasks.

Tip

For chat and completion tools, learn more about the large language model [(LLM) tool](llm-tool?view=foundry-classic).

## Prerequisites

Important

This article provides legacy support for hub-based projects. It will not work for **Foundry projects**. See [How do I know which type of project I have?](../../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have)

**SDK compatibility note**: Code examples require a specific Microsoft Foundry SDK version. If you encounter compatibility issues, consider [migrating from a hub-based to a Foundry project](../migrate-project?view=foundry-classic).

- An Azure account with an active subscription. If you don't have one, create a
[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - If you don't have one,
[create a hub-based project](../hub-create-projects?view=foundry-classic).

## Build with the Embedding tool

Create or open a flow in

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). For more information, see[Create a flow](../flow-develop?view=foundry-classic).Select

**+ More tools**>**Embedding**to add the Embedding tool to your flow.Select the connection to one of your provisioned resources. For example, select

**Default_AzureOpenAI**.Enter values for the Embedding tool input parameters described in the

[Inputs table](#inputs).Add more tools to your flow, as needed. Or select

**Run**to run the flow.The outputs are described in the

[Outputs table](#outputs).

## Inputs

The following input parameters are available.

| Name | Type | Description | Required |
|---|---|---|---|
| input | string | The input text to embed. | Yes |
| model, deployment_name | string | The instance of the text-embedding engine to use. | Yes |

## Outputs

The output is a list of vector representations for the input text. For example:

```
[
0.123,
0.456,
0.789
]
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/prompt-flow-tools/prompt-tool -->

# Prompt tool for flows in Microsoft Foundry portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

The prompt flow Prompt tool offers a collection of textual templates that serve as a starting point for creating prompts. These templates, based on the [Jinja](https://jinja.palletsprojects.com/en/stable/) template engine, facilitate the definition of prompts. The tool proves useful when prompt tuning is required before the prompts are fed into the large language model (LLM) in the prompt flow.

## Prerequisites

Important

This article provides legacy support for hub-based projects. It will not work for **Foundry projects**. See [How do I know which type of project I have?](../../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have)

**SDK compatibility note**: Code examples require a specific Microsoft Foundry SDK version. If you encounter compatibility issues, consider [migrating from a hub-based to a Foundry project](../migrate-project?view=foundry-classic).

- An Azure account with an active subscription. If you don't have one, create a
[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - If you don't have one,
[create a hub-based project](../hub-create-projects?view=foundry-classic).

Prepare a prompt. The [LLM tool](llm-tool?view=foundry-classic) and Prompt tool both support [Jinja](https://jinja.palletsprojects.com/en/stable/) templates.

In this example, the prompt incorporates Jinja templating syntax to dynamically generate the welcome message and personalize it based on the user's name. It also presents a menu of options for the user to choose from. Depending on whether the `user_name`

variable is provided, it either addresses the user by name or uses a generic greeting.

```
Welcome to {{ website_name }}!
{% if user_name %}
Hello, {{ user_name }}!
{% else %}
Hello there!
{% endif %}
Please select an option from the menu below:
1. View your account
2. Update personal information
3. Browse available products
4. Contact customer support
```


For more information and best practices, see [Prompt engineering techniques](../../openai/concepts/advanced-prompt-engineering?view=foundry-classic).

## Build with the Prompt tool

Create or open a flow in

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). For more information, see[Create a flow](../flow-develop?view=foundry-classic).Select

**+ Prompt**to add the Prompt tool to your flow.Enter values for the Prompt tool input parameters described in the

[Inputs table](#inputs). For information about how to prepare the prompt input, see[Prerequisites](#prerequisites).Add more tools (such as the

[LLM tool](llm-tool?view=foundry-classic)) to your flow, as needed. Or select**Run**to run the flow.The outputs are described in the

[Outputs table](#outputs).

## Inputs

The following input parameters are available.

| Name | Type | Description | Required |
|---|---|---|---|
| prompt | string | The prompt template in Jinja. | Yes |
| Inputs | - | The list of variables of a prompt template and its assignments. | - |

## Outputs

### Example 1

Inputs:

| Variable | Type | Sample value |
|---|---|---|
| website_name | string | "Microsoft" |
| user_name | string | "Jane" |

Outputs:

```
Welcome to Microsoft! Hello, Jane! Please select an option from the menu below: 1. View your account 2. Update personal information 3. Browse available products 4. Contact customer support
```


### Example 2

Inputs:

| Variable | Type | Sample value |
|---|---|---|
| website_name | string | "Bing" |
| user_name | string | " |

Outputs:

```
Welcome to Bing! Hello there! Please select an option from the menu below: 1. View your account 2. Update personal information 3. Browse available products 4. Contact customer support
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/prompt-flow-tools/llm-tool -->

# LLM tool for flows in Microsoft Foundry portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

To use large language models (LLMs) for natural language processing, you use the prompt flow LLM tool.

Tip

For embeddings to convert text into dense vector representations for various natural language processing tasks, see [Embedding tool](embedding-tool?view=foundry-classic).

## Prerequisites

Important

This article provides legacy support for hub-based projects. It will not work for **Foundry projects**. See [How do I know which type of project I have?](../../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have)

**SDK compatibility note**: Code examples require a specific Microsoft Foundry SDK version. If you encounter compatibility issues, consider [migrating from a hub-based to a Foundry project](../migrate-project?view=foundry-classic).

- An Azure account with an active subscription. If you don't have one, create a
[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - If you don't have one,
[create a hub-based project](../hub-create-projects?view=foundry-classic).

Prepare a prompt as described in the [Prompt tool](prompt-tool?view=foundry-classic#prerequisites) documentation. The LLM tool and Prompt tool both support [Jinja](https://jinja.palletsprojects.com/en/stable/) templates. For more information and best practices, see [Prompt engineering techniques](../../openai/concepts/advanced-prompt-engineering?view=foundry-classic).

## Build with the LLM tool

Create or open a flow in

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). For more information, see[Create a flow](../flow-develop?view=foundry-classic).Select

**+ LLM**to add the LLM tool to your flow.Select the connection to one of your provisioned resources. For example, select

**Default_AzureOpenAI**.From the

**Api**dropdown list, select**chat**or**completion**.Enter values for the LLM tool input parameters described in the

[Text completion inputs table](#inputs). If you selected the**chat**API, see the[Chat inputs table](#chat-inputs). If you selected the**completion**API, see the[Text completion inputs table](#text-completion-inputs). For information about how to prepare the prompt input, see[Prerequisites](#prerequisites).Add more tools to your flow, as needed. Or select

**Run**to run the flow.The outputs are described in the

[Outputs table](#outputs).

## Inputs

The following input parameters are available.

### Text completion inputs

| Name | Type | Description | Required |
|---|---|---|---|
| prompt | string | Text prompt for the language model. | Yes |
| model, deployment_name | string | The language model to use. | Yes |
| max_tokens | integer | The maximum number of tokens to generate in the completion. Default is 16. | No |
| temperature | float | The randomness of the generated text. Default is 1. | No |
| stop | list | The stopping sequence for the generated text. Default is null. | No |
| suffix | string | The text appended to the end of the completion. | No |
| top_p | float | The probability of using the top choice from the generated tokens. Default is 1. | No |
| logprobs | integer | The number of log probabilities to generate. Default is null. | No |
| echo | boolean | The value that indicates whether to echo back the prompt in the response. Default is false. | No |
| presence_penalty | float | The value that controls the model's behavior regarding repeating phrases. Default is 0. | No |
| frequency_penalty | float | The value that controls the model's behavior regarding generating rare phrases. Default is 0. | No |
| best_of | integer | The number of best completions to generate. Default is 1. | No |
| logit_bias | dictionary | The logit bias for the language model. Default is empty dictionary. | No |

### Chat inputs

| Name | Type | Description | Required |
|---|---|---|---|
| prompt | string | The text prompt that the language model should reply to. | Yes |
| model, deployment_name | string | The language model to use. | Yes |
| max_tokens | integer | The maximum number of tokens to generate in the response. Default is inf. | No |
| temperature | float | The randomness of the generated text. Default is 1. | No |
| stop | list | The stopping sequence for the generated text. Default is null. | No |
| top_p | float | The probability of using the top choice from the generated tokens. Default is 1. | No |
| presence_penalty | float | The value that controls the model's behavior regarding repeating phrases. Default is 0. | No |
| frequency_penalty | float | The value that controls the model's behavior regarding generating rare phrases. Default is 0. | No |
| logit_bias | dictionary | The logit bias for the language model. Default is empty dictionary. | No |

## Outputs

The output varies depending on the API you selected for inputs.

| API | Return type | Description |
|---|---|---|
| Completion | string | The text of one predicted completion. |
| Chat | string | The text of one response of conversation. |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/prompt-flow-tools/python-tool -->

# Python tool for flows in Microsoft Foundry portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

The prompt flow Python tool offers customized code snippets as self-contained executable nodes. You can quickly create Python tools, edit code, and verify results.

## Prerequisites

Important

This article provides legacy support for hub-based projects. It will not work for **Foundry projects**. See [How do I know which type of project I have?](../../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have)

**SDK compatibility note**: Code examples require a specific Microsoft Foundry SDK version. If you encounter compatibility issues, consider [migrating from a hub-based to a Foundry project](../migrate-project?view=foundry-classic).

- An Azure account with an active subscription. If you don't have one, create a
[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - If you don't have one,
[create a hub-based project](../hub-create-projects?view=foundry-classic).

## Build with the Python tool

Create or open a flow in

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). For more information, see[Create a flow](../flow-develop?view=foundry-classic).Select

**+ Python**to add the Python tool to your flow.Enter values for the Python tool input parameters that are described in the

[Inputs table](#inputs). For example, in the**Code**input text box, you can enter the following Python code:`from promptflow import tool @tool def my_python_tool(message: str) -> str: return 'hello ' + message`

For more information, see

[Python code input requirements](#python-code-input-requirements).Add more tools to your flow, as needed. Or select

**Run**to run the flow.The outputs are described in the

[Outputs table](#outputs). Based on the previous example Python code input, if the input message is "world," the output is`hello world`

.

## Inputs

The list of inputs change based on the arguments of the tool function, after you save the code. Adding type to arguments and `return`

values helps the tool show the types properly.

| Name | Type | Description | Required |
|---|---|---|---|
| Code | string | The Python code snippet. | Yes |
| Inputs | - | The list of the tool function parameters and its assignments. | - |

## Outputs

The output is the `return`

value of the Python tool function. For example, consider the following Python tool function:

```
from promptflow import tool
@tool
def my_python_tool(message: str) -> str:
return 'hello ' + message
```


If the input message is "world," the output is `hello world`

.

### Types

| Type | Python example | Description |
|---|---|---|
| int | param: int | Integer type |
| bool | param: bool | Boolean type |
| string | param: str | String type |
| double | param: float | Double type |
| list | param: list or param: List[T] | List type |
| object | param: dict or param: Dict[K, V] | Object type |
| Connection | param: CustomConnection | Connection type is handled specially. |

Parameters with `Connection`

type annotation are treated as connection inputs, which means:

- The prompt flow extension shows a selector to select the connection.
- During execution time, the prompt flow tries to find the connection with the same name from the parameter value that was passed in.

Note

The `Union[...]`

type annotation is only supported for connection type. An example is `param: Union[CustomConnection, OpenAIConnection]`

.

## Python code input requirements

This section describes requirements of the Python code input for the Python tool.

- Python tool code should consist of a complete Python code, including any necessary module imports.
- Python tool code must contain a function decorated with
`@tool`

(tool function), serving as the entry point for execution. The`@tool`

decorator should be applied only once within the snippet. - Python tool function parameters must be assigned in the
`Inputs`

section. - Python tool function shall have a return statement and value, which is the output of the tool.

The following Python code is an example of best practices:

```
from promptflow import tool
@tool
def my_python_tool(message: str) -> str:
return 'hello ' + message
```


## Consume a custom connection in the Python tool

If you're developing a Python tool that requires calling external services with authentication, you can use the custom connection in a prompt flow. It allows you to securely store the access key and then retrieve it in your Python code.

### Create a custom connection

Create a custom connection that stores all your large language model API key or other required credentials.

Important

This article provides legacy support for hub-based projects. It will not work for **Foundry projects**. See [How do I know which type of project I have?](../../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have)

**SDK compatibility note**: Code examples require a specific Microsoft Foundry SDK version. If you encounter compatibility issues, consider [migrating from a hub-based to a Foundry project](../migrate-project?view=foundry-classic).

- An Azure account with an active subscription. If you don't have one, create a
[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - If you don't have one,
[create a hub-based project](../hub-create-projects?view=foundry-classic).

Go to the

**Management center**page for your project.Under either the

**Hub**or**Project**heading, select**Connected resources**.Select

**+ New Connection**.Select

**Custom**service. You can define your connection name. You can add multiple key-value pairs to store your credentials and keys by selecting**Add key-value pairs**.Note

Make sure at least one key-value pair is set as secret. Otherwise, the connection won't be created successfully. To set one key-value pair as secret, select

**is secret**to encrypt and store your key value.

### Consume a custom connection in Python

To consume a custom connection in your Python code:

- In the code section in your Python node, import the custom connection library
`from promptflow.connections import CustomConnection`

. Define an input parameter of the type`CustomConnection`

in the tool function. - Parse the input to the input section. Then select your target custom connection in the value dropdown list.

For example:

```
from promptflow import tool
from promptflow.connections import CustomConnection
@tool
def my_python_tool(message: str, myconn: CustomConnection) -> str:
# Get authentication key-values from the custom connection
connection_key1_value = myconn.key1
connection_key2_value = myconn.key2
```
