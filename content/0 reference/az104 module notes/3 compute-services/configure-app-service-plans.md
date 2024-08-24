---
{}
---
Here is a compressed version of the technical documentation:

# Azure App Service Plans & Scaling

## 1. Intro
- Azure App Service plans define compute resources for web apps
- Scaling keeps apps responsive during high demand & saves $ when low
- Hotel website example: traffic fluctuates seasonally 

## 2. Objectives
- ID App Service features/use cases
- Select appropriate pricing tier
- Scale App Service plan
- Scale out App Service plan

## 3. Prerequisites 
- Basic scaling/performance knowledge
- Azure portal familiarity

## 4. Core Functionality

### App Service Plans
- Define: region, # of VMs, VM size
- Apps in plan share resources
- Scaling unit for apps

### Pricing Tiers
Tier | Usage | Apps | Disk | Autoscale | Slots | Max Instances
-----|-------|------|------|-----------|-------|---------------
Free/Shared | Dev/Test | 10-100 | 1 GB | No | 0 | n/a
Basic | Low traffic | ∞ | 10 GB | No | 0 | 3
Standard | Production | ∞ | 50 GB | Yes | 5 | 10
Premium | Enhanced perf | ∞ | 250 GB | Yes | 20 | 30 
Isolated | Mission-critical | ∞ | 1 TB | Yes | 20 | 100

### Scaling Methods
1. Scale Up: ↑ CPU, memory, disk (change tier)
2. Scale Out: ↑ # of VM instances (max 30, 100 for Isolated)
3. Autoscale: Auto ↑↓ based on rules/schedules

## 5. Implementation Guide

### Autoscale Config
1. Set min/max instances
2. Create rules:
   - Metric-based (e.g. CPU > 50%)
   - Time-based (e.g. every Sat @ 8AM)
3. Define actions (scale in/out)
4. Set notifications (email/webhook)

## 6. Advanced Topics
- Custom domains/certs (Standard+)
- Staging slots (Standard+)
- Web Jobs
- Diagnostics/backups

## 7. Monitoring/Maintenance
- Track: CPU%, memory, disk usage, HTTP queue length
- Regular OS patching (auto)
- Troubleshoot: Check logs, restart app/service

## 8. Best Practices
- Start low tier, scale up as needed
- Use autoscale to balance performance/cost
- Set adequate min/max instances
- Always use scale in/out rule pairs
- Configure notifications

## 9. Resources
- [App Service plans docs](https://docs.microsoft.com/azure/app-service/overview-hosting-plans)
- [Manage App Service plan](https://docs.microsoft.com/azure/app-service/app-service-plan-manage)
- [Scale up guide](https://docs.microsoft.com/azure/app-service/manage-scale-up)

Stats:
Original character count: 9,514
Compressed character count: 2,942
Compression ratio: 69.1%