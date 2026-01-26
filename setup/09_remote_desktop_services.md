# Remote Desktop Services(RDP) Configuration

## Objective:

This section demonstrates how **Remote Desktop Services(RDP)** is configured within an **Active Directory environment** to allow authorized adminstrators and Help Desk users to remotely access domain-joined client machines.

**Remote Desktop** is a critical tool used by **IT Support** and **System Adminstrators** for troubleshooting, maintenance, and user support while enforcing **Least-Privilege Access**.

## Prequisites: 
Before completing this section of the homelab, it is important to have followed the previous setup documents and have configured the following:
- Windows Server 2022 Domain Controller
- Active Directory Domain Services(AD DS)
- Organizational Units (OU) created
- Domain Users created and managed
- Windows client machine joined to the domain
- Basic user account management completed
- Basic Group Policy Knowledge
- Help Desk Security Group created

---

## Overview:

The purpose of **Remote Desktop Services(RDS)** allows authorized users to connect to another computer over the network using the **Remote Desktop Protocol(RDP)**. In enterprise environments, RDP access is tightly controlled to prevent unauthorized access to systems/

In this lab, I will demonstrate how to: 

- Enable Remote Desktop on domain-joined client machines
- Create a security group to control RDP access
- Use Group Policy to grant Remote Desktop permissions
- Restrict Remote Desktop access for standard users
- Test and troubleshoot RDP connectivity

---

### Step 0: Verify Remote Desktop is disabled on Client Machine

1. Boot up and login to the **Client VM** with a **Domain Admin** account.
2. Open **Settings** > **System** > **Remote Desktop**.
3. You should observe that the **"Enable Remote Desktop** option is turned off and is greyed out to confirm that **Remote Desktop** isn't enabled on the machine prior.

Because the client machine is joined to the **Active Directory** domain, **Remote Desktop settings** are controlled by **Group Policy Objects (GPOs)**. Domain-level policies override local system settings, preventing Remote Desktop from being enabled locally on the client machine.

![ClientRDP](./screen-recordings/ClientRDP1.gif)

### Step 1: Create a Remote Desktop Security Group

1. Boot up and log into the **Domain Controller VM**
2. Open **Active Directory Users and Computers(ADUC)**
3. Navigate to the standard **Users** OU under your domain(Not the created **_USERS**).
4. Right-Click > **New** > **Group**.
5. Create the following group:
    - **Group Name:** HelpDesk-RDP
    - **Group Scope:** Global
    - **Group Type:** Security

![RDP1](./screen-recordings/RDP1.gif)

6. Right-Click on the newly created security group > **Properties**.
7. The **Properties** window will pop up and go to the **"Members"** tab.
8. Add Help Desk and administrative users to this group.

![RDP2](./images/RDP2.png)

This group will be used to control which users are allowed to remotely access client machines.

---

