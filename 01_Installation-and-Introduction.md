# Terraform

Terraform is an open-source tool created by HashiCorp. It helps you manage your infrastructure using code. You can define and set up your data center infrastructure with a language called HashiCorp Configuration Language (HCL). Terraform makes it easy to automate, update, and version your infrastructure resources.

## Getting Started with Terraform

- **Install Terraform**: Install Terraform on your local machine.
- **Write Configuration**: Define your desired infrastructure state using HCL in .tf files.
- **Initialize**: Run `terraform init` to initialize your working directory containing Terraform configuration files.
- **Plan**: Use `terraform plan` to preview the changes that will be applied to your infrastructure.
- **Apply**: Execute `terraform apply` to provision the defined infrastructure.
- **Manage**: Use `terraform destroy` to tear down infrastructure when it's no longer needed.
- **Don't worry we will discuss about all these commands in the next chapters**

## Installation

1. install necessary dependencies.
   ```bash
   sudo apt-get install -y gnupg software-properties-common curl

2. Add the HashiCorp GPG key.
   ```bash
   curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -

3. Add the official HashiCorp Linux repository.
   ```bash
   sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"

4. Update the package list.
   ```bash
   sudo apt-get update

5. Install Terraform.
   ```bash
   sudo apt-get install -y terraform

6. Verify the installation.
   ```bash
   terraform --version
