# Azure Virtual Network (VNet)

An Azure Virtual Network (VNet) is a representation of your network in the cloud. It provides logical isolation of the Azure cloud dedicated to your subscription. 

VNets enable Azure resources, such as Virtual Machines (VMs), to securely communicate with each other, the internet, and on-premises networks. 

A VNet is similar to a traditional network in your data centre but offers additional benefits of Azure infrastructure such as scalability, availability, and isolation.

VNets are created at the subscription level, within a specific resource group and region. The default limit for the number of VNets you can create in a single Azure subscription is 1,000.

When you create multiple resources (e.g., VMs) within a single VNet, they can communicate with each other using private IP addresses without needing internet access or VNet peering. If you create resources in different VNets, they can communicate using private IPs after establishing VNet peering.

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

## DDOS Protection
Azure DDoS protection, combined with application design best practices, provides defence against DDoS attacks. Azure DDoS protection offers basic and standard tier services with some feature differences.

## FireWall
Azure Firewall is a managed cloud-based network security service that protects your Azure virtual network resources. It allows you to create, enforce, and log application and network connectivity policies across subscriptions and virtual networks. 

If you need more flexibility than NSGs provide, or if you want a more powerful solution without using third-party services, Azure Firewall is a suitable option.

## Service endpoints
Service endpoints allow you to secure your critical Azure resources to your virtual networks. They provide access to PaaS services like Azure Storage, SQL Database, MySQL, Key Vault, and App Services, directly from within your VNet.