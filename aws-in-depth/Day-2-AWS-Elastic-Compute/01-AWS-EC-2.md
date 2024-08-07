# Amazon Elastic Compute Cloud (EC2)

Amazon EC2 is a service that provides scalable virtual servers in the AWS cloud, enabling flexible and cost-effective web-scale computing.

## Key Points
- **Scalability**: Easily scale computing resources up or down based on demand.
- **Virtual Servers**: Launch multiple instances with customizable configurations.
- **Security and Storage**: Configure security settings and choose between Elastic Block Store (EBS) for persistent storage and Instance Store for temporary storage.
- **Preconfigured Templates**: Use Amazon Machine Images (AMIs) to quickly deploy instances with predefined configurations.
- **Instance Limits**: Default limit of 20 instances per region, supporting high I/O operations.

## Types of EC2 instances
General purpose instance, Compute optimized, memory optimized, storage optimized, Accelerated computing or GPU, High memory instances, previous generation instances.
**General purpose instance-** it provides a balance of compute, memory and networking resources and can be used verity of workloads

**In general purpose 3 Series are available -** A series(A1), M series (M4, M5, M5A, M5AD, M5D), T series (T2(T2 micro Free tier), T3, T3A)

In general purpose instances available in four sizes- nano, small, medium, large.

A series Medium and large size, M Series have only large size and T series have all the four size.
**A1 Instances –** Ideally suited for scale out workloads that are supported by the ARM Ecosystem.
A1 Instances are well suited for following applications-
Web Server, Containerized Micro services, Caching Fleets, Distributed data stores, Application that requires ARM instruction set.
**M4 Instances –** used for high computational tasks
vCPU- 2 to 40 (max), RAM 8 to 160 GB(max), instance storage EBS(elastic block store) only for root volume.
**M5 Instances –** used for high computational tasks and it provides an ideal and balanced cloud environment.
vCPU- 2 to 96 (max), RAM 8 to 384 GB(max), instance storage EBS and NVMe SSD or nitro VM SSD.

EC2 Instance Purchasing options-

  1) On Demand 
  2) Dedicated instance
  3) Dedicated Host
  4) Spot instance
  5) Schedule Instance
  6) Reserved Instance

But mainly there are three way to pay for amazon EC2 instances i.e. On-Demand, Reserved instance and Spot Instances.
## EC2 Access-
To access instances, we need to a key and key pair name, we can download private key only once. The public key is saved by AWS to match it to the pair name and private key when you try to login to the EC2 instances. Without key pair we can’t access instance via RDP or SSH.

There is 20 EC2 instances (soft limit) per account in a region, we can submit a request to increase it. 

## EC2 Architecture

### 1. EC2 Instances
   - **Description:** Virtual servers that run applications and services. Instances can be launched with various configurations based on CPU, memory, storage, and networking requirements.
   - **Architecture:** 
     - **Instance Types:** Different types are optimized for various use cases, such as compute-optimized (C-series), memory-optimized (R-series), and storage-optimized (I-series) instances.
     - **Instance Sizes:** Each instance type comes in different sizes (e.g., `t2.micro`, `m5.large`) to accommodate various workloads.
   - **Use Case:** A startup needs scalable web servers to handle varying traffic loads. EC2 instances can be configured to scale up or down based on demand.
   - **Billing Details:** Charged based on the instance type, size, and usage hours. Pricing varies for On-Demand, Reserved, and Spot instances.
   - **Commands:**
     ```bash
     # Launch a new EC2 instance
     aws ec2 run-instances --image-id <AMI_ID> --count 1 --instance-type <INSTANCE_TYPE> --key-name <KEY_NAME> --security-group-ids <SECURITY_GROUP_ID> --subnet-id <SUBNET_ID>
     
     # Describe EC2 instances
     aws ec2 describe-instances
     
     # Terminate an EC2 instance
     aws ec2 terminate-instances --instance-ids <INSTANCE_ID>
     ```

### 2. AMI (Amazon Machine Image)
   - **Description:** Pre-configured templates that include the operating system, application server, and applications. AMIs provide a standardized way to launch instances with the desired configuration.
   - **Architecture:** 
     - **Base AMIs:** Include a default OS and may include additional software.
     - **Custom AMIs:** Created by users to include specific configurations or software.
   - **Use Case:** A company requires a consistent development environment across multiple instances. A custom AMI is created with all necessary tools and configurations pre-installed.
   - **Billing Details:** AMIs themselves are free, but charges apply for storage and instance usage based on the AMI.
   - **Commands:**
     ```bash
     # Create an AMI from an existing instance
     aws ec2 create-image --instance-id <INSTANCE_ID> --name "My Custom AMI" --no-reboot
     
     # List available AMIs
     aws ec2 describe-images --owners self
     ```

### 3. EBS (Elastic Block Store)
   - **Description:** Persistent block storage volumes that can be attached to EC2 instances. EBS volumes retain data even when instances are stopped or terminated.
   - **Architecture:** 
     - **Volume Types:** Includes General Purpose SSD (GP3), Provisioned IOPS SSD (io1), and Magnetic volumes.
     - **Snapshots:** Backups of EBS volumes that can be used to create new volumes.
   - **Use Case:** A web application requires a database with persistent storage. EBS volumes provide reliable storage that persists beyond instance termination.
   - **Billing Details:** Charged based on the volume size, type, and I/O operations. Snapshots are billed based on the amount of data stored.
   - **Commands:**
     ```bash
     # Create a new EBS volume
     aws ec2 create-volume --size 100 --volume-type gp3 --availability-zone <AZ>
     
     # Attach an EBS volume to an instance
     aws ec2 attach-volume --volume-id <VOLUME_ID> --instance-id <INSTANCE_ID> --device /dev/sdh
     
     # Create a snapshot of an EBS volume
     aws ec2 create-snapshot --volume-id <VOLUME_ID> --description "Snapshot of volume"
     ```

### 4. Security Groups
   - **Description:** Virtual firewalls that control inbound and outbound traffic to EC2 instances. Security groups allow or deny traffic based on specified rules.
   - **Architecture:** 
     - **Inbound Rules:** Define allowed incoming traffic.
     - **Outbound Rules:** Define allowed outgoing traffic.
   - **Use Case:** A web server needs to be accessible from the internet on port 80, but access to port 22 (SSH) should be restricted. Security groups are configured to allow HTTP traffic and restrict SSH access.
   - **Billing Details:** No additional cost for security groups; charges are based on the resources using them (e.g., EC2 instances).
   - **Commands:**
     ```bash
     # Create a new security group
     aws ec2 create-security-group --group-name <GROUP_NAME> --description "My security group" --vpc-id <VPC_ID>
     
     # Add a rule to a security group
     aws ec2 authorize-security-group-ingress --group-id <GROUP_ID> --protocol tcp --port 80 --cidr 0.0.0.0/0
     
     # Describe security groups
     aws ec2 describe-security-groups
     ```

### 5. Elastic IP (EIP)
   - **Description:** A static IPv4 address designed for dynamic cloud computing. Elastic IPs can be associated with EC2 instances to provide a persistent IP address.
   - **Architecture:** 
     - **Allocation:** EIP is allocated from a pool of public IP addresses.
     - **Association:** EIP can be associated with any running instance or network interface.
   - **Use Case:** A company requires a fixed IP address for their web application to ensure DNS records remain consistent, even if the underlying instance changes.
   - **Billing Details:** Charged for EIPs that are allocated but not associated with running instances. Additional charges apply if the EIP is associated with an instance.
   - **Commands:**
     ```bash
     # Allocate a new Elastic IP
     aws ec2 allocate-address --domain vpc
     
     # Associate an Elastic IP with an instance
     aws ec2 associate-address --instance-id <INSTANCE_ID> --allocation-id <ALLOCATION_ID>
     
     # Release an Elastic IP
     aws ec2 release-address --allocation-id <ALLOCATION_ID>
     ```

### 6. Auto Scaling
   - **Description:** Automatically adjusts the number of EC2 instances in a group based on demand. Ensures the right number of instances are available to handle the load.
   - **Architecture:** 
     - **Launch Configuration:** Defines instance configuration (AMI, instance type, etc.).
     - **Scaling Policies:** Define how and when to scale in or out.
   - **Use Case:** An e-commerce site experiences traffic spikes during sales events. Auto Scaling adjusts the number of instances to handle increased load and scales down when traffic decreases.
   - **Billing Details:** Charges are based on the number of instances running and the instance types used.
   - **Commands:**
     ```bash
     # Create an Auto Scaling group
     aws autoscaling create-auto-scaling-group --auto-scaling-group-name <ASG_NAME> --launch-configuration-name <LC_NAME> --min-size 1 --max-size 10 --desired-capacity 2 --vpc-zone-identifier <SUBNET_ID>
     
     # Create a scaling policy
     aws autoscaling put-scaling-policy --policy-name <POLICY_NAME> --auto-scaling-group-name <ASG_NAME> --scaling-adjustment 1 --adjustment-type ChangeInCapacity
     
     # Describe Auto Scaling groups
     aws autoscaling describe-auto-scaling-groups
     ```

### 7. Key Pairs
   - **Description:** Secure SSH key pairs used to access EC2 instances. The private key remains with the user, while the public key is stored on the instance.
   - **Architecture:** 
     - **Public Key:** Added to instances at launch time.
     - **Private Key:** Used by users to securely connect to instances.
   - **Use Case:** An administrator needs to securely access a Linux EC2 instance. A key pair is created and the public key is added to the instance.
   - **Billing Details:** Key pairs are free of charge. Costs are associated with the EC2 instances using them.
   - **Commands:**
     ```bash
     # Create a new key pair
     aws ec2 create-key-pair --key-name <KEY_NAME> --query 'KeyMaterial' --output text > <KEY_NAME>.pem
     
     # Describe key pairs
     aws ec2 describe-key-pairs
     ```

### 8. Elastic Load Balancer (ELB)
   - **Description:** Automatically distributes incoming application traffic across multiple EC2 instances to ensure high availability and fault tolerance.
   - **Architecture:** 
     - **Classic Load Balancer:** Operates at the transport layer.
     - **Application Load Balancer:** Operates at the application layer (Layer 7).
     - **Network Load Balancer:** Operates at the network layer (Layer 4).
   - **Use Case:** A web application with multiple EC2 instances behind an ELB to balance traffic and ensure high availability.
   - **Billing Details:** Charged based on the number of hours the load balancer is running and the amount of data processed.
   - **Commands:**
     ```bash
     # Create a new load balancer
     aws elb create-load-balancer --load-balancer-name <LB_NAME> --listeners Protocol=HTTP,LoadBalancerPort=80,InstanceProtocol=HTTP,InstancePort=80 --availability-zones <AZ1> <AZ2>
     
     # Describe load balancers
     aws elb describe-load-balancers
     
     # Delete a load balancer
     aws elb delete-load-balancer --load-balancer-name <LB_NAME>
     ```

## Pricing and Billing Details

### 1. EC2 Instances
   - **On-Demand Instances:** Pay for compute capacity by the hour or second.
   - **Reserved Instances:** Commit to a specific instance type in a specific region for 1 or 3 years to receive a discount.
   - **Spot Instances:** Bid for unused EC2 capacity at a lower price.

### 2. AMI Storage
   - **Standard Storage:** Charged based on the size of the AMI and storage duration.
   - **Snapshot Storage:** Charged based on the amount of data stored in snapshots.

### 3. EBS Volumes
   - **Volume Type:** Charges based on the type and size of the volume.
   - **Snapshot Storage:** Charged based on the size and duration of snapshots.

### 4. Security Groups
   - **No Additional Cost:** Included in the cost of the associated EC2 instances.

### 5. Elastic IPs
   - **Idle EIP Charges:** Charged for Elastic IP addresses that are not associated with a running instance.
   - **Association Charges:** Charged for each EIP associated with a running instance.

### 6. Auto Scaling
   - **No Additional Cost:** Charges based on the EC2 instances in the Auto Scaling group.

### 7. Key Pairs
   - **No Additional Cost:** Key pairs are free; charges are based on the EC2 instances.

### 8. Elastic Load Balancer (ELB)
   - **Load Balancer Hours:** Charged based on the hours the load balancer is running.
   - **Data Processed:** Charges based on the amount of data processed by the load balancer.

For detailed and up-to-date pricing information, refer to the [AWS Pricing Calculator](https://calculator.aws/#/) and the [AWS EC2 pricing page](https://aws.amazon.com/ec2/pricing/).

This README provides a comprehensive overview of AWS EC2, including its components, architecture, use cases, billing details, and relevant commands. It serves as a complete guide for understanding and managing EC2 instances in AWS environments.
