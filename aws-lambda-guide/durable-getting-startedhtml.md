---
source_url: https://docs.aws.amazon.com/lambda/latest/dg/durable-getting-started.html
fetched_at: 2026-01-30T23:32:41.593054
---

# Creating Lambda durable functions

To get started with Lambda durable functions, use the Lambda console to create a durable function. In a few minutes, you can create and deploy a durable function that uses steps and waits to demonstrate checkpoint-based execution.

As you carry out the tutorial, you'll learn fundamental durable function concepts, like how to use the `DurableContext`

object,
create checkpoints with steps, and pause execution with waits. You'll also learn how replay works when your function resumes after a wait.

To keep things simple, you create your function using either the Python or Node.js runtime. With these interpreted languages, you can edit function code directly in the console's built-in code editor.

###### Note

Durable functions currently support Python and Node.js (JavaScript/TypeScript) runtimes. For a complete list of supported runtime versions and container image options, see [Supported runtimes for durable functions](./durable-supported-runtimes.html).

###### Tip

To learn how to build **serverless solutions**, check out the [Serverless Developer Guide](https://docs.aws.amazon.com/serverless/latest/devguide/).

## Prerequisites

If you do not have an AWS account, complete the following steps to create one.

###### To sign up for an AWS account

Follow the online instructions.

Part of the sign-up procedure involves receiving a phone call or text message and entering a verification code on the phone keypad.

When you sign up for an AWS account, an

*AWS account root user*is created. The root user has access to all AWS services and resources in the account. As a security best practice, assign administrative access to a user, and use only the root user to perform[tasks that require root user access](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html#root-user-tasks).

AWS sends you a confirmation email after the sign-up process is
complete. At any time, you can view your current account activity and manage your account by
going to [https://aws.amazon.com/](https://aws.amazon.com/) and choosing

**My Account**.

After you sign up for an AWS account, secure your AWS account root user, enable AWS IAM Identity Center, and create an administrative user so that you don't use the root user for everyday tasks.

###### Secure your AWS account root user

-
Sign in to the

[AWS Management Console](https://console.aws.amazon.com/)as the account owner by choosing**Root user**and entering your AWS account email address. On the next page, enter your password.For help signing in by using root user, see

[Signing in as the root user](https://docs.aws.amazon.com/signin/latest/userguide/console-sign-in-tutorials.html#introduction-to-root-user-sign-in-tutorial)in the*AWS Sign-In User Guide*. -
Turn on multi-factor authentication (MFA) for your root user.

For instructions, see

[Enable a virtual MFA device for your AWS account root user (console)](https://docs.aws.amazon.com/IAM/latest/UserGuide/enable-virt-mfa-for-root.html)in the*IAM User Guide*.

###### Create a user with administrative access

-
Enable IAM Identity Center.

For instructions, see

[Enabling AWS IAM Identity Center](https://docs.aws.amazon.com//singlesignon/latest/userguide/get-set-up-for-idc.html)in the*AWS IAM Identity Center User Guide*. -
In IAM Identity Center, grant administrative access to a user.

For a tutorial about using the IAM Identity Center directory as your identity source, see

[Configure user access with the default IAM Identity Center directory](https://docs.aws.amazon.com//singlesignon/latest/userguide/quick-start-default-idc.html)in the*AWS IAM Identity Center User Guide*.

###### Sign in as the user with administrative access

-
To sign in with your IAM Identity Center user, use the sign-in URL that was sent to your email address when you created the IAM Identity Center user.

For help signing in using an IAM Identity Center user, see

[Signing in to the AWS access portal](https://docs.aws.amazon.com/signin/latest/userguide/iam-id-center-sign-in-tutorial.html)in the*AWS Sign-In User Guide*.

###### Assign access to additional users

-
In IAM Identity Center, create a permission set that follows the best practice of applying least-privilege permissions.

For instructions, see

[Create a permission set](https://docs.aws.amazon.com//singlesignon/latest/userguide/get-started-create-a-permission-set.html)in the*AWS IAM Identity Center User Guide*. -
Assign users to a group, and then assign single sign-on access to the group.

For instructions, see

[Add groups](https://docs.aws.amazon.com//singlesignon/latest/userguide/addgroups.html)in the*AWS IAM Identity Center User Guide*.

## Create a Lambda durable function with the console

In this example, your durable function processes an order through multiple steps with automatic checkpointing. The function takes a JSON object containing an order ID, validates the order, processes payment, and confirms the order. Each step is automatically checkpointed, so if the function is interrupted, it resumes from the last completed step.

Your function also demonstrates a wait operation, pausing execution for a short period to simulate waiting for external confirmation.

###### To create a durable function with the console

Open the

[Functions page](https://console.aws.amazon.com/lambda/home#/functions)of the Lambda console.-
Choose

**Create function**. -
Select

**Author from scratch**. -
In the

**Basic information**pane, for**Function name**, enter

.`myDurableFunction`

-
For

**Runtime**, choose either**Node.js 24**or**Python 3.14**. -
Select

**Enable durable execution**.

Lambda creates your durable function with an [execution role](./lambda-intro-execution-role.html) that includes permissions for
checkpoint operations (`lambda:CheckpointDurableExecutions`

and `lambda:GetDurableExecutionState`

).

###### Note

Lambda runtimes include the Durable Execution SDK, so you can test durable functions without packaging dependencies. However, we recommend including the SDK in your deployment package for production. This ensures version consistency and avoids potential runtime updates that might affect your function.

Use the console's built-in code editor to add your durable function code.

## Invoke the durable function using the console code editor

When no explicit version is specified (or published), the console invokes the durable function using the `$LATEST`

version qualifier.
However, for deterministic execution of your code, you must always use a qualified ARN pointing to a stable version.

###### To publish a version of your function

-
Choose the

**Versions**tab. -
Choose

**Publish new version**. -
For

**Version description**, enter`Initial version`

(optional). -
Choose

**Publish**. -
Lambda creates version 1 of your function. Note that the function ARN now includes

`:1`

at the end, indicating this is version 1.

Now create a test event to send to your function. The event is a JSON formatted document containing an order ID.

###### To create the test event

-
In the

**TEST EVENTS**section of the console code editor, choose**Create test event**. -
For

**Event Name**, enter`myTestEvent`

. -
In the

**Event JSON**section, replace the default JSON with the following:`{ "orderId": "order-12345" }`

-
Choose

**Save**.

**To test your durable function and view execution**

In the **TEST EVENTS** section of the console code editor, choose the run icon next to your test event:

Your durable function starts executing. Because it includes a 10-second wait, the initial invocation completes quickly, and the function
resumes after the wait period. You can view the execution progress in the **Durable executions** tab.

###### To view your durable function execution

-
Choose the

**Durable executions**tab. -
Find your execution in the list. The execution shows the current status (Running, Succeeded, or Failed).

-
Choose the execution ID to view details, including:

Execution timeline showing when each step completed

Checkpoint history

Wait periods

Step results


You can also view your function's logs in CloudWatch Logs to see the console output from each step.

###### To view your function's invocation records in CloudWatch Logs

-
Open the

[Log groups](https://console.aws.amazon.com/cloudwatch/home#logs:)page of the CloudWatch console. -
Choose the log group for your function (

`/aws/lambda/myDurableFunction`

). -
Scroll down and choose the

**Log stream**for the function invocations you want to look at.You should see log entries for each invocation of your function, including the initial execution and the replay after the wait.


###### Note

When you use the logger from the `DurableContext`

(such as `context.logger`

or `stepContext.logger`

), logs also appear in the durable execution and step views in the Lambda console. These logs may take a moment to load.

## Clean up

When you're finished working with the example durable function, delete it. You can also delete the log group that stores
the function's logs, and the [execution role](./lambda-intro-execution-role.html) that the console created.

###### To delete the Lambda function

-
Open the

[Functions page](https://console.aws.amazon.com/lambda/home#/functions)of the Lambda console. -
Select the function that you created.

-
Choose

**Actions**,**Delete**. -
Type

`confirm`

in the text input field and choose**Delete**.

###### To delete the log group

-
Open the

[Log groups](https://console.aws.amazon.com/cloudwatch/home#logs:)page of the CloudWatch console. -
Select the function's log group (

`/aws/lambda/myDurableFunction`

). -
Choose

**Actions**,**Delete log group(s)**. -
In the

**Delete log group(s)**dialog box, choose**Delete**.

###### To delete the execution role

-
Open the

[Roles page](https://console.aws.amazon.com/iam/home?#/roles)of the AWS Identity and Access Management (IAM) console. -
Select the function's execution role (for example,

`myDurableFunction-role-`

).`31exxmpl`

-
Choose

**Delete**. -
In the

**Delete role**dialog box, enter the role name, and then choose**Delete**.

## Additional resources and next steps

Now that you've created and tested a simple durable function using the console, take these next steps:

-
Learn about common use cases for durable functions, including distributed transactions, order processing, and human review workflows. See

[Examples](./durable-examples.html). -
Understand how to monitor durable function executions with CloudWatch metrics and execution history. See

[Monitoring and debugging](./durable-monitoring.html). -
Learn about invoking durable functions synchronously and asynchronously, and managing long-running executions. See

[Invoking durable functions](./durable-invoking.html). -
Follow best practices for writing deterministic code, managing checkpoint sizes, and optimizing costs. See

[Best practices](./durable-best-practices.html). -
Learn how to test durable functions locally and in the cloud. See

[Testing durable functions](./durable-testing.html). -
Compare durable functions with Step Functions to understand when each approach is most effective. See

[Durable functions or Step Functions](./durable-step-functions.html).