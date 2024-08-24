---
title: az104 - Networking Übersicht
description: description
authors: niclasedge
images:
- default.png
tags:
- azure
- networking
toc_max_heading_level: 5
created: 03.07.2024
---

## Azure Networking Services Overview

Description: This diagram illustrates the main Azure networking services, their key features, and relationships.

```mermaid
stateDiagram-v2
    [*] --> AzureNetworking

    state AzureNetworking {
        state "Azure Virtual Network\nIsolate and segment Azure resources" as VNet {
            state "Subnets\nLogical divisions of IP address space" as Subnets
            state "Network Security Groups\nFilter network traffic to and from resources" as NSG
            state "Route Tables\nControl network traffic routing" as RouteTables
        }
        
        state "Azure Load Balancer\nDistribute network traffic across resources" as LoadBalancer {
            state "Public Load Balancer\nLoad balance internet traffic to VMs" as PublicLB
            state "Internal Load Balancer\nLoad balance traffic inside a VNet" as InternalLB
        }
        
        state "Azure VPN Gateway\nConnect on-premises networks to Azure" as VPNGateway {
            state "Site-to-Site VPN\nConnect on-premises to Azure over IPsec/IKE" as S2SVPN
            state "Point-to-Site VPN\nConnect individual devices to Azure" as P2SVPN
            state "VNet-to-VNet VPN\nConnect Azure VNets in different regions" as V2VVPN
        }
    }

    VNet --> Subnets
    VNet --> NSG
    VNet --> RouteTables

    LoadBalancer --> PublicLB
    LoadBalancer --> InternalLB

    VPNGateway --> S2SVPN
    VPNGateway --> P2SVPN
    VPNGateway --> V2VVPN

    %% Connections between services
    VNet --> LoadBalancer : Hosts load-balanced resources
    VNet --> VPNGateway : Connects to on-premises
    LoadBalancer --> VPNGateway : Can load balance VPN connections

    %% Warnings
    state "Warnings" as Warnings {
        state "VNet peering required for inter-VNet communication" as PeeringWarning
        state "Load Balancer SKUs have different features and limits" as LBWarning
        state "VPN Gateway bandwidth caps based on SKU" as VPNBandwidthWarning
    }

    AzureNetworking --> Warnings : Important considerations
```

Metadata:
- Version: Azure Networking Services 2023
- Last Updated: July 2023
- Responsible Team: Azure Networking Team

Key Features:
1. Azure Virtual Network:
   - Provides network isolation and segmentation
   - Enables communication between Azure resources, internet, and on-premises networks
   - Supports network security groups and user-defined routing

2. Azure Load Balancer:
   - Distributes incoming traffic across multiple instances
   - Provides high availability and performance for applications
   - Supports both public (internet-facing) and internal load balancing

3. Azure VPN Gateway:
   - Enables secure connections between Azure and on-premises networks
   - Supports various VPN types: Site-to-Site, Point-to-Site, and VNet-to-VNet
   - Provides encrypted tunnels over the public internet

Warnings:
- VNet peering is required for communication between different virtual networks
- Load Balancer features and limits vary depending on the chosen SKU (Basic vs. Standard)
- VPN Gateway bandwidth is capped based on the selected SKU, affecting connection speeds

This diagram provides an overview of Azure's main networking services, their key components, and relationships. It highlights how these services work together to create secure, scalable, and performant network architectures in Azure.

Key points to note:
- Virtual Networks form the foundation of Azure networking, providing isolation and segmentation.
- Load Balancers can distribute traffic to resources within a VNet or across VNets.
- VPN Gateways enable secure connectivity between Azure and on-premises networks or between Azure VNets in different regions.