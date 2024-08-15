# Modules

**Modules in Terraform are reusable sets of Terraform configuration files. By using modules, you can break down complex infrastructure into smaller, manageable parts, making your code more organized and easier to maintain. You can also share and reuse modules across different projects.**

## How to use

- Create a file in ./module/main.tf this location. In this file write code to make instance.

    ```bash
    resource "aws_instance" "goldy1" {
      ami             = "ami-04a81a99f5ec58529"
      instance_type   = "t2.micro"
      key_name = "your-key-name"
      security_groups = [ "default" ]

      tags = {
        Name = "terraform"
      }
    }

- Now write a a file in another location main.tf.

    ```bash
    module "instance" {
      source = "./module"
    }

- In my module directory my instance code is placed. Now i give the path in `source` of instance code directory.
- If i run `terraform apply` then terraform create a resource which i define in `./module` directory.

### 1. To change anything in module

**Now i want to change instance type but in `./module/main.tf` file instance type in t2.micro i want t2.small**

- Create a variable.tf and files in module folder.

- variable.tf.

    ```bash
    variable "ami" {
    }

    variable "instance_type" {
    }

    variable "key_name" {
    }

    variable "security_groups" {
    }

    variable "Instance_name" {
    }

- `main.tf` of module folder.

    ```bash
    resource "aws_instance" "goldy1" {
      ami             = var.ami
      instance_type   = var.instance_type
      key_name        = var.key_name
      security_groups = ["${var.security_groups}"]

      tags = {
        Name = var.Instance_name
      }
    }

- Now in you your source file.

    ```bash
    module "instance" {
      source = "./module"
      instance_type = "t2.small"
      ami="123456789"
      Instance_name="bawa"
      security_groups="default"
      key_name="goldy"
    }

- Now you can change whatever you want.

- Additionally we can add variable.tf and terraform.tfvars file in this for values.


### 2. Print output in modules

- I want to print public ip of instance.
- In you module folder create a file `output.md`.

    ```bash
    output "pubicIP" {
      value = aws_instance.goldy1.public_ip
    }

-  Now in source file Give the refrence of this.

    ```bash
    module "instance" {
      source = "./module"
      instance_type = "t2.small"
      ami="ami-04a81a99f5ec58529"
      Instance_name="bawa"
      security_groups="default"
      key_name="goldy"
    }

    output "pubicIP" {
      value = module.instance
    }

- Now run `terraform apply` you can see in the output. `publicIP = know after apply`.