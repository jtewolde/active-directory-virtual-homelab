# User Account Management (Help Desk Operations)

---

## Objective:

This section demostrates common **IT Help Desk** and **Desktop Support tasks** performed using **Active Directory Users and Computers**. These actions represent real-world user management scenarios such as password resets, account lockouts, and disabling accounts for "terminated" employees.

## Overview:

In an enterprise environment, IT support staff are responsible for managing user accounts throughout their lifecycle. This includes:
- Resetting passwords
- Unlocking locked accounts
- Disabling and re-enabling accounts
- Moving users between Organizational Units(OUs)
- Verifying access on client machines

All actions in this section are performed using **Active Directory Users and Computers (ADUC)** on the **Domain Controller.**

### Step 1: Open Active Directory Users and Computers(ADUC)
1. Log into the **Domain Controller**
2. Open **Server Manager** > **Tools** > **Active Directory Users and Computers**
3. Expand on your domain by clicking on the arrow next to it > Navigate to the **_USERS** organizational unit.

### Ticket 1: Resetting User's Password

**Scenario**: A user puts in a ticket, saying that they have forgotten their password and cannot log into their workstation.

**Steps to Resolve Ticket:**
1. In **ADUC**, find the user's account by either locating it in the **_USERS** OU or right click on the OU and navigate to the **"Find"** option where you can quickly find the user by typing in their username.
2. Once you found the user, right-click on the user object and select **Reset Password**.
3. A window will pop up to create a temporary password.
4. Check the **"User must change password at next logon"** to make it so that the user will have to create a new password.
    - The option will be greyed out if the password is set to never expire.
5. Click **OK** to finalize changes

![ResetPassword](./screen-recordings/ResetPassword.gif)


**Verification:**
- Boot up the Windows Client VM
- Sign in with the same user you made changes for with the temporary password set previously.
- If successful, the user will be prompted to set a new password upon login.



![ResetPasswordClient](./screen-recordings/ResetPassword2.gif)

## Ticket 2: Unlocking a Locked Account

**Scenario:** A user puts in a ticket, saying that they entered the wrong password too many times and have been locked out of their account.


**Steps to Resolve Ticket:**
1. In **ADUC**, find the user's account by either locating it in the **_USERS** OU using the **Find** option to quickly look them up as mentioned in the previous ticket
2. Once you found the locked out account, right click on the user object > Select **"Properties"**.
3. The **Properties** window will appear > click on the **Account** tab.
4. Check the following box: **Unlock Account. This account is currently locked out on this Active Directory Domain Controller**
5. Click **Apply > OK**.

**Verification:**
- Boot up the **Windows Client VM**
- Choose an example account to lock out by entering the wrong password for 3 to 5 times until a message says the account is locked out.
- On the **Window Server VM**, follow the steps above to unlock the account.
- If successful, the user's account will be unlocked and they will be able to sign in.

![UnlockAccount](./images/Unlock3.png)
![UnlockAccount](./screen-recordings/Unlock1.gif)
![UnlockAccount](./screen-recordings/Unlock2.gif)

## Ticket 3: Disabling an User's Account

**Scenario:** An employee has left the company and their access must be revoked immediately for off-boarding.

**Steps to Resolve Ticket:**
1. Right-Click on the user's account that you want to disable.
2. Select **Disable Account** option.
3. The account's icon will now have a downward arrow.

![DisableAccount](./screen-recordings/Disable1.gif)

**Verification:**
- First, disable the account that you want to test on the **Client VM**.
- Verify that when you try to sign in to the account, the account is disabled.
![DisableAccount](./images/Disable2.png)


## Ticket 4: Re-enable an User's Account

**Scenario:** A previously disabled user returns from leave is rehired.

**Steps to Resolve:**
1. Right-Click on the user's account that you want to enable.
2. Select **Enable Account** option.
3. The account's icon will no longer have a downward arrow.

**Verification:**
- Follow the steps above on the **Domain Controller** and attempt to sign in back with the same account to successfully log in.


## Ticket 5: Moving a User to a Different Organizational Unit

**Scenairo:** A user changes departments and needs new policies applied.

**Steps to Resolve:**
1. Find the desired user account that you want to change departments/organizational units.
2. Drag the user to the appropriate organizational unit or right-click on the user and select **"Move"**. A window will appear that has all of the organizational units in the domain > Select the OU that this appropriate for the user.
3. Confirm the move.

![Move1](./screen-recordings/Move1.gif)

## Conclusion:

This section demonstrates real-world Active Directory account management tasks commonly handled by IT Help Desk and Desktop Support professionals. By completing these actions, you have validated your ability to manage users securely and efficiently within an enterprise Windows domain environment.

These skills are foundational for roles such as:

- **IT Help Desk Technician**

- **Desktop Support Specialist**

- **Junior Systems Administrator**

➡️ Continue to: **[Group Policy Object (GPO) Setup](./07_group_policy_setup.md)**

