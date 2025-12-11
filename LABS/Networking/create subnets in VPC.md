# 🌐 AWS Lab: Creating Subnets and Allocating IP Addresses in an Amazon VPC

This lab focuses on building core networking skills in AWS by creating subnets and understanding how IP addressing works inside an Amazon Virtual Private Cloud (VPC).  
You will learn how IP ranges are assigned, how subnetting works, and how AWS allocates IP addresses within each subnet.

---

## ✅ Lab Objectives

- Create a custom VPC  
- Design and configure multiple subnets  
- Understand AWS‑reserved IP addresses  
- Allocate and verify private IP addresses  
- Launch EC2 instances to observe IP allocation  

# 🛠️ Lab Steps (Checklist)

1. Create a custom VPC → VPC Console → Create VPC → VPC Only → Name: MySubnetLabVPC → CIDR: 10.0.0.0/16  
2. Create Public Subnet → Name: PublicSubnet-A → AZ: us-east-1a → CIDR: 10.0.1.0/24  
3. Create Private Subnet → Name: PrivateSubnet-B → AZ: us-east-1b → CIDR: 10.0.2.0/24  
4. Review AWS-reserved IPs → 5 reserved per subnet → usable range starts at .4  
5. Launch EC2 instance → VPC: MySubnetLabVPC → Subnet: PublicSubnet-A → Auto-assign Public IP ON  
6. Verify IP allocation → EC


<img width="975" height="109" alt="image" src="https://github.com/user-attachments/assets/34c31a26-5d45-4653-9e6f-77b2fe5797f2" />
<img width="975" height="230" alt="image" src="https://github.com/user-attachments/assets/02902410-c693-4df8-914d-eb6292ddede7" />
<img width="975" height="253" alt="image" src="https://github.com/user-attachments/assets/c20464c6-c933-4b6b-814e-dca29efac598" />
<img width="975" height="398" alt="image" src="https://github.com/user-attachments/assets/0a352b23-c51f-48d6-a597-01308d418fc6" />
<img width="975" height="113" alt="image" src="https://github.com/user-attachments/assets/2c439e62-b0f7-4630-96a2-adbde8c389bf" />
<img width="975" height="356" alt="image" src="https://github.com/user-attachments/assets/cc71d97f-6284-479f-be3f-31cf5c7e4990" />
## 📘 Takeaways

- Learned how to design and allocate IP ranges for a VPC  
- Understood subnet creation across different AZs  
- Discovered how AWS automatically reserves 5 IPs per subnet  
- Observed how EC2 instances receive private IP addresses  
- Built a foundation for advanced VPC networking (NAT, IGWs, routing)  


## ⚠️ Challenges Encountered

1 **Overlapping CIDR Blocks**  
- Invalid subnet creation due to overlapping or incorrect CIDR ranges.

2 **Incorrect Availability Zones**  
- Instances failed to launch when subnets and resources were placed in mismatched AZs.

3 **Misunderstanding Reserved IPs**  
- Users attempted to use AWS‑reserved IPs (.0, .1, .2, .3, .255).

4 **Missing IP Allocation**  
- Instances launched without receiving expected private IP addresses.

Instances launched without IPs when “Auto-assign Public IP” was off.

## 🧩 Solutions

###  Proper CIDR Planning
- Ensured subnet CIDRs fit inside the VPC  
- Used non‑overlapping ranges  

### Verified Availability Zones
- Checked available AZs before subnet creation  

###  Clarified Reserved IP Rules
- Used only valid EC2‑assignable IPs (10.0.1.4 → 10.0.1.254)  

###  Ensured IP Assignment
- Enabled Auto‑assign Public IP  
- Verified DHCP settings in the VPC  

