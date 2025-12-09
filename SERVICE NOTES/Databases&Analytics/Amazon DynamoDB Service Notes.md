# Amazon DynamoDB Service Notes
<img width="337" height="150" alt="image" src="https://github.com/user-attachments/assets/2e875bf2-e547-48e9-ad24-5a9327c631cb" />

Amazon DynamoDB is a **fully managed, serverless, NoSQL key‑value and document database service** designed for single‑digit millisecond performance at any scale.

---

## 1. Core Concepts & Terminology

- **NoSQL**: Non‑relational schema (no SQL queries, no joins). Designed for flexibility and massive horizontal scalability.
- **Tables**: Collections of items.
- **Items**: Analogous to a row in a relational database. A collection of attributes.
- **Attributes**: Analogous to a column in a relational database. Can be nested.
- **Primary Key**: Uniquely identifies each item in a table. The only required attribute.

---

## 2. Key Structure and Indexing

The **primary key** is essential for efficient data retrieval.

- **Partition Key (Hash Key)**:  
  A simple primary key. Data is distributed across partitions based on this key's hash value.  
  Good partition key design ensures even distribution of reads/writes.

- **Sort Key (Range Key)**:  
  A composite primary key (`Partition Key + Sort Key`). Items with the same partition key are grouped and sorted by the sort key.  
  Enables efficient range queries (e.g., *all orders for a user between date X and date Y*).

### Indexes

- **GSI (Global Secondary Index)**:  
  Partition key and sort key can differ from the table's primary key. Queries can span all partitions.  
  *Consistency*: Eventually consistent by default.

- **LSI (Local Secondary Index)**:  
  Shares the same partition key as the table but uses a different sort key. Queries restricted to a single partition key value.  
  *Consistency*: Always strongly consistent.

---

## 3. Operations & Consistency

DynamoDB is optimized for three main operations:

- **GetItem**: Retrieves a single item using its full primary key.
- **Query**: Retrieves items that share the same partition key, with optional filtering on the sort key.
- **Scan**: Retrieves all items in the table.  
  ⚠️ Avoid in production — inefficient, slow, and expensive.

### Read Consistency Models

- **Eventually Consistent Reads (Default)**:  
  Returns data from a replica immediately. Faster and cheaper, but may not reflect recent writes.

- **Strongly Consistent Reads**:  
  Returns the most up‑to‑date data, even if multiple replicas must be read. Slower and costs **2×** as much.

---

## 4. Pricing & Provisioned Throughput

DynamoDB offers two capacity modes:

- **Provisioned Mode (Standard)**  
  - You specify Reads Per Second (RCUs) and Writes Per Second (WCUs).  
  - Best for predictable workloads.  
  - **Definitions**:  
    - 1 RCU = 1 strongly consistent read per second (up to 4 KB item).  
    - 1 WCU = 1 write per second (up to 1 KB item).

- **On‑Demand Mode**  
  - Pay‑per‑request. No need to provision capacity.  
  - Ideal for unpredictable or spiky workloads.  
  - Costs more per request than well‑tuned provisioned capacity.

---

## 5. Security & Features

- **DynamoDB Streams**:  
  Time‑ordered sequence of item‑level modifications. Commonly used to trigger AWS Lambda functions in real time.

- **TTL (Time To Live)**:  
  Automatically deletes items after a specified timestamp. Useful for ephemeral data (e.g., session logs, temporary carts).

- **Encryption**:  
  All data encrypted at rest by default using **AWS KMS**. No user configuration required.
