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

What is SSH?
SSH stands for Secure Shell.

It is a secure way to connect to another computer remotely
You need a private key file (like MyKeyPair.pem) to prove it’s you.

ssh -i MyKeyPair.pem ec2-user@54.123.45.67

A Security Group is like a firewall for your EC2 instance.

| Type  | Protocol | Port | Source                         |
| ----- | -------- | ---- | ------------------------------ |
| SSH   | TCP      | 22   | 0.0.0.0/0 (anyone, not secure) |
| HTTP  | TCP      | 80   | 0.0.0.0/0                      |
| HTTPS | TCP      | 443  | 0.0.0.0/0                      |


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

Point to remember:
Terraform installed
AWS installed and configured
terraform components:

🔹 provider block
provider "aws" {
  region = "us-east-1"
}

🔹 resource block for EC2 instance
resource "aws_instance" "linux_vm" {
  ami           = "ami-0c02fb55956c7d316"  # Example for Amazon Linux 2 in us-east-1
  instance_type = "t2.micro"
  key_name      = "my-key-pair"            # Must match an existing EC2 key pair

  tags = {
    Name = "MyLinuxVM"
  }
}

🔹 resource block for key pair:

resource "aws_key_pair" "deployer" {
  key_name   = "my-key-pair"
  public_key = file("~/.ssh/id_rsa.pub")  # Make sure this path and file exist
}

🔹 resource block for security group (for SSH access)

resource "aws_security_group" "ssh" {
  name        = "allow_ssh"
  description = "Allow SSH inbound traffic"

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]  # Allow from anywhere (not safe for production)
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

Attach this security group to the instance:

  vpc_security_group_ids = [aws_security_group.ssh.id]

output block:
output "instance_public_ip" {
  value = aws_instance.linux_vm.public_ip
}

✅ 3. Commands to Use

terraform init     # Initialize Terraform
terraform plan     # Preview changes
terraform apply    # Create resources
terraform destroy  # Delete resources

Write terraform scipts to create S3 buckets:

mkdir terraformbucket
cd terraformbucket
nano main.tf

#provider block
provider "aws" {
  region = "us-east-1"
}
#resource block
resource "aws_s3_bucket" "my_bucket" {
  bucket = "my-unique-bucket-name-2025-009"  # must be globally unique

  tags = {
    Name        = "MyS3Bucket"
    Environment = "Dev"
  }
}
#object ownership block
resource "aws_s3_bucket_ownership_controls" "example" {
  bucket = aws_s3_bucket.my_bucket.id

  rule {
    object_ownership = "BucketOwnerEnforced"
 }
}
output "s3_bucket_name" {
  value = aws_s3_bucket.my_bucket.bucket
}

terraform init
terraform plan
terraform apply

s3_bucket_name = "my-unique-bucket-name-2025-009"

AWS CLI: 
aws s3 ls
2025-05-30 13:08:51 my-unique-bucket-name-2025-009

o/p: 

Create the IAM role /policy using Terraform:

nano main.tf

# Define IAM Policy
resource "aws_iam_policy" "example_policy" {
  name        = "example-policy"
  description = "Example IAM policy for demonstration"
  path        = "/"

  policy = jsonencode({
    Version = "2012-10-17",
    Statement = [
      {
        Action = [
          "s3:ListBucket",
          "s3:GetObject"
        ],
        Effect   = "Allow",
        Resource = [
          "arn:aws:s3:::example-bucket",
          "arn:aws:s3:::example-bucket/*"
        ]
      }
    ]
  })
}

# Define IAM Role
resource "aws_iam_role" "example_role" {
  name = "example-role"

  assume_role_policy = jsonencode({
    Version = "2012-10-17",
    Statement = [
      {
        Effect = "Allow",
        Principal = {
          Service = "ec2.amazonaws.com"
        },
        Action = "sts:AssumeRole"
      }
    ]
  })
}

# Attach IAM Policy to Role
resource "aws_iam_role_policy_attachment" "example_attach" {
  role       = aws_iam_role.example_role.name
  policy_arn = aws_iam_policy.example_policy.arn
}

terraform init
terraform plan
terraform apply

What is cloud computing:

The cloud computing is the delivery of computing services like servers, database, storage, networking and software over the internet.
Instead of owing the physical server, you can rent computer powers and services from the cloud provider.

Common Cloud Providers
AWS – Amazon Web Services
Azure – Microsoft’s cloud platform
Google Cloud Platform (GCP)

🔑 Cloud Computing Models

IaaS: Infrasturture as a Service(Example: AWS EC2, Azure Virtual Machines)
PaaS: Platform as a Service( you manage app,Easier for developers to deploy code. Eg:AWS Elastic Beanstalk, Heroku
SaaS: Software as a Service( Fully managed software delivered via the web eg: Gmail, Dropbox, Office 365) 

🏗️ Cloud Service Categories:

| Category       | Example AWS Service       | What It Does                    |
| -------------- | ------------------------- | ------------------------------- |
| **Compute**    | EC2, Lambda               | Run code or apps                |
| **Storage**    | S3, EBS, Glacier          | Store files or backups          |
| **Databases**  | RDS, DynamoDB             | Manage structured data          |
| **Networking** | VPC, Route 53, CloudFront | Manage traffic and security     |
| **Security**   | IAM, KMS, Shield          | Control access and protect data |

📈 Benefits of Cloud Computing:

Scalability – Automatically grow/shrink resources
Cost Efficiency – Pay-as-you-go
High Availability – Services across multiple regions
Security – Built-in controls and compliance

 IAM in the Cloud (Identity and Access Management)

IAM lets you:
Create User.
Define what resources they can access
securely manage permission

🛠️ Real-Life Example

Want to run the website,

Launch a virtual server (EC2)
Store images/files (S3)
Use a database (RDS)
Restrict access using IAM

Types of deployment model:

1.Deployment model:

Public cloud:Owned and operated by third-party cloud providers like AWS, Azure, GCP.
Example: Hosting a website on AWS EC2.

Private cloud: Cloud infrastructure is used exclusively by one organization.
Example: A bank hosting internal applications on its own data center.

Hybrid Cloud:A mix of public and private clouds working together.
Example: An e-commerce app that runs the website on AWS and keeps customer records in a private cloud.

✅ d. Multi-Cloud
Use of multiple public cloud providers.
Example: Using AWS for compute and Azure for backup storage.

🧩 2. Service Models
| Model    | What You Manage               | What Cloud Provider Manages | Example Service               |
| -------- | ----------------------------- | --------------------------- | ----------------------------- |
| **IaaS** | OS, apps, runtime, middleware | Hardware, virtualization    | AWS EC2, Azure VM             |
| **PaaS** | Your application/code only    | OS, runtime, infrastructure | AWS Elastic Beanstalk, Heroku |
| **SaaS** | Just use the software         | Everything else             | Gmail, Dropbox, Salesforce    |

| Type              | Key Focus              | Example Use Case                   |
| ----------------- | ---------------------- | ---------------------------------- |
| **Public Cloud**  | General-purpose use    | Hosting apps/websites              |
| **Private Cloud** | Secure, customized use | Internal enterprise systems        |
| **Hybrid Cloud**  | Mix of both            | Scalable & secure app hosting      |
| **Multi-Cloud**   | Diverse provider use   | Risk mitigation, best-of-breed use |
| **IaaS**          | Infrastructure control | Hosting VMs, building networks     |
| **PaaS**          | App development        | Rapid coding, auto-scaling apps    |
| **SaaS**          | End-user software      | Email, CRM, document management    |

how to access the EC2 instance from local machine (windows/Linux) using SSM:

step1: create IAM role -> AmazonSSMMangedinstancecore ->add this permission
step2: Launch instance-> remove SSH-> advanced tools-> instance congifure ->add role rule
step3: open ubuntu-> start the session->aws ssm start-session --target <instance-id>
step4: shell opens-> install nginx and apply simple script
sudo apt update
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx

echo '<!DOCTYPE html><html><body><h1>Hello from NGINX via SSM!</h1></body></html>' \
  | sudo tee /usr/share/nginx/html/index.html

sudo systemctl status nginx

4. Allow HTTP Traffic (Security Group)
Outside of SSM, make sure your EC2's security group allows:

Inbound rule for port 80 (HTTP)

From your IP or 0.0.0.0/0 (for testing)

http://<your-ec2-public-ip>/

what is cloud: is the delivery of computing services like servers, storage, databases, networking, software, and more—over the internet ("the cloud").
why cloud: cost effective,accessibility,security, scalabitity, speed and agility

Types of cloud: Deployment and Service model

Deployment model:Public(you can access the cloud publicly),
private(you own one private cloud for an organisation)
hybrid cloud(mix of public and private)

Service model: IAAS(, PaaS, SaaS)

| Component                  | Purpose                              | Scope        | Used For                                  |
| -------------------------- | ------------------------------------ | ------------ | ----------------------------------------- |
| **Region**                 | Group of data centers in a location  | Global       | Choose based on user location/legal needs |
| **Availability Zone (AZ)** | Independent data centers in a Region | Regional     | High availability & fault tolerance       |
| **Edge Location**          | Content delivery points              | Global       | Fast delivery using caching/CDN           |
| **Local Zone**             | Extension of Region near users       | Metro cities | Low-latency workloads                     |

Characteristics of cloud:
On demand self service
Resource pooling
board network access
measured service(pay as you go)
Elasticity and scalability

Learn about pricing and purchasing plans in AWS:
 Pricing: AWS follow pay as you go model

Purchase plan:
Free tier: free for 12 month
Reserved instances: commit to use the instance for 1 to 2 years
On demand pricing:Pay per hour or per second
Spot instances:Buy unused EC2 capacity at up to 90% discount
Savings plan:Flexible pricing model 

Disaster recovery (DR) is a critical part of cloud architecture
recover quickly from failures like hardware issues, data loss, or entire region outages.

Disaster recovery strageries:
backuo and restore:regular backups (amazon s3)
pilot light: minimal version of your environment(EC2 AMI's)
warm standby:scaled-down but fully functional version of your environment (route 53)
multi-site:fully functional systems in two or more locations(Global Load Balancing (Route 53)
| Service                                 | Purpose                                  |
| --------------------------------------- | ---------------------------------------- |
| **AWS Backup**                          | Centralized backup management            |
| **Amazon S3 Glacier**                   | Low-cost long-term backup                |
| **AWS Elastic Disaster Recovery (DRS)** | Fast failover and replication            |
| **AWS CloudFormation**                  | Infrastructure as Code for fast rebuilds |
| **Amazon Route 53**                     | DNS failover and traffic routing         |

Latency: is a delay between the user action and system response.
time it takes data to travel :
->user and cloud
->service with aws
->bewtween az and region

⚡ Common Sources of Latency in AWS
Geographic distance
network routing
server performance
service interaction
Data Transfer Between AZ/Region

AWS Tools & Services That Help Reduce Latency:
->amazon cloufront
->AWS global accelator
->amazon route 53
->aws local zones
->Elastic load balancing

Amazon EC2 – Virtual servers in the cloud
Amazon S3 – Scalable object storage
IAM – Secure access control and identity management
Amazon RDS – Managed relational databases
Lambda – Serverless function execution
VPC – Isolated virtual network environment
CloudFront – Content delivery network (CDN)
Route 53 – Scalable DNS and domain management
EBS – Block storage for EC2
CloudWatch – Monitoring and logging service
DynamoDB – Serverless NoSQL database
Elastic Beanstalk – Platform-as-a-Service for apps
ECS/EKS – Container orchestration services
AWS Backup – Centralized backup automation
SNS/SQS – Messaging and queuing services

