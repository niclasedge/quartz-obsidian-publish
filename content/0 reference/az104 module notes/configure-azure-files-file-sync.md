---
{}
---
	# Azure Files and Azure File Sync Technical Documentation

## 1. Azure Files Overview
- Fully managed file shares in the cloud
- Accessible via SMB and NFS protocols
- Use cases: Replace on-premises file servers, lift-and-shift apps, shared application settings

## 2. Azure Files vs. Blob Storage vs. Azure Disks
| Feature | Azure Files | Blob Storage | Azure Disks |
|---------|-------------|--------------|-------------|
| Access | SMB, NFS, REST | REST | REST |
| Structure | Directory objects | Flat namespace | 512-byte pages |
| Best for | File system APIs, shared data | Streaming, random access | Frequent read/write ops |

## 3. Azure File Shares
- Types: Standard (HDD) and Premium (SSD)
- SMB shares: Open port 445, enable secure transfer
- Mounting: Windows (PowerShell), Linux (CIFS kernel client)

## 4. File Share Snapshots
- Point-in-time, read-only copies
- Incremental and share-level
- Use cases: Protect against errors, accidental deletions, backups

## 5. Soft Delete for Azure Files
- Recover deleted files and shares
- 1-365 day retention period
- Storage account level feature
- Not available for NFS shares

## 6. Azure Storage Explorer
- Standalone app for Windows, macOS, Linux
- Manage multiple accounts and subscriptions
- Connection options: Azure subscription, local development, external storage, SAS

## 7. Azure File Sync
- Cache Azure Files shares on Windows Server or cloud VM
- Features:
  - Multi-site access
  - Cloud tiering (optional)
  - Backup and disaster recovery
- Use cases: Branch offices, file archiving, application lift and shift

## 8. Best Practices
- Use premium tier for performance-sensitive workloads
- Enable soft delete for data protection
- Implement file share snapshots for point-in-time recovery
- Use Azure File Sync for distributed caching and tiering

## 9. Additional Resources
- [Azure Files documentation](https://docs.microsoft.com/en-us/azure/storage/files/)
- [Azure File Sync documentation](https://docs.microsoft.com/en-us/azure/storage/file-sync/)
- [Introduction to Azure Files](https://docs.microsoft.com/en-us/training/modules/introduction-to-azure-files/)
- [Implement a hybrid file server infrastructure](https://docs.microsoft.com/en-us/training/modules/implement-hybrid-file-server-infrastructure/)