---
merged_at: 2026-01-26T23:20:36.861756
merged_files: 5
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/how-to/how-to-chat-application-with-open-web-ui -->

# Integrate Open WebUI with Foundry Local

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

This article shows you how to create a chat application by using Foundry Local and Open WebUI. When you finish, you have a working chat interface that runs entirely on your local device.

## Prerequisites

Before you start, make sure you have the following prerequisites:

**Foundry Local**installed on your computer. For installation instructions, see[Get started with Foundry Local](../get-started?view=foundry-classic).**Open WebUI**installed. Follow the instructions in the[Open WebUI GitHub repository](https://github.com/open-webui/open-webui).**Azure RBAC**: Not applicable (runs locally).

## Start Foundry Local and verify the endpoint

**Start a model**(or confirm one is already running):`foundry model run qwen2.5-0.5b`

Keep this terminal open.

Reference:

[Foundry Local CLI reference](../reference/reference-cli?view=foundry-classic)**Find your local service endpoint**. In a second terminal, run:`foundry service status`

Copy the endpoint URL from the output. Foundry Local dynamically assigns a port each time the service starts.

Reference:

[Foundry Local CLI reference](../reference/reference-cli?view=foundry-classic)**Verify the REST server is reachable**. Run this command, replacing`PORT`

with your endpoint port:`curl http://localhost:PORT/openai/status`

A successful response is JSON that includes

`Endpoints`

,`ModelDirPath`

, and`PipeName`

.Reference:

[Foundry Local REST API reference](../reference/reference-rest?view=foundry-classic)

## Set up Open WebUI for chat

**Install Open WebUI**by following the instructions from the[Open WebUI GitHub repository](https://github.com/open-webui/open-webui).**Launch Open WebUI**by using this command in your terminal:`open-webui serve`

Reference:

[Open WebUI GitHub repository](https://github.com/open-webui/open-webui)Open your web browser and go to

[http://localhost:8080](http://localhost:8080).Enable Direct Connections:

- Select
**Settings**and**Admin Settings**in the profile menu. - Select
**Connections**in the navigation menu. - Enable
**Direct Connections**by turning on the toggle. This setting allows users to connect to their own OpenAI compatible API endpoints.

- Select
**Connect Open WebUI to Foundry Local**:- Select
**Settings**in the profile menu. - Select
**Connections**in the navigation menu. - Select
**+**by**Manage Direct Connections**. - For the
**URL**, enter`http://localhost:PORT/v1`

where`PORT`

is the port from`foundry service status`

(for example,`http://localhost:5272/v1`

). Foundry Local dynamically assigns a port, so it isn't always the same. - For the
**Auth**, select**None**. - Select
**Save**.

- Select
**Start chatting with your model**:- Confirm your loaded models appear in the dropdown at the top.
- Select a model from the list.
- Type your message in the input box at the bottom.


That's it! You're now chatting with an AI model running entirely on your local device.

## Troubleshooting

- If
`foundry service status`

reports an error, run`foundry service restart`

and try again. - If no models appear in Open WebUI, start a model with
`foundry model run <model>`

and then reload Open WebUI. - If Open WebUI doesn't connect, confirm you're using the current port from
`foundry service status`

.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/how-to/how-to-use-native-chat-completions -->

# Use Foundry Local native chat completions API

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

The native chat completions API enables you to run chat completions directly in-process, without starting a REST web server.

In this article, you create a console app that downloads a local model, generates a streaming chat response, and then unloads the model.

This article explains how to use the native chat completions API in the Foundry Local SDK.

## Prerequisites

[.NET 9.0 SDK](https://dotnet.microsoft.com/download/dotnet/9.0)or later installed.- Azure role-based access control (RBAC): Not applicable.

## Samples repository

You can find the sample in this article in the [Foundry Local C# SDK Samples GitHub repository](https://aka.ms/foundrylocalSDK).

## Set up project

Use Foundry Local in your C# project by following these Windows-specific or Cross-Platform (macOS/Linux/Windows) instructions:

- Create a new C# project and navigate into it:
`dotnet new console -n app-name cd app-name`

- Open and edit the
`app-name.csproj`

file to:`<Project Sdk="Microsoft.NET.Sdk"> <PropertyGroup> <OutputType>Exe</OutputType> <TargetFramework>net9.0-windows10.0.26100</TargetFramework> <RootNamespace>app-name</RootNamespace> <ImplicitUsings>enable</ImplicitUsings> <Nullable>enable</Nullable> <WindowsAppSDKSelfContained>false</WindowsAppSDKSelfContained> <WindowsPackageType>None</WindowsPackageType> <EnableCoreMrtTooling>false</EnableCoreMrtTooling> </PropertyGroup> <ItemGroup> <PackageReference Include="Microsoft.AI.Foundry.Local.WinML" Version="0.8.2.1" /> <PackageReference Include="Microsoft.Extensions.Logging" Version="9.0.10" /> <PackageReference Include="OpenAI" Version="2.5.0" /> </ItemGroup> </Project>`

- Create a
`nuget.config`

file in the project root with the following content so that the packages restore correctly:`<?xml version="1.0" encoding="utf-8"?> <configuration> <packageSources> <clear /> <add key="nuget.org" value="https://api.nuget.org/v3/index.json" /> <add key="ORT" value="https://aiinfra.pkgs.visualstudio.com/PublicPackages/_packaging/ORT/nuget/v3/index.json" /> </packageSources> <packageSourceMapping> <packageSource key="nuget.org"> <package pattern="*" /> </packageSource> <packageSource key="ORT"> <package pattern="*Foundry*" /> </packageSource> </packageSourceMapping> </configuration>`


## Use native chat completions API

The following example demonstrates how to use the native chat completions API in Foundry Local. The code includes the following steps:

Initializes a

`FoundryLocalManager`

instance with a`Configuration`

.Gets a

`Model`

object from the model catalog using an alias.Note

Foundry Local automatically selects the best variant for the model based on the available hardware of the host machine.

Downloads and loads the model variant.

Uses the native chat completions API to generate a response.

Unloads the model.


Copy and paste the following code into a C# file named `Program.cs`

:

```
using Microsoft.AI.Foundry.Local;
using Betalgo.Ranul.OpenAI.ObjectModels.RequestModels;
using Microsoft.Extensions.Logging;
CancellationToken ct = CancellationToken.None;
var config = new Configuration
{
AppName = "app-name",
LogLevel = Microsoft.AI.Foundry.Local.LogLevel.Information
};
using var loggerFactory = LoggerFactory.Create(builder =>
{
builder.SetMinimumLevel(Microsoft.Extensions.Logging.LogLevel.Information);
});
var logger = loggerFactory.CreateLogger<Program>();
// Initialize the singleton instance.
await FoundryLocalManager.CreateAsync(config, logger);
var mgr = FoundryLocalManager.Instance;
// Get the model catalog
var catalog = await mgr.GetCatalogAsync();
// Get a model using an alias
var model = await catalog.GetModelAsync("qwen2.5-0.5b") ?? throw new Exception("Model not found");
// Download the model (the method skips download if already cached)
await model.DownloadAsync(progress =>
{
Console.Write($"\rDownloading model: {progress:F2}%");
if (progress >= 100f)
{
Console.WriteLine();
}
});
// Load the model
await model.LoadAsync();
// Get a chat client
var chatClient = await model.GetChatClientAsync();
// Create a chat message
List<ChatMessage> messages = new()
{
new ChatMessage { Role = "user", Content = "Why is the sky blue?" }
};
var streamingResponse = chatClient.CompleteChatStreamingAsync(messages, ct);
await foreach (var chunk in streamingResponse)
{
Console.Write(chunk.Choices[0].Message.Content);
Console.Out.Flush();
}
Console.WriteLine();
// Tidy up - unload the model
await model.UnloadAsync();
```


References:

### Optional: list model aliases available on your device

If you don't know which model alias to use, list the models available for your hardware.

```
// List available models and aliases
Console.WriteLine("Available models for your hardware:");
var models = await catalog.ListModelsAsync();
foreach (var availableModel in models)
{
foreach (var variant in availableModel.Variants)
{
Console.WriteLine($" - Alias: {variant.Alias}");
}
}
```


References:

Run the code by using the following command:

For x64 Windows, use the following command:

```
dotnet run -r:win-x64
```


For arm64 Windows, use the following command:

```
dotnet run -r:win-arm64
```


## Troubleshooting

**Build errors referencing**: Install the`net9.0`

[.NET 9.0 SDK](https://dotnet.microsoft.com/download/dotnet/9.0), then rebuild the app.: Run the optional model listing snippet to find an alias available on your device, then update the alias passed to`Model not found`

`GetModelAsync`

.**Slow first run**: Model downloads can take time the first time you run the app.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/how-to/how-to-use-langchain-with-foundry-local -->

# Build a translation app with LangChain

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

This article shows you how to build a translation app by using the Foundry Local SDK and [LangChain](https://www.langchain.com/langchain). Use a local model to translate text between languages.

## Prerequisites

Before starting this tutorial, you need:

**Foundry Local**installed on your computer. Read the[Get started with Foundry Local](../get-started?view=foundry-classic)guide for installation instructions.**Python 3.10 or later**installed on your computer. You can download Python from the[official website](https://www.python.org/downloads/).

## Install Python packages

You need to install the following Python packages:

```
pip install langchain[openai]
pip install foundry-local-sdk
```


Tip

We recommend using a virtual environment to avoid package conflicts. You can create a virtual environment using either `venv`

or `conda`

.

## Create a translation application

Create a new Python file named `translation_app.py`

in your favorite IDE and add the following code:

```
import os
from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from foundry_local import FoundryLocalManager
# By using an alias, the most suitable model will be downloaded
# to your end-user's device.
# TIP: You can find a list of available models by running the
# following command: `foundry model list`.
alias = "qwen2.5-0.5b"
# Create a FoundryLocalManager instance. This will start the Foundry
# Local service if it is not already running and load the specified model.
manager = FoundryLocalManager(alias)
# Configure ChatOpenAI to use your locally-running model
llm = ChatOpenAI(
model=manager.get_model_info(alias).id,
base_url=manager.endpoint,
api_key=manager.api_key,
temperature=0.6,
streaming=False
)
# Create a translation prompt template
prompt = ChatPromptTemplate.from_messages([
(
"system",
"You are a helpful assistant that translates {input_language} to {output_language}."
),
("human", "{input}")
])
# Build a simple chain by connecting the prompt to the language model
chain = prompt | llm
input = "I love to code."
print(f"Translating '{input}' to French...")
# Run the chain with your inputs
ai_msg = chain.invoke({
"input_language": "English",
"output_language": "French",
"input": input
})
# print the result content
print(f"Response: {ai_msg.content}")
```


#### References

- Reference:
[Foundry Local SDK reference](../reference/reference-sdk?view=foundry-classic) - Reference:
[Get started with Foundry Local](../get-started?view=foundry-classic)

Note

One of key benefits of Foundry Local is that it **automatically** selects the most suitable model **variant** for the user's hardware. For example, if the user has a GPU, it downloads the GPU version of the model. If the user has an NPU (Neural Processing Unit), it downloads the NPU version. If the user doesn't have either a GPU or NPU, it downloads the CPU version of the model.

## Run the application

To run the application, open a terminal and navigate to the directory where you saved the `translation_app.py`

file. Then, run the following command:

```
python translation_app.py
```


You're done when you see a `Response:`

line with the translated text.

You should see output similar to:

```
Translating 'I love to code.' to French...
Response: <translated text>
```


## Prerequisites

Before starting this tutorial, you need:

**Foundry Local**installed on your computer. Read the[Get started with Foundry Local](../get-started?view=foundry-classic)guide for installation instructions.**Node.js 18 or later**installed on your computer. You can download Node.js from the[official website](https://nodejs.org/).

## Install Node.js packages

You need to install the following Node.js packages:

```
npm install @langchain/openai @langchain/core
npm install foundry-local-sdk
```


This example uses ES modules (`import`

) and top-level `await`

. If you haven't already, initialize a Node.js project and enable ES modules:

```
npm init -y
```


In your `package.json`

, set:

```
{
"type": "module"
}
```


## Create a translation application

Create a new JavaScript file named `translation_app.js`

in your favorite IDE and add the following code:

```
import { FoundryLocalManager } from "foundry-local-sdk";
import { ChatOpenAI } from "@langchain/openai";
import { ChatPromptTemplate } from "@langchain/core/prompts";
// By using an alias, the most suitable model will be downloaded
// to your end-user's device.
// TIP: You can find a list of available models by running the
// following command in your terminal: `foundry model list`.
const alias = "phi-3-mini-4k";
// Create a FoundryLocalManager instance. This will start the Foundry
// Local service if it is not already running.
const foundryLocalManager = new FoundryLocalManager()
// Initialize the manager with a model. This will download the model
// if it is not already present on the user's device.
const modelInfo = await foundryLocalManager.init(alias)
console.log("Model Info:", modelInfo)
// Configure ChatOpenAI to use your locally-running model
const llm = new ChatOpenAI({
model: modelInfo.id,
configuration: {
baseURL: foundryLocalManager.endpoint,
apiKey: foundryLocalManager.apiKey
},
temperature: 0.6,
streaming: false
});
// Create a translation prompt template
const prompt = ChatPromptTemplate.fromMessages([
{
role: "system",
content: "You are a helpful assistant that translates {input_language} to {output_language}."
},
{
role: "user",
content: "{input}"
}
]);
// Build a simple chain by connecting the prompt to the language model
const chain = prompt.pipe(llm);
const input = "I love to code.";
console.log(`Translating '${input}' to French...`);
// Run the chain with your inputs
chain.invoke({
input_language: "English",
output_language: "French",
input: input
}).then(aiMsg => {
// Print the result content
console.log(`Response: ${aiMsg.content}`);
}).catch(err => {
console.error("Error:", err);
});
```


#### References

- Reference:
[Foundry Local SDK reference](../reference/reference-sdk?view=foundry-classic) - Reference:
[Get started with Foundry Local](../get-started?view=foundry-classic)

Note

One of the key benefits of Foundry Local is that it **automatically** selects the most suitable model **variant** for the user's hardware. For example, if the user has a GPU, it downloads the GPU version of the model. If the user has an NPU (Neural Processing Unit), it downloads the NPU version. If the user doesn't have either a GPU or NPU, it downloads the CPU version of the model.

## Run the application

To run the application, open a terminal and navigate to the directory where you saved the `translation_app.js`

file. Then, run the following command:

```
node translation_app.js
```


You're done when you see a `Response:`

line with the translated text.

You should see output similar to:

```
Model Info: { ... }
Translating 'I love to code.' to French...
Response: <translated text>
```


## Troubleshooting

- If you see a service connection error, restart the Foundry Local service and try again.
- The first run can take longer because Foundry Local might download the model.
- If Node.js fails with an import or top-level await error, confirm your project is configured for ES modules.

## Related content

- Explore the
[LangChain documentation](https://python.langchain.com/docs/introduction)for advanced features. [Compile Hugging Face models to run on Foundry Local](how-to-compile-hugging-face-models?view=foundry-classic)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/how-to/how-to-compile-hugging-face-models -->

# Compile Hugging Face models to run on Foundry Local

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

Foundry Local runs ONNX models on your device. Use [Olive](https://microsoft.github.io/Olive/) to convert and optimize models from Hugging Face (Safetensors or PyTorch) into ONNX so you can run them with Foundry Local.

Important

The Olive CLI and optimization settings change over time, and a single command line example might not work for every model, device, or execution provider.

For the most reliable, up-to-date examples, start with the [Olive Recipes repository](https://github.com/microsoft/olive-recipes). It includes a dedicated recipe for [ meta-llama/Llama-3.2-1B-Instruct](https://github.com/microsoft/olive-recipes/tree/main/meta-llama-Llama-3.2-1B-Instruct).

- For Olive CLI configs for this model, see the recipe folder:
[https://github.com/microsoft/olive-recipes/tree/main/meta-llama-Llama-3.2-1B-Instruct/olive](https://github.com/microsoft/olive-recipes/tree/main/meta-llama-Llama-3.2-1B-Instruct/olive). - For a Foundry Local-oriented artifact layout (for example, an
`inference_model.json`

you can reuse), see:[https://github.com/microsoft/olive-recipes/tree/main/meta-llama-Llama-3.2-1B-Instruct/aitk](https://github.com/microsoft/olive-recipes/tree/main/meta-llama-Llama-3.2-1B-Instruct/aitk).

This guide shows how to:

- Convert and optimize models from Hugging Face to run in Foundry Local. The examples use the
`Llama-3.2-1B-Instruct`

model, but many Hugging Face models can work. - Run your optimized models with Foundry Local.

## Prerequisites

- Foundry Local installed. For installation instructions, see
[Get started with Foundry Local](../get-started?view=foundry-classic). - Python 3.10 or later
- A Hugging Face account and token with access to
`meta-llama/Llama-3.2-1B-Instruct`


Verify your tools:

```
python --version
foundry --version
olive --help
huggingface-cli --help
```


## Install Olive

[Olive](https://github.com/microsoft/olive) optimizes models and converts them to the ONNX format.

```
pip install olive-ai[auto-opt]
```


Expected result: `olive auto-opt --help`

prints usage information.

References:

- Reference:
[Olive documentation](https://microsoft.github.io/Olive/) - Reference:
[Olive repository](https://github.com/microsoft/olive)

## Sign in to Hugging Face

The `Llama-3.2-1B-Instruct`

model requires Hugging Face authentication.

```
huggingface-cli login
```


Note

[Create a Hugging Face token](https://huggingface.co/docs/hub/security-tokens) and [request model access](https://huggingface.co/meta-llama/Llama-3.2-1B-Instruct) before proceeding.

Tip

If `huggingface-cli`

isn't found, install it by running `pip install -U huggingface_hub`

.

Expected result: The authentication command finishes without errors.

References:

- Reference:
[Hugging Face user access tokens](https://huggingface.co/docs/hub/security-tokens)

## Compile the model

### Manual example (might require adjustments)

#### Step 1: Run the Olive auto-opt command

Use the Olive `auto-opt`

command to download, convert, quantize, and optimize the model:

```
olive auto-opt \
--model_name_or_path meta-llama/Llama-3.2-1B-Instruct \
--trust_remote_code \
--output_path models/llama \
--device cpu \
--provider CPUExecutionProvider \
--use_ort_genai \
--precision int4 \
--log_level 1
```


Note

The compilation process takes about 60 seconds, plus download time.

Expected result: The command creates the `models/llama/model`

directory.

The command uses the following parameters:

| Parameter | Description |
|---|---|
`model_name_or_path` |
Model source: Hugging Face ID, local path, or Azure AI Model registry ID |
`output_path` |
Where to save the optimized model |
`device` |
Target hardware: `cpu` , `gpu` , or `npu` |
`provider` |
Execution provider (for example, `CPUExecutionProvider` , `CUDAExecutionProvider` ) |
`precision` |
Model precision: `fp16` , `fp32` , `int4` , or `int8` |
`use_ort_genai` |
Creates inference configuration files |

Tip

If you have a local copy of the model, use a local path instead of the Hugging Face ID. For example, `--model_name_or_path models/llama-3.2-1B-Instruct`

. Olive handles the conversion, optimization, and quantization automatically.

References:

- Reference:
[Olive documentation](https://microsoft.github.io/Olive/)

#### Step 2: Rename the output model

Olive creates a generic `model`

directory. Rename it for easier reuse:

```
cd models/llama
mv model llama-3.2
```


Expected result: The `models/llama/llama-3.2`

directory exists.

#### Step 3: Create chat template file

Foundry Local requires a chat template JSON file named `inference_model.json`

in the model directory. Foundry Local injects the user prompt into the template using the `{Content}`

placeholder at runtime.

Create the chat template file by using the `apply_chat_template`

method from the Hugging Face library:

Note

This example uses the Hugging Face library (a dependency of Olive) to create a chat template. If you're using the same Python virtual environment, you don't need to install it. In a different environment, install it by running `pip install transformers`

.

```
# generate_inference_model.py
import json
import os
from transformers import AutoTokenizer
model_path = "models/llama/llama-3.2"
tokenizer = AutoTokenizer.from_pretrained(model_path)
chat = [
{"role": "system", "content": "You are a helpful assistant."},
{"role": "user", "content": "{Content}"},
]
template = tokenizer.apply_chat_template(chat, tokenize=False, add_generation_prompt=True)
json_template = {
"Name": "llama-3.2",
"PromptTemplate": {
"assistant": "{Content}",
"prompt": template
}
}
json_file = os.path.join(model_path, "inference_model.json")
with open(json_file, "w") as f:
json.dump(json_template, f, indent=2)
```


Run the script by using the following command:

```
python generate_inference_model.py
```


Expected result: `models/llama/llama-3.2/inference_model.json`

exists.

References:

- Reference:
[Transformers documentation](https://huggingface.co/docs/transformers/index)

## Run the model

Run your compiled model by using the Foundry Local CLI, REST API, or OpenAI Python SDK. First, change the model cache directory to the models directory you created in the previous step:

```
foundry cache cd models
foundry cache list # should show llama-3.2
```


Caution

Change the model cache back to the default directory when you're done:

```
foundry cache cd ./foundry/cache/models
```


If you're not sure what your current cache directory is, run `foundry cache location`

.

Expected result: `foundry cache list`

shows `llama-3.2`

.

References:

- Reference:
[Get started with Foundry Local](../get-started?view=foundry-classic) - Reference:
[Foundry Local CLI reference](../reference/reference-cli?view=foundry-classic)

### Using the Foundry Local CLI

```
foundry model run llama-3.2 --verbose
```


Expected result: Foundry Local starts (if needed) and you can interact with the model in your terminal.

References:

- Reference:
[Foundry Local CLI reference](../reference/reference-cli?view=foundry-classic)

### Using the OpenAI Python SDK

Use the OpenAI Python SDK to interact with the Foundry Local REST API. Install it by using the following command:

```
pip install openai
pip install foundry-local-sdk
```


Then run the model with the following code:

```
import openai
from foundry_local import FoundryLocalManager
modelId = "llama-3.2"
# Create a FoundryLocalManager instance. This starts the Foundry Local service if it's not already running and loads the specified model.
manager = FoundryLocalManager(modelId)
# The remaining code uses the OpenAI Python SDK to interact with the local model.
# Configure the client to use the local Foundry service
client = openai.OpenAI(
base_url=manager.endpoint,
api_key=manager.api_key # API key is not required for local usage
)
# Set the model to use and generate a streaming response
stream = client.chat.completions.create(
model=manager.get_model_info(modelId).id,
messages=[{"role": "user", "content": "What is the golden ratio?"}],
stream=True
)
# Print the streaming response
for chunk in stream:
if chunk.choices[0].delta.content is not None:
print(chunk.choices[0].delta.content, end="", flush=True)
```


Expected result: The script prints a streamed response from the local model.

Tip

Use any language that supports HTTP requests. For more information, see [Integrated inferencing SDKs with Foundry Local](how-to-integrate-with-inference-sdks?view=foundry-classic).

References:

- Reference:
[Foundry Local SDK reference](../reference/reference-sdk?view=foundry-classic) - Reference:
[Use chat completions via REST server with Foundry Local](how-to-integrate-with-inference-sdks?view=foundry-classic)

## Reset the model cache

After you finish using the custom model, reset the model cache to the default directory:

```
foundry cache cd ./foundry/cache/models
```


References:

- Reference:
[Foundry Local CLI reference](../reference/reference-cli?view=foundry-classic)

## Troubleshooting

- If the
`foundry`

command isn't found, install Foundry Local. See[Get started with Foundry Local](../get-started?view=foundry-classic). - If Foundry Local starts but requests fail, run
`foundry service restart`

. For an example error and fix, see the troubleshooting section in[Get started with Foundry Local](../get-started?view=foundry-classic). - If the
`huggingface-cli`

command isn't found, install it by running`pip install -U huggingface_hub`

, and then run`huggingface-cli login`

. - If
`olive auto-opt`

fails with an authentication or access error, confirm your token and model access request is approved.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/how-to/how-to-integrate-with-inference-sdks -->

# Integrate inference SDKs with Foundry Local

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

Foundry Local integrates with OpenAI-compatible SDKs and HTTP clients through a local REST server. This article shows you how to connect your app to local AI models by using popular SDKs.

## Prerequisites

- Foundry Local installed and available on your PATH. For setup steps, see
[Get started with Foundry Local](../get-started?view=foundry-classic). - Python 3.9 or later installed. You can download Python from the
[official Python website](https://www.python.org/downloads/).

## Install pip packages

Install the following Python packages:

```
pip install openai
pip install foundry-local-sdk
pip install requests
```


Tip

We recommend using a virtual environment to avoid package conflicts. You can create a virtual environment using either `venv`

or `conda`

.

## Use OpenAI SDK with Foundry Local

The following example demonstrates how to use the OpenAI SDK with Foundry Local. The code initializes the Foundry Local service, loads a model, and generates a response using the OpenAI SDK.

Copy-and-paste the following code into a Python file named `app.py`

:

```
import openai
from foundry_local import FoundryLocalManager
# By using an alias, the most suitable model will be downloaded
# to your end-user's device.
alias = "qwen2.5-0.5b"
# Create a FoundryLocalManager instance. This will start the Foundry
# Local service if it is not already running and load the specified model.
manager = FoundryLocalManager(alias)
# The remaining code uses the OpenAI Python SDK to interact with the local model.
# Configure the client to use the local Foundry service
client = openai.OpenAI(
base_url=manager.endpoint,
api_key=manager.api_key # API key is not required for local usage
)
# Set the model to use and generate a response
response = client.chat.completions.create(
model=manager.get_model_info(alias).id,
messages=[{"role": "user", "content": "What is the golden ratio?"}]
)
print(response.choices[0].message.content)
```


Reference: [Foundry Local SDK reference](../reference/reference-sdk?view=foundry-classic)
Reference: [Foundry Local REST API reference](../reference/reference-rest?view=foundry-classic)

Run the code using the following command:

```
python app.py
```


You should see a text response printed in your terminal. On the first run, Foundry Local might download execution providers and the model, which can take a few minutes.

### Streaming Response

If you want to receive a streaming response, you can modify the code as follows:

```
import openai
from foundry_local import FoundryLocalManager
# By using an alias, the most suitable model will be downloaded
# to your end-user's device.
alias = "qwen2.5-0.5b"
# Create a FoundryLocalManager instance. This will start the Foundry
# Local service if it is not already running and load the specified model.
manager = FoundryLocalManager(alias)
# The remaining code uses the OpenAI Python SDK to interact with the local model.
# Configure the client to use the local Foundry service
client = openai.OpenAI(
base_url=manager.endpoint,
api_key=manager.api_key # API key is not required for local usage
)
# Set the model to use and generate a streaming response
stream = client.chat.completions.create(
model=manager.get_model_info(alias).id,
messages=[{"role": "user", "content": "What is the golden ratio?"}],
stream=True
)
# Print the streaming response
for chunk in stream:
if chunk.choices[0].delta.content is not None:
print(chunk.choices[0].delta.content, end="", flush=True)
```


Reference: [Foundry Local REST API reference](../reference/reference-rest?view=foundry-classic)

You can run the code using the same command as before:

```
python app.py
```


You should see tokens stream to your terminal.

## Use `requests`

with Foundry Local

```
# Install with: pip install requests
import requests
import json
from foundry_local import FoundryLocalManager
# By using an alias, the most suitable model will be downloaded
# to your end-user's device.
alias = "qwen2.5-0.5b"
# Create a FoundryLocalManager instance. This will start the Foundry
# Local service if it is not already running and load the specified model.
manager = FoundryLocalManager(alias)
url = manager.endpoint + "/chat/completions"
payload = {
"model": manager.get_model_info(alias).id,
"messages": [
{"role": "user", "content": "What is the golden ratio?"}
]
}
headers = {
"Content-Type": "application/json"
}
response = requests.post(url, headers=headers, data=json.dumps(payload))
print(response.json()["choices"][0]["message"]["content"])
```


Reference: [Foundry Local REST API reference](../reference/reference-rest?view=foundry-classic)

## Prerequisites

- Install Foundry Local. For setup steps, see
[Get started with Foundry Local](../get-started?view=foundry-classic). [.NET 9.0 SDK](https://dotnet.microsoft.com/download/dotnet/9.0)or later installed.

## Samples repository

The sample in this article can be found in the [Foundry Local C# SDK Samples GitHub repository](https://aka.ms/foundrylocalSDK).

## Set up project

Use Foundry Local in your C# project by following these Windows-specific or Cross-Platform (macOS/Linux/Windows) instructions:

- Create a new C# project and navigate into it:
`dotnet new console -n app-name cd app-name`

- Open and edit the
`app-name.csproj`

file to:`<Project Sdk="Microsoft.NET.Sdk"> <PropertyGroup> <OutputType>Exe</OutputType> <TargetFramework>net9.0-windows10.0.26100</TargetFramework> <RootNamespace>app-name</RootNamespace> <ImplicitUsings>enable</ImplicitUsings> <Nullable>enable</Nullable> <WindowsAppSDKSelfContained>false</WindowsAppSDKSelfContained> <WindowsPackageType>None</WindowsPackageType> <EnableCoreMrtTooling>false</EnableCoreMrtTooling> </PropertyGroup> <ItemGroup> <PackageReference Include="Microsoft.AI.Foundry.Local.WinML" Version="0.8.2.1" /> <PackageReference Include="Microsoft.Extensions.Logging" Version="9.0.10" /> <PackageReference Include="OpenAI" Version="2.5.0" /> </ItemGroup> </Project>`

- Create a
`nuget.config`

file in the project root with the following content so that the packages restore correctly:`<?xml version="1.0" encoding="utf-8"?> <configuration> <packageSources> <clear /> <add key="nuget.org" value="https://api.nuget.org/v3/index.json" /> <add key="ORT" value="https://aiinfra.pkgs.visualstudio.com/PublicPackages/_packaging/ORT/nuget/v3/index.json" /> </packageSources> <packageSourceMapping> <packageSource key="nuget.org"> <package pattern="*" /> </packageSource> <packageSource key="ORT"> <package pattern="*Foundry*" /> </packageSource> </packageSourceMapping> </configuration>`


## Use OpenAI SDK with Foundry Local

The following example demonstrates how to use the OpenAI SDK with Foundry Local. The code includes the following steps:

Initializes a

`FoundryLocalManager`

instance with a`Configuration`

that includes the web service configuration. The web service is an OpenAI compliant endpoint.Gets a

`Model`

object from the model catalog using an alias.Note

Foundry Local will select the best variant for the model automatically based on the available hardware of the host machine.

Downloads and loads the model variant.

Starts the web service.

Uses the OpenAI SDK to call the local Foundry web service.

Tidies up by stopping the web service and unloading the model.


Copy-and-paste the following code into a C# file named `Program.cs`

:

```
using Microsoft.AI.Foundry.Local;
using Microsoft.Extensions.Logging;
using OpenAI;
using System.ClientModel;
var config = new Configuration
{
AppName = "app-name",
LogLevel = Microsoft.AI.Foundry.Local.LogLevel.Information,
Web = new Configuration.WebService
{
Urls = "http://127.0.0.1:55588"
}
};
using var loggerFactory = LoggerFactory.Create(builder =>
{
builder.SetMinimumLevel(Microsoft.Extensions.Logging.LogLevel.Information);
});
var logger = loggerFactory.CreateLogger<Program>();
// Initialize the singleton instance.
await FoundryLocalManager.CreateAsync(config, logger);
var mgr = FoundryLocalManager.Instance;
// Get the model catalog
var catalog = await mgr.GetCatalogAsync();
// Get a model using an alias
var model = await catalog.GetModelAsync("qwen2.5-0.5b") ?? throw new Exception("Model not found");
// Download the model (the method skips download if already cached)
await model.DownloadAsync(progress =>
{
Console.Write($"\rDownloading model: {progress:F2}%");
if (progress >= 100f)
{
Console.WriteLine();
}
});
// Load the model
await model.LoadAsync();
// Start the web service
await mgr.StartWebServiceAsync();
// <<<<<< OPEN AI SDK USAGE >>>>>>
// Use the OpenAI SDK to call the local Foundry web service
ApiKeyCredential key = new ApiKeyCredential("notneeded");
OpenAIClient client = new OpenAIClient(key, new OpenAIClientOptions
{
Endpoint = new Uri(config.Web.Urls + "/v1"),
});
var chatClient = client.GetChatClient(model.Id);
var completionUpdates = chatClient.CompleteChatStreaming("Why is the sky blue?");
Console.Write($"[ASSISTANT]: ");
foreach (var completionUpdate in completionUpdates)
{
if (completionUpdate.ContentUpdate.Count > 0)
{
Console.Write(completionUpdate.ContentUpdate[0].Text);
}
}
Console.WriteLine();
// <<<<<< END OPEN AI SDK USAGE >>>>>>
// Tidy up
// Stop the web service and unload model
await mgr.StopWebServiceAsync();
await model.UnloadAsync();
```


Reference: [Foundry Local SDK reference](../reference/reference-sdk?view=foundry-classic)
Reference: [Foundry Local REST API reference](../reference/reference-rest?view=foundry-classic)

Run the code using the following command:

For x64 Windows, use the following command:

```
dotnet run -r win-x64
```


For arm64 Windows, use the following command:

```
dotnet run -r win-arm64
```


## Prerequisites

- Foundry Local installed and running. For installation instructions, see
[Get started with Foundry Local](../get-started?view=foundry-classic). [Node.js](https://nodejs.org/en/download/)version 18 or later installed.

## Install Node.js packages

You need to install the following Node.js packages:

```
npm install openai
npm install foundry-local-sdk
```


The Foundry Local SDK allows you to manage the Foundry Local service and models.

## Use OpenAI SDK with Foundry Local

The following example demonstrates how to use the OpenAI SDK with Foundry Local. The code initializes the Foundry Local service, loads a model, and generates a response using the OpenAI SDK.

Copy-and-paste the following code into a JavaScript file named `app.mjs`

:

```
import { OpenAI } from "openai";
import { FoundryLocalManager } from "foundry-local-sdk";
// By using an alias, the most suitable model will be downloaded
// to your end-user's device.
// TIP: You can find a list of available models by running the
// following command in your terminal: `foundry model list`.
const alias = "qwen2.5-0.5b";
// Create a FoundryLocalManager instance. This will start the Foundry
// Local service if it is not already running.
const foundryLocalManager = new FoundryLocalManager();
// Initialize the manager with a model. This will download the model
// if it is not already present on the user's device.
const modelInfo = await foundryLocalManager.init(alias);
console.log("Model Info:", modelInfo);
const openai = new OpenAI({
baseURL: foundryLocalManager.endpoint,
apiKey: foundryLocalManager.apiKey,
});
async function generateText() {
const response = await openai.chat.completions.create({
model: modelInfo.id,
messages: [
{
role: "user",
content: "What is the golden ratio?",
},
],
});
console.log(response.choices[0].message.content);
}
generateText();
```


Reference: [Foundry Local SDK reference](../reference/reference-sdk?view=foundry-classic)
Reference: [Foundry Local REST API reference](../reference/reference-rest?view=foundry-classic)

Run the code using the following command:

```
node app.mjs
```


You should see a text response printed in your terminal. On the first run, Foundry Local might download execution providers and the model, which can take a few minutes.

### Streaming Responses

If you want to receive streaming responses, you can modify the code as follows:

```
import { OpenAI } from "openai";
import { FoundryLocalManager } from "foundry-local-sdk";
// By using an alias, the most suitable model will be downloaded
// to your end-user's device.
// TIP: You can find a list of available models by running the
// following command in your terminal: `foundry model list`.
const alias = "qwen2.5-0.5b";
// Create a FoundryLocalManager instance. This will start the Foundry
// Local service if it is not already running.
const foundryLocalManager = new FoundryLocalManager();
// Initialize the manager with a model. This will download the model
// if it is not already present on the user's device.
const modelInfo = await foundryLocalManager.init(alias);
console.log("Model Info:", modelInfo);
const openai = new OpenAI({
baseURL: foundryLocalManager.endpoint,
apiKey: foundryLocalManager.apiKey,
});
async function streamCompletion() {
const stream = await openai.chat.completions.create({
model: modelInfo.id,
messages: [{ role: "user", content: "What is the golden ratio?" }],
stream: true,
});
for await (const chunk of stream) {
if (chunk.choices[0]?.delta?.content) {
process.stdout.write(chunk.choices[0].delta.content);
}
}
}
streamCompletion();
```


Reference: [Foundry Local REST API reference](../reference/reference-rest?view=foundry-classic)

Run the code using the following command:

```
node app.mjs
```


You should see tokens stream to your terminal.

## Use Fetch API with Foundry Local

If you prefer to use an HTTP client like `fetch`

, you can do so as follows:

```
import { FoundryLocalManager } from "foundry-local-sdk";
// By using an alias, the most suitable model will be downloaded
// to your end-user's device.
// TIP: You can find a list of available models by running the
// following command in your terminal: `foundry model list`.
const alias = "qwen2.5-0.5b";
// Create a FoundryLocalManager instance. This will start the Foundry
// Local service if it is not already running.
const foundryLocalManager = new FoundryLocalManager();
// Initialize the manager with a model. This will download the model
// if it is not already present on the user's device.
const modelInfo = await foundryLocalManager.init(alias);
console.log("Model Info:", modelInfo);
async function queryModel() {
const response = await fetch(
foundryLocalManager.endpoint + "/chat/completions",
{
method: "POST",
headers: {
"Content-Type": "application/json",
},
body: JSON.stringify({
model: modelInfo.id,
messages: [{ role: "user", content: "What is the golden ratio?" }],
}),
}
);
const data = await response.json();
console.log(data.choices[0].message.content);
}
queryModel();
```


Reference: [Foundry Local REST API reference](../reference/reference-rest?view=foundry-classic)

### Streaming Responses

If you want to receive streaming responses using the Fetch API, you can modify the code as follows:

```
import { FoundryLocalManager } from "foundry-local-sdk";
// By using an alias, the most suitable model will be downloaded
// to your end-user's device.
// TIP: You can find a list of available models by running the
// following command in your terminal: `foundry model list`.
const alias = "qwen2.5-0.5b";
// Create a FoundryLocalManager instance. This will start the Foundry
// Local service if it is not already running.
const foundryLocalManager = new FoundryLocalManager();
// Initialize the manager with a model. This will download the model
// if it is not already present on the user's device.
const modelInfo = await foundryLocalManager.init(alias);
console.log("Model Info:", modelInfo);
async function streamWithFetch() {
const response = await fetch(
foundryLocalManager.endpoint + "/chat/completions",
{
method: "POST",
headers: {
"Content-Type": "application/json",
Accept: "text/event-stream",
},
body: JSON.stringify({
model: modelInfo.id,
messages: [{ role: "user", content: "what is the golden ratio?" }],
stream: true,
}),
}
);
const reader = response.body.getReader();
const decoder = new TextDecoder();
while (true) {
const { done, value } = await reader.read();
if (done) break;
const chunk = decoder.decode(value);
const lines = chunk.split("\n").filter((line) => line.trim() !== "");
for (const line of lines) {
if (line.startsWith("data: ")) {
const data = line.substring(6);
if (data === "[DONE]") continue;
try {
const json = JSON.parse(data);
const content = json.choices[0]?.delta?.content || "";
if (content) {
// Print to console without line breaks, similar to process.stdout.write
process.stdout.write(content);
}
} catch (e) {
console.error("Error parsing JSON:", e);
}
}
}
}
}
// Call the function to start streaming
streamWithFetch();
```


Reference: [Foundry Local REST API reference](../reference/reference-rest?view=foundry-classic)

## Prerequisites

- Foundry Local installed and running. For installation instructions, see
[Get started with Foundry Local](../get-started?view=foundry-classic). [Rust and Cargo](https://www.rust-lang.org/tools/install)installed.

## Create project

Create a new Rust project and navigate into it:

```
cargo new hello-foundry-local
cd hello-foundry-local
```


### Install crates

Install the following Rust crates using Cargo:

```
cargo add foundry-local anyhow env_logger serde_json
cargo add reqwest --features json
cargo add tokio --features full
```


## Update the `main.rs`

file

The following example demonstrates how to run inference by sending a request to the Foundry Local service. The code initializes the Foundry Local service, loads a model, and generates a response using the `reqwest`

library.

Copy-and-paste the following code into the Rust file named `main.rs`

:

```
use foundry_local::FoundryLocalManager;
use anyhow::Result;
#[tokio::main]
async fn main() -> Result<()> {
// Create a FoundryLocalManager instance with default options
let mut manager = FoundryLocalManager::builder()
.alias_or_model_id("qwen2.5-0.5b") // Specify the model to use
.bootstrap(true) // Start the service if not running
.build()
.await?;
// Use the OpenAI compatible API to interact with the model
let client = reqwest::Client::new();
let endpoint = manager.endpoint()?;
let response = client.post(format!("{}/chat/completions", endpoint))
.header("Content-Type", "application/json")
.header("Authorization", format!("Bearer {}", manager.api_key()))
.json(&serde_json::json!({
"model": manager.get_model_info("qwen2.5-0.5b", true).await?.id,
"messages": [{"role": "user", "content": "What is the golden ratio?"}],
}))
.send()
.await?;
let result = response.json::<serde_json::Value>().await?;
println!("{}", result["choices"][0]["message"]["content"]);
Ok(())
}
```


Reference: [Foundry Local SDK reference](../reference/reference-sdk?view=foundry-classic)
Reference: [Foundry Local REST API reference](../reference/reference-rest?view=foundry-classic)

Run the code using the following command:

```
cargo run
```


You should see a text response printed in your terminal. On the first run, Foundry Local might download execution providers and the model, which can take a few minutes.
