# Amazon EC2 (Elastic Compute Cloud) Service Notes

EC2 provides resizable compute capacity in the cloud, acting as the fundamental **virtual server** building block of AWS.

---

## 1. Core Concepts

- **Instances**: Virtual servers running in the AWS cloud.
- **AMIs (Amazon Machine Images)**: Templates containing the software configuration (OS, application server, applications) required to launch an instance.
- **Security Groups**: Virtual firewalls at the instance level, controlling inbound and outbound traffic. They are **stateful**.
- **EBS (Elastic Block Store) Volumes**: Persistent block-level storage volumes for use with EC2 instances. These volumes persist independently from the life of an instance.
- **Instance Metadata / User Data**:
  - **User Data**: A script run only once when the instance is first launched, typically used for bootstrapping (installing software, updating, etc.).
  - **Metadata**: Information about the instance itself (e.g., public IP, instance ID, security credentials) accessible from within the running instance.

---

## 2. EC2 Instance Types

Instances are categorized based on their primary use case, represented by a **letter code** and **generation number** (e.g., `t2.micro`).

- **T-Type (Burstable)**  
  Ideal for general-purpose workloads with baseline performance and the ability to "burst" above the baseline.  
  *Example*: `t2.micro` — good for test/dev environments.

- **M-Type (General Purpose)**  
  Balanced CPU and memory resources. Suitable for most general application workloads.

- **C-Type (Compute Optimized)**  
  Designed for high computational loads requiring more CPU power.  
  *Use cases*: scientific computing, batch processing.

- **R/X-Type (Memory Optimized)**  
  Provides higher RAM for memory-intensive applications.  
  *Use cases*: databases, in-memory caches.
