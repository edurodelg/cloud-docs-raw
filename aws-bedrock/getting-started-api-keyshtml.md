---
source_url: https://docs.aws.amazon.com/bedrock/latest/userguide/getting-started-api-keys.html
fetched_at: 2026-01-25T03:10:40.454249
---

# Get started with Amazon Bedrock API keys: Generate a 30-day key and make your first API call

This tutorial walks you through creating a long-term Amazon Bedrock API key that expires in 30 days and using it to make a simple [Converse](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_Converse.html) API call using Python. This is the fastest way to start experimenting with Amazon Bedrock without setting up complex AWS credentials.

###### Warning

Long-term API keys are recommended only for exploration and development of Amazon Bedrock. For production applications, use [alternatives to long-term access keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/security-creds-programmatic-access.html#security-creds-alternatives-to-long-term-access-keys) such as IAM roles or temporary credentials.

Follow these steps to create a long-term Amazon Bedrock API key that expires in 30 days:

-
Sign in to the AWS Management Console with an IAM identity that has permissions to use the Amazon Bedrock console. Then, open the Amazon Bedrock console at

[https://console.aws.amazon.com/bedrock](https://console.aws.amazon.com/bedrock). -
In the left navigation pane, select

**API keys**. -
In the

**Long-term API keys**tab, choose**Generate long-term API keys**. -
In the

**API key expiration**section, select**30 days**. -
Choose

**Generate**. The key you generate provides permissions to carry out core Amazon Bedrock actions, as defined in the attached[AmazonBedrockLimitedAccess](./security-iam-awsmanpol.html#security-iam-awsmanpol-AmazonBedrockLimitedAccess)policy. -
Copy the generated API key and store it securely. You'll need this key for the next step.

###### Important

The API key is only displayed once. Make sure to copy and save it before closing the dialog. Remember that your API key will expire in 30 days. You can generate a new one by following the same steps, or consider transitioning to more secure authentication methods for ongoing use.

-
Set the API key as an environment variable by replacing

`${api-key}`

with your generated API key value and use it to generate a response in your method of choice:

Congratulations! You've successfully generated an Amazon Bedrock API key and made your first API call to the Amazon Bedrock service. After exploring some more Amazon Bedrock actions, you should transition to more secure methods of authentication such as short-term Amazon Bedrock API keys or AWS-wide temporary credentials. Refer to the following resources to learn more:

-
**Explore different models**– Learn about other foundation models available in Amazon Bedrock at[Amazon Bedrock foundation model information](./foundation-models-reference.html)and change the`model_id`

in your code to try them out. -
**Learn about model inference**– Learn about generating responses with model inference by reading about concepts and the options available in Amazon Bedrock at[Submit prompts and generate responses with model inference](./inference.html). -
**Plan for production with more secure authentication methods**– Read about Amazon Bedrock API keys in greater detail at[Generate Amazon Bedrock API keys to easily authenticate to the Amazon Bedrock API](./api-keys.html)and how to create more secure, short-term Amazon Bedrock API keys. When you're ready to build production applications, you should also review[alternatives to long-term access keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/security-creds-programmatic-access.html#security-creds-alternatives-to-long-term-access-keys)for more secure options that also allow access to other AWS services.