# datasource

**data source in Terraform is a way to get information about things that already exist outside your Terraform setup. For example, finding new ami image of ubuntu we can use datadource**

## How to use

- Example :- I set hard core ami id in terraform code after some time aws change the ami id, Now i don't know this changing. To solve this we use datasource, datasource will find the new ami id of ubuntu or any other opreting system.
- Syntax-

    ```bash
    data "aws_ami" "ubuntu" {
      most_recent = true
      owners = ["099720109477"]
      filter {
        name = "name"
        values = ["ubuntu/images/hvm-ssd-gp3/ubuntu-noble-24.04-amd64-server-*"]
      }
      filter {
        name = "root-device-type"
        values = ["ebs"]
      }
      filter {
        name = "virtualization-type"
        values = ["hvm"]
      }
    }

- After the `data` we have to give the resource name in which we want to search.
- `most_recent` = it is true or false.
- `owener` = here we have to give the value of the owner of image. We can find it from ami session of ec2.
- `filters` we can add filter in our datasource, like i want to filter a image based on the `name, root-device-type and virtualization` then terraform will find the image based on these filters.

- Now print the id of you `ami` with `output`.

    ```bash
    output "ami-id" {
      value = "${data.aws_ami.ubuntu.id}"
    }

### How to use this id with instance

- Full code .

    ```bash
    data "aws_ami" "ubuntu" {
      most_recent = true
      owners      = ["099720109477"]
      filter {
        name   = "name"
        values = ["ubuntu/images/hvm-ssd-gp3/ubuntu-noble-24.04-amd64-server-*"]
      }
      filter {
        name   = "root-device-type"
        values = ["ebs"]
      }
      filter {
        name   = "virtualization-type"
        values = ["hvm"]
      }
    }

    output "name" {
      value = data.aws_ami.ubuntu.id
    }

    resource "aws_instance" "instance" {
      ami             = data.aws_ami.ubuntu.id
      instance_type   = "t2.micro"
      key_name        = "goldy"
      security_groups = ["default"]

      tags = {
        Name = "HelloWorld"
      }
    }