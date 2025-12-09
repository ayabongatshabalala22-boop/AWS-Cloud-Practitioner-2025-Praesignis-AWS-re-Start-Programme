🟦 AWS Lab: Understanding Public and Private IP Addresses in Amazon VPC

This lab teaches the fundamentals of public vs. private IP addresses in AWS by launching EC2 instances, analyzing their IP allocations, and understanding how AWS handles IP addressing inside a Virtual Private Cloud (VPC).

You will learn how devices communicate within a private network and how instances connect to the internet using public IPs.

🎯 Lab Objectives

By the end of this lab, you will:

Understand the difference between public and private IP addresses

Launch EC2 instances with private-only and public IPs

Observe how AWS auto-assigns IPs to instances

Test connectivity between instances

Understand how public IPs enable internet access

Identify AWS IP behavior (Elastic IPs, DNS, reserved addresses)

🛠️ Lab Steps
1️⃣ Create a Custom VPC

Navigate to VPC Console → Create VPC

Select VPC Only

Configure:

Name: IPLabVPC

IPv4 CIDR: 10.0.0.0/16

Create the VPC

2️⃣ Create Two Subnets (Public & Private)
🔹 Public Subnet

Name: PublicSubnet

CIDR: 10.0.1.0/24

AZ: choose any (e.g., us-east-1a)

🔹 Private Subnet

Name: PrivateSubnet

CIDR: 10.0.2.0/24

AZ: us-east-1a

Create both subnets.

3️⃣ Create and Attach an Internet Gateway (IGW)

Go to Internet Gateways → Create IGW

Name: IPLabIGW

Create & Attach to IPLabVPC

4️⃣ Configure Route Tables
🔹 Public Route Table

Create route table named PublicRT in your VPC

Add route:

Destination: 0.0.0.0/0

Target: Internet Gateway

Associate with PublicSubnet

✔ This subnet now supports public IPs.

🔹 Private Route Table

Create route table named PrivateRT

Do not add an IGW route

Associate with PrivateSubnet

✔ This subnet will NOT have internet access.

5️⃣ Launch EC2 Instances
🔹 Instance 1: Public Instance

Launch an instance in:

VPC: IPLabVPC

Subnet: PublicSubnet

Enable Auto-assign Public IP: Yes

Name the instance: PublicInstance

Launch

You will see:

A public IP (e.g., 44.202.x.x)

A private IP (e.g., 10.0.1.4)

🔹 Instance 2: Private-Only Instance

Launch another instance in:

Subnet: PrivateSubnet

Set Auto-assign Public IP: Disabled

Name the instance: PrivateInstance

Launch

You will see:

No public IP

Only a private IP (e.g., 10.0.2.5)

🔍 6️⃣ Verify IP Behavior
A. Public Instance

Connect using SSH:

ping google.com


✔ Should work — it has a public IP.

B. Private Instance

You cannot SSH directly (no public IP).
To test connectivity:

SSH into PublicInstance

From there, SSH into PrivateInstance, using its private IP:

ssh ec2-user@10.0.2.5


✔ Works because both are in the same VPC.

C. Test Internet Access From Private Instance

Inside PrivateInstance, run:

ping google.com


❌ Should fail — no public IP or NAT access

📘 Takeaways

🌐 Public IPs allow internet communication

🔐 Private IPs allow internal communication only

🔁 Instances can reach each other inside a VPC using private IPs

🛰️ Public IPs change on restart unless you use an Elastic IP

📌 AWS reserves 5 IPs in every subnet

🔄 Public and private IPs are dynamically assigned by AWS DHCP

⚠️ Challenges Encountered
1️⃣ Instance Had No Internet Access

Occurred when placed in a private subnet

No IGW route

No public IP assigned

2️⃣ Could Not SSH Into Private Instance

No public IP

Only reachable from inside the VPC

3️⃣ Incorrect Route Table Assignments

Wrong associations caused connectivity failures

🧩 Solutions
✔ Added Public Routes

Public subnet received IGW route (0.0.0.0/0 → IGW)

✔ Used Public Instance as a Jump Host

Used public EC2 to access private EC2 internally

✔ Reattached Subnets to Correct Route Tables

Ensured traffic flowed through the intended network paths
<img width="975" height="548" alt="image" src="https://github.com/user-attachments/assets/cd4de9bb-6b0c-47d2-b48e-3cdb87f8c598" />
<img width="975" height="548" alt="image" src="https://github.com/user-attachments/assets/d9a9fc4c-ce33-4a78-949b-e241f2fe5dd1" />
<img width="975" height="548" alt="image" src="https://github.com/user-attachments/assets/83594e94-dee1-4938-9ada-1e795fa58a80" />
<img width="975" height="548" alt="image" src="https://github.com/user-attachments/assets/e23c870f-de6b-463f-93a0-943864f823c0" />
<img width="975" height="548" alt="image" src="https://github.com/user-attachments/assets/d9c7f375-1ad9-4b0d-bede-46ff12f6eeef" />

