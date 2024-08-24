---
{}
---
parent: [[kk_Terraform Basics Training Course]]
tags::
status:: bereich
```dataview
table tags, status FROM [[kk_Terraform Basics Training Course]]  sort status
```


### Intro to Terraform State
- after execution, terraform creates a file in the directory
	- terraform.tfstate, storring all details of the infrastructure and state vatiables
 ![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230523094622.png]]
![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230523094844.png]]

### Purpouse of State
- performance
- collaboration
	- save statefile in remote state store (aws s3, terraform cloud)
- considerations
	- security
		- store the state file in Remote State backends (sensitive information)
	- Store the .tf files in Version Control



