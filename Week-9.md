🔶 1. Public IP, Private IP, IPv4 & IPv6
📌 Public IP
Assigned by AWS (automatically or manually).

Used when you want your EC2 instance to communicate with the internet.

Associated with Elastic IP if you want a persistent public IP.

📌 Private IP
Used for internal communication between instances within the same VPC.

Not routable from the internet.

Each instance gets a private IP from the subnet’s CIDR block.

📌 IPv4
Format: 192.168.1.1 (32-bit).

AWS allows CIDR block allocation like 10.0.0.0/16.

📌 IPv6
Format: 2001:0db8:85a3:0000:0000:8a2e:0370:7334 (128-bit).

Not enabled by default in VPC.

Supports massive scale and internet-ready communication.

🔶 2. VPC, CIDR, Subnets
📌 VPC (Virtual Private Cloud)
Your own isolated network in AWS cloud.

You can control IP ranges, subnets, route tables, gateways, etc.

Can span across multiple Availability Zones (AZs).

📌 CIDR Block
Defines IP range of the VPC.

Example: 10.0.0.0/16 → gives 65,536 IP addresses.

Each subnet is a subset of the VPC’s CIDR block.

📌 Subnets
Segments of the VPC.

You typically create:

Public Subnets → connect to the internet.

Private Subnets → no direct internet access.

Each subnet must be in one Availability Zone only.

🔶 3. NACL, Security Groups
📌 Network Access Control List (NACL)
Stateless firewall: Rules must be defined for both inbound and outbound traffic.

Applied at subnet level.

Useful for controlling traffic at a broader level (e.g., allow only certain IP ranges).

Example Rule: Allow port 80 inbound from 0.0.0.0/0.

📌 Security Groups
Stateful firewall: If inbound is allowed, outbound is automatically allowed.

Applied to EC2 instances (not subnets).

Acts like a virtual firewall for your instance.

Example: Allow SSH (port 22) from your IP only.

🔶 4. NAT Gateway, Internet Gateway, Route Tables
📌 Internet Gateway (IGW)
A component that allows instances in your VPC to access the internet.

Must be attached to the VPC.

Route table must have a route like:

0.0.0.0/0 → IGW (for public subnet)

📌 NAT Gateway
Allows instances in private subnets to access the internet (e.g., for software updates).

Blocks inbound traffic initiated from the internet.

Needs a public subnet and Elastic IP.

📌 Route Tables
Defines how traffic is routed in your VPC.

Each subnet is associated with one route table.

Example entries:

Local → for internal VPC traffic.

0.0.0.0/0 → IGW (for public subnets)

0.0.0.0/0 → NAT Gateway (for private subnets)

✅ Summary Diagram (Textual)
pgsql
Copy
Edit
                +-------------------------+
                |       Internet          |
                +-----------+-------------+
                            |
                      [Internet Gateway]
                            |
      +---------------------+----------------------+
      |                                            |
Public Subnet (with IGW)                  Private Subnet (with NAT)
  - Web Servers                            - App DB, Backends
  - Public IP                              - No direct internet access
  - Route: 0.0.0.0/0 → IGW                 - Route: 0.0.0.0/0 → NAT GW

             [ VPC CIDR: 10.0.0.0/16 ]

