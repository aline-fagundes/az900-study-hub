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
Logical containers that organize related resources.

- Every resource must belong to **one** resource group.
- A resource group has a **location** but can host resources in multiple regions.
- Resources can be **moved** between groups.
- Resources inherit settings from resource groups.
- **Resource groups cannot be nested**.
- Commonly group by:
  - Type;
  - Lifecycle;
  - App;
  - Environment;
  - Department;
  - Billing;
  - Location.

### 🧠 Azure Resource Manager (ARM)
The **management layer** that enables to deploy, manage, and organize Azure resources consistently.

- Supports management via **Azure Portal**, **CLI**, **PowerShell**, and **ARM templates**.
- Enables **infrastructure as code**, tagging, policy enforcement, and automation.

### 📜 Subscriptions
A logical container to logically organize resource groups by billing, access management, and provisioning.

- Provide **authenticated access** to Azure resources.
- Enable **separation of billing**, **resource quotas**, and **service access**.
- An account can have **multiple subscriptions**, but only **one is required**.
- Resource groups inherit settings from subscriptions.

### 🏢 Management Groups
Provide a scope above subscriptions for **centralized governance**.

- **Supports nesting** (up to 6 levels deep).
- Limit: **10,000** management groups per directory.
- Each management group and subscription can support only **one parent**.
- Subscriptions inherit settings from management groups.

---

## ⚙️ Azure Compute and Networking Services

### 🖥️ Azure Compute Services

#### 🧱 Virtual Machines (VMs)
**Virtual Machines (VMs)** are Azure's IaaS compute offering.

- Provides **full control** over OS, environment, and configurations.
- Supports **marketplace** and **custom images**.
- Ideal for:
  - Custom software that requires specific system settings.
  - Legacy application hosting.
  - Lift-and-shift migrations.
  - Running web apps, databases, desktop apps, and more.

**VM Resources** typically include:
- Size (CPU, memory);
- Storage (HDD/SSD);
- Networking (VNet, public IP, NSG rules).

  > * Virtualization is the **emulation of physical machines** using software. It allows multiple virtual environments to run on a single physical machine.

#### 🔄 Virtual Machine Scale Sets
**VM Scale Sets** are an IaaS service that allows you to deploy and manage a set of **identical, load-balanced VMs**.

- Built-in **auto-scaling** features based on metrics or schedules.
- Best for:
  - Large-scale services such as **web apps** or **batch jobs**.
- Integrates with Azure Load Balancer by default.

#### 🧳 Availability Sets
**Availability Sets** are a **resiliency feature** for VMs, designed to increase uptime during maintenance or failure events.

- Groups VMs into:
  - **Fault domains**: Separate power/network hardware.
  - **Update domains**: Groupings for rolling updates without full outage.
- Ensures high availability during maintenance or unexpected failures.
- No additional cost.

#### 🖥️ Azure Virtual Desktop
Azure Virtual Desktop provides **desktop and app virtualization** from the cloud.

- Allows users to access Windows desktops and apps **from anywhere**.
- Supports **multi-session Windows 10/11 Enterprise**, enabling multiple users per VM.
- Enhances **security** and **centralized management** using Microsoft Entra ID and RBAC.
- Separates local devices from cloud-hosted data for improved security.

### 📦 Containers and Orchestration

#### 🧱 Azure Container Instances (ACI)
**PaaS** for running **single-container** instances quickly.

- No need to manage VMs or orchestration services.
- Serverless, billed per second.
- Ideal for:
  - Background tasks;
  - Event-driven apps;
  - Microservices.

#### ⚙️ Azure Container Apps
**PaaS** managed container service with scaling and traffic control.

- Supports multiple containers and microservices scenarios.
- Integrated with **Dapr**, **KEDA**, and **Envoy** for advanced routing.

#### 🧩 Azure Kubernetes Service (AKS)
**PaaS** solution for **container orchestration**.

- Based on the open-source **Kubernetes** platform.
- Used to deploy, manage, and scale complex container-based applications.
- Highly customizable, supports auto-scaling, and integrates with CI/CD pipelines.

### 🌐 Web Apps and Serverless Compute

#### 🔧 Azure App Service
**PaaS** for hosting **web apps, REST APIs, and mobile backends**.

- Supports multiple languages (.NET, Node.js, Python, PHP, Java).
- Features:
  - Built-in load balancing and autoscaling;
  - Deployment slots for staging and testing;
  - Integration with GitHub and DevOps pipelines.

#### ⚡ Azure Functions
**Serverless event-driven** compute service.
  
- Supports:
  - **Stateless functions** (default behavior);
  - **Durable Functions** for stateful workflows.
- **Pricing models**:
  - **Consumption plan**: Auto-scales, pay-per-execution;
  - **Premium/dedicated plans**: Pre-warmed, reserved capacity.
- Ideal for:
  - Microservices;
  - IoT event handling;
  - Real-time data processing.

---

### 💻 Azure VMware Solution
Service for running VMware workloads **natively in Azure**.

- Ideal for organizations using VMware on-premises and migrating to the cloud.
- Provides **seamless integration** and **scalability** using familiar VMware tools.

---

### 🧠 Summary Table

| Service                     | Model        | Use Case                                               |
|-----------------------------|--------------|--------------------------------------------------------|
| **Virtual Machines**        | IaaS         | Custom OS/config, legacy apps, full control            |
| **VM Scale Sets**           | IaaS         | Auto-scaled and load-balanced identical VMs            |
| **Availability Sets**       | IaaS         | Fault-tolerance across power/network infrastructure    |
| **Azure Virtual Desktop**   | PaaS         | Cloud-hosted desktop and app virtualization            |
| **Container Instances**     | PaaS         | Lightweight single-container deployments               |
| **Container Apps**          | PaaS         | Microservices and scalable container solutions         |
| **Kubernetes Service (AKS)**| PaaS         | Complex container orchestration                        |
| **App Services**            | PaaS         | Web apps, REST APIs, auto-scaled backend               |
| **Azure Functions**         | Serverless   | Microservices, real-time processing, event-driven code |
| **Azure VMware Solution**   | Hybrid IaaS  | Migrate/extend on-prem VMware workloads                |

---

### 🌐 Azure Networking Services
