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





