# Azure-Networking-Storage
This project demonstrates secure deployment and monitoring of Azure storage using best practices. It includes virtual network creation, NSG rules, private endpoint configuration, backup encryption, and secure access testing via SAS tokens and Azure Storage Explorer.


````markdown
# 🔐 Azure Networking & Storage – Project 2 (AZ-104 Lab)

This project demonstrates secure deployment and monitoring of Azure storage using best practices. It includes virtual network creation, NSG rules, private endpoint configuration, backup encryption, and secure access testing via SAS tokens and AzCopy/Azure Storage Explorer.

---

## 📁 Step-by-Step Implementation

---

### **1. Create a Virtual Network (VNet)**

- Created a virtual network with two subnets:
  - **Database Subnet**: `10.0.0.0/27`
    - Marked as private
    - Enabled Service Endpoint for `Microsoft.Storage`
  - **Web Subnet**: `10.0.1.0/27`

📸 _Screenshot: VNet and Subnet Configuration_  
→ **Paste here**

---

### **2. Deploy a Network Security Group (NSG)**

- Attached NSG to the **Web** subnet.
- Added the following inbound security rules:
  - ✅ Allow HTTPS traffic (Port 443)
  - ❌ Block all other inbound traffic
  - System rules: `AllowVnetInBound`, `AllowAzureLoadBalancerInBound`, `DenyAllInBound`

📸 _Screenshot: NSG Rules Applied to Web Subnet_  
→ **Paste here**

---

### **3. Create and Configure a Storage Account**

- Created a **StorageV2** account.
- Set replication to **LRS**.
- **Disabled public access**.
- Created a **Private Endpoint** within the `Database` subnet.
- Used **Microsoft-managed keys** for encryption.

📸 _Screenshot: Storage Account Configuration with Private Endpoint_  
→ **Paste here**

---

### **4. Query Logs in Azure Monitor (Log Analytics)**

- Navigated to Log Analytics Workspace.
- Ran the following Kusto query to monitor CPU usage:

```kql
Perf
| where ObjectName == "Processor" and CounterName == "% Processor Time"
| summarize Avg_CPU = avg(CounterValue) by bin(TimeGenerated, 5m)
````

* Visualized the data as a time-series chart.

📸 *Screenshot: KQL Output & Visualization in Log Analytics*
→ **Paste here**

---

### **5. Secure Backup and Recovery**

* Opened **Recovery Services Vault**.
* Verified that:

  * ✅ TLS encryption was enabled for backup data.
  * ✅ Microsoft-managed key encryption was in use under **Properties**.

📸 *Screenshot: Backup Vault Showing TLS & Encryption Settings*
→ **Paste here**

---

### **6. Test Access and Encryption**

#### A. Generate SAS Token

* Went to:
  `Storage Account → Security + Networking → Shared Access Signature`
* Set permissions: `Read`, `Add`, `Write`.
* Generated a **SAS URI**.

📸 *Screenshot: SAS Token Configuration*
→ **Paste here**

---

#### B. Upload File Using AzCopy (CLI)

* Opened PowerShell and ran:

```powershell
azcopy copy "$env:USERPROFILE\Desktop\sample.txt" "https://<youraccount>.blob.core.windows.net/<container>/sample.txt?<SAS-Token>"
```

* Verified successful upload via terminal output.

📸 *Screenshot: AzCopy Upload Confirmation*
→ **Paste here**

---

#### C. Upload File Using Azure Storage Explorer (GUI)

* Connected to the blob container using **SAS URI**.
* Uploaded `sample.txt` successfully via GUI.
* Confirmed upload visually in the interface.

📸 *Screenshot: File in Azure Storage Explorer*
→ **Paste here**

---

## ✅ Summary

This project covered:

* Azure networking & subnet isolation
* Traffic filtering via NSGs
* Storage secured via private endpoints
* Monitoring with KQL and Log Analytics
* Backup encryption validation
* Access testing using both CLI and GUI tools

---

## 🧰 Tools Used

* Azure Portal
* Network Security Groups
* Azure Storage (Private Endpoints + SAS)
* Azure Monitor / Log Analytics
* Recovery Services Vault
* AzCopy
* Azure Storage Explorer

---

## 👤 Author

**Yveto Meus**
*M.S. Cybersecurity | U.S. Navy Veteran 

