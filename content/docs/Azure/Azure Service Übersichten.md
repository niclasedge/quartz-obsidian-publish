---
title: Azure Service Übersichten
description: description
authors: niclasedge
images:
- default.png
tags:
- azure
- networking
toc_max_heading_level: 5
created: 07.07.2024
---

Here is an overview of some of the most important Azure services:

• **Storage**: 
  - Azure Blob Storage - Object storage for unstructured data
  - Azure Files - Managed file shares for cloud or on-premises deployment
  - Azure Disk Storage - Block-level storage volumes for Azure VMs

• **Databases**:
  - Azure SQL Database - Managed relational database service
  - Azure Cosmos DB - Globally distributed, multi-model database
  - Azure Database for MySQL/PostgreSQL - Managed open-source databases

• **Networking**:
  - Azure Virtual Network - Isolate and segment Azure resources
  - Azure Load Balancer - Distribute network traffic across resources
  - Azure VPN Gateway - Connect on-premises networks to Azure

• **Security**:
  - Azure Active Directory - Cloud-based identity and access management
  - Azure Key Vault - Securely store and manage keys, secrets, and certificates
  - Azure Security Center - Unified security management and threat protection

• **Monitoring & Management**:
  - Azure Monitor - Collect, analyze, and act on telemetry data
  - Azure Resource Manager - Deploy, manage, and organize Azure resources

• **AI & Machine Learning**:
  - Azure Machine Learning - Build, train, and deploy ML models
  - Azure Cognitive Services - Add AI capabilities to applications

• **DevOps & Integration**:
  - Azure DevOps - Development collaboration tools including pipelines
  - Azure Logic Apps - Automate workflows and business processes

This overview covers some of the core Azure services across various categories. Each service is designed to address specific cloud computing needs and can be combined to create comprehensive solutions.

```mermaid
mindmap
  root((Azure Services))
    Compute
      Virtual Machines
        Run Windows and Linux VMs
      App Service
        Host web apps, mobile backends, and RESTful APIs
      Azure Kubernetes Service (AKS)
        Managed Kubernetes container orchestration
      Azure Functions
        Serverless compute for event-driven applications
    Networking
      Virtual Network
        Isolate and segment Azure resources
      Load Balancer
        Distribute network traffic across resources
      VPN Gateway
        Connect on-premises networks to Azure
      Azure CDN
        Deliver high-bandwidth content globally
    Storage
      Blob Storage
        Scalable object storage for unstructured data
      File Storage
        Fully managed file shares
      Queue Storage
        Message queuing for decoupled architectures
      Disk Storage
        Block-level storage volumes for Azure VMs
    Databases
      Azure SQL Database
        Managed relational database service
      Azure Cosmos DB
        Globally distributed, multi-model database
      Azure Database for MySQL
        Managed MySQL database service
      Azure Database for PostgreSQL
        Managed PostgreSQL database service
    AI + Machine Learning
      Azure Machine Learning
        Build, train, and deploy ML models
      Cognitive Services
        Add AI capabilities to applications
      Azure Bot Service
        Develop intelligent bots for natural communication
    Analytics
      Azure Synapse Analytics
        Limitless analytics service with data integration
      Azure Databricks
        Apache Spark-based analytics platform
      HDInsight
        Managed open-source analytics service
    Integration
      Logic Apps
        Automate workflows and business processes
      Service Bus
        Enterprise message broker and queues
      Event Grid
        Managed event routing service
    Identity
      Azure Active Directory
        Cloud-based identity and access management
      Azure AD B2C
        Customer identity and access management
    Security
      Azure Security Center
        Unified security management and threat protection
      Key Vault
        Securely store and manage keys, secrets, and certificates
    Management and Governance
      Azure Monitor
        Collect, analyze, and act on telemetry data
      Azure Policy
        Enforce organizational standards at scale
      Azure Resource Manager
        Deploy, manage, and organize Azure resources
    Developer Tools
      Azure DevOps
        Development collaboration tools including pipelines
      Visual Studio Code
        Lightweight code editor with Azure integrations
    IoT
      IoT Hub
        Managed service for bi-directional IoT communication
      IoT Central
        Fully managed IoT application platform
```


### Übersicht mit allen Optionen der Services
```mermaid
mindmap
  root((Azure Services))
    Storage
      Blob Storage
        Block Blobs
          Optimized for streaming and storing cloud objects
        Page Blobs
          Used for random read/write operations, VHDs
        Append Blobs
          Optimized for append operations like logging
        Access tiers
          Hot
            Frequent access, higher storage cost
          Cool
            Infrequent access, lower storage cost
          Archive
            Rarely accessed, lowest storage cost
      File Storage
        SMB file shares
        NFS file shares
      Queue Storage
        Message queuing
        Supports up to 64 KB per message
      Table Storage
        NoSQL key-attribute data store
      Disk Storage
        Ultra Disk
          Highest performance SSD
        Premium SSD
          High-performance production workloads
        Standard SSD
          General-purpose SSD
        Standard HDD
          Backup and non-critical workloads
    Databases
      Azure SQL Database
        Single Database
        Elastic Pool
        Managed Instance
        Hyperscale
      Azure Cosmos DB
        SQL API
        MongoDB API
        Cassandra API
        Gremlin API
        Table API
      Azure Database for MySQL
        Single Server
        Flexible Server
      Azure Database for PostgreSQL
        Single Server
        Flexible Server
        Hyperscale Citus
    Compute
      Virtual Machines
        Windows VMs
        Linux VMs
        Spot VMs
        Scale Sets
      App Service
        Web Apps
        Mobile Apps
        API Apps
        Web App for Containers
      Azure Kubernetes Service AKS
        Managed Kubernetes
        Dev Spaces
        Virtual Nodes
      Azure Functions
        HTTP trigger
        Timer trigger
        Queue trigger
        Event Grid trigger
        IoT Hub trigger
    Networking
      Virtual Network
      Load Balancer
      VPN Gateway
      Azure CDN
    AI + Machine Learning
      Azure Machine Learning
      Cognitive Services
      Azure Bot Service
    Analytics
      Azure Synapse Analytics
      Azure Databricks
      HDInsight
    Integration
      Logic Apps
      Service Bus
      Event Grid
    Identity
      Azure Active Directory
      Azure AD B2C
    Security
      Azure Security Center
      Key Vault
    Management and Governance
      Azure Monitor
      Azure Policy
      Azure Resource Manager
    Developer Tools
      Azure DevOps
      Visual Studio Code
    IoT
      IoT Hub
      IoT Central
```