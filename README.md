# Active Directory Virtual Home Lab
This GitHub repo is to demonstrate and show my journey on learning Microsoft's **Active Directory** system used in **IT Help Desk** and **Support Roles**. I’m using **Windows Server 2022** and **Windows 11** virtual machines inside **VirtualBox** to simulate a small business network and practice real-world IT administration skills.


## Network Diagram

Here is a visualization of what is happening in this Active Directory home lab and the connections between the Domain Controller to the Windows Client Machine

![active-directory-diagram](active_directory_diagram.jpg)

## Lab Overview:

This homelab project will cover:
  - Installing and configuring **Windows Server 2022**
  - Setting up **Active Directory Domain Services (AD DS)**
  - Creating and managing **users, groups, and organizational units**

  - Configuring **DNS**, **DHCP**, and **Remote Acess**
  - Applying **Group Policy Objects (GPOs)**
  - Joining a **Windows 11 client** to the domain
  - Using **PowerShell** for automation and administrative tasks

---

## 📘 Documentation Index

Each document below covers a specific phase of the Active Directory homelab and builds on the previous steps.

---

### 🖥️ Server & Client Setup
- [01 – Windows Server Installation](./setup/01_windows-server-installiation.md)  
  _Covers Windows Server 2022 installation, initial configuration, and VM setup._

- [06 – Windows Client Setup](./setup/06_windows-client-setup.md)  
  _Documents Windows 10/11 client VM setup, domain joining, and initial testing._

  ----

### 🌐 Network & Domain Configuration
- [02 – Network Configuration](./setup/02_network-configuration.md)  
  _Details internal network setup, static IP assignment, DNS configuration, and VM connectivity._

- [03 – Active Directory Setup](./setup/03_active-directory-setup.md)  
  _Step-by-step Active Directory Domain Services installation and domain promotion._

- [04 – Remote Access & DHCP Setup](./setup/04_remote-access-DHCP-setup.md)  
  _Covers DHCP scope creation, Remote Access (NAT), and client connectivity._

  ----

### 👤 User & Account Management
- [05 – Bulk User Creation in Active Directory](./setup/05_bulkusers_active-directory.md)  
  _Uses PowerShell automation to create multiple users for enterprise-scale testing._

- [07 – User Account Management](./setup/07_user_account_management.md)  
  _Simulates real help desk scenarios such as enabling/disabling users, password resets, and account unlocks._

  -----

### 🛡️ Group Policy & Security
- [08 – Group Policy Management](./setup/08_group_policy_management.md)  
  _Documents creation, enforcement, and verification of Group Policy Objects for security and user restrictions._

---

## Progress Logs

| Date | Topic | Description |
|------|--------|-------------|
| 2025-10-20 | Windows Server Installation | Installed Windows Server 2022 on VirtualBox and set up the initial Administrator account. |
| 2025-10-22  | Domain Configuration | Configured Windows Server 22 VM to use Active Directory server's IP Address as its DNS server to connect client and DC VMs together |
| 2025-10-24 | Active Directory Installiation | Installed Active Directory Domain Services to Server 2022 for promoting server to Domain Controller. Named domain to jotewodomain.com |
| 2025-10-25 | New User Creation | Opened Active Directory Users and Computers application, practiced creating new user account by adding all information like name, creating password, etc |
| 2025-10-27 | Creating Local Admin Account | Created an Organizational Unit (OU) for Admins and added a new Admin account with appropriate permissions. Tested login under the new admin credentials successfully. |
| 2025-10-29 | Remote Access Configuration | Installed Remote Access on Server in order for client machines within the internal network to have access to the internet with NAT |
| 2025-10-31 | DHCP Server Configuration | Installed and configured the DHCP role on the Domain Controller to automatically assign IP addresses within the internal network via a defined DHCP Scope and subnet. |
| 2025-11-02 | PowerShell AD Automation | Ran a PowerShell script from Josh Madakor’s AD Homelab tutorial that automatically created hundreds of random user accounts within a specific Organizational Unit in Active Directory to simulate a real-world enterprise environment. |
| 2025-11-06 | Windows 10 Client Installation | Installed Windows 10 Pro VM for Client after dealing with issues with Windows 11 OS. Created local user account. Added router to DHCP Server on Domain Controller to connect with client VM |
| 2025-11-07 | Account Management Testing | Tested enabling and disabling user accounts on the Windows 10 client VM through Active Directory Users and Computers to simulate real-world account management scenarios. Verified that disabled accounts were unable to log in and re-enabled accounts regained access successfully. |
| 2025-11-09 | Group Policy Configuration | Created and tested common Group Policy Objects (GPOs) such as password complexity, account lockout policies, and disabling Command Prompt for standard users to strengthen security and practice centralized policy management. |
| 2025-11-11 | Group Policy Testing | Tested enforced GPOs such as account lockout and restrictions on Control Panel and Command Prompt access for client users. Additionally, practiced unlocking a locked-out user account through Active Directory Users and Computers to simulate real-world account recovery procedures. |
| 2025-11-15 | File Sharing & Permissions | Created a shared folder in Server Manager and configured file-share permissions. Set up department-based security groups (e.g., HR, Front Desk) and assigned users to each group to test access control. Verified that only authorized groups could access specific folders and practiced mapping the shared folder as a network drive on the client machine. |
| 2025-11-19 | Advanced File Sharing & OU Organization | Continued practicing file sharing by creating additional department-based security groups such as Sales and Marketing and assigning users accordingly. Also created separate Organizational Units (OUs) for each department to improve user organization and streamline permission management. |
| 2025-11-26 | Remote Desktop Services | Researched how to enable and configure Remote Desktop for domain-joined clients, including setting up an RDP access group, applying the necessary Group Policy settings, and confirming remote access using MSTSC. |
| 2025-12-03 | Remote Desktop Services Part 2 | Continued configuring Remote Desktop in the lab by enabling RDP on the client VM, testing admin access, and researching how to let administrators access specific user desktops through Remote Desktop. |
| 2025-12-14 | Help Desk Role Design | Designed a least-privilege Help Desk role in Active Directory by creating a dedicated HelpDesk security group, organizing privileged accounts into a separate OU, and planning OU-based delegation to avoid assigning Domain Admin rights while still allowing user support tasks. |
| 2025-12-15 | Help Desk Delegation & Remote Access | Delegated Help Desk permissions for password resets and account unlocks using the Delegate Control Wizard on user OUs, and configured Remote Desktop access for Help Desk users by adding the HelpDesk group to the Remote Desktop Users group via computer-based Group Policy. Verified that Help Desk accounts could support users without accessing Domain Controllers. |
| 2025-12-16 | RSAT Installation & Troubleshooting | Installed Remote Server Administration Tools (RSAT) on a domain-joined Windows client for Help Desk use, troubleshooting installation failures caused by Windows Update connectivity and DNS forwarding misconfigurations in the Active Directory lab. Confirmed successful access to Active Directory Users and Computers (ADUC) from a non-admin Help Desk account. |
| 2025-12-18 | Restricting ADUC Access with GPO | Implemented a user-based Group Policy to restrict access to Active Directory Users and Computers (ADUC) for standard client users by limiting Microsoft Management Console snap-ins. Applied the policy to regular user OUs while excluding Help Desk accounts through OU separation and security filtering, ensuring only authorized support staff could access AD administrative tools. |
| 2025-12-26 | Group Policy – Personal Network Drives | Configured Group Policy Objects to map personal network drives for users across the Users OU, ensuring each user receives a private, automatically mapped personal folder upon login. |
| 2026-01-08 | Group Policy – Verification/Fix | Verified and fixed Group Policy application issues by correcting GPO links and enforcement on the Users OU, ensuring user-level policies such as a universal desktop wallpaper and Command Prompt restrictions were properly applied on client machines. |
| 2026-01-18 | Remote Desktop Services Part 3 | Used Remote Desktop from the server to connect to a client machine and create a folder on a user’s desktop to verify administrative access and user-level file management through RDP. |
| 2026-01-24 | Remote Desktop Services – Help Desk RDP Configuration | Successfully configured Help Desk users to remotely access client machines via RDP by applying the correct Group Policy permissions and security group assignments, resolving prior authorization issues. |
| 2026-02-08 | Group Policy & RDP Session Behavior Testing | Validated how Group Policy Objects apply during Remote Desktop sessions by testing Help Desk logins on domain-joined machines, confirming user- and computer-based GPO processing, session isolation from Domain Admin logins, and documenting best-practice restrictions for Domain Controller access. |
| 2026-02-14 | Dell Personal Laptop Audio Troubleshooting – Code 45 Resolution | Diagnosed a “No audio device installed” issue on my personal Dell laptop where Realtek High Definition Audio appeared greyed out in Device Manager with error Code 45 (hardware not connected). Verified Windows Audio services were running and confirmed BIOS audio settings were enabled. Resolved the issue by uninstalling the Realtek audio driver and rebooting the system, allowing Windows to automatically redetect and reinstall the device successfully. |

## Tools Used
- [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Windows Server 2022 Standard (Desktop Experience)](https://go.microsoft.com/fwlink/p/?linkid=2195686&clcid=0x409&culture=en-us&country=us)
- [Windows 11 Enterprise](https://go.microsoft.com/fwlink/p/?linkid=2195682&clcid=0x409&culture=en-us&country=us)
- PowerShell
- Active Directory Domain Services (AD DS)
- Remote Access
- DNS & DHCP
