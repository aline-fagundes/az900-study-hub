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

Protect critical resources from **accidental deletion or modification**. Locks work **with** RBAC—permissions alone aren’t enough to bypass a lock; the lock must be removed first.

- **Lock types**
  - **CanNotDelete** — All operations except **delete** are allowed.
  - **ReadOnly** — Only **read** operations are allowed; create/update/delete (write) operations are blocked.

- **Scope & inheritance**
  - Locks can be applied at **Subscription → Resource Group → Resource**.
  - Locks are **inherited downward** (a lock on a resource group applies to all resources inside it).
  - If multiple locks apply, the **most restrictive** takes precedence.
  - **Management groups cannot be locked**.

- **Who can manage locks**
  - Built-in roles that can create/remove locks: **Owner** and **User Access Administrator**. 

### 🏷️ Tags
**Key–value metadata** for **organization**, **governance**, **cost management**, and **automation**.

- **Where you can tag**
  - **Resources**, **Resource Groups**, and **Subscriptions**.
  - ⚠️ **Not inherited by default** from Resource Group/Subscription. Use **Azure Policy** to **enforce or auto-apply** required tags.

- **Common tagging strategies**
  - **Environment**: `environment=prod|dev|test`
  - **Cost/Finance**: `costCenter=1234`, `department=Finance`, `project=ContosoApp`
  - **Ownership**: `owner=alice@contoso.com`, `team=Platform`
  - **Classification/Compliance**: `dataClass=Confidential`, `retention=1year`
  - **Ops**: `app=webapi`, `tier=frontend`, `region=westus2`

- **Governance & operations**
  - Use **Azure Policy** to **require**, **validate**, or **auto-correct** tags (Append/Modify/Deny).
  - Query estate with **Azure Resource Graph** (KQL) using tags.
  - In **Cost Management**, **filter/group** costs by tags for showback/chargeback.  
    *Note*: Tag-based cost reporting applies **from the time tags are set**.

### 🧯 Azure Policy
**Azure Policy** enforces **governance and compliance** by evaluating **resource properties** at scale (whereas **RBAC** governs **who can do what**).

- **Policy definition**: Describes a rule (IF condition on resource properties, THEN **effect**).
    - Common **effects**: **Deny**, **Audit**, **AuditIfNotExists**, **Append**, **Modify**, **DeployIfNotExists**.
    - Examples: **Allowed locations**, **allowed SKUs**, **allowed resource types**, **require/inherit tags**, **require encryption**.
  - **Initiative (policy set)**: A **group** of policy definitions managed as a single item.
  - **Assignment**: Applies a **definition or initiative** to a **scope**.

- **Scopes & exclusions**
  - Assign at **Management Group → Subscription → Resource Group → Resource** (inherits to child scopes).
  - Add **exclusions** to carve out exceptions.

- **Evaluation & remediation**
  - Evaluated on **create/update** and **periodically** for existing resources to produce **compliance state**.
  - Use **Remediation tasks** (often with a **managed identity**) to **auto-fix** non-compliant resources for effects like **Modify**/**DeployIfNotExists**.

- **Built-in vs custom**
  - Start with **built-in** policies and initiatives for common standards (security, cost, locations).
  - Create **custom** definitions (JSON) for org-specific rules.

- **Operations & reporting**
  - View posture in **Azure Policy compliance dashboard**.
  - Combine with **Tags**, **RBAC**, and **Management Groups** for layered governance.

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
- **Docs**: [Lock resources (Azure Resource Manager)](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/lock-resources?WT.mc_id=AZ-MVP-5003556&tabs=json)
- **Docs**: [Use resource locks to protect resources](https://learn.microsoft.com/en-us/training/modules/control-and-organize-with-azure-resource-manager/6-use-resource-locks-to-protect-resources?WT.mc_id=AZ-MVP-5003556)  
- **Docs**: [Tags](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/tag-resources)
- **Microsoft Learn (Module)**: [Use tagging to organize resources](https://learn.microsoft.com/en-us/training/modules/control-and-organize-with-azure-resource-manager/3-use-tagging-to-organize-resources?WT.mc_id=AZ-MVP-5003556)  
- **Docs**: [Tag resources to logically organize your Azure assets](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/tag-resources?WT.mc_id=AZ-MVP-5003556)
- **Docs**: [Azure Policy](https://learn.microsoft.com/en-us/azure/governance/policy/overview)
- **Microsoft Learn**: [Azure Policy overview](https://learn.microsoft.com/en-us/azure/governance/policy/overview)  
- **Microsoft Learn (Module)**: [Control and organize with Azure Resource Manager – Azure Policy](https://learn.microsoft.com/en-us/training/modules/control-and-organize-with-azure-resource-manager/?WT.mc_id=AZ-MVP-5003556)
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
