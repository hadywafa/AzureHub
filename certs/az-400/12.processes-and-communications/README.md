# 🧩 Processes & Communications (AZ-400)

Here’s the **topic breakdown** (ordered as they build on each other):

1. 🌍 **Agile Methodology Basics**
2. 📈 **Agile Metrics & Reporting** (velocity, burndown, cumulative flow, lead/cycle time)
3. 🏉 **Scrum Framework** (roles, artifacts, ceremonies)
4. 📊 **Work Item Processes in Azure DevOps** (Basic, Agile, Scrum, CMMI)
5. 🗂️ **Boards, Backlogs, Sprints, Queries** (work tracking tools)
6. 📖 **Wikis & Knowledge Sharing**
7. 📊 **Dashboards & Widgets** (project visibility & reporting)
8. 📨 **Communication & Collaboration** (integrations: Teams, Slack, email, Service Hooks)
9. 🧭 **Project Governance** (policies, approvals, branch policies, compliance docs)

---

## 🌍 1. Agile Methodology Basics

- Agile = **mindset** → deliver value quickly, adapt to change.
- Core values: **people > processes, working software > docs, collaboration > contracts, change > fixed plan.**
- Exam tip → Remember Agile = umbrella, Scrum/Kanban = frameworks.

👉 **Keyword to memorize**: _“Agile = small, fast, adaptive.”_

---

## 🏉 2. Scrum Framework

- Roles: **PO (what), Dev Team (how), SM (coach)**
- Artifacts: **Product Backlog, Sprint Backlog, Increment**
- Events: **Planning, Daily Scrum, Review, Retrospective**
- Exam tip → Scrum is **time-boxed** (2–4 weeks).

👉 **Keyword to memorize**: _“Scrum = sprints, roles, ceremonies.”_

---

## 📊 3. Work Item Processes in Azure DevOps

- **Basic** → simple (Issues, Tasks, Epics).
- **Agile** → uses User Stories.
- **Scrum** → uses PBIs (Product Backlog Items).
- **CMMI** → heavy, enterprise governance.

👉 **Keyword to memorize**: _“Process = naming + structure of work items.”_

---

## 🗂️ 4. Boards, Backlogs, Sprints, Queries

- **Boards** → Kanban view of work items (To Do → Doing → Done).
- **Backlogs** → ordered lists of work (Epics → Features → Stories/Tasks).
- **Sprints** → time-boxed slices with burndown tracking.
- **Queries** → filters & reports (e.g., “All open bugs in Sprint 2”).

👉 **Keyword to memorize**: _“Boards = tracking, Backlog = planning, Sprints = execution, Queries = reporting.”_

---

## 📖 5. Wikis & Knowledge Sharing

- **Wikis** → team documentation hub (Markdown pages).
- Stores runbooks, architecture notes, decisions.
- Can link Wiki pages to work items.

👉 **Keyword to memorize**: _“Wiki = project memory.”_

---

## 📊 6. Dashboards & Widgets

- **Dashboards** = visual control panels.
- **Widgets** = building blocks inside dashboards (burndown, velocity, build status).
- Used by managers/stakeholders for quick project health checks.

👉 **Keyword to memorize**: _“Dashboard = cockpit, Widgets = instruments.”_

---

## 📨 7. Communication & Collaboration

- Azure DevOps integrates with **Microsoft Teams, Slack, email**.
- **Service hooks** → notify external systems (e.g., post to Teams when build fails).
- Keeps dev team + stakeholders updated automatically.

👉 **Keyword to memorize**: _“Integration = no surprises.”_

---

## 🧭 8. Project Governance

- Define rules to ensure quality & compliance:

  - **Branch policies** (PRs, reviewers, builds).
  - **Approvals** in pipelines.
  - **Auditing & documentation** (often stored in Wikis).

- Helps maintain security & compliance.

👉 **Keyword to memorize**: _“Governance = rules + approvals.”_

---

## 📈 9. Metrics & Reporting

- Common Agile metrics:

  - **Velocity** (SP completed per sprint)
  - **Burndown chart** (work left vs time)
  - **Cumulative flow** (WIP tracking)
  - **Lead time & cycle time** (delivery speed)

👉 **Keyword to memorize**: _“Metrics = visibility + improvement.”_

---

## ✅ Exam-Style Recap

- **Agile = mindset** → flexible, iterative.
- **Scrum = framework** → sprints, roles, artifacts.
- **Processes** (Agile, Scrum, CMMI, Basic) = how work items are structured.
- **Boards/Backlogs/Sprints** = track and execute work.
- **Wikis** = team documentation.
- **Dashboards + Widgets** = reporting visibility.
- **Communication tools** = Teams, Slack, service hooks.
- **Governance** = policies, approvals, compliance.
- **Metrics** = measure velocity, flow, cycle time.

---

## 🔄 AZ-400 Topic 12: Processes and Communications

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
