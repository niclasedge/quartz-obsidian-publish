---
{}
---
# Azure VM Scaling & Availability

## 1. Intro
- Azure VMs: Manage at scale w/ varying usage patterns
- Key benefits: Adjust resources to match demand, maintain consistency, ↑ throughput & responsiveness, ↓ costs

## 2. Objectives
- Implement availability sets/zones
- Implement update/fault domains
- Implement VM Scale Sets
- Autoscale VMs

## 3. Prerequisites
- Azure VM creation/management knowledge
- Understanding of scaling infrastructure for fluctuating workloads

## 4. Core Functionality

### Availability Options
- **Availability Sets**: Logical grouping for VMs
  - Ensures VMs deploy across multiple physical servers, racks, storage, & network switches
  - ↑ fault tolerance
- **Availability Zones**: Unique physical locations in Azure region
  - Combination of fault domain & update domain
  - Min. 3 separate zones per enabled region

### Update & Fault Domains
- Update Domain: Group of nodes upgraded together
  - Default: 5 (non-configurable), max: 20
- Fault Domain: Group sharing common hardware/single point of failure

### VM Scale Sets
- Deploy/manage identical VMs
- Supports up to 1000 VM instances (600 for custom images)
- Enables true autoscaling

## 5. Implementation Guide

### Create Availability Set
1. Create VM & availability set simultaneously
2. Add VMs with identical functionality/software
3. Use Azure portal, ARM templates, scripts, or API tools

### Configure Autoscale
1. Enable autoscaling in Azure portal
2. Define min, max, & default VM instances
3. Set CPU thresholds & duration for scale out/in
4. Specify # of VMs to add/remove

### Create VM Scale Set
1. Choose orchestration mode (flexible/uniform)
2. Select base OS image
3. Choose VM architecture (x64/Arm64)
4. Set VM size
5. Configure advanced options (scaling beyond 100 instances, spreading algorithm)

## 6. Advanced Topics

### Vertical vs Horizontal Scaling
- Vertical (scale up/down): Adjust VM size
- Horizontal (scale out/in): Adjust # of VMs

### Autoscaling Considerations
- Automatic capacity adjustment
- Scale out for ↑ demand
- Scale in for ↓ demand
- Schedule events for fixed-time scaling
- ↓ management overhead

## 7. Monitoring & Maintenance
- Monitor CPU usage & other metrics
- Regularly review autoscale rules
- Adjust thresholds as needed

## 8. Best Practices
- Use availability sets for redundancy
- Separate application tiers into different availability sets
- Implement load balancing for high availability
- Use managed disks with availability sets

## 9. Resources
- [Azure VMs Availability Options](https://docs.microsoft.com/azure/virtual-machines/availability)
- [Autoscale with VM Scale Sets](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview)
- [Create VM Scale Sets in Azure Portal](https://docs.microsoft.com/azure/virtual-machine-scale-sets/flexible-virtual-machine-scale-sets-portal)