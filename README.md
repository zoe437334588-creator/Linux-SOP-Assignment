# Standard Operating Procedure: Setup of Virtual Linux Server for Web Application Testing

## 1. Purpose
This SOP explains how to create and configure a Red Hat Linux virtual server for web application testing. It helps ensure the system is set up correctly and ready for use.

## 2. Scope
This document is for students and IT administrators who need to deploy a Red Hat Enterprise Linux (RHEL) virtual machine for testing web applications.

## 3. System Requirements

**Hardware**
- CPU: 2 cores
- RAM: 4 GB
- Disk: 20 GB

**Software**
- Virtualization: VMware / VirtualBox
- OS: Red Hat Enterprise Linux 9 (or Rocky Linux / AlmaLinux)
- ISO file for installation

## 4. Definitions

| Term   | Description           |
| ------ | --------------------- |
| VM     | Virtual Machine       |
| SSH    | Remote login protocol |
| HTTP   | Web service protocol  |
| Apache | Web server software   |


## 5. Responsibilities

| Task               | Responsible          |
| ------------------ | -------------------- |
| VM Setup           | System Administrator |
| OS Installation    | System Administrator |
| Network Setup      | Network Admin        |
| Web Server Install | Developer / Tester   |
| Testing            | QA Team              |

## 6. Procedure

**Step 1: Create Virtual Machine**

**1.** Open VMware or VirtualBox

**2.** Click Create New Virtual Machine

**3.** Set:

- Name: rhel-web-test

- OS Type: Linux (RHEL 9)

**4.** Allocate:

- CPU: 2 cores

- RAM: 4 GB

**5.** Create disk (20 GB)

**6.** Attach RHEL ISO

### Step 2: Install Red Hat Linux

**1.** Start VM and select Install RHEL 9

**2.** Configure:

- Language: English
  
- Installation Destination: automatic
  
**3.** Set:
  
- Hostname: webtest-rhel
  
- Root password
  
- Create user account
  
**4.** Enable network during installation
  
**5.** Complete installation and reboot

### Step 3: Configure Network
1. Check IP address:
   ```bash
   ip a

2. Test connection:
   ```bash
   ping -c 4 google.com

3. Set hostname if needed:
   ```bash
   sudo hostnamectl set-hostname webtest-rhel

### Step 4: Install Required Packages
1. Update system:
   ```bash
   sudo dnf update -y
   
2. Install Apache (httpd):
   ```bash
   sudo dnf install httpd -y
   
3. Install tools (optional but useful):
   ```bash
   sudo dnf install wget curl git -y

### Step 5: Start and Enable Web Service
1. Start Apache:
   ```bash
   sudo systemctl start httpd

2. Enable auto start:
   ```bash
   sudo systemctl enable httpd

3. Check status:
   ```bash
   systemctl status httpd

### Step 6: Configure Firewall
1. Allow HTTP service:
   ```bash
   sudo firewall-cmd --permanent --add-service=http

2. Reload firewall:
   ```bash
   sudo firewall-cmd --reload

3. Verify firewall settings:
   ```bash
   firewall-cmd --list-all

### Step 7: Configure SELinux (Important for RHEL)
1. Check SELinux status:
   ```bash
   sestatus

2. If needed, allow web content:
   ```bash
   sudo setsebool -P httpd_can_network_connect 1

### Step 8: Deploy Test Web Page
1. Go to web directory:
   ```bash
   cd /var/www/html

2. Create test page:
   ```bash
   sudo nano index.html

3. Add content:
   ```html
   <h1>RHEL Web Server is Working</h1>

### Step 9: Testing
1. Open a web browser on your host machine.
2. Enter the server's IP address in the address bar.
3. Confirm the test web page displays correctly.
4. Test SSH remote connection:
   ```bash
   ssh username@server-ip

## 7. Verification Checklist
- [x] VM created successfully
- [x] RHEL 9 installed and updated
- [x] Network connectivity confirmed
- [x] Apache (httpd) service is active
- [x] Firewall configured for Port 80
- [x] Web page accessible via browser

## 8. Notes
* **Package Manager**: Use `dnf` instead of `apt` on RHEL systems.
* **Security**: Always check **SELinux** settings if the web page fails to load.
* **Best Practice**: Always run `sudo dnf update` before installing new software.

## 9. Revision History
| Version | Date | Author | Description |
| :--- | :--- | :--- | :--- |
| **1.0** | **2026-03-26** | **Jie Zhuang** | **Initial Release of Document** |
