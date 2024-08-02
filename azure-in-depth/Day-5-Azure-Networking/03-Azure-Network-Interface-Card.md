# Network Interface Card (NIC)

A Network Interface Card (NIC) is a crucial component in Azure that connects a virtual machine (VM) or other Azure resources to a virtual network (VNet). It facilitates communication between the resource and the network, allowing it to send and receive data.

## Use Cases of Network Interface Card (NIC)

1. **Virtual Machine Connectivity**
   - **Scenario:** A company deploys virtual machines (VMs) in Azure to run applications and needs them to connect to the virtual network for internal communication.
   - **Solution:** Each VM is assigned a Network Interface Card (NIC) that connects it to the VNet, allowing the VM to communicate with other resources in the network and access external services.

2. **High Availability and Load Balancing**
   - **Scenario:** An application running on multiple VMs needs to ensure high availability and load balancing across instances.
   - **Solution:** NICs are used in conjunction with Azure Load Balancer or Application Gateway to distribute traffic across VMs, ensuring that the application remains available and performs well even under heavy load.

3. **Network Segmentation**
   - **Scenario:** An organization needs to isolate different parts of its application for security and compliance reasons.
   - **Solution:** NICs can be attached to VMs in different subnets within a VNet. Network Security Groups (NSGs) and routing rules can then be applied to control and segment traffic between different subnets.

4. **Connecting to On-Premises Networks**
   - **Scenario:** A business wants to securely connect its Azure VMs to an on-premises network for hybrid cloud scenarios.
   - **Solution:** NICs are used with VPN Gateway or ExpressRoute to establish secure connections between Azure VNets and on-premises networks, facilitating seamless data exchange.

5. **Public and Private IP Addressing**
   - **Scenario:** A web application needs to be accessible from the internet while also communicating privately with other internal resources.
   - **Solution:** NICs can be configured with both public and private IP addresses, allowing the application to be accessible from the internet and also communicate internally within the VNet.

## Why Use Network Interface Cards (NICs)?

- **Connectivity:** NICs provide the essential link between Azure resources and virtual networks, enabling communication with other resources and external networks.
- **Flexibility:** NICs can be associated with different subnets, assigned static or dynamic IP addresses, and configured with network security features.
- **Scalability:** Multiple NICs can be attached to a single VM or other Azure resources, supporting advanced networking scenarios and high-performance applications.
- **Isolation:** NICs help segment network traffic and apply security policies, ensuring that different parts of an application or infrastructure remain isolated as needed.

## Key Concepts

### Components of a NIC

- **IP Addresses:** Each NIC can have one or more IP addresses assigned, including private (internal) and public (external) IP addresses.
- **Network Security Groups (NSGs):** NSGs can be associated with NICs to control inbound and outbound traffic based on defined security rules.
- **Subnet:** NICs are associated with specific subnets within a VNet, which defines the IP address range and network policies for the resource.
- **DNS Settings:** NICs support custom DNS settings to resolve domain names within the VNet.

### Types of NICs

1. **Standard NICs**
   - **Description:** Basic NICs used for most scenarios with standard features and performance.
   - **Use Case:** Suitable for general-purpose VMs and typical network configurations.

2. **Accelerated NICs**
   - **Description:** NICs with enhanced performance and lower latency, often used for high-performance computing scenarios.
   - **Use Case:** Ideal for applications requiring high network throughput and low latency.

## Setting Up a Network Interface Card (NIC)

### Steps to Configure

1. **Create a Virtual Network:**

   - **Navigate to the Azure Portal:**
     - Go to "Create a resource" > "Networking" > "Virtual Network".
     - Define the address space, subnets, and other network settings.

2. **Create a Network Interface Card:**

   - **Navigate to the Azure Portal:**
     - Go to "Create a resource" > "Networking" > "Network Interface".
     - Click "Create" to start the NIC creation process.

   - **Configure NIC Settings:**
     - Provide a name for the NIC, select the virtual network and subnet, and configure IP address settings (static or dynamic).
     - Optionally, configure Network Security Groups (NSGs) and DNS settings.

   - **Review and Create:**
     - Review the NIC configuration and click "Create" to provision the NIC.

3. **Attach NIC to a Virtual Machine:**

   - **Navigate to the Azure Portal:**
     - Go to the VM settings and select "Networking".
     - Attach the NIC to the VM by selecting the existing NIC or creating a new one.

4. **Verify Configuration:**

   - **Check Connectivity:**
     - Ensure that the NIC is correctly associated with the VM and that network connectivity is functioning as expected.
   - **Test Network Traffic:**
     - Verify that traffic flows between the VM and other resources according to the network configuration.

## Billing Details

### Cost Factors

- **Number of NICs:** The cost is based on the number of Network Interface Cards created and used.
- **IP Addresses:** Charges apply for public IP addresses associated with NICs.
- **Data Transfer:** Costs may be incurred for data transfer between NICs and other Azure resources or external networks.

### Pricing Tiers

- **Standard NIC Pricing:** Generally, the cost is based on the number of NICs and IP addresses used.
- **Accelerated NIC Pricing:** Higher cost for NICs with enhanced performance features.

For the most current pricing details, refer to the [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/) and the [Azure NIC pricing page](https://azure.microsoft.com/en-us/pricing/details/network-interface/).

This README provides a detailed overview of Network Interface Cards (NICs) in Azure, including their use cases, components, setup steps, and billing information. It serves as a comprehensive guide for understanding and configuring NICs in Azure environments.
