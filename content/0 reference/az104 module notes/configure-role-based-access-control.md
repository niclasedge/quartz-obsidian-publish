---
{}
---
# Azure Role-Based Access Control (RBAC): Comprehensive Guide

## 1. Introduction
- RBAC: Authorization system for managing access to Azure resources
- Enables fine-grained access management

## 2. Core Concepts
- Security principal: Object requesting access (user, group, service principal, managed identity)
- Role definition: Set of permissions defining allowed operations
- Scope: Boundary for access level (management group, subscription, resource group, resource)
- Role assignment: Attaches role definition to security principal at a scope

## 3. Role Definitions
- Components: Actions, NotActions, DataActions, AssignableScopes
- Built-in roles: Owner, Contributor, Reader, User Access Administrator
- Custom roles: Create for specific organizational needs

## 4. Role Assignments
- Purpose: Control access by scoping role definition
- Inheritance: Resources inherit role assignments from parent resources
- Effective permissions: Combination of assigned roles and resource roles

## 5. Azure RBAC vs Microsoft Entra Roles
| Azure RBAC | Microsoft Entra Roles |
|------------|------------------------|
| Manages Azure resources | Manages Microsoft Entra resources |
| Multi-level scope | Tenant-level scope |
| Defined via Azure tools | Defined via admin portals, PowerShell |

## 6. Implementation Best Practices
- Use built-in roles when possible
- Create custom roles for specific needs
- Limit access scope to minimum required
- Control data changes carefully
- Consider deny assignments for explicit blocking

## 7. Fundamental Azure RBAC Roles
- Owner: Full access, can delegate
- Contributor: Can create/manage resources, can't delegate
- Reader: Can view resources
- User Access Administrator: Can manage user access

## 8. Management Tips
- Regularly review and audit role assignments
- Use management groups for organizing subscriptions
- Implement least privilege principle
- Use PIM for just-in-time access

## 9. Additional Resources
- [Azure RBAC documentation](https://docs.microsoft.com/en-us/azure/role-based-access-control/)
- [Built-in roles list](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles)
- [Custom roles tutorial](https://docs.microsoft.com/en-us/azure/role-based-access-control/tutorial-custom-role-powershell)