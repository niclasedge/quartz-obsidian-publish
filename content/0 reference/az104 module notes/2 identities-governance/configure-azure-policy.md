---
{}
---
# Azure Policy and Management Groups Summary

## Azure Policy
- Service for creating, assigning, managing policies
- Enforces rules, ensures compliance
- Key capabilities:
  - Enforce rules & compliance
  - Apply at scale
  - Remediation
  - Cross-team/subscription governance

### Policy Definitions
- Express conditions & actions
- Custom or built-in
- Examples: VM size restrictions, location limits, tagging

### Initiative Definitions
- Group policies for compliance tracking
- Custom or built-in
- Example: security regulation compliance

### Implementation
1. Create policy definitions
2. Create initiative definition
3. Scope initiative
4. Check compliance

## Management Groups
- Scope/control above subscriptions
- Organize subscriptions, apply governance
- Key points:
  - Inheritance from parent groups
  - Up to 6 hierarchy levels
  - Target policies/budgets across subscriptions
  - Unified policy/access management

### Usage Scenarios
- Align with org structure
- Apply inherited policies
- Manage compliance
- Consolidate cost reporting

## Best Practices
- Use management groups for subscription organization
- Create initiatives, even for few policies
- Use built-in policies/initiatives when possible
- Scope policies carefully
- Regular compliance checks