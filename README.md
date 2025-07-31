# iac-azure-vm-storage-stack

### 🧭 Overview

This repository provisions a secure and reusable infrastructure on Azure using Bicep and JSON parameterization. The deployment includes:

- Storage Account with SMB File Share  
- Virtual Network and Subnet  
- Network Interface with Public IP and NSG  
- Windows Virtual Machine with RDP and HTTP access

---

### 📂 Files Included

| File                  | Description                                             |
|-----------------------|---------------------------------------------------------|
| `main.bicep`          | Core infrastructure template using Bicep syntax         |
| `parameters.json`     | Configurable input values for deployment customization  |

---

### 🛠 Parameters Defined in `main.bicep`

| Parameter           | Description                                  | Example                        |
|---------------------|----------------------------------------------|--------------------------------|
| `location`          | Azure region to deploy resources             | `"eastus"`                     |
| `storageAccountName`| Name of the Storage Account                  | `"smbstorageaccount123"`       |
| `fileShareName`     | SMB file share name                          | `"qsfileshare"`                |
| `vmName`            | Name for the Virtual Machine                 | `"VM1"`                        |
| `adminUsername`     | Admin login for VM                           | `"localadmin"`                 |
| `adminPassword`     | Secure password for VM login                 | `"Password12345"` (secure)     |
| `vnetName`          | Name of the Virtual Network                  | `"VM1-vnet"`                   |
| `subnetName`        | Name of the Subnet                           | `"VM1-subnet"`                 |
| `nicName`           | Name of the Network Interface                | `"VM1-nic"`                    |

> 💡 _Use Key Vault or pipeline secrets for `adminPassword` in production._

---

### 🚀 Deployment Steps

1. **Log into Azure**
   ```bash
   az login
   ```

2. **Deploy the resources**
   ```bash
   az deployment group create \
     --resource-group <your-resource-group> \
     --template-file main.bicep \
     --parameters @parameters.json
   ```

---

### 🔐 Security & Network Setup

- **NSG Rules**: Allows inbound RDP (3389) and HTTP (80)
- **Public IP**: Static assignment for VM access
- **Private IP**: Dynamically assigned within `10.0.0.0/24`
- **File Share Quota**: 100 GB enabled for SMB

---

### 📌 Outputs

| Output Name     | Description                        |
|------------------|------------------------------------|
| `fileShareId`    | Full ID of the deployed file share |
| `vmNameOut`      | Name of the created virtual machine|

---

### 🧱 Suggestions for Improvement
