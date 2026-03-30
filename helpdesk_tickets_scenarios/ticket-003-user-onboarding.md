# Ticket 003 - New User Onboarding and Account Setup

---

This document demostrates the process of onboarding a new user within an **Active Directory** Environment. The ticket was created and tracked using **Jira Service Management** to simulate a real-world IT help desk workflow. The steps below outline how a new user account was created, configured with appropriate permissions, and prepared for first-time login within a Windows Server 2022 domain environment.

## Ticket Information:
- **Ticket Key:** SUP-08
- **Request Type:** New User Onboarding
- **Priority:** High
- **Status:** Waiting for Support
- **Reported by:** HR Department
- **Assigned Techinican:** Joseph Tewolde

---

## Ticket Creation

A request was submitted through **Jira Service Management** by the HR department to onboard a new employee. The request included the employee’s name, department, and required access to company resources.

The ticket was categorized as a **User Onboarding Request** and assigned to the IT support team to provision the necessary accounts and permissions.

![OnboardingTicket](/images/OnboardingTicket.png)

---

## Ticket Assignment and Status Updates

After reviewing the onboarding request, the ticket was assigned to the IT Support techincian for provisioning

1. The ticket was **assigned to Joseph Tewolde**.
2. The ticket status was updated from **Waiting for Support → In Progress**.
3. Initial notes were added outlining the onboarding steps to be completed.

![InternalNotes](/images/InternalNotesOnboarding.png)

---

## Lab Environment:

- **Domain Controller:** Windows Server 2022  
- **Client Machine:** Windows 10 / Windows 11 Domain-Joined Workstation  
- **Directory Service:** Active Directory Domain Services (AD DS)  
- **Ticketing Platform:** Jira Service Management  
---

## Onboarding Process

#### Step 1: Create User in Active Directory

1. First, boot up the **Windows Server 2022 Domain Controller** using adminstrative credentials.
2. Open **Server Manager** and navigate to the **Tools** section > **Active Directory Users and Computers**.
3. Navigate to the **_USERS** organizational unit > **Finance Department** OU where the new user works in.
4. Right-click on the **Finance OU** > New > User.
5. Enter the user details for the new user:
    - **First Name:** Pat
    - **Last Name:** Bryant
    - **User Logon Name:** pbyrant
6. Click **"Next** to proceed with user creation.

![UserCreation](/images/UserCreation.png)

#### Step 2: Set Initial Temporary Password

1. Next, you will be asked to set an initial password for the onboarded user.
2. Make sure that the **"User must change password at next logon"** checkbox is enabled in order for the new user to create their own password after successful logon.
3. Enter a temporary password that the user can use to establish their new password.
    - **Example:** Friday13
4. Click **Next** > **Finish** to complete the user creation process.

![TemporaryPassword](/images/TemporaryPassword.png)

#### Step 3: Assign User to Security Groups

1. Right-click on the new user object > Select **Properties**.
2. Click **Add** within the **Member Of** tab.
3. Enter the name of the security group that the user need to be in to access the network drive. With this user's problem, they need to be added to the **HR Department Security Group**.
4. Click **Apply** and **OK** to update the group membership.

This grants access to department-specific resources such as shared drives.

#### Step 4 - Refresh User Group Policies

To apply the changes immediately, the following command was executed on the user's workstation:

```gpupdate /force```

This refreshed the user's group memberships and applied updated permissions.

---

## Customer Communication

Once the account setup progress was completed, the user was notified through the ticket that their account has been created and to attempt to log in with the account on their workstation with the provided username and temporary password.

![OnboardingResponse](/images/OnboardingResponse.png)

---

## Verification

The user successfully logged into their workstation using the provided credentials.

The following confirmations were made:

- Login to the domain was successful
- Password change prompt appeared at first login
- Access to the Finance network drive was verified