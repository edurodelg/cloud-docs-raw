---
source_url: https://docs.aws.amazon.com/bedrock/latest/userguide/models-supported.html
fetched_at: 2026-01-25T02:05:29.375364
---

# Supported foundation models in Amazon Bedrock

The table below lists information for foundation models supported by Amazon Bedrock. The following list describes the columns in the table:

-
**Provider**– The model provider. -
**Model**– The name of the foundation model. -
**Model ID**– The AWS Region-agnostic ID of the model. Used in inference operations. -
**Single-region model support**– The AWS Regions that support inference calls to the model in that single Region. For more information, see[Submit prompts and generate responses with model inference](./inference.html). -
**Cross-region inference profile support**– The AWS Regions that support inference calls to multiple Regions within the same geographical area. For more information, see[Supported Regions and models for inference profiles](./inference-profiles-support.html). -
**Input modalities**– The modalities that can be provided as input to the model in inference. -
**Output modalities**– The modalities that can be output from the model in inference. -
**Streaming**– Whether the model supports streaming operations, such as[InvokeModelWithResponseStream](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_InvokeModelWithResponseStream.html)and[ConverseStream](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_ConverseStream.html). -
**Inference parameters**– A link to the inference parameters that you can specify when invoking the model.

| Provider | Model | Model ID | Single-region model support | Cross-region inference profile support | Input modalities | Output modalities | Streaming | Inference parameters |
|---|---|---|---|---|---|---|---|---|
| AI21 Labs | Jamba 1.5 Large | ai21.jamba-1-5-large-v1:0 |
us-east-1 |
Text |
Text |
Yes |
|

us-east-1

Text

Text

[Link](./model-parameters-jamba.html)us-east-1

Text

Image

Audio

Video

Embedding

[Link](https://docs.aws.amazon.com/nova/latest/userguide/getting-started-schema.html)ap-east-2

ap-northeast-1

ap-northeast-2

ap-south-1

ap-southeast-1

ap-southeast-2

ap-southeast-3

ap-southeast-4

ap-southeast-5

ap-southeast-7

ca-central-1

ca-west-1

eu-central-1

eu-north-1

eu-south-1

eu-south-2

eu-west-1

eu-west-2

eu-west-3

il-central-1

me-central-1

us-east-1

us-east-2

us-west-1

us-west-2

Text

Image

Video

Text

ap-northeast-1

eu-north-1

us-east-1

us-west-2

Speech

Speech

Text

ap-northeast-1

eu-west-1

us-east-1

Text

Image

Image

[Link](https://docs.aws.amazon.com/nova/latest/userguide/image-gen-req-resp-structure.html)ap-northeast-1

ap-southeast-2

ap-southeast-3

eu-north-1

eu-west-2

me-central-1

us-east-1

us-gov-west-1

ap-east-2

ap-northeast-1

ap-northeast-2

ap-south-1

ap-southeast-1

ap-southeast-2

ap-southeast-3

ap-southeast-4

ap-southeast-5

ap-southeast-7

ca-central-1

ca-west-1

eu-central-1

eu-north-1

eu-south-1

eu-south-2

eu-west-1

eu-west-3

il-central-1

me-central-1

us-east-1

us-east-2

us-west-1

us-west-2

Text

Image

Video

Text

[Link](https://docs.aws.amazon.com/nova/latest/userguide/getting-started-schema.html)ap-southeast-2

eu-west-2

us-east-1

us-gov-west-1

ap-east-2

ap-northeast-1

ap-northeast-2

ap-south-1

ap-southeast-1

ap-southeast-2

ap-southeast-3

ap-southeast-5

ap-southeast-7

eu-central-1

eu-north-1

eu-south-1

eu-south-2

eu-west-1

eu-west-3

il-central-1

me-central-1

us-east-1

us-east-2

us-west-2

Text

Text

[Link](https://docs.aws.amazon.com/nova/latest/userguide/getting-started-schema.html)us-east-1

us-east-2

us-west-2

Text

Image

Video

Text

[Link](https://docs.aws.amazon.com/nova/latest/userguide/getting-started-schema.html)ap-southeast-2

ap-southeast-3

eu-west-2

me-central-1

us-east-1

us-gov-west-1

ap-east-2

ap-northeast-1

ap-northeast-2

ap-south-1

ap-southeast-1

ap-southeast-2

ap-southeast-3

ap-southeast-4

ap-southeast-5

ap-southeast-7

eu-central-1

eu-north-1

eu-south-1

eu-south-2

eu-west-1

eu-west-3

il-central-1

me-central-1

us-east-1

us-east-2

us-west-1

us-west-2

Text

Image

Video

Text

[Link](https://docs.aws.amazon.com/nova/latest/userguide/getting-started-schema.html)ap-northeast-1

eu-west-1

us-east-1

Text

Image

Video

[Link](https://docs.aws.amazon.com/nova/latest/userguide/video-gen-access.html)us-east-1

Text

Image

Video

[Link](https://docs.aws.amazon.com/nova/latest/userguide/video-gen-access.html)ap-northeast-1

eu-north-1

us-east-1

Speech

Speech

Text

[Link](https://docs.aws.amazon.com/nova/latest/userguide/video-gen-access.html)ap-northeast-1

ca-central-1

eu-central-1

us-west-2

Text

Text

ap-northeast-1

eu-central-1

us-east-1

us-west-2

Text

Embedding

[Link](./model-parameters-titan-embed-text.html)us-east-1

us-west-2

Text

Image

Image

[Link](./model-parameters-titan-image.html)ap-south-1

ap-southeast-2

ca-central-1

eu-central-1

eu-west-1

eu-west-2

eu-west-3

sa-east-1

us-east-1

us-west-2

Text

Image

Embedding

[Link](./model-parameters-titan-embed-mm.html)ap-northeast-1

ap-northeast-2

ap-northeast-3

ap-south-1

ap-south-2

ap-southeast-2

ca-central-1

eu-central-1

eu-central-2

eu-north-1

eu-south-1

eu-south-2

eu-west-1

eu-west-2

eu-west-3

sa-east-1

us-east-1

us-east-2

us-west-2

us-gov-west-1

us-gov-east-1

Text

Embedding

[Link](./model-parameters-titan-embed-text.html)us-east-1

us-west-2

Text

Embedding

us-east-1

us-west-2

Text

Text

[Link](./model-parameters-titan-text.html)ap-northeast-1

ap-northeast-2

ap-south-1

ap-southeast-1

ap-southeast-2

ca-central-1

eu-central-1

eu-central-2

eu-west-1

eu-west-2

eu-west-3

me-central-1

sa-east-1

us-east-1

us-west-2

us-gov-west-1

eu-central-1

us-east-2

us-gov-east-1

Text

Image

Text

[Link](./model-parameters-claude.html)me-central-1

us-west-2

us-east-1

us-east-2

Text

Text

[Link](./model-parameters-claude.html)ap-northeast-1

ap-northeast-2

ap-northeast-3

ap-south-1

ap-south-2

ap-southeast-1

ap-southeast-2

ap-southeast-3

ap-southeast-4

ca-central-1

eu-central-1

eu-central-2

eu-north-1

eu-south-1

eu-south-2

eu-west-1

eu-west-2

eu-west-3

me-central-1

sa-east-1

us-east-1

us-east-2

us-west-1

us-west-2

Text

Image

Text

[Link](./model-parameters-claude.html)me-central-1

us-east-1

us-east-2

us-west-2

Text

Image

Text

[Link](./model-parameters-claude.html)ap-northeast-1

ap-northeast-2

ap-northeast-3

ap-south-1

ap-south-2

ap-southeast-1

ap-southeast-2

ap-southeast-3

ap-southeast-4

ca-central-1

eu-central-1

eu-central-2

eu-north-1

eu-south-1

eu-south-2

eu-west-1

eu-west-2

eu-west-3

me-central-1

sa-east-1

us-east-1

us-east-2

us-west-1

us-west-2

Text

Image

Text

[Link](./model-parameters-claude.html)af-south-1

ap-northeast-1

ap-northeast-2

ap-northeast-3

ap-south-1

ap-south-2

ap-southeast-1

ap-southeast-2

ap-southeast-3

ap-southeast-4

ca-central-1

ca-west-1

eu-central-1

eu-central-2

eu-north-1

eu-south-1

eu-south-2

eu-west-1

eu-west-2

eu-west-3

me-south-1

mx-central-1

sa-east-1

us-east-1

us-east-2

us-west-1

us-west-2

us-gov-west-1

us-gov-east-1

Text

Image

Text

[Link](./model-parameters-claude.html)ap-east-2

ap-northeast-1

ap-northeast-2

ap-northeast-3

ap-south-1

ap-south-2

ap-southeast-1

ap-southeast-2

ap-southeast-3

ap-southeast-4

ap-southeast-5

ap-southeast-7

eu-central-1

eu-north-1

eu-south-1

eu-south-2

eu-west-1

eu-west-3

il-central-1

me-central-1

us-east-1

us-east-2

us-west-1

us-west-2

Text

Image

Text

[Link](./model-parameters-claude.html)us-east-1

us-west-2

Text

Text

[Link](./model-parameters-cohere-command-r-plus.html)us-east-1

us-west-2

Text

Text

[Link](./model-parameters-cohere-command-r-plus.html)ap-northeast-1

ap-south-1

ap-southeast-1

ap-southeast-2

ca-central-1

eu-central-1

eu-west-1

eu-west-2

eu-west-3

sa-east-1

us-east-1

us-west-2

Text

Embedding

[Link](./model-parameters-embed.html)ap-northeast-1

ap-south-1

ap-southeast-1

ap-southeast-2

ca-central-1

eu-central-1

eu-west-1

eu-west-2

eu-west-3

sa-east-1

us-east-1

us-west-2

Text

Embedding

[Link](./model-parameters-embed.html)ap-northeast-1

eu-west-1

us-east-1

ap-northeast-1

ap-northeast-2

ap-northeast-3

ap-south-1

ap-south-2

ap-southeast-1

ap-southeast-2

ap-southeast-3

ap-southeast-4

ca-central-1

eu-central-1

eu-central-2

eu-north-1

eu-south-1

eu-south-2

eu-west-1

eu-west-2

eu-west-3

me-central-1

sa-east-1

us-east-1

us-east-2

us-west-1

us-west-2

Text

Image

Embedding

[Link](./model-parameters-embed.html)ap-northeast-1

ca-central-1

eu-central-1

us-east-1

us-west-2

Text

Text

[Link](https://docs.cohere.com/reference/rerank)us-east-1

us-east-2

us-west-2

Text

Text

[Link](https://www.deepseek.com/)ap-northeast-1

ap-south-1

ap-southeast-3

eu-north-1

eu-west-2

us-east-2

us-west-2

Text

Text

[Link](https://www.deepseek.com/)ap-northeast-1

ap-south-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Image

Text

ap-northeast-1

ap-south-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Image

Text

ap-northeast-1

ap-south-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Image

Text

us-west-2

Text

Video

[Link](https://lumalabs.ai/learning-hub)ap-south-1

ca-central-1

eu-west-2

us-east-1

us-west-2

us-gov-west-1

Text

Text

[Link](./model-parameters-meta.html)ap-south-1

ca-central-1

eu-west-2

us-east-1

us-west-2

us-gov-west-1

Text

Text

[Link](./model-parameters-meta.html)us-west-2

us-east-2

Text

Text

[Link](./model-parameters-meta.html)us-west-2

us-east-1

us-east-2

us-west-2

Text

Text

[Link](./model-parameters-meta.html)us-west-2

us-east-1

us-east-2

us-west-2

Text

Text

[Link](./model-parameters-meta.html)us-east-1

us-east-2

us-west-2

Text

Image

Text

[Link](./model-parameters-meta.html)eu-central-1

eu-west-1

eu-west-3

us-east-1

us-east-2

us-west-2

Text

Text

[Link](./model-parameters-meta.html)eu-central-1

eu-west-1

eu-west-3

us-east-1

us-east-2

us-west-2

Text

Text

[Link](./model-parameters-meta.html)us-east-1

us-east-2

us-west-2

Text

Image

Text

[Link](./model-parameters-meta.html)us-east-2

us-east-1

us-east-2

us-west-2

Text

Text

[Link](./model-parameters-meta.html)us-east-1

us-east-2

us-west-1

us-west-2

Text

Image

Text

[Link](./model-parameters-meta.html)us-east-1

us-east-2

us-west-1

us-west-2

Text

Image

Text

[Link](./model-parameters-meta.html)ap-northeast-1

ap-south-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Text

ap-northeast-1

ap-south-1

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Image

Text

ap-northeast-1

ap-south-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Text

ap-northeast-1

ap-south-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Text

ap-northeast-1

ap-south-1

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Text

ap-south-1

ap-southeast-2

ca-central-1

eu-west-1

eu-west-2

eu-west-3

sa-east-1

us-east-1

us-west-2

Text

Text

[Link](./model-parameters-mistral.html)ap-south-1

ap-southeast-2

ca-central-1

eu-west-1

eu-west-2

eu-west-3

sa-east-1

us-east-1

us-west-2

Text

Text

[Link](./model-parameters-mistral.html)us-west-2

Text

Text

[Link](./model-parameters-mistral.html)ap-northeast-1

ap-south-1

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Image

Text

us-east-1

Text

Text

[Link](./model-parameters-mistral.html)ap-south-1

ap-southeast-2

ca-central-1

eu-west-1

eu-west-2

eu-west-3

sa-east-1

us-east-1

us-west-2

Text

Text

[Link](./model-parameters-mistral.html)eu-central-1

eu-north-1

eu-west-1

eu-west-3

us-east-1

us-east-2

us-west-2

Text

Image

Text

[Link](./model-parameters-mistral.html)ap-northeast-1

ap-south-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Speech

Text

Text

ap-northeast-1

ap-south-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Speech

Text

Text

ap-northeast-1

ap-south-1

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Text

ap-northeast-1

ap-south-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Image

Text

ap-northeast-1

ap-south-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Text

ap-northeast-1

ap-south-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Text

ap-northeast-1

ap-south-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Text

ap-northeast-1

ap-south-1

ap-southeast-3

eu-central-1

eu-north-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Text

[Link](./model-parameters-openai.html)ap-northeast-1

ap-south-1

ap-southeast-3

eu-central-1

eu-north-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Text

[Link](./model-parameters-openai.html)ap-northeast-1

ap-south-1

ap-southeast-3

eu-central-1

eu-north-1

eu-south-1

eu-west-2

us-east-2

us-west-2

Text

Text

[Link](https://www.alibabacloud.com)ap-northeast-1

ap-south-1

ap-southeast-3

eu-central-1

eu-north-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Text

[Link](https://www.alibabacloud.com)ap-northeast-1

ap-south-1

ap-southeast-3

eu-north-1

eu-west-2

us-east-2

us-west-2

Text

Text

[Link](https://www.alibabacloud.com)ap-northeast-1

ap-south-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Text

ap-northeast-1

ap-south-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Image

Text

ap-northeast-1

ap-south-1

ap-southeast-3

eu-central-1

eu-north-1

eu-south-1

eu-west-1

eu-west-2

sa-east-1

us-east-1

us-east-2

us-west-2

Text

Text

[Link](https://www.alibabacloud.com)us-west-2

Text

Image

Image

[Link](./model-parameters-stability-diffusion.html)us-east-1

us-east-2

us-west-2

Text

Image

Image

[Link](./stable-image-services.html)us-east-1

us-east-2

us-west-2

Text

Image

Image

[Link](./model-parameters-stability-diffusion.html)us-east-1

us-east-2

us-west-2

Text

Image

Image

[Link](./model-parameters-stability-diffusion.html)us-west-2

Text

Image

[Link](./model-parameters-stability-diffusion.html)us-east-1

us-east-2

us-west-2

Text

Image

Image

[Link](./stable-image-services.html)us-east-1

us-east-2

us-west-2

Text

Image

Image

[Link](./model-parameters-stability-diffusion.html)us-east-1

us-east-2

us-west-2

Text

Image

Image

[Link](./stable-image-services.html)us-east-1

us-east-2

us-west-2

Text

Image

Image

[Link](./model-parameters-stability-diffusion.html)us-east-1

us-east-2

us-west-2

Text

Image

Image

[Link](./stable-image-services.html)us-east-1

us-east-2

us-west-2

Text

Image

Image

[Link](./model-parameters-stability-diffusion.html)us-east-1

us-east-2

us-west-2

Text

Image

Image

[Link](./model-parameters-stability-diffusion.html)us-east-1

us-east-2

us-west-2

Text

Image

Image

[Link](./model-parameters-stability-diffusion.html)us-east-1

us-east-2

us-west-2

Text

Image

Image

[Link](./model-parameters-stability-diffusion.html)us-east-1

us-east-2

us-west-2

Text

Image

Image

[Link](./model-parameters-stability-diffusion.html)us-west-2

Text

Image

[Link](./model-parameters-stability-diffusion.html)ap-northeast-2

us-east-1

eu-west-1

us-east-1

Text

Image

Speech

Video

Embedding

[Link](./model-parameters-marengo.html)ap-northeast-2

eu-west-1

us-east-1

Text

Image

Speech

Video

Embedding

[Link](./model-parameters-marengo.html)ap-northeast-2

us-east-1

af-south-1

ap-east-2

ap-northeast-1

ap-northeast-2

ap-northeast-3

ap-south-1

ap-south-2

ap-southeast-1

ap-southeast-2

ap-southeast-3

ap-southeast-4

ap-southeast-5

ap-southeast-7

ca-central-1

ca-west-1

eu-central-1

eu-central-2

eu-north-1

eu-south-1

eu-south-2

eu-west-1

eu-west-2

eu-west-3

il-central-1

me-central-1

me-south-1

mx-central-1

sa-east-1

us-east-1

us-east-2

us-west-1

us-west-2

Text

Video

Text

[Link](./model-parameters-pegasus.html)us-east-1

us-east-2

us-west-1

us-west-2

Text

Text

[Link](./model-parameters-writer-palmyra.html)us-east-1

us-east-2

us-west-1

us-west-2

Text

Text

[Link](./model-parameters-writer-palmyra.html)The following models are also supported by Amazon Bedrock:

| Provider | Model | Model ID |
|---|---|---|
| Qwen | Qwen3 Next 80B A3B Instruct | qwen.qwen3-next-80b-a3b |
| Qwen | Qwen3 VL 235B A22B | qwen.qwen3-vl-235b-a22b |
| OpenAI | GPT OSS Safeguard 20B | openai.gpt-oss-safeguard-20b |
| OpenAI | GPT OSS Safeguard 120B | openai.gpt-oss-safeguard-120b |
| Gemma 3 4B IT | google.gemma-3-4b-it | |
| Gemma 3 12B IT | google.gemma-3-12b-it | |
| Gemma 3 27B IT | google.gemma-3-27b-it | |
| MiniMax | MiniMax M2 | minimax.minimax-m2 |
| Moonshot AI | Kimi K2 Thinking | moonshot.kimi-k2-thinking |
| NVIDIA | NVIDIA Nemotron Nano 9B v2 | nvidia.nemotron-nano-9b-v2 |
| NVIDIA | NVIDIA Nemotron Nano 12B v2 VL BF16 | nvidia.nemotron-nano-12b-v2 |
| Mistral AI | Magistral Small 2509 | mistral.magistral-small-2509 |
| Mistral AI | Voxtral Mini 3B 2507 | mistral.voxtral-mini-3b-2507 |
| Mistral AI | Voxtral Small 24B 2507 | mistral.voxtral-small-24b-2507 |
| Mistral | Ministral 3B | mistral.ministral-3-3b-instruct |
| Mistral | Ministral 3 8B | mistral.ministral-3-8b-instruct |
| Mistral | Ministral 3 14B | mistral.ministral-3-14b-instruct |
| Mistral | Mistral Large 3 | mistral.mistral-large-3-675b-instruct |

Certain models have a targeted date for deprecation. For more information, see [Model lifecycle](./model-lifecycle.html).

To learn more about a provider, navigate to the following links: