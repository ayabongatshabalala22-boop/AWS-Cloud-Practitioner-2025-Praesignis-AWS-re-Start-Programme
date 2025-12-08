# 📘 Amazon CloudFront Service Notes
<img width="1536" height="1024" alt="Copilot_20251208_035410" src="https://github.com/user-attachments/assets/487c8792-5452-484b-b9be-fcb57fa164b2" />


Amazon CloudFront is a **fast content delivery network (CDN)** service that securely delivers data, videos, applications, and APIs to customers globally with **low latency** and **high transfer speeds**.

---

## 1. 🔑 Core Concepts & Terminology

- **CDN (Content Delivery Network):** A geographically distributed network of proxy servers and data centers.  
- **Edge Location (POP – Point of Presence):** Global data centers where CloudFront caches copies of your content. Requests are routed to the nearest edge location.  
- **Origin:** The source of the content that the CDN distributes. This can be an Amazon S3 bucket, an EC2 instance, an Elastic Load Balancer, or any external custom HTTP server.  
- **Distribution:** The primary CloudFront configuration entity. It manages how content is delivered from your origins to your users.  
- **Cache Hit Ratio:** The percentage of requests that are served directly from the edge cache, improving performance and reducing load on your origin server.  

---

## 2. ⚙️ Key Features and Operation

### How CloudFront Works
1. A user requests a file (e.g., `image.jpg`) from your website.  
2. The DNS routes the request to the nearest CloudFront edge location.  
3. The edge location checks its cache for the file.  
   - **Cache Hit:** The file is immediately returned to the user (low latency).  
   - **Cache Miss:** The edge location retrieves the file from the Origin (e.g., S3 or EC2).  
4. The file is returned to the user and cached at the edge location for future requests.  

### Caching and TTL (Time To Live)
- **Default TTL:** CloudFront typically uses the origin's cache-control headers. If none are present, the default is 24 hours.  
- **Invalidation:** You can manually clear cached content across all edge locations before the TTL expires if you need to update a file immediately (e.g., deploying a new logo).  

---

## 3. 🔒 Security and Optimization

- **HTTPS Support:** CloudFront supports end-to-end encryption (Viewer Protocol Policy and Origin Protocol Policy).  
- **OAI (Origin Access Identity) / OAC (Origin Access Control):** A virtual user identity used to securely restrict access to an S3 bucket. Prevents users from bypassing CloudFront and accessing S3 content directly. OAC is the modern, preferred method.  
- **AWS WAF (Web Application Firewall):** Integrate WAF with CloudFront distributions to protect against common web exploits (SQL injection, XSS).  
- **Geo-Restriction:** Block users from specific geographic locations from accessing your content.  

---

## 4. 💰 Price Classes

CloudFront uses a global network architecture and prices based on the geographic region where the data is served.  

| Price Class | Coverage | Use Case |
|-------------|----------|----------|
| **All (Recommended)** | All global edge locations | Best performance |
| **200** | Most locations (excludes some latency-sensitive regions like Australia, South America, Asia) | Lower cost |
| **100** | Only cost-effective North American and European locations | Lowest cost |

---

## 5. 🌐 Integration with Route 53

- A **Route 53 Alias Record** maps your domain name (e.g., `www.example.com`) to your CloudFront distribution domain name (e.g., `d1234abcd.cloudfront.net`).  

---

## 📊 CloudFront Workflow Diagram

![Amazon CloudFront Workflow](cloudfront-workflow-diagram.png)
