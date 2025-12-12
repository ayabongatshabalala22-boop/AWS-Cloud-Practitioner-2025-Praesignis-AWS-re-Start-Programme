#  AWS Lambda Lab

##  Introduction
This lab introduces you to **AWS Lambda**, a serverless compute service that lets you run code without provisioning or managing servers.  
You will learn how Lambda functions work, how they integrate with other AWS services, and how to deploy and test your own function.

---

## Lab Objectives
- Understand the purpose and benefits of **serverless computing**  
- Create and configure an **AWS Lambda function**  
- Trigger Lambda using different event sources (API Gateway, S3, CloudWatch Events)  
- Explore Lambda **runtime environments** and **execution roles**  
- Test, monitor, and troubleshoot Lambda functions  
- Learn how Lambda scales automatically based on demand  

---

## 🛠️ Lab Steps
1. Navigate to **AWS Lambda Console**  
2. Create a new Lambda function  
3. Choose a runtime (Python, Node.js, etc.)  
4. Configure execution role (IAM role with basic Lambda permissions)  
5. Write or upload your function code  
6. Configure a trigger (API Gateway, S3 event, or manual test)  
7. Test the function using the built‑in test tool  
8. View logs in **CloudWatch Logs**  
9. Modify memory, timeout, and environment variables  
10. Deploy and retest  

---

## ✅ Takeaways
- Learned how to create and deploy a **serverless function**  
- Understood how Lambda integrates with other AWS services  
- Practiced configuring IAM roles and permissions  
- Explored logging and monitoring with **CloudWatch**  
- Observed how Lambda scales automatically without server management  
- Gained confidence in building event‑driven applications  

---

## 🧩 Challenges Encountered
- Incorrect IAM role permissions  
- Timeout errors due to long‑running code  
- Misconfigured event triggers  
- Missing environment variables  
- Errors not visible until checking CloudWatch logs  

---

## 🧩 Solutions
- Assign correct IAM policies (AWSLambdaBasicExecutionRole)  
- Increase function timeout in configuration  
- Re‑check event source mapping or API Gateway integration  
- Add required environment variables in Lambda settings  
- Use CloudWatch Logs to debug and trace issues  

---

 <img width="940" height="483" alt="image" src="https://github.com/user-attachments/assets/a669063a-d2a9-4071-a80c-b14f50d287bb" />
<img width="940" height="523" alt="image" src="https://github.com/user-attachments/assets/b839d1d7-feeb-47c8-96db-156f184a0009" />
<img width="940" height="486" alt="image" src="https://github.com/user-attachments/assets/3ee10ef5-df05-46d0-8b50-76defd2f0371" />
<img width="940" height="481" alt="image" src="https://github.com/user-attachments/assets/d595589c-0441-4133-8a8f-7ab27e49b057" />
<img width="940" height="452" alt="image" src="https://github.com/user-attachments/assets/d723119c-82e0-42f6-a4ab-e71ec3eecd76" />
<img width="940" height="486" alt="image" src="https://github.com/user-attachments/assets/b46ca015-75e2-4d16-85d8-70d4950ec8b0" />

##  Conclusion
successfully built a production-style workflow for **AWS Lambda**: authoring a Python function, assigning least-privilege IAM, configuring environment variables, testing invocations, wiring API Gateway, and managing versions with aliases.  



 
