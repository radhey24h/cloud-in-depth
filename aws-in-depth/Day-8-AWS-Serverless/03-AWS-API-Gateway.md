# AWS API Gateway

AWS API Gateway is a fully managed service that allows developers to create, publish, maintain, monitor, and secure APIs at any scale. It provides a robust framework for building and managing APIs that serve as the front-end for your backend services.

## Overview

AWS API Gateway enables you to build and manage APIs with minimal overhead. Key features and benefits include:

- **API Creation**: Easily create RESTful APIs, WebSocket APIs, and HTTP APIs to enable communication between your applications and backend services.
- **Traffic Management**: Handle and manage traffic to your APIs efficiently, including throttling and request/response transformation.
- **Security**: Protect your APIs with integrated security features, including AWS Identity and Access Management (IAM), API keys, and OAuth 2.0.
- **Monitoring and Analytics**: Monitor API performance and usage with built-in analytics and CloudWatch integration.

## Key Features

### API Types

- **REST APIs**: Enable HTTP requests to interact with backend services. REST APIs are ideal for creating web and mobile applications.
- **HTTP APIs**: A simpler and more cost-effective option for building APIs with lower latency and reduced complexity compared to REST APIs.
- **WebSocket APIs**: Support real-time, two-way communication between clients and servers. Useful for applications requiring low-latency updates and real-time data.

### Integration with Backend Services

- **Lambda Functions**: Easily integrate your APIs with AWS Lambda functions to run backend code in response to API requests.
- **AWS Services**: Connect APIs to other AWS services, such as Amazon S3, DynamoDB, or SNS, to interact with various AWS resources.
- **HTTP Endpoints**: Route API requests to HTTP endpoints or services hosted outside of AWS.

### Security

- **IAM Roles and Policies**: Control access to your APIs using IAM roles and policies.
- **API Keys**: Use API keys to manage and control access to your APIs.
- **OAuth 2.0**: Implement OAuth 2.0 authorization for secure access to your APIs.

### Monitoring and Analytics

- **CloudWatch Integration**: Monitor API performance, set up alarms, and collect metrics with Amazon CloudWatch.
- **API Gateway Metrics**: Track metrics such as request count, latency, and error rates directly within API Gateway.

## Usage Scenarios

AWS API Gateway is ideal for:

- **Building APIs**: Develop and deploy APIs that connect web or mobile applications to backend services.
- **Microservices**: Manage and orchestrate microservices with different endpoints and integrations.
- **Serverless Architectures**: Integrate with AWS Lambda to create serverless applications with minimal management.


## AWS API Gateway Architecture

AWS API Gateway architecture consists of several key components that work together to manage and expose APIs:

### 1. API Gateway

- **Description:** The core component that provides the endpoint for clients to interact with. API Gateway handles request processing, routing, and response formatting.
- **Architecture:** 
  - **API Stages:** Different versions of an API are deployed to stages. Each stage can have different settings and configurations.
  - **Resources:** Represents the paths and endpoints for the API.
  - **Methods:** HTTP methods (GET, POST, PUT, DELETE) attached to resources.
- **Use Case:** A company wants to expose its backend services via a RESTful API. API Gateway provides a unified endpoint for clients to interact with these services.
- **Billing Details:** Charges are based on the number of API calls, the amount of data transferred, and additional features like caching.
- **Commands:**
```bash
  # Create a new API
  aws apigateway create-rest-api --name "MyAPI"

  # Deploy an API to a stage
  aws apigateway create-deployment --rest-api-id <api-id> --stage-name <stage-name>
```
2. Resources
Description: Defines the URIs (paths) in the API, representing different endpoints.
Architecture:
Path: Represents the URL path in the API.
Resource Methods: Methods (GET, POST, etc.) associated with the resource path.
Use Case: To create a REST API for an e-commerce platform, resources are defined for endpoints like /products and /orders.
Billing Details: No additional cost for resources; costs are part of the overall API Gateway usage.
YAML Code:
```yaml
# Define a resource in OpenAPI specification
paths:
  /products:
    get:
      summary: Retrieve all products
      responses:
        '200':
          description: List of products
```
3. Methods
Description: The HTTP methods (e.g., GET, POST, PUT, DELETE) that can be applied to resources.
Architecture:
Integration: Specifies how the method interacts with backend services (e.g., Lambda functions, HTTP endpoints).
Method Request and Response: Configurations for request validation and response formatting.
Use Case: An API for a payment gateway with methods like POST to create transactions and GET to retrieve transaction history.
Billing Details: Costs based on the number of API calls and the data transferred.
YAML Code:
```yaml
# Define methods in OpenAPI specification
paths:
  /transactions:
    post:
      summary: Create a new transaction
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                amount:
                  type: number
      responses:
        '201':
          description: Transaction created

```
4. Integration
Description: Configures how API Gateway integrates with backend services.
Architecture:
Lambda Integration: API Gateway invokes AWS Lambda functions.
HTTP Integration: API Gateway routes requests to HTTP endpoints.
Mock Integration: API Gateway returns static responses without invoking a backend.
Use Case: An API endpoint that triggers an AWS Lambda function to process data and return a result.
Billing Details: Charges are based on the number of Lambda invocations or HTTP requests.

Commands:
```bash
# Set up Lambda integration for a method
aws apigateway put-integration --rest-api-id <api-id> --resource-id <resource-id> --http-method POST --type AWS_PROXY --integration-http-method POST --uri arn:aws:lambda:region:account-id:function:function-name

```
5. Stages
Description: Deployment stages of the API, representing different versions or environments (e.g., development, staging, production).
Architecture:
Stage Variables: Key-value pairs that are available to the API and backend integration.
Deployment History: Tracks changes and deployments for each stage.
Use Case: Different stages are used to test new features in a staging environment before promoting them to production.
Billing Details: Costs are associated with the API calls made to different stages and the data transferred.

Commands:
```bash
# Create a deployment for a stage
aws apigateway create-deployment --rest-api-id <api-id> --stage-name <stage-name>

```
6. Custom Domain Names
Description: Allows APIs to be accessed via custom domain names instead of default API Gateway endpoints.
Architecture:
Domain Name Mapping: Maps custom domain names to API Gateway APIs.
SSL Certificates: Secure custom domains with SSL/TLS certificates.
Use Case: An organization wants to use its branded domain name (e.g., api.example.com) for accessing APIs.
Billing Details: Charges for custom domain names include the cost of SSL certificate management and custom domain name setup.
Commands:
```bash
# Create a custom domain name
aws apigateway create-domain-name --domain-name <custom-domain-name> --certificate-arn <certificate-arn>

```
7. Caching
Description: API Gateway can cache responses to reduce backend load and improve performance.
Architecture:
Cache Capacity: Configurable based on the cache size and time-to-live (TTL) settings.
Use Case: Caching responses for frequently accessed data to minimize backend processing and improve response times.
Billing Details: Charges based on cache capacity and data transfer.
Commands:
```bash
# Enable caching for a stage
aws apigateway update-stage --rest-api-id <api-id> --stage-name <stage-name> --patch-operations op=replace,path=/cacheClusterSize,value=0.5

```
8. Throttling and Rate Limiting
Description: Control the rate of requests to the API to prevent abuse and ensure fair usage.
Architecture:
Usage Plans: Define rate limits and quotas for API access.
Use Case: An API that enforces rate limits to prevent overuse by individual clients and ensure service availability.
Billing Details: Costs are related to the number of requests and any additional usage plans.
Commands:
```bash
# Create a usage plan
aws apigateway create-usage-plan --name <usage-plan-name> --api-stages apiId=<api-id>,stage=<stage-name>

```
Billing Details
Cost Factors
API Calls: Charges based on the number of API requests processed by API Gateway.
Data Transfer: Costs associated with the amount of data transferred out of API Gateway.
Caching: Costs for cache capacity and data transfer.
Custom Domain Names: Charges for custom domain name setup and SSL certificates.
Additional Features: Costs for features such as usage plans, throttling, and rate limiting.
Pricing Tiers
Basic Pricing: Includes standard API Gateway usage and data transfer costs.
Advanced Features: Additional charges for caching, custom domain names, and advanced usage plans.
For detailed and up-to-date pricing information, refer to the AWS Pricing Calculator and the AWS API Gateway pricing page.