# 🧪 AZ-400 Topic 5: Design and Implement Testing

📚 Objective: Master automated testing integration within your CI/CD pipelines in Azure DevOps — including unit tests, integration tests, load tests, code coverage, quality gates, and test reporting.

---

## 🧱 Core Knowledge You Must Master

### 🔹 1. Why Testing in DevOps Matters

> Testing is not a "QA thing" anymore — it's a **first-class citizen** in DevOps.
> A true CI/CD pipeline ensures code is **tested automatically and continuously**, before it’s ever promoted.

💡 Testing is your gatekeeper. No test? No deploy.

---

### 🔹 2. Types of Tests to Automate in Pipelines

| Test Type                  | Purpose                                                  | When to Run                |
| -------------------------- | -------------------------------------------------------- | -------------------------- |
| **Unit Tests**             | Test individual functions/methods in isolation           | Every build                |
| **Integration Tests**      | Validate interaction between components or APIs          | After build, in Dev        |
| **UI/Functional Tests**    | Simulate user behavior via Selenium, Playwright, Cypress | In staging/test            |
| **Load/Performance Tests** | Stress test performance under load                       | On demand or pre-prod      |
| **Security Tests**         | SAST, dependency scanning                                | Pre-deploy or nightly runs |

✅ You must know **where each type belongs** in the pipeline stages.

---

### 🔹 3. Running Unit & Integration Tests in Azure DevOps

Typical test tasks you’ll use:

```yaml
- task: DotNetCoreCLI@2
  inputs:
    command: "test"
    projects: "**/*Tests.csproj"
    arguments: '--configuration Release --collect:"Code Coverage"'
```

✅ Use language-specific test runners:

- `.NET` ➝ `dotnet test`
- `Python` ➝ `pytest`, `unittest`
- `Node.js` ➝ `jest`, `mocha`
- `Java` ➝ `Maven`, `JUnit`

---

### 🔹 4. Publishing and Analyzing Test Results

| Step                  | Task                            |
| --------------------- | ------------------------------- |
| Run tests             | `DotNetCoreCLI@2` or `VSTest@2` |
| Publish test results  | `PublishTestResults@2`          |
| Publish code coverage | `PublishCodeCoverageResults@1`  |

✅ Supported formats: `JUnit`, `TRX`, `Cobertura`, `JaCoCo`, `LCOV`

🧠 Published results:

- Show up in **Azure DevOps test tab**
- Help enforce **quality gates**
- Give you **failures at-a-glance**, even across builds

---

### 🔹 5. Test Coverage Metrics

| Metric             | Description                           |
| ------------------ | ------------------------------------- |
| Line coverage      | % of code lines executed during tests |
| Branch coverage    | % of control flow paths covered       |
| Statement coverage | % of code statements run              |

✅ Tools:

- .NET ➝ `coverlet`, `Visual Studio Coverage`, `reportgenerator`
- Java ➝ `JaCoCo`
- JS ➝ `Istanbul`, `nyc`
- Python ➝ `coverage.py`

💡 You can **fail builds** if coverage drops below threshold.

---

### 🔹 6. Quality Gates and Validation Policies

| Policy                | Use Case                          |
| --------------------- | --------------------------------- |
| Min % Code Coverage   | Prevent merge if < 80%            |
| Required test success | Fail build/release if tests fail  |
| Approval gates        | Delay deployment until tests pass |
| Static code analysis  | Enforce code rules/linting        |

✅ Enforce via **branch policies + pipeline conditions**.

---

### 🔹 7. Test Environments and Isolation

| Concept                 | Why It Matters                                                  |
| ----------------------- | --------------------------------------------------------------- |
| Disposable environments | Use infra-as-code (e.g., Bicep, Terraform) to spin up test envs |
| Parallel test jobs      | Speed up total test time                                        |
| Data mocking/seeding    | Ensure repeatable integration tests                             |
| Containerized tests     | Use Docker to isolate test environments                         |

✅ Your test stage must be **idempotent**, **repeatable**, and **portable**.

---

### 🔹 8. Load and Performance Testing

Azure-native options:

- 🔹 **Azure Load Testing** – managed JMeter at scale
- 🔹 **Visual Studio Load Test** (deprecated)
- 🔹 3rd party: JMeter, k6, Locust

✅ Run these only on staging/pre-prod, not on every commit.
✅ Validate **latency, throughput, error rate**, and fail if thresholds breached.

---

### 🔹 9. UI & End-to-End Testing

| Tool       | Used For                    |
| ---------- | --------------------------- |
| Selenium   | Browser automation          |
| Playwright | Fast, reliable UI tests     |
| Cypress    | Frontend JS testing         |
| Puppeteer  | Headless Chrome-based tests |

✅ Run these in **post-build jobs**, often in **staging** environment.
Use **headless mode** in pipeline agents.

---

### 🔹 10. Test Reporting and Feedback Loops

- Show test failures with tracebacks in DevOps pipeline UI
- Link failures to commits or pull requests
- Comment on PRs with test pass/fail status
- Export test data to Azure Monitor or App Insights if needed

---

## 🧠 Summary of What You Must Be Able to Do

✅ You can:

- Add **unit, integration, UI, and load tests** to the right pipeline stage
- Publish **test results** and **code coverage** in Azure DevOps
- Enforce test quality via **branch policies** and **gates**
- Run test steps in YAML or Classic pipelines using language-specific tools
- Understand test isolation, mocking, and environment setup
- Fail builds or block deployments if tests or metrics fall below threshold

---

## 🧪 DevOps Interview Questions – Testing

Here’s what you might be asked (and how to shine):

---

### 💬 Q1. What types of tests do you include in your pipeline?

**Answer:**

> I include unit tests during the build stage to catch logic bugs early, integration tests in the Dev environment to validate service interaction, and end-to-end/UI tests in Staging. For high-traffic apps, I also add performance tests before Prod.

---

### 💬 Q2. How do you ensure test failures are caught before release?

**Answer:**

> I configure pipelines to **fail builds** if any tests fail, and require test pass status as a **branch policy** before merging. I also gate releases with test checks and deploy only if tests succeed in lower environments.

---

### 💬 Q3. How do you publish and visualize test results in Azure DevOps?

**Answer:**

> I use `PublishTestResults` and `PublishCodeCoverageResults` tasks in the YAML. These show test run history in the DevOps UI, help track flaky tests, and support trend analysis.

---

### 💬 Q4. How do you handle environment-specific integration tests?

**Answer:**

> I use infrastructure-as-code to provision disposable test environments per run, seed test data, and clean up afterward. This guarantees isolation and prevents test pollution.

---

### 💬 Q5. How would you prevent UI tests from becoming flaky?

**Answer:**

> Use reliable tools like Playwright with smart wait logic, avoid hardcoded sleeps, mock external APIs, and containerize tests for consistency. Run in headless mode in agents.

---

### 💬 Q6. What tools do you use to monitor test quality over time?

**Answer:**

> Azure DevOps built-in dashboards show test trends. For deeper insights, I export test metrics to Azure Monitor or integrate with tools like SonarQube for test coverage tracking.

---

## 🔚 Final Thoughts

✔ Testing isn’t an afterthought — it’s a **release gate, a quality signal, and a safety net**.
✔ A DevOps engineer must know how to **plug in automated testing**, **fail fast**, and **protect prod**.
