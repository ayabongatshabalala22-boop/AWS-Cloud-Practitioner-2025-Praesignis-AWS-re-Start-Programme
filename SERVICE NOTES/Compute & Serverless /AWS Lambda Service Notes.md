# AWS Lambda Service Notes
<img width="313" height="198" alt="image" src="https://github.com/user-attachments/assets/d392fcc8-cbc8-4a03-b2d9-03fcfcf72e06" />

AWS Lambda is a **serverless compute service** that runs your code in response to events without requiring you to provision or manage servers. It is the core of *serverless architecture* on AWS.

---

## 1. Core Concepts & Terminology

- **Function**: The primary resource in Lambda; your code snippet (e.g., Python, Node.js, Java) that is executed.
- **Event Source**: The AWS service or custom application that triggers the Lambda function (e.g., S3 PUT event, API Gateway request, CloudWatch schedule).
- **Execution Role (IAM Role)**: Permissions that the Lambda function assumes when it runs. Dictates which AWS services the function can interact with (e.g., writing logs to CloudWatch, reading from DynamoDB).
- **Trigger**: Configuration connecting an event source to a Lambda function.
- **Cold Start**: Delay experienced when a Lambda function is invoked after being idle, as AWS spins up the underlying container.
- **Provisioned Concurrency**: Keeps functions initialized and ready to respond in milliseconds, mitigating cold starts for latency‑sensitive applications.

---

## 2. Execution & Runtime Model

- **Stateless**: Functions should be stateless. Persistent data should be stored in S3, DynamoDB, or RDS.
- **Environment Variables**: Store configuration settings, database connection strings, or feature flags without hardcoding them.
- **Ephemeral Disk Space (`/tmp`)**: Temporary writable disk space (up to 10 GB) available only during execution.
- **Time Limit (Timeout)**: Maximum execution time is **15 minutes (900 seconds)**.

---

## 3. Pricing Model

Lambda is cost‑effective because you pay only for the precise execution time consumed.

- **Requests**: Billed per million requests.
- **Duration**: Billed in 1 ms increments, measured from start until termination.
- **Free Tier**: Includes ~1 million free requests per month.

---

## 4. Integration Points (Event Sources)

Lambda integrates deeply with AWS services. Common integrations include:

- **API Gateway**: Builds serverless APIs by triggering Lambda functions for HTTP requests (GET, POST, etc.).
- **S3**: Trigger functions on object events (PUT, DELETE).
- **CloudWatch Events / Schedules**: Run functions on cron‑like schedules.
- **DynamoDB Streams**: React to database changes in real time.

•	Layers: Allows you to manage shared code, libraries, and custom runtimes separately from your main function logic. This keeps deployment packages small and promotes code reuse.
•	Monitoring: All logs are automatically sent to Amazon CloudWatch Logs. Metrics are sent to Amazon CloudWatch.
•	VPC Configuration: Lambda functions can be deployed inside a VPC to access private resources (like an RDS database), but this requires careful configuration of ENIs (Elastic Network Interfaces) and security groups.
•	Versioning and Aliases: Manage different versions of your code (e.g., $LATEST, version 1) and use aliases (e.g., PROD, BETA) to route traffic to specific versions, enabling safe deployments and rollbacks.

