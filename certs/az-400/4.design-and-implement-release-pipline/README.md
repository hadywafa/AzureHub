# 🚀 AZ-400 Topic 4: Design and Implement Release Pipelines

📚 Objective: Master release pipelines (CD) in Azure DevOps — deploying apps to test/staging/prod environments, managing approvals, approvals, variables, gates, artifact flows, and rollback strategies.

---

## 🧱 Core Knowledge You Must Master

### 🔹 1. What is a Release Pipeline?

> A **release pipeline** automates deploying **build artifacts** from your CI process into multiple environments like Dev, QA, UAT, and Production — with **checks**, **approvals**, and **rollbacks** built in.

🧠 Think of CI = build + test → ✅
CD = deploy + validate + approve → ✅✅✅

---

### 🔹 2. Pipeline Types: Build vs Release

| Feature      | Build Pipeline (CI)             | Release Pipeline (CD)           |
| ------------ | ------------------------------- | ------------------------------- |
| Triggered by | Code change / PR                | Artifact published              |
| Purpose      | Compile, test, produce artifact | Deploy artifact to environments |
| Format       | YAML (recommended)              | Classic UI or YAML multi-stage  |
| Key Features | Tasks, stages                   | Approvals, gates, environments  |

✅ Modern teams use **multi-stage YAML pipelines** for both CI and CD in a single file.

---

### 🔹 3. YAML Multi-Stage Pipeline: Build + Release

```yaml
stages:
  - stage: Build
    jobs:
      - job: BuildJob
        steps:
          - script: dotnet build

  - stage: Deploy
    dependsOn: Build
    condition: succeeded()
    jobs:
      - deployment: DeployToDev
        environment: "Dev"
        strategy:
          runOnce:
            deploy:
              steps:
                - script: echo "Deploying to Dev"
```

| Part           | Description                                     |
| -------------- | ----------------------------------------------- |
| `stage:`       | A logical step (build, deploy, test)            |
| `environment:` | Logical group for deployments (Dev/UAT/Prod)    |
| `deployment:`  | YAML keyword for CD behavior                    |
| `strategy:`    | Deployment flow: `runOnce`, `rolling`, `canary` |

✅ YAML gives **code-as-infrastructure, traceability, and reuse**.

---

### 🔹 4. Classic Release Pipelines (Visual Designer)

| Component | Purpose                                             |
| --------- | --------------------------------------------------- |
| Artifact  | Output from build pipeline                          |
| Stage     | Dev, QA, UAT, Prod (one or more)                    |
| Tasks     | Deployment actions (e.g., Azure App Service Deploy) |
| Approvals | Manual checks before/after stages                   |
| Gates     | Automated checks (e.g., query API, run script)      |

✅ Great for legacy or UI-first teams. YAML is preferred long-term.

---

### 🔹 5. Deployment Methods in Azure DevOps

| Target              | Task                                       | Notes                         |
| ------------------- | ------------------------------------------ | ----------------------------- |
| Azure App Service   | `AzureWebApp@1`                            | Zip deploy, slot swap support |
| VMs (Windows/Linux) | `AzureVMs@2`, WinRM/SSH                    | Needs agent or SSH key        |
| Azure Functions     | `func azure functionapp publish` or task   |                               |
| Containers          | Push to ACR → Deploy to AKS                |                               |
| Kubernetes          | `kubectl`, `helm`, `Kustomize` in pipeline |                               |

✅ Master at least 1–2 deployment targets (App Service & AKS highly preferred).

---

### 🔹 6. Approval & Gates

| Feature                   | Description                                                 |
| ------------------------- | ----------------------------------------------------------- |
| Pre-deployment approvals  | Manual validation (e.g., QA signoff)                        |
| Post-deployment approvals | Manual rollback check                                       |
| Gates                     | Auto-checks: API query, Azure Monitor, Service Health, etc. |
| Delay gates               | E.g., “Wait 2 hours after QA pass before deploying to Prod” |

✅ Ensures human + machine checks before sensitive deployments.

---

### 🔹 7. Environments

| What Are They?                                  | Why Use Them?                                                   |
| ----------------------------------------------- | --------------------------------------------------------------- |
| Logical names for target stages (Dev/Test/Prod) | Centralizes approval flow, deployment history, resource mapping |
| Environment secrets                             | Secure variables scoped per environment                         |
| Deployment history                              | View who deployed what, when, where                             |
| Auditing & rollback                             | Easy traceability + retention logs                              |

✅ Use environment-level RBAC to **restrict access by stage**.

---

### 🔹 8. Variables, Parameters, Templates (CD-Specific)

| Feature                | Usage                          |
| ---------------------- | ------------------------------ |
| Pipeline variables     | `$(var)` for reuse             |
| Stage-scoped variables | Only apply within 1 stage      |
| Variable groups        | Shared config (e.g., API keys) |
| Templates              | Reusable deployment steps      |

✅ Store sensitive values in **Azure Key Vault** or pipeline secrets.

---

### 🔹 9. Deployment Strategies

| Strategy   | Description                                     |
| ---------- | ----------------------------------------------- |
| RunOnce    | Basic deployment (default)                      |
| Rolling    | Gradually deploy across regions/instances       |
| Canary     | Deploy to a small subset of traffic first       |
| Blue/Green | New environment spun up → swapped when verified |

✅ Canary + Gates + Monitoring = **safe production deployment**

---

### 🔹 10. Rollback Planning

| Feature                 | Tool                                                |
| ----------------------- | --------------------------------------------------- |
| Manual rollback         | Redeploy previous release                           |
| Automated rollback      | Requires custom script/gate on failure              |
| Versioning              | Tag releases clearly                                |
| Infrastructure rollback | Use IaC versioned templates (Bicep, ARM, Terraform) |

✅ Plan rollback **before** you deploy — not after 😅.

---

## 🧠 Summary of What You Must Be Able to Do

✅ You can:

- Design release pipelines for **multi-stage deployments** using YAML or Classic
- Automate deployments to Azure, Kubernetes, Linux/Windows VMs
- Use **environments** to apply approval gates, secrets, and logs
- Implement **manual approvals**, **automated gates**, and **deployment strategies**
- Safely promote from Dev → QA → Prod using **artifact-based CD**
- Handle deployment failures with **rollback and alerting logic**

---

## 🧪 DevOps Interview Questions – Release Pipelines

Here are real-world, behavioral and technical questions:

---

### 💬 Q1. What’s the difference between a build pipeline and a release pipeline?

**Answer:**

> A build pipeline compiles and tests code to produce artifacts. A release pipeline deploys those artifacts to target environments, usually with manual approvals, gates, and rollback logic. I prefer using multi-stage YAML pipelines to do both in one file.

---

### 💬 Q2. How do you deploy an app to multiple environments in Azure DevOps?

**Answer:**

> I define stages for each environment (Dev, QA, Prod), and assign deployment jobs with conditions and approvals. I use environment-level variables and link them to service connections to avoid duplication.

---

### 💬 Q3. How do you ensure safety when deploying to production?

**Answer:**

> I use canary deployments, monitoring gates (e.g., Azure Monitor), and post-deployment approvals. If any health check fails, I trigger an automatic rollback or halt the release.

---

### 💬 Q4. What tools/tasks do you use to deploy .NET apps to Azure?

**Answer:**

> I use the `AzureWebApp@1` task in Azure DevOps, along with slot deployment and swap. I configure ARM or Bicep templates beforehand to provision the environment.

---

### 💬 Q5. How do you manage secrets in release pipelines?

**Answer:**

> Secrets are stored in Azure Key Vault and accessed through service connections. In pipelines, I use secret variables or link variable groups. They’re never echoed in logs.

---

### 💬 Q6. Can you explain the purpose of gates in a release pipeline?

**Answer:**

> Gates are automated checks that run before or after a deployment. They can query an API, check service health, wait a delay, or run a script. They act as smart filters to protect against bad rollouts.

---

### 💬 Q7. How would you rollback a failed deployment?

**Answer:**

> I version artifacts and infra templates. If a deployment fails, I can redeploy a previous artifact using the release history. If infra is broken, I roll back Terraform or ARM to the previous version.

---

## 🔚 Final Thoughts

✔ A release pipeline is **not just a script** — it's a smart, staged system of **environments, policies, validations, and approvals**.
✔ Think of it as your organization's **last line of defense** before prod — secure it like a bank vault.
