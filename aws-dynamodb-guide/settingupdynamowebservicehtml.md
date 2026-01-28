---
source_url: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/SettingUp.DynamoWebService.html
fetched_at: 2026-01-28T07:13:56.542978
---

# Setting up DynamoDB (web service)

To use the Amazon DynamoDB web service:

-
[Get an AWS access key](#SettingUp.DynamoWebService.GetCredentials)(used to access DynamoDB programmatically).###### Note

If you plan to interact with DynamoDB only through the AWS Management Console, you don't need an AWS access key, and you can skip ahead to

[Using the console](./AccessingDynamoDB.html#ConsoleDynamoDB). -
[Configure your credentials](#SettingUp.DynamoWebService.ConfigureCredentials)(used to access DynamoDB programmatically).

## Signing up for AWS

To use the DynamoDB service, you must have an AWS account. If you don't already have an account, you are prompted to create one when you sign up. You're not charged for any AWS services that you sign up for unless you use them.

###### To sign up for AWS

Follow the online instructions.

Part of the sign-up procedure involves receiving a phone call or text message and entering a verification code on the phone keypad.

When you sign up for an AWS account, an

*AWS account root user*is created. The root user has access to all AWS services and resources in the account. As a security best practice, assign administrative access to a user, and use only the root user to perform[tasks that require root user access](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html#root-user-tasks).

## Granting programmatic access

Before you can access DynamoDB programmatically or through the AWS Command Line Interface (AWS CLI), you must have programmatic access. You don't need programmatic access if you plan to use the DynamoDB console only.

Users need programmatic access if they want to interact with AWS outside of the AWS Management Console. The way to grant programmatic access depends on the type of user that's accessing AWS.

To grant users programmatic access, choose one of the following options.

| Which user needs programmatic access? | To | By |
|---|---|---|
| IAM | (Recommended) Use console credentials as temporary credentials to sign programmatic requests to the AWS CLI, AWS SDKs, or AWS APIs. |
Following the instructions for the interface that you want to use.
|
|
Workforce identity (Users managed in IAM Identity Center) |
Use temporary credentials to sign programmatic requests to the AWS CLI, AWS SDKs, or AWS APIs. |
Following the instructions for the interface that you want to use.
|
| IAM | Use temporary credentials to sign programmatic requests to the AWS CLI, AWS SDKs, or AWS APIs. | Following the instructions in
IAM User Guide. |

(Not recommended)

Use long-term credentials to sign programmatic requests to the AWS CLI, AWS SDKs, or AWS APIs.Following the instructions for the interface that you want to use.

-
For the AWS CLI, see

[Authenticating using IAM user credentials](https://docs.aws.amazon.com//cli/latest/userguide/cli-authentication-user.html)in the*AWS Command Line Interface User Guide*. -
For AWS SDKs and tools, see

[Authenticate using long-term credentials](https://docs.aws.amazon.com//sdkref/latest/guide/access-iam-users.html)in the*AWS SDKs and Tools Reference Guide*. -
For AWS APIs, see

[Managing access keys for IAM users](https://docs.aws.amazon.com//IAM/latest/UserGuide/id_credentials_access-keys.html)in the*IAM User Guide*.

## Configuring your credentials

Before you can access DynamoDB programmatically or through the AWS CLI, you must configure your credentials to enable authorization for your applications.

There are several ways to do this. For example, you can manually create the
credentials file to store your access key ID and secret access key. You also can use
the AWS CLI command `aws configure`

to automatically create the file.
Alternatively, you can use environment variables. For more information about
configuring your credentials, see the programming-specific AWS SDK developer
guide.

To install and configure the AWS CLI, see [Using the AWS CLI](./AccessingDynamoDB.html#Tools.CLI).

## Integrating with other DynamoDB services

You can integrate DynamoDB with many other AWS services. For more information, see the following: