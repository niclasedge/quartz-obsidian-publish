---
{}
---
# Comprehensive Guide: Custom Routing and Network Virtual Appliances in Azure

## 1. Introduction

Azure virtual networks provide a powerful platform for creating secure, isolated environments in the cloud. This guide focuses on advanced networking concepts:

- Custom routing to control traffic flow within and between virtual networks
- Network Virtual Appliances (NVAs) for enhanced security and traffic inspection

Use case: A retail organization recovering from a major security breach is implementing a new security strategy using Azure networking features.

Key goals:
1. Implement granular traffic control
2. Enhance security through traffic inspection
3. Create isolated network segments for sensitive data

## 2. Azure Routing in Depth

### 2.1 System Routes

Azure automatically creates system routes for each subnet. These include:

Route | Address Prefix | Next Hop Type
--- | --- | ---
Virtual network | Unique to the VNet | Virtual network
Internet | 0.0.0.0/0 | Internet
None | 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 100.64.0.0/10 | None

### 2.2 Custom Routes

Two main types:
1. User-Defined Routes (UDRs)
2. Border Gateway Protocol (BGP) routes

#### User-Defined Routes
- Created in route tables and associated with subnets
- Override system routes
- Useful for directing traffic through NVAs or VPN gateways

Next hop types for UDRs:
- Virtual appliance (specify IP)
- Virtual network gateway
- Virtual network
- Internet
- None (drop traffic)

#### BGP Routes
- Used with ExpressRoute or Site-to-Site VPN connections
- Dynamically exchange routes between on-premises and Azure networks

### 2.3 Route Selection and Priority

1. Longest prefix match: More specific routes take precedence
2. Priority order: 
   a. User-defined routes
   b. BGP routes
   c. System routes

## 3. Implementing Custom Routes

Detailed steps:

1. Create a route table:
```bash
az network route-table create \
    --name publictable \
    --resource-group "MyResourceGroup" \
    --disable-bgp-route-propagation false
```

2. Add a custom route:
```bash
az network route-table route create \
    --route-table-name publictable \
    --name productionsubnet \
    --address-prefix 10.0.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 10.0.2.4
```

3. Create virtual network and subnets:
```bash
az network vnet create \
    --name vnet \
    --resource-group "MyResourceGroup" \
    --address-prefixes 10.0.0.0/16 \
    --subnet-name publicsubnet \
    --subnet-prefixes 10.0.0.0/24

az network vnet subnet create \
    --name privatesubnet \
    --vnet-name vnet \
    --resource-group "MyResourceGroup" \
    --address-prefixes 10.0.1.0/24

az network vnet subnet create \
    --name dmzsubnet \
    --vnet-name vnet \
    --resource-group "MyResourceGroup" \
    --address-prefixes 10.0.2.0/24
```

4. Associate route table with subnet:
```bash
az network vnet subnet update \
    --name publicsubnet \
    --vnet-name vnet \
    --resource-group "MyResourceGroup" \
    --route-table publictable
```

## 4. Network Virtual Appliances (NVAs) in Depth

### 4.1 NVA Components
- Firewall: Stateful packet inspection
- IDS/IPS: Intrusion detection/prevention
- VPN endpoint: Secure remote access
- WAN optimization: Traffic compression, caching
- Load balancing: Distribute traffic across multiple backends

### 4.2 NVA Deployment Options
1. Azure Marketplace: Pre-configured appliances from vendors like Cisco, Palo Alto, F5
2. Custom VM: Manually configured Linux/Windows VM with routing enabled

### 4.3 Implementing an NVA

1. Deploy NVA VM:
```bash
az vm create \
    --resource-group "MyResourceGroup" \
    --name nva \
    --image Ubuntu2204 \
    --vnet-name vnet \
    --subnet dmzsubnet \
    --admin-username azureuser \
    --admin-password <password>
```

2. Enable IP forwarding on Azure NIC:
```bash
az network nic update --name $NICNAME \
    --resource-group "MyResourceGroup" \
    --ip-forwarding true
```

3. Enable IP forwarding within NVA (Linux example):
```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

4. Configure NVA software (firewall rules, packet inspection, etc.)

## 5. Routing Traffic Through NVA

1. Create test VMs:
```bash
az vm create \
    --resource-group "MyResourceGroup" \
    --name public \
    --vnet-name vnet \
    --subnet publicsubnet \
    --image Ubuntu2204

az vm create \
    --resource-group "MyResourceGroup" \
    --name private \
    --vnet-name vnet \
    --subnet privatesubnet \
    --image Ubuntu2204
```

2. Test routing:
```bash
# From public VM to private VM
ssh -t azureuser@$PUBLICIP 'traceroute private --type=icmp; exit'

# From private VM to public VM
ssh -t azureuser@$PRIVATEIP 'traceroute public --type=icmp; exit'
```

3. Analyze results to confirm traffic is routing through NVA

## 6. Advanced NVA Scenarios

### 6.1 High Availability NVA Deployment
- Use Azure Load Balancer for active-active configuration
- Implement health probes to detect NVA failures
- Use availability sets or zones for fault tolerance

### 6.2 NVA Scaling
- Implement Azure VM Scale Sets for automatic scaling
- Use Azure Application Gateway for layer 7 load balancing

### 6.3 NVA Monitoring and Management
- Use Azure Monitor for performance metrics and logs
- Implement Azure Automation for routine maintenance tasks
- Use Azure Security Center for security recommendations

## 7. Best Practices and Considerations

1. Security:
   - Regularly update and patch NVAs
   - Use Just-In-Time VM Access for management
   - Implement Network Security Groups as an additional layer of protection

2. Performance:
   - Size NVAs appropriately for expected traffic
   - Use accelerated networking for improved throughput

3. Compliance:
   - Ensure NVA logging meets regulatory requirements
   - Implement encryption for data in transit and at rest

4. Cost optimization:
   - Use Azure Reserved VM Instances for long-term NVA deployments
   - Implement auto-shutdown for non-production NVAs

## 8. Troubleshooting

1. Connectivity issues:
   - Verify route table associations
   - Check NVA firewall rules and IP forwarding settings
   - Use Network Watcher to diagnose routing problems

2. Performance problems:
   - Monitor NVA resource utilization (CPU, memory, network)
   - Use Network Performance Monitor for end-to-end latency analysis

3. Security concerns:
   - Review Azure Activity Logs for unauthorized changes
   - Use Azure Security Center to identify potential vulnerabilities

## 9. Additional Resources

- [Azure Networking Documentation](https://docs.microsoft.com/azure/networking/)
- [Network Virtual Appliance Best Practices](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha)
- [Azure Route Server for BGP routing](https://docs.microsoft.com/azure/route-server/overview)
- [Implement a Hub-Spoke network topology in Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)
