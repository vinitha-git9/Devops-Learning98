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


🔐 Security in Amazon S3
1. Identity and Access Management (IAM)
2. Bucket Policies
3. Access Control Lists (ACLs)
4. Block Public Access
5. Encryption
6. Logging & Monitoring
7. MFA (Multi-Factor Authentication) Delete

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





