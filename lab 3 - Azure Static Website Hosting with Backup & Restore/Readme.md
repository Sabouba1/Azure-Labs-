# Azure Static Website Hosting with Backup & Restore (Lab)

## 📌 Overview
In this lab, I deployed a **Static Website** on **Azure Blob Storage** to host my **Image Metadata Analyzer** project.  
Additionally, I implemented a simple **Backup & Restore** mechanism using **Blob Snapshots** to recover files in case of accidental deletion or modification.

---

## 🎯 Objectives
- Create a Storage Account (Standard LRS).
- Enable the Static Website feature.
- Upload project files to the `$web` container.
- Access the website via the public endpoint.
- Create a Snapshot as a backup of the files.
- Simulate file changes and restore the original state from the Snapshot.

---

## 🛠️ Steps

### 1. Create Resource Group
- Create a new Resource Group:  
  **`Lab_3rg`**

### 2. Create Storage Account
- Storage account name: **sablab3** (must be globally unique).  
- Region: **West Europe**.  
- Performance: **Standard**.  
- Redundancy: **Locally-redundant storage (LRS)**.  
- Primary service: **Azure Blob Storage**.  

### 3. Enable Static Website
- In the Storage Account → **Static website** → set to **Enabled**.  
- Index document name: `index.html`.  
- Error document path: `404.html` (optional).  
- Save → copy the **Primary endpoint**, e.g.:  
  `https://sablab3.z6.web.core.windows.net/`

### 4. Upload Files
- Go to **Containers** → open **$web**.  
- Upload files:
  - `index.html`
  - `404.html` (optional).  
- Open the Primary endpoint link → your site is live ✅  

### 5. Backup (Blob Snapshot)
- Inside the `$web` container → select `index.html`.  
- From (…) menu → **Create Snapshot**.  
- A snapshot is now saved with a timestamp.  

### 6. Test Restore
- Modify `index.html` and upload a new version (e.g., “Oops! changed”).  
- Open the site → you’ll see the change.  
- Go back to `index.html` → **Snapshots** → select the older version.  
- Click **Promote** (Restore).  
- Refresh the site → it is back to the original state ✅  

---

## 📸 Screenshots
<img width="1788" height="903" alt="Screenshot 2025-08-19 021838" src="https://github.com/user-attachments/assets/a046a714-41ef-4789-b383-3988b2444bd1" />
<img width="1872" height="893" alt="Screenshot 2025-08-19 021903" src="https://github.com/user-attachments/assets/8fb3e9c8-82fa-4de1-8e81-cafdb631ba58" />
<img width="1860" height="989" alt="Screenshot 2025-08-19 021940" src="https://github.com/user-attachments/assets/eb645412-67d8-45a9-ad7d-090b252debe9" />
i edited it so i can get my snapshot i took before (:
 <img width="1731" height="776" alt="Screenshot 2025-08-19 022221" src="https://github.com/user-attachments/assets/a5e93d9c-4edd-45cb-86ef-53b8faa726ca" />
<img width="1201" height="741" alt="Screenshot 2025-08-19 022346" src="https://github.com/user-attachments/assets/78540b66-2c3c-44ac-ba83-9bebee3e2d91" />
its back again! <img width="1585" height="969" alt="Screenshot 2025-08-19 022351" src="https://github.com/user-attachments/assets/f6c5ca65-0ce7-4e8b-aa4b-dcc09949a4c1" />


---

## 🏗️ Architecture Diagram
```plaintext
User Browser  --->  Azure Blob Storage (Static Website)
                        |
                        |--- $web Container
                                |--- index.html
                                |--- 404.html
                                |
                                +--- Snapshots (Backup)
