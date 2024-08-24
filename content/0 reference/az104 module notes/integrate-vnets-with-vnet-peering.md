---
{}
---
# Azure Virtual Network Peering Technical Documentation

## 1. Introduction
Azure Virtual Network (VNet) Peering enables seamless connection between Azure virtual networks, allowing resources to communicate as if they're in the same network.

Key benefits:
- Private communication using Azure backbone (no public internet)
- Low latency, high bandwidth connections
- No downtime for resources during peering setup
- Simplified network topology compared to VPN/ExpressRoute

## 2. Types of VNet Peering
1. Regional VNet Peering: Connects VNets in the same Azure region
2. Global VNet Peering: Connects VNets across different Azure regions

## 3. Features and Considerations

### 3.1 Reciprocal Connections
- Peering requires configuration on both VNets
- Azure portal: Configures both sides automatically
- Azure PowerShell/CLI: Manual configuration for each side

### 3.2 Cross-Subscription Peering
- Supports peering VNets in different subscriptions
- Can use different Microsoft Entra tenants
- Requires `Network Contributor` role for administrators

### 3.3 Transitivity
- VNet peering is non-transitive
- Direct peering required for communication (A <-> B <-> C, A ≠ C)

### 3.4 Gateway Transit
- Enables on-premises connectivity through a single VNet gateway
- Configure "Allow gateway transit" on hub VNet
- Set "Use remote gateways" on spoke VNets

### 3.5 Address Spaces
- Peered VNets must have non-overlapping IP address spaces

## 4. Implementation Guide

### 4.1 Creating VNet Peering (Azure CLI)
```bash
# Peer VNet1 to VNet2
az network vnet peering create \
  --name VNet1-To-VNet2 \
  --resource-group myResourceGroup \
  --vnet-name VNet1 \
  --remote-vnet VNet2 \
  --allow-vnet-access

# Peer VNet2 to VNet1 (reciprocal connection)
az network vnet peering create \
  --name VNet2-To-VNet1 \
  --resource-group myResourceGroup \
  --vnet-name VNet2 \
  --remote-vnet VNet1 \
  --allow-vnet-access
```

### 4.2 Verifying Peering Status
```bash
az network vnet peering list \
  --resource-group myResourceGroup \
  --vnet-name VNet1 \
  --query "[].{Name:name, PeeringState:peeringState}" \
  --output table
```

### 4.3 Checking Effective Routes
```bash
az network nic show-effective-route-table \
  --resource-group myResourceGroup \
  --name myVMNic \
  --output table
```

## 5. Use Cases and Topologies

### 5.1 Hub and Spoke Topology
- Central hub VNet connected to multiple spoke VNets
- Ideal for centralized management and shared services

Example:
```
Hub VNet (10.0.0.0/16)
 ├─ Spoke VNet 1 (10.1.0.0/16)
 ├─ Spoke VNet 2 (10.2.0.0/16)
 └─ Spoke VNet 3 (10.3.0.0/16)
```

### 5.2 Full Mesh Topology
- Each VNet is peered with every other VNet
- Provides direct communication between all VNets

Example:
```
VNet A (10.0.0.0/16) ─┐
  │                    ├─ VNet C (10.2.0.0/16)
VNet B (10.1.0.0/16) ─┘
```

### 5.3 Hybrid Cloud Connectivity
- Peer on-premises network with Azure VNets using VPN Gateway or ExpressRoute
- Extend on-premises network to Azure

## 6. Best Practices
1. Plan IP address spaces carefully to avoid overlaps
2. Use Network Security Groups (NSGs) to control traffic between peered VNets
3. Implement least privilege access for peering management
4. Monitor peering state and bandwidth usage
5. Consider using Azure Private Link for added security

## 7. Limitations and Constraints
- Max 500 peerings per VNet
- Peering connections can't span clouds (e.g., Azure Commercial to Azure Government)
- Address space can't be added/removed from a VNet once peered
- Can't peer VNets with overlapping IP address ranges

## 8. Troubleshooting
1. Verify peering state is "Connected" on both sides
2. Check effective routes on VM network interfaces
3. Ensure NSGs aren't blocking traffic
4. Validate IP address ranges don't overlap

## 9. Monitoring and Management
- Use Azure Monitor for peering metrics and diagnostics
- Azure Network Watcher for topology view and connection troubleshooting
- Azure Policy for enforcing peering standards and compliance

## 10. Cost Considerations
- Inbound/Outbound data transfer charges apply for Global VNet Peering
- No additional charges for Regional VNet Peering (beyond standard data transfer)

## 11. Security Considerations
- Peering doesn't encrypt traffic by default
- Use Azure Private Link for added security when accessing PaaS services
- Implement network security groups (NSGs) to control traffic flow

## 12. Alternatives to VNet Peering
1. VPN Gateway
   - Pros: Works across subscriptions and tenants
   - Cons: Higher latency, more complex setup
2. ExpressRoute
   - Pros: Dedicated private connection, high bandwidth
   - Cons: Higher cost, longer setup time
3. Azure Virtual WAN
   - Pros: Managed networking service, simplifies complex topologies
   - Cons: May be overkill for simple peering scenarios

## 13. Integration with Other Azure Services
- Azure Firewall: Centralized network security management
- Azure Bastion: Secure RDP/SSH access to VMs
- Azure Private Link: Secure access to PaaS services
- Azure DNS: Custom DNS resolution across peered VNets

## 14. Testing VNet Peering Connectivity
1. Use Network Watcher's Connection Troubleshoot feature
2. Perform ping tests between VMs in peered VNets
3. Use tools like PsPing or iPerf for advanced network testing

Example test script (PowerShell):
```powershell
Test-NetConnection -ComputerName <remote_vm_ip> -Port 3389
```

## 15. Disaster Recovery Considerations
- Peer production and DR site VNets for seamless failover
- Use Global VNet Peering for cross-region DR scenarios
- Consider using Azure Site Recovery for VM replication

## 16. Additional Resources
- [Azure VNet Peering Documentation](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-peering-overview)
- [VNet Peering Pricing](https://azure.microsoft.com/en-us/pricing/details/virtual-network/)
- [Azure Networking Blog](https://azure.microsoft.com/en-us/blog/topics/networking/)
- [Azure Virtual Network GitHub Samples](https://github.com/Azure-Samples/virtual-network-management-dotnet)