# Azure Virtual Network (VNet)

An Azure Virtual Network (VNet) is a representation of your network in the cloud. It provides logical isolation of the Azure cloud dedicated to your subscription. 

VNets enable Azure resources, such as Virtual Machines (VMs), to securely communicate with each other, the internet, and on-premises networks. 

A VNet is similar to a traditional network in your data centre but offers additional benefits of Azure infrastructure such as scalability, availability, and isolation.

VNets are created at the subscription level, within a specific resource group and region. The default limit for the number of VNets you can create in a single Azure subscription is 1,000.

When you create multiple resources (e.g., VMs) within a single VNet, they can communicate with each other using private IP addresses without needing internet access or VNet peering. If you create resources in different VNets, they can communicate using private IPs after establishing VNet peering.

Microsoft doesn't charge for VNet, they always charge for inbound/outbound traffic.

## Key Features

- **Isolation**: VNets provide network isolation, allowing you to separate resources and control traffic flow within your virtual network.

- **Subnets**: VNets can be divided into multiple subnets, enabling you to segment resources and apply different network policies to each subnet.

- **Connectivity**: VNets can connect to other VNets, on-premises networks, or the internet, providing flexible connectivity options.

- **Security**: VNets offer built-in security features such as Network Security Groups (NSGs) and virtual network service endpoints, allowing you to control access to resources and protect them from unauthorized access.

- **Traffic Routing**: VNets support user-defined routes and Network Virtual Appliances (NVAs), enabling you to customize traffic routing within your virtual network.

## VNet Components

When creating a VNet, you need to define the following components:

- **Address Space**: The IP address range used by the VNet and its subnets.

- **Subnets**: Subdivisions within the VNet, each with its own IP address range.

  - For example, if you allocate the address range `10.0.0.0/24` for a subnet, the following IP addresses are reserved:
    - `10.0.0.0`: Network address
    - `10.0.0.1`: Default gateway
    - `10.0.0.2 - 10.0.0.3`: DNS
    - `10.0.0.255`: Broadcast address

  - Therefore, using `/24` allows `256 - 5 = 251` usable IP addresses, and using `/16` allows `65,536 - 5 = 65,531` usable IP addresses.

- **Network Interface Card (NIC)**: A component that connects a VM to a VNet.

- **Azure Load Balancer**: Distributes network traffic across multiple VMs.

- **Application Gateway**: Provides application-level routing and load balancing.

- **Traffic Manager**: Distributes user traffic across multiple regions.

- **Network Security Groups (NSGs)**: Optional security groups that can be associated with subnets or NICs to control inbound and outbound traffic.

- **Virtual Network Peering**: Connects VNets, enabling resources in different VNets to communicate securely.

- **Virtual Network Gateways**: Enables connectivity between VNets, on-premises networks, and the internet.

## Creating a VNet

To create a VNet in Azure, you can use the Azure portal, Azure CLI, Azure PowerShell, or Azure Resource Manager templates. Here's an example of creating a VNet using Azure CLI:

```bash
az network vnet create \
    --name myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.0.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefixes 10.0.0.0/24
```

## DDOS (distributed denial of service) Protection
Azure DDoS protection, combined with application design best practices, provides defence against DDoS attacks. Azure DDoS protection offers basic and standard tier services with some feature differences.

### Use Case: E-Commerce Website

**Scenario:** Imagine you run an online shopping site. During a big sale, lots of people visit your site at the same time, causing a huge spike in traffic. This could crash your site, similar to a DDoS attack, where the goal is to overwhelm your servers.

**Solution:**  
Azure DDoS Protection steps in to help. It automatically handles the extra traffic, making sure real customers can shop without any issues while blocking any malicious traffic. This way, your site stays up and running, and customers can enjoy their shopping experience without disruptions.

## FireWall
Azure Firewall is a managed cloud-based network security service that protects your Azure virtual network resources. It allows you to create, enforce, and log application and network connectivity policies across subscriptions and virtual networks. 

If you need more flexibility than NSGs provide, or if you want a more powerful solution without using third-party services, Azure Firewall is a suitable option.

### Use Case: Financial Institution

**Scenario:** Consider a bank that has several applications on Azure. Each app needs to be very secure because they handle sensitive financial information.

**Solution:**  
Azure Firewall is used to keep everything safe. It acts like a security guard for your network, watching all the data coming in and going out. You can set rules about who can access what, ensuring only trusted users can see confidential information. This makes managing security easier and helps keep customer data safe, complying with all necessary regulations.

## Service endpoints
Service endpoints allow you to secure your critical Azure resources to your virtual networks. They provide access to PaaS services like Azure Storage, SQL Database, MySQL, Key Vault, and App Services, directly from within your VNet.

### Use Case: Healthcare Application

**Scenario:** Think of a healthcare provider that stores patient records on Azure. This data is very sensitive and needs to be protected from unauthorized access.

**Solution:**  
Service Endpoints are used to make sure that the data can only be accessed from within the provider’s own Azure network. It’s like having a private, secure road that only authorized users can travel on to reach the data. This keeps patient information safe and helps the healthcare provider meet privacy and security regulations.

# Lab - Creation of virtual network
**Step 1**: All Services-> Virtual Network->Add+
**Step 2**: Name (VNet1)-> Address Space (10.0.0.0/8)-> Subscription (free trial) -> Resource Group (Create New) -> Location (US-West)-> Subnet Name (VNet1-subnet1)-> Address Range (10.0.0.0/16)-> DDOS Protection  (Basic) -> Service end Point (disable) -> Firewall (disable) -> Create


