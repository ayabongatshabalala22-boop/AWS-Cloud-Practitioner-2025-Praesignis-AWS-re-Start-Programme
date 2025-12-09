:

🟧 AWS Lab: Creating Subnets and Allocating IP Addresses in an Amazon VPC

This lab focuses on building core networking skills in AWS by creating subnets and understanding how IP addressing works inside an Amazon Virtual Private Cloud (VPC).
You will learn how IP ranges are assigned, how subnetting works, and how AWS allocates IP addresses within each subnet.

🎯 Lab Objectives

Create a custom VPC

Design and configure multiple subnets

Understand AWS-reserved IP addresses

Allocate and verify private IP addresses

Launch EC2 instances to observe IP allocation

🛠️ Lab Steps
1️⃣ Create a Custom VPC

Open the VPC Console

Select Create VPC

Choose VPC Only

Configure:

Name: MySubnetLabVPC

IPv4 CIDR block: 10.0.0.0/16

Click Create VPC

2️⃣ Create Subnets
🔹 Create a Public Subnet

Go to Subnets → Create Subnet

Select VPC: MySubnetLabVPC

Configure:

Name: PublicSubnet-A

AZ: us-east-1a

CIDR: 10.0.1.0/24

Create Subnet

🔹 Create a Private Subnet

Repeat using:

Name: PrivateSubnet-B

AZ: us-east-1b

CIDR: 10.0.2.0/24

3️⃣ AWS-Reserved IP Addresses

AWS automatically reserves 5 IP addresses in every subnet.
These cannot be assigned to EC2 instances.

For subnet 10.0.1.0/24, reserved IPs are:

IP Address	Purpose
10.0.1.0	Network address
10.0.1.1	VPC router
10.0.1.2	Amazon DNS
10.0.1.3	Reserved
10.0.1.255	Broadcast address

Usable IP range: 10.0.1.4 → 10.0.1.254

4️⃣ Allocate IP Addresses (Launch EC2 Instances)

Go to EC2 → Launch Instance

Choose Amazon Linux 2

Under Network Settings:

VPC: MySubnetLabVPC

Subnet: PublicSubnet-A

Auto-assign Public IP: Enabled

Under Network Interfaces, review:

Assigned private IPv4 address from subnet pool

Launch the instance

Optional

Launch another instance in PrivateSubnet-B to compare IP allocation.

5️⃣ Verify IP Allocation
In EC2 Console

Go to Instances → Details

Check Private IPv4 Address

From the terminal (if connected via SSH):
hostname -I


This displays the private IP your EC2 received.

📘 Takeaways

Learned how to design and allocate IP ranges for a VPC

Understood subnet creation across different AZs

Discovered how AWS automatically reserves 5 IPs per subnet

Observed how EC2 instances receive private IP addresses

Built a foundation for advanced VPC networking (NAT, IGWs, routing)

⚠️ Challenges Encountered
1️⃣ Overlapping CIDR Blocks

Invalid subnet creation due to overlapping or incorrect blocks.

2️⃣ Incorrect Availability Zones

Instances failed when AZs were mismatched.

3️⃣ Misunderstanding Reserved IPs

Users expected to use .0, .1, or .2 — which AWS blocks.

4️⃣ Missing IP Allocation

Instances launched without IPs when “Auto-assign Public IP” was off.

🧩 Solutions
✔ Proper CIDR Planning

Ensured subnet CIDRs fit inside the VPC

Used non-overlapping ranges

✔ Verified Availability Zones

Checked available AZs before subnet creation

✔ Clarified Reserved IP Rules

Only used IPs 10.0.1.4 → 10.0.1.254 for EC2

✔ Ensured IP Assignment

Enabled Auto-assign Public IP

Verified DHCP settings in VPC
<img width="975" height="109" alt="image" src="https://github.com/user-attachments/assets/34c31a26-5d45-4653-9e6f-77b2fe5797f2" />
<img width="975" height="230" alt="image" src="https://github.com/user-attachments/assets/02902410-c693-4df8-914d-eb6292ddede7" />
<img width="975" height="253" alt="image" src="https://github.com/user-attachments/assets/c20464c6-c933-4b6b-814e-dca29efac598" />
<img width="975" height="398" alt="image" src="https://github.com/user-attachments/assets/0a352b23-c51f-48d6-a597-01308d418fc6" />
<img width="975" height="113" alt="image" src="https://github.com/user-attachments/assets/2c439e62-b0f7-4630-96a2-adbde8c389bf" />
<img width="975" height="356" alt="image" src="https://github.com/user-attachments/assets/cc71d97f-6284-479f-be3f-31cf5c7e4990" />

