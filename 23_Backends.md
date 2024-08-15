# Terraform Backends

**backend defines where and how state data is stored and managed. supports remote storage solutions like S3, and allowing multiple users to work on the same infrastructure.**

### Requirements

- Aws cli installed and configured.

### 1. How to configures

- Now i'm going to to create s3 my remote backend.
- Firstly create a new s3 bucket with any name. 
- Code .

    ```bash
    terraform {
      backend "s3" {
        region = "us-east-1"
        bucket = "terraform-48"
        key = "terraform.tfstate"
      }
     } 

- Now replace the name and region of you s3 bucket.
- Now you have to run `terraform init`.
- Now when you run `terraform apply` your state will created in you s3 bucket.

### 2. Locking

**Imagine you and you team worker both are working on the same terraform code and you run `terraform apply` and after 5 seconds you team member also run `terraform apply`. We can solve that problem by locking**

- Create a table in DynamoDB with any name. Partition id is `lockID`.
- Now add table in your backend code.

    ```bash
    terraform {
      backend "s3" {
        region = "us-east-1"
        bucket = "terraform-48"
        key = "terraform.tfstate"
        dynamodb_table = "terraform-lock"
      }
    }

- Replace `terraform-lock` with you table name.

- Now when you run `terraform apply` then you team member could not run `terraform apply` untile your apply is not completed.

### 3. Migrate Backend

**Suppose you are using backend S3 and now you want to change it to any another backend. It is called migrate backend**

- Commet backend lines.

    ```bash
    terraform {
      # backend "s3" {
      #   region = "us-east-1"
      #   bucket = "terraform-48"
      #   key = "terraform.tfstate"
      #   dynamodb_table = "terraform-lock"
      # }
    }

- Now run `terraform init` it will give you the command og migration.
- `terraform init -migrate-state` run this command.
- Enter yes in value
- Now you tfstate file is downloaded in your local system now you can change the backend.