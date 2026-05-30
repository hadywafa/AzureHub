# AZ-305 Overview

## Current AZ-305 Exam Structure (Latest Update)

Microsoft updated the skills measured in April 2026. ([Microsoft Learn](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/az-305?utm_source=chatgpt.com 'Study guide for Exam AZ-305: Designing Microsoft Azure ...'))

Main domains:

| Domain                                                | Weight |
| ----------------------------------------------------- | ------ |
| Design identity, governance, and monitoring solutions | 25–30% |
| Design data storage solutions                         | 20–25% |
| Design business continuity solutions                  | 15–20% |
| Design infrastructure solutions                       | 30–35% |
|                                                       |        |

Infrastructure is the largest section. ([Microsoft Learn](https://learn.microsoft.com/zh-tw/credentials/certifications/exams/az-305/?utm_source=chatgpt.com '測驗AZ-305: 設計Microsoft Azure 基礎設施解決方案'))

---

## What Microsoft Actually Tests

The exam is heavily focused on:

- Trade-offs
- Architecture decisions
- Cost optimization
- High availability
- Disaster recovery
- Security
- Enterprise governance

Less focus on:

- CLI commands
- PowerShell syntax
- Portal screenshots

You will see questions like:

> Company has 3 regions, 5000 users, hybrid environment, RPO=15 min, RTO=1 hour.
>
> Which architecture should be selected?

That is AZ-305.

---

## The Best Study Order For You

Because you already know Azure and DevOps, I would NOT follow Microsoft Learn order.

Follow this instead:

---

## Phase 1 — Azure Architecture Foundation

Study:

### Azure Well-Architected Framework

Understand:

- Reliability
- Security
- Cost Optimization
- Operational Excellence
- Performance Efficiency

Very important because almost every scenario question is secretly testing WAF thinking. ([Microsoft Learn](https://learn.microsoft.com/en-us/training/courses/az-305t00?utm_source=chatgpt.com 'Course AZ-305T00-A: Design Microsoft Azure Infrastructure Solutions'))

---

### Cloud Adoption Framework (CAF)

Know:

- Landing Zones
- Enterprise Scale
- Management Groups
- Governance Strategy

Not deeply tested directly, but many design questions assume CAF concepts.

---

## Phase 2 — Identity & Governance

This domain appears everywhere.

Focus heavily on:

### Microsoft Entra ID

Know:

- Users
- Groups
- Administrative Units
- B2B
- B2C
- Cross-tenant access

---

### Identity Patterns

Know when to use:

- Managed Identity
- Service Principal
- Workload Identity
- Federated Credentials

---

### RBAC

Focus on:

- Scope inheritance
- Management Groups
- Subscription
- Resource Groups
- Resource-level assignments

---

### Governance

Know:

- Azure Policy
- Initiative
- Resource Locks
- Tags
- Blueprints (legacy awareness)
- Cost Management

---

### Monitoring

Know:

- Azure Monitor
- Log Analytics
- Application Insights
- Data Collection Rules
- Alerts

---

## Phase 3 — Networking (Very Important)

This is one of the biggest sections.

Master:

### Virtual Network

- Peering
- Global Peering
- Hub-Spoke
- Mesh

---

### Connectivity

Know exactly:

| Service      | Usage              |
| ------------ | ------------------ |
| VPN Gateway  | Internet-based     |
| ExpressRoute | Private connection |
| Virtual WAN  | Large enterprises  |
| Route Server | Dynamic routing    |

---

### Security

- NSG
- ASG
- Azure Firewall
- WAF
- DDoS Protection

---

### Traffic Distribution

Know differences:

| Service             | Layer     |
| ------------------- | --------- |
| Load Balancer       | L4        |
| Application Gateway | L7        |
| Front Door          | Global L7 |
| Traffic Manager     | DNS       |

This is one of the most common exam areas.

---

## Phase 4 — Compute

Know architecture choices.

### VM vs VMSS

When to choose each.

---

### AKS

Know:

- Private Cluster
- Node Pools
- Availability Zones
- Ingress

Not deep Kubernetes administration.

Design level only.

---

### App Service

Know:

- Deployment Slots
- Autoscaling
- Regional deployment

---

### Container Apps

Microsoft is increasing focus on Container Apps.

Know:

- When to use Container Apps
- When AKS is overkill

---

### Functions

Know:

- Consumption
- Premium
- Dedicated

---

## Phase 5 — Storage

Very important.

Know:

### Storage Account Types

- GPv2
- Premium
- Blob
- Files

---

### Replication

Most tested topic.

Know exactly:

| Replication | Region                      |
| ----------- | --------------------------- |
| LRS         | Single                      |
| ZRS         | Multi-zone                  |
| GRS         | Secondary region            |
| RA-GRS      | Read access secondary       |
| GZRS        | Zone + Region               |
| RA-GZRS     | Read access + zone + region |

This appears constantly.

---

### Storage Security

Know:

- SAS
- User Delegation SAS
- Private Endpoint
- Service Endpoint

---

## Phase 6 — Databases

Architecture-focused.

Know differences between:

### SQL

- Azure SQL Database
- Managed Instance
- SQL on VM

---

### Cosmos DB

Must know:

- Consistency Levels

Strong

Bounded Staleness

Session

Consistent Prefix

Eventual

These are frequently tested.

---

### PostgreSQL

### MySQL

### SQL Hyperscale

Know high-level use cases.

---

## Phase 7 — High Availability & Disaster Recovery

This section is extremely important.

Know:

### Availability Zones

### Availability Sets

### Zone Redundant Services

---

### Backup Services

- Azure Backup
- Recovery Vault

---

### Disaster Recovery

- Azure Site Recovery

---

Understand:

RPO

Recovery Point Objective

RTO

Recovery Time Objective

These appear everywhere.

---

## Phase 8 — Migration

Know:

### Azure Migrate

- Discovery
- Assessment
- Migration

---

### Database Migration Service

When to use it.

---

## Newer Topics Showing Up More Often

Focus on these because many old courses are outdated.

### Azure Container Apps

### Workload Identity

### Private Endpoints

### Landing Zones

### Azure Virtual WAN

### Confidential Computing

### Defender for Cloud

### Cost Optimization Architectures

### Multi-region Design

### Zone-redundant Architecture

### Hybrid Connectivity

### AKS Architecture Patterns

Microsoft has been modernizing questions around these services. ([Microsoft Learn](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/az-305?utm_source=chatgpt.com 'Study guide for Exam AZ-305: Designing Microsoft Azure ...'))

---

## Topics You Should Not Overstudy

Because you already have AZ-104 and AZ-400:

- Azure CLI syntax
- PowerShell commands
- ARM template syntax
- Bicep syntax
- Detailed Kubernetes administration
- Detailed Terraform syntax

AZ-305 is not an implementation exam.

---

## Real Exam Difficulty

For your background:

| Area            | Difficulty  |
| --------------- | ----------- |
| Networking      | High        |
| Storage         | Medium      |
| Identity        | Medium      |
| Governance      | Medium      |
| AKS Design      | Easy        |
| DevOps Concepts | Easy        |
| HA/DR           | Medium      |
| Data Solutions  | Medium-High |

---

## My Recommended Learning Sequence For You

1. Azure Well-Architected Framework
2. Landing Zones & CAF
3. Entra ID & Governance
4. Networking
5. Storage
6. Compute
7. Databases
8. Business Continuity & DR
9. Migration
10. Full Architecture Case Studies
11. Practice Exams
12. Microsoft Learn Review

This order matches how architects actually think and will be much faster for you than following Microsoft Learn module-by-module.

Official resources:

- [AZ-305 Exam Page](https://learn.microsoft.com/en-us/credentials/certifications/exams/az-305/?utm_source=chatgpt.com)
- [Latest AZ-305 Study Guide (April 2026 Skills Measured)](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/az-305?utm_source=chatgpt.com)
- [Azure Solutions Architect Expert Certification Page](https://learn.microsoft.com/en-us/credentials/certifications/azure-solutions-architect/?utm_source=chatgpt.com)
