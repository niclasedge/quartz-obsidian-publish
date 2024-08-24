---
{}
---
# Azure Resource Manager Templates: Comprehensive Guide

## 1. Introduction
- JSON files defining infrastructure and configuration
- Enable consistent, repeatable deployments

## 2. Benefits
- Improved consistency
- Complex deployment expression
- Reduced manual errors
- Infrastructure as Code
- Reusability
- Modularity
- Simplified orchestration

## 3. Template Schema
```json
{
  "$schema": "http://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "",
  "parameters": {},
  "variables": {},
  "functions": [],
  "resources": [],
  "outputs": {}
}
```

## 4. Parameters
```json
"parameters": {
  "<parameter-name>": {
    "type": "<type-of-parameter-value>",
    "defaultValue": "<default-value-of-parameter>",
    "allowedValues": [ "<array-of-allowed-values>" ],
    "minValue": <minimum-value-for-int>,
    "maxValue": <maximum-value-for-int>,
    "minLength": <minimum-length-for-string-or-array>,
    "maxLength": <maximum-length-for-string-or-array-parameters>,
    "metadata": {
      "description": "<description-of-the parameter>"
    }
  }
}
```

## 5. Bicep Templates
- Domain-specific language for Azure deployments
- Simpler syntax than JSON
- Features:
  - Modules
  - Automatic dependency management
  - Type validation and IntelliSense

## 6. QuickStart Templates
- Community-provided templates
- Available at: https://azure.microsoft.com/resources/templates/
- Useful for learning and starting points

## 7. Best Practices
- Use parameters for values that change
- Use variables for repeated values
- Follow naming conventions
- Comment your templates
- Use linked templates for complex deployments

## 8. Deployment
- Azure portal
- Azure PowerShell
- Azure CLI
- REST API
- GitHub Actions

## 9. Additional Resources
- [ARM template documentation](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/)
- [Bicep documentation](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/)
- [Template best practices](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/best-practices)