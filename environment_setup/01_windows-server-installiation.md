# Windows Server 2022 Virtual Machine Installiation

## Objective:
In this markdown file, I will show how I set up my base Windows 2022 Server virtual machine in VirtualBox to serve as the foundation for this homelab.

### Overview:
Windows Server 2022 will serve as the Domain Controller that has Active Directory Installed on it. It will have two network interfaces.
- One for connecting to the Internet
- Another for communicating within the internal network


### Step 1 - Install Necessary Software
First, you will have to download the following software needed to conduct this virtual homelab on your desktop.

- [Oracle VirtualBox & Extension Pack](https://www.virtualbox.org/wiki/Downloads)
- [Windows Server 2022 Standard (Desktop Experience) ISO](https://go.microsoft.com/fwlink/p/?linkid=2195686&clcid=0x409&culture=en-us&country=us)
- [Windows 11 Enterprise ISO](https://go.microsoft.com/fwlink/p/?linkid=2195682&clcid=0x409&culture=en-us&country=us)


## Step 2 - Create and Configure Domain Controller Virtual Machine

1. Open VirtualBox > Click **'New'**
2. Put the following settings:
    - **Name**: DC
    - **ISO Image**: Enter the ISO File for Windows Server 2022
    - Click **Skip Unattended Installation**
    - **RAM**: 2048MB or 4096MB depending on your host machine
    - **Processors**: 1 or 2
    - **Hard Disk**: Select 'Create a virtual hard disk' > Set to 25GB or more
3. Click 'Finish'

![Screenshot](/setup/images/Setup1.png)
![Screenshot](/setup/images/Setup2.png)
![Screenshot](/setup/images/Setup3.png)

### Configure Settings for DC Virutal Machine: 
- Click on **'Settings'** > **General Section > Advanced Tab**:
    - Set both **Shared Clipboard and Drag n' Drop** > **Bi-directional**
- Navigate to the **Network Section**:
    - Set Adapter 1 > **NAT** (by default)
    - Set Adapter 2 > **Internal Network**
- Click **'OK'** to confirm settings

![Screenshot](/setup/images/Setup4.png)
![Screenshot](/setup/images/Setup5.png)
![Screenshot](/setup/images/Setup6.png)

### Start Windows Server 2022 Virtual Machine
- Click on the newly created Server 2022 VM and boot it up.
- Proceed through the installation by selecting options like Language to Install, Time, etc
- For the selection of the Operating System > Select **Windows Server 2022 Standard Desktop Experience**
- Select **Custom Install** for the type of installation.
- Wait for the installation to fully complete. It should take a few minutes.
- Once the installation is complete, set a secure password for the Administrator account.
![Screenshot](/setup/images/Setup7.png)

### Step 3 - Configure Network Adapters
- First, toggle the 'CTRL + ALT + DELETE' action on your VM to unlock it by going to **'Input > Keyboard'** option on your VM and select **Insert CTRL + ALT + Del** to unlock the login in form.
![Screenshot](/setup/images/Setup8.png)
- Enter the password that you assigned previously for the local adminstrator account to sign in!

## ✅ Summary
At this stage, the Windows Server 2022 Virtual Machine is successfully installed and operational within VirtualBox.  
This VM will serve as the **Domain Controller (DC)** for the Active Directory lab.

Next, we’ll move on to **configuring the network interfaces** to ensure proper communication between the domain controller and client machines.

➡️ Continue to: [Network Configuration](./02-network-configuration.md)
