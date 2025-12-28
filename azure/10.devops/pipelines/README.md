# Azure Pipelines Mastery Roadmap (From Zero → Architect Level)

hady please master ci cd pipeline as it the most important thing in your new e&
and then you need to create cicd for your logging solution and try azure devops.

## 1. Core Foundations (Non-Negotiable)

These are the **laws of physics** of Azure Pipelines. If any of these are weak, everything else breaks.

### 1.1 Pipeline Architecture

- What actually happens when a pipeline runs
- Pipeline service vs agent
- Job isolation and why state is lost
- Hosted vs self-hosted agents
- Agent capabilities and demands

### 1.2 YAML Pipeline Anatomy

- Pipeline root structure
- Stages vs Jobs vs Steps
- Script tasks vs built-in tasks
- Task lifecycle and execution order
- What “checkout: self” really does

### 1.3 Evaluation Model (CRITICAL)

- Compile-time vs runtime
- `${{ }}` vs `$( )` vs `$[ ]`
- When variables exist and when they don’t
- Why most “variable bugs” happen

---

## 2. Variables, Parameters & Data Flow (Deep Internals)

This category alone separates **junior** from **senior** engineers.

### 2.1 Variables (Complete)

- Variable scopes and precedence
- System vs user variables
- Environment variables mapping
- Variable templates
- Debugging variable resolution

### 2.2 Parameters (Advanced Usage)

- Strong typing (string, boolean, object)
- Object and array parameters
- Template-driven pipelines
- Dynamic job/stage generation
- Parameter-based pipeline branching

### 2.3 Output Variables & Data Passing

- Job isolation model
- `##vso` internals
- Cross-job vs cross-stage communication
- `dependencies` vs `stageDependencies`
- Anti-patterns and best practices

---

## 3. Conditions, Expressions & Control Flow

This is where pipelines become **logic engines**.

### 3.1 Conditions

- Default conditions
- Custom runtime conditions
- Logical operators
- Expression functions (`eq`, `and`, `or`, `startsWith`)
- Short-circuit behavior

### 3.2 Expressions Deep Dive

- Runtime expressions `$[ ]`
- Compile-time expressions `${{ }}`
- Variable dereferencing pitfalls
- Expression evaluation order

### 3.3 Looping & Dynamic Pipelines

- `each` loops
- Object iteration
- Conditional insertion of steps/jobs
- Environment fan-out patterns

---

## 4. Templates & Modularization (Enterprise Design)

This is how **large companies** build pipelines.

### 4.1 Template Types

- Step templates
- Job templates
- Stage templates
- Variable templates

### 4.2 Template Composition

- `extends` vs `template`
- Parameter inheritance
- Template contracts
- Template versioning strategies

### 4.3 Real-World Template Patterns

- Microservice pipelines
- Monorepo pipelines
- Multi-environment templates
- Shared DevOps platform repos

---

## 5. Agents & Execution Infrastructure

This is where **performance and cost** decisions live.

### 5.1 Hosted Agents

- Microsoft-hosted pools
- Image versions
- Tool caching
- Cold start behavior

### 5.2 Self-Hosted Agents

- Agent architecture
- Security boundaries
- Scaling strategies
- Maintenance pitfalls

### 5.3 VMSS Agent Pools (Advanced)

- Elastic scaling model
- Job queue behavior
- Image baking strategies
- Cost optimization

---

## 6. CI: Build Pipelines (Production Grade)

### 6.1 Source Control Integration

- Triggers (CI, PR, path filters)
- Branch policies
- Shallow clones
- Multi-repo checkout

### 6.2 Build Optimization

- Caching strategies
- Artifact staging
- Parallel jobs
- Matrix builds

### 6.3 Artifact Management

- Pipeline artifacts vs build artifacts
- Publishing strategies
- Artifact retention
- Cross-pipeline consumption

---

## 7. CD: Deployment Pipelines (Very Important)

This is where Azure Pipelines shines.

### 7.1 Deployment Jobs

- Deployment job vs normal job
- Environments
- Resource types (VM, Kubernetes, App Service)
- Deployment history

### 7.2 Deployment Strategies

- RunOnce
- Rolling
- Canary
- Blue-Green
- Rollback mechanics

### 7.3 Approvals & Gates

- Pre-deployment approvals
- Post-deployment approvals
- Manual interventions
- Timeout handling

---

## 8. Environments & Infrastructure Awareness

### 8.1 Environments

- Logical vs physical environments
- Environment variables
- Resource health tracking

### 8.2 Infrastructure as Code Integration

- ARM deployments
- Bicep pipelines
- Terraform pipelines
- State handling strategies

---

## 9. Security & Secrets (Enterprise Critical)

### 9.1 Secrets Handling

- Secret variables
- Variable groups security
- Masking behavior
- Common leakage mistakes

### 9.2 Azure Key Vault Integration

- Service connections
- Runtime secret injection
- Secret rotation patterns

### 9.3 Permissions & RBAC

- Pipeline permissions
- Environment permissions
- Service connection security

---

## 10. Logging, Debugging & Observability

### 10.1 Logging Internals

- Log folding
- Sections
- `##vso` commands
- Error classification

### 10.2 Debugging Pipelines

- `system.debug`
- Diagnosing variable issues
- Agent diagnostics
- Rerun failed jobs

---

## 11. Advanced Scenarios (Architect Level)

### 11.1 Multi-Project Pipelines

- Cross-project artifacts
- Service connections
- Governance boundaries

### 11.2 Hybrid & Multi-Cloud

- Azure + AWS pipelines
- On-prem deployments
- Secure hybrid agents

### 11.3 Compliance & Governance

- Auditing pipelines
- Approval enforcement
- Change control patterns

---

## 12. Interview & Real-World Mastery

### 12.1 Common Interview Scenarios

- “Why is my variable empty?”
- “Why does this condition not work?”
- “How do you share data across jobs?”
- “How do you secure secrets?”

### 12.2 Anti-Patterns

- Overusing variables
- Hardcoding environment logic
- Monolithic pipelines
- Template abuse

---

## How We Should Proceed (Recommended)

**Best path to mastery:**

1. Start with **Evaluation Model**
2. Then **Variables + Parameters + `##vso`**
3. Then **Conditions & Expressions**
4. Then **Templates**
5. Then **Deployment jobs & strategies**
6. Then **Security & governance**

I recommend this exact next step:

> **Next Topic:** > **Azure Pipelines Evaluation Model (Compile-time vs Runtime) — the root of all bugs**
