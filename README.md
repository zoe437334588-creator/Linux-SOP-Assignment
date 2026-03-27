# Standard Operating Procedure: Setup of Virtual Linux Server for Web Application Testing

## 1. Title
**SOP Name:** Virtual Linux Server Deployment and Web Configuration  
**Document ID:** MITT-NSA-2026-01  
**Category:** Systems Administration / Testing Environment  

## 2. Approval Table
| Role | Name | Date | Signature |
| :--- | :--- | :--- | :--- |
| **Author** | Jie Zhuang | 2026-03-26 | ____________ |
| **Reviewer** | IT Instructor | 2026-03-27 | ____________ |
| **Approver** | QA Lead | 2026-03-28 | ____________ |

## 3. Purpose
The purpose of this document is to provide a standardized, repeatable process for setting up a Red Hat Enterprise Linux (RHEL) virtual machine. This ensures that web application testing environments are consistent and reduce configuration errors.

## 4. Scope/Objectives
- **Scope:** This procedure covers VM creation, OS installation, network configuration, and web server setup.
- **Objectives:**
  - Deploy a functional RHEL 9 server.
  - Successfully host a test web page.
  - Ensure remote access via SSH for testing.

## 5. Accountability Matrix (RACI)

| Task | Responsible (R) | Accountable (A) | Consulted (C) | Informed (I) |
| :--- | :--- | :--- | :--- | :--- |
| **VM Hardware Setup** | System Admin | IT Manager | Hardware Lead | QA Team |
| **OS & Network Config** | System Admin | IT Manager | - | Security Team |
| **Web Service Config** | System Admin | IT Manager | Dev Team | QA Team |
| **Security (Firewall)** | Network Admin | Security Lead | System Admin | - |

## 6. Steps

**Step 1: Create Virtual Machine**

1. Open VMware or VirtualBox

2. Click Create New Virtual Machine

3. Set:

   - Name: rhel-web-test

   - OS Type: Linux (RHEL 9)

4. Allocate:

   - CPU: 2 cores

   - RAM: 4 GB

5. Create disk (20 GB)

6. Attach RHEL ISO

### Step 2: Install Red Hat Linux

1. Start VM and select Install RHEL 9

2. Configure:

   - Language: English
  
   - Installation Destination: automatic
  
3. Set:
  
   - Hostname: webtest-rhel
  
   - Root password
  
   - Create user account
  
4. Enable network during installation
  
5. Complete installation and reboot

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





## 9. Reversion History

| Version | Date       | Author      | Description                          |
| :------ | :--------- | :---------- | :----------------------------------- |
| 0.1     | 2026-03-26 | Jie Zhuang  | Initial Draft (Internal Review)      |
| 0.2     | 2026-03-27 | Jie Zhuang  | Added RACI Matrix and Screenshots    |
| 1.0     | 2026-03-27 | Jie Zhuang  | Final Version for Assignment Submission |

