---
{}
---
# Azure Resource Manager (ARM) Tech Doc

## 1. Intro
- ARM: Azure's deployment & mgmt service for infrastructure
- Solves: Unorganized resource creation, accidental deletions, ownership tracking
- Key benefits: 
  * Unified resource mgmt & organization
  * Consistent deployment across environments
  * Improved security & access control
  * Cost management & optimization

## 2. Objectives
1. Understand ARM features & use cases
2. Organize resources effectively with resource groups
3. Apply & manage resource locks for protection
4. Move resources between groups/subscriptions/regions
5. Remove resources/groups safely
6. Track & manage resource limits

## 3. Core Functionality
- Consistent mgmt layer across tools (PowerShell, CLI, portal, REST API, SDKs)
- Group-based resource deployment/mgmt for easier administration
- Declarative template-based infrastructure for reproducibility
- Dependency management to ensure proper resource deployment order
- Access control via RBAC for granular permissions
- Resource tagging for logical organization & cost tracking
- Auditing capabilities for compliance & troubleshooting

## 4. Key Components
- Resource: Manageable Azure item (VM, storage, web app, etc.)
  * Identified by resource ID: /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider-namespace}/{resource-type}/{resource-name}
- Resource group: Container for related resources
  * Logical grouping, not a physical container
  * Resources can interact across groups
- Resource provider: Service supplying deployable resources
  * Examples: Microsoft.Compute, Microsoft.Storage, Microsoft.Web
  * Each provider offers specific resource types
- Template: JSON file defining resources to deploy
  * Supports parameters, variables, functions for flexibility
  * Can be version-controlled & reused
- Declarative syntax: State-based resource definition
  * Describes desired end-state, not step-by-step instructions

## 5. Resource Groups
- Logical collection of resources with shared lifecycle
- Rules:
  * Resources can exist in only one group at a time
  * Groups can't be renamed after creation
  * Can contain multiple resource types from different regions
- Creation considerations:
  * Shared lifecycle: Deploy, update, delete together
  * Access control scoping: Apply permissions at group level
  * Regional compliance: Metadata storage location
- Best practices:
  * Use consistent naming convention
  * Limit access using RBAC
  * Use tags for additional organization & automation

## 6. Resource Locks
- Prevent accidental resource deletion/modification
- Types: 
  * Read-Only: Prevent modifications
  * Delete: Prevent deletion, allow modifications
- Inherited by child resources automatically
- Applied at subscription/group/resource level
- Manageable by Owner/User Access Administrator roles
- Considerations:
  * Plan lock strategy carefully to avoid blocking necessary changes
  * Document lock usage for team awareness
  * Regularly review & update locks as needed

## 7. Resource Movement
- Move resources between groups/subscriptions
- Limitations exist (check move support docs for each resource type)
- Process:
  1. Validate move eligibility
  2. Source/target groups locked during move
  3. Update resource references (e.g., VNet peerings)
  4. Reconfigure monitoring/alerts post-move
- Best practices:
  * Test in non-production environment first
  * Schedule moves during low-traffic periods
  * Update scripts & automation post-move

## 8. Resource/Group Removal
- Caution: Deleting group deletes all contained resources
- Process:
  1. Review group contents & dependencies
  2. Backup important data
  3. Remove or update dependencies
  4. Delete group or individual resources
- PowerShell: Remove-AzResourceGroup -Name "GroupName" -Force
- Azure CLI: az group delete --name "GroupName" --yes
- Considerations:
  * Some resources (e.g., managed disks) may require separate deletion
  * Soft-delete features available for certain resource types

## 9. Resource Limits
- View usage against limits in Azure portal
- Limits categories:
  * Subscription-level (e.g., max VMs per subscription)
  * Resource group-level (e.g., max resources per group)
  * Resource-specific (e.g., max storage account capacity)
- Request limit increases if needed:
  * Some limits adjustable, others fixed
  * Justify increase requests with business needs
- Best practices:
  * Regularly monitor usage against limits
  * Plan capacity proactively
  * Consider using multiple subscriptions for large-scale deployments

## Best Practices
- Use declarative templates for consistent, repeatable deployments
- Group resources by lifecycle for easier management
- Apply least-privilege access control using RBAC
- Use tags for non-lifecycle organization & reporting
- Regularly review & optimize resource usage for cost efficiency
- Implement naming conventions for clear resource identification
- Utilize policies to enforce organizational standards
- Implement proper backup & disaster recovery strategies

## Additional Resources
- [ARM documentation](https://docs.microsoft.com/en-us/azure/azure-resource-manager/)
- [ARM template reference](https://docs.microsoft.com/en-us/azure/templates/)
- [Move operation support](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/move-support-resources)
- [Azure limits reference](https://docs.microsoft.com/en-us/azure/azure-subscription-service-limits)
- [Azure Policy documentation](https://docs.microsoft.com/en-us/azure/governance/policy/)
- [Azure Cost Management documentation](https://docs.microsoft.com/en-us/azure/cost-management-billing/)