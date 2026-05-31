# Notes

## Note 1 -AU Roles and administrators

> there is no dedicated _Administrative Unit Administrator_ in Roles and administrators in AU

![[notes-1780248496024.webp]]

Many people think:

```text
Administrative Unit
↓
Administrative Unit Administrator
```

exists as a dedicated role.

Actually Microsoft does:

```text
Role
+
Administrative Unit Scope
```

Example:

```text
User Administrator
scoped to Dev-AU
```

which effectively creates:

```text
Dev-AU Administrator
```

without having a role literally called that.

For your lab, assign:

```text
User Administrator
Groups Administrator
```

to:

```text
devadmin
```

inside Dev-AU, then sign in as devadmin and you'll immediately understand the power of Administrative Units.

## Note 2 - **Global Administrator ≠ Azure Resource Administrator**

![[notes-1780243936735.webp]]

![[notes-1780247168819.webp]]

This is one of the most common Azure beginner mistakes.

**Global Administrator ≠ Azure Resource Administrator**

You are mixing:

```text
Microsoft Entra ID Roles
```

with

```text
Azure RBAC Roles
```

---

### What you currently have

You made:

```text
hady@hadywafa.com
```

a:

```text
Global Administrator
```

inside Entra ID.

This gives you permission to manage:

- ✅ Users
- ✅ Groups
- ✅ Administrative Units
- ✅ MFA
- ✅ Conditional Access
- ✅ Domains
- ✅ Entra Roles

But it does **NOT** automatically give:

- ❌ Owner
- ❌ Contributor
- ❌ User Access Administrator

on Azure subscriptions.

### Why?

Because when Azure created the subscription, it likely attached it to the tenant, but the subscription owner is:

```text
admin@hadywafa.onmicrosoft.com
```

or another billing identity.

Remember:

```text
Entra Global Administrator
≠
Azure Subscription Owner
```

![[notes-1780247950948.webp]]

![[notes-1780247972227.webp]]

---

#### Fix (2 minutes)

![[notes-1780248218796.webp]]

Login as:

```text
admin@hadywafa.onmicrosoft.com
```

Then:

```text
Subscriptions
→ Azure subscription 1
→ Access Control (IAM)
→ Role Assignments
→ Add
→ Add role assignment
```

Assign:

```text
Role:
Owner
```

to:

```text
hady@hadywafa.com
```

---

#### Alternative

![[notes-1780248383486.webp]]

Microsoft has a setting called:

```text
Global Administrator can elevate access
```

Go to:

```text
Portal
→ Entra ID
→ Properties
→ Access management for Azure resources
```

Enable:

```text
Yes
```

This gives the current Global Administrator:

```text
User Access Administrator
```

at root scope.

Then:

```text
Subscriptions
→ Azure subscription 1
→ IAM
```

and assign yourself:

```text
Owner
```

---

## Note 3 - User Access Administrator Limits

![[notes-1780244968248.webp]]

---

## Note 4 - Create Subscription

![[_notes-1780253175714.webp]]

### Azure Billing Hierarchy

```text
Billing Account
│
├── Billing Profile
│     │
│     ├── Invoice Section
│     │      │
│     │      ├── Subscription DEV-SUB
│     │      └── Subscription PROD-SUB
│     │
│     └── Invoice Section
│
└── Billing Profile
```

---

### 1. Billing Account

In your screenshot:

```text
Billing Account:
Hady Wafa
(b57b372b-526a-464b-...)
```

Think of it as:

```text
The legal customer
```

Microsoft sees:

```text
Hady Wafa
Visa ****4624
Address in UAE
```

as one customer.

---

#### Real Company Example

```text
Microsoft Corporation
```

might have:

```text
Billing Account
```

and underneath:

```text
Middle East
Europe
US
Asia
```

billing structures.

---

#### Can you create another Billing Account?

For a personal lab:

```text
Normally NO
```

and there is no reason to.

You already have:

```text
1 Billing Account
```

which is perfect.

---

### 2. Billing Profile

Your screenshot:

```text
Billing Profile:
Hady Wafa
(IA47-DJOM-BG7-PGB)
```

Think of it as:

```text
A payment bucket
```

It determines:

```text
Credit Card
Currency
Tax
Billing Cycle
```

---

Example:

```text
Billing Account
│
├── Personal Profile
│     AED
│
├── Company Profile
│     USD
│
└── Client Profile
      EUR
```

Each profile can generate separate invoices.

---

For your lab:

```text
Use the existing one
```

---

### 3. Invoice Section

This is what Azure is asking you to choose.

You currently have:

```text
Hady Wafa
(7abb957a-...)
```

and

```text
Hady Wafa
(84cdc88f-...)
```

---

Invoice Sections are simply:

```text
Cost separation containers
```

inside a Billing Profile.

---

#### Example

A company might have:

```text
Invoice Section:
Development

Invoice Section:
Production

Invoice Section:
Security
```

All receive separate invoices.

---

### What should YOU choose?

Honestly:

```text
Pick either one.
```

For a personal lab:

```text
Invoice Section
=
almost irrelevant
```

because everything hits:

```text
same credit card
same billing profile
same billing account
```

---

### Recommended Enterprise-Like Setup

For learning Azure Governance:

```text
Billing Account
│
└── Billing Profile
      │
      ├── Invoice Section: DEV
      │       └── DEV-SUB
      │
      └── Invoice Section: PROD
              └── PROD-SUB
```

If Azure lets you create Invoice Sections later, that's the cleanest setup.

---
