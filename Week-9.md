VPC= Virtual Private Cloud

VPC stands for Virtual Private Cloud — it's your own isolated network in AWS where you can launch resources like:
EC2 (virtual servers),RDS (databases),Load balancers and more...

You control: IP address ranges,Subnets,Routing,Security (firewalls)

🧱 Key Components of VPC:
| Component                | Description                                  |
| ------------------------ | -------------------------------------------- |
| **CIDR Block**           | IP range of the VPC (e.g. `10.0.0.0/16`)     |
| **Subnet**               | Smaller sections of the VPC (private/public) |
| **Internet Gateway**     | Enables internet access for the VPC          |
| **Route Table**          | Controls routing within the VPC              |
| **Security Groups**      | Virtual firewalls for EC2 instances          |
| **NACLs (Network ACLs)** | Optional subnet-level firewalls              |

📦 Simple Architecture Example

VPC: 10.0.0.0/16
│
├── Public Subnet: 10.0.1.0/24
│   └── EC2 instance with internet access
│
├── Private Subnet: 10.0.2.0/24
    └── RDS (no internet access)

| Term           | Description                                                                                                     |
| -------------- | --------------------------------------------------------------------------------------------------------------- |
| **Public IP**  | Globally unique IP assigned to resources (like EC2) that can be accessed over the internet.                     |
| **Private IP** | IP used for communication within a VPC. Not routable on the internet.                                           |
| **IPv4**       | 32-bit address format (e.g., `192.168.0.1`). Most commonly used.                                                |
| **IPv6**       | 128-bit address format (e.g., `2400:cb00:2048:1::c629:d7a2`) with a much larger address space. Optional in VPC. |

| Term                                      | Description                                                                                  |
| ----------------------------------------- | -------------------------------------------------------------------------------------------- |
| **VPC (Virtual Private Cloud)**           | A virtual network in AWS where you launch AWS resources.                                     |
| **CIDR (Classless Inter-Domain Routing)** | IP address range for a network. Example: `10.0.0.0/16` means 65,536 IPs.                     |
| **Subnet**                                | A segment of the VPC CIDR block. Can be public (internet-facing) or private (internal only). |

| Security Tool                          | Description                                                                                           |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| **NACL (Network Access Control List)** | Subnet-level firewall. Supports **allow** and **deny** rules. Stateless.                              |
| **Security Group**                     | Instance-level firewall. Only supports **allow** rules. Stateful (response is automatically allowed). |

| Component                  | Purpose                                                                                                 |
| -------------------------- | ------------------------------------------------------------------------------------------------------- |
| **Internet Gateway (IGW)** | Allows internet access for public subnets.                                                              |
| **NAT Gateway**            | Allows **private subnets** to access the internet (for updates) without exposing the instances.         |
| **Route Table**            | A set of rules (routes) that control traffic direction. Each subnet is associated with one route table. |
| Resource | IP          | Subnet  | Access                                 |
| -------- | ----------- | ------- | -------------------------------------- |
| EC2-A    | `10.0.1.10` | Public  | Has Public IP, Internet access via IGW |
| EC2-B    | `10.0.2.10` | Private | Uses NAT Gateway for internet access   |

CIDR RANGE:

What does 10.0.0.0/24 mean?
CIDR block: 10.0.0.0/24

Subnet mask: 255.255.255.0

Total IPs:
2^(32 - 24) = 2^8 = 256 IP addresses

Usable IPs in AWS:
256 - 5 = 251 IP addresses
(Because AWS reserves 5 IPs in each subnet)

IP Address Range:
Starts from: 10.0.0.0
Ends at: 10.0.0.255

But usable host IPs are:

From 10.0.0.1 to 10.0.0.254
Because:

10.0.0.0 → Network address (not usable)

10.0.0.255 → Broadcast address (not usable)

And AWS reserves 3 more for internal use:
Router
DNS
Reserved for future

| Item          | Value                         |
| ------------- | ----------------------------- |
| CIDR Block    | `10.0.0.0/24`                 |
| Subnet Mask   | `255.255.255.0`               |
| Total IPs     | 256                           |
| Usable in AWS | 251                           |
| Suitable for  | Small subnet (public/private) |


If 10.0.0.0/16

2^(32-16)=65536
usable in AWS= 65536-5= 65531

10.0.0.0--- 10.0.0.0.65535

10.0.0.0 and 10.0.0.65535 for internet and broadcast address

total ip= 65536
cidr block=10.0.0.0/16
subnet mask=255.255.0.0
usable in AWS=65531

And AWS reserves 3 more for internal use:
Router
DNS
Reserved for future

 Learn and create VPC and subnets:

 steps1: Create VPC with CIDR block
 Step2: Create two subnet public and private with correct range
 step3: create seperate route table 

 step 4: Go to edit route table submission and add public subnet to pub-route
 and private subnet to pri route

step5: then create Internet gateway and connect it to VPC
step 6: then go to pub route --> edit---> add route ---> add Internet gateway---> save

Network ACL'S:A network access control list (ACL) is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets.

A security group acts as a virtual firewall that controls the traffic for one or more instances

| Feature                 | **Security Group**                               | **NACL (Network ACL)**                          |
| ----------------------- | ------------------------------------------------ | ----------------------------------------------- |
| **1. Type of Firewall** | **Stateful** – Response traffic is auto-allowed  | **Stateless** – Inbound & outbound rules needed |
| **2. Rule Types**       | Only **Allow** rules supported                   | Supports both **Allow** and **Deny** rules      |
| **3. Scope**            | Applied to **EC2 Instances** (network interface) | Applied to **Subnets**                          |




Internet Gateway (IGW)
✅ What is it?
An Internet Gateway is a VPC component that allows communication between resources in your VPC and the internet.

✅ Key Features:
Used to give public internet access to resources (like EC2 instances) in a public subnet.

Required for outbound and inbound traffic to/from the internet.

Must be attached to the VPC (one IGW per VPC).

✅ Use Case:
Public-facing web servers (e.g., websites hosted on EC2 or S3).

EC2 instances with public IPs need IGW for internet access.

🔁 NAT Gateway (Network Address Translation Gateway)
✅ What is it?
A NAT Gateway allows instances in private subnets to access the internet (for updates, software install, etc.) without exposing them to incoming internet traffic.

✅ Key Features:
Only allows outbound internet traffic from private subnets.

Does not allow inbound connections from the internet.

Managed AWS service, more scalable and reliable than NAT instances.

✅ Use Case:
EC2 instances in a private subnet need to download packages, updates, etc.

Used when you want to keep resources private but still allow limited internet access.
| Feature                                | Internet Gateway (IGW) | NAT Gateway    |
| -------------------------------------- | ---------------------- | -------------- |
| **Direction**                          | Inbound & Outbound     | Outbound only  |
| **Used By**                            | Public Subnet          | Private Subnet |
| **Requires Public IP?**                | Yes (on EC2)           | No             |
| **Attached To**                        | VPC                    | Subnet         |
| **Can receive traffic from internet?** | Yes                    | No             |


✅ Public Subnet Route Table (NO NAT Gateway)
📝 Goal: Instance has a public IP, must access the internet directly.

Steps to Remember:
Create Internet Gateway (IGW)
Create Route Table → Name it public-rt
Add Route:
Destination: 0.0.0.0/0
Target: Internet Gateway

Associate this route table to your public subnet

🔁 Simple Rule:

0.0.0.0/0 → Internet Gateway
✅ Private Subnet Route Table (WITH NAT Gateway)
📝 Goal: Instance has no public IP, but must access the internet (outbound only).

Steps to Remember:
Create NAT Gateway in a public subnet
Create Route Table → Name it private-rt
Add Route:
Destination: 0.0.0.0/0
Target: NAT Gateway
Associate this route table to your private subnet
🔁 Simple Rule:
0.0.0.0/0 → NAT Gateway
🧠 Easy Way to Memorize:
Subnet	Target	Internet Access	Needs Public IP?
Public	Internet Gateway	✅ Yes (in & out)	✅ Yes
Private	NAT Gateway	✅ 
Outbound only	❌ No

Learn about AMI, types of EC2 instances available, and what is a key pair?

AMI: An AMI is a blueprint for your EC2 instance

Operating system (like Amazon Linux, Ubuntu, Windows)
Installed software (web server, database, etc.)

🟢 2. Types of EC2 Instances
Family	Purpose	Example Types
General Purpose	Balanced CPU, memory	t2.micro, t3.medium
Compute Optimized	High-performance CPU workloads	c5.large, c6g.large

🟢 3. What is a Key Pair in EC2?
A Key Pair is used for secure access to your EC2 instance via SSH (Linux) or RDP (Windows).

1. AWS EC2 Basic Pricing Models
AWS offers multiple pricing options so you can choose based on your cost, performance, and availability needs.

🧾 a. On-Demand Instances
Pay-as-you-go
No long-term commitment
💡 Use When: You have short-term or unpredictable workloads

💸 b. Reserved Instances (RI)
Commit for 1 or 3 years
Get up to 75% discount compared to On-Demand
Choose Standard RI or Convertible RI
💡 Use When: You have steady workloads (e.g., production systems)

🌀 c. Spot Instances
Buy unused EC2 capacity at up to 90% discount
Can be terminated by AWS anytime
💡 Use When:Your app can handle interruptions
Great for batch jobs, CI/CD, testing, big data

🧮 d. Savings Plans
Flexible alternative to RIs
Commit to a spending level ($/hour) for 1 or 3 years
Applies to many services (EC2, Fargate, Lambda)

✅ 2. What is a Launch Template?
A Launch Template in EC2 is a pre-defined configuration used to launch instances repeatedly without re-entering settings.

✨ It Includes:
AMI ID,Instance type,Key pair,Security groups,IAM role,User data (startup scripts)
Volume settings, etc.

 What is a Volume?
In AWS, a Volume refers to an EBS (Elastic Block Store) volume — it is a virtual hard disk that you can attach to an EC2 instance.

🔹 Think of it like:
Your EC2 is a computer 💻
An EBS volume is the hard disk (C: drive or D: drive) 💽

| Feature         | Description                                        |
| --------------- | -------------------------------------------------- |
| **Type**        | EBS Volume (e.g., gp3, io1, st1, etc.)             |
| **Attached to** | One EC2 instance at a time (but can detach/attach) |
| **Use**         | Store OS, apps, files, DBs, etc.                   |
| **Size**        | You choose (e.g., 8 GB, 100 GB)                    |
| **Durability**  | Data persists even if EC2 stops                    |
| **Billing**     | You pay per GB per month                           |

What is a Snapshot?
A Snapshot is a backup of an EBS volume at a specific point in time.

🔹 Think of it like:
A snapshot is a photo of your hard disk that you can restore later


| Feature         | Description                                             |
| --------------- | ------------------------------------------------------- |
| **Type**        | Stored in Amazon S3 (managed by AWS, not visible in S3) |
| **Used for**    | Backup, restore, creating new volumes                   |
| **Incremental** | Only changes since last snapshot are stored             |
| **Restorable?** | Yes, you can create a new volume from any snapshot      |
| **Billing**     | You pay only for data stored (not full volume size)     |


What is EFS?
EFS (Elastic File System) is a fully managed, shared, scalable file storage service for use with EC2 and other AWS services.

Think of EFS like a shared drive (network file system) that multiple EC2 instances can mount at the same time — like a cloud version of an NFS server.

What is Instance Store?
Instance Store is temporary block-level storage that comes physically attached to the host machine running your EC2 instance.
Unlike EBS or EFS, instance store data is lost when:
The instance stops
The instance terminates
The host fails

What is a Snapshot in AWS?
A snapshot is a point-in-time backup of an EBS volume.
It's stored in Amazon S3 (internally — not visible in your S3 console).
You can restore a snapshot to create a new EBS volume.

Snapshot Lifecycle
EC2 instance uses an EBS volume
You create a snapshot of the volume
You can later:
Restore to new EBS volume
Launch a new EC2 instance using that volume
Copy to another region

 1. What is Auto Scaling and Why Do We Use It?
Auto Scaling means automatically increasing or decreasing the number of EC2 instances (servers) in your application based on current demand.

✅ Why it's useful:

Saves money by removing unused instances
Maintains performance by adding instances when needed
Handles unexpected traffic spikes
Reduces manual work – it’s automatic!

⚙️ 2. Step Scaling and Target Tracking Policies
📏 Step Scaling:
You set steps or levels for scaling.

🎯 Target Tracking Scaling:
You tell AWS: “Keep CPU at 50%”
It automatically adjusts the number of servers to keep that average.

⏰ 3. Predictive, Scheduled, and Dynamic Scaling
🔮 Predictive Scaling:
AWS uses machine learning to guess future traffic based on past patterns.
Example: It learns that traffic always increases at 10 AM, so it adds servers before that.

📅 Scheduled Scaling:
You tell AWS to scale at specific times.
Example: Add 2 servers every weekday at 8 AM and remove them at 6 PM.

📊 Dynamic Scaling:
Scaling based on real-time usage data, like CPU, memory, etc.
Adds/removes servers based on actual demand.

🧊 4. Warm Pool, Scale-In Protection, and Cool Down Period
🔥 Warm Pool:
These are standby servers that are already initialized but not running.
They start quickly when needed, saving launch time.

🛡️ Scale-In Protection:
Protects important servers from being accidentally shut down when scaling in (removing instances).
You can mark certain instances as “don’t remove these.”

⏱️ Cool Down Period:
A rest time after scaling action.
Prevents rapid scaling in/out too quickly.
Gives time for the instance to start and metrics to stabilize.

🔐 5. Important Ports

| Port     | Use                              |
| -------- | -------------------------------- |
| **22**   | SSH (connect to Linux servers)   |
| **3389** | RDP (connect to Windows servers) |
| **80**   | HTTP (normal website traffic)    |
| **443**  | HTTPS (secure website traffic)   |
