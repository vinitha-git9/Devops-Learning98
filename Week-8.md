What is S3:

is a Simple Storage Service
It is a cloud-based object storage service used to store files like:
Documents,Images,Videos,Backups,Logs,Static website files (like HTML, CSS, JS)

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


Key Features of S3:
Object-based storage: Stores data as objects (not files or blocks), each containing data, metadata, and a unique key.
Unlimited storage: You can store as much data as you want.
High durability: Designed for 99.999999999% (11 9's) durability.
Scalability: Automatically scales to handle growing amounts of data and traffic.
Security: Supports encryption, IAM, bucket policies, and ACLs.
Versioning: Tracks changes to objects, allowing recovery of deleted or modified files.
Static website hosting: Can serve HTML/CSS/JS files directly via HTTP.
Lifecycle policies: Automate transitions between storage classes or deletion of old data.

Storage tiers:

| Storage Class               | Use Case                              | Key Feature                         |
| --------------------------- | ------------------------------------- | ----------------------------------- |
| **S3 Standard**             | Frequently accessed files             | Fast access, high availability      |
| **S3 Intelligent-Tiering**  | Data with changing access patterns    | Auto-moves data to cheaper tier     |
| **S3 Standard-IA**          | Infrequently accessed files           | Lower cost, but small retrieval fee |
| **S3 One Zone-IA**          | Infrequent access, not critical files | Stored in a single AZ, cheaper      |
| **S3 Glacier**              | Archive storage (long-term backups)   | Cheap, 1-5 min retrieval            |
| **S3 Glacier Deep Archive** | Rarely accessed (e.g. yearly backups) | Lowest cost, 12+ hours to restore   |

Security:
| Security Layer        | Purpose                                    | Recommended  |
| --------------------- | ------------------------------------------ | ------------ |
| IAM Policies          | Control user/role access                   | ✅            |
| Bucket Policies       | Control access to buckets                  | ✅            |
| ACLs                  | Object-level control (legacy)              | ❌ Avoid      |
| Block Public Access   | Prevent accidental public exposure         | ✅            |
| Encryption at Rest    | Protect stored data                        | ✅            |
| Encryption in Transit | Protect data on the move                   | ✅            |
| S3 Access Logging     | Monitor access                             | ✅            |
| MFA Delete            | Protect from accidental deletions          | ✅ (optional) |
| Versioning            | Recover from accidental overwrites/deletes | ✅            |

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

Terraform for S3:

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

When a user makes a request for your content, CloudFront delivers it from the nearest edge location, reducing latency and improving load times. This ensures low-latency delivery, high transfer speeds, and an optimized user experience.

it easily integrates with other AWS services like Amazon S3, EC2, Lambda@Edge, and API Gateway.

How cloud front works:
 Step 1: User Requests Content
 Step 2: DNS Routes the Request
 Step 3: CloudFront Checks for Cached Content

If it’s stored: CloudFront gives the content right away.
If not stored: CloudFront sends the request to the main server to get the content.
Step 4: Content Comes from the Origin Server
Step 5: CloudFront Caches the Content
Step 6: CloudFront Delivers Content
Step 7: Future Requests
Step 8: Cache Update (When Needed)

Key Features of AWS CloudFront:

1. Faster Content Delivery Across the Globe
2. Works Seamlessly with AWS Services
3. Built-in Security & Protection Against Attacks
4. Efficient Caching for Both Static & Dynamic Content
5. Budget-Friendly & Scales with Your Needs
6. Customizable with Lambda@Edge

Pricing Component	Description	Cost:
Data Transfer Out	Data delivered from CloudFront to the internet.	Starting at $0.085 per GB for the first 10 TB/month in the U.S., Mexico, and Canada. 
HTTP/HTTPS Requests	Number of requests processed by CloudFront.	$0.0075 per 10,000 HTTP requests; $0.0100 per 10,000 HTTPS requests in the U.S. region. 
Invalidation Requests	Removing cached objects before expiration.	First 1,000 paths free each month; $0.005 per path thereafter. 
Real-Time Log Requests	Detailed logging of CloudFront requests.	$0.01 per 1,000,000 log lines. 
Origin Shield Requests	Additional caching layer to reduce origin load.	$0.0075 per 10,000 requests in the U.S. region. 

Terraform for CloudFront:

 1. Requirements
An S3 bucket (with static website hosting enabled)
A public ACM certificate (in us-east-1c region for CloudFront)
A custom domain (optional)
Terraform installed locally

Create static s3 site with HTTPS:

S3 bucket with static website hosting
ACM SSL certificate (in us-east-1, required for CloudFront)
CloudFront distribution with HTTPS
Route 53 record pointing to your domain (optional)

IAM Basics:
IAM is a service by AWS that lets you securely control access to AWS services and resources.

It allows you to manage:
Who can access your AWS resources
What actions they can perform
Which resources they can access

| Component       | Description                                                                                      |
| --------------- | ------------------------------------------------------------------------------------------------ |
| **User**        | An individual identity with credentials to access AWS (e.g., admin, developer)                   |
| **Group**       | A collection of IAM users; you can assign **policies** to a group                                |
| **Policy**      | A JSON document that defines permissions (Allow/Deny)                                            |
| **Role**        | An IAM identity **you can assume temporarily** — often used by services (e.g., EC2 to access S3) |
| **Access Key**  | Used by IAM users to access AWS programmatically (CLI, SDK)                                      |
| **Permissions** | Defined using policies that determine what a user or role can do                                 |


What Are Access Keys and Secret Keys?
They are credentials used by IAM users to make programmatic requests to AWS (via:
AWS CLI
SDKs (like Python Boto3, Node.js, etc.)

Terraform:

Key	Description
Access Key ID	Public identifier (like a username)
Secret Access Key	Private key (like a password)

❗ Keep the Secret Key secure — it’s only shown once when you create it!

