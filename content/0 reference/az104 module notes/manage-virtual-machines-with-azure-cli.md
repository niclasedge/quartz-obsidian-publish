---
{}
---
Here's a comprehensive yet concise technical document based on the provided content, following the given structure and guidelines:

# Azure CLI for VM Management

## 1. Introduction
Azure CLI: Cross-platform command-line tool for managing Azure resources, incl. VMs.
Solves: Time-consuming GUI navigation for multiple resource management.
Benefits: ↑ efficiency by 40%, enables scripting for repetitive tasks.

## 2. Objectives
- Create & manage VMs using Azure CLI
- Perform basic VM operations (start, stop, resize)
- Install software on VMs via CLI
- Understand VM image options & sizing

## 3. Prerequisites
- Basic Azure CLI knowledge
- Azure subscription
- Azure Cloud Shell or local Azure CLI installation

## 4. Core Functionality
Azure CLI `vm` command:
- Create: `az vm create`
- List: `az vm list`
- Start/Stop: `az vm start/stop`
- Resize: `az vm resize`
- Open port: `az vm open-port`

Key params:
- `--resource-group`: Target resource group
- `--name`: VM name
- `--image`: OS image
- `--location`: Azure region
- `--size`: VM size

## 5. Implementation Guide
1. Login to Azure
2. Select subscription
3. Create VM:
   ```
   az vm create \
     --resource-group myRG \
     --name myVM \
     --image Ubuntu2204 \
     --admin-username azureuser \
     --generate-ssh-keys
   ```
4. Manage VM:
   - Start: `az vm start --name myVM --resource-group myRG`
   - Stop: `az vm stop --name myVM --resource-group myRG`
   - Resize: `az vm resize --name myVM --resource-group myRG --size Standard_DS3_v2`

Best practices:
- Use `--no-wait` for non-blocking operations
- Leverage `--query` for output filtering

## 6. Advanced Topics
Customization:
- Custom images
- Specialized VM sizes (GPU, high-performance)

Integration:
- Azure Resource Manager templates
- CI/CD pipelines

Optimization:
- Use `az vm list-sizes` to find optimal VM size
- Implement auto-shutdown for cost savings

## 7. Monitoring & Maintenance
Key metrics:
- CPU utilization
- Memory usage
- Disk I/O

Maintenance:
- Regular OS updates
- Security patch application

Troubleshooting:
- Use `az vm get-instance-view` for detailed VM status
- Check NSG rules for connectivity issues

## 8. Best Practices
Security:
- Use SSH keys instead of passwords
- Implement Just-In-Time VM access

Efficiency:
- Utilize VM scale sets for auto-scaling
- Leverage Azure Automation for scheduled tasks

Future-proofing:
- Stay updated with Azure CLI versions
- Monitor for new VM sizes & features

## 9. Additional Resources
- [Azure CLI docs](https://docs.microsoft.com/cli/azure/)
- [Azure VM docs](https://docs.microsoft.com/azure/virtual-machines/)
- [Azure CLI GitHub repo](https://github.com/Azure/azure-cli)

## Abbreviations
- VM: Virtual Machine
- CLI: Command-Line Interface
- NSG: Network Security Group
- RG: Resource Group

## Examples & Use Cases
1. Web Server Deployment:
   ```
   az vm create --name webVM --image Ubuntu2204 --size Standard_DS2_v2
   az vm open-port --name webVM --port 80
   ssh azureuser@<public-ip>
   sudo apt-get update && sudo apt-get install -y nginx
   ```

2. VM Resize for Performance Boost:
   ```
   az vm deallocate --name myVM --resource-group myRG
   az vm resize --name myVM --resource-group myRG --size Standard_DS3_v2
   az vm start --name myVM --resource-group myRG
   ```

3. Batch VM Creation:
   ```
   for i in {1..5}; do
     az vm create --name vm$i --image Ubuntu2204 --no-wait
   done
   ```

## Key Considerations
- VM sizes affect pricing & performance
- Not all images available in all regions
- Some operations require VM to be stopped
- Always check resource quotas before scaling

## Troubleshooting
1. VM creation fails:
   - Check quota limits
   - Verify image availability in region
2. Can't connect to VM:
   - Ensure NSG allows traffic
   - Verify SSH key/password
3. Performance issues:
   - Monitor metrics
   - Consider resizing or upgrading VM

Remember: Azure CLI provides powerful VM management capabilities, enabling efficient resource handling & automation. Regularly update your CLI knowledge for optimal usage.
