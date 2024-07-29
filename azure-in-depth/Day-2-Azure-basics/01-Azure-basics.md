# Getting Started with Azure

Welcome to the Getting Started with azure.!
This document provides a comprehensive overview of Azure cloud computing platform, covering key concepts, services, and practical use cases.

## Table of Contents

1. [Introduction to Azure](#introduction-to-azure)
2. [IaaS vs PaaS vs SaaS Models in Azure](#iaas-vs-paas-vs-saas-models-in-azure)
3. [Creating an Account with Azure](#creating-an-account-with-azure)
4. [Azure Account, Subscription, and Resource Group Hierarchy Explained](#azure-account-subscription-and-resource-group-hierarchy-explained)
5. [Components of Azure Architecture](#components-of-azure-architecture)

---

## Introduction to Azure

### Definition

Azure is Microsoft's cloud platform, allowing you to use powerful computers over the internet. You can store data, run applications, and manage resources without needing your own physical servers.

### Benefits

- **Scalability**: Easily scale resources up or down based on demand.
- **Flexibility**: Supports various programming languages, frameworks, and operating systems.
- **Global Reach**: Azure has data centers in multiple regions around the world, providing low-latency access and compliance with local regulations.
- **Security**: Azure offers robust security features, including advanced threat protection, encryption, and compliance certifications, ensuring your data and applications are secure.
- **Cost Efficiency**: Azure provides a pay-as-you-go pricing model, allowing you to optimize costs by only paying for the resources you use. Additionally, Azure offers various cost management tools to monitor and control expenses.
- **Reliability**: With a strong service level agreement (SLA), Azure ensures high availability and uptime for your applications, minimizing downtime and business disruptions.
- **Innovation**: Azure continuously evolves, offering cutting-edge technologies such as artificial intelligence, machine learning, and Internet of Things (IoT) services to drive innovation and competitive advantage.
- **Hybrid Capability**: Azure supports hybrid cloud scenarios, allowing you to integrate on-premises data centers with the cloud, providing flexibility and control over your IT environment.
- **Developer Productivity**: Azure offers a comprehensive set of development tools, including Visual Studio, Azure DevOps, and GitHub integration, enabling developers to build, deploy, and manage applications efficiently.

### Drawbacks

- **Complexity**: Learning curve due to vast features and services.
- **Cost Management**: Monitoring costs and optimizing usage can be challenging.

### Use Case

Both startups and large companies use Azure to build and run their applications because it can easily grow with their needs.

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
subscription allows us to use a service based on a fee. It alllow us to use the service on an on-demand basis, and they ask for payment monthly basis and also they only ask what-ever service we have used.
After creating an account on azure portal we get 
1) Free trail and 
2) Azure Active directory

Without subscription we can't create any resource.

There are different types of subscriptions.
1) Free trail
2) visual studio yearly subscription: where we get visual studio free credis every month
3) Pay as you go :

## Subscription permission level
When we create an azure account, we get three level of permission in azure.
1) **Account Administratior**: When we create an azure account we get 1 Account Administratior Per account.
It manage all the subscription in an account
It create new subscription
it can cencel subscription
He can change the billing for a subscription
He can change the service administrator.

2) **Service administrator**: When we create an subscription, we can get 1 Service Administratior Per subscription.
Manage services in azure portal
Assign users to the co-administartor role.

2) **Co-administartor**: When we create an subscription service administartor can create 200 co-administartor rolethe access will be same like service administrator but he can't change the role of Service administrator.

## Management group
when we create multiple subscription we use management group to manage multiple subscrption.
We can go Management group and we can add multiple suscription for multiple company.

Now let us say you have a product company and it is growing very well after a certain duration you aquire your competetior and he is also running an azure account so we can transfer that subscription one account.
**Benifits of Management group**
using Management group we can manage company(Management group) level cost and azure policy(like change wallpaper or change password).

### Azure Resource Manager (ARM)
- **Definition**: Management layer for deploying and managing Azure resources.
- **Benefits**: Simplifies resource deployment, ensures consistent management.
- **Drawbacks**: Learning curve for complex deployments.

---

## Components of Azure Architecture

### Data Centers
These are massive warehouses where Azure stores data and runs applications for users. Think of them like giant storage facilities for digital information.

### Regions
Azure divides the world into regions, much like how continents divide the Earth. Each region contains multiple data centers. These regions help Azure users choose where they want their data and applications to be located for optimal performance and compliance with local laws.
**Example**: Similar to how different countries have their own rules and regulations, Azure regions ensure that data stays within legal boundaries and operates efficiently across the globe.

### Availability Zones
Within each region, there are availability zones, similar to neighborhoods in a city. Each zone has its own infrastructure, providing redundancy and ensuring high availability of services.

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

## There are multiple ways to connect with Azure:
1. **Azure portal**: The web-based interface provided by Azure for managing and interacting with your resources.
2. **Azure PowerShell**: A command-line tool that allows you to manage and automate Azure resources using PowerShell scripts.
3. **Azure CLI**: A cross-platform command-line tool that provides a command-line interface for managing Azure resources.
4. **Azure ARM template**: Azure Resource Manager templates allow you to define and deploy your infrastructure as code.
5. **Azure SDKs**: Software development kits (SDKs) are available for various programming languages, providing libraries and tools to interact with Azure services programmatically.

---

For more information and detailed documentation, visit [Azure Documentation](https://docs.microsoft.com/en-us/azure/).

---

## Additional Resources

- [Azure Documentation](https://docs.microsoft.com/en-us/azure/)
- [Azure Learning Paths](https://learn.microsoft.com/en-us/azure/)
- [Azure Tutorials and Samples](https://github.com/Azure-Samples)
