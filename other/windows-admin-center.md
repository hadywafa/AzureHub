# 🖥 Windows Admin Center (WAC) in Azure VMs

## 📌 1. Official Definition

> **Windows Admin Center (WAC)** is a browser-based, modern Windows Server management tool that lets you **securely manage your Azure Windows VMs without RDP**, directly from the Azure Portal.

It’s basically **"Server Manager 2.0"** — but with a clean web UI, better integration, and no need to open **port 3389** to the internet.

---

## 🔄 2. AWS Perspective (Mapping Table)

| Azure Concept                   | AWS Rough Equivalent                        | Key Difference                               |
| ------------------------------- | ------------------------------------------- | -------------------------------------------- |
| Windows Admin Center            | AWS Systems Manager (SSM) + Session Manager | WAC is GUI-based, SSM is mostly CLI          |
| Azure VM Extension for WAC      | SSM Agent on EC2                            | WAC gives direct Windows admin GUI           |
| Azure AD Authentication for WAC | IAM Identity Federation to SSM              | WAC integrates Azure RBAC for access control |

**Quick Take:**
In AWS, you'd use **SSM Session Manager** to connect without RDP — but you’d still be CLI-driven. In Azure, WAC gives you **clicky-click control** over almost everything in the OS.

---

## 🛠 3. What You Can Do with WAC in Azure

Once enabled, you can:

- 📂 **Manage files** (upload/download without RDP)
- 🖥 **View live performance metrics** (CPU, RAM, network)
- ⚙ **Install/remove roles and features** (e.g., IIS, Hyper-V)
- 🛡 **Manage firewall rules**
- 🔄 **Start/stop/restart services**
- 🧰 **Run PowerShell in-browser**
- 🗄 **Manage disks and storage pools**
- 📅 **Install Windows Updates**
- 🧭 **Edit registry directly**

---

## ⚙ 4. How WAC Works in Azure

```mermaid
flowchart LR
    User[You in Azure Portal Browser] -->|HTTPS Secure Proxy| Azure[Azure Control Plane]
    Azure -->|Tunnel| Gateway[WAC Gateway Extension on VM]
    Gateway --> OS[Windows Server Management APIs]
```

- **Gateway Extension**: Installed automatically when you enable WAC
- **Secure Tunnel**: Uses Azure’s control plane to proxy connections — no need to open inbound ports
- **Authentication**: Azure AD identity + RBAC roles

---

## 🚀 5. How to Enable WAC

### 📌 During VM Creation

1. In **Azure Portal → Create VM → Management Tab**
2. **Enable Windows Admin Center** toggle
3. Azure deploys the WAC extension with the VM

---

### 📌 On an Existing VM

1. Go to your **VM → Windows Admin Center (Preview)**
2. Click **Set up Windows Admin Center**
3. Wait for the **extension** to be installed
4. Click **Connect** → WAC web UI opens in a new browser tab

**PowerShell Method**:

```powershell
Set-AzVMExtension `
  -ResourceGroupName "myRG" `
  -VMName "myVM" `
  -Name "WindowsAdminCenter" `
  -Publisher "Microsoft.WindowsAdminCenter" `
  -ExtensionType "WindowsAdminCenter" `
  -TypeHandlerVersion "0.1"
```

---

## 🖱 6. Using WAC — Example: Install IIS on a VM Without RDP

1. Open **VM → Windows Admin Center → Connect**
2. Go to **Roles & Features**
3. Search for **Web Server (IIS)** → check box → Install
4. Monitor status in WAC → IIS ready 🎉

No RDP. No manual login. Just browser magic.

---

## 🔐 7. Security Benefits

- ✅ No public **RDP port 3389** needed
- ✅ Azure **RBAC** controls who can access WAC
- ✅ Uses **Azure AD** authentication
- ✅ All traffic over **HTTPS** via Azure control plane

---

## 📏 8. Best Practices

- **Disable public RDP** if WAC meets your needs
- Assign **least privilege** via custom Azure roles
- Keep the **WAC extension updated**
- Combine with **Azure Bastion** for occasional full desktop access
- Use **Private Endpoints** for even tighter security

---

## 🧠 9. Exam Tips (AZ-104)

- WAC is **browser-based** and can be enabled at VM creation or later via **extension**
- Works **only** on **Windows Server** or Windows-based Azure VMs
- Removes need for **public RDP**
- Uses **Azure AD authentication** and respects RBAC

---

## 🆚 10. WAC vs Azure Bastion vs RDP

| Feature             | WAC                       | Azure Bastion              | RDP                           |
| ------------------- | ------------------------- | -------------------------- | ----------------------------- |
| Protocol            | HTTPS                     | HTML5 over TLS             | RDP (TCP 3389)                |
| UI Type             | Web GUI (Server Admin)    | Full desktop session       | Full desktop session          |
| Inbound Port Needed | None                      | None                       | TCP 3389                      |
| OS Support          | Windows only              | Windows & Linux            | Windows only (native)         |
| Ideal Use           | Admin tasks, service mgmt | Full OS access via browser | Full OS access via RDP client |

---

> ✅ **Memory Hook for You (AWS Expert)**:  
> Think of WAC as **"AWS SSM Session Manager but with full Windows GUI"**, deployed as an **Azure VM Extension**, and using **Azure AD RBAC** instead of IAM policies.
