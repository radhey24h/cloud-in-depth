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
Before knowing cloud computing let us understand what is computer and what is computing?

- **Computer**: A computer is a device that processes data according to set of instruction. It can perform various tasks such as calculations, data storage, and communication.

- **Computing**: Computing refers to the use of computers, It includes everything from basic tasks like data entry and word processing to complex processes like software development, data analysis, and artificial intelligence.

## how many computing models is available?

### 1. Desktop Computing Model
When we talk about standalone PC, it is called desktop computing model, desktop computing model was the first cmputing model in IT industry.
This model is also famous today because we run this model to complete our day to day task.
- **Benefits**: Personalization, full control over resources.
- **Drawbacks**: Limited scalability, high maintenance costs and not able to run remotelly it becomes just a device to manage some personal work.
- **Use Case**: Small offices or personal computing.

### 2. Client-Server Computing Model
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
To avoid the drawback of client-server computing moldel Cluster computing model came in picture, So using the Cluster Computing model we can add more then one server in a cluster, so using this we can reduce the down time or any type of failure
- **Benefits**: High availability, increased computing power.
- **Drawbacks**: Complexity in management, cost of setup.
There was a major drawback of this system is its presence is not available in multiple location so in case if your cluster is available in specific area and any natural or un natural disaster will happen it will stop all the process.
- **Use Case**: Scientific computations, big data processing.

### 4. Grid Computing Model
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
- **Amazon AWS**: Leading in IaaS and PaaS, holding the largest share, about 33%.
- **Microsoft Azure**: Strong enterprise integration, coming in second with around 22%.
- **Google Cloud**: Emphasizes data analytics and AI, at approximately 10%.

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


## Top Security Concerns in Cloud Computing
1. **Data Breaches**: Unauthorized access to sensitive data.
2. **Hijacking of Accounts**: Unauthorized access to user accounts.
3. **Insider Threats**: Security risks from within the organization.
4. **Malware Injection**: Introduction of malicious software.
5. **Abuse of Cloud Services**: Misuse of cloud resources.
6. **Insecure APIs**: Vulnerabilities in application programming interfaces.


## Cloud Design Patterns
A cloud design pattern is a reusable solution to common problems encountered in cloud computing. Here are some key patterns:

- **Ambassador**: Offloads common client connectivity tasks (e.g., monitoring, logging, routing, security) in a language-agnostic manner.
- **Anti-Corruption Layer**: Provides a façade between new and legacy systems to prevent dependencies on outdated systems.
- **Backends for Frontends**: Creates separate backend services for different types of clients (e.g., desktop vs. mobile) to handle specific client needs efficiently.
- **Bulkhead**: Isolates critical resources (e.g., connection pool, memory, CPU) to prevent one service from consuming all resources and affecting others, enhancing resiliency.
- **Gateway Aggregation**: Aggregates requests to multiple microservices into a single request to reduce chattiness.
- **Gateway Offloading**: Allows microservices to offload shared functionalities (e.g., SSL certificates) to an API gateway.
- **Gateway Routing**: Routes requests to multiple microservices using a single endpoint, simplifying endpoint management.
- **Sidecar**: Deploys helper components as separate containers or processes for isolation and encapsulation.
- **Strangler**: Supports incremental migration by gradually replacing pieces of functionality with new services.



# Other Cloud Computing terminology

## Cloud Agnostic
- **Definition**: Flexibility to use any cloud service provider.
- **Use Case**: Multi-cloud environments, flexibility in provider choices.

## Cloud Native
- **Definition**: Applications built specifically for cloud environments.
- **Use Case**: Microservices architectures, rapid deployment.

## Virtualization
- **Definition**: Creates virtual versions of computing resources.
- **Use Case**: Server consolidation, efficient resource utilization.

## Virtual Machine (VM/EC2)
- **Definition**: Software emulation of a physical computer.
- **Use Case**: Running multiple operating systems on a single physical server.

## API (Application Programming Interface)
- **Definition**: Rules and protocols allowing software applications to interact.
- **Use Case**: Integrating third-party services, automation.

## Scalability vs. Elasticity

## Scalability
- **Definition**: Scalability refers to the ability of a system to handle an increasing workload by proportionally increasing its resource capacity.
- **Characteristics**:
  - **Proportional Growth**: Resources are added in proportion to the demand.
  - **Handling Increased Traffic**: Scales up to accommodate higher traffic or workload.

## Elasticity
- **Definition**: Elasticity refers to the capability of a system to dynamically commission and decommission resources as needed.
- **Characteristics**:
  - **Dynamic Adjustment**: Resources are adjusted in real-time based on current demand.
  - **Cost-Efficiency**: Ensures optimal resource usage by scaling resources up or down as required.

## Agility
Agility in cloud computing means being able to make changes quickly and easily. 
**Use-Case:** It's like being able to rearrange your furniture instantly to make room for guests. In the cloud, this means deploying new applications, scaling resources, or making updates rapidly, allowing businesses to respond to market demands and opportunities more effectively.

## High Availability
High availability in cloud computing means that a system or service is always up and running, even if something goes wrong. **Use-Case:** Imagine a store that never closes, even if one entrance is blocked; customers can still get in through another door. In the cloud, this means that your data and applications remain accessible, with backup systems ready to take over if there's an issue.

## Load Balancing
Load balancing distributes incoming network traffic across multiple servers or resources in a balanced manner. It ensures optimal resource utilization, improves responsiveness, and prevents any single server from being overwhelmed by distributing workloads effectively.


## What is Serverless?
- **Definition**: Serverless computing allows developers to build and deploy applications without managing underlying servers or infrastructure. The cloud provider handles resource allocation, scaling, and operational aspects.
- **Key Characteristics**:
  - **Focus on Code**: Developers focus on writing code and defining functionality.
  - **Managed Infrastructure**: The cloud provider manages resource allocation and scaling.

### Advantages of Serverless Computing
- **Cost-Effective**: Pay only for the execution time and resources used.
- **Simplified Operations**: Reduces the need for server management.
- **Increased Productivity**: Developers can concentrate on code and functionality.
- **Automatic Scaling**: Scales resources automatically based on demand.
- **No Server Management**: No need to manage the underlying servers.

### Disadvantages of Serverless Computing
- **Response Latency**: Potential for latency due to cold starts or resource allocation delays.
- **Resource Limitations**: Not ideal for high-computing operations due to resource constraints.
- **Security Responsibility**: Security responsibilities lie with the service provider, which might be a concern.
- **Debugging Challenges**: Debugging serverless code can be more complex.


## Fault Tolerance
Fault tolerance in cloud computing means that a system can keep working even if some parts fail. Think of it like a car with extra tires that automatically replace a flat tire while you’re driving, so you don’t have to stop. This ensures that services remain available and reliable, even when issues occur.

Fault tolerance is the ability of a system to continue operating in the event of hardware or software failures. It involves designing systems with redundancy and failover mechanisms to mitigate the impact of failures on overall system performance and availability.

## Disaster Recovery
Disaster recovery refers to the process and procedures for recovering and restoring data, applications, and infrastructure in the event of a natural or man-made disaster. It includes backup strategies, replication of data across geographically diverse locations, and comprehensive recovery plans.

## What is VPN?
- **Definition**: VPN stands for Virtual Private Network. It is a technology that secures data transmission over a public network by creating a private network.
- **Purpose**: VPN allows secure communication in cloud environments and can transform a public network into a private one.


## Introduction to Azure

### Definition

Azure is Microsoft's cloud platform, allowing you to use powerful computers over the internet. You can store data, run applications, and manage resources without needing your own physical servers.

### Benefits

- **Scalability**: Easily scale resources up or down based on demand.
- **Flexibility**: Supports various programming languages, frameworks, and operating systems.
- **Global Reach**: Azure has data centres in multiple regions around the world, providing low-latency access and compliance with local regulations.
- **Security**: Azure offers robust security features, including advanced threat protection, encryption, and compliance certifications, ensuring your data and applications are secure.
- **Cost Efficiency**: Azure provides a pay-as-you-go pricing model, allowing you to optimize costs by only paying for the resources you use. Additionally, Azure offers various cost management tools to monitor and control expenses.
- **Reliability**: With a strong service level agreement (SLA), Azure ensures high availability and uptime for your applications, minimizing downtime and business disruptions.
- **Innovation**: Azure continuously evolves, offering cutting-edge technologies such as artificial intelligence, machine learning, and Internet of Things (IoT) services to drive innovation and competitive advantage.
- **Hybrid Capability**: Azure supports hybrid cloud scenarios, allowing you to integrate on-premises data centres with the cloud, providing flexibility and control over your IT environment.
- **Developer Productivity**: Azure offers a comprehensive set of development tools, including Visual Studio, Azure DevOps, and GitHub integration, enabling developers to build, deploy, and manage applications efficiently.

### Drawbacks
- **Complexity**: Learning curve due to vast features and services.
- **Cost Management**: Monitoring costs and optimizing usage can be challenging.

### Use Case
Both start-ups and large companies use Azure to build and run their applications because it can easily grow with their needs.

---

## IaaS vs PaaS vs SaaS Models in Azure

### Infrastructure as a Service (IaaS)

#### Definition
IaaS provides virtualized computing resources over the internet. Users rent virtual machines (VMs), storage, and networking, managing operating systems and applications hosted on the infrastructure.

#### Examples
- **Virtual Machines (VMs)**: Renting VMs to run applications and manage operating systems, akin to renting a computer in the cloud.
- **Azure Blob Storage**: Storing unstructured data like documents, images, and videos, similar to using a digital storage unit.

### Platform as a Service (PaaS)
#### Definition
PaaS provides a platform for developers to build, deploy, and manage applications without managing underlying infrastructure. Developers focus on coding and deploying applications, while Azure manages the rest.

#### Examples
- **Azure App Service**: Hosting web applications and APIs with built-in scaling and load balancing capabilities.
- **Azure SQL Database**: Managed relational database service, handling backups, patching, and high availability.

### Software as a Service (SaaS)
#### Definition
SaaS delivers software applications over the internet on a subscription basis. Users access applications via a web browser without worrying about installation, maintenance, or infrastructure.

#### Examples
- **Microsoft 365**: Suite of productivity applications like Word, Excel, and Outlook accessible through a web browser.
- **Salesforce**: CRM software accessed online for managing customer relationships.

---

## Creating an Account with Azure

### Process
To get started with Azure:

1. Sign up for an Azure account via the [Azure portal](https://portal.azure.com) or Microsoft's website.
2. Follow the registration process and provide necessary details.
3. Access Azure services and resources upon account creation.

### Benefits: 
Access to a wide range of Azure services and resources to build and deploy applications.

### Drawbacks
Potential initial setup complexities may require guidance for first-time users.

### Use Case
Individuals or organizations looking to explore Azure services for development and deployment purposes.

---

## Azure Account, Subscription, and Resource Group Hierarchy Explained

### Azure Account
An Azure Account is the top-level entity that represents your access to Azure services. It is associated with a unique email address and acts as a container for all your Azure resources. When you sign up for Azure, you create an Azure Account.

### Subscription
Within an Azure Account, you can have one or more Subscriptions. A Subscription is a logical unit that provides access to Azure services and resources. It is associated with a specific billing and payment plan. Each Subscription has its own resource limits and usage quotas. You can think of a Subscription as a way to organize and manage your Azure resources based on different projects, departments, or environments.

### Resource Group
Inside a Subscription, you can create one or more Resource Groups. A Resource Group is a logical container that holds related Azure resources. It helps you organize and manage resources based on their lifecycle, ownership, or purpose. For example, you might have a Resource Group for a web application that contains virtual machines, storage accounts, and a database.

### Resource Groups provide several benefits:
- They enable you to manage and monitor resources collectively.
  They allow you to apply consistent policies and permissions to a group of resources.
  They provide a way to organize resources based on their lifecycle, such as deleting all resources in a Resource Group when they are no longer needed.
  It's important to note that resources within a Resource Group must be in the same Azure region.

- To summarize, the hierarchy is as follows: An Azure Account can have multiple Subscriptions, and each Subscription can have multiple Resource Groups. Resource Groups, in turn, contain the actual Azure resources like virtual machines, storage accounts, databases, etc.

### Azure Resources
Any manageable item in Azure, such as virtual machines, databases, or web apps.

## Manage subscription
### Subscription 
subscription allows us to use a service based on a fee. It allow us to use the service on an on-demand basis, and they ask for payment monthly basis and also they only ask what-ever service we have used.
After creating an account on azure portal we get 
1) Free trail and 
2) Azure Active directory

Without subscription we can't create any resource.

There are different types of subscriptions.
1) Free trail
2) visual studio yearly subscription: where we get visual studio free credits every month
3) Pay as you go :

## Subscription permission level
When we create an azure account, we get three level of permission in azure.
1) **Account Administrator**: When we create an azure account we get 1 Account Administrator Per account.
It manage all the subscription in an account
It create new subscription
it can cancel subscription
He can change the billing for a subscription
He can change the service administrator.

2) **Service administrator**: When we create an subscription, we can get 1 Service Administrator Per subscription.
Manage services in azure portal
Assign users to the co-Administrator role.

2) **Co-Administrator**: When we create an subscription service Administrator can create 200 co-Administrator role the access will be same like service administrator but he can't change the role of Service administrator.

## Management group
when we create multiple subscription we use management group to manage multiple subscription.
We can go Management group and we can add multiple subscription for multiple company.

Now let us say you have a product company and it is growing very well after a certain duration you acquire your competitor and he is also running an azure account so we can transfer that subscription one account.
**Benefits of Management group**
using Management group we can manage company(Management group) level cost and azure policy(like change wallpaper or change password).

---

## Components of Azure Architecture
### Data centres
A data center is like a big, secure building full of powerful computers and storage devices. It keeps all kinds of information safe and available so that people and businesses can access it whenever they need it. 

### Regions
Azure divides the world into regions, much like how continents divide the Earth. Each region contains multiple data centres. These regions help Azure users choose where they want their data and applications to be located for optimal performance and compliance with local laws.
**Example**: Similar to how different countries have their own rules and regulations, Azure regions ensure that data stays within legal boundaries and operates efficiently across the globe.

### Availability Zones
Within each region, there are availability zones, similar to neighbourhoods in a city. Each zone has its own infrastructure, providing redundancy and ensuring high availability of services.

Availability zones provide redundancy and ensure that if one zone goes down (due to maintenance or other issues), the services in other zones remain unaffected.

Availability Zones in Azure are physically separate locations within an Azure region with independent power, cooling, and networking.

#### Benefits
- **High Availability**: Redundancy across Availability Zones minimizes downtime.
- **Data Residency**: Compliance with data residency and sovereignty requirements.

### Resources
Azure offers various resources that users can use to build and run their applications. These include virtual machines (VMs), storage accounts, databases, and networking capabilities. Resources are the fundamental building blocks you use to create your digital services in Azure.

### Services
Azure provides a wide range of services that users can integrate into their applications. These services include computing power (to run programs), storage solutions (to store data), databases (to manage information), and networking tools (to connect different parts of an application). These services help developers build, deploy, and manage applications efficiently.

**Example**: Services in Azure are like tools in a toolbox. Just as a carpenter uses different tools to build a house, developers use Azure services to build and maintain their digital applications efficiently.

---

### Azure Resource Manager (ARM)
- **Definition**: Management layer for deploying and managing Azure resources.
- **Benefits**: Simplifies resource deployment, ensures consistent management.
- **Drawbacks**: Learning curve for complex deployments.
---

## There are multiple ways to connect with Azure:
1. **Azure portal**: The web-based interface provided by Azure for managing and interacting with your resources.
2. **Azure PowerShell**: A command-line tool that allows you to manage and automate Azure resources using PowerShell scripts.
3. **Azure CLI**: A cross-platform command-line tool that provides a command-line interface for managing Azure resources.
4. **Azure ARM template**: Azure Resource Manager templates allow you to define and deploy your infrastructure as code.
5. **Azure SDKs**: Software development kits (SDKs) are available for various programming languages, providing libraries and tools to interact with Azure services programmatically.

## Additional Resources
- [AWS Cloud Documentation](https://aws.amazon.com/documentation/)
- [Microsoft Azure Documentation](https://docs.microsoft.com/en-us/azure/)
- [Google Cloud Documentation](https://cloud.google.com/docs)
