# ☁️ AWS DynamoDB Lab: Table Operations

## 📖 Overview
This lab demonstrates a step by step walk in on  how to create, query, update, and delete items in an **Amazon DynamoDB table** using the AWS CLI. It’s designed for cloud practitioners who want hands‑on experience with AWS database services.

---

## 🎯 Learning Objectives
- Create a DynamoDB table with a primary key.
- Insert items into the table.
- Query and scan data.
- Update and delete items.
- Clean up resources to avoid charges.

## 🚀 Lab Steps

### 1. Create a DynamoDB Table
- Open DynamoDB Console → Tables → Create Table  
- Enter table name (e.g., `Students`)  
- Define partition key (e.g., `StudentID` as String)  
- Optionally add a sort key  
- Choose On‑demand capacity mode  
- Create the table  

### 2. Insert Items into the Table
- Use **Create Item** in the console to add attributes  
- Or use AWS CLI with `put-item` to insert data  

### 3. Query the Table
- Query using the partition key  
- Optionally filter using sort key conditions  
- Use AWS CLI with `query` for key‑based lookups  

### 4. Scan the Table
- Retrieve all items in the table  
- Use AWS CLI with `scan` for full table reads  

### 5. Update an Item
- Modify attributes using update expressions  
- Use AWS CLI with `update-item`  

### 6. Delete an Item
- Remove specific items using the console or CLI  
- Use AWS CLI with `delete-item`  

### 7. Delete the Table
- Select the table → Delete Table  
- Confirm deletion  

<img width="975" height="430" alt="image" src="https://github.com/user-attachments/assets/b6c943c8-dc69-48ca-be74-335c2e2dc7e7" />
<img width="975" height="380" alt="image" src="https://github.com/user-attachments/assets/972068d5-acf4-463b-80e2-68d45c177bcb" />
<img width="950" height="425" alt="image" src="https://github.com/user-attachments/assets/d0844023-bdf5-4a2b-a67c-6f46e74b0702" />
<img width="975" height="383" alt="image" src="https://github.com/user-attachments/assets/52895a3f-f572-4ef3-bb07-acbc0166f364" />
<img width="975" height="392" alt="image" src="https://github.com/user-attachments/assets/05febb82-bd6b-43ec-91a6-88e862fa9f55" />
<img width="975" height="375" alt="image" src="https://github.com/user-attachments/assets/ea3fb1f7-ec54-40ca-b902-56d69257723e" />
<img width="975" height="423" alt="image" src="https://github.com/user-attachments/assets/707247ce-2fdf-4fe6-90c2-983e2e31af89" />
<img width="975" height="405" alt="image" src="https://github.com/user-attachments/assets/41607a43-2f92-43ba-bbd0-ea5e9dd95755" />
<img width="975" height="416" alt="image" src="https://github.com/user-attachments/assets/e17603cc-5368-41a8-a574-017782238cea" />
<img width="975" height="427" alt="image" src="https://github.com/user-attachments/assets/4b2f46f3-4916-4530-babf-5d04e3c6d06c" />
## ✅ Takeaways

- Learned how to create a DynamoDB table with partition and optional sort keys  
- Understood the difference between Query (key‑based) and Scan (full table read)  
- Practiced inserting, updating, and deleting items using both console and CLI  
- Gained experience with DynamoDB’s JSON‑like attribute structure and data types  
- Saw how update expressions modify specific attributes without replacing the whole item  
- Learned how on‑demand capacity mode simplifies scaling and cost management  
- Understood how DynamoDB enforces strict typing (S, N, BOOL, etc.)  
- Became familiar with common CLI commands: `put-item`, `query`, `scan`, `update-item`, `delete-item`  
## ⚠️ Challenges

### 1. Understanding Primary Keys
- Confusion between partition key and sort key  
- Difficulty querying without the correct key structure  

### 2. CLI Syntax Errors
- JSON formatting mistakes caused command failures  
- Missing braces, quotes, or incorrect attribute types  

### 3. Query vs Scan Confusion
- Query requires a partition key  
- Scan reads the entire table, leading to slower performance  

### 4. Attribute Type Mismatches
- DynamoDB requires explicit types (S, N, BOOL, etc.)  
- Incorrect types caused validation errors  

---

## 🧩 Solutions

### Clarified Key Structure
- Reviewed how partition keys determine item placement  
- Used sort keys for more precise queries when needed  

### Fixed CLI Formatting Issues
- Ensured proper JSON structure in CLI commands  
- Validated commands before execution  

### Understood Query vs Scan
- Used Query for efficient key‑based lookups  
- Used Scan only when full table reads were necessary  

### Corrected Attribute Types
- Ensured all attributes used correct DynamoDB data types  
- Matched each value with its required type (S, N, BOOL, etc.)  

