---
source_url: https://docs.aws.amazon.com/bedrock/latest/userguide/getting-started-console.html
fetched_at: 2026-01-25T02:03:52.933842
---

# Get started in the Amazon Bedrock console

This section describes how to use the [playgrounds](./playgrounds.html) in the AWS console to submit a text prompt to an Amazon Bedrock foundation model (FM) and generate a text or image response. Before you run the following examples, you should check that you have fulfilled the following prerequisites:

**Prerequisites**

-
You have an AWS account and have permissions to access a role in that account with the necessary permissions for Amazon Bedrock. Otherwise, follow the steps at

[I already have an AWS account](./getting-started.html#getting-started-bedrock-role). -
You're in the US East (N. Virginia) (us-east-1) Region. To change Regions, choose the Region name at the top right of the console, next to your IAM role. Then select US East (N. Virginia) (us-east-1).


## Explore the text playground

The following example demonstrates how to use the text playground:

-
Sign in to the AWS Management Console with an IAM identity that has permissions to use the Amazon Bedrock console. Then, open the Amazon Bedrock console at

[https://console.aws.amazon.com/bedrock](https://console.aws.amazon.com/bedrock). -
From the left navigation pane, choose

**Text**under**Playgrounds**. -
Choose

**Select model**and select a provider and model. For this example, we will select**Amazon Titan Text G1 - Lite**. Then choose**Apply** -
Select a default prompt from below the text panel, or enter a prompt into the text panel, such as

`Describe the purpose of a "hello world" program in one line`

. -
Choose

**Run**to run inference on the model. The generated text appears below your prompt in the text panel.

## Explore the image playground

The following example demonstrates how to use the image playground.

-
Sign in to the AWS Management Console with an IAM identity that has permissions to use the Amazon Bedrock console. Then, open the Amazon Bedrock console at

[https://console.aws.amazon.com/bedrock](https://console.aws.amazon.com/bedrock). -
From the left navigation pane, choose

**Image**under**Playgrounds**. -
Choose

**Select model**and select a provider and model. For this example, we will select**Amazon Titan Image Generator G1 V1**. Then choose**Apply** -
Select a default prompt from below the text panel, or enter a prompt into the text panel, such as

`Generate an image of happy cats`

. -
In the

**Configurations**pane, change the**Number of images**to`1`

. -
Choose

**Run**to run inference on the model. The generated image appears above the prompt.