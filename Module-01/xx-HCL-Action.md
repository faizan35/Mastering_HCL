### HCL in Action

#### 1.2.1 Installing Required Tools

**Install Terraform:**

- Follow the official installation guide for Terraform: Terraform Installation Guide

**Verify Installation:**

- Open a terminal and run `terraform --version` to ensure a successful installation.

#### 1.2.2 Setting Up a Basic Project Structure

**Create a New Project Directory:**

```bash
mkdir terraform-intro cd terraform-intro
```

**Initialize a Terraform Configuration File:**

```bash
touch main.tf
```

#### 1.2.3 Writing and Running a Simple HCL Script

**Open `main.tf` in a Text Editor:**

```hcl
# main.tf

provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

**Understand the HCL Script:**

- The script defines an AWS provider with the specified region.
- It declares an AWS EC2 instance using the specified Amazon Machine Image (AMI) and instance type.

**Run Terraform Commands:**

1.  Initialize the Terraform configuration:

    ```bash
    terraform init
    ```

2.  Preview the changes to be applied:

    ```bash
    terraform plan
    ```

3.  Apply the changes to create the AWS EC2 instance:

    ```bash
    terraform apply
    ```

4.  Verify the created resources on the AWS Console.

---

### Exercise:

1.  **Explore Terraform Commands:**

    - Understand the purpose of `terraform init`, `terraform plan`, and `terraform apply`.
    - Experiment with other Terraform commands like `terraform destroy` and `terraform refresh`.

2.  **Modify the Configuration:**

    - Experiment with changing the AWS region, instance type, or any other parameters in the `main.tf` file.

3.  **Version Control Setup:**

    - Initialize a Git repository in your project directory.
    - Add and commit your Terraform configuration file.
