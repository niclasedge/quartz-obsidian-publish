---
title: az104 - Databases Übersicht
description: description
authors: niclasedge
images:
- default.png
tags:
- azure
- database
toc_max_heading_level: 5
created: 02.07.2024
---

## Azure Database Services Overview

Description: This diagram illustrates the main Azure database services, their key features, and relationships.

```mermaid
stateDiagram-v2
    [*] --> AzureDatabases

    state AzureDatabases {
        state "Azure SQL Database\nManaged relational database service" as SQLDatabase {
            state "Elastic Pool\nResource sharing for multiple databases" as ElasticPool
            state "Hyperscale\nHighly scalable storage and compute" as Hyperscale
            state "Managed Instance\nFull SQL Server compatibility" as ManagedInstance
        }
        
        state "Azure Cosmos DB\nGlobally distributed, multi-model database" as CosmosDB {
            state "SQL API\nDocument database with SQL querying" as SQLAPI
            state "MongoDB API\nMongoDB-compatible document database" as MongoAPI
            state "Cassandra API\nWide-column database" as CassandraAPI
            state "Gremlin API\nGraph database" as GremlinAPI
            state "Table API\nKey-value database" as TableAPI
        }
        
        state "Azure Database for MySQL\nManaged open-source MySQL database" as MySQLDB
        
        state "Azure Database for PostgreSQL\nManaged open-source PostgreSQL database" as PostgreSQLDB {
            state "Single Server\nFully managed single PostgreSQL server" as SingleServer
            state "Flexible Server\nMore control and flexibility" as FlexibleServer
            state "Hyperscale (Citus)\nHorizontally scalable PostgreSQL" as HyperscaleCitus
        }
    }

    SQLDatabase --> ElasticPool
    SQLDatabase --> Hyperscale
    SQLDatabase --> ManagedInstance

    CosmosDB --> SQLAPI
    CosmosDB --> MongoAPI
    CosmosDB --> CassandraAPI
    CosmosDB --> GremlinAPI
    CosmosDB --> TableAPI

    PostgreSQLDB --> SingleServer
    PostgreSQLDB --> FlexibleServer
    PostgreSQLDB --> HyperscaleCitus

    %% Connections between services
    SQLDatabase --> CosmosDB : Data migration
    MySQLDB --> PostgreSQLDB : Data migration
    CosmosDB --> SQLDatabase : Analytics integration

    %% Warnings
    state "Warnings" as Warnings {
        state "Not all features available in all regions" as RegionWarning
        state "Pricing varies by service and tier" as PricingWarning
        state "Some services have specific scaling limits" as ScalingWarning
    }

    AzureDatabases --> Warnings : Important considerations
```

Metadata:
- Version: Azure Database Services 2023
- Last Updated: July 2023
- Responsible Team: Azure Data Team

Key Features:
1. Azure SQL Database:
   - Fully managed SQL Server database engine
   - Built-in intelligence and security
   - High availability and disaster recovery options

2. Azure Cosmos DB:
   - Multi-model database with global distribution
   - Guaranteed single-digit millisecond response times
   - Automatic and instant scalability

3. Azure Database for MySQL:
   - Fully managed and scalable MySQL database
   - Built-in high availability
   - Automated backups and point-in-time restore

4. Azure Database for PostgreSQL:
   - Fully managed and scalable PostgreSQL database
   - Built-in intelligence and security
   - Multiple deployment options for various workloads

Warnings:
- Not all features are available in all Azure regions
- Pricing can vary significantly between services and tiers
- Some services have specific scaling limits that may affect large-scale deployments

This diagram provides an overview of Azure's main database services, their key components, and relationships. It highlights the versatility of Azure's database offerings, from relational to NoSQL and open-source options, each with its own set of features and deployment models.
