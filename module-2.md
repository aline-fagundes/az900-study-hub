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

### 🌎 Geographies
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

#### 💻 Azure VMware Solution
Service for running VMware workloads **natively in Azure**.

- Ideal for organizations using VMware on-premises and migrating to the cloud.
- Provides **seamless integration** and **scalability** using familiar VMware tools.

#### 📦 Containers and Orchestration

##### 🧱 Azure Container Instances (ACI)
**PaaS** for running **single-container** instances quickly.

- No need to manage VMs or orchestration services.
- Serverless, billed per second.
- Ideal for:
  - Background tasks;
  - Event-driven apps;
  - Microservices.

##### ⚙️ Azure Container Apps
**PaaS** managed container service with scaling and traffic control.

- Supports multiple containers and microservices scenarios.
- Integrated with **Dapr**, **KEDA**, and **Envoy** for advanced routing.

##### 🧩 Azure Kubernetes Service (AKS)
**PaaS** solution for **container orchestration**.

- Based on the open-source **Kubernetes** platform.
- Used to deploy, manage, and scale complex container-based applications.
- Highly customizable, supports auto-scaling, and integrates with CI/CD pipelines.

#### 🌐 Web Apps and Serverless Compute

##### 🔧 Azure App Service
**PaaS** for hosting **web apps, REST APIs, and mobile backends**.

- Supports multiple languages (.NET, Node.js, Python, PHP, Java).
- Features:
  - Built-in load balancing and autoscaling;
  - Deployment slots for staging and testing;
  - Integration with GitHub and DevOps pipelines.

##### ⚡ Azure Functions
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

### 🧠 Summary Table

| Service                     | Model | Use Case                                                                          |
|-----------------------------|-------|-----------------------------------------------------------------------------------|
| **Virtual Machines**        | IaaS  | Custom OS/config, legacy apps, full control                                       |
| **VM Scale Sets**           | IaaS  | Auto-scaled and load-balanced identical VMs                                       |
| **Availability Sets**       | IaaS  | Fault-tolerance across power/network infrastructure                               |
| **Azure Virtual Desktop**   | PaaS  | Cloud-hosted desktop and app virtualization                                       |
| **Container Instances**     | PaaS  | Lightweight single-container deployments                                          |
| **Container Apps**          | PaaS  | Microservices and scalable container solutions                                    |
| **Kubernetes Service (AKS)**| PaaS  | Complex container orchestration                                                   |
| **App Services**            | PaaS  | Web apps, REST APIs, auto-scaled backend                                          |
| **Azure Functions**         | FaaS  | Micro and nano services, consumption-based pricing, event-driven code, serverless |
| **Azure VMware Solution**   | IaaS  | Migrate/extend on-prem VMware workloads                                           |

---

### 🌐 Azure Networking Services

Azure Networking enables secure and scalable connectivity across Azure resources, between Azure and on-premises environments, and with the public internet. Key networking components help ensure **isolation**, **communication**, **routing**, **security**, and **performance**.

#### 🛡️ Virtual Network (VNet)
A **Virtual Network (VNet)** is a fundamental building block for private networking in Azure.

- Enables **logical isolation and segmentation** of networked Azure resources.
- Scopes to a **single region**.
- Cross-regional communication can be enabled via **VNet Peering**.
- Provides **IP address allocation**, **routing**, **filtering** and **traffic control**.

**Capabilities**:
- **Subnets**: Segment networks into smaller address spaces.
- **NSGs / ASGs**: Apply security rules to control inbound/outbound traffic.
- **Private/Public Endpoints**: Enable internal or internet-facing communication.
- **Communication**: Between Azure VMs, services, and on-premises resources.

> 🔸 Use VNets to build hybrid solutions or secure internal app communication.

#### 🔁 Azure Load Balancer
A **Layer 4 (TCP/UDP) load balancer** that distributes traffic across resources for performance and redundancy.

- Supports **inbound** and **outbound** scenarios.
- Two types:
  - **Public** Load Balancer: For internet-facing workloads.
  - **Internal** Load Balancer: For private/internal workloads.
- Features:
  - **Health probes** to monitor availability.
  - **Port forwarding** and **NAT rules** for configuration.
  - **High throughput** (millions of flows).

> 🔸 Use Azure Load Balancer for stateless workloads requiring ultra-fast, low-latency distribution.

#### 🔐 VPN Gateway
A **VPN Gateway** provides encrypted tunnels over the public internet to connect on-premises and Azure networks securely.

- Supports **site-to-site** and **point-to-site** VPN configurations.
- Ideal for secure cross-premises communication over untrusted networks.
- Can be deployed as **zone-redundant** for high availability.
- Enables cross-regional communication of VNets.

> 🔸 Choose VPN Gateway when budget-sensitive or using existing internet infrastructure.

#### 🧭 Application Gateway
A **Layer 7 (HTTP/HTTPS) load balancer** designed for web apps.

- Features:
  - **Web Application Firewall (WAF)** for OWASP protection.
  - **SSL termination**, **URL-based routing**, **redirection**, **session affinity**.
  - Autoscaling and zone redundancy.

> 🔸 Best for intelligent traffic routing at the application layer.

#### 🌍 Content Delivery Network (CDN)
Azure CDN improves **latency and performance** for delivering web content to users.

- Distributes cached content to **global POPs (Points of Presence)**.
- Reduces load on origin servers.
- Works well for static content: images, videos, scripts, stylesheets.

> 🔸 Use Azure CDN to optimize web performance for global users.

#### 🚇 ExpressRoute
**ExpressRoute** creates a **private, dedicated connection** between on-prem infrastructure and Azure, bypassing the public internet.

- Offers **higher reliability**, **faster speeds**, **lower latencies**, and **better security**.
- Ideal for:
  - Financial services
  - Large data migrations
  - Compliance-sensitive environments

> 🔸 Use ExpressRoute for mission-critical workloads needing private connectivity.

#### 🧭 Azure DNS
Azure DNS is a **high-availability, ultra-fast DNS hosting service** for domain name resolution.

- Hosted on Microsoft’s global infrastructure.
- Does **not** support domain name purchasing — only hosting and resolution.

> 🔸 Integrate Azure DNS with your domain registrar for scalable and reliable DNS management.

---

### 🧠 Summary Table

| Service                 | Layer       | Purpose                                         |
|-------------------------|-------------|-------------------------------------------------|
| **Virtual Network**     | Network     | Internal networking, segmentation, hybrid setup |
| **Load Balancer**       | Layer 4     | Distributes TCP/UDP traffic across VMs/services |
| **VPN Gateway**         | Network     | Secure on-prem to Azure communication           |
| **Application Gateway** | Layer 7     | HTTP/HTTPS load balancing + WAF                 |
| **CDN**                 | Edge        | Low-latency delivery of static content          |
| **ExpressRoute**        | Private WAN | Private, high-performance connection to Azure   |
| **Azure DNS**           | DNS         | Domain resolution via Microsoft infrastructure  |

---

## 🗄️ Azure Storage Services

### 📚 Data Types
- **Structured**: Tabular data with strict schema and relationships (relational databases).
- **Semi-structured**: Key–value or document-style data without a rigid schema (JSON).
- **Unstructured**: Files of any type (images, videos, binaries, logs, backups).

### 🏷️ Storage Account
A **storage account** provides a unique namespace reachable over **HTTP/HTTPS** and is the **billing and security boundary** for Azure Storage services.

- **Services hosted**: **Blob**, **File**, **Queue**, **Table**.
- **Scale & durability**: Petabyte-scale, up to 11–16 “nines” durability (depending on redundancy).
- **Security & access**:
  - Encryption at rest by default.
  - **RBAC with Microsoft Entra ID** for authorization.
  - **Private Endpoints**, **service endpoints**, and **firewall rules** for network isolation.
- **Management & cost control**:
  - **Lifecycle Management** policies (auto-tier, archive, delete).
  - **Soft delete**, **blob versioning**, **immutability** (time-based / legal hold).
  - **Standard** (HDD/standard performance) vs **Premium** (SSD/low-latency) SKUs.

### 🧱 Blob Storage
**BLOB = Binary Large Object**. General-purpose file/object storage for backups, media, data lakes, and static websites.

- **Tiers**:
  - **Hot**: frequently accessed data;
  - **Cool**: infrequently accessed data;
  - **Archive**: rarely accessed data.
- **Features**: Static website hosting, multipart upload, lifecycle policies, soft delete, versioning, immutability.

**Use cases**: Backups, archival, big data lakes, content serving, log ingestion.

### 📬 Queue Storage
Lightweight **asynchronous messaging** between components.

- **Messages** stored in FIFO-style queues.
- **Decouple** producers/consumers.

**Use cases**: Background jobs, task buffers, resilient work pipelines.

### 📒 Table Storage
Storage for **semi-structured** data (**NoSQL**).

- **Schema-less**; entities addressed by **PartitionKey** + **RowKey**.
- **Fast and cost-effective** for large, sparse datasets.

**Use cases**: Metadata, catalogs, logs, simple user profiles.

### 📁 Azure Files
**Fully managed file shares** in the cloud with **SMB**.

- Designed to extend on-premise file shares or implement **lift-and-shift** scenarios.
- **Azure File Sync**: Cache Azure Files on Windows Server for local performance & centralized cloud storage.

**Use cases**: User profiles, app shares, legacy apps expecting SMB/NFS.

### 💽 Disk Storage
Managed disks for Azure VMs and other services.

- Different **types** (SSD, HDD), sizes, performance tiers.
- Disk can be unmanaged or managed.

**Use cases**: VM OS/data disks, databases, high-IO workloads.

### 🚚 Data Movement
- **AzCopy** / **Storage Explorer** for uploads, management.
- **Azure Data Box** / **Import/Export** for large offline migrations.
- **Data Factory** / **Synapse** for pipelines and analytics integration.

---

### 🧠 Summary Table

| Service           | Data Type           | Highlights                                | Typical Use                          |
|-------------------|---------------------|-------------------------------------------|--------------------------------------|
| **Blob Storage**  | Unstructured        | Hot/Cool/Archive tiers                    | Backups, data lakes, media, logs     |
| **Queue Storage** | Messages            | Simple async messaging, decoupling        | Background jobs, task queues         |
| **Table Storage** | Semi-structured     | NoSQL key–value, schema-less              | Metadata, catalogs, logs             |
| **Azure Files**   | Un/structured files | SMB/NFS shares, File Sync, snapshots      | Lift-and-shift shares, user profiles |
| **Disk Storage**  | Block (page blobs)  | Managed disks, multiple performance tiers | VM OS/data disks, databases          |

---

## 📚 Study Resources

### 🧩 **Core Azure Architecture**
- **YouTube**: [Azure Regions and Availability Zones](https://youtu.be/C-nNw1mGwzE)
- **Microsoft Learn**: [Availability Zones](https://learn.microsoft.com/en-us/azure/reliability/availability-zones-overview)
- **Microsoft Learn**: [Products available by region](https://azure.microsoft.com/en-us/explore/global-infrastructure/products-by-region/)
- **Azure Speed Test**: [Measure Latency](http://azurespeedtest.azurewebsites.net/)

### 🧱 **Azure Resource Management**
- **YouTube**: [Azure Resource Groups and Resource Manager](https://youtu.be/gIhf-S7BCdo)
- **YouTube**: [Managing Azure resources with Azure CLI](https://youtu.be/GqpwiyYsNIw)
- **YouTube**: [Azure Resource Manager Templates](https://youtu.be/Ge_Sp-1lWZ4)
- **Microsoft Learn**: [Resource Groups Overview](https://learn.microsoft.com/en-us/training/modules/control-and-organize-with-azure-resource-manager/2-principles-of-resource-groups)
- **Microsoft Learn**: [Tagging Resources](https://learn.microsoft.com/en-us/training/modules/control-and-organize-with-azure-resource-manager/3-use-tagging-to-organize-resources)
- **Microsoft Learn**: [Azure Resource Manager (ARM)](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview)
- **Microsoft Learn**: [ Resource Groups](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview#resource-groups)
- **Microsoft Learn**: [Azure Management Groups](https://learn.microsoft.com/en-us/azure/governance/management-groups/overview)
- **Azure Resources Portal**: [Azure Resource JSON definition](https://resources.azure.com/)

### ⚙️ **Azure Compute Services**
- **YouTube**: [Azure Compute Services](https://youtu.be/inaXkN2UrFE)
- **Microsoft Learn**: [Virtual Machines](https://azure.microsoft.com/en-in/resources/cloud-computing-dictionary/what-is-a-virtual-machine)
- **Microsoft Learn**: [Virtual Machines Scale Sets](https://azure.microsoft.com/en-us/services/virtual-machine-scale-sets/)
- **Microsoft Learn**: [App Services](https://azure.microsoft.com/en-us/services/app-service/)
- **Microsoft Learn**: [Azure Functions](https://azure.microsoft.com/en-us/services/functions/)
- **Microsoft Learn**: [Container Instances](https://azure.microsoft.com/en-in/services/container-instances/)
- **Microsoft Learn**: [Azure Kubernetes Service (AKS)](https://azure.microsoft.com/en-us/services/kubernetes-service)
- **Wikipedia**: [Kubernetes](https://en.wikipedia.org/wiki/Kubernetes)
- **Kubernetes**: [Official Website](https://kubernetes.io/)
- **Microsoft Learn**: [Azure Virtual Desktop](https://learn.microsoft.com/en-us/azure/virtual-desktop/overview)
- **YouTube**: [Azure Virtual Machine (VM) Tutorial](https://youtu.be/iUaTq06m26g)
- **YouTube**: [Azure App Service (Web Apps) Tutorial](https://youtu.be/4BwyqmRTrx8)
- **YouTube**: [Azure Function Apps Tutorial](https://youtu.be/Vxf-rOEO1q4)
- **YouTube**: [Azure Container Instances Tutorial](https://youtu.be/jAWLQFi4USk)

### 🌐 **Azure Networking Services**
- **YouTube**: [Azure Networking Services](https://youtu.be/5NMcM4zJPM4)
- **Microsoft Learn**: [Virtual Network Overview](https://azure.microsoft.com/en-us/products/virtual-network/)
- **Microsoft Learn**: [Load Balancer Overview](https://azure.microsoft.com/en-us/products/load-balancer/)
- **Microsoft Learn**: [VPN Gateway Overview](https://azure.microsoft.com/en-in/services/vpn-gateway/)
- **Microsoft Learn**: [Application Gateway Overview](https://azure.microsoft.com/en-us/products/application-gateway/)
- **Microsoft Learn**: [Content Delivery Network (CDN)](https://azure.microsoft.com/en-us/products/cdn/)
- **Microsoft Learn**: [ExpressRoute Overview](https://learn.microsoft.com/en-us/azure/expressroute/)
- **Microsoft Learn**: [Azure DNS Overview](https://learn.microsoft.com/en-us/azure/dns/dns-overview)
- **YouTube**: [Azure Load Balancer Tutorial](https://youtu.be/T7XU6Lz8lJw)
- **YouTube**: [Azure Traffic Manager Tutorial](https://youtu.be/aPNa7Axulhg)

### 🗄️ **Azure Storage Services**
- **Microsoft Learn**: [Azure Storage Overview](https://learn.microsoft.com/en-us/azure/storage/common/storage-introduction?WT.mc_id=AZ-MVP-5003556)
- **Azure Products**: [All Storage Products](https://azure.microsoft.com/en-us/products/category/storage/?WT.mc_id=AZ-MVP-5003556)
- **Azure Products**: [Blob Storage](https://azure.microsoft.com/en-us/products/storage/blobs/?WT.mc_id=AZ-MVP-5003556)
- **Azure Products**: [Azure Files](https://azure.microsoft.com/en-us/products/storage/files/?WT.mc_id=AZ-MVP-5003556)
- **Azure Products**: [Disk Storage](https://azure.microsoft.com/en-us/products/storage/disks/?WT.mc_id=AZ-MVP-5003556)
- **Azure Products**: [Table Storage](https://azure.microsoft.com/en-us/products/storage/tables/?WT.mc_id=AZ-MVP-5003556)
- **Azure Products**: [Queue Storage](https://azure.microsoft.com/en-us/products/storage/queues/?WT.mc_id=AZ-MVP-5003556)
- **YouTube**: [Azure Storage Overview](https://www.youtube.com/watch?v=UzTtastcBsk)
- **YouTube**: [Azure Queue Storage Tutorial](https://www.youtube.com/watch?v=JQ6KhjU5Zsg)
- **YouTube**: [Azure Table Storage Tutorial](https://www.youtube.com/watch?v=HSL1poL1VR0)
- **YouTube**: [Azure Files Tutorial](https://www.youtube.com/watch?v=BCzeb0IAy2k)
