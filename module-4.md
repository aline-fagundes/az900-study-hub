# 📘 AZ-900 Summary: Module 4 – Describe Azure Cost Management and Service Level Agreements (10–15%)

## 💵 Cost Management

### 💡 Cost & Pricing Fundamentals
Azure pricing is **meter-based**: you pay for what you use according to each service’s meters (CPU hours, GB stored, transactions, egress GB, etc).

- **Cost drivers**
  - **Resource type & SKU**: Different tiers (example: GP vs Premium) and sizes have different rates.
  - **Region**: Prices vary **by region**.
  - **Data transfer**: **Outbound (egress)** to the internet/other regions usually costs; inbound is typically free.
  - **Storage redundancy**: **LRS/ZRS/GRS/GZRS** affect price and durability.
  - **Offers/agreements**: Azure purchasing channels (Microsoft Customer Agreement / Enterprise Agreement / Cloud Solution Provider) and **Dev/Test** subscriptions can change billing or discounts.
  - **Licensing**: Windows/SQL licensing can be optimized with **Hybrid Benefit**.

- **Saving mechanisms**
  - **Reservations** (commit to 1 or 3 years).
  - **Savings Plan for Compute** (spend commitment, flexible across compute).
  - **Azure Hybrid Benefit** (reuse existing Windows/SQL licenses).
  - **Spot VMs** (steep discounts for interruptible workloads).

### 🏷️ Azure Reservations (RIs & Reserved Capacity)
Commit to a **1- or 3-year** term for a lower rate.

- **Applies to**:  
  - **VMs** (Reserved **Instances**),  
  - **Reserved capacity** for **Azure SQL vCores**, **Cosmos DB RUs**, **Storage**, **Databricks DBUs**, and more,  
  - **Software plans** (Red Hat, SUSE, etc) via separate reservation SKUs.
- **Scope**: **Shared** (subscription-wide) or **single** (resource group).
- **Payment**: **Upfront or monthly** (same discount).
- **Flexibility**: Exchanges/scope changes allowed; cancellations may have fees.

**When to use**: Steady-state workloads you’ll run for months/years.

### 🧠 Azure Savings Plan for Compute
A 1- or 3-year **spend commitment per hour** that **automatically applies** the lowest eligible compute prices across:

- **VMs**, **VMSS**, **AKS** nodes, **App Service (Linux)**, **Functions Premium**, etc., **across regions**.
- More **flexible** than reservations (not tied to a specific VM family/size), usually a **smaller discount** than highly targeted RIs.

### ⚡ Azure Hybrid Benefit
Bring existing **Windows Server** and **SQL Server** licenses with active Software Assurance to Azure.

- **Windows Server** → reduce VM cost (you pay base compute).
- **SQL Server** → reduce cost on **Azure SQL Database**, **SQL Managed Instance**, or **SQL on VMs**.
- Note: Red Hat / SUSE discounts are handled via **software plan reservations**, not Azure Hybrid Benefit.

### 🧪 Spot VMs
Use **unused Azure capacity** at deep discounts.

- **Evictable** at any time (capacity reclaimed); set a **max price** or choose **capacity-only** eviction policy.
- **Best for**: Batch jobs, CI/CD agents, stateless processing, dev/test **not** for critical/stateful services.

### 🧮 Pricing & TCO Calculators
- **Pricing Calculator**: Model **per-service** costs by region, SKU, and usage.
- **TCO Calculator**: Compare **on-prem vs Azure** costs (hardware, energy, ops) to justify migration.

### 📊 Azure Cost Management and Billing
Central tooling to **track, analyze, and optimize** spending.

- **Cost analysis** (by **Subscription/Resource Group/Tag**).
- **Budgets & alerts** (thresholds on cost or usage).
- **Exports** (CSV to Storage) & API access.
- **Recommendations** (right-size, idle resources).
- **Chargeback/showback** via **tags** and **management groups**.

> **Tip**: Tag diligently; **cost reports only include tags from the time they’re applied**.

### 🔧 Practical Cost Optimization
- **Right-size** compute; shut down dev/test after hours; use **auto-shutdown** and **scale-in**.
- Prefer **PaaS/Serverless** when possible (scale to zero).
- Choose **storage tiers** (Hot/Cool/Archive) with **Lifecycle Management**.
- **Reserve** predictable workloads; **Savings Plan** for mixed compute; **Azure Hybrid Benefit** for Windows/SQL.
- Consider **Spot** for interruptible jobs.
- Use **Advisor** + **Cost Management** regularly.

---

## 📄 SLAs

### 📜 Service Level Agreements (SLAs)

An **SLA** is a **formal agreement** between Microsoft and the customer that specifies a service’s **availability (uptime & connectivity)** target and **service credits** if the target isn’t met.

- **Per-service**: Each Azure service/tier has its **own SLA** (some **free/preview** features have **no SLA**).
- **Typical range**: **99.0% → 99.999%** depending on service and configuration (zones, redundancy).
- **Credits**: Breaking an SLA results in **service credits** (discount on your bill), not cash refunds.
- **Composite SLA**: For multi-service apps, **overall availability** depends on how components are combined.

**Approximate maximum monthly downtime equivalents**

| SLA         | Max downtime / month |
|-------------|-----------------------|
| **99.0%**   | ~7 h 18 m 17 s        |
| **99.5%**   | ~3 h 39 m 08 s        |
| **99.9%**   | ~43 m 49 s            |
| **99.95%**  | ~21 m 54 s            |
| **99.99%**  | ~4 m 22 s             |
| **99.999%** | ~26 s                 |

> **Design tip**: Use **Availability Zones/sets**, multiple instances, and **health probes** to increase SLA; place dependencies in **redundant** configurations when possible.

### 🔁 Service Lifecycle
Every Azure service/feature moves through a **lifecycle**:

- **Preview** (Public/Private)  
  - **No SLA**; some services have **limited or no support**  
  - Often **limited regions/features**; **pricing** and direction can change  
  - Intended for **evaluation/testing**, **not** production  
  - Preview portal: <https://preview.portal.azure.com>

- **GA (General Availability)**  
  - **Production-ready**, **SLA-backed**, and broadly supported

---

### 📚 Study Resources

## 💵 Cost Management
- **Tool**: [Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/)
- **Tool**: [TCO Calculator](https://azure.microsoft.com/en-us/pricing/tco/calculator/)
- **Docs**: [Cost Management + Billing](https://learn.microsoft.com/en-us/azure/cost-management-billing/cost-management-billing-overview)


### 📄 SLAs
- *Docs*: [Service Level Agreements](https://azure.microsoft.com/en-us/support/legal/sla/)
- *Status*: [Azure Status (public)](https://status.azure.com/)
