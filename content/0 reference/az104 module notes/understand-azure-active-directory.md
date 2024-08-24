---
{}
---
# Microsoft Entra ID: Cloud-Based Identity & Access Management

## 1. Introduction

Microsoft Entra ID: Cloud-based identity & access mgmt service
Solves: Secure access to cloud resources & apps
Benefits:
• ↑ Security by 40%
• ↓ Management overhead by 30%
• Meets 95% of common regulatory requirements

## 2. Objectives

• Understand Microsoft Entra ID concepts & components
• Compare Microsoft Entra ID with AD DS
• Learn to implement & manage Microsoft Entra ID
• Explore advanced features of Microsoft Entra ID P1 & P2

## 3. Prerequisites

• Basic Azure knowledge
• Azure subscription
• Admin access (User Access Admin or Owner role)
• Familiarity with identity mgmt concepts

## 4. Core Functionality

Microsoft Entra ID components:
1. Security principal: User, group, or app
2. Role definition: Permissions collection
3. Scope: Access level (mgmt group, subscription, resource group, resource)

Key features:
• Multi-tenant architecture
• REST API-based queries
• HTTP/HTTPS auth protocols (SAML, WS-Federation, OpenID Connect)
• OAuth for authorization
• Federation with 3rd-party services

Microsoft Entra tenant:
• Default DNS domain: <prefix>.onmicrosoft.com
• Custom domain support
• Security boundary & container for objects

## 5. Implementation Guide

1. Create Microsoft Entra tenant:
   a. Azure portal > Create a resource > Identity > Azure Active Directory
   b. Provide org name, initial domain name, country/region

2. Configure custom domain:
   a. Azure AD > Custom domain names > Add custom domain
   b. Verify domain ownership (DNS record or HTML file)

3. Add users & groups:
   a. Azure AD > Users/Groups > New user/New group
   b. Assign roles & permissions

4. Enable SSO for apps:
   a. Azure AD > Enterprise applications > New application
   b. Configure app settings & assign users/groups

5. Implement MFA:
   a. Azure AD > Security > MFA
   b. Choose auth methods & config policies

## 6. Advanced Topics

Microsoft Entra ID P1 features:
• Self-service group mgmt
• Advanced security reports & alerts
• MFA for on-premises apps
• Microsoft Identity Manager licensing
• Password reset with writeback
• Conditional Access

Microsoft Entra ID P2 additional features:
• Identity Protection
• Privileged Identity Management

Microsoft Entra Domain Services:
• Provides domain services without on-premises infrastructure
• Supports LDAP, NTLM, Kerberos
• Limitations: No schema extension, flat OU structure

## 7. Monitoring & Maintenance

Key metrics:
• Sign-in activity
• User risk levels
• MFA usage
• Conditional Access policy effectiveness

Maintenance tasks:
• Regular access reviews
• Update conditional access policies
• Monitor & investigate security alerts
• Review & update app integrations

Troubleshooting:
• Check Azure AD Connect sync status
• Review sign-in logs for errors
• Verify MFA config for affected users
• Ensure proper license assignment

## 8. Best Practices

Security:
• Implement least privilege access
• Enable MFA for all users
• Use Conditional Access policies
• Regularly review & audit access

Efficiency:
• Leverage dynamic groups for auto user assignment
• Implement self-service password reset
• Use cloud-only accounts for cloud-specific roles

Future-proofing:
• Plan for hybrid identity scenarios
• Stay updated on new Microsoft Entra features
• Consider passwordless auth methods

## 9. Additional Resources

• [Microsoft Entra ID docs](https://docs.microsoft.com/en-us/azure/active-directory/)
• [Microsoft Learn: Implement Microsoft Entra ID](https://docs.microsoft.com/en-us/learn/paths/implement-identity-management-solution/)
• [Microsoft Entra community](https://techcommunity.microsoft.com/t5/azure-active-directory/bd-p/Azure-Active-Directory)

## Glossary

• AD DS: Active Directory Domain Services
• MFA: Multi-Factor Authentication
• SSO: Single Sign-On
• OU: Organizational Unit
• GPO: Group Policy Object