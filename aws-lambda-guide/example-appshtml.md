---
source_url: https://docs.aws.amazon.com/lambda/latest/dg/example-apps.html
fetched_at: 2026-02-05T08:16:09.838749
---

# Getting started with example applications and patterns

The following resources can be used to quickly create and deploy serverless apps that implement some common Lambda uses cases. For each of the example apps, we provide instructions to either create and configure resources manually using the AWS Management Console, or to use the AWS Serverless Application Model to deploy the resources using IaC. Follow the console intructions to learn more about configuring the individual AWS resources for each app, or use to AWS SAM to quickly deploy resources as you would in a production environment.

## File Processing

: Create a serverless application that encrypts PDF files when they are uploaded to an Amazon Simple Storage Service bucket and saves them to another bucket, which is useful for securing sensitive documents upon upload.[PDF Encryption Application](./file-processing-app.html)

: Create a serverless application that extracts text from images using Amazon Rekognition, which is useful for document processing, content moderation, and automated image analysis.[Image Analysis Application](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-example-s3.html)

## Database Integration

: Create a serverless application that writes queue messages to an Amazon RDS database, which is useful for processing user registrations and handling order submissions.[Queue-to-Database Application](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-lambda-tutorial.html)

: Create a serverless application that responds to Amazon DynamoDB table changes, which is useful for audit logging, data replication, and automated workflows.[Database Event Handler](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-example-ddb.html)

## Scheduled Tasks

: Create a serverless application that automatically deletes entries more than 12 months old from an Amazon DynamoDB table using a cron schedule, which is useful for automated database maintenance and data lifecycle management.[Database Maintenance Application](./scheduled-task-app.html): Use scheduled expressions for rules in EventBridge to trigger a Lambda function on a timed schedule. This format uses cron syntax and can be set with a one-minute granularity.[Create an EventBridge scheduled rule for Lambda functions](https://docs.aws.amazon.com/eventbridge/latest/userguide/run-lambda-schedule.html)

## Long-running Workflows

: Create a serverless application using Durable Functions that handles complex order fulfillment, including payment processing, inventory checks, and shipping coordination. This example demonstrates how to build workflows that can run for extended periods while maintaining state.[Order Processing Application](./order-processing-app.html)

## Additional resources

Use the following resources to further explore Lambda and serverless application development:

: a library of ready-to-use patterns for building serverless apps. It helps developers create applications faster using AWS services like Lambda, API Gateway, and EventBridge. The site offers pre-built solutions and best practices, making it easier to develop serverless systems.[Serverless Land](https://serverlessland.com/)-
: Applications that are available in the GitHub repository for this guide. These samples demonstrate the use of various languages and AWS services. Each sample application includes scripts for easy deployment and cleanup and supporting resources.[Lambda sample applications](https://docs.aws.amazon.com/lambda/latest/dg/lambda-samples.html) -
: Examples that show you how to use Lambda with AWS software development kits (SDKs). These examples include basics, actions, scenarios, and AWS community contributions. Examples cover essential operations, individual service functions, and specific tasks using multiple functions or AWS services.[Code examples for Lambda using AWS SDKs](https://docs.aws.amazon.com/lambda/latest/dg/service_code_examples.html)