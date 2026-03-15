# Ticket 001 - Password Reset for Locked User Account

---

This document demonstrates the process of resolving a common IT help desk issue involving a locked user account and password reset within an Active Directory environment. The ticket was created and tracked using Jira Service Management to simulate a real-world help desk workflow. The steps below outline the troubleshooting process performed on a Windows Server 2022 domain controller to unlock the user account, reset the password, and restore the user's access to their workstation.

## Ticket Information:
- **Ticket Key:** SUP-5
- **Request Type:** Account Access/Password Reset
- **Priority**: Medium
- **Status:** Waiting for Support
- **Reported by:** csutton@lab.local
- **Assigned Techincian:** Joseph Tewolde


## Ticket Creation

A support request was submitted through **Jira Service Management** after a user reported being unable to log into their workstation. The issue description indicated that the system displayed a message stating that the user was locked out of their account on their workstation and needs to be unlocked and their password reset as well.

The ticket was categorized as an **Account Access Issue** and assigned to the IT support queue for investigation and resolution.

## Ticket Assignment and Status Updates

After reviewing the support request, the ticket was assigned to the IT support technician responsible for account management.

1. The ticket was **assigned to Joseph Tewolde** for investigation.
2. The ticket status was updated from **Waiting for Support → In Progress**.
3. Initial investigation notes were added to the ticket to document the troubleshooting process that will be taken to resolve issue.

Updating the ticket status helps maintain visibility for both the IT team and the user requesting

![InternalNotes](/images/InternalNotes.png)

## Issue Description

The user reported that they could not log into their domain-joined workstation due to forgetting their password. Multiple login attempts resulted in the account becoming locked based on the **Account Lockout Policy** configured through Group Policy.

This issue prevented the user from accessing their workstation and required administrative intervention to restore access.

![PracticeTicket](/images/PracticeTicket1.png)

![LockedAccount](/images/LockedAccount.png)
---

## Lab Environment:

All of the tickets are resolved in the following environment that I demostrated how to create and configure earlier in the repo.

- **Domain Controller:** Windows Server 2022  
- **Client Machine:** Windows 10 / Windows 11 Domain-Joined Workstation  
- **Directory Service:** Active Directory Domain Services (AD DS)  
- **Ticketing Platform:** Jira Service Management  
- **User Location:** USERS Organizational Unit (OU)

---

## Troubleshooting and Resolving Steps

#### Step 1 - Access Active Directory Users and Computers

1. First, boot up the **Windows Server 2022 Domain Controller** using adminstrative credentials.
2. Open **Server Manager** and navigate to the **Tools** section > **Active Directory Users and Computers**.
3. Locate the affected user account by right-clicking on the **_USERS** OU and selecting **"Find"**.

#### Step 2 - Verify Account Lockout Status
1. Enter the name of the user account and right-click on the user object > Select **Reset Password**.
2. Ensure that the **"User must change password at next logon"** checkbox is enabled.
3. Check to see that the **Account Lockout Status** of the user is **locked out.**
4. Enter a temporary password that the user can use to establish their new password.
    - **Example:** Friday13
5. Click **OK** to unlock the user's account and reset their password.

![UnlockTicket](/screen-recordings/UnlockTicket.gif)

This ensured the user could regain access while maintaining security standards.

---

## Customer Communication

After resetting the user's password and unlocking the account with following troubleshooting steps, the user was notified through the Jira ticket to test their login.

![ReplyCustomer](/images/ReplyCustomer.png)

---

## Verification

After completing the password reset, the user attempted to log into their workstation using the temporary password.

The following results confirmed successful resolution:

- The user successfully authenticated with the domain.
- The system prompted the user to **create a new password upon login**.
- The user confirmed full access to their workstation.

![ResetPassword](/screen-recordings/ResetPassword2.gif)

---

## Ticket Resolution

After the user confirmed successful access to their workstation, the ticket was updated to reflect that the issue had been resolved.

The user account had been successfully unlocked and the password was reset through **Active Directory Users and Computers**. The user was able to log in using the temporary password and was prompted to create a new secure password upon login, ensuring compliance with the domain's password policy.

The ticket status was updated from **In Progress → Resolved** within Jira Service Management.

---

## Ticket Closure

Once the user confirmed that they were able to log into their workstation without further issues, the ticket was closed.

Final notes were added to the ticket documenting the troubleshooting steps and resolution. The ticket status was updated to **Closed** to indicate that no further action was required.

---

## Conclusion

This ticket demonstrates a common IT help desk scenario involving a user account lockout and password reset within an Active Directory environment. Using administrative tools on a Windows Server 2022 domain controller, the technician was able to quickly identify the issue, unlock the user account, and reset the password to restore access.

The issue was documented and tracked through **Jira Service Management**, simulating a real-world help desk workflow that included ticket creation, assignment, investigation, customer communication, verification, and final resolution.

This process highlights key IT support skills such as Active Directory account management, troubleshooting authentication issues, maintaining ticket documentation, and communicating effectively with end users tonsure successful resolution of technical problems.**