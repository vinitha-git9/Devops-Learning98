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


🛠️ Basic Terraform Commands

| **Command**           | **Use / Description**                                                              |
| --------------------- | ---------------------------------------------------------------------------------- |
| `terraform init`      | Initializes the working directory with necessary files and provider plugins.       |
| `terraform plan`      | Shows what changes will be made before applying them. Helps you review the impact. |
| `terraform apply`     | Applies the configuration and creates/modifies infrastructure.                     |
| `terraform destroy`   | Destroys the infrastructure defined in the configuration.                          |
| `terraform validate`  | Checks whether the configuration is syntactically valid.                           |
| `terraform fmt`       | Formats `.tf` files to a standard style.                                           |
| `terraform show`      | Displays the current state or plan in a human-readable format.                     |
| `terraform output`    | Shows the output values defined in your config after applying.                     |
| `terraform state`     | Advanced command to inspect or modify Terraform state files.                       |
| `terraform providers` | Lists all providers used in the current configuration.                             |
| `terraform version`   | Displays the Terraform version installed.                                          |


🚀 Suggested Command Workflow

terraform init        # Initialize the project
terraform validate    # Check for syntax errors
terraform fmt         # Format your code
terraform plan        # Preview the changes
terraform apply       # Apply changes
terraform destroy     # (Optional) Tear everything down


