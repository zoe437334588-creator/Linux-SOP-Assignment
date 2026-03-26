# Standard Operating Procedure: Setup of Virtual Linux Server for Web Application Testing

## 1. Purpose
This SOP describes the steps to create and configure a virtual Linux server for web application testing. [cite_start]It ensures the setup is consistent, stable, and ready for testing tasks. [cite: 5, 21]

## 2. Scope
[cite_start]This document is for students, system administrators, and IT staff who need to deploy a Linux virtual machine for testing web applications. [cite: 7, 23]

[cite_start]**This SOP includes:** [cite: 27]
* VM creation
* Linux installation
* Network setup
* Web service configuration
* Basic testing

## 3. Environment & Requirements

### [cite_start]Hardware Requirements [cite: 39]
* **CPU**: Minimum 2 cores
* **RAM**: Minimum 4 GB
* **Disk**: Minimum 20 GB

### Software Requirements
* [cite_start]**Virtualization**: VMware Workstation / VirtualBox [cite: 49]
* [cite_start]**OS**: Ubuntu Server 22.04 LTS [cite: 56]
* [cite_start]**ISO Image**: Ubuntu Server ISO [cite: 62]

## [cite_start]4. Definitions [cite: 12]
| Term | Meaning |
| :--- | :--- |
| **VM** | Virtual Machine |
| **SSH** | Secure Shell (remote access tool) |
| **Apache** | Web server software |
| **IP Address** | Network identifier |

## [cite_start]5. Accountability Matrix [cite: 10, 34]
| Task | Responsible | Approval |
| :--- | :--- | :--- |
| VM Creation | System Administrator | IT Manager |
| OS Installation | System Administrator | IT Manager |
| Network Setup | Network Admin | IT Manager |
| Web Server Setup | Dev/Test Engineer | IT Ops Manager |
| Testing | QA Team | QA Manager |

## [cite_start]6. Procedure Steps [cite: 14, 35]

### [cite_start]Step 1: Create Virtual Machine [cite: 47]
1. [cite_start]Open VMware or VirtualBox. [cite: 49]
2. [cite_start]Click **Create New VM**. [cite: 50]
3. [cite_start]Set VM name: `web-test-server`. [cite: 55]
4. [cite_start]Select OS: **Linux → Ubuntu (64-bit)**. [cite: 56]
5. [cite_start]Allocate resources: [cite: 57]
    * CPU: 2 cores
    * RAM: 4 GB
    * Disk: 20 GB (dynamically allocated)
6. [cite_start]Attach Ubuntu ISO file. [cite: 61]

### [cite_start]Step 2: Install Linux OS [cite: 60]
1. [cite_start]Start the VM. [cite: 65]
2. [cite_start]Select **Install Ubuntu Server**. [cite: 66]
3. [cite_start]Choose language: **English**. [cite: 66]
4. [cite_start]Configure: [cite: 67]
    * Hostname: `webtest01`
    * Username & password
5. [cite_start]Select **OpenSSH Server** during installation. [cite: 66]
6. Complete installation and reboot.

### [cite_start]Step 3: Configure Network [cite: 68]
1. Check IP address:
   ```bash
   ip a
   Test network connection:
Bash
Copy code
ping google.com
3. (Optional) Set static IP by editing Netplan:
Bash
Copy code
sudo nano /etc/netplan/*.yaml
4. Apply changes:
Bash
Copy code
sudo netplan apply
Step 4: Install Web Server
1. Update system: 
￼
View source details. Opens side panel.
Bash
Copy code
sudo apt update && sudo apt upgrade -y
2. Install Apache: 
￼
View source details. Opens side panel.
Bash
Copy code
sudo apt install apache2 -y
3. Start and enable service:
Bash
Copy code
sudo systemctl start apache2
Bash
Copy code
sudo systemctl enable
 apache2
Step 5: Configure Firewall 
￼
View source details. Opens side panel.
1. Allow HTTP traffic: 
￼
View source details. Opens side panel.
Bash
Copy code
sudo ufw allow 80
2. Enable firewall and check status:
Bash
Copy code
sudo ufw enable
Bash
Copy code
sudo ufw status
Step 6: Deploy Test Web Application
1. Go to web directory:
Bash
Copy code
cd
 /var/www/html
2. Create test page:
Bash
Copy code
sudo nano index.html
3. Add content: <h1>Web Test Server Working</h1>.
4. Save and exit.
Step 7: Verification & Testing 
￼
View source details. Opens side panel.
1. Open browser and enter server IP address. 
￼
View source details. Opens side panel.
2. Confirm the page displays correctly. 
￼
View source details. Opens side panel.
3. Test SSH connection:
Bash
Copy code
ssh username@server-ip
7. Post-Setup Checklist 
￼
View source details. Opens side panel.
• [ ] VM is running
• [ ] Linux installed successfully
• [ ] Network is working
• [ ] Apache is running
• [ ] Web page is accessible
• [ ] SSH access works
8. Security Notes 
￼
View source details. Opens side panel.
• Use strong passwords.
• Disable root login (recommended).
• Keep system updated regularly.
9. Revision History 
￼
View source details. Opens side panel.
Version
Date
Description
1.0
2026-03-26
Initial version
Export to Sheets
Copy table
