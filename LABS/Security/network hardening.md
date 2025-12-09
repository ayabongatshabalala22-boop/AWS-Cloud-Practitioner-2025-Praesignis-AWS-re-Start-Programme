1.	276-[SF]-Lab - Network-Hardening
2.	🔒 AWS Network Hardening Lab

A hands-on lab designed to teach you how to strengthen your AWS network against attacks.

This lab walks you through real AWS security practices such as securing VPCs, locking down traffic with Security Groups & NACLs, using AWS WAF & Shield, configuring VPC Flow Logs, and testing hardened network behavior.

🎯 Lab Objectives

By the end of this lab, you will be able to:

Implement Network Hardening in AWS

Lock down inbound & outbound access using Security Groups

Use Network ACLs to block malicious traffic

Configure AWS WAF to protect web applications

Enable VPC Flow Logs and analyze network traffic

Test hardened configurations using an EC2 “attacker” instance

Apply least-privilege networking best practices

🏗️ Lab Architecture Overview
                Internet
                    |
      ┌─────────────────────────────────┐
      │       AWS WAF + ALB (Public)    │
      └─────────────────────────────────┘
                    |
           Hardened Security Group
                    |
           Private EC2 Application
                    |
          Subnet + Strict NACL Rules
                    |
             VPC Flow Logs → CloudWatch

🛠️ Lab Steps
1️⃣ Create a VPC

Open VPC Console → Create VPC

Choose: VPC Only

CIDR: 10.0.0.0/16

Create two subnets:

Subnet	CIDR	Type
Public Subnet	10.0.1.0/24	Public
Private Subnet	10.0.2.0/24	Private

Attach Internet Gateway to VPC

Route public subnet → Internet Gateway

Keep private subnet isolated

2️⃣ Create Hardened Security Groups
Security Group: public-alb-sg

Inbound:

HTTP (80): 0.0.0.0/0

HTTPS (443): 0.0.0.0/0

Outbound:

Allow only necessary ports (80, 443)

Security Group: private-app-sg

Inbound:

Allow traffic only from public-alb-sg on port 80

Outbound:

Allow all (or restrict to DB, logging services, etc.)

This enforces layered network access.

3️⃣ Configure Network ACLs (NACLs)
Public Subnet NACL (controlled)

Inbound:

80, 443 → ALLOW from anywhere

All others → DENY

Outbound:

Ephemeral ports 1024–65535 → ALLOW

All others → DENY

Private Subnet NACL (very strict)

Inbound:

Allow ALB subnets → port 80 only

Deny all other traffic

Outbound:

Allow response traffic → ephemeral ports

Deny everything else

This blocks malicious port scans and unwanted east-west traffic.

4️⃣ Launch an Application EC2 (Private)

Launch EC2 into the private subnet

Assign private-app-sg

Install a sample web app:

sudo yum install httpd -y
sudo systemctl enable httpd
sudo systemctl start httpd
echo "Private App: Network Hardened" | sudo tee /var/www/html/index.html

5️⃣ Create an Application Load Balancer (Public)

Go to EC2 → Load Balancers

Create Application Load Balancer

Scheme: Internet-facing

Subnets: Public Subnet

Security Group: public-alb-sg

Target Group:

Target type: Instances

Add your private EC2 instance

ALB → SG → App EC2 Layer = Hardened access path

6️⃣ Enable AWS WAF for Layer 7 Protection

Go to AWS WAF Console → Create Web ACL

Associate with ALB

Add these rule groups:

AWS Managed Core Rule Set

Amazon Known Bad Inputs

IP Reputation List

Enable rate limiting (e.g., 2000 req/min)

AWS WAF helps block:

SQL injection

XSS

Known botnets

Bad request patterns

7️⃣ Enable VPC Flow Logs for Traffic Analysis

Go to VPC → Your VPC → Flow Logs

Create Flow Log

Destination: CloudWatch Logs

Filter: ALL

This lets you track:

Allowed/Denied traffic

Possible attacks

Unexpected outbound connections

8️⃣ Launch Attacker EC2 (Testing)

Launch a small EC2 instance in the public subnet
Assign it a separate Security Group.

SSH into attacker instance:

ssh -i mykey.pem ec2-user@<attacker-ip>

Try to scan the private subnet (should fail):
nmap 10.0.2.0/24


Expected:
❌ No response — NACL + SG block it.

Try to connect directly to private EC2:
curl http://10.0.2.x


Expected:
❌ Connection timed out.

Try going through ALB:
curl http://<ALB-DNS>


Expected:
✔ Works — only approved entry path allowed.

9️⃣ Analyze Logs for Denied Traffic

Go to CloudWatch Logs → Flow Logs group

Find logs with "REJECT"

Identify:

Port scans

Rejected inbound connections

Misconfigured services

🎓 Takeaways

Segmentation and layered network access are essential

Security Groups control traffic at instance level

NACLs control traffic at subnet level

ALB + WAF protects applications from external attacks

Flow Logs are critical for auditing denied traffic

Principle of Least Privilege makes attacks harder

Never expose private workloads directly to the internet

🧩 Challenges Faced
Challenge	Description
NACL order confusion	Rules evaluated in numeric order
ALB health check failures	SG or NACL blocking ALB traffic
Flow Logs not showing REJECT	Using the wrong VPC/subnet
WAF rules blocking valid traffic	Overly strict patterns
EC2 unreachable	Wrong SG referencing or subnet routes
🛠️ Solutions

✔ Use explicit ALLOW + DENY rules in NACLs
✔ Allow ALB health check IP ranges
✔ Ensure correct subnet/VPC selected for Flow Logs
✔ Start with AWS Managed Rules before adding custom ones
✔ Carefully map SG inbound/outbound dependencies
✔ Keep private subnets isolated (no IGW, no public IPs)
<img width="940" height="521" alt="image" src="https://github.com/user-attachments/assets/1ddf194c-882d-4e45-bd3a-881a68188f12" />
<img width="940" height="505" alt="image" src="https://github.com/user-attachments/assets/3b1d68d6-6d6e-477a-8b3a-9df166b663f7" />
<img width="940" height="510" alt="image" src="https://github.com/user-attachments/assets/f5f98e31-c050-47a7-aa1c-ecdb88dccb7e" />
<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/8d841198-92e4-44ee-a73f-ed351416f809" />
<img width="940" height="515" alt="image" src="https://github.com/user-attachments/assets/1ef72cdf-8ac3-465d-865b-e97abd4d148f" />
<img width="940" height="512" alt="image" src="https://github.com/user-attachments/assets/991ceafe-a72a-4eba-9fed-e37ec47b341c" />
<img width="940" height="556" alt="image" src="https://github.com/user-attachments/assets/2e9eebd5-0992-4e32-a61d-c65b03316ec6" />
<img width="940" height="335" alt="image" src="https://github.com/user-attachments/assets/6800831d-d51d-4d9a-8c69-885a6e2ac163" />
