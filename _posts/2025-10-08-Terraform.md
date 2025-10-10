
---

🧱 Terraform for DevOps – Complete Guide

🧩 1. What is Terraform?

Terraform is an Infrastructure as Code (IaC) tool developed by HashiCorp that allows you to provision, configure, and manage cloud resources (AWS, Azure, GCP, etc.) using declarative configuration files written in HCL (HashiCorp Configuration Language).

💡 Example:
Instead of manually creating an EC2 instance in AWS Console, Terraform does it automatically via code.


---

🧾 2. Why DevOps Uses Terraform

Infrastructure as Code (IaC) – Manage infrastructure like software.

Automation – Eliminates manual setup.

Version Control – Code stored in Git for rollback.

Multi-cloud Support – AWS, Azure, GCP, and on-prem.

Integration – Works with Jenkins, Ansible, Docker, Kubernetes.



---

⚙️ 3. Terraform Workflow

1. Write → Define .tf files (resources & providers).


2. Initialize → terraform init (downloads provider plugins).


3. Plan → terraform plan (previews actions).


4. Apply → terraform apply (creates infrastructure).


5. Destroy → terraform destroy (removes infrastructure).




---

📁 4. Basic Terraform File Structure

/my-terraform-project
 ├── main.tf
 ├── variables.tf
 ├── outputs.tf
 ├── terraform.tfvars
 └── provider.tf

Example:

provider.tf

provider "aws" {
  region = "us-east-1"
}

main.tf

resource "aws_instance" "my_ec2" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  tags = {
    Name = "DevOps-Server"
  }
}

Commands:

terraform init
terraform plan
terraform apply


---

📊 5. Variables and Outputs

variables.tf

variable "instance_type" {
  description = "EC2 instance type"
  default     = "t2.micro"
}

outputs.tf

output "instance_id" {
  value = aws_instance.my_ec2.id
}

terraform.tfvars

instance_type = "t3.micro"


---

🧮 6. State Files (terraform.tfstate)

Stores current infrastructure state.

Acts as a single source of truth.

Always store it remotely (S3, Terraform Cloud, etc.) in team environments.


Example (Remote Backend):

terraform {
  backend "s3" {
    bucket = "my-tf-state-bucket"
    key    = "terraform/state"
    region = "us-east-1"
  }
}


---

🧰 7. Terraform Provisioners

Used for post-deployment configuration (e.g., installing packages).

provisioner "remote-exec" {
  inline = [
    "sudo apt update",
    "sudo apt install nginx -y"
  ]
}


---

🧩 8. Terraform Modules

Modules are reusable blocks of Terraform code.

Example structure:

modules/
  └── ec2/
       ├── main.tf
       ├── variables.tf
       ├── outputs.tf

Root main.tf

module "my_ec2" {
  source = "./modules/ec2"
  instance_type = "t2.micro"
}


---

☁️ 9. Real-world DevOps Example (Terraform + Ansible)

1. Terraform → Creates EC2 instance on AWS.


2. Ansible → Configures Apache and deploys web app.



Terraform output:

output "server_ip" {
  value = aws_instance.web.public_ip
}

Ansible inventory (auto-generated via Terraform):

[web]
${terraform output -raw server_ip} ansible_user=ubuntu


---

🧠 10. Terraform Workspaces

Used for multi-environment setups (dev, stage, prod).

Commands:

terraform workspace new dev
terraform workspace select dev

You can manage separate states for each environment.


---

🔐 11. Sensitive Data Handling

Use AWS Secrets Manager, Vault, or Terraform variable files with .gitignore.

Example:

variable "db_password" {
  sensitive = true
}


---

🧩 12. Terraform Cloud / Enterprise

Used for:

Remote state storage

Team collaboration

Role-based access

Cost estimation



---

🚀 13. Terraform + Jenkins Pipeline Example

Automate Infrastructure Deployment:

pipeline {
  agent any
  stages {
    stage('Init') {
      steps {
        sh 'terraform init'
      }
    }
    stage('Plan') {
      steps {
        sh 'terraform plan -out=tfplan'
      }
    }
    stage('Apply') {
      steps {
        sh 'terraform apply -auto-approve tfplan'
      }
    }
  }
}


---

💡 14. Terraform Advanced Topics

Topic	Description

Data Sources	Fetch existing infra data.
Dynamic Blocks	Create resources dynamically.
Count & For_each	Loop through multiple resources.
Lifecycle Rules	Manage create/update/destroy behavior.
Terraform Import	Manage existing infra.
Terragrunt	Wrapper for Terraform best practices.


Example (Count Loop):

resource "aws_instance" "servers" {
  count = 3
  ami   = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  tags = {
    Name = "Server-${count.index}"
  }
}


---

📘 15. Best Practices for DevOps

✅ Keep state remote (S3 + DynamoDB lock).
✅ Use variables & outputs consistently.
✅ Use modules for reusability.
✅ Tag all resources.
✅ Run terraform plan before apply.
✅ Store Terraform code in Git (GitOps).
✅ Use CI/CD (Jenkins, GitHub Actions).


---
