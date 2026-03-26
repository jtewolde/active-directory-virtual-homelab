# Ticket 002 - User Unable to Access Department Network Drive

---

This document demonstrates the process of troubleshooting and resolving a network drive access issue within an Active Directory environment. The ticket was created and tracked using Jira Service Management to simulate a real-world help desk workflow. The steps below outline how the issue was investigated and resolved on a Windows Server 2022 domain controller by verifying network drive permissions and correcting the user's access rights.

## Ticket Information:
- **Ticket Key:** SUP-6
- **Request Type:** Network Drive Issue
- **Priority**: Medium
- **Status:** Waiting for Support
- **Reported by:** jwaddle@lab.local
- **Assigned Techincian:** Joseph Tewolde

## Ticket Creation:

A support request was submitted through **Jira Service Management** after a user reported being unable to access their department’s shared network drive. The user stated that the drive appears on their workstation but displays an **"Access Denied"** message when attempting to open it.

The ticket was categorized as a **Network Access Issue** and assigned to the IT support queue for investigation and resolution.

## Ticket Assignment and Status Updates:

After reviewing the ticket details, the request was assigned to the IT support technician responsible for user account and network resource management.

1. The ticket was **assigned to Joseph Tewolde**.
2. The ticket status was updated from **Waiting for Support → In Progress**.
3. Investigation notes were added to document the troubleshooting process.

Updating ticket statuses ensures visibility for both IT staff and the user requesting support.

![NetworkTicket](/images/NetworkTicket.png)

## Issue Description

The user reported that they were unable to open their department's network drive from their workstation. The drive was mapped on the user's system but displayed an **Access Denied** error when accessed.

Because the drive was visible but inaccessible, the issue was suspected to be related to **Active Directory permissions or group membership** rather than a network connectivity issue.

![NetTicket](/images/NetTicket.png)

![NetworkError](/images/NetworkDriveError.png)

---

## Lab Environment:

All of the tickets are resolved in the following environment that I demostrated how to create and configure earlier in the repo.

- **Domain Controller:** Windows Server 2022  
- **Client Machine:** Windows 10 / Windows 11 Domain-Joined Workstation  
- **Directory Service:** Active Directory Domain Services (AD DS)  
- **Ticketing Platform:** Jira Service Management  
- **User Location:** USERS Organizational Unit (OU)

---

## Techincal Investigation Notes:

**Initial Response:** Reviewed the support ticket in queue and confirmed the user was attempting to access a department shared drive.

**Investigation:** Connected into the user's workstation using **Remote Desktop Protocol(RDP)** to verify the issue. Confirmed that the network drive is visible but displays an **Access Denied** error when trying to open the folder. Checked what groups the user is apart of and discovered that the user isn't apart of the **HR Security Group** that grants access to **HR Department Network Drive**.

**Action Plan:** Add the user to the appropriate **Active Directory security group** responsible for granting access to the shared network drive.

![AddedHRGroup](/images/HRGroupAdded.png)

---

## Troubleshooting and Resolving Steps:

#### Step 1 - Verify Shared Folder Permissions

1. First, boot up the **Windows Server 2022 Domain Controller** using adminstrative credentials.
2. Open **File Explorer** > Navigate to the shared folder hosting the **HR Network Drive**.
3. Right-click on the shared folder and select **Properties**.
4. Check the **Security permissions** and confirm that access was granted through an Active Directory **HR Security Group**.

![SecurityGroup](/images/SecurityGroup.png)

#### Step 2 - Verify User Group Membership
1. Open **Active Directory Users and Computers** on the Domain Controller.
2. Locate the affected user account by right-clicking on the **_USERS** OU and selecting **"Find"**.
3. Right-click on the user account and select **Properties**.
4. Navigate to the **Members Of** tab and see if the user is in **HR Security Group**.

In this case, the user is not in the security group.

![GroupMembership](/images/GroupMembership.png)

#### Step 3 - Add User to the Correct Security Group

1. Click **Add** within the **Member Of** tab.
2. Enter the name of the security group that the user need to be in to access the network drive. With this user's problem, they need to be added to the **HR Department Security Group**.
3. Click **Apply** and **OK** to update group membership.

![AddUserHRDrive](/images/AddHRNetworkDrive.png)

This granted the user the required permissions to access the shared network drive.

#### Step 4 - Refresh User Group Policies

To apply the changes immediately, the following command was executed on the user's workstation:

```gpupdate /force```

This refreshed the user's group memberships and applied updated permissions.

---

## Customer Communication

After updating the user's permissions, a response was provided through the Jira ticket to notify the user to try again with accessing the **HR Department Network Drive** from their end.

![ReplyCustomerMessage](/images/ReplyCustomer2.png)

---

## Verification

The user attempted to access the network drive afer the permissions were updated.

The following results confirmed successful resolution:

- The user was able to open the shared network drive.
- All folders and files within the department share were accessible.
- No further access errors were reported.

![NetworkdriveSuccess](/screen-recordings/NetworkDriveSuccess.gif)

---

## Ticket Resolution

Once the user confirmed successful access to the shared network drive, the issue was marked as resolved in Jira Service Management.

The ticket status was updated from **In Progress → Resolved**.

---

## Ticket Closure

After confirming that the user was able to access the network drive without issues, the ticket was closed.

Final documentation was added to the ticket describing the troubleshooting process and resolution steps.

The ticket status was updated to **Closed** to indicate that the issue had been fully resolved.

---

## Conclusion

This ticket demonstrates a common IT support issue involving network drive access within an Active Directory environment. By reviewing shared folder permissions and verifying the user's group membership, the issue was quickly identified and resolved.

The troubleshooting process involved checking Active Directory security groups, updating user permissions, and verifying that the changes were applied successfully on the user's workstation.

The issue was documented and tracked using **Jira Service Management**, demonstrating the full help desk ticket lifecycle including ticket creation, assignment, investigation, customer communication, verification, and final resolution.

This scenario highlights important IT support skills such as **Active Directory administration, file share permission management, troubleshooting network access issues, and maintaining clear technical documentation.**