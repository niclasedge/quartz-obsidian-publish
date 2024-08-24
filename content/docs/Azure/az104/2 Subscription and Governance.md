---
{}
---
parent: [[kk_AZ-104 Microsoft Azure Administrator]]
tags::
status:: bereich
```dataview
table tags, status FROM [[kk_AZ-104 Microsoft Azure Administrator]]  sort status
```

### Managing subscriptions
![[docusaurus/docs/Azure/az104/Pasted image 20230601170615.png]]
![[docusaurus/docs/Azure/az104/Pasted image 20230601170722.png]]


### Understanding the hierachy
![[docusaurus/docs/Azure/az104/Pasted image 20230601171024.png]]

### Working with RBAC
- Principal of least Privileged
	- only grant the neccessary privileged for a given job/task
![[docusaurus/docs/Azure/az104/Pasted image 20230601171135.png]]

You can apply a role on different Scopes
- depending on where the role is applied the resources (under the resource, that the role was applied to) the role also has access to those
- ![[docusaurus/docs/Azure/az104/Pasted image 20230601171712.png]]

#### Azure RBAC vs Azure AD roles
- scope at different Levels vs Scope at AD tenant level
![[docusaurus/docs/Azure/az104/Pasted image 20230601171854.png]]
![[docusaurus/docs/Azure/az104/Pasted image 20230601172017.png]]
 

### Built-in-roles and Custom Roles
![[docusaurus/docs/Azure/az104/Pasted image 20230601172150.png]]
![[docusaurus/docs/Azure/az104/Pasted image 20230601172409.png]]

### Managing access using Azure Portal
- directly add a user to the IAM Role in Azure Portal
	- Roles are inherited to the underlying ressources
![[docusaurus/docs/Azure/az104/Pasted image 20230605123128.png]]

### Azure Tags
- adding metadata using tags
	- to subscriptionn, resource groups, and resources
- Name-Value-Pair:
	- Tag Name is liomited to 512 characters, tag value 256 characters
	- assign maximum of 50 tags
- Manage Costs
	- filter for department etc.
	- tag on resource level (only resources are billed)
![[docusaurus/docs/Azure/az104/Pasted image 20230605124511.png]]

> [!info] Tags are not inherited
- inherit via azure policy

### Ressource locks
![[docusaurus/docs/Azure/az104/Pasted image 20230605124904.png]]
**Apply Resource Locks at:**
- subscription
- resource group level
- resource


### Analyzing costs


### Azure Policies