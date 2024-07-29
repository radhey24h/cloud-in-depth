# Cloud Computing Documentation

## Table of Contents
1. [What is Cloud Computing?](#what-is-cloud-computing)
2. [What is Computer and Computing?](#what-is-computer-and-computing)
3. [Computing Models](#how-many-computing-models-is-available)
   - [Desktop Computing Model](#1-desktop-computing-model)
   - [Client-Server Computing Model](#2-client-server-computing-model)
   - [Cluster Computing Model](#3-cluster-computing-model)
   - [Grid Computing Model](#4-grid-computing-model)
   - [Cloud Computing Model](#5-cloud-computing-model)
4. [Cloud Market Share](#cloud-market-share)
5. [Cloud Agnostic](#cloud-agnostic)
6. [Cloud Native](#cloud-native)
7. [Cloud Service Models](#cloud-service-models)
8. [Cloud Deployment Models](#cloud-deployment-models)
9. [Virtualization](#virtualization)
10. [Virtual Machine (VM/EC2)](#virtual-machine-vmec2)
11. [API (Application Programming Interface)](#api-application-programming-interface)
12. [Other Cloud Computing Terminology](#other-cloud-computing-terminology)
    - [Scalability](#scalability)
    - [Elasticity](#elasticity)
    - [Agility](#agility)
    - [High Availability](#high-availability)
    - [Fault Tolerance](#fault-tolerance)
    - [Disaster Recovery](#disaster-recovery)
    - [Load Balancing](#load-balancing)

## What is Cloud Computing?
Before knowing cloud computing let us understand what is computer and computing?

## What is Computer and Computing?
- **Computer**: A computer is a device that processes data according to instructions stored internally or externally. It can perform various tasks such as calculations, data storage, and communication.

- **Computing**: Computing refers to the use of computers and computer technology to process information, perform calculations, and manage data.

## how many computing models is available?

### 1. Desktop Computing Model
- **Definition**: Traditional model with dedicated desktop computers. 
When we talk about standalone PC, it is called desktop computing model, desktop computing model was the first cmputing model in IT industry.
This model is also famous today because we run this model to complete our day to day task.
- **Benefits**: Personalization, full control over resources.
- **Drawbacks**: Limited scalability, high maintenance costs and not able to run remotelly it becomes just a device to manage some personal work.
- **Use Case**: Small offices or personal computing.

### 2. Client-Server Computing Model
- **Definition**: Clients request services from centralized servers. 
To avoid the desktop model drawback client server computing model came in picture, So in Client server model multiple client machine was connected to a server and all client can work on a centrlised source.
- **Benefits**: Centralized management, easier updates.
- **Drawbacks**: Single point of failure, scalability limitations. 
  
  **What all reason is possible for server failure**
    1. Hardware Failure: Components such as hard drives, power supplies, or memory modules can fail due to wear and tear, overheating, or manufacturing defects.
    2. Software Issues: Bugs in operating systems, firmware, or applications can lead to crashes or instability, causing the server to fail.
    3. Network Problems: Issues with routers, switches, or cables can disrupt communication between servers.
    4. Human Error: Misconfigurations, improper maintenance procedures
    5. Power Outages: Interruptions in electrical power supply, whether due to grid failures can cause servers to shut down unexpectedly.
    6. Natural Disasters: Events such as earthquakes, floods, or fires can physically damage server infrastructure, leading to complete or partial failures.

- **Use Case**: Web applications, email servers.

### 3. Cluster Computing Model
- **Definition**: Multiple computers work together as a single system. 
To avoid the drawback of client-server computing moldel Cluster computing model came in picture, So using the Cluster Computing model we can add more then one server in a cluster, so using this we can reduce the down time or any type of failure
- **Benefits**: High availability, increased computing power.
- **Drawbacks**: Complexity in management, cost of setup.
There was a major drawback of this system is its presence is not available in multiple location so in case if your cluster is available in specific area and any natural or un natural disaster will happen it will stop all the process.
- **Use Case**: Scientific computations, big data processing.

### 4. Grid Computing Model
- **Definition**: Coordinates resources across multiple domains.
To avoid the drawback of cluster computing model grid computing model came in piture.
- **Benefits**: Resource sharing, cost efficiency.
- **Drawbacks**: Complex scheduling, security concerns.
The major drawback of this system was its cost.
### what all type of costs came in piture to manage server?
- **Copex** Capital expenditure refers to the funds a company spends on acquiring, upgrading, or maintaining physical assets such as buildings, equipment, or infrastructure. These expenditures are typically one-time investments that are expected to generate benefits over a long period. Examples include purchasing servers,  or investing in machinery.
- **Opex** Operational expenditure, on the other hand, refers to the ongoing costs that a business incurs to maintain its daily operations. These expenses are necessary for running the business and usually recur regularly. Examples include salaries, rent, utilities, maintenance contracts, and consumables.
- **Use Case**: Research collaborations, large-scale computations.

### 5. Cloud Computing Model
Now to avoid these major problem of grid computing model, a new concept came from **NIST** 
The National Institute of Standards and Technology (NIST) provides a framework for understanding and adopting cloud computing, hardwares and softwares. 

So NIST provides a provision if anyone want to rent-out the free space of their server and earn some money they can.
From here the cloud computing concept came in picture.

## What is Cloud Computing?
In simpler terms, imagine cloud is an virtual space where you can store files, run software, and access various services over the internet.

Cloud computing is like using a remote computer over the internet to store and manage your data or run applications. Instead of storing files or running software on your local computer, you can access them through the internet from a provider's server (the "cloud"). It allows you to use resources like storage space or software without needing to own or manage the physical infrastructure yourself.

Cloud computing involves the delivery of computing services (servers, storage, databases, networking, software, etc.) over the internet. It offers scalability, cost-efficiency, and flexibility compared to traditional computing models.

### Benefits
- **Scalability**: Easily scale resources up or down based on demand.
- **Cost Efficiency**: Pay only for what you use, reducing upfront costs.
- **Flexibility**: Access resources from anywhere with an internet connection.
- **Reliability**: Providers offer robust backup and disaster recovery options.
- **Maintenance**: Providers handle infrastructure maintenance and updates.

### Drawbacks
- **Dependency on Internet**: Reliability on internet connectivity is crucial.
- **Security and Privacy**: Concerns over data security and privacy.
- **Vendor Lock-in**: Switching providers can be complex.
- **Performance**: Can vary based on internet connection and provider.

### Use Cases
- **Startups and Small Businesses**: Scale operations without large upfront costs.
- **Large Enterprises**: Handle fluctuating workloads and global operations efficiently.
- **Development and Testing**: On-demand resources for testing and development.

## Cloud Market Share
- **Amazon AWS**: Leading in IaaS and PaaS.
- **Microsoft Azure**: Strong enterprise integration.
- **Google Cloud**: Emphasizes data analytics and AI.

## Cloud Agnostic
- **Definition**: Flexibility to use any cloud service provider.
- **Use Case**: Multi-cloud environments, flexibility in provider choices.

## Cloud Native
- **Definition**: Applications built specifically for cloud environments.
- **Use Case**: Microservices architectures, rapid deployment.

## Cloud Service Models
- **IaaS (Infrastructure as a Service)**: Virtualized computing resources over the internet.
  - **Use Case**: Hosting virtual machines, scalable storage solutions.

- **PaaS (Platform as a Service)**: Platform for developing, running, and managing applications.
  - **Use Case**: Application development, database management.

- **SaaS (Software as a Service)**: Software delivered over the internet on a subscription basis.
  - **Use Case**: Email services, CRM systems.

## Cloud Deployment Models
- **Public Cloud**: Services over the public internet, shared across organizations.
  - **Use Case**: General-purpose applications, websites.

- **Private Cloud**: Dedicated infrastructure operated for a single organization.
  - **Use Case**: Highly regulated industries, sensitive data.

- **Hybrid Cloud**: Combination of public and private cloud environments.
  - **Use Case**: Scalable applications with data residency requirements.

## Virtualization
- **Definition**: Creates virtual versions of computing resources.
- **Use Case**: Server consolidation, efficient resource utilization.

## Virtual Machine (VM/EC2)
- **Definition**: Software emulation of a physical computer.
- **Use Case**: Running multiple operating systems on a single physical server.

## API (Application Programming Interface)
- **Definition**: Rules and protocols allowing software applications to interact.
- **Use Case**: Integrating third-party services, automation.

# Other Cloud Computing terminology

## Scalability
Scalability in cloud computing means the ability to easily increase or decrease resources like storage, computing power, or bandwidth as needed. 
**Use-Case:** Imagine if your favorite website suddenly had a lot more visitors—scalability ensures it can handle that extra traffic smoothly by adding more resources quickly, without any downtime or slow performance. It's like being able to expand a restaurant's seating instantly when more customers arrive.

## Elasticity
Elasticity is the capability of a system to automatically provision and release resources as needed, based on demand. It goes hand in hand with scalability but focuses on the automatic nature of resource allocation, ensuring optimal performance and cost efficiency.

## Agility
Agility in cloud computing means being able to make changes quickly and easily. 
**Use-Case:** It's like being able to rearrange your furniture instantly to make room for guests. In the cloud, this means deploying new applications, scaling resources, or making updates rapidly, allowing businesses to respond to market demands and opportunities more effectively.

## High Availability
High availability in cloud computing means that a system or service is always up and running, even if something goes wrong. **Use-Case:** Imagine a store that never closes, even if one entrance is blocked; customers can still get in through another door. In the cloud, this means that your data and applications remain accessible, with backup systems ready to take over if there's an issue.

## Fault Tolerance
Fault tolerance in cloud computing means that a system can keep working even if some parts fail. Think of it like a car with extra tires that automatically replace a flat tire while you’re driving, so you don’t have to stop. This ensures that services remain available and reliable, even when issues occur.

Fault tolerance is the ability of a system to continue operating in the event of hardware or software failures. It involves designing systems with redundancy and failover mechanisms to mitigate the impact of failures on overall system performance and availability.

## Disaster Recovery

Disaster recovery refers to the process and procedures for recovering and restoring data, applications, and infrastructure in the event of a natural or man-made disaster. It includes backup strategies, replication of data across geographically diverse locations, and comprehensive recovery plans.

## Load Balancing

Load balancing distributes incoming network traffic across multiple servers or resources in a balanced manner. It ensures optimal resource utilization, improves responsiveness, and prevents any single server from being overwhelmed by distributing workloads effectively.


## Additional Resources
- [AWS Cloud Documentation](https://aws.amazon.com/documentation/)
- [Microsoft Azure Documentation](https://docs.microsoft.com/en-us/azure/)
- [Google Cloud Documentation](https://cloud.google.com/docs)
