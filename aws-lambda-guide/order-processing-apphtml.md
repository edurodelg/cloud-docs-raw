---
source_url: https://docs.aws.amazon.com/lambda/latest/dg/order-processing-app.html
fetched_at: 2026-01-29T15:12:47.834757
---

# Creating an Order Processing System with Lambda Durable Functions

###### Note

NEED: Add architecture diagram showing API Gateway, Durable Function workflow, and supporting services (DynamoDB, EventBridge)

## Prerequisites

AWS CLI installed and configured

NEED: Specific Durable Functions requirements


## Create the Source Code Files

Create the following files in your project directory:

`lambda_function.py`

- the function code`requirements.txt`

- dependencies manifest

### Function Code

`# NEED: Verify correct imports import boto3 import json def lambda_handler(event, context): # NEED: Verify DurableContext syntax durable = context.durable try: # Validate and store order order = await durable.step('validate', async () => { return validate_order(event['order']) }) # Process payment # NEED: Verify wait syntax await durable.wait(/* wait configuration */) # Additional steps # NEED: Complete implementation except Exception as e: # NEED: Error handling patterns raise e def validate_order(order_data): # NEED: Implementation pass`


### Requirements File

`# NEED: List of required packages`


## Deploy the App

### Create a DynamoDB Table for Orders

Open the DynamoDB console at

[https://console.aws.amazon.com/dynamodb/](https://console.aws.amazon.com/dynamodb/)Choose

**Create table**For

**Table name**, enter`Orders`

For

**Partition key**, enter`orderId`

Leave other settings as default

Choose

**Create table**

### Create the Lambda Function

Open the Lambda console at

[https://console.aws.amazon.com/lambda/](https://console.aws.amazon.com/lambda/)Choose

**Create function**Select

**Author from scratch**For

**Function name**, enter`ProcessOrder`

For

**Runtime**, choose your preferred runtimeNEED: Add Durable Functions-specific configuration

Choose

**Create function**

### Create the API Gateway Endpoint

Open the API Gateway console at

[https://console.aws.amazon.com/apigateway/](https://console.aws.amazon.com/apigateway/)Choose

**Create API**Select

**HTTP API**Choose

**Build**Add an integration with your Lambda function

Configure routes for order processing

Deploy the API


## Test the App

Submit a test order:

`{ "orderId": "12345", "items": [ { "productId": "ABC123", "quantity": 1 } ] }`


NEED: Add specific monitoring instructions for Durable Functions

## Next Steps

### Add Business Logic

Implement inventory management:

`async def check_inventory(order): # Add inventory check logic pass`


Add price calculations:

`async def calculate_total(order): # Add pricing logic pass`


### Improve Error Handling

Add compensation logic:

`async def reverse_payment(order): # Add payment reversal logic pass`


Handle order cancellations:

`async def cancel_order(order): # Add cancellation logic pass`


### Integrate External Systems

`async def notify_shipping_provider(order): # Add shipping integration pass async def send_customer_notification(order): # Add notification logic pass`


### Enhance Monitoring

Create CloudWatch dashboards

Set up metrics for order processing times

Configure alerts for delayed orders