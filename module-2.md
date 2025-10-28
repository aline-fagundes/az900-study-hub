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

- A zone is composed of one or more data centers.
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

- Manage via **Azure Portal**, **CLI**, **PowerShell**, **ARM/Bicep templates**.
- Enables **infrastructure as code**, **tagging**, **policy enforcement**, **locks**, and automation.

### 📜 Subscriptions
A logical container for **billing**, **resource quotas**, **access boundaries**, and **service enablement**.

- Provide **authenticated access** to Azure resources.
- One account can have **multiple subscriptions**, but only **one is required**.
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
- **Hybrid connectivity**: Communicate with on-premises networks via **VPN Gateway** or **ExpressRoute**.

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

- **Site-to-site**, **point-to-site**, and **VNet-to-VNet** configurations.
- Ideal for secure cross-premises communication over untrusted networks.
- Can be deployed as **zone-redundant** for high availability.
- Enables cross-regional communication of VNets.

> 🔸 Choose VPN Gateway when leveraging existing internet connectivity or for cost-sensitive hybrid links.

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

#### 🌍 Azure Front Door
A **global, anycast Layer 7** entry service that provides **smart routing**, **WAF**, **TLS offload**, and **edge caching**.

- Improves global performance and availability for web apps/APIs.
- Works well with regional backends (App Service, AKS, VMs) and integrates with CDN/WAF.

#### 🧭 Azure Traffic Manager
A **DNS load-balancing** service for distributing traffic across **multiple endpoints/regions**.

- Routing methods: **Priority**, **Weighted**, **Performance**, **Geographic**, **Multi-value**, **Subnet**.
- Great for geo-distribution, disaster recovery/failover, and blue/green at DNS layer.

---

### 🧠 Summary Table

| Service                 | Layer       | Purpose                                                 |
|-------------------------|-------------|---------------------------------------------------------|
| **Virtual Network**     | Network     | Internal networking, segmentation, hybrid setup         |
| **Load Balancer**       | Layer 4     | Distributes TCP/UDP traffic across VMs/services         |
| **VPN Gateway**         | Network     | Secure on-prem to Azure communication                   |
| **Application Gateway** | Layer 7     | HTTP/HTTPS load balancing + WAF                         |
| **CDN**                 | Edge        | Low-latency delivery of static content                  |
| **ExpressRoute**        | Private WAN | Private, high-performance connection to Azure           |
| **Azure DNS**           | DNS         | Domain resolution via Microsoft infrastructure          |
| **Front Door**          | Layer 7     | Global entry point with smart routing, WAF, TLS offload |
| **Traffic Manager**     | DNS         | DNS-based global traffic distribution/failover          |


---

## 🗄️ Azure Storage Services

### 📚 Data Types
- **Structured**  
  Tabular data with a **strict, predefined schema** and relationships.  
  *Examples*: Records in **relational databases** (SQL).  

- **Semi-structured**  
  Data with a **flexible (schema-on-read)** format. Fields may vary between records, but each item has a unique identifier.  
  *Examples*: **JSON**, **CSV**, **XML**, logs.  

- **Unstructured**  
  Files that **don’t fit a tabular model**.  
  *Examples*: Images, videos, audio, PDFs, binaries, large backups.

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

> **Use cases**: Backups, archival, big data lakes, content serving, log ingestion.

### 📬 Queue Storage
Lightweight **asynchronous messaging** between components.

- **Messages** stored in FIFO-style queues.
- **Decouple** producers/consumers.

> **Use cases**: Background jobs, task buffers, resilient work pipelines.

### 📒 Table Storage
Storage for **semi-structured** data (**NoSQL**).

- **Schema-less**; entities addressed by **PartitionKey** + **RowKey**.
- **Fast and cost-effective** for large, sparse datasets.

> **Use cases**: Metadata, catalogs, logs, simple user profiles.

### 📁 Azure Files
**Fully managed file shares** in the cloud with **SMB**.

- Designed to extend on-premises file shares or implement **lift-and-shift** scenarios.
- **Azure File Sync**: Cache Azure Files on Windows Server for local performance & centralized cloud storage.

> **Use cases**: User profiles, app shares, legacy apps expecting SMB/NFS.

### 💽 Disk Storage
Managed disks for Azure VMs and other services.

- Different **types** (SSD, HDD), sizes, performance tiers.
- Features: **Snapshots**, **images**, encryption; choose type by required IOPS/latency.
- *Unmanaged disks* are legacy and generally discouraged.

> **Use cases**: VM OS/data disks, databases, high-IO workloads.

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

## 🗄️ Database Services

### 🌍 Cosmos DB

- **Type**: Fully managed, **globally distributed NoSQL** database for semi-structured data.
- **Global distribution**: Multi-region **replication** with optional **multi-master writes**; read/write from the nearest region.
- Supports **multiple APIs**:
 - **SQL**,
 - **MongoDB**,
 - **Cassandra**,
 - **Gremlin** (Graph),
 - **Table Storage** (Key-value).
- **Performance model**: **RU/s (Request Units)** with **Provisioned**, **Autoscale**, or **Serverless** options.
- **Data model & scale**: Logical **partitions** by **partition key**; automatic **global indexing**.
- **Resiliency & SLA**: 99.999% for multi-region (availability), latency and consistency SLAs.

>  **Best for**: **Low-latency (<10 ms)**, **planet-scale**, **JSON** workloads (IoT, telemetry, user profiles, catalogs, real-time apps).

### 🧮 Azure SQL Database

- **Type**: Fully managed (PaaS) **relational** database based on SQL Server engine.
- **Deployment options**: **Single database**, **Elastic pool** (share compute), **Hyperscale** (very large DBs).
- **Tiers & purchasing**:
  - **Service tiers**: **General Purpose**, **Business Critical**, **Hyperscale**.
  - **Compute models**: **vCore** (recommended; choose CPU/Memory; **serverless** or **provisioned**), or **DTU** (legacy).
  - **Serverless**: Auto-pause/auto-resume to save cost on intermittent workloads.
- **Business continuity**: Automated **backups**, **Point-in-Time Restore**, **Zone redundancy**, **Active Geo-Replication** (up to 4 readable secondaries).
- **Security**: **TDE** at rest, **Always Encrypted**, **Auditing**, **Azure AD (Entra ID)** auth, **Private Link**.

>  **Best for**: Transactional apps needing **SQL**, **strong consistency**, and minimal ops.    

### 🧩 Azure SQL Product Family
- **Azure SQL Database** – (PaaS) Cloud-native SQL Server database for modern apps needing managed SQL.
- **Azure SQL Managed Instance** – (PaaS)  **Near full SQL Server compatibility**; ideal for **lift-and-shift** from on-prem without managing OS.
- **SQL Server on Azure VM** – (IaaS) Full SQL Server on Windows/Linux VM for **maximum control** (you manage OS/patching/HA/backup).
- **Azure Database for MySQL** – (PaaS) Managed **MySQL** (Flexible Server); Automated patching, backups, **zone-redundant HA**, scaling.
- **Azure Database for PostgreSQL** – (PaaS) Managed **PostgreSQL** (Flexible Server / Hyperscale-Citus); Vertical and horizontal scale-out for sharded workloads.
- **Azure Synapse Analytics** (formerly SQL Data Warehouse) – (PaaS) **MPP** analytics for **data warehousing**; Integrates with Spark, pipelines, Power BI.

---

### 🔍 Key Concepts to Remember about Database Services

- **Cosmos DB** = NoSQL, globally distributed, <10ms latency, supports multiple APIs.
- **Azure SQL Database** = Fully managed relational database.
- **Azure SQL Managed Instance** = Near-complete SQL Server compatibility with PaaS benefits.
- **SQL on VM** = Traditional SQL Server with full control (IaaS).
- **Azure Database for MySQL/PostgreSQL** = Open-source relational DB engines with managed hosting.
- **Synapse Analytics** = Data warehouse solution for large-scale analytics and reporting.

---

### 🛒 Azure Marketplace

**Azure Marketplace** is Microsoft’s catalog of **certified** solutions that run on or integrate with Azure.

- **What you get**
  - **IaaS**, **PaaS**, and **SaaS**.
  - **VM images** (preconfigured OS and software)
  - **SaaS apps** (subscription-based services hosted by the publisher)
  - **Managed apps** (publisher deploys/operates resources in your subscription)
  - **Containers, templates, connectors**, and **consulting services**

- **Who publishes**
  - **First-party (Microsoft)** and **third-party vendors**.  
  - Offers are **validated** to meet Azure policies and compliance standards.

- **Pricing & billing**
  - You may pay for **Azure resources** **and** the **publisher’s software or service fees** (varies by offer).
  - Common models: **pay-as-you-go**, bring your own license, **free trials**, and **private offers** negotiated with the publisher.
  - Charges appear on your **Azure bill** for consolidated management.

---

### 🌐 Azure IoT (Internet of Things)

**Internet of Things (IoT)** is a network of internet-connected devices (sensors, controllers, appliances) that **send telemetry**, **receive commands**, and can be **remotely managed**.

#### 🛰️ Azure IoT Hub (PaaS)
A **managed message hub** for **bi-directional** device–cloud communication.

- **Secure, scalable, reliable** device connectivity and management
- **Protocols**: HTTPS, AMQP, MQTT
- **SDKs**: C, C#, Java, Python, Node.js
- Integrates with **Event Hubs**, **Stream Analytics**, **Functions**, **Storage**, **Synapse**, etc.

> **Use cases**: Ingest telemetry at scale, command & control, device lifecycle management.

#### 🧭 Azure IoT Central (SaaS)
A **ready-to-use IoT application platform** built on top of IoT Hub and 30+ Azure services.

- **No deep cloud expertise** required; **industry templates** for fast start
- Built-in **device modeling**, dashboards, rules/alerts, jobs, and user roles
- **Secure, scalable** device onboarding, management, and monitoring

> **Use cases**: Rapid solution rollout with minimal engineering; business-ready IoT applications.

#### 🔐 Azure Sphere
A secure platform for **microcontroller (MCU)-class devices**.

- **Azure Sphere–certified chips**
- **Azure Sphere OS** (Linux-based)
- **Azure Sphere Security Service** for trusted device-to-cloud communication, updates, and certificate-based auth

> **Use cases**: Highly secured embedded devices.
  
---

### 📊 Azure Big Data & Analytics

**Big Data** refers to information that is **too large, fast, or diverse** to be processed effectively with traditional systems, requiring scalable storage, distributed processing, and specialized analytics services.

#### 3 V’s of Big Data
- **Volume** – Amount of data (GB → TB → PB+)
- **Velocity** – Speed of generation/processing  
  *Batch · Periodic · Near real-time · Real time*
- **Variety** – Types and structure of data  
  *Tables/DBs · Logs · Images/Audio/Video · Social media · JSON/CSV*

#### 🧠 Azure Synapse Analytics (PaaS)
An **end-to-end analytics platform** that unifies **data ingestion, preparation, warehousing, and big data**.

- **Synapse Studio**: Unified UI (author, monitor, analyze).
- **Compute options**:
  - **Dedicated SQL pools** (provisioned MPP data warehouse; predictable performance/cost).
  - **Serverless SQL** (ad-hoc queries over data in Data Lake; pay per TB processed).
  - **Apache Spark** (data engineering, ML, batch/stream processing).
- **Orchestration**: **Synapse Pipelines** (Data Factory ETL/ELT inside Synapse).
- **Storage**: Tightly integrates with **Azure Data Lake Storage Gen2** (HNS).
- **Integration**: Power BI, Azure ML, Event Hubs/IoT Hub, Functions.

> **Use cases**: Enterprise data warehouse, lakehouse analytics, ELT at scale, ad-hoc SQL over files.

#### ☁️ Azure HDInsight (PaaS)
Fully managed **open-source big data** clusters.

- Supports **Hadoop**, **Spark**, **Kafka**, **Hive**, **HBase**, **Storm**.
- You choose the tech; Azure manages the cluster lifecycle.
- Integrates with Azure Storage / Data Lake.

> **Use cases**: OSS-centric analytics, Kafka streaming, Hadoop/Spark migrations.

#### 🔥 Azure Databricks (PaaS)
Fast, collaborative **Apache Spark** based analytics platform optimized for Azure.

- **Notebooks** (Python/SQL/Scala/R), **Delta Lake**, **MLflow** integration.
- Auto-scaling clusters, job scheduling, Unity Catalog (governance).
- Deep integration with **ADLS Gen2**, **Event Hubs**, **Synapse**, **Power BI**.

> **Use cases**: Data engineering, lakehouse ETL, advanced analytics & ML at scale.

#### 🧩 Complementary Services
- **Azure Data Lake Storage Gen2**: Low-cost, scalable storage with **hierarchical namespace** for analytics.
- **Azure Data Factory** / **Synapse Pipelines**: **Code-free** and code-first **ETL/ELT** across on-prem and cloud sources.
- **Azure Stream Analytics**: **Serverless** SQL-like engine for **real-time** analytics over streams (Event Hubs/IoT Hub).
- **Azure Event Hubs**: High-throughput **ingestion** for telemetry and streaming data.
- **Power BI**: Self-service **data visualization** and reporting (often paired with Synapse/Databricks).

---

### 🤖 Artificial Intelligence & Machine Learning

**Artificial Intelligence (AI)** is the simulation of human intelligence and capabilities by software.  
**Machine Learning (ML)** is a subfield of AI where models learn patterns from data to make predictions or decisions.

#### 🧪 Azure Machine Learning (PaaS)
A **cloud platform** for building, training, deploying, and managing ML models at scale.

- **Core concepts**
  - **Workspaces**: Top-level resource for all ML assets.
  - **Azure ML Studio**: Web portal for end-to-end authoring and MLOps.
  - **SDK & CLI**: Python/R SDKs, CLI for automation and CI/CD.
- **Features**
  - **Notebooks**: Author in Python/R with managed compute.
  - **Automated ML (AutoML)**: Tries multiple algorithms/parameters and selects the best model.
  - **Designer**: Drag-and-drop no-code/low-code pipelines.
  - **Data & Compute**: Datastores, data labeling, compute clusters/instances, job scheduling.
  - **Pipelines**: Reproducible training/ETL; track runs and metrics.
  - **Model registry & endpoints**: Register, version, and deploy models to **managed online/batch endpoints**.

> **Use cases**: Forecasting, classification, recommendation, computer vision, NLP.

#### 🧠 Azure AI Services (PaaS)
Prebuilt AI APIs to add intelligence without training your own models.

- **Vision**: Image analysis, OCR, face detection, document intelligence.
- **Language**: Text analytics, key phrases, sentiment, language detection, Q&A.
- **Speech**: Speech-to-text, text-to-speech, translation, speaker recognition.
- **Decision**: Anomaly detection, personalization (some services vary by region).
- **Responsible AI**: Content filters, abuse monitoring, and policy controls.

**Model consumption**: Call via REST/SDK; **consumption-based** pricing (per call/second).

#### 🔎 Azure AI Search
AI-powered search over your **structured and unstructured** content.

- **Indexers** to pull data from Storage/Databases.
- **Skillsets** to enrich content (OCR, language detection, entity extraction).
- **Vector & hybrid search** for semantic relevance and RAG scenarios.
- Expose **search indexes** via REST/SDK to apps and websites.

#### 💬 Azure Bot Service
Build and deploy conversational bots.

- Works with **Bot Framework** SDK/Composer.
- Connect to channels (Teams, Web Chat, etc).
- Integrate with **Azure AI Services** for NLU, speech, and Q&A.

---

### ⚡ Serverless Computing

**Serverless** is a cloud execution model where you run code or workflows **without managing servers**. The platform **auto-scales**, handles **infrastructure**, and you pay for **actual usage** (events/executions), not idle capacity.

#### 🧩 Azure Functions (FaaS)
Event-driven code execution for **micro/nano-services**.

- **Triggers & Bindings**: Respond to events (HTTP, Timer, Queue/Service Bus, Blob, Event Grid, Event Hubs, Cosmos DB, etc) with input/output bindings.
- **Languages**: .NET/.NET Core, Java, Node.js, Python, PowerShell.
- **State**: Default **stateless**; use **Durable Functions** for stateful workflows/orchestrations (fan-out/in, chaining, human interaction).
- **Scaling**: Automatic (event-driven); can scale to zero.
- **Plans/Pricing**:
  - **Consumption**: Pay-per-execution and compute time (*cold starts possible*).
  - **Premium**: Pre-warmed instances, VNET integration, no cold start.
  - **Dedicated (App Service plan)**: Fixed capacity; useful when sharing with existing App Service.

> **Use cases**: APIs, webhooks, file processing, scheduled jobs, event processing, ETL steps.

#### 🔗 Azure Logic Apps
No/low-code **orchestration** for apps, data, and business processes.

- **Connectors**: 200+ managed connectors (Office 365, Salesforce, SAP, Service Bus, SQL, Storage, etc.).
- **Workflows**: Triggers → Actions, conditions, loops, parallel branches, exception handling.

> **Use cases**: System integration, approvals, data sync, RPA alternatives, enterprise workflows.

#### 📮 Azure Event Grid
**Publish–subscribe** eventing for near real-time apps.

- **Sources**: Many Azure services (Storage, Resource Groups, IoT Hub), custom topics/domains.
- **Handlers**: Functions, Logic Apps, Webhooks, Service Bus, Event Hubs, etc.
- **Features**: At-least-once delivery, filtering/advanced routing, retry & dead-letter.
- **Scale**: High throughput, low-latency event distribution.

> **Use cases**: Reactive architectures, resource lifecycle events, decoupled microservices.

#### 🧭 Related Messaging Services (Know the Role)
- **Azure Service Bus**: Enterprise **messages/queues/topics** with ordering, sessions, transactions, dead-lettering (**commands** pattern).
- **Azure Event Hubs**: **Telemetry ingestion** at massive scale (streaming events; **ingest** pattern).
- **Event Grid**: **Event routing**/notifications (react **to** events; **notify** pattern).

---

### 🚀 DevOps

**DevOps** combines **Development (Dev)** and **Operations (Ops)** practices to deliver software **faster and more reliably**. Core ideas include **Continuous Integration (CI)**, **Continuous Delivery/Deployment (CD)**, collaboration, automation, and monitoring.

#### 🧰 Azure DevOps Services (SaaS)
A suite of services for planning, coding, building, testing, and releasing software.

- **Boards** – Agile planning & tracking (Epics/Features/Stories/Tasks, Kanban/Scrum, backlogs, dashboards).
- **Repos** – Git repositories with pull requests, code reviews, branch policies.
- **Pipelines** – **CI/CD** with YAML/classic pipelines; build, test, and deploy to Azure and beyond. 
  - Hosted agents (Microsoft-provided) or self-hosted agents.
  - Environments, approvals/checks, multi-stage releases.
- **Test Plans** – Manual & exploratory testing, test suites, traceability.
- **Artifacts** – Package management (NuGet, npm, Maven, Python), versioning, retention.
- **Extensions Marketplace** (1,000+ add-ons) and REST APIs.
- Works with **ARM/Bicep/Terraform** for **Infrastructure as Code (IaC)**.
- Can integrate with **GitHub** (source) and **GitHub Actions** (CI/CD).

#### 🧪 Azure DevTest Labs (PaaS)
Create cost-controlled **self-service dev/test environments**.

- Quick provisioning of **preconfigured VM templates** and reusable **artifacts** (tools, scripts).
- **Policies**: quotas, VM sizes, **auto-shutdown**, cost tracking.
- Share **custom images**, automate via **ARM/Bicep/CLI** and pipeline plugins.
- Ideal for **sandboxing**, training, and reproducible test setups.

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

### 🗄️ **Database Services**
- **Azure Products**: [Azure Cosmos DB](https://azure.microsoft.com/en-us/products/cosmos-db/?WT.mc_id=AZ-MVP-5003556)
- **Microsoft Learn**: [Azure Cosmos DB – Introduction](https://learn.microsoft.com/en-us/azure/cosmos-db/introduction?WT.mc_id=AZ-MVP-5003556)
- **Azure Products**: [Azure SQL (SQL Database, Managed Instance, SQL on VMs)](https://azure.microsoft.com/en-us/products/azure-sql/?WT.mc_id=AZ-MVP-5003556)
- **Microsoft Learn**: [Azure SQL – Documentation Hub](https://learn.microsoft.com/en-us/azure/azure-sql/?view=azuresql&WT.mc_id=AZ-MVP-5003556)
- **YouTube**: [Azure Cosmos DB Tutorial](https://www.youtube.com/watch?v=BgvEOkcR0Wk)
- **YouTube**: [Azure SQL Overview](https://www.youtube.com/watch?v=R_Fi59j6BMo)

### 📡 **Azure IoT**
- **Azure Products**: [IoT Hub](https://azure.microsoft.com/en-us/products/iot-hub/?WT.mc_id=AZ-MVP-5003556)
- **Microsoft Learn**: [IoT Hub Documentation](https://learn.microsoft.com/en-us/azure/iot-hub/?WT.mc_id=AZ-MVP-5003556)
- **Azure Products**: [IoT Central](https://azure.microsoft.com/en-us/products/iot-central/?WT.mc_id=AZ-MVP-5003556)
- **Microsoft Learn**: [IoT Central Documentation](https://learn.microsoft.com/en-us/azure/iot-central/?WT.mc_id=AZ-MVP-5003556)
- **Azure Products**: [Azure Sphere](https://azure.microsoft.com/en-us/products/azure-sphere/?WT.mc_id=AZ-MVP-5003556)
- **Microsoft Learn**: [What is Azure Sphere?](https://learn.microsoft.com/en-us/azure-sphere/product-overview/what-is-azure-sphere?view=azure-sphere-integrated&WT.mc_id=AZ-MVP-5003556)

### 📊 **Azure Big Data & Analytics**
- **Azure Products**: [Azure Synapse Analytics](https://azure.microsoft.com/en-us/products/synapse-analytics/?WT.mc_id=AZ-MVP-5003556)
- **Microsoft Learn**: [What is Azure Synapse (SQL Data Warehouse)?](https://learn.microsoft.com/en-us/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-overview-what-is?WT.mc_id=AZ-MVP-5003556)
- **Azure Products**: [Azure HDInsight](https://azure.microsoft.com/en-us/products/hdinsight/?WT.mc_id=AZ-MVP-5003556)
- **Microsoft Learn**: [HDInsight Documentation](https://learn.microsoft.com/en-us/azure/hdinsight/?WT.mc_id=AZ-MVP-5003556)
- **Azure Products**: [Azure Databricks](https://azure.microsoft.com/en-us/products/databricks/?WT.mc_id=AZ-MVP-5003556)
- **Microsoft Learn**: [Azure Databricks Introduction](https://learn.microsoft.com/en-us/azure/databricks/introduction/?WT.mc_id=AZ-MVP-5003556)
- **Wikipedia**: [Big Data](https://en.wikipedia.org/wiki/Big_data)

### 🤖 **Artificial Intelligence & Machine Learning**
- **Azure Products**: [Azure Machine Learning](https://azure.microsoft.com/en-us/products/machine-learning/?WT.mc_id=AZ-MVP-5003556)
- **Microsoft Learn**: [What is Azure Machine Learning?](https://learn.microsoft.com/en-us/azure/machine-learning/overview-what-is-azure-machine-learning?view=azureml-api-2&WT.mc_id=AZ-MVP-5003556)
- **Microsoft Learn (Module)**: [Get started with AI fundamentals](https://learn.microsoft.com/en-us/training/modules/get-started-ai-fundamentals/1-introduction?WT.mc_id=AZ-MVP-5003556)

### ⚡ **Serverless Computing**
- **Azure Products**: [Azure Functions](https://azure.microsoft.com/en-us/products/functions/?WT.mc_id=AZ-MVP-5003556)
- **Microsoft Learn**: [Azure Functions Documentation](https://learn.microsoft.com/en-us/azure/azure-functions/?WT.mc_id=AZ-MVP-5003556)
- **Azure Products**: [Azure Logic Apps](https://azure.microsoft.com/en-us/products/logic-apps/?WT.mc_id=AZ-MVP-5003556)
- **Microsoft Learn**: [Azure Logic Apps Documentation](https://learn.microsoft.com/en-us/azure/logic-apps/?WT.mc_id=AZ-MVP-5003556)
- **Azure Products**: [Azure Event Grid](https://azure.microsoft.com/en-us/products/event-grid/?WT.mc_id=AZ-MVP-5003556)
- **Microsoft Learn**: [Azure Event Grid Documentation](https://learn.microsoft.com/en-us/azure/event-grid/overview?WT.mc_id=AZ-MVP-5003556)

### 🛠️ **DevOps**
- **Azure Products**: [Azure DevOps](https://azure.microsoft.com/en-us/products/devops/?WT.mc_id=AZ-MVP-5003556)
- **Microsoft Learn**: [Azure DevOps Documentation](https://learn.microsoft.com/en-us/azure/devops/?view=azure-devops&viewFallbackFrom=azure-devops%3Fwt.mc_id%3Daz-mvp-5003556)
- **Azure Products**: [Azure DevTest Labs](https://azure.microsoft.com/en-us/products/devtest-lab/?WT.mc_id=AZ-MVP-5003556)
- **Microsoft Learn**: [Azure DevTest Labs Overview](https://learn.microsoft.com/en-us/azure/devtest-labs/devtest-lab-overview?WT.mc_id=AZ-MVP-5003556)
