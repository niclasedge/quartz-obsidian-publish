---
title: Az Infra Update July 12, 2024
description: A summary of recent Azure infrastructure updates and announcements
authors: niclasedge
images: null
tags:
- azure
toc_max_heading_level: 5
created: 06.07.2024
---
# Az Infra Update - July 13, 2024

## Overview

```mermaid
gantt
    title Azure Infrastructure Updates
    dateFormat  YYYY-MM-DD
    section Compute
    Retirement of Guest OS Families 2,3,4 (Windows 2008 R2)    :milestone, 2024-12-31, 0d
    Retirement of Guest OS Families 2,3,4 (Windows 2012/R2)    :milestone, 2025-02-28, 0d
    section Networking
    AKS Network Observability GA    :milestone, 2024-07-13, 0d
    section Storage
    Elastic SAN Updates GA    :milestone, 2024-07-13, 0d
    section Identity
    Entra Suite Announcement    :milestone, 2024-07-13, 0d
    section Backup & Recovery
    Azure Backup Vault CMK Support    :milestone, 2024-07-13, 0d
    Azure Backup PE-enabled Disk Support    :milestone, 2024-07-13, 0d
    ASR Trusted Launch VM Support GA    :milestone, 2024-07-13, 0d
```

## Compute

### Retirement of Guest OS Families for Azure Cloud Services - December 2024 / February 2025

- Windows Server 2008 R2 retiring on December 31, 2024
- Windows Server 2012 and 2012 R2 retiring on February 28, 2025
- Recommendation to upgrade to newer OS versions like Windows Server 2022 (OS Family 7)

```mermaid
classDiagram
    class AzureCloudServices {
        +RetireGuestOSFamilies()
    }
    class WindowsServer2008R2 {
        -RetirementDate: Dec 31, 2024
    }
    class WindowsServer2012 {
        -RetirementDate: Feb 28, 2025
    }
    class WindowsServer2012R2 {
        -RetirementDate: Feb 28, 2025
    }
    class WindowsServer2022 {
        +RecommendedUpgrade
    }
    AzureCloudServices --> WindowsServer2008R2
    AzureCloudServices --> WindowsServer2012
    AzureCloudServices --> WindowsServer2012R2
    AzureCloudServices --> WindowsServer2022
```

## Networking

### AKS Network Observability - Generally Available

- Based on Hubble
- Works for Linux workloads (Cilium and non-Cilium data planes)
- Provides pod-level metrics, DNS metrics, Layer 4 connections, and enhanced debug capabilities
- Integrates with Azure Monitor's managed service for Prometheus
- Pre-built dashboard in Azure Managed Grafana

```mermaid
flowchart TD
    AKS[AKS Cluster] --> NO[Network Observability]
    NO --> Hubble[Hubble]
    NO --> Linux[Linux Workloads]
    Linux --> Cilium[Cilium Data Plane]
    Linux --> NonCilium[Non-Cilium Data Plane]
    NO --> Metrics[Metrics Collection]
    Metrics --> PodMetrics[Pod-level Metrics]
    Metrics --> DNSMetrics[DNS Metrics]
    Metrics --> L4Connections[Layer 4 Connections]
    NO --> Debug[Enhanced Debug Capabilities]
    NO --> AzureMonitor[Azure Monitor]
    AzureMonitor --> Prometheus[Managed Prometheus]
    AzureMonitor --> Grafana[Managed Grafana]
    Grafana --> Dashboard[Pre-built Dashboard]
```

## Storage

### Azure Elastic SAN Updates - Generally Available

- Ability to delete unused space and scale down SAN size
- Diagnostic settings for all logs or just audit logs
- New regions added for service availability

```mermaid
classDiagram
    class AzureElasticSAN {
        +DeleteUnusedSpace()
        +ScaleDown()
        +EnableDiagnosticSettings()
    }
    class DiagnosticSettings {
        +AllLogs
        +AuditLogs
    }
    class AzureStorage {
        +StorageClusters
    }
    class iSCSITarget {
        +NetworkConnection
    }
    AzureElasticSAN --> DiagnosticSettings
    AzureElasticSAN --> AzureStorage
    AzureElasticSAN --> iSCSITarget
    iSCSITarget --> AzureVMwareSolution
    iSCSITarget --> AzureContainerStorage
    iSCSITarget --> CustomWorkloads
```

## Identity

### Entra Suite Announcement

- Combines multiple Entra components for $12/month (requires Entra ID P1 license)
- Includes:
  - Entra ID Protection
  - Entra ID Governance
  - Entra Verified ID
  - Entra Internet Access
  - Entra Private Access

```mermaid
flowchart TD
    EntraSuite[Entra Suite $12/month] --> EntraIDP1[Entra ID P1 License Required]
    EntraSuite --> EntraIDProtection[Entra ID Protection]
    EntraSuite --> EntraIDGovernance[Entra ID Governance]
    EntraSuite --> EntraVerifiedID[Entra Verified ID]
    EntraSuite --> EntraInternetAccess[Entra Internet Access]
    EntraSuite --> EntraPrivateAccess[Entra Private Access]
    EntraInternetAccess --> ConditionalAccess[Conditional Access]
    EntraInternetAccess --> Categories[Access Categories]
    EntraPrivateAccess --> GSAClient[Global Secure Access Client]
    EntraPrivateAccess --> TCPUDPSupport[TCP/UDP Support]
    EntraPrivateAccess --> EntraEdge[Entra Edge]
    EntraEdge --> VerifiableConnection[Constantly Verifiable Connection]
```

## Backup & Recovery

### Azure Backup Vault Customer Managed Key (CMK) Support

- Allows customers to use their own keys for encrypting backup content
- Keys can be managed and rotated in Azure Key Vault

### Azure Backup Private Endpoint-enabled Disk Support

- Supports backup and restore of managed disks with private endpoint restrictions
- Restore options include:
  - Restoring with the same network settings
  - Restoring with additional network access
  - Enabling public access for operations

### Azure Site Recovery (ASR) Trusted Launch VM Support - Generally Available

- Supports replication of VMs with Trusted Launch features
- Includes VMs with virtual TPM, secure boot, and UEFI-based configuration
- Enables replication to other zones or regions

```mermaid
classDiagram
    class AzureBackup {
        +SupportCMK()
        +SupportPrivateEndpointEnabledDisks()
    }
    class AzureKeyVault {
        +ManageKeys()
        +RotateKeys()
    }
    class ManagedDisk {
        +PrivateEndpointRestrictions
    }
    class RestoreOptions {
        +SameNetworkSettings
        +AdditionalNetworkAccess
        +EnablePublicAccess
    }
    class AzureSiteRecovery {
        +SupportTrustedLaunchVMs()
    }
    class TrustedLaunchVM {
        +VirtualTPM
        +SecureBoot
        +UEFIBased
    }
    AzureBackup --> AzureKeyVault
    AzureBackup --> ManagedDisk
    ManagedDisk --> RestoreOptions
    AzureSiteRecovery --> TrustedLaunchVM
```

