---
{}
---
# Azure Network Security Groups (NSGs): Comprehensive Guide

## 1. Introduction
- NSGs limit network traffic to resources in virtual networks
- Contain security rules to allow/deny inbound/outbound traffic

## 2. Key Concepts
- Can be associated with subnets or network interfaces
- Multiple associations possible
- Created and managed in Azure portal

## 3. Security Rules
- Default rules: Inbound (deny all except VNet and Azure Load Balancer), Outbound (allow internet and VNet)
- Custom rules include:
  - Name, Priority, Port, Protocol, Source, Destination, Action

## 4. Rule Processing
- Inbound: Subnet NSG rules, then NIC NSG rules
- Outbound: NIC NSG rules, then Subnet NSG rules
- Intra-subnet traffic considered

## 5. Effective Rules
- Combination of default and custom rules
- Viewed in Azure portal under "Effective security rules"

## 6. Best Practices
- Leave gaps in priority numbering (e.g., 100, 200, 300)
- Define allow rules for both subnet and NIC
- Consider intra-subnet traffic
- Use lowest priority for critical rules

## 7. Application Security Groups (ASGs)
- Logically group VMs by workload
- Simplify NSG rule management
- Reduce IP address maintenance
- Enable workload-centric organization

## 8. Implementation Steps
1. Create NSG
2. Define security rules
3. Associate with subnets or NICs
4. Create ASGs (if needed)
5. Assign VM interfaces to ASGs
6. Update NSG rules to reference ASGs

## 9. Considerations
- Default "allow all" for unassociated resources
- Rule priority is crucial
- Balance between security and functionality
- Regular review and updates of rules

## 10. Additional Resources
- [Network security groups overview](https://docs.microsoft.com/en-us/azure/virtual-network/security-overview)
- [NSG tutorial](https://docs.microsoft.com/en-us/azure/virtual-network/tutorial-filter-network-traffic)
- [Manage NSGs](https://docs.microsoft.com/en-us/azure/virtual-network/manage-network-security-group)
- [ASG documentation](https://docs.microsoft.com/en-us/azure/virtual-network/application-security-groups)