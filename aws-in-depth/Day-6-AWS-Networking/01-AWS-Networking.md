# Networking in AWS

## Internet Protocol Addressing
### Types of Addressing
1. **Physical Addressing**: MAC Address (48 bits)
- **Definition**: Refers to the unique hardware address assigned to a network interface card (NIC) or other hardware devices on a network.
- **Example**: MAC Address (Media Access Control Address) is a 48-bit address used to uniquely identify network devices at the hardware level.

2. **Logical Addressing**: 
- **Definition**: Refers to an address used to identify devices on a network at a more abstract level, typically managed by network protocols.
- **Example**: IP Address (Internet Protocol Address), such as IPv4 or IPv6, is used to identify devices on a network and route data between them. IPv4 addresses are 32-bit, while IPv6 addresses are 128-bit.
   - **IP Version 4 (IPV4)**: 32-bit address with 4 octets, each octet ranging from 0 to 255.
   - **IP Version 6 (IPV6)**: 128-bit address designed to replace IPv4.

### IP Version 4 (IPV4)
- **Address Format**: IPv4 addresses are composed of 4 octets, each containing 8 bits. Example: `192.168.39.240`.
- **Classes**:
  - **Class A**: `1.0.0.0` to `126.0.0.0` (127 is reserved for loopback address)
  - **Class B**: `128.0.0.0` to `191.255.0.0`
  - **Class C**: `192.0.0.0` to `223.255.255.0`
  - **Class D**: `224.0.0.0` to `239.255.255.255` (Multicast)
  - **Class E**: `240.0.0.0` to `255.255.255.255` (Reserved for research)

**Identifying IP Class**:
- For `137.20.20.10`, the first octet `137` indicates Class B.
- For `201.100.10.0`, the first octet `201` indicates Class C.

**Network ID Calculation**:
- **Class A**: Network ID is the first octet, remaining are for hosts.
  - Example: `115.10.0.15` -> Network ID: `115.0.0.0`
- **Class B**: Network ID is the first two octets, remaining are for hosts.
  - Example: `150.10.10.100` -> Network ID: `150.10.0.0`
- **Class C**: Network ID is the first three octets, remaining is for hosts.
  - Example: `196.10.10.10` -> Network ID: `196.10.10.0`

**Subnet Mask Calculation**:
- **Class A**: `255.0.0.0`
- **Class B**: `255.255.0.0`
- **Class C**: `255.255.255.0`

### Private IP Ranges
- **Class A**: `10.0.0.0` to `10.255.255.255`
- **Class B**: `172.16.0.0` to `172.31.255.255`
- **Class C**: `192.168.0.0` to `192.168.255.255`

**Example**:
- For `150.10.20.30`:
  - Network ID: `150.10.0.0`
  - Broadcast ID: `150.10.255.255`
  - Usable IPs: `2^8 - 2 = 65534`

### Subnetting
- **Definition**: Dividing a large network into smaller, more manageable sub-networks.
- **Purpose**: Improves network efficiency and security.

### CIDR (Classless Inter-Domain Routing)
- **Class A CIDR**: `/8`
- **Class B CIDR**: `/16`
- **Class C CIDR**: `/24`

## Amazon VPC (Virtual Private Cloud)
Amazon VPC allows you to create a virtual network within AWS, closely resembling a traditional data center network.

- **Purpose**: Provides a virtual network space to launch AWS resources.
- **Benefits**: Full control over your virtual networking environment, including IP address range, subnets, route tables, and network gateways.

### VPC Features
- **Max VPCs**: Up to 5 VPCs per AWS account.
- **Max Subnets**: Up to 200 subnets per VPC.
- **Elastic IPs**: Up to 5 per VPC.
- **Automatic Creation**: DHCP, Network ACLs (NACLs), and Security Groups are automatically created.

### Types of VPC
1. **Default VPC**:
   - Automatically created in each AWS region.
   - Includes a default CIDR block, security groups, NACLs, route tables, and an internet gateway.
   - Used by default when launching EC2 instances if a custom VPC is not specified.

2. **Custom VPC**:
   - Created manually by the AWS account owner.
   - Allows specifying the CIDR block and configuring security groups, NACLs, and route tables.
   - Requires manual creation of an internet gateway if needed.

### Public vs. Private Subnets
- **Public Subnet**:
  - Routed to an internet gateway.
  - Instances need a public IP or Elastic IP to communicate with the internet.

- **Private Subnet**:
  - Not routed to an internet gateway.
  - Instances do not have direct internet access.

**Reserved IPs in Subnets**:
- `10.0.0.0` -> Reserved for VPC router
- `10.0.0.1` -> Reserved for VPC route
- `10.0.0.2` -> Reserved for DNS server
- `10.0.0.3` -> Reserved for future use
- `10.0.0.255` -> Broadcast address


## Components of VPC
### CIDR & IP Addressing
- **CIDR (Classless Inter-Domain Routing)**: A method for specifying IP address ranges. CIDR notation is written as `<IP_Address>/prefix_length`, where `prefix_length` defines the number of bits in the subnet mask. For example, `192.168.1.0/24` indicates a network where the first 24 bits are the network part of the address.
- **IP Addressing**: Within a VPC, you assign IP addresses to various components. You can define private IP address ranges for your VPC, and these ranges can be divided into subnets to segment your network.

### Implied Router & Route Table
- **Implied Router**: Each VPC automatically includes an implied router, which is responsible for routing traffic between subnets within the VPC and handling the routing between your VPC and the internet or other AWS services.
- **Route Table**: A set of rules (routes) that determine where network traffic is directed. Each subnet in a VPC is associated with a route table, which controls the traffic routing between subnets and to/from the internet, VPN, or other VPCs.

### Internet Gateway
- **Purpose**: An Internet Gateway (IGW) allows instances in your VPC to connect to the internet. It facilitates bidirectional communication between your VPC and the internet.
- **Function**: Provides a route to the internet for instances in public subnets, enabling them to access the internet and receive inbound traffic from the internet.

### Security Groups
- **Purpose**: Security Groups act as virtual firewalls for your instances to control inbound and outbound traffic. They are associated with EC2 instances and can be used to define rules that allow or deny traffic based on IP address, port, and protocol.
- **Characteristics**:
  - **State-aware**: Security Groups automatically allow return traffic for established connections.
  - **Instance Association**: Can be applied to multiple instances.

### Network ACLs (Access Control Lists)
- **Purpose**: Network ACLs control inbound and outbound traffic at the subnet level, providing an additional layer of security by allowing or denying traffic based on rules.
- **Characteristics**:
  - **Stateless**: Rules must be defined for both inbound and outbound traffic separately.
  - **Subnet Application**: Applied to all instances in a subnet.

### Virtual Private Gateway
- **Purpose**: A Virtual Private Gateway (VGW) connects your VPC to an on-premises network via a VPN connection. It allows secure communication between your AWS environment and your on-premises network.
- **Function**: Acts as a bridge between the VPC and your on-premises network, enabling encrypted communication over the internet.

### Peering Connection
- **Purpose**: A VPC Peering Connection allows you to connect two VPCs, enabling them to route traffic between each other as if they were within the same network.
- **Use Cases**: Useful for sharing resources between VPCs, such as databases or applications, or integrating different environments.

### Elastic IPs
- **Purpose**: An Elastic IP (EIP) is a static, public IP address designed for dynamic cloud computing. Unlike standard public IPs, Elastic IPs remain the same across instance stops and starts.
- **Function**: Provides a way to maintain a fixed IP address for your instances, ensuring that your application's IP address does not change.

### NAT (Network Address Translation)
- **Purpose**: NAT conserves IP addresses by allowing private IP networks to connect to the internet using a single public IP.
- **Types**:
  - **NAT Instance**: A legacy solution for enabling outbound internet traffic for instances in a private subnet.
  - **NAT Gateway**: A managed service offering better availability, higher bandwidth, and less administrative effort.

## AWS Direct Connect
- **Purpose**: AWS Direct Connect establishes a private connection between your premises and AWS. It provides better network performance and throughput compared to internet-based connections.

