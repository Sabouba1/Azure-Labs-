# 🔐 Lab 04 – Azure Role-Based Access Control (RBAC)

> Implementing secure, group-based access control in Azure using Microsoft Entra ID and scoped RBAC assignments.

This lab demonstrates how to configure Azure Role-Based Access Control (RBAC) following enterprise security best practices.  
The focus is on **least privilege**, **group-based authorization**, and **resource-level scoping**.

---

## 🏗 Lab Architecture

### 🔹 Identity Layer – Microsoft Entra ID

#### 👤 Users
- `Joseph Price` – Senior Admin
- `Isabel Garcia` – Junior Admin
- `Dylan Williams` – Service Desk Engineer

#### 👥 Security Groups
- `Senior Admins`
- `Junior Admins`
- `Service Desk`

---

### 🔹 Authorization Layer – Azure RBAC

| Component | Configuration |
|------------|---------------|
| Resource Group | `AZ500Lab01` |
| Role Assigned | `Virtual Machine Contributor` |
| Scope | Resource Group |
| Assigned To | `Service Desk` (Security Group) |

---

## 🎯 Lab Objectives

- Create users in Microsoft Entra ID  
- Create security groups  
- Add users to groups  
- Assign RBAC role to a group


- Validate effective permissions  
- Enforce least-privilege design  

---
---

# 🧪 Exercise 1 – Azure Portal (Senior Admin)

## 🎯 Objective
Create a user and security group using Microsoft Entra ID via Azure Portal.

---

## Step 1 – Create User

Navigate to:

Microsoft Entra ID → Users → New User


Configure:

- Display Name: `Joseph Price`
- User Principal Name: `Joseph@yourtenant.onmicrosoft.com`
- Auto-generate password: Enabled

Create the user.

---

## Step 2 – Create Security Group

Navigate to:

Microsoft Entra ID → Groups → New Group


Configure:

- Group Type: `Security`
- Group Name: `Senior Admins`
- Membership Type: `Assigned`

Add:
- Owner → `Joseph Price`
- Member → `Joseph Price`

Create the group.
---

# 🧪 Exercise 2 – PowerShell (Junior Admin)

## 🎯 Objective
Create a user and group using Azure PowerShell.

Open:
Azure Cloud Shell → PowerShell
---

## Step 1 – Create User

```powershell
$pw = ConvertTo-SecureString "Pa55w.rd1234" -AsPlainText -Force

New-AzADUser `
  -DisplayName "Isabel Garcia" `
  -UserPrincipalName "Isabel@yourtenant.onmicrosoft.com" `
  -Password $pw `
  -MailNickname "Isabel"
```
Step 2 – Create Group
```powershell

$group = New-AzADGroup `
  -DisplayName "Junior Admins" `
  -MailNickname "JuniorAdmins"
```
Step 3 – Add User to Group

```
Add-AzADGroupMember `
  -TargetGroupObjectId $group.Id `
  -MemberUserPrincipalName "Isabel@yourtenant.onmicrosoft.com"
```
Verify Membership
```
Get-AzADGroupMember -GroupObjectId $group.Id
```
---

# 🧪 Exercise 3 – Azure CLI (Service Desk)

## 🎯 Objective
Create a user and group using Azure CLI.

Switch Cloud Shell to:
---

## Step 1 – Create User

```
az ad user create \
  --display-name "Dylan Williams" \
  --user-principal-name Dylan@yourtenant.onmicrosoft.com \
  --password "Pa55w.rd1234"
```
## Step 2 – Create Group
```
az ad group create \
  --display-name "Service Desk" \
  --mail-nickname "ServiceDesk"
```
## Step 3 – Add User to Group
```
USER_ID=$(az ad user show \
  --id Dylan@yourtenant.onmicrosoft.com \
  --query id -o tsv)

az ad group member add \
  --group "Service Desk" \
  --member-id $USER_ID
```
Verify Membership
```
az ad group member list --group "Service Desk" -o table
```
---
# 🧪 Exercise 4 – RBAC Role Assignment

## 🎯 Objective
Assign a scoped RBAC role to a security group and validate access.

---

## Step 1 – Create Resource Group

Navigate to:
Azure Portal → Resource Groups → Create
Configure:

- Name: `AZ500Lab01`
- Region: `East US`

---

## Step 2 – Assign RBAC Role

Navigate to:

AZ500Lab01 → Access Control (IAM) → Add Role Assignment
Configure:

- Role: `Virtual Machine Contributor`
- Assign Access To: `User, group, or service principal`
- Member: `Service Desk`
- Scope: `This resource`

Review and assign.

---

## Step 3 – Validate Access

Navigate to:

AZ500Lab01 → Access Control (IAM) → Check Access


Validate:

- `Dylan Williams` → Has `Virtual Machine Contributor`
- Other users → Do NOT have access at this scope
