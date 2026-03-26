1. Purpose

This SOP describes the steps to create and configure a virtual Linux server for web application testing. It ensures the setup is consistent, stable, and ready for testing tasks.

2. Scope

This document is for students, system administrators, and IT staff who need to deploy a Linux virtual machine for testing web applications.

This SOP includes:

VM creation
Linux installation
Network setup
Web service configuration
Basic testing
3. Environment & Requirements
Hardware Requirements
CPU: Minimum 2 cores
RAM: Minimum 4 GB
Disk: Minimum 20 GB
Software Requirements
Virtualization: VMware Workstation / VirtualBox
OS: Ubuntu Server 22.04 LTS
ISO Image: Ubuntu Server ISO
4. Definitions
Term	Meaning
VM	Virtual Machine
SSH	Secure Shell (remote access tool)
Apache	Web server software
IP Address	Network identifier
5. Accountability Matrix
Task	Responsible
VM Creation	System Administrator
OS Installation	System Administrator
Network Setup	Network Admin
Web Server Setup	Dev/Test Engineer
Testing	QA Team
6. Procedure Steps
Step 1: Create Virtual Machine
Open VMware or VirtualBox
Click Create New VM
Set VM name: web-test-server
Select OS: Linux → Ubuntu (64-bit)
Allocate resources:
CPU: 2 cores
RAM: 4 GB
Create virtual disk (20 GB, dynamically allocated)
Attach Ubuntu ISO file
Step 2: Install Linux OS
Start the VM
Select Install Ubuntu Server
Choose language: English
Configure:
Hostname: webtest01
Username & password
Select OpenSSH Server during installation
Complete installation and reboot
Step 3: Configure Network

Check IP address:

ip a

Test network connection:

ping google.com

(Optional) Set static IP by editing:

sudo nano /etc/netplan/*.yaml

Apply changes:

sudo netplan apply
Step 4: Install Web Server

Update system:

sudo apt update && sudo apt upgrade -y

Install Apache:

sudo apt install apache2 -y

Start service:

sudo systemctl start apache2

Enable auto start:

sudo systemctl enable apache2
Step 5: Configure Firewall

Allow HTTP traffic:

sudo ufw allow 80

Enable firewall:

sudo ufw enable

Check status:

sudo ufw status
Step 6: Deploy Test Web Application

Go to web directory:

cd /var/www/html

Create test page:

sudo nano index.html

Add simple HTML content:

<h1>Web Test Server Working</h1>
Save and exit
Step 7: Verification & Testing
Open browser
Enter server IP address
Confirm the page displays correctly

Test SSH connection:

ssh username@server-ip
7. Post-Setup Checklist
 VM is running
 Linux installed successfully
 Network is working
 Apache is running
 Web page is accessible
 SSH access works
8. Security Notes
Use strong passwords
Disable root login (recommended)
Keep system updated regularly
9. Revision History
Version	Date	Description
1.0	2026-03-26	Initial version


