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
- 