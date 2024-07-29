# Azure Virtual Network (VNet)

Azure Virtual Network (VNet) is a fundamental building block for creating and managing your Azure resources. It provides a secure and isolated network environment in the cloud, allowing you to connect and control your Azure resources as if they were on-premises.

## Key Features

- **Isolation**: VNets provide network isolation, allowing you to separate your resources and control traffic flow within your virtual network.

- **Subnets**: VNets can be divided into multiple subnets, enabling you to segment your resources and apply different network policies to each subnet.

- **Connectivity**: VNets can be connected to other VNets, on-premises networks, or even to the internet, providing flexible connectivity options for your resources.

- **Security**: VNets offer built-in security features such as network security groups (NSGs) and virtual network service endpoints, allowing you to control access to your resources and protect them from unauthorized access.

- **Traffic Routing**: VNets support user-defined routes and network virtual appliances (NVAs), enabling you to customize the routing of traffic within your virtual network.

## VNet Components

When creating a VNet, you need to define the following components:

- **Address Space**: The IP address range that will be used by the VNet and its subnets.

- **Subnets**: The subnets within the VNet, each with its own IP address range.

- **Network Security Groups (NSGs)**: Optional security groups that can be associated with subnets or network interfaces to control inbound and outbound traffic.

- **Virtual Network Peering**: Allows you to connect VNets together, enabling resources in different VNets to communicate with each other securely.

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

This command creates a VNet named "myVNet" with an address space of 10.0.0.0/16 and a subnet named "mySubnet" with an address space of 10.0.0.0/24.

## Conclusion

Azure Virtual Network is a powerful networking feature that allows you to create and manage isolated network environments in Azure. By understanding its key features and components, you can effectively design and deploy your resources within a VNet.