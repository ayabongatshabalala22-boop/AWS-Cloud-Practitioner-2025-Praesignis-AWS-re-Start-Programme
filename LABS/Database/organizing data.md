# 🟦 AWS DynamoDB Lab: Organizing Data

## 📘 Overview
This lab focuses on how DynamoDB organizes data using tables, items, attributes, primary keys, and indexes.  
You will learn how to design a table structure, choose the right key schema, insert and retrieve data efficiently, and understand how DynamoDB partitions and stores information for scalability.

This lab builds essential skills for designing NoSQL data models in AWS.

---

## 🛠️ Lab Objectives
- Understand how DynamoDB organizes data  
- Create a table with an effective key schema  
- Insert and retrieve structured data  
- Use sort keys to organize related items  
- Explore how DynamoDB partitions data  
- Learn when to use secondary indexes  

---

## 🚀 Lab Steps

### 1. Create a DynamoDB Table for Organized Data
- Open **DynamoDB Console → Tables → Create Table**  
- Table name: `Orders`  
- Partition key: `OrderID` (String)  
- Sort key: `CustomerID` (String)  
- Capacity mode: On‑demand  
- Create the table  

### 2. Insert Structured Items
- Use **Create Item** in the console  
- Add attributes such as:  
  - `OrderID: "1001"`  
  - `CustomerID: "C001"`  
  - `Product: "Laptop"`  
  - `Quantity: 1`  
  - `Status: "Shipped"`  

- Insert multiple items with the same `CustomerID` to demonstrate sorting  

### 3. Query Items by Partition Key
- Query using `OrderID`  
- Observe that DynamoDB returns all matching items  
- Sort key organizes items by `CustomerID`  

### 4. Query Items by Partition + Sort Key
- Query for a specific customer’s orders  
- Use conditions like `CustomerID > "C000"`  
- Observe how sort keys group related data  

### 5. Scan the Table
- Retrieve all items  
- Compare performance differences between Scan and Query  

### 6. Add a Global Secondary Index (GSI)
- Create GSI:  
  - Partition key: `CustomerID`  
  - Sort key: `Status`  
- Use GSI to retrieve all orders for a customer regardless of `OrderID`  

### 7. Explore Data Partitioning
- Review **Table → Partitions**  
- Observe how DynamoDB distributes data based on partition key values  
- Understand how even distribution improves performance  

# Task 1: Connect to the Command Host (Continued)

8. For **Connect to instance**, choose the **Session Manager** tab.

9. Choose **Connect** to open a terminal window.  
   **Note:** If the **Connect** button is not available, wait for a few minutes and try again.

10. To configure the terminal to access all required tools and resources, run the following command:

```bash
sudo su
cd /home/ec2-user/
# Task 2: Query the world database

In this task, you query the `world` database using various `SELECT` statements and database functions.

---

## Step 12: Show Existing Databases

To show the existing databases, enter the following command in the terminal:

```sql
SHOW DATABASES;
# Task 2: Query the world database (Continued)

---

## Step 16: Aggregate Population by Region

This query returns the total population for the *Australia and New Zealand* region using the `SUM()` function and `GROUP BY` clause:

```sql
SELECT Region, SUM(Population) 
FROM world.country 
WHERE Region = 'Australia and New Zealand' 
GROUP BY Region 
ORDER BY SUM(Population) DESC;
# Conclusion

👍 **Congratulations!** You have now successfully:

- Used the `GROUP BY` clause with the aggregate function `SUM()`
- Used the `OVER` clause with the `RANK()` window function

<img width="940" height="463" alt="image" src="https://github.com/user-attachments/assets/fc13ea54-74f7-4d85-af8a-c2a44f7fb65b" />
<img width="940" height="470" alt="image" src="https://github.com/user-attachments/assets/30d5e842-d9a9-4ca1-8dcf-5798191806c5" />
<img width="940" height="280" alt="image" src="https://github.com/user-attachments/assets/cc3bc41b-bf87-4ec1-914d-e5d053233285" />
<img width="940" height="405" alt="image" src="https://github.com/user-attachments/assets/2a11ee21-e746-41fb-98b5-abad1a8662e9" />
<img width="940" height="417" alt="image" src="https://github.com/user-attachments/assets/970c0717-f2ef-4288-a6f1-814f7906e778" />
<img width="940" height="275" alt="image" src="https://github.com/user-attachments/assets/228da1ed-5288-40fa-932b-9ac24276d868" />
<img width="940" height="370" alt="image" src="https://github.com/user-attachments/assets/93975d92-5cc3-4a9d-bdfb-cba90fb39025" />
<img width="940" height="523" alt="image" src="https://github.com/user-attachments/assets/3814effa-a0d7-46a6-87ed-e5f12d08e5f3" />
## ✅ Takeaways
- DynamoDB organizes data into **tables → items → attributes**  
- **Partition keys** determine item distribution across partitions  
- **Sort keys** group and order related items  
- **Query** is efficient because it targets specific keys  
- **Scan** reads the entire table and is less efficient  
- **Global Secondary Indexes (GSIs)** allow alternative query patterns  
- Good key design is essential for performance and scalability  

---

## ⚠️ Challenges

### 1. Choosing the Right Key Schema
- Difficulty deciding between partition‑only vs. partition + sort key  
- Poor key choice led to uneven data distribution  

### 2. Query Limitations
- Queries require the partition key  
- Users attempted to query by attributes not part of the key  

### 3. Understanding Indexes
- Confusion between GSI and LSI  
- Uncertainty about when to use each  

### 4. Partitioning Behavior
- Hard to visualize how DynamoDB distributes data  
- Uneven partition keys caused hot partitions  

---

## 🧩 Solutions

### Improved Key Schema Design
- Chose partition keys with high cardinality  
- Used sort keys to group related items logically  

### Corrected Query Patterns
- Used Query only with valid key attributes  
- Used Scan only when necessary  

### Clarified Index Usage
- GSIs allow querying by non‑key attributes  
- LSIs require the same partition key but different sort keys  

### Understood Partitioning
- Reviewed partition metrics in the console  
- Ensured partition keys were evenly distributed  

---

## 📌 Summary
This lab demonstrated how DynamoDB organizes data using keys, items, and partitions.  
You learned how to design tables, insert structured data, query efficiently, and use indexes to support additional access patterns.

