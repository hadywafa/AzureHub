# 📜 Azure Service Level Agreements (SLAs) — The Cloud's Promise Contract

## 🌍 1. What is an SLA in Azure?

In Azure, a **Service Level Agreement (SLA)** is a **formal commitment** from Microsoft that a service will meet specific **uptime and connectivity guarantees** over a **billing month**.

💡 Think of it as **Microsoft’s uptime warranty** for their cloud services.

- If Azure fails to meet this SLA, **you get service credits** (not cash).
- Measured **per billing month**.
- SLAs can apply to **individual services**, **combinations of services**, or **service tiers**.

---

## 🧩 2. Key SLA Terms You Must Know

| Term                 | Meaning                                                               | Example                                            |
| -------------------- | --------------------------------------------------------------------- | -------------------------------------------------- |
| **Uptime**           | Percentage of time service is available                               | 99.9% uptime = ≤ 43.2 min downtime/month           |
| **Downtime**         | When the service is unavailable due to Microsoft’s fault              | Azure VM host crash                                |
| **Service Credit**   | Percentage of monthly bill refunded if SLA not met                    | 10% credit for 99.0% uptime instead of 99.9%       |
| **Monthly Uptime %** | Formula to measure SLA                                                | `(Total minutes - Downtime) / Total minutes × 100` |
| **Composite SLA**    | When multiple services combine — overall SLA is lower than individual | VM + SQL Database                                  |

💡 **AWS Parallel:** AWS also has SLAs for each service (e.g., EC2 = 99.99% in multi-AZ), but Azure is slightly stricter in requiring **redundancy configuration** to get the highest SLA.

---

## 🛠 3. SLA Calculation Example

Let’s say **Azure SQL Database** guarantees **99.99%** monthly uptime.

- **Total minutes in 30-day month:** `43,200 min`
- Allowed downtime = `0.01% of 43,200 = 4.32 min`

If downtime exceeds 4.32 min, Microsoft must issue service credits.

---

## 🏗 4. SLA Tiers for Common Services

| Azure Service                          | Basic SLA | High Availability SLA | Requirement                |
| -------------------------------------- | --------- | --------------------- | -------------------------- |
| **Azure VMs (Single Instance)**        | 99.9%     | ❌                    | Just one VM in 1 zone      |
| **Azure VMs (Availability Set)**       | ❌        | 99.95%                | 2+ VMs in Availability Set |
| **Azure VMs (Availability Zones)**     | ❌        | 99.99%                | 2+ VMs in different AZs    |
| **Azure Storage (General Purpose v2)** | 99.9%     | 99.99%                | RA-GRS redundancy          |
| **Azure SQL Database (Single)**        | 99.99%    | —                     | No extra config            |
| **Azure Load Balancer**                | 99.99%    | —                     | Standard SKU               |

---

## 📦 5. Composite SLAs

When services **depend on each other**, overall SLA = **multiplication of individual SLAs**.

Example:

- Azure App Service = **99.95% SLA**
- Azure SQL Database = **99.99% SLA**

**Composite SLA** = 0.9995 × 0.9999 = **99.94% overall**
👉 This means \~26.3 minutes allowed downtime/month.

💡 AWS parallel: Same concept — multi-service dependencies reduce your total guarantee.

---

## 🔐 6. SLA Eligibility Rules

- SLA applies **only if you configure redundancy** according to Microsoft’s best practices.
- SLA **doesn’t apply** for:

  - Preview services
  - Free tiers
  - Issues caused by your configurations or network
  - Force majeure (e.g., natural disasters)

---

## 📜 7. Service Credit Tiers Example (VM SLA)

| Monthly Uptime %     | Service Credit |
| -------------------- | -------------- |
| < 99.99% but ≥ 99.0% | 10%            |
| < 99.0% but ≥ 95.0%  | 25%            |
| < 95.0%              | 100%           |

---

## 🚦 8. Best Practices to Achieve High SLA

- ✅ Deploy in **Availability Zones** or **Availability Sets** for redundancy
- ✅ Use **Load Balancers** to spread traffic
- ✅ Implement **auto-healing** for failed VMs
- ✅ Choose **Standard SKU** services where possible
- ✅ Monitor SLA changes — Microsoft can update SLA terms anytime

---

## 🧠 9. Exam Tip for AZ-104

- **99.9% SLA** → Single VM
- **99.95% SLA** → VMs in Availability Set
- **99.99% SLA** → VMs in Availability Zones
- **Composite SLA** is **always less** than individual SLAs
- SLAs do **not apply to preview or free tiers**

---

## 📊 10. SLA Comparison (Azure vs AWS)

| Feature              | Azure              | AWS                  |
| -------------------- | ------------------ | -------------------- |
| Highest VM SLA       | 99.99% with AZ     | 99.99% with Multi-AZ |
| Service Credit Model | % of bill refunded | % of bill refunded   |
| Free/Preview SLA     | ❌                 | ❌                   |
| Composite SLA        | Yes                | Yes                  |
