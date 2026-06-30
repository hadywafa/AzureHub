You scored 673, only 27 points below the 700 passing score. Your report identifies three specific weaknesses:

1. Design governance
2. Design logging and monitoring
3. Design data integration  

Do not spend the next six hours reviewing the whole course equally. Concentrate on architectural service-selection questions.

Also note: your score report is from October 10, 2025, while the English AZ-305 exam was updated on April 17, 2026. The four domain weights remain:

- Infrastructure: 30–35%
- Identity, governance and monitoring: 25–30%
- Data storage: 20–25%
- Business continuity: 15–20%  

Your six-hour rescue plan

Hour 1 — Governance

Study these distinctions until you can answer them immediately.

Azure hierarchy

Tenant

└── Management groups

    └── Subscriptions

        └── Resource groups

            └── Resources

Remember:

- Management groups: apply governance across multiple subscriptions.
- Subscriptions: billing, quota, administrative and workload boundaries.
- Resource groups: lifecycle boundary; resources deployed and deleted together when appropriate.
- Tags: classification and cost reporting, but tags do not automatically inherit by default.
- Azure Policy: enforce or audit resource configuration.
- RBAC: controls who can perform actions.
- Resource locks: prevent accidental deletion or modification.

Policy effects

|   |   |
|---|---|
|Requirement|Correct effect|
|Block noncompliant deployment|Deny|
|Report noncompliance only|Audit|
|Add or change properties|Modify|
|Deploy supporting configuration|DeployIfNotExists|
|Prevent policy evaluation|Disabled|

Know:

- Initiative = collection of policies.
- Exemption = approved exception without changing the policy assignment.
- Remediation task = fixes existing resources for supported effects.
- Policy assignment can be at management group, subscription or resource-group scope.

Identity governance

Know when to choose:

- Privileged Identity Management: just-in-time privileged access.
- Access reviews: periodically verify that access is still needed.
- Entitlement management/access packages: package access to groups, applications and SharePoint resources.
- Conditional Access: enforce authentication conditions such as MFA, location, risk and device compliance.
- Managed identity: application accesses Azure resources without storing credentials.
- Key Vault: secrets, certificates and encryption keys.

The current exam explicitly covers subscription hierarchy, tagging, compliance and identity governance.  

  

Hour 2 — Logging and monitoring

Build this mental model:

Resources

   ↓ diagnostic settings

Log Analytics workspace / Storage account / Event Hub

   ↓

Azure Monitor

   ├── Metrics

   ├── Logs

   ├── Alerts

   ├── Workbooks

   └── Application Insights

Service-selection table

|   |   |
|---|---|
|Requirement|Choose|
|Query logs using KQL|Log Analytics workspace|
|Application performance, dependencies and traces|Application Insights|
|Near-real-time numerical measurements|Azure Monitor Metrics|
|Long-term inexpensive log archive|Storage account|
|Stream monitoring data to external SIEM|Event Hub|
|Centralized security analytics and SIEM|Microsoft Sentinel|
|Network traffic metadata|NSG flow logs / Traffic Analytics|
|VM guest OS monitoring|Azure Monitor Agent + Data Collection Rule|
|Visual interactive dashboard|Azure Monitor Workbook|
|Automatically respond to alert|Action group / Automation / Logic App|

Critical distinctions

Activity Log

- Subscription-level control-plane activity.
- Examples: resource created, policy assigned, VM deleted.
- Not application or guest operating-system logs.

Resource logs

- Service-specific data-plane or operational logs.
- Must normally be routed using diagnostic settings.

Metrics

- Numeric, time-series data.
- Fast alerting.
- Better for CPU percentage, request count and latency thresholds.

Logs

- Rich records queried using KQL.
- Better for correlation, troubleshooting and analytics.

Application Insights

- Requests, exceptions, dependencies, distributed tracing and application performance monitoring.

The current objective explicitly requires selecting logging, log-routing and monitoring solutions.  

  

Hour 3 — Data integration

This is probably where you can gain the fastest marks.

Messaging and integration comparison

|   |   |
|---|---|
|Requirement|Choose|
|Enterprise message broker, queues, topics, transactions|Azure Service Bus|
|Massive event ingestion or telemetry streaming|Event Hubs|
|React to individual Azure resource events|Event Grid|
|Visual workflow and SaaS integration|Logic Apps|
|Serverless custom code|Azure Functions|
|Batch data movement and ETL/ELT orchestration|Azure Data Factory|
|Big-data processing and Spark|Azure Databricks|
|Enterprise analytics and data warehouse|Azure Synapse Analytics|
|Real-time stream processing using SQL-like queries|Azure Stream Analytics|
|API publishing, security and throttling|API Management|

Service Bus versus Event Hubs versus Event Grid

Service Bus

- Commands and business messages.
- Queues and topics.
- Competing consumers.
- Sessions, transactions, dead-letter queues and duplicate detection.
- Consumers process messages reliably.

Event Hubs

- High-throughput event ingestion.
- Telemetry, logs and streaming.
- Partitions and consumer groups.
- Events are retained for a configured period and can be replayed.

Event Grid

- Event notification and reactive architecture.
- Push-based publish/subscribe.
- Example: trigger processing when a blob is created.
- Not a durable enterprise queue.

Data Factory versus Logic Apps

Choose Data Factory when the requirement concerns:

- Moving or transforming large datasets.
- ETL/ELT pipelines.
- Scheduled data integration.
- On-premises data using self-hosted integration runtime.

Choose Logic Apps when the requirement concerns:

- Business workflows.
- Approval processes.
- SaaS connectors.
- Email, Teams, ServiceNow, Salesforce and similar integrations.

The current AZ-305 guide explicitly assesses both data integration and data analysis recommendations.  

  

Hour 4 — Infrastructure high-weight revision

This is the largest domain, so do not ignore it even though it was not among your weakest three areas.

Compute selection

|   |   |
|---|---|
|Requirement|Choose|
|Full OS control or legacy application|Virtual Machines|
|Autoscaling web application with minimal infrastructure|App Service|
|Kubernetes orchestration and portability|AKS|
|Simple container deployment without orchestration|Azure Container Instances|
|Event-driven short-running code|Azure Functions|
|Serverless containers and revision-based deployment|Azure Container Apps|
|Large parallel or HPC jobs|Azure Batch|
|Globally distributed static frontend|Azure Static Web Apps|

Networking selection

|   |   |
|---|---|
|Requirement|Choose|
|Private dedicated connection from on-premises|ExpressRoute|
|Encrypted connection over the internet|Site-to-Site VPN|
|Individual user connects remotely|Point-to-Site VPN|
|Global HTTP(S) load balancing and acceleration|Azure Front Door|
|Regional Layer 7 load balancing and WAF|Application Gateway|
|Regional Layer 4 load balancing|Azure Load Balancer|
|DNS-based global traffic distribution|Traffic Manager|
|Private access to a PaaS resource from a VNet|Private Endpoint|
|Secure outbound connectivity from private subnet|NAT Gateway|
|Hub-and-spoke managed transit and security|Azure Virtual WAN|

Key trap:

- Front Door: global, HTTP/HTTPS, edge service.
- Application Gateway: regional, Layer 7.
- Load Balancer: regional, Layer 4.
- Traffic Manager: DNS only; it does not proxy traffic.

  

Hour 5 — Business continuity and storage

RPO and RTO

- RPO: acceptable amount of data loss measured in time.
- RTO: acceptable time to restore the service.

Availability

|   |   |
|---|---|
|Requirement|Design|
|Datacenter failure protection within one region|Availability Zones|
|Hardware/rack maintenance protection|Availability Sets|
|Regional outage protection|Multi-region deployment|
|VM disaster recovery to another region|Azure Site Recovery|
|Backup VMs and supported workloads|Azure Backup|
|Global web application failover|Front Door or Traffic Manager|
|SQL Database regional failover|Failover groups / active geo-replication|

Storage redundancy

|   |   |
|---|---|
|Option|Protection|
|LRS|One datacenter|
|ZRS|Multiple availability zones in one region|
|GRS|Primary region plus paired secondary region|
|RA-GRS|GRS plus read access to secondary|
|GZRS|Zone redundancy in primary plus regional replication|
|RA-GZRS|GZRS plus read access to secondary|

Remember:

- Blob versioning protects against overwrites.
- Soft delete protects against accidental deletion.
- Immutable storage supports WORM and compliance.
- Lifecycle management automatically moves blobs between tiers or deletes them.
- Azure Files supports SMB/NFS shares.
- Blob Storage is object storage.
- Managed disks are block storage for VMs.

  

Hour 6 — Questions only

Do not watch another long video.

Take the official Microsoft Practice Assessment or your best available practice test. The official exam page provides a free assessment.  

Use this method:

1. Answer 40–50 questions under time pressure.
2. For every incorrect answer, write one sentence:

Requirement → selected service → why alternatives fail

Example:

Reliable transactional messaging → Service Bus →

Event Hubs is streaming ingestion and Event Grid is event notification.

3. Spend the final 20 minutes reviewing only those mistakes.

Do not repeatedly retake questions until you memorize their positions. Understand the constraint that changes the answer.

Exam-answering method

For every architecture question, identify these five things:

1. Functional requirement

2. Availability and disaster-recovery requirement

3. Security and network requirement

4. Operational-management requirement

5. Cost constraint

Then eliminate options.

Watch for phrases such as:

- least administrative effort
- minimize cost
- highest availability
- no public internet exposure
- support automatic failover
- retain messages until processed
- globally route users to the nearest endpoint
- apply governance across all subscriptions

These phrases usually determine the answer more strongly than the general technical scenario.

Final 15-minute memory sheet

Memorize this:

RBAC = who can do what

Policy = what resources are allowed

PIM = just-in-time privileged access

Access Reviews = periodically validate access

  

Metrics = fast numerical time-series

Logs = detailed KQL analysis

Application Insights = application telemetry

Diagnostic Settings = route resource logs

Event Hub = stream logs externally

  

Service Bus = reliable business messaging

Event Hubs = high-volume telemetry

Event Grid = event notification

Data Factory = ETL/data pipelines

Logic Apps = business workflow

  

Front Door = global L7

Application Gateway = regional L7

Load Balancer = regional L4

Traffic Manager = global DNS

  

Private Endpoint = private IP for PaaS

Service Endpoint = secure PaaS access through service routing

ExpressRoute = private dedicated on-premises connectivity

VPN = encrypted connectivity over internet

  

RPO = acceptable data loss

RTO = acceptable recovery time

Availability Zones = datacenter failure

Site Recovery = VM disaster recovery

Azure Backup = backup and restore

Your target is not to learn everything in six hours. You only need to convert approximately three to five uncertain architecture decisions into correct answers. Given your previous 673, this focused plan gives you a realistic chance of passing.