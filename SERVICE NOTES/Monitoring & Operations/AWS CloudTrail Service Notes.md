# AWS CloudTrail Service Notes
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/40704dec-dd53-4731-9092-24703209e6a7" />

AWS CloudTrail is a service that enables **governance, compliance, operational auditing, and risk auditing** of your AWS account.  
It provides a history of AWS API calls, including **who made the call, when, from which IP address, and which resources were affected**.

---

## 1. Core Concepts & Terminology

- **API Activity Focus**: Records API calls (actions performed by users, roles, or AWS services).  
  ⚠️ Does *not* monitor network traffic or data plane operations within a VPC (that’s handled by **VPC Flow Logs**).
- **Event**: A record of an activity or API call in AWS. Includes caller identity, time, source IP, request parameters, and response elements.
- **Trails**: Configuration that determines where CloudTrail sends event records (commonly to an **S3 bucket**, optionally to **CloudWatch Logs**).
- **Event History**: Console feature showing the past **90 days of management events** in your AWS account.

---

## 2. Event Types

CloudTrail captures two main types of events:

### A. Management Events (Default)
- Records **management operations** performed on AWS resources.  
- **Examples**:  
  - Launching an EC2 instance (`RunInstances`)  
  - Creating an S3 bucket (`CreateBucket`)  
  - Changing IAM permissions (`AttachRolePolicy`)  
- Enabled by default in **Event History**.

### B. Data Events (Optional, Additional Cost)
- Records **data plane operations** and resource activities.  
- High‑volume, disabled by default.  
- **Examples**:  
  - S3 object‑level APIs (`GetObject`, `PutObject`, `DeleteObject`)  
  - Lambda function invoke APIs (`InvokeFunction`)  
  - DynamoDB item‑level APIs (`PutItem`, `GetItem`, `DeleteItem`)  

---

## 3. Configuration & Delivery

- **S3 Bucket Delivery**: Standard long‑term storage destination for CloudTrail logs. Delivered within ~15 minutes of the API call.  
- **Log File Integrity Validation**: Ensures logs are not tampered with after delivery to S3.  
- **CloudWatch Logs Integration**: Send events to CloudWatch Logs for real‑time analysis, searching, and alarms.  
  *Example*: Trigger an alarm when `DeleteTable` is called on a critical DynamoDB table.

---

## 4. Key Use Cases and Best Practices

- **Security Analysis & Auditing**: Identify who deleted a resource or modified permissions.  
- **Compliance**: Meet regulatory requirements (HIPAA, PCI‑DSS, GDPR).  
- **Operational Troubleshooting**: Pinpoint exact API call failures causing application issues.  
- **Best Practice – Global Trail**:  
  Create one **multi‑region trail** that logs all activity globally and delivers logs to a single, dedicated S3 bucket in a separate, locked‑down AWS account.  
- **Insights Events**: Detect unusual activity or high‑volume error rates in API usage (additional cost feature).
