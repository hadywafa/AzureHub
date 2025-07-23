# 🎯 AZ-400 Topic 1: Design and Implement Source Control

📚 Objective: Master Git-based source control practices, repository structures, branching strategies, security policies, and how all of this integrates into DevOps automation and team workflows.

---

## 🧱 Core Knowledge You Must Master

### 🔹 1. **Distributed vs Centralized Source Control**

| Concept                                                 | You Should Know                                                                                  |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| Centralized                                             | Uses a central server (e.g., TFVC, SVN). Simpler but less resilient.                             |
| Distributed                                             | Git. Every developer has a full copy. Enables offline work, fast branching, decentralized power. |
| ✅ In Azure DevOps, Git is the default. TFVC is legacy. |                                                                                                  |

---

### 🔹 2. **Git Core Concepts**

| Feature             | What You Must Know                             |
| ------------------- | ---------------------------------------------- |
| Repository          | `git init`, `.git/` directory structure        |
| Working Directory   | Where changes happen                           |
| Staging Area        | `git add` prepares for commit                  |
| Commits             | `git commit`, unique hashes                    |
| HEAD                | Points to current snapshot                     |
| Branching & Merging | Fast in Git, supports multiple parallel tracks |
| Merge Conflicts     | How to resolve manually                        |
| Rebase              | Rewriting history vs merge                     |

✅ Understand how Git tracks and rewrites changes using DAG (Directed Acyclic Graph).
✅ Know `revert`, `reset`, `checkout`, and `stash`.

---

### 🔹 3. **Branching Strategies**

| Strategy                    | When to Use                                                                                  |
| --------------------------- | -------------------------------------------------------------------------------------------- |
| **Git Flow**                | Large teams, structured releases. Has `develop`, `release/*`, `hotfix/*`.                    |
| **GitHub Flow**             | Simpler: Just `main` + `feature/*`. Ideal for CI/CD.                                         |
| **Trunk-Based Development** | All commits to `main`. Use **feature flags** to disable WIP. High-performing teams use this. |

✅ Know how to implement each using **branch naming policies** and **PR validation**.

---

### 🔹 4. **Pull Requests & Code Review Policies**

| What to Master               | Why It Matters                                        |
| ---------------------------- | ----------------------------------------------------- |
| Pull Request process         | Create PR, assign reviewers, comment, approve         |
| Azure DevOps branch policies | Require approval, build validation, linked work items |
| Auto-complete PR             | Enables clean merge when checks pass                  |
| Enforcing policies           | Protect against direct pushes, deletions              |

✅ These policies ensure **code quality and auditability**. Essential in regulated environments.

---

### 🔹 5. **Repository Design (Monorepo vs Polyrepo)**

| Design       | Pros                                                    | Cons                                 |
| ------------ | ------------------------------------------------------- | ------------------------------------ |
| **Monorepo** | Easier to share libs, single versioning, atomic changes | Gets big, tooling must scale         |
| **Polyrepo** | Cleaner per-service repo, flexible scaling              | Duplication, cross-repo changes hard |

✅ In DevOps, **monorepo is fine** if you automate builds and have dependency management in place.

---

### 🔹 6. **Security & Access Management**

| What to Know         | Best Practices                                              |
| -------------------- | ----------------------------------------------------------- |
| Role-based access    | Azure DevOps: Reader, Contributor, Admin                    |
| Protect `main`       | Use branch policies, disable force push, limit deletions    |
| Secret scanning      | Ensure credentials aren’t checked in                        |
| Git history clean-up | Use `filter-branch` or `BFG` to remove secrets from history |

✅ Always lock down sensitive branches. Set permissions per repo and per branch level.

---

### 🔹 7. **Source Control in CI/CD Triggers**

| Feature         | Purpose                                                       |
| --------------- | ------------------------------------------------------------- |
| Branch filters  | Trigger pipeline on `main` or `feature/*` only                |
| Path filters    | Only trigger if code under `/src` changes                     |
| Version tagging | Use `git tag` for release artifacts                           |
| Git in YAML     | Use `checkout`, `fetchDepth`, `submodules` in Azure Pipelines |

✅ Know how to control pipeline runs based on **source control activity**.

---

## 🧠 Summary of What You Must Be Able to Do

✅ You can:

- Choose a suitable **branching strategy** for your team
- Enforce **PR reviews**, **build validations**, and **commit policies**
- Structure a repo (monorepo or polyrepo) based on org size and build tooling
- Configure **permissions** and **access controls** on branches and repos
- Use **Git concepts** (merge, rebase, revert) to maintain clean history
- Use **Git triggers** to start build/release pipelines in DevOps

---

## 🧪 DevOps Interview Questions – Source Control

Here are real-world interview-style questions (and how to approach them):

---

### 💬 Q1. What branching strategy do you recommend in a fast-paced CI/CD team?

**Answer:**

> I prefer Trunk-Based Development with feature flags. This minimizes merge conflicts and keeps deployment fast and continuous. We use short-lived branches and enforce policies to keep `main` clean.

---

### 💬 Q2. How do you ensure code quality and security in source control?

**Answer:**

> Through branch policies: mandatory pull requests, at least 2 reviewers, successful build validation, and linked work items. We also use secret scanning and disallow direct pushes to `main`.

---

### 💬 Q3. What are the trade-offs between monorepo and polyrepo?

**Answer:**

> Monorepo simplifies dependency management and atomic commits across services but requires strong tooling. Polyrepo isolates services better but makes shared code management harder. I choose based on team size and release independence.

---

### 💬 Q4. How do you integrate Git with Azure Pipelines?

**Answer:**

> I configure triggers in the pipeline YAML file to watch specific branches and paths. I use `checkout: self`, set fetchDepth to 1 for performance, and handle submodules if needed.

---

### 💬 Q5. What’s the difference between `merge` and `rebase`?

**Answer:**

> `merge` combines histories and creates a new commit, keeping branches intact. `rebase` rewrites commit history linearly, useful for clean mainline history. Rebase is great before merging to main, but avoid on shared branches.

---

### 💬 Q6. How do you recover from accidentally committed secrets?

**Answer:**

> First, revoke the exposed secret. Then, remove it using tools like BFG or `git filter-branch`. Finally, force-push the cleaned history (if allowed), and update team members to re-clone.

---

### 💬 Q7. What tools or best practices do you follow for PR reviews?

**Answer:**

> Use Azure DevOps PR templates, assign code owners, and automate checks like build validation and linting. Encourage smaller PRs for easier review and faster feedback.

---

## 🔚 Final Thoughts

✔ You don’t just need to “know Git” — you need to know how **Git connects to team workflows, build pipelines, security policies, and collaboration**.
✔ Focus on real-world discipline: clean commit history, smart branch use, PR reviews, and trigger management.
