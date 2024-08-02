# Azure Cosmos DB

Azure Cosmos DB is a globally distributed, multi-model database service provided by Microsoft Azure. It offers turnkey global distribution, elastic scaling of throughput and storage, and comprehensive service level agreements (SLAs) for latency, availability, consistency, and throughput. This document provides an in-depth overview of Azure Cosmos DB, including its architecture, components, use cases, billing details, and relevant commands.

## Azure Cosmos DB Architecture

Azure Cosmos DB is designed for modern application development with the following architectural features:

### 1. Global Distribution
   - **Description:** Azure Cosmos DB allows you to distribute your data globally with a few clicks. It supports multiple regions and automatically replicates your data to ensure low latency and high availability.
   - **Architecture:** 
     - **Multi-Region Writes:** Enables writing data to any region with low latency.
     - **Automatic Failover:** Ensures high availability with automatic failover capabilities.
   - **Use Case:** A global e-commerce platform needs low-latency access to its product catalog. By using Azure Cosmos DB, the platform can serve users from the nearest geographic region.
   - **Billing Details:** Charges are based on the number of regions and the amount of data replicated. Additional costs for multi-region writes.
   - **Commands:**
     ```bash
     # Enable multi-region writes
     az cosmosdb update --name <CosmosDBAccountName> --resource-group <ResourceGroupName> --enable-multiple-write-locations true
     ```

### 2. Multi-Model Support
   - **Description:** Azure Cosmos DB supports various data models, including document, key-value, graph, and column-family, allowing flexibility in how data is stored and accessed.
   - **Architecture:** 
     - **Core (SQL) API:** For document data model.
     - **MongoDB API:** For MongoDB applications.
     - **Cassandra API:** For column-family data model.
     - **Gremlin API:** For graph data model.
     - **Table API:** For key-value data model.
   - **Use Case:** A social media application uses the Gremlin API to model user relationships and interactions as a graph.
   - **Billing Details:** Costs depend on the provisioned throughput and storage used, regardless of the data model.
   - **Commands:**
     ```bash
     # Create a Cosmos DB account with MongoDB API
     az cosmosdb create --name <CosmosDBAccountName> --resource-group <ResourceGroupName> --kind MongoDB
     ```

### 3. Consistency Levels
   - **Description:** Azure Cosmos DB provides five consistency levels to balance between consistency, availability, and latency: Strong, Bounded Staleness, Session, Consistent Prefix, and Eventual.
   - **Architecture:** 
     - **Strong:** Guarantees linearizability.
     - **Bounded Staleness:** Guarantees consistent reads within a specified lag.
     - **Session:** Guarantees consistency for a client session.
     - **Consistent Prefix:** Guarantees no out-of-order writes.
     - **Eventual:** Guarantees eventual consistency.
   - **Use Case:** A financial application uses Strong consistency to ensure the accuracy of transaction data across all regions.
   - **Billing Details:** Consistency level affects latency and throughput, potentially impacting costs.
   - **Commands:**
     ```bash
     # Set consistency level to Strong
     az cosmosdb update --name <CosmosDBAccountName> --resource-group <ResourceGroupName> --default-consistency-level Strong
     ```

### 4. Resource Model
   - **Description:** Azure Cosmos DB's resource model includes accounts, databases, containers, items, and offers (provisioned throughput).
   - **Architecture:** 
     - **Account:** The top-level resource representing a Cosmos DB instance.
     - **Database:** A container for users, permissions, containers, and items.
     - **Container:** A schema-agnostic container for items, automatically indexed.
     - **Item:** An individual record in a container.
     - **Offer:** Provisioned throughput for a container or database.
   - **Use Case:** An IoT application uses a single Cosmos DB account with multiple databases, each representing a different IoT device type.
   - **Billing Details:** Costs depend on the provisioned throughput (measured in Request Units per second) and storage used.
   - **Commands:**
     ```bash
     # Create a new database
     az cosmosdb sql database create --account-name <CosmosDBAccountName> --resource-group <ResourceGroupName> --name <DatabaseName>

     # Create a new container with provisioned throughput
     az cosmosdb sql container create --account-name <CosmosDBAccountName> --resource-group <ResourceGroupName> --database-name <DatabaseName> --name <ContainerName> --partition-key-path "/myPartitionKey" --throughput 400
     ```

### 5. Indexing
   - **Description:** Azure Cosmos DB automatically indexes all data, offering rich querying capabilities without requiring schema or secondary indexes.
   - **Architecture:** 
     - **Automatic Indexing:** All fields in items are automatically indexed.
     - **Indexing Policies:** Customizable indexing modes and paths to optimize performance and storage.
   - **Use Case:** A search application uses indexing policies to enhance query performance by excluding certain properties from indexing.
   - **Billing Details:** No additional cost for indexing, but indexing impacts storage and throughput usage.
   - **Commands:**
     ```bash
     # Update indexing policy
     az cosmosdb sql container update --account-name <CosmosDBAccountName> --resource-group <ResourceGroupName> --database-name <DatabaseName> --name <ContainerName> --idx @indexingPolicy.json
     ```

### 6. Security
   - **Description:** Azure Cosmos DB offers advanced security features, including encryption at rest, role-based access control (RBAC), and virtual network service endpoints.
   - **Architecture:** 
     - **Encryption at Rest:** Data is automatically encrypted.
     - **RBAC:** Fine-grained access control to resources.
     - **Private Link:** Securely connects to Azure services over a private endpoint.
   - **Use Case:** A healthcare application uses RBAC to restrict access to patient data based on user roles.
   - **Billing Details:** Security features may affect overall performance but typically do not have direct additional costs.
   - **Commands:**
     ```bash
     # Create a private endpoint
     az network private-endpoint create --name <PrivateEndpointName> --resource-group <ResourceGroupName> --vnet-name <VNetName> --subnet <SubnetName> --private-connection-resource-id <CosmosDBResourceId> --group-ids sql
     ```

## Billing Details

### Cost Factors

1. **Provisioned Throughput:** Charges based on the number of Request Units (RUs) provisioned per second. RUs are consumed by read, write, and query operations.
2. **Storage:** Costs for the amount of data stored in Azure Cosmos DB, including index storage.
3. **Data Transfer:** Charges for data egress across regional boundaries or to external clients.
4. **Global Distribution:** Additional costs for replicating data across multiple regions.

### Pricing Tiers

- **Provisioned Throughput:** Configurable RUs per second, starting at a baseline cost.
- **Serverless:** Pay only for the RUs consumed, ideal for infrequent or unpredictable workloads.

For detailed and up-to-date pricing information, refer to the [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/) and the [Azure Cosmos DB pricing page](https://azure.microsoft.com/en-us/pricing/details/cosmos-db/).

This README provides a comprehensive guide to Azure Cosmos DB, covering its architecture, components, use cases, billing details, and relevant commands. It serves as a valuable resource for understanding and leveraging Azure Cosmos DB in modern applications.
