---
merged_at: 2026-01-31T00:00:15.019797
merged_files: 4
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/concepts/foundry-local-architecture -->

# Foundry Local architecture

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

Foundry Local provides efficient, secure, and scalable AI model inference directly on your device. This article explains the core components of Foundry Local and how they work together to deliver AI capabilities.

## Prerequisites

- Install Foundry Local. For setup steps, see
[Get started with Foundry Local](../get-started?view=foundry-classic). - Use a local terminal where the
`foundry`

CLI is available.

## Quick verification

Use the following quick checks to confirm the service is running and reachable.

- Get the service status and local endpoint:

```
foundry service status
```


This command prints the service status and the dynamically assigned local endpoint.

Reference: [Foundry Local CLI Reference](../reference/reference-cli?view=foundry-classic#service-commands)

- Call the local REST status endpoint:

```
curl http://localhost:PORT/openai/status
```


Replace `PORT`

with the port shown by `foundry service status`

. A successful response is JSON that includes `Endpoints`

, `ModelDirPath`

, and `PipeName`

.

Reference: [Foundry Local REST API Reference](../reference/reference-rest?view=foundry-classic#get-openaistatus)

Foundry Local offers these key benefits:

**Low latency**: Run models locally to minimize processing time and deliver faster results.**Data privacy**: Process sensitive data locally without sending it to the cloud for inference, helping meet data protection requirements.**Flexibility**: Support for diverse hardware configurations lets you choose the optimal setup for your needs.**Scalability**: Deploy across various devices, from laptops to servers, to suit different use cases.**Cost-effectiveness**: Reduce cloud computing costs, especially for high-volume applications.**Offline operation**: Work without an internet connection in remote or disconnected environments.**Seamless integration**: Easily incorporate into existing development workflows for smooth adoption.

Foundry Local can still use the network for operations like downloading models and execution providers. If you report a problem, you might choose to share logs (for example, by using `foundry zip-logs`

).

## Key components

The Foundry Local architecture consists of these main components:


### Foundry Local service

The Foundry Local Service includes an OpenAI-compatible REST server that provides a standard interface for working with the inference engine. You can also manage models over REST. Developers use this API to send requests, run models, and get results programmatically.

**Endpoint**: The endpoint is*dynamically allocated*when the service starts. Find it by running the`foundry service status`

command, or by calling`GET /openai/status`

. When using Foundry Local in your applications, use an integration SDK that automatically handles endpoint discovery. For more details, see[Integrate with inference SDKs](../how-to/how-to-integrate-with-inference-sdks?view=foundry-classic)and the[Foundry Local REST API Reference](../reference/reference-rest?view=foundry-classic).**Use Cases**:- Connect Foundry Local to your custom applications
- Execute models through HTTP requests


### ONNX runtime

The ONNX Runtime is a core component that executes AI models. It runs optimized ONNX models efficiently on local hardware like CPUs, GPUs, or NPUs.

**Features**:

- Works with multiple hardware providers (NVIDIA, AMD, Intel, Qualcomm) and device types (NPUs, CPUs, GPUs)
- Offers a consistent interface for running models across different hardware
- Delivers high performance
- Supports quantized models for faster inference

### Model management

Foundry Local provides robust tools for managing AI models, ensuring that they're readily available for inference and easy to maintain. You handle model management through the **Model Cache** and the **Command-Line Interface (CLI)**.

#### Model cache

The model cache stores downloaded AI models locally on your device, which ensures models are ready for inference without needing to download them repeatedly. You can manage the cache by using either the Foundry CLI or REST API.

**Purpose**: Speeds up inference by keeping models locally available**Key Commands**:`foundry cache list`

: Shows all models in your local cache`foundry cache remove <model-name>`

: Removes a specific model from the cache`foundry cache cd <path>`

: Changes the storage location for cached models


#### Model lifecycle

**Download**: Download models from the Foundry model catalog and save them to your local disk.**Load**: Load models into the Foundry Local service memory for inference. Set a TTL (time-to-live) to control how long the model stays in memory (default: 600 seconds).**Run**: Execute model inference for your requests.**Unload**: Remove models from memory to free up resources when no longer needed.**Delete**: Remove models from your local cache to reclaim disk space.

#### Model compilation using Olive

Before you can use models with Microsoft Foundry Local, you must compile and optimize them in the [ONNX](https://onnx.ai) format. Microsoft provides a selection of published models in the Foundry model catalog that are already optimized for Foundry Local. However, you aren't limited to those models - by using [Olive](https://microsoft.github.io/Olive/). Olive is a powerful framework for preparing AI models for efficient inference. It converts models into the ONNX format, optimizes their graph structure, and applies techniques like quantization to improve performance on local hardware.

Tip

To learn more about compiling models for Foundry Local, see [How to compile Hugging Face models to run on Foundry Local](../how-to/how-to-compile-hugging-face-models?view=foundry-classic).

### Hardware abstraction layer

The hardware abstraction layer ensures that Foundry Local runs on various devices by abstracting the underlying hardware. To optimize performance based on the available hardware, Foundry Local supports:

**multiple**, such as NVIDIA CUDA, AMD, Qualcomm, Intel.*execution providers***multiple**, such as CPU, GPU, NPU.*device types*

Note

For Intel NPU support on Windows, install the [Intel NPU driver](https://www.intel.com/content/www/us/en/download/794734/intel-npu-driver-windows.html) to enable hardware acceleration.

Note

For Qualcomm NPU support, install the [Qualcomm NPU driver](https://softwarecenter.qualcomm.com/catalog/item/QHND). If you encounter the error `Qnn error code 5005: "Failed to load from EpContext model. qnn_backend_manager."`

, this error typically indicates an outdated driver or NPU resource conflicts. Try rebooting to clear NPU resource conflicts, especially after using Windows Copilot+ features.

### Developer experiences

The Foundry Local architecture is designed to provide a seamless developer experience, enabling easy integration and interaction with AI models. Developers can choose from various interfaces to interact with the system, including:

#### Command-Line Interface (CLI)

The Foundry CLI is a powerful tool for managing models, the inference engine, and the local cache.

**Examples**:

`foundry model list`

: Lists all available models in the local cache.`foundry model run <model-name>`

: Runs a model.`foundry service status`

: Checks the status of the service.

Tip

To learn more about the CLI commands, read [Foundry Local CLI Reference](../reference/reference-cli?view=foundry-classic).

#### Inferencing SDK integration

Foundry Local supports integration with various SDKs in most languages, such as the OpenAI SDK, enabling developers to use familiar programming interfaces to interact with the local inference engine.

Tip

To learn more about integrating with inferencing SDKs, read [Integrate inferencing SDKs with Foundry Local](../how-to/how-to-integrate-with-inference-sdks?view=foundry-classic).

#### AI Toolkit for Visual Studio Code

The AI Toolkit for Visual Studio Code provides a user-friendly interface for developers to interact with Foundry Local. It allows users to run models, manage the local cache, and visualize results directly within the IDE.

**Features**:

- Model management: Download, load, and run models from within the IDE.
- Interactive console: Send requests and view responses in real-time.
- Visualization tools: Graphical representation of model performance and results.

**Prerequisites:**

- You have installed
[Foundry Local](../get-started?view=foundry-classic)and have a model service running. - You have installed the
[AI Toolkit for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-windows-ai-studio.windows-ai-studio)extension.

**Connect a Foundry Local model to AI Toolkit:**

**Add model in AI Toolkit**: Open AI Toolkit from the activity bar of Visual Studio Code. In the 'My Models' panel, select the 'Add model for remote interface' button and then select 'Add a custom model' from the dropdown menu.**Enter the chat-compatible endpoint URL**: Enter`http://localhost:PORT/v1/chat/completions`

, where`PORT`

is the port number of your Foundry Local endpoint. Find the port by running`foundry service status`

. Foundry Local dynamically assigns a port, so it might not always be the same.**Provide the model name**: Enter the exact model name you want to use, for example`phi-3.5-mini`

. List downloaded and cached models with`foundry cache list`

, or use`foundry model list`

to see models available for local use. You'll also be asked to enter a display name, which is only for your local use. To avoid confusion, use the same value as the model name.**Authentication**: If your local setup doesn't require authentication, leave the authentication headers field blank.

After completing these steps, your Foundry Local model appears in the **My Models** list in AI Toolkit. To start using it, right-click the model and select **Load in Playground**.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/ -->

# Foundry Local (preview) documentation

Safely design, customize, and manage AI applications and agents on-device.

This browser is no longer supported.

Upgrade to Microsoft Edge to take advantage of the latest features, security updates, and technical support.

Safely design, customize, and manage AI applications and agents on-device.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/what-is-foundry-local -->

# What is Foundry Local?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

Foundry Local is an on-device AI inference solution that you use to run AI models locally through a CLI, SDK, or REST API.

## Prerequisites

- Install Foundry Local. Follow
[Get started with Foundry Local](get-started?view=foundry-classic). - Use a terminal (for example, Windows Terminal or macOS Terminal).
- Have an internet connection for first-time model downloads.
- If you use Foundry Local only on your device, you don't need an Azure subscription and there are no Azure RBAC role requirements.

## Try it (CLI)

Run these commands to verify your installation and run a model locally.

```
foundry --help
foundry model list
foundry model run qwen2.5-0.5b
```


`foundry --help`

prints the available CLI commands.`foundry model list`

lists available models. The first run might download execution providers for your hardware.`foundry model run qwen2.5-0.5b`

downloads the model (first run) and starts an interactive prompt in your terminal.

Reference: [Foundry Local CLI reference](reference/reference-cli?view=foundry-classic)

## Key features

**On-device inference**: Run models locally to reduce costs and help keep data on your device.**Model customization**: Select a preset model or use your own to meet specific needs.**Cost efficiency**: Use existing hardware to eliminate recurring cloud costs and make AI more accessible.**Seamless integration**: Integrate with your apps through the SDK, API endpoints, or CLI. For multi-user or high-throughput workloads, move to[Microsoft Foundry](../?view=foundry-classic).

## Use cases

Foundry Local is ideal when you need to:

- Keep sensitive data on your device
- Operate in limited or offline environments
- Reduce cloud inference costs
- Get low latency AI responses for real-time applications
- Experiment with AI models before you deploy to the cloud

## Frequently asked questions

### Does Foundry Local send my prompts or outputs to Microsoft?

Foundry Local is designed to run inference on your device. When you send prompts to a local Foundry Local endpoint (for example, `http://localhost:PORT`

), your prompts and model outputs are processed locally.

Foundry Local can still use the network for operations like:

**Model and component downloads**: The first time you run a model, Foundry Local downloads the model files. It might also download execution providers for your hardware.**Optional diagnostics you choose to share**: If you report a problem, you might choose to share logs (for example, by using`foundry zip-logs`

).

Your use of Foundry Local is governed by the product terms and licenses that apply to the software and the models you run. If the terms allow Microsoft to collect diagnostic information, the details are described in those terms and the [Microsoft Privacy Statement](https://www.microsoft.com/en-us/privacy/privacystatement).

### Do I need an Azure subscription?

No. Foundry Local runs on your hardware, letting you run supported models locally without requiring an Azure subscription.

### Do I need special drivers for NPU acceleration?

Install the driver for your NPU hardware:

Intel NPU: Install the

[Intel NPU driver](https://www.intel.com/content/www/us/en/download/794734/intel-npu-driver-windows.html)to enable NPU acceleration on Windows.Qualcomm NPU: Install the

[Qualcomm NPU driver](https://softwarecenter.qualcomm.com/catalog/item/QHND)to enable NPU acceleration. If you see the error`Qnn error code 5005: Failed to load from EpContext model. qnn_backend_manager.`

, it likely indicates an outdated driver or an NPU resource conflict. Reboot to clear the conflict, especially after using Windows Copilot+ features.

After you install the drivers, Foundry Local automatically detects and uses the NPU.

## Get started

Follow the [Get started with Foundry Local](get-started?view=foundry-classic) guide to set up Foundry Local, discover models, and run your first local AI model.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/get-started -->

# Get started with Foundry Local

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

This guide shows you how to set up Foundry Local to run AI models on your device.

## Prerequisites

Your system must meet the following requirements to run Foundry Local:

**Operating System**: Windows 10 (x64), Windows 11 (x64/ARM), Windows Server 2025, macOS.**Hardware**: Minimum 8 GB RAM and 3 GB free disk space. Recommended 16 GB RAM and 15 GB free disk space.**Network**: Internet connection to download models and execution providers. After you download a model, you can run cached models offline.**Acceleration (optional)**: NVIDIA GPU (2000 series or newer), AMD GPU (6000 series or newer), AMD NPU, Intel iGPU, Intel NPU (32 GB or more of memory), Qualcomm Snapdragon X Elite (8 GB or more of memory), Qualcomm NPU, or Apple silicon.

To install Foundry Local by using the commands in this quickstart:

- On Windows, make sure
`winget`

is available. - On macOS, install Homebrew if you use the
`brew`

option.

Note

New NPUs are supported only on systems running Windows 24H2 or later. If you use an Intel NPU on Windows, install the [Intel NPU driver](https://www.intel.com/content/www/us/en/download/794734/intel-npu-driver-windows.html) to enable NPU acceleration in Foundry Local.

Make sure you have admin rights to install software.

Tip

If you see a service connection error after installation (for example, 'Request to local service failed'), run `foundry service restart`

.

## Quickstart

Get started quickly with Foundry Local:

### Option 1: Quick CLI setup

**Install Foundry Local**.**Windows**: Open a terminal and run the following command.`winget install Microsoft.FoundryLocal`

**macOS**: Open a terminal and run the following command.

Alternatively, you can download the installer from the`brew tap microsoft/foundrylocal brew install foundrylocal`

[Foundry Local GitHub repository](https://aka.ms/foundry-local-installer).

Reference:

[Foundry Local documentation](https://aka.ms/foundry-local-docs)**Verify the installation**. Run:`foundry --version`

You should see the installed version number.

Reference:

[Foundry Local CLI reference](reference/reference-cli?view=foundry-classic)**Run your first model**. Open a terminal and run this command:`foundry model run qwen2.5-0.5b`

Foundry Local downloads the model, which can take a few minutes depending on your internet speed, then runs it. After the model starts, interact with it by using the command-line interface (CLI). For example, you can ask:

`Why is the sky blue?`


Reference: [Foundry Local CLI reference](reference/reference-cli?view=foundry-classic)

### Option 2: Download starter projects

For practical, hands-on learning, download one of the starter projects that demonstrate real-world scenarios:

[Chat Application Starter](https://github.com/microsoft/Foundry-Local/tree/main/samples/electron/foundry-chat): Build a local chat interface with multiple model support.[Summarize Sample](https://github.com/microsoft/Foundry-Local/tree/main/samples/python/summarize): A command-line utility that generates summaries of text files or direct text input.[Function Calling Example](https://github.com/microsoft/Foundry-Local/tree/main/samples/python/functioncalling): Enable and use function calling with Phi-4 mini.

Each project includes:

- Step-by-step setup instructions
- Complete source code
- Configuration examples
- Best practices

Tip

These starter projects align with scenarios in the [how-to guides](how-to/how-to-chat-application-with-open-web-ui?view=foundry-classic) and provide immediate practical value.

Tip

Replace `qwen2.5-0.5b`

with any model name from the catalog (run `foundry model list`

to view available models). Foundry Local downloads the variant that best matches your system's hardware and software configuration. For example, if you have an NVIDIA GPU, Foundry Local downloads the CUDA version. If you have a Qualcomm NPU, Foundry Local downloads the NPU variant. If you have no GPU or NPU, Foundry Local downloads the CPU version.

When you run `foundry model list`

the first time, you see a download progress bar while Foundry Local downloads the execution providers for your hardware.

Reference: [Foundry Local CLI reference](reference/reference-cli?view=foundry-classic)

## Explore commands

The Foundry CLI organizes commands into these main categories:

**Model**: Commands for managing and running models.**Service**: Commands for managing the Foundry Local service.**Cache**: Commands for managing the local model cache (downloaded models on local disk).

To view all commands, use:

```
foundry --help
```


```
foundry model --help
```


foundry --help

```
foundry service --help
```


View **cache** commands:

```
foundry cache --help
```


Reference: [Foundry Local CLI reference](reference/reference-cli?view=foundry-classic)

## Optional: Run the latest GPT OSS 20B model

Run the `gpt-oss-20b`

model:

```
foundry model run gpt-oss-20b
```


Important

If the model isn't available for your device, run a smaller model (for example, `qwen2.5-0.5b`

).

For the CUDA variant, you typically need an NVIDIA GPU with 16 GB of VRAM or more.

Foundry Local version **0.6.87** or later adds support for this model. Check your version with:

```
foundry --version
```


Reference: [Foundry Local CLI reference](reference/reference-cli?view=foundry-classic)

Tip

For details on all CLI commands, see [Foundry Local CLI reference](reference/reference-cli?view=foundry-classic).

## Upgrade Foundry Local

Run the command for your OS to upgrade Foundry Local.

- Windows: In a terminal, run:
`winget upgrade --id Microsoft.FoundryLocal`

- macOS: In a terminal, run:
`brew upgrade foundrylocal`


## Uninstall Foundry Local

To uninstall Foundry Local, run the command for your operating system:

**Windows**: Open a terminal and run:`winget uninstall Microsoft.FoundryLocal`

**macOS**: Open a terminal and run:`brew rm foundrylocal brew untap microsoft/foundrylocal brew cleanup --scrub`


## Troubleshooting

### Service connection problems

If you see this error when you run `foundry model list`

or a similar command:

```
foundry model list
Exception: Request to local service failed.
Uri: http://127.0.0.1:0/foundry/list
The requested address is not valid in its context. (127.0.0.1:0)
Please check service status with 'foundry service status'.
```


Run this command to restart the service:

```
foundry service restart
```


This command fixes cases where the service runs but isn't accessible because of a port binding problem.

Reference: [Best practices and troubleshooting](reference/reference-best-practice?view=foundry-classic)

---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/reference/windows-server-frequently-asked-questions -->

# Foundry Local on Windows Server 2025

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Foundry Local on Windows Server 2025 lets you run selected Microsoft Foundry model capabilities entirely on a single Windows Server machine you operate. Use this FAQ to quickly confirm what differentiates the Local runtime from the cloud service, how you deploy it, supported OS and GPU scenarios, concurrency behavior, and how the SDK relates to the service.

## Frequently asked questions

**What is the capability differentiation between Foundry Local on Windows Server vs Foundry?****Capability****Foundry Local (on server)****Foundry (cloud)**Model catalog Local catalog is smaller, BYOM possible. Embeddings models aren't yet available in the Local catalog. Broad catalog, including embeddings in the service; managed updates, evaluation, safety tools, and agent services. Scale & HA Single node runtime. No ‑built-in ‑autoscale or ‑multinode‑ distribution. Managed scale, multiregional‑ options, HA/DR patterns, and platform governance. Best for high concurrency and bursting. Concurrency / throughput Limited; throughput declines as concurrent clients grow. No continuous batching today. Cloud scale and load distribution; platform services for concurrency and throughput. APIs OpenAI ‑compatible REST surface for chat/completions; MCP integration possible. Full Foundry APIs, Responses API, Agent Service, eval, and integration with dev tools. Operations You operate it like any server app: install, secure, monitor, back up; manage model bits locally. Enterprise governance, cost controls, environments, RBAC/Networking, evaluation, and integrated DevOps. **Is Foundry Local a Windows component, an app, or a service?**It runs as a service on a Windows Server machine. You can install it by using winget.

`winget install Microsoft.FoundryLocal`

**Which versions of server support Foundry Local?**- Windows Server 2025 Datacenter
- Windows Server 2025 Standard

**Does Foundry Local run on virtual machines with GPU-P?**Foundry Local

**detects the partitioned GPU inside a GPU-P VM**and picks up a CUDA-enabled model when one is available. Otherwise, it falls back appropriately. The execution provider is also automatically selected based on the availability of GPU inside the VM.**What are the concurrency limitations of Foundry Local on server?**Foundry Local isn't optimized to serve multiple users as a shared on-premises endpoint. It doesn't yet support concurrent inference requests. Requests to one Foundry Local endpoint are processed sequentially. You must manage parallel execution across multiple endpoints at the application level. As concurrent requests increase, throughput drops and latency increases. There's no continuous batching in the Local runtime, so request coalescing doesn't happen under load. For multiple users or spiky traffic, move to[Microsoft Foundry](../?view=foundry-classic).**How is Foundry Local SDK different from the Foundry Local service?**The

[Foundry Local SDK](reference-sdk?view=foundry-classic)is a development toolkit to build software or applications by using the Foundry Local service without using the Foundry Local CLI or REST APIs directly.

## Sample code

The [Medical report summary tool](https://github.com/microsoft/foundry-local-on-windowsserver-samples) demonstrates a medical report summarizer and translator using Foundry Local running in a remote Windows Server.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/reference/reference-best-practice -->

# Best practices and troubleshooting guide for Foundry Local

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

This article lists best practices and troubleshooting tips for Foundry Local.

## Prerequisites

- Install Foundry Local.
- Have internet access to download models (recommended).
- If you use the machine-scope installation workaround in this article, run PowerShell as Administrator.

### Verify the CLI

Run the following command to confirm that the Foundry Local CLI is installed and available in your PATH:

```
foundry --help
```


This command lists available commands and options.

Reference: [Foundry Local CLI Reference](reference-cli?view=foundry-classic)

## Security best practices

- Run Foundry Local only in environments that comply with your organization's security policies.
- Make sure your device meets your organization's security requirements when you handle sensitive data.
- Encrypt disks on devices that cache models containing sensitive fine-tuning data.

## Licensing considerations

Review the licensing implications for the models you run in Foundry Local. To view the full model license terms for each model in the catalog, run the following command. In the following command, replace the placeholder * <model>* with the model name:

```
foundry model info <model> --license
```


Reference: [Foundry Local CLI Reference](reference-cli?view=foundry-classic)

## Performance best practices

If you experience slow inference, consider the following strategies:

- Stop any AI Toolkit for VS Code inference session before you run Foundry Local.
- Use GPU acceleration when available.
- Identify bottlenecks by monitoring memory usage during inference.
- Try more quantized model variants (for example, INT8 instead of FP16).
- Adjust batch sizes for noninteractive workloads.

## Production deployment scope

Foundry Local is for on-device inference, not distributed, containerized, or multi-machine production deployments.

## Troubleshooting

### Common issues and solutions

| Issue | Possible cause | Solution |
|---|---|---|
| Slow inference | CPU-only model with a large parameter count. | Use GPU-optimized model variants when available. |
| Model download failures | Network connectivity issues. | Check your internet connection, and run `foundry cache list` to verify cache status. |
Service connection errors (`Request to local service failed. Uri:http://127.0.0.1:0/foundry/list` ) |
Port binding issues or the service isn't accessible. | Run `foundry service restart` to restart the service and resolve port binding problems. |
| Service fails to start. | Port conflicts or permission issues. | Run `foundry service restart` , or
`foundry zip-logs` . |
| Intel NPU not detected or not working | Missing or outdated Intel NPU driver. | Install the
|

`Qnn error code 5005: "Failed to load from EpContext model. qnn_backend_manager."`

)[Qualcomm NPU driver](https://softwarecenter.qualcomm.com/catalog/item/QHND). If the issue persists, reboot to clear NPU resource conflicts, especially after using Windows Copilot+ features.`winget install Microsoft.FoundryLocal --scope machine`

fails with “The current system configuration doesn't support the installation of this package.”[Installation issues](#installation-issues).### Installation issues

If `winget install Microsoft.FoundryLocal --scope machine`

fails with “The current system configuration doesn't support the installation of this package.”, use `Add-AppxProvisionedPackage`

instead.

- Download the
`.msix`

and its dependency package. - Run PowerShell as Administrator.
- Run the following command to install Foundry Local for all users:

```
Add-AppxProvisionedPackage -Online -PackagePath .\FoundryLocal.msix `
-DependencyPackagePath .\VcLibs.appx -SkipLicense
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/reference/reference-catalog-api -->

# Catalog API reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

Foundry Local lets you build and integrate your own catalog service. This article covers:

- Model format required for the catalog API
- Request and response format required for your catalog API to integrate with Foundry Local

## Prerequisites

- You have Foundry Local installed.
- You can run a web service that exposes a
`POST`

endpoint. - Your model artifacts are available in ONNX format.
- Azure role-based access control (RBAC): Not applicable.

## Model format

To work with Foundry Local, your model catalog must contain model files in the [Open Neural Network Exchange (ONNX)](https://onnx.ai/) format. To learn how to compile Hugging Face and PyTorch models to ONNX, see [Compile Hugging Face models to run on Foundry Local](../how-to/how-to-compile-hugging-face-models?view=foundry-classic).

## API format

### Request

Implement a POST endpoint in your catalog service that accepts a JSON request body. The request format for the catalog API is as follows:

**Method**:`POST`

**Content-Type**:`application/json`


#### Example request

```
curl -X POST <your-catalog-api-endpoint> \
-H "Content-Type: application/json" \
-d '{
"resourceIds": [
{
"resourceId": "azureml",
"entityContainerType": "Registry"
}
],
"indexEntitiesRequest": {
"filters": [
{
"field": "type",
"operator": "eq",
"values": [
"models"
]
},
{
"field": "kind",
"operator": "eq",
"values": [
"Versioned"
]
},
{
"field": "properties/variantInfo/variantMetadata/device",
"operator": "eq",
"values": [
"cpu",
"gpu"
]
},
{
"field": "properties/variantInfo/variantMetadata/executionProvider",
"operator": "eq",
"values": [
"cpuexecutionprovider",
"webgpuexecutionprovider"
]
}
],
"pageSize": 10,
"skip": null,
"continuationToken": null
}
}'
```


Replace `<your-catalog-api-endpoint>`

with your catalog service URL.

**What to expect**

- A successful response includes an
`indexEntitiesResponse`

object. - Search results are returned in
`indexEntitiesResponse.value`

.

Reference:

The request body must be a JSON object with the following fields:

`resourceIds`

: An array of resource IDs that specify the resources to query. Each item includes:`resourceId`

: The ID of the resource.`entityContainerType`

: The type of entity container, such as`Registry`

,`Workspace`

, and others.

`indexEntitiesRequest`

: An object that contains the search parameters.`filters`

: An array of filter objects that specify the criteria for filtering the search results. Each filter includes:`field`

: The field to filter on, such as`type`

,`kind`

, and others.`operator`

: The operator to use for the filter. For example,`eq`

(equals),`ne`

(not equals),`gt`

(greater than),`lt`

(less than), and others.`values`

: An array of values to match against the field.

`orderBy`

: An array of fields to order the results by.`searchText`

: A string to search for in the results.`pageSize`

: The maximum number of results to return (for pagination).`skip`

: The number of results to skip (for pagination).`continuationToken`

: A token for pagination to continue from a previous request.


#### Filterable fields (optional)

Implement the catalog API so it accepts the [Request](#request) format. Server-side filtering is optional. Skipping server-side filtering is faster to implement but is less efficient for searching models.

If you implement server-side filtering, use the following fields:

`type`

: The type of the model, such as`models`

,`datasets`

, and others.`kind`

: The kind of the model, such as`Versioned`

,`Unversioned`

, and others.`properties/variantInfo/variantMetadata/device`

: The device type, such as`cpu`

,`gpu`

, and others.`properties/variantInfo/variantMetadata/executionProvider`

: The execution provider, such as`cpuexecutionprovider`

,`webgpuexecutionprovider`

, and others.

### Response

The catalog API returns a JSON object that contains the search results.

#### Example response

```
{
"indexEntitiesResponse": {
"totalCount": 1,
"value": [
{
"assetId": "example-asset-id",
"version": "1",
"properties": {
"name": "example-model",
"version": 1,
"variantInfo": {
"variantMetadata": {
"device": "cpu",
"executionProvider": "cpuexecutionprovider"
}
}
}
}
],
"nextSkip": null,
"continuationToken": null
}
}
```


#### Response schema

```
{
"$schema": "http://json-schema.org/draft-07/schema#",
"type": "object",
"properties": {
"indexEntitiesResponse": {
"type": "object",
"properties": {
"totalCount": {
"type": "integer",
"description": "The total count of entities."
},
"value": {
"type": "array",
"description": "An array of LocalModel objects.",
"items": {
"$ref": "#/definitions/LocalModel"
}
},
"nextSkip": {
"type": "integer",
"description": "The number of items to skip for the next request."
},
"continuationToken": {
"type": "string",
"description": "A token to continue fetching results."
}
}
}
},
"definitions": {
"LocalModel": {
"type": "object",
"properties": {
"annotations": {
"type": "object",
"description": "Annotations associated with the model.",
"properties": {
"tags": {
"type": "object",
"description": "Tags associated with the annotation.",
"properties": {
"author": { "type": "string" },
"alias": { "type": "string" },
"directoryPath": { "type": "string" },
"license": { "type": "string" },
"licenseDescription": { "type": "string" },
"promptTemplate": { "type": "string" },
"task": { "type": "string" }
}
},
"systemCatalogData": {
"type": "object",
"properties": {
"publisher": { "type": "string" },
"displayName": { "type": "string" }
}
},
"name": { "type": "string" }
}
},
"properties": {
"type": "object",
"description": "Properties of the model.",
"properties": {
"name": { "type": "string" },
"version": { "type": "integer" },
"alphanumericVersion": { "type": "string" },
"variantInfo": {
"type": "object",
"properties": {
"parents": {
"type": "array",
"items": {
"type": "object",
"properties": {
"assetId": { "type": "string" }
}
}
},
"variantMetadata": {
"type": "object",
"properties": {
"modelType": { "type": "string" },
"device": { "type": "string" },
"executionProvider": { "type": "string" },
"fileSizeBytes": { "type": "integer" }
}
}
}
}
}
},
"version": {
"type": "string",
"description": "The version of the model."
},
"assetId": {
"type": "string",
"description": "The asset ID of the model."
}
}
}
}
}
```


Reference:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/reference/reference-cli -->

# Foundry Local CLI reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

This article provides a comprehensive reference for the Foundry Local command-line interface (CLI). The CLI organizes commands into logical categories to help you manage models, control the service, and maintain your local cache.

## Prerequisites

- Install Foundry Local. For setup steps, see
[Get started with Foundry Local](../get-started?view=foundry-classic). - Use a local terminal where the
`foundry`

CLI is available. - Ensure you have internet access for first-time downloads (execution providers and models).
- Azure RBAC: Not applicable (runs locally).
- If you have an Intel NPU on Windows, install the
[Intel NPU driver](https://www.intel.com/content/www/us/en/download/794734/intel-npu-driver-windows.html)for optimal NPU acceleration.

## Quick verification

Run these commands to confirm the CLI is installed and the service is reachable.

Show CLI help:

`foundry --help`

This command prints usage information and the list of available command groups.

Reference:

[Overview](#overview)Check the service status:

`foundry service status`

This command prints whether the Foundry Local service is running and includes its local endpoint.

Reference:

[Service commands](#service-commands)

## Overview

Use the built-in help to explore commands and options.

The CLI organizes commands into three main categories:

**Model**: Commands for managing and running AI models**Service**: Commands for controlling the Foundry Local service**Cache**: Commands for managing your local model storage

## Model commands

The following table summarizes the commands related to managing and running models:

Note

You can specify the `model`

argument by its **alias** or **model ID**. Using an alias:

- Selects the best model for your available hardware automatically. For example, if you have an Nvidia GPU available, Foundry Local selects the best GPU model. If you have a supported NPU available, Foundry Local selects the NPU model.
- Lets you use a shorter name without needing to remember the model ID.

If you want to run a specific model, use the model ID. For example, to run the `qwen2.5-0.5b`

on CPU - irrespective of your available hardware - use: `foundry model run qwen2.5-0.5b-instruct-generic-cpu`

.

Command |
Description |
|---|---|
`foundry model --help` |
Displays all available model-related commands and their usage. |
`foundry model run <model>` |
Runs a specified model, downloads it if it isn't cached, and starts an interaction. |
`foundry model list` |
Lists all available models for local use. On first run, it downloads execution providers (EPs) for your hardware. |
`foundry model list --filter <key>=<value>` |
Lists models filtered by the specified criteria (device, task, alias, provider). |
`foundry model info <model>` |
Displays detailed information about a specific model. |
`foundry model info <model> --license` |
Displays the license information for a specific model. |
`foundry model download <model>` |
Downloads a model to the local cache without running it. |
`foundry model load <model>` |
Loads a model into the service. |
`foundry model unload <model>` |
Unloads a model from the service. |

### Model list ordering

When multiple model ID variants are available for an alias, the model list shows the models in priority order. The first model in the list is the model that runs when you specify the model by `alias`

.

### Model list filtering

The `foundry model list`

command supports filtering models by using the `--filter`

option. You can filter models based on a single attribute by using key-value pairs.

```
foundry model list --filter <key>=<value>
```


This command prints models that match the filter key and value.

Reference: [Model list filtering](#model-list-filtering)

Note

When you run `foundry model list`

for the first time after installation, Foundry Local automatically downloads the relevant execution providers (EPs) for your machine's hardware configuration. You see a progress bar indicating the download completion before the model list appears.

**Supported filter keys:**

#### device - Hardware Device Type

Filters models by the hardware device they run on.

**Possible values:**

`CPU`

- Central processing unit models`GPU`

- Graphics processing unit models`NPU`

- Neural processing unit models

#### provider - Execution Provider

Filters models by their execution provider or runtime.

**Possible values:**

`CPUExecutionProvider`

- CPU-based execution`CUDAExecutionProvider`

- NVIDIA CUDA GPU execution`WebGpuExecutionProvider`

- WebGPU execution`QNNExecutionProvider`

- Qualcomm Neural Network execution (NPU)`OpenVINOExecutionProvider`

- Intel OpenVINO execution`NvTensorRTRTXExecutionProvider`

- NVIDIA TensorRT execution`VitisAIExecutionProvider`

- AMD Vitis AI execution

#### task - Model Task Type

Filters models by their intended use case or task.

**Common values:**

`chat-completion`

: Conversational AI models`text-generation`

: Text generation models

#### alias - Model Alias

Filters models by their alias identifier. Supports wildcard matching with `*`

suffix.

**Sample values:**

`phi4-cpu`

`qwen2.5-coder-0.5b-instruct-generic-cpu`

`deepseek-r1-distill-qwen-1.5b-generic-cpu`

`phi-4-mini-instruct-generic-cpu`


### Special filter features

**Negation Support:** Prefix any value with `!`

to exclude matching models.

```
foundry model list --filter device=!GPU
```


This command excludes GPU models from the results.

Reference: [Special filter features](#special-filter-features)

**Wildcard Matching (alias only):** Append `*`

to match prefixes when filtering by alias.

```
foundry model list --filter alias=qwen*
```


This command returns models whose alias starts with `qwen`

.

Reference: [Special filter features](#special-filter-features)

### Examples

```
foundry model list --filter device=GPU
foundry model list --filter task=chat-completion
foundry model list --filter provider=CUDAExecutionProvider
```


These examples filter the model list by device, task, and execution provider.

Reference: [Model list filtering](#model-list-filtering)

Note

- All comparisons are case-insensitive.
- Only one filter can be used per command.
- Unrecognized filter keys result in an error.

## Service commands

The following table summarizes the commands related to managing and running the Foundry Local service:

Command |
Description |
|---|---|
`foundry service --help` |
Displays all available service-related commands and their usage. |
`foundry service start` |
Starts the Foundry Local service. |
`foundry service stop` |
Stops the Foundry Local service. |
`foundry service restart` |
Restarts the Foundry Local service. |
`foundry service status` |
Displays the current status of the Foundry Local service. |
`foundry service ps` |
Lists all models currently loaded in the Foundry Local service. |
`foundry service diag` |
Displays the logs of the Foundry Local service. |
`foundry service set <options>` |
Sets the configuration of the Foundry Local service. |

## Cache commands

The following table summarizes the commands for managing the local cache where models are stored:

Command |
Description |
|---|---|
`foundry cache --help` |
Shows all available cache-related commands and their usage. |
`foundry cache location` |
Shows the current cache directory. |
`foundry cache list` |
Lists all models stored in the local cache. |
`foundry cache cd <path>` |
Changes the cache directory to the specified path. |
`foundry cache remove <model>` |
Removes a model from the local cache. |

## Execution providers

Execution providers are hardware-specific acceleration libraries that run models as efficiently as possible on your device.

### Built-in execution providers

Foundry Local includes the CPU execution provider, the WebGPU execution provider, and the CUDA execution provider.

The CPU execution provider uses [Microsoft Linear Algebra Subroutines (MLAS)](https://github.com/microsoft/mlas) to run on any CPU and is the CPU fallback for Foundry Local.

The WebGPU execution provider uses [Dawn](https://github.com/google/dawn), the native implementation of the web-based API, for acceleration on any GPU, and is the GPU fallback for Foundry Local.

The CUDA execution provider uses NVIDIA CUDA for acceleration on NVIDIA GPUs. It requires an NVIDIA GeForce RTX 30 series and later with a minimum recommended driver version 32.0.15.5585 and CUDA version 12.5. It's subject to the following license terms: [License Agreement for NVIDIA Software Development Kits—EULA](https://docs.nvidia.com/cuda/eula/index.html).

### Plugin execution providers

The execution providers listed in the following table are available for dynamic download and registration on Windows, depending on device and driver compatibility. They're subject to the license terms specified.

Foundry Local automatically downloads these execution providers on first run. The plugin execution providers automatically update when new versions are available.

| Name (Vendor) | Requirements | License terms |
|---|---|---|
`NvTensorRTRTXExecutionProvider` (NVIDIA) |
NVIDIA GeForce RTX 30XX and later versions with minimum recommended driver version 32.0.15.5585 and CUDA version 12.5 |
|

`OpenVINOExecutionProvider`

(Intel)GPU: Intel AlderLake (12th Gen) and later versions with min recommended driver 32.0.101.1029

NPU: Intel ArrowLake (15th Gen) and later versions with min recommended driver 32.0.100.4239

[Intel OBL Distribution Commercial Use License Agreement v2025.02.12](https://cdrdv2.intel.com/v1/dl/getContent/849090?explicitVersion=true)`QNNExecutionProvider`

(Qualcomm)Snapdragon(R) X Plus - X1Pxxxxx - Qualcomm(R) Hexagon(TM) NPU with minimum driver version 30.0.140.0 and later versions

`VitisAIExecutionProvider`

(AMD)Max: Adrenalin Edition 25.9.1 with NPU driver 32.00.0203.297

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/reference/reference-rest -->

# Foundry Local REST API Reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

Caution

This API refers to the REST API available in the Foundry Local CLI. This API is under active development and may include breaking changes without notice. We strongly recommend monitoring the changelog before building production applications.

## POST /v1/chat/completions

This endpoint processes chat completion requests.

It's fully compatible with the [OpenAI Chat Completions API](https://platform.openai.com/docs/api-reference/chat/create).

**Request Body:**

*---Standard OpenAI Properties---*

`model`

(string)

The specific model to use for completion.`messages`

(array)

The conversation history as a list of messages.- Each message requires:
`role`

(string)

The message sender's role. Must be`system`

,`user`

, or`assistant`

.`content`

(string)

The actual message text.


- Each message requires:
`temperature`

(number, optional)

Controls randomness, ranging from 0 to 2. Higher values (0.8) create varied outputs, while lower values (0.2) create focused, consistent outputs.`top_p`

(number, optional)

Controls token selection diversity from 0 to 1. A value of 0.1 means only the tokens in the top 10% probability are considered.`n`

(integer, optional)

Number of alternative completions to generate for each input message.`stream`

(boolean, optional)

When true, sends partial message responses as server-sent events, ending with a`data: [DONE]`

message.`stop`

(string or array, optional)

Up to 4 sequences that will cause the model to stop generating further tokens.`max_tokens`

(integer, optional)

Maximum number of tokens to generate. For newer models, use`max_completion_tokens`

instead.`max_completion_tokens`

(integer, optional)

Maximum number of tokens the model can generate, including visible output and reasoning tokens.`presence_penalty`

(number, optional)

Value between -2.0 and 2.0. Positive values encourage the model to discuss new topics by penalizing tokens that have already appeared.`frequency_penalty`

(number, optional)

Value between -2.0 and 2.0. Positive values discourage repetition by penalizing tokens based on their frequency in the text.`logit_bias`

(map, optional)

Adjusts the probability of specific tokens appearing in the completion.`user`

(string, optional)

A unique identifier for your end-user that helps with monitoring and abuse prevention.`functions`

(array, optional)

Available functions for which the model can generate JSON inputs.- Each function must include:
`name`

(string)

Function name.`description`

(string)

Function description.`parameters`

(object)

Function parameters described as a JSON Schema object.


- Each function must include:
`function_call`

(string or object, optional)

Controls how the model responds to function calls.- If object, can include:
`name`

(string, optional)

The name of the function to call.`arguments`

(object, optional)

The arguments to pass to the function.


- If object, can include:
`metadata`

(object, optional)

A dictionary of metadata key-value pairs.`top_k`

(number, optional)

The number of highest probability vocabulary tokens to keep for top-k-filtering.`random_seed`

(integer, optional)

Seed for reproducible random number generation.`ep`

(string, optional)

Overwrite the provider for ONNX models. Supports:`"dml"`

,`"cuda"`

,`"qnn"`

,`"cpu"`

,`"webgpu"`

.`ttl`

(integer, optional)

Time to live in seconds for the model in memory.`tools`

(object, optional)

Tools calculated for the request.

**Response body:**

`id`

(string)

Unique identifier for the chat completion.`object`

(string)

The object type, always`"chat.completion"`

.`created`

(integer)

Creation timestamp in epoch seconds.`model`

(string)

The model used for completion.`choices`

(array)

List of completion choices, each containing:`index`

(integer)

The index of this choice.`message`

(object)

The generated message with:`role`

(string)

Always`"assistant"`

for responses.`content`

(string)

The actual generated text.

`finish_reason`

(string)

Why generation stopped (e.g.,`"stop"`

,`"length"`

,`"function_call"`

).

`usage`

(object)

Token usage statistics:`prompt_tokens`

(integer)

Tokens in the prompt.`completion_tokens`

(integer)

Tokens in the completion.`total_tokens`

(integer)

Total tokens used.


**Example:**

Request body

```
{
"model": "qwen2.5-0.5b-instruct-generic-cpu",
"messages": [
{
"role": "user",
"content": "Hello, how are you?"
}
],
"temperature": 0.7,
"top_p": 1,
"n": 1,
"stream": false,
"stop": null,
"max_tokens": 100,
"presence_penalty": 0,
"frequency_penalty": 0,
"logit_bias": {},
"user": "user_id_123",
"functions": [],
"function_call": null,
"metadata": {}
}
```


Response body

```
{
"id": "chatcmpl-1234567890",
"object": "chat.completion",
"created": 1677851234,
"model": "qwen2.5-0.5b-instruct-generic-cpu",
"choices": [
{
"index": 0,
"message": {
"role": "assistant",
"content": "I'm doing well, thank you! How can I assist you today?"
},
"finish_reason": "stop"
}
],
"usage": {
"prompt_tokens": 10,
"completion_tokens": 20,
"total_tokens": 30
}
}
```


## GET /openai/status

Get server status information.

**Response body:**

`Endpoints`

(array of strings)

The HTTP server binding endpoints.`ModelDirPath`

(string)

Directory where local models are stored.`PipeName`

(string)

The current NamedPipe server name.

**Example:**

Response body

```
{
"Endpoints": ["http://localhost:5272"],
"ModelDirPath": "/path/to/models",
"PipeName": "inference_agent"
}
```


## GET /foundry/list

Get a list of available Foundry Local models in the catalog.

**Response:**

`models`

(array)

Array of model objects. Each model includes:`name`

: The unique identifier for the model.`displayName`

: A human-readable name for the model, often the same as the name.`providerType`

: The type of provider hosting the model (for example, AzureFoundry).`uri`

: The resource URI pointing to the model's location in the registry.`version`

: The version number of the model.`modelType`

: The format or type of the model (for example, ONNX).`promptTemplate`

:`assistant`

: The template for the assistant's response.`prompt`

: The template for the user-assistant interaction.

`publisher`

: The entity or organization that published the model.`task`

: The primary task the model is designed to perform (for example, chat completion).`runtime`

:`deviceType`

: The type of hardware the model is designed to run on (for example, CPU).`executionProvider`

: The execution provider used for running the model.

`fileSizeMb`

: The size of the model file in megabytes.`modelSettings`

:`parameters`

: A list of configurable parameters for the model.

`alias`

: An alternative name or shorthand for the model`supportsToolCalling`

: Indicates whether the model supports tool-calling functionality.`license`

: The license type under which the model is distributed.`licenseDescription`

: A detailed description or link to the license terms.`parentModelUri`

: The URI of the parent model from which this model is derived.


## GET /openai/models

Get a list of cached models, including local and registered external models.

**Response:**

- 200 OK

An array of model names as strings.

**Example:**

Response body

```
["Phi-4-mini-instruct-generic-cpu", "phi-3.5-mini-instruct-generic-cpu"]
```


## POST /openai/download

Download a model from the catalog to local storage.

Note

Large model downloads can take a long time. Set a high timeout for this request to avoid early termination.

**Request Body:**

`model`

(`WorkspaceInferenceModel`

object)`Uri`

(string)

The model URI to download.`Name`

(string) The model name.`ProviderType`

(string, optional)

The provider type (for example,`"AzureFoundryLocal"`

,`"HuggingFace"`

).`Path`

(string, optional)

Remote path to the model files. For example, in a Hugging Face repository, this is the path to the model files.`PromptTemplate`

(`Dictionary<string, string>`

, optional)

Includes:`system`

(string, optional)

The template for the system message.`user`

(string, optional) The template for the user's message.`assistant`

(string, optional)

The template for the assistant's response.`prompt`

(string, optional)

The template for the user-assistant interaction.

`Publisher`

(string, optional)

The publisher of the model.

`token`

(string, optional)

Authentication token for protected models (GitHub or Hugging Face).`progressToken`

(object, optional)

For AITK only. Token to track download progress.`customDirPath`

(string, optional)

Custom download directory (used for CLI, not needed for AITK).`bufferSize`

(integer, optional)

HTTP download buffer size in KB. No effect on NIM or Azure Foundry models.`ignorePipeReport`

(boolean, optional)

If`true`

, forces progress reporting via HTTP stream instead of pipe. Defaults to`false`

for AITK and`true`

for Foundry Local.

**Streaming Response:**

During download, the server streams progress updates in the format:

```
("file name", percentage_complete)
```


**Final Response body:**

`Success`

(boolean)

Whether the download completed successfully.`ErrorMessage`

(string, optional)

Error details if download failed.

**Example:**

Request URI

```
POST /openai/download
```


Request body

Note that the version suffix must be supplied in the model name.

```
{
"model": {
"Uri": "azureml://registries/azureml/models/Phi-4-mini-instruct-generic-cpu/versions/4",
"ProviderType": "AzureFoundryLocal",
"Name": "Phi-4-mini-instruct-generic-cpu:4",
"Publisher": "",
"PromptTemplate": {
"system": "<|system|>{Content}<|end|>",
"user": "<|user|>{Content}<|end|>",
"assistant": "<|assistant|>{Content}<|end|>",
"prompt": "<|user|>{Content}<|end|><|assistant|>"
}
}
}
```


Response stream

```
("genai_config.json", 0.01)
("genai_config.json", 0.2)
("model.onnx.data", 0.5)
("model.onnx.data", 0.78)
...
("", 1)
```


Final response

```
{
"Success": true,
"ErrorMessage": null
}
```


## GET /openai/load/{name}

Load a model into memory for faster inference.

**URI Parameters:**

`name`

(string)

The model name to load.

**Query Parameters:**

`unload`

(boolean, optional)

Whether to automatically unload the model after idle time. Defaults to`true`

.`ttl`

(integer, optional)

Time to live in seconds. If it's greater than 0, this value overrides the`unload`

parameter.`ep`

(string, optional)

Execution provider to run this model. Supports:`"dml"`

,`"cuda"`

,`"qnn"`

,`"cpu"`

,`"webgpu"`

.

If not specified, uses settings from`genai_config.json`

.

**Response:**

- 200 OK

Empty response body

**Example:**

Request URI

```
GET /openai/load/Phi-4-mini-instruct-generic-cpu?ttl=3600&ep=dml
```


## GET /openai/unload/{name}

Unload a model from memory.

**URI Parameters:**

`name`

(string) The model name to unload.

**Query Parameters:**

`force`

(boolean, optional) If`true`

, ignores TTL settings and unloads immediately.

**Response:**

- 200 OK Empty response body

**Example:**

Request URI

```
GET /openai/unload/Phi-4-mini-instruct-generic-cpu?force=true
```


## GET /openai/unloadall

Unloads all models from memory.

**Response:**

- 200 OK

Empty response body

## GET /openai/loadedmodels

Get the list of currently loaded models.

**Response:**

- 200 OK

An array of model names as strings.

**Example:**

Response body

```
["Phi-4-mini-instruct-generic-cpu", "phi-3.5-mini-instruct-generic-cpu"]
```


## GET /openai/getgpudevice

Get the current GPU device ID.

**Response:**

- 200 OK

An integer representing the current GPU device ID.

## GET /openai/setgpudevice/{deviceId}

Set the active GPU device.

**URI Parameters:**

`deviceId`

(integer)

The GPU device ID to use.

**Response:**

- 200 OK

Empty response body

**Example:**

- Request URI
`GET /openai/setgpudevice/1`


## POST /v1/chat/completions/tokenizer/encode/count

Counts tokens for a given chat completion request without performing inference.

**Request Body:**

- Content-Type: application/json
- JSON object in
`ChatCompletionCreateRequest`

format with:`model`

(string)

Model to use for tokenization.`messages`

(array)

Array of message objects with`role`

and`content`

.


**Response Body:**

- Content-Type: application/json
- JSON object with token count:
`tokenCount`

(integer)

Number of tokens in the request.


**Example:**

Request body

```
{
"messages": [
{
"role": "system",
"content": "This is a system message"
},
{
"role": "user",
"content": "Hello, what is Microsoft?"
}
],
"model": "Phi-4-mini-instruct-cuda-gpu"
}
```


Response body

```
{
"tokenCount": 23
}
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/reference/reference-sdk -->

# Foundry Local SDK reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

The Foundry Local SDK simplifies AI model management in local environments by providing control plane operations separate from data plane inference code. This reference documents SDK implementations for Python, JavaScript, C#, and Rust.

## Python SDK Reference

### Prerequisites

- Install Foundry Local and ensure the
`foundry`

command is available on your`PATH`

. - Use Python 3.9 or later.

### Installation

Install the Python package:

```
pip install foundry-local-sdk
```


### Quickstart

Use this snippet to verify that the SDK can start the service and reach the local catalog.

```
from foundry_local import FoundryLocalManager
manager = FoundryLocalManager()
manager.start_service()
catalog = manager.list_catalog_models()
print(f"Catalog models available: {len(catalog)}")
```


This example prints a non-zero number when the service is running and the catalog is available.

References:

### FoundryLocalManager Class

The `FoundryLocalManager`

class provides methods to manage models, cache, and the Foundry Local service.

#### Initialization

```
from foundry_local import FoundryLocalManager
# Initialize and optionally bootstrap with a model
manager = FoundryLocalManager(alias_or_model_id=None, bootstrap=True)
```


`alias_or_model_id`

: (optional) Alias or Model ID to download and load at startup.`bootstrap`

: (default True) If True, starts the service if not running and loads the model if provided.

### A note on aliases

Many methods outlined in this reference have an `alias_or_model_id`

parameter in the signature. You can pass into the method either an **alias** or **model ID** as a value. Using an alias will:

- Select the
*best model*for the available hardware. For example, if a Nvidia CUDA GPU is available, Foundry Local selects the CUDA model. If a supported NPU is available, Foundry Local selects the NPU model. - Allow you to use a shorter name without needing to remember the model ID.

Tip

We recommend passing into the `alias_or_model_id`

parameter an **alias** because when you deploy your application, Foundry Local acquires the best model for the end user's machine at run-time.

Note

If you have an Intel NPU on Windows, ensure you have installed the [Intel NPU driver](https://www.intel.com/content/www/us/en/download/794734/intel-npu-driver-windows.html) for optimal NPU acceleration.

### Service Management

| Method | Signature | Description |
|---|---|---|
`is_service_running()` |
`() -> bool` |
Checks if the Foundry Local service is running. |
`start_service()` |
`() -> None` |
Starts the Foundry Local service. |
`service_uri` |
`@property -> str` |
Returns the service URI. |
`endpoint` |
`@property -> str` |
Returns the service endpoint. |
`api_key` |
`@property -> str` |
Returns the API key (from env or default). |

### Catalog Management

| Method | Signature | Description |
|---|---|---|
`list_catalog_models()` |
`() -> list[FoundryModelInfo]` |
Lists all available models in the catalog. |
`refresh_catalog()` |
`() -> None` |
Refreshes the model catalog. |
`get_model_info()` |
`(alias_or_model_id: str, raise_on_not_found=False) -> FoundryModelInfo \| None` |
Gets model info by alias or ID. |

### Cache Management

| Method | Signature | Description |
|---|---|---|
`get_cache_location()` |
`() -> str` |
Returns the model cache directory path. |
`list_cached_models()` |
`() -> list[FoundryModelInfo]` |
Lists models downloaded to the local cache. |

### Model Management

| Method | Signature | Description |
|---|---|---|
`download_model()` |
`(alias_or_model_id: str, token: str = None, force: bool = False) -> FoundryModelInfo` |
Downloads a model to the local cache. |
`load_model()` |
`(alias_or_model_id: str, ttl: int = 600) -> FoundryModelInfo` |
Loads a model into the inference server. |
`unload_model()` |
`(alias_or_model_id: str, force: bool = False) -> None` |
Unloads a model from the inference server. |
`list_loaded_models()` |
`() -> list[FoundryModelInfo]` |
Lists all models currently loaded in the service. |

### FoundryModelInfo

The methods `list_catalog_models()`

, `list_cached_models()`

, and `list_loaded_models()`

return a list of `FoundryModelInfo`

objects. You can use the information contained in this object to further refine the list. Or get the information for a model directly by calling the `get_model_info(alias_or_model_id)`

method.

These objects contain the following fields:

| Field | Type | Description |
|---|---|---|
`alias` |
`str` |
Alias of the model. |
`id` |
`str` |
Unique identifier of the model. |
`version` |
`str` |
Version of the model. |
`execution_provider` |
`str` |
The accelerator (
|

`device_type`

`DeviceType`

`uri`

`str`

`file_size_mb`

`int`

`supports_tool_calling`

`bool`

`prompt_template`

`dict \| None`

`provider`

`str`

`publisher`

`str`

`license`

`str`

`task`

`str`

`chat-completions`

or `automatic-speech-recognition`

.`ep_override`

`str \| None`

### Execution Providers

One of:

`CPUExecutionProvider`

- CPU-based execution`CUDAExecutionProvider`

- NVIDIA CUDA GPU execution`WebGpuExecutionProvider`

- WebGPU execution`QNNExecutionProvider`

- Qualcomm Neural Network execution (NPU)`OpenVINOExecutionProvider`

- Intel OpenVINO execution`NvTensorRTRTXExecutionProvider`

- NVIDIA TensorRT execution`VitisAIExecutionProvider`

- AMD Vitis AI execution

## Example Usage

The following code demonstrates how to use the `FoundryLocalManager`

class to manage models and interact with the Foundry Local service.

```
from foundry_local import FoundryLocalManager
# By using an alias, the most suitable model will be selected
# to your end-user's device.
alias = "qwen2.5-0.5b"
# Create a FoundryLocalManager instance. This will start the Foundry.
manager = FoundryLocalManager()
# List available models in the catalog
catalog = manager.list_catalog_models()
print(f"Available models in the catalog: {catalog}")
# Download and load a model
model_info = manager.download_model(alias)
model_info = manager.load_model(alias)
print(f"Model info: {model_info}")
# List models in cache
local_models = manager.list_cached_models()
print(f"Models in cache: {local_models}")
# List loaded models
loaded = manager.list_loaded_models()
print(f"Models running in the service: {loaded}")
# Unload a model
manager.unload_model(alias)
```


This example lists models, downloads and loads one model, and then unloads it.

References:

### Integrate with OpenAI SDK

Install the OpenAI package:

```
pip install openai
```


The following code demonstrates how to integrate the `FoundryLocalManager`

with the OpenAI SDK to interact with a local model.

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
messages=[{"role": "user", "content": "Why is the sky blue?"}],
stream=True
)
# Print the streaming response
for chunk in stream:
if chunk.choices[0].delta.content is not None:
print(chunk.choices[0].delta.content, end="", flush=True)
```


This example streams a chat completion response from the local model.

References:

## JavaScript SDK Reference

### Prerequisites

- Install Foundry Local and ensure the
`foundry`

command is available on your`PATH`

.

### Installation

Install the package from npm:

```
npm install foundry-local-sdk
```


### Quickstart

Use this snippet to verify that the SDK can start the service and reach the local catalog.

```
import { FoundryLocalManager } from "foundry-local-sdk";
const manager = new FoundryLocalManager();
await manager.startService();
const catalogModels = await manager.listCatalogModels();
console.log(`Catalog models available: ${catalogModels.length}`);
```


This example prints a non-zero number when the service is running and the catalog is available.

References:

### FoundryLocalManager Class

The `FoundryLocalManager`

class lets you manage models, control the cache, and interact with the Foundry Local service in both browser and Node.js environments.

#### Initialization

```
import { FoundryLocalManager } from "foundry-local-sdk";
const foundryLocalManager = new FoundryLocalManager();
```


Available options:

`host`

: Base URL of the Foundry Local service`fetch`

: (optional) Custom fetch implementation for environments like Node.js

### A note on aliases

Many methods outlined in this reference have an `aliasOrModelId`

parameter in the signature. You can pass into the method either an **alias** or **model ID** as a value. Using an alias will:

- Select the
*best model*for the available hardware. For example, if a Nvidia CUDA GPU is available, Foundry Local selects the CUDA model. If a supported NPU is available, Foundry Local selects the NPU model. - Allow you to use a shorter name without needing to remember the model ID.

Tip

We recommend passing into the `aliasOrModelId`

parameter an **alias** because when you deploy your application, Foundry Local acquires the best model for the end user's machine at run-time.

Note

If you have an Intel NPU on Windows, ensure you have installed the [Intel NPU driver](https://www.intel.com/content/www/us/en/download/794734/intel-npu-driver-windows.html) for optimal NPU acceleration.

### Service Management

| Method | Signature | Description |
|---|---|---|
`init()` |
`(aliasOrModelId?: string) => Promise<FoundryModelInfo \| void>` |
Initializes the SDK and optionally loads a model. |
`isServiceRunning()` |
`() => Promise<boolean>` |
Checks if the Foundry Local service is running. |
`startService()` |
`() => Promise<void>` |
Starts the Foundry Local service. |
`serviceUrl` |
`string` |
The base URL of the Foundry Local service. |
`endpoint` |
`string` |
The API endpoint (`serviceUrl` + `/v1` ). |
`apiKey` |
`string` |
The API key (none). |

### Catalog Management

| Method | Signature | Description |
|---|---|---|
`listCatalogModels()` |
`() => Promise<FoundryModelInfo[]>` |
Lists all available models in the catalog. |
`refreshCatalog()` |
`() => Promise<void>` |
Refreshes the model catalog. |
`getModelInfo()` |
`(aliasOrModelId: string, throwOnNotFound = false) => Promise<FoundryModelInfo \| null>` |
Gets model info by alias or ID. |

### Cache Management

| Method | Signature | Description |
|---|---|---|
`getCacheLocation()` |
`() => Promise<string>` |
Returns the model cache directory path. |
`listCachedModels()` |
`() => Promise<FoundryModelInfo[]>` |
Lists models downloaded to the local cache. |

### Model Management

| Method | Signature | Description |
|---|---|---|
`downloadModel()` |
`(aliasOrModelId: string, token?: string, force = false, onProgress?) => Promise<FoundryModelInfo>` |
Downloads a model to the local cache. |
`loadModel()` |
`(aliasOrModelId: string, ttl = 600) => Promise<FoundryModelInfo>` |
Loads a model into the inference server. |
`unloadModel()` |
`(aliasOrModelId: string, force = false) => Promise<void>` |
Unloads a model from the inference server. |
`listLoadedModels()` |
`() => Promise<FoundryModelInfo[]>` |
Lists all models currently loaded in the service. |

## Example Usage

The following code demonstrates how to use the `FoundryLocalManager`

class to manage models and interact with the Foundry Local service.

```
import { FoundryLocalManager } from "foundry-local-sdk";
// By using an alias, the most suitable model will be downloaded
// to your end-user's device.
// TIP: You can find a list of available models by running the
// following command in your terminal: `foundry model list`.
const alias = "qwen2.5-0.5b";
const manager = new FoundryLocalManager();
// Initialize the SDK and optionally load a model
const modelInfo = await manager.init(alias);
console.log("Model Info:", modelInfo);
// Check if the service is running
const isRunning = await manager.isServiceRunning();
console.log(`Service running: ${isRunning}`);
// List available models in the catalog
const catalog = await manager.listCatalogModels();
// Download and load a model
await manager.downloadModel(alias);
await manager.loadModel(alias);
// List models in cache
const localModels = await manager.listCachedModels();
// List loaded models
const loaded = await manager.listLoadedModels();
// Unload a model
await manager.unloadModel(alias);
```


This example downloads and loads a model, then lists cached and loaded models.

References:

## Integration with OpenAI Client

Install the OpenAI package:

```
npm install openai
```


The following code demonstrates how to integrate the `FoundryLocalManager`

with the OpenAI client to interact with a local model.

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


This example streams a chat completion response from the local model.

References:

## Browser Usage

The SDK includes a browser-compatible version where you must specify the host URL manually:

```
import { FoundryLocalManager } from "foundry-local-sdk/browser";
// Specify the service URL
// Run the Foundry Local service using the CLI: `foundry service start`
// and use the URL from the CLI output
const host = "HOST";
const manager = new FoundryLocalManager({ host });
// Note: The `init`, `isServiceRunning`, and `startService` methods
// are not available in the browser version
```


Note

The browser version doesn't support the `init`

, `isServiceRunning`

, and `startService`

methods. You must ensure that the Foundry Local service is running before using the SDK in a browser environment. You can start the service using the Foundry Local CLI: `foundry service start`

. You can glean the service URL from the CLI output.

#### Example Usage

```
import { FoundryLocalManager } from "foundry-local-sdk/browser";
// Specify the service URL
// Run the Foundry Local service using the CLI: `foundry service start`
// and use the URL from the CLI output
const host = "HOST";
const manager = new FoundryLocalManager({ host });
const alias = "qwen2.5-0.5b";
// Get all available models
const catalog = await manager.listCatalogModels();
console.log("Available models in catalog:", catalog);
// Download and load a specific model
await manager.downloadModel(alias);
await manager.loadModel(alias);
// View models in your local cache
const localModels = await manager.listCachedModels();
console.log("Cached models:", localModels);
// Check which models are currently loaded
const loaded = await manager.listLoadedModels();
console.log("Loaded models in inference service:", loaded);
// Unload a model when finished
await manager.unloadModel(alias);
```


References:

## C# SDK Reference

### Project setup guide

There are two NuGet packages for the Foundry Local SDK - a WinML and a cross-platform package - that have the same API surface but are optimized for different platforms:

**Windows**: Uses the`Microsoft.AI.Foundry.Local.WinML`

package that's specific to Windows applications, which uses the Windows Machine Learning (WinML) framework.**Cross-platform**: Uses the`Microsoft.AI.Foundry.Local`

package that can be used for cross-platform applications (Windows, Linux, macOS).

Depending on your target platform, follow these instructions to create a new C# application and add the necessary dependencies:

Use Foundry Local in your C# project by following these Windows-specific or Cross-Platform (macOS/Linux/Windows) instructions:

- Create a new C# project and navigate into it:
`dotnet new console -n app-name cd app-name`

- Open and edit the
`app-name.csproj`

file to:`<Project Sdk="Microsoft.NET.Sdk"> <PropertyGroup> <OutputType>Exe</OutputType> <TargetFramework>net9.0-windows10.0.26100</TargetFramework> <RootNamespace>app-name</RootNamespace> <ImplicitUsings>enable</ImplicitUsings> <Nullable>enable</Nullable> <WindowsAppSDKSelfContained>false</WindowsAppSDKSelfContained> <WindowsPackageType>None</WindowsPackageType> <EnableCoreMrtTooling>false</EnableCoreMrtTooling> </PropertyGroup> <ItemGroup> <PackageReference Include="Microsoft.AI.Foundry.Local.WinML" Version="0.8.2.1" /> <PackageReference Include="Microsoft.Extensions.Logging" Version="9.0.10" /> <PackageReference Include="OpenAI" Version="2.5.0" /> </ItemGroup> </Project>`

- Create a
`nuget.config`

file in the project root with the following content so that the packages restore correctly:`<?xml version="1.0" encoding="utf-8"?> <configuration> <packageSources> <clear /> <add key="nuget.org" value="https://api.nuget.org/v3/index.json" /> <add key="ORT" value="https://aiinfra.pkgs.visualstudio.com/PublicPackages/_packaging/ORT/nuget/v3/index.json" /> </packageSources> <packageSourceMapping> <packageSource key="nuget.org"> <package pattern="*" /> </packageSource> <packageSource key="ORT"> <package pattern="*Foundry*" /> </packageSource> </packageSourceMapping> </configuration>`


### Quickstart

Use this snippet to verify that the SDK can initialize and access the local model catalog.

```
using Microsoft.AI.Foundry.Local;
using Microsoft.Extensions.Logging;
using System.Linq;
var config = new Configuration
{
AppName = "app-name",
LogLevel = Microsoft.AI.Foundry.Local.LogLevel.Information,
};
using var loggerFactory = LoggerFactory.Create(builder =>
{
builder.SetMinimumLevel(Microsoft.Extensions.Logging.LogLevel.Information);
});
var logger = loggerFactory.CreateLogger<Program>();
await FoundryLocalManager.CreateAsync(config, logger);
var manager = FoundryLocalManager.Instance;
var catalog = await manager.GetCatalogAsync();
var models = await catalog.ListModelsAsync();
Console.WriteLine($"Models available: {models.Count()}");
```


This example prints the number of models available for your hardware.

References:

### Redesign

To improve your ability to ship applications using on-device AI, there are substantial changes to the architecture of the C# SDK in version `0.8.0`

and later. In this section, we outline the key changes to help you migrate your applications to the latest version of the SDK.

Note

In the SDK version `0.8.0`

and later, there are breaking changes in the API from previous versions.

The following diagram shows how the previous architecture - for versions earlier than `0.8.0`

- relied heavily on using a REST webserver to manage models and inference like chat completions:

The SDK would use a Remote Procedural Call (RPC) to find Foundry Local CLI executable on the machine, start the webserver, and then communicate with it over HTTP. This architecture had several limitations, including:

- Complexity in managing the webserver lifecycle.
- Challenging deployment: End users needed to have the Foundry Local CLI installed on their machines
*and*your application. - Version management of the CLI and SDK could lead to compatibility issues.

To address these issues, the redesigned architecture in version `0.8.0`

and later uses a more streamlined approach. The new architecture is as follows:

In this new architecture:

- Your application is
**self-contained**. It doesn't require the Foundry Local CLI to be installed separately on the end user's machine making it easier for you to deploy applications. - The REST
**web server is**. You can still use the web server if you want to integrate with other tools that communicate over HTTP. Read*optional*[Use chat completions via REST server with Foundry Local](../how-to/how-to-integrate-with-inference-sdks?view=foundry-classic)for details on how to use this feature. - The SDK has
**native support for chat completions and audio transcriptions**, allowing you to build conversational AI applications with fewer dependencies. Read[Use Foundry Local native chat completions API](../how-to/how-to-use-native-chat-completions?view=foundry-classic)for details on how to use this feature. - On Windows devices, you can use a Windows ML build that handles
**hardware acceleration**for models on the device by pulling in the right runtime and drivers.

#### API changes

Version `0.8.0`

and later provides a more object-orientated and composable API. The main entry point continues to be the `FoundryLocalManager`

class, but instead of being a flat set of methods that operate via static calls to a stateless HTTP API, the SDK now exposes methods on the `FoundryLocalManager`

instance that maintain state about the service and models.

| Primitive | Versions < 0.8.0 | Versions >= 0.8.0 |
|---|---|---|
Configuration |
N/A | `config = Configuration(...)` |
Get Manager |
`mgr = FoundryLocalManager();` |
`await FoundryLocalManager.CreateAsync(config, logger);` `var mgr = FoundryLocalManager.Instance;` |
Get Catalog |
N/A | `catalog = await mgr.GetCatalogAsync();` |
List Models |
`mgr.ListCatalogModelsAsync();` |
`catalog.ListModelsAsync();` |
Get Model |
`mgr.GetModelInfoAsync("aliasOrModelId");` |
`catalog.GetModelAsync(alias: "alias");` |
Get Variant |
N/A | `model.SelectedVariant;` |
Set Variant |
N/A | `model.SelectVariant();` |
Download a model |
`mgr.DownloadModelAsync("aliasOrModelId");` |
`model.DownloadAsync()` |
Load a model |
`mgr.LoadModelAsync("aliasOrModelId");` |
`model.LoadAsync()` |
Unload a model |
`mgr.UnloadModelAsync("aliasOrModelId");` |
`model.UnloadAsync()` |
List loaded models |
`mgr.ListLoadedModelsAsync();` |
`catalog.GetLoadedModelsAsync();` |
Get model path |
N/A | `model.GetPathAsync()` |
Start service |
`mgr.StartServiceAsync();` |
`mgr.StartWebServerAsync();` |
Stop service |
`mgr.StopServiceAsync();` |
`mgr.StopWebServerAsync();` |
Cache location |
`mgr.GetCacheLocationAsync();` |
`config.ModelCacheDir` |
List cached models |
`mgr.ListCachedModelsAsync();` |
`catalog.GetCachedModelsAsync();` |

The API allows Foundry Local to be more configurable over the web server, logging, cache location, and model variant selection. For example, the `Configuration`

class allows you to set up the application name, logging level, web server URLs, and directories for application data, model cache, and logs:

```
var config = new Configuration
{
AppName = "app-name",
LogLevel = Microsoft.AI.Foundry.Local.LogLevel.Information,
Web = new Configuration.WebService
{
Urls = "http://127.0.0.1:55588"
},
AppDataDir = "./foundry_local_data",
ModelCacheDir = "{AppDataDir}/model_cache",
LogsDir = "{AppDataDir}/logs"
};
```


References:

In the previous version of the Foundry Local C# SDK, you couldn't configure these settings directly through the SDK, which limited your ability to customize the behavior of the service.

### Reduce application package size

The Foundry Local SDK pulls in `Microsoft.ML.OnnxRuntime.Foundry`

NuGet package as a dependency. The `Microsoft.ML.OnnxRuntime.Foundry`

package provides the *inference runtime bundle*, which is the set of libraries required to efficiently run inference on specific vendor hardware devices. The inference runtime bundle includes the following components:

**ONNX Runtime library**: The core inference engine (`onnxruntime.dll`

).**ONNX Runtime Execution Provider (EP) library**. A hardware-specific backend in ONNX Runtime that optimizes and executes parts of a machine learning model a hardware accelerator. For example:- CUDA EP:
`onnxruntime_providers_cuda.dll`

- QNN EP:
`onnxruntime_providers_qnn.dll`


- CUDA EP:
**Independent Hardware Vendor (IHV) libraries**. For example:- WebGPU: DirectX dependencies (
`dxcompiler.dll`

,`dxil.dll`

) - QNN: Qualcomm QNN dependencies (
`QnnSystem.dll`

, etc.)

- WebGPU: DirectX dependencies (

The following table summarizes what EP and IHV libraries are bundled with your application and what WinML will download/install at runtime:

In all platforms and architectures, the CPU EP is required. The WebGPU EP and IHV libraries are small in size (for example, WebGPU only adds ~7MB to your application package) and are required in Windows and macOS. However, the CUDA and QNN EPs are large in size (for example, CUDA adds ~1GB to your application package) so we recommend excluding these EPs from your application package. WinML will download/install CUDA and QNN at runtime if the end user has compatible hardware.

Note

We're working on removing the CUDA and QNN EPs from the `Microsoft.ML.OnnxRuntime.Foundry`

package in future releases so that you don't need to include an `ExcludeExtraLibs.props`

file to remove them from your application package.

To reduce the size of your application package, you can create an `ExcludeExtraLibs.props`

file in your project directory with the following content, which excludes the CUDA and QNN EP and IHV libraries when you publish your application:

```
<Project>
<!-- we want to ensure we're using the onnxruntime libraries from Foundry Local Core so
we delete the WindowsAppSdk versions once they're unzipped. -->
<Target Name="ExcludeOnnxRuntimeLibs" AfterTargets="ExtractMicrosoftWindowsAppSDKMsixFiles">
<Delete Files="$(MicrosoftWindowsAppSDKMsixContent)\onnxruntime.dll"/>
<Delete Files="$(MicrosoftWindowsAppSDKMsixContent)\onnxruntime_providers_shared.dll"/>
<Message Importance="Normal" Text="Deleted onnxruntime libraries from $(MicrosoftWindowsAppSDKMsixContent)." />
</Target>
<!-- Remove CUDA EP and IHV libraries on Windows x64 -->
<Target Name="ExcludeCudaLibs" Condition="'$(RuntimeIdentifier)'=='win-x64'" AfterTargets="ResolvePackageAssets">
<ItemGroup>
<!-- match onnxruntime*cuda.* (we're matching %(Filename) which excludes the extension) -->
<NativeCopyLocalItems Remove="@(NativeCopyLocalItems)"
Condition="$([System.Text.RegularExpressions.Regex]::IsMatch('%(Filename)',
'^onnxruntime.*cuda.*', RegexOptions.IgnoreCase))" />
</ItemGroup>
<Message Importance="Normal" Text="Excluded onnxruntime CUDA libraries from package." />
</Target>
<!-- Remove QNN EP and IHV libraries on Windows arm64 -->
<Target Name="ExcludeQnnLibs" Condition="'$(RuntimeIdentifier)'=='win-arm64'" AfterTargets="ResolvePackageAssets">
<ItemGroup>
<NativeCopyLocalItems Remove="@(NativeCopyLocalItems)"
Condition="$([System.Text.RegularExpressions.Regex]::IsMatch('%(Filename)%(Extension)',
'^QNN.*\.dll', RegexOptions.IgnoreCase))" />
<NativeCopyLocalItems Remove="@(NativeCopyLocalItems)"
Condition="$([System.Text.RegularExpressions.Regex]::IsMatch('%(Filename)',
'^libQNNhtp.*', RegexOptions.IgnoreCase))" />
<NativeCopyLocalItems Remove="@(NativeCopyLocalItems)"
Condition="'%(FileName)%(Extension)' == 'onnxruntime_providers_qnn.dll'" />
</ItemGroup>
<Message Importance="Normal" Text="Excluded onnxruntime QNN libraries from package." />
</Target>
<!-- need to manually copy on linux-x64 due to the nuget packages not having the correct props file setup -->
<ItemGroup Condition="'$(RuntimeIdentifier)' == 'linux-x64'">
<!-- 'Update' as the Core package will add these dependencies, but we want to be explicit about the version -->
<PackageReference Update="Microsoft.ML.OnnxRuntime.Gpu" />
<PackageReference Update="Microsoft.ML.OnnxRuntimeGenAI.Cuda" />
<OrtNativeLibs Include="$(NuGetPackageRoot)microsoft.ml.onnxruntime.gpu.linux/$(OnnxRuntimeVersion)/runtimes/$(RuntimeIdentifier)/native/*" />
<OrtGenAINativeLibs Include="$(NuGetPackageRoot)microsoft.ml.onnxruntimegenai.cuda/$(OnnxRuntimeGenAIVersion)/runtimes/$(RuntimeIdentifier)/native/*" />
</ItemGroup>
<Target Name="CopyOrtNativeLibs" AfterTargets="Build" Condition=" '$(RuntimeIdentifier)' == 'linux-x64'">
<Copy SourceFiles="@(OrtNativeLibs)" DestinationFolder="$(OutputPath)"></Copy>
<Copy SourceFiles="@(OrtGenAINativeLibs)" DestinationFolder="$(OutputPath)"></Copy>
</Target>
</Project>
```


In your project file (`.csproj`

), add the following line to import the `ExcludeExtraLibs.props`

file:

```
<!-- other project file content -->
<Import Project="ExcludeExtraLibs.props" />
```


#### Windows: CUDA dependencies

The CUDA EP is pulled into your Linux application via `Microsoft.ML.OnnxRuntime.Foundry`

, but we don't include the IHV libraries. If you want to allow your end users with CUDA-enabled devices to benefit from higher performance, you need *add* the following CUDA IHV libraries to your application:

- CUBLAS v12.8.4 (
[download from NVIDIA Developer](https://developer.download.nvidia.com/compute/cuda/redist/libcublas/windows-x86_64/libcublas-windows-x86_64-12.8.4.1-archive.zip))- cublas64_12.dll
- cublasLt64_12.dll

- CUDA RT v12.8.90 (
[download from NVIDIA Developer](https://developer.download.nvidia.com/compute/cuda/redist/cuda_cudart/windows-x86_64/cuda_cudart-windows-x86_64-12.8.90-archive.zip))- cudart64_12.dll

- CUDNN v9.8.0 (
[download from NVIDIA Developer](https://developer.download.nvidia.com/compute/cudnn/redist/cudnn/windows-x86_64/cudnn-windows-x86_64-9.8.0.87_cuda12-archive.zip))- cudnn_graph64_9.dll
- cudnn_ops64_9.dll
- cudnn64_9.dll

- CUDA FFT v11.3.3.83 (
[download from NVIDIA Developer](https://developer.download.nvidia.com/compute/cuda/redist/libcufft/windows-x86_64/libcufft-windows-x86_64-11.3.3.83-archive.zip))- cufft64_11.dll


Warning

Adding the CUDA EP and IHV libraries to your application increase the size of your application package by 1GB.

### Samples

- For sample applications that demonstrate how to use the Foundry Local C# SDK, see the
[Foundry Local C# SDK Samples GitHub repository](https://aka.ms/foundrylocalSDK).

### API reference

- For more details on the Foundry Local C# SDK read
[Foundry Local C# SDK API Reference](https://aka.ms/fl-csharp-api-ref).

## Rust SDK reference

The Rust SDK for Foundry Local provides a way to manage models, control the cache, and interact with the Foundry Local service.

### Prerequisites

- Install Foundry Local and ensure the
`foundry`

command is available on your`PATH`

. - Use Rust 1.70.0 or later.

### Installation

To use the Foundry Local Rust SDK, add the following to your `Cargo.toml`

:

```
[dependencies]
foundry-local = "0.1.0"
```


Alternatively, you can add the Foundry Local crate using `cargo`

:

```
cargo add foundry-local
```


### Quickstart

Use this snippet to verify that the SDK can start the service and read the local catalog.

```
use anyhow::Result;
use foundry_local::FoundryLocalManager;
#[tokio::main]
async fn main() -> Result<()> {
let mut manager = FoundryLocalManager::builder().bootstrap(true).build().await?;
let models = manager.list_catalog_models().await?;
println!("Catalog models available: {}", models.len());
Ok(())
}
```


This example prints a non-zero number when the service is running and the catalog is available.

References:

`FoundryLocalManager`


Manager for Foundry Local SDK operations.

#### Fields

`service_uri: Option<String>`

— URI of the Foundry service.`client: Option<HttpClient>`

— HTTP client for API requests.`catalog_list: Option<Vec<FoundryModelInfo>>`

— Cached list of catalog models.`catalog_dict: Option<HashMap<String, FoundryModelInfo>>`

— Cached dictionary of catalog models.`timeout: Option<u64>`

— Optional HTTP client timeout.

#### Methods

`pub fn builder() -> FoundryLocalManagerBuilder`


Create a new builder for`FoundryLocalManager`

.`pub fn service_uri(&self) -> Result<&str>`


Get the service URI.

**Returns:**URI of the Foundry service.`fn client(&self) -> Result<&HttpClient>`


Get the HTTP client instance.

**Returns:**HTTP client.`pub fn endpoint(&self) -> Result<String>`


Get the endpoint for the service.

**Returns:**Endpoint URL.`pub fn api_key(&self) -> String`


Get the API key for authentication.

**Returns:**API key.`pub fn is_service_running(&mut self) -> bool`


Check if the service is running and set the service URI if found.

**Returns:**`true`

if running,`false`

otherwise.`pub fn start_service(&mut self) -> Result<()>`


Start the Foundry Local service.`pub async fn list_catalog_models(&mut self) -> Result<&Vec<FoundryModelInfo>>`


Get a list of available models in the catalog.`pub fn refresh_catalog(&mut self)`


Refresh the catalog cache.`pub async fn get_model_info(&mut self, alias_or_model_id: &str, raise_on_not_found: bool) -> Result<FoundryModelInfo>`


Get model information by alias or ID.

**Arguments:**`alias_or_model_id`

: Alias or Model ID.`raise_on_not_found`

: If true, error if not found.

`pub async fn get_cache_location(&self) -> Result<String>`


Get the cache location as a string.`pub async fn list_cached_models(&mut self) -> Result<Vec<FoundryModelInfo>>`


List cached models.`pub async fn download_model(&mut self, alias_or_model_id: &str, token: Option<&str>, force: bool) -> Result<FoundryModelInfo>`


Download a model.

**Arguments:**`alias_or_model_id`

: Alias or Model ID.`token`

: Optional authentication token.`force`

: Force re-download if already cached.

`pub async fn load_model(&mut self, alias_or_model_id: &str, ttl: Option<i32>) -> Result<FoundryModelInfo>`


Load a model for inference.

**Arguments:**`alias_or_model_id`

: Alias or Model ID.`ttl`

: Optional time-to-live in seconds.

`pub async fn unload_model(&mut self, alias_or_model_id: &str, force: bool) -> Result<()>`


Unload a model.

**Arguments:**`alias_or_model_id`

: Alias or Model ID.`force`

: Force unload even if in use.

`pub async fn list_loaded_models(&mut self) -> Result<Vec<FoundryModelInfo>>`


List loaded models.

`FoundryLocalManagerBuilder`


Builder for creating a `FoundryLocalManager`

instance.

#### Fields

`alias_or_model_id: Option<String>`

— Alias or model ID to download and load.`bootstrap: bool`

— Whether to start the service if not running.`timeout_secs: Option<u64>`

— HTTP client timeout in seconds.

#### Methods

`pub fn new() -> Self`


Create a new builder instance.`pub fn alias_or_model_id(mut self, alias_or_model_id: impl Into<String>) -> Self`


Set the alias or model ID to download and load.`pub fn bootstrap(mut self, bootstrap: bool) -> Self`


Set whether to start the service if not running.`pub fn timeout_secs(mut self, timeout_secs: u64) -> Self`


Set the HTTP client timeout in seconds.`pub async fn build(self) -> Result<FoundryLocalManager>`


Build the`FoundryLocalManager`

instance.

`FoundryModelInfo`


Represents information about a model.

#### Fields

`alias: String`

— The model alias.`id: String`

— The model ID.`version: String`

— The model version.`runtime: ExecutionProvider`

— The execution provider (CPU, CUDA, etc.).`uri: String`

— The model URI.`file_size_mb: i32`

— Model file size in MB.`prompt_template: serde_json::Value`

— Prompt template for the model.`provider: String`

— Provider name.`publisher: String`

— Publisher name.`license: String`

— License type.`task: String`

— Model task (e.g., text-generation).

#### Methods

`from_list_response(response: &FoundryListResponseModel) -> Self`


Creates a`FoundryModelInfo`

from a catalog response.`to_download_body(&self) -> serde_json::Value`


Converts the model info to a JSON body for download requests.

`ExecutionProvider`


Enum for supported execution providers.

`CPU`

`WebGPU`

`CUDA`

`QNN`


##### Methods

`get_alias(&self) -> String`


Returns a string alias for the execution provider.

`ModelRuntime`


Describes the runtime environment for a model.

`device_type: DeviceType`

`execution_provider: ExecutionProvider`
