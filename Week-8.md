S3: is a Simple Storage Service

It is a cloud-based object storage service used to store files like:
Documents,Images,Videos,Backups,Logs,Static website files (like HTML, CSS, JS)

 Key Features of S3:
Object-based storage: Stores data as objects (not files or blocks), each containing data, metadata, and a unique key.
Unlimited storage: You can store as much data as you want.
High durability: Designed for 99.999999999% (11 9's) durability.
Scalability: Automatically scales to handle growing amounts of data and traffic.
Security: Supports encryption, IAM, bucket policies, and ACLs.
Versioning: Tracks changes to objects, allowing recovery of deleted or modified files.
Static website hosting: Can serve HTML/CSS/JS files directly via HTTP.
Lifecycle policies: Automate transitions between storage classes or deletion of old data.

How S3 Works (Basics):
S3 bucket: container to hold files
Object: set of files stored in a bucket is called object
Key: every file is named as key in the bucket
Region:Buckets are created in a specific AWS region

| Task            | Command                                    
| --------------- | ------------------------------------------ |
| Create a bucket |   aws s3 mb s3://bucket name          |
| Upload file     |  aws s3 cp file.txt s3://bucket name/ |
| Download file   |  aws s3 cp s3://bucketname/file.txt |
| List contents   |   aws s3 ls s3://bucketname  

Storage tiers:

| Storage Class               | Use Case                              | Key Feature                         |
| --------------------------- | ------------------------------------- | ----------------------------------- |
| **S3 Standard**             | Frequently accessed files             | Fast access, high availability      |
| **S3 Intelligent-Tiering**  | Data with changing access patterns    | Auto-moves data to cheaper tier     |
| **S3 Standard-IA**          | Infrequently accessed files           | Lower cost, but small retrieval fee |
| **S3 One Zone-IA**          | Infrequent access, not critical files | Stored in a single AZ, cheaper      |
| **S3 Glacier**              | Archive storage (long-term backups)   | Cheap, 1-5 min retrieval            |
| **S3 Glacier Deep Archive** | Rarely accessed (e.g. yearly backups) | Lowest cost, 12+ hours to restore   |


| Feature                          | Description                                                                                                                                                      |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **IAM Policies**                 | Controls access at the **user/role level** across AWS services.                                                                                                  |
| **Bucket Policies**              | JSON-based rules that control **who can access a bucket** and how.                                                                                               |
| **ACLs (Access Control Lists)**  | A legacy way to grant **basic read/write permissions** to users.                                                                                                 |
| **Block Public Access Settings** | Global setting to **prevent public access** at account or bucket level.                                                                                          |
| **Server-Side Encryption (SSE)** | Automatically encrypts data at rest using:<br>🔸 SSE-S3 (default Amazon keys)<br>🔸 SSE-KMS (your keys via AWS KMS)<br>🔸 SSE-C (your own customer-managed keys) |
| **Object Lock**                  | Prevents object deletion or modification for a fixed time (for compliance).                                                                                      |
| **Access Logs**                  | Logs all requests to your bucket (optional for auditing).                                                                                                        |
| **CloudTrail Integration**       | Tracks who accessed what data and when at the API level.                                                                                                         |


AWS PRICING:

Storage Cost – Charged per GB per month based on the storage class (e.g., Standard, Glacier).
Request Cost – Charges apply for each operation like PUT, GET, DELETE, etc.
Data Transfer – Outbound data transfer from S3 to the internet incurs charges.
Lifecycle Transitions – Costs apply when objects move between storage tiers (e.g., to Glacier).
Replication – Additional charges for cross-region or same-region replication of data.
Management Tools – Features like S3 Inventory, analytics, and Object Lock incur extra costs.
Early Deletion Fees – Some storage classes (like Glacier) charge if objects are deleted early.

Bucket Policy:
Bucket Policy is a JSON-based access control mechanism that defines who can access your S3 bucket and what actions they can perform.

🔹 Common Use Cases with Examples:
Allow Public Read Access – For static website hosting:
{
  "Effect": "Allow",
  "Principal": "*",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::my-bucket-name/*"
}

Allow Only a Specific IAM User:
{
  "Effect": "Allow",
  "Principal": { "AWS": "arn:aws:iam::123456789012:user/MyUser" },
  "Action": "s3:*",
  "Resource": ["arn:aws:s3:::my-bucket-name", "arn:aws:s3:::my-bucket-name/*"]
}

Restrict Access by IP Address:

 {
  "Effect": "Deny",
  "Principal": "*",
  "Action": "s3:*",
  "Resource": "arn:aws:s3:::my-bucket-name/*",
  "Condition": {
    "NotIpAddress": {
      "aws:SourceIp": "192.0.2.0/24"
    }
  }
}


Terraform is an Infrastructure as Code (IaC) tool used to automate the creation and management of S3 buckets and their configurations in AWS.

🔹 Common Terraform Examples for S3:
✅ Create a Private S3 Bucket:

resource "aws_s3_bucket" "example" {
  bucket = "my-unique-bucket-name"
  acl    = "private"
}

🔄 Enable Versioning:

resource "aws_s3_bucket_versioning" "versioning" {
  bucket = aws_s3_bucket.example.id

  versioning_configuration {
    status = "Enabled"
  }
}

 Add Lifecycle Rules:

 resource "aws_s3_bucket_lifecycle_configuration" "lifecycle" {
  bucket = aws_s3_bucket.example.id

  rule {
    id     = "archive-old-data"
    status = "Enabled"

    transition {
      days          = 30
      storage_class = "GLACIER"
    }
  }
}

Apply a Bucket Policy:


resource "aws_s3_bucket_policy" "policy" {
  bucket = aws_s3_bucket.example.id
  policy = jsonencode({
    Version = "2012-10-17",
    Statement = [{
      Effect = "Allow",
      Principal = "*",
      Action = "s3:GetObject",
      Resource = "${aws_s3_bucket.example.arn}/*"
    }]
  })
}

Step-by-Step Guide
🔸 Step 1: Create an S3 Bucket with Your Domain Name
Go to S3 Console

Click Create bucket

Bucket name = www.yourdomain.com (must match your domain exactly)

Uncheck Block all public access

Click Create bucket

🔸 Step 2: Enable Static Website Hosting
Go to the bucket → Properties

Scroll down to Static website hosting

Enable it:

Hosting type: Host a static website

Index document: index.html

Error document: error.html (optional)

Click Save changes

🔸 Step 3: Upload Your Website Files
Go to Objects tab in the bucket

Click Upload → Select index.html (and others if any)

Click Upload

🔸 Step 4: Make Your Files Public
Go to Permissions → Bucket Policy

Add this policy (replace your bucket name):

json
Copy
Edit
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicRead",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::www.yourdomain.com/*"
    }
  ]
}
Step 5: Set Up DNS in Route 53
Go to Route 53 → Hosted Zones

Click on your domain (e.g., yourdomain.com)

Click Create Record

Choose Record type: A – IPv4 address

Select Alias: Yes

Choose Alias target → From the dropdown, pick your S3 website endpoint (e.g., s3-website-us-east-1.amazonaws.com)

Name: www or root (@) depending on setup

Click Create records

🔸 Step 6: Test Your Website
Wait for DNS to propagate (usually 1–5 minutes)

Open http://www.yourdomain.com

Learn how to created terraform code for S3:

cd /
nano main.tf

provider "aws" {
  region = "us-east-1"  # Change this to your desired region
}

resource "aws_s3_bucket" "example" {
  bucket = "vinitha98-example-bucket"  # MUST be globally unique
  acl    = "private"
}

terraform init
terraform plan
terraform apply


Cloud front:

Amazon CloudFront is a Content Delivery Network (CDN) service from AWS that securely delivers data, videos, applications, 
and APIs to users globally with low latency and high transfer speeds.

Features of Amazon CloudFront:
Global Content Delivery
Content Caching
HTTPS & SSL Support
Origin Flexibility
Custom Error Pages
Real-Time Logs & Metrics
Security Integration
Cache Invalidation
Geo-Restriction
Lambda@Edge

CloudFront & IAM Basics Guide
1. CloudFront
i) Features
Learn about the Amazon CloudFront service and its key features such as global edge locations, content caching, low latency delivery, and DDoS protection.

ii) Configuration
Understand how to configure CloudFront with an origin (like an S3 bucket), set viewer protocol policies, default root object, and caching behavior.

iii) Pricing
CloudFront pricing depends on data transfer, requests, and region-specific rates. Check the CloudFront Pricing Page for details.

iv) Terraform for CloudFront
Learn how to create infrastructure as code for CloudFront using Terraform.

Example tasks:

Create a static S3 site.

Configure CloudFront distribution with that S3 origin.

Attach SSL (ACM certificate).

Use Terraform to automate the process.

2. ACM (AWS Certificate Manager)
Obtain an SSL certificate using AWS Certificate Manager.

Attach the certificate to your CloudFront distribution for HTTPS support.

IAM Basics
a. IAM User
Represents a person or application with long-term credentials (username/password or access keys).

b. IAM Roles
Define a set of permissions for making AWS service requests. Used by services or users temporarily assuming roles.

c. IAM Policies
JSON documents that define permissions. Attach to users, groups, or roles to grant or restrict access.

d. Groups
A collection of IAM users. Apply the same set of permissions to multiple users.

e. Access Keys & Secret Keys
Programmatic credentials used for CLI, SDK, and API access.

