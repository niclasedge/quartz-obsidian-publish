---
{}
---
# Azure Virtual Machine Configuration

## 1. Introduction
- Azure VMs: On-demand, scalable compute resources
- Key benefits: Greater control over computing environment

## 2. Objectives
- Configure VM names, locations, sizes, storage
- Understand pricing models
- Create VMs in Azure portal
- Select secure connection methods
- Configure Windows/Linux VM connections

## 3. Prerequisites
- Cloud computing & IaaS concepts
- Azure fundamentals (subscriptions, resource groups, storage)
- Basic networking knowledge
- Azure portal familiarity

## 4. Core Functionality

### Shared Responsibility Model
- IaaS: Customer manages OS, storage, networking
- PaaS: Customer manages applications & data
- SaaS: Customer manages data & access

### Planning Considerations
1. Network configuration
2. VM naming conventions
3. Location selection
4. Size determination
5. Pricing model & cost estimation
6. Storage selection
7. OS choice

### Sizing Options
- General purpose: Balanced CPU-to-memory ratio
- Compute optimized: High CPU-to-memory ratio
- Memory optimized: High memory-to-CPU ratio
- Storage optimized: High disk throughput/IO
- GPU: For graphics-intensive workloads
- High performance compute: Fastest CPUs, high-throughput networking

### Storage Options
- OS disk: Pre-installed OS
- Temporary disk: Non-persistent storage
- Data disks: For application data
- Premium Storage: High-performance SSDs
- Managed disks: Azure-managed VHDs

## 5. Implementation Guide

### Create VM in Azure Portal
1. Choose image (Windows/Linux)
2. Configure basic settings
3. Set up disks
4. Configure networking
5. Set up management options
6. Review & create

### Connect to VMs
- Windows: Use Remote Desktop Protocol (RDP)
- Linux: Use Secure Shell (SSH)
- Azure Bastion: Secure, seamless RDP/SSH over SSL

## 6. Best Practices
- Use meaningful, consistent VM names
- Choose appropriate VM size for workload
- Implement Azure Managed Disks
- Secure VM connections (Azure Bastion or SSH keys)
- Regularly monitor VM performance

## 7. Resources
- [Azure VMs documentation](https://docs.microsoft.com/azure/virtual-machines/)
- [VM size selector](https://azure.microsoft.com/pricing/vm-selector/)
- [Intro to Azure VMs (sandbox)](https://docs.microsoft.com/training/modules/intro-to-azure-virtual-machines/)