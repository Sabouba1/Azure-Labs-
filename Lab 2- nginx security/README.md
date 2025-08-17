# Lab 2 – Azure VM with Nginx & Security Posture Review

## 📌 Overview
In this lab, I deployed a **Linux Virtual Machine (Ubuntu)** in Microsoft Azure, installed **Nginx** as a web server, and reviewed the security posture of the environment using **Azure Advisor** and **Defender for Cloud**.  

This demonstrates how to:
- Deploy a basic workload (Nginx) on Azure.
- Open access through **Network Security Groups (NSGs)**.
- Monitor usage and logs with **Azure Monitor + Log Analytics**.
- Evaluate security and reliability posture with Azure’s built-in tools.

---

## 🏗️ Architecture
+-------------------------+

| Azure VNet |

| (App-VNet) |

+-------------------------+

|

+-----------------+

| App-Subnet |

+-----------------+

|

+-------------------------+

| VM: app-vm (Ubuntu) |

| - Nginx Web Server |

| - Public IP + NSG |

+-------------------------+

|

Accessible via browser:

http://<Public_IP>
---

## 🔧 Steps Performed

### 1. Resource Group
- Created resource group `rg-nginx-lab`.

### 2. Virtual Machine Deployment
- VM name: `app-vm`
- Size: `Standard_B1s`
- OS: Ubuntu Server 22.04 LTS
- Authentication: Password
- NSG inbound rules:
  - SSH (22) → Allowed from My IP
  - HTTP (80) → Allowed from All

### 3. Install Nginx
Connected to the VM with SSH:
```bash
ssh azureuser@<PublicIP>
sudo apt update
sudo apt install nginx -y
      Verified the service:  systemctl status nginx
Tested by browsing: http://<PublicIP>
Result → Nginx Welcome Page ✅
```
### 4. Monitoring & Logging

Created Log Analytics Workspace (law-monitoring-lab).

Enabled VM Insights → confirmed Heartbeat + performance metrics in Log Analytics.

Ran KQL queries to view CPU, memory, and disk metrics.

### 5. Security Posture

Azure Advisor:

Cost: 0%

Performance: 100%

Reliability: 75% (1 high impact recommendation)

Operational Excellence: 100%

Defender for Cloud:

Recommendations: enable backup, enable alert notifications, encrypt disks, enable Defender plans.

Secure Score updated with findings.
### 📸 Screenshots

✅ Nginx welcome page in browser

✅ Log Analytics Heartbeat query result

✅ Azure Advisor dashboard

✅ Defender for Cloud recommendations

### 🎯 Key Learnings

Deploying and securing an Azure VM.

Publishing a web server with Nginx.

Using NSGs to restrict/allow traffic.

Centralizing monitoring with Log Analytics & KQL queries.

Reviewing posture with Advisor & Defender.

### 🧹 Cleanup

To avoid costs:

Delete the resource group:

Go to Resource Groups → rg-nginx-lab

Click Delete resource group



