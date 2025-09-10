# 🗂️ What is a DACPAC?

**DACPAC = Data-tier Application Package!**

- A **single `.dacpac` file** (basically a zipped bundle of XML + schema definitions).
- Contains the **schema of a SQL Server / Azure SQL Database** (tables, views, stored procedures, functions, etc.).
- It does **not** contain the actual data (that would be a BACPAC).

👉 Think of it as:

- **DACPAC** = “blueprint of your database schema.”
- **BACPAC** = “blueprint + the actual data.”

---

## 🛠️ Why is it Important?

- 📦 Lets you **version control** your database schema (like you do code).
- 🚀 Used in **CI/CD pipelines** to deploy changes to SQL databases.
- ⚡ Can perform **incremental updates**: compares schema in `.dacpac` vs target DB → generates a **diff script** → applies changes.
- ✅ Ensures **consistency** across environments (dev, test, prod).

---

## 🔹 Real-World Example

You have an **Azure DevOps pipeline** for your app + database:

1. Developer changes a SQL table (`ALTER TABLE Customers ADD Email NVARCHAR(100)`).
2. They update the schema in the **SQL Project** (in Visual Studio).
3. Build pipeline compiles the project into a `.dacpac` file.
4. Release pipeline deploys that `.dacpac` into **Azure SQL Database** using `SqlPackage.exe` or the Azure DevOps task.

---

## 🔹 Key Tools

- **Visual Studio SQL Server Data Tools (SSDT)** → used to create SQL Projects and build `.dacpac`.
- **SqlPackage.exe** → command-line tool to deploy or extract `.dacpac`.
- **Azure DevOps Task** → _Azure SQL Database deployment_ task can consume `.dacpac`.

---

## 🔹 Hands-On Example

### Build Step: Generate DACPAC

From a SQL Project:

```bash
msbuild MyDatabaseProject.sqlproj /p:Configuration=Release
```

Output: `bin/Release/MyDatabase.dacpac`

---

### Release Step: Deploy DACPAC

Using `SqlPackage.exe`:

```bash
SqlPackage.exe /Action:Publish `
  /SourceFile:"MyDatabase.dacpac" `
  /TargetServerName:"myserver.database.windows.net" `
  /TargetDatabaseName:"MyAppDB" `
  /TargetUser:"sqladmin" `
  /TargetPassword:"P@ssword123"
```

👉 This will **compare** schema in the DACPAC vs target DB and apply changes.

---

## 🔹 DACPAC vs BACPAC

| Package    | Contains                                 | Use Case                                                     |
| ---------- | ---------------------------------------- | ------------------------------------------------------------ |
| **DACPAC** | Schema only (tables, views, procs, etc.) | Schema migrations, CI/CD pipelines                           |
| **BACPAC** | Schema + Data                            | Database export/import, backups, moving data between servers |

---

## ✅ TL;DR

- **DACPAC = zipped file with DB schema.**
- Built from SQL projects or extracted from DB.
- Used in **Azure DevOps pipelines** to deploy schema changes safely.
- `SqlPackage.exe` = main tool to deploy.
- **DACPAC → Schema only**, **BACPAC → Schema + Data**.

---

⚡ Exam Tip: If you see a question like:

- _“How to automate schema deployments to Azure SQL?”_ → Answer: **Use DACPAC in Azure Pipelines with SqlPackage.exe or Azure SQL Database deployment task.**

## 📚 References

- <https://learn.microsoft.com/en-us/azure/devops/pipelines/targets/azure-sqldb?view=azure-devops&tabs=yaml>
- <https://learn.microsoft.com/en-us/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-ver16>
- <https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/reference/sql-azure-dacpac-deployment-v1?view=azure-pipelines>
