# Architecture

## Tenant

You have:

```text
Tenant:
hadywafa.onmicrosoft.com

Custom Domain:
hadywafa.com

Users:
admin@hadywafa.onmicrosoft.com
hady@hadywafa.com

Microsoft 365 Business Basic:
1 license

Entra ID P1 Trial:
25 licenses
30 days
```

This is enough to build a surprisingly realistic enterprise lab.

---

## My Recommended Final Design

### 🔴 Account 1 - Break Glass Account

```text
admin@hadywafa.onmicrosoft.com
```

Roles:

```text
Global Administrator
```

License:

```text
No M365
No P1
```

Purpose:

```text
Emergency account
Tenant recovery
Billing
Domain management
```

Never use it daily.

Enable:

```text
MFA
```

---

### 🟢 Account 2 - Daily Account

```text
hady@hadywafa.com
```

Roles:

```text
Global Administrator
```

Licenses:

```text
Microsoft 365 Business Basic
Entra ID P1
```

Use this for:

```text
Azure Portal
Entra Portal
Microsoft Learn
Certifications
Outlook
Teams
Labs
```

This becomes your primary cloud identity.

---

## Setup

### 1. Create Lab Users

Create:

```text
devadmin@hadywafa.com
dev1@hadywafa.com
dev2@hadywafa.com

prodadmin@hadywafa.com
prod1@hadywafa.com
prod2@hadywafa.com

manager1@hadywafa.com
auditor1@hadywafa.com
```

Total:

```text
8 lab users
```

No M365 license needed.

Assign P1 only when testing P1 features.

---

### 2. Create Groups

#### Dev

```text
Dev-Admins
Dev-Contributors
Dev-Readers
```

#### Production

```text
Prod-Admins
Prod-Contributors
Prod-Readers
```

#### Operations

```text
Security-Team
Auditors
Managers
```

---

### Administrative Units

This is where the fun starts.

#### AU #1

```text
Dev-AU
```

Contains:

```text
devadmin
dev1
dev2

Dev-Admins
Dev-Contributors
```

Assign:

```text
Administrative Unit Administrator
```

to:

```text
devadmin
```

---

#### AU #2

```text
Prod-AU
```

Contains:

```text
prodadmin
prod1
prod2

Prod-Admins
Prod-Contributors
```

Assign:

```text
Administrative Unit Administrator
```

to:

```text
prodadmin
```

---

### Azure Subscriptions

Create:

```text
Subscription
```

Then:

```text
RG-DEV
RG-PROD
RG-SHARED
```

---

### RBAC

Assign:

### Dev

```text
Dev-Admins
```

to:

```text
Contributor
```

on:

```text
RG-DEV
```

Only.

---

### Production

Assign:

```text
Prod-Admins
```

to:

```text
Contributor
```

on:

```text
RG-PROD
```

Only.

---

## Labs

### ✅ Lab 1 - Administrative Units

> Prove user-administration for Dev-AU can't manage any users in Prod-AU

![[notes-1780243627059.webp]]

![[architectures-1780244781654.webp]]
![[architectures-1780244805123.webp]]

---

### Lab 2

Dynamic Groups

Example:

```text
Department=Dev
```

Automatically joins:

```text
Dev-Users
```

---

### Lab 3

Conditional Access

Example:

```text
Require MFA for Production Users
```

---

### Lab 4

Named Locations

Example:

```text
Allow UAE only
```

---

### Lab 5

Group-Based Licensing

Assign P1 to a group.

Watch users inherit licenses automatically.

---

### Lab 6

Authentication Methods

```text
Authenticator
FIDO2
SMS
```

---

## Azure Governance Labs

Create:

```text
Management Group
 ├── Development
 └── Production
```

Then:

```text
Subscription
```

under Production.

Practice:

```text
RBAC
Policy
Tags
Locks
Budgets
```

---

## Final Architecture

```text
Tenant
│
├── admin@hadywafa.onmicrosoft.com
│      Global Admin
│      Emergency Account
│
├── hady@hadywafa.com
│      Global Admin
│      M365
│      P1
│
├── Dev-AU
│      ├── devadmin
│      ├── dev1
│      └── dev2
│
├── Prod-AU
│      ├── prodadmin
│      ├── prod1
│      └── prod2
│
└── Azure
       ├── RG-DEV
       ├── RG-PROD
       └── RBAC Assignments
```
