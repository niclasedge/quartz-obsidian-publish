---
title: Protect Agains Credential and Token Theft
description: description
authors: niclasedge
images: null
tags:
- azure
toc_max_heading_level: 5
created: 24.06.2024
---
# Credential and Token Theft Protection

## 1. Introduction
- Overview: Comprehensive approach to protecting credentials and tokens in modern authentication systems
- Problem: Increasing sophistication of attacks targeting credentials and tokens
- Key benefits: ↑ security, ↓ risk of unauthorized access by 70-80%

## 2. Objectives
1. Implement strong authentication methods
2. Secure token handling and storage
3. Enable device-level protections
4. Implement detection and response mechanisms

## 3. Prerequisites
- Knowledge: Basic understanding of authentication flows
- Resources: Entra ID (Azure AD) tenant, managed devices

## 4. Core Functionality

### Authentication Flow
1. User authenticates to Entra ID
2. Entra ID issues tokens:
   - Primary Refresh Token (PRT): 14-day validity
   - Session Key: Hardware-bound to device
   - Refresh Tokens: 90-day validity (24h for SPA)
   - Access Tokens: 1h validity (extendable with revocation tech)

### Token Binding
- PRT linked to Session Key
- Session Key stored in TPM/secure hardware
- Enables Proof of Possession (PoP) for token requests

## 5. Implementation Guide

### Strong Authentication
1. Enable phishing-resistant MFA (e.g., FIDO2, Windows Hello)
2. Implement Conditional Access policies
3. Educate users on phishing attacks

### Device Management
1. Register/join devices to Entra ID
2. Deploy MDM solution (e.g., Intune)
3. Install Microsoft Defender for Endpoint

### Network Protection
1. Implement Entra Internet Access
2. Enable adaptive network checks in Conditional Access

### Token Protection
1. Use Microsoft Authentication Library (MSAL) in applications
2. Leverage platform-specific token brokers (e.g., WAM on Windows)
3. Enable "Require token protection" in Conditional Access (preview)

## 6. Advanced Topics

### Continuous Access Evaluation (CAE)
- Enables real-time token revocation
- Integrates with Conditional Access policies

### Identity Protection
- Detects anomalous token usage
- Triggers risk-based Conditional Access policies

## 7. Monitoring and Maintenance

### Key Metrics
- User risk levels
- Device compliance status
- Token binding success rate

### Troubleshooting
1. Check device registration status
2. Verify TPM functionality
3. Review Conditional Access policy conflicts

## 8. Best Practices
1. Always use managed devices for accessing sensitive resources
2. Implement least-privilege access model
3. Regularly update and patch all systems
4. Monitor and respond to Identity Protection alerts

## 9. Additional Resources
- [Entra ID documentation](https://docs.microsoft.com/en-us/azure/active-directory/)
- [MSAL documentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/msal-overview)
- [Conditional Access documentation](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/)