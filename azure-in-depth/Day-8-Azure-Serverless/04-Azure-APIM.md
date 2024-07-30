# Azure API Management (APIM)

Azure API Management (APIM) is a fully managed service by Microsoft Azure that helps organizations publish, manage, secure, and analyse APIs. It provides a comprehensive suite of tools for creating and managing APIs with robust security, performance, and scalability.

## APIM Architecture

Azure API Management (APIM) architecture includes several key components that work together to manage and secure APIs:

### 1. API Management Service
   - **Description:** The core component of Azure APIM, responsible for handling API requests, applying policies, and managing traffic.
   - **Architecture:**
     - **Gateway:** Processes incoming API requests and applies policies for authentication, caching, transformation, etc.
     - **Management Plane:** Provides a user interface and APIs for managing APIs, users, and policies.
     - **Developer Portal:** A customizable portal where developers can discover, test, and subscribe to APIs.
   - **Use Case:** An enterprise needs to expose its internal APIs securely to external partners. Azure APIM provides a centralized platform for managing these APIs, enforcing security policies, and analysing usage.
   - **Billing Details:** Costs are based on the tier of the APIM instance (Developer, Basic, Standard, Premium) and the number of API calls, data transfer, and additional features like caching and developer portal customization.
   - **Commands:**
     ```bash
     # Create an API Management service
     az apim create --resource-group <ResourceGroupName> --name <APIMServiceName> --publisher-email <PublisherEmail> --publisher-name <PublisherName> --location <Location>

     # List all API Management services in a resource group
     az apim list --resource-group <ResourceGroupName>
     ```

### 2. APIs
   - **Description:** Represents the set of endpoints exposed through API Management. APIs define the operations and request/response formats.
   - **Architecture:**
     - **Frontend:** The interface exposed to consumers. Can include multiple versions and revisions.
     - **Backend:** The actual implementation of the API, which could be hosted on Azure services or other external systems.
   - **Use Case:** A company wants to expose its internal microservices as APIs to external developers. They use Azure APIM to create and manage these APIs, ensuring consistent and secure access.
   - **Billing Details:** Costs are included in the overall APIM service pricing, with additional charges for API calls and data transfer.
   - **YAML Code:**
     ```yaml
     apiVersion: apimanagement.azure.com/v1
     kind: Api
     metadata:
       name: my-api
     spec:
       displayName: My API
       serviceUrl: https://mybackend.example.com/api
       protocols:
         - https
       operations:
         - displayName: Get Data
           method: GET
           urlTemplate: /data
           response:
             status: 200
             description: OK
     ```

### 3. Policies
   - **Description:** Rules applied to API requests and responses to control behaviour, enforce security, and perform transformations.
   - **Architecture:**
     - **Inbound Policies:** Applied before the request is forwarded to the backend.
     - **Backend Policies:** Applied to the request after it reaches the backend.
     - **Outbound Policies:** Applied before the response is sent to the client.
   - **Use Case:** To enforce rate limiting and request validation on an API, policies are used to throttle requests and validate inputs before processing them.
   - **Billing Details:** Policy usage is included in the overall APIM pricing. Charges may apply for advanced policies and custom policy implementations.
   - **YAML Code:**
     ```yaml
     apiVersion: apimanagement.azure.com/v1
     kind: Policy
     metadata:
       name: rate-limit-policy
     spec:
       inbound:
         - rate-limit-by-key:
             key: subscription-key
             rate-limit: 100
             per: 1m
       outbound:
         - set-header:
             name: X-Custom-Header
             value: custom-value
     ```

### 4. Developer Portal
   - **Description:** A customizable portal for developers to explore, test, and subscribe to APIs.
   - **Architecture:**
     - **Public Portal:** Accessible to developers for discovering APIs, viewing documentation, and testing endpoints.
     - **Customization:** Allows for branding and layout modifications to fit organizational needs.
   - **Use Case:** A company customizes the developer portal to include its branding and provides detailed API documentation and interactive API testing for third-party developers.
   - **Billing Details:** Customization and traffic to the developer portal are included in the overall APIM service pricing.
   - **Commands:**
     ```bash
     # Enable the developer portal
     az apim update --resource-group <ResourceGroupName> --name <APIMServiceName> --set portal=True

     # Configure custom portal settings
     az apim portal update --resource-group <ResourceGroupName> --name <APIMServiceName> --set <SettingName>=<SettingValue>
     ```

### 5. Subscriptions
   - **Description:** Allows users to access and consume APIs by subscribing to them. Subscriptions can have different access levels and quotas.
   - **Architecture:**
     - **Subscription Keys:** Used to authenticate API requests and manage access control.
   - **Use Case:** An API provider offers multiple subscription tiers (e.g., Free, Standard, Premium) with varying levels of access and rate limits. Users subscribe to these tiers based on their needs.
   - **Billing Details:** Costs are associated with the number of active subscriptions and the tier of the API Management instance.
   - **Commands:**
     ```bash
     # Create a new subscription
     az apim subscription create --resource-group <ResourceGroupName> --service-name <APIMServiceName> --name <SubscriptionName> --display-name <DisplayName>
     ```

### 6. Analytics and Monitoring
   - **Description:** Provides insights into API usage, performance, and error rates. Useful for identifying issues and optimizing API performance.
   - **Architecture:**
     - **Metrics:** Track API calls, response times, and error rates.
     - **Logs:** Capture detailed information about API requests and responses.
   - **Use Case:** An API provider uses analytics to monitor traffic patterns, identify performance bottlenecks, and optimize API endpoints for better performance.
   - **Billing Details:** Analytics and monitoring are included in the APIM service pricing, but additional charges may apply for Azure Monitor and Log Analytics.
   - **Commands:**
     ```bash
     # Enable Application Insights for monitoring
     az apim update --resource-group <ResourceGroupName> --name <APIMServiceName> --set diagnosticSettings[0].workspaceId=<WorkspaceId>

     # View API analytics
     az apim api list --resource-group <ResourceGroupName> --service-name <APIMServiceName>
     ```

## Billing Details

### Cost Factors

1. **Service Tier:** Azure API Management offers different pricing tiers (Developer, Basic, Standard, Premium) with varying features and capacities.
2. **API Calls:** Charges based on the number of API calls processed by the APIM instance.
3. **Data Transfer:** Costs for outbound data transfer from APIM.
4. **Developer Portal:** Customization and traffic to the developer portal are included in the service pricing.
5. **Additional Features:** Costs for features like caching, Application Insights integration, and additional policies.

### Pricing Tiers

- **Developer Tier:** Intended for development and testing environments. Includes limited capacity and features.
- **Basic Tier:** Suitable for small to medium-sized production workloads. Provides more features and capacity.
- **Standard Tier:** Designed for larger production environments with more advanced features and higher capacity.
- **Premium Tier:** Includes advanced features for global deployments and high-availability requirements.

For detailed and up-to-date pricing information, refer to the [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/) and the [Azure API Management pricing page](https://azure.microsoft.com/en-us/pricing/details/api-management/).

This README provides a comprehensive overview of Azure API Management (APIM), including its components, architecture, use cases, billing details, and relevant commands and YAML code. It serves as a detailed guide for understanding and managing Azure APIM in various scenarios.
