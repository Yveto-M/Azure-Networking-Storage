# Azure-Networking-Storage
This project demonstrates secure deployment and monitoring of Azure storage using best practices. It includes virtual network creation, NSG rules, private endpoint configuration, backup encryption, and secure access testing via SAS tokens and Azure Storage Explorer.


## ✅ Step 1: Create a Virtual Network (VNet)

* Created a virtual network with two subnets:

  * `Database` subnet: `10.0.0.0/27`, marked as private, with service endpoint `Microsoft.Storage` enabled.
  * `Web` subnet: `10.0.1.0/27` with default settings.

<img width="738" alt="creating vnet" src="https://github.com/user-attachments/assets/15599483-e866-4b2a-a0dc-db6b09568c20" />

---

## ✅ Step 2: Deploy a Network Security Group (NSG)

* Created a Network Security Group and associated it with the `Web` subnet.
* Configured inbound rules:

  * Allowed HTTPS (port 443).
  * Denied all other inbound traffic not explicitly permitted.
  * Verified default rules: `AllowVnetInBound`, `AllowAzureLoadBalancerInBound`, `DenyAllInBound`.

<img width="486" alt="nsg creation" src="https://github.com/user-attachments/assets/18f5f2a6-3be8-4d07-8adc-542f73f2b486" />

---

## ✅ Step 3: Create and Configure a Storage Account

* Deployed a Storage Account with replication set to **LRS**.
* Disabled public access and created a **private endpoint** scoped to the `Database` subnet.
* Enabled **Microsoft-managed encryption** to protect stored data.

<img width="789" alt="storage account" src="https://github.com/user-attachments/assets/a59e915b-04b6-4599-99fa-79931c2af76e" />

---

## ✅ Step 4: Query Logs in Azure Monitor

* Opened Log Analytics Workspace and ran the following KQL query:

  ```kql
  Perf
  | where ObjectName == "Processor" and CounterName == "% Processor Time"
  | summarize Avg_CPU = avg(CounterValue) by bin(TimeGenerated, 5m)
  ```

* Visualized average CPU usage over 5-minute intervals using built-in charting tools.


## ✅ Step 5: Secure Backup and Recovery

* Navigated to **Recovery Services Vault** settings.
* Verified:

  * **TLS** was enabled for secure backup traffic.
  * **Encryption settings** were properly configured in the Vault’s properties.

<img width="630" alt="storage backup" src="https://github.com/user-attachments/assets/4462c7cd-42c8-4431-a8cf-d22af11c321e" />

---

## ✅ Step 6: Test Access and Encryption

### 🔹 A. Generate SAS Token

* Opened the storage account, went to **Security + Networking → Shared Access Signature**.
* Configured permissions and generated a valid SAS URI for Blob access.

<img width="607" alt="rr SAS" src="https://github.com/user-attachments/assets/db04b178-3dc8-47a4-b413-4640f9afb53f" />

### 🔹 B. Use Azure Storage Explorer

* Opened Storage Explorer, connected using the generated **SAS URI**.
* Successfully uploaded `sample.txt` and confirmed the upload via the interface.

<img width="993" alt="storage x-initial" src="https://github.com/user-attachments/assets/00f44b7f-6252-4d0d-9210-eb08f4ec4e0a" />

<img width="651" alt="storage x-final" src="https://github.com/user-attachments/assets/0c6c5b4a-d716-4bca-ac0f-62491ac45369" />

✅ Summary

This project covered:

Azure networking & subnet isolation
Traffic filtering via NSGs
Storage secured via private endpoints
Monitoring with KQL and Log Analytics
Backup encryption validation
Access testing using both CLI and GUI tools

🧰 Tools Used
Azure Portal
Network Security Groups
Azure Storage (Private Endpoints + SAS)
Azure Monitor / Log Analytics
Recovery Services Vault
AzCopy
Azure Storage Explorer

👤 Author
Yveto Meus
M.S. Cybersecurity | U.S. Navy Veteran 



