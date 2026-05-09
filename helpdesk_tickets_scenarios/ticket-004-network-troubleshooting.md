# Ticket 004 - User Unable to Access Internet

---

This document demonstrates the process of troubleshooting and resolving a network connectivity issue where a user is unable to access the internet within an **Active Directory** environment. The ticket was created and tracked using **Jira Service Management** to simulate a real-world IT help desk workflow. The steps below outline how network configuration, DHCP settings, and connectivity were verified and corrected on a Windows Server 2022 domain controller and client machine.

## Ticket Information:
- **Ticket Key:** SUP-9
- **Request Type:** Network / Internet Access Issue
- **Priority:** High
- **Status:** Waiting for Support
- **Reported by:** csutton@lab.local
- **Assigned Technician:** Joseph Tewolde

---

## Ticket Creation:

A support request was submitted through **Jira Service Management** after a user reported that they were unable to access the internet on their workstation. The user stated that they can't use Google Chrome or go on any websites despite being logged into the system.

The ticket was categorized as a **Network Connectivity Issue** and assigned to IT support for investigation.

![Ticket009](/images/Ticket009.png)

---

## Ticket Assignment and Status Updates

1. The ticket was **assigned to Joseph Tewolde**.
2. The ticket status was updated from **Waiting for Support → In Progress**.
3. Initial troubleshooting notes were added to document the investigation.

---

## Issue Description:

The user reported that they were unable to access external websites from their workstation. The system appeared to be functioning normally otherwise, and the user was able to log into the domain successfully.

This suggested that the issue was likely related to **network configuration**, specifically involving the default gateway or DHCP settings.

---

## Lab Environment (Simulation):

- **Domain Controller:** Windows Server 2022  
- **Client Machine:** Windows 10 / Windows 11 Domain-Joined Workstation  
- **Directory Service:** Active Directory Domain Services (AD DS)  
- **Network Services:** DHCP, NAT (Remote Access)  
- **Ticketing Platform:** Jira Service Management  

To simulate a realistic enterprise networking issue, the DHCP Scope on the Domain Controller was intentionally misconfigured by removing the configured **Default Gateway** under: **DHCP Option 003 - Router**.

---

## Step 1: Simulate the DHCP Network Issue

1. Boot up and log into the **Windows Server 2022 Domain Controller** using adminstrative credentials.
2. Open **Server Manager** and navigate to the **Tools** section > **DHCP**.
3. Click on the right arrow next to your domain to expand it > Right-Click on **IPv4** > **"Internal Scope"** > **Scope Options**.
4. Locate and double-click the following DHCP setting
    - **003 - Router**
5. Remove or intentionally misconfigure the **Default Gateway**:
    - Incorrect example: **172.16.0.99** or leave it blank.
6. Click **OK** to apply the changes.

This causes client machines to receive invalid routing information from DHCP, preventing internet access.

![DHCPRouter](/screen-recordings/DHCPRouter.gif)

## Step 2: Remote into User Machine (RDP)

1. First, boot up the **Windows Server 2022 Domain Controller** using adminstrative credentials.
2. Open **Remote Desktop Connection** by entering it in te search bar. 
3. Enter the client machine's Computer Name to idenitfy which workstation needs to be remoted into.
4. Log in using admin credentials to get access to the **Command Prompt**.

This allows direct access to the user’s desktop to troubleshoot the issue.

![RDPTicket9](/screen-recordings/Ticket009RDP.gif)

---

## Step 3: Verify IP Configuration

1. Open **Command Prompt** on the client machine.
2. Run the following command in the terminal to display all current **TCP/IP** network configurations:
```ipconfig /all```
3. Review the following configurations:
    - **IP Address**
    - **Subnet Mask**
    - **Default Gateway**
    - **DNS Server**
4. Look and identify any problems that could be causing the network issues for the computer.
    - In the screenshot below, you can see that the **Default Gateway** is incorrect where there is nothing configured. That is the most likely cause of this ticket.

![ipconfig/all](/images/ipconfigAll.png)

---

## Step 4: Test Network Connectivity
1. In the command prompt, use the following ping command to test external connectivity: ```ping 8.8.8.8``` 
    - If the request runs out, this indicates that the client machine is unable to reach the internet.
3. Next, test internal network connectivity by pinging the **Domain Controller**:```ping 172.16.0.1```
    - If this ping command is successful, it confirms that the client machine is connected within the internal network and can communicate within the **Domain Controller**.

This confirms that the issue is specifically related to outbound routing and internet access.

![pingTest](/images/pingTest.png)

## Step 5: Verify DHCP Configuratin on the Domain Controller

1. Return to the **Windows Server 2022 Domain Controller**.
2. Open **Server Manager** and navigate to the **Tools** section > **DHCP**.
3. Navigate to: **IPv4** > **Internal Scope** > **Scope Options**.
4. Locate and double-click the following DHCP setting
    - **003 - Router**
5. Verify that the configured default gateway is incorrect or missing.
6. Correct the **Default Gateway** to the previous IP Address:
    - 172.16.0.1
7. Click **OK** to save the correct configuration.

This ensures all **DHCP** clients receive the proper default gateway for internet routing.

![DHCPFix](/images/DHCPRouter1.png)

## Step 6: Renew DHCP Lease on Client Machine

After correcting the DHCP configuration, the client machine still retains the previous invalid lease.

To request updated network settings:
1. Return to the client machine through the RDP Session or signing directly into the machine.
2. Open **Command Prompt** as Adminstrator.
3. Run the following commands in the terminal:
    - ```ipconfig /release```: **Removes the current DHCP Lease**
    - ```ipconfig /renew```: **Requests updated network settings from the DHCP Server**.
4. Run the following command again: ```ipconfig /all```.
5. Verify that the following settings are now correct:
    - **Valid IP Address**
    - **Correct Subnet Mask**
    - **Default Gateway:** ```172.16.0.1```
    - **DNS Server:** ```172.16.0.1```

