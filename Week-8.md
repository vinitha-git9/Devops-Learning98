S3: is a Simple Storage Service

It is a cloud-based object storage service used to store files like:
Documents,Images,Videos,Backups,Logs,Static website files (like HTML, CSS, JS)

How S3 Works (Basics):
S3 bucket: container to hold files
Object: set of files stored in a bucket is called object
Key: every file is named as key in the bucket
Region:Buckets are created in a specific AWS region

✅ Features of S3
Durability, versioning, scalable, access control, lifycycle rule

💡 Real-Life Examples

| Use Case                 | Example                        |
| ------------------------ | ------------------------------ |
| Website hosting          | Host HTML/CSS/JS in S3         |
| Backup storage           | Store daily or weekly backups  |
| Mobile app media storage | Store profile photos or videos |
| Big data                 | Store log files or data sets   |


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


