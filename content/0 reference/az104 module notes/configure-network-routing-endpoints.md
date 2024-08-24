---
{}
---
# Azure Network Routing and Endpoints: Comprehensive Guide

## 1. System Routes
- Control traffic between VMs, on-premises networks, and internet
- Recorded in route tables associated with subnets
- Handle traffic based on destination (IP, gateway, appliance, internet)

## 2. User-Defined Routes (UDRs)
- Custom configuration for network traffic
- Next hop targets: 
  - Virtual network gateway
  - Virtual network
  - Internet
  - Network virtual appliance (NVA)
- One route table per subnet, multiple subnets per table

## 3. Service Endpoints
- Extend virtual network identity to Azure services
- Use virtual network private addresses as source IPs
- Improve security by removing public internet access
- Optimal routing for Azure service traffic
- Easy configuration and maintenance

### Supported Services
- Azure Storage
- Azure SQL Database
- Azure Cosmos DB
- Azure Key Vault
- Azure Service Bus and Event Hubs

## 4. Azure Private Link
- Private connectivity to Azure PaaS, customer-owned, or partner services
- Keeps traffic on Microsoft global network
- No regional restrictions
- No need for gateways, NAT, ExpressRoute, VPN, or public IPs

### Benefits
- Private connectivity to Azure services
- Integration with on-premises and peered networks
- Protection against data exfiltration
- Direct service delivery to customer virtual networks

## 5. Best Practices
- Use UDRs for custom routing through NVAs
- Implement service endpoints for improved security and optimal routing
- Leverage Private Link for sensitive services and data exfiltration protection
- Regularly review and update routing configurations

## 6. Implementation Steps
1. Create virtual network and subnets
2. Deploy VMs into different subnets
3. Configure private and public IP addresses
4. Set up network security groups
5. Configure Azure DNS for internal name resolution
6. Configure Azure DNS for external name resolution

## 7. Additional Resources
- [Virtual network traffic routing docs](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-udr-overview)
- [Route table tutorial](https://docs.microsoft.com/en-us/azure/virtual-network/tutorial-create-route-table-portal)
- [BGP for Azure VPN Gateway](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-bgp-resource-manager-ps)
- [Azure Private Link intro](https://docs.microsoft.com/en-us/training/modules/introduction-azure-private-link/)