# 🌐 AWS Lab: Understanding Public and Private IP Addresses in Amazon VPC

This lab teaches the fundamentals of public vs. private IP addresses in AWS by launching EC2 instances, analyzing their IP allocations, and understanding how AWS handles IP addressing inside a Virtual Private Cloud (VPC).

You will learn how devices communicate within a private network and how instances connect to the internet using public IPs.

---

## 🎯 Lab Objectives

By the end of this lab, you will:

- Understand the difference between public and private IP addresses  
- Launch EC2 instances with private‑only and public IPs  
- Observe how AWS auto‑assigns IPs to instances  
- Test connectivity between instances  
- Understand how public IPs enable internet access  
- Identify AWS IP behavior (Elastic IPs, DNS, reserved addresses)  

## 🛠️ Lab Steps
1. Create VPC (IPLabVPC, 10.0.0.0/16)  
2. Create PublicSubnet (10.0.1.0/24) and PrivateSubnet (10.0.2.0/24)  
3. Create and attach IGW (IPLabIGW)  
4. Configure PublicRT (0.0.0.0/0 → IGW) and PrivateRT (no IGW)  
5. Launch PublicInstance (public IP on) and PrivateInstance (public IP off)  
6. Verify: PublicInstance has internet; PrivateInstance reachable only internally and no internet  



<img width="975" height="548" alt="image" src="https://github.com/user-attachments/assets/cd4de9bb-6b0c-47d2-b48e-3cdb87f8c598" />
<img width="975" height="548" alt="image" src="https://github.com/user-attachments/assets/d9a9fc4c-ce33-4a78-949b-e241f2fe5dd1" />
<img width="975" height="548" alt="image" src="https://github.com/user-attachments/assets/83594e94-dee1-4938-9ada-1e795fa58a80" />
<img width="975" height="548" alt="image" src="https://github.com/user-attachments/assets/e23c870f-de6b-463f-93a0-943864f823c0" />
<img width="975" height="548" alt="image" src="https://github.com/user-attachments/assets/d9c7f375-1ad9-4b0d-bede-46ff12f6eeef" />
## Takeaways

- Public IPs allow internet communication  
- Private IPs allow internal communication only  
- Instances can reach each other inside a VPC using private IPs  
- Public IPs change on restart unless you use an Elastic IP  
- AWS reserves 5 IPs in every subnet  
- Public and private IPs are dynamically assigned by AWS DHCP  HCP

## Challenges Encountered

1. Instance Had No Internet Access  
   - Occurred when placed in a private subnet  
   - No IGW route  
   - No public IP assigned  

2. Could Not SSH Into Private Instance  
   - No public IP  
   - Only reachable from inside the VPC  

3. Incorrect Route Table Assignments  
   - Wrong associations caused connectivity failures  

## Solutions

- Added public routes  
  - Public subnet received IGW route (0.0.0.0/0 → IGW)

- Used public instance as a jump host  
  - Accessed the private EC2 instance internally through the public EC2 instance

- Reattached subnets to correct route tables  
  - Ensured traffic flowed through the intended network paths
