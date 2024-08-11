# local-exec provisioner

**The local-exec provisioner in Terraform runs commands on your local system after creating or deleting resources. It's useful for tasks like running scripts or setting up configurations that need to happen locally. Like when resources is created i want to run a command on my local system and when the resource is delete i want to take its backup with shell script including SSH**

## How to use

- Example :- i want to run `echo "Hello world"` command after when my inrfa is created with `terraform apply`

- Code . **Provisioner always write under the resource**

    ```bash
    provisioner "local-exec" {
      command = "echo hello world > echo.txt"
    }

- Now when my apply command seccesfully finished terraform will run this `local-exec` command. Now the one file is created in my present working directory `echo.txt`.

- If i want to change my working directory in `local-exec`.

    ```bash
    provisioner "local-exec" {
      working_dir = "/home/goldy/"
      command = "echo hello world > echo.txt"
    }

- Now the working directory is `/home/goldy`, The file `echo.txt` is created in my home directory.
- The by diffault interpretor in local exec is `bin/bash -c`. But i want to run any python code then i will change the interpretor.

    ```bash
    provisioner "local-exec" {
      interpreter = [ 
        "/usr/bin/python3", "-c"
       ]
      command = "print('hello World')"
    }

- Now i want to run any command on the destroy time of resource. By default `local-exec` run the commands on the apply time. We use `when` when we want to run the commands on the destroy time.

    ```bash
    provisioner "local-exec" {
      when = destroy
      working_dir = "/home/goldy/"
      command = "echo hello world > echo.txt"
    }
  
- Now this command is run when i run `terraform destroy`.

- If any provisioner fails during the apply time then terraform marked taint to this resource.
- if we want everything going forward on the failure of provisioner then add `on_failure`

    ```bash
    provisioner "local-exec" {
      on_failure = continue
      when = destroy
      working_dir = "/home/goldy/"
      command = "echo hello world > echo.txt"
    }

- we can replace continue with fail then resources will failes to create if any provisiner fails.

## NOTE 

- We don't have to provide connection in this provisioner.