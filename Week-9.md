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


