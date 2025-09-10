# 🏗️ AZ-400 Topic 2: Design and Implement Build Pipelines

📚 Objective: Master the setup of automated build pipelines (CI) using Azure DevOps, including pipeline structure, YAML syntax, triggers, build agents, tasks, templates, variables, and artifact publishing.

---

## 🧱 Core Knowledge You Must Master

### 🔹 1. What Is a Build Pipeline?

> A build pipeline (CI) **automates the process** of compiling, testing, and packaging your code every time a change is made.

✅ In Azure DevOps, pipelines can be written using:

- **YAML (recommended)** — stored as code (`azure-pipelines.yml`)
- **Classic UI** — visual designer, older style but still used

---

### 🔹 2. Pipeline Structure (YAML-Based)

```yaml
trigger:
  branches:
    include:
      - main

pool:
  vmImage: "windows-latest"

variables:
  buildConfiguration: "Release"

steps:
  - task: UseDotNet@2
    inputs:
      packageType: "sdk"
      version: "7.x"

  - script: dotnet build --configuration $(buildConfiguration)
```

| Part        | What It Does                                         |
| ----------- | ---------------------------------------------------- |
| `trigger`   | When to run the pipeline (branch, path)              |
| `pool`      | Defines the agent VM image                           |
| `variables` | Reusable values                                      |
| `steps`     | Series of tasks/scripts (e.g., restore, build, test) |

---

### 🔹 3. Agents, Pools, and Parallelism

| Concept       | Description                                                 |
| ------------- | ----------------------------------------------------------- |
| Agent         | A build runner (Microsoft-hosted or self-hosted)            |
| Pool          | Group of agents                                             |
| Parallel jobs | You get 1 free parallel job per org; scale with paid agents |

✅ Microsoft-hosted agents support:

- `ubuntu-latest`, `windows-latest`, `macos-latest`
- Pre-installed with popular SDKs (e.g., .NET, Node.js, Python)

---

### 🔹 4. Pipeline Triggers

| Trigger Type  | Use Case                          | Syntax                          |
| ------------- | --------------------------------- | ------------------------------- |
| `trigger`     | On push to branch                 | `trigger: { branches: [main] }` |
| `pr`          | On pull request                   | `pr: { branches: [main] }`      |
| `path` filter | Only when specific folders change | `paths: include: [src/**]`      |
| Scheduled     | Nightly or weekly                 | `schedules:` with cron          |

✅ Combine triggers to **optimize build frequency**.

---

### 🔹 5. Build Tasks and Scripts

| Type              | Examples                                                |
| ----------------- | ------------------------------------------------------- |
| Built-in tasks    | `DotNetCoreCLI@2`, `NodeTool@0`, `UsePythonVersion@0`   |
| Script            | Inline shell/PowerShell scripts (`bash`, `pwsh`, `cmd`) |
| Custom extensions | Install from Azure Marketplace                          |
| REST API          | Trigger pipelines programmatically                      |

✅ Reuse common steps using templates:

```yaml
- template: my-common-steps.yml
```

---

### 🔹 6. Variables, Secrets, Templates

| Type               | Use Case                                          |
| ------------------ | ------------------------------------------------- |
| Variables          | Global or step-specific values                    |
| Secret Variables   | Store passwords or tokens securely                |
| Variable Groups    | Shared across pipelines                           |
| Templates          | Modularize complex pipelines into reusable pieces |
| Runtime parameters | Accept values at run time                         |

✅ Use variable substitution: `$(myVar)`
✅ Secure secrets using **Azure Key Vault integration** or secrets in Library.

---

### 🔹 7. Artifact Management

| Concept                   | Purpose                                          |
| ------------------------- | ------------------------------------------------ |
| Build Artifact            | Output of your build (e.g., `.zip`, `.dll`)      |
| `PublishBuildArtifacts@1` | Task to publish the output                       |
| Pipeline Artifacts        | Better performance for large builds              |
| Feed Publishing           | Push artifacts to Azure Artifacts or NuGet feeds |

✅ In CI/CD, artifacts from the **Build stage** flow into **Release stage**.

---

### 🔹 8. Status Badges, Notifications, and Logs

- Azure Pipelines support **status badges** (green/red) for dashboards or README
- Notifications via Teams, Slack, Email
- Rich **logs with timestamps, steps, and output**

---

### 🔹 9. Pipeline Best Practices

| Practice                                   | Why It Matters                                        |
| ------------------------------------------ | ----------------------------------------------------- |
| Keep pipelines in YAML, version-controlled | Traceable and consistent                              |
| Fail fast                                  | Run unit tests early to catch issues quickly          |
| Use caching                                | Speed up builds (e.g., `nuget`, `npm`)                |
| Modularize                                 | Use templates to reduce repetition                    |
| Isolate stages                             | Build, Test, Lint, Package, Publish as separate steps |

---

## 🧠 Summary of What You Must Be Able to Do

✅ You can:

- Design a CI pipeline using **YAML**
- Select proper **agent pools** and understand Microsoft-hosted vs self-hosted agents
- Use **triggers and path filters** to optimize pipeline runs
- Write **multi-stage pipelines** (Build → Test → Publish)
- Secure secrets and environment-specific values using variable groups or Key Vault
- Produce and publish **artifacts** to feeds or release stages
- Build CI pipelines for .NET, Node, Python, Java with ease

---

## 🧪 DevOps Interview Questions – Build Pipelines

Here are some smart, experience-driven interview questions:

---

### 💬 Q1. How do you design a CI pipeline for a .NET microservice?

**Answer:**

> I create a YAML-based Azure DevOps pipeline with steps to install the .NET SDK, restore NuGet packages, run unit tests, and build the service. I use triggers to run on every push to `main`, and publish build artifacts for downstream use in release.

---

### 💬 Q2. What are agent pools and why would you use self-hosted agents?

**Answer:**

> Agent pools are collections of build runners. I use Microsoft-hosted agents for general builds, but switch to self-hosted agents when I need custom software, faster builds, or access to private networks.

---

### 💬 Q3. How do you handle secrets in build pipelines?

**Answer:**

> I store secrets in Azure Key Vault or mark pipeline variables as secret. These are injected at runtime and never exposed in logs. I avoid hardcoding credentials in YAML or scripts.

---

### 💬 Q4. How can you optimize pipeline performance?

**Answer:**

> Use caching (`NuGet`, `npm`), run builds in parallel, split long jobs into smaller stages, use path/branch filters to avoid unnecessary runs, and reuse common steps with templates.

---

### 💬 Q5. What’s the difference between Classic pipelines and YAML pipelines?

**Answer:**

> Classic pipelines use a UI designer; YAML pipelines are infrastructure-as-code, version-controlled, and easier to review and reuse. YAML is the modern, preferred method.

---

### 💬 Q6. What’s a build artifact and how do you use it?

**Answer:**

> A build artifact is the output from a successful build — binaries, zip files, packages, etc. I publish them using `PublishBuildArtifacts` and use them in release pipelines to deploy or test.

---

### 💬 Q7. What are some common pipeline mistakes you’ve seen?

**Answer:**

> Overtriggering (e.g., building on every commit to every branch), hardcoding secrets, untested YAML syntax, not version-controlling pipelines, and not separating build/test/deploy logically.

---

## 🔚 Final Thoughts

✔ A build pipeline is not just about compiling code — it's about **making your entire team productive, automating quality gates, and creating reproducible outputs**.
✔ In Azure DevOps, **YAML pipelines** are king. Learn how to **combine templates, variables, triggers, and agents** like a pro.
