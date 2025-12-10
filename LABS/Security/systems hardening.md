1.	277-[SF]-Lab - Systems-Hardening
## 2. 🔒 AWS Systems Hardening Lab

This lab teaches you how to harden AWS systems, specifically **EC2 instances**, to reduce attack surfaces, enforce best security practices, and follow compliance standards.  

You will practice **patch management**, **user hardening**, **logging and monitoring**, as well as configuring **secure services**.

---

## 🎯 Lab Objectives

By the end of this lab, you will be able to:

- Apply **OS-level hardening** on EC2 instances  
- Configure **SSH security** and **IAM roles**  
- Apply **automatic updates and patches**  
- Enable **logging and monitoring**  
- Restrict **network access and services**  
- Enforce **least-privilege access policies**  
- Test **hardened system behavior**  



## 🛠️ Lab Steps

1️⃣ Launch a Hardened EC2 Instance  
2️⃣ Enable IAM Role for EC2  
3️⃣ Update and Patch the OS  
4️⃣ Configure SSH Hardening  
5️⃣ Remove Unnecessary Services  
6️⃣ Enable Logging & Monitoring  
7️⃣ Configure System Auditing  
8️⃣ Enable Disk Encryption  
9️⃣ Test Hardened System  




<img width="940" height="508" alt="image" src="https://github.com/user-attachments/assets/388d4c0e-07c7-4cf5-a814-fbf2c588d117" />
<img width="940" height="496" alt="image" src="https://github.com/user-attachments/assets/c2ef4ea5-15f7-49e6-9071-b1b675ab88f1" />
<img width="940" height="475" alt="image" src="https://github.com/user-attachments/assets/1fde3b94-ae4d-4fa5-9532-a5db171f67db" />
<img width="940" height="473" alt="image" src="https://github.com/user-attachments/assets/37b5d71a-9ddf-4ac1-aec3-53556c107762" />
<img width="940" height="468" alt="image" src="https://github.com/user-attachments/assets/90c1b43c-9757-4771-a3be-f32dc334c1cd" />
<img width="940" height="482" alt="image" src="https://github.com/user-attachments/assets/c2bf2c5d-8d8c-4843-a272-3c29f9f128ff" />
<img width="940" height="480" alt="image" src="https://github.com/user-attachments/assets/15be783f-a662-4921-bdce-ab2efbbea4d0" />
<img width="940" height="524" alt="image" src="https://github.com/user-attachments/assets/a4a217ea-60a5-489f-ba3a-e6510e8842fe" />
<img width="940" height="494" alt="image" src="https://github.com/user-attachments/assets/dc3a38bd-ec23-4a50-a2a3-7d13f370720e" />
<img width="940" height="521" alt="image" src="https://github.com/user-attachments/assets/49e1005a-965a-441a-9989-a22637e930d6" />
<img width="940" height="491" alt="image" src="https://github.com/user-attachments/assets/92621bda-3f24-4c01-837b-ebdd0cd6bd7d" />
<img width="940" height="471" alt="image" src="https://github.com/user-attachments/assets/22e9534f-1060-462a-9003-e255404e69f2" />
<img width="940" height="360" alt="image" src="https://github.com/user-attachments/assets/3354cda6-ce42-416d-8396-00b023c1ad01" />
<img width="940" height="457" alt="image" src="https://github.com/user-attachments/assets/c617d41b-4acb-4376-aa3e-2edaaae511ea" />
<img width="940" height="452" alt="image" src="https://github.com/user-attachments/assets/b052b531-1021-4125-b230-4eee757ac11c" />
<img width="940" height="450" alt="image" src="https://github.com/user-attachments/assets/31730151-0ad0-4b58-b54f-1567b89a1d18" />
<img width="940" height="473" alt="image" src="https://github.com/user-attachments/assets/f615a9d3-0f0f-4a1e-b633-3d9bcbf2783c" />
<img width="940" height="491" alt="image" src="https://github.com/user-attachments/assets/8862cb1e-8620-4be7-9703-107165485ee2" />
<img width="940" height="431" alt="image" src="https://github.com/user-attachments/assets/7de1c7c8-a6cf-46fa-9448-38b75ff6eab3" />
<img width="940" height="494" alt="image" src="https://github.com/user-attachments/assets/f9781c21-8f1f-44ec-bfbb-d998649c5330" />
## 🎓 Takeaways
- **OS-level hardening** reduces attack surfaces  
- Only allow **SSH from trusted IPs**  
- **IAM roles** prevent hard‑coded credentials  
- **Automatic updates** keep systems patched  
- **Logging & monitoring** detect suspicious activity  
- **Audit and encryption** improve compliance and security  

---

## 🧩 Challenges Encountered

| Challenge                     | Explanation                                      |
|-------------------------------|--------------------------------------------------|
| SSH blocked after hardening   | Firewall or SSH config misconfigured             |
| Automatic updates not enabled | `yum-cron` or `unattended-upgrades` not installed |
| Logs not appearing in CloudWatch | CloudWatch Agent misconfigured                 |
| Service breakage              | Disabled essential service by mistake            |

---

## 🛠️ Solutions
- Always **backup SSH config** before making changes  
- Test **firewall changes** in a separate session  
- Verify **CloudWatch Agent** configuration  
- Review services carefully before disabling  
