# Azure Virtual Machines

## Table of Contents
1. [Overview](#overview)
2. [Types of Azure Virtual Machines](#types-of-azure-virtual-machines)
3. [Virtualization Recap](#virtualization-recap)
4. [Create a Virtual Machine in Azure](#create-a-virtual-machine-in-azure)
5. [Connect to the Virtual Machine](#connect-to-the-virtual-machine)
   - [Windows](#windows)
   - [Linux](#linux)
6. [Deploy Your First Application on an Azure VM](#deploy-your-first-application-on-an-azure-vm)
7. [Virtual Machine Scale Sets for Autoscaling](#virtual-machine-scale-sets-for-autoscaling)
8. [References](#references)

## Overview
Azure Virtual Machines provide on-demand, scalable computing resources. They allow users to run applications and software without needing physical hardware.

## Types of Azure Virtual Machines
1. **General Purpose**
   - **Use Case**: Balanced CPU and memory. Suitable for development and testing.
   - **Example**: B-series VMs for web servers.

2. **Compute Optimized**
   - **Use Case**: High CPU-to-memory ratio. Ideal for compute-intensive applications.
   - **Example**: F-series VMs for gaming servers.

3. **Memory Optimized**
   - **Use Case**: High memory-to-CPU ratio. Suitable for database servers.
   - **Example**: E-series VMs for SAP HANA.

4. **Storage Optimized**
   - **Use Case**: High disk throughput and IO. Best for large data processing.
   - **Example**: L-series VMs for data warehousing.

5. **GPU**
   - **Use Case**: Graphic-intensive workloads. Suitable for machine learning.
   - **Example**: NV-series VMs for AI training.

6. **High Performance Compute**
   - **Use Case**: Extremely fast CPUs and high-performance networking.
   - **Example**: H-series VMs for simulations.

## Virtualization Recap
Virtualization allows multiple virtual machines to run on a single physical server. Each VM operates independently with its own OS and applications.

## Create a Virtual Machine in Azure
1. **Log in** to the Azure Portal.
2. **Navigate** to "Create a resource" > "Compute" > "Virtual Machine".
3. **Configure** settings (name, region, size, image).
4. **Review** and create the VM.

## Steps to Attach an Extra Disk to a VM

### 1. Log in to Azure Portal
1. Navigate to [Azure Portal](https://portal.azure.com).
2. Sign in with your Azure account credentials.

### 2. Navigate to the Virtual Machine
1. In the Azure portal, go to the **"Virtual machines"** service.
2. Select the VM to which you want to attach the disk.

### 3. Stop the Virtual Machine
1. Click on the **"Stop"** button to deallocate the VM if it is currently running.
2. Wait for the VM status to change to **"Stopped (deallocated)"**.

### 4. Add a New Data Disk
1. In the VM's menu, under **"Settings"**, click on **"Disks"**.
2. Click on the **"+ Add data disk"** button.
3. In the **"Name"** field, select **"Create disk"**.
4. Fill in the required details for the new disk:
    - **Name**: Provide a name for the new disk.
    - **Resource group**: Select the same resource group as the VM.
    - **Location**: Choose the same region as the VM.
    - **Size**: Specify the size of the disk in GB.
    - **Performance**: Choose between Standard (HDD), Premium (SSD), or Ultra (SSD) based on your requirements.
5. Click on **"Create"** to create the new disk.
6. The new disk will appear in the **"Data disks"** section of the VM.

### 5. Save and Apply Changes
1. Click on the **"Save"** button to apply the changes.
2. Wait for the disk to be attached to the VM.

### 6. Start the Virtual Machine
1. Click on the **"Start"** button to start the VM.
2. Wait for the VM status to change to **"Running"**.

## Connecting to a Linux VM

### 1. Obtain the VM's Public IP Address
1. In the Azure portal, navigate to the **"Virtual machines"** service.
2. Select your VM.
3. In the VM's overview page, find the **"Public IP address"**.

### 2. Connect via SSH
1. Open a terminal on your local machine.
2. Use the following command to connect to your VM, replacing `<username>` with your VM's username and `<public-ip>` with the VM's public IP address:
    ```bash
    ssh <username>@<public-ip>
    ```
3. If you are using an SSH key for authentication, make sure to specify the path to your private key:
    ```bash
    ssh -i C:\Users\admin\Downloads\linuxdevelopment_key.pem azureuser@20.197.21.57
    
    ssh -i /path/to/private-key <username>@<public-ip>
    ```

### 3. Verify Connection
1. Once connected, you should see a welcome message from your VM, indicating that you are now logged in.

## Connecting to a Windows VM

### 1. Obtain the VM's Public IP Address
1. In the Azure portal, navigate to the **"Virtual machines"** service.
2. Select your VM.
3. In the VM's overview page, find the **"Public IP address"**.

### 2. Connect via Remote Desktop (RDP)
1. Open Remote Desktop Connection on your local machine. You can search for "Remote Desktop Connection" in the Start menu.
2. In the Remote Desktop Connection window, enter the VM's public IP address in the **"Computer"** field and click **"Connect"**.
3. A login prompt will appear. Enter your VM's username and password.
4. Click **"OK"**. You may receive a warning about the certificate. Click **"Yes"** to continue.

### 3. Verify Connection
1. Once connected, you should see the Windows desktop of your VM, indicating that you are now logged in.

## Initialize and Format the New Disk to enable additional Disk

### For Linux VM
1. Connect to the VM using SSH.
2. Use `lsblk` to list the available disks and identify the new disk (e.g., `/dev/sdc`).
3. Create a partition using `fdisk` or `parted`:
    ```bash
    sudo fdisk /dev/sdc
    ```
4. Create a filesystem on the new partition:
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
5. Create a mount point and mount the new disk:
    ```bash
    sudo mkdir /mnt/newdisk
    sudo mount /dev/sdc1 /mnt/newdisk
    ```
6. Update `/etc/fstab` to mount the disk automatically at boot:
    ```bash
    echo '/dev/sdc1 /mnt/newdisk ext4 defaults,nofail 0 2' | sudo tee -a /etc/fstab
    ```

### For Windows VM
1. Connect to the VM using RDP.
2. Open **"Disk Management"**.
3. You should see the new disk listed as **"Offline"**. Right-click on it and select **"Online"**.
4. Right-click on the unallocated space and select **"New Simple Volume"**.
5. Follow the wizard to assign a drive letter and format the disk.

## Virtual Machine Scale Sets for Autoscaling
- **Definition**: Automatically manage and scale the number of VMs based on demand.
- **Use Case**: Web applications that experience variable traffic.
- **Example**: Set up a scale set to increase instances during high traffic and decrease during low traffic to optimize costs.

### Example:
1. **Create a Scale Set** in the Azure portal.
2. **Define** scaling rules based on CPU usage.
3. **Deploy** your application to the scale set.
4. **Monitor** performance and adjust scaling as necessary.

## References
- [Azure Virtual Machines Documentation](https://docs.microsoft.com/en-us/azure/virtual-machines/)
- [Azure Virtual Machine Scale Sets](https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/)
