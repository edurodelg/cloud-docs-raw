---
source_url: https://docs.aws.amazon.com/lambda/latest/dg/durable-getting-started-iac.html
fetched_at: 2026-01-25T15:07:26.429089
---

# Deploy Lambda durable functions with Infrastructure as Code

You can deploy Lambda durable functions using Infrastructure as Code (IaC) tools like AWS CloudFormation, AWS CDK, or AWS Serverless Application Model. These tools let you define your function, execution role, and permissions in code, making deployments repeatable and version-controlled.

All three tools require you to:

Enable durable execution on the function

Grant checkpoint permissions to the execution role

Publish a version or create an alias (durable functions require qualified ARNs)


## AWS CloudFormation

Use CloudFormation to define your durable function in a template. The following example creates a durable function with the required permissions.

`AWSTemplateFormatVersion: '2010-09-09' Description: Lambda durable function example Resources: DurableFunctionRole: Type: AWS::IAM::Role Properties: AssumeRolePolicyDocument: Version: '2012-10-17' Statement: - Effect: Allow Principal: Service: lambda.amazonaws.com Action: sts:AssumeRole ManagedPolicyArns: - arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole Policies: - PolicyName: DurableExecutionPolicy PolicyDocument: Version: '2012-10-17' Statement: - Effect: Allow Action: - lambda:CheckpointDurableExecutions - lambda:GetDurableExecutionState Resource: !GetAtt DurableFunction.Arn DurableFunction: Type: AWS::Lambda::Function Properties: FunctionName: myDurableFunction Runtime: nodejs22.x Handler: index.handler Role: !GetAtt DurableFunctionRole.Arn Code: ZipFile: | // Your durable function code here export const handler = async (event, context) => { return { statusCode: 200 }; }; DurableConfig: ExecutionTimeout: 10 RetentionPeriodInDays: 1 DurableFunctionVersion: Type: AWS::Lambda::Version Properties: FunctionName: !Ref DurableFunction Description: Initial version DurableFunctionAlias: Type: AWS::Lambda::Alias Properties: FunctionName: !Ref DurableFunction FunctionVersion: !GetAtt DurableFunctionVersion.Version Name: prod Outputs: FunctionArn: Description: Durable function ARN Value: !GetAtt DurableFunction.Arn AliasArn: Description: Function alias ARN (use this for invocations) Value: !Ref DurableFunctionAlias`


**To deploy the template**

`aws cloudformation deploy \ --template-file template.yaml \ --stack-name my-durable-function-stack \ --capabilities CAPABILITY_IAM`


## AWS CDK

AWS CDK lets you define infrastructure using programming languages. The following examples show how to create a durable function using TypeScript and Python.

**To deploy the CDK stack**

`cdk deploy`


## AWS Serverless Application Model

AWS SAM simplifies CloudFormation templates for serverless applications. The following template creates a durable function with AWS SAM.

`AWSTemplateFormatVersion: '2010-09-09' Transform: AWS::Serverless-2016-10-31 Description: Lambda durable function with SAM Resources: DurableFunction: Type: AWS::Serverless::Function Properties: FunctionName: myDurableFunction Runtime: nodejs22.x Handler: index.handler CodeUri: ./src DurableConfig: ExecutionTimeout: 10 RetentionPeriodInDays: 1 Policies: - Version: '2012-10-17' Statement: - Effect: Allow Action: - lambda:CheckpointDurableExecutions - lambda:GetDurableExecutionState Resource: !Sub 'arn:aws:lambda:${AWS::Region}:${AWS::AccountId}:function:${DurableFunction}' AutoPublishAlias: prod Outputs: FunctionArn: Description: Durable function ARN Value: !GetAtt DurableFunction.Arn AliasArn: Description: Function alias ARN (use this for invocations) Value: !Ref DurableFunction.Alias`


**To deploy the SAM template**

`sam build sam deploy --guided`


## Common configuration patterns

Regardless of which IaC tool you use, follow these patterns for durable functions:

###### Enable durable execution

Set the `DurableExecution.Enabled`

property to `true`

. This property is only available when creating the function—you cannot enable durable execution on existing functions.

###### Grant checkpoint permissions

Add `lambda:CheckpointDurableExecutions`

and `lambda:GetDurableExecutionState`

to the execution role. Scope these permissions to the specific function ARN.

###### Use qualified ARNs

Create a version or alias for your function. Durable functions require qualified ARNs (with version or alias) for invocation. Use `AutoPublishAlias`

in AWS SAM or create explicit versions in CloudFormation and AWS CDK.

###### Package dependencies

Include the durable execution SDK in your deployment package. For Node.js, install `@aws/durable-execution-sdk-js`

. For Python, install `aws-durable-execution-sdk-python`

.

## Next steps

After deploying your durable function:

-
Test your function using the qualified ARN (version or alias)

-
Monitor execution progress in the Lambda console under the Durable executions tab

-
View checkpoint operations in AWS CloudTrail data events

-
Review CloudWatch Logs for function output and replay behavior


For more information about deploying Lambda functions with IaC tools, see: