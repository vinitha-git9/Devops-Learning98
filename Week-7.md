# 🌐 Terraform: Infrastructure as Code

Terraform is an open-source **Infrastructure as Code (IaC)** tool developed by [HashiCorp](https://www.hashicorp.com/).  
It allows you to define and provision infrastructure using a high-level configuration language called **HCL (HashiCorp Configuration Language)** or JSON.

Terraform supports managing infrastructure on **AWS, Azure, GCP, Kubernetes**, and many other platforms.

---

## ❓ Why is Terraform Required?

- **Infrastructure as Code (IaC)**  
  Write and manage infrastructure using code — repeatable, version-controlled, and automated.

- **Consistency Across Environments**  
  Use the same codebase for dev, staging, and production environments.

- **Multi-Cloud Support**  
  Supports multiple cloud providers (AWS, Azure, GCP, Kubernetes, etc.) from a single tool.

- **Dependency Management**  
  Automatically handles resource dependencies and builds in the correct order.

- **Version Control**  
  Configuration files are plain text and can be stored in Git for team collaboration and history tracking.

- **Plan and Review Before Applying**  
  Use `terraform plan` to preview changes before execution.

- **Automation and Integration**  
  Easily integrates into CI/CD pipelines for automated deployments.

---

## 🖥️ Install Terraform on Linux

Run the following commands in your terminal:

```bash
# Add HashiCorp GPG key
wget -O - https://apt.releases.hashicorp.com/gpg | \
sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

# Add the Terraform repository
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list

# Update and install Terraform
sudo apt update && sudo apt install terraform -y


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
