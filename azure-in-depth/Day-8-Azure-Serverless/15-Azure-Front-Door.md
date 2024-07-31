# Azure Front Door

Azure Front Door is a scalable and secure entry point for fast delivery of your global applications. It provides high availability and low latency by distributing traffic across multiple regions. Azure Front Door also offers features like SSL offloading, URL-based routing, and application firewall.

## Azure Front Door Architecture

Azure Front Door's architecture consists of several components that work together to optimize the performance, security, and reliability of web applications:

### 1. Front Door Profile
   - **Description:** A Front Door profile defines the configuration and settings for your application delivery, including routing, health probes, and security policies.
   - **Architecture:** 
     - **Routing Rules:** Determine how traffic is directed based on criteria such as URL path, HTTP headers, or request methods.
     - **Backend Pools:** A group of backend endpoints (e.g., web servers, APIs) that handle requests routed through Front Door.
   - **Use Case:** A global e-commerce website uses Azure Front Door to distribute user requests to the nearest backend server, ensuring fast response times and high availability.
   - **Billing Details:** Charges based on routing rules, data transfer, and optional services like Web Application Firewall (WAF).
   - **Commands:**
     ```bash
     # Create a Front Door profile
     az network front-door create --resource-group <ResourceGroupName> --name <FrontDoorName> --backend-address <BackendAddress>
     
     # Update routing rules
     az network front-door routing-rule update --resource-group <ResourceGroupName> --front-door-name <FrontDoorName> --name <RoutingRuleName> --backend-pool <BackendPoolName>
     ```

### 2. Backend Pools
   - **Description:** Backend pools consist of one or more backend endpoints that serve incoming requests. They can be hosted anywhere, such as in Azure, on-premises, or in other clouds.
   - **Architecture:** 
     - **Backend Endpoints:** Defined by FQDN or IP address, associated with load balancing settings and health probes.
   - **Use Case:** An application with multiple microservices running in different Azure regions uses backend pools to route traffic to the appropriate service based on user location.
   - **Billing Details:** Costs depend on the number of requests and data transfer between Front Door and backend pools.
   - **Commands:**
     ```bash
     # Add a backend pool
     az network front-door backend-pool create --resource-group <ResourceGroupName> --front-door-name <FrontDoorName> --name <BackendPoolName> --backend-address <BackendAddress>
     ```

### 3. Routing Rules
   - **Description:** Define how requests are routed to backend pools based on specific criteria, such as URL paths or request headers.
   - **Architecture:** 
     - **Path-Based Routing:** Directs traffic to different backend pools based on URL paths.
     - **Priority Routing:** Assigns priorities to backend pools, allowing traffic to be rerouted in case of failure.
   - **Use Case:** A multi-tenant SaaS application uses routing rules to direct customer requests to different backend pools based on the subdomain or URL path.
   - **Billing Details:** Charges for routing rule configurations and data transfer.
   - **YAML Configuration:**
     ```yaml
     routes:
     - name: my-route
       patternsToMatch: 
       - "/*"
       backendPool: 
         name: my-backend-pool
     ```

### 4. Health Probes
   - **Description:** Periodically checks the health of backend endpoints. Determines endpoint availability and helps Front Door make informed routing decisions.
   - **Architecture:** 
     - **Probe Configuration:** Define probe paths, intervals, and protocols to monitor endpoint health.
   - **Use Case:** A critical application uses health probes to ensure traffic is only routed to healthy backend endpoints, improving reliability.
   - **Billing Details:** No additional costs for health probes, but they influence the availability and reliability of backend routing.
   - **Commands:**
     ```bash
     # Create a health probe
     az network front-door probe create --resource-group <ResourceGroupName> --front-door-name <FrontDoorName> --name <ProbeName> --path "/health" --protocol Http --interval 30
     ```

### 5. Web Application Firewall (WAF)
   - **Description:** Provides centralized protection for your web applications from common threats and vulnerabilities. WAF policies can be defined to block, allow, or monitor requests.
   - **Architecture:** 
     - **WAF Policies:** Includes custom rules and managed rule sets to protect against common attacks like SQL injection and cross-site scripting.
   - **Use Case:** A financial services company uses WAF to protect its online banking portal from malicious attacks while allowing legitimate traffic.
   - **Billing Details:** Additional charges for WAF policies based on the number of rules and data processed.
   - **Commands:**
     ```bash
     # Create a WAF policy
     az network front-door waf-policy create --resource-group <ResourceGroupName> --name <WAFPolicyName>

     # Associate a WAF policy with a Front Door
     az network front-door update --resource-group <ResourceGroupName> --name <FrontDoorName> --waf-policy <WAFPolicyName>
     ```

## Use Cases of Azure Front Door

1. **Global Application Acceleration**
   - **Scenario:** A media streaming service needs to deliver content to users worldwide with minimal latency.
   - **Solution:** Azure Front Door routes user requests to the nearest regional server, reducing latency and providing fast, responsive access to media content.

2. **High Availability for E-commerce Platforms**
   - **Scenario:** An e-commerce website experiences fluctuating traffic demands during sales events.
   - **Solution:** Azure Front Door distributes incoming requests across multiple regions and backend servers, ensuring high availability and resilience during peak traffic periods.

3. **Centralized Security Management**
   - **Scenario:** A healthcare provider needs to secure its web applications from common vulnerabilities and attacks.
   - **Solution:** Azure Front Door integrates with Azure WAF, offering centralized management of security policies to protect against threats like SQL injection and cross-site scripting.

## Billing Details

### Cost Factors

1. **Requests and Data Transfer:** Charges are based on the number of requests processed by Front Door and the amount of data transferred.
2. **Routing Rules:** Costs for the configuration and execution of routing rules.
3. **Web Application Firewall (WAF):** Additional charges for WAF policies, depending on the number of rules and data processed.

### Pricing Tiers

- **Standard Pricing:** Includes base costs for request processing and data transfer.
- **Premium Features:** Additional costs for WAF and advanced routing configurations.

For detailed and up-to-date pricing information, refer to the [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/) and the [Azure Front Door pricing page](https://azure.microsoft.com/en-us/pricing/details/frontdoor/).

This README provides a comprehensive overview of Azure Front Door, including its components, architecture, use cases, billing details, and relevant commands and configurations. It serves as a guide for understanding and leveraging Azure Front Door to optimize application performance and security.
