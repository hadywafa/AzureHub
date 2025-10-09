# 💧 Azure Data Lake Analytics (ADLA)

> 🚨 Azure Data Lake Analytics (ADLA) is still available, but it's largely deprecated and rarely used in modern Azure architectures. Microsoft now recommends using Azure Synapse, Databricks, or HDInsight for scalable analytics.

## 🧠 What It Is

> **Azure Data Lake Analytics (ADLA)** is a **serverless big data analytics service** that lets you **analyze massive amounts of data stored in Azure Data Lake Storage** using a **simple SQL-like language called U-SQL** — without managing any servers or clusters.

Think of it as:

> “Run a huge query on petabytes of data in Data Lake without creating a Hadoop cluster.”

---

## 🧩 The Core Idea

ADF = **moves** data
ADLS = **stores** data
ADLA = **analyzes** data

✅ You **write queries**, not code.
✅ You **don’t manage clusters**, Azure handles scaling automatically.
✅ You **pay only per job**, not per hour.

---

## 🧱 Architecture Overview

Let’s visualize it 👇

```mermaid
---
config:
  theme: dark
---
flowchart LR
    A[Azure Data Lake Storage<br>(Raw / Processed Data)] --> B[Azure Data Lake Analytics<br>(U-SQL Job)]
    B -->|Query Results| C[Power BI / Excel / Azure SQL]
```

### 🔍 Explanation:

1️⃣ You store data (CSV, JSON, Parquet, etc.) in **ADLS**
2️⃣ You write **U-SQL** queries to process or aggregate the data
3️⃣ ADLA automatically **scales compute nodes** to process it
4️⃣ You get your **results saved back** to ADLS or other sinks

---

## ⚙️ Key Features

| Feature               | Description                                           |
| --------------------- | ----------------------------------------------------- |
| **Serverless**        | No need to create or manage clusters                  |
| **Scalable**          | Automatically allocates compute resources             |
| **Pay-per-job**       | You only pay for the job duration and resources used  |
| **U-SQL Language**    | Combines SQL + C# for advanced processing             |
| **Tight Integration** | Works natively with Azure Data Lake Storage Gen1/Gen2 |
| **Security**          | Uses Azure AD for access and RBAC for permissions     |

---

## 🧮 What Is U-SQL?

> U-SQL = **SQL + C# hybrid language** designed for big data processing.

It looks like SQL but lets you embed C# for complex logic.
Example 👇

```sql
@data =
    EXTRACT UserId int,
            Product string,
            Amount float
    FROM "adl://mydatalake.azuredatalakestore.net/raw/sales.csv"
    USING Extractors.Csv();

@result =
    SELECT Product, SUM(Amount) AS TotalSales
    FROM @data
    GROUP BY Product;

OUTPUT @result
TO "adl://mydatalake.azuredatalakestore.net/output/sales_summary.csv"
USING Outputters.Csv();
```

✅ Reads from Data Lake
✅ Aggregates using SQL logic
✅ Writes result back to Data Lake

---

## 🪜 How to Use It — Step-by-Step (Portal)

### 🧩 Step 1️⃣ — Create a Data Lake Store (ADLS Gen1 or Gen2)

You need storage first.

1. Go to **Azure Portal → Create Resource → Data Lake Storage Gen2**
2. Choose **StorageV2 (general purpose)** and **Hierarchical namespace: Enabled**
3. Upload some files (e.g., `sales.csv`)

---

### 🧩 Step 2️⃣ — Create a Data Lake Analytics Account

1. Go to **Azure Portal → Create Resource → Data Lake Analytics**
2. Choose:

   - **Name:** `my-adla`
   - **Resource Group:** existing or new
   - **Data Lake Store:** link the one you just created

3. Click **Review + Create → Create**

---

### 🧩 Step 3️⃣ — Open Data Lake Analytics Studio

You can use:

- **Azure Portal Job UI**
- or **Visual Studio Data Lake Tools Extension**

1. Go to your ADLA resource → **Author → New Job**
2. Paste your U-SQL query
3. Select **Submit Job**

✅ Azure executes your query serverlessly
✅ You can watch progress, logs, and job cost in real-time

---

### 🧩 Step 4️⃣ — Check Job Output

- Output file will be stored back into ADLS.
- You can view results or visualize them in **Power BI / Synapse / Excel**.

---

## 🧠 Example Use Cases

| Use Case                  | Description                                              |
| ------------------------- | -------------------------------------------------------- |
| **Log Analysis**          | Parse TBs of log files for errors                        |
| **ETL**                   | Clean and aggregate raw data before loading into Synapse |
| **Data Exploration**      | Quick ad-hoc queries on massive CSV or JSON              |
| **Machine Learning Prep** | Prepare training datasets (filter, join, aggregate)      |
| **Reporting**             | Summarize data for dashboards                            |

---

## 🔍 How Scaling Works

ADLA has the concept of **Analytics Units (AUs)** —
similar to “compute power per job.”

| Setting                | Description                                  |
| ---------------------- | -------------------------------------------- |
| **AUs**                | Defines how many compute nodes your job gets |
| **Dynamic Scaling**    | ADLA automatically allocates AUs             |
| **Parallel Execution** | Each AU processes data in parallel           |
| **Billing**            | You pay per AU-minute                        |

💡 Example:
A small query = 10 AUs × 2 minutes
→ billed as 20 AU-minutes.

---

## 🔒 Security

| Security Feature                     | Description                                 |
| ------------------------------------ | ------------------------------------------- |
| **Azure AD Authentication**          | Secure login and access                     |
| **RBAC (Role-Based Access Control)** | Control who can submit or cancel jobs       |
| **Access Control Lists (ACLs)**      | File-level permissions in ADLS              |
| **Encryption**                       | Data encrypted at rest and in transit       |
| **Key Vault**                        | For secret management (e.g., database keys) |

---

## 🧩 Integration With Other Services

| Service           | Integration                                  |
| ----------------- | -------------------------------------------- |
| **ADF**           | Use ADF to schedule or orchestrate ADLA jobs |
| **Synapse**       | Move processed data to Synapse for analysis  |
| **Power BI**      | Visualize query outputs                      |
| **Databricks**    | Use ADLA to pre-process data for notebooks   |
| **Azure Monitor** | Monitor job performance and errors           |

---

## 💸 Pricing Summary

| Cost Factor   | Unit            | Description                 |
| ------------- | --------------- | --------------------------- |
| **Compute**   | Per AU-minute   | Based on AUs used           |
| **Storage**   | Separate (ADLS) | Pay for data stored in ADLS |
| **Metadata**  | Minimal         | Job logs and history        |
| **Idle Cost** | None            | Pay only for job runtime    |

🧠 Example:

- Query runs 5 minutes using 20 AUs = **100 AU-minutes**
- Stop paying immediately when job finishes ✅

---

## ⚠️ Note: ADLA vs Modern Tools

Azure Data Lake Analytics was an **early Azure big data engine** (pre-Synapse era).
Today, most workloads have **migrated to Azure Synapse or Databricks**, which are more modern and flexible.

| Feature                | ADLA             | Synapse                      | Databricks             |
| ---------------------- | ---------------- | ---------------------------- | ---------------------- |
| **Language**           | U-SQL            | T-SQL / SparkSQL             | PySpark / SQL / R      |
| **Compute**            | Serverless (AUs) | Serverless + Dedicated Pools | Spark clusters         |
| **Active Development** | Limited          | Yes                          | Yes                    |
| **Best Use Today**     | Legacy workloads | Modern analytics             | Machine learning + ETL |

💡 **In 2025**, ADLA is _still available_, but new projects usually use **Synapse Serverless SQL Pools** or **Databricks** instead.

---

## 🧾 Summary

| Concept                  | Description                                    |
| ------------------------ | ---------------------------------------------- |
| **Service Type**         | Serverless analytics on top of Azure Data Lake |
| **Language**             | U-SQL (SQL + C#)                               |
| **Storage Dependency**   | Azure Data Lake Gen1/Gen2                      |
| **Scaling**              | Automatic with AUs                             |
| **Pricing**              | Pay-per-job                                    |
| **Replaced By (Modern)** | Synapse or Databricks                          |

---

✅ **In one line:**

> **Azure Data Lake Analytics (ADLA)** is a **serverless, pay-per-job query engine** for analyzing data in Azure Data Lake using **U-SQL**, with **no cluster management required**.
