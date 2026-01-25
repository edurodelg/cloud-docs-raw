---
source_url: https://docs.aws.amazon.com/bedrock/latest/userguide/api-keys-modify.html
fetched_at: 2026-01-25T03:11:30.476382
---

# Modify permissions for long-term and short-term Amazon Bedrock API keys

When you generate a long-term Amazon Bedrock API key, you create an IAM user associated with the key. To change the permissions associated with the key, modify permissions for the IAM user through the IAM service. For more information, see [Adding and removing IAM identity permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage-attach-detach.html) in the IAM User Guide.

###### Note

If you generated the long-term key in the AWS Management Console, the [AmazonBedrockLimitedAccess](./security-iam-awsmanpol.html#security-iam-awsmanpol-AmazonBedrockLimitedAccess) is attached to it by default. If you plan to modify permissions, remove this policy first before setting custom permissions.

## Example of modifying permissions for API keys

The following procedure shows how you can replace the [AmazonBedrockLimitedAccess](./security-iam-awsmanpol.html#security-iam-awsmanpol-AmazonBedrockLimitedAccess) with a more restrictive one:

-
Sign in to the AWS Management Console with an IAM identity that has permissions to use the Amazon Bedrock console. Then, open the Amazon Bedrock console at

[https://console.aws.amazon.com/bedrock](https://console.aws.amazon.com/bedrock). -
From the left navigation pane, select

**API keys**. -
Select the

**Long-term API keys**tab. -
Select your API key and choose

**Manage in IAM Console**. -
Select the

**Permissions**tab, choose the**AmazonBedrockLimitedAccess**policy, and choose**Remove**.###### Note

At this point, you've removed all permissions from the APi key and you won't be able to do anything with it.

-
In the

**Permissions policies**section, select**Create inline policy**from the**Add permissions**dropdown. -
In the

**Policy editor**, select**JSON**. Then paste the following policy into the editor: -
Choose

**Next**, provide a**Policy name**, and then choose**Create policy**. -
With this API key, a user now can only run inference with the US Anthropic Claude 3 Haiku inference profile in US West (Oregon).