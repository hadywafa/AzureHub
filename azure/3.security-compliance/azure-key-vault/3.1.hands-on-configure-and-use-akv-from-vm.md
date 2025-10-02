# 🔐 **Project: Configure and Use Azure Key Vault from a VM**

## 📌 **Project Scenario**

You’re deploying a **web app on a VM** that needs to connect to a **database**.
Instead of hardcoding the DB password, you store it in **Azure Key Vault**.

The VM will use a **Managed Identity** to securely fetch the secret.
No credentials in code, no secrets in environment variables. 🚀

---

## 📌 **Step-by-Step Implementation**

### 🔹 Step 1: Create a Resource Group

```bash
az group create --name rg-kv-demo --location eastus
```

---

### 🔹 Step 2: Create Key Vault

```bash
az keyvault create \
  --name kvdemoproject123 \
  --resource-group rg-kv-demo \
  --location eastus \
  --sku standard \
  --enable-rbac-authorization true
```

---

### 🔹 Step 3: Add a Secret

```bash
az keyvault secret set \
  --vault-name kvdemoproject123 \
  --name "DbPassword" \
  --value "SuperSecretP@ss123"
```

---

### 🔹 Step 4: Create a VM (with System-Assigned Identity)

```bash
az vm create \
  --name myVmDemo \
  --resource-group rg-kv-demo \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys \
  --assign-identity
```

This enables a **system-assigned managed identity** automatically.

---

### 🔹 Step 5: Give VM Access to Key Vault

```bash
# Assign "Key Vault Secrets User" role to the VM’s managed identity
VM_PRINCIPAL_ID=$(az vm show -g rg-kv-demo -n myVmDemo --query identity.principalId -o tsv)

az role assignment create \
  --assignee $VM_PRINCIPAL_ID \
  --role "Key Vault Secrets User" \
  --scope $(az keyvault show -n kvdemoproject123 --query id -o tsv)
```

---

### 🔹 Step 6: Test from Inside the VM

SSH into the VM:

```bash
az vm ssh -g rg-kv-demo -n myVmDemo
```

Install Azure CLI + login using **Managed Identity**:

```bash
# Enable MSI-based authentication
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
az login --identity
```

Fetch the secret:

```bash
az keyvault secret show \
  --vault-name kvdemoproject123 \
  --name DbPassword \
  --query value -o tsv
```

👉 Expected output:

```ini
SuperSecretP@ss123
```

---

## 📌 **(Optional) Access Secrets in Code**

### Example: Python Script (on VM)

```python
from azure.identity import DefaultAzureCredential
from azure.keyvault.secrets import SecretClient

KVUri = "https://kvdemoproject123.vault.azure.net/"
credential = DefaultAzureCredential()
client = SecretClient(vault_url=KVUri, credential=credential)

secret = client.get_secret("DbPassword")
print("Fetched secret:", secret.value)
```

✅ Runs without credentials → uses VM Managed Identity.

---

## 📌 **Security Notes**

- **Never store secrets in VM files or code.** Always fetch dynamically.
- Use **RBAC** roles like _Key Vault Secrets User_ (read-only).
- Use **Access Policies** if RBAC is disabled.
- Rotate secrets automatically in Key Vault when possible.

---

## 🏁 **TL;DR Project Flow**

1. Create **Key Vault** → store secret.
2. Create **VM with Managed Identity**.
3. Assign **Key Vault Secrets User role** to VM.
4. From VM → authenticate with **MSI** → fetch secret.
5. Use in app/script (Python, .NET, Node, etc.).
