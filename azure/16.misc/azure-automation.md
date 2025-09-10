# 🤖 Azure Automation Service

## 📌 1. What is Azure Automation?

👉 **Azure Automation** is a **cloud-based automation service** that helps you:

- Run **scripts (PowerShell / Python)** in Azure or on-premises.
- Automate **repetitive tasks** (VM start/stop, patching, cleanup).
- Enforce **configuration management** (like Puppet/Chef/Ansible).
- Orchestrate workflows across Azure + on-prem + external services.

💡 Think of it as **“Azure’s Swiss Army Knife for IT automation”** 🔧.

---

## 📌 2. Why Use It?

- 🕒 **Save time** → Automate manual, repeatable tasks.
- 🛡️ **Ensure compliance** → Standardize configurations.
- 💸 **Save money** → Auto shut down idle VMs.
- 🌍 **Hybrid automation** → Works in Azure **and** on-prem.

---

## 📌 3. Key Components

| Component                       | What it Does                                    | Example                                 |
| ------------------------------- | ----------------------------------------------- | --------------------------------------- |
| **Runbooks**                    | Scripts (PowerShell, Python, Graphical) you run | VM start/stop schedule                  |
| **Automation Account**          | Container for runbooks, configs, credentials    | Like a workspace                        |
| **Hybrid Runbook Worker**       | Runs runbooks **on-prem** (not just in Azure)   | Automate on-prem AD cleanup             |
| **Update Management**           | Patches OS (Windows/Linux) at scale             | Monthly patch Tuesday                   |
| **Change Tracking & Inventory** | Track changes in software/configs               | Detect registry/file updates            |
| **State Configuration (DSC)**   | Desired State Configuration                     | Enforce IIS installed, services running |

---

## 📌 4. Real-World Examples

- 🖥️ **VM Management**

  - Auto start/stop VMs at business hours.
  - Cleanup unused disks.

- 🔒 **Security & Compliance**

  - Apply latest OS patches.
  - Detect unauthorized software installs.

- 🌐 **Hybrid Use Case**

  - Runbooks executed **on-prem servers** with **Hybrid Runbook Worker**.
  - Example: Resetting AD user passwords from the cloud.

---

## 📌 5. Hands-On Demo (VM Start/Stop Schedule)

### 🔹 Step 1: Create Automation Account

1. Go to **Azure Portal → Automation Accounts → + Add**.
2. Name = `MyAutomation`.
3. Assign Resource Group, Region.

---

### 🔹 Step 2: Create Runbook

Example PowerShell Runbook:

```powershell
param(
    [string]$vmName,
    [string]$rgName
)

$connection = Get-AutomationConnection -Name "AzureRunAsConnection"
Connect-AzAccount -ServicePrincipal -Tenant $connection.TenantId `
    -ApplicationId $connection.ApplicationId -CertificateThumbprint $connection.CertificateThumbprint

Stop-AzVM -Name $vmName -ResourceGroupName $rgName -Force
```

👉 This will **stop a VM** when executed.

---

### 🔹 Step 3: Schedule Runbook

1. Go to Runbook → **Link to Schedule**.
2. Example: Run daily at 7 PM to **shut down dev VMs**.

---

### 🔹 Step 4: (Optional) Run Hybrid Worker

- Install Hybrid Runbook Worker on an **on-prem VM**.
- Now, the same Runbook can manage **local servers** (like shutting down SQL service).

---

## 📊 Visual Flow

```mermaid
flowchart TD
A[Automation Account] --> B[Runbooks (PowerShell/Python)]
B --> C[Azure Resources: VMs, SQL, Storage]
B --> D[On-Prem Servers via Hybrid Runbook Worker]
B --> E[External Services via API/REST]
```

---

## 📌 6. Common Use Cases for Exams

- **Update Management** → patch Windows/Linux VMs.
- **Change Tracking** → track config drift.
- **Runbooks** → automate VM lifecycle tasks.
- **Hybrid Runbook Worker** → extend automation to on-prem.
- **DSC** → enforce system state (install IIS, ensure services running).

---

## 📌 7. Exam Tips (AZ-400 / AZ-104 / AZ-500)

- If the question says:

  - “Automate VM shutdown/startup” → **Azure Automation Runbook**.
  - “Apply OS updates to 1000 VMs” → **Azure Automation Update Management**.
  - “Detect config drift in servers” → **Azure Automation State Configuration (DSC)**.
  - “Run Azure scripts on on-prem servers” → **Hybrid Runbook Worker**.

⚠️ Don’t confuse with:

- **Logic Apps** → workflow orchestration (app integrations).
- **Functions** → event-driven code execution.
- **Automation** → infra management + patching + configs.

---

## ✅ TL;DR

- **Azure Automation** = automate infra + operations with runbooks.
- Supports **PowerShell, Python, graphical workflows**.
- Handles **VM lifecycle, patching, compliance, hybrid tasks**.
- Core exam keywords → **Runbooks, Update Management, DSC, Hybrid Runbook Worker**.
