# 📘 AZ-900 Summary: Module 2 – Describe Azure Architecture and Services (35–40%)

## 🧩 Core Architectural Components of Azure

### 🏢 Datacenter 
A **datacenter** is a physical facility used to house groups of networked servers. 

- Equipped with its own **power**, **cooling**, and **networking** to operate independently.
- Forms the building block of Azure's global infrastructure.
- Hosts Azure compute, storage, and network resources.

### 🗺️ Region
A **region** is a geographical area on the planet that contains **one or more datacenters** connected through a **low-latency network** (typically <2ms).

- Serves as a deployment location for services.
- Azure offers **50+ regions** across the globe, including:
  - Standard commercial regions;
  - Specialized government regions (US DoD Central, US Gov Virginia);
  - Partnered regions (China East, China North).
- Some services are **regional** (VMs, storage), others are **global** (Microsoft Entra ID, DNS).
- Some Azure services are **only available in specific regions** due to compliance or infrastructure availability.

### 🧭 Availability Zone
**Availability Zones** are physically separate locations **within a single Azure region**, each with its own **independent power, cooling, and networking**.

- A zone is composed by one or more data centers.
- Designed for **high availability** and **fault isolation**.
- Only available in zone-enabled regions (not all regions support them).
- A region with Availability Zones has at least **three separate zones**.

**Service Categories**:
- **Zonal Services**: Deployed directly into a specific zone (VMs, managed disks,  IP addresses).
- **Zone-Redundant Services**: Automatically replicated across multiple zones (SQL Database, Azure Storage).
- **Non-Regional Services**: Not tied to a region or zone, resilient by default and globally distributed (Microsoft Entra ID, Azure DNS).

### 🌐 Region Pairs
Azure groups most regions into **region pairs** to ensure resilience, disaster recovery, and data residency.

- Regions are statically paired within the same geography (when possible).
- Paired regions are located at least **300 miles apart**, when possible.
- During planned maintenance, updates are applied to only one region in the pair at a time.
- **Platform-level replication** may occur automatically between paired regions.
- Helps ensure **business continuity** and **jurisdictional compliance**.
- Each pair resides within the same geography*.

**Examples**:
| Region A        | Region B        |
|-----------------|-----------------|
| East US         | West US         |
| UK West         | UK South        |
| North Europe    | West Europe     |
| East Asia       | Southeast Asia  |

> * Note: Some regions (Brazil South) have **one-way pairings** or no backup pairing.

### 🛡️ Sovereign Regions
**Sovereign regions** are **physically and logically isolated instances** of Azure to meet strict regulatory and legal requirements.

- Operated separately from public Azure infrastructure.
- Commonly used by **government agencies** and **regulated industries**.

**Examples**:
- US Government: US Gov Virginia, US DoD Central;
- China: China North, China East.

#### 🌎 Geographies
An **Azure geography** is a discrete market containing two or more regions, designed to preserve **data residency**, **compliance**, and **sovereignty**.

- Each region belongs to one geography.
- Geographies help with **regulatory compliance** by ensuring customer data stays within legal boundaries.

**Examples**:
- Americas;
- Europe;
- Asia Pacific;
- Middle East & Africa.

---

## 🗂️ Organizing and Managing Azure Resources

### 🔗 Azure Resources
Any object created, provisioned, or managed in Azure.

- Represented as **JSON** objects with metadata and configuration definitions.

### 📁 Resource Groups
Logical containers that organize related resources for management and billing.

- Every resource must belong to **one** resource group.
- A resource group has a **location** but can host resources in multiple regions.
- Resources can be **moved** between groups.
- **Resource groups cannot be nested**.

**Best Practices**:
- Group by **lifecycle**, **application**, **environment**, or **department**.
- Use for **role-based access control (RBAC)**, **cost tracking**, and **automation**.

### 🧠 Azure Resource Manager (ARM)
The **management layer** that enables to deploy, manage, and organize Azure resources consistently.

- Supports management via **Azure Portal**, **CLI**, **PowerShell**, and **ARM templates**.
- Enables **infrastructure as code**, tagging, policy enforcement, and automation.

### 📜 Subscriptions
A logical container for billing, access, and provisioning.

- Provide **authenticated access** to Azure resources.
- Enable **separation of billing**, **resource quotas**, and **service access**.
- An account can have **multiple subscriptions**, but only **one is required**.

### 🏢 Management Groups
Provide a scope above subscriptions for **centralized governance**.

- **Inheritance**: Policies, access controls applied to a management group cascade to all subscriptions beneath it.
- **Supports nesting** (up to 6 levels deep).
- Limit: **10,000** management groups per directory.

---
