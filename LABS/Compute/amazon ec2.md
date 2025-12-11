# 🟦 AWS EC2 Lab: Launching and Managing Virtual Servers

## 📘 Overview
This lab introduces Amazon EC2 (Elastic Compute Cloud), a core AWS service that provides scalable virtual servers in the cloud.  
You will learn how to launch an EC2 instance, connect to it, manage security groups, explore instance metadata, and stop/terminate instances safely.

This lab builds foundational cloud computing and Linux administration skills.

---

## 🛠️ Lab Objectives
- Launch an EC2 instance  
- Configure networking and security groups  
- Connect using EC2 Instance Connect or SSH  
- Explore EC2 instance metadata  
- Manage instance lifecycle (start, stop, reboot, terminate)  
- Understand public vs private IP behavior  

---

## 🚀 Lab Steps

### 1. Choose an Amazon Machine Image (AMI)
- Open **EC2 Console → Launch Instance**  
- Select an AMI such as:  
  - Amazon Linux 2  
  - Ubuntu Server  
  - Amazon Linux 2023  
- AMI determines OS, kernel, and preinstalled tools  

### 2. Select an Instance Type
- Choose a free‑tier eligible type:  
  - `t2.micro` or `t3.micro`  
- Instance type defines CPU, memory, and network performance  

### 3. Configure Instance Settings
- Name the instance (e.g., `EC2LabInstance`)  
- Select a VPC and subnet  
- Enable **Auto‑assign Public IP** for internet access  
- Keep default storage unless otherwise required  

### 4. Configure Security Group
Create a new security group:
- Allow **SSH (port 22)** from your IP  
- Allow additional ports only if needed  
- Security groups act as virtual firewalls  

### 5. Launch the Instance
- Review settings  
- Launch the instance  
- Wait for the instance state to become **Running**  

### 6. Connect to the Instance
#### Using EC2 Instance Connect
- Select instance → Connect → EC2 Instance Connect  
- Opens a browser‑based terminal  

#### Using SSH (if key pair was created)
```bash
ssh -i mykey.pem ec2-user@<public-ip>

## LAB SCREENSHOTS 


## ✅ Takeaways
- Learned how to launch and configure an EC2 instance  
- Understood the role of AMIs, instance types, and storage  
- Practiced connecting using EC2 Instance Connect and SSH  
- Gained experience managing security groups and inbound rules  
- Explored EC2 instance metadata for system details  
- Observed how public and private IPs behave during stop/start cycles  
- Learned how to safely stop, reboot, and terminate instances  
<img width="940" height="475" alt="image" src="https://github.com/user-attachments/assets/cfd5902a-3a52-4457-acb5-eefb6eb85b3e" />
<img width="940" height="450" alt="image" src="https://github.com/user-attachments/assets/7f58970c-b954-4f63-82c2-4b94ca9dfd5c" />
<img width="940" height="455" alt="image" src="https://github.com/user-attachments/assets/7617eb1e-53f2-48b4-9a06-b4e44ac520ec" />
<img width="940" height="475" alt="image" src="https://github.com/user-attachments/assets/7a93c84c-3358-4e4b-8bd1-27dd630e3b37" />
<img width="940" height="453" alt="image" src="https://github.com/user-attachments/assets/d68cbfaa-95b0-42b3-b988-2f0051f3a98f" />
<img width="940" height="463" alt="image" src="https://github.com/user-attachments/assets/b282fbf6-9090-49af-96a7-5acdbe9e4b10" />
<img width="940" height="431" alt="image" src="https://github.com/user-attachments/assets/d8184388-a2bc-404a-bdbf-3264bd38c24b" />
<img width="940" height="75" alt="image" src="https://github.com/user-attachments/assets/a0e8a0aa-9390-44a0-9f4b-f2f04c2dddcb" />
---

## ⚠️ Challenges
- SSH blocked by incorrect security group rules  
- Wrong AMI username used  
- EC2 Instance Connect not supported in selected AZ  
- Public IP not assigned  
- Instance launched in a private subnet  
- Incorrect key pair permissions  
- Wrong key pair selected  
- Public IP changed after stop/start  
- Root volume deleted on termination  

---

## 🧩 Solutions
- Allow SSH (port 22) from correct IP  
- Use correct AMI username  
- Use EC2 Instance Connect when supported  
- Enable Auto‑assign Public IP  
- Launch instance in a public subnet  
- Fix key permissions with `chmod 400`  
- Ensure correct key pair is chosen  
- Use Elastic IP for static public address  
- Review EBS settings before termination  
