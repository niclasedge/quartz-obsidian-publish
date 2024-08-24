---
{}
---
# Azure Network Watcher: Comprehensive Guide

## 1. Introduction
- Tool for monitoring, diagnosing, and managing Azure virtual networks
- Regional service for network-level diagnostics

## 2. Key Features
1. IP Flow Verify:
   - Diagnoses connectivity issues
   - Checks if security rules block traffic
   - Configuration: VM, ports, IP, protocol, direction
   - Returns allow/deny status and controlling rule

2. Next Hop:
   - Checks if traffic reaches intended destination
   - Configuration: VM, source/destination IP
   - Returns: Next hop type, IP, route table
   - Helps identify unresponsive VMs or broken routes

3. VPN Troubleshoot:
   - Diagnoses virtual network gateway/connection health
   - Provides connection stats, CPU/memory info, errors
   - Stores detailed logs in Azure storage

4. NSG Diagnostics:
   - Uses flow logs for NSG traffic mapping
   - Supports compliance and auditing requirements

5. Connection Troubleshoot:
   - Checks direct TCP/ICMP connections
   - Supports VMs, app gateways, Azure Bastion hosts

6. Topology Tool:
   - Visualizes virtual network resources and connections
   - Shows subnets, VMs, NICs, IPs, NSGs, route tables

## 3. Use Cases
- Remote network monitoring
- Alert-triggered packet capture
- NSG flow log analysis
- VPN Gateway and connection troubleshooting

## 4. Best Practices
- Use for systematic troubleshooting
- Combine features for comprehensive diagnostics
- Regularly review network topology
- Leverage NSG flow logs for security audits

## 5. Implementation Steps
1. Enable Network Watcher in your region
2. Configure diagnostic settings for resources
3. Use appropriate tool for specific issue:
   - Connectivity: IP Flow Verify
   - Routing: Next Hop
   - VPN: VPN Troubleshoot
   - Security: NSG Diagnostics
4. Analyze results and take corrective actions

## 6. Considerations
- Requires Owner, Contributor, or Network Contributor role
- Some features may incur additional costs
- Use in conjunction with other Azure monitoring tools

## 7. Additional Resources
- [Network Watcher documentation](https://docs.microsoft.com/en-us/azure/network-watcher/)
- [Diagnose VM routing problem tutorial](https://docs.microsoft.com/en-us/azure/network-watcher/diagnose-vm-network-routing-problem)
- [Diagnose VNet communication problem tutorial](https://docs.microsoft.com/en-us/azure/network-watcher/diagnose-communication-problem-between-networks)