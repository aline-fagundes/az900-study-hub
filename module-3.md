# 📘 AZ-900 Summary: Module 3 – Describe Azure Management and Governance (30–35%)

## 🛠️ Azure Management Tools

### 🧭 Azure Portal
A **public, web-based** interface to manage Azure resources.

- Designed for **self-service** and **discoverability**.
- **Customizable** dashboards.
- Great for **ad-hoc** tasks, visual deployment, and troubleshooting.

### 💻 Azure PowerShell
Task automation using **PowerShell** with the **Az** module.

- Cross-platform (Windows, macOS, Linux – PowerShell 7+).
- Ideal for **automation**, **scripting**, and **repeatability**.
- Example cmdlets:
  - `Connect-AzAccount` – sign in;
  - `Get-AzResourceGroup` – list RGs;  
  - `New-AzResourceGroup` – create RG;  
  - `New-AzVM` – create VM.

### 🧰 Azure CLI
**Command Line Interface** for scripting Azure, `az` tool.

- Cross-platform (written in Python; runs everywhere).
- Great for **automation** and **CI/CD**.
- Example commands:
  - `az login` – sign in;
  - `az group list` – list RGs;  
  - `az group create` – create RG;  
  - `az vm create` – create VM.

### ☁️ Azure Cloud Shell
Browser-based **shell environment** hosted in Azure.

- Runs **Bash** or **PowerShell**.
- Includes **Azure CLI**, **Azure PowerShell**, **Git**, **Terraform**, **kubectl**, etc.
- Accessible from:
  - **Azure Portal**;
  - **Shell Portal**;
  - **VS Code** extension;
  - **Windows Terminal**;
  - **Microsoft Docs** integrated “Try It”.

### 🧩 ARM Templates & Bicep (Infrastructure as Code)
Define infrastructure **declaratively**.

- **ARM templates (JSON)**: native IaC format.
- **Bicep**: higher-level language that **compiles to ARM**.
- Benefits: **Idempotent**, **source-controlled**, **repeatable** deployments.

### 🌐 Azure Mobile App
Manage and monitor resources **on the go** (alerts, simple actions, status).

### 🔎 Azure Resource Graph
**Query at scale** across subscriptions for inventory, compliance, and reporting using **Kusto Query Language (KQL)**.

---

## 📈 Monitoring, Health, and Guidance

### 📊 Azure Monitor
End-to-end platform for **metrics**, **logs**, **alerts**, and **visualization**.

- **Metrics**: Near real-time numeric values (e.g., CPU, latency).
- **Logs**: Detailed events in **Log Analytics workspace** (KQL queries).
- **Alerts**: Metric- or log-based, action groups for notifications/automation.
- **Dashboards & Workbooks** for visualization.

#### 🔍 Application Insights
**APM** for apps (requests, dependencies, failures, traces, live metrics).

#### 🧾 Log Analytics Workspace
Central **log store** for queries, analysis, and cross-resource insights.

### 🩺 Service Health vs Resource Health
- **Azure Service Health**: Personalized alerts for **service-wide** issues (outages, planned maintenance) **affecting your regions/services**.
- **Resource Health**: Status for **your specific** resource (e.g., a VM unhealthy).

### 🧠 Azure Advisor
Personalized **best-practice** recommendations across:
 - **Cost** (SKU sizes, idle services, reserved instances);
 - **Security** (MFA settings, vulnerability settings, agent installations);
 - **Reliability** (redundanccy settings, soft delete on clocs);
 - **Operational excellence** (service health, subscription limits);
 - **Performance** (SKU sizes, SDK versions, IO throttling).
- Actionable guidance with estimated **savings/impact**.
- Integrates with **Azure Policy** and **Workbooks**.

---

## 🧭 Governance & Compliance

### 👥 Role-Based Access Control (RBAC)
Grant **fine-grained** access at the right **scope**.

- **Scopes**: Management group → Subscription → Resource group → Resource.
- **Built-in roles** (Reader, Contributor, Owner) + **custom roles**.
- Uses **Microsoft Entra ID** identities (users, groups, service principals, managed identities).

### 🔐 Resource Locks
Protect critical resources from accidental changes.

- **CanNotDelete** and **ReadOnly** locks
- Applied at **resource** or **resource group** (inherits down).

### 🏷️ Tags
Key–value metadata for **organization**, **cost allocation**, and **automation**.

- Apply at resource/RG/subscription; use **Azure Policy** to **enforce/append** tags.

### 🧯 Azure Policy
Create and assign **policy definitions** to **enforce compliance**.

- **Effects**: **Deny**, **Audit**, **Append**, **Modify**, **DeployIfNotExists**.
- Group multiple policies as an **Initiative (policy set)**.
- Evaluate and remediate **at scale** across scopes.

> ℹ️ **Blueprints** have been superseded by **Template Specs** and **Deployment Stacks** for packaging and governing deployment artifacts.

### 🗃️ Management Groups
Govern **multiple subscriptions** together (RBAC, Policy, Tags, Locks applied top-down).

---

## 💵 Cost Management & SLAs

### 💰 Azure Cost Management + Billing
Track, analyze, and optimize spend.

- **Cost analysis**, **budgets**, **alerts**, **exports**.
- **Reservations** (VM, SQL, etc.) and **Azure Savings Plans for Compute** for long-term savings.
- **Tags** and **management groups** for chargeback/showback.

### 🧮 Pricing Calculator & TCO Calculator
- **Pricing Calculator**: Estimate service costs.
- **TCO Calculator**: On-prem vs Azure **total cost** comparison.

### 📜 Service Level Agreements (SLAs)
Azure provides SLAs per service.

- Example: **99.9%**, **99.95%**, **99.99%** availability (varies by service/tier).
- **Composite SLA** for multi-service apps is **multiplicative**.
  *Example*: 99.9% (0.999) × 99.9% (0.999) ≈ **99.8%**

### 🔁 Service Lifecycle
- **Preview** (Public/Private): For evaluation; **no SLA**.
- **General Availability (GA)**: **Production-ready**, SLA-backed.

---

## 📚 Study Resources

### 🛠️ **Management & Automation**
- **Microsoft Learn**: [Describe Azure management and governance](https://learn.microsoft.com/en-us/training/paths/azure-fundamentals-describe-azure-management-governance/)
- **Docs**: [Azure Portal](https://learn.microsoft.com/en-us/azure/azure-portal/azure-portal-overview)
- **Docs**: [Azure PowerShell (Az)](https://learn.microsoft.com/en-us/powershell/azure/what-is-azure-powershell)
- **Docs**: [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/)
- **Docs**: [Azure Cloud Shell](https://learn.microsoft.com/en-us/azure/cloud-shell/overview)
- **Docs**: [Bicep](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/overview) · [ARM Templates](https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/overview)
- **Docs**: [Azure Resource Graph](https://learn.microsoft.com/en-us/azure/governance/resource-graph/overview)

### 📈 **Monitoring & Health**
- **Docs**: [Azure Monitor](https://learn.microsoft.com/en-us/azure/azure-monitor/overview)
- **Docs**: [Application Insights](https://learn.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview)
- **Docs**: [Service Health](https://learn.microsoft.com/en-us/azure/service-health/overview)
- **Docs**: [Resource Health](https://learn.microsoft.com/en-us/azure/service-health/resource-health-overview)
- **Docs**: [Azure Advisor](https://learn.microsoft.com/en-us/azure/advisor/advisor-overview)

### 🧭 **Governance**
- **Docs**: [RBAC](https://learn.microsoft.com/en-us/azure/role-based-access-control/overview)
- **Docs**: [Resource Locks](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/lock-resources)
- **Docs**: [Tags](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/tag-resources)
- **Docs**: [Azure Policy](https://learn.microsoft.com/en-us/azure/governance/policy/overview)
- **Docs**: [Management Groups](https://learn.microsoft.com/en-us/azure/governance/management-groups/overview)

### 💵 **Cost & SLAs**
- **Tool**: [Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/)
- **Tool**: [TCO Calculator](https://azure.microsoft.com/en-us/pricing/tco/calculator/)
- **Docs**: [Cost Management + Billing](https://learn.microsoft.com/en-us/azure/cost-management-billing/cost-management-billing-overview)
- **Docs**: [Service Level Agreements](https://azure.microsoft.com/en-us/support/legal/sla/)
- **Status**: [Azure Status (public)](https://status.azure.com/)

---

## 🧠 Quick Review (Exam Tips)

- **Monitor everything**: **Metrics vs Logs**, **App Insights**, **Alerts**, **Service Health** vs **Resource Health**.
- **Govern the platform**: **RBAC** (who can do what), **Policy** (what is allowed), **Locks** (protect), **Tags** (organize), **Management Groups** (govern at scale).
- **Control costs**: **Budgets/alerts**, **Reservations**/**Savings Plans**, **Pricing/TCO calculators**.
- **Know SLAs & lifecycle**: **Preview ≠ SLA**, **GA = SLA**, **Composite SLA** multiplies.
