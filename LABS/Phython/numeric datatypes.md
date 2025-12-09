🧮 Numeric Datatypes Lab

Introduction to Numeric Types in Programming (Beginner-Friendly)

This lab helps you understand and practice working with numeric datatypes commonly used in programming and databases. You’ll learn how integers, floating-point numbers, and decimals behave, how they differ, and when to use each one.

🎯 Lab Objectives

By the end of this lab, you will be able to:

Understand the difference between INT, FLOAT, and DECIMAL datatypes

Perform basic operations on numeric values

Identify which datatype is appropriate for different use cases

Experiment with precision, rounding, and arithmetic behavior

🧪 Lab Tasks
Task 1 — Understanding Numeric Datatypes
1️⃣ Integer (INT)

Stores whole numbers

No decimals

Example: 10, -4, 5000

2️⃣ Floating Point (FLOAT / DOUBLE)

Stores decimal values

Not always 100% precise (because binary representation)

Example: 3.14, 0.0004

3️⃣ Decimal (DECIMAL / NUMERIC)

Exact precision

Best for money, banking, and financial data

Example: DECIMAL(10,2) → 1245.50

Task 2 — Try Creating Numeric Variables

Below is example syntax in different languages.
Choose any language you like for your GitHub repo.

Python Example
# Integer
x = 10  
print(type(x), x)

# Float
y = 3.14
print(type(y), y)

# Decimal (with precise math)
from decimal import Decimal
z = Decimal("10.25") + Decimal("2.30")
print(type(z), z)

SQL Example
CREATE TABLE numeric_demo (
    quantity INT,
    price FLOAT,
    total_amount DECIMAL(10,2)
);

INSERT INTO numeric_demo VALUES
(5, 12.50, 62.50);

Task 3 — Observe Precision Differences
FLOAT can behave strangely:
print(0.1 + 0.2)


Output might be:

0.30000000000000004

DECIMAL stays accurate:
from decimal import Decimal
print(Decimal("0.1") + Decimal("0.2"))


Output:

0.3

🧠 Real-World Use Cases
Datatype	Best Use Case
INT	Counting items, IDs, ages, quantities
FLOAT	Scientific math, measurements, sensor data
DECIMAL	Money, finance, billing, pricing
🚧 Challenges You Might Face
❗ Challenge 1: FLOAT rounding issues

Calculations may not give exact results

Example: 0.1 + 0.2 != 0.3

❗ Challenge 2: Choosing the correct datatype

Using FLOAT for money will cause rounding errors

Using DECIMAL everywhere can be slower

❗ Challenge 3: Overflow

INT too small for big values

DECIMAL needs correct precision (p,s) settings

✅ Solutions / What You Learned
✔ Use INT for whole numbers
✔ Use DECIMAL for accurate financial values
✔ Use FLOAT only when small precision errors don’t matter
✔ Test your numeric values before using them in production
✔ Understand how precision works to avoid common bugs
🎉 Conclusion

You now understand:

The difference between INT, FLOAT, and DECIMAL

How numeric precision works

When to use each datatype

Common issues and how to avoid them

This is an essential skill for anyone learning programming, SQL, or cloud platforms like AWS and Python.
<img width="940" height="208" alt="image" src="https://github.com/user-attachments/assets/6af05883-a918-433d-8ecb-b1208bdc7c98" />
<img width="940" height="444" alt="image" src="https://github.com/user-attachments/assets/e1a90813-80f0-4c4c-bb13-82f983b80949" />
<img width="940" height="183" alt="image" src="https://github.com/user-attachments/assets/3166bd32-38d3-4887-b514-b9de315c2d4b" />
<img width="940" height="553" alt="image" src="https://github.com/user-attachments/assets/b8118630-579a-42dc-8059-6e882fb35402" />
<img width="940" height="353" alt="image" src="https://github.com/user-attachments/assets/e35ef4d4-12d7-4c63-a55e-e0e09adffe78" />
<img width="940" height="520" alt="image" src="https://github.com/user-attachments/assets/3da7b3d4-1f27-4b8f-9953-f8e923a4d13e" />
<img width="940" height="533" alt="image" src="https://github.com/user-attachments/assets/5b2f1567-3b79-408e-a184-c2188b1d375e" />

