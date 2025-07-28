# 🚀 AZ-400 Topic 8: Design and Implement Deployments

📚 Objective: Master the methods and tools to deploy applications in a **repeatable**, **safe**, and **automated** way across different environments, including support for **infrastructure deployment**, **progressive delivery**, and **environment-specific controls**.

---

## 🧱 Core Knowledge You Must Master

### 🔹 1. What Is a Deployment in DevOps?

> A **deployment** is the act of delivering software or infrastructure into a target environment (Dev, QA, Prod) — ideally **automated**, **auditable**, and **safe to repeat**.

✅ Key goals:

- Repeatability (no manual steps)
- Safety (rollback + health checks)
- Traceability (who deployed what, when, where)
- Visibility (logs, approval, notifications)

---

### 🔹 2. Types of Deployments You Must Know

| Type                          | Description                                                                 | Tool Examples                            |
| ----------------------------- | --------------------------------------------------------------------------- | ---------------------------------------- |
| **Application Deployment**    | Delivering app code (e.g., .NET API) to servers, containers, Azure services | Azure Pipelines, GitHub Actions, Octopus |
| **Infrastructure Deployment** | Provisioning infrastructure via code                                        | Terraform, Bicep, ARM, Pulumi            |
| **Rolling Deployment**        | Gradually replace old versions                                              | Azure App Service, AKS                   |
| **Blue/Green Deployment**     | Deploy to new slot/environment, swap on success                             | Azure App Service slots                  |
| **Canary Deployment**         | Deploy to small % of traffic first                                          | AKS + Ingress, Azure Front Door          |
| **Shadow Deployment**         | Release new version silently alongside live version                         | Custom routing logic, A/B infra          |
| **Feature Toggles**           | Deploy code but control via runtime flags                                   | LaunchDarkly, Azure App Config           |

---

### 🔹 3. Deployment Targets in Azure

| Target                         | Tools                                               |
| ------------------------------ | --------------------------------------------------- |
| Azure App Service              | `AzureWebApp@1` task, slot swaps                    |
| Azure Functions                | `func azure functionapp publish`, or Azure CLI task |
| Azure Kubernetes Service (AKS) | `kubectl`, `helm`, GitOps (Flux/ArgoCD)             |
| Azure VMs                      | SSH, WinRM, Deployment Groups                       |
| Azure Container Apps           | Bicep, CLI, GitHub Actions                          |
| On-prem or hybrid              | Self-hosted agents, custom scripts                  |

✅ Learn to automate **deployment AND infra provisioning** — DevOps = App + Infra.

---

### 🔹 4. YAML-Based CD Pipelines in Azure DevOps

```yaml
stages:
  - stage: DeployDev
    jobs:
      - deployment: DeployToAppService
        environment: "dev"
        strategy:
          runOnce:
            deploy:
              steps:
                - task: AzureWebApp@1
                  inputs:
                    azureSubscription: "MySPN"
                    appName: "my-api-dev"
                    package: "$(Pipeline.Workspace)/drop/*.zip"
```

✅ Know how to:

- Use `deployment:` keyword for CD stages
- Use `environment:` for approvals and gates
- Promote artifacts from build to release stages

---

### 🔹 5. Infrastructure-as-Code (IaC) for Deployments

You must manage infra changes the same way you manage code.

| Tool              | Description                          |
| ----------------- | ------------------------------------ |
| **Terraform**     | Platform-neutral, declarative IaC    |
| **Bicep**         | Azure-native, ARM template wrapper   |
| **ARM templates** | Raw JSON Azure resource templates    |
| **Pulumi**        | IaC using real programming languages |

✅ Deploy via Azure CLI task or IaC-specific tasks in pipeline
✅ Store templates in Git and version control infra releases

---

### 🔹 6. Safe Deployment Practices

| Practice             | What to Do                                                |
| -------------------- | --------------------------------------------------------- |
| Staging environments | Always deploy to test/stage before prod                   |
| Slot deployments     | Use staging slot + swap for App Services                  |
| Health probes        | Use availability tests or custom scripts post-deploy      |
| Release gates        | Use App Insights or Azure Monitor to validate deployments |
| Auto-rollback        | Trigger rollback on failed health or alert                |

✅ Use **“manual intervention”** and **approval gates** for production.

---

### 🔹 7. Deployment Approvals and Environments

| Feature                      | Purpose                               |
| ---------------------------- | ------------------------------------- |
| Pre-deployment approval      | Prevent accidental deploys            |
| Post-deployment approval     | Ensure verification before proceeding |
| Environment-scoped variables | Per-env API keys, config values       |
| Deployment history           | Auditable release trails              |

✅ Protect prod with **RBAC, approvals, and audit logging**

---

## 🧠 Summary of What You Must Be Able to Do

✅ You can:

- Design **automated deployments** for app code and infra using Azure Pipelines
- Choose the right strategy: blue/green, canary, rolling, etc.
- Deploy to **Azure-native targets** (App Service, AKS, VMs, Functions)
- Use **IaC templates** (Terraform, Bicep) in your pipeline to provision/update infra
- Define **safe delivery flows** with approvals, gates, and health checks
- Manage **environment-specific config and secrets**

---

## 🧪 DevOps Interview Questions – Deployments

Here are the kinds of questions they’ll ask (and how to stand out):

---

### 💬 Q1. How do you deploy a .NET application to Azure?

**Answer:**

> I build the app in a CI pipeline and publish the artifact (e.g., ZIP). In the CD stage, I use the `AzureWebApp@1` task to deploy to Azure App Service. I use slots for staging and swap only when validation passes.

---

### 💬 Q2. How do you manage infrastructure as part of deployment?

**Answer:**

> I use Terraform or Bicep as part of the pipeline to provision infrastructure. The IaC scripts are version-controlled, tested, and validated before deploying. This ensures environments are reproducible and consistent.

---

### 💬 Q3. What is a canary deployment? When would you use it?

**Answer:**

> A canary deployment sends a small % of traffic to the new version while the rest stays on the old one. If no issues arise, we gradually roll out to all users. I’d use it in high-traffic, customer-facing services where risk is high.

---

### 💬 Q4. How do you handle production rollback?

**Answer:**

> I use versioned artifacts and infrastructure templates. If a deploy fails validation or monitoring gates, the pipeline either halts or triggers a rollback using the last known-good release.

---

### 💬 Q5. What tools do you use to deploy to Kubernetes?

**Answer:**

> I use `kubectl` or `helm` in Azure Pipelines, along with Kubernetes manifest files or Helm charts. For progressive delivery, I may use ArgoCD or Flux with GitOps.

---

### 💬 Q6. How do you configure approvals in Azure DevOps?

**Answer:**

> I define environments in the pipeline with pre- or post-deployment approvals. Only users in the approval group can proceed. This adds a governance checkpoint before sensitive stages like Prod.

---

## 🔚 Final Thoughts

✔ A DevOps engineer must treat **deployments as products**: safe, automated, and auditable
✔ Combine app + infra deployment, approvals, and post-deploy checks for **reliable delivery**
