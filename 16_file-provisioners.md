# Provisioners

**In terraform ther are three types of provisioners `File provisioner`, `local-exec provsioner` and `remote-exec provisioner`.**

**In this chapter we will talk about file provisioners.**

## File provisioners

**File provisioners in Terraform are used to upload files from your local machine to a resource. This is useful for transferring configuration files, scripts, or other assets needed for the resource setup.**

- Example :- I have to send a file index.html from my local system to my remote system i can to this with the help of file provisioner.

- code .

    ```bash
    provisioner "file" {
      source = "index.html"
      destination = "/home/ubuntu/index.html"
      connection {
        type = "ssh"
        user = "ubuntu"
        private_key = file("${path.module}/goldy.pem")
        host = "${aws_instance.web.public_ip}"
      }
    }

- After `provisioner` we have to define provisioner type.
- Source is a file which i want to send.
- Destination is a path of remote.
- we have to give connection type in this.
- I think all the connection  atributes you know because we discuss all about theses in last chapters.

- Proper working code with instance.

    ```bash
    provider "aws" {
      region = "us-east-1"
      access_key = "${var.access-key}"
      secret_key = "${var.secret-key}"
    }


    resource "aws_instance" "web" {
      ami           = "ami-04a81a99f5ec58529"
      instance_type = "t2.micro"
      key_name = "goldy"
      security_groups = [ "default" ]

      tags = {
        Name = "HelloWorld"
      }

    provisioner "file" {
      source = "index.html"
      destination = "/home/ubuntu/index.html"
      connection {
        type = "ssh"
        user = "ubuntu"
        private_key = file("${path.module}/goldy.pem")
        host = "${aws_instance.web.public_ip}"
      }
     }
    }

- We can also send the content using this.

    ```bash
    provisioner "file" {
      content = "Hello from Goldy"
      destination = "/home/ubuntu/content.html"
      connection {
        type = "ssh"
        user = "ubuntu"
        private_key = file("${path.module}/goldy.pem")
        host = "${aws_instance.web.public_ip}"
      }
     }

- The connection part in provisioners is repeating. So it's solution is

    ```bash
    provider "aws" {
      region = "us-east-1"
      access_key = "${var.access-key}"
      secret_key = "${var.secret-key}"
    }

    resource "aws_instance" "web" {
      ami           = "ami-04a81a99f5ec58529"
      instance_type = "t2.micro"
      key_name = "goldy"
      security_groups = [ "default" ]

      tags = {
        Name = "HelloWorld"
      }

      connection {
        type = "ssh"
        user = "ubuntu"
        private_key = file("${path.module}/goldy.pem")
        host = "${aws_instance.web.public_ip}"
      }

    provisioner "file" {
      source = "index.html"
      destination = "/home/ubuntu/index.html"
    }

    provisioner "file" {
      content = "Hello from goldy"
      destination = "/home/ubuntu/content.html"
     }
   }
