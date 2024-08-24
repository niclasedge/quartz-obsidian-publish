---
title: ' Azure AD Administrative Units Overview'
description: overview
authors: niclasedge
images: null
hide_table_of_contents: false
tags:
- Azure
- Active
- Directory
- Identity
---
# Azure AD Administrative Units: Overview and Benefits

```mermaid
stateDiagram-v2
    [*] --> AzureAD: Azure AD Tenant
    AzureAD --> Users: Contains
    AzureAD --> Groups: Contains
    AzureAD --> AdminUnit1: Contains
    AzureAD --> AdminUnit2: Contains
    
    state AzureAD {
        [*] --> GlobalAdmin: Global Administrator
        [*] --> PrivRoleAdmin: Privileged Role Administrator
        note right of GlobalAdmin
            Can create and manage
            Administrative Units
        end note
    }
    
    state AdminUnit1 {
        [*] --> AU1Users: Users
        [*] --> AU1Groups: Groups
        [*] --> AU1Roles: Scoped Roles
        note right of AU1Roles
            - User Administrator
            - Password Administrator
            - etc.
        end note
    }
    
    state AdminUnit2 {
        [*] --> AU2Users: Users
        [*] --> AU2Groups: Groups
        [*] --> AU2Roles: Scoped Roles
    }
    
    Users --> AU1Users: Can be part of
    Users --> AU2Users: Can be part of
    Groups --> AU1Groups: Can be part of
    Groups --> AU2Groups: Can be part of

    note right of AdminUnit1
        Users can belong to
        multiple Admin Units
    end note

    note right of AdminUnit2
        Groups in Admin Units
        don't grant control
        over group members
    end note
```

## Introduction
Azure AD Administrative Units (AUs) provide a way to delegate administrative permissions over subsets of users and groups within an Azure Active Directory instance. This feature allows for more granular control and management of resources in large organizations.

## Core Functionality

### Traditional Azure AD Structure
- Flat structure with no hierarchy
- Users, groups, service principals, and applications in a single tenant
- Roles applied at the tenant level

### Administrative Units
- Create logical groupings of users and groups
- Apply roles at the AU level instead of tenant-wide
- Users can belong to multiple AUs
- Cannot nest AUs

## Implementation Guide

### Prerequisites
- Azure AD instance
- Global Administrator or Privileged Role Administrator role
- Azure AD P1 or higher license for role assignment

### Creation and Management
- Create AUs via Azure Portal, PowerShell, or REST API
- Add users and groups to AUs
- Assign roles scoped to specific AUs

## Key Points
1. AUs allow for delegation of admin tasks to specific subsets of users/groups
2. Adding a group to an AU does not grant control over group members
3. Users with AU-scoped roles cannot manage accounts with global scope permissions
4. AUs are not available in Azure AD B2C

## Best Practices
- Use AUs for departmental or branch office management
- Carefully consider which roles to delegate at the AU level
- Regularly review AU memberships and assigned roles

## Monitoring and Maintenance
- Use My Staff portal (mystaff.microsoft.com) for AU-scoped management tasks
- Monitor role assignments and AU memberships for security

## Additional Resources
- Azure Portal: Azure Active Directory > Administrative Units
- PowerShell and Graph API for bulk operations and automation

