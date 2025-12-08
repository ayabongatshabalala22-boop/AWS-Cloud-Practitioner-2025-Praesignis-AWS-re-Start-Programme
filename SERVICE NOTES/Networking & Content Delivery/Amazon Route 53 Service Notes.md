# 📘 Amazon Route 53 Service Notes
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/619e46a3-9553-49b8-a95e-11e6f6330240" />

Amazon Route 53 is a **highly available and scalable cloud Domain Name System (DNS)** web service.  
It translates human-readable domain names (like `example.com`) into machine-readable IP addresses (like `192.0.2.1`).

---

## 1. 🔑 Core Concepts & Terminology

- **DNS:** The "phonebook of the internet," linking domain names with IP addresses.  
- **Domain Name Registrar:** Route 53 can act as a registrar to purchase and manage domain names directly.  
- **Hosted Zone:** A container for records that manage traffic for a specific domain (e.g., `example.com`).  
  - Public Hosted Zones  
  - Private Hosted Zones  
- **Record Set (Records):** Entries within a Hosted Zone that define how traffic is routed.  

### Common Record Types
- **A (Address):** Maps a domain name to an IPv4 address.  
- **AAAA (Quad A):** Maps a domain name to an IPv6 address.  
- **CNAME (Canonical Name):** Maps one domain name to another (e.g., `blog.example.com` → load balancer URL).  
  - Note: CNAMEs cannot be used for naked domains (`example.com` must use A record or ALIAS).  
- **NS (Name Server):** Specifies authoritative name servers (created automatically).  
- **MX (Mail Exchange):** Specifies mail servers for handling email.  
- **TXT (Text):** Used for verification (e.g., SPF records for email validation).  

---

## 2. ⚙️ Alias Records (AWS Specific)

Alias records are an AWS-specific extension of standard DNS records.

- **Functionality:** Behaves like a CNAME but works for root/naked domains (e.g., `example.com`).  
- **AWS Resources Only:** Alias records can point to:  
  - Elastic Load Balancers (ELBs)  
  - CloudFront Distributions  
  - S3 Buckets (static website hosting)  
  - Other Route 53 records  
- **Key Advantage:**  
  - Automatically handle IP address changes of AWS resources.  
  - Free of charge for DNS queries.  

---

## 3. 🌍 Routing Policies

Route 53 supports advanced routing beyond simple A/CNAME lookups:

- **Simple Routing:** Default policy, routes traffic to a single resource.  
- **Weighted Routing:** Distribute traffic among multiple resources by weight (e.g., 80% US, 20% EU). Useful for A/B testing or blue/green deployments.  
- **Latency-Based Routing (LBR):** Routes requests to the AWS region with the lowest latency.  
- **Geolocation Routing:** Routes traffic based on the user’s geographic location (e.g., Germany → German-localized site).  
- **Failover Routing:** Primary/Secondary setup. Health checks monitor the primary; traffic fails over to secondary if unhealthy.  
- **Multi-Value Answer Routing:** Returns multiple IP addresses to improve availability (works with health checks).  

---

## 4. 🩺 Health Checks

Route 53 Health Checks monitor endpoint health and performance:

- Can check endpoints by IP address or domain name.  
- Can monitor other Route 53 records or AWS resources via CloudWatch alarms.  
- **Essential for Failover Routing:** Health checks are mandatory for reliable failover setups.  

---

## 📊 Route 53 Overview Diagram

![Amazon Route 53](route53-diagram.png)
