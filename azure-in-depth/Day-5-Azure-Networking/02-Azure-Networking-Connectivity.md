# Azure Virtual Network (VNet) Connectivity

Azure Virtual Network (VNet) connectivity allows you to connect and integrate different VNets to enable seamless communication between resources in your cloud environment. This can be done within the same region or across different regions globally.

1) VNet to VNet Peering
2) Global VNet Peering

## VNet to VNet Peering

VNet to VNet peering allows you to connect virtual networks within the same Azure region. This enables resources in different VNets to communicate with each other using private IP addresses.

### Real-Time Use Case

**Scenario:** A technology company operates several applications in Azure. Their development and production environments are hosted in separate VNets within the same region to maintain isolation and security.

**Solution:** VNet to VNet peering is implemented to allow secure communication between these environments. Developers can access necessary production data without exposing it to the internet, improving workflow efficiency while keeping sensitive information secure.

- **Same Subscription and Tenant:** The company's HR and finance applications are in different VNets but within the same subscription. VNet peering allows seamless data exchange for payroll processing without moving sensitive data over the internet.

- **Different Subscription, Same Tenant:** The company’s IT and marketing teams are in separate subscriptions but need to collaborate. VNet peering connects their environments, facilitating access to shared services like databases and file storage.

- **Different Subscription and Tenant:** In a strategic partnership with another company, the firms maintain separate subscriptions and tenants. VNet peering enables their systems to interact securely without merging their administrative domains.

## Global VNet Peering
Global VNet peering extends the capabilities of VNet peering to connect VNets across different Azure regions. This ensures low-latency, high-bandwidth connectivity without routing traffic over the public internet, keeping it on Microsoft’s private network.

### Real-Time Use Case

**Scenario:** An international e-commerce platform has data centres in multiple Azure regions. They need efficient, secure connectivity between these regions to provide a seamless shopping experience globally.

**Solution:** Global VNet peering is used to connect VNets in different regions. This allows the platform to synchronize inventory and user data in real-time, providing customers with accurate product availability and personalized experiences regardless of location.

- **Same Subscription and Tenant:** The platform's analytics and customer service teams operate in separate regions but under the same subscription. Global VNet peering ensures real-time data analysis and customer support, improving service delivery.

- **Different Subscription, Same Tenant:** The company’s European and North American divisions are in different subscriptions. Global VNet peering allows them to collaborate on international campaigns while maintaining regional autonomy.

- **Different Subscription and Tenant:** In a joint venture with another global retailer, the companies keep their networks separate but use global VNet peering to share logistics and supply chain data securely.


# Azure VNet Connectivity Lab Guide

This lab provides step-by-step instructions to set up Azure Virtual Network (VNet) connectivity for various scenarios.

## Prerequisites

- An active Azure subscription
- Basic knowledge of Azure Portal, Azure CLI, or Azure PowerShell

## Scenario 1: VNet to VNet Peering (Same Region)

### Objective

Connect two VNets in the same region to allow secure communication between resources.

### Steps

1. **Create VNets:**

   - Go to the Azure Portal.
   - Navigate to "Create a resource" > "Networking" > "Virtual Network".
   - Create `VNet1` with the address space `10.1.0.0/16`.
   - Create `VNet2` with the address space `10.2.0.0/16`.

2. **Create Subnets:**

   - In `VNet1`, add a subnet named `Subnet1` with the range `10.1.1.0/24`.
   - In `VNet2`, add a subnet named `Subnet2` with the range `10.2.1.0/24`.

3. **Deploy Virtual Machines (Optional):**

   - Deploy a VM in each VNet to test connectivity later.
   - Ensure each VM is placed in its respective subnet.

4. **Set Up VNet Peering:**

   - Go to `VNet1` and select "Peering" under Settings.
   - Click "Add" and fill in the details:
     - Name: `VNet1ToVNet2`
     - Virtual Network: `VNet2`
   - Go to `VNet2` and create a peering back to `VNet1`:
     - Name: `VNet2ToVNet1`
     - Virtual Network: `VNet1`

5. **Test Connectivity:**

   - SSH or RDP into the VM in `VNet1`.
   - Ping the IP address of the VM in `VNet2` to verify connectivity.

```

```

## Scenario 2: Global VNet Peering (Different Regions)

### Objective

Connect VNets across different Azure regions for seamless communication.

### Steps

1. **Create VNets:**

   - In the Azure Portal, create `VNet3` in East US with the address space `10.3.0.0/16`.
   - Create `VNet4` in West Europe with the address space `10.4.0.0/16`.

2. **Create Subnets:**

   - In `VNet3`, add a subnet named `Subnet3` with the range `10.3.1.0/24`.
   - In `VNet4`, add a subnet named `Subnet4` with the range `10.4.1.0/24`.

3. **Deploy Virtual Machines (Optional):**

   - Deploy a VM in each VNet for testing.

4. **Set Up Global VNet Peering:**

   - Go to `VNet3` and select "Peering" under Settings.
   - Click "Add" and fill in the details:
     - Name: `VNet3ToVNet4`
     - Virtual Network: `VNet4`
   - Go to `VNet4` and create a peering back to `VNet3`:
     - Name: `VNet4ToVNet3`
     - Virtual Network: `VNet3`

5. **Test Global Connectivity:**

   - SSH or RDP into the VM in `VNet3`.
   - Ping the IP address of the VM in `VNet4` to verify global connectivity.

## Additional Scenarios

### Peering Across Subscriptions

- Ensure both subscriptions have access to each other’s resources and are in the same Azure AD tenant.
- Use the same steps as above, specifying the subscription details during VNet creation and peering.

### Peering Across Tenants

- Establish guest access and permissions between tenants.
- Follow similar steps as above, ensuring tenant-specific permissions are configured for peering.

