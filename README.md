# Elevated-Lab-Internship-Task7
Connect the MySQL database using python, mysql.connector module and execute the SQL query to analyse the data.
# Sales Analytics with MySQL and Python

This project demonstrates how to use Python to connect to a MySQL database, pull simple sales information (such as total quantity sold and total revenue), and visualize the results with a basic bar chart inside a Jupyter Notebook.

## Features

- Connect to MySQL from Python using `mysql-connector-python`
- Run SQL queries to aggregate sales data (by product)
- Load SQL results into a Pandas DataFrame
- Print sales summaries in the notebook
- Visualize total revenue by product using a bar chart (with Matplotlib)
- Save the chart as a PNG file

## Prerequisites

- Python 3.x
- MySQL Server (with a database and a `sales` table containing at least: `product`, `quantity`, and `price` columns)
- Jupyter Notebook

## Required Python Packages

Install these packages in your Jupyter Notebook or environment:

```bash
pip install mysql-connector-python pandas matplotlib
```

## Database Table Example

Your MySQL table should look like this:

| product   | quantity | price |
|-----------|----------|-------|
| Widget A  |    10    |  5.00 |
| Widget B  |     3    | 12.00 |
| ...       |   ...    |  ...  |

## Usage

1. **Open the Jupyter Notebook** provided in this repository (or create your own using the code snippets below).
2. **Set up your MySQL connection** by editing the host, user, password, and database fields.
3. **Run the notebook cells** to:
    - Connect to MySQL
    - Query the sales data
    - View and visualize the results

## Example Code

```python
import mysql.connector
import pandas as pd
import matplotlib.pyplot as plt

# Connect to MySQL
conn = mysql.connector.connect(
    host='localhost',         # Change as needed
    user='your_username',     # Change as needed
    password='your_password', # Change as needed
    database='your_database'  # Change as needed
)

# Query sales data
query = """
SELECT
    product,
    SUM(quantity) AS total_qty,
    SUM(quantity * price) AS revenue
FROM sales
GROUP BY product
"""
df = pd.read_sql(query, conn)

# Print results
print(df)

# Plot bar chart
df.plot(kind='bar', x='product', y='revenue', legend=False)
plt.ylabel('Revenue')
plt.title('Revenue by Product')
plt.tight_layout()
plt.show()

# Save chart (optional)
plt.figure()
df.plot(kind='bar', x='product', y='revenue', legend=False)
plt.ylabel('Revenue')
plt.title('Revenue by Product')
plt.tight_layout()
plt.savefig("sales_chart.png")
plt.close()

# Close connection
conn.close()
```

## Notes

- Make sure your MySQL server is running and accessible from your Python environment.
- Adjust table/column names in the SQL query if your schema is different.
- The code can be adapted for other SQL databases (such as SQLite or PostgreSQL) by changing the connector and connection logic.

