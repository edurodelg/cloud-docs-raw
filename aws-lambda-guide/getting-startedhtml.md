---
source_url: https://docs.aws.amazon.com/lambda/latest/dg/getting-started.html
fetched_at: 2026-02-06T16:34:54.131016
---

# Create your first Lambda function

To get started with Lambda, use the Lambda console to create a function. In a few minutes, you can create and deploy a function and test it in the console.

As you carry out the tutorial, you'll learn some fundamental Lambda concepts, like how to pass arguments to
your function using the Lambda *event object*. You'll also learn how to return log outputs from your function, and how to
view your function's invocation logs in Amazon CloudWatch Logs.

To keep things simple, you create your function using either the Python or Node.js runtime. With these interpreted languages, you can edit
function code directly in the console's built-in code editor. With compiled languages like Java and C#, you must create a deployment package on
your local build machine and upload it to Lambda. To learn about deploying functions to Lambda using other runtimes, see the links in the
[Additional resources and next steps](#getting-started-more-resources) section.

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

## Create a Lambda function with the console

In this example, your function takes a JSON object containing two integer values labeled `"length"`

and `"width"`

.
The function multiplies these values to calculate an area and returns this as a JSON string.

Your function also prints the calculated area, along with the name of its CloudWatch log group. Later in the tutorial, you’ll learn to use [CloudWatch Logs](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html)
to view records of your functions’ invocation.

###### To create a Hello world Lambda function with the console

Open the

[Functions page](https://console.aws.amazon.com/lambda/home#/functions)of the Lambda console.-
Choose

**Create function**. -
Select

**Author from scratch**. -
In the

**Basic information**pane, for**Function name**, enter

.`myLambdaFunction`

-
For

**Runtime**, choose either**Node.js 24**or**Python 3.14**. -
Leave

**architecture**set to**x86_64**, and then choose**Create function**.

In addition to a simple function that returns the message `Hello from Lambda!`

, Lambda also creates an [execution role](./lambda-intro-execution-role.html) for your function. An execution role is an AWS Identity and Access Management (IAM) role that grants a Lambda function
permission to access AWS services and resources. For your function, the role that Lambda creates grants basic permissions to write to CloudWatch Logs.

Use the console's built-in code editor to replace the Hello world code that Lambda created with your own function code.

## Invoke the Lambda function using the console code editor

To invoke your function using the Lambda console code editor, create a test event to send to your function. The event is a JSON formatted
document containing two key-value pairs with the keys `"length"`

and `"width"`

.

###### To create the test event

-
In the

**TEST EVENTS**section of the console code editor, choose**Create test event**. -
For

**Event Name**, enter`myTestEvent`

. -
In the

**Event JSON**section, replace the default JSON with the following:`{ "length": 6, "width": 7 }`

-
Choose

**Save**.

**To test your function and view invocation records**

In the **TEST EVENTS** section of the console code editor, choose the run icon next to your test event:

When your function finishes running, the response and function logs are displayed in the **OUTPUT** tab. You should see results similar to the following:

When you invoke your function outside of the Lambda console, you must use CloudWatch Logs to view your function's execution results.

###### To view your function's invocation records in CloudWatch Logs

-
Open the

[Log groups](https://console.aws.amazon.com/cloudwatch/home#logs:)page of the CloudWatch console. -
Choose the log group for your function (

`/aws/lambda/myLambdaFunction`

). This is the log group name that your function printed to the console. -
Scroll down and choose the

**Log stream**for the function invocations you want to look at.You should see output similar to the following:


## Clean up

When you're finished working with the example function, delete it. You can also delete the log group that stores
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

`/aws/lambda/myLambdaFunction`

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

`myLambdaFunction-role-`

).`31exxmpl`

-
Choose

**Delete**. -
In the

**Delete role**dialog box, enter the role name, and then choose**Delete**.

## Additional resources and next steps

Now that you’ve created and tested a simple Lambda function using the console, take these next steps:

-
Learn to add dependencies to your function and deploy it using a .zip deployment package. Choose your preferred language from the following links.

-
To learn how to invoke a Lambda function using another AWS service, see

[Tutorial: Using an Amazon S3 trigger to invoke a Lambda function](./with-s3-example.html). -
Choose one of the following tutorials for more complex examples of using Lambda with other AWS services.

-
[Tutorial: Using Lambda with API Gateway](./services-apigateway-tutorial.html): Create an Amazon API Gateway REST API that invokes a Lambda function. -
[Using a Lambda function to access an Amazon RDS database](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-lambda-tutorial.html): Use a Lambda function to write data to an Amazon Relational Database Service (Amazon RDS) database through RDS Proxy. -
[Using an Amazon S3 trigger to create thumbnail images](./with-s3-tutorial.html): Use a Lambda function to create a thumbnail every time an image file is uploaded to an Amazon S3 bucket.

-