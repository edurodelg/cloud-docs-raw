---
source_url: https://docs.aws.amazon.com/bedrock/latest/userguide/models-get-info.html
fetched_at: 2026-01-25T02:05:23.189865
---

# Get information about foundation models

In the Amazon Bedrock console, you can find overarching information about Amazon Bedrock foundation model providers and the models they provide in the **Providers** and **Base models** sections.

Use the API to retrieve information about Amazon Bedrock foundation model, including its ARN, model ID, modalities and features it supports, and whether it is deprecated or not, in a [FoundationModelSummary](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_FoundationModelSummary.html) object.

-
To return information about all the foundation models that Amazon Bedrock provides, send a

[ListFoundationModels](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_ListFoundationModels.html)request.###### Note

The response also returns model IDs that aren't in the

[base model ID](./models-supported.html)or base model IDs for Provisioned Throughput charts. These model IDs are deprecated or for backwards compability. -
To return information about a specific foundation model, send a

[GetFoundationModel](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_GetFoundationModel.html)request, specifying the[model ID](./models-supported.html).

Choose a tab to see code examples in an interface or language.