# AWS RDS (Relational Database Service) Service Notes
![Uploading image.png…]()

Amazon RDS is a **managed database service** that simplifies the setup, operation, and scaling of relational databases in the cloud.  
It manages administrative tasks like patching, backups, and scaling.

---

## 1. Core Concepts & Features

- **Managed Service**: AWS handles the underlying OS, database patching, backups, failure detection, and recovery.
- **Supported Engines**: RDS supports six popular database engines:
  - PostgreSQL
  - MySQL
  - MariaDB
  - Oracle
  - Microsoft SQL Server
  - Amazon Aurora (AWS's high‑performance, cloud‑native relational database)
- **Automated Backups**: Daily full snapshots + transaction logs enable **Point‑In‑Time Recovery (PITR)** (up to 35 days).
- **DB Subnet Group**: A collection of subnets (ideally spanning multiple AZs) designated for DB instances within a VPC. Used for placement during scaling or failover.

---

## 2. High Availability (Multi‑AZ Deployments)

Multi‑AZ provides **fault tolerance** and **high availability** for production workloads.

- **Synchronous Replication**: Data is synchronously replicated from primary to standby in a different AZ.
- **Automatic Failover**: If the primary fails, RDS flips the CNAME record to the standby replica automatically.
- **Disaster Recovery**: Standby replica is passive and cannot be used for read queries.

---

## 3. Performance & Scalability (Read Replicas)

Read Replicas increase read throughput and offload read‑heavy traffic.

- **Asynchronous Replication**: Data is asynchronously replicated from primary to replicas.
- **Cross‑AZ & Cross‑Region**: Replicas can be created in the same AZ, across AZs, or across Regions.
- **Read‑Only**: Replicas are read‑only copies of the data.
- **Scalability**: Replicas can be scaled independently and promoted to standalone primaries if needed.

---

## 4. Security & Access

- **VPC Placement**: RDS instances are typically deployed into private subnets for enhanced security.
- **Security Groups**: Control network access to DB instances (e.g., port `3306` for MySQL, `5432` for PostgreSQL).
- **Encryption at Rest**: Encrypt RDS instances and snapshots using **KMS**. Must be enabled at creation time.
- **Encryption in Transit**: Use **SSL/TLS** to encrypt data between applications and DB endpoints.

---

## 5. Aurora Specifics

Aurora is AWS's premium database engine offering **up to 5× MySQL performance** and **3× PostgreSQL performance** at a similar price point.

- **Storage Automation**: Aurora storage automatically scales from **10 GB up to 128 TB**.

•	Aurora Serverless: An on-demand, auto-scaling configuration for Aurora that starts up immediately and shuts down when not in use, ideal for infrequent or unpredictable workloads.
•	High Durability: Aurora uses a unique distributed, fault-tolerant storage system that transparently replicates data across 3 AZs with 6 total copies of your data.

