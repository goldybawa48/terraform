# Terraform workspaces

**Terraform workspaces allow you to manage multiple environments (like development, staging, and production) within the same configuration. Each workspace has its own state file, so you can use the same code to create separate environments without interfering with each other.**

## Explanation

**Like i have two .tfvar files one is for development and second is for production. When i use tfvarfile of dev. of tfstate file is created and when i use tfvarfile of prod. then terraform will modify the tfstate of dev. But i want seprate tfstate files of both Enviorments. The solution id terraform workpaces.**

### 1. How to create and use

- Create two files (dev.tfvars) (prod.tfvars). 
- Now create two workspaces one is dev and second is prod.
- Run `terraform workspace list` to list all the workspaces. By default you are using default workspace.
- Run `terraform workspace new prod` then `terraform workspace new dev`.
- Now you have three workspaces dev,prod and default.
- Now you are in dev workspace and run terraform apply the tfstate file is created in the directory `terraform.tfstate.d/dev`. 
- `terraform workspace select prod`. Now you are in prod workspace and run terraform apply the tfstate file is created in the directory `terraform.tfstate.d/prod`.  

- **So that's how workspaces work in terraform**

## Commands

- `terraform workspace list` - to list workspaces.
- `terraform workspace show` - to see current workspace.
- `terraform workspace new (Env-name)` - to create new workspace.
- `terraform workspace delete (Env)` - to delete workspace.