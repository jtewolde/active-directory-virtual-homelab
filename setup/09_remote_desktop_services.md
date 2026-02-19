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

### Step 1: Add Authorized Users to the Built-In Remote Desktop Users Group

Before configuring Group Policy, it is important to prepare the built-in Remote Desktop Users group. This group determines who is permitted to initiate Remote Desktop sessions on domain-joined systems.

Adding groups here allows centralized control of RDP access and will later be enforced through Group Policy to automatically apply to client machines.

1. Boot up and log into the **Domain Controller VM**
2. Open **Active Directory Users and Computers(ADUC)**
3. Navigate to the standard **Builtin** OU under your domain(Not the created **_USERS**).
4. Locate and double click on the **"Remote Desktop Users"** security group.
5. Once the **Properties** window appears, navigate to the **Members** tab.
6. Click the **Add** button to add new members and add the following groups:
    - **Domain Admins**
    - **Help Desk Users** or your help desk security group
7. Click **Apply** to save these changes.

![RDP1](./screen-recordings/RDPGroupCreation.gif)

**The built-in Remote Desktop Users group:**

- Grants permission to initiate RDP sessions

- Does NOT grant administrative privileges

- Supports the principle of least privilege
- Can be enforced and managed via GPO (Restricted Groups)

Later in this lab, we will use **Group Policy** to ensure this group membership is automatically applied to client machines for consistency and scalability.

---

### Configure Remote Desktop Via Group Policies

To centrally manage **RDP Access**, a **Computer-Based GPO** will be used to ensure that client machines can be remoted into authorized admins/employees. In a enterprise environment, this would be necessary for the IT Department to easily provide assistance remotely to client machines within the network.

#### Step 3: Create a Group Policy Object for RDP Access

1. Open the **Group Policy Management Console** either through **Server Manager** or searching it during the search bar.
2. Locate and right-click on the **_COMPUTERS** OU.
3. Select **Create a GPO in this domain, and Link it here...**
4. Name the following GPO: **Allow Remote Desktop Access**.
5. Click **"OK"** to confirm the GPO creation.

![RDP3](./screen-recordings/RDP3.gif)

#### Step 4: Enable Remote Desktop Connections via GPO

The purpose of the policy for **Enabling Remote Desktop Connections** is to simply allow Remote Desktop Access on the client machine.

Domain-joined computers rely on **Group Policy** to control RDP behavior. Enabling this policy ensures that **Remote Desktop** is explicitly permitted at the system level instead of relying on local machine settings, which are overridden in a domain environment.

1. Right-click the newly created **Allow Remote Desktop Access** GPO -> **Edit**.
2. Navigate to: **Computer Configuration** > **Policies** > **Adminstrative Templates** > **Windows Components** > **Remote Desktop Services** > **Remote Desktop Session Host** > **Connections**.
3. Locate the following policy: **"Allow users to connect remotely using Remote Desktop Services."**
4. Set the policy to **Enabled**. This will allow computers to enable Remote Desktop Access and connections to be made.

![RDP4](./screen-recordings/RDP4.gif)

#### Step 5: Allow log on through Remote Desktop Services

The purpose of this policy is to determine which users or groups are allowed to log on using **Remote Desktop**.

Even if **Remote Desktop** is enabled, users will be denied access unless they are granted the “Log on through Remote Desktop Services” right.

By assigning this right to a **Help Desk security group**, you:
- Allow support staff to remotely access user desktops.
- Avoid granting Domain Admin or local administrator privileges.
- Follow the principle of least privilege.

Inside of the same GPO you created:
1. Go to: **Computer Configuration** > **Policies** > **Windows Settings** > **Security Settings** > **Local Policies** > **User Rights Assignment**.
2. Add users and groups that you want to be allowed to log on using **Remote Desktop**. For example:
     - **HelpDesk-RDP**
     - **Domain Admins**

![RDP5](./screen-recordings/RDP5.gif)

#### Step 6: Allow inbound Remote Desktop exceptions through Windows Defender Firewall

The purpose of this policy is to allow **RDP Traffic (TCP 3389)** through the **Windows Firewall**.

Even with **Remote Desktop** enabled and user rights assigned, firewall restrictions will block connections unless RDP traffic is explicitly allowed.

Using **Group Policy** to manage firewall rules ensure:
- Consistent behavior across all client machines.
- No manual firewall configuration is required per machine.
- RDP access remains controlled and auditable.


Inside of the same GPO you created:
1. Go to: **Computer Configuration** > **Policies** > **Adminstrative Templates** > **Network** > **Network Connections** > **Windows Defender Firewall** > **Domain Profile** > 
    - Select this setting: **Windows Defender Firewall: Allow inbound Remote Desktop exceptions**.
2. Enable this setting wo allow computers in the network to receive Remote Desktop connection requests by opening **TCP Port 3389**.

![RDP6](./screen-recordings/RDP6.gif)

#### Step 7: Restrict Remote Desktop Access for Standard Users

The purpose of enabling this setting is to add **Help Desk Groups** to the **Local Remote Desktop Users** group on client machines.

This ensures that help desk users can:
- RDP into client machines
- Don't have to be local adminstrators
- Without manually configuring each client

This centralizes access control and simplifies ongoing management.

1. In the same GPO, navigate to:
    - **Computer Configuration** > **Policies** > **Windows Settings** > **Security Settings** > **Local Policies** > **User Rights Assignment**
2. Edit the following setting: **Allow log on through Remote Desktop Services**.
3. Add the following groups:
    - **Domain Admins**
    - OR a custom group like: **HelpDesk-RDP**

![RDP7](./screen-recordings/RDP7.gif)
