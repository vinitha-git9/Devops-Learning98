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

Learn about state file and why it is required:

State file: A state file is a crucial component that keeps track of the infrastructure resources that the tool manages.
Typically named: terraform.tfstate

It contains a JSON-formatted record of:

All resources that have been created
Resource metadata (IDs, attributes, dependencies, etc.)
The current state and configuration
Resource mappings to your code.

Why it is required:

Mapping real infrastructure to code
Detecting Drift
Performance
Tracking changes
supports collaboration

Consideration:
Sensitive data, locking, corruption/loss

🔄 Common Commands Involving State in Terraform

terraform state list
terraform state show (resource)
terraform refresh

| Concept         | Description                                                   |
| --------------- | ------------------------------------------------------------- |
| What it is      | JSON file tracking current state of managed infrastructure    |
| Why it's needed | Maps code to real resources, enables safe & efficient updates |
| Risks           | Sensitive, must be secured and managed carefully              |
| Best practice   | Use remote storage with locking for team use                  |

What is a Backend in Terraform?

A backend in Terraform determines:
where the state file is stored
how state operation like reading, locking and writing are performed
who can access and update the state file

commonly named backend.tf

Write terraform scripts to execute basic linux commands, to create and zip a file:

Step:1  How can I use Terraform to run Linux commands like "create a file" and "zip it"?

So, to run Linux commands, we need to:
Use Terraform to create a virtual machine (like an EC2 instance in AWS).
SSH into that machine automatically.
Run the Linux commands using a "provisioner."

Basic Flow
Terraform creates a Linux server (like an EC2 in AWS).
Terraform connects to that server using SSH.
It runs your Linux commands: create file → zip file.

🧩 What You Need
To make it work, you’ll need:

An AWS account
A key pair (SSH key)
Terraform installed

Let’s first do it on your own machine using local-exec.

cd /
mkdir terraform
cd terraform
nano main.tf

resource "null_resource" "file_example" {
  provisioner "local-exec" {
    command = <<EOT
      echo "Hello from Terraform" > myfile.txt
      zip myfile.zip myfile.txt
    EOT
  }
}

What this does:
Creates a file called myfile.txt with some text
Compresses (zips) that file into myfile.zip
All on your own computer, not in the cloud

terraform init
terraform apply
 You’ll see the files myfile.txt and myfile.zip in your folder.

 step:3 running Linux commands on a remote VM (like an AWS EC2 instance) using Terraform.

create a directory: mkdir demotera
cd demotera
nano ec2.tf

make sure you have:
AWS account, aws key pair, access key, 

provider "aws" {
  region = "us-east-1"      # Change to your preferred region
}

resource "aws_key_pair" "deployer" {
  key_name   = "my-key"     # Replace with your key name
  public_key = file("~/.ssh/id_rsa.pub")  # Path to your public SSH key
}

resource "aws_security_group" "ssh_access" {
  name        = "allow_ssh"
  description = "Allow SSH inbound traffic"

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]   # Allow SSH from anywhere (for testing only)
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

resource "aws_instance" "linux_vm" {
  ami                    = "ami-0c02fb55956c7d316"  # Amazon Linux 2 AMI in us-east-1; change for your region
  instance_type          = "t2.micro"
  key_name               = aws_key_pair.deployer.key_name
  security_groups        = [aws_security_group.ssh_access.name]

  tags = {
    Name = "TerraformExampleInstance"
  }
}

output "instance_public_ip" {
  value = aws_instance.linux_vm.public_ip
}


terraform init
terraform plan
terraform apply

Apply complete!
Outputs:
instance_public_ip = "3.91.123.45"

SSH into your EC2 instance using the command:

2. Set correct permissions on the key
chmod 400 ~/.ssh/id_rsa

ssh -i ~/.ssh/id_rsa ec2-user@3.91.123.45

now connected to AWS EC2 user.
