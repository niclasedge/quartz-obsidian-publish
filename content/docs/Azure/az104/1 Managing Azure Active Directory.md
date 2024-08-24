---
title: az104 - 1 Managing Azure Entra ID
description: First part of the az104 course
authors: niclasedge
images: ./docs/azure/az104/Pasted image 20230508124233.png
hide_table_of_contents: false
tags:
- az104
- Azure
- Active Directory
- Identity
draft: true
---


## Entra ID Overview
- Cloud-based identity and directory management
- Enables access to Azure services and other SaaS solutions
- Offers:
  - Self-service options including:
    - Password reset
    - Authentication
    - Device management
    - Hybrid identities
    - Single sign-on
![[_special notes/docusaurus/docs/Azure/az104/Pasted image 20230508125013.png]]

```
				 [Devices]
                     ^
                     |
 [Business]          |          [Public cloud]
 [Partners]          |               [Azure]
     ^               |          +--------------+
     |               |          |              |
     |               |          |   [SaaS apps]|
     |               |          | +----------+ |
     |               |          | |salesforce| |
     |               |          | |Office 365| |
     |               |          | |DocuSign  | |
     |               |          | |SAP       | |
     |               |          | |Google    | |
     |               |          | |box       | |
     |               |          | +----------+ |
     |               |          |              |
     |               |          +--------------+
     |               |                 ^
     |     +---------------------+     |
     |     |                     |     |
     +-----|    Azure Active     |-----+
           |     Directory       |
     +-----|                     |-----+
     |     +---------------------+     |
     |                                 |
     |                                 |
     v                                 v
+------------+                  +-------------+
|On-premises |                  |   Active    |
|applications|                  |  Directory  |
+------------+                  +-------------+
```
### Entra ID Concepts
- **Identity**: Everything that can be authenticated
  - User, group, managed identity, or service principal
- **Account**: When we associate data attributes to an identity
- **Entra ID Account**: Account created in Entra ID or other Microsoft cloud service
- **Entra ID Tenant or Directory**: Dedicated instance of Entra ID, created with a service subscription. Tenant and directory mean the same.

### Entra ID vs ADDS (Azure Directory Domain Services)
- Operate completely differently

Entra ID:
- Queried using HTTP/HTTPS
- Protocols used for authentication include SAML, WS-Federation, OpenID Connect, OAuth for authorization
- Federation can be set up with third-party providers like Facebook
- Entra ID is a managed service offering

ADDS:
- Queried using LDAP
- Kerberos is used for AD DS authentication
- Federation only to other domains, third-party services are not supported
- ADDS will be running on VM or physical server
![[_special notes/docusaurus/docs/Azure/az104/Pasted image 20230523162431.png]]

### Entra ID Editions
![[_special notes/docusaurus/docs/Azure/az104/Pasted image 20230523162830.png]]

### User Accounts
- For authentication and authorization
- Have optional properties
- Can be accessed from Entra ID/users/All Users
- Can perform bulk operations like bulk create, bulk invite, and bulk delete
- **Cloud Identity**: Can only exist in Entra ID
- **Guest Accounts**: Exist outside of Azure and are invited for collaboration
- **Directory Synchronized Users**: These users are synchronized from your on-premises Windows AD
  - We cannot create directory synchronized users; they need to be synchronized

### Bulk Operations
- Bulk Create: Create multiple users based on a CSV file
- Bulk Invite
- Bulk Delete
- Download Users
![[_special notes/docusaurus/docs/Azure/az104/Pasted image 20230531082449.png]]

### Group Accounts
**There are 2 types of Groups in Entra ID**:
- Security Groups: For permissions
- Microsoft 365 Groups: In addition to access management
  - Makes use of M365 Apps, shared mailbox, calendar
  - Needs a mail address for use in shared mailbox, SharePoint, etc.
  - Extend membership to people outside the organization

**Assignment Types**:
- Defined when creating the group, only can have one type
  - Assigned
  - Dynamic Users: Adds users based on defined attributes automatically
    - ![[_special notes/docusaurus/docs/Azure/az104/Pasted image 20230531085112.png]]
    - Validate if user is in dynamic group:
      ![[docusaurus/docs/Azure/az104/Pasted image 20230531085348.png]]
  - Dynamic Device (only for Security group type)

### Entra ID Join
- Join a device to Entra ID to make use of multiple Azure features
![[docusaurus/docs/Azure/az104/Pasted image 20230531085748.png]]

### SSPR (Self-Service Password Reset)
- Setup: www.aka.ms/ssprsetup
- Reset password: www.aka.ms/sspr
- Enables users to reset their own password
- Setup multiple methods for resetting the password
- **Requires Premium P2 license**, as this is a premium feature
- Target all users or a group of users
![[docusaurus/docs/Azure/az104/Pasted image 20230531090148.png]]

### Multi-Tenant Environments
- No parent-child relationship between tenants
- Resource independence
- Administration independence
- Synchronization independence
