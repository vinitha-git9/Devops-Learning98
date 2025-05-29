
Terraform is an open-source Infrastructure as Code (IaC) tool developed by HashiCorp. 
It allows you to define and provision infrastructure using a high-level configuration language called HashiCorp Configuration Language (HCL) or optionally JSON.

Terraform helps manage cloud services (like AWS, Azure, Google Cloud), as well as on-premises infrastructure,
with a single configuration language and set of commands.

Why is Terraform Required?

Infrastructure as Code (IaC): manage infrastructure ,repeatable, version-controlled, and automated.
Consistency Across Environments: same code used to create identical environments (e.g., development, staging, production)
Multi-Cloud Support:(AWS, Azure, GCP, Kubernetes, etc.), allowing you to manage all infrastructure from a single tool.
Dependency Management: Automatically understands resource.
Version Control:Terraform files are text-based and can be stored in Git, enabling collaboration and change tracking.
Plan and Review Before Applying: changes will be made before executing them.
Automation and Integration: Works well with CI/CD pipelines.

Install and config Terraform in linux machine:

wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform

A simple Configure Terraform (Basic Setup):

mkdir ~/terraformdemo
cd ~/main.tf
nano main.tf

terraform {
  required_version = ">= 1.0"
}

provider "local" {}

resource "local_file" "example" {
  content  = "Hello, Terraform!"
  filename = "${path.module}/hello.txt"
}

terraform init
terraform plan
terraform apply

Terraform will create a file named hello.txt with the content:

Hello, Terraform!

To remove the created resources:
 terraform detroy
