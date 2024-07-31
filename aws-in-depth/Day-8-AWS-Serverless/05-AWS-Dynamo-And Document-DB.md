
# AWS DynamoDB and Amazon DocumentDB

AWS DynamoDB and Amazon DocumentDB are managed database services offered by Amazon Web Services (AWS). They cater to different use cases and data models, providing high performance and scalability.

## AWS DynamoDB

AWS DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability. It is designed for high-performance applications requiring low-latency data access.

### Components of DynamoDB

#### 1. Tables
   - **Description:** Tables are the primary containers for data in DynamoDB. They store items and their attributes.
   - **Architecture:** Each table has a primary key (partition key and optionally a sort key) that uniquely identifies each item.
   - **Use Case:** An e-commerce application stores product details in a DynamoDB table where the product ID is the primary key.
   - **Billing Details:** Charges based on the number of read and write requests, data storage, and any additional features like DynamoDB Streams.
   - **Commands:**
     ```bash
     # Create a DynamoDB table
     aws dynamodb create-table --table-name Products --attribute-definitions AttributeName=ProductID,AttributeType=N --key-schema AttributeName=ProductID,KeyType=HASH --provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5
     
     # Describe a DynamoDB table
     aws dynamodb describe-table --table-name Products
     ```

#### 2. Items
   - **Description:** Individual records in a DynamoDB table. Each item is a collection of attributes.
   - **Architecture:** Items are stored as JSON-like documents and can have varying attributes.
   - **Use Case:** An item representing a customer in a table includes attributes like CustomerID, Name, and Email.
   - **Billing Details:** Costs are included in the read and write request charges.
   - **Commands:**
     ```bash
     # Put an item into a DynamoDB table
     aws dynamodb put-item --table-name Products --item '{"ProductID": {"N": "101"}, "Name": {"S": "Laptop"}, "Price": {"N": "799"}}'
     
     # Get an item from a DynamoDB table
     aws dynamodb get-item --table-name Products --key '{"ProductID": {"N": "101"}}'
     ```

#### 3. Indexes
   - **Description:** Indexes improve query performance by allowing queries on non-primary key attributes.
   - **Architecture:** Includes Local Secondary Indexes (LSIs) and Global Secondary Indexes (GSIs).
   - **Use Case:** An LSI allows querying products by category while the GSI allows querying by price range.
   - **Billing Details:** Charges are based on index read and write capacity, and additional storage.
   - **Commands:**
     ```bash
     # Create a Global Secondary Index (GSI)
     aws dynamodb update-table --table-name Products --attribute-definitions AttributeName=Category,AttributeType=S --global-secondary-index-updates '[{"Create":{"IndexName":"CategoryIndex","KeySchema":[{"AttributeName":"Category","KeyType":"HASH"}],"Projection":{"ProjectionType":"ALL"},"ProvisionedThroughput":{"ReadCapacityUnits":5,"WriteCapacityUnits":5}}]}'
     ```

#### 4. Streams
   - **Description:** DynamoDB Streams capture changes to items in a table and allow for event-driven processing.
   - **Architecture:** Streams provide a time-ordered sequence of item-level changes.
   - **Use Case:** An application updates a search index when items in a DynamoDB table change.
   - **Billing Details:** Charges based on the data processed by streams and the associated Lambda functions.
   - **Commands:**
     ```bash
     # Enable DynamoDB Streams on a table
     aws dynamodb update-table --table-name Products --stream-specification StreamEnabled=true,StreamViewType=NEW_AND_OLD_IMAGES
     
     # List stream ARN
     aws dynamodb describe-table --table-name Products --query 'Table.StreamArn'
     ```

## Amazon DocumentDB

Amazon DocumentDB is a fully managed document database service that is compatible with MongoDB. It is designed for scalable, high-performance document database use cases.

### Components of DocumentDB

#### 1. Clusters
   - **Description:** A cluster is a set of instances and a primary node that manages read and write operations.
   - **Architecture:** Includes one primary instance and multiple replica instances for read scaling and high availability.
   - **Use Case:** A social media application uses a DocumentDB cluster to handle user profiles and posts, with replica instances to distribute read traffic.
   - **Billing Details:** Charges are based on the instance types, storage used, and data transfer.
   - **Commands:**
     ```bash
     # Create a DocumentDB cluster
     aws docdb create-db-cluster --db-cluster-identifier my-cluster --master-username admin --master-user-password password --engine docdb
     
     # Describe a DocumentDB cluster
     aws docdb describe-db-clusters --db-cluster-identifier my-cluster
     ```

#### 2. Instances
   - **Description:** Instances are the compute resources within a DocumentDB cluster. They handle database queries and data processing.
   - **Architecture:** Instances include one primary instance and zero or more replica instances.
   - **Use Case:** A web application deploys multiple DocumentDB instances to handle high query loads and ensure fault tolerance.
   - **Billing Details:** Costs depend on the instance type and the number of instances.
   - **Commands:**
     ```bash
     # Create a DocumentDB instance
     aws docdb create-db-instance --db-instance-identifier my-instance --db-cluster-identifier my-cluster --instance-class db.r5.large
     
     # Describe DocumentDB instances
     aws docdb describe-db-instances --db-instance-identifier my-instance
     ```

#### 3. Snapshots
   - **Description:** Snapshots are backups of your DocumentDB cluster data, taken at specific points in time.
   - **Architecture:** Snapshots provide a way to restore the cluster to a previous state.
   - **Use Case:** A company schedules automated snapshots to ensure data recovery in case of accidental data loss.
   - **Billing Details:** Charges are based on the amount of storage used for snapshots.
   - **Commands:**
     ```bash
     # Create a snapshot of a DocumentDB cluster
     aws docdb create-db-cluster-snapshot --db-cluster-snapshot-identifier my-snapshot --db-cluster-identifier my-cluster
     
     # Describe snapshots
     aws docdb describe-db-cluster-snapshots --db-cluster-snapshot-identifier my-snapshot
     ```

#### 4. Parameter Groups
   - **Description:** Parameter groups allow you to manage database configuration settings for your DocumentDB instances.
   - **Architecture:** Includes custom and default parameter groups for instance configuration.
   - **Use Case:** Customize settings for memory, performance, or security configurations specific to your application needs.
   - **Billing Details:** No additional cost for parameter groups, but they influence the instance performance and cost.
   - **Commands:**
     ```bash
     # Create a custom parameter group
     aws docdb create-db-cluster-parameter-group --db-cluster-parameter-group-name my-parameter-group --db-parameter-group-family docdb-3.6 --description "My custom parameter group"
     
     # Describe parameter groups
     aws docdb describe-db-cluster-parameter-groups --db-cluster-parameter-group-name my-parameter-group
     ```

## Billing Details

### Cost Factors for DynamoDB

1. **Read and Write Requests:** Charges for the number of read and write operations on the tables.
2. **Storage:** Costs based on the amount of data stored in DynamoDB tables.
3. **Indexes:** Additional charges for using Global Secondary Indexes and Local Secondary Indexes.
4. **Streams:** Costs for data processed by DynamoDB Streams and any associated Lambda functions.

### Cost Factors for Amazon DocumentDB

1. **Instance Hours:** Charges for the compute instances in the DocumentDB cluster.
2. **Storage:** Costs based on the amount of storage used for data and snapshots.
3. **Data Transfer:** Charges for data transferred in and out of the DocumentDB cluster.
4. **Snapshots:** Costs associated with snapshot storage.

For detailed and up-to-date pricing information, refer to the [AWS DynamoDB pricing page](https://aws.amazon.com/dynamodb/pricing/) and the [Amazon DocumentDB pricing page](https://aws.amazon.com/documentdb/pricing/).

This README provides an overview of AWS DynamoDB and Amazon DocumentDB, including their components, architecture, use cases, billing details, and relevant commands and code snippets. It serves as a comprehensive guide for understanding and managing these AWS database services.
