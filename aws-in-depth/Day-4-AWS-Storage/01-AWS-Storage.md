# AWS Storage Services

AWS provides a variety of storage solutions tailored for different needs. This document offers an in-depth overview of AWS Storage services, including architecture, use cases, billing details, and relevant commands and configuration examples.

## 1. Amazon S3 (Simple Storage Service)

### Overview
Amazon S3 is a scalable object storage service designed for storing and retrieving any amount of data from anywhere on the web.

### Architecture
- **Buckets:** Containers for storing objects. Each bucket has a unique name within AWS.
- **Objects:** The fundamental entities stored in S3, including data and metadata.
- **Access Control:** Managed via bucket policies, IAM roles, and access control lists (ACLs).

### Use Cases
1. **Backup and Restore**
   - **Scenario:** A company needs to back up its critical data and ensure it can be restored if needed.
   - **Solution:** Store backup data in S3 with lifecycle policies to transition older backups to cheaper storage classes like S3 Glacier.

2. **Data Archiving**
   - **Scenario:** An organization needs to archive infrequently accessed data.
   - **Solution:** Use S3 Glacier for long-term archival with lower costs compared to S3 Standard.

3. **Static Website Hosting**
   - **Scenario:** A business wants to host a static website.
   - **Solution:** Configure an S3 bucket for static website hosting and use Route 53 for domain management.

### Billing Details
- **Storage Costs:** Based on the amount of data stored and the storage class (e.g., Standard, Intelligent-Tiering, Glacier).
- **Data Transfer Costs:** Charges for data transferred out of S3 to the internet or other AWS regions.
- **Request Costs:** Charges for requests to S3 (e.g., PUT, GET).

### Commands
```bash
# Create an S3 bucket
aws s3api create-bucket --bucket my-bucket --region us-west-1

# Upload a file to an S3 bucket
aws s3 cp my-file.txt s3://my-bucket/

# List objects in an S3 bucket
aws s3 ls s3://my-bucket/
```
YAML Configuration
```JSON
# Example S3 bucket policy allowing public read access
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-bucket/*"
    }
  ]
}

```
2. Amazon EBS (Elastic Block Store)
Overview
Amazon EBS provides persistent block storage for Amazon EC2 instances. It allows you to create and attach volumes to instances for data storage.

Architecture
Volumes: Block-level storage devices that can be attached to EC2 instances.
Snapshots: Point-in-time backups of EBS volumes stored in S3.
Use Cases
Database Storage

Scenario: A company runs a relational database on an EC2 instance and needs reliable storage.
Solution: Attach an EBS volume to the EC2 instance for database storage and use EBS snapshots for backups.
Application Data

Scenario: An application requires persistent storage for user data.
Solution: Attach EBS volumes to EC2 instances and use them to store application data.
Backup and Restore

Scenario: An organization needs to back up and restore EBS volumes.
Solution: Use EBS snapshots to create backups and restore data when needed.
Billing Details
Volume Costs: Based on the size and type of EBS volume (e.g., General Purpose SSD, Provisioned IOPS SSD).
Snapshot Costs: Charges for storing EBS snapshots in S3.
Commands
```bash
# Create an EBS volume
aws ec2 create-volume --size 10 --volume-type gp2 --availability-zone us-west-1a

# Attach an EBS volume to an EC2 instance
aws ec2 attach-volume --volume-id vol-12345678 --instance-id i-12345678 --device /dev/sdf

# Create an EBS snapshot
aws ec2 create-snapshot --volume-id vol-12345678 --description "Backup Snapshot"
```
```yaml
# Example EBS volume configuration in a CloudFormation template
Resources:
  MyEBSVolume:
    Type: AWS::EC2::Volume
    Properties:
      Size: 10
      VolumeType: gp2
      AvailabilityZone: us-west-1a
```
3. Amazon EFS (Elastic File System)
Overview
Amazon EFS provides scalable and elastic file storage for use with Amazon EC2 instances. It supports the NFS protocol, allowing multiple instances to access the same file system concurrently.

Architecture
File Systems: Managed file systems that can be mounted to EC2 instances.
Mount Targets: Network interfaces that allow EC2 instances to access EFS file systems.
Use Cases
Shared File Storage

Scenario: Multiple EC2 instances need to share access to the same files.
Solution: Use EFS to create a shared file system that can be mounted on multiple EC2 instances.
Content Management

Scenario: A content management system needs a scalable file system.
Solution: Store content in EFS, allowing multiple web servers to access and serve the content.
Data Processing

Scenario: Data processing applications require shared storage for input and output files.
Solution: Use EFS to store data that needs to be accessed by multiple processing nodes.
Billing Details
Storage Costs: Based on the amount of data stored and the throughput mode (e.g., Bursting, Provisioned).
Data Transfer Costs: Charges for data transferred out of EFS.
Commands

```bash 
# Create an EFS file system
aws efs create-file-system --creation-token my-token

# Create a mount target
aws efs create-mount-target --file-system-id fs-12345678 --subnet-id subnet-12345678

# List EFS file systems
aws efs describe-file-systems
```
```yaml
# Example EFS file system configuration in a CloudFormation template
Resources:
  MyEFSFileSystem:
    Type: AWS::EFS::FileSystem
    Properties:
      PerformanceMode: generalPurpose
      Encrypted: true
```
4. Amazon Glacier
Overview
Amazon Glacier is a low-cost archival storage service for long-term data backup and archival. It is designed for data that is infrequently accessed.

Architecture
Archives: Individual files or objects stored in Glacier.
Vaults: Containers for organizing and managing archives.
Use Cases
Long-Term Data Archival

Scenario: An organization needs to archive historical records and compliance data.
Solution: Use Glacier to store archival data at a low cost, with retrieval options when needed.
Backup Retention

Scenario: A company requires long-term backups of data stored in S3 or EBS.
Solution: Implement S3 Lifecycle policies to transition data to Glacier for long-term storage.
Regulatory Compliance

Scenario: An organization must retain data for compliance reasons.
Solution: Store the data in Glacier to meet regulatory requirements for long-term data retention.
Billing Details
Storage Costs: Based on the amount of data stored and the storage class (e.g., Standard, Deep Archive).
Data Retrieval Costs: Charges for accessing data from Glacier (e.g., expedited, standard, bulk retrieval).
Commands
```bash
# Create a Glacier vault
aws glacier create-vault --account-id - --vault-name my-vault

# Upload an archive to Glacier
aws glacier upload-archive --account-id - --vault-name my-vault --archive-description "My Archive" --body my-file.txt

# List Glacier vaults
aws glacier list-vaults --account-id -

```
```yaml configuration
# Example Glacier vault configuration in a CloudFormation template
Resources:
  MyGlacierVault:
    Type: AWS::Glacier::Vault
    Properties:
      VaultName: my-vault
```
Billing Summary
Cost Factors
Storage Costs: Based on the amount of data stored and the type of storage used (e.g., S3 Standard, EBS SSD).
Data Transfer Costs: Charges for data transfer out of AWS to the internet or other AWS regions.
Request Costs: Fees for API requests (e.g., S3 PUT, GET; EBS snapshots).
Retrieval Costs: Charges for retrieving data from Glacier or EFS.
Pricing Tiers
Standard Storage: Regular usage and data access.
Infrequent Access: Lower-cost storage for data accessed less frequently.
Archive Storage: Long-term archival with lower costs but higher retrieval fees.

For detailed and up-to-date pricing information, refer to the AWS Pricing Calculator and the respective service pricing pages:

Amazon S3 Pricing
Amazon EBS Pricing
Amazon EFS Pricing
Amazon Glacier Pricing