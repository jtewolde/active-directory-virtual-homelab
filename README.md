## Active Directory Virtual Home Lab
This GitHub repo is to demonstrate and show my journey on learning Microsoft's **Active Directory** system used in **IT Help Desk** and **Support Roles**.  
I’m using **Windows Server 2022** and **Windows 11** virtual machines inside **VirtualBox** to simulate a small business network and practice real-world IT administration skills.

---

## Lab Overview:

This homelab project will cover:
  - Installing and configuring **Windows Server 2022**
  - Setting up **Active Directory Domain Services (AD DS)**
  - Creating and managing **users, groups, and organizational units**
  - Configuring **DNS** and **DHCP**
  - Applying **Group Policy Objects (GPOs)**
  - Joining a **Windows 11 client** to the domain
  - Using **PowerShell** for automation and administrative tasks

## Progress Logs

| Date | Topic | Description |
|------|--------|-------------|
| 2025-10-20 | Windows Server Installation | Installed Windows Server 2022 on VirtualBox and set up the initial Administrator account. |
| 2025-10-22  | Domain Configuration | Configured Windows Server 22 VM to use Active Directory server's IP Address as its DNS server to connect client and DC VMs together |
| 2025-10-24 | Active Directory Installiation | Installed Active Directory Domain Services to Server 2022 for promoting server to Domain Controller. Named domain to jotewodomain.com |
| 2025-10-25 | New User Creation | Opened Active Directory Users and Computers application, practiced creating new user account by adding all information like name, creating password, etc |
| 2025-10-27 | Creating Local Admin Account | Opened AD and created an Organizational Unit for Admins and created new Admin account. Restarted VM and logged in successfully under that admin account |

## Tools Used
- Oracle VirtualBox
- Windows Server 2022 Standard (Desktop Experience)
- Windows 11 Enterprise
- PowerShell
- Active Directory Domain Services (AD DS)
- DNS & DHCP
