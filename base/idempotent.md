# 🔁 What Does "Idempotent" Mean?

In software and systems design, an **idempotent operation** is one that can be **executed multiple times** without changing the result **beyond the initial application**.

---

## 🧠 Real-World Analogy:

Imagine a button that turns off a light:

- Press it once → light turns off ✅
- Press it again → light stays off ✅
- Press it 100 times → light still off ✅

The **state doesn’t change** after the first successful action. That’s idempotency.

---

## 💻 In Tech Terms:

- **HTTP methods**:

  - `GET`, `PUT`, and `DELETE` are **idempotent**
  - `POST` is **not** — it creates a new resource each time

- **APIs**:  
  An idempotent API call ensures that **retries won’t cause duplication or corruption**. This is critical in distributed systems and SRE patterns.

- **Infrastructure as Code (IaC)**:  
  Tools like Terraform aim for idempotency — running the same plan twice shouldn’t change your infrastructure.

---

## 🔧 Why It Matters in Your Context:

- **Retry logic**: You can safely retry failed operations without side effects.
- **Circuit breakers**: Idempotent calls help maintain system stability under failure.
- **Portfolio projects**: Demonstrating idempotent design in your modules (e.g., typed clients, storage provisioning, API calls) shows architectural maturity.
