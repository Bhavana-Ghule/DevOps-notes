**What is Terraform?**
- Terraform is an Infrastructure as Code (IaC) tool created by HashiCorp.
- Using Terraform, we can create, update, and delete infrastructure with a single command.
- Terraform works on multiple cloud platforms like AWS, Azure, and GCP.

What is Terraform Plugin?
- It is an external component that helps Terraform communicate with multiple cloud providers and services.

Difference between Terraform and HCL (HashiCorp Configuration Language)

Terraform is a tool.
HCL is the language used to write Terraform configuration files.
-It is a human-readable declarative language used to define and create infrastructure resources.

Difference between Terraform and CloudFormation

* Terraform supports multi-cloud environments like AWS, Azure, and GCP.
* CloudFormation supports only AWS services.
* Terraform uses **HCL (HashiCorp Configuration Language)**.
* CloudFormation uses **YAML** or **JSON** templates.
* Terraform is an open-source Infrastructure as Code tool by HashiCorp.
* CloudFormation is an AWS-managed service.
* Terraform is mainly used to automate infrastructure across different cloud providers.
* CloudFormation supports only AWS services.

---

# Explain a Terraform Resource with an Example

```hcl
resource "aws_instance" "myserver" {
  ami           = "ami-12345678"
  instance_type = "t3.micro"
}
```

This resource creates an AWS EC2 instance.

---

# Creating an EC2 Instance through Terraform

### Step 1

* Open Microsoft PowerShell.
* Install Terraform using:

```powershell
winget install Hashicorp.Terraform
```

* Verify Terraform installation:

```powershell
terraform version
```

* Download and install VS Code.
* Create a file named **main.tf**.

---

### Step 2

To connect VS Code with AWS, we need to add the AWS provider configuration from the Terraform Registry.

Copy the provider code:

```hcl
provider "aws" {
  region     = "us-east-1"
  access_key = "YOUR_ACCESS_KEY"
  secret_key = "YOUR_SECRET_KEY"
}
```

Choose the region according to the AMI you are using.

Now create the EC2 instance resource:

```hcl
resource "aws_instance" "example" {
  ami           = "ami-xxxxxxxxxxxxxxxxx"
  instance_type = "t3.micro"

  tags = {
    Name = "New-Terraform-Instance"
  }
}
```

---

### Step 3

In the VS Code terminal, run:

```bash
terraform init
```

After the resource code is saved, run:

```bash
terraform plan
```

```bash
terraform apply
```

Type:

```text
yes
```

to confirm the creation.

---
terraform destroy -auto approved
### Step 4

* Your EC2 instance is successfully created.
* Verify the instance in the AWS EC2 Console.

---

These notes follow the same structure as your notebook but with corrected grammar and clearer wording.
