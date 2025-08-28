# 🧭 Goal

- Move **authentication** to a managed service (Microsoft **Entra External ID** for customer-facing apps).
- Keep your **domain logic** (registrations, event-lock checks, entitlements) living in your **own database/services**.
- Migrate **passwords** without a “big bang” and **preserve referential integrity** across tables.

---

## 🧩 Key Idea: Split “Who you are” from “What you can do”

- **Authentication (Who you are)** → Entra issues tokens.
- **Authorization/Eligibility (What you can do right now)** → your **domain services** and DB decide (registrations, event lock, quotas…).

You **don’t** cram domain logic into the identity provider. You **do** expose it via your APIs and claims.

---

## 🏗️ Target Architecture (at a glance)

```mermaid
flowchart LR
  U[Angular App (Your custom UI)]
  E[Entra External ID (Managed Auth)]
  M[Migration & Business Rules API (Yours)]
  DB[(Legacy SQL: Users + Registrations + Events + ...)]
  API[Your Application APIs]

  U -->|Sign-in / Sign-up (OIDC/OAuth)| E
  E -->|Custom Policy calls (first login + optional pre-checks)| M
  M -->|Password check + business flags| DB
  M -->|OK + claims (flags, legacyUserId)| E
  E -->|ID/Access Tokens (JWT)| U
  U -->|Bearer| API
  API -->|Authorize using claims + live checks| DB
```

---

## 🧱 Data & Identity Model (keep FKs, add mapping)

**Do not drop your Users table.** Evolve it:

- Keep your **Users** row and all **foreign keys** (Registrations, Events, …).
- **Stop** storing/using password _after_ migration (or mark as legacy).
- Introduce a **mapping** table: `UserIdentityMap( LegacyUserId, EntraObjectId, CreatedAt, IsMigrated )`.
- On first successful login (migration), store the **Entra objectId** alongside the **LegacyUserId**.
- Over time, your apps switch from “who is this?” via LegacyUserId → **resolve EntraObjectId** (and vice versa).

**Result:** Referential integrity stays intact; identity becomes **external**.

---

## 🔀 Two Where-to-Check Patterns

### Pattern A — **Pre-Auth Gate** (in Entra External ID)

Use **Custom Policies** to call your **Migration & Rules API** _during sign-in_:

- First login:

  - Validate **username/password** against your SQL (legacy hash).
  - Return flags like `isRegistrationOpen`, `isEventLocked`, `mustAcceptTerms`.
  - Custom policy can **fail the login** or inject **claims**.

- After first login:

  - Password now lives in Entra; **no more legacy password checks**.
  - You may still call your API for **gate flags** if you want pre-auth denial.

**Use when:** you must **block sign-in** early (e.g., user not eligible until some business rule passes).

### Pattern B — **Post-Auth Enforcement** (in your APIs)

Let users sign in (get a token), then your **APIs** enforce business rules:

- The API reads claims (e.g., `legacyUserId`, `roles`).
- The API queries your DB: registrations, locks, quotas.
- If not allowed → return **403** with a helpful message for the UI.

**Use when:** business rules are **contextual** (per action/route), not general “deny all sign-in.”

> Most teams do **Pattern B** for flexibility, and optionally add **Pattern A** for a few global gates (banned user, hard locks).

---

## 🪄 Password Migration (no “reset day”)

- Configure External ID “**Seamless Migration**” (custom policy + REST call):

  - **First** login → External ID calls your **Migration API** with username/password.
  - You check the old password in SQL; if valid → **create** user in External ID (password set there).
  - Store the **Entra objectId** in `UserIdentityMap`.
  - Next logins → fully **cloud-managed**; no more DB password checks.

- After migration window → **remove** the migration step; the password column can be deprecated.

---

## 🧪 Step-by-Step (no code, just actions)

### Phase 0 — Plan

1. Pick **Entra External ID** (CIAM) to support your **custom Angular UI** & migration hook.
2. Inventory: apps, APIs, flows, claims, business rules that block/allow access.

### Phase 1 — Foundation

3. Create External ID tenant; define **custom policies** (sign-in, sign-up, reset).
4. Set **branding** so your Angular keeps its **custom UI** (you host pages; External ID does flows).

### Phase 2 — Mapping & Data

5. Add `UserIdentityMap` and a **new immutable external key** column if needed.
6. Keep Users + relationships untouched; mark password as **legacy**.

### Phase 3 — Migration Bridge

7. Stand up **Migration & Rules API**:

   - Endpoint to **validate legacy password** and return **business flags** (+ legacyUserId).
   - Endpoint to **lookup** legacy user from Entra objectId if needed.

8. Wire the Migration API into External ID **custom policy** (first-login only).

### Phase 4 — App & API Registrations

9. Register **APIs** (define scopes, app roles).
10. Register **clients** (Angular, web, daemons) with correct redirect URIs.
11. Decide where to enforce rules:

- **Pre-auth** gates (rare, simple)
- **Post-auth** in **APIs** (common, flexible)

### Phase 5 — Cutover Gradually

12. Switch **one app** to External ID → users log in → first hit migrates them.
13. Monitor sign-in logs, API denials, and UX.
14. Migrate app-by-app.

### Phase 6 — Consolidate

15. Disable migration step; **passwords** no longer needed in SQL.
16. Update services to rely on **EntraObjectId** via `UserIdentityMap`.
17. Decommission IdentityServer4.

---

## ✅ Best Practices (focused on your realities)

- **Don’t delete your Users table.** Keep FKs; drop password usage later.
- Introduce **`UserIdentityMap`** early; never rewrite all FKs at once.
- Keep **business rules in your domain** (APIs + DB), not in the IdP.
- Use **Authorization Code + PKCE** for Angular; **Client Credentials** for daemons.
- Keep tokens **small**: include `legacyUserId` and required roles/entitlements as claims **only if needed**; prefer API lookups for dynamic rules.
- Enable **MFA**, **Conditional Access**, and **risk checks** in External ID once sign-in is stable.
- Log everything: **sign-in logs** (External ID) + **authorization denials** (your APIs).
- Roll out in **small cohorts**; keep IS4 as **fallback** only if you must (short window).

---

## 🏁 TL;DR

- Move **auth** to **Entra External ID** (managed, supports your custom UI).
- Keep **domain logic** (registrations, locks) in **your APIs + SQL**.
- Use a **seamless migration** step to validate old passwords **once**, then stop using the password column.
- Preserve FKs with a **User ↔ Entra mapping** table; evolve your system without a risky rewrite.
