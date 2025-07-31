# iac-azure-vm-storage-stack

## 📘 README: Azure Bicep Deployment — VM, Storage, and Networking

### 🧭 Overview

This deployment uses a structured Bicep template (`main.bicep`) to provision a full-stack Azure environment. Configuration is externally driven via a JSON parameter file to support customization and reuse across environments.

Provisioned resources include:

- 🔐 Virtual Machine with public IP, NSG, and secured admin credentials  
- 📁 Storage Account with an SMB-enabled File Share  
- 🌐 Virtual Network, Subnet, and Network Interface with dynamic private IP  
- 📤 Public IP and inbound NSG rules (RDP + HTTP)

---

### 📂 File Structure

| File             | Purpose                                                    |
|------------------|------------------------------------------------------------|
| `main.bicep`     | Defines the entire infrastructure as code using Bicep      |
| `parameters.json`| Supplies values for parameters used in the Bicep file      |

---

### 🛠 Parameters (Defined in `parameters.json`)

The infrastructure is outlined in `main.bicep`, while the following values must be provided via the parameter file:

| Parameter           | Description                                |
|---------------------|--------------------------------------------|
| `location`          | Azure region for resource deployment       |
| `storageAccountName`| Unique name for the Storage Account        |
| `fileShareName`     | SMB File Share name                        |
| `vmName`            | Name of the virtual machine                |
| `adminUsername`     | VM administrator username                  |
| `adminPassword`     | VM administrator password (**secure**)     |
| `vnetName`          | Virtual Network name                       |
| `subnetName`        | Subnet name within the VNet                |
| `nicName`           | Network Interface name                     |

> 💡 `adminPassword` is marked `@secure()` in Bicep. For production deployments, consider referencing Azure Key Vault for secrets instead of hardcoding values.

---

### 🚀 Deployment Instructions

1. **Log into Azure**  
   ```bash
   az login
   ```

2. **Deploy the stack**  
   ```bash
   az deployment group create \
     --resource-group <your-resource-group> \
     --template-file main.bicep \
     --parameters @parameters.json
   ```

---

### 🌐 Networking & Security Details

- **NSG Rules**:  
  - Port 3389 (RDP) — enabled  
  - Port 80 (HTTP) — enabled  

- **IP Configuration**:  
  - Public IP (Static)  
  - Private IP (Dynamic via subnet)

---

### 📤 Outputs

| Output Name     | Description                                |
|------------------|--------------------------------------------|
| `fileShareId`    | Resource ID of the deployed file share     |
| `vmNameOut`      | Name of the created virtual machine        |


