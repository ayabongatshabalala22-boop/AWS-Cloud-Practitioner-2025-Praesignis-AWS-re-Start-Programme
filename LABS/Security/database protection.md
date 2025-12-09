🛡️ AWS Database Protection Lab

A hands-on lab to practice securing databases in AWS.

This lab teaches you how to secure Amazon RDS by applying IAM, security groups, encryption, and backups. You will work with real AWS security features to protect your data.

🎯 Lab Objectives

By the end of this lab, you will:

Understand how database security works in AWS

Configure Security Groups to restrict access

Create an IAM policy & role for database access

Enable Encryption at Rest (KMS)

Configure Automatic Backups & Snapshots

Enable Multi-AZ for high availability

Test secure and insecure access

🏗️ Lab Architecture Overview

You will build:

Your Laptop → Bastion Host (EC2) → RDS Database  
               ↑
         Secure SG Rules


Security features:

IAM Role for DB access

Security Groups

KMS Encryption

Backups & Snapshots

Multi-AZ protection

🛠️ Lab Steps
1️⃣ Create a VPC (Optional if you already have one)

Create a new VPC (10.0.0.0/16)

Create 2 subnets:

Public subnet (10.0.1.0/24)

Private subnet (10.0.2.0/24)

Attach an Internet Gateway

Create Route Table:

Public subnets → Internet

Private subnets → Local only

2️⃣ Launch an RDS Database (MySQL / PostgreSQL)

Go to RDS Console → Create database

Choose Standard Create

Engine: MySQL or PostgreSQL

Templates: Free-tier

Select:

DB instance identifier: protected-db

Username: admin

Password: (your password)

Connectivity

VPC: your VPC

Subnets: private subnets

Public Access: NO ❌

Security Group

Create a new SG named: rds-private-sg

No inbound rules yet

Storage

Enable Storage Auto Scaling

Encryption

Enable KMS Encryption

Key: aws/rds or your custom KMS key

Availability

Enable Multi-AZ deployment

Click Create Database.

3️⃣ Create a Security Group for Access
EC2 Security Group (Bastion Host)

Go to EC2 → Security Groups

Create SG: bastion-sg

Inbound:

SSH (22) → your IP only

Outbound:

Allow all (default)

RDS Security Group Rules

Edit rds-private-sg:

Allow MySQL/Aurora (3306)

Source: bastion-sg

This means:

✔ Only the bastion host can talk to RDS
✔ No one else from the internet can connect

4️⃣ Create a Bastion Host (EC2)

Launch EC2 → Amazon Linux 2

Subnet: Public

SG: bastion-sg

Key pair for SSH

Connect from your terminal:

ssh -i mykey.pem ec2-user@<EC2-Public-IP>

5️⃣ Connect to RDS Securely

Install DB client:

For MySQL
sudo yum install mariadb -y


Connect:

mysql -h <rds-endpoint> -u admin -p


If connection works → Your security setup is correct.

If connection fails → Security Group or subnet issue.

6️⃣ Test Protection Features
🔐 Encryption Test

Run this in the RDS console:

Create a manual snapshot

Download snapshot metadata

Verify "Encrypted: Yes"

🔁 Backup & Restore Test

Modify DB → Set backup retention: 7 days

Create a manual snapshot

Restore snapshot into new DB instance

🌐 Firewall Test

Try to connect to RDS from your local machine:

mysql -h <rds-endpoint> -u admin -p


Expected result:
❌ Connection timed out (Correct! It's private)

🧪 IAM Authentication Test (Optional)

Enable IAM authentication on RDS

Create IAM Policy:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "rds-db:*",
      "Resource": "*"
    }
  ]
}


Attach role to EC2

Connect using IAM token instead of password

🎓 Takeaways

Databases must run in a private subnet, not public

Network access is controlled by Security Groups

KMS encryption protects data at rest

Backups & Snapshots protect against corruption

Multi-AZ ensures high availability

IAM can remove the need for database passwords

Bastion hosts provide secure, isolated access to private systems

🧩 Challenges Faced
Challenge	Explanation
RDS not accessible	Security Groups or subnet blocking
IAM authentication confusion	Requires token-based login
Misconfigured subnets	DB placed in public subnet by accident
KMS errors	Using wrong key or missing permissions
EC2 can't reach RDS	Wrong SG inbound source
🛠️ Solutions

✔ Double-check routing tables & subnet types
✔ Only allow access from the bastion SG
✔ Give EC2 role permission to use KMS key
✔ Ensure DB runs in private subnet
✔ Use AWS docs for IAM-token DB login
<img width="902" height="528" alt="image" src="https://github.com/user-attachments/assets/004676f8-b6b5-4556-89bf-9196f2219cdd" />
<img width="940" height="485" alt="image" src="https://github.com/user-attachments/assets/d4eb124e-2fb3-4930-91e4-2232016a2308" />
<img width="940" height="487" alt="image" src="https://github.com/user-attachments/assets/e73c95fc-1fa7-400d-a42d-47cd349052e4" />
<img width="877" height="464" alt="image" src="https://github.com/user-attachments/assets/d56ef003-5c52-4bed-ac1f-616c17ea669d" />
<img width="628" height="512" alt="image" src="https://github.com/user-attachments/assets/9b05c502-2cf7-4ffc-a2e6-9a6d4d84b778" />
<img width="632" height="524" alt="image" src="https://github.com/user-attachments/assets/e5134006-9cbc-4788-81c2-7b1de3411fe5" />
<img width="618" height="528" alt="image" src="https://github.com/user-attachments/assets/1b7235b0-031d-4c77-bc17-4cf84dbb2061" />
<img width="616" height="524" alt="image" src="https://github.com/user-attachments/assets/ea0dfc7b-ca61-47e5-a2b1-104c6ddf75c4" />
<img width="623" height="538" alt="image" src="https://github.com/user-attachments/assets/3dc14b39-edf5-410e-a926-b9e6a3041b1d" />
<img width="611" height="526" alt="image" src="https://github.com/user-attachments/assets/dae3448c-7bc3-4e1b-b667-846b883731f1" />
<img width="621" height="478" alt="image" src="https://github.com/user-attachments/assets/01235009-c2ee-49fe-bda9-5b9bacc85ed2" />
<img width="623" height="521" alt="image" src="https://github.com/user-attachments/assets/1fe37310-6302-4f39-87d3-f9a8da41cab7" />
<img width="611" height="401" alt="image" src="https://github.com/user-attachments/assets/35a7a384-b790-40dd-83d6-b6285eadf038" />
<img width="940" height="526" alt="image" src="https://github.com/user-attachments/assets/1c6ba7b2-c0fe-4782-a2d1-f8b21b285b1a" />
<img width="940" height="496" alt="image" src="https://github.com/user-attachments/assets/467cb8a9-9603-438f-97e6-16874517bb9a" />
