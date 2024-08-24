---
{}
---
# Azure VM Backup & Recovery

## 1. Intro
- Azure Backup: Protects VMs against data loss/corruption
- Key services: MARS agent, MABS, managed disk snapshots, Site Recovery

## 2. Objectives
- Identify VM backup features & use cases
- Configure VM snapshots & backup options
- Implement VM backup/restore, incl. soft delete
- Perform site-to-site recovery with Azure Site Recovery
- Compare VM backup options

## 3. Prerequisites
- Azure & on-prem VM knowledge
- Understanding of enterprise backup/storage
- Basic data protection & disaster recovery knowledge

## 4. Core Functionality

### Azure Site Recovery
- Replicates workloads to secondary location
- Supports: Azure VMs, on-prem VMs, physical servers, AWS instances
- Benefits: Consolidated management, ↓ cost/complexity, continuous replication

### Backup Options
1. Azure Backup: Full VM snapshots, app-consistent
2. Site Recovery: Region-wide disaster protection
3. Managed disk snapshots: Point-in-time backups
4. Managed disk images: Custom VM templates

### Recovery Services Vault
- Stores backup data & config info
- Supports various Azure services (IaaS VMs, SQL DBs, etc.)

## 5. Implementation Guide

### Create VM Snapshot
1. Azure Backup job: 2 phases
   a. Take VM data snapshot
   b. Transfer to Recovery Services vault
2. Set snapshot retention (1-5 days)

### Set Up Recovery Services Vault
1. Create vault in target region
2. Choose replication: Geo-redundant (GRS) or Locally redundant (LRS)
3. Define backup policy (frequency, retention)

### Back Up VM
1. Create Recovery Services vault
2. Define backup policy
3. Run Azure Backup job

### Restore VM
1. Access snapshot/recovery point
2. Trigger restore operation
3. Monitor job notifications

### Implement Soft Delete
1. Stop active backup job
2. Apply soft-delete state (14-day retention)
3. Undelete backup items if needed
4. Restore items
5. Resume backups

## 6. Best Practices
- Use soft delete to protect against accidental deletion
- Configure appropriate snapshot retention based on needs
- Regularly test restore processes

## 7. Resources
- [Azure VM backup overview](https://docs.microsoft.com/azure/backup/backup-azure-vms-introduction)
- [Quick-start: Back up a VM](https://docs.microsoft.com/azure/backup/quick-backup-vm-portal)
- [Set up disaster recovery for Azure VM](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)