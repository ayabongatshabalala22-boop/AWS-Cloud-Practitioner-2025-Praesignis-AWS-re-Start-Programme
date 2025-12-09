# AWS VPC (Virtual Private Cloud) Service Notes
<img width="178" height="198" alt="image" src="https://github.com/user-attachments/assets/9d731388-b8d0-4eb8-b5b5-30e475296c23" />

AWS VPC provides a **private, isolated section** of the AWS Cloud where you can launch AWS resources in a virtual network that you define.  
It is the fundamental networking service in AWS.

---

## 1. Core Concepts & Terminology

- **VPC**: Your private virtual network boundary within a Region.
- **CIDR (Classless Inter‑Domain Routing)**: Notation used to define IP address ranges for your VPC and subnets (e.g., `10.0.0.0/16`).
- **Subnet**: A subdivision of a VPC's IP address range. Subnets are tied to a single Availability Zone (AZ).
  - **Public Subnet**: Routed to the Internet via an Internet Gateway (IGW). Resources here are publicly accessible.
  - **Private Subnet**: Not routed to the IGW. Resources here are private and must use a NAT Gateway (NAT GW) or NAT Instance to reach the internet.
- **Internet Gateway (IGW)**: A horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet.
- **Route Table**: A set of rules (routes) used to determine where network traffic is directed. Each subnet must be associated with one route table.

---

## 2. Security Layers

VPCs use two distinct layers of security controls:

### A. Security Groups (SG)
- **Instance Level**: Acts as a virtual firewall for a single EC2 instance (or group of instances).
- **Stateful**: If inbound traffic is allowed, outbound response traffic is automatically allowed.
- **Allow Rules Only**: You cannot explicitly deny traffic within an SG rule; you only allow specific ports/IPs.

### B. Network ACLs (NACLs)
- **Subnet Level**: Acts as a firewall for an entire subnet.
- **Stateless**: You must explicitly allow both inbound and outbound traffic rules.
- **Allow and Deny Rules**: You can create both ALLOW and DENY rules.
- **Ordered Evaluation**: Rules are evaluated by number, starting with the lowest. The first matching rule is applied immediately.

---

## 3. Connectivity & Advanced Topics

- **NAT Gateway (NAT GW)**:  
  Used by instances in private subnets to initiate outbound traffic to the internet while preventing inbound internet traffic.  
  Requires an Elastic IP and resides in a public subnet.

- **VPC Peering**:  
  Connects two VPCs together privately using a direct network link. Instances behave as if they are on the same network.  
  *Note*: Peering is **non‑transitive** (VPC A ↔ B and B ↔ C does not mean A ↔ C).

- **VPC Endpoints**:  
  Enables private connectivity to supported AWS services (like S3, DynamoDB) without using an Internet Gateway or NAT gateway. Traffic stays within the AWS network.  
  - **Interface Endpoints**: Uses an Elastic Network Interface (ENI) with private IPs (most services).  
  - **Gateway Endpoints**: For S3 and DynamoDB only; uses a route table entry.

- **Site‑to‑Site VPN**:  
  Connects your on‑premises data center to your VPC via a secure tunnel. Requires a **Customer Gateway (CGW)** device on‑premises and a **Virtual Private Gateway (VGW)** on AWS.
