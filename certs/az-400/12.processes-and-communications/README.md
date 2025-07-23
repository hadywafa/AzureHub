# 🔄 AZ-400 Topic 12: Processes and Communications

📚 Objective: Master collaboration, visibility, traceability, and feedback loops across Dev, Ops, QA, and Business — using Azure DevOps tools like Boards, Work Items, Wikis, Notifications, and Dashboards to **align people with pipelines**.

---

## 🧱 Core Knowledge You Must Master

### 🔹 1. Why This Matters in DevOps

> DevOps isn't just automation — it's **culture + communication + collaboration**.
> People and processes must align to deliver software **continuously, safely, and transparently**.

✅ Without communication, all your YAML and Terraform won’t save you when prod goes down.

---

### 🔹 2. Azure DevOps Boards – Work Items for Traceability

| Feature    | Use Case                                         |
| ---------- | ------------------------------------------------ |
| Work Items | Track tasks, bugs, features, epics               |
| Boards     | Visual Kanban tracking                           |
| Backlogs   | Plan and prioritize work                         |
| Queries    | Custom filters (e.g., “All open bugs in QA”)     |
| Tags       | Organize or flag items (e.g., `hotfix`, `infra`) |

✅ Tie commits, builds, PRs, and deployments to work items → **full traceability**

💬 Example:

> PR #42 fixed Bug #1234, which was deployed in Release #5.

---

### 🔹 3. Communication Flows You Should Implement

| Flow              | Tool/Feature                                                |
| ----------------- | ----------------------------------------------------------- |
| Dev ↔ QA          | Link work items to tests, use Boards, pull request comments |
| Dev ↔ Ops         | Deployment dashboards, environment alerts, incident logs    |
| Dev ↔ Business    | Dashboards with KPIs (cycle time, deployment frequency)     |
| Incident Response | Alerts + ChatOps (Teams/Slack integration)                  |
| Change Approvals  | Use PRs + release approvals with audit logs                 |

✅ DevOps is about **blameless transparency** and **shared responsibility**.

---

### 🔹 4. Linking Code → Pipeline → Work

| Artifact     | How to Link                                      |
| ------------ | ------------------------------------------------ |
| Commit       | Use `#WorkItemID` in commit messages             |
| Pull Request | Automatically links when branch name includes ID |
| Build        | Builds show linked work items                    |
| Release      | Releases show what work items were included      |
| Wiki         | Link from docs to WI and vice versa              |

💡 This creates a **living audit trail** of everything from feature → bug → fix → deploy.

---

### 🔹 5. Wiki and Knowledge Sharing

| Feature            | Benefit                                             |
| ------------------ | --------------------------------------------------- |
| Azure DevOps Wiki  | Markdown-based docs for teams                       |
| Versioned          | Changes are tracked (like Git)                      |
| Cross-linking      | Link to work items, builds, dashboards              |
| Project onboarding | Use wiki for SOPs, release playbooks, RCA templates |

✅ Encourage a “write-it-down” culture — future-you will thank you.

---

### 🔹 6. Dashboards and Visual Reporting

| Widget               | What to Show                        |
| -------------------- | ----------------------------------- |
| Build health         | Last 5 builds, duration, status     |
| Active bugs          | By priority, by team                |
| Deployment frequency | How often to prod? Success/failure? |
| Test results         | Pass/fail by stage or sprint        |
| Lead time            | Work Item to deployment time →      |

✅ Use dashboards for **stand-ups, retros, and incident reviews**.

---

### 🔹 7. Notifications and Integrations

| Tool            | Use Case                                         |
| --------------- | ------------------------------------------------ |
| Email           | Pipeline failures, PR approvals                  |
| Microsoft Teams | PR merged, build failed, alert fired             |
| Slack           | Deployments or incident ChatOps                  |
| Webhooks        | Trigger external systems (PagerDuty, Jira, etc.) |

✅ Filter noise — alert only when action is required.

---

### 🔹 8. DevOps Metrics You Should Know (DORA)

| Metric                    | Description                        |
| ------------------------- | ---------------------------------- |
| **Deployment Frequency**  | How often you ship                 |
| **Lead Time for Changes** | Code commit → prod                 |
| **Change Failure Rate**   | % of deployments that cause issues |
| **MTTR**                  | Mean time to recovery              |

💡 Elite teams **deploy often, fail less, recover faster**. These metrics prove it.

---

## 🧠 Summary of What You Must Be Able to Do

✅ You can:

- Use **Azure Boards** to manage and trace work items end-to-end
- Tie code, builds, PRs, and deployments to **specific features, tasks, and bugs**
- Create **custom dashboards** for visibility across pipelines, teams, and stakeholders
- Set up **automated notifications** for incidents, deployments, and approvals
- Use a **Wiki for internal knowledge sharing** and RCA documentation
- Implement and track **DORA metrics** for DevOps health

---

## 🧪 DevOps Interview Questions – Communication & Process

Here are people-focused, DevOps-practical questions:

---

### 💬 Q1. How do you ensure traceability from feature request to deployment?

**Answer:**

> I use Azure Boards to manage work items, link commits and PRs to those items, and ensure each build/release includes linked work. This way, I can tell exactly what was deployed and why — with full traceability for audits and RCA.

---

### 💬 Q2. What DevOps metrics do you track and why?

**Answer:**

> I track DORA metrics: Deployment Frequency, Lead Time, Change Failure Rate, and MTTR. These help us understand delivery speed, stability, and recovery — essential to drive process improvements.

---

### 💬 Q3. How do you communicate build/release status to the team?

**Answer:**

> I set up Azure DevOps Dashboards and integrate with Microsoft Teams to notify about PRs, failed builds, and deployments. Everyone sees what’s happening in real time, without checking email or dashboards.

---

### 💬 Q4. What’s your approach to documentation?

**Answer:**

> I use the Azure Wiki for onboarding guides, SOPs, deployment runbooks, and RCA reports. It’s markdown-based, easy to update, and version-controlled. I link it with Boards and pipelines for seamless navigation.

---

### 💬 Q5. How do you involve Ops and QA in your DevOps processes?

**Answer:**

> QA gets visibility into what features are shipped via Boards and PR links. Ops gets environment-level dashboards and monitoring alerts via Azure Monitor. We also hold weekly reviews of incidents and pipeline failures.

---

## 🔚 Final Thoughts

✔ DevOps is not just a tech practice — it’s a **people-first operating model**.
✔ Tools like Boards, Wikis, Dashboards, and Alerts **connect people to code**, and create **shared visibility + accountability**.
✔ Communication must be **automated, transparent, and traceable** — just like deployments.
