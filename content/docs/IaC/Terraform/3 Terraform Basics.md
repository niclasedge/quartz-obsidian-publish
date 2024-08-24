---
{}
---
parent: [[kk_Terraform Basics Training Course]]
tags::
status:: bereich
```dataview
table tags, status FROM [[kk_Terraform Basics Training Course]]  sort status
```
## Terraform Providers
![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230508161103.png]]

![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230508161334.png]]

## Configuration Directory
and Filenaming

 ![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230508161631.png]]

### input variables

![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230509095258.png]]
![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230509095329.png]]
![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230509095358.png]]
![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230509095632.png]]
![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230509095503.png]]
![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230509095547.png]]
![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230509095723.png]]
- Tuples can have different types, other than list

![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230509101123.png]]
- the inline deffinition overrides the above


### Ressource Attributes
![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230509151445.png]]

### Ressource Dependencies
- implicit: specify via variable, terraform automatically creates resources who have dependencies at the end
- explicit: via depends_on specifying 
- ![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230515110654.png]]

### Output Variables
- to store value of expression
- dispay details when executing
- for later use in other automation tools
![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230515115140.png]]



