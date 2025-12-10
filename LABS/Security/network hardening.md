1.	276-[SF]-Lab - Network-Hardening
## 2. 🔒 AWS Network Hardening Lab

A hands-on lab designed to teach you how to strengthen your AWS network against attacks.  

This lab walks you through real AWS security practices, including:

- Securing **VPCs**  
- Locking down traffic with **Security Groups** & **NACLs**  
- Using **AWS WAF** & **Shield**  
- Configuring **VPC Flow Logs**  
- Testing hardened network behavior  

## 🎯 Lab Objectives

By the end of this lab, you will be able to:

- Implement **Network Hardening** in AWS  
- Lock down inbound & outbound access using **Security Groups**  
- Use **Network ACLs** to block malicious traffic  
- Configure **AWS WAF** to protect web applications  
- Enable **VPC Flow Logs** and analyze network traffic  
- Test hardened configurations using an **EC2 “attacker” instance**  
- Apply **least-privilege networking best practices**  

## 🛠️ Lab Steps

1️⃣ **Create a VPC**  
- Open VPC Console → Create VPC  
- Choose **VPC Only**  
- CIDR: `10.0.0.0/16`  
- Create public and private subnets  

---

2️⃣ **Create Hardened Security Groups**  
- Public ALB SG → Allow HTTP/HTTPS inbound, restrict outbound  
- Private App SG → Allow inbound only from ALB SG, restrict outbound  

---

3️⃣ **Configure Network ACLs (NACLs)**  
- Public Subnet NACL → Allow 80/443 inbound, ephemeral outbound  
- Private Subnet NACL → Allow ALB traffic only, deny all else  

---

4️⃣ **Launch an Application EC2 (Private)**  
- Deploy EC2 in private subnet  
- Attach private SG  
- Install and run sample web app  

---

5️⃣ **Create an Application Load Balancer (Public)**  
- Internet-facing ALB in public subnet  
- Attach public SG  
- Target group → Private EC2 instance  

---

6️⃣ **Enable AWS WAF for Layer 7 Protection**  
- Create Web ACL  
- Associate with ALB  
- Add AWS Managed Rules + IP reputation lists  
- Configure rate limiting  

---

7️⃣ **Enable VPC Flow Logs for Traffic Analysis**  
- Create Flow Logs for VPC  
- Send logs to CloudWatch  
- Capture ALL traffic


<img width="940" height="521" alt="image" src="https://github.com/user-attachments/assets/1ddf194c-882d-4e45-bd3a-881a68188f12" />
<img width="940" height="505" alt="image" src="https://github.com/user-attachments/assets/3b1d68d6-6d6e-477a-8b3a-9df166b663f7" />
<img width="940" height="510" alt="image" src="https://github.com/user-attachments/assets/f5f98e31-c050-47a7-aa1c-ecdb88dccb7e" />
<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/8d841198-92e4-44ee-a73f-ed351416f809" />
<img width="940" height="515" alt="image" src="https://github.com/user-attachments/assets/1ef72cdf-8ac3-465d-865b-e97abd4d148f" />
<img width="940" height="512" alt="image" src="https://github.com/user-attachments/assets/991ceafe-a72a-4eba-9fed-e37ec47b341c" />
<img width="940" height="556" alt="image" src="https://github.com/user-attachments/assets/2e9eebd5-0992-4e32-a61d-c65b03316ec6" />
<img width="940" height="335" alt="image" src="https://github.com/user-attachments/assets/6800831d-d51d-4d9a-8c69-885a6e2ac163" />
## 🎓 Takeaways

- Segmentation and **layered network access** are essential  
- **Security Groups** control traffic at the instance level  
- **NACLs** control traffic at the subnet level  
- **ALB + WAF** protect applications from external attacks  
- **Flow Logs** are critical for auditing denied traffic  
- The **Principle of Least Privilege** makes attacks harder  
- Never expose **private workloads** directly to the internet  

## 🧩 Challenges Faced

- **NACL order confusion** → Rules are evaluated in numeric order  
- **ALB health check failures** → Security Group or NACL blocking ALB traffic  
- **Flow Logs not showing REJECT** → Using the wrong VPC or subnet  
- **WAF rules blocking valid traffic** → Overly strict patterns applied  
- **EC2 unreachable** → Wrong Security Group referencing or subnet routes  

## 🛠️ Solutions

- Use explicit **ALLOW + DENY** rules in NACLs  
- Allow **ALB health check IP ranges**  
- Ensure correct **subnet/VPC** selected for Flow Logs  
- Start with **AWS Managed Rules** before adding custom ones  
- Carefully map **Security Group inbound/outbound dependencies**  
- Keep **private subnets isolated** (no Internet Gateway, no public IPs)  
