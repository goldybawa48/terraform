# remote-ecex provisioner

**We use remote-exec provisioner when we have to run any command on the remote server**

## How to use

- Example :- I have to install `nginx` on the remote server after the creation of resource.

    ```bash
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

    provisioner "remote-exec" {
      inline = [ 
        "sudo apt update -y",
        "sudo apt install nginx -y"
       ]
     }
    }

- I can provide my `*.sh` file with `remote-exec`.

    ```bash
    provisioner "remote-exec" {
      script = "./user.sh"
     }


**So this is how provisioners work in the terraform.**