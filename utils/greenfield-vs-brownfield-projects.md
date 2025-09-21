# 🌱 Greenfield vs 🏭 Brownfield Projects

## 1. 🌱 Greenfield Project

- **Definition**: Building something **brand new from scratch**.
- **Analogy**: Like building a house on an empty field (green field 🌱).
- **Characteristics**:

  - No existing codebase.
  - Freedom to choose latest tech stack.
  - Clean design, no legacy baggage.

- **Example**:

  - Creating a **new mobile app** for a startup that didn’t exist before.
  - Building a **fresh microservices platform** in Azure.

---

## 2. 🏭 Brownfield Project

- **Definition**: Working on an **existing system/codebase**, often old or legacy.
- **Analogy**: Renovating a factory (brown, old 🏭) — you must work around existing walls, pipes, and wiring.
- **Characteristics**:

  - Lots of existing code.
  - Must deal with old design choices.
  - May require migrations, integrations, refactoring.

- **Example**:

  - Adding cloud features to a **10-year-old on-prem ERP system**.
  - Migrating a **legacy .NET Framework app** to .NET 8 and Azure.

---

## 💸 Technical Debt

- **Definition**: “The extra cost you pay later for quick-and-dirty coding decisions made earlier.”
- Happens when:

  - Code is rushed without proper tests.
  - Old architecture lingers without refactoring.
  - Tech stack is outdated (e.g., old libraries, unpatched systems).

👉 **Brownfield projects almost always have more technical debt** because they inherit all the old shortcuts, outdated patterns, and “patches” from years of development.

---

## 📝 Question:

❓ _In which of the following choices would you find large amounts of technical debt?_

✅ **Answer** → **Brownfield project**

---

## ⚡ Memory Hack

- **Greenfield** = fresh start, no debt → clean field.
- **Brownfield** = old legacy, lots of debt → muddy/dirty field.
