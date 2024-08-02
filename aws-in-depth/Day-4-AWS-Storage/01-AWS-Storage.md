# AWS Storage and Content Delivery

AWS offers a range of storage and content delivery services designed to store, manage, and process data efficiently. These services cater to diverse storage needs, from high-performance block storage to long-term data archiving.

## Storage Services

### Amazon S3 (Simple Storage Service)

Amazon S3 is a scalable object storage service designed for storing and retrieving any amount of data from anywhere on the web.

- **Object-Based Storage**: Store any type of data, such as images, documents, and backups.
- **Scalable Capacity**: Store objects ranging from 0 Bytes to 5 TB with unlimited total storage capacity.
- **Global Namespace**: Buckets have unique names across the AWS platform, which serve as the address for accessing stored objects.
- **Security and Durability**: Offers robust security features and stores data redundantly across multiple devices and facilities.

#### Use Cases
1. **Backup and Restore**: Store backup data in S3 with lifecycle policies to transition older backups to cheaper storage classes like S3 Glacier.
2. **Data Archiving**: Use S3 Glacier for long-term archival with lower costs compared to S3 Standard.
3. **Static Website Hosting**: Configure an S3 bucket for static website hosting and use Route 53 for domain management.

#### Billing Details
- **Storage Costs**: Based on the amount of data stored and the storage class (e.g., Standard, Intelligent-Tiering, Glacier).
- **Data Transfer Costs**: Charges for data transferred out of S3 to the internet or other AWS regions.
- **Request Costs**: Charges for requests to S3 (e.g., PUT, GET).

#### Commands
```bash
# Create an S3 bucket
aws s3api create-bucket --bucket my-bucket --region us-west-1

# Upload a file to an S3 bucket
aws s3 cp my-file.txt s3://my-bucket/

# List objects in an S3 bucket
aws s3 ls s3://my-bucket/
```
## YAML Configuration
## Example S3 bucket policy allowing public read access
```yaml
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
# Amazon EBS (Elastic Block Store)
Amazon EBS provides persistent block-level storage for use with Amazon EC2 instances.

**Block Storage:-** Functions like a traditional hard drive, supporting file systems, databases, and applications that require raw, unformatted block storage.
**Volume Types:-** Offers three volume types to suit different workloads:
- General Purpose (SSD)
- Provisioned IOPS (SSD)
- Magnetic
**Reliability and Security:-** Ensures data protection through automatic replication within its Availability Zone.
**Consistent Performance:-** SSD-backed storage delivers consistent I/O performance for applications.
**Data Backup:-** Supports point-in-time snapshots for easy data backup and restoration.
**Use Cases**
**Database Storage:** Attach an EBS volume to an EC2 instance for reliable database storage.
**Application Data:** Use EBS volumes for persistent storage of application data.
**Backup and Restore:** Utilize EBS snapshots to create backups and restore data when needed.
## Billing Details
**Volume Costs:** Based on the size and type of EBS volume (e.g., General Purpose SSD, Provisioned IOPS SSD).
**Snapshot Costs:** Charges for storing EBS snapshots in S3.
Commands
```bash
# Create an EBS volume
aws ec2 create-volume --size 10 --volume-type gp2 --availability-zone us-west-1a

# Attach an EBS volume to an EC2 instance
aws ec2 attach-volume --volume-id vol-12345678 --instance-id i-12345678 --device /dev/sdf

# Create an EBS snapshot
aws ec2 create-snapshot --volume-id vol-12345678 --description "Backup Snapshot"
```
YAML Configuration
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
# Amazon EFS (Elastic File System)
Amazon EFS provides scalable and elastic file storage for use with Amazon EC2 instances, supporting the NFS protocol for concurrent access.

**File Systems:** Managed file systems that can be mounted to EC2 instances.
**Mount Targets:** Network interfaces allowing EC2 instances to access EFS file systems.
Use Cases
**Shared File Storage:** Use EFS to create a shared file system accessible by multiple EC2 instances.
Content Management: Store content in EFS for scalable access by multiple web servers.
**Data Processing:** Use EFS for data that needs to be accessed by multiple processing nodes.
## Billing Details
**Storage Costs:** Based on the amount of data stored and the throughput mode (e.g., Bursting, Provisioned).
**Data Transfer Costs:** Charges for data transferred out of EFS.
Commands
```bash
# Create an EFS file system
aws efs create-file-system --creation-token my-token

# Create a mount target
aws efs create-mount-target --file-system-id fs-12345678 --subnet-id subnet-12345678

# List EFS file systems
aws efs describe-file-systems
```
## YAML Configuration
```yaml
# Example EFS file system configuration in a CloudFormation template
Resources:
  MyEFSFileSystem:
    Type: AWS::EFS::FileSystem
    Properties:
      PerformanceMode: generalPurpose
      Encrypted: true
```
# Amazon Glacier
Amazon Glacier is a low-cost archival storage service for long-term data backup and archival, designed for infrequently accessed data.

**Archives:-**Individual files or objects stored in Glacier.
**Vaults:** Containers for organizing and managing archives.
**Use Cases**
**Long-Term Data Archival:** Use Glacier to store archival data at a low cost, with retrieval options when needed.
**Backup Retention:** Implement S3 Lifecycle policies to transition data to Glacier for long-term storage.
Regulatory Compliance: Store data in Glacier to meet regulatory requirements for long-term data retention.
## Billing Details
**Storage Costs:** Based on the amount of data stored and the storage class (e.g., Standard, Deep Archive).
**Data Retrieval Costs:** Charges for accessing data from Glacier (e.g., expedited, standard, bulk retrieval).
Commands
```bash
# Create a Glacier vault
aws glacier create-vault --account-id - --vault-name my-vault

# Upload an archive to Glacier
aws glacier upload-archive --account-id - --vault-name my-vault --archive-description "My Archive" --body my-file.txt

# List Glacier vaults
aws glacier list-vaults --account-id -
```
YAML Configuration
```yaml
# Example Glacier vault configuration in a CloudFormation template
Resources:
  MyGlacierVault:
    Type: AWS::Glacier::Vault
    Properties:
      VaultName: my-vault
```

# Billing Summary
## Cost Factors
Storage Costs: Based on the amount of data stored and the type of storage used (e.g., S3 Standard, EBS SSD).
Data Transfer Costs: Charges for data transfer out of AWS to the internet or other AWS regions.
Request Costs: Fees for API requests (e.g., S3 PUT, GET; EBS snapshots).
Retrieval Costs: Charges for retrieving data from Glacier or EFS.
## Pricing Tiers
Standard Storage: Regular usage and data access.
Infrequent Access: Lower-cost storage for data accessed less frequently.
Archive Storage: Long-term archival with lower costs but higher retrieval fees.