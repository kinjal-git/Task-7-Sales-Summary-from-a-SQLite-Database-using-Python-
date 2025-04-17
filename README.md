# Task-7-Sales-Summary-from-a-SQLite-Database-using-Python-
The goal is to use SQL inside Python to pull **simple sales info (like total quantity sold, total revenue)**, and display it using a simple **bar chart**.

---

## 🧰 Tools Used
1. Jupyter Notebook
2. SQL inside Python using SQLite

---

## 📊 Objectives
1. Create a database.
2. Create a table and insert values into it.
3. Pull out basic information from the table, like total quantity sold and total revenue.
4. Display the information using a simple bar chart.

---

## 📝 Python Script
```python
# Importing Libraries

import sqlite3
import pandas as pd
import matplotlib.pyplot as plt

# Establishing a connection

conn = sqlite3.connect("sales_data.db")

cur = conn.cursor()

# Creating a table

table1 = """CREATE TABLE IF NOT EXISTS
TOTAL_SALES(customer_id INTEGER PRIMARY KEY, product TEXT, total_quantity INTEGER, item_price FLOAT)"""

cur.execute(table1)

# Insert values

cur.execute("INSERT INTO TOTAL_SALES VALUES (1584, 'Coffee beans', 5, 10.56)")
cur.execute("INSERT INTO TOTAL_SALES VALUES (1654, 'Complan', 8, 60.50)")
cur.execute("INSERT INTO TOTAL_SALES VALUES (1789, 'Baby Milk', 9, 40.70)")
cur.execute("INSERT INTO TOTAL_SALES VALUES (1463, 'Apple', 10, 30.00)")
cur.execute("INSERT INTO TOTAL_SALES VALUES (1963, 'Sugar', 15, 15.50)")
cur.execute("INSERT INTO TOTAL_SALES VALUES (1328, 'Candy', 7, 6.58)")
cur.execute("INSERT INTO TOTAL_SALES VALUES (1234, 'Protein Shake', 16, 180.60)")
cur.execute("INSERT INTO TOTAL_SALES VALUES (1462, 'Biscuits', 4, 50.40)")
cur.execute("INSERT INTO TOTAL_SALES VALUES (1892, 'Cookies', 6, 70.50)")
cur.execute("INSERT INTO TOTAL_SALES VALUES (1336, 'Cake', 2, 140.50)")

# Getting results

results = "SELECT * FROM TOTAL_SALES"

df1 = pd.read_sql_query(results, conn)

print(df1)

# Getting results of a specific query

query = "SELECT product, SUM(total_quantity) AS total_qty, SUM(total_quantity * item_price) AS revenue FROM TOTAL_SALES GROUP BY product"

df = pd.read_sql_query(query, conn)

print(df)

# Bar Chart (Product Vs Revenue)

df.plot(kind = 'bar', x = 'product', y = 'revenue')
```

---

## 📂 Files Included
1. `sales_data.db`: Database created.
2. `sales_data.db-journal`: Journal of the Database created.
3. `Sales Summary using SQLite Database.ipynb`: Python Notebook of the script.
4. `Sales_Chart.png`: Bar Chart of the results.
5. `README.md`: This file.
