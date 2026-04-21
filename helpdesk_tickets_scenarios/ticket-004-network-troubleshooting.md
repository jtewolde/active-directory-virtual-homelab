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

To simulate this issue in the homelab environment, the client machine was intentionally configured with an incorrect **default gateway**. This resulted in loss of internet connectivity while still allowing access to internal network resources.

---

## Step 1: Remote into User Machine (RDP)

1. First, boot up the **Windows Server 2022 Domain Controller** using adminstrative credentials.
2. Open **Remote Desktop Connection** by entering it in te search bar. 
3. Enter the client machine's Computer Name to idenitfy which workstation needs to be remoted into.
4. Log in using admin credentials to get access to the **Command Prompt**.

This allows direct access to the user’s desktop to troubleshoot the issue.

![RDPTicket9](/screen-recordings/Ticket009RDP.gif)

## Step 2: Verify IP Configuration

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

## Step 3: Test Network Connectivity
1. In the command prompt, use the following ping command to test external connectivity:
    - ```ping 8.8.8.8``` 
2. If the request runs out, this indicates that the client machine is unable to reach the internet.
3. Next, test internal network connectivity by pinging the **Domain Controller**:
    - Example: ```ping 172.16.0.1```
4. If this ping command is successful, it confirms that:
    - The client machine can communicate within the internal network.
    - The issue is specifically related to outbound internet connectivity.
5. This further supports that the problem is likely due to an incorrect or missing default gateway.

![pingTest](/images/pingTest.png)

## Step 4: Correct Network Configuration

Since the issue was identified as a missing/incorrect default gateway, the next step is to correct the network settings.

In **Command Prompt**, run the following commands:
- ```ipconfig /release```
- ```ipconfig /renew```

These commands force the client machine to request a new IP configuration from the **DHCP Server**, including: **IP Address**, **Default Gateway**, and **DNS Server**.


### Note: DHCP vs Static IP Configuration:

During troubleshooting, the `ipconfig /release` command may return the following error:

> *“The operation failed as no adapter is in the state permissible for this operation.”*

This typically occurs when the client machine is configured with a **static IP address instead of using DHCP**.

In this homelab scenario, the issue was intentionally created by manually assigning network settings (including an incorrect or missing default gateway). Because of this, the system is not using DHCP, and therefore the `/release` command cannot be executed.

