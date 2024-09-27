# Table of Contents

- [Azure Storage](#azure-storage)
    - [Blob Storage](#blob-storage)
    - [File Storage](#file-storage)
    - [Queue Storage](#queue-storage)
    - [Table Storage](#table-storage)
    - [Disk Storage](#disk-storage)

## Azure Storage
Azure Storage is a cloud-based storage solution provided by Microsoft Azure. It offers a variety of storage services that can be used to store and manage large amounts of data.
### Generally Azure storage used in three category
1) Storage for virtual machine (virtual machine disks and files)
2) Unstructured data (blobs and DATALAKE stores)
3) Structured Data (table SQL cosmos DB)

## Blob Storage
Azure Blob Storage is a service that allows you to store and serve large amounts of unstructured data, such as text or binary files. It is commonly used for storing and serving static website content. 
For example, you can store HTML, CSS, JavaScript, and image files for a website in Blob Storage and serve them directly to users.

## Blob Containers & Categories
### Containers
Blobs are used to store unstructured data like unmanaged disks, text files or binary data.
We can create multiple blobs under one container and multiple containers under one storage account.

### Blob storage Categories
We have three categories in blob

1) **Block Blob**
when we store any file, video and image it will be saved as "Block Blob"
It store text and binary data, Block blob are block of data that can be managed individually.

2) **Page Blob**
It store random access files up to 8 TB in size. Page blobs stores Virtual hard drive (VHD) files and serve as disks for virtual machines.

3) **Append Blob**
Append blob are made up of blocks like block blobs, but are optimized for append operations. Append blobs are ideal for scenarios such as logging data from VM.

## File Storage
Azure File Storage provides a fully managed file share in the cloud. It allows you to create file shares that can be accessed from multiple virtual machines or on-premises servers. These files can be accessed by using the standard server message block (SMB) protocol. This makes it easy to share files between different applications and environments.

## Queue Storage
Azure Queue Storage is a service that allows you to store and retrieve large numbers of messages. It provides reliable message delivery between components of distributed applications. You can use Queue Storage to build scalable and decoupled applications that can handle high message volumes.
The max size of message is 64kb in size.

## Table Storage
Azure Table Storage is a NoSQL key-value store that can store large amounts of structured data. It is a good choice for storing structured data that does not require complex querying or transactions. Table Storage is highly scalable and can handle large amounts of data.

## Disk Storage
Azure Disk Storage provides durable and high-performance block storage for virtual machines. It allows you to attach disks to virtual machines and use them as persistent storage. Disk Storage is commonly used for storing operating system disks, data disks, and temporary disks for virtual machines.

These are the main types of Azure Storage and their real-time use cases. Each type offers different capabilities and is suitable for different scenarios. For more information, please refer to the official Azure Storage documentation.


## Storage Account Performance
Azure Storage provides different performance tiers for storage accounts. The performance tier determines the level of performance and scalability that is available for your storage account.

There are two performance tiers available for Azure Blob Storage and Azure File Storage:

1. **Standard**: This is the default performance tier and offers a balance between cost and performance. It is suitable for most general-purpose workloads.
1) Are backed up by HDD (Magnetic drives)
2) Lowest cost per GB
3) Best for applications that require bulk storage
4) Data is accessed infrequently (means high latency)

2. **Premium**: This performance tier offers higher performance and lower latency compared to the Standard tier. It is designed for high-performance workloads that require low latency and high throughput.
1) Are backed up by SSD
2) Offer consistent low latency performance
3) Use with Azure Virtual machine disks
4) Best for I/O intensive application like database

For Azure Queue Storage and Azure Table Storage, there is only one performance tier available, which is the **Standard** tier.

## Azure Storage kinds

### General purpose V1
Legacy account type for blobs, files and queues and tables. Try to use General purpose V2 accounts because in this account may not have all the latest feature.
1) It supports service only like Blob, File, Queue, Table and disk.
2) It does not support any access like HOT and Cool.
3) It supports only replication like LRS, GRS, RA- GRS.
4) It supports both standard and premium performance tier.

### General purpose V2
Both basic and latest account type for blob, files, queues and tables. Recommended for most scenario using azure storage and Microsoft also recommend to use this type of account.
1) It supports services like Blobs, files Queue, table , disk and Data Lake Gen 2
2) It supports any access like HOT, Cool and Archive.
3) It supports replication like LRS, GRS, RA-GRS, ZRS, GZRS, RA-GZRS 
4) It supports both standard and premium performance tier.

### Blob storage
The blob storage is used for storing unstructured data

1) It supports only services of Blob (block blobs and append blobs only)
2) It supports only standard performance tier
3) It supports access tier like Hot, Cool, Archive
4) It supports only replication like LRS, GRS, RA- GRS.

# Azure Storage Performance Tiers

Azure Storage offers different performance tiers to optimize storage costs based on how frequently you access your data. Here’s a breakdown of the Hot, Cool, and Archive tiers:

## Hot Tier
The Hot tier is designed for data that is accessed frequently. It offers the lowest latency and highest throughput for read and write operations.

- **Use case**: Data that is accessed and modified often, such as active documents, media files, and application data.
- **Characteristics**:
  - Lowest access costs
  - Higher storage costs compared to Cool and Archive tiers

## Cool Tier
The Cool tier is designed for data that is infrequently accessed and stored for at least 30 days. It provides a balance between storage and access costs.

- **Use case**: Data that is accessed less frequently but needs to be retained for a longer period, such as backups, older documents, and media files that are not frequently viewed.
- **Characteristics**:
  - Lower storage costs compared to the Hot tier
  - Higher access costs compared to the Hot tier
  - Minimum retention period of 30 days


## Cold Tier
The Cold tier is designed for data that is infrequently accessed and stored for at least 90 days.

- **Use case**: Data that is accessed less frequently but needs to be retained for a longer period, such as backups, older documents, and media files that are not frequently viewed.
- **Characteristics**:
  - Lower storage costs compared to the Hot tier
  - Higher access costs compared to the Hot tier
  - Minimum retention period of 90 days

## Archive Tier
The Archive tier is designed for data that is rarely accessed and stored for at least 180 days. It offers the lowest storage costs but has higher latency and costs for accessing the data.

- **Use case**: Long-term storage of data that is rarely accessed, such as compliance records, long-term backups, and archival data.
- **Characteristics**:
  - Lowest storage costs
  - Highest access costs and latency
  - Minimum retention period of 180 days
  - Requires rehydration to Hot or Cool tier before the data can be accessed

## Choosing the Right Performance Tier
When selecting a performance tier, consider the following factors:
- **Access frequency**: How often do you need to access your data?
- **Retention period**: How long will you store the data before it can be deleted or moved to a lower-cost tier?
- **Cost**: Balance the storage and access costs based on your data usage patterns.

By choosing the appropriate performance tier, you can optimize your storage costs while ensuring that your data is available when you need it.


## Storage Replication
Azure Storage Replication refers to the different options available for replicating data in Azure Storage. Replication is important for ensuring data durability, availability, and disaster recovery.

### In Azure Storage, there are six types of replication:
Azure provides several redundancy options to ensure data availability and durability. Here are the different redundancy options explained:

### Locally Redundant Storage (LRS)
LRS replicates your data three times within a single data centre in a region. This ensures data durability by keeping multiple copies, but it does not protect against data centre-level failures.

- **Use case**: Cost-effective redundancy within a single data centre.
- **Data replication**: 3 copies in one data centre.

### Zone-Redundant Storage (ZRS)
ZRS replicates your data synchronously across three Azure availability zones within a region. This provides higher durability and availability compared to LRS.

- **Use case**: Protect against data centre-level failures within a region.
- **Data replication**: Synchronous replication across 3 availability zones.

### Geo-Redundant Storage (GRS)
GRS replicates your data to a secondary region that is hundreds of miles away from the primary region. It offers protection against regional outages.

- **Use case**: Disaster recovery with data replication across regions.
- **Data replication**: Asynchronous replication to a secondary region, 6 copies in total (3 in the primary region and 3 in the secondary region).

### Read-Access Geo-Redundant Storage (RA-GRS)
RA-GRS provides the same replication as GRS but with read access to the data in the secondary region. This allows for read-only access to your data even if the primary region is unavailable.

- **Use case**: Disaster recovery with read access to secondary region data.
- **Data replication**: Asynchronous replication to a secondary region with read access, 6 copies in total.

### Geo-Zone-Redundant Storage (GZRS)
GZRS combines the benefits of ZRS and GRS. It synchronously replicates your data across three availability zones in the primary region and asynchronously replicates it to a secondary region.

- **Use case**: High availability and durability with protection against both data centre and regional failures.
- **Data replication**: Synchronous replication across 3 availability zones and asynchronous replication to a secondary region, 6 copies in total.

### Read-Access Geo-Zone-Redundant Storage (RA-GZRS)
RA-GZRS provides the same replication as GZRS but with read access to the data in the secondary region. This ensures that your data is available for read-only access even if the primary region is unavailable.

- **Use case**: High availability, durability, and read access to secondary region data.
- **Data replication**: Synchronous replication across 3 availability zones and asynchronous replication to a secondary region with read access, 6 copies in total.


