# 🆚 Billing Notes

## Note 1

> Payment methods and credits are only available for billing accounts, billing profiles, and pay-as-you-go subscriptions. Please change to a supported scope.

## Note 2

> Changing country/region
> for existing billing account
> is not supported.

## Note 3 - Delete Tenant

A user with the Global Administrator role can delete the tenant, but there are some conditions.

### Requirements

The account deleting the tenant should be:

```text
Global Administrator
```

and ideally:

```text
Tenant Creator
```

> If you are a **Global Administrator** in a tenant, you can typically delete the tenant even if someone else originally created it.

---

### Before Azure allows deletion

Azure runs validation checks.

You must remove or satisfy all blockers such as:

```text
❌ Active subscriptions
❌ Azure resources
❌ Enterprise Applications
❌ App Registrations
❌ Custom domains
❌ Other users (sometimes)
❌ Azure AD B2C configuration
❌ Management groups
❌ Marketplace subscriptions
```

If any blocker exists, Azure will show:

```text
Delete Tenant
→ Validation Failed
```

with a list of exactly what is preventing deletion.

---

### How to check

Go to:

```text
portal.azure.com
→ Microsoft Entra ID
→ Manage Tenants
→ Select Tenant
→ Delete Tenant
```

If you are Global Admin, you should see the button.

---

### Important distinction

Many people confuse these:

```text
Delete Subscription
```

and

```text
Delete Tenant
```

They are different.

#### Delete Subscription

Removes:

```text
VMs
Storage
AKS
Databases
```

Billing stops.

#### Delete Tenant

Removes:

```text
Users
Groups
Applications
Entra ID
Entire directory
```

The whole Entra directory disappears.

---

### For your case

Since you said:

```text
No resources
No workloads
No need for this account
```

As Global Admin, you can likely:

1. Cancel the subscription.
2. Wait for it to become disabled/canceled.
3. Go to Delete Tenant.
4. Resolve any validation warnings.
5. Delete the tenant.

After that, create a fresh UAE-based Azure account.

Before deleting, I'd still recommend checking:

```text
Entra ID
→ App Registrations
→ All Applications
```

because sometimes people forget old service principals, app registrations, or Azure DevOps integrations that block tenant deletion. If the tenant is from 2019, there may be a few leftover objects even if no resources exist today.
![[notes-1780222215623.webp]]

## Note 4 - Pay-as-you-go vs Azure free account

![[notes-1780227602027.webp]]
Here’s the difference in simple terms:

**Azure Free Account**

- Designed for new users to explore and learn.
- Includes **$200 credit for the first 30 days** to try any service.
- Offers **20+ popular services free for 12 months** and **65+ services always free**.
- No charges unless you upgrade to Pay-As-You-Go after credit or 30 days expire.
- Great for proof of concept and learning without risk of unexpected charges.

**Pay-As-You-Go**

- No initial credit, but you can start building production workloads immediately.
- Same free services (20+ for 12 months, 65+ always free) apply.
- You pay only for what you use beyond the free limits.
- No time limit; continues indefinitely.

**Which is ideal for you?** Since you’re new and want to learn first, start with the **Azure Free Account**. It gives you $200 credit and free services to experiment safely. When you’re ready for long-term company use, you can seamlessly switch to Pay-As-You-Go and keep your resources running.

Learn more about Azure account options: ​[https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account![](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7 'Opens in new tab')](https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account)​

## NOTE 4 - Microsft account vs azure account

No. This is the most common misunderstanding about Microsoft Entra ID.

If you create:

```text
Tenant:
hadywafa.onmicrosoft.com

User:
john@hadywafa.com
```

inside Entra ID, then:

### The user CAN

✅ Sign in to Azure Portal
✅ Sign in to Entra Admin Center
✅ Sign in to Enterprise Applications
✅ Sign in to applications federated with Entra ID
✅ Use Azure resources if assigned RBAC permissions

---

### The user CANNOT

❌ Send emails
❌ Receive emails
❌ Log into Outlook Mail
❌ Have a mailbox

unless you purchase an email service.

---

### Example

Suppose you do this:

```text
Entra Tenant
└── hadywafa.com

Users:
├── hady@hadywafa.com
└── dev@hadywafa.com
```

These are only **identities**.

Think of them as:

```text
Username + Password
```

not

```text
Email Inbox
```

---

### What happens if [dev@hadywafa.com](mailto:dev@hadywafa.com) tries Outlook?

He goes to:

```text
outlook.office.com
```

and signs in.

Microsoft checks:

```text
Does this user have an Exchange Online mailbox?
```

Result:

```text
No mailbox found.
```

He can authenticate successfully but cannot use email.

---

### To make it a real email

You need one of:

#### Microsoft 365

```text
Exchange Online
```

or

#### Google Workspace

```text
Gmail for custom domain
```

or

#### Zoho Mail

```text
Custom domain mailbox
```

---

### Real-world company example

At Microsoft:

```text
john@microsoft.com
```

is:

```text
Entra User
+
Exchange Mailbox
```

At a company that only uses Azure:

```text
john@company.com
```

might be:

```text
Entra User only
```

with no mailbox at all.

---

### For your case

If you create:

```text
hadywafa.com
```

and add it to Entra ID without Microsoft 365:

```text
hady@hadywafa.com
```

will work for:

```text
Azure Portal
Azure CLI
Entra ID
Microsoft Learn
```

but **will not work as a real email address**.

That's the reason people buy:

```text
Microsoft 365 Business Basic
```

because it adds:

```text
Exchange Online Mailbox
```

to the same Entra user.

So the same account becomes:

```text
hady@hadywafa.com

✓ Azure Login
✓ Entra Login
✓ Outlook Email
✓ Teams
✓ OneDrive
```

all under one identity.

For someone in your position (Azure + recruiters + certifications), my setup would be:

```text
Domain:
hadywafa.com

Identity:
Microsoft Entra ID

Mailbox:
Microsoft 365 Business Basic

Primary User:
hady@hadywafa.com
```

This gives you one professional identity for Azure, AWS, NVIDIA certifications, LinkedIn, recruiters, and email.
