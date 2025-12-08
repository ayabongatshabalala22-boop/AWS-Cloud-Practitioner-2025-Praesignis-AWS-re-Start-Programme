# Amazon CloudWatch Service Notes

Amazon CloudWatch is a **monitoring and observability service** built for AWS resources and the applications you run on AWS.  
It provides data and actionable insights to monitor applications, respond to system‑wide performance changes, and optimize resource utilization.

---

## 1. Core Concepts & Terminology

- **Metrics**: Time‑ordered set of data points (e.g., EC2 CPU utilization, Lambda invocations, S3 bucket size).  
  - Default resolution: **1‑minute intervals**  
  - Detailed Monitoring: **1‑second intervals** (additional cost for some services like EC2)

- **Namespaces**: Containers for metrics, grouping them by service or application (e.g., `AWS/EC2`, `AWS/Lambda`, or custom namespaces).

- **Dimensions**: Attributes used to uniquely identify a metric (e.g., `InstanceId`, `FunctionName`).

- **Alarms**: Watches a single metric and performs an action when thresholds are met.  
  *Examples*: Send SNS notifications, trigger Auto Scaling, stop an EC2 instance.

---

## 2. CloudWatch Logs

Centralizes and stores log files from AWS services and applications.

- **Log Groups**: Collections of log streams with shared retention, monitoring, and access control.
- **Log Streams**: Sequences of log events from the same source (e.g., one EC2 instance or Lambda invocation).
- **Log Retention**: Configurable from **1 day to indefinite**.
- **Metric Filters**: Create custom metrics based on log patterns (e.g., count `"ERROR"` lines).
- **Log Insights**: Interactive query language for searching and analyzing log data efficiently.

---

## 3. CloudWatch Events / Amazon EventBridge

EventBridge (formerly CloudWatch Events) is a **serverless event bus** for connecting applications using AWS, SaaS, or custom events.

- **Event Bus**: Pipeline for events.
- **Rules**: Define criteria for routing events.
- **Targets**: AWS resources that respond to events (e.g., Lambda, SQS, EC2).
- **Schedules**: Run tasks on a schedule (cron‑like), triggering targets such as Lambda functions.

---

## 4. CloudWatch Dashboards

- **Customizable Visualization**: Create reusable visualizations of metrics and alarms.
- **Cross‑Service Visibility**: Combine data from multiple AWS services (EC2, RDS, Lambda) into a single dashboard.

---

## 5. Billing and Pricing

- **Basic Monitoring**: Free for most AWS services.
- **Additional Costs**:  
  - Detailed monitoring  
  - Custom metrics  
  - Log ingestion and retention beyond the free tier  
  Costs scale with usage volume.
