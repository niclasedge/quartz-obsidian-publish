---
title: Azure Services Map
description: description
authors: niclasedge
images:
- default.png
tags:
- azure
- networking
toc_max_heading_level: 5
created: 05.07.2024
---

### Compute Services
```mermaid
mindmap
  root((Compute Services))
    Virtual Machines
      :: scales with
      Virtual Machine Scale Sets
      :: uses
      Azure Dedicated Host
    Azure Kubernetes Service
      :: orchestrates
      Container Instances
      :: uses
      Virtual Machines
    Azure Functions
      :: part of
      Serverless Compute
      :: integrates with
      App Service
    App Service
      :: hosts
      Web Apps
      API Apps
      Mobile Apps
    Azure Batch
      :: manages
      Large-scale parallel and HPC applications
    Azure Service Fabric
      :: builds and operates
      Microservices and containerized applications
    Azure CycleCloud
      :: orchestrates
      High-Performance Computing (HPC) clusters
```


### Storage Services
```mermaid
mindmap
  root((Storage Services))
    Blob Storage
      :: stores
      Unstructured data
      :: used by
      Data Lake Storage Gen2
    File Storage
      :: provides
      Fully managed file shares
    Queue Storage
      :: enables
      Asynchronous message queueing
    Table Storage
      :: stores
      Semi-structured NoSQL data
    Disk Storage
      :: provides
      Block-level storage volumes for VMs
    Data Lake Storage
      :: optimized for
      Big data analytics workloads
      :: integrates with
      Azure Synapse Analytics
```

### Network Services
```mermaid
mindmap
  root((Networking Services))
    Virtual Network
      :: connects to
      VPN Gateway
      ExpressRoute
    Load Balancer
      :: distributes
      Network traffic
    Application Gateway
      :: manages
      Web traffic
    VPN Gateway
      :: connects
      On-premises to Azure
    ExpressRoute
      :: provides
      Private connections to Azure
    Content Delivery Network
      :: delivers
      High-bandwidth content
    DDoS Protection
      :: defends against
      Distributed Denial of Service attacks
    DNS
      :: manages
      Domain name systems
    Azure Firewall
      :: protects
      Virtual Network resources
    Azure Bastion
      :: provides
      Secure VM access
```

### Compute Services
```mermaid
mindmap
  root((Database Services))
    Azure SQL Database
      :: provides
      Managed SQL Server databases
    Azure Cosmos DB
      :: offers
      Globally distributed, multi-model database
    Azure Database for MySQL
      :: manages
      MySQL databases
    Azure Database for PostgreSQL
      :: manages
      PostgreSQL databases
    Azure Database for MariaDB
      :: manages
      MariaDB databases
    Azure Synapse Analytics
      :: integrates
      Big data and data warehousing
    Azure Cache for Redis
      :: improves
      Application performance and scale
```

### Azure AI and Machine Learing Services
```mermaid
mindmap
  root((AI and Machine Learning Services))
    Azure Machine Learning
      :: provides
      End-to-end ML lifecycle management
      :: uses
      Automated ML
      :: integrates with
      Azure Databricks
    Azure Cognitive Services
      :: offers
      Vision
      Speech
      Language
      Decision
    Azure Bot Service
      :: builds
      Intelligent bots
      :: uses
      Language Understanding (LUIS)
    Azure Databricks
      :: enables
      Big data analytics and AI solutions
    Azure Open Datasets
      :: provides
      Curated datasets for ML models
```

### Compute Services
```mermaid

```