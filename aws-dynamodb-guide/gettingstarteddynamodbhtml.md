---
source_url: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GettingStartedDynamoDB.html
fetched_at: 2026-01-28T07:13:36.420756
---

# Getting started with DynamoDB

You’ll learn how to connect to, create, and manage DynamoDB tables in the following sections.

Before you begin, you should familiarize yourself with the basic concepts in Amazon DynamoDB.
You can get a quick overview in [What is Amazon DynamoDB?](./Introduction.html)
and a more in-depth look in [Core components of Amazon DynamoDB](./HowItWorks.CoreComponents.html). Then, continue on to [Prerequisites](#GettingStarted.SettingUp.DynamoWebService).

###### Note

When you sign up for AWS, you can get started with DynamoDB using the [AWS Free Tier](https://aws.amazon.com/free/). If you have not already
exceeded the free tier benefits for Amazon DynamoDB, it won't cost you anything to complete
the examples in this section. Otherwise, you'll incur the standard DynamoDB usage fees from
the time that you create the tables until you delete the tables.

If you don't want to sign up for a free tier account, you can set up [DynamoDB local (downloadable version)](./DynamoDBLocal.html) on your computer.
The downloadable version lets you develop and test applications locally without signing
up for an AWS account or accessing the DynamoDB web service.

###### Topics

## Prerequisites

Before starting the Amazon DynamoDB tutorial, learn about the ways you can access DynamoDB in
[Accessing DynamoDB](./AccessingDynamoDB.html). Then, set up
DynamoDB through either the web service or the locally downloaded version in [ Setting up DynamoDB ](./SettingUp.html). After
that, continue on to [Step 1: Create a table in DynamoDB](./getting-started-step-1.html).

###### Note

-
If you plan to interact with DynamoDB only through the AWS Management Console, you don't need an AWS access key. Complete the steps in

[Signing up for AWS](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/SettingUp.DynamoWebService.html#SettingUp.DynamoWebService.SignUpForAWS), and then continue on to[Step 1: Create a table in DynamoDB](./getting-started-step-1.html). -
If you don't want to sign up for a free tier account, you can set up

[DynamoDB local (downloadable version)](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBLocal.html). Then continue on to[Step 1: Create a table in DynamoDB](./getting-started-step-1.html). -
There are differences when working with CLI commands in terminals on Linux and Windows. The following guide presents commands formatted for Linux terminals (this includes macOS), and commands formatted for Windows CMD. Choose the command that best fits the terminal application you are using.