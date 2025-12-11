# 🟦 AWS Lab: Introduction to Amazon Linux AMI

## 📘 Overview
This lab introduces the Amazon Linux AMI, a secure and high‑performance Linux environment designed specifically for Amazon EC2.  
You will learn how to launch, access, and work with Amazon Linux while building foundational AWS and Linux skills.

---

## 🛠️ Lab Objectives
- Launch an EC2 instance  
- Connect using EC2 Instance Connect  
- Run basic Linux commands  
- Configure the AWS CLI  
- Understand how Amazon Linux is optimized for AWS environments  

---

## 🚀 Lab Steps

### 1. Launch an EC2 Instance
- Select Amazon Linux AMI  
- Choose an instance type (t2.micro recommended)  
- Configure VPC, subnet, and security group  
- Launch the instance  

### 2. Connect Using EC2 Instance Connect
- Use browser‑based SSH  
- No private key required  
- Ensure the instance is in a supported Availability Zone  

### 3. Run Linux Commands
- Navigation: `cd`, `ls`, `pwd`  
- File operations: `mkdir`, `cat`, `nano`, `less`  
- System info: `top`, `uname`, `df -h`  

### 4. Configure the AWS CLI
- Run `aws configure`  
- Enter Access Key, Secret Key, Region, Output Format  
- Test with `aws s3 ls`  

### 5. Explore Amazon Linux Features
- Fast boot times  
- AWS‑optimized kernel  
- Preinstalled AWS tools (CLI, CloudInit, SSM Agent)  
- Differences between Amazon Linux AMI and Amazon Linux 2  

---

## ✅ Takeaways
- Learned how to launch and manage EC2 instances  
- Understood how to securely connect to an Amazon Linux instance  
- Practiced Linux navigation and file management  
- Learned to configure and use the AWS CLI  
- Saw how Amazon Linux offers built‑in AWS optimizations  
- Understood the importance of choosing the right AMI  

---

## ⚠️ Challenges

### 1. Connecting to the EC2 Instance
- Connection failed due to incorrect methods or missing permissions  

### 2. AWS CLI Setup
- Errors occurred when credentials or regions were misconfigured  

### 3. Learning Linux Commands
- Commands like `cd`, `ls`, `mkdir`, and permissions required practice  

### 4. Understanding AMI Types
- Differentiating between Amazon Linux AMI, Amazon Linux 2, and other AMIs was initially confusing  

---

## 🧩 Solutions

### Fixed EC2 Connection Issues
- Used EC2 Instance Connect when no private key was available  
- Ensured the instance was running and in the correct Availability Zone  

### Solved AWS CLI Configuration Errors
- Ran `aws configure` with correct credentials  
- Ensured IAM user had required permissions  

### Improved Linux Skills
- Used cheat sheets and `man` pages  
- Practiced commands repeatedly  

### Understood AMI Differences
- Reviewed AWS documentation  
- Compared Amazon Linux vs Amazon Linux 2 for performance and compatibility  

---

## 📌 Summary
This lab provided hands‑on experience with Amazon Linux AMI, EC2 connectivity, Linux fundamentals, and AWS CLI configuration.  
It strengthened your understanding of AWS‑optimized operating systems and how to interact with them effectively.


<img width="940" height="592" alt="image" src="https://github.com/user-attachments/assets/a04976d7-e855-4726-ab57-7bb52d0f0094" />
<img width="940" height="577" alt="image" src="https://github.com/user-attachments/assets/aa6a16cb-cb8d-4f04-95d0-a3ce8c11f664" />
<img width="940" height="588" alt="image" src="https://github.com/user-attachments/assets/7960d7e2-d864-42ee-9a18-62e210b5c250" />
<img width="940" height="589" alt="image" src="https://github.com/user-attachments/assets/66a133e4-4fe8-4ebb-9f1e-d1f4d2bf7882" />
<img width="940" height="583" alt="image" src="https://github.com/user-attachments/assets/40b957fb-8796-431e-9dd5-ce3a0c55b194" />
<img width="940" height="501" alt="image" src="https://github.com/user-attachments/assets/be2881a9-7779-4cee-882a-69c78bd17474" />
<img width="940" height="501" alt="image" src="https://github.com/user-attachments/assets/158b98da-1c66-4b9b-8b71-f1d440816b80" />

