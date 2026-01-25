---
source_url: https://docs.aws.amazon.com/lambda/latest/dg/scheduled-task-app.html
fetched_at: 2026-01-25T15:06:16.586099
---

# Create an app to perform scheduled database maintenance

You can use AWS Lambda to replace scheduled processes such as automated system backups, file conversions, and maintenance tasks. In this example, you create a serverless application that performs regular scheduled maintenance on a DynamoDB table by deleting old entries. The app uses EventBridge Scheduler to invoke a Lambda function on a cron schedule. When invoked, the function queries the table for items older than one year, and deletes them. The function logs each deleted item in CloudWatch Logs.

To implement this example, first create a DynamoDB table and populate it with some test data for your function to query. Then, create a Python Lambda function with an EventBridge Scheduler trigger and an IAM execution role that gives the function permission to read, and delete, items from your table.

###### Tip

If you’re new to Lambda, we recommend that you complete the tutorial [Create your first Lambda function](./getting-started.html) before
creating this example app.

You can deploy your app manually by creating and configuring resources with the AWS Management Console. You can also deploy the app by using the AWS Serverless Application Model (AWS SAM). AWS SAM is an infrastructure as code (IaC) tool. With IaC, you don’t create resources manually, but define them in code and then deploy them automatically.

If you want to learn more about using Lambda with IaC before deploying this example app, see [Using Lambda with infrastructure as code (IaC)](./foundation-iac.html).

## Prerequisites

Before you can create the example app, make sure you have the required command line tools and programs installed.

-
**Python**To populate the DynamoDB table you create to test your app, this example uses a Python script and a CSV file to write data into the table. Make sure you have Python version 3.8 or later installed on your machine.

-
**AWS SAM CLI**If you want to create the DynamoDB table and deploy the example app using AWS SAM, you need to install the AWS SAM CLI. Follow the

[installation instructions](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html)in the*AWS SAM User Guide*. -
**AWS CLI**To use the provided Python script to populate your test table, you need to have installed and configured the AWS CLI. This is because the script uses the AWS SDK for Python (Boto3), which needs access to your AWS Identity and Access Management (IAM) credentials. You also need the AWS CLI installed to deploy resources using AWS SAM. Install the CLI by following the

[installation instructions](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)in the*AWS Command Line Interface User Guide*. -
**Docker**To deploy the app using AWS SAM, Docker must also be installed on your build machine. Follow the instructions in

[Install Docker Engine](https://docs.docker.com/engine/install/)on the Docker documentation website.

## Downloading the example app files

To create the example database and the scheduled-maintenance app, you need to create the following files in your project directory:

**Example database files**

-
`template.yaml`

- an AWS SAM template you can use to create the DynamoDB table -
`sample_data.csv`

- a CSV file containing sample data to load into your table -
`load_sample_data.py`

- a Python script that writes the data in the CSV file into the table

**Scheduled-maintenance app files**

-
`lambda_function.py`

- the Python function code for the Lambda function that performs the database maintenance -
`requirements.txt`

- a manifest file defining the dependencies that your Python function code requires -
`template.yaml`

- an AWS SAM template you can use to deploy the app

**Test file**

-
`test_app.py`

- a Python script that scans the table and confirms successful operation of your function by outputting all records older than one year

Expand the following sections to view the code and to learn more about the role of each file in creating and testing your app. To create the files on your local machine, copy and paste the code below.

Copy and paste the following code into a file named `template.yaml`

.

`AWSTemplateFormatVersion: '2010-09-09' Transform: AWS::Serverless-2016-10-31 Description: SAM Template for DynamoDB Table with Order_number as Partition Key and Date as Sort Key Resources: MyDynamoDBTable: Type: AWS::DynamoDB::Table DeletionPolicy: Retain UpdateReplacePolicy: Retain Properties: TableName: MyOrderTable BillingMode: PAY_PER_REQUEST AttributeDefinitions: - AttributeName: Order_number AttributeType: S - AttributeName: Date AttributeType: S KeySchema: - AttributeName: Order_number KeyType: HASH - AttributeName: Date KeyType: RANGE SSESpecification: SSEEnabled: true GlobalSecondaryIndexes: - IndexName: Date-index KeySchema: - AttributeName: Date KeyType: HASH Projection: ProjectionType: ALL PointInTimeRecoverySpecification: PointInTimeRecoveryEnabled: true Outputs: TableName: Description: DynamoDB Table Name Value: !Ref MyDynamoDBTable TableArn: Description: DynamoDB Table ARN Value: !GetAtt MyDynamoDBTable.Arn`


###### Note

AWS SAM templates use a standard naming convention of `template.yaml`

. In this example, you have two template files - one to create the
example database and another to create the app itself. Save them in separate sub-directories in your project folder.

This AWS SAM template defines the DynamoDB table resource you create to test your app. The table uses a primary key of `Order_number`

with a sort
key of `Date`

. In order for your Lambda function to find items directly by date, we also define a [Global Secondary Index](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GSI.html)
named `Date-index`

.

To learn more about creating and configuring a DynamoDB table using the `AWS::DynamoDB::Table`

resource, see [AWS::DynamoDB::Table](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-dynamodb-table.html) in
the *AWS CloudFormation User Guide*.

Copy and paste the following code into a file named `sample_data.csv`

.

`Date,Order_number,CustomerName,ProductID,Quantity,TotalAmount 2023-09-01,ORD001,Alejandro Rosalez,PROD123,2,199.98 2023-09-01,ORD002,Akua Mansa,PROD456,1,49.99 2023-09-02,ORD003,Ana Carolina Silva,PROD789,3,149.97 2023-09-03,ORD004,Arnav Desai,PROD123,1,99.99 2023-10-01,ORD005,Carlos Salazar,PROD456,2,99.98 2023-10-02,ORD006,Diego Ramirez,PROD789,1,49.99 2023-10-03,ORD007,Efua Owusu,PROD123,4,399.96 2023-10-04,ORD008,John Stiles,PROD456,2,99.98 2023-10-05,ORD009,Jorge Souza,PROD789,3,149.97 2023-10-06,ORD010,Kwaku Mensah,PROD123,1,99.99 2023-11-01,ORD011,Li Juan,PROD456,5,249.95 2023-11-02,ORD012,Marcia Oliveria,PROD789,2,99.98 2023-11-03,ORD013,Maria Garcia,PROD123,3,299.97 2023-11-04,ORD014,Martha Rivera,PROD456,1,49.99 2023-11-05,ORD015,Mary Major,PROD789,4,199.96 2023-12-01,ORD016,Mateo Jackson,PROD123,2,199.99 2023-12-02,ORD017,Nikki Wolf,PROD456,3,149.97 2023-12-03,ORD018,Pat Candella,PROD789,1,49.99 2023-12-04,ORD019,Paulo Santos,PROD123,5,499.95 2023-12-05,ORD020,Richard Roe,PROD456,2,99.98 2024-01-01,ORD021,Saanvi Sarkar,PROD789,3,149.97 2024-01-02,ORD022,Shirley Rodriguez,PROD123,1,99.99 2024-01-03,ORD023,Sofia Martinez,PROD456,4,199.96 2024-01-04,ORD024,Terry Whitlock,PROD789,2,99.98 2024-01-05,ORD025,Wang Xiulan,PROD123,3,299.97`


This file contains some example test data to populate your DynamoDB table with in a standard comma-separated values (CSV) format.

Copy and paste the following code into a file named `load_sample_data.py`

.

`import boto3 import csv from decimal import Decimal # Initialize the DynamoDB client dynamodb = boto3.resource('dynamodb') table = dynamodb.Table('MyOrderTable') print("DDB client initialized.") def load_data_from_csv(filename): with open(filename, 'r') as file: csv_reader = csv.DictReader(file) for row in csv_reader: item = { 'Order_number': row['Order_number'], 'Date': row['Date'], 'CustomerName': row['CustomerName'], 'ProductID': row['ProductID'], 'Quantity': int(row['Quantity']), 'TotalAmount': Decimal(str(row['TotalAmount'])) } table.put_item(Item=item) print(f"Added item: {item['Order_number']} - {item['Date']}") if __name__ == "__main__": load_data_from_csv('sample_data.csv') print("Data loading completed.")`


This Python script first uses the AWS SDK for Python (Boto3) to create a connection to your DynamoDB table. It then iterates over each row in the example-data CSV file, creates an item from that row, and writes the item to the DynamoDB table using the boto3 SDK.

Copy and paste the following code into a file named `lambda_function.py`

.

`import boto3 from datetime import datetime, timedelta from boto3.dynamodb.conditions import Key, Attr import logging logger = logging.getLogger() logger.setLevel("INFO") def lambda_handler(event, context): # Initialize the DynamoDB client dynamodb = boto3.resource('dynamodb') # Specify the table name table_name = 'MyOrderTable' table = dynamodb.Table(table_name) # Get today's date today = datetime.now() # Calculate the date one year ago one_year_ago = (today - timedelta(days=365)).strftime('%Y-%m-%d') # Scan the table using a global secondary index response = table.scan( IndexName='Date-index', FilterExpression='#date < :one_year_ago', ExpressionAttributeNames={ '#date': 'Date' }, ExpressionAttributeValues={ ':one_year_ago': one_year_ago } ) # Delete old items with table.batch_writer() as batch: for item in response['Items']: Order_number = item['Order_number'] batch.delete_item( Key={ 'Order_number': Order_number, 'Date': item['Date'] } ) logger.info(f'deleted order number {Order_number}') # Check if there are more items to scan while 'LastEvaluatedKey' in response: response = table.scan( IndexName='DateIndex', FilterExpression='#date < :one_year_ago', ExpressionAttributeNames={ '#date': 'Date' }, ExpressionAttributeValues={ ':one_year_ago': one_year_ago }, ExclusiveStartKey=response['LastEvaluatedKey'] ) # Delete old items with table.batch_writer() as batch: for item in response['Items']: batch.delete_item( Key={ 'Order_number': item['Order_number'], 'Date': item['Date'] } ) return { 'statusCode': 200, 'body': 'Cleanup completed successfully' }`


The Python function code contains the [handler function](./python-handler.html) (`lambda_handler`

) that Lambda runs when your function is
invoked.

When the function is invoked by EventBridge Scheduler, it uses the AWS SDK for Python (Boto3) to create a connection to the DynamoDB table on which the scheduled maintenance task is to be performed.
It then uses the Python `datetime`

library to calculate the date one year ago, before scanning the table for items older than this and deleting them.

Note that responses from DynamoDB query and scan operations are limited to a maximum of 1 MB in size. If the response is larger than 1 MB, DynamoDB paginates the
data and returns a `LastEvaluatedKey`

element in the response. To ensure that our function processes all the records in the table, we check for the presence of this key
and continue performing table scans from the last evaluated position until the whole table has been scanned.

Copy and paste the following code into a file named `requirements.txt`

.

`boto3`


For this example, your function code has only one dependency that isn't part of the standard Python library - the SDK for Python (Boto3) that the function uses to scan and delete items from the DynamoDB table.

###### Note

A version of the SDK for Python (Boto3) is included as part of the Lambda runtime, so your code would run without adding Boto3 to your
function's deployment package. However, to maintain full control of your function's dependencies and avoid possible issues with
version misalignment, best practice for Python is to include all function dependencies in your function's deployment package.
See [Runtime dependencies in Python](./python-package.html#python-package-dependencies) to learn more.

Copy and paste the following code into a file named `template.yaml`

.

`AWSTemplateFormatVersion: '2010-09-09' Transform: AWS::Serverless-2016-10-31 Description: SAM Template for Lambda function and EventBridge Scheduler rule Resources: MyLambdaFunction: Type: AWS::Serverless::Function Properties: FunctionName: ScheduledDBMaintenance CodeUri: ./ Handler: lambda_function.lambda_handler Runtime: python3.11 Architectures: - x86_64 Events: ScheduleEvent: Type: ScheduleV2 Properties: ScheduleExpression: cron(0 3 1 * ? *) Description: Run on the first day of every month at 03:00 AM Policies: - CloudWatchLogsFullAccess - Statement: - Effect: Allow Action: - dynamodb:Scan - dynamodb:BatchWriteItem Resource: !Sub 'arn:aws:dynamodb:${AWS::Region}:${AWS::AccountId}:table/MyOrderTable' LambdaLogGroup: Type: AWS::Logs::LogGroup Properties: LogGroupName: !Sub /aws/lambda/${MyLambdaFunction} RetentionInDays: 30 Outputs: LambdaFunctionName: Description: Lambda Function Name Value: !Ref MyLambdaFunction LambdaFunctionArn: Description: Lambda Function ARN Value: !GetAtt MyLambdaFunction.Arn`


###### Note

AWS SAM templates use a standard naming convention of `template.yaml`

. In this example, you have two template files - one to create the
example database and another to create the app itself. Save them in separate sub-directories in your project folder.

This AWS SAM template defines the resources for your app. We define the Lambda function using the `AWS::Serverless::Function`

resource. The EventBridge Scheduler schedule and the
trigger to invoke the Lambda function are created by using the `Events`

property of this resource using a type of `ScheduleV2`

. To learn more about defining EventBridge Scheduler schedules in AWS SAM templates,
see [ScheduleV2](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-property-function-schedulev2.html) in the
*AWS Serverless Application Model Developer Guide*.

In addition to the Lambda function and the EventBridge Scheduler schedule, we also define a CloudWatch log group for your function to send records of deleted items to.

Copy and paste the following code into a file named `test_app.py`

.

`import boto3 from datetime import datetime, timedelta import json # Initialize the DynamoDB client dynamodb = boto3.resource('dynamodb') # Specify your table name table_name = 'YourTableName' table = dynamodb.Table(table_name) # Get the current date current_date = datetime.now() # Calculate the date one year ago one_year_ago = current_date - timedelta(days=365) # Convert the date to string format (assuming the date in DynamoDB is stored as a string) one_year_ago_str = one_year_ago.strftime('%Y-%m-%d') # Scan the table response = table.scan( FilterExpression='#date < :one_year_ago', ExpressionAttributeNames={ '#date': 'Date' }, ExpressionAttributeValues={ ':one_year_ago': one_year_ago_str } ) # Process the results old_records = response['Items'] # Continue scanning if we have more items (pagination) while 'LastEvaluatedKey' in response: response = table.scan( FilterExpression='#date < :one_year_ago', ExpressionAttributeNames={ '#date': 'Date' }, ExpressionAttributeValues={ ':one_year_ago': one_year_ago_str }, ExclusiveStartKey=response['LastEvaluatedKey'] ) old_records.extend(response['Items']) for record in old_records: print(json.dumps(record)) # The total number of old records should be zero. print(f"Total number of old records: {len(old_records)}")`


This test script uses the AWS SDK for Python (Boto3) to create a connection to your DynamoDB table and scan for items older than one year. To confirm if the Lambda function has run successfully, at the end of the test, the function prints the number of records older than one year still in the table. If the Lambda function was successful, the number of old records in the table should be zero.

## Creating and populating the example DynamoDB table

To test your scheduled-maintenance app, you first create a DynamoDB table and populate it with some sample data. You can create the table either manually using the AWS Management Console or by using AWS SAM. We recommend that you use AWS SAM to quickly create and configure the table using a few AWS CLI commands.

After you've created your table, you next add some sample data to test your app. The CSV file `sample_data.csv`

you downloaded
earlier contains a number of example entries comprised of order numbers, dates, and customer and order information. Use the provided python script
`load_sample_data.py`

to add this data to your table.

###### To add the sample data to the table

-
Navigate to the directory containing the

`sample_data.csv`

and`load_sample_data.py`

files. If these files are in separate directories, move them so they're saved in the same location. -
Create a Python virtual environment to run the script in by running the following command. We recommend that you use a virtual environment because in a following step you'll need to install the AWS SDK for Python (Boto3).

`python -m venv venv`

-
Activate the virtual environment by running the following command.

`source venv/bin/activate`

-
Install the SDK for Python (Boto3) in your virtual environment by running the following command. The script uses this library to connect to your DynamoDB table and add the items.

`pip install boto3`

-
Run the script to populate the table by running the following command.

`python load_sample_data.py`

If the script runs successfully, it should print each item to the console as it loads it and report

`Data loading completed`

. -
Deactivate the virtual environment by running the following command.

`deactivate`

-
You can verify that the data has been loaded to your DynamoDB table by doing the following:

-
Open the

[Explore items](https://console.aws.amazon.com/dynamodbv2/home#item-explorer)page of the DynamoDB console and select your table (`MyOrderTable`

). -
In the

**Items returned**pane, you should see the 25 items from the CSV file that the script added to the table.

-

## Creating the scheduled-maintenance app

You can create and deploy the resources for this example app step by step using the AWS Management Console or by using AWS SAM. In a production environment, we recommend that you use an Infrustracture-as-Code (IaC) tool like AWS SAM to repeatably deploy serverless applications without using manual processes.

For this example, follow the console instructions to learn how to configure each AWS resource separately, or follow the AWS SAM instructions to quickly deploy the app using AWS CLI commands.

## Testing the app

To test that your schedule correctly triggers your function, and that your function correctly cleans records
from the database, you can temporarily modify your schedule to run once at a specific time. You can then run `sam deploy`

again to
reset your recurrence schedule to run once a month.

###### To run the application using the AWS Management Console

-
Navigate back to the EventBridge Scheduler console page.

-
Choose your schedule, then choose

**Edit**. -
In the

**Schedule pattern**section, under**Recurrence**, choose**One-time schedule**. -
Set your invocation time to a few minutes from now, review your settings, then choose

**Save**.

After the schedule runs and invokes its target, you run the `test_app.py`

script to verify that your function successfully removed all old records
from the DynamoDB table.

###### To verify that old records are deleted using a Python script

-
In your command line, navigate to the folder where you saved

`test_app.py`

. -
Run the script.

`python test_app.py`

If successful, you will see the following output.

Total number of old records: 0


## Next steps

You can now modify the EventBridge Scheduler schedule to meet your particular application requirements. EventBridge Scheduler supports the following schedule expressions: cron, rate, and one-time schedules.

For more information about EventBridge Scheduler schedule expressions, see [Schedule types](https://docs.aws.amazon.com/scheduler/latest/UserGuide/schedule-types.html) in the
*EventBridge Scheduler User Guide*.
[Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*