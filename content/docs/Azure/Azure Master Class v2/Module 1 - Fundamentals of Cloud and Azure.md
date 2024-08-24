---
title: Module 01 - Fundamentals of Cloud and Azure
description: overview
authors: niclasedge
images: null
hide_table_of_contents: false
tags:
- Azure
- Active
- Directory
- Identity
---
# Azure and Cloud Computing Fundamentals

## Types of Cloud Services

```mermaid
graph TD
    A[Cloud Services] --> B[Public Cloud]
    A --> C[Private Cloud]
    A --> D[Hybrid Cloud]
    A --> E[Community Cloud]
    B --> F[Azure]
    B --> G[AWS]
    B --> H[Google Cloud]
    C --> I[On-premises]
    C --> J[Hosted Private Cloud]
    D --> K[Mix of Public and Private]
    E --> L[Shared among organizations]
```

- Public Cloud: Accessible over the internet, shared resources (e.g., Azure, AWS, Google Cloud)
- Private Cloud: Dedicated to a single organization, can be on-premises or hosted
- Hybrid Cloud: Combination of public and private clouds
- Community Cloud: Shared by several organizations with common concerns

## Cloud Service Models

```mermaid
graph TD
    A[Cloud Service Models] --> B[IaaS]
    A --> C[PaaS]
    A --> D[SaaS]
    B --> E[Virtual Machines]
    B --> F[Storage]
    B --> G[Networking]
    C --> H[App Services]
    C --> I[Databases]
    C --> J[Containers]
    D --> K[Office 365]
    D --> L[Dynamics 365]
    D --> M[Salesforce]
```

- IaaS (Infrastructure as a Service): Provides virtualized computing resources
- PaaS (Platform as a Service): Offers development and deployment environments
- SaaS (Software as a Service): Delivers software applications over the internet

## Core Characteristics of Cloud Computing

```mermaid
graph TD
    A[Cloud Characteristics] --> B[On-demand self-service]
    A --> C[Broad network access]
    A --> D[Resource pooling]
    A --> E[Rapid elasticity]
    A --> F[Measured service]
    B --> G[Automatic provisioning]
    C --> H[Access from various devices]
    D --> I[Multi-tenant model]
    E --> J[Scale up/down quickly]
    F --> K[Pay-per-use billing]
```

1. On-demand self-service: Users can provision resources without human interaction
2. Broad network access: Services are available over the network and accessed through standard mechanisms
3. Resource pooling: Provider's resources are pooled to serve multiple consumers
4. Rapid elasticity: Capabilities can be elastically provisioned and released to scale with demand
5. Measured service: Resource usage is monitored, controlled, and reported

## Benefits of Public Cloud

```mermaid
graph TD
    A[Public Cloud Benefits] --> B[Cost Efficiency]
    A --> C[Scalability]
    A --> D[Global Reach]
    A --> E[High Availability]
    A --> F[Faster Innovation]
    B --> G[OpEx vs CapEx]
    B --> H[Pay-as-you-go]
    C --> I[Auto-scaling]
    C --> J[Handle traffic spikes]
    D --> K[Multiple regions]
    D --> L[Edge locations]
    E --> M[SLAs]
    E --> N[Redundancy]
    F --> O[Managed services]
    F --> P[Rapid deployment]
```

- Cost Efficiency: Pay for what you use, reduce capital expenses
- Scalability: Easily scale resources up or down based on demand
- Global Reach: Deploy applications closer to users worldwide
- High Availability: Built-in redundancy and fault tolerance
- Faster Innovation: Access to latest technologies and managed services

## Microsoft Azure Services

```mermaid
graph TD
    A[Azure Services] --> B[Compute]
    A --> C[Storage]
    A --> D[Networking]
    A --> E[Databases]
    A --> F[AI/ML]
    A --> G[IoT]
    A --> H[Security]
    B --> I[VMs]
    B --> J[App Service]
    B --> K[Functions]
    C --> L[Blob Storage]
    C --> M[File Storage]
    C --> N[Disk Storage]
    D --> O[Virtual Network]
    D --> P[Load Balancer]
    D --> Q[VPN Gateway]
    E --> R[SQL Database]
    E --> S[Cosmos DB]
    E --> T[PostgreSQL]
    F --> U[Cognitive Services]
    F --> V[Machine Learning]
    G --> W[IoT Hub]
    G --> X[IoT Central]
    H --> Y[Azure AD]
    H --> Z[Key Vault]
```

Azure offers a comprehensive set of services across various categories, including compute, storage, networking, databases, AI/ML, IoT, and security.

## Getting Started with Azure

```mermaid
graph TD
    A[Azure Access Options] --> B[Free Trial]
    A --> C[Pay-as-you-go]
    A --> D[Enterprise Agreement]
    A --> E[Visual Studio Subscription]
    B --> F[$200 credit for 30 days]
    B --> G[12 months of free services]
    C --> H[No upfront costs]
    C --> I[Pay only for what you use]
    D --> J[Bulk discounts]
    D --> K[Centralized billing]
    E --> L[$50-$150 monthly credit]
    E --> M[Dev/Test pricing]
```

- Free Trial: Offers $200 credit for 30 days and 12 months of free services
- Pay-as-you-go: No upfront costs, pay only for what you use
- Enterprise Agreement: For large organizations, offers bulk discounts and centralized management
- Visual Studio Subscription: Includes monthly Azure credit for development and testing

## Azure Reliability and Resiliency

```mermaid
graph TD
    A[Azure Reliability] --> B[Software-based Resilience]
    A --> C[Multiple Instances]
    A --> D[Load Balancing]
    A --> E[Auto-scaling]
    B --> F[Fault Domains]
    B --> G[Update Domains]
    C --> H[Availability Sets]
    C --> I[Availability Zones]
    D --> J[Azure Load Balancer]
    D --> K[Traffic Manager]
    E --> L[VM Scale Sets]
    E --> M[App Service Auto-scaling]
```

- Software-based Resilience: Focus on distributing workloads across multiple instances
- Multiple Instances: Use of availability sets and zones for redundancy
- Load Balancing: Distribute traffic across multiple instances
- Auto-scaling: Automatically adjust resources based on demand

## Why Choose Azure

```mermaid
graph TD
    A[Azure Advantages] --> B[Market Leadership]
    A --> C[Comprehensive Services]
    A --> D[Hybrid Capabilities]
    A --> E[Security and Compliance]
    A --> F[Integration with Microsoft Ecosystem]
    B --> G[Gartner Magic Quadrant Leader]
    C --> H[Wide range of services]
    C --> I[Regular new feature releases]
    D --> J[Azure Arc]
    D --> K[Azure Stack]
    E --> L[Azure Active Directory]
    E --> M[Compliance certifications]
    F --> N[Integration with Office 365]
    F --> O[Windows Server integration]
```

- Market Leadership: Consistently ranked as a leader in Gartner Magic Quadrant
- Comprehensive Services: Wide range of services covering various IT needs
- Hybrid Capabilities: Strong support for hybrid cloud scenarios
- Security and Compliance: Advanced security features and compliance certifications
- Integration with Microsoft Ecosystem: Seamless integration with other Microsoft products and services