# Azure 3-Tier Infrastructure Lab

This project demonstrates the deployment of a basic **3-tier architecture** on Microsoft Azure using Virtual Machines, networking, and Azure Files.  
It is designed as a **hands-on lab** to practice Azure services, understand networking, and build a professional project for a cloud portfolio.  

---

## 📌 Lab Overview

The lab includes:  
- **Web Tier (WEB-SRV)** → Hosts a sample website.  
- **App Tier (APP-SRV)** → Acts as the middle layer, accessing both web and data tiers.  
- **Data Tier (DATA-SRV)** → Stores data using an attached private data disk.  
- **Azure File Share** → Shared storage mounted on both APP-SRV and DATA-SRV.  
- **Network Security Group (App-NSG)** → Allows only secure access:
  - RDP from my public IP
  - HTTP open to everyone
- **Virtual Network (App-VNet)** → With a subnet (App-Subnet) where all VMs are deployed.  
- **Region Pairing** → The environment is deployed in one region with redundancy best practices in mind.  

---

## ⚙️ Deployment Steps

1. **Create Resource Group**
   - `rg-3tier-lab` in your chosen region.  

2. **Deploy Virtual Network + Subnet**
   - VNet: `App-VNet` (192.168.20.0/24)  
   - Subnet: `App-Subnet`  

3. **Deploy Virtual Machines**
   - `WEB-SRV`: With Public IP for web hosting  
   - `APP-SRV`: Connected to subnet, public IP for RDP initially  
   - `DATA-SRV`: No Public IP (private only), with 256 TiB data disk  

4. **Configure NSG (App-NSG)**
   - Allow **RDP (3389)** only from my public IP  
   - Allow **HTTP (80)** from any source  

5. **Azure File Share**
   - Create storage account + file share  
   - Mount the share on both APP-SRV and DATA-SRV  

6. **Publish Web Application**
   - Deploy a simple IIS/Apache website on `WEB-SRV`  
   - Verify access using APP-SRV Public IP in a browser  

7. **Private Connectivity**
   - Remove the public IP from DATA-SRV  
   - Access DATA-SRV using its private IP from inside the VNet  

---

## 📖 Key Learnings

- How to deploy and secure **Azure Virtual Machines**  
- Using **NSGs** to control access  
- Attaching and configuring **data disks** in Azure  
- Setting up **Azure File Shares** for cross-VM storage  
- Understanding **private vs. public IP connectivity**  
- Designing a **3-tier infrastructure** in the cloud  

---

