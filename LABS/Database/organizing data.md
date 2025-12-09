# Scenario

The database operations team has created a relational database named `world` containing three tables: `city`, `country`, and `countrylanguage`. You help write a few queries to group records for analysis by using both the `GROUP BY` and `OVER` clauses.

---

# Lab Overview and Objectives

This lab demonstrates how to use some common database functions with the `GROUP BY` and `OVER` clauses.

After completing this lab, you should be able to:

- Use the `GROUP BY` clause with the aggregate function `SUM()`
- Use the `OVER` clause with the `RANK()` window function
- Use the `OVER` clause with the aggregate function `SUM()` and the `RANK()` window function

When you start the lab, the following resources are already created for you:

---

# Task 1: Connect to the Command Host

In this task, you connect to an instance containing a database client, which is used to connect to a database. This instance is referred to as the **Command Host**.

1. In the AWS Management Console, choose the **Services** menu. Under **Compute**, choose **EC2**.
2. In the navigation pane, choose **Instances**.
# Task 1: Connect to the Command Host (Continued)

7. Next to the instance labelled **Command Host**, select the check box ☑ and then choose **Connect**.  
   **Note:** If you do not see the **Command Host**, the lab is possibly still being provisioned, or you may be using another Region.

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

