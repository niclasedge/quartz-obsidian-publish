---
{}
---
parent: [[kk_Terraform Basics Training Course]]
tags::
status:: bereich
```dataview
table tags, status FROM [[kk_Terraform Basics Training Course]]  sort status
```
## Installing Terraform
## HashiCorp Configuration Language (HCL) Basics
```hcl local.tf
resource "local_file" "pet" {
filename = "/root/pets.txt"
content = "we love pets"
}
```
![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230508152716.png]]

![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230508152913.png]]

### Provision infrastructure workflow
1. write the hcl file
2. run the `terraform init`
3. review the execution plan using the `terraform plan` comand
4. apply the changes using the `terraform apply` comand
![[_special notes/docusaurus/docs/IaC/Terraform/Pasted image 20230508153601.png]]

### Update and Destroy the resource
Update
- change something in the hcl file anr run `terraform apply`
Delete
- to delete run `terraform destroy`