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

### Step 1: Verify Remote Desktop is disabled on Client Machine

1. Boot up and login to the **Client VM** with a **Domain Admin** account.
2. Open **Settings** > **System** > **Remote Desktop**.
3. You should observe that the **"Enable Remote Desktop** option is turned off and is greyed out to confirm that **Remote Desktop** isn't enabled on the machine prior.

Because the client machine is joined to the **Active Directory** domain, **Remote Desktop settings** are controlled by **Group Policy Objects (GPOs)**. Domain-level policies override local system settings, preventing Remote Desktop from being enabled locally on the client machine.

![ClientRDP](./screen-recordings/ClientRDP1.gif)

### Step 2: Add Authorized Users to the Built-In Remote Desktop Users Group

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

### Step 3: Create a Group Policy Object for RDP Access

1. Open the **Group Policy Management Console** either through **Server Manager** or searching it during the search bar.
2. Locate and right-click on the **_COMPUTERS** OU.
3. Select **Create a GPO in this domain, and Link it here...**
4. Name the following GPO: **Allow Remote Desktop Access**.
5. Click **"OK"** to confirm the GPO creation.

![RDP3](./screen-recordings/RDP3.gif)

### Step 4: Enable Remote Desktop Connections via GPO

The purpose of the policy for **Enabling Remote Desktop Connections** is to simply allow Remote Desktop Access on the client machine.

Domain-joined computers rely on **Group Policy** to control RDP behavior. Enabling this policy ensures that **Remote Desktop** is explicitly permitted at the system level instead of relying on local machine settings, which are overridden in a domain environment.

1. Right-click the newly created **Allow Remote Desktop Access** GPO -> **Edit**.
2. Navigate to: **Computer Configuration** > **Policies** > **Adminstrative Templates** > **Windows Components** > **Remote Desktop Services** > **Remote Desktop Session Host** > **Connections**.
3. Locate the following policy: **"Allow users to connect remotely using Remote Desktop Services."**
4. Set the policy to **Enabled**. This will allow computers to enable Remote Desktop Access and connections to be made.

![RDP4](./screen-recordings/RDP4.gif)

### Step 5: Allow log on through Remote Desktop Services

The purpose of this policy is to determine which users or groups are allowed to log on using **Remote Desktop**.

Even if **Remote Desktop** is enabled, users will be denied access unless they are granted the “Log on through Remote Desktop Services” right.

By assigning this right to the **Remote Desktop Users Security Group**, you:
- Allow support staff to remotely access user desktops.
- Avoid granting Domain Admin or local administrator privileges.
- Follow the principle of least privilege.

1. In the same GPO, navigate to:
    - **Computer Configuration** > **Policies** > **Windows Settings** > **Security Settings** > **Local Policies** > **User Rights Assignment**
2. Edit the following setting: **Allow log on through Remote Desktop Services**.
3. Check the **Define these policy settings** checkbox to add groups.
4. Add the **Remote Desktop Users Group** that you created earlier in Step 0 that contains help desk users and domain admins.

![RDP7](./screen-recordings/RDPStep5.gif)

### Step 6: Ensure No Deny Policy Conflicts

The purpose of this step is to ensure that no users or groups that are being denied logging on through **Remote Desktop** that should have that permission.

Still under **User Rights Assignment**, verify that the following policy, **"Deny log on through Remote Desktop Services"**, is not defined or doesn't have any group that should have access like **Remote Desktop Users Group**.

Deny policies override allow policies.

### Step 7: Allow inbound Remote Desktop exceptions through Windows Defender Firewall

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

### Step 8: Enforce Group Membership using Restricted Groups

The purpose of configuring this policy is to automatically manage and enforce membership of the local **Remote Desktop Users** group on all client machines. This eliminates manual configuration and ensures consistency

1. Navigate to:
    - **Computer Configuration** > **Policies** > **Windows Settings** > **Security Settings** > **Restricted Groups**
2. Right-click on the empty group list and select **Add Group**.
3. Click the **Browse** button, type **"Remote Desktop"** and click the **Check Names** button. You should see the **Remote Desktop Users** Group appear > Select that group.
4. Click **OK** on the Add Group window.
5. The properties window should appear. Click on the **Add** button that is next to **Members of this group**.
6. Add the following groups as members:
    - **Domain Admins**
    - **Any Help Desk Group**
7. After adding those groups, click **OK** to close the box to complete the addition of these groups to the **Remote Desktop Users Group**.

![Step8](./screen-recordings/RDPStep8.gif)

This ensures every client machine automatically includes the correct RDP groups.

### Step 9: Apply and Update Group Policy

To immediately apply new policy settings and ensure **User Rights Assignments** take effect.

- Boot up the client VM.
- Sign in with an account that is permitted to use the **Command Prompt**
- Open the Command Prompt.
- Execute the following command: ```gpupdate /force``` to update the newly created GPOs
- Reboot the client VM.

### Step 10: Test Remote Desktop Connectivity

In this final step, we are going to validate that the configuration of **Remote Desktop** is functioning correctly and only authorized users can connect.

1. Boot up the Domain Controller VM and login.
2. Open **Remote Desktop Connection** by searching for it in the search bar.
3. The window will pop up where you need to provide the **Computer Name** of the client machine and the username of the user you want to sign in with.
    - **Computer Name**: CLIENT1
    - **Username**: DOMAINNAME\USERNAME (e.g JOTEWODOMAIN\\hd-jdudley)
4. Click **Connect** and enter the password for the **Domain Admin** or the **Help Desk** user. 
5. If configured properly, the connection to the client machine should succeed and you should be logged in with the Admin or help desk account!

![Step10](./images/RDPStep10.png)
![Step10b](./images/RDPStep10a.png)

## Conclusion:

Successfully configuring and validating **Remote Desktop Services (RDP)** through **Group Policy** demonstrates centralized access control within the **Active Directory environment**. By enabling RDP, assigning proper user rights, configuring firewall exceptions, and enforcing security group membership, remote access is managed securely and consistently across all domain-joined client machines.

This implementation reflects real-world IT administration practices by enforcing the principle of least privilege, reducing manual configuration, and ensuring scalable, policy-based management of remote support access.