---
merged_at: 2026-01-25T15:32:35.923694
merged_files: 3
---

# Documentos Fusionados

Este archivo contiene 3 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/ -->

# Foundry Local (preview) documentation

Safely design, customize, and manage AI applications and agents on-device.

This browser is no longer supported.

Upgrade to Microsoft Edge to take advantage of the latest features, security updates, and technical support.

Safely design, customize, and manage AI applications and agents on-device.


---

<!-- DOCUMENTO FUSIONADO: what-is-foundry-local.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/what-is-foundry-local -->

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

<!-- DOCUMENTO FUSIONADO: get-started.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/get-started -->

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
