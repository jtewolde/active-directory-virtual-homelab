# Remote Access and DHCP Server Setup

## Objective:
In this section, I will show how to configure **Remote Access (NAT Routing)** and **DHCP Server** on the Windows Server 2022 Domain Controller. These services enable client machines in the internal network to:
- Access the internet through the Domain Controller
- Automatically receive IP Addresses, default gateway, DNS settings, and subnet mask
- Communicate properly within the lab environment

Essentially, this configuration allows for Windows 10 client VMs to join the domain and operate like real corporate workstations.

## Overview:
We will complete two major configurations: **NAT Routing** and **DHCP Server**.

1. **Remote Access(NAT Routing)**:
    - This allows for the Domain Controller to act like a **Router** for the internal network. The usage of NAT allows for the DC's outbound interface to touch the internet, while the internal network remains isolated.
2. **DHCP Server**:
    - The **DHCP** role will automatically assign/lease out IP addresses and network settings to all internal client machines. 

## Step 1: Install Remote Access (NAT) and DHCP Server Roles
1. Open up **Server Manager** > Click **Manage** (top-right) > **Add Roles and Features**.
2. A Wizard should pop up, click **Next** until you reach the **Server Roles** Section.
3. Check the boxes for **DHCP Server** and **Remote Access**,
4. Click 'Next' until you reach **Role Services** > Select **Routing** and click **Add Features** when prompted.
5. Continue clicking **Next** until you reach the **Confirmation** Page, then click **Install**.
6. Wait for the installation to finish and then close the window

![DHCP_Remote](./screen-recordings/DHCP1.gif)

## Step 2: Enable NAT Routing

