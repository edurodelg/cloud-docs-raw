---
source_url: https://docs.aws.amazon.com/bedrock/latest/userguide/foundation-models-reference.html
fetched_at: 2026-01-25T03:11:55.476769
---

# Amazon Bedrock foundation model information

A foundation model is an Artificial Intelligence model with a large number of parameters
and trained on a massive amount of diverse data. A foundation model can generate a variety
of responses for a wide range of use cases. Foundation models can generate text or image,
and can also convert input into *embeddings*. This section provides
information about the foundation models (FM) that you can use in Amazon Bedrock, such as the
features that models support and the AWS Regions in which models are available. For
information about the foundation models that Amazon Bedrock supports, see [Supported foundation models in Amazon Bedrock](./models-supported.html).

Access to all Amazon Bedrock foundation models is enabled by default. To get started, simply select a model from the model catalog in the Amazon Bedrock console and open it in the playground. For Anthropic models, first-time users may need to submit use case details before they can access the model. Once you have selected a model, you can then use it in the following ways.

-
[Run inference](./inference.html)by sending prompts to a model and generating responses. The[playgrounds](./playgrounds.html)offer a user-friendly interface in the AWS Management Console for generating text, images, or chats. See the**Output modality**column to determine the models you can use in each playground.###### Note

The console playgrounds don't support running inference on embeddings models. Use the API to run inference on embeddings models.

-
[Evaluate models](./evaluation.html)to compare outputs and determine the best model for your use-case. -
[Set up a knowledge base](./knowledge-base.html)with the help of an embeddings model. Then use a text model to generate responses to queries. -
[Create an agent](./agents.html)and use a model to run inference on prompts to carry out orchestration. -
[Customize a model](./custom-models.html)by feeding training and validation data to adjust model parameters for your use-case. To use a customized model, you must purchase[Provisioned Throughput](./prov-throughput.html)for it. -
[Purchase Provisioned Throughput](./prov-throughput.html)for a model to increase throughput for it.

To use an FM with the Amazon Bedrock API, you need to determine the appropriate **model ID** to use. Refer to the following table to determine where to find the model ID that you need to use.

| Use case | How to find the model ID |
|---|---|
| Use a base model | Look up the ID in the
|

[supported inference profiles](./inference-profiles-support.html)page`modelId`

in the [CreateProvisionedModelThroughput](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_CreateProvisionedModelThroughput.html)request.`modelId`

in the [CreateProvisionedModelThroughput](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_CreateProvisionedModelThroughput.html)request.`provisionedModelArn`

. This ARN is the model ID.[Purchase Provisioned Throughput](./prov-throughput.html)for the custom model and use the returned`provisionedModelArn`

as the model ID.For example code, see the documentation
for the feature you are using and also [Code examples for Amazon Bedrock using AWS SDKs](./service_code_examples.html).