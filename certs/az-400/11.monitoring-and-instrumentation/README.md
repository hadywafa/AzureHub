# 📈 AZ-400 Topic 11: Monitoring and Instrumentation

📚 Objective: Master how to collect, analyze, and visualize **logs**, **metrics**, **traces**, and **alerts** in Azure DevOps and Azure Monitor. Ensure your pipelines and apps are observable, support proactive issue detection, and enable postmortem analysis.

---

## 🧱 Core Knowledge You Must Master

### 🔹 1. Why Monitoring in DevOps?

> DevOps isn't complete without **feedback loops**. Monitoring tells you:

- What broke?
- When?
- Why?
- And how to fix it **before customers scream**.

✅ **Telemetry is a pillar** of DevOps: Plan → Build → Test → Release → Monitor 🔁

---

### 🔹 2. Key Monitoring Concepts

| Term          | Description                                                 |
| ------------- | ----------------------------------------------------------- |
| **Metric**    | Numeric value over time (e.g., CPU %, request count)        |
| **Log**       | Textual data or event stream (e.g., error logs, trace logs) |
| **Trace**     | Flow of a request across services (distributed tracing)     |
| **Alert**     | Notification based on metric or log thresholds              |
| **Dashboard** | Visualized telemetry data for human eyes 👀                 |

✅ Azure Monitor, Application Insights, and Log Analytics are core Azure tools here.

---

### 🔹 3. Tools You Should Know

| Tool                     | Purpose                                                  |
| ------------------------ | -------------------------------------------------------- |
| **Azure Monitor**        | Full-stack telemetry engine for Azure resources          |
| **Application Insights** | App-level monitoring: requests, dependencies, exceptions |
| **Log Analytics**        | Query logs via KQL (Kusto Query Language)                |
| **Azure Dashboards**     | Visualize metrics and logs in custom views               |
| **Alerts**               | Create rules based on thresholds or log queries          |

✅ All integrate seamlessly into **Azure DevOps Pipelines**, **App Services**, **Kubernetes (AKS)**, and more.

---

### 🔹 4. Application Insights (App Insights)

| Tracks        | Examples                               |
| ------------- | -------------------------------------- |
| Requests      | `GET /api/orders` success/failure rate |
| Exceptions    | Stack traces, handled/unhandled        |
| Dependencies  | SQL calls, external APIs, queues       |
| Custom Events | Business events, user actions          |
| Availability  | Ping test from different regions       |

✅ Use **instrumentation key** or `connection string` to wire up SDKs in your app.
✅ Works with .NET, Java, Node.js, Python, etc.

---

### 🔹 5. Enabling App Insights in .NET

```csharp
// Startup.cs
services.AddApplicationInsightsTelemetry(Configuration["APPINSIGHTS_CONNECTIONSTRING"]);
```

✅ Automatically tracks:

- HTTP requests
- Exceptions
- Dependencies
- Performance counters

---

### 🔹 6. Log Analytics + KQL

**KQL (Kusto Query Language)** is used to search, analyze, and correlate telemetry.

```kql
requests
| where timestamp > ago(1h)
| summarize count() by resultCode
```

✅ Know how to:

- Search logs
- Aggregate metrics
- Join across tables
- Visualize in dashboards

---

### 🔹 7. Azure Monitor Alerts

| Type               | Triggered By                               |
| ------------------ | ------------------------------------------ |
| Metric Alert       | CPU > 80%, Memory > 75%                    |
| Log Alert          | “Exception” in last 5 mins                 |
| Activity Log Alert | Azure resource events (e.g., delete VM)    |
| Smart Detection    | ML-based anomaly detection in App Insights |

✅ Alerts can notify via:

- Email
- SMS
- Webhook
- Azure DevOps (Work Items)
- Teams / Slack

---

### 🔹 8. Integrating Monitoring in Pipelines

| Step                        | Description                                       |
| --------------------------- | ------------------------------------------------- |
| Monitor pipeline health     | Use built-in logs and test result views           |
| Publish telemetry           | Add custom logging in build/release tasks         |
| Post-deployment validation  | Run smoke tests + App Insights availability tests |
| Alert on failed deployments | Use Azure Monitor to track failures               |

✅ Use “**Deployment Gates**” in release pipelines to **query App Insights** before proceeding.

---

### 🔹 9. Distributed Tracing (Optional but 💎 in Interviews)

> For microservices and serverless: **Trace a request across services** using correlation IDs.

✅ Tools:

- App Insights (includes trace correlation)
- OpenTelemetry (industry standard)
- Azure Monitor OpenTelemetry Exporter

---

### 🔹 10. Dashboards & Workbooks

| Feature         | Description                                  |
| --------------- | -------------------------------------------- |
| Azure Dashboard | Drag-and-drop panels from different services |
| Workbooks       | Rich reporting with charts, metrics, logs    |
| Shared View     | Collaborate with DevOps, QA, Support teams   |

✅ Create a dashboard showing:

- CPU/Memory of App Service
- Requests and errors from App Insights
- Recent alerts from Azure Monitor
- SLA/latency per API route

---

## 🧠 Summary of What You Must Be Able to Do

✅ You can:

- Instrument .NET apps with **Application Insights**
- Use **Log Analytics (KQL)** to analyze errors and performance
- Set up **Azure Monitor Alerts** for proactive notification
- Visualize performance using **Dashboards & Workbooks**
- Add **availability tests** to monitor from global locations
- Use **monitoring gates in pipelines** to block bad deploys
- Explain the value of **distributed tracing** in microservices

---

## 🧪 DevOps Interview Questions – Monitoring

Let’s prep for smart questions you may get asked:

---

### 💬 Q1. How do you monitor your applications in Azure?

**Answer:**

> I use Application Insights for tracking requests, exceptions, and performance metrics. I also integrate it with Azure Monitor and Log Analytics to create alerts and dashboards. I configure availability tests and use KQL to analyze logs when things go wrong.

---

### 💬 Q2. What’s the difference between Application Insights and Log Analytics?

**Answer:**

> App Insights is for app-level telemetry like requests and exceptions. Log Analytics is a general log platform that can query App Insights, Azure Monitor, and other sources using KQL. I use both to correlate events and monitor the entire stack.

---

### 💬 Q3. How do you alert your team when something breaks?

**Answer:**

> I create alert rules in Azure Monitor that trigger on metric thresholds or error logs. Alerts notify via email, Teams, and Azure DevOps. For prod deployments, I even configure release gates that check for health metrics before proceeding.

---

### 💬 Q4. How do you monitor a multi-service architecture?

**Answer:**

> I use distributed tracing with correlation IDs. App Insights supports automatic tracing for HTTP calls between services. I can trace a single request through all layers and identify where it failed or slowed down.

---

### 💬 Q5. How do you know a deployment didn’t break the app?

**Answer:**

> I run automated smoke tests and availability tests post-deployment. I monitor App Insights for spikes in failed requests or exceptions. If metrics breach the threshold, alerts trigger and I roll back the deployment.

---

### 💬 Q6. Have you used KQL? What for?

**Answer:**

> Yes. I use KQL to query logs for failed requests, slow performance, and API usage patterns. I also use KQL to build dashboards and define alert rules — like exceptions in the last 5 minutes or high 5xx error rates.

---

## 🔚 Final Thoughts

✔ Monitoring is the **backbone of modern DevOps**.
✔ It's not just about alerts — it's about **visibility, action, and trust**.
✔ If you deploy fast but can’t detect problems fast — you’re flying blind.
