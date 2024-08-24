---
title: Entra PowerShell Module Overview
date: 07/15/2024 13:51:15
authors: niclasedge
tags:
- Azure
- Update
---

# Executive Summary of Entra PowerShell Module Overview

Video by John Savill's Technical Training

<iframe width="100%" height="415" src="https://www.youtube.com/embed/YOgpAkshmYI" frameborder="0" allowfullscreen></iframe>

[Watch on YouTube](https://www.youtube.com/watch?v=YOgpAkshmYI)


# Introduction to Microsoft Graph Enta Module
=====================================================

## Overview
-----------

The Microsoft Graph Enta module is a new PowerShell module designed to make interacting with the Microsoft Graph API more friendly and scenario-based. It is built on top of the existing Microsoft Graph module, which was automatically generated using AutoRest.

## History of Microsoft Graph API
--------------------------------

In the past, interacting with Azure Active Directory (Azure AD) required multiple modules, which spoke to the Azure AD endpoint. However, with the introduction of Microsoft Graph, these modules were deprecated and retired. Microsoft Graph is a single endpoint that enables interaction with multiple Microsoft services, including Azure AD, Microsoft 365, and Dynamics 365.

## Microsoft Graph API
----------------------

The Microsoft Graph API is a RESTful API that provides access to various Microsoft services. It is designed for developers and provides a single endpoint for interacting with multiple services. The API is based on the OpenAPI standard and is automatically generated using AutoRest.

## Microsoft Graph Enta Module
-----------------------------

The Microsoft Graph Enta module is a new PowerShell module that provides a more friendly and scenario-based interface for interacting with the Microsoft Graph API. It is designed to make it easier for users to perform common tasks and is built on top of the existing Microsoft Graph module.

## Key Features
--------------

*   **Scenario-based interface**: The Enta module provides a more friendly and scenario-based interface for interacting with the Microsoft Graph API.
*   **98% compatibility with Azure AD**: The Enta module provides 98% compatibility with the Azure AD module, making it easier to migrate existing scripts.
*   **Pipeline support**: The Enta module supports piping, making it easier to chain commands together.
*   **Debugging**: The Enta module provides a debugging feature that allows users to see the actual REST calls being made.

## Installing the Microsoft Graph Enta Module
--------------------------------------------

To install the Microsoft Graph Enta module, run the following command:

```powershell
Install-Module -Name Microsoft.Graph.Enta
```

## Enabling Azure AD Alias
---------------------------

To enable the Azure AD alias, run the following command:

```powershell
Enable-GraphEntaAzureAdAlias
```

This will enable the alias and provide 98% compatibility with the Azure AD module.

## Using the Microsoft Graph Enta Module
-----------------------------------------

To use the Microsoft Graph Enta module, connect to your tenant using the following command:

```powershell
Connect-GraphEnta
```

This will prompt you to authenticate and authorize the module.

## Conclusion
----------

The Microsoft Graph Enta module provides a more friendly and scenario-based interface for interacting with the Microsoft Graph API. It is designed to make it easier for users to perform common tasks and provides 98% compatibility with the Azure AD module. The module supports piping and provides a debugging feature that allows users to see the actual REST calls being made.

# Glossary
------------

*   **Microsoft Graph API**: A RESTful API that provides access to various Microsoft services.
*   **AutoRest**: A tool used to automatically generate client libraries for APIs.
*   **OpenAPI standard**: A standard for describing APIs.
*   **Powershell module**: A set of commands and functions that can be used in PowerShell.
*   **Azure AD module**: A PowerShell module that provides access to Azure Active Directory.
*   **Microsoft Graph Enta module**: A PowerShell module that provides a more friendly and scenario-based interface for interacting with the Microsoft Graph API.

---

*Report by: [Name] | Date: [Date] | Version: [1.0]*
