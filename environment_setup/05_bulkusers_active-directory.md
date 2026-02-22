# Creating Bulk Active Directory Users with PowerShell

## Objective:

In this section, I will demostrate how to create hundreds of sample users using a PowerShell Script. This simulates a realistic enterprise environment where IT Support and System Admins must manage large number of accounts, organizational units, and department structures.

## Overview:

Manually creating dozens or hundreds of users in **Active Directory** will be very time-consuming and unrealistic for enterprise workflows. **PowerShell** solves this by allowing adminstrators to automate user creation with repeatable, customizable scripts.

For this lab, I used a bulk-import PowerShell Script from **Josh Madakor's Active Directory Home Lab Tutorial**. Below, I have linked his YouTube video of this active directory homelab and the downloadable link for the PowerShell Script and users.txt for creating bulk AD Users:
- **YouTube Link:** https://www.youtube.com/watch?v=MHsI8hJmggI&t=1921s
- **PowerShell Script Download**: https://github.com/joshmadakor1/AD_PS/archive/refs/heads/master.zip

## Step 1: Download the User Creation Script on Domain Controller

To create bulk users, you need to download **Josh Madakor's PowerShell Script** and user list.

1. Open **Server Manager** > Click **Configure this local server** or **Local Server** on the left side bar.
2. In the **Properties** section of your domain, look for the *IE Enhanced Security Configuration* option on the right side. By default, it should be turned 'ON'.
3. Click on the 'ON' Switch and a window should pop up to turn off the security configuration for both users and admins.
4. Turn off **IE ESC** for both users and admins temporarily to allow downloads.

![PowerShell](./screen-recordings/PS1.gif)

5. Open **Internet Explorer** or **Microsoft Edge** > Copy and paste the **PowerShell Script Download Link** mentioned above or here to download the folder:
    - https://github.com/joshmadakor1/AD_PS/archive/refs/heads/master.zip
6. The folder named, **"AD_PS-master"** will be downloaded and appear either on your **Desktop** or **Downloads** folder in File Explorer.
7. Extract the downloaded ZIP folder to access the contents inside.
8. Inside the **AD_PS-master** folder, there will be 4 files inside, we are only going to interact with two of them. One being the **"names.txt"** file and the PowerShell File, **"1_CREATE_USERS"**.

![PowerShell](./images/PS2.png)

Inside of the **"names.txt"** file, you will find hundreds of sample names that will be used to create sample user accounts in Active Directory. You can add some other names to the text file that you are familar with to create accounts as well.

## Step 2: Open PowerShell ISE as Adminstrator
Next, the **1_CREATE-USERS** script needs to be opened and inside of **PowerShell ISE**.

1. Go to the search bar on the Task Bar and type in **"Windows PowerShell ISE"** inside.
2. Right-click on "Windows PowerShell ISE" > Select **"Run as Adminstrator"**.
3. Once PowerShell has opened, click on the **Open Script** icon above the file name. The icon will look like a opened folder.
4. Navigate to the extracted **"AD_PS-master"** folder and select the **1_CREATE-USERS** file > Click "Open".

## Summary of 1_CREATE-USERS Script

The **1_CREATE_USERS.ps1** PowerShell script automates the creation of bulk Active Directory users for lab or enterprise simulation. It reads first and last names from a **names.txt** file, generates usernames in the format first initial + last name, and creates each account inside a new OU called **_USERS**. Each user is assigned a default password (**Password1** by default), set so the password never expires, and enabled automatically. The script also handles generating secure strings for the password and provides on-screen status messages while creating each account.

![CreateUsers](./images/PS3.png)

## Step 3: Allow Script Execution
By default, PowerShell will block this script due to execution policy restrictions. In order to resolve this:

1. In the PowerShell command line at the bottom, type the following:
```bash
     Set-ExecutionPolicy Unrestricted
```
2. Press **Enter**.
3. A security prompt will appear on the screen, click **"Yes to all"** to proceed.

Now, this authorizes PowerShell to run the script to create users in Active Directory

## Step 4: Run the Script
1. Click the **Run** button(Green Play Icon) in **PowerShell ISE**.
2. PowerShell will start to generate users automatically, you should see cyan text saying, "creating user: (user)".

![PowerShell](./images/PS5.png)

3. After the script is done running, check if the users were created in Active Directory under the **_USERS** OU.
    - Open **Server Manager** > **Tools** > **Active Directory Users and Computers**
4. Navigate to the **organizational unit** created by the script(**_USERS**)
5. If successful, you should see hundreds of newly created accounts were added to Active Directory!

![NewUsers](./screen-recordings/PS6.gif)

This wraps up the process of generating bulk Active Directory users using PowerShell. With dozens of realistic accounts now added to your domain, your homelab now mirrors a real enterprise environment—complete with an organizational structure and user base to manage. 

The next phase is to bring a Windows client machine into the environment so you can begin testing authentication, Group Policy, and user login behavior across the domain.

➡️ Continue to: [Creating the Windows Client VM & Joining it to the Domain](./06_windows-client-setup.md)