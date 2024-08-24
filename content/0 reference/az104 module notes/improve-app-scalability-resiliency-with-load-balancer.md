---
{}
---
# Azure Load Balancer Technical Documentation

## 1. Introduction
Azure Load Balancer is a Layer 4 (TCP, UDP) load balancing service that distributes incoming traffic across multiple instances to ensure high availability and reliability. It enables you to:
- ↑ app scalability by 200%
- Improve resiliency with 99.99% uptime SLA
- Distribute traffic evenly across VMs or services

Key benefits:
- Supports inbound & outbound scenarios
- Low latency & high throughput
- Scales to millions of flows for TCP & UDP apps

## 2. Objectives
1. Understand Load Balancer features & capabilities
2. Learn to deploy & configure Load Balancer instances
3. Implement best practices for scalability & resilience
4. Optimize performance & cost efficiency

## 3. Prerequisites
- Azure subscription
- Basic networking knowledge
- Familiarity with Azure VMs
- Understanding of high availability concepts

## 4. Core Functionality

### 4.1 Distribution Algorithms
- Default: Five-tuple hash (source IP, source port, destination IP, destination port, protocol type)
- Alternative: Source IP affinity (session affinity)

### 4.2 Availability Options
1. Availability Sets
   - Logical grouping within datacenter
   - Protection from hardware failures
   - 99.95% SLA
2. Availability Zones
   - Physical separation across datacenters
   - Protection from datacenter failures
   - 99.99% SLA

### 4.3 Load Balancer Types
1. Public (External) Load Balancer
   - Distributes internet traffic to VMs
   - Uses public IP address
2. Internal Load Balancer
   - Distributes traffic within virtual network
   - Uses private IP address

### 4.4 SKUs
1. Basic
   - Free, limited features
   - Single availability set
2. Standard
   - Enhanced features
   - Availability zones support
   - Guaranteed SLA

## 5. Implementation Guide

### 5.1 Deploying a Public Load Balancer
1. Create Load Balancer resource
   ```
   az network lb create --resource-group myRG --name myLB --sku Standard --public-ip-address myPublicIP
   ```
2. Create backend pool
   ```
   az network lb address-pool create --resource-group myRG --lb-name myLB --name myBackendPool
   ```
3. Create health probe
   ```
   az network lb probe create --resource-group myRG --lb-name myLB --name myHealthProbe --protocol tcp --port 80
   ```
4. Create load balancing rule
   ```
   az network lb rule create --resource-group myRG --lb-name myLB --name myHTTPRule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name LoadBalancerFrontEnd --backend-pool-name myBackendPool --probe-name myHealthProbe
   ```

### 5.2 Configuring an Internal Load Balancer
1. Create internal Load Balancer
   ```
   az network lb create --resource-group myRG --name myInternalLB --sku Standard --vnet-name myVNet --subnet mySubnet --frontend-ip-name myFrontEnd --backend-pool-name myBackendPool
   ```
2. Add backend pool, health probe, and rule (similar to public LB)

### 5.3 Adding VMs to backend pool
```
az network nic ip-config address-pool add --address-pool myBackendPool --ip-config-name ipconfig1 --nic-name myNIC1 --resource-group myRG --lb-name myLB
```

## 6. Advanced Topics

### 6.1 Session Persistence
- Enable source IP affinity for stateful apps
- Configure in Azure Portal or use PowerShell:
  ```
  $lb = Get-AzLoadBalancer -Name myLB -ResourceGroupName myRG
  $lb.LoadBalancingRules[0].LoadDistribution = "SourceIP"
  Set-AzLoadBalancer -LoadBalancer $lb
  ```

### 6.2 SSL Offloading
- Use Application Gateway for SSL termination
- Reduces CPU load on backend servers

### 6.3 Multi-region Load Balancing
- Use Traffic Manager or Front Door for global load balancing
- Improves app responsiveness & resilience

## 7. Monitoring & Maintenance

### 7.1 Key Metrics
- Data path availability
- Health probe status
- Concurrent connections
- Throughput (bytes/packets per second)

### 7.2 Azure Monitor Integration
- Enable diagnostic logging
- Create custom dashboards
- Set up alerts for critical thresholds

### 7.3 Regular Maintenance Tasks
- Review & update health probe settings
- Optimize backend pool resources
- Analyze traffic patterns for scaling decisions

## 8. Best Practices
1. Use Standard SKU for production workloads
2. Implement proper health probes (↑ accuracy by 30%)
3. Configure appropriate idle timeout (default: 4 minutes)
4. Use availability zones for maximum resilience
5. Implement proper logging & monitoring
6. Regularly review & optimize LB rules
7. Use NSGs to control traffic flow

## 9. Troubleshooting
1. Verify backend pool VM health
2. Check NSG rules for conflicts
3. Validate health probe settings
4. Review load balancing rules
5. Check for quota limitations

## 10. Cost Optimization
- Use Basic SKU for dev/test environments
- Implement auto-scaling for backend pools
- Monitor & adjust reserved instances
- Use Azure Hybrid Benefit for Windows Server VMs

## 11. Security Considerations
- Enable DDoS protection
- Use NSGs to restrict traffic
- Implement Azure Firewall for advanced threat protection
- Regularly update & patch backend VMs

## 12. Limitations & Constraints
- Max 1000 backend pool resources per LB
- Max 150 outbound rules per LB
- IPv6 support limitations in some regions

## 13. Integration with Other Azure Services
- Azure Kubernetes Service (AKS)
- Virtual Machine Scale Sets
- Azure App Service
- Azure Functions

## 14. Additional Resources
- [Azure Load Balancer documentation](https://docs.microsoft.com/azure/load-balancer/)
- [Load Balancer pricing](https://azure.microsoft.com/pricing/details/load-balancer/)
- [Load Balancer limits](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits#load-balancer)
- [Azure Friday: Load Balancer Deep Dive](https://azure.microsoft.com/resources/videos/azure-load-balancer-deep-dive/)