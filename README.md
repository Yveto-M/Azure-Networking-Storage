# Azure-Networking-Storage
This project demonstrates secure deployment and monitoring of Azure storage using best practices. It includes virtual network creation, NSG rules, private endpoint configuration, backup encryption, and secure access testing via SAS tokens and Azure Storage Explorer.

Perfect — here’s your **Project 2 rewritten entirely in the same concise, structured format as Steps 5 and 6**, with a focus on action + outcome. This is ideal for a GitHub README, a portfolio writeup, or progress documentation:

---

## ✅ Step 1: Create a Virtual Network (VNet)

* Created a virtual network with two subnets:

  * `Database` subnet: `10.0.0.0/27`, marked as private, with service endpoint `Microsoft.Storage` enabled.
  * `Web` subnet: `10.0.1.0/27` with default settings.

---

## ✅ Step 2: Deploy a Network Security Group (NSG)

* Created a Network Security Group and associated it with the `Web` subnet.
* Configured inbound rules:

  * Allowed HTTPS (port 443).
  * Denied all other inbound traffic not explicitly permitted.
  * Verified default rules: `AllowVnetInBound`, `AllowAzureLoadBalancerInBound`, `DenyAllInBound`.

---

## ✅ Step 3: Create and Configure a Storage Account

* Deployed a Storage Account with replication set to **LRS**.
* Disabled public access and created a **private endpoint** scoped to the `Database` subnet.
* Enabled **Microsoft-managed encryption** to protect stored data.

---

## ✅ Step 4: Query Logs in Azure Monitor

* Opened Log Analytics Workspace and ran the following KQL query:

  ```kql
  Perf
  | where ObjectName == "Processor" and CounterName == "% Processor Time"
  | summarize Avg_CPU = avg(CounterValue) by bin(TimeGenerated, 5m)
  ```

* Visualized average CPU usage over 5-minute intervals using built-in charting tools.

---

## ✅ Step 5: Secure Backup and Recovery

* Navigated to **Recovery Services Vault** settings.
* Verified:

  * **TLS** was enabled for secure backup traffic.
  * **Encryption settings** were properly configured in the Vault’s properties.

---

## ✅ Step 6: Test Access and Encryption

### 🔹 A. Generate SAS Token

* Opened the storage account, went to **Security + Networking → Shared Access Signature**.
* Configured permissions and generated a valid SAS URI for Blob access.

### 🔹 B. Use Azure Storage Explorer

* Opened Storage Explorer, connected using the generated **SAS URI**.
* Successfully uploaded `sample.txt` and confirmed the upload via the interface.

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



