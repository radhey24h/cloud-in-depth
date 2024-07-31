# AWS Lambda

AWS Lambda is a serverless compute service that lets you run code without provisioning or managing servers. You only pay for the compute time you consume, and you don't have to manage any infrastructure. This document provides an in-depth overview of AWS Lambda, including its architecture, use cases, billing details, commands, and code snippets.

## AWS Lambda Architecture

AWS Lambda operates on a serverless model, handling the execution of code in response to events without the need for provisioning or managing servers. The architecture includes several key components:

### 1. Lambda Functions
   - **Description:** The core component of AWS Lambda. Functions contain the code you want to execute and are triggered by events from various AWS services or HTTP requests via API Gateway.
   - **Architecture:** 
     - **Function Code:** Contains the code you want to execute. Supports various languages, including Python, Node.js, Java, and more.
     - **Execution Role:** An IAM role that grants permissions for the Lambda function to interact with other AWS services.
   - **Use Case:** A company wants to process incoming data files automatically. They create a Lambda function that triggers on file uploads to an S3 bucket, processes the data, and stores results in another S3 bucket.
   - **Billing Details:** Charges based on the number of requests and the duration of function execution. The first 1 million requests and 400,000 GB-seconds of compute time per month are free.
   - **Commands:**
     ```bash
     # Create a Lambda function
     aws lambda create-function --function-name my-function --runtime nodejs14.x --role arn:aws:iam::account-id:role/service-role/my-role --handler index.handler --zip-file fileb://function.zip

     # Invoke a Lambda function
     aws lambda invoke --function-name my-function --payload '{"key": "value"}' response.json
     ```

### 2. Triggers
   - **Description:** Events that invoke Lambda functions. Triggers can come from various sources, such as S3, DynamoDB, Kinesis, and API Gateway.
   - **Architecture:** 
     - **Event Source:** Defines the event that triggers the Lambda function.
     - **Event Mapping:** Configures how events are mapped to Lambda functions.
   - **Use Case:** A company needs to send a notification email every time a new item is added to a DynamoDB table. They set up a DynamoDB stream that triggers a Lambda function to send an email.
   - **Billing Details:** Triggers themselves do not incur additional charges. Costs are based on Lambda execution and associated AWS services (e.g., S3, DynamoDB).
   - **Commands:**
     ```bash
     # Add an S3 trigger to a Lambda function
     aws lambda create-event-source-mapping --function-name my-function --event-source-arn arn:aws:s3:::my-bucket --starting-position LATEST
     ```

### 3. Layers
   - **Description:** A distribution mechanism for libraries, custom runtimes, or other dependencies that Lambda functions need. Layers help manage and share common dependencies across multiple functions.
   - **Architecture:** 
     - **Layer:** A ZIP archive that contains libraries, a custom runtime, or other function dependencies.
     - **Versioning:** Layers can have multiple versions.
   - **Use Case:** A development team uses a common logging library across multiple Lambda functions. They create a Lambda Layer for the logging library and attach it to each function.
   - **Billing Details:** Charges for Lambda Layers are included in the function execution costs. There are no separate charges for using layers.
   - **Commands:**
     ```bash
     # Publish a new version of a Lambda Layer
     aws lambda publish-layer-version --layer-name my-layer --zip-file fileb://layer.zip --compatible-runtimes nodejs14.x

     # Add a Layer to a Lambda function
     aws lambda update-function-configuration --function-name my-function --layers arn:aws:lambda:region:account-id:layer:my-layer:1
     ```

### 4. API Gateway Integration
   - **Description:** API Gateway provides a RESTful API endpoint that triggers Lambda functions. This allows you to create serverless APIs that can handle HTTP requests and responses.
   - **Architecture:** 
     - **API Gateway:** Acts as an intermediary between clients and Lambda functions.
     - **Integration Request:** Configures how requests are mapped to Lambda functions.
     - **Integration Response:** Configures how Lambda responses are mapped back to clients.
   - **Use Case:** A company creates a serverless web application where users interact via an API. They use API Gateway to route HTTP requests to Lambda functions, which handle business logic and interact with a database.
   - **Billing Details:** Charges for API Gateway are based on the number of API calls and the amount of data transferred. Lambda execution costs are additional.
   - **Commands:**
     ```bash
     # Create a new API Gateway REST API
     aws apigateway create-rest-api --name my-api

     # Create a new resource in API Gateway
     aws apigateway create-resource --rest-api-id api-id --parent-id parent-id --path-part resource-path

     # Create a new method in API Gateway
     aws apigateway put-method --rest-api-id api-id --resource-id resource-id --http-method POST --authorization-type NONE

     # Link Lambda function to API Gateway
     aws apigateway put-integration --rest-api-id api-id --resource-id resource-id --http-method POST --type AWS_PROXY --integration-http-method POST --uri arn:aws:apigateway:region:lambda:path/2015-03-31/functions/function-arn/invocations
     ```

### 5. Event Source Mappings
   - **Description:** Event source mappings link a Lambda function to a stream-based event source, such as DynamoDB Streams or Kinesis Data Streams.
   - **Architecture:** 
     - **Event Source:** Stream-based services that provide events.
     - **Mapping:** Configures how events are processed and how often Lambda functions are invoked.
   - **Use Case:** A company needs to process logs in real time from a Kinesis Data Stream. They set up an event source mapping to trigger a Lambda function that processes and stores logs.
   - **Billing Details:** Charges for event source mappings are included in the Lambda execution costs. Costs for the event source (e.g., Kinesis, DynamoDB) are separate.
   - **Commands:**
     ```bash
     # Create an event source mapping for a Kinesis stream
     aws lambda create-event-source-mapping --function-name my-function --event-source-arn arn:aws:kinesis:region:account-id:stream/my-stream --starting-position LATEST
     ```

### 6. Environment Variables
   - **Description:** Key-value pairs that are passed to Lambda functions at runtime. They are used to provide configuration settings to your function code.
   - **Architecture:** 
     - **Environment Variables:** Configurable key-value pairs defined in the Lambda function configuration.
   - **Use Case:** A Lambda function needs database connection details. The details are stored as environment variables and accessed by the function code.
   - **Billing Details:** No additional costs for environment variables. Costs are included in the overall Lambda execution pricing.
   - **Commands:**
     ```bash
     # Update environment variables for a Lambda function
     aws lambda update-function-configuration --function-name my-function --environment Variables={KEY1=VALUE1,KEY2=VALUE2}
     ```

### 7. VPC Integration
   - **Description:** Allows Lambda functions to access resources within a Virtual Private Cloud (VPC) by associating the function with specific VPC subnets and security groups.
   - **Architecture:** 
     - **Subnet:** Network segment within a VPC that provides IP addresses to Lambda functions.
     - **Security Group:** Defines rules for inbound and outbound traffic to Lambda functions.
   - **Use Case:** A Lambda function needs to access a database within a private VPC. The function is configured with appropriate VPC settings, subnets, and security groups.
   - **Billing Details:** Costs for VPC integration include Lambda execution and any data transfer within the VPC.
   - **Commands:**
     ```bash
     # Update a Lambda function to connect to a VPC
     aws lambda update-function-configuration --function-name my-function --vpc-config SubnetIds=subnet-12345678,SecurityGroupIds=sg-12345678
     ```

## Billing Details

### Cost Factors

1. **Request Charges:** Costs are based on the number of requests made to the Lambda function. The first 1 million requests per month are free.
2. **Duration Charges:** Costs are based on the execution duration of the Lambda function, measured in milliseconds. The first 400,000 GB-seconds of compute time per month are free.
3. **Provisioned Concurrency:** If using provisioned concurrency, charges apply based on the number of provisioned instances and the duration they are active.
4. **Data Transfer:** Costs for data transferred out of Lambda functions, such as to S3 or other services, are additional.

### Pricing Tiers

- **Free Tier:** Includes 1 million requests and 400,000 GB-seconds of compute time per month.
- **Pay-As-You-Go:** Charges based on actual usage beyond the free tier, including requests, compute time, and data transfer.

For detailed and up-to-date pricing information, refer to the [AWS Lambda Pricing page](https://aws.amazon.com/lambda/pricing/).

This README provides a comprehensive overview of AWS Lambda, detailing its components, architecture, use cases, billing details, and relevant commands and code snippets. It serves as a guide for understanding and managing AWS Lambda functions effectively.
