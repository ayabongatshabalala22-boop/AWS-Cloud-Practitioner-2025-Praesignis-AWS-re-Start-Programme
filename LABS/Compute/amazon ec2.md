#  AWS EC2 Lab: Launching and Managing Virtual Servers

##  Overview
This lab introduces Amazon EC2 (Elastic Compute Cloud), a core AWS service that provides scalable virtual servers in the cloud.  
You will learn how to launch an EC2 instance, connect to it, manage security groups, explore instance metadata, and stop/terminate instances safely.

This lab builds foundational cloud computing and Linux administration skills.

---

##  Lab Objectives
- Launch an EC2 instance  
- Configure networking and security groups  
- Connect using EC2 Instance Connect or SSH  
- Explore EC2 instance metadata  
- Manage instance lifecycle (start, stop, reboot, terminate)  
- Understand public vs private IP behavior  

---

## Lab Steps

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

---

##  Takeaways

- Learned how to launch and configure an **EC2 instance**  
- Understood the role of **AMIs, instance types, and storage**  
- Practiced connecting using **EC2 Instance Connect** and **SSH**  
- Gained experience managing **security groups** and inbound rules  
- Explored **EC2 instance metadata** for system details  
- Observed how **public and private IPs** behave during stop/start cycles  
- Learned how to safely **stop, reboot, and terminate** instances  

---


##  Challenges
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

## Solutions
- Allow SSH (port 22) from correct IP  
- Use correct AMI username  
- Use EC2 Instance Connect when supported  
- Enable Auto‑assign Public IP  
- Launch instance in a public subnet  
- Fix key permissions with `chmod 400`  
- Ensure correct key pair is chosen  
- Use Elastic IP for static public address  
- Review EBS settings before termination



<img width="1088" height="704" alt="image" src="https://github.com/user-attachments/assets/08e3ab91-7612-4f76-8400-d994f8a2d07b" />
<img width="1099" height="227" alt="image" src="https://github.com/user-attachments/assets/cf58e130-20d8-41c6-b28c-f87325a83690" />
<img width="1083" height="584" alt="image" src="https://github.com/user-attachments/assets/89f884df-3da5-464e-8d7c-a837088a191a" />
<img width="1091" height="315" alt="image" src="https://github.com/user-attachments/assets/956d8e89-b8f7-4bd1-917b-b5bedc6b4045" />
<img width="1068" height="505" alt="image" src="https://github.com/user-attachments/assets/e9737240-f7ac-49ab-9e32-ab743aef4dca" />





