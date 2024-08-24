---
{}
---
parent: [[kk_Terraform Basics Training Course]]
tags::
status:: bereich
```dataview
table tags, status FROM [[kk_Terraform Basics Training Course]]  sort status
```

### Terraform Comands

terraform validate - checks if the configuration is valid or there is an error
terraform fmt - formats comand
	- formats code in canonical format
terraform show
	- terraform show -json: shows output in json
terraform providers, shows the used providers
	- terraform providers mirror /root/terraform/
terraform output
	- prints all output variables
terraform refresh, refreshes the state file
	- automatic with plan
terraform graph
	- apt isntall graphviz -y
	- terraform graph | dot -Tsvg > graph.svg
	- ![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230523133615.png]]
